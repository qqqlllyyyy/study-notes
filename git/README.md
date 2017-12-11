# Git Notes

Check whether git is installed
```bash
which git # Check whether git is installed
git --version # Get version
```

### Configurations

There are three levels of configurations:

* System:
  * Location: `/etc/gitconfig`
  * How to direct: `git config --system`
* User:
  * `~/.gitconfig`
  * How to direct: `git config --global`
* Project:
  * `my_project/.git/config`
  * How to direct: `git config`

Examples:

```bash
# Set username, email and default editor
git config --global user.name "qqqlllyyyy"
git config --global user.email "qinliyu1990@gmail.com"
git config --global core.editor "mate -wl1"

# Allow git to use different colors
git config --global color.ui true

# View configurations
git config --list
git config user.name
```

Setup Auto-completion:

```bash
# Change to home dir
cd ~
# Download
curl -0L https://github.com/git/git/raw/master/contrib/completion/git-completion.bash
# Rename file
mv ~/git-completion.bash ~/.git-completion.bash
# Edit ~/.bash_profile or ~/.bashrc
```
