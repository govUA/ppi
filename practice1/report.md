### Git Directory
* .git - all VCS info for repo
* HEAD - currently checked-out commit/branch
* description - repo desc.
* info/exclude - like .gitignore but local
* config - config (remote url, account data)
* hooks - pre-commit, pre-push, etc.
* refs/heads - hashes of last commit on each branch
* refs/tags - releases/specific commits
* objects - commits, trees, blobs and tags
* objects/info - metadata on objects
* objects/pack - packed objects to save space

### Git Add
* New blob
* folder name - first 2 chars of its hash
* file name - remaining chars

### Git Restore
* objects/ do not change
* As per www.git-tower.com "With the --staged option, however, the file will only be removed from the Staging Area - but its actual modifications will remain untouched"

### Tracking HEAD and Branch Refs
* HEAD - pointer to current branch
* refs/heads/main - latest commit hash
* The hash does match the commit

### Another Commit
* in refs/heads/main 1st commit hash changes is replaced with 2nd commit hash

### Manually Editing
* git log shows only the 1st commit
* 2nd commit unreachable from any branch or tag, but can be found in objects

### Revert to 2nd Commit
* Commit history successfully restored

### Branches and Commits
* Checked-out branch is updated (master)

### Manually Switching Branches
* HEAD points to new specified branch (test_2_branhc)
* logs - every update to HEAD and branch refs

### Cherry-Picking
* Cherry-picked hashes do not match original commits
* "It creates new commit, with a different hash, and has no reference to original" (https://medium.com/@vitali-s/danger-of-cherry-pick-42a56141577f)

### Python vs git cat-file
* Python - raw header + body
* git cat-file - human-readable parsed output

### Analyse objects
* 2 commits, 2 blobs, 2 trees
* Each commit points to a tree, trees point to blobs
* 2nd commit is a child to the 1st commit

### The "^"
* [commit]^ - first parent of the commit
* [commit]^^ - parent's parent
* [commit]^2 - second parent on merge commit (https://stackoverflow.com/questions/2221658/what-is-the-difference-between-head-and-head-in-git)

### Git Remote Add
* git remote add - link local repo to remote one
* url here is local path to test2
* commits from test1 repo pushed onto test2 repo
* new branch in test2 is named myNewBranchInTets2

### Patches
* Commit hashes differ after applying patches
* "git commit hashes are generated from the commit and its parent commits" (https://www.reddit.com/r/git/comments/3lrwt1/comment/cv8sliz/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)