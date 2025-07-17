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