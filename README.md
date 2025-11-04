# Ansible Role - wipe-disks

Ansible role for wiping disks with multiple methods:

### `dd_lazy`

This is a quicker option that wipes the filesystem signatures and writes zeroes to the first 10MB of the device.

### `dd_full`

This is a much slower but complete option that writes zeroes to the full device. This role does not current run multiple disks in parallel, but this is something I am interested in looking into.

### `blkdiscard`

This is a faster full discard for supported SSDs.

### Customisation

There are a few variables that can be used to adjust the above options:

```
# Input device for overwriting the disk path, recommend /dev/zero or /dev/urandom
wipe_disks_dd_input: "/dev/zero"

# Block size for overwriting the disk path
wipe_disks_dd_blocksize: "1M"

# Number of blocks to overwrite in dd_lazy mode
wipe_disks_dd_lazy_count: "10"
```
