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
