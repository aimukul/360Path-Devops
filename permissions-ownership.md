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