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


