## Always Check the Subsystem Development Tree

Before preparing a new patch series or revision, check the current subsystem development branch for related changes.

During the ADXL313 cleanup work, one proposed `guard()` conversion was already present in `iio/testing`. The change was therefore dropped and the remaining work was rebased onto the current subsystem tree.

This avoids duplicate submissions and ensures that new work is developed on top of the changes maintainers are already integrating.

**Related Series**

- [Series 006 – ADXL Accelerometer Cleanup](../patch-series/series-006-adxl-accelerometer-cleanup.md)
