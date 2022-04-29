# Installation of Required Packages for a New Ubuntu OS

Ubuntu OS ကို စက်အသစ်မှာ installation လုပ်ပြီးသွားတဲ့အခါမှာ လုပ်လေ့ရှိတဲ့ installation step နဲ့ ပတ်သက်တဲ့ log ပါ။  
Default Ubuntu OS မှာက ကိုယ်လိုချင်တဲ့ library တို့ဘာတို့က အဆင်သင့် ရှိမနေပါဘူး။ အဲဒါကြောင့် ကိုယ့်ဖာသာကိုယ် customize လုပ်ရပါတယ်။  

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

ပထမဆုံး run တဲ့အခါမှာ project path တို့ ဘာတို့ကို setup လုပ်ပေးရပါလိမ့်မယ်။  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/pycharm-1.png" alt="folder setup of PyCharm" width="800"/> </p>  
<div align="center">
  Fig. Folder and path setting for the PyCharm <br />
</div> 

<br />

ပြီးရင်တော့ coding လုပ်ဖို့အတွက် IDE interface တက်လာပါလိမ့်မယ်။  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/pycharm-2.png" alt="folder setup of PyCharm" width="1200"/> </p>  
<div align="center">
  Fig. IDE of PyCharm <br />
</div> 

<br />

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



## Reference

- https://blog.jetbrains.com/pycharm/2017/09/pycharm-community-edition-and-professional-edition-explained-licenses-and-more/

