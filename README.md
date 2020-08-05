# dotfiles

A place to keep my dotfiles safe and versioned. This repo follows the bare git repo approach outlined [here](https://www.atlassian.com/git/tutorials/dotfiles).

## setting up a new machine

The steps I take to commission a new machine with the dotfiles contained in this repo.

1. Initialize this repo as a bare git repository in your home directory.
```
git clone --bare git@github.com:Parker-Bartlett/dotfiles.git $HOME/dotfiles
```

2. Create an alias for your new dotfiles repository, you'll use this in replace of `git` when interacting with your dotfiles.
```
echo "alias dotfiles='/usr/bin/git --git-dir=$HOME/dotfiles/ --work-tree=$HOME'" >> $HOME/.zshrc
```

3. Get dotfiles in this repo on your machine. Running this command will add the given gitfiles in the location they were added, such as putting your `.vimrc` in your home directory.
```
cd $HOME/dotfiles && dotfiles checkout
```
The above command assumes you don't have any existing configuration files that will conflict with the incoming git changes. You may receive an error that looks like the below code snippet, to fix this remove the existing file or back them up elsewhere.
```
error: The following untracked working tree files would be overwritten by checkout:
	.vimrc
Please move or remove them before you switch branches.
Aborting
```

4. Since we want to ignore that majority of what is on our system can also set the `showUntrackedFiles` to `no`, this will help alleviate clutter when running commands like `dotfiles status` in your home directory.
```
dotfiles config --local status.showUntrackedFiles no
```
