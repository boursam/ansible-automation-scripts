# Data Partitioning

Automates disk partitioning and mounting a dedicated data volume using **LVM** (Logical Volume Manager) on Debian/Ubuntu targets.

This playbook takes a raw block device, partitions it, builds a physical volume → volume group → logical volume on top of it, formats it with `ext4`, and mounts it persistently by UUID.

---

## What it does

1. Installs the `lvm2` package
2. Creates a GPT partition on the target disk (`disk_device`)
3. Creates a physical volume (PV) on that partition
4. Creates a volume group (VG) from the PV
5. Creates a logical volume (LV) using 100% of the available space
6. Formats the LV with an `ext4` filesystem
7. Creates the mount point directory
8. Retrieves the filesystem UUID
9. Mounts the LV persistently via `/etc/fstab` (by UUID, with `nofail`)
10. Displays disk usage (`df -h`) for verification

---

## Run

```bash
ansible-playbook -i inventory.ini install.yml
```

---

## Variables

| Variable | Default | Description |
|---|---|---|
| `disk_device` | `/dev/sdb` | Raw disk to partition |
| `partition_number` | `1` | Partition number to create on the disk |
| `vg_name` | `data-vg` | Name of the LVM volume group |
| `lv_name` | `data-lv` | Name of the LVM logical volume |
| `mount_point` | `/data` | Directory where the volume will be mounted |
| `fs_type` | `ext4` | Filesystem type used to format the logical volume |

---

## Requirements

- Debian/Ubuntu target hosts (uses the `apt` module)
- Ansible collection `ansible.posix` (for the `mount` module)
  ```bash
  ansible-galaxy collection install ansible.posix
  ```
- A raw, unpartitioned (or reusable) block device available on the target (default: `/dev/sdb`)
- `sudo`/`root` privileges on the target

---

## Warning

This playbook **partitions and formats a disk**. Double-check `disk_device` before running — running it against the wrong device (e.g. your OS disk) will result in **data loss**. There is no confirmation prompt; it runs unattended like any Ansible playbook.

It is safe to re-run only if the target state (partition, VG, LV, filesystem, mount) is unchanged — Ansible modules used here are idempotent, but the initial partitioning step should only be done once per disk.

---

## Notes

- The partition is created as **GPT**, using the full disk (`1MiB` → `100%`) — no manual `fdisk`/`parted` interaction needed.
- The logical volume consumes **100% of free space** in the volume group by default (`size: 100%FREE`).
- The mount uses `nofail` in `fstab` so the system still boots even if the disk is missing/unavailable at boot time.
- Mounting by **UUID** (rather than device path) avoids issues if device names shift (e.g. `/dev/sdb` becoming `/dev/sdc` after a reboot).
