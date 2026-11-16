# Wicofe Repository Documentation Map

- **Purpose:** Canonical navigation map for documentation distributed across Wicofe repositories.
- **Status:** Maintained index; repository owners remain authoritative for their own technical documents.
- **Rule:** A repository README explains that repository's responsibility. Its `docs/INDEX.md` lists technical documents owned there. This central map links to those indexes and identifies cross-repository boundaries.

## System and governance

| Repository | Documentation responsibility |
|---|---|
| [Wicofe](https://github.com/Waizusora/Wicofe) | Whole-system overview, architecture, roadmap, repository map, project decisions |
| [Wicofe-Docs](https://github.com/Waizusora/Wicofe-Docs) | User, administrator, developer, contributor, and troubleshooting guides; central documentation navigation |
| [Wicofe-Specs](https://github.com/Waizusora/Wicofe-Specs) | Normative cross-component specifications and shared contracts |
| [Wicofe-Tests](https://github.com/Waizusora/Wicofe-Tests) | Cross-repository conformance, integration tests, fixtures, and test strategy |
| [Wicofe-Tools](https://github.com/Waizusora/Wicofe-Tools) | Shared developer, validation, maintenance, and release tools; [documentation validator](https://github.com/Waizusora/Wicofe-Tools/blob/main/docs/REPOSITORY_DOCUMENTATION_VALIDATOR.md) |
| [Wicofe-ThirdParty](https://github.com/Waizusora/Wicofe-ThirdParty) | Third-party inventory, provenance, licensing, notices, and approval records |

## Kernel and low-level interfaces

| Repository | Documentation responsibility |
|---|---|
| [Wicofe-Kernel](https://github.com/Waizusora/Wicofe-Kernel) | Kernel architecture, boot, CPU, memory, scheduling, syscalls implementation, VFS, block I/O, drivers, DKM ABI |
| [Wicofe-ABI](https://github.com/Waizusora/Wicofe-ABI) | Public userspace syscall ABI, data structures, calling conventions, errors, and compatibility |
| [Wicofe-Drivers](https://github.com/Waizusora/Wicofe-Drivers) | Optional device drivers, hardware matrices, DKM packaging, driver lifecycle and validation |
| [Wicofe-Storage](https://github.com/Waizusora/Wicofe-Storage) | Userspace storage administration, partitioning, mount orchestration, diagnostics |
| [ONWFS](https://github.com/Waizusora/ONWFS) | ONWFS disk format, filesystem behavior, formatter/checker/recovery, conformance vectors |

## Userspace foundations and services

| Repository | Documentation responsibility |
|---|---|
| [Wicofe-Lib](https://github.com/Waizusora/Wicofe-Lib) | Shared Rust userspace libraries and safe ABI wrappers |
| [Wicofe-Libc](https://github.com/Waizusora/Wicofe-Libc) | C standard library/runtime port, startup, syscall glue, compatibility |
| [Osynit](https://github.com/Waizusora/Osynit) | PID 1, init, service definitions, dependency ordering, supervision, shutdown |
| [Mysh](https://github.com/Waizusora/Mysh) | Independent command-line shell; Wicofe shell integration is a planned target. Package management belongs to WPM |
| [Wicofe-Services](https://github.com/Waizusora/Wicofe-Services) | Individual system daemons, IPC, privilege model, service lifecycle |
| [Wicofe-Network](https://github.com/Waizusora/Wicofe-Network) | Userspace networking configuration, services, and diagnostics |
| [Wicofe-Input](https://github.com/Waizusora/Wicofe-Input) | Userspace input policy, event routing, key maps, seats, and diagnostics |
| [Wicofe-Graphics](https://github.com/Waizusora/Wicofe-Graphics) | Reusable userspace graphics/display infrastructure and APIs |
| [Wicofe-Audio](https://github.com/Waizusora/Wicofe-Audio) | Userspace audio services, routing, APIs, formats, and validation |
| [WDE](https://github.com/Waizusora/WDE) | Desktop session, compositor/window management, panel, launcher, settings, themes |
| [WPM](https://github.com/Waizusora/WPM) | Package formats, repositories, dependency resolution, package transactions |

## Build, deployment, and lifecycle

| Repository | Documentation responsibility |
|---|---|
| [Wicofe-Build](https://github.com/Waizusora/Wicofe-Build) | Whole-system build graph, pinned toolchains, cross-builds, reproducibility |
| [Wicofe-Image](https://github.com/Waizusora/Wicofe-Image) | Image manifests, image assembly, release artifacts, image validation |
| [Wicofe-Installer](https://github.com/Waizusora/Wicofe-Installer) | Installation workflow, disk selection, boot setup, deployment safety |
| [Wicofe-Update](https://github.com/Waizusora/Wicofe-Update) | Whole-system updates, signed metadata, staging, activation, rollback |
| [Wicofe-Recovery](https://github.com/Waizusora/Wicofe-Recovery) | Recovery environment, diagnostics, restore, repair orchestration |
| [Wicofe-SDK](https://github.com/Waizusora/Wicofe-SDK) | Application developer toolchain, sysroot, headers, linker, templates |
| [Wicofe-Ports](https://github.com/Waizusora/Wicofe-Ports) | Upstream build recipes, patches, port status, integration notes |

## Project-level documentation indexes

- [Wicofe project documentation](https://github.com/Waizusora/Wicofe/blob/main/docs/INDEX.md) — whole-system architecture, roadmap, repository map, and project decisions.
- [Wicofe-Docs central guide index](https://github.com/Waizusora/Wicofe-Docs/blob/main/INDEX.md) — user, administrator, developer, contributor, and troubleshooting guides.

## Component documentation indexes

Every linked `docs/INDEX.md` is scoped to its repository. The root Wicofe repository remains the only place for the whole-system architecture overview; component repositories must not copy that overview as their own technical documentation.

- [Kernel](https://github.com/Waizusora/Wicofe-Kernel/blob/main/docs/INDEX.md) · [ABI](https://github.com/Waizusora/Wicofe-ABI/blob/main/docs/INDEX.md) · [Drivers](https://github.com/Waizusora/Wicofe-Drivers/blob/main/docs/INDEX.md) · [Storage](https://github.com/Waizusora/Wicofe-Storage/blob/main/docs/INDEX.md) · [ONWFS](https://github.com/Waizusora/ONWFS/blob/main/docs/INDEX.md)
- [Lib](https://github.com/Waizusora/Wicofe-Lib/blob/main/docs/INDEX.md) · [Libc](https://github.com/Waizusora/Wicofe-Libc/blob/main/docs/INDEX.md) · [Services](https://github.com/Waizusora/Wicofe-Services/blob/main/docs/INDEX.md) · [Network](https://github.com/Waizusora/Wicofe-Network/blob/main/docs/INDEX.md) · [Input](https://github.com/Waizusora/Wicofe-Input/blob/main/docs/INDEX.md)
- [Graphics](https://github.com/Waizusora/Wicofe-Graphics/blob/main/docs/INDEX.md) · [Audio](https://github.com/Waizusora/Wicofe-Audio/blob/main/docs/INDEX.md) · [WDE](https://github.com/Waizusora/WDE/blob/main/docs/INDEX.md) · [Osynit](https://github.com/Waizusora/Osynit/blob/main/docs/INDEX.md) · [Mysh](https://github.com/Waizusora/Mysh/blob/main/docs/INDEX.md) · [WPM](https://github.com/Waizusora/WPM/blob/main/docs/INDEX.md)
- [Build](https://github.com/Waizusora/Wicofe-Build/blob/main/docs/INDEX.md) · [Image](https://github.com/Waizusora/Wicofe-Image/blob/main/docs/INDEX.md) · [Installer](https://github.com/Waizusora/Wicofe-Installer/blob/main/docs/INDEX.md) · [Update](https://github.com/Waizusora/Wicofe-Update/blob/main/docs/INDEX.md) · [Recovery](https://github.com/Waizusora/Wicofe-Recovery/blob/main/docs/INDEX.md)
- [SDK](https://github.com/Waizusora/Wicofe-SDK/blob/main/docs/INDEX.md) · [Ports](https://github.com/Waizusora/Wicofe-Ports/blob/main/docs/INDEX.md) · [Tools](https://github.com/Waizusora/Wicofe-Tools/blob/main/docs/INDEX.md) · [Specs](https://github.com/Waizusora/Wicofe-Specs/blob/main/docs/INDEX.md) · [Tests](https://github.com/Waizusora/Wicofe-Tests/blob/main/docs/INDEX.md) · [ThirdParty](https://github.com/Waizusora/Wicofe-ThirdParty/blob/main/docs/INDEX.md)

## Documentation synchronization rules

1. Component-specific implementation details live in the owning repository.
2. Cross-component requirements live in Wicofe-Specs and link to component authorities.
3. Wicofe-Docs explains system use and development; it links to normative component documents rather than copying them.
4. Each component README describes only that component's purpose, boundaries, status, build/test entry points, and documentation index.
5. When a canonical document changes, update this map or the central index only if navigation, ownership, status, or cross-repository links change.
6. Planned functionality must be labeled as planned or proposed. Do not imply implementation or test success without evidence.
