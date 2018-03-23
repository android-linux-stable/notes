# 3.18.71 to 3.18.87

* `drivers/gpu/drm/msm/msm_gem_submit.c`

  * **Resolution:** Take right side

  * **Cause:**

    * Commit [`77336ca65ccf`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=77336ca65ccf544bbca59d55b0a1bb10bf420fe3) ("drm/msm: fix an integer overflow test") had to be changed to work around the extra `nr` variable, added in commit [`f81b352dbb7f`](https://source.codeaurora.org/quic/la/kernel/msm-3.18/commit/?id=f81b352dbb7f8ecd938527e2c8da7523b8ea63eb) ("drm/msm: Don't limit number of GPU commands").

    * Commit [`f449835963f4`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=f449835963f47a3755d2f893a49928cf8d7ca58e) ("drm/msm: Fix potential buffer overflow issue") is already present as commit [`9be5b16de622`](https://source.codeaurora.org/quic/la/kernel/msm-3.18/commit/?id=9be5b16de622c2426408425e3df29e945cd21d37) ("drm/msm: Fix potential buffer overflow issue".


* `drivers/scsi/sg.c`

  * **Resolution:** Take right side

  * **Cause:** Commit [`de93dd11b78f`](https://source.codeaurora.org/quic/la/kernel/msm-3.18/commit/?id=de93dd11b78f31a9ec77e072cb413ebb15f3de29) ("Prevent potential double frees in sg driver") removed some whitespace that was unexpected by commit [`691e12db75fb`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=691e12db75fb7f55bbbf8c1fea7d462eb1a5e38a) ("scsi: sg: factor out sg_fill_request_table()").


* `drivers/usb/class/cdc-acm.c`, `drivers/usb/core/quirks.c`, `drivers/usb/serial/cp210x.c`, `drivers/usb/serial/qcserial.c`

  * **Resolution:** Take right side (make final diff match upstream's)

  * **Cause:** The changes to these files were omitted by CAF during the merge up to 3.18.71 (every merge commit message states that USB changes were completely ignored).


* `net/packet/af_packet.c`

  * **Resolution:** Take right side (make diff match mainline's version)

  * **Cause:** Commit [`008ba2a13f2d`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=008ba2a13f2d04c947adc536d19debb8fe66f110) ("packet: hold bind lock when rebinding to fanout hook") was slightly modified for 3.18 as commit [`e4ffdf9ead59`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=e4ffdf9ead59a909f2824a4270356909d6d64380) ("packet: hold bind lock when rebinding to fanout hook") because commit [`d199fab63c11`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=d199fab63c11998a602205f7ee7ff7c05c97164b) ("packet: fix races in fanout_add()") is missing from 3.18. However, it is present in this tree as commit [`be671c7e1745`](https://source.codeaurora.org/quic/la/kernel/msm-3.18/commit/?id=be671c7e17454b4f144a8e05268a6071748a8791) ("UPSTREAM: packet: fix races in fanout_add()") so use the upstream resolution.


# 3.18.91

* `drivers/net/usb/qmi_wwan.c`, `drivers/usb/core/quirks.c`, and `drivers/usb/serial/option.c`

  * **Resolution:** Take right side (make final diff match upstream's)

  * **Cause:** The changes to these files were omitted by CAF during the merge up to 3.18.71 (every merge commit message states that USB changes were completely ignored).


* `net/ipv4/raw.c`

  * **Resolution:** Take right side (make final diff match upstream's)

  * **Cause:** When mainline commit [`8f659a03a0ba`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=8f659a03a0ba9289b9aeb9b4470e6fb263d6f483) ("net: ipv4: fix for a race condition in raw_sendmsg") was backported to the 3.18 stable tree as commit [`000c7141a1fe`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=000c7141a1feace09bf4c0f65008e51fa69ecede), it was slightly changed because mainline commit [`e2d118a1cb5e`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=e2d118a1cb5e60d077131a09db1d81b90a5295fe) ("net: inet: Support UID-based routing in IP protocols.") is not present in the stable 3.18 tree. However, since CAF merged kernel/common from Google, it is present as commit [`04c0eace816f`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=04c0eace816f2b2c33830ec7f5e882de674841ae) ("net: inet: Support UID-based routing in IP protocols.") so adjust the diff to account for this (final diff matches both the stable and mainline commit).


# 3.18.92

* `drivers/usb/serial/cp210x.c`

  * **Resolution:** Take right side (make final diff match upstream's)

  * **Cause:** The changes to this file were omitted by CAF during the merge up to 3.18.71 (every merge commit message states that USB changes were completely ignored).


# 3.18.94

* `drivers/input/input.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** Commit [`33fd368597ad`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=33fd368597ad615f9f7232ca9daa3ed3fdba1516) is already present in this tree as commit [`b7e92bfe94d1`](https://source.codeaurora.org/quic/la/kernel/msm-3.18/commit?id=b7e92bfe94d17178fea6c12552ab5fbafd48ad96) but git couldn't tell because the context of the stable version was adjusted due to absence of mainline commit [`3e2b03dad54b`](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=3e2b03dad54bbcab5be948629a644d55ce7b5a2e), which is present in our tree as commit [`f4497aed6014`](https://source.codeaurora.org/quic/la/kernel/msm-3.18/commit?id=f4497aed6014730521b7736db0139ebb6fadeee5). The version in our tree is identical to mainline commit [`00159f19a505`](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=00159f19a5057cb779146afce1cceede692af346) so no changes are necessary.


* `drivers/usb/gadget/function/f_fs.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** Commit [`3e6a2db8df25`](https://source.codeaurora.org/quic/la/kernel/msm-3.18/commit?id=3e6a2db8df258fc6d609a2827d0e0cbe30fbbce0) removed the statement modified by stable commmit [`512b79f1410f`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=512b79f1410fd05c2c7f2aab9fb4b0050560db89).


# 3.18.102

* `drivers/gpu/drm/msm/msm_gem.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** Commits [`46a5a5fd5fff`](https://source.codeaurora.org/quic/la/kernel/msm-3.18/commit/?id=46a5a5fd5fffffaebfe1867396af0d653375c053) ("drm:msm move GEM back buffer from SHMEM to DMA") and [`a47d70392fcd`](https://source.codeaurora.org/quic/la/kernel/msm-3.18/commit/?id=a47d70392fcdf0cf55daff156164e984383d63ff) ("drm:msm Fix issue of iommu unmap fails") heavily changed the area modified by stable commit [`1fa04de1af73`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=1fa04de1af7354d6cb795ed47bee2194ea9c8a17) ("drm/msm: fix leak in failed get_pages").
