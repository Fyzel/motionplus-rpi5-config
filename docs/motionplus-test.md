# Testing MotionPlus

Test the MotionPlus configuration by running it on the command line.

```bash
sudo /usr/local/bin/motionplus -c /etc/motionplus/motionplus.conf
```

This will start the motionplus application. The log file can be reviewed by tailing the motionplus log file.

```bash
sudo tail -f /var/log/motionplus/motionplus.log
```

Review the log for any errors or warnings.

The motionplus web interface is accessible on your Raspberry Pi by navigating to http://<your-raspberry-pi-ip-address:8080/>.

You will be prompted to logon using the username `admin` and the password value you replaced `<WEBCONTROL_PASSWORD>`.

The video will stream after successfully authenticating.

Terminate the motionplus service using `cttl-c`

Next Step: [Configure MotionPlus as a System Service](./motionplus-service.md)
