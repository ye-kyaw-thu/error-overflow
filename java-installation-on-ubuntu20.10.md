## No Java Yet

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ java --version
Command 'java' not found, but can be installed with:
sudo apt install default-jre              # version 2:1.11-72, or
sudo apt install openjdk-11-jre-headless  # version 11.0.9.1+1-0ubuntu1~20.10
sudo apt install openjdk-13-jre-headless  # version 13.0.4+8-1
sudo apt install openjdk-14-jre-headless  # version 14.0.2+12-1
sudo apt install openjdk-15-jre-headless  # version 15+36-1
sudo apt install openjdk-8-jre-headless   # version 8u275-b01-0ubuntu1~20.10
```

## Install Java

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ sudo apt install default-jdk
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  ca-certificates-java default-jdk-headless default-jre default-jre-headless fonts-dejavu-extra java-common libatk-wrapper-java libatk-wrapper-java-jni libice-dev
  libpthread-stubs0-dev libsm-dev libx11-dev libxau-dev libxcb1-dev libxdmcp-dev libxt-dev openjdk-11-jdk openjdk-11-jdk-headless openjdk-11-jre openjdk-11-jre-headless
  x11proto-core-dev x11proto-dev xorg-sgml-doctools xtrans-dev
Suggested packages:
  libice-doc libsm-doc libx11-doc libxcb-doc libxt-doc openjdk-11-demo openjdk-11-source visualvm fonts-ipafont-gothic fonts-ipafont-mincho fonts-wqy-microhei | fonts-wqy-zenhei
The following NEW packages will be installed:
  ca-certificates-java default-jdk default-jdk-headless default-jre default-jre-headless fonts-dejavu-extra java-common libatk-wrapper-java libatk-wrapper-java-jni libice-dev
  libpthread-stubs0-dev libsm-dev libx11-dev libxau-dev libxcb1-dev libxdmcp-dev libxt-dev openjdk-11-jdk openjdk-11-jdk-headless openjdk-11-jre openjdk-11-jre-headless
  x11proto-core-dev x11proto-dev xorg-sgml-doctools xtrans-dev
0 upgraded, 25 newly installed, 0 to remove and 13 not upgraded.
Need to get 270 MB of archives.
After this operation, 425 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 java-common all 0.72 [6,816 B]
Get:2 http://mm.archive.ubuntu.com/ubuntu groovy-updates/main amd64 openjdk-11-jre-headless amd64 11.0.9.1+1-0ubuntu1~20.10 [37.8 MB]
Get:3 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 default-jre-headless amd64 2:1.11-72 [3,192 B]                  
...
...
...
Adding debian:DigiCert_Assured_ID_Root_G2.pem
Adding debian:TWCA_Root_Certification_Authority.pem
Adding debian:AC_RAIZ_FNMT-RCM.pem
done.
Setting up default-jdk (2:1.11-72) ...
Processing triggers for man-db (2.9.3-2) ...
Processing triggers for ca-certificates (20201027ubuntu0.20.10.1) ...
Updating certificates in /etc/ssl/certs...
0 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d...

done.
done.
Processing triggers for sgml-base (1.30) ...
Setting up x11proto-dev (2020.1-1) ...
Processing triggers for fontconfig (2.13.1-2ubuntu3) ...
Processing triggers for desktop-file-utils (0.24-1ubuntu4) ...
Processing triggers for mime-support (3.64ubuntu1) ...
Setting up libxau-dev:amd64 (1:1.0.9-0ubuntu1) ...
Processing triggers for hicolor-icon-theme (0.17-2) ...
Setting up libice-dev:amd64 (2:1.0.10-1) ...
Processing triggers for gnome-menus (3.36.0-1ubuntu1) ...
Setting up libsm-dev:amd64 (2:1.2.3-1) ...
Setting up libxdmcp-dev:amd64 (1:1.1.3-0ubuntu1) ...
Setting up x11proto-core-dev (2020.1-1) ...
Setting up libxcb1-dev:amd64 (1.14-2) ...
Setting up libx11-dev:amd64 (2:1.6.12-1) ...
Setting up libxt-dev:amd64 (1:1.2.0-1) ...
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$
```

## Check Java Version

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ java --version
openjdk 11.0.9.1 2020-11-04
OpenJDK Runtime Environment (build 11.0.9.1+1-Ubuntu-0ubuntu1.20.10)
OpenJDK 64-Bit Server VM (build 11.0.9.1+1-Ubuntu-0ubuntu1.20.10, mixed mode, sharing)
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$
```
