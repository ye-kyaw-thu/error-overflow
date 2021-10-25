
အောက်ပါ link ကို ကိုယ့်စက်ထဲမှာ ပြင်ဆင်ပြီး run တဲ့ log file:  
[https://www.analyticsvidhya.com/blog/2021/10/hands-on-hindi-text-analysis-using-natural-language-processing-nlp/](https://www.analyticsvidhya.com/blog/2021/10/hands-on-hindi-text-analysis-using-natural-language-processing-nlp/)

## 1st Error

အောက်ပါ RE က run တဲ့အခါမှာ error ပေးတယ်...  
```
 text = re.sub(r'[.!:?-'"\/]', r'', text)
```

error ကတော့ အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/4github/4students/word-cloud/indic-cloud$ python ./indic-cloud.py 
  File "./indic-cloud.py", line 74
    text = re.sub(r'[.!:?-'"\/]', r'', text)
                                           ^
SyntaxError: EOL while scanning string literal
```

RE syntax ကို အောက်ပါအတိုင်း escape လုပ်ပေးလိုက်မှ အဆင်ပြေသွားခဲ့...  
```python
    text = re.sub(r'[.!:?\-\'\"\/]', r'', text)
```

## 2nd Error

ဒုတိယ ပြဿနာက အောက်ပါအတိုင်း 'indicnlp.tokenize' module ကို မသိတဲ့ပြဿနာ...  

```    
 काम करके यह सिखाया कि संघर्ष से दूर ना भागे । आत्महत्या ना करें और अब खुद ही आत्महत्या कर ली।\n# # # # # //./w  ...         36
16175  बॉलीवुड एक्टर #सुशांतसिंहराजपूत ने #फांसी लगाकर की खुदखुशी-\n#खुदखुशी करने वालो पर मुझे तरस नही आता,\nक्योंकि दुनिया मे #खुशी और #गम दोनों मिलते है जो उसे न झेल सके वो इंसान #बुझदिल होता है!\nसुशांत तुमने सही नहीं किया!\nखैर #अल्लाह घर वालों को सब्र अता करे-आमीन\n# //./  ...         45
16176                                                                                               # #  क्यों चमक धमक सिर्फ दिखावा है इस फिल्म इंडस्ट्री का, बाकी सब अंदर से टूटे हुए हैं चाहे फिर वो कितना भी महान अदाकार  क्यों न सबकी जिंदगी सिर्फ दिखावा है सिर्फ घोर दिखावा 👎 #  ...         40
16177                                                                                                                        हर हाल में #खुश रहना सीख लो🙃\n        उस दिल को क्या #उदास रखना🧐\n               जिसमें मेरा #भोले बसता हो❤🙏\n\n#जयभोलेनाथ की 🙏☘🌺 📿🐚🛐\n\n  \ny y\n  //./  ...         47
16178                                                                               इतना कुछ पाने के बाद भी अगर इंसान जिदंगी से हार जाए , \n   🙄😒  तो उसने क्या पाया , और क्या वो खोए .... # #wy \n# # # # 🙏🙏\n  जिदंगी को हारना उत्तम नहीं है, जिदंगी को जीना सर्वोत्तम है...🙏🥺 //./  ...         48

[10 rows x 3 columns]
./indic-cloud.py:79: SettingWithCopyWarning: 
A value is trying to be set on a copy of a slice from a DataFrame

See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
  df['text'][i] = processText(df['text'][i])
Traceback (most recent call last):
  File "./indic-cloud.py", line 86, in <module>
    from indicnlp.tokenize import indic_tokenize
ModuleNotFoundError: No module named 'indicnlp.tokenize'
```

pip install indicnlp, pip install indic တွေ လုပ်ပေမဲ့ အဆင်မပြေဘူး။  
module ကို မသိဘူးပဲ ပြောနေလို့...  

အောက်ပါ link ထဲမှာ ပြောဆိုနေကြတာကို အခြေခံပြီးတော့   

[https://stackoverflow.com/questions/46992718/cannot-find-python-library]((base) ye@:/media/ye/project2/4github/4students/word-cloud/indic-cloud/anoopkunchukuttan-indic_nlp_library-1e0f224$ python setup.py install)  

anoopkunchukuttan-indic_nlp_library-INDIC_NLP_0.81-0-g1e0f224.zip ဆိုတဲ့ module ကို တိုက်ရိုက် download လုပ်ပြီး  
ကိုယ့်စက်ထဲမှာ install လုပ်ခဲ့တယ်။  

```
$ unzip anoopkunchukuttan-indic_nlp_library-INDIC_NLP_0.81-0-g1e0f224.zip
(base) ye@:/media/ye/project2/4github/4students/word-cloud/indic-cloud/anoopkunchukuttan-indic_nlp_library-1e0f224$ python setup.py install
```

အဆင်မပြေပဲ same error ပေးနေလို့ ပထမပိုင်းက pip နဲ့ install လုပ်ခဲ့တာကို သတိရပြီး pip uninstall လုပ်ခဲ့မှာ အဆင်ပြေသွားတယ်။  

```
(base) ye@:/media/ye/project2/4github/4students/word-cloud/indic-cloud$ pip uninstall indicnlp
Found existing installation: indicnlp 0.0.1
Uninstalling indicnlp-0.0.1:
  Would remove:
    /home/ye/anaconda3/lib/python3.7/site-packages/indicnlp-0.0.1.dist-info/*
    /home/ye/anaconda3/lib/python3.7/site-packages/indicnlp/*
Proceed (Y/n)? Y
  Successfully uninstalled indicnlp-0.0.1
```

## 3rd Error

တတိယကြုံရတဲ့ error ကတော့ "Remove Stopwords and Punctuations" ဆိုတဲ့ အဆင့်မှာ...  

```
(base) ye@:/media/ye/project2/4github/4students/word-cloud/indic-cloud$ python ./indic-cloud.py 
  File "./indic-cloud.py", line 106
    punctuations = ['nn','n', '।','/', '`', '+', '\', '"', '?', '▁(', '$', '@', '[', '_', "'", '!', ',', ':', '^', '|', ']', '=', '%', '&', '.', ')', '(', '#', '*', '', ';', '-', '}','|','"']
                                                                                                ^
SyntaxError: invalid syntax
(base) ye@:/media/ye/project2/4github/4students/word-cloud/indic-cloud$ 
```

အထက်မှာ ကြုံခဲ့ရတဲ့ RE သင်္ကေတတွေကို escape လုပ်ဖို့ လိုတဲ့ကိစ္စလို့ပဲ ယူဆခဲ့...  

```
punctuations = ['nn','n', '।','/', '`', '+', '\', '"', '?', '▁(', '$', '@', '[', '_', "'", '!', ',', ':', '^', '|', ']', '=', '%', '&', '.', ')', '(', '#', '*', '', ';', '-', '}','|','"']
```
ကို  
အောက်ပါအတိုင်း ပြင်ရေးလိုက်တော့ error clear ဖြစ်သွားခဲ့တယ်...  
(| က နှစ်ခါပါနေတာမျိုး ရှိနေပေမဲ့ ဒီအတိုင်းပဲ ထားထားလိုက်ပြီး run ခဲ့...)  

```
punctuations = ['nn','n', '।','/', '`', '+', '\\', '"', '?', '▁(', '$', '@', '[', '_', "\'", '!', ',', ':', '^', '|', ']', '=', '%', '&', '.', ')', '(', "#", '*', '', ';', '-', '}','|','"']
```

## Saving Graph

ပထမဆုံး graph ထုတ်တဲ့ အဆင့်ထိ ရောက်လာပြီ...  

```
df.hist(column = 'word_count', by ='label',figsize=(12,4), bins = 5)
```

Jupyter Notebook ကို သုံးရင် (.ipynb) တော့ graph က မြင်ရမှာ ဖြစ်ပေမဲ့ python ပရိုဂရမ်အနေနဲ့ run မယ်ဆိုရင်တော့ အောက်ပါလိုင်းကို ဖြည့်ပေးရပါမယ်...  

```
plt.savefig("Distribution-of-each-tweet-length-per-Label.png", bbox_inches='tight', dpi=100)
```

## After plt.savefig(), run plt.show()

မသိသေးတဲ့သူတွေရှိနိုင်လို့ ဖြည့်ပြောပြထားတာပါ။  
plt.show() ကို အရင် လုပ်ပြီးမှ plt.savefig() run ရင် output အနေနဲ့ သိမ်းထားတဲ့ပုံက အဖြူထည်ချည်းပဲ ဖြစ်နေတာမျိုး ဖြစ်တတ်တယ်။  
အဲဒါကြောင့် အရင်သိမ်းပြီးမှ plt.show() လုပ်ပါ။ ဥပမာ အောက်ပါအတိုင်း...  

```python
# plot the WordCloud image                      
plt.figure(figsize = (18, 8), facecolor = None)
plt.imshow(wordcloud,interpolation="bilinear")
plt.axis("off")
plt.tight_layout(pad = 0)

plt.savefig("error-graph-of-hindi-wordcloud.png")
plt.show()
```

## Graphs for Tweet Distribution

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/Distribution-of-each-tweet-length-per-Label.png" alt="distribution-before-cleaning" width="750"/>  
</p>  
<div align="center">
  Fig.1 Distribution of each tweet-length per Label  
</div> 

<br />

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/Distribution-of-each-tweet-length-per-Label-after-cleaning-data.png" alt="distribution-after-cleaning" width="750"/>  
</p>  
<div align="center">
  Fig.2 Distribution of each tweet-length per Label after cleaning data 
</div> 

<br />

## Font Download

Unicode font ကို download လုပ်ပြီး assign မလုပ်ပေးရင် Hindi စာလုံးတွေက wordcloud လုပ်တဲ့အခါမှာ မပြပေးနိုင်ဘူး...  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/error-graph-of-hindi-wordcloud.png" alt="error-graph-of-hindi-wordcloud" width="640"/>  
</p>  
<div align="center">
  Fig.3 a graph with font error 
</div> 

<br />


အဲဒါကြောင့် Hindi font တွေကို အောက်ပါ link ကနေ download လုပ်ယူခဲ့ပြီး python running လုပ်တဲ့ path အောက်မှာ save လုပ်ထားခဲ့...  

[http://www.lipikaar.com/support/download-unicode-fonts-for-hindi-marathi-sanskrit-nepali](http://www.lipikaar.com/support/download-unicode-fonts-for-hindi-marathi-sanskrit-nepali)

```
(base) ye@:/media/ye/project2/4github/4students/word-cloud/indic-cloud$ unzip Devanagari.zip 
Archive:  Devanagari.zip
  inflating: Devanagari/chandas1-2.ttf  
  inflating: Devanagari/gargi.ttf    
  inflating: Devanagari/kalimati.ttf  
  inflating: Devanagari/lohit_kok.ttf  
  inflating: Devanagari/lohit_ks.ttf  
  inflating: Devanagari/lohit_mai.ttf  
  inflating: Devanagari/lohit_ne.ttf  
  inflating: Devanagari/lohit_sd.ttf  
  inflating: Devanagari/Lohit-Devanagari.ttf  
  inflating: Devanagari/Lohit-Marathi.ttf  
  inflating: Devanagari/nakula.ttf   
  inflating: Devanagari/sahadeva.ttf  
  inflating: Devanagari/samanata.ttf  
  inflating: Devanagari/Samyak-Devanagari.ttf  
  inflating: Devanagari/Sarai_07.ttf  
(base) ye@:/media/ye/project2/4github/4students/word-cloud/indic-cloud$ cd Devanagari/
(base) ye@:/media/ye/project2/4github/4students/word-cloud/indic-cloud/Devanagari$ ls
chandas1-2.ttf  kalimati.ttf          lohit_kok.ttf  lohit_mai.ttf      lohit_ne.ttf  nakula.ttf    samanata.ttf           Sarai_07.ttf
gargi.ttf       Lohit-Devanagari.ttf  lohit_ks.ttf   Lohit-Marathi.ttf  lohit_sd.ttf  sahadeva.ttf  Samyak-Devanagari.ttf
(base) ye@:/media/ye/project2/4github/4students/word-cloud/indic-cloud/Devanagari$ 
```

## Font Installation

Linux command line ကနေ font installation လုပ်တာက install လုပ်ချင်တဲ့ font ဖိုင်ကို "~/.local/share/fonts/" ဆိုတဲ့ path အောက်ကို ကူးထည့်ပေးယုံပါပဲ။  

```
(base) ye@:/media/ye/project2/4github/4students/word-cloud/indic-cloud/Devanagari$ cp gargi.ttf ~/.local/share/fonts/
```

ပြီးရင်တော့ fc-cache ကို ရှင်းလိုက်ပြီး regenerate လုပ်ပေးရပါတယ်။  

```
(base) ye@:/media/ye/project2/4github/4students/word-cloud/indic-cloud/Devanagari$ fc-cache -f -v
/usr/share/fonts: caching, new cache contents: 0 fonts, 8 dirs
/usr/share/fonts/X11: caching, new cache contents: 0 fonts, 4 dirs
/usr/share/fonts/X11/Type1: caching, new cache contents: 81 fonts, 0 dirs
/usr/share/fonts/X11/encodings: caching, new cache contents: 0 fonts, 1 dirs
/usr/share/fonts/X11/encodings/large: caching, new cache contents: 0 fonts, 0 dirs
...
...
...
/usr/share/fonts/X11/encodings/large: skipping, looped directory detected
/usr/share/fonts/truetype/roboto/unhinted: skipping, looped directory detected
/usr/share/fonts/truetype/roboto/unhinted/RobotoTTF: skipping, looped directory detected
/home/ye/anaconda3/var/cache/fontconfig: cleaning cache directory
/home/ye/.cache/fontconfig: cleaning cache directory
/home/ye/.fontconfig: not cleaning non-existent cache directory
fc-cache: succeeded
(base) ye@:/media/ye/project2/4github/4students/word-cloud/indic-cloud/Devanagari$ 
```

font cache က update ဖြစ်သွားပြီလား သိချင်လို့ အောက်ပါအတိုင်း confirmation လုပ်ခဲ့...  

```
(base) ye@:/media/ye/project2/4github/4students/word-cloud/indic-cloud/Devanagari$ fc-list | grep gargi
/home/ye/.local/share/fonts/gargi.ttf: gargi:style=Medium
```

## Assign Unicode Font

font ကို installation လုပ်ပြီးတဲ့အခါမှာတော့ နဂိုရေးထားတဲ့ အောက်ပါ wordcloud ဆောက်တဲ့ statement ကို ...  

```
wordcloud = WordCloud(width = 1000, height = 700,
                background_color ='white',
                min_font_size = 10).generate_from_frequencies(dictionary)
```

အောက်ပါ အတိုင်း gargi.ttf ဖောင့် assign လုပ်ခဲ့...  

```
font = "./Devanagari/gargi.ttf"
dictionary=Counter(df_list)
wordcloud = WordCloud(width = 1000, height = 700,
                background_color ='white',
                min_font_size = 10, font_path= font).generate_from_frequencies(dictionary)    
```

ဖိုင်နာမည်ကိုတော့ အောက်ပါအတိုင်း သိမ်းဆည်းခဲ့...  

```
#plt.savefig("error-graph-of-hindi-wordcloud.png")
plt.savefig("beautiful-hindi-wordcloud.png")
```

## Getting Hindi Wordcloud

ပြင်ဆင်ရတာ... Debug လုပ်ရတာ တွေပါ ထည့်တွက်ရင် ၄နာရီလောက် ကြာသွားခဲ့ပေမဲ့...  
တကယ် Hindi wordcloud ပုံ ထွက်လာဖို့အတွက် Running time က ၄၅ စက္ကန့်လောက်ပဲ ကြာပါတယ်...  

```
(base) ye@:/media/ye/project2/4github/4students/word-cloud/indic-cloud$ time python ./indic-cloud.py
...
...
...
5, 'दुखी': 5, 'धोनी': 5, 'बहुतों': 5, 'शिकायतें': 5, 'सेबहुतों': 5, 'थोड़ी': 5, '‘मैं': 5, 'ना’': 5, 'सकें': 5, 'बात1': 5, 'y😂😂😂': 5, 'फ़िल्म': 5, 'कुम्हार': 5, 'थाप': 5, 'मिट्टी': 5, 'सुंदर': 5, 'घड़े': 5, 'डांट': 5, 'फटकर': 5, 'संस्कारी': 5, 'निर्माण': 5, 'दख़ल': 5, 'अंदाज़': 5, 'फेंको': 5, 'उन्हे': 5, 'धड़कते': 5, 'पैगाम': 5, '👀आया': 5, 'तुमने': 5, 'देखकर': 5, '🚶\u200d♀wअभीतोज़िन्दगीकापैगाम1': 5, 'हसतमुख': 5, 'चेहराटिपलेला': 5, 'क्षणफ': 5, 'फोटुतलाzxx1': 5, '🎂🎂आपको': 5, '🙌': 5, '🤲': 5, '😈': 5, '😞w': 5, 'चुनौतियाँ': 5, 'वालो': 5, 'आज़माती': 5, 'जिनकी': 5, '😘😘': 5, 'हक': 5, 'बनता': 5, 'डालें': 5, 'पंछी': 5, 'हैकौन': 5, 'तपन': 5, 'जतन': 5, 'दृष्टिकोण': 5, 'सम्पदा': 5, 'परिवारो': 5, 'तनावमुक्त': 5, 'जख्म': 5, 'दिखते': 5, 'दुखते': 5, 'हूंखुशियों': 5, 'ग़मो': 5, 'काखरीदार': 5, 'हूंमैं': 5, 'यार1': 5, '🖕🏻1': 5, 'जादा': 5, 'चीज': 5, 'उल्झो': 5, 'नाहि': 5, 'बोझ': 5, 'रखो': 5, 'संभाळ': 5, 'साको': 5, 'उतना': 5, 'लेनायाहा': 5, 'रहेगी': 5, 'मुस्कुराहटपर': 5, 'होसोचता': 5, 'रहू': 5, 'यूं': 5, 'आते': 5, '👌💕😊1': 5, 'ज़रूरत': 5, 'इत्तफाक': 5, '😻😻बचपन': 5, 'यादें': 5, 'ताज़ा': 5, 'बताओ': 5, 'लाइक': 5, 'यार😀👇👇👇👇👇👇': 5, '🙈🙈🙈🙈': 5, '🙈😹😹1': 5, 'वारियर्स': 5, 'पूंजी': 5, 'खेती': 5, 'सौंपने': 5, 'लाये': 5, '–': 5, 'वर्चुअल': 5, 'रैली': 5, '💞जिंदगी': 5, 'राहों': 5, 'इरादा': 5, 'कत्ल': 5, 'सर': 5, 'इश्क': 5, 'डाल': 5, 'तुने': 5, 'हुनर': 5, 'तरीका': 5, 'बताओदिल': 5, 'छूटे': 5, 'रूठे': 5, 'रिश्तो': 5, 'निभाने': 5, 'भावनाएं': 5, 'विवशता': 5, 'दोस्तों': 5, 'होसोचकर': 5, 'गयाजाते': 5, 'गयादुखी': 5, 'दोस्तोंखुश': 5, 'दुखों': 5, 'आज़ाद': 5, '🌹छू': 5, 'बेशक': 5, 'कातिल': 5, 'महवा': 5, 'ओम': 5, 'प्रकाश': 5, 'हुड़ला': 5, 'तुझको': 5, 'खोना': 5, 'थाइस': 5, '📍1': 5, '🚶\u200d♂आज': 5, '👀परेशानकोईकरताथाकभी1': 5, 'लड़का': 5, 'मायानगरी': 5, 'भयावह': 5, 'जाल': 5, 'फसने': 5, 'देंगेकैसा': 5, 'w1': 5, 'मुकाम': 5, 'नाहासिल': 5, '🙏पर': 5, 'चाहने': 5, 'भूलिए': 5, '🙏🙏🙏1': 5, '😔😢': 5, '¡': 5, '😬💃': 5, '😊🖤': 5, '🥺1': 5, 'क्षति': 5, 'दिलो': 5, 'छाये': 5, 'रहेगे': 5, 'भगवानआपकी': 5, 'दें': 5, '💐😭😭😭': 5, 'जनों': 5, '🙏😭': 5, 'सुनी': 5, 'ऋषि': 5, 'कपूर': 5, 'इरफान': 5, 'पठान': 5, 'सितारे': 5, 'क्याक्या': 5, 'आनी': 5, 'दिखाना': 5, 'कष्ट': 5, 'लिखे': 5, 'मौजूद': 5, 'मौजूदा': 5, 'इतिहास': 5, '🤐1': 5, 'आेैर': 5, 'दरमियान': 5, 'दूरी': 5, 'बढ़ती': 5, 'जीना': 5, 'बड़ीबड़ी': 5, 'कलाओं': 5, 'माहिर': 5, 'पाते': 5, 'दुनियां': 5, 'रुखसत': 5, 'रांची': 5, 'रिम्स': 5, 'हॉस्पिटल': 5, 'केक': 5, 'काटते': 5, 'लालू': 5, 'जी1': 5, 'लीपर': 5, 'ली😒🥺पर': 5, 'पैसों': 5, 'नाराजगी': 5, 'उफ्फ्फ': 5, 'मानसून': 5, 'दस्तक': 5, 'अभिनेतायुवा': 5, 'ली😒🥺😢पर': 5, 'लगातर': 5, 'मतलब': 5, 'जनतामगर': 5, 'तुलना': 5, 'थेखुश': 5, 'दोस्त1': 5, 'मुंबई': 5, 'शानदार': 5, 'धोखा': 5, 'दियामेरा': 5, 'यकीन': 5, 'नही1': 5, 'बोलूंगा': 5, '😞': 5, 'कायरता': 5, '\U0001f90e\U0001f90e': 5, 'रखिए': 5, '😔1': 5, '🙏💐1': 5, 'वाकई': 5, 'दायरे': 5, 'दुःखद🙏💐😥1': 5, 'खैरियत': 5, 'पूछी': 5, 'दीवाने': 5, 'दुआओ': 5, 'सौ': 5, 'दफा': 5, 'लूँ': 5, 'अभिनय': 5, 'रोशन': 5, 'दिवंगत': 5, 'ग़लत': 5, '😔': 5, '“तुम': 5, 'सूना': 5, 'आकार': 5, 'दुगना': 5, 'हानि': 5, 'लाभ': 5, 'मरण': 5, 'अपयश': 5, 'फिल्मों': 5, 'प्रेरणा': 5, '🙏🙏🙏': 5, 'स्वर्गीय': 5, 'छिछोरे': 5, 'मूवी': 5, 'भागे': 5, 'सदी': 4, 'सूर्य': 4, 'गोविंद': 4, 'देव': 4, 'मंदिर': 4, 'हरि': 4, 'संकीर्तन': 4, 'yyv': 4, 'राष्ट्रपति': 3, 'फूंका': 3, 'पूतला': 3, 'पावटा': 3, 'अजय': 3, 'चौहान': 3, 'उपलक्ष': 3, 'फिट': 3, 'संस्थान': 3, 'प्रतिभागियों': 3, 'अरविंद': 3, 'बिहारी': 2, 'हुंकार': 2, 'चीजों': 2, 'सिखाता': 2, 'सहा': 1, 'सहना': 1, 'जासकता': 1, 'जन': 1, 'जागरूकता': 1, 'अभियान': 1, 'चलेगा': 1})
./indic-cloud.py:138: SettingWithCopyWarning: 
A value is trying to be set on a copy of a slice from a DataFrame

See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
  df['text'][i]=[ele for ele in df['text'][i] if ele not in (to_remove)]
./indic-cloud.py:145: SettingWithCopyWarning: 
A value is trying to be set on a copy of a slice from a DataFrame

See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
  df['text'][i]=[ele for ele in df['text'][i] if ele not in (least_common)]

real	0m45.279s
user	0m36.036s
sys	0m0.935s
```

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/beautiful-hindi-wordcloud.png" alt="beautiful-hindi-wordcloud" width="640"/>  
</p>  
<div align="center">
  Fig.4 a beautiful Hindi wordcloud with gargi.ttf 
</div> 

<br />

