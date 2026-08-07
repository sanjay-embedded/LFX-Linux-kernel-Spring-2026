## Lesson: Respect subsystem boundaries

Initially, I grouped related cleanup changes across several subsystems into one patch series.

Reviewer feedback explained that even when the technical change is similar, submissions should generally be scoped to a single subsystem so that maintainers can review them independently.

This lesson became the basis for restructuring later work into subsystem-specific series.

---

## Design improvements over mechanical cleanups

My initial approach focused on removing unnecessary `kmalloc()` calls.

Reviewer feedback encouraged looking beyond API replacement and asking whether the allocation was needed at all.

By reusing the driver's existing `buffer_data[]` field, the final solution reduced both allocation overhead and cleanup complexity while better matching the driver's design.

---

## Managing Large Multi-Revision Series

The SSP Sensors series demonstrated that substantial upstream work often evolves through many revisions rather than reaching its final form immediately.

Key observations:

- Keep each patch logically independent.
- Separate cleanup, functional changes, and refactoring whenever possible.
- Allow reviewer feedback to reshape the implementation instead of defending the initial approach.
- Maintain a clear revision history to help reviewers focus on incremental changes.
- Plan hardware validation early for hardware-dependent drivers.

**Related Series**

- Series 002 – SSP Sensors: Resource Cleanup & Driver Modernization

---

## Scope Changes Can Improve Acceptance

A larger patch series is not always the best submission unit.

While modernizing the GC0310 camera sensor driver, the initial proposal combined cleanup work with a functional improvement. Reviewer feedback recommended isolating the functional change, allowing it to be reviewed independently and merged without waiting for unrelated cleanup patches.

Key observations:

- Submit one logical improvement per patch or series.
- Functional enhancements generally deserve independent review.
- Subsystem helper APIs simplify maintenance and improve consistency.
- Partial acceptance of a larger series is a positive outcome and often forms the basis for future follow-up work.

**Related Series**

- Series 003 – GC0310 Clock Modernization

---

## Static Analysis Tools Support Review, They Do Not Replace It

Automated tools such as `checkpatch.pl` are designed to help identify potential issues, but their output should always be interpreted in context.

During review of the AD7173 cleanup series, a reported CamelCase warning was found to be caused by a limitation in `checkpatch.pl` rather than incorrect kernel code. Reviewers preferred preserving technically correct SI unit notation instead of modifying code solely to satisfy the tool.

Key observations:

- Investigate every warning before proposing a fix.
- Understand subsystem conventions and domain-specific terminology.
- Preserve technically correct code even when tooling produces false positives.
- Consider improving tooling when repeated false positives are identified.

**Related Series**

- Series 004 – AD7173 Checkpatch Analysis
