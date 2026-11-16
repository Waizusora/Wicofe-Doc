# Wicofe OS Dependency License Audit — 2026-11-16

**Policy authority:** [Wicofe Dependency License Policy 0.2](https://github.com/Waizusora/Wicofe-ThirdParty/blob/main/policies/DEPENDENCY_LICENSE_POLICY_0.2.md)  
**Scope:** Canonical 29 repositories in Waizusora  
**Implementation:** Wicofe-Tools Dependency License Auditor  
**Latest completed cross-repository evidence:** [GitHub Actions run 43881861767](https://github.com/Waizusora/Wicofe-Tools/actions/runs/43881861767)  
**Cross-repository artifact:** [JSON/Markdown reports and Cargo metadata — artifact 14233016601](https://github.com/Waizusora/Wicofe-Tools/actions/runs/43881861767/artifacts/14233016601)  
**Result:** BLOCKED — prohibited GPL dependencies, unreviewed records, unknown evidence and incomplete coverage remain.

## 1. Executive summary

The cross-repository workflow checked out all 29 repositories and generated per-repository reports. The strict audit failed closed.

| Cross-repository source/build finding | Result |
|---|---:|
| Repositories checked out and revision-recorded | 29 / 29 |
| Repositories with resolved Cargo manifests | 4 |
| Cargo.toml manifests | 16 |
| Transient Cargo.lock files generated in CI | 4 |
| Total source/build dependency records | 347 |
| NEEDS_REVIEW | 243 |
| UNKNOWN | 102 |
| REJECTED | 2 |
| PASS / APPROVED_WITH_CONDITIONS | 0 |
| Cargo dependency records | 217 |
| GitHub Actions records | 22 |
| Build-tool command records | 72 |
| System-package references from source workflows | 14 |
| Build-script command records | 12 |
| Runner-image records | 6 |
| Rust toolchain records | 3 |
| Downloaded-artifact records | 1 |
| Known asset records | 2 (both UNKNOWN) |
| Git submodule records | 0 |

The 347 records are not all Cargo crates. They include resolved Rust packages, GitHub Actions, host system package references, build commands, runner images, toolchains and downloaded artifacts. Security and maintenance status have not been completed for every record.

Six repositories emitted dependency/build-time records: Wicofe-Kernel (45), WDE (239), Mysh (32), Osynit (8), Wicofe-Tools (22) and Wicofe-Build (1 UNKNOWN). The other 23 repositories emitted no dependency records in this run; that is not a no-dependency approval. Their coverage remains UNKNOWN until source/build/asset inspection is complete and a scoped human attestation is recorded where justified.

## 2. Cargo dependency closure

Cargo metadata was resolved for Wicofe-Kernel, Osynit, WDE and Mysh. The workflow found 16 Cargo.toml files and generated four transient Cargo.lock files in disposable CI checkouts where no committed lockfile existed. Those lockfiles were uploaded as evidence and were not committed to source repositories.

The 217 Cargo records include direct/transitive relationships, enabled feature contexts, dependency kinds, package source identifiers, repository URLs, checksums where available and license metadata/evidence. Package license metadata and source license files still require human review; the scanner does not grant legal approval.

## 3. Prohibited GPL dependencies in the source/build graph

Two direct GPL host-tool records were detected in Wicofe-Kernel CI:

| Dependency | Version | Role | License |
|---|---|---|---|
| `qemu-system-x86` | `1:10.2.1+ds-1ubuntu3.3` | x86-64 BIOS boot test | Upstream source evidence: GPL-2.0-or-later; package copyright also contains a non-SPDX `GPL2-or-LGPL2-with-additions` expression that needs file/binary mapping |
| `xorriso` | `1:1.5.6-1.1ubuntu4` | ISO generation and ISO notice inspection | GPL-2.0-or-later |

They are build/test environment packages and are not copied into the Wicofe ISO. Policy 0.2 has no build-only exception. Both remain blocked. The QEMU package-level license expression requires reconciliation with its upstream GPL source evidence; it is not approved while that discrepancy is unresolved.

## 4. Additional CI system-package closure evidence

The source/build scanner does not install every repository's host dependencies. Repository-specific CI workflows therefore upload separate package-delta inventories. These are additional evidence snapshots and are **not included in the 347-record cross-repository total**.

### Wicofe-Kernel

[Kernel CI run 43881542034](https://github.com/Waizusora/Wicofe-Kernel/actions/runs/43881542034) completed successfully and uploaded [system package evidence artifact 14231614886](https://github.com/Waizusora/Wicofe-Kernel/actions/runs/43881542034/artifacts/14231614886).

| Package inventory status | Count |
|---|---:|
| Installed package records | 103 |
| REJECTED | 15 |
| NEEDS_REVIEW | 84 |
| UNKNOWN | 4 |

The 15 REJECTED package records are `cpu-checker`, `ipxe-qemu`, `libburn4t64`, `libcdparanoia0`, `libfdt1`, `libfftw3-single3`, `libiscsi7`, `libisoburn1t64`, `libisofs6t64`, `libv4l-0t64`, `libv4lconvert0t64`, `libvte-2.91-0`, `libvte-2.91-common`, `msr-tools` and `xorriso`. The artifact contains exact versions and Debian copyright evidence.

The 103 records are the installed package delta, not a proven minimal direct/transitive/recommended closure. Package dependency edges and actual tool usage still need mapping. The xorriso stack includes GPL packages `libburn4t64`, `libisoburn1t64` and `libisofs6t64`. Other records require direct/transitive/recommended relationship mapping.

Three multi-license expressions were held at NEEDS_REVIEW rather than auto-rejected:
- `ipxe-qemu-256k-compat-efi-roms`: GPL-2+ OR UBDL.
- `libflac14`: GPL-2+ OR LGPL-2.1+.
- `librdmacm1t64`: BSD-MIT OR GPL-2.

Sixty-three package records contain LGPL declarations in their copyright metadata: 27 have primary category LGPL, 26 are MIXED_REVIEW, three are OTHER_REVIEW and seven are REJECTED because their primary/required license is GPL. All non-rejected LGPL/mixed records remain NEEDS_REVIEW; the seven GPL-required records remain REJECTED. The QEMU package family contains a non-SPDX `GPL2-or-LGPL2-with-additions` expression. The source-level scanner conservatively rejects QEMU based on upstream COPYING evidence; the package-level records remain NEEDS_REVIEW pending file/binary-level mapping. QEMU remains blocked.

The same run verified formatting, unit tests, x86-64 build, Limine ISO generation, ISO notice presence, QEMU BIOS boot and AArch64 target checks. Successful execution does not waive license blockers.

### WDE

[WDE CI run 43881760690](https://github.com/Waizusora/WDE/actions/runs/43881760690) completed successfully and uploaded [system package evidence artifact 14232651762](https://github.com/Waizusora/WDE/actions/runs/43881760690/artifacts/14232651762).

| Package inventory status | Count |
|---|---:|
| Installed package records | 32 |
| REJECTED | 0 |
| NEEDS_REVIEW | 19 |
| UNKNOWN | 13 |

Fourteen GLVND/Mesa package records have MIT as the primary `Files: *` license but also contain GPL-3+ declarations in non-default copyright stanzas. They remain NEEDS_REVIEW until the installed binary payload is mapped to the relevant copyright stanzas.

The 13 UNKNOWN package identities are `libx11-dev`, `libxau-dev`, `libxcb1-dev`, `libxcursor-dev`, `libxext-dev`, `libxfixes-dev`, `libxi-dev`, `libxinerama-dev`, `libxkbcommon-dev`, `libxrandr-dev`, `libxrender-dev`, `xorg-sgml-doctools` and `xtrans-dev`. Their exact source package/license evidence remains incomplete.

## 5. LGPL-bearing optional license alternatives

The WDE Cargo graph contains two `r-efi` versions with the expression `MIT OR Apache-2.0 OR LGPL-2.1-or-later`:

| Package | Version | Parent | Target condition |
|---|---|---|---|
| `r-efi` | 5.3.0 | `getrandom 0.3.4` | UEFI target with `getrandom_backend = "efi_rng"` |
| `r-efi` | 6.0.0 | `getrandom 0.4.3` | UEFI target with `getrandom_backend = "efi_rng"` |

These are target-conditioned transitive edges captured by all-target metadata, not evidence that the current Linux WDE build links an LGPL library. The supported target matrix and an explicit selected license branch still require review. The scanner does not select MIT/Apache automatically and does not treat the LGPL alternative as approved.

## 6. GitHub Actions and build-time dependencies

The scan found 22 GitHub Actions dependency records across Mysh, Osynit, WDE, Wicofe-Kernel, Wicofe-Tools and Wicofe-Build. Upstream license evidence was collected for selected action revisions, including MIT, Apache-2.0, MIT OR Apache-2.0 and the internal MPL-2.0 reusable Wicofe workflow. All remain NEEDS_REVIEW until scoped project approval, consumer pinning, transitive action review, security and maintenance review are complete.

The remaining 72 build-tool command records, 14 system-package references, 12 build-script command records, six runner-image records, three Rust toolchain records and one downloaded-artifact record also require evidence/review. A pinned action or package version does not establish license approval.

## 7. Vendored assets and final image

Two known vendored source/license files were detected in Wicofe-Kernel under `third_party/licenses/limine-12.9.6/`. Both remain UNKNOWN as asset records because their presence as license documents is not a complete component/source/binary distribution record.

No Git submodules were detected by the current scanner. This does not prove that all firmware, fonts, codecs, schemas, generated code, source bundles or binary assets have been inspected.

Wicofe-Image and Wicofe-Build still need to provide a final image inventory/SBOM and reconcile it with the complete dependency, toolchain, vendored-source and notice inventory.

## 8. CI and release-gate status

The strict cross-repository workflow [43881861767](https://github.com/Waizusora/Wicofe-Tools/actions/runs/43881861767) completed with **failure**, not success. Its evidence artifact was uploaded successfully. The failure is fail-closed behavior while the prohibited and unapproved records remain.

Wicofe-Tools local CI, auditor unit tests and local inventory generation passed on the reviewed revision. That does not mean the 29-repository strict audit passes.

Wicofe-Build has a reusable/tag-triggered release dependency gate that invokes the Wicofe-Tools strict cross-repository workflow using an immutable workflow revision and a separately pinned auditor source revision. This is not yet a complete end-to-end release pipeline: final-image publication is not fully gated on a successful strict audit, per-repository system-package artifacts are not yet automatically reconciled by the cross-repository gate, and final-image SBOM reconciliation remains outstanding.

## 9. Required follow-up

1. Replace the rejected GPL host tools and their GPL-only package closure with reviewed permitted alternatives; preserve ISO generation and boot-validation parity.
2. Resolve the QEMU package-level custom license expression against upstream source/file/binary evidence.
3. Review and approve/reject all 243 NEEDS_REVIEW source/build records and all 84 Kernel CI package records with exact scope, source revision, license evidence, obligations, notices, security and maintenance status.
4. Investigate all 102 UNKNOWN source/build records and all four Kernel CI UNKNOWN package records.
5. Resolve the 13 WDE UNKNOWN package records and 19 WDE NEEDS_REVIEW package records.
6. Complete non-Cargo ecosystem resolvers where manifests are found and record reviewed no-dependency attestations only where justified.
7. Inspect vendored source, submodules, firmware, fonts, codecs, schemas, generated code and binary assets.
8. Reconcile Wicofe-Build outputs and Wicofe-Image final image contents against a complete SBOM and notice bundle.
9. Require a successful strict audit and final-image reconciliation tied to the exact release commit.

See the [detailed Wicofe-ThirdParty review queue](https://github.com/Waizusora/Wicofe-ThirdParty/blob/main/DEPENDENCY_REVIEW_QUEUE_2026-11-16.md) for package-level GPL, LGPL, optional-license and UNKNOWN lists.

**This report does not certify Wicofe OS as license-compliant.**
