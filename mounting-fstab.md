
# Manually mount a filesystem
sudo mount /dev/vg_data/lv_storage /mnt
# Mounts the device /dev/vg_data/lv_storage to the /mnt directory. The mount point must exist beforehand.

# View currently mounted filesystems in a clean column format
mount | column -t
# Displays all currently mounted filesystems neatly in columns.

# Check disk usage and mounted filesystems in human-readable format
df -h
# Shows disk space usage of mounted partitions in a readable format.

# Create a mount point directory (if not already present)
sudo mkdir -p /mnt/mydata
# Creates a new directory to use as a mount point.

# Mount a device specifying the filesystem type (e.g., ext4)
sudo mount -t ext4 /dev/sdb1 /mnt/mydata
# Use this if the system doesn’t automatically detect the filesystem type.

# Mount with specific options (e.g., read-only)
sudo mount -o ro /dev/sdb1 /mnt/mydata
# Mounts the filesystem as read-only.

# Add an entry to /etc/fstab to mount automatically at boot
echo '/dev/vg_data/lv_storage /mnt xfs defaults 0 0' | sudo tee -a /etc/fstab
# Adds an entry in the fstab file for automatic mounting on system boot.

# Use UUID instead of device path for reliability
sudo blkid /dev/vg_data/lv_storage
# Get the UUID of the device for more reliable fstab entries.

# Example /etc/fstab entry using UUID
echo 'UUID=abcd-1234-ef56-7890 /mnt xfs defaults 0 0' | sudo tee -a /etc/fstab

# Test all fstab entries without rebooting
sudo mount -a
# Attempts to mount all filesystems specified in /etc/fstab.

# Unmount a mounted filesystem
sudo umount /mnt
# Unmounts the filesystem from the mount point.

# Force unmount if regular unmount fails
sudo umount -f /mnt

# Check which processes are using the mount point
sudo lsof /mnt
# Lists open files and processes using the mount point.

# Remount a filesystem with new options (e.g., read-write)
sudo mount -o remount,rw /mnt
# Changes the mount options of an already mounted filesystem.

# List block devices and partitions with mount points
lsblk
# Shows devices, partitions, and their mount points.

