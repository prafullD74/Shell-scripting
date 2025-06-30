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
