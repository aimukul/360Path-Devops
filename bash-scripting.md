# Bash Script Examples

## arrey.sh
```bash
#!/bin/bash
IndexArray=(egg burger milk)
for i in "${IndexArray[@]}"; do 
  echo $i
done
```

## exist.sh
```bash
#!/bin/bash
myfile=file.txt
if [ -f "$myfile" ]; then
  echo "$myfile exists"
else
  echo "It doesn't exist at all"
fi
```

## if.sh
```bash
#!/bin/bash
echo "Enter Your Salary:"
read Salary
echo "Enter Your Expense:"
read Expense

if [ "$Salary" == "$Expense" ]; then
  echo "Salary and Expense are equal."
else
  echo "Salary and Expense are not equal."
fi
```

## loop.sh
```bash
#!/bin/bash
for (( n=2; n<=10; n++ )); do
  echo "$n Seconds"
done
```

## read.sh
```bash
#!/bin/bash
echo "What is your age?"
read age
echo "Your age is $age years old."
```

## sleep.sh
```bash
#!/bin/bash
echo "Going to sleep for 10 seconds..."
sleep 10 && echo "I have been sleeping for 10 seconds."
echo "I am awake now."
```

## strlength.sh
```bash
#!/bin/bash
mystring="Let's count the length of this string"
length=${#mystring}
echo "Length: $length"
```

## system.sh
```bash
#!/bin/bash
echo "Date:"
date
echo "Uptime:"
uptime
```

## variable.sh
```bash
#!/bin/bash
bash='Hello World'
echo $bash

echo "When I feel good I say $bash."
echo "When I visit Japan I say $bash."
echo "When I see you I say $bash."
```

## backup.sh (Backup Script Example)
```bash
#!/bin/bash
BACKUP_DIR="/home/mukul/backup"
SOURCE_DIR="/home/mukul/documents"
DATE=$(date +%F)
BACKUP_FILE="backup-$DATE.tar.gz"

tar -czf $BACKUP_DIR/$BACKUP_FILE $SOURCE_DIR
echo "Backup completed: $BACKUP_FILE"
```
