make sure to reboot.

```bash
# brew

/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# zsh + oh my zsh

brew install zsh
chsh -s $(which zsh)

sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"  
nano ~/.zshrc # set `ZSH_THEME="refined`

# persist bash config in zsh (not sure if this is useful)

echo "source /Users/sueszli/.bash_profile" >> ~/.zshenv
echo "source /Users/sueszli/.bash_profile" >> ~/.zshrc

# asdf: install
# alt: venv, sdkman, jenv, nvm

brew install curl git
brew install asdf
echo -e "\n. $(brew --prefix asdf)/libexec/asdf.sh" >> ${ZDOTDIR:-~}/.zshrc

asdf plugin list all
asdf list all python
asdf current

# asdf: node

brew install gpg gawk
asdf plugin add nodejs
asdf install nodejs latest
asdf global nodejs latest
node --version

# asdf: java

asdf plugin add java
asdf install java openjdk-17
asdf global java openjdk-17
. ~/.asdf/plugins/java/set-java-home.zsh
java --version

# asdf: python

brew install openssl readline sqlite3 xz zlib tcl-tk
asdf plugin add python
asdf install python 3.11.9
asdf global python 3.11.9

python3 --version

# apps

brew install --cask google-chrome
brew install --cask google-drive
brew install --cask obsidian
brew install --cask microsoft-office
brew install --cask android-file-transfer # alternatively: openmtp

# development

xcode-select --install
brew install git
brew install --cask git-credential-manager
brew install --cask visual-studio-code@insiders
brew install --cask jetbrains-toolbox
brew install --cask docker

# menu bar apps

brew install --cask hiddenbar
sudo xattr -r -d com.apple.quarantine /Applications/Hidden\ Bar.app

brew install --cask raycast
brew install --cask alt-tab # has turned very slow since macos security measures
brew install --cask notion-calendar
brew install rectangle # cycle between ½ etc.
brew install stats # show in dock, disable start at startup
brew install --cask scroll-reverser # alt: unnaturalscrollwheels

# other stuff

brew install --cask obs # use native shortcut
brew install --cask shottr # use native shortcut
brew install --cask aldente # too experimental
brew install --cask hyperkey # or rcmd, hotkey-app, karabiner-elements

# remove .DS_FILE from all git commits

echo ".DS_Store" >> ~/.gitignore_global
echo "._.DS_Store" >> ~/.gitignore_global
echo "**/.DS_Store" >> ~/.gitignore_global
echo "**/._.DS_Store" >> ~/.gitignore_global
git config --global core.excludesfile ~/.gitignore_global

# show dot files in finder 

defaults write com.apple.finder AppleShowAllFiles YES

# remove all apps from dockbar

defaults write com.apple.dock persistent-apps -array

# reset launchpad

defaults write com.apple.dock ResetLaunchPad -bool true; killall Dock

# make dockbar hide faster

defaults write com.apple.dock autohide-delay -float 0; defaults write com.apple.dock autohide-time-modifier -int 0;killall Dock
# undo: defaults write com.apple.dock autohide-delay -float 0.5; defaults write com.apple.dock autohide-time-modifier -int 0.5 ;killall Dock

# disable eject notification

sudo defaults write /Library/Preferences/SystemConfiguration/com.apple.DiskArbitration.diskarbitrationd.plist DADisableEjectNotification -bool YES && sudo pkill diskarbitrationd
# undo: sudo defaults delete Library/Preferences/SystemConfiguration/com.apple.DiskArbitration.diskarbitrationd.plist DADisableEjectNotification && sudo pkill diskarbitrationd
```

*app store apps*

- horo timer (timer) → use clock app instead
- tinyStopwatch (stopwatch) → use clock app instead
- qi fm focus & relax songs (white noise) → configure to hide dock icon

*driver: canon scanner*

- https://hk.canon/en/support/0200553204
- then go to settings > (icon on top right that displays the physical device) > scan options > image processing settings > detect the orientation of text original and rotate image

*driver: lenovo docking station*

- might not be necessary
- https://www.synaptics.com/products/displaylink-graphics/downloads/macos-connectivity-1.7.1?filetype=exe

*driver: external monitor*

- might not be necessary
- problem described here: https://apple.stackexchange.com/questions/342682/how-to-properly-use-scaling-on-an-external-display-from-macbook-pro-2016?newreg=f9211d6ea2b14a96888112602c4e0536
- download here: https://github.com/waydabber/BetterDisplay → create dummy display, set resolution to 115% with slider

# settings app

_us-keyboard layout with umlaute_

- https://github.com/patrick-zippenfenig/us-with-german-umlauts
- alt: http://wordherd.com/keyboards/ 
- alt: https://hci.rwth-aachen.de/usgermankeyboard 
- alt: https://ke-complex-modifications.pqrs.org/?q=umlaut

_configuration in settings app_

- notifications:
	- disable when screen is locked
- general:
	- general > language & region > number format: point seperated
- appearance:
	- set dark mode
- control centre:
	- select what to show
- desktop & dock:
	- dock
		- automatically hide and show the dock > true
		- minimize windows using > set to "scale" instead of "genie"
	- desktop & stage manager
		- click wallpaper to reveal desktop > set to "only in stage manager"
	- hot corners (button at bottom)
		- disable all corners
- displays:
	- reduce font size and scale, arrange
- wallpaper:
	- set to black
- keyboard:
	- turn off spotlight (replace with raycast app)
	- click on the "keyboard shortcuts..." button
		- set capslock to no action and globe to emojis
		- screenshots > double click > set to `shift + cmd + s`
	- select "modifier keys" tab on the left
	- select "spotlight" tab on the left and untoggle it all
- mouse:
	- max tracking speed
	- min scrolling speed
- trackpad:
	- high tracking speed
	- light click
	- tap to click
	- disable all shortcuts

# alternative window managers

- rectangle (most beginner friendly)
	- `brew install rectangle`
	- “repeated commands → cycle through 1/2, 1/3…”
	- don’t restore window size when unsnapped
- yabai (21k stars)
	- requires you to disable "system integrity protection"
	- https://github.com/koekeishiya/yabai
	- is based on: skhd - https://github.com/koekeishiya/skhd
- amethyst (14k stars)
	- doesn’t support multiple displays
	- https://github.com/ianyh/Amethyst
- slate (8k stars)
	- https://github.com/jigish/slate

# emulators

_linux emulators_

- asahi linux: https://asahilinux.org/
- lima: https://github.com/lima-vm/lima

_windows emulators_

- UTM (improved QEMU - better performance than virtualbox)
	- ✓ great free option
	- “Windows 11 ARM” virtualization
	- `brew install --cask utm`
	- download win11: https://mac.getutm.app/gallery/windows-11-arm
	- https://mac.getutm.app/
- virtualbox
	- ✓ great free option
	- “Windows 11 ARM” virtualization
	- `brew install --cask virtualbox`
	- https://www.virtualbox.org/
- parallels desktop
	- ✓ best paid option
	- “Windows 11 ARM” virtualization
	- https://www.parallels.com/eu/
- citrix
	- 𝙓 paid and noth worth it
	- desktop as a service (daas) / virtual desktop infrastructure (vdi)
	- alternatives: vnc connect, teamviewer, microsoft remote desktop, anydesk
	- https://www.citrix.com/
- vmware fusion
	- 𝙓 paid and noth worth it
	- “Windows 11 ARM” virtualization
	- https://store-us.vmware.com/fusion_buy_dual#GS
- crossover (improved WINE)
	- 𝙓 paid and noth worth it
	- mostly specialized on games
	- https://www.codeweavers.com/crossover/download

_macos keyboard shortcuts on windows and linux_

- https://github.com/gurbindersingh/mac-keybindings
- https://github.com/rbreaves/sorun
- https://github.com/rbreaves/kinto