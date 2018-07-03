# How to Access iPhone Camera Photos on Ubuntu (16.04 LTS)

တကယ်လို့ iPhone ကိုသုံးရင် ဖုန်းနဲ့ရိုက်ထားတဲ့ ဓာတ်ပုံတွေကို HDD မှာ backup ကူးချင်တဲ့အခါမျိုးမှာ၊  
Ubuntu OS ကနေ iPhone အထဲက ဖိုလ်ဒါတွေကို access လုပ်နိုင်အောင် လုပ်ရမဲ့ အဆင့်တွေကတော့ အောက်ပါအတိုင်း ဖြစ်ပါတယ်။  

## Running iphone-setup.sh

```
lar@lar-air:~/tool$ chmod +x ./iphone-setup.sh 
lar@lar-air:~/tool$ ex -bsc '%!awk "{sub(/\r/,\"\")}1"' -cx iphone_setup.sh
lar@lar-air:~/tool$ sudo ./iphone-setup.sh 
```

## Running "idevicepair" and "ifuse" commands

```
(py3.6.2) lar@lar-air:~/student/nie/from/17jun2018$ idevicepair pair
SUCCESS: Paired with device ec4c86554046aa2ad8751b79cce01131943b3407

(py3.6.2) lar@lar-air:~/student/nie/from/17jun2018$ ifuse ~/iphone/

```

## Accessing iPhone Photos

```
(py3.6.2) lar@lar-air:~/student/nie/from/17jun2018$ cd ~/iphone/

(py3.6.2) lar@lar-air:~/iphone$ ls
AirFair  Downloads       MediaAnalysis  PhotoStreamsData  Recordings
Books    FactoryLogs     PhotoData      Purchases
DCIM     iTunes_Control  Photos         Radio

(py3.6.2) lar@lar-air:~/iphone$ nautilus .
```

## Relating to Some Error Messages

idevicepair pair လုပ်စဉ်မှာ၊ တကယ်လို့ iphone ကနေ trust ဆိုတဲ့ button ကို မနှိပ်ပေးရသေးရင် အောက်ပါအတိုင်း error message ပေးပါလိမ့်မယ်။  

```
(py3.6.2) lar@lar-air:~/student/nie/from/17jun2018$ idevicepair pair
ERROR: Please accept the trust dialog on the screen of device ec4c86554046aa2ad8751b79cce01131943b3407, then attempt to pair again.
```

တကယ်လို့ USB ကြိုးမချိတ်ထားခဲ့ရင် အောက်ပါအတိုင်း error message ပေးလိမ့်မယ်။

```
(py3.6.2) lar@lar-air:~/student/nie/from/17jun2018$ idevicepair pair
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
