# Create gzip compressed archive
tar -czvf backup-$(date +%F).tar.gz /home/mukul/documents

# Extract gzip archive
tar -xzvf backup-2025-07-16.tar.gz

# Create bzip2 compressed archive
tar -cjvf backup-$(date +%F).tar.bz2 /home/mukul/documents

# Extract bzip2 archive
tar -xjvf backup-2025-07-16.tar.bz2