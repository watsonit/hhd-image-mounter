# Encrypted Drive Images

[How to encrypt files on Linux](https://devconnected.com/how-to-encrypt-file-on-linux/)

[Creating Virtual Disks Using Linux Command Line](http://www.linuxandubuntu.com/home/creating-virtual-disks-using-linux-command-line)

[How to generate a random string? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/230673/how-to-generate-a-random-string#230676)

Based on content found in the above, write a script to

* Create a disk image of specified size
* Format the image and create partitions
* Generate a random password
* Encrypt the image using gpg 
* Decrypt the image and mount



Note that all scripting is based in the **fish** shell.

## create the image

```bash
dd if=/dev/zero of=$img_name bs=1M count=$count		# count is Mb * 1024 to create n GB image
```

## format the image

```bash
printf "g\nn\n\n\nw\n" | sudo fdisk $img_name
#   then commands g (use GPT table), n (create it now), w (write changes)
echo "-- mkfs.ext4 $img_name"
mkfs.ext4 $img_name		# may not be needed
```

## create the loopback device and mount

```bash
set dev (sudo losetup -Pf --show $img_name)
if not test -d /media/$mountpoint
	sudo mkdir /media/$mountpoint
	sudo chown jim.jim /media/$mountpoint
end
sudo mount $dev $mountpoint		# where $mountpoint is derived in the script; something like /media/<name>
```



Upon unmount and reboot, the loopback device will be cleared from the kernel.



# Automation Scripts

## virtualhdd

Creates the virtual drive image.

`/home/jim/Dropbox/dev/encrypted_disk_images/virtualhdd`

```bash
virtualhdd --image=<image name> --size=<size in GB> [--encrypted]
      if drive is to be encrypted, specify --encrypted
```

## mountvhd

Mounts the drive image.

`/home/jim/Dropbox/dev/encrypted_disk_images/mountvhd`

```bash
mountvhd --image=<image name> --mountpoint=<mount path> [--encrypted]
```

