# Sentence Segmentation by NMT Tagging Experiment

## Code for end-mark Error Checking

```bash
root@105d5ce0073b:/home/ye/exp/mysent# cat check-end-mark.sh
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliate Professor, CADT, Cambodia
## Checking end-mark tags
## Last updated: 13 Oct 2022
## How to run: bash ./check-end-mark.sh <input-file> <output-file>

cat $1 | grep -o '[^/]*$' \
        | nl -s: | sed 's/^ *//g' | grep "N\|O" > $2
```

## Checking Again

```
root@105d5ce0073b:/home/ye/exp/mysent/checked-thura# ls
err.para.txt  err.sent.txt  paragraph.txt  sentences.txt
root@105d5ce0073b:/home/ye/exp/mysent/checked-thura# ../check-end-mark.sh ./sentences.txt ./chk.out
root@105d5ce0073b:/home/ye/exp/mysent/checked-thura# wc chk.out
0 0 0 chk.out
root@105d5ce0073b:/home/ye/exp/mysent/checked-thura# ../check-end-mark.sh ./paragraph.txt ./chk.out
root@105d5ce0073b:/home/ye/exp/mysent/checked-thura# wc chk.out
0 0 0 chk.out
root@105d5ce0073b:/home/ye/exp/mysent/checked-thura#
```

## Connection Dropped

```
ye@lst-gpu-3090:~$ screen -r
There is a screen on:
        97054.nmt       (18/10/2565 07:29:58)   (Attached)
There is no screen to be resumed.
ye@lst-gpu-3090:~$ screen -d 97054.nmt
[97054.nmt detached.]

ye@lst-gpu-3090:~$ screen -r 97054.nmt
```

## Download mk-wordtag.pl

```
root@105d5ce0073b:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag# wget https://raw.githubusercontent.com/ye-kyaw-thu/myPOS/master/corpus-draft-ver-1.0/mk-wordtag.pl
--2022-10-18 06:58:42--  https://raw.githubusercontent.com/ye-kyaw-thu/myPOS/master/corpus-draft-ver-1.0/mk-wordtag.pl
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.109.133, 185.199.110.133, 185.199.108.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.109.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3967 (3.9K) [text/plain]
Saving to: 'mk-wordtag.pl'

mk-wordtag.pl                     100%[===========================================================>]   3.87K  --.-KB/s    in 0s

2022-10-18 06:58:43 (34.9 MB/s) - 'mk-wordtag.pl' saved [3967/3967]

root@105d5ce0073b:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag# ls
mk-wordtag.pl  paragraph.txt  sentences.txt
root@105d5ce0073b:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag#
```

## Updating mk-wordtag.pl 

```perl 

#!/usr/bin/perl
use warnings;
use utf8;

#last updated: 18 Oct 2022
#written by Ye, IDRI, CADT, Cambodia,
#How to run: perl mk-wordtag2.pl <input-file-name> <delimeter> <w|t|wt>
#Here,
# w = print word only (i.e. without POS tags),
# t = print tag only
# wt = print word/tag
# c = print sentence that contain tagging error of "word/"
#
# How to run:
# e.g. ./mk-wordtag.pl ./kh-pos.all.f2.utf8 "\/" w | less -r
# e.g ./mk-wordtag.pl ./kh-pos.all.f2.utf8 "\/" t
# e.g ./mk-wordtag.pl ./kh-pos.all.f2.utf8 "\/" wt

binmode STDIN,  ":utf8";
binmode STDOUT, ":utf8";

my $TagMarker=$ARGV[1]; # give command line parameter such as "\|", "\/" ...
my $word_or_tag=$ARGV[2];

open (my $inputFILE,"<:encoding(utf8)", $ARGV[0]) or die "Couldn't open input file $ARGV[0]!, $!\n";

my $one_token; my $tmpLine=""; my $tmpLine2="";

   while($line = <$inputFILE>)
   {
      if ($line!~/^$/)
      {
         chomp ($line);
         my $originalLine = $line;
         #print $line, "\n";

         $line =~ s/\s+/ /g;
         $line =~ s/^\s+|\s+$//g;
         my @token = split('\s', $line);
         #print "\@tokens:\n"."@token\n";
         foreach $one_token(@token)
         {
            #print "one_token: $one_token\n";
            my ($text, $tag) = split(/$TagMarker/, $one_token);
            if($word_or_tag eq "w")
            {
               $tmpLine = $tmpLine.$text." ";
            }elsif($word_or_tag eq "t")
            {
               $tmpLine = $tmpLine.$tag." ";
            }elsif($word_or_tag eq "wt" || $word_or_tag eq "c")
            {
               $tmpLine = $tmpLine.$text." ";
               $tmpLine2 = $tmpLine2.$tag." ";

            }
        }
            #chomp($tmpLine);
            if ($word_or_tag eq "w" || $word_or_tag eq "t")
            {
               $tmpLine =~ s/^\s+|\s+$//g;
               print $tmpLine."\n";
            }elsif ($word_or_tag eq "wt")
            {

               $tmpLine =~ s/^\s+|\s+$//g;
               $tmpLine2 =~ s/^\s+|\s+$//g;
               print $tmpLine."\n"; print $tmpLine2."\n";
            }elsif ($word_or_tag eq "c")
            {
               $tmpLine =~ s/^\s+|\s+$//g;
               $tmpLine =~ s/\s+/ /g;
               $tmpLine2 =~ s/^\s+|\s+$//g;
               $tmpLine2 =~ s/\s+/ /g;
               my $word_count = split / /,$tmpLine;
               my $tag_count = split / /,$tmpLine2;

               if ($word_count != $tag_count)
               {
                  print "$originalLine\n";
                  print "$word_count: $tag_count\n";
                  print $tmpLine."\n"; print $tmpLine2."\n";
               }

             }
                    $tmpLine = ""; $tmpLine2 = "";
         }
      }

close($inputFILE);
```
	
## Splitting for sentences.txt

```
root@105d5ce0073b:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag# perl ./mk-wordtag2.pl ./sentences.txt "\/" w > sentences.word
root@105d5ce0073b:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag# wc ./sentences.txt
   47127   639484 10534167 ./sentences.txt
root@105d5ce0073b:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag# wc ./sentences.word
  47127    4411 9254497 ./sentences.word
```

```
root@105d5ce0073b:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag# head ./sentences.word
Summit ဟဟိုတယ် အခန်း နံပါတ် ၃၀၂ မှာ နေ ဖဖိဖို့ ခင်ဗျား အတွက် စီစဉ် ပေး ထား ပါ တယ်
ကူးစက်ရောဂါ ဖြစ် ပါ တယ်
ဘာ ကကို ခင်ဗျား အကြြိုက်ဆဆုံး လဲ
ခင်ဗျား ဘယ်လောက် ဆဆိုဒ် ကြီးကြီး လလို ချင် တာ လဲ
အနီးဆဆုံး စားသောက်ဆဆိုင် ဘယ် နား မှာ လဲ
လူ မှာ ပါးစပ် ရှိ ရင် ထင်မြင်ယူဆချက် တွေ ဝေဖန်ချက် တွေ က တော့ ရှိ မှာ ပဲ
၅၀ သား
အအို ကကို တတိုက်ရရိုက် သွား ဖဖိဖို့ လား
ကျွန်တော် အထက်တန်း အိပ်စင် တွဲ မှာ ပါ
ကြား ဖူး တာ ထက် ပပို တော် တယ် ဆဆို တာ ကကို လူကကိုယ်တတိုင် တွေ့ မှ သိ တော့ တယ်
root@105d5ce0073b:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag#
```
As you see in above, some Myanmar characters are repeating. Why?  
Confirm outside of docker container env again and the output is as follows:  

```
ye@lst-gpu-3090:~/exp/mysent/checked-thura/preprocessing/split-tag$ head ./sentences.word
Summit ဟိုတယ် အခန်း နံပါတ် ၃၀၂ မှာ နေ ဖို့ ခင်ဗျား အတွက် စီစဉ် ပေး ထား ပါ တယ်
ကူးစက်ရောဂါ ဖြစ် ပါ တယ်
ဘာ ကို ခင်ဗျား အကြိုက်ဆုံး လဲ
ခင်ဗျား ဘယ်လောက် ဆိုဒ် ကြီးကြီး လို ချင် တာ လဲ
အနီးဆုံး စားသောက်ဆိုင် ဘယ် နား မှာ လဲ
လူ မှာ ပါးစပ် ရှိ ရင် ထင်မြင်ယူဆချက် တွေ ဝေဖန်ချက် တွေ က တော့ ရှိ မှာ ပဲ
၅၀ သား
အို ကို တိုက်ရိုက် သွား ဖို့ လား
ကျွန်တော် အထက်တန်း အိပ်စင် တွဲ မှာ ပါ
ကြား ဖူး တာ ထက် ပို တော် တယ် ဆို တာ ကို လူကိုယ်တိုင် တွေ့ မှ သိ တော့ တယ်
ye@lst-gpu-3090:~/exp/mysent/checked-thura/preprocessing/split-tag$
```

It looks OK! :)  

Confirmation on the numbers of word outside of the docker env also:  

```
ye@lst-gpu-3090:~/exp/mysent/checked-thura/preprocessing/split-tag$ wc sentences.{txt,word,tag}
   47127   639526 10534167 sentences.txt
   47127   639501  9254497 sentences.word
   47127   639484  1279422 sentences.tag
  141381  1918511 21068086 total
ye@lst-gpu-3090:~/exp/mysent/checked-thura/preprocessing/split-tag$
```

I think there are some tagging errors!!!  

```
root@105d5ce0073b:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag# perl ./mk-wordtag2.pl ./sentences.txt "\/" t > sentences.
tag
root@105d5ce0073b:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag# wc ./sentences.tag
  47127  639484 1279422 ./sentences.tag
root@105d5ce0073b:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag# head ./sentences.tag
B O O O O O O O O O O N N N E
B N N E
B N N N E
B O O O N N N E
B O N N N E
B O O O O O O O O O N N N E
B E
B O N N N E
B O N N N E
B O O O O O O O O O O O N N N E
root@105d5ce0073b:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag#
```

## Check the Splitted Files

```
root@105d5ce0073b:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag# perl ./mk-wordtag2.pl ./sentences.txt "\/" c > chk.err
root@105d5ce0073b:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag# wc chk.err
   72   805 11688 chk.err
```

```
ye@lst-gpu-3090:~/exp/mysent/checked-thura/preprocessing/split-tag$ head chk.err
၁၈၇၉/B /Bခုနှစ်/O တွင်/O ရုရှား/O လူမျိုး/O ထဲ/O မှ/O ဒေသ/O သစ်/O ရှာဖွေ/O သော/O ပါဇီဗားလစကီး/O ဆို/O သူ/O ထံ/O သို့/O အထက်/O ထက်/O က/O မည်သူ/O တစ်စုံတစ်ယောက်/O မျှ/O မ/O တွေ့မြင်/O ဖူး/O သေး/O သော/O ဤ/O မြင်း/O ရိုင်း/O မျိုး/O ရောက်/N ရှိ/N လာ/N သည်/E
34: 35
၁၈၇၉ တွင် ရုရှား လူမျိုး ထဲ မှ ဒေသ သစ် ရှာဖွေ သော ပါဇီဗားလစကီး ဆို သူ ထံ သို့ အထက် ထက် က မည်သူ တစ်စုံတစ်ယောက် မျှ မ တွေ့မြင် ဖူး သေး သော ဤ မြင်း ရိုင်း မျိုး ရောက် ရှိ လာ သည်
B Bခုနှစ် O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
အဲဒီ/B ပုံစံ/O ထဲ/O မှာ/O နိုင်ငံခြား/O ငွေ/O ရွှေထည်/O ငွေထည်/O /Bနဲ့/O တခြား/O အဖိုးတန်/O ပစ္စည်း/O တွေ/N ဖြည့်/N ရ/N မယ်/E
15: 16
အဲဒီ ပုံစံ ထဲ မှာ နိုင်ငံခြား ငွေ ရွှေထည် ငွေထည် တခြား အဖိုးတန် ပစ္စည်း တွေ ဖြည့် ရ မယ်
B O O O O O O O Bနဲ့ O O O N N N E
ကျွန်တော်/B တို့/O က/O ပြိုင်ဘက်/O ကုမ္ပဏီ/O မှာ/O အကြီးအကျယ်/O ခံ/O ခဲ့/O ရ/O ပြီး/O နင်/O တခါတည်း/O /N မှတ်/N သွား/N တယ်/E
16: 17
ye@lst-gpu-3090:~/exp/mysent/checked-thura/preprocessing/split-tag$ tail chk.err
ရထား က ၁၁ ဝ၄ မှာ ထွက် တယ်
B O O N O N N E
/E
0: 1

E
/B ဥပမာ/O ခရစ်နှစ်/O ၂၀၁၂/O တွင်/O ၂/O ၆၀၀/O ဗုဒ္ဓသာသနာ/O နှစ်/O ၂၀၁၂ဘီစီ၅၈၈၂၆၀၀/O ဗုဒ္ဓသာသနာ/O နှစ်/O ဖြစ်/N ရ/N ပါ/N မည်/E
15: 16
ဥပမာ ခရစ်နှစ် ၂၀၁၂ တွင် ၂ ၆၀၀ ဗုဒ္ဓသာသနာ နှစ် ၂၀၁၂ဘီစီ၅၈၈၂၆၀၀ ဗုဒ္ဓသာသနာ နှစ် ဖြစ် ရ ပါ မည်
B O O O O O O O O O O O N N N E
ye@lst-gpu-3090:~/exp/mysent/checked-thura/preprocessing/split-tag$
```

## Updated sentences.txt And Re-Check

```
perl ./mk-wordtag2.pl ./sentences.txt "\/" c

root@f84cbd307135:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag# cat ./sentences.chk
အယ်ဆာဗေဒို/B အစိုးရ/O ၏/O လက်ယာ/O ပိုမို/O ယိမ်းယိုင်/O လာ/O မှု/O ကြောင့်/O လက်ဝဲ/O အဖွဲ့အစည်း/O များ/O /O ဆိုရှယ်ဒီမိုကရက်တစ်/O များ/O ၊/O ခရစ်ယာန်/O ဒီမိုကရက်တစ်/O အချို့/O နှင့်/O တောင်သူလယ်သမား/O အဖွဲ့အစည်း/O များ/O ၊/O ကျောင်းသား/O များ/O ၊/O အလုပ်သမား/O သမဂ္ဂ/O များ/O ၊/O ဘာသာ/O ရေး/O အဖွဲ့အစည်း/O များ/O မှ/O ပုဂ္ဂိုလ်/O များ/O သည်/O ဒီမိုကရက်တစ်/O တော်လှန်/O ရေး/O တပ်ဦး/O ကို/O ဖွဲ့စည်း/O ပြီး/O အစိုးရ/O ကို/O ပိုမို/O ဆန့်ကျင်/O လာ/N ခဲ့/N ကြ/N သည်/E
53: 54
အယ်ဆာဗေဒို အစိုးရ ၏ လက်ယာ ပိုမို ယိမ်းယိုင် လာ မှု ကြောင့် လက်ဝဲ အဖွဲ့အစည်း များ ဆိုရှယ်ဒီမိုကရက်တစ် များ ၊ ခရစ်ယာန် ဒီမိုကရက်တစ် အချို့ နှင့် တောင်သူလယ်သမား အဖွဲ့အစည်း များ ၊ ကျောင်းသား များ ၊ အလုပ်သမား သမဂ္ဂ များ ၊ ဘာသာ ရေး အဖွဲ့အစည်း များ မှ ပုဂ္ဂိုလ် များ သည် ဒီမိုကရက်တစ် တော်လှန် ရေး တပ်ဦး ကို ဖွဲ့စည်း ပြီး အစိုးရ ကို ပိုမို ဆန့်ကျင် လာ ခဲ့ ကြ သည်
B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
root@f84cbd307135:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag#
```

I think, I forgot to delete /O tag.  
When I see with vi editor inside the docker env, it looks OK. ?!?!  

```
37363 ~@~@~Z~@~@~F~@~@~W~@~@~R~@~@/B ~@~@~E~@~@~@~@~[/O ~A~O/O ~@~\~@~@~@~@~Z~@/O ~@~U~@~@~@~Y
      ~@~@/O ~@~Z~@~@~Y~@~@~@~Z~@~@~@~D~@/O ~@~\~@/O ~@~Y~@~@/O ~@~@~@~@~@~@~D~@~@/O ~@~\~@~@
      ~@~@~]~@/O ~@~@~V~@~@~@~@~@~E~@~J~@~@/O ~@~Y~@~@~@/O ~A~J/O ~@~F~@~@~@~[~@~@~Z~@~@~R~@
      ~@~Y~@~@~@~@~@~[~@~@~@~@~P~@~E~@/O ~@~Y~@~@~@/O ~@~A~@~[~@~E~@~@~Z~@~@~T~@/O ~@~R~@~@~Y~@~~
      @~@~@~@~[~@~@~@~@~P~@~E~@/O ~@~@~A~@~@~@~@/O ~@~T~@~@~D~@~@/O ~@~P~@~@~@~D~@~@~^~@~@~\~~
      @~Z~@~@~^~@~Y~@~@/O ~@~@~V~@~@~@~@~@~E~@~J~@~@/O ~@~Y~@~@~@/O ~@~@~@~@~@~@~D~@~@~@~^^
      ~@~@/O ~@~Y~@~@~@/O ~@~@~\~@~@~U~@~@~^~@~Y~@~@/O ~@~^~@~Y~@~B~@~@~B/O ~@~Y~@~@~@/O ~@~X~@@
      ~@~^~@/O ~@~[~@~@/O ~@~@~V~@~@~@~@~@~E~@~J~@~@/O ~@~Y~@~@~@/O ~@~Y~@/O ~@~U~@~@~B~@~@~~
      B~@~@~@~\~@/O ~@~Y~@~@~@/O ~@~^~@~J~@/O ~@~R~@~@~Y~@~@~@~@~@~[~@~@~@~@~P~@~E~@/O ~@~P~@~@
      ~@~@~\~@~@~T~@/O ~@~[~@~@/O ~@~P~@~U~@~@~@/O ~@~@~@~@/O ~@~V~@~@~@~@~E~@~J~@~@/O ~@~U~@
      ~@~@/O ~@~@~E~@~@~@~@~[/O ~@~@~@~@/O ~@~U~@~@~@~Y~@~@/O ~@~F~@~T~@~@~@~@~@~@~D~@/O ~@~\\
      ~@/N ~@~A~@~@/N ~@~@~@/N ~@~^~@~J~@/E
```	  

When I checked in details:  

```
That sentence typed 2 times in the corpus. One I can found as follows at line no. 37363:  

အင်္ဂလိပ်/B လို/O လည်း/N ပြော/N တတ်/N လား/E
အယ်ဆာဗေဒို/B အစိုးရ/O ၏/O လက်ယာ/O ပိုမို/O ယိမ်းယိုင်/O လာ/O မှု/O ကြောင့်/O လက်ဝဲ/O အဖွဲ့အစည်း/O များ/O ၊/O ဆိုရှယ်ဒီမိုကရက်တစ်/O များ/O ခရစ်ယာန်/O ဒီမိုကရက်တစ်/O အချို့/O နှင့်/O တောင်သူလယ်သမား/O အဖွဲ့အစည်း/O များ/O ကျောင်းသား/O များ/O အလုပ်သမား/O သမဂ္ဂ/O များ/O ဘာသာ/O ရေး/O အဖွဲ့အစည်း/O များ/O မှ/O ပုဂ္ဂိုလ်/O များ/O သည်/O ဒီမိုကရက်တစ်/O တော်လှန်/O ရေး/O တပ်ဦး/O ကို/O ဖွဲ့စည်း/O ပြီး/O အစိုးရ/O ကို/O ပိုမို/O ဆန့်ကျင်/O လာ/N ခဲ့/N ကြ/N သည်/E
ကား/B တစ်/O စီး/O လောက်/N ရ/N နိုင်/N မလား/E

line no. 38347:

ကျွန်တော်/B ပါ/N ပဲ/E
အယ်ဆာဗေဒို/B အစိုးရ/O ၏/O လက်ယာ/O ပိုမို/O ယိမ်းယိုင်/O လာ/O မှု/O ကြောင့်/O လက်ဝဲ/O အဖွဲ့အစည်း/O များ/O /O ဆိုရှယ်ဒီမိုကရက်တစ်/O များ/O ၊/O ခရစ်ယာန်/O ဒီမိုကရက်တစ်/O အချို့/O နှင့်/O တောင်သူလယ်သမား/O အဖွဲ့အစည်း/O များ/O ၊/O ကျောင်းသား/O များ/O ၊/O အလုပ်သမား/O သမဂ္ဂ/O များ/O ၊/O ဘာသာ/O ရေး/O အဖွဲ့အစည်း/O များ/O မှ/O ပုဂ္ဂိုလ်/O များ/O သည်/O ဒီမိုကရက်တစ်/O တော်လှန်/O ရေး/O တပ်ဦး/O ကို/O ဖွဲ့စည်း/O ပြီး/O အစိုးရ/O ကို/O ပိုမို/O ဆန့်ကျင်/O လာ/N ခဲ့/N ကြ/N သည်/E
‌ဆေး/B အလုံး/N နှစ်ဆယ်/N ပါ/N တယ်/E
```

## Fixed Line No. 38347 and Re-Check

```
root@1df80c9b2102:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag# perl ./mk-wordtag2.pl ./sentences.txt "\/" w > ./sentences.word
root@1df80c9b2102:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag# perl ./mk-wordtag2.pl ./sentences.txt "\/" t > ./sentences
.tag
root@1df80c9b2102:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag# perl ./mk-wordtag2.pl ./sentences.txt "\/" c
root@1df80c9b2102:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag#
```

## Check No. of Words for Sentence Data

```
root@1df80c9b2102:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag# wc sentences.{word,tag}
   47126     4411  9254522 sentences.word
   47126   639469  1279356 sentences.tag
   94252   643880 10533878 total
root@1df80c9b2102:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag# exit
exit
ye@lst-gpu-3090:~/exp/mysent/checked-thura/preprocessing/split-tag$ wc sentences.{word,tag}
   47126   639505  9254522 sentences.word
   47126   639469  1279356 sentences.tag
   94252  1278974 10533878 total
ye@lst-gpu-3090:~/exp/mysent/checked-thura/preprocessing/split-tag$
ye@lst-gpu-3090:~/exp/mysent/checked-thura/preprocessing/split-tag$ wc sentences.txt
   47126   639511 10534119 sentences.txt
```

Althoug I wish to check more in details, no time. Should start experiment ASAP.  

## Shuffle the Sentence Data

```
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# shuf ./sentences.txt > sentences.txt.shuf
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# head ./sentences.txt
Summit/B ဟိုတယ်/O အခန်း/O နံပါတ်/O ၃၀၂/O မှာ/O နေ/O ဖို့/O ခင်ဗျား/O အတွက်/O စီစဉ်/O ပေး/N ထား/N ပါ/N တယ်/E
ကူးစက်ရောဂါ/B ဖြစ်/N ပါ/N တယ်/E
ဘာ/B ကို/N ခင်ဗျား/N အကြိုက်ဆုံး/N လဲ/E
ခင်ဗျား/B ဘယ်လောက်/O ဆိုဒ်/O ကြီးကြီး/O လို/N ချင်/N တာ/N လဲ/E
အနီးဆုံး/B စားသောက်ဆိုင်/O ဘယ်/N နား/N မှာ/N လဲ/E
လူ/B မှာ/O ပါးစပ်/O ရှိ/O ရင်/O ထင်မြင်ယူဆချက်/O တွေ/O ဝေဖန်ချက်/O တွေ/O က/O တော့/N ရှိ/N မှာ/N ပဲ/E
၅၀/B သား/E
အို/B ကို/O တိုက်ရိုက်/N သွား/N ဖို့/N လား/E
ကျွန်တော်/B အထက်တန်း/O အိပ်စင်/N တွဲ/N မှာ/N ပါ/E
ကြား/B ဖူး/O တာ/O ထက်/O ပို/O တော်/O တယ်/O ဆို/O တာ/O ကို/O လူကိုယ်တိုင်/O တွေ့/O မှ/N သိ/N တော့/N တယ်/E
```

```
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# head ./sentences.txt.shuf
ဘာ/B ရယ်/O လို့/O တိတိကျကျ/O ထောက်မပြ/O နိုင်/O ပေမဲ့/O ပြဿနာ/O တစ်/O ခု/O ခု/O ရှိ/O တယ်/N နဲ့/N တူ/N တယ်/E
လူ့/B အဖွဲ့အစည်း/O က/O ရှပ်ထွေး/O လာ/O တာ/O နဲ့/O အမျှ/O အရင်/O က/O မ/O ရှိ/O ခဲ့/O တဲ့/O လူမှုရေး/O ပြဿနာ/O တွေ/O ဖြစ်ပေါ်/N လာ/N ခဲ့/N တယ်/E
အခု/B အလုပ်/O လုပ်/N နေ/N ပါ/N တယ်/E
ကြည့်/B ရေစာ/O တွေ/O က/O အဲဒီ/O တစ်/O ခု/O နဲ့/N မ/N တူ/N ဘူး/E
ဘူမိ/B ရုပ်သွင်/O ပညာ/O သည်/O ကုန်းမြေသဏ္ဌာန်/O များ/O ကို/O လေ့လာ/O သော/N ပညာရပ်/N ဖြစ်/N သည်/E
ခြေဆစ်/B လက်ဆစ်/O တို့/O ၏/O အထက်/O နား/O မှ/O ရှည်လျား/O သော/O အမွေး/O မျှင်/O များ/O ကျ/N လျက်/N ရှိ/N သည်/E
အမြန်နှုန်း/B မြင့်/O လွန်း/O တဲ့/O ကား/O က/N အန္တရာယ်/N များ/N တယ်/E
မချုပ်/B တည်း/O နိုင်/O တော့/O ပဲ/O ကျောင်းဆောင်/O ထဲ/O က/O အပျိုစင်/O နတ်/O ဘုရား/O အသီးနား/O ရဲ့/O ရုပ်/O ထု/O ရှေ့/O မှာ/O ပဲ/O မက်ဒူးဆာ/O ကို/O အနိုင်/O အထက်/O ပြု/O လို့မယား/O အဖြစ်/O သိမ်းပိုက်/O လိုက်/N ပါ/N လေ/N တယ်/E
နောက်/B မှ/O ကော်ဖီ/O ဖြစ်/O ဖြစ်/O တစ်/O ခွက်/O လောက်/N သောက်/N ကြ/N ရအောင်/E
နေ့/B တိုင်း/O အသား/O ပဲ/O စား/O နေ/O ရ/O တော့/O အခု/O ဆို/N ငြီးငွေ့/N လာ/N ပြီ/E
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data#
```

## Data Preparation for Sentence Data

Test data:  
```
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# tail -n 4712 ./sentences.txt.shuf > test.txt
```

Training data:  

```
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# head -n 40000 ./sentences.txt.shuf > train.txt
```

Valid data:  

```
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# head -n 42414 ./sentences.txt.shuf | tail -n 2414 > valid.txt

Rename files for avoiding errors with paragraph data:
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# mv train.txt train.sent.txt
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# mv valid.txt valid.sent.txt
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# mv test.txt test.sent.txt
```

Note/Check the data size:  

```
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# wc train.sent.txt
  40000  543534 8956178 train.sent.txt
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# wc valid.sent.txt
  2414  32315 531172 valid.sent.txt
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# wc test.sent.txt
   4712   63620 1046769 test.sent.txt
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data#
```

## Splitting word and tag files

```
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# perl ./mk-wordtag2.pl ./train.sent.txt  "\/" w > train.my
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# perl ./mk-wordtag2.pl ./train.sent.txt  "\/" t > train.tg
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# perl ./mk-wordtag2.pl ./valid.sent.txt  "\/"
w > valid.my
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# perl ./mk-wordtag2.pl ./valid.sent.txt  "\/"
t > valid.tg
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# perl ./mk-wordtag2.pl ./test.sent.txt  "\/" w
 > test.my
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# perl ./mk-wordtag2.pl ./test.sent.txt  "\/" t > test.tg
```

## Backup Sentence Train/valid/Test

```
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# perl ./mk-wordtag2.pl ./train.sent.txt  "\/" w > train.my
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# perl ./mk-wordtag2.pl ./train.sent.txt  "\/" t > train.tg
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# perl ./mk-wordtag2.pl ./valid.sent.txt  "\/"
w > valid.my
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# perl ./mk-wordtag2.pl ./valid.sent.txt  "\/"
t > valid.tg
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# perl ./mk-wordtag2.pl ./test.sent.txt  "\/" w
 > test.my
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data# perl ./mk-wordtag2.pl ./test.sent.txt  "\/" t > test.tg
```

## Check Stastics of Sentence Train/Valid/Test

```
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data/final-bk# wc train.{my,tg}
  40000    3703 7868550 train.my
  40000  543534 1087429 train.tg
  80000  547237 8955979 total
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data/final-bk# wc valid.{my,tg}
  2414    257 466524 valid.my
  2414  32315  64642 valid.tg
  4828  32572 531166 total
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data/final-bk# wc test.{my,tg}
   4712     451  919448 test.my
   4712   63620  127285 test.tg
   9424   64071 1046733 total
root@d1e452255dc6:/home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data/final-bk#
```

## Vocab Building

```
root@d1e452255dc6:/home/ye/exp/mysent# mkdir data-sent
root@d1e452255dc6:/home/ye/exp/mysent# cp /home/ye/exp/mysent/checked-thura/preprocessing/split-tag/shuffle-data/final-bk/* ./data-sent/
root@d1e452255dc6:/home/ye/exp/mysent# cd data-sent
root@d1e452255dc6:/home/ye/exp/mysent/data-sent# ls
test.my  test.tg  train.my  train.tg  valid.my  valid.tg
root@d1e452255dc6:/home/ye/exp/mysent/data-sent# mkdir vocab
root@d1e452255dc6:/home/ye/exp/mysent/data-sent# cat train.my valid.my test.my > ./vocab/all.my
root@d1e452255dc6:/home/ye/exp/mysent/data-sent# cat train.tg valid.tg test.tg > ./vocab/all.tg
```

```
root@d1e452255dc6:/home/ye/exp/mysent/data-sent/vocab# ls
all.my  all.tg
root@d1e452255dc6:/home/ye/exp/mysent/data-sent/vocab# marian-vocab < all.my > vocab.my.yml
[2022-10-18 11:09:35] Creating vocabulary...
[2022-10-18 11:09:35] [data] Creating vocabulary stdout from stdin
[2022-10-18 11:09:36] Finished
root@d1e452255dc6:/home/ye/exp/mysent/data-sent/vocab# marian-vocab < all.tg > vocab.tg.yml
[2022-10-18 11:09:48] Creating vocabulary...
[2022-10-18 11:09:48] [data] Creating vocabulary stdout from stdin
[2022-10-18 11:09:48] Finished
```

```
root@d1e452255dc6:/home/ye/exp/mysent/data-sent/vocab# head vocab.my.yml
</s>: 0
<unk>: 1
ကို: 2
သည်: 3
တယ်: 4
က: 5
ပါ: 6
မှာ: 7
များ: 8
ရှိ: 9
```
	
```
root@d1e452255dc6:/home/ye/exp/mysent/data-sent/vocab# head vocab.tg.yml
</s>: 0
<unk>: 1
O: 2
N: 3
E: 4
B: 5
NN: 6
BBအိုး: 7
BEအကြိမ်: 8
Bကြီး: 9
root@d1e452255dc6:/home/ye/exp/mysent/data-sent/vocab#
```
	
Printout the whole vocab file of tg:  

root@d1e452255dc6:/home/ye/exp/mysent/data-sent/vocab# cat vocab.tg.yml
</s>: 0
<unk>: 1
O: 2
N: 3
E: 4
B: 5
NN: 6
BBအိုး: 7
BEအကြိမ်: 8
Bကြီး: 9
Bတ်: 10
Bနင်္ဂနွေ: 11
Bဖြတ်: 12
Bလုံး: 13
B၀: 14
ENယာဉ်စီးE: 15
Eရှုပ်: 16
NBတယ်: 17
NEစကားပြော: 18
NEတယ်: 19
NEလဲ: 20
NNခဲ့: 21
NNထား: 22
NNပါ: 23
NNသည်: 24
Nမလား: 25
Nါဏဗေဒ: 26
Nး: 27
ONကာကွယ်NN: 28
ONပေး: 29
ONပြော: 30
ONရာဇပNတ္တ: 31
ONရိုက်နှိပE: 32
ONရေးမှတE: 33
ONသာလွန်NN: 34
Oး: 35
Oးပေါက်: 36root@d1e452255dc6:/home/ye/exp/mysent/data-sent/vocab#

From the above result, I found that manual tagging error still exist.

## Check Current Vocab Filesize

root@d1e452255dc6:/home/ye/exp/mysent/data-sent/vocab# wc *.yml
  32611   65224 1072535 vocab.my.yml
     36      74     635 vocab.tg.yml
  32647   65298 1073170 total
  
## Check the Prepared Data Folder for Sentence-Level

root@d1e452255dc6:/home/ye/exp/mysent/data-sent# tree
.
|-- test.my
|-- test.tg
|-- train.my
|-- train.tg
|-- valid.my
|-- valid.tg
`-- vocab
    |-- all.my
    |-- all.tg
    |-- vocab.my.yml
    `-- vocab.tg.yml

1 directory, 10 files
root@d1e452255dc6:/home/ye/exp/mysent/data-sent#

## Prepare marian configuration file for Transformer Archi

root@d1e452255dc6:/home/ye/exp/mysent# head -n 20 ./transformer.sent1.sh
#!/bin/bash

## Written by Ye Kyaw Thu, LST, NECTEC, Thailand
## Experiments for mySent, also preparation for 4th NLP/AI Workshop 2022

#     --mini-batch-fit -w 10000 --maxi-batch 1000 \
#    --mini-batch-fit -w 1000 --maxi-batch 100 \
#     --tied-embeddings-all \
#     --tied-embeddings \
#     --valid-metrics cross-entropy perplexity translation bleu \
#     --transformer-dropout 0.1 --label-smoothing 0.1 \
#     --learn-rate 0.0003 --lr-warmup 16000 --lr-decay-inv-sqrt 16000 --lr-report \
#     --optimizer-params 0.9 0.98 1e-09 --clip-norm 5 \

mkdir model.transformer.sent1;

marian \
    --model model.transformer.sent1/model.npz --type transformer \
    --train-sets data-sent/train.my data-sent/train.tg \
    --max-length 200 \
    --vocabs data-sent/vocab/vocab.my.yml data-sent/vocab/vocab.tg.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets data-sent/valid.my data-sent/valid.tg \
    --valid-translation-output model.transformer.sent1/valid.my-tg.output --quiet-translation \
    --valid-mini-batch 64 \
    --beam-size 6 --normalize 0.6 \
    --log model.transformer.sent1/train.log --valid-log model.transformer.sent1/valid.log \
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
    --dump-config > model.transformer.sent1/config.yml

time marian -c model.transformer.sent1/config.yml  2>&1 | tee transformer.sent1.log

## Training NMT Model for Sentence Data

[2022-10-18 11:24:13] Using synchronous SGD
[2022-10-18 11:24:13] [comm] Compiled without MPI support. Running as a single process on cb9dcb03dfe7
[2022-10-18 11:24:13] Synced seed 1111
[2022-10-18 11:24:13] [data] Loading vocabulary from JSON/Yaml file data-sent/vocab/vocab.my.yml
[2022-10-18 11:24:13] [data] Setting vocabulary size for input 0 to 32,612
[2022-10-18 11:24:13] [data] Loading vocabulary from JSON/Yaml file data-sent/vocab/vocab.tg.yml
[2022-10-18 11:24:13] [data] Setting vocabulary size for input 1 to 37
[2022-10-18 11:24:13] [batching] Collecting statistics for batch fitting with step size 10
[2022-10-18 11:24:43] Error: Curand error 203 - /temp/marian/src/tensors/rand.cpp:74: curandCreateGenerator(&generator_, CURAND_RNG_PSEUDO_DEFAULT)
[2022-10-18 11:24:43] Error: Aborted from marian::CurandRandomGenerator::CurandRandomGenerator(size_t, marian::DeviceId) in /temp/marian/src/tensors/rand.cpp:74

[CALL STACK]
[0x56529df29050]    marian::CurandRandomGenerator::  CurandRandomGenerator  (unsigned long,  marian::DeviceId) + 0x750
[0x56529df29689]    marian::  createRandomGenerator  (unsigned long,  marian::DeviceId) + 0x69
[0x56529df23f20]    marian::  BackendByDeviceId  (marian::DeviceId,  unsigned long) + 0xa0
[0x56529da13220]    marian::ExpressionGraph::  setDevice  (marian::DeviceId,  std::shared_ptr<marian::Device>) + 0x80
[0x56529dd0ccd5]    marian::GraphGroup::  initGraphsAndOpts  ()        + 0x1e5
[0x56529dd0e1f8]    marian::GraphGroup::  GraphGroup  (std::shared_ptr<marian::Options>,  std::shared_ptr<marian::IMPIWrapper>) + 0x548
[0x56529dcec773]    marian::SyncGraphGroup::  SyncGraphGroup  (std::shared_ptr<marian::Options>,  std::shared_ptr<marian::IMPIWrapper>) + 0x83
[0x56529d8458ab]    marian::Train<marian::SyncGraphGroup>::  run  ()   + 0x1c2b
[0x56529d773347]    mainTrainer  (int,  char**)                        + 0x147
[0x7f469fdd5d90]                                                       + 0x29d90
[0x7f469fdd5e40]    __libc_start_main                                  + 0x80
[0x56529d76c995]    _start                                             + 0x25


real    0m37.309s
user    0m0.149s
sys     0m29.984s
root@cb9dcb03dfe7:/home/ye/exp/mysent# ./transformer.sent1.sh

Check the GPU status:

root@cb9dcb03dfe7:/home/ye/exp/mysent# nvidia-smi
Tue Oct 18 11:28:04 2022
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 515.65.01    Driver Version: 515.65.01    CUDA Version: 11.7     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  On   | 00000000:01:00.0 Off |                  Off |
|ERR!   59C    P0    66W / 480W |    120MiB / 24564MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
+-----------------------------------------------------------------------------+
root@cb9dcb03dfe7:/home/ye/exp/mysent#

## Updated the script

#!/bin/bash

## Written by Ye Kyaw Thu, LST, NECTEC, Thailand
## Experiments for mySent, also preparation for 4th NLP/AI Workshop 2022

#     --mini-batch-fit -w 10000 --maxi-batch 1000 \
#    --mini-batch-fit -w 1000 --maxi-batch 100 \
#     --tied-embeddings-all \
#     --tied-embeddings \
#     --valid-metrics cross-entropy perplexity translation bleu \
#     --transformer-dropout 0.1 --label-smoothing 0.1 \
#     --learn-rate 0.0003 --lr-warmup 16000 --lr-decay-inv-sqrt 16000 --lr-report \
#     --optimizer-params 0.9 0.98 1e-09 --clip-norm 5 \

mkdir model.transformer.sent1;

marian \
    --model model.transformer.sent1/model.npz --type transformer \
    --train-sets data-sent/train.my data-sent/train.tg \
    --max-length 200 \
    --vocabs data-sent/vocab/vocab.my.yml data-sent/vocab/vocab.tg.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets data-sent/valid.my data-sent/valid.tg \
    --valid-translation-output model.transformer.sent1/valid.my-tg.output --quiet-translation \
    --valid-mini-batch 32 \
    --beam-size 6 --normalize 0.6 \
    --log model.transformer.sent1/train.log --valid-log model.transformer.sent1/valid.log \
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
    --dump-config > model.transformer.sent1/config.yml

time marian -c model.transformer.sent1/config.yml  2>&1 | tee transformer.sent1.log

## Training

[2022-10-19 00:34:44] [data] Done shuffling 40,000 sentences to temp files
[2022-10-19 00:35:41] Ep. 567 : Up. 135000 : Sen. 28,293 : Cost 0.67268777 * 1,222,632 @ 3,197 after 330,467,583 : Time 170.19s : 7183.90 words/s : gNorm 0.2991 : L.r. 1.0328e-04
[2022-10-19 00:35:41] Saving model weights and runtime parameters to model.transformer.sent1/model.iter135000.npz
[2022-10-19 00:35:42] Saving model weights and runtime parameters to model.transformer.sent1/model.npz
[2022-10-19 00:35:43] Saving Adam parameters
[2022-10-19 00:35:44] [training] Saving training checkpoint to model.transformer.sent1/model.npz and model.transformer.sent1/model.npz.optimizer.npz
[2022-10-19 00:35:49] [valid] Ep. 567 : Up. 135000 : cross-entropy : 1.2978 : stalled 4 times (last best: 1.28588)
[2022-10-19 00:35:51] [valid] Ep. 567 : Up. 135000 : perplexity : 1.0944 : stalled 4 times (last best: 1.0935)
[2022-10-19 00:36:11] [valid] Ep. 567 : Up. 135000 : bleu : 86.8418 : stalled 19 times (last best: 97.8322)
[2022-10-19 00:36:35] Seen 39,999 samples
[2022-10-19 00:36:35] Starting data epoch 568 in logical epoch 568
[2022-10-19 00:36:35] [data] Shuffling data
[2022-10-19 00:36:35] [data] Done reading 40,000 sentences
[2022-10-19 00:36:35] [data] Done shuffling 40,000 sentences to temp files
[2022-10-19 00:37:57] Seen 39,999 samples
[2022-10-19 00:37:57] Starting data epoch 569 in logical epoch 569
[2022-10-19 00:37:57] [data] Shuffling data
[2022-10-19 00:37:57] [data] Done reading 40,000 sentences
[2022-10-19 00:37:57] [data] Done shuffling 40,000 sentences to temp files
[2022-10-19 00:39:02] Ep. 569 : Up. 135500 : Sen. 32,671 : Cost 0.67287427 * 1,229,235 @ 2,581 after 331,696,818 : Time 200.93s : 6117.66 words/s : gNorm 0.3458 : L.r. 1.0309e-04
[2022-10-19 00:39:18] Seen 39,999 samples
[2022-10-19 00:39:18] Starting data epoch 570 in logical epoch 570
[2022-10-19 00:39:18] [data] Shuffling data
[2022-10-19 00:39:18] [data] Done reading 40,000 sentences
[2022-10-19 00:39:18] [data] Done shuffling 40,000 sentences to temp files
[2022-10-19 00:40:39] Seen 39,999 samples
[2022-10-19 00:40:39] Starting data epoch 571 in logical epoch 571
[2022-10-19 00:40:39] [data] Shuffling data
[2022-10-19 00:40:39] [data] Done reading 40,000 sentences

## Got GPU Error

ye@lst-gpu-3090:~/exp/mysent$ nvidia-smi
Wed Oct 19 07:39:48 2022
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 515.65.01    Driver Version: 515.65.01    CUDA Version: 11.7     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  On   | 00000000:01:00.0 Off |                  Off |
|ERR!   79C    P0    66W / 480W |   2667MiB / 24564MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A      1524      G   /usr/lib/xorg/Xorg                 59MiB |
|    0   N/A  N/A      1760      G   /usr/bin/gnome-shell               58MiB |
|    0   N/A  N/A    114254      C   marian                           2545MiB |
+-----------------------------------------------------------------------------+

## Check the valid.log file

ye@lst-gpu-3090:~/exp/mysent/model.transformer.sent1$ cat ./valid.log
...
...
...
[2022-10-19 00:36:11] [valid] Ep. 567 : Up. 135000 : bleu : 86.8418 : stalled 19 times (last best: 97.8322)
[2022-10-19 01:04:45] [valid] Ep. 588 : Up. 140000 : cross-entropy : 1.30716 : stalled 5 times (last best: 1.28588)
[2022-10-19 01:04:47] [valid] Ep. 588 : Up. 140000 : perplexity : 1.09512 : stalled 5 times (last best: 1.0935)
[2022-10-19 01:05:07] [valid] Ep. 588 : Up. 140000 : bleu : 85.0503 : stalled 20 times (last best: 97.8322)
[2022-10-19 01:33:42] [valid] Ep. 609 : Up. 145000 : cross-entropy : 1.3068 : stalled 6 times (last best: 1.28588)
[2022-10-19 01:33:43] [valid] Ep. 609 : Up. 145000 : perplexity : 1.09509 : stalled 6 times (last best: 1.0935)
[2022-10-19 01:34:04] [valid] Ep. 609 : Up. 145000 : bleu : 84.902 : stalled 21 times (last best: 97.8322)
[2022-10-19 02:02:38] [valid] Ep. 630 : Up. 150000 : cross-entropy : 1.28477 : new best
[2022-10-19 02:02:39] [valid] Ep. 630 : Up. 150000 : perplexity : 1.09341 : new best
[2022-10-19 02:02:58] [valid] Ep. 630 : Up. 150000 : bleu : 82.6084 : stalled 22 times (last best: 97.8322)
[2022-10-19 02:31:32] [valid] Ep. 651 : Up. 155000 : cross-entropy : 1.2344 : new best
[2022-10-19 02:31:33] [valid] Ep. 651 : Up. 155000 : perplexity : 1.08959 : new best
[2022-10-19 02:31:53] [valid] Ep. 651 : Up. 155000 : bleu : 82.1772 : stalled 23 times (last best: 97.8322)
[2022-10-19 03:00:26] [valid] Ep. 672 : Up. 160000 : cross-entropy : 1.24967 : stalled 1 times (last best: 1.2344)
[2022-10-19 03:00:27] [valid] Ep. 672 : Up. 160000 : perplexity : 1.09075 : stalled 1 times (last best: 1.08959)
[2022-10-19 03:00:50] [valid] Ep. 672 : Up. 160000 : bleu : 81.4707 : stalled 24 times (last best: 97.8322)
[2022-10-19 03:29:24] [valid] Ep. 693 : Up. 165000 : cross-entropy : 1.21882 : new best
[2022-10-19 03:29:25] [valid] Ep. 693 : Up. 165000 : perplexity : 1.08841 : new best
[2022-10-19 03:29:45] [valid] Ep. 693 : Up. 165000 : bleu : 81.6355 : stalled 25 times (last best: 97.8322)
[2022-10-19 03:58:17] [valid] Ep. 714 : Up. 170000 : cross-entropy : 1.20379 : new best
[2022-10-19 03:58:18] [valid] Ep. 714 : Up. 170000 : perplexity : 1.08728 : new best
[2022-10-19 03:58:35] [valid] Ep. 714 : Up. 170000 : bleu : 82.814 : stalled 26 times (last best: 97.8322)
[2022-10-19 04:27:11] [valid] Ep. 735 : Up. 175000 : cross-entropy : 1.17087 : new best
[2022-10-19 04:27:12] [valid] Ep. 735 : Up. 175000 : perplexity : 1.08479 : new best
[2022-10-19 04:27:28] [valid] Ep. 735 : Up. 175000 : bleu : 87.6136 : stalled 27 times (last best: 97.8322)
[2022-10-19 04:56:02] [valid] Ep. 756 : Up. 180000 : cross-entropy : 1.18173 : stalled 1 times (last best: 1.17087)
[2022-10-19 04:56:03] [valid] Ep. 756 : Up. 180000 : perplexity : 1.08561 : stalled 1 times (last best: 1.08479)
[2022-10-19 04:56:20] [valid] Ep. 756 : Up. 180000 : bleu : 82.7266 : stalled 28 times (last best: 97.8322)
[2022-10-19 05:24:52] [valid] Ep. 777 : Up. 185000 : cross-entropy : 1.17364 : stalled 2 times (last best: 1.17087)
[2022-10-19 05:24:53] [valid] Ep. 777 : Up. 185000 : perplexity : 1.085 : stalled 2 times (last best: 1.08479)
[2022-10-19 05:25:10] [valid] Ep. 777 : Up. 185000 : bleu : 82.351 : stalled 29 times (last best: 97.8322)


## Preparing bash Script for Testing with Best Model

root@8c9f9e316b59:/home/ye/exp/mysent/model.transformer.sent1# cat test-eval-best.sh
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments for Myanmar language sentence segmentation
## used Marian NMT Framework for training
## Last updated: 20 Oct 2022

data_path="/home/ye/exp/mysent/data-sent";
src="my"; tgt="tg";

marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml --devices 0 --output hyp.best.${tgt} < ${data_path}/test.${src};
echo "Evaluation with hyp.best.${tgt}, Transformer model:" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl ${data_path}/test.${tgt} < ./hyp.best.${tgt} >> eval-best-result.txt;

root@8c9f9e316b59:/home/ye/exp/mysent/model.transformer.sent1#

## Testing with Test Data

[2022-10-19 22:46:31] Best translation 4688 : B O O N N N E
[2022-10-19 22:46:31] Best translation 4689 : B O N N N E
[2022-10-19 22:46:31] Best translation 4690 : B O O O O O N N N E
[2022-10-19 22:46:31] Best translation 4691 : B O O O O O O O O O O O N N N E
[2022-10-19 22:46:31] Best translation 4692 : B O O O O O N N N E
[2022-10-19 22:46:31] Best translation 4693 : B O N N N E
[2022-10-19 22:46:31] Best translation 4694 : B O O N N N E
[2022-10-19 22:46:31] Best translation 4695 : B N N E
[2022-10-19 22:46:31] Best translation 4696 : B O O O O N N N E
[2022-10-19 22:46:31] Best translation 4697 : B O O O N N N E
[2022-10-19 22:46:31] Best translation 4698 : B O O O N N N E
[2022-10-19 22:46:31] Best translation 4699 : B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-10-19 22:46:31] Best translation 4700 : B O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-10-19 22:46:31] Best translation 4701 : B O O N N N E
[2022-10-19 22:46:31] Best translation 4702 : B O O N N N E
[2022-10-19 22:46:31] Best translation 4703 : B O O O O O O O N N N E
[2022-10-19 22:46:31] Best translation 4704 : B O O O O O N N N E
[2022-10-19 22:46:31] Best translation 4705 : B O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
[2022-10-19 22:46:31] Best translation 4706 : B N N N E
[2022-10-19 22:46:31] Best translation 4707 : B N N N E
[2022-10-19 22:46:31] Best translation 4708 : B N N E
[2022-10-19 22:46:31] Best translation 4709 : B O N N N E
[2022-10-19 22:46:31] Best translation 4710 : B O O O O O N N N E
[2022-10-19 22:46:31] Best translation 4711 : B N N E
[2022-10-19 22:46:31] Total time: 61.31771s wall
It is not advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    1m3.558s
user    1m0.199s
sys     0m3.328s
root@8c9f9e316b59:/home/ye/exp/mysent/model.transformer.sent1# time ./test-eval-best.sh

Let's check the result:  

Evaluation with hyp.best.tg, Transformer model:
BLEU = 95.28, 95.8/95.5/95.1/94.7 (BP=1.000, ratio=1.036, hyp_len=65926, ref_len=63620)

## To Do

- chrF score calculation
- WER Calculation, check the top ten Error and make translation error analysis in details

