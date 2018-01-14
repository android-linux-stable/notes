# Tips and tricks

## 1. How to resolve conflicts

While I cannot possibly teach you how to resolve every conflict given that a lot of that involves understanding C, I can give you some helpful hints about how I resolve conflicts.


* If you are merging, figure out what commit is causing the conflict. You can do this one of two ways:

  * `git log -p v$(make kernelversion)..<latest_tag>` to get the changes between your current version and the latest from upstream. The `-p` flag will give you the changes done by each commit so you can see.

  * Run `git blame` on the file to get the hashes of each commit in the area. You can then run `git show --format=fuller` to see if the committer was from mainline/stable, Google, or CodeAurora.

* Figure out if you already have the commit. Some vendors like Google or CAF will attempt to look upstream for critical bugs, like the Dirty COW fix, and their backports could conflict with upstream's. You can run `git log --grep="<part_of_commit_message>"` and see if it returns anything. If it does, you can skip the commit (if cherry-picking using `git reset --hard && git cherry-pick --continue`) or ignore the conflicts (remove the `<<<<<<` and everything between the `======` and `>>>>>>`).

* Figure out if there has been a backport that is messing up resolution. Google and CAF like to backport certain patches that stable wouldn't. Stable will often need to adapt the resolution of the mainline commit to the abscence of certain patches that Google opts to backport. You can look at the mainline commit by running `git show <hash>` (the mainline hash will be available in the commit message of the stable commit). If there is a backport messing it up, you can either discard the changes or you can use the mainline version (which is what you will usually need to do).

* Read what the commit is trying to do and see if the problem is already fixed. Sometimes CAF may fix a bug independent of upstream, meaning you can either overwrite their fix for upstream's or discard it, like above.

Otherwise, it may just be a result of a CAF/Google/OEM addition, in which case you just need to shuffle some things around.

I have [a mirror of the linux-stable kernel.org repository](https://github.com/nathanchance/linux-stable) on GitHub, which can be easier for looking up commit lists and diffs for conflict resolution. I recommend going to the commit list view first and locating the problem commit to see the original diff to compare it to yours.

Example URL:
https://github.com/nathanchance/linux-stable/commits/linux-3.10.y/arch/arm64/mm/mmu.c

You can also do it via the command line:
```bash
git log <current_version>..<version_being_added> <path>
git show <hash>
```

Solving resolutions is all about context. What you should ALWAYS do is make sure your final diff matches upstream's by running the following commands in two separate windows:

```bash
git diff HEAD

git diff v$(make kernelversion)..$(git tag --sort=-taggerdate -l v$(make kernelversion | cut -d . -f 1,2)* | head -n1)
```


## 2. Enable rerere

Git has a feature called rerere (standing for reuse recorded resolution), meaning that when it detects a conflict, it will record how you resolved it so you can reuse it later. This is especially helpful for both chronic rebasers with both merging and cherry-picking as you will just need to run
`git add . && git <merge|cherry-pick> --continue`
when redoing the upstream bringup as the conflict will be resolved how you previously resolved it.

It can be enabled by running the following command in your kernel repo: `git config rerere.enabled true`


## 3. How to git bisect when running into a compiler or runtime error

Given that you will be adding a sizable number of commits, it's very possible for you to introduce a compiler or runtime error. Instead of just giving up, you can use git's built-in bisect tool to figure out the root cause of the issue! Ideally, you will be building and flashing every single kernel version as you add it so bisecting will take less time if needed but you can bisect 5000 commits without any issues.

What `git bisect` will do is take a range of commits, from where the issue is present to where it wasn't present, and then start halving the commit range, allowing you to build and test and let it know if it is good or not. It will continue this until it spits out the commit causing your issue. At that point, you can either fix it or revert it.

1. Start bisecting: `git bisect start`
2. Label the current revision as bad: `git bisect bad`
3. Label a revision as good: `git bisect good <sha1>`
4. Build with the new revision
5. Based on the result (if the issue is present or not), tell git: `git bisect good` OR `git bisect bad`
6. Rinse and repeat steps 4-5 until the problem commit is found!
7. Revert or fix the problem commit.

**NOTE:** Mergers will need to temporarily run `git rebase -i <good_sha>` to apply all the patches to your branch for proper bisecting, as bisecting with the merges in place will often times checkout onto the upstream commits, meaning you have none of the Android specific commits. I can go into more depth on this upon request but trust me, it is needed. Once you have identified the problem commit, you can revert or rebase it into the merge.


## 4. Do NOT squash upstream updates

A lot of new developers are tempted to do this as it is "cleaner" and "easier" to manage. This is terrible for a few reasons:

* Authorship is lost. It's unfair to other developers to have their credit stipped for their work.
* Bisecting is impossible. If you squash a series of commits and something is an issue in that series, it's impossible to tell what commit caused an issue in a squash.
* Future cherry-picks are harder. If you need to rebase with a squashed series, it is difficult/impossible to tell where an conflict results from.

Leave the updates unsquashed, you'll thank me later.


## 5. Subscribe to the Linux Kernel mailing list for timely updates

In order to get notified whenever there is an upstream update, subscribe to [the linux-kernel-announce list](http://vger.kernel.org/vger-lists.html#linux-kernel-announce). This will allow you to get an email every time a new kernel is released so you can update and push as quick as possible.


## 6. Known problem commits

See the [breakage section](/info/why-is-linux-stable-important.md#there-is-a-lot-of-breakage-when-merging-and-using-linux-stable-in-my-tree) of the "why is linux-stable important?" page.
