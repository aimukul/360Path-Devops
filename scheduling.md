
# List current user crontab entries
crontab -l

# Edit crontab for current user
crontab -e

# Sample cron job (run script every day at 2am)
0 2 * * * /home/mukul/script.sh

# Schedule a one-time job at 5pm today
echo "/home/mukul/script.sh" | at 17:00

# List scheduled 'at' jobs
atq

# Remove an 'at' job
atrm job_number