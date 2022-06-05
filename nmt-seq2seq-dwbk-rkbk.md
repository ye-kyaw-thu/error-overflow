# Seq2Seq Archi for NMT Baseline

## Data Information

10-folds data for dw-bk language pair:  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/data/word/dw-bk$ for i in {1..10}; do echo "path: $i/"; wc ./$i/*.{dw,bk}; done;
path: 1/
    500    3032   48817 ./1/dev.dw
    670    4013   64228 ./1/test.dw
   5452   32614  524213 ./1/train.dw
    500    3213   46186 ./1/dev.bk
    670    4267   60615 ./1/test.bk
   5452   34473  494687 ./1/train.bk
  13244   81612 1238746 total
path: 2/
    500    3032   48817 ./2/dev.dw
    670    4030   65195 ./2/test.dw
   5452   32597  523246 ./2/train.dw
    500    3213   46186 ./2/dev.bk
    670    4295   61799 ./2/test.bk
   5452   34445  493503 ./2/train.bk
  13244   81612 1238746 total
path: 3/
    500    3032   48817 ./3/dev.dw
    670    3998   65039 ./3/test.dw
   5452   32629  523402 ./3/train.dw
    500    3213   46186 ./3/dev.bk
    670    4284   61312 ./3/test.bk
   5452   34456  493990 ./3/train.bk
  13244   81612 1238746 total
path: 4/
    500    3032   48817 ./4/dev.dw
    670    4012   64983 ./4/test.dw
   5452   32615  523458 ./4/train.dw
    500    3213   46186 ./4/dev.bk
    670    4137   60685 ./4/test.bk
   5452   34603  494617 ./4/train.bk
  13244   81612 1238746 total
path: 5/
    500    3032   48817 ./5/dev.dw
    670    4011   63713 ./5/test.dw
   5452   32616  524728 ./5/train.dw
    500    3213   46186 ./5/dev.bk
    670    4188   61079 ./5/test.bk
   5452   34552  494223 ./5/train.bk
  13244   81612 1238746 total
path: 6/
    500    3032   48817 ./6/dev.dw
    670    4042   64120 ./6/test.dw
   5452   32585  524321 ./6/train.dw
    500    3213   46186 ./6/dev.bk
    670    4276   60268 ./6/test.bk
   5452   34464  495034 ./6/train.bk
  13244   81612 1238746 total
path: 7/
    500    3032   48817 ./7/dev.dw
    670    4025   63846 ./7/test.dw
   5452   32602  524595 ./7/train.dw
    500    3213   46186 ./7/dev.bk
    670    4279   60287 ./7/test.bk
   5452   34461  495015 ./7/train.bk
  13244   81612 1238746 total
path: 8/
    500    3032   48817 ./8/dev.dw
    670    3993   65355 ./8/test.dw
   5452   32634  523086 ./8/train.dw
    500    3213   46186 ./8/dev.bk
    670    4235   60716 ./8/test.bk
   5452   34505  494586 ./8/train.bk
  13244   81612 1238746 total
path: 9/
    500    3032   48817 ./9/dev.dw
    670    3985   63827 ./9/test.dw
   5452   32642  524614 ./9/train.dw
    500    3213   46186 ./9/dev.bk
    670    4245   60518 ./9/test.bk
   5452   34495  494784 ./9/train.bk
  13244   81612 1238746 total
 path: 10/
    500    2946   47560 ./10/dev.dw
    592    3550   56952 ./10/test.dw
   5530   33163  532746 ./10/train.dw
    500    3164   45302 ./10/dev.bk
    592    3747   54209 ./10/test.bk
   5530   35042  501977 ./10/train.bk
  13244   81612 1238746 total
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/data/word/dw-bk$
```

data info for rk-bk language pair:  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/data/word/rk-bk$ for i in {1..10}; do echo "path: $i/"; wc ./$i/*.{rk,bk}; done;
path: 1/
    800    5175   85367 ./1/dev.rk
   1072    6739  110724 ./1/test.rk
   8850   57071  927947 ./1/train.rk
    800    5306   79716 ./1/dev.bk
   1072    6956  103337 ./1/test.bk
   8850   58185  864939 ./1/train.bk
  21444  139432 2172030 total
path: 2/
    800    5175   85367 ./2/dev.rk
   1072    7004  115305 ./2/test.rk
   8850   56806  923366 ./2/train.rk
    800    5306   79716 ./2/dev.bk
   1072    7142  107707 ./2/test.bk
   8850   57999  860569 ./2/train.bk
  21444  139432 2172030 total
path: 3/
    800    5175   85367 ./3/dev.rk
   1072    7019  114329 ./3/test.rk
   8850   56791  924342 ./3/train.rk
    800    5306   79716 ./3/dev.bk
   1072    7152  106704 ./3/test.bk
   8850   57989  861572 ./3/train.bk
  21444  139432 2172030 total
path: 4/
    800    5175   85367 ./4/dev.rk
   1072    6796  109356 ./4/test.rk
   8850   57014  929315 ./4/train.rk
    800    5306   79716 ./4/dev.bk
   1072    6905  101225 ./4/test.bk
   8850   58236  867051 ./4/train.bk
  21444  139432 2172030 total
path: 5/
    800    5175   85367 ./5/dev.rk
   1072    6851  109765 ./5/test.rk
   8850   56959  928906 ./5/train.rk
    800    5306   79716 ./5/dev.bk
   1072    7007  102834 ./5/test.bk
   8850   58134  865442 ./5/train.bk
  21444  139432 2172030 total
path: 6/
    800    5175   85367 ./6/dev.rk
   1072    6798  112415 ./6/test.rk
   8850   57012  926256 ./6/train.rk
    800    5306   79716 ./6/dev.bk
   1072    6982  104609 ./6/test.bk
   8850   58159  863667 ./6/train.bk
  21444  139432 2172030 total
path: 7/
    800    5175   85367 ./7/dev.rk
   1072    7021  112493 ./7/test.rk
   8850   56789  926178 ./7/train.rk
    800    5306   79716 ./7/dev.bk
   1072    7142  105254 ./7/test.bk
   8850   57999  863022 ./7/train.bk
  21444  139432 2172030 total
path: 8/
    800    5175   85367 ./8/dev.rk
   1072    7014  114156 ./8/test.rk
   8850   56796  924515 ./8/train.rk
    800    5306   79716 ./8/dev.bk
   1072    7149  106394 ./8/test.bk
   8850   57992  861882 ./8/train.bk
  21444  139432 2172030 total
path: 9/
    800    5175   85367 ./9/dev.rk
   1072    6830  110901 ./9/test.rk
   8850   56980  927770 ./9/train.rk
    800    5306   79716 ./9/dev.bk
   1072    6918  103287 ./9/test.bk
   8850   58223  864989 ./9/train.bk
  21444  139432 2172030 total
path: 10/
    800    5128   83237 ./10/dev.rk
   1072    6898  114428 ./10/test.rk
   8850   56959  926373 ./10/train.rk
    800    5173   77217 ./10/dev.bk
   1072    7081  106504 ./10/test.bk
   8850   58193  864271 ./10/train.bk
  21444  139432 2172030 total
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/data/word/rk-bk$
```

## Let's Peek the Data

both dw-bk and rk-bk data are manually segmented ...  
for dw-bk pair:  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/data/word/dw-bk$ ./head-3-for-all.sh
/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/1
head -n 3 for Dawei:
==> dev.dw <==
ခံဗျား ပ္လေးသေး ဟှလား ။
ကျွန်တော့် အစ်မက လွဲဟှီး အားလုံး အယ်မှာ ရှိဟှယ် ။
၁ နာရီ ပဲ ရှိသေးဟှယ် သူမ ညစာ ရှစ် ပီးပီ ။

==> test.dw <==
အဲဝယ်ဟှား ခံဗျား ဟှို အဲဇာ ပေး ဟှို့ မှုဝ ။
နန် ဟှယ်လူ့ ဟှို ဒုက္ခပေး ရစ်ဇာနူး ။
သိပ်  ပြေ တာပေါ့ ။

==> train-dev.dw <==
နန် ဟှဲဇာ စီစဉ် နေဟှယ် ဆိုတာ ငါ့ ကို  ပြော သင့်ဟှယ် ။
သူးနို့ စာအုပ် သုံး ထော် ကျော် ရောပီးပီ ။
ချို့လူလေဟှာ မွီးရာပါ ဇာတ်မှန်းသား လေ မား  ။

==> train.dw <==
နန် ဟှဲဇာ စီစဉ် နေဟှယ် ဆိုတာ ငါ့ ကို  ပြော သင့်ဟှယ် ။
သူးနို့ စာအုပ် သုံး ထော် ကျော် ရောပီးပီ ။
ချို့လူလေဟှာ မွီးရာပါ ဇာတ်မှန်းသား လေ မား  ။
head -n 3 for Beik:
==> dev.bk <==
နင် မ ပြေး သေးရလား ။
အားလုံးက ဒါမှာဘဲ အစ်မ တစ် ယောက် မရှိရ  ။
၁ နာရီ ပဲ ရှိ သေးရိ ဒယ်ကောင်မငယ်  ညစာ ချက် ပြီးလေ  ။

==> test.bk <==
သူ ခင်ဗျား ကို ဒယ်ဇာ ပေး ဟုတ် ဝ ။
နင် ဖယ်သူ့ ဝို စိတ်ညစ်ပေး ခဲ့လဲ  ။
သိပ် ပြေ တာပေါ့  ။

==> train.bk <==
နင် ဘာ စီစဉ် နေရယ်ဆိုတာ ငါ့ ဝို ပြော သင့်ပေါ့လန်း  ။
သူလို့ စာအုပ် သုံးထောင် ကျော် ရောင်း ပီး ဟောဘီ  ။
ငယ်ငယ်တည်းက မင်းသား လုပ်ဝို့ ဝါသနာ ပါစ  ။

==> train-dev.bk <==
နင် ဘာ စီစဉ် နေရယ်ဆိုတာ ငါ့ ဝို ပြော သင့်ပေါ့လန်း  ။
သူလို့ စာအုပ် သုံးထောင် ကျော် ရောင်း ပီး ဟောဘီ  ။
ငယ်ငယ်တည်းက မင်းသား လုပ်ဝို့ ဝါသနာ ပါစ  ။
==========
/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/2
head -n 3 for Dawei:
==> dev.dw <==
ခံဗျား ပ္လေးသေး ဟှလား ။
ကျွန်တော့် အစ်မက လွဲဟှီး အားလုံး အယ်မှာ ရှိဟှယ် ။
၁ နာရီ ပဲ ရှိသေးဟှယ် သူမ ညစာ ရှစ် ပီးပီ ။

==> test.dw <==
နန် ဟှဲဇာ စီစဉ် နေဟှယ် ဆိုတာ ငါ့ ကို  ပြော သင့်ဟှယ် ။
သူးနို့ စာအုပ် သုံး ထော် ကျော် ရောပီးပီ ။
ချို့လူလေဟှာ မွီးရာပါ ဇာတ်မှန်းသား လေ မား  ။

==> train-dev.dw <==
အဲဝယ်ဟှား ခံဗျား ဟှို အဲဇာ ပေး ဟှို့ မှုဝ ။
နန် ဟှယ်လူ့ ဟှို ဒုက္ခပေး ရစ်ဇာနူး ။
သိပ်  ပြေ တာပေါ့ ။

==> train.dw <==
အဲဝယ်ဟှား ခံဗျား ဟှို အဲဇာ ပေး ဟှို့ မှုဝ ။
နန် ဟှယ်လူ့ ဟှို ဒုက္ခပေး ရစ်ဇာနူး ။
သိပ်  ပြေ တာပေါ့ ။
head -n 3 for Beik:
==> dev.bk <==
နင် မ ပြေး သေးရလား ။
အားလုံးက ဒါမှာဘဲ အစ်မ တစ် ယောက် မရှိရ  ။
၁ နာရီ ပဲ ရှိ သေးရိ ဒယ်ကောင်မငယ်  ညစာ ချက် ပြီးလေ  ။

==> test.bk <==
နင် ဘာ စီစဉ် နေရယ်ဆိုတာ ငါ့ ဝို ပြော သင့်ပေါ့လန်း  ။
သူလို့ စာအုပ် သုံးထောင် ကျော် ရောင်း ပီး ဟောဘီ  ။
ငယ်ငယ်တည်းက မင်းသား လုပ်ဝို့ ဝါသနာ ပါစ  ။

==> train.bk <==
သူ ခင်ဗျား ကို ဒယ်ဇာ ပေး ဟုတ် ဝ ။
နင် ဖယ်သူ့ ဝို စိတ်ညစ်ပေး ခဲ့လဲ  ။
သိပ် ပြေ တာပေါ့  ။

==> train-dev.bk <==
သူ ခင်ဗျား ကို ဒယ်ဇာ ပေး ဟုတ် ဝ ။
နင် ဖယ်သူ့ ဝို စိတ်ညစ်ပေး ခဲ့လဲ  ။
သိပ် ပြေ တာပေါ့  ။
==========
/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/3
head -n 3 for Dawei:
==> dev.dw <==
ခံဗျား ပ္လေးသေး ဟှလား ။
ကျွန်တော့် အစ်မက လွဲဟှီး အားလုံး အယ်မှာ ရှိဟှယ် ။
၁ နာရီ ပဲ ရှိသေးဟှယ် သူမ ညစာ ရှစ် ပီးပီ ။

==> test.dw <==
နန် ဟှဲဖြစ်ဟှိ ငို နေဟှယ် ။
သူ စိမကော ဖြစ် ဟှလား ။
သူ ဟှယ်ဒူ့ ဒါရိုက်တာ နူး ။

==> train-dev.dw <==
အဲဝယ်ဟှား ခံဗျား ဟှို အဲဇာ ပေး ဟှို့ မှုဝ ။
နန် ဟှယ်လူ့ ဟှို ဒုက္ခပေး ရစ်ဇာနူး ။
သိပ်  ပြေ တာပေါ့ ။

==> train.dw <==
အဲဝယ်ဟှား ခံဗျား ဟှို အဲဇာ ပေး ဟှို့ မှုဝ ။
နန် ဟှယ်လူ့ ဟှို ဒုက္ခပေး ရစ်ဇာနူး ။
သိပ်  ပြေ တာပေါ့ ။
head -n 3 for Beik:
==> dev.bk <==
နင် မ ပြေး သေးရလား ။
အားလုံးက ဒါမှာဘဲ အစ်မ တစ် ယောက် မရှိရ  ။
၁ နာရီ ပဲ ရှိ သေးရိ ဒယ်ကောင်မငယ်  ညစာ ချက် ပြီးလေ  ။

==> test.bk <==
နင် ဘာဖြစ်ရိ ငို နေရယ်  ။
ဒယ်ကောင်မငယ်  စိတ်မကောင်း မ ဖြစ် ရလား ။
နင် ဖယ်သူ့ ဒါရိုက်တာ  ။

==> train.bk <==
သူ ခင်ဗျား ကို ဒယ်ဇာ ပေး ဟုတ် ဝ ။
နင် ဖယ်သူ့ ဝို စိတ်ညစ်ပေး ခဲ့လဲ  ။
သိပ် ပြေ တာပေါ့  ။

==> train-dev.bk <==
သူ ခင်ဗျား ကို ဒယ်ဇာ ပေး ဟုတ် ဝ ။
နင် ဖယ်သူ့ ဝို စိတ်ညစ်ပေး ခဲ့လဲ  ။
သိပ် ပြေ တာပေါ့  ။
==========
/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/4
head -n 3 for Dawei:
==> dev.dw <==
ခံဗျား ပ္လေးသေး ဟှလား ။
ကျွန်တော့် အစ်မက လွဲဟှီး အားလုံး အယ်မှာ ရှိဟှယ် ။
၁ နာရီ ပဲ ရှိသေးဟှယ် သူမ ညစာ ရှစ် ပီးပီ ။

==> test.dw <==
အဲဇာဟှို နန် ဖရစ်ဆီး လိုက်လား ။
ရှစ်ကော ခြေနေ ကောန်း လာ ဟှို့ပဲ ။
အိရေး ပျက် ဇာဟှို ဖြစ်စေ ဇာဟှာ စိတ်ဖိစီးမှု ဆိုပီး လွယ်လွယ် န  ပြော ရပါဟှယ် ။

==> train-dev.dw <==
အဲဝယ်ဟှား ခံဗျား ဟှို အဲဇာ ပေး ဟှို့ မှုဝ ။
နန် ဟှယ်လူ့ ဟှို ဒုက္ခပေး ရစ်ဇာနူး ။
သိပ်  ပြေ တာပေါ့ ။

==> train.dw <==
အဲဝယ်ဟှား ခံဗျား ဟှို အဲဇာ ပေး ဟှို့ မှုဝ ။
နန် ဟှယ်လူ့ ဟှို ဒုက္ခပေး ရစ်ဇာနူး ။
သိပ်  ပြေ တာပေါ့ ။
head -n 3 for Beik:
==> dev.bk <==
နင် မ ပြေး သေးရလား ။
အားလုံးက ဒါမှာဘဲ အစ်မ တစ် ယောက် မရှိရ  ။
၁ နာရီ ပဲ ရှိ သေးရိ ဒယ်ကောင်မငယ်  ညစာ ချက် ပြီးလေ  ။

==> test.bk <==
ဒယ်ဇာ ကို မင်း ဖျက်ဆီး လိုက်ရယ်လား ။
မကြာခင် အခြေအနေ ဒေ ကောင်းလာ မှာ  ။
အအိပ်အစား ပျက်စေ ရဲ့ စိတ်ဖိစီးမှု ရိ အလွယ် ပြော နိုင်ပေါ့  ။

==> train.bk <==
သူ ခင်ဗျား ကို ဒယ်ဇာ ပေး ဟုတ် ဝ ။
နင် ဖယ်သူ့ ဝို စိတ်ညစ်ပေး ခဲ့လဲ  ။
သိပ် ပြေ တာပေါ့  ။

==> train-dev.bk <==
သူ ခင်ဗျား ကို ဒယ်ဇာ ပေး ဟုတ် ဝ ။
နင် ဖယ်သူ့ ဝို စိတ်ညစ်ပေး ခဲ့လဲ  ။
သိပ် ပြေ တာပေါ့  ။
==========
/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/5
head -n 3 for Dawei:
==> dev.dw <==
ခံဗျား ပ္လေးသေး ဟှလား ။
ကျွန်တော့် အစ်မက လွဲဟှီး အားလုံး အယ်မှာ ရှိဟှယ် ။
၁ နာရီ ပဲ ရှိသေးဟှယ် သူမ ညစာ ရှစ် ပီးပီ ။

==> test.dw <==
သူးနို့ အယ် မှာ တာဝန်ထမ်းဆော် ကေ့ဟှို့လား ။
မီးနူးကို နည်းညစ်ပတ်ပတ်ဟှီး ။
စာ ဝီ ဇာလား ။

==> train-dev.dw <==
အဲဝယ်ဟှား ခံဗျား ဟှို အဲဇာ ပေး ဟှို့ မှုဝ ။
နန် ဟှယ်လူ့ ဟှို ဒုက္ခပေး ရစ်ဇာနူး ။
သိပ်  ပြေ တာပေါ့ ။

==> train.dw <==
အဲဝယ်ဟှား ခံဗျား ဟှို အဲဇာ ပေး ဟှို့ မှုဝ ။
နန် ဟှယ်လူ့ ဟှို ဒုက္ခပေး ရစ်ဇာနူး ။
သိပ်  ပြေ တာပေါ့ ။
head -n 3 for Beik:
==> dev.bk <==
နင် မ ပြေး သေးရလား ။
အားလုံးက ဒါမှာဘဲ အစ်မ တစ် ယောက် မရှိရ  ။
၁ နာရီ ပဲ ရှိ သေးရိ ဒယ်ကောင်မငယ်  ညစာ ချက် ပြီးလေ  ။

==> test.bk <==
သူ့လို ဒယ်မှာ တာဝန် ထမ်း ကြမယ်လား ။
မီနူး လည်း အား ညစ်ပတ်  ။
စာ ဝေ ရယ်လား ။

==> train.bk <==
သူ ခင်ဗျား ကို ဒယ်ဇာ ပေး ဟုတ် ဝ ။
နင် ဖယ်သူ့ ဝို စိတ်ညစ်ပေး ခဲ့လဲ  ။
သိပ် ပြေ တာပေါ့  ။

==> train-dev.bk <==
သူ ခင်ဗျား ကို ဒယ်ဇာ ပေး ဟုတ် ဝ ။
နင် ဖယ်သူ့ ဝို စိတ်ညစ်ပေး ခဲ့လဲ  ။
သိပ် ပြေ တာပေါ့  ။
==========
/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/6
head -n 3 for Dawei:
==> dev.dw <==
ခံဗျား ပ္လေးသေး ဟှလား ။
ကျွန်တော့် အစ်မက လွဲဟှီး အားလုံး အယ်မှာ ရှိဟှယ် ။
၁ နာရီ ပဲ ရှိသေးဟှယ် သူမ ညစာ ရှစ် ပီးပီ ။

==> test.dw <==
အဲဇာ ကျွန်တော့် မီးမ မွီးနေ့ တွက်ပါ ။
သူ ထိုင်ခေါင်ထပ်မာ ထိုင် နေဟှယ် ။
လတ်တန်းဘော့ ဟှို ကျွန်တော် ပိ နိုင်ဆိုဟှီး နန် ထန် လား ။

==> train-dev.dw <==
အဲဝယ်ဟှား ခံဗျား ဟှို အဲဇာ ပေး ဟှို့ မှုဝ ။
နန် ဟှယ်လူ့ ဟှို ဒုက္ခပေး ရစ်ဇာနူး ။
သိပ်  ပြေ တာပေါ့ ။

==> train.dw <==
အဲဝယ်ဟှား ခံဗျား ဟှို အဲဇာ ပေး ဟှို့ မှုဝ ။
နန် ဟှယ်လူ့ ဟှို ဒုက္ခပေး ရစ်ဇာနူး ။
သိပ်  ပြေ တာပေါ့ ။
head -n 3 for Beik:
==> dev.bk <==
နင် မ ပြေး သေးရလား ။
အားလုံးက ဒါမှာဘဲ အစ်မ တစ် ယောက် မရှိရ  ။
၁ နာရီ ပဲ ရှိ သေးရိ ဒယ်ကောင်မငယ်  ညစာ ချက် ပြီးလေ  ။

==> test.bk <==
ဒယ်ဇာ ငါ့ မိန်းမ မွေးနေ့ တွက်ပန်း  ။
သူ ထိုင်ခုံ ပေါ်မှာ ထိုင် နေရယ် ။
တံခါးပေါက် ကို ငါ ပိတ် နိုင်တယ်လို့ နင် ထင် နေလား  ။

==> train.bk <==
သူ ခင်ဗျား ကို ဒယ်ဇာ ပေး ဟုတ် ဝ ။
နင် ဖယ်သူ့ ဝို စိတ်ညစ်ပေး ခဲ့လဲ  ။
သိပ် ပြေ တာပေါ့  ။

==> train-dev.bk <==
သူ ခင်ဗျား ကို ဒယ်ဇာ ပေး ဟုတ် ဝ ။
နင် ဖယ်သူ့ ဝို စိတ်ညစ်ပေး ခဲ့လဲ  ။
သိပ် ပြေ တာပေါ့  ။
==========
/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/7
head -n 3 for Dawei:
==> dev.dw <==
ခံဗျား ပ္လေးသေး ဟှလား ။
ကျွန်တော့် အစ်မက လွဲဟှီး အားလုံး အယ်မှာ ရှိဟှယ် ။
၁ နာရီ ပဲ ရှိသေးဟှယ် သူမ ညစာ ရှစ် ပီးပီ ။

==> test.dw <==
ကိုယ် နန့်နဲ့ တူးတူ နေ ရဝို့လား ။
ကျွန်တော် ရောင်းတစ်ရောင်းမှာ တွမ်းရေးမှူး လောက်ဟှို့ စိကူး ခဲ့ဟှယ် ။
သူ ချင်း ဆို ဟှ ၊ ဆို လား ။

==> train-dev.dw <==
အဲဝယ်ဟှား ခံဗျား ဟှို အဲဇာ ပေး ဟှို့ မှုဝ ။
နန် ဟှယ်လူ့ ဟှို ဒုက္ခပေး ရစ်ဇာနူး ။
သိပ်  ပြေ တာပေါ့ ။

==> train.dw <==
အဲဝယ်ဟှား ခံဗျား ဟှို အဲဇာ ပေး ဟှို့ မှုဝ ။
နန် ဟှယ်လူ့ ဟှို ဒုက္ခပေး ရစ်ဇာနူး ။
သိပ်  ပြေ တာပေါ့ ။
head -n 3 for Beik:
==> dev.bk <==
နင် မ ပြေး သေးရလား ။
အားလုံးက ဒါမှာဘဲ အစ်မ တစ် ယောက် မရှိရ  ။
၁ နာရီ ပဲ ရှိ သေးရိ ဒယ်ကောင်မငယ်  ညစာ ချက် ပြီးလေ  ။

==> test.bk <==
ငါ နင် နဲ့တူးတူ နေ ရမယ်လား ။
ငါတို့ ရုံး တစ် ရုံး မှာ အတွင်းရေးမှူး လုပ် ဝို့ စိတ်ကူး ခဲ့ရယ်  ။
ဒယ်ကောင်မ သီချင်း မ ဆို ရနား ၊ ဆို ရား  ။

==> train.bk <==
သူ ခင်ဗျား ကို ဒယ်ဇာ ပေး ဟုတ် ဝ ။
နင် ဖယ်သူ့ ဝို စိတ်ညစ်ပေး ခဲ့လဲ  ။
သိပ် ပြေ တာပေါ့  ။

==> train-dev.bk <==
သူ ခင်ဗျား ကို ဒယ်ဇာ ပေး ဟုတ် ဝ ။
နင် ဖယ်သူ့ ဝို စိတ်ညစ်ပေး ခဲ့လဲ  ။
သိပ် ပြေ တာပေါ့  ။
==========
/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/8
head -n 3 for Dawei:
==> dev.dw <==
ခံဗျား ပ္လေးသေး ဟှလား ။
ကျွန်တော့် အစ်မက လွဲဟှီး အားလုံး အယ်မှာ ရှိဟှယ် ။
၁ နာရီ ပဲ ရှိသေးဟှယ် သူမ ညစာ ရှစ် ပီးပီ ။

==> test.dw <==
ဟှိုဖော့သယ်ဟှ သူ့ မဲသားဟှို ပ္လန် ပို့ လား  ။
ရေတွင်းထဲဟှို ကလယားထိလ ရေဟှို လှိုင်းထ သွားဘဲစာ ဟှယ်မာ နူး ။
ကျွန်တော် အယ်ဇာဂို ခွပ်လွတ် ဟှို့ စိမှေ့ဟှ ။

==> train-dev.dw <==
အဲဝယ်ဟှား ခံဗျား ဟှို အဲဇာ ပေး ဟှို့ မှုဝ ။
နန် ဟှယ်လူ့ ဟှို ဒုက္ခပေး ရစ်ဇာနူး ။
သိပ်  ပြေ တာပေါ့ ။

==> train.dw <==
အဲဝယ်ဟှား ခံဗျား ဟှို အဲဇာ ပေး ဟှို့ မှုဝ ။
နန် ဟှယ်လူ့ ဟှို ဒုက္ခပေး ရစ်ဇာနူး ။
သိပ်  ပြေ တာပေါ့ ။
head -n 3 for Beik:
==> dev.bk <==
နင် မ ပြေး သေးရလား ။
အားလုံးက ဒါမှာဘဲ အစ်မ တစ် ယောက် မရှိရ  ။
၁ နာရီ ပဲ ရှိ သေးရိ ဒယ်ကောင်မငယ်  ညစာ ချက် ပြီးလေ  ။

==> test.bk <==
ဟုတ် ဖောက်သည် အမဲသား ပြန် ပေးရယ်လား  ။
ရေတွင်း ထဲကို ကျသွားပေမဲ့ တွင်းထဲက ရေကို လှိုင်းထလှုပ်ရှား မ သွား စေတဲ့ အရာ ဟာ ဘာဇာ ။
ကျွန်တော် အဲဒါကို ခွင့်လွှတ် ဖို့ ဆန္ဒ မ ရှိ ရ  ။

==> train.bk <==
သူ ခင်ဗျား ကို ဒယ်ဇာ ပေး ဟုတ် ဝ ။
နင် ဖယ်သူ့ ဝို စိတ်ညစ်ပေး ခဲ့လဲ  ။
သိပ် ပြေ တာပေါ့  ။

==> train-dev.bk <==
သူ ခင်ဗျား ကို ဒယ်ဇာ ပေး ဟုတ် ဝ ။
နင် ဖယ်သူ့ ဝို စိတ်ညစ်ပေး ခဲ့လဲ  ။
သိပ် ပြေ တာပေါ့  ။
==========
/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/9
head -n 3 for Dawei:
==> dev.dw <==
ခံဗျား ပ္လေးသေး ဟှလား ။
ကျွန်တော့် အစ်မက လွဲဟှီး အားလုံး အယ်မှာ ရှိဟှယ် ။
၁ နာရီ ပဲ ရှိသေးဟှယ် သူမ ညစာ ရှစ် ပီးပီ ။

==> test.dw <==
ငါ အိ ရှင်ဟှယ် အယ်ပေမယ့် အိ နိုင်ဟှ ။
အဲထက် ပိုကောန်းဇာ မှေ့မှုပီ ။
ကျွန်တော် အဲဟှို သွား ရဇာ စယ်ဇာ ဘဲ့ ။

==> train-dev.dw <==
အဲဝယ်ဟှား ခံဗျား ဟှို အဲဇာ ပေး ဟှို့ မှုဝ ။
နန် ဟှယ်လူ့ ဟှို ဒုက္ခပေး ရစ်ဇာနူး ။
သိပ်  ပြေ တာပေါ့ ။

==> train.dw <==
အဲဝယ်ဟှား ခံဗျား ဟှို အဲဇာ ပေး ဟှို့ မှုဝ ။
နန် ဟှယ်လူ့ ဟှို ဒုက္ခပေး ရစ်ဇာနူး ။
သိပ်  ပြေ တာပေါ့ ။
head -n 3 for Beik:
==> dev.bk <==
နင် မ ပြေး သေးရလား ။
အားလုံးက ဒါမှာဘဲ အစ်မ တစ် ယောက် မရှိရ  ။
၁ နာရီ ပဲ ရှိ သေးရိ ဒယ်ကောင်မငယ်  ညစာ ချက် ပြီးလေ  ။

==> test.bk <==
ငါ အိပ် ချင်ရယ် ဒါမဲ့ မ အိပ် နိုင်ရ ။
ဒါထက် ကောင်း ဇာ ရှိဝို့ မ ဟုတ် ပြီ  ။
ကျွန်တော် ဒယ်ဝို သွား ရဇာ ပျော် လိုက်တာ ။

==> train.bk <==
သူ ခင်ဗျား ကို ဒယ်ဇာ ပေး ဟုတ် ဝ ။
နင် ဖယ်သူ့ ဝို စိတ်ညစ်ပေး ခဲ့လဲ  ။
သိပ် ပြေ တာပေါ့  ။

==> train-dev.bk <==
သူ ခင်ဗျား ကို ဒယ်ဇာ ပေး ဟုတ် ဝ ။
နင် ဖယ်သူ့ ဝို စိတ်ညစ်ပေး ခဲ့လဲ  ။
သိပ် ပြေ တာပေါ့  ။
==========
/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/10
head -n 3 for Dawei:
==> dev.dw <==
သူးနို့ ကြိုးစား ဟှားကေဟှလား ။
အယ်ပေမဲ့ အယ်လိုန နိကူးချုပ်သွားတာမှုတ်ဟှ ။
သူးနို့ ဟှယ်ဒူ့ မီး လေ နူး ။

==> test.dw <==
ဟှယ်ဒူ့ မှန်းဘုံး နူး ။
ဟှယ်ဒူ့ မှန်းဘုံး နူး ။
သူ စိဆိုး ဟှလား ။

==> train-dev.dw <==
အဲဝယ်ဟှား ခံဗျား ဟှို အဲဇာ ပေး ဟှို့ မှုဝ ။
နန် ဟှယ်လူ့ ဟှို ဒုက္ခပေး ရစ်ဇာနူး ။
သိပ်  ပြေ တာပေါ့ ။

==> train.dw <==
အဲဝယ်ဟှား ခံဗျား ဟှို အဲဇာ ပေး ဟှို့ မှုဝ ။
နန် ဟှယ်လူ့ ဟှို ဒုက္ခပေး ရစ်ဇာနူး ။
သိပ်  ပြေ တာပေါ့ ။
head -n 3 for Beik:
==> dev.bk <==
သူ့လို မ ကြိုးစား ကြကလား ။
ဒါမဲ့ ဒီလိုနဲ့ နိဂုံးချုပ်သွားတာမဟုတ်ဘူး ။
သူတို့ ဖယ်သူ့ သားသမီးလဲ ။

==> test.bk <==
အယ့်ဒါ ဘယ်သူ့ ထမင်းဘူး ရိ  ။
အယ့်ဒါ ဘယ်သူ့ ထမင်းဘူး ရိ  ။
ဒယ်ကောင်မငယ်  စိတ်မဆိုး ဝလား ။

==> train.bk <==
သူ ခင်ဗျား ကို ဒယ်ဇာ ပေး ဟုတ် ဝ ။
နင် ဖယ်သူ့ ဝို စိတ်ညစ်ပေး ခဲ့လဲ  ။
သိပ် ပြေ တာပေါ့  ။

==> train-dev.bk <==
သူ ခင်ဗျား ကို ဒယ်ဇာ ပေး ဟုတ် ဝ ။
နင် ဖယ်သူ့ ဝို စိတ်ညစ်ပေး ခဲ့လဲ  ။
သိပ် ပြေ တာပေါ့  ။
==========
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/data/word/dw-bk$
```

for rk-bk pair:  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/data/word/rk-bk$ ./head-3-for-all.sh
/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/1
head -n 3 for Rakhine:
==> dev.rk <==
ထိုမချေ  ငါ့ကို စ ခစွာလား ။
မင်း ဆင် စီး ဖူး ပါလား ။
ကျွန်တော် သတင်းစာ ရ နိုင်ဖို့လား ။

==> test.rk <==
ကျွန်တော်က သာမန် ကစားသမားအဆင့် လောက်ပါယာ ။
ယင်းချင့်ဇာလောက် မှန် လေး ။
သူရို့ကိုယ်သူရို့ သိဂတ်ပါရေ ။

==> train-dev.rk <==
တွင်း မ တူး ပါလား ။
အမျိုးသား ချဖောင်းသာ ဇာမာ လေး ။
ထိုမချေ  ဘေးမာ ဟိရေ   စာအုပ် ။

==> train.rk <==
တွင်း မ တူး ပါလား ။
အမျိုးသား ချဖောင်းသာ ဇာမာ လေး ။
ထိုမချေ  ဘေးမာ ဟိရေ   စာအုပ် ။
head -n 3 for Beik:
==> dev.bk <==
ဒယ်ကောင်ငါ့ ဝို စ ခဲ့ရယ်လား  ။
နင် ဆင် စီး ဖူးလား  ။
သတင်းစာ ရှိ ရယ်လား  ။

==> test.bk <==
ငါ ရိုးရိုး ကစားသမားပဲ လန်း  ။
အယ့်ဒါ ဘဇာလောက် မှန်  ရိ  ။
သူတို့ကိုယ်သူတို့ သိ ရယ်  ။

==> train.bk <==
တွင်း မ တူး ရလား ။
အမျိုးသား သန့်စင်ခန်း ဘာမှာ  ။
နင့် ဘေး မှာ ရှိတဲ့ စာအုပ်  ။

==> train-dev.bk <==
တွင်း မ တူး ရလား ။
အမျိုးသား သန့်စင်ခန်း ဘာမှာ  ။
နင့် ဘေး မှာ ရှိတဲ့ စာအုပ်  ။
==========
/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/2
head -n 3 for Rakhine:
==> dev.rk <==
ထိုမချေ  ငါ့ကို စ ခစွာလား ။
မင်း ဆင် စီး ဖူး ပါလား ။
ကျွန်တော် သတင်းစာ ရ နိုင်ဖို့လား ။

==> test.rk <==
တွင်း မ တူး ပါလား ။
အမျိုးသား ချဖောင်းသာ ဇာမာ လေး ။
ထိုမချေ  ဘေးမာ ဟိရေ   စာအုပ် ။

==> train-dev.rk <==
ကျွန်တော်က သာမန် ကစားသမားအဆင့် လောက်ပါယာ ။
ယင်းချင့်ဇာလောက် မှန် လေး ။
သူရို့ကိုယ်သူရို့ သိဂတ်ပါရေ ။

==> train.rk <==
ကျွန်တော်က သာမန် ကစားသမားအဆင့် လောက်ပါယာ ။
ယင်းချင့်ဇာလောက် မှန် လေး ။
သူရို့ကိုယ်သူရို့ သိဂတ်ပါရေ ။
head -n 3 for Beik:
==> dev.bk <==
ဒယ်ကောင်ငါ့ ဝို စ ခဲ့ရယ်လား  ။
နင် ဆင် စီး ဖူးလား  ။
သတင်းစာ ရှိ ရယ်လား  ။

==> test.bk <==
တွင်း မ တူး ရလား ။
အမျိုးသား သန့်စင်ခန်း ဘာမှာ  ။
နင့် ဘေး မှာ ရှိတဲ့ စာအုပ်  ။

==> train.bk <==
ငါ ရိုးရိုး ကစားသမားပဲ လန်း  ။
အယ့်ဒါ ဘဇာလောက် မှန်  ရိ  ။
သူတို့ကိုယ်သူတို့ သိ ရယ်  ။

==> train-dev.bk <==
ငါ ရိုးရိုး ကစားသမားပဲ လန်း  ။
အယ့်ဒါ ဘဇာလောက် မှန်  ရိ  ။
သူတို့ကိုယ်သူတို့ သိ ရယ်  ။
==========
/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/3
head -n 3 for Rakhine:
==> dev.rk <==
ထိုမချေ  ငါ့ကို စ ခစွာလား ။
မင်း ဆင် စီး ဖူး ပါလား ။
ကျွန်တော် သတင်းစာ ရ နိုင်ဖို့လား ။

==> test.rk <==
ယေကေ ငါရို့ တစ်ခုခု လား စား ကတ်မယ် ။
ဒေ အိတ် က ဆွဲရ ခက် လိုက်ရေ ။
သူရို့ အဂု တစ်ခုလေ့ မ လုပ် ပါ ။

==> train-dev.rk <==
ကျွန်တော်က သာမန် ကစားသမားအဆင့် လောက်ပါယာ ။
ယင်းချင့်ဇာလောက် မှန် လေး ။
သူရို့ကိုယ်သူရို့ သိဂတ်ပါရေ ။

==> train.rk <==
ကျွန်တော်က သာမန် ကစားသမားအဆင့် လောက်ပါယာ ။
ယင်းချင့်ဇာလောက် မှန် လေး ။
သူရို့ကိုယ်သူရို့ သိဂတ်ပါရေ ။
head -n 3 for Beik:
==> dev.bk <==
ဒယ်ကောင်ငါ့ ဝို စ ခဲ့ရယ်လား  ။
နင် ဆင် စီး ဖူးလား  ။
သတင်းစာ ရှိ ရယ်လား  ။

==> test.bk <==
ဒါဆို တို့တခုခု သွား စားရမယ်လေ  ။
ဒယ် အိတ် ဆွဲရ အား ခက် မား ။
သူတို့ အခု ဘား မ လုပ် ဝ  ။

==> train.bk <==
ငါ ရိုးရိုး ကစားသမားပဲ လန်း  ။
အယ့်ဒါ ဘဇာလောက် မှန်  ရိ  ။
သူတို့ကိုယ်သူတို့ သိ ရယ်  ။

==> train-dev.bk <==
ငါ ရိုးရိုး ကစားသမားပဲ လန်း  ။
အယ့်ဒါ ဘဇာလောက် မှန်  ရိ  ။
သူတို့ကိုယ်သူတို့ သိ ရယ်  ။
==========
/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/4
head -n 3 for Rakhine:
==> dev.rk <==
ထိုမချေ  ငါ့ကို စ ခစွာလား ။
မင်း ဆင် စီး ဖူး ပါလား ။
ကျွန်တော် သတင်းစာ ရ နိုင်ဖို့လား ။

==> test.rk <==
ဆိုးပါရေ ။
ယင်ချင်က အကုန်အကျ များလွန်း ရေ ။
ယင်း ကို မ လား ပါ လား ။

==> train-dev.rk <==
ကျွန်တော်က သာမန် ကစားသမားအဆင့် လောက်ပါယာ ။
ယင်းချင့်ဇာလောက် မှန် လေး ။
သူရို့ကိုယ်သူရို့ သိဂတ်ပါရေ ။

==> train.rk <==
ကျွန်တော်က သာမန် ကစားသမားအဆင့် လောက်ပါယာ ။
ယင်းချင့်ဇာလောက် မှန် လေး ။
သူရို့ကိုယ်သူရို့ သိဂတ်ပါရေ ။
head -n 3 for Beik:
==> dev.bk <==
ဒယ်ကောင်ငါ့ ဝို စ ခဲ့ရယ်လား  ။
နင် ဆင် စီး ဖူးလား  ။
သတင်းစာ ရှိ ရယ်လား  ။

==> test.bk <==
ဆိုးပဲ့  ။
မီဝေးအားလုံးမှား ။
အဲဒီကို မ သော ရလား ။

==> train.bk <==
ငါ ရိုးရိုး ကစားသမားပဲ လန်း  ။
အယ့်ဒါ ဘဇာလောက် မှန်  ရိ  ။
သူတို့ကိုယ်သူတို့ သိ ရယ်  ။

==> train-dev.bk <==
ငါ ရိုးရိုး ကစားသမားပဲ လန်း  ။
အယ့်ဒါ ဘဇာလောက် မှန်  ရိ  ။
သူတို့ကိုယ်သူတို့ သိ ရယ်  ။
==========
/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/5
head -n 3 for Rakhine:
==> dev.rk <==
ထိုမချေ  ငါ့ကို စ ခစွာလား ။
မင်း ဆင် စီး ဖူး ပါလား ။
ကျွန်တော် သတင်းစာ ရ နိုင်ဖို့လား ။

==> test.rk <==
ယင်းချင့်ကို သိမ်းသိမ်း မ သိမ်းသိမ်း ။
ဒေချင့် ဇာသူ့ အိတ် လေး ။
မင်းက ရက်ပြတ် ရှေ့ကို ကြို တွေးတတ်ရေဆိုစွာကျွန်တော်သိရေ။

==> train-dev.rk <==
ကျွန်တော်က သာမန် ကစားသမားအဆင့် လောက်ပါယာ ။
ယင်းချင့်ဇာလောက် မှန် လေး ။
သူရို့ကိုယ်သူရို့ သိဂတ်ပါရေ ။

==> train.rk <==
ကျွန်တော်က သာမန် ကစားသမားအဆင့် လောက်ပါယာ ။
ယင်းချင့်ဇာလောက် မှန် လေး ။
သူရို့ကိုယ်သူရို့ သိဂတ်ပါရေ ။
head -n 3 for Beik:
==> dev.bk <==
ဒယ်ကောင်ငါ့ ဝို စ ခဲ့ရယ်လား  ။
နင် ဆင် စီး ဖူးလား  ။
သတင်းစာ ရှိ ရယ်လား  ။

==> test.bk <==
နင့်စာနင် သိမ်းချင်သိမ်း မသိမ်းချင်နေ  ။
အယ့်ဒါ ဘယ်သူ့ အိတ် ရိ  ။
မင်း က အမြဲ ကြိုသိနေရယ်ဆိုတာ ငါသိ ရယ်လန်း  ။

==> train.bk <==
ငါ ရိုးရိုး ကစားသမားပဲ လန်း  ။
အယ့်ဒါ ဘဇာလောက် မှန်  ရိ  ။
သူတို့ကိုယ်သူတို့ သိ ရယ်  ။

==> train-dev.bk <==
ငါ ရိုးရိုး ကစားသမားပဲ လန်း  ။
အယ့်ဒါ ဘဇာလောက် မှန်  ရိ  ။
သူတို့ကိုယ်သူတို့ သိ ရယ်  ။
==========
/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/6
head -n 3 for Rakhine:
==> dev.rk <==
ထိုမချေ  ငါ့ကို စ ခစွာလား ။
မင်း ဆင် စီး ဖူး ပါလား ။
ကျွန်တော် သတင်းစာ ရ နိုင်ဖို့လား ။

==> test.rk <==
ကျွန်တော် ကျောင်းသား တိ ကို စကား ပြော နီရေ ။
အကြင်နာ ကော ဟိ ပါ ယင့်လား ။
အစိမ်းရောင် ဟိရေ ငှက် တိ ။

==> train-dev.rk <==
ကျွန်တော်က သာမန် ကစားသမားအဆင့် လောက်ပါယာ ။
ယင်းချင့်ဇာလောက် မှန် လေး ။
သူရို့ကိုယ်သူရို့ သိဂတ်ပါရေ ။

==> train.rk <==
ကျွန်တော်က သာမန် ကစားသမားအဆင့် လောက်ပါယာ ။
ယင်းချင့်ဇာလောက် မှန် လေး ။
သူရို့ကိုယ်သူရို့ သိဂတ်ပါရေ ။
head -n 3 for Beik:
==> dev.bk <==
ဒယ်ကောင်ငါ့ ဝို စ ခဲ့ရယ်လား  ။
နင် ဆင် စီး ဖူးလား  ။
သတင်းစာ ရှိ ရယ်လား  ။

==> test.bk <==
ကျွန်တော် ကျောင်းသား တွေ ကို စကား ပြော နေရယ်  ။
အကြင်နာ ကော ရှိ ရယ်ပဲ့လား ။
အစိမ်းရောင် ငှက် ဒွေ  ။

==> train.bk <==
ငါ ရိုးရိုး ကစားသမားပဲ လန်း  ။
အယ့်ဒါ ဘဇာလောက် မှန်  ရိ  ။
သူတို့ကိုယ်သူတို့ သိ ရယ်  ။

==> train-dev.bk <==
ငါ ရိုးရိုး ကစားသမားပဲ လန်း  ။
အယ့်ဒါ ဘဇာလောက် မှန်  ရိ  ။
သူတို့ကိုယ်သူတို့ သိ ရယ်  ။
==========
/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/7
head -n 3 for Rakhine:
==> dev.rk <==
ထိုမချေ  ငါ့ကို စ ခစွာလား ။
မင်း ဆင် စီး ဖူး ပါလား ။
ကျွန်တော် သတင်းစာ ရ နိုင်ဖို့လား ။

==> test.rk <==
မင်း  ဇာသူ့ ကို မ နိုင်လေး ။
အလှပ ကလိန့်မေချေတိ  အခန်း ထဲ မာ ဟိရေ။
ဇာဖြစ်လို့ မ က စွာလေး ။

==> train-dev.rk <==
ကျွန်တော်က သာမန် ကစားသမားအဆင့် လောက်ပါယာ ။
ယင်းချင့်ဇာလောက် မှန် လေး ။
သူရို့ကိုယ်သူရို့ သိဂတ်ပါရေ ။

==> train.rk <==
ကျွန်တော်က သာမန် ကစားသမားအဆင့် လောက်ပါယာ ။
ယင်းချင့်ဇာလောက် မှန် လေး ။
သူရို့ကိုယ်သူရို့ သိဂတ်ပါရေ ။
head -n 3 for Beik:
==> dev.bk <==
ဒယ်ကောင်ငါ့ ဝို စ ခဲ့ရယ်လား  ။
နင် ဆင် စီး ဖူးလား  ။
သတင်းစာ ရှိ ရယ်လား  ။

==> test.bk <==
နင် ဖယ်သူ့ ဝို မ နိုင်ရယ်  ။
မိန်းမချော ငယ် ရ အခန်း ထဲမှာ ရှိ ရယ်  ။
ဘာဖြစ်ရိ မ က  ။

==> train.bk <==
ငါ ရိုးရိုး ကစားသမားပဲ လန်း  ။
အယ့်ဒါ ဘဇာလောက် မှန်  ရိ  ။
သူတို့ကိုယ်သူတို့ သိ ရယ်  ။

==> train-dev.bk <==
ငါ ရိုးရိုး ကစားသမားပဲ လန်း  ။
အယ့်ဒါ ဘဇာလောက် မှန်  ရိ  ။
သူတို့ကိုယ်သူတို့ သိ ရယ်  ။
==========
/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/8
head -n 3 for Rakhine:
==> dev.rk <==
ထိုမချေ  ငါ့ကို စ ခစွာလား ။
မင်း ဆင် စီး ဖူး ပါလား ။
ကျွန်တော် သတင်းစာ ရ နိုင်ဖို့လား ။

==> test.rk <==
အားလုံး ကို သူ ကတိ မ ဖျက် ခပါ ။
ကျွန်တော်ကြားရစွာက တစ်ပတ် ငါးကြိမ်လတ်။
ထိုမချေ မင်း ကို ဆက်သွယ် ဖို့လား ။

==> train-dev.rk <==
ကျွန်တော်က သာမန် ကစားသမားအဆင့် လောက်ပါယာ ။
ယင်းချင့်ဇာလောက် မှန် လေး ။
သူရို့ကိုယ်သူရို့ သိဂတ်ပါရေ ။

==> train.rk <==
ကျွန်တော်က သာမန် ကစားသမားအဆင့် လောက်ပါယာ ။
ယင်းချင့်ဇာလောက် မှန် လေး ။
သူရို့ကိုယ်သူရို့ သိဂတ်ပါရေ ။
head -n 3 for Beik:
==> dev.bk <==
ဒယ်ကောင်ငါ့ ဝို စ ခဲ့ရယ်လား  ။
နင် ဆင် စီး ဖူးလား  ။
သတင်းစာ ရှိ ရယ်လား  ။

==> test.bk <==
အားလုံးကို သူ ကတိ မ ဖျက် ရ ။
ငါ ကြား တာတော့ တပတ် ငါး ကြိမ် တဲ့  ။
သူ ခင်ဗျား ကို ဆက်သွယ် မယ်လား ။

==> train.bk <==
ငါ ရိုးရိုး ကစားသမားပဲ လန်း  ။
အယ့်ဒါ ဘဇာလောက် မှန်  ရိ  ။
သူတို့ကိုယ်သူတို့ သိ ရယ်  ။

==> train-dev.bk <==
ငါ ရိုးရိုး ကစားသမားပဲ လန်း  ။
အယ့်ဒါ ဘဇာလောက် မှန်  ရိ  ။
သူတို့ကိုယ်သူတို့ သိ ရယ်  ။
==========
/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/9
head -n 3 for Rakhine:
==> dev.rk <==
ထိုမချေ  ငါ့ကို စ ခစွာလား ။
မင်း ဆင် စီး ဖူး ပါလား ။
ကျွန်တော် သတင်းစာ ရ နိုင်ဖို့လား ။

==> test.rk <==
ယင်းချင့် ကို ပြင် လိုက်စွာလား ။
ကိုယ် မြတ်နိုး ရေ  ဘဝ မာ ထာဝရ  နီ ဖို့ ဆုံးဖြတ်ပြီးသားပါ ။
ဒေကလိန့်မေ  ဖြတ် ခပါရေ ။

==> train-dev.rk <==
ကျွန်တော်က သာမန် ကစားသမားအဆင့် လောက်ပါယာ ။
ယင်းချင့်ဇာလောက် မှန် လေး ။
သူရို့ကိုယ်သူရို့ သိဂတ်ပါရေ ။

==> train.rk <==
ကျွန်တော်က သာမန် ကစားသမားအဆင့် လောက်ပါယာ ။
ယင်းချင့်ဇာလောက် မှန် လေး ။
သူရို့ကိုယ်သူရို့ သိဂတ်ပါရေ ။
head -n 3 for Beik:
==> dev.bk <==
ဒယ်ကောင်ငါ့ ဝို စ ခဲ့ရယ်လား  ။
နင် ဆင် စီး ဖူးလား  ။
သတင်းစာ ရှိ ရယ်လား  ။

==> test.bk <==
ဒယ်ဇာ ကို ပြင် လိုက်ရယ်လား ။
နင် ကြိုက် တဲ့ ဘဝ မှာ ငါ တစ်သက်လုံး နေ ဖို့ ဆုံးဖြတ် ပြီးသား  ။
ဒယ်ကောင်မငယ် ဖြတ် ခဲ့ပါရယ် ။

==> train.bk <==
ငါ ရိုးရိုး ကစားသမားပဲ လန်း  ။
အယ့်ဒါ ဘဇာလောက် မှန်  ရိ  ။
သူတို့ကိုယ်သူတို့ သိ ရယ်  ။

==> train-dev.bk <==
ငါ ရိုးရိုး ကစားသမားပဲ လန်း  ။
အယ့်ဒါ ဘဇာလောက် မှန်  ရိ  ။
သူတို့ကိုယ်သူတို့ သိ ရယ်  ။
==========
/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/10
head -n 3 for Rakhine:
==> dev.rk <==
သူ မင်းကို တွိလို့ ဝမ်းသာ နီစွာ ။
ငါရို့တိ နောက်ထပ် ဇာခါ  တွိကတ်ဖို့လေ ။
သူ ဇာ ပြော နိုင်စွာလေး ။

==> test.rk <==
မင်း ဇာကို ရွီး ဖို့လေး။
ယင်းချင့် သူ  ရို့ အတွက် အလွယ်ချေပါ ။
မင်း  ဇာသူ့ ကို အပြစ်တင် ခစွာလေး ။

==> train-dev.rk <==
ကျွန်တော်က သာမန် ကစားသမားအဆင့် လောက်ပါယာ ။
ယင်းချင့်ဇာလောက် မှန် လေး ။
သူရို့ကိုယ်သူရို့ သိဂတ်ပါရေ ။

==> train.rk <==
ကျွန်တော်က သာမန် ကစားသမားအဆင့် လောက်ပါယာ ။
ယင်းချင့်ဇာလောက် မှန် လေး ။
သူရို့ကိုယ်သူရို့ သိဂတ်ပါရေ ။
head -n 3 for Beik:
==> dev.bk <==
သူ မင့်ကို တွေ့ ရရိ ဝမ်းသာ နေဇာ  ။
တို့တေ နောက်ထပ် ဘယ်တော့ ဆုံကြ မလဲ ။
သူ ဘာ ပြော နိုင်ရိ  ။

==> test.bk <==
နင် ဘာဇာ ရွေး ဝို့  ။
အဲ့ဇာက  သူတို့ အတွက် လွယ်လွယ်ငယ်ပဲ  ။
နင် ဖယ်သူ့ ဝို အပြစ် ပြော ခဲ့လဲ  ။

==> train.bk <==
ငါ ရိုးရိုး ကစားသမားပဲ လန်း  ။
အယ့်ဒါ ဘဇာလောက် မှန်  ရိ  ။
သူတို့ကိုယ်သူတို့ သိ ရယ်  ။

==> train-dev.bk <==
ငါ ရိုးရိုး ကစားသမားပဲ လန်း  ။
အယ့်ဒါ ဘဇာလောက် မှန်  ရိ  ။
သူတို့ကိုယ်သူတို့ သိ ရယ်  ။
==========
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/data/word/rk-bk$
```

## Vocab Building

write build-vocab.sh for bk-dw pair:  

```bash
#!/bin/bash

## Written by Ye, Affiliate Professor, CADT, Cambodia
## Last updated: 30 May 2022
## Vocab building with marian

for i in {1..10}
do
   cd $i; mkdir vocab;

   # for dw
   cat ./train.dw ./dev.dw > train-dev.dw
   marian-vocab < ./train-dev.dw > ./vocab/vocab.dw.yml
   # for bk
   cat ./train.bk ./dev.bk > train-dev.bk
   marian-vocab < ./train-dev.bk > ./vocab/vocab.bk.yml
   pwd; wc ./vocab/*.{dw,bk}.yml;

   cd ..;
done
```

run build-vocab.sh for dw-bk pair:  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/data/word/dw-bk$ ./build-vocab.sh | tee build-vocab.log
[2022-05-30 17:02:34] Creating vocabulary...
[2022-05-30 17:02:34] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:02:35] Finished
[2022-05-30 17:02:35] Creating vocabulary...
[2022-05-30 17:02:35] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:02:35] Finished
/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/1
  7444  14890 235984 ./vocab/vocab.dw.yml
  5580  11162 164884 ./vocab/vocab.bk.yml
 13024  26052 400868 total
[2022-05-30 17:02:35] Creating vocabulary...
[2022-05-30 17:02:35] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:02:35] Finished
[2022-05-30 17:02:35] Creating vocabulary...
[2022-05-30 17:02:35] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:02:35] Finished
/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/2
  7416  14834 235271 ./vocab/vocab.dw.yml
  5573  11148 164680 ./vocab/vocab.bk.yml
 12989  25982 399951 total
[2022-05-30 17:02:35] Creating vocabulary...
[2022-05-30 17:02:35] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:02:35] Finished
[2022-05-30 17:02:35] Creating vocabulary...
[2022-05-30 17:02:35] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:02:35] Finished
/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/3
  7381  14764 233509 ./vocab/vocab.dw.yml
  5528  11058 163311 ./vocab/vocab.bk.yml
 12909  25822 396820 total
[2022-05-30 17:02:35] Creating vocabulary...
[2022-05-30 17:02:35] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:02:35] Finished
[2022-05-30 17:02:35] Creating vocabulary...
[2022-05-30 17:02:35] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:02:35] Finished
/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/4
  7392  14786 233774 ./vocab/vocab.dw.yml
  5533  11068 162563 ./vocab/vocab.bk.yml
 12925  25854 396337 total
[2022-05-30 17:02:35] Creating vocabulary...
[2022-05-30 17:02:35] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:02:35] Finished
[2022-05-30 17:02:35] Creating vocabulary...
[2022-05-30 17:02:35] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:02:35] Finished
/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/5
  7424  14850 235559 ./vocab/vocab.dw.yml
  5513  11028 162525 ./vocab/vocab.bk.yml
 12937  25878 398084 total
[2022-05-30 17:02:35] Creating vocabulary...
[2022-05-30 17:02:35] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:02:35] Finished
[2022-05-30 17:02:35] Creating vocabulary...
[2022-05-30 17:02:35] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:02:35] Finished
/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/6
  7423  14848 235438 ./vocab/vocab.dw.yml
  5567  11136 164787 ./vocab/vocab.bk.yml
 12990  25984 400225 total
[2022-05-30 17:02:35] Creating vocabulary...
[2022-05-30 17:02:35] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:02:35] Finished
[2022-05-30 17:02:35] Creating vocabulary...
[2022-05-30 17:02:35] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:02:35] Finished
/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/7
  7445  14892 235808 ./vocab/vocab.dw.yml
  5568  11138 164545 ./vocab/vocab.bk.yml
 13013  26030 400353 total
[2022-05-30 17:02:35] Creating vocabulary...
[2022-05-30 17:02:35] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:02:35] Finished
[2022-05-30 17:02:36] Creating vocabulary...
[2022-05-30 17:02:36] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:02:36] Finished
/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/8
  7386  14774 233881 ./vocab/vocab.dw.yml
  5540  11082 163542 ./vocab/vocab.bk.yml
 12926  25856 397423 total
[2022-05-30 17:02:36] Creating vocabulary...
[2022-05-30 17:02:36] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:02:36] Finished
[2022-05-30 17:02:36] Creating vocabulary...
[2022-05-30 17:02:36] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:02:36] Finished
/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/9
  7397  14796 234973 ./vocab/vocab.dw.yml
  5532  11066 163226 ./vocab/vocab.bk.yml
 12929  25862 398199 total
[2022-05-30 17:02:36] Creating vocabulary...
[2022-05-30 17:02:36] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:02:36] Finished
[2022-05-30 17:02:36] Creating vocabulary...
[2022-05-30 17:02:36] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:02:36] Finished
/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/10
  7476  14954 237041 ./vocab/vocab.dw.yml
  5545  11092 164075 ./vocab/vocab.bk.yml
 13021  26046 401116 total
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/data/word/dw-bk$
```

bash script for building vocab of rk-bk:  

```bash
#!/bin/bash

## Written by Ye, Affiliate Professor, CADT, Cambodia
## Last updated: 30 May 2022
## Vocab building with marian for rk-bk language pair

for i in {1..10}
do
   cd $i; mkdir vocab;

   # for rk
   cat ./train.rk ./dev.rk > train-dev.rk
   marian-vocab < ./train-dev.rk > ./vocab/vocab.rk.yml
   # for bk
   cat ./train.bk ./dev.bk > train-dev.bk
   marian-vocab < ./train-dev.bk > ./vocab/vocab.bk.yml
   pwd; wc ./vocab/*.{rk,bk}.yml;

   cd ..;
done
```

run build-vocab.sh for rk-bk language pair:  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/data/word/rk-bk$ ./build-vocab.sh | tee build-vocab.log
[2022-05-30 17:08:48] Creating vocabulary...
[2022-05-30 17:08:48] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:08:48] Finished
[2022-05-30 17:08:48] Creating vocabulary...
[2022-05-30 17:08:48] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:08:48] Finished
/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/1
  9354  18710 308007 ./vocab/vocab.rk.yml
  9082  18166 286148 ./vocab/vocab.bk.yml
 18436  36876 594155 total
[2022-05-30 17:08:48] Creating vocabulary...
[2022-05-30 17:08:48] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:08:48] Finished
[2022-05-30 17:08:48] Creating vocabulary...
[2022-05-30 17:08:48] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:08:48] Finished
/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/2
  9377  18756 308810 ./vocab/vocab.rk.yml
  9076  18154 286074 ./vocab/vocab.bk.yml
 18453  36910 594884 total
[2022-05-30 17:08:48] Creating vocabulary...
[2022-05-30 17:08:48] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:08:48] Finished
[2022-05-30 17:08:48] Creating vocabulary...
[2022-05-30 17:08:48] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:08:48] Finished
/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/3
  9324  18650 306799 ./vocab/vocab.rk.yml
  9058  18118 285514 ./vocab/vocab.bk.yml
 18382  36768 592313 total
[2022-05-30 17:08:49] Creating vocabulary...
[2022-05-30 17:08:49] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:08:49] Finished
[2022-05-30 17:08:49] Creating vocabulary...
[2022-05-30 17:08:49] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:08:49] Finished
/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/4
  9362  18726 309034 ./vocab/vocab.rk.yml
  9114  18230 288274 ./vocab/vocab.bk.yml
 18476  36956 597308 total
[2022-05-30 17:08:49] Creating vocabulary...
[2022-05-30 17:08:49] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:08:49] Finished
[2022-05-30 17:08:49] Creating vocabulary...
[2022-05-30 17:08:49] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:08:49] Finished
/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/5
  9367  18736 309035 ./vocab/vocab.rk.yml
  9099  18200 287903 ./vocab/vocab.bk.yml
 18466  36936 596938 total
[2022-05-30 17:08:49] Creating vocabulary...
[2022-05-30 17:08:49] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:08:49] Finished
[2022-05-30 17:08:49] Creating vocabulary...
[2022-05-30 17:08:49] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:08:49] Finished
/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/6
  9309  18620 306625 ./vocab/vocab.rk.yml
  9051  18104 285480 ./vocab/vocab.bk.yml
 18360  36724 592105 total
[2022-05-30 17:08:49] Creating vocabulary...
[2022-05-30 17:08:49] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:08:49] Finished
[2022-05-30 17:08:49] Creating vocabulary...
[2022-05-30 17:08:49] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:08:49] Finished
/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/7
  9348  18698 308161 ./vocab/vocab.rk.yml
  9093  18188 287035 ./vocab/vocab.bk.yml
 18441  36886 595196 total
[2022-05-30 17:08:49] Creating vocabulary...
[2022-05-30 17:08:49] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:08:49] Finished
[2022-05-30 17:08:49] Creating vocabulary...
[2022-05-30 17:08:49] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:08:49] Finished
/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/8
  9353  18708 308231 ./vocab/vocab.rk.yml
  9080  18162 286851 ./vocab/vocab.bk.yml
 18433  36870 595082 total
[2022-05-30 17:08:50] Creating vocabulary...
[2022-05-30 17:08:50] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:08:50] Finished
[2022-05-30 17:08:50] Creating vocabulary...
[2022-05-30 17:08:50] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:08:50] Finished
/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/9
  9360  18722 308253 ./vocab/vocab.rk.yml
  9078  18158 286094 ./vocab/vocab.bk.yml
 18438  36880 594347 total
[2022-05-30 17:08:50] Creating vocabulary...
[2022-05-30 17:08:50] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:08:50] Finished
[2022-05-30 17:08:50] Creating vocabulary...
[2022-05-30 17:08:50] [data] Creating vocabulary stdout from stdin
[2022-05-30 17:08:50] Finished
/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/10
  9368  18738 307986 ./vocab/vocab.rk.yml
  9075  18152 286001 ./vocab/vocab.bk.yml
 18443  36890 593987 total
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/data/word/rk-bk$
```

## Hyperparemeters of Seq2Seq or Script for Training

I changed --enc-depth and --dec-depth to "3",  --enc-cell-depth to "4", --dec-cell-base-depth to "4" and --workspace "5500" ...  
1st trying with following bash script:  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese dialects
## used Marian NMT Framework for seq2seq training
## Last updated: 30 May 2022

## Reference: https://marian-nmt.github.io/examples/mtm2017/complex/

model_folder="model.seq2seq.bkdw.1";
mkdir ${model_folder};
data_path="/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/1/";
src="bk"; tgt="dw";


marian \
  --type s2s \
  --train-sets ${data_path}/train.${src} ${data_path}/train.${tgt} \
  --max-length 200 \
  --valid-sets ${data_path}/dev.${src} ${data_path}/dev.${tgt} \
  --vocabs  ${data_path}/vocab/vocab.${src}.yml  ${data_path}/vocab/vocab.${tgt}.yml \
  --model ${model_folder}/model.npz \
  --workspace 5500 \
  --enc-depth 3 --enc-type alternating --enc-cell lstm --enc-cell-depth 4 \
  --dec-depth 3 --dec-cell lstm --dec-cell-base-depth 4 --dec-cell-high-depth 2 \
  --tied-embeddings --layer-normalization --skip \
  --mini-batch-fit \
  --valid-mini-batch 32 \
  --valid-metrics cross-entropy perplexity bleu\
  --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
  --dropout-rnn 0.3 --dropout-src 0.3 --exponential-smoothing \
  --early-stopping 10 \
  --log ${model_folder}/train.log --valid-log ${model_folder}/valid.log \
  --devices 0 1 --sync-sgd --seed 1111  \
  --dump-config > ${model_folder}/config.yml

time marian -c ${model_folder}/config.yml  2>&1 | tee ${model_folder}/s2s.${src}-${tgt}.log
```

When I run I got "out of memory" ERROR as follows:  

```
[2022-05-30 17:56:50] [data] Done reading 5,452 sentences
[2022-05-30 17:56:50] [data] Done shuffling 5,452 sentences to temp files
[2022-05-30 17:56:50] [training] Batches are processed as 1 process(es) x 2 devices/process
[2022-05-30 17:56:50] [memory] Reserving 729 MB, device gpu0
[2022-05-30 17:56:50] [memory] Reserving 729 MB, device gpu1
[2022-05-30 17:56:50] [memory] Reserving 729 MB, device gpu0
[2022-05-30 17:56:51] [memory] Reserving 729 MB, device gpu1
[2022-05-30 17:56:52] Parameter type float32, optimization type float32, casting types false
[2022-05-30 17:56:52] Allocating memory for general optimizer shards
[2022-05-30 17:56:52] [memory] Reserving 364 MB, device gpu0
[2022-05-30 17:56:52] [memory] Reserving 364 MB, device gpu1
[2022-05-30 17:56:52] Error: CUDA error 2 'out of memory' - /home/ye/tool/marian/src/tensors/gpu/device.cu:38: cudaMalloc(&data_, size)
[2022-05-30 17:56:52] Error: Aborted from virtual void marian::gpu::Device::reserve(size_t) in /home/ye/tool/marian/src/tensors/gpu/device.cu:38
Allocating memory for Adam-specific shards
[memory] Reserving 729 MB, device gpu0

[CALL STACK]
[0x55f07f1566fb]    marian::gpu::Device::  reserve  (unsigned long)    + 0x127b
[0x55f07f0cfcb3]    marian::Allocator::  Allocator  (marian::DeviceId,  unsigned long,  unsigned long,  unsigned long) + 0x243
[0x55f07f0ca5bf]    marian::OptimizerBase::  update  (IntrusivePtr<marian::TensorBase>,  IntrusivePtr<marian::TensorBase>,  unsigned long,  float) + 0x7ef
[0x55f07ee2a81e]                                                       + 0x92281e
[0x55f07ee5b5fc]    marian::ThreadPool::enqueue<std::function<float (unsigned long,unsigned long,unsigned long)> const&,unsigned long&,unsigned long&,unsigned long&>(std::function<float (unsigned long,unsigned long,unsigned long)> const&,unsigned long&,unsigned long&,unsigned long&)::{lambda()#1}::  operator()  () const + 0x5c
[0x55f07ee5c2d6]    std::_Function_handler<std::unique_ptr<std::__future_base::_Result_base,std::__future_base::_Result_base::_Deleter> (),std::__future_base::_Task_setter<std::unique_ptr<std::__future_base::_Result<float>,std::__future_base::_Result_base::_Deleter>,std::__future_base::_Task_state<marian::ThreadPool::enqueue<std::function<float (unsigned long,unsigned long,unsigned long)> const&,unsigned long&,unsigned long&,unsigned long&>(std::function<float (unsigned long,unsigned long,unsigned long)> const&,unsigned long&,unsigned long&,unsigned long&)::{lambda()#1},std::allocator<int>,float ()>::_M_run()::{lambda()#1},float>>::  _M_invoke  (std::_Any_data const&) + 0x36
[0x55f07e8b59bd]    std::__future_base::_State_baseV2::  _M_do_set  (std::function<std::unique_ptr<std::__future_base::_Result_base,std::__future_base::_Result_base::_Deleter> ()>*,  bool*) + 0x2d
[0x7fec02e6af68]                                                       + 0x99f68
[0x55f07ee4cf45]    std::_Function_handler<void (),marian::ThreadPool::enqueue<std::function<float (unsigned long,unsigned long,unsigned long)> const&,unsigned long&,unsigned long&,unsigned long&>(std::function<float (unsigned long,unsigned long,unsigned long)> const&,unsigned long&,unsigned long&,unsigned long&)::{lambda()#3}>::  _M_invoke  (std::_Any_data const&) + 0x115
[0x55f07e8bb7b5]    std::thread::_State_impl<std::thread::_Invoker<std::tuple<marian::ThreadPool::reserve(unsigned long)::{lambda()#1}>>>::  _M_run  () + 0x1a5
[0x7fec030d52c3]                                                       + 0xdc2c3
[0x7fec02e65b43]                                                       + 0x94b43
[0x7fec02ef7a00]                                                       + 0x126a00


real    1m21.506s
user    1m19.704s
sys     0m1.813s
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline$
```

And thus, I updated the training script as follows:  
(--workspace 4500)  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese dialects
## used Marian NMT Framework for seq2seq training
## Last updated: 30 May 2022

## Reference: https://marian-nmt.github.io/examples/mtm2017/complex/

model_folder="model.seq2seq.bkdw.1";
mkdir ${model_folder};
data_path="/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/1/";
src="bk"; tgt="dw";


marian \
  --type s2s \
  --train-sets ${data_path}/train.${src} ${data_path}/train.${tgt} \
  --max-length 200 \
  --valid-sets ${data_path}/dev.${src} ${data_path}/dev.${tgt} \
  --vocabs  ${data_path}/vocab/vocab.${src}.yml  ${data_path}/vocab/vocab.${tgt}.yml \
  --model ${model_folder}/model.npz \
  --workspace 4500 \
  --enc-depth 3 --enc-type alternating --enc-cell lstm --enc-cell-depth 4 \
  --dec-depth 3 --dec-cell lstm --dec-cell-base-depth 4 --dec-cell-high-depth 2 \
  --tied-embeddings --layer-normalization --skip \
  --mini-batch-fit \
  --valid-mini-batch 32 \
  --valid-metrics cross-entropy perplexity bleu\
  --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
  --dropout-rnn 0.3 --dropout-src 0.3 --exponential-smoothing \
  --early-stopping 10 \
  --log ${model_folder}/train.log --valid-log ${model_folder}/valid.log \
  --devices 0 1 --sync-sgd --seed 1111  \
  --dump-config > ${model_folder}/config.yml

time marian -c ${model_folder}/config.yml  2>&1 | tee ${model_folder}/s2s.${src}-${tgt}.log
```

GPU usage for seq2seq model for bk-my (1/ of 10-folds) is as follows:  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/nmt-exp/seq2seq-bkdw-1-running-GPU-usage.png" alt="GPU Usage Infor for Seq2Seq Training" width="800"/>  
</p>  
<div align="center">
  Fig. GPU usage of training seq2seq model for bk-my  
</div> 

<br />

1st time training ...  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline$ ./seq2seq.bkdw.1.sh
...
...
...
[2022-05-31 07:19:11] [data] Done reading 5,452 sentences
[2022-05-31 07:19:11] [data] Done shuffling 5,452 sentences to temp files
[2022-05-31 07:19:26] Seen 5,452 samples
[2022-05-31 07:19:26] Starting data epoch 3235 in logical epoch 3235
[2022-05-31 07:19:26] [data] Shuffling data
[2022-05-31 07:19:26] [data] Done reading 5,452 sentences
[2022-05-31 07:19:26] [data] Done shuffling 5,452 sentences to temp files
[2022-05-31 07:19:40] Seen 5,452 samples
[2022-05-31 07:19:40] Starting data epoch 3236 in logical epoch 3236
[2022-05-31 07:19:40] [data] Shuffling data
[2022-05-31 07:19:40] [data] Done reading 5,452 sentences
[2022-05-31 07:19:40] [data] Done shuffling 5,452 sentences to temp files
[2022-05-31 07:19:45] Ep. 3236 : Up. 55000 : Sen. 2,100 : Cost 0.06274325 * 1,123,966 @ 1,412 after 123,157,504 : Time 432.95s : 2596.07 words/s : gNorm 0.0841
[2022-05-31 07:19:45] Saving model weights and runtime parameters to model.seq2seq.bkdw.1/model.iter55000.npz
[2022-05-31 07:19:46] Saving model weights and runtime parameters to model.seq2seq.bkdw.1/model.npz
[2022-05-31 07:19:51] Saving Adam parameters
[2022-05-31 07:19:52] [training] Saving training checkpoint to model.seq2seq.bkdw.1/model.npz and model.seq2seq.bkdw.1/model.npz.optimizer.npz
[2022-05-31 07:20:09] [valid] Ep. 3236 : Up. 55000 : cross-entropy : 51.095 : stalled 10 times (last best: 40.3277)
[2022-05-31 07:20:10] [valid] Ep. 3236 : Up. 55000 : perplexity : 1384.58 : stalled 10 times (last best: 301.54)
[2022-05-31 07:20:10] Translating validation set...
[2022-05-31 07:20:10] Best translation 0 : နန် ဟှဲဖြစ်ဟှိ ပ္လေး နေဟှယ် ။
[2022-05-31 07:20:10] Best translation 1 : အဲဟှာ ကြောက်-က်စာ အီတ် ဟှီးမား ။
[2022-05-31 07:20:10] Best translation 2 : အယ်ပြီး နေ့ဒါန်ပပိုင်း တနေ့ မှ ကျွန်မ စကိတ်ပွဲ တစ် ခု သွား ခခဲ့ဟှယ် ။
[2022-05-31 07:20:10] Best translation 3 : ကျွန်တော် မမိုးလန်းတတိုင်း တစ် နာရီ ကစားဟှယ် ။
[2022-05-31 07:20:10] Best translation 4 : ဟှယ်လူဝဝဲ့ ဖုန်း ဆစ်ဆစ် ၊ သူးနနိနို့ဂဂို ငါ ပ္လန်သွားဟှယ်ဆဆို ပြော လလိုက် ။
[2022-05-31 07:20:10] Best translation 5 : ဝယ်ယား ဟှ က သူးနနိနို့ ဝဝို သိ နေရယ် ။
[2022-05-31 07:20:10] Best translation 10 : ကျွန်တော် ဟှယ်ဒဒူ့ဟှှိုလည်း ပြစ်တန် ခခဲ့ဟှ ။
[2022-05-31 07:20:10] Best translation 20 : ကားလေမှာ ဘီးလေ ရှိဟှယ် ။
[2022-05-31 07:20:10] Best translation 40 : အဲထက် ပပိုကောန်းဇာ မှေ့မှုပီ ။
[2022-05-31 07:20:10] Best translation 80 : နန့် ဟှှို ငါ ဝဝိုင်း သယ် ပေးမယ် ။
[2022-05-31 07:20:10] Best translation 160 : နန့် ဟှှို ငါ ဝဝိုင်း သယ် ပေးမယ် ။
[2022-05-31 07:20:10] Best translation 320 : နန် ဟှယ်သသူ့ ဟှှို ပလပ် ဇာနူး ။
[2022-05-31 07:20:10] Total translation time: 0.56958s
[2022-05-31 07:20:10] [valid] Ep. 3236 : Up. 55000 : bleu : 10.3312 : new best
[2022-05-31 07:20:10] Training finished
[2022-05-31 07:20:11] Saving model weights and runtime parameters to model.seq2seq.bkdw.1/model.npz
[2022-05-31 07:20:16] Saving Adam parameters
[2022-05-31 07:20:17] [training] Saving training checkpoint to model.seq2seq.bkdw.1/model.npz and model.seq2seq.bkdw.1/model.npz.optimizer.npz

real    801m25.131s
user    960m36.334s
sys     2m24.628s
```

Check the models ...  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.bkdw.1$ ls *.npz | sort -V
model.iter5000.npz
model.iter10000.npz
model.iter15000.npz
model.iter20000.npz
model.iter25000.npz
model.iter30000.npz
model.iter35000.npz
model.iter40000.npz
model.iter45000.npz
model.iter50000.npz
model.iter55000.npz
model.npz
model.npz.optimizer.npz
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.bkdw.1$
```

prepare script for testing ...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese dialects
## used Marian NMT Framework for training
## Last updated: 31 May 2022

data_path="/home/ye/exp/my-nmt/data/4nmt/dw-bk/";
src="bk"; tgt="dw";

for i in {5000..55000..5000}
do
    marian-decoder -m ./model.iter$i.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml --devices 0 1 --output hyp.iter$i.${tgt} < ${data_path}/test.${src};
    echo "Evaluation with hyp.iter$i.${tgt}, Transformer model:" >> eval-result.txt;
    perl /home/ye/tool/moses-scripts/scripts/generic/multi-bleu.perl ${data_path}/test.${tgt} < ./hyp.iter$i.${tgt} >> eval-result.txt;

done
```

testing and evaluation ...  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.bkdw.1$ time ./test-eval.sh
...
...
...
[2022-05-31 07:42:54] Best translation 636 : ကော်ဟှား မှာ ပြစ် ရှိဇာ သူးနနိနို့ သိ ဟှားဟှယ် ။
[2022-05-31 07:42:54] Best translation 637 : သူးနနိနို့ ဟှယ်သသူ့ ဝန်ထမ်း လေ နူး ။
[2022-05-31 07:42:54] Best translation 638 : ဟှယ်လူလေ ရေကူး နေကေ့နူး ။
[2022-05-31 07:42:54] Best translation 639 : သူ ဂါး ပြော နေဇာ ။
[2022-05-31 07:42:54] Best translation 640 : သူ အအဲ့ဇာဝဝို ဖယ်ရှား ခခဲ့ရယ် ။
[2022-05-31 07:42:54] Best translation 641 : ငါ့ သွပ် သူ အီ မှာ နေ ရဟှူ ဆင် ပြေ ဟှယ် ။
[2022-05-31 07:42:54] Best translation 642 : ငါ့ဟှှို ယယုံလူ လေ ဟှှို လလုံးဝ သစ္စာ ဖွတ်ဟှ ။
[2022-05-31 07:42:54] Best translation 643 : နန် လတ်ထပ် နနိုင်ဟှယ် ။
[2022-05-31 07:42:54] Best translation 644 : နန် အအဲ့မာ ဟှှို ခန်မှန်းကေ့ လယ် ။
[2022-05-31 07:42:54] Best translation 645 : ခေါ့ပေါ့က်မှာ တယော့က်ယော့က် ရှိ ဟှယ် ။
[2022-05-31 07:42:54] Best translation 646 : အယ်ဘဘဲ့ ။
[2022-05-31 07:42:54] Best translation 647 : နန် ဟှဲဇာ စိပျစ် နေဟှယ် ။
[2022-05-31 07:42:54] Best translation 648 : ကျွန်တော်ဝဝိဝို့ အအဲ့ဇာ ဝဝို နှှိုင်းယှဉ် မှာ မှုဝ ။
[2022-05-31 07:42:54] Best translation 649 : ခံဗျား ငါးဟှန်း နည်းနည်း ယူ ဦးမွန် ။
[2022-05-31 07:42:54] Best translation 650 : ခံဗျား ငါးဟှန်း နည်းနည်း ယူ ဦးမွန် ။
[2022-05-31 07:42:54] Best translation 651 : ခံဗျား မွီးနေ့ တွက် ခံဗျား ကြြိုက်ဇာ ခံဗျား ယူ ရဟှယ် ။
[2022-05-31 07:42:54] Best translation 652 : ကျွန်တော်ဟှားဒေ အဲမှာ ဟှှို နားလည် ကေ့ဟှ ။
[2022-05-31 07:42:54] Best translation 653 : ကျွန်တော် ခရီး ဂဂို စ ဟှှို မျှော်လင့် ဟှယ် ။
[2022-05-31 07:42:55] Best translation 654 : နန် ဟှဲဇာ မ ဝယ် ခခဲ့ဟှ ။
[2022-05-31 07:42:55] Best translation 655 : နန် ပြော ဟှှိှို့ ဂါး လေဟှှို ငါ ယယုံ ဟှ ။
[2022-05-31 07:42:55] Best translation 656 : နန် ပြော ဟှှိှို့ ဂါး လေဟှှို ငါ ယယုံ ဟှ ။
[2022-05-31 07:42:55] Best translation 657 : ဟှယ်ဒဒူ့ အန်းဂီ နူး ။
[2022-05-31 07:42:55] Best translation 658 : နန် သသူ့ဟှှို တောပန် ဟှှိှို့ မှုဝလား ။
[2022-05-31 07:42:55] Best translation 659 : နန့် သား လေ ဟှ ဟှယ်လူ လေ နူး ။
[2022-05-31 07:42:55] Best translation 660 : ဟှယ်လူလေ ဟှှို ထန်သေး ကေ့နူး ။
[2022-05-31 07:42:55] Best translation 661 : အဲဝယ်ဟှား နန့်ဟှှို နှိစစ် ဟှှိှို့လောမှုဝ ။
[2022-05-31 07:42:55] Best translation 662 : ဟှယ်လော့ ရုပ်ဆဆိုး ဟှယ် ။
[2022-05-31 07:42:55] Best translation 663 : နန် ငါ့ ဟှှို ပြော ပြ ပါလား ။
[2022-05-31 07:42:55] Best translation 664 : အဲဟှှို သွား ဟှှိှို့ ငါ တတိုက်တွန်း ဟှ ။
[2022-05-31 07:42:55] Best translation 665 : နန် အဲဟှှို သွား လလိုက်ဟှလား ။
[2022-05-31 07:42:55] Best translation 666 : သူးနနိနို့ ဟှယ်လော့ သွမ့်လတ် ဟှယ် ။
[2022-05-31 07:42:55] Best translation 667 : အယ်မာရှိဟှှို ပစ်ဆံအိဟှ ငါဇာ ။
[2022-05-31 07:42:55] Best translation 668 : အယ်မာရှိဟှှို ပစ်ဆံအိဟှ ငါဇာ ။
[2022-05-31 07:42:55] Best translation 669 : အဲဝယ်ဟှားဟှှို ဝီးချယ် လလိုက်လား ။
[2022-05-31 07:42:55] Total time: 8.74806s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    2m3.489s
user    3m22.412s
sys     0m26.770s
```

Results for bk-dw, word unit, seq2seq with above configuration are as follows:  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.bkdw.1$ cat eval-result.txt
Evaluation with hyp.iter5000.dw, Transformer model:
BLEU = 10.50, 37.3/12.1/6.6/4.8 (BP=0.958, ratio=0.959, hyp_len=3848, ref_len=4013)
Evaluation with hyp.iter10000.dw, Transformer model:
BLEU = 12.90, 39.2/13.8/8.2/6.6 (BP=0.986, ratio=0.986, hyp_len=3956, ref_len=4013)
Evaluation with hyp.iter15000.dw, Transformer model:
BLEU = 13.24, 39.2/14.4/8.5/6.7 (BP=0.988, ratio=0.988, hyp_len=3965, ref_len=4013)
Evaluation with hyp.iter20000.dw, Transformer model:
BLEU = 13.34, 39.9/14.6/8.6/6.6 (BP=0.989, ratio=0.989, hyp_len=3968, ref_len=4013)
Evaluation with hyp.iter25000.dw, Transformer model:
BLEU = 13.25, 39.3/14.4/8.5/6.5 (BP=0.997, ratio=0.997, hyp_len=3999, ref_len=4013)
Evaluation with hyp.iter30000.dw, Transformer model:
BLEU = 13.32, 39.7/14.5/8.5/6.7 (BP=0.990, ratio=0.990, hyp_len=3973, ref_len=4013)
Evaluation with hyp.iter35000.dw, Transformer model:
BLEU = 13.34, 39.6/14.6/8.5/6.7 (BP=0.992, ratio=0.992, hyp_len=3982, ref_len=4013)
Evaluation with hyp.iter40000.dw, Transformer model:
BLEU = 13.14, 39.6/14.4/8.3/6.5 (BP=0.993, ratio=0.993, hyp_len=3985, ref_len=4013)
Evaluation with hyp.iter45000.dw, Transformer model:
BLEU = 13.84, 40.1/15.1/9.0/7.1 (BP=0.986, ratio=0.986, hyp_len=3958, ref_len=4013)
Evaluation with hyp.iter50000.dw, Transformer model:
BLEU = 13.64, 40.0/15.0/8.8/7.0 (BP=0.985, ratio=0.985, hyp_len=3954, ref_len=4013)
Evaluation with hyp.iter55000.dw, Transformer model:
BLEU = 13.48, 40.2/15.0/8.7/6.8 (BP=0.984, ratio=0.984, hyp_len=3949, ref_len=4013)
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.bkdw.1$
```

**Best score is 13.84.**  

## dw-bk, word unit, seq2seq

bash script for dw-bk, word unit, seq2seq ...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese and Ethnic Languages
## used Marian NMT Framework for seq2seq training
## Last updated: 31 May 2022

## Reference: https://marian-nmt.github.io/examples/mtm2017/complex/

model_folder="model.seq2seq.dwbk.1";
mkdir ${model_folder};
data_path="/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/1/";
src="dw"; tgt="bk";


marian \
  --type s2s \
  --train-sets ${data_path}/train.${src} ${data_path}/train.${tgt} \
  --max-length 200 \
  --valid-sets ${data_path}/dev.${src} ${data_path}/dev.${tgt} \
  --vocabs  ${data_path}/vocab/vocab.${src}.yml  ${data_path}/vocab/vocab.${tgt}.yml \
  --model ${model_folder}/model.npz \
  --workspace 4500 \
  --enc-depth 3 --enc-type alternating --enc-cell lstm --enc-cell-depth 4 \
  --dec-depth 3 --dec-cell lstm --dec-cell-base-depth 4 --dec-cell-high-depth 2 \
  --tied-embeddings --layer-normalization --skip \
  --mini-batch-fit \
  --valid-mini-batch 32 \
  --valid-metrics cross-entropy perplexity bleu\
  --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
  --dropout-rnn 0.3 --dropout-src 0.3 --exponential-smoothing \
  --early-stopping 10 \
  --log ${model_folder}/train.log --valid-log ${model_folder}/valid.log \
  --devices 0 1 --sync-sgd --seed 1111  \
  --dump-config > ${model_folder}/config.yml

time marian -c ${model_folder}/config.yml  2>&1 | tee ${model_folder}/s2s.${src}-${tgt}.log
```

training ...  
from 08:05 ...  
```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline$ ./seq2seq.dwbk.1.sh
...
...
...
[2022-05-31 21:28:02] [data] Done reading 5,452 sentences
[2022-05-31 21:28:02] [data] Done shuffling 5,452 sentences to temp files
[2022-05-31 21:28:17] Seen 5,452 samples
[2022-05-31 21:28:17] Starting data epoch 3235 in logical epoch 3235
[2022-05-31 21:28:17] [data] Shuffling data
[2022-05-31 21:28:17] [data] Done reading 5,452 sentences
[2022-05-31 21:28:17] [data] Done shuffling 5,452 sentences to temp files
[2022-05-31 21:28:32] Seen 5,452 samples
[2022-05-31 21:28:32] Starting data epoch 3236 in logical epoch 3236
[2022-05-31 21:28:32] [data] Shuffling data
[2022-05-31 21:28:32] [data] Done reading 5,452 sentences
[2022-05-31 21:28:32] [data] Done shuffling 5,452 sentences to temp files
[2022-05-31 21:28:36] Ep. 3236 : Up. 55000 : Sen. 1,654 : Cost 0.04235865 * 1,173,302 @ 2,820 after 129,168,120 : Time 435.25s : 2695.68 words/s : gNorm 0.0676
[2022-05-31 21:28:36] Saving model weights and runtime parameters to model.seq2seq.dwbk.1/model.iter55000.npz
[2022-05-31 21:28:37] Saving model weights and runtime parameters to model.seq2seq.dwbk.1/model.npz
[2022-05-31 21:28:42] Saving Adam parameters
[2022-05-31 21:28:43] [training] Saving training checkpoint to model.seq2seq.dwbk.1/model.npz and model.seq2seq.dwbk.1/model.npz.optimizer.npz
[2022-05-31 21:29:00] [valid] Ep. 3236 : Up. 55000 : cross-entropy : 57.3937 : stalled 10 times (last best: 42.4461)
[2022-05-31 21:29:01] [valid] Ep. 3236 : Up. 55000 : perplexity : 2272.75 : stalled 10 times (last best: 303.65)
[2022-05-31 21:29:01] Translating validation set...
[2022-05-31 21:29:01] Best translation 0 : ခင်ဗျား မ ငို ရလား ။
[2022-05-31 21:29:01] Best translation 1 : ငါ လက်သည်း သွားပြုပြင် ချင်ရိ ။
[2022-05-31 21:29:01] Best translation 2 : စု နေတဲ့ လူ ဒေ ကို နင် မြင် ရယ် ။
[2022-05-31 21:29:01] Best translation 3 : ကျေးဇူးပြု၍ ကျွန်တော့်ရဲ့ မွေးနေ့ပွဲ ကို လာ ပါလား ။
[2022-05-31 21:29:01] Best translation 4 : ဘသူပဲ့ တယ်လီဖုန်း ဆက်ဆက် ၊ သူ့လို့ဝို ငါ အပြင် သွား ဝယ်လိ ပြော လိုက်န ။
[2022-05-31 21:29:01] Best translation 5 : အဲ့အမ လေ အဲ့ဇာ ကို သိ ရယ် ။
[2022-05-31 21:29:01] Best translation 10 : သူတို့ ဘာ ကို စိတ်အနှောင့်အယှက်ဖြစ် သွားလဲ ။
[2022-05-31 21:29:01] Best translation 20 : လူတွေ ချမ်းသာ နေကြတောင် ဒါထက် ချမ်းသာ ချင်သေးတယ် ။
[2022-05-31 21:29:01] Best translation 40 : ဒါတပတ် ကုန်ခါနီးမှာ ရာသီဥတုသာယာပ ပြီး နေပူ မယ်တဲ့ ။
[2022-05-31 21:29:01] Best translation 80 : ဒယ်ကောင်မငယ် ဝို အဲဒီဝို သွားခိုင်း ခဲ့ရယ်လား ။
[2022-05-31 21:29:01] Best translation 160 : သူ ခရီး ရှည် ထွက် နေကျလေ ။
[2022-05-31 21:29:01] Best translation 320 : နင် ဖယ်သူ့ ဝို မယုံ ဖြစ်ခဲ့လဲ ။
[2022-05-31 21:29:01] Total translation time: 0.53674s
[2022-05-31 21:29:01] [valid] Ep. 3236 : Up. 55000 : bleu : 9.76287 : stalled 7 times (last best: 10.1296)
[2022-05-31 21:29:01] Training finished
[2022-05-31 21:29:02] Saving model weights and runtime parameters to model.seq2seq.dwbk.1/model.npz
[2022-05-31 21:29:07] Saving Adam parameters
[2022-05-31 21:29:08] [training] Saving training checkpoint to model.seq2seq.dwbk.1/model.npz and model.seq2seq.dwbk.1/model.npz.optimizer.npz

real    804m18.561s
user    963m49.461s
sys     2m26.816s
```
end the training around 21:30 ...  

check the models ...  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.dwbk.1$ ls *.npz | sort -V
model.iter5000.npz
model.iter10000.npz
model.iter15000.npz
model.iter20000.npz
model.iter25000.npz
model.iter30000.npz
model.iter35000.npz
model.iter40000.npz
model.iter45000.npz
model.iter50000.npz
model.iter55000.npz
model.npz
model.npz.optimizer.npz
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.dwbk.1$
```

bash script for dw-bk, word unit, seq2seq ...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese dialects
## used Marian NMT Framework for training
## Last updated: 31 May 2022

data_path="/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/1/";
src="dw"; tgt="bk";

for i in {5000..55000..5000}
do
    marian-decoder -m ./model.iter$i.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml --devices 0 1 --output hyp.iter$i.${tgt} < ${data_path}/test.${src};
    echo "Evaluation with hyp.iter$i.${tgt}, Transformer model:" >> eval-result.txt;
    perl /home/ye/tool/moses-scripts/scripts/generic/multi-bleu.perl ${data_path}/test.${tgt} < ./hyp.iter$i.${tgt} >> eval-result.txt;

done
```

testing and evaluation for dw-bk, word, seq2seq ...  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.dwbk.1$ time ./test-eval.sh
...
...
...
[2022-05-31 22:11:54] Best translation 636 : တကယ် ကောင်း ဝယ်ပပဲ့ ။
[2022-05-31 22:11:54] Best translation 637 : သသူ့အတွက် ကျွန်တော်လလိလို့ က မေး မှာ မ ဟုတ် ဝ ။
[2022-05-31 22:11:54] Best translation 638 : ဖယ်သူလေ ဝန်းသာ ရိလဲ ။
[2022-05-31 22:11:54] Best translation 639 : မင်း စကား ပြော နေရယ် ။
[2022-05-31 22:11:54] Best translation 640 : သူ ဒယ်စာဝဝို ဖယ်ပစ် ခခဲ့ဟယ် ။
[2022-05-31 22:11:54] Best translation 641 : ဒယ်ကောင်မငယ် ကကို ငါ မေး ရအအုံးမယ် ။
[2022-05-31 22:11:54] Best translation 642 : ငါ့ ဝဝို ယယုံ တတဲ့ သူ ဒေ ဂဂို ဘယ်ခါမှ သစ္စာ မ ဖောက် ရ ။
[2022-05-31 22:11:54] Best translation 643 : နင် ဘောလ်ပင် မ ကောက် ရလား ။
[2022-05-31 22:11:54] Best translation 644 : နင် ဒယ်စာ ဝဝို ကြား ဟယ် ။
[2022-05-31 22:11:54] Best translation 645 : ရေဒီယယို ဖွင့် ရင် စိတ်ဆဆိုး ဝဝိဝို့လား ။
[2022-05-31 22:11:54] Best translation 646 : မဟုတ်ဝ ။
[2022-05-31 22:11:54] Best translation 647 : နင် ဘာတွေ အသံထွက် ခခဲ့ရိ ။
[2022-05-31 22:11:54] Best translation 648 : ငါလလိလို့ ဒယ်စာ ဝဝို စီစဉ် ခခဲ့ကြဇာ ။
[2022-05-31 22:11:54] Best translation 649 : ခင်ဗျား ဘာ သောက် နေရယ် ။
[2022-05-31 22:11:54] Best translation 650 : ခင်ဗျား ဘာ သောက် နေရယ် ။
[2022-05-31 22:11:54] Best translation 651 : နင် မှန် ရယ်ရိ ငါ ထင် ရ ယ် ။
[2022-05-31 22:11:54] Best translation 652 : ကျွန်တော်ဝဝိဝို့ အအဲ့ဒါဝဝို ပထမတော့ မ အောင်မြင် ခခဲ့ရလေ ။
[2022-05-31 22:11:54] Best translation 653 : ကျွန်တော် ခရီး ကကို စလုပ် ဖဖိဖို့ မျှော်လင့် တယ် ။
[2022-05-31 22:11:54] Best translation 654 : နင် အရက် သောက် လာခခဲ့ဟယ် ။
[2022-05-31 22:11:54] Best translation 655 : ငါ နင်နနဲ့ စကားပြောတာ အား ဝမ်းသာရရ် ။
[2022-05-31 22:11:54] Best translation 656 : မင်းဘယ်သသူ့ကကို အားကကိုး မင်း တစ်နေ့ကျ ဒုက္ခ ရောက် မယ် ။
[2022-05-31 22:11:54] Best translation 657 : အယ့်ဒါ ဘယ်သသူ့ ပပိုက်ဆံ ရိ ။
[2022-05-31 22:11:54] Best translation 658 : နင် သသူ့ ကကို သံယောဇဉ် ရှိ သောရိမယ် ။
[2022-05-31 22:11:54] Best translation 659 : နင့် ဆွေမျျိုး တတိတို့ က ဖယ်သူတွေ ။
[2022-05-31 22:11:54] Best translation 660 : ဖယ်သူလေ အထင်သေး ရိလဲ ။
[2022-05-31 22:11:55] Best translation 661 : သူ ဒယ်အကြောင်း ကကို သိ ဟုတ်ဝ ။
[2022-05-31 22:11:55] Best translation 662 : သူ ဖျားပပဲ့ဖျား နေမလား ။
[2022-05-31 22:11:55] Best translation 663 : ခင်ဗျား ကျွန်တော့် ကကို ရရိုက် ဝဝိဝို့လား ။
[2022-05-31 22:11:55] Best translation 664 : ဘယ်သူဟ မင့် အကြောင်း ဝဝို တတိုင်တတိုင် ငါ မ ယယုံ ဝ ။
[2022-05-31 22:11:55] Best translation 665 : သူ ဆေးလိပ် သောက် ဇာ မ ကြြိုက် ရ ။
[2022-05-31 22:11:55] Best translation 666 : မင်းက ဘဇာလောက်် သတ္တိရှိ လဲ ။
[2022-05-31 22:11:55] Best translation 667 : ကျွန်နော် သူ ဝက် အကြာကြီး စကား ပြော ခခဲ့ဇာ ။
[2022-05-31 22:11:55] Best translation 668 : အဲဒါ ကကို ရှင်းပြ ဖဖိဖို့ ငါ ဆန္ဒ ရှိ တယ် ။
[2022-05-31 22:11:55] Best translation 669 : သူ အိမ်ထောင် ထိန်းသိမ်း နနိုင်မယ်ပပဲ့လား ။
[2022-05-31 22:11:55] Total time: 8.71540s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    2m3.005s
user    3m21.565s
sys     0m26.594s
```

results are as follows:  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.dwbk.1$ cat eval-result.txt
Evaluation with hyp.iter5000.bk, Transformer model:
BLEU = 6.81, 32.1/7.6/3.7/2.7 (BP=0.968, ratio=0.968, hyp_len=4131, ref_len=4267)
Evaluation with hyp.iter10000.bk, Transformer model:
BLEU = 10.61, 37.2/11.8/6.4/4.5 (BP=1.000, ratio=1.001, hyp_len=4272, ref_len=4267)
Evaluation with hyp.iter15000.bk, Transformer model:
BLEU = 11.27, 37.4/12.4/6.9/5.0 (BP=1.000, ratio=1.002, hyp_len=4277, ref_len=4267)
Evaluation with hyp.iter20000.bk, Transformer model:
BLEU = 11.33, 37.6/12.5/7.0/5.0 (BP=1.000, ratio=1.000, hyp_len=4266, ref_len=4267)
Evaluation with hyp.iter25000.bk, Transformer model:
BLEU = 11.23, 38.0/12.6/6.9/4.8 (BP=1.000, ratio=1.001, hyp_len=4272, ref_len=4267)
Evaluation with hyp.iter30000.bk, Transformer model:
BLEU = 11.19, 37.5/12.5/6.9/4.9 (BP=1.000, ratio=1.005, hyp_len=4288, ref_len=4267)
Evaluation with hyp.iter35000.bk, Transformer model:
BLEU = 11.10, 37.6/12.4/6.8/4.8 (BP=1.000, ratio=1.000, hyp_len=4267, ref_len=4267)
Evaluation with hyp.iter40000.bk, Transformer model:
BLEU = 11.08, 37.5/12.6/6.7/4.7 (BP=1.000, ratio=1.004, hyp_len=4282, ref_len=4267)
Evaluation with hyp.iter45000.bk, Transformer model:
BLEU = 11.12, 37.8/12.5/6.8/4.8 (BP=0.999, ratio=0.999, hyp_len=4264, ref_len=4267)
Evaluation with hyp.iter50000.bk, Transformer model:
BLEU = 11.04, 37.7/12.5/6.7/4.7 (BP=1.000, ratio=1.007, hyp_len=4295, ref_len=4267)
Evaluation with hyp.iter55000.bk, Transformer model:
BLEU = 11.17, 37.4/12.5/6.9/4.8 (BP=1.000, ratio=1.011, hyp_len=4314, ref_len=4267)
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.dwbk.1$
```

**Best BLEU Score for dw-bk, word, seq2seq archi is 11.33**  

## rk-bk, word unit, seq2seq

script for training ...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese and Ethnic Languages
## used Marian NMT Framework for seq2seq training
## Last updated: 30 May 2022

## Reference: https://marian-nmt.github.io/examples/mtm2017/complex/

model_folder="model.seq2seq.rkbk.1";
mkdir ${model_folder};
data_path="/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/1/";
src="rk"; tgt="bk";


marian \
  --type s2s \
  --train-sets ${data_path}/train.${src} ${data_path}/train.${tgt} \
  --max-length 200 \
  --valid-sets ${data_path}/dev.${src} ${data_path}/dev.${tgt} \
  --vocabs  ${data_path}/vocab/vocab.${src}.yml  ${data_path}/vocab/vocab.${tgt}.yml \
  --model ${model_folder}/model.npz \
  --workspace 4500 \
  --enc-depth 3 --enc-type alternating --enc-cell lstm --enc-cell-depth 4 \
  --dec-depth 3 --dec-cell lstm --dec-cell-base-depth 4 --dec-cell-high-depth 2 \
  --tied-embeddings --layer-normalization --skip \
  --mini-batch-fit \
  --valid-mini-batch 32 \
  --valid-metrics cross-entropy perplexity bleu\
  --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
  --dropout-rnn 0.3 --dropout-src 0.3 --exponential-smoothing \
  --early-stopping 10 \
  --log ${model_folder}/train.log --valid-log ${model_folder}/valid.log \
  --devices 0 1 --sync-sgd --seed 1111  \
  --dump-config > ${model_folder}/config.yml

time marian -c ${model_folder}/config.yml  2>&1 | tee ${model_folder}/s2s.${src}-${tgt}.log
```

training ...    

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline$ ./seq2seq.rkbk.1.sh
...
...
...
[2022-06-01 15:31:23] [data] Done shuffling 8,850 sentences to temp files
[2022-06-01 15:31:52] Seen 8,850 samples
[2022-06-01 15:31:52] Starting data epoch 1925 in logical epoch 1925
[2022-06-01 15:31:52] [data] Shuffling data
[2022-06-01 15:31:52] [data] Done reading 8,850 sentences
[2022-06-01 15:31:52] [data] Done shuffling 8,850 sentences to temp files
[2022-06-01 15:32:20] Seen 8,850 samples
[2022-06-01 15:32:20] Starting data epoch 1926 in logical epoch 1926
[2022-06-01 15:32:20] [data] Shuffling data
[2022-06-01 15:32:20] [data] Done reading 8,850 sentences
[2022-06-01 15:32:20] [data] Done shuffling 8,850 sentences to temp files
[2022-06-01 15:32:42] Ep. 1926 : Up. 60000 : Sen. 7,064 : Cost 0.04219449 * 1,062,165 @ 1,827 after 129,095,679 : Time 445.63s : 2383.50 words/s : gNorm 0.0841
[2022-06-01 15:32:42] Saving model weights and runtime parameters to model.seq2seq.rkbk.1/model.iter60000.npz
[2022-06-01 15:32:43] Saving model weights and runtime parameters to model.seq2seq.rkbk.1/model.npz
[2022-06-01 15:32:48] Saving Adam parameters
[2022-06-01 15:32:49] [training] Saving training checkpoint to model.seq2seq.rkbk.1/model.npz and model.seq2seq.rkbk.1/model.npz.optimizer.npz
[2022-06-01 15:33:07] [valid] Ep. 1926 : Up. 60000 : cross-entropy : 47.9898 : stalled 10 times (last best: 35.8691)
[2022-06-01 15:33:07] [valid] Ep. 1926 : Up. 60000 : perplexity : 537.841 : stalled 10 times (last best: 109.895)
[2022-06-01 15:33:07] Translating validation set...
[2022-06-01 15:33:08] Best translation 0 : ဒယ်ကောင်မ နင့်ဝို့ နှောင့်ယှက် လိမ့်မယ်မော် ။
[2022-06-01 15:33:08] Best translation 1 : မင်း နာမယ် ဘယ်မျိုး ပေါင်း ရယ် ။
[2022-06-01 15:33:08] Best translation 2 : ကျွန်တော် လိုင်းချိတ် ပေးမယ် ။
[2022-06-01 15:33:08] Best translation 3 : သူရဲ့ သား မိုက် ကို သူ က စွန့်လွှတ် လိုက်ရယ် ။
[2022-06-01 15:33:08] Best translation 4 : ခုန် နေတဲ့ ခွေး ဒွေ ။
[2022-06-01 15:33:08] Best translation 5 : နင် ဘာ မေး ဝို့ ။
[2022-06-01 15:33:08] Best translation 10 : သူက ရာရာစစ နေရရယ် ။
[2022-06-01 15:33:08] Best translation 20 :
[2022-06-01 15:33:08] Best translation 40 : အယ့်ဒါ ဘယ်သူ့ စက်ဘီး ရိ ။
[2022-06-01 15:33:08] Best translation 80 : ဒါ စာအုပ် ဝ အပိုင်း လေး ပိုင်း ပါရယ် ။
[2022-06-01 15:33:08] Best translation 160 : မင့် ဘီယာ သောက် ချင် ဆို သောက် ။
[2022-06-01 15:33:08] Best translation 320 : သူ က သနား တော့ ဟုတ် ဝ ။
[2022-06-01 15:33:08] Best translation 640 : ငါ လိမ္မော်ဖျော်ရယ် သောက် ချင် ရယ် ။
[2022-06-01 15:33:08] Total translation time: 0.95058s
[2022-06-01 15:33:08] [valid] Ep. 1926 : Up. 60000 : bleu : 18.1531 : stalled 1 times (last best: 18.3091)
[2022-06-01 15:33:08] Training finished
[2022-06-01 15:33:09] Saving model weights and runtime parameters to model.seq2seq.rkbk.1/model.npz
[2022-06-01 15:33:14] Saving Adam parameters
[2022-06-01 15:33:16] [training] Saving training checkpoint to model.seq2seq.rkbk.1/model.npz and model.seq2seq.rkbk.1/model.npz.optimizer.npz

real    376m51.006s
user    451m35.261s
sys     1m5.551s
```

Actually, I have to run two times. Stopped during training and thus above time information is for the 2nd time training.  

script for testing-evaluation ...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese dialects
## used Marian NMT Framework for training
## Last updated: 31 May 2022

data_path="/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/1/";
src="rk"; tgt="bk";

for i in {5000..60000..5000}
do
    marian-decoder -m ./model.iter$i.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml --devices 0 1 --output hyp.iter$i.${tgt} < ${data_path}/test.${src};
    echo "Evaluation with hyp.iter$i.${tgt}, Transformer model:" >> eval-result.txt;
    perl /home/ye/tool/moses-scripts/scripts/generic/multi-bleu.perl ${data_path}/test.${tgt} < ./hyp.iter$i.${tgt} >> eval-result.txt;

done
```

testing ...  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.rkbk.1$ time ./test-eval.sh
...
...
...
[2022-06-01 19:31:12] Best translation 1039 : နင် က ဘာတွေ သင်ပေး ခခဲ့ရိ ။
[2022-06-01 19:31:12] Best translation 1040 : သူ ခင်ဗျား ကကို သံသယ ဖြစ်မယ်နား ။
[2022-06-01 19:31:12] Best translation 1041 : သူတတိတို့ ဘဇာလောက် စိတ်ရှည် လဲ ။
[2022-06-01 19:31:13] Best translation 1042 : သူဝဝိဝို့ အစားစာ နနဲ့ အဝတ်ဒေ လလိုအပ်တတဲ့အခါ မီးခွက်စောင့် ဘီလူး ကကိုပဲ ခခိုင်း ရယ် ။
[2022-06-01 19:31:13] Best translation 1043 : ဝေဖန် တတဲ့ လူ ဒေ ဝဝို ငါ မ ကြြိုက် ရ ။
[2022-06-01 19:31:13] Best translation 1044 : သူဝဝိဝို့ရရဲ့ ကူညီမှု အတွက် ကျေးဇူးတင်ကြောင်း သူ က ပြော ရယ် ။
[2022-06-01 19:31:13] Best translation 1045 : ဟိတ် နင် ဘာ တင်ပြ အုန်း ။
[2022-06-01 19:31:13] Best translation 1046 : နင်ဝဝိဝို့ အအဲ့ဇာဝဝို သိမ်းဟား ဝဝိဝို့လား ။
[2022-06-01 19:31:13] Best translation 1047 : မင်း ပပိပို့စကဒ် တေ မ စုဆောင်း ရလား ။
[2022-06-01 19:31:13] Best translation 1048 : ဒါကကို မင်းကြြိုက်ချင်ကြြိုက် မကြြိုက်ချင်နေ ။
[2022-06-01 19:31:13] Best translation 1049 : ဒယ်ကောင်မငယ် စောရီး သွားပီး နေမရ် ။
[2022-06-01 19:31:13] Best translation 1050 : သူ စာ ကြြိုးစား ခခဲ့ရာဆဆိုတော့ စာမေးပွဲ အောင် လေ့မယ် ။
[2022-06-01 19:31:13] Best translation 1051 : သူ နင့်ဆီကကို သော ရယ်လား ။
[2022-06-01 19:31:13] Best translation 1052 : ရရုံး ဝ ဆင်း ဒေါ့ သူ ဈေး ဝဝို သွား ဝယ် ။
[2022-06-01 19:31:13] Best translation 1053 : အဲဒါ ကနေ မင့် ကြြိုက် တတဲ့ဟာ ရ နနိုင်ရယ် ။
[2022-06-01 19:31:13] Best translation 1054 : ဒီ မိန်းမ က ဖယ်သူ ဖြစ်နနိုင်လဲ ။
[2022-06-01 19:31:13] Best translation 1055 : နင် ဒယ်ဇာ ဘယ်သသူ့ ဝဝို ပေးသင့် ရယ် ။
[2022-06-01 19:31:13] Best translation 1056 : ဒါဇာ မျက်နှာကျက် လေ ။
[2022-06-01 19:31:13] Best translation 1057 : နင် ဖယ်သသူ့ ကကို ကူညီ ဝဝိဝို့လဲ ။
[2022-06-01 19:31:13] Best translation 1058 : ကျွန်တော် သူငယ်ချင်း တွေ ဒါကကို ရောက် လာလား ။
[2022-06-01 19:31:13] Best translation 1059 : ကျွန်တော်လလိလို့က ခင်ဗျား ကကို လက်ခံ ရမယ်လား ။
[2022-06-01 19:31:13] Best translation 1060 : ကျွန်တော်ဝဝိဝို့ ထပ် မ ကြြိုးစား တော့ဝီလား ။
[2022-06-01 19:31:13] Best translation 1061 : ဘယ်လောက် နာရီ ရှိပြီ ။
[2022-06-01 19:31:13] Best translation 1062 : ကျွန်တော်ဝဝိဝို့ လေးစား တတဲ့ ဆရာ က လူတတိုင်း အပေါ် နားလည် တတ်ရယ် ။
[2022-06-01 19:31:13] Best translation 1063 : တတိတို့ သူ ကကို အားပေး စစိစို့ ။
[2022-06-01 19:31:13] Best translation 1064 : နင် ဒယ်ကောင်မငယ် နနဲ့စကားများ ခခဲ့ရယ်လား ။
[2022-06-01 19:31:13] Best translation 1065 : ငါ တံခါး ပိတ် ဇာ မင်း စိတ်ညစ် နေရယ်လား ။
[2022-06-01 19:31:13] Best translation 1066 : နောက်ဆဆုံးတော့ မမိုးလင်းတစ်ခုမှာ မယ်မယ်ဟာ ဗဗိုက်နာလာရယ်ဒါနနဲ့ ဒယ်ကောင်မငယ် နနဲ့ဘဘဆေးရရုံကကိုသောကြရယ်၊ အဲအချိန်မှာ ကျွန်တော်က ကျောင်းသောနေပြီ ။
[2022-06-01 19:31:13] Best translation 1067 : ကျေးဇူးပြုပြီး အသံမြှင့် ပေးပါ ။
[2022-06-01 19:31:13] Best translation 1068 : သော စစုံစမ်း ။
[2022-06-01 19:31:13] Best translation 1069 : နင် ဘာ ဝယ် ဝဝိဝို့ ။
[2022-06-01 19:31:13] Best translation 1070 : ကျေးဇူးပြုပြီး ပြန် လာ ရမှာ ဘယ်လလိုမှ စနောင့်စနင်း မ ဖြစ် ပါနှင့် ။
[2022-06-01 19:31:13] Best translation 1071 : အအဲ့ဇာက ကျွန်တော့် အတွက် လွယ်လွယ်ငယ်ပဲ ။
[2022-06-01 19:31:13] Total time: 14.23964s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    3m43.385s
user    5m45.709s
sys     0m34.881s
```

Results are as follows:  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.rkbk.1$ cat eval-result.txt
Evaluation with hyp.iter5000.bk, Transformer model:
BLEU = 3.38, 32.7/5.2/1.6/0.8 (BP=0.872, ratio=0.880, hyp_len=6119, ref_len=6956)
Evaluation with hyp.iter10000.bk, Transformer model:
BLEU = 14.22, 38.7/14.5/9.3/7.8 (BP=1.000, ratio=1.004, hyp_len=6983, ref_len=6956)
Evaluation with hyp.iter15000.bk, Transformer model:
BLEU = 15.71, 40.1/16.0/10.6/9.0 (BP=0.998, ratio=0.998, hyp_len=6944, ref_len=6956)
Evaluation with hyp.iter20000.bk, Transformer model:
BLEU = 16.57, 40.5/16.9/11.5/9.6 (BP=0.999, ratio=0.999, hyp_len=6948, ref_len=6956)
Evaluation with hyp.iter25000.bk, Transformer model:
BLEU = 16.57, 40.6/17.0/11.5/9.5 (BP=0.999, ratio=0.999, hyp_len=6947, ref_len=6956)
Evaluation with hyp.iter30000.bk, Transformer model:
BLEU = 17.13, 41.0/17.5/12.0/10.0 (BP=1.000, ratio=1.006, hyp_len=6999, ref_len=6956)
Evaluation with hyp.iter35000.bk, Transformer model:
BLEU = 17.48, 41.4/17.9/12.3/10.2 (BP=1.000, ratio=1.006, hyp_len=7001, ref_len=6956)
Evaluation with hyp.iter40000.bk, Transformer model:
BLEU = 17.55, 41.3/17.9/12.4/10.3 (BP=1.000, ratio=1.004, hyp_len=6985, ref_len=6956)
Evaluation with hyp.iter45000.bk, Transformer model:
BLEU = 17.39, 41.3/18.0/12.3/10.1 (BP=1.000, ratio=1.011, hyp_len=7033, ref_len=6956)
Evaluation with hyp.iter50000.bk, Transformer model:
BLEU = 17.62, 41.4/18.1/12.5/10.3 (BP=1.000, ratio=1.011, hyp_len=7032, ref_len=6956)
Evaluation with hyp.iter55000.bk, Transformer model:
BLEU = 17.98, 42.0/18.6/12.8/10.5 (BP=1.000, ratio=1.005, hyp_len=6994, ref_len=6956)
Evaluation with hyp.iter60000.bk, Transformer model:
BLEU = 18.61, 42.4/19.2/13.3/11.1 (BP=1.000, ratio=1.004, hyp_len=6987, ref_len=6956)
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.rkbk.1$
```

**Best BLEU for rkbk, word unit, Seq2Seq is 18.61.**  

## bk-rk, word unit, Seq2Seq

script ...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese and Ethnic Languages
## used Marian NMT Framework for seq2seq training
## Last updated: 30 May 2022

## Reference: https://marian-nmt.github.io/examples/mtm2017/complex/

model_folder="model.seq2seq.bkrk.1";
mkdir ${model_folder};
data_path="/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/1/";
src="bk"; tgt="rk";


marian \
  --type s2s \
  --train-sets ${data_path}/train.${src} ${data_path}/train.${tgt} \
  --max-length 200 \
  --valid-sets ${data_path}/dev.${src} ${data_path}/dev.${tgt} \
  --vocabs  ${data_path}/vocab/vocab.${src}.yml  ${data_path}/vocab/vocab.${tgt}.yml \
  --model ${model_folder}/model.npz \
  --workspace 4500 \
  --enc-depth 3 --enc-type alternating --enc-cell lstm --enc-cell-depth 4 \
  --dec-depth 3 --dec-cell lstm --dec-cell-base-depth 4 --dec-cell-high-depth 2 \
  --tied-embeddings --layer-normalization --skip \
  --mini-batch-fit \
  --valid-mini-batch 32 \
  --valid-metrics cross-entropy perplexity bleu\
  --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
  --dropout-rnn 0.3 --dropout-src 0.3 --exponential-smoothing \
  --early-stopping 10 \
  --log ${model_folder}/train.log --valid-log ${model_folder}/valid.log \
  --devices 0 1 --sync-sgd --seed 1111  \
  --dump-config > ${model_folder}/config.yml

time marian -c ${model_folder}/config.yml  2>&1 | tee ${model_folder}/s2s.${src}-${tgt}.log
```

training ...  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline$ vi ./seq2seq.bkrk.1.sh
...
...
...
[2022-06-02 09:39:24] [data] Done shuffling 8,850 sentences to temp files
[2022-06-02 09:39:48] Seen 8,850 samples
[2022-06-02 09:39:48] Starting data epoch 1936 in logical epoch 1936
[2022-06-02 09:39:48] [data] Shuffling data
[2022-06-02 09:39:48] [data] Done reading 8,850 sentences
[2022-06-02 09:39:48] [data] Done shuffling 8,850 sentences to temp files
[2022-06-02 09:40:13] Seen 8,850 samples
[2022-06-02 09:40:13] Starting data epoch 1937 in logical epoch 1937
[2022-06-02 09:40:13] [data] Shuffling data
[2022-06-02 09:40:13] [data] Done reading 8,850 sentences
[2022-06-02 09:40:13] [data] Done shuffling 8,850 sentences to temp files
[2022-06-02 09:40:18] Ep. 1937 : Up. 55000 : Sen. 2,130 : Cost 0.04683007 * 1,158,935 @ 1,887 after 127,637,194 : Time 442.52s : 2618.93 words/s : gNorm 0.0963
[2022-06-02 09:40:18] Saving model weights and runtime parameters to model.seq2seq.bkrk.1/model.iter55000.npz
[2022-06-02 09:40:20] Saving model weights and runtime parameters to model.seq2seq.bkrk.1/model.npz
[2022-06-02 09:40:27] Saving Adam parameters
[2022-06-02 09:40:28] [training] Saving training checkpoint to model.seq2seq.bkrk.1/model.npz and model.seq2seq.bkrk.1/model.npz.optimizer.npz
[2022-06-02 09:41:02] [valid] Ep. 1937 : Up. 55000 : cross-entropy : 41.6271 : stalled 10 times (last best: 30.9605)
[2022-06-02 09:41:02] [valid] Ep. 1937 : Up. 55000 : perplexity : 263.356 : stalled 10 times (last best: 63.1392)
[2022-06-02 09:41:02] Translating validation set...
[2022-06-02 09:41:02] Best translation 0 : ထထိုမချေ ကကို စ လား ခပါလား ။
[2022-06-02 09:41:02] Best translation 1 : မင်း ပါတီပွဲ နောက်ကျ နီဗျာယ် ။
[2022-06-02 09:41:02] Best translation 2 : ကျေးဇူးပြု၍ သတင်းစာ ဖတ် ပါလား ။
[2022-06-02 09:41:02] Best translation 3 : သူ အိမ် ကကို ကျိန်းသီ ပြန် ဖဖိဖို့ပါ ။
[2022-06-02 09:41:02] Best translation 4 : အူ နီ ရေ ခွီး တိ ။
[2022-06-02 09:41:02] Best translation 5 : မင်း ဇာ မိန်း လေး ။
[2022-06-02 09:41:02] Best translation 10 : ယင်းသူ က ဆရာဝန် ပါ ။
[2022-06-02 09:41:02] Best translation 20 : ငါ ၂၅ ဆင့် နှစ် ခက် နန့် ၁၀ ဆင့် တန် ငါး ခက် လလို ချင်ရေ ။
[2022-06-02 09:41:02] Best translation 40 : ဒေချင့် ဇာသသူ့ ထမင်းဘူး လေး ။
[2022-06-02 09:41:02] Best translation 80 : မင်းရရဲ့ ဝမ်းကွဲ ညီ တိ က မချေ ကကို ဒေါသပပိုကြီး စီရေ ။
[2022-06-02 09:41:02] Best translation 160 : မင်း ဆီးလိပ် မ သောက် ပါလား ။
[2022-06-02 09:41:03] Best translation 320 : ထထိုမချေ က ယင်းချင့် ကကို ယယုံကြည် ခပါလား ။
[2022-06-02 09:41:03] Best translation 640 : ကျွန်တော် ဘီယာ သောက် ခပါရေ ။
[2022-06-02 09:41:03] Total translation time: 0.97518s
[2022-06-02 09:41:03] [valid] Ep. 1937 : Up. 55000 : bleu : 20.1678 : stalled 10 times (last best: 22.0371)
[2022-06-02 09:41:03] Training finished
[2022-06-02 09:41:04] Saving model weights and runtime parameters to model.seq2seq.bkrk.1/model.npz
[2022-06-02 09:41:11] Saving Adam parameters
[2022-06-02 09:41:12] [training] Saving training checkpoint to model.seq2seq.bkrk.1/model.npz and model.seq2seq.bkrk.1/model.npz.optimizer.npz

real    820m39.883s
user    986m59.393s
sys     2m19.510s
```

check the output models ...  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.bkrk.1$ ls *.npz | sort -V
model.iter5000.npz
model.iter10000.npz
model.iter15000.npz
model.iter20000.npz
model.iter25000.npz
model.iter30000.npz
model.iter35000.npz
model.iter40000.npz
model.iter45000.npz
model.iter50000.npz
model.iter55000.npz
model.npz
model.npz.optimizer.npz
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.bkrk.1$
```

script for running ...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese dialects
## used Marian NMT Framework for training
## Last updated: 31 May 2022

data_path="/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/1/";
src="bk"; tgt="rk";

for i in {5000..55000..5000}
do
    marian-decoder -m ./model.iter$i.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml --devices 0 1 --output hyp.iter$i.${tgt} < ${data_path}/test.${src};
    echo "Evaluation with hyp.iter$i.${tgt}, Transformer model:" >> eval-result.txt;
    perl /home/ye/tool/moses-scripts/scripts/generic/multi-bleu.perl ${data_path}/test.${tgt} < ./hyp.iter$i.${tgt} >> eval-result.txt;

done
```

Testing and evaluation ...  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.bkrk.1$ time ./test-eval.sh
...
...
...
[2022-06-02 10:40:22] Best translation 1038 : မင်း ဇာသသူ့ ကကို ချစ် ဖဖိဖို့လေး။
[2022-06-02 10:40:22] Best translation 1039 : မင်းဇာတိ လလိုချင် ခလေး ။
[2022-06-02 10:40:22] Best translation 1040 : သူရရိရို့ မင်း ကကို ကူညီ ကတ်ယင့်လား ။
[2022-06-02 10:40:22] Best translation 1041 : သူရရိရို့ ဇာလောက် ကတ်တီးကတ်ဖဖဲ့နနိုင် လေး။
[2022-06-02 10:40:22] Best translation 1042 : စားပွဲက ညစ်ပတ်ရေ ပန်းကန် တိ ကကို သူ ဖယ် လလိုက်တေ ။
[2022-06-02 10:40:22] Best translation 1043 : အစွပ်စွဲခံရ ရေ လူ တစ်ယောက်စွာ ဇာပပိုင် ခံစား ရဖဖိဖို့လေး ဆဆိုစွာ မင်း စဉ်းစားကြည့် ။
[2022-06-02 10:40:22] Best translation 1044 : မင်းကကို ဖက်ထား မယ် နန့် မ ဖက် ထားရ ပါလား ။
[2022-06-02 10:40:22] Best translation 1045 : မင်း တစ်ခုခု တင်ပြဖဖိဖို့ ဟိ လား ။
[2022-06-02 10:40:22] Best translation 1046 : မင်းရရိရို့ ယင်းချင့် ကကို သိမ်းထား ဖဖိဖို့လား ။
[2022-06-02 10:40:22] Best translation 1047 : မင်း ဒုက္ခ ရောက် ဖဖိဖို့ မဟုတ်ပါလား ။
[2022-06-02 10:40:22] Best translation 1048 : ယင်းချင့်ကကို သိမ်းသိမ်း မ သိမ်းသိမ်း ။
[2022-06-02 10:40:22] Best translation 1049 : သူ ညက သင်တန်း မ တက် ခ ပါ ။
[2022-06-02 10:40:22] Best translation 1050 : သူ ယင်းချင့် ကကို ကြြိုးစား ဖဖိဖို့ မဟုတ် ပါ လား ။
[2022-06-02 10:40:22] Best translation 1051 : ထထိုမချေ က သသူ့ ကကို မြတ်နနိုး ခစွာလား ။
[2022-06-02 10:40:22] Best translation 1052 : သူ တစ်ပတ်မာ ငါး ရက် အလုပ် လား ရေ ။
[2022-06-02 10:40:22] Best translation 1053 : ယင်းချင့် အတွက် မင်းငါ အိမ် ကကို လာ ရဖဖိဖို့ ။
[2022-06-02 10:40:22] Best translation 1054 : သူ ရရိရို့ တစ်ယောက်နန့် တစ်ယောက် ရန်ဖြစ် ကတ်ရေ ။
[2022-06-02 10:40:22] Best translation 1055 : မင်း ယင်းချင့် ကကို ခန့်မှန်းကြည့် ပါ။
[2022-06-02 10:40:22] Best translation 1056 : ယင်းစွာ ခက်ခဲရေ ။
[2022-06-02 10:40:22] Best translation 1057 : သူရရိရို့ ဇာသသူ့ ကကို ကူညီ ဖဖိဖို့ လေး ။
[2022-06-02 10:40:22] Best translation 1058 : သူ တင်းနစ် ကဇတ် နီရေ။
[2022-06-02 10:40:22] Best translation 1059 : ကျွန်တော်ရရိရို့ က မင်းကကို လက်ခံ ရဖဖိဖို့လား ။
[2022-06-02 10:40:22] Best translation 1060 : ကျွန်တော်ရရိရို့ မ ကြြိုးစား ခကတ်ပါ ။
[2022-06-02 10:40:22] Best translation 1061 : ဇာ အတွက် လေး။
[2022-06-02 10:40:22] Best translation 1062 : ကျွန်တော်ရရိရို့ အရုပ် တိ ရောင်းခ ဂတ် စွာ ။
[2022-06-02 10:40:22] Best translation 1063 : ကျွန်တော်ရရိရို့ သသူ့ ကကို နှှိုး ရဖဖိဖို့ မဟုတ် ပါ ။
[2022-06-02 10:40:22] Best translation 1064 : မင်း သူရရိရို့ နန့် ဆဆုံ ခရေ ။
[2022-06-02 10:40:22] Best translation 1065 : ငါ ဆရာဝန် ဘက် လား ဖဖိဖို့ ဟိရေ ။
[2022-06-02 10:40:22] Best translation 1066 : ယေကေလေ့ ၁၀၀၀မြောက် စစုံတွဲက ဒေမာ လာ ဗျာယ် ။
[2022-06-02 10:40:22] Best translation 1067 : လူကြီးမင်း ပြန်ခေါ် ချင်ပါလား ။
[2022-06-02 10:40:22] Best translation 1068 : လား မိန်းပါ ။
[2022-06-02 10:40:22] Best translation 1069 : မင်း ဇာ ကူညီ ဖဖိဖို့လေး။
[2022-06-02 10:40:22] Best translation 1070 : ဒေမာ ဆက်နီလလိလို့ မ ရဗျာယ်လား ။
[2022-06-02 10:40:22] Best translation 1071 : ယင်းချင့် ထထိုမချေ အတွက် အလွယ်ချေပါ ။
[2022-06-02 10:40:22] Total time: 14.27738s wall
It is in-advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    3m4.491s
user    5m19.878s
sys     0m31.760s
```

Results are as follows:  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.bkrk.1$ cat eval-result.txt
Evaluation with hyp.iter5000.rk, Transformer model:
BLEU = 23.24, 50.7/28.5/20.4/14.6 (BP=0.908, ratio=0.912, hyp_len=6148, ref_len=6739)
Evaluation with hyp.iter10000.rk, Transformer model:
BLEU = 21.08, 47.0/24.7/16.4/10.9 (BP=0.988, ratio=0.988, hyp_len=6661, ref_len=6739)
Evaluation with hyp.iter15000.rk, Transformer model:
BLEU = 21.04, 46.4/24.4/16.1/10.7 (BP=1.000, ratio=1.013, hyp_len=6825, ref_len=6739)
Evaluation with hyp.iter20000.rk, Transformer model:
BLEU = 20.96, 46.8/24.6/16.0/10.5 (BP=1.000, ratio=1.010, hyp_len=6806, ref_len=6739)
Evaluation with hyp.iter25000.rk, Transformer model:
BLEU = 20.33, 46.3/23.9/15.4/10.0 (BP=1.000, ratio=1.014, hyp_len=6832, ref_len=6739)
Evaluation with hyp.iter30000.rk, Transformer model:
BLEU = 20.81, 46.4/24.2/15.9/10.5 (BP=1.000, ratio=1.008, hyp_len=6791, ref_len=6739)
Evaluation with hyp.iter35000.rk, Transformer model:
BLEU = 20.92, 46.8/24.4/16.0/10.5 (BP=1.000, ratio=1.004, hyp_len=6769, ref_len=6739)
Evaluation with hyp.iter40000.rk, Transformer model:
BLEU = 20.92, 46.9/24.5/15.9/10.5 (BP=1.000, ratio=1.007, hyp_len=6785, ref_len=6739)
Evaluation with hyp.iter45000.rk, Transformer model:
BLEU = 20.57, 46.2/24.1/15.7/10.2 (BP=1.000, ratio=1.009, hyp_len=6802, ref_len=6739)
Evaluation with hyp.iter50000.rk, Transformer model:
BLEU = 20.84, 46.5/24.3/15.9/10.5 (BP=1.000, ratio=1.000, hyp_len=6736, ref_len=6739)
Evaluation with hyp.iter55000.rk, Transformer model:
BLEU = 20.93, 46.4/24.3/16.0/10.6 (BP=1.000, ratio=1.003, hyp_len=6756, ref_len=6739)
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.bkrk.1$
```

**Best BLEU score for bkrk, word unit, seq2seq is 23.24.**  

## Running with 2 Hidden Layers

for this time, I wish to run with 2 hidden layers and .  

## Updated Running Script Example for bk-dw

training bash script for 2 hidden layers and valid-mini-batch = 64.  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese and Ethnic Languages
## used Marian NMT Framework for seq2seq training
## Last updated: 2 June 2022
## for this time, enc-depth and dec-depth = 2 and valid-mini-batch = 64
## Reference: https://marian-nmt.github.io/examples/mtm2017/complex/

model_folder="model.seq2seq.bkdw.1-2hl";
mkdir ${model_folder};
data_path="/home/ye/exp/pivot-nmt-baseline/data/word/dw-bk/1/";
src="bk"; tgt="dw";


marian \
  --type s2s \
  --train-sets ${data_path}/train.${src} ${data_path}/train.${tgt} \
  --max-length 200 \
  --valid-sets ${data_path}/dev.${src} ${data_path}/dev.${tgt} \
  --vocabs  ${data_path}/vocab/vocab.${src}.yml  ${data_path}/vocab/vocab.${tgt}.yml \
  --model ${model_folder}/model.npz \
  --workspace 4500 \
  --enc-depth 2 --enc-type alternating --enc-cell lstm --enc-cell-depth 4 \
  --dec-depth 2 --dec-cell lstm --dec-cell-base-depth 4 --dec-cell-high-depth 2 \
  --tied-embeddings --layer-normalization --skip \
  --mini-batch-fit \
  --valid-mini-batch 64 \
  --valid-metrics cross-entropy perplexity bleu\
  --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
  --dropout-rnn 0.3 --dropout-src 0.3 --exponential-smoothing \
  --early-stopping 10 \
  --log ${model_folder}/train.log --valid-log ${model_folder}/valid.log \
  --devices 0 1 --sync-sgd --seed 1111  \
  --dump-config > ${model_folder}/config.yml

time marian -c ${model_folder}/config.yml  2>&1 | tee ${model_folder}/s2s.${src}-${tgt}.log
```

## bk-dw, Word, Seq2Seq, 2 Hidden Layers and Valid-Mini-Batch 64

training ...  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline$ ./seq2seq.bkdw.1-2hidden-layers.sh
...
...
...
[2022-06-02 22:04:44] [data] Done reading 5,452 sentences
[2022-06-02 22:04:44] [data] Done shuffling 5,452 sentences to temp files
[2022-06-02 22:04:53] Seen 5,452 samples
[2022-06-02 22:04:53] Starting data epoch 3928 in logical epoch 3928
[2022-06-02 22:04:53] [data] Shuffling data
[2022-06-02 22:04:53] [data] Done reading 5,452 sentences
[2022-06-02 22:04:53] [data] Done shuffling 5,452 sentences to temp files
[2022-06-02 22:05:02] Seen 5,452 samples
[2022-06-02 22:05:02] Starting data epoch 3929 in logical epoch 3929
[2022-06-02 22:05:02] [data] Shuffling data
[2022-06-02 22:05:02] [data] Done reading 5,452 sentences
[2022-06-02 22:05:02] [data] Done shuffling 5,452 sentences to temp files
[2022-06-02 22:05:08] Ep. 3929 : Up. 55000 : Sen. 3,414 : Cost 0.05739907 * 1,363,042 @ 4,606 after 149,546,172 : Time 324.39s : 4201.91 words/s : gNorm 0.0814
[2022-06-02 22:05:08] Saving model weights and runtime parameters to model.seq2seq.bkdw.1-2hl/model.iter55000.npz
[2022-06-02 22:05:08] Saving model weights and runtime parameters to model.seq2seq.bkdw.1-2hl/model.npz
[2022-06-02 22:05:14] Saving Adam parameters
[2022-06-02 22:05:14] [training] Saving training checkpoint to model.seq2seq.bkdw.1-2hl/model.npz and model.seq2seq.bkdw.1-2hl/model.npz.optimizer.npz
[2022-06-02 22:05:33] [valid] Ep. 3929 : Up. 55000 : cross-entropy : 55.6634 : stalled 10 times (last best: 42.6357)
[2022-06-02 22:05:33] [valid] Ep. 3929 : Up. 55000 : perplexity : 2643.52 : stalled 10 times (last best: 418.063)
[2022-06-02 22:05:33] Translating validation set...
[2022-06-02 22:05:33] Best translation 0 : နန် ဟှဲဖြစ်ဟှိ ပ္လေး နေဟှယ် ။
[2022-06-02 22:05:33] Best translation 1 : အဲဟှာ ကြောက်-က်စာ အီတ် ဟှီးမား ။
[2022-06-02 22:05:33] Best translation 2 : မမိုးလန်းပပိုင်း မှာ ခံဗျား ဟှယ် ခီ အိယာ က ထ နူး ။
[2022-06-02 22:05:33] Best translation 3 : ကျေးဇူးပြုပီး ကျွန်တော့ မွီးနေ့ ပွဲ ဟှှို လာ ပါလား ။
[2022-06-02 22:05:33] Best translation 4 : ဟှင့်အင်း ၊ နန် က ငါ့ ကကို တစ် ဒေါ်လာ ပေး ၊ အဲဆဆိုဟှာ ငါ့မှာ ရှိဇာ နတ်မှာ ရှိ ဇာန ၂ ဆ ဖြစ်ဟှားလလီ့မယ် ။
[2022-06-02 22:05:33] Best translation 5 : ဝယ်ယား ဟှ က သူးနနိနို့ ဝဝို သိ နေရယ် ။
[2022-06-02 22:05:34] Best translation 10 : သူ ဟှယ်ဒဒူ့ဟှှိုလည်းဖွမ့် ပြောခခဲ့ဟှှိှို့ မမိမို့ ဟှ ။
[2022-06-02 22:05:34] Best translation 20 : ကားမာ ဘီး လေးဘီးရှိဟှယ် ။
[2022-06-02 22:05:34] Best translation 40 : နေ ဟှ ခြော့-က် နာရီ ထထိုးခံ ထွပ်ဟှယ် ။
[2022-06-02 22:05:34] Best translation 80 : နန့် ဟှှို ငါ ဝဝိုင်း သယ် ပေးမယ် ။
[2022-06-02 22:05:34] Best translation 160 : နန့် ဟှှို ငါ ဝဝိုင်း သယ် ပေးမယ် ။
[2022-06-02 22:05:34] Best translation 320 : နန် ဟှယ်လလူ့ ဟှှို ရှာ ဟှှိှို့နူး ။
[2022-06-02 22:05:34] Total translation time: 0.36855s
[2022-06-02 22:05:34] [valid] Ep. 3929 : Up. 55000 : bleu : 10.1864 : stalled 4 times (last best: 10.268)
[2022-06-02 22:05:34] Training finished
[2022-06-02 22:05:34] Saving model weights and runtime parameters to model.seq2seq.bkdw.1-2hl/model.npz
[2022-06-02 22:05:39] Saving Adam parameters
[2022-06-02 22:05:40] [training] Saving training checkpoint to model.seq2seq.bkdw.1-2hl/model.npz and model.seq2seq.bkdw.1-2hl/model.npz.optimizer.npz

real    600m24.423s
user    736m10.027s
sys     2m35.297s
```

I skip to show testing steps...    
Results are as follows:  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.bkdw.1-2hl$ cat eval-result.txt
Evaluation with hyp.iter5000.dw, Transformer model:
BLEU = 9.92, 37.3/11.7/6.3/4.3 (BP=0.949, ratio=0.950, hyp_len=3813, ref_len=4013)
Evaluation with hyp.iter10000.dw, Transformer model:
BLEU = 12.64, 39.2/13.9/7.9/6.1 (BP=0.992, ratio=0.992, hyp_len=3980, ref_len=4013)
Evaluation with hyp.iter15000.dw, Transformer model:
BLEU = 11.71, 39.1/13.5/7.1/5.3 (BP=0.987, ratio=0.988, hyp_len=3963, ref_len=4013)
Evaluation with hyp.iter20000.dw, Transformer model:
BLEU = 11.97, 38.9/13.5/7.5/5.6 (BP=0.982, ratio=0.983, hyp_len=3943, ref_len=4013)
Evaluation with hyp.iter25000.dw, Transformer model:
BLEU = 12.90, 39.2/14.2/8.3/6.4 (BP=0.984, ratio=0.984, hyp_len=3949, ref_len=4013)
Evaluation with hyp.iter30000.dw, Transformer model:
BLEU = 12.85, 38.3/13.8/8.2/6.3 (BP=1.000, ratio=1.000, hyp_len=4013, ref_len=4013)
Evaluation with hyp.iter35000.dw, Transformer model:
BLEU = 13.02, 38.8/14.0/8.4/6.6 (BP=0.988, ratio=0.988, hyp_len=3964, ref_len=4013)
Evaluation with hyp.iter40000.dw, Transformer model:
BLEU = 13.11, 39.3/14.3/8.5/6.7 (BP=0.981, ratio=0.981, hyp_len=3937, ref_len=4013)
Evaluation with hyp.iter45000.dw, Transformer model:
BLEU = 13.10, 39.0/14.1/8.4/6.7 (BP=0.985, ratio=0.985, hyp_len=3954, ref_len=4013)
Evaluation with hyp.iter50000.dw, Transformer model:
BLEU = 13.38, 39.3/14.5/8.7/6.9 (BP=0.982, ratio=0.983, hyp_len=3943, ref_len=4013)
Evaluation with hyp.iter55000.dw, Transformer model:
BLEU = 13.60, 39.4/14.7/9.0/7.0 (BP=0.984, ratio=0.984, hyp_len=3950, ref_len=4013)
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.bkdw.1-2hl$
```

**Best BLEU score, bk-dw, word unit, seq2seq, config2: 13.60**  

## dw-bk, Word, Seq2Seq, 2 Hidden Layers and Valid-Mini-Batch 64

Training ...  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline$ ./seq2seq.dwbk.1-2hidden-layers.sh
...
...
...
[2022-06-03 09:08:21] [data] Done reading 5,452 sentences
[2022-06-03 09:08:21] [data] Done shuffling 5,452 sentences to temp files
[2022-06-03 09:08:30] Seen 5,452 samples
[2022-06-03 09:08:30] Starting data epoch 4230 in logical epoch 4230
[2022-06-03 09:08:30] [data] Shuffling data
[2022-06-03 09:08:30] [data] Done reading 5,452 sentences
[2022-06-03 09:08:30] [data] Done shuffling 5,452 sentences to temp files
[2022-06-03 09:08:39] Seen 5,452 samples
[2022-06-03 09:08:39] Starting data epoch 4231 in logical epoch 4231
[2022-06-03 09:08:39] [data] Shuffling data
[2022-06-03 09:08:39] [data] Done reading 5,452 sentences
[2022-06-03 09:08:39] [data] Done shuffling 5,452 sentences to temp files
[2022-06-03 09:08:46] Ep. 4231 : Up. 55000 : Sen. 3,788 : Cost 0.03955685 * 1,530,453 @ 508 after 168,911,035 : Time 338.79s : 4517.36 words/s : gNorm 0.0644
[2022-06-03 09:08:46] Saving model weights and runtime parameters to model.seq2seq.dwbk.1-2hl/model.iter55000.npz
[2022-06-03 09:08:47] Saving model weights and runtime parameters to model.seq2seq.dwbk.1-2hl/model.npz
[2022-06-03 09:08:52] Saving Adam parameters
[2022-06-03 09:08:53] [training] Saving training checkpoint to model.seq2seq.dwbk.1-2hl/model.npz and model.seq2seq.dwbk.1-2hl/model.npz.optimizer.npz
[2022-06-03 09:09:11] [valid] Ep. 4231 : Up. 55000 : cross-entropy : 57.4461 : stalled 10 times (last best: 40.6634)
[2022-06-03 09:09:12] [valid] Ep. 4231 : Up. 55000 : perplexity : 2288.85 : stalled 10 times (last best: 238.847)
[2022-06-03 09:09:12] Translating validation set...
[2022-06-03 09:09:12] Best translation 0 : နင် ဟုတ်ဘောင်းဘီ မ ဝတ် ကမား ။
[2022-06-03 09:09:12] Best translation 1 : မိန်းမချော ငယ် ရ အခန်း ထဲမှာ ရှိ ရယ် ။
[2022-06-03 09:09:12] Best translation 2 : ကိုး နာရီ ထိုးချိန် မှာ သူ ထွက် သွားရယ် ။
[2022-06-03 09:09:12] Best translation 3 : ကျေးဇူးပြု၍ ကျွန်တော့်ရဲ့ မွေးနေ့ပွဲ ကို လာ ပါလား ။
[2022-06-03 09:09:12] Best translation 4 : ဘသူပဲ့ တယ်လီဖုန်း ဆက်ဆက် ၊ သူ့လို့ဝို ငါ အပြင် သွား ဝယ်လိ ပြော လိုက်န ။
[2022-06-03 09:09:12] Best translation 5 : အဲ့အမ လေ အဲ့ဇာ ကို သိ ရယ် ။
[2022-06-03 09:09:12] Best translation 10 : သူလို့ ငါ့ အကြောင်း ကို အချင်းမပြော ကြကလား ။
[2022-06-03 09:09:12] Best translation 20 : သူ့ရဲ့ မျက်နှာလေး ကို သိ နေရယ်၊ ဒါမဲ့ သူ့ရဲ့ နာမည် ကို မ မှတ်မိ ဖြစ်နေရယ် ။
[2022-06-03 09:09:12] Best translation 40 : ဒါ ဟင်းသီးဟင်းရွက် ဒေ က ကျက်အားကြီးပြီး ပျော့ပြဲ နေရဘ် ။
[2022-06-03 09:09:12] Best translation 80 : ဒယ်ကောင်မငယ် ဝို တွေ့ ရဇာ ဝမ်းသာ ရယ် ။
[2022-06-03 09:09:12] Best translation 160 : ဒယ်ကောင်မငယ် ဝို မ ကူညီ ရရိ စိတ်တောင် မကောင်းရ ။
[2022-06-03 09:09:12] Best translation 320 : နင် ဖယ်သူ့ ဝို တွေ့ ဝို့လဲ ။
[2022-06-03 09:09:12] Total translation time: 0.37010s
[2022-06-03 09:09:12] [valid] Ep. 4231 : Up. 55000 : bleu : 11.3127 : stalled 4 times (last best: 11.5023)
[2022-06-03 09:09:12] Training finished
[2022-06-03 09:09:12] Saving model weights and runtime parameters to model.seq2seq.dwbk.1-2hl/model.npz
[2022-06-03 09:09:17] Saving Adam parameters
[2022-06-03 09:09:18] [training] Saving training checkpoint to model.seq2seq.dwbk.1-2hl/model.npz and model.seq2seq.dwbk.1-2hl/model.npz.optimizer.npz

real    626m59.828s
user    768m43.898s
sys     2m45.149s
```

Results are as follows:  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.dwbk.1-2hl$ cat eval-result.txt
Evaluation with hyp.iter5000.bk, Transformer model:
BLEU = 9.98, 38.7/11.9/6.2/4.4 (BP=0.942, ratio=0.944, hyp_len=4027, ref_len=4267)
Evaluation with hyp.iter10000.bk, Transformer model:
BLEU = 11.96, 39.9/13.8/7.5/5.2 (BP=0.987, ratio=0.987, hyp_len=4213, ref_len=4267)
Evaluation with hyp.iter15000.bk, Transformer model:
BLEU = 12.65, 40.6/14.4/8.0/5.6 (BP=0.992, ratio=0.992, hyp_len=4232, ref_len=4267)
Evaluation with hyp.iter20000.bk, Transformer model:
BLEU = 12.67, 40.1/14.3/8.1/5.6 (BP=1.000, ratio=1.001, hyp_len=4271, ref_len=4267)
Evaluation with hyp.iter25000.bk, Transformer model:
BLEU = 12.35, 40.4/14.1/7.7/5.3 (BP=0.999, ratio=0.999, hyp_len=4262, ref_len=4267)
Evaluation with hyp.iter30000.bk, Transformer model:
BLEU = 12.21, 40.1/13.8/7.6/5.3 (BP=0.998, ratio=0.998, hyp_len=4260, ref_len=4267)
Evaluation with hyp.iter35000.bk, Transformer model:
BLEU = 12.34, 40.4/13.9/7.7/5.5 (BP=0.995, ratio=0.995, hyp_len=4244, ref_len=4267)
Evaluation with hyp.iter40000.bk, Transformer model:
BLEU = 12.40, 40.5/14.0/7.8/5.4 (BP=0.998, ratio=0.998, hyp_len=4260, ref_len=4267)
Evaluation with hyp.iter45000.bk, Transformer model:
BLEU = 12.30, 40.2/13.9/7.6/5.4 (BP=1.000, ratio=1.001, hyp_len=4273, ref_len=4267)
Evaluation with hyp.iter50000.bk, Transformer model:
BLEU = 12.67, 40.8/14.5/8.0/5.6 (BP=0.993, ratio=0.993, hyp_len=4238, ref_len=4267)
Evaluation with hyp.iter55000.bk, Transformer model:
BLEU = 12.31, 40.3/14.0/7.7/5.3 (BP=0.996, ratio=0.996, hyp_len=4251, ref_len=4267)
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.dwbk.1-2hl$
```

**Best BLEU score for dw-bk, word unit, seq2seq, config2 is 12.67.**  

## rk-bk, Word, Seq2Seq, 2 Hidden Layers and Valid-Mini-Batch 64

config2 preparation and training bash script for rk-bk language pair...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese and Ethnic Languages
## used Marian NMT Framework for seq2seq training
## Last updated: 2 June 2022
## for this time, enc-depth and dec-depth = 2 and valid-mini-batch = 64
## Reference: https://marian-nmt.github.io/examples/mtm2017/complex/

model_folder="model.seq2seq.rkbk.1-2hl";
mkdir ${model_folder};
data_path="/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/1/";
src="rk"; tgt="bk";


marian \
  --type s2s \
  --train-sets ${data_path}/train.${src} ${data_path}/train.${tgt} \
  --max-length 200 \
  --valid-sets ${data_path}/dev.${src} ${data_path}/dev.${tgt} \
  --vocabs  ${data_path}/vocab/vocab.${src}.yml  ${data_path}/vocab/vocab.${tgt}.yml \
  --model ${model_folder}/model.npz \
  --workspace 4500 \
  --enc-depth 2 --enc-type alternating --enc-cell lstm --enc-cell-depth 4 \
  --dec-depth 2 --dec-cell lstm --dec-cell-base-depth 4 --dec-cell-high-depth 2 \
  --tied-embeddings --layer-normalization --skip \
  --mini-batch-fit \
  --valid-mini-batch 64 \
  --valid-metrics cross-entropy perplexity bleu\
  --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
  --dropout-rnn 0.3 --dropout-src 0.3 --exponential-smoothing \
  --early-stopping 10 \
  --log ${model_folder}/train.log --valid-log ${model_folder}/valid.log \
  --devices 0 1 --sync-sgd --seed 1111  \
  --dump-config > ${model_folder}/config.yml

time marian -c ${model_folder}/config.yml  2>&1 | tee ${model_folder}/s2s.${src}-${tgt}.log
```

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline$ ./seq2seq.rkbk.1-2hidden-layers.sh
...
...
...
[2022-06-03 23:12:20] [data] Done shuffling 8,850 sentences to temp files
[2022-06-03 23:12:36] Seen 8,850 samples
[2022-06-03 23:12:36] Starting data epoch 2304 in logical epoch 2304
[2022-06-03 23:12:36] [data] Shuffling data
[2022-06-03 23:12:36] [data] Done reading 8,850 sentences
[2022-06-03 23:12:36] [data] Done shuffling 8,850 sentences to temp files
[2022-06-03 23:12:53] Seen 8,850 samples
[2022-06-03 23:12:53] Starting data epoch 2305 in logical epoch 2305
[2022-06-03 23:12:53] [data] Shuffling data
[2022-06-03 23:12:53] [data] Done reading 8,850 sentences
[2022-06-03 23:12:53] [data] Done shuffling 8,850 sentences to temp files
[2022-06-03 23:13:05] Ep. 2305 : Up. 55000 : Sen. 6,830 : Cost 0.03575936 * 1,402,000 @ 313 after 154,500,231 : Time 347.08s : 4039.44 words/s : gNorm 0.0892
[2022-06-03 23:13:05] Saving model weights and runtime parameters to model.seq2seq.rkbk.1-2hl/model.iter55000.npz
[2022-06-03 23:13:06] Saving model weights and runtime parameters to model.seq2seq.rkbk.1-2hl/model.npz
[2022-06-03 23:13:11] Saving Adam parameters
[2022-06-03 23:13:12] [training] Saving training checkpoint to model.seq2seq.rkbk.1-2hl/model.npz and model.seq2seq.rkbk.1-2hl/model.npz.optimizer.npz
[2022-06-03 23:13:32] [valid] Ep. 2305 : Up. 55000 : cross-entropy : 42.9832 : stalled 10 times (last best: 31.7675)
[2022-06-03 23:13:32] [valid] Ep. 2305 : Up. 55000 : perplexity : 279.112 : stalled 10 times (last best: 64.2083)
[2022-06-03 23:13:32] Translating validation set...
[2022-06-03 23:13:32] Best translation 0 : ဒယ်ကောင်မ ငါ့ ဝို စ ခဲ့ဇာ မ ဟုတ် ဝလား ။
[2022-06-03 23:13:32] Best translation 1 : မင်း ရှူးဖိနပ် မ စီး ရလား ။
[2022-06-03 23:13:32] Best translation 2 : ကျွန်တော် အကြံပြု မယ်လန်း ။
[2022-06-03 23:13:32] Best translation 3 : သူရဲ့ အိမ် ကို အလည် လာ ဖို့ သူ က ဒယ်ကောင်မငယ် ကို မ ဖိတ် ခဲ့ဘူး ။
[2022-06-03 23:13:32] Best translation 4 : အူနေ တဲ့ ခွေး ဒွေ ။
[2022-06-03 23:13:32] Best translation 5 : နင် ဘာ မေး ဝို့ ။
[2022-06-03 23:13:32] Best translation 10 : သူ မင်္ဂလာဆောင် ပြီး လား ။
[2022-06-03 23:13:32] Best translation 20 :
[2022-06-03 23:13:32] Best translation 40 : အယ့်ဒါ ဘယ်သူ့ ဓာတ်ပုံ ရိ ။
[2022-06-03 23:13:32] Best translation 80 : ဒါ စာအုပ် မှာ ဝတ္တုတို ဆယ် ပုဒ် ပါ ရယ် ။
[2022-06-03 23:13:32] Best translation 160 : မင့် အကုန်အကျ ရက် ပတ်သက်ရိ မ ပူ တတ် ။
[2022-06-03 23:13:32] Best translation 320 : ဒါမယ့် ယဉ်ကျေးတဲ့ ပေါင်းစည်းနေထိုင်ခြင်း ကိုတော့ ယုံကြည် မှု ရှိရယ် ။
[2022-06-03 23:13:33] Best translation 640 : ငါ လိမ္မော်ဖျော်ရယ် သောက် ချင် ရယ် ။
[2022-06-03 23:13:33] Total translation time: 0.65891s
[2022-06-03 23:13:33] [valid] Ep. 2305 : Up. 55000 : bleu : 22.5573 : stalled 2 times (last best: 22.6372)
[2022-06-03 23:13:33] Training finished
[2022-06-03 23:13:33] Saving model weights and runtime parameters to model.seq2seq.rkbk.1-2hl/model.npz
[2022-06-03 23:13:38] Saving Adam parameters
[2022-06-03 23:13:39] [training] Saving training checkpoint to model.seq2seq.rkbk.1-2hl/model.npz and model.seq2seq.rkbk.1-2hl/model.npz.optimizer.npz

real    644m25.648s
user    787m56.514s
sys     2m27.794s
```

Checked the output models and prepared test-eval.sh bash script.  
After the testing/evaluation ...  
Results are as follows:  

```
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.rkbk.1-2hl$ cat eval-result.txt
Evaluation with hyp.iter5000.bk, Transformer model:
BLEU = 10.67, 42.6/13.7/8.3/6.7 (BP=0.796, ratio=0.814, hyp_len=5662, ref_len=6956)
Evaluation with hyp.iter10000.bk, Transformer model:
BLEU = 21.40, 45.1/21.8/16.1/13.6 (BP=0.994, ratio=0.994, hyp_len=6916, ref_len=6956)
Evaluation with hyp.iter15000.bk, Transformer model:
BLEU = 21.62, 45.3/22.1/16.2/13.5 (BP=1.000, ratio=1.003, hyp_len=6977, ref_len=6956)
Evaluation with hyp.iter20000.bk, Transformer model:
BLEU = 21.30, 45.1/21.9/15.8/13.2 (BP=1.000, ratio=1.009, hyp_len=7017, ref_len=6956)
Evaluation with hyp.iter25000.bk, Transformer model:
BLEU = 21.92, 45.7/22.5/16.4/13.7 (BP=1.000, ratio=1.011, hyp_len=7030, ref_len=6956)
Evaluation with hyp.iter30000.bk, Transformer model:
BLEU = 21.57, 45.6/22.2/16.0/13.4 (BP=1.000, ratio=1.023, hyp_len=7113, ref_len=6956)
Evaluation with hyp.iter35000.bk, Transformer model:
BLEU = 21.77, 45.7/22.4/16.2/13.5 (BP=1.000, ratio=1.014, hyp_len=7050, ref_len=6956)
Evaluation with hyp.iter40000.bk, Transformer model:
BLEU = 21.85, 46.0/22.5/16.2/13.6 (BP=1.000, ratio=1.009, hyp_len=7020, ref_len=6956)
Evaluation with hyp.iter45000.bk, Transformer model:
BLEU = 21.63, 45.6/22.2/16.0/13.5 (BP=1.000, ratio=1.012, hyp_len=7037, ref_len=6956)
Evaluation with hyp.iter50000.bk, Transformer model:
BLEU = 21.80, 45.7/22.4/16.2/13.6 (BP=1.000, ratio=1.015, hyp_len=7057, ref_len=6956)
Evaluation with hyp.iter55000.bk, Transformer model:
BLEU = 22.06, 46.0/22.7/16.5/13.7 (BP=1.000, ratio=1.014, hyp_len=7053, ref_len=6956)
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline/model.seq2seq.rkbk.1-2hl$
```

**Best BLEU score for rkbk, word unit, seq2seq archi with 2nd configuration file is 22.06.**  

## bk-rk, Word, Seq2Seq, 2 Hidden Layers and Valid-Mini-Batch 64

bash script for training bk-rk is as follows:  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese and Ethnic Languages
## used Marian NMT Framework for seq2seq training
## Last updated: 2 June 2022
## for this time, enc-depth and dec-depth = 2 and valid-mini-batch = 64
## Reference: https://marian-nmt.github.io/examples/mtm2017/complex/

model_folder="model.seq2seq.bkrk.1-2hl";
mkdir ${model_folder};
data_path="/home/ye/exp/pivot-nmt-baseline/data/word/rk-bk/1/";
src="bk"; tgt="rk";


marian \
  --type s2s \
  --train-sets ${data_path}/train.${src} ${data_path}/train.${tgt} \
  --max-length 200 \
  --valid-sets ${data_path}/dev.${src} ${data_path}/dev.${tgt} \
  --vocabs  ${data_path}/vocab/vocab.${src}.yml  ${data_path}/vocab/vocab.${tgt}.yml \
  --model ${model_folder}/model.npz \
  --workspace 4500 \
  --enc-depth 2 --enc-type alternating --enc-cell lstm --enc-cell-depth 4 \
  --dec-depth 2 --dec-cell lstm --dec-cell-base-depth 4 --dec-cell-high-depth 2 \
  --tied-embeddings --layer-normalization --skip \
  --mini-batch-fit \
  --valid-mini-batch 64 \
  --valid-metrics cross-entropy perplexity bleu\
  --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
  --dropout-rnn 0.3 --dropout-src 0.3 --exponential-smoothing \
  --early-stopping 10 \
  --log ${model_folder}/train.log --valid-log ${model_folder}/valid.log \
  --devices 0 1 --sync-sgd --seed 1111  \
  --dump-config > ${model_folder}/config.yml

time marian -c ${model_folder}/config.yml  2>&1 | tee ${model_folder}/s2s.${src}-${tgt}.log
```

training ...  
```
[2022-06-04 21:58:33] [data] Done shuffling 8,850 sentences to temp files
[2022-06-04 21:58:49] Seen 8,850 samples
[2022-06-04 21:58:49] Starting data epoch 2420 in logical epoch 2420
[2022-06-04 21:58:49] [data] Shuffling data
[2022-06-04 21:58:49] [data] Done reading 8,850 sentences
[2022-06-04 21:58:49] [data] Done shuffling 8,850 sentences to temp files
[2022-06-04 21:59:04] Seen 8,850 samples
[2022-06-04 21:59:04] Starting data epoch 2421 in logical epoch 2421
[2022-06-04 21:59:04] [data] Shuffling data
[2022-06-04 21:59:04] [data] Done reading 8,850 sentences
[2022-06-04 21:59:04] [data] Done shuffling 8,850 sentences to temp files
[2022-06-04 21:59:13] Ep. 2421 : Up. 55000 : Sen. 5,744 : Cost 0.04726242 * 1,455,864 @ 4,550 after 159,570,212 : Time 340.43s : 4276.59 words/s : gNorm 0.1414
[2022-06-04 21:59:13] Saving model weights and runtime parameters to model.seq2seq.bkrk.1-2hl/model.iter55000.npz
[2022-06-04 21:59:14] Saving model weights and runtime parameters to model.seq2seq.bkrk.1-2hl/model.npz
[2022-06-04 21:59:19] Saving Adam parameters
[2022-06-04 21:59:20] [training] Saving training checkpoint to model.seq2seq.bkrk.1-2hl/model.npz and model.seq2seq.bkrk.1-2hl/model.npz.optimizer.npz
[2022-06-04 21:59:40] [valid] Ep. 2421 : Up. 55000 : cross-entropy : 42.8806 : stalled 10 times (last best: 33.181)
[2022-06-04 21:59:40] [valid] Ep. 2421 : Up. 55000 : perplexity : 311.479 : stalled 10 times (last best: 84.9989)
[2022-06-04 21:59:40] Translating validation set...
[2022-06-04 21:59:40] Best translation 0 : သူရို့ ကို မင်း အပြစ်ပီး ခပါလား ။
[2022-06-04 21:59:40] Best translation 1 : ယေကေဆင်ဟိ လား ။
[2022-06-04 21:59:40] Best translation 2 : ချစ်သူ ဟိ ပါလား ။
[2022-06-04 21:59:40] Best translation 3 : သူ ကောင်ခေျ ကို ဇာ သင်ပီးစွာလေ။
[2022-06-04 21:59:40] Best translation 4 : သံသယဖြစ် ရေ နီရာတိ ကို စစ်ဆီး ပါ ။
[2022-06-04 21:59:40] Best translation 5 : မင်း ဇာ မိန်း လေး ။
[2022-06-04 21:59:40] Best translation 10 : ယင်းသူ က ဆရာဝန် ပါ ။
[2022-06-04 21:59:40] Best translation 20 : ငါ ၂၅ ဆင့် နှစ် ခက် နန့် ၁၀ ဆင့် တန် ငါး ခက် လို ချင်ရေ ။
[2022-06-04 21:59:40] Best translation 40 : ဒေချင့် ဇာသူ့ အရုပ် လေး ။
[2022-06-04 21:59:40] Best translation 80 : မင်းရဲ့ ကော်ဖီ ထဲ သကြား မဟုတ်ကေ နှို့မှုန့် ထည့် ဖို့လား ။
[2022-06-04 21:59:40] Best translation 160 : မင်း ဆီးလိပ် မ သောက် ပါလား ။
[2022-06-04 21:59:40] Best translation 320 : ထိုမချေ က ယင်းချင့်ကို မှတ်တမ်းတင် ချင် ရေ ။
[2022-06-04 21:59:40] Best translation 640 : ကျွန်တော် ဘီယာ သောက် ဖို့ ။
[2022-06-04 21:59:40] Total translation time: 0.63411s
[2022-06-04 21:59:40] [valid] Ep. 2421 : Up. 55000 : bleu : 19.4985 : new best
[2022-06-04 21:59:41] Training finished
[2022-06-04 21:59:41] Saving model weights and runtime parameters to model.seq2seq.bkrk.1-2hl/model.npz
[2022-06-04 21:59:47] Saving Adam parameters
[2022-06-04 21:59:48] [training] Saving training checkpoint to model.seq2seq.bkrk.1-2hl/model.npz and model.seq2seq.bkrk.1-2hl/model.npz.optimizer.npz

real    631m0.818s
user    781m10.016s
sys     2m33.116s
(marian) ye@ye-System-Product-Name:~/exp/pivot-nmt-baseline$ ./seq2seq.bkrk.1-2hidden-layers.sh
```

Prepared test-eval script and run testing-evaluation.  
Results are as follows:  

```

```

Some more experiments ...  

```

```

```

```

```

```


