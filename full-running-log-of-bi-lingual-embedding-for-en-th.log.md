# Full Running Log of Bi-lingual Embedding for English-Thai

English-Thai bi-lingual embedding experiment (Vector Size: 500, Window: 4, Min_Count: 2, Iteration: 10, Experiment Folder#: 16) တစ်ခု run စဉ်က log ပါ။  

```
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ time ./repeat-train-eval-myen.sh 500 4 2 10 16 en th
build word2vec or fasttext model ...
change python environment...
start building a word2vec model for SRC language ...  
2021-09-30 11:12:28,667 : INFO : collecting all words and their counts
2021-09-30 11:12:31,413 : INFO : PROGRESS: at sentence #0, processed 0 words, keeping 0 word types
2021-09-30 11:12:32,642 : INFO : PROGRESS: at sentence #10000, processed 856417 words, keeping 37157 word types
2021-09-30 11:12:33,755 : INFO : PROGRESS: at sentence #20000, processed 1639648 words, keeping 57687 word types
2021-09-30 11:12:35,010 : INFO : PROGRESS: at sentence #30000, processed 2572059 words, keeping 74632 word types
2021-09-30 11:12:36,332 : INFO : PROGRESS: at sentence #40000, processed 3530495 words, keeping 93905 word types
2021-09-30 11:12:37,760 : INFO : PROGRESS: at sentence #50000, processed 4532267 words, keeping 110510 word types
2021-09-30 11:12:38,964 : INFO : PROGRESS: at sentence #60000, processed 5314109 words, keeping 120800 word types
2021-09-30 11:12:40,109 : INFO : PROGRESS: at sentence #70000, processed 6097063 words, keeping 130023 word types
2021-09-30 11:12:41,882 : INFO : PROGRESS: at sentence #80000, processed 7397249 words, keeping 143683 word types
2021-09-30 11:12:42,979 : INFO : PROGRESS: at sentence #90000, processed 8198407 words, keeping 148940 word types
2021-09-30 11:12:44,035 : INFO : PROGRESS: at sentence #100000, processed 8959383 words, keeping 157723 word types
2021-09-30 11:12:45,017 : INFO : PROGRESS: at sentence #110000, processed 9687655 words, keeping 164381 word types
2021-09-30 11:12:46,149 : INFO : PROGRESS: at sentence #120000, processed 10525118 words, keeping 171206 word types
2021-09-30 11:12:47,198 : INFO : PROGRESS: at sentence #130000, processed 11280108 words, keeping 177213 word types
2021-09-30 11:12:48,205 : INFO : PROGRESS: at sentence #140000, processed 12016743 words, keeping 182472 word types
2021-09-30 11:12:49,310 : INFO : PROGRESS: at sentence #150000, processed 12826975 words, keeping 188977 word types
2021-09-30 11:12:50,686 : INFO : PROGRESS: at sentence #160000, processed 13855182 words, keeping 194528 word types
2021-09-30 11:12:51,950 : INFO : PROGRESS: at sentence #170000, processed 14751080 words, keeping 199284 word types
2021-09-30 11:12:53,207 : INFO : PROGRESS: at sentence #180000, processed 15637158 words, keeping 207749 word types
2021-09-30 11:12:54,261 : INFO : PROGRESS: at sentence #190000, processed 16403465 words, keeping 213279 word types
2021-09-30 11:12:55,297 : INFO : PROGRESS: at sentence #200000, processed 17173239 words, keeping 217945 word types
2021-09-30 11:12:56,311 : INFO : PROGRESS: at sentence #210000, processed 17908845 words, keeping 222598 word types
2021-09-30 11:12:57,457 : INFO : PROGRESS: at sentence #220000, processed 18748603 words, keeping 228947 word types
2021-09-30 11:12:59,926 : INFO : PROGRESS: at sentence #230000, processed 20575993 words, keeping 258944 word types
2021-09-30 11:13:03,837 : INFO : PROGRESS: at sentence #240000, processed 23460183 words, keeping 289437 word types
2021-09-30 11:13:07,619 : INFO : PROGRESS: at sentence #250000, processed 26231994 words, keeping 314656 word types
2021-09-30 11:13:08,999 : INFO : PROGRESS: at sentence #260000, processed 27221411 words, keeping 328432 word types
2021-09-30 11:13:10,158 : INFO : PROGRESS: at sentence #270000, processed 28078797 words, keeping 334035 word types
2021-09-30 11:13:11,203 : INFO : PROGRESS: at sentence #280000, processed 28851753 words, keeping 337254 word types
2021-09-30 11:13:12,891 : INFO : PROGRESS: at sentence #290000, processed 30046848 words, keeping 343424 word types
2021-09-30 11:13:14,897 : INFO : PROGRESS: at sentence #300000, processed 31526004 words, keeping 350103 word types
2021-09-30 11:13:16,196 : INFO : PROGRESS: at sentence #310000, processed 32476995 words, keeping 357010 word types
2021-09-30 11:13:17,462 : INFO : PROGRESS: at sentence #320000, processed 33378244 words, keeping 363313 word types
2021-09-30 11:13:18,510 : INFO : PROGRESS: at sentence #330000, processed 34117385 words, keeping 369287 word types
2021-09-30 11:13:19,464 : INFO : PROGRESS: at sentence #340000, processed 34812365 words, keeping 374372 word types
2021-09-30 11:13:20,473 : INFO : PROGRESS: at sentence #350000, processed 35538094 words, keeping 378906 word types
2021-09-30 11:13:21,459 : INFO : PROGRESS: at sentence #360000, processed 36255461 words, keeping 383282 word types
2021-09-30 11:13:22,480 : INFO : PROGRESS: at sentence #370000, processed 36964781 words, keeping 388524 word types
2021-09-30 11:13:23,467 : INFO : PROGRESS: at sentence #380000, processed 37688733 words, keeping 392198 word types
2021-09-30 11:13:24,434 : INFO : PROGRESS: at sentence #390000, processed 38391799 words, keeping 395639 word types
2021-09-30 11:13:25,374 : INFO : PROGRESS: at sentence #400000, processed 39091452 words, keeping 399275 word types
2021-09-30 11:13:26,782 : INFO : PROGRESS: at sentence #410000, processed 40128198 words, keeping 406541 word types
2021-09-30 11:13:27,939 : INFO : PROGRESS: at sentence #420000, processed 40965191 words, keeping 411288 word types
2021-09-30 11:13:29,109 : INFO : PROGRESS: at sentence #430000, processed 41804806 words, keeping 418558 word types
2021-09-30 11:13:30,154 : INFO : PROGRESS: at sentence #440000, processed 42582172 words, keeping 426512 word types
2021-09-30 11:13:31,263 : INFO : PROGRESS: at sentence #450000, processed 43405228 words, keeping 432963 word types
2021-09-30 11:13:32,462 : INFO : PROGRESS: at sentence #460000, processed 44275969 words, keeping 438462 word types
2021-09-30 11:13:33,569 : INFO : PROGRESS: at sentence #470000, processed 45052117 words, keeping 444093 word types
2021-09-30 11:13:34,569 : INFO : PROGRESS: at sentence #480000, processed 45788235 words, keeping 449915 word types
2021-09-30 11:13:35,851 : INFO : PROGRESS: at sentence #490000, processed 46743365 words, keeping 455392 word types
2021-09-30 11:13:37,077 : INFO : PROGRESS: at sentence #500000, processed 47618987 words, keeping 459461 word types
2021-09-30 11:13:38,337 : INFO : PROGRESS: at sentence #510000, processed 48517973 words, keeping 466706 word types
2021-09-30 11:13:39,309 : INFO : PROGRESS: at sentence #520000, processed 49226448 words, keeping 469858 word types
2021-09-30 11:13:42,045 : INFO : PROGRESS: at sentence #530000, processed 51241838 words, keeping 501749 word types
2021-09-30 11:13:43,585 : INFO : PROGRESS: at sentence #540000, processed 52355129 words, keeping 509849 word types
2021-09-30 11:13:45,885 : INFO : PROGRESS: at sentence #550000, processed 54028410 words, keeping 518729 word types
2021-09-30 11:13:47,938 : INFO : PROGRESS: at sentence #560000, processed 55506699 words, keeping 526525 word types
2021-09-30 11:13:49,857 : INFO : PROGRESS: at sentence #570000, processed 56880618 words, keeping 532262 word types
2021-09-30 11:13:51,877 : INFO : PROGRESS: at sentence #580000, processed 58314262 words, keeping 537453 word types
2021-09-30 11:13:53,744 : INFO : PROGRESS: at sentence #590000, processed 59666884 words, keeping 542212 word types
2021-09-30 11:13:55,643 : INFO : PROGRESS: at sentence #600000, processed 61062281 words, keeping 548435 word types
2021-09-30 11:13:56,742 : INFO : PROGRESS: at sentence #610000, processed 61865180 words, keeping 554018 word types
2021-09-30 11:13:57,878 : INFO : PROGRESS: at sentence #620000, processed 62676312 words, keeping 558491 word types
2021-09-30 11:13:59,044 : INFO : PROGRESS: at sentence #630000, processed 63514480 words, keeping 562733 word types
2021-09-30 11:14:00,157 : INFO : PROGRESS: at sentence #640000, processed 64316617 words, keeping 570041 word types
2021-09-30 11:14:01,215 : INFO : PROGRESS: at sentence #650000, processed 65083808 words, keeping 575243 word types
2021-09-30 11:14:02,328 : INFO : PROGRESS: at sentence #660000, processed 65887991 words, keeping 581842 word types
2021-09-30 11:14:03,594 : INFO : PROGRESS: at sentence #670000, processed 66754003 words, keeping 588822 word types
2021-09-30 11:14:04,988 : INFO : PROGRESS: at sentence #680000, processed 67749136 words, keeping 599561 word types
2021-09-30 11:14:06,812 : INFO : PROGRESS: at sentence #690000, processed 69074992 words, keeping 614237 word types
2021-09-30 11:14:07,879 : INFO : PROGRESS: at sentence #700000, processed 69843721 words, keeping 618301 word types
2021-09-30 11:14:08,959 : INFO : PROGRESS: at sentence #710000, processed 70624501 words, keeping 624489 word types
2021-09-30 11:14:09,969 : INFO : PROGRESS: at sentence #720000, processed 71354447 words, keeping 627874 word types
2021-09-30 11:14:10,816 : INFO : PROGRESS: at sentence #730000, processed 71984100 words, keeping 630330 word types
2021-09-30 11:14:11,768 : INFO : PROGRESS: at sentence #740000, processed 72677704 words, keeping 633269 word types
2021-09-30 11:14:12,852 : INFO : PROGRESS: at sentence #750000, processed 73444285 words, keeping 637636 word types
2021-09-30 11:14:14,131 : INFO : PROGRESS: at sentence #760000, processed 74335505 words, keeping 643632 word types
2021-09-30 11:14:15,462 : INFO : PROGRESS: at sentence #770000, processed 75298780 words, keeping 649674 word types
2021-09-30 11:14:16,741 : INFO : PROGRESS: at sentence #780000, processed 76189579 words, keeping 653527 word types
2021-09-30 11:14:17,728 : INFO : PROGRESS: at sentence #790000, processed 76892306 words, keeping 657840 word types
2021-09-30 11:14:18,806 : INFO : PROGRESS: at sentence #800000, processed 77669230 words, keeping 661077 word types
2021-09-30 11:14:19,890 : INFO : PROGRESS: at sentence #810000, processed 78462935 words, keeping 666292 word types
2021-09-30 11:14:21,073 : INFO : PROGRESS: at sentence #820000, processed 79343863 words, keeping 670021 word types
2021-09-30 11:14:22,190 : INFO : PROGRESS: at sentence #830000, processed 80149716 words, keeping 675961 word types
2021-09-30 11:14:23,262 : INFO : PROGRESS: at sentence #840000, processed 80919098 words, keeping 682270 word types
2021-09-30 11:14:24,373 : INFO : PROGRESS: at sentence #850000, processed 81725718 words, keeping 686449 word types
2021-09-30 11:14:25,610 : INFO : PROGRESS: at sentence #860000, processed 82646589 words, keeping 690320 word types
2021-09-30 11:14:26,652 : INFO : PROGRESS: at sentence #870000, processed 83407421 words, keeping 694791 word types
2021-09-30 11:14:27,707 : INFO : PROGRESS: at sentence #880000, processed 84173268 words, keeping 698857 word types
2021-09-30 11:14:29,007 : INFO : PROGRESS: at sentence #890000, processed 85116837 words, keeping 702016 word types
2021-09-30 11:14:30,153 : INFO : PROGRESS: at sentence #900000, processed 85960765 words, keeping 704437 word types
2021-09-30 11:14:31,307 : INFO : PROGRESS: at sentence #910000, processed 86818510 words, keeping 709250 word types
2021-09-30 11:14:32,275 : INFO : PROGRESS: at sentence #920000, processed 87525406 words, keeping 711820 word types
2021-09-30 11:14:33,467 : INFO : PROGRESS: at sentence #930000, processed 88390961 words, keeping 716278 word types
2021-09-30 11:14:35,039 : INFO : PROGRESS: at sentence #940000, processed 89521569 words, keeping 721182 word types
2021-09-30 11:14:36,602 : INFO : PROGRESS: at sentence #950000, processed 90683265 words, keeping 726458 word types
2021-09-30 11:14:38,175 : INFO : PROGRESS: at sentence #960000, processed 91833857 words, keeping 730935 word types
2021-09-30 11:14:39,753 : INFO : PROGRESS: at sentence #970000, processed 92996895 words, keeping 735274 word types
2021-09-30 11:14:41,264 : INFO : PROGRESS: at sentence #980000, processed 94125957 words, keeping 738796 word types
2021-09-30 11:14:42,811 : INFO : PROGRESS: at sentence #990000, processed 95256200 words, keeping 742224 word types
2021-09-30 11:14:44,043 : INFO : PROGRESS: at sentence #1000000, processed 96155404 words, keeping 746900 word types
2021-09-30 11:14:44,153 : INFO : PROGRESS: at sentence #1010000, processed 96225885 words, keeping 749366 word types
2021-09-30 11:14:44,263 : INFO : PROGRESS: at sentence #1020000, processed 96296616 words, keeping 750634 word types
2021-09-30 11:14:44,302 : INFO : collected 752320 word types from a corpus of 96321721 raw words and 1023403 sentences
2021-09-30 11:14:44,302 : INFO : Loading a fresh vocabulary
2021-09-30 11:14:44,864 : INFO : effective_min_count=2 retains 331256 unique words (44% of original 752320, drops 421064)
2021-09-30 11:14:44,864 : INFO : effective_min_count=2 leaves 95900657 word corpus (99% of original 96321721, drops 421064)
2021-09-30 11:14:45,340 : INFO : deleting the raw counts dictionary of 752320 items
2021-09-30 11:14:45,350 : INFO : sample=0.001 downsamples 36 most-common words
2021-09-30 11:14:45,350 : INFO : downsampling leaves estimated 70188603 word corpus (73.2% of prior 95900657)
2021-09-30 11:14:45,858 : INFO : estimated required memory for 331256 words and 500 dimensions: 1490652000 bytes
2021-09-30 11:14:45,858 : INFO : resetting layer weights
2021-09-30 11:15:24,311 : INFO : training model with 3 workers on 331256 vocabulary and 500 features, using sg=0 hs=0 sample=0.001 negative=5 window=4
2021-09-30 11:15:25,319 : INFO : EPOCH 1 - PROGRESS: at 0.58% examples, 348169 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:15:26,327 : INFO : EPOCH 1 - PROGRESS: at 1.25% examples, 384933 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:15:27,357 : INFO : EPOCH 1 - PROGRESS: at 1.97% examples, 397416 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:15:28,394 : INFO : EPOCH 1 - PROGRESS: at 2.62% examples, 406649 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:15:29,402 : INFO : EPOCH 1 - PROGRESS: at 3.19% examples, 403383 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:15:30,405 : INFO : EPOCH 1 - PROGRESS: at 3.84% examples, 415840 words/s, in_qsize 0, out_qsize 0
2021-09-30 11:15:31,413 : INFO : EPOCH 1 - PROGRESS: at 4.39% examples, 410065 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:15:32,421 : INFO : EPOCH 1 - PROGRESS: at 4.93% examples, 412574 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:15:33,449 : INFO : EPOCH 1 - PROGRESS: at 5.69% examples, 411577 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:15:34,529 : INFO : EPOCH 1 - PROGRESS: at 6.44% examples, 413359 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:15:35,539 : INFO : EPOCH 1 - PROGRESS: at 7.01% examples, 416314 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:15:36,628 : INFO : EPOCH 1 - PROGRESS: at 7.33% examples, 414779 words/s, in_qsize 5, out_qsize 5
2021-09-30 11:15:37,651 : INFO : EPOCH 1 - PROGRESS: at 8.00% examples, 416301 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:15:38,690 : INFO : EPOCH 1 - PROGRESS: at 8.69% examples, 415063 words/s, in_qsize 6, out_qsize 4
2021-09-30 11:15:39,711 : INFO : EPOCH 1 - PROGRESS: at 9.44% examples, 416966 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:15:40,801 : INFO : EPOCH 1 - PROGRESS: at 10.09% examples, 410484 words/s, in_qsize 2, out_qsize 6
2021-09-30 11:15:41,805 : INFO : EPOCH 1 - PROGRESS: at 10.98% examples, 414195 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:15:42,806 : INFO : EPOCH 1 - PROGRESS: at 11.62% examples, 414319 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:15:43,847 : INFO : EPOCH 1 - PROGRESS: at 12.32% examples, 413353 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:15:44,862 : INFO : EPOCH 1 - PROGRESS: at 13.05% examples, 412844 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:15:45,946 : INFO : EPOCH 1 - PROGRESS: at 13.81% examples, 411022 words/s, in_qsize 6, out_qsize 3
2021-09-30 11:15:46,948 : INFO : EPOCH 1 - PROGRESS: at 14.51% examples, 411003 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:15:47,957 : INFO : EPOCH 1 - PROGRESS: at 15.03% examples, 410239 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:15:48,977 : INFO : EPOCH 1 - PROGRESS: at 15.55% examples, 408304 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:15:49,984 : INFO : EPOCH 1 - PROGRESS: at 16.12% examples, 408506 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:15:51,004 : INFO : EPOCH 1 - PROGRESS: at 16.85% examples, 410217 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:15:52,056 : INFO : EPOCH 1 - PROGRESS: at 17.53% examples, 411343 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:15:53,063 : INFO : EPOCH 1 - PROGRESS: at 18.23% examples, 411003 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:15:54,072 : INFO : EPOCH 1 - PROGRESS: at 18.99% examples, 411613 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:15:55,078 : INFO : EPOCH 1 - PROGRESS: at 19.61% examples, 409663 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:15:56,113 : INFO : EPOCH 1 - PROGRESS: at 20.36% examples, 409380 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:15:57,116 : INFO : EPOCH 1 - PROGRESS: at 21.07% examples, 410395 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:15:58,140 : INFO : EPOCH 1 - PROGRESS: at 21.64% examples, 408725 words/s, in_qsize 3, out_qsize 8
2021-09-30 11:15:59,167 : INFO : EPOCH 1 - PROGRESS: at 22.14% examples, 410919 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:16:00,179 : INFO : EPOCH 1 - PROGRESS: at 22.32% examples, 410616 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:16:01,186 : INFO : EPOCH 1 - PROGRESS: at 22.53% examples, 410288 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:16:02,195 : INFO : EPOCH 1 - PROGRESS: at 22.72% examples, 409980 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:16:03,227 : INFO : EPOCH 1 - PROGRESS: at 22.91% examples, 409317 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:16:04,232 : INFO : EPOCH 1 - PROGRESS: at 23.10% examples, 408948 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:16:05,265 : INFO : EPOCH 1 - PROGRESS: at 23.31% examples, 408505 words/s, in_qsize 0, out_qsize 0
2021-09-30 11:16:06,273 : INFO : EPOCH 1 - PROGRESS: at 23.50% examples, 407953 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:16:07,274 : INFO : EPOCH 1 - PROGRESS: at 23.69% examples, 407357 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:16:08,327 : INFO : EPOCH 1 - PROGRESS: at 23.87% examples, 405984 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:16:09,367 : INFO : EPOCH 1 - PROGRESS: at 24.05% examples, 404521 words/s, in_qsize 1, out_qsize 3
2021-09-30 11:16:10,382 : INFO : EPOCH 1 - PROGRESS: at 24.25% examples, 403487 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:16:11,383 : INFO : EPOCH 1 - PROGRESS: at 24.43% examples, 402734 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:16:12,438 : INFO : EPOCH 1 - PROGRESS: at 24.88% examples, 400694 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:16:13,475 : INFO : EPOCH 1 - PROGRESS: at 25.48% examples, 401109 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:16:14,509 : INFO : EPOCH 1 - PROGRESS: at 26.17% examples, 401394 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:16:15,533 : INFO : EPOCH 1 - PROGRESS: at 26.89% examples, 402023 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:16:16,578 : INFO : EPOCH 1 - PROGRESS: at 27.64% examples, 402246 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:16:17,592 : INFO : EPOCH 1 - PROGRESS: at 28.17% examples, 402688 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:16:18,608 : INFO : EPOCH 1 - PROGRESS: at 28.42% examples, 402410 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:16:19,612 : INFO : EPOCH 1 - PROGRESS: at 28.85% examples, 402439 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:16:20,615 : INFO : EPOCH 1 - PROGRESS: at 29.23% examples, 402862 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:16:21,616 : INFO : EPOCH 1 - PROGRESS: at 29.82% examples, 403703 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:16:22,627 : INFO : EPOCH 1 - PROGRESS: at 30.36% examples, 403102 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:16:23,687 : INFO : EPOCH 1 - PROGRESS: at 30.89% examples, 401786 words/s, in_qsize 6, out_qsize 3
2021-09-30 11:16:24,734 : INFO : EPOCH 1 - PROGRESS: at 31.58% examples, 402059 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:16:25,761 : INFO : EPOCH 1 - PROGRESS: at 32.39% examples, 402554 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:16:26,866 : INFO : EPOCH 1 - PROGRESS: at 33.23% examples, 402396 words/s, in_qsize 1, out_qsize 8
2021-09-30 11:16:27,883 : INFO : EPOCH 1 - PROGRESS: at 34.13% examples, 403587 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:16:28,889 : INFO : EPOCH 1 - PROGRESS: at 34.93% examples, 403945 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:16:29,906 : INFO : EPOCH 1 - PROGRESS: at 35.78% examples, 404406 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:16:30,936 : INFO : EPOCH 1 - PROGRESS: at 36.50% examples, 404116 words/s, in_qsize 5, out_qsize 4
2021-09-30 11:16:31,973 : INFO : EPOCH 1 - PROGRESS: at 37.46% examples, 405416 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:16:32,979 : INFO : EPOCH 1 - PROGRESS: at 38.28% examples, 405687 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:16:34,013 : INFO : EPOCH 1 - PROGRESS: at 39.08% examples, 405673 words/s, in_qsize 5, out_qsize 3
2021-09-30 11:16:35,026 : INFO : EPOCH 1 - PROGRESS: at 39.68% examples, 406030 words/s, in_qsize 2, out_qsize 3
2021-09-30 11:16:36,042 : INFO : EPOCH 1 - PROGRESS: at 40.05% examples, 404462 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:16:37,052 : INFO : EPOCH 1 - PROGRESS: at 40.73% examples, 404650 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:16:38,133 : INFO : EPOCH 1 - PROGRESS: at 41.37% examples, 404776 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:16:39,139 : INFO : EPOCH 1 - PROGRESS: at 42.17% examples, 405510 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:16:40,172 : INFO : EPOCH 1 - PROGRESS: at 42.84% examples, 405203 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:16:41,172 : INFO : EPOCH 1 - PROGRESS: at 43.58% examples, 405467 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:16:42,196 : INFO : EPOCH 1 - PROGRESS: at 44.24% examples, 405504 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:16:43,203 : INFO : EPOCH 1 - PROGRESS: at 44.92% examples, 406021 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:16:44,235 : INFO : EPOCH 1 - PROGRESS: at 45.65% examples, 406401 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:16:45,254 : INFO : EPOCH 1 - PROGRESS: at 46.51% examples, 406711 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:16:46,290 : INFO : EPOCH 1 - PROGRESS: at 47.10% examples, 406587 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:16:47,299 : INFO : EPOCH 1 - PROGRESS: at 47.77% examples, 407231 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:16:48,308 : INFO : EPOCH 1 - PROGRESS: at 48.38% examples, 407548 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:16:49,310 : INFO : EPOCH 1 - PROGRESS: at 49.10% examples, 407980 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:16:50,311 : INFO : EPOCH 1 - PROGRESS: at 49.64% examples, 407424 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:16:51,356 : INFO : EPOCH 1 - PROGRESS: at 50.38% examples, 407502 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:16:52,370 : INFO : EPOCH 1 - PROGRESS: at 51.09% examples, 407422 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:16:53,422 : INFO : EPOCH 1 - PROGRESS: at 51.18% examples, 406832 words/s, in_qsize 6, out_qsize 7
2021-09-30 11:16:54,440 : INFO : EPOCH 1 - PROGRESS: at 51.46% examples, 406902 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:16:55,470 : INFO : EPOCH 1 - PROGRESS: at 51.74% examples, 406580 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:16:56,534 : INFO : EPOCH 1 - PROGRESS: at 52.20% examples, 405943 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:16:57,577 : INFO : EPOCH 1 - PROGRESS: at 52.60% examples, 405222 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:16:58,596 : INFO : EPOCH 1 - PROGRESS: at 52.87% examples, 404398 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:16:59,623 : INFO : EPOCH 1 - PROGRESS: at 53.12% examples, 403649 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:17:00,629 : INFO : EPOCH 1 - PROGRESS: at 53.43% examples, 403474 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:17:01,646 : INFO : EPOCH 1 - PROGRESS: at 53.75% examples, 403031 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:17:02,666 : INFO : EPOCH 1 - PROGRESS: at 54.15% examples, 403107 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:17:03,683 : INFO : EPOCH 1 - PROGRESS: at 54.45% examples, 402321 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:17:04,723 : INFO : EPOCH 1 - PROGRESS: at 54.73% examples, 401451 words/s, in_qsize 4, out_qsize 4
2021-09-30 11:17:05,730 : INFO : EPOCH 1 - PROGRESS: at 55.05% examples, 401078 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:17:06,731 : INFO : EPOCH 1 - PROGRESS: at 55.35% examples, 400185 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:17:07,793 : INFO : EPOCH 1 - PROGRESS: at 55.77% examples, 399785 words/s, in_qsize 1, out_qsize 6
2021-09-30 11:17:08,853 : INFO : EPOCH 1 - PROGRESS: at 56.24% examples, 400202 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:17:09,864 : INFO : EPOCH 1 - PROGRESS: at 56.54% examples, 399707 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:17:10,887 : INFO : EPOCH 1 - PROGRESS: at 56.88% examples, 399847 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:17:11,896 : INFO : EPOCH 1 - PROGRESS: at 57.17% examples, 399439 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:17:12,901 : INFO : EPOCH 1 - PROGRESS: at 57.77% examples, 399997 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:17:13,914 : INFO : EPOCH 1 - PROGRESS: at 58.16% examples, 400133 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:17:14,930 : INFO : EPOCH 1 - PROGRESS: at 58.61% examples, 400857 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:17:15,957 : INFO : EPOCH 1 - PROGRESS: at 59.29% examples, 400958 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:17:16,957 : INFO : EPOCH 1 - PROGRESS: at 60.00% examples, 401198 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:17:18,005 : INFO : EPOCH 1 - PROGRESS: at 60.70% examples, 401414 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:17:19,017 : INFO : EPOCH 1 - PROGRESS: at 61.39% examples, 401811 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:17:20,047 : INFO : EPOCH 1 - PROGRESS: at 62.13% examples, 402159 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:17:21,069 : INFO : EPOCH 1 - PROGRESS: at 62.85% examples, 402243 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:17:22,100 : INFO : EPOCH 1 - PROGRESS: at 63.62% examples, 402444 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:17:23,115 : INFO : EPOCH 1 - PROGRESS: at 64.34% examples, 402670 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:17:24,124 : INFO : EPOCH 1 - PROGRESS: at 65.07% examples, 402928 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:17:25,138 : INFO : EPOCH 1 - PROGRESS: at 65.67% examples, 403074 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:17:26,141 : INFO : EPOCH 1 - PROGRESS: at 66.27% examples, 403140 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:17:27,145 : INFO : EPOCH 1 - PROGRESS: at 66.64% examples, 402986 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:17:28,179 : INFO : EPOCH 1 - PROGRESS: at 67.03% examples, 403290 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:17:29,190 : INFO : EPOCH 1 - PROGRESS: at 67.60% examples, 403207 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:17:30,202 : INFO : EPOCH 1 - PROGRESS: at 68.33% examples, 403333 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:17:31,205 : INFO : EPOCH 1 - PROGRESS: at 69.04% examples, 403405 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:17:32,224 : INFO : EPOCH 1 - PROGRESS: at 69.89% examples, 403849 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:17:33,249 : INFO : EPOCH 1 - PROGRESS: at 70.70% examples, 403922 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:17:34,254 : INFO : EPOCH 1 - PROGRESS: at 71.65% examples, 404323 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:17:35,259 : INFO : EPOCH 1 - PROGRESS: at 72.34% examples, 403987 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:17:36,278 : INFO : EPOCH 1 - PROGRESS: at 73.12% examples, 404226 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:17:37,296 : INFO : EPOCH 1 - PROGRESS: at 73.72% examples, 404072 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:17:38,297 : INFO : EPOCH 1 - PROGRESS: at 74.30% examples, 403935 words/s, in_qsize 1, out_qsize 7
2021-09-30 11:17:39,330 : INFO : EPOCH 1 - PROGRESS: at 74.98% examples, 404401 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:17:40,381 : INFO : EPOCH 1 - PROGRESS: at 75.60% examples, 404863 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:17:41,381 : INFO : EPOCH 1 - PROGRESS: at 76.40% examples, 405228 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:17:42,388 : INFO : EPOCH 1 - PROGRESS: at 77.14% examples, 405044 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:17:43,415 : INFO : EPOCH 1 - PROGRESS: at 77.91% examples, 405257 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:17:44,477 : INFO : EPOCH 1 - PROGRESS: at 78.67% examples, 405289 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:17:45,482 : INFO : EPOCH 1 - PROGRESS: at 79.29% examples, 405250 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:17:46,495 : INFO : EPOCH 1 - PROGRESS: at 79.92% examples, 405184 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:17:47,510 : INFO : EPOCH 1 - PROGRESS: at 80.50% examples, 404970 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:17:48,535 : INFO : EPOCH 1 - PROGRESS: at 81.28% examples, 405242 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:17:49,540 : INFO : EPOCH 1 - PROGRESS: at 82.00% examples, 405342 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:17:50,570 : INFO : EPOCH 1 - PROGRESS: at 82.75% examples, 405186 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:17:51,603 : INFO : EPOCH 1 - PROGRESS: at 83.32% examples, 405671 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:17:52,619 : INFO : EPOCH 1 - PROGRESS: at 84.06% examples, 405853 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:17:53,632 : INFO : EPOCH 1 - PROGRESS: at 84.83% examples, 406017 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:17:54,648 : INFO : EPOCH 1 - PROGRESS: at 85.66% examples, 406130 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:17:55,686 : INFO : EPOCH 1 - PROGRESS: at 86.33% examples, 406521 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:17:56,687 : INFO : EPOCH 1 - PROGRESS: at 86.81% examples, 406331 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:17:57,697 : INFO : EPOCH 1 - PROGRESS: at 87.55% examples, 406334 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:17:58,716 : INFO : EPOCH 1 - PROGRESS: at 88.26% examples, 406537 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:17:59,723 : INFO : EPOCH 1 - PROGRESS: at 88.84% examples, 406507 words/s, in_qsize 2, out_qsize 6
2021-09-30 11:18:00,743 : INFO : EPOCH 1 - PROGRESS: at 89.76% examples, 406908 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:18:01,756 : INFO : EPOCH 1 - PROGRESS: at 90.59% examples, 407262 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:18:02,759 : INFO : EPOCH 1 - PROGRESS: at 91.04% examples, 407124 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:18:03,768 : INFO : EPOCH 1 - PROGRESS: at 91.59% examples, 407426 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:18:04,785 : INFO : EPOCH 1 - PROGRESS: at 92.07% examples, 407518 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:18:05,788 : INFO : EPOCH 1 - PROGRESS: at 92.58% examples, 407698 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:18:06,903 : INFO : EPOCH 1 - PROGRESS: at 93.13% examples, 407811 words/s, in_qsize 0, out_qsize 7
2021-09-30 11:18:07,931 : INFO : EPOCH 1 - PROGRESS: at 93.61% examples, 407829 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:18:08,934 : INFO : EPOCH 1 - PROGRESS: at 94.05% examples, 407724 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:18:09,960 : INFO : EPOCH 1 - PROGRESS: at 94.53% examples, 407652 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:18:10,984 : INFO : EPOCH 1 - PROGRESS: at 95.06% examples, 407844 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:18:12,045 : INFO : EPOCH 1 - PROGRESS: at 95.61% examples, 408159 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:18:13,060 : INFO : EPOCH 1 - PROGRESS: at 96.14% examples, 408231 words/s, in_qsize 2, out_qsize 3
2021-09-30 11:18:14,060 : INFO : EPOCH 1 - PROGRESS: at 96.70% examples, 408594 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:18:15,113 : INFO : EPOCH 1 - PROGRESS: at 97.27% examples, 408715 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:18:15,909 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-30 11:18:15,920 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-30 11:18:15,926 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-30 11:18:15,926 : INFO : EPOCH - 1 : training on 96321721 raw words (70188982 effective words) took 171.6s, 408993 effective words/s
2021-09-30 11:18:16,931 : INFO : EPOCH 2 - PROGRESS: at 0.60% examples, 364029 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:18:17,937 : INFO : EPOCH 2 - PROGRESS: at 1.25% examples, 385764 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:18:18,938 : INFO : EPOCH 2 - PROGRESS: at 1.98% examples, 404557 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:18:19,957 : INFO : EPOCH 2 - PROGRESS: at 2.53% examples, 397661 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:18:21,046 : INFO : EPOCH 2 - PROGRESS: at 3.18% examples, 399887 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:18:22,048 : INFO : EPOCH 2 - PROGRESS: at 3.69% examples, 396293 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:18:23,079 : INFO : EPOCH 2 - PROGRESS: at 4.34% examples, 401190 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:18:24,093 : INFO : EPOCH 2 - PROGRESS: at 4.83% examples, 399995 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:18:25,099 : INFO : EPOCH 2 - PROGRESS: at 5.47% examples, 398670 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:18:26,101 : INFO : EPOCH 2 - PROGRESS: at 6.10% examples, 395108 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:18:27,105 : INFO : EPOCH 2 - PROGRESS: at 6.74% examples, 394244 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:18:28,129 : INFO : EPOCH 2 - PROGRESS: at 7.13% examples, 396617 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:18:29,142 : INFO : EPOCH 2 - PROGRESS: at 7.58% examples, 401035 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:18:30,157 : INFO : EPOCH 2 - PROGRESS: at 8.33% examples, 404546 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:18:31,173 : INFO : EPOCH 2 - PROGRESS: at 9.03% examples, 404257 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:18:32,200 : INFO : EPOCH 2 - PROGRESS: at 9.74% examples, 403541 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:18:33,232 : INFO : EPOCH 2 - PROGRESS: at 10.51% examples, 404034 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:18:34,328 : INFO : EPOCH 2 - PROGRESS: at 11.26% examples, 404309 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:18:35,356 : INFO : EPOCH 2 - PROGRESS: at 12.02% examples, 406595 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:18:36,371 : INFO : EPOCH 2 - PROGRESS: at 12.76% examples, 406427 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:18:37,378 : INFO : EPOCH 2 - PROGRESS: at 13.56% examples, 407732 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:18:38,456 : INFO : EPOCH 2 - PROGRESS: at 14.22% examples, 403697 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:18:39,465 : INFO : EPOCH 2 - PROGRESS: at 14.68% examples, 400182 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:18:40,496 : INFO : EPOCH 2 - PROGRESS: at 15.19% examples, 399481 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:18:41,507 : INFO : EPOCH 2 - PROGRESS: at 15.75% examples, 399949 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:18:42,519 : INFO : EPOCH 2 - PROGRESS: at 16.35% examples, 400045 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:18:43,527 : INFO : EPOCH 2 - PROGRESS: at 16.99% examples, 400270 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:18:44,533 : INFO : EPOCH 2 - PROGRESS: at 17.66% examples, 401503 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:18:45,560 : INFO : EPOCH 2 - PROGRESS: at 18.39% examples, 401727 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:18:46,569 : INFO : EPOCH 2 - PROGRESS: at 19.22% examples, 403827 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:18:47,581 : INFO : EPOCH 2 - PROGRESS: at 19.99% examples, 404781 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:18:48,590 : INFO : EPOCH 2 - PROGRESS: at 20.74% examples, 405524 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:18:49,696 : INFO : EPOCH 2 - PROGRESS: at 21.44% examples, 405176 words/s, in_qsize 2, out_qsize 7
2021-09-30 11:18:50,711 : INFO : EPOCH 2 - PROGRESS: at 22.05% examples, 406135 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:18:51,718 : INFO : EPOCH 2 - PROGRESS: at 22.24% examples, 406458 words/s, in_qsize 1, out_qsize 3
2021-09-30 11:18:52,725 : INFO : EPOCH 2 - PROGRESS: at 22.44% examples, 406372 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:18:53,727 : INFO : EPOCH 2 - PROGRESS: at 22.62% examples, 405681 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:18:54,730 : INFO : EPOCH 2 - PROGRESS: at 22.83% examples, 406300 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:18:55,751 : INFO : EPOCH 2 - PROGRESS: at 23.01% examples, 405185 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:18:56,751 : INFO : EPOCH 2 - PROGRESS: at 23.20% examples, 405107 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:18:57,760 : INFO : EPOCH 2 - PROGRESS: at 23.41% examples, 404975 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:18:58,761 : INFO : EPOCH 2 - PROGRESS: at 23.62% examples, 405544 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:18:59,787 : INFO : EPOCH 2 - PROGRESS: at 23.82% examples, 404973 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:19:00,849 : INFO : EPOCH 2 - PROGRESS: at 24.03% examples, 404822 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:19:01,874 : INFO : EPOCH 2 - PROGRESS: at 24.25% examples, 404429 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:19:02,906 : INFO : EPOCH 2 - PROGRESS: at 24.45% examples, 403841 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:19:03,906 : INFO : EPOCH 2 - PROGRESS: at 24.98% examples, 403892 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:19:04,925 : INFO : EPOCH 2 - PROGRESS: at 25.64% examples, 404416 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:19:05,934 : INFO : EPOCH 2 - PROGRESS: at 26.37% examples, 405689 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:19:06,993 : INFO : EPOCH 2 - PROGRESS: at 27.14% examples, 405933 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:19:08,003 : INFO : EPOCH 2 - PROGRESS: at 27.88% examples, 406513 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:19:09,006 : INFO : EPOCH 2 - PROGRESS: at 28.25% examples, 406619 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:19:10,024 : INFO : EPOCH 2 - PROGRESS: at 28.59% examples, 407163 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:19:11,029 : INFO : EPOCH 2 - PROGRESS: at 29.04% examples, 408144 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:19:12,039 : INFO : EPOCH 2 - PROGRESS: at 29.48% examples, 407894 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:19:13,088 : INFO : EPOCH 2 - PROGRESS: at 30.05% examples, 407667 words/s, in_qsize 6, out_qsize 3
2021-09-30 11:19:14,114 : INFO : EPOCH 2 - PROGRESS: at 30.81% examples, 409011 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:19:15,153 : INFO : EPOCH 2 - PROGRESS: at 31.52% examples, 409713 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:19:16,193 : INFO : EPOCH 2 - PROGRESS: at 32.32% examples, 409877 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:19:17,219 : INFO : EPOCH 2 - PROGRESS: at 33.05% examples, 409164 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:19:18,244 : INFO : EPOCH 2 - PROGRESS: at 33.79% examples, 408836 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:19:19,271 : INFO : EPOCH 2 - PROGRESS: at 34.58% examples, 408973 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:19:20,278 : INFO : EPOCH 2 - PROGRESS: at 35.31% examples, 408531 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:19:21,319 : INFO : EPOCH 2 - PROGRESS: at 36.15% examples, 408764 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:19:22,343 : INFO : EPOCH 2 - PROGRESS: at 36.88% examples, 408446 words/s, in_qsize 3, out_qsize 3
2021-09-30 11:19:23,346 : INFO : EPOCH 2 - PROGRESS: at 37.66% examples, 408500 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:19:24,369 : INFO : EPOCH 2 - PROGRESS: at 38.54% examples, 409051 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:19:25,427 : INFO : EPOCH 2 - PROGRESS: at 39.33% examples, 409436 words/s, in_qsize 1, out_qsize 4
2021-09-30 11:19:26,450 : INFO : EPOCH 2 - PROGRESS: at 39.88% examples, 409594 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:19:27,479 : INFO : EPOCH 2 - PROGRESS: at 40.57% examples, 410371 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:19:28,493 : INFO : EPOCH 2 - PROGRESS: at 41.25% examples, 410491 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:19:29,532 : INFO : EPOCH 2 - PROGRESS: at 42.07% examples, 411289 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:19:30,534 : INFO : EPOCH 2 - PROGRESS: at 42.75% examples, 411539 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:19:31,562 : INFO : EPOCH 2 - PROGRESS: at 43.61% examples, 412247 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:19:32,614 : INFO : EPOCH 2 - PROGRESS: at 44.25% examples, 411949 words/s, in_qsize 4, out_qsize 4
2021-09-30 11:19:33,615 : INFO : EPOCH 2 - PROGRESS: at 44.94% examples, 412623 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:19:34,684 : INFO : EPOCH 2 - PROGRESS: at 45.73% examples, 412996 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:19:35,738 : INFO : EPOCH 2 - PROGRESS: at 46.62% examples, 413150 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:19:36,767 : INFO : EPOCH 2 - PROGRESS: at 47.17% examples, 412959 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:19:37,792 : INFO : EPOCH 2 - PROGRESS: at 47.71% examples, 412292 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:19:38,800 : INFO : EPOCH 2 - PROGRESS: at 48.30% examples, 412472 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:19:39,807 : INFO : EPOCH 2 - PROGRESS: at 48.96% examples, 412176 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:19:40,832 : INFO : EPOCH 2 - PROGRESS: at 49.51% examples, 411847 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:19:41,836 : INFO : EPOCH 2 - PROGRESS: at 50.26% examples, 412141 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:19:42,851 : INFO : EPOCH 2 - PROGRESS: at 51.06% examples, 412198 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:19:43,882 : INFO : EPOCH 2 - PROGRESS: at 51.18% examples, 412114 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:19:44,884 : INFO : EPOCH 2 - PROGRESS: at 51.37% examples, 411870 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:19:45,891 : INFO : EPOCH 2 - PROGRESS: at 51.69% examples, 411604 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:19:46,900 : INFO : EPOCH 2 - PROGRESS: at 52.18% examples, 411466 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:19:47,945 : INFO : EPOCH 2 - PROGRESS: at 52.63% examples, 410969 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:19:48,987 : INFO : EPOCH 2 - PROGRESS: at 52.94% examples, 410686 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:19:50,030 : INFO : EPOCH 2 - PROGRESS: at 53.24% examples, 410690 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:19:51,037 : INFO : EPOCH 2 - PROGRESS: at 53.59% examples, 410434 words/s, in_qsize 3, out_qsize 3
2021-09-30 11:19:52,146 : INFO : EPOCH 2 - PROGRESS: at 54.01% examples, 410357 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:19:53,173 : INFO : EPOCH 2 - PROGRESS: at 54.39% examples, 410328 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:19:54,185 : INFO : EPOCH 2 - PROGRESS: at 54.72% examples, 410203 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:19:55,206 : INFO : EPOCH 2 - PROGRESS: at 55.10% examples, 410260 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:19:56,248 : INFO : EPOCH 2 - PROGRESS: at 55.51% examples, 410025 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:19:57,284 : INFO : EPOCH 2 - PROGRESS: at 55.97% examples, 410030 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:19:58,288 : INFO : EPOCH 2 - PROGRESS: at 56.37% examples, 410219 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:19:59,298 : INFO : EPOCH 2 - PROGRESS: at 56.69% examples, 409964 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:20:00,344 : INFO : EPOCH 2 - PROGRESS: at 57.00% examples, 409580 words/s, in_qsize 3, out_qsize 3
2021-09-30 11:20:01,346 : INFO : EPOCH 2 - PROGRESS: at 57.42% examples, 409792 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:20:02,347 : INFO : EPOCH 2 - PROGRESS: at 57.88% examples, 409526 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:20:03,348 : INFO : EPOCH 2 - PROGRESS: at 58.29% examples, 409501 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:20:04,404 : INFO : EPOCH 2 - PROGRESS: at 58.76% examples, 409672 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:20:05,417 : INFO : EPOCH 2 - PROGRESS: at 59.40% examples, 409468 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:20:06,455 : INFO : EPOCH 2 - PROGRESS: at 60.13% examples, 409630 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:20:07,455 : INFO : EPOCH 2 - PROGRESS: at 60.79% examples, 409750 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:20:08,528 : INFO : EPOCH 2 - PROGRESS: at 61.41% examples, 409402 words/s, in_qsize 3, out_qsize 5
2021-09-30 11:20:09,573 : INFO : EPOCH 2 - PROGRESS: at 62.05% examples, 409182 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:20:10,593 : INFO : EPOCH 2 - PROGRESS: at 62.78% examples, 409212 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:20:11,640 : INFO : EPOCH 2 - PROGRESS: at 63.46% examples, 408796 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:20:12,665 : INFO : EPOCH 2 - PROGRESS: at 64.17% examples, 408997 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:20:13,697 : INFO : EPOCH 2 - PROGRESS: at 64.85% examples, 408875 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:20:14,720 : INFO : EPOCH 2 - PROGRESS: at 65.47% examples, 408774 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:20:15,751 : INFO : EPOCH 2 - PROGRESS: at 66.04% examples, 408578 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:20:16,814 : INFO : EPOCH 2 - PROGRESS: at 66.49% examples, 408100 words/s, in_qsize 4, out_qsize 4
2021-09-30 11:20:17,819 : INFO : EPOCH 2 - PROGRESS: at 66.88% examples, 408406 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:20:18,838 : INFO : EPOCH 2 - PROGRESS: at 67.28% examples, 408367 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:20:19,880 : INFO : EPOCH 2 - PROGRESS: at 68.00% examples, 408150 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:20:20,880 : INFO : EPOCH 2 - PROGRESS: at 68.75% examples, 408395 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:20:21,918 : INFO : EPOCH 2 - PROGRESS: at 69.41% examples, 408002 words/s, in_qsize 1, out_qsize 6
2021-09-30 11:20:22,933 : INFO : EPOCH 2 - PROGRESS: at 70.17% examples, 408012 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:20:23,957 : INFO : EPOCH 2 - PROGRESS: at 71.09% examples, 408274 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:20:24,989 : INFO : EPOCH 2 - PROGRESS: at 71.86% examples, 407888 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:20:26,106 : INFO : EPOCH 2 - PROGRESS: at 72.65% examples, 407562 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:20:27,115 : INFO : EPOCH 2 - PROGRESS: at 73.27% examples, 407352 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:20:28,178 : INFO : EPOCH 2 - PROGRESS: at 73.94% examples, 407528 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:20:29,180 : INFO : EPOCH 2 - PROGRESS: at 74.60% examples, 407585 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:20:30,186 : INFO : EPOCH 2 - PROGRESS: at 75.08% examples, 407183 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:20:31,195 : INFO : EPOCH 2 - PROGRESS: at 75.67% examples, 407650 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:20:32,232 : INFO : EPOCH 2 - PROGRESS: at 76.46% examples, 407734 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:20:33,307 : INFO : EPOCH 2 - PROGRESS: at 77.31% examples, 407804 words/s, in_qsize 0, out_qsize 5
2021-09-30 11:20:34,320 : INFO : EPOCH 2 - PROGRESS: at 78.09% examples, 408092 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:20:35,326 : INFO : EPOCH 2 - PROGRESS: at 78.87% examples, 408426 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:20:36,344 : INFO : EPOCH 2 - PROGRESS: at 79.54% examples, 408588 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:20:37,346 : INFO : EPOCH 2 - PROGRESS: at 80.24% examples, 408814 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:20:38,367 : INFO : EPOCH 2 - PROGRESS: at 80.92% examples, 408901 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:20:39,389 : INFO : EPOCH 2 - PROGRESS: at 81.66% examples, 408997 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:20:40,391 : INFO : EPOCH 2 - PROGRESS: at 82.41% examples, 408823 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:20:41,424 : INFO : EPOCH 2 - PROGRESS: at 83.07% examples, 409026 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:20:42,462 : INFO : EPOCH 2 - PROGRESS: at 83.59% examples, 409023 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:20:43,480 : INFO : EPOCH 2 - PROGRESS: at 84.32% examples, 408946 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:20:44,553 : INFO : EPOCH 2 - PROGRESS: at 85.02% examples, 408665 words/s, in_qsize 3, out_qsize 5
2021-09-30 11:20:45,572 : INFO : EPOCH 2 - PROGRESS: at 85.89% examples, 409143 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:20:46,584 : INFO : EPOCH 2 - PROGRESS: at 86.44% examples, 409054 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:20:47,588 : INFO : EPOCH 2 - PROGRESS: at 87.09% examples, 409117 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:20:48,616 : INFO : EPOCH 2 - PROGRESS: at 87.82% examples, 409370 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:20:49,631 : INFO : EPOCH 2 - PROGRESS: at 88.57% examples, 409588 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:20:50,645 : INFO : EPOCH 2 - PROGRESS: at 89.25% examples, 409813 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:20:51,664 : INFO : EPOCH 2 - PROGRESS: at 90.18% examples, 410186 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:20:52,729 : INFO : EPOCH 2 - PROGRESS: at 90.80% examples, 410152 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:20:53,783 : INFO : EPOCH 2 - PROGRESS: at 91.35% examples, 410280 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:20:54,799 : INFO : EPOCH 2 - PROGRESS: at 91.81% examples, 410222 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:20:55,870 : INFO : EPOCH 2 - PROGRESS: at 92.25% examples, 409884 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:20:56,873 : INFO : EPOCH 2 - PROGRESS: at 92.79% examples, 410179 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:20:57,907 : INFO : EPOCH 2 - PROGRESS: at 93.34% examples, 410443 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:20:58,908 : INFO : EPOCH 2 - PROGRESS: at 93.87% examples, 410811 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:20:59,911 : INFO : EPOCH 2 - PROGRESS: at 94.38% examples, 411011 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:21:00,913 : INFO : EPOCH 2 - PROGRESS: at 94.90% examples, 411228 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:21:01,914 : INFO : EPOCH 2 - PROGRESS: at 95.38% examples, 411239 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:21:02,914 : INFO : EPOCH 2 - PROGRESS: at 95.92% examples, 411509 words/s, in_qsize 0, out_qsize 3
2021-09-30 11:21:03,920 : INFO : EPOCH 2 - PROGRESS: at 96.42% examples, 411494 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:21:04,932 : INFO : EPOCH 2 - PROGRESS: at 96.90% examples, 411480 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:21:05,942 : INFO : EPOCH 2 - PROGRESS: at 97.59% examples, 411601 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:21:06,411 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-30 11:21:06,416 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-30 11:21:06,416 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-30 11:21:06,416 : INFO : EPOCH - 2 : training on 96321721 raw words (70190974 effective words) took 170.5s, 411702 effective words/s
2021-09-30 11:21:07,449 : INFO : EPOCH 3 - PROGRESS: at 0.63% examples, 368063 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:21:08,452 : INFO : EPOCH 3 - PROGRESS: at 1.31% examples, 402355 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:21:09,457 : INFO : EPOCH 3 - PROGRESS: at 2.04% examples, 417403 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:21:10,476 : INFO : EPOCH 3 - PROGRESS: at 2.62% examples, 408822 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:21:11,476 : INFO : EPOCH 3 - PROGRESS: at 3.26% examples, 415943 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:21:12,531 : INFO : EPOCH 3 - PROGRESS: at 3.84% examples, 414432 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:21:13,534 : INFO : EPOCH 3 - PROGRESS: at 4.49% examples, 420394 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:21:14,540 : INFO : EPOCH 3 - PROGRESS: at 5.02% examples, 419012 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:21:15,549 : INFO : EPOCH 3 - PROGRESS: at 5.77% examples, 418356 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:21:16,571 : INFO : EPOCH 3 - PROGRESS: at 6.60% examples, 425244 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:21:17,576 : INFO : EPOCH 3 - PROGRESS: at 7.08% examples, 426873 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:21:18,621 : INFO : EPOCH 3 - PROGRESS: at 7.50% examples, 430077 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:21:19,639 : INFO : EPOCH 3 - PROGRESS: at 8.23% examples, 430330 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:21:20,643 : INFO : EPOCH 3 - PROGRESS: at 8.99% examples, 431572 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:21:21,663 : INFO : EPOCH 3 - PROGRESS: at 9.65% examples, 428204 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:21:22,673 : INFO : EPOCH 3 - PROGRESS: at 10.45% examples, 428253 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:21:23,722 : INFO : EPOCH 3 - PROGRESS: at 11.16% examples, 426065 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:21:24,736 : INFO : EPOCH 3 - PROGRESS: at 11.84% examples, 425664 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:21:25,772 : INFO : EPOCH 3 - PROGRESS: at 12.62% examples, 425031 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:21:26,807 : INFO : EPOCH 3 - PROGRESS: at 13.41% examples, 424953 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:21:27,911 : INFO : EPOCH 3 - PROGRESS: at 14.20% examples, 422716 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:21:28,937 : INFO : EPOCH 3 - PROGRESS: at 14.81% examples, 422989 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:21:29,978 : INFO : EPOCH 3 - PROGRESS: at 15.39% examples, 422814 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:21:31,007 : INFO : EPOCH 3 - PROGRESS: at 16.04% examples, 423784 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:21:32,020 : INFO : EPOCH 3 - PROGRESS: at 16.74% examples, 424654 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:21:33,056 : INFO : EPOCH 3 - PROGRESS: at 17.39% examples, 424581 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:21:34,085 : INFO : EPOCH 3 - PROGRESS: at 18.07% examples, 423911 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:21:35,099 : INFO : EPOCH 3 - PROGRESS: at 18.88% examples, 424801 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:21:36,106 : INFO : EPOCH 3 - PROGRESS: at 19.63% examples, 424768 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:21:37,111 : INFO : EPOCH 3 - PROGRESS: at 20.31% examples, 423176 words/s, in_qsize 5, out_qsize 4
2021-09-30 11:21:38,141 : INFO : EPOCH 3 - PROGRESS: at 21.09% examples, 424798 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:21:39,148 : INFO : EPOCH 3 - PROGRESS: at 21.82% examples, 425485 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:21:40,152 : INFO : EPOCH 3 - PROGRESS: at 22.14% examples, 424940 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:21:41,154 : INFO : EPOCH 3 - PROGRESS: at 22.35% examples, 425337 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:21:42,186 : INFO : EPOCH 3 - PROGRESS: at 22.54% examples, 423902 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:21:43,203 : INFO : EPOCH 3 - PROGRESS: at 22.74% examples, 423312 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:21:44,223 : INFO : EPOCH 3 - PROGRESS: at 22.94% examples, 423110 words/s, in_qsize 1, out_qsize 5
2021-09-30 11:21:45,256 : INFO : EPOCH 3 - PROGRESS: at 23.15% examples, 422948 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:21:46,283 : INFO : EPOCH 3 - PROGRESS: at 23.36% examples, 422500 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:21:47,305 : INFO : EPOCH 3 - PROGRESS: at 23.57% examples, 421960 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:21:48,306 : INFO : EPOCH 3 - PROGRESS: at 23.77% examples, 421511 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:21:49,334 : INFO : EPOCH 3 - PROGRESS: at 23.97% examples, 420649 words/s, in_qsize 3, out_qsize 5
2021-09-30 11:21:50,356 : INFO : EPOCH 3 - PROGRESS: at 24.22% examples, 421454 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:21:51,374 : INFO : EPOCH 3 - PROGRESS: at 24.41% examples, 420727 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:21:52,388 : INFO : EPOCH 3 - PROGRESS: at 24.98% examples, 421326 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:21:53,389 : INFO : EPOCH 3 - PROGRESS: at 25.63% examples, 421645 words/s, in_qsize 1, out_qsize 3
2021-09-30 11:21:54,391 : INFO : EPOCH 3 - PROGRESS: at 26.30% examples, 421769 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:21:55,431 : INFO : EPOCH 3 - PROGRESS: at 27.07% examples, 422137 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:21:56,465 : INFO : EPOCH 3 - PROGRESS: at 27.88% examples, 422934 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:21:57,515 : INFO : EPOCH 3 - PROGRESS: at 28.24% examples, 422064 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:21:58,556 : INFO : EPOCH 3 - PROGRESS: at 28.60% examples, 422554 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:21:59,586 : INFO : EPOCH 3 - PROGRESS: at 29.00% examples, 422156 words/s, in_qsize 5, out_qsize 3
2021-09-30 11:22:00,589 : INFO : EPOCH 3 - PROGRESS: at 29.55% examples, 423411 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:22:01,601 : INFO : EPOCH 3 - PROGRESS: at 30.16% examples, 423562 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:22:02,663 : INFO : EPOCH 3 - PROGRESS: at 30.84% examples, 423474 words/s, in_qsize 4, out_qsize 4
2021-09-30 11:22:03,683 : INFO : EPOCH 3 - PROGRESS: at 31.56% examples, 424079 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:22:04,727 : INFO : EPOCH 3 - PROGRESS: at 32.33% examples, 423726 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:22:05,755 : INFO : EPOCH 3 - PROGRESS: at 33.20% examples, 423952 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:22:06,777 : INFO : EPOCH 3 - PROGRESS: at 34.02% examples, 424110 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:22:07,802 : INFO : EPOCH 3 - PROGRESS: at 34.81% examples, 423882 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:22:08,806 : INFO : EPOCH 3 - PROGRESS: at 35.67% examples, 424264 words/s, in_qsize 1, out_qsize 3
2021-09-30 11:22:09,839 : INFO : EPOCH 3 - PROGRESS: at 36.53% examples, 424734 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:22:10,857 : INFO : EPOCH 3 - PROGRESS: at 37.28% examples, 424211 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:22:11,865 : INFO : EPOCH 3 - PROGRESS: at 38.19% examples, 424971 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:22:12,866 : INFO : EPOCH 3 - PROGRESS: at 38.97% examples, 424658 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:22:13,895 : INFO : EPOCH 3 - PROGRESS: at 39.58% examples, 424200 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:22:14,896 : INFO : EPOCH 3 - PROGRESS: at 40.09% examples, 424165 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:22:15,930 : INFO : EPOCH 3 - PROGRESS: at 40.85% examples, 424374 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:22:16,959 : INFO : EPOCH 3 - PROGRESS: at 41.43% examples, 424096 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:22:17,988 : INFO : EPOCH 3 - PROGRESS: at 42.20% examples, 424248 words/s, in_qsize 0, out_qsize 6
2021-09-30 11:22:18,999 : INFO : EPOCH 3 - PROGRESS: at 42.95% examples, 424202 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:22:20,020 : INFO : EPOCH 3 - PROGRESS: at 43.73% examples, 424790 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:22:21,085 : INFO : EPOCH 3 - PROGRESS: at 44.41% examples, 424244 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:22:22,131 : INFO : EPOCH 3 - PROGRESS: at 45.02% examples, 424116 words/s, in_qsize 5, out_qsize 3
2021-09-30 11:22:23,135 : INFO : EPOCH 3 - PROGRESS: at 45.76% examples, 424213 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:22:24,136 : INFO : EPOCH 3 - PROGRESS: at 46.63% examples, 424329 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:22:25,174 : INFO : EPOCH 3 - PROGRESS: at 47.24% examples, 424403 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:22:26,197 : INFO : EPOCH 3 - PROGRESS: at 47.89% examples, 424606 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:22:27,229 : INFO : EPOCH 3 - PROGRESS: at 48.58% examples, 424835 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:22:28,311 : INFO : EPOCH 3 - PROGRESS: at 49.21% examples, 424558 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:22:29,350 : INFO : EPOCH 3 - PROGRESS: at 49.91% examples, 424492 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:22:30,414 : INFO : EPOCH 3 - PROGRESS: at 50.74% examples, 424473 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:22:31,480 : INFO : EPOCH 3 - PROGRESS: at 51.17% examples, 424768 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:22:32,483 : INFO : EPOCH 3 - PROGRESS: at 51.21% examples, 424737 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:22:33,504 : INFO : EPOCH 3 - PROGRESS: at 51.69% examples, 424427 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:22:34,574 : INFO : EPOCH 3 - PROGRESS: at 52.13% examples, 424235 words/s, in_qsize 3, out_qsize 5
2021-09-30 11:22:35,577 : INFO : EPOCH 3 - PROGRESS: at 52.66% examples, 424581 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:22:36,597 : INFO : EPOCH 3 - PROGRESS: at 52.96% examples, 424088 words/s, in_qsize 3, out_qsize 4
2021-09-30 11:22:37,607 : INFO : EPOCH 3 - PROGRESS: at 53.28% examples, 424160 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:22:38,638 : INFO : EPOCH 3 - PROGRESS: at 53.61% examples, 423486 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:22:39,640 : INFO : EPOCH 3 - PROGRESS: at 53.98% examples, 423260 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:22:40,643 : INFO : EPOCH 3 - PROGRESS: at 54.38% examples, 423282 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:22:41,667 : INFO : EPOCH 3 - PROGRESS: at 54.73% examples, 423262 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:22:42,730 : INFO : EPOCH 3 - PROGRESS: at 55.08% examples, 422699 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:22:43,742 : INFO : EPOCH 3 - PROGRESS: at 55.56% examples, 423127 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:22:44,762 : INFO : EPOCH 3 - PROGRESS: at 56.04% examples, 423211 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:22:45,795 : INFO : EPOCH 3 - PROGRESS: at 56.42% examples, 423006 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:22:46,807 : INFO : EPOCH 3 - PROGRESS: at 56.77% examples, 423109 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:22:47,813 : INFO : EPOCH 3 - PROGRESS: at 57.10% examples, 422952 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:22:48,816 : INFO : EPOCH 3 - PROGRESS: at 57.66% examples, 423245 words/s, in_qsize 0, out_qsize 0
2021-09-30 11:22:49,834 : INFO : EPOCH 3 - PROGRESS: at 58.05% examples, 423057 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:22:50,868 : INFO : EPOCH 3 - PROGRESS: at 58.43% examples, 422558 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:22:51,880 : INFO : EPOCH 3 - PROGRESS: at 58.94% examples, 422330 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:22:52,912 : INFO : EPOCH 3 - PROGRESS: at 59.66% examples, 422468 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:22:53,923 : INFO : EPOCH 3 - PROGRESS: at 60.37% examples, 422556 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:22:54,949 : INFO : EPOCH 3 - PROGRESS: at 61.01% examples, 422384 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:22:56,068 : INFO : EPOCH 3 - PROGRESS: at 61.77% examples, 422521 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:22:57,074 : INFO : EPOCH 3 - PROGRESS: at 62.59% examples, 422924 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:22:58,142 : INFO : EPOCH 3 - PROGRESS: at 63.26% examples, 422376 words/s, in_qsize 3, out_qsize 7
2021-09-30 11:22:59,143 : INFO : EPOCH 3 - PROGRESS: at 64.00% examples, 422548 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:23:00,196 : INFO : EPOCH 3 - PROGRESS: at 64.76% examples, 422734 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:23:01,197 : INFO : EPOCH 3 - PROGRESS: at 65.37% examples, 422393 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:23:02,210 : INFO : EPOCH 3 - PROGRESS: at 65.96% examples, 422321 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:23:03,243 : INFO : EPOCH 3 - PROGRESS: at 66.47% examples, 422056 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:23:04,282 : INFO : EPOCH 3 - PROGRESS: at 66.87% examples, 422262 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:23:05,313 : INFO : EPOCH 3 - PROGRESS: at 67.24% examples, 421869 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:23:06,317 : INFO : EPOCH 3 - PROGRESS: at 67.97% examples, 421785 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:23:07,329 : INFO : EPOCH 3 - PROGRESS: at 68.66% examples, 421526 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:23:08,331 : INFO : EPOCH 3 - PROGRESS: at 69.44% examples, 421727 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:23:09,343 : INFO : EPOCH 3 - PROGRESS: at 70.14% examples, 421402 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:23:10,345 : INFO : EPOCH 3 - PROGRESS: at 71.05% examples, 421522 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:23:11,363 : INFO : EPOCH 3 - PROGRESS: at 71.88% examples, 421346 words/s, in_qsize 2, out_qsize 4
2021-09-30 11:23:12,409 : INFO : EPOCH 3 - PROGRESS: at 72.73% examples, 421477 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:23:13,411 : INFO : EPOCH 3 - PROGRESS: at 73.43% examples, 421529 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:23:14,417 : INFO : EPOCH 3 - PROGRESS: at 74.01% examples, 421378 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:23:15,431 : INFO : EPOCH 3 - PROGRESS: at 74.71% examples, 421457 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:23:16,446 : INFO : EPOCH 3 - PROGRESS: at 75.22% examples, 421285 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:23:17,485 : INFO : EPOCH 3 - PROGRESS: at 75.82% examples, 421234 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:23:18,487 : INFO : EPOCH 3 - PROGRESS: at 76.49% examples, 420885 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:23:19,487 : INFO : EPOCH 3 - PROGRESS: at 77.30% examples, 420925 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:23:20,496 : INFO : EPOCH 3 - PROGRESS: at 77.92% examples, 420478 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:23:21,519 : INFO : EPOCH 3 - PROGRESS: at 78.61% examples, 420144 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:23:22,552 : INFO : EPOCH 3 - PROGRESS: at 79.20% examples, 419744 words/s, in_qsize 6, out_qsize 4
2021-09-30 11:23:23,569 : INFO : EPOCH 3 - PROGRESS: at 79.85% examples, 419709 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:23:24,572 : INFO : EPOCH 3 - PROGRESS: at 80.44% examples, 419467 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:23:25,610 : INFO : EPOCH 3 - PROGRESS: at 81.15% examples, 419291 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:23:26,632 : INFO : EPOCH 3 - PROGRESS: at 81.82% examples, 419103 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:23:27,634 : INFO : EPOCH 3 - PROGRESS: at 82.59% examples, 418916 words/s, in_qsize 2, out_qsize 3
2021-09-30 11:23:28,648 : INFO : EPOCH 3 - PROGRESS: at 83.19% examples, 419206 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:23:29,693 : INFO : EPOCH 3 - PROGRESS: at 83.75% examples, 418854 words/s, in_qsize 2, out_qsize 7
2021-09-30 11:23:30,701 : INFO : EPOCH 3 - PROGRESS: at 84.56% examples, 418974 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:23:31,716 : INFO : EPOCH 3 - PROGRESS: at 85.23% examples, 418688 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:23:32,722 : INFO : EPOCH 3 - PROGRESS: at 85.96% examples, 418743 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:23:33,738 : INFO : EPOCH 3 - PROGRESS: at 86.50% examples, 418630 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:23:34,755 : INFO : EPOCH 3 - PROGRESS: at 87.23% examples, 418835 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:23:35,810 : INFO : EPOCH 3 - PROGRESS: at 87.88% examples, 418609 words/s, in_qsize 4, out_qsize 5
2021-09-30 11:23:36,822 : INFO : EPOCH 3 - PROGRESS: at 88.65% examples, 418980 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:23:37,833 : INFO : EPOCH 3 - PROGRESS: at 89.32% examples, 418901 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:23:38,838 : INFO : EPOCH 3 - PROGRESS: at 90.21% examples, 419171 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:23:39,845 : INFO : EPOCH 3 - PROGRESS: at 90.81% examples, 419186 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:23:40,898 : INFO : EPOCH 3 - PROGRESS: at 91.33% examples, 419113 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:23:41,957 : INFO : EPOCH 3 - PROGRESS: at 91.83% examples, 419069 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:23:42,965 : INFO : EPOCH 3 - PROGRESS: at 92.32% examples, 419110 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:23:43,997 : INFO : EPOCH 3 - PROGRESS: at 92.89% examples, 419514 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:23:45,010 : INFO : EPOCH 3 - PROGRESS: at 93.38% examples, 419408 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:23:46,043 : INFO : EPOCH 3 - PROGRESS: at 93.87% examples, 419415 words/s, in_qsize 4, out_qsize 3
2021-09-30 11:23:47,043 : INFO : EPOCH 3 - PROGRESS: at 94.43% examples, 419841 words/s, in_qsize 0, out_qsize 0
2021-09-30 11:23:48,113 : INFO : EPOCH 3 - PROGRESS: at 94.92% examples, 419704 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:23:49,126 : INFO : EPOCH 3 - PROGRESS: at 95.44% examples, 419860 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:23:50,132 : INFO : EPOCH 3 - PROGRESS: at 95.99% examples, 420021 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:23:51,147 : INFO : EPOCH 3 - PROGRESS: at 96.55% examples, 420236 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:23:52,189 : INFO : EPOCH 3 - PROGRESS: at 97.06% examples, 420316 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:23:53,210 : INFO : EPOCH 3 - PROGRESS: at 98.77% examples, 420361 words/s, in_qsize 0, out_qsize 3
2021-09-30 11:23:53,270 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-30 11:23:53,287 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-30 11:23:53,288 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-30 11:23:53,288 : INFO : EPOCH - 3 : training on 96321721 raw words (70186593 effective words) took 166.9s, 420604 effective words/s
2021-09-30 11:23:54,300 : INFO : EPOCH 4 - PROGRESS: at 0.65% examples, 390239 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:23:55,325 : INFO : EPOCH 4 - PROGRESS: at 1.27% examples, 387950 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:23:56,359 : INFO : EPOCH 4 - PROGRESS: at 1.97% examples, 394211 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:23:57,361 : INFO : EPOCH 4 - PROGRESS: at 2.52% examples, 391684 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:23:58,457 : INFO : EPOCH 4 - PROGRESS: at 3.20% examples, 398771 words/s, in_qsize 1, out_qsize 8
2021-09-30 11:23:59,463 : INFO : EPOCH 4 - PROGRESS: at 3.84% examples, 410419 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:24:00,548 : INFO : EPOCH 4 - PROGRESS: at 4.46% examples, 408142 words/s, in_qsize 4, out_qsize 3
2021-09-30 11:24:01,584 : INFO : EPOCH 4 - PROGRESS: at 5.06% examples, 412971 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:24:02,588 : INFO : EPOCH 4 - PROGRESS: at 5.83% examples, 415581 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:24:03,598 : INFO : EPOCH 4 - PROGRESS: at 6.66% examples, 422350 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:24:04,604 : INFO : EPOCH 4 - PROGRESS: at 7.13% examples, 427574 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:24:05,623 : INFO : EPOCH 4 - PROGRESS: at 7.58% examples, 429571 words/s, in_qsize 0, out_qsize 3
2021-09-30 11:24:06,651 : INFO : EPOCH 4 - PROGRESS: at 8.31% examples, 429639 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:24:07,703 : INFO : EPOCH 4 - PROGRESS: at 9.11% examples, 430558 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:24:08,706 : INFO : EPOCH 4 - PROGRESS: at 9.86% examples, 430494 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:24:09,721 : INFO : EPOCH 4 - PROGRESS: at 10.70% examples, 431181 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:24:10,735 : INFO : EPOCH 4 - PROGRESS: at 11.33% examples, 429265 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:24:11,755 : INFO : EPOCH 4 - PROGRESS: at 12.04% examples, 428477 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:24:12,772 : INFO : EPOCH 4 - PROGRESS: at 12.88% examples, 429732 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:24:13,786 : INFO : EPOCH 4 - PROGRESS: at 13.66% examples, 429498 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:24:14,823 : INFO : EPOCH 4 - PROGRESS: at 14.45% examples, 429952 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:24:15,836 : INFO : EPOCH 4 - PROGRESS: at 15.00% examples, 429209 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:24:16,866 : INFO : EPOCH 4 - PROGRESS: at 15.60% examples, 429242 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:24:17,923 : INFO : EPOCH 4 - PROGRESS: at 16.16% examples, 426528 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:24:18,931 : INFO : EPOCH 4 - PROGRESS: at 16.84% examples, 426661 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:24:19,963 : INFO : EPOCH 4 - PROGRESS: at 17.50% examples, 426727 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:24:20,981 : INFO : EPOCH 4 - PROGRESS: at 18.27% examples, 427441 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:24:22,006 : INFO : EPOCH 4 - PROGRESS: at 19.11% examples, 428785 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:24:23,045 : INFO : EPOCH 4 - PROGRESS: at 19.85% examples, 427764 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:24:24,081 : INFO : EPOCH 4 - PROGRESS: at 20.70% examples, 429385 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:24:25,082 : INFO : EPOCH 4 - PROGRESS: at 21.29% examples, 427767 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:24:26,092 : INFO : EPOCH 4 - PROGRESS: at 21.99% examples, 427413 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:24:27,106 : INFO : EPOCH 4 - PROGRESS: at 22.21% examples, 428123 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:24:28,134 : INFO : EPOCH 4 - PROGRESS: at 22.42% examples, 427520 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:24:29,146 : INFO : EPOCH 4 - PROGRESS: at 22.60% examples, 426470 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:24:30,155 : INFO : EPOCH 4 - PROGRESS: at 22.80% examples, 425931 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:24:31,156 : INFO : EPOCH 4 - PROGRESS: at 23.00% examples, 425519 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:24:32,175 : INFO : EPOCH 4 - PROGRESS: at 23.19% examples, 424706 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:24:33,264 : INFO : EPOCH 4 - PROGRESS: at 23.40% examples, 423058 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:24:34,365 : INFO : EPOCH 4 - PROGRESS: at 23.60% examples, 421687 words/s, in_qsize 0, out_qsize 7
2021-09-30 11:24:35,371 : INFO : EPOCH 4 - PROGRESS: at 23.80% examples, 421068 words/s, in_qsize 5, out_qsize 3
2021-09-30 11:24:36,389 : INFO : EPOCH 4 - PROGRESS: at 24.00% examples, 420457 words/s, in_qsize 5, out_qsize 3
2021-09-30 11:24:37,397 : INFO : EPOCH 4 - PROGRESS: at 24.19% examples, 418914 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:24:38,407 : INFO : EPOCH 4 - PROGRESS: at 24.40% examples, 418467 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:24:39,433 : INFO : EPOCH 4 - PROGRESS: at 24.92% examples, 418657 words/s, in_qsize 1, out_qsize 7
2021-09-30 11:24:40,458 : INFO : EPOCH 4 - PROGRESS: at 25.54% examples, 418802 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:24:41,477 : INFO : EPOCH 4 - PROGRESS: at 26.19% examples, 418400 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:24:42,479 : INFO : EPOCH 4 - PROGRESS: at 26.98% examples, 419605 words/s, in_qsize 0, out_qsize 0
2021-09-30 11:24:43,487 : INFO : EPOCH 4 - PROGRESS: at 27.74% examples, 419810 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:24:44,490 : INFO : EPOCH 4 - PROGRESS: at 28.19% examples, 419693 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:24:45,517 : INFO : EPOCH 4 - PROGRESS: at 28.50% examples, 420055 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:24:46,534 : INFO : EPOCH 4 - PROGRESS: at 28.93% examples, 419968 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:24:47,638 : INFO : EPOCH 4 - PROGRESS: at 29.43% examples, 420398 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:24:48,688 : INFO : EPOCH 4 - PROGRESS: at 30.09% examples, 420973 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:24:49,715 : INFO : EPOCH 4 - PROGRESS: at 30.82% examples, 421843 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:24:50,788 : INFO : EPOCH 4 - PROGRESS: at 31.54% examples, 422087 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:24:51,794 : INFO : EPOCH 4 - PROGRESS: at 32.35% examples, 422417 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:24:52,807 : INFO : EPOCH 4 - PROGRESS: at 33.20% examples, 422649 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:24:53,848 : INFO : EPOCH 4 - PROGRESS: at 34.09% examples, 423288 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:24:54,858 : INFO : EPOCH 4 - PROGRESS: at 34.90% examples, 423408 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:24:55,860 : INFO : EPOCH 4 - PROGRESS: at 35.82% examples, 424261 words/s, in_qsize 0, out_qsize 0
2021-09-30 11:24:56,874 : INFO : EPOCH 4 - PROGRESS: at 36.61% examples, 424309 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:24:57,931 : INFO : EPOCH 4 - PROGRESS: at 37.48% examples, 424544 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:24:58,935 : INFO : EPOCH 4 - PROGRESS: at 38.29% examples, 424442 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:24:59,939 : INFO : EPOCH 4 - PROGRESS: at 39.12% examples, 424556 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:25:00,950 : INFO : EPOCH 4 - PROGRESS: at 39.72% examples, 424865 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:25:01,961 : INFO : EPOCH 4 - PROGRESS: at 40.25% examples, 424188 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:25:02,969 : INFO : EPOCH 4 - PROGRESS: at 40.98% examples, 424490 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:25:03,977 : INFO : EPOCH 4 - PROGRESS: at 41.64% examples, 424837 words/s, in_qsize 1, out_qsize 3
2021-09-30 11:25:05,002 : INFO : EPOCH 4 - PROGRESS: at 42.38% examples, 425112 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:25:06,006 : INFO : EPOCH 4 - PROGRESS: at 43.12% examples, 424609 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:25:07,036 : INFO : EPOCH 4 - PROGRESS: at 43.79% examples, 424559 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:25:08,066 : INFO : EPOCH 4 - PROGRESS: at 44.54% examples, 424805 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:25:09,098 : INFO : EPOCH 4 - PROGRESS: at 45.09% examples, 424257 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:25:10,104 : INFO : EPOCH 4 - PROGRESS: at 45.83% examples, 424139 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:25:11,112 : INFO : EPOCH 4 - PROGRESS: at 46.73% examples, 424498 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:25:12,145 : INFO : EPOCH 4 - PROGRESS: at 47.25% examples, 423953 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:25:13,179 : INFO : EPOCH 4 - PROGRESS: at 47.96% examples, 424571 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:25:14,193 : INFO : EPOCH 4 - PROGRESS: at 48.62% examples, 424699 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:25:15,200 : INFO : EPOCH 4 - PROGRESS: at 49.24% examples, 424992 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:25:16,231 : INFO : EPOCH 4 - PROGRESS: at 50.00% examples, 425064 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:25:17,250 : INFO : EPOCH 4 - PROGRESS: at 50.90% examples, 425635 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:25:18,271 : INFO : EPOCH 4 - PROGRESS: at 51.17% examples, 425259 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:25:19,277 : INFO : EPOCH 4 - PROGRESS: at 51.25% examples, 425453 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:25:20,280 : INFO : EPOCH 4 - PROGRESS: at 51.69% examples, 425458 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:25:21,301 : INFO : EPOCH 4 - PROGRESS: at 52.17% examples, 425176 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:25:22,336 : INFO : EPOCH 4 - PROGRESS: at 52.63% examples, 424637 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:25:23,353 : INFO : EPOCH 4 - PROGRESS: at 52.96% examples, 424715 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:25:24,360 : INFO : EPOCH 4 - PROGRESS: at 53.28% examples, 424715 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:25:25,372 : INFO : EPOCH 4 - PROGRESS: at 53.65% examples, 424827 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:25:26,381 : INFO : EPOCH 4 - PROGRESS: at 54.04% examples, 424400 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:25:27,410 : INFO : EPOCH 4 - PROGRESS: at 54.41% examples, 424211 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:25:28,417 : INFO : EPOCH 4 - PROGRESS: at 54.78% examples, 424492 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:25:29,435 : INFO : EPOCH 4 - PROGRESS: at 55.18% examples, 424485 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:25:30,477 : INFO : EPOCH 4 - PROGRESS: at 55.57% examples, 423794 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:25:31,481 : INFO : EPOCH 4 - PROGRESS: at 55.99% examples, 423360 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:25:32,593 : INFO : EPOCH 4 - PROGRESS: at 56.40% examples, 423181 words/s, in_qsize 1, out_qsize 8
2021-09-30 11:25:33,685 : INFO : EPOCH 4 - PROGRESS: at 56.80% examples, 423442 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:25:34,692 : INFO : EPOCH 4 - PROGRESS: at 57.16% examples, 423636 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:25:35,702 : INFO : EPOCH 4 - PROGRESS: at 57.71% examples, 423476 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:25:36,787 : INFO : EPOCH 4 - PROGRESS: at 58.08% examples, 423079 words/s, in_qsize 5, out_qsize 3
2021-09-30 11:25:37,817 : INFO : EPOCH 4 - PROGRESS: at 58.53% examples, 423433 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:25:38,824 : INFO : EPOCH 4 - PROGRESS: at 59.16% examples, 423451 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:25:39,838 : INFO : EPOCH 4 - PROGRESS: at 59.87% examples, 423370 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:25:40,858 : INFO : EPOCH 4 - PROGRESS: at 60.64% examples, 423898 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:25:41,939 : INFO : EPOCH 4 - PROGRESS: at 61.32% examples, 423771 words/s, in_qsize 1, out_qsize 8
2021-09-30 11:25:42,951 : INFO : EPOCH 4 - PROGRESS: at 62.10% examples, 424275 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:25:43,955 : INFO : EPOCH 4 - PROGRESS: at 62.86% examples, 424427 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:25:44,965 : INFO : EPOCH 4 - PROGRESS: at 63.62% examples, 424449 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:25:45,969 : INFO : EPOCH 4 - PROGRESS: at 64.36% examples, 424596 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:25:46,983 : INFO : EPOCH 4 - PROGRESS: at 65.06% examples, 424527 words/s, in_qsize 2, out_qsize 3
2021-09-30 11:25:48,004 : INFO : EPOCH 4 - PROGRESS: at 65.63% examples, 424274 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:25:49,006 : INFO : EPOCH 4 - PROGRESS: at 66.24% examples, 424162 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:25:50,078 : INFO : EPOCH 4 - PROGRESS: at 66.65% examples, 423948 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:25:51,083 : INFO : EPOCH 4 - PROGRESS: at 67.01% examples, 423823 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:25:52,145 : INFO : EPOCH 4 - PROGRESS: at 67.62% examples, 423742 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:25:53,170 : INFO : EPOCH 4 - PROGRESS: at 68.36% examples, 423659 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:25:54,170 : INFO : EPOCH 4 - PROGRESS: at 69.03% examples, 423393 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:25:55,208 : INFO : EPOCH 4 - PROGRESS: at 69.79% examples, 423272 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:25:56,216 : INFO : EPOCH 4 - PROGRESS: at 70.47% examples, 422828 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:25:57,228 : INFO : EPOCH 4 - PROGRESS: at 71.45% examples, 423130 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:25:58,229 : INFO : EPOCH 4 - PROGRESS: at 72.29% examples, 423221 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:25:59,234 : INFO : EPOCH 4 - PROGRESS: at 73.09% examples, 423366 words/s, in_qsize 1, out_qsize 4
2021-09-30 11:26:00,241 : INFO : EPOCH 4 - PROGRESS: at 73.76% examples, 423486 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:26:01,257 : INFO : EPOCH 4 - PROGRESS: at 74.42% examples, 423486 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:26:02,291 : INFO : EPOCH 4 - PROGRESS: at 75.01% examples, 423417 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:26:03,330 : INFO : EPOCH 4 - PROGRESS: at 75.52% examples, 423180 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:26:04,384 : INFO : EPOCH 4 - PROGRESS: at 76.22% examples, 422963 words/s, in_qsize 4, out_qsize 6
2021-09-30 11:26:05,402 : INFO : EPOCH 4 - PROGRESS: at 77.19% examples, 423532 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:26:06,408 : INFO : EPOCH 4 - PROGRESS: at 77.89% examples, 423348 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:26:07,513 : INFO : EPOCH 4 - PROGRESS: at 78.67% examples, 423212 words/s, in_qsize 2, out_qsize 5
2021-09-30 11:26:08,516 : INFO : EPOCH 4 - PROGRESS: at 79.40% examples, 423586 words/s, in_qsize 0, out_qsize 0
2021-09-30 11:26:09,520 : INFO : EPOCH 4 - PROGRESS: at 80.06% examples, 423607 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:26:10,559 : INFO : EPOCH 4 - PROGRESS: at 80.70% examples, 423354 words/s, in_qsize 5, out_qsize 3
2021-09-30 11:26:11,568 : INFO : EPOCH 4 - PROGRESS: at 81.45% examples, 423392 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:26:12,615 : INFO : EPOCH 4 - PROGRESS: at 82.30% examples, 423491 words/s, in_qsize 2, out_qsize 4
2021-09-30 11:26:13,633 : INFO : EPOCH 4 - PROGRESS: at 83.02% examples, 423645 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:26:14,634 : INFO : EPOCH 4 - PROGRESS: at 83.57% examples, 423958 words/s, in_qsize 0, out_qsize 0
2021-09-30 11:26:15,667 : INFO : EPOCH 4 - PROGRESS: at 84.40% examples, 424033 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:26:16,693 : INFO : EPOCH 4 - PROGRESS: at 85.21% examples, 424180 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:26:17,694 : INFO : EPOCH 4 - PROGRESS: at 85.92% examples, 424110 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:26:18,749 : INFO : EPOCH 4 - PROGRESS: at 86.50% examples, 424041 words/s, in_qsize 2, out_qsize 5
2021-09-30 11:26:19,752 : INFO : EPOCH 4 - PROGRESS: at 87.23% examples, 424202 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:26:20,772 : INFO : EPOCH 4 - PROGRESS: at 87.92% examples, 424282 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:26:21,791 : INFO : EPOCH 4 - PROGRESS: at 88.66% examples, 424402 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:26:22,796 : INFO : EPOCH 4 - PROGRESS: at 89.44% examples, 424590 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:26:23,808 : INFO : EPOCH 4 - PROGRESS: at 90.24% examples, 424570 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:26:24,822 : INFO : EPOCH 4 - PROGRESS: at 90.84% examples, 424575 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:26:25,887 : INFO : EPOCH 4 - PROGRESS: at 91.39% examples, 424570 words/s, in_qsize 4, out_qsize 3
2021-09-30 11:26:26,888 : INFO : EPOCH 4 - PROGRESS: at 91.91% examples, 424835 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:26:27,907 : INFO : EPOCH 4 - PROGRESS: at 92.45% examples, 425048 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:26:28,909 : INFO : EPOCH 4 - PROGRESS: at 92.91% examples, 424934 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:26:29,945 : INFO : EPOCH 4 - PROGRESS: at 93.44% examples, 425007 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:26:30,968 : INFO : EPOCH 4 - PROGRESS: at 93.97% examples, 425194 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:26:31,973 : INFO : EPOCH 4 - PROGRESS: at 94.47% examples, 425201 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:26:33,002 : INFO : EPOCH 4 - PROGRESS: at 94.95% examples, 425049 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:26:34,006 : INFO : EPOCH 4 - PROGRESS: at 95.45% examples, 425153 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:26:35,006 : INFO : EPOCH 4 - PROGRESS: at 96.01% examples, 425342 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:26:36,031 : INFO : EPOCH 4 - PROGRESS: at 96.49% examples, 425103 words/s, in_qsize 1, out_qsize 4
2021-09-30 11:26:37,102 : INFO : EPOCH 4 - PROGRESS: at 97.04% examples, 425214 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:26:38,133 : INFO : EPOCH 4 - PROGRESS: at 97.98% examples, 425031 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:26:38,293 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-30 11:26:38,306 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-30 11:26:38,311 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-30 11:26:38,311 : INFO : EPOCH - 4 : training on 96321721 raw words (70187300 effective words) took 165.0s, 425319 effective words/s
2021-09-30 11:26:39,315 : INFO : EPOCH 5 - PROGRESS: at 0.65% examples, 393587 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:26:40,351 : INFO : EPOCH 5 - PROGRESS: at 1.32% examples, 405204 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:26:41,361 : INFO : EPOCH 5 - PROGRESS: at 1.96% examples, 394656 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:26:42,385 : INFO : EPOCH 5 - PROGRESS: at 2.56% examples, 398699 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:26:43,389 : INFO : EPOCH 5 - PROGRESS: at 3.13% examples, 395948 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:26:44,416 : INFO : EPOCH 5 - PROGRESS: at 3.57% examples, 383017 words/s, in_qsize 4, out_qsize 3
2021-09-30 11:26:45,417 : INFO : EPOCH 5 - PROGRESS: at 4.13% examples, 383273 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:26:46,437 : INFO : EPOCH 5 - PROGRESS: at 4.72% examples, 390475 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:26:47,464 : INFO : EPOCH 5 - PROGRESS: at 5.39% examples, 393826 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:26:48,512 : INFO : EPOCH 5 - PROGRESS: at 6.17% examples, 398227 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:26:49,547 : INFO : EPOCH 5 - PROGRESS: at 6.89% examples, 402007 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:26:50,560 : INFO : EPOCH 5 - PROGRESS: at 7.23% examples, 405402 words/s, in_qsize 1, out_qsize 4
2021-09-30 11:26:51,570 : INFO : EPOCH 5 - PROGRESS: at 7.74% examples, 406786 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:26:52,573 : INFO : EPOCH 5 - PROGRESS: at 8.43% examples, 408208 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:26:53,641 : INFO : EPOCH 5 - PROGRESS: at 9.21% examples, 408769 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:26:54,652 : INFO : EPOCH 5 - PROGRESS: at 9.93% examples, 408866 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:26:55,654 : INFO : EPOCH 5 - PROGRESS: at 10.78% examples, 411465 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:26:56,683 : INFO : EPOCH 5 - PROGRESS: at 11.45% examples, 411217 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:26:57,686 : INFO : EPOCH 5 - PROGRESS: at 12.19% examples, 412992 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:26:58,699 : INFO : EPOCH 5 - PROGRESS: at 13.00% examples, 414344 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:26:59,734 : INFO : EPOCH 5 - PROGRESS: at 13.76% examples, 413744 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:27:00,742 : INFO : EPOCH 5 - PROGRESS: at 14.43% examples, 412198 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:27:01,759 : INFO : EPOCH 5 - PROGRESS: at 14.91% examples, 409389 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:27:02,763 : INFO : EPOCH 5 - PROGRESS: at 15.40% examples, 407755 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:27:03,774 : INFO : EPOCH 5 - PROGRESS: at 15.98% examples, 407606 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:27:04,824 : INFO : EPOCH 5 - PROGRESS: at 16.70% examples, 409001 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:27:05,834 : INFO : EPOCH 5 - PROGRESS: at 17.39% examples, 410997 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:27:06,836 : INFO : EPOCH 5 - PROGRESS: at 18.17% examples, 412991 words/s, in_qsize 0, out_qsize 0
2021-09-30 11:27:07,847 : INFO : EPOCH 5 - PROGRESS: at 18.86% examples, 412293 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:27:08,868 : INFO : EPOCH 5 - PROGRESS: at 19.68% examples, 413675 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:27:09,880 : INFO : EPOCH 5 - PROGRESS: at 20.48% examples, 414477 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:27:10,907 : INFO : EPOCH 5 - PROGRESS: at 21.11% examples, 413899 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:27:12,005 : INFO : EPOCH 5 - PROGRESS: at 21.84% examples, 413577 words/s, in_qsize 5, out_qsize 4
2021-09-30 11:27:13,006 : INFO : EPOCH 5 - PROGRESS: at 22.16% examples, 414782 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:27:14,079 : INFO : EPOCH 5 - PROGRESS: at 22.38% examples, 414444 words/s, in_qsize 2, out_qsize 4
2021-09-30 11:27:15,082 : INFO : EPOCH 5 - PROGRESS: at 22.59% examples, 414985 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:27:16,101 : INFO : EPOCH 5 - PROGRESS: at 22.81% examples, 415918 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:27:17,124 : INFO : EPOCH 5 - PROGRESS: at 23.01% examples, 415902 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:27:18,142 : INFO : EPOCH 5 - PROGRESS: at 23.22% examples, 415897 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:27:19,154 : INFO : EPOCH 5 - PROGRESS: at 23.44% examples, 416143 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:27:20,208 : INFO : EPOCH 5 - PROGRESS: at 23.67% examples, 416745 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:27:21,210 : INFO : EPOCH 5 - PROGRESS: at 23.88% examples, 416890 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:27:22,247 : INFO : EPOCH 5 - PROGRESS: at 24.11% examples, 417025 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:27:23,252 : INFO : EPOCH 5 - PROGRESS: at 24.32% examples, 416655 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:27:24,265 : INFO : EPOCH 5 - PROGRESS: at 24.72% examples, 416458 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:27:25,303 : INFO : EPOCH 5 - PROGRESS: at 25.26% examples, 416830 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:27:26,334 : INFO : EPOCH 5 - PROGRESS: at 25.91% examples, 415895 words/s, in_qsize 5, out_qsize 4
2021-09-30 11:27:27,347 : INFO : EPOCH 5 - PROGRESS: at 26.65% examples, 417108 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:27:28,359 : INFO : EPOCH 5 - PROGRESS: at 27.43% examples, 417605 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:27:29,383 : INFO : EPOCH 5 - PROGRESS: at 28.09% examples, 418427 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:27:30,386 : INFO : EPOCH 5 - PROGRESS: at 28.37% examples, 418222 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:27:31,403 : INFO : EPOCH 5 - PROGRESS: at 28.83% examples, 418782 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:27:32,422 : INFO : EPOCH 5 - PROGRESS: at 29.22% examples, 418916 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:27:33,439 : INFO : EPOCH 5 - PROGRESS: at 29.79% examples, 419238 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:27:34,457 : INFO : EPOCH 5 - PROGRESS: at 30.37% examples, 418797 words/s, in_qsize 0, out_qsize 7
2021-09-30 11:27:35,518 : INFO : EPOCH 5 - PROGRESS: at 30.96% examples, 417773 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:27:36,521 : INFO : EPOCH 5 - PROGRESS: at 31.55% examples, 417088 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:27:37,547 : INFO : EPOCH 5 - PROGRESS: at 32.25% examples, 416375 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:27:38,552 : INFO : EPOCH 5 - PROGRESS: at 33.10% examples, 416769 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:27:39,557 : INFO : EPOCH 5 - PROGRESS: at 33.90% examples, 416931 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:27:40,564 : INFO : EPOCH 5 - PROGRESS: at 34.74% examples, 417408 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:27:41,579 : INFO : EPOCH 5 - PROGRESS: at 35.57% examples, 417587 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:27:42,615 : INFO : EPOCH 5 - PROGRESS: at 36.43% examples, 418030 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:27:43,654 : INFO : EPOCH 5 - PROGRESS: at 37.19% examples, 417705 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:27:44,658 : INFO : EPOCH 5 - PROGRESS: at 38.16% examples, 419023 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:27:45,682 : INFO : EPOCH 5 - PROGRESS: at 39.07% examples, 419617 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:27:46,693 : INFO : EPOCH 5 - PROGRESS: at 39.60% examples, 418944 words/s, in_qsize 4, out_qsize 5
2021-09-30 11:27:47,695 : INFO : EPOCH 5 - PROGRESS: at 40.27% examples, 420083 words/s, in_qsize 0, out_qsize 0
2021-09-30 11:27:48,711 : INFO : EPOCH 5 - PROGRESS: at 40.98% examples, 420190 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:27:49,721 : INFO : EPOCH 5 - PROGRESS: at 41.57% examples, 420075 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:27:50,745 : INFO : EPOCH 5 - PROGRESS: at 42.37% examples, 420713 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:27:51,771 : INFO : EPOCH 5 - PROGRESS: at 43.13% examples, 420440 words/s, in_qsize 4, out_qsize 3
2021-09-30 11:27:52,805 : INFO : EPOCH 5 - PROGRESS: at 43.92% examples, 421315 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:27:53,812 : INFO : EPOCH 5 - PROGRESS: at 44.59% examples, 421146 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:27:54,905 : INFO : EPOCH 5 - PROGRESS: at 45.27% examples, 421290 words/s, in_qsize 3, out_qsize 6
2021-09-30 11:27:55,916 : INFO : EPOCH 5 - PROGRESS: at 46.13% examples, 421700 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:27:56,935 : INFO : EPOCH 5 - PROGRESS: at 46.86% examples, 421405 words/s, in_qsize 5, out_qsize 3
2021-09-30 11:27:57,960 : INFO : EPOCH 5 - PROGRESS: at 47.38% examples, 420773 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:27:58,991 : INFO : EPOCH 5 - PROGRESS: at 47.97% examples, 420534 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:27:59,994 : INFO : EPOCH 5 - PROGRESS: at 48.70% examples, 421356 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:28:01,008 : INFO : EPOCH 5 - PROGRESS: at 49.25% examples, 421158 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:28:02,021 : INFO : EPOCH 5 - PROGRESS: at 50.02% examples, 421373 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:28:03,052 : INFO : EPOCH 5 - PROGRESS: at 50.93% examples, 421929 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:28:04,076 : INFO : EPOCH 5 - PROGRESS: at 51.17% examples, 421974 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:28:05,079 : INFO : EPOCH 5 - PROGRESS: at 51.35% examples, 422170 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:28:06,127 : INFO : EPOCH 5 - PROGRESS: at 51.74% examples, 422161 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:28:07,183 : INFO : EPOCH 5 - PROGRESS: at 52.32% examples, 422407 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:28:08,206 : INFO : EPOCH 5 - PROGRESS: at 52.76% examples, 422615 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:28:09,235 : INFO : EPOCH 5 - PROGRESS: at 53.11% examples, 422914 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:28:10,252 : INFO : EPOCH 5 - PROGRESS: at 53.46% examples, 423094 words/s, in_qsize 1, out_qsize 3
2021-09-30 11:28:11,299 : INFO : EPOCH 5 - PROGRESS: at 53.90% examples, 423442 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:28:12,306 : INFO : EPOCH 5 - PROGRESS: at 54.31% examples, 423600 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:28:13,343 : INFO : EPOCH 5 - PROGRESS: at 54.68% examples, 423602 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:28:14,385 : INFO : EPOCH 5 - PROGRESS: at 55.03% examples, 423194 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:28:15,390 : INFO : EPOCH 5 - PROGRESS: at 55.39% examples, 422600 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:28:16,422 : INFO : EPOCH 5 - PROGRESS: at 55.90% examples, 422871 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:28:17,425 : INFO : EPOCH 5 - PROGRESS: at 56.33% examples, 423229 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:28:18,466 : INFO : EPOCH 5 - PROGRESS: at 56.67% examples, 422845 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:28:19,536 : INFO : EPOCH 5 - PROGRESS: at 57.04% examples, 423000 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:28:20,563 : INFO : EPOCH 5 - PROGRESS: at 57.46% examples, 422766 words/s, in_qsize 0, out_qsize 3
2021-09-30 11:28:21,569 : INFO : EPOCH 5 - PROGRESS: at 57.95% examples, 422699 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:28:22,576 : INFO : EPOCH 5 - PROGRESS: at 58.37% examples, 422803 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:28:23,576 : INFO : EPOCH 5 - PROGRESS: at 58.85% examples, 422676 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:28:24,599 : INFO : EPOCH 5 - PROGRESS: at 59.58% examples, 422848 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:28:25,685 : INFO : EPOCH 5 - PROGRESS: at 60.24% examples, 422280 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:28:26,715 : INFO : EPOCH 5 - PROGRESS: at 60.90% examples, 422241 words/s, in_qsize 4, out_qsize 3
2021-09-30 11:28:27,724 : INFO : EPOCH 5 - PROGRESS: at 61.66% examples, 422685 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:28:28,725 : INFO : EPOCH 5 - PROGRESS: at 62.35% examples, 422778 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:28:29,739 : INFO : EPOCH 5 - PROGRESS: at 63.12% examples, 422955 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:28:30,764 : INFO : EPOCH 5 - PROGRESS: at 63.84% examples, 422844 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:28:31,794 : INFO : EPOCH 5 - PROGRESS: at 64.60% examples, 422931 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:28:32,803 : INFO : EPOCH 5 - PROGRESS: at 65.32% examples, 423185 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:28:33,806 : INFO : EPOCH 5 - PROGRESS: at 65.86% examples, 422901 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:28:34,826 : INFO : EPOCH 5 - PROGRESS: at 66.44% examples, 422990 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:28:35,865 : INFO : EPOCH 5 - PROGRESS: at 66.82% examples, 422925 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:28:36,954 : INFO : EPOCH 5 - PROGRESS: at 67.24% examples, 422821 words/s, in_qsize 5, out_qsize 4
2021-09-30 11:28:37,971 : INFO : EPOCH 5 - PROGRESS: at 68.11% examples, 423284 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:28:38,971 : INFO : EPOCH 5 - PROGRESS: at 68.79% examples, 423113 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:28:39,971 : INFO : EPOCH 5 - PROGRESS: at 69.60% examples, 423373 words/s, in_qsize 0, out_qsize 0
2021-09-30 11:28:40,974 : INFO : EPOCH 5 - PROGRESS: at 70.40% examples, 423538 words/s, in_qsize 0, out_qsize 0
2021-09-30 11:28:41,977 : INFO : EPOCH 5 - PROGRESS: at 71.34% examples, 423635 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:28:43,006 : INFO : EPOCH 5 - PROGRESS: at 72.23% examples, 423856 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:28:44,011 : INFO : EPOCH 5 - PROGRESS: at 72.97% examples, 423652 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:28:45,043 : INFO : EPOCH 5 - PROGRESS: at 73.67% examples, 423799 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:28:46,120 : INFO : EPOCH 5 - PROGRESS: at 74.28% examples, 423417 words/s, in_qsize 2, out_qsize 5
2021-09-30 11:28:47,131 : INFO : EPOCH 5 - PROGRESS: at 74.81% examples, 422978 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:28:48,155 : INFO : EPOCH 5 - PROGRESS: at 75.37% examples, 422755 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:28:49,194 : INFO : EPOCH 5 - PROGRESS: at 76.09% examples, 423081 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:28:50,205 : INFO : EPOCH 5 - PROGRESS: at 76.90% examples, 423013 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:28:51,210 : INFO : EPOCH 5 - PROGRESS: at 77.70% examples, 423309 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:28:52,252 : INFO : EPOCH 5 - PROGRESS: at 78.55% examples, 423447 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:28:53,252 : INFO : EPOCH 5 - PROGRESS: at 79.22% examples, 423602 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:28:54,253 : INFO : EPOCH 5 - PROGRESS: at 79.87% examples, 423589 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:28:55,285 : INFO : EPOCH 5 - PROGRESS: at 80.49% examples, 423337 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:28:56,317 : INFO : EPOCH 5 - PROGRESS: at 81.08% examples, 422671 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:28:57,332 : INFO : EPOCH 5 - PROGRESS: at 81.73% examples, 422375 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:28:58,338 : INFO : EPOCH 5 - PROGRESS: at 82.58% examples, 422455 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:28:59,372 : INFO : EPOCH 5 - PROGRESS: at 83.12% examples, 422247 words/s, in_qsize 6, out_qsize 3
2021-09-30 11:29:00,378 : INFO : EPOCH 5 - PROGRESS: at 83.73% examples, 422399 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:29:01,393 : INFO : EPOCH 5 - PROGRESS: at 84.59% examples, 422674 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:29:02,443 : INFO : EPOCH 5 - PROGRESS: at 85.41% examples, 422663 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:29:03,464 : INFO : EPOCH 5 - PROGRESS: at 86.01% examples, 422449 words/s, in_qsize 2, out_qsize 7
2021-09-30 11:29:04,496 : INFO : EPOCH 5 - PROGRESS: at 86.63% examples, 422756 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:29:05,497 : INFO : EPOCH 5 - PROGRESS: at 87.44% examples, 422975 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:29:06,529 : INFO : EPOCH 5 - PROGRESS: at 88.07% examples, 422785 words/s, in_qsize 0, out_qsize 6
2021-09-30 11:29:07,532 : INFO : EPOCH 5 - PROGRESS: at 88.82% examples, 423282 words/s, in_qsize 0, out_qsize 0
2021-09-30 11:29:08,545 : INFO : EPOCH 5 - PROGRESS: at 89.62% examples, 423131 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:29:09,594 : INFO : EPOCH 5 - PROGRESS: at 90.48% examples, 423276 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:29:10,596 : INFO : EPOCH 5 - PROGRESS: at 91.04% examples, 423610 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:29:11,598 : INFO : EPOCH 5 - PROGRESS: at 91.52% examples, 423449 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:29:12,629 : INFO : EPOCH 5 - PROGRESS: at 92.03% examples, 423540 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:29:13,672 : INFO : EPOCH 5 - PROGRESS: at 92.60% examples, 423890 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:29:14,711 : INFO : EPOCH 5 - PROGRESS: at 93.14% examples, 424006 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:29:15,740 : INFO : EPOCH 5 - PROGRESS: at 93.66% examples, 424149 words/s, in_qsize 0, out_qsize 5
2021-09-30 11:29:16,771 : INFO : EPOCH 5 - PROGRESS: at 94.19% examples, 424321 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:29:17,823 : INFO : EPOCH 5 - PROGRESS: at 94.73% examples, 424426 words/s, in_qsize 0, out_qsize 4
2021-09-30 11:29:18,855 : INFO : EPOCH 5 - PROGRESS: at 95.31% examples, 424766 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:29:19,881 : INFO : EPOCH 5 - PROGRESS: at 95.85% examples, 424895 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:29:20,904 : INFO : EPOCH 5 - PROGRESS: at 96.40% examples, 425066 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:29:21,942 : INFO : EPOCH 5 - PROGRESS: at 96.92% examples, 425076 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:29:22,952 : INFO : EPOCH 5 - PROGRESS: at 97.61% examples, 425118 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:29:23,399 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-30 11:29:23,417 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-30 11:29:23,420 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-30 11:29:23,420 : INFO : EPOCH - 5 : training on 96321721 raw words (70189542 effective words) took 165.1s, 425112 effective words/s
2021-09-30 11:29:24,456 : INFO : EPOCH 6 - PROGRESS: at 0.63% examples, 366897 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:29:25,460 : INFO : EPOCH 6 - PROGRESS: at 1.31% examples, 401520 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:29:26,463 : INFO : EPOCH 6 - PROGRESS: at 1.98% examples, 400216 words/s, in_qsize 4, out_qsize 4
2021-09-30 11:29:27,509 : INFO : EPOCH 6 - PROGRESS: at 2.60% examples, 402398 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:29:28,543 : INFO : EPOCH 6 - PROGRESS: at 3.27% examples, 412167 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:29:29,545 : INFO : EPOCH 6 - PROGRESS: at 3.82% examples, 411327 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:29:30,558 : INFO : EPOCH 6 - PROGRESS: at 4.39% examples, 407921 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:29:31,562 : INFO : EPOCH 6 - PROGRESS: at 4.87% examples, 404698 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:29:32,564 : INFO : EPOCH 6 - PROGRESS: at 5.49% examples, 400648 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:29:33,589 : INFO : EPOCH 6 - PROGRESS: at 6.13% examples, 397352 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:29:34,617 : INFO : EPOCH 6 - PROGRESS: at 6.81% examples, 397428 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:29:35,636 : INFO : EPOCH 6 - PROGRESS: at 7.19% examples, 402825 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:29:36,640 : INFO : EPOCH 6 - PROGRESS: at 7.71% examples, 406347 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:29:37,680 : INFO : EPOCH 6 - PROGRESS: at 8.46% examples, 409290 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:29:38,693 : INFO : EPOCH 6 - PROGRESS: at 9.15% examples, 408352 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:29:39,751 : INFO : EPOCH 6 - PROGRESS: at 9.90% examples, 407829 words/s, in_qsize 1, out_qsize 4
2021-09-30 11:29:40,756 : INFO : EPOCH 6 - PROGRESS: at 10.75% examples, 410433 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:29:41,764 : INFO : EPOCH 6 - PROGRESS: at 11.37% examples, 409508 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:29:42,778 : INFO : EPOCH 6 - PROGRESS: at 12.10% examples, 410685 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:29:43,784 : INFO : EPOCH 6 - PROGRESS: at 12.85% examples, 410503 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:29:44,799 : INFO : EPOCH 6 - PROGRESS: at 13.61% examples, 410457 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:29:45,805 : INFO : EPOCH 6 - PROGRESS: at 14.32% examples, 409468 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:29:46,861 : INFO : EPOCH 6 - PROGRESS: at 14.83% examples, 407013 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:29:47,865 : INFO : EPOCH 6 - PROGRESS: at 15.31% examples, 405201 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:29:48,890 : INFO : EPOCH 6 - PROGRESS: at 15.92% examples, 405809 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:29:49,915 : INFO : EPOCH 6 - PROGRESS: at 16.56% examples, 406334 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:29:50,923 : INFO : EPOCH 6 - PROGRESS: at 17.20% examples, 407128 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:29:51,924 : INFO : EPOCH 6 - PROGRESS: at 17.89% examples, 407453 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:29:52,928 : INFO : EPOCH 6 - PROGRESS: at 18.53% examples, 406107 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:29:53,941 : INFO : EPOCH 6 - PROGRESS: at 19.11% examples, 403488 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:29:54,961 : INFO : EPOCH 6 - PROGRESS: at 19.75% examples, 401951 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:29:56,055 : INFO : EPOCH 6 - PROGRESS: at 20.58% examples, 402946 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:29:57,075 : INFO : EPOCH 6 - PROGRESS: at 21.31% examples, 404362 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:29:58,100 : INFO : EPOCH 6 - PROGRESS: at 21.96% examples, 403481 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:29:59,103 : INFO : EPOCH 6 - PROGRESS: at 22.14% examples, 401395 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:30:00,111 : INFO : EPOCH 6 - PROGRESS: at 22.28% examples, 399005 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:30:01,151 : INFO : EPOCH 6 - PROGRESS: at 22.45% examples, 397007 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:30:02,175 : INFO : EPOCH 6 - PROGRESS: at 22.64% examples, 396354 words/s, in_qsize 3, out_qsize 5
2021-09-30 11:30:03,183 : INFO : EPOCH 6 - PROGRESS: at 22.81% examples, 395623 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:30:04,204 : INFO : EPOCH 6 - PROGRESS: at 23.01% examples, 395795 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:30:05,265 : INFO : EPOCH 6 - PROGRESS: at 23.22% examples, 395878 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:30:06,265 : INFO : EPOCH 6 - PROGRESS: at 23.42% examples, 395890 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:30:07,276 : INFO : EPOCH 6 - PROGRESS: at 23.62% examples, 395776 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:30:08,309 : INFO : EPOCH 6 - PROGRESS: at 23.82% examples, 395674 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:30:09,356 : INFO : EPOCH 6 - PROGRESS: at 24.01% examples, 394827 words/s, in_qsize 6, out_qsize 5
2021-09-30 11:30:10,368 : INFO : EPOCH 6 - PROGRESS: at 24.22% examples, 394767 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:30:11,379 : INFO : EPOCH 6 - PROGRESS: at 24.43% examples, 395131 words/s, in_qsize 0, out_qsize 0
2021-09-30 11:30:12,386 : INFO : EPOCH 6 - PROGRESS: at 24.94% examples, 394989 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:30:13,411 : INFO : EPOCH 6 - PROGRESS: at 25.66% examples, 396515 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:30:14,438 : INFO : EPOCH 6 - PROGRESS: at 26.22% examples, 395653 words/s, in_qsize 5, out_qsize 3
2021-09-30 11:30:15,450 : INFO : EPOCH 6 - PROGRESS: at 26.97% examples, 396596 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:30:16,474 : INFO : EPOCH 6 - PROGRESS: at 27.68% examples, 396682 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:30:17,492 : INFO : EPOCH 6 - PROGRESS: at 28.18% examples, 397177 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:30:18,517 : INFO : EPOCH 6 - PROGRESS: at 28.42% examples, 396685 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:30:19,526 : INFO : EPOCH 6 - PROGRESS: at 28.88% examples, 397382 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:30:20,539 : INFO : EPOCH 6 - PROGRESS: at 29.31% examples, 398534 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:30:21,544 : INFO : EPOCH 6 - PROGRESS: at 29.87% examples, 398640 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:30:22,558 : INFO : EPOCH 6 - PROGRESS: at 30.53% examples, 399211 words/s, in_qsize 2, out_qsize 6
2021-09-30 11:30:23,670 : INFO : EPOCH 6 - PROGRESS: at 31.24% examples, 400070 words/s, in_qsize 1, out_qsize 8
2021-09-30 11:30:24,694 : INFO : EPOCH 6 - PROGRESS: at 32.13% examples, 401454 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:30:25,748 : INFO : EPOCH 6 - PROGRESS: at 32.92% examples, 401297 words/s, in_qsize 6, out_qsize 3
2021-09-30 11:30:26,776 : INFO : EPOCH 6 - PROGRESS: at 33.88% examples, 402911 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:30:27,795 : INFO : EPOCH 6 - PROGRESS: at 34.72% examples, 403515 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:30:28,805 : INFO : EPOCH 6 - PROGRESS: at 35.62% examples, 404378 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:30:29,806 : INFO : EPOCH 6 - PROGRESS: at 36.40% examples, 404683 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:30:30,825 : INFO : EPOCH 6 - PROGRESS: at 37.32% examples, 405864 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:30:31,837 : INFO : EPOCH 6 - PROGRESS: at 38.12% examples, 405997 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:30:32,864 : INFO : EPOCH 6 - PROGRESS: at 38.98% examples, 406446 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:30:33,873 : INFO : EPOCH 6 - PROGRESS: at 39.60% examples, 406595 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:30:34,895 : INFO : EPOCH 6 - PROGRESS: at 40.04% examples, 405787 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:30:35,896 : INFO : EPOCH 6 - PROGRESS: at 40.76% examples, 406306 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:30:36,924 : INFO : EPOCH 6 - PROGRESS: at 41.43% examples, 406996 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:30:38,052 : INFO : EPOCH 6 - PROGRESS: at 42.23% examples, 407135 words/s, in_qsize 4, out_qsize 4
2021-09-30 11:30:39,060 : INFO : EPOCH 6 - PROGRESS: at 43.04% examples, 407621 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:30:40,076 : INFO : EPOCH 6 - PROGRESS: at 43.66% examples, 407203 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:30:41,089 : INFO : EPOCH 6 - PROGRESS: at 44.20% examples, 406326 words/s, in_qsize 5, out_qsize 3
2021-09-30 11:30:42,090 : INFO : EPOCH 6 - PROGRESS: at 44.88% examples, 406682 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:30:43,122 : INFO : EPOCH 6 - PROGRESS: at 45.54% examples, 406774 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:30:44,132 : INFO : EPOCH 6 - PROGRESS: at 46.25% examples, 406234 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:30:45,138 : INFO : EPOCH 6 - PROGRESS: at 46.97% examples, 406469 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:30:46,145 : INFO : EPOCH 6 - PROGRESS: at 47.60% examples, 406982 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:30:47,175 : INFO : EPOCH 6 - PROGRESS: at 48.20% examples, 407016 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:30:48,208 : INFO : EPOCH 6 - PROGRESS: at 48.82% examples, 406707 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:30:49,222 : INFO : EPOCH 6 - PROGRESS: at 49.24% examples, 405716 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:30:50,230 : INFO : EPOCH 6 - PROGRESS: at 49.88% examples, 405360 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:30:51,258 : INFO : EPOCH 6 - PROGRESS: at 50.65% examples, 405402 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:30:52,318 : INFO : EPOCH 6 - PROGRESS: at 51.15% examples, 405284 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:30:53,335 : INFO : EPOCH 6 - PROGRESS: at 51.20% examples, 405697 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:30:54,422 : INFO : EPOCH 6 - PROGRESS: at 51.68% examples, 405538 words/s, in_qsize 3, out_qsize 5
2021-09-30 11:30:55,436 : INFO : EPOCH 6 - PROGRESS: at 51.98% examples, 405654 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:30:56,445 : INFO : EPOCH 6 - PROGRESS: at 52.54% examples, 405778 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:30:57,446 : INFO : EPOCH 6 - PROGRESS: at 52.91% examples, 406106 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:30:58,490 : INFO : EPOCH 6 - PROGRESS: at 53.20% examples, 406075 words/s, in_qsize 3, out_qsize 6
2021-09-30 11:30:59,504 : INFO : EPOCH 6 - PROGRESS: at 53.63% examples, 406740 words/s, in_qsize 1, out_qsize 4
2021-09-30 11:31:00,521 : INFO : EPOCH 6 - PROGRESS: at 54.08% examples, 407315 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:31:01,553 : INFO : EPOCH 6 - PROGRESS: at 54.48% examples, 407661 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:31:02,578 : INFO : EPOCH 6 - PROGRESS: at 54.87% examples, 408158 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:31:03,626 : INFO : EPOCH 6 - PROGRESS: at 55.26% examples, 408137 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:31:04,629 : INFO : EPOCH 6 - PROGRESS: at 55.60% examples, 407233 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:31:05,660 : INFO : EPOCH 6 - PROGRESS: at 55.99% examples, 406585 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:31:06,682 : INFO : EPOCH 6 - PROGRESS: at 56.34% examples, 406251 words/s, in_qsize 5, out_qsize 3
2021-09-30 11:31:07,709 : INFO : EPOCH 6 - PROGRESS: at 56.73% examples, 406727 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:31:08,713 : INFO : EPOCH 6 - PROGRESS: at 57.08% examples, 407021 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:31:09,733 : INFO : EPOCH 6 - PROGRESS: at 57.54% examples, 406980 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:31:10,749 : INFO : EPOCH 6 - PROGRESS: at 58.00% examples, 407164 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:31:11,853 : INFO : EPOCH 6 - PROGRESS: at 58.44% examples, 407172 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:31:12,868 : INFO : EPOCH 6 - PROGRESS: at 58.90% examples, 406756 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:31:13,906 : INFO : EPOCH 6 - PROGRESS: at 59.61% examples, 406944 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:31:14,923 : INFO : EPOCH 6 - PROGRESS: at 60.36% examples, 407345 words/s, in_qsize 0, out_qsize 0
2021-09-30 11:31:15,934 : INFO : EPOCH 6 - PROGRESS: at 60.95% examples, 407107 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:31:16,948 : INFO : EPOCH 6 - PROGRESS: at 61.69% examples, 407516 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:31:17,991 : INFO : EPOCH 6 - PROGRESS: at 62.43% examples, 407716 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:31:18,993 : INFO : EPOCH 6 - PROGRESS: at 63.16% examples, 407940 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:31:20,012 : INFO : EPOCH 6 - PROGRESS: at 63.83% examples, 407733 words/s, in_qsize 2, out_qsize 3
2021-09-30 11:31:21,038 : INFO : EPOCH 6 - PROGRESS: at 64.54% examples, 407714 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:31:22,060 : INFO : EPOCH 6 - PROGRESS: at 65.21% examples, 407625 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:31:23,069 : INFO : EPOCH 6 - PROGRESS: at 65.75% examples, 407513 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:31:24,110 : INFO : EPOCH 6 - PROGRESS: at 66.30% examples, 407178 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:31:25,165 : INFO : EPOCH 6 - PROGRESS: at 66.71% examples, 407248 words/s, in_qsize 0, out_qsize 3
2021-09-30 11:31:26,189 : INFO : EPOCH 6 - PROGRESS: at 67.07% examples, 407178 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:31:27,247 : INFO : EPOCH 6 - PROGRESS: at 67.79% examples, 407553 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:31:28,262 : INFO : EPOCH 6 - PROGRESS: at 68.56% examples, 407754 words/s, in_qsize 0, out_qsize 3
2021-09-30 11:31:29,312 : INFO : EPOCH 6 - PROGRESS: at 69.32% examples, 407952 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:31:30,361 : INFO : EPOCH 6 - PROGRESS: at 70.13% examples, 408029 words/s, in_qsize 5, out_qsize 3
2021-09-30 11:31:31,377 : INFO : EPOCH 6 - PROGRESS: at 71.09% examples, 408489 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:31:32,399 : INFO : EPOCH 6 - PROGRESS: at 72.04% examples, 408870 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:31:33,410 : INFO : EPOCH 6 - PROGRESS: at 72.82% examples, 408923 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:31:34,437 : INFO : EPOCH 6 - PROGRESS: at 73.55% examples, 409360 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:31:35,439 : INFO : EPOCH 6 - PROGRESS: at 74.20% examples, 409447 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:31:36,459 : INFO : EPOCH 6 - PROGRESS: at 74.84% examples, 409710 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:31:37,465 : INFO : EPOCH 6 - PROGRESS: at 75.43% examples, 409864 words/s, in_qsize 0, out_qsize 3
2021-09-30 11:31:38,496 : INFO : EPOCH 6 - PROGRESS: at 76.13% examples, 410135 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:31:39,509 : INFO : EPOCH 6 - PROGRESS: at 77.01% examples, 410378 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:31:40,510 : INFO : EPOCH 6 - PROGRESS: at 77.72% examples, 410456 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:31:41,538 : INFO : EPOCH 6 - PROGRESS: at 78.53% examples, 410565 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:31:42,544 : INFO : EPOCH 6 - PROGRESS: at 79.20% examples, 410742 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:31:43,548 : INFO : EPOCH 6 - PROGRESS: at 79.93% examples, 411177 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:31:44,568 : INFO : EPOCH 6 - PROGRESS: at 80.64% examples, 411476 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:31:45,659 : INFO : EPOCH 6 - PROGRESS: at 81.44% examples, 411566 words/s, in_qsize 1, out_qsize 4
2021-09-30 11:31:46,666 : INFO : EPOCH 6 - PROGRESS: at 82.28% examples, 411862 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:31:47,681 : INFO : EPOCH 6 - PROGRESS: at 82.97% examples, 411850 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:31:48,681 : INFO : EPOCH 6 - PROGRESS: at 83.49% examples, 412234 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:31:49,684 : INFO : EPOCH 6 - PROGRESS: at 84.30% examples, 412425 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:31:50,716 : INFO : EPOCH 6 - PROGRESS: at 85.06% examples, 412482 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:31:51,717 : INFO : EPOCH 6 - PROGRESS: at 85.86% examples, 412687 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:31:52,754 : INFO : EPOCH 6 - PROGRESS: at 86.48% examples, 412896 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:31:53,764 : INFO : EPOCH 6 - PROGRESS: at 87.04% examples, 412484 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:31:54,810 : INFO : EPOCH 6 - PROGRESS: at 87.71% examples, 412342 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:31:55,831 : INFO : EPOCH 6 - PROGRESS: at 88.40% examples, 412363 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:31:56,854 : INFO : EPOCH 6 - PROGRESS: at 89.04% examples, 412460 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:31:57,871 : INFO : EPOCH 6 - PROGRESS: at 89.88% examples, 412583 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:31:58,885 : INFO : EPOCH 6 - PROGRESS: at 90.59% examples, 412482 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:31:59,894 : INFO : EPOCH 6 - PROGRESS: at 91.14% examples, 412757 words/s, in_qsize 1, out_qsize 3
2021-09-30 11:32:00,919 : INFO : EPOCH 6 - PROGRESS: at 91.69% examples, 413077 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:32:01,948 : INFO : EPOCH 6 - PROGRESS: at 92.21% examples, 413284 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:32:02,967 : INFO : EPOCH 6 - PROGRESS: at 92.72% examples, 413382 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:32:04,011 : INFO : EPOCH 6 - PROGRESS: at 93.18% examples, 413153 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:32:05,028 : INFO : EPOCH 6 - PROGRESS: at 93.66% examples, 413162 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:32:06,075 : INFO : EPOCH 6 - PROGRESS: at 94.22% examples, 413498 words/s, in_qsize 2, out_qsize 3
2021-09-30 11:32:07,098 : INFO : EPOCH 6 - PROGRESS: at 94.75% examples, 413741 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:32:08,113 : INFO : EPOCH 6 - PROGRESS: at 95.31% examples, 414053 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:32:09,125 : INFO : EPOCH 6 - PROGRESS: at 95.81% examples, 414059 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:32:10,126 : INFO : EPOCH 6 - PROGRESS: at 96.30% examples, 414044 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:32:11,142 : INFO : EPOCH 6 - PROGRESS: at 96.80% examples, 414045 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:32:12,155 : INFO : EPOCH 6 - PROGRESS: at 97.43% examples, 414190 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:32:12,747 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-30 11:32:12,766 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-30 11:32:12,766 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-30 11:32:12,766 : INFO : EPOCH - 6 : training on 96321721 raw words (70187854 effective words) took 169.3s, 414466 effective words/s
2021-09-30 11:32:13,770 : INFO : EPOCH 7 - PROGRESS: at 0.71% examples, 422298 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:32:14,808 : INFO : EPOCH 7 - PROGRESS: at 1.41% examples, 426300 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:32:15,808 : INFO : EPOCH 7 - PROGRESS: at 2.09% examples, 429318 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:32:16,836 : INFO : EPOCH 7 - PROGRESS: at 2.79% examples, 437817 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:32:17,853 : INFO : EPOCH 7 - PROGRESS: at 3.42% examples, 436676 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:32:18,854 : INFO : EPOCH 7 - PROGRESS: at 4.03% examples, 436534 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:32:19,881 : INFO : EPOCH 7 - PROGRESS: at 4.64% examples, 436691 words/s, in_qsize 1, out_qsize 3
2021-09-30 11:32:20,932 : INFO : EPOCH 7 - PROGRESS: at 5.29% examples, 434153 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:32:21,951 : INFO : EPOCH 7 - PROGRESS: at 6.12% examples, 439107 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:32:22,981 : INFO : EPOCH 7 - PROGRESS: at 6.87% examples, 440021 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:32:24,002 : INFO : EPOCH 7 - PROGRESS: at 7.24% examples, 443981 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:32:25,004 : INFO : EPOCH 7 - PROGRESS: at 7.79% examples, 443121 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:32:26,081 : INFO : EPOCH 7 - PROGRESS: at 8.53% examples, 441065 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:32:27,082 : INFO : EPOCH 7 - PROGRESS: at 9.19% examples, 437247 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:32:28,113 : INFO : EPOCH 7 - PROGRESS: at 9.97% examples, 436826 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:32:29,114 : INFO : EPOCH 7 - PROGRESS: at 10.75% examples, 435252 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:32:30,140 : INFO : EPOCH 7 - PROGRESS: at 11.48% examples, 435693 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:32:31,147 : INFO : EPOCH 7 - PROGRESS: at 12.20% examples, 435748 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:32:32,156 : INFO : EPOCH 7 - PROGRESS: at 13.02% examples, 436425 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:32:33,169 : INFO : EPOCH 7 - PROGRESS: at 13.81% examples, 435835 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:32:34,189 : INFO : EPOCH 7 - PROGRESS: at 14.46% examples, 432605 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:32:35,219 : INFO : EPOCH 7 - PROGRESS: at 15.07% examples, 433311 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:32:36,229 : INFO : EPOCH 7 - PROGRESS: at 15.69% examples, 433849 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:32:37,308 : INFO : EPOCH 7 - PROGRESS: at 16.27% examples, 431092 words/s, in_qsize 4, out_qsize 3
2021-09-30 11:32:38,356 : INFO : EPOCH 7 - PROGRESS: at 16.88% examples, 428443 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:32:39,400 : INFO : EPOCH 7 - PROGRESS: at 17.50% examples, 427670 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:32:40,431 : INFO : EPOCH 7 - PROGRESS: at 18.31% examples, 428704 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:32:41,447 : INFO : EPOCH 7 - PROGRESS: at 19.08% examples, 428864 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:32:42,452 : INFO : EPOCH 7 - PROGRESS: at 19.85% examples, 428836 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:32:43,452 : INFO : EPOCH 7 - PROGRESS: at 20.55% examples, 427815 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:32:44,468 : INFO : EPOCH 7 - PROGRESS: at 21.23% examples, 427881 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:32:45,474 : INFO : EPOCH 7 - PROGRESS: at 21.98% examples, 428476 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:32:46,504 : INFO : EPOCH 7 - PROGRESS: at 22.21% examples, 429165 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:32:47,522 : INFO : EPOCH 7 - PROGRESS: at 22.42% examples, 428875 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:32:48,533 : INFO : EPOCH 7 - PROGRESS: at 22.62% examples, 428724 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:32:49,535 : INFO : EPOCH 7 - PROGRESS: at 22.82% examples, 428231 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:32:50,557 : INFO : EPOCH 7 - PROGRESS: at 23.02% examples, 427510 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:32:51,558 : INFO : EPOCH 7 - PROGRESS: at 23.20% examples, 426333 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:32:52,597 : INFO : EPOCH 7 - PROGRESS: at 23.43% examples, 426372 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:32:53,599 : INFO : EPOCH 7 - PROGRESS: at 23.64% examples, 426090 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:32:54,612 : INFO : EPOCH 7 - PROGRESS: at 23.84% examples, 425286 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:32:55,621 : INFO : EPOCH 7 - PROGRESS: at 24.05% examples, 425142 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:32:56,649 : INFO : EPOCH 7 - PROGRESS: at 24.30% examples, 425606 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:32:57,703 : INFO : EPOCH 7 - PROGRESS: at 24.66% examples, 425080 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:32:58,724 : INFO : EPOCH 7 - PROGRESS: at 25.19% examples, 425261 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:32:59,755 : INFO : EPOCH 7 - PROGRESS: at 25.94% examples, 425530 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:33:00,775 : INFO : EPOCH 7 - PROGRESS: at 26.69% examples, 426497 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:33:01,807 : INFO : EPOCH 7 - PROGRESS: at 27.46% examples, 426491 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:33:02,810 : INFO : EPOCH 7 - PROGRESS: at 28.07% examples, 426751 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:33:03,845 : INFO : EPOCH 7 - PROGRESS: at 28.39% examples, 426946 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:33:04,854 : INFO : EPOCH 7 - PROGRESS: at 28.87% examples, 427660 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:33:05,867 : INFO : EPOCH 7 - PROGRESS: at 29.27% examples, 427811 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:33:06,886 : INFO : EPOCH 7 - PROGRESS: at 29.84% examples, 427740 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:33:07,904 : INFO : EPOCH 7 - PROGRESS: at 30.50% examples, 427927 words/s, in_qsize 1, out_qsize 6
2021-09-30 11:33:08,955 : INFO : EPOCH 7 - PROGRESS: at 31.19% examples, 428361 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:33:09,964 : INFO : EPOCH 7 - PROGRESS: at 32.03% examples, 429069 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:33:10,981 : INFO : EPOCH 7 - PROGRESS: at 32.89% examples, 429424 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:33:12,007 : INFO : EPOCH 7 - PROGRESS: at 33.72% examples, 429462 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:33:13,052 : INFO : EPOCH 7 - PROGRESS: at 34.61% examples, 429957 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:33:14,052 : INFO : EPOCH 7 - PROGRESS: at 35.49% examples, 430386 words/s, in_qsize 2, out_qsize 3
2021-09-30 11:33:15,088 : INFO : EPOCH 7 - PROGRESS: at 36.40% examples, 431105 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:33:16,112 : INFO : EPOCH 7 - PROGRESS: at 37.25% examples, 431332 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:33:17,113 : INFO : EPOCH 7 - PROGRESS: at 38.14% examples, 431816 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:33:18,117 : INFO : EPOCH 7 - PROGRESS: at 39.05% examples, 432471 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:33:19,198 : INFO : EPOCH 7 - PROGRESS: at 39.68% examples, 432214 words/s, in_qsize 3, out_qsize 3
2021-09-30 11:33:20,201 : INFO : EPOCH 7 - PROGRESS: at 40.28% examples, 432423 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:33:21,211 : INFO : EPOCH 7 - PROGRESS: at 40.97% examples, 432082 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:33:22,292 : INFO : EPOCH 7 - PROGRESS: at 41.61% examples, 431767 words/s, in_qsize 4, out_qsize 4
2021-09-30 11:33:23,300 : INFO : EPOCH 7 - PROGRESS: at 42.37% examples, 432049 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:33:24,310 : INFO : EPOCH 7 - PROGRESS: at 43.14% examples, 431811 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:33:25,319 : INFO : EPOCH 7 - PROGRESS: at 43.86% examples, 432087 words/s, in_qsize 1, out_qsize 3
2021-09-30 11:33:26,424 : INFO : EPOCH 7 - PROGRESS: at 44.60% examples, 431792 words/s, in_qsize 2, out_qsize 7
2021-09-30 11:33:27,430 : INFO : EPOCH 7 - PROGRESS: at 45.24% examples, 431989 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:33:28,457 : INFO : EPOCH 7 - PROGRESS: at 46.08% examples, 431971 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:33:29,497 : INFO : EPOCH 7 - PROGRESS: at 46.90% examples, 432268 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:33:30,505 : INFO : EPOCH 7 - PROGRESS: at 47.53% examples, 432441 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:33:31,550 : INFO : EPOCH 7 - PROGRESS: at 48.08% examples, 431681 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:33:32,575 : INFO : EPOCH 7 - PROGRESS: at 48.82% examples, 432099 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:33:33,599 : INFO : EPOCH 7 - PROGRESS: at 49.44% examples, 432127 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:33:34,604 : INFO : EPOCH 7 - PROGRESS: at 50.25% examples, 432530 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:33:35,641 : INFO : EPOCH 7 - PROGRESS: at 51.01% examples, 431863 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:33:36,677 : INFO : EPOCH 7 - PROGRESS: at 51.18% examples, 432290 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:33:37,681 : INFO : EPOCH 7 - PROGRESS: at 51.57% examples, 432474 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:33:38,682 : INFO : EPOCH 7 - PROGRESS: at 51.77% examples, 432224 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:33:39,753 : INFO : EPOCH 7 - PROGRESS: at 52.37% examples, 432042 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:33:40,761 : INFO : EPOCH 7 - PROGRESS: at 52.73% examples, 431214 words/s, in_qsize 2, out_qsize 5
2021-09-30 11:33:41,774 : INFO : EPOCH 7 - PROGRESS: at 53.09% examples, 431579 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:33:42,800 : INFO : EPOCH 7 - PROGRESS: at 53.45% examples, 431862 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:33:43,813 : INFO : EPOCH 7 - PROGRESS: at 53.84% examples, 431877 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:33:44,813 : INFO : EPOCH 7 - PROGRESS: at 54.22% examples, 431514 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:33:45,834 : INFO : EPOCH 7 - PROGRESS: at 54.58% examples, 431279 words/s, in_qsize 0, out_qsize 3
2021-09-30 11:33:46,835 : INFO : EPOCH 7 - PROGRESS: at 54.91% examples, 430805 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:33:47,863 : INFO : EPOCH 7 - PROGRESS: at 55.32% examples, 430770 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:33:48,900 : INFO : EPOCH 7 - PROGRESS: at 55.84% examples, 430940 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:33:49,914 : INFO : EPOCH 7 - PROGRESS: at 56.24% examples, 430734 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:33:50,915 : INFO : EPOCH 7 - PROGRESS: at 56.64% examples, 431095 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:33:51,995 : INFO : EPOCH 7 - PROGRESS: at 57.02% examples, 431192 words/s, in_qsize 1, out_qsize 3
2021-09-30 11:33:53,023 : INFO : EPOCH 7 - PROGRESS: at 57.54% examples, 431580 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:33:54,046 : INFO : EPOCH 7 - PROGRESS: at 58.00% examples, 431495 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:33:55,056 : INFO : EPOCH 7 - PROGRESS: at 58.45% examples, 431714 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:33:56,139 : INFO : EPOCH 7 - PROGRESS: at 59.02% examples, 431381 words/s, in_qsize 6, out_qsize 3
2021-09-30 11:33:57,152 : INFO : EPOCH 7 - PROGRESS: at 59.72% examples, 431370 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:33:58,156 : INFO : EPOCH 7 - PROGRESS: at 60.45% examples, 431481 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:33:59,247 : INFO : EPOCH 7 - PROGRESS: at 61.15% examples, 431441 words/s, in_qsize 2, out_qsize 7
2021-09-30 11:34:00,263 : INFO : EPOCH 7 - PROGRESS: at 61.93% examples, 431885 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:34:01,339 : INFO : EPOCH 7 - PROGRESS: at 62.74% examples, 431879 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:34:02,371 : INFO : EPOCH 7 - PROGRESS: at 63.58% examples, 432216 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:34:03,372 : INFO : EPOCH 7 - PROGRESS: at 64.32% examples, 432366 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:34:04,377 : INFO : EPOCH 7 - PROGRESS: at 65.07% examples, 432527 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:34:05,411 : INFO : EPOCH 7 - PROGRESS: at 65.67% examples, 432400 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:34:06,423 : INFO : EPOCH 7 - PROGRESS: at 66.32% examples, 432502 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:34:07,434 : INFO : EPOCH 7 - PROGRESS: at 66.69% examples, 432190 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:34:08,472 : INFO : EPOCH 7 - PROGRESS: at 67.10% examples, 432284 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:34:09,523 : INFO : EPOCH 7 - PROGRESS: at 67.75% examples, 432047 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:34:10,574 : INFO : EPOCH 7 - PROGRESS: at 68.48% examples, 431728 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:34:11,601 : INFO : EPOCH 7 - PROGRESS: at 69.31% examples, 432116 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:34:12,617 : INFO : EPOCH 7 - PROGRESS: at 70.10% examples, 432042 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:34:13,623 : INFO : EPOCH 7 - PROGRESS: at 71.01% examples, 432064 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:34:14,713 : INFO : EPOCH 7 - PROGRESS: at 71.79% examples, 431366 words/s, in_qsize 6, out_qsize 5
2021-09-30 11:34:15,743 : INFO : EPOCH 7 - PROGRESS: at 72.64% examples, 431349 words/s, in_qsize 3, out_qsize 5
2021-09-30 11:34:16,772 : INFO : EPOCH 7 - PROGRESS: at 73.37% examples, 431397 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:34:17,810 : INFO : EPOCH 7 - PROGRESS: at 74.05% examples, 431520 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:34:18,836 : INFO : EPOCH 7 - PROGRESS: at 74.77% examples, 431828 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:34:19,843 : INFO : EPOCH 7 - PROGRESS: at 75.31% examples, 431594 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:34:20,850 : INFO : EPOCH 7 - PROGRESS: at 75.89% examples, 431463 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:34:21,896 : INFO : EPOCH 7 - PROGRESS: at 76.72% examples, 431373 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:34:22,941 : INFO : EPOCH 7 - PROGRESS: at 77.46% examples, 431129 words/s, in_qsize 6, out_qsize 3
2021-09-30 11:34:23,956 : INFO : EPOCH 7 - PROGRESS: at 78.33% examples, 431471 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:34:24,957 : INFO : EPOCH 7 - PROGRESS: at 79.09% examples, 431674 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:34:25,978 : INFO : EPOCH 7 - PROGRESS: at 79.70% examples, 431375 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:34:26,978 : INFO : EPOCH 7 - PROGRESS: at 80.37% examples, 431482 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:34:27,984 : INFO : EPOCH 7 - PROGRESS: at 81.04% examples, 431200 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:34:28,990 : INFO : EPOCH 7 - PROGRESS: at 81.73% examples, 431023 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:34:30,042 : INFO : EPOCH 7 - PROGRESS: at 82.64% examples, 431164 words/s, in_qsize 0, out_qsize 3
2021-09-30 11:34:31,085 : INFO : EPOCH 7 - PROGRESS: at 83.20% examples, 431128 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:34:32,114 : INFO : EPOCH 7 - PROGRESS: at 83.85% examples, 431091 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:34:33,136 : INFO : EPOCH 7 - PROGRESS: at 84.68% examples, 431184 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:34:34,173 : INFO : EPOCH 7 - PROGRESS: at 85.57% examples, 431356 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:34:35,182 : INFO : EPOCH 7 - PROGRESS: at 86.14% examples, 431157 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:34:36,227 : INFO : EPOCH 7 - PROGRESS: at 86.71% examples, 431166 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:34:37,251 : INFO : EPOCH 7 - PROGRESS: at 87.51% examples, 431153 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:34:38,263 : INFO : EPOCH 7 - PROGRESS: at 88.17% examples, 431062 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:34:39,296 : INFO : EPOCH 7 - PROGRESS: at 88.82% examples, 431028 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:34:40,308 : INFO : EPOCH 7 - PROGRESS: at 89.68% examples, 431070 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:34:41,330 : INFO : EPOCH 7 - PROGRESS: at 90.48% examples, 430993 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:34:42,331 : INFO : EPOCH 7 - PROGRESS: at 91.00% examples, 431091 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:34:43,355 : INFO : EPOCH 7 - PROGRESS: at 91.54% examples, 431111 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:34:44,372 : INFO : EPOCH 7 - PROGRESS: at 92.02% examples, 431045 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:34:45,411 : INFO : EPOCH 7 - PROGRESS: at 92.53% examples, 430979 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:34:46,441 : INFO : EPOCH 7 - PROGRESS: at 93.09% examples, 431222 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:34:47,479 : INFO : EPOCH 7 - PROGRESS: at 93.57% examples, 431053 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:34:48,527 : INFO : EPOCH 7 - PROGRESS: at 94.09% examples, 431085 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:34:49,534 : INFO : EPOCH 7 - PROGRESS: at 94.61% examples, 431139 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:34:50,552 : INFO : EPOCH 7 - PROGRESS: at 95.13% examples, 431165 words/s, in_qsize 0, out_qsize 3
2021-09-30 11:34:51,561 : INFO : EPOCH 7 - PROGRESS: at 95.67% examples, 431391 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:34:52,568 : INFO : EPOCH 7 - PROGRESS: at 96.23% examples, 431569 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:34:53,601 : INFO : EPOCH 7 - PROGRESS: at 96.74% examples, 431451 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:34:54,657 : INFO : EPOCH 7 - PROGRESS: at 97.42% examples, 431649 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:34:55,296 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-30 11:34:55,300 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-30 11:34:55,303 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-30 11:34:55,303 : INFO : EPOCH - 7 : training on 96321721 raw words (70186372 effective words) took 162.5s, 431819 effective words/s
2021-09-30 11:34:56,328 : INFO : EPOCH 8 - PROGRESS: at 0.66% examples, 392271 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:34:57,376 : INFO : EPOCH 8 - PROGRESS: at 1.31% examples, 395220 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:34:58,385 : INFO : EPOCH 8 - PROGRESS: at 2.00% examples, 402219 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:34:59,402 : INFO : EPOCH 8 - PROGRESS: at 2.70% examples, 418850 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:35:00,421 : INFO : EPOCH 8 - PROGRESS: at 3.26% examples, 411062 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:35:01,423 : INFO : EPOCH 8 - PROGRESS: at 3.82% examples, 411561 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:35:02,475 : INFO : EPOCH 8 - PROGRESS: at 4.41% examples, 407959 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:35:03,476 : INFO : EPOCH 8 - PROGRESS: at 4.94% examples, 410188 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:35:04,495 : INFO : EPOCH 8 - PROGRESS: at 5.69% examples, 409069 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:35:05,515 : INFO : EPOCH 8 - PROGRESS: at 6.46% examples, 414957 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:35:06,552 : INFO : EPOCH 8 - PROGRESS: at 7.01% examples, 415488 words/s, in_qsize 5, out_qsize 3
2021-09-30 11:35:07,557 : INFO : EPOCH 8 - PROGRESS: at 7.40% examples, 422925 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:35:08,586 : INFO : EPOCH 8 - PROGRESS: at 8.10% examples, 422422 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:35:09,606 : INFO : EPOCH 8 - PROGRESS: at 8.91% examples, 425803 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:35:10,691 : INFO : EPOCH 8 - PROGRESS: at 9.64% examples, 423831 words/s, in_qsize 5, out_qsize 3
2021-09-30 11:35:11,730 : INFO : EPOCH 8 - PROGRESS: at 10.57% examples, 427381 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:35:12,736 : INFO : EPOCH 8 - PROGRESS: at 11.30% examples, 428836 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:35:13,773 : INFO : EPOCH 8 - PROGRESS: at 11.97% examples, 426138 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:35:14,777 : INFO : EPOCH 8 - PROGRESS: at 12.78% examples, 427026 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:35:15,786 : INFO : EPOCH 8 - PROGRESS: at 13.56% examples, 426992 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:35:16,790 : INFO : EPOCH 8 - PROGRESS: at 14.35% examples, 427604 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:35:17,804 : INFO : EPOCH 8 - PROGRESS: at 14.90% examples, 426647 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:35:18,865 : INFO : EPOCH 8 - PROGRESS: at 15.45% examples, 424398 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:35:19,866 : INFO : EPOCH 8 - PROGRESS: at 16.08% examples, 425507 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:35:20,866 : INFO : EPOCH 8 - PROGRESS: at 16.78% examples, 426548 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:35:21,885 : INFO : EPOCH 8 - PROGRESS: at 17.41% examples, 426108 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:35:22,900 : INFO : EPOCH 8 - PROGRESS: at 18.03% examples, 423986 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:35:23,956 : INFO : EPOCH 8 - PROGRESS: at 18.68% examples, 421233 words/s, in_qsize 6, out_qsize 6
2021-09-30 11:35:24,972 : INFO : EPOCH 8 - PROGRESS: at 19.46% examples, 421926 words/s, in_qsize 5, out_qsize 3
2021-09-30 11:35:26,022 : INFO : EPOCH 8 - PROGRESS: at 20.35% examples, 423591 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:35:27,117 : INFO : EPOCH 8 - PROGRESS: at 21.03% examples, 422254 words/s, in_qsize 3, out_qsize 5
2021-09-30 11:35:28,142 : INFO : EPOCH 8 - PROGRESS: at 21.73% examples, 422563 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:35:29,183 : INFO : EPOCH 8 - PROGRESS: at 22.14% examples, 423346 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:35:30,185 : INFO : EPOCH 8 - PROGRESS: at 22.34% examples, 423004 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:35:31,185 : INFO : EPOCH 8 - PROGRESS: at 22.53% examples, 421828 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:35:32,206 : INFO : EPOCH 8 - PROGRESS: at 22.74% examples, 421818 words/s, in_qsize 1, out_qsize 3
2021-09-30 11:35:33,208 : INFO : EPOCH 8 - PROGRESS: at 22.94% examples, 421684 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:35:34,215 : INFO : EPOCH 8 - PROGRESS: at 23.15% examples, 421839 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:35:35,234 : INFO : EPOCH 8 - PROGRESS: at 23.35% examples, 420985 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:35:36,295 : INFO : EPOCH 8 - PROGRESS: at 23.55% examples, 419939 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:35:37,335 : INFO : EPOCH 8 - PROGRESS: at 23.74% examples, 418974 words/s, in_qsize 5, out_qsize 4
2021-09-30 11:35:38,345 : INFO : EPOCH 8 - PROGRESS: at 23.98% examples, 419927 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:35:39,395 : INFO : EPOCH 8 - PROGRESS: at 24.19% examples, 418926 words/s, in_qsize 4, out_qsize 4
2021-09-30 11:35:40,441 : INFO : EPOCH 8 - PROGRESS: at 24.42% examples, 419205 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:35:41,446 : INFO : EPOCH 8 - PROGRESS: at 25.00% examples, 420248 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:35:42,463 : INFO : EPOCH 8 - PROGRESS: at 25.66% examples, 420301 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:35:43,473 : INFO : EPOCH 8 - PROGRESS: at 26.37% examples, 421118 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:35:44,506 : INFO : EPOCH 8 - PROGRESS: at 27.17% examples, 421562 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:35:45,558 : INFO : EPOCH 8 - PROGRESS: at 27.87% examples, 421074 words/s, in_qsize 1, out_qsize 3
2021-09-30 11:35:46,569 : INFO : EPOCH 8 - PROGRESS: at 28.24% examples, 420837 words/s, in_qsize 2, out_qsize 5
2021-09-30 11:35:47,629 : INFO : EPOCH 8 - PROGRESS: at 28.60% examples, 421062 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:35:48,665 : INFO : EPOCH 8 - PROGRESS: at 29.02% examples, 421044 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:35:49,667 : INFO : EPOCH 8 - PROGRESS: at 29.49% examples, 421117 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:35:50,690 : INFO : EPOCH 8 - PROGRESS: at 30.09% examples, 421227 words/s, in_qsize 1, out_qsize 5
2021-09-30 11:35:51,690 : INFO : EPOCH 8 - PROGRESS: at 30.84% examples, 422413 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:35:52,692 : INFO : EPOCH 8 - PROGRESS: at 31.48% examples, 422408 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:35:53,705 : INFO : EPOCH 8 - PROGRESS: at 32.31% examples, 422802 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:35:54,706 : INFO : EPOCH 8 - PROGRESS: at 33.20% examples, 423483 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:35:55,720 : INFO : EPOCH 8 - PROGRESS: at 33.98% examples, 423340 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:35:56,737 : INFO : EPOCH 8 - PROGRESS: at 34.72% examples, 422832 words/s, in_qsize 1, out_qsize 5
2021-09-30 11:35:57,767 : INFO : EPOCH 8 - PROGRESS: at 35.68% examples, 423853 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:35:58,775 : INFO : EPOCH 8 - PROGRESS: at 36.42% examples, 423482 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:35:59,781 : INFO : EPOCH 8 - PROGRESS: at 37.33% examples, 424401 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:36:00,791 : INFO : EPOCH 8 - PROGRESS: at 38.09% examples, 423932 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:36:01,805 : INFO : EPOCH 8 - PROGRESS: at 38.96% examples, 424207 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:36:02,820 : INFO : EPOCH 8 - PROGRESS: at 39.59% examples, 424165 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:36:03,831 : INFO : EPOCH 8 - PROGRESS: at 40.18% examples, 424463 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:36:04,854 : INFO : EPOCH 8 - PROGRESS: at 40.89% examples, 424447 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:36:05,860 : INFO : EPOCH 8 - PROGRESS: at 41.50% examples, 424613 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:36:06,879 : INFO : EPOCH 8 - PROGRESS: at 42.23% examples, 424509 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:36:07,891 : INFO : EPOCH 8 - PROGRESS: at 43.09% examples, 425056 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:36:08,913 : INFO : EPOCH 8 - PROGRESS: at 43.79% examples, 425250 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:36:09,962 : INFO : EPOCH 8 - PROGRESS: at 44.53% examples, 425279 words/s, in_qsize 1, out_qsize 5
2021-09-30 11:36:10,996 : INFO : EPOCH 8 - PROGRESS: at 45.22% examples, 425890 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:36:11,996 : INFO : EPOCH 8 - PROGRESS: at 46.04% examples, 426107 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:36:13,000 : INFO : EPOCH 8 - PROGRESS: at 46.86% examples, 426400 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:36:14,003 : INFO : EPOCH 8 - PROGRESS: at 47.45% examples, 426384 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:36:15,013 : INFO : EPOCH 8 - PROGRESS: at 48.09% examples, 426740 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:36:16,064 : INFO : EPOCH 8 - PROGRESS: at 48.83% examples, 427069 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:36:17,092 : INFO : EPOCH 8 - PROGRESS: at 49.48% examples, 427318 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:36:18,097 : INFO : EPOCH 8 - PROGRESS: at 50.25% examples, 427521 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:36:19,106 : INFO : EPOCH 8 - PROGRESS: at 51.09% examples, 428023 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:36:20,119 : INFO : EPOCH 8 - PROGRESS: at 51.18% examples, 427407 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:36:21,158 : INFO : EPOCH 8 - PROGRESS: at 51.56% examples, 427638 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:36:22,168 : INFO : EPOCH 8 - PROGRESS: at 51.77% examples, 427318 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:36:23,186 : INFO : EPOCH 8 - PROGRESS: at 52.38% examples, 427788 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:36:24,212 : INFO : EPOCH 8 - PROGRESS: at 52.77% examples, 427266 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:36:25,222 : INFO : EPOCH 8 - PROGRESS: at 53.11% examples, 427678 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:36:26,227 : INFO : EPOCH 8 - PROGRESS: at 53.47% examples, 427944 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:36:27,231 : INFO : EPOCH 8 - PROGRESS: at 53.87% examples, 427969 words/s, in_qsize 1, out_qsize 5
2021-09-30 11:36:28,232 : INFO : EPOCH 8 - PROGRESS: at 54.30% examples, 428268 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:36:29,246 : INFO : EPOCH 8 - PROGRESS: at 54.62% examples, 427796 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:36:30,294 : INFO : EPOCH 8 - PROGRESS: at 54.92% examples, 426697 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:36:31,316 : INFO : EPOCH 8 - PROGRESS: at 55.26% examples, 425981 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:36:32,392 : INFO : EPOCH 8 - PROGRESS: at 55.73% examples, 425735 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:36:33,394 : INFO : EPOCH 8 - PROGRESS: at 56.11% examples, 425129 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:36:34,418 : INFO : EPOCH 8 - PROGRESS: at 56.52% examples, 425446 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:36:35,430 : INFO : EPOCH 8 - PROGRESS: at 56.85% examples, 425233 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:36:36,433 : INFO : EPOCH 8 - PROGRESS: at 57.20% examples, 425286 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:36:37,456 : INFO : EPOCH 8 - PROGRESS: at 57.77% examples, 425194 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:36:38,458 : INFO : EPOCH 8 - PROGRESS: at 58.10% examples, 424637 words/s, in_qsize 3, out_qsize 4
2021-09-30 11:36:39,477 : INFO : EPOCH 8 - PROGRESS: at 58.50% examples, 424466 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:36:40,480 : INFO : EPOCH 8 - PROGRESS: at 59.11% examples, 424551 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:36:41,507 : INFO : EPOCH 8 - PROGRESS: at 59.92% examples, 425035 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:36:42,525 : INFO : EPOCH 8 - PROGRESS: at 60.53% examples, 424596 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:36:43,532 : INFO : EPOCH 8 - PROGRESS: at 61.17% examples, 424542 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:36:44,596 : INFO : EPOCH 8 - PROGRESS: at 61.89% examples, 424531 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:36:45,598 : INFO : EPOCH 8 - PROGRESS: at 62.47% examples, 423732 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:36:46,598 : INFO : EPOCH 8 - PROGRESS: at 63.10% examples, 423302 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:36:47,615 : INFO : EPOCH 8 - PROGRESS: at 63.86% examples, 423414 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:36:48,617 : INFO : EPOCH 8 - PROGRESS: at 64.52% examples, 423078 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:36:49,639 : INFO : EPOCH 8 - PROGRESS: at 65.26% examples, 423362 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:36:50,644 : INFO : EPOCH 8 - PROGRESS: at 65.88% examples, 423567 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:36:51,650 : INFO : EPOCH 8 - PROGRESS: at 66.43% examples, 423454 words/s, in_qsize 2, out_qsize 4
2021-09-30 11:36:52,651 : INFO : EPOCH 8 - PROGRESS: at 66.84% examples, 423772 words/s, in_qsize 0, out_qsize 0
2021-09-30 11:36:53,659 : INFO : EPOCH 8 - PROGRESS: at 67.20% examples, 423408 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:36:54,669 : INFO : EPOCH 8 - PROGRESS: at 67.73% examples, 422498 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:36:55,755 : INFO : EPOCH 8 - PROGRESS: at 68.44% examples, 422085 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:36:56,822 : INFO : EPOCH 8 - PROGRESS: at 69.19% examples, 421976 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:36:57,842 : INFO : EPOCH 8 - PROGRESS: at 70.10% examples, 422578 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:36:58,870 : INFO : EPOCH 8 - PROGRESS: at 70.89% examples, 422190 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:36:59,884 : INFO : EPOCH 8 - PROGRESS: at 71.77% examples, 422202 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:37:00,884 : INFO : EPOCH 8 - PROGRESS: at 72.66% examples, 422532 words/s, in_qsize 0, out_qsize 0
2021-09-30 11:37:01,906 : INFO : EPOCH 8 - PROGRESS: at 73.36% examples, 422503 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:37:02,916 : INFO : EPOCH 8 - PROGRESS: at 73.99% examples, 422562 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:37:03,945 : INFO : EPOCH 8 - PROGRESS: at 74.68% examples, 422585 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:37:04,953 : INFO : EPOCH 8 - PROGRESS: at 75.27% examples, 422872 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:37:05,957 : INFO : EPOCH 8 - PROGRESS: at 75.85% examples, 422759 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:37:06,970 : INFO : EPOCH 8 - PROGRESS: at 76.62% examples, 422684 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:37:07,976 : INFO : EPOCH 8 - PROGRESS: at 77.39% examples, 422639 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:37:09,005 : INFO : EPOCH 8 - PROGRESS: at 78.15% examples, 422724 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:37:10,021 : INFO : EPOCH 8 - PROGRESS: at 78.93% examples, 422819 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:37:11,033 : INFO : EPOCH 8 - PROGRESS: at 79.51% examples, 422522 words/s, in_qsize 1, out_qsize 5
2021-09-30 11:37:12,035 : INFO : EPOCH 8 - PROGRESS: at 80.23% examples, 422762 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:37:13,043 : INFO : EPOCH 8 - PROGRESS: at 80.85% examples, 422518 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:37:14,045 : INFO : EPOCH 8 - PROGRESS: at 81.58% examples, 422580 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:37:15,053 : INFO : EPOCH 8 - PROGRESS: at 82.50% examples, 422914 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:37:16,057 : INFO : EPOCH 8 - PROGRESS: at 83.06% examples, 422687 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:37:17,099 : INFO : EPOCH 8 - PROGRESS: at 83.50% examples, 422364 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:37:18,121 : INFO : EPOCH 8 - PROGRESS: at 84.30% examples, 422383 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:37:19,140 : INFO : EPOCH 8 - PROGRESS: at 85.01% examples, 422199 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:37:20,187 : INFO : EPOCH 8 - PROGRESS: at 85.72% examples, 421760 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:37:21,220 : INFO : EPOCH 8 - PROGRESS: at 86.26% examples, 421421 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:37:22,223 : INFO : EPOCH 8 - PROGRESS: at 86.82% examples, 421415 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:37:23,227 : INFO : EPOCH 8 - PROGRESS: at 87.54% examples, 421282 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:37:24,252 : INFO : EPOCH 8 - PROGRESS: at 88.12% examples, 420890 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:37:25,275 : INFO : EPOCH 8 - PROGRESS: at 88.80% examples, 421049 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:37:26,279 : INFO : EPOCH 8 - PROGRESS: at 89.60% examples, 420991 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:37:27,335 : INFO : EPOCH 8 - PROGRESS: at 90.45% examples, 421030 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:37:28,362 : INFO : EPOCH 8 - PROGRESS: at 90.97% examples, 421070 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:37:29,371 : INFO : EPOCH 8 - PROGRESS: at 91.51% examples, 421243 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:37:30,409 : INFO : EPOCH 8 - PROGRESS: at 92.04% examples, 421422 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:37:31,440 : INFO : EPOCH 8 - PROGRESS: at 92.59% examples, 421676 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:37:32,498 : INFO : EPOCH 8 - PROGRESS: at 93.13% examples, 421803 words/s, in_qsize 0, out_qsize 4
2021-09-30 11:37:33,508 : INFO : EPOCH 8 - PROGRESS: at 93.64% examples, 421921 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:37:34,510 : INFO : EPOCH 8 - PROGRESS: at 94.14% examples, 422049 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:37:35,539 : INFO : EPOCH 8 - PROGRESS: at 94.69% examples, 422274 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:37:36,540 : INFO : EPOCH 8 - PROGRESS: at 95.20% examples, 422350 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:37:37,565 : INFO : EPOCH 8 - PROGRESS: at 95.67% examples, 422181 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:37:38,586 : INFO : EPOCH 8 - PROGRESS: at 96.25% examples, 422464 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:37:39,611 : INFO : EPOCH 8 - PROGRESS: at 96.78% examples, 422559 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:37:40,623 : INFO : EPOCH 8 - PROGRESS: at 97.44% examples, 422790 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:37:41,194 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-30 11:37:41,200 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-30 11:37:41,201 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-30 11:37:41,201 : INFO : EPOCH - 8 : training on 96321721 raw words (70187624 effective words) took 165.9s, 423080 effective words/s
2021-09-30 11:37:42,207 : INFO : EPOCH 9 - PROGRESS: at 0.64% examples, 384935 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:37:43,252 : INFO : EPOCH 9 - PROGRESS: at 1.35% examples, 409923 words/s, in_qsize 1, out_qsize 4
2021-09-30 11:37:44,257 : INFO : EPOCH 9 - PROGRESS: at 2.11% examples, 431945 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:37:45,263 : INFO : EPOCH 9 - PROGRESS: at 2.77% examples, 435173 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:37:46,305 : INFO : EPOCH 9 - PROGRESS: at 3.41% examples, 433731 words/s, in_qsize 0, out_qsize 3
2021-09-30 11:37:47,345 : INFO : EPOCH 9 - PROGRESS: at 4.06% examples, 436130 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:37:48,379 : INFO : EPOCH 9 - PROGRESS: at 4.67% examples, 436979 words/s, in_qsize 0, out_qsize 3
2021-09-30 11:37:49,425 : INFO : EPOCH 9 - PROGRESS: at 5.39% examples, 438312 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:37:50,429 : INFO : EPOCH 9 - PROGRESS: at 6.00% examples, 430138 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:37:51,429 : INFO : EPOCH 9 - PROGRESS: at 6.68% examples, 426547 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:37:52,485 : INFO : EPOCH 9 - PROGRESS: at 7.12% examples, 426882 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:37:53,494 : INFO : EPOCH 9 - PROGRESS: at 7.56% examples, 429971 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:37:54,516 : INFO : EPOCH 9 - PROGRESS: at 8.33% examples, 432338 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:37:55,551 : INFO : EPOCH 9 - PROGRESS: at 9.10% examples, 432035 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:37:56,567 : INFO : EPOCH 9 - PROGRESS: at 9.82% examples, 430598 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:37:57,570 : INFO : EPOCH 9 - PROGRESS: at 10.64% examples, 431142 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:37:58,579 : INFO : EPOCH 9 - PROGRESS: at 11.38% examples, 432674 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:37:59,583 : INFO : EPOCH 9 - PROGRESS: at 12.06% examples, 431330 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:38:00,663 : INFO : EPOCH 9 - PROGRESS: at 12.81% examples, 428054 words/s, in_qsize 5, out_qsize 4
2021-09-30 11:38:01,697 : INFO : EPOCH 9 - PROGRESS: at 13.56% examples, 426741 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:38:02,719 : INFO : EPOCH 9 - PROGRESS: at 14.28% examples, 424639 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:38:03,760 : INFO : EPOCH 9 - PROGRESS: at 14.74% examples, 419776 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:38:04,766 : INFO : EPOCH 9 - PROGRESS: at 15.28% examples, 419452 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:38:05,792 : INFO : EPOCH 9 - PROGRESS: at 15.92% examples, 420339 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:38:06,805 : INFO : EPOCH 9 - PROGRESS: at 16.36% examples, 415731 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:38:07,813 : INFO : EPOCH 9 - PROGRESS: at 17.01% examples, 415652 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:38:08,815 : INFO : EPOCH 9 - PROGRESS: at 17.76% examples, 417959 words/s, in_qsize 0, out_qsize 0
2021-09-30 11:38:09,853 : INFO : EPOCH 9 - PROGRESS: at 18.51% examples, 417702 words/s, in_qsize 1, out_qsize 5
2021-09-30 11:38:10,890 : INFO : EPOCH 9 - PROGRESS: at 19.33% examples, 418928 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:38:11,930 : INFO : EPOCH 9 - PROGRESS: at 20.04% examples, 417888 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:38:12,957 : INFO : EPOCH 9 - PROGRESS: at 20.85% examples, 419359 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:38:13,959 : INFO : EPOCH 9 - PROGRESS: at 21.47% examples, 418321 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:38:14,964 : INFO : EPOCH 9 - PROGRESS: at 22.03% examples, 417709 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:38:15,966 : INFO : EPOCH 9 - PROGRESS: at 22.22% examples, 417059 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:38:16,991 : INFO : EPOCH 9 - PROGRESS: at 22.41% examples, 416066 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:38:18,000 : INFO : EPOCH 9 - PROGRESS: at 22.62% examples, 416302 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:38:19,054 : INFO : EPOCH 9 - PROGRESS: at 22.81% examples, 415391 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:38:20,068 : INFO : EPOCH 9 - PROGRESS: at 23.01% examples, 415465 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:38:21,085 : INFO : EPOCH 9 - PROGRESS: at 23.23% examples, 415649 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:38:22,136 : INFO : EPOCH 9 - PROGRESS: at 23.45% examples, 415688 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:38:23,176 : INFO : EPOCH 9 - PROGRESS: at 23.64% examples, 414647 words/s, in_qsize 3, out_qsize 5
2021-09-30 11:38:24,221 : INFO : EPOCH 9 - PROGRESS: at 23.88% examples, 415712 words/s, in_qsize 2, out_qsize 3
2021-09-30 11:38:25,255 : INFO : EPOCH 9 - PROGRESS: at 24.11% examples, 415752 words/s, in_qsize 3, out_qsize 3
2021-09-30 11:38:26,287 : INFO : EPOCH 9 - PROGRESS: at 24.33% examples, 416085 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:38:27,308 : INFO : EPOCH 9 - PROGRESS: at 24.77% examples, 416030 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:38:28,332 : INFO : EPOCH 9 - PROGRESS: at 25.29% examples, 415934 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:38:29,348 : INFO : EPOCH 9 - PROGRESS: at 26.07% examples, 417138 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:38:30,396 : INFO : EPOCH 9 - PROGRESS: at 26.76% examples, 417121 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:38:31,408 : INFO : EPOCH 9 - PROGRESS: at 27.53% examples, 417464 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:38:32,436 : INFO : EPOCH 9 - PROGRESS: at 28.15% examples, 418359 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:38:33,497 : INFO : EPOCH 9 - PROGRESS: at 28.42% examples, 417815 words/s, in_qsize 5, out_qsize 3
2021-09-30 11:38:34,548 : INFO : EPOCH 9 - PROGRESS: at 28.90% examples, 418705 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:38:35,565 : INFO : EPOCH 9 - PROGRESS: at 29.35% examples, 419292 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:38:36,637 : INFO : EPOCH 9 - PROGRESS: at 29.97% examples, 419319 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:38:37,639 : INFO : EPOCH 9 - PROGRESS: at 30.59% examples, 418991 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:38:38,646 : INFO : EPOCH 9 - PROGRESS: at 31.11% examples, 417972 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:38:39,658 : INFO : EPOCH 9 - PROGRESS: at 31.85% examples, 418072 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:38:40,708 : INFO : EPOCH 9 - PROGRESS: at 32.69% examples, 418402 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:38:41,751 : INFO : EPOCH 9 - PROGRESS: at 33.56% examples, 418745 words/s, in_qsize 0, out_qsize 0
2021-09-30 11:38:42,758 : INFO : EPOCH 9 - PROGRESS: at 34.25% examples, 417882 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:38:43,877 : INFO : EPOCH 9 - PROGRESS: at 35.09% examples, 417598 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:38:44,879 : INFO : EPOCH 9 - PROGRESS: at 35.86% examples, 417276 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:38:45,910 : INFO : EPOCH 9 - PROGRESS: at 36.57% examples, 416645 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:38:46,971 : INFO : EPOCH 9 - PROGRESS: at 37.44% examples, 416973 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:38:47,983 : INFO : EPOCH 9 - PROGRESS: at 38.27% examples, 417155 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:38:49,043 : INFO : EPOCH 9 - PROGRESS: at 39.08% examples, 416807 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:38:50,078 : INFO : EPOCH 9 - PROGRESS: at 39.66% examples, 416668 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:38:51,079 : INFO : EPOCH 9 - PROGRESS: at 40.23% examples, 416704 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:38:52,129 : INFO : EPOCH 9 - PROGRESS: at 40.92% examples, 416545 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:38:53,149 : INFO : EPOCH 9 - PROGRESS: at 41.51% examples, 416530 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:38:54,176 : INFO : EPOCH 9 - PROGRESS: at 42.17% examples, 415813 words/s, in_qsize 5, out_qsize 3
2021-09-30 11:38:55,193 : INFO : EPOCH 9 - PROGRESS: at 42.92% examples, 415936 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:38:56,195 : INFO : EPOCH 9 - PROGRESS: at 43.64% examples, 416054 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:38:57,251 : INFO : EPOCH 9 - PROGRESS: at 44.28% examples, 415586 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:38:58,252 : INFO : EPOCH 9 - PROGRESS: at 44.92% examples, 415836 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:38:59,277 : INFO : EPOCH 9 - PROGRESS: at 45.54% examples, 415279 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:39:00,344 : INFO : EPOCH 9 - PROGRESS: at 46.32% examples, 414785 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:39:01,352 : INFO : EPOCH 9 - PROGRESS: at 47.02% examples, 414983 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:39:02,356 : INFO : EPOCH 9 - PROGRESS: at 47.57% examples, 414613 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:39:03,359 : INFO : EPOCH 9 - PROGRESS: at 48.20% examples, 414960 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:39:04,375 : INFO : EPOCH 9 - PROGRESS: at 48.87% examples, 414967 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:39:05,386 : INFO : EPOCH 9 - PROGRESS: at 49.50% examples, 415265 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:39:06,456 : INFO : EPOCH 9 - PROGRESS: at 50.18% examples, 414762 words/s, in_qsize 2, out_qsize 6
2021-09-30 11:39:07,476 : INFO : EPOCH 9 - PROGRESS: at 51.06% examples, 415279 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:39:08,550 : INFO : EPOCH 9 - PROGRESS: at 51.18% examples, 415196 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:39:09,573 : INFO : EPOCH 9 - PROGRESS: at 51.56% examples, 415477 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:39:10,593 : INFO : EPOCH 9 - PROGRESS: at 51.76% examples, 415101 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:39:11,598 : INFO : EPOCH 9 - PROGRESS: at 52.24% examples, 414545 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:39:12,607 : INFO : EPOCH 9 - PROGRESS: at 52.67% examples, 414333 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:39:13,618 : INFO : EPOCH 9 - PROGRESS: at 52.98% examples, 414159 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:39:14,646 : INFO : EPOCH 9 - PROGRESS: at 53.31% examples, 414255 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:39:15,650 : INFO : EPOCH 9 - PROGRESS: at 53.63% examples, 413821 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:39:16,706 : INFO : EPOCH 9 - PROGRESS: at 54.01% examples, 413478 words/s, in_qsize 0, out_qsize 4
2021-09-30 11:39:17,728 : INFO : EPOCH 9 - PROGRESS: at 54.41% examples, 413659 words/s, in_qsize 0, out_qsize 0
2021-09-30 11:39:18,806 : INFO : EPOCH 9 - PROGRESS: at 54.75% examples, 413294 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:39:19,830 : INFO : EPOCH 9 - PROGRESS: at 55.15% examples, 413529 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:39:20,831 : INFO : EPOCH 9 - PROGRESS: at 55.55% examples, 413285 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:39:21,838 : INFO : EPOCH 9 - PROGRESS: at 56.01% examples, 413310 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:39:22,862 : INFO : EPOCH 9 - PROGRESS: at 56.38% examples, 413101 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:39:23,867 : INFO : EPOCH 9 - PROGRESS: at 56.71% examples, 412900 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:39:24,951 : INFO : EPOCH 9 - PROGRESS: at 57.05% examples, 412750 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:39:25,990 : INFO : EPOCH 9 - PROGRESS: at 57.51% examples, 412786 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:39:27,018 : INFO : EPOCH 9 - PROGRESS: at 58.02% examples, 413139 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:39:28,040 : INFO : EPOCH 9 - PROGRESS: at 58.45% examples, 413406 words/s, in_qsize 0, out_qsize 5
2021-09-30 11:39:29,045 : INFO : EPOCH 9 - PROGRESS: at 59.07% examples, 413852 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:39:30,047 : INFO : EPOCH 9 - PROGRESS: at 59.83% examples, 414249 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:39:31,064 : INFO : EPOCH 9 - PROGRESS: at 60.54% examples, 414461 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:39:32,089 : INFO : EPOCH 9 - PROGRESS: at 61.24% examples, 414770 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:39:33,134 : INFO : EPOCH 9 - PROGRESS: at 61.95% examples, 414909 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:39:34,181 : INFO : EPOCH 9 - PROGRESS: at 62.71% examples, 414844 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:39:35,196 : INFO : EPOCH 9 - PROGRESS: at 63.44% examples, 414815 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:39:36,219 : INFO : EPOCH 9 - PROGRESS: at 64.11% examples, 414787 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:39:37,221 : INFO : EPOCH 9 - PROGRESS: at 64.82% examples, 414907 words/s, in_qsize 1, out_qsize 3
2021-09-30 11:39:38,252 : INFO : EPOCH 9 - PROGRESS: at 65.48% examples, 414907 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:39:39,295 : INFO : EPOCH 9 - PROGRESS: at 66.05% examples, 414612 words/s, in_qsize 6, out_qsize 3
2021-09-30 11:39:40,296 : INFO : EPOCH 9 - PROGRESS: at 66.54% examples, 414721 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:39:41,325 : INFO : EPOCH 9 - PROGRESS: at 66.90% examples, 414531 words/s, in_qsize 3, out_qsize 5
2021-09-30 11:39:42,339 : INFO : EPOCH 9 - PROGRESS: at 67.33% examples, 414518 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:39:43,391 : INFO : EPOCH 9 - PROGRESS: at 67.97% examples, 413916 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:39:44,393 : INFO : EPOCH 9 - PROGRESS: at 68.73% examples, 414105 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:39:45,438 : INFO : EPOCH 9 - PROGRESS: at 69.56% examples, 414398 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:39:46,450 : INFO : EPOCH 9 - PROGRESS: at 70.33% examples, 414430 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:39:47,495 : INFO : EPOCH 9 - PROGRESS: at 71.17% examples, 414227 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:39:48,535 : INFO : EPOCH 9 - PROGRESS: at 72.05% examples, 414222 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:39:49,542 : INFO : EPOCH 9 - PROGRESS: at 72.91% examples, 414697 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:39:50,634 : INFO : EPOCH 9 - PROGRESS: at 73.55% examples, 414382 words/s, in_qsize 5, out_qsize 6
2021-09-30 11:39:51,674 : INFO : EPOCH 9 - PROGRESS: at 74.33% examples, 414982 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:39:52,675 : INFO : EPOCH 9 - PROGRESS: at 74.92% examples, 414986 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:39:53,676 : INFO : EPOCH 9 - PROGRESS: at 75.48% examples, 415159 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:39:54,698 : INFO : EPOCH 9 - PROGRESS: at 76.14% examples, 415047 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:39:55,722 : INFO : EPOCH 9 - PROGRESS: at 76.98% examples, 415067 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:39:56,763 : INFO : EPOCH 9 - PROGRESS: at 77.77% examples, 415256 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:39:57,831 : INFO : EPOCH 9 - PROGRESS: at 78.58% examples, 415313 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:39:58,837 : INFO : EPOCH 9 - PROGRESS: at 79.22% examples, 415350 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:39:59,861 : INFO : EPOCH 9 - PROGRESS: at 79.88% examples, 415329 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:40:00,891 : INFO : EPOCH 9 - PROGRESS: at 80.55% examples, 415412 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:40:01,920 : INFO : EPOCH 9 - PROGRESS: at 81.38% examples, 415757 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:40:02,959 : INFO : EPOCH 9 - PROGRESS: at 82.16% examples, 415826 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:40:03,960 : INFO : EPOCH 9 - PROGRESS: at 82.92% examples, 415935 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:40:04,989 : INFO : EPOCH 9 - PROGRESS: at 83.43% examples, 416264 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:40:05,994 : INFO : EPOCH 9 - PROGRESS: at 84.15% examples, 416120 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:40:07,008 : INFO : EPOCH 9 - PROGRESS: at 85.01% examples, 416504 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:40:08,061 : INFO : EPOCH 9 - PROGRESS: at 85.77% examples, 416340 words/s, in_qsize 4, out_qsize 4
2021-09-30 11:40:09,068 : INFO : EPOCH 9 - PROGRESS: at 86.38% examples, 416461 words/s, in_qsize 4, out_qsize 4
2021-09-30 11:40:10,078 : INFO : EPOCH 9 - PROGRESS: at 87.06% examples, 416655 words/s, in_qsize 3, out_qsize 3
2021-09-30 11:40:11,130 : INFO : EPOCH 9 - PROGRESS: at 87.81% examples, 416842 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:40:12,180 : INFO : EPOCH 9 - PROGRESS: at 88.58% examples, 417013 words/s, in_qsize 3, out_qsize 3
2021-09-30 11:40:13,226 : INFO : EPOCH 9 - PROGRESS: at 89.32% examples, 417239 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:40:14,253 : INFO : EPOCH 9 - PROGRESS: at 90.21% examples, 417460 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:40:15,266 : INFO : EPOCH 9 - PROGRESS: at 90.82% examples, 417515 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:40:16,303 : INFO : EPOCH 9 - PROGRESS: at 91.36% examples, 417593 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:40:17,304 : INFO : EPOCH 9 - PROGRESS: at 91.86% examples, 417711 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:40:18,379 : INFO : EPOCH 9 - PROGRESS: at 92.39% examples, 417863 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:40:19,380 : INFO : EPOCH 9 - PROGRESS: at 92.90% examples, 418029 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:40:20,397 : INFO : EPOCH 9 - PROGRESS: at 93.42% examples, 418102 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:40:21,466 : INFO : EPOCH 9 - PROGRESS: at 93.92% examples, 418029 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:40:22,506 : INFO : EPOCH 9 - PROGRESS: at 94.42% examples, 418039 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:40:23,513 : INFO : EPOCH 9 - PROGRESS: at 94.94% examples, 418211 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:40:24,532 : INFO : EPOCH 9 - PROGRESS: at 95.44% examples, 418315 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:40:25,552 : INFO : EPOCH 9 - PROGRESS: at 96.00% examples, 418446 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:40:26,554 : INFO : EPOCH 9 - PROGRESS: at 96.51% examples, 418488 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:40:27,579 : INFO : EPOCH 9 - PROGRESS: at 97.06% examples, 418795 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:40:28,639 : INFO : EPOCH 9 - PROGRESS: at 98.63% examples, 418703 words/s, in_qsize 4, out_qsize 3
2021-09-30 11:40:28,691 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-30 11:40:28,697 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-30 11:40:28,697 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-30 11:40:28,697 : INFO : EPOCH - 9 : training on 96321721 raw words (70188294 effective words) took 167.5s, 419047 effective words/s
2021-09-30 11:40:29,701 : INFO : EPOCH 10 - PROGRESS: at 0.63% examples, 378399 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:40:30,705 : INFO : EPOCH 10 - PROGRESS: at 1.37% examples, 422309 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:40:31,721 : INFO : EPOCH 10 - PROGRESS: at 2.06% examples, 424401 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:40:32,739 : INFO : EPOCH 10 - PROGRESS: at 2.73% examples, 430089 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:40:33,789 : INFO : EPOCH 10 - PROGRESS: at 3.39% examples, 431703 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:40:34,790 : INFO : EPOCH 10 - PROGRESS: at 3.99% examples, 432400 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:40:35,816 : INFO : EPOCH 10 - PROGRESS: at 4.55% examples, 426226 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:40:36,816 : INFO : EPOCH 10 - PROGRESS: at 5.21% examples, 431030 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:40:37,846 : INFO : EPOCH 10 - PROGRESS: at 5.92% examples, 428927 words/s, in_qsize 1, out_qsize 5
2021-09-30 11:40:38,866 : INFO : EPOCH 10 - PROGRESS: at 6.76% examples, 433916 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:40:39,884 : INFO : EPOCH 10 - PROGRESS: at 7.16% examples, 435831 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:40:40,899 : INFO : EPOCH 10 - PROGRESS: at 7.64% examples, 436636 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:40:41,952 : INFO : EPOCH 10 - PROGRESS: at 8.36% examples, 435821 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:40:42,974 : INFO : EPOCH 10 - PROGRESS: at 9.10% examples, 434164 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:40:43,991 : INFO : EPOCH 10 - PROGRESS: at 9.89% examples, 434894 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:40:45,006 : INFO : EPOCH 10 - PROGRESS: at 10.71% examples, 434886 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:40:46,006 : INFO : EPOCH 10 - PROGRESS: at 11.37% examples, 433910 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:40:47,022 : INFO : EPOCH 10 - PROGRESS: at 12.07% examples, 432973 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:40:48,081 : INFO : EPOCH 10 - PROGRESS: at 12.88% examples, 431953 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:40:49,090 : INFO : EPOCH 10 - PROGRESS: at 13.65% examples, 431328 words/s, in_qsize 3, out_qsize 5
2021-09-30 11:40:50,124 : INFO : EPOCH 10 - PROGRESS: at 14.44% examples, 431795 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:40:51,138 : INFO : EPOCH 10 - PROGRESS: at 14.95% examples, 429318 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:40:52,144 : INFO : EPOCH 10 - PROGRESS: at 15.52% examples, 428556 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:40:53,179 : INFO : EPOCH 10 - PROGRESS: at 16.13% examples, 428628 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:40:54,203 : INFO : EPOCH 10 - PROGRESS: at 16.83% examples, 428640 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:40:55,208 : INFO : EPOCH 10 - PROGRESS: at 17.46% examples, 428290 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:40:56,209 : INFO : EPOCH 10 - PROGRESS: at 18.18% examples, 428433 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:40:57,236 : INFO : EPOCH 10 - PROGRESS: at 18.97% examples, 428692 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:40:58,257 : INFO : EPOCH 10 - PROGRESS: at 19.79% examples, 429619 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:40:59,260 : INFO : EPOCH 10 - PROGRESS: at 20.57% examples, 430006 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:41:00,277 : INFO : EPOCH 10 - PROGRESS: at 21.23% examples, 429512 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:41:01,300 : INFO : EPOCH 10 - PROGRESS: at 21.98% examples, 429843 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:41:02,329 : INFO : EPOCH 10 - PROGRESS: at 22.20% examples, 430086 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:41:03,335 : INFO : EPOCH 10 - PROGRESS: at 22.40% examples, 429101 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:41:04,338 : INFO : EPOCH 10 - PROGRESS: at 22.59% examples, 428489 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:41:05,367 : INFO : EPOCH 10 - PROGRESS: at 22.81% examples, 428573 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:41:06,401 : INFO : EPOCH 10 - PROGRESS: at 23.02% examples, 428785 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:41:07,416 : INFO : EPOCH 10 - PROGRESS: at 23.22% examples, 427763 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:41:08,417 : INFO : EPOCH 10 - PROGRESS: at 23.44% examples, 428011 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:41:09,447 : INFO : EPOCH 10 - PROGRESS: at 23.66% examples, 427901 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:41:10,456 : INFO : EPOCH 10 - PROGRESS: at 23.87% examples, 427407 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:41:11,488 : INFO : EPOCH 10 - PROGRESS: at 24.11% examples, 427961 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:41:12,530 : INFO : EPOCH 10 - PROGRESS: at 24.33% examples, 427606 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:41:13,577 : INFO : EPOCH 10 - PROGRESS: at 24.79% examples, 427681 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:41:14,590 : INFO : EPOCH 10 - PROGRESS: at 25.40% examples, 428538 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:41:15,599 : INFO : EPOCH 10 - PROGRESS: at 26.10% examples, 428613 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:41:16,604 : INFO : EPOCH 10 - PROGRESS: at 26.72% examples, 427818 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:41:17,660 : INFO : EPOCH 10 - PROGRESS: at 27.56% examples, 428321 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:41:18,714 : INFO : EPOCH 10 - PROGRESS: at 28.16% examples, 428642 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:41:19,731 : INFO : EPOCH 10 - PROGRESS: at 28.46% examples, 429201 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:41:20,741 : INFO : EPOCH 10 - PROGRESS: at 28.94% examples, 429943 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:41:21,743 : INFO : EPOCH 10 - PROGRESS: at 29.37% examples, 429924 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:41:22,764 : INFO : EPOCH 10 - PROGRESS: at 29.96% examples, 429739 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:41:23,773 : INFO : EPOCH 10 - PROGRESS: at 30.66% examples, 430221 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:41:24,784 : INFO : EPOCH 10 - PROGRESS: at 31.32% examples, 430651 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:41:25,795 : INFO : EPOCH 10 - PROGRESS: at 32.12% examples, 430671 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:41:26,813 : INFO : EPOCH 10 - PROGRESS: at 33.04% examples, 431477 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:41:27,864 : INFO : EPOCH 10 - PROGRESS: at 33.87% examples, 431300 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:41:28,874 : INFO : EPOCH 10 - PROGRESS: at 34.71% examples, 431526 words/s, in_qsize 3, out_qsize 1
2021-09-30 11:41:29,891 : INFO : EPOCH 10 - PROGRESS: at 35.60% examples, 431939 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:41:30,902 : INFO : EPOCH 10 - PROGRESS: at 36.44% examples, 432334 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:41:31,916 : INFO : EPOCH 10 - PROGRESS: at 37.32% examples, 432727 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:41:32,937 : INFO : EPOCH 10 - PROGRESS: at 38.11% examples, 432269 words/s, in_qsize 3, out_qsize 3
2021-09-30 11:41:33,943 : INFO : EPOCH 10 - PROGRESS: at 39.01% examples, 432801 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:41:34,952 : INFO : EPOCH 10 - PROGRESS: at 39.62% examples, 432569 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:41:35,973 : INFO : EPOCH 10 - PROGRESS: at 40.19% examples, 432461 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:41:37,016 : INFO : EPOCH 10 - PROGRESS: at 40.88% examples, 431993 words/s, in_qsize 2, out_qsize 3
2021-09-30 11:41:38,036 : INFO : EPOCH 10 - PROGRESS: at 41.50% examples, 432067 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:41:39,037 : INFO : EPOCH 10 - PROGRESS: at 42.22% examples, 431859 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:41:40,061 : INFO : EPOCH 10 - PROGRESS: at 43.03% examples, 431930 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:41:41,062 : INFO : EPOCH 10 - PROGRESS: at 43.69% examples, 431729 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:41:42,085 : INFO : EPOCH 10 - PROGRESS: at 44.42% examples, 431725 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:41:43,122 : INFO : EPOCH 10 - PROGRESS: at 45.02% examples, 431446 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:41:44,130 : INFO : EPOCH 10 - PROGRESS: at 45.76% examples, 431425 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:41:45,149 : INFO : EPOCH 10 - PROGRESS: at 46.67% examples, 431628 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:41:46,170 : INFO : EPOCH 10 - PROGRESS: at 47.20% examples, 431138 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:41:47,223 : INFO : EPOCH 10 - PROGRESS: at 47.84% examples, 430905 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:41:48,237 : INFO : EPOCH 10 - PROGRESS: at 48.50% examples, 430982 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:41:49,252 : INFO : EPOCH 10 - PROGRESS: at 49.15% examples, 430978 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:41:50,290 : INFO : EPOCH 10 - PROGRESS: at 49.86% examples, 431092 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:41:51,335 : INFO : EPOCH 10 - PROGRESS: at 50.59% examples, 430554 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:41:52,373 : INFO : EPOCH 10 - PROGRESS: at 51.16% examples, 430907 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:41:53,425 : INFO : EPOCH 10 - PROGRESS: at 51.20% examples, 430532 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:41:54,434 : INFO : EPOCH 10 - PROGRESS: at 51.68% examples, 430847 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:41:55,474 : INFO : EPOCH 10 - PROGRESS: at 52.13% examples, 430973 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:41:56,483 : INFO : EPOCH 10 - PROGRESS: at 52.58% examples, 430316 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:41:57,500 : INFO : EPOCH 10 - PROGRESS: at 52.97% examples, 430898 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:41:58,529 : INFO : EPOCH 10 - PROGRESS: at 53.31% examples, 430881 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:41:59,534 : INFO : EPOCH 10 - PROGRESS: at 53.68% examples, 431110 words/s, in_qsize 0, out_qsize 0
2021-09-30 11:42:00,549 : INFO : EPOCH 10 - PROGRESS: at 54.10% examples, 430753 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:42:01,584 : INFO : EPOCH 10 - PROGRESS: at 54.48% examples, 430687 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:42:02,621 : INFO : EPOCH 10 - PROGRESS: at 54.82% examples, 430378 words/s, in_qsize 2, out_qsize 1
2021-09-30 11:42:03,671 : INFO : EPOCH 10 - PROGRESS: at 55.20% examples, 430017 words/s, in_qsize 3, out_qsize 4
2021-09-30 11:42:04,706 : INFO : EPOCH 10 - PROGRESS: at 55.72% examples, 430430 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:42:05,716 : INFO : EPOCH 10 - PROGRESS: at 56.13% examples, 430021 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:42:06,741 : INFO : EPOCH 10 - PROGRESS: at 56.51% examples, 429921 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:42:07,749 : INFO : EPOCH 10 - PROGRESS: at 56.84% examples, 429678 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:42:08,771 : INFO : EPOCH 10 - PROGRESS: at 57.18% examples, 429535 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:42:09,784 : INFO : EPOCH 10 - PROGRESS: at 57.73% examples, 429229 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:42:10,801 : INFO : EPOCH 10 - PROGRESS: at 58.12% examples, 429127 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:42:11,808 : INFO : EPOCH 10 - PROGRESS: at 58.51% examples, 429022 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:42:12,810 : INFO : EPOCH 10 - PROGRESS: at 59.20% examples, 429430 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:42:13,836 : INFO : EPOCH 10 - PROGRESS: at 59.96% examples, 429592 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:42:14,914 : INFO : EPOCH 10 - PROGRESS: at 60.66% examples, 429420 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:42:15,917 : INFO : EPOCH 10 - PROGRESS: at 61.39% examples, 429827 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:42:16,920 : INFO : EPOCH 10 - PROGRESS: at 62.15% examples, 430168 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:42:17,928 : INFO : EPOCH 10 - PROGRESS: at 62.87% examples, 429991 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:42:18,991 : INFO : EPOCH 10 - PROGRESS: at 63.67% examples, 430084 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:42:20,015 : INFO : EPOCH 10 - PROGRESS: at 64.34% examples, 429712 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:42:21,025 : INFO : EPOCH 10 - PROGRESS: at 65.07% examples, 429745 words/s, in_qsize 2, out_qsize 3
2021-09-30 11:42:22,028 : INFO : EPOCH 10 - PROGRESS: at 65.64% examples, 429577 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:42:23,036 : INFO : EPOCH 10 - PROGRESS: at 66.27% examples, 429454 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:42:24,038 : INFO : EPOCH 10 - PROGRESS: at 66.64% examples, 429135 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:42:25,067 : INFO : EPOCH 10 - PROGRESS: at 66.99% examples, 428876 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:42:26,087 : INFO : EPOCH 10 - PROGRESS: at 67.61% examples, 428961 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:42:27,090 : INFO : EPOCH 10 - PROGRESS: at 68.39% examples, 429146 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:42:28,128 : INFO : EPOCH 10 - PROGRESS: at 69.08% examples, 428762 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:42:29,133 : INFO : EPOCH 10 - PROGRESS: at 69.88% examples, 428829 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:42:30,133 : INFO : EPOCH 10 - PROGRESS: at 70.68% examples, 428785 words/s, in_qsize 1, out_qsize 0
2021-09-30 11:42:31,162 : INFO : EPOCH 10 - PROGRESS: at 71.53% examples, 428508 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:42:32,194 : INFO : EPOCH 10 - PROGRESS: at 72.26% examples, 428038 words/s, in_qsize 5, out_qsize 5
2021-09-30 11:42:33,271 : INFO : EPOCH 10 - PROGRESS: at 73.17% examples, 428478 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:42:34,294 : INFO : EPOCH 10 - PROGRESS: at 73.82% examples, 428384 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:42:35,313 : INFO : EPOCH 10 - PROGRESS: at 74.51% examples, 428455 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:42:36,331 : INFO : EPOCH 10 - PROGRESS: at 75.13% examples, 428566 words/s, in_qsize 1, out_qsize 2
2021-09-30 11:42:37,363 : INFO : EPOCH 10 - PROGRESS: at 75.71% examples, 428694 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:42:38,402 : INFO : EPOCH 10 - PROGRESS: at 76.36% examples, 428051 words/s, in_qsize 3, out_qsize 5
2021-09-30 11:42:39,480 : INFO : EPOCH 10 - PROGRESS: at 77.13% examples, 427614 words/s, in_qsize 3, out_qsize 9
2021-09-30 11:42:40,483 : INFO : EPOCH 10 - PROGRESS: at 77.96% examples, 427962 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:42:41,499 : INFO : EPOCH 10 - PROGRESS: at 78.67% examples, 427743 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:42:42,516 : INFO : EPOCH 10 - PROGRESS: at 79.29% examples, 427494 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:42:43,551 : INFO : EPOCH 10 - PROGRESS: at 79.96% examples, 427402 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:42:44,574 : INFO : EPOCH 10 - PROGRESS: at 80.58% examples, 427154 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:42:45,590 : INFO : EPOCH 10 - PROGRESS: at 81.24% examples, 426765 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:42:46,594 : INFO : EPOCH 10 - PROGRESS: at 81.99% examples, 426820 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:42:47,606 : INFO : EPOCH 10 - PROGRESS: at 82.79% examples, 426810 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:42:48,635 : INFO : EPOCH 10 - PROGRESS: at 83.26% examples, 426544 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:42:49,644 : INFO : EPOCH 10 - PROGRESS: at 83.93% examples, 426505 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:42:50,655 : INFO : EPOCH 10 - PROGRESS: at 84.70% examples, 426448 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:42:51,666 : INFO : EPOCH 10 - PROGRESS: at 85.59% examples, 426738 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:42:52,670 : INFO : EPOCH 10 - PROGRESS: at 86.19% examples, 426740 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:42:53,729 : INFO : EPOCH 10 - PROGRESS: at 86.75% examples, 426637 words/s, in_qsize 6, out_qsize 3
2021-09-30 11:42:54,730 : INFO : EPOCH 10 - PROGRESS: at 87.50% examples, 426528 words/s, in_qsize 4, out_qsize 0
2021-09-30 11:42:55,756 : INFO : EPOCH 10 - PROGRESS: at 88.18% examples, 426479 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:42:56,774 : INFO : EPOCH 10 - PROGRESS: at 88.82% examples, 426518 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:42:57,788 : INFO : EPOCH 10 - PROGRESS: at 89.68% examples, 426586 words/s, in_qsize 0, out_qsize 1
2021-09-30 11:42:58,810 : INFO : EPOCH 10 - PROGRESS: at 90.49% examples, 426589 words/s, in_qsize 2, out_qsize 3
2021-09-30 11:42:59,818 : INFO : EPOCH 10 - PROGRESS: at 91.03% examples, 426789 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:43:00,841 : INFO : EPOCH 10 - PROGRESS: at 91.57% examples, 426886 words/s, in_qsize 3, out_qsize 0
2021-09-30 11:43:01,863 : INFO : EPOCH 10 - PROGRESS: at 92.09% examples, 427028 words/s, in_qsize 0, out_qsize 2
2021-09-30 11:43:02,895 : INFO : EPOCH 10 - PROGRESS: at 92.57% examples, 426865 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:43:03,911 : INFO : EPOCH 10 - PROGRESS: at 93.09% examples, 426981 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:43:04,986 : INFO : EPOCH 10 - PROGRESS: at 93.66% examples, 427207 words/s, in_qsize 2, out_qsize 2
2021-09-30 11:43:05,987 : INFO : EPOCH 10 - PROGRESS: at 94.17% examples, 427303 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:43:07,073 : INFO : EPOCH 10 - PROGRESS: at 94.69% examples, 427212 words/s, in_qsize 5, out_qsize 4
2021-09-30 11:43:08,117 : INFO : EPOCH 10 - PROGRESS: at 95.30% examples, 427685 words/s, in_qsize 1, out_qsize 1
2021-09-30 11:43:09,140 : INFO : EPOCH 10 - PROGRESS: at 95.87% examples, 427940 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:43:10,153 : INFO : EPOCH 10 - PROGRESS: at 96.35% examples, 427759 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:43:11,174 : INFO : EPOCH 10 - PROGRESS: at 96.89% examples, 427930 words/s, in_qsize 2, out_qsize 0
2021-09-30 11:43:12,183 : INFO : EPOCH 10 - PROGRESS: at 97.53% examples, 427823 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:43:12,604 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-30 11:43:12,621 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-30 11:43:12,623 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-30 11:43:12,623 : INFO : EPOCH - 10 : training on 96321721 raw words (70184630 effective words) took 163.9s, 428148 effective words/s
2021-09-30 11:43:12,623 : INFO : training on a 963217210 raw words (701878165 effective words) took 1668.3s, 420712 effective words/s
2021-09-30 11:43:12,623 : INFO : storing 331256x500 projection weights into /media/ye/project2/exp/bilingual-induction/exp1/en/en_corpus.txt_model=word2vec_vectors.vec
Loading corpus: /media/ye/project2/exp/bilingual-induction/exp1/en/en_corpus.txt
Embeddings saved to /media/ye/project2/exp/bilingual-induction/exp1/en/en_corpus.txt_model=word2vec_vectors.vec

real	31m43.583s
user	67m44.208s
sys	0m15.381s
start building a word2vec model for TRG language ...  
2021-09-30 11:44:11,959 : INFO : collecting all words and their counts
2021-09-30 11:44:12,055 : INFO : PROGRESS: at sentence #0, processed 0 words, keeping 0 word types
2021-09-30 11:44:12,965 : INFO : PROGRESS: at sentence #10000, processed 610756 words, keeping 19454 word types
2021-09-30 11:44:13,672 : INFO : PROGRESS: at sentence #20000, processed 1101607 words, keeping 27158 word types
2021-09-30 11:44:13,947 : INFO : PROGRESS: at sentence #30000, processed 1286807 words, keeping 31927 word types
2021-09-30 11:44:14,247 : INFO : PROGRESS: at sentence #40000, processed 1489810 words, keeping 35328 word types
2021-09-30 11:44:14,563 : INFO : PROGRESS: at sentence #50000, processed 1705793 words, keeping 38701 word types
2021-09-30 11:44:14,899 : INFO : PROGRESS: at sentence #60000, processed 1933905 words, keeping 42599 word types
2021-09-30 11:44:15,280 : INFO : PROGRESS: at sentence #70000, processed 2180748 words, keeping 46212 word types
2021-09-30 11:44:16,430 : INFO : PROGRESS: at sentence #80000, processed 2555380 words, keeping 54008 word types
2021-09-30 11:44:17,716 : INFO : PROGRESS: at sentence #90000, processed 3027559 words, keeping 62852 word types
2021-09-30 11:44:18,492 : INFO : PROGRESS: at sentence #100000, processed 3564854 words, keeping 70996 word types
2021-09-30 11:44:18,941 : INFO : PROGRESS: at sentence #110000, processed 3876595 words, keeping 74656 word types
2021-09-30 11:44:19,314 : INFO : PROGRESS: at sentence #120000, processed 4135019 words, keeping 76320 word types
2021-09-30 11:44:19,766 : INFO : PROGRESS: at sentence #130000, processed 4448732 words, keeping 78290 word types
2021-09-30 11:44:20,222 : INFO : PROGRESS: at sentence #140000, processed 4764187 words, keeping 79958 word types
2021-09-30 11:44:20,646 : INFO : PROGRESS: at sentence #150000, processed 5056619 words, keeping 81906 word types
2021-09-30 11:44:20,766 : INFO : PROGRESS: at sentence #160000, processed 5133769 words, keeping 84736 word types
2021-09-30 11:44:20,886 : INFO : PROGRESS: at sentence #170000, processed 5211641 words, keeping 87195 word types
2021-09-30 11:44:20,917 : INFO : collected 87462 word types from a corpus of 5230564 raw words and 172373 sentences
2021-09-30 11:44:20,917 : INFO : Loading a fresh vocabulary
2021-09-30 11:44:20,974 : INFO : effective_min_count=2 retains 40665 unique words (46% of original 87462, drops 46797)
2021-09-30 11:44:20,974 : INFO : effective_min_count=2 leaves 5183767 word corpus (99% of original 5230564, drops 46797)
2021-09-30 11:44:21,029 : INFO : deleting the raw counts dictionary of 87462 items
2021-09-30 11:44:21,031 : INFO : sample=0.001 downsamples 58 most-common words
2021-09-30 11:44:21,031 : INFO : downsampling leaves estimated 4153223 word corpus (80.1% of prior 5183767)
2021-09-30 11:44:21,078 : INFO : estimated required memory for 40665 words and 500 dimensions: 182992500 bytes
2021-09-30 11:44:21,078 : INFO : resetting layer weights
2021-09-30 11:44:25,721 : INFO : training model with 3 workers on 40665 vocabulary and 500 features, using sg=0 hs=0 sample=0.001 negative=5 window=4
2021-09-30 11:44:26,723 : INFO : EPOCH 1 - PROGRESS: at 4.66% examples, 393483 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:44:27,729 : INFO : EPOCH 1 - PROGRESS: at 12.53% examples, 439238 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:44:28,731 : INFO : EPOCH 1 - PROGRESS: at 29.37% examples, 447355 words/s, in_qsize 4, out_qsize 3
2021-09-30 11:44:29,739 : INFO : EPOCH 1 - PROGRESS: at 42.35% examples, 453937 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:44:30,753 : INFO : EPOCH 1 - PROGRESS: at 50.53% examples, 456620 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:44:31,816 : INFO : EPOCH 1 - PROGRESS: at 56.67% examples, 451577 words/s, in_qsize 6, out_qsize 5
2021-09-30 11:44:32,837 : INFO : EPOCH 1 - PROGRESS: at 67.91% examples, 452861 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:44:33,855 : INFO : EPOCH 1 - PROGRESS: at 78.76% examples, 453725 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:44:34,741 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-30 11:44:34,751 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-30 11:44:34,760 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-30 11:44:34,760 : INFO : EPOCH - 1 : training on 5230564 raw words (4153900 effective words) took 9.0s, 459590 effective words/s
2021-09-30 11:44:35,766 : INFO : EPOCH 2 - PROGRESS: at 4.78% examples, 399972 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:44:36,794 : INFO : EPOCH 2 - PROGRESS: at 11.74% examples, 421856 words/s, in_qsize 5, out_qsize 4
2021-09-30 11:44:37,800 : INFO : EPOCH 2 - PROGRESS: at 29.37% examples, 442852 words/s, in_qsize 4, out_qsize 4
2021-09-30 11:44:38,804 : INFO : EPOCH 2 - PROGRESS: at 42.09% examples, 447008 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:44:39,813 : INFO : EPOCH 2 - PROGRESS: at 50.31% examples, 451550 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:44:40,815 : INFO : EPOCH 2 - PROGRESS: at 56.70% examples, 454599 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:44:41,820 : INFO : EPOCH 2 - PROGRESS: at 67.43% examples, 454165 words/s, in_qsize 5, out_qsize 4
2021-09-30 11:44:42,826 : INFO : EPOCH 2 - PROGRESS: at 78.94% examples, 458540 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:44:43,713 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-30 11:44:43,721 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-30 11:44:43,722 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-30 11:44:43,722 : INFO : EPOCH - 2 : training on 5230564 raw words (4153515 effective words) took 9.0s, 463508 effective words/s
2021-09-30 11:44:44,752 : INFO : EPOCH 3 - PROGRESS: at 4.68% examples, 382464 words/s, in_qsize 4, out_qsize 3
2021-09-30 11:44:45,762 : INFO : EPOCH 3 - PROGRESS: at 11.69% examples, 420480 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:44:46,785 : INFO : EPOCH 3 - PROGRESS: at 28.97% examples, 436761 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:44:47,786 : INFO : EPOCH 3 - PROGRESS: at 42.36% examples, 448897 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:44:48,834 : INFO : EPOCH 3 - PROGRESS: at 50.70% examples, 451073 words/s, in_qsize 6, out_qsize 2
2021-09-30 11:44:49,843 : INFO : EPOCH 3 - PROGRESS: at 57.92% examples, 461611 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:44:50,904 : INFO : EPOCH 3 - PROGRESS: at 69.22% examples, 455384 words/s, in_qsize 6, out_qsize 8
2021-09-30 11:44:51,964 : INFO : EPOCH 3 - PROGRESS: at 82.18% examples, 464180 words/s, in_qsize 5, out_qsize 4
2021-09-30 11:44:52,508 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-30 11:44:52,511 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-30 11:44:52,515 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-30 11:44:52,515 : INFO : EPOCH - 3 : training on 5230564 raw words (4154031 effective words) took 8.8s, 472492 effective words/s
2021-09-30 11:44:53,531 : INFO : EPOCH 4 - PROGRESS: at 5.10% examples, 418439 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:44:54,630 : INFO : EPOCH 4 - PROGRESS: at 13.55% examples, 428076 words/s, in_qsize 5, out_qsize 6
2021-09-30 11:44:55,650 : INFO : EPOCH 4 - PROGRESS: at 32.51% examples, 460050 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:44:56,697 : INFO : EPOCH 4 - PROGRESS: at 45.19% examples, 462979 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:44:57,812 : INFO : EPOCH 4 - PROGRESS: at 52.37% examples, 454852 words/s, in_qsize 6, out_qsize 8
2021-09-30 11:44:58,874 : INFO : EPOCH 4 - PROGRESS: at 61.48% examples, 468084 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:44:59,910 : INFO : EPOCH 4 - PROGRESS: at 73.85% examples, 466850 words/s, in_qsize 4, out_qsize 6
2021-09-30 11:45:00,924 : INFO : EPOCH 4 - PROGRESS: at 84.03% examples, 464210 words/s, in_qsize 5, out_qsize 8
2021-09-30 11:45:01,222 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-30 11:45:01,225 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-30 11:45:01,230 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-30 11:45:01,230 : INFO : EPOCH - 4 : training on 5230564 raw words (4153226 effective words) took 8.7s, 476577 effective words/s
2021-09-30 11:45:02,238 : INFO : EPOCH 5 - PROGRESS: at 5.02% examples, 414200 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:45:03,253 : INFO : EPOCH 5 - PROGRESS: at 13.64% examples, 447873 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:45:04,418 : INFO : EPOCH 5 - PROGRESS: at 30.31% examples, 432155 words/s, in_qsize 6, out_qsize 8
2021-09-30 11:45:05,430 : INFO : EPOCH 5 - PROGRESS: at 44.83% examples, 455254 words/s, in_qsize 4, out_qsize 2
2021-09-30 11:45:06,443 : INFO : EPOCH 5 - PROGRESS: at 52.25% examples, 460603 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:45:07,499 : INFO : EPOCH 5 - PROGRESS: at 59.26% examples, 459516 words/s, in_qsize 4, out_qsize 6
2021-09-30 11:45:08,503 : INFO : EPOCH 5 - PROGRESS: at 72.37% examples, 465847 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:45:09,506 : INFO : EPOCH 5 - PROGRESS: at 82.93% examples, 466083 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:45:10,030 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-30 11:45:10,033 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-30 11:45:10,038 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-30 11:45:10,039 : INFO : EPOCH - 5 : training on 5230564 raw words (4153885 effective words) took 8.8s, 471609 effective words/s
2021-09-30 11:45:11,040 : INFO : EPOCH 6 - PROGRESS: at 4.90% examples, 409210 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:45:12,055 : INFO : EPOCH 6 - PROGRESS: at 11.74% examples, 425847 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:45:13,080 : INFO : EPOCH 6 - PROGRESS: at 29.07% examples, 439999 words/s, in_qsize 3, out_qsize 2
2021-09-30 11:45:14,088 : INFO : EPOCH 6 - PROGRESS: at 41.83% examples, 442532 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:45:15,128 : INFO : EPOCH 6 - PROGRESS: at 50.54% examples, 451584 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:45:16,140 : INFO : EPOCH 6 - PROGRESS: at 57.26% examples, 457843 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:45:17,152 : INFO : EPOCH 6 - PROGRESS: at 69.28% examples, 459783 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:45:18,193 : INFO : EPOCH 6 - PROGRESS: at 80.70% examples, 461377 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:45:18,967 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-30 11:45:18,970 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-30 11:45:18,975 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-30 11:45:18,975 : INFO : EPOCH - 6 : training on 5230564 raw words (4154547 effective words) took 8.9s, 464931 effective words/s
2021-09-30 11:45:19,994 : INFO : EPOCH 7 - PROGRESS: at 5.02% examples, 409514 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:45:21,035 : INFO : EPOCH 7 - PROGRESS: at 12.11% examples, 420231 words/s, in_qsize 5, out_qsize 8
2021-09-30 11:45:22,079 : INFO : EPOCH 7 - PROGRESS: at 31.98% examples, 459778 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:45:23,102 : INFO : EPOCH 7 - PROGRESS: at 44.96% examples, 465202 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:45:24,209 : INFO : EPOCH 7 - PROGRESS: at 52.12% examples, 457336 words/s, in_qsize 6, out_qsize 6
2021-09-30 11:45:25,216 : INFO : EPOCH 7 - PROGRESS: at 60.21% examples, 468045 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:45:26,224 : INFO : EPOCH 7 - PROGRESS: at 72.37% examples, 467411 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:45:27,272 : INFO : EPOCH 7 - PROGRESS: at 82.95% examples, 464890 words/s, in_qsize 6, out_qsize 4
2021-09-30 11:45:27,722 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-30 11:45:27,725 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-30 11:45:27,728 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-30 11:45:27,728 : INFO : EPOCH - 7 : training on 5230564 raw words (4153892 effective words) took 8.8s, 474590 effective words/s
2021-09-30 11:45:28,741 : INFO : EPOCH 8 - PROGRESS: at 4.90% examples, 403829 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:45:29,770 : INFO : EPOCH 8 - PROGRESS: at 12.94% examples, 435321 words/s, in_qsize 4, out_qsize 3
2021-09-30 11:45:30,839 : INFO : EPOCH 8 - PROGRESS: at 30.43% examples, 442746 words/s, in_qsize 5, out_qsize 4
2021-09-30 11:45:31,893 : INFO : EPOCH 8 - PROGRESS: at 43.95% examples, 451123 words/s, in_qsize 6, out_qsize 3
2021-09-30 11:45:32,909 : INFO : EPOCH 8 - PROGRESS: at 52.25% examples, 463352 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:45:33,942 : INFO : EPOCH 8 - PROGRESS: at 59.27% examples, 463422 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:45:34,943 : INFO : EPOCH 8 - PROGRESS: at 71.87% examples, 467221 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:45:35,994 : INFO : EPOCH 8 - PROGRESS: at 83.12% examples, 467387 words/s, in_qsize 4, out_qsize 3
2021-09-30 11:45:36,504 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-30 11:45:36,507 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-30 11:45:36,511 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-30 11:45:36,511 : INFO : EPOCH - 8 : training on 5230564 raw words (4152076 effective words) took 8.8s, 472755 effective words/s
2021-09-30 11:45:37,531 : INFO : EPOCH 9 - PROGRESS: at 4.86% examples, 401508 words/s, in_qsize 6, out_qsize 1
2021-09-30 11:45:38,602 : INFO : EPOCH 9 - PROGRESS: at 14.33% examples, 440903 words/s, in_qsize 4, out_qsize 3
2021-09-30 11:45:39,759 : INFO : EPOCH 9 - PROGRESS: at 32.01% examples, 439255 words/s, in_qsize 6, out_qsize 7
2021-09-30 11:45:40,828 : INFO : EPOCH 9 - PROGRESS: at 46.03% examples, 461603 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:45:41,867 : INFO : EPOCH 9 - PROGRESS: at 53.37% examples, 463350 words/s, in_qsize 5, out_qsize 4
2021-09-30 11:45:42,905 : INFO : EPOCH 9 - PROGRESS: at 61.34% examples, 464348 words/s, in_qsize 4, out_qsize 5
2021-09-30 11:45:43,925 : INFO : EPOCH 9 - PROGRESS: at 74.53% examples, 469945 words/s, in_qsize 6, out_qsize 0
2021-09-30 11:45:44,951 : INFO : EPOCH 9 - PROGRESS: at 84.60% examples, 465417 words/s, in_qsize 6, out_qsize 4
2021-09-30 11:45:45,279 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-30 11:45:45,283 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-30 11:45:45,287 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-30 11:45:45,287 : INFO : EPOCH - 9 : training on 5230564 raw words (4153385 effective words) took 8.8s, 473314 effective words/s
2021-09-30 11:45:46,311 : INFO : EPOCH 10 - PROGRESS: at 5.10% examples, 414939 words/s, in_qsize 5, out_qsize 1
2021-09-30 11:45:47,340 : INFO : EPOCH 10 - PROGRESS: at 13.93% examples, 444897 words/s, in_qsize 5, out_qsize 0
2021-09-30 11:45:48,366 : INFO : EPOCH 10 - PROGRESS: at 30.63% examples, 450200 words/s, in_qsize 4, out_qsize 3
2021-09-30 11:45:49,368 : INFO : EPOCH 10 - PROGRESS: at 43.41% examples, 456648 words/s, in_qsize 4, out_qsize 3
2021-09-30 11:45:50,371 : INFO : EPOCH 10 - PROGRESS: at 51.60% examples, 464401 words/s, in_qsize 4, out_qsize 1
2021-09-30 11:45:51,409 : INFO : EPOCH 10 - PROGRESS: at 58.40% examples, 465284 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:45:52,415 : INFO : EPOCH 10 - PROGRESS: at 70.51% examples, 466510 words/s, in_qsize 5, out_qsize 2
2021-09-30 11:45:53,530 : INFO : EPOCH 10 - PROGRESS: at 82.77% examples, 466857 words/s, in_qsize 4, out_qsize 6
2021-09-30 11:45:54,021 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-30 11:45:54,023 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-30 11:45:54,027 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-30 11:45:54,027 : INFO : EPOCH - 10 : training on 5230564 raw words (4153237 effective words) took 8.7s, 475235 effective words/s
2021-09-30 11:45:54,027 : INFO : training on a 52305640 raw words (41535694 effective words) took 88.3s, 470360 effective words/s
2021-09-30 11:45:54,027 : INFO : storing 40665x500 projection weights into /media/ye/project2/exp/bilingual-induction/exp1/th/th_corpus.txt_model=word2vec_vectors.vec
Loading corpus: /media/ye/project2/exp/bilingual-induction/exp1/th/th_corpus.txt
Embeddings saved to /media/ye/project2/exp/bilingual-induction/exp1/th/th_corpus.txt_model=word2vec_vectors.vec

real	1m49.735s
user	3m20.585s
sys	0m2.052s
check for SRC:  see word2vec and fastext models...
1_all.en.word
big-model
data_eng.txt
en_corpus.txt
en_corpus.txt_model=word2vec_vectors.vec
UMBC_tokenized_1million.txt
word2vec
check for TRG:  see word2vec and fastext models...
2_all.th.word
best.clean.corpus
data_tha-token.txt.line.rm-lineno
fasttext
th_corpus.txt
th_corpus.txt_model=fasttext_vectors.vec
th_corpus.txt_model=word2vec_vectors.vec
word2vec
mkdir word2vec-output16/
Processing /media/ye/project2/exp/bilingual-induction/exp1/en/word2vec/en_corpus.txt_model=word2vec_vectors.vec
Processing /media/ye/project2/exp/bilingual-induction/exp1/th/word2vec/th_corpus.txt_model=word2vec_vectors.vec
Source vocab is 1887310 tokens
Target vocab is 28721 tokens

real	1m6.707s
user	0m30.860s
sys	0m2.888s
source_vocab.txt  target_vocab.txt  test_dict.csv  train_dict.csv
Loading source vocab
Source vocab has 1887310 words
---
Loading target vocab
Target vocab has 28721 words
Loading dictionary - Done 1000 of 125516
Loading dictionary - Done 2000 of 125516
Loading dictionary - Done 3000 of 125516
Loading dictionary - Done 4000 of 125516
Loading dictionary - Done 5000 of 125516
Loading dictionary - Done 6000 of 125516
Loading dictionary - Done 7000 of 125516
Loading dictionary - Done 8000 of 125516
Loading dictionary - Done 9000 of 125516
Loading dictionary - Done 10000 of 125516
Loading dictionary - Done 11000 of 125516
Loading dictionary - Done 12000 of 125516
Loading dictionary - Done 13000 of 125516
Loading dictionary - Done 14000 of 125516
Loading dictionary - Done 15000 of 125516
Loading dictionary - Done 16000 of 125516
Loading dictionary - Done 17000 of 125516
Loading dictionary - Done 18000 of 125516
Loading dictionary - Done 19000 of 125516
Loading dictionary - Done 20000 of 125516
Loading dictionary - Done 21000 of 125516
Loading dictionary - Done 22000 of 125516
Loading dictionary - Done 23000 of 125516
Loading dictionary - Done 24000 of 125516
Loading dictionary - Done 25000 of 125516
Loading dictionary - Done 26000 of 125516
Loading dictionary - Done 27000 of 125516
Loading dictionary - Done 28000 of 125516
Loading dictionary - Done 29000 of 125516
Loading dictionary - Done 30000 of 125516
Loading dictionary - Done 31000 of 125516
Loading dictionary - Done 32000 of 125516
Loading dictionary - Done 33000 of 125516
Loading dictionary - Done 34000 of 125516
Loading dictionary - Done 35000 of 125516
Loading dictionary - Done 36000 of 125516
Loading dictionary - Done 37000 of 125516
Loading dictionary - Done 38000 of 125516
Loading dictionary - Done 39000 of 125516
Loading dictionary - Done 40000 of 125516
Loading dictionary - Done 41000 of 125516
Loading dictionary - Done 42000 of 125516
Loading dictionary - Done 43000 of 125516
Loading dictionary - Done 44000 of 125516
Loading dictionary - Done 45000 of 125516
Loading dictionary - Done 46000 of 125516
Loading dictionary - Done 47000 of 125516
Loading dictionary - Done 48000 of 125516
Loading dictionary - Done 49000 of 125516
Loading dictionary - Done 50000 of 125516
Loading dictionary - Done 51000 of 125516
Loading dictionary - Done 52000 of 125516
Loading dictionary - Done 53000 of 125516
Loading dictionary - Done 54000 of 125516
Loading dictionary - Done 55000 of 125516
Loading dictionary - Done 56000 of 125516
Loading dictionary - Done 57000 of 125516
Loading dictionary - Done 58000 of 125516
Loading dictionary - Done 59000 of 125516
Loading dictionary - Done 60000 of 125516
Loading dictionary - Done 61000 of 125516
Loading dictionary - Done 62000 of 125516
Loading dictionary - Done 63000 of 125516
Loading dictionary - Done 64000 of 125516
Loading dictionary - Done 65000 of 125516
Loading dictionary - Done 66000 of 125516
Loading dictionary - Done 67000 of 125516
Loading dictionary - Done 68000 of 125516
Loading dictionary - Done 69000 of 125516
Loading dictionary - Done 70000 of 125516
Loading dictionary - Done 71000 of 125516
Loading dictionary - Done 72000 of 125516
Loading dictionary - Done 73000 of 125516
Loading dictionary - Done 74000 of 125516
Loading dictionary - Done 75000 of 125516
Loading dictionary - Done 76000 of 125516
Loading dictionary - Done 77000 of 125516
Loading dictionary - Done 78000 of 125516
Loading dictionary - Done 79000 of 125516
Loading dictionary - Done 80000 of 125516
Loading dictionary - Done 81000 of 125516
Loading dictionary - Done 82000 of 125516
Loading dictionary - Done 83000 of 125516
Loading dictionary - Done 84000 of 125516
Loading dictionary - Done 85000 of 125516
Loading dictionary - Done 86000 of 125516
Loading dictionary - Done 87000 of 125516
Loading dictionary - Done 88000 of 125516
Loading dictionary - Done 89000 of 125516
Loading dictionary - Done 90000 of 125516
Loading dictionary - Done 91000 of 125516
Loading dictionary - Done 92000 of 125516
Loading dictionary - Done 93000 of 125516
Loading dictionary - Done 94000 of 125516
Loading dictionary - Done 95000 of 125516
Loading dictionary - Done 96000 of 125516
Loading dictionary - Done 97000 of 125516
Loading dictionary - Done 98000 of 125516
Loading dictionary - Done 99000 of 125516
Loading dictionary - Done 100000 of 125516
Loading dictionary - Done 101000 of 125516
Loading dictionary - Done 102000 of 125516
Loading dictionary - Done 103000 of 125516
Loading dictionary - Done 104000 of 125516
Loading dictionary - Done 105000 of 125516
Loading dictionary - Done 106000 of 125516
Loading dictionary - Done 107000 of 125516
Loading dictionary - Done 108000 of 125516
Loading dictionary - Done 109000 of 125516
Loading dictionary - Done 110000 of 125516
Loading dictionary - Done 111000 of 125516
Loading dictionary - Done 112000 of 125516
Loading dictionary - Done 113000 of 125516
Loading dictionary - Done 114000 of 125516
Loading dictionary - Done 115000 of 125516
Loading dictionary - Done 116000 of 125516
Loading dictionary - Done 117000 of 125516
Loading dictionary - Done 118000 of 125516
Loading dictionary - Done 119000 of 125516
Loading dictionary - Done 120000 of 125516
Loading dictionary - Done 121000 of 125516
Loading dictionary - Done 122000 of 125516
Loading dictionary - Done 123000 of 125516
Loading dictionary - Done 124000 of 125516
Loading dictionary - Done 125000 of 125516
Loaded 22464 entries from the original dictionary, which had: 125516

real	0m1.667s
user	0m1.723s
sys	0m1.114s
source_vocab.txt  target_vocab.txt  test_dict.csv  train_dict.csv
run get_vocab_from_vectors.py ...
Processing /media/ye/project2/exp/bilingual-induction/exp1/en/word2vec/en_corpus.txt_model=word2vec_vectors.vec
Processing /media/ye/project2/exp/bilingual-induction/exp1/th/word2vec/th_corpus.txt_model=word2vec_vectors.vec
Source vocab is 1887310 tokens
Target vocab is 28721 tokens

real	0m36.075s
user	0m23.776s
sys	0m1.274s
mkdir vecmap-output16/
mkdir: cannot create directory ‘/media/ye/project2/exp/bilingual-induction/exp1/en-th/vecmap-output16/’: File exists
run mk-vecmap.sh ...
WARNING: OOV dictionary entry (english - welsh)
WARNING: OOV dictionary entry (palindrome - หลัง)
WARNING: OOV dictionary entry (peregrinate - เดินทาง)
WARNING: OOV dictionary entry (zonk - หมดสติ)
WARNING: OOV dictionary entry (snick - เล็ม)
WARNING: OOV dictionary entry (airdrome - สนามบิน)
WARNING: OOV dictionary entry (minimart - มินิมาร์ท)
WARNING: OOV dictionary entry (soothsay - ทำนาย)
WARNING: OOV dictionary entry (henpeck - ด่าว่า)
WARNING: OOV dictionary entry (whirlybird - เฮลิคอปเตอร์)
WARNING: OOV dictionary entry (malmsey - เหล้าองุ่น)
WARNING: OOV dictionary entry (baccy - บุหรี่)
WARNING: OOV dictionary entry (madden - บ้า)
WARNING: OOV dictionary entry (ruck - ต่อสู้)
WARNING: OOV dictionary entry (nippy - จัดจ้าน)
WARNING: OOV dictionary entry (indite - ประพันธ์)
WARNING: OOV dictionary entry (bonzo - บ้า)
WARNING: OOV dictionary entry (submerse - จุ่ม)
WARNING: OOV dictionary entry (lithesome - อ่อนช้อย)
WARNING: OOV dictionary entry (pinstriper - นักธุรกิจ)
WARNING: OOV dictionary entry (dipper - จวัก)
WARNING: OOV dictionary entry (tomtit - อึ)
WARNING: OOV dictionary entry (culantro - ผักชีฝรั่ง)
WARNING: OOV dictionary entry (reenforce - เสริม)
WARNING: OOV dictionary entry (resentfully - ตาขวาง)
WARNING: OOV dictionary entry (headspring - ต้นน้ำ)
WARNING: OOV dictionary entry (quaver - สั่น)
WARNING: OOV dictionary entry (tike - สุนัข)
WARNING: OOV dictionary entry (manful - กล้าหาญ)
WARNING: OOV dictionary entry (desperado - อาชญากร)
WARNING: OOV dictionary entry (louvre - บานเกล็ด)
WARNING: OOV dictionary entry (jessamine - มะลิ)
WARNING: OOV dictionary entry (tegument - เปลือก)
WARNING: OOV dictionary entry (cancellate - บาง)
WARNING: OOV dictionary entry (sermonize - เทศนา)
WARNING: OOV dictionary entry (niter - ดินประสิว)
WARNING: OOV dictionary entry (ligate - ผูก)
WARNING: OOV dictionary entry (gingiva - เหงือก)
WARNING: OOV dictionary entry (stabile - มั่นคง)
WARNING: OOV dictionary entry (dosh - เงิน)
WARNING: OOV dictionary entry (blandish - ปากหวาน)
WARNING: OOV dictionary entry (whelm - ครอบงำ)
WARNING: OOV dictionary entry (overjoy - ลิงโลด)
WARNING: OOV dictionary entry (glitteringly - วับแวม)
WARNING: OOV dictionary entry (peckish - หิว)
WARNING: OOV dictionary entry (abominate - ชิงชัง)
WARNING: OOV dictionary entry (hexapod - แมลง)
WARNING: OOV dictionary entry (chippy - โสเภณี)
WARNING: OOV dictionary entry (jillion - มากมาย)
WARNING: OOV dictionary entry (brill - สุดยอด)
WARNING: OOV dictionary entry (oldish - แก่)
WARNING: OOV dictionary entry (parboil - ลวก)
WARNING: OOV dictionary entry (sweepingly - กราด)
WARNING: OOV dictionary entry (trustfully - สนิทใจ)
WARNING: OOV dictionary entry (psammite - หินทราย)
WARNING: OOV dictionary entry (knackered - เสีย)
WARNING: OOV dictionary entry (nacre - ไข่มุก)
WARNING: OOV dictionary entry (faff - จู้จี้)
WARNING: OOV dictionary entry (earplug - อากาศ)
WARNING: OOV dictionary entry (shallot - หอม)
WARNING: OOV dictionary entry (highjack - เรือ)
WARNING: OOV dictionary entry (marge - ริม)
WARNING: OOV dictionary entry (langur - ค่าง)
WARNING: OOV dictionary entry (sparge - พรม)
WARNING: OOV dictionary entry (baboo - นาย)
WARNING: OOV dictionary entry (nark - รบกวน)
WARNING: OOV dictionary entry (boodie - ก้น)
WARNING: OOV dictionary entry (konk - หัว)
WARNING: OOV dictionary entry (spatter - กระเด็น)
WARNING: OOV dictionary entry (cank - จ้อ)
WARNING: OOV dictionary entry (nim - สะเดา)
WARNING: OOV dictionary entry (ruffly - กระเพื่อม)
WARNING: OOV dictionary entry (ranee - ราชินี)
WARNING: OOV dictionary entry (bate - ลด)
WARNING: OOV dictionary entry (scurf - สะเก็ด)
WARNING: OOV dictionary entry (taters - มันฝรั่ง)
WARNING: OOV dictionary entry (boody - ก้น)
WARNING: OOV dictionary entry (scutcheon - โล่)
WARNING: OOV dictionary entry (grizzle - ขาว)
WARNING: OOV dictionary entry (middlebrow - สามัญ)
WARNING: OOV dictionary entry (persimmon - พลับ)
WARNING: OOV dictionary entry (padre - บาทหลวง)
WARNING: OOV dictionary entry (champaign - ที่ราบ)
WARNING: OOV dictionary entry (tauten - ตึง)
WARNING: OOV dictionary entry (regina - ราชินี)
WARNING: OOV dictionary entry (snoot - จมูก)
WARNING: OOV dictionary entry (tremblingly - สั่น)
WARNING: OOV dictionary entry (bate - อดกลั้น)
WARNING: OOV dictionary entry (pernickety - จู้จี้)
WARNING: OOV dictionary entry (seclude - แยกตัว)
WARNING: OOV dictionary entry (grandmamma - ยาย)
WARNING: OOV dictionary entry (hallo - ร้องเรียก)
WARNING: OOV dictionary entry (tabor - ตะโพน)
WARNING: OOV dictionary entry (gride - ครูด)
WARNING: OOV dictionary entry (kvetch - บ่น)
WARNING: OOV dictionary entry (adventurously - ผาดโผน)
WARNING: OOV dictionary entry (corking - สุดยอด)
WARNING: OOV dictionary entry (madden - คลั่ง)
WARNING: OOV dictionary entry (logy - เฉื่อยชา)
WARNING: OOV dictionary entry (kak - อึ)
WARNING: OOV dictionary entry (waspish - เจ้าอารมณ์)
WARNING: OOV dictionary entry (protuberant - โหนก)
WARNING: OOV dictionary entry (gallinaceous - ไก่)
WARNING: OOV dictionary entry (cockscomb - หงอนไก่)
WARNING: OOV dictionary entry (musjid - มัสยิด)
WARNING: OOV dictionary entry (boku - มาก)
WARNING: OOV dictionary entry (thunderbox - ห้องส้วม)
WARNING: OOV dictionary entry (mingy - ขี้เหนียว)
WARNING: OOV dictionary entry (guv’nor - เจ้านาย)
WARNING: OOV dictionary entry (rambutan - เงาะ)
WARNING: OOV dictionary entry (sobbingly - กระซิก)
WARNING: OOV dictionary entry (trolly - รถเข็น)
WARNING: OOV dictionary entry (noddle - หัว)
WARNING: OOV dictionary entry (muskmelon - แตงไทย)
WARNING: OOV dictionary entry (razz - หยอกล้อ)
WARNING: OOV dictionary entry (gateau - เค้ก)
WARNING: OOV dictionary entry (punctiliously - พิถีพิถัน)
WARNING: OOV dictionary entry (coxcomb - หงอนไก่)
WARNING: OOV dictionary entry (lade - บรรทุก)
WARNING: OOV dictionary entry (charbroil - ต้ม)
WARNING: OOV dictionary entry (retroact - โต้ตอบ)
WARNING: OOV dictionary entry (shillelagh - กระบอง)
WARNING: OOV dictionary entry (tremblingly - ระรัว)
WARNING: OOV dictionary entry (pukka - แท้)
WARNING: OOV dictionary entry (tatter - ผ้าขี้ริ้ว)
WARNING: OOV dictionary entry (semblable - คล้าย)
WARNING: OOV dictionary entry (bawd - โสเภณี)
WARNING: OOV dictionary entry (lightsome - ร่าเริง)
WARNING: OOV dictionary entry (banger - ไส้กรอก)
WARNING: OOV dictionary entry (vapourize - ระเหย)
WARNING: OOV dictionary entry (datura - ลำโพง)
WARNING: OOV dictionary entry (jape - เยาะเย้ย)
WARNING: OOV dictionary entry (dearie - ที่รัก)
WARNING: OOV dictionary entry (grandmamma - ย่า)
WARNING: OOV dictionary entry (melodiously - แจ้ว)
WARNING: OOV dictionary entry (gammon - โกง)
WARNING: OOV dictionary entry (lichi - ลิ้นจี่)
WARNING: OOV dictionary entry (unfix - ปลด)
WARNING: OOV dictionary entry (ramie - ป่าน)
WARNING: OOV dictionary entry (prexy - ประธาน)
WARNING: OOV dictionary entry (baluster - กรง)
WARNING: OOV dictionary entry (yaws - คุดทะราด)
WARNING: OOV dictionary entry (wizen - เหี่ยวแห้ง)
WARNING: OOV dictionary entry (zonk - ตี)
WARNING: OOV dictionary entry (viand - อาหาร)
WARNING: OOV dictionary entry (distend - อืด)
WARNING: OOV dictionary entry (gravid - ตั้งครรภ์)
WARNING: OOV dictionary entry (pulverise - โขลก)
WARNING: OOV dictionary entry (corsair - โจรสลัด)
WARNING: OOV dictionary entry (argosy - ตะเภา)
WARNING: OOV dictionary entry (gateaux - เค้ก)
WARNING: OOV dictionary entry (gammon - แฮม)
WARNING: OOV dictionary entry (lattermost - ล่าสุด)
WARNING: OOV dictionary entry (cakehole - ปาก)
WARNING: OOV dictionary entry (underripe - ห่าม)
WARNING: OOV dictionary entry (lutist - เวณิก)
WARNING: OOV dictionary entry (bewitchingly - เปรี้ยว)
WARNING: OOV dictionary entry (bombardier - ปืนใหญ่)
WARNING: OOV dictionary entry (grannie - ย่า)
WARNING: OOV dictionary entry (blenny - ตีน)
WARNING: OOV dictionary entry (spoony - คลั่งไคล้)
WARNING: OOV dictionary entry (tutti - ทั้งหมด)
WARNING: OOV dictionary entry (helve - ด้าม)
WARNING: OOV dictionary entry (wazz - ฉี่)
WARNING: OOV dictionary entry (indurate - แข็ง)
WARNING: OOV dictionary entry (taters - หนาวเย็น)
WARNING: OOV dictionary entry (famish - อดอยาก)
WARNING: OOV dictionary entry (whup - เฆี่ยน)
WARNING: OOV dictionary entry (myrobalan - สมอ)
WARNING: OOV dictionary entry (phyle - ชนชาติ)
WARNING: OOV dictionary entry (thuddingly - กุบกับ)
WARNING: OOV dictionary entry (chokey - คุก)
WARNING: OOV dictionary entry (springhead - ต้นกำเนิด)
WARNING: OOV dictionary entry (tremblingly - เร่า)
WARNING: OOV dictionary entry (cloy - เอียน)
WARNING: OOV dictionary entry (abloom - บาน)
WARNING: OOV dictionary entry (comestible - อาหาร)
WARNING: OOV dictionary entry (vocable - คำ)
WARNING: OOV dictionary entry (dicky - อ่อนแอ)
WARNING: OOV dictionary entry (ropey - ป่วย)
WARNING: OOV dictionary entry (proteid - โปรตีน)
WARNING: OOV dictionary entry (lour - มืดครึ้ม)
WARNING: OOV dictionary entry (granger - ชาวนา)
WARNING: OOV dictionary entry (earthman - มนุษย์)
WARNING: OOV dictionary entry (blooey - เสียหาย)
WARNING: OOV dictionary entry (fila - เส้นใย)
WARNING: OOV dictionary entry (smoulder - คั่งแค้น)
WARNING: OOV dictionary entry (unbridle - ปลดปล่อย)
WARNING: OOV dictionary entry (lave - ล้าง)
WARNING: OOV dictionary entry (gobsmacked - ประหลาดใจ)
WARNING: OOV dictionary entry (burgle - บ้าน)
WARNING: OOV dictionary entry (smoulder - อัดอั้น)
WARNING: OOV dictionary entry (unsmooth - ฝืด)
WARNING: OOV dictionary entry (fitba - ฟุตบอล)
WARNING: OOV dictionary entry (superfine - ดีเยี่ยม)
WARNING: OOV dictionary entry (fantasise - จินตนาการ)
WARNING: OOV dictionary entry (cutty - สั้น)
WARNING: OOV dictionary entry (drat - สับสน)
WARNING: OOV dictionary entry (intonate - สวดมนต์)
WARNING: OOV dictionary entry (uncourtly - หยาบ)
WARNING: OOV dictionary entry (bazoo - ปาก)
WARNING: OOV dictionary entry (drub - ตี)
WARNING: OOV dictionary entry (drub - เอาชนะ)
WARNING: OOV dictionary entry (surcease - เลิก)
WARNING: OOV dictionary entry (grandpapa - ตา)
WARNING: OOV dictionary entry (brewster - เบียร์)
WARNING: OOV dictionary entry (summersault - ตีลังกา)
WARNING: OOV dictionary entry (vivisect - ชำแหละ)
WARNING: OOV dictionary entry (enceinte - ตั้งครรภ์)
WARNING: OOV dictionary entry (contuse - ฟกช้ำ)
WARNING: OOV dictionary entry (emmet - นักท่องเที่ยว)
WARNING: OOV dictionary entry (slimline - บอบบาง)
WARNING: OOV dictionary entry (slattern - โสเภณี)
WARNING: OOV dictionary entry (mooch - ขโมย)
WARNING: OOV dictionary entry (brokenly - กระท่อนกระแท่น)
WARNING: OOV dictionary entry (gamecock - ไก่ชน)
WARNING: OOV dictionary entry (eldritch - ประหลาด)
WARNING: OOV dictionary entry (percuss - เคาะ)
WARNING: OOV dictionary entry (deva - พระเจ้า)
WARNING: OOV dictionary entry (conjuration - เวทมนตร์)
WARNING: OOV dictionary entry (animadvert - วิจารณ์)
WARNING: OOV dictionary entry (varda - มอง)
WARNING: OOV dictionary entry (swop - แลกเปลี่ยน)
WARNING: OOV dictionary entry (steeve - อัด)
WARNING: OOV dictionary entry (rotorhead - นักบิน)
WARNING: OOV dictionary entry (khazi - ส้วม)
WARNING: OOV dictionary entry (tiffin - ปิ่นโต)
WARNING: OOV dictionary entry (ket - ลูกอม)
WARNING: OOV dictionary entry (waitperson - บริกร)
WARNING: OOV dictionary entry (boisterously - ปึงปัง)
WARNING: OOV dictionary entry (spicula - หนาม)
WARNING: OOV dictionary entry (pyknic - อ้วน)
WARNING: OOV dictionary entry (unsharpened - ทู่)
WARNING: OOV dictionary entry (sailer - เรือใบ)
WARNING: OOV dictionary entry (ruck - ยับ)
WARNING: OOV dictionary entry (thirl - เจาะ)
WARNING: OOV dictionary entry (largehearted - ใจดี)
WARNING: OOV dictionary entry (gesticulate - โบกไม้โบกมือ)
WARNING: OOV dictionary entry (sonance - เสียง)
WARNING: OOV dictionary entry (marihuana - กัญชา)
WARNING: OOV dictionary entry (telly - โทรทัศน์)
WARNING: OOV dictionary entry (inveterately - งอมแงม)
WARNING: OOV dictionary entry (freebee - เสรีภาพ)
WARNING: OOV dictionary entry (truncheon - กระบอง)
WARNING: OOV dictionary entry (earplug - เสียง)
WARNING: OOV dictionary entry (diphthong - ควบกล้ำ)
WARNING: OOV dictionary entry (bedeck - ประดับประดา)
WARNING: OOV dictionary entry (lurcher - ขโมย)
WARNING: OOV dictionary entry (crunchie - ทหาร)
WARNING: OOV dictionary entry (tatty - หยาบ)
WARNING: OOV dictionary entry (pintle - เดือย)
WARNING: OOV dictionary entry (lumpish - อืดอาด)
WARNING: OOV dictionary entry (freeby - เสรีภาพ)
WARNING: OOV dictionary entry (uncloak - เปิดเผย)
WARNING: OOV dictionary entry (brill - ดีมาก)
WARNING: OOV dictionary entry (boozer - ผับ)
WARNING: OOV dictionary entry (advertent - สนใจ)
WARNING: OOV dictionary entry (maestoso - ผึ่งผาย)
WARNING: OOV dictionary entry (wonga - เงิน)
WARNING: OOV dictionary entry (overmaster - ครอบงำ)
WARNING: OOV dictionary entry (cocoanut - มะพร้าว)
WARNING: OOV dictionary entry (unclose - เปิด)
WARNING: OOV dictionary entry (florae - พืชพรรณ)
WARNING: OOV dictionary entry (motionlessly - แอ้งแม้ง)
WARNING: OOV dictionary entry (crotchet - ตะขอ)
WARNING: OOV dictionary entry (pother - ยุ่งเหยิง)
WARNING: OOV dictionary entry (doorsill - ธรณีประตู)
WARNING: OOV dictionary entry (splashboard - กันสาด)
WARNING: OOV dictionary entry (slantwise - เอียง)
WARNING: OOV dictionary entry (inhabitancy - ที่อยู่อาศัย)
WARNING: OOV dictionary entry (ubosot - อุโบสถ)
WARNING: OOV dictionary entry (wame - ท้อง)
WARNING: OOV dictionary entry (interlard - สอดแทรก)
WARNING: OOV dictionary entry (braise - เคี่ยว)
WARNING: OOV dictionary entry (asafetida - มหาหิงคุ์)
WARNING: OOV dictionary entry (faubourg - ชานเมือง)
WARNING: OOV dictionary entry (summerset - ตีลังกา)
WARNING: OOV dictionary entry (carambola - มะเฟือง)
WARNING: OOV dictionary entry (hankie - ผ้าเช็ดหน้า)
WARNING: OOV dictionary entry (triggerman - มือปืน)
WARNING: OOV dictionary entry (serration - ปากฉลาม)
WARNING: OOV dictionary entry (tiddly - เล็กน้อย)
WARNING: OOV dictionary entry (incise - ผ่าตัด)
WARNING: OOV dictionary entry (papilla - หัวนม)
WARNING: OOV dictionary entry (chinky - เจ๊ก)
WARNING: OOV dictionary entry (vitamine - วิตามิน)
WARNING: OOV dictionary entry (dissimulate - ปิดบัง)
WARNING: OOV dictionary entry (chavvy - เด็ก)
WARNING: OOV dictionary entry (modish - ทันสมัย)
WARNING: OOV dictionary entry (homie - เพื่อน)
WARNING: OOV dictionary entry (kris - กริช)
WARNING: OOV dictionary entry (maleficent - ชั่วร้าย)
WARNING: OOV dictionary entry (univalent - เดี่ยว)
WARNING: OOV dictionary entry (nauseate - คลื่นไส้)
WARNING: OOV dictionary entry (hunchbacked - ค่อม)
WARNING: OOV dictionary entry (brewski - เบียร์)
WARNING: OOV dictionary entry (resect - ชำแหละ)
WARNING: OOV dictionary entry (epiphyte - เฟิร์น)
WARNING: OOV dictionary entry (camelopard - ยีราฟ)
WARNING: OOV dictionary entry (wive - แต่งงาน)
WARNING: OOV dictionary entry (rollick - กระโดดโลดเต้น)
WARNING: OOV dictionary entry (meliorate - บรรเทา)
WARNING: OOV dictionary entry (pulchritudinous - สวย)
WARNING: OOV dictionary entry (agley - บิด)
WARNING: OOV dictionary entry (peevishly - กระเง้ากระงอด)
WARNING: OOV dictionary entry (kiester - ก้น)
WARNING: OOV dictionary entry (strop - สาย)
WARNING: OOV dictionary entry (hackle - หวี)
WARNING: OOV dictionary entry (scurf - รังแค)
WARNING: OOV dictionary entry (tomtom - เถิดเทิง)
WARNING: OOV dictionary entry (entwine - พัวพัน)
WARNING: OOV dictionary entry (weatherboard - กันสาด)
WARNING: OOV dictionary entry (solitarily - เดียวดาย)
WARNING: OOV dictionary entry (bazoo - ท้อง)
WARNING: OOV dictionary entry (longan - ลำไย)
WARNING: OOV dictionary entry (gib - ลิ่ม)
WARNING: OOV dictionary entry (moggie - แมว)
WARNING: OOV dictionary entry (palfrey - ม้า)
WARNING: OOV dictionary entry (manoeuver - กลยุทธ์)
WARNING: OOV dictionary entry (sodbuster - ชาวนา)
WARNING: OOV dictionary entry (bootie - ก้น)
WARNING: OOV dictionary entry (sarky - เสียดสี)
WARNING: OOV dictionary entry (clarty - สกปรก)
WARNING: OOV dictionary entry (gourami - ใบไม้)
WARNING: OOV dictionary entry (argosy - สำเภา)
WARNING: OOV dictionary entry (ravel - ยุ่งเหยิง)
WARNING: OOV dictionary entry (venge - แก้แค้น)
WARNING: OOV dictionary entry (preterit - อดีตกาล)
WARNING: OOV dictionary entry (gran - ยาย)
WARNING: OOV dictionary entry (mickle - มาก)
WARNING: OOV dictionary entry (rani - ราชินี)
WARNING: OOV dictionary entry (pretermit - ละทิ้ง)
WARNING: OOV dictionary entry (billie - แบงค์)
WARNING: OOV dictionary entry (peculate - ยักยอก)
WARNING: OOV dictionary entry (overcloud - มืดมัว)
WARNING: OOV dictionary entry (waspy - เจ้าอารมณ์)
WARNING: OOV dictionary entry (cank - เม้าท์)
WARNING: OOV dictionary entry (parky - หนาวเย็น)
WARNING: OOV dictionary entry (magnetize - ดึงดูดใจ)
WARNING: OOV dictionary entry (meshugah - บ้า)
WARNING: OOV dictionary entry (lissome - คล่องแคล่ว)
WARNING: OOV dictionary entry (rugose - ย่น)
WARNING: OOV dictionary entry (labium - ริมฝีปาก)
WARNING: OOV dictionary entry (grannie - ยาย)
WARNING: OOV dictionary entry (whiffle - รวนเร)
WARNING: OOV dictionary entry (guber - เนื้องอก)
WARNING: OOV dictionary entry (hardhearted - โหดร้าย)
WARNING: OOV dictionary entry (translocate - โยกย้าย)
WARNING: OOV dictionary entry (snoot - ดูถูก)
WARNING: OOV dictionary entry (bijou - เพชร)
WARNING: OOV dictionary entry (pule - คร่ำครวญ)
WARNING: OOV dictionary entry (sparge - ประปราย)
WARNING: OOV dictionary entry (appendent - ผนวก)
WARNING: OOV dictionary entry (magnetise - ดึงดูดใจ)
WARNING: OOV dictionary entry (shipside - ท่าเรือ)
WARNING: OOV dictionary entry (reave - แย่ง)
WARNING: OOV dictionary entry (yammer - คราง)
WARNING: OOV dictionary entry (coquet - ยั่วยวน)
WARNING: OOV dictionary entry (sourish - เปรี้ยว)
WARNING: OOV dictionary entry (glim - แหล่ง)
WARNING: OOV dictionary entry (eidolon - ผี)
WARNING: OOV dictionary entry (roister - เอะอะโวยวาย)
WARNING: OOV dictionary entry (stang - สตางค์)
WARNING: OOV dictionary entry (chuddy - หมากฝรั่ง)
WARNING: OOV dictionary entry (indistinctively - กำปั้นทุบดิน)
WARNING: OOV dictionary entry (melodiously - เจื้อยแจ้ว)
WARNING: OOV dictionary entry (wilfull - ดื้อดึง)
WARNING: OOV dictionary entry (skene - กริช)
WARNING: OOV dictionary entry (finical - จุกจิก)
WARNING: OOV dictionary entry (tumid - บวม)
WARNING: OOV dictionary entry (copter - เฮลิคอปเตอร์)
WARNING: OOV dictionary entry (stymy - ขัดขวาง)
WARNING: OOV dictionary entry (aks - ถาม)
WARNING: OOV dictionary entry (rumple - ยับ)
WARNING: OOV dictionary entry (swaddle - พัน)
WARNING: OOV dictionary entry (pushchair - รถเข็น)
WARNING: OOV dictionary entry (spathe - กาบ)
WARNING: OOV dictionary entry (spatter - กระเซ็น)
WARNING: OOV dictionary entry (chivvy - ไล่ล่า)
WARNING: OOV dictionary entry (anear - ใกล้)
WARNING: OOV dictionary entry (redskin - อินเดียนแดง)
WARNING: OOV dictionary entry (unfetter - ปลดปล่อย)
WARNING: OOV dictionary entry (sawbones - ศัลยแพทย์)
WARNING: OOV dictionary entry (immure - กักขัง)
WARNING: OOV dictionary entry (quirt - แส้)
WARNING: OOV dictionary entry (kraal - หมู่บ้าน)
WARNING: OOV dictionary entry (perfuse - พรม)
WARNING: OOV dictionary entry (untidily - รกเรื้อ)
WARNING: OOV dictionary entry (declamatory - ฉะฉาน)
WARNING: OOV dictionary entry (scurf - ไคล)
WARNING: OOV dictionary entry (bazoo - ก้น)
WARNING: OOV dictionary entry (outmanoeuvre - ได้เปรียบ)
WARNING: OOV dictionary entry (pukka - ของแท้)
WARNING: OOV dictionary entry (strickle - ปาด)
WARNING: OOV dictionary entry (kouprey - กูปรี)
WARNING: OOV dictionary entry (globefish - ปักเป้า)
WARNING: OOV dictionary entry (whelm - ท่วม)
WARNING: OOV dictionary entry (zeds - หลับ)
WARNING: OOV dictionary entry (cack - อึ)
WARNING: OOV dictionary entry (moggy - แมว)
WARNING: OOV dictionary entry (pedagog - อาจารย์)
WARNING: OOV dictionary entry (phonate - ออกเสียง)
WARNING: OOV dictionary entry (macerate - เปื่อย)
WARNING: OOV dictionary entry (toffy - ลูกอม)
WARNING: OOV dictionary entry (epiphyte - กล้วยไม้)
WARNING: OOV dictionary entry (evenfall - พลบค่ำ)
WARNING: OOV dictionary entry (scrag - คอ)
WARNING: OOV dictionary entry (gingerroot - ขิง)
WARNING: OOV dictionary entry (tiptop - สุดยอด)
WARNING: OOV dictionary entry (bangle - กำไล)
WARNING: OOV dictionary entry (wazz - รีบ)
WARNING: OOV dictionary entry (burgle - ยกเค้า)
WARNING: OOV dictionary entry (gestate - ตั้งครรภ์)
WARNING: OOV dictionary entry (outmanoeuver - ได้เปรียบ)
WARNING: OOV dictionary entry (joanna - เปียโน)
WARNING: OOV dictionary entry (lollop - เอน)
WARNING: OOV dictionary entry (boisterously - เอะอะ)
WARNING: OOV dictionary entry (pertinacious - ดื้อรั้น)
WARNING: OOV dictionary entry (flummox - สับสน)
WARNING: OOV dictionary entry (copyreader - บรรณาธิการ)
WARNING: OOV dictionary entry (acrobatically - โลดโผน)
WARNING: OOV dictionary entry (rarefy - เบาบาง)
WARNING: OOV dictionary entry (flashily - แปลบ)
WARNING: OOV dictionary entry (yeld - ว่างเปล่า)
WARNING: OOV dictionary entry (flyboy - นักบิน)
WARNING: OOV dictionary entry (springhead - ต้นน้ำ)
WARNING: OOV dictionary entry (thunderclap - ฟ้าผ่า)
WARNING: OOV dictionary entry (yankee - ชาวอเมริกัน)
WARNING: OOV dictionary entry (whomp - ตบ)
WARNING: OOV dictionary entry (maraud - ปล้น)
WARNING: OOV dictionary entry (chuggy - หมากฝรั่ง)
WARNING: OOV dictionary entry (shammy - แชมเปญ)
WARNING: OOV dictionary entry (philanthropical - ใจบุญ)
WARNING: OOV dictionary entry (moonstone - โมรา)
WARNING: OOV dictionary entry (moult - ลอกคราบ)
WARNING: OOV dictionary entry (ackers - เงิน)
WARNING: OOV dictionary entry (gismo - กลไก)
WARNING: OOV dictionary entry (cist - กล่อง)
WARNING: OOV dictionary entry (retrocede - ถอยหลัง)
WARNING: OOV dictionary entry (twangy - อู้อี้)
WARNING: OOV dictionary entry (draggy - เชื่องช้า)
WARNING: OOV dictionary entry (artfulness - กระบวน)
WARNING: OOV dictionary entry (eggbeater - เฮลิคอปเตอร์)
WARNING: OOV dictionary entry (springe - กับดัก)
WARNING: OOV dictionary entry (shillalah - กระบอง)
WARNING: OOV dictionary entry (seahorse - ม้าน้ำ)
WARNING: OOV dictionary entry (heroical - กล้าหาญ)
WARNING: OOV dictionary entry (tumescent - บวม)
WARNING: OOV dictionary entry (undersecretariat - สำนักงานปลัดกระทรวง)
WARNING: OOV dictionary entry (foppery - เสื้อผ้า)
WARNING: OOV dictionary entry (speechlessly - คอแข็ง)
WARNING: OOV dictionary entry (inculpate - กล่าวหา)
WARNING: OOV dictionary entry (roger - ร่วมเพศ)
WARNING: OOV dictionary entry (jobby - ขี้)
WARNING: OOV dictionary entry (voluntaryist - อาสาสมัคร)
WARNING: OOV dictionary entry (conk - จมูก)
WARNING: OOV dictionary entry (butty - แซนด์วิช)
WARNING: OOV dictionary entry (magnific - สง่างาม)
WARNING: OOV dictionary entry (wurst - ไส้กรอก)
WARNING: OOV dictionary entry (emblazon - สัญลักษณ์)
WARNING: OOV dictionary entry (reginae - ราชินี)
WARNING: OOV dictionary entry (transship - ถ่ายเท)
WARNING: OOV dictionary entry (gorgon - น่าเกลียดน่ากลัว)
WARNING: OOV dictionary entry (transfix - ตรึง)
WARNING: OOV dictionary entry (fenestra - หน้าต่าง)
WARNING: OOV dictionary entry (photoplay - ภาพยนตร์)
WARNING: OOV dictionary entry (rozzer - ตำรวจ)
WARNING: OOV dictionary entry (mustachio - หนวด)
WARNING: OOV dictionary entry (gabbin - พูด)
WARNING: OOV dictionary entry (smoulder - กรุ่น)
WARNING: OOV dictionary entry (rabbet - บาก)
WARNING: OOV dictionary entry (squama - สะเก็ด)
WARNING: OOV dictionary entry (popinjay - นกแก้ว)
WARNING: OOV dictionary entry (barmy - บ้า)
WARNING: OOV dictionary entry (gruffly - แหบ)
WARNING: OOV dictionary entry (grandad - ตา)
WARNING: OOV dictionary entry (arris - ก้น)
WARNING: OOV dictionary entry (waggish - ตลกขบขัน)
WARNING: OOV dictionary entry (trencher - เขียง)
WARNING: OOV dictionary entry (neckband - คอเสื้อ)
WARNING: OOV dictionary entry (waff - พัด)
WARNING: OOV dictionary entry (millionairess - เศรษฐีนี)
WARNING: OOV dictionary entry (cozen - หลอกลวง)
WARNING: OOV dictionary entry (grandpapa - ปู่)
WARNING: OOV dictionary entry (gawd - พระเจ้า)
WARNING: OOV dictionary entry (caddish - หยาบคาย)
WARNING: OOV dictionary entry (highjack - รถไฟ)
WARNING: OOV dictionary entry (plonker - งี่เง่า)
WARNING: OOV dictionary entry (kraal - คอก)
WARNING: OOV dictionary entry (garuda - ครุฑ)
WARNING: OOV dictionary entry (riverhead - ต้นน้ำ)
WARNING: OOV dictionary entry (misspend - หมดเปลือง)
WARNING: OOV dictionary entry (gardenia - เหลือง)
WARNING: OOV dictionary entry (telly - ทีวี)
WARNING: OOV dictionary entry (incise - แกะสลัก)
WARNING: OOV dictionary entry (flysheet - ใบปลิว)
WARNING: OOV dictionary entry (porker - หมู)
WARNING: OOV dictionary entry (epicene - อ่อนแอ)
WARNING: OOV dictionary entry (emblazon - รูปภาพ)
WARNING: OOV dictionary entry (criminate - ตำหนิ)
WARNING: OOV dictionary entry (lachrymose - ขี้แย)
WARNING: OOV dictionary entry (braw - ดี)
WARNING: OOV dictionary entry (sigil - เครื่องหมาย)
WARNING: OOV dictionary entry (swinish - หยาบคาย)
WARNING: OOV dictionary entry (myna - นกขุนทอง)
WARNING: OOV dictionary entry (chib - มีด)
WARNING: OOV dictionary entry (whump - ทุบ)
WARNING: OOV dictionary entry (execrate - ประณาม)
WARNING: OOV dictionary entry (cadge - ขอ)
WARNING: OOV dictionary entry (piddle - เสียเวลา)
WARNING: OOV dictionary entry (verruca - หูด)
WARNING: OOV dictionary entry (steffi - หัวเราะ)
WARNING: OOV dictionary entry (piffle - เหลวไหล)
WARNING: OOV dictionary entry (chunder - อ้วก)
WARNING: OOV dictionary entry (nett - ตาข่าย)
WARNING: OOV dictionary entry (skillion - มากมาย)
WARNING: OOV dictionary entry (heehaw - ร้อง)
WARNING: OOV dictionary entry (benzine - เบนซิน)
WARNING: OOV dictionary entry (grouty - อารมณ์เสีย)
WARNING: OOV dictionary entry (stria - ร่อง)
WARNING: OOV dictionary entry (restitute - ชดใช้)
WARNING: OOV dictionary entry (gaur - กระทิง)
WARNING: OOV dictionary entry (gaoler - ผู้คุม)
WARNING: OOV dictionary entry (halberd - ง้าว)
WARNING: OOV dictionary entry (steeve - กระดก)
WARNING: OOV dictionary entry (smoulder - คุกรุ่น)
WARNING: OOV dictionary entry (clearway - ทางด่วน)
WARNING: OOV dictionary entry (brolly - ร่ม)
WARNING: OOV dictionary entry (countlessly - นับไม่ถ้วน)
WARNING: OOV dictionary entry (coco - มะพร้าว)
WARNING: OOV dictionary entry (stria - แถบ)

real	1m23.845s
user	1m32.547s
sys	0m17.594s
prepare folders and cp ... 
mkdir: cannot create directory ‘/media/ye/project2/exp/bilingual-induction/exp1/en-th/vecmap-output16/src_super’: File exists
mkdir: cannot create directory ‘/media/ye/project2/exp/bilingual-induction/exp1/en-th/vecmap-output16/trg_super’: File exists
run vecmap_launcher.py script ...
path:  /media/ye/project2/exp/bilingual-induction/exp1/en-th/vecmap-output16/src_super/word2vec_s500_mc2_w4.vec
path:  /media/ye/project2/exp/bilingual-induction/exp1/en-th/vecmap-output16/trg_super/word2vec_s500_mc2_w4.vec
EN:  /media/ye/project2/exp/bilingual-induction/exp1/en-th/vecmap-output16/src_super/word2vec_s500_mc2_w4.vec
WEL:  /media/ye/project2/exp/bilingual-induction/exp1/en-th/vecmap-output16/trg_super/word2vec_s500_mc2_w4.vec
=== CMD ===
python3 vecmap/map_embeddings.py --supervised /media/ye/project2/exp/bilingual-induction/exp1/en-th/word2vec-output16/train_dict.csv "/media/ye/project2/exp/bilingual-induction/exp1/en-th/vecmap-output16/src_super/word2vec_s500_mc2_w4.vec" "/media/ye/project2/exp/bilingual-induction/exp1/en-th/vecmap-output16/trg_super/word2vec_s500_mc2_w4.vec" "/media/ye/project2/exp/bilingual-induction/exp1/en-th/vecmap-output16/src_super/word2vec_s500_mc2_w4.vec_mapped.vec" "/media/ye/project2/exp/bilingual-induction/exp1/en-th/vecmap-output16/trg_super/word2vec_s500_mc2_w4.vec_mapped.vec"
WARNING: OOV dictionary entry (english - welsh)
WARNING: OOV dictionary entry (palindrome - หลัง)
WARNING: OOV dictionary entry (peregrinate - เดินทาง)
WARNING: OOV dictionary entry (zonk - หมดสติ)
WARNING: OOV dictionary entry (snick - เล็ม)
WARNING: OOV dictionary entry (airdrome - สนามบิน)
WARNING: OOV dictionary entry (minimart - มินิมาร์ท)
WARNING: OOV dictionary entry (soothsay - ทำนาย)
WARNING: OOV dictionary entry (henpeck - ด่าว่า)
WARNING: OOV dictionary entry (whirlybird - เฮลิคอปเตอร์)
WARNING: OOV dictionary entry (malmsey - เหล้าองุ่น)
WARNING: OOV dictionary entry (baccy - บุหรี่)
WARNING: OOV dictionary entry (madden - บ้า)
WARNING: OOV dictionary entry (ruck - ต่อสู้)
WARNING: OOV dictionary entry (nippy - จัดจ้าน)
WARNING: OOV dictionary entry (indite - ประพันธ์)
WARNING: OOV dictionary entry (bonzo - บ้า)
WARNING: OOV dictionary entry (submerse - จุ่ม)
WARNING: OOV dictionary entry (lithesome - อ่อนช้อย)
WARNING: OOV dictionary entry (pinstriper - นักธุรกิจ)
WARNING: OOV dictionary entry (dipper - จวัก)
WARNING: OOV dictionary entry (tomtit - อึ)
WARNING: OOV dictionary entry (culantro - ผักชีฝรั่ง)
WARNING: OOV dictionary entry (reenforce - เสริม)
WARNING: OOV dictionary entry (resentfully - ตาขวาง)
WARNING: OOV dictionary entry (headspring - ต้นน้ำ)
WARNING: OOV dictionary entry (quaver - สั่น)
WARNING: OOV dictionary entry (tike - สุนัข)
WARNING: OOV dictionary entry (manful - กล้าหาญ)
WARNING: OOV dictionary entry (desperado - อาชญากร)
WARNING: OOV dictionary entry (louvre - บานเกล็ด)
WARNING: OOV dictionary entry (jessamine - มะลิ)
WARNING: OOV dictionary entry (tegument - เปลือก)
WARNING: OOV dictionary entry (cancellate - บาง)
WARNING: OOV dictionary entry (sermonize - เทศนา)
WARNING: OOV dictionary entry (niter - ดินประสิว)
WARNING: OOV dictionary entry (ligate - ผูก)
WARNING: OOV dictionary entry (gingiva - เหงือก)
WARNING: OOV dictionary entry (stabile - มั่นคง)
WARNING: OOV dictionary entry (dosh - เงิน)
WARNING: OOV dictionary entry (blandish - ปากหวาน)
WARNING: OOV dictionary entry (whelm - ครอบงำ)
WARNING: OOV dictionary entry (overjoy - ลิงโลด)
WARNING: OOV dictionary entry (glitteringly - วับแวม)
WARNING: OOV dictionary entry (peckish - หิว)
WARNING: OOV dictionary entry (abominate - ชิงชัง)
WARNING: OOV dictionary entry (hexapod - แมลง)
WARNING: OOV dictionary entry (chippy - โสเภณี)
WARNING: OOV dictionary entry (jillion - มากมาย)
WARNING: OOV dictionary entry (brill - สุดยอด)
WARNING: OOV dictionary entry (oldish - แก่)
WARNING: OOV dictionary entry (parboil - ลวก)
WARNING: OOV dictionary entry (sweepingly - กราด)
WARNING: OOV dictionary entry (trustfully - สนิทใจ)
WARNING: OOV dictionary entry (psammite - หินทราย)
WARNING: OOV dictionary entry (knackered - เสีย)
WARNING: OOV dictionary entry (nacre - ไข่มุก)
WARNING: OOV dictionary entry (faff - จู้จี้)
WARNING: OOV dictionary entry (earplug - อากาศ)
WARNING: OOV dictionary entry (shallot - หอม)
WARNING: OOV dictionary entry (highjack - เรือ)
WARNING: OOV dictionary entry (marge - ริม)
WARNING: OOV dictionary entry (langur - ค่าง)
WARNING: OOV dictionary entry (sparge - พรม)
WARNING: OOV dictionary entry (baboo - นาย)
WARNING: OOV dictionary entry (nark - รบกวน)
WARNING: OOV dictionary entry (boodie - ก้น)
WARNING: OOV dictionary entry (konk - หัว)
WARNING: OOV dictionary entry (spatter - กระเด็น)
WARNING: OOV dictionary entry (cank - จ้อ)
WARNING: OOV dictionary entry (nim - สะเดา)
WARNING: OOV dictionary entry (ruffly - กระเพื่อม)
WARNING: OOV dictionary entry (ranee - ราชินี)
WARNING: OOV dictionary entry (bate - ลด)
WARNING: OOV dictionary entry (scurf - สะเก็ด)
WARNING: OOV dictionary entry (taters - มันฝรั่ง)
WARNING: OOV dictionary entry (boody - ก้น)
WARNING: OOV dictionary entry (scutcheon - โล่)
WARNING: OOV dictionary entry (grizzle - ขาว)
WARNING: OOV dictionary entry (middlebrow - สามัญ)
WARNING: OOV dictionary entry (persimmon - พลับ)
WARNING: OOV dictionary entry (padre - บาทหลวง)
WARNING: OOV dictionary entry (champaign - ที่ราบ)
WARNING: OOV dictionary entry (tauten - ตึง)
WARNING: OOV dictionary entry (regina - ราชินี)
WARNING: OOV dictionary entry (snoot - จมูก)
WARNING: OOV dictionary entry (tremblingly - สั่น)
WARNING: OOV dictionary entry (bate - อดกลั้น)
WARNING: OOV dictionary entry (pernickety - จู้จี้)
WARNING: OOV dictionary entry (seclude - แยกตัว)
WARNING: OOV dictionary entry (grandmamma - ยาย)
WARNING: OOV dictionary entry (hallo - ร้องเรียก)
WARNING: OOV dictionary entry (tabor - ตะโพน)
WARNING: OOV dictionary entry (gride - ครูด)
WARNING: OOV dictionary entry (kvetch - บ่น)
WARNING: OOV dictionary entry (adventurously - ผาดโผน)
WARNING: OOV dictionary entry (corking - สุดยอด)
WARNING: OOV dictionary entry (madden - คลั่ง)
WARNING: OOV dictionary entry (logy - เฉื่อยชา)
WARNING: OOV dictionary entry (kak - อึ)
WARNING: OOV dictionary entry (waspish - เจ้าอารมณ์)
WARNING: OOV dictionary entry (protuberant - โหนก)
WARNING: OOV dictionary entry (gallinaceous - ไก่)
WARNING: OOV dictionary entry (cockscomb - หงอนไก่)
WARNING: OOV dictionary entry (musjid - มัสยิด)
WARNING: OOV dictionary entry (boku - มาก)
WARNING: OOV dictionary entry (thunderbox - ห้องส้วม)
WARNING: OOV dictionary entry (mingy - ขี้เหนียว)
WARNING: OOV dictionary entry (guv’nor - เจ้านาย)
WARNING: OOV dictionary entry (rambutan - เงาะ)
WARNING: OOV dictionary entry (sobbingly - กระซิก)
WARNING: OOV dictionary entry (trolly - รถเข็น)
WARNING: OOV dictionary entry (noddle - หัว)
WARNING: OOV dictionary entry (muskmelon - แตงไทย)
WARNING: OOV dictionary entry (razz - หยอกล้อ)
WARNING: OOV dictionary entry (gateau - เค้ก)
WARNING: OOV dictionary entry (punctiliously - พิถีพิถัน)
WARNING: OOV dictionary entry (coxcomb - หงอนไก่)
WARNING: OOV dictionary entry (lade - บรรทุก)
WARNING: OOV dictionary entry (charbroil - ต้ม)
WARNING: OOV dictionary entry (retroact - โต้ตอบ)
WARNING: OOV dictionary entry (shillelagh - กระบอง)
WARNING: OOV dictionary entry (tremblingly - ระรัว)
WARNING: OOV dictionary entry (pukka - แท้)
WARNING: OOV dictionary entry (tatter - ผ้าขี้ริ้ว)
WARNING: OOV dictionary entry (semblable - คล้าย)
WARNING: OOV dictionary entry (bawd - โสเภณี)
WARNING: OOV dictionary entry (lightsome - ร่าเริง)
WARNING: OOV dictionary entry (banger - ไส้กรอก)
WARNING: OOV dictionary entry (vapourize - ระเหย)
WARNING: OOV dictionary entry (datura - ลำโพง)
WARNING: OOV dictionary entry (jape - เยาะเย้ย)
WARNING: OOV dictionary entry (dearie - ที่รัก)
WARNING: OOV dictionary entry (grandmamma - ย่า)
WARNING: OOV dictionary entry (melodiously - แจ้ว)
WARNING: OOV dictionary entry (gammon - โกง)
WARNING: OOV dictionary entry (lichi - ลิ้นจี่)
WARNING: OOV dictionary entry (unfix - ปลด)
WARNING: OOV dictionary entry (ramie - ป่าน)
WARNING: OOV dictionary entry (prexy - ประธาน)
WARNING: OOV dictionary entry (baluster - กรง)
WARNING: OOV dictionary entry (yaws - คุดทะราด)
WARNING: OOV dictionary entry (wizen - เหี่ยวแห้ง)
WARNING: OOV dictionary entry (zonk - ตี)
WARNING: OOV dictionary entry (viand - อาหาร)
WARNING: OOV dictionary entry (distend - อืด)
WARNING: OOV dictionary entry (gravid - ตั้งครรภ์)
WARNING: OOV dictionary entry (pulverise - โขลก)
WARNING: OOV dictionary entry (corsair - โจรสลัด)
WARNING: OOV dictionary entry (argosy - ตะเภา)
WARNING: OOV dictionary entry (gateaux - เค้ก)
WARNING: OOV dictionary entry (gammon - แฮม)
WARNING: OOV dictionary entry (lattermost - ล่าสุด)
WARNING: OOV dictionary entry (cakehole - ปาก)
WARNING: OOV dictionary entry (underripe - ห่าม)
WARNING: OOV dictionary entry (lutist - เวณิก)
WARNING: OOV dictionary entry (bewitchingly - เปรี้ยว)
WARNING: OOV dictionary entry (bombardier - ปืนใหญ่)
WARNING: OOV dictionary entry (grannie - ย่า)
WARNING: OOV dictionary entry (blenny - ตีน)
WARNING: OOV dictionary entry (spoony - คลั่งไคล้)
WARNING: OOV dictionary entry (tutti - ทั้งหมด)
WARNING: OOV dictionary entry (helve - ด้าม)
WARNING: OOV dictionary entry (wazz - ฉี่)
WARNING: OOV dictionary entry (indurate - แข็ง)
WARNING: OOV dictionary entry (taters - หนาวเย็น)
WARNING: OOV dictionary entry (famish - อดอยาก)
WARNING: OOV dictionary entry (whup - เฆี่ยน)
WARNING: OOV dictionary entry (myrobalan - สมอ)
WARNING: OOV dictionary entry (phyle - ชนชาติ)
WARNING: OOV dictionary entry (thuddingly - กุบกับ)
WARNING: OOV dictionary entry (chokey - คุก)
WARNING: OOV dictionary entry (springhead - ต้นกำเนิด)
WARNING: OOV dictionary entry (tremblingly - เร่า)
WARNING: OOV dictionary entry (cloy - เอียน)
WARNING: OOV dictionary entry (abloom - บาน)
WARNING: OOV dictionary entry (comestible - อาหาร)
WARNING: OOV dictionary entry (vocable - คำ)
WARNING: OOV dictionary entry (dicky - อ่อนแอ)
WARNING: OOV dictionary entry (ropey - ป่วย)
WARNING: OOV dictionary entry (proteid - โปรตีน)
WARNING: OOV dictionary entry (lour - มืดครึ้ม)
WARNING: OOV dictionary entry (granger - ชาวนา)
WARNING: OOV dictionary entry (earthman - มนุษย์)
WARNING: OOV dictionary entry (blooey - เสียหาย)
WARNING: OOV dictionary entry (fila - เส้นใย)
WARNING: OOV dictionary entry (smoulder - คั่งแค้น)
WARNING: OOV dictionary entry (unbridle - ปลดปล่อย)
WARNING: OOV dictionary entry (lave - ล้าง)
WARNING: OOV dictionary entry (gobsmacked - ประหลาดใจ)
WARNING: OOV dictionary entry (burgle - บ้าน)
WARNING: OOV dictionary entry (smoulder - อัดอั้น)
WARNING: OOV dictionary entry (unsmooth - ฝืด)
WARNING: OOV dictionary entry (fitba - ฟุตบอล)
WARNING: OOV dictionary entry (superfine - ดีเยี่ยม)
WARNING: OOV dictionary entry (fantasise - จินตนาการ)
WARNING: OOV dictionary entry (cutty - สั้น)
WARNING: OOV dictionary entry (drat - สับสน)
WARNING: OOV dictionary entry (intonate - สวดมนต์)
WARNING: OOV dictionary entry (uncourtly - หยาบ)
WARNING: OOV dictionary entry (bazoo - ปาก)
WARNING: OOV dictionary entry (drub - ตี)
WARNING: OOV dictionary entry (drub - เอาชนะ)
WARNING: OOV dictionary entry (surcease - เลิก)
WARNING: OOV dictionary entry (grandpapa - ตา)
WARNING: OOV dictionary entry (brewster - เบียร์)
WARNING: OOV dictionary entry (summersault - ตีลังกา)
WARNING: OOV dictionary entry (vivisect - ชำแหละ)
WARNING: OOV dictionary entry (enceinte - ตั้งครรภ์)
WARNING: OOV dictionary entry (contuse - ฟกช้ำ)
WARNING: OOV dictionary entry (emmet - นักท่องเที่ยว)
WARNING: OOV dictionary entry (slimline - บอบบาง)
WARNING: OOV dictionary entry (slattern - โสเภณี)
WARNING: OOV dictionary entry (mooch - ขโมย)
WARNING: OOV dictionary entry (brokenly - กระท่อนกระแท่น)
WARNING: OOV dictionary entry (gamecock - ไก่ชน)
WARNING: OOV dictionary entry (eldritch - ประหลาด)
WARNING: OOV dictionary entry (percuss - เคาะ)
WARNING: OOV dictionary entry (deva - พระเจ้า)
WARNING: OOV dictionary entry (conjuration - เวทมนตร์)
WARNING: OOV dictionary entry (animadvert - วิจารณ์)
WARNING: OOV dictionary entry (varda - มอง)
WARNING: OOV dictionary entry (swop - แลกเปลี่ยน)
WARNING: OOV dictionary entry (steeve - อัด)
WARNING: OOV dictionary entry (rotorhead - นักบิน)
WARNING: OOV dictionary entry (khazi - ส้วม)
WARNING: OOV dictionary entry (tiffin - ปิ่นโต)
WARNING: OOV dictionary entry (ket - ลูกอม)
WARNING: OOV dictionary entry (waitperson - บริกร)
WARNING: OOV dictionary entry (boisterously - ปึงปัง)
WARNING: OOV dictionary entry (spicula - หนาม)
WARNING: OOV dictionary entry (pyknic - อ้วน)
WARNING: OOV dictionary entry (unsharpened - ทู่)
WARNING: OOV dictionary entry (sailer - เรือใบ)
WARNING: OOV dictionary entry (ruck - ยับ)
WARNING: OOV dictionary entry (thirl - เจาะ)
WARNING: OOV dictionary entry (largehearted - ใจดี)
WARNING: OOV dictionary entry (gesticulate - โบกไม้โบกมือ)
WARNING: OOV dictionary entry (sonance - เสียง)
WARNING: OOV dictionary entry (marihuana - กัญชา)
WARNING: OOV dictionary entry (telly - โทรทัศน์)
WARNING: OOV dictionary entry (inveterately - งอมแงม)
WARNING: OOV dictionary entry (freebee - เสรีภาพ)
WARNING: OOV dictionary entry (truncheon - กระบอง)
WARNING: OOV dictionary entry (earplug - เสียง)
WARNING: OOV dictionary entry (diphthong - ควบกล้ำ)
WARNING: OOV dictionary entry (bedeck - ประดับประดา)
WARNING: OOV dictionary entry (lurcher - ขโมย)
WARNING: OOV dictionary entry (crunchie - ทหาร)
WARNING: OOV dictionary entry (tatty - หยาบ)
WARNING: OOV dictionary entry (pintle - เดือย)
WARNING: OOV dictionary entry (lumpish - อืดอาด)
WARNING: OOV dictionary entry (freeby - เสรีภาพ)
WARNING: OOV dictionary entry (uncloak - เปิดเผย)
WARNING: OOV dictionary entry (brill - ดีมาก)
WARNING: OOV dictionary entry (boozer - ผับ)
WARNING: OOV dictionary entry (advertent - สนใจ)
WARNING: OOV dictionary entry (maestoso - ผึ่งผาย)
WARNING: OOV dictionary entry (wonga - เงิน)
WARNING: OOV dictionary entry (overmaster - ครอบงำ)
WARNING: OOV dictionary entry (cocoanut - มะพร้าว)
WARNING: OOV dictionary entry (unclose - เปิด)
WARNING: OOV dictionary entry (florae - พืชพรรณ)
WARNING: OOV dictionary entry (motionlessly - แอ้งแม้ง)
WARNING: OOV dictionary entry (crotchet - ตะขอ)
WARNING: OOV dictionary entry (pother - ยุ่งเหยิง)
WARNING: OOV dictionary entry (doorsill - ธรณีประตู)
WARNING: OOV dictionary entry (splashboard - กันสาด)
WARNING: OOV dictionary entry (slantwise - เอียง)
WARNING: OOV dictionary entry (inhabitancy - ที่อยู่อาศัย)
WARNING: OOV dictionary entry (ubosot - อุโบสถ)
WARNING: OOV dictionary entry (wame - ท้อง)
WARNING: OOV dictionary entry (interlard - สอดแทรก)
WARNING: OOV dictionary entry (braise - เคี่ยว)
WARNING: OOV dictionary entry (asafetida - มหาหิงคุ์)
WARNING: OOV dictionary entry (faubourg - ชานเมือง)
WARNING: OOV dictionary entry (summerset - ตีลังกา)
WARNING: OOV dictionary entry (carambola - มะเฟือง)
WARNING: OOV dictionary entry (hankie - ผ้าเช็ดหน้า)
WARNING: OOV dictionary entry (triggerman - มือปืน)
WARNING: OOV dictionary entry (serration - ปากฉลาม)
WARNING: OOV dictionary entry (tiddly - เล็กน้อย)
WARNING: OOV dictionary entry (incise - ผ่าตัด)
WARNING: OOV dictionary entry (papilla - หัวนม)
WARNING: OOV dictionary entry (chinky - เจ๊ก)
WARNING: OOV dictionary entry (vitamine - วิตามิน)
WARNING: OOV dictionary entry (dissimulate - ปิดบัง)
WARNING: OOV dictionary entry (chavvy - เด็ก)
WARNING: OOV dictionary entry (modish - ทันสมัย)
WARNING: OOV dictionary entry (homie - เพื่อน)
WARNING: OOV dictionary entry (kris - กริช)
WARNING: OOV dictionary entry (maleficent - ชั่วร้าย)
WARNING: OOV dictionary entry (univalent - เดี่ยว)
WARNING: OOV dictionary entry (nauseate - คลื่นไส้)
WARNING: OOV dictionary entry (hunchbacked - ค่อม)
WARNING: OOV dictionary entry (brewski - เบียร์)
WARNING: OOV dictionary entry (resect - ชำแหละ)
WARNING: OOV dictionary entry (epiphyte - เฟิร์น)
WARNING: OOV dictionary entry (camelopard - ยีราฟ)
WARNING: OOV dictionary entry (wive - แต่งงาน)
WARNING: OOV dictionary entry (rollick - กระโดดโลดเต้น)
WARNING: OOV dictionary entry (meliorate - บรรเทา)
WARNING: OOV dictionary entry (pulchritudinous - สวย)
WARNING: OOV dictionary entry (agley - บิด)
WARNING: OOV dictionary entry (peevishly - กระเง้ากระงอด)
WARNING: OOV dictionary entry (kiester - ก้น)
WARNING: OOV dictionary entry (strop - สาย)
WARNING: OOV dictionary entry (hackle - หวี)
WARNING: OOV dictionary entry (scurf - รังแค)
WARNING: OOV dictionary entry (tomtom - เถิดเทิง)
WARNING: OOV dictionary entry (entwine - พัวพัน)
WARNING: OOV dictionary entry (weatherboard - กันสาด)
WARNING: OOV dictionary entry (solitarily - เดียวดาย)
WARNING: OOV dictionary entry (bazoo - ท้อง)
WARNING: OOV dictionary entry (longan - ลำไย)
WARNING: OOV dictionary entry (gib - ลิ่ม)
WARNING: OOV dictionary entry (moggie - แมว)
WARNING: OOV dictionary entry (palfrey - ม้า)
WARNING: OOV dictionary entry (manoeuver - กลยุทธ์)
WARNING: OOV dictionary entry (sodbuster - ชาวนา)
WARNING: OOV dictionary entry (bootie - ก้น)
WARNING: OOV dictionary entry (sarky - เสียดสี)
WARNING: OOV dictionary entry (clarty - สกปรก)
WARNING: OOV dictionary entry (gourami - ใบไม้)
WARNING: OOV dictionary entry (argosy - สำเภา)
WARNING: OOV dictionary entry (ravel - ยุ่งเหยิง)
WARNING: OOV dictionary entry (venge - แก้แค้น)
WARNING: OOV dictionary entry (preterit - อดีตกาล)
WARNING: OOV dictionary entry (gran - ยาย)
WARNING: OOV dictionary entry (mickle - มาก)
WARNING: OOV dictionary entry (rani - ราชินี)
WARNING: OOV dictionary entry (pretermit - ละทิ้ง)
WARNING: OOV dictionary entry (billie - แบงค์)
WARNING: OOV dictionary entry (peculate - ยักยอก)
WARNING: OOV dictionary entry (overcloud - มืดมัว)
WARNING: OOV dictionary entry (waspy - เจ้าอารมณ์)
WARNING: OOV dictionary entry (cank - เม้าท์)
WARNING: OOV dictionary entry (parky - หนาวเย็น)
WARNING: OOV dictionary entry (magnetize - ดึงดูดใจ)
WARNING: OOV dictionary entry (meshugah - บ้า)
WARNING: OOV dictionary entry (lissome - คล่องแคล่ว)
WARNING: OOV dictionary entry (rugose - ย่น)
WARNING: OOV dictionary entry (labium - ริมฝีปาก)
WARNING: OOV dictionary entry (grannie - ยาย)
WARNING: OOV dictionary entry (whiffle - รวนเร)
WARNING: OOV dictionary entry (guber - เนื้องอก)
WARNING: OOV dictionary entry (hardhearted - โหดร้าย)
WARNING: OOV dictionary entry (translocate - โยกย้าย)
WARNING: OOV dictionary entry (snoot - ดูถูก)
WARNING: OOV dictionary entry (bijou - เพชร)
WARNING: OOV dictionary entry (pule - คร่ำครวญ)
WARNING: OOV dictionary entry (sparge - ประปราย)
WARNING: OOV dictionary entry (appendent - ผนวก)
WARNING: OOV dictionary entry (magnetise - ดึงดูดใจ)
WARNING: OOV dictionary entry (shipside - ท่าเรือ)
WARNING: OOV dictionary entry (reave - แย่ง)
WARNING: OOV dictionary entry (yammer - คราง)
WARNING: OOV dictionary entry (coquet - ยั่วยวน)
WARNING: OOV dictionary entry (sourish - เปรี้ยว)
WARNING: OOV dictionary entry (glim - แหล่ง)
WARNING: OOV dictionary entry (eidolon - ผี)
WARNING: OOV dictionary entry (roister - เอะอะโวยวาย)
WARNING: OOV dictionary entry (stang - สตางค์)
WARNING: OOV dictionary entry (chuddy - หมากฝรั่ง)
WARNING: OOV dictionary entry (indistinctively - กำปั้นทุบดิน)
WARNING: OOV dictionary entry (melodiously - เจื้อยแจ้ว)
WARNING: OOV dictionary entry (wilfull - ดื้อดึง)
WARNING: OOV dictionary entry (skene - กริช)
WARNING: OOV dictionary entry (finical - จุกจิก)
WARNING: OOV dictionary entry (tumid - บวม)
WARNING: OOV dictionary entry (copter - เฮลิคอปเตอร์)
WARNING: OOV dictionary entry (stymy - ขัดขวาง)
WARNING: OOV dictionary entry (aks - ถาม)
WARNING: OOV dictionary entry (rumple - ยับ)
WARNING: OOV dictionary entry (swaddle - พัน)
WARNING: OOV dictionary entry (pushchair - รถเข็น)
WARNING: OOV dictionary entry (spathe - กาบ)
WARNING: OOV dictionary entry (spatter - กระเซ็น)
WARNING: OOV dictionary entry (chivvy - ไล่ล่า)
WARNING: OOV dictionary entry (anear - ใกล้)
WARNING: OOV dictionary entry (redskin - อินเดียนแดง)
WARNING: OOV dictionary entry (unfetter - ปลดปล่อย)
WARNING: OOV dictionary entry (sawbones - ศัลยแพทย์)
WARNING: OOV dictionary entry (immure - กักขัง)
WARNING: OOV dictionary entry (quirt - แส้)
WARNING: OOV dictionary entry (kraal - หมู่บ้าน)
WARNING: OOV dictionary entry (perfuse - พรม)
WARNING: OOV dictionary entry (untidily - รกเรื้อ)
WARNING: OOV dictionary entry (declamatory - ฉะฉาน)
WARNING: OOV dictionary entry (scurf - ไคล)
WARNING: OOV dictionary entry (bazoo - ก้น)
WARNING: OOV dictionary entry (outmanoeuvre - ได้เปรียบ)
WARNING: OOV dictionary entry (pukka - ของแท้)
WARNING: OOV dictionary entry (strickle - ปาด)
WARNING: OOV dictionary entry (kouprey - กูปรี)
WARNING: OOV dictionary entry (globefish - ปักเป้า)
WARNING: OOV dictionary entry (whelm - ท่วม)
WARNING: OOV dictionary entry (zeds - หลับ)
WARNING: OOV dictionary entry (cack - อึ)
WARNING: OOV dictionary entry (moggy - แมว)
WARNING: OOV dictionary entry (pedagog - อาจารย์)
WARNING: OOV dictionary entry (phonate - ออกเสียง)
WARNING: OOV dictionary entry (macerate - เปื่อย)
WARNING: OOV dictionary entry (toffy - ลูกอม)
WARNING: OOV dictionary entry (epiphyte - กล้วยไม้)
WARNING: OOV dictionary entry (evenfall - พลบค่ำ)
WARNING: OOV dictionary entry (scrag - คอ)
WARNING: OOV dictionary entry (gingerroot - ขิง)
WARNING: OOV dictionary entry (tiptop - สุดยอด)
WARNING: OOV dictionary entry (bangle - กำไล)
WARNING: OOV dictionary entry (wazz - รีบ)
WARNING: OOV dictionary entry (burgle - ยกเค้า)
WARNING: OOV dictionary entry (gestate - ตั้งครรภ์)
WARNING: OOV dictionary entry (outmanoeuver - ได้เปรียบ)
WARNING: OOV dictionary entry (joanna - เปียโน)
WARNING: OOV dictionary entry (lollop - เอน)
WARNING: OOV dictionary entry (boisterously - เอะอะ)
WARNING: OOV dictionary entry (pertinacious - ดื้อรั้น)
WARNING: OOV dictionary entry (flummox - สับสน)
WARNING: OOV dictionary entry (copyreader - บรรณาธิการ)
WARNING: OOV dictionary entry (acrobatically - โลดโผน)
WARNING: OOV dictionary entry (rarefy - เบาบาง)
WARNING: OOV dictionary entry (flashily - แปลบ)
WARNING: OOV dictionary entry (yeld - ว่างเปล่า)
WARNING: OOV dictionary entry (flyboy - นักบิน)
WARNING: OOV dictionary entry (springhead - ต้นน้ำ)
WARNING: OOV dictionary entry (thunderclap - ฟ้าผ่า)
WARNING: OOV dictionary entry (yankee - ชาวอเมริกัน)
WARNING: OOV dictionary entry (whomp - ตบ)
WARNING: OOV dictionary entry (maraud - ปล้น)
WARNING: OOV dictionary entry (chuggy - หมากฝรั่ง)
WARNING: OOV dictionary entry (shammy - แชมเปญ)
WARNING: OOV dictionary entry (philanthropical - ใจบุญ)
WARNING: OOV dictionary entry (moonstone - โมรา)
WARNING: OOV dictionary entry (moult - ลอกคราบ)
WARNING: OOV dictionary entry (ackers - เงิน)
WARNING: OOV dictionary entry (gismo - กลไก)
WARNING: OOV dictionary entry (cist - กล่อง)
WARNING: OOV dictionary entry (retrocede - ถอยหลัง)
WARNING: OOV dictionary entry (twangy - อู้อี้)
WARNING: OOV dictionary entry (draggy - เชื่องช้า)
WARNING: OOV dictionary entry (artfulness - กระบวน)
WARNING: OOV dictionary entry (eggbeater - เฮลิคอปเตอร์)
WARNING: OOV dictionary entry (springe - กับดัก)
WARNING: OOV dictionary entry (shillalah - กระบอง)
WARNING: OOV dictionary entry (seahorse - ม้าน้ำ)
WARNING: OOV dictionary entry (heroical - กล้าหาญ)
WARNING: OOV dictionary entry (tumescent - บวม)
WARNING: OOV dictionary entry (undersecretariat - สำนักงานปลัดกระทรวง)
WARNING: OOV dictionary entry (foppery - เสื้อผ้า)
WARNING: OOV dictionary entry (speechlessly - คอแข็ง)
WARNING: OOV dictionary entry (inculpate - กล่าวหา)
WARNING: OOV dictionary entry (roger - ร่วมเพศ)
WARNING: OOV dictionary entry (jobby - ขี้)
WARNING: OOV dictionary entry (voluntaryist - อาสาสมัคร)
WARNING: OOV dictionary entry (conk - จมูก)
WARNING: OOV dictionary entry (butty - แซนด์วิช)
WARNING: OOV dictionary entry (magnific - สง่างาม)
WARNING: OOV dictionary entry (wurst - ไส้กรอก)
WARNING: OOV dictionary entry (emblazon - สัญลักษณ์)
WARNING: OOV dictionary entry (reginae - ราชินี)
WARNING: OOV dictionary entry (transship - ถ่ายเท)
WARNING: OOV dictionary entry (gorgon - น่าเกลียดน่ากลัว)
WARNING: OOV dictionary entry (transfix - ตรึง)
WARNING: OOV dictionary entry (fenestra - หน้าต่าง)
WARNING: OOV dictionary entry (photoplay - ภาพยนตร์)
WARNING: OOV dictionary entry (rozzer - ตำรวจ)
WARNING: OOV dictionary entry (mustachio - หนวด)
WARNING: OOV dictionary entry (gabbin - พูด)
WARNING: OOV dictionary entry (smoulder - กรุ่น)
WARNING: OOV dictionary entry (rabbet - บาก)
WARNING: OOV dictionary entry (squama - สะเก็ด)
WARNING: OOV dictionary entry (popinjay - นกแก้ว)
WARNING: OOV dictionary entry (barmy - บ้า)
WARNING: OOV dictionary entry (gruffly - แหบ)
WARNING: OOV dictionary entry (grandad - ตา)
WARNING: OOV dictionary entry (arris - ก้น)
WARNING: OOV dictionary entry (waggish - ตลกขบขัน)
WARNING: OOV dictionary entry (trencher - เขียง)
WARNING: OOV dictionary entry (neckband - คอเสื้อ)
WARNING: OOV dictionary entry (waff - พัด)
WARNING: OOV dictionary entry (millionairess - เศรษฐีนี)
WARNING: OOV dictionary entry (cozen - หลอกลวง)
WARNING: OOV dictionary entry (grandpapa - ปู่)
WARNING: OOV dictionary entry (gawd - พระเจ้า)
WARNING: OOV dictionary entry (caddish - หยาบคาย)
WARNING: OOV dictionary entry (highjack - รถไฟ)
WARNING: OOV dictionary entry (plonker - งี่เง่า)
WARNING: OOV dictionary entry (kraal - คอก)
WARNING: OOV dictionary entry (garuda - ครุฑ)
WARNING: OOV dictionary entry (riverhead - ต้นน้ำ)
WARNING: OOV dictionary entry (misspend - หมดเปลือง)
WARNING: OOV dictionary entry (gardenia - เหลือง)
WARNING: OOV dictionary entry (telly - ทีวี)
WARNING: OOV dictionary entry (incise - แกะสลัก)
WARNING: OOV dictionary entry (flysheet - ใบปลิว)
WARNING: OOV dictionary entry (porker - หมู)
WARNING: OOV dictionary entry (epicene - อ่อนแอ)
WARNING: OOV dictionary entry (emblazon - รูปภาพ)
WARNING: OOV dictionary entry (criminate - ตำหนิ)
WARNING: OOV dictionary entry (lachrymose - ขี้แย)
WARNING: OOV dictionary entry (braw - ดี)
WARNING: OOV dictionary entry (sigil - เครื่องหมาย)
WARNING: OOV dictionary entry (swinish - หยาบคาย)
WARNING: OOV dictionary entry (myna - นกขุนทอง)
WARNING: OOV dictionary entry (chib - มีด)
WARNING: OOV dictionary entry (whump - ทุบ)
WARNING: OOV dictionary entry (execrate - ประณาม)
WARNING: OOV dictionary entry (cadge - ขอ)
WARNING: OOV dictionary entry (piddle - เสียเวลา)
WARNING: OOV dictionary entry (verruca - หูด)
WARNING: OOV dictionary entry (steffi - หัวเราะ)
WARNING: OOV dictionary entry (piffle - เหลวไหล)
WARNING: OOV dictionary entry (chunder - อ้วก)
WARNING: OOV dictionary entry (nett - ตาข่าย)
WARNING: OOV dictionary entry (skillion - มากมาย)
WARNING: OOV dictionary entry (heehaw - ร้อง)
WARNING: OOV dictionary entry (benzine - เบนซิน)
WARNING: OOV dictionary entry (grouty - อารมณ์เสีย)
WARNING: OOV dictionary entry (stria - ร่อง)
WARNING: OOV dictionary entry (restitute - ชดใช้)
WARNING: OOV dictionary entry (gaur - กระทิง)
WARNING: OOV dictionary entry (gaoler - ผู้คุม)
WARNING: OOV dictionary entry (halberd - ง้าว)
WARNING: OOV dictionary entry (steeve - กระดก)
WARNING: OOV dictionary entry (smoulder - คุกรุ่น)
WARNING: OOV dictionary entry (clearway - ทางด่วน)
WARNING: OOV dictionary entry (brolly - ร่ม)
WARNING: OOV dictionary entry (countlessly - นับไม่ถ้วน)
WARNING: OOV dictionary entry (coco - มะพร้าว)
WARNING: OOV dictionary entry (stria - แถบ)
/media/ye/project2/exp/bilingual-induction/exp1/en-th/vecmap-output16/
├── src_mapped_supervised.emb
├── src_super
│   ├── word2vec_s500_mc2_w4.vec
│   └── word2vec_s500_mc2_w4.vec_mapped.vec
├── trg_mapped_supervised.emb
└── trg_super
    ├── word2vec_s500_mc2_w4.vec
    └── word2vec_s500_mc2_w4.vec_mapped.vec

2 directories, 6 files
Evaluation ... 
--retrieval nn:
Coverage: 95.55%  Accuracy:  4.12%

real	0m20.729s
user	0m20.806s
sys	0m5.818s
--retrieval invnn:
Coverage: 95.55%  Accuracy:  2.86%

real	34m28.491s
user	35m44.256s
sys	3m22.307s
--retrieval invsoftmax:
Coverage: 95.55%  Accuracy:  4.35%

real	2m8.583s
user	9m3.169s
sys	4m31.295s
--retrieval csls:
Coverage: 95.55%  Accuracy:  5.07%

real	2m56.585s
user	6m28.570s
sys	1m29.045s

real	78m0.185s
user	126m42.866s
sys	10m29.582s
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$
```
