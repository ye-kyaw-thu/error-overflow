# Installation of Required Packages for a New Ubuntu OS

လက်ရှိ သုံးနေတဲ့ ubuntu version က ...  

```
ye@ye-System-Product-Name:~$ lsb_release -a
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 22.04 LTS
Release:	22.04
Codename:	jammy
```

Ubuntu OS ကို စက်အသစ်မှာ installation လုပ်ပြီးသွားတဲ့အခါမှာ လုပ်လေ့ရှိတဲ့ installation step နဲ့ ပတ်သက်တဲ့ log ပါ။  
Default Ubuntu OS မှာက ကိုယ်လိုချင်တဲ့ library တို့ဘာတို့က အဆင်သင့် ရှိမနေပါဘူး။ အဲဒါကြောင့် ကိုယ့်ဖာသာကိုယ် customize လုပ်ရပါတယ်။  

```
sudo apt update && sudo apt upgrade -y  
```

## git

ကိုယ်မှာ GitHub account ရှိပြီးတော့ repository တွေနဲ့အလုပ်လုပ်ဖို့အတွက် လိုအပ်ပါတယ်။ တကယ်လို့ ကိုယ့်မှာ GitHub account မရှိရင်တောင်မှာ command line ကနေ တခြားသူတွေရဲ့ source code repository တစ်ခုခုကို clone လုပ်ဖို့အတွက် ($git clone) က install လုပ်ထားသင့်ပါတယ်။  


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
Get:2 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 git-man all 1:2.34.1-1ubuntu1.2 [952 kB]ye@ye-System-Product-Name:~$ sudo apt install curl
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libcurl4
The following NEW packages will be installed:
  curl
The following packages will be upgraded:
  libcurl4
1 upgraded, 1 newly installed, 0 to remove and 21 not upgraded.
Need to get 483 kB of archives.
After this operation, 452 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 libcurl4 amd64 7.81.0-1ubuntu1.1 [289 kB]
Get:2 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 curl amd64 7.81.0-1ubuntu1.1 [194 kB]
Fetched 483 kB in 1s (756 kB/s)
(Reading database ... 179956 files and directories currently installed.)
Preparing to unpack .../libcurl4_7.81.0-1ubuntu1.1_amd64.deb ...
Unpacking libcurl4:amd64 (7.81.0-1ubuntu1.1) over (7.81.0-1) ...
Selecting previously unselected package curl.
Preparing to unpack .../curl_7.81.0-1ubuntu1.1_amd64.deb ...
Unpacking curl (7.81.0-1ubuntu1.1) ...
Setting up libcurl4:amd64 (7.81.0-1ubuntu1.1) ...
Setting up curl (7.81.0-1ubuntu1.1) ...
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for libc-bin (2.35-0ubuntu3) ...
ye@ye-System-Product-Name:~$ curl --version
curl 7.81.0 (x86_64-pc-linux-gnu) libcurl/7.81.0 OpenSSL/3.0.2 zlib/1.2.11 brotli/1.0.9 zstd/1.4.8 libidn2/2.3.2 libpsl/0.21.0 (+libidn2/2.3.2) libssh/0.9.6/openssl/zlib nghttp2/1.43.0 librtmp/2.3 OpenLDAP/2.5.11
Release-Date: 2022-01-05
Protocols: dict file ftp ftps gopher gophers http https imap imaps ldap ldaps mqtt pop3 pop3s rtmp rtsp scp sftp smb smbs smtp smtps telnet tftp 
Features: alt-svc AsynchDNS brotli GSS-API HSTS HTTP2 HTTPS-proxy IDN IPv6 Kerberos Largefile libz NTLM NTLM_WB PSL SPNEGO SSL TLS-SRP UnixSockets zstd
ye@ye-System-Product-Name:~$
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

ပထမဆုံး run တဲ့အခါမှာ project path တို့ ဘာတို့ကို setup လုပ်ပေးရပါလိမ့်မယ်။  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/pycharm-1.png" alt="folder setup of PyCharm" width="800"/> </p>  
<div align="center">
  Fig. Folder and path setting for the PyCharm <br />
</div> 

<br />

ပြီးရင်တော့ coding လုပ်ဖို့အတွက် IDE interface တက်လာပါလိမ့်မယ်။  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/pycharm-2.png" alt="IDE of PyCharm" width="1200"/> </p>  
<div align="center">
  Fig. IDE of PyCharm <br />
</div> 

<br />

## curl

Wiki ကနေ အင်္ဂလိပ်လိုရှင်းထားတာကတော့...  
cURL is a command-line tool for getting or sending data including files using URL syntax.  

url ကနေတဆင့် ကိုယ့်စက်ထဲကို download လုပ်လို့ ရဖို့အတွက် curl tool ကို installation လုပ်မယ်ဆိုရင်...  

```
ye@ye-System-Product-Name:~$ sudo apt install curl
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libcurl4
The following NEW packages will be installed:
  curl
The following packages will be upgraded:
  libcurl4
1 upgraded, 1 newly installed, 0 to remove and 21 not upgraded.
Need to get 483 kB of archives.
After this operation, 452 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 libcurl4 amd64 7.81.0-1ubuntu1.1 [289 kB]
Get:2 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 curl amd64 7.81.0-1ubuntu1.1 [194 kB]
Fetched 483 kB in 1s (756 kB/s)
(Reading database ... 179956 files and directories currently installed.)
Preparing to unpack .../libcurl4_7.81.0-1ubuntu1.1_amd64.deb ...
Unpacking libcurl4:amd64 (7.81.0-1ubuntu1.1) over (7.81.0-1) ...
Selecting previously unselected package curl.
Preparing to unpack .../curl_7.81.0-1ubuntu1.1_amd64.deb ...
Unpacking curl (7.81.0-1ubuntu1.1) ...
Setting up libcurl4:amd64 (7.81.0-1ubuntu1.1) ...
Setting up curl (7.81.0-1ubuntu1.1) ...
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for libc-bin (2.35-0ubuntu3) ...
```

curl command ကို --version option နဲ့ ကိုခေါ်ပြီးတော့ installation ကို confirmation လုပ်ကြည့်ရအောင်...  

```
ye@ye-System-Product-Name:~$ curl --version
curl 7.81.0 (x86_64-pc-linux-gnu) libcurl/7.81.0 OpenSSL/3.0.2 zlib/1.2.11 brotli/1.0.9 zstd/1.4.8 libidn2/2.3.2 libpsl/0.21.0 (+libidn2/2.3.2) libssh/0.9.6/openssl/zlib nghttp2/1.43.0 librtmp/2.3 OpenLDAP/2.5.11
Release-Date: 2022-01-05
Protocols: dict file ftp ftps gopher gophers http https imap imaps ldap ldaps mqtt pop3 pop3s rtmp rtsp scp sftp smb smbs smtp smtps telnet tftp 
Features: alt-svc AsynchDNS brotli GSS-API HSTS HTTP2 HTTPS-proxy IDN IPv6 Kerberos Largefile libz NTLM NTLM_WB PSL SPNEGO SSL TLS-SRP UnixSockets zstd
ye@ye-System-Product-Name:~$
```

## java

လက်ရှိ စက်ထဲမှာ java က ရှိမနေသေးတာကို အောက်ပါအတိုင်း တွေ့ရပါလိမ့်မယ်။  

```
ye@ye-System-Product-Name:~$ java --version
Command 'java' not found, but can be installed with:
sudo apt install openjdk-11-jre-headless  # version 11.0.15+10-0ubuntu0.22.04.1, or
sudo apt install default-jre              # version 2:1.11-72build2
sudo apt install openjdk-17-jre-headless  # version 17.0.3+7-0ubuntu0.22.04.1
sudo apt install openjdk-18-jre-headless  # version 18~36ea-1
sudo apt install openjdk-8-jre-headless   # version 8u312-b07-0ubuntu1
ye@ye-System-Product-Name:~$
```

default Java Runtime Environment ကို install လုပ်ဖို့အတွက် ...  

```
ye@ye-System-Product-Name:~$ sudo apt install default-jre
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  ca-certificates-java default-jre-headless fonts-dejavu-extra java-common libatk-wrapper-java libatk-wrapper-java-jni openjdk-11-jre openjdk-11-jre-headless
Suggested packages:
  fonts-ipafont-gothic fonts-ipafont-mincho fonts-wqy-microhei | fonts-wqy-zenhei
The following NEW packages will be installed:
  ca-certificates-java default-jre default-jre-headless fonts-dejavu-extra java-common libatk-wrapper-java libatk-wrapper-java-jni openjdk-11-jre
  openjdk-11-jre-headless
0 upgraded, 9 newly installed, 0 to remove and 21 not upgraded.
Need to get 43.8 MB of archives.
After this operation, 180 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 java-common all 0.72build2 [6,782 B]
Get:2 http://th.archive.ubuntu.com/ubuntu jammye@ye-System-Product-Name:~$ java --version
openjdk 11.0.15 2022-04-19
OpenJDK Runtime Environment (build 11.0.15+10-Ubuntu-0ubuntu0.22.04.1)
OpenJDK 64-Bit Server VM (build 11.0.15+10-Ubuntu-0ubuntu0.22.04.1, mixed mode, sharing)
ye@ye-System-Product-Name:~$y-updates/main amd64 openjdk-11-jre-headless amd64 11.0.15+10-0ubuntu0.22.04.1 [41.5 MB]
Get:3 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 default-jre-headless amd64 2:1.11-72build2 [3,042 B]
Get:4 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 ca-certificates-java all 20190909 [12.1 kB]
Get:5 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 openjdk-11-jre amd64 11.0.15+10-0ubuntu0.22.04.1 [194 kB]
Get:6 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 default-jre amd64 2:1.11-72build2 [896 B]
Get:7 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 fonts-dejavu-extra all 2.37-2build1 [2,041 kB]
Get:8 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libatk-wrapper-java all 0.38.0-5build1 [53.1 kB]
Get:9 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libatk-wrapper-java-jni amd64 0.38.0-5build1 [49.0 kB]
Fetched 43.8 MB in 2s (27.6 MB/s)                  
Selecting previously unselected package java-common.
(Reading database ... 167859 files and directories currently installed.)
Preparing to unpack .../0-java-common_0.72build2_all.deb ...
Unpacking java-common (0.72build2) ...
Selecting previously unselected package openjdk-11-jre-headless:amd64.
Preparing to unpack .../1-openjdk-11-jre-headless_11.0.15+10-0ubuntu0.22.04.1_amd64.deb ...
Unpacking openjdk-11-jre-headless:amd64 (11.0.15+10-0ubuntu0.22.04.1) ...
Selecting previously unselected package default-jre-headless.
Preparing to unpack .../2-default-jre-headless_2%3a1.11-72build2_amd64.deb ...
Unpacking default-jre-headless (2:1.11-72build2) ...
Selecting previously unselected package ca-certificates-java.
Preparing to unpack .../3-ca-certificates-java_20190909_all.deb ...
Unpacking ca-certificates-java (20190909) ...
Selecting previously unselected package openjdk-11-jre:amd64.
Preparing to unpack .../4-openjdk-11-jre_11.0.15+10-0ubuntu0.22.04.1_amd64.deb ...
Unpacking openjdk-11-jre:amd64 (11.0.15+10-0ubuntu0.22.04.1) ...
Selecting previously unselected package default-jre.
Preparing to unpack .../5-default-jre_2%3a1.11-72build2_amd64.deb ...
Unpacking default-jre (2:1.11-72build2) ...
Selecting previously unselected package fonts-dejavu-extra.
Preparing to unpack .../6-fonts-dejavu-extra_2.37-2build1_all.deb ...
Unpacking fonts-dejavu-extra (2.37-2build1) ...
Selecting previously unselected package libatk-wrapper-java.
Preparing to unpack .../7-libatk-wrapper-java_0.38.0-5build1_all.deb ...
Unpacking libatk-wrapper-java (0.38.0-5build1) ...
Selecting previously unselected package libatk-wrapper-java-jni:amd64.
Preparing to unpack .../8-libatk-wrapper-java-jni_0.38.0-5build1_amd64.deb ...
Unpacking libatk-wrapper-java-jni:amd64 (0.38.0-5build1) ...
Setting up java-common (0.72build2) ...
Setting up fonts-dejavu-extra (2.37-2build1) ...
Setting up libatk-wrapper-java (0.38.0-5build1) ...
Setting up libatk-wrapper-java-jni:amd64 (0.38.0-5build1) ...
Setting up default-jre-headless (2:1.11-72build2) ...
Setting up openjdk-11-jre-headless:amd64 (11.0.15+10-0ubuntu0.22.04.1) ...
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/java to provide /usr/bin/java (java) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/jjs to provide /usr/bin/jjs (jjs) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/keytool to provide /usr/bin/keytool (keytool) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/rmid to provide /usr/bin/rmid (rmid) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/rmiregistry to provide /usr/bin/rmiregistry (rmiregistry) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/pack200 to provide /usr/bin/pack200 (pack200) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/unpack200 to provide /usr/bin/unpack200 (unpack200) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/lib/jexec to provide /usr/bin/jexec (jexec) in auto mode
Setting up openjdk-11-jre:amd64 (11.0.15+10-0ubuntu0.22.04.1) ...
Setting up default-jre (2:1.11-72build2) ...
Setting up ca-certificates-java (20190909) ...
head: cannot open '/etc/ssl/certs/java/cacerts' for reading: No such file or directory
Adding debian:Actalis_Authentication_Root_CA.pem
Adding debian:Hongkong_Post_Root_CA_3.pem
Adding debian:AC_RAIZ_FNMT-RCM_SERVIDORES_SEGUROS.pem
Adding debian:Hongkong_Post_Root_CA_1.pem
Adding debian:DigiCert_Assured_ID_Root_CA.pem
Adding debian:E-Tugra_Certification_Authority.pem
Adding debian:TWCA_Global_Root_CA.pem
Adding debian:UCA_Extended_Validation_Root.pem
Adding debian:GlobalSign_ECC_Root_CA_-_R4.pem
Adding debian:Amazon_Root_CA_4.pem
Adding debian:OISTE_WISeKey_Global_Root_GC_CA.pem
Adding debian:GlobalSign_Root_CA_-_R6.pem
Adding debian:QuoVadis_Root_CA_2.pem
Adding debian:CA_Disig_Root_R2.pem
Adding debian:TrustCor_RootCert_CA-1.pem
Adding debian:COMODO_ECC_Certification_Authority.pem
Adding debian:Trustwave_Global_ECC_P384_Certification_Authority.pem
Adding debian:GlobalSign_Root_E46.pem
Adding debian:Secure_Global_CA.pem
Adding debian:SSL.com_Root_Certification_Authority_ECC.pem
Adding debian:GlobalSign_Root_CA_-_R2.pem
Adding debian:GTS_Root_R1.pem
Adding debian:D-TRUST_Root_Class_3_CA_2_EV_2009.pem
Adding debian:DigiCert_High_Assurance_EV_Root_CA.pem
Adding debian:Go_Daddy_Root_Certificate_Authority_-_G2.pem
Adding debian:GTS_Root_R3.pem
Adding debian:ISRG_Root_X1.pem
Adding debian:ANF_Secure_Server_Root_CA.pem
Adding debian:USERTrust_RSA_Certification_Authority.pem
Adding debian:Security_Communication_Root_CA.pem
Adding debian:DigiCert_Global_Root_CA.pem
Adding debian:certSIGN_ROOT_CA.pem
Adding debian:USERTrust_ECC_Certification_Authority.pem
Adding debian:Certum_Trusted_Network_CA.pem
Adding debian:Amazon_Root_CA_3.pem
Adding debian:SecureTrust_CA.pem
Adding debian:GlobalSign_ECC_Root_CA_-_R5.pem
Adding debian:DigiCert_Assured_ID_Root_G3.pem
Adding debian:certSIGN_Root_CA_G2.pem
Adding debian:TUBITAK_Kamu_SM_SSL_Kok_Sertifikasi_-_Surum_1.pem
Adding debian:Entrust_Root_Certification_Authority_-_G4.pem
Adding debian:COMODO_Certification_Authority.pem
Adding debian:GDCA_TrustAUTH_R5_ROOT.pem
Adding debian:AffirmTrust_Premium.pem
Adding debian:Hellenic_Academic_and_Research_Institutions_RootCA_2015.pem
Adding debian:ssl-cert-snakeoil.pem
Adding debian:GTS_Root_R2.pem
Adding debian:Trustwave_Global_ECC_P256_Certification_Authority.pem
Adding debian:emSign_Root_CA_-_G1.pem
Adding debian:Comodo_AAA_Services_root.pem
Adding debian:T-TeleSec_GlobalRoot_Class_3.pem
Adding debian:DigiCert_Global_Root_G2.pem
Adding debian:e-Szigno_Root_CA_2017.pem
Adding debian:DigiCert_Global_Root_G3.pem
Adding debian:GlobalSign_Root_CA.pem
Adding debian:IdenTrust_Public_Sector_Root_CA_1.pem
Adding debian:GLOBALTRUST_2020.pem
Adding debian:GTS_Root_R4.pem
Adding debian:Starfield_Services_Root_Certificate_Authority_-_G2.pem
Adding debian:Network_Solutions_Certificate_Authority.pem
Adding debian:DigiCert_Assured_ID_Root_G2.pem
Adding debian:CFCA_EV_ROOT.pem
Adding debian:NetLock_Arany_=Class_Gold=_Főtanúsítvány.pem
Adding debian:COMODO_RSA_Certification_Authority.pem
Adding debian:Buypass_Class_3_Root_CA.pem
Adding debian:EC-ACC.pem
Adding debian:Cybertrust_Global_Root.pem
Adding debian:SSL.com_Root_Certification_Authority_RSA.pem
Adding debian:SwissSign_Gold_CA_-_G2.pem
Adding debian:SwissSign_Silver_CA_-_G2.pem
Adding debian:SZAFIR_ROOT_CA2.pem
Adding debian:Baltimore_CyberTrust_Root.pem
Adding debian:Entrust_Root_Certification_Authority_-_EC1.pem
Adding debian:Certum_Trusted_Network_CA_2.pem
Adding debian:Go_Daddy_Class_2_CA.pem
Adding debian:TeliaSonera_Root_CA_v1.pem
Adding debian:GlobalSign_Root_CA_-_R3.pem
Adding debian:QuoVadis_Root_CA_2_G3.pem
Adding debian:Entrust.net_Premium_2048_Secure_Server_CA.pem
Adding debian:Trustwave_Global_Certification_Authority.pem
Adding debian:emSign_Root_CA_-_C1.pem
Adding debian:emSign_ECC_Root_CA_-_C3.pem
Adding debian:XRamp_Global_CA_Root.pem
Adding debian:Amazon_Root_CA_2.pem
Adding debian:DigiCert_Trusted_Root_G4.pem
Adding debian:SSL.com_EV_Root_Certification_Authority_ECC.pem
Adding debian:AffirmTrust_Commercial.pem
Adding debian:GlobalSign_Root_R46.pem
Adding debian:TrustCor_ECA-1.pem
Adding debian:AffirmTrust_Premium_ECC.pem
Adding debian:Security_Communication_RootCA2.pem
Adding debian:AC_RAIZ_FNMT-RCM.pem
Adding debian:SecureSign_RootCA11.pem
Adding debian:Certum_Trusted_Root_CA.pem
Adding debian:TWCA_Root_Certification_Authority.pem
Adding debian:UCA_Global_G2_Root.pem
Adding debian:Certigna_Root_CA.pem
Adding debian:Starfield_Root_Certificate_Authority_-_G2.pem
Adding debian:D-TRUST_Root_Class_3_CA_2_2009.pem
Adding debian:Starfield_Class_2_CA.pem
Adding debian:Certigna.pem
Adding debian:Entrust_Root_Certification_Authority_-_G2.pem
Adding debian:QuoVadis_Root_CA_1_G3.pem
Adding debian:TrustCor_RootCert_CA-2.pem
Adding debian:emSign_ECC_Root_CA_-_G3.pem
Adding debian:ePKI_Root_Certification_Authority.pem
Adding debian:ACCVRAIZ1.pem
Adding debian:Entrust_Root_Certification_Authority.pem
Adding debian:Microsoft_ECC_Root_Certificate_Authority_2017.pem
Adding debian:Staat_der_Nederlanden_EV_Root_CA.pem
Adding debian:Izenpe.com.pem
Adding debian:T-TeleSec_GlobalRoot_Class_2.pem
Adding debian:IdenTrust_Commercial_Root_CA_1.pem
Adding debian:Microsec_e-Szigno_Root_CA_2009.pem
Adding debian:Atos_TrustedRoot_2011.pem
Adding debian:NAVER_Global_Root_Certification_Authority.pem
Adding debian:Certum_EC-384_CA.pem
Adding debian:Autoridad_de_Certificacion_Firmaprofesional_CIF_A62634068.pem
Adding debian:Hellenic_Academic_and_Research_Institutions_ECC_RootCA_2015.pem
Adding debian:QuoVadis_Root_CA_3_G3.pem
Adding debian:Amazon_Root_CA_1.pem
Adding debian:QuoVadis_Root_CA_3.pem
Adding debian:AffirmTrust_Networking.pem
Adding debian:Hellenic_Academic_and_Research_Institutions_RootCA_2011.pem
Adding debian:Microsoft_RSA_Root_Certificate_Authority_2017.pem
Adding debian:Buypass_Class_2_Root_CA.pem
Adding debian:OISTE_WISeKey_Global_Root_GB_CA.pem
Adding debian:SSL.com_EV_Root_Certification_Authority_RSA_R2.pem
done.
Processing triggers for mailcap (3.70+nmu1ubuntu1) ...
Processing triggers for fontconfig (2.13.1-4.2ubuntu5) ...
Processing triggers for desktop-file-utils (0.26-1ubuntu3) ...
Processing triggers for hicolor-icon-theme (0.17-2) ...
Processing triggers for gnome-menus (3.36.0-1ubuntu3) ...
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for ca-certificates (20211016) ...
Updating certificates in /etc/ssl/certs...
0 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d...

done.
done.
ye@ye-System-Product-Name:~$ye@ye-System-Product-Name:~$ java --version
openjdk 11.0.15 2022-04-19
OpenJDK Runtime Environment (build 11.0.15+10-Ubuntu-0ubuntu0.22.04.1)
OpenJDK 64-Bit Server VM (build 11.0.15+10-Ubuntu-0ubuntu0.22.04.1, mixed mode, sharing)
ye@ye-System-Product-Name:~$
```

သေချာအောင် Java version ကို ရိုက်ထုတ်ကြည့်ပြီး confirmation လုပ်ကြည့်ကြရအောင်...  

```
ye@ye-System-Product-Name:~$ java --version
openjdk 11.0.15 2022-04-19
OpenJDK Runtime Environment (build 11.0.15+10-Ubuntu-0ubuntu0.22.04.1)
OpenJDK 64-Bit Server VM (build 11.0.15+10-Ubuntu-0ubuntu0.22.04.1, mixed mode, sharing)
ye@ye-System-Product-Name:~$
```

ဒီအဆင့်ထိ ပြီးသွားရင် ကိုယ့်စက်ထဲမှာ java runtime environment ရှိသွားပြီမို့ java နဲ့ ရေးထားတဲ့ ပရိုဂရမ်တွေကို run လို့ ရပါပြီ။ တကယ်လို့ Java source code တွေကို compile လုပ်တာ၊ run တာကို လုပ်ချင်ရင်တော့ အောက်ပါ command ကို ရိုက်ထည့်ပြီး Java Development Kit (JDK) ကို installation လုပ်ယူပါ။  

```
ye@ye-System-Product-Name:~$ sudo apt install default-jdk
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  default-jdk-headless libice-dev libpthread-stubs0-dev libsm-dev libx11-dev libxau-dev libxcb1-dev libxdmcp-dev libxt-dev openjdk-11-jdk openjdk-11-jdk-headless
  x11proto-dev xorg-sgml-doctools xtrans-dev
Suggested packages:
  libice-doc libsm-doc libx11-doc libxcb-doc libxt-doc openjdk-11-demo openjdk-11-source visualvm
The following NEW packages will be installed:
  default-jdk default-jdk-headless libice-dev libpthread-stubs0-dev libsm-dev libx11-dev libxau-dev libxcb1-dev libxdmcp-dev libxt-dev openjdk-11-jdk
  openjdk-11-jdk-headless x11proto-dev xorg-sgml-doctools xtrans-dev
0 upgraded, 15 newly installed, 0 to remove and 21 not upgraded.
Need to get 218 MB of archives.
After this operation, 233 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 openjdk-11-jdk-headless amd64 11.0.15+10-0ubuntu0.22.04.1 [214 MB]
Get:2 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 default-jdk-headless amd64 2:1.11-72build2 [942 B]                                                          
Get:3 http://th.archive.ubuntu.com/ubuntu jammy-updates/main amd64 openjdk-11-jdk amd64 11.0.15+10-0ubuntu0.22.04.1 [2,569 kB]                                         
Get:4 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 default-jdk amd64 2:1.11-72build2 [908 B]                                                                   
Get:5 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 xorg-sgml-doctools all 1:1.11-1.1 [10.9 kB]                                                                 
Get:6 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 x11proto-dev all 2021.5-1 [604 kB]                                                                          
Get:7 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libice-dev amd64 2:1.0.10-1build2 [51.4 kB]                                                                 
Get:8 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libpthread-stubs0-dev amd64 0.4-1build2 [5,516 B]                                                           
Get:9 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libsm-dev amd64 2:1.2.3-1build2 [18.1 kB]                                                                   
Get:10 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libxau-dev amd64 1:1.0.9-1build5 [9,724 B]                                                                 
Get:11 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libxdmcp-dev amd64 1:1.1.3-0ubuntu5 [26.5 kB]                                                              
Get:12 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 xtrans-dev all 1.4.0-1 [68.9 kB]                                                                           
Get:13 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libxcb1-dev amd64 1.14-3ubuntu3 [86.5 kB]                                                                  
Get:14 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libx11-dev amd64 2:1.7.5-1 [744 kB]                                                                        
Get:15 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libxt-dev amd64 1:1.2.1-1 [396 kB]                                                                         
Fetched 218 MB in 23s (9,653 kB/s)                                                                                                                                     
Selecting previously unselected package openjdk-11-jdk-headless:amd64.
(Reading database ... 168268 files and directories currently installed.)
Preparing to unpack .../00-openjdk-11-jdk-headless_11.0.15+10-0ubuntu0.22.04.1_amd64.deb ...
Unpacking openjdk-11-jdk-headless:amd64 (11.0.15+10-0ubuntu0.22.04.1) ...
Selecting previously unselected package default-jdk-headless.
Preparing to unpack .../01-default-jdk-headless_2%3a1.11-72build2_amd64.deb ...
Unpacking default-jdk-headless (2:1.11-72build2) ...
Selecting previously unselected package openjdk-11-jdk:amd64.
Preparing to unpack .../02-openjdk-11-jdk_11.0.15+10-0ubuntu0.22.04.1_amd64.deb ...
Unpacking openjdk-11-jdk:amd64 (11.0.15+10-0ubuntu0.22.04.1) ...
Selecting previously unselected package default-jdk.
Preparing to unpack .../03-default-jdk_2%3a1.11-72build2_amd64.deb ...
Unpacking default-jdk (2:1.11-72build2) ...
Selecting previously unselected package xorg-sgml-doctools.
Preparing to unpack .../04-xorg-sgml-doctools_1%3a1.11-1.1_all.deb ...
Unpacking xorg-sgml-doctools (1:1.11-1.1) ...
Selecting previously unselected package x11proto-dev.
Preparing to unpack .../05-x11proto-dev_2021.5-1_all.deb ...
Unpacking x11proto-dev (2021.5-1) ...
Selecting previously unselected package libice-dev:amd64.
Preparing to unpack .../06-libice-dev_2%3a1.0.10-1build2_amd64.deb ...
Unpacking libice-dev:amd64 (2:1.0.10-1build2) ...
Selecting previously unselected package libpthread-stubs0-dev:amd64.
Preparing to unpack .../07-libpthread-stubs0-dev_0.4-1build2_amd64.deb ...
Unpacking libpthread-stubs0-dev:amd64 (0.4-1build2) ...
Selecting previously unselected package libsm-dev:amd64.
Preparing to unpack .../08-libsm-dev_2%3a1.2.3-1build2_amd64.deb ...
Unpacking libsm-dev:amd64 (2:1.2.3-1build2) ...
Selecting previously unselected package libxau-dev:amd64.
Preparing to unpack .../09-libxau-dev_1%3a1.0.9-1build5_amd64.deb ...
Unpacking libxau-dev:amd64 (1:1.0.9-1build5) ...
Selecting previously unselected package libxdmcp-dev:amd64.
Preparing to unpack .../10-libxdmcp-dev_1%3a1.1.3-0ubuntu5_amd64.deb ...
Unpacking libxdmcp-dev:amd64 (1:1.1.3-0ubuntu5) ...
Selecting previously unselected package xtrans-dev.
Preparing to unpack .../11-xtrans-dev_1.4.0-1_all.deb ...
Unpacking xtrans-dev (1.4.0-1) ...
Selecting previously unselected package libxcb1-dev:amd64.
Preparing to unpack .../12-libxcb1-dev_1.14-3ubuntu3_amd64.deb ...
Unpacking libxcb1-dev:amd64 (1.14-3ubuntu3) ...
Selecting previously unselected package libx11-dev:amd64.
Preparing to unpack .../13-libx11-dev_2%3a1.7.5-1_amd64.deb ...
Unpacking libx11-dev:amd64 (2:1.7.5-1) ...
Selecting previously unselected package libxt-dev:amd64.
Preparing to unpack .../14-libxt-dev_1%3a1.2.1-1_amd64.deb ...
Unpacking libxt-dev:amd64 (1:1.2.1-1) ...
Setting up openjdk-11-jdk-headless:amd64 (11.0.15+10-0ubuntu0.22.04.1) ...
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/jar to provide /usr/bin/jar (jar) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/jarsigner to provide /usr/bin/jarsigner (jarsigner) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/javac to provide /usr/bin/javac (javac) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/javadoc to provide /usr/bin/javadoc (javadoc) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/javap to provide /usr/bin/javap (javap) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/jcmd to provide /usr/bin/jcmd (jcmd) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/jdb to provide /usr/bin/jdb (jdb) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/jdeprscan to provide /usr/bin/jdeprscan (jdeprscan) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/jdeps to provide /usr/bin/jdeps (jdeps) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/jfr to provide /usr/bin/jfr (jfr) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/jimage to provide /usr/bin/jimage (jimage) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/jinfo to provide /usr/bin/jinfo (jinfo) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/jlink to provide /usr/bin/jlink (jlink) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/jmap to provide /usr/bin/jmap (jmap) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/jmod to provide /usr/bin/jmod (jmod) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/jps to provide /usr/bin/jps (jps) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/jrunscript to provide /usr/bin/jrunscript (jrunscript) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/jshell to provide /usr/bin/jshell (jshell) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/jstack to provide /usr/bin/jstack (jstack) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/jstat to provide /usr/bin/jstat (jstat) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/jstatd to provide /usr/bin/jstatd (jstatd) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/rmic to provide /usr/bin/rmic (rmic) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/serialver to provide /usr/bin/serialver (serialver) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/jaotc to provide /usr/bin/jaotc (jaotc) in auto mode
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/jhsdb to provide /usr/bin/jhsdb (jhsdb) in auto mode
Setting up libpthread-stubs0-dev:amd64 (0.4-1build2) ...
Setting up xtrans-dev (1.4.0-1) ...
Setting up default-jdk-headless (2:1.11-72build2) ...
Setting up openjdk-11-jdk:amd64 (11.0.15+10-0ubuntu0.22.04.1) ...
update-alternatives: using /usr/lib/jvm/java-11-openjdk-amd64/bin/jconsole to provide /usr/bin/jconsole (jconsole) in auto mode
Setting up xorg-sgml-doctools (1:1.11-1.1) ...
Setting up default-jdk (2:1.11-72build2) ...
Processing triggers for sgml-base (1.30) ...
Setting up x11proto-dev (2021.5-1) ...
Setting up libxau-dev:amd64 (1:1.0.9-1build5) ...
Setting up libice-dev:amd64 (2:1.0.10-1build2) ...
Setting up libsm-dev:amd64 (2:1.2.3-1build2) ...
Processing triggers for man-db (2.10.2-1) ...
Setting up libxdmcp-dev:amd64 (1:1.1.3-0ubuntu5) ...
Setting up libxcb1-dev:amd64 (1.14-3ubuntu3) ...
Setting up libx11-dev:amd64 (2:1.7.5-1) ...
Setting up libxt-dev:amd64 (1:1.2.1-1) ...
ye@ye-System-Product-Name:~
```

Java compiler ရဲ့ version ကို comfirm လုပ်ပါ။  

```
ye@ye-System-Product-Name:~$ javac --version
javac 11.0.15
```

help screen ကိုလည်း ခေါ်ကြည့်ရအောင်...  

```
ye@ye-System-Product-Name:~$ javac --help
Usage: javac <options> <source files>
where possible options include:
  @<filename>                  Read options and filenames from file
  -Akey[=value]                Options to pass to annotation processors
  --add-modules <module>(,<module>)*
        Root modules to resolve in addition to the initial modules, or all modules
        on the module path if <module> is ALL-MODULE-PATH.
  --boot-class-path <path>, -bootclasspath <path>
        Override location of bootstrap class files
  --class-path <path>, -classpath <path>, -cp <path>
        Specify where to find user class files and annotation processors
  -d <directory>               Specify where to place generated class files
  -deprecation
        Output source locations where deprecated APIs are used
  --enable-preview
        Enable preview language features. To be used in conjunction with either -source or --release.
  -encoding <encoding>         Specify character encoding used by source files
  -endorseddirs <dirs>         Override location of endorsed standards path
  -extdirs <dirs>              Override location of installed extensions
  -g                           Generate all debugging info
  -g:{lines,vars,source}       Generate only some debugging info
  -g:none                      Generate no debugging info
  -h <directory>
        Specify where to place generated native header files
  --help, -help, -?            Print this help message
  --help-extra, -X             Print help on extra options
  -implicit:{none,class}
        Specify whether or not to generate class files for implicitly referenced files
  -J<flag>                     Pass <flag> directly to the runtime system
  --limit-modules <module>(,<module>)*
        Limit the universe of observable modules
  --module <module-name>, -m <module-name>
        Compile only the specified module, check timestamps
  --module-path <path>, -p <path>
        Specify where to find application modules
  --module-source-path <module-source-path>
        Specify where to find input source files for multiple modules
  --module-version <version>
        Specify version of modules that are being compiled
  -nowarn                      Generate no warnings
  -parameters
        Generate metadata for reflection on method parameters
  -proc:{none,only}
        Control whether annotation processing and/or compilation is done.
  -processor <class1>[,<class2>,<class3>...]
        Names of the annotation processors to run; bypasses default discovery process
  --processor-module-path <path>
        Specify a module path where to find annotation processors
  --processor-path <path>, -processorpath <path>
        Specify where to find annotation processors
  -profile <profile>
        Check that API used is available in the specified profile
  --release <release>
        Compile for a specific VM version. Supported targets: 6, 7, 8, 9, 10, 11
  -s <directory>               Specify where to place generated source files
  -source <release>
        Provide source compatibility with specified release
  --source-path <path>, -sourcepath <path>
        Specify where to find input source files
  --system <jdk>|none          Override location of system modules
  -target <release>            Generate class files for specific VM version
  --upgrade-module-path <path>
        Override location of upgradeable modules
  -verbose                     Output messages about what the compiler is doing
  --version, -version          Version information
  -Werror                      Terminate compilation if warnings occur

ye@ye-System-Product-Name:~$
```

## Google Chrome Browser

Ubuntu မှာက FireFox browser က default ပါ။ တကယ်လို့ Google chrome browser ကို သုံးချင်တယ်ဆိုရင်တော့...  

```
sudo apt install -y chromium-browser
```

## Zoom

```
ye@ye-System-Product-Name:~$ wget https://zoom.us/client/latest/zoom_amd64.deb
--2022-04-29 11:58:03--  https://zoom.us/client/latest/zoom_amd64.deb
Resolving zoom.us (zoom.us)... 170.114.10.87
Connecting to zoom.us (zoom.us)|170.114.10.87|:443... connected.
HTTP request sent, awaiting response... 302 
Location: https://cdn.zoom.us/prod/5.10.4.2845/zoom_amd64.deb [following]
--2022-04-29 11:58:04--  https://cdn.zoom.us/prod/5.10.4.2845/zoom_amd64.deb
Resolving cdn.zoom.us (cdn.zoom.us)... 13.35.19.248
Connecting to cdn.zoom.us (cdn.zoom.us)|13.35.19.248|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 128995720 (123M) [binary/octet-stream]
Saving to: ‘zoom_amd64.deb’

zoom_amd64.deb                            100%[=====================================================================================>] 123.02M  37.3MB/s    in 3.3s    

2022-04-29 11:58:07 (37.3 MB/s) - ‘zoom_amd64.deb’ saved [128995720/128995720]

ye@ye-System-Product-Name:~$
```

```
ye@ye-System-Product-Name:~$ sudo apt install ./zoom_amd64.deb
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Note, selecting 'zoom' instead of './zoom_amd64.deb'
The following additional packages will be installed:
  libegl1-mesa libgl1-mesa-glx libxcb-xinerama0 libxcb-xtest0
The following NEW packages will be installed:
  libegl1-mesa libgl1-mesa-glx libxcb-xinerama0 libxcb-xtest0 zoom
0 upgraded, 5 newly installed, 0 to remove and 21 not upgraded.
Need to get 22.4 kB/129 MB of archives.
After this operation, 479 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 /home/ye/zoom_amd64.deb zoom amd64 5.10.4.2845 [129 MB]
Get:2 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libegl1-mesa amd64 22.0.1-1ubuntu2 [6,658 B]
Get:3 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libgl1-mesa-glx amd64 22.0.1-1ubuntu2 [5,456 B]
Get:4 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libxcb-xinerama0 amd64 1.14-3ubuntu3 [5,414 B]
Get:5 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libxcb-xtest0 amd64 1.14-3ubuntu3 [4,874 B]
Fetched 22.4 kB in 3s (6,445 B/s)         
Selecting previously unselected package libegl1-mesa:amd64.
(Reading database ... 169052 files and directories currently installed.)
Preparing to unpack .../libegl1-mesa_22.0.1-1ubuntu2_amd64.deb ...
Unpacking libegl1-mesa:amd64 (22.0.1-1ubuntu2) ...
Selecting previously unselected package libgl1-mesa-glx:amd64.
Preparing to unpack .../libgl1-mesa-glx_22.0.1-1ubuntu2_amd64.deb ...
Unpacking libgl1-mesa-glx:amd64 (22.0.1-1ubuntu2) ...
Selecting previously unselected package libxcb-xinerama0:amd64.
Preparing to unpack .../libxcb-xinerama0_1.14-3ubuntu3_amd64.deb ...
Unpacking libxcb-xinerama0:amd64 (1.14-3ubuntu3) ...
Selecting previously unselected package libxcb-xtest0:amd64.
Preparing to unpack .../libxcb-xtest0_1.14-3ubuntu3_amd64.deb ...
Unpacking libxcb-xtest0:amd64 (1.14-3ubuntu3) ...
Selecting previously unselected package zoom.
Preparing to unpack /home/ye/zoom_amd64.deb ...
Unpacking zoom (5.10.4.2845) ...
Setting up libegl1-mesa:amd64 (22.0.1-1ubuntu2) ...
Setting up libxcb-xinerama0:amd64 (1.14-3ubuntu3) ...
Setting up libxcb-xtest0:amd64 (1.14-3ubuntu3) ...
Setting up libgl1-mesa-glx:amd64 (22.0.1-1ubuntu2) ...
Setting up zoom (5.10.4.2845) ...
run post install script, action is configure...
Processing triggers for gnome-menus (3.36.0-1ubuntu3) ...
Processing triggers for libc-bin (2.35-0ubuntu3) ...
Processing triggers for shared-mime-info (2.1-2) ...
Processing triggers for mailcap (3.70+nmu1ubuntu1) ...
Processing triggers for desktop-file-utils (0.26-1ubuntu3) ...
N: Download is performed unsandboxed as root as file '/home/ye/zoom_amd64.deb' couldn't be accessed by user '_apt'. - pkgAcquire::Run (13: Permission denied)
ye@ye-System-Product-Name:~$
```

command prompt မှာ zoom ဆိုပြီး ရိုက်ထည့်ပြီး run လိုက်ရင် zoom program က တက်လာပါလိမ့်မယ်။ အောက်ပါလိုမျိုး screen နဲ့...  
  
<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/zoom-welcome-screen.png" alt="zoom program welcome screen" /> </p>  
<div align="center">
  Fig. Welcome screen of the Zoom video conferencing program <br />
</div> 

<br />

## gimp

gimp ကတော့ raster graphics editing software ဖြစ်ပြီးတော့ ဝယ်သုံးစရာမလိုတဲ့အပြင်၊ open-source ပါ။ ဓာတ်ပုံတွေ၊ ပုံတွေကို editing လုပ်ဖို့အတွက် အသုံးဝင်ပါတယ်။  

```
ye@ye-System-Product-Name:~$ sudo apt install gimp
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  gimp-data graphviz libamd2 libann0 libbabl-0.1-0 libcamd2 libccolamd2 libcdt5 libcgraph6 libcholmod3 libde265-0 libgegl-0.4-0 libgegl-common libgimp2.0 libgts-0.7-5
  libgts-bin libgvc6 libgvpr2 libheif1 libilmbase25 liblab-gamut1 libmetis5 libmng2 libmypaint-1.5-1 libmypaint-common libopenexr25 libpathplan4 libumfpack5
  libwmf0.2-7
Suggested packages:
  gimp-help-en | gimp-help gimp-data-extras gsfonts graphviz-doc
The following NEW packages will be installed:
  gimp gimp-data graphviz libamd2 libann0 libbabl-0.1-0 libcamd2 libccolamd2 libcdt5 libcgraph6 libcholmod3 libde265-0 libgegl-0.4-0 libgegl-common libgimp2.0
  libgts-0.7-5 libgts-bin libgvc6 libgvpr2 libheif1 libilmbase25 liblab-gamut1 libmetis5 libmng2 libmypaint-1.5-1 libmypaint-common libopenexr25 libpathplan4
  libumfpack5 libwmf0.2-7
0 upgraded, 30 newly installed, 0 to remove and 21 not upgraded.
Need to get 22.2 MB of archives.
After this operation, 110 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libbabl-0.1-0 amd64 1:0.1.92-1 [440 kB]
Get:2 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libilmbase25 amd64 2.5.7-2 [175 kB]
Get:3 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libopenexr25 amd64 2.5.7-1 [780 kB]
Get:4 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libamd2 amd64 1:5.10.1+dfsg-4build1 [21.6 kB]
Get:5 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libcamd2 amd64 1:5.10.1+dfsg-4build1 [23.3 kB]
Get:6 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libccolamd2 amd64 1:5.10.1+dfsg-4build1 [25.2 kB]
Get:7 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libmetis5 amd64 5.1.0.dfsg-7build2 [181 kB]
Get:8 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libcholmod3 amd64 1:5.10.1+dfsg-4build1 [346 kB]
Get:9 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libumfpack5 amd64 1:5.10.1+dfsg-4build1 [250 kB]
Get:10 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libgegl-common all 1:0.4.34-1build1 [866 kB]
Get:11 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libgegl-0.4-0 amd64 1:0.4.34-1build1 [1,392 kB]
Get:12 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libgimp2.0 amd64 2.10.30-1build1 [500 kB]
Get:13 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 gimp-data all 2.10.30-1build1 [7,633 kB]
Get:14 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libann0 amd64 1.1.2+doc-7build1 [26.0 kB]
Get:15 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libcdt5 amd64 2.42.2-6 [21.1 kB]
Get:16 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libcgraph6 amd64 2.42.2-6 [45.8 kB]
Get:17 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libgts-0.7-5 amd64 0.7.6+darcs121130-5 [164 kB]
Get:18 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libpathplan4 amd64 2.42.2-6 [23.5 kB]
Get:19 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libgvc6 amd64 2.42.2-6 [726 kB]
Get:20 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libgvpr2 amd64 2.42.2-6 [191 kB]
Get:21 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 liblab-gamut1 amd64 2.42.2-6 [1,964 kB]
Get:22 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 graphviz amd64 2.42.2-6 [650 kB]
Get:23 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libde265-0 amd64 1.0.8-1 [243 kB]
Get:24 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libheif1 amd64 1.12.0-2build1 [196 kB]
Get:25 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libmng2 amd64 2.0.3+dfsg-3 [168 kB]
Get:26 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libmypaint-common all 1.6.0-2 [140 kB]
Get:27 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libmypaint-1.5-1 amd64 1.6.0-2 [49.0 kB]
Get:28 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libwmf0.2-7 amd64 0.2.12-5ubuntu1 [14.0 kB]
Get:29 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 gimp amd64 2.10.30-1build1 [4,921 kB]
Get:30 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 libgts-bin amd64 0.7.6+darcs121130-5 [44.3 kB]
Fetched 22.2 MB in 2s (11.0 MB/s)      
Selecting previously unselected package libbabl-0.1-0:amd64.
(Reading database ... 170421 files and directories currently installed.)
Preparing to unpack .../00-libbabl-0.1-0_1%3a0.1.92-1_amd64.deb ...
Unpacking libbabl-0.1-0:amd64 (1:0.1.92-1) ...
Selecting previously unselected package libilmbase25:amd64.
Preparing to unpack .../01-libilmbase25_2.5.7-2_amd64.deb ...
Unpacking libilmbase25:amd64 (2.5.7-2) ...
Selecting previously unselected package libopenexr25:amd64.
Preparing to unpack .../02-libopenexr25_2.5.7-1_amd64.deb ...
Unpacking libopenexr25:amd64 (2.5.7-1) ...
Selecting previously unselected package libamd2:amd64.
Preparing to unpack .../03-libamd2_1%3a5.10.1+dfsg-4build1_amd64.deb ...
Unpacking libamd2:amd64 (1:5.10.1+dfsg-4build1) ...
Selecting previously unselected package libcamd2:amd64.
Preparing to unpack .../04-libcamd2_1%3a5.10.1+dfsg-4build1_amd64.deb ...
Unpacking libcamd2:amd64 (1:5.10.1+dfsg-4build1) ...
Selecting previously unselected package libccolamd2:amd64.
Preparing to unpack .../05-libccolamd2_1%3a5.10.1+dfsg-4build1_amd64.deb ...
Unpacking libccolamd2:amd64 (1:5.10.1+dfsg-4build1) ...
Selecting previously unselected package libmetis5:amd64.
Preparing to unpack .../06-libmetis5_5.1.0.dfsg-7build2_amd64.deb ...
Unpacking libmetis5:amd64 (5.1.0.dfsg-7build2) ...
Selecting previously unselected package libcholmod3:amd64.
Preparing to unpack .../07-libcholmod3_1%3a5.10.1+dfsg-4build1_amd64.deb ...
Unpacking libcholmod3:amd64 (1:5.10.1+dfsg-4build1) ...
Selecting previously unselected package libumfpack5:amd64.
Preparing to unpack .../08-libumfpack5_1%3a5.10.1+dfsg-4build1_amd64.deb ...
Unpacking libumfpack5:amd64 (1:5.10.1+dfsg-4build1) ...
Selecting previously unselected package libgegl-common.
Preparing to unpack .../09-libgegl-common_1%3a0.4.34-1build1_all.deb ...
Unpacking libgegl-common (1:0.4.34-1build1) ...
Selecting previously unselected package libgegl-0.4-0:amd64.
Preparing to unpack .../10-libgegl-0.4-0_1%3a0.4.34-1build1_amd64.deb ...
Unpacking libgegl-0.4-0:amd64 (1:0.4.34-1build1) ...
Selecting previously unselected package libgimp2.0:amd64.
Preparing to unpack .../11-libgimp2.0_2.10.30-1build1_amd64.deb ...
Unpacking libgimp2.0:amd64 (2.10.30-1build1) ...
Selecting previously unselected package gimp-data.
Preparing to unpack .../12-gimp-data_2.10.30-1build1_all.deb ...
Unpacking gimp-data (2.10.30-1build1) ...
Selecting previously unselected package libann0.
Preparing to unpack .../13-libann0_1.1.2+doc-7build1_amd64.deb ...
Unpacking libann0 (1.1.2+doc-7build1) ...
Selecting previously unselected package libcdt5:amd64.
Preparing to unpack .../14-libcdt5_2.42.2-6_amd64.deb ...
Unpacking libcdt5:amd64 (2.42.2-6) ...
Selecting previously unselected package libcgraph6:amd64.
Preparing to unpack .../15-libcgraph6_2.42.2-6_amd64.deb ...
Unpacking libcgraph6:amd64 (2.42.2-6) ...
Selecting previously unselected package libgts-0.7-5:amd64.
Preparing to unpack .../16-libgts-0.7-5_0.7.6+darcs121130-5_amd64.deb ...
Unpacking libgts-0.7-5:amd64 (0.7.6+darcs121130-5) ...
Selecting previously unselected package libpathplan4:amd64.
Preparing to unpack .../17-libpathplan4_2.42.2-6_amd64.deb ...
Unpacking libpathplan4:amd64 (2.42.2-6) ...
Selecting previously unselected package libgvc6.
Preparing to unpack .../18-libgvc6_2.42.2-6_amd64.deb ...
Unpacking libgvc6 (2.42.2-6) ...
Selecting previously unselected package libgvpr2:amd64.
Preparing to unpack .../19-libgvpr2_2.42.2-6_amd64.deb ...
Unpacking libgvpr2:amd64 (2.42.2-6) ...
Selecting previously unselected package liblab-gamut1:amd64.
Preparing to unpack .../20-liblab-gamut1_2.42.2-6_amd64.deb ...
Unpacking liblab-gamut1:amd64 (2.42.2-6) ...
Selecting previously unselected package graphviz.
Preparing to unpack .../21-graphviz_2.42.2-6_amd64.deb ...
Unpacking graphviz (2.42.2-6) ...
Selecting previously unselected package libde265-0:amd64.
Preparing to unpack .../22-libde265-0_1.0.8-1_amd64.deb ...
Unpacking libde265-0:amd64 (1.0.8-1) ...
Selecting previously unselected package libheif1:amd64.
Preparing to unpack .../23-libheif1_1.12.0-2build1_amd64.deb ...
Unpacking libheif1:amd64 (1.12.0-2build1) ...
Selecting previously unselected package libmng2:amd64.
Preparing to unpack .../24-libmng2_2.0.3+dfsg-3_amd64.deb ...
Unpacking libmng2:amd64 (2.0.3+dfsg-3) ...
Selecting previously unselected package libmypaint-common.
Preparing to unpack .../25-libmypaint-common_1.6.0-2_all.deb ...
Unpacking libmypaint-common (1.6.0-2) ...
Selecting previously unselected package libmypaint-1.5-1:amd64.
Preparing to unpack .../26-libmypaint-1.5-1_1.6.0-2_amd64.deb ...
Unpacking libmypaint-1.5-1:amd64 (1.6.0-2) ...
Selecting previously unselected package libwmf0.2-7:amd64.
Preparing to unpack .../27-libwmf0.2-7_0.2.12-5ubuntu1_amd64.deb ...
Unpacking libwmf0.2-7:amd64 (0.2.12-5ubuntu1) ...
Selecting previously unselected package gimp.
Preparing to unpack .../28-gimp_2.10.30-1build1_amd64.deb ...
Unpacking gimp (2.10.30-1build1) ...
Selecting previously unselected package libgts-bin.
Preparing to unpack .../29-libgts-bin_0.7.6+darcs121130-5_amd64.deb ...
Unpacking libgts-bin (0.7.6+darcs121130-5) ...
Setting up libamd2:amd64 (1:5.10.1+dfsg-4build1) ...
Setting up libmng2:amd64 (2.0.3+dfsg-3) ...
Setting up libmypaint-common (1.6.0-2) ...
Setting up libwmf0.2-7:amd64 (0.2.12-5ubuntu1) ...
Setting up libbabl-0.1-0:amd64 (1:0.1.92-1) ...
Setting up liblab-gamut1:amd64 (2.42.2-6) ...
Setting up libilmbase25:amd64 (2.5.7-2) ...
Setting up libmetis5:amd64 (5.1.0.dfsg-7build2) ...
Setting up libmypaint-1.5-1:amd64 (1.6.0-2) ...
Setting up libopenexr25:amd64 (2.5.7-1) ...
Setting up libgts-0.7-5:amd64 (0.7.6+darcs121130-5) ...
Setting up libcamd2:amd64 (1:5.10.1+dfsg-4build1) ...
Setting up libpathplan4:amd64 (2.42.2-6) ...
Setting up libann0 (1.1.2+doc-7build1) ...
Setting up gimp-data (2.10.30-1build1) ...
Setting up libccolamd2:amd64 (1:5.10.1+dfsg-4build1) ...
Setting up libgegl-common (1:0.4.34-1build1) ...
Setting up libcdt5:amd64 (2.42.2-6) ...
Setting up libcgraph6:amd64 (2.42.2-6) ...
Setting up libde265-0:amd64 (1.0.8-1) ...
Setting up libcholmod3:amd64 (1:5.10.1+dfsg-4build1) ...
Setting up libgts-bin (0.7.6+darcs121130-5) ...
Setting up libheif1:amd64 (1.12.0-2build1) ...
Setting up libumfpack5:amd64 (1:5.10.1+dfsg-4build1) ...
Setting up libgvc6 (2.42.2-6) ...
Setting up libgvpr2:amd64 (2.42.2-6) ...
Setting up libgegl-0.4-0:amd64 (1:0.4.34-1build1) ...
Setting up graphviz (2.42.2-6) ...
Setting up libgimp2.0:amd64 (2.10.30-1build1) ...
Setting up gimp (2.10.30-1build1) ...
Processing triggers for hicolor-icon-theme (0.17-2) ...
Processing triggers for gnome-menus (3.36.0-1ubuntu3) ...
Processing triggers for libc-bin (2.35-0ubuntu3) ...
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for mailcap (3.70+nmu1ubuntu1) ...
Processing triggers for desktop-file-utils (0.26-1ubuntu3) ...
ye@ye-System-Product-Name:~$
```

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/gimp-UI.png" alt="gimp UI" /> </p>  
<div align="center">
  Fig. User interface of the gimp (graphics editing software)<br />
</div> 

<br />

## telegram

telegram ကလည်း ကိုယ်ရောက်နေတဲ့နိုင်ငံ၊ ကိုယ်မှာရှိတဲ့ မိတ်ဆွေတွေရဲ့ အသုံးပြုမှုအပေါ်ကို မူတည်ပြီး လိုအပ်တတ်ပါတယ်။ ဥပမာ ကမ္ဘောဒီယားမှာ ဆိုရင် သူငယ်ချင်း အချင်းချင်း၊ ဆရာနဲ့တပည့်အကြား ဆက်သွယ်ဖို့အတွက်က telegram က အဓိက ကျပါတယ်။ ထိုနည်းလည်းကောင်း ထိုင်းနိုင်ငံမှာ ဆိုရင်တော့ LINE ကို အားထားပြီး သုံးကြပါတယ်။  

```
ye@ye-System-Product-Name:~$ sudo snap install telegram-desktop
[sudo] password for ye: 
telegram-desktop 3.7.3 from Telegram FZ-LLC (telegram.desktop) installed
ye@ye-System-Product-Name:~$
```

command line ကနေ run မယ်ဆိုရင်တော့  

```
telegram-desktop 
```

အဲဒါဆိုရင် အောက်ပါလိုမျိုး welcome screen ကို မြင်ရပါလိမ့်မယ်။  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/telegram-welcome-screen.png" alt="telegram Welcome Screen" /> </p>  
<div align="center">
  Fig. Welcome screen of telegram <br />
</div> 

<br />

telegram မှာ ပထမဆုံး သုံးဖို့အတွက် ဆိုရင်တော့ mobile phone နဲ့ QR code ကိုသုံးပြီး confirmation လုပ်ပြီးမှ login ဝင်လို့ ရပါလိမ့်မယ်။  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/telegram-login.png" alt="telegram Login Screen" /> </p>  
<div align="center">
  Fig. Login screen of telegram <br />
</div> 

<br />

## build-essential

Linux OS မှာ software တွေကို compile လုပ်ဖို့အတွက် နောက်ထပ် အရေးကြီးတာ တစ်ခုကတော့ build-essential ပါပဲ။ build-essential မှာ ပါဝင်တာတွေကတော့ GNU debugger, g++/GNU compiler collection တို့နဲ့တကွ compile လုပ်တဲ့အခါမှာလိုအပ်တဲ့ library တွေ tool (e.g. make tool) တွေပါပဲ။  

```
ye@ye-System-Product-Name:~$ sudo apt install build-essential
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  dpkg-dev fakeroot g++ g++-11 libalgorithm-diff-perl libalgorithm-diff-xs-perl libalgorithm-merge-perl libdpkg-perl libfakeroot
  libfile-fcntllock-perl libstdc++-11-dev lto-disabled-list
Suggested packages:
  debian-keyring g++-multilib g++-11-multilib gcc-11-doc bzr libstdc++-11-doc
The following NEW packages will be installed:
  build-essential dpkg-dev fakeroot g++ g++-11 libalgorithm-diff-perl libalgorithm-diff-xs-perl libalgorithm-merge-perl libdpkg-perl libfakeroot
  libfile-fcntllock-perl libstdc++-11-dev lto-disabled-list
0 upgraded, 13 newly installed, 0 to remove and 22 not upgraded.
Need to get 14.8 MB of archives.
After this operation, 54.4 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libstdc++-11-dev amd64 11.2.0-19ubuntu1 [2,083 kB]
Get:2 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 g++-11 amd64 11.2.0-19ubuntu1 [11.4 MB]
Get:3 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 g++ amd64 4:11.2.0-1ubuntu1 [1,412 B]
Get:4 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libdpkg-perl all 1.21.1ubuntu2 [236 kB]
Get:5 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 lto-disabled-list all 24 [12.5 kB]
Get:6 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 dpkg-dev all 1.21.1ubuntu2 [922 kB]
Get:7 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 build-essential amd64 12.9ubuntu3 [4,744 B]
Get:8 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libfakeroot amd64 1.28-1ubuntu1 [31.5 kB]
Get:9 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 fakeroot amd64 1.28-1ubuntu1 [60.4 kB]
Get:10 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libalgorithm-diff-perl all 1.201-1 [41.8 kB]
Get:11 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libalgorithm-diff-xs-perl amd64 0.04-6build3 [11.9 kB]
Get:12 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libalgorithm-merge-perl all 0.08-3 [12.0 kB]
Get:13 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libfile-fcntllock-perl amd64 0.22-3build7 [33.9 kB]
Fetched 14.8 MB in 1s (15.7 MB/s)                  
Selecting previously unselected package libstdc++-11-dev:amd64.
(Reading database ... 175388 files and directories currently installed.)
Preparing to unpack .../00-libstdc++-11-dev_11.2.0-19ubuntu1_amd64.deb ...
Unpacking libstdc++-11-dev:amd64 (11.2.0-19ubuntu1) ...
Selecting previously unselected package g++-11.
Preparing to unpack .../01-g++-11_11.2.0-19ubuntu1_amd64.deb ...
Unpacking g++-11 (11.2.0-19ubuntu1) ...
Selecting previously unselected package g++.
Preparing to unpack .../02-g++_4%3a11.2.0-1ubuntu1_amd64.deb ...
Unpacking g++ (4:11.2.0-1ubuntu1) ...
Selecting previously unselected package libdpkg-perl.
Preparing to unpack .../03-libdpkg-perl_1.21.1ubuntu2_all.deb ...
Unpacking libdpkg-perl (1.21.1ubuntu2) ...
Selecting previously unselected package lto-disabled-list.
Preparing to unpack .../04-lto-disabled-list_24_all.deb ...
Unpacking lto-disabled-list (24) ...
Selecting previously unselected package dpkg-dev.
Preparing to unpack .../05-dpkg-dev_1.21.1ubuntu2_all.deb ...
Unpacking dpkg-dev (1.21.1ubuntu2) ...
Selecting previously unselected package build-essential.
Preparing to unpack .../06-build-essential_12.9ubuntu3_amd64.deb ...
Unpacking build-essential (12.9ubuntu3) ...
Selecting previously unselected package libfakeroot:amd64.
Preparing to unpack .../07-libfakeroot_1.28-1ubuntu1_amd64.deb ...
Unpacking libfakeroot:amd64 (1.28-1ubuntu1) ...
Selecting previously unselected package fakeroot.
Preparing to unpack .../08-fakeroot_1.28-1ubuntu1_amd64ye@ye-System-Product-Name:~$ gcc --version
gcc (Ubuntu 11.2.0-19ubuntu1) 11.2.0
Copyright (C) 2021 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

ye@ye-System-Product-Name:~$.deb ...
Unpacking fakeroot (1.28-1ubuntu1) ...
Selecting previously unselected package libalgorithm-diff-perl.
Preparing to unpack .../09-libalgorithm-diff-perl_1.201-1_all.deb ...
Unpacking libalgorithm-diff-perl (1.201-1) ...
Selecting previously unselected package libalgorithm-diff-xs-perl.
Preparing to unpack .../10-libalgorithm-diff-xs-perl_0.04-6build3_amd64.deb ...
Unpacking libalgorithm-diff-xs-perl (0.04-6build3) ...
Selecting previously unselected package libalgorithm-merge-perl.
Preparing to unpack .../11-libalgorithm-merge-perl_0.08-3_all.deb ...
Unpacking libalgorithm-merge-perl (0.08-3) ...
Selecting previously unselected package libfile-fcntllock-perl.
Preparing to unpack .../12-libfile-fcntllock-perl_0.22-3build7_amd64.deb ...
Unpacking libfile-fcntllock-perl (0.22-3build7) ...
Setting up lto-disabled-list (24) ...
Setting up libfile-fcntllock-perl (0.22-3build7) ...
Setting up libalgorithm-diff-perl (1.201-1) ...
Setting up libfakeroot:amd64 (1.28-1ubuntu1) ...
Setting up fakeroot (1.28-1ubuntu1) ...
update-alternatives: using /usr/bin/fakeroot-sysv to provide /usr/bin/fakeroot (fakeroot) in auto mode
Setting up libdpkg-perl (1.21.1ubuntu2) ...
Setting up libstdc++-11-dev:amd64 (11.2.0-19ubuntu1) ...
Setting up libalgorithm-diff-xs-perl (0.04-6build3) ...
Setting up libalgorithm-merge-perl (0.08-3) ...
Setting up g++-11 (11.2.0-19ubuntu1) ...
Setting up dpkg-dev (1.21.1ubuntu2) ...
Setting up g++ (4:11.2.0-1ubuntu1) ...
update-alternatives: using /usr/bin/g++ to provide /usr/bin/c++ (c++) in auto mode
Setting up build-essential (12.9ubuntu3) ...
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for libc-bin (2.35-0ubuntu3) ...
ye@ye-System-Product-Name:~$
```

gcc version က ဘယ်လောက်လဲ ဆိုတာကို ကြည့်ရအောင်...  

```
ye@ye-System-Product-Name:~$ gcc --version
gcc (Ubuntu 11.2.0-19ubuntu1) 11.2.0
Copyright (C) 2021 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

ye@ye-System-Product-Name:~$
```

c ပရိုဂရမ် အသေးတစ်ပုဒ် ရေးပြီးတော့ hello.c အနေနဲ့ သိမ်းခဲ့တယ်။  

```
ye@ye-System-Product-Name:~$ vi hello.c
ye@ye-System-Product-Name:~$ cat hello.c
#include <stdio.h>

int main() {
    printf("နေကောင်းလား\n");
    return 0;
}
```

compile လုပ်ပြီး output filename ကို hello လို့ သတ်မှတ်ခဲ့တယ်။  

```
ye@ye-System-Product-Name:~$ gcc ./hello.c -o hello
```

coding မှာက အမှားအယွင်းမရှိရင် hello ဆိုတဲ့ executable program ကို output အနေနဲ့ ထုတ်ပေးပါလိမ့်မယ်။  

```
ye@ye-System-Product-Name:~$ ls hello*
hello  hello.c
```

run ကြည့်ရအောင် ...  

```
ye@ye-System-Product-Name:~$ ./hello
နေကောင်းလား
ye@ye-System-Product-Name:~$
```

## Check g++

```
(xnmt) ye@ye-System-Product-Name:~/tool/dynet-base$ g++ --version
g++ (Ubuntu 11.2.0-19ubuntu1) 11.2.0
Copyright (C) 2021 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

## vim

vim editor ကလည်း စသုံးစလူတွေအတွက် ခက်ပေမဲ့ linux သမားတွေ၊ ပရိုဂရမ်မာတွေအတွက်က powerful text editor တစ်ခုပါ။  

```
ye@ye-System-Product-Name:~$ sudo apt install vim
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  vim-runtime
Suggested packages:
  ctags vim-doc vim-scripts
The following NEW packages will be installed:
  vim vim-runtime
0 upgraded, 2 newly installed, 0 to remove and 22 not upgraded.
Need to get 8,548 kB of archives.
After this operation, 37.6 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 vim-runtime all 2:8.2.3995-1ubuntu2 [6,825 kB]
Get:2 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 vim amd64 2:8.2.3995-1ubuntu2 [1,724 kB]
Fetched 8,548 kB in 1s (9,041 kB/s)
Selecting previously unselected package vim-runtime.
(Reading database ... 176765 files and directories currently installed.)
Preparing to unpack .../vim-runtime_2%3a8.2.3995-1ubuntu2_all.deb ...
Adding 'diversion of /usr/share/vim/vim82/doc/help.txt to /usr/share/vim/vim82/doc/help.txt.vim-tiny by vim-runtime'
Adding 'diversion of /usr/share/vim/vim82/doc/tags to /usr/share/vim/vim82/doc/tags.vim-tiny by vim-runtime'
Unpacking vim-runtime (2:8.2.3995-1ubuntu2) ...
Selecting previously unselected package vim.
Preparing to unpack .../vim_2%3a8.2.3995-1ubuntu2_amd64.deb ...
Unpacking vim (2:8.2.3995-1ubuntu2) ...
Setting up vim-runtime (2:8.2.3995-1ubuntu2) ...
Setting up vim (2:8.2.3995-1ubuntu2) ...
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vim (vim) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vimdiff (vimdiff) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/rvim (rvim) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/rview (rview) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vi (vi) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/view (view) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/ex (ex) in auto mode
Processing triggers for man-db (2.10.2-1) ...
ye@ye-System-Product-Name:~$
```

installation လုပ်ပြီးတဲ့အခါမှာ command prompt ကနေ vim လို့ရိုက်ပြီးတော့ Enter ခေါက်လိုက်ရင် vim text editor တက်လာပါလိမ့်မယ်။  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/vim-text-editor-screen.png" alt="vim text editor Screen" /> </p>  
<div align="center">
  Fig. vim text editor <br />
</div> 

<br />

## python

NLP (Natural Language Processing), AI (Artificial Intelligence) နဲ့ ML (Machine Learning) သုတေသနလုပ်ကြတဲ့ သူတွေအတွက်က python programming က မရှိမဖြစ်ပါပဲ။ Ubuntu OS အသစ် install လုပ်လိုက်ရင် default အနေနဲ့ python2.7 နဲ့ python3 ရဲ့ version တစ်ခုခုကတော့ ပါလာတတ်ပြီးသားပါ။ ကိုယ်တိုင် လုပ်မယ် experimental setting ပေါ်ကိုမူတည်ပြီးတော့ လိုချင်တဲ့ သုံးချင်တဲ့ ဗားရှင်းကို ထပ်ထည့်တာမျိုး လုပ်ကြရပါတယ်။  

ကိုယ့်စက်ထဲမှာ ဘယ်လို python version တွေရှိနေသလဲ ဆိုတာကို သိချင်ရင် python လို့ ရိုက်ထည့်ပြီးတော့ TAB key ကိုနှိပ်လိုက်ရင် အောက်ပါလိုမျိုး အသေးစိတ် ပြပေးပါလိမ့်မယ်။  

```
ye@ye-System-Product-Name:~$ python
python2             python2.7           python3             python3.10          python3.8           python3-futurize    python3-pasteurize
```

python2 ကို ရိုက်လိုက်ရင် ဘယ် python2 ရဲ့ ဗားရှင်း (တနည်းအားဖြင့် detail version information) ကိုယူသုံးသွားမှာလဲ ဆိုတာကို အောက်ပါလိုမျိုး ဖော်ပြပေးပါလိမ့်မယ်။  

```
ye@ye-System-Product-Name:~$ python2 --version
Python 2.7.18
```

ထိုနည်းလည်းကောင်း python3 ရဲ့ ဗားရှင်းကိုလည်း အသေးစိတ်ကြည့်ကြည့်ရအောင်...  
(စက်တစ်လုံးနဲ့ တစ်လုံး တူမှာ မဟုတ်ဘူးနော်)  

```
ye@ye-System-Product-Name:~$ python3 --version
Python 3.10.4
```

## pip3

python library တွေကို installation လုပ်ဖို့အတွက်က pip3 (pip for Python3) က လိုအပ်ပါတယ်။  

```
Command 'pip3' not found, but can be installed with:
sudo apt install python3-pip
ye@ye-System-Product-Name:~$ sudo apt install python3-pip
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  javascript-common libexpat1-dev libjs-jquery libjs-sphinxdoc libjs-underscore libpython3-dev libpython3.10-dev python3-dev python3-distutils
  python3-setuptools python3-wheel python3.10-dev zlib1g-dev
Suggested packages:
  apache2 | lighttpd | httpd python-setuptools-doc
The following NEW packages will be installed:
  javascript-common libexpat1-dev libjs-jquery libjs-sphinxdoc libjs-underscore libpython3-dev libpython3.10-dev python3-dev python3-distutils
  python3-pip python3-setuptools python3-wheel python3.10-dev zlib1g-dev
0 upgraded, 14 newly installed, 0 to remove and 22 not upgraded.
Need to get 8,008 kB of archives.
After this operation, 34.1 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 javascript-common all 11+nmu1 [5,936 B]
Get:2 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libexpat1-dev amd64 2.4.7-1 [147 kB]
Get:3 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libjs-jquery all 3.6.0+dfsg+~3.5.13-1 [321 kB]
Get:4 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libjs-underscore all 1.13.2~dfsg-2 [118 kB]
Get:5 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libjs-sphinxdoc all 4.3.2-1 [139 kB]
Get:6 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 zlib1g-dev amd64 1:1.2.11.dfsg-2ubuntu9 [164 kB]
Get:7 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libpython3.10-dev amd64 3.10.4-3 [4,758 kB]
Get:8 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libpython3-dev amd64 3.10.4-0ubuntu2 [7,242 B]
Get:9 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 python3.10-dev amd64 3.10.4-3 [507 kB]
Get:10 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 python3-distutils all 3.10.4-0ubuntu1 [138 kB]
Get:11 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 python3-dev amd64 3.10.4-0ubuntu2 [26.0 kB]
Get:12 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 python3-setuptools all 59.6.0-1.2 [339 kB]
Get:13 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 python3-wheel all 0.37.1-2 [31.9 kB]
Get:14 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 python3-pip all 22.0.2+dfsg-1 [1,306 kB]
Fetched 8,008 kB in 0s (30.9 MB/s)      
Selecting previously unselected package javascript-common.
(Reading database ... 178706 files and directories currently installed.)
Preparing to unpack .../00-javascript-common_11+nmu1_all.deb ...
Unpacking javascript-common (11+nmu1) ...
Selecting previously unselected package libexpat1-dev:amd64.
Preparing to unpack .../01-libexpat1-dev_2.4.7-1_amd64.deb ...
Unpacking libexpat1-dev:amd64 (2.4.7-1) ...
Selecting previously unselected package libjs-jquery.
Preparing to unpack .../02-libjs-jquery_3.6.0+dfsg+~3.5.13-1_all.deb ...
Unpacking libjs-jquery (3.6.0+dfsg+~3.5.13-1) ...
Selecting previously unselected package libjs-underscore.
Preparing to unpack .../03-libjs-underscore_1.13.2~dfsg-2_all.deb ...
Unpacking libjs-underscore (1.13.2~dfsg-2) ...
Selecting previously unselected package libjs-sphinxdoc.
Preparing to unpack .../04-libjs-sphinxdoc_4.3.2-1_all.deb ...
Unpacking libjs-sphinxdoc (4.3.2-1) ...
Selecting previously unselected package zlib1g-dev:amd64.
Preparing to unpack .../05-zlib1g-dev_1%3a1.2.11.dfsg-2ubuntu9_amd64.deb ...
Unpacking zlib1g-dev:amd64 (1:1.2.11.dfsg-2ubuntu9) ...
Selecting previously unselected package libpython3.10-dev:amd64.
Preparing to unpack .../06-libpython3.10-dev_3.10.4-3_amd64.deb ...
Unpacking libpython3.10-dev:amd64 (3.10.4-3) ...
Selecting previously unselected package libpython3-dev:amd64.
Preparing to unpack .../07-libpython3-dev_3.10.4-0ubuntu2_amd64.deb ...
Unpacking libpython3-dev:amd64 (3.10.4-0ubuntu2) ...
Selecting previously unselected package python3.10-dev.
Preparing to unpack .../08-python3.10-dev_3.10.4-3_amd64.deb ...
Unpacking python3.10-dev (3.10.4-3) ...
Selecting previously unselected package python3-distutils.
Preparing to unpack .../09-python3-distutils_3.10.4-0ubuntu1_all.deb ...
Unpacking python3-distutils (3.10.4-0ubuntu1) ...
Selecting previously unselected package python3-dev.
Preparing to unpack .../10-python3-dev_3.10.4-0ubuntu2_amd64.deb ...
Unpacking python3-dev (3.10.4-0ubuntu2) ...
Selecting previously unselected package python3-setuptools.
Preparing to unpack .../11-python3-setuptools_59.6.0-1.2_all.deb ...
Unpacking python3-setuptools (59.6.0-1.2) ...
Selecting previously unselected package python3-wheel.
Preparing to unpack .../12-python3-wheel_0.37.1-2_all.deb ...
Unpacking python3-wheel (0.37.1-2) ...
Selecting previously unselected package python3-pip.
Preparing to unpack .../13-python3-pip_22.0.2+dfsg-1_all.deb ...
Unpacking python3-pip (22.0.2+dfsg-1) ...
Setting up python3-distutils (3.10.4-0ubuntu1) ...
Setting up javascript-common (11+nmu1) ...
Setting up python3-setuptools (59.6.0-1.2) ...
Setting up python3-wheel (0.37.1-2) ...
Setting up libexpat1-dev:amd64 (2.4.7-1) ...
Setting up python3-pip (22.0.2+dfsg-1) ...
Setting up zlib1g-dev:amd64 (1:1.2.11.dfsg-2ubuntu9) ...
Setting up libjs-jquery (3.6.0+dfsg+~3.5.13-1) ...
Setting up libjs-underscore (1.13.2~dfsg-2) ...
Setting up libpython3.10-dev:amd64 (3.10.4-3) ...
Setting up libjs-sphinxdoc (4.3.2-1) ...
Setting up python3.10-dev (3.10.4-3) ...
Setting up libpython3-dev:amd64 (3.10.4-0ubuntu2) ...
Setting up python3-dev (3.10.4-0ubuntu2) ...
Processing triggers for man-db (2.10.2-1) ...
ye@ye-System-Product-Name:~$
```

pip3 ရဲ့ ဗားရှင်းကို confirm လုပ်ကြည့်ရအောင်...  

```
ye@ye-System-Product-Name:~$ pip3 --version
pip 22.0.2 from /usr/lib/python3/dist-packages/pip (python 3.10)
ye@ye-System-Product-Name:~$
```

## pip (or) pip for Python2

Python2 အတွက် pip က default မှာ Ubuntu OS မှာ installation လုပ်မထားပါဘူး။  

```
ye@ye-System-Product-Name:~$ pip
pip                     pip3                    pip3.10                 pipewire                pipewire-media-session
```

curl command နဲ့ get-pip.py ဆိုတဲ့ script ကို ကိုယ့်စက်ထဲကို download လုပ်ရအောင်...  

```
ye@ye-System-Product-Name:~$ curl https://bootstrap.pypa.io/pip/2.7/get-pip.py --output get-pip.py
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 1863k  100 1863k    0     0  4235k      0 --:--:-- --:--:-- --:--:-- 4244k
ye@ye-System-Product-Name:~$
```

အထက်က curl နဲ့ download လုပ်ထားတဲ့ get-pip.py ဆိုတဲ့ script ကို python version 2 နဲ့ run ပြီး pip2 ကို download/install လုပ်ခိုင်းရအောင်...  

```
ye@ye-System-Product-Name:~$ sudo python2 get-pip.py
DEPRECATION: Python 2.7 reached the end of its life on January 1st, 2020. Please upgrade your Python as Python 2.7 is no longer maintained. pip 21.0 will drop support for Python 2.7 in January 2021. More details about Python 2 support in pip can be found at https://pip.pypa.io/en/latest/development/release-process/#python-2-support pip 21.0 will remove support for this functionality.
Collecting pip<21.0
  Downloading pip-20.3.4-py2.py3-none-any.whl (1.5 MB)
     |████████████████████████████████| 1.5 MB 1.8 MB/s 
Collecting setuptools<45
  Downloading setuptools-44.1.1-py2.py3-none-any.whl (583 kB)
     |████████████████████████████████| 583 kB 122.5 MB/s 
Collecting wheel
  Downloading wheel-0.37.1-py2.py3-none-any.whl (35 kB)
Installing collected packages: pip, setuptools, wheel
Successfully installed pip-20.3.4 setuptools-44.1.1 wheel-0.37.1
ye@ye-System-Product-Name:~$
```

pip2 command ကို --version option ပေးပြီးတော့ installation အဆင်ပြေပြေနဲ့ ပြီးသွားသလား ဆိုတာကို confirmation လုပ်ကြည့်ရအောင်...  

```
ye@ye-System-Product-Name:~$ pip2 --version
pip 20.3.4 from /usr/local/lib/python2.7/dist-packages/pip (python 2.7)
ye@ye-System-Product-Name:~$
```

## Anaconda

လက်ရှိ အချိန်အခါမှာ machine learning, data science စတဲ့ ပရောဂျက်တွေနဲ့ အလုပ်လုပ်နေတဲ့ သူတွေအနေနဲ့က virtual environment တစ်ခုခုကို installation လုပ်ထားဖို့ လိုအပ်ပါတယ်။ အဲ့ဒါကြောင့် Anaconda သို့မဟုတ် Virtualenv တစ်ခုခုကို installation လုပ်ဖို့ လိုအပ်ပါတယ်။ နှစ်ခုအနက် ဘယ်ဟာကိုသုံးမလဲ ဆိုတာကတော့ အောက်ပါအချက်အလက်တွေကို ကြည့်ပြီးတော့ ဆုံးဖြတ်ပါ။  

### Anaconda

- Data Science ပဲ လုပ်မယ်ဆိုရင် သင့်တော်တယ်
- လိုအပ်တဲ့ library တွေ အများစုက ပါပြီးသားပါ (Tensorflow, Numpy, Jupyter, Pandas, Matplotlib etc.)
- experiment လုပ်ဖို့သက်သက်၊ R&D အတွက်ဆိုရင် သင့်တော်တယ်
- HDD size နေရာတော့ ယူထက် (virtualenv ထက်စာရင် အများကြီး ယူတယ်)

### Virtualenv

- Frontend + Data Science တွဲလုပ်မယ် ဆိုရင် သင့်တော်တယ်
- Flask
- SQLAlchemy
- Ninja2
- Pandas
- Matplotlib

## Anaconda Installation 

folder အသစ်တစ်ခု ဆောက်ခဲ့...  

```
ye@ye-System-Product-Name:~/tool$ mkdir anaconda
ye@ye-System-Product-Name:~/tool$ cd anaconda/
```

wget command နဲ့ shell ဖိုင်ကို download လုပ်ယူ...  

```
ye@ye-System-Product-Name:~/tool/anaconda$ wget -P /tmp https://repo.anaconda.com/archive/Anaconda3-2020.02-Linux-x86_64.sh
--2022-04-30 12:55:33--  https://repo.anaconda.com/archive/Anaconda3-2020.02-Linux-x86_64.sh
Resolving repo.anaconda.com (repo.anaconda.com)... 104.16.131.3, 104.16.130.3, 2606:4700::6810:8303, ...
Connecting to repo.anaconda.com (repo.anaconda.com)|104.16.131.3|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 546910666 (522M) [application/x-sh]
Saving to: ‘/tmp/Anaconda3-2020.02-Linux-x86_64.sh’

Anaconda3-2020.02-Linux-x86_64.sh     100%[========================================================================>] 521.57M  15.7MB/s    in 35s     

2022-04-30 12:56:09 (14.7 MB/s) - ‘/tmp/Anaconda3-2020.02-Linux-x86_64.sh’ saved [546910666/546910666]

ye@ye-System-Product-Name:~/tool/anaconda$
```

checksum နံပါတ်ကို ထုတ်ကြည့်ပြီး ဒေါင်းလုပ်လုပ်ခဲ့စဉ်က error ရှိမရှိ detect လုပ်ကြည့်.... (ဒီအဆင့်က optional ပါ)  

```
ye@ye-System-Product-Name:~/tool/anaconda$ sha256sum /tmp/Anaconda3-2020.02-Linux-x86_64.sh
2b9f088b2022edb474915d9f69a803d6449d5fdb4c303041f60ac4aefcc208bb  /tmp/Anaconda3-2020.02-Linux-x86_64.sh
ye@ye-System-Product-Name:~/tool/anaconda$
```

installation လုပ်ဖို့ shell script ကို run ...  

```
ye@ye-System-Product-Name:~/tool/anaconda$ bash /tmp/Anaconda3-2020.02-Linux-x86_64.sh

Welcome to Anaconda3 2020.02

In order to continue the installation process, please review the license
agreement.
Please, press ENTER to continue
>>>
```

installation လုပ်မှာ သေချာရင် ENTER key ကိုခေါက်ပါ။ အဲဒါဆိုရင် လိုင်စင်နဲ့ ပတ်သက်တဲ့ အချက်အလက်တွေကို အောက်ပါအတိုင်း မြင်ရလိမ့်မယ်။  

```
===================================
End User License Agreement - Anaconda Individual Edition
===================================

Copyright 2015-2020, Anaconda, Inc.

All rights reserved under the 3-clause BSD License:

This End User License Agreement (the "Agreement") is a legal agreement between you and Anaconda, Inc. ("Anaconda") and governs your use of Anaconda Ind
ividual Edition (which was formerly known as Anaconda Distribution).

Subject to the terms of this Agreement, Anaconda hereby grants you a non-exclusive, non-transferable license to:

  * Install and use the Anaconda Individual Edition (which was formerly known as Anaconda Distribution),
  * Modify and create derivative works of sample source code delivered in Anaconda Individual Edition; and
  * Redistribute code files in source (if provided to you by Anaconda as source) and binary forms, with or without modification subject to the requirem
ents set forth below.

Anaconda may, at its option, make available patches, workarounds or other updates to Anaconda Individual Edition. Unless the updates are provided with 
their separate governing terms, they are deemed part of Anaconda Individual Edition licensed to you as provided in this Agreement.  This Agreement does
 not entitle you to any support for Anaconda Individual Edition.

Anaconda reserves all rights not expressly granted to you in this Agreement.

Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:

  * Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.
  * Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation
 and/or other materials provided with the distribution.
  * Neither the name of Anaconda nor the names of its contributors may be used to endorse or promote products derived from this software without specif
ic prior written permission.

You acknowledge that, as between you and Anaconda, Anaconda owns all right, title, and interest, including all intellectual property rights, in and to 
Anaconda Individual Edition and, with respect to third-party products distributed with or in Anaconda Individual Edition, the applicable third-party li
censors own all right, title and interest, including all intellectual property rights, in and to such products.  If you send or transmit any communicat
ions or materials to Anaconda suggesting or recommending changes to the software or documentation, including without limitation, new features or functi
--More--

```

လိုင်စင်နဲ့ ပတ်သက်တာကို page down လုပ်သွားပြီးရင် yes ကိုရွေးပါ  

```
Do you accept the license terms? [yes|no]
[no] >>> yes
```

yes နှိပ်ပြီးရင်... installation လုပ်မယ့် path ကိုဆုံးဖြတ်ပါ။ သူပြထားတဲ့ default path အတိုင်းပဲ installation လုပ်မယ်ဆိုရင်တော့ ENTER ကို နှိပ်ပါ။  
```
Anaconda3 will now be installed into this location:
/home/ye/anaconda3

  - Press ENTER to confirm the location
  - Press CTRL-C to abort the installation
  - Or specify a different location below

[/home/ye/anaconda3] >>>
```

ENTER နှိပ်လိုက်ရင်...  

```
[/home/ye/anaconda3] >>> 
PREFIX=/home/ye/anaconda3
Unpacking payload ...
Collecting package metadata (current_repodata.json): done                                                                                              
Solving environment: done

## Package Plan ##

  environment location: /home/ye/anaconda3

  added / updated specs:
    - _ipyw_jlab_nb_ext_conf==0.1.0=py37_0
    - _libgcc_mutex==0.1=main
    - alabaster==0.7.12=py37_0
    - anaconda-client==1.7.2=py37_0
    - anaconda-navigator==1.9.12=py37_0
    - anaconda-project==0.8.4=py_0
    - anaconda==2020.02=py37_0
    - argh==0.26.2=py37_0
    - asn1crypto==1.3.0=py37_0
    - astroid==2.3.3=py37_0
    - astropy==4.0=py37h7b6447c_0
    - atomicwrites==1.3.0=py37_1
    - attrs==19.3.0=py_0
    - autopep8==1.4.4=py_0
    - babel==2.8.0=py_0
    - backcall==0.1.0=py37_0
    - backports.functools_lru_cache==1.6.1=py_0
    - backports.shutil_get_terminal_size==1.0.0=py37_2
    - backports.tempfile==1.0=py_1
    - backports.weakref==1.0.post1=py_1
    - backports==1.0=py_2

...
...
...
  xmltodict          pkgs/main/noarch::xmltodict-0.12.0-py_0
  xz                 pkgs/main/linux-64::xz-5.2.4-h14c3975_4
  yaml               pkgs/main/linux-64::yaml-0.1.7-had09818_2
  yapf               pkgs/main/noarch::yapf-0.28.0-py_0
  zeromq             pkgs/main/linux-64::zeromq-4.3.1-he6710b0_3
  zict               pkgs/main/noarch::zict-1.0.0-py_0
  zipp               pkgs/main/noarch::zipp-2.2.0-py_0
  zlib               pkgs/main/linux-64::zlib-1.2.11-h7b6447c_3
  zstd               pkgs/main/linux-64::zstd-1.3.7-h0b5b093_0


Preparing transaction: done
Executing transaction: done
installation finished.
Do you wish the installer to initialize Anaconda3
by running conda init? [yes|no]
[no] >>> yes
no change     /home/ye/anaconda3/condabin/conda
no change     /home/ye/anaconda3/bin/conda
no change     /home/ye/anaconda3/bin/conda-env
no change     /home/ye/anaconda3/bin/activate
no change     /home/ye/anaconda3/bin/deactivate
no change     /home/ye/anaconda3/etc/profile.d/conda.sh
no change     /home/ye/anaconda3/etc/fish/conf.d/conda.fish
no change     /home/ye/anaconda3/shell/condabin/Conda.psm1
no change     /home/ye/anaconda3/shell/condabin/conda-hook.ps1
no change     /home/ye/anaconda3/lib/python3.7/site-packages/xontrib/conda.xsh
no change     /home/ye/anaconda3/etc/profile.d/conda.csh
modified      /home/ye/.bashrc

==> For changes to take effect, close and re-open your current shell. <==

If you'd prefer that conda's base environment not be activated on startup, 
   set the auto_activate_base parameter to false: 

conda config --set auto_activate_base false

Thank you for installing Anaconda3!

===========================================================================

Anaconda and JetBrains are working together to bring you Anaconda-powered
environments tightly integrated in the PyCharm IDE.
[/home/ye/anaconda3] >>> 
PREFIX=/home/ye/anaconda3
Unpacking payload ...
Collecting package metadata (current_repodata.json): done                                                                                              
Solving environment: done

## Package Plan ##

  environment location: /home/ye/anaconda3

  added / updated specs:
    - _ipyw_jlab_nb_ext_conf==0.1.0=py37_0
    - _libgcc_mutex==0.1=main
    - alabaster==0.7.12=py37_0
    - anaconda-client==1.7.2=py37_0
    - anaconda-navigator==1.9.12=py37_0
    - anaconda-project==0.8.4=py_0
    - anaconda==2020.02=py37_0
    - argh==0.26.2=py37_0
    - asn1crypto==1.3.0=py37_0
    - astroid==2.3.3=py37_0
    - astropy==4.0=py37h7b6447c_0
    - atomicwrites==1.3.0=py37_1
    - attrs==19.3.0=py_0
    - autopep8==1.4.4=py_0
    - babel==2.8.0=py_0
    - backcall==0.1.0=py37_0
    - backports.functools_lru_cache==1.6.1=py_0
    - backports.shutil_get_terminal_size==1.0.0=py37_2
    - backports.tempfile==1.0=py_1
    - backports.weakref==1.0.post1=py_1
    - backports==1.0=py_2

PyCharm for Anaconda is available at:
https://www.anaconda.com/pycharm

ye@ye-System-Product-Name:~/tool/anaconda$
```

activate လုပ်ကြည့်ရအောင်...  

```
ye@ye-System-Product-Name:~/tool/anaconda$ source ~/.bashrc
(base) ye@ye-System-Product-Name:~/tool/anaconda$
```

conda command ရဲ့ help ကို ခေါ်ကြည့်ပြီး installation ကို confirm လုပ်ရအောင်။  

```
(base) ye@ye-System-Product-Name:~/tool/anaconda$ conda --help
usage: conda [-h] [-V] command ...

conda is a tool for managing and deploying applications, environments and packages.

Options:

positional arguments:
  command
    clean        Remove unused packages and caches.
    config       Modify configuration values in .condarc. This is modeled
                 after the git config command. Writes to the user .condarc
                 file (/home/ye/.condarc) by default.
    create       Create a new conda environment from a list of specified
                 packages.
    help         Displays a list of available conda commands and their help
                 strings.
    info         Display information about current conda install.
    init         Initialize conda for shell interaction. [Experimental]
    install      Installs a list of packages into a specified conda
                 environment.
    list         List linked packages in a conda environment.
    package      Low-level conda package utility. (EXPERIMENTAL)
    remove       Remove a list of packages from a specified conda environment.
    uninstall    Alias for conda remove.
    run          Run an executable in a conda environment. [Experimental]
    search       Search for packages and display associated information. The
                 input is a MatchSpec, a query language for conda packages.
                 See examples below.
    update       Updates conda packages to the latest compatible version.
    upgrade      Alias for conda update.

optional arguments:
  -h, --help     Show this help message and exit.
  -V, --version  Show the conda version number and exit.

conda commands available from other packages:
  build
  convert
  debug
  develop
  env
  index
  inspect
  metapackage
  render
  server
  skeleton
  verify
(base) ye@ye-System-Product-Name:~/tool/anaconda$
```

update လုပ်မယ်...  

```
(base) ye@ye-System-Product-Name:~/tool/anaconda$ conda update --all
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/ye/anaconda3


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    _ipyw_jlab_nb_ext_conf-0.1.0|   py37h06a4308_1           5 KB
    backports.functools_lru_cache-1.6.4|     pyhd3eb1b0_0           9 KB
    backports.tempfile-1.0     |     pyhd3eb1b0_1          11 KB
    conda-4.12.0               |   py37h06a4308_0        14.5 MB
    conda-build-3.21.8         |   py37h06a4308_2         547 KB
    conda-package-handling-1.8.1|   py37h7f8727e_0         889 KB
    navigator-updater-0.2.1    |           py37_1         687 KB
    xmltodict-0.12.0           |     pyhd3eb1b0_0          13 KB
    ------------------------------------------------------------
                                           Total:        16.6 MB

The following packages will be UPDATED:

  _ipyw_jlab_nb_ext~                           0.1.0-py37_0 --> 0.1.0-py37h06a4308_1
  backports.functoo~                             1.6.1-py_0 --> 1.6.4-pyhd3eb1b0_0
  conda                                        4.8.2-py37_0 --> 4.12.0-py37h06a4308_0
  conda-build                                3.18.11-py37_0 --> 3.21.8-py37h06a4308_2
  conda-package-han~                   1.6.0-py37h7b6447c_0 --> 1.8.1-py37h7f8727e_0
  navigator-updater                            0.2.1-py37_0 --> 0.2.1-py37_1

The following packages will be DOWNGRADED:

  backports.tempfile                               1.0-py_1 --> 1.0-pyhd3eb1b0_1
  xmltodict                                     0.12.0-py_0 --> 0.12.0-pyhd3eb1b0_0


Proceed ([y]/n)? 
Downloading and Extracting Packages
_ipyw_jlab_nb_ext_co | 5 KB      | ############################################################################################################ | 100% 
navigator-updater-0. | 687 KB    | ############################################################################################################ | 100% 
conda-package-handli | 889 KB    | ############################################################################################################ | 100% 
backports.functools_ | 9 KB      | ############################################################################################################ | 100% 
backports.tempfile-1 | 11 KB     | ############################################################################################################ | 100% 
conda-build-3.21.8   | 547 KB    | ############################################################################################################ | 100% 
conda-4.12.0         | 14.5 MB   | ############################################################################################################ | 100% 
xmltodict-0.12.0     | 13 KB     | ############################################################################################################ | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(base) ye@ye-System-Product-Name:~/tool/anaconda$
```


## jupyter notebook

Jupyter notebook က အရမ်းအသုံးဝင်တဲ့ web-browser ကို အခြေခံထားတဲ့ IDE ပါ။ Python programming တစ်မျိုးတည်း မဟုတ်ပဲ၊ တခြား programming language တွေကိုလည်း support လုပ်ပါတယ်။ ပြီးတော့ linux command တွေကိုလည်း jupyter notebook cell တွေထဲကနေ ခေါ်run လို့ရလို့ အရမ်းအဆင်ပြေပါတယ်။ program running output တစ်ခုတည်းသာမကပဲ matplotlib တို့ကိုသုံးပြီး graph ဆွဲတာတို့လုပ်ပြီး code နဲ့တကွ တွဲသိမ်းထားလို့ ရတာကြောင့် demo လုပ်တဲ့အခါမျိုးတွေ၊ စာသင်တဲ့အခါမျိုးတွေအတွက်လည်း အသုံးဝင်ပါတယ်။  

Ubuntu OS အသစ် installation လုပ်ထားတဲ့စက်မှာ jupyter notebook က မရှိသေးပါဘူး...  

```
ye@ye-System-Product-Name:~$ jupyter
Command 'jupyter' not found, but can be installed with:
sudo snap install jupyter       # version 1.0.0, or
sudo apt  install jupyter-core  # version 4.9.1-1
See 'snap info jupyter' for additional versions.
ye@ye-System-Product-Name:~$ 
```

သို့သော် အထက်ကလိုမျိုး Anaconda ကို installation လုပ်ပြီးသွားရင်တော့ Jupyter notebook လည်း ခေါ် run လို့ ရပါပြီ။  

```
(base) ye@ye-System-Product-Name:~/tool/anaconda$ jupyter notebook
```

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/jupyter-IDE.png" alt="UI of Jupyter Notebook" /> </p>  
<div align="center">
  Fig. UI of Jupyter Notebook <br />
</div> 

<br />

## emacs

Linux သမားတွေ၊ programmer တွေထဲမှာ emacs ကို ချစ်တဲ့သူတွေ အများကြီးပါ။ လေ့လာလို့ မကုန်နိုင်အောင်ပဲလို့ အပြောများကြပါတယ်။ သုံးရင်းလေ့လာ၊ လေ့လာရင်းသုံး သွားရတဲ့ ပုံစံပါ။ ပြောရရင် text editor ဆိုတာထက် operating system တစ်ခုလိုပါပဲ...   

command line ကနေပဲ emacs ကို installation လုပ်မယ်ဆိုရင်တော့ အောက်ပါအတိုင်းပါ။  

```
(base) ye@ye-System-Product-Name:~/tool/anaconda$ sudo apt install emacs
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  emacs-bin-common emacs-common emacs-el emacs-gtk libm17n-0 libotf1 m17n-db
Suggested packages:
  mailutils emacs-common-non-dfsg ncurses-term m17n-docs gawk
The following NEW packages will be installed:
  emacs emacs-bin-common emacs-common emacs-el emacs-gtk libm17n-0 libotf1 m17n-db
0 upgraded, 8 newly installed, 0 to remove and 22 not upgraded.
Need to get 36.4 MB of archives.
After this operation, 117 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 emacs-common all 1:27.1+1-3ubuntu5 [14.6 MB]
Get:2 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 emacs-bin-common amd64 1:27.1+1-3ubuntu5 [133 kB]
Get:3 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 m17n-db all 1.8.0-3 [1,215 kB]
Get:4 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libotf1 amd64 0.9.16-3build1 [49.7 kB]
Get:5 http://th.archive.ubuntu.com/ubuntu jammy/main amd64 libm17n-0 amd64 1.8.0-4 [267 kB]
Get:6 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 emacs-gtk amd64 1:27.1+1-3ubuntu5 [3,956 kB]
Get:7 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 emacs all 1:27.1+1-3ubuntu5 [13.3 kB]
Get:8 http://th.archive.ubuntu.com/ubuntu jammy/universe amd64 emacs-el all 1:27.1+1-3ubuntu5 [16.1 MB]
Fetched 36.4 MB in 1s (24.5 MB/s)    
Selecting previously unselected package emacs-common.
(Reading database ... 179963 files and directories currently installed.)
Preparing to unpack .../0-emacs-common_1%3a27.1+1-3ubuntu5_all.deb ...
Unpacking emacs-common (1:27.1+1-3ubuntu5) ...
Selecting previously unselected package emacs-bin-common.
Preparing to unpack .../1-emacs-bin-common_1%3a27.1+1-3ubuntu5_amd64.deb ...
Unpacking emacs-bin-common (1:27.1+1-3ubuntu5) ...
Selecting previously unselected package m17n-db.
Preparing to unpack .../2-m17n-db_1.8.0-3_all.deb ...
Unpacking m17n-db (1.8.0-3) ...
Selecting previously unselected package libotf1:amd64.
Preparing to unpack .../3-libotf1_0.9.16-3build1_amd64.deb ...
Unpacking libotf1:amd64 (0.9.16-3build1) ...
Selecting previously unselected package libm17n-0:amd64.
Preparing to unpack .../4-libm17n-0_1.8.0-4_amd64.deb ...
Unpacking libm17n-0:amd64 (1.8.0-4) ...
Selecting previously unselected package emacs-gtk.
Preparing to unpack .../5-emacs-gtk_1%3a27.1+1-3ubuntu5_amd64.deb ...
Unpacking emacs-gtk (1:27.1+1-3ubuntu5) ...
Selecting previously unselected package emacs.
Preparing to unpack .../6-emacs_1%3a27.1+1-3ubuntu5_all.deb ...
Unpacking emacs (1:27.1+1-3ubuntu5) ...
Selecting previously unselected package emacs-el.
Preparing to unpack .../7-emacs-el_1%3a27.1+1-3ubuntu5_all.deb ...
Unpacking emacs-el (1:27.1+1-3ubuntu5) ...
Setting up libotf1:amd64 (0.9.16-3build1) ...
Setting up m17n-db (1.8.0-3) ...
Setting up libm17n-0:amd64 (1.8.0-4) ...
Setting up emacs-common (1:27.1+1-3ubuntu5) ...
Setting up emacs-el (1:27.1+1-3ubuntu5) ...
Setting up emacs-bin-common (1:27.1+1-3ubuntu5) ...
update-alternatives: using /usr/bin/ctags.emacs to provide /usr/bin/ctags (ctags) in auto mode
update-alternatives: using /usr/bin/ebrowse.emacs to provide /usr/bin/ebrowse (ebrowse) in auto mode
update-alternatives: using /usr/bin/emacsclient.emacs to provide /usr/bin/emacsclient (emacsclient) in auto mode
update-alternatives: using /usr/bin/etags.emacs to provide /usr/bin/etags (etags) in auto mode
Setting up emacs-gtk (1:27.1+1-3ubuntu5) ...
update-alternatives: using /usr/bin/emacs-gtk to provide /usr/bin/emacs (emacs) in auto mode
Install emacsen-common for emacs
emacsen-common: Handling install of emacsen flavor emacs
Install dictionaries-common for emacs
install/dictionaries-common: Byte-compiling for emacsen flavour emacs
Setting up emacs (1:27.1+1-3ubuntu5) ...
Processing triggers for hicolor-icon-theme (0.17-2) ...
Processing triggers for gnome-menus (3.36.0-1ubuntu3) ...
Processing triggers for libc-bin (2.35-0ubuntu3) ...
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for install-info (6.8-4build1) ...
Processing triggers for mailcap (3.70+nmu1ubuntu1) ...
Processing triggers for desktop-file-utils (0.26-1ubuntu3) ...
(base) ye@ye-System-Product-Name:~/tool/anaconda$
```

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/UI-of-emacs.png" alt="UI of emacs" /> </p>  
<div align="center">
  Fig. UI of emacs text editor <br />
</div> 

<br />


## Reference

- https://blog.jetbrains.com/pycharm/2017/09/pycharm-community-edition-and-professional-edition-explained-licenses-and-more/  
- https://en.wikipedia.org/wiki/CURL  
- https://linuxize.com/post/how-to-install-pip-on-ubuntu-20.04/  
- https://stackoverflow.com/questions/38217545/what-is-the-difference-between-pyenv-virtualenv-anaconda
- https://dataaspirant.com/anaconda-python-virtualenv/

