# LFX Linux Kernel Mentorship — Spring 2026

**Final Report — Sanjay Chitroda**  
**Mentorship:** 1 March 2026 – 31 August 2026  
**Primary subsystem:** Industrial I/O (IIO)  
**Mentors:** Shuah Khan & Brigham Campbell

---

## 1. Mentorship summary

The LFX Linux Kernel Mentorship gave me six months of focused experience contributing to the upstream Linux kernel, primarily in the Industrial I/O (IIO) subsystem.

I entered the mentorship with more than eight years of Embedded Linux experience covering BSP development, Linux device drivers, multimedia systems, the Yocto Project and Linux kernel development in product environments. I already had upstream contribution experience through Yocto; the specific goal of this mentorship was to build deeper and sustained experience in the **upstream Linux kernel community**.

The mentorship focused on practical upstream development rather than a standalone coding exercise: understanding subsystem conventions, preparing reviewable patches, working through mailing-list review, following linux-next and mainline, and learning how maintainers evaluate long-term changes.

## 2. Graduation requirement and contribution result

The LFX graduation requirement was at least five accepted upstream kernel patches during the mentorship. I exceeded that requirement with **21 accepted mainline commits** during the mentorship period.

In addition, **27 further changes progressed through linux-next**, giving a total of **48 kernel contributions** across mainline and linux-next.

For the graduation requirement, I count the substantive mainline changes below and do **not** rely on spelling-only or code-formatting-only patches as qualifying contributions.

| Result | Count |
|---|---:|
| Accepted in mainline | **21** |
| Additional accepted/progressing in linux-next | **27** |
| Total contribution activity | **48** |
| LFX minimum requirement | **5** |

## 3. Main contribution areas

The work was centered on **driver modernization and preventive maintenance** in IIO rather than waiting for a specific user-visible bug to be reported.

The main areas were:

- Modernizing drivers toward current kernel patterns.
- Resource lifetime and ownership improvements using `devm_*` and devres.
- `cleanup.h` patterns, including `__free` and `guard()` where appropriate.
- Probe and error-path improvements, including `dev_err_probe()`.
- Driver lifecycle and ordering correctness.
- HID-IIO cross-driver modernization and common infrastructure work.
- `MAINTAINERS` updates based on actual ownership and review coverage.

A recurring goal was to reduce unnecessary complexity and potential future failure paths through conservative modernization. The intent was preventive: improve lifecycle, ownership and error handling before they become sources of bugs, rather than limiting the work to reacting to an existing failure.

## 4. How my development workflow changed

Before the mentorship, I had experience implementing kernel changes in product-focused Embedded Linux environments. During the mentorship, I learned to treat an upstream contribution as a complete engineering process:

```text
Understand the subsystem
        ↓
Study existing patterns and ownership
        ↓
Choose a logical change boundary
        ↓
Implement and validate
        ↓
Prepare the patch / series
        ↓
Submit to the mailing list
        ↓
Receive review
        ↓
Revise or restructure
        ↓
Track linux-next
        ↓
Track mainline
```

The biggest change was in how I judged a patch. Before mentorship, I thought a good patch was primarily about fixing the code. During the mentorship I learned that a good upstream patch must also be easy to **review, maintain, integrate and bisect**.

## 5. Review-driven learning

The review process was one of the most valuable parts of the mentorship. Review feedback sometimes changed individual lines, but it could also change the scope and structure of an entire series.

My first memorable experience was a multi-patch series spanning multiple subsystems. The series was not accepted as-is, but constructive review comments and reviewer guidance helped redirect the work and ultimately shaped the subsystem focus of my six-month journey.

The clearest review principle I took away was:

> **“The rule of thumb is one logical change per patch.”**

Keeping logical boundaries makes a patch easier to review, maintain and bisect when a later regression needs investigation.

The HID-IIO work was another important example. The work grew to a 36-patch series before review-driven restructuring separated common infrastructure from driver-specific conversions. That experience taught me that implementation relationships do not automatically define the right patch-series boundaries.

## 6. Representative accepted contributions

Rather than reproducing a raw `git log`, the following table groups the mainline work into representative engineering themes. The commit links provide the exact upstream evidence.

| Area | Representative contribution | Lesson / impact |
|---|---|---|
| `mma8452` | `dev_err_probe()`, I2C error handling, IRQ/resource decisions | Probe/error-path reasoning and careful resource ownership |
| ADXL3xx | `dev_err_probe()`, devm-managed mutex initialization | Preventive modernization and consistent lifecycle handling |
| SSP sensors | Delayed-work cancellation and cleanup | Remove-path correctness and workqueue lifetime |
| HID-IIO | Callback setup vs. device exposure ordering | Lifecycle, concurrency and externally visible state |
| `MAINTAINERS` | IIO ownership/review coverage updates | Sustainable upstream ownership and review paths |
| ST sensors | Temporary buffer/lifetime cleanup | Simpler resource handling and maintainability |

## 7. Accepted mainline contributions

The following are the **21 accepted mainline commits** attributed to me during the mentorship period. The list is intentionally separated from linux-next work so the graduation evidence is easy to verify.

| Commit | Subsystem / change | Type |
|---|---|---|
| [32a5c04d](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=32a5c04d457540af67507494f30261580213df94) | `iio: accel: mma8452: Use dev_err_probe()` | Error handling |
| [0a6726ec](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=0a6726ec20cd4c0101f2de0ca485a11676224dea) | `iio: accel: mma8452: switch to non-devm request_threaded_irq()` | Resource / IRQ lifecycle |
| [5bdff291](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=5bdff291d20c31b365d9ddfe9c426fbfb41da5bb) | `iio: accel: mma8452: handle I2C read error(s)` | Error handling |
| [bdc573d5](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=bdc573d5c33b90a21c3799c1b3f08dc8092188af) | `MAINTAINERS: Update maintainer for IIO drivers` | Ownership |
| [d350cb2b](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=d350cb2b23aee0f9a5107e87dc80929f93a04b00) | `MAINTAINERS: Update Analog Devices IIO drivers entry` | Ownership |
| [eedf7602](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=eedf7602fbd929e97e0c480da501dc7a34beb2a8) | `iio: ssp_sensors: cancel delayed work_refresh on remove` | Lifecycle |
| [d47d6bdc](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=d47d6bdc81cfe56a1e7af40528ac81162a547e1b) | `iio: accel: adxl372: Use dev_err_probe()` | Error handling |
| [24ab1d9a](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=24ab1d9a2fc4c1e4f2546bebcee2b420295120a0) | `iio: accel: adxl372: Use devm-managed mutex initialization` | Resource management |
| [f710a0fa](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=f710a0fa462ce5fc356ab4a77787b49fc1f47f7b) | `iio: accel: adxl367: Use devm-managed mutex initialization` | Resource management |
| [70cc2c65](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=70cc2c65c23ba212c6de61a727131ebf94a66610) | `iio: accel: adxl355: Use dev_err_probe()` | Error handling |
| [07fd6291](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=07fd62916c7d2adb65926b989d337c7bfc7b2357) | `iio: accel: adxl355_core: Use devm-managed mutex initialization` | Resource management |
| [1ed49c5e](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=1ed49c5e6b6da868ff226706d54919e1e10cf991) | `iio: accel: adxl380: Use devm-managed mutex initialization` | Resource management |
| [c27837e4](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=c27837e49fd1fa0eae1b6d3988d2ae5a9d924739) | `iio: accel: adxl313: Use dev_err_probe()` | Error handling |
| [d2ed8a2f](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=d2ed8a2f630abe69d87eeffb2781df9237d7c1dd) | `iio: accel: adxl313_core: Use devm-managed mutex initialization` | Resource management |
| [1ac30f58](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=1ac30f58f0336287203109872f71a81d4bb271db) | `iio: st_sensors: drop temporary kmalloc buffer and reuse buffer_data` | Buffer / lifetime |
| [74c39233](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=74c3923344c6ad4b7199948d54dc947504c39483) | `iio: ssp_sensors: cleanup codestyle warning` | Cleanup* |
| [a9ecd9a1](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=a9ecd9a121752f2d7bb69da264bda65b6b6e6c6e) | `iio: ssp_sensors: cleanup codestyle check` | Cleanup* |
| [dcc80f2f](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=dcc80f2fdff721ced4ea1ef7a3ea43f3fbe0b27a) | `iio: ssp_sensors: cleanup codestyle warning` | Cleanup* |
| [b4f6b124](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b4f6b124467f5d770e170d93e6e12a2fe3977927) | `iio: accel: mma8452: cleanup codestyle warning` | Cleanup* |
| [e9f14394](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=e9f143941584ae27e9981649a3f9916c322ee01d) | `iio: accel: mma8452: sort headers alphabetically` | Cleanup* |

*Cleanup/spelling/code-format changes are retained as contribution history for completeness, but are not relied upon for the LFX graduation requirement.

## 8. Additional linux-next contributions

A further **27 changes** progressed through linux-next during the mentorship. These included HID-IIO lifecycle fixes, devres modernization, type cleanups and cross-driver improvements.

Representative examples include:

- `iio: accel: hid-sensor-accel-3d: Avoid race between callback setup and device exposure`
- `iio: magnetometer: hid-sensor-magn-3d: Avoid race between callback setup and device exposure`
- `iio: temperature: hid-sensor-temperature: switch to non-devm iio_device_register()`
- `iio: hid-sensors: use common device for devres`
- Multiple HID-IIO conversions from `unsigned int` to `u32`
- IIO resource-management TODO refinement
- `media: i2c: gc0310: Use devm_v4l2_sensor_clk_get()`

The complete author log is retained in the repository history and linked below.

## 9. Testing, validation and tools

Testing was matched to the claim being made by each patch. For driver modernization and cleanup work, validation commonly included:

- Kernel builds and warning checks.
- `W=1` builds where applicable.
- `checkpatch.pl` and kernel coding-style checks.
- Sparse and `coccicheck` where applicable.
- Source-level inspection of probe, remove and error paths.
- Review of lifecycle and ordering changes against existing subsystem patterns.
- linux-next tracking after acceptance into subsystem development.

Dedicated hardware was not available for every IIO driver, so compilation, static analysis and code inspection are **not represented as hardware validation**. Where a change depended on hardware-specific behavior, I treated the absence of hardware as a limitation rather than claiming validation that was not performed.

Other tools and resources used throughout the mentorship included Git, `b4`, mailing-list archives, `lore.kernel.org`, Sashiko review results and the Linux kernel development trees.

## 10. Syzbot and bug-analysis experience

I did not use a Syzbot bug as the primary driver for the mentorship contribution work. The project started from a **preventive-maintenance mindset**: modernize existing IIO drivers according to current kernel practices, improve ownership and lifecycle handling, and reduce potential failure paths before a user-visible bug is reported.

As a result, there are no Syzbot bugs in this report claimed as fixed. I do not want to manufacture a bug-fixing narrative where the actual mentorship work was focused elsewhere.

The self-learning and analysis work instead centered on reviewing existing driver behavior, understanding subsystem lifecycle and resource ownership, following review discussions, and reasoning about possible failure paths introduced by ordering or resource-management changes.

## 11. What I learned from the mentorship

### From my mentors

Shuah Khan's office-hour discussions and Brigham Campbell's guidance helped me understand that upstream contribution includes much more than writing code. Important lessons included starting to contribute before knowledge feels complete, learning how to validate and review other changes, understanding linux-next and merge windows, and using standard kernel communication and patch-management practices.

### From fellow mentees

Fellow mentees provided **motivation and accountability**. Seeing others make progress, discuss reviews and continue submitting work helped maintain momentum during longer review cycles.

### From the Linux kernel community

The community reinforced the importance of **constructive feedback and maintainability over cleverness**. The review process showed that the quality of an upstream change is measured not only by whether it works, but also by whether other developers can understand, review, maintain and integrate it.

## 12. Mentorship outcome

The biggest outcome was a change in how I approach kernel development.

I entered the mentorship with product-focused Embedded Linux and kernel experience. I leave with practical experience in an upstream subsystem, mailing-list development, review-driven patch restructuring, linux-next tracking and mainline integration.

The central lesson is:

> **A good upstream patch is not only about fixing the code. It is about making the change easy to review, maintain and integrate.**

I plan to continue contributing to IIO, participate more actively in upstream review and expand my Linux kernel development experience beyond the mentorship.

## Contribution sources

- **Mainline:** https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/log/?qt=author&q=sanjay+chitroda
- **linux-next:** https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/log/?qt=author&q=sanjay+chitroda
- **Mentorship repository:** https://github.com/sanjay-embedded/LFX-Linux-kernel-Spring-2026
- **Kernel upstream contribution guide:** https://github.com/sanjay-embedded/oss-guide/blob/master/kernel-upstream.rst
