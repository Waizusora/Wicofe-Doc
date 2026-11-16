# Wicofe Cross-Repository Consistency Audit — 2026-11-16

**Status:** Initial documentation and ownership audit  
**Scope:** 29 Wicofe repositories listed in the central repository map  
**Audit depth:** Repository inventory, README files, documentation indexes, and selected project-level governance/specification documents. This is not a source-code, dependency graph, or exhaustive hyperlink audit.

## 1. Executive summary

The 29-repository documentation inventory is present and the repository ownership model is broadly consistent. All 29 repository README files and their canonical documentation entry points were reviewed. The root Wicofe repository uses `docs/INDEX.md`; Wicofe-Docs uses root `INDEX.md`; the remaining component repositories use `docs/INDEX.md`.

Three ownership/status ambiguities were corrected during this audit:
1. Specification lifecycle is now separate from implementation and verification state.
2. ONWFS format ownership is distinguished from Wicofe-Storage system-level workflows.
3. Kernel DKM loader/ABI ownership is distinguished from concrete driver implementations.

The initial license-policy conflict has been resolved by project-owner decision and recorded in the binding Wicofe Dependency License Policy 0.1. Repository-wide dependency compliance remains unaudited.

No system-wide implementation or CI conformance claim is made.

## 2. Findings

### AUD-2026-01 — Third-party license policy was inconsistent

**Severity:** High  
**Status:** Project decision recorded; known documentation conflicts aligned; repository-wide dependency compliance audit remains open  
**Affected repositories:** All 29 Wicofe repositories; policy authority in Wicofe-ThirdParty

**Decision recorded:** [Wicofe Dependency License Policy 0.1](https://github.com/Waizusora/Wicofe-ThirdParty/blob/main/policies/DEPENDENCY_LICENSE_POLICY_0.1.md).
- GPL: prohibited.
- AGPL: prohibited.
- LGPL: conditionally eligible only when essential, not reasonably implementable in-house, exact-version legal and technical review passes, and the project owner explicitly approves the scoped use.
- All other third-party dependency license families: disallowed unless the policy is formally amended.
- Unknown or incomplete license evidence: blocked.
- Original Wicofe-authored code targets MPL-2.0.

The policy applies to direct and transitive dependencies, build tools and shipped non-code assets. Wicofe-Docs/LICENSE_POLICY.md, Wicofe-ThirdParty README/index/intake architecture, Osynit README, and WDE README/licensing documentation were aligned with the decision. The decision resolves the policy conflict; it does not prove that existing manifests, vendored code, build outputs or release images comply. Those inventories still require inspection.

### AUD-2026-02 — Specification lifecycle previously mixed implementation status

**Severity:** High  
**Status:** Corrected in this audit  
**Affected repository:** Wicofe-Specs

The earlier governance text included **Implemented** among specification lifecycle statuses while also requiring implementation state to be tracked independently. This made a specification's approval state ambiguous.

**Correction committed:**
- Specification lifecycle is now Draft, Proposed, Accepted, Deprecated, or Superseded.
- Implementation state is recorded separately as Not started, In progress, Implemented, or Removed.
- Verification state is recorded separately as Not run, Blocked, Failed, or Passed.
- README, repository-boundary governance, and traceability policy were aligned.

### AUD-2026-03 — ONWFS and system storage ownership wording was ambiguous

**Severity:** Medium  
**Status:** Corrected in this audit  
**Affected repository:** Wicofe-Docs

The project governance document used the phrase “ONWFS / storage component repository,” which could be read as a shared or interchangeable ownership assignment.

**Correction committed:** ONWFS owns its on-disk format, filesystem implementation, and format-specific tooling. Wicofe-Storage owns system-level device discovery, partition workflows, mount orchestration, and administrative tools.

### AUD-2026-04 — Driver implementation and DKM contract ownership was ambiguous

**Severity:** Medium  
**Status:** Corrected in this audit  
**Affected repository:** Wicofe project architecture

The project architecture previously listed “Wicofe-Kernel / Wicofe-Drivers” as a combined owner for driver and DKM interfaces.

**Correction committed:**
- Wicofe-Kernel owns the driver core, DKM loader, and privileged DKM ABI.
- Wicofe-Drivers owns concrete optional driver implementations and driver-specific packaging.

### AUD-2026-05 — Kernel roadmap may lag current implementation evidence

**Severity:** Medium  
**Status:** Open — reconcile against CI and source revisions  
**Affected repositories:** Wicofe, Wicofe-Kernel

The kernel README describes x86-64 boot foundation work including memory-map validation, usable-memory planning, HHDM-backed PMM initialization, and a runtime frame allocate/free smoke test. The project roadmap still lists early physical-memory discovery and allocator work as unchecked.

This may be a partially completed milestone rather than a false status. The roadmap should split the work into verifiable sub-milestones and link the exact source/CI evidence before changing checkboxes. The broader PMM remains limited; the kernel README explicitly states that it is single-core and not yet available for general kernel allocations.

### AUD-2026-06 — Requirement IDs and test traceability are not yet demonstrated project-wide

**Severity:** Medium  
**Status:** Open — adoption work required  
**Affected repositories:** Wicofe-Specs, Wicofe-Tests, all component repositories

The new policy and test matrix define stable requirement IDs and a traceability chain, but the current audit did not assign or verify IDs for every normative requirement in every component specification.

**Recommended resolution:** Roll out IDs incrementally, starting with boot handoff, userspace ABI, DKM, VFS, ONWFS journal, storage destructive operations, package/update trust, and recovery. Each test must reference the exact requirement and specification revision.

## 3. Repository inventory and navigation review

The central map lists 29 Wicofe repositories. The authenticated GitHub inventory also contains unrelated repositories; those were not counted as Wicofe components.

Reviewed:
- All 29 Wicofe README files.
- The root project and central documentation indexes.
- Component `docs/INDEX.md` files for the component repositories.
- Selected governance, architecture, roadmap, ONWFS, kernel, licensing, and specification documents.

The central map's repository ownership groupings are broadly aligned with the README/index descriptions. No confirmed missing component README or canonical documentation index was found in this pass.

**Link-check limitation:** This audit did not perform an exhaustive HTTP/404 check of every Markdown link or inspect every linked technical document. The presence of a link in a README/index is not proof that every target is valid. A separate automated link-validation run is still required.

## 4. Architecture and status consistency

The following boundaries were consistent across the reviewed materials:
- Wicofe-ABI owns public userspace syscall definitions; Wicofe-Kernel implements them.
- Wicofe-Kernel owns VFS internals, driver core, and privileged DKM ABI.
- ONWFS owns its on-disk format; Wicofe-Storage owns system-level storage workflows.
- Osynit owns PID 1 and service supervision; Wicofe-Services owns individual daemons.
- WPM owns package transactions; Wicofe-Update owns whole-system update orchestration.
- Wicofe-Build owns whole-system build orchestration; Wicofe-Image owns image composition.
- Mysh remains a standalone shell project; Wicofe integration is a planned target and package management belongs to WPM.

The reviewed documentation consistently labels ONWFS 0.2.x as draft and does not claim a production formatter or crash-safe filesystem implementation. Mysh's README identifies its own BSD 3-Clause license; this is an explicit repository-specific license, not a conflict with the project's MPL-2.0 default for original Wicofe components.

## 5. Follow-up action plan

1. Apply the approved dependency license policy to every direct/transitive dependency and shipped asset; audit manifests, vendored code, build outputs and release images.
2. Reconcile Wicofe roadmap milestones with current kernel source and CI evidence.
3. Assign stable requirement IDs to canonical normative specifications.
4. Add automated Markdown link checking and repository-map/index consistency checks to Wicofe-Tools or Wicofe-Tests.
5. Build a machine-readable repository/contract ownership manifest only after owners agree on the current boundary model.
6. Repeat this audit after policy decisions and traceability rollout.

## 6. Audit limitations

This audit is documentation-focused. It did not:
- inspect every source file or dependency manifest in all 29 repositories;
- execute builds, tests, CI workflows, emulators, or hardware tests;
- verify every Markdown link by requesting its target;
- perform legal analysis of dependency compatibility;
- establish that any planned subsystem is implemented or conformant.

All findings should be interpreted within that scope.


## 7. Follow-up implementation — repository documentation validator

After the initial audit, Wicofe-Tools received an initial read-only Markdown validator:

- [Validator source](https://github.com/Waizusora/Wicofe-Tools/blob/main/scripts/validate_repository_docs.py)
- [Unit tests](https://github.com/Waizusora/Wicofe-Tools/blob/main/tests/test_validate_repository_docs.py)
- [Usage and limitations](https://github.com/Waizusora/Wicofe-Tools/blob/main/docs/REPOSITORY_DOCUMENTATION_VALIDATOR.md)
- [GitHub Actions workflow](https://github.com/Waizusora/Wicofe-Tools/blob/main/.github/workflows/repository-docs-validator.yml)

The initial tool checks local Markdown links and heading fragments, directory index targets, workspace path escapes, and optional forbidden terms. It is read-only and uses only the Python standard library.

This partially completes follow-up action 4. It does **not** yet check remote HTTP links, compare the central repository inventory with local checkouts, validate repository-map/index completeness, inspect SPDX/dependency metadata, or verify requirement/test ID coverage.

Unit tests and the workflow definition were committed and fetched back for content verification. A successful GitHub Actions run was not confirmed during this session; therefore test status remains **not verified**.


## 8. Follow-up implementation — repository inventory validator and license policy

The project owner resolved AUD-2026-01 and the policy is now canonical in Wicofe-ThirdParty:

- [Dependency license policy](https://github.com/Waizusora/Wicofe-ThirdParty/blob/main/policies/DEPENDENCY_LICENSE_POLICY_0.1.md)
- [Third-party intake architecture](https://github.com/Waizusora/Wicofe-ThirdParty/blob/main/docs/THIRD_PARTY_INTAKE_ARCHITECTURE_0.1.md)
- [Central repository documentation map](REPOSITORY_DOCUMENTATION_MAP.md)

Wicofe-Tools also contains a canonical 29-repository checkout list and a read-only local inventory validator:

- [Canonical inventory](https://github.com/Waizusora/Wicofe-Tools/blob/main/config/repository_inventory.txt)
- [Validator source](https://github.com/Waizusora/Wicofe-Tools/blob/main/scripts/validate_repository_inventory.py)
- [Unit tests](https://github.com/Waizusora/Wicofe-Tools/blob/main/tests/test_validate_repository_inventory.py)
- [Usage guide](https://github.com/Waizusora/Wicofe-Tools/blob/main/docs/REPOSITORY_INVENTORY_VALIDATOR.md)

The existing GitHub Actions test workflow now watches all scripts, tests and configuration files. The validator compares local checkout directories only; it does not prove remote GitHub repository existence. GitHub Actions run [43808126021](https://github.com/Waizusora/Wicofe-Tools/actions/runs/43808126021) completed successfully. The `unit-tests` job and `Run validator unit tests` step both report success. This verifies the unit-test suite at commit `c5cd3f1b8965f4fe9658a26b2a2ec3331607c028`; it does not establish full 29-repository inventory or dependency-license compliance.
