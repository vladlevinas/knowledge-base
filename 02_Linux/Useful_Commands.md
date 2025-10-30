# Useful Commands

Let's create 10 directories, starting with testdir1 to testdir10. How to do it in one command?

```bash
mkdir testdir{1..10}
```

Ok, let's create more complicated stuff. In order to create deeper structure, we have to use -p argument. This allows us to create the whole structure, without creating parent directory as first step.

```bash
mkdir -p parentdir/childdir{01..100}
```

Of course, like in previous scenario, we can create multiple files.
```bash
touch my{01..100}file
```

Some admins like to see the hierarchy of processes, therefore they use
```bash
ps aux --forest
```
But in reality, is used by them most often. Let's trypstree
```bash
pstree
```

Anyway, let's go through some.

ps -f -u syslog

shows all processes run by user .syslog

ps -f -C cron

shows all processes, where the executable is .cron

ps -f -p 1

shows process with specified PID.

ps -f --ppid 1

Journactl, continuation
Here we will explore some possibilities given by . More is in manual. These examples will give you the picture of the functionality.journalctl

journalctl --since "$(date '+%Y-%m-%d %H:%M:%S' --date='5 minutes ago')" log entries from specific time

But wait, what happened here? Let's take a look:

journalctl - command for work with journal
--since - argument for limit logs from specific date
"$()" part this everything what is inside brackets will be executed and output put as value to argument--since
Ok, so, now . The command itself shows current date.date

'+%Y-%m-%d %H:%M:%S' formats the output. We need to pass date in this format to journalctl
--date='5 minutes ago' will take the time from 5 minutes earlier.
journalctl --since "$(date '+%Y-%m-%d %H:%M:%S' --date='5 minutes ago')" --until "$(date '+%Y-%m-%d %H:%M:%S' --date='2 minutes ago')" logs from specific range

journalctl --since yesterday - logs from today and yesterday. Here works as well.--until

journalctl -u nginx.service - lists only nginx service. In this way we can list all records related to (in this case).nginx

journalctl -u nginx.service --since today - lists nginx related entries from today

journalctl _PID=8088 - lists entries for PID (Process IDentifier) 8088. Let's try for one of the Nginx processes:

journalctl _PID=$(pgrep nginx| tail -n1) I trust you already know what happened here?

id -u www-data - collect id of user www-data. Let's suppose it is 33, which is the standard UID (User IDentifier) for this user.

journalctl _UID=33 --since today will print records for specified UID. If this UID doesn't match, we can always... use command inside command:

journalctl _UID=$(id -u www-data)

journalctl -F _GID

This is interesting. It lists all GIDs (Group IDentifiers) with entries in journal. The same approach works for UIDs - _UID

journalctl -k - displays kernel messages

journalctl -p err -b - display errors, criticals, alerts and emergencies.

journalctl -b -u nginx -o json-pretty - parsing and better formatting

man systemd.journal-fields - read more in man :)
