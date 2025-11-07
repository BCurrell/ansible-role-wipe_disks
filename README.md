# Ansible Role - wipe-disks

Ansible role for wiping disks with multiple methods.

### Usage

In your inventory, add a list called `wipe_disks` that contains objects with the following structure:

```yaml
- path: "<disk_path>"
  type: "[type]"
  dd_if: "[dd_if]"
  dd_bs: "[dd_bs]"
  dd_lazy_count: "[dd_lazy_count]"
  dd_extra: "[dd_extra]"
  blkdiscard_secure: false
```

The only required variable is `<disk_path>`: the path to the disk device that you are wiping.

`[type]` is an optional variable that sets the type of wipe you want to apply to a disk. This overrides `wipe_disks_default_type`.

There are also optional variables depending on the type.

##### `dd_lazy`

This is a quicker option that writes zeroes to the first 10MB of the device.

Optional variables:

- `[dd_if] (string)` can be set to the input path that is written to the disk. This overrides `wipe_disks_default_dd_if`.
- `[dd_bs] (string)` can be set to the block size that is written to the disk. This overrides `wipe_disks_default_dd_bs`.
- `[dd_lazy_count] (integer)` can be set to the number of blocks to write to the disk. This overrides `wipe_disks_default_dd_lazy_count`.
- `[dd_extra] (string)` can be set to add additional flags to the `dd` command. This overrides `wipe_disks_default_dd_extra`.

##### `dd_full`

This is a much slower but complete option that writes zeroes to the full device. This role does not current run multiple disks in parallel, but this is something I am interested in looking into.

Optional variables:

- `[dd_if] (string)` can be set to the input path that is written to the disk. This overrides `wipe_disks_default_dd_if`.
- `[dd_bs] (string)` can be set to the block size that is written to the disk. This overrides `wipe_disks_default_dd_bs`.
- `[dd_extra] (string)` can be set to add additional flags to the `dd` command. This overrides `wipe_disks_default_dd_extra`.

##### `blkdiscard`

This is a faster full discard for supported SSDs.

Optional variables:

- `[blkdiscard_secure] (boolean)` can be set to enable a secure discard rather than the default. This overrides `wipe_disks_default_blkdiscard_secure`.

### Defaults

Below is a list of overridable defaults and their values in the role.

```yaml
# Default type if not specified in wipe_disks list object
wipe_disks_default_type: "dd_lazy"

# Default dd input filesystem (if) argument if not specified in wipe_disks list object
# Recommended to use /dev/zero or /dev/urandom
wipe_disks_default_dd_if: "/dev/zero"

# Default dd block size (bs) argument if not specified in wipe_disks list object
wipe_disks_default_dd_bs: "1M"

# Default dd_lazy count argument if not specified in wipe_disks list object
wipe_disks_default_dd_lazy_count: "10"

# Default dd extra arguments if not specified in wipe_disks list object
wipe_disks_default_dd_extra: "conv=sync,noerror"

# Default blkdiscard secure mode if not specified in wipe_disks list object
wipe_disks_default_blkdiscard_secure: false
```