# Armada OS for Pimax Portal XR2 Gen 1 (SM8250 VR Variant)

<img width="600" height="234" alt="pimaxarmadaos" src="https://github.com/user-attachments/assets/4abb7877-3bb2-422b-adcd-612c32e6d2dd" />


Using the Armada framework, this hopes to serve as the collaborative staging ground for porting Armada OS to the Pimax Portal with the primary objective to bypass the closed Android ecosystem to establish a hardware accelerated Linux container baseline.

Please note! We are currently in the exploratory and reverse engineering phase. 

## System Architecture & Target HW/SW

* **SoC:** Qualcomm Snapdragon XR2 Gen 1 (SM8250 VR Variant)
* **Target Framework:** Armada OS 
* **Hardware:** Pimax Portal (Standard and QLED models)

## Engineering Challenges & Roadmap (We're taking the backroads! It'll be bumpy...)

Stock Armada images function on alternative handhelds due to existing bootloader scripts and standardized inputs. However, our annoying stepchild (The Pimax Portal) lacks this infrastructure. (Pffft, pathetic brat. Amirite?) 

Bringing this port to a bootable state requires solving three specific hardware isolation issues. Therefore, contributors with experience in Qualcomm boot sequences, uinput mapping, and Linux kernel patching are highly encouraged to offer their support. (plz?)

### 1. Boot Sequence and Partition Mapping
The Portal requires a custom bootloader hook to redirect initialization away from the native Android boot image and into the Fedora based Linux container.
* **Goal:** Map the complete SM8250 logical partition table.
* **Goal:** Develop a custom boot script that safely hijacks the boot process without altering the `persist` or `calit` hardware calibration partitions.

### 2. Input Wrapper Reverse Engineering
The magnetic detachable controllers rely on closed Hardware Abstraction Layers and proprietary Qualcomm binaries which inhibit use of standard generic gamepad mapping systems.
* **Goal:** Extract and analyze raw hardware dumps from the stock firmware to document the serial protocols and polling rates.
* **Goal:** Write a custom kernel level input wrapper that translates these proprietary signals into standard Linux gamepad event nodes for native Steam Input recognition.

### 3. Thermal Management Integration
The Portal utilizes an active cooling fan that relies on proprietary system triggers to operate which the stock Linux kernels will not recognize natively.
* **Goal:** Isolate the fan control daemon.
* **Goal:** Integrate a custom thermal script into the early boot sequence to prevent hardware throttling to ensure safe operating temperatures during OS load.

## Contribution Guidelines

This is an open engineering effort. If you are working on a similar Snapdragon 865 hardware enablement project or want to tackle one of the specific roadblocks listed above, please open an issue to discuss your approach or submit a pull request! This is a... fraught undertaking I'm constantly being told. (Although, it has become such a constant... I could use it for white noise at this point) 

Ensure all pull requests target the `development` branch and include detailed commit messages specifying the exact hardware subsystem being modified.
