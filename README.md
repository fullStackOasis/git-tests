# Simple test

Working on the green feature at this point.

Information about the blue feature.

Saving work at this point on feature-blue.

# What I did

Create main with this README.
Checkout a new branch called `feature-blue`.
Add a file with some things about blue, and update the README with that info.
Check in my code locally.
`git push origin feature-blue`


Next, when someone asks me for a new feature that needs to be done before blue:
Checkout main and pull.
Checkout a new branch called `feature-green`.
Add a file with some things about green, and update the README with that info.
At this point, I realize that the README will have conflicts. This is because I've edited README differently in the `feature-blue` branch. Okay, deal.
Check in my code locally.
`git push origin feature-green`
In GH, create a PR for this branch into `main`. Merge the branch. No conflicts and expected and there are none.
You can safely delete `feature-green` both locally and on GH.
In local, checkout `main`:
`git checkout main`
`git pull`
The latter pulls down the changes from `feature-green` branch, and I can do whatever needed to be done (build e.g.).

Rebase:
Now I need to go back to `feature-blue` and finish work there.
`git checkout feature-blue`.
`git rebase`
... there's a conflict. Address the conflict manually, and `git rebase --continue` as instructed.
... there's another conflict! Repeat. After the second rebase, there are no further complaints.
`git push origin feature-blue` results in a complaint, "Updates were rejected...".
Rename this branch locally:
`git checkout -b feature-blue-after-green`.
`git push origin feature-blue-after-green`.
On GH create a PR and merge the PR into `main`. The PR has no conflicts. 
Voila, you are done. You can delete all the branches.

NOTE: when rebasing you lose all the hashes in your `feature-blue` branch. The original hashes are gone forever and will not be seen in your commits.
You will also lose the timestamps when those changes were made. My `feature-blue` branch for example was changed perhaps 10 days ago.
When I do the rebase, new commits are made with the changes, and they are new hashes timestamped from today. If you're good about it, you can keep the git comments that you made for those commits.
If you think about it, you really have no choice but to lose the timestamps. You are shifting the state of main which had `feature-green` rework applied to `main`'s tip. Then you're applying `feature-blue` on top of that. Either `feature-green` timestamps would have to be shifted back in time artificially or `feature-blue` timestamps need to be shifted forward. Applying the timestamps when the rebasing is done avoids any possible conflicts with respect to shifting timestamps around.

So, in rebasing, you do lose some information. This is not magic.
