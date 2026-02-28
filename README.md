# Migrating to APatch on Tecno Spark Go 1 (KL4)

I was currently running an InfinityX GSI rooted with SukiSU-Ultra, but I wanted to migrate over to APatch. The tricky part was that I had completely forgotten my exact current build version. On this phone, having the exact same build variant (or region, like OPPJ) is mandatory. This is a simple tutorial on how I safely made it.

### The Toolkit
* A Linux (I used Arch Linux) or Windows computer.
* The `spd_dump` tool.
* A 100% stock `boot.img` extracted from the official `.pac` firmware that exactly matches your region (e.g., OPPJ) or dumped from your current device. 
* The APatch app.

### The Methodology
Migrating to APatch on this device requires a specific approach because compiling and patching a custom kernel will not guarantee that the phone will boot. The Tecno KL4 runs an Android 14 interface on top of an older Android 13 vendor base, meaning any mismatched files or standard fastboot flashes will result in a frozen Tecno logo. To get around this, I extracted a pure untouched stock `boot.img` from the official firmware that matched my specific firmware region because any other firmware won't work. Instead of swapping out kernels, I patched this pure stock image directly in the APatch app, which keeps all of Tecno's original file signatures perfectly intact. To flash it, I bypassed the bootloader entirely by using `spd_dump` to write the patched image directly in BROM mode. You can enter BROM mode by long-pressing the Volume Down and Power buttons simultaneously while the `spd_dump` script is waiting in the terminal.

**Note:**
> If you don't know your current build number/version, you can use avbtool from android-tools to read your `vendot_boot` image to check it or using this shell command:
```shell
adb shell getprop ro.vendor.build.fingerprint
```

### Current Setup
* **Device:** Tecno Spark Go 1 (KL4) OPPJ
* **Kernel:** 5.15.180-android13-8 (Stock)
* **Root Solution:** APatch
* **System:** InfinityX GSI

### Sources
- [Apatch Docs](https://apatch.dev/what-is-apatch.html)
- [Apatch Manager](https://apatch.dev/what-is-apatch.html](https://github.com/bmax121/APatch/releases))
- [KL4 Firmwares](https://www.needrom.com/download/tecno-kl4/)
- [InfinityX GSI](https://github.com/Doze-off/ProjectInfinity-X_gsi)

### Warning
Always use `spd_dump` to read and backup your current `boot` partitions before you write any new images to your phone.
