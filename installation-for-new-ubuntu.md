# Installation of Required Packages for a New Ubuntu OS

```
sudo apt-get update  
```

## git

```
ye@ye-System-Product-Name:~$ sudo apt-get install git
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  git-man liberror-perl
Suggested packages:
  git-daemon-run | git-daemon-sysvinit git-doc git-email git-gui gitk gitweb git-cvs git-mediawiki git-svn
The following NEW packages will be installed:
  git git-man liberror-perl
0 upgraded, 3 newly installed, 0 to remove and 21 not upgraded.
Need to get 4,108 kB of archives.
After this operation, 20.9 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 liberror-perl all 0.17029-1 [26.5 kB]
Get:2 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 git-man all 1:2.34.1-1ubuntu1.2 [952 kB]
Get:3 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 git amd64 1:2.34.1-1ubuntu1.2 [3,130 kB]
Fetched 4,108 kB in 0s (12.0 MB/s)
Selecting previously unselected package liberror-perl.
(Reading database ... 166874 files and directories currently installed.)
Preparing to unpack .../liberror-perl_0.17029-1_all.deb ...
Unpacking liberror-perl (0.17029-1) ...
Selecting previously unselected package git-man.
Preparing to unpack .../git-man_1%3a2.34.1-1ubuntu1.2_all.deb ...
Unpacking git-man (1:2.34.1-1ubuntu1.2) ...
Selecting previously unselected package git.
Preparing to unpack .../git_1%3a2.34.1-1ubuntu1.2_amd64.deb ...
Unpacking git (1:2.34.1-1ubuntu1.2) ...
Setting up liberror-perl (0.17029-1) ...
Setting up git-man (1:2.34.1-1ubuntu1.2) ...
Setting up git (1:2.34.1-1ubuntu1.2) ...
Processing triggers for man-db (2.10.2-1) ...
```

```
ye@ye-System-Product-Name:~$ git --version
git version 2.34.1
```

##  pycharm

အောက်ပါ command ကို သုံးပြီး installation လုပ်မယ်...  

```
sudo snap install pycharm-community --classic
```

```
ye@ye-System-Product-Name:~$ sudo snap install pycharm-community --classic
pycharm-community 2022.1 from jetbrains✓ installed
ye@ye-System-Product-Name:~$
```

1st time running pycharm ...  

```
ye@ye-System-Product-Name:~$ pycharm-community 
```

## 

## Reference

- https://blog.jetbrains.com/pycharm/2017/09/pycharm-community-edition-and-professional-edition-explained-licenses-and-more/

