# How to merge linux-stable into an Android kernel

## 1. Figure out what version you are on

As trivial as this seems, it is necessary to know where you need to begin. Run the following command in your kernel tree:
```bash
make kernelversion
```

It will spit back some version. The first two number will be used to figure out the branch you need (e.g. linux-4.4.y for any 4.4 kernel) and the last number will be used to determine what version you need to start with merging (e.g. if you are on 4.4.21, you'll merge 4.4.22 next).

## 2. Fetch the latest kernel source from kernel.org

[kernel.org](https://www.kernel.org/) houses the latest kernel source in [the linux-stable repository](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/). At the bottom of that page, there will be three fetch links. In my experience, Google's mirror tends to be the fastest but your results may vary. Run the following commands:
```bash
git remote add linux-stable https://kernel.googlesource.com/pub/scm/linux/kernel/git/stable/linux-stable.git
git fetch linux-stable
```

## 3. Decide if you want to merge or cherry-pick the commits in

Next, you will need to choose if you want to merge the commits or cherry-pick. Here's the pros and cons of each and when you may want to do them.

**NOTE:** If your kernel source is in the form of a tarball, you will most likely need to cherry-pick, otherwise you will get thousands of file conflicts because git is populating the history based purely on upstream, not what the OEM or CAF has changed. Just skip to step 4.

### Cherry-picking

Pros:
* Easier to resolve conflicts as you know exactly what conflict is causing an issue.
* Easier to rebase as each commit is on its own.
* Easier to bisect if running into issues

Cons:
* It takes longer as each commit has to be individually picked.
* Little more difficult to tell if commit is from upstream on first glance

### Merge

Pros:
* It's faster as you do not have to wait for all of the clean patches to merge.
* It's easier to see when a commit is from upstream as you will not be the committer, the upstream maintainer will be.

Cons:
* Resolving conflicts can be a bit more difficult as you will need to look up which commit is causing the conflict using `git log`/`git blame`, it will not directly tell you.
* Rebasing is difficult as you cannot rebase a merge, it will offer to cherry-pick all of the commit individually. However, you should not be rebasing often, instead using `git revert` and `git merge` where possible.

I would recommend doing a cherry-pick to figure out any problem conflicts then do a merge then revert the problem commits afterwards so updating is easier (as merging is quicker after being up to date).


## 4. Add the commits into your source, one version at a time

The most important part of this process is the one version at a time part. There MAY be a problem patch in your upstream series, which could cause a problem with booting or break something like sound or charging (explained in the tips and tricks section). Doing incremental version changes is important for this reason, it's easier to find an issue in 50 commits than upwards of 2000 commits for some versions. I would only recommend doing a full merge once you know all of the problem commits and conflict resolutions.

### Cherry-picking

Format:
```bash
git cherry-pick <previous_tag>..<next_tag>
```

Example:
```bash
git cherry-pick v3.10.73..v3.10.74
```

### Merge

Format:
```bash
git merge <next_tag>
```

Example:
```bash
git merge v3.10.74
```

I recommend keeping track of the conflicts in merge commits by removing the `#` markers.
