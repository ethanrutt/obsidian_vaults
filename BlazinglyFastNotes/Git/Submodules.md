* Submodules are basically nested repositories. You can have a repository inside of another repository.
* My use case for this is in my [dots](https://github.com/ethanrutt/dots) repository. I have stuff like my neovim config, awesomewm config, and this obsidian vault collection submoduled, that way I can edit them separately and then reference them inside my config.
* These repositories will have a separate lifespan from my dotfiles. Making a couple changes in my `.bashrc` shouldn't make me have to commit something to my neovim config, and vice versa. This is just another way of decoupling my configuration files from each other. This is also very nice when working on multiple systems (which I do). I don't want to have to pull my linux config files if i'm working on windows or mac
* Getting started is pretty simple, once you have your two repositories that you want to set up, you can do a simple command to start submoduling.
* Let's walk through this example. You have your dotfiles and you want to add your second brain to them, in my case obsidian.
* Going to the  `obsidian/files` directory, I can do
```bash
git submodule add https://github.com/ethanrutt/obsidian_vaults
```
*  Once this is done, I now have effectively cloned the repository and placed it into this folder.
* We also now have a `.gitmodules` file at the top level at the parent repository. This contains the relative path to where the repository lives in your parent repository
* It also contains the remote url where the child repository lives.
* Changes you make to the child repository can be committed directly to that repository from inside.
* It's important to note that doing this effectively checks out a `commit` of the child repository. When you run something like `git status` in the parent repository, you will see a particular commit, not the actual stuff that you've changed.
* Whenever pushing code, you have to make sure that you add that submodule too if you want to update the commits that it's going to grab the next time you pull.
* Pulling and cloning with submodules is also a little different. Again, we are working in commit land for that submodule.
* If you look in the  `dots` binary in my dotfiles repository, you'll see that when I clone the repository, I have a special flag in there. The command is
```bash
  git clone --recurse-submodules --quiet https://github.com/ethanrutt/dots.git "$DOTS_DIR"
```
* There is a `--recurse-submodules` flag in there. This means that we will also have to grab the submodules and set up our `.gitmodules` file
* [submodule documentation](https://git-scm.com/book/en/v2/Git-Tools-Submodules)

