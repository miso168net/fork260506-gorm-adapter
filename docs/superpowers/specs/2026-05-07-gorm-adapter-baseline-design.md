# Feature Specification: gorm-adapter Baseline Reference

**Feature Branch**: `001-baseline-reference`
**Created**: 2026-05-07
**Status**: Draft
**Type**: Reverse-engineered baseline spec (not a new feature)
**Baseline target**: `master @ bc66b93` (2022-11-27, "Update go.mod") — the last
upstream-derived commit before this fork's infrastructure-only commits.

> **About this document.** This spec captures the *current* behaviour of
> `github.com/go-admin-team/gorm-adapter/v3` so future changes have a written
> reference point. It deliberately uses the SpecKit `spec-template.md`
> structure with two terminology adaptations: "User Scenarios" → "Usage
> Scenarios" (no end-users; consumers are Go programs) and "Functional
> Requirements" → "Adapter Contract" (the library's exposed obligations
> rather than feature requirements). "Success Criteria" is repurposed to
> "Library Quality Outcomes" since there is no implementation work being
> proposed.

## Usage Scenarios & Testing *(mandatory)*

### Usage Scenario 1 — Persist Casbin policy to a relational database (Priority: P1)

A Go service uses Casbin for authorization and needs its policy rules stored in
the same database as its application data. The service constructs an Adapter
from a driver name and DSN, hands it to `casbin.NewEnforcer`, and from that
point on `enforcer.LoadPolicy()` / `SavePolicy()` round-trip rules through the
`casbin_rule` table without the application code knowing about Gorm.

**Why this priority**: This is the entry use case the README leads with and
the path the largest share of `TestAdapters` exercises. It is the contract on
which every other usage builds.

**Independent test**: Build a fresh Adapter against any single supported
driver, load a small `rbac_model.conf` policy, save, reload, and assert the
loaded policy equals the saved policy. Equivalent to running
`testGetPolicy` / `testAutoSave` for that driver.

**Acceptance Scenarios** (existing behaviour — what already works):

1. **Given** a clean MySQL/PostgreSQL/SQL Server/SQLite3 database, **When** a
   caller invokes `NewAdapter(driverName, dataSourceName)` and uses the result
   in `casbin.NewEnforcer`, **Then** the adapter creates the database (where
   driver semantics permit), creates the `casbin_rule` table, and the
   resulting enforcer can `LoadPolicy()` returning an empty model.
2. **Given** an enforcer wired to the adapter, **When** the caller adds rules
   via `enforcer.AddPolicy(...)` and calls `SavePolicy()`, **Then** the rules
   are persisted as `CasbinRule` rows.
3. **Given** rules persisted by a prior process, **When** a new enforcer is
   constructed against the same database, **Then** `LoadPolicy()` reproduces
   the stored rules in policy-load order.

---

### Usage Scenario 2 — Attach Casbin to an existing `*gorm.DB` (Priority: P2)

A service already manages a Gorm connection (with its own pooling, logging,
migrations) and wants Casbin to share that connection rather than open a
second one. The caller passes their `*gorm.DB` into one of the
`NewAdapterByDB*` constructors, optionally choosing a custom table prefix,
table name, or fully custom row struct.

**Why this priority**: Common in monoliths and frameworks (e.g., go-admin
itself) where Gorm is the established ORM. Also the path that exercises
custom-table customization which the README documents under "Customize table
columns".

**Independent test**: Open a `*gorm.DB` directly with a Gorm driver,
construct an adapter via `NewAdapterByDBUseTableName(db, "my_", "auth")`,
and verify policy CRUD lands in `my_auth` rather than `casbin_rule`.

**Acceptance Scenarios**:

1. **Given** a caller-owned `*gorm.DB`, **When** the caller invokes
   `NewAdapterByDB(db)`, **Then** the adapter reuses that connection (no new
   `gorm.Open`) and operates on the default `casbin_rule` table.
2. **Given** a caller wanting a renamed table, **When** they call
   `NewAdapterByDBUseTableName(db, prefix, name)`, **Then** all subsequent
   policy reads/writes target `<prefix><name>`.
3. **Given** a caller wanting fully custom columns, **When** they call
   `NewAdapterByDBWithCustomTable(db, &MyRule{}, optionalName...)` with a
   struct that embeds the required `Ptype`/`V0..VN` fields, **Then** the
   adapter migrates that struct's schema and uses it for CRUD.
4. **Given** an environment that already manages migrations externally,
   **When** the caller invokes `TurnOffAutoMigrate(db)` before constructing
   the adapter, **Then** the adapter skips its `AutoMigrate` step at startup.

---

### Usage Scenario 3 — Filtered policy loading for large policy sets (Priority: P3)

A service has a large policy table (millions of rules across many tenants)
and only needs the rules matching a tenant or `ptype` for a given enforcer
instance. The caller constructs a filtered adapter, then calls
`LoadFilteredPolicy(model, &Filter{...})` to load a subset; subsequent
`SavePolicy` honours the loaded scope so unrelated rules are not wiped.

**Why this priority**: A correctness-critical edge — naïve `SavePolicy` after
a partial load would truncate the table. Lower priority than P1/P2 only
because most consumers do not need it; for those who do, getting it wrong is
a data-loss bug.

**Independent test**: Insert rules for `Ptype` `p` and `p2`; load with
`Filter{Ptype: []string{"p"}}`; verify `IsFiltered()` returns true; modify
loaded rules; call `SavePolicy`; verify `p2` rules are untouched. Mirrors
the existing `testFilteredPolicy` coverage.

**Acceptance Scenarios**:

1. **Given** a database with rules across multiple `Ptype` values, **When**
   the caller invokes `NewFilteredAdapter(driver, dsn).LoadFilteredPolicy(...)`
   with a non-nil `Filter`, **Then** only matching rows are materialised into
   the model and `IsFiltered()` returns `true`.
2. **Given** an adapter in the filtered state, **When** the caller invokes
   `SavePolicy`, **Then** the save is scoped to the loaded subset and rows
   outside the filter are not touched.
3. **Given** a `Filter{}` zero value, **When** passed to
   `LoadFilteredPolicy`, **Then** the call behaves equivalently to
   `LoadPolicy`.

---

### Edge Cases (existing handling, not new requirements)

- **`NilField` rows**: `CasbinRule` rows with `NULL` value columns are
  tolerated on load (per `TestNilField`).
- **Empty policy**: `SavePolicy` on an empty model truncates / no-ops without
  error.
- **AutoMigrate disabled**: When `TurnOffAutoMigrate(db)` was called, the
  adapter trusts caller-managed schema and does not call `db.AutoMigrate`.
- **Custom table-name collision**: `NewAdapterByDBUseTableName` does not
  validate uniqueness against existing tables in the DB; reuse is the
  caller's responsibility.
- **Multi-DB switching**: `DbPool.switchDb(dbName)` selects from the resolver
  pool; an unknown name returns the default policy connection (verified
  against the resolver setup hyperedge in the graph report).
- **Adapter lifecycle**: A package-level `finalizer` registered on the
  Adapter releases the underlying `*sql.DB` on GC; explicit
  `Adapter.Close()` is supported and preferred for deterministic shutdown.

---

## Requirements *(mandatory)*

### Adapter Contract

- **AC-001** — The Adapter MUST satisfy Casbin's `persist.Adapter` interface
  (`LoadPolicy`, `SavePolicy`, `AddPolicy`, `RemovePolicy`,
  `RemoveFilteredPolicy`).
- **AC-002** — The Adapter MUST satisfy Casbin's `persist.FilteredAdapter`
  interface (`LoadFilteredPolicy`, `IsFiltered`).
- **AC-003** — The Adapter MUST satisfy Casbin's `persist.BatchAdapter`
  interface (`AddPolicies`, `RemovePolicies`).
- **AC-004** — The Adapter MUST satisfy Casbin's `persist.UpdatableAdapter`
  interface (`UpdatePolicy`, `UpdatePolicies`, `UpdateFilteredPolicies`).
- **AC-005** — The Adapter MUST support these driver names in the
  `driverName` argument of `NewAdapter` / `NewFilteredAdapter`: `mysql`,
  `postgres`, `sqlserver`. The fourth driver `sqlite3` is only available
  when the package is built with the `sqlite3` build tag (per
  `// +build sqlite3` on `open_sqlite3.go` and `// +build !sqlite3` on
  `open.go`). Unsupported names MUST cause an error return, not a silent
  fallback.
- **AC-006** — The Adapter MUST default to a `casbin_rule` (singular) table.
  This is the post-v3.0.4 schema; the v3.0.3 plural form `casbin_rules` is
  not supported.
- **AC-007** — The Adapter MUST run `db.AutoMigrate` on its row type during
  construction unless `TurnOffAutoMigrate(db)` was called against the same
  `*gorm.DB` first.
- **AC-008** — The Adapter MUST expose six top-level constructors:
  `NewAdapter`, `NewAdapterByDB`, `NewAdapterByDBUseTableName`,
  `NewAdapterByDBWithCustomTable`, `NewFilteredAdapter`, and
  `NewAdapterByMulDb`. Adding constructors is governed by the constitution's
  Principle V (Minimal Surface).
- **AC-009** — The Adapter MUST expose `Open`, `Close`, and `AddLogger` for
  lifecycle and Gorm logger override.
- **AC-010** — In Multi-DB mode, `InitDbResolver(dialectors, names)` MUST
  return a `DbPool` whose `switchDb(name)` resolves to the registered
  `*gorm.DB`; this is the only documented path for multi-tenant DB
  switching.
- **AC-011** — All driver-specific code paths MUST stay inside `open.go`
  and `open_sqlite3.go`; policy CRUD methods on `Adapter` MUST remain
  driver-agnostic. (Cross-reference: constitution Principle II.)

### Key Entities

- **`Adapter`** — Singleton-per-construction; holds `driverName`,
  `dataSourceName`, `databaseName`, `tablePrefix`, `tableName`,
  `dbSpecified`, `db *gorm.DB`, `isFiltered`. Not safe to mutate fields
  after construction.
- **`CasbinRule`** — Default row model. Columns: `ID` (uint primary key,
  autoincrement), `Ptype`, `V0`–`V5` (size 100), `V6`–`V7` (size 25).
  Custom-table users replace this with their own struct.
- **`Filter`** — Filter conditions for `LoadFilteredPolicy`. String slices
  for `Ptype` and `V0`–`V6`. **Asymmetry to note**: `CasbinRule` has
  `V0`–`V7` (8 value columns) but `Filter` only matches on `V0`–`V6`
  (7 columns). `V7` is storable but not filterable.
- **`DbPool`** — Multi-DB resolver. Holds `dbMap` (name → policy index),
  `policy` (round-robin/weighted resolver), and `source` (Gorm dialectors).
  All fields are private; constructed via `InitDbResolver`.
- **`specificPolicy`** — Private resolver implementation; not part of the
  public surface.

---

## Success Criteria *(mandatory — repurposed as Library Quality Outcomes for this baseline)*

### Library Quality Outcomes (current state, observable)

- **SC-001** — `TestAdapters` and the helper test suite (`testGetPolicy`,
  `testAutoSave`, `testFilteredPolicy`, `testGetFilteredPolicy`,
  `TestNilField`, etc.) pass against MySQL, PostgreSQL, SQL Server, and
  SQLite3 when run with valid DSNs.
- **SC-002** — Every public constructor has a runnable example in either
  `README.md` or the `examples/` directory.
- **SC-003** — The default schema matches v3.0.4+ (`casbin_rule` singular,
  V-columns sized as documented).
- **SC-004** — No driver-specific symbol leaks into the public Go API
  (verified by inspection: only generic Gorm types appear in exported
  signatures).
- **SC-005** — A consumer can integrate the adapter against any one
  supported driver in roughly 5–7 lines of setup code (per the README
  "Simple Example": one constructor call, one enforcer construction,
  one policy load).

---

## Architecture in Brief *(supplementary — facts that don't fit a single Usage Scenario)*

This section captures structural truths the graph report surfaces. It is not
required for using the library but is preserved here so the baseline is
complete.

- **Constructor convergence**: All six constructors funnel into
  `(a *Adapter).Open()` (line 294), which dispatches to the per-driver
  open switch in `open.go` / `open_sqlite3.go`. Customisation (custom table,
  multi-DB) is applied around this convergent core.
- **Multi-DB lifecycle**: `NewAdapterByMulDb` registers a finalizer (per
  the graph report's "Multi-DB Pool & Lifecycle" community) so dropped
  Adapter references release their underlying connections during GC.
  Explicit `Close()` is preferred when shutdown timing matters.
- **Filtered query construction**: `Adapter.filterQuery` (in the
  "Filtered Policy Loading" community) builds the WHERE clause from the
  `Filter` struct's slices via `appendWhere` / `checkQueryField` helpers.
- **Driver choice for SQLite (DRIFT)**: `README.md` states the package
  uses `github.com/glebarez/sqlite` to avoid a CGO dependency. The code
  at this baseline (`open_sqlite3.go` line 8 and `go.mod`) actually
  imports `gorm.io/driver/sqlite v1.4.3`, which **does** require CGO.
  README and code are out of sync at `bc66b93`. This is a fork-state
  observation, not a recommendation to change either side.
- **Logger wiring**: `Adapter.AddLogger` is the only hook for replacing
  the underlying Gorm logger; it must be called after construction but
  before any policy operation.

---

## Assumptions

- **Baseline target is `bc66b93`** (master, 2022-11-27, "Update go.mod"),
  not the current `main` HEAD. Commits after `bc66b93` on `main` are
  fork-only infrastructure (graphify, CLAUDE.md, SpecKit, constitution)
  and add no library behaviour. Locking the baseline to `bc66b93` keeps
  this spec aligned with the upstream-derived behaviour.
- **Source of truth for facts**: `adapter.go` (read directly for symbol
  names and signatures), `open.go` / `open_sqlite3.go` (driver switch),
  `README.md` (usage examples), and `graphify-out/GRAPH_REPORT.md`
  (architectural relationships and hyperedges). No new tests were run
  to produce this spec; behavioural claims that go beyond what the code
  reads or the graph asserts are flagged in the relevant scenario.
- **Audience**: A future reader of this fork (the user themselves, per
  `x_fork.branch-origin.md`) wanting a User-reference-level mental model
  without reading every internal helper. Maintainer-level internals
  (resolver internals, finalizer details, CGO rationale beyond a one-line
  note) are deliberately out of scope.
- **Module path**: `github.com/go-admin-team/gorm-adapter/v3` is the
  fork's module path; `/v3` is part of the import contract per Go module
  semantics.
- **Go version floor**: `go 1.14` per `go.mod`. Raising this is a
  breaking change for downstream consumers and is out of scope for this
  baseline.

---

## Drift Surfaced by This Baseline (informational)

Two facts emerged during this baseline write-up that diverge from claims in
sibling documents. They are recorded here for traceability; acting on them
is out of scope for this spec.

1. **Constitution v1.0.0 inherits the README's `glebarez/sqlite` claim.**
   Constitution Principle II ("Cross-Database Parity") and the
   "Quality & Compatibility Standards" section both reference
   `glebarez/sqlite` as the SQLite driver and state that swapping to
   `gorm.io/driver/sqlite` would be a deliberate cgo-policy decision.
   The code at baseline `bc66b93` already uses `gorm.io/driver/sqlite`.
   A constitution PATCH bump (1.0.0 → 1.0.1) is the natural follow-up:
   either correct the principle to match code, or treat the divergence
   as a known fork-state issue.

2. **SQLite support is build-tag-conditional, not unconditional.**
   The README and constitution treat SQLite3 as a peer of MySQL/PG/SQL
   Server. In practice, omitting `-tags sqlite3` at build time produces
   a binary that returns an error on `NewAdapter("sqlite3", ...)`. The
   constitution's Principle II "MUST behave identically across the four
   officially supported drivers" should be read with this build-tag
   precondition in mind.

---

## Out of Scope (explicit non-requirements)

- Behaviour of unofficial third-party drivers beyond MySQL/PG/SQL Server/SQLite.
- Performance characterisation (benchmarks, query plans).
- Comparison with alternative Casbin adapters.
- Upstream-divergence audit — covered by `x_fork.branch-origin.md` and the
  constitution's Principle IV.
- Future improvement proposals — this is a current-state baseline, not a
  roadmap.
