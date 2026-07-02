# 💽 Linux Disk & Storage Management

## 🖥️ What is Disk & Storage Management?

Disk and Storage Management is the process of organizing, partitioning, formatting, mounting, monitoring, and maintaining storage devices in Linux. It ensures that data is stored efficiently and that disks are available for the operating system and applications.

Disk management helps administrators:

* View available storage devices
* Create and manage disk partitions
* Format disks with different file systems
* Mount and unmount storage devices
* Monitor disk usage
* Configure Logical Volume Management (LVM)
* Manage swap space for virtual memory

> 💡 **Why it matters:** Every Linux system relies on storage devices to store the operating system, applications, user files, and logs. Understanding disk management is essential for system administration, storage expansion, troubleshooting, and performance optimization.

## 💾 Linux Storage Components

A Linux storage device consists of several components:

* Physical Disk (/dev/sdb)
* Partitions (/dev/sdb1)
* File System  (ext4/xfs)
* Mount Point
* Logical Volumes (LVM)
* Swap Space

## 🧩 Understanding Linux Storage

Linux represents storage devices as special files under the **/dev** directory.

Examples, Where:

* `/dev/sda` → First SATA/SCSI disk
* `/dev/sdb` → Second disk
* `/dev/sda1` → First partition on sda
* `/dev/nvme0n1` → NVMe SSD
* `/dev/nvme0n1p1` → First partition on NVMe SSD

### 📦 Block Devices

A **block device** is a storage device that reads and writes data in fixed-size blocks.

Examples:

* Hard Disk Drive (HDD)
* Solid State Drive (SSD)
* NVMe SSD
* USB Flash Drive
* Virtual Disk

#### 🔍 Viewing Disk Information

Linux provides several utilities to inspect storage devices.

| Command        | Purpose                                  |
| -------------- | ---------------------------------------- |
| `lsblk`        | Display block devices and partitions     |
| `fdisk -l`     | Show partition tables                    |
| `blkid`        | Display UUIDs and filesystem information |
| `df -h`        | Show filesystem disk usage               |
| `du -sh /path` | Display directory size                   |

### 💿 Disk Partitions

A partition divides a physical disk into multiple logical sections.

Benefits:

* Organizes storage
* Isolates operating systems
* Separates user data from system files
* Improves storage management

Example:

```
Disk
│
├── Partition 1 (/)
├── Partition 2 (/home)
└── Partition 3 (Swap)
```

#### 🛠️ Partition Management

Linux provides tools to create and manage partitions.

| Command  | Purpose                    |
| -------- | -------------------------- |
| `fdisk`  | Manage MBR partitions      |
| `parted` | Manage GPT and large disks |

Create a partition:

```bash
sudo fdisk /dev/sdb
```

### 🧱 File Systems

A file system organizes how data is stored and retrieved.

Common Linux file systems:

* ext4
* XFS
* Btrfs
* FAT32
* NTFS (supported)

Format a partition as ext4:

```bash
mkfs.ext4 /dev/sdb1
```

Format as XFS:

```bash
mkfs.xfs /dev/sdb1
```

> ⚠️ **Warning:** Formatting permanently erases all data on the selected partition.

### 📂 Mounting File Systems

Before Linux can use a partition, it must be mounted.

Example:

```
Partition
      │
      ▼
Mount Point (/data)
      │
      ▼
Accessible by Users
```

Mount a partition:

```bash
sudo mount /dev/sdb1 /mnt
```

Unmount a partition:

```bash
sudo umount /mnt
```

Remount as read-write:

```bash
sudo mount -o remount,rw /mnt
```

#### 📍 Mount Points

A mount point is a directory where a storage device becomes accessible.

Common mount points:

* `/`
* `/home`
* `/boot`
* `/mnt`
* `/media`
* `/data`

Example:

```bash
mkdir /data
mount /dev/sdb1 /data
```
Now everything stored in `/data` is written to `/dev/sdb1`.

#### 🔄 Persistent Mounting

Temporary mounts disappear after reboot.

To mount automatically during boot, edit:

/etc/fstab

Example entry:

UUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx /data ext4 defaults 0 2

Find the UUID:

```bash
blkid
```

### 📦 Logical Volume Management (LVM)

LVM provides flexible storage management by allowing logical volumes to span one or more physical disks.

Benefits:

* Resize storage dynamically
* Combine multiple disks
* Easier storage expansion
* Better flexibility than traditional partitions

LVM Architecture:

```
Physical Disk
      │
      ▼
Physical Volume (PV)
      │
      ▼
Volume Group (VG)
      │
      ▼
Logical Volume (LV)
      │
      ▼
File System
      │
      ▼
Mount Point
```

#### ⚙️ LVM Commands

Create a Physical Volume:

```bash
pvcreate /dev/sdb
```

Create a Volume Group:

```bash
vgcreate vg_data /dev/sdb
```

Create a Logical Volume:

```bash
lvcreate -L 10G -n lv_backup vg_data
```

Format it:

```bash
mkfs.ext4 /dev/vg_data/lv_backup
```

Mount it:

```bash
mount /dev/vg_data/lv_backup /mnt
```

### 💾 Swap Space

Swap is disk space used as virtual memory when RAM becomes full.

Example:

```
RAM Full
    │
    ▼
Swap Space Used
```

Commands:

Create swap:

```bash
mkswap /dev/sdb2
```

Enable swap:

```bash
swapon /dev/sdb2
```

Disable swap:

```bash
swapoff /dev/sdb2
```

View swap:

```bash
swapon --show
```

## 📊 Monitoring Disk Usage

Useful commands:

| Command       | Purpose                   |
| ---------     | ------------------------- |
| `df -h`       | Display filesystem usage  |
| du -sh /home  | Directory size            |
| `lsblk`       | Show disks and partitions |
| `findmnt`     | Show mounted filesystems  |


## 🔍 When to Use `fdisk`, `mount`, or Both

### ✅ Use `fdisk` When

Use **fdisk** if:

* The disk is brand new
* There are no existing partitions
* You need to create `/dev/sdb1`, `/dev/sdb2`, etc.

### ✅ Use `mount` When

Use **mount** if:

* The partition already exists
* The partition is already formatted
* You simply want to access the storage

### ✅ Use `fdisk + mkfs + mount` When

Use all three commands when setting up a brand-new disk.
```bash
# 1. Check available disks
lsblk
# 2. Create partition
sudo fdisk /dev/sdb
# 3. Format the partition
sudo mkfs.ext4 /dev/sdb1
# 4. Mount it
sudo mkdir /data
sudo mount /dev/sdb1 /data
```
## 🔄 Linux Disk Management Workflow

The diagram below summarizes the complete storage setup process.

New Disk
    │
    ▼
Detect Disk
(lsblk)
    │
    ▼
Partition Disk
(fdisk / parted)
    │
    ▼
Create File System
(mkfs.ext4 / mkfs.xfs)
    │
    ▼
Create Mount Point
(mkdir)
    │
    ▼
Mount File System
(mount)
    │
    ▼
Verify
(df -h, lsblk)
    │
    ▼
(Optional)
Configure /etc/fstab
    │
    ▼
Persistent Storage

💡 This workflow illustrates the complete lifecycle of preparing a new storage device for use in Linux—from detecting the disk to configuring it for automatic mounting after system reboots.

## 🎯 Key Takeaways

- Linux represents storage devices as block devices under the /dev directory (e.g., /dev/sda, /dev/sdb1).
- A new disk must typically be partitioned, formatted with a file system, and mounted before it can be used.
- Mounting makes a filesystem accessible through a directory such as /mnt, /data, or /home.
- Essential disk management commands include lsblk, df, du, fdisk, blkid, and mount for viewing and managing storage.
- LVM provides flexible storage management, while swap space extends memory by using disk space when RAM is full.