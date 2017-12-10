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

  * **Cause:** The changes to these file were omitted by CAF during the merge up to 3.18.71 (every merge commit message states that USB changes were completely ignored).


* `net/packet/af_packet.c`

  * **Resolution:** Take right side (make diff match mainline's version)

  * **Cause:** Commit [`008ba2a13f2d`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=008ba2a13f2d04c947adc536d19debb8fe66f110) ("packet: hold bind lock when rebinding to fanout hook") was slightly modified for 3.18 as commit [`e4ffdf9ead59`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=e4ffdf9ead59a909f2824a4270356909d6d64380) ("packet: hold bind lock when rebinding to fanout hook") because commit [`d199fab63c11`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=d199fab63c11998a602205f7ee7ff7c05c97164b) ("packet: fix races in fanout_add()") is missing from 3.18. However, it is present in this tree as commit [`be671c7e1745`](https://source.codeaurora.org/quic/la/kernel/msm-3.18/commit/?id=be671c7e17454b4f144a8e05268a6071748a8791) ("UPSTREAM: packet: fix races in fanout_add()") so use the upstream resolution.
