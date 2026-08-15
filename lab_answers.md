# IT3130 Lab 4 — Written Answers

1. Difference between `git branch <name>` and `git switch -c <name>`:
> `git branch <name>` creates a new branch reference but does not change your working branch. `git switch -c <name>` (or `git checkout -b <name>`) creates the branch and immediately switches your working tree to it. Use `git branch` when you only want to create a branch; use `git switch -c` to create-and-checkout.
>

2. Why develop a new feature in a feature branch instead of directly in `main`?
> Feature branches isolate work so the `main` branch remains stable. They let you develop, test, and iterate without affecting production code, enable code review via pull requests, support parallel development by multiple contributors, and make it easier to revert or discard unfinished work.
>

3. What does `git push -u origin <branch-name>` achieve?
> This pushes the local branch to the remote named `origin` and sets the remote branch as the upstream (tracking) branch for the local branch. After this, plain `git push` and `git pull` will default to that upstream branch.
>

4. Purpose of a pull request, and what a reviewer should check before approving:
> A pull request (PR) is a formal request to merge changes from one branch into another (typically a feature into `main`). It provides a place for discussion, automated checks (CI), and code review. A reviewer should check:
- Correctness: the code does what it claims and covers edge cases.
- Tests: unit/integration tests pass and new tests are added where appropriate.
- Style and readability: code is clear, consistent, and well-documented.
- Security and performance: no obvious vulnerabilities or regressions.
- Build and CI: the PR passes automated checks and builds cleanly.
- Scope: the changes are focused and the commit messages are meaningful.
- Mergeability: no unresolved conflicts with the base branch.
>

5. Describe the GitHub Flow sequence from starting a feature to completing the work:
> Typical GitHub Flow:
1. Update local `main`: `git switch main && git pull origin main`.
2. Create a feature branch: `git switch -c feature/<id>/<short-name>`.
3. Implement the feature in small, atomic commits with clear messages.
4. Push the branch: `git push -u origin <branch>`.
5. Open a PR on GitHub, request reviewers, and describe the change and test plan.
6. Address feedback by pushing further commits to the same branch.
7. Once approved and CI passes, merge the PR (or squash/merge per project policy).
8. Delete the remote feature branch and update local branches: `git switch main && git pull origin main && git branch -d <branch>`.
>

6. Why are meaningful branch names and small atomic commits important in team development?
> Meaningful branch names make it easy to know the purpose of a branch at a glance and find related work. Small, focused commits are easier to review, bisect, revert, and reason about; they reduce review friction and improve the quality of code history.
>

7. Why is it good practice to delete a feature branch after it's merged?
> Deleting merged feature branches keeps the repo tidy and reduces confusion about which branches are active. The branch's commits remain in the project's history after merging, so the branch can be recreated if needed.
>

8. Steps to safely resolve a PR conflict with `main` and update the PR:
> One safe approach (merge-based):
1. Fetch and update `main`: `git fetch origin && git switch main && git pull origin main`.
2. Switch to your feature branch: `git switch feature/<id>/<name>`.
3. Merge `main` into your branch: `git merge main`.
4. Resolve conflicts in your editor, run tests, and `git add` the resolved files.
5. Commit the merge: `git commit` (if needed) and push: `git push`.
6. The PR updates automatically with the conflict resolution.

Alternative (rebase-based):
- Rebase your feature branch onto the latest `main` (`git fetch origin && git rebase origin/main`) resolve conflicts, then `git push --force-with-lease` to update the PR. Use rebasing only if your team permits history rewriting.

Commands example (merge approach):
```bash
git fetch origin
git switch main
git pull origin main
git switch feature/it24102843/profile-page
git merge main
# Resolve conflicts, run tests
git add .
git commit
git push
```

>
