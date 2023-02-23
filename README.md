pussh
=====

PUSSH is "Pythonic Ubiquitous SSH" - a command line wrapper script for 
sending commands to multiple machines in parallel, i.e. in *real time*, with 
options for controlling the degree of parallelism, timeouts, and node selections.

This latest PuSSH from Feb 23, 2023 - version 2.3! ...  makes it so you can specify 
your key ... which means you are no longer locked into using .ssh/id_rsa, or id_dsa as
before.

A few, smaller problems have appeared in the meantime:

- sequential command processing no longer works
- you MUST now specify the timeout value with the -t flag 
- you MUST now specify the abovementioned, specific ssh key whatever that may be

The above 3 issues are of a smaller, interim nature that I didn't get a chance to fix yet, but 
clearly not so bad as not being able to specify keys. 

Don't forget also you need the 'nc' package installed. All of the above points are in the
TODO.txt.

The way to use this tool, right out of the box is like so:

```git clone https://github.com/linksonice/pussh.git
cd pussh
./pussh -t 4  -i ../.ssh/london.pem node0[3-7,9] uptime

which will output:

node07:
 11:56:40 up  2:32,  1 user,  load average: 0.32, 0.09, 0.03
node03:
 11:56:40 up  2:32,  1 user,  load average: 0.32, 0.09, 0.03
node04:
 11:56:40 up  2:32,  1 user,  load average: 0.32, 0.09, 0.03
node05:
 11:56:40 up  2:32,  1 user,  load average: 0.32, 0.09, 0.03
node06:
 11:56:40 up  2:32,  1 user,  load average: 0.32, 0.09, 0.03
node09:
 11:56:40 up  2:32,  1 user,  load average: 0.32, 0.09, 0.03

or if you like:

[andrei@ip-10-0-1-110 pussh]$ ./pussh -t 4  -i ../.ssh/london.pem --prefix node0[3-7,9] uptime

which will output like so for 1 line outputs:

node03:  12:03:03 up  2:38,  1 user,  load average: 0.88, 0.20, 0.06
node04:  12:03:03 up  2:38,  1 user,  load average: 0.88, 0.20, 0.06
node05:  12:03:03 up  2:38,  1 user,  load average: 0.88, 0.20, 0.06
node06:  12:03:03 up  2:38,  1 user,  load average: 0.88, 0.20, 0.06
node07:  12:03:03 up  2:38,  1 user,  load average: 0.88, 0.20, 0.06
node09:  12:03:03 up  2:38,  1 user,  load average: 0.88, 0.20, 0.06

or much the same for multi-line cmd outputs:

[andrei@ip-10-0-1-110 pussh]$ ./pussh -t 4  -i ../.ssh/london.pem --prefix node0[3-7,9] cat /etc/hosts
node03: 127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4 node01 node02 node03 node04 node05 node06 node07 node08 node09 node10
node03: ::1         localhost6 localhost6.localdomain6
node04: 127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4 node01 node02 node03 node04 node05 node06 node07 node08 node09 node10
node04: ::1         localhost6 localhost6.localdomain6
node05: 127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4 node01 node02 node03 node04 node05 node06 node07 node08 node09 node10
node05: ::1         localhost6 localhost6.localdomain6
node06: 127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4 node01 node02 node03 node04 node05 node06 node07 node08 node09 node10
node06: ::1         localhost6 localhost6.localdomain6
node07: 127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4 node01 node02 node03 node04 node05 node06 node07 node08 node09 node10
node07: ::1         localhost6 localhost6.localdomain6
node09: 127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4 node01 node02 node03 node04 node05 node06 node07 node08 node09 node10
node09: ::1         localhost6 localhost6.localdomain6
