# Wicofe License and Third-Party Policy

**Status:** Project policy summary. The authoritative dependency rules are maintained in Wicofe-ThirdParty.

## Project-wide principles

Wicofe is a Unix-like, POSIX-compatible, non-GNU alternative. Native software must use Wicofe interfaces and must not require Linux libc, GNU libc, musl-for-Linux, Linux binary compatibility, or GNU compatibility layers. See the canonical [Wicofe Project Principles](PROJECT_PRINCIPLES.md).

## Original project material

The project-wide default for original Wicofe source code is MPL-2.0 unless a repository explicitly documents a different license. Each repository must carry the applicable license text and preserve required notices. Do not infer a license solely from a project-wide statement.

## Approved repository-specific license exception

- [Wlibc](https://github.com/Waizusora/WLibc) licenses original Wlibc-authored
  code and documentation under MIT. This is an explicit, project-owner-approved
  exception to the project-wide MPL-2.0 default.
- Imported musl source retains the upstream MIT license and copyright notices.
  File-level and bundled third-party components retain their own applicable
  notices and terms. The Wlibc repository-level MIT license does not relicense
  third-party material.
- The exact upstream revision and component-level provenance audit are required
  before importing musl source.

## Binding dependency license rules

The canonical [Wicofe Dependency License Policy 0.2](https://github.com/Waizusora/Wicofe-ThirdParty/blob/main/policies/DEPENDENCY_LICENSE_POLICY_0.2.md) applies to all Wicofe repositories, direct/transitive dependencies, build tools and shipped assets:

- **GPL and AGPL:** avoided and prohibited for normal project integration.
- **Permissive licenses:** preferred when suitable, including MIT, BSD, ISC, Apache-2.0 and Zlib.
- **LGPL:** considered only when no technically and legally suitable permissive alternative exists, after exact-version review and explicit project-owner approval.
- **Other licenses:** require review of exact terms, compatibility and obligations; copyleft licenses other than GPL/AGPL require explicit project-owner approval where applicable.
- **Other copyleft, custom, proprietary or ambiguous terms:** require careful compatibility review and explicit project-owner approval.
- **Unknown, ambiguous or incomplete license evidence:** blocked pending review.

The policy applies to direct and transitive dependencies, build tools, firmware, fonts, codecs, generated code and other shipped assets. A successful build does not constitute license approval.

## Reuse and original implementation

Wicofe encourages original implementations where practical, but does not require difficult components to be recreated from scratch. Reuse or fork an upstream project when that is the safer and more maintainable choice, provided its license and architecture meet Wicofe policy and it is adapted to native Wicofe interfaces.

## Third-party material

Third-party code, generated files, specifications, fonts, firmware, binary blobs and documentation retain their applicable upstream terms. Do not relicense them as MPL-2.0 merely because they are stored in a Wicofe repository.

Record upstream identity, exact version/commit and hashes, license evidence, notices, dependency closure, modifications, enabled features, target architectures and security status.

## Notices and source availability

Preserve upstream copyright notices, license texts, attribution, source-distribution obligations and modification notices as required by the applicable license. A dependency inventory is not a substitute for shipping required notices.

This document summarizes engineering policy and is not legal advice. Ambiguous or high-impact licensing cases require qualified review.
\n\n## Dependency audit implementation status\n\nThe initial Dependency License Auditor is maintained in [Wicofe-Tools](https://github.com/Waizusora/Wicofe-Tools/blob/main/docs/DEPENDENCY_LICENSE_AUDITOR.md). It currently resolves Cargo metadata and discovers other manifest ecosystems. This is not a declaration of repository-wide compliance: non-Cargo resolvers, vendored/source assets, build outputs and final image inventories remain subject to audit. Policy 0.2 remains authoritative.\n