# Cron Jobs in Linux
>Cron is a job scheduling utility present in Unix like systems. The crond daemon enables cron functionality and runs in background. The cron reads the crontab (cron tables) for running predefined scripts.

- For individual users, the cron service checks the following file:  `/var/spool/cron/crontabs`
- **Any task that you schedule through crons is called a cron job**
- `sudo systemctl status cron.service` to check the status of the cron service.

### Cron job syntax
1. **`crontab -e`**: edits crontab entries to add, delete, or edit cron jobs.
2. **`crontab -l`**: list all the cron jobs for the current user.
3. **`crontab -u username -l`**: list another user's crons.
4. **`crontab -u username -e`**: edit another user's crons.
5. `* * * * * sh /path/to/script.sh` to list crons.
   - `sh` represents that the script is a bash script and should be run from `/bin/bash`.
   - `/path/to/script.sh` specifies the path to script
  
|  | Value | Description |
|---|---|---|
| Minutes | 0-59 | Command would be executed at the specific minute. |
| Hours | 0-23 | Command would be executed at the specific hour. |
| Days | 1-31 | Commands would be executed in these days of the months. |
| Months | 1-12 | The month in which tasks need to be executed. |
| Weekdays | 0-6 | Days of the week where commands would run. Here, 0 is Sunday. |

### How to Troubleshoot crons
1. Check the schedule.
   - `crontab -l` lists the cron jobs scheduled for the currently logged-in user.
   - `sudo cat /etc/crontab` System-Wide Crontabs.
   - `ls -l /etc/cron.d/` This directory contains individual cron job files, often installed by packages.
2. Check cron logs.
   - `/var/log/syslog` (on Ubuntu/Debian-based systems)
   - `/var/log/cron` (on RHEL/CentOS-based systems)
   - `grep CRON /var/log/syslog`
3. Redirect cron output to a file.
   - `* * * * * sh /path/to/script.sh &> log_file.log` 

```linux
root@Swarajay:/etc# sudo cat /etc/crontab
# /etc/crontab: system-wide crontab
# Unlike any other crontab you don't have to run the `crontab'
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# that none of the other crontabs do.

SHELL=/bin/sh
# You can also override PATH, but by default, newer versions inherit it from the environment
#PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  * user-name command to be executed
17 *    * * *   root    cd / && run-parts --report /etc/cron.hourly
25 6    * * *   root    test -x /usr/sbin/anacron || { cd / && run-parts --report /etc/cron.daily; }
47 6    * * 7   root    test -x /usr/sbin/anacron || { cd / && run-parts --report /etc/cron.weekly; }
52 6    1 * *   root    test -x /usr/sbin/anacron || { cd / && run-parts --report /etc/cron.monthly; }
#
```
