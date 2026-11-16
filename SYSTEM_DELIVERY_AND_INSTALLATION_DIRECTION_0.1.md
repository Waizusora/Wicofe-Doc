# Wicofe System Delivery, Installation and Update Direction 0.1

- **Status:** Planned product direction / discussion draft; not a normative specification and not implementation evidence.
- **Date:** 2026-11-16
- **System targets:** x86-64 and AArch64.
- **Owners:** Wicofe-Installer (installation), Wicofe-Update (whole-system update orchestration), WPM (package manager and proposed command entry point), Wicofe-Image (system/release artifacts), Wicofe-Build (build and provenance), Wicofe-Recovery (repair/restore).

This document records the intended user experience and release philosophy. It does not change component ownership, select technical formats, promise a delivery schedule, or claim that installation/update functionality exists.

## 1. Product direction

The intended Wicofe experience is a command-line-first installation flow followed by a user-managed update workflow from the installed Terminal.

The project uses a **Delivery Release** model: deliver a stable system release when it is ready, rather than forcing a release on a fixed calendar. The approximate goal is one stable delivery around each month, but this is not a deadline or guaranteed cadence. A stable release may arrive after a month plus several days, or later, when quality and compatibility criteria are not yet met.

Security-critical fixes are handled outside the ordinary stable-delivery cadence. A validated fix may be delivered as a narrowly scoped update—even when only one binary needs to change—without waiting for the next general stable delivery.

“Delivery Release” is Wicofe's project-defined name for this intended model; it should not be confused with a standardized upstream release taxonomy.

## 2. Installation user experience

### 2.1 Intended entry point

The intended installation media boots into a text-based CLI environment. The user starts the guided installation workflow by entering:

```sh
wicofe-install
```

The command is the user-facing entry point, not a claim that the installer is already available in the current system. The installation environment, shell, command discovery and privileged execution contract still need to be designed.

### 2.2 End-to-end responsibility

Wicofe-Installer should orchestrate the complete installation lifecycle across the owning components:

1. Start in the installation CLI environment and identify the running installer image.
2. Discover candidate storage devices and stable device identities through Wicofe-Storage.
3. Validate architecture, firmware/boot mode, image compatibility, capacity and required artifacts.
4. Present the target device, proposed partition/filesystem layout and all destructive effects.
5. Require explicit confirmation for the exact plan; revalidate target identity immediately before writes.
6. Prepare storage using the versioned layout and filesystem contracts once those contracts are accepted.
7. Deploy verified Wicofe-Image payloads and boot components.
8. Configure the boot path and installed-system handoff to Osynit as PID 1, following the accepted kernel/image/boot contracts.
9. Apply first-boot configuration without copying machine-specific secrets or identities from the generic image.
10. Verify deployed files, partition/filesystem metadata, boot configuration and installation records.
11. Report whether installation is complete, incomplete or indeterminate, and provide the next action (for example, reboot to the installed storage).
12. Confirm the installed system's first successful boot through an explicit boot-health signal before reporting the full install-to-boot journey as verified.

The desired outcome is a system installed on persistent storage that can boot from that storage. A successful image write alone is not sufficient evidence of a successful installed boot. The exact distinction between “deployment complete” and “first boot confirmed” must be represented in installer state and logs.

### 2.3 Component boundaries

- **Wicofe-Installer:** CLI workflow, preflight, consent, orchestration, deployment status and handoff.
- **Wicofe-Storage:** device discovery, identity, partition inspection and storage operations.
- **Wicofe-Image:** manifest, selected payloads, image and boot artifact composition.
- **ONWFS / filesystem owners:** filesystem format, formatter/checker and consistency semantics.
- **Wicofe-Kernel:** boot/runtime contracts and supported device interfaces.
- **Osynit:** installed PID 1 and first-boot/service lifecycle; installer does not reimplement init.
- **Wicofe-Recovery:** repair path when deployment or boot fails.

The installer must not invent disk layouts, filesystem semantics, boot paths or init contracts owned by these components.

### 2.4 Safety invariants

No implicit disk wipe or format. The installer must identify the exact target, show irreversible effects, require explicit consent, revalidate identity before destructive writes, verify input authenticity/integrity, handle power loss and preserve diagnostics. It must not promise rollback of arbitrary full-disk overwrites. Installation and boot tests must use disposable virtual disks or dedicated test hardware.

## 3. Installed-system update user experience

The intended user-facing workflow is to run update commands from the installed Wicofe Terminal. The proposed command examples are:

```sh
wpm sync
wpm upgrade
```

The intended high-level meaning is:

- `wpm sync`: synchronize trusted repository/release metadata and discover the update state, analogous to an “update/check for updates” operation. It does not, by itself, imply that system files have been installed.
- `wpm upgrade`: request installation of the applicable updates after compatibility, trust, dependency and transaction checks.

These are planned command semantics only. Exact flags, prompts, privilege model, offline behavior, output format, reboot behavior and whether `sync` reports package updates, whole-system releases, or both remain to be specified.

### 3.1 Preserve ownership boundaries

WPM currently owns individual package formats, repositories, dependency resolution and package transactions. Wicofe-Update owns whole-system release discovery/policy, compatibility, staging, activation, rollback coordination and reporting.

If `wpm sync` and `wpm upgrade` become the unified user-facing entry point for OS updates, WPM should act as the CLI/front-end or coordinator and delegate whole-system operations to Wicofe-Update through a versioned interface. It must not silently absorb Wicofe-Update's release/activation responsibilities or independently replace kernel/boot/system components.

A shared transaction/lock contract is required so package operations cannot race with whole-system staging or activation. This command-to-component mapping is a proposed direction, not an accepted interface.

## 4. Delivery Release model

### 4.1 Ordinary stable deliveries

- Aim for approximately one stable delivery per month.
- There is no mandatory monthly publication date and no requirement to ship merely because a calendar interval elapsed.
- Publish when the release candidate meets the defined quality, security, compatibility, provenance and installation/update validation gates.
- If those gates are not met after one month, delay the stable delivery. A delay of one month and seven days, or longer, is acceptable.
- Do not lower test, license, security or reliability requirements to meet a target date.
- Publish release notes describing component changes, compatibility, known issues, upgrade path and required user action.

This is a cadence objective, not a service-level commitment.

### 4.2 Urgent security deliveries

A critical vulnerability must not wait for the next ordinary stable delivery. When a vulnerability affects a shipped component, the project should:

1. Triage severity, exploitability, affected versions/architectures and exposure.
2. Develop or obtain a permitted fix and review its source/dependency/license provenance.
3. Build the smallest safe update set; a single corrected binary may be sufficient when its ABI, dependencies and compatibility permit.
4. Test the changed binary and all affected integration boundaries, including rollback/recovery behavior where applicable.
5. Publish authenticated metadata and signed artifacts with affected versions, fixed versions, urgency and installation guidance.
6. Deliver the update as soon as the required safety gates pass, independently of the ordinary stable schedule.
7. Publish an advisory and incorporate the fix into the next ordinary stable delivery.

A one-binary emergency delivery must still carry the manifest, hashes, signature/authenticity evidence, provenance, license notices/SBOM delta, compatibility constraints and rollback/recovery instructions required by the release system. “Only one binary changed” does not mean “skip release controls.”

### 4.3 Release units and compatibility

The release system should support both:
- **Full stable delivery:** a coherent, tested set of system components and metadata.
- **Targeted security delivery:** the smallest compatible artifact set needed to remediate a critical issue.

The release manifest must state whether an artifact is independently replaceable or requires coordinated updates to libraries, kernel, ABI, boot components, configuration or data schemas. Never publish a binary-only update when its dependencies or ABI require a larger coordinated set.

## 5. Required release trust and quality gates

Before publication, the future release pipeline should require:

- Immutable source revisions, reproducible build inputs where feasible, and artifact hashes.
- Authenticated/signed release metadata and artifacts, documented trust roots, key rotation and revocation.
- Exact architecture and ABI compatibility declarations for x86-64 and AArch64.
- Unit, integration, conformance and regression results for the changed components.
- Boot/install/update/recovery evidence for the release scope.
- Dependency closure and final-image SBOM reconciliation under Wicofe Dependency License Policy 0.2.
- Required third-party notices and attribution in the delivered artifacts.
- Security review, known-issue record, release notes and rollback/recovery procedure.
- A strict release gate that fails closed when required evidence is missing or blocked.

A successful component CI run is not a complete OS release qualification. A successful build is not proof of installation, boot, update or recovery.

## 6. Relationship to existing architecture

This direction builds on, but does not supersede, the current draft component designs:

- [Wicofe installation/deployment architecture 0.1](https://github.com/Waizusora/Wicofe-Installer/blob/main/docs/INSTALLATION_DEPLOYMENT_ARCHITECTURE_0.1.md)
- [Wicofe whole-system update architecture 0.1](https://github.com/Waizusora/Wicofe-Update/blob/main/docs/WHOLE_SYSTEM_UPDATE_ARCHITECTURE_0.1.md)
- [Wicofe system image architecture 0.1](https://github.com/Waizusora/Wicofe-Image/blob/main/docs/IMAGE_SYSTEM_ARCHITECTURE_0.1.md)
- [WPM documentation and package-manager boundary](https://github.com/Waizusora/WPM/tree/main/docs)
- [Wicofe-Build release dependency-license gate](https://github.com/Waizusora/Wicofe-Build/blob/main/.github/workflows/release-dependency-license-gate.yml)

These documents remain draft architecture baselines. This product-direction note does not select A/B slots, snapshots or in-place updates; partition layout; filesystem default; package/release manifest format; signing envelope; release channels; or first-boot success protocol.

## 7. Decisions still required

1. Define whether the installation CLI uses Mysh or a dedicated minimal shell/runtime.
2. Specify the `wicofe-install` command contract, privilege boundary, interactive and unattended modes.
3. Freeze the supported firmware/boot and partition-layout matrix for x86-64 and AArch64.
4. Define the install-to-first-boot completion handshake and recovery behavior.
5. Decide the WPM CLI's exact relationship to Wicofe-Update and package-only operations.
6. Specify package/release metadata, signature format, trust roots, key lifecycle and anti-rollback policy.
7. Select and test the whole-system activation model (A/B, snapshots or in-place transaction).
8. Define stable and urgent security delivery artifact formats, versioning, compatibility and support policy.
9. Define release evidence thresholds, vulnerability severity/response policy and publication authorization.
10. Define user control for network/offline updates, reboot deferral and recovery.

## 8. Status and non-claims

- **Product direction:** Planned.
- **CLI command availability:** Not implemented / not verified.
- **Installer end-to-end workflow:** Not implemented / not verified.
- **WPM OS-update command integration:** Not specified / not implemented.
- **Delivery Release publication pipeline:** Not implemented / not verified.
- **Boot-from-installed-storage success:** Not demonstrated.
- **Production update/rollback guarantees:** Not established.

No current Wicofe release, installer, updater, or bootable installed system is claimed by this document.
