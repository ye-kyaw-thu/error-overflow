# Alignment Tutorial for ITC Students

Prepare the data in advance ... 

## Download the alignment shell script

https://raw.githubusercontent.com/ye-kyaw-thu/tools/master/bash/align-GIZA%2B%2B.sh


(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/alignment$ wget https://raw.githubusercontent.com/ye-kyaw-thu/tools/master/bash/align-GIZA%2B%2B.sh
--2023-04-03 18:12:24--  https://raw.githubusercontent.com/ye-kyaw-thu/tools/master/bash/align-GIZA%2B%2B.sh
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.111.133, 185.199.110.133, 185.199.109.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.111.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2464 (2.4K) [text/plain]
Saving to: ‘align-GIZA++.sh’

align-GIZA++.sh           100%[==================================>]   2.41K  6.76KB/s    in 0.4s    

2023-04-03 18:12:25 (6.76 KB/s) - ‘align-GIZA++.sh’ saved [2464/2464]

(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/alignment$

## Check the script

open gedit and assign the Giza++ installed path:  

GIZA_PATH="/home/ye/tool/giza-pp/GIZA++-v2";

## Shell script running pattern

# ./align.sh <source> <target> <output-folder>
# ./align.sh train.en train.th align2

## Python Script for Word Segmentation with Spacy

import spacy
import sys

nlp = spacy.load("en_core_web_sm")
file = open(sys.argv[1], 'r')

for line in file:
   #print(line)
   print(' '.join([token.text for token in nlp(line.strip())]))

## Word Segmentation for English

(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/alignment$ python ./spacy-seg.py ./test.alt.en > ./test.alt.en.seg

## Perl Script for the Lower Casing

(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/alignment$ cat ./lowercase.perl 
#!/usr/bin/env perl
#
# This file is part of moses.  Its use is licensed under the GNU Lesser General
# Public License version 2.1 or, at your option, any later version.

use warnings;
use strict;

binmode(STDIN, ":utf8");
binmode(STDOUT, ":utf8");

while(<STDIN>) {
  print lc($_);
}


## Copy the Original ALT Training Data

(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/alignment/wat2020.km-en/alt$ cp train.alt.{en,km} ../../data/

## Preprocessing

(1) Lower Casing for English
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/alignment/data$ cat ./train.alt.en | perl ./lowercase.perl > train.alt.en.lc
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/alignment/data$ head ./train.alt.en.lc 
italy have defeated portugal 31-5 in pool c of the 2007 rugby world cup at parc des princes, paris, france.
andrea masi opened the scoring in the fourth minute with a try for italy.
despite controlling the game for much of the first half, italy could not score any other tries before the interval but david bortolussi kicked three penalties to extend their lead.
portugal never gave up and david penalva scored a try in the 33rd minute, providing their only points of the match.
italy led 16-5 at half time but were matched by portugal for much of the second half.
however bortolussi scored his fourth penalty of the match, followed by tries from mauro bergamasco and a second from andrea masi to wrap up the win for italy.
currently third in pool c with eight points, italy face a tough match against second placed scotland on 29 september.
new zealand lead the group with ten points, ahead of scotland on points difference.
portugal are bottom of the group with no points, behind romania with one.
some personal details of 3 million british learner drivers who had applied for the 'theory test' component of their driving licence have been lost in iowa, in the usa.
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/alignment/data$ 

(2) Tokenization for English

(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/alignment/data$ python ./spacy-seg.py ./train.alt.en.lc > ./train.alt.en.lc.seg
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/alignment/data$ head ./train.alt.en.lc.seg 
italy have defeated portugal 31 - 5 in pool c of the 2007 rugby world cup at parc des princes , paris , france .
andrea masi opened the scoring in the fourth minute with a try for italy .
despite controlling the game for much of the first half , italy could not score any other tries before the interval but david bortolussi kicked three penalties to extend their lead .
portugal never gave up and david penalva scored a try in the 33rd minute , providing their only points of the match .
italy led 16 - 5 at half time but were matched by portugal for much of the second half .
however bortolussi scored his fourth penalty of the match , followed by tries from mauro bergamasco and a second from andrea masi to wrap up the win for italy .
currently third in pool c with eight points , italy face a tough match against second placed scotland on 29 september .
new zealand lead the group with ten points , ahead of scotland on points difference .
portugal are bottom of the group with no points , behind romania with one .
some personal details of 3 million british learner drivers who had applied for the ' theory test ' component of their driving licence have been lost in iowa , in the usa .
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/alignment/data$ 

## Check the filesize of both source and target

(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/alignment/data$ wc ./train.alt.km 
  18088  643785 8088870 ./train.alt.km
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/alignment/data$ wc ./train.alt.en.lc.seg 
  18088  477318 2578619 ./train.alt.en.lc.seg
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/alignment/data$ 

It looks OK ...  

## Change Filenames 

This step is optional ...

(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/alignment/data$ cp ./preprocessing/train.alt.km .
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/alignment/data$ cp ./preprocessing/train.alt.en.lc.seg .
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/alignment/data$ ls
preprocessing  train.alt.en.lc.seg  train.alt.km
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/alignment/data$ mv train.alt.km train.km
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/alignment/data$ mv train.alt.en.lc.seg train.en
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/alignment/data$ 

## Alignment with GIZA++ Toolkit

When I run on my local laptop with the whole corpus, it tooks around 20 minutes. The reason might be I am also running many jupyter notebooks on my local notebook. And thus, I installed GIZA++ toolkit on CADT server and run demo on server.

(base) rnd@gpu:~/demo/alignment$ time ./align-GIZA++.sh train.en train.km align-output | tee alignment.log.txt
...
...
...
Entire Viterbi H3333344444 Training took: 144 seconds
==========================================================
writing decoder configuration file to align-output/Result.Decoder.config
Writing PERPLEXITY report to: align-output/Result.perp
Writing source vocabulary list to : align-output/Result.trn.src.vcb
Writing source vocabulary list to : align-output/Result.trn.trg.vcb
Writing source vocabulary list to : align-output/Result.tst.src.vcb
Writing source vocabulary list to : align-output/Result.tst.trg.vcb

Entire Training took: 220 seconds
Program Finished at: Mon Apr  3 23:48:22 2023

==========================================================
##########
finished ...
ls ./align-output/*.final
./align-output/Result.A3.final
./align-output/Result.D4.final
./align-output/Result.a3.final
./align-output/Result.d3.final
./align-output/Result.d4.final
./align-output/Result.n3.final
./align-output/Result.p0_3.final
./align-output/Result.t3.final
##########
Note by Ye ...
output folder name: align-output
GIZA++ learns the translation tables of IBM Model 4, but we are only interested in ".A3.final"

real    9m13.053s
user    9m9.801s
sys     0m2.363s

## Let's Check the Output Folder

(base) rnd@gpu:~/demo/alignment$ ls ./align-output/
Result.A3.final        Result.a3.final  Result.gizacfg     Result.perp         Result.trn.trg.vcb
Result.D4.final        Result.d3.final  Result.n3.final    Result.t3.final     Result.tst.src.vcb
Result.Decoder.config  Result.d4.final  Result.p0_3.final  Result.trn.src.vcb  Result.tst.trg.vcb
(base) rnd@gpu:~/demo/alignment$ 

## The Alignment File 

(base) rnd@gpu:~/demo/alignment/align-output$ head ./Result.A3.final 
# Sentence pair (1) source length 25 target length 32 alignment score : 1.30476e-53
អ៊ីតាលី បាន ឈ្នះ លើ ព័រទុយហ្គាល់ 31-5 ក្នុង ប៉ូល C នៃ ពិធី ប្រកួត ពាន រង្វាន់ ពិភព លោក នៃ កីឡា បាល់ ឱប ឆ្នាំ 2007 ដែល ប្រព្រឹត្ត នៅ ប៉ាស ឌេស ប្រីន ក្រុង ប៉ារីស បារាំង ។ 
NULL ({ 2 17 23 25 }) italy ({ 1 }) have ({ }) defeated ({ 3 4 }) portugal ({ 5 }) 31 ({ }) - ({ }) 5 ({ }) in ({ 7 }) pool ({ }) c ({ 9 }) of ({ 10 }) the ({ }) 2007 ({ 21 22 }) rugby ({ 18 19 20 }) world ({ 15 16 }) cup ({ 12 13 14 }) at ({ }) parc ({ 6 8 11 24 }) des ({ }) princes ({ 26 27 28 }) , ({ }) paris ({ 29 30 }) , ({ }) france ({ 31 }) . ({ 32 }) 
# Sentence pair (2) source length 15 target length 17 alignment score : 1.07162e-31
អេនត្រា ម៉ាស៊ី បាន ស៊ុត ចូល ក្នុង នាទី ទី បួន គ្រា ដំបូង នៃ ពាក់ កណ្តាល សំរាប់ អ៊ីតាលី ។ 
NULL ({ 3 }) andrea ({ 1 10 11 12 13 14 }) masi ({ 2 4 5 }) opened ({ }) the ({ }) scoring ({ }) in ({ 6 }) the ({ }) fourth ({ 8 9 }) minute ({ 7 }) with ({ }) a ({ }) try ({ }) for ({ 15 }) italy ({ 16 }) . ({ 17 }) 
# Sentence pair (3) source length 32 target length 44 alignment score : 1.66617e-82
ទោះបី បាន គ្រប់ គ្រង ក្នុង គ្រា ដំបូង នៃ វគ្គ ពាក់ កណ្តាល ដំបូង ក៏ ដោយ អ៊ីតាលី មិន បាន បន្ថែម ពិន្ទុ មុន នឹង សំរាក បាន ឡើយ តែ ដេវីត បូតុលូសស៊ី បាន ទាត់ ចូល ៣ គ្រាប់ នៃ បាល់ ពិន័យ ហើយ ពង្វាត បន្ថែម ទៀត នៃ ការ នាំ មុខ ។ 
NULL ({ 2 5 8 17 21 23 28 41 }) despite ({ 1 }) controlling ({ 3 4 6 }) the ({ }) game ({ }) for ({ }) much ({ }) of ({ }) the ({ }) first ({ 7 12 }) half ({ 9 10 11 }) , ({ 13 14 }) italy ({ 15 }) could ({ }) not ({ 16 }) score ({ }) any ({ }) other ({ }) tries ({ 18 19 }) before ({ 20 }) the ({ }) interval ({ 22 24 }) but ({ 25 }) david ({ 26 }) bortolussi ({ 27 30 31 32 33 36 37 38 40 }) kicked ({ 29 }) three ({ }) penalties ({ 34 35 }) to ({ }) extend ({ 39 }) their ({ }) lead ({ 42 43 }) . ({ 44 }) 
# Sentence pair (4) source length 23 target length 29 alignment score : 2.62978e-54
(base) rnd@gpu:~/demo/alignment/align-output$ 

## Reference

https://okapiframework.org/wiki/index.php/GIZA%2B%2B_Installation_and_Running_Tutorial

https://fabioticconi.wordpress.com/2011/01/17/how-to-do-a-word-alignment-with-giza-or-mgiza-from-parallel-corpus/

https://www.mail-archive.com/search?l=moses-support@mit.edu&q=subject:%22Re%5C%3A+%5C%5BMoses%5C-support%5C%5D+Error+in+training+phrase%22&o=newest&f=1

