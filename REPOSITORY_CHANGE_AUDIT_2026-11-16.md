# Wicofe Cross-Repository Change Audit — 2026-11-16

**Scope:** All 29 repositories in `Wicofe-Tools/config/repository_inventory.txt`  
**Branch inspected:** Default branch (`main` for all 29 repositories)  
**Snapshot:** 2026-11-16, 14:03:46 UTC, from cross-repository audit run 43881861767 (later documentation-only follow-ups listed below)  
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

The SHA column records the exact commit observed by the 29-repository audit run 43881861767. Subsequent documentation-only commits are listed in §7 and do not change the dependency graph captured by that run.

| Repository | Main HEAD | Latest observed change |
|---|---|---|
| Wicofe | `56ccdb80b1fabd5cb4f1286fbe8889d8af29ed53` | Standardize project name as Osynit |
| Wicofe-Docs | `7dbd536be99baeebe29111ac8fda4a50c79e19e7` | Record latest 29-repository change audit |
| Wicofe-Specs | `a9e86236617bfc00489eaacaaf507f0506b048d5` | Remove duplicate Osynit contract index entries |
| Wicofe-Tests | `6210042246ce0d3553dd852df4e0358019085dce` | Standardize project name as Osynit |
| Wicofe-Tools | `fd10793b4fe6e8311cf016042e67fe7ec635923e` | Fix tooling index and list dependency audit docs |
| Wicofe-ThirdParty | `2b2ed2baabe6eb88a549fa056826dc3fc0d2c3c1` | Document Limine release license inclusion and notices |
| Wicofe-Kernel | `8986aa49192ddc9e03aacb20ebae666022515fa7` | Remove duplicate Osynit documentation index entry |
| Wicofe-ABI | `cab3cc6fd8c05f27e7862147f30a087a852f94e5` | Standardize project name as Osynit |
| Wicofe-Drivers | `7c3d05e8dec0cd66c103491d8b04f7e6c3877953` | Index driver subsystem design |
| Wicofe-Storage | `b42c7f75ff3c1ef93a7af06e7246792c68b73c4e` | Index storage management design |
| ONWFS | `ae06ce4178dd8cecb7ec47ea5d0f5715dadb0339` | Clarify ordered-data overwrite limitations |
| Wicofe-Lib | `cda650b19eef95463bf41596ecfa02e512571e77` | Index Rust userspace library architecture |
| Wicofe-Libc | `0d7314819ec66ca36bd06ff712250a4cb37c3fc4` | Index C runtime porting architecture |
| Osynit | `1b983d09963556b928631f78d411dde000af5809` | Format supervisor duplicate-event assertion |
| Wicofe-Services | `4121d9b0a1090088df0c4243ad4ff7ed249c9181` | Standardize project name as Osynit |
| Wicofe-Network | `a003e296eba39356d510f38da3077042da3b9f20` | Index userspace networking architecture |
| Wicofe-Input | `2e8220baaf3f88a085d6dd5890e2c95b2b3905ab` | Index input subsystem architecture |
| Wicofe-Graphics | `2e66c3270dc4ea3ea9ed44ef9c8987864ca183a9` | Index graphics architecture draft |
| Wicofe-Audio | `ce8237a6c94093a378e8ca9388a5a5ce211d0369` | Index audio architecture draft |
| WDE | `ee8f12326ebb7054668bab31a5b89432dfffbf8e` | Pin CI actions and inventory apt package licenses |
| WPM | `184d483bce67c377b8e4fc9581fb0116b5ce954f` | Link package manager documentation index |
| Mysh | `f84227e3dfb2a0fe8154003b63997d3f32a9652f` | Document concurrent external pipeline execution |
| Wicofe-Build | `3d7a9fbd13aa1028eac9c33c776d878a60943896` | Remove duplicate Osynit documentation index entry |
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
| Wicofe-Tools | [43881861725](https://github.com/Waizusora/Wicofe-Tools/actions/runs/43881861725) | SUCCESS | Tooling metadata CI |
| Wicofe-Tools | [43881861746](https://github.com/Waizusora/Wicofe-Tools/actions/runs/43881861746) | SUCCESS | Dependency auditor unit tests and local inventory generation |
| Wicofe-Tools | [43881861874](https://github.com/Waizusora/Wicofe-Tools/actions/runs/43881861874) | SUCCESS | Cross-repository baseline validation and checkout inventory |
| Wicofe-Tools | [43881861767](https://github.com/Waizusora/Wicofe-Tools/actions/runs/43881861767) | FAILURE (expected strict block) | 29-repository audit; 2 direct GPL rejects, 243 NEEDS_REVIEW and 102 UNKNOWN |
| Mysh | [43878047450](https://github.com/Waizusora/Mysh/actions/runs/43878047450) | SUCCESS | Rust quality checks, Android ARM64/x86-64 builds and smoke tests, Linux musl ARM64/x86-64 builds/tests |
| Osynit | [43878064271](https://github.com/Waizusora/Osynit/actions/runs/43878064271) | SUCCESS | Rust CI on the documentation-index cleanup commit |
| WDE | [43882021012](https://github.com/Waizusora/WDE/actions/runs/43882021012) | SUCCESS | CI with the corrected pinned package-license auditor; [system-package artifact 14231069939](https://github.com/Waizusora/WDE/actions/runs/43882021012/artifacts/14231069939) |
| Wicofe-Kernel | [43882011372](https://github.com/Waizusora/Wicofe-Kernel/actions/runs/43882011372) | SUCCESS | x86-64 build, ISO generation/notice check, QEMU boot, AArch64 check; [package artifact 14232692459](https://github.com/Waizusora/Wicofe-Kernel/actions/runs/43882011372/artifacts/14232692459) |

## 6. Verification boundaries

- GitHub default-branch commit and tree reads succeeded for all 29 repositories.
- The dependency audit artifact is a separate point-in-time snapshot. Its recorded repository revisions must not be conflated with the newer commit table above.
- Documentation changes were committed and fetched back from GitHub before being recorded here.
- The selected CI runs above are verified; they do not establish that every repository or every release target builds and tests successfully.
- No hardware boot test or final-image SBOM reconciliation was performed in this audit.
- A successful local dependency-auditor CI run does not imply that the strict cross-repository audit passes.

## 7. Post-snapshot documentation-only follow-ups

The following changes were made after the 14:03:46 UTC repository snapshot. They update documentation/evidence links or CI pin references; they do not change the Cargo dependency graphs captured by run 43881861767.

- Wicofe-Kernel licensing documentation with the latest package artifact reference: `9834a073b3245057882984a76c4576ce941d64ec`.
- WDE licensing documentation with the latest cross-repository snapshot and package artifact reference: `0284f943b70a6d0db9ac726b8998de7aff12b514`.
- Wicofe-Docs dependency audit report refreshed to the latest cross-repository artifact: `a6f065cde51204bb18db677fb8f687a4fb8a0c5a`.
- Wicofe-ThirdParty dependency review queue refreshed with package closure, LGPL, mixed-license and UNKNOWN identities: `fcdc85b9dc38ed3d71461413f81460f912ae44eb`.
- Wicofe-ThirdParty AUDIT synchronized with latest CI package closure and replacement candidate evidence: `7196dcedc43bddd80767b92ed5b9dc23a92a8f78`.

## 8. Next work

1. Re-run strict cross-repository audit against the current 29 default-branch heads after the latest documentation commits.
2. Replace or explicitly resolve the two prohibited GPL host tools in Wicofe-Kernel without losing ISO generation and boot-validation coverage.
3. Review all LGPL/copy-left candidates, including exact version, link method, source/relinking obligations, notices and replacement tests.
4. Complete human review for the 241 NEEDS_REVIEW dependency/build-time records and investigate the UNKNOWN records from the latest evidence artifact.
5. Resolve non-Cargo ecosystems, system package closure, vendored assets and final-image SBOM coverage.
6. Update the dependency report and Wicofe-ThirdParty inventory from the refreshed artifact; do not claim Wicofe-wide compliance until release-image reconciliation passes.
