# 🐧 Linux Filesystem & Directory Management

## 📂 What is a Filesystem?

A filesystem is the way Linux organizes, stores, and manages files and directories on storage devices such as HDDs and SSDs.

Its main responsibilities are:

* Store and organize files
* Manage file permissions and ownership
* Track file information (metadata)
* Allocate storage space efficiently
* Recover data after crashes using journaling

## 🌳 Linux Filesystem Structure

Linux follows a hierarchical directory structure that starts from a single root directory (`/`).

```text
        /
        |
 ┌──────┼──────────────┐
 |      |              |
/bin   /etc         /home
```

Unlike Windows, Linux does not use drive letters (C:, D:, etc.). Everything is organized under the root directory.

## 📁 Important Linux Directories

| Directory | Purpose                                              |
| --------- | ---------------------------------------------------- |
| `/`       | Root directory (starting point of the filesystem)    |
| `/home`   | Home directories of normal users                     |
| `/root`   | Home directory of the root user                      |
| `/etc`    | System configuration files                           |
| `/bin`    | Essential Linux commands                             |
| `/boot`   | Bootloader and kernel files                          |
| `/dev`    | Device files                                         |
| `/proc`   | Process and kernel information (virtual filesystem)  |
| `/sys`    | Hardware and kernel information (virtual filesystem) |
| `/usr`    | Applications, libraries, and documentation           |
| `/var`    | Logs, cache, databases, and other changing data      |
| `/tmp`    | Temporary files                                      |
| `/opt`    | Optional third-party software                        |
| `/mnt`    | Temporary mount point                                |
| `/media`  | USB drives and removable media                       |

## 📍 File Paths

### Absolute Path

Starts from the root directory (`/`).

Example:

```bash
/home/user/Documents/file.txt
```
### Relative Path

Starts from your current directory.

Example:

```bash
Documents/file.txt
```
## 📂 Everyday File & Directory Commands

### Navigation

```bash
pwd         # Show current directory
ls          # List files
ls -alh     # Detailed listing
cd          # Go to home directory
cd ..       # Move up one directory
cd -        # Return to previous directory
```
### 📁 Create Files & Directories

```bash 
mkdir project            # Create a new directory
mkdir -p app/src/logs    # Create nested directories
touch file.txt           # Create an empty file
```
### Manage Files

```bash
cp file1 file2          # Copy
mv old.txt new.txt      # Move or rename
rm file.txt             # Delete file
rm -r folder            # Delete directory
```
⚠️ Warning: rm -r permanently deletes files and directories. Recovering them can be difficult or impossible, so always double-check before pressing Enter.

### 👀 View File Contents

```bash
cat file.txt             # Display the entire file
less file.txt            # View a file page by page
head file.txt            # Show the first 10 lines
tail file.txt            # Show the last 10 lines
tail -f app.log          # Monitor a log file in real time
```
### 🔍 Search Files

```bash 
find /home -name file.txt   # Search for a file by name
find . -type f              # Find all files in the current directory
find . -type d              # Find all directories in the current directory
locate nginx.conf           # Quickly locate a file using the database
```
### 💽 check Disk & Storage

```bash
df -h                 # Show disk space usage
df -i                 # Show inode usage
du -sh folder         # Show the size of a directory
lsblk                 # List disks and partitions
```
## ⚙️ How Linux Stores a File

When a file is created, Linux follows this process:

```text
Filename
     │
     ▼
Directory Entry
     │
     ▼
Inode
     │
     ▼
Data Blocks
     │
     ▼
Actual File Data
```

### Main Components

#### Superblock

Stores information about the entire filesystem, such as its type, size, available space, and status.

#### Inode

Every file and directory has an inode.

It stores:

* File permissions
* Owner and group
* File size
* Timestamps
* Location of data blocks

**Note:** The inode stores metadata, not the filename.

#### Data Blocks

Store the actual contents of a file, such as text, images, videos, or application data.

#### Directory Entry

Maps a filename to its inode.

Example:

```text
notes.txt → inode 105
```
## 💽 Filesystem Types

| Filesystem | Purpose                                  |
| ---------- | ---------------------------------------- |
| ext4       | Most common Linux filesystem             |
| XFS        | High-performance filesystem              |
| Btrfs      | Supports snapshots and advanced features |
| exFAT      | Cross-platform compatibility             |
| tmpfs      | Memory-based filesystem                  |
| procfs     | Process information                      |
| sysfs      | Hardware and kernel information          |

## 📦 Filesystem Management

```bash
stat file.txt           # Display detailed file information
mkfs.ext4 /dev/sdb1     # Create an ext4 filesystem
fsck /dev/sda1          # Check and repair a filesystem
mount /dev/sdb1 /mnt    # Mount a filesystem
umount /mnt             # Unmount a filesystem
```
# 📦 Mounting Filesystems

Linux uses one directory tree that begins at `/`.

A storage device becomes accessible only after it is mounted to a directory.

Mount a filesystem:

```bash
mount /dev/sdb1 /mnt
```
Unmount it:

```bash
umount /mnt
```
To make a mount permanent after reboot, configure:

```text
/etc/fstab
```
Verify the configuration:

```bash
mount -a
```

# 🛡️ Journaling

Journaling helps protect the filesystem from corruption during unexpected shutdowns.

Instead of writing changes directly to disk, Linux records them in a journal first and then updates the filesystem.

Filesystems that support journaling include:

* ext4
* XFS
* Btrfs

# 🎯 Key Takeaways

* A filesystem organizes and manages data on storage devices.
* Every file has an inode that stores metadata, while data blocks store the actual content.
* Directories map filenames to inode numbers.
* Mounting connects storage devices to the Linux directory tree.
* Journaling helps recover from crashes and reduces filesystem corruption.
* `/proc` and `/sys` are virtual filesystems that provide process, hardware, and kernel information.