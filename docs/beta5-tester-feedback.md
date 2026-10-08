# Tester feedback on 0.2.0-beta.5

These are the problems and wishes a tester reported after testing 0.2.0-beta.5 on a **Pixhawk 6C mini** and a **Lectron Pi5 H7** (ArduPilot and PX4) on 8 October 2026, and what changed in **0.2.0-beta.6**.

✅ fixed / added · 🟡 partly done (see the note) · ❓ needs more detail from the tester

Checked on virtual ArduPilot and PX4 vehicles. Items marked *needs hardware check* still have to be confirmed on the real boards.

## Bugs

| # | Report | Status in beta.6 |
|---|---|---|
| 1 | ArduPilot firmware flashing always timed out on the Lectron Pi5 H7 (`.apj` and `.bin`, local and stable), while a Pixhawk 6C mini worked | ✅ A custom board's bootloader can show up under its own USB name, which wasn't tried: after a few seconds every serial port is tried now. The erase wait is 90 s (2 MB H7 boards can take longer than 30 s). *Needs hardware check.* |
| 2 | After a reset to defaults (ArduPilot and PX4), wizard steps still looked done | ✅ After a reset or a flash, the wizard's marks for that board are cleared. On PX4 "already calibrated" is judged by the calibration offsets, not the sensor IDs (which PX4 can set without a calibration). |
| 3 | Accelerometer auto-capture never finished: "Hold still… 4 s" kept restarting | ✅ Only a real move (more than 15°) restarts the hold; and once the right side has been down for 8 s it is saved anyway. If ArduPilot doesn't ask for the next side, it is sent again. *Needs hardware check.* |
| 4 | PX4 compass calibration still fails | 🟡 Step-by-step instructions like QGroundControl, and every message PX4 sends during the calibration is shown. *Please send the last `[cal]` message PX4 shows when it fails.* |
| 5 | Accelerometer calibration "gone" and buzzer volume back to default after the LED step | ✅ *Undo* / *Revert to boot values* put back every setting changed since boot, including fresh calibration results. Calibration results are never reverted now, and a revert always asks first with the list of settings. |
| 6 | Battery settings from the wizard not applied (critical and arming voltage 0); Battery page showed 9 batteries | ✅ Saved cell voltages from an older version made the critical voltage invalid: fixed. Settings that appear only after a reboot are reported. Only batteries with a monitor set are shown. |
| 7 | *Battery 1 below minimum arming voltage* but the Battery tile was green | ✅ A tile turns amber when a PreArm message is about it; click any tile for the reasons. |
| 8 | The log replay couldn't be popped out | ✅ The window was blocked; it opens now. |

## Setup and calibration

| # | Request | Status in beta.6 |
|---|---|---|
| 9 | Compass priority before the calibration, with the reboot it needs | ✅ Priority first, with a note to write and reboot before calibrating. |
| 10 | Show whether level / gyro / baro were calibrated | ✅ Each shows when it was last calibrated (from this PC). |
| 11 | Radio calibration started without a receiver | ✅ Needs live sticks; otherwise it says why. |
| 12 | Show transmitter modes 1-2-3-4 | ✅ Stick mode card with both sticks live. |
| 13 | Switches: knobs and sliders, show where a function turns on | ✅ LOW / MID / HIGH zones with the live position for every channel with a function. |
| 14 | Battery voltage calibration only for analog monitors | ✅ Hidden for digital monitors (INA2xx, DroneCAN, SMBus, ESC). |
| 15 | No fence in the recommended first-setup failsafes | ✅ Removed (set a fence after drawing it on the Map). |
| 16 | Motor test only after outputs are assigned, written and rebooted | ✅ Motor test and Output test are locked until then, and say what is missing. |
| 17 | DShot-only options hidden with PWM; ESC calibration only with PWM / OneShot | ✅ |
| 18 | Receiver: show the active flight-mode slot | ✅ |
| 19 | Output buttons: just "FMU (AUX)" / "IO (MAIN)" | ✅ |
| 20 | Motor assignment wizard (PX4 and ArduPilot) | ✅ Four steps: outputs, write, reboot, test. |
| 21 | Buzzer volume on PX4 | ✅ PX4 has no buzzer volume setting (only on / off); the page says so. |
| 22 | Reset parameters from the wizard's first page, with confirmation steps | ✅ *Start from a clean vehicle*: save a backup, confirm, reset, reboot, start again. |
| 23 | ArduPilot compass calibration: per-side percentages not needed | ✅ |
| 24 | PID gains changed by a wrong click; a plain parameter list; Initial tune "Write 30 values" too easy to press | ✅ Gains are locked until *Edit gains*; *Parameter list* view; every write asks with the list of changes. |

## Pages

| # | Request | Status in beta.6 |
|---|---|---|
| 25 | MAVLink Inspector, Messages, Backup & Restore are not only for advanced users | ✅ Under *Vehicle*. |
| 26 | Inspector: chart a field without going to Plots | ✅ Live chart right under the message. |
| 27 | Messages panel: copy, save, clear | ✅ |
| 28 | Attitude: 3D and horizon together | ✅ Side by side. |
| 29 | Show the build variant (e.g. bdshot) | ✅ Badge next to the version. |
| 30 | Board capabilities from the board's documentation (UARTs, IMUs, compass, SD card…) | ✅ *Capabilities → Board hardware*, read from ArduPilot's board definition. |
| 31 | Search can't find sections inside pages; Ctrl+F | ✅ Sections are found and opened (e.g. "buzzer" → Peripherals › LEDs & buzzer); Ctrl+F opens the search. |
| 32 | Sensors: click a fault for the reason | ✅ |
| 33 | Ready-to-fly: clearer explanations (no RC, GPS, battery not connected / wrong cell count) | ✅ |

## Logs

| # | Request | Status in beta.6 |
|---|---|---|
| 34 | Vehicle size adjustable; position and height source | ✅ |
| 35 | Replay only a chosen time range | ✅ *Play only m:ss to m:ss*. |
| 36 | Log parameters: save all / changed; description on click | ✅ |
| 37 | System: internal errors (DRDY, SPI, SD, longest loop…) | ✅ *Internal problems* on the System tab. |
| 38 | Events: filter out repeating events | ✅ One chip per kind of event. |
| 39 | Clicking an event syncs the replay (±5 s) | ✅ |
| 40 | Compare: charts of both logs, switch logs, compare events | ✅ Charts on the Compare tab, *Swap A ↔ B*, events side by side. |

## Other

| # | Request | Status in beta.6 |
|---|---|---|
| 41 | Keep the source in its own (private) repository with a setup guide for a new computer | ✅ |
| 42 | "FAT32 default" (from the beta.4 list) | ❓ Still unclear where this belongs. |
