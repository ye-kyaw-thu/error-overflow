# LibreOffice (soffice) Crashing When I Start

Date: 2 July 2018

# In English:

For some reasons, LibreOffice crushed.   
I removed and re-install LibreOffice but keep crushing when I run.  

How to solve:  
Rename LibreOffice user profile.  
On Ubuntu:  
cd /home/YOUR_USER_ID/.config/libreoffice/4  

And then, change foldername user to user.old as follows:  
mv user user.old  

Start LibreOffice:  
soffice  

# In Myanmar Language:  

LibreOffice က တရက်မှာသုံးနေရင်းနဲ့ crash ဖြစ်သွားပြီးတော့၊  စာသင်ဖို့အတွက် presentation slide ပြင်ဖို့ Impress presentation ဖိုင်တစ်ဖိုင်ကို ဖွင့်လိုက်တိုင်းမှာ အောက်ပါ အတိုင်း အရင်ဖွင့်ခဲ့တဲ့ ဖိုင်တစ်ဖိုင်ကို recover လုပ်မလားမေးတဲ့ dialog box ပေါ်လာပြီး၊ OK button ကို နှိပ်လိုက်ရင် LibreOffice က တက်မလာတော့ပါဘူး။  

Discard Recovery Data ကို ရွေးလည်း အတူတူပါပဲ။ LibreOffice က တက်မလာပါဘူး။ Impress presentation slide ဖိုင်သာမက၊ တခြား Writer Document, Calc Spreadsheet ဖိုင်တွေကို ဖွင့်လို့လည်းမရဖြစ်နေတဲ့ အခြေအနေပါ။   

<p align="center">
 <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/LibreOffice-Error.png" alt="Error" width="552px" height="428px" /> 
</p>

အဲဒါနဲ့ LibreOffice ကို အောက်ပါအတိုင်း uninstall လုပ်လိုက်ပါတယ်။  

```
   $ sudo apt-get remove --purge libreoffice*

   $ sudo apt-get clean

   $ sudo apt-get autoremove

```

ပြီးတော့ အောက်ပါအတိုင်း install ပြန်လုပ်ခဲ့ပါတယ်။  
(အင်တာနက် ချိတ်ဆက်ထားရပါမယ်)  

```
   $ sudo apt-get install libreoffice | tee libreoffice-installation.log
```

ဒါပေမဲ့ command prompt မှာ ``` $ soffice ``` ရိုက်ပြီး ဖွင့်လိုက်တိုင်းမှာ အထက်မှာ ပြထားတဲ့ Recovery Dialog Box က ပြန်ပြနေပြီးတော့  
recovery လုပ်လုပ်၊ မလုပ်လုပ် soffice က ပြန်ထွက်သွားပြီး၊ သုံးလို့ မရဖြစ်နေခဲ့ပါတယ်။  

# How to Solve:  

Googling လုပ်ကြည့်လိုက်တော့ ပြဿနာက user profile ကို သိမ်းပေးထားလို့၊ ရှိနေတဲ့ LibreOffice ကို ဖျက်ပြီးတော့ installation အသစ်လုပ်ထားလဲ  
ဘာမှ အပြောင်းအလဲမဖြစ်ပဲ၊ soffice က မတက်နိုင်ဘူးဖြစ်နေတယ်လို့ သိလိုက်ရပါတယ်။  

ဖြေရှင်းနည်းကတော့ "/home/YOUR_USER_ID/.config/libreoffice/4" ဆိုတဲ့ path အောက်ကိုဝင်ပြီးတော့ "user" ဆိုတဲ့ ဖိုလ်ဒါကို နာမည်ပြောင်းပါ။  
ဥပမာ mv user user.old

Note: YOUR_USER_ID ဆိုတဲ့ နေရာမှာ ကိုယ့် login account name နဲ့ အစားထိုးပါ

တကယ်လို့ GUI ကနေ သွားမယ်ဆိုရင်တော့ "Ctrl+H" ကိုနှိပ် (သို့) View menu အောက်က "Show Hidden Files" ကို ရွေးမှသာ ဖွက်ထားတဲ့ ဖိုလ်ဒါဖြစ်တဲ့ ".config" ကို မြင်ရမှာ ဖြစ်ပါတယ်။  

user ဖိုလ်ဒါကို နာမည်တစ်ခုခု ပြောင်းပြီးသွားပြီဆိုရင်တော့ command prompt မှာ ``` $ soffice``` ဆိုပြီး ရိုက်လိုက်ရင် LibreOffice ရဲ့ Welcome Dialog Box တက်လာပြီး အောက်ပါအတိုင်း အဆင်ပြေပြေနဲ့ LibreOffice က သုံးဖို့ အဆင်သင့်ဖြစ်တာကို တွေ့ရပါလိမ့်မယ်။  

<p align="center">
 <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/LibreOffice_Now-OK.png" alt="LibreOffice Now Ready" width="652px" height="358px" /> 
</p>

စောစောက LibreOffice ရဲ့ configuration ဖိုလ်ဒါအောက်ကို ပြန်ဝင်ကြည့်တဲ့အခါ အောက်ပါအတိုင်း user ဖိုလ်ဒါအသစ်ကို ဆောက်ပေးတာကို တွေ့ရှိရပါလိမ့်မယ်။  

<p align="center">
 <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/new-user-profile-and-old-one.png" alt="user vs user.old folders" width="652px" height="258px" /> 
</p>

# Reference:  

[[Solved] OpenOffice keeps crashing when I try to use it](https://forum.openoffice.org/en/forum/viewtopic.php?f=6&t=88521)  
[OpenOffice vs. LibreOffice](https://www.howtogeek.com/187663/openoffice-vs.-libreoffice-whats-the-difference-and-which-should-you-use/)
