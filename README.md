# Note: These notes are not everything you need to know about git but should suffice for day to day use of git.
 * Please take the time to read [this awesome book](https://git-scm.com/book/en/v2) to learn about git in further detail. 
 * Your life as a programmer will be a little bit more enjoyable and free if you
understand and use git to it's fullest extent.

# Git's goals when it was created (still is):
  * Speed
  * Simple design
  * `Strong support for non-linear development (thousands of parallel branches)`
  * `Fully distributed`
  * Able to handle large projects like the Linux kernel efficiently 
    (speed and data size)

# Getting a git repository
  * Use `SSH` or the `Github CLI` to clone repos
  * Using `HTTPS` is quite cumbersome due to the constant need for loging in,
    note (this is just my opinion)
  * If you use 2FA (which you should be), `SSH` is easier
  * Setting up `SSH` is not that difficult, follow [this guide by Github](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
# Creating your first branch
  * `git checkout -b <branch name>`, where b is branch (my guess :D)
  * Note this is a shorthand for:
  ```
  git branch <branch name>
  git checkout <branch name>
  ```
# Staging and Commiting 
  * `git add <file name>` to stage a change
  * `git add .` to stage all files
  * `git commit ` to commit changes
  * `git commit -m "<commit message>"` to commit with message
  * `git commit -a -m "<commit message>"` to stage & commit with commit message

# Undoing Things
  * **NOTE**: You cannot undo some of these undo's so please be careful!
  * If you commit too early and forget to remove something like a comment or
    something trivial, you can use `git commit --amend`. This command takes you
    to the staging area. **NOTE**: Only use this for trivial changes as this
    (trivial change) won't show up in your commit history
  * *Unstaging* a staged file `git restore --staged <file name>`. 
  * Restoring/Unmodyfing a file: `git checkout -- <file>` | `git restore <file>`
    **NOTE**: the changes you amde will be completely lost.
# Structuring commit messages
  * `<Ticket Number>: The change that was made`; keep it brief and in present
    tense of what it does. ex: `PJ22:Change version number`
  * If commit needs more explanation leave a line after the title (which should
    be short and precise), and then add a list of changes and why you made them.
    The why is more important than the what, as developers we can see what is
    happening in the code, the why not so much.

# Remote branches
  * `git ls-remote <remote>` | `git remote show <remote>` to list remote
    branches
  * `origin` is not special, it's just widely used default name for remote. Just
    like main or master
    * `git fetch <remote>` to pull all meta-data from remote and does not do any
      file transferring, it's more to check if there are changes available
    * `git pull <remote>` copies the changes from the remote repository
    * `git push <remote> <branch>` to push changes to the remote repository
    * `git branch -u <remote/branch>` to track remote branch, let's you push
      using `git push` and also warns against any changes you might need to
      `pull` before pushing your changes
    * You can also use `git checkout --track <remote/branch>` for the same
      results as above before switching. Only needs to be done once.
  
# Deleting a branch
  * `git branch -d <branch name>`; Once the branch has been merged to develop or
    main, it no longer serves any purpose. You can delete it. Currently if you
    notice when a `pr` gets merged the branch get's automatically deleted for
    the same reason.

# Merge Conflicts 
## Mindset: 
  * Merge conflicts are good, it's git letting you know that I'm going to let 
    you decide which lines to keep cause I'm not sure

## You can `--abort` a change
  * Yes you can stop the merge, if the conflict is large and you need to include
    a team member into the plan use `git merge --abort` or `git rebase --abort`.
    If your current merge strategy is rebase, if you don't know what rebase does
    use the first one and read about rebase :D
    
## Ways to avoid Merge conflicts:
  * Push and pull changes as often as possible
  * Avoid the solo programmer mindset by keeping in mind that other people 
    are working on the same code
    
## Understanding the symbols of fear
  * `<<<<<<<` : Denotes the cause of the conflict (HEAD of current branch)
  * `=======` : Is just a seperator
  * `>>>>>>>` : Denotes the end of the conflict (Branch you are pulling into
    current branch)

## Ways to resolve Merge Conflicts:
  * Accept local version `git checkout --ours <file name>` 
  * Accept remote version `git checkout --theirs <file name>` 
  
  ### Using `git mergetool` 
    1. L(ocal)
    2. Base (Middle)
    3. R(emote)
    4. Merged

    * Then use:
      * :diffg LOCAL updates the to the LOCAL version.
      * :diffg BASE updates to the BASE version.
      * :diffg REMOTE updates to the REMOTE version.
    
    * If using mergetool, remember to `commit` and `clean`
    * To clean up, use `git clean -f`

## Stashing Changes
  * `git stash` to stash uncommited changes
  * `git stash apply` | `git stash pop` to get the changes back
  * Keep in mind `apply` keeps the stash whereas `pop` removes the stash from
    the stack
  * `git stash list` for multiple stashes
  * `git stash apply stash@{<stash number>} `| `pop` to get a particular stash
  * `git stash drop` to remove stash without using it

## Git Worktrees:
  * If you find yourself switching branches quite often, look into [git
    worktree](https://git-scm.com/docs/git-worktree)
    
## Useful Extensions:
  * VSCode
   * [Github PR's and Issues](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)

 * Vim
   * [Vim Fugitive](https://github.com/tpope/vim-fugitive), so awesome, it should be illegal ????
   * [Git Worktree](https://github.com/ThePrimeagen/git-worktree.nvim)
   * [Vim Gitgutter](https://github.com/airblade/vim-gitgutter)
  

