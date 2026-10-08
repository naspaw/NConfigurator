# Tester feedback on the first version (0.2.0-beta.2)

These are the problems and wishes a tester reported after testing 0.2.0-beta.2 on a real flight controller (SpeedyBee F405 V4, ArduPilot 4.7.1) on 5 October 2026, and what changed in **0.2.0-beta.3**.

✅ fixed / added · 🟡 partly done (see the note)

## Bugs

| # | Report | Status in beta.3 |
|---|---|---|
| 1 | Clicking **Reboot** while disconnecting reboots straight away and the app reconnects | ✅ The disconnect dialog offers **Reboot & disconnect**: it reboots and stays disconnected. |
| 2 | The app sometimes crashed after a **factory reset** | 🟡 Not reproduced. A page that fails now shows the error with **Try again** instead of a blank window. Please report the shown error if it happens. |
| 3 | **Setup Wizard:** steps marked done just by visiting them; after a reboot they showed as not done | ✅ Explicit **Mark done** / **Skip this step**, remembered per board. Steps that are already set on the vehicle show **Looks done**. |
| 4 | **RCOUT channels** did not match the motor outputs on boards with an IO co-processor | ✅ The two output groups (IO and FMU) were overwriting each other. Outputs are now named **MAIN n / AUX n** as printed on the board. |
| 5 | **PX4:** the frame step applied a quadrotor without offering a choice | ✅ Airframe picker (quad, hexa, octo, coaxial, plane, flying wing, VTOL, rover) or any `SYS_AUTOSTART` number. |
| 6 | Clicking the map's **Leaflet** link opened the website inside the app with no way back | ✅ Links open in the web browser. |
| 7 | **Compass calibration** looked unstable or showed errors | 🟡 ArduPilot restarts a failed fit by itself; the app now shows the attempt and **why** it failed (bad orientation, radius, offsets…) with what to do, lets you pick compasses and the fit, and offers **Retry with relaxed fit**. Needs more testing on hardware. |

## Setup and calibration

| # | Request | Status in beta.3 |
|---|---|---|
| 8 | A way to turn warnings off; PreArm messages covering buttons on setup pages | ✅ PreArm messages no longer pop up (they stay in the PreArm chip); at most 3 pop-ups, each closable. Settings for pop-ups (all / errors / off) and page banners. |
| 9 | Connect page: flight controllers at the top | ✅ Flight controllers listed first, tagged ArduPilot / PX4. |
| 10 | Warn when the board is not official or the firmware is beta / dev | ✅ Red banner for beta / dev builds with the stable version; amber banner for boards not on the official ArduPilot server; amber firmware chip. |
| 11 | Frame: show ArduPilot's motor letters A-B-C-D | ✅ Diagram shows output number, motor-test letter and spin direction. |
| 12 | Accelerometer calibration: save each side by itself when the vehicle is still | ✅ 4 s still on the right side saves it; moving resets the timer; a wrong side is named. |
| 13 | Level, gyro and baro calibration separate from the accelerometer | ✅ Own wizard step and Calibration tab. |
| 14 | Show `INS_TCALx_TMIN / TMAX` (IMU temperature calibration) | ✅ IMU temperature calibration card with the learned range, live temperature and **Learn on next boot**. |
| 15 | Move Mag Tools to Tuning & Health | ✅ |
| 16 | Guided motor-compass (CompassMot) route with pictures | ✅ Five steps with drawings: why, secure (props swapped to push down), current source, run, result. |
| 17 | Realistic perspective calibration pictures that follow the vehicle | ✅ 3D vehicle on every side tile, and a live 3D model that turns exactly like the vehicle in your hands. |
| 18 | Calibration quality / health, especially for compasses | ✅ **Calibration quality** card grading offsets, scale, soft-iron, motor compensation and field strength. |
| 19 | ESC calibration missing | ✅ Guided ESC calibration (ArduPilot `ESC_CALIBRATION = 3`, PX4 calibration command). |
| 20 | Tool to identify which output is which motor, without spinning servos | ✅ **Identify motors:** spins one motor output, you click its position and direction, the swaps are staged. Servo outputs are never spun. |
| 21 | Passthrough / bi-directional DShot only after the motors are assigned | ✅ Wizard order Motors → ESCs; those options appear once motor outputs are assigned. |
| 22 | Default motor test throttle 5 % | ✅ |
| 23 | Choose the height source (baro / rangefinder / GPS / optical flow) | ✅ **Height & position sources** card (EKF3 sources, primary baro, rangefinder below x %). PX4: `EKF2_HGT_REF` and fusion switches. |
| 24 | Same kind of sensors on one row (2 IMUs, 2 baros, 2 GPS) | ✅ One row per sensor type on Sensors & Peripherals. |
| 25 | Failsafe setup with all options and one-click defaults | ✅ **Recommended failsafe settings** per vehicle type with one click; new Logging group. |
| 26 | More than one battery; editable cell voltages | ✅ 1–3 batteries with a tab each; full / low / critical / empty per cell editable for LiPo, LiHV and Li-ion. |
| 27 | Tip-speed warning too alarming for a proven setup | ✅ Judged at nominal voltage with loaded RPM; red only above Mach 0.8. |
| 28 | Own custom sets in Setup recipes | ✅ **New custom set** from staged changes, non-default values or a `.param` file; export / import to share. |
| 29 | Wizard step to check buzzer and LEDs | ✅ **LEDs & buzzer** step with a test beep. |
| — | Radio calibration as throttle max / min, yaw, pitch, roll max / min, then all other channels | ✅ Stick ends one at a time, then every other channel end to end with a tick each. |
| — | Arm / disarm, emergency stop and other switches in the wizard | ✅ **Switches** step: press Assign and flip the switch. |

## Layout and app

| # | Request | Status in beta.3 |
|---|---|---|
| 30 | "For advanced users" group; Capabilities, Inspector and Messages near Connect / Overview; Guides near Peripherals | ✅ Sidebar regrouped. |
| 31 | Vehicle orientation on Overview; pop-out windows for graphs and the inspector | ✅ 3D attitude on Overview; **Pop out** on every page. |
| 32 | Board brand name at the top | ✅ |
| 33 | Blue themes and editable colours | ✅ Steel blue, Sky light, and a full colour editor (every colour, export / import). |
| 34 | CPU, RAM, bus / comm errors | ✅ System card: CPU load, free memory, internal errors in words (SPI, I2C, DMA, IO resets…), comm drops, measured link loss. |
| — | Live graphs empty ("IMU 1 vs 2 vs 3") | ✅ A chart with one missing line drew nothing; fixed. Legends show the average when not hovering. |

## Logs

| # | Request | Status in beta.3 |
|---|---|---|
| 35 | Show means when nothing is selected | ✅ Mean / min / max of the whole log or the zoomed range under every chart. |
| 36 | Export graphs as PNG; merge graphs | ✅ PNG and CSV export; merge preset charts into one, with a second axis when units differ. |
| 37 | Vibration verdict hid peaks of 40–60 | ✅ Typical level, peak with time, and time above 30 / 60. |
| 38 | Compare two logs | ✅ Lined up at arming, checks side by side, parameter differences. |
| 39 | RC sticks, orientation and parameters on the log page | ✅ Replay panel (3D attitude, both sticks, mode, altitude…) and a Parameters tab. |
| 40 | When clipping happened; GPS HAcc / VAcc; EKF innovations explained; long-loop causes | ✅ |
| 41 | Timeline of baro jumps, IMU errors, GPS glitches and EKF messages with times | ✅ **Events** tab with explanations; click to jump the chart there. |
| 42 | PID tuning estimate from the log | ✅ Tracking error, lag, overshoot and oscillation per axis with a suggestion. |
| 43 | eRPM vs output and thrust loss, beyond motor saturation | ✅ **Motors & ESC** tab: headroom, CW/CCW yaw imbalance, eRPM per % output. |
| 44 | Hover throttle against battery voltage; compare loads | ✅ **Hover & battery** tab, also across two logs. |

## Map

| # | Request | Status in beta.3 |
|---|---|---|
| 45 | Drone picture on the map | ✅ |
| 46 | Offline maps for fields without network | ✅ Viewed tiles are kept; **Download this area** (satellite / topo). |
| 47 | No-fly zones (airports, military, government) with a warning at arming | 🟡 Approximate airport circles for Türkiye (**not official**), own no-fly / allowed areas, GeoJSON / KML import, warning when armed inside. Official zone data is not included. |
| 48 | Mission planning: RTL, missions, fence | ✅ Mission editor with upload / download and `.waypoints` files, geofence, Return to launch and Set home. |
