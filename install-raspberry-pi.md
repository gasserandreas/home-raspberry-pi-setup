# Install Raspberry PI Platform

## Install Raspberry PI OS

Install Raspberry PI Operation System.

1. Download Install Raspberry Pi OS using Raspberry Pi Imager - https://www.raspberrypi.com/software/
2. Open installer and select device, platform and location
3. Add OS Customisation:
  - General:
    - Set Username and Password
    - Set local settings:
      - Time zone: `Europe/Zurich`
      - Keyboard layout:  `us`
  - Services:
    - Enable SSH:
      - Allow public-key authentication only: `add your public ssh key`
4. Run installation
5. Inject memory card into Raspberry PI and boot

## Setup Bluetooth mouse

1. start bluetooth utils: `bluetoothctl`
2. make sure the device and agent is on: `power on && agent on`
3. scan for devices: `scan on`
4. identify mac address of device to connect
5. stop scan: `scan off`
6. connect device: `pair <dev>`
  - e.g. <dev>=00:1D:A5:F7:FF:0D

more details can be found here: https://forums.raspberrypi.com/viewtopic.php?t=214373

## Install PCIE Hat
Follow the hardware installation instructions in "EP-0241 - 52Pi Wiki", then setup the hat as described below


### Setup PCIE Hat
1. open: `/boot/firmware/config.txt`
2. add
  - `dtparam=pciex1` to `[ALL]` section
  - `dtparam=pciex1_gen=3` to `[ALL]` section
3. update eeprom: `sudo rpi-eeprom-config --edit`
4. add:`PCIE_PROBE=1`
5. Check disks: `sudo lsblk` (nmve0n1p1 should be connected)
6. format disk to enable read/write: `sudo mkfs.ext4 /dev/nmve0n1p1`
7. reboot Raspberry PI, NVP disk should be visible on next boot

### Enable boot from PCIE HAT
1. clone rpi-clone project: `git clone https://github.com/geerlingguy/rpi-clone.git`
2. install project:
  - `cd rpi-clone`
  - `sudo cp rpi-clone rpi-clone-setup /usr/local/sbin`
3. wipe PCIE SSD first:
  - `sudo umount /dev/nvme0n1p?`
  - `sudo wipefs --all --force /dev/nvme0n1p?`
  - `sudo wipefs --all --force /dev/nvme0n1`
  - `sudo dd if=/dev/zero of=/dev/nvme0n1 bs=1024 count=1`
4. update eeprom: `sudo rpi-eeprom-config --edit`
5. add to change boot order: `BOOT_ORDER=0xf416`
6. reboot to try
7. if it worked, remove SD_Card

# Additional setup & checks

## Check SSH connection
SSH should be enabled if followed this installation guide.
Try to connect like: `ssh administrator@<raspberry-pi-IP>`

## Update all packages
1. `sudo apt-get update`
2. `sudo apt-get upgrade`
3. `sudo apt-get full-upgrade`
4. `sudo apt-get autoremove`
5. `sudo apt-get clean`

## Change important system configs
Open raspberry-pi config: `sudo raspi-config`

1. Change Boot/Login to be console only: System Options -> Boot / Auto Login -> Console