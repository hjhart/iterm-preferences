# Why

We use quite a few machines, and we only want to make changes to iTerm preferences once – and have them sync across all of our machines!

# What

These iTerm preferences are opinionated, and are configured as such:

* Does not copy text on selection
* Dim affects only text, not background. 
* Hides the scroll bar and the window number
* Do not show per-pane title bar when in split pane mode

# How

iTerm loads an XML file and will happily load configuration. 

When you modify the configuration, it will save it as a binary object. This binary object can be converted back to a XML file (which is easily diff-able) by running the `convert_to_xml.sh` script.

**Beware** The directions below will blow away your current configuration.

1. Symlink your configuration to the configuration in this file

```
cd ~/workspace/
git clone github.com:hjhart/iterm-preferences.git
rm  ~/Library/Preferences/com.googlecode.iterm2.plist
ln -s ~/workspace/iterm-preferences/com.googlecode.iterm2.plist ~/Library/Preferences/com.googlecode.iterm2.plist
```

2. Make changes to your configuration in iTerm2. You'll need to close iTerm2 at this point for the configuration to save.

3. Check in your preferences for iTerm

```
cd ~/workspace/iterm-preferences
./convert_to_xml.sh
git diff
```

You should see the changes that you made at this point as a reasonable delta in git. You can check this file in at that point and sync it across all of your machines.

# Developing

According to [this](http://apple.stackexchange.com/questions/111534/iterm2-doesnt-read-com-googlecode-iterm2-plist?answertab=active#tab-top) article, preferences are cached in iTerm2. When you are making changes that need preferences to be reloaded make sure you follow instructions in [this answer](http://apple.stackexchange.com/a/111559)
