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