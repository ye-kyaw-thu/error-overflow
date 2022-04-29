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

## Reference

- https://blog.jetbrains.com/pycharm/2017/09/pycharm-community-edition-and-professional-edition-explained-licenses-and-more/

