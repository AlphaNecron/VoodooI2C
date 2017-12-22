#<cldoc:Installation>

&#8291;

## A Warning

VoodooI2C is for **advanced** tinkerers. In particular, you should know how to perform the following. If you do not know even one of the following then please do not proceed with this guide and please do not request help on the Gitter channel:

	1. How to install a kext
	2. How to patch your DSDT
	3. How to edit your Clover configuration file

Furthermore, the development team of VoodooI2C accepts no responsibility for any damage to your system that arises because of misuse of this kext or installation guide. VoodooI2C is safe to use when installed correctly but, as always with hackintoshes, proceed at your own risk.

## System Requirements

VoodooI2C is designed to run on the vast majority of modern systems. However, there are some minimum system requirements:

1. Your machine should have an Intel CPU (usually i3/i5/i7) with at least the `Haswell` microarchitecture. It is easy to determine your system's microarchitecture given that you know your CPU's model number. The model number is usually 4 digits long and sometimes has some letters that come after it. For example, 'Intel® Core™ i7-**4**600U'. The bold number here determines your system's microarchitecture and the list below provides a classification:
	1. 4 - Haswell
	2. 5 - Broadwell
	3. 6 - Skylake
	4. 7 - Kabylake
If the number is not **at least** 4 then your system is not suitable for VoodooI2C.kext.

2. If your machine shipped with Windows then the minimum required version of Windows is Windows 7. If your machine shipped with a previous version of Windows then it is unlikely that your machine will be supported by VoodooI2C. If your machine did not ship with Windows (for example, it may have shipped with Linux or with no preinstalled OS) then you may skip this requirement.

3. Your machine should have at least one supported I2C controller. The following are the device IDs of the supported controllers:

	1. 'INT33C2' and 'INT33C3' - Haswell era
	2. 'INT3432' and 'INT3433' - Broadwell era
	3. 'pci8086,9d60', 'pci8086,9d61', 'pci8086,a160' and 'pci8086,a161' - Skylake/Kabylake era

4. Your machine should have at least one supported I2C device. For the vast majority of users, this will be an I2C-HID device. Examples of I2C-HID devices include Precision touchpads, touchscreens and sensor hubs.

5. Your hackintosh is running at least 10.10 Yosemite. VoodooI2C may work on earlier versions of macOS but we do not provide support for machines that are not running at least 10.10.

6. Your hackintosh is using the Clover bootloader. Your mileage may vary with other bootloaders but we do not provide support for machines that do not use the Clover bootloader.

If you meet all 5 of these requirements then you may proceed with the next section of this installation guide.

## Preparing your machine for VoodooI2C

You **must** be familiar with DSDT patching. If you do not know how to patch your DSDT then VoodooI2C is **not** for you. We will not provide support for basic DSDT patching. Moreover, your DSDT should be be fully patched according to your system's needs before you attempt to further patch it for VoodooI2C.

You must be using the latest version of MaciASL found [here](https://bitbucket.org/RehabMan/os-x-maciasl-patchmatic/downloads/) (or an equivalent ACPI patcher). You must ensure that MaciASL's compiler version is set to the latest one. This can be done in the `iASL` tab of MaciASL's Preferences. After applying each patch, save your DSDT and restart your system.

### Adding the VoodooI2C DSDT Patch Repository

Follow these instructions in order to add the VoodooI2C patch repository to MaciASL:

1. Open MaciASL and navigate to the preferences.
2. In the preferences, open up the Sources tab and click the plus button.
3. In the name column write `VoodooI2C` and put `http://raw.github.com/alexandred/VoodooI2C-Patches/master` as the URL.
4. Close the preferences window.

### Windows Patches

Regardless of whether or not your machine shipped with Windows, it is likely that you will require a Windows patch. Under the `VoodooI2C` section in the MaciASL patches dialog box, there are a few patches labelled `Windows`. Choose the patch corresponding to the version of Windows that shipped with your machine. If you are not sure which version of Windows your machine shipped with, check the product key sticker which is usually located on the bottom of your machine. If your machine did not ship with Windows then you will have to test each patch until you find one that works - it is recommended that you start with Windows 7 and work your way up.

### Controller Patches (Skylake systems)

If your machine is Skylake then it is possible that you need a controller patch. Applying it can't hurt if you don't need it so let's apply that patch. Under the `VoodooI2C` section in the MaciASL patches dialog box, there is a patch labelled `I2C Controllers [SKL+]`. Apply this patch.

### GPIO Patches (Skylake+ systems)

If your machine is Skylake or above, you will likely need a GPIO patches as well. 

#### Controller Enabling

Under the `VoodooI2C` section in the MaciASL patches dialog box, there are a few patches labelled `GPIO`. You will need to apply the one labelled `GPIO Controller Enable`.

#### Pin Enabling (Apply for each I2C device)

Under the `VoodooI2C` section in the MaciASL patches dialog box, there are a few patches labelled `GPIO`. If you can find a patch pertaining to your machine and I2C device then you may apply it. Else you will need to follow the <GPIO Pinning> guide for each I2C device you wish to use.

## Installing the kext

Once your machine has been prepared for VoodooI2C, you will now be able to install the kexts. Vist the [release page](https://github.com/alexandred/VoodooI2C/releases) and download the latest release. You will usually need to install two kexts: a core kext and a satellite kext. Sometimes it is the case that you will need to install more than one statellite. You should consult the <Satellite Kexts> page to determine which satellite kexts your device needs.

Install the core kext `VoodooI2C.kext` and your chosen satellite kexts using your favourite kext installation method to your favourite kext installation destination. Restart your computer and enjoy your system!

Should you run into any problems when trying to install or use VoodooI2C, please visit the <Troubleshooting> page.