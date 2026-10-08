# Troubleshooting

What the common warnings mean and what to do. The text in quotes is what NConfigurator or the firmware shows.

## Connection

| Symptom | What to do |
|---|---|
| No COM port appears | Use a USB **data** cable (many are charge-only), plug in directly (no hub), check that the board's LED is on. |
| Port appears but "Waiting for heartbeat…" | Wrong port or baud for a telemetry radio (try 57600). On USB the baud doesn't matter. Betaflight/INAV boards don't speak MAVLink; flash ArduPilot or PX4 first. |
| "Legacy FMU" / "PX4 FMU" in the port name | The board runs PX4. |
| Connection drops after a reboot | Normal for USB. NConfigurator reconnects automatically and returns to the same page. |

## Sensors

| Warning | Cause and fix |
|---|---|
| "No barometer detected" / "No compass detected" / "GPS enabled but not detected" | The sensor isn't powered or wired. Many boards power the baro, compass, GPS or receiver only from the battery rail: connect the battery and **Reboot**. |
| "Not detected this boot but seen before on this board" | A device that was there on an earlier connection is missing. Check the connector. If you removed it on purpose, press **Removed on purpose**. |
| "1 compass in the priority list is missing" / PreArm "Compass not found" | A compass was unplugged or replaced. **Mag Tools → Remove from list**, then calibrate. |
| PreArm "Compasses inconsistent" | Mag Tools → **Compass consistency** shows which pair disagrees. Usually a wrong orientation (`COMPASS_ORIENTn` / `CAL_MAGn_ROT`) or a compass near power wires. |
| "Unhealthy: Gyro 2, Accel 2" / PreArm "Gyros inconsistent" | One IMU is faulty or disturbed. Let the board warm up and reboot. If it persists, see Calibration → Sensor selection (expert) to stop using that IMU. |
| "EKF unhealthy: variance … (1.0 = rejected)" | Keep the vehicle still; check vibration, the compass and GPS on Sensors & Peripherals. Indoors without GPS this is expected until you set an origin (Guides → optical-flow recipe). |
| Vibration above 30, rising clipping | Balance the props, soft-mount the flight controller, check for loose parts. Logs → **Vibration per IMU** shows the details. |
| Compass calibration starts again from 0 % | ArduPilot restarts a failed fit by itself. The panel shows why (bad orientation, radius, offsets, residuals) and what to do; move away from metal, rotate slower, or try **Retry with relaxed fit**. |
| Log: "Thrust loss" / "Potential Thrust Loss" | A motor ran at full output without getting the attitude or climb asked for. Logs → **Motors & ESC** shows the headroom (average output while flying), motors working harder than others and CW/CCW yaw imbalance: usually an overloaded vehicle, a damaged prop or a tilted motor. |

## Radio

| Warning | Cause and fix |
|---|---|
| "Unhealthy: RC receiver" / PreArm "RC not found" | No RC signal: transmitter off, receiver not bound, or wrong port or protocol (Ports page). |
| "Radio calibration covers only CH1 1200–1800 µs" | The transmitter's endpoints are below 100 %. Raise the channel weights, then run **Calibration → Radio** again. |
| PX4 "sticks not mapped" | Run the radio calibration; it sets `RC_MAP_*`. |
| RC loss test: "No RC loss seen" | The receiver holds its last values when the signal is lost. Set its failsafe to "no pulses", or throttle below the failsafe PWM. |

## Outputs and motors

| Warning | Cause and fix |
|---|---|
| "DShot is selected but motors … are on IO (MAIN) outputs" | On Pixhawk/Cube boards DShot works only on FMU (AUX) outputs. Move the motors to AUX (**Motors & Outputs → Assign motors**) or set `BRD_IO_DSHOT = 1` where supported. |
| Motor test rejected | Disarm, switch the safety switch off (or `BRD_SAFETY_DEFLT = 0`), connect the battery. |
| A motor spins the wrong way or in the wrong position | Wrong direction: swap two motor wires or use ESC reversal. Wrong position: **Swap two outputs**. |

## Battery

| Symptom | Cause and fix |
|---|---|
| Battery chip yellow or red while the percentage looks fine | The voltage is below the low or critical failsafe voltage. The percentage is only as good as the capacity setting (`BATT_CAPACITY` / PX4 cell settings). |
| Voltage or current reads wrong | Peripherals → Battery → calibrate against a multimeter or clamp meter. |

## Parameters

| Symptom | Cause and fix |
|---|---|
| A write fails ("… failed", or the vehicle reports "refused") | The parameter is read-only, out of range, or locked by the firmware. The old value is kept. |
| "Reboot required" | Some settings (ports, channel map, sensor priority, CAN…) take effect after a reboot. |
| Yellow dots / "changed since boot" | Only values you changed during this power-up. Values the autopilot updates itself (gyro offsets, ground pressure) are ignored. |

## Simulation

| Symptom | Cause and fix |
|---|---|
| SITL starts but nothing connects | Use **Start & connect**, or connect to TCP `127.0.0.1:5760` (instance 0). Only one program can use that port. |
| PX4 SITL: "WSL is not installed" | Run `wsl --install -d Ubuntu-22.04` in an administrator PowerShell, reboot, then follow the commands in the tab. |
