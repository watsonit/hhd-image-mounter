# hhd-image-mounter
Create and mount virtual drive images with optional encryption
The two executable shell scripts automate the creation, optional encryption, and mounting of a drive image having specified size. See **Automation Scripts** below.

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

