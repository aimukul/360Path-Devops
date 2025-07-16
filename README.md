#### RHCSA Practice Repository ####
......................................

Welcome to my **Red Hat Certified System Administrator (RHCSA)** practice repo!  
Here you'll find my hands-on tasks, command references, and configuration files that helped me prepare for the RHCSA exam. 🎯

---

## 📁 Folder Structure

rhcsa-practice/
├── users-groups/ # User creation, password policies, group management
├── storage-management/ # Partitioning, LVM, mount, fstab
├── firewalld-config/ # firewalld commands, zones, service handling
├── cron-at/ # Scheduling tasks using cron and at
├── systemctl-service/ # Managing services and systemd units
├── selinux-practice/ # SELinux modes, booleans, file contexts
└── notes.md # Summary, exam tips, command references

---


## 🔧 Topics Covered

- ✅ User & Group Management (`adduser`, `passwd`, `usermod`)
- ✅ File Permissions & Ownership (`chmod`, `chown`)
- ✅ Partitioning & LVM
- ✅ Mounting & FSTAB
- ✅ Firewalld Configuration
- ✅ SELinux Basics
- ✅ Scheduling (cron, at)
- ✅ Systemd & Services
- ✅ Boot Process & Rescue Mode
- ✅ Archiving & Compression with tar, gzip, and bzip2
- ✅ Bash script


---

## ⚙️ Sample Commands

✅ User & Group Management (adduser, passwd, usermod)

Add a new user
sudo adduser username

# Set or change user password
sudo passwd username

# Modify user properties (e.g., change shell)
sudo usermod -s /bin/bash username

# Add user to a group
sudo usermod -aG groupname username

# Create a new group
sudo groupadd groupname

# Delete a user and its home directory
sudo userdel -r username

# View all users
cut -d: -f1 /etc/passwd

# View all groups
cut -d: -f1 /etc/group

✅ Mounting & FSTAB

# Mount a filesystem
sudo mount /dev/vg_data/lv_storage /mnt

# View currently mounted filesystems
mount | column -t

# Add entry in /etc/fstab to mount automatically at boot
echo '/dev/vg_data/lv_storage /mnt xfs defaults 0 0' | sudo tee -a /etc/fstab

# Test fstab entries without reboot
sudo mount -a

✅ Firewalld Configuration

# Start firewalld service
sudo systemctl start firewalld

# Enable firewalld service on boot
sudo systemctl enable firewalld

# Check firewalld status
sudo firewall-cmd --state

# List all active zones
sudo firewall-cmd --get-active-zones

# Allow HTTP service permanently
sudo firewall-cmd --permanent --add-service=http

# Reload firewall to apply changes
sudo firewall-cmd --reload

# Remove HTTP service permanently
sudo firewall-cmd --permanent --remove-service=http
sudo firewall-cmd --reload

✅ Scheduling (cron, at)

# List current user crontab entries
crontab -l

# Edit crontab for current user
crontab -e

# Sample cron job (run script every day at 2am)
0 2 * * * /home/mukul/script.sh

# Schedule a one-time job at 5pm today
echo "/home/mukul/script.sh" | at 17:00

# List scheduled 'at' jobs
atq

# Remove an 'at' job
atrm job_number

✅ Systemd & Services

# Start a service
sudo systemctl start httpd

# Stop a service
sudo systemctl stop httpd

# Restart a service
sudo systemctl restart httpd

# Enable a service to start at boot
sudo systemctl enable httpd

# Disable a service from starting at boot
sudo systemctl disable httpd

# Check service status
sudo systemctl status httpd

# List all enabled services
systemctl list-unit-files --type=service | grep enabled

✅ Bash Script Examples

#!/bin/bash
# Simple Hello World
echo "Hello, World!"

# Variables & Conditionals
USER="Mukul"
if [ "$USER" == "Mukul" ]; then
  echo "Welcome, $USER!"
else
  echo "Who are you?"
fi

# Loop example: Print numbers 1 to 5
for i in {1..5}; do
  echo "Number: $i"
done

# Backup Script Example
BACKUP_DIR="/home/mukul/backup"
SOURCE_DIR="/home/mukul/documents"
DATE=$(date +%F)
BACKUP_FILE="backup-$DATE.tar.gz"

tar -czf $BACKUP_DIR/$BACKUP_FILE $SOURCE_DIR
echo "Backup completed: $BACKUP_FILE"

✅ SELinux Basics

# Check current SELinux mode
getenforce

# View SELinux status and mode
sestatus

# Temporarily set SELinux mode to permissive
sudo setenforce 0

# Permanently change SELinux mode (edit config file)
sudo vi /etc/selinux/config
# Set SELINUX=permissive or enforcing or disabled

# List all SELinux booleans
sudo getsebool -a

# Enable an SELinux boolean (example: allow httpd to connect to network)
sudo setsebool -P httpd_can_network_connect on

# Check file context of a file
ls -Z /var/www/html/index.html

# Restore default SELinux context for a file or directory
sudo restorecon -v /path/to/file

✅ Partitioning & LVM

# 1. List all disks and partitions (to identify your disks)
sudo fdisk -l

# 2. Create a new partition on /dev/sdb using fdisk:
sudo fdisk /dev/sdb
# Inside fdisk:
#   - type 'n' for new partition
#   - choose partition number (usually 1)
#   - accept default start and end sectors (or specify size e.g. +10G)
#   - type 'w' to write changes and exit

# 3. Inform kernel about partition changes (optional if reboot is not desired)
sudo partprobe /dev/sdb

# 4. Create Physical Volume (PV) on new partition, e.g., /dev/sdb1
sudo pvcreate /dev/sdb1

# 5. Display Physical Volumes (check PV created)
sudo pvdisplay

# 6. Create Volume Group (VG) named 'vg_data' using the PV
sudo vgcreate vg_data /dev/sdb1

# 7. Display Volume Groups (check VG details)
sudo vgdisplay

# 8. Create Logical Volume (LV) inside VG 'vg_data'
# Example: Create 5 GB LV named 'lv_storage'
sudo lvcreate -L 5G -n lv_storage vg_data

# 9. Display Logical Volumes (confirm LV creation)
sudo lvdisplay

# 10. Format Logical Volume with XFS filesystem
sudo mkfs.xfs /dev/vg_data/lv_storage

# 11. Create a mount point directory, e.g., /mnt/storage
sudo mkdir -p /mnt/storage

# 12. Mount the logical volume
sudo mount /dev/vg_data/lv_storage /mnt/storage

# 13. Verify mounted volumes
df -h | grep storage

# 14. Make mount permanent by adding entry to /etc/fstab:
# Use UUID for better reliability:
sudo blkid /dev/vg_data/lv_storage
# Output example: UUID="abcd-1234-ef56-7890"

# Edit /etc/fstab and add line like:
# UUID=abcd-1234-ef56-7890   /mnt/storage    xfs    defaults    0 0

# Or use device path directly (less preferred):
echo '/dev/vg_data/lv_storage /mnt/storage xfs defaults 0 0' | sudo tee -a /etc/fstab

# 15. Test /etc/fstab without reboot
sudo mount -a

# 16. Resize Logical Volume (if needed later)
# Extend LV by 2G:
sudo lvextend -L +2G /dev/vg_data/lv_storage

# Resize filesystem after extending LV (for XFS):
sudo xfs_growfs /mnt/storage

# Shrink LV (more complex and risky, usually requires unmounting and filesystem resize)

# 17. Remove Logical Volume
sudo lvremove /dev/vg_data/lv_storage

# 18. Remove Volume Group
sudo vgremove vg_data

# 19. Remove Physical Volume
sudo pvremove /dev/sdb1

✅ Archiving & Compression with tar, gzip, and bzip2

# Create gzip compressed archive
tar -czvf backup-$(date +%F).tar.gz /home/mukul/documents

# Extract gzip archive
tar -xzvf backup-2025-07-16.tar.gz

# Create bzip2 compressed archive
tar -cjvf backup-$(date +%F).tar.bz2 /home/mukul/documents

# Extract bzip2 archive
tar -xjvf backup-2025-07-16.tar.bz2

✅ File Permissions & Ownership (chmod, chown)

# Give everyone read, write and execute permission
chmod 777 file.txt

# Give owner read and write, group read, others no permission
chmod 640 file.txt

# Add execute permission for owner only
chmod u+x script.sh

# Remove write permission from group
chmod g-w file.txt

# Set file permissions to rwxr-xr--
chmod 754 file.txt
# Change owner of a file
sudo chown mukul file.txt

# Change owner and group
sudo chown mukul:developers file.txt

# Change group only
sudo chown :developers file.txt

# Recursively change owner and group for directory and all contents
sudo chown -R mukul:developers /var/www/html/
ls -l file.txt

# Output example:
# -rw-r--r-- 1 mukul developers 4096 Jul 16 10:00 file.txt

