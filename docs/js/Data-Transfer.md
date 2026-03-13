# Transferring Your Data

This guide explains how to move Sayori's memories (your save data) between different devices.

---

## PC to PC Transfer

This is for moving your save data from one computer to another.

### 1. Locate and Back Up Your Data
First, you need to find the folder containing Sayori's memories on your original PC.

-   **Windows:** Press `Windows Key + R`, type `%APPDATA%/RenPy`, and press Enter.
-   **macOS:** In Finder, select "Go" > "Go to Folder..." and type `~/Library/RenPy`.
-   **Linux:** The folder is at `~/.renpy`.

Inside that `RenPy` folder, find the directory for the mod (e.g., `JustSayori`) and copy it to a safe place like a USB drive.

### 2. Restore Your Data
On your new PC, install the mod first. Then, navigate to the same `RenPy` directory and paste the folder you backed up, replacing the existing one if prompted.

---

## Android to PC Transfer

1.  On your Android device, use the **"Export Persistent"** button in the launcher. This creates a `.zip` file with your save data.
2.  Transfer this `.zip` file to your PC and unzip it. You will get a file named `persistent`.
3.  On your PC, find the mod's save data folder as described in the "PC to PC Transfer" section. Copy the `persistent` file into that folder, replacing the old one.
4.  Start the game.

---

## PC to Android Transfer

1.  On your PC, locate your `persistent` file inside the mod's save data folder (see "PC to PC Transfer" section).
2.  Create a `.zip` archive containing **only** that `persistent` file.
3.  Transfer this `.zip` file to your Android device.
4.  In the Android launcher, use the **"Import Persistent"** button and select the `.zip` file you created.
5.  Start the game to confirm your memories are loaded.
