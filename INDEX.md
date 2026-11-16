# Documentation Index

This repository contains explanatory documentation for Wicofe OS. Normative contracts remain in the owning component repositories or Wicofe-Specs.

## Documentation areas

- `user/` — end-user operation and desktop workflows.
- `admin/` — installation, configuration, services, storage, networking, updates, and recovery.
- `developer/` — toolchains, build workflows, debugging, and cross-repository development.
- `contributing/` — contribution and review process.
- `troubleshooting/` — diagnostics and recovery procedures.

## Repository documentation ownership

- [Repository documentation map](REPOSITORY_DOCUMENTATION_MAP.md) — component-by-component ownership, canonical documentation indexes, and synchronization rules.
- [OSynit system specification 0.1](https://github.com/Waizusora/Osynit/blob/main/docs/OSYNIT_SYSTEM_SPEC_0.1.md) — canonical init architecture, Core Init boundary, optional modules and service lifecycle.
- [Cross-repository consistency audit — 2026-11-16](AUDIT_REPORT_2026-11-16.md) — initial review of all 29 Wicofe repository READMEs/indexes, ownership boundaries, lifecycle status, licensing policy alignment, and outstanding actions.\n- [Dependency license audit — 2026-11-16](DEPENDENCY_LICENSE_AUDIT_2026-11-16.md) — actual 29-repository dependency scan, Cargo and GitHub Actions evidence, strict-gate result and remaining compliance work.
- [Wicofe dependency license policy](https://github.com/Waizusora/Wicofe-ThirdParty/blob/main/policies/DEPENDENCY_LICENSE_POLICY_0.2.md) — project-wide GPL/AGPL prohibition, conditional LGPL approval, and review requirements for other licenses.

## Canonical project references

- [Wicofe repository map](https://github.com/Waizusora/Wicofe/blob/main/docs/REPOSITORY_MAP.md)
- [Wicofe architecture](https://github.com/Waizusora/Wicofe/blob/main/docs/ARCHITECTURE.md)
- [Wicofe roadmap](https://github.com/Waizusora/Wicofe/blob/main/docs/ROADMAP.md)
- [Cross-component specifications](https://github.com/Waizusora/Wicofe-Specs)
- [Userspace ABI](https://github.com/Waizusora/Wicofe-ABI)
- [Kernel implementation and DKM contract](https://github.com/Waizusora/Wicofe-Kernel)

## Publication rules

Documentation must label functionality as implemented, tested, experimental, planned, deferred, or unsupported. Commands and procedures should identify their tested environment and expected result. Do not document a planned feature as available.

## Status

Index baseline. Individual guides will be added as features become usable and verifiable.
