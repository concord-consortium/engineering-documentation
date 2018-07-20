# Git Cheatsheet

> Author:   D.Love  
> Original: 13-Oct-2011  
> Revised:  20-Jul-2018  

Suppose you already know, kind of, how git works. You're conceptually familiar with the git flavor of repos, staging, committing, branching, merging, pulling and pushing. I am, but even so, I find it helpful to have my most frequently used commands handy, particularly if I'm away from daily programming for more than a couple of weeks.

There are many sources for this information, just google for "git commands" and you'll find several write-ups, usually with far greater detail. But that's more than what I want; what I really want is a little table I can cut out and tape to my monitor.

## Basic Commands

| Task                       | Command                      |
|:---------------------------|:-----------------------------|
| Where am I?                | `git status` or `git branch` |
| Sync from repo             | `git pull`[^1]               |
| Create new branch & switch | `git checkout -b <b-name>`   |
| Switch to different branch | `git checkout <b-name>`      |
| Abandon changes            | `git checkout -- <file>`     |   
| Move/Delete[^2] | `git mv <from> <to>` or `git rm <file>` |
| Stage all files            | `git add .`                  |
| Commit staged              | `git commit -m <comment>`    |
| Save in repo               | `git push origin <b-name>`   | 
 
[^1]: Often, I do a `git pull` before I get down to work, so I'm working with a freshly updated set of files with all the latest and greatest changes. Later, I will checkout master, pull again, and merge master onto my feature branch, and push. I try to **never** work without managing my work within a branch. See [Create a new branch with git and manage branches](https://github.com/Kunena/Kunena-Forum/wiki/Create-a-new-branch-with-git-and-manage-branches) for a short writeup on how to use branches. For a more complex, but extremely useful branching model, see Atlassian's [Gitflow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) documentation.

[^2]: For git to track file movements and deletions, there are these two commands, `git mv` and `git rm`, which not only manipulate the files, they make sure git has a record of the changes. Forgetting to use these and just using the native command-line utilities `mv` and `rm` is a mistake I usually make, at least once a month.

## Less Frequently Used Commands

| Task            | Command                                  |
|:----------------|:-----------------------------------------|
| Git setup[^3]   | `git config --global user.name <u-name>` |
| New repo[^4]    | `cd <working-dir>`, `git init`           |
| Complete fetch  | `git clone <repo-URL>`[^5]               |

[^3]: All the global (and local, for that matter) settings are too much for this quick cheatsheet. Many web-resources are available, if needed.

[^4]: I almost never do this, anymore. I usually go to GitHub, create a new repo there, then clone it to my local working directory.

[^5]: Here is an example repo-URL: `https://github.com/concord-consortium/engineering-documentation`
