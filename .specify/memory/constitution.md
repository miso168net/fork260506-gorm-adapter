<!--
SYNC IMPACT REPORT
==================
Version change: (uninitialized template) → 1.0.0
Bump rationale: MAJOR — initial ratification, replacing empty placeholder template
                with concrete, testable principles for the gorm-adapter fork.

Modified principles:
  - [PRINCIPLE_1_NAME]            → I. Adapter Contract Stability
  - [PRINCIPLE_2_NAME]            → II. Cross-Database Parity
  - [PRINCIPLE_3_NAME]            → III. Test-First for Policy Logic (NON-NEGOTIABLE)
  - [PRINCIPLE_4_NAME]            → IV. Fork Hygiene & Upstream Traceability
  - [PRINCIPLE_5_NAME]            → V. Minimal Surface & Explicit Migration

Added sections:
  - Quality & Compatibility Standards (was [SECTION_2_NAME])
  - Development Workflow & Release Process (was [SECTION_3_NAME])

Removed sections: none

Templates requiring updates:
  - .specify/templates/plan-template.md     ✅ no change needed (Constitution Check
                                              gate is principle-agnostic; gates will
                                              be derived per-feature against this file)
  - .specify/templates/spec-template.md     ✅ no change needed (no constitution
                                              references; principles operate at
                                              plan/code level, not spec level)
  - .specify/templates/tasks-template.md    ✅ no change needed (task categorization
                                              already supports test-first discipline
                                              and cross-cutting polish phase)
  - .specify/templates/checklist-template.md ✅ not reviewed in detail; principles
                                              are advisory, not structurally
                                              required by checklist generation
  - .claude/skills/speckit-*/                ⚠ pending review — slash command
                                              prompts reference generic templates
                                              only; no per-principle content to sync
  - README.md                                ✅ no change needed (upstream-derived;
                                              fork-specific notes already live in
                                              x_fork.branch-origin.md)
  - CLAUDE.md (project)                      ✅ no change needed (graphify guidance
                                              orthogonal to constitution principles)

Follow-up TODOs: none. RATIFICATION_DATE set to today (2026-05-07) since this
                 is the first ratified version of the constitution; no prior
                 adoption date exists.
-->

# Gorm Adapter Constitution

## Core Principles

### I. Adapter Contract Stability

The exported Casbin `persist.Adapter` surface — `LoadPolicy`, `SavePolicy`, `AddPolicy`,
`RemovePolicy`, `RemoveFilteredPolicy`, and the batch / filtered / multi-DB extensions
re-exported by this package — MUST remain backward compatible within a major version.
Any signature change, behavioural redefinition, or removal of an exported symbol
requires a MAJOR version bump and an explicit migration note in `README.md`.

**Rationale**: Downstream projects pin this adapter into Casbin enforcers; silent
contract drift breaks policy loading in production with no compile-time signal.
The v3.0.3 → v3.0.4 `casbin_rules` → `casbin_rule` rename is the canonical example
of a breaking change that MUST be advertised, not absorbed.

### II. Cross-Database Parity

Every policy operation MUST behave identically across the four officially supported
drivers: MySQL, PostgreSQL, SQL Server, and SQLite3 (via `github.com/glebarez/sqlite`).
New features MUST either (a) ship with test coverage exercising all four drivers, or
(b) document the unsupported drivers explicitly in the feature's godoc and `README.md`.
Driver-specific code paths SHOULD be confined to `open.go` / `open_sqlite3.go` and the
DB-open switch; policy CRUD MUST stay driver-agnostic.

**Rationale**: A Casbin adapter's value proposition is database neutrality. Silent
driver divergence — a policy save that succeeds on MySQL and corrupts on SQL Server —
defeats the abstraction and is hard for users to diagnose because the bug surfaces
far from the adapter call.

### III. Test-First for Policy Logic (NON-NEGOTIABLE)

Any change to policy CRUD, filter logic, table-name handling, multi-DB resolution,
or the SavePolicy/LoadPolicy round-trip MUST land with a failing test in
`adapter_test.go` (or a new `*_test.go`) authored before the implementation.
The existing `TestAdapters` suite MUST pass on every supported driver before merge;
a green run on a single driver is not sufficient evidence of correctness.

**Rationale**: Policy data is security-critical — bugs here silently grant or deny
access. The repo already has a strong integration-test culture (`TestAdapters`,
`testGetPolicy`, `testAutoSave`, ~24 test helpers); this principle codifies that
culture as non-negotiable rather than aspirational.

### IV. Fork Hygiene & Upstream Traceability

This repository is a fork of `casbin/gorm-adapter` published as
`github.com/go-admin-team/gorm-adapter/v3`. Every divergence from upstream MUST be
recorded in a `x_fork.*.md` note at the repo root, capturing: the upstream commit
forked from, the reason for the divergence, and whether the change is intended to
be upstreamed. Changes that are not fork-specific SHOULD be filed as an upstream
PR before, or alongside, the local merge.

**Rationale**: Forks rot. Without a deliberate trail of what was changed and why,
future merges from upstream become archaeological digs. The existing
`x_fork.branch-origin.md` and `x_fork.graphify-20260506.md` set the pattern; this
principle locks it in.

### V. Minimal Surface & Explicit Migration

The adapter SHOULD expose only what Casbin requires plus the demonstrably-needed
constructors (`NewAdapter`, `NewAdapterByDB`, `NewAdapterByDBUseTableName`,
`NewAdapterByDBWithCustomTable`, `NewFilteredAdapter`, `NewAdapterByMulDb`). New
exported constructors, options, or configuration knobs MUST justify their need in
the PR description and SHOULD prefer extending an existing constructor with an
options struct over adding a new top-level function. Any change to schema, default
table name, column types, or auto-migrate behaviour MUST ship with explicit
migration guidance in `README.md`.

**Rationale**: The constructor count is already the largest source of API
confusion in this repo (six top-level entry points; see graph report's "Adapter
constructor variants" hyperedge). Discipline here protects users from a Cartesian
explosion of init paths and protects maintainers from supporting permutations
nobody actually uses.

## Quality & Compatibility Standards

- **Go version**: Module declares `go 1.14`; raising the minimum Go version is a
  MAJOR change because it forces downstream upgrades. Use only language and stdlib
  features available in the declared minimum.
- **Dependency discipline**: New direct dependencies require justification. Prefer
  `gorm.io/*` ecosystem packages over alternatives. The `glebarez/sqlite` choice
  (no-cgo) is intentional — do not replace with `gorm.io/driver/sqlite` without a
  deliberate cgo-policy decision.
- **Schema changes**: Default table name is `casbin_rule` (singular). Custom-table
  flows MUST continue to work; `CasbinRule` struct field additions MUST be additive
  and tested with `TestNilField`-style coverage for legacy rows.
- **Concurrency**: Adapter instances are intended to be safe for concurrent use by
  a single Casbin enforcer; multi-DB pool changes MUST preserve this guarantee and
  document any new locking expectations.

## Development Workflow & Release Process

- **PR review gate**: Every PR MUST verify compliance with the five Core Principles.
  Reviewers SHOULD reject PRs that change the exported adapter surface without a
  version-bump plan, that add a driver-specific code path outside the open-switch
  layer, or that lack test coverage for policy logic changes.
- **CI expectation**: `go test ./...` MUST pass; integration tests against all four
  drivers SHOULD run in CI. A PR that only proves correctness on the developer's
  local driver is incomplete evidence.
- **Versioning**: Semantic Versioning (`vMAJOR.MINOR.PATCH`) per the Go module
  convention. The `/v3` import path is part of the contract — `/v4` requires a
  fresh import path under module-path semantics.
- **Constitution amendments**: Changes to this file follow the same versioning
  rules as the principles themselves (MAJOR for principle removal/redefinition,
  MINOR for additions, PATCH for clarifications). Amendments MUST update the
  Sync Impact Report and the version line below.
- **Runtime guidance**: Day-to-day "how to do X in this repo" lives in `CLAUDE.md`
  (graphify rules) and `README.md` (user-facing API examples), not here. This
  constitution is the authority on *what is non-negotiable*, not on *how to use
  the package*.

## Governance

This constitution supersedes ad-hoc convention when the two conflict. Compliance
is verified at PR review; violations require either a fix or a documented
exception in the PR description with reviewer sign-off. Constitution amendments
require: (1) a PR modifying this file with a Sync Impact Report, (2) propagation
to any dependent templates noted in that report, and (3) a version bump matching
the nature of the change. The `RATIFICATION_DATE` below is the date of initial
adoption and does not change on subsequent amendments; only `LAST_AMENDED_DATE`
and `Version` move.

**Version**: 1.0.0 | **Ratified**: 2026-05-07 | **Last Amended**: 2026-05-07
