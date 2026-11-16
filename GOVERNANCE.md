# Wicofe Project Governance

**Status:** Draft 0.1

This document describes project-wide governance. Component-specific technical authority remains with the owning repository.

## Repository ownership

- **Wicofe-ABI:** syscall and userspace ABI definitions and compatibility policy.
- **Wicofe-Kernel:** kernel architecture and implementation, VFS mechanisms, driver core, and privileged DKM interfaces.
- **ONWFS:** native filesystem on-disk format, filesystem implementation, and format-specific tooling. **Wicofe-Storage** owns system-level storage discovery, partition workflows, mount orchestration, and administrative tools.
- **Component repositories:** their own implementation, local tests, build instructions, and component-specific documentation.
- **Wicofe-Specs:** cross-component specifications and specification index; it does not silently override component-owned interfaces.
- **Wicofe-Tests:** cross-repository conformance and integration tests.
- **Wicofe-Docs:** project-wide explanatory documentation and governance.
- **Wicofe-Tools:** shared development and validation tooling.
- **Wicofe-ThirdParty:** upstream provenance, license records, patches, and dependency maintenance metadata.

The [repository map](https://github.com/Waizusora/Wicofe/blob/main/docs/REPOSITORY_MAP.md) is the authoritative inventory. If this summary conflicts with a component's accepted specification or repository map, raise a governance issue rather than guessing.

## Change authority

Changes confined to one component should be reviewed in that component repository. Changes crossing repository boundaries must identify all affected owners and include an interface or migration impact analysis.

Changes to syscall ABI, DKM ABI, boot protocol, filesystem on-disk format, or shared data structures require a versioned specification or an explicit proposal before implementation is treated as stable.

## Proposal lifecycle

Use these labels consistently:

- **Draft:** incomplete working material.
- **Proposed:** ready for technical review; not binding.
- **Accepted:** approved design; not proof of implementation.
- **Deprecated:** retained temporarily but discouraged.
- **Superseded:** replaced by a newer decision or specification.

Implementation state and verification state must be recorded separately from specification lifecycle. An accepted design does not imply implemented code or passing tests. Use the [Wicofe-Specs traceability policy](https://github.com/Waizusora/Wicofe-Specs/blob/main/governance/SPECIFICATION_TRACEABILITY_POLICY_0.1.md) for the shared model.

## Review and evidence

Pull requests should state scope, affected repositories, compatibility impact, test commands, observed results, and known limitations. Cross-repository changes should link related pull requests or commits.

Architecture support claims must distinguish cross-compilation, emulator execution, and physical-hardware validation.

## Licensing

Original Wicofe components target MPL-2.0 unless a repository explicitly states otherwise. Third-party components retain their upstream licenses and notices. See [LICENSE_POLICY.md](LICENSE_POLICY.md). This policy is project guidance, not legal advice.
