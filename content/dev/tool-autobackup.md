+++ 
date = "2020-06-04"
title = "Automated Mongodb github Backups"
tags = ["tool"]

+++


refer: [https://github.com/VeliovGroup/ostrio/blob/master/tutorials/linux/security/automated-backups.md](https://github.com/VeliovGroup/ostrio/blob/master/tutorials/linux/security/automated-backups.md)


A script to automatically backup your mongodb database and related logs etc., then commit to your github daily.
It also deletes your old backup that older than 7 days.
```bash
#!/bin/bash
# Change Directory to repository
cd /root/backup/

DATE=$(date +%Y%m%d)
DATEOLD=`date -d "${DATE} -7 day" +%Y%m%d`


mongodump \
  -d datadb \
  -u xx \
  -p xx \
  --gzip \
  --archive="/root/backup/mongodb.$DATE.gz"


tar -zcf "/root/backup/syslog.$DATE.tar.gz" -C / var/log/syslog
tar -zcf "/root/backup/auth.$DATE.tar.gz" -C / var/log/auth.log
tar -zcf "/root/backup/mongod.$DATE.tar.gz" -C / var/log/mongodb/mongod.log
tar -zcf "/root/backup/nginx-access.$DATE.tar.gz" -C / var/log/nginx/access.log
tar -zcf "/root/backup/nginx-error.$DATE.tar.gz" -C / var/log/nginx/error.log

# CHANGE <PASSWORD> TO THE PASSWORD OF YOUR CHOICE
7z a "/root/backup/b.$DATE.7z" "/root/backup/mongodb.$DATE.gz" "/root/backup/syslog.$DATE.tar.gz" "/root/backup/pictures.$DATE.tar.gz"  "/root/backup/auth.$DATE.tar.gz"  "/root/backup/mongod.$DATE.tar.gz" "/root/backup/nginx-error.$DATE.tar.gz" "/root/backup/nginx-access.$DATE.tar.gz" -p'your7zippassword'

rm "/root/backup/mongodb.$DATE.gz"
rm "/root/backup/syslog.$DATE.tar.gz"
rm "/root/backup/auth.$DATE.tar.gz"
rm "/root/backup/mongod.$DATE.tar.gz"
rm "/root/backup/nginx-error.$DATE.tar.gz"
rm "/root/backup/nginx-access.$DATE.tar.gz"
rm "/root/backup/pictures.$DATE.tar.gz"

# Remove backup older than 7 days:
rm "/root/backup/b.$DATEOLD.7z"
# Remove old backup from repository history (save LFS storage space):
git rm --cached "b.$DATEOLD.7z"

# Optional for rare cases (save LFS storage space):
# git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch b.$DATEOLD.7z' --prune-empty --tag-name-filter cat -- --all
git pull
git add .
git commit -m "bckp $DATE"
git push origin master

```