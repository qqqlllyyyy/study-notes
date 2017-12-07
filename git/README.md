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
