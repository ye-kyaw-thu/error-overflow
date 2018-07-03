# How to Access iPhone Camera Photos on Ubuntu (16.04 LTS)

တကယ်လို့ iPhone ကိုသုံးရင် ဖုန်းနဲ့ရိုက်ထားတဲ့ ဓာတ်ပုံတွေကို HDD မှာ backup ကူးချင်တဲ့အခါမျိုးမှာ၊  
Ubuntu OS ကနေ iPhone အထဲက ဖိုလ်ဒါတွေကို access လုပ်နိုင်အောင် လုပ်ရမဲ့ အဆင့်တွေကတော့ အောက်ပါအတိုင်း ဖြစ်ပါတယ်။  

## Download "iphone-setup.sh" Program

အောက်ပါ PASTEBIN လင့်ခ်ကနေ "iphone-setup.sh" ပရိုဂရမ်ကို download လုပ်ယူနိုင်ပါတယ်။  

[https://pastebin.com/6u0TEhjz](https://pastebin.com/6u0TEhjz)

အဲဒီ "iphone-setup.sh" ပရိုဂရမ်ကတော့ iphone နဲ့ Ubuntu OS နှစ်ခုအကြား ချိတ်ဆက်ဖို့အတွက်၊ လိုအပ်တဲ့ library ဖိုင်တွေ (ဥပမာ libimobiledevice), library တွေကို install လုပ်တဲ့ အခါမှာလိုအပ်တဲ့ dependencies တွေကို ဒေါင်းလုဒ်လုပ်ပေးတာမျိုး၊ install လုပ်ပေးတာမျိုး အားလုံးကို လုပ်ပေးမဲ့ ဖိုင်ဖြစ်လို့ အရမ်းအထောက်အကူဖြစ်ပါတယ်။  
အထက်ပါ လင့်ခ်ကို access မလုပ်နိုင်တဲ့ အခါမျိုးအတွက် script တစ်ခုလုံးကို အောက်ပါအတိုင်း ကော်ပီကူးပေးထားပါတယ်။  

```bash
#!/bin/bash
zip_dir_name=""
function install_package () {
    ./autogen.sh
    make
    make install
}
 
function unzip_name () {
    d="`mktemp -d`"
    unzip -d "$d" "$1"
    zip_dir_name="`basename "$d"/*`"
    mv "$d"/"$zip_dir_name" "$zip_dir_name"
    rmdir "$d"
}
 
function download_package_cd () {
    echo $1
    RESULT=zip$RANDOM.zip
    wget -O $RESULT "$1"
    unzip_name $RESULT
    rm $RESULT
    cd $zip_dir_name
}
#Install everything (step 1)
apt-get -y install ideviceinstaller python-imobiledevice libimobiledevice-utils python-plist usbmuxd libtool autoconf automake libxml2-dev python-dev \
    libssl-dev
download_package_cd "https://github.com/libimobiledevice/libplist/archive/master.zip"
install_package
cd ..
download_package_cd "https://github.com/libimobiledevice/libusbmuxd/archive/master.zip"
install_package
cd ..
download_package_cd "https://github.com/libimobiledevice/libimobiledevice/archive/master.zip"
install_package
cd ..
apt-get -y remove usbmuxd
apt-get -y install libimobiledevice-dev libplist-dev libusb-dev libusb-1.0.0-dev libtool-bin libtool libfuse-dev
download_package_cd "https://github.com/libimobiledevice/usbmuxd/archive/master.zip"
install_package
cd ..
download_package_cd "https://github.com/libimobiledevice/ifuse/archive/master.zip"
./autogen.sh
./configure
make
make install
cd ..
#Create a mount point (step 3)
mkdir /media/iPhone
chmod 777 /media/iPhone
# Edit the fuse configuration file (step 4)
ALLOW_COMMENT_LINE=$(grep -n "# Allow non-root users to specify the allow_other or allow_root mount options." /etc/fuse.conf | grep -Eo '^[^:]+')
sed -i "$(($ALLOW_COMMENT_LINE+1))iuser_allow_other" /etc/fuse.conf
sed -i "$(($ALLOW_COMMENT_LINE+1))iop$" /etc/fuse.conf
```

## Running iphone-setup.sh

```
lar@lar-air:~/tool$ chmod +x ./iphone-setup.sh 
lar@lar-air:~/tool$ ex -bsc '%!awk "{sub(/\r/,\"\")}1"' -cx iphone_setup.sh
lar@lar-air:~/tool$ sudo ./iphone-setup.sh 
```

## Running "idevicepair" and "ifuse" commands

```
lar@lar-air:~$ mkdir ~/iphone/

lar@lar-air:~$ idevicepair pair
SUCCESS: Paired with device ec4c86554046aa2ad8751b79cce01131943b3407

lar@lar-air:~$ ifuse ~/iphone/

```

## Accessing iPhone Photos

```
lar@lar-air:~$ cd ~/iphone/

lar@lar-air:~/iphone$ ls
AirFair  Downloads       MediaAnalysis  PhotoStreamsData  Recordings
Books    FactoryLogs     PhotoData      Purchases
DCIM     iTunes_Control  Photos         Radio

lar@lar-air:~/iphone$ nautilus .
```

အောက်ပါအတိုင်း iPhone အထဲက ဖိုလ်ဒါတွေကို မြင်ရပါလိမ့်မယ်။  

<p align="center">
 <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/iphone_folders.png" alt="Folders of iPhone" width="797px" height="550px" /> 
</p>

DCIM ဖိုလ်ဒါအထဲကို ဝင်ပြီးတော့ ကိုယ်ကြည့်ချင်တဲ့ ဓာတ်ပုံတွေကို သိမ်းထားတဲ့ ဖိုလ်ဒါတစ်ခုခုကို ဖွင့်ကြည့်ရင်တော့ အောက်ပါကဲ့သို့သော ဓာတ်ပုံတွေကို မြင်ရပါလိမ့်မယ်။ အဲဒါဆိုရင် လိုချင်တဲ့ ဓာတ်ပုံတွေကို ဖိုလ်ဒါတစ်ခုခုဆီကို ကော်ပီကူးတာမျိုး၊ တခြား HDD တစ်လုံးဆီကို backup လုပ်တာမျိုး လုပ်လို့ ရပါပြီ။ :)  

<p align="center">
 <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/eg-photos-under-a-DCIM-folder.png" alt="Example photos" width="797px" height="550px" /> 
</p>


## Relating to Some Error Messages

idevicepair pair လုပ်စဉ်မှာ၊ တကယ်လို့ iphone ကနေ trust ဆိုတဲ့ button ကို မနှိပ်ပေးရသေးရင် အောက်ပါအတိုင်း error message ပေးပါလိမ့်မယ်။  

```
lar@lar-air:~$ idevicepair pair
ERROR: Please accept the trust dialog on the screen of device ec4c86554046aa2ad8751b79cce01131943b3407, then attempt to pair again.
```

တကယ်လို့ USB ကြိုးမချိတ်ထားခဲ့ရင် အောက်ပါအတိုင်း error message ပေးလိမ့်မယ်။

```
lar@lar-air:~$ idevicepair pair
No device found, is it plugged in?
```

iphone ဖိုလ်ဒါကို infuse နဲ့ ခေါ်ချိတ်တဲ့ အခါမှာ အောက်ပါအတိုင်း Permission denied ဆိုတဲ့ error message ကိုပေးနေရင်

```
lar@lar-air:~$ sudo ifuse ~/iphone/
[sudo] password for lar: 
There was an error accessing the mount point: Permission denied
```

sudo ခံပြီးမှ command ကို ရိုက်ပါ။  

```
lar@lar-air:~$ sudo umount ~/iphone/

lar@lar-air:~$ ifuse ~/iphone/
```

# Reference

[https://askubuntu.com/questions/928750/how-do-i-access-ios-camera-pictures-on-ubuntu-17-04](https://askubuntu.com/questions/928750/how-do-i-access-ios-camera-pictures-on-ubuntu-17-04)  
[How to access and mount iPhone 6 in Linux - Tutorial](https://www.dedoimedo.com/computers/linux-iphone-6.html)  
[On Ubuntu 16.04, since iOS 10 update, libimobiledevice can't connect to my iPhone. This is my attempt to document a fix.](https://gist.github.com/samrocketman/70dff6ebb18004fc37dc5e33c259a0fc)  
[https://askubuntu.com/questions/812006/how-can-i-mount-my-iphone-6s-on-ubuntu-16-04](https://askubuntu.com/questions/812006/how-can-i-mount-my-iphone-6s-on-ubuntu-16-04)  
