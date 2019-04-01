# Cron
Cron.daily
you can set tasks to be run daily by adding a file with your script to /etc/cron.daily

Cron Log
On a default installation the cron jobs get logged to
/var/log/syslog

You can see just cron jobs in that logfile by running
grep CRON /var/log/syslog

Test your cron tasks
run-parts --verbose --test /etc/cron.daily
