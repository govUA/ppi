## Git

### Observation 1: content of the files and git log.
```
~$ cat 1.txt
Line 1
Line 2
Line 3
Line 4
Line 5
~$ cat 2.txt
Line 1
Line 2
Line 3
Line 4
Line 5
~$ cat 3.txt
Line 1
Line 2
Line 3
Line 4
Line 5
```
```
~$ git log
commit d6fc86f03eafd125e69e90bfc86d7816521fed72 (HEAD -> main)
Author: govUA <kotlyarihor@gmail.com>
Date:   Fri May 30 19:30:19 2025 +0000

    Initial version of 3 files.
```

### Observation 2: Use git log to demonstrate and describe the change.
```
~$ git branch branchA d6fc86f
~$ git branch branchB d6fc86f
~$ git log
commit d6fc86f03eafd125e69e90bfc86d7816521fed72 (HEAD -> main, branchB, branchA)
Author: govUA <kotlyarihor@gmail.com>
Date:   Fri May 30 19:30:19 2025 +0000

    Initial version of 3 files.
```

All branches point to the same commit. No divergence, all branches identical. Hence, HEAD is still on main.

### Observation 3: Use `git log` and `git show` to provide a clear picture what changes where introduced.
```
~$ git checkout branchB
Switched to branch 'branchB'
~$ echo "Updated line in 2.txt" >> 2.txt
~$ git add 2.txt
~$ git commit -m "Update 2.txt"
[branchB 87e2a3a] Update 2.txt
 1 file changed, 1 insertion(+)
~$ git log
commit 87e2a3a9fc6ef5735f55697298fdbc05906cb84d (HEAD -> branchB)
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed Jun 4 19:42:03 2025 +0000

    Update 2.txt

commit d6fc86f03eafd125e69e90bfc86d7816521fed72 (main, branchA)
Author: govUA <kotlyarihor@gmail.com>
Date:   Fri May 30 19:30:19 2025 +0000

    Initial version of 3 files.
~$ git show
commit 87e2a3a9fc6ef5735f55697298fdbc05906cb84d (HEAD -> branchB)
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed Jun 4 19:42:03 2025 +0000

    Update 2.txt

diff --git a/2.txt b/2.txt
index 572d5d9..23db6ad 100644
--- a/2.txt
+++ b/2.txt
@@ -3,3 +3,4 @@ Line 2
 Line 3
 Line 4
 Line 5
+Updated line in 2.txt
```

### Observation 4: Provide `git show` of the recent commit and `git log`. Write down the hash of the HEAD for `branchB`.
```
~$ echo "New line in 3.txt" >> 3.txt
~$ git add 3.txt
~$ git commit -m "Update 3.txt"
[branchB 30048c0] Update 3.txt
 1 file changed, 1 insertion(+)
~$ git show
commit 30048c07277b025c3bda3841c54ce69c0b16032c (HEAD -> branchB)
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed Jun 4 19:46:38 2025 +0000

    Update 3.txt

diff --git a/3.txt b/3.txt
index 572d5d9..afbc1a8 100644
--- a/3.txt
+++ b/3.txt
@@ -3,3 +3,4 @@ Line 2
 Line 3
 Line 4
 Line 5
+New line in 3.txt
~$ git log
commit 30048c07277b025c3bda3841c54ce69c0b16032c (HEAD -> branchB)
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed Jun 4 19:46:38 2025 +0000

    Update 3.txt

commit 87e2a3a9fc6ef5735f55697298fdbc05906cb84d
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed Jun 4 19:42:03 2025 +0000

    Update 2.txt

commit d6fc86f03eafd125e69e90bfc86d7816521fed72 (main, branchA)
Author: govUA <kotlyarihor@gmail.com>
Date:   Fri May 30 19:30:19 2025 +0000

    Initial version of 3 files.
```

HEAD hash: 30048c07277b025c3bda3841c54ce69c0b16032c

### Observation 5: Use `git show` and `git log --oneline --all --graph` to demonstrate the changes in the repository. Write down the hash of the HEAD for `branchA`.
```
ubuntu@ppi:~/week3_repo1$ git checkout branchA
Switched to branch 'branchA'
ubuntu@ppi:~/week3_repo1$ echo "New line in 1.txt" >> 1.txt
ubuntu@ppi:~/week3_repo1$ git add 1.txt
ubuntu@ppi:~/week3_repo1$ git commit -m "Update 1.txt"
[branchA 695d97e] Update 1.txt
 1 file changed, 1 insertion(+)
ubuntu@ppi:~/week3_repo1$ git show
commit 695d97ea802001e98dbe78f33740e468e68d4716 (HEAD -> branchA)
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed Jun 4 19:49:56 2025 +0000

    Update 1.txt

diff --git a/1.txt b/1.txt
index 572d5d9..4f6436a 100644
--- a/1.txt
+++ b/1.txt
@@ -3,3 +3,4 @@ Line 2
 Line 3
 Line 4
 Line 5
+New line in 1.txt
ubuntu@ppi:~/week3_repo1$ git log --oneline --all --graph
* 695d97e (HEAD -> branchA) Update 1.txt
| * 30048c0 (branchB) Update 3.txt
| * 87e2a3a Update 2.txt
|/
* d6fc86f (main) Initial version of 3 files.
```

HEAD hash: 695d97ea802001e98dbe78f33740e468e68d4716

### Observation 6: Use cat-file command to get a list of blobs associated with the trees. Provide a detailed analysis of the differences between each pair of the trees for that 3 commits e.g. branchA&branchB, branchA&main, branchB&main.
```
ubuntu@ppi:~/week3_repo1$ git rev-parse main
d6fc86f03eafd125e69e90bfc86d7816521fed72
ubuntu@ppi:~/week3_repo1$ git cat-file -p d6fc86f03eafd125e69e90bfc86d7816521fed72
tree 4f76c0774ac72a4a246e02af60a695d493d69e0a
author govUA <kotlyarihor@gmail.com> 1748633419 +0000
committer govUA <kotlyarihor@gmail.com> 1748633419 +0000

Initial version of 3 files.
ubuntu@ppi:~/week3_repo1$ git cat-file -p 695d97ea802001e98dbe78f33740e468e68d4716
tree f44ac0f033ae5fdd76195b819d12a2cdc25b6861
parent d6fc86f03eafd125e69e90bfc86d7816521fed72
author govUA <kotlyarihor@gmail.com> 1749066596 +0000
committer govUA <kotlyarihor@gmail.com> 1749066596 +0000

Update 1.txt
ubuntu@ppi:~/week3_repo1$ git cat-file -p 30048c07277b025c3bda3841c54ce69c0b16032c
tree f629c27e095c73cc690caefb3de3a22f2f1deca7
parent 87e2a3a9fc6ef5735f55697298fdbc05906cb84d
author govUA <kotlyarihor@gmail.com> 1749066398 +0000
committer govUA <kotlyarihor@gmail.com> 1749066398 +0000

Update 3.txt
ubuntu@ppi:~/week3_repo1$ git cat-file -p 4f76c0774ac72a4a246e02af60a695d493d69e0a
100644 blob 572d5d94839464f28ef959932515ee6624dbfe01    1.txt
100644 blob 572d5d94839464f28ef959932515ee6624dbfe01    2.txt
100644 blob 572d5d94839464f28ef959932515ee6624dbfe01    3.txt
ubuntu@ppi:~/week3_repo1$ git cat-file -p f44ac0f033ae5fdd76195b819d12a2cdc25b6861
100644 blob 4f6436a267ef21c74007fc003baddaf575598ac4    1.txt
100644 blob 572d5d94839464f28ef959932515ee6624dbfe01    2.txt
100644 blob 572d5d94839464f28ef959932515ee6624dbfe01    3.txt
ubuntu@ppi:~/week3_repo1$ git cat-file -p f629c27e095c73cc690caefb3de3a22f2f1deca7
100644 blob 572d5d94839464f28ef959932515ee6624dbfe01    1.txt
100644 blob 23db6adfe8467dd2c4cdfd7729d88e375df57348    2.txt
100644 blob afbc1a86b3e9dffb0e5774825350246a137de5a1    3.txt
```

1.txt hash in branchA different to one in main.
2.txt and 3.txt hashes in branchB different to ones in main.
Every hash in branchA is different to branchB, since 2.txt and 3.txt in branchA are unchanged from main, and 1.txt is unchanged in branchB, while other files in their respective branches are changed.

### Observation 7: describe which commit is a base and why.
```
ubuntu@ppi:~/week3_repo1$ git merge-base branchA branchB
d6fc86f03eafd125e69e90bfc86d7816521fed72
```

d6fc86f03eafd125e69e90bfc86d7816521fed72 is the base commit as it is the common parent for two branches.

### Observation 8: Provide the explanation of the result e.g. do we add a new commit, if so provide its cat-file output, check the parent field and tree; provide the list of blobs inside the tree. Compare with the trees we considered before for `main`, `branchA` and `branchB`. Explain the reason of the observed behavior and tree state.
```
ubuntu@ppi:~/week3_repo1$ git checkout branchA
Already on 'branchA'
ubuntu@ppi:~/week3_repo1$ git merge branchB -m "Cool merge B=>A"
Merge made by the 'ort' strategy.
 2.txt | 1 +
 3.txt | 1 +
 2 files changed, 2 insertions(+)
ubuntu@ppi:~/week3_repo1$ git show
commit 9b063720261ee71c6006753d0799757c1cf21a92 (HEAD -> branchA)
Merge: 695d97e 30048c0
Author: govUA <kotlyarihor@gmail.com>
Date:   Wed Jun 4 20:09:09 2025 +0000

    Cool merge B=>A

ubuntu@ppi:~/week3_repo1$ git cat-file -p HEAD
tree 4699d3621284916caaff4fc34ae028e39ad6ff29
parent 695d97ea802001e98dbe78f33740e468e68d4716
parent 30048c07277b025c3bda3841c54ce69c0b16032c
author govUA <kotlyarihor@gmail.com> 1749067749 +0000
committer govUA <kotlyarihor@gmail.com> 1749067749 +0000

Cool merge B=>A
```

New merge commit with two parents, all merged file versions.

### Observation 9: provide resolved commit hashes and describe how do they map to `git log --oneline --graph` output for the current HEAD. Check `git merge-base` for `branchA` and `branchB`
```
ubuntu@ppi:~/week3_repo1$ git cat-file -p $(git rev-parse HEAD^{tree})
100644 blob 4f6436a267ef21c74007fc003baddaf575598ac4    1.txt
100644 blob 23db6adfe8467dd2c4cdfd7729d88e375df57348    2.txt
100644 blob afbc1a86b3e9dffb0e5774825350246a137de5a1    3.txt
ubuntu@ppi:~/week3_repo1$ git rev-parse HEAD^
695d97ea802001e98dbe78f33740e468e68d4716
ubuntu@ppi:~/week3_repo1$ git rev-parse HEAD^1
695d97ea802001e98dbe78f33740e468e68d4716
ubuntu@ppi:~/week3_repo1$ git rev-parse HEAD^2
30048c07277b025c3bda3841c54ce69c0b16032c
ubuntu@ppi:~/week3_repo1$ git rev-parse HEAD^2^
87e2a3a9fc6ef5735f55697298fdbc05906cb84d
ubuntu@ppi:~/week3_repo1$ git log --oneline --graph
*   9b06372 (HEAD -> branchA) Cool merge B=>A
|\
| * 30048c0 (branchB) Update 3.txt
| * 87e2a3a Update 2.txt
* | 695d97e Update 1.txt
|/
* d6fc86f (main) Initial version of 3 files.
```

## Git 2

### Observation 10: content of the files and git log.
```
ubuntu@ppi:~/week3_repo2$ git commit --allow-empty -m "Initial empty commit"
[main (root-commit) a8d806f] Initial empty commit
ubuntu@ppi:~/week3_repo2$ for file in a.txt b.txt c.txt; do
>   for i in {1..10}; do echo "$file line $i" >> $file; done
> done
ubuntu@ppi:~/week3_repo2$
ubuntu@ppi:~/week3_repo2$ git add .
ubuntu@ppi:~/week3_repo2$ git commit -m "Initial version of a.txt, b.txt, and c.txt"
[main 497ad1d] Initial version of a.txt, b.txt, and c.txt
 3 files changed, 30 insertions(+)
 create mode 100644 a.txt
 create mode 100644 b.txt
 create mode 100644 c.txt
ubuntu@ppi:~/week3_repo2$ git log --oneline
497ad1d (HEAD -> main) Initial version of a.txt, b.txt, and c.txt
a8d806f Initial empty commit
```

### Observation 11: analyse `git log` output.
```
ubuntu@ppi:~/week3_repo2$ git branch branch1
ubuntu@ppi:~/week3_repo2$ git branch branch2
ubuntu@ppi:~/week3_repo2$ git checkout branch1
Switched to branch 'branch1'
ubuntu@ppi:~/week3_repo2$ git log --oneline --graph
* 497ad1d (HEAD -> branch1, main, branch2) Initial version of a.txt, b.txt, and c.txt
* a8d806f Initial empty commit
```

### Observation 12: use `git diff --word-diff` command to demonstrate the delta you introduce. Commit the changes with Patch1 commit message.
```
ubuntu@ppi:~/week3_repo2$ sed -i '2s/line/LINE/' a.txt
ubuntu@ppi:~/week3_repo2$ sed -i '4s/line/LINE/' b.txt
ubuntu@ppi:~/week3_repo2$ git diff --word-diff
diff --git a/a.txt b/a.txt
index d5c7f08..e224fd3 100644
--- a/a.txt
+++ b/a.txt
@@ -1,5 +1,5 @@
a.txt line 1
a.txt [-line-]{+LINE+} 2
a.txt line 3
a.txt line 4
a.txt line 5
diff --git a/b.txt b/b.txt
index 2fa71af..aeaaaf4 100644
--- a/b.txt
+++ b/b.txt
@@ -1,7 +1,7 @@
b.txt line 1
b.txt line 2
b.txt line 3
b.txt [-line-]{+LINE+} 4
b.txt line 5
b.txt line 6
b.txt line 7
ubuntu@ppi:~/week3_repo2$ git add .
ubuntu@ppi:~/week3_repo2$ git commit -m "Patch1"
[branch1 abb8fa2] Patch1
 2 files changed, 2 insertions(+), 2 deletions(-)
```

### Observation 13: use `git diff --word-diff` command to demonstrate the delta you introduce. Commit the changes with Patch2 commit message.
```
ubuntu@ppi:~/week3_repo2$ git checkout branch2
Switched to branch 'branch2'
ubuntu@ppi:~/week3_repo2$ sed -i '10s/line/LINE/' a.txt
ubuntu@ppi:~/week3_repo2$ sed -i '3s/line/LINE/' b.txt
ubuntu@ppi:~/week3_repo2$ sed -i '5s/line/LINE/' b.txt
ubuntu@ppi:~/week3_repo2$ echo "new line" >> c.txt
ubuntu@ppi:~/week3_repo2$
ubuntu@ppi:~/week3_repo2$ git diff --word-diff
diff --git a/a.txt b/a.txt
index d5c7f08..c524796 100644
diff --git a/a.txt b/a.txt
index d5c7f08..c524796 100644
--- a/a.txt
+++ b/a.txt
@@ -7,4 +7,4 @@ a.txt line 6
a.txt line 7
a.txt line 8
a.txt line 9
a.txt [-line-]{+LINE+} 10
diff --git a/b.txt b/b.txt
index 2fa71af..b518eb0 100644
--- a/b.txt
+++ b/b.txt
@@ -1,8 +1,8 @@
b.txt line 1
b.txt line 2
b.txt [-line-]{+LINE+} 3
b.txt line 4
b.txt [-line-]{+LINE+} 5
b.txt line 6
b.txt line 7
b.txt line 8
diff --git a/c.txt b/c.txt
index bc59712..0f58125 100644
--- a/c.txt
+++ b/c.txt
@@ -8,3 +8,4 @@ c.txt line 7
c.txt line 8
c.txt line 9
set mark: ...skipping...
diff --git a/a.txt b/a.txt
index d5c7f08..c524796 100644
--- a/a.txt
+++ b/a.txt
@@ -7,4 +7,4 @@ a.txt line 6
a.txt line 7
a.txt line 8
a.txt line 9
a.txt [-line-]{+LINE+} 10
diff --git a/b.txt b/b.txt
index 2fa71af..b518eb0 100644
--- a/b.txt
+++ b/b.txt
@@ -1,8 +1,8 @@
b.txt line 1
b.txt line 2
b.txt [-line-]{+LINE+} 3
b.txt line 4
b.txt [-line-]{+LINE+} 5
b.txt line 6
b.txt line 7
b.txt line 8
diff --git a/c.txt b/c.txt
index bc59712..0f58125 100644
--- a/c.txt
+++ b/c.txt
@@ -8,3 +8,4 @@ c.txt line 7
c.txt line 8
c.txt line 9
...skipping...
diff --git a/a.txt b/a.txt
index d5c7f08..c524796 100644
--- a/a.txt
+++ b/a.txt
@@ -7,4 +7,4 @@ a.txt line 6
a.txt line 7
a.txt line 8
a.txt line 9
a.txt [-line-]{+LINE+} 10
diff --git a/b.txt b/b.txt
index 2fa71af..b518eb0 100644
--- a/b.txt
+++ b/b.txt
@@ -1,8 +1,8 @@
b.txt line 1
b.txt line 2
b.txt [-line-]{+LINE+} 3
b.txt line 4
b.txt [-line-]{+LINE+} 5
b.txt line 6
b.txt line 7
b.txt line 8
diff --git a/c.txt b/c.txt
index bc59712..0f58125 100644
--- a/c.txt
+++ b/c.txt
@@ -8,3 +8,4 @@ c.txt line 7
c.txt line 8
c.txt line 9
```

### Observation 14: Collect all the commits hashes for `main`, `branch1` and `branch2` HEADs, extract trees and use cat-file to get the list of blobs for every tree from the list. Describe a difference between the trees of all the possible pairs(main & branch1, main & branch2, branch1 & branch2).
```
ubuntu@ppi:~/week3_repo2$ git log --oneline --graph --all
* abb8fa2 (branch1) Patch1
* 497ad1d (HEAD -> branch2, main) Initial version of a.txt, b.txt, and c.txt
* a8d806f Initial empty commit
```

### Observation 15: Note the output of git merge command. Explain why merge behave that way. Run git status and then `git diff` and `git diff --cached` commands to view the state of repository.
```
ubuntu@ppi:~/week3_repo2$ git merge-base branch1 branch2
497ad1d2b9b7ab2b9a33d05d0136099a43a31098
ubuntu@ppi:~/week3_repo2$ git checkout branch2
M       a.txt
M       b.txt
M       c.txt
Already on 'branch2'
ubuntu@ppi:~/week3_repo2$ git merge branch1
Updating 497ad1d..abb8fa2
error: Your local changes to the following files would be overwritten by merge:
        a.txt
        b.txt
Please commit your changes or stash them before you merge.
Aborting
ubuntu@ppi:~/week3_repo2$ git status
On branch branch2
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   a.txt
        modified:   b.txt
        modified:   c.txt

no changes added to commit (use "git add" and/or "git commit -a")
ubuntu@ppi:~/week3_repo2$ git diff
diff --git a/a.txt b/a.txt
index d5c7f08..c524796 100644
--- a/a.txt
+++ b/a.txt
@@ -7,4 +7,4 @@ a.txt line 6
 a.txt line 7
 a.txt line 8
 a.txt line 9
-a.txt line 10
+a.txt LINE 10
diff --git a/b.txt b/b.txt
index 2fa71af..b518eb0 100644
--- a/b.txt
+++ b/b.txt
@@ -1,8 +1,8 @@
 b.txt line 1
 b.txt line 2
-b.txt line 3
+b.txt LINE 3
 b.txt line 4
-b.txt line 5
+b.txt LINE 5
 b.txt line 6
 b.txt line 7
 b.txt line 8
diff --git a/c.txt b/c.txt
index bc59712..0f58125 100644
--- a/c.txt
+++ b/c.txt
@@ -8,3 +8,4 @@ c.txt line 7
 c.txt line 8
 c.txt line 9
 c.txt line 10
+new line
```

### Observation 16: Find `<<<<<HEAD` mark inside a file and manually edit that part to have some reasonable aggregated content of the file. Save the file and add it to staging area. Run `git merge --continue` to complete the merge after conflict resolve. Provide the output of `git log --oneline --graph` command after that.


## Test Cases

| Test Case | Precondition | Steps | Expected Results |
|-----------|--------------|-------|------------------|
| **1: Browse and filter the menu by dietary preference** | User is on the homepage and has access to the full menu. | - Navigate to the 'Menu' page  <br> - Observe each item to confirm that it displays a name, description, price and image <br> - Select the "Vegetarian" dietary filter <br> - Clear the filter <br> - Select an uncommon filter like 'Gluten-free' <br> - Switch categories while a dietary filter is still applied <br> - Reload the page | - Menu grouped by category <br> - Name, description, price, image visible <br> - Only vegetarian items shown <br> - All items reappear <br> - Matching items or 'No items' message shown <br> - Filtered items shown in new category <br> - Filter resets to default |
| **2: Place a pickup order with valid inputs** | Customer has accessed the menu and selected at least one item | - Add burger and drink to basket <br> - Proceed to checkout <br> - Choose 'Pickup' <br> - Enter name, phone, collection time <br> - Submit order <br> - Receive confirmation email/SMS <br> - Check cart is empty | - Cart updates to 2 items <br> - Checkout shows item/price <br> - Pickup selected, delivery hidden <br> - Fields accept input <br> - Confirmation page with order ID <br> - Message includes summary <br> - Cart is reset |
| **3: Order fails due to missing required fields** | User adds item and proceeds to checkout | - Select 'Delivery' <br> - Leave fields blank, submit <br> - Enter name/phone only <br> - Enter invalid phone/address <br> - Correct inputs <br> - Submit order <br> - Open dev console | - Address fields visible <br> - Required field errors <br> - Address field shows error <br> - Validation errors for both <br> - Errors disappear <br> - Confirmation shown <br> - No uncaught exceptions |
| **4: Find the nearest restaurant using location access** | Browser supports geolocation and permissions granted | - Go to 'Find a Location' <br> - Click 'Use my location' <br> - Accept location access <br> - Click on a listed location <br> - Reload and deny access <br> - Enter invalid address <br> - Enter valid address | - Location/manual input option shown <br> - Browser prompts for permission <br> - Locations shown by distance <br> - Info displayed <br> - Manual field shown <br> - 'Unable to find location' error <br> - Nearest branch shown |
| **5: Admin updates the price of a menu item** | Admin is logged in via secure login | - Go to 'Admin Panel' → 'Menu Management' <br> - Select item (e.g. 'Classic Burger') <br> - Change price from $5.99 to $6.49 <br> - Submit update <br> - Visit public menu <br> - Edit price to -1 <br> - Set price to £0 and submit | - Item list appears <br> - Edit form shows item info <br> - New price accepted <br> - 'Item updated' message <br> - Public price is $6.49 <br> - Validation error for negative <br> - Item shown as free or flagged |
| **6: Repeat a previous order** | Returning customer logged in with past orders | - Log in <br> - Go to 'Order History' <br> - Click 'Repeat Order' <br> - View cart <br> - Remove one item <br> - Proceed to checkout with 'Pickup' <br> - Complete the order | - Dashboard shown <br> - Orders listed <br> - Items added to cart <br> - Correct quantities and prices <br> - Cart updates <br> - Checkout works normally <br> - Confirmation and notification |
