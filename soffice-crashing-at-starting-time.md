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


# Reference:  

[[Solved] OpenOffice keeps crashing when I try to use it](https://forum.openoffice.org/en/forum/viewtopic.php?f=6&t=88521)  
[OpenOffice vs. LibreOffice](https://www.howtogeek.com/187663/openoffice-vs.-libreoffice-whats-the-difference-and-which-should-you-use/)
