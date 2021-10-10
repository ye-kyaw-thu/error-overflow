# LePoD Measuring for Myanmar Paraphrases

Link: [https://github.com/xingniu/multitask-ft-fsmt/tree/master/LePoD](https://github.com/xingniu/multitask-ft-fsmt/tree/master/LePoD)  
အထက်ပါ ဖိုင်တွေကို တစ်ဖိုင်ချင်း ကိုယ့်စက်ထဲကို copy ကူးထည့်ပြီးသွားတဲ့အခါမှာ အောက်ပါအတိုင်း file တွေကို တွေ့ရလိမ့်မယ်။  

```
(base) ye@:~/exp/LePoD$ ls
example.sh  lepod.png  lepod-score.py  README.md  setup.sh
(base) ye@:~/exp/LePoD$ 
```

## Run setup.sh

LePoD က moses scripts တွေနဲ့ meteor-1.5 ကို သုံးတာမို့ အဲဒါတွေက ကိုယ့်စက်ထဲမှာ မရှိသေးရင် install လုပ်ဖို့ လုပ်အပ်တယ်။  
အဲဒီအတွက် steup.sh ကို ပြင်ပေးထားတာမို့ အဲဒီ shell script ကို run ပေးရပါမယ်။  
(တကယ်လို့ ကိုယ့်စက်ထဲမှာ moses scripts တို့ meteor-1.5 တွေကရှိပြီးသားဆိုရင်တော့ example.sh မှာ path ကို ဝင်ပြင်ပေးပြီး run ရင်လည်း ရပါတယ်)  

```
(base) ye@:~/exp/LePoD$ bash ./setup.sh 
Cloning into 'mosesdecoder'...
remote: Enumerating objects: 148070, done.
remote: Counting objects: 100% (498/498), done.
remote: Compressing objects: 100% (206/206), done.
remote: Total 148070 (delta 315), reused 433 (delta 289), pack-reused 147572
Receiving objects: 100% (148070/148070), 129.86 MiB | 14.72 MiB/s, done.
Resolving deltas: 100% (114341/114341), done.
Note: switching to '06f519d'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 06f519d4e Handle glottal stops in Somalian
--2021-10-10 10:17:20--  http://www.cs.cmu.edu/~alavie/METEOR/download/meteor-1.5.tar.gz
Resolving www.cs.cmu.edu (www.cs.cmu.edu)... 128.2.42.95
Connecting to www.cs.cmu.edu (www.cs.cmu.edu)|128.2.42.95|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 223646468 (213M) [application/x-gzip]
Saving to: ‘meteor-1.5.tar.gz’

meteor-1.5.tar.gz                     100%[=========================================================================>] 213.29M   119KB/s    in 26m 48s 

2021-10-10 10:44:09 (136 KB/s) - ‘meteor-1.5.tar.gz’ saved [223646468/223646468]

(base) ye@:~/exp/LePoD$ 

```

## Updating example.sh

"file_1", "file_2" နဲ့ "work_dir "ဆိုတဲ့ variable သုံးခုကို comment ပိတ်ခဲ့တယ်။  
ဘာကြောင့်လည်း ဆိုတော့ "file_1", "file_2" က segmentation မလုပ်ထားရသေးတဲ့ input ဖိုင်တွေ ဖြစ်ပြီး မြန်မာစာအတွက်က တော့ myWord နဲ့ ဖြစ်ဖြစ် သို့မဟုတ်  
manual word segmentation လုပ်ထားပြီးသားလို့ ယူဆပြီး သွားမှာမို့ "file_1", "file_2" variable နှစ်ခုက မလိုအပ်လို့...   
ပြီးတော့ "work_dir" ဆိုတဲ့ variable ကိုလည်း run ရတာ အဆင်ပြေဖို့အတွက် command line argument ကနေပဲ ပေးလိုက်ချင်လို့...  

```bash
#file_1=$root_dir/experiments/osi-tag-translation-unk-transfer/decode-1/perplexity/test_1.trans.detok 
#file_2=$root_dir/experiments/osi-tag-translation-unk-transfer/decode-1/perplexity/test_2.trans.detok 
#work_dir=$root_dir/LePoD/score
```

ပြီးတော့ lepod ဆိုတဲ့ variable ကိုလည်း ကိုယ့်စက်ထဲမှာ LePoD ကို installation လုပ်ထားတဲ့ path နဲ့ အစားထိုးချင်လို့ အောက်ပါအတိုင်း update လုပ်ခဲ့...  

```
#lepod=$root_dir/LePoD/lepod-score.py
lepod=/home/ye/exp/LePoD/lepod-score.py
```

ပြီးတော့ "input_1", "input_2", "work_dir", "output" variable တွေကို command line argument ကနေပဲ ယူဖတ်ပြီး assignment လုပ်ဖို့အတွက်  
အောက်ပါအတိုင်း example.sh ပရိုဂရမ်ကို update လုပ်ခဲ့...  

```
input_1=$1;
input_2=$2;
work_dir=$3;
output=$4;

mkdir -p $work_dir
#input_1=$work_dir/input_1.tok
#input_2=$work_dir/input_2.tok
#output=$work_dir/score
```

moses ရဲ့ tokenizer.perl ကို သုံးပြီးတော့ word segmentation လုပ်တာကလည်း မြန်မာစာအတွက်က မလိုအပ်လို့ comment ပိတ်ခဲ့...  

```
#$moses_scripts_path/tokenizer/tokenizer.perl -l $lang_base -a -no-escape -q < $file_1 > $input_1
#$moses_scripts_path/tokenizer/tokenizer.perl -l $lang_base -a -no-escape -q < $file_2 > $input_2
```

တကယ်လို့ moses script တွေထဲကနေမှ tokenizer.perl ကိုပဲ ယူသုံးတာဆိုရင်တော့ setup.sh ကိုပါ ဝင်ပြင်ပြီး moses-scripts တွေကို install မလုပ်အောင်လည်း လုပ်လို့ ရတယ်။  

## Preparing Paraphrase Data for Myanmar Language

data ရှိတဲ့ folder ကနေ LePoD measuring experiment လုပ်မယ့် folder အောက်ကို copy ကူးယူခဲ့...  

```
(base) ye@:~/exp/myPara3/data/original$ cp train.txt /home/ye/exp/LePoD/mypara-data/
```

ကော်ပီကူးလာတဲ့ paraphrasing ဒေတာကို check လုပ်ခဲ့...  

```
(base) ye@:~/exp/LePoD/mypara-data$ wc train.txt 
  40461  764288 8442342 train.txt
(base) ye@:~/exp/LePoD/mypara-data$ head train.txt 
ကျွန်တော် စီး ဖို့ ချစ် စရာ ဖိနပ် တစ် ရံ ကို ရှာ မ တွေ့ လို့ ပါ ။	တစ်ခါတစ်ခါ ကျွန်တော် က ခင်ဗျား ကို အရမ်း အပြောင်းအလဲ များ တဲ့ လူ လို့ ထင် မိ တယ် ။	0
ကျေးဇူး ပဲ ၊ ကျွန်တော် ဘယ်လောက် ပေး ရ မ လဲ ။	ကျေးဇူး နော် ၊ ဘယ် တော့ ပြန် တွေ့ ကြ မ လဲ ။	0
ကျေးဇူး အများကြီး တင် ပါ တယ် ။	ကျေးဇူးတင် တယ် လို့ မ ပြော သွား ဘူး ။	0
ကျောင်းအုပ်ကြီး က တော် တဲ့ ကျောင်းသား တွေ ကို ချီးကျူး ကြ တယ် ။	ကျောင်းအုပ်ကြီး က ဆိုး တဲ့ ကျောင်းသား တွေ ကို ဒဏ် ပေး ကြ တယ် ။	0
 ကောင်း ပြီ ကျွန်တော် လုပ် ပါ့ မယ် ။	ကောင်း ပြီ ကျွန်တော် ဒီ အလုပ် ကို လက် မ ခံ တော့ ဘူး ။	0
 ကောင်း သော ည ပါ ။	ကောင်း သော နေ့ ပါ ။	0
ကောင် လေး က လူ ကြီး ကို ရှင်းရှင်းလင်းလင်း မြင် နေ တယ် ။	သာယာ တဲ့ နေ့ က လေး ပါ ပဲ ။	0
ခဏ အကြာ မှာ ကျွန်တော် ခင်ဗျား ကို ပြန် ဆက် ပါ ရ စေ ။	ခဏ ကြာ တော့ သူ မ တည်ငြိမ် စ ပြု လာ ပြီး သူ ပြော တာ ကို နားထောင် နေ တော့ တယ် ။	0
ခေါင်မိုး ပေါ် မှာ ကြောင် တစ် ကောင် ရှိ တယ် ။	အတန်း လွတ် သွား မှာ စိုး တယ် ။	0
ငါ ခိုင်း တာ မင်း လုပ် ခဲ့ လား ။	ဒါ က အသစ် တပ်ဆင် မှာ ဖြစ် တယ် ။	0
(base) ye@:~/exp/LePoD/mypara-data$ 
```

စာကြောင်းရေ နည်းနည်းလျှော့ပြီး စမ်းဖို့အတွက် အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့...  

```
(base) ye@:~/exp/LePoD/mypara-data$ head -n 10000 ./train.txt > 10k-mypara.txt
(base) ye@:~/exp/LePoD/mypara-data$ wc 10k-mypara.txt 
  10000  189255 2165478 10k-mypara.txt
```

input လုပ်မယ့် ဖိုင် နှစ်ဖိုင် အဖြစ် ခွဲခဲ့...  

```
(base) ye@:~/exp/LePoD/mypara-data$ cut -f1 ./10k-mypara.txt > para1
(base) ye@:~/exp/LePoD/mypara-data$ cut -f2 ./10k-mypara.txt > para2
(base) ye@:~/exp/LePoD/mypara-data$ head para1
ကျွန်တော် စီး ဖို့ ချစ် စရာ ဖိနပ် တစ် ရံ ကို ရှာ မ တွေ့ လို့ ပါ ။
ကျေးဇူး ပဲ ၊ ကျွန်တော် ဘယ်လောက် ပေး ရ မ လဲ ။
ကျေးဇူး အများကြီး တင် ပါ တယ် ။
ကျောင်းအုပ်ကြီး က တော် တဲ့ ကျောင်းသား တွေ ကို ချီးကျူး ကြ တယ် ။
 ကောင်း ပြီ ကျွန်တော် လုပ် ပါ့ မယ် ။
 ကောင်း သော ည ပါ ။
ကောင် လေး က လူ ကြီး ကို ရှင်းရှင်းလင်းလင်း မြင် နေ တယ် ။
ခဏ အကြာ မှာ ကျွန်တော် ခင်ဗျား ကို ပြန် ဆက် ပါ ရ စေ ။
ခေါင်မိုး ပေါ် မှာ ကြောင် တစ် ကောင် ရှိ တယ် ။
ငါ ခိုင်း တာ မင်း လုပ် ခဲ့ လား ။
(base) ye@:~/exp/LePoD/mypara-data$ head para2
တစ်ခါတစ်ခါ ကျွန်တော် က ခင်ဗျား ကို အရမ်း အပြောင်းအလဲ များ တဲ့ လူ လို့ ထင် မိ တယ် ။
ကျေးဇူး နော် ၊ ဘယ် တော့ ပြန် တွေ့ ကြ မ လဲ ။
ကျေးဇူးတင် တယ် လို့ မ ပြော သွား ဘူး ။
ကျောင်းအုပ်ကြီး က ဆိုး တဲ့ ကျောင်းသား တွေ ကို ဒဏ် ပေး ကြ တယ် ။
ကောင်း ပြီ ကျွန်တော် ဒီ အလုပ် ကို လက် မ ခံ တော့ ဘူး ။
ကောင်း သော နေ့ ပါ ။
သာယာ တဲ့ နေ့ က လေး ပါ ပဲ ။
ခဏ ကြာ တော့ သူ မ တည်ငြိမ် စ ပြု လာ ပြီး သူ ပြော တာ ကို နားထောင် နေ တော့ တယ် ။
အတန်း လွတ် သွား မှာ စိုး တယ် ။
ဒါ က အသစ် တပ်ဆင် မှာ ဖြစ် တယ် ။
(base) ye@:~/exp/LePoD/mypara-data$
```

path info က အောက်ပါအတိုင်း...  

```
  (base) ye@:~/exp/LePoD/mypara-data$ pwd
/home/ye/exp/LePoD/mypara-data
```

## Preparing work and score Folders

example.sh ကို ဝင်လေ့လာတဲ့အခါမှာ scoring လုပ်မယ့် ဖိုင်နှစ်ဖိုင်ကို parameter အဖြစ် ပေးရတဲ့အပြင် folder နှစ်ခုကိုလည်း ပြင်ဆင်ဖို့ လိုအပ်တာတွေ့ရလို့ ပြင်ဆင်ခဲ့...  

```
(base) ye@:~/exp/LePoD$ mkdir -p work1/score
(base) ye@:~/exp/LePoD$ tree work1
work1
└── score

1 directory, 0 files
(base) ye@:~/exp/LePoD$ 
```

## Running example.sh 

example.sh ကို ဝင်လေ့လာတော့ တကယ်တမ်း အဓိက လုပ်တာက အောက်ပါ statement နှစ်ကြောင်းပါ။  

```
java -Xmx2G -cp $meteor_jar Matcher $input_1.lc $input_2.lc -l $lang_base > $work_dir/alignment

python $lepod -l -d 4 -p "," -a $work_dir/alignment -f $input_1 $input_2 -r $output
```

အထက်မှာ မြင်ရတဲ့အတိုင်း meteor java ပရိုဂရမ်ကို သုံးပြီးတော့ string နှစ်ခုအကြား alignment လုပ်တာနဲ့...  
LePoD ရဲ့ python program ကို သုံးပြီးတော့ LePoD measure လုပ်သွားတဲ့ နှစ်ပိုင်းပါ။  

ပထမဆုံး run ကြည့်တော့ အောက်ပါအတိုင်း error ပေးတယ်...  

```
(base) ye@:~/exp/LePoD$ bash ./example.sh ./mypara-data/para1 ./mypara-data/para2 ./work1/ ./work1/score/ 
Traceback (most recent call last):
  File "/home/ye/exp/LePoD/lepod-score.py", line 108, in <module>
    substitution_score = (len(sub_tokens1)*1.0/len(raw_tokens1) + len(sub_tokens2)*1.0/len(raw_tokens2)) / 2
ZeroDivisionError: float division by zero
```

check the output folder:  

```
(base) ye@:~/exp/LePoD$ tree work1/
work1/
├── alignment
└── score

1 directory, 1 file
(base) ye@:~/exp/LePoD$
```

alignment ဖိုင်ကတော့ ရှိတာမို့ METEOR ကတော့ အလုပ်လုပ်ပေးတယ်...  

```
(base) ye@:~/exp/LePoD/work1$ head -n 30 ./alignment 
Alignment 1
ကျွန်တော် စီး ဖို့ ချစ် စရာ ဖိနပ် တစ် ရံ ကို ရှာ မ တွေ့ လို့ ပါ ။
တစ်ခါတစ်ခါ ကျွန်တော် က ခင်ဗျား ကို အရမ်း အပြောင်းအလဲ များ တဲ့ လူ လို့ ထင် မိ တယ် ။
Line2Start:Length	Line1Start:Length	Module		Score
1:1			0:1			0		1.0
4:1			8:1			0		1.0
10:1			12:1			0		1.0
14:1			14:1			0		1.0

Alignment 2
ကျေးဇူး ပဲ ၊ ကျွန်တော် ဘယ်လောက် ပေး ရ မ လဲ ။
ကျေးဇူး နော် ၊ ဘယ် တော့ ပြန် တွေ့ ကြ မ လဲ ။
Line2Start:Length	Line1Start:Length	Module		Score
2:1			2:1			0		1.0
8:1			7:1			0		1.0
9:1			8:1			0		1.0
10:1			9:1			0		1.0

Alignment 3
ကျေးဇူး အများကြီး တင် ပါ တယ် ။
ကျေးဇူးတင် တယ် လို့ မ ပြော သွား ဘူး ။
Line2Start:Length	Line1Start:Length	Module		Score
1:1			4:1			0		1.0
7:1			5:1			0		1.0

Alignment 4
ကျောင်းအုပ်ကြီး က တော် တဲ့ ကျောင်းသား တွေ ကို ချီးကျူး ကြ တယ် ။
ကျောင်းအုပ်ကြီး က ဆိုး တဲ့ ကျောင်းသား တွေ ကို ဒဏ် ပေး ကြ တယ် ။
Line2Start:Length	Line1Start:Length	Module		Score
1:1			1:1			0		1.0
(base) ye@:~/exp/LePoD/work1$ 
```

သေချာအောင်လို့ example.sh မှာ အောက်ပါအတိုင်းဝင် update လုပ်ပြီးတော့  
command line argument တွေကို မြင်ရအောင် လုပ်ခဲ့...  

```
echo "Info of command line arguments:" ;
echo "input_1: $input_1";
echo "input_2: $input_2";
echo "work_dir: $work_dir";
echo "output: $output";
```

example.sh ကို ထပ် run ကြည့်ခဲ့...  

```
(base) ye@:~/exp/LePoD$ bash ./example.sh ./mypara-data/para1 ./mypara-data/para2 ./work1/ ./work1/score/ 
Info of command line arguments:
input_1: ./mypara-data/para1
input_2: ./mypara-data/para2
work_dir: ./work1/
output: ./work1/score/
Traceback (most recent call last):
  File "/home/ye/exp/LePoD/lepod-score.py", line 108, in <module>
    substitution_score = (len(sub_tokens1)*1.0/len(raw_tokens1) + len(sub_tokens2)*1.0/len(raw_tokens2)) / 2
ZeroDivisionError: float division by zero
(base) ye@:~/exp/LePoD$
```

full path နဲ့ assign လုပ်ထားတာ မဟုတ်ပေမဲ့ command line argument တွေကတော့ passing လုပ်သွားတာကို အထက်ပါအတိုင်း confirm လုပ်ခဲ့...  

-v verbose mode ပါလို့ အသေးစိတ်မြင်ရမလား ဆိုပြီး example.sh မှာ အောက်ပါအတိုင်း ဝင်ပြင်ပြီးတော့ 

```
#python $lepod -l -d 4 -p "," -a $work_dir/alignment -f $input_1 $input_2 -r $output
python $lepod -p ",၊။" -a $work_dir/alignment -f $input_1 $input_2 -r $output -v
```

run ကြည့်ခဲ့တော့ ပြဿနာရဲ့ အကြောင်းအရင်းကိုတော့ တွေ့ရပြီ...  

```
(base) ye@:~/exp/LePoD$ bash ./example.sh ./mypara-data/para1 ./mypara-data/para2 ./work1/ ./work1/score/
...
...
...
====================================================================================================
    RAW-1	ခင်ဗျား နဲ့ တွေ့ ခဲ့ ရ လို့ ကျွန်တော် အရမ်း ဝမ်းသာ ပါ တယ် ။
    RAW-2	ခင်ဗျား နဲ့ တွေ့ ရ တာ စိတ် မ ချမ်းသာ ဘူး ။
MAT | SUB	ခင်ဗျား နဲ့ တွေ့ ရ | ခဲ့ လို့ ကျွန်တော် အရမ်း ဝမ်းသာ ပါ တယ်
MAT | SUB	ခင်ဗျား နဲ့ တွေ့ ရ | တာ စိတ် မ ချမ်းသာ ဘူး
6971	distortion-score=0.000   substitution-score=0.542
====================================================================================================
    RAW-1	ခင်ဗျား နဲ့ တွေ့ တာ ကျွန်တော့် အမေ က မ ကြိုက် ဘူး ။
    RAW-2	လမ်း ပေါ် မှာ ဆင် တစ် ကောင် လွတ် လာ တယ် ။
MAT | SUB	 | ခင်ဗျား နဲ့ တွေ့ တာ ကျွန်တော့် အမေ က မ ကြိုက် ဘူး
MAT | SUB	 | လမ်း ပေါ် မှာ ဆင် တစ် ကောင် လွတ် လာ တယ်
6972	distortion-score=0.000   substitution-score=0.905
====================================================================================================
    RAW-1	ခင်ဗျား နဲ့ ပြော ချင် လို့ ။
    RAW-2	သူ မ နဲ့ စကား ပြော ချင် လို့ ပါ ။
MAT | SUB	နဲ့ ပြော ချင် လို့ | ခင်ဗျား
MAT | SUB	နဲ့ ပြော ချင် လို့ | သူ မ စကား ပါ
6973	distortion-score=0.000   substitution-score=0.306
====================================================================================================
    RAW-1	ခင်ဗျား နဲ့ ပြော ချင် လို့ ။
    RAW-2	
Traceback (most recent call last):
  File "/home/ye/exp/LePoD/lepod-score.py", line 108, in <module>
    substitution_score = (len(sub_tokens1)*1.0/len(raw_tokens1) + len(sub_tokens2)*1.0/len(raw_tokens2)) / 2
ZeroDivisionError: float division by zero
(base) ye@:~/exp/LePoD$ 

```

line no. 6974 မှာ ပြဿနာဖြစ်နေတာမို့ ... cut မလုပ်ခင်က (i.e. para1, para2 ဖိုင် နှစ်ဖိုင်အဖြစ် မခွဲထုတ်ခင်က) ဖိုင်ကို print ထုတ်ကြည့်တော့ အောက်ပါအတိုင်း တွေ့ရ...  

```
(base) ye@:~/exp/LePoD/mypara-data$ sed -n '6973,6975p;' ./10k-mypara.txt 
ခင်ဗျား နဲ့ ပြော ချင် လို့ ။	သူ မ နဲ့ စကား ပြော ချင် လို့ ပါ ။	0
ခင်ဗျား နဲ့ ပြော ချင် လို့ ။		0
ခင်ဗျား ပင်ပန်း တာ ကျွန်တော် မ အံ့ဩ ဘူး ။	ခင်ဗျား ဒီ လောက် လုပ် ထား တာ မ ပင်ပန်း ဘူး လား ။	0
(base) ye@:~/exp/LePoD/mypara-data$ 
```

အဲဒါကြောင့် အဲဒီ လိုင်းကို ဖြုတ်၊ 10000 လိုင်းအတွက် တစ်ကြောင်းအသစ်ကို ပြန်ဖြည့်ပြီး cut ပြန်လုပ်ခဲ့...   
(စာကြောင်းဖျက်တာနဲ့ အသစ်ကော်ပီကူးထည့်တာကိုတော့ gedit text editor ကို သုံးပြီး manual လုပ်ခဲ့)

cutting for para1, para2 ကို အောက်ပါအတိုင်း လုပ်ခဲ့...  

```
(base) ye@:~/exp/LePoD/mypara-data$ rm para1
(base) ye@:~/exp/LePoD/mypara-data$ rm para2
(base) ye@:~/exp/LePoD/mypara-data$ cut -f1 ./10k-mypara.txt > para1
(base) ye@:~/exp/LePoD/mypara-data$ cut -f2 ./10k-mypara.txt > para2
```

ထပ် run ကြည့်ခဲ့...  

```
(base) ye@:~/exp/LePoD$ bash ./example.sh ./mypara-data/para1 ./mypara-data/para2 ./work1/ ./work1/score/ 2>&1 | tee running.log
...
...
...
====================================================================================================
    RAW-1	ငါ သူ့ အပေါ် ထား တဲ့ မေတ္တာ တရား တွေ ခြောက် ခန်း ပြီ ။
    RAW-2	ငါ သူ့ အပေါ် ထား တဲ့ မေတ္တာ တရား တွေ ကုန် ပြီ ။
MAT | SUB	ငါ သူ့ အပေါ် ထား တဲ့ မေတ္တာ တရား တွေ ပြီ | ခြောက် ခန်း
MAT | SUB	ငါ သူ့ အပေါ် ထား တဲ့ မေတ္တာ တရား တွေ ပြီ | ကုန်
9987	distortion-score=0.000   substitution-score=0.129
====================================================================================================
    RAW-1	ငါ သူ့ အပေါ် ထား တဲ့ မေတ္တာ တရား တွေ ခြောက် ခန်း ပြီ ။
    RAW-2	သူ့ အပေါ် ထား တဲ့ ချစ် ခြင်း မေတ္တာ တွေ ပိုမို တိုးပွား လာ နေ ပြီ ။
MAT | SUB	သူ့ အပေါ် ထား တဲ့ မေတ္တာ တွေ ပြီ | ငါ တရား ခြောက် ခန်း
MAT | SUB	သူ့ အပေါ် ထား တဲ့ မေတ္တာ တွေ ပြီ | ချစ် ခြင်း ပိုမို တိုးပွား လာ နေ
9988	distortion-score=0.000   substitution-score=0.381
====================================================================================================
    RAW-1	ငါ သူ့ အပေါ် ထား တဲ့ မေတ္တာ တရား တွေ ခြောက် ခန်း ပြီ ။
    RAW-2	သူ့ အပေါ် ထား တဲ့ ငါ့ မေတ္တာ တွေ က သိပ် ကို ကြီးမား တယ် ။
MAT | SUB	သူ့ အပေါ် ထား တဲ့ မေတ္တာ တွေ | ငါ တရား ခြောက် ခန်း ပြီ
MAT | SUB	သူ့ အပေါ် ထား တဲ့ မေတ္တာ တွေ | ငါ့ က သိပ် ကို ကြီးမား တယ်
9989	distortion-score=0.000   substitution-score=0.439
====================================================================================================
    RAW-1	ငါ သူ့ အပေါ် ထား တဲ့ မေတ္တာ တရား တွေ ခြောက် ခန်း ပြီ ။
    RAW-2	ငါ သူ့ အပေါ် ထား တဲ့ မေတ္တာ တရား တွေ ကုန် ခန်း ပြီ ။
MAT | SUB	ငါ သူ့ အပေါ် ထား တဲ့ မေတ္တာ တရား တွေ ခန်း ပြီ | ခြောက်
MAT | SUB	ငါ သူ့ အပေါ် ထား တဲ့ မေတ္တာ တရား တွေ ခန်း ပြီ | ကုန်
9990	distortion-score=0.000   substitution-score=0.083
====================================================================================================
    RAW-1	ငါ သူ့ အိမ် သွား တယ် ၊ ဒါပေမဲ့ သူ အိမ် မှာ မ ရှိ ဘူး ။
    RAW-2	ငါ သူ့ အိမ် သွား ပြီး သူ နဲ့ စကား တွေ ပြော ခဲ့ တယ် ။
MAT | SUB	ငါ သူ့ အိမ် သွား တယ် သူ | ၊ ဒါပေမဲ့ အိမ် မှာ မ ရှိ ဘူး
MAT | SUB	ငါ သူ့ အိမ် သွား သူ တယ် | ပြီး နဲ့ စကား တွေ ပြော ခဲ့
9991	distortion-score=0.167   substitution-score=0.481
====================================================================================================
    RAW-1	ငါ သူ့ ကို ကျောင်း မှာ စာသင် တယ် ။
    RAW-2	ခင်ဗျား ဘာ တွေ ကြိုးစား မ လဲ ။
MAT | SUB	 | ငါ သူ့ ကို ကျောင်း မှာ စာသင် တယ်
MAT | SUB	 | ခင်ဗျား ဘာ တွေ ကြိုးစား မ လဲ
9992	distortion-score=0.000   substitution-score=0.866
====================================================================================================
    RAW-1	ငါ သူ့ ကို တွေ့ ချင် လှ ပြီ ။
    RAW-2	အဲဒါ ကို စား စား မ စား စား ။
MAT | SUB	ကို | ငါ သူ့ တွေ့ ချင် လှ ပြီ
MAT | SUB	ကို | အဲဒါ စား စား မ စား စား
9993	distortion-score=0.000   substitution-score=0.750
====================================================================================================
    RAW-1	ငါ့ သူငယ်ချင်း က သူ ဂီတ အကြောင်း အများကြီး သိ တာ ကို ကြွားဝါ ရ တာ ကြိုက် တယ် ။
    RAW-2	ငါ့ သူငယ်ချင်း က သူ ဂီတ အကြောင်း အများကြီး သိ တာ ကို ကြွား ရ တာ ကြိုက် တယ် ။
MAT | SUB	ငါ့ သူငယ်ချင်း က သူ ဂီတ အကြောင်း အများကြီး သိ တာ ကို ရ တာ ကြိုက် တယ် | ကြွားဝါ
MAT | SUB	ငါ့ သူငယ်ချင်း က သူ ဂီတ အကြောင်း အများကြီး သိ တာ ကို ရ တာ ကြိုက် တယ် | ကြွား
9994	distortion-score=0.000   substitution-score=0.062
====================================================================================================
    RAW-1	ငါ့ သူငယ်ချင်း ကို မ ယုံ ဘူး လား ။
    RAW-2	ဟို က မင်း ရဲ့ သူငယ်ချင်း ဟာ လည်း ငါ့ သား ပဲ ဖြစ် တယ် ဆို တာ က တော့ အတွင်း ရေး လျှို့ဝှက် ချက် ပဲ ပေါ့ ။
MAT | SUB	ငါ့ သူငယ်ချင်း | ကို မ ယုံ ဘူး လား
MAT | SUB	သူငယ်ချင်း ငါ့ | ဟို က မင်း ရဲ့ ဟာ လည်း သား ပဲ ဖြစ် တယ် ဆို တာ က တော့ အတွင်း ရေး လျှို့ဝှက် ချက် ပဲ ပေါ့
9995	distortion-score=0.500   substitution-score=0.747
====================================================================================================
    RAW-1	ငါ သူ တို့ ကို ပေး ရ မှာ လား ။
    RAW-2	အလုပ် ကောင်း ကောင်း ရ ရှိ ဖို့ ခင်ဗျား ဘယ်လို ကြိုးစား မ လဲ ။
MAT | SUB	ရ | ငါ သူ တို့ ကို ပေး မှာ လား
MAT | SUB	ရ | အလုပ် ကောင်း ကောင်း ရှိ ဖို့ ခင်ဗျား ဘယ်လို ကြိုးစား မ လဲ
9996	distortion-score=0.000   substitution-score=0.806
====================================================================================================
    RAW-1	ငါ သူ တို့ ကို လုပ် ခိုင်း တာ ကို သူ တို့ လုပ် လိမ့် မယ် ။
    RAW-2	ငါ့ အမေ အသက် က ၆၀ ရှိ ပြီ ။
MAT | SUB	 | ငါ သူ တို့ ကို လုပ် ခိုင်း တာ ကို သူ တို့ လုပ် လိမ့် မယ်
MAT | SUB	 | ငါ့ အမေ အသက် က ၆၀ ရှိ ပြီ
9997	distortion-score=0.000   substitution-score=0.902
====================================================================================================
    RAW-1	ငါ သူ တို့ နဲ့ ဘယ် တုန်း က မှ မ ပတ်သက် ဘူး ။
    RAW-2	ငါ့ ကို ယုံ ပါ ။
MAT | SUB	 | ငါ သူ တို့ နဲ့ ဘယ် တုန်း က မှ မ ပတ်သက် ဘူး
MAT | SUB	 | ငါ့ ကို ယုံ ပါ
9998	distortion-score=0.000   substitution-score=0.858
====================================================================================================
    RAW-1	ငါ သူ မ ကို ထား ခဲ့ မယ် လို့ မင်း ထင် သလား ။
    RAW-2	ငါ သူ မ ကို ခေါ် ခဲ့ လိမ့် မယ် လို့ မင်း ထင် သလား ။
MAT | SUB	ငါ သူ မ ကို ခဲ့ မယ် လို့ မင်း ထင် သလား | ထား
MAT | SUB	ငါ သူ မ ကို ခဲ့ မယ် လို့ မင်း ထင် သလား | ခေါ် လိမ့်
9999	distortion-score=0.000   substitution-score=0.119
====================================================================================================
    RAW-1	ငါ သူ မ ကို ထား ခဲ့ မယ် လို့ မင်း ထင် သလား ။
    RAW-2	နောက် တစ် ခု ဘယ်လို သဘော ရ သလဲ ။
MAT | SUB	 | ငါ သူ မ ကို ထား ခဲ့ မယ် လို့ မင်း ထင် သလား
MAT | SUB	 | နောက် တစ် ခု ဘယ်လို သဘော ရ သလဲ
10000	distortion-score=0.000   substitution-score=0.896
====================================================================================================
LeD=0.492
   min=0.000
   max=1.000
PoD=0.040
   min=0.000
   max=0.875
10000 pairs were read in total
   9977 pairs (99.77%) got non-zero LeD scores
   889 pairs (8.89%) got non-zero PoD scores
   11 pairs (0.11%) got all zero scores
```

run တာတော့ အဆင်ပြေသွားပြီ။  

-v ကိုဖြုတ်ပြီးလည်း run ကြည့်ခဲ့...  
ဒီ တစ်ခါတော့ alignment က လုပ်ထားပြီးသားမို့ python ဖိုင်ကိုပဲ တိုက်ရိုက် ခေါ် run ခဲ့...  

```
(base) ye@:~/exp/LePoD$ python ./lepod-score.py -p ",၊။" -a ./work1/alignment -f ./mypara-data/para1 ./mypara-data/para2 -r ./work1/score
LeD=0.492
   min=0.000
   max=1.000
PoD=0.040
   min=0.000
   max=0.875
10000 pairs were read in total
   9977 pairs (99.77%) got non-zero LeD scores
   889 pairs (8.89%) got non-zero PoD scores
   11 pairs (0.11%) got all zero scores
(base) ye@:~/exp/LePoD$ tree ./work1/
./work1/
├── alignment
├── score
├── score.led
└── score.pod

1 directory, 3 files
(base) ye@:~/exp/LePoD$ 
```

မြန်မာစာမို့လို့ -l (lowercase) နဲ့ -d (digit) တွေက မဆိုင်ဘူးလို့ ယူဆပေမဲ့ အဲဒီ parameter ကိုလည်း ထည့်ပြီး run ကြည့်ခဲ့...  

```
(base) ye@:~/exp/LePoD$ python ./lepod-score.py -l -d 4 -p ",၊။" -a ./work1/alignment -f ./mypara-data/para1 ./mypara-data/para2 -r ./work1/score
LeD=0.4924
   min=0.0000
   max=1.0000
PoD=0.0399
   min=0.0000
   max=0.8750
10000 pairs were read in total
   9977 pairs (99.77%) got non-zero LeD scores
   889 pairs (8.89%) got non-zero PoD scores
   11 pairs (0.11%) got all zero scores
(base) ye@:~/exp/LePoD$ 
```

Lexical Difference (LeD) နဲ့ pairwise Positional Difference (PoD) score တွေမှာတော့ -l, -d ကို ထည့် run လည်း လက်ရှိ para1, para2 ဖိုင်နှစ်ဖိုင်ပေါ်မှာတွက်ကြည့်တဲ့အခါမှာတော့ အပြာင်းအလဲ မရှိတာကို တွေ့ရ...  

## Reference

https://github.com/xingniu/multitask-ft-fsmt/tree/master/LePoD
http://www.cs.cmu.edu/~alavie/METEOR/
