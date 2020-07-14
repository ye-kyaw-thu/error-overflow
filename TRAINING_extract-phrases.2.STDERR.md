# Example Error Relating to Myanmar-Braille SMT

SMTလုပ်တဲ့ ကျောင်းသားတွေ လေ့လာနိုင်အောင် example အဖြစ် တင်ထားပေးထားတာပါ။  
Output of "TRAINING_extract-phrases.2.STDERR".  

```
Using SCRIPTS_ROOTDIR: /home/ye/tool/moses-bin/ubuntu-17.04/moses/scripts
using gzip 
(5) extract phrases @ Tue Jul 14 10:47:28 +0630 2020
/home/ye/tool/moses-bin/ubuntu-17.04/moses/scripts/generic/extract-parallel.perl 4 split "sort    " /home/ye/tool/moses-bin/ubuntu-17.04/moses/scripts/../bin/extract /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/training/corpus.1.br /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/training/corpus.1.my /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/aligned.1.grow-diag-final-and /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/extract.2 5 orientation --model wbe-msd --GZOutput 
Executing: /home/ye/tool/moses-bin/ubuntu-17.04/moses/scripts/generic/extract-parallel.perl 4 split "sort    " /home/ye/tool/moses-bin/ubuntu-17.04/moses/scripts/../bin/extract /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/training/corpus.1.br /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/training/corpus.1.my /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/aligned.1.grow-diag-final-and /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/extract.2 5 orientation --model wbe-msd --GZOutput 
using gzip 
isBSDSplit=0 
Executing: mkdir -p /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/tmp.24516; ls -l /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/tmp.24516 
split -d -l 1169 -a 7 /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/training/corpus.1.my /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/tmp.24516/source.split -d -l 1169 -a 7 /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/training/corpus.1.br /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/tmp.24516/target.split -d -l 1169 -a 7 /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/aligned.1.grow-diag-final-and /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/tmp.24516/align.merging extract / extract.inv
gunzip -c /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/tmp.24516/extract.0000000.gz /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/tmp.24516/extract.0000001.gz /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/tmp.24516/extract.0000002.gz /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/tmp.24516/extract.0000003.gz  | LC_ALL=C sort     -T /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/tmp.24516 2>> /dev/stderr | gzip -c > /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/extract.2.sorted.gz 2>> /dev/stderr 
gunzip -c /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/tmp.24516/extract.0000000.inv.gz /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/tmp.24516/extract.0000001.inv.gz /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/tmp.24516/extract.0000002.inv.gz /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/tmp.24516/extract.0000003.inv.gz  | LC_ALL=C sort     -T /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/tmp.24516 2>> /dev/stderr | gzip -c > /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/extract.2.inv.sorted.gz 2>> /dev/stderr 
gunzip -c /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/tmp.24516/extract.0000000.o.gz /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/tmp.24516/extract.0000001.o.gz /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/tmp.24516/extract.0000002.o.gz /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/tmp.24516/extract.0000003.o.gz  | LC_ALL=C sort     -T /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/tmp.24516 2>> /dev/stderr | gzip -c > /media/ye/Transcend/exp/my-braille/exp1/1/baseline/my-br/model/extract.2.o.sorted.gz 2>> /dev/stderr 
Finished Tue Jul 14 10:47:33 2020
 liek' .*1 :ta1 < k5iek' k t*1 tie1 :ta r>a mxa mie2 < ka p/' yc jk' 6[ k jn'2 r>k' nx/'1 6/' ?('1 <im' .5ce t/'2 jim' n>a2 :r ./'2 lie1 (v'1 t>/'2 p :l> :k9a0 nx/'1 :^9a0 p;a1 my' :l2 4
ERROR: some opened tags were never closed: .k' 6s' < ^>/'1
ERROR: some opened tags were never closed: 6n' s p;a2 ?(' k9>n'ep' tie1 nie/' /c o < ?k' :?>2 :k5a ^5s' ?(' 4
ERROR: malformed XML: :%a fi :r>x :k9a/'2 < :rx1 kie :l9xak' p;a lie1 < :nak' kie t*1 :m9xa0 liek' r/' 4
no target (0) or source (18) words << end insentence 1177
T: :%a fi :r>x :k9a/'2 < :rx1 kie :l9xak' p;a lie1 < :nak' kie t*1 :m9xa0 liek' r/' 4
S: ဗော ဓိ ရွှေ ကျောင်း အ ရှေ့ ကို လျှောက် ပါ လို့ အ နောက် ကို တဲ့ မျှော် လိုက် ရင် ။
ERROR: some opened tags were never closed: k9>n' m tie1 ?(' sa <ep' m9a2 kie rie :? s>a kie/' t>y' ^t' rxe k5 p;a ?(' sa ^t' .n'2 t>/' 6u 6u (c (c m lep' k5 b* tit' 6it' s>a sa ^t' k5 p;a ?(' 4
ERROR: some opened tags were never closed: #c 4 t ra2 k9 ;7 < :ka/'2 < 6ie2 kie .>* .5a2 ?i m5/' ?(' 4
ERROR: malformed XML: 7 . 7 m(' ?('1 < .;a t>/' :<a/' ju p5[ he :<a0 nie/' ? n('2 4
ERROR: some opened tags were never closed: 7 . 7 m(' ?('1 < .;a t>/' :<a/' ju p5[ he :<a0 nie/' ? n('2 4
ERROR: some opened tags were never closed: %iel' .9ep' :<a/' 6n'2 ha tk-k ?iel' mxa p (a ?/' k5a2 :n ten'2 mxa p* :k9a/'2 ?a2 < :r2 kis-s :t> kie ;e[2 :6a/' p5[2 :6a/' r>k' :p2 ty' 4
ERROR: some opened tags were never closed: m :ha0 ? fa ?e . min' ?(' jie ?u nxs' :yak' kie :.;a0 :.9 he :s liek' ? ^5/'1 ^>a2 ^k' :r> :^a0 tie1 :.;a0 .*1 & jie ?u nxs' :yak' tie1 la lt' :?a0 be ra2 :la/'2 ?(' ;[ ?u ka2 ?u ts' p;a2 kie .n'1 (a2 :k5ak' r>c1 .5/'2 t sie2 t si m9x m rxi < l>n' r* r/'1 o 4
PhraseExtract v1.5, written by Philipp Koehn et al.
phrase extraction from an aligned parallel corpus
ERROR: some opened tags were never closed: y .e < .;a pe ?im' j[2 :6a/'2 ?u n('2 p;a2 ?>a2 p5[ ^5s' ?(' 4
PhraseExtract v1.5, written by Philipp Koehn et al.
phrase extraction from an aligned parallel corpus
ERROR: malformed XML: #ac 4 :.9a/'2 :.9a/'2 ;7 < m5* m p5t' < rip' < .5(' k5('1 & 4
no target (0) or source (16) words << end insentence 2
T: #ac 4 :.9a/'2 :.9a/'2 ;7 < m5* m p5t' < rip' < .5(' k5('1 & 4
S: ၁၃ ။ ချောင်း ချောင်း = အ မြဲ မ ပြတ် အ ရိပ် အ ခြည် ကြည့် ၍ ။
ERROR: malformed XML: < t>/'2 < p5/' lu < :p;a/'2 tie1 l('2 .9s' lie nxs' ?k' .5/'2 rxi k5 ken' o 4
ERROR: some opened tags were never closed: ERROR: some opened tags were never closed: :la/' sa < t>k' j/'2 kie l('2 r rxi ?(' 4< t>/'2 < p5/' lu < :p;a/'2 tie1 l('2 .9s' lie nxs' ?k' .5/'2 rxi k5 ken' o 4

ERROR: some opened tags were never closed: .k' 6s' < ^>/'1
ERROR: some opened tags were never closed: #c 4 :<ak' p;a :m2 .>n'2 m9a2 kie :^5 p;a 4
ERROR: malformed XML: 7 g 7 .5":?1 ?(' piek' mx l>t' :<a/' m ren'2 nie/' ? ^5/'1 - - - :<a0 hs' :l o 4
ERROR: some opened tags were never closed: no target (0) or source (22) words << end insentence 2341
T: 7 g 7 .5":?1 ?(' piek' mx l>t' :<a/' m ren'2 nie/' ? ^5/'1 - - - :<a0 hs' :l o 4
S: ( ဂ ) ခြင်္သေ့ သည် ပိုက် မှ လွတ် အောင် မ ရုန်း နိုင် သ ဖြင့် - - - အော် ဟစ် လေ ၏ ။
ERROR: malformed XML: jie < .;a wi :d h raz' tie/'2 ?(' be ra2 p>/'1 :ta0 mu :?a < .;a k*1 ?ie1 m9a2 :?a <a2 ^5/'1 het' mxn' :?a t ra2 < k9/'1 tie1 8 ?a t(' ken' o 4
ERROR: some opened tags were never closed: jie < .;a wi :d h raz' tie/'2 ?(' be ra2 p>/'1 :ta0 mu :?a < .;a k*1 ?ie1 m9a2 :?a <a2 ^5/'1 het' mxn' :?a t ra2 < k9/'1 tie1 8 ?a t(' ken' o 4
ERROR: malformed XML: jie :m5 nn'2 p5 ?ad' :ta0 k5[2 < t>/'2 8 < .n'2 m9a2 .>* .5a2 ja2 ?(' 4ERROR: malformed XML: #b 4 ^n' ^n' ;7 < k5im' k5im' 4
no target (0) or source (9) words << end insentence 3514
T: #b 4 ^n' ^n' ;7 < k5im' k5im' 4
S: ၂ ။ ဖန် ဖန် = အ ကြိမ် ကြိမ် ။
ERROR: malformed XML: :lx :lxa0 :lx .t' nx/'1 < tt' ky' m*1 ?u mxa wn' jm'2 ?a ^5s' m5* 3 p (a rx/' ^5s' :p k lu1 p5(' mxa pu :za0 lie1 zm-%u :p;a0 ge$' j/' p lim'1 m(' mie2 l jk' k* 4
< ?/' < lie rxi :?a ?s' ?[2 kie yu .*1 p;a p5[ 4
ERROR: some opened tags were never closed: no target (0) or source (41) words << end insentence 3515
T: :lx :lxa0 :lx .t' nx/'1 < tt' ky' m*1 ?u mxa wn' jm'2 ?a ^5s' m5* 3 p (a rx/' ^5s' :p k lu1 p5(' mxa pu :za0 lie1 zm-%u :p;a0 ge$' j/' p lim'1 m(' mie2 l jk' k* 4
S: လှေ လှော် လှေ ခတ် နှင့် အ တတ် ကယ် မဲ့ သူ မှာ ဝန် ထမ်း သာ ဖြစ် မြဲ ၊ ပ ညာ ရှင် ဖြစ် ပေ က လူ့ ပြည် မှာ ပူ ဇော် လို့ ဇမ္ဗူ ပေါ် ဂုဏ် ထင် ပ လိမ့် မည် မိုး လ ထက် ကဲ ။
ERROR: some opened tags were never closed: jie1 < p5/' j[2 r>k' kp' rn' j[2 lk' tc :.;a0 w;a2 sit' /y' m9a2 l('2 rxi r ?(' 4
ERROR: malformed XML: #h 4 k9p' .ie2 .c ;7 m[2 ^ie < jk' t>/' lep' ja2 :?a s/' 7 k9p' s/' 7 t>/' ?a2 :ka/' m9a2 kie < :.5ak' .c ?(' 4
ERROR: some opened tags were never closed: #h 4 k9p' .ie2 .c ;7 m[2 ^ie < jk' t>/' lep' ja2 :?a s/' 7 k9p' s/' 7 t>/' ?a2 :ka/' m9a2 kie < :.5ak' .c ?(' 4
ERROR: malformed XML: 
no target (0) or source (14) words << end insentence 8het' p;a bu2 :< 3 ^n' 6>t' :r ?"kn'2 4ERROR: malformed XML: mi ns' ?ce2 6y' k5a :?a < .;a p j m pie/'2 < .9in' :s1 & 6y' mi ns' < na2 :p2 p;a ?(' 4

#c 4 wxn' tk' ;7 < jk' ?ie1 p9c1 nxc1 ?(' 4
T: 
no target (0) or source (12) words << end insentence 1188
T: #c 4 wxn' tk' ;7 < jk' ?ie1 p9c1 nxc1 ?(' 4
S: ၃ ။ ဝှန် တက် = အ ထက် သို့ ပျံ့ နှံ့ သည် ။ERROR: some opened tags were never closed: no target (< ?/' < lie rxi :?a ?s' ?[2 kie yu .*1 p;a p5[ 4
#c 4 :<ak' p;a :m2 .>n'2 m9a2 kie :^5 6ie p;a 4
ERROR: malformed XML: lu k5[2 mi b 6 ra ? ma2 tie1 k ps-s('2 :p2 l9x/' < na2 ?ie1 kp' & lk' nxs' ^k' ^5/'1 rie rie :? :? :p2 r ?(' 4
no target (0) or source (30) words << end insentence 1190
T: lu k5[2 mi b 6 ra ? ma2 tie1 k ps-s('2 :p2 l9x/' < na2 ?ie1 kp' & lk' nxs' ^k' ^5/'1 rie rie :? :? :p2 r ?(' 4
S: 0
ERROR: malformed XML: လူ ကြီး မိ ဘ ဆ ရာ သ မား တို့ က ပစ္စည်း ပေး လျှင် အ နား သို့ ကပ် ၍ လက် နှစ် ဖက် ဖြင့် ရို ရို သေ သေ ပေး ရ သည် ။) or source (S: :.9a liek' :l lie1 :p5a r m la2 :<ak' :m1 ja2 p;a ty' 4
25အ သင် အ လို ရှိ သော သစ် သီး ကို ယူ ခဲ့ ပါ ပြီ ။
no target (0) or source (14) words << end insentence 2346
T: :.9a liek' :l lie1 :p5a r m la2 :<ak' :m1 ja2 p;a ty' 4
S: ချော လိုက် လေ လို့ ပြော ရ မ လား အောက် မေ့ ထား ပါ တယ် ။
ERROR: malformed XML: lu tie1 l('2 m ps' .t' wc1 & m/'2 <a2 k5a2 :l9ak' o 4
no target (0) or source (14) words << end insentence 2347
T: lu tie1 l('2 m ps' .t' wc1 & m/'2 <a2 k5a2 :l9ak' o 4
S: လူ တို့ လည်း မ ပစ် ခတ် ဝံ့ ၍ မင်း အား ကြား လျောက် ၏ ။
ERROR: malformed XML: ;[ ?ie1 pt' wie/'2 nx/'1 6ie/'2 wie/'2 tie1 ?(' ? :ba .9/'2 tu ([ :?a0 l('2 y .e < .;a t>/' 6ie/'2 wie/'2 he 6ie liek' l9x/' pt' wie/'2 k5[2 < p;a < w/'+ nx/'1 < tu t>* ^k' t[2 mxet' r ?('1 tu ri ya m9a2 p;a w/' :?a < t[2 3 < mxet' 4
ERROR: some opened tags were never closed: ) words << end insentence 
ERROR: malformed XML: ;[ ?ie1 pt' wie/'2 nx/'1 6ie/'2 wie/'2 tie1 ?(' ? :ba .9/'2 tu ([ :?a0 l('2 y .e < .;a t>/' 6ie/'2 wie/'2 he 6ie liek' l9x/' pt' wie/'2 k5[2 < p;a < w/'+ nx/'1 < tu t>* ^k' t[2 mxet' r ?('1 tu ri ya m9a2 p;a w/' :?a < t[2 3 < mxet' 43519ERROR: malformed XML: #f 4 m[2 .9it' ;7 m[2 :la/' :?a < ra kie 6>* .9 /5im'2 ?t' rn' < rie2 rx(' tp' ja2 :?a ?c :kak' s ?(' 4

jie ?u kie r l9x/' ?/' tie1 m sie2 rim' l/'1 he 6ie & m/'2 k5[2 <a2 :l9xak' ja2 wc1 :?a ?u kie :.;a0 :s & jie ?u :rak' l9x/' m/'2 k5[2 <a2 :l9xak' ja2 sim'1 :?a /xa m :ha0 ? fa ?e . min' ?(' ;[ ?ie1 mxa ja2 o 4
T: 
ERROR: some opened tags were never closed: mi ns' ?ce2 6y' k5a :?a < .;a p j m pie/'2 < .9in' :s1 & 6y' mi ns' < na2 :p2 p;a ?(' 4no target (#f 4 m[2 .9it' ;7 m[2 :la/' :?a < ra kie 6>* .9 /5im'2 ?t' rn' < rie2 rx(' tp' ja2 :?a ?c :kak' s ?(' 4
0
S: ) or source (မိ နစ် သုံး ဆယ် ကြာ သော အ ခါ ပ ထ မ ပိုင်း အ ချိန် စေ့ ၍ ဆယ် မိ နစ် အ နား ပေး ပါ သည် ။52
) words << end insentence 9
T: jie ?u kie r l9x/' ?/' tie1 m sie2 rim' l/'1 he 6ie & m/'2 k5[2 <a2 :l9xak' ja2 wc1 :?a ?u kie :.;a0 :s & jie ?u :rak' l9x/' m/'2 k5[2 <a2 :l9xak' ja2 sim'1 :?a /xa m :ha0 ? fa ?e . min' ?(' ;[ ?ie1 mxa ja2 o 4
ERROR: some opened tags were never closed: S: #a 4 :yak' m ;7 :ya/'2 m he < ?c j>k' p;a 4ထို သူ ကို ရ လျှင် သင် တို့ မ စိုး ရိမ် လင့် ဟု ဆို ၍ မင်း ကြီး အား လျှောက် ထား ဝံ့ သော သူ ကို ခေါ် စေ ၍ ထို သူ ရောက် လျှင် မင်း ကြီး အား လျှောက် ထား စိမ့် သော ငှာ မ ဟော် သ ဓာ သု ခ မိန် သည် ဤ သို့ မှာ ထား ၏ ။

ERROR: malformed XML: tie/' jip' ?ie1 nie/' /c :ta0 < lc :rak' l9x/' t(' /5im' rie :? s>a < :l2 p5e k5 ?(' 4
ERROR: some opened tags were never closed: tie/' jip' ?ie1 nie/' /c :ta0 < lc :rak' l9x/' t(' /5im' rie :? s>a < :l2 p5e k5 ?(' 4
ERROR: malformed XML: tie/'2 r/'2 ?a2 < .9/'2 .9/'2 ts' ;e[2 nx/'1 ts' ;e[2 na2 l(' mxe l('2 r nie/' ?(' 4
no target (0) or source (19) words << end insentence 1193
T: tie/'2 r/'2 ?a2 < .9/'2 .9/'2 ts' ;e[2 nx/'1 ts' ;e[2 na2 l(' mxe l('2 r nie/' ?(' 4
S: တိုင်း ရင်း သား အ ချင်း ချင်း တစ် ဦး နှင့် တစ် ဦး နား လည် မှု လည်း ရ နိုင် သည် ။ERROR: malformed XML: pie2 m>xa2 m9a2 k/'2 rx/'2 :<a/' jce2 mxen'1 ^5u2 :p2 r ?(' 4
no target (0) or source (13) words << end insentence 11
T: pie2 m>xa2 m9a2 k/'2 rx/'2 :<a/' jce2 mxen'1 ^5u2 :p2 r ?(' 4
S: ပိုး မွှား များ ကင်း ရှင်း အောင် ထုံး မှုန့် ဖြူး ပေး ရ သည် ။
ERROR: some opened tags were never closed: .k' 6s' < ^>/'1
ERROR: malformed XML: ;[ kis-s t>/' k9>n'ep' o :p;a1 p;a2 ^9t' lt' .5/'2 ?(' ?a l9x/' < ?ce2 k9 o 4
no target (0) or source (18) words << end insentence 13
T: ;[ kis-s t>/' k9>n'ep' o :p;a1 p;a2 ^9t' lt' .5/'2 ?(' ?a l9x/' < ?ce2 k9 o 4
S: ဤ ကိစ္စ တွင် ကျွန်ုပ် ၏ ပေါ့ ပါး ဖျတ် လတ် ခြင်း သည် သာ လျှင် အ သုံး ကျ ၏ ။
ERROR: malformed XML: 7 #c 7 <i ti :ka/'2 mie2 :?ak' j 3 sa2 ti :ka/'2 mxn'2 .9ie2 s 4
no target (0) or source (17) words << end insentence 14
T: 7 #c 7 <i ti :ka/'2 mie2 :?ak' j 3 sa2 ti :ka/'2 mxn'2 .9ie2 s 4
S: ( ၃ ) အိ တိ ကောင်း မိုး သောက် ထ ၊ စား တိ ကောင်း မှန်း ချိုး စ ။

ERROR: some opened tags were never closed: y ./' k pe ?im' j[2 kie w;a2 pit' tie1 ^5/'1 ?a lep' .*1 :?a0 l('2 y .e < .;a :.t' nx/'1 < ([ lx p .ie/' .c1 & < 6/'1 < tn'2 m5/'1 la :<a/' < m9ie2 m9ie2 t[ j>/' lep' :6a/' ?/'1 :p ?(' 4
ERROR: some opened tags were never closed: /;a1 8 < r>y' m :rak' :?2 :?a :k92 ?a2 /y' tie1 ?(' rxi ken' o 4
ERROR: malformed XML: p5[2 l9x/' < rp' kie :w p;a ?(' 4
no target (0) or source (9) words << end insentence 1198
T: p5[2 l9x/' < rp' kie :w p;a ?(' 4
S: ပြီး လျှင် အ ရပ် ကို ဝေ ပါ သည် ။
ERROR: some opened tags were never closed: m :ha0 ? fa ?e . min' ?(' m/'2 k5[2 sa nx/'1 n>a2 la2 kie wi bz-z %9a k r $ ^5 /'1 :^5 .5/'2 /xa m jiek' p \i pes-6a %9a k r $ ^5/'1 :m2 tce1 :m2 & :^5 .5/'2 /xa jiek' o he k5c p5[2 :?a0 r>a ?a2 < :p;a/'2 tie1 3 ?/' tie1 ?(' m/'2 k5[2 nx/'1 < k9>m'2 w/' ?(' ^5s' & r* r/'1 s>a m/'2 k5[2 <a2 m :k5ak' m r>c1 :l9xak' ja2 wc1 :?a ?u kie r nie/' p;a m(' :la he :m2 o 4
ERROR: malformed XML: die/'2 6e k5[2 kie p j m gie2 ?>/'2 :?a k9>n' :ta0 tie1 r>a < ?/'2 k p j m :.5ak' l jin'2 ?im'2 r p;a m(' 4
no target (0) or source (28) words << end insentence 18
T: die/'2 6e k5[2 kie p j m gie2 ?>/'2 :?a k9>n' :ta0 tie1 r>a < ?/'2 k p j m :.5ak' l jin'2 ?im'2 r p;a m(' 4
S: ဒိုင်း ဆု ကြီး ကို ပ ထ မ ဂိုး သွင်း သော ကျွန် တော် တို့ ရွာ အ သင်း က ပ ထ မ ခြောက် လ ထိန်း သိမ်း ရ ပါ မည် ။
```
