# Wicofe Cross-Repository Change Audit — 2026-11-16

**Scope:** All 29 repositories in `Wicofe-Tools/config/repository_inventory.txt`  
**Branch inspected:** Default branch (`main` for all 29 repositories)  
**Snapshot:** 2026-11-16, approximately 13:42 UTC (with later documentation-only follow-ups listed below)  
**Method:** Read the latest default-branch commit and recursive Git tree for every repository; inspect manifest/lockfile names and selected changed documentation/source files. This is not a full source-code, full dependency, build, or test audit.

## 1. Executive summary

All 29 repositories were reachable and their default-branch heads were inspected. Recent changes are concentrated in three areas:

1. **Osynit integration and naming:** Wicofe, Wicofe-Docs, Wicofe-Specs, Wicofe-Tests, Wicofe-Kernel, Wicofe-Services, Wicofe-Build, Wicofe-Image and Wicofe-Installer received Osynit architecture/integration documentation updates and project-name standardization.
2. **Runtime implementation:** Osynit received supervisor test/formatting commits; Mysh received concurrent pipeline output-draining and regression-test commits.
3. **Supply-chain/licensing:** Wicofe-Tools expanded the cross-repository dependency auditor; Wicofe-ThirdParty recorded Limine and kernel host-tool evidence; WDE pinned CI actions/toolchain and added apt package license inventory.

Documentation corrections made during this audit:
- Fixed literal escaped newline in Wicofe-Docs `INDEX.md`.
- Removed duplicate Osynit contract entries from Wicofe-Specs `docs/INDEX.md`.
- Removed duplicate CLI reference from Osynit `docs/INDEX.md`.
- Removed duplicate Osynit architecture links from Wicofe-Build `docs/INDEX.md`.
- Updated Mysh README, architecture, command reference and changelog to distinguish concurrent OS-pipe execution for all-external simple pipelines from buffered fallback for mixed/in-process pipelines.
- Corrected Wicofe-Tools auditor documentation to reflect the Wicofe-Build release-gate integration.
- Updated central repository navigation to link the canonical Osynit specification and cross-component contract.

## 2. Current default-branch commit snapshot

The SHA column records the exact commit observed at the snapshot. Later documentation commits made during this audit are reflected for Wicofe-Docs, Wicofe-Specs and Wicofe-Tools where noted.

| Repository | Main HEAD | Latest observed change |
|---|---|---|
| Wicofe | `56ccdb80b1fabd5cb4f1286fbe8889d8af29ed53` | Standardize project name as Osynit |
| Wicofe-Docs | `6ace755b79b94808276626d1cb224de9a7e1afc5` | Record latest 29-repository change audit |
| Wicofe-Specs | `a9e86236617bfc00489eaacaaf507f0506b048d5` | Remove duplicate Osynit contract index entries |
| Wicofe-Tests | `6210042246ce0d3553dd852df4e0358019085dce` | Standardize project name as Osynit |
| Wicofe-Tools | `e113ec275cb45278683ac4a3da08fc6561bb59c2` | Fix tooling index and list dependency audit docs |
| Wicofe-ThirdParty | `d7755a6d9d9e8aa26e68e55aaa3bcd079b297f70` | Document Limine release license inclusion and notices |
| Wicofe-Kernel | `ff6ec4bb8aa36fdf656fbbfff402eba016493221` | Remove duplicate Osynit documentation index entry |
| Wicofe-ABI | `cab3cc6fd8c05f27e7862147f30a087a852f94e5` | Standardize project name as Osynit |
| Wicofe-Drivers | `7c3d05e8dec0cd66c103491d8b04f7e6c3877953` | Index driver subsystem design |
| Wicofe-Storage | `b42c7f75ff3c1ef93a7af06e7246792c68b73c4e` | Index storage management design |
| ONWFS | `ae06ce4178dd8cecb7ec47ea5d0f5715dadb0339` | Clarify ordered-data overwrite limitations |
| Wicofe-Lib | `cda650b19eef95463bf41596ecfa02e512571e77` | Index Rust userspace library architecture |
| Wicofe-Libc | `0d7314819ec66ca36bd06ff712250a4cb37c3fc4` | Index C runtime porting architecture |
| Osynit | `95f53171c3606c22ef34292c1b0e5398830242da` | Format supervisor duplicate-event assertion |
| Wicofe-Services | `4121d9b0a1090088df0c4243ad4ff7ed249c9181` | Standardize project name as Osynit |
| Wicofe-Network | `a003e296eba39356d510f38da3077042da3b9f20` | Index userspace networking architecture |
| Wicofe-Input | `2e8220baaf3f88a085d6dd5890e2c95b2b3905ab` | Index input subsystem architecture |
| Wicofe-Graphics | `2e66c3270dc4ea3ea9ed44ef9c8987864ca183a9` | Index graphics architecture draft |
| Wicofe-Audio | `ce8237a6c94093a378e8ca9388a5a5ce211d0369` | Index audio architecture draft |
| WDE | `471c66ed8951295d9f8533c0a43c786ffe552074` | Pin CI actions and inventory apt package licenses |
| WPM | `184d483bce67c377b8e4fc9581fb0116b5ce954f` | Link package manager documentation index |
| Mysh | `f84227e3dfb2a0fe8154003b63997d3f32a9652f` | Document concurrent external pipeline execution |
| Wicofe-Build | `7563cd28f9205cabd334e29716759f22ae756477` | Remove duplicate Osynit documentation index entry |
| Wicofe-Image | `6ebb653f9e555dfb849d860aaf89c79b2da0570b` | Standardize project name as Osynit |
| Wicofe-Installer | `9d88c64e41baab6c7aacb5d9637f3629facaef70` | Standardize project name as Osynit |
| Wicofe-Update | `2e9ecfb1ba93d6f6d0175d6fe8bda51ed233397e` | Index installer and update architecture |
| Wicofe-Recovery | `8a8f04a0285b6f9b200614cadd5021ee580d1766` | Document recovery and ports architecture |
| Wicofe-SDK | `b7e4bc62b7d09ebb66ef2c0de7172ada020bdb77` | Index SDK architecture draft |
| Wicofe-Ports | `9257b6e27bee8d9f367b522c29f758dc4a438e77` | Document recovery and ports architecture |

## 3. Dependency-manifest discovery

Recursive repository-tree inspection identified Cargo manifests in four repositories:

| Repository | Cargo.toml files observed | Additional evidence |
|---|---:|---|
| Wicofe-Kernel | 2 | Kernel workspace and kernel crate |
| Osynit | 2 | Workspace and core crate |
| WDE | 11 | Multi-crate Rust workspace |
| Mysh | 1 | Standalone Rust package and Cargo.lock |

This is a source-tree discovery snapshot, not a resolved dependency inventory. Wicofe-Tools separately contains Python audit tooling and workflows; Wicofe-Build and other repositories contain build/workflow dependencies even where no Cargo manifest exists. The strict cross-repository auditor also inspects build scripts, GitHub Actions, host package installs, runner images, assets and submodules.

## 4. Change-specific documentation status

### Osynit integration

The canonical design authority is [Osynit System Specification 0.1](https://github.com/Waizusora/Osynit/blob/main/docs/OSYNIT_SYSTEM_SPEC_0.1.md). The cross-repository Core Init boundary and boot/service integration are coordinated in [Wicofe-Specs](https://github.com/Waizusora/Wicofe-Specs/tree/main/boot).

The specification explicitly records an accepted design baseline while implementation remains partial/prototype. Native PID 1, complete IPC/CLI and bootable integration must not be inferred from documentation-only commits.

### Mysh pipeline execution

The latest source implements connected kernel pipes and concurrent draining of every child stderr stream plus the final stdout stream for pipelines made entirely of simple external commands. Pipelines involving in-process built-ins, functions, compound commands or unresolved commands still use a sequential buffered fallback. Compound stages in that fallback do not yet receive input from the preceding stage. Documentation was corrected to preserve this distinction.

### WDE and kernel licensing

WDE's latest CI change pins the Rust toolchain/action sources and inventories installed system package licenses. Wicofe-Kernel's CI and licensing documentation identify GPL-2.0-or-later QEMU and xorriso host tools as REJECTED under Policy 0.2; they remain present pending validated replacements and are release blockers. Do not remove them before boot/ISO parity tests and a permitted replacement are available.

### Third-party and build integration

Wicofe-ThirdParty contains Limine source/license evidence and the current kernel host-tool review. Wicofe-Build contains a reusable strict dependency gate that invokes the Wicofe-Tools cross-repository workflow at an immutable workflow revision and pins the auditor source separately. This does not yet establish a completed end-to-end image publication gate.

## 5. CI evidence checked

| Repository | Workflow run | Result | Verified scope |
|---|---|---|---|
| Wicofe-Tools | [43878335350](https://github.com/Waizusora/Wicofe-Tools/actions/runs/43878335350) | SUCCESS | Tooling CI |
| Wicofe-Tools | [43878335263](https://github.com/Waizusora/Wicofe-Tools/actions/runs/43878335263) | SUCCESS | Local dependency auditor and unit-test workflow |
| Wicofe-Tools | [43878335380](https://github.com/Waizusora/Wicofe-Tools/actions/runs/43878335380) | FAILURE (expected strict block) | 29-repository audit; two GPL rejects, unresolved approvals and UNKNOWN coverage |
| Mysh | [43878047450](https://github.com/Waizusora/Mysh/actions/runs/43878047450) | SUCCESS | Rust quality checks, Android ARM64/x86-64 builds and smoke tests, Linux musl ARM64/x86-64 builds/tests |
| Osynit | [43878064271](https://github.com/Waizusora/Osynit/actions/runs/43878064271) | SUCCESS | Rust CI on the documentation-index cleanup commit |
| WDE | [43878701227](https://github.com/Waizusora/WDE/actions/runs/43878701227) | SUCCESS | WDE CI after its licensing audit-status documentation update |

## 6. Verification boundaries

- GitHub default-branch commit and tree reads succeeded for all 29 repositories.
- The dependency audit artifact is a separate point-in-time snapshot. Its recorded repository revisions must not be conflated with the newer commit table above.
- Documentation changes were committed and fetched back from GitHub before being recorded here.
- The selected CI runs above are verified; they do not establish that every repository or every release target builds and tests successfully.
- No hardware boot test or final-image SBOM reconciliation was performed in this audit.
- A successful local dependency-auditor CI run does not imply that the strict cross-repository audit passes.

## 7. Post-snapshot documentation-only follow-ups

The following documentation changes were made after the main commit survey and strict-audit snapshot. They do not alter dependency resolution inputs; WDE's CI was re-run after its licensing status note and completed successfully.

- WDE licensing status note: `c15da9e096822ac25a86235002b978ca8d781a31`.
- Wicofe-Docs dependency report refresh and review-queue link: `d026f5bd7f7863d1b84c9f5902cd25e080b63d49`.
- Wicofe-ThirdParty dependency review queue and index link: `8995c332f396e50a60652f973070a5e7668ef332`.
- Wicofe-ThirdParty verified Bochs 3.1 and PyCdlib 1.22.0 release tags, exact LGPL-2.1 evidence and replacement-review notes: `6aa13b76e0ccca70b1ed9108c0fe417bc9322ed9`.

## 8. Next work

1. Re-run strict cross-repository audit against the current 29 default-branch heads after the latest documentation commits.
2. Replace or explicitly resolve the two prohibited GPL host tools in Wicofe-Kernel without losing ISO generation and boot-validation coverage.
3. Review all LGPL/copy-left candidates, including exact version, link method, source/relinking obligations, notices and replacement tests.
4. Complete human review for the 241 NEEDS_REVIEW dependency/build-time records and investigate the UNKNOWN records from the latest evidence artifact.
5. Resolve non-Cargo ecosystems, system package closure, vendored assets and final-image SBOM coverage.
6. Update the dependency report and Wicofe-ThirdParty inventory from the refreshed artifact; do not claim Wicofe-wide compliance until release-image reconciliation passes.
