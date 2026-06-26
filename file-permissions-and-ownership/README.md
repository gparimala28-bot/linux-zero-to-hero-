# 🔐 Linux File Permissions & Ownership

## 📂 What are File Permissions?

File permissions control who can access a file or directory and what actions they can perform.

Linux uses permissions to protect files from unauthorized access and ensure system security.

### Main Purposes

* Control access to files and directories
* Protect sensitive system files
* Prevent accidental modifications
* Improve system security

## 👥 Permission Categories

Linux assigns permissions to three groups:

| Category   | Description                         |
| ---------- | ----------------------------------- |
| User (u)   | The owner of the file               |
| Group (g)  | Users belonging to the file's group |
| Others (o) | All other users                     |

Example:

```text
-rwxr-xr--
```

Breakdown:

```text
- rwx r-x r--
  │   │   │
  │   │   └── Others
  │   └────── Group
  └────────── User (Owner)
```

## 📖 Permission Types

| Permission | Symbol | Value | Meaning                                             |
| ---------- | ------ | ----- | --------------------------------------------------- |
| Read       | r      | 4     | View file contents or list a directory              |
| Write      | w      | 2     | Modify a file or create/delete files in a directory |
| Execute    | x      | 1     | Run a program or access a directory                 |

## 📁 File vs Directory Permissions

### File Permissions

| Permission | Allows                        |
| ---------- | ----------------------------- |
| r          | Read the file                 |
| w          | Edit the file                 |
| x          | Execute the file as a program |

### Directory Permissions

| Permission | Allows                          |
| ---------- | ------------------------------- |
| r          | List directory contents         |
| w          | Create, delete, or rename files |
| x          | Enter (access) the directory    |

## 🔢 Numeric (Octal) Permissions

Linux combines permission values using numbers.

| Number | Permission |
| ------ | ---------- |
| 7      | rwx        |
| 6      | rw-        |
| 5      | r-x        |
| 4      | r--        |
| 0      | ---        |

Common examples:

| Permission | Meaning                                    |
| ---------- | ------------------------------------------ |
| 755        | Owner: rwx, Group: r-x, Others: r-x        |
| 744        | Owner: rwx, Group: r--, Others: r--        |
| 700        | Owner only has full access                 |
| 644        | Owner can read/write, others can only read |
| 600        | Only owner can read and write              |

## 🔤 Symbolic Permissions

Instead of numbers, permissions can be modified using symbols.

Examples:

```bash
chmod u+x script.sh      # Add execute permission to owner
chmod g-w file.txt       # Remove write permission from group
chmod o+r file.txt       # Give read permission to others
chmod a+x script.sh      # Give execute permission to everyone
```

## 👤 File Ownership

Every file belongs to:

* One owner (User)
* One group

View ownership:

```bash
ls -l
```

Example:

```text
-rw-r--r-- 1 john developers file.txt
```

## 🔄 Change Permissions

Change permissions using `chmod`.

Examples:

```bash
chmod 755 script.sh
chmod 644 file.txt
chmod +x install.sh
chmod -w file.txt
```

## 👥 Change Ownership

Change the owner:

```bash
chown user file.txt
```

Change owner and group:

```bash
chown user:group file.txt
```

Change only the group:

```bash
chgrp developers file.txt
```

## 🎭 Default Permissions (umask)

Linux assigns default permissions when new files and directories are created.

The **umask** value removes permissions from the default settings.

View current umask:

```bash
umask
```

Example:

```text
Default File Permission : 666
Default Directory Permission : 777

Final Permission = Default - Umask
```

Common umask:

```text
022
```

Results in:

```text
Files       → 644
Directories → 755
```
## ⭐ Special Permissions

Linux provides three special permissions.

### SUID (Set User ID)

Runs a program with the owner's privileges.

```bash
chmod u+s program
```
### SGID (Set Group ID)

Files run with the group's permissions.

Directories allow newly created files to inherit the same group.

```bash
chmod g+s directory
```
### Sticky Bit

Used mainly on shared directories.

Only the file owner can delete their own files.

Example:

```text
/tmp
```

Enable Sticky Bit:

```bash
chmod +t directory
```

## 🎯 Key Takeaways

* Linux protects files using permissions and ownership.
* Numeric permissions such as **755** and **644** are commonly used.
* `chmod` changes permissions, while `chown` and `chgrp` manage ownership.
* `umask` determines the default permissions for newly created files and directories.
* Special permissions (**SUID**, **SGID**, and **Sticky Bit**) provide advanced access control.
* Understanding permissions is essential for Linux administration, DevOps, and cloud environments.

