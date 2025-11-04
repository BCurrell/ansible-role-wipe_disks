# Ansible Role - wipe-disks

Ansible role for wiping disks with 2 types: lazy vs full

### Lazy

This is a quicker option that wipes the filesystem signatures and writes zeroes to the first 10MB of the device.

### Full

This is a much slower but complete option that writes zeroes to the full device. This role does not current run multiple disks in parallel, but this is something I am interested in looking into.
