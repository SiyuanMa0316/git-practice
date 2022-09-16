# git-practice
Work with your teammate to practice git collaboration:

both clone the repo:
```
git clone <url>
```
```
siyuan@:~/person1$ git clone https://github.com/EE422C/git-practice-test2.git
Cloning into 'git-practice-test2'...
Username for 'https://github.com': siyuanma0316
Password for 'https://siyuanma0316@github.com':
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 4 (delta 0), reused 3 (delta 0), pack-reused 0
Receiving objects: 100% (4/4), done.
```

person 1 add some arbitrary lines to the file

person 1 commit and push:
```
git add *
git commit -m "person 1 modified"
git push origin main
```
```
siyuan@:~/person1/git-practice-test2$ git push origin main
Username for 'https://github.com': siyuanma0316
Password for 'https://siyuanma0316@github.com':
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 16 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 290 bytes | 290.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/EE422C/git-practice-test2.git
   2034d36..85a3b4e  main -> main
```
person 2 add some arbitrary lines to the file

person 2 commit and push (push fails because person 2 modified the same line)
```
git add *
git commit -m "person 2 modified"
git push origin main
```
```
siyuan@:~/person2/git-practice-test2$ git push origin main
Username for 'https://github.com': siyuanma0316
Password for 'https://siyuanma0316@github.com':
To https://github.com/EE422C/git-practice-test2.git
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/EE422C/git-practice-test2.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
person 2 pull
```
git pull origin main
```
```
siyuan@:~/person2/git-practice-test2$ git pull origin main
Username for 'https://github.com': siyuanma0316
Password for 'https://siyuanma0316@github.com':
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 270 bytes | 270.00 KiB/s, done.
From https://github.com/EE422C/git-practice-test2
 * branch            main       -> FETCH_HEAD
   2034d36..85a3b4e  main       -> origin/main
hint: You have divergent branches and need to specify how to reconcile them.
hint: You can do so by running one of the following commands sometime before
hint: your next pull:
hint:
hint:   git config pull.rebase false  # merge (the default strategy)
hint:   git config pull.rebase true   # rebase
hint:   git config pull.ff only       # fast-forward only
hint:
hint: You can replace "git config" with "git config --global" to set a default
hint: preference for all repositories. You can also pass --rebase, --no-rebase,
hint: or --ff-only on the command line to override the configured default per
hint: invocation.
fatal: Need to specify how to reconcile divergent branches.
```

person 2 pull and solve the conflict
```
siyuan@:~/person2/git-practice-test2$ git config pull.rebase false
siyuan@:~/person2/git-practice-test2$ git pull origin main
Username for 'https://github.com': siyuanma0316
Password for 'https://siyuanma0316@github.com':
From https://github.com/EE422C/git-practice-test2
 * branch            main       -> FETCH_HEAD
Auto-merging practice_file
CONFLICT (content): Merge conflict in practice_file
Automatic merge failed; fix conflicts and then commit the result.
```
manual merge: change practice_file from
```
<<<<<<< HEAD
line 2
=======
line 1
>>>>>>> 85a3b4e2f7c9147f425d8ced90970f31db9deec8
```
to
```
line 1
line 2
```

person 2 commit and push
```
siyuan@:~/person2/git-practice-test2$ git add *
siyuan@:~/person2/git-practice-test2$ git commit -m "person 2 manual merge"
[main a14cb83] person 2 manual merge
siyuan@:~/person2/git-practice-test2$ git push origin main
Username for 'https://github.com': siyuanma0316
Password for 'https://siyuanma0316@github.com':
Enumerating objects: 10, done.
Counting objects: 100% (10/10), done.
Delta compression using up to 16 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 585 bytes | 585.00 KiB/s, done.
Total 6 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/EE422C/git-practice-test2.git
   85a3b4e..a14cb83  main -> main
```

git log will look like
```
siyuan@:~/person2/git-practice-test2$ git log
commit a14cb832123f6348234649eb49c2a41e9ed8095a (HEAD -> main, origin/main, origin/HEAD)
Merge: 81c2eb1 85a3b4e
Author: Siyuan Ma <masiyuan0@gmail.com>
Date:   Fri Sep 16 01:33:30 2022 -0500

    person 2 manual merge

commit 81c2eb1950fbac412305a4b1739152fbec50d008
Author: Siyuan Ma <masiyuan0@gmail.com>
Date:   Fri Sep 16 01:25:04 2022 -0500

    person 2 modified

commit 85a3b4e2f7c9147f425d8ced90970f31db9deec8
Author: Siyuan Ma <masiyuan0@gmail.com>
Date:   Fri Sep 16 01:23:15 2022 -0500

    person 1 modified

commit 2034d36833a534516b5fda482ae564affd339565
Author: github-classroom[bot] <66690702+github-classroom[bot]@users.noreply.github.com>
Date:   Fri Sep 16 06:18:29 2022 +0000

    Initial commit
```

Person 1 can do the same practice again.
