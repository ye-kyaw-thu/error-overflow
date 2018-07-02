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

LibreOffice က တရက်မှာသုံးနေရင်းနဲ့ crash ဖြစ်သွားပြီးတော့၊  စာသင်ဖို့အတွက် presentation slide ပြင်ဖို့ Impress presentation ဖိုင်တစ်ဖိုင်ကို ဖွင့်လိုက်တိုင်းမှာ အောက်ပါ အတိုင်း   



<p align="center">
 <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/LibreOffice-Error.png" alt="Error" width="552px" height="538px" /> 
</p>

# Reference:  

[OpenOffice vs. LibreOffice](https://www.howtogeek.com/187663/openoffice-vs.-libreoffice-whats-the-difference-and-which-should-you-use/)
