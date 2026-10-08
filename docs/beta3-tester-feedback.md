# Tester feedback on 0.2.0-beta.3

These are the problems and wishes a tester reported after testing 0.2.0-beta.3 on a **Pixhawk 6X** and a custom **Lectron Pi5 H7** (BMM350 compass) on 6 October 2026, and what changed in **0.2.0-beta.4**.

✅ fixed / added · 🟡 partly done (see the note) · ❌ not possible

Changes were checked on virtual ArduPilot and PX4 vehicles and on a SpeedyBee F405 V4 (ArduPilot). Items marked *needs hardware check* still have to be confirmed on a Pixhawk 6X / PX4 board.

## Bugs

| # | Report | Status in beta.4 |
|---|---|---|
| 1 | Setup Wizard *done* marks still lost after a reboot | ✅ The board is now recognised by its unique ID (or name / board ID) consistently, so the marks come back after a reboot or reconnect. |
| 2 | Popping out the MAVLink Inspector graphs gave an error | ✅ Charts now draw in pop-out windows. |
| 3 | **PX4:** magnetometer not detected (BMM350 on the Pi5 H7, and another board) although QGC and nsh see it | ✅ PX4 only stores a sensor's ID after it is calibrated. The app now also uses the "sensor present" flags, as QGC does, and lists such a sensor as *detected, not calibrated yet*. *Needs hardware check.* |
| 4 | **PX4:** compass calibration screen broken | ✅ PX4's progress messages per side are now read correctly; the side tiles and progress follow them. *Needs hardware check.* |
| 5 | **PX4:** baro calibration shown, but PX4 has none | ✅ Hidden on PX4; the tab is *Level · Gyro* there. |
| 6 | Messages still cover buttons | ✅ Pop-ups moved below the top bar and let clicks through; only their × is clickable. (The photos did not arrive; please report if it still happens.) |
| 7 | Logs: motor charts used SERVO1–8 even when the motors are on AUX (IO boards) | ✅ Motor outputs are found from the `SERVOn_FUNCTION` parameters in the log, on any output (RCOU, RCO2, RCO3). |
| 8 | Logs: *vibration per IMU* showed one IMU on a 3-IMU board | ✅ VIBE records are split per IMU. |
| 9 | Accelerometer calibration never reached *4 s still* because of normal IMU noise; on the 3D picture front and top were unclear | ✅ Stillness is judged on short averages, so normal noise is tolerated (tested with simulated noise). The 3D model shows **FRONT** and **TOP** labels. |
| 10 | Compass calibration (ArduPilot): side tiles stuck when sides are done out of order; quality card not updated after calibration | ✅ Side tiles follow the real progress per side; after a successful calibration the offsets are read back so the quality card updates. |
| 11 | BDShot firmware missing in *Choose firmware* | ✅ A **Build** choice for boards with variants, e.g. `Pixhawk6X` / `Pixhawk6X-bdshot`. |
| 12 | Inspector chart time window: 1 s, 10 s, 30 s, 1 min, 10 min | ✅ Window picker; the page also remembers the tab, preset and custom fields. |

## Setup Wizard

| # | Request | Status in beta.4 |
|---|---|---|
| 13 | Compass priority in the wizard when there are 2+ compasses | ✅ Shown in the Compass step. |
| 14 | Switches: allow the full / advanced channel options too | ✅ **All channel functions (advanced)** opens the complete `RCn_OPTION` list. |
| 15 | Battery before Failsafes; cell count and chemistry at the top of Battery | ✅ |
| 16 | Initial tune: an "only if you know what you're doing" warning | ✅ Warning added; hidden on PX4. |
| 17 | Extra passthrough mask: mark outputs that are already motors | ✅ Motor outputs are ticked and labelled (e.g. *6 = Motor 2*). |
| 18 | Safety switch step | ✅ New step: is there a safety button, and must it be pressed before the motors can spin (ArduPilot `BRD_SAFETY*`, PX4 `CBRK_IO_SAFETY`). |
| 19 | One button instead of *Write* and *Write & continue* | ✅ One **Write** button for everything pending. |
| 20 | After finishing, the wizard list didn't look finished | ✅ The Finish step lists every step as done / skipped / open with **Go**. |
| 21 | After a factory reset or new firmware, send the user to the Setup Wizard | ✅ After a flash or a reset to firmware defaults the app opens the wizard when the board reconnects. |
| 22 | "Factory reset" wording | ✅ Now **Reset to firmware defaults** and **Reset tuning to defaults (keep calibration & hardware)**. |
| 23 | Frame / PX4 airframe as a picture grid | ✅ Frames and airframes are picked from pictures. |
| 24 | PX4: hide ArduPilot-only steps; add the PX4 ESC protocol | ✅ Initial tune hidden on PX4; ESC protocol per output group (PWM / OneShot / DShot). |

## Health and tools

| # | Request | Status in beta.4 |
|---|---|---|
| 25 | Sensors: EKF2 vs EKF3 in use, IMU priority / used / unused | ✅ Estimator in the header; **EKF / priority** column per sensor. |
| 26 | Mag Tools only for advanced users, behind a confirmation | ✅ Moved to *For Advanced Users* and locked until **I understand the risks → Unlock**. |
| 27 | CompassMot: pictures of flipped / swapped props; live throttle, current, voltage graphs with interference | ✅ |
| 28 | Motors & Outputs: frame picture with assignments and directions; manual PWM output behind a confirmation | ✅ **Frame & motor wiring** card; manual sliders unlock per visit. |
| 29 | Separate Messages and MAVLink console; more nsh commands; an error explainer; copy selected text | ✅ **MAVLink Console** page (PX4) with grouped commands (`listener sensor_mag / baro / accel / gyro / gps`, `battery_status`, `system_power`, `work_queue status`…); **What does this mean?** box on Messages; **Copy** on both. |
| 30 | Pixhawk 6X peripheral / high-power rail power-cycle button | ❌ Neither ArduPilot nor PX4 offers a MAVLink command to switch only that rail; a reboot (or unplugging power) is the way. |

## Logs

| # | Request | Status in beta.4 |
|---|---|---|
| 31 | Replay with a map, like plot.ardupilot.org | ✅ **Map & replay** tab: flight path, Play 1×–32×, click to jump; charts, 3D and sticks follow. |
| 32 | Keep the opened log when switching pages | ✅ |
| 33 | Comparison: more data, comparable graphics | ✅ Flight figures, hover, vibration, motors and PID tracking side by side with % change; one-click comparison charts. |
| 34 | Log-based PID / filter / compass suggestions ("should be around …") with staging | ✅ **Suggested changes** in the Summary tab with **Stage**. Estimates from one flight: change in small steps. |
| 35 | IMU / baro / compass chip names in logs | ✅ *Sensors in this log* in the Summary tab. |
| 36 | Logs hard to use | ✅ A plain-language **Summary** tab opens first; the detailed checks moved under Charts. |
| 37 | AutoTune and similar scenario guides | ✅ Guides & Recipes: AutoTune, QuikTune, PX4 auto-tuning, Save Trim. |

## Layout and theme

| # | Request | Status in beta.4 |
|---|---|---|
| 38 | Logging and other sections under *For Advanced Users*; review the sidebar | ✅ Sidebar regrouped (Parameters, Filters, Mag Tools, Logs, Inspector, Messages, Console under *For Advanced Users*); on Safety & Failsafes, arming, logging and expert failsafes are in a collapsed *For advanced users* section. |
| 39 | Remove the Toprak dark / light themes; add QGC-like themes | ✅ **Ground station dark** (new default) and **Ground station light**. Saved Toprak settings switch over automatically. |
| 40 | Settings: empty space under the Language card | ✅ Two independent columns. |
| 41 | Overview: 3D vs horizon plus magnetic north; card size fixed when switching | ✅ Fixed-size attitude card with a compass rose. |
