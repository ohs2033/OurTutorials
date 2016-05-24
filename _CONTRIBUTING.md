# Contributing

##Git Rebase Workflow : A Summary(in korean)

1. git checkout master

2. git pull --rebase upstream master
    **1,2 : 기존에 다른사람이 업데이트했을 수 있는 upstream의 내용을 전부 pull한다.

3. git chekout -b feature-branch
    **모든 local 작업들은 **절대** master 브랜치에서 하지 않는다.
    **모든 local 작업들은 **절대** master 브랜치에 merge하거나 rebase하지 않는다.

4. edd/git add/git commit (작업하기)
    **모든 local 작업들은 해당 각 작업에 맞는 branch에서 수행하도록 한다.
    **branch 이름은 다음 convention을 따르도록 한다.
      - bug/...
      - feat/...
      - test/...
      - doc/...
      - refactor/...
5. git pull --rebase upstream master 

    *push를 하기 전에 upstream(원래 repo)에 있는 정보들을 전부 최신화 해 주기
    *반드시 모든 local change를 커밋한 후 실행할 것!

-----------------**---------여기서 CONFLICT가 일어날 경우-----------**----------------
    5-1. 이 때 conflict가 일어난다는 것은, 4에서 수정했던 파일을 다른 Contributor가 수정하여 Pull request를 날렸다는 의미이다.
         먼저 Conflict가 일어난 파일로 가서 수정을 해 준다.
    5-2. 그리고 git add 를 해 준다.
    5-3. git rebase --continue 를 입력한다.
    5-4. 이 과정을 충돌이 일어난 개수만큼 반복한다.
    5-5. CONFLICT가 해결되었다.
-----------------**--------------------------------------------**----------------

6. git push origin feature-branch
    **push origin master를 하면 안된다. 반드시 작업한 해당 branch에 Pull Request를 날릴 것 !

7. Submit PR
    ** 자기자신이 pullrequest를 받지 말고, 반드시 타인이 Review를 한 후 실행하도록 함.






## General Workflow

1. Fork the repo
2. Cut a namespaced feature branch from master
  - bug/...
  - feat/...
  - test/...
  - doc/...
  - refactor/...
3. Make commits to your feature branch. Prefix each commit like so:
  - (feat) Added a new feature
  - (fix) Fixed inconsistent tests [Fixes #0]
  - (refactor) ...
  - (cleanup) ...
  - (test) ...
  - (doc) ...
4. When you've finished with your fix or feature, Rebase upstream changes into your branch. submit a pull request
   directly to master. Include a description of your changes.
5. Your pull request will be reviewed by another maintainer. The point of code
   reviews is to help keep the codebase clean and of high quality and, equally
   as important, to help you grow as a programmer. If your code reviewer
   requests you make a change you don't understand, ask them why.
6. Fix any issues raised by your code reviwer, and push your fixes as a single
   new commit.
7. Once the pull request has been reviewed, it will be merged by another member of the team. Do not merge your own commits.

## Detailed Workflow

### Fork the repo

Use github’s interface to make a fork of the repo, then add that repo as an upstream remote:

```
git remote add upstream https://github.com/codestates/<NAME_OF_REPO>.git
```

### Cut a namespaced feature branch from master

Your branch should follow this naming convention:
  - bug/...
  - feat/...
  - test/...
  - doc/...
  - refactor/...

These commands will help you do this:

``` bash

# Creates your branch and brings you there
git checkout -b `your-branch-name`
```

### Make commits to your feature branch. 

Prefix each commit like so
  - (feat) Added a new feature
  - (fix) Fixed inconsistent tests [Fixes #0]
  - (refactor) ...
  - (cleanup) ...
  - (test) ...
  - (doc) ...

Make changes and commits on your branch, and make sure that you
only make changes that are relevant to this branch. If you find
yourself making unrelated changes, make a new branch for those
changes.

#### Commit Message Guidelines

- Commit messages should be written in the present tense; e.g. "Fix continuous
  integration script".
- The first line of your commit message should be a brief summary of what the
  commit changes. Aim for about 70 characters max. Remember: This is a summary,
  not a detailed description of everything that changed.
- If you want to explain the commit in more depth, following the first line should
  be a blank line and then a more detailed description of the commit. This can be
  as detailed as you want, so dig into details here and keep the first line short.

### Rebase upstream changes into your branch

Once you are done making changes, you can begin the process of getting
your code merged into the main repo. Step 1 is to rebase upstream
changes to the master branch into yours by running this command
from your branch:

```bash
git pull --rebase upstream master
```

This will start the rebase process. You must commit all of your changes
before doing this. If there are no conflicts, this should just roll all
of your changes back on top of the changes from upstream, leading to a
nice, clean, linear commit history.

If there are conflicting changes, git will start yelling at you part way
through the rebasing process. Git will pause rebasing to allow you to sort
out the conflicts. You do this the same way you solve merge conflicts,
by checking all of the files git says have been changed in both histories
and picking the versions you want. Be aware that these changes will show
up in your pull request, so try and incorporate upstream changes as much
as possible.

You pick a file by `git add`ing it - you do not make commits during a
rebase.

Once you are done fixing conflicts for a specific commit, run:

```bash
git rebase --continue
```

This will continue the rebasing process. Once you are done fixing all
conflicts you should run the existing tests to make sure you didn’t break
anything, then run your new tests (there are new tests, right?) and
make sure they work also.

If rebasing broke anything, fix it, then repeat the above process until
you get here again and nothing is broken and all the tests pass.

### Make a pull request

Make a clear pull request from your fork and branch to the upstream master
branch, detailing exactly what changes you made and what feature this
should add. The clearer your pull request is the faster you can get
your changes incorporated into this repo.

At least one other person MUST give your changes a code review, and once
they are satisfied they will merge your changes into upstream. Alternatively,
they may have some requested changes. You should make more commits to your
branch to fix these, then follow this process again from rebasing onwards.

Once you get back here, make a comment requesting further review and
someone will look at your code again. If they like it, it will get merged,
else, just repeat again.

Thanks for contributing!

### Guidelines

1. Uphold the current code standard:
    - Keep your code DRY.
    - Follow STYLE-GUIDE.md
2. Run the tests before submitting a pull request.
3. Tests are very, very important. Submit tests if your pull request contains
   new, testable behavior.
4. Your pull request is comprised of a single squashed commit.

## Checklist:

This is just to help you organize your process

- [ ] Did I cut my work branch off of master (don't cut new branches from existing feature brances)?
- [ ] Did I follow the correct naming convention for my branch?
- [ ] Is my branch focused on a single main change?
 - [ ] Do all of my changes directly relate to this change?
- [ ] Did I rebase the upstream master branch after I finished all my
  work?
- [ ] Did I write a clear pull request message detailing what changes I made?
- [ ] Did I get a code review?
- [ ] Did I make any requested changes from that code review?

If you follow all of these guidelines and make good changes, you should have
no problem getting your changes merged in.
