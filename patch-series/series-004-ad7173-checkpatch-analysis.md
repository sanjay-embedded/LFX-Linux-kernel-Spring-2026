# Series 004 – AD7173: Checkpatch & Coding Style Analysis

## 1. Executive Summary

This series attempted to resolve coding-style and spelling issues reported by `checkpatch.pl` in the AD7173 ADC driver. During review, maintainers identified that one of the reported CamelCase warnings was not a driver issue but a limitation of `checkpatch.pl` in recognizing standard SI unit abbreviations. Rather than modifying technically correct code to satisfy tooling, the discussion concluded that improving the tool would be the better long-term solution. Although the series was not merged, it reinforced an important upstream engineering principle: developer judgment takes precedence over blindly following static analysis tools.

---

## 2. Project Overview

| Item | Details |
|------|---------|
| **Series** | iio: adc: ad7173: cleanup codestyle check and spell correct |
| **Subsystem** | Industrial I/O (ADC) |
| **Driver** | AD7173 |
| **Duration** | April 2026 |
| **Initial Submission** | 13 April 2026 |
| **Final Revision** | v1 |
| **Revisions** | 1 |
| **Patch Count** | 3 |
| **Status** | Closed after review |

---

## 3. Background

This series focused on improving code quality by addressing `checkpatch.pl` warnings, coding-style issues, and spelling corrections in the AD7173 driver. The intent was to align the driver more closely with kernel coding standards while removing minor issues reported by automated tooling.

---

## 4. Engineering Goals

- Resolve `checkpatch.pl` warnings.
- Improve coding style consistency.
- Correct spelling mistakes.
- Reduce static analysis noise.
- Improve overall code readability.

---

## 5. Technical Evolution

### Phase 1 – Initial Cleanup

- Submitted a three-patch cleanup series.
- Addressed coding style and spelling issues.
- Fixed warnings reported by `checkpatch.pl`.

---

### Phase 2 – Review Discussion

During review, maintainers identified that one reported CamelCase warning was caused by a limitation of `checkpatch.pl` rather than incorrect driver code.

The identifier used standard SI notation (`uV`, `C`) and was technically correct.

---

### Phase 3 – Conclusion

Rather than changing correct code to satisfy tooling, the discussion concluded that the appropriate long-term solution would be improving `checkpatch.pl`.

The series therefore concluded without further revisions.

---

## 6. Review Summary

| Reviewer | Key Feedback |
|----------|--------------|
| **Andy Shevchenko** | Explained that the CamelCase warning resulted from a limitation in `checkpatch.pl`, not an actual coding-style violation. Suggested improving the tool rather than changing valid identifiers. |
| **Jonathan Cameron, David Lechner, Nuno Sá** | Participated in review of the cleanup series and subsystem discussion. |
| **Author** | Acknowledged that improving tooling was preferable to modifying technically correct driver code. |

---

## 7. Interesting Engineering Discussions

- Static analysis tools are advisory rather than authoritative.
- SI unit abbreviations (`uV`, `C`) are valid kernel terminology.
- Tool limitations should not drive unnecessary source code changes.
- Sometimes the correct contribution is to improve the development tools instead of the driver itself.

---

## 8. Revision Timeline

| Revision | Evolution |
| -------- | --------- |
| **v1** | Initial cleanup series submitted. Review determined that the reported issue originated from a `checkpatch.pl` limitation rather than a driver defect, so the series did not continue. |

---

## 9. Final Status

| Item | Status |
|------|--------|
| Mainline | ❌ Not merged |
| linux-next | ❌ Not applied |
| Latest Revision | v1 |
| Outcome | Closed after review |
| Reason | Tool limitation identified instead of a driver issue |

---

## 10. Key Lessons Learned

- `checkpatch.pl` is a valuable guideline, but its warnings require engineering judgment.
- Standards-compliant identifiers should not be changed solely to silence tooling.
- Understanding the intent behind coding standards is more important than mechanically fixing warnings.
- Upstream review may reveal opportunities to improve development tools rather than kernel code.

---

## 11. Looking Back

If revisiting this work today, I would:

- Investigate whether a reported warning reflects a genuine issue before preparing patches.
- Validate automated tool output against subsystem conventions.
- Consider contributing improvements to `checkpatch.pl` when appropriate.
- Focus cleanup efforts on issues that improve code quality rather than only satisfying static analysis.

---

## 12. Related Journey

- `journey/growth.md`
- Previous Series:
  - Series 000 – Exploratory cleanup.h conversions
  - Series 001 – ST Sensors buffer reuse
  - Series 002 – SSP Sensors modernization
  - Series 003 – GC0310 Clock Modernization

---

## 13. Related Learning

- `learning/review-process.md`

---

## 14. References

### Lore

- Cover Letter (0/3)
- Patch 1
- Patch 2
- Patch 3

### Discussion

- Andy Shevchenko review explaining the `checkpatch.pl` limitation.
