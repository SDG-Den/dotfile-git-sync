# dotfile-git-sync
simple script to selectively migrate your dotfiles to a git repository using stow. 

how it works:

run sync.sh either with file path to a github repository, or without and have it ask you.


the script will list all the directories in your .config directory, you can select multiple directories with tab.

all the selected directories will be moved to your github repository, stowed back into your .config file with gnu stow (via symlink), and the github repository will be added, commited and pushed. 

the script will add a note to the bottom of your README.md file to let you know when the import was run and what files were added. 


the script does the following:

first, it presents you with a menu of *folders in your .config directory*, this specifically excludes both files and symlinks, so only things that still need to be imported are shown.

you can select multiple with tab and press enter to commit, this will then output a list.

the script will check if each of those folder names already exists in your chosen git repository folder, and if it does, renames it. 

then, it will move the folder from your config to your chosen git repository folder.

it'll then get a list of all folders in the git repository folder, and check if those folders exist either as symlinks or as directories in your .config folder.

if they exist as symlinks, the symlink is removed safely without affecting the content.

if they exist as folders, the folders are renamed. 

then, the script will stow your chosen git repo directory in .config, symlinking all of your config directories back into their correct place (except the actual files are now in your github repository)

lastly, it will check if there's a .git folder, and if there is, it'll run the git add, git commit and git push commands to upsync your repository, leaving a note in your README.md


# to install
make sure you have the following requirements:

- bash
- stow
- git
- fzf

step 1: make a directory in ~/.local/share:

`mkdir -p ~/.local/share/dotfile-git-sync`


step 2: copy the file to this directory

`cp ./dotfile-git-sync ~/.local/share/dotfile-git-sync`


step 3: optionally link this to your /usr/bin folder to add it as a command

`sudo ln -sf /home/$(whoami)/.local/share/dotfile-git-sync /usr/bin`


now you can run the following:

`dotfile-git-sync ~/My-Dotfile-Repository`

if your github repository is called "My Dotfile Repository" and is directly in your home directory, you can now use the script to import your dotfiles and symlink them back. 