# Moto G13 — CODM Performance Tuning

Unlocking maximum FPS on the Helio G85 (MT6768) for Call of Duty: Mobile using Magisk modules.

## Hardware
- **Device:** Moto G13 (penangf)
- **SoC:** MediaTek Helio G85 (MT6768)
- **GPU:** Mali-G52 MC2
- **RAM:** 4GB
- **OS:** Android 13, rooted with Magisk

## Magisk Modules Used
- **PerfMTK** (v17.1): MediaTek CPU/GPU frequency tuning, thermal bypass.
- **Mediatek Mali GPU Governor** (v2.12.5): Forces GPU to max clocks for games.
- **Thermal Void** (v3.0.0): Disables system thermal throttling daemons.
- **Flame Unlocker** (v2.0): Spoofs device as OnePlus 11R (CPH2747) to unlock CODM graphics tiers.

## Post-Reboot Configuration
Run these commands via ADB after booting:

~~~bash
# 1. Set PerfMTK to performance mode
adb shell "su -c 'perfmtk performance'"

# 2. Disable PerfMTK thermal throttling
adb shell "su -c 'perfmtk --thermal disable'"

# 3. Set GPU Governor to fast mode
adb shell "su -c 'sed -i \"s/mode = \\\"balance\\\"/mode = \\\"fast\\\"/\" /data/adb/gpu_governor/config/config.toml'"
~~~

## Verification
~~~bash
adb shell "su -c 'perfmtk --status'"
# Expect: ACTIVE_PROFILE = performance

adb shell getprop ro.product.model
# Expect: CPH2747 (OnePlus 11R)

adb shell "su -c 'cat /sys/class/thermal/thermal_zone5/temp'"
# Expect: 50000-75000 (50-75°C)
~~~

## In-Game Settings (CODM)
- Graphics Quality: Low / Medium
- Frame Rate: Max
- Depth of Field: OFF
- Ragdoll: OFF
- Anti-Aliasing: OFF
- Real-Time Shadows: OFF
- Bloom: OFF

## Warnings
1. **Heat:** With thermal throttling disabled, the SoC will hit 70-80°C. The phone WILL overheat without physical cooling.
2. **Cooling:** Use a desk fan pointed at the back of the phone. Do not play while charging.
3. **Expected FPS:** 35-45 FPS stable. Dips to 11-20 FPS indicate thermal throttling is still occurring.
4. **Do NOT use scrcpy while gaming.** Screen mirroring eats CPU and causes lag.
5. **No custom kernel** exists for penangf. GPU overclocking beyond stock 853 MHz is not possible.
