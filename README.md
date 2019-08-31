# check_linux_tcp_sockets
Nagios and Icinga2 plugin to check the TCP sockets on a Linux system and provide statistics from /proc/net/sockstat.

## Dependencies
This plugin requires:
  - Python3

## How it works
The plugin reads the TCP statistics from '/proc/net/sockstat'.

Notes:
  - All TCP states count as `alloc`
  - All TCP states except `TCP_CLOSE` count as `inuse`

## Performance data
This plugin provides all availale metrics as provided by /proc/net/sockstat.
  - alloc
  - inuse
  - mem
  - orphan
  - tw

Let me know if you find additional metrics on operating systems or kernel versions I did not test - or feel free to add them to the README. :)

## Usage
See the examples below or execute the plugin with -h/--help.

## Examples
Raise a critical alarm if there are more than 1000 used or 1500 allocated TCP sockets:
```
./check_linux_tcp_sockets  --tcp-inuse-crit 1000 --tcp-alloc-crit 1500
SOCKSTAT TCP OK - inuse is 3; orphan is 0; tw is 0; alloc is 4; mem is 1 | inuse=3;;1000 orphan=0 tw=0 alloc=4;;1500 mem=1
```

Raise a warning alarm if there are more the mem counter is greater than 5000 or a critical alarm if there are more than 20000 allocated TCP sockets:
```
./check_linux_tcp_sockets  --tcp-inuse-crit 20000 --tcp-mem-warn 5000
SOCKSTAT TCP OK - inuse is 3; orphan is 0; tw is 0; alloc is 4; mem is 1 | inuse=3;;20000 orphan=0 tw=0 alloc=4 mem=1;5000
```

So you can define thresholds for any metrics and it's fine to omit just the warn or crit thresholds.
