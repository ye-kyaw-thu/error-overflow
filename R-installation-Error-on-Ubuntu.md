## R Installation Error on Ubuntu

I wanna draw error-bar graph with R. And thus, install R on my Ubuntu notebook and got error relating to "packages have unmet dependencies". This is the log file for clearing that error. You can skip directly to the Solution<a this id='solution'></a>.

y@CADT, Cambodia  
15 Aug 2022  

## Check the R

```
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ R --version

Command 'R' not found, but can be installed with:

sudo apt install r-base-core
```

## Install Dependencies

```
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ sudo apt install dirmngr gnupg apt-transport-https ca-certificates software-properties-common
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
ca-certificates is already the newest version (20211016~18.04.1).
ca-certificates set to manually installed.
dirmngr is already the newest version (2.2.4-1ubuntu1.6).
dirmngr set to manually installed.
gnupg is already the newest version (2.2.4-1ubuntu1.6).
gnupg set to manually installed.
The following packages were automatically installed and are no longer required:
  linux-hwe-5.4-headers-5.4.0-117 linux-hwe-5.4-headers-5.4.0-120 linux-hwe-5.4-headers-5.4.0-121
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  python3-software-properties software-properties-gtk
The following packages will be upgraded:
  apt-transport-https python3-software-properties software-properties-common software-properties-gtk
4 upgraded, 0 newly installed, 0 to remove and 135 not upgraded.
Need to get 103 kB of archives.
After this operation, 15.4 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://mm.archive.ubuntu.com/ubuntu bionic-updates/universe amd64 apt-transport-https all 1.6.14 [4,348 B]
Get:2 http://mm.archive.ubuntu.com/ubuntu bionic-updates/main amd64 software-properties-common all 0.96.24.32.18 [10.1 kB]
Get:3 http://mm.archive.ubuntu.com/ubuntu bionic-updates/main amd64 software-properties-gtk all 0.96.24.32.18 [64.9 kB]
Get:4 http://mm.archive.ubuntu.com/ubuntu bionic-updates/main amd64 python3-software-properties all 0.96.24.32.18 [23.8 kB]
Fetched 103 kB in 2s (43.5 kB/s)                       
(Reading database ... 470654 files and directories currently installed.)
Preparing to unpack .../apt-transport-https_1.6.14_all.deb ...
Unpacking apt-transport-https (1.6.14) over (1.6.12ubuntu0.2) ...
Preparing to unpack .../software-properties-common_0.96.24.32.18_all.deb ...
Unpacking software-properties-common (0.96.24.32.18) over (0.96.24.32.14) ...
Preparing to unpack .../software-properties-gtk_0.96.24.32.18_all.deb ...
Unpacking software-properties-gtk (0.96.24.32.18) over (0.96.24.32.14) ...
Preparing to unpack .../python3-software-properties_0.96.24.32.18_all.deb ...
Unpacking python3-software-properties (0.96.24.32.18) over (0.96.24.32.14) ...
Setting up apt-transport-https (1.6.14) ...
Setting up python3-software-properties (0.96.24.32.18) ...
Setting up software-properties-common (0.96.24.32.18) ...
Setting up software-properties-gtk (0.96.24.32.18) ...
Processing triggers for shared-mime-info (1.9-2) ...
Processing triggers for gnome-menus (3.13.3-11ubuntu1.1) ...
Processing triggers for dbus (1.12.2-1ubuntu1.3) ...
Processing triggers for hicolor-icon-theme (0.17-2) ...
Processing triggers for mime-support (3.60ubuntu1) ...
Processing triggers for desktop-file-utils (0.23-1ubuntu3.18.04.2) ...
Processing triggers for libglib2.0-0:amd64 (2.56.4-0ubuntu0.18.04.9) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$
```

## Add the CRAN Repository to Your System Sources' List

```
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
Executing: /tmp/apt-key-gpghome.lPYEQoCMAv/gpg.1.sh --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
gpg: key 51716619E084DAB9: public key "Michael Rutter <marutter@gmail.com>" imported
gpg: Total number processed: 1
gpg:               imported: 1
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$
```

```
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ sudo add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/'
Hit:1 http://packages.microsoft.com/repos/vscode stable InRelease
Get:2 http://dl.google.com/linux/chrome/deb stable InRelease [1,811 B]                                                       
Hit:3 https://packages.microsoft.com/repos/ms-teams stable InRelease                                                         
Get:4 https://dl.yarnpkg.com/debian stable InRelease [17.1 kB]                                                               
Hit:5 https://apt.repos.intel.com/mkl all InRelease                                                                          
Hit:6 http://mm.archive.ubuntu.com/ubuntu bionic InRelease                                                                   
Err:2 http://dl.google.com/linux/chrome/deb stable InRelease                                                                 
  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 4EB27DB2A3B88B8B
Hit:7 http://ppa.launchpad.net/malteworld/ppa/ubuntu bionic InRelease                                                        
Get:8 http://security.ubuntu.com/ubuntu bionic-security InRelease [88.7 kB]                                                  
Get:9 http://mm.archive.ubuntu.com/ubuntu bionic-updates InRelease [88.7 kB]                                                 
Err:4 https://dl.yarnpkg.com/debian stable InRelease                                                                         
  The following signatures were invalid: EXPKEYSIG 23E7166788B63E1E Yarn Packaging <yarn@dan.cx>
Hit:10 http://ppa.launchpad.net/peek-developers/stable/ubuntu bionic InRelease                                               
Err:11 https://dl.bintray.com/sbt/debian  InRelease                                                                          
  502  Bad Gateway [IP: 52.36.126.31 443]
Hit:12 http://ppa.launchpad.net/ubuntu-toolchain-r/test/ubuntu bionic InRelease                                              
Get:13 http://mm.archive.ubuntu.com/ubuntu bionic-backports InRelease [74.6 kB]                                              
Get:14 https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/ InRelease [3,622 B]                              
Get:15 http://security.ubuntu.com/ubuntu bionic-security/main amd64 DEP-11 Metadata [55.3 kB]                      
Get:16 http://mm.archive.ubuntu.com/ubuntu bionic-updates/main amd64 DEP-11 Metadata [297 kB]             
Get:17 http://security.ubuntu.com/ubuntu bionic-security/universe amd64 DEP-11 Metadata [61.1 kB]
Get:18 http://security.ubuntu.com/ubuntu bionic-security/multiverse amd64 DEP-11 Metadata [2,464 B]                          
Get:19 https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/ Packages [54.9 kB]                                        
Get:20 http://mm.archive.ubuntu.com/ubuntu bionic-updates/universe amd64 DEP-11 Metadata [302 kB]
Get:21 http://mm.archive.ubuntu.com/ubuntu bionic-updates/multiverse amd64 DEP-11 Metadata [2,468 B]
Get:22 http://mm.archive.ubuntu.com/ubuntu bionic-backports/universe amd64 DEP-11 Metadata [9,284 B]
Fetched 1,040 kB in 3s (331 kB/s)                                           
Reading package lists... Done
W: An error occurred during the signature verification. The repository is not updated and the previous index files will be used. GPG error: http://dl.google.com/linux/chrome/deb stable InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 4EB27DB2A3B88B8B
W: An error occurred during the signature verification. The repository is not updated and the previous index files will be used. GPG error: https://dl.yarnpkg.com/debian stable InRelease: The following signatures were invalid: EXPKEYSIG 23E7166788B63E1E Yarn Packaging <yarn@dan.cx>
W: Failed to fetch http://dl.google.com/linux/chrome/deb/dists/stable/InRelease  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 4EB27DB2A3B88B8B
W: Failed to fetch https://dl.bintray.com/sbt/debian/InRelease  502  Bad Gateway [IP: 52.36.126.31 443]
W: Failed to fetch https://dl.yarnpkg.com/debian/dists/stable/InRelease  The following signatures were invalid: EXPKEYSIG 23E7166788B63E1E Yarn Packaging <yarn@dan.cx>
W: Some index files failed to download. They have been ignored, or old ones used instead.
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ 
```

## Install R

```
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ sudo apt install r-base
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 r-base : Depends: r-base-core (>= 4.2.1-2.2004.0) but it is not going to be installed
          Depends: r-recommended (= 4.2.1-2.2004.0) but it is not going to be installed
          Recommends: r-base-html but it is not going to be installed
E: Unable to correct problems, you have held broken packages.
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ 
```

## Download the Key

Trying with Ubuntu 22.04 OS Installation ...  

```
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ wget -qO- https://cloud.r-project.org/bin/linux/ubuntu/marutter_pubkey.asc | sudo gpg --dearmor -o /usr/share/keyrings/r-project.gpg
gpg: WARNING: unsafe ownership on homedir '/home/ye/.gnupg'
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$
```

## Add the R-Source List

```
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ echo "deb [signed-by=/usr/share/keyrings/r-project.gpg] https://cloud.r-project.org/bin/linux/ubuntu jammy-cran40/" | sudo tee -a /etc/apt/sources.list.d/r-project.list
deb [signed-by=/usr/share/keyrings/r-project.gpg] https://cloud.r-project.org/bin/linux/ubuntu jammy-cran40/
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$
```

## Update the Package List

```
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ sudo apt update
Get:1 http://dl.google.com/linux/chrome/deb stable InRelease [1,811 B]
Hit:2 https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/ InRelease                                                   
Hit:3 http://packages.microsoft.com/repos/vscode stable InRelease                                                            
Get:4 https://dl.yarnpkg.com/debian stable InRelease [17.1 kB]                                                               
Get:5 https://cloud.r-project.org/bin/linux/ubuntu jammy-cran40/ InRelease [3,626 B]                                         
Hit:6 https://packages.microsoft.com/repos/ms-teams stable InRelease                                                         
Err:1 http://dl.google.com/linux/chrome/deb stable InRelease                                                                 
  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 4EB27DB2A3B88B8B
Hit:7 https://apt.repos.intel.com/mkl all InRelease                                                                          
Hit:8 http://ppa.launchpad.net/malteworld/ppa/ubuntu bionic InRelease                                                        
Hit:9 http://security.ubuntu.com/ubuntu bionic-security InRelease                                                            
Hit:10 http://mm.archive.ubuntu.com/ubuntu bionic InRelease                                                                  
Err:4 https://dl.yarnpkg.com/debian stable InRelease                                                                   
  The following signatures were invalid: EXPKEYSIG 23E7166788B63E1E Yarn Packaging <yarn@dan.cx>
Hit:11 http://ppa.launchpad.net/peek-developers/stable/ubuntu bionic InRelease                   
Get:12 https://cloud.r-project.org/bin/linux/ubuntu jammy-cran40/ Packages [16.7 kB]                                        
Err:13 https://dl.bintray.com/sbt/debian  InRelease                                                                          
  502  Bad Gateway [IP: 35.166.126.94 443]
Hit:14 http://mm.archive.ubuntu.com/ubuntu bionic-updates InRelease                                                         
Hit:15 http://ppa.launchpad.net/ubuntu-toolchain-r/test/ubuntu bionic InRelease                       
Hit:16 http://mm.archive.ubuntu.com/ubuntu bionic-backports InRelease    
Fetched 20.3 kB in 2s (8,504 B/s)                  
Reading package lists... Done
Building dependency tree       
Reading state information... Done
135 packages can be upgraded. Run 'apt list --upgradable' to see them.
W: An error occurred during the signature verification. The repository is not updated and the previous index files will be used. GPG error: http://dl.google.com/linux/chrome/deb stable InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 4EB27DB2A3B88B8B
W: An error occurred during the signature verification. The repository is not updated and the previous index files will be used. GPG error: https://dl.yarnpkg.com/debian stable InRelease: The following signatures were invalid: EXPKEYSIG 23E7166788B63E1E Yarn Packaging <yarn@dan.cx>
W: Failed to fetch http://dl.google.com/linux/chrome/deb/dists/stable/InRelease  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 4EB27DB2A3B88B8B
W: Failed to fetch https://dl.bintray.com/sbt/debian/InRelease  502  Bad Gateway [IP: 35.166.126.94 443]
W: Failed to fetch https://dl.yarnpkg.com/debian/dists/stable/InRelease  The following signatures were invalid: EXPKEYSIG 23E7166788B63E1E Yarn Packaging <yarn@dan.cx>
W: Some index files failed to download. They have been ignored, or old ones used instead.
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ 
```

## Install R

```
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ sudo apt install --no-install-recommends r-base
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 r-base : Depends: r-base-core (>= 4.2.1-2.2204.0) but it is not going to be installed
          Depends: r-recommended (= 4.2.1-2.2204.0) but it is not going to be installed
E: Unable to correct problems, you have held broken packages.
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$
```

## Check the APT sources.list.d Folder

```
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ cat /etc/apt/sources.list.d/*
### THIS FILE IS AUTOMATICALLY CONFIGURED ###
# You may comment out this entry, but any other modifications may be lost.
deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main
### THIS FILE IS AUTOMATICALLY CONFIGURED ###
# You may comment out this entry, but any other modifications may be lost.
deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main
deb https://apt.repos.intel.com/mkl all main
deb https://apt.repos.intel.com/mkl all main
deb http://ppa.launchpad.net/malteworld/ppa/ubuntu bionic main
# deb-src http://ppa.launchpad.net/malteworld/ppa/ubuntu bionic main
deb http://ppa.launchpad.net/malteworld/ppa/ubuntu bionic main
# deb-src http://ppa.launchpad.net/malteworld/ppa/ubuntu bionic main
deb http://ppa.launchpad.net/peek-developers/stable/ubuntu bionic main
# deb-src http://ppa.launchpad.net/peek-developers/stable/ubuntu bionic main
deb http://ppa.launchpad.net/peek-developers/stable/ubuntu bionic main
# deb-src http://ppa.launchpad.net/peek-developers/stable/ubuntu bionic main
deb [signed-by=/usr/share/keyrings/r-project.gpg] https://cloud.r-project.org/bin/linux/ubuntu jammy-cran40/
deb https://dl.bintray.com/sbt/debian /
deb https://dl.bintray.com/sbt/debian /
### THIS FILE IS AUTOMATICALLY CONFIGURED ###
# You may comment out this entry, but any other modifications may be lost.
deb [arch=amd64] https://packages.microsoft.com/repos/ms-teams stable main
### THIS FILE IS AUTOMATICALLY CONFIGURED ###
# You may comment out this entry, but any other modifications may be lost.
deb [arch=amd64] https://packages.microsoft.com/repos/ms-teams stable main
deb http://ppa.launchpad.net/ubuntu-toolchain-r/test/ubuntu bionic main
# deb-src http://ppa.launchpad.net/ubuntu-toolchain-r/test/ubuntu bionic main
deb http://ppa.launchpad.net/ubuntu-toolchain-r/test/ubuntu bionic main
# deb-src http://ppa.launchpad.net/ubuntu-toolchain-r/test/ubuntu bionic main
### THIS FILE IS AUTOMATICALLY CONFIGURED ###
# You may comment out this entry, but any other modifications may be lost.
deb [arch=amd64] http://packages.microsoft.com/repos/vscode stable main
### THIS FILE IS AUTOMATICALLY CONFIGURED ###
# You may comment out this entry, but any other modifications may be lost.
deb [arch=amd64] http://packages.microsoft.com/repos/vscode stable main
deb https://dl.yarnpkg.com/debian/ stable main
deb https://dl.yarnpkg.com/debian/ stable main
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ 
```

## Installation Again

```
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ sudo add-apt-repository ppa:marutter/rrutter
 Contains packages related to my use of R for research and teaching.  This PPA is also mirrored on the CRAN Ubuntu page.  Please note, R 3.3.0 and above are no longer supported for 12.04 (precise).
 More info: https://launchpad.net/~marutter/+archive/ubuntu/rrutter
Press [ENTER] to continue or Ctrl-c to cancel adding it.

Get:1 http://dl.google.com/linux/chrome/deb stable InRelease [1,811 B]
Hit:2 http://packages.microsoft.com/repos/vscode stable InRelease                                                            
Hit:3 https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/ InRelease                                                   
Get:4 https://dl.yarnpkg.com/debian stable InRelease [17.1 kB]                                                               
Hit:5 https://cloud.r-project.org/bin/linux/ubuntu jammy-cran40/ InRelease                                                   
Hit:6 https://packages.microsoft.com/repos/ms-teams stable InRelease                                                         
Err:1 http://dl.google.com/linux/chrome/deb stable InRelease                                                                 
  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 4EB27DB2A3B88B8B
Hit:7 https://apt.repos.intel.com/mkl all InRelease                                                                          
Hit:8 http://ppa.launchpad.net/malteworld/ppa/ubuntu bionic InRelease                                                        
Hit:9 http://security.ubuntu.com/ubuntu bionic-security InRelease                                                            
Hit:10 http://mm.archive.ubuntu.com/ubuntu bionic InRelease                                                                  
Err:4 https://dl.yarnpkg.com/debian stable InRelease                                                                         
  The following signatures were invalid: EXPKEYSIG 23E7166788B63E1E Yarn Packaging <yarn@dan.cx>
Get:11 http://ppa.launchpad.net/marutter/rrutter/ubuntu bionic InRelease [15.4 kB]                                    
Hit:12 http://mm.archive.ubuntu.com/ubuntu bionic-updates InRelease                                         
Err:13 https://dl.bintray.com/sbt/debian  InRelease                                                         
  502  Bad Gateway [IP: 52.36.126.31 443]
Hit:14 http://mm.archive.ubuntu.com/ubuntu bionic-backports InRelease                                       
Hit:15 http://ppa.launchpad.net/peek-developers/stable/ubuntu bionic InRelease  
Hit:16 http://ppa.launchpad.net/ubuntu-toolchain-r/test/ubuntu bionic InRelease 
Get:17 http://ppa.launchpad.net/marutter/rrutter/ubuntu bionic/main i386 Packages [996 B]
Get:18 http://ppa.launchpad.net/marutter/rrutter/ubuntu bionic/main amd64 Packages [984 B]
Get:19 http://ppa.launchpad.net/marutter/rrutter/ubuntu bionic/main Translation-en [928 B]
Fetched 18.3 kB in 3s (5,547 B/s)                    
Reading package lists... Done
W: An error occurred during the signature verification. The repository is not updated and the previous index files will be used. GPG error: http://dl.google.com/linux/chrome/deb stable InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 4EB27DB2A3B88B8B
W: An error occurred during the signature verification. The repository is not updated and the previous index files will be used. GPG error: https://dl.yarnpkg.com/debian stable InRelease: The following signatures were invalid: EXPKEYSIG 23E7166788B63E1E Yarn Packaging <yarn@dan.cx>
W: Failed to fetch http://dl.google.com/linux/chrome/deb/dists/stable/InRelease  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 4EB27DB2A3B88B8B
W: Failed to fetch https://dl.bintray.com/sbt/debian/InRelease  502  Bad Gateway [IP: 52.36.126.31 443]
W: Failed to fetch https://dl.yarnpkg.com/debian/dists/stable/InRelease  The following signatures were invalid: EXPKEYSIG 23E7166788B63E1E Yarn Packaging <yarn@dan.cx>
W: Some index files failed to download. They have been ignored, or old ones used instead.
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ 
```

```
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ sudo apt-get update
Hit:1 http://packages.microsoft.com/repos/vscode stable InRelease
Hit:2 https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/ InRelease                                                   
Get:3 http://dl.google.com/linux/chrome/deb stable InRelease [1,811 B]                                                       
Get:4 https://dl.yarnpkg.com/debian stable InRelease [17.1 kB]                                                               
Hit:5 https://cloud.r-project.org/bin/linux/ubuntu jammy-cran40/ InRelease                                                   
Hit:6 https://packages.microsoft.com/repos/ms-teams stable InRelease                                                         
Hit:7 https://apt.repos.intel.com/mkl all InRelease                                                                          
Hit:8 http://ppa.launchpad.net/malteworld/ppa/ubuntu bionic InRelease                                                        
Hit:9 http://mm.archive.ubuntu.com/ubuntu bionic InRelease                                                                   
Hit:10 http://security.ubuntu.com/ubuntu bionic-security InRelease                                                           
Err:3 http://dl.google.com/linux/chrome/deb stable InRelease                                                                 
  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 4EB27DB2A3B88B8B
Hit:11 http://mm.archive.ubuntu.com/ubuntu bionic-updates InRelease                                                          
Err:4 https://dl.yarnpkg.com/debian stable InRelease                                                                   
  The following signatures were invalid: EXPKEYSIG 23E7166788B63E1E Yarn Packaging <yarn@dan.cx>
Hit:12 http://ppa.launchpad.net/marutter/rrutter/ubuntu bionic InRelease                       
Err:13 https://dl.bintray.com/sbt/debian  InRelease                                                                         
  502  Bad Gateway [IP: 35.166.126.94 443]
Hit:14 http://mm.archive.ubuntu.com/ubuntu bionic-backports InRelease                                                       
Hit:15 http://ppa.launchpad.net/peek-developers/stable/ubuntu bionic InRelease                        
Hit:16 http://ppa.launchpad.net/ubuntu-toolchain-r/test/ubuntu bionic InRelease 
Reading package lists... Done                       
W: An error occurred during the signature verification. The repository is not updated and the previous index files will be used. GPG error: http://dl.google.com/linux/chrome/deb stable InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 4EB27DB2A3B88B8B
W: An error occurred during the signature verification. The repository is not updated and the previous index files will be used. GPG error: https://dl.yarnpkg.com/debian stable InRelease: The following signatures were invalid: EXPKEYSIG 23E7166788B63E1E Yarn Packaging <yarn@dan.cx>
W: Failed to fetch http://dl.google.com/linux/chrome/deb/dists/stable/InRelease  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 4EB27DB2A3B88B8B
W: Failed to fetch https://dl.bintray.com/sbt/debian/InRelease  502  Bad Gateway [IP: 35.166.126.94 443]
W: Failed to fetch https://dl.yarnpkg.com/debian/dists/stable/InRelease  The following signatures were invalid: EXPKEYSIG 23E7166788B63E1E Yarn Packaging <yarn@dan.cx>
W: Some index files failed to download. They have been ignored, or old ones used instead.
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$
```

```
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ sudo apt-get install r-base r-base-dev
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 r-base : Depends: r-base-core (>= 4.2.1-2.2204.0) but it is not going to be installed
          Depends: r-recommended (= 4.2.1-2.2204.0) but it is not going to be installed
          Recommends: r-base-html but it is not going to be installed
 r-base-dev : Depends: r-base-core (>= 4.2.1-2.2204.0) but it is not going to be installed
E: Unable to correct problems, you have held broken packages.
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$

Error အတူတူပဲ ပေးနေတယ် ...  
```

## Used autoremove

```
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ sudo apt-get autoremove
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages will be REMOVED:
  linux-hwe-5.4-headers-5.4.0-117 linux-hwe-5.4-headers-5.4.0-120 linux-hwe-5.4-headers-5.4.0-121
0 upgraded, 0 newly installed, 3 to remove and 135 not upgraded.
After this operation, 214 MB disk space will be freed.
Do you want to continue? [Y/n] Y
(Reading database ... 470653 files and directories currently installed.)
Removing linux-hwe-5.4-headers-5.4.0-117 (5.4.0-117.132~18.04.1) ...
Removing linux-hwe-5.4-headers-5.4.0-120 (5.4.0-120.136~18.04.1) ...
Removing linux-hwe-5.4-headers-5.4.0-121 (5.4.0-121.137~18.04.1) ...
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$
```

## Retried Again

```
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ sudo add-apt-repository ppa:marutter/rrutter
 Contains packages related to my use of R for research and teaching.  This PPA is also mirrored on the CRAN Ubuntu page.  Please note, R 3.3.0 and above are no longer supported for 12.04 (precise).
 More info: https://launchpad.net/~marutter/+archive/ubuntu/rrutter
Press [ENTER] to continue or Ctrl-c to cancel adding it.

Get:1 http://dl.google.com/linux/chrome/deb stable InRelease [1,811 B]
Hit:2 http://packages.microsoft.com/repos/vscode stable InRelease                                                            
Get:3 https://dl.yarnpkg.com/debian stable InRelease [17.1 kB]                                                               
Hit:4 https://apt.repos.intel.com/mkl all InRelease                                                                          
Hit:5 https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/ InRelease                                                   
Hit:6 https://packages.microsoft.com/repos/ms-teams stable InRelease                                                         
Hit:7 https://cloud.r-project.org/bin/linux/ubuntu jammy-cran40/ InRelease                                                   
Err:1 http://dl.google.com/linux/chrome/deb stable InRelease                                                                 
  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 4EB27DB2A3B88B8B
Hit:8 http://ppa.launchpad.net/malteworld/ppa/ubuntu bionic InRelease                                                        
Hit:9 http://security.ubuntu.com/ubuntu bionic-security InRelease                                                            
Hit:10 http://mm.archive.ubuntu.com/ubuntu bionic InRelease                                                                  
Err:3 https://dl.yarnpkg.com/debian stable InRelease                                                                         
  The following signatures were invalid: EXPKEYSIG 23E7166788B63E1E Yarn Packaging <yarn@dan.cx>
Hit:11 http://mm.archive.ubuntu.com/ubuntu bionic-updates InRelease                                                          
Hit:12 http://ppa.launchpad.net/marutter/rrutter/ubuntu bionic InRelease                                               
Hit:13 http://mm.archive.ubuntu.com/ubuntu bionic-backports InRelease                          
Err:14 https://dl.bintray.com/sbt/debian  InRelease                                                   
  502  Bad Gateway [IP: 35.166.126.94 443]
Hit:15 http://ppa.launchpad.net/peek-developers/stable/ubuntu bionic InRelease                        
Hit:16 http://ppa.launchpad.net/ubuntu-toolchain-r/test/ubuntu bionic InRelease 
Reading package lists... Done                      
W: An error occurred during the signature verification. The repository is not updated and the previous index files will be used. GPG error: http://dl.google.com/linux/chrome/deb stable InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 4EB27DB2A3B88B8B
W: An error occurred during the signature verification. The repository is not updated and the previous index files will be used. GPG error: https://dl.yarnpkg.com/debian stable InRelease: The following signatures were invalid: EXPKEYSIG 23E7166788B63E1E Yarn Packaging <yarn@dan.cx>
W: Failed to fetch http://dl.google.com/linux/chrome/deb/dists/stable/InRelease  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 4EB27DB2A3B88B8B
W: Failed to fetch https://dl.bintray.com/sbt/debian/InRelease  502  Bad Gateway [IP: 35.166.126.94 443]
W: Failed to fetch https://dl.yarnpkg.com/debian/dists/stable/InRelease  The following signatures were invalid: EXPKEYSIG 23E7166788B63E1E Yarn Packaging <yarn@dan.cx>
W: Some index files failed to download. They have been ignored, or old ones used instead.
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ 
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ sudo apt-get update
Get:1 http://dl.google.com/linux/chrome/deb stable InRelease [1,811 B]
Hit:2 http://packages.microsoft.com/repos/vscode stable InRelease                                                            
Hit:3 https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/ InRelease                                                   
Get:4 https://dl.yarnpkg.com/debian stable InRelease [17.1 kB]                                                               
Hit:5 https://packages.microsoft.com/repos/ms-teams stable InRelease                                                         
Err:1 http://dl.google.com/linux/chrome/deb stable InRelease                                                                 
  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 4EB27DB2A3B88B8B
Hit:6 https://cloud.r-project.org/bin/linux/ubuntu jammy-cran40/ InRelease                                                   
Hit:7 https://apt.repos.intel.com/mkl all InRelease                                                                          
Hit:8 http://ppa.launchpad.net/malteworld/ppa/ubuntu bionic InRelease                                                        
Hit:9 http://mm.archive.ubuntu.com/ubuntu bionic InRelease                                                                   
Hit:10 http://security.ubuntu.com/ubuntu bionic-security InRelease                                                           
Err:4 https://dl.yarnpkg.com/debian stable InRelease                                                                         
  The following signatures were invalid: EXPKEYSIG 23E7166788B63E1E Yarn Packaging <yarn@dan.cx>
Hit:11 http://ppa.launchpad.net/marutter/rrutter/ubuntu bionic InRelease                                                     
Hit:12 http://mm.archive.ubuntu.com/ubuntu bionic-updates InRelease                            
Err:13 https://dl.bintray.com/sbt/debian  InRelease                                                                         
  502  Bad Gateway [IP: 52.36.126.31 443]
Hit:14 http://mm.archive.ubuntu.com/ubuntu bionic-backports InRelease                                                       
Hit:15 http://ppa.launchpad.net/peek-developers/stable/ubuntu bionic InRelease                        
Hit:16 http://ppa.launchpad.net/ubuntu-toolchain-r/test/ubuntu bionic InRelease
Reading package lists... Done                       
W: An error occurred during the signature verification. The repository is not updated and the previous index files will be used. GPG error: http://dl.google.com/linux/chrome/deb stable InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 4EB27DB2A3B88B8B
W: An error occurred during the signature verification. The repository is not updated and the previous index files will be used. GPG error: https://dl.yarnpkg.com/debian stable InRelease: The following signatures were invalid: EXPKEYSIG 23E7166788B63E1E Yarn Packaging <yarn@dan.cx>
W: Failed to fetch http://dl.google.com/linux/chrome/deb/dists/stable/InRelease  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 4EB27DB2A3B88B8B
W: Failed to fetch https://dl.bintray.com/sbt/debian/InRelease  502  Bad Gateway [IP: 52.36.126.31 443]
W: Failed to fetch https://dl.yarnpkg.com/debian/dists/stable/InRelease  The following signatures were invalid: EXPKEYSIG 23E7166788B63E1E Yarn Packaging <yarn@dan.cx>
W: Some index files failed to download. They have been ignored, or old ones used instead.
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ sudo apt-get install r-base r-base-dev
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 r-base : Depends: r-base-core (>= 4.2.1-2.2204.0) but it is not going to be installed
          Depends: r-recommended (= 4.2.1-2.2204.0) but it is not going to be installed
          Recommends: r-base-html but it is not going to be installed
 r-base-dev : Depends: r-base-core (>= 4.2.1-2.2204.0) but it is not going to be installed
E: Unable to correct problems, you have held broken packages.
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ 
```

Error ပေးနေသေးတယ်။  

## Searching with apt search

```
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ sudo apt search r-base
Sorting... Done
Full Text Search... Done
cairo-perf-utils/bionic-updates 1.15.10-2ubuntu0.1 amd64
  Cairo 2D vector graphics library performance utilities

courier-base/bionic 0.78.0-2ubuntu2 amd64
  Courier mail server - base system

dacs/bionic 1.4.38a-2build1 amd64
  Distributed Access Control System (DACS)

dacs-examples/bionic,bionic 1.4.38a-2build1 all
  Distributed Access Control System (DACS) - example web root

dc-qt/bionic 0.2.0.alpha-4.3build1 amd64
  GUI frontend for the dc protocol

dh-consoledata/bionic,bionic 0.7.89 all
  debhelper-based script to help packaging console data files

dh-octave/bionic,bionic 0.3.2 all
  Debhelper-based infrastructure for building Octave add-on packages

elpa-ert-expectations/bionic,bionic 0.2-1 all
  very simple unit test framework for Emacs Lisp

flashproxy-client/bionic,bionic 1.7-4 all
  Pluggable transport to circumvent IP address blocking - client transport plugin

flashproxy-common/bionic,bionic 1.7-4 all
  Pluggable transport to circumvent IP address blocking - common library

flashproxy-facilitator/bionic,bionic 1.7-4 all
  Pluggable transport to circumvent IP address blocking - facilitator

flashproxy-proxy/bionic,bionic 1.7-4 all
  Pluggable transport to circumvent IP address blocking - browser proxy

gcc-m68hc1x/bionic 1:3.3.6+3.1+dfsg-3ubuntu2 amd64
  GNU C compiler for the Motorola 68HC11/12 processors

gimp-plugin-registry/bionic 7.20140602ubuntu3 amd64
  repository of optional extensions for GIMP

gir1.2-mutter-2/bionic-updates 3.28.4+git20200505-0ubuntu18.04.2 amd64 [upgradable from: 3.28.4-0ubuntu18.04.2]
  GObject introspection data for Mutter

gir1.2-ukwm-1/bionic 1.1.8-0ubuntu1 amd64
  GObject introspection data for Ukwm

gtk-gnutella/bionic 1.1.8-2 amd64
  shares files in a peer to peer network

gtk-gnutella-dbg/bionic 1.1.8-2 amd64
  shares files in a peer to peer network (debugging symbols)

haskell-hosc-utils/bionic,bionic 0.15-1 all
  Haskell Open Sound Control

ikarus/bionic 0.0.3+bzr.2010.01.26-4ubuntu1 amd64
  Scheme compiler and interpreter

inkscape/bionic 0.92.3-1 amd64
  vector-based drawing program

kamailio-presence-modules/bionic 5.1.2-1ubuntu2 amd64
  SIP presence modules for Kamailio

kodi-pvr-vuplus/bionic 2.4.12+dfsg1-1 amd64
  Vu+/Enigma2 PVR Addon for Kodi

language-pack-ar/bionic-updates,bionic-updates 1:18.04+20180712 all
  translation updates for language Arabic

language-pack-ar-base/bionic-updates,bionic-updates 1:18.04+20180712 all
  translations for language Arabic

language-pack-br/bionic-updates,bionic-updates 1:18.04+20180712 all
  translation updates for language Breton

language-pack-br-base/bionic-updates,bionic-updates 1:18.04+20180712 all
  translations for language Breton

language-pack-fr/bionic-updates,bionic-updates 1:18.04+20200702 all
  translation updates for language French

language-pack-fr-base/bionic-updates,bionic-updates 1:18.04+20180712 all
  translations for language French

language-pack-fur/bionic-updates,bionic-updates 1:18.04+20180712 all
  translation updates for language Friulian

language-pack-fur-base/bionic-updates,bionic-updates 1:18.04+20180712 all
  translations for language Friulian

language-pack-gnome-ar/bionic-updates,bionic-updates 1:18.04+20180712 all
  GNOME translation updates for language Arabic

language-pack-gnome-ar-base/bionic-updates,bionic-updates 1:18.04+20180712 all
  GNOME translations for language Arabic

language-pack-gnome-br/bionic-updates,bionic-updates 1:18.04+20180712 all
  GNOME translation updates for language Breton

language-pack-gnome-br-base/bionic-updates,bionic-updates 1:18.04+20180712 all
  GNOME translations for language Breton

language-pack-gnome-fr/bionic-updates,bionic-updates 1:18.04+20200702 all
  GNOME translation updates for language French

language-pack-gnome-fr-base/bionic-updates,bionic-updates 1:18.04+20180712 all
  GNOME translations for language French

language-pack-gnome-fur/bionic-updates,bionic-updates 1:18.04+20180712 all
  GNOME translation updates for language Friulian

language-pack-gnome-fur-base/bionic-updates,bionic-updates 1:18.04+20180712 all
  GNOME translations for language Friulian

language-pack-gnome-hr/bionic-updates,bionic-updates 1:18.04+20180712 all
  GNOME translation updates for language Croatian

language-pack-gnome-hr-base/bionic-updates,bionic-updates 1:18.04+20180712 all
  GNOME translations for language Croatian

language-pack-gnome-mr/bionic-updates,bionic-updates 1:18.04+20180712 all
  GNOME translation updates for language Marathi

language-pack-gnome-mr-base/bionic-updates,bionic-updates 1:18.04+20180712 all
  GNOME translations for language Marathi

language-pack-gnome-or/bionic-updates,bionic-updates 1:18.04+20180712 all
  GNOME translation updates for language Oriya

language-pack-gnome-or-base/bionic-updates,bionic-updates 1:18.04+20180712 all
  GNOME translations for language Oriya

language-pack-gnome-sr/bionic-updates,bionic-updates 1:18.04+20180712 all
  GNOME translation updates for language Serbian

language-pack-gnome-sr-base/bionic-updates,bionic-updates 1:18.04+20180712 all
  GNOME translations for language Serbian

language-pack-gnome-tr/bionic-updates,bionic-updates 1:18.04+20180712 all
  GNOME translation updates for language Turkish

language-pack-gnome-tr-base/bionic-updates,bionic-updates 1:18.04+20180712 all
  GNOME translations for language Turkish

language-pack-hr/bionic-updates,bionic-updates 1:18.04+20180712 all
  translation updates for language Croatian

language-pack-hr-base/bionic-updates,bionic-updates 1:18.04+20180712 all
  translations for language Croatian

language-pack-mr/bionic-updates,bionic-updates 1:18.04+20180712 all
  translation updates for language Marathi

language-pack-mr-base/bionic-updates,bionic-updates 1:18.04+20180712 all
  translations for language Marathi

language-pack-or/bionic-updates,bionic-updates 1:18.04+20180712 all
  translation updates for language Oriya

language-pack-or-base/bionic-updates,bionic-updates 1:18.04+20180712 all
  translations for language Oriya

language-pack-sr/bionic-updates,bionic-updates 1:18.04+20180712 all
  translation updates for language Serbian

language-pack-sr-base/bionic-updates,bionic-updates 1:18.04+20180712 all
  translations for language Serbian

language-pack-tr/bionic-updates,bionic-updates 1:18.04+20180712 all
  translation updates for language Turkish

language-pack-tr-base/bionic-updates,bionic-updates 1:18.04+20180712 all
  translations for language Turkish

libace-flreactor-6.4.5/bionic 6.4.5+dfsg-1build2 amd64
  ACE-GUI reactor integration for FLTK

libace-foxreactor-6.4.5/bionic 6.4.5+dfsg-1build2 amd64
  ACE-GUI reactor integration for FOX

libace-tkreactor-6.4.5/bionic 6.4.5+dfsg-1build2 amd64
  ACE-GUI reactor integration for Tk

libace-xtreactor-6.4.5/bionic 6.4.5+dfsg-1build2 amd64
  ACE-GUI reactor integration for Xt

libapache2-mod-dacs/bionic 1.4.38a-2build1 amd64
  Distributed Access Control System (DACS) - Apache Module

libapache2-mod-r-base/bionic 1.2.8-1 amd64
  server-side R integration with Apache 2

libcairo-gobject2/bionic-updates,now 1.15.10-2ubuntu0.1 amd64 [installed,automatic]
  Cairo 2D vector graphics library (GObject library)

libcairo-ocaml/bionic 1:1.2.0-6build3 amd64
  OCaml bindings for Cairo (runtime)

libcairo-ocaml-dev/bionic 1:1.2.0-6build3 amd64
  OCaml bindings for Cairo

libcairo-script-interpreter2/bionic-updates,now 1.15.10-2ubuntu0.1 amd64 [installed,automatic]
  Cairo 2D vector graphics library (script interpreter)

libcairo2/bionic-updates,now 1.15.10-2ubuntu0.1 amd64 [installed,automatic]
  Cairo 2D vector graphics library

libcairo2-dev/bionic-updates,now 1.15.10-2ubuntu0.1 amd64 [installed]
  Development files for the Cairo 2D graphics library

libcairo2-doc/bionic-updates,bionic-updates 1.15.10-2ubuntu0.1 all
  Documentation for the Cairo Multi-platform 2D graphics library

libcairomm-1.0-1v5/bionic,now 1.12.2-3 amd64 [installed,automatic]
  C++ wrappers for Cairo (shared libraries)

libcairomm-1.0-dev/bionic 1.12.2-3 amd64
  C++ wrappers for Cairo (development files)

libcairomm-1.0-doc/bionic,bionic 1.12.2-3 all
  C++ wrappers for Cairo (documentation)

libconfig-grammar-perl/bionic,bionic 1.12-1 all
  grammar-based user-friendly config parser

libdacs-dev/bionic 1.4.38a-2build1 amd64
  Distributed Access Control System (DACS) - development files

libdacs1/bionic 1.4.38a-2build1 amd64
  Distributed Access Control System (DACS) - shared library

libfast-zip-visit-clojure/bionic,bionic 1.0.2-2 all
  Clojure zipper-based visitor library (fast-zip version)

libfile-next-perl/bionic,bionic 1.16-2 all
  file-finding iterator

libgcr-base-3-1/bionic,now 3.28.0-1 amd64 [installed,automatic]
  Library for Crypto related tasks

libghc-formatting-dev/bionic 6.2.5-1 amd64
  combinator-based type-safe formatting

libghc-formatting-doc/bionic,bionic 6.2.5-1 all
  combinator-based type-safe formatting; documentation

libghc-formatting-prof/bionic 6.2.5-1 amd64
  combinator-based type-safe formatting; profiling libraries

libghc-hosc-dev/bionic 0.15-1 amd64
  Haskell Open Sound Control

libghc-hosc-doc/bionic,bionic 0.15-1 all
  Haskell Open Sound Control; documentation

libghc-hosc-prof/bionic 0.15-1 amd64
  Haskell Open Sound Control; profiling libraries

libjs-jquery-colorpicker/bionic,bionic 1.2.16-1 all
  full-featured colorpicker for jQuery UI

libjs-jscommunicator/bionic,bionic 2.1.3-1 all
  Browser-based messaging, phone and video chat application

libjs-proj4/bionic,bionic 2.3.17+ds-1 all
  JavaScript library to transform point coordinates systems

libmediastreamer-base3/bionic 3.6.1-3build1 amd64
  Linphone web phone's media library

libmutter-2-0/bionic-updates 3.28.4+git20200505-0ubuntu18.04.2 amd64 [upgradable from: 3.28.4-0ubuntu18.04.2]
  window manager library from the Mutter window manager

libmutter-2-dev/bionic-updates 3.28.4+git20200505-0ubuntu18.04.2 amd64
  Development files for the Mutter window manager

libnoggit-java/bionic,bionic 0.7-1 all
  Fast streaming JSON parser for Java

libopenni-java/bionic 1.5.4.0-14build1 amd64
  Java framework for sensor-based 'Natural Interaction'

libopenni0/bionic 1.5.4.0-14build1 amd64
  framework for sensor-based 'Natural Interaction'

libopenni2-0/bionic 2.2.0.33+dfsg-10 amd64
  framework for sensor-based 'Natural Interaction'

librandom123-dev/bionic,bionic 1.09+dfsg-1 all
  parallel random numbers library

librandom123-doc/bionic,bionic 1.09+dfsg-1 all
  documentation and examples of parallel random numbers library

libsms-send-perl/bionic,bionic 1.06-3 all
  driver-based API for sending SMS messages

libtest-class-perl/bionic,bionic 0.50-1 all
  module for creating test classes in an xUnit style

libtest-yaml-valid-perl/bionic,bionic 0.04-1 all
  module to test for valid YAML

libtrapperkeeper-status-clojure/bionic,bionic 0.7.1-1ubuntu1 all
  status monitoring for trapperkeeper services

libukwm-1-0/bionic 1.1.8-0ubuntu1 amd64
  window manager library from the Ukwm window manager

libukwm-1-dev/bionic 1.1.8-0ubuntu1 amd64
  Development files for the Ukwm window manager

libutempter-dev/bionic 1.1.6-3 amd64
  privileged helper for utmp/wtmp updates (development)

mancala/bionic 1.0.3-1build1 amd64
  Implementation of the simple board game called Mancala

miniasm/bionic 0.2+dfsg-2 amd64
  ultrafast de novo assembler for long noisy DNA sequencing reads

muchsync/bionic 5-1 amd64
  synchronize maildirs and notmuch databases

mutter/bionic-updates 3.28.4+git20200505-0ubuntu18.04.2 amd64 [upgradable from: 3.28.4-0ubuntu18.04.2]
  lightweight GTK+ window manager

mutter-common/bionic-updates,bionic-updates 3.28.4+git20200505-0ubuntu18.04.2 all [upgradable from: 3.28.4-0ubuntu18.04.2]
  shared files for the Mutter window manager

node-cipher-base/bionic,bionic 1.0.4-1 all
  abstract base class for crypto-streams

node-flashproxy/bionic,bionic 1.7-4 all
  Pluggable transport to circumvent IP address blocking - nodejs proxy

node-proj4/bionic,bionic 2.3.17+ds-1 all
  Node.js module to transform point coordinates systems

opensips-presence-modules/bionic 2.2.2-3build4 amd64
  SIMPLE presence modules for OpenSIPS

pd-bassemu/bionic 0.3-5 amd64
  Pd object for transistor bass emulation

pd-xsample/bionic 0.3.2+git20170905.1.4441ae5-2 amd64
  extended sample objects for Pure Data

printer-driver-hpcups/bionic,now 3.17.10+repack0-5 amd64 [installed,automatic]
  HP Linux Printing and Imaging - CUPS Raster driver (hpcups)

python-napalm-iosxr/bionic,bionic 0.5.6-1 all
  abstraction layer for multivendor network automation - IOS-XR support

python-pyeclib/bionic 1.3.1-1ubuntu3 amd64
  interface for implementing erasure codes - Python 2.x

python-pykmip/bionic,bionic 0.7.0-2 all
  implementation of the Key Management Interoperability Protocol - Python 2.x

python-tktreectrl/bionic,bionic 2.0.1-1 all
  Tkinter-based wrapper for Tk TreeCtrl

python3-cairo-doc/bionic,bionic 1.16.2-1 all
  Python 3 cairo bindings: documentation files

python3-pyeclib/bionic 1.3.1-1ubuntu3 amd64
  interface for implementing erasure codes - Python 3.x

python3-pykmip/bionic,bionic 0.7.0-2 all
  KMIP v1.1 library - Python 3.x

python3-pytest-tempdir/bionic,bionic 2016.8.20-1 all
  predictable and repeatable temporary directory for tests

r-base/jammy-cran40 4.2.1-2.2204.0 all
  GNU R statistical computation and graphics system

r-base-core/jammy-cran40 4.2.1-2.2204.0 amd64
  GNU R core of statistical computation and graphics system

r-base-core-dbg/focal-cran40 4.1.3-1.2004.0 amd64
  GNU R debug symbols for statistical comp. language and environment

r-base-dev/jammy-cran40 4.2.1-2.2204.0 all
  GNU R installation of auxiliary GNU R packages

r-base-html/jammy-cran40 4.2.1-2.2204.0 all
  GNU R html docs for statistical computing system functions

r-cran-date/bionic 1.2.38-1 amd64
  GNU R package for date handling

r-cran-matrixstats/bionic 0.52.2-2 amd64
  GNU R methods that apply to rows and columns of a matrix

rapmap/bionic 0.5.0+dfsg-3 amd64
  rapid sensitive and accurate DNA read mapping via quasi-mapping

roundcube/bionic,bionic 1.3.6+dfsg.1-1 all
  skinnable AJAX based webmail solution for IMAP servers - metapackage

roundcube-core/bionic,bionic 1.3.6+dfsg.1-1 all
  skinnable AJAX based webmail solution for IMAP servers

roundcube-plugins/bionic,bionic 1.3.6+dfsg.1-1 all
  skinnable AJAX based webmail solution for IMAP servers - plugins

ruby-cairo/bionic 1.15.12-1 amd64
  Cairo bindings for the Ruby language

ruby-cairo-gobject/bionic 3.2.4-1 amd64
  CairoGObject bindings for the Ruby language

ruby-celluloid/bionic,bionic 0.16.0-5 all
  actor-based concurrent object framework for ruby

ruby-celluloid-essentials/bionic,bionic 0.20.5-1 all
  internally used Celluloid tools and superstructural dependencies

ruby-celluloid-extras/bionic,bionic 0.20.5-1 all
  Celluloid expansion, testing, and example classes

ruby-celluloid-fsm/bionic,bionic 0.20.5-1 all
  Celluloid Finite State Machines

ruby-celluloid-pool/bionic,bionic 0.20.5-1 all
  actor pool based on Celluloid

ruby-celluloid-supervision/bionic,bionic 0.20.5-1 all
  Supervision support for Celluloid

sbd/bionic 1.3.1-2 amd64
  STONITH Block Device daemon

screen/bionic-updates,bionic-security 4.6.2-1ubuntu1.1 amd64
  terminal multiplexer with VT100/ANSI terminal emulation

solfege/bionic,bionic 3.22.2-2 all
  Ear training software

synfig/bionic 1.2.1-0ubuntu4 amd64
  vector-based 2D animation renderer

synfigstudio/bionic 1.2.1-0.1 amd64
  vector-based 2D animation package (graphical user interface)

texlive-publishers/bionic,bionic 2017.20180305-2 all
  TeX Live: Publisher styles, theses, etc.

timewarrior/bionic 1.0.0+ds.1-3 amd64
  feature-rich time tracking utility

ukwm/bionic 1.1.8-0ubuntu1 amd64
  lightweight GTK+ window manager

ukwm-common/bionic,bionic 1.1.8-0ubuntu1 all
  shared files for the Ukwm window manager

vectoroids/bionic 1.1.0-13build1 amd64
  vector-based rock-shooting

vim-youcompleteme/bionic,bionic 0+20161219+git194ff33-1 all
  fast, as-you-type, fuzzy-search code completion engine for Vim

vspline-dev/bionic,bionic 0.3.1-1 all
  header-only C++ template library for uniform b-spline processing

xdm/bionic 1:1.1.11-3ubuntu1 amd64
  X display manager

xinv3d/bionic 1.3.6-6build1 amd64
  3D space invaders for X

(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ sudo apt search r-base-dev
Sorting... Done
Full Text Search... Done
r-base-dev/jammy-cran40 4.2.1-2.2204.0 all
  GNU R installation of auxiliary GNU R packages

(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$
```

## [Editing sources.list File](#solution)

```
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ sudo gedit  /etc/apt/sources.list
```

sources.list ဖိုင်ကို ဖွင့်ပြီး focal-cran40 လိုင်းကို comment ပိတ်ပြီး bionic-cran35 ဆိုတဲ့ လိုင်းကို ဝင်ဖြည့်ခဲ့ ...   

```
# deb https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/
# deb-src https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/
deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/
```

## Reinstall the R Again

```
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ sudo apt-get install -y r-base r-base-dev
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  cdbs debhelper dh-autoreconf dh-strip-nondeterminism dh-translations gfortran gfortran-7 intltool jq libarchive-cpio-perl
  libblas-dev libfile-stripnondeterminism-perl libgfortran-7-dev libjq1 liblapack-dev libmail-sendmail-perl libncurses5-dev
  libonig4 libsys-hostname-long-perl po-debconf python3-scour r-base-core r-base-html r-cran-boot r-cran-class
  r-cran-cluster r-cran-codetools r-cran-foreign r-cran-kernsmooth r-cran-lattice r-cran-mass r-cran-matrix r-cran-mgcv
  r-cran-nlme r-cran-nnet r-cran-rpart r-cran-spatial r-cran-survival r-doc-html r-recommended scour
Suggested packages:
  devscripts dh-make dwz gfortran-multilib gfortran-doc gfortran-7-multilib gfortran-7-doc libgfortran4-dbg libcoarrays-dev
  liblapack-doc ncurses-doc libmail-box-perl ess r-doc-info | r-doc-pdf r-mathlib texlive-generic-recommended texinfo
The following NEW packages will be installed:
  cdbs debhelper dh-autoreconf dh-strip-nondeterminism dh-translations gfortran gfortran-7 intltool jq libarchive-cpio-perl
  libblas-dev libfile-stripnondeterminism-perl libgfortran-7-dev libjq1 liblapack-dev libmail-sendmail-perl libncurses5-dev
  libonig4 libsys-hostname-long-perl po-debconf python3-scour r-base r-base-core r-base-dev r-base-html r-cran-boot
  r-cran-class r-cran-cluster r-cran-codetools r-cran-foreign r-cran-kernsmooth r-cran-lattice r-cran-mass r-cran-matrix
  r-cran-mgcv r-cran-nlme r-cran-nnet r-cran-rpart r-cran-spatial r-cran-survival r-doc-html r-recommended scour
0 upgraded, 43 newly installed, 0 to remove and 135 not upgraded.
Need to get 54.1 MB of archives.
After this operation, 111 MB of additional disk space will be used.
Get:1 http://mm.archive.ubuntu.com/ubuntu bionic/main amd64 dh-autoreconf all 17 [15.8 kB]
Get:2 http://mm.archive.ubuntu.com/ubuntu bionic/main amd64 libfile-stripnondeterminism-perl all 0.040-1.1~build1 [13.8 kB]
Get:3 http://mm.archive.ubuntu.com/ubuntu bionic/main amd64 dh-strip-nondeterminism all 0.040-1.1~build1 [5,208 B]
Get:4 http://mm.archive.ubuntu.com/ubuntu bionic/main amd64 po-debconf all 1.0.20 [232 kB]
Get:5 http://mm.archive.ubuntu.com/ubuntu bionic-updates/main amd64 debhelper all 11.1.6ubuntu2 [902 kB]
Get:6 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 intltool all 0.51.0-5ubuntu1 [44.6 kB]
Get:7 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 libonig4 amd64 6.7.0-1 [119 kB]
Get:8 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 libjq1 amd64 1.5+dfsg-2 [111 kB]
Get:9 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 jq amd64 1.5+dfsg-2 [45.6 kB]
Get:10 http://mm.archive.ubuntu.com/ubuntu bionic-updates/universe amd64 dh-translations all 138.18.04.1 [24.6 kB]
Get:11 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 python3-scour all 0.36-2 [44.8 kB]
Get:12 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 scour all 0.36-2 [7,372 B]
Get:13 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 cdbs all 0.4.156ubuntu4 [45.4 kB]
Get:14 http://mm.archive.ubuntu.com/ubuntu bionic-updates/main amd64 libgfortran-7-dev amd64 7.5.0-3ubuntu1~18.04 [530 kB]
Get:15 http://mm.archive.ubuntu.com/ubuntu bionic-updates/main amd64 gfortran-7 amd64 7.5.0-3ubuntu1~18.04 [9,014 kB]
Get:16 http://mm.archive.ubuntu.com/ubuntu bionic-updates/main amd64 gfortran amd64 4:7.4.0-1ubuntu2.3 [1,356 B]
Get:17 http://mm.archive.ubuntu.com/ubuntu bionic/main amd64 libarchive-cpio-perl all 0.10-1 [9,644 B]
Get:18 http://mm.archive.ubuntu.com/ubuntu bionic/main amd64 libblas-dev amd64 3.7.1-4ubuntu1 [143 kB]
Get:19 http://mm.archive.ubuntu.com/ubuntu bionic/main amd64 liblapack-dev amd64 3.7.1-4ubuntu1 [2,140 kB]
Get:20 http://mm.archive.ubuntu.com/ubuntu bionic/main amd64 libsys-hostname-long-perl all 1.5-1 [11.7 kB]
Get:21 http://mm.archive.ubuntu.com/ubuntu bionic/main amd64 libmail-sendmail-perl all 0.80-1 [22.6 kB]
Get:22 http://mm.archive.ubuntu.com/ubuntu bionic-updates/main amd64 libncurses5-dev amd64 6.1-1ubuntu1.18.04 [174 kB]
Get:23 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 r-base-core amd64 3.4.4-1ubuntu1 [23.2 MB]
Get:24 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 r-cran-boot all 1.3-20-1.1 [613 kB]                         
Get:25 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 r-cran-cluster amd64 2.0.6-2build1 [502 kB]                 
Get:26 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 r-cran-foreign amd64 0.8.69-1build1 [228 kB]                
Get:27 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 r-cran-mass amd64 7.3-49-1 [1,100 kB]                       
Get:28 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 r-cran-kernsmooth amd64 2.23-15-3build1 [89.4 kB]           
Get:29 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 r-cran-lattice amd64 0.20-35-1build1 [713 kB]               
Get:30 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 r-cran-nlme amd64 3.1.131-3build1 [2,186 kB]                
Get:31 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 r-cran-matrix amd64 1.2-12-1 [2,334 kB]                     
Get:32 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 r-cran-mgcv amd64 1.8-23-1 [2,496 kB]                       
Get:33 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 r-cran-survival amd64 2.41-3-2build1 [5,156 kB]             
Get:34 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 r-cran-rpart amd64 4.1-13-1 [878 kB]                        
Get:35 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 r-cran-class amd64 7.3-14-2build1 [85.9 kB]                 
Get:36 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 r-cran-nnet amd64 7.3-12-2build1 [110 kB]                   
Get:37 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 r-cran-spatial amd64 7.3-11-2build1 [127 kB]                
Get:38 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 r-cran-codetools all 0.2-15-1.1 [46.1 kB]                   
Get:39 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 r-recommended all 3.4.4-1ubuntu1 [2,820 B]                  
Get:40 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 r-base all 3.4.4-1ubuntu1 [9,312 B]                         
Get:41 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 r-base-dev all 3.4.4-1ubuntu1 [4,532 B]                     
Get:42 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 r-doc-html all 3.4.4-1ubuntu1 [527 kB]                      
Get:43 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 r-base-html all 3.4.4-1ubuntu1 [54.8 kB]                    
Fetched 54.1 MB in 11s (5,046 kB/s)                                                                                          
Extracting templates from packages: 100%
Selecting previously unselected package dh-autoreconf.
(Reading database ... 417374 files and directories currently installed.)
Preparing to unpack .../00-dh-autoreconf_17_all.deb ...
Unpacking dh-autoreconf (17) ...
Selecting previously unselected package libfile-stripnondeterminism-perl.
Preparing to unpack .../01-libfile-stripnondeterminism-perl_0.040-1.1~build1_all.deb ...
Unpacking libfile-stripnondeterminism-perl (0.040-1.1~build1) ...
Selecting previously unselected package dh-strip-nondeterminism.
Preparing to unpack .../02-dh-strip-nondeterminism_0.040-1.1~build1_all.deb ...
Unpacking dh-strip-nondeterminism (0.040-1.1~build1) ...
Selecting previously unselected package po-debconf.
Preparing to unpack .../03-po-debconf_1.0.20_all.deb ...
Unpacking po-debconf (1.0.20) ...
Selecting previously unselected package debhelper.
Preparing to unpack .../04-debhelper_11.1.6ubuntu2_all.deb ...
Unpacking debhelper (11.1.6ubuntu2) ...
Selecting previously unselected package intltool.
Preparing to unpack .../05-intltool_0.51.0-5ubuntu1_all.deb ...
Unpacking intltool (0.51.0-5ubuntu1) ...
Selecting previously unselected package libonig4:amd64.
Preparing to unpack .../06-libonig4_6.7.0-1_amd64.deb ...
Unpacking libonig4:amd64 (6.7.0-1) ...
Selecting previously unselected package libjq1:amd64.
Preparing to unpack .../07-libjq1_1.5+dfsg-2_amd64.deb ...
Unpacking libjq1:amd64 (1.5+dfsg-2) ...
Selecting previously unselected package jq.
Preparing to unpack .../08-jq_1.5+dfsg-2_amd64.deb ...
Unpacking jq (1.5+dfsg-2) ...
Selecting previously unselected package dh-translations.
Preparing to unpack .../09-dh-translations_138.18.04.1_all.deb ...
Unpacking dh-translations (138.18.04.1) ...
Selecting previously unselected package python3-scour.
Preparing to unpack .../10-python3-scour_0.36-2_all.deb ...
Unpacking python3-scour (0.36-2) ...
Selecting previously unselected package scour.
Preparing to unpack .../11-scour_0.36-2_all.deb ...
Unpacking scour (0.36-2) ...
Selecting previously unselected package cdbs.
Preparing to unpack .../12-cdbs_0.4.156ubuntu4_all.deb ...
Unpacking cdbs (0.4.156ubuntu4) ...
Selecting previously unselected package libgfortran-7-dev:amd64.
Preparing to unpack .../13-libgfortran-7-dev_7.5.0-3ubuntu1~18.04_amd64.deb ...
Unpacking libgfortran-7-dev:amd64 (7.5.0-3ubuntu1~18.04) ...
Selecting previously unselected package gfortran-7.
Preparing to unpack .../14-gfortran-7_7.5.0-3ubuntu1~18.04_amd64.deb ...
Unpacking gfortran-7 (7.5.0-3ubuntu1~18.04) ...
Selecting previously unselected package gfortran.
Preparing to unpack .../15-gfortran_4%3a7.4.0-1ubuntu2.3_amd64.deb ...
Unpacking gfortran (4:7.4.0-1ubuntu2.3) ...
Selecting previously unselected package libarchive-cpio-perl.
Preparing to unpack .../16-libarchive-cpio-perl_0.10-1_all.deb ...
Unpacking libarchive-cpio-perl (0.10-1) ...
Selecting previously unselected package libblas-dev:amd64.
Preparing to unpack .../17-libblas-dev_3.7.1-4ubuntu1_amd64.deb ...
Unpacking libblas-dev:amd64 (3.7.1-4ubuntu1) ...
Selecting previously unselected package liblapack-dev:amd64.
Preparing to unpack .../18-liblapack-dev_3.7.1-4ubuntu1_amd64.deb ...
Unpacking liblapack-dev:amd64 (3.7.1-4ubuntu1) ...
Selecting previously unselected package libsys-hostname-long-perl.
Preparing to unpack .../19-libsys-hostname-long-perl_1.5-1_all.deb ...
Unpacking libsys-hostname-long-perl (1.5-1) ...
Selecting previously unselected package libmail-sendmail-perl.
Preparing to unpack .../20-libmail-sendmail-perl_0.80-1_all.deb ...
Unpacking libmail-sendmail-perl (0.80-1) ...
Selecting previously unselected package libncurses5-dev:amd64.
Preparing to unpack .../21-libncurses5-dev_6.1-1ubuntu1.18.04_amd64.deb ...
Unpacking libncurses5-dev:amd64 (6.1-1ubuntu1.18.04) ...
Selecting previously unselected package r-base-core.
Preparing to unpack .../22-r-base-core_3.4.4-1ubuntu1_amd64.deb ...
Unpacking r-base-core (3.4.4-1ubuntu1) ...
Selecting previously unselected package r-cran-boot.
Preparing to unpack .../23-r-cran-boot_1.3-20-1.1_all.deb ...
Unpacking r-cran-boot (1.3-20-1.1) ...
Selecting previously unselected package r-cran-cluster.
Preparing to unpack .../24-r-cran-cluster_2.0.6-2build1_amd64.deb ...
Unpacking r-cran-cluster (2.0.6-2build1) ...
Selecting previously unselected package r-cran-foreign.
Preparing to unpack .../25-r-cran-foreign_0.8.69-1build1_amd64.deb ...
Unpacking r-cran-foreign (0.8.69-1build1) ...
Selecting previously unselected package r-cran-mass.
Preparing to unpack .../26-r-cran-mass_7.3-49-1_amd64.deb ...
Unpacking r-cran-mass (7.3-49-1) ...
Selecting previously unselected package r-cran-kernsmooth.
Preparing to unpack .../27-r-cran-kernsmooth_2.23-15-3build1_amd64.deb ...
Unpacking r-cran-kernsmooth (2.23-15-3build1) ...
Selecting previously unselected package r-cran-lattice.
Preparing to unpack .../28-r-cran-lattice_0.20-35-1build1_amd64.deb ...
Unpacking r-cran-lattice (0.20-35-1build1) ...
Selecting previously unselected package r-cran-nlme.
Preparing to unpack .../29-r-cran-nlme_3.1.131-3build1_amd64.deb ...
Unpacking r-cran-nlme (3.1.131-3build1) ...
Selecting previously unselected package r-cran-matrix.
Preparing to unpack .../30-r-cran-matrix_1.2-12-1_amd64.deb ...
Unpacking r-cran-matrix (1.2-12-1) ...
Selecting previously unselected package r-cran-mgcv.
Preparing to unpack .../31-r-cran-mgcv_1.8-23-1_amd64.deb ...
Unpacking r-cran-mgcv (1.8-23-1) ...
Selecting previously unselected package r-cran-survival.
Preparing to unpack .../32-r-cran-survival_2.41-3-2build1_amd64.deb ...
Unpacking r-cran-survival (2.41-3-2build1) ...
Selecting previously unselected package r-cran-rpart.
Preparing to unpack .../33-r-cran-rpart_4.1-13-1_amd64.deb ...
Unpacking r-cran-rpart (4.1-13-1) ...
Selecting previously unselected package r-cran-class.
Preparing to unpack .../34-r-cran-class_7.3-14-2build1_amd64.deb ...
Unpacking r-cran-class (7.3-14-2build1) ...
Selecting previously unselected package r-cran-nnet.
Preparing to unpack .../35-r-cran-nnet_7.3-12-2build1_amd64.deb ...
Unpacking r-cran-nnet (7.3-12-2build1) ...
Selecting previously unselected package r-cran-spatial.
Preparing to unpack .../36-r-cran-spatial_7.3-11-2build1_amd64.deb ...
Unpacking r-cran-spatial (7.3-11-2build1) ...
Selecting previously unselected package r-cran-codetools.
Preparing to unpack .../37-r-cran-codetools_0.2-15-1.1_all.deb ...
Unpacking r-cran-codetools (0.2-15-1.1) ...
Selecting previously unselected package r-recommended.
Preparing to unpack .../38-r-recommended_3.4.4-1ubuntu1_all.deb ...
Unpacking r-recommended (3.4.4-1ubuntu1) ...
Selecting previously unselected package r-base.
Preparing to unpack .../39-r-base_3.4.4-1ubuntu1_all.deb ...
Unpacking r-base (3.4.4-1ubuntu1) ...
Selecting previously unselected package r-base-dev.
Preparing to unpack .../40-r-base-dev_3.4.4-1ubuntu1_all.deb ...
Unpacking r-base-dev (3.4.4-1ubuntu1) ...
Selecting previously unselected package r-doc-html.
Preparing to unpack .../41-r-doc-html_3.4.4-1ubuntu1_all.deb ...
Unpacking r-doc-html (3.4.4-1ubuntu1) ...
Selecting previously unselected package r-base-html.
Preparing to unpack .../42-r-base-html_3.4.4-1ubuntu1_all.deb ...
Unpacking r-base-html (3.4.4-1ubuntu1) ...
Setting up po-debconf (1.0.20) ...
Setting up libblas-dev:amd64 (3.7.1-4ubuntu1) ...
update-alternatives: using /usr/lib/x86_64-linux-gnu/blas/libblas.so to provide /usr/lib/x86_64-linux-gnu/libblas.so (libblas.so-x86_64-linux-gnu) in auto mode
Setting up intltool (0.51.0-5ubuntu1) ...
Setting up libonig4:amd64 (6.7.0-1) ...
Setting up r-base-core (3.4.4-1ubuntu1) ...

Creating config file /etc/R/Renviron with new version
Setting up libarchive-cpio-perl (0.10-1) ...
Setting up python3-scour (0.36-2) ...
Setting up scour (0.36-2) ...
Setting up r-cran-nnet (7.3-12-2build1) ...
Setting up libncurses5-dev:amd64 (6.1-1ubuntu1.18.04) ...
Setting up libsys-hostname-long-perl (1.5-1) ...
Setting up libjq1:amd64 (1.5+dfsg-2) ...
Setting up libmail-sendmail-perl (0.80-1) ...
Setting up r-base-html (3.4.4-1ubuntu1) ...
Setting up r-cran-spatial (7.3-11-2build1) ...
Setting up libgfortran-7-dev:amd64 (7.5.0-3ubuntu1~18.04) ...
Setting up gfortran-7 (7.5.0-3ubuntu1~18.04) ...
Setting up r-cran-mass (7.3-49-1) ...
Setting up r-cran-cluster (2.0.6-2build1) ...
Setting up r-doc-html (3.4.4-1ubuntu1) ...
Setting up libfile-stripnondeterminism-perl (0.040-1.1~build1) ...
Setting up liblapack-dev:amd64 (3.7.1-4ubuntu1) ...
update-alternatives: using /usr/lib/x86_64-linux-gnu/lapack/liblapack.so to provide /usr/lib/x86_64-linux-gnu/liblapack.so (liblapack.so-x86_64-linux-gnu) in auto mode
Setting up gfortran (4:7.4.0-1ubuntu2.3) ...
update-alternatives: using /usr/bin/gfortran to provide /usr/bin/f95 (f95) in auto mode
update-alternatives: using /usr/bin/gfortran to provide /usr/bin/f77 (f77) in auto mode
Setting up r-cran-boot (1.3-20-1.1) ...
Setting up jq (1.5+dfsg-2) ...
Setting up r-cran-codetools (0.2-15-1.1) ...
Setting up r-cran-lattice (0.20-35-1build1) ...
Setting up r-cran-nlme (3.1.131-3build1) ...
Setting up r-cran-foreign (0.8.69-1build1) ...
Setting up r-cran-class (7.3-14-2build1) ...
Setting up r-cran-kernsmooth (2.23-15-3build1) ...
Setting up r-cran-matrix (1.2-12-1) ...
Setting up r-cran-mgcv (1.8-23-1) ...
Setting up r-cran-survival (2.41-3-2build1) ...
Setting up r-cran-rpart (4.1-13-1) ...
Setting up r-recommended (3.4.4-1ubuntu1) ...
Setting up r-base (3.4.4-1ubuntu1) ...
Setting up dh-autoreconf (17) ...
Setting up dh-strip-nondeterminism (0.040-1.1~build1) ...
Setting up debhelper (11.1.6ubuntu2) ...
Setting up dh-translations (138.18.04.1) ...
Setting up cdbs (0.4.156ubuntu4) ...
Setting up r-base-dev (3.4.4-1ubuntu1) ...
Processing triggers for libc-bin (2.27-3ubuntu1.5) ...
/sbin/ldconfig.real: /usr/local/lib/libwx_gtk2u_ribbon-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_gtk2u_html-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_gtk2u_adv-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_gtk2u_aui-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libpialign.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_gtk2u_richtext-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_gtk2u_xrc-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_gtk2u_qa-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_baseu_net-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_baseu_xml-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_gtk2u_core-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_gtk2u_stc-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_gtk2u_gl-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_gtk2u_propgrid-3.0.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/liboll.so.0 is not a symbolic link

/sbin/ldconfig.real: /usr/local/lib/libwx_baseu-3.0.so.0 is not a symbolic link

Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
Processing triggers for gnome-menus (3.13.3-11ubuntu1.1) ...
Processing triggers for hicolor-icon-theme (0.17-2) ...
Processing triggers for ccache (3.4.1-1) ...
Updating symlinks in /usr/lib/ccache ...
Processing triggers for tex-common (6.09) ...
Running mktexlsr. This may take some time... done.
Processing triggers for mime-support (3.60ubuntu1) ...
Processing triggers for desktop-file-utils (0.23-1ubuntu3.18.04.2) ...
Processing triggers for install-info (6.5.0.dfsg.1-2) ...
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$
```

## Check R Version

```
(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$ R --version
R version 3.4.4 (2018-03-15) -- "Someone to Lean On"
Copyright (C) 2018 The R Foundation for Statistical Computing
Platform: x86_64-pc-linux-gnu (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under the terms of the
GNU General Public License versions 2 or 3.
For more information about these matters see
http://www.gnu.org/licenses/.

(base) ye@ykt-pro:/media/ye/project2/thazin-journal/pivot-journal/18Oct2021/TALLIP/error-bar-graph/draw-with-R$
```

## Run Example R Script

```

```


## References

- https://linuxize.com/post/how-to-install-r-on-ubuntu-20-04/
- https://www.digitalocean.com/community/tutorials/how-to-install-r-on-ubuntu-22-04
- https://askubuntu.com/questions/496788/you-have-held-broken-package-while-trying-to-install-r
- https://linuxpip.org/fix-unable-to-correct-problems-you-have-held-broken-packages/
- https://linuxconfig.org/install-r-on-ubuntu-18-04-bionic-beaver-linux

This reference helped me:  

- https://forums.linuxmint.com/viewtopic.php?t=297881



