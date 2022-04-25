# Verify You Have a CUDA-Capable GPU

```
ye@ye-System-Product-Name:~$ lspci | grep -i nvidia
01:00.0 VGA compatible controller: NVIDIA Corporation TU102 [GeForce RTX 2080 Ti Rev. A] (rev a1)
01:00.1 Audio device: NVIDIA Corporation TU102 High Definition Audio Controller (rev a1)
01:00.2 USB controller: NVIDIA Corporation TU102 USB 3.1 Host Controller (rev a1)
01:00.3 Serial bus controller: NVIDIA Corporation TU102 USB Type-C UCSI Controller (rev a1)
05:00.0 VGA compatible controller: NVIDIA Corporation TU106 [GeForce RTX 2070 Rev. A] (rev a1)
05:00.1 Audio device: NVIDIA Corporation TU106 High Definition Audio Controller (rev a1)
05:00.2 USB controller: NVIDIA Corporation TU106 USB 3.1 Host Controller (rev a1)
05:00.3 Serial bus controller: NVIDIA Corporation TU106 USB Type-C UCSI Controller (rev a1)
ye@ye-System-Product-Name:~$
```

## Check Linux OS Version

```
ye@ye-System-Product-Name:~$  uname -m && cat /etc/*release
x86_64
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=22.04
DISTRIB_CODENAME=jammy
DISTRIB_DESCRIPTION="Ubuntu 22.04 LTS"
PRETTY_NAME="Ubuntu 22.04 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04 (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy
ye@ye-System-Product-Name:~$Verify You Have a CUDA-Capable GPU
```

## Check gcc 

```
ye@ye-System-Product-Name:~$ gcc --version
Command 'gcc' not found, but can be installed with:
sudo apt install gcc
```

gcc က စက်အသစ်မှာ မရှိသေးလို့ installation လုပ်ခဲ့...  

```
ye@ye-System-Product-Name:~$ sudo apt install gcc
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  binutils binutils-common binutils-x86-64-linux-gnu gcc-11 libasan6 libatomic1 libbinutils libc-dev-bin libc-devtools
  libc6-dev libcc1-0 libcrypt-dev libctf-nobfd0 libctf0 libgcc-11-dev libitm1 liblsan0 libnsl-dev libquadmath0 libtirpc-dev
  libtsan0 libubsan1 linux-libc-dev manpages-dev rpcsvc-proto
Suggested packages:
  binutils-doc gcc-multilib make autoconf automake libtool flex bison gcc-doc gcc-11-multilib gcc-11-doc gcc-11-locales
  glibc-doc
The following NEW packages will be installed:
  binutils binutils-common binutils-x86-64-linux-gnu gcc gcc-11 libasan6 libatomic1 libbinutils libc-dev-bin libc-devtools
  libc6-dev libcc1-0 libcrypt-dev libctf-nobfd0 libctf0 libgcc-11-dev libitm1 liblsan0 libnsl-dev libquadmath0 libtirpc-dev
  libtsan0 libubsan1 linux-libc-dev manpages-dev rpcsvc-proto
0 upgraded, 26 newly installed, 0 to remove and 0 not upgraded.
Need to get 39.1 MB of archives.
After this operation, 131 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 binutils-common amd64 2.38-3ubuntu1 [221 kB]
Get:2 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libbinutils amd64 2.38-3ubuntu1 [662 kB]
Get:3 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libctf-nobfd0 amd64 2.38-3ubuntu1 [106 kB]
Get:4 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libctf0 amd64 2.38-3ubuntu1 [103 kB]
Get:5 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 binutils-x86-64-linux-gnu amd64 2.38-3ubuntu1 [2,328 kB]
Get:6 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 binutils amd64 2.38-3ubuntu1 [3,186 B]
Get:7 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libcc1-0 amd64 12-20220319-1ubuntu1 [47.2 kB]
Get:8 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libitm1 amd64 12-20220319-1ubuntu1 [30.2 kB]
Get:9 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libatomic1 amd64 12-20220319-1ubuntu1 [10.4 kB]
Get:10 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libasan6 amd64 11.2.0-19ubuntu1 [2,283 kB]
Get:11 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 liblsan0 amd64 12-20220319-1ubuntu1 [1,069 kB]
Get:12 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libtsan0 amd64 11.2.0-19ubuntu1 [2,261 kB]
Get:13 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libubsan1 amd64 12-20220319-1ubuntu1 [976 kB]
Get:14 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libquadmath0 amd64 12-20220319-1ubuntu1 [154 kB]
Get:15 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libgcc-11-dev amd64 11.2.0-19ubuntu1 [2,526 kB]
Get:16 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 gcc-11 amd64 11.2.0-19ubuntu1 [20.1 MB]
Get:17 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 gcc amd64 4:11.2.0-1ubuntu1 [5,112 B]
Get:18 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libc-dev-bin amd64 2.35-0ubuntu3 [20.3 kB]
Get:19 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libc-devtools amd64 2.35-0ubuntu3 [28.9 kB]
Get:20 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 linux-libc-dev amd64 5.15.0-25.25 [1,305 kB]
Get:21 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libcrypt-dev amd64 1:4.4.27-1 [112 kB]
Get:22 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 rpcsvc-proto amd64 1.4.2-0ubuntu6 [68.5 kB]
Get:23 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libtirpc-dev amd64 1.3.2-2build1 [192 kB]
Get:24 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libnsl-dev amd64 1.3.0-2build2 [71.3 kB]
Get:25 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libc6-dev amd64 2.35-0ubuntu3 [2,099 kB]
Get:26 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 manpages-dev all 5.10-1ubuntu1 [2,309 kB]
Fetched 39.1 MB in 2s (20.6 MB/s)        
Selecting previously unselected package binutils-common:amd64.
(Reading database ... 160258 files and directories currently installed.)
Preparing to unpack .../00-binutils-common_2.38-3ubuntu1_amd64.deb ...
Unpacking binutils-common:amd64 (2.38-3ubuntu1) ...
Selecting previously unselected package libbinutils:amd64.
Preparing to unpack .../01-libbinutils_2.38-3ubuntu1_amd64.deb ...
Unpacking libbinutils:amd64 (2.38-3ubuntu1) ...
Selecting previously unselected package libctf-nobfd0:amd64.
Preparing to unpack .../02-libctf-nobfd0_2.38-3ubuntu1_amd64.deb ...
Unpacking libctf-nobfd0:amd64 (2.38-3ubuntu1) ...
Selecting previously unselected package libctf0:amd64.
Preparing to unpack .../03-libctf0_2.38-3ubuntu1_amd64.deb ...
Unpacking libctf0:amd64 (2.38-3ubuntu1) ...
Selecting previously unselected package binutils-x86-64-linux-gnu.
Preparing to unpack .../04-binutils-x86-64-linux-gnu_2.38-3ubuntu1_amd64.deb ...
Unpacking binutils-x86-64-linux-gnu (2.38-3ubuntu1) ...
Selecting previously unselected package binutils.
Preparing to unpack .../05-binutils_2.38-3ubuntu1_amd64.deb ...
Unpacking binutils (2.38-3ubuntu1) ...
Selecting previously unselected package libcc1-0:amd64.
Preparing to unpack .../06-libcc1-0_12-20220319-1ubuntu1_amd64.deb ...
Unpacking libcc1-0:amd64 (12-20220319-1ubuntu1) ...
Selecting previously unselected package libitm1:amd64.
Preparing to unpack .../07-libitm1_12-20220319-1ubuntu1_amd64.deb ...
Unpacking libitm1:amd64 (12-20220319-1ubuntu1) ...
Selecting previously unselected package libatomic1:amd64.
Preparing to unpack .../08-libatomic1_12-20220319-1ubuntu1_amd64.deb ...
Unpacking libatomic1:amd64 (12-20220319-1ubuntu1) ...
Selecting previously unselected package libasan6:amd64.
Preparing to unpack .../09-libasan6_11.2.0-19ubuntu1_amd64.deb ...
Unpacking libasan6:amd64 (11.2.0-19ubuntu1) ...
Selecting previously unselected package liblsan0:amd64.
Preparing to unpack .../10-liblsan0_12-20220319-1ubuntu1_amd64.deb ...
Unpacking liblsan0:amd64 (12-20220319-1ubuntu1) ...
Selecting previously unselected package libtsan0:amd64.
Preparing to unpack .../11-libtsan0_11.2.0-19ubuntu1_amd64.deb ...
Unpacking libtsan0:amd64 (11.2.0-19ubuntu1) ...
Selecting previously unselected package libubsan1:amd64.ye@ye-System-Product-Name:~$ sudo apt install gcc
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  binutils binutils-common binutils-x86-64-linux-gnu gcc-11 libasan6 libatomic1 libbinutils libc-dev-bin libc-devtools
  libc6-dev libcc1-0 libcrypt-dev libctf-nobfd0 libctf0 libgcc-11-dev libitm1 liblsan0 libnsl-dev libquadmath0 libtirpc-dev
  libtsan0 libubsan1 linux-libc-dev manpages-dev rpcsvc-proto
Suggested packages:
  binutils-doc gcc-multilib make autoconf automake libtool flex bison gcc-doc gcc-11-multilib gcc-11-doc gcc-11-locales
  glibc-doc
The following NEW packages will be installed:
  binutils binutils-common binutils-x86-64-linux-gnu gcc gcc-11 libasan6 libatomic1 libbinutils libc-dev-bin libc-devtools
  libc6-dev libcc1-0 libcrypt-dev libctf-nobfd0 libctf0 libgcc-11-dev libitm1 liblsan0 libnsl-dev libquadmath0 libtirpc-dev
  libtsan0 libubsan1 linux-libc-dev manpages-dev rpcsvc-proto
0 upgraded, 26 newly installed, 0 to remove and 0 not upgraded.
Need to get 39.1 MB of archives.
After this operation, 131 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 binutils-common amd64 2.38-3ubuntu1 [221 kB]
Get:2 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libbinutils amd64 2.38-3ubuntu1 [662 kB]
Get:3 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libctf-nobfd0 amd64 2.38-3ubuntu1 [106 kB]
Get:4 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libctf0 amd64 2.38-3ubuntu1 [103 kB]
Get:5 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 binutils-x86-64-linux-gnu amd64 2.38-3ubuntu1 [2,328 kB]
Get:6 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 binutils amd64 2.38-3ubuntu1 [3,186 B]
Get:7 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libcc1-0 amd64 12-20220319-1ubuntu1 [47.2 kB]
Get:8 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libitm1 amd64 12-20220319-1ubuntu1 [30.2 kB]
Get:9 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libatomic1 amd64 12-20220319-1ubuntu1 [10.4 kB]
Get:10 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libasan6 amd64 11.2.0-19ubuntu1 [2,283 kB]
Get:11 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 liblsan0 amd64 12-20220319-1ubuntu1 [1,069 kB]
Get:12 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libtsan0 amd64 11.2.0-19ubuntu1 [2,261 kB]
Get:13 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libubsan1 amd64 12-20220319-1ubuntu1 [976 kB]
Get:14 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libquadmath0 amd64 12-20220319-1ubuntu1 [154 kB]
Get:15 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libgcc-11-dev amd64 11.2.0-19ubuntu1 [2,526 kB]
Get:16 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 gcc-11 amd64 11.2.0-19ubuntu1 [20.1 MB]
Get:17 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 gcc amd64 4:11.2.0-1ubuntu1 [5,112 B]
Get:18 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libc-dev-bin amd64 2.35-0ubuntu3 [20.3 kB]
Get:19 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libc-devtools amd64 2.35-0ubuntu3 [28.9 kB]
Get:20 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 linux-libc-dev amd64 5.15.0-25.25 [1,305 kB]
Get:21 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libcrypt-dev amd64 1:4.4.27-1 [112 kB]
Get:22 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 rpcsvc-proto amd64 1.4.2-0ubuntu6 [68.5 kB]
Get:23 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libtirpc-dev amd64 1.3.2-2build1 [192 kB]
Get:24 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libnsl-dev amd64 1.3.0-2build2 [71.3 kB]
Get:25 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libc6-dev amd64 2.35-0ubuntu3 [2,099 kB]
Get:26 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 manpages-dev all 5.10-1ubuntu1 [2,309 kB]
Fetched 39.1 MB in 2s (20.6 MB/s)        
Selecting previously unselected package binutils-common:amd64.
(Reading database ... 160258 files and directories currently installed.)
Preparing to unpack .../00-binutils-common_2.38-3ubuntu1_amd64.deb ...ye@ye-System-Product-Name:~$ sudo apt install gcc
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  binutils binutils-common binutils-x86-64-linux-gnu gcc-11 libasan6 libatomic1 libbinutils libc-dev-bin libc-devtools
  libc6-dev libcc1-0 libcrypt-dev libctf-nobfd0 libctf0 libgcc-11-dev libitm1 liblsan0 libnsl-dev libquadmath0 libtirpc-dev
  libtsan0 libubsan1 linux-libc-dev manpages-dev rpcsvc-proto
Suggested packages:
  binutils-doc gcc-multilib make autoconf automake libtool flex bison gcc-doc gcc-11-multilib gcc-11-doc gcc-11-locales
  glibc-doc
The following NEW packages will be installed:
  binutils binutils-common binutils-x86-64-linux-gnu gcc gcc-11 libasan6 libatomic1 libbinutils libc-dev-bin libc-devtools
  libc6-dev libcc1-0 libcrypt-dev libctf-nobfd0 libctf0 libgcc-11-dev libitm1 liblsan0 libnsl-dev libquadmath0 libtirpc-dev
  libtsan0 libubsan1 linux-libc-dev manpages-dev rpcsvc-proto
0 upgraded, 26 newly installed, 0 to remove and 0 not upgraded.
Need to get 39.1 MB of archives.
After this operation, 131 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 binutils-common amd64 2.38-3ubuntu1 [221 kB]
Get:2 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libbinutils amd64 2.38-3ubuntu1 [662 kB]
Get:3 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libctf-nobfd0 amd64 2.38-3ubuntu1 [106 kB]
Get:4 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libctf0 amd64 2.38-3ubuntu1 [103 kB]
Get:5 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 binutils-x86-64-linux-gnu amd64 2.38-3ubuntu1 [2,328 kB]
Get:6 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 binutils amd64 2.38-3ubuntu1 [3,186 B]
Get:7 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libcc1-0 amd64 12-20220319-1ubuntu1 [47.2 kB]
Get:8 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libitm1 amd64 12-20220319-1ubuntu1 [30.2 kB]
Get:9 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libatomic1 amd64 12-20220319-1ubuntu1 [10.4 kB]
Get:10 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libasan6 amd64 11.2.0-19ubuntu1 [2,283 kB]
Get:11 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 liblsan0 amd64 12-20220319-1ubuntu1 [1,069 kB]
Get:12 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libtsan0 amd64 11.2.0-19ubuntu1 [2,261 kB]
Get:13 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libubsan1 amd64 12-20220319-1ubuntu1 [976 kB]
Get:14 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libquadmath0 amd64 12-20220319-1ubuntu1 [154 kB]
Get:15 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libgcc-11-dev amd64 11.2.0-19ubuntu1 [2,526 kB]
Get:16 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 gcc-11 amd64 11.2.0-19ubuntu1 [20.1 MB]
Get:17 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 gcc amd64 4:11.2.0-1ubuntu1 [5,112 B]
Get:18 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libc-dev-bin amd64 2.35-0ubuntu3 [20.3 kB]
Get:19 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libc-devtools amd64 2.35-0ubuntu3 [28.9 kB]
Get:20 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 linux-libc-dev amd64 5.15.0-25.25 [1,305 kB]
Get:21 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libcrypt-dev amd64 1:4.4.27-1 [112 kB]
Get:22 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 rpcsvc-proto amd64 1.4.2-0ubuntu6 [68.5 kB]
Get:23 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libtirpc-dev amd64 1.3.2-2build1 [192 kB]
Get:24 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libnsl-dev amd64 1.3.0-2build2 [71.3 kB]
Get:25 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libc6-dev amd64 2.35-0ubuntu3 [2,099 kB]
Get:26 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 manpages-dev all 5.10-1ubuntu1 [2,309 kB]
Fetched 39.1 MB in 2s (20.6 MB/s)        
Selecting previously unselected package binutils-common:amd64.
(Reading database ... 160258 files and directories currently installed.)
Preparing to unpack .../00-binutils-common_2.38-3ubuntu1_amd64.deb ...
Unpacking binutils-common:amd64 (2.38-3ubuntu1) ...
Selecting previously unselected package libbinutils:amd64.
Preparing to unpack .../01-libbinutils_2.38-3ubuntu1_amd64.deb ...
Unpacking libbinutils:amd64 (2.38-3ubuntu1) ...
Selecting previously unselected package libctf-nobfd0:amd64.
Preparing to unpack .../02-libctf-nobfd0_2.38-3ubuntu1_amd64.deb ...
Unpacking libctf-nobfd0:amd64 (2.38-3ubuntu1) ...
Selecting previously unselected package libctf0:amd64.
Preparing to unpack .../03-libctf0_2.38-3ubuntu1_amd64.deb ...
Unpacking libctf0:amd64 (2.38-3ubuntu1) ...
Selecting previously unselected package binutils-x86-64-linux-gnu.
Preparing to unpack .../04-binutils-x86-64-linux-gnu_2.38-3ubuntu1_amd64.deb ...
Unpacking binutils-x86-64-linux-gnu (2.38-3ubuntu1) ...
Selecting previously unselected package binutils.
Preparing to unpack .../05-binutils_2.38-3ubuntu1_amd64.deb ...
Unpacking binutils (2.38-3ubuntu1) ...
Selecting previously unselected package libcc1-0:amd64.
Preparing to unpack .../06-libcc1-0_12-20220319-1ubuntu1_amd64.deb ...
Unpacking libcc1-0:amd64 (12-20220319-1ubuntu1) ...
Selecting previously unselected package libitm1:amd64.
Preparing to unpack .../07-libitm1_12-20220319-1ubuntu1_amd64.deb ...
Unpacking libitm1:amd64 (12-20220319-1ubuntu1) ...
Selecting previously unselected package libatomic1:amd64.
Preparing to unpack .../08-libatomic1_12-20220319-1ubuntu1_amd64.deb ...
Unpacking libatomic1:amd64 (12-20220319-1ubuntu1) ...
Selecting previously unselected package libasan6:amd64.
Preparing to unpack .../09-libasan6_11.2.0-19ubuntu1_amd64.deb ...
Unpacking libasan6:amd64 (11.2.0-19ubuntu1) ...
Selecting previously unselected package liblsan0:amd64.
Preparing to unpack .../10-liblsan0_12-20220319-1ubuntu1_amd64.deb ...
Unpacking liblsan0:amd64 (12-20220319-1ubuntu1) ...
Selecting previously unselected package libtsan0:amd64.
Preparing to unpack .../11-libtsan0_11.2.0-19ubuntu1_amd64.deb ...
Unpacking libtsan0:amd64 (11.2.0-19ubuntu1) ...
Selecting previously unselected package libubsan1:amd64.
Preparing to unpack .../12-libubsan1_12-20220319-1ubuntu1_amd64.deb ...
Unpacking libubsan1:amd64 (12-20220319-1ubuntu1) ...
Selecting previously unselected package libquadmath0:amd64.
Preparing to unpack .../13-libquadmath0_12-20220319-1ubuntu1_amd64.deb ...
Unpacking libquadmath0:amd64 (12-20220319-1ubuntu1) ...
Selecting previously unselected package libgcc-11-dev:amd64.
Preparing to unpack .../14-libgcc-11-dev_11.2.0-19ubuntu1_amd64.deb ...
Unpacking libgcc-11-dev:amd64 (11.2.0-19ubuntu1) ...
Selecting previously unselected package gcc-11.
Preparing to unpack .../15-gcc-11_11.2.0-19ubuntu1_amd64.deb ...
Unpacking gcc-11 (11.2.0-19ubuntu1) ...
Selecting previously unselected package gcc.
Preparing to unpack .../16-gcc_4%3a11.2.0-1ubuntu1_amd64.deb ...
Unpacking gcc (4:11.2.0-1ubuntu1) ...
Selecting previously unselected package libc-dev-bin.
Preparing to unpack .../17-libc-dev-bin_2.35-0ubuntu3_amd64.deb ...
Unpacking libc-dev-bin (2.35-0ubuntu3) ...
Selecting previously unselected package libc-devtools.
Preparing to unpack .../18-libc-devtools_2.35-0ubuntu3_amd64.deb ...
Unpacking libc-devtools (2.35-0ubuntu3) ...
Selecting previously unselected package linux-libc-dev:amd64.
Preparing to unpack .../19-linux-libc-dev_5.15.0-25.25_amd64.deb ...
Unpacking linux-libc-dev:amd64 (5.15.0-25.25) ...
Selecting previously unselected package libcrypt-dev:amd64.
Preparing to unpack .../20-libcrypt-dev_1%3a4.4.27-1_amd64.deb ...
Unpacking libcrypt-dev:amd64 (1:4.4.27-1) ...
Selecting previously unselected package rpcsvc-proto.
Preparing to unpack .../21-rpcsvc-proto_1.4.2-0ubuntu6_amd64.deb ...
Unpacking rpcsvc-proto (1.4.2-0ubuntu6) ...
Selecting previously unselected package libtirpc-dev:amd64.
Preparing to unpack .../22-libtirpc-dev_1.3.2-2build1_amd64.deb ...
Unpacking libtirpc-dev:amd64 (1.3.2-2build1) ...
Selecting previously unselected package libnsl-dev:amd64.
Preparing to unpack .../23-libnsl-dev_1.3.0-2build2_amd64.deb ...
Unpacking libnsl-dev:amd64 (1.3.0-2build2) ...
Selecting previously unselected package libc6-dev:amd64.
Preparing to unpack .../24-libc6-dev_2.35-0ubuntu3_amd64.deb ...
Unpacking libc6-dev:amd64 (2.35-0ubuntu3) ...
Selecting previously unselected package manpages-dev.
Preparing to unpack .../25-manpages-dev_5.10-1ubuntu1_all.deb ...
Unpacking manpages-dev (5.10-1ubuntu1) ...
Setting up manpages-dev (5.10-1ubuntu1) ...
Setting up binutils-common:amd64 (2.38-3ubuntu1) ...
Setting up linux-libc-dev:amd64 (5.15.0-25.25) ...
Setting up libctf-nobfd0:amd64 (2.38-3ubuntu1) ...
Setting up libasan6:amd64 (11.2.0-19ubuntu1) ...
Setting up libtirpc-dev:amd64 (1.3.2-2build1) ...
Setting up rpcsvc-proto (1.4.2-0ubuntu6) ...
Setting up libquadmath0:amd64 (12-20220319-1ubuntu1) ...
Setting up libatomic1:amd64 (12-20220319-1ubuntu1) ...
Setting up libubsan1:amd64 (12-20220319-1ubuntu1) ...
Setting up libnsl-dev:amd64 (1.3.0-2build2) ...
Setting up libcrypt-dev:amd64 (1:4.4.27-1) ...
Setting up libbinutils:amd64 (2.38-3ubuntu1) ...
Setting up libc-dev-bin (2.35-0ubuntu3) ...
Setting up libcc1-0:amd64 (12-20220319-1ubuntu1) ...
Setting up liblsan0:amd64 (12-20220319-1ubuntu1) ...
Setting up libitm1:amd64 (12-20220319-1ubuntu1) ...
Setting up libc-devtools (2.35-0ubuntu3) ...
Setting up libtsan0:amd64 (11.2.0-19ubuntu1) ...
Setting up libctf0:amd64 (2.38-3ubuntu1) ...
Setting up libgcc-11-dev:amd64 (11.2.0-19ubuntu1) ...
Setting up libc6-dev:amd64 (2.35-0ubuntu3) ...
Setting up binutils-x86-64-linux-gnu (2.38-3ubuntu1) ...
Setting up binutils (2.38-3ubuntu1) ...
Setting up gcc-11 (11.2.0-19ubuntu1) ...
Setting up gcc (4:11.2.0-1ubuntu1) ...
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for libc-bin (2.35-0ubuntu3) ...
ye@ye-System-Product-Name:~$ sudo apt install gcc

Unpacking binutils-common:amd64 (2.38-3ubuntu1) ...
Selecting previously unselected package libbinutils:amd64.
Preparing to unpack .../01-libbinutils_2.38-3ubuntu1_amd64.deb ...
Unpacking libbinutils:amd64 (2.38-3ubuntu1) ...
Selecting previously unselected package libctf-nobfd0:amd64.
Preparing to unpack .../02-libctf-nobfd0_2.38-3ubuntu1_amd64.deb ...
Unpacking libctf-nobfd0:amd64 (2.38-3ubuntu1) ...
Selecting previously unselected package libctf0:amd64.
Preparing to unpack .../03-libctf0_2.38-3ubuntu1_amd64.deb ...
Unpacking libctf0:amd64 (2.38-3ubuntu1) ...
Selecting previously unselected package binutils-x86-64-linux-gnu.
Preparing to unpack .../04-binutils-x86-64-linux-gnu_2.38-3ubuntu1_amd64.deb ...
Unpacking binutils-x86-64-linux-gnu (2.38-3ubuntu1) ...
Selecting previously unselected package binutils.
Preparing to unpack .../05-binutils_2.38-3ubuntu1_amd64.deb ...
Unpacking binutils (2.38-3ubuntu1) ...
Selecting previously unselected package libcc1-0:amd64.
Preparing to unpack .../06-libcc1-0_12-20220319-1ubuntu1_amd64.deb ...
Unpacking libcc1-0:amd64 (12-20220319-1ubuntu1) ...
Selecting previously unselected package libitm1:amd64.
Preparing to unpack .../07-libitm1_12-20220319-1ubuntu1_amd64.deb ...
Unpacking libitm1:amd64 (12-20220319-1ubuntu1) ...
Selecting previously unselected package libatomic1:amd64.
Preparing to unpack .../08-libatomic1_12-20220319-1ubuntu1_amd64.deb ...
Unpacking libatomic1:amd64 (12-20220319-1ubuntu1) ...
Selecting previously unselected package libasan6:amd64.
Preparing to unpack .../09-libasan6_11.2.0-19ubuntu1_amd64.deb ...
Unpacking libasan6:amd64 (11.2.0-19ubuntu1) ...
Selecting previously unselected package liblsan0:amd64.
Preparing to unpack .../10-liblsan0_12-20220319-1ubuntu1_amd64.deb ...
Unpacking liblsan0:amd64 (12-20220319-1ubuntu1) ...
Selecting previously unselected package libtsan0:amd64.
Preparing to unpack .../11-libtsan0_11.2.0-19ubuntu1_amd64.deb ...
Unpacking libtsan0:amd64 (11.2.0-19ubuntu1) ...
Selecting previously unselected package libubsan1:amd64.
Preparing to unpack .../12-libubsan1_12-20220319-1ubuntu1_amd64.deb ...
Unpacking libubsan1:amd64 (12-20220319-1ubuntu1) ...
Selecting previously unselected package libquadmath0:amd64.
Preparing to unpack .../13-libquadmath0_12-20220319-1ubuntu1_amd64.deb ...
Unpacking libquadmath0:amd64 (12-20220319-1ubuntu1) ...
Selecting previously unselected package libgcc-11-dev:amd64.
Preparing to unpack .../14-libgcc-11-dev_11.2.0-19ubuntu1_amd64.deb ...
Unpacking libgcc-11-dev:amd64 (11.2.0-19ubuntu1) ...
Selecting previously unselected package gcc-11.
Preparing to unpack .../15-gcc-11_11.2.0-19ubuntu1_amd64.deb ...
Unpacking gcc-11 (11.2.0-19ubuntu1) ...
Selecting previously unselected package gcc.
Preparing to unpack .../16-gcc_4%3a11.2.0-1ubuntu1_amd64.deb ...
Unpacking gcc (4:11.2.0-1ubuntu1) ...
Selecting previously unselected package libc-dev-bin.
Preparing to unpack .../17-libc-dev-bin_2.35-0ubuntu3_amd64.deb ...
Unpacking libc-dev-bin (2.35-0ubuntu3) ...
Selecting previously unselected package libc-devtools.
Preparing to unpack .../18-libc-devtools_2.35-0ubuntu3_amd64.deb ...
Unpacking libc-devtools (2.35-0ubuntu3) ...
Selecting previously unselected package linux-libc-dev:amd64.
Preparing to unpack .../19-linux-libc-dev_5.15.0-25.25_amd64.deb ...
Unpacking linux-libc-dev:amd64 (5.15.0-25.25) ...
Selecting previously unselected package libcrypt-dev:amd64.
Preparing to unpack .../20-libcrypt-dev_1%3a4.4.27-1_amd64.deb ...
Unpacking libcrypt-dev:amd64 (1:4.4.27-1) ...
Selecting previously unselected package rpcsvc-proto.
Preparing to unpack .../21-rpcsvc-proto_1.4.2-0ubuntu6_amd64.deb ...
Unpacking rpcsvc-proto (1.4.2-0ubuntu6) ...
Selecting previously unselected package libtirpc-dev:amd64.
Preparing to unpack .../22-libtirpc-dev_1.3.2-2build1_amd64.deb ...
Unpacking libtirpc-dev:amd64 (1.3.2-2build1) ...
Selecting previously unselected package libnsl-dev:amd64.
Preparing to unpack .../23-libnsl-dev_1.3.0-2build2_amd64.deb ...
Unpacking libnsl-dev:amd64 (1.3.0-2build2) ...
Selecting previously unselected package libc6-dev:amd64.
Preparing to unpack .../24-libc6-dev_2.35-0ubuntu3_amd64.deb ...
Unpacking libc6-dev:amd64 (2.35-0ubuntu3) ...
Selecting previously unselected package manpages-dev.
Preparing to unpack .../25-manpages-dev_5.10-1ubuntu1_all.deb ...
Unpacking manpages-dev (5.10-1ubuntu1) ...
Setting up manpages-dev (5.10-1ubuntu1) ...
Setting up binutils-common:amd64 (2.38-3ubuntu1) ...
Setting up linux-libc-dev:amd64 (5.15.0-25.25) ...
Setting up libctf-nobfd0:amd64 (2.38-3ubuntu1) ...
Setting up libasan6:amd64 (11.2.0-19ubuntu1) ...
Setting up libtirpc-dev:amd64 (1.3.2-2build1) ...
Setting up rpcsvc-proto (1.4.2-0ubuntu6) ...
Setting up libquadmath0:amd64 (12-20220319-1ubuntu1) ...
Setting up libatomic1:amd64 (12-20220319-1ubuntu1) ...
Setting up libubsan1:amd64 (12-20220319-1ubuntu1) ...
Setting up libnsl-dev:amd64 (1.3.0-2build2) ...
Setting up libcrypt-dev:amd64 (1:4.4.27-1) ...
Setting up libbinutils:amd64 (2.38-3ubuntu1) ...
Setting up libc-dev-bin (2.35-0ubuntu3) ...
Setting up libcc1-0:amd64 (12-20220319-1ubuntu1) ...
Setting up liblsan0:amd64 (12-20220319-1ubuntu1) ...
Setting up libitm1:amd64 (12-20220319-1ubuntu1) ...
Setting up libc-devtools (2.35-0ubuntu3) ...
Setting up libtsan0:amd64 (11.2.0-19ubuntu1) ...
Setting up libctf0:amd64 (2.38-3ubuntu1) ...
Setting up libgcc-11-dev:amd64 (11.2.0-19ubuntu1) ...
Setting up libc6-dev:amd64 (2.35-0ubuntu3) ...
Setting up binutils-x86-64-linux-gnu (2.38-3ubuntu1) ...
Setting up binutils (2.38-3ubuntu1) ...
Setting up gcc-11 (11.2.0-19ubuntu1) ...
Setting up gcc (4:11.2.0-1ubuntu1) ...
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for libc-bin (2.35-0ubuntu3) ...
ye@ye-System-Product-Name:~$ sudo apt install gcc

Preparing to unpack .../12-libubsan1_12-20220319-1ubuntu1_amd64.deb ...
Unpacking libubsan1:amd64 (12-20220319-1ubuntu1) ...
Selecting previously unselected package libquadmath0:amd64.
Preparing to unpack .../13-libquadmath0_12-20220319-1ubuntu1_amd64.deb ...
Unpacking libquadmath0:amd64 (12-20220319-1ubuntu1) ...
Selecting previously unselected package libgcc-11-dev:amd64.
Preparing to unpack .../14-libgcc-11-dev_11.2.0-19ubuntu1_amd64.deb ...
Unpacking libgcc-11-dev:amd64 (11.2.0-19ubuntu1) ...
Selecting previously unselected package gcc-11.
Preparing to unpack .../15-gcc-11_11.2.0-19ubuntu1_amd64.deb ...
Unpacking gcc-11 (11.2.0-19ubuntu1) ...
Selecting previously unselected package gcc.
Preparing to unpack .../16-gcc_4%3a11.2.0-1ubuntu1_amd64.deb ...
Unpacking gcc (4:11.2.0-1ubuntu1) ...
Selecting previously unselected package libc-dev-bin.
Preparing to unpack .../17-libc-dev-bin_2.35-0ubuntu3_amd64.deb ...
Unpacking libc-dev-bin (2.35-0ubuntu3) ...
Selecting previously unselected package libc-devtools.
Preparing to unpack .../18-libc-devtools_2.35-0ubuntu3_amd64.deb ...
Unpacking libc-devtools (2.35-0ubuntu3) ...
Selecting previously unselected package linux-libc-dev:amd64.
Preparing to unpack .../19-linux-libc-dev_5.15.0-25.25_amd64.deb ...
Unpacking linux-libc-dev:amd64 (5.15.0-25.25) ...
Selecting previously unselected package libcrypt-dev:amd64.
Preparing to unpack .../20-libcrypt-dev_1%3a4.4.27-1_amd64.deb ...
Unpacking libcrypt-dev:amd64 (1:4.4.27-1) ...
Selecting previously unselected package rpcsvc-proto.
Preparing to unpack .../21-rpcsvc-proto_1.4.2-0ubuntu6_amd64.deb ...
Unpacking rpcsvc-proto (1.4.2-0ubuntu6) ...
Selecting previously unselected package libtirpc-dev:amd64.
Preparing to unpack .../22-libtirpc-dev_1.3.2-2build1_amd64.deb ...
Unpacking libtirpc-dev:amd64 (1.3.2-2build1) ...
Selecting previously unselected package libnsl-dev:amd64.
Preparing to unpack .../23-libnsl-dev_1.3.0-2build2_amd64.deb ...
Unpacking libnsl-dev:amd64 (1.3.0-2build2) ...
Selecting previously unselected package libc6-dev:amd64.
Preparing to unpack .../24-libc6-dev_2.35-0ubuntu3_amd64.deb ...
Unpacking libc6-dev:amd64 (2.35-0ubuntu3) ...
Selecting previously unselected package manpages-dev.
Preparing to unpack .../25-manpages-dev_5.10-1ubuntu1_all.deb ...
Unpacking manpages-dev (5.10-1ubuntu1) ...
Setting up manpages-dev (5.10-1ubuntu1) ...
Setting up binutils-common:amd64 (2.38-3ubuntu1) ...
Setting up linux-libc-dev:amd64 (5.15.0-25.25) ...
Setting up libctf-nobfd0:amd64 (2.38-3ubuntu1) ...
Setting up libasan6:amd64 (11.2.0-19ubuntu1) ...
Setting up libtirpc-dev:amd64 (1.3.2-2build1) ...
Setting up rpcsvc-proto (1.4.2-0ubuntu6) ...
Setting up libquadmath0:amd64 (12-20220319-1ubuntu1) ...
Setting up libatomic1:amd64 (12-20220319-1ubuntu1) ...
Setting up libubsan1:amd64 (12-20220319-1ubuntu1) ...
Setting up libnsl-dev:amd64 (1.3.0-2build2) ...
Setting up libcrypt-dev:amd64 (1:4.4.27-1) ...
Setting up libbinutils:amd64 (2.38-3ubuntu1) ...
Setting up libc-dev-bin (2.35-0ubuntu3) ...
Setting up libcc1-0:amd64 (12-20220319-1ubuntu1) ...
Setting up liblsan0:amd64 (12-20220319-1ubuntu1) ...
Setting up libitm1:amd64 (12-20220319-1ubuntu1) ...
Setting up libc-devtools (2.35-0ubuntu3) ...
Setting up libtsan0:amd64 (11.2.0-19ubuntu1) ...
Setting up libctf0:amd64 (2.38-3ubuntu1) ...
Setting up libgcc-11-dev:amd64 (11.2.0-19ubuntu1) ...
Setting up libc6-dev:amd64 (2.35-0ubuntu3) ...
Setting up binutils-x86-64-linux-gnu (2.38-3ubuntu1) ...
Setting up binutils (2.38-3ubuntu1) ...
Setting up gcc-11 (11.2.0-19ubuntu1) ...
Setting up gcc (4:11.2.0-1ubuntu1) ...
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for libc-bin (2.35-0ubuntu3) ...
ye@ye-System-Product-Name:~$ 
```

## Check Kernel Headers and Development Packages

```
ye@ye-System-Product-Name:~$ uname -r
5.15.0-25-generic
ye@ye-System-Product-Name:~$
```

```
ye@ye-System-Product-Name:~$ sudo apt-get install linux-headers-$(uname -r)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
linux-headers-5.15.0-25-generic is already the newest version (5.15.0-25.25).
linux-headers-5.15.0-25-generic set to manually installed.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
ye@ye-System-Product-Name:~$
```

##  Update apt-get

```
ye@ye-System-Product-Name:~$ sudo apt-get update
Hit:1 http://th.archive.ubuntu.com/ubuntu jammy InRelease
Hit:2 http://th.archive.ubuntu.com/ubuntu jammy-updates InRelease
Hit:3 http://th.archive.ubuntu.com/ubuntu jammy-backports InRelease    
Hit:4 https://dl.google.com/linux/chrome/deb stable InRelease                          
Hit:5 https://packages.microsoft.com/repos/ms-teams stable InRelease
Hit:6 http://security.ubuntu.com/ubuntu jammy-security InRelease
Reading package lists... Done
ye@ye-System-Product-Name:~$
```

## Download Cuda

Refer following link:
https://developer.nvidia.com/cuda-downloads  

```
ye@ye-System-Product-Name:~$ wget https://developer.download.nvidia.com/compute/cuda/11.6.2/local_installers/cuda_11.6.2_510.47.03_linux.run
--2022-04-25 12:24:40--  https://developer.download.nvidia.com/compute/cuda/11.6.2/local_installers/cuda_11.6.2_510.47.03_linux.run
Resolving developer.download.nvidia.com (developer.download.nvidia.com)... 152.199.39.144
Connecting to developer.download.nvidia.com (developer.download.nvidia.com)|152.199.39.144|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3462542823 (3.2G) [application/octet-stream]
Saving to: ‘cuda_11.6.2_510.47.03_linux.run’

cuda_11.6.2_510.47.03_linux.run 100%[=====================================================>]   3.22G  18.0MB/s    in 2m 5s   

2022-04-25 12:26:46 (26.4 MB/s) - ‘cuda_11.6.2_510.47.03_linux.run’ saved [3462542823/3462542823]

ye@ye-System-Product-Name:~$
```

အောက်ပါ command ကိုပေးလိုက်ရင်...  

```
sudo sh cuda_11.6.2_510.47.03_linux.run
```

လိုင်စင်နဲ့ ပတ်သက်ပြီး အောက်ပါအတိုင်း confirm လုပ်ပေးရပါလိမ့်မယ်။  

add image here ...  

accept ဆိုပြီး ရိုက်ထည့်ပေးပါ။  

menu မှာ ရွေးစရာရှိတာကို ရွေးပေးပါ။  

add picture  

install ကို ရွေးလိုက်တဲ့အခါမှာ အောက်ပါအတိုင်း installation fail ဆိုတဲ့ error တက်တယ်...  

```
ye@ye-System-Product-Name:~$ sudo sh cuda_11.6.2_510.47.03_linux.run
 Installation failed. See log at /var/log/cuda-installer.log for details.
ye@ye-System-Product-Name:~$
```

cuda installation log ဖိုင်ကို ကြည့်တော့ အောက်ပါအတိုင်း တွေ့ရ ...  

```
[INFO]: Driver not installed.
[INFO]: Checking compiler version...
[INFO]: gcc location: /usr/bin/gcc

[INFO]: gcc version: gcc version 11.2.0 (Ubuntu 11.2.0-19ubuntu1) 

[INFO]: Initializing menu
[INFO]: Setup complete
[INFO]: Components to install: 
[INFO]: Driver
[INFO]: 510.47.03
[INFO]: Executing NVIDIA-Linux-x86_64-510.47.03.run --ui=none --no-questions --accept-license --disable-nouveau --no-cc-version-check --install-libglvnd  2>&1
[INFO]: Finished with code: 256
[ERROR]: Install of driver component failed.
[ERROR]: Install of 510.47.03 failed, quitting
```

driver installation log ကို ကြည့်ကြည့်တော့ အောက်ပါအတိုင်း တွေ့ရ ...  
ye@ye-System-Product-Name:~$ gedit /var/log/nvidia-installer.log  

```
nvidia-installer log file '/var/log/nvidia-installer.log'
creation time: Mon Apr 25 12:33:00 2022
installer version: 510.47.03

PATH: /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin

nvidia-installer command line:
    ./nvidia-installer
    --ui=none
    --no-questions
    --accept-license
    --disable-nouveau
    --no-cc-version-check
    --install-libglvnd

Using built-in stream user interface
-> Detected 12 CPUs online; setting concurrency level to 12.
-> The file '/tmp/.X0-lock' exists and appears to contain the process ID '2027' of a running X server.
ERROR: You appear to be running an X server; please exit X before installing.  For further details, please see the section INSTALLING THE NVIDIA DRIVER in the README available on the Linux driver download page at www.nvidia.com.
ERROR: Installation has failed.  Please see the file '/var/log/nvidia-installer.log' for details.  You may find suggestions on fixing installation problems in the README available on the Linux driver download page at www.nvidia.com.
```

X server ကို stop လုပ်ဖို့လိုအပ်တယ် ...  

```
ye@ye-System-Product-Name:~$ sudo service lightdm stop
[sudo] password for ye: 
Failed to stop lightdm.service: Unit lightdm.service not loaded.
ye@ye-System-Product-Name:~$
```

lightdm က load မလုပ်ထားဘူးလို့ ပြောတယ်။ အဲဒါကြောင့် sudo service ကိုရိုက်ပြီး TAB key နှိပ်ပြီး service list ကို ထုတ်ကြည့်တယ်။  

add pic  

gdm ကိုတွေ့လို့ gdm service ကို stop လုပ်ကြည့်ခဲ့...  

sudo service gdm stop

အထက်ပါ command ကို ပေးလိုက်ရင် GUI အကုန်က သုံးမရတော့ဘူး ဖြစ်သွားလိမ့်မယ်။  
prompt ကနေပဲ Alt+F2 ကို နှိပ်ပြီးတော့ login ပြန်ဝင်ပါ။   
ပြီးတော့မှ cuda ကို installation ပြန်လုပ်ကြည့်ပါ။  sudo sh cuda_11.6.2_510.47.03_linux.run

```
sudo sh cuda_11.6.2_510.47.03_linux.run
```

လက်ရှိစက်မှာက ထပ် error ပေးတယ်။ driver log ဖိုင်ကို ဝင်ကြည့်တော့ အောက်ပါအတိုင်း တွေ့ရတယ်။  

```
ye@ye-System-Product-Name:~$ cat /var/log/nvidia-installer.log 
nvidia-installer log file '/var/log/nvidia-installer.log'
creation time: Mon Apr 25 14:16:03 2022
installer version: 510.47.03

PATH: /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin

nvidia-installer command line:
    ./nvidia-installer
    --ui=none
    --no-questions
    --accept-license
    --disable-nouveau
    --no-cc-version-check
    --install-libglvnd

Using built-in stream user interface
-> Detected 12 CPUs online; setting concurrency level to 12.
-> Installing NVIDIA driver version 510.47.03.
-> An alternate method of installing the NVIDIA driver was detected. (This is usually a package provided by your distributor.) A driver installed via that method may integrate better with your system than a driver installed by nvidia-installer.

Please review the message provided by the maintainer of this alternate installation method and decide how to proceed:

The NVIDIA driver provided by Ubuntu can be installed by launching the "Software & Updates" application, and by selecting the NVIDIA driver from the "Additional Drivers" tab.


(Answer: Continue installation)
ERROR: The Nouveau kernel driver is currently in use by your system.  This driver is incompatible with the NVIDIA driver, and must be disabled before proceeding.  Please consult the NVIDIA driver README and your Linux distribution's documentation for details on how to correctly disable the Nouveau kernel driver.
-> For some distributions, Nouveau can be disabled by adding a file in the modprobe configuration directory.  Would you like nvidia-installer to attempt to create this modprobe file for you? (Answer: Yes)
-> One or more modprobe configuration files to disable Nouveau have been written.  For some distributions, this may be sufficient to disable Nouveau; other distributions may require modification of the initial ramdisk.  Please reboot your system and attempt NVIDIA driver installation again.  Note if you later wish to re-enable Nouveau, you will need to delete these files: /usr/lib/modprobe.d/nvidia-installer-disable-nouveau.conf, /etc/modprobe.d/nvidia-installer-disable-nouveau.conf
ERROR: Installation has failed.  Please see the file '/var/log/nvidia-installer.log' for details.  You may find suggestions on fixing installation problems in the README available on the Linux driver download page at www.nvidia.com.
ye@ye-System-Product-Name:~$
```

အထက်ပါ error က menu option မှာ path ကို ပေးတဲ့နေရာကို ဝင်ချပြီး blank ပဲ ထားပြီးထွက်လိုက်လို့ ဖြစ်တာလို့ ယူဆ ...  
နောက်တစ်ခေါက် ထပ် install လုပ်တော့လည်း error ပေးနေလို့ log ဖိုင်ကို ဝင်ကြည့်တော့ အောက်ပါအတိုင်း တွေ့ရ...  

```
nvidia-installer log file '/var/log/nvidia-installer.log'
creation time: Mon Apr 25 14:31:09 2022
installer version: 510.47.03

PATH: /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin

nvidia-installer command line:
    ./nvidia-installer
    --ui=none
    --no-questions
    --accept-license
    --disable-nouveau
    --no-cc-version-check
    --install-libglvnd

Using built-in stream user interface
-> Detected 12 CPUs online; setting concurrency level to 12.
-> Installing NVIDIA driver version 510.47.03.
-> An alternate method of installing the NVIDIA driver was detected. (This is usually a package provided by your distributor.) A driver installed via that method may integrate better with your system than a driver installed by nvidia-installer.

Please review the message provided by the maintainer of this alternate installation method and decide how to proceed:

The NVIDIA driver provided by Ubuntu can be installed by launching the "Software & Updates" application, and by selecting the NVIDIA driver from the "Additional Drivers" tab.


(Answer: Continue installation)
WARNING: One or more modprobe configuration files to disable Nouveau are already present at: /usr/lib/modprobe.d/nvidia-installer-disable-nouveau.conf, /etc/modprobe.d/nvidia-installer-disable-nouveau.conf.  Please be sure you have rebooted your system since these files were written.  If you have rebooted, then Nouveau may be enabled for other reasons, such as being included in the system initial ramdisk or in your X configuration file.  Please consult the NVIDIA driver README and your Linux distribution's documentation for details on how to correctly disable the Nouveau kernel driver.
-> For some distributions, Nouveau can be disabled by adding a file in the modprobe configuration directory.  Would you like nvidia-installer to attempt to create this modprobe file for you? (Answer: Yes)
-> One or more modprobe configuration files to disable Nouveau have been written.  For some distributions, this may be sufficient to disable Nouveau; other distributions may require modification of the initial ramdisk.  Please reboot your system and attempt NVIDIA driver installation again.  Note if you later wish to re-enable Nouveau, you will need to delete these files: /usr/lib/modprobe.d/nvidia-installer-disable-nouveau.conf, /etc/modprobe.d/nvidia-installer-disable-nouveau.conf
ERROR: Unable to find the development tool `make` in your path; please make sure that you have the package 'make' installed.  If make is installed on your system, then please check that `make` is in your PATH.
ERROR: Installation has failed.  Please see the file '/var/log/nvidia-installer.log' for details.  You may find suggestions on fixing installation problems in the README available on the Linux driver download page at www.nvidia.com.

```

စက်က ubuntu OS ကို installation လုပ်ပြီး ဘာမှကို မထည့်ရသေးတာမို့ make လည်း မရှိသေးလို့ ပေးတဲ့ error လို့ ယူဆတယ်။ အဲဒါကြောင့် make ကို install လုပ်ခဲ့တယ်။  

```
Reading package lists...
Building dependency tree...
Reading state information...
Suggested packages:
  make-doc
The following NEW packages will be installed:
  make
0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
Need to get 180 kB of archives.
After this operation, 426 kB of additional disk space will be used.
Get:1 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 make amd64 4.3-4.1build1 [180 kB]
Fetched 180 kB in 0s (1,711 kB/s)
Selecting previously unselected package make.
(Reading database ... 164652 files and directories currently installed.)
Preparing to unpack .../make_4.3-4.1build1_amd64.deb ...
Unpacking make (4.3-4.1build1) ...
Setting up make (4.3-4.1build1) ...
Processing triggers for man-db (2.10.2-1) ...
ye@ye-System-Product-Name:~$
```

ထပ် install လုပ်ကြည့်တော့ ...  

```
sudo sh ./cuda_11.6.2_510.47.03_linux.run | tee cuda-installation.log3
```

အောက်ပါအတိုင်း အဆင်ပြေပြေနဲ့ installation လုပ်သွားတဲ့ ပုံတော့ရှိတယ်။  

```
┌──────────────────────────────────────────────────────────────────────────────┐
│ CUDA Installer                                                               │
│ - [X] Driver                                                                 │
│      [X] 510.47.03                                                           │
│ + [X] CUDA Toolkit 11.6                                                      │
│   [X] CUDA Samples 11.6                                                      │
│   [X] CUDA Demo Suite 11.6                                                   │
│   [X] CUDA Documentation 11.6                                                │
│   Options                                                                    │
│   Install                                                                    │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│ Up/Down: Move | Left/Right: Expand | 'Enter': Select | 'A': Advanced options │
└──────────────────────────────────────────────────────────────────────────────┘





===========
= Summary =
===========

Driver:   Installed
Toolkit:  Installed in /usr/local/cuda-11.6/

Please make sure that
 -   PATH includes /usr/local/cuda-11.6/bin
 -   LD_LIBRARY_PATH includes /usr/local/cuda-11.6/lib64, or, add /usr/local/cuda-11.6/lib64 to /etc/ld.so.conf and run ldconfig as root

To uninstall the CUDA Toolkit, run cuda-uninstaller in /usr/local/cuda-11.6/bin
To uninstall the NVIDIA Driver, run nvidia-uninstall
Logfile is /var/log/cuda-installer.log
ye@ye-System-Product-Name:~$
```

nvdia command ကို ခေါ်ကြည့်ခဲ့တော့ အလုပ်လုပ်တာကို တွေ့ရတယ်။  

```
ye@ye-System-Product-Name:~$ nvidia-smi
Mon Apr 25 14:52:07 2022       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 510.47.03    Driver Version: 510.47.03    CUDA Version: 11.6     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:01:00.0 Off |                  N/A |
|  0%   41C    P8     1W / 300W |      9MiB / 11264MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  NVIDIA GeForce ...  Off  | 00000000:05:00.0 Off |                  N/A |
|  0%   43C    P8    11W / 185W |      5MiB /  8192MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A      1812      G   /usr/lib/xorg/Xorg                  4MiB |
|    0   N/A  N/A      2027      G   ...ome-remote-desktop-daemon        2MiB |
|    1   N/A  N/A      1812      G   /usr/lib/xorg/Xorg                  4MiB |
+-----------------------------------------------------------------------------+
ye@ye-System-Product-Name:~$
```

## Testing GPU

link: [https://www.geeks3d.com/gputest/](https://www.geeks3d.com/gputest/)  

Download လုပ်ပြီး unzip လုပ်ခဲ့ ...  

```
ye@ye-System-Product-Name:~/tool$ mv ~/Downloads/GpuTest_Linux_x64_0.7.0.zip .
ye@ye-System-Product-Name:~/tool$ ls
GpuTest_Linux_x64_0.7.0.zip
ye@ye-System-Product-Name:~/tool$ unzip ./GpuTest_Linux_x64_0.7.0.zip 
Archive:  ./GpuTest_Linux_x64_0.7.0.zip
   creating: GpuTest_Linux_x64_0.7.0/
  inflating: GpuTest_Linux_x64_0.7.0/EULA.txt  
  inflating: GpuTest_Linux_x64_0.7.0/GpuTest  
  inflating: GpuTest_Linux_x64_0.7.0/README.txt  
  inflating: GpuTest_Linux_x64_0.7.0/_geeks3d_gputest_scores.csv  
   creating: GpuTest_Linux_x64_0.7.0/data/
  inflating: GpuTest_Linux_x64_0.7.0/data/.DS_Store  
  inflating: GpuTest_Linux_x64_0.7.0/data/_bg.jpg  
  inflating: GpuTest_Linux_x64_0.7.0/data/_fur.jpg  
  inflating: GpuTest_Linux_x64_0.7.0/data/apple_logo.jpg  
  inflating: GpuTest_Linux_x64_0.7.0/data/bg.jpg  
  inflating: GpuTest_Linux_x64_0.7.0/data/bg02.jpg  
  inflating: GpuTest_Linux_x64_0.7.0/data/bg02_.jpg  
  inflating: GpuTest_Linux_x64_0.7.0/data/bg08.jpg  
  inflating: GpuTest_Linux_x64_0.7.0/data/bg09.jpg  
  inflating: GpuTest_Linux_x64_0.7.0/data/fur.jpg  
  inflating: GpuTest_Linux_x64_0.7.0/data/linux_logo.jpg  
  inflating: GpuTest_Linux_x64_0.7.0/data/piano_texture.jpg  
  inflating: GpuTest_Linux_x64_0.7.0/data/piano_texture_01.jpg  
  inflating: GpuTest_Linux_x64_0.7.0/data/tess_bump.jpg  
  inflating: GpuTest_Linux_x64_0.7.0/data/tess_diffuse.jpg  
  inflating: GpuTest_Linux_x64_0.7.0/data/tess_normal.jpg  
  inflating: GpuTest_Linux_x64_0.7.0/data/windows_logo.jpg  
  inflating: GpuTest_Linux_x64_0.7.0/gputest_gui.py  
  inflating: GpuTest_Linux_x64_0.7.0/libgxl3d_r_linux.so  
  inflating: GpuTest_Linux_x64_0.7.0/plugin_gxl3d_gpu_monitor_gml_x64.so  
  inflating: GpuTest_Linux_x64_0.7.0/plugin_gxl3d_opencl_x64.so  
  inflating: GpuTest_Linux_x64_0.7.0/start_furmark_benchmark_fullscreen_1920x1080.sh  
 extracting: GpuTest_Linux_x64_0.7.0/start_furmark_windowed_1024x640.sh  
  inflating: GpuTest_Linux_x64_0.7.0/start_gimark_benchmark_fullscreen_1920x1080.sh  
 extracting: GpuTest_Linux_x64_0.7.0/start_gimark_windowed_1024x640.sh  
  inflating: GpuTest_Linux_x64_0.7.0/start_pixmark_piano_benchmark_fullscreen_1920x1080.sh  
  inflating: GpuTest_Linux_x64_0.7.0/start_pixmark_piano_windowed_1024x640.sh  
  inflating: GpuTest_Linux_x64_0.7.0/start_pixmark_volplosion_benchmark_fullscreen_1920x1080.sh  
  inflating: GpuTest_Linux_x64_0.7.0/start_pixmark_volplosion_windowed_1024x640.sh  
  inflating: GpuTest_Linux_x64_0.7.0/start_plot3d_benchmark_fullscreen_1920x1080.sh  
 extracting: GpuTest_Linux_x64_0.7.0/start_plot3d_windowed_1024x640.sh  
  inflating: GpuTest_Linux_x64_0.7.0/start_tessmark_benchmark_fullscreen_1920x1080.sh  
  inflating: GpuTest_Linux_x64_0.7.0/start_tessmark_windowed_1024x640.sh  
  inflating: GpuTest_Linux_x64_0.7.0/start_triangle_benchmark_fullscreen_1920x1080.sh  
 extracting: GpuTest_Linux_x64_0.7.0/start_triangle_windowed_1024x640.sh  
```
 
unzip လုပ်ထားတဲ့ folder အောက်ကို ဝင်ကြည့်ရင်...  
 
```
ye@ye-System-Product-Name:~/tool$ cd GpuTest_Linux_x64_0.7.0/
ye@ye-System-Product-Name:~/tool/GpuTest_Linux_x64_0.7.0$ ls
data                                             start_gimark_windowed_1024x640.sh
EULA.txt                                         start_pixmark_piano_benchmark_fullscreen_1920x1080.sh
_geeks3d_gputest_scores.csv                      start_pixmark_piano_windowed_1024x640.sh
GpuTest                                          start_pixmark_volplosion_benchmark_fullscreen_1920x1080.sh
gputest_gui.py                                   start_pixmark_volplosion_windowed_1024x640.sh
libgxl3d_r_linux.so                              start_plot3d_benchmark_fullscreen_1920x1080.sh
plugin_gxl3d_gpu_monitor_gml_x64.so              start_plot3d_windowed_1024x640.sh
plugin_gxl3d_opencl_x64.so                       start_tessmark_benchmark_fullscreen_1920x1080.sh
README.txt                                       start_tessmark_windowed_1024x640.sh
start_furmark_benchmark_fullscreen_1920x1080.sh  start_triangle_benchmark_fullscreen_1920x1080.sh
start_furmark_windowed_1024x640.sh               start_triangle_windowed_1024x640.sh
start_gimark_benchmark_fullscreen_1920x1080.sh
ye@ye-System-Product-Name:~/tool/GpuTest_Linux_x64_0.7.0$
```

testing1 ...  

```
ye@ye-System-Product-Name:~/tool/GpuTest_Linux_x64_0.7.0$ sh ./start_furmark_benchmark_fullscreen_1920x1080.sh
```


## Reference

- [https://forums.developer.nvidia.com/t/info-finished-with-code-256-error-install-of-driver-component-failed/107661](https://forums.developer.nvidia.com/t/info-finished-with-code-256-error-install-of-driver-component-failed/107661)  
- [https://unix.stackexchange.com/questions/25668/how-to-close-x-server-to-avoid-errors-while-updating-nvidia-driver](https://unix.stackexchange.com/questions/25668/how-to-close-x-server-to-avoid-errors-while-updating-nvidia-driver)  
- [https://geeks3d.com/furmark/downloads/](https://geeks3d.com/furmark/downloads/)  
- link: [https://www.geeks3d.com/gputest/](https://www.geeks3d.com/gputest/)  
(This is better, it includs several GPU testing tools.)  



