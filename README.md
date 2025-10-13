# zsh-screensaver
A customizable terminal screensaver for ZSH that activates after a period of inactivity, featuring multiple display styles including animated GIFs.

![ZSH](https://img.shields.io/badge/ZSH-Screensaver-blue?logo=gnu-bash&logoColor=white)
![Shell](https://img.shields.io/badge/Shell-ZSH-orange)
![Platform](https://img.shields.io/badge/Platform-macOS%20%7C%20Linux-lightgrey)
![License](https://img.shields.io/badge/License-MIT-green)
![Dependencies](https://img.shields.io/badge/Dependencies-Optional-yellow)

## Features
🕐 Auto-activation - Triggers after configurable idle time (default: 5 minutes)

🎨 Multiple Styles - Choose from banner, fancy overlay, or animated GIF screensavers

🖼️ GIF Support - Random animated GIFs from curated collection

⌨️ Smart Detection - Tracks all terminal activity (typing, commands, navigation)

🔄 Seamless Restoration - Press any key to return to your exact terminal state (Ctrl+C, then any key for GIFs)

⚙️ Easy Control - Enable/disable/test with simple commands

## Installation
  - download `.screensaver` and move it to `/home/$USER/.screensaver`.
  - add the following:
    
    ```bash
    source /home/$USER/.screensaver
    ```
    at the end of your `~/.zshrc` file.

2. Install Dependencies (Required for GIF terminal screensavers): [gif-for-cli](https://github.com/google/gif-for-cli)

3. Reload Configuration

```bash
source ~/.zshrc
```

## Configuration
### Basic Settings

```bash
# Set timeout (in seconds)
SCREENSAVER_TIMEOUT=300  # 5 minutes

# Enable/disable screensaver
SCREENSAVER_ENABLED=true
```

### Screensaver Styles
The script includes multiple screensaver styles. Change the `show_gif_overlay` call in `check_screensaver()` to use different styles:

- **show_banner_overlay** - Minimal red banner at top
- **show_fancy_overlay** - Centered box with semi-transparent background
- **show_screensaver_overlay** - Blue banner overlay
- **show_gif_overlay** - Random animated GIF display from user-defined array

## Usage

### Control Commands

| Command |	Description |
| :------ | :---------: |
| `ss-on`	| Enable screensaver |
| `ss-off`| 	Disable screensaver |
| `ss-test`| 	Test screensaver immediately |

## Customization

### Adding GIFs
Edit the gifs array in `show_gif_overlay()` to add your own Tenor GIF URLs:

bash
```
local gifs=(
    "https://tenor.com/view/your-gif-url-here"
    "https://tenor.com/view/another-gif-here"
)
```

### Changing Timeout
Modify the SCREENSAVER_TIMEOUT variable:

```bash
# 10 minute timeout
SCREENSAVER_TIMEOUT=600

# 2 minute timeout  
SCREENSAVER_TIMEOUT=120
```

### Creating Custom Styles
Add new display functions following the pattern:

```bash
show_custom_overlay() {
    printf '\033[s\033[?25l'  # Save cursor, hide it
    # Your display logic here
    read -s -k  # Wait for any key
    printf '\033[u\033[?25h'  # Restore cursor
}
```

## Technical Details
- Uses ZSH hooks (preexec, precmd) for activity detection
- Implements terminal escape sequences for overlay display
- Preserves terminal state using alternative buffer
- Background process management for GIF playback
- Cross-platform compatible (macOS, Linux)

### Activity monitoring graph

<img width="500" height="800" alt="image" src="https://github.com/user-attachments/assets/1bd0a7c9-e612-4937-bab7-eb7e4dd531c0" />

## Troubleshooting

### GIFs Not Displaying
1. Ensure `gif-for-cli` is installed.
2. Check internet connection for GIF loading.

### Screensaver Not Activating
1. Verify `SCREENSAVER_ENABLED=true`.
2. Check that hooks are properly loaded in zsh.

### Flickering with GIFs
1. The script automatically reduces dimensions to prevent terminal flicker.
2. Uses conservative sizing for stable playback.

## License
Free to use and modify. Feel free to contribute improvements!
