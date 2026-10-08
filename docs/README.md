# NConfigurator user manual

NConfigurator is a Windows setup and diagnostics tool for flight controllers running **ArduPilot** or **PX4**. It covers the path from a new board to the first flight: flashing, calibration, setup, tuning, health checks, logs and simulation.

> **Pre-release software.** NConfigurator was developed with AI assistance and is still being tested. Check every change before you fly, keep the propellers off while you work on the bench, and keep a parameter backup.

## Where to start

| You want to… | Read |
|---|---|
| Install the app and connect for the first time | [Getting started](#getting-started) below |
| Learn the screen layout, search, dock and warnings | [Working with the app](00-working-with-the-app.md) |
| Connect, see the vehicle status and capabilities, use the inspector, plan missions on the map, flash firmware | [Vehicle](01-vehicle.md) |
| Set up a new vehicle, calibrate, set failsafes, outputs and peripherals, use recipes | [Setup](02-setup.md) |
| Check sensor health, tune, compasses, edit parameters, back up, review logs | [Tuning & Health](03-tuning-and-health.md) |
| Filters and notch, scripts, simulation, settings | [For Advanced Users & App](04-tools.md) |
| Understand a warning or fix a problem | [Troubleshooting](05-troubleshooting.md) |
| See what testers reported on beta.5 and what changed | [Tester feedback on beta.5](beta5-tester-feedback.md) |
| See what testers reported on beta.4 and what changed | [Tester feedback on beta.4](beta4-tester-feedback.md) |
| See what testers reported on beta.3 and what changed | [Tester feedback on beta.3](beta3-tester-feedback.md) |
| See what testers reported on the first version and what changed | [Tester feedback on beta.2](beta2-tester-feedback.md) |

The chapters follow the groups in the app's sidebar.

## Getting started

1. **Install.** Run `NConfigurator-Setup-<version>.exe` and pick English or Turkish. The portable `.exe` needs no installation.
2. **Connect the flight controller over USB.** With **Auto-connect** on (top bar), NConfigurator connects as soon as the board appears. Otherwise pick the port and press **Connect**.
3. **Wait for the parameters.** The top bar shows the firmware, armed state, mode, GPS and battery. ArduPilot parameters come over MAVLink FTP with their default values, which takes a few seconds.
4. **Read the yellow banners.** After the first boot or a parameter reset, NConfigurator lists what is missing: undetected sensors, calibrations, frame or airframe.
5. **New vehicle?** Open **Setup → Setup Wizard** and go through the steps. **Existing vehicle?** Make a backup first (**Tuning & Health → Backup & Restore**).

### Safety rules that apply everywhere

- **Remove the propellers** for motor tests, ESC calibration, radio calibration tests, hardware simulation and anything else that can spin a motor.
- **Changes are staged.** Edited values are marked and stay on the PC until you press **Write**. **Discard** throws them away.
- Some settings only take effect **after a reboot**. The top bar then shows **Reboot required**.
- Boards that power the barometer, compass, GPS or receiver only from the battery rail don't detect them on USB alone. Connect the battery and reboot before trusting a "not detected" warning.

## Language

**Settings → Language** switches between English and Turkish. Parameter names and the firmware's own messages stay in English.
