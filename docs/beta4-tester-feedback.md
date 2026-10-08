# Tester feedback on 0.2.0-beta.4

These are the problems and wishes a tester reported after testing 0.2.0-beta.4 on a **Pixhawk 6X**, a **Pixhawk 6C mini** (PX4 and ArduPilot) on 7 October 2026, and what changed in **0.2.0-beta.5**.

✅ fixed / added · 🟡 partly done (see the note) · ❓ needs more detail from the tester

Checked on virtual ArduPilot and PX4 vehicles and on a SpeedyBee F405 V4 (ArduPilot). Items marked *needs hardware check* still have to be confirmed on a Pixhawk / PX4 board.

## Firmware and PX4

| # | Report | Status in beta.5 |
|---|---|---|
| 1 | Detect PX4 (running) or a board waiting in its bootloader | ✅ With PX4 running, the board is identified with nsh `ver hw` and the matching `.px4` build is pre-selected. A board sitting in its bootloader (USB name "…BL") is shown on the Firmware page. *Needs hardware check.* |
| 2 | Only `.apj` and `.px4` files; `.bin` needed | ✅ Raw `.bin` application images can be flashed (with a warning, since a `.bin` has no board ID). A `.bin` that includes the bootloader is refused: it must go through DFU. |
| 3 | PX4 compass calibration still fails — use QGC's basics | ✅ The app re-sent the start command when PX4 answered *in progress*, which restarted the running calibration. Calibration commands are now sent once, and progress follows PX4's `[cal]` messages even without a command answer, as QGC does. *Needs hardware check.* |
| 4 | Buzzer circuit breaker: a button and volume instead of typing the number | ✅ Buzzer **On / Off** switch (`CBRK_BUZZER`), volume slider on ArduPilot (PX4 has no volume setting). |
| 5 | PX4 battery showed **65.53 V** on USB, capacity −1 | ✅ 65535 mV is MAVLink's "no reading": shown as no reading now. A voltage that doesn't fit the cell count gets a warning with the calibration steps; capacity −1 is explained. |
| 6 | MAVLink Inspector: other IMUs not visible, only RAW | ✅ All IMU streams are requested (PX4 too). |

## Calibration and setup

| # | Report | Status in beta.5 |
|---|---|---|
| 7 | ArduPilot accelerometer calibration: vibration stops the automatic capture | ✅ Stillness is judged by the direction of gravity on 1-second averages, so noise and vibration no longer reset the timer (tested with ±0.4 g simulated noise). |
| 8 | IMU temperature calibration: a confirmation box and how-to | ✅ Behind *I understand the risks*, with step-by-step instructions and the TMAX setting. |
| 9 | ArduPilot compass calibration fine, but the quality card was not updated | ✅ The results are read back again after ArduPilot saves them. |
| 10 | Bi-directional DShot shown even with PWM | ✅ Only with a DShot protocol. |
| 11 | Per-motor interference test usable only after ticking *props removed* | ✅ Throttle and test locked until ticked. |
| 12 | CompassMot: explain which prop goes where (B's prop to A, A to D…), better pictures | ✅ Picture and list of the moves: B's prop → A, A's → D, D's → C, C's → B. |
| 13 | Each advanced setup section: undo only that section's changes | ✅ **Undo** on each Safety & Failsafes card and each Setup Wizard step. |
| 14 | Inspector IMU chart: a 6C mini has no third IMU | ✅ Only the IMUs the board has. |
| 15 | *Failsafe vs flags* belongs after setup, not only for advanced users | ✅ New **Failsafe check** page under Tuning & Health. |
| 16 | A disabled feature (fence) takes a lot of space | ✅ While switched off only the on/off setting is shown. |
| 17 | Manual output for every servo output, not only motors | ✅ **Output test**: a row per output pin. |
| 18 | Identify motors: test every output pin and assign Servo x → Motor y, so wiring and PWM faults show | ✅ **Output test** replaces it: spin a motor output or move a servo / free output, and pick *which motor spun* — the outputs are re-assigned for you. |
| 19 | What about planes? | ✅ For planes the Output test lists each control surface with what it must do for each stick, and a **Reverse** switch. |
| 20 | Mag Tools: *Change ΔB* looked wrong (|B| fine) | ✅ The reference follows the field at rest, so turning the vehicle by hand no longer looks like interference. |

## Logs

| # | Report | Status in beta.5 |
|---|---|---|
| 21 | Map replay is 2D; wanted 3D like ArduPilot's web log viewer | ✅ **3D flight view**: satellite ground, path coloured by flight mode at its logged height, the vehicle with its attitude at the replay time; orbit / pan / zoom, Follow. 2D map still available. |
| 22 | The replay should open in its own window with more details | ✅ **Pop out**: flight view, replay panel and chart in a separate window. |
| 23 | Log parameters vs firmware defaults | ✅ A *Firmware default* column and *Only changed from default* (ArduPilot 4.1+ and recent PX4 logs record the defaults). |
| 24 | Compare: name the columns by log file | ✅ |
| 25 | Compare: more data, better style | ✅ About 15 more figures (current, power, consumption, angles, climb / descent, GPS, EKF, CPU, long loops, errors, modes) with A/B bars. |

## Other

| # | Report | Status in beta.5 |
|---|---|---|
| 26 | Board & device mapping should match the firmware's default mapping, with a warning | ✅ Ports and outputs that differ from the firmware default are marked, with a warning. |
| 27 | ArduPilot `-bdshot` vs normal build: something wrong after flashing | 🟡 When bi-directional DShot is on without RPM telemetry, the app now explains that boards with an IO co-processor usually need the `-bdshot` build. Please describe what went wrong, so it can be reproduced. |
| 28 | "FAT32 default" | ❓ Not clear where this belongs (SD card formatting?). Please give more detail. |
| 29 | The map sometimes covered dialogs and menus | ✅ Maps stay underneath dialogs and menus. |
