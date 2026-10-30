## Solution for Andromeda Cheats: muOS Cheat Sync & Migration Script :video_game::arrows_counterclockwise:

A simple and robust PowerShell script designed to migrate, clean, and synchronize standard RetroArch-style cheat folders (`.cht`) into the exact directory structure required by **muOS (Andromeda / MustardOS)** and the **muOS Pickles** utility.

### :rocket: Why do you need this?
muOS requires cheats to be placed inside specific core folders under `MUOS/pickles/cheats/<core_name>/<rom_subpath>/` and demands that the `.cht` filename matches the exact ROM filename 100% to work correctly upon game startup. 

Manually reorganizing hundreds of files or fixing mismatched names/tags is painful. This script automates the entire process safely using strict matching logic to prevent false positives.

### :sparkles: Features
- **Core Mapping:** Automatically maps standard RetroArch system folders (e.g., *Nintendo - Game Boy Advance*) to their respective default muOS core folders (e.g., `mgba`).
- **Strict Matching:** Cleans region/revision tags (like `(USA)`, `[T-Eng]`, etc.) to ensure precise matching, avoiding accidental cross-matching between sequels or similarly named games (e.g., *Power Stone* vs. *Power Stone 2*).
- **Subfolder Mirroring:** Perfectly mirrors your ROM directory tree inside each core folder.
- **Safe Execution:** Uses non-destructive copying (`Copy-Item`), meaning your original cheat repository remains untouched.

### Project is still in Alpha stage...
