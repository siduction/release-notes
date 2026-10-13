The siduction team is pleased to present another release finally. More time has passed since the last release than originally planned.

Traditionally, Big Crime was supposed to be released between Christmas and New Year. However, a lack of time among the team members delayed the release until now. The latest images are available for[Download](https://siduction.org/installation-media/) now.

### What can you expect from siduction 2026.1.0?

First, a few words about the new artwork for siduction 2026.1.0, titled “Big Crime”. It was inspired by Neil Young's song of the same name, in which he sharply criticizes the policies of the current US administration. The wallpaper was generated using ChatGPT AI.

### siduction Editions

The editions we offer with siduction 2026.1.0 are KDE Plasma 6.7.4, Xfce 4.20, Xorg, and NOX. Unfortunately, GNOME, MATE, and Cinnamon did not make it into the selection because there are no maintainers for them within siduction. If you are interested or know someone who might be, please get in touch. Perhaps they will return one day. Of course, they can still be installed from the repository.

LXDE is currently not in a release-ready state. We will provide it later once it is ready for release.

The released siduction 2026.1.0 images are snapshots of Debian Unstable, also known as Sid, from October 12, 2026. They include several useful packages and scripts, a Calamares-based installer, a substantially revised CLI installer, and a customized version of Linux kernel 7.2.10, while systemd is at version 262-1.

### KDE Plasma 6.7.4

We ultimately waited for Plasma 6.7 before releasing siduction 2026.1.0 “Big Crime”. This new major version marks a turning point, as it is the last major release of KDE Plasma to include an X11 session. Starting with Plasma 6.8, scheduled for release on October 14, Wayland will be the only supported display protocol.

Users who still encounter problems with individual applications under Wayland can switch to Xfce, which does not yet use Wayland by default.

A fork called [SonicDE](https://%28https://github.com/Sonic-DE) is currently being developed on GitHub. It can already be installed in Testing and Unstable, although we have not yet tested it extensively. If you have any experience with it, feel free to share your findings in our forum.

### Xfce 4.20

Xfce remains true to its slow release cycle and, as with our previous release, is still at [Xfce 4.20](https://www.xfce.org/about/tour420/). It currently offers an experimental Wayland implementation, which has been further developed since its release. In addition, the Thunar file manager, among other components, has received significant improvements.

### Xorg

As before, Xorg provides a way to build your own system based on a preinstalled X server. This currently still works with all the desktop environments we provide, but starting with Plasma 6.8, it will no longer work with KDE and LXQt.

Fluxbox serves as the window manager, offering an extremely fast and resource-efficient environment for the X Window System. This also makes Xorg a suitable starting point for users who cannot or do not yet want to use Wayland.

### NOX

NOX differs from Xorg in that it does not include an X server. With the revised cli-installer (see below), installation on a modern UEFI/GPT system is now also possible.

### cli-installer

For siduction 2026.1.0, the cli-installer has been completely modernized. It is included in all editions.

The main highlight is the integration of the systemd-boot boot manager, which is now available as an installation option in all editions. For users with straightforward hardware configurations, systemd-boot is a good choice.

The revised cli-installer guides users through the configuration process, suggests appropriate actions, checks dependencies and prerequisites, and provides information about the selected settings. The program can be canceled at any time.

With the introduction of Calamares as the graphical installer, the underlying fll-installer gradually lost importance. As a result, both the cli-installer and fll-installer had remained largely unchanged since 2018. Since siduction intends to continue providing a NOX edition, both installers required a fundamental overhaul to integrate modern features.

To clarify: While the cli-installer provides the user interface, the fll-installer is the actual tool working in the background that writes the data to the disk.

The most important changes:

- Updated outdated commands, checks, and dialogs.
- Non-free sources are now opt-in.
- Full UEFI/GPT support.
- Support for the Btrfs filesystem, including the creation of siduction's standard Subvolumes.
- Choice between the systemd-boot and GRUB boot managers.
- Consistent user interface across all dialogs.
- Removal of graphical interface components.

### Btrfs Filesystem

When using the Btrfs filesystem with siduction, we make it possible to manage your snapshots with [Snapper](https://documentation.suse.com/de-de/sles/12-SP5/html/SLES-all/cha-snapper.html), a tool developed by SUSE. A dedicated chapter in the [siduction manual](https://manual.siduction.org/index_en.html) under System Administration → Btrfs and Snapper, covers this functionality.

The Btrfs Assistant application has now been added. It is available to users of graphical desktop environments and replaces snapper-gui.

**Excerpt from the siduction-btrfs documentation:**

siduction-btrfs can be used on systems with either MBR or GPT partition tables, with or without a separate /boot partition.

Since version 0.3.0, siduction-btrfs uses the Snapper plugin directory.

**When using the GRUB boot manager**

After a rollback, the /boot/grub/grub.cfg file is regenerated in the rollback target using chroot, and GRUB is then reinstalled from within that target. This allows users to boot directly into the rollback target with a simple reboot.

All other Subvolumes, including the previously used one, remain accessible through the siduction snapshots submenu.

When the /boot/grub/grub.cfg file is updated during software installation or an upgrade, the grub-menu-title script adds the edition and Subvolume information to the default boot entry's menu title.

**When using the systemd-boot boot manager**

After a rollback, the rollback-sd-boot script creates the boot entries, considering all kernels contained in the rollback target. The default boot entry is set to the rollback target, which is now the default Subvolume.

If a Subvolume with existing boot entries is deleted, those entries are also removed.

**Snapper Snapshot Descriptions**

After an APT operation, the snapshot-description script replaces the generic description (apt) displayed by Snapper with a more informative text.

**Changelog:**

siduction-btrfs (0.2.0) unstable; urgency=medium

- Added support for systemd-boot.
- Removed installation dependencies on grub-common and grub-btrfs.
    - Together, these changes enable a complete migration from GRUB to systemd-boot.
- Improved snapshot descriptions in Snapper.

siduction-btrfs (0.3.0-1) unstable; urgency=medium

- Rewritten to use the Snapper plugin directory.
- Added support for a separate boot partition when using GRUB.

### onoff

This small script replaces the removed init command. It restores the functionality of init 0 through init 6, which was removed by systemd 258~rc1-1, allowing users to change system states on a running system.

To switch to another system state, simply enter onoff, followed by the number of the desired state, in a terminal with root privileges. This eliminates the need to remember the longer systemd commands.

### Non-free and Contrib

The following non-free and contrib packages are installed by default:

Non-free:

- amd64-microcode – Processor microcode firmware for AMD CPUs
- firmware-amd-graphics – Binary firmware for AMD/ATI graphics chips
- firmware-atheros – Binary firmware for Atheros wireless cards
- firmware-bnx2 – Binary firmware for Broadcom NetXtremeII
- firmware-bnx2x – Binary firmware for Broadcom NetXtreme II 10Gb
- firmware-brcm80211 – Binary firmware for Broadcom 802.11 wireless cards
- firmware-crystalhd – Crystal HD Video Decoder firmware
- firmware-intelwimax – Binary firmware for Intel WiMAX Connection
- firmware-iwlwifi – Binary firmware for Intel wireless cards
- firmware-libertas – Binary firmware for Marvell Libertas 8xxx wireless cards
- firmware-linux-nonfree – Binary firmware for various drivers in the Linux kernel
- firmware-misc-nonfree – Binary firmware for various drivers in the Linux kernel
- firmware-myricom – Firmware for Myri-10G Ethernet adapters
- firmware-netxen – Firmware for QLogic Intelligent Ethernet (3000)
- firmware-qlogic – Binary firmware for QLogic HBAs
- firmware-realtek – Binary firmware for Realtek wired/Wi-Fi/Bluetooth adapters
- firmware-ti-connectivity – Binary firmware for TI Connectivity wireless networking
- firmware-zd1211 – Binary firmware for the zd1211rw wireless driver
- firmware-sof-signed – Intel audio firmware
- intel-microcode – Processor microcode firmware for Intel CPUs

Contrib:

- b43-fwcutter – Utility for extracting Broadcom 43xx firmware
- firmware-b43-installer – Firmware installer for the b43 driver
- firmware-b43legacy-installer – Firmware installer for the b43legacy driver
- iucode-tool – Intel processor microcode utility

### Removing Non-free Software

If you opted to install non-free software in Calamares but later change your mind, you can use the vrms (Virtual Richard Stallman) command to identify non-free packages installed on your system.

You can remove unwanted packages manually or use the command `apt purge $(vrms -s)` to remove them all at once, including their configuration files. Our remove-nonfree script achieves the same result.

### Installation Notes and Known Issues

If you want to reuse an existing home partition (or another data partition), you should configure this after installation rather than in the Calamares installer.

On some devices with Intel GPUs, the live system may freeze shortly after booting. To resolve this issue, set the kernel parameter `intel_iommu=igfx_off` before booting again.

### Credits for siduction 2026.1.0

Core Team:

Torsten Wohlfarth (towo)

Hendrik Lehmbruch (hendrikL)

Axel Konrad (akli)

Vinzenz Vietzke (vinzv)

Ferdinand Thommes (devil)

Former Contributors:

Alf Gaida (agaida) (eaten by the cat)

Axel Beu 2021†

Markus Meyer (coruja)

Server & Hosting

Stefan (sla)

### Our Thanks Go to Everyone Involved and Our Loyal Users!

We would like to thank all of you, all our testers, and everyone who has supported us over the years. This release is also your achievement.

With this release, we would also like to thank the KDE community for providing an excellent desktop environment.

And now, enjoy!

On behalf of the siduction team:

Ferdinand Thommes
