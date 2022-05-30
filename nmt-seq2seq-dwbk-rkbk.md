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


```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```


