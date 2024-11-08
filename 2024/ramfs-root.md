# Running Rasbperry OS Lite entirely from RAM

Foremost your root must fit in the RAM to even attempt this. I used Rasbperry OS Lite version on my Raspberry Pi 4 with 4 GB of RAM.

If you try this, have a lot of backups ready, because I locked my system many times. I'm not responsible for any damage you do to your system. It's almost guaranteed that you will lock your system if your setup differs from mine. It might be helpful to add the debug `00-shell.sh` to Initramfs first from the end of document before you attempt this. 

If you want to understand how Initramfs and root is handled, read my previous post [Journey of the Linux root file system in boot up](./root.md). After that this makes a lot more sense.

## 1. Create a ramfs root inside Initramfs

Add the following lines to the file:

```bash
$ sudo pico /etc/initramfs-tools/scripts/init-bottom/01-ramfs-root.sh
```

Contents:

```sh
#!/bin/sh

set -e

# This test ensures that the script is not run in the special environment of the initramfs update command, only during boot.
if [ -f /scripts/functions ]; then
    mkdir /oldroot
    mount -o move /root /oldroot
    mount -t ramfs ramfs /root

    # Note: Adding `echo` statements aren't visible during bootup.
    # Following takes a while, for me it was ~3 minutes
    cp -a /oldroot/. /root/
fi
```

Make the file executable:

```sh
$ sudo chmod +x /etc/initramfs-tools/scripts/init-bottom/01-ramfs-root.sh
```

Now, update the initramfs:

```sh
$ sudo update-initramfs -u
```

That's it! 🎉

## 2. Reboot the system and hope it starts up

After bootup see if the root is mounted on ramfs:

```sh
$ mount

ramfs on / type ramfs (rw,noatime)
```

You don't have much memory left though:

```sh
$ cat /proc/meminfo
MemTotal:        3881968 kB
MemFree:          710684 kB
MemAvailable:    1805936 kB
```

## If you get stuck, enter Initramfs' shell during bootup

You need physical keyboard and monitor because Initramfs doesn't have network support. First read the [previous post](./root.md) to understand how the boot process works and see how to debug it more throughly. 

However, entering shell during *Initramfs* boot is the easiest way to experiment with the Initramfs. To do this, add following Initramfs script that just drops you to shell:

```sh
sudo pico /etc/initramfs-tools/scripts/init-bottom/00-shell.sh
sudo chmod +x /etc/initramfs-tools/scripts/init-bottom/00-shell.sh
```

```sh
#!/bin/sh

if [ -f /scripts/functions ]; then
    . /scripts/functions
    panic "Dropping to shell!"
fi
```

Now, update the initramfs:

```sh
$ sudo update-initramfs -u
```

When you bootup you should get to shell with prompt `(initramfs)`. From here you can try to mount the root manually and see what's wrong.

Also typing `exit` will continue the boot process, if you have `01-ramfs-root.sh` script in place, it will run that next.