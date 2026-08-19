---
layout: default
title: "From Embedded Linux to Kernel Contributor"
---

# From Embedded Linux to Kernel Contributor

## My Linux Kernel Mentorship Journey — LFX Spring 2026

**Sanjay Chitroda**  
**Mentorship:** 1 March 2026 – 31 August 2026  
**Primary subsystem:** Industrial I/O (IIO)  
**Mentors:** Shuah Khan & Brigham Campbell

---

## The journey

My LFX Linux Kernel Mentorship journey is best understood as a transition in how I approached Linux kernel development:

```text
Before mentorship

Embedded Linux / BSP / product development
                ↓
Mentorship

Upstream Linux kernel development
                ↓
After mentorship

Independent kernel contributor
```

I already came to the mentorship with more than eight years of Embedded Linux experience, including BSP development, Linux device drivers, multimedia work and experience with the Yocto Project and Linux kernel development. My goal was not simply to learn Linux kernel programming from scratch. I wanted to deepen my practical experience with the **upstream kernel development process** and become a more effective long-term kernel contributor.

The mentorship gave me an opportunity to work within the Linux kernel community, learn subsystem expectations, submit patches to the mailing list, respond to reviews, restructure patch series, follow linux-next and understand the path from an initial contribution to mainline integration.

## Why I joined the mentorship

Working with the Linux kernel in a product environment and contributing to the upstream kernel are related, but they require different habits.

In product development, the immediate objective is often to implement and validate functionality for a particular platform or product. Upstream development adds another dimension: the change must fit the subsystem's architecture, conventions, maintainership model and long-term maintenance expectations.

I joined the LFX mentorship to strengthen that upstream perspective and learn through real contributions and community review rather than only through documentation or isolated experimentation.

## Starting point: Embedded Linux and BSP development

Before the mentorship, my professional experience was centered around Embedded Linux and product development. My background includes:

- Embedded Linux and BSP development
- Linux device drivers
- Multimedia systems, including camera and display
- Yocto Project and build-system work
- Linux kernel development in product environments

I had already contributed to upstream projects, including the Yocto Project. The LFX mentorship therefore represented a focused opportunity to build deeper and more sustained experience specifically in **upstream Linux kernel development and collaboration**.

## Entering the IIO subsystem

The mentorship focused on the **Industrial I/O (IIO)** subsystem. This gave me an opportunity to study a subsystem in depth while working on real drivers and infrastructure.

My work covered several closely related areas:

- Driver modernization
- `devm_*` and devres-based resource management
- `cleanup.h`, including `__free` and `guard()` patterns
- Error-path improvements
- Driver lifecycle handling
- `dev_err_probe()` adoption
- Resource ownership and teardown considerations
- HID-IIO infrastructure and cross-driver modernization
- Maintainer and review metadata

The work began with focused cleanup and modernization changes and gradually expanded into larger, review-driven patch series.

## Learning the upstream workflow

One of the most important outcomes of the mentorship was learning that upstream development is more than writing code and sending a patch.

My workflow evolved toward:

```text
Understand the subsystem
        ↓
Study existing implementation and conventions
        ↓
Define a logical patch boundary
        ↓
Implement and validate the change
        ↓
Prepare the commit and cover letter
        ↓
Submit to the mailing list
        ↓
Receive maintainer and reviewer feedback
        ↓
Revise or restructure the series
        ↓
Track linux-next
        ↓
Track mainline integration
```

This process changed how I think about a kernel change. A patch is not finished merely because the code builds or the local problem is solved. It also needs to be understandable, reviewable, appropriately scoped and maintainable within the subsystem.

## What code review taught me

The review process became one of the most valuable parts of the mentorship.

Review feedback was not limited to correcting individual lines. In several cases, review affected the **scope, structure and architecture of the patch series**.

The HID-IIO work was a particularly useful example. What started as driver modernization expanded into a large series and eventually reached 36 patches before review-driven restructuring separated common infrastructure work from driver-specific conversions.

That experience reinforced several lessons:

- Patch scope should follow logical ownership and reviewability rather than implementation convenience.
- A technically simple cleanup can expose deeper API, lifecycle or resource-management considerations.
- `devm_*` conversions require understanding resource ownership and teardown ordering rather than mechanical API replacement.
- Patches should remain independently understandable and applicable where possible.
- Review feedback can change the architecture and scope of a contribution, not only individual lines of code.
- Upstream collaboration requires precise communication and careful tracking of subsystem development trees.

## From cleanup patches to broader modernization

The contribution journey progressed from focused cleanups to broader modernization work.

Examples included adopting `dev_err_probe()`, improving resource lifetime handling, using devm-managed resources where appropriate, addressing error paths, and improving lifecycle correctness.

Some changes were intentionally small. That was valuable because small patches provided a way to learn subsystem conventions, commit structure and review expectations. As my understanding grew, I became more comfortable working on larger changes and multi-revision series.

A recurring lesson was that a seemingly mechanical modernization is rarely just a search-and-replace exercise. For example, changing resource management requires understanding who owns the resource, when it is acquired, when it is released, what happens on probe failure, and whether changing the lifetime introduces ordering or race concerns.

## A concrete example: driver exposure and callback ordering

The HID-IIO work also exposed an important driver-lifecycle consideration: the order in which callbacks are configured and an IIO device becomes visible to userspace.

Several changes addressed races between callback setup and device exposure. The important lesson was that API calls cannot always be evaluated independently; their ordering can define whether another execution context can observe a partially initialized device.

This was a good example of how upstream review helped move the work beyond simple modernization toward reasoning about **lifecycle, concurrency and externally visible state**.

## Contribution snapshot

During the mentorship, my work in IIO progressed from focused cleanups to multi-revision series and broader infrastructure and cross-driver modernization.

| Area | Result |
|---|---|
| Mentorship | LFX Linux Kernel Mentorship — Spring 2026 |
| Duration | 1 March 2026 – 31 August 2026 |
| Primary subsystem | Industrial I/O (IIO) |
| Mainline | **20+ accepted commits** |
| linux-next | **25+ additional commits** |
| Main focus | Driver modernization, resource management, error handling and lifecycle improvements |
| Workflow | Submission → review → revision → linux-next → mainline |

The repository contains the detailed contribution evidence, patch series, milestones, growth notes and final report.

## Beyond the number of patches

The number of accepted commits is useful as a measurable outcome, but it is not the main measure of what I gained from the mentorship.

The larger change was in my development workflow.

I became more conscious of:

- Subsystem-specific expectations
- Patch boundaries and series organization
- Resource ownership and lifetime
- Error-path correctness
- Reviewability and maintainability
- Mailing-list communication
- Maintainer expectations
- linux-next and mainline tracking
- Reviewing and learning from other contributors' work

The mentorship helped turn upstream contribution from an occasional activity into a more deliberate part of my kernel development practice.

## What changed for me

### Before mentorship

I approached Linux kernel development primarily from the perspective of an Embedded Linux and product engineer. I had kernel experience, but my day-to-day engineering context was strongly tied to platforms, BSPs and product requirements.

### During mentorship

I worked inside an upstream subsystem, followed its development tree, submitted patches to the mailing list, received and incorporated review feedback, and learned to structure changes around maintainability and subsystem expectations.

### After mentorship

The goal is to continue as an **independent Linux kernel contributor**, with IIO as an area where I can continue developing subsystem knowledge and contributing reviews and patches beyond the formal mentorship period.

The important transition is therefore not simply:

```text
5 patches accepted
```

It is:

```text
Product-focused kernel development
            ↓
Understanding upstream expectations
            ↓
Participating in review and subsystem development
            ↓
Independent kernel contribution
```

## Advice I would give to future mentees

If I had to summarize the mentorship experience for someone preparing to contribute upstream, I would emphasize a few things:

1. **Learn the subsystem, not just the API.** Understanding how the subsystem is structured makes reviews much easier to understand.
2. **Start with changes you can explain completely.** Small cleanups can teach a surprising amount about conventions and review expectations.
3. **Treat review as part of development.** A review comment is often an opportunity to understand a design constraint that was not obvious from the code alone.
4. **Do not make large series large only because the implementation is related.** Logical boundaries make review and maintenance easier.
5. **Follow linux-next.** Seeing how work moves through subsystem trees provides context that a single patch cannot provide.
6. **Read other people's patches.** Reviewing and comparing approaches is one of the fastest ways to learn subsystem conventions.
7. **Think about lifetime and ownership.** Resource management changes should be based on lifecycle reasoning, not just API replacement.

## What's next

The mentorship ends on 31 August 2026, but upstream contribution does not.

I plan to continue contributing to the IIO subsystem, increase my participation in upstream review and continue expanding my Linux kernel knowledge into other areas of interest.

The mentorship was therefore not an endpoint. It was a structured transition from having Linux kernel experience in an Embedded Linux/product environment to participating more deeply in the **upstream Linux kernel community**.

---

## Explore the work

- [LFX Mentorship repository](https://github.com/sanjay-embedded/LFX-Linux-kernel-Spring-2026)
- [Final report](https://github.com/sanjay-embedded/LFX-Linux-kernel-Spring-2026/blob/LFX-submission-v2/submission/final-report.md)
- [Mentorship milestones](https://github.com/sanjay-embedded/LFX-Linux-kernel-Spring-2026/blob/LFX-submission-v2/mentorship-milestones.md)
- [Mentorship growth](https://github.com/sanjay-embedded/LFX-Linux-kernel-Spring-2026/blob/LFX-submission-v2/mentorship-growth.md)
- [Upstream review process](https://github.com/sanjay-embedded/LFX-Linux-kernel-Spring-2026/blob/LFX-submission-v2/upstream-review-process.md)
- [Linux kernel contributions](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/log/?qt=author&q=sanjay+chitroda)
- [linux-next contributions](https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/log/?qt=author&q=sanjay+chitroda)

---

*This is the first draft of the mentorship blog and will be refined as the mentorship documentation and contribution data are finalized.*
