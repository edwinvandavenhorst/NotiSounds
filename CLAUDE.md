# CLAUDE.md — NotiSounds

## Working directory
All source editing, building, and testing happens from:
```
~/Documents/Claude/NotiSoundsApp/
```

## Build & install
```bash
cd ~/Documents/Claude/NotiSoundsApp

# Compile, sign (ad-hoc), install to /Applications, relaunch
swiftc -framework Cocoa -O main.swift \
  -o build/NotiSounds.app/Contents/MacOS/NotiSounds
codesign --force --sign - build/NotiSounds.app
pkill -x NotiSounds 2>/dev/null || true
sleep 0.3
rm -rf /Applications/NotiSounds.app
cp -r build/NotiSounds.app /Applications/
open /Applications/NotiSounds.app
```

**Important:** always `rm -rf /Applications/NotiSounds.app` before `cp -r`.
`cp -r src /Applications/ExistingApp.app` nests the bundle instead of replacing it.

## Version control workflow
GitHub is the version tracker: **github.com/edwinvandavenhorst/NotiSounds**

After every meaningful change:
```bash
cd ~/Documents/Claude/NotiSoundsApp
git add -p          # or git add <specific files>
git commit -m "..."
git push
```

## App structure
All Swift source lives in a single file: `main.swift`
- `ToggleSwitch`          — custom CoreGraphics toggle (replaces NSSwitch)
- `ContentViewController` — dropdown panel UI
- `AboutWindowController` — About window
- `AppDelegate`           — status item, panel, audio, login item

## Key commands
```bash
notif-sounds status   # check alert volume from terminal
notif-sounds off      # mute notifications
notif-sounds on       # restore
```

## Regenerate icon
```bash
swift make_icns.swift   # rewrites icons/AppIcon.icns + iconset
# then rebuild the app to bundle the new icon
```
