# Unzipping Long Filenames from MacOS

Filename ပေးတဲ့အခါမှာ ဖြစ်နိုင်ရင် long name တွေ မလုပ်ကြစေချင်ဘူး။ ပြီးတော့ ဖိုင်နာမည်မှာ space ပါတာတို့ slash တို့က လုံးဝကို မလုပ်သင့်ပါဘူး။ 
ဘာကြောင့်လဲ ဆိုတော့ OS မတူတဲ့ သူတွေဆီကို အဲဒီ ဖိုင်တွေကို ပို့ပေးကြတဲ့အခါမှာ ပြဿနာရှိလို့ပါ။ ပြီးတော့ တကယ် command line နဲ့ အလုပ်လုပ်ကြတဲ့သူတွေအတွက်က အဲဒီလို ဖိုင်နာမည်အရှည်ကြီးတွေနဲ့က အဆင်မပြေဘူးလေ။ 
program ရေးပြီး ဖိုင်တွေကို ဖွင့်ကြ၊ ရေးကြ၊ ပြင်ကြရတဲ့အခါမျိုးမှာလည်း အနှောက်အယှက် ပေးနိုင်လို့ပါ။  

ဒီ log ဖိုင်က iSAI-NLP 2021 NLP/AI Workshop မှာ ရိုက်ထားတဲ့ ဓာတ်ပုံတွေကို ရလာလို့ unzip လုပ်ကြည့်တဲ့အခါမှာ unzip လုပ်လို့ မရလို့ hacking လုပ်ပြီး ဖြေထားတဲ့ log ပါ။
တစ်ယောက်ယောက် ဒါမျိုး ပြဿနာကြုံလာတဲ့အခါမှာ အသုံးဝင်မှာမို့ log ရေးထားတာပါ။  

y  
9 Jan 2022  

```
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$ mv ~/Downloads/3th\ Southeast\ Asian\ NLP_AI\ R\&D\ Workshop.zip .
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$ ls
'3th Southeast Asian NLP_AI R&D Workshop.zip'
```

```
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$ unzip ./3th\ Southeast\ Asian\ NLP_AI\ R\&D\ Workshop.zip 
Archive:  ./3th Southeast Asian NLP_AI R&D Workshop.zip
checkdir error:  cannot create 3th Southeast Asian NLP:AI R&D Workshop
                 Invalid argument
                 unable to process 3th Southeast Asian NLP:AI R&D Workshop/.
error:  cannot create __MACOSX/._3th Southeast Asian NLP:AI R&D Workshop
        Invalid argument
checkdir error:  cannot create 3th Southeast Asian NLP:AI R&D Workshop
                 Invalid argument
                 unable to process 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/.
checkdir error:  cannot create __MACOSX/3th Southeast Asian NLP:AI R&D Workshop
                 Invalid argument
                 unable to process __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/._Keynote#1_ Prof. Yves Lepage.
checkdir error:  cannot create 3th Southeast Asian NLP:AI R&D Workshop
                 Invalid argument
                 unable to process 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/.
...
...
...
checkdir error:  cannot create __MACOSX/3th Southeast Asian NLP:AI R&D Workshop
                 Invalid argument
                 unable to process __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 13.20.25.png.
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$ 
```

## Check Filenames

```
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$ zipnote ./3th\ Southeast\ Asian\ NLP_AI\ R\&D\ Workshop.zip > long-names
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$ head long-names 
@ 3th Southeast Asian NLP:AI R&D Workshop/
@ (comment above this line)
@ __MACOSX/._3th Southeast Asian NLP:AI R&D Workshop
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/._Keynote#1_ Prof. Yves Lepage
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/
@ (comment above this line)
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$ tail ./long-names 
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 14.26.21.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 14.26.21.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 13.20.25.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 13.20.25.png
@ (comment above this line)
@ (zip file comment below this line)
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$
```

gedit နဲ့ long-names ဖိုင်ကို ဖွင့်ပြီး ဝင်ပြင်တယ်။  
```
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$ gedit ./long-names 
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$ cp long-names original-long-names
```

ပြင်လိုက်ပြီးတဲ့ ဖိုင်က အောက်ပါအတိုင်း...  
```
@ 3th Southeast Asian NLP:AI R&D Workshop/
@=workshop/
@ (comment above this line)
@ __MACOSX/._3th Southeast Asian NLP:AI R&D Workshop
@=photo/workshop
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/
@=workshop/yves-sensei/
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/._Keynote#1_ Prof. Yves Lepage
@=photo/workshop/yves-sensei/
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/
@=workshop/neubig-sensei/
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/._Keynote#2_ Assoc. Prof. Graham Neubig
@=photo/workshop/neubig-sensei/
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/
@=workshop/presentation/
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/._Presentation Session
@=photo/workshop/presentation/
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/Screen Shot 2564-12-21 at 10.05.58.png
@=workshop/yves-sensei/screenshot1.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/._Screen Shot 2564-12-21 at 10.05.58.png
@=photo/workshop/yves-sensei/screenshot1.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/Screen Shot 2564-12-21 at 09.45.23.png
@=workshop/yves-sensei/screenshot2.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/._Screen Shot 2564-12-21 at 09.45.23.png
@=photo/workshop/yves-sensei/screenshot2.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/Screen Shot 2564-12-21 at 09.38.34.png
@=workshop/yves-sensei/screenshot3.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/._Screen Shot 2564-12-21 at 09.38.34.png
@=photo/workshop/yves-sensei/screenshot3.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/Screen Shot 2564-12-21 at 09.41.43.png
@=workshop/yves-sensei/screenshot4.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/._Screen Shot 2564-12-21 at 09.41.43.png
@=photo/workshop/yves-sensei/screenshot4.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/Screen Shot 2564-12-21 at 10.05.34.png
@=workshop/yves-sensei/screenshot5.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/._Screen Shot 2564-12-21 at 10.05.34.png
@=photo/workshop/yves-sensei/screenshot5.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/Screen Shot 2564-12-21 at 10.34.03.png
@=workshop/yves-sensei/screenshot6.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/._Screen Shot 2564-12-21 at 10.34.03.png
@=photo/workshop/yves-sensei/screenshot6.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/Screen Shot 2564-12-21 at 09.35.45.png
@=workshop/yves-sensei/screenshot7.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/._Screen Shot 2564-12-21 at 09.35.45.png
@=photo/workshop/yves-sensei/screenshot7.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/Screen Shot 2564-12-21 at 09.45.39.png
@=workshop/yves-sensei/screenshot8.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/._Screen Shot 2564-12-21 at 09.45.39.png
@=photo/workshop/yves-sensei/screenshot8.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/Screen Shot 2564-12-21 at 10.34.12.png
@=workshop/yves-sensei/screenshot9.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/._Screen Shot 2564-12-21 at 10.34.12.png
@=photo/workshop/yves-sensei/screenshot9.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/Screen Shot 2564-12-21 at 10.24.16.png
@=workshop/yves-sensei/screenshot10.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/._Screen Shot 2564-12-21 at 10.24.16.png
@=photo/workshop/yves-sensei/screenshot10.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/Screen Shot 2564-12-21 at 10.16.06.png
@=workshop/yves-sensei/screenshot11.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/._Screen Shot 2564-12-21 at 10.16.06.png
@=photo/workshop/yves-sensei/screenshot11.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 10.47.50.png
@=workshop/neubig-sensei/screenshot1.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 10.47.50.png
@=photo/workshop/neubig-sensei/screenshot1.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 11.47.08.png
@=workshop/neubig-sensei/screenshot2.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 11.47.08.png
@=photo/workshop/neubig-sensei/screenshot2.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 10.51.33.png
@=workshop/neubig-sensei/screenshot3.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 10.51.33.png
@=photo/workshop/neubig-sensei/screenshot3.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 11.20.34.png
@=workshop/neubig-sensei/screenshot4.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 11.20.34.png
@=photo/workshop/neubig-sensei/screenshot4.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 10.47.26.png
@=workshop/neubig-sensei/screenshot5.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 10.47.26.png
@=photo/workshop/neubig-sensei/screenshot5.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 11.20.25.png
@=workshop/neubig-sensei/screenshot6.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 11.20.25.png
@=photo/workshop/neubig-sensei/screenshot6.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 10.53.57.png
@=workshop/neubig-sensei/screenshot7.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 10.53.57.png
@=photo/workshop/neubig-sensei/screenshot7.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 10.47.34.png
@=workshop/neubig-sensei/screenshot8.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 10.47.34.png
@=photo/workshop/neubig-sensei/screenshot8.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 11.09.56.png
@=workshop/neubig-sensei/screenshot9.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 11.09.56.png
@=photo/workshop/neubig-sensei/screenshot9.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 10.49.02.png
@=workshop/neubig-sensei/screenshot10.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 10.49.02.png
@=photo/workshop/neubig-sensei/screenshot10.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/kn2group.png
@=workshop/neubig-sensei/screenshot11.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._kn2group.png
@=photo/workshop/neubig-sensei/screenshot11.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 11.09.46.png
@=workshop/neubig-sensei/screenshot12.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 11.09.46.png
@=photo/workshop/neubig-sensei/screenshot12.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 10.51.16.png
@=workshop/neubig-sensei/screenshot13.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 10.51.16.png
@=photo/workshop/neubig-sensei/screenshot13.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/kn2ss2.png
@=workshop/neubig-sensei/screenshot14.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._kn2ss2.png
@=photo/workshop/neubig-sensei/screenshot14.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 11.27.46.png
@=workshop/neubig-sensei/screenshot15.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 11.27.46.png
@=photo/workshop/neubig-sensei/screenshot15.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/kn2ss5.png
@=workshop/neubig-sensei/screenshot16.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._kn2ss5.png
@=photo/workshop/neubig-sensei/screenshot16.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 13.29.33.png
@=workshop/presentation/screenshot1.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 13.29.33.png
@=photo/workshop/presentation/screenshot1.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 14.27.45.png
@=workshop/presentation/screenshot2.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 14.27.45.png
@=photo/workshop/presentation/screenshot2.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/.DS_Store
@=workshop/presentation/DS_Store
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._.DS_Store
@=photo/workshop/presentation/DS_Store
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 14.40.33.png
@=workshop/presentation/screenshot3.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 14.40.33.png
@=photo/workshop/presentation/screenshot3.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 16.05.11.png
@=workshop/presentation/screenshot4.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 16.05.11.png
@=photo/workshop/presentation/screenshot4.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 15.42.30.png
@=workshop/presentation/screenshot5.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 15.42.30.png
@=photo/workshop/presentation/screenshot5.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 14.48.37.png
@=workshop/presentation/screenshot6.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 14.48.37.png
@=photo/workshop/presentation/screenshot6.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 16.06.53.png
@=workshop/presentation/screenshot7.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 16.06.53.png
@=photo/workshop/presentation/screenshot7.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 16.04.59.png
@=workshop/presentation/screenshot8.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 16.04.59.png
@=photo/workshop/presentation/screenshot8.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 16.06.59.png
@=workshop/presentation/screenshot9.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 16.06.59.png
@=photo/workshop/presentation/screenshot9.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 13.55.34.png
@=workshop/presentation/screenshot10.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 13.55.34.png
@=photo/workshop/presentation/screenshot10.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 16.06.59(1).png
@=workshop/presentation/screenshot11.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 16.06.59(1).png
@=photo/workshop/presentation/screenshot11.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 15.30.23.png
@=workshop/presentation/screenshot12.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 15.30.23.png
@=photo/workshop/presentation/screenshot12.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 13.25.05.png
@=workshop/presentation/screenshot13.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 13.25.05.png
@=photo/workshop/presentation/screenshot13.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 14.26.21.png
@=workshop/presentation/screenshot14.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 14.26.21.png
@=photo/workshop/presentation/screenshot14.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 13.20.25.png
@=workshop/presentation/screenshot15.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 13.20.25.png
@=photo/workshop/presentation/screenshot15.png
@ (comment above this line)
@ (zip file comment below this line)
```

long-names-edited ဆိုတဲ့ filename အသစ်နဲ့ သိမ်းခဲ့တယ်။  
ပြီးတော့ အောက်ပါ command နဲ့ zip ဖိုင်ကို ဝင် update လုပ်ခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$ zipnote -w ./3th\ Southeast\ Asian\ NLP_AI\ R\&D\ Workshop.zip < long-names-edited 
```

ဖြေပေးနိုင်ပြီ။ ဒါပေမဲ့ အောက်ပါအတိုင်း error ပေးတယ်...  

```
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$ unzip ./3th\ Southeast\ Asian\ NLP_AI\ R\&D\ Workshop.zip 
Archive:  ./3th Southeast Asian NLP_AI R&D Workshop.zip
   creating: workshop/
  inflating: photo/workshop          
   creating: workshop/yves-sensei/
checkdir error:  photo/workshop exists but is not directory
                 unable to process photo/workshop/yves-sensei/.
   creating: workshop/neubig-sensei/
checkdir error:  photo/workshop exists but is not directory
                 unable to process photo/workshop/neubig-sensei/.
   creating: workshop/presentation/
checkdir error:  photo/workshop exists but is not directory
                 unable to process photo/workshop/presentation/.
  inflating: workshop/yves-sensei/screenshot1.png  
checkdir error:  photo/workshop exists but is not directory
                 unable to process photo/workshop/yves-sensei/screenshot1.png.
  inflating: workshop/yves-sensei/screenshot2.png  
checkdir error:  photo/workshop exists but is not directory
                 unable to process photo/workshop/yves-sensei/screenshot2.png.
  inflating: workshop/yves-sensei/screenshot3.png  
checkdir error:  photo/workshop exists but is not directory
                 unable to process photo/workshop/yves-sensei/screenshot3.png.
  inflating: workshop/yves-sensei/screenshot4.png  
checkdir error:  photo/workshop exists but is not directory
                 unable to process photo/workshop/yves-sensei/screenshot4.png.
  inflating: workshop/yves-sensei/screenshot5.png  
checkdir error:  photo/workshop exists but is not directory
                 unable to process photo/workshop/yves-sensei/screenshot5.png.
  inflating: workshop/yves-sensei/screenshot6.png  
checkdir error:  photo/workshop exists but is not directory
                 unable to process photo/workshop/yves-sensei/screenshot6.png.
  inflating: workshop/yves-sensei/screenshot7.png  
checkdir error:  photo/workshop exists but is not directory
                 unable to process photo/workshop/yves-sensei/screenshot7.png.
```

အသစ်ရလာတဲ့ file, folder တွေကအောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$ tree -L 2
.
├── 3th Southeast Asian NLP_AI R&D Workshop.zip
├── chk-names
├── long-names
├── long-names-edited
├── original-long-names
├── photo
│   └── workshop
├── unzip-error.log.md
└── workshop
    ├── neubig-sensei
    ├── presentation
    └── yves-sensei

5 directories, 7 files
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$
```

png ပုံဖိုင်တွေကတော့ သက်ဆိုင်ရာ folder အောက်မှာ ရှိပေမဲ့ ငါထင်တယ် folder structure ဆောက်တဲ့ format မှာ တစ်ခုခုလွဲနေပြီလားလို့....  

## Update 

```
@ 3th Southeast Asian NLP:AI R&D Workshop/
@=workshop/
@ (comment above this line)
@ __MACOSX/._3th Southeast Asian NLP:AI R&D Workshop
@=photo/._workshop
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/
@=workshop/yves-sensei/
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/._Keynote#1_ Prof. Yves Lepage
@=photo/workshop/._yves-sensei/
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/
@=workshop/neubig-sensei/
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/._Keynote#2_ Assoc. Prof. Graham Neubig
@=photo/workshop/._neubig-sensei/
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/
@=workshop/presentation/
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/._Presentation Session
@=photo/workshop/._presentation/
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/Screen Shot 2564-12-21 at 10.05.58.png
@=workshop/yves-sensei/screenshot1.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/._Screen Shot 2564-12-21 at 10.05.58.png
@=photo/workshop/yves-sensei/._screenshot1.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/Screen Shot 2564-12-21 at 09.45.23.png
@=workshop/yves-sensei/screenshot2.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/._Screen Shot 2564-12-21 at 09.45.23.png
@=photo/workshop/yves-sensei/._screenshot2.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/Screen Shot 2564-12-21 at 09.38.34.png
@=workshop/yves-sensei/screenshot3.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/._Screen Shot 2564-12-21 at 09.38.34.png
@=photo/workshop/yves-sensei/._screenshot3.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/Screen Shot 2564-12-21 at 09.41.43.png
@=workshop/yves-sensei/screenshot4.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/._Screen Shot 2564-12-21 at 09.41.43.png
@=photo/workshop/yves-sensei/._screenshot4.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/Screen Shot 2564-12-21 at 10.05.34.png
@=workshop/yves-sensei/screenshot5.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/._Screen Shot 2564-12-21 at 10.05.34.png
@=photo/workshop/yves-sensei/._screenshot5.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/Screen Shot 2564-12-21 at 10.34.03.png
@=workshop/yves-sensei/screenshot6.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/._Screen Shot 2564-12-21 at 10.34.03.png
@=photo/workshop/yves-sensei/._screenshot6.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/Screen Shot 2564-12-21 at 09.35.45.png
@=workshop/yves-sensei/screenshot7.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/._Screen Shot 2564-12-21 at 09.35.45.png
@=photo/workshop/yves-sensei/._screenshot7.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/Screen Shot 2564-12-21 at 09.45.39.png
@=workshop/yves-sensei/screenshot8.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/._Screen Shot 2564-12-21 at 09.45.39.png
@=photo/workshop/yves-sensei/._screenshot8.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/Screen Shot 2564-12-21 at 10.34.12.png
@=workshop/yves-sensei/screenshot9.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/._Screen Shot 2564-12-21 at 10.34.12.png
@=photo/workshop/yves-sensei/._screenshot9.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/Screen Shot 2564-12-21 at 10.24.16.png
@=workshop/yves-sensei/screenshot10.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/._Screen Shot 2564-12-21 at 10.24.16.png
@=photo/workshop/yves-sensei/._screenshot10.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/Screen Shot 2564-12-21 at 10.16.06.png
@=workshop/yves-sensei/screenshot11.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#1_ Prof. Yves Lepage/._Screen Shot 2564-12-21 at 10.16.06.png
@=photo/workshop/yves-sensei/._screenshot11.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 10.47.50.png
@=workshop/neubig-sensei/screenshot1.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 10.47.50.png
@=photo/workshop/neubig-sensei/._screenshot1.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 11.47.08.png
@=workshop/neubig-sensei/screenshot2.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 11.47.08.png
@=photo/workshop/neubig-sensei/._screenshot2.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 10.51.33.png
@=workshop/neubig-sensei/screenshot3.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 10.51.33.png
@=photo/workshop/neubig-sensei/._screenshot3.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 11.20.34.png
@=workshop/neubig-sensei/screenshot4.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 11.20.34.png
@=photo/workshop/neubig-sensei/._screenshot4.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 10.47.26.png
@=workshop/neubig-sensei/screenshot5.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 10.47.26.png
@=photo/workshop/neubig-sensei/._screenshot5.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 11.20.25.png
@=workshop/neubig-sensei/screenshot6.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 11.20.25.png
@=photo/workshop/neubig-sensei/._screenshot6.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 10.53.57.png
@=workshop/neubig-sensei/screenshot7.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 10.53.57.png
@=photo/workshop/neubig-sensei/._screenshot7.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 10.47.34.png
@=workshop/neubig-sensei/screenshot8.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 10.47.34.png
@=photo/workshop/neubig-sensei/._screenshot8.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 11.09.56.png
@=workshop/neubig-sensei/screenshot9.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 11.09.56.png
@=photo/workshop/neubig-sensei/._screenshot9.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 10.49.02.png
@=workshop/neubig-sensei/screenshot10.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 10.49.02.png
@=photo/workshop/neubig-sensei/._screenshot10.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/kn2group.png
@=workshop/neubig-sensei/screenshot11.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._kn2group.png
@=photo/workshop/neubig-sensei/._screenshot11.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 11.09.46.png
@=workshop/neubig-sensei/screenshot12.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 11.09.46.png
@=photo/workshop/neubig-sensei/._screenshot12.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 10.51.16.png
@=workshop/neubig-sensei/screenshot13.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 10.51.16.png
@=photo/workshop/neubig-sensei/._screenshot13.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/kn2ss2.png
@=workshop/neubig-sensei/screenshot14.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._kn2ss2.png
@=photo/workshop/neubig-sensei/._screenshot14.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/Screen Shot 2564-12-21 at 11.27.46.png
@=workshop/neubig-sensei/screenshot15.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._Screen Shot 2564-12-21 at 11.27.46.png
@=photo/workshop/neubig-sensei/._screenshot15.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/kn2ss5.png
@=workshop/neubig-sensei/screenshot16.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Keynote#2_ Assoc. Prof. Graham Neubig/._kn2ss5.png
@=photo/workshop/neubig-sensei/._screenshot16.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 13.29.33.png
@=workshop/presentation/screenshot1.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 13.29.33.png
@=photo/workshop/presentation/._screenshot1.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 14.27.45.png
@=workshop/presentation/screenshot2.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 14.27.45.png
@=photo/workshop/presentation/._screenshot2.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/.DS_Store
@=workshop/presentation/.DS_Store
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._.DS_Store
@=photo/workshop/presentation/._.DS_Store
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 14.40.33.png
@=workshop/presentation/screenshot3.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 14.40.33.png
@=photo/workshop/presentation/._screenshot3.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 16.05.11.png
@=workshop/presentation/screenshot4.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 16.05.11.png
@=photo/workshop/presentation/._screenshot4.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 15.42.30.png
@=workshop/presentation/screenshot5.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 15.42.30.png
@=photo/workshop/presentation/._screenshot5.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 14.48.37.png
@=workshop/presentation/screenshot6.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 14.48.37.png
@=photo/workshop/presentation/._screenshot6.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 16.06.53.png
@=workshop/presentation/screenshot7.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 16.06.53.png
@=photo/workshop/presentation/._screenshot7.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 16.04.59.png
@=workshop/presentation/screenshot8.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 16.04.59.png
@=photo/workshop/presentation/._screenshot8.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 16.06.59.png
@=workshop/presentation/screenshot9.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 16.06.59.png
@=photo/workshop/presentation/._screenshot9.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 13.55.34.png
@=workshop/presentation/screenshot10.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 13.55.34.png
@=photo/workshop/presentation/._screenshot10.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 16.06.59(1).png
@=workshop/presentation/screenshot11.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 16.06.59(1).png
@=photo/workshop/presentation/._screenshot11.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 15.30.23.png
@=workshop/presentation/screenshot12.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 15.30.23.png
@=photo/workshop/presentation/._screenshot12.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 13.25.05.png
@=workshop/presentation/screenshot13.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 13.25.05.png
@=photo/workshop/presentation/._screenshot13.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 14.26.21.png
@=workshop/presentation/screenshot14.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 14.26.21.png
@=photo/workshop/presentation/._screenshot14.png
@ (comment above this line)
@ 3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/Screen Shot 2564-12-21 at 13.20.25.png
@=workshop/presentation/screenshot15.png
@ (comment above this line)
@ __MACOSX/3th Southeast Asian NLP:AI R&D Workshop/Presentation Session/._Screen Shot 2564-12-21 at 13.20.25.png
@=photo/workshop/presentation/._screenshot15.png
@ (comment above this line)
@ (zip file comment below this line)
```

## Rewrite Zip File

အရင် update လုပ်ထားပြီးသား zip ဖိုင်ကို ဖျက်ရမယ်...  
```
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$ rm ./3th\ Southeast\ Asian\ NLP_AI\ R\&D\ Workshop.zip 
```

zip ဖိုင်ကို ပြန် download လုပ်ပြီးတော့ လက်ရှိ folder ဆီကို ပြန်ရွှေ့ခဲ့...  
```
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$ mv ~/Downloads/3th\ Southeast\ Asian\ NLP_AI\ R\&D\ Workshop.zip .
```

Rewrite ပြန်လုပ်ခဲ့...  

```
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$ zipnote -w ./3th\ Southeast\ Asian\ NLP_AI\ R\&D\ Workshop.zip < long-names-edited2
```

## Unzip Again

unzip မလုပ်ခင်မှာ စောစောက ဖြေလို့ ရထားတဲ့ photo တွေကိုတော့ လိုရမယ်ရ backup လုပ်ထားခဲ့...  

```
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$ mkdir bk
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$ mv workshop/ ./bk/
```

unzip ပြန်လုပ်ကြည့်...  

```
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$ unzip ./3th\ Southeast\ Asian\ NLP_AI\ R\&D\ Workshop.zip 
Archive:  ./3th Southeast Asian NLP_AI R&D Workshop.zip
   creating: workshop/
  inflating: photo/._workshop        
   creating: workshop/yves-sensei/
   creating: photo/workshop/._yves-sensei/
   creating: workshop/neubig-sensei/
   creating: photo/workshop/._neubig-sensei/
   creating: workshop/presentation/
   creating: photo/workshop/._presentation/
  inflating: workshop/yves-sensei/screenshot1.png  
  inflating: photo/workshop/yves-sensei/._screenshot1.png  
  inflating: workshop/yves-sensei/screenshot2.png  
  inflating: photo/workshop/yves-sensei/._screenshot2.png  
  inflating: workshop/yves-sensei/screenshot3.png  
  inflating: photo/workshop/yves-sensei/._screenshot3.png  
  inflating: workshop/yves-sensei/screenshot4.png  
  inflating: photo/workshop/yves-sensei/._screenshot4.png  
  inflating: workshop/yves-sensei/screenshot5.png  
  inflating: photo/workshop/yves-sensei/._screenshot5.png  
  inflating: workshop/yves-sensei/screenshot6.png  
  inflating: photo/workshop/yves-sensei/._screenshot6.png  
  inflating: workshop/yves-sensei/screenshot7.png  
  inflating: photo/workshop/yves-sensei/._screenshot7.png  
  inflating: workshop/yves-sensei/screenshot8.png  
  inflating: photo/workshop/yves-sensei/._screenshot8.png  
  inflating: workshop/yves-sensei/screenshot9.png  
  inflating: photo/workshop/yves-sensei/._screenshot9.png  
  inflating: workshop/yves-sensei/screenshot10.png  
  inflating: photo/workshop/yves-sensei/._screenshot10.png  
  inflating: workshop/yves-sensei/screenshot11.png  
  inflating: photo/workshop/yves-sensei/._screenshot11.png  
  inflating: workshop/neubig-sensei/screenshot1.png  
  inflating: photo/workshop/neubig-sensei/._screenshot1.png  
  inflating: workshop/neubig-sensei/screenshot2.png  
  inflating: photo/workshop/neubig-sensei/._screenshot2.png  
  inflating: workshop/neubig-sensei/screenshot3.png  
  inflating: photo/workshop/neubig-sensei/._screenshot3.png  
  inflating: workshop/neubig-sensei/screenshot4.png  
  inflating: photo/workshop/neubig-sensei/._screenshot4.png  
  inflating: workshop/neubig-sensei/screenshot5.png  
  inflating: photo/workshop/neubig-sensei/._screenshot5.png  
  inflating: workshop/neubig-sensei/screenshot6.png  
  inflating: photo/workshop/neubig-sensei/._screenshot6.png  
  inflating: workshop/neubig-sensei/screenshot7.png  
  inflating: photo/workshop/neubig-sensei/._screenshot7.png  
  inflating: workshop/neubig-sensei/screenshot8.png  
  inflating: photo/workshop/neubig-sensei/._screenshot8.png  
  inflating: workshop/neubig-sensei/screenshot9.png  
  inflating: photo/workshop/neubig-sensei/._screenshot9.png  
  inflating: workshop/neubig-sensei/screenshot10.png  
  inflating: photo/workshop/neubig-sensei/._screenshot10.png  
  inflating: workshop/neubig-sensei/screenshot11.png  
  inflating: photo/workshop/neubig-sensei/._screenshot11.png  
  inflating: workshop/neubig-sensei/screenshot12.png  
  inflating: photo/workshop/neubig-sensei/._screenshot12.png  
  inflating: workshop/neubig-sensei/screenshot13.png  
  inflating: photo/workshop/neubig-sensei/._screenshot13.png  
  inflating: workshop/neubig-sensei/screenshot14.png  
  inflating: photo/workshop/neubig-sensei/._screenshot14.png  
  inflating: workshop/neubig-sensei/screenshot15.png  
  inflating: photo/workshop/neubig-sensei/._screenshot15.png  
  inflating: workshop/neubig-sensei/screenshot16.png  
  inflating: photo/workshop/neubig-sensei/._screenshot16.png  
  inflating: workshop/presentation/screenshot1.png  
  inflating: photo/workshop/presentation/._screenshot1.png  
  inflating: workshop/presentation/screenshot2.png  
  inflating: photo/workshop/presentation/._screenshot2.png  
  inflating: workshop/presentation/.DS_Store  
  inflating: photo/workshop/presentation/._.DS_Store  
  inflating: workshop/presentation/screenshot3.png  
  inflating: photo/workshop/presentation/._screenshot3.png  
  inflating: workshop/presentation/screenshot4.png  
  inflating: photo/workshop/presentation/._screenshot4.png  
  inflating: workshop/presentation/screenshot5.png  
  inflating: photo/workshop/presentation/._screenshot5.png  
  inflating: workshop/presentation/screenshot6.png  
  inflating: photo/workshop/presentation/._screenshot6.png  
  inflating: workshop/presentation/screenshot7.png  
  inflating: photo/workshop/presentation/._screenshot7.png  
  inflating: workshop/presentation/screenshot8.png  
  inflating: photo/workshop/presentation/._screenshot8.png  
  inflating: workshop/presentation/screenshot9.png  
  inflating: photo/workshop/presentation/._screenshot9.png  
  inflating: workshop/presentation/screenshot10.png  
  inflating: photo/workshop/presentation/._screenshot10.png  
  inflating: workshop/presentation/screenshot11.png  
  inflating: photo/workshop/presentation/._screenshot11.png  
  inflating: workshop/presentation/screenshot12.png  
  inflating: photo/workshop/presentation/._screenshot12.png  
  inflating: workshop/presentation/screenshot13.png  
  inflating: photo/workshop/presentation/._screenshot13.png  
  inflating: workshop/presentation/screenshot14.png  
  inflating: photo/workshop/presentation/._screenshot14.png  
  inflating: workshop/presentation/screenshot15.png  
  inflating: photo/workshop/presentation/._screenshot15.png  
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$
```

## Check the Output Folder and Files

```
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$ tree -L 2 .
.
├── 3th Southeast Asian NLP_AI R&D Workshop.zip
├── bk
│   └── workshop
├── chk-names
├── long-names
├── long-names-edited
├── long-names-edited2
├── original-long-names
├── photo
│   └── workshop
├── unzip-error.log.md
└── workshop
    ├── neubig-sensei
    ├── presentation
    └── yves-sensei

8 directories, 7 files
(base) ye@:/media/ye/project2/photo/iSAI-NLP2021/from-jip$
```

ဘာကြောင့် photo/workshop ရှိပြီး သပ်သပ် workshop/ ဖြစ်နေတာလည်း ဆိုတာကို သိပ်မရှင်းဘူး...  
သို့သော် zip ဖိုင်ကို ဖြေလို့ ရသွားတာမို့ solution တော့ ဖြစ်သွားပြီ။ အချိန်မရှိလို့ ဒီမှာပဲ ရပ်ထားလိုက်တော့မယ်...  


## Reference

- [https://askubuntu.com/questions/915041/how-to-rename-extract-files-with-long-names-in-zip-archive](https://askubuntu.com/questions/915041/how-to-rename-extract-files-with-long-names-in-zip-archive)  

