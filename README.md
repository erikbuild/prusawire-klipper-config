# Prusawire Config for Klipper

## Installation

- Run the following command from your SSH terminal

```shell
cd ~/
git clone https://github.com/Positron3D/prusawire-klipper-config.git ~/printer_data/config/prusawire
```

- Add this section to your moonraker.conf file

```ini
[update_manager prusawire-config]
type: git_repo
path: ~/printer_data/config/prusawire
origin: https://github.com/Positron3D/prusawire-klipper-config.git
managed_services: klipper
```

- Refer to the `printer.cfg.example` file on setting up your printer.cfg for the first time

- Run PID calibration on your hotend:
```shell
PID_CALIBRATE heater=extruder TARGET=250
```

- If running boards other than the Einsy, PID calibrate your heated bed:
```shell
PID_CALIBRATE heater=heater_bed TARGET=110
```

## Sensorless Homing

If you are running the Einsy board, congrats, you are now done.

For the BTT SKR Mini E3, some further tuning likely needs to happen. Refer to [this guide](https://gist.github.com/clee/9108f7717defce8b1222698f816def0a#finding-the-right-stallguard-threshold) by clee
on setting the correct stallguard threshold.

## Input Shaper

Some defaults have been provided, but they are no doubt unsuitable for your exact machine. We recommend installing [ShakeTune](https://github.com/Frix-x/klippain-shaketune) for measuring resonances, and reading the [Klipper guide](https://www.klipper3d.org/Measuring_Resonances.html#max-smoothing) on understanding which value to choose.

In addition, 

### Y Axis Input Shaping

This requires an external accelerometer (eg LDO Input Shaper) to be mounted to your heated bed.
