# 3.18.70 to 3.18.87

* `drivers/media/v4l2-core/v4l2-compat-ioctl32.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** Commit [`b9c210ed25a2`](https://android.googlesource.com/kernel/msm/+/b9c210ed25a2fdb7e0ac73a36571b164213e1933) ("v4l2: Refactor, fix security bug in compat ioctl32") rewrote the `put_user` statements with a `convert_in_user` macro, which was unexpected by commit [`6b3412ff9661`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=6b3412ff96615bab06863c00c371b5601e3b1e1c) ("media: v4l2-compat-ioctl32: Fix timespec conversion"). The former fixes the issue described by the latter (as they are by the same author).


* `net/packet/af_packet.c`

  * **Resolution:** Take right side (make final diff match upstream's)

  * **Cause:** Commit [`008ba2a13f2d`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=008ba2a13f2d04c947adc536d19debb8fe66f110) ("packet: hold bind lock when rebinding to fanout hook") was slightly modified for 3.18 as commit [`e4ffdf9ead59`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=e4ffdf9ead59a909f2824a4270356909d6d64380) ("packet: hold bind lock when rebinding to fanout hook") because commit [`d199fab63c11`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=d199fab63c11998a602205f7ee7ff7c05c97164b) ("packet: fix races in fanout_add()") is missing from 3.18. However, it is present in this tree as commit [`de0f20edf203`](https://android.googlesource.com/kernel/msm/+/de0f20edf203b949ae8b0d1cebd8618f7c636f77) ("UPSTREAM: packet: fix races in fanout_add()") so use the upstream resolution.


# 3.18.91

* `net/ipv4/raw.c`

  * **Resolution:** Take right side (make final diff match upstream's)

  * **Cause:** When mainline commit [`8f659a03a0ba`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=8f659a03a0ba9289b9aeb9b4470e6fb263d6f483) ("net: ipv4: fix for a race condition in raw_sendmsg") was backported to the 3.18 stable tree as commit [`000c7141a1fe`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=000c7141a1feace09bf4c0f65008e51fa69ecede), it was slightly changed because mainline commit [`e2d118a1cb5e`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=e2d118a1cb5e60d077131a09db1d81b90a5295fe) ("net: inet: Support UID-based routing in IP protocols.") is not present in the stable 3.18 tree. However, it is in this one since Google added it as a backport in commit [`083e6660c733`](https://android.googlesource.com/kernel/msm/+/083e6660c733a56865c1ae1239c02d788a123fbd) ("net: inet: Support UID-based routing in IP protocols.") so adjust the diff to account for this (final diff matches both the stable and mainline commit).


# 3.18.94

* `drivers/input/input.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** Commit [`33fd368597ad`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=33fd368597ad615f9f7232ca9daa3ed3fdba1516) is already present in this tree as commit [`b7e92bfe94d1`](https://android.googlesource.com/kernel/msm/+/b7e92bfe94d17178fea6c12552ab5fbafd48ad96) but git couldn't tell because the context of the stable version was adjusted due to absence of mainline commit [`3e2b03dad54b`](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=3e2b03dad54bbcab5be948629a644d55ce7b5a2e), which is present in our tree as commit [`f4497aed6014`](https://android.googlesource.com/kernel/msm/+/f4497aed6014730521b7736db0139ebb6fadeee5). The version in our tree is identical to mainline commit [`00159f19a505`](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=00159f19a5057cb779146afce1cceede692af346) so no changes are necessary.


* `drivers/usb/gadget/function/f_fs.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** Commit [`3e6a2db8df25`](https://android.googlesource.com/kernel/msm/+/3e6a2db8df258fc6d609a2827d0e0cbe30fbbce0) removed the statement modified by stable commmit [`512b79f1410fd`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=512b79f1410fd05c2c7f2aab9fb4b0050560db89).
