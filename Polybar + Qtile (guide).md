# Quick guide to setting up Qtile with Polybar as main bar

### This little guide shows how to get rid of the Qtile bar and instead use Polybar. Its not the best solution, but it works for me.

### Polybar config:
#### To enable system tray, and move it by x to right
```
tray-position = center
tray-offset-x = 500
```

### Create a file in polybar config directory:
#### launch.sh - which could be standard launch script from official polybar wiki
```
#!/bin/bash

# Terminate already running bar instances
#killall -q polybar
# If all your bars have ipc enabled, you can also use
polybar-msg cmd quit

# Launch Polybar, using default config location ~/.config/polybar/config.ini
#echo "---" | tee -a /tmp/polybar1.log /tmp/polybar2.log
polybar bar1 2>&1 | tee -a /tmp/polybar.log & disown

echo "Polybar launched..."
```
### REMEMBER TO MAKE IT EXECUTEABLE: chmod +x lauch.sh

### Qtile config:
#### To "Reload the config" key add lazy.spawn with path to launch.sh:
```
Original: Key([mod, "control"], desc="Reload the config"),
Replace with: Key([mod, "control"], "r", lazy.reload_config(), lazy.spawn("~/.config/polybar/launch.sh"), desc="Reload the config"),
```
#### Delete everything in screens
```
screens = [
    Screen()
]
```
