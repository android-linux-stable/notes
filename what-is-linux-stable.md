# What is linux-stable?


## Background

[linux-stable](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git), as its name somewhat obviously implies, is the stable arm of the Linux kernel. The other arm is called "mainline", which is the master branch. All development happens in mainline, according to the following process:
1. [Linus Torvalds](https://github.com/torvalds) will take a bunch of patches from his maintainers for two weeks.
2. After this two weeks, he releases an rc1 (e.g. 4.14-rc1) kernel.
3. For each week for the next 6-8 weeks, he will release another RC (e.g. 4.14-rc2, 4.14-rc3, etc) kernel, which contains ONLY bug and regression fixes.
4. Once it is deemed stable, it will be released as a tarball for download on [kernel.org](https://www.kernel.org) (e.g. 4.14).

The stable process exists because people don't want to worry about steps 1-3 in the above process. While there are not many issues during development, they can happen. This is the stable process:
1. Once a kernel is released on kernel.org, [Greg Kroah-Hartman](https://github.com/gregkh), the stable kernel maintainer, will take it and fork it to the linux-stable repo.
2. He'll add patches from mainline that fix issues or code in the older kernel(s).
3. After the patch has been added to his queue, he'll do an RC push for testing.
4. After the RC has been tested for two days, he'll release an stable kernel (e.g. 4.14.1, 4.14.2, etc).

These two processes work side by side to make sure users are getting the highest quality end product.


## Long-term support kernels

Every year, Greg will pick one kernel and maintain it for either two years (LTS) or six years (extended LTS). These are designed to have products that need stability (like Android phones or other IOT devices). The process is the exact same as above, it just happens for a longer time. There are currently six LTS kernels (which can always be viewed on [the kernel.org releases page](https://www.kernel.org/category/releases.html)):
- [4.14 (LTS)](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/log/?h=linux-4.14.y), maintained by Greg Kroah-Hartman
- [4.9 (LTS)](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/log/?h=linux-4.9.y), maintained by Greg Kroah-Hartman
- [4.4 (eLTS)](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/log/?h=linux-4.4.y), maintained by Greg Kroah-Hartman
- [4.1(LTS)](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/log/?h=linux-4.1.y), maintained by Sasha Levin
- [3.16 (LTS)](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/log/?h=linux-3.16.y), maintained by Ben Hutchings
- [3.2 (LTS)](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/log/?h=linux-3.2.y), maintained by Ben Hutchings

When a company bases a product off of a long-term support kernel, they'll usually need to add platform specific patches. In Android, this is for stuff like the touchscreen, speakers, vibration motor, and SoC. Because this stuff is out of tree, it can take a long time to update those things for new kernel versions, necessitating something that is maintained for a long time. Taking these linux-stable patches are even more important because they can't jump ahead to a mainline kernel that would automatically have all this stuff.


## What is a stable patch?

Thankfully, the stable maintainers have created a set of rules for what patches can and cannot go into a stable tree, which guarantees stability:
 - It must be obviously correct and tested.
 - It cannot be bigger than 100 lines, with context.
 - It must fix only one thing.
 - It must fix a real bug that bothers people (not a, "This could be a problem..." type thing).
 - It must fix a problem that causes a build error (but not for things marked CONFIG_BROKEN), an oops, a hang, data corruption, a real security issue, or some "oh, that's not good" issue.  In short, something critical.
 - Serious issues as reported by a user of a distribution kernel may also be considered if they fix a notable performance or interactivity issue. As these fixes are not as obvious and have a higher risk of a subtle regression they should only be submitted by a distribution kernel maintainer and include an addendum linking to a bugzilla entry if it exists and additional information on the user-visible impact.
 - New device IDs and quirks are also accepted.
 - No "theoretical race condition" issues, unless an explanation of how the race can be exploited is also provided.
 - It cannot contain any "trivial" fixes in it (spelling changes, whitespace cleanups, etc).
 - It must follow the [Documentation/process/submitting-patches.rst](https://github.com/torvalds/linux/blob/master/Documentation/process/submitting-patches.rst) rules.
 - It or an equivalent fix must already exist in Linus' tree (upstream).

 The last one is super important because it makes sure that jumping forward (whenever possible) doesn't introduce new bugs. Everything else keeps the stable trees sane, which means you should update yours to match the latest!


## Sources

- [2. Process.rst](https://github.com/torvalds/linux/blob/master/Documentation/process/2.Process.rst)
- [stable-kernel-rules.rst](https://github.com/torvalds/linux/blob/master/Documentation/process/stable-kernel-rules.rst)
- [Kernel Recipes 2017 - Linux Kernel release model - Greg KH](https://www.youtube.com/watch?v=RKadXpQLmPU)
- [Linux Kernel Development, Greg Kroah-Hartman - Git Merge 2016](https://www.youtube.com/watch?v=vyenmLqJQjs)
- [Keynote: State of the Linux Kernel, Greg Kroah-Hartman](https://www.youtube.com/watch?v=SIQr2-Dh0es)
