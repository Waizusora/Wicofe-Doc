# Wicofe Repository Documentation Map

- **Purpose:** Canonical navigation map for documentation distributed across Wicofe repositories.
- **Status:** Maintained index; repository owners remain authoritative for their own technical documents.
- **Rule:** A repository README explains that repository's responsibility. Its `docs/INDEX.md` lists technical documents owned there. This central map links to those indexes and identifies cross-repository boundaries.

## System and governance

| Repository | Documentation responsibility |
|---|---|
| [Wicofe](https://github.com/Waizusora/Wicofe) | Whole-system overview, architecture, roadmap, repository map, project decisions |
| [Wicofe-Doc](https://github.com/Waizusora/Wicofe-Doc) | User, administrator, developer, contributor, and troubleshooting guides; central documentation navigation |
| [Wicofe-Spec](https://github.com/Waizusora/Wicofe-Spec) | Normative cross-component specifications and shared contracts |
| [Wicofe-Test](https://github.com/Waizusora/Wicofe-Test) | Cross-repository conformance, integration tests, fixtures, and test strategy |
| [Wicofe-Tool](https://github.com/Waizusora/Wicofe-Tool) | Shared developer, validation, maintenance, and release tools; [documentation validator](https://github.com/Waizusora/Wicofe-Tool/blob/main/docs/REPOSITORY_DOCUMENTATION_VALIDATOR.md), [repository inventory validator](https://github.com/Waizusora/Wicofe-Tool/blob/main/docs/REPOSITORY_INVENTORY_VALIDATOR.md) |
| [Wicofe-ThirdParty](https://github.com/Waizusora/Wicofe-ThirdParty) | Third-party inventory, provenance, licensing, notices, and approval records |

## Project-wide principles

The canonical [Wicofe Project Principles](https://github.com/Waizusora/Wicofe-Doc/blob/main/PROJECT_PRINCIPLES.md) define Wicofe as a Unix-like, POSIX-compatible, non-GNU alternative. Native software must use Wicofe interfaces and must not require Linux libc or GNU compatibility layers. Permissive licenses are preferred; GPL/AGPL are avoided, and LGPL is considered only when no suitable permissive alternative exists. Reuse or fork upstream components when implementing them from scratch would be disproportionately difficult.

## Project-wide dependency licensing

The binding [Wicofe Dependency License Policy 0.2](https://github.com/Waizusora/Wicofe-ThirdParty/blob/main/policies/DEPENDENCY_LICENSE_POLICY_0.2.md) applies to every repository: GPL and AGPL dependencies are prohibited; LGPL is conditionally allowed after exact review and scoped approval; other licenses are allowed subject to compatibility and obligations review. Other copyleft, custom, proprietary or ambiguous terms require careful review and explicit project-owner approval. Unknown license evidence blocks approval.

## Kernel and low-level interfaces

| Repository | Documentation responsibility |
|---|---|
| [Wicofe-Kernel](https://github.com/Waizusora/Wicofe-Kernel) | Kernel architecture, boot, CPU, memory, scheduling, syscalls implementation, VFS, block I/O, drivers, DKM ABI |
| [Wicofe-ABI](https://github.com/Waizusora/Wicofe-ABI) | Public userspace syscall ABI, data structures, calling conventions, errors, and compatibility |
| [Wicofe-Driver](https://github.com/Waizusora/Wicofe-Driver) | Optional device drivers, hardware matrices, DKM packaging, driver lifecycle and validation |
| [Wicofe-Storage](https://github.com/Waizusora/Wicofe-Storage) | Userspace storage administration, partitioning, mount orchestration, diagnostics |
| [ONWFS](https://github.com/Waizusora/ONWFS) | ONWFS disk format, filesystem behavior, formatter/checker/recovery, conformance vectors |

## Userspace foundations and services

| Repository | Documentation responsibility |
|---|---|
| [Wicofe-Lib](https://github.com/Waizusora/Wicofe-Lib) | Shared Rust userspace libraries and safe ABI wrappers |
| [Wlibc](https://github.com/Waizusora/WLibc) | C standard library/runtime, ISO C17 and POSIX.1-2024 interfaces, native syscall adaptation, timezone runtime and conformance; [pinned musl baseline](https://github.com/Waizusora/WLibc/blob/main/docs/UPSTREAM_BASELINE_MUSL_1.2.6.md) |
| [Frenit](https://github.com/Waizusora/Frenit) | Free Init implementation, CLI, service-management foundation; native Wicofe PID 1 integration remains unverified |
| [Mysh](https://github.com/Waizusora/Mysh) | Independent command-line shell; Wicofe shell integration is a planned native Rust target. Package management belongs to WPM |
| Wutils (planned) | Native Rust fork of uutils for POSIX utilities; target requirements are defined in [WUTILS_NATIVE_PORTING_REQUIREMENTS_0.1](https://github.com/Waizusora/Wicofe-Spec/blob/main/userspace/WUTILS_NATIVE_PORTING_REQUIREMENTS_0.1.md). No Linux libc or GNU compatibility backend is permitted |
| [Wicofe-Service](https://github.com/Waizusora/Wicofe-Service) | Individual system daemons, IPC, privilege model, service lifecycle |
| [Wicofe-Network](https://github.com/Waizusora/Wicofe-Network) | Userspace networking configuration, services, and diagnostics |
| [Wicofe-Input](https://github.com/Waizusora/Wicofe-Input) | Userspace input policy, event routing, key maps, seats, and diagnostics |
| [Wicofe-Graphic](https://github.com/Waizusora/Wicofe-Graphic) | Reusable userspace graphics/display infrastructure and APIs |
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
| [Wicofe-Port](https://github.com/Waizusora/Wicofe-Port) | Upstream build recipes, patches, port status, integration notes |

## Project-level documentation indexes

- [Wicofe project documentation](https://github.com/Waizusora/Wicofe/blob/main/docs/INDEX.md) — whole-system architecture, roadmap, repository map, and project decisions.
- [Frenit README](https://github.com/Waizusora/Frenit/blob/main/README.md) — canonical project identity, executable name, CLI convention, and current implementation status.
- [Frenit integration contract 0.1](https://github.com/Waizusora/Wicofe-Spec/blob/main/boot/FRENIT_INTEGRATION_CONTRACT_0.1.md) — proposed cross-repository integration boundary.
- [Unix userspace foundation 0.1](https://github.com/Waizusora/Wicofe-Spec/blob/main/userspace/UNIX_USERSPACE_FOUNDATION_0.1.md) — proposed WFH, Wlibc, POSIX and timezone architecture.
- [Native Wutils porting requirements 0.1](https://github.com/Waizusora/Wicofe-Spec/blob/main/userspace/WUTILS_NATIVE_PORTING_REQUIREMENTS_0.1.md) — native Rust target, no Linux libc backend, POSIX utility behavior.
- [Wlibc documentation index](https://github.com/Waizusora/WLibc/blob/main/docs/INDEX.md) — C runtime architecture, porting and conformance plan.
- [Wicofe-Doc central guide index](https://github.com/Waizusora/Wicofe-Doc/blob/main/INDEX.md) — user, administrator, developer, contributor, and troubleshooting guides.
- [System delivery and installation direction 0.1](https://github.com/Waizusora/Wicofe-Doc/blob/main/SYSTEM_DELIVERY_AND_INSTALLATION_DIRECTION_0.1.md) — planned CLI install/update experience and Delivery Release policy direction; not normative implementation evidence.

## Component documentation indexes

Every linked `docs/INDEX.md` is scoped to its repository. The root Wicofe repository remains the only place for the whole-system architecture overview; component repositories must not copy that overview as their own technical documentation.

- [Kernel](https://github.com/Waizusora/Wicofe-Kernel/blob/main/docs/INDEX.md) · [ABI](https://github.com/Waizusora/Wicofe-ABI/blob/main/docs/INDEX.md) · [Drivers](https://github.com/Waizusora/Wicofe-Driver/blob/main/docs/INDEX.md) · [Storage](https://github.com/Waizusora/Wicofe-Storage/blob/main/docs/INDEX.md) · [ONWFS](https://github.com/Waizusora/ONWFS/blob/main/docs/INDEX.md)
- [Lib](https://github.com/Waizusora/Wicofe-Lib/blob/main/docs/INDEX.md) · [Wlibc](https://github.com/Waizusora/WLibc/blob/main/docs/INDEX.md) · [Services](https://github.com/Waizusora/Wicofe-Service/blob/main/docs/INDEX.md) · [Network](https://github.com/Waizusora/Wicofe-Network/blob/main/docs/INDEX.md) · [Input](https://github.com/Waizusora/Wicofe-Input/blob/main/docs/INDEX.md)
- [Graphics](https://github.com/Waizusora/Wicofe-Graphic/blob/main/docs/INDEX.md) · [Audio](https://github.com/Waizusora/Wicofe-Audio/blob/main/docs/INDEX.md) · [WDE](https://github.com/Waizusora/WDE/blob/main/docs/INDEX.md) · [Frenit](https://github.com/Waizusora/Frenit)

## Frenit cross-repository integration

Frenit owns init policy, service definitions, dependency ordering, supervision, restart policy and shutdown orchestration. The kernel owns process, exec, wait/reap, signal, descriptor, IPC, clock and power primitives. Wicofe-ABI owns their syscall definitions and error semantics. Wicofe-Spec coordinates boot and image integration. Wicofe-Service owns daemon implementations. Wicofe-Image and Wicofe-Installer package and deploy Frenit with the system. Wicofe-Test validates the integration. Native PID 1 handoff remains unverified until the ABI, kernel, boot, image and runtime gates pass.
