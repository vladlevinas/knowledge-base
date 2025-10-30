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
