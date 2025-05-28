## Git

### Observation 1: Record the commit hashes in your report based on git log command output.

```
~$ git log
commit 9626f8767f6b7bd1ae13023a310cc3c2b272c9ea (HEAD -> main)
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed May 28 07:32:14 2025 +0000

    init 3 files

commit 96b0c530d5221f3f3e2d41359e428e38dd58b716
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed May 28 07:31:08 2025 +0000

    initial empty commit
```

### Observation 2: Extract hashes of tree and parent commit and note them. Use `git cat-file -p <hash of tree>` and note the output. You should find a tree object in the output - note its hash and run `git cat-file -p` on it. Note the result. Check parent hash with `git cat-file -t` to ensure that its type is commit. Use `git cat-file -p` to find the hash of the corresponding tree, use cat-file on that tree hash. Note the results.

```
~$ git cat-file -p HEAD
tree 104f495dd25da7d96405da66b0b4d0a642d22a23
parent 96b0c530d5221f3f3e2d41359e428e38dd58b716
```

```
~$ git cat-file -p 104f495dd25da7d96405da66b0b4d0a642d22a23
100644 blob 03393f2f612ef64f154e9d5847becf6988cc8440    1.txt
100644 blob 56b7a55cd1de65ffdaeacb64b89b7a8e42a5438c    2.txt
040000 tree 331c53678d60db65ec90ad6518f31bc3dc689cf3    dir
```

```
~$ git cat-file -p 331c53678d60db65ec90ad6518f31bc3dc689cf3
100644 blob 6c52c6b96661a1683918387f87f58d80ab6aef83    3.txt
```

```
~$ git cat-file -t 96b0c530d5221f3f3e2d41359e428e38dd58b716
commit
```

```
~$ git cat-file -p 96b0c530d5221f3f3e2d41359e428e38dd58b716
tree 4b825dc642cb6eb9a060e54bf8d69288fbee4904
author govUA <kotlyarihor@gmail.com> 1748417468 +0000
committer govUA <kotlyarihor@gmail.com> 1748417468 +0000

initial empty commit
```

```
~$ git cat-file -p 4b825dc642cb6eb9a060e54bf8d69288fbee4904

```

### Observation 3: Use `git log` command to find the hashes of all new commits. Note the results. Use the hash of Update 1.txt commit and note the result of both `git show <hash>` to view the delta. Note the results. Use `git cat-file -p` to find the tree hash associated with it and use `git cat-file -p` on that tree to view the result. Note the results.

```
~$ git log
commit ce0ae3a8b7e257e5c1a9c0ce5a387b76b722f715 (HEAD -> main)
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed May 28 07:48:27 2025 +0000

    Update 3.txt

commit 2cf04168ce7154388d279e27efc40902a14fb31b
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed May 28 07:48:15 2025 +0000

    Update 2.txt

commit 1c6a4dbeb110253f8b70b27dff09c22ba76994b6
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed May 28 07:48:04 2025 +0000

    Update 1.txt
```

```
~$ git show 1c6a4dbeb110253f8b70b27dff09c22ba76994b6
commit 1c6a4dbeb110253f8b70b27dff09c22ba76994b6
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed May 28 07:48:04 2025 +0000

    Update 1.txt

diff --git a/1.txt b/1.txt
index 03393f2..6f467db 100644
--- a/1.txt
+++ b/1.txt
@@ -1 +1,2 @@
 File 1 line 1
+File 1 Line 2
```

```
~$ git cat-file -p 1c6a4dbeb110253f8b70b27dff09c22ba76994b6
tree 636558dcce710c831848f93e4f61598809e5d305
parent 9626f8767f6b7bd1ae13023a310cc3c2b272c9ea
author govUA <kotlyarihor@gmail.com> 1748418484 +0000
committer govUA <kotlyarihor@gmail.com> 1748418484 +0000

Update 1.txt
```

```
~$ git cat-file -p 636558dcce710c831848f93e4f61598809e5d305
100644 blob 6f467dbd73ad0c24b3af421da0ee7a7724de2571    1.txt
100644 blob 56b7a55cd1de65ffdaeacb64b89b7a8e42a5438c    2.txt
040000 tree 331c53678d60db65ec90ad6518f31bc3dc689cf3    dir
```

### Observation 4: Use `git log` to check the history and branch mapping. What is the active branch at the moment? Add branches `new_branch_2` and `new_branch_3` based on `Update 2.txt` and `Update 3.txt` commits. Note `git log` output. Check the tree objects of all 3 branches e.g. `git cat-file -p new_branch_1` and so on. Note the results.

```
~$ git log
commit ce0ae3a8b7e257e5c1a9c0ce5a387b76b722f715 (HEAD -> main, new_branch_3)
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed May 28 07:48:27 2025 +0000

    Update 3.txt

commit 2cf04168ce7154388d279e27efc40902a14fb31b (new_branch_2)
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed May 28 07:48:15 2025 +0000

    Update 2.txt

commit 1c6a4dbeb110253f8b70b27dff09c22ba76994b6 (new_branch_1)
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed May 28 07:48:04 2025 +0000

    Update 1.txt
```

main is the active branch at the moment.

```
~$ git cat-file -p new_branch_1
tree 636558dcce710c831848f93e4f61598809e5d305
parent 9626f8767f6b7bd1ae13023a310cc3c2b272c9ea
author govUA <kotlyarihor@gmail.com> 1748418484 +0000
committer govUA <kotlyarihor@gmail.com> 1748418484 +0000

Update 1.txt
~$ git cat-file -p new_branch_2
tree 28fb522a073d6550c26f86a93de2a675db18abc6
parent 1c6a4dbeb110253f8b70b27dff09c22ba76994b6
author govUA <kotlyarihor@gmail.com> 1748418495 +0000
committer govUA <kotlyarihor@gmail.com> 1748418495 +0000

Update 2.txt
~$ git cat-file -p new_branch_3
tree 037e0fc66bd150e9af4d80f7240cca738a71ac68
parent 2cf04168ce7154388d279e27efc40902a14fb31b
author govUA <kotlyarihor@gmail.com> 1748418507 +0000
committer govUA <kotlyarihor@gmail.com> 1748418507 +0000

Update 3.txt
```

```
~$ git checkout new_branch_3
Switched to branch 'new_branch_3'
ubuntu@ppi:~/week2/newRepo$ cat 2.txt
File 2 line 1
File 2 Line 2
```

```
~$ git checkout 1c6a4dbeb110253f8b70b27dff09c22ba76994b6 -- 2.txt
~$ cat 2.txt
File 2 line 1
```

```
~$ git diff
~$ git diff --staged
diff --git a/2.txt b/2.txt
index 70cc821..56b7a55 100644
--- a/2.txt
+++ b/2.txt
@@ -1,2 +1 @@
 File 2 line 1
-File 2 Line 2
```

### Observation 5: use git graph command on different branches you created early and note the result. Add another global config option to ensure that default branch for new repositories will be `main` (Check init.defaultBranch field of config).

```
~$ git graph new_branch_1
* 1c6a4dbeb110253f8b70b27dff09c22ba76994b6 Update 1.txt
* 9626f8767f6b7bd1ae13023a310cc3c2b272c9ea init 3 files
* 96b0c530d5221f3f3e2d41359e428e38dd58b716 initial empty commit
~$ git graph new_branch_2
* 2cf04168ce7154388d279e27efc40902a14fb31b Update 2.txt
* 1c6a4dbeb110253f8b70b27dff09c22ba76994b6 Update 1.txt
* 9626f8767f6b7bd1ae13023a310cc3c2b272c9ea init 3 files
* 96b0c530d5221f3f3e2d41359e428e38dd58b716 initial empty commit
~$ git graph new_branch_3
* ce0ae3a8b7e257e5c1a9c0ce5a387b76b722f715 Update 3.txt
* 2cf04168ce7154388d279e27efc40902a14fb31b Update 2.txt
* 1c6a4dbeb110253f8b70b27dff09c22ba76994b6 Update 1.txt
* 9626f8767f6b7bd1ae13023a310cc3c2b272c9ea init 3 files
* 96b0c530d5221f3f3e2d41359e428e38dd58b716 initial empty commit
```

```
~.$ git config --global init.defaultBranch main
```

### Observation 6: you should make Update 2.txt to be the oldest commit from those, Update 3.txt after it and Update 1.txt to be on top of them with new commit message "New Update 1.txt". After rebase use `git graph` alias you introduced before to get the history. Compare with the log before the rebase.

```
~$ git rebase -i HEAD~3
[detached HEAD 69dce13] New Update 1.txt
 Date: Wed May 28 07:48:04 2025 +0000
 1 file changed, 1 insertion(+)
Successfully rebased and updated refs/heads/new_branch_3.
~$ git graph
* 69dce1392e945884af9962dd95c7443c88eb2feb New Update 1.txt
* b76db417da7f1064e905a266f7acc75887dd6ba5 Update 3.txt
* 4b05b5a7485bb9faff851c68708701b3a0d61b15 Update 2.txt
* 9626f8767f6b7bd1ae13023a310cc3c2b272c9ea init 3 files
* 96b0c530d5221f3f3e2d41359e428e38dd58b716 initial empty commit
```

Hashes changed due to rebase.

### Observation 7: Check `git log` to get hash of new commit. Use `git show` for `HEAD` and `HEAD^`. Note the result. Use interactive rebase to append changes from the latest commit into the previous one. Use `git show HEAD` to view the result. Note the outputs and write you concluusion on the behavior.

```
~$ git log
commit 807043cb18eaf7e02450376a8dd68deaf6ad1a36 (HEAD -> new_branch_3)
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed May 28 16:10:21 2025 +0000

    One more Update for 1.txt

commit 69dce1392e945884af9962dd95c7443c88eb2feb
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed May 28 07:48:04 2025 +0000

    New Update 1.txt

commit b76db417da7f1064e905a266f7acc75887dd6ba5
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed May 28 07:48:27 2025 +0000

    Update 3.txt

commit 4b05b5a7485bb9faff851c68708701b3a0d61b15
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed May 28 07:48:15 2025 +0000

    Update 2.txt
```

```
~$ git show HEAD
commit 807043cb18eaf7e02450376a8dd68deaf6ad1a36 (HEAD -> new_branch_3)
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed May 28 16:10:21 2025 +0000

    One more Update for 1.txt

diff --git a/1.txt b/1.txt
index 6f467db..0dbb064 100644
--- a/1.txt
+++ b/1.txt
@@ -1,2 +1,3 @@
 File 1 line 1
 File 1 Line 2
+File 1 Line 3
```

```
~$ git show HEAD^
commit 69dce1392e945884af9962dd95c7443c88eb2feb
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed May 28 07:48:04 2025 +0000

    New Update 1.txt

diff --git a/1.txt b/1.txt
index 03393f2..6f467db 100644
--- a/1.txt
+++ b/1.txt
@@ -1 +1,2 @@
 File 1 line 1
+File 1 Line 2
```

### Observation 8: Check `git log` to get hash of new commit. Use `git show` for `HEAD` and `HEAD^`. Note the result. Use interactive rebase to append changes from the latest commit into the previous one. Use `git show HEAD` to view the result. Note the outputs and write you concluusion on the behavior.

```
~$ git show HEAD
commit 5bfa536c0a82cb6d1dd9d7efd6ebc3afd58da5c7 (HEAD -> new_branch_3)
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed May 28 07:48:04 2025 +0000

    New Update 1.txt

    One more Update for 1.txt

diff --git a/1.txt b/1.txt
index 03393f2..0dbb064 100644
--- a/1.txt
+++ b/1.txt
@@ -1 +1,3 @@
 File 1 line 1
+File 1 Line 2
+File 1 Line 3
```

Changes from both commits combined into one, literally what squash is for. Hash different from both initial commits.

### Observation 9: Note the differences in your staging area and working tree.

```
~$ git reset --soft HEAD^
~$ git status
On branch new_branch_3
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   1.txt

~$ git diff --staged
diff --git a/1.txt b/1.txt
index 03393f2..0dbb064 100644
--- a/1.txt
+++ b/1.txt
@@ -1 +1,3 @@
 File 1 line 1
+File 1 Line 2
+File 1 Line 3
~$ git reset --hard HEAD
HEAD is now at b76db41 Update 3.txt
~$ git status
On branch new_branch_3
nothing to commit, working tree clean
~$ git diff
```

--soft keeps changes but removes the commit itself
--hard removes both
this is reflected in staging area:
for --soft there are changes to be commited
for --hard the commit is completely removed and there's nothing to commit

## Website for a fast-food franchise

| Priority | User Story | Requirements |
| --- | --- | --- |
| P1 | As a customer I want to have a simple infocard about the food item I'm ordering, so that I know what I'm ordering, what it looks like and how much am I paying. | Infocard that shows item's:<ul><li>name</li><li>image</li><li>calories</li><li>price</li><li>ingredients</li></ul> |
