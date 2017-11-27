# 4.4.78 to 4.4.102

* `drivers/android/binder.c`

  * **Resolution:** Take left side (discard all changes)

  * **Causes:**

    * Commit [`596b97ec2e5e`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=596b97ec2e5e24c966b9cb4aa9a9766e53ecdd43) ("binder: use group leader instead of open thread") is already present as commit [`9036bcc59e36`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=9036bcc59e36952da230f31187b1ab2f866ebfae) ("binder: use group leader instead of open thread") and commit [`359795138dc5`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=359795138dc5440e09c58025e28ec1b38d648c09) ("binder: use group leader instead of open thread") and there have been other changes to this section since then.

    * Commit [`1792d6c17cb2`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=1792d6c17cb282fd8e5cd197a8b33cb78484eb6a) ("binder: Use wake up hint for synchronous transactions.") is already present as commit [`0cebb407b2f`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=0cebb407b2f431d748d9cc85cf7e4232a9223342) ("FROMLIST: binder: Use wake up hint for synchronous transactions.") and commit [`3956eabb34de`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=3956eabb34de6b24bdbe90013c7567867bb139ea) ("android: binder: Use wake up hint for synchronous transactions.") and there have been other changes to this section since then.

    * Commit [`9dac44d5d4b0`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=9dac44d5d4b0a7fffe04ad505e0a082e900ad767) ("ANDROID: binder: fix proc->tsk check.") was included as part of commit [`9036bcc59e36`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=9036bcc59e36952da230f31187b1ab2f866ebfae) ("binder: use group leader instead of open thread").


* `drivers/gpu/drm/msm/adreno/adreno_gpu.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** Commit [`b54e58ccceb7`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=b54e58ccceb794176b37037e76df3a7ed876b360) ("drm/msm: Ensure that the hardware write pointer is valid") is already present as commit [`7d080736a4b4`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=7d080736a4b4601a16a2d81a4537d0202fc05157) ("drm/msm: Make sure that WPTR stays in bounds") and there have been other changes to this section since then.


* `drivers/gpu/drm/msm/msm_gem_submit.c`

  * **Resolution:** Take right side (reworked upstream version) for first, take left side for others

  * **Cause:**

    * Commit [`ded34f97234`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=ded34f972348b0f252256bee161839c1aa5d8ae4) ("drm/msm: fix an integer overflow test") has to be changed to work around the extra `nr` variable (added in commit [`c9d1b0f37a99`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=c9d1b0f37a99eb67d5f96e20ea37d7953558ce3c) ("drm/msm: deal with arbitrary # of cmd buffers").

    * Commit [`031b02bc16ae`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=031b02bc16aeeb34c8038026cbbca1e6430c9d75) ("drm/msm: Fix potential buffer overflow issue") is already present as commit [`a61bcfad3278`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=a61bcfad32789785760c516299035d4c28e85670) ("drm/msm: Fix potential buffer overflow issue") and there have been other changes to this section since then.

    * Commit [`7de922c14e83`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=7de922c14e838c46b3ce3ff4719bbb82ee307e8d) ("drm/msm: Verify that MSM_SUBMIT_BO_FLAGS are set") is already present as commit [`ef41564a3e4a`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=ef41564a3e4af0c3c101fae76f77b3ea65aca5be) ("drm/msm: Make sure that MSM_SUBMIT_BO_FLAGS are set").


* `drivers/gpu/drm/msm/msm_ringbuffer.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** The power of 2 alignment check in commit [`b54e58ccceb7`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=b54e58ccceb794176b37037e76df3a7ed876b360) ("drm/msm: Ensure that the hardware write pointer is valid") is already present in commit [`378583458fa1`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=378583458fa167277b15d145dccce253459393ec) ("drm/msm: Add support for multiple ringbuffers") and there have been other changes to this section since then.


* `drivers/net/wireless/ath/ath10k/core.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** Commit [`2c65494080c9`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=2c65494080c900c8a0aa4a865b57a8001960ff26) ("ath10k: fix memory leak in rx ring buffer allocation") is already present as commit [`69a6025f67b4`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=69a6025f67b41a3b03e165db46ea7d346a45ae81) ("ath10k: fix memory leak in rx ring buffer allocation") and the former did not account for commit [`9eaeb4e0974b`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=9eaeb4e0974b976a037b7c55f0fe409bccbb7fdd) ("ath10k: fix spurious tx/rx during boot"), which was added by CAF to 4.4 (since it didn't appear upstream until v4.8-rc2).


* `drivers/scsi/ufs/ufshcd.h`

  * **Solution:** Take left side (discard all changes)

  * **Cause:** Commit [`0c098158785b`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=0c098158785b5c8091c0bae3aa505060414076cc) ("scsi: ufs: add capability to keep auto bkops always enabled") is already present as commit [`9f06dddf5bee`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=9f06dddf5beecbcdf36535e0e587c23aaa7785f5) ("scsi: ufs: add capability to keep auto bkops always enabled") with a different shift value.


* `fs/f2fs/crypto_key.c`

  * **Resolution:** Take right side (mainline version)

  * **Cause:** Commit [`4db9f1113196`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=4db9f1113196e7b4df4e754e7e770b22aee81c01) ("f2fs crypto: replace some BUG_ON()'s with error checks") conflicts with commit [`26bf3dc7e25b`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=26bf3dc7e25b813ff5c92234f8165941fdc12a63) ("f2fs crypto: use per-inode tfm structure") because the latter is not in 4.4 upstream (it was added by CAF). Use the version from mainline, commit [`66aa3e1274fc`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=66aa3e1274fcf887e9d6501a68163270fc7718e7) ("f2fs crypto: replace some BUG_ON()'s with error checks").


* `kernel/power/process.c`

  * **Resolution:** Take both sides

  * **Cause:** Commit [`57caa2ad5ce3`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=57caa2ad5ce35bedb7ab374a2e5b4d7adf63da2b) ("power: Adds functionality to log the last suspend abort reason.") added an include, which was not expected by commit [`90fd6738731b`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=90fd6738731b6d105fc8f04832ae17a9ac82c05c) ("sched/cpuset/pm: Fix cpuset vs. suspend-resume bugs").

* `kernel/sched/sched.h`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** Commit [`62208707b466`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=62208707b466cc3c6ce951a7c4b7b4bb9b9192f6) ("sched/cputime: Fix prev steal time accouting during CPU hotplug") is already present as commit [`3366a508ffb6`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=3366a508ffb6b0698dd309d1ca19a66522b886b1) ("Revert "sched/cputime: Fix steal time accounting vs. CPU hotplug"") and there have been a few commits to this section since then, namely commit [`f02702dcf231`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=f02702dcf231c3258aabd702023286f6c01aaa21) ("sched: backport cpufreq hooks from 4.9-rc4").

* `mm/debug-pagealloc.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** Commit [`5c69adad61e2`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=5c69adad61e27f467fa8e1671633e455741e3fae) ("mm/page_poison.c: enable PAGE_POISONING as a separate option") renamed this file to `mm/page_poison.c`. Commit [`e34e744f70a6`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=e34e744f70a68f8f16f945a286802898c56a8b5a) ("mm: check the return value of lookup_page_ext for all call sites") does not apply to `mm/page_poison.c` as there are no more instances of `lookup_page_ext` in that file after commit [`49118fe6a32a`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=49118fe6a32a49d198128a6dd1d6bfd0e3b189f8) ("mm: enable page poisoning early at boot").

* `mm/migrate.c`

  * **Resolution:** Take both sides

  * **Cause:** Commit [`e91e9112cb03`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=e91e9112cb03570cf572365bfdaeacd1c13a3dbd) ("mm, page_owner: copy page owner info during migration") added an include, which was not expected by commit [`46d51a26efbc`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=46d51a26efbc7cbaa2bc1f01628a00a604193856) ("Sanitize 'move_pages()' permission checks").

* `mm/page_ext.c`

  * **Resolution:** Take right side

  * **Cause:** Commit [`2c00b603db67`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=2c00b603db67af40aa0b02c834cc58fec98d3023) ("mm/page_poisoning.c: allow for zero poisoning") added an extra condition to this block that commit [`3630b2801907`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=3630b28019075639a9db00491349e05fbf0f901e) ("mm/page_ext.c: check if page_ext is not prepared") did not expect.

* `mm/page_owner.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** Commit [`e34e744f70a6`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=e34e744f70a68f8f16f945a286802898c56a8b5a) ("mm: check the return value of lookup_page_ext for all call sites") is already present as commit [`acda305dcb54`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=acda305dcb5474a401753912db382358b3436ab9) ("mm: check the return value of lookup_page_ext for all call sites") and there have been several changes to this file since then.

* `net/wireless/nl80211.c`

  * **Resolution:** Take left side

  * **Cause:** Commit [`6a6c61d8467d`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=6a6c61d8467d2dd7059b7d52773c18f8122e4f68) ("nl80211: Define policy for packet pattern attributes") is already present as commit [`b084c13dfb8f`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=b084c13dfb8f9081192dc7168a94d48f419d09fc) ("nl80211: Define policy for packet pattern attributes") and the former did not account for commit [`3fee1ede34a6`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=3fee1ede34a6c3b2dd7d816643e887c2308f6a78) ("nl80211: add feature for BSS selection support") being present.

* `sound/usb/card.c`

  * **Resolution:** Take right side (shuffle resolution)

  * **Cause:** Commit [`2ecedf5dc75b`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=2ecedf5dc75bc770ec09bd2238e798063aeafc4b) ("sound: usb: Add support for parsing AudioStreaming intf for BADD devices") shuffled the function `snd_usb_create_streams`, which commit [`46c7b1fa4911`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=46c7b1fa4911a859a82575e3ffb55b34a89a222d) ("ALSA: usb-audio: Check out-of-bounds access by corrupted buffer descriptor") did not expect. Resolution is identical but has been moved into the `switch` statement to satisfy the changes made by CAF's shuffling.
