# Wicofe OS Dependency License Audit — 2026-11-16

**Policy authority:** Wicofe Dependency License Policy 0.2  
**Scope:** Canonical 29 repositories in Waizusora  
**Implementation:** Wicofe-Tools Dependency License Auditor  
**Result:** BLOCKED — audit coverage and human approvals remain incomplete

## Executive summary

The cross-repository workflow successfully checked out all 29 repositories and captured a checked-out commit SHA for each repository. The strict audit correctly failed closed rather than treating missing manifests or unreviewed build-time actions as compliant.

| Finding | Result |
|---|---:|
| Repositories checked out and revision-recorded | 29 / 29 |
| Repositories with resolved Cargo manifest coverage | 4 |
| Repositories with no recognized dependency manifest | 25 |
| Cargo manifests | 16 |
| Transient Cargo lockfiles generated in CI | 4 |
| External Cargo package records | 0 |
| GitHub Actions dependency records | 20 |
| Repositories with GitHub Actions dependencies | 6 |
| Known vendored/binary asset records | 0 |
| Git submodule records | 0 |

## Cargo findings

Cargo metadata was resolved for:
- Wicofe-Kernel
- Osynit
- WDE
- Mysh

These repositories contained 16 Cargo.toml manifests in total. The resolved Cargo graphs contained zero external Cargo package records. Four transient Cargo.lock files were generated in disposable CI checkouts because the source repositories did not have committed lockfiles. They were uploaded as audit evidence and were not committed to source repositories.

The zero Cargo package count is limited to the resolved Cargo graph. It does not cover system packages, external tools, image contents or other dependency ecosystems.

## Build-time GitHub Actions

The scanner found 20 GitHub Actions dependency records across Mysh, Osynit, WDE, Wicofe-Kernel, Wicofe-Tools and Wicofe-Build.

Upstream license evidence was retrieved for the external action references:
- MIT
- Apache-2.0
- MIT OR Apache-2.0

The internal reusable Wicofe-Tools workflow is MPL-2.0. No GPL/AGPL license was identified in this limited set of inspected upstream license files.

All 20 records remain NEEDS_REVIEW. Source/license evidence is not approval. Wicofe-Tools workflows were moved to immutable action commit pins; other consumers still have mutable tag/branch references. Security and maintenance review, transitive dependencies bundled inside actions, and owner approval remain outstanding.

The Wicofe-Build release dependency gate calls the reusable Wicofe-Tools cross-repository workflow at an immutable workflow commit and supplies a separate immutable auditor source commit.

## Coverage findings

Twenty-five repositories had no dependency manifest recognized by the current scanner. Their coverage status is UNKNOWN, not PASS. No human no-dependency attestations have been added.

The scanner also found zero known vendored/binary asset records and zero Git submodules. This is only a result of the currently implemented path/extension checks; it does not prove that all firmware, fonts, codecs, schemas, generated code, source bundles or binary assets have been inspected.

## Strict CI result

**BLOCKED**

The strict cross-repository workflow failed because:
1. 25 repositories have UNKNOWN dependency coverage.
2. 20 GitHub Actions records remain NEEDS_REVIEW.
3. No scoped human approvals or no-manifest coverage attestations have been entered.

This is the intended fail-closed behavior. No dependency was automatically approved and no GPL/AGPL compliance claim is made.

- [GitHub Actions run](https://github.com/Waizusora/Wicofe-Tools/actions/runs/43812088175)
- [Audit evidence artifact](https://github.com/Waizusora/Wicofe-Tools/actions/runs/43812088175/artifacts/14201310393)
- [Wicofe-Tools auditor documentation](https://github.com/Waizusora/Wicofe-Tools/blob/main/docs/DEPENDENCY_LICENSE_AUDITOR.md)
- [Wicofe-ThirdParty CI action evidence inventory](https://github.com/Waizusora/Wicofe-ThirdParty/blob/main/AUDIT.md)

## Remaining work

1. Implement and test resolvers for every non-Cargo ecosystem actually used.
2. Inspect all 25 no-manifest repositories and record evidence-backed coverage attestations only where justified.
3. Review and approve or reject the 20 action records; pin all remaining mutable refs.
4. Audit vendored code, Git submodules, compiler/toolchain downloads and build scripts.
5. Inspect Wicofe-Build outputs and Wicofe-Image final image contents.
6. Reconcile final SBOM, license texts, notices and attribution.
7. Require a successful strict audit and image reconciliation for release authorization.

**This report does not certify Wicofe OS as license-compliant.**
