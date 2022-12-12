# စာကြောင်း တစ်ကြောင်းချင်းစီ ဖြတ်တာကို classification problem အနေနဲ့ လုပ်ကြည့်ခဲ့တဲ့ experiment log

## preprocessing

```
(base) ye@ykt-pro:~/exp/mySent/data/clean-data-rdy2train/data-sent$ ls
test.my  test.tg  train.my  train.tg  valid.my  valid.tg
(base) ye@ykt-pro:~/exp/mySent/data/clean-data-rdy2train/data-sent$ cat train.my valid.my > ../../pre-process/train-valid.sent.my
(base) ye@ykt-pro:~/exp/mySent/data/clean-data-rdy2train/data-sent$ cp test.my ../../pre-process/test.sent.my
(base) ye@ykt-pro:~/exp/mySent/data/clean-data-rdy2train/data-sent$ cd ../data-sent
data-sent/      data-sent+para/ 
(base) ye@ykt-pro:~/exp/mySent/data/clean-data-rdy2train/data-sent$ cd ../data-sent+para/
(base) ye@ykt-pro:~/exp/mySent/data/clean-data-rdy2train/data-sent+para$ ls
test.my  test.tg  train.my  train.tg  valid.my  valid.tg
(base) ye@ykt-pro:~/exp/mySent/data/clean-data-rdy2train/data-sent+para$ cat train.my valid.my > ../../pre-process/train-valid.para.my
(base) ye@ykt-pro:~/exp/mySent/data/clean-data-rdy2train/data-sent+para$ cp test.my > ../../pre-process/test.para.my
cp: missing destination file operand after 'test.my'
Try 'cp --help' for more information.
(base) ye@ykt-pro:~/exp/mySent/data/clean-data-rdy2train/data-sent+para$ cp test.my ../../pre-process/test.para.my
(base) ye@ykt-pro:~/exp/mySent/data/clean-data-rdy2train/data-sent+para$ cd ..
(base) ye@ykt-pro:~/exp/mySent/data/clean-data-rdy2train$ cd ..
(base) ye@ykt-pro:~/exp/mySent/data$ ls
clean-data-rdy2train  clean-data-rdy2train.zip  pre-process
(base) ye@ykt-pro:~/exp/mySent/data$ cd pre-process/
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ ls
test.para.my  test.sent.my  train-valid.para.my  train-valid.sent.my
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ chmod -x test.sent.my 
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ ls
test.para.my  test.sent.my  train-valid.para.my  train-valid.sent.my
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ wc *
    5512    96632  1380183 test.para.my
    4712    63622   919423 test.sent.my
   50081   896025 12821847 train-valid.para.my
   42414   575856  8335164 train-valid.sent.my
  102719  1632135 23456617 total
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ 
```

check current content:  

```
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ head -n 3 train-valid.sent.my 
ဘာ ရယ် လို့ တိတိကျကျ ထောက်မပြ နိုင် ပေမဲ့ ပြဿနာ တစ် ခု ခု ရှိ တယ် နဲ့ တူ တယ်
လူ့ အဖွဲ့အစည်း က ရှပ်ထွေး လာ တာ နဲ့ အမျှ အရင် က မ ရှိ ခဲ့ တဲ့ လူမှုရေး ပြဿနာ တွေ ဖြစ်ပေါ် လာ ခဲ့ တယ်
အခု အလုပ် လုပ် နေ ပါ တယ်
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ head -n 3 train-valid.para.my 
နားလည် ပါ ပြီ
ဈေး က များ လှ ချေ လား
သူ ဒီ နေ့ နည်းနည်း ပင်ပန်း နေ တယ် ထင် တယ်
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ tail -n 3 train-valid.para.my 
စစ်ကြည့် ပါ
သို့သော် အချို့ မှာ ကုန်း ပေါ် တွင် သိမ်း များ စင်ရော် များ ဂဏန်း များ မြွေ များ ၏ ဘေးရန် ကြောင့် သေ ကြေ ကြ ၍ ရေ တွင် ငါး ကြီး များ မိကျောင်း များ ဝါးမျို စားသောက် သဖြင့် ပျက်စီး ကြ ရ သည်
ကျွန်တော် တို့ လက်ထပ် တာ ကို မိဘ က သဘောတူ ခွင့်ပြု ခဲ့ တယ်
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ 
```

## Preparation for Sentence Level

I updated the print-ngram.pl program as follows:  

```perl
#!/usr/bin/env perl

# printing bi-gram, tri-gram, ngram word list with label
# this program is updated version of "print-ngram.pl"
# Written by Ye Kyaw Thu, Affiliate Professor,
# CADT, Phnom Penh, Cambodia
# Last updated: 12 Dec 2022
#
# How to run: perl print-ngram.pl <input-file> <n-gram value>
# e.g. for 2 gram: perl ./change-ngram-label.pl ./input.txt 2
# e.g. for 3 gram: perl ./change-ngram-label.pl ./input.txt 3
 

use strict;
use warnings;
use utf8;

binmode(STDIN, ":utf8");
binmode(STDOUT, ":utf8");
binmode(STDERR, ":utf8");

# assign ngram value
my $n = $ARGV[1]-1; 

open (my $inputFILE,"<:encoding(utf8)", $ARGV[0]) or die "Couldn't open input file $ARGV[0]!, $!\n";

while (!eof($inputFILE)) {
     
   my $line = <$inputFILE>;
   if (($line ne '') & ($line !~ /^ *$/)) {

       chomp($line);

       # split the sentence with space and assign into array
       my @tokens = split(' ', $line);
  
      for(my $i=0;$i<=$#tokens-$n;$i++){
         if($i==$#tokens-$n){
             print ("__label__E "."@tokens[$i .. $i+$n]\n");
         }else{
            print ("__label__O "."@tokens[$i .. $i+$n]\n");
         }
      }
    }
}

close ($inputFILE);
```

start test run ...  
test input file is as follows:  

```
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ head input
ဘာ ရယ် လို့ တိတိကျကျ ထောက်မပြ နိုင် ပေမဲ့ ပြဿနာ တစ် ခု ခု ရှိ တယ် နဲ့ တူ တယ်
လူ့ အဖွဲ့အစည်း က ရှပ်ထွေး လာ တာ နဲ့ အမျှ အရင် က မ ရှိ ခဲ့ တဲ့ လူမှုရေး ပြဿနာ တွေ ဖြစ်ပေါ် လာ ခဲ့ တယ်
အခု အလုပ် လုပ် နေ ပါ တယ်
ကြည့် ရေစာ တွေ က အဲဒီ တစ် ခု နဲ့ မ တူ ဘူး
ဘူမိ ရုပ်သွင် ပညာ သည် ကုန်းမြေသဏ္ဌာန် များ ကို လေ့လာ သော ပညာရပ် ဖြစ် သည်
ခြေဆစ် လက်ဆစ် တို့ ၏ အထက် နား မှ ရှည်လျား သော အမွေး မျှင် များ ကျ လျက် ရှိ သည်
အမြန်နှုန်း မြင့် လွန်း တဲ့ ကား က အန္တရာယ် များ တယ်
မချုပ် တည်း နိုင် တော့ ပဲ ကျောင်းဆောင် ထဲ က အပျိုစင် နတ် ဘုရား အသီးနား ရဲ့ ရုပ် ထု ရှေ့ မှာ ပဲ မက်ဒူးဆာ ကို အနိုင် အထက် ပြု လို့မယား အဖြစ် သိမ်းပိုက် လိုက် ပါ လေ တယ်
နောက် မှ ကော်ဖီ ဖြစ် ဖြစ် တစ် ခွက် လောက် သောက် ကြ ရအောင်
နေ့ တိုင်း အသား ပဲ စား နေ ရ တော့ အခု ဆို ငြီးငွေ့ လာ ပြီ
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$
```

test run for 2-gram output:  

```
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ perl ./change-ngram-label.pl ./input 2 
__label__O ဘာ ရယ်
__label__O ရယ် လို့
__label__O လို့ တိတိကျကျ
__label__O တိတိကျကျ ထောက်မပြ
__label__O ထောက်မပြ နိုင်
__label__O နိုင် ပေမဲ့
__label__O ပေမဲ့ ပြဿနာ
__label__O ပြဿနာ တစ်
__label__O တစ် ခု
__label__O ခု ခု
__label__O ခု ရှိ
__label__O ရှိ တယ်
__label__O တယ် နဲ့
__label__O နဲ့ တူ
__label__E တူ တယ်
__label__O လူ့ အဖွဲ့အစည်း
__label__O အဖွဲ့အစည်း က
__label__O က ရှပ်ထွေး
__label__O ရှပ်ထွေး လာ
__label__O လာ တာ
__label__O တာ နဲ့
__label__O နဲ့ အမျှ
__label__O အမျှ အရင်
__label__O အရင် က
__label__O က မ
__label__O မ ရှိ
__label__O ရှိ ခဲ့
__label__O ခဲ့ တဲ့
__label__O တဲ့ လူမှုရေး
__label__O လူမှုရေး ပြဿနာ
__label__O ပြဿနာ တွေ
__label__O တွေ ဖြစ်ပေါ်
__label__O ဖြစ်ပေါ် လာ
__label__O လာ ခဲ့
__label__E ခဲ့ တယ်
__label__O အခု အလုပ်
__label__O အလုပ် လုပ်
__label__O လုပ် နေ
__label__O နေ ပါ
__label__E ပါ တယ်
__label__O ကြည့် ရေစာ
__label__O ရေစာ တွေ
__label__O တွေ က
__label__O က အဲဒီ
__label__O အဲဒီ တစ်
__label__O တစ် ခု
__label__O ခု နဲ့
__label__O နဲ့ မ
__label__O မ တူ
__label__E တူ ဘူး
__label__O ဘူမိ ရုပ်သွင်
__label__O ရုပ်သွင် ပညာ
__label__O ပညာ သည်
__label__O သည် ကုန်းမြေသဏ္ဌာန်
__label__O ကုန်းမြေသဏ္ဌာန် များ
__label__O များ ကို
__label__O ကို လေ့လာ
__label__O လေ့လာ သော
__label__O သော ပညာရပ်
__label__O ပညာရပ် ဖြစ်
__label__E ဖြစ် သည်
__label__O ခြေဆစ် လက်ဆစ်
__label__O လက်ဆစ် တို့
__label__O တို့ ၏
__label__O ၏ အထက်
__label__O အထက် နား
__label__O နား မှ
__label__O မှ ရှည်လျား
__label__O ရှည်လျား သော
__label__O သော အမွေး
__label__O အမွေး မျှင်
__label__O မျှင် များ
__label__O များ ကျ
__label__O ကျ လျက်
__label__O လျက် ရှိ
__label__E ရှိ သည်
__label__O အမြန်နှုန်း မြင့်
__label__O မြင့် လွန်း
__label__O လွန်း တဲ့
__label__O တဲ့ ကား
__label__O ကား က
__label__O က အန္တရာယ်
__label__O အန္တရာယ် များ
__label__E များ တယ်
__label__O မချုပ် တည်း
__label__O တည်း နိုင်
__label__O နိုင် တော့
__label__O တော့ ပဲ
__label__O ပဲ ကျောင်းဆောင်
__label__O ကျောင်းဆောင် ထဲ
__label__O ထဲ က
__label__O က အပျိုစင်
__label__O အပျိုစင် နတ်
__label__O နတ် ဘုရား
__label__O ဘုရား အသီးနား
__label__O အသီးနား ရဲ့
__label__O ရဲ့ ရုပ်
__label__O ရုပ် ထု
__label__O ထု ရှေ့
__label__O ရှေ့ မှာ
__label__O မှာ ပဲ
__label__O ပဲ မက်ဒူးဆာ
__label__O မက်ဒူးဆာ ကို
__label__O ကို အနိုင်
__label__O အနိုင် အထက်
__label__O အထက် ပြု
__label__O ပြု လို့မယား
__label__O လို့မယား အဖြစ်
__label__O အဖြစ် သိမ်းပိုက်
__label__O သိမ်းပိုက် လိုက်
__label__O လိုက် ပါ
__label__O ပါ လေ
__label__E လေ တယ်
__label__O နောက် မှ
__label__O မှ ကော်ဖီ
__label__O ကော်ဖီ ဖြစ်
__label__O ဖြစ် ဖြစ်
__label__O ဖြစ် တစ်
__label__O တစ် ခွက်
__label__O ခွက် လောက်
__label__O လောက် သောက်
__label__O သောက် ကြ
__label__E ကြ ရအောင်
__label__O နေ့ တိုင်း
__label__O တိုင်း အသား
__label__O အသား ပဲ
__label__O ပဲ စား
__label__O စား နေ
__label__O နေ ရ
__label__O ရ တော့
__label__O တော့ အခု
__label__O အခု ဆို
__label__O ဆို ငြီးငွေ့
__label__O ငြီးငွေ့ လာ
__label__E လာ ပြီ
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ 
```

test run for 3-gram output:  

```
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ perl ./change-ngram-label.pl ./input 3
__label__O ဘာ ရယ် လို့
__label__O ရယ် လို့ တိတိကျကျ
__label__O လို့ တိတိကျကျ ထောက်မပြ
__label__O တိတိကျကျ ထောက်မပြ နိုင်
__label__O ထောက်မပြ နိုင် ပေမဲ့
__label__O နိုင် ပေမဲ့ ပြဿနာ
__label__O ပေမဲ့ ပြဿနာ တစ်
__label__O ပြဿနာ တစ် ခု
__label__O တစ် ခု ခု
__label__O ခု ခု ရှိ
__label__O ခု ရှိ တယ်
__label__O ရှိ တယ် နဲ့
__label__O တယ် နဲ့ တူ
__label__E နဲ့ တူ တယ်
__label__O လူ့ အဖွဲ့အစည်း က
__label__O အဖွဲ့အစည်း က ရှပ်ထွေး
__label__O က ရှပ်ထွေး လာ
__label__O ရှပ်ထွေး လာ တာ
__label__O လာ တာ နဲ့
__label__O တာ နဲ့ အမျှ
__label__O နဲ့ အမျှ အရင်
__label__O အမျှ အရင် က
__label__O အရင် က မ
__label__O က မ ရှိ
__label__O မ ရှိ ခဲ့
__label__O ရှိ ခဲ့ တဲ့
__label__O ခဲ့ တဲ့ လူမှုရေး
__label__O တဲ့ လူမှုရေး ပြဿနာ
__label__O လူမှုရေး ပြဿနာ တွေ
__label__O ပြဿနာ တွေ ဖြစ်ပေါ်
__label__O တွေ ဖြစ်ပေါ် လာ
__label__O ဖြစ်ပေါ် လာ ခဲ့
__label__E လာ ခဲ့ တယ်
__label__O အခု အလုပ် လုပ်
__label__O အလုပ် လုပ် နေ
__label__O လုပ် နေ ပါ
__label__E နေ ပါ တယ်
__label__O ကြည့် ရေစာ တွေ
__label__O ရေစာ တွေ က
__label__O တွေ က အဲဒီ
__label__O က အဲဒီ တစ်
__label__O အဲဒီ တစ် ခု
__label__O တစ် ခု နဲ့
__label__O ခု နဲ့ မ
__label__O နဲ့ မ တူ
__label__E မ တူ ဘူး
__label__O ဘူမိ ရုပ်သွင် ပညာ
__label__O ရုပ်သွင် ပညာ သည်
__label__O ပညာ သည် ကုန်းမြေသဏ္ဌာန်
__label__O သည် ကုန်းမြေသဏ္ဌာန် များ
__label__O ကုန်းမြေသဏ္ဌာန် များ ကို
__label__O များ ကို လေ့လာ
__label__O ကို လေ့လာ သော
__label__O လေ့လာ သော ပညာရပ်
__label__O သော ပညာရပ် ဖြစ်
__label__E ပညာရပ် ဖြစ် သည်
__label__O ခြေဆစ် လက်ဆစ် တို့
__label__O လက်ဆစ် တို့ ၏
__label__O တို့ ၏ အထက်
__label__O ၏ အထက် နား
__label__O အထက် နား မှ
__label__O နား မှ ရှည်လျား
__label__O မှ ရှည်လျား သော
__label__O ရှည်လျား သော အမွေး
__label__O သော အမွေး မျှင်
__label__O အမွေး မျှင် များ
__label__O မျှင် များ ကျ
__label__O များ ကျ လျက်
__label__O ကျ လျက် ရှိ
__label__E လျက် ရှိ သည်
__label__O အမြန်နှုန်း မြင့် လွန်း
__label__O မြင့် လွန်း တဲ့
__label__O လွန်း တဲ့ ကား
__label__O တဲ့ ကား က
__label__O ကား က အန္တရာယ်
__label__O က အန္တရာယ် များ
__label__E အန္တရာယ် များ တယ်
__label__O မချုပ် တည်း နိုင်
__label__O တည်း နိုင် တော့
__label__O နိုင် တော့ ပဲ
__label__O တော့ ပဲ ကျောင်းဆောင်
__label__O ပဲ ကျောင်းဆောင် ထဲ
__label__O ကျောင်းဆောင် ထဲ က
__label__O ထဲ က အပျိုစင်
__label__O က အပျိုစင် နတ်
__label__O အပျိုစင် နတ် ဘုရား
__label__O နတ် ဘုရား အသီးနား
__label__O ဘုရား အသီးနား ရဲ့
__label__O အသီးနား ရဲ့ ရုပ်
__label__O ရဲ့ ရုပ် ထု
__label__O ရုပ် ထု ရှေ့
__label__O ထု ရှေ့ မှာ
__label__O ရှေ့ မှာ ပဲ
__label__O မှာ ပဲ မက်ဒူးဆာ
__label__O ပဲ မက်ဒူးဆာ ကို
__label__O မက်ဒူးဆာ ကို အနိုင်
__label__O ကို အနိုင် အထက်
__label__O အနိုင် အထက် ပြု
__label__O အထက် ပြု လို့မယား
__label__O ပြု လို့မယား အဖြစ်
__label__O လို့မယား အဖြစ် သိမ်းပိုက်
__label__O အဖြစ် သိမ်းပိုက် လိုက်
__label__O သိမ်းပိုက် လိုက် ပါ
__label__O လိုက် ပါ လေ
__label__E ပါ လေ တယ်
__label__O နောက် မှ ကော်ဖီ
__label__O မှ ကော်ဖီ ဖြစ်
__label__O ကော်ဖီ ဖြစ် ဖြစ်
__label__O ဖြစ် ဖြစ် တစ်
__label__O ဖြစ် တစ် ခွက်
__label__O တစ် ခွက် လောက်
__label__O ခွက် လောက် သောက်
__label__O လောက် သောက် ကြ
__label__E သောက် ကြ ရအောင်
__label__O နေ့ တိုင်း အသား
__label__O တိုင်း အသား ပဲ
__label__O အသား ပဲ စား
__label__O ပဲ စား နေ
__label__O စား နေ ရ
__label__O နေ ရ တော့
__label__O ရ တော့ အခု
__label__O တော့ အခု ဆို
__label__O အခု ဆို ငြီးငွေ့
__label__O ဆို ငြီးငွေ့ လာ
__label__E ငြီးငွေ့ လာ ပြီ
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$
```

## Preparing Labeled Data for the Sentence Level Dataset

for train-valid dataset:  

```
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ perl ./change-ngram-label.pl ./train-valid.sent.my 2 > ./train-valid.sent.my.2gram
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ perl ./change-ngram-label.pl ./train-valid.sent.my 3 > ./train-valid.sent.my.3gram
```

for test dataset:  

```
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ perl ./change-ngram-label.pl ./test.sent.my 2 > ./test.sent.my.2gram
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ perl ./change-ngram-label.pl ./test.sent.my 3 > ./test.sent.my.3gram
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$
```

Check the filesize:  

```
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ wc *.2gram
   58910   176730  2351938 test.sent.my.2gram
  533442  1600326 21323463 train-valid.sent.my.2gram
  592352  1777056 23675401 total
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ wc *.3gram
   54226   216904  2966031 test.sent.my.3gram
  491385  1965540 26913648 train-valid.sent.my.3gram
  545611  2182444 29879679 total
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ 
```

## Training/Testing FastText Model for 2gram Sentences

အရင်ဆုံး memory များတဲ့ server ပေါ်ကို အထက်မှာပြင်ဆင်ခဲ့တဲ့ ဒေတာတွေကို copy ကူးပြီး ပြင်ဆင်ခဲ့ ....  

```
(base) yekyaw.thu@gpu:~/exp/mySent/data$ cp ./pre-process/*.2gram ./sent/
(base) yekyaw.thu@gpu:~/exp/mySent/data$ cp ./pre-process/*.3gram ./sent/
(base) yekyaw.thu@gpu:~/exp/mySent/data$ cd ./sent/
(base) yekyaw.thu@gpu:~/exp/mySent/data/sent$ ls
test.sent.my.2gram  test.sent.my.3gram	train-valid.sent.my.2gram  train-valid.sent.my.3gram
(base) yekyaw.thu@gpu:~/exp/mySent/data/sent$ 
```

Training with 2-gram model with default parameters for sentence level data:  

```
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext supervised -input ../data/sent/train-valid.sent.my.2gram -output sent-model-default
Read 2M words
Number of words:  30615
Number of labels: 2
Progress: 100.0% words/sec/thread:  682820 lr:  0.000000 avg.loss:  0.099836 ETA:   0h 0m 0s

real	0m2.660s
user	0m16.577s
sys	0m0.136s
(base) yekyaw.thu@gpu:~/exp/mySent/model$ 
```

testing ...  

```(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext test ./sent-model-default.bin ../data/sent/test.sent.my.2gram 
N	58910
P@1	0.97
R@1	0.97

real	0m0.073s
user	0m0.065s
sys	0m0.008s
(base) yekyaw.thu@gpu:~/exp/mySent/model$ 
```

Let's make evaluation in details ...  

```
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext test-label ./sent-model-default.bin ../data/sent/test.sent.my.2gram 
F1-Score : 0.983509  Precision : 0.981046  Recall : 0.985985   __label__O
F1-Score : 0.802859  Precision : 0.827703  Recall : 0.779462   __label__E
N	58910
P@1	0.970
R@1	0.970

real	0m0.073s
user	0m0.069s
sys	0m0.004s
(base) yekyaw.thu@gpu:~/exp/mySent/model$
```

## Training/Testing FastText Model for 3-gram Sentences

Training ...  

```
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext supervised -input ../data/sent/train-valid.sent.my.3gram -output sent-model-3gram-default
Read 2M words
Number of words:  30529
Number of labels: 2
Progress: 100.0% words/sec/thread:  851138 lr:  0.000000 avg.loss:  0.109665 ETA:   0h 0m 0s

real	0m2.610s
user	0m15.145s
sys	0m0.104s
```

Testing ...  

```(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext test ./sent-model-3gram-default.bin ../data/sent/test.sent.my.3gram 
N	54226
P@1	0.96
R@1	0.96

real	0m0.078s
user	0m0.074s
sys	0m0.004s
```

Testing with test-label ...  

```
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext test-label ./sent-model-3gram-default.bin ../data/sent/test.sent.my.3gram 
F1-Score : 0.978155  Precision : 0.975011  Recall : 0.981318   __label__O
F1-Score : 0.755316  Precision : 0.783613  Recall : 0.728990   __label__E
N	54226
P@1	0.960
R@1	0.960

real	0m0.078s
user	0m0.067s
sys	0m0.012s
(base) yekyaw.thu@gpu:~/exp/mySent/model$ 
```

အထက်ပါ ရလဒ်တွေကနေ အခြေခံအားဖြင့် ငါနားလည်တာက 2-gram က classification အတွက် အတော်ပဲ။  
3-gram ဖြစ်လာရင် decision making အတွက် noise ဖြစ်လာတယ်။  

## Playing Number of Epoch for 2-gram Model

2-gram model ကိုပဲ no. of epoch ကစားကြည့်ပြီး ရလဒ်က ဘယ်လောက်ထိ တက်လာနိုင်သလဲ ဆိုတာကို confirmation လုပ်ကြည့်ခဲ့တယ်။  

for epoch=5 ...  

```
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext supervised -input ../data/sent/train-valid.sent.my.2gram -output sent-model-2gram-tmp -epoch 5
Read 2M words
Number of words:  30615
Number of labels: 2
Progress: 100.0% words/sec/thread:  682484 lr:  0.000000 avg.loss:  0.099706 ETA:   0h 0m 0s

real	0m2.710s
user	0m16.209s
sys	0m0.108s
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext test-label ./sent-model-2gram-tmp.bin ../data/sent/test.sent.my.2gram
F1-Score : 0.983390  Precision : 0.981448  Recall : 0.985339   __label__O
F1-Score : 0.802797  Precision : 0.822108  Recall : 0.784372   __label__E
N	58910
P@1	0.969
R@1	0.969

real	0m0.075s
user	0m0.071s
sys	0m0.004s
(base) yekyaw.thu@gpu:~/exp/mySent/model$ 
```

for epoch=10 ...  

```
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext supervised -input ../data/sent/train-valid.sent.my.2gram -output sent-model-2gram-tmp -epoch 10
Read 2M words
Number of words:  30615
Number of labels: 2
Progress: 100.0% words/sec/thread:  710068 lr:  0.000000 avg.loss:  0.095963 ETA:   0h 0m 0s

real	0m4.539s
user	0m31.060s
sys	0m0.132s
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext test-label ./sent-model-2gram-tmp.bin ../data/sent/test.sent.my.2gram
F1-Score : 0.983299  Precision : 0.980737  Recall : 0.985874   __label__O
F1-Score : 0.800088  Precision : 0.825909  Recall : 0.775833   __label__E
N	58910
P@1	0.969
R@1	0.969

real	0m0.079s
user	0m0.070s
sys	0m0.009s
(base) yekyaw.thu@gpu:~/exp/mySent/model$ 
```

for epoch=15 ...  

```
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext supervised -input ../data/sent/train-valid.sent.my.2gram -output sent-model-2gram-tmp -epoch 15
Read 2M words
Number of words:  30615
Number of labels: 2
Progress: 100.0% words/sec/thread:  700785 lr:  0.000000 avg.loss:  0.094026 ETA:   0h 0m 0s

real	0m5.330s
user	0m45.895s
sys	0m0.172s
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext test-label ./sent-model-2gram-tmp.bin ../data/sent/test.sent.my.2gram
F1-Score : 0.983099  Precision : 0.980907  Recall : 0.985302   __label__O
F1-Score : 0.798685  Precision : 0.820536  Recall : 0.777968   __label__E
N	58910
P@1	0.969
R@1	0.969

real	0m0.078s
user	0m0.066s
sys	0m0.013s
(base) yekyaw.thu@gpu:~/exp/mySent/model$ 
```

for epoch=20 ...  

```
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext supervised -input ../data/sent/train-valid.sent.my.2gram -output sent-model-2gram-tmp -epoch 20
Read 2M words
Number of words:  30615
Number of labels: 2
Progress: 100.0% words/sec/thread:  710204 lr:  0.000000 avg.loss:  0.094504 ETA:   0h 0m 0s

real	0m6.528s
user	1m0.864s
sys	0m0.192s
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext test-label ./sent-model-2gram-tmp.bin ../data/sent/test.sent.my.2gram
F1-Score : 0.983179  Precision : 0.980133  Recall : 0.986243   __label__O
F1-Score : 0.797342  Precision : 0.828348  Recall : 0.768574   __label__E
N	58910
P@1	0.969
R@1	0.969

real	0m0.077s
user	0m0.072s
sys	0m0.004s
(base) yekyaw.thu@gpu:~/exp/mySent/model$
```

for epoch=25 ...

```
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext supervised -input ../data/sent/train-valid.sent.my.2gram -output sent-model-2gram-tmp -epoch 25
Read 2M words
Number of words:  30615
Number of labels: 2
Progress: 100.0% words/sec/thread:  715853 lr:  0.000000 avg.loss:  0.091941 ETA:   0h 0m 0s

real	0m7.709s
user	1m15.622s
sys	0m0.208s
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext test-label ./sent-model-2gram-tmp.bin ../data/sent/test.sent.my.2gram
F1-Score : 0.983238  Precision : 0.981018  Recall : 0.985468   __label__O
F1-Score : 0.800263  Precision : 0.822443  Recall : 0.779249   __label__E
N	58910
P@1	0.969
R@1	0.969

real	0m0.078s
user	0m0.073s
sys	0m0.004s
(base) yekyaw.thu@gpu:~/exp/mySent/model$ 
```

for epoch=30 ...  

```
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext supervised -input ../data/sent/train-valid.sent.my.2gram -output sent-model-2gram-tmp -epoch 30
Read 2M words
Number of words:  30615
Number of labels: 2
Progress: 100.0% words/sec/thread:  719799 lr:  0.000000 avg.loss:  0.091004 ETA:   0h 0m 0s

real	0m8.900s
user	1m28.987s
sys	0m0.232s
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext test-label ./sent-model-2gram-tmp.bin ../data/sent/test.sent.my.2gram
F1-Score : 0.983531  Precision : 0.981931  Recall : 0.985136   __label__O
F1-Score : 0.805353  Precision : 0.821167  Recall : 0.790137   __label__E
N	58910
P@1	0.970
R@1	0.970

real	0m0.077s
user	0m0.069s
sys	0m0.008s
(base) yekyaw.thu@gpu:~/exp/mySent/model$ 
```

for epoch=35 ...  

```
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext supervised -input ../data/sent/train-valid.sent.my.2gram -output sent-model-2gram-tmp -epoch 35
Read 2M words
Number of words:  30615
Number of labels: 2
Progress: 100.0% words/sec/thread:  714253 lr:  0.000000 avg.loss:  0.090842 ETA:   0h 0m 0s

real	0m10.192s
user	1m44.749s
sys	0m0.288s
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext test-label ./sent-model-2gram-tmp.bin ../data/sent/test.sent.my.2gram
F1-Score : 0.983341  Precision : 0.981022  Recall : 0.985671   __label__O
F1-Score : 0.801229  Precision : 0.824486  Recall : 0.779249   __label__E
N	58910
P@1	0.969
R@1	0.969

real	0m0.075s
user	0m0.067s
sys	0m0.008s
(base) yekyaw.thu@gpu:~/exp/mySent/model$ 
```

for epoch=40 ...  

```
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext supervised -input ../data/sent/train-valid.sent.my.2gram -output sent-model-2gram-tmp -epoch 40
Read 2M words
Number of words:  30615
Number of labels: 2
Progress: 100.0% words/sec/thread:  710179 lr:  0.000000 avg.loss:  0.090572 ETA:   0h 0m 0s

real	0m11.538s
user	2m0.216s
sys	0m0.276s
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext test-label ./sent-model-2gram-tmp.bin ../data/sent/test.sent.my.2gram
F1-Score : 0.983383  Precision : 0.982352  Recall : 0.984417   __label__O
F1-Score : 0.805057  Precision : 0.815098  Recall : 0.795260   __label__E
N	58910
P@1	0.969
R@1	0.969

real	0m0.076s
user	0m0.072s
sys	0m0.004s
(base) yekyaw.thu@gpu:~/exp/mySent/model$
```

for epoch=45 ...  

```(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext supervised -input ../data/sent/train-valid.sent.my.2gram -output sent-model-2gram-tmp -epoch 45
Read 2M words
Number of words:  30615
Number of labels: 2
Progress: 100.0% words/sec/thread:  713455 lr:  0.000000 avg.loss:  0.088769 ETA:   0h 0m 0s

real	0m12.840s
user	2m14.916s
sys	0m0.324s
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext test-label ./sent-model-2gram-tmp.bin ../data/sent/test.sent.my.2gram
F1-Score : 0.983581  Precision : 0.982288  Recall : 0.984878   __label__O
F1-Score : 0.806721  Precision : 0.819423  Recall : 0.794406   __label__E
N	58910
P@1	0.970
R@1	0.970

real	0m0.078s
user	0m0.070s
sys	0m0.009s
(base) yekyaw.thu@gpu:~/exp/mySent/model$
```

for epoch=50 ...  

```
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext supervised -input ../data/sent/train-valid.sent.my.2gram -output sent-model-2gram-tmp -epoch 50
Read 2M words
Number of words:  30615
Number of labels: 2
Progress: 100.0% words/sec/thread:  715935 lr:  0.000000 avg.loss:  0.089110 ETA:   0h 0m 0s

real	0m13.950s
user	2m29.672s
sys	0m0.360s
(base) yekyaw.thu@gpu:~/exp/mySent/model$ time ../../../tool/fastText/fasttext test-label ./sent-model-2gram-tmp.bin ../data/sent/test.sent.my.2gram
F1-Score : 0.983103  Precision : 0.981260  Recall : 0.984952   __label__O
F1-Score : 0.799651  Precision : 0.817857  Recall : 0.782237   __label__E
N	58910
P@1	0.969
R@1	0.969

real	0m0.078s
user	0m0.062s
sys	0m0.016s
(base) yekyaw.thu@gpu:~/exp/mySent/model$ 
```

အထက်ပါ playing with no. of epoch experiment ကနေ တွေ့ရတာက epoch 35, 45 ကပဲ ရလဒ် အပြောင်းအလဲ ဖြစ်တယ်။ ပိုကောင်းလာတယ်။ တကယ်ကတော့ အများကြီး အပြောင်းအလဲတော့ မဟုတ်ပေမဲ့ ....  
လက်ရှိ အချိန်အထိ Precision, Recall အကောင်းဆုံးက 97.  

## To Do

paragraph level အတွက် စမ်းချင်တယ်။  

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
