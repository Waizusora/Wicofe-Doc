# Wicofe-Docs

Central user, developer, administrator, and contributor documentation for Wicofe OS.

## Scope

- Getting-started material and project overview.
- User and administrator guides.
- Developer workflows and contribution guidance.
- System operation, configuration, troubleshooting, and maintenance guides.
- Cross-component documentation that does not belong exclusively to a component repository.

## Project-wide principles

The [Wicofe Project Principles](PROJECT_PRINCIPLES.md) define the system-wide identity, native architecture, POSIX/non-GNU direction, licensing preferences, and upstream reuse policy. These principles apply to every Wicofe repository and component.

## Documentation ownership

Normative interface and format requirements belong in Wicofe-Specs or the owning component's specification. This repository explains how to use, develop, configure, and operate the system. Component-specific implementation details should link to the authoritative component documentation rather than duplicate it.

## Canonical init-system reference

[Frenit (Free Init)](https://github.com/Waizusora/Frenit) is the canonical Wicofe init-system project. Its CLI and implementation documentation live in Frenit; the proposed kernel/ABI/boot integration gates are maintained in [WIC-SPEC-BOOT-FRENIT-001](https://github.com/Waizusora/Wicofe-Specs/blob/main/boot/FRENIT_INTEGRATION_CONTRACT_0.1.md). Native PID 1 integration is not yet verified and must not be described as available.

## Documentation standards

- Clearly label planned, experimental, implemented, and stable functionality.
- Identify the Wicofe version or specification revision where relevant.
- Include tested commands and expected results.
- Keep security-sensitive procedures explicit and review destructive steps.
- Link to canonical specifications and source repositories.

## Suggested structure

- `user/` — end-user guides.
- `admin/` — system administration.
- `developer/` — development environment and workflows.
- `contributing/` — contribution process.
- `troubleshooting/` — diagnostics and recovery.

## Status

Initial repository baseline. Documentation must not imply that planned functionality is already available.

## License

Original Wicofe documentation is intended to use MPL-2.0 unless a file states otherwise. External material must retain required attribution and license notices.

## Documentation index

Start at [INDEX.md](INDEX.md). The [repository documentation map](REPOSITORY_DOCUMENTATION_MAP.md) identifies the documentation owner and canonical index for every Wicofe component.
