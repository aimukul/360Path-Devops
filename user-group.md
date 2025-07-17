# Add a new user
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