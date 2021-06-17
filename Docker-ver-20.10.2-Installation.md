# Docker Installation on Local Machine

Local machine စက်ထဲမှာ docker က ရှိမနေပါဘူး။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/NECTEC/hpc/tst$ docker
Command 'docker' not found, but can be installed with:
sudo snap install docker     # version 19.03.13, or
sudo apt  install docker.io  # version 20.10.2-0ubuntu1~20.10.1
See 'snap info docker' for additional versions.
```

အရင် ဆုံး ကိုယ့်စက်ထဲမှာ docker ရှိနေခဲ့ရင်၊ ဖျက်ချင်ရင် အောက်ပါ command:  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/NECTEC/hpc/tst$ sudo apt-get remove docker docker-engine docker.io
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
E: Unable to locate package docker-engine
```

system က up-to-date ဖြစ်စေချင်ရင်...   

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/NECTEC/hpc/tst$ sudo apt-get update
Hit:1 http://dl.google.com/linux/chrome/deb stable InRelease
Hit:2 https://packages.microsoft.com/repos/ms-teams stable InRelease                                                                        
Hit:3 http://ppa.launchpad.net/sylvain-pineau/kazam/ubuntu groovy InRelease                                                                 
Get:4 http://security.ubuntu.com/ubuntu groovy-security InRelease [110 kB]                                                                                  
Ign:5 http://ppa.launchpad.net/videolan/stable-daily/ubuntu groovy InRelease                                                                                
Hit:6 http://mm.archive.ubuntu.com/ubuntu groovy InRelease                    
Get:7 http://mm.archive.ubuntu.com/ubuntu groovy-updates InRelease [115 kB]         
Err:8 http://ppa.launchpad.net/videolan/stable-daily/ubuntu groovy Release                
  404  Not Found [IP: 91.189.95.85 80]
Get:9 http://mm.archive.ubuntu.com/ubuntu groovy-backports InRelease [101 kB]             
Reading package lists... Done     
E: The repository 'http://ppa.launchpad.net/videolan/stable-daily/ubuntu groovy Release' does not have a Release file.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
```

Docker ကို installation လုပ်...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/NECTEC/hpc/tst$ sudo apt install docker.io
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  apturl-common gir1.2-goa-1.0 ibverbs-providers libboost-atomic-dev libboost-atomic1.71-dev libboost-atomic1.71.0 libboost-chrono-dev libboost-chrono1.71-dev libboost-chrono1.71.0
  libboost-container-dev libboost-container1.71-dev libboost-container1.71.0 libboost-context-dev libboost-context1.71-dev libboost-context1.71.0 libboost-coroutine-dev libboost-coroutine1.71-dev
  libboost-coroutine1.71.0 libboost-date-time-dev libboost-date-time1.71-dev libboost-dev libboost-exception-dev libboost-exception1.71-dev libboost-fiber-dev libboost-fiber1.71-dev
  libboost-fiber1.71.0 libboost-filesystem-dev libboost-filesystem1.71-dev libboost-graph-parallel-dev libboost-graph-parallel1.71-dev libboost-graph-parallel1.71.0 libboost-graph1.71.0
  libboost-locale-dev libboost-locale1.71-dev libboost-log1.71.0 libboost-math-dev libboost-math1.71-dev libboost-math1.71.0 libboost-mpi-dev libboost-mpi-python-dev libboost-mpi-python1.71-dev
  libboost-mpi-python1.71.0 libboost-mpi1.71-dev libboost-mpi1.71.0 libboost-numpy-dev libboost-numpy1.71-dev libboost-numpy1.71.0 libboost-program-options-dev libboost-program-options1.71-dev
  libboost-program-options1.71.0 libboost-python-dev libboost-python1.71-dev libboost-python1.71.0 libboost-random-dev libboost-random1.71-dev libboost-random1.71.0 libboost-regex1.71.0
  libboost-serialization-dev libboost-serialization1.71-dev libboost-serialization1.71.0 libboost-stacktrace-dev libboost-stacktrace1.71-dev libboost-stacktrace1.71.0 libboost-system-dev
  libboost-system1.71-dev libboost-system1.71.0 libboost-test-dev libboost-test1.71-dev libboost-test1.71.0 libboost-thread-dev libboost-thread1.71-dev libboost-timer-dev libboost-timer1.71-dev
  libboost-timer1.71.0 libboost-tools-dev libboost-type-erasure-dev libboost-type-erasure1.71-dev libboost-type-erasure1.71.0 libboost-wave-dev libboost-wave1.71-dev libboost-wave1.71.0
  libboost1.71-dev libboost1.71-tools-dev libcaf-openmpi-3 libcoarrays-openmpi-dev libevent-2.1-7 libevent-core-2.1-7 libevent-dev libevent-extra-2.1-7 libevent-openssl-2.1-7 libevent-pthreads-2.1-7
  libfabric1 libhwloc-dev libhwloc-plugins libhwloc15 libibverbs-dev libibverbs1 libnl-3-dev libnl-route-3-dev libnuma-dev libopenmpi-dev libopenmpi3 libpmix2 libpsm-infinipath1 libpsm2-2 librdmacm1
  mpi-default-bin mpi-default-dev openmpi-bin openmpi-common python3-click python3-colorama python3-dateutil python3-software-properties software-properties-common unattended-upgrades
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  bridge-utils containerd pigz runc ubuntu-fan
Suggested packages:
  ifupdown aufs-tools btrfs-progs cgroupfs-mount | cgroup-lite debootstrap docker-doc rinse zfs-fuse | zfsutils
The following NEW packages will be installed:
  bridge-utils containerd docker.io pigz runc ubuntu-fan
0 upgraded, 6 newly installed, 0 to remove and 81 not upgraded.
Need to get 71.3 MB of archives.
After this operation, 342 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 pigz amd64 2.4-1 [57.4 kB]
Get:2 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 bridge-utils amd64 1.6-3ubuntu1 [30.9 kB]
Get:3 http://mm.archive.ubuntu.com/ubuntu groovy-updates/main amd64 runc amd64 1.0.0~rc95-0ubuntu1~20.10.1 [4,075 kB]
Get:4 http://mm.archive.ubuntu.com/ubuntu groovy-updates/main amd64 containerd amd64 1.4.4-0ubuntu1~20.10.1 [30.2 MB]
Get:5 http://mm.archive.ubuntu.com/ubuntu groovy-updates/universe amd64 docker.io amd64 20.10.2-0ubuntu1~20.10.1 [36.9 MB]
Get:6 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 ubuntu-fan all 0.12.13 [34.5 kB]                                                                                                              
Fetched 71.3 MB in 6s (11.5 MB/s)                                                                                                                                                                         
Preconfiguring packages ...
Selecting previously unselected package pigz.
(Reading database ... 573451 files and directories currently installed.)
Preparing to unpack .../0-pigz_2.4-1_amd64.deb ...
Unpacking pigz (2.4-1) ...
Selecting previously unselected package bridge-utils.
Preparing to unpack .../1-bridge-utils_1.6-3ubuntu1_amd64.deb ...
Unpacking bridge-utils (1.6-3ubuntu1) ...
Selecting previously unselected package runc.
Preparing to unpack .../2-runc_1.0.0~rc95-0ubuntu1~20.10.1_amd64.deb ...
Unpacking runc (1.0.0~rc95-0ubuntu1~20.10.1) ...
Selecting previously unselected package containerd.
Preparing to unpack .../3-containerd_1.4.4-0ubuntu1~20.10.1_amd64.deb ...
Unpacking containerd (1.4.4-0ubuntu1~20.10.1) ...
Selecting previously unselected package docker.io.
Preparing to unpack .../4-docker.io_20.10.2-0ubuntu1~20.10.1_amd64.deb ...
Unpacking docker.io (20.10.2-0ubuntu1~20.10.1) ...
Selecting previously unselected package ubuntu-fan.
Preparing to unpack .../5-ubuntu-fan_0.12.13_all.deb ...
Unpacking ubuntu-fan (0.12.13) ...
Setting up runc (1.0.0~rc95-0ubuntu1~20.10.1) ...
Setting up bridge-utils (1.6-3ubuntu1) ...
Setting up pigz (2.4-1) ...
Setting up containerd (1.4.4-0ubuntu1~20.10.1) ...
Created symlink /etc/systemd/system/multi-user.target.wants/containerd.service → /lib/systemd/system/containerd.service.
Setting up ubuntu-fan (0.12.13) ...
Created symlink /etc/systemd/system/multi-user.target.wants/ubuntu-fan.service → /lib/systemd/system/ubuntu-fan.service.
Setting up docker.io (20.10.2-0ubuntu1~20.10.1) ...
Adding group `docker' (GID 137) ...
Done.
Created symlink /etc/systemd/system/multi-user.target.wants/docker.service → /lib/systemd/system/docker.service.
Created symlink /etc/systemd/system/sockets.target.wants/docker.socket → /lib/systemd/system/docker.socket.
Processing triggers for systemd (246.6-1ubuntu1.3) ...
Processing triggers for man-db (2.9.3-2) ...
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/NECTEC/hpc/tst$ 
```

dependency packages တွေကို installation လုပ်...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/NECTEC/hpc/tst$ sudo snap install docker
```

ခဏ ကြာမယ်... အဆင်ပြေပြေနဲ့ docker dependency package တွေကို installation လုပ်နိုင်ခဲ့ရင် အောက်ပါ message ကို မြင်ရလိမ့်မယ်။  

```
docker 19.03.13 from Canonical✓ installed
```

install လုပ်ထားတဲ့ Docker ရဲ့ version ကို ရိုက်ကြည့်ရအောင်...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/NECTEC/hpc/tst$ docker --version
Docker version 20.10.2, build 20.10.2-0ubuntu1~20.10.1
```

Docker hub ကနေ hello-world လို့ခေါ်တဲ့ image ကို pull လုပ်ကြည့်ရအောင်...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/NECTEC/hpc/tst$ time sudo docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
b8dfde127a29: Pull complete 
Digest: sha256:9f6ad537c5132bcce57f7a0a20e317228d382c3cd61edae14650eec68b2b345c
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/


real	0m7.060s
user	0m0.032s
sys	0m0.032s
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/NECTEC/hpc/tst$
```

အဆင်ပြေပြေနဲ့ docker image ကို pull လုပ်သွားခဲ့သလား ဆိုတာကို confirmation လုပ်ကြည့်ရအောင်...   

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/NECTEC/hpc/tst$ sudo docker images
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
hello-world   latest    d1165f221234   3 months ago   13.3kB
```

Pull လုပ်ထားတဲ့ container အားလုံးကို ကြည့်ချင်ရင်...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/NECTEC/hpc/tst$ sudo docker ps -a
CONTAINER ID   IMAGE         COMMAND    CREATED              STATUS                          PORTS     NAMES
b656b6c2a86b   hello-world   "/hello"   About a minute ago   Exited (0) About a minute ago             gracious_chebyshev
```

လက်ရှိ run နေတဲ့ docker တွေကို ကြည့်ချင်ရင်...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/NECTEC/hpc/tst$ sudo docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/NECTEC/hpc/tst$ 
```
