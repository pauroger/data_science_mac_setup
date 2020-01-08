# Mac set up for data science projects

My stable set-up to be able to have self-contained and reproducible projects.

## Motivation

* Have you ever struggled with installations paths and packages versions?

* Have you end up installing everything in both Anaconda and Homebrew to avoid ``path`` issues? Only to result in a big mess when an actual issue presents itself?

* Have you forgot to activate a virtual environment and then messed up the project?

After facing all these issues and more, I've come up with this setup and I thought I make a small repo about it :)

## Table of contents

- [Mac set up for data science projects](#mac-set-up-for-data-science-projects)
  - [Motivation](#motivation)
  - [Table of contents](#table-of-contents)
  - [Uninstall Anaconda ](#uninstall-anaconda)
  - [Install the basics ](#install-the-basics)
  - [Virtual enviroments ](#virtual-enviroments)
  - [Webography ](#webography)

## Uninstall Anaconda <a name="anaconda"></a>

This set up will use Homebrew, I find it more lightweight and easier to work with. If you have Anaconda installed:

```bash
# Delete configs
conda install anaconda-clean

anaconda-clean --yes

# Delete the anaconda install folder
rm -rf ~/anaconda
```

## Install the basics <a name="basics"></a>

```bash
# Homebrew
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# Latest Python
brew install python3

# iTerm2
brew cask install iterm2  # Or download here: https://iterm2.com/

# Oh My Zsh
brew install zsh zsh-completions

# Looks matter! Make the terminal look nice
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
```

In your `~/.zshrc.` change the followoing:

```bash
# This
export PATH="/Users/<your_user>/anaconda3/bin:$PATH"

# To this
export PATH="/usr/local/bin:$PATH"

# Then add the line
ZSH_THEME=powerlevel10k/powerlevel10k

# You will probably want to set up at least a couple of aliases
alias pip="pip3"
alias python="python3"
```

Then save, restart your terminal and follow the instructions.

## Virtual enviroments <a name="venv"></a>

One virtual environment per project will make your life much easier. However, the 'standard' way requires you to remember to activate and deactivate them every time you switch folders.

This is why I find this auto-switch piece of code helpful.

```bash
pip install virtualenv

pip install virtualenvwrapper

cd /Users/<your_user>/.oh-my-zsh/custom/plugins

git clone "https://github.com/MichaelAquilina/zsh-autoswitch-virtualenv.git" "$ZSH_CUSTOM/plugins/autoswitch_virtualenv"
```

Add the following plugin to your `.zshrc`: `plugins=(autoswitch_virtualenv $plugins)`.

Now, every time you get into a folder that contains a `requirements.txt`, your terminal will switch automatically to the virtual environment if exists, or recommend you to create a new one by running the command `mkvenv`. To delete it, run `rmvenv`.

Auto-switch will add a file called `.venv` into every project, you will have to add it into your `.gitignore`'s.

**Use the same virtual environment in the Jupyter Notebooks within that project.**

You will need to create a new kernel per project by following the next steps:

```bash
# If needed install Jupyter
pip install jupyter

# Install IPython kernel for Jupyter
pip install ipykernel

# If required, create virtual environment
mkvenv

# Build new Kernel
ipython kernel install --user --name=<repo-name>

# Start notebook and select the new kernel
jupyter notebook
```

To uninstall Kernels:

```bash
# See a list of current Kernels
jupyter kernelspec list

# Uninstall the desired one
jupyter kernelspec uninstall <unwanted-kernel>
```

## Webography <a name="webography"></a>

In alphabetical order.

```bash
https://docs.anaconda.com/anaconda/install/uninstall/
https://github.com/MichaelAquilina/zsh-autoswitch-virtualenv/
https://github.com/robbyrussell/oh-my-zsh/wiki/Installing-ZSH
https://github.com/romkatv/powerlevel10k
https://iterm2.com/
```
