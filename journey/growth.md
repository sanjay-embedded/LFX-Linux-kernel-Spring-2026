## April 2026 – Learning to Track Subsystem State

The ADXL313 cleanup series provided an important upstream workflow lesson.

The initial three-patch series included a `guard()` conversion that was already available in the IIO development tree. After reviewer feedback, the work was rebased on `iio/testing` and the redundant change was removed.

The remaining cleanup was then extended to closely related ADXL accelerometer drivers and accepted as an eight-patch series.

This reinforced the importance of synchronizing development with the subsystem tree before preparing new revisions and avoiding duplicate work already present upstream.

**Related Series**

- [Series 006 – ADXL Accelerometer Cleanup](../patch-series/series-006-adxl-accelerometer-cleanup.md)
