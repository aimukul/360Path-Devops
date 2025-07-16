# RHCSA Practice Repository 🇧🇩

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

---

## ⚙️ Sample Commands

```bash
# Add a user and set password
useradd devops
passwd devops

# Create an LVM volume
pvcreate /dev/sdb
vgcreate vg01 /dev/sdb
lvcreate -L 5G -n lvdata vg01
mkfs.xfs /dev/vg01/lvdata

# Mount the logical volume
mount /dev/vg01/lvdata /mnt
