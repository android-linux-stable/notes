# 3.18.66 to 3.18.92


* `Makefile`

  * **Resolution:** Take right side

  * **Cause:** CAF's upgrade from 3.18.63 to 3.18.66 was squashed in commit [`8cc3973a1385`](https://github.com/OnePlusOSS/android_kernel_oneplus_msm8996/commit/8cc3973a13855b9040c89e5d85572ab4e7c1d5db) ("Synchronize codes for OxygenOS 5.0.0").


* `drivers/gpu/drm/msm/msm_gem_submit.c`

  * **Resolution:** Take right side

  * **Cause:**

    * Commit [`77336ca65ccf`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=77336ca65ccf544bbca59d55b0a1bb10bf420fe3) ("drm/msm: fix an integer overflow test") had to be changed to work around the extra `nr` variable, added in commit [`f81b352dbb7f`](https://source.codeaurora.org/quic/la/kernel/msm-3.18/commit/?id=f81b352dbb7f8ecd938527e2c8da7523b8ea63eb) ("drm/msm: Don't limit number of GPU commands").

    * Commit [`f449835963f4`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=f449835963f47a3755d2f893a49928cf8d7ca58e) ("drm/msm: Fix potential buffer overflow issue") is already present as commit [`9be5b16de622`](https://source.codeaurora.org/quic/la/kernel/msm-3.18/commit/?id=9be5b16de622c2426408425e3df29e945cd21d37) ("drm/msm: Fix potential buffer overflow issue".


* `drivers/net/usb/qmi_wwan.c`, `drivers/usb/class/cdc-acm.c`, `drivers/usb/core/quirks.c`, `drivers/usb/serial/cp210x.c`, `drivers/usb/serial/option.c`, `drivers/usb/serial/qcserial.c`, and `sound/usb/quirks.c`

  * **Resolution:** Take right side (make final diff match upstream's)

  * **Cause:** The changes to these files were omitted by CAF during the merge up to 3.18.66 (every merge commit message states that USB changes were completely ignored).


* `fs/f2fs/super.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** Stable commit [`64133595b549`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=64133595b549c1036ffe8598f4c53aa355d9e3f1) ("f2fs: sanity check checkpoint segno and blkoff") is already present in this tree as a part of OnePlus commit [`8cc3973a1385`](https://github.com/OnePlusOSS/android_kernel_oneplus_msm8996/commit/8cc3973a13855b9040c89e5d85572ab4e7c1d5db) ("Synchronize codes for OxygenOS 5.0.0") and the addition of mainline commit [`2040fce83fe1`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=2040fce83fe17763b07c97c1f691da2bb85e4135) ("f2fs: detect wrong layout") prevented git from resolving cleanly.


* `include/linux/workqueue.h`

  * **Resolution:** Take right side

  * **Cause:** Stable commit [`06114f074b92`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=06114f074b92f87eeaf12e2560362a2105a1d5b3) ("workqueue: implicit ordered attribute should be overridable") is already present in this tree as part of OnePlus commit [`8cc3973a1385`](https://github.com/OnePlusOSS/android_kernel_oneplus_msm8996/commit/8cc3973a13855b9040c89e5d85572ab4e7c1d5db) ("Synchronize codes for OxygenOS 5.0.0") but the follow up fix in commit [`18f9ff5c8ad5`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=18f9ff5c8ad53a70aff203d79dc76fada3829101) ("workqueue: Fix flag collision") is not, meaning git couldn't resolve cleanly.


* `mm/cma.c`

  * **Resolution:** Take modified right side (make diff match upstream's)

  * **Cause:** CAF commits [`263a20e2ca96`](https://source.codeaurora.org/quic/la/kernel/msm-3.18/commit/?id=263a20e2ca967e1e68c1e7a87fa5c4cd882f8c81) ("mm: cma: sleep between retries in cma_alloc"), [`4d24f88f41ff`](https://source.codeaurora.org/quic/la/kernel/msm-3.18/commit/?id=4d24f88f41ffce3195bd6f0faf16cd4bd5c66b27) ("cma: skip kmemleak for common cma region"), and [`91d62943f4e2`](https://source.codeaurora.org/quic/la/kernel/msm-3.18/commit/?id=91d62943f4e2dcfeb3c1163900d67114fa9ec8c9) ("mm: cma: add trace events for CMA allocations and freeings") added various includes and changes to this file. 


* `net/ipv4/raw.c`

  * **Resolution:** Take right side (make final diff match upstream's)

  * **Cause:** When mainline commit [`8f659a03a0ba`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=8f659a03a0ba9289b9aeb9b4470e6fb263d6f483) ("net: ipv4: fix for a race condition in raw_sendmsg") was backported to the 3.18 stable tree as commit [`000c7141a1fe`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=000c7141a1feace09bf4c0f65008e51fa69ecede), it was slightly changed because mainline commit [`e2d118a1cb5e`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=e2d118a1cb5e60d077131a09db1d81b90a5295fe) ("net: inet: Support UID-based routing in IP protocols.") is not present in the stable 3.18 tree. However, since CAF merged kernel/common from Google, it is present as commit [`04c0eace816f`](https://source.codeaurora.org/quic/la/kernel/msm-3.18/commit/?id=04c0eace816f2b2c33830ec7f5e882de674841ae) ("net: inet: Support UID-based routing in IP protocols.") so adjust the diff to account for this (final diff matches both the stable and mainline commit).


* `net/ipv6/output_core.c`

  * **Resolution:** Take right side

  * **Cause:** The history of 3.18.64 that contained stable commit [`41d33a5b803b`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=41d33a5b803bd1c3ca84f5bfb9ab77d06ce09fca) ("ipv6: avoid overflow of offset in ip6_find_1stfragopt") was lost in OnePlus commit [`8cc3973a1385`](https://github.com/OnePlusOSS/android_kernel_oneplus_msm8996/commit/8cc3973a13855b9040c89e5d85572ab4e7c1d5db) ("Synchronize codes for OxygenOS 5.0.0"), causing the application of stable commit [`51ef0b663c13`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=51ef0b663c13cffbc1cc74102122bd4013726c1b) ("ipv6: accept 64k - 1 packet length in ip6_find_1stfragopt()") to fail.


* `net/ipv4/raw.c`

  * **Resolution:** Take right side (make final diff match upstream's)

  * **Cause:** When mainline commit [`8f659a03a0ba`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=8f659a03a0ba9289b9aeb9b4470e6fb263d6f483) ("net: ipv4: fix for a race condition in raw_sendmsg") was backported to the 3.18 stable tree as commit [`000c7141a1fe`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=000c7141a1feace09bf4c0f65008e51fa69ecede), it was slightly changed because mainline commit [`e2d118a1cb5e`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=e2d118a1cb5e60d077131a09db1d81b90a5295fe) ("net: inet: Support UID-based routing in IP protocols.") is not present in the stable 3.18 tree. However, since CAF merged kernel/common from Google, it is present as commit [`04c0eace816f`](https://source.codeaurora.org/quic/la/kernel/msm-3.18/commit/?id=04c0eace816f2b2c33830ec7f5e882de674841ae) ("net: inet: Support UID-based routing in IP protocols.") so adjust the diff to account for this (final diff matches both the stable and mainline commit).


* `net/sched/act_ipt.c`

  * **Resolution:** Take right side

  * **Cause:** The history of 3.18.65 that contained stable commit [`74926bfeaf9b`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=74926bfeaf9bab3f6a6bedaef5ff79d32bd38c1a) ("net: sched: set xt_tgchk_param par.nft_compat as 0 in ipt_init_target") was lost in OnePlus commit [`8cc3973a1385`](https://github.com/OnePlusOSS/android_kernel_oneplus_msm8996/commit/8cc3973a13855b9040c89e5d85572ab4e7c1d5db) ("Synchronize codes for OxygenOS 5.0.0"), causing the application of stable commit [`28ae858736a4`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=28ae858736a42b37ff4352e3cb46e4a9e9299d2f) ("net: sched: fix NULL pointer dereference when action calls some targets") to fail.


# 3.18.94

* `drivers/input/input.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** Commit [`33fd368597ad`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=33fd368597ad615f9f7232ca9daa3ed3fdba1516) is already present in this tree as commit [`b7e92bfe94d1`](https://source.codeaurora.org/quic/la/kernel/msm-3.18/commit?id=b7e92bfe94d17178fea6c12552ab5fbafd48ad96) but git couldn't tell because the context of the stable version was adjusted due to absence of mainline commit [`3e2b03dad54b`](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=3e2b03dad54bbcab5be948629a644d55ce7b5a2e), which is present in our tree as commit [`f4497aed6014`](https://source.codeaurora.org/quic/la/kernel/msm-3.18/commit?id=f4497aed6014730521b7736db0139ebb6fadeee5). The version in our tree is identical to mainline commit [`00159f19a505`](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=00159f19a5057cb779146afce1cceede692af346) so no changes are necessary.


* `drivers/usb/gadget/function/f_fs.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** Commit [`3e6a2db8df25`](https://source.codeaurora.org/quic/la/kernel/msm-3.18/commit?id=3e6a2db8df258fc6d609a2827d0e0cbe30fbbce0) removed the statement modified by stable commmit [`512b79f1410f`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=512b79f1410fd05c2c7f2aab9fb4b0050560db89).
