# Error building a language model with Kenlm

```
$ lmplz -o 3 < ./bookmar.zh-my.f2 > ./bookmar.zh-my.f2.arpa
=== 1/5 Counting and sorting n-grams ===
Reading /media/lar/Transcend/talk/demo-en/my-syl-checker/perl-code/substring/syl-lm/kenlm-tst/tst-tmp/bookmar.zh-my.f2
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
****************************************************************************************************
/home/lar/tool/kenlm/util/scoped.cc:20 in void* util::{anonymous}::InspectAddr(void*, std::size_t, const char*) threw MallocException because `!addr && requested'.
Cannot allocate memory for 5067657200 bytes in malloc
Aborted (core dumped)
```

# Use -S option

```
lar@lar-air:/media/lar/Transcend/talk/demo-en/my-syl-checker/perl-code/substring/syl-lm/kenlm-tst/tst-tmp$ lmplz -S 10% -o 3 < ./bookmar.zh-my.f2 > ./bookmar.zh-my.f2.arpa
=== 1/5 Counting and sorting n-grams ===
Reading /media/lar/Transcend/talk/demo-en/my-syl-checker/perl-code/substring/syl-lm/kenlm-tst/tst-tmp/bookmar.zh-my.f2
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
****************************************************************************************************
Unigram tokens 473780 types 26532
=== 2/5 Calculating and sorting adjusted counts ===
Chain sizes: 1:318384 2:287416224 3:538905408
Statistics:
1 26532 D1=0.711925 D2=0.98516 D3+=1.44059
2 149588 D1=0.782511 D2=1.12265 D3+=1.36236
3 284979 D1=0.854926 D2=1.17796 D3+=1.39277
Memory estimate for binary LM:
type       kB
probing  9189 assuming -p 1.5
probing 10169 assuming -r models -p 1.5
trie     3993 without quantization
trie     2338 assuming -q 8 -b 8 quantization 
trie     3790 assuming -a 22 array pointer compression
trie     2135 assuming -a 22 -q 8 -b 8 array pointer compression and quantization
=== 3/5 Calculating and sorting initial probabilities ===
Chain sizes: 1:318384 2:2393408 3:5699580
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
####################################################################################################
=== 4/5 Calculating and writing order-interpolated probabilities ===
Chain sizes: 1:318384 2:2393408 3:5699580
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
####################################################################################################
=== 5/5 Writing ARPA model ===
----5---10---15---20---25---30---35---40---45---50---55---60---65---70---75---80---85---90---95--100
****************************************************************************************************
Name:lmplz	VmPeak:985864 kB	VmRSS:14480 kB	RSSMax:215772 kB	user:0.441743	sys:0.317368	CPU:0.759155	real:0.923923
```
