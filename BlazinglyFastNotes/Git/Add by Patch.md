* Purpose
	* To add parts of changes to a file, in case you don't want everything committed
```
git add --patch <filename>
```

or

```
git add -p <filename>
```

* this pulls up a list of options and steps through in "hunks"
* It then prompts with the question

```
Stage this hunk [y,n,q,a,d,/,j,J,g,s,e,?]?
```

Here is a description of each option:

- `y` stage this hunk for the next commit
- `n` do not stage this hunk for the next commit
- `q` quit; do not stage this hunk or any of the remaining hunks
- `a` stage this hunk and all later hunks in the file
- `d` do not stage this hunk or any of the later hunks in the file
- `g` select a hunk to go to
- `/` search for a hunk matching the given regex
- `j` leave this hunk undecided, see next undecided hunk
- `J` leave this hunk undecided, see next hunk
- `k` leave this hunk undecided, see previous undecided hunk
- `K` leave this hunk undecided, see previous hunk
- `s` split the current hunk into smaller hunks
- `e` manually edit the current hunk
    - You can then edit the hunk manually by replacing `+`/`-` by `#` (thanks [veksen](https://stackoverflow.com/users/1732521/veksen))
- `?` print hunk help

If the file is not in the repository yet, you can first do `git add -N <filename>`. Afterwards you can go on with `git add -p <filename>`.

Afterwards, you can use:

- `git diff --staged` to check that you staged the correct changes
- `git reset -p` to unstage mistakenly added hunks
- `git commit -v` to view your commit while you edit the commit message.

Note this is far different than the `git format-patch` command, whose purpose is to parse commit data into a `.patch` files.

### More patch magic
* You can pull specific files from a different branch to your own branch
* Run this command on the branch you want to bring code **into**
```
git checkout --patch origin/[branch] [folder/path]
```
* This has the same functionality, but for a specific file or folder from another branch. Useful for easily merging small changes