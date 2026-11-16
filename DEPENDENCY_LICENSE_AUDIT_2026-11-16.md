# Wicofe OS Dependency License Audit — 2026-11-16

**Policy authority:** [Wicofe Dependency License Policy 0.2](https://github.com/Waizusora/Wicofe-ThirdParty/blob/main/policies/DEPENDENCY_LICENSE_POLICY_0.2.md)  
**Scope:** Canonical 29 repositories in Waizusora  
**Implementation:** Wicofe-Tools Dependency License Auditor  
**Latest completed evidence snapshot in this report:** [GitHub Actions run 43877691846](https://github.com/Waizusora/Wicofe-Tools/actions/runs/43877691846)  
**Artifact:** [29-repository JSON/Markdown reports and Cargo metadata](https://github.com/Waizusora/Wicofe-Tools/actions/runs/43877691846/artifacts/14231895200)  
**Result:** BLOCKED — prohibited GPL build tools, unreviewed dependencies, unknown evidence and incomplete coverage remain.

## 1. Executive summary

The cross-repository workflow checked out all 29 repositories and generated a per-repository report. The strict audit failed closed. This is the expected result while prohibited or unapproved dependencies and incomplete evidence remain.

| Finding | Result |
|---|---:|
| Repositories checked out and revision-recorded | 29 / 29 |
| Repositories with resolved Cargo manifests | 4 |
| Cargo.toml manifests | 16 |
| Transient Cargo.lock files generated in CI | 4 |
| Total dependency/build-time records | 347 |
| NEEDS_REVIEW | 244 |
| UNKNOWN | 101 |
| REJECTED | 2 |
| GitHub Actions records | 22 |
| Build-tool command records | 72 |
| System-package records | 14 |
| Build-script command records | 12 |
| Runner-image records | 6 |
| Rust toolchain records | 3 |
| Downloaded artifact records | 1 |
| Known asset records | 2 (both UNKNOWN) |
| Git submodule records | 0 |
| Build-script/workflow scan records | 14 (9 NEEDS_REVIEW, 5 DISCOVERED) |

The 347 records are not 347 independent Cargo crates. They include resolved Rust packages, GitHub Actions, host system packages, build commands, runner images, toolchains and downloaded artifacts. Security and maintenance status have not been completed for every record.

## 2. Dependency results by repository

| Repository | Records | NEEDS_REVIEW | UNKNOWN | REJECTED |
|---|---:|---:|---:|---:|
| Wicofe-Kernel | 45 | 7 | 36 | 2 |
| WDE | 239 | 220 | 19 | 0 |
| Mysh | 32 | 9 | 23 | 0 |
| Osynit | 8 | 3 | 5 | 0 |
| Wicofe-Tools | 22 | 4 | 18 | 0 |
| Wicofe-Build | 1 | 1 | 0 | 0 |
| Other 23 repositories | 0 | 0 | 0 | 0 |

The 23 repositories with zero emitted dependency records are **not approved as dependency-free**. Their repository coverage remains UNKNOWN until source/build/asset inspection is complete and a scoped human no-dependency attestation is recorded. The 25 repositories without resolved Cargo manifests must not be treated as PASS.

## 3. Cargo dependency closure

Cargo metadata was resolved for:
- Wicofe-Kernel
- Osynit
- WDE
- Mysh

The workflow found 16 Cargo.toml files across those four repositories. It generated four transient Cargo.lock files in disposable CI checkouts where no committed lockfile existed. These lockfiles were uploaded as evidence and were not committed to the source repositories.

The audit artifact contains 217 Cargo dependency records. The graph includes direct/transitive relationships, enabled feature contexts, dependency kinds, package source identifiers, repository URLs, checksums where available and license metadata/evidence. Package license data and source license files still require human review; the scanner does not grant legal approval.

## 4. Prohibited GPL dependencies

<badge>REJECTED — release blockers</badge>

Two GPL-2.0-or-later host tools were detected in Wicofe-Kernel's `.github/workflows/kernel-check.yml`:

| Dependency | Version | Role | License |
|---|---|---|---|
| `qemu-system-x86` | `1:10.2.1+ds-1ubuntu3.3` | x86-64 BIOS boot test | GPL-2.0-or-later |
| `xorriso` | `1:1.5.6-1.1ubuntu4` | ISO generation and notice inspection | GPL-2.0-or-later |

They are build/test environment packages and are not copied into the Wicofe ISO. Policy 0.2 does not define a build-only exception, so both remain REJECTED. Their removal is deferred until a permitted replacement preserves the boot and ISO workflows and passes parity tests.

Candidate replacements recorded for review:
- QEMU: Bochs (LGPL-2.1; explicit LGPL review/approval required; x86-only).
- xorriso: cdrtools/mkisofs (CDDL-1.0; explicit other-copyleft review/approval required) or libisofs/libburn (LGPL-family; linking/relinking and notice obligations require review).

No candidate is approved by this report. The current Wicofe-Kernel CI path remains blocked pending replacement validation or an explicit policy-owner decision.

## 5. GitHub Actions and build-time dependencies

The scan found 22 GitHub Actions records across six repositories: Mysh, Osynit, WDE, Wicofe-Kernel, Wicofe-Tools and Wicofe-Build.

Upstream license evidence was collected for selected action revisions, including MIT, Apache-2.0, MIT OR Apache-2.0 and the internal MPL-2.0 reusable Wicofe workflow. All 22 remain NEEDS_REVIEW until scoped project approval, consumer pinning, transitive action review, security and maintenance review are complete.

The remaining 72 build-tool command records, 14 system-package records, 12 build-script command records, six runner-image records, three Rust toolchain records and one downloaded-artifact record also require evidence/review. A pinned action or package version does not establish license approval.

## 6. Vendored assets and final image

Two known vendored source/license files were detected in Wicofe-Kernel under `third_party/licenses/limine-12.9.6/`. Both remain UNKNOWN in the asset inventory because their presence as license documents is not a complete component/source/binary distribution record.

No Git submodules were detected by the current scanner. This does not prove that all firmware, fonts, codecs, schemas, generated code, source bundles or binary assets have been inspected.

Wicofe-Image and Wicofe-Build still need to provide a final image inventory/SBOM and reconcile it with the complete dependency, toolchain, vendored-source and notice inventory.

## 7. CI and release-gate status

The strict cross-repository workflow run [43877691846](https://github.com/Waizusora/Wicofe-Tools/actions/runs/43877691846) completed with **failure**, not success. Its evidence artifact was uploaded successfully. The failure is intentional fail-closed behavior.

The run's checked-out repository revisions are recorded inside each JSON report as `repository_commit`. They are a point-in-time audit snapshot and must not be conflated with later default-branch commits listed in [Repository Change Audit](REPOSITORY_CHANGE_AUDIT_2026-11-16.md).

Wicofe-Build has a reusable/tag-triggered release dependency gate that invokes the Wicofe-Tools strict cross-repository workflow using an immutable workflow revision and a separately pinned auditor source revision. This is not yet a complete end-to-end release pipeline: final-image publication is not fully gated on a successful strict audit and final-image SBOM reconciliation.

## 8. Required follow-up

1. Replace the two rejected GPL host tools with reviewed, permitted alternatives; preserve ISO-generation and x86 boot-validation parity.
2. Review and approve/reject all 244 NEEDS_REVIEW records with exact scope, source revision, license evidence, obligations, notices, security and maintenance status.
3. Investigate all 101 UNKNOWN records; pin toolchain, runner, package and command sources where practical.
4. Complete non-Cargo ecosystem resolvers where manifests are found and record reviewed no-dependency attestations only where justified.
5. Inspect vendored source, submodules, firmware, fonts, codecs, schemas, generated code and binary assets.
6. Reconcile Wicofe-Build outputs and Wicofe-Image final image contents against a complete SBOM and notice bundle.
7. Require a successful strict audit and final-image reconciliation tied to the exact release commit.

**This report does not certify Wicofe OS as license-compliant.**
