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

## Project is still in Alpha stage... Take in count that the margin of error is around 20%

# How-To: Automated RetroArch Cheat Synchronization for muOS

This guide explains how to use and customize the PowerShell script to automatically synchronize and filter RetroArch `.cht` files into the proper muOS Pickles folder structure (`pickles/cheats`).

The script features **Perfect Region Matching**, automatic **clean cheat prioritization** (avoiding utility tools like *Game Genie* or *GameShark*), and isolated system core mapping.

---

## Step 1: File Preparation

1. Place your PowerShell script (e.g., `Sync-Cheats.ps1`) and your batch launcher (`run.bat`) in a working directory on your computer.
2. Ensure you have your source RetroArch cheat files organized by system folders (e.g., `Nintendo - Game Boy Advance`, `Sega - Mega Drive - Genesis`).

---

## Step 2: Customizing Your Directories

Before running the script, you **must** update the root path variables at the very top of the PowerShell script to match your computer's directory layout.

Open `Sync-Cheats.ps1` in any text editor (like Notepad or VS Code) and modify the following lines:

```powershell
$romRoot = 'E:\ROMS'                  # Path to your main ROMs directory
$sourceCheatRoot = 'E:\Cheats_Originais' # Path to your raw/original RetroArch cheat folders
$destCheatRoot = 'E:\MUOS\pickles\cheats'  # Path to your muOS SD card pickles cheat destination
```

### What to change:
- **`$romRoot`**: Point this to the root folder where all your system ROM folders (`GBA`, `SFC`, `MD`, etc.) are located.
- **`$sourceCheatRoot`**: Point this to the folder where your unzipped RetroArch cheat files are stored (typically structured with full Libretro system names like `Nintendo - Game Boy Advance`).
- **`$destCheatRoot`**: Point this to your muOS target directory where the synchronized, clean cheat files will be generated.

---

## Step 3: Understanding Folder Mappings (If Your Folders Have Custom Names)

If your folder naming convention differs from standard Libretro or muOS defaults, you can adjust the translation bridges inside the script:

### 1. The Folder Bridge (`$folderBridge`)
This maps your short ROM folder names (`GBA`, `SFC`, etc.) to your source cheat folder names (`Nintendo - Game Boy Advance`, etc.):

```powershell
$folderBridge = @{
    'GBA'  = 'Nintendo - Game Boy Advance'
    'SFC'  = 'Nintendo - Super Nintendo Entertainment System'
    'MD'   = 'Sega - Mega Drive - Genesis'
    # Add or modify your custom folder names here
}
```

### 2. The Core Map (`$coreMap`)
This maps the source system folders directly to the specific muOS emulator core folder names required by your device:

```powershell
$coreMap = @{
    'Nintendo - Game Boy Advance'                    = 'mgba'
    'Nintendo - Super Nintendo Entertainment System'  = 'snes9x'
    'Sega - Mega Drive - Genesis'                    = 'genesis_plus_gx'
    # Adjust cores according to your muOS setup requirements
}
```

---

## Step 4: Running the Automation

1. Create a batch file named `run.bat` in the same folder as your PowerShell script with the following contents:

```cmd
@echo off
powershell -NoProfile -ExecutionPolicy Bypass -File "%~dp0Sync-Cheats.ps1"
pause
```

2. Double-click **`run.bat`** to execute the script.
3. The script will automatically:
   - Scan your ROM directories.
   - Match regions strictly (`USA`, `EUR`, `JP`, `WORLD`).
   - Prioritize clean cheat files over tools like *GameShark* or *Game Genie*.
   - Generate the final organized structure inside your muOS `pickles/cheats` path.
