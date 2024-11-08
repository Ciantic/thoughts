# Journey of the Linux root file system in boot up

Following examples are with Raspbian Bookworm and Raspberry Pi 4. Partition layout was this:

```
$ lsblk
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda      8:0    1  3.7G  0 disk
├─sda1   8:1    1  512M  0 part /boot/firmware
└─sda2   8:2    1  3.2G  0 part /
```

Bootloader stored in `/boot/firmware/` starts up Linux Kernel's main function `start_kernel` with command line parameters defined in the `/boot/firmware/cmdline.txt` and `/boot/firmware/config.txt`. Note one setting which is `auto_initramfs=1`. Raspberry Pi's Initramfs root file system is stored in CPIO-archive `/boot/initrd.img-6.6.51+rpt-rpi-v8` which is relative to normal root partition. Kernel uses identical copy of this file positioned in the `/boot/firmware/initramfs8` which is in the bootloader partition.

## Initramfs

Initramfs is feature of the Linux Kernel, it creates temporary root file system (`/`) stored in RAM from given files before actual boot up of the distribution. Distributor author creates the root file system in CPIO-archive format, and Kernel extracts it to RAM. After Kernel has extracted the file system it can start executing it from `/init` in the root of the file system. 

In Raspberry Pi the CPIO-archive is stored in `/boot/initrd.img-6.6.51+rpt-rpi-v8` and is additionally compressed with `zstd`. You can modify these CPIO-archives and append your own files, and run your own functionality in the Initramfs scripts. To add new scripts to be run in this environment you must have `initramfs-tools` package installed. 

For debugging how all of this works, first add `debug` kernel parameter to `/boot/firmware/cmdline.txt`:

```txt
console=serial0,115200 console=tty1 root=PARTUUID=a66e351c-02 rootfstype=ext4 fsck.repair=yes rootwait cfg80211.ieee80211_regdom=FI debug
```

If you boot up the system and look at the `dmesg` you should see these lines:

```txt
$ dmesg
...
[    0.000000] Kernel command line: coherent_pool=1M 8250.nr_uarts=0 snd_bcm2835.enable_headphones=0 cgroup_disable=memory numa_policy=interleave snd_bcm2835.enable_headphones=1 snd_bcm2835.enable_hdmi=1 snd_bcm2835.enable_hdmi=0  smsc95xx.macaddr=DC:A6:32:03:A1:95 vc_mem.mem_base=0x3eb00000 vc_mem.mem_size=0x3ff00000  console=ttyS0,115200 console=tty1 root=PARTUUID=a66e351c-02 rootfstype=ext4 fsck.repair=yes rootwait cfg80211.ieee80211_regdom=FI debug
...
[    1.092378] Trying to unpack rootfs image as initramfs...
```

Where kernel started and with which parameters, and where Initramfs was unpacked.

After booting up the system with `debug` in the command line it also created a file `/run/initramfs/initramfs.debug` which shows the executed commands within the Initramfs, here is an example output:

<details>
<summary>Click to see the debug log</summary>

```bash
$ cat /run/initramfs/initramfs.debug

+ unset log_output
+ maybe_break top
+ run_scripts /scripts/init-top
+ initdir=/scripts/init-top
+ '[' '!' -d /scripts/init-top ]
+ shift
+ . /scripts/init-top/ORDER
+ /scripts/init-top/all_generic_ide
+ '[' -e /conf/param.conf ]
+ /scripts/init-top/blacklist
+ '[' -e /conf/param.conf ]
+ /scripts/init-top/keymap
+ '[' -e /conf/param.conf ]
+ /scripts/init-top/udev
Starting systemd-udevd version 252.30-1~deb12u2
+ '[' -e /conf/param.conf ]
+ maybe_break modules
+ '[' n '!=' y ]
+ log_begin_msg 'Loading essential drivers'
+ _log_msg 'Begin: %s ... ' 'Loading essential drivers'
+ '[' n '=' y ]
+ printf 'Begin: %s ... ' 'Loading essential drivers'
Begin: Loading essential drivers ... + return 0
+ '[' -n  ]
+ load_modules
+ '[' -e /conf/modules ]
+ '[' n '!=' y ]
+ log_end_msg
+ _log_msg 'done.\n'
+ '[' n '=' y ]
+ printf 'done.\n'
done.
+ return 0
+ _uptime
+ local uptime
+ cat /proc/uptime
+ uptime='2.21 5.65'
+ uptime=2
+ echo 2
+ starttime=2
+ starttime=3
+ export starttime
+ '['  ]
+ maybe_break premount
+ '[' n '!=' y ]
+ log_begin_msg 'Running /scripts/init-premount'
+ _log_msg 'Begin: %s ... ' 'Running /scripts/init-premount'
+ '[' n '=' y ]
+ printf 'Begin: %s ... ' 'Running /scripts/init-premount'
Begin: Running /scripts/init-premount ... + return 0
+ run_scripts /scripts/init-premount
+ initdir=/scripts/init-premount
+ '[' '!' -d /scripts/init-premount ]
+ return
+ '[' n '!=' y ]
+ log_end_msg
+ _log_msg 'done.\n'
+ '[' n '=' y ]
+ printf 'done.\n'
done.
+ return 0
+ maybe_break mount
+ log_begin_msg 'Mounting root file system'
+ _log_msg 'Begin: %s ... ' 'Mounting root file system'
+ '[' n '=' y ]
+ printf 'Begin: %s ... ' 'Mounting root file system'
Begin: Mounting root file system ... + return 0
+ . /scripts/local
+ . /scripts/nfs
+ . /scripts/local
+ parse_numeric 'PARTUUID=a66e351c-02'
+ return
+ maybe_break mountroot
+ mount_top
+ local_top
+ '['  '!=' yes ]
+ '[' n '!=' y ]
+ log_begin_msg 'Running /scripts/local-top'
+ _log_msg 'Begin: %s ... ' 'Running /scripts/local-top'
+ '[' n '=' y ]
+ printf 'Begin: %s ... ' 'Running /scripts/local-top'
Begin: Running /scripts/local-top ... + return 0
+ run_scripts /scripts/local-top
+ initdir=/scripts/local-top
+ '[' '!' -d /scripts/local-top ]
+ return
+ '[' n '!=' y ]
+ log_end_msg
+ _log_msg 'done.\n'
+ '[' n '=' y ]
+ printf 'done.\n'
done.
+ return 0
+ local_top_used=yes
+ mount_premount
+ local_premount
+ '['  '!=' yes ]
+ '[' n '!=' y ]
+ log_begin_msg 'Running /scripts/local-premount'
+ _log_msg 'Begin: %s ... ' 'Running /scripts/local-premount'
+ '[' n '=' y ]
+ printf 'Begin: %s ... ' 'Running /scripts/local-premount'
Begin: Running /scripts/local-premount ... + return 0
+ run_scripts /scripts/local-premount
+ initdir=/scripts/local-premount
+ '[' '!' -d /scripts/local-premount ]
+ shift
+ . /scripts/local-premount/ORDER
+ /scripts/local-premount/firstboot
+ '[' -e /conf/param.conf ]
+ /scripts/local-premount/ntfs_3g
+ '[' -e /conf/param.conf ]
+ /scripts/local-premount/resume
+ '[' -e /conf/param.conf ]
+ '[' n '!=' y ]
+ log_end_msg
+ _log_msg 'done.\n'
+ '[' n '=' y ]
+ printf 'done.\n'
done.
+ return 0
+ local_premount_used=yes
+ mountroot
+ local_mount_root
+ local_top
+ '[' yes '!=' yes ]
+ local_top_used=yes
+ '[' -z 'PARTUUID=a66e351c-02' ]
+ local_device_setup 'PARTUUID=a66e351c-02' 'root file system'
+ local 'dev_id=PARTUUID=a66e351c-02'
+ local 'name=root file system'
+ local 'may_panic=true'
+ local real_dev
+ local time_elapsed
+ local count
+ wait_for_udev 10
+ command -v udevadm
+ udevadm settle '--timeout=10'
+ '[' -n  ]
+ '[' 'PARTUUID=a66e351c-02' '=' 'PARTUUID=a66e351c-02' ]
+ '[' a66e351c-02 '=' 'PARTUUID=a66e351c-02' ]
+ resolve_device 'PARTUUID=a66e351c-02'
+ DEV='PARTUUID=a66e351c-02'
+ blkid -l -t 'PARTUUID=a66e351c-02' -o device
+ DEV=
+ return 1
+ real_dev=
+ log_begin_msg 'Waiting for root file system'
+ _log_msg 'Begin: %s ... ' 'Waiting for root file system'
+ '[' n '=' y ]
+ printf 'Begin: %s ... ' 'Waiting for root file system'
Begin: Waiting for root file system ... + return 0
+ slumber=30
+ '[' 0 -gt 30 ]
+ true
+ sleep 1
+ time_elapsed
+ '[' -z 3 ]
+ local delta
+ _uptime
+ local uptime
+ cat /proc/uptime
+ uptime='3.33 9.92'
+ uptime=3
+ echo 3
+ delta=3
+ delta=0
+ echo 0
+ time_elapsed=0
+ local_block 'PARTUUID=a66e351c-02'
+ '[' n '!=' y ]
+ log_begin_msg 'Running /scripts/local-block'
+ _log_msg 'Begin: %s ... ' 'Running /scripts/local-block'
+ '[' n '=' y ]
+ printf 'Begin: %s ... ' 'Running /scripts/local-block'
Begin: Running /scripts/local-block ... + return 0
+ run_scripts /scripts/local-block 'PARTUUID=a66e351c-02'
+ initdir=/scripts/local-block
+ '[' '!' -d /scripts/local-block ]
+ return
+ '[' n '!=' y ]
+ log_end_msg
+ _log_msg 'done.\n'
+ '[' n '=' y ]
+ printf 'done.\n'
done.
+ return 0
+ true
+ '[' -f /run/count.mdadm.initrd ]
+ '[' -n  ]
+ break
+ resolve_device 'PARTUUID=a66e351c-02'
+ DEV='PARTUUID=a66e351c-02'
+ blkid -l -t 'PARTUUID=a66e351c-02' -o device
+ DEV=/dev/sda2
+ '[' -e /dev/sda2 ]
+ echo /dev/sda2
+ real_dev=/dev/sda2
+ get_fstype /dev/sda2
+ local FS FSTYPE
+ FS=/dev/sda2
+ FSTYPE=unknown
+ fstype /dev/sda2
+ eval 'FSTYPE=ext4
FSSIZE=3481272320'
+ FSTYPE=ext4
+ FSSIZE=3481272320
+ '[' ext4 '=' unknown ]
+ echo ext4
+ return 0
+ wait_for_udev 10
+ command -v udevadm
+ udevadm settle '--timeout=10'
+ log_end_msg 0
+ _log_msg 'done.\n'
+ '[' n '=' y ]
+ printf 'done.\n'
done.
+ return 0
+ break
+ resolve_device 'PARTUUID=a66e351c-02'
+ DEV='PARTUUID=a66e351c-02'
+ blkid -l -t 'PARTUUID=a66e351c-02' -o device
+ DEV=/dev/sda2
+ '[' -e /dev/sda2 ]
+ echo /dev/sda2
+ real_dev=/dev/sda2
+ get_fstype /dev/sda2
+ local FS FSTYPE
+ FS=/dev/sda2
+ FSTYPE=unknown
+ fstype /dev/sda2
+ eval 'FSTYPE=ext4
FSSIZE=3481272320'
+ FSTYPE=ext4
+ FSSIZE=3481272320
+ '[' ext4 '=' unknown ]
+ echo ext4
+ return 0
+ DEV=/dev/sda2
+ ROOT=/dev/sda2
+ '[' -z ext4 ]
+ '[' ext4 '=' auto ]
+ FSTYPE=ext4
+ local_premount
+ '[' yes '!=' yes ]
+ local_premount_used=yes
+ '[' y '=' y ]
+ roflag=-r
+ checkfs /dev/sda2 root ext4
+ _checkfs_once /dev/sda2 root ext4
+ DEV=/dev/sda2
+ NAME=root
+ TYPE=ext4
+ '[' root '=' / ]
+ FSCK_LOGFILE=/run/initramfs/fsck.log
+ FSCK_STAMPFILE=/run/initramfs/fsck-root
+ '[' ext4 '=' auto ]
+ FSCKCODE=0
+ '[' -z ext4 ]
+ command -v fsck
+ '[' n '=' y ]
+ '[' n '=' y ]
+ force=
+ '[' y '=' y ]
+ fix=-y
+ spinner=
+ '[' -z y ]
+ '[' n '=' n ]
+ log_begin_msg 'Will now check root file system'
+ _log_msg 'Begin: %s ... ' 'Will now check root file system'
+ '[' n '=' y ]
+ printf 'Begin: %s ... ' 'Will now check root file system'
Begin: Will now check root file system ... + return 0
+ logsave -a -s /run/initramfs/fsck.log fsck -y -V -t ext4 /dev/sda2
fsck from util-linux 2.38.1
[/sbin/fsck.ext4 (1) -- /dev/sda2] fsck.ext4 -y /dev/sda2 
e2fsck 1.47.0 (5-Feb-2023)
rootfs: clean, 69756/205088 files, 656193/849920 blocks
+ FSCKCODE=0
+ log_end_msg
+ _log_msg 'done.\n'
+ '[' n '=' y ]
+ printf 'done.\n'
done.
+ return 0
+ '[' 0 -eq 32 ]
+ '[' 0 -eq 4 ]
+ '[' 0 -gt 1 ]
+ true
+ return 0
+ mount -r -t ext4 /dev/sda2 /root
+ log_end_msg
+ _log_msg 'done.\n'
+ '[' n '=' y ]
+ printf 'done.\n'
done.
+ return 0
+ read_fstab_entry /usr
+ found=1
+ '[' -f /root/etc/fstab ]
+ read -r MNT_FSNAME MNT_DIR MNT_TYPE MNT_OPTS MNT_FREQ MNT_PASS MNT_JUNK
+ '[' /proc '=' /usr ]
+ read -r MNT_FSNAME MNT_DIR MNT_TYPE MNT_OPTS MNT_FREQ MNT_PASS MNT_JUNK
+ '[' /boot/firmware '=' /usr ]
+ read -r MNT_FSNAME MNT_DIR MNT_TYPE MNT_OPTS MNT_FREQ MNT_PASS MNT_JUNK
+ '[' / '=' /usr ]
+ read -r MNT_FSNAME MNT_DIR MNT_TYPE MNT_OPTS MNT_FREQ MNT_PASS MNT_JUNK
+ continue
+ read -r MNT_FSNAME MNT_DIR MNT_TYPE MNT_OPTS MNT_FREQ MNT_PASS MNT_JUNK
+ continue
+ read -r MNT_FSNAME MNT_DIR MNT_TYPE MNT_OPTS MNT_FREQ MNT_PASS MNT_JUNK
+ return 1
+ mount_bottom
+ local_bottom
+ '[' yes '=' yes ]
+ '[' n '!=' y ]
+ log_begin_msg 'Running /scripts/local-bottom'
+ _log_msg 'Begin: %s ... ' 'Running /scripts/local-bottom'
+ '[' n '=' y ]
+ printf 'Begin: %s ... ' 'Running /scripts/local-bottom'
Begin: Running /scripts/local-bottom ... + return 0
+ run_scripts /scripts/local-bottom
+ initdir=/scripts/local-bottom
+ '[' '!' -d /scripts/local-bottom ]
+ shift
+ . /scripts/local-bottom/ORDER
+ /scripts/local-bottom/firstboot_fstrim
+ '[' -e /conf/param.conf ]
+ /scripts/local-bottom/imager_fixup
+ '[' -e /conf/param.conf ]
+ /scripts/local-bottom/ntfs_3g
+ '[' -e /conf/param.conf ]
+ '[' n '!=' y ]
+ log_end_msg
+ _log_msg 'done.\n'
+ '[' n '=' y ]
+ printf 'done.\n'
done.
+ return 0
+ local_premount_used=no
+ local_top_used=no
+ nfs_bottom
+ '['  '=' yes ]
+ '['  '=' yes ]
+ nfs_premount_used=no
+ nfs_top_used=no
+ local_bottom
+ '[' no '=' yes ]
+ '[' no '=' yes ]
+ local_premount_used=no
+ local_top_used=no
+ maybe_break bottom
+ '[' n '!=' y ]
+ log_begin_msg 'Running /scripts/init-bottom'
+ _log_msg 'Begin: %s ... ' 'Running /scripts/init-bottom'
+ '[' n '=' y ]
+ printf 'Begin: %s ... ' 'Running /scripts/init-bottom'
Begin: Running /scripts/init-bottom ... + return 0
+ run_scripts /scripts/init-bottom
+ initdir=/scripts/init-bottom
+ '[' '!' -d /scripts/init-bottom ]
+ shift
+ . /scripts/init-bottom/ORDER
+ /scripts/init-bottom/ramfiles.sh # <---------- notice I had created my own test file in here
+ '[' -e /conf/param.conf ]
+ /scripts/init-bottom/udev
+ '[' -e /conf/param.conf ]
+ '[' n '!=' y ]
+ log_end_msg
+ _log_msg 'done.\n'
+ '[' n '=' y ]
+ printf 'done.\n'
done.
+ return 0
+ mount -n -o move /run /root/run
+ validate_init /sbin/init
+ run-init -n /root /sbin/init
+ validate_init /sbin/init
+ run-init -n /root /sbin/init
+ maybe_break init
+ unset debug
+ unset MODPROBE_OPTIONS
+ unset DPKG_ARCH
+ unset ROOTFLAGS
+ unset ROOTFSTYPE
+ unset ROOTDELAY
+ unset ROOT
+ unset IP
+ unset BOOT
+ unset BOOTIF
+ unset DEVICE
+ unset UBIMTD
+ unset blacklist
+ unset break
+ unset noresume
+ unset panic
+ unset quiet
+ unset readonly
+ unset resume
+ unset resume_offset
+ unset noresume
+ unset fastboot
+ unset forcefsck
+ unset fsckfix
+ unset starttime
+ mount -n -o move /sys /root/sys
+ mount -n -o move /proc /root/proc
+ exec run-init /root /sbin/init
```
</details>

If you want to follow the debug output it is also helpful to extract the Initramfs CPIO-archive and look at the scripts, specifically `/scripts/local`. You can extract the CPIO-archive with `unzstd` and `cpio` commands. Since we are interested of the root file system, we will look at the implementation of the `local_mount_root` function in the `/scripts/local` script:

```bash
$ mkdir -p /home/pi/initramfs-contents
$ cd /home/pi/initramfs-contents
$ sudo cat /boot/initrd.img-6.6.51+rpt-rpi-v8 | unzstd -- | cpio -idvm
$ sudo chown -R pi:pi .

# Then view the local script responsible for mounting the root file system
$ cat ./scripts/local

# ...
local_mount_root()
{
  local_top
  if [ -z "${ROOT}" ]; then
    panic "No root device specified. Boot arguments must include a root= parameter."
  fi
  local_device_setup "${ROOT}" "root file system"
  ROOT="${DEV}"

  # Get the root filesystem type if not set
  if [ -z "${ROOTFSTYPE}" ] || [ "${ROOTFSTYPE}" = auto ]; then
    FSTYPE=$(get_fstype "${ROOT}")
  else
    FSTYPE=${ROOTFSTYPE}
  fi

  local_premount

  if [ "${readonly?}" = "y" ]; then
    roflag=-r
  else
    roflag=-w
  fi

  checkfs "${ROOT}" root "${FSTYPE}"

  # Mount root
  # shellcheck disable=SC2086
  if ! mount ${roflag} ${FSTYPE:+-t "${FSTYPE}"} ${ROOTFLAGS} "${ROOT}" "${rootmnt?}"; then
    panic "Failed to mount ${ROOT} as root file system."
  fi
}
# ...

```

The Initramfs mounts the root file system as read-only by default, but it also runs `checkfs` before mounting the root file system. If you want to understand how the Initramfs starts up then read the contents of `/init` script inside the CPIO-archive, it contains for example the defined variables like: 

```
export init=/sbin/init
export readonly=y
export rootmnt=/root
```

Slight detour from understanding root file system, but interesting nonetheless is to how to add your own functionality to Initramfs image. Notice the script points in the debug log `init-bottom`, ` init-premount`, `init-top`, `local-bottom`, `local-premount`, `local-top` these are points where you can execute your own setup scripts within the Initramfs. Suppose you want to mount something before the distribution's INIT-call but not via fstab, you could create a script e.g., `/etc/initramfs-tools/scripts/init-bottom/ramfiles.sh` :

```bash
$ sudo pico /etc/initramfs-tools/scripts/init-bottom/ramfiles.sh

# Will be executed in initramfs `init-bottom` script point
#!/bin/sh
mkdir -p /my-example-ram
mount -t tmpfs -o size=10M none /my-example-ram
mount -n -o move /my-example-ram /root/my-example-ram

# Make it also executable
$ sudo chmod +x /etc/initramfs-tools/scripts/init-bottom/ramfiles.sh

# Create the /my-example-ram root point to your file system
$ sudo mkdir -p /my-example-ram

# Then recreate the initramfs cpio archive with initramfs-tools:
$ sudo update-initramfs -u 
```

This will recreate `/boot/initrd.img-6.6.51+rpt-rpi-v8` with the new file placed in the `/scripts/init-bottom/ramfiles.sh`. If you now boot up your machine you should see the `/my-example-ram` directory in the root:

```bash
$ mount
none on /my-example-ram type tmpfs (rw,relatime,size=10240k)
```

If your script fails or works erroneously, look at the `/run/initramfs/initramfs.debug` file for the error messages.

Finally note from the debug log the call `/sbin/init` which is your distro's INIT-binary which in this case is `systemd`. 

## Systemd `/sbin/init`

Understanding how Systemd works would require mountains of books, but we are interested only the journey of the root file system. First look at the startup tree of Systemd:

```bash
$ systemd-analyze  critical-chain
The time when unit became active or started is printed after the "@" character.
The time the unit took to start is printed after the "+" character.

multi-user.target @33.697s
└─podman-restart.service @14.831s +18.764s
  └─network-online.target @14.797s
    └─NetworkManager-wait-online.service @8.532s +6.261s
      └─NetworkManager.service @6.779s +1.717s
        └─dbus.service @5.929s +808ms
          └─basic.target @5.860s
            └─sockets.target @5.858s
              └─triggerhappy.socket @5.858s
                └─sysinit.target @5.834s
                  └─systemd-timesyncd.service @4.895s +937ms
                    └─systemd-tmpfiles-setup.service @4.467s +334ms
                      └─local-fs.target @4.381s
                        └─run-user-1000.mount @19.300s
                          └─local-fs-pre.target @2.096s
                            └─systemd-tmpfiles-setup-dev.service @1.812s +283ms
                              └─systemd-sysusers.service @1.456s +334ms
                                └─systemd-remount-fs.service @1.308s +133ms
                                  └─systemd-journald.socket @1.182s
                                    └─system.slice @1.139s
                                      └─-.slice @1.139s

```

First important entry is `systemd-remount-fs.service` which remounts the root (`/`) as writable, as it was previously mounted read-only by Initramfs. 

The `systemd-remount-fs.service` is located in the `/usr/lib/systemd/system/systemd-remount-fs.service` file:


```bash
$ cat systemd-remount-fs.service
...
[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/lib/systemd/systemd-remount-fs

```

Now take a look at the source code of [run() function](https://github.com/systemd/systemd/blob/78b032d727e8f9e925c10c6617a1e409307ffc24/src/remount-fs/remount-fs.c#L110) of the `/lib/systemd/systemd-remount-fs`:

```c
static int run(int argc, char *argv[]) {
   // ...
   r = do_remount("/", true, &pids);
   // ...
}
```

It calls function `do_remount()` for the root file system. The [`do_remount` is defined like this](https://github.com/systemd/systemd/blob/78b032d727e8f9e925c10c6617a1e409307ffc24/src/remount-fs/remount-fs.c#L47):

```c
static int do_remount(const char *path, bool force_rw, Hashmap **pids) {
    // ...
    execv(MOUNT_PATH, STRV_MAKE(MOUNT_PATH, path, "-o", force_rw ? "remount,rw" : "remount"));
    // ...
}
```

And that's how it is done, now the root file system is writable again and process continues.
