i hate the workspace switcher. its gone now.
this is a certified tickbox mod.

thank you juandamian18 for making the media player


## step-by-step installation (recommended, user-local)

### 1. clone the repository

### 2. configure the build directory
```bash
meson setup build --prefix=/usr
```
if `build` already exists:
```bash
meson setup build --reconfigure --prefix=/usr
```

### 3. build
```bash
ninja -C build
```
ignore warnings and chill

### 4. install just for your user (recommended)
so that the system doesnt get angy, and also keeps a backup just in case:
```bash
set -euo pipefail
mkdir -p "$HOME/.local/bin" "$HOME/.local/bin/backups"
if [ -f "$HOME/.local/bin/io.elementary.dock" ]; then
  ts="$(date +%Y%m%d-%H%M%S)"
  cp -a "$HOME/.local/bin/io.elementary.dock" \
    "$HOME/.local/bin/backups/io.elementary.dock.$ts"
fi
install -m 0755 build/src/io.elementary.dock "$HOME/.local/bin/io.elementary.dock"
```

### 5. kick the dock
```bash
pkill -f '^io.elementary.dock$' || true
```
it'll come back on its own. probably.

### 6. make sure yours is the one actually running
```bash
which io.elementary.dock
```
should say:
```text
/home/your-user/.local/bin/io.elementary.dock
```

## global installation (optional)
if you like to live dangerously:
```bash
sudo ninja -C build install
pkill -f '^io.elementary.dock$' || true
```
note: this nukes the package-installed binary and a system update might just nuke yours right back.
