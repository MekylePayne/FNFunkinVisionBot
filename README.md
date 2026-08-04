# FunkinVision is a high-performance, computer vision-based autoplay bot for rhythm games like Roblox Funky Friday, Ro-Beats, and OSUmania.

Instead of injecting code or reading game memory (which easily gets you banned), FunkinVision uses ultra-fast screen capture to read pixels on your screen and simulates hardware-level keyboard inputs with perfect, zero-delay timing.

PythonPlatformStatus

✨ Features
Zero-Latency Inputs: Bypasses Roblox's anti-cheat and the standard 50ms pydirectinput delay by using native 64-bit Windows SendInput hardware scan codes.
Precision Timing Queue: A built-in execution queue allows you to offset your timing by exact milliseconds. Perfect for compensating for visual lag or engine differences (e.g., OSUmania vs. FNF).
Long Note (Sustain) Support: Features a 15ms release buffer that bridges transparent pixel gaps in long note tails, preventing the bot from "machine-gunning" sustain notes.
Fast Jack/Double Note Support: Tuned to release just fast enough to hit rapid-fire jacks without merging them into a single held note.
Sleek Overlay UI: A transparent, click-through overlay showing a visual trigger line, live CPS counter, total click count, and current bot status.
Live MS Tuning: A built-in slider on the overlay allows you to adjust the input delay on the fly while the bot is actively playing.
🛠️ Technology Used
Screen Capture: mss (Manic Screen Shooter) - Captures specific screen regions in ~1 millisecond.
Input Simulation: ctypes + Windows SendInput API - Sends DirectX-compatible hardware scan codes directly to the OS kernel.
GUI: tkinter - Used for the lightweight, always-on-top transparent overlay.
Hotkeys: keyboard - Asynchronous global hotkey listener.
⌨️ Default Bindings
The bot is pre-configured for standard rhythm game layouts using Hardware Scan Codes.

Arrow	Key	Scan Code
Left	D	0x20
Down	F	0x21
Up	J	0x24
Right	K	0x25
Note: To change these, you will need to update the SCAN_CODES dictionary in the script with the appropriate DirectX scan codes for your desired keys.

🚀 Installation & Setup
Ensure you have Python 3.8+ installed.
Install the required dependencies via Command Prompt:
pip install mss keyboard pydirectinput
Run the bot:
bash

python fnf_bot.py
🎮 Hotkeys
Key
Action
F7	Hide / Show the UI Overlay
F8	Start / Pause the Bot
F9	Emergency Kill Switch (Safely exits the app)

⚙️ Best Optimizations (How to get 100% Accuracy)
To get the most out of FunkinVision, you need to optimize your game's visual settings. Computer vision relies on contrast and clarity.

Pitch Black Background:
The bot checks if a pixel is "not black" (RGB > 30). A pure black background guarantees zero false positives from stage lighting or character animations. If your game doesn't support a black background, you will need to adjust the is_not_black function to look for specific RGB color ranges.
Trigger Line Placement:
The calibration tool places the trigger line below the arrows. This is intentional! If you place it directly on the arrow, the arrow's "confirmation glow" when hit will cause the bot to hold the key forever. Keep it slightly below the targets.
Increase Scroll Speed:
If you are missing fast "jacks" (two of the same notes right next to each other), increase your in-game scroll speed. Faster scroll speeds stretch the visual gap between the notes on your screen, giving the bot the few extra milliseconds it needs to release the first note and press the second one.
Live MS Tuning:
Use the slider on the right side of the overlay! If you notice you are getting "Goods" instead of "Sicks", drag the slider.
Hitting too early? Increase the MS (e.g., to 45 or 50).
Hitting too late? Decrease the MS (e.g., to 30).
OSUmania generally requires a higher delay (~90ms) than Roblox FNF (~40ms).
📜 License
This project is open-source. Feel free to fork, modify, and distribute. If you make a cool improvement, feel free to submit a pull request!
