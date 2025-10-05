# Prusawire Config for Klipper

## Installation

### Some Basic Assumptions

This guide assumes you are running an out-of-the-box installation of [MainsailOS](https://docs-os.mainsail.xyz/) on a Raspberry Pi.
We do not recommend using KIAUH, as this tends to be over-zealous with how it configures your machine.

For installing MainsailOS (and with that, Klipper) for the first time, please refer to their [installation guide](https://docs-os.mainsail.xyz/getting-started/raspberry-pi-os-based).

### Upgrading the Einsy Rambo to Klipper - Read this!
Installing Klipper on the Einsy Rambo board is possible, with extra steps. Follow the guide published by the awesome folks at [MyRigs3D](https://myrigs3d.com/blogs/infos/revive-your-prusa-mk3s-with-klipper-1-5-flash-bootloader)! We recommend Method 2.

**Note:** Some users have reported problems using `avrdude` with the latest Raspberry Pi OS version (bookworm). If you experience error messages from avrdude complaining about gpio ports being busy, please try using the bullseye version of Raspberry Pi OS instead, available as "Raspberry Pi OS (Legacy)" in Raspberry Pi Imager.

### Process

- Run the following command from your SSH terminal

```shell
cd ~/
git clone https://github.com/Positron3D/prusawire-klipper-config.git ~/printer_data/config/prusawire
```

- Add this section to your moonraker.conf file

```ini
[update_manager prusawire-config]
type: git_repo
primary_branch: main
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
