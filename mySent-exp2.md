## My Sentence Breaking with +Paragraph

### Check the Data

I found some manual tagging errors such as follows:  

```
472: မင်း/B သဘောပေါက်/O အောင်/O ယုန်/O တောင်/O ပြNး/O ခွေး/O မြောက်/O လိုက်/E ဆို/O တဲ့/O စကားပုံ/N နဲ့/N ရှင်းပြ/N မယ်/E
768: ရ/B ပါ/N ပြီ/N ခင်ဗျာ/E ဒီ/B မှာ/O အမေရိကန်/O ဒေါ်လာ/O ၁/O ဒေါ်လာ/O ကို/O ၁၃၅၀/O နှုန်း/O နဲN/O မNန်မာ/N ငွေ/OEစုစုပေါင်း/B ၆၇၅၀၀၀/N ပါ/N ခင်ဗျာ/E
827: မျNးသောအEးဖြင့်/B လူငယ်/O တွေ/O ဆီ/O က/O ပေါ်ပေါက်/N လာ/N တာ/N ပါ/E မင်း/B တို့/O ကြား/N ဖူး/N ပါ/N တယ်/E ပဲ/B များ/O တယ်/O ဆို/N တဲ့/N စကား/N လေ/E
```

Why /E tags are tagging in wrong positions?!  
```
1162: နောက်ဆုNး/B ၌/O ဗိုလ်/O လရေNင်/E ခေါ်/O ဦးမင်းရောင်/E အား/O ဗြိတိသျှ/O တို့/O က/O ဖမ်းဆီး/O သတ်ဖြတ်/N လိုက်/N ပါ/N သည်/E
1035: ဘE/B ဖြစ်/B လို့/ONဒီ/O လို/E အစောကြီး/NBပြန်လEN တာ/N လE/E
2236: သူငယ်ချင်း/E က/OB မ/O တွေ့/O တာ/O အတော်ကြာ/O လို့/O တွေ့/O ရအောင်/O ပြော/O တဲ့/O အချိန်/O မှာ/O အခြား/O ချိန်းထား/O တာ/O ရှိ/O ရင်/N ဘယ်လို/N လုပ်/N မလဲ/E
```

Word segmentation error:  

```
3095: အခု/B ဂျပန်/O နိုင်ငံ/O မှာ/O Omicron/O အမျိုးအစား/O မျိုး/O ဗီဇ/O ပြောင်း/O ကိုရိုနာ/O ဗိုင်းရပ်စ်ကျယ်ကျယ်ပြန့်ပြန့်ကူးစက်/O ပြန့်ပွား/O မှု/O တွေ/O ဖြစ်/N နေ/N ပါ/N တယ်/E အခု/B အချိန်/O မှာ/O Hinoki/O လို့/O ခေါ်/O တဲ့/O ထင်းရှူးပင်/O က/O ပန်းဝတ်မှုန်/O တွေ/O ပျံ့လွင့်/O နေ/O တာ/O ကြောင့်/O ရာသီ/O ပေါ်/O ရောဂါ/O တစ်/O မျိုး/O ဖြစ်/O တဲ့/O ပန်းဝတ်မှုန်/O နဲ့/O ဓာတ်မတည့်/O တဲ့/O ရောဂါ/O လည်း/O အဖြစ်/O များ/O နေ/N ကြ/N ပါ/N တယ်/E
It should be: ဗိုင်းရပ်စ်/O ကျယ်ကျယ်ပြန့်ပြန့်/O ကူးစက်/O
```

```
3466: အပြီး/B သတ်/O စစ်ဆေး/O မှု/O ရလဒ်/O ထွက်/O တဲ့/O အထိ/O ခန့်မှန်းခြေကြာမြင့်ချိန်/O က/O ၁၂/O နာရီ/O လောက်/N ရှိ/N ပါ/N မယ်/E တကယ်/B လို့/O အဲဒီ/O တံတွေးPCR/O စစ်ဆေး/O မှု/O မှာ/O လည်းပိုး/O မ/O ရှိ/O ကြောင်း/O မ/O သေချာ/O တာ/O ဒါမှမဟုတ်/O ဗိုင်းရပ်စ်ပိုး/O တွေ့/O ရှိ/O တာ/O စတဲ့/O ရလဒ်/O ထွက်/O ပေါ်/O မယ်/O ဆို/O ရင်/O နှာခေါင်း/O အနောက်/O ဘက်/O က/O အရည်/O ကို/O တို့/O ဖတ်/O ယူ/O ပြီး/O ထပ်မံ/O စစ်ဆေး/O မှု/O ခံ/O ရယူ/O မှာ/N ဖြစ်/N ပါ/N တယ်/E ဒီလို/B ထပ်မံ/O စစ်ဆေး/O မှု/O ခံယူ/O တာ/O ကို/O အိုလံပစ်/O နဲ့/O ပါရာလင်း/O ပစ်/O အားကစား/O ရွာ/O မှာ/O ရှိ/O တဲ့/O COVID19/O ဆေးခန်း/O မှာ/O ပြုလုပ်/O ရ/O မှာ/N ဖြစ်/N ပါ/N တယ်/E ဗိုင်းရပ်စ်ပိုး/B မ/O ရှိ/O ကြောင်း/O ရလဒ်/O ထွက်/O လာ/O မှ/O သာ/O အဲဒီ/O သူ/O ဟာ/O အိုလံပစ်/O အားကစားပွဲ/O မှာ/O ပါဝင်/O ယှဉ်ပြိုင်ခွင့်/O ရ/O မှာ/N ဖြစ်/N ပါ/N တယ်/E
It should be ... eg: ခန့်မှန်းခြေ/O ကြာမြင့်ချိန်/O
```

```
4383: တစ်ရက်ဂယ်လီလီယို/B တစ်/O ယောက်/O ဘုရားကျောင်း/O မှာ/O ဝတ်ပြု/O ရင်း/O မီးဆိုင်းကြီး/O ရမ်း/O နေပုံ/O ကို/N သတိပြု/N မိ/N တယ်/E မီးဆိုင်း/B ဟာ/O လွှဲချိန်/O period/O မှန်မှန်/O နဲ့/O ရမ်း/O နေ/O တာ/N ဖြစ်/N ပါ/N တယ်/E ဒါ/B ကို/O သွေးခုန်နှုန်း/O ကို/O အချိန်မှတ်/O အနေ/O နဲ့/O အသုံးပြု/O ပြီး/O သူ/O က/N စမ်းသပ်/N ခဲ့/N တယ်/E မီးဆိုင်း/B လို/O ပဲ/O ချိန်သီး/O က/O လည်း/O လွှဲချိန်/O မှန်မှန်/O နဲ့/O ရိုးရိုး/O စည်းချက်ကျ/O ရွေ့လျား/O ခြင်း/O ကို/O ဖြစ်/O စေ/O တယ်/O ဆို/O တာ/O စမ်းသပ်/O ချက်/O တွေ/O အရ/O သတိထား/O မိ/N သွား/N ပါ/N တယ်/E
It should be: တစ်ရက်/B ဂယ်လီလီယို/O
```

```
4801: အတွေးဝါထုတ်လုပ်/B လိုက်/O တဲ့/O ပုံရိပ်/O က/O အာရုံ/O ကို/O ကျော်/O သွား/O ပြီ/O ဆို/O ရင်/O တော့/O ဒါ/O အာသီ/O သ/N ဖြစ်/N သွား/N ပြီ/E အာရုံ/B သည်/N အာသီသမ/N ဟုတ်/N ဘူး/E အာရုံ/B က/N အာရုံ/N ပဲ/E ဒါပေမဲ့/B အတွေးဝင်/O လာ/O ပြီး/N ပြည့်စုံ/N ချင်/N တယ်/E အဲ့ဒီ/B မှာ/O အာသီ/O သ/N ဖြစ်/N သွား/N ပြီ/E တကယ်/B တော့/N အချက်အလက်/N ပဲ/E သဘောတရားမ/B ဟုတ်/N ဘူး/E ဒါ/B က/N အချက်အလက်/N တစ်/N ခု/E
It should be: အတွေး/B ဝါ/O ထုတ်လုပ်/O
```

```
5021: ထို/B သို့/O ချိန်/O ထား/O မည်/O ဆို/O လျှင်/O ထို/O ဒြပ်ထု/O နှစ်/O ခု/O သည်မီးရှို့/O ပြီး/O သောအခါ/O တွင်/O ဖြစ်ပေါ်/O လာ/O သော/O ထို/O ကျောက်မီးသွေး/O ပြာ၏/O ဒြပ်ထုအခြား/O ဖြစ်ပေါ်/O လာ/O သော/O အရာဝတ္ထု/O များ/O ၏/O ဒြပ်ထု/O နှင့်လောင်ကျွမ်း/O ရာတွင်/O ဖြစ်ပေါ်/O လာ/O သော/O ဓာတ်ငွေ့/O အားလုံး/O ၏ဒြပ်ထု/O တို့/O ၏/O ပေါင်း/O ခြင်း/O နှင့်/O တူ/O သည်/O ကို/O တွေ့/O ရ/N မည်/N ဖြစ်/N ၏/E တ/B နည်း/O ဆို/O လျှင်/O ဒြပ်/O ကို/O အဖြစ်/O အမျိုးမျိုး/O သို့/O ပြောင်းလဲ/O ပေး/O နိုင်သော်လည်း/O ဒြပ်/O ကို/O မ/O ဖျက်ဆီး/O နိုင်/O ရုံမျှမက/O ဒြပ်/O ၏/O ဒြပ်ထု/O ကိုလည်း/O တိုး/O အောင်လျော့/O အောင်/O မ/N ပြုလုပ်/N နိုင်/N ချေ/E မိုမင်တမ်/B ခေါ်/O အဟုန်/O သည်/O ရွေ့ရှား/O မှု/N ၏/N အတိုင်းအဆဖြစ်/N ၏/E
It shoulde be: သည်/O မီးရှို့/O
```

```
3869: သတင်းစာရှင်းလင်းပွဲ/B တစ်/O ခု/O မှာ/O အစိုးရ/O ရဲ့/O အကြံပေး/O အဖွဲ့/O ခေါင်းဆောင်အိုးမိရှီဂဲရုOmiShigeruက/O နတ်/O ကွန်း/O တွေ/O နဲ့/O ဘုရား/O ကျောင်း/O တွေ/O ရဲ့/O ကျောင်းဝင်း/O ထဲ/O မှာ/O ဘုရား/O ကျောင်း/O ရှေ့/O မှာ/O ရပ်/O ပြီး/O တိတ်ဆိတ်/O စွာ/O ဝတ်ပြု/O ဆုတောင်း/O တာ/O က/O ကြီးမား/O တဲ့/O ကူးစက်မှု/O အန္တရာယ်/O မ/O ရှိ/O ဘူး/O လို့/N ပြော/N ပါ/N တယ်/E ဒါပေမဲ့/B ဘုရား/O ကျောင်း/O နဲ့/O နတ်/O ကွန်း/O တွေ/O ကို/O မ/O လာ/O ခင်/O ဒါမှမဟုတ်/O လာ/O ပြီး/O တော့/O မှ/O သူငယ်ချင်း/O တွေ/O ဆွေမျိုး/O တွေ/O နဲ့/O အတူတွေ့ဆုံ/O ပြီး/O အစားစား/O တာ/O အရက်သေစာ/O သောက်/O တာ/O စကား/O ပြောဆို/O တာ/O တွေ/O လုပ်/O ရင်/O တော့/O ကူးစက်မှု/O အန္တရာယ်/O ကြီး/O နိုင်/O တဲ့/O အတွက်/O လူ/O တွေ/O အနေနဲ့/O သတိပြု/O သင့်/O တယ်/O လို့/N ဆို/N ပါ/N တယ်/E
3900: Nihon/B တက္ကသိုလ်/O ဆေး/O ပညာ/O ဌာန/O က/O ပါမောက္ခ/O စာ/O တိုး/O ရှိ/O ဟာယာခါဝါSatoshiHayakawa/O က/O စစ်တမ်း/O ရဲ့/O အဓိက/O အချက်/O တွေ/O ကိုအတူ/O လေ့လာ/O ခဲ့/O ရာ/O မှာ/O သန္ဓသား/O ကြီးထွား/O လာ/O တာ/O နဲ့/O အမျှ/O ကိုယ်ဝန်ရင့်/O လာ/O တဲ့/O အမျိုးသမီး/O တွေ/O ရဲ့/O အဆုတ်/O ဟာ/O အလုပ်/O ပို/O လုပ်/O ရ/O တဲ့/O အတွက်/O အဆုတ်/O က/O ပင်ပန်း/O လာ/O ပြီး/O တကယ်/O လို့/O အဆုတ်/O ရောင်/O ရောဂါ/O ဖြစ်/O လာ/O မယ်/O ဆို/O ရင်/O ကိုဗစ်/O ရောဂါ/O လက္ခဏာ/O တွေ/O ပြင်းထန်/O လာ/O နိုင်/O ပါ/O တယ်/O လို့/N ပြော/N ပါ/N တယ်/E ပါမောက္ခဟာယာခါဝါ/B က/O စစ်တမ်း/O ရလဒ်/O တွေ/O ဟာ/O သူ/O တို့/O မျှော်လင့်/O ထား/O တဲ့/O အတိုင်း/O ဖြစ်/O လာ/O ခဲ့/O တယ်/O လို့/N ပြော/N ပါ/N တယ်/E ကိုယ်ဝန်ဆောင်/B အမျိုးသမီး/O တွေ/O မှာ/O အသည်း/O အသန်/O နေမကောင်း/O ဖြစ်/O တာ/O က/O အနည်းငယ်/O ပဲ/O ရှိ/O တဲ့/O အတွက်/O အလွန်အမင်း/O စိုးရိမ်ကြောက်ရွံ့/O စရာ/O မ/O လို/O ပါ/O ဘူး/O လို့/O ပါမောက္ခဟာယာခါဝါ/O က/N ပြော/N ပါ/N တယ်/E ဒါပေမဲ့/B ဗိုင်းရပ်စ်ပိုး/O မ/O ကူးစက်/O အောင်/O ကာကွယ်/O ဖို့/O တော့/O ဂရုစိုက်/O သင့်/O တယ်/O လို့ဖြည့်စွက်/O ပြောကြား/N ထား/N ပါ/N တယ်/E
```

```
5264: ကွန်ပျု/B တာ/O များ/O အင်တာနက်/O အတွင်း/O ၌/O အချင်းချင်း/O ဆက်သွယ်/O ခြင်း/O မှာ/O ဆက်သွယ်/O ရေး/O စနစ်/O ၏/O ထင်ရှား/O သော/O ဥပမာ/O တစ်/N ခု/N ဖြစ်/N သည်/E အမည်ရင်း/B မြစ်အင်္ဂလိပ်/O အခေါ်အဝေါ်/O ဆို/O သော/O စကားလုံး/O မှာ/O ပြင်သစ်/O စကားလုံး/O éé/O မှ/O ရယူ/O ထား/N ခြင်း/N ဖြစ်/N သည်/E
It should be: ကွန်ပျုတာ/B များ/O
```

```
5299: သရက်/B သင်္ဘော/O ကုက္/O ကိုကျွန်း/O အင်သစ်ချထင်းရူးအစ/O ရှိ/O သည့်အပင်/O များ/O ၌/O တွယ်ကပ်/O ပေါက်ရောက်/O ခြင်း/O များပြား/O ၍သစ်ပင်/O အခေါက်/O ချောမွေ့/O ခြင်းကြမ်းတမ်း/O ခြင်း/O တို့/O ၌/O လည်းသစ်ခွ/O တစ်/O မျိုး/O နှင့်/O တစ်/O မျိုး/O နှစ်သက်/O ပုံ/N မ/N တူ/N ချေ/E သစ်ပင်/B များ/O ၌/O တွယ်ကပ်/O ပေါက်ရောက်/O ကြ/O သော်လည်းသစ်ခွ/O ပင်/O အများအပြား/O စိုက်ပျိုး/O လို/O သူ/O တို့/O အတွက်ပန်းအိုး/O များ/O ဖြင့်/O ထည့်/O ၍/O စိုက်ပျိုး/O ခြင်း/O သည်ပို/N ၍/N အဆင်ပြေ/N သည်/E
It should be: ကုက္ကိုကျွန်း/O
```

```
5435: လူ/B သာမာ/N တင်း/E ဥရောပ/B ရှိ/O အခြား/O နိုင်ငံ/O များ/O ၌/O လည်း/O မာ/O တင်/O လူ/O သာ/O ဆောင်ရွက်ပုံ/O ကိုအားကျ/O ကြ/O သဖြင့်/O ပရိုတက်စတန့်/O ဂိုဏ်း/N တည်ထောင်/N ကြ/N သည်/E လူ/B တို့/O စိတ်ဓာတ်/O ပြောင်း/O လာ/O သည်/O နှင့်/O အမျှ/O တိုင်းပြည်/O အုပ်ချုပ်/O ရေး/O လည်း/O ပြောင်း/N လာ/N လေ/N သည်/E
It should be: လူသာမာတင်း/E
```

```
5622: လုံး/B ⁠/O လုံး/O လွတ်လပ်/O တဲ့/O ကိစ္စ/O ပြီးပြတ်/O သည်/O အထိ/O ကြိုးစား/O ပါ/O မယ်/O ’/O ဟု/O ပြောကြား/N ခဲ့/N လေ/N သည်/E ဘဝ/B နိဂုံး၁၉၄၇/O ခုနှစ်/O ဇူလိုင်/O လ/O ၁၉/O ရက်နေ့/O တွင်/O ရန်ကုန်/O မြို့/O ရှိ/O အတွင်းဝန်/O များ/O ရုံး/O ၌/O နိုင်ငံ/O ရေး/O တွင်/O အလွန်/O အရေးပါ/O သော/O ခေါင်းဆောင်/O ကြီး/O များ/O အာဇာနည်/O ကိုး/O ဦး/O တို့/O နှင့်/O အတူ/O လုပ်ကြံ/O ခြင်း/O ခံ/O ခဲ့/O ရ/O ပြီး/N ကျဆုံး/N ခဲ့/N သည်/E အမွေအနှစ်/B ‌စကော့/O ဈေး/O နှင့်/O ကော်မရှင်နာ/O လမ်း/O များ/O ကို/O လည်း/O ဗိုလ်ချုပ်/O အောင်ဆန်း/O ဈေး/O နှင့်/O ဗိုလ်ချုပ်/O အောင်ဆန်း/O လမ်း/O များ/O အဖြစ်/O လွတ်လပ်ရေး/O နောက်ပိုင်း/O တွင်/O ပြောင်းလဲ/O မှည့်/N ခေါ်/N ခဲ့/N သည်/E
It should be: လုံး/B လုံး/O
```

```
6290: ဟွန်း/E ညည်း/B က/N ကောင်းခန်းဆိုဖြတ်/N ပြီ/E ပွဲတော်ကွင်း/B ထဲ/O တုန်း/O က/O ပြ/O တဲ့/O ဘိုင်စကုတ်ကျ/N နေ/N တာ/N ပဲ/E
It should be: ကောင်းခန်း/O ဆို/O ဖြတ်/N
```

```
6346: တစ်ခါတစ်/B လေ/O ကို/O စီ/O ဖောင်း/O ရွာ/O ပြန်/O လာ/O လို့/O စစ်ဘောင်းဘီ/O တိုအိတ်/O ထဲ/O က/O မိန်းမသား/O ဓာတ်ပုံ/O တွေ/O တွေ့/O တော့/O လည်း/O ဘယ်/O က/O မိန်းမလည်း/O ဘယ်လို/O ပက်သပ်/O တာ/O လည်း/O တစ်/O ခွန်း/N မ/N မေး/N ဘူး/E သည်/B မိန်းမ/O သည်/O ဓာတ်ပုံ/O ဘယ်/O မှာ/O ရိုက်/N တာ/N ပါ/N လိမ့်/E ကျုပ်/B တောင်/O ဓာတ်ပုံရိုက်/O ချင်/O သေး/O ဆို/O တာ/O လောက်/N ပြော/N တာ/N ပါ/E
It should be: တစ်ခါတစ်လေ/B ကို/O
```

```
6596: လက်ပဒေါကို/B ငှက်စုန်းဖြတ်/O သွား/O ပြီး/O လူ/O တွေ/O အားလုံး/O လောက်/O အိပ်မောကျ/O နေ/O ချိန်/O မှာ/O လှတင်/O ကြွက်/O ထိုး/O တဲ့/O မှိန်း/O ကို/O ထောက်/O ရင်း/O သူ့/O တဲ/O ကို/O ပြန်/N ရောက်/N လာ/N တယ်/E
It should be: လက်ပဒေါ/B ကို/O ငှက်စုန်း/O ဖြတ်/O သွား/O
```

```
6707: ဖွေး/B လက်တောက်ပ/O နေ/O သည့်သည်/O ဝတ်စုံ/O ပေါ်/O မှ/O ကြယ်/O ပွင့်/O လက်/O လက်ကလေး/O တွေ/O က/O ဖြိုးဖြိုးပြက်ပြက်/O ရှိ/O နေ/N ပေ/N လိမ့်/N မည်/E နောက်အပြာနုရောင်/B ကို/O ဖယ်ကြဉ်/O ၍/O အဖြူရောင်/O ဝတ်စုံ/O ကို/O သက်မောင်/O တွေ့/O လျှင်/O သူ/N မ/N ကျေနပ်/N ပြီ/E
It should be: ဖွေးလက်တောက်ပ/B နေ/O သည့်/O သည်/O ဝတ်စုံ/O
```

```
6721: အချို့/B အပိတ်တော်တော်လေး/N သေသပ်/N သည်/E သည်/B ဒိုးဆစ်ကြား/O မှာ/O ခင်/O သက်ရီ/O ဘယ်လို/O က/O နေ/O သည်/O ကို/O သူ့/O စိတ်/O မှာ/O ရုပ်မြင်သံကြား/O လို/N မြင်/N နေမိ/N သည်/E
It should be: အချို့/B အပိတ်/N တော်တော်လေး/N သေသပ်/N သည်/E
```

```
6725: သက်မောင်ဝုန်းခနဲ/B ထ/N ထိုင်/N လိုက်/N သည်/E သည်/B စကား/O သည်/O စင်/O ပေါ်/O မှာ/O ပြော/O ရ/O မည့်/O စကားစု/O တွင်/O ပါ/N နေကျ/N မ/N ဟုတ်/E
It should be: သက်မောင်/B ဝုန်းခနဲ/O ထ/N ထိုင်/N လိုက်/N သည်/E
```

Shouldn't combined Burmese and English words  

```
More than one spaces:
816: ကျန်/B  တာ/O ခင်ဗျား/O မိတ်ဆွေ/O ကို/E ပြန်ယူ/B သွား/N ခိုင်း/N ပါ/E
```

## Shuffling and Splitting Word and Tags

```
root@85f02f4cfa85:/home/ye/exp/mysent/data-para# wc ./paragraph.txt
   8464  353339 5655932 ./paragraph.txt
root@85f02f4cfa85:/home/ye/exp/mysent/data-para# wc ./paragraph.txt.error
   8465  353328 5655900 ./paragraph.txt.error
root@85f02f4cfa85:/home/ye/exp/mysent/data-para#
```

I will used roughly cleaning data by myself (i.e. paragraph.txt).  

```
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# ls
paragraph.txt
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# shuf ./paragraph.txt > ./paragraph.txt.shuf
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# head ./paragraph.txt.shuf
နိုင်ငံတော်/B အလံ/O ကို/O လည်း/O ယခင်/O နိုင်ငံတော်/O အေးချမ်းသာယာ/O ရေး/O နှင့်/O ဖွံ့ဖြိုးရေး/O ကောင်စီ/O အစိုးရ/O လက်ထက်/O ၂၀⁠၀၈/O ခုနှစ်/O တွင်/O ပြဋ္ဌာန်း/O ခဲ့/O သော/O ဖွဲ့စည်းပုံ/O အခြေခံ/O ဥပဒေ/O ၂၀၀၈/O တွင်/O သတ်မှတ်/O ထား/O သည့်/O နိုင်ငံတော်/O အလံ/O ဖြင့်/O အစားထိုး/O ၍/O ပြောင်းလဲ/N အသုံးပြု/N ခဲ့/N သည်/E ဝေါဟာရ/B ဗေဒ၁၉၈၉/O ခုနှစ်/O တွင်/O စစ်/O အစိုးရ/O က/O အင်္ဂလိပ်/O ဘာသာ/O ဖြင့်/O ‌/O ဘားမား/O ကို/O မြန်မာ/O ဟု/O ပြောင်းလဲ/O ရန်/O ဆုံးဖြတ်/O ခဲ့/O ခြင်း/O သည်/O အငြင်းပွား/O စရာ/N ဖြစ်/N ခဲ့/N သည်/E
မောင်/B ဟူသော/O စကားလုံး/O သည်/O အဓိပ္ပာယ်/N အမျိုးမျိုး/N ရှိ/N သည်/E ဤ/B နေရာ/O တွင်/O အမည်/O အသုံးပြု/O ပုံ/O ကို/O ရှင်းပြ/N မည်/N ဖြစ်/N သည်/E
ကာကွယ်/B ဆေး/O ဆို/O တာ/O ဗိုင်းရပ်စ်/O တွေ/O ကို/O အားနည်း/O သွား/O အောင်/O လုပ်ဆောင်/O ပြီး/O ခန္ဓာကိုယ်/O က/O ပဋိပစ္စည်း/O တွေ/O ထွက်/O လာ/O အောင်/O လှုံ့ဆော်/O တဲ့/O နည်း/O နဲ့/O ကူးစက်ရောဂါ/O တွေ/O ကို/O ခုခံ/O နိုင်/O အောင်/O ပံ့ပိုး/O ပေး/O ဖို့/N ရည်ရွယ်/N ပါ/N တယ်/E ဒါပေမဲ့/B ရောဂါ/O ကူးစက်ခံ/O ထား/O ရ/O သူ/O ရဲ့/O ခန္ဓာကိုယ်/O က/O ပဋိပစ္စည်း/O တွေ/O ကို/O ထုတ်/O ထား/O ပြီး/O ဖြစ်/O နေ/O လျက်/O နဲ့/O တစ်ဖန်/O ပြန်/O ကူးစက်ခံ/O ရ/O မယ်/O ဆို/O ရင်/O တော့/O ကာကွယ်/O ဆေး/O ရဲ့/O ထိရောက်/O မှု/O နဲ့/O ပတ်သက်/O ပြီး/O မေးခွန်း/O ထုတ်/O စရာ/O တွေ/O ဖြစ်/N နေ/N ပါ/N တယ်/E
လောက/B အသစ်/O တစ်/O ခု/O ဖန်တီး/O ဖို့/O ဒါမှမဟုတ်လက်ရှိ/O လူ့/O အဖွဲ့အစည်း/O ကို/O ပြောင်းလဲ/O ပစ်/O နိုင်ဖိ့ု/O အတွက်လုံးဝ/O လွတ်လပ်/O တဲ့/O စိတ်ဓါတ်/O တစ်/O ခု/O ကို/O ပညာရေး/O က/O သင့်/O ကို/O ပြုလုပ်/O ပေး/N ရ/N လိမ့်/N မယ်/E ကျွန်တော်/B တို့/O ဟာ/O ဒီ/O လွတ်လပ်/O မှု/O ကို/O နောင်/O အနာဂတ်/O အထိ/O စောင့်/O ဆိုင်း/O မ/O နေ/O ဘဲ/O အခု/O လက်ရှိ/O အချိန်/O မှာ/O ပဲ/O ရအောင်ယူ/N ရ/N လိမ့်/N မယ်/E ဒီလို/B မှ/O မဟုတ်/O ရင်/O ကျွန်တော်/O တို့/O ဟာ/O ပျက်သုဉ်း/N ရ/N လိမ့်/N မယ်/E လွတ်လပ်/B စွာ/O နေထိုင်/O နိုင်/O မယ့်/O အခြေအနေ/O တစ်/O ခု/O ကို/O ကျွန်တော်/O တို့/O ချက်ချင်း/O ဖန်တီး/O ရ/N လိမ့်/N မယ်/N ။/E
မ/B လို/N ပါ/N ဘူး/E အခမဲ့/B သွား/O ရ/O မှာ/N ဖြစ်/N ပါ/N တယ်/E
အားနာ/B ပါ/N တယ်/E ကျွန်တော့်/B အခန်း/O ထဲ/O မှာ/O သော့/N ကျန်/N ခဲ့/N တယ်/E
သိ/B ပါ/N တယ်/E သိ/B ပါ/O တယ်/E ဘာ/B လုပ်/O လာ/O တယ်/O ဆို/O တာ/N ကို/N သိ/N တယ်/E မ/B ပြော/N ချင်/N ဘူး/E သူ/B တို့/O ခေါင်းတုံးတုံး/O တာ/O နဲ့/O ဘာ/O မှ/O မ/N ဆိုင်/N ဘူး/E
ဂျပန်/B နိုင်ငံ/O မှာ/O ၂၀၂၁/O ခုနှစ်/O ဖေဖော်ဝါရီ/O လ/O ၁၇/O ရက်နေ့/O က/O စတင်/O ခဲ့/O တဲ့/O COVID19/O ကာကွယ်/O ဆေးထိုး/O အစီအစဉ်/O မှာ/O အမေရိကန်/O ဆေးဝါး/O ကုမ္ပဏီ/O Pfizer/O နဲ့/O ဂျာမနီ/O ကုမ္ပဏီ/O BioNTech/O တို့/O ပူးပေါင်း/O တီထွင်/O ထုတ်လုပ်/O ခဲ့/O တဲ့/O ကာကွယ်/O ဆေး/O ကို/O အသုံးပြု/N ထား/N ပါ/N တယ်/E အဲဒီ/B ကာကွယ်/O ဆေး/O နဲ့/O အမေရိကန်/O Moderna/O ကုမ္ပဏီ/O က/O တီထွင်/O ထုတ်လုပ်/O တဲ့/O တခြား/O ကာကွယ်/O ဆေး/O တွေ/O ဟာ/O m/O RNA/O ကာကွယ်/O ဆေး/O တွေ/O ဖြစ်/O ပြီး/O ကိုရိုနာ/O ဗိုင်းရပ်စ်/O အမျိုးအစားသစ်/O ရဲ့/O မျိုး/O ဗီဇ/O ထဲ/O က/O ပရိုတိန်း/O နဲ့/O ထုတ်လုပ်/O ထား/O တာ/N ဖြစ်/N ပါ/N တယ်/E
အရက်မူး/B နေ/O တဲ့/O ခင်/O အောင်/N ကို/N ဆင်းခိုင်း/N တယ်/E သူ့/B လွယ်အိတ်/O ထဲ/O က/O ပြောင်/O လက်/O ပြီး/O အင်္ဂလိပ်စာ/O တွေ/O ရေး/O ထား/O တဲ့/O သံမဏိသတ္တု/O ဘူး/O သုံး/O ဘူး/N ကို/N တွေ့/N တယ်/E
ခင်ဗျား/B လို/O ချင်/O တဲ့/O နံပါတ်/O ဒီ/O မှာ/N ရှိ/N ပါ/N တယ်/E ဒါပေမဲ့/B ခင်ဗျား/O လို/O ချင်/O တဲ့/O အရောင်/N မ/N ရှိ/N ဘူး/E
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing#
```

Copying updated mk-wordtag perl script to current path:  

```
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# cp ../../checked-thura/preprocessing/split-tag/mk-wordtag2.pl .

root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# perl ./mk-wordtag2.pl ./paragraph.txt.shuf "\/" w > ./para.word
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# perl ./mk-wordtag2.pl ./paragraph.txt.shuf "\/" t > ./para.tag
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# wc ./para.word
   8465    2944 4949034 ./para.word
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# wc ./para.tag
  8465 353340 706792 ./para.tag
```

Check the content:  

```
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# head -n 3 para.word
နိုင်ငံတော် အလံ ကို လည်း ယခင် နိုင်ငံတော် အေးချမ်းသာယာ ရေး နှင့် ဖွံ့ဖြိုးရေး ကောင်စီ အစိုးရ လက်ထက် ၂၀⁠၀၈ ခုနှစ် တွင် ပြဋ္ဌာန်း ခဲ့ သော ဖွဲ့စည်းပုံ အခြေခံ ဥပဒေ ၂၀၀၈ တွင် သတ်မှတ် ထား သည့် နိုင်ငံတော် အလံ ဖြင့် အစားထိုး ၍ ပြောင်းလဲ အသုံးပြု ခဲ့ သည် ဝေါဟာရ ဗေဒ၁၉၈၉ ခုနှစ် တွင် စစ် အစိုးရ က အင်္ဂလိပ် ဘာသာ ဖြင့် ‌ ဘားမား ကို မြန်မာ ဟု ပြောင်းလဲ ရန် ဆုံးဖြတ် ခဲ့ ခြင်း သည် အငြင်းပွား စရာ ဖြစ် ခဲ့ သည်
မောင် ဟူသော စကားလုံး သည် အဓိပ္ပာယ် အမျိုးမျိုး ရှိ သည် ဤ နေရာ တွင် အမည် အသုံးပြု ပုံ ကို ရှင်းပြ မည် ဖြစ် သည်
ကာကွယ် ဆေး ဆို တာ ဗိုင်းရပ်စ် တွေ ကို အားနည်း သွား အောင် လုပ်ဆောင် ပြီး ခန္ဓာကိုယ် က ပဋိပစ္စည်း တွေ ထွက် လာ အောင် လှုံ့ဆော် တဲ့ နည်း နဲ့ ကူးစက်ရောဂါ တွေ ကို ခုခံ နိုင် အောင် ပံ့ပိုး ပေး ဖို့ ရည်ရွယ် ပါ တယ် ဒါပေမဲ့ ရောဂါ ကူးစက်ခံ ထား ရ သူ ရဲ့ ခန္ဓာကိုယ် က ပဋိပစ္စည်း တွေ ကို ထုတ် ထား ပြီး ဖြစ် နေ လျက် နဲ့ တစ်ဖန် ပြန် ကူးစက်ခံ ရ မယ် ဆို ရင် တော့ ကာကွယ် ဆေး ရဲ့ ထိရောက် မှု နဲ့ ပတ်သက် ပြီး မေးခွန်း ထုတ် စရာ တွေ ဖြစ် နေ ပါ တယ်
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# head -n 3 para.tag
B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E B O O O O O O O O O O O O O O O O O O O O O N N N E
B O O O N N N E B O O O O O O N N N E
B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing#
```

## Splitting Training/Valid/Test

```
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# tail -n 800 ./para.word > test.my
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# tail -n 800 ./para.tag > test.tg
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# head -n 7000 ./para.word > train.my
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# head -n 7000 ./para.tag > train.tg
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# head -n 7665 ./para.word | tail -n 665 > valid.my
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# head -n 7665 ./para.tag | tail -n 665 > valid.tg
```

Check filesize:

```
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# wc train.{my,tg}
   7000    2370 4077210 train.my
   7000  290848  581798 train.tg
  14000  293218 4659008 total
```

```
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# wc valid.{my,tg}
   665    262 411050 valid.my
   665  29471  58952 valid.tg
  1330  29733 470002 total
```

```
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# wc test.{my,tg}
   800    312 460774 test.my
   800  33021  66042 test.tg
  1600  33333 526816 total
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing#
```

Check the content:  

```
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# head -n 3 train.my
နိုင်ငံတော် အလံ ကို လည်း ယခင် နိုင်ငံတော် အေးချမ်းသာယာ ရေး နှင့် ဖွံ့ဖြိုးရေး ကောင်စီ အစိုးရ လက်ထက် ၂၀⁠၀၈ ခုနှစ် တွင် ပြဋ္ဌာန်း ခဲ့ သော ဖွဲ့စည်းပုံ အခြေခံ ဥပဒေ ၂၀၀၈ တွင် သတ်မှတ် ထား သည့် နိုင်ငံတော် အလံ ဖြင့် အစားထိုး ၍ ပြောင်းလဲ အသုံးပြု ခဲ့ သည် ဝေါဟာရ ဗေဒ၁၉၈၉ ခုနှစ် တွင် စစ် အစိုးရ က အင်္ဂလိပ် ဘာသာ ဖြင့် ‌ ဘားမား ကို မြန်မာ ဟု ပြောင်းလဲ ရန် ဆုံးဖြတ် ခဲ့ ခြင်း သည် အငြင်းပွား စရာ ဖြစ် ခဲ့ သည်
မောင် ဟူသော စကားလုံး သည် အဓိပ္ပာယ် အမျိုးမျိုး ရှိ သည် ဤ နေရာ တွင် အမည် အသုံးပြု ပုံ ကို ရှင်းပြ မည် ဖြစ် သည်
ကာကွယ် ဆေး ဆို တာ ဗိုင်းရပ်စ် တွေ ကို အားနည်း သွား အောင် လုပ်ဆောင် ပြီး ခန္ဓာကိုယ် က ပဋိပစ္စည်း တွေ ထွက် လာ အောင် လှုံ့ဆော် တဲ့ နည်း နဲ့ ကူးစက်ရောဂါ တွေ ကို ခုခံ နိုင် အောင် ပံ့ပိုး ပေး ဖို့ ရည်ရွယ် ပါ တယ် ဒါပေမဲ့ ရောဂါ ကူးစက်ခံ ထား ရ သူ ရဲ့ ခန္ဓာကိုယ် က ပဋိပစ္စည်း တွေ ကို ထုတ် ထား ပြီး ဖြစ် နေ လျက် နဲ့ တစ်ဖန် ပြန် ကူးစက်ခံ ရ မယ် ဆို ရင် တော့ ကာကွယ် ဆေး ရဲ့ ထိရောက် မှု နဲ့ ပတ်သက် ပြီး မေးခွန်း ထုတ် စရာ တွေ ဖြစ် နေ ပါ တယ်
```

```
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# head -n 3 train.tg
B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E B O O O O O O O O O O O O O O O O O O O O O N N N E
B O O O N N N E B O O O O O O N N N E
B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing#
```

```
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# head -n 3 valid.my
sharedhouse အိမ် တစ် လုံး မှာ နေထိုင် ကြ တဲ့ သူ တိုင်း ဟာ သီးသန့် အိပ်ခန်း တစ် ခန်း စီရှိ ကြ ပေ မယ့် သူ တို့ တွေ ဟာ မီးဖိုခန်း နဲ့ ဧည့်ခန်း ကို တော့ အတူတူ မျှ သုံး ကြ ရ တာ ဖြစ် ပါ တယ် အဲဒါ ကြောင့် မကြာခဏ ထိ တွေ့ ကိုင်တွယ် လေ့ ရှိ တဲ့ နေရာ တွေ ဖြစ် တဲ့ ရေဘုံ ပိုင် ခေါင်း တွေ ဒါမှမဟုတ် လျှပ်စစ်မီးခလုတ် စ တဲ့ အများ ကိုင်တွယ် အသုံးပြု တဲ့ နေရာ တွေ ကို အာနိသင်ပျော့ တဲ့ ကြေးချွတ်ဆေး ဒါမှမဟုတ် အရက် ပြန် ကို အခြေခံ ပြီး လုပ် ထား တဲ့ ပိုးသတ်ဆေး နဲ့ ပိုးသတ် ပြီး သန့်ရှင်း အောင် ထား ဖို့ အရေးကြီး တယ် လို့ ဂျပန် က StLukes International Hospital က ကူးစက်ရောဂါ ဆိုင်ရာ ကျွမ်းကျင် သူ စာခါ့ မို တို က ပြော ပါ တယ်
အဲဒီ လို လက္ခဏာ တွေ ဘယ် အကြောင်းရင်းကြောင့် ဖြစ် လာ သလဲ ဆို တာဝေခွဲ ရအောင် လုပ်ဆောင် ရ မယ့် အချက် တွေ ကို လေ့လာ ပါ မယ် ပထမ ပိုင်း မှာ တော့ ဘာ တွေ ကို သတိပြု သင့် ပြီး ကြိုတင်ပြင်ဆင်သင့် သလဲ ဆို တာ ကို လေ့လာ ကြ ရအောင်
ဒါ က ဘယ် က ရောက် လာ တာ တုန်း ဘာ လုပ် ရ တာ တုန်း ဘယ် ထဲ က ထုတ်ယူ တာ တုန်း မြေကြီး ထဲ က တူးဆွဲ ယူ လို့ ရ တာ လား သူ သိချင် တယ်
```

```
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# head -n 3 valid.tg
B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
B O O O O O O O O O O O O O O O O N N N E B O O O O O O O O O O O O O N N N E
B O O O N N N E B N N N E B O N N N E B O O O O O O O N N N E
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing#
```

```
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# head -n 3 test.my
ရှေ့ မှာ ဝယ် လို့ ရ တယ် ဒါပေမယ့် လူ နည်းနည်း ပဲ လက်မှတ် ဝယ်တာ သိပ် တော့ မ လို ဘူး
ပထမဆုံး ဓမ္မစကြာ ရဲ့ တည်‌ဆောက် ပုံ လေး မြင်ကွင်းကျယ် လေး ကို ဘုန်းဘုန်း whiteboard ပေါ် မှာ ရေးပြ မယ် နော် စာ လေ့လာ တဲ့ အခါ မှာ bird’s eyeview and worm’s eyeview ငှက် ရဲ့ အမြင် နဲ့ တီကောင် ရဲ့ အမြင် အဲဒီ လို အမြင် နှစ် ခု ကြည့် ရ မယ်
မ လို ပါ ဘူး ကျွန်မ ကိုယ်တိုင် သယ် လို့ ရ ပါ တယ်
```

```
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing# head -n 3 test.tg
B O N N N E B O O O O O O N N N E
B O O O O O O O O O O O N N N E B O O O O O O O O O O O O O O O O O O O O N N N E
B N N E B O O N N N E
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/preprocessing#
```

## Combination of Sentence and Paragraph

Combination for word data:  

```
root@85f02f4cfa85:/home/ye/exp/mysent/data-para/combind-process# cat ../../data-sent/train.my ../preprocessing/train.my > train.my.combi
root@62e76e3751ae:/home/ye/exp/mysent/data-para/combind-process# cat ../../data-sent/valid.my ../preprocessing/valid.my > valid.my.combi
root@62e76e3751ae:/home/ye/exp/mysent/data-para/combind-process# cat ../../data-sent/test.my ../preprocessing/test.my > test.my.combi
```

```
root@62e76e3751ae:/home/ye/exp/mysent/data-para/combind-process# wc *.combi
    5512      763  1380222 test.my.combi
   47000     6073 11945760 train.my.combi
    3079      519   877574 valid.my.combi
   55591     7355 14203556 total
root@62e76e3751ae:/home/ye/exp/mysent/data-para/combind-process#
```

Combination for tag data:  

```
root@62e76e3751ae:/home/ye/exp/mysent/data-para/combind-process# cat ../../data-sent/valid.tg ../preprocessing/valid.tg > valid.tg.comb
i
root@62e76e3751ae:/home/ye/exp/mysent/data-para/combind-process# cat ../../data-sent/train.tg ../preprocessing/train.tg > train.tg.comb
i
root@62e76e3751ae:/home/ye/exp/mysent/data-para/combind-process#
root@62e76e3751ae:/home/ye/exp/mysent/data-para/combind-process# cat ../../data-sent/test.tg ../preprocessing/test.tg > test.tg.combi

root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# wc {train,valid,test}.tg.combi
  47000  834382 1669227 train.tg.combi
   3079   61786  123594 valid.tg.combi
   5512   96641  193327 test.tg.combi
  55591  992809 1986148 total
```

## Shuffling the Combined Data

```
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# ls
test.my.combi  test.tg.combi  train.my.combi  train.tg.combi  valid.my.combi  valid.tg.combi
```

```
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# head -n 2 train.my.combi
ဘာ ရယ် လို့ တိတိကျကျ ထောက်မပြ နိုင် ပေမဲ့ ပြဿနာ တစ် ခု ခု ရှိ တယ် နဲ့ တူ တယ်
လူ့ အဖွဲ့အစည်း က ရှပ်ထွေး လာ တာ နဲ့ အမျှ အရင် က မ ရှိ ခဲ့ တဲ့ လူမှုရေး ပြဿနာ တွေ ဖြစ်ပေါ် လာ ခဲ့ တယ်
```

```
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# head -n 2 train.tg.combi
B O O O O O O O O O O O N N N E
B O O O O O O O O O O O O O O O O N N N E
```

```
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# head -n 2 valid.my.combi
ထို အချိန် မှ စ ၍ စင်္ကာပူ ကျွန်း ၏ ခေတ်သစ် တစ် ခေတ် စ ခဲ့ သည်
ကျေးဇူးပြုပြီး အချိုသာဆုံး စျေး နဲ့ ရောင်း ပေး ပါ
```

```
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# head -n 2 valid.tg.combi
B O O O O O O O O O N N N E
B O O N N N E
```

```
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# head -n 2 test.my.combi
အခု သန့်စင်ခန်း ကို သုံး ပါရစေ
လူငယ် တွေ က ပုံစံတကျ ရှိ မှု ကို မ ကြိုက် ဘူး
```

```
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# head -n 2 test.tg.combi
B N N N E
B O O O O O N N N E
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process#
```

Before shuffle, we have to paste each my and tg pair:  

```
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# ls
test.my.combi  test.tg.combi  train.my.combi  train.tg.combi  valid.my.combi  valid.tg.combi
```

```
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# head -n 2 train.my.combi
ဘာ ရယ် လို့ တိတိကျကျ ထောက်မပြ နိုင် ပေမဲ့ ပြဿနာ တစ် ခု ခု ရှိ တယ် နဲ့ တူ တယ်
လူ့ အဖွဲ့အစည်း က ရှပ်ထွေး လာ တာ နဲ့ အမျှ အရင် က မ ရှိ ခဲ့ တဲ့ လူမှုရေး ပြဿနာ တွေ ဖြစ်ပေါ် လာ ခဲ့ တယ်
```

```
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# head -n 2 train.tg.combi
B O O O O O O O O O O O N N N E
B O O O O O O O O O O O O O O O O N N N E
```

```
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# head -n 2 valid.my.combi
ထို အချိန် မှ စ ၍ စင်္ကာပူ ကျွန်း ၏ ခေတ်သစ် တစ် ခေတ် စ ခဲ့ သည်
ကျေးဇူးပြုပြီး အချိုသာဆုံး စျေး နဲ့ ရောင်း ပေး ပါ
```

```
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# head -n 2 valid.tg.combi
B O O O O O O O O O N N N E
B O O N N N E
```

```
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# head -n 2 test.my.combi
အခု သန့်စင်ခန်း ကို သုံး ပါရစေ
လူငယ် တွေ က ပုံစံတကျ ရှိ မှု ကို မ ကြိုက် ဘူး
```

```
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# head -n 2 test.tg.combi
B N N N E
B O O O O O N N N E
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process#
```

Shuffling  

```
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# shuf ./train.my-tg > ./train.my-tg.shuf
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# shuf ./valid.my-tg > ./valid.my-tg.shuf
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# shuf ./test.my-tg > ./test.my-tg.shuf
```

Check with eyeball:  

```
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# head -n 2 ./train.my-tg.shuf
နားလည် ပါ ပြီ   N N E
ဈေး က များ လှ ချေ လား   B O N N N E
```

```
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# head -n 2 ./valid.my-tg.shuf
သူ ဘယ်သူ နဲ့ အရင်းနှီးဆုံး လဲ   B N N N E
ဒီ က နေ ရှေ့ ကို တည့်တည့် သွား မီးပွိုင့် တွေ့ ရင် ဘယ်ဘက် ကွေ့ ၂ မှတ်တိုင် ဆက်လက် သွား ရင် ရောက် ပါ လိမ့် မယ်   B O O O O O O O O O O O O O O O O N N N E
```

```
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# head -n 2 ./test.my-tg.shuf
ရင်ဘတ် အောင့် လာ ရင် သတိထား ပါ ။        B O N N N E B
ဘယ်လောက် နောက်ကျ သလဲ    B N E
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process#
```

```
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# cut -f 1 ./train.my-tg.shuf > train.my.final
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# cut -f 2 ./train.my-tg.shuf > train.tg.final
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# cut -f 1 ./valid.my-tg.shuf > valid.my.final
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# cut -f 2 ./valid.my-tg.shuf > valid.tg.final
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# cut -f 1 ./test.my-tg.shuf > test.my.final
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# cut -f 2 ./test.my-tg.shuf > test.tg.final
```

Check the final data or read to train NMT dataset:  

root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# head -n 2 train.{my,tg}.final
==> train.my.final <==
နားလည် ပါ ပြီ
ဈေး က များ လှ ချေ လား

==> train.tg.final <==
N N E
B O N N N E
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# head -n 2 valid.{my,tg}.final
==> valid.my.final <==
သူ ဘယ်သူ နဲ့ အရင်းနှီးဆုံး လဲ
ဒီ က နေ ရှေ့ ကို တည့်တည့် သွား မီးပွိုင့် တွေ့ ရင် ဘယ်ဘက် ကွေ့ ၂ မှတ်တိုင် ဆက်လက် သွား ရင် ရောက် ပါ လိမ့် မယ်

==> valid.tg.final <==
B N N N E
B O O O O O O O O O O O O O O O O N N N E
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process# head -n 2 test.{my,tg}.final
==> test.my.final <==
ရင်ဘတ် အောင့် လာ ရင် သတိထား ပါ ။
ဘယ်လောက် နောက်ကျ သလဲ

==> test.tg.final <==
B O N N N E B
B N E
root@2d563285774c:/home/ye/exp/mysent/data-para/combind-process#

Copied to the folder called inside configuration file:

root@2d563285774c:/home/ye/exp/mysent/data-para# cp ./combind-process/*.final .
root@2d563285774c:/home/ye/exp/mysent/data-para# ls
combind-process  paragraph.txt.error  test.my.final  train.my.final  valid.my.final
paragraph.txt    preprocessing        test.tg.final  train.tg.final  valid.tg.final
root@2d563285774c:/home/ye/exp/mysent/data-para# mv train.my.final train.my
root@2d563285774c:/home/ye/exp/mysent/data-para# mv train.tg.final train.tg
root@2d563285774c:/home/ye/exp/mysent/data-para#
root@2d563285774c:/home/ye/exp/mysent/data-para# mv valid.my.final valid.my
root@2d563285774c:/home/ye/exp/mysent/data-para# mv valid.tg.final valid.tg
root@2d563285774c:/home/ye/exp/mysent/data-para#
root@2d563285774c:/home/ye/exp/mysent/data-para# mv test.my.final test.my
root@2d563285774c:/home/ye/exp/mysent/data-para# mv test.tg.final test.tg

## Build Vocabs

root@2d563285774c:/home/ye/exp/mysent/data-para# mkdir vocab
root@2d563285774c:/home/ye/exp/mysent/data-para# cat train.my valid.my test.my > vocab/all.my
root@2d563285774c:/home/ye/exp/mysent/data-para# cat train.tg valid.tg test.tg > vocab/all.tg
root@2d563285774c:/home/ye/exp/mysent/data-para# cd vocab
root@2d563285774c:/home/ye/exp/mysent/data-para/vocab# marian-vocab < ./all.my > vocab.my.yml
[2022-10-19 05:32:43] Creating vocabulary...
[2022-10-19 05:32:43] [data] Creating vocabulary stdout from stdin
[2022-10-19 05:32:43] Finished
root@2d563285774c:/home/ye/exp/mysent/data-para/vocab# marian-vocab < ./all.tg > vocab.tg.yml
[2022-10-19 05:32:52] Creating vocabulary...
[2022-10-19 05:32:52] [data] Creating vocabulary stdout from stdin
[2022-10-19 05:32:52] Finished
root@2d563285774c:/home/ye/exp/mysent/data-para/vocab#

Check/confirm the vocab files:

root@2d563285774c:/home/ye/exp/mysent/data-para/vocab# head vocab.my.yml
</s>: 0
<unk>: 1
ကို: 2
တယ်: 3
က: 4
သည်: 5
ပါ: 6
မှာ: 7
တွေ: 8
တဲ့: 9
root@2d563285774c:/home/ye/exp/mysent/data-para/vocab# head vocab.tg.yml
</s>: 0
<unk>: 1
O: 2
N: 3
E: 4
B: 5
NN: 6
BBအိုး: 7
BEအကြိမ်: 8
BN: 9
root@2d563285774c:/home/ye/exp/mysent/data-para/vocab#

## Prepare Shell Script for NMT Training

mkdir model.transformer.para1;

marian \
    --model model.transformer.para1/model.npz --type transformer \
    --train-sets data-para/train.my data-para/train.tg \
    --max-length 200 \
    --vocabs data-para/vocab/vocab.my.yml data-para/vocab/vocab.tg.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets data-para/valid.my data-para/valid.tg \
    --valid-translation-output model.transformer.para1/valid.my-tg.output --quiet-translation \
    --valid-mini-batch 32 \
    --beam-size 6 --normalize 0.6 \
    --log model.transformer.para1/train.log --valid-log model.transformer.para1/valid.log \
    --enc-depth 2 --dec-depth 2 \
    --transformer-heads 8 \
    --transformer-postprocess-emb d \
    --transformer-postprocess dan \
    --transformer-dropout 0.3 --label-smoothing 0.1 \
    --learn-rate 0.0003 --lr-warmup 0 --lr-decay-inv-sqrt 16000 --lr-report \
    --clip-norm 5 \
    --tied-embeddings \
    --devices 0 --sync-sgd --seed 1111 \
    --exponential-smoothing \
    --dump-config > model.transformer.para1/config.yml

time marian -c model.transformer.para1/config.yml  2>&1 | tee transformer.para1.log

## Training NMT Model

ye@lst-gpu-3090:~$ screen -ls
There is a screen on:
        97054.nmt       (18/10/2565 07:29:58)   (Detached)
1 Socket in /run/screen/S-ye.
ye@lst-gpu-3090:~$ screen -r 97054.nmt

[2022-10-19 05:48:16] Using synchronous SGD
[2022-10-19 05:48:16] [comm] Compiled without MPI support. Running as a single process on cb9dcb03dfe7
[2022-10-19 05:48:16] Synced seed 1111
[2022-10-19 05:48:16] [data] Loading vocabulary from JSON/Yaml file data-para/vocab/vocab.my.yml
[2022-10-19 05:48:16] [data] Setting vocabulary size for input 0 to 46,192
[2022-10-19 05:48:16] [data] Loading vocabulary from JSON/Yaml file data-para/vocab/vocab.tg.yml
[2022-10-19 05:48:16] [data] Setting vocabulary size for input 1 to 45
[2022-10-19 05:48:16] [batching] Collecting statistics for batch fitting with step size 10
[2022-10-19 05:48:16] Error: Curand error 203 - /temp/marian/src/tensors/rand.cpp:74: curandCreateGenerator(&generator_, CURAND_RNG_PSEUDO_DEFAULT)
[2022-10-19 05:48:16] Error: Aborted from marian::CurandRandomGenerator::CurandRandomGenerator(size_t, marian::DeviceId) in /temp/marian/src/tensors/rand.cpp:74

[CALL STACK]
[0x55f553739050]    marian::CurandRandomGenerator::  CurandRandomGenerator  (unsigned long,  marian::DeviceId) + 0x750
[0x55f553739689]    marian::  createRandomGenerator  (unsigned long,  marian::DeviceId) + 0x69
[0x55f553733f20]    marian::  BackendByDeviceId  (marian::DeviceId,  unsigned long) + 0xa0
[0x55f553223220]    marian::ExpressionGraph::  setDevice  (marian::DeviceId,  std::shared_ptr<marian::Device>) + 0x80
[0x55f55351ccd5]    marian::GraphGroup::  initGraphsAndOpts  ()        + 0x1e5
[0x55f55351e1f8]    marian::GraphGroup::  GraphGroup  (std::shared_ptr<marian::Options>,  std::shared_ptr<marian::IMPIWrapper>) + 0x548
[0x55f5534fc773]    marian::SyncGraphGroup::  SyncGraphGroup  (std::shared_ptr<marian::Options>,  std::shared_ptr<marian::IMPIWrapper>) + 0x83
[0x55f5530558ab]    marian::Train<marian::SyncGraphGroup>::  run  ()   + 0x1c2b
[0x55f552f83347]    mainTrainer  (int,  char**)                        + 0x147
[0x7f92607d5d90]                                                       + 0x29d90
[0x7f92607d5e40]    __libc_start_main                                  + 0x80
[0x55f552f7c995]    _start                                             + 0x25


real    0m0.382s
user    0m0.202s
sys     0m0.033s
root@cb9dcb03dfe7:/home/ye/exp/mysent# ./transformer.para1.sh


## Updating the Shell Script

As usual, we need to adjust some hyperparameters based on our current machine and GPU card ...
Final Script is as follows:  

mkdir model.transformer.para1;

marian \
    --model model.transformer.para1/model.npz --type transformer \
    --train-sets data-para/train.my data-para/train.tg \
    --max-length 200 \
    --vocabs data-para/vocab/vocab.my.yml data-para/vocab/vocab.tg.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets data-para/valid.my data-para/valid.tg \
    --valid-translation-output model.transformer.para1/valid.my-tg.output --quiet-translation \
    --valid-mini-batch 16 \
    --beam-size 6 --normalize 0.6 \
    --log model.transformer.para1/train.log --valid-log model.transformer.para1/valid.log \
    --enc-depth 2 --dec-depth 2 \
    --transformer-heads 8 \
    --transformer-postprocess-emb d \
    --transformer-postprocess dan \
    --transformer-dropout 0.3 --label-smoothing 0.1 \
    --learn-rate 0.0003 --lr-warmup 0 --lr-decay-inv-sqrt 16000 --lr-report \
    --clip-norm 5 \
    --tied-embeddings \
    --devices 0 --sync-sgd --seed 1111 \
    --exponential-smoothing \
    --dump-config > model.transformer.para1/config.yml

time marian -c model.transformer.para1/config.yml  2>&1 | tee transformer.para1.log
root@8c9f9e316b59:/home/ye/exp/mysent#

## Training

root@8c9f9e316b59:/home/ye/exp/mysent# ./transformer.para1.sh
...
...
...
words/s : gNorm 0.7127 : L.r. 1.1239e-04
[2022-10-19 14:34:31] Seen 46,970 samples
[2022-10-19 14:34:31] Starting data epoch 330 in logical epoch 330
[2022-10-19 14:34:31] [data] Shuffling data
[2022-10-19 14:34:31] [data] Done reading 47,000 sentences
[2022-10-19 14:34:31] [data] Done shuffling 47,000 sentences to temp files
[2022-10-19 14:34:34] Ep. 330 : Up. 114500 : Sen. 21,592 : Cost 0.73408455 * 1,263,648 @ 2,633 after 287,873,528 : Time 9.45s : 133773.31 words/s : gNorm 0.8392 : L.r. 1.1214e-04
[2022-10-19 14:34:38] Seen 46,970 samples
[2022-10-19 14:34:38] Starting data epoch 331 in logical epoch 331
[2022-10-19 14:34:38] [data] Shuffling data
[2022-10-19 14:34:38] [data] Done reading 47,000 sentences
[2022-10-19 14:34:38] [data] Done shuffling 47,000 sentences to temp files
[2022-10-19 14:34:44] Ep. 331 : Up. 115000 : Sen. 41,821 : Cost 0.73509383 * 1,253,425 @ 2,337 after 289,126,953 : Time 9.44s : 132823.44 words/s : gNorm 0.9424 : L.r. 1.1190e-04
[2022-10-19 14:34:44] Saving model weights and runtime parameters to model.transformer.para1/model.iter115000.npz
[2022-10-19 14:34:44] Saving model weights and runtime parameters to model.transformer.para1/model.npz
[2022-10-19 14:34:45] Saving Adam parameters
[2022-10-19 14:34:46] [training] Saving training checkpoint to model.transformer.para1/model.npz and model.transformer.para1/model.npz.optimizer.npz
[2022-10-19 14:34:52] [valid] Ep. 331 : Up. 115000 : cross-entropy : 3.14871 : stalled 10 times (last best: 3.07433)
[2022-10-19 14:34:53] [valid] Ep. 331 : Up. 115000 : perplexity : 1.16121 : stalled 10 times (last best: 1.15712)
[2022-10-19 14:35:06] [valid] Ep. 331 : Up. 115000 : bleu : 85.5658 : stalled 2 times (last best: 86.5449)
[2022-10-19 14:35:06] Training finished
[2022-10-19 14:35:06] Saving model weights and runtime parameters to model.transformer.para1/model.npz
[2022-10-19 14:35:08] Saving Adam parameters
[2022-10-19 14:35:08] [training] Saving training checkpoint to model.transformer.para1/model.npz and model.transformer.para1/model.npz.optimizer.npz

real    46m29.086s
user    46m14.094s
sys     1m22.137s

## Prepare bas Script for Testing with the Best Model

root@8c9f9e316b59:/home/ye/exp/mysent/model.transformer.para1# cat ./test-eval-best.sh
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments for Myanmar language sentence segmentation
## used Marian NMT Framework for training
## Last updated: 20 Oct 2022

data_path="/home/ye/exp/mysent/data-para";
src="my"; tgt="tg";

marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml --devices 0 --output hyp.best.${tgt} < ${data_path}/test.${src};
echo "Evaluation with hyp.best.${tgt}, Transformer model, with sent+para training data:" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl ${data_path}/test.${tgt} < ./hyp.best.${tgt} >> eval-best-result.txt;

root@8c9f9e316b59:/home/ye/exp/mysent/model.transformer.para1#

## Testing with Best Model

[2022-10-19 22:53:07] Best translation 5490 : B O O O O O N N N E
[2022-10-19 22:53:07] Best translation 5491 : B O O O N N N E
[2022-10-19 22:53:07] Best translation 5492 : B O O O O O O O O O O O O O O O O O N N N E
[2022-10-19 22:53:07] Best translation 5493 : B O O O N N N E B O O N N N E B O O O O O O O O N N N E
[2022-10-19 22:53:07] Best translation 5494 : B O O O O O O O O O O N N N E B O O O O O O O O O O O N N N E
[2022-10-19 22:53:07] Best translation 5495 : B O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-10-19 22:53:07] Best translation 5496 : B O N N N E
[2022-10-19 22:53:07] Best translation 5497 : B O N N N E
[2022-10-19 22:53:07] Best translation 5498 : B
[2022-10-19 22:53:07] Best translation 5499 : B O O O O O O O O O O O O O O O O O O O N N N E
[2022-10-19 22:53:07] Best translation 5500 : B O O O O O O O O O O O O O O N N N E B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-10-19 22:53:07] Best translation 5501 : B O O O O O O O O O O O O O O O O O O O O O N N N E B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-10-19 22:53:07] Best translation 5502 : B O O O O O O O N N N E
[2022-10-19 22:53:07] Best translation 5503 : B N N N E
[2022-10-19 22:53:07] Best translation 5504 : B N N N E
[2022-10-19 22:53:07] Best translation 5505 : B O O O O O O O N N N E
[2022-10-19 22:53:07] Best translation 5506 : B O O O O O N N N E
[2022-10-19 22:53:07] Best translation 5507 : B O O O O O N N N E
[2022-10-19 22:53:07] Best translation 5508 : B O O O O O O O O O O O N N N E
[2022-10-19 22:53:07] Best translation 5509 : B O O O O O O O O O O O N N N E
[2022-10-19 22:53:07] Best translation 5510 : B O O O O O O O O O O O O O O N N N E
[2022-10-19 22:53:07] Best translation 5511 : B O O O O O O O O O O O O O N N N E
[2022-10-19 22:53:07] Total time: 89.05642s wall
It is not advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    1m30.069s
user    1m27.975s
sys     0m3.616s
root@8c9f9e316b59:/home/ye/exp/mysent/model.transformer.para1# time ./test-eval-best.sh

## Check the Result

root@8c9f9e316b59:/home/ye/exp/mysent/model.transformer.para1# cat eval-best-result.txt
Evaluation with hyp.best.tg, Transformer model, with sent+para training data:
BLEU = 91.66, 95.0/93.9/92.7/91.4 (BP=0.983, ratio=0.983, hyp_len=95015, ref_len=96641)

## To Do

- chrF score calculation
- WER Calculation, check the top ten Error and make translation error analysis in details

