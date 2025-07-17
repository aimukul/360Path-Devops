
# Check if a service is active (running)
sudo systemctl is-active service_name
# Example: sudo systemctl is-active httpd
# Returns "active" if running, "inactive" if stopped.

# Check the status of a service with detailed info
sudo systemctl status service_name
# Shows whether the service is running, enabled on boot, logs, and more.

# Start a service
sudo systemctl start service_name

# Stop a service
sudo systemctl stop service_name

# Restart a service
sudo systemctl restart service_name

# Enable a service to start on boot
sudo systemctl enable service_name

# Disable a service from starting on boot
sudo systemctl disable service_name

# List all running services
systemctl list-units --type=service --state=running

# Find if a process is running by name
pgrep process_name
# Returns process IDs (PIDs) of running processes matching the name.

# View detailed info about running processes
ps aux | grep process_name

# Kill a process by PID
sudo kill PID
# Example: sudo kill 1234

# Force kill a process (if it doesn’t stop gracefully)
sudo kill -9 PID

# Kill all processes by name
sudo pkill process_name
# Example: sudo pkill httpd

# Check all processes listening on ports (helpful to identify services)
sudo netstat -tulpn
# Or
sudo ss -tulpn
