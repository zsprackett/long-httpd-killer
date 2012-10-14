# long-httpd-killer

## Reap long running httpd processes

Sometimes Apache request handler processes can become blocked waiting on
things like NFS.  This reaper process is designed to be run either manually
or via cron to clean things up.

## Example Usage

    ./long-httpd-killer -t 60 -f -s

This command will hit the Apache server status running at 127.0.0.1.  Look
for request handlers that have been running for longer than 60 seconds,
send them a kill -9 and report the reaping via syslog.

Syslog log messages will be generated like the following:

    kill -9 - PID: 27744 Srv: 13-2 Acc: 0/22/52325 M: W CPU: 7.92 Ss: 0: Req: 0
    Conn: 0.0 Child: 0.08 Slot: 568.37 Client: 10.13.1.15 VHost:
    foo.bar.baz POST /slow.php CWD: /var/www

To run this via cron, I would suggess adding an entry like the following to
instruct cron to run it every minute:

    * * * * * /usr/local/bin/long-httpd-killer -t 60 -f -s


## Feedback

Please send feedback or patches through github:

https://github.com/zsprackett/long-httpd-killer

Thanks!
S. Zachariah Sprackett <zac@sprackett.com>
