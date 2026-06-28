# 👥 Linux User & Group Management

## 👤 What is User Management?

Linux is a **multi-user operating system**, meaning multiple users can
securely share the same computer while keeping their own files,
settings, and permissions.

User management helps administrators:

-   Create and remove user accounts
-   Manage passwords and account security
-   Control access to files and resources
-   Organize users using groups
-   Enforce security policies

💡 **Why it matters:** Every action performed on a Linux system is
associated with a user account. Linux uses users and groups to decide
**who can access what**.

## 👥 Types of Linux Users

  -----------------------------------------------------------------------
  User Type                                Purpose
  ---------------------------------------- ------------------------------
  **Root User**                            Full administrative access
                                           (UID 0)

  **System Users**                         Created automatically to run
                                           services like MySQL and Nginx

  **Normal Users**                         Human users who log in and use
                                           the system
  -----------------------------------------------------------------------

> **Note:** Root always has **UID 0**, while normal users usually start
> from **UID 1000**.

⚠️ **Best Practice:** Avoid logging in directly as the root user for
everyday work. Instead, use `sudo` when administrative privileges are
required.

## 🆔 User Identity

Every Linux user has:

-   Username
-   User ID (UID)
-   Primary Group (GID)
-   Home Directory
-   Login Shell
-   Password

## UID Ranges

``` text
UID 0        → Root user
UID 1–999    → System / Service accounts
UID 1000+    → Regular users
```
## 👥 Primary vs Supplementary Groups

Every user has:

-   **One Primary Group**
-   **Zero or More Supplementary Groups**

``` text
alice

Primary Group
      │
      ▼
    alice

Supplementary Groups

sudo
docker
developers
```
## 📂 Important User Files

  File             Purpose
  ---------------- ----------------------------------------
  `/etc/passwd`    User account information
  `/etc/shadow`    Encrypted passwords and password aging
  `/etc/group`     Group information
  `/etc/gshadow`   Secure group information

### What is stored?

  -----------------------------------------------------------------------
  File                       Contains
  -------------------------- --------------------------------------------
  `/etc/passwd`              Username, UID, GID, shell, home directory
                             (**not passwords**)

  `/etc/shadow`              Encrypted passwords, password expiration,
                             aging

  `/etc/group`               Group names and members

  `/etc/gshadow`             Secure group passwords and administration
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## 👀 View User Information
```bash
whoami                         # Show the current logged-in user
id                             # Show UID, GID, and groups of the current user
id username                    # Show UID, GID, and groups of a specific user
who                            # Show all logged-in users
users                          # Show only logged-in usernames
```
## ➕ User Management

### adduser vs useradd

#### adduser

-   Interactive
-   Creates home directory
-   Prompts for password
-   Beginner-friendly

``` bash
sudo adduser john
```
#### useradd

-   Low-level command
-   Common in automation/scripts
-   Requires additional options

``` bash
sudo useradd -m john
```
### ➕ User Management
```bash
sudo adduser john              # Create a new user (interactive)
sudo useradd -m john           # Create a new user with a home directory
sudo useradd -u 1050 john      # Create a user with a specific UID
sudo useradd -d /data/john john # Create a user with a custom home directory
sudo useradd -s /bin/zsh john  # Create a user with a custom login shell
sudo useradd -u 1050 -d /data/john -s /bin/zsh john   # Create a user with custom UID, home, and shell
```
### Change Password

``` bash
passwd
sudo passwd john
```
### Lock / Unlock User

``` bash
sudo passwd -l john
sudo passwd -u john
```
### Modify Existing User

``` bash
sudo usermod [options] username
```

  Option   Purpose
  -------- --------------------------
  `-l`     Rename user
  `-u`     Change UID
  `-d`     Change home directory
  `-m`     Move home directory
  `-g`     Change primary group
  `-aG`    Add supplementary groups
  `-s`     Change login shell
  `-L`     Lock account
  `-U`     Unlock account

### Give a User Administrative Access

Ubuntu/Debian:

``` bash
sudo usermod -aG sudo john
```

RHEL/CentOS/Fedora:

``` bash
sudo usermod -aG wheel john
```
## 🗑️ Remove Users

``` bash
sudo deluser username
sudo deluser --remove-home username

sudo userdel username
sudo userdel -r username
```

> **Note:** `userdel -r` removes the user's home directory, while
> `userdel` removes only the account.

⚠️ **Warning:** `userdel -r` permanently deletes the user's home
directory.

## 🔐 Password Aging

Linux can enforce password expiration for better security.

``` bash
sudo chage -l username   # List password aging information sudo chage -M 90 username 
sudo chage -M 90 username # Set password to expire after 90 days
sudo chage -W 7 username  # Warn user 7 days before password expires
sudo chage -E YYYY-MM-DD username # Set account expiration date
sudo chage -d 0 username  # Force password change at next login
```
# 👥 Linux Groups

A **group** is a collection of users.

Groups simplify permission management by assigning permissions to
multiple users at once.

## 📂 Group Files

  File             Purpose
  ---------------- --------------------------------
  `/etc/group`     Group names, GIDs, and members
  `/etc/gshadow`   Secure group information

## ⚙️ Group Management

### Create Group

``` bash
sudo groupadd developers
```
### Delete Group

``` bash
sudo groupdel developers
```
### Modify Group

``` bash
sudo groupmod -n devteam developers
sudo groupmod -g 1500 developers
```
## 👥 Manage Group Members

``` bash
sudo gpasswd -a alice developers
sudo gpasswd -d alice developers
groups alice
getent group developers
```
## 🔍 View Users & Groups

Local users:

``` bash
cat /etc/passwd
```

Enterprise-friendly:

``` bash
getent passwd
```
💡 `cat /etc/passwd` only reads the local file, while `getent` also
works with centralized authentication (LDAP, Active Directory, etc.).

Groups:

``` bash
getent group
```
## 🔄 Linux User Management Workflow

``` text
Create User
      │
      ▼
Assign UID & Group
      │
      ▼
Create Home Directory
      │
      ▼
Set Password
      │
      ▼
Modify User
      │
      ▼
Manage Groups
      │
      ▼
Lock / Unlock / Delete User
```
##  🎯 Key Takeaways

- Linux is a **multi-user operating system** where every user and service has its own identity.
- Every user has a unique **UID**, and every group has a unique **GID** for identification.
- User account information is stored in **`/etc/passwd`**, while encrypted passwords are stored in **`/etc/shadow`**.
- Every user belongs to **one primary group** and can belong to **multiple supplementary groups**.
- Groups simplify permission management by allowing multiple users to share the same access rights.
- Password aging policies improve security by enforcing password expiration and account lifecycle management.
- System users are created for applications and services, while normal users are intended for interactive login.
- User and group accounts can be safely created, modified, locked, unlocked, and removed using Linux administration tools.
- Use **`getent`** to retrieve user and group information in systems that use centralized authentication (such as LDAP or NIS).
- Understanding users and groups is the foundation for learning **Linux permissions, ownership, security, and system administration**.