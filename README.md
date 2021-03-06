# launchd-sar
Modifications to the included Apple sa1 and sa2 scripts and new plists to run them via launchd.

The included sysstat scripts for OS X were intended to be run via cron. This project modifes them and adds launchd plists so that the tools run in a modern OS X environment. They are currently scheduled around a user workstation that is being monitored during a standard work week.

There are still minor bugs and work arounds in this project. The version of sadc that Apple supplies in OS X truncates data files when writing, thus the script is modified to redirect stdio to the log file and append instead. There is a known flaw with this in that errors are sent to stderr when running sar on these binary data files, and entries about "New Disk" appear in the processed text output of sar. The sa2 script has been written to account for these flaws and bugs.

To use:

Copy sa1 and sa2 to /usr/local/lib/sa directory, and make them executable with 755 permissions.

Copy the plist files to /Library/LaunchDaemons directory, where they should be owned by root:wheel and with 644 permissions.

Add the plist entries to the launchd scheduler vi a root shell or sudo:

launchctl load /Library/LaunchDaemons/com.riskalytics.corp.jpruente.sa1.plist

launchctl load /Library/LaunchDaemons/com.riskalytics.corp.jpruente.sa2.plist

The binary saXX and text sarXX log files will be put in to /var/log/sa
