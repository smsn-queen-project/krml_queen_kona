
# Queen kernel

The Queen kernel is made to support the Samsung Snapdragon 865 device family on higher Android versions.
With the latest Android versions, Kernel versions are also plays a critical part and this kernel focuses on supporting devices in the long term.

Note that Queen kernel absoluetly not supported by OneUI 5.1 (Android 13)

Use with only known supported ROMs as some features require system side modification to take advantage of them.  

## Features


* Completely rebased kernel source

This kernel is based on latest Qualcomm Snapdragon 865 BSP kernel with Google's android-4.19-stable merged in.
It includes bare minimum required changes from Samsung. No unnecessary code, no unneeded OEM changes. Only the required pieces.

* Always builded with latest Clang + ThinLTO

* Latest F2FS changes merged from mainline

* MGLRU & LRNG backported from upstream Linux versions

* Latest Wi-Fi drivers from Qualcomm

* OEM changes to Samsung drivers from SM8350

Please note that after booting with Queen, flashing another kernel doesn't suggested. There is a major code base differences (Avg 15-20K files changed) between other kernels and Queen. Stability may not be guaranteed and you may have issues after flashing.

## Frequently asked questions (FAQ)

### I am getting a black Download mode screen after flashing another kernel? Is this the fault of Queen?

Not entirely. The Queen kernel comes with its own source-built DTBO image,

which is much different than the Stock DTBO image. Since most custom kernels are based on stock DTBO,

flashing another kernel will cause a conflict with the DTBO provided by Queen,

so the bootloader will crash into Download mode due to this conflict and you will get that black Download mode screen.

**Solution**: Flash the stock DTBO.img from recovery.

<br/><br/>  

### Switching from Queen to another kernel caused a data wipe? Why is that happened?

This issue is caused by the kernel you flashed and the nature of the Queen kernel. In the stock kernel, fs-verity is disabled,

and most custom kernels follow the same behavior. In Queen, fs-verity is enabled by default. And due to the nature of fs-verity,

switching from a kernel with fs-verity to a kernel with fs-verity disabled will wipe your data for your safety.

**Solution**: There is not much that can be done about this. Flash your custom kernel after flashing your ROM, or if you booted with the Queen kernel, don't flash it unless you have backed up your data.

Everything will be wiped, including your Secure Folder, so be sure to back up everything.

Remember that it is safe to switch from another kernel to Queen. No issue reported or observed yet.

<br/><br/>  

### My device reboots randomly? What's the issue with this kernel?

This issue was caused by a conflict between FuseFS and SDCardFS file systems.

SDCardFS was deprecated long ago with Android 11 and FuseFS is now the default File system for Emulated Storage. Since SDCardFS is no longer supported, it caused a kernel panic with the new FuseFS changes.

This issue is fixed by using the stock FuseFS driver when SDCardFS is built into the kernel.

This workaround will be deprecated with the next possible OneUI port release and FuseFS will be the default.

**Solution**: This issue is now fixed with latest builds. Update your kernel if you suffer from that.
<br/><br/>  

### Why it's name Queen?

Queen is the internal project name for Android Q (10) at Samsung.

Snapdragon 865 was also released with Android 10, so I wanted to make a reference to that.

<br/><br/> 
