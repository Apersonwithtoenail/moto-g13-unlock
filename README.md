# Motorola Moto G13 - Bootloader Unlock Guide

Motorola official website fails to generate bootloader unlock codes for the Moto G13 and G23. This guide documents the working method to unlock the bootloader on Kali Linux / Linux.

## Requirements
* Moto G13 (Tested on XT2331-3)
* ADB and Fastboot installed
* USB Cable

## Step 1: Enable OEM Unlocking
1. Go to `Settings > About phone` and tap `Build number` 7 times.
2. Go to `Settings > System > Developer options`.
3. Enable **OEM unlocking** and **USB debugging**.

## Step 2: Get the Device Key
Connect the phone to your PC and boot into fastboot:
```bash
adb reboot bootloader
```
Get the unique 32-character key:
```bash
fastboot oem get_key
```
*Copy the 32-character string it prints out.*

## Step 3: Generate the Unlock Code
Because the official Motorola portal rejects G13 keys, use the community generator:
1. Go to: [Moto G13/G23 OEM Key Generator](https://cxzstuff.github.io/Moto-G23-G13-OEM-Key-Generator/)
2. Paste your 32-character key and click **Generate**.

## Step 4: Unlock the Bootloader
Send the generated key to the phone:
```bash
fastboot oem key <YOUR_GENERATED_KEY>
```
Now unlock the bootloader:
```bash
fastboot flashing unlock
```
*Note: Your phone will prompt you on the screen. Use Volume Down to highlight Yes and Power to confirm.*

## Step 5: Verify
```bash
fastboot getvar unlocked
```
If it says `unlocked: yes`, you are done! The bootloader is unlocked and you can proceed to root with Magisk.

## Warning
Unlocking the bootloader will **wipe all data** on the phone. Back up your files first!