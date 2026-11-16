# Wicofe License and Third-Party Policy

**Status:** Project policy summary — authoritative dependency rules are maintained in Wicofe-ThirdParty.

## Original project material

The project-wide default for original Wicofe source code is Mozilla Public License 2.0 (MPL-2.0), unless a repository explicitly documents a different license. Each repository must carry the applicable license text and preserve required notices.

The root project/coordination repository may contain documentation, metadata, or links rather than independently licensed implementation code. Its licensing status must be explicit before original code is added; do not infer a license solely from a project-wide statement.

## Binding dependency license rules

The canonical [Wicofe Dependency License Policy 0.1](https://github.com/Waizusora/Wicofe-ThirdParty/blob/main/policies/DEPENDENCY_LICENSE_POLICY_0.1.md) applies to every Wicofe repository, direct and transitive dependencies, build tools and shipped assets:

- **GPL:** prohibited.
- **AGPL:** prohibited.
- **LGPL:** conditionally allowed only when the capability is essential, cannot reasonably be implemented in-house, exact-version legal and technical review passes, obligations are met, and the project owner explicitly approves the scoped use.
- **All other third-party dependency licenses:** not permitted unless the canonical policy is formally amended.
- **Unknown, ambiguous or incomplete license evidence:** blocked.

A dependency is an exception, not a default. Convenience, popularity or faster development are not sufficient reasons to adopt one. Review the full dependency closure, optional features, generated code, firmware, fonts, codecs and other assets.

## Third-party material

Third-party code, generated files, specifications, fonts, firmware, binary blobs, and documentation retain their applicable upstream terms. Do not relicense them as MPL-2.0 merely because they are stored in a Wicofe repository.

Before considering an eligible dependency, record upstream project and canonical source URL, exact version/commit and hashes, SPDX/license evidence, notices, direct and transitive dependencies, local modifications, build/runtime use, enabled features, target architectures and security status.

Use Wicofe-ThirdParty component records and approval workflow. No dependency is approved merely because it builds.

## Notices and source availability

Preserve upstream copyright notices, license texts, attribution, source-offer obligations, and modification notices as required by the applicable license. A dependency inventory is not a substitute for shipping required notices with releases.

## Scope

This document summarizes engineering policy and is not legal advice. LGPL cases require qualified review of the exact version and distribution model before project-owner approval.
