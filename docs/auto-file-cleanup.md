# Automated File Cleanup

Older video files can be removed using tmp-reaper

## Step 1 - Install tmp-reaper

```bash
sudo apt-get install tmpreaper
```

You will need to acknowledge the security warning.

# Step 2 - Create a Scheduled cron Job to remove old files

Install a cron job under the `motion` user to remove video files older than 180 days.

```bash
sudo crontab -e -u motion
```

In the crontab, add a daily job.

```ini
# remove video files older than 180 days
0 0 * * * /usr/sbin/tmpreaper 180d /home/motion >/dev/null 2>&1
```
