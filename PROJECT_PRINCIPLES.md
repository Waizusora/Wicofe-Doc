# Wicofe Project Principles

**Status:** Project-wide engineering and governance principles  
**Applies to:** All Wicofe repositories, components, ports, tools, SDKs, images, and documentation

## 1. Project identity

Wicofe is an independent Unix-like, POSIX-compatible operating system and software ecosystem, designed as an alternative to established and widely adopted software ecosystems and technologies, including GNU.

Wicofe aims to provide independent implementations and a coherent native platform while remaining interoperable through established standards such as POSIX. This direction is not limited to replacing GNU software, and it does not require recreating every popular project from scratch. POSIX compatibility is a core design objective; it does not imply GNU compatibility, Linux binary compatibility, or implementation compatibility with any particular Linux distribution. The project must distinguish its POSIX conformance goals from features that are merely planned or implemented.

## 2. Native system architecture

Native Wicofe software must target Wicofe interfaces and execution environments.

- Use the Wicofe syscall ABI and documented native system interfaces.
- Do not require Linux libc, glibc, musl-for-Linux, or a Linux compatibility layer to build or run native Wicofe software.
- Do not require GNU compatibility layers or GNU-specific behavior as a native platform contract.
- Keep kernel mechanisms, language runtimes, C libraries, and application-level utilities as separate architectural layers.
- POSIX interfaces may be implemented over Wicofe's own ABI; POSIX source compatibility does not imply Linux syscall or binary ABI compatibility.

A component may use a native Wicofe runtime written specifically for its language. It must not silently inherit Linux host assumptions through its target triple, standard library, linker, or transitive dependencies.

## 3. POSIX compatibility and ecosystem independence

Wicofe targets a coherent Unix-like userspace with documented POSIX interfaces and behavior. It is intended as an independent alternative to established and widely adopted software ecosystems and technologies, including GNU.

The project is not limited to replacing GNU components. It may develop independent alternatives to popular tools, libraries, runtimes, services, and development technologies across the wider software ecosystem. GNU-specific extensions, GNU command behavior, GNU toolchain assumptions, and GNU compatibility are not project goals.

Where an established utility or library is reused, adapt it to Wicofe's native interfaces and the selected POSIX requirements. Do not claim complete POSIX conformance without a declared profile and reproducible conformance evidence.

## 4. Licensing policy

Wicofe prefers permissive licenses for new original code and third-party dependencies. This preference does not automatically change or relicense existing repositories; each repository's current LICENSE file and approved third-party terms remain authoritative unless changed through a separate, rights-aware decision.

- Prefer MIT, BSD, ISC, Apache-2.0, Zlib, and other suitable permissive licenses, subject to their exact terms.
- Avoid GPL and AGPL software and dependencies; they are not acceptable for normal project integration.
- LGPL may be considered only when no technically and legally suitable permissively licensed alternative is available. The exact component, version, license, integration method, and distribution obligations require review and explicit project-owner approval.
- Do not choose a copyleft dependency merely for convenience when a suitable permissive alternative exists.
- Preserve all third-party copyright notices, license texts, attribution, source obligations, and other applicable terms. Never relicense imported code without the necessary rights.

The binding dependency policy and compliance records are maintained by [Wicofe-ThirdParty](https://github.com/Waizusora/Wicofe-ThirdParty).

## 5. Reuse and implementation from scratch

Independent implementation is encouraged when it is practical and maintainable. Wicofe does not require every component to be written from scratch.

Before adopting an upstream component, evaluate its license, architecture, portability, security, maintenance cost, and native integration requirements. Reuse or fork an existing project when a from-scratch implementation would be disproportionately difficult, risky, or wasteful.

Any reused component must be adapted to Wicofe's native architecture. Upstream Linux or GNU assumptions must not become mandatory Wicofe platform dependencies.

## 6. Engineering priorities

1. Native Wicofe execution and system interfaces.
2. POSIX compatibility and documented conformance.
3. Independence from GNU and Linux-specific runtime requirements.
4. Permissive licensing and auditable third-party provenance.
5. Stable, versioned interfaces and clear component ownership.
6. Security, maintainability, portability, and reproducible validation.
7. Honest status reporting: planned, experimental, implemented, and verified are distinct states.

These principles apply to the kernel, syscall ABI, C and language runtimes, libraries, shell, utilities, init system, filesystem, services, desktop, SDK, ports, build infrastructure, and future components.
