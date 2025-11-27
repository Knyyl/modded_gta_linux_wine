# Running modded/pirated GTA V under Linux

This guide explains how to run GTA (modded, pirated) on **Linux** using **Bottles (Flatpak)**, **Wine-Staging 10.19**, and  **Ultimate ASI Loader (dinput8.dll)**.
You can set up everything yourself *or* use the provided Wine prefix. 

---

## Tested on this config

* Arch Linux (x86_64)
* Bottles (Flatpak)
* “Gaming” Bottle (Wine Staging 10.19)
* Ultimate ASI Loader
* Your GTA installation directory
* Sept. 27 2025

---

## Method 1: Create and Configure the Bottle (Recommended)

### 1. Create a Gaming Bottle

1. Open **Bottles**
2. Create a new **Gaming** bottle
3. Wait until it finishes setting up

### 2. Locate the Bottle’s Wine Prefix

Bottles stores prefixes under:

```
~/.var/app/com.usebottles.bottles/data/bottles/bottles/<your-bottle-name>/
```


## Method 2: Use the Provided Wine Prefix

If you want to try it with mine:

Place it reasonably, so you can find it easyly in case you loose the path

### 3. Install Dependencies
Enter your WINEPREFIX
```
export WINEPREFIX="/home/youruser/.var/app/com.usebottles.bottles/data/bottles/bottles/your-bottle-name"
```
and run these
```
winetricks d3dcompiler_43 d3dx9 d3dx10 dinput8 xinput
winetricks dotnet48
winetricks vcrun2019 vcrun2015
winetricks d3dcompiler_43 d3dx9_43 dinput8 xinput
winetricks d3dx11_43
winetricks d3dx9 d3dx10 d3dx11 dxvk
```
Even if you see errors, try if it worked at the end. Were practially bombing the prefix with required packages, without bloating it *too* hard

### 4. Install Ultimate ASI Loader

Download the latest release and place **dinput8.dll** (win64) inside your GTA game root folder.
→ [Ultimate ASI Loader](https://github.com/ThirteenAG/Ultimate-ASI-Loader/releases])
Alternatively, you can try to use other ones, such as the OpenIV asi loader, but revert back to this one if it fails.


## ▶Launching the Game

Creating the launch script

**launch-gta.sh**

```bash
#!/bin/bash
export WINEPREFIX="<path-to-your-just-created-prefix>"
export WINEDLLOVERRIDES="dinput8=n,b"

cd "<path-to-your-gta-root-directory>"
wine GTA.exe
```

Make it executable:

```bash
chmod +x launch-gta.sh
```

Run it:

```bash
./launch-gta.sh
```

GTA should start without issues — mods, ASI scripts, and even pirated copies (for testing purposes obviously) work as well.

---

##  Done!

Enjoy :3


