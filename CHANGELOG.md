# Changelog

## 0.2.0-beta.6 — 2026-10-08

Fixes and additions from testing beta.5 on a Pixhawk 6C mini and a Lectron Pi5 H7. Every reported item and its status: [Tester feedback on 0.2.0-beta.5](docs/beta5-tester-feedback.md).

### Fixed

- Flashing custom boards whose bootloader has its own USB name; longer erase wait for H7 boards.
- Accelerometer auto-capture on real boards; calibration results can no longer be undone by *Revert*; wizard marks cleared after a reset or flash; PX4 "already calibrated" detection.
- Battery settings from the wizard (critical / arming voltage) and the battery count; replay pop-out window; health tiles agree with PreArm messages.

### Setup and calibration

- Compass priority before calibrating; level / gyro / baro show when calibrated; radio calibration needs live sticks; stick mode 1–4; flight-mode slots and switch zones.
- Motor assignment in four steps, motor tests only after write + reboot; voltage calibration only for analog monitors; no fence in the first-setup failsafes.
- Wizard: start from a clean vehicle (backup, reset, reboot). PID gains locked until *Edit gains*, parameter list view, confirmations before writing.

### Pages

- Messages, MAVLink Inspector and Backup & Restore under *Vehicle*; live field chart in the Inspector; Copy / Save / Clear for messages.
- Overview: horizon and 3D side by side, build variant badge; clickable sensor tiles with reasons; clearer ready-to-fly explanations.
- Search finds sections inside pages (Ctrl+F); *Board hardware* from ArduPilot's board definition.

### Logs

- Replay: time range, vehicle size, position / height source; event filters; an event click moves the replay to it.
- Parameters: save all / changed, descriptions; *Internal problems* on System; Compare charts of both logs, *Swap A ↔ B*, events side by side.

## 0.2.0-beta.5 — 2026-10-07

Fixes and additions from testing beta.4 on a Pixhawk 6X and a Pixhawk 6C mini. Every reported item and its status: [Tester feedback on 0.2.0-beta.4](docs/beta4-tester-feedback.md).

### Fixed

- **PX4 compass calibration:** the start command was sent again when PX4 answered *in progress*, restarting the calibration. It is sent once now, as in QGC.
- **PX4 battery** showed 65.53 V on USB power (the "no reading" value).
- ArduPilot accelerometer auto-capture with a vibrating board; compass quality after calibrating.
- The map no longer covers dialogs and menus. Mag Tools ΔB at rest. Inspector shows only existing IMUs, and all of them on PX4.

### Firmware

- PX4 board detected with `ver hw`; boards waiting in the bootloader are shown; raw `.bin` images.

### Setup and tools

- **Output test** replaces *Identify motors*: every output pin, spin / move it, *which motor spun* re-assigns outputs, plane surface checks with Reverse.
- CompassMot prop moves (B to A, A to D, D to C, C to B); **Undo** per section; disabled fence collapses; bi-dir DShot only with DShot.
- Buzzer On / Off and volume; IMU temperature learning with steps behind a confirmation.
- **Failsafe check** page under Tuning & Health; board mapping marks changes from the firmware defaults.

### Logs

- **3D flight view** over satellite imagery with the vehicle at the replay time; **Pop out**.
- Parameters vs firmware defaults; Compare named by file with many more figures.

## 0.2.0-beta.4 — 2026-10-06

Fixes and additions from testing on a Pixhawk 6X and a Lectron Pi5 H7. Every reported item and its status: [Tester feedback on 0.2.0-beta.3](docs/beta3-tester-feedback.md).

### Fixed

- Setup Wizard marks were still lost after a reboot on some boards.
- Inspector charts failed in pop-out windows.
- **PX4:** an uncalibrated compass (e.g. BMM350) was not detected; compass calibration progress was not shown; a baro calibration was offered.
- Pop-up messages no longer block the buttons under them.
- Logs: motors on AUX / IO outputs, vibration for every IMU.
- Accelerometer calibration could not see *still* with normal IMU noise.
- Compass side tiles when sides are done out of order; calibration quality refreshes after calibrating.

### Setup

- Frame and PX4 airframe chosen from **pictures**; new **Safety switch** step; Battery before Failsafes; compass priority and all channel functions in the wizard; one **Write** button; a finished-steps summary; PX4 ESC protocol; Initial tune marked expert-only and hidden on PX4.
- After a firmware flash or a reset the app opens the Setup Wizard; reset buttons say what they reset (**firmware defaults** / **tuning defaults**).
- Firmware: **Build** choice, e.g. `-bdshot`.
- Motors: **Frame & motor wiring** card; manual motor sliders behind a confirmation.

### Health and tools

- Sensors: estimator in use and an **EKF / priority** column.
- Mag Tools behind a confirmation; CompassMot with prop-swap pictures and live throttle / current / voltage / interference chart.
- **MAVLink Console** page for PX4 with more quick commands; Messages explains errors in plain words; **Copy** on both.
- Inspector: time window 1 s – 10 min.

### Logs

- **Summary** tab: verdict, flight figures, checks in plain words, sensor chips and **suggested changes** you can stage.
- **Map & replay** with Play; replay line on every chart.
- Richer **Compare**; the open log stays loaded across pages.
- New guides: AutoTune, QuikTune, PX4 auto-tuning, Save Trim.

### App

- Sidebar regrouped: Parameters, Filters, Mag Tools, Logs, Inspector, Messages and Console under *For Advanced Users*; expert failsafe groups collapsed.
- **Ground station dark / light** themes (QGC-like) replace the Toprak themes; Settings in two columns; Overview attitude card with a compass rose and a fixed size.

## 0.2.0-beta.3 — 2026-10-06

Fixes and additions from the first round of real-hardware testing. Every reported item and its status: [Tester feedback on 0.2.0-beta.2](docs/beta2-tester-feedback.md).

### Fixed

- Outputs on boards with an IO co-processor flickered between MAIN and AUX values; outputs are now named **MAIN n / AUX n**.
- Live charts with one missing line (e.g. no IMU 3) drew nothing.
- Setup Wizard steps were marked done just by visiting them, and the marks were lost after a reboot.
- PreArm messages popped up as errors and covered the page buttons.
- Clicking the map's attribution link replaced the app with a web page.
- Reboot from the disconnect dialog reconnected instead of disconnecting.
- A failing page no longer blanks the whole window.

### Setup and calibration

- **Setup Wizard:** Mark done / Skip remembered per board; new steps *Level · gyro · baro*, *Switches* (arm, emergency stop, RTL…) and *LEDs & buzzer*; PX4 airframe picker; recommended failsafes; 1–3 batteries with editable cell voltages; motor letters on the frame diagram.
- **Radio calibration** by stick ends (throttle, yaw, pitch, roll max / min), then all other channels.
- **Accelerometer** sides saved by themselves when the vehicle is still; **3D vehicle** on every side tile and live during calibration.
- **Compass:** reasons for failed attempts, compass and fit choice, retry with relaxed fit; **calibration quality** grades; guided **CompassMot**.
- **ESC calibration**, **IMU temperature calibration** card, **height source** selection (EKF3 / EKF2).
- **Identify motors** tool; motor test starts at 5 %; passthrough and bi-directional DShot after motors are assigned.
- **Custom setup recipes** you can share.

### Logs

- Event timeline with explanations, vibration peaks, clipping times, long-loop causes, motors & eRPM, hover vs battery, PID estimate, replay with 3D attitude and sticks, compare two logs, PNG / CSV export, merged charts.

### Map

- Mission planning with upload / download and `.waypoints` files, geofence, Return to launch / Set home, flight-restriction zones (approximate, not official) with an arming warning, offline map tiles.

### App

- Sidebar regrouped (*For Advanced Users*), pop-out windows, 3D attitude on Overview, board name in the top bar, beta / dev firmware warnings.
- Steel blue and Sky light themes and a full colour editor; pop-up and banner settings.
- System health: CPU, memory, internal errors, link loss.

## 0.2.0-beta.2 — 2026-10-03

First public pre-release under the name **NConfigurator** (formerly Naspier). Settings from an earlier Naspier installation are carried over on the first start.

### Calibration and setup

- **Radio calibration wizard** (QGC style): transmitter mode, then stick-by-stick detection with reversal, extents, flight-mode switch, a review with checks, write with restore, and an RC-loss test.
- **Compass calibration** with six orientation tiles for ArduPilot and PX4, plus ArduPilot's sphere coverage.
- **Device names** on every calibration, e.g. "Mag 1 · IST8310 · I2C1 · internal".
- **Sensor selection & EKF** (locked expert settings): IMU and EKF lanes, primary lane, compass priority, primary baro/GPS; PX4 sensor priorities.

### Pages

- **Safety & Failsafes** page with a plain-language "what happens when…" summary.
- **OSD layout editor** (ArduPilot).
- **Mag Tools:** compass consistency check, live interference (mG per amp, heading shift), per-motor interference test.

### Tools

- **Simulation:** ArduPilot SITL on Windows (stable / beta / dev), real devices attached to the simulation, PX4 SITL via WSL2, PX4 HITL / SIH.
- **PX4 shell (nsh)** on the Messages page.

### Layout

- Collapsible sidebar, **Ctrl+K** search for pages and parameters.
- Inspection dock with pinned live values (**Ctrl+J**).
- PreArm reasons collected in the top bar.

### Warnings

- New warnings: EKF unhealthy, short radio endpoints, DShot on IOMCU outputs.
- The battery chip judges by voltage too, and shows "No battery" on USB power.

### Fixes

- Settings the autopilot updates by itself no longer show as "changed since boot".
- "Seen before on this board" is now tracked per board and firmware, and can be dismissed for good.
- PX4 dev builds are shown as such.
- MAVLink Inspector: the IMU 1 chart stayed empty on ArduPilot; it now uses the IMU data ArduPilot streams by default.
- Live charts: time labels no longer repeat, and long value labels are no longer cut off.

## 0.2.0-beta.1

Mag Tools, parameter filters (modified / default / since boot), MAVLink inspector presets and failsafe view, setup recipes, firmware capabilities, Lua script library, hardware warnings after the first boot, log presets and spectrogram, installer in English and Turkish.
