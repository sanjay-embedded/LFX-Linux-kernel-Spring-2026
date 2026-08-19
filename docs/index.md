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

> **Before mentorship:** Embedded Linux / BSP / product development  
> ↓  
> **Mentorship:** Upstream Linux kernel development  
> ↓  
> **After mentorship:** Independent Linux kernel contributor

---

## The journey

I entered the LFX mentorship with more than eight years of Embedded Linux experience, including BSP development, Linux device drivers, multimedia systems, the Yocto Project and Linux kernel development in product environments.

I was already an upstream contributor through work in the Yocto Project. The specific transition I wanted to make through LFX was deeper and more sustained participation in the **upstream Linux kernel community**: working within a subsystem, submitting changes through the mailing-list workflow, responding to reviews, following linux-next and understanding how changes reach mainline.

The mentorship focused on the **Industrial I/O (IIO)** subsystem and gave me a structured opportunity to make that transition through real kernel contributions.

## Why I joined

Working with the Linux kernel in a product environment and contributing to the upstream kernel are closely related, but the engineering priorities are not identical.

Product development often starts with a platform requirement, a feature or a problem that needs to be solved. Upstream development adds another question:

> **Is this change the right long-term change for the subsystem?**

That means considering architecture, existing kernel patterns, resource ownership, lifecycle, reviewability, maintainability and the expectations of the maintainers who will carry the code forward.

I joined LFX to develop that upstream perspective through actual contributions and community review rather than only through documentation or isolated experimentation.

## What I worked on

My primary area was IIO driver modernization and maintenance. The work included:

- `devm_*` and devres-based resource management
- `cleanup.h`, including `__free` and `guard()` patterns
- `dev_err_probe()` adoption
- Error-path and driver-lifecycle improvements
- Resource ownership and teardown considerations
- HID-IIO infrastructure and cross-driver modernization
- Maintainer and review metadata
- Small cleanups that prepared drivers for current kernel practices

A recurring theme was **modernizing drivers in line with current kernel patterns as preventive maintenance**. The goal was not to wait for a reported bug and then repair it. Many changes were intended to reduce unnecessary lifetime, cleanup and error-path complexity and avoid potential failures or bugs before they become user-visible problems.

## Kernel timeline

The contribution journey also gave me a practical view of how kernel development moves through versions rather than existing as a single release event.

```text
Linux 7.1 development / early mentorship
                 │
                 ▼
          Linux 7.2 merge window
                 │
                 ▼
             Linux 7.2-rc
                 │
                 ▼
        Linux 7.3 merge window
                 │
                 ▼
       Continued linux-next work
```

Following the subsystem tree, linux-next and mainline helped me understand where a patch actually sits in the upstream development cycle and why timing, review and integration matter.

## From a patch to an upstream change

My development workflow evolved during the mentorship:

```text
Understand the subsystem
        ↓
Study existing implementation and kernel patterns
        ↓
Identify a meaningful, reviewable change
        ↓
Implement and validate
        ↓
Prepare the patch / series
        ↓
Submit to the mailing list
        ↓
Receive maintainer and reviewer feedback
        ↓
Revise or restructure
        ↓
Track linux-next
        ↓
Track mainline integration
```

The most important lesson was that **writing the code is only one part of an upstream contribution**.

## What code review taught me

The review process became one of the most valuable parts of the mentorship. Review was not simply about correcting lines of code; it could change the scope, structure or architecture of a patch series.

One example was the HID-IIO work. What started as driver modernization grew into a large series and reached 36 patches before review-driven restructuring separated common infrastructure from driver-specific conversions.

That experience changed how I approached patch series. Related changes do not necessarily belong in one series simply because they can be implemented together. The series should also make sense to a reviewer and leave logical, maintainable changes behind.

Another important lesson came from driver lifecycle work. Changes involving resource management or device exposure require reasoning about **ownership, teardown ordering and what another execution context can observe**, rather than simply replacing one API with another.

> **Before mentorship, I thought a good patch was primarily about fixing the code. After mentorship, I realized a good upstream patch is also about making the change easy to review, maintain and integrate.**

That became one of the most important changes in my engineering approach.

## Representative contributions

Rather than listing every patch, the following examples represent the different types of engineering lessons I gained.

### Driver modernization and error handling

The `mma8452` and ADXL3xx work provided focused examples of driver modernization, including `dev_err_probe()`, devm-managed resources and error-path improvements.

These changes reinforced that small patches can still require careful reasoning about probe failures, resource lifetime and kernel conventions.

### HID-IIO lifecycle and concurrency

The HID-IIO work went beyond mechanical cleanup. Several drivers required changes to avoid races between callback setup and device exposure.

This highlighted an important principle: **API ordering can be part of correctness**. A device should not become externally visible while the state required for its callbacks or operation is still being established.

### Maintainer and ownership metadata

Updating `MAINTAINERS` entries was another useful upstream lesson. Maintainer information is not simply a list of email addresses; it represents sustainable ownership and review coverage for code.

This showed that upstream contribution also includes the community and maintenance model around the code, not only the implementation itself.

## Contribution snapshot

| Area | Result |
|---|---|
| Program | LFX Linux Kernel Mentorship — Spring 2026 |
| Duration | 1 March 2026 – 31 August 2026 |
| Primary subsystem | Industrial I/O (IIO) |
| Mainline | **20+ accepted commits** |
| linux-next | **25+ additional commits** |
| Main focus | Driver modernization, resource management, error handling and lifecycle improvements |
| Development model | Submission → review → revision → linux-next → mainline |

The numbers provide a useful measure of activity, but the larger outcome was learning how to develop changes with upstream review and long-term maintenance in mind.

## Testing and tools

The validation approach depended on the type of change and available hardware. For many IIO driver cleanups and modernization patches, validation included kernel builds, static analysis and source-level checks, together with careful review of probe, remove and error paths. Dedicated hardware was not available for every driver, so I have avoided presenting compilation or static analysis as hardware validation.

The wider upstream workflow also involved tools and resources such as:

- Kernel build and warning checks
- `checkpatch.pl`
- Sparse and static analysis where applicable
- Coccinelle / `coccicheck` where applicable
- Git and patch-series tooling
- `lore.kernel.org` and mailing-list archives
- linux-next tracking
- Mainline kernel history

The important lesson was to match validation to the actual claim being made by a patch and to be explicit about what was and was not tested.

## What changed for me

### Before mentorship

I approached Linux kernel development primarily from an Embedded Linux and product-development perspective. I had kernel experience and upstream Yocto experience, but the kernel community was not yet a sustained part of my development workflow.

### During mentorship

I worked within IIO, followed its development tree, submitted patches to the mailing list, responded to review, reworked patch series and tracked changes through linux-next and mainline.

### After mentorship

I want to continue as an **independent Linux kernel contributor**, with IIO as an area where I can continue developing subsystem knowledge, reviewing patches and contributing improvements beyond the formal mentorship period.

The transition is therefore not simply:

```text
More accepted patches
```

It is:

```text
Embedded Linux / product development
              ↓
Understanding upstream kernel expectations
              ↓
Review-driven subsystem development
              ↓
Independent Linux kernel contribution
```

## What I learned from the community

The mentorship was not only about working with my mentors. Reading other contributors' patches, following mailing-list discussions and seeing how maintainers evaluate changes provided a broader view of kernel development.

Some of the most useful lessons were:

- Learn the subsystem, not just the API.
- Start with changes you can explain completely.
- Treat review as part of development, not as a final gate.
- Keep patch boundaries logical and reviewable.
- Think about resource ownership and lifetime before changing resource-management APIs.
- Follow linux-next to understand how subsystem work progresses.
- Read other contributors' patches to learn established patterns.
- Prefer preventive modernization when it reduces complexity and potential failure paths.

## A practical guide for future contributors

During this journey, I also created a reusable guide for people interested in contributing to the Linux kernel with or without an LFX mentorship:

**[Kernel Upstream Contribution Guide](https://github.com/sanjay-embedded/oss-guide/blob/master/kernel-upstream.rst)**

The guide collects the practical steps, tools and workflow that I found useful while learning how to participate in upstream kernel development.

## Tips for future mentees

If I were starting the mentorship again, I would keep these points in mind:

1. **Understand the subsystem before trying to understand every API.**
2. **Start small, but choose changes that teach you something about the subsystem.**
3. **Read review discussions carefully.** The reasoning behind a requested change can be more valuable than the code change itself.
4. **Do not measure progress only by patch count.** Understanding why a patch is accepted, rejected or restructured matters more.
5. **Follow the development trees.** linux-next and mainline provide context that individual patches cannot.
6. **Learn from other contributors.** The mailing list is both a review system and a large technical knowledge base.
7. **Think beyond today's bug.** Modernizing code according to current kernel practices can remove complexity and reduce potential future failures.

## What's next

The mentorship is a milestone, not an endpoint. I plan to continue contributing to IIO, participate more actively in upstream review and expand my Linux kernel development experience into other areas.

The most important outcome is the change in how I approach kernel work: from primarily solving a product or code problem to thinking about the **quality, reviewability, maintainability and long-term integration of the upstream change**.

---

## Explore the work

- [LFX Mentorship repository](https://github.com/sanjay-embedded/LFX-Linux-kernel-Spring-2026)
- [Final report](https://github.com/sanjay-embedded/LFX-Linux-kernel-Spring-2026/blob/master/submission/final-report.md)
- [Mentorship milestones](https://github.com/sanjay-embedded/LFX-Linux-kernel-Spring-2026/blob/master/mentorship-milestones.md)
- [Mentorship growth](https://github.com/sanjay-embedded/LFX-Linux-kernel-Spring-2026/blob/master/mentorship-growth.md)
- [Upstream review process](https://github.com/sanjay-embedded/LFX-Linux-kernel-Spring-2026/blob/master/upstream-review-process.md)
- [Patch series](https://github.com/sanjay-embedded/LFX-Linux-kernel-Spring-2026/tree/master/patch-series)
- [Linux kernel contributions](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/log/?qt=author&q=sanjay+chitroda)
- [linux-next contributions](https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/log/?qt=author&q=sanjay+chitroda)

---

*This is a working draft of the mentorship blog and will be refined section-by-section before the final submission.*
