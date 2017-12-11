# Introduction

```bash
# Install Homebrew
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
# Update Brew to the newest version
brew update
# Install Node
brew install node
# Get version for Node
node -v
# Update Node
brew upgrade node
# Uninstall Node and npm
brew uninstall node
```

Environment setup for Mercury
```bash
# Install yarn
npm install -g yarn
# Set up your NPM registry
npm config set registry https://sj-artifactory.marketo.com/artifactory/api/npm/npm-mkto
curl -u$(whoami) "https://sj-artifactory.marketo.com/artifactory/api/npm/auth" >> ~/.npmrc
```
