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
