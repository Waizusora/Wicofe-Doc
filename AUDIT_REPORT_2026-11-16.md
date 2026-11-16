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

One policy conflict remains unresolved and requires a project decision: third-party GPL-family dependency handling.

No system-wide implementation or CI conformance claim is made.

## 2. Findings

### AUD-2026-01 — Third-party license policy is inconsistent

**Severity:** High  
**Status:** Open — project policy decision required  
**Affected repositories:** Wicofe-Docs, Wicofe-ThirdParty, Osynit, WDE

Evidence:
- Osynit README states its default dependency set is intended to exclude GPL, LGPL, and AGPL components.
- WDE README states GNU GPL, LGPL, and AGPL dependencies are not permitted by its current policy.
- Wicofe-ThirdParty README calls for explicit compatibility and distribution review of GPL-family components before inclusion.
- Wicofe-Docs/LICENSE_POLICY.md requires review of actual license terms and distribution context but does not state a blanket GPL-family prohibition.

These rules are not equivalent. A blanket exclusion and a case-by-case review policy produce different dependency decisions.

**Recommended resolution:** Choose one project-wide rule:
- **Strict exclusion:** prohibit GPL/LGPL/AGPL dependencies for all shipped components, with a documented exception authority if exceptions are ever allowed; or
- **Case-by-case review:** permit evaluation of each exact component/version/use/distribution context, then remove blanket-exclusion wording from Osynit and WDE.

Do not silently infer the intended rule. Update the central policy and all component policies together after the decision.

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

1. Resolve AUD-2026-01 with an explicit project-wide GPL/LGPL/AGPL policy.
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
