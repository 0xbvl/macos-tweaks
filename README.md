# configure pmset
```
sudo pmset -a destroyfvkeyonstandby 1
sudo pmset -a hibernatemode 0
sudo pmset -a powernap 0
sudo pmset -a standby 0
sudo pmset -a standbydelay 0
sudo pmset -a autopoweroff 0
sudo pmset -a sms 0
sudo pmset -a womp 0
```

# configure firewall
```
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --setglobalstate on
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --setloggingmode on
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --setstealthmode on
socketfilter - prevent auto
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --setallowsigned off
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --setallowsignedapp off
sudo pkill -HUP socketfilterfw
```

# install homebrew & packages
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew install ccleaner firefox funter keka libreoffice macfuse macs-fan-control onyx telegram tor-browser veracrypt vlc
brew install nextdns/tap/nextdns
optional:
brew install balenaetcher spotify visual-studio-code
brew install --cask transmission
```

# setup nextdns
```
sudo nextdns install
sudo nextdns start
sudo nextdns activate
sudo nextdns run
sudo nextdns config set -hardened-privacy=true
sudo nextdns config set -report-client-info=true
sudo nextdns config set -auto-activate=true
```


# adjust launchpad
```
defaults write com.apple.dock springboard-columns -int 8;
defaults write com.apple.dock springboard-rows -int 6;
defaults write com.apple.dock ResetLaunchPad -bool TRUE;killall Dock
```

# clear finder preferences
```
defaults delete ~/Library/Preferences/com.apple.finder.plist FXDesktopVolumePositions
defaults delete ~/Library/Preferences/com.apple.finder.plist FXRecentFolders
defaults delete ~/Library/Preferences/com.apple.finder.plist RecentMoveAndCopyDestinations
defaults delete ~/Library/Preferences/com.apple.finder.plist RecentSearches
defaults delete ~/Library/Preferences/com.apple.finder.plist SGTRecentFileSearches
```

# disable show recent apps in dock
```
defaults write com.apple.dock show-recents -bool FALSE
```

# show all filename extension
```
defaults write NSGlobalDomain AppleShowAllExtensions -bool true
```

# expose hidden files
```
defaults write com.apple.finder AppleShowAllFiles -bool true
```

# expose library folder in finder
```
chflags nohidden ~/Library
```

# don't default to saving documents to iCloud
```
defaults write NSGlobalDomain NSDocumentSaveNewDocumentsToCloud -bool false
```

# disable crash reporter
```
defaults write com.apple.CrashReporter DialogType none
```

# disable bonjour advertisements
```
sudo defaults write /Library/Preferences/com.apple.mDNSResponder.plist NoMulticastAdvertisements -bool YES
```

# disable captive portal
```
sudo defaults write /Library/Preferences/SystemConfiguration/com.apple.captive.control.plist Active -bool false
```

# disable remote apple events
```
sudo systemsetup -setremoteappleevents off
```

# avoid Creating .DS_Store Files On Network Or USB Volumes
```
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool true
defaults write com.apple.desktopservices DSDontWriteUSBStores -bool true
```

# disable ARD Agent and Remove Access Privileges for All Users
```
sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -deactivate -configure -access -off
```

# disable remote login
```
sudo launchctl unload -w /System/Library/LaunchDaemons/ssh.plist
```

# remove Apple Remote Desktop Settings
```
sudo rm -rf /var/db/RemoteManagement ; \
sudo defaults delete /Library/Preferences/com.apple.RemoteDesktop.plist ; \
defaults delete ~/Library/Preferences/com.apple.RemoteDesktop.plist ; \
sudo rm -r /Library/Application\ Support/Apple/Remote\ Desktop/ ; \
rm -r ~/Library/Application\ Support/Remote\ Desktop/ ; \
rm -r ~/Library/Containers/com.apple.RemoteDesktop
```

# uninstall Google Update
```
~/Library/Google/GoogleSoftwareUpdate/GoogleSoftwareUpdate.bundle/Contents/Resources/ksinstall --nuke
```

# disable sidecar
```
defaults delete com.apple.sidecar.display
```

# show External, Internal, Removable Media and Network Volumes
```
defaults write com.apple.finder ShowExternalHardDrivesOnDesktop -bool true && \
defaults write com.apple.finder ShowHardDrivesOnDesktop -bool true && \
defaults write com.apple.finder ShowRemovableMediaOnDesktop -bool true && \
defaults write com.apple.finder ShowMountedServersOnDesktop -bool true && \
```

# show Full Path in Finder Title
```
defaults write com.apple.finder _FXShowPosixPathInTitle -bool true
```

# show Path Bar and Status Bar
```
defaults write com.apple.finder ShowPathbar -bool true
defaults write com.apple.finder ShowStatusBar -bool true
```

# disable startup sound
```
sudo nvram SystemAudioVolume=0
```

# check for macOS updates more often
```
defaults write com.apple.SoftwareUpdate ScheduleFrequency -int 1
```

# always show scrollbars
```
defaults write NSGlobalDomain AppleShowScrollBars -string “Always”
```

# disable opening and closing window animations
```
defaults write NSGlobalDomain NSAutomaticWindowAnimationsEnabled -bool false
```

# disable natural scrolling
```
defaults write NSGlobalDomain com.apple.swipescrolldirection -bool false
```

# disable all animations - finder
```
defaults write com.apple.finder DisableAllAnimations -bool true
```

# display full posix path as finder window tile
```
defaults write com.apple.finder _FXShowPosixPathInTitle -bool true
```

# set the icon size of dock items to 35px
```
defaults write com.apple.dock tilesize -int 35
```
# remove animation when hiding/showing dock
```
defaults write com.apple.dock autohide-time-modifier -float 0
```
# enable 2d dock
```
defaults write com.apple.dock no-glass -bool true
```
# disable safari thumbnail cache
```
defaults write com.apple.Safari DebugSnapshotsUpdatePolicy -int 2
```
# remove useless icons from safari bookmarks bar
```
defaults write com.apple.Safari ProxiesInBookmarksBar “()”
```
# disable send and reply animations in mail
```
defaults write com.apple.mail DisableReplyAnimations -bool true
defaults write com.apple.mail DisableSendAnimations -bool true
```

# Prevent Time Machine from prompting to use new hard drives as backup volume
```
defaults write com.apple.TimeMachine DoNotOfferNewDisksForBackup -bool true
```

# speedup mission control animations
```
defaults write com.apple.dock expose-animation-duration -float 0.1
```

# clear DNS cache
```
sudo dscacheutil -flushcache && \
sudo killall -HUP mDNSResponder
purge memory cache
sudo purge
```

# Terminal (choose one) bash or zsh
### BASH
```
brew install bash && \
echo $(brew --prefix)/bin/bash | sudo tee -a /etc/shells && \
chsh -s $(brew --prefix)/bin/bash
```

### ZSH
```
brew install zsh && \
sudo sh -c 'echo $(brew --prefix)/bin/zsh >> /etc/shells' && \
chsh -s $(brew --prefix)/bin/zsh
```
