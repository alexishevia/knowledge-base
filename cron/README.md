# Cron
Cron is a time-based job scheduler included by default in most unix distributions.

Using cron you can run scripts periodically, without much hassle.

## Cron.daily
You can set tasks to be run daily by adding a file with your script to `/etc/cron.daily`

## Cron Log
On a default Linux installation, the cron jobs get logged to `/var/log/syslog`

You can see cron jobs in that logfile by running:
```
grep CRON /var/log/syslog
```

## Test your cron tasks
`run-parts --verbose --test /etc/cron.daily`
