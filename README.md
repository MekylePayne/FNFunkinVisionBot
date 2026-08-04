# FNFunkinVisionBot - Zero-Delay FNF & OSUmania Autoplayer
FunkinVision is a high-performance, computer vision-based autoplay bot for rhythm games like Roblox Funky Friday, Ro-Beats, and OSUmania.

Instead of injecting code or reading game memory (which easily gets you banned), FunkinVision uses ultra-fast screen capture to read pixels on your screen and simulates hardware-level keyboard inputs with perfect, zero-delay timing. This method absolutely cannot get you banned, since it's client-side only! (Not even OSU!Mania detects)

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=flat&logo=python)
![Platform](https://img.shields.io/badge/Platform-Windows-grey?style=flat)
![Status](https://img.shields.io/badge/Status-Beta-brightgreen?style=flat)

Bot Working: (Click to open YouTube link)
[![FNFunkinVisionBot Showcase!](https://img.youtube.com/vi/FfSp4aKSKhQ/maxresdefault.jpg)](https://www.youtube.com/watch?v=FfSp4aKSKhQ)
P.S: I've fixed the MS Counter overlapping the CPS.

---
## Features
- Zero-Latency Inputs: Bypasses Roblox's anti-cheat and the standard 50ms pydirectinput delay by using native 64-bit Windows SendInput hardware scan codes.
- Precision Timing Queue: A built-in execution queue allows you to offset your timing by exact milliseconds. Perfect for compensating for visual lag or engine differences (e.g., OSUmania vs. FNF).
- Long Note (Sustain) Support: Features a 15ms release buffer that bridges transparent pixel gaps in long note tails, preventing the bot from "machine-gunning" sustain notes.
- Fast Jack/Double Note Support: Tuned to release just fast enough to hit rapid-fire jacks without merging them into a single held note.
- Sleek Overlay UI: A transparent, click-through overlay showing a visual trigger line, live CPS counter, total click count, and current bot status.

## Technology Used
- Screen Capture: mss (Manic Screen Shooter) - Captures specific screen regions in ~1 millisecond.
- Input Simulation: ctypes + Windows SendInput API - Sends DirectX-compatible hardware scan codes directly to the OS kernel.
- GUI: tkinter - Used for the lightweight, always-on-top transparent overlay.
- Hotkeys: keyboard - Asynchronous global hotkey listener.

## Bindings
- Left: D (0x20)
- Down: F (0x21)
- Up: J (0x24)
- Right: K (0x25)
>Note: To change these, you will need to update the SCAN_CODES dictionary in the script with the appropriate DirectX scan codes for your binding keys. Rather, keep the current bindings, and change your game's bindings.
---
# Installation & Setup
1. Ensure you have Python 3.8+ installed via PATH.
2. Install the required dependencies via Command Prompt:

`pip install mss keyboard pydirectinput`

3. Run the bot by double-clicking the .pyw file. Thats all, for now.
---
## Current Hotkeys
- F7	Hide / Show the UI Overlay
- F8	Start / Pause the Bot
- F9	Emergency Kill Switch (Safely exits the app)
---
# Best Optimizations (How to get 95-100% Accuracy)
To get the most out of FunkinVision, you need to optimize your game's visual settings. Computer vision relies on contrast and clarity.

### Pitch Black Background:
- The bot checks if a pixel is "not black" (RGB > 30). A pure black background guarantees zero false positives from stage lighting or character animations. If your game doesn't support a black background, you will need to adjust the is_not_black function to look for specific RGB color ranges. 
>Psych Engine and Roblox-based engines have underlay transparency options. Look into your settings, and change its setting to 0 for zero transparency. OSU!mania's background can be set to pitch black when loading in a song.

### Remove Splash Notes:
- For the best accuracy and no key ghosting. Remove splash note registers. This should be on every engine/game there is. If the trigger detects any colour that is not black, it will trigger, which screws the rhythm.
>If you're on OSU!Mania, get a simple skin that hardly has effects and one single colour for notes. (For example, white circle notes)

### Trigger Line Placement:
The calibration tool places the trigger line below the arrows. This is intentional! If you place it directly on the arrow, the arrow's "confirmation glow" when hit will cause the bot to hold the key forever. Keep it slightly below the targets.
>For the default config, you will require a 1080P screen. Read at the end on how to set up on your screen.

### (IMPORTANT) Increase Scroll Speed:
If you are missing fast "jacks" (two of the same notes right next to each other), increase your in-game scroll speed. Faster scroll speeds stretch the visual gap between the notes on your screen, giving the bot the few extra milliseconds it needs to release the first note and press the second one.
>DO NOT INCREASE TO UNGODLY SPEEDS, or else accuracy will be ass.

### (WIP) Live MS Tuning:
Use the slider on the right side of the overlay! If you notice you are getting "Goods" instead of "Sicks", drag the slider.
Hitting too early? Increase the MS (e.g., to 45 or 50).
Hitting too late? Decrease the MS (e.g., to 30).
>OSU!mania generally requires a higher delay (~90ms) than Roblox FNF (~40ms).
---
# How to tune the Trigger Points
1. Load into your game/engine (Use Funky Friday on Roblox since it was basically meant for it lol.) Play a hard song and let it run.
2. Double-click the .pyw file; a config overlay will show.
3. Go back into your game window, and hold down a note. You will notice that there's a glow; you will need to hover your mouse RIGHT underneath that glow (not touching the glow; it must be black). Then press 1, you will see a red circle showing confirmation.
4. Repeat for other keys.
5. Once done, you will see the straight line with an MS config. Leave the MS for now, and test the script.
6. Press F8; you will see the bot working. Note that the script works best with the vanilla FNF notes, or circles.

If you want to reset your config, you can delete the .config file that the .pyw file is in. Then double-click again and reconfigure.
>If the accuracy is bad, press F8 again and mess with the MS counter until the latency aligns just right. If you're still confused on how to set up, contact me on Discord (MekylePain).
---
# Known Issues:
- Pausing a running session will freeze the script while it's still running. You will need to go inside your task manager and terminate python32 or python. Have no idea what's causing it.
- I've only tested this bot on a 60hz 1080p monitor; I have no clue what will happen on higher-end monitors. I did add an MS configurator on the line itself so you can change respectively.
- YOU WILL NEED ATLEAST 60FPS on any engine you run. You can also uncap the fps for better accuracy. I suggest at least 75+ fps for best accuracy. (I used 240FPS, which is the max supported on Roblox)
---
This project is open-source. Feel free to fork, modify, and distribute. If you make a cool improvement, feel free to submit a pull request! Hell, even sell it, I don't care :P

`If you appreciate my work, please feel free to add me on Discord (MekylePain). I would love to play with you!`
