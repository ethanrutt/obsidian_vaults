# Checkout has more uses than just switching branches
* The [checkout](https://git-scm.com/docs/git-checkout) command has a lot of cool stuff other than just switching branches or creating new ones.
* Quick refresher:
	* `git checkout main` will checkout the main branch
	* `git checkout -b new_branch` will create a new branch called `new_branch` and check it out (switch to that branch)
* For most people, this might be all they know about checkout
**Fix this later** 
```bash
git checkout feature_branch -- app.js
```

to grab `app.js` from `feature_branch`
`feature_branch` can also be a commit instead
```bash
git checkout 123456789 -- app.js
```
