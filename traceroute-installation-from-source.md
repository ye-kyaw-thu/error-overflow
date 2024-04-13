## Installation of Traceroute

Sometimes you will need traceroute command for tracing the network connections.  
Got Errorn on my Ubuntu OS 23.10 machine as follows:  

```
(base) ye@lst-hpc3090:~$ sudo apt-get install traceroute
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Package traceroute is not available, but is referred to by another package.
This may mean that the package is missing, has been obsoleted, or
is only available from another source

E: Package 'traceroute' has no installation candidate
```

```
(base) ye@lst-hpc3090:~$ sudo apt install traceroute
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Package traceroute is not available, but is referred to by another package.
This may mean that the package is missing, has been obsoleted, or
is only available from another source

E: Package 'traceroute' has no installation candidate
(base) ye@lst-hpc3090:~$
```

## Installation from Source

```
(base) ye@lst-hpc3090:~/tool$ wget http://deb.debian.org/debian/pool/main/t/traceroute/traceroute_2.1.0.orig.tar.gz
--2024-04-13 11:25:30--  http://deb.debian.org/debian/pool/main/t/traceroute/traceroute_2.1.0.orig.tar.gz
Resolving deb.debian.org (deb.debian.org)... 199.232.166.132, 2a04:4e42:69::644
Connecting to deb.debian.org (deb.debian.org)|199.232.166.132|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 71460 (70K) [application/x-gzip]
Saving to: ‘traceroute_2.1.0.orig.tar.gz’

traceroute_2.1.0.orig.tar. 100%[========================================>]  69.79K  --.-KB/s    in 0.07s   

2024-04-13 11:25:34 (1.03 MB/s) - ‘traceroute_2.1.0.orig.tar.gz’ saved [71460/71460]
```

```
(base) ye@lst-hpc3090:~/tool$ tar xvf ./traceroute_2.1.0.orig.tar.gz 
traceroute-2.1.0/
traceroute-2.1.0/chvers.sh
traceroute-2.1.0/COPYING
traceroute-2.1.0/wrappers/
traceroute-2.1.0/wrappers/tracepath
traceroute-2.1.0/wrappers/README.wrappers
traceroute-2.1.0/wrappers/Makefile
traceroute-2.1.0/wrappers/tcptraceroute.8
traceroute-2.1.0/wrappers/traceroute-nanog
traceroute-2.1.0/wrappers/tcptraceroute
traceroute-2.1.0/wrappers/traceproto
traceroute-2.1.0/wrappers/lft
traceroute-2.1.0/README
traceroute-2.1.0/VERSION
traceroute-2.1.0/Makefile
traceroute-2.1.0/traceroute.spec
traceroute-2.1.0/TODO
traceroute-2.1.0/libsupp/
traceroute-2.1.0/libsupp/clif.h
traceroute-2.1.0/libsupp/clif.c
traceroute-2.1.0/CREDITS
traceroute-2.1.0/traceroute/
traceroute-2.1.0/traceroute/module.c
traceroute-2.1.0/traceroute/mod-tcpconn.c
traceroute-2.1.0/traceroute/mod-raw.c
traceroute-2.1.0/traceroute/poll.c
traceroute-2.1.0/traceroute/random.c
traceroute-2.1.0/traceroute/extension.c
traceroute-2.1.0/traceroute/flowlabel.h
traceroute-2.1.0/traceroute/as_lookups.c
traceroute-2.1.0/traceroute/mod-udp.c
traceroute-2.1.0/traceroute/csum.c
traceroute-2.1.0/traceroute/traceroute.h
traceroute-2.1.0/traceroute/mod-tcp.c
traceroute-2.1.0/traceroute/mod-dccp.c
traceroute-2.1.0/traceroute/mod-icmp.c
traceroute-2.1.0/traceroute/traceroute.c
traceroute-2.1.0/traceroute/time.c
traceroute-2.1.0/traceroute/traceroute.8
traceroute-2.1.0/store.sh
traceroute-2.1.0/include/
traceroute-2.1.0/include/version.h
traceroute-2.1.0/Make.rules
traceroute-2.1.0/COPYING.LIB
traceroute-2.1.0/Make.defines
traceroute-2.1.0/default.rules
traceroute-2.1.0/ChangeLog
(base) ye@lst-hpc3090:~/tool$ cd traceroute-2.1.0/
(base) ye@lst-hpc3090:~/tool/traceroute-2.1.0$ 
(base) ye@lst-hpc3090:~/tool/traceroute-2.1.0$ make
gcc -O2 -Wall -D_GNU_SOURCE -c clif.c
In file included from /usr/include/string.h:548,
                 from clif.c:11:
In function ‘strncpy’,
    inlined from ‘err_bad_arg’ at clif.c:236:6:
/usr/include/x86_64-linux-gnu/bits/string_fortified.h:95:10: warning: ‘__builtin_strncpy’ specified bound 80 equals destination size [-Wstringop-truncation]
   95 |   return __builtin___strncpy_chk (__dest, __src, __len,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   96 |       __glibc_objsize (__dest));
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~
In function ‘strncpy’,
    inlined from ‘err_bad_arg’ at clif.c:232:6:
/usr/include/x86_64-linux-gnu/bits/string_fortified.h:95:10: warning: ‘__builtin_strncpy’ specified bound 80 equals destination size [-Wstringop-truncation]
   95 |   return __builtin___strncpy_chk (__dest, __src, __len,
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
   96 |       __glibc_objsize (__dest));
      |       ~~~~~~~~~~~~~~~~~~~~~~~~~
rm -f libsupp.a
ar -rc libsupp.a clif.o
ranlib libsupp.a
gcc -O2 -Wall -D_GNU_SOURCE -c as_lookups.c
gcc -O2 -Wall -D_GNU_SOURCE -c csum.c
gcc -O2 -Wall -D_GNU_SOURCE -c extension.c
gcc -O2 -Wall -D_GNU_SOURCE -c mod-dccp.c
gcc -O2 -Wall -D_GNU_SOURCE -c mod-icmp.c
gcc -O2 -Wall -D_GNU_SOURCE -c mod-raw.c
gcc -O2 -Wall -D_GNU_SOURCE -c mod-tcp.c
gcc -O2 -Wall -D_GNU_SOURCE -c mod-tcpconn.c
gcc -O2 -Wall -D_GNU_SOURCE -c mod-udp.c
gcc -O2 -Wall -D_GNU_SOURCE -c module.c
gcc -O2 -Wall -D_GNU_SOURCE -c poll.c
gcc -O2 -Wall -D_GNU_SOURCE -c random.c
gcc -O2 -Wall -D_GNU_SOURCE -c time.c
gcc -O2 -Wall -D_GNU_SOURCE -c traceroute.c
gcc -s -o traceroute as_lookups.o csum.o extension.o mod-dccp.o mod-icmp.o mod-raw.o mod-tcp.o mod-tcpconn.o mod-udp.o module.o poll.o random.o time.o traceroute.o  -lsupp -lm 
(base) ye@lst-hpc3090:~/tool/traceroute-2.1.0$
```

```
(base) ye@lst-hpc3090:~/tool/traceroute-2.1.0$ sudo make install
cp traceroute /usr/local/bin
cp -f traceroute.8 /usr/local/share/man/man8
(base) ye@lst-hpc3090:~/tool/traceroute-2.1.0$
```

Call --help ...  

```
(base) ye@lst-hpc3090:~/tool/traceroute-2.1.0$ traceroute --help
Usage:
  traceroute [ -46dFITnreAUDV ] [ -f first_ttl ] [ -g gate,... ] [ -i device ] [ -m max_ttl ] [ -N squeries ] [ -p port ] [ -t tos ] [ -l flow_label ] [ -w MAX,HERE,NEAR ] [ -q nqueries ] [ -s src_addr ] [ -z sendwait ] [ --fwmark=num ] host [ packetlen ]
Options:
  -4                          Use IPv4
  -6                          Use IPv6
  -d  --debug                 Enable socket level debugging
  -F  --dont-fragment         Do not fragment packets
  -f first_ttl  --first=first_ttl
                              Start from the first_ttl hop (instead from 1)
  -g gate,...  --gateway=gate,...
                              Route packets through the specified gateway
                              (maximum 8 for IPv4 and 127 for IPv6)
  -I  --icmp                  Use ICMP ECHO for tracerouting
  -T  --tcp                   Use TCP SYN for tracerouting (default port is 80)
  -i device  --interface=device
                              Specify a network interface to operate with
  -m max_ttl  --max-hops=max_ttl
                              Set the max number of hops (max TTL to be
                              reached). Default is 30
  -N squeries  --sim-queries=squeries
                              Set the number of probes to be tried
                              simultaneously (default is 16)
  -n                          Do not resolve IP addresses to their domain names
  -p port  --port=port        Set the destination port to use. It is either
                              initial udp port value for "default" method
                              (incremented by each probe, default is 33434), or
                              initial seq for "icmp" (incremented as well,
                              default from 1), or some constant destination
                              port for other methods (with default of 80 for
                              "tcp", 53 for "udp", etc.)
  -t tos  --tos=tos           Set the TOS (IPv4 type of service) or TC (IPv6
                              traffic class) value for outgoing packets
  -l flow_label  --flowlabel=flow_label
                              Use specified flow_label for IPv6 packets
  -w MAX,HERE,NEAR  --wait=MAX,HERE,NEAR
                              Wait for a probe no more than HERE (default 3)
                              times longer than a response from the same hop,
                              or no more than NEAR (default 10) times than some
                              next hop, or MAX (default 5.0) seconds (float
                              point values allowed too)
  -q nqueries  --queries=nqueries
                              Set the number of probes per each hop. Default is
                              3
  -r                          Bypass the normal routing and send directly to a
                              host on an attached network
  -s src_addr  --source=src_addr
                              Use source src_addr for outgoing packets
  -z sendwait  --sendwait=sendwait
                              Minimal time interval between probes (default 0).
                              If the value is more than 10, then it specifies a
                              number in milliseconds, else it is a number of
                              seconds (float point values allowed too)
  -e  --extensions            Show ICMP extensions (if present), including MPLS
  -A  --as-path-lookups       Perform AS path lookups in routing registries and
                              print results directly after the corresponding
                              addresses
  -M name  --module=name      Use specified module (either builtin or external)
                              for traceroute operations. Most methods have
                              their shortcuts (`-I' means `-M icmp' etc.)
  -O OPTS,...  --options=OPTS,...
                              Use module-specific option OPTS for the
                              traceroute module. Several OPTS allowed,
                              separated by comma. If OPTS is "help", print info
                              about available options
  --sport=num                 Use source port num for outgoing packets. Implies
                              `-N 1'
  --fwmark=num                Set firewall mark for outgoing packets
  -U  --udp                   Use UDP to particular port for tracerouting
                              (instead of increasing the port per each probe),
                              default port is 53
  -UL                         Use UDPLITE for tracerouting (default dest port
                              is 53)
  -D  --dccp                  Use DCCP Request for tracerouting (default port
                              is 33434)
  -P prot  --protocol=prot    Use raw packet of protocol prot for tracerouting
  --mtu                       Discover MTU along the path being traced. Implies
                              `-F -N 1'
  --back                      Guess the number of hops in the backward path and
                              print if it differs
  -V  --version               Print version info and exit
  --help                      Read this help and exit

Arguments:
+     host          The host to traceroute to
      packetlen     The full packet length (default is the length of an IP
                    header plus 40). Can be ignored or increased to a minimal
                    allowed value
(base) ye@lst-hpc3090:~/tool/traceroute-2.1.0$ 
```

## Testing 

testing with facebook.com  

```
(base) ye@lst-hpc3090:~/tool/traceroute-2.1.0$ traceroute facebook.com
traceroute to facebook.com (163.70.149.35), 30 hops max, 60 byte packets
 1  _gateway (10.222.32.1)  0.885 ms  0.864 ms  0.860 ms
 2  * * *
 3  * * *
 4  * * *
 5  10.255.255.1 (10.255.255.1)  0.360 ms 10.224.251.145 (10.224.251.145)  0.477 ms  0.473 ms
 6  10.224.251.1 (10.224.251.1)  0.420 ms 10.224.251.141 (10.224.251.141)  0.549 ms  0.526 ms
 7  10.224.251.38 (10.224.251.38)  0.869 ms  0.860 ms 10.224.251.1 (10.224.251.1)  0.421 ms
 8  10.224.251.33 (10.224.251.33)  1.159 ms  1.155 ms  1.141 ms
 9  202.29.227.29 (202.29.227.29)  1.349 ms 10.224.251.33 (10.224.251.33)  1.133 ms 202.29.227.29 (202.29.227.29)  1.341 ms
10  202.29.227.29 (202.29.227.29)  1.231 ms 100.64.255.142 (100.64.255.142)  3.863 ms 202.29.227.29 (202.29.227.29)  1.211 ms
11  100.64.255.142 (100.64.255.142)  3.846 ms  3.842 ms  3.708 ms
12  202.28.218.101 (202.28.218.101)  3.294 ms  4.034 ms 203.159.68.162 (203.159.68.162)  20.556 ms
13  po204.asw03.bkk1.tfbnw.net (157.240.120.182)  2.981 ms po204.asw01.bkk1.tfbnw.net (157.240.119.210)  4.817 ms po204.asw04.bkk1.tfbnw.net (157.240.120.190)  4.845 ms
14  po204.asw02.bkk1.tfbnw.net (157.240.120.174)  3.001 ms  2.997 ms psw04.bkk1.tfbnw.net (129.134.112.150)  2.987 ms
15  psw04.bkk1.tfbnw.net (129.134.112.150)  3.011 ms msw1ac.02.bkk1.tfbnw.net (129.134.112.167)  7.950 ms msw1ar.02.bkk1.tfbnw.net (129.134.112.170)  6.597 ms
16  * * msw1ag.02.bkk1.tfbnw.net (129.134.112.163)  7.136 ms
17  * * *
18  * * *
19  * * *
20  * * *
21  * * *
22  * * *
23  * * *
24  * * *
25  * * *
26  * * *
27  * * *
28  * * *
29  * * *
30  * * *
(base) ye@lst-hpc3090:~/tool/traceroute-2.1.0$
```

The traceroute to Facebook (facebook.com) also seems to be functioning normally.  

testing with the problem link repo.anaconda.com  ...   

```
(base) ye@lst-hpc3090:~/tool/traceroute-2.1.0$ traceroute repo.anaconda.com
traceroute to repo.anaconda.com (104.16.191.158), 30 hops max, 60 byte packets
 1  _gateway (10.222.32.1)  0.721 ms  0.898 ms  0.894 ms
 2  * * *
 3  * * *
 4  * 10.255.255.1 (10.255.255.1)  0.399 ms *
 5  10.255.255.1 (10.255.255.1)  0.392 ms  0.389 ms 10.224.251.145 (10.224.251.145)  0.433 ms
 6  10.224.251.1 (10.224.251.1)  0.434 ms  0.396 ms 10.224.251.141 (10.224.251.141)  0.385 ms
 7  10.224.251.1 (10.224.251.1)  0.383 ms  0.379 ms *
 8  * * *
 9  * * *
10  * * *
11  * * *
12  * * *
13  * * *
14  * * *
15  * * *
16  * * *
17  * * *
18  * * *
19  * * *
20  * * *
21  * * *
22  * * *
23  * * *
24  * * *
25  * * *
26  * * *
27  * * *
28  * * *
29  * * *
30  * * *
(base) ye@lst-hpc3090:~/tool/traceroute-2.1.0$
```

Problem!

```
(base) ye@lst-hpc3090:~/tool/traceroute-2.1.0$ traceroute google.com
traceroute to google.com (172.217.194.113), 30 hops max, 60 byte packets
 1  _gateway (10.222.32.1)  0.913 ms  1.090 ms  1.085 ms
 2  * * *
 3  * * *
 4  10.255.255.1 (10.255.255.1)  0.488 ms * *
 5  10.255.255.1 (10.255.255.1)  0.476 ms 10.224.251.145 (10.224.251.145)  0.466 ms 10.255.255.1 (10.255.255.1)  0.468 ms
 6  10.224.251.141 (10.224.251.141)  0.566 ms  0.482 ms 10.224.251.1 (10.224.251.1)  0.465 ms
 7  10.224.251.38 (10.224.251.38)  0.901 ms 10.224.251.1 (10.224.251.1)  0.457 ms 10.224.251.38 (10.224.251.38)  0.876 ms
 8  10.224.251.38 (10.224.251.38)  0.830 ms  0.808 ms  0.790 ms
 9  202.29.227.29 (202.29.227.29)  1.508 ms  1.504 ms 10.224.251.33 (10.224.251.33)  1.089 ms
10  100.64.255.142 (100.64.255.142)  2.744 ms 202.29.227.29 (202.29.227.29)  1.493 ms  1.277 ms
11  100.64.254.49 (100.64.254.49)  3.240 ms 100.64.255.142 (100.64.255.142)  2.471 ms 100.64.254.49 (100.64.254.49)  2.937 ms
12  100.64.249.25 (100.64.249.25)  2.207 ms 202.28.218.17 (202.28.218.17)  4.541 ms 100.64.251.205 (100.64.251.205)  6.698 ms
13  61.19.7.86 (61.19.7.86)  6.315 ms  5.970 ms 122.155.230.129 (122.155.230.129)  4.178 ms
14  74.125.50.222 (74.125.50.222)  29.535 ms 61.19.7.206 (61.19.7.206)  3.137 ms 74.125.50.222 (74.125.50.222)  29.531 ms
15  142.251.232.69 (142.251.232.69)  33.312 ms  35.531 ms 64.233.175.139 (64.233.175.139)  34.746 ms
16  192.178.109.212 (192.178.109.212)  30.360 ms 142.251.230.50 (142.251.230.50)  34.820 ms 142.251.232.69 (142.251.232.69)  34.863 ms
17  216.239.50.192 (216.239.50.192)  35.247 ms 192.178.109.212 (192.178.109.212)  34.890 ms *
18  * 142.251.252.39 (142.251.252.39)  35.036 ms *
19  74.125.37.235 (74.125.37.235)  33.972 ms 142.251.229.238 (142.251.229.238)  40.752 ms 209.85.246.225 (209.85.246.225)  32.567 ms
20  209.85.245.135 (209.85.245.135)  33.922 ms 66.249.94.85 (66.249.94.85)  34.261 ms 66.249.94.185 (66.249.94.185)  33.818 ms
21  * * *
22  * * *
23  * * *
24  * * *
25  * * *
26  * * *
27  * * *
28  * si-in-f113.1e100.net (172.217.194.113)  33.551 ms *
(base) ye@lst-hpc3090:~/tool/traceroute-2.1.0$ 
```

Success!  



