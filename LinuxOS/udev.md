# Udev

## Introduction
* Udev is a _userspace_ system that can be used to register userspace handlers for events
    - Udev receives notification from the kernel when a new device is introduced to the system.
    - Udev's main purpose is to act upon peripheral detection and hot-plugging
* It will examines the device, creates the device file, and then initializes the device.
    - Udev also manages device nodes in the `/dev` directory by adding, symlinking and renaming them.

## Udev Rules
* Udev rules go in `/etc/udev/rules.d/` with file names ended with `.rules`
* Udev rules shipped with various packages are found in `/usr/lib/udev/rules.d/`, however, the ones in `/etc` take precedence
