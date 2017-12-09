# Why is linux-stable important?

NOTE: Most of this information will be most revelant within the context of Android but it's also true for desktop distributions and such.


## Stable fixes

These patches have been thoroughly vetted before getting into the stable tree. There are only two ways a patch can get into the stable tree:

1. It was explicitly requested with a `cc: stable <stable@vger.kernel.org>` when the patch went into Linus's tree.
2. It was explicitly requested with either a commit ID or backported patch sent to `stable@vger.kernel.org`.

Additionally, these patches have at least three times to be validated as correct:

1. When they first go into Linus's tree (mainline)
2. When they go into the stable-queue (Greg's list of pending patches)
3. When they go into the stable-rc (Greg's list of patches that will be released after two days of review).

The author and subsystem maintainer get an email for numbers 2 and 3, meaning that they can say if the patch is good or not. There are times where things are missed but the critical errors are often fixed within a few hours (Wi-Fi broke in 4.9.55, 4.9.56 was released 10 hours later and CONFIG_PAGE_POISON was broken in 4.4.101, 4.4.102 was released 5 hours later).

Lastly, as stated in the [what is linux-stable](what-is-linux-stable.md), these patches fix legitimate issues, not theoretical ones.


## Lots of investment behind it

First and foremost, the Linux kernel is the biggest software development project in the world and many many companies contribute to it, like Redhat, Intel, Google, Facebook, and many more. In fact, Google has been working with Greg to get these stable releases into their common Android kernel on the [android-3.18 branch](https://android-review.googlesource.com/q/project:kernel%252Fcommon+branch:android-3.18+owner:%2522Greg+Kroah-Hartman+%253Cgregkh%2540google.com%253E%2522+is:merged+into+android-3.18), [android-4.4 branch](https://android-review.googlesource.com/q/project:kernel%252Fcommon+branch:android-4.4+owner:%2522Greg+Kroah-Hartman+%253Cgregkh%2540google.com%253E%2522+is:merged+into+android-4.4), and [android-4.9 branch](https://android-review.googlesource.com/q/project:kernel%252Fcommon+branch:android-4.9+owner:%2522Greg+Kroah-Hartman+%253Cgregkh%2540google.com%253E%2522+is:merged+into+android-4.9), which are in turn merged into Qualcomm's vendor kernel trees. If they weren't confident these releases weren't 100% stable or worthwhile, they wouldn't put the effort (and by extension, money) behind it. Facebook has stated that they upgrade their servers with the stable kernels and experience no issues when doing so.


## Get fixes as soon as they are available

When important vulnerabilities are disclosed/fixed, the stable kernels are the first ones to get them. Sure, you could watch CVE lists to get the fixes but there are already other people doing that. It's easier to just take the stable release when it drops. Just two examples...

* Commit [`9691eac5593f`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit?id=9691eac5593ff1e2f82391ad327f21d90322aec1) ("mm: remove gup_flags FOLL_WRITE games from __get_user_pages()"), otherwise referred to as the fix for the Dirty COW vulnerability, was released in 3.10.104 on October 21st. It wasn't added to Google trees until [their December 2016 security update](https://source.android.com/security/bulletin/2016-12-01). That is fast in the world of software development but by tracking linux-stable, that could be added and flashed day one.

* Commit [`4f996e234dad`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=4f996e234dad488e5d9ba0858bc1bae12eff82c3) ("percpu: fix synchronization between chunk->map_extend_work and chunk destruction") was labeled as a "critical" security fix by Google in [their December 2016 security update](https://source.android.com/security/bulletin/2016-12-01). It was fixed in 3.18.37, which was released on July 13th, 2016. That's a gap of six months!

There are certainly others I could find but the point is ignore CVEs, the fixes get added to linux-stable almost as soon as they are available so tracking those results in the least amount of effort for the most gain.


## Common complaints from Android developers

### "Most of the fixes are for architectures/drivers we don't use/run"

Depending on your version of "mostly", this is true. There is a lot of code Android doesn't use in the Linux kernel. However, that means there will be no conflicts from those files when merging new version! Nobody builds every single part of the kernel, not even your most common distributions like Ubuntu or Mint. It doesn't mean you shouldn't be taking these fixes because there ARE fixes for drivers you DO run. Take arm/arm64 and ext4 for example, which are the most common Android architecture and file system respectively. In 4.4, from 4.4.21 (version of the latest Nougat CAF tag) to 4.4.103 (latest upstream tag), these are the following numbers for the commits of those systems:

```bash
nathan@flashbox ~/kernels/linux-stable (master) $ git log --format=%h v4.4.21..v4.4.103 | wc -l
3599

nathan@flashbox ~/kernels/linux-stable (master) $ git log --format=%h v4.4.21..v4.4.103 arch/arm | wc -l
91

nathan@flashbox ~/kernels/linux-stable (master) $ git log --format=%h v4.4.21..v4.4.103 arch/arm64 | wc -l
45

nathan@flashbox ~/kernels/linux-stable (master) $ git log --format=%h v4.4.21..v4.4.103 fs/ext4 | wc -l
63
```

Sure, there may even be patches in those folders that aren't run or built but that blanket statement is false. A quote from Greg Kroah-Hartman...

> These are known bug fixes that you need to be taking. Take them all, don't cherry-pick. Don't say "this isn't good, this isn't bad", look at them and take them all. There's no reason you shouldn't be taking them all. If you say "oh I don't want to take them all because I don't build all those patches or I don't build those drivers" then take them anyways, it doesn't matter, it's just empty code in your tree. It makes your merge harder. Take them  all and merge them in so you know you're clean and you're good going forward".

### "There is a lot of breakage when merging and using linux-stable in my tree"

In fact, within the three Android versions I have personally worked with (3.10, 3.18, 4.4), I have only had to revert a small handful of commits for various reasons. Yes, conflicts can sometimes be tricky to solve depending on the context but they are easily resolvable by looking at what was done to cause the conflict (using `git log` and `git blame`).

* 3.10: Only commit [`9a76e683b643`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?h=linux-3.10.y&id=9a76e683b64361450f3e331dd6634f5aa39ea51b) ("ASoC: compress: Fix compress device direction check") needed to be reverted, as it broke sound. For context, the Nexus 6P ships with a 3.10.73 kernel where as linux-stable is up to 3.10.108.
```bash
nathan@flashbox ~/kernels/linux-stable (master) $ git log --format=%h v3.10.73..v3.10.108 | wc -l
2337
```

* 3.18: Only commit [`08b1ade02e58`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?h=linux-3.18.y&id=08b1ade02e584ac5eb8d9c075debf202bed9d085) ("pinctrl: qcom: Don't clear status bit on irq_unmask") needed to be reverted, done by CAF in commit [`8b4f04992b06`](https://source.codeaurora.org/quic/la/kernel/msm-3.18/commit?id=8b4f04992b064cb0c6d78adc2c2593f1aec92773) ("pinctrl: qcom: Clear status bit on irq_unmask"). The OnePlus 3 ships with a 3.18.31 kernel on Nougat where as linux-stable is up to 3.18.85.
```bash
nathan@flashbox ~/kernels/linux-stable (master) $ git log --format=%h v3.18.31..v3.18.85 | wc -l
2394
```

* 4.4: Only commit [`800791e7e0fd`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?h=linux-4.4.y&id=800791e7e0fd9835be2f55c55147c379888b7442) ("pinctrl: qcom: Don't clear status bit on irq_unmask") and commit [`e2968fb8e798`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?h=linux-4.4.y&id=e2968fb8e7980dccc199dac2593ad476db20969f) ("ext4: require encryption feature for EXT4_IOC_SET_ENCRYPTION_POLICY") needed to be reverted. The former was done by Google in commit [`7d16e880c625`](https://android.googlesource.com/kernel/common/+/7d16e880c62547936b431cde966d17e39e6e92e0) ("Revert "ext4: require encryption feature for EXT4_IOC_SET_ENCRYPTION_POLICY"") and the latter was done by CAF in commit [`ce9e5bde6654`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=ce9e5bde6654677cb61c4685f5f164d89cba2a0b) ("pinctrl: qcom: Clear status bit on irq_unmask"). The OnePlus 5 and 5T ship with a 4.4.21 kernel on Nougat where as linux-stable is up to 4.4.103.
```bash
nathan@flashbox ~/kernels/linux-stable (master) $ git log --format=%h v4.4.21..v4.4.103 | wc -l
3599
```

Those numbers don't lie: out of two to three thousand commits, there is almost next to zero breakage when merging in linux-stable and furthermore, git has built-in tools to easily deal with breakage (namely `git bisect`) so dealing with issues is not that difficult at all.

### "It takes too much time/effort"

This can be true, especially for a bring up like 4.4.21 to 4.4.102. However, when I first did it for the OnePlus 5, it probably took me an evening (like 4-5 hours). The most time consuming part is the initial bring up; once you are all the way up to date, it takes no time at all to merge in a new release, which usually contains no more than 100 commits. The benefits that this brings (more stability and better security for your users) should necessitate this process though.

### "I'm secure enough with Google and CAF's patches" OR "We merge in all relevant CVEs"

Not all fixes are labeled as security vulnerabilities even though they may be discovered to be so later on. Also, Google and CAF do not find all the relevant bug and security fixes in upstream. Just in the security update which I linked above, there was a critical security fix in a kernel released in July that was not released to the public via an Android security update until December. There are plenty of other instances where that happens. Greg Kroah-Hartman states it best in [his Kernel Recipes 2017 talk](https://youtu.be/RKadXpQLmPU?t=24m26s) and [a Google+ post regarding CVEs](). Be sensible and merge everything.


## Demonstration

Greg Kroah-Hartman gave [a talk at Kernel Recipes 2017](https://youtu.be/RKadXpQLmPU?t=46m37s) where he did a demonstration on the Pixel XL (Google's latest flagship at the time) with the latest security patch, running a 3.18.52. Using an untrusted app and context, he was able to shut down the device with a simple C program. The fix for this bug was available in 3.18.60, which was released two months later. By taking the latest update as soon as it is available, you make sure you are secure as possible. As Greg said himself:

> If you are not using a[n up to date] stable / longterm kernel, your machine is insecure."

Kees Cook would later say:

>If you are not using the latest kernel, you don't have the most recently added security defenses, which, in the face of newly exploited bugs, may render your machine less secure than it could have been.

Basically... take the updates!!
