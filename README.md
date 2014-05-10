# Why

We use quite a few machines, and we only want to make changes to iTerm preferences once – and have them sync across all of our machines!

# What

These iTerm preferences are opinionated, and are configured as such:

* Dark solarized theme
* Hides the scroll bar and the window number
* Use the same current directory when opening a new tab or window
* Does not insert last newline on paste (to not accidentally execute commands)
* Flashing Bell instead of audio bell
* Clearer selections in solarized theme
* Does not copy text on selection
* Background dimming affects only text, not background. 
* Do not show per-pane title bar when in split pane mode
* Uses a blinking vertical bar for a cursor

# Installation

iTerm loads an XML file and will happily load configuration. 

When you modify the configuration, it will save it as a binary object. This binary object can be converted back to a XML file (which is easily diff-able) by running the `convert_preferences_from_binary_to_xml.sh` script.

**Beware** The directions below will blow away your current configuration.

1. Close iTerm and open up Terminal

2. Symlink your configuration to the git repository

```
killall cfprefsd     # This will get rid of cached settings
cd ~/workspace/
git clone https://github.com/hjhart/iterm-preferences.git
rm  ~/Library/Preferences/com.googlecode.iterm2.plist
ln -s ~/workspace/iterm-preferences/com.googlecode.iterm2.plist ~/Library/Preferences/com.googlecode.iterm2.plist
```

3. Open up iTerm and make some changes to your configuration. You'll need to close iTerm2 at this point for the configuration to save.

4. Checking in your preferences for iTerm

```
cd ~/workspace/iterm-preferences
./convert_preferences_from_binary_to_xml.sh
git diff
```

You should see the changes that you made at this point as a reasonable delta in git. You can check this file in at that point and sync it across all of your machines.

# Updating

After pulling in new changes from git, make sure you exit out of iTerm, open up Terminal and run `killall cfprefsd`. This will ensure that the cached configurations get unloaded. 

# Developing

According to [this](http://apple.stackexchange.com/questions/111534/iterm2-doesnt-read-com-googlecode-iterm2-plist?answertab=active#tab-top) article, preferences are cached in iTerm2. When you are making changes that need preferences to be reloaded make sure you follow instructions in [this answer](http://apple.stackexchange.com/a/111559)
