Concepts and principles that do not fit neatly into smaller topic documents or tool specifics.

# Logging

On FreeBSD (as an example of a UNIX system) programs use `syslog` directly to create text based log files which are stored on disk and which can be forwarded as needed.

On Linux programs use `systemd-journal` which forwards to `syslog`. `systemd-journal` is binary and indexed.

To guard against log files consuming the disk, use partitions.

On linux systems `rsyslogd` has replaced `syslogd` and is available for install on BSD.

Programs that are `syslog` aware will write log entries to `/dev/log`. 