# SETUP

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

brew cask install iterm2 git mounty
brew link --overwrite git

brew install zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
brew install fzf
source ~/.zshrc # copy file first

brew install coreutils diffutils findutils \
  gawk gnu-indent gnu-sed gnu-tar gnu-getopt gnu-which \
  grep gzip watch wdiff wget \
  rsync vim node ripgrep flake8

brew cask install brave-browser google-chrome firefox \
  slack spotify textmate unshaky virtualbox dashlane \
  the-unarchiver transmission itsycal skype \
  sublime-text visual-studio-code vlc chromedriver gimp

brew install python
pip install selenium bs4 requests lxml

npm install less
npm install -g create-react-app

brew tap homebrew/cask-fonts
brew cask install font-fira-code font-firacode-nerd-font \
  font-iosevka-nerd-font font-iosevka-nerd-font-mono \
  font-firacode-nerd-font-mono

# openssl
brew install openssl
export PATH="/usr/local/opt/openssl@1.1/bin:$PATH"
export LDFLAGS="-L/usr/local/opt/openssl@1.1/lib"
export CPPFLAGS="-I/usr/local/opt/openssl@1.1/include"
```

# add spacer on menu
`defaults write com.apple.dock persistent-apps -array-add '{"tile-type"="spacer-tile";}'; killall Dock`
