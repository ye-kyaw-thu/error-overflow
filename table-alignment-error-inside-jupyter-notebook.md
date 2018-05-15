# Markdown Table Alignment Error inside Jupyter Notebook 

# In English:  
Although I tried ":---" for left alignment, "---:" for right alignment and ":---:" for center alignment, not working at all.
My current solution is adding HTML code such as "<p align="left"> in each cell.

# In Myanmar Language:
Jupyter notebook ရဲ့ cell ထဲမှာ markdown table တစ်ခု ဆောက်ဖို့ လိုအပ်လာလို့ ဆောက်တဲ့အခါမှာ cell တစ်ခုချင်းစီမှာရှိတဲ့ စာကြောင်းတွေကို ဘယ်ဘက်ကပ်ရေးခိုင်း (left alignment)၊ ညာဘက်ကပ်ရေးခိုင်း (right alignment)၊ အလယ်မှာကပ်ရေးခိုင်း (center alignment) တာက တစ်ခုမှ အလုပ်မလုပ်ပေးလို့ မြန်မာစာ စာလုံးတွေကြောင့်များလား၊ format အတွက် ပေးရတဲ့ markdown markup tag တွေဖြစ်တဲ့ ":---" (ဘယ်ဘက် ကပ်)၊ "---:" (ညာဘက်ကပ်)၊ ":---:" (အလယ်မှာနေရာချ) တွေကို ရိုက်ထည့်တဲ့နေရာမှာများ မှားနေသလား ပြန်စစ်တာ၊ Googling လုပ်ကြည့်တာနဲ့ ၁၅မိနစ်၊ မိနစ် ၂၀ လောက် အချိန်ကုန်သွားခဲ့ပါတယ်။ နောက်ဆုံး လက်ရှိ လုပ်လို့ရတဲ့နည်းကတော့ table ရဲ့ cell တစ်ခုချင်းစီမှာ HTML tag နဲ့ alignment ကို ဝင်ပြင်တဲ့နည်းပါပဲ။ နည်းနည်း ရုပ်ဆိုးပေမဲ့ ဖြေရှင်းလို့ရတဲ့ နည်းတစ်ခုမို့လို့ error-overflow အဖြစ် note မှတ်ထားလိုက်ပါတယ်။  

ပထမတော့ အောက်ပါအတိုင်း ဇယားကို လုပ်ထားတာ လုံးဝကို alignment လုပ်မပေးပါဘူး။  

```
| Escape sequence | အလုပ်လုပ်ပုံ |
| :--- | :---: |
| \a | သတိပေးချင်တဲ့ အခါ၊ စပီကာကနေ bell အသံပေးချင်တဲ့အခါ သုံးတယ်။ ASCII bell character လို့လည်းခေါ်တယ်။ |
| \b | Backspace ကီးကို ရိုက်ချင်တဲ့အခါ သုံးတယ်။ |
| \c | သူ့နောက်က စာလုံးတွေကို ရိုက်မပေးတော့ဘူး။ နောက်ပြီး စာကြောင်းအသစ်တစ်ကြောင်းအနေနဲ့လည်း ခွဲမပေးပါဘူး|
| \f | form feed (စာမျက်နှာ အသစ်ခွဲ) အလုပ်ကို လုပ်ပေးတယ်။ |
| \n | လက်ရှိ ရောက်ရှိနေတဲ့နေရာကနေ စာကြောင်းအသစ်ရဲ့ ဘယ်ဘက် အကျဆုံးနေရာကို ရွှေ့ပေးလိမ့်မယ်။ |
| \r | Carriage return သင်္ကေတပါ။ လက်ရှိစာကြောင်းရဲ့ ဘယ်ဘက်ထိပ်ဆုံး နေရာကို ရွှေ့ချင်တဲ့အခါ အသုံးပြုတယ်။ |
| \t | Horizontal Tab ကီးကို ရိုက်ဖို့အတွက် သုံးတယ်။ |
| \v | Vertical Tab ကီးကို ရိုက်ဖို့အတွက် သုံးတယ်။ |
| \\&zwnj;[ | စကရင်မှာ ရိုက်ပြဖို့မဟုတ်ပဲ၊ တစ်ခြား အလုပ်လုပ်ဖို့ သတ်မှတ်ထားသောစာလုံး (non-printing character) တွေရဲ့ ကွင်းစ |
| \\&zwnj;] | စကရင်မှာ ရိုက်ပြဖို့မဟုတ်ပဲ၊ တစ်ခြား အလုပ်လုပ်ဖို့ သတ်မှတ်ထားသောစာလုံး (non-printing character) တွေရဲ့ ကွင်းပိတ် |
| \\' | single quote ကို ရိုက်ဖို့အတွက်သုံးတယ်။ |
| \\" | double quote ကို ရိုက်ဖို့အတွက်သုံးတယ်။ |
| \\nnn | eight-bit စာလုံးတွေကို　octal value နဲ့ ရိုက်ဖို့အတွက်သုံးတယ်။  |
| \\xHH | eight-bit စာလုံးတွေကို hexadecimal value နဲ့ ရိုက်ဖို့အတွက်သုံးတယ်။  |
|\uHHHH |Unicode (ISO/IEC 10646) စာလုံးတွေကို hexadecimal value နဲ့ ရိုက်ဖို့သုံးပါတယ်။ (hexadecimal ဂဏန်း 4 လုံးအထိ) |
|\UHHHHHHHH | Unicode (ISO/IEC 10646) စာလုံးတွေကို hexadecimal value နဲ့ ရိုက်ဖို့သုံးပါတယ်။ (hexadecimal ဂဏန်း ၈ လုံးအထိ) |
|\cx | control ကီးနဲ့ တခြားကီးတစ်ခုခုကို တွဲရိုက်ဖို့ (control-x) အတွက် သုံးပါတယ်။ |
```

လက်ရှိ ဖြေရှင်းထားတဲ့ နည်းကတော့ အောက်ပါအတိုင်းဖြစ်ပါတယ်။  

```
| <p align="center"> Escape sequence | အလုပ်လုပ်ပုံ |
| --- | --- |
| <p align="left"> \a | <p align="left"> သတိပေးချင်တဲ့ အခါ၊ စပီကာကနေ bell အသံပေးချင်တဲ့အခါ သုံးတယ်။ ASCII bell character လို့လည်းခေါ်တယ်။ |
| <p align="center"> \b | <p align="center"> Backspace ကီးကို ရိုက်ချင်တဲ့အခါ သုံးတယ်။ |
| <p align="center"> \c | <p align="center"> သူ့နောက်က စာလုံးတွေကို ရိုက်မပေးတော့ဘူး။ နောက်ပြီး စာကြောင်းအသစ်တစ်ကြောင်းအနေနဲ့လည်း ခွဲမပေးပါဘူး|
| <p align="center"> \f | <p align="center"> form feed (စာမျက်နှာ အသစ်ခွဲ) အလုပ်ကို လုပ်ပေးတယ်။ |
| <p align="center"> \n | <p align="center"> လက်ရှိ ရောက်ရှိနေတဲ့နေရာကနေ စာကြောင်းအသစ်ရဲ့ ဘယ်ဘက် အကျဆုံးနေရာကို ရွှေ့ပေးလိမ့်မယ်။ |
| <p align="center"> \r | <p align="center"> Carriage return သင်္ကေတပါ။ လက်ရှိစာကြောင်းရဲ့ ဘယ်ဘက်ထိပ်ဆုံး နေရာကို ရွှေ့ချင်တဲ့အခါ အသုံးပြုတယ်။ |
| <p align="center"> \t | <p align="center"> Horizontal Tab ကီးကို ရိုက်ဖို့အတွက် သုံးတယ်။ |
| <p align="center"> \v | <p align="center"> Vertical Tab ကီးကို ရိုက်ဖို့အတွက် သုံးတယ်။ |
| <p align="center"> \\&zwnj;[ | <p align="center"> စကရင်မှာ ရိုက်ပြဖို့မဟုတ်ပဲ၊ တစ်ခြား အလုပ်လုပ်ဖို့ သတ်မှတ်ထားသောစာလုံး (non-printing character) တွေရဲ့ ကွင်းစ |
| <p align="center"> \\&zwnj;] | <p align="center"> စကရင်မှာ ရိုက်ပြဖို့မဟုတ်ပဲ၊ တစ်ခြား အလုပ်လုပ်ဖို့ သတ်မှတ်ထားသောစာလုံး (non-printing character) တွေရဲ့ ကွင်းပိတ် |
| <p align="center"> \\' | <p align="center"> single quote ကို ရိုက်ဖို့အတွက်သုံးတယ်။ |
| <p align="center"> \\" | <p align="center"> double quote ကို ရိုက်ဖို့အတွက်သုံးတယ်။ |
| <p align="center"> \\nnn | <p align="center"> eight-bit စာလုံးတွေကို　octal value နဲ့ ရိုက်ဖို့အတွက်သုံးတယ်။  |
| <p align="center"> \\xHH | <p align="center"> eight-bit စာလုံးတွေကို hexadecimal value နဲ့ ရိုက်ဖို့အတွက်သုံးတယ်။  |
| <p align="center"> \uHHHH | <p align="center"> Unicode (ISO/IEC 10646) စာလုံးတွေကို hexadecimal value နဲ့ ရိုက်ဖို့သုံးပါတယ်။ (hexadecimal ဂဏန်း 4 လုံးအထိ) |
| <p align="center"> \UHHHHHHHH | <p align="center"> Unicode (ISO/IEC 10646) စာလုံးတွေကို hexadecimal value နဲ့ ရိုက်ဖို့သုံးပါတယ်။ (hexadecimal ဂဏန်း ၈ လုံးအထိ) |
| <p align="center"> \cx | <p align="center"> control ကီးနဲ့ တခြားကီးတစ်ခုခုကို တွဲရိုက်ဖို့ (control-x) အတွက် သုံးပါတယ်။ |
```

Google Chrome Browser မှာ မြင်ရတဲ့ ဇယားပုံကတော့ အောက်ပါအတိုင်း left alignment ဖြစ်ပါတယ်။  

<p align="center">
 <img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/markdown-table-alignment-error-within-Jupyter-notebook-solution.png" alt="aligned-table" width="855px" height="646px" /> 
</p>

# Reference:  

[Markdown table alignment #3024](https://github.com/jupyter/notebook/issues/3024)  

