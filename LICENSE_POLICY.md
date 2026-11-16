# Wicofe License and Third-Party Policy

**Status:** Draft 0.1

## Original project material

The project-wide default for original Wicofe source code is Mozilla Public License 2.0 (MPL-2.0), unless a repository explicitly documents a different license. Each repository must carry the applicable license text and preserve required notices.

The root project/coordination repository may contain documentation, metadata, or links rather than independently licensed implementation code. Its licensing status must be explicit before original code is added; do not infer a license solely from a project-wide statement.

## Third-party material

Third-party code, generated files, specifications, fonts, firmware, binary blobs, and documentation retain their applicable upstream terms. Do not relicense them as MPL-2.0 merely because they are stored in a Wicofe repository.

Before adding a dependency, record at minimum:

- Upstream project and canonical source URL.
- Exact version or commit and source checksum where practical.
- SPDX license identifier and included license/notice files.
- Direct and transitive dependencies relevant to redistribution.
- Local modifications and patch rationale.
- Build-time and runtime use, enabled features, and target architectures.
- Known security advisories and maintenance status.

Use Wicofe-ThirdParty/COMPONENT_RECORD_TEMPLATE.md for component records.

## Compatibility review

Review the actual license texts and distribution model before combining or redistributing components. Pay particular attention to static or dynamic linking, generated code, kernel modules, firmware, binary-only material, and bundled assets.

Do not describe a dependency as compatible, permissive, or safe to redistribute based only on its repository label. Record unresolved questions and defer inclusion until reviewed.

## Notices and source availability

Preserve upstream copyright notices, license texts, attribution, source-offer obligations, and modification notices as required by the applicable license. A dependency inventory is not a substitute for shipping required notices with releases.

## Scope

This document is engineering policy and is not legal advice. When a licensing question materially affects distribution, obtain qualified legal review.
