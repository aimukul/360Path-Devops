## Start firewalld service
```bash
sudo systemctl start firewalld
```

## Enable firewalld service on boot
```bash
sudo systemctl enable firewalld
```

## Check firewalld status
```bash
sudo firewall-cmd --state
```

## List all active zones
```bash
sudo firewall-cmd --get-active-zones
```

## Allow HTTP service permanently
```bash
sudo firewall-cmd --permanent --add-service=http
```

## Reload firewall to apply changes
```bash
sudo firewall-cmd --reload
```

## Remove HTTP service permanently
```bash
sudo firewall-cmd --permanent --remove-service=http
sudo firewall-cmd --reload
```
