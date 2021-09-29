# Full Running Log of Bi-lingual Embedding for Myanmar-English

```
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ time ./repeat-train-eval-myen.sh 200 3 2 10 10 my en
build word2vec or fasttext model ...
change python environment...
start building a word2vec model for SRC language ...  
2021-09-29 15:45:24,366 : INFO : collecting all words and their counts
2021-09-29 15:45:27,106 : INFO : PROGRESS: at sentence #0, processed 0 words, keeping 0 word types
2021-09-29 15:45:27,707 : INFO : PROGRESS: at sentence #10000, processed 404396 words, keeping 14939 word types
2021-09-29 15:45:28,268 : INFO : PROGRESS: at sentence #20000, processed 795992 words, keeping 22404 word types
2021-09-29 15:45:28,824 : INFO : PROGRESS: at sentence #30000, processed 1185635 words, keeping 28543 word types
2021-09-29 15:45:29,366 : INFO : PROGRESS: at sentence #40000, processed 1565097 words, keeping 31906 word types
2021-09-29 15:45:29,908 : INFO : PROGRESS: at sentence #50000, processed 1942659 words, keeping 34985 word types
2021-09-29 15:45:30,153 : INFO : PROGRESS: at sentence #60000, processed 2110765 words, keeping 37539 word types
2021-09-29 15:45:30,511 : INFO : PROGRESS: at sentence #70000, processed 2356771 words, keeping 45277 word types
2021-09-29 15:45:30,845 : INFO : PROGRESS: at sentence #80000, processed 2587997 words, keeping 50975 word types
2021-09-29 15:45:31,164 : INFO : PROGRESS: at sentence #90000, processed 2807378 words, keeping 55860 word types
2021-09-29 15:45:31,536 : INFO : PROGRESS: at sentence #100000, processed 3063817 words, keeping 62206 word types
2021-09-29 15:45:31,830 : INFO : PROGRESS: at sentence #110000, processed 3264765 words, keeping 65474 word types
2021-09-29 15:45:32,106 : INFO : PROGRESS: at sentence #120000, processed 3454083 words, keeping 68501 word types
2021-09-29 15:45:32,375 : INFO : PROGRESS: at sentence #130000, processed 3638371 words, keeping 71517 word types
2021-09-29 15:45:32,658 : INFO : PROGRESS: at sentence #140000, processed 3833731 words, keeping 74424 word types
2021-09-29 15:45:32,921 : INFO : PROGRESS: at sentence #150000, processed 4015385 words, keeping 76225 word types
2021-09-29 15:45:33,173 : INFO : PROGRESS: at sentence #160000, processed 4188425 words, keeping 78178 word types
2021-09-29 15:45:33,468 : INFO : PROGRESS: at sentence #170000, processed 4390456 words, keeping 80136 word types
2021-09-29 15:45:33,839 : INFO : PROGRESS: at sentence #180000, processed 4646631 words, keeping 87082 word types
2021-09-29 15:45:34,280 : INFO : PROGRESS: at sentence #190000, processed 4950304 words, keeping 93402 word types
2021-09-29 15:45:34,605 : INFO : PROGRESS: at sentence #200000, processed 5175174 words, keeping 96795 word types
2021-09-29 15:45:34,810 : INFO : PROGRESS: at sentence #210000, processed 5312555 words, keeping 100982 word types
2021-09-29 15:45:35,091 : INFO : PROGRESS: at sentence #220000, processed 5502552 words, keeping 105536 word types
2021-09-29 15:45:35,248 : INFO : PROGRESS: at sentence #230000, processed 5607012 words, keeping 107965 word types
2021-09-29 15:45:35,645 : INFO : PROGRESS: at sentence #240000, processed 5880528 words, keeping 110626 word types
2021-09-29 15:45:36,033 : INFO : PROGRESS: at sentence #250000, processed 6143958 words, keeping 114520 word types
2021-09-29 15:45:36,592 : INFO : PROGRESS: at sentence #260000, processed 6534771 words, keeping 116197 word types
2021-09-29 15:45:37,159 : INFO : PROGRESS: at sentence #270000, processed 6930916 words, keeping 116225 word types
2021-09-29 15:45:37,714 : INFO : PROGRESS: at sentence #280000, processed 7318094 words, keeping 116254 word types
2021-09-29 15:45:38,260 : INFO : PROGRESS: at sentence #290000, processed 7701231 words, keeping 116270 word types
2021-09-29 15:45:38,812 : INFO : PROGRESS: at sentence #300000, processed 8088365 words, keeping 116283 word types
2021-09-29 15:45:39,121 : INFO : PROGRESS: at sentence #310000, processed 8301041 words, keeping 116293 word types
2021-09-29 15:45:39,444 : INFO : PROGRESS: at sentence #320000, processed 8526343 words, keeping 116400 word types
2021-09-29 15:45:39,782 : INFO : PROGRESS: at sentence #330000, processed 8761044 words, keeping 116472 word types
2021-09-29 15:45:40,084 : INFO : PROGRESS: at sentence #340000, processed 8969964 words, keeping 116504 word types
2021-09-29 15:45:40,456 : INFO : PROGRESS: at sentence #350000, processed 9228172 words, keeping 116532 word types
2021-09-29 15:45:40,776 : INFO : PROGRESS: at sentence #360000, processed 9450439 words, keeping 116558 word types
2021-09-29 15:45:41,023 : INFO : PROGRESS: at sentence #370000, processed 9621180 words, keeping 116574 word types
2021-09-29 15:45:41,309 : INFO : PROGRESS: at sentence #380000, processed 9819398 words, keeping 116589 word types
2021-09-29 15:45:41,593 : INFO : PROGRESS: at sentence #390000, processed 10013810 words, keeping 116601 word types
2021-09-29 15:45:41,859 : INFO : PROGRESS: at sentence #400000, processed 10197753 words, keeping 116611 word types
2021-09-29 15:45:42,113 : INFO : PROGRESS: at sentence #410000, processed 10373478 words, keeping 116634 word types
2021-09-29 15:45:42,374 : INFO : PROGRESS: at sentence #420000, processed 10553764 words, keeping 116648 word types
2021-09-29 15:45:42,751 : INFO : PROGRESS: at sentence #430000, processed 10816871 words, keeping 116665 word types
2021-09-29 15:45:43,161 : INFO : PROGRESS: at sentence #440000, processed 11100208 words, keeping 116703 word types
2021-09-29 15:45:43,529 : INFO : PROGRESS: at sentence #450000, processed 11355526 words, keeping 116724 word types
2021-09-29 15:45:43,706 : INFO : PROGRESS: at sentence #460000, processed 11472977 words, keeping 117201 word types
2021-09-29 15:45:43,972 : INFO : PROGRESS: at sentence #470000, processed 11653157 words, keeping 120451 word types
2021-09-29 15:45:44,125 : INFO : PROGRESS: at sentence #480000, processed 11756694 words, keeping 120953 word types
2021-09-29 15:45:44,253 : INFO : PROGRESS: at sentence #490000, processed 11843806 words, keeping 121253 word types
2021-09-29 15:45:44,402 : INFO : PROGRESS: at sentence #500000, processed 11945450 words, keeping 122251 word types
2021-09-29 15:45:44,572 : INFO : PROGRESS: at sentence #510000, processed 12059808 words, keeping 123004 word types
2021-09-29 15:45:44,691 : INFO : PROGRESS: at sentence #520000, processed 12140699 words, keeping 123218 word types
2021-09-29 15:45:44,820 : INFO : PROGRESS: at sentence #530000, processed 12227537 words, keeping 123537 word types
2021-09-29 15:45:44,937 : INFO : PROGRESS: at sentence #540000, processed 12307214 words, keeping 123548 word types
2021-09-29 15:45:45,059 : INFO : PROGRESS: at sentence #550000, processed 12390648 words, keeping 123557 word types
2021-09-29 15:45:45,197 : INFO : PROGRESS: at sentence #560000, processed 12484502 words, keeping 123573 word types
2021-09-29 15:45:45,339 : INFO : PROGRESS: at sentence #570000, processed 12582381 words, keeping 123583 word types
2021-09-29 15:45:45,461 : INFO : PROGRESS: at sentence #580000, processed 12664130 words, keeping 123593 word types
2021-09-29 15:45:45,584 : INFO : PROGRESS: at sentence #590000, processed 12748588 words, keeping 123601 word types
2021-09-29 15:45:45,725 : INFO : PROGRESS: at sentence #600000, processed 12844413 words, keeping 123604 word types
2021-09-29 15:45:45,859 : INFO : PROGRESS: at sentence #610000, processed 12935798 words, keeping 123611 word types
2021-09-29 15:45:45,996 : INFO : PROGRESS: at sentence #620000, processed 13028189 words, keeping 124636 word types
2021-09-29 15:45:46,135 : INFO : PROGRESS: at sentence #630000, processed 13121681 words, keeping 125801 word types
2021-09-29 15:45:46,191 : INFO : collected 126033 word types from a corpus of 13159108 raw words and 633956 sentences
2021-09-29 15:45:46,191 : INFO : Loading a fresh vocabulary
2021-09-29 15:45:46,344 : INFO : effective_min_count=2 retains 105879 unique words (84% of original 126033, drops 20154)
2021-09-29 15:45:46,344 : INFO : effective_min_count=2 leaves 13138954 word corpus (99% of original 13159108, drops 20154)
2021-09-29 15:45:46,483 : INFO : deleting the raw counts dictionary of 126033 items
2021-09-29 15:45:46,485 : INFO : sample=0.001 downsamples 65 most-common words
2021-09-29 15:45:46,485 : INFO : downsampling leaves estimated 9842694 word corpus (74.9% of prior 13138954)
2021-09-29 15:45:46,611 : INFO : estimated required memory for 105879 words and 200 dimensions: 222345900 bytes
2021-09-29 15:45:46,611 : INFO : resetting layer weights
2021-09-29 15:45:58,335 : INFO : training model with 3 workers on 105879 vocabulary and 200 features, using sg=0 hs=0 sample=0.001 negative=5 window=3
2021-09-29 15:45:59,351 : INFO : EPOCH 1 - PROGRESS: at 1.95% examples, 373321 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:00,358 : INFO : EPOCH 1 - PROGRESS: at 4.22% examples, 400479 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:01,370 : INFO : EPOCH 1 - PROGRESS: at 6.59% examples, 411611 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:46:02,395 : INFO : EPOCH 1 - PROGRESS: at 10.09% examples, 414483 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:03,416 : INFO : EPOCH 1 - PROGRESS: at 14.07% examples, 414439 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:04,428 : INFO : EPOCH 1 - PROGRESS: at 18.23% examples, 418342 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:05,429 : INFO : EPOCH 1 - PROGRESS: at 22.77% examples, 417784 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:06,433 : INFO : EPOCH 1 - PROGRESS: at 27.33% examples, 418142 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:07,447 : INFO : EPOCH 1 - PROGRESS: at 30.55% examples, 419305 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:08,456 : INFO : EPOCH 1 - PROGRESS: at 35.89% examples, 415745 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:09,460 : INFO : EPOCH 1 - PROGRESS: at 39.47% examples, 418281 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:10,481 : INFO : EPOCH 1 - PROGRESS: at 41.74% examples, 419275 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:46:11,482 : INFO : EPOCH 1 - PROGRESS: at 44.06% examples, 420720 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:12,484 : INFO : EPOCH 1 - PROGRESS: at 46.27% examples, 419717 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:46:13,496 : INFO : EPOCH 1 - PROGRESS: at 49.72% examples, 420292 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:46:14,508 : INFO : EPOCH 1 - PROGRESS: at 53.68% examples, 420161 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:46:15,526 : INFO : EPOCH 1 - PROGRESS: at 57.59% examples, 421145 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:16,528 : INFO : EPOCH 1 - PROGRESS: at 62.29% examples, 420755 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:17,533 : INFO : EPOCH 1 - PROGRESS: at 66.92% examples, 420385 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:18,550 : INFO : EPOCH 1 - PROGRESS: at 70.17% examples, 420746 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:19,557 : INFO : EPOCH 1 - PROGRESS: at 76.53% examples, 420000 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:20,586 : INFO : EPOCH 1 - PROGRESS: at 86.24% examples, 418098 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:21,607 : INFO : EPOCH 1 - PROGRESS: at 96.35% examples, 416569 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:21,874 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-29 15:46:21,876 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-29 15:46:21,878 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-29 15:46:21,878 : INFO : EPOCH - 1 : training on 13159108 raw words (9841146 effective words) took 23.5s, 418028 effective words/s
2021-09-29 15:46:22,879 : INFO : EPOCH 2 - PROGRESS: at 1.95% examples, 379191 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:46:23,888 : INFO : EPOCH 2 - PROGRESS: at 4.18% examples, 399536 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:46:24,903 : INFO : EPOCH 2 - PROGRESS: at 6.52% examples, 407893 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:25,929 : INFO : EPOCH 2 - PROGRESS: at 9.93% examples, 409659 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:46:26,947 : INFO : EPOCH 2 - PROGRESS: at 13.92% examples, 410939 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:46:27,975 : INFO : EPOCH 2 - PROGRESS: at 17.85% examples, 414450 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:28,997 : INFO : EPOCH 2 - PROGRESS: at 22.68% examples, 415219 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:30,019 : INFO : EPOCH 2 - PROGRESS: at 27.28% examples, 415021 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:31,038 : INFO : EPOCH 2 - PROGRESS: at 30.45% examples, 415579 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:32,066 : INFO : EPOCH 2 - PROGRESS: at 36.17% examples, 414407 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:33,077 : INFO : EPOCH 2 - PROGRESS: at 39.54% examples, 417077 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:34,078 : INFO : EPOCH 2 - PROGRESS: at 41.78% examples, 418107 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:35,090 : INFO : EPOCH 2 - PROGRESS: at 44.06% examples, 418712 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:36,101 : INFO : EPOCH 2 - PROGRESS: at 46.32% examples, 418172 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:46:37,130 : INFO : EPOCH 2 - PROGRESS: at 49.81% examples, 418882 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:38,130 : INFO : EPOCH 2 - PROGRESS: at 53.68% examples, 418228 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:39,144 : INFO : EPOCH 2 - PROGRESS: at 57.59% examples, 419444 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:40,154 : INFO : EPOCH 2 - PROGRESS: at 62.29% examples, 418965 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:41,161 : INFO : EPOCH 2 - PROGRESS: at 66.92% examples, 418638 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:42,173 : INFO : EPOCH 2 - PROGRESS: at 70.12% examples, 418872 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:43,191 : INFO : EPOCH 2 - PROGRESS: at 76.53% examples, 418318 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:44,235 : INFO : EPOCH 2 - PROGRESS: at 86.24% examples, 416233 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:46:45,262 : INFO : EPOCH 2 - PROGRESS: at 96.35% examples, 414673 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:45,525 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-29 15:46:45,530 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-29 15:46:45,532 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-29 15:46:45,532 : INFO : EPOCH - 2 : training on 13159108 raw words (9843686 effective words) took 23.7s, 416170 effective words/s
2021-09-29 15:46:46,550 : INFO : EPOCH 3 - PROGRESS: at 1.99% examples, 379624 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:47,553 : INFO : EPOCH 3 - PROGRESS: at 4.26% examples, 404421 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:46:48,555 : INFO : EPOCH 3 - PROGRESS: at 6.59% examples, 413098 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:46:49,562 : INFO : EPOCH 3 - PROGRESS: at 10.03% examples, 415374 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:50,578 : INFO : EPOCH 3 - PROGRESS: at 13.92% examples, 412755 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:46:51,590 : INFO : EPOCH 3 - PROGRESS: at 17.71% examples, 415870 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:46:52,593 : INFO : EPOCH 3 - PROGRESS: at 22.42% examples, 415518 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:53,612 : INFO : EPOCH 3 - PROGRESS: at 27.11% examples, 415373 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:54,617 : INFO : EPOCH 3 - PROGRESS: at 30.30% examples, 416521 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:46:55,624 : INFO : EPOCH 3 - PROGRESS: at 35.58% examples, 415673 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:56,669 : INFO : EPOCH 3 - PROGRESS: at 39.20% examples, 415040 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:46:57,675 : INFO : EPOCH 3 - PROGRESS: at 41.65% examples, 418194 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:46:58,698 : INFO : EPOCH 3 - PROGRESS: at 43.92% examples, 418455 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:46:59,729 : INFO : EPOCH 3 - PROGRESS: at 46.31% examples, 418933 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:47:00,774 : INFO : EPOCH 3 - PROGRESS: at 49.76% examples, 418619 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:47:01,802 : INFO : EPOCH 3 - PROGRESS: at 53.91% examples, 419559 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:02,817 : INFO : EPOCH 3 - PROGRESS: at 57.72% examples, 419312 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:47:03,829 : INFO : EPOCH 3 - PROGRESS: at 62.37% examples, 418769 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:04,842 : INFO : EPOCH 3 - PROGRESS: at 66.97% examples, 418333 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:47:05,853 : INFO : EPOCH 3 - PROGRESS: at 70.22% examples, 418951 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:06,864 : INFO : EPOCH 3 - PROGRESS: at 76.53% examples, 417849 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:07,865 : INFO : EPOCH 3 - PROGRESS: at 85.87% examples, 415939 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:47:08,867 : INFO : EPOCH 3 - PROGRESS: at 95.55% examples, 414284 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:47:09,202 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-29 15:47:09,204 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-29 15:47:09,206 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-29 15:47:09,206 : INFO : EPOCH - 3 : training on 13159108 raw words (9841569 effective words) took 23.7s, 415718 effective words/s
2021-09-29 15:47:10,213 : INFO : EPOCH 4 - PROGRESS: at 1.95% examples, 377198 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:47:11,249 : INFO : EPOCH 4 - PROGRESS: at 4.22% examples, 396725 words/s, in_qsize 5, out_qsize 2
2021-09-29 15:47:12,264 : INFO : EPOCH 4 - PROGRESS: at 6.63% examples, 411328 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:13,265 : INFO : EPOCH 4 - PROGRESS: at 10.09% examples, 414657 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:14,270 : INFO : EPOCH 4 - PROGRESS: at 14.02% examples, 414408 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:15,275 : INFO : EPOCH 4 - PROGRESS: at 17.71% examples, 415222 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:16,295 : INFO : EPOCH 4 - PROGRESS: at 22.51% examples, 414892 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:17,299 : INFO : EPOCH 4 - PROGRESS: at 27.11% examples, 414728 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:18,303 : INFO : EPOCH 4 - PROGRESS: at 30.30% examples, 415999 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:19,321 : INFO : EPOCH 4 - PROGRESS: at 35.28% examples, 413402 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:20,323 : INFO : EPOCH 4 - PROGRESS: at 39.08% examples, 414288 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:47:21,338 : INFO : EPOCH 4 - PROGRESS: at 41.52% examples, 416727 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:22,339 : INFO : EPOCH 4 - PROGRESS: at 43.79% examples, 417832 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:47:23,350 : INFO : EPOCH 4 - PROGRESS: at 46.08% examples, 417320 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:47:24,360 : INFO : EPOCH 4 - PROGRESS: at 49.36% examples, 417741 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:25,388 : INFO : EPOCH 4 - PROGRESS: at 53.11% examples, 417392 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:26,446 : INFO : EPOCH 4 - PROGRESS: at 57.02% examples, 417042 words/s, in_qsize 5, out_qsize 2
2021-09-29 15:47:27,466 : INFO : EPOCH 4 - PROGRESS: at 61.95% examples, 417718 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:28,478 : INFO : EPOCH 4 - PROGRESS: at 66.69% examples, 417273 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:29,478 : INFO : EPOCH 4 - PROGRESS: at 69.90% examples, 417755 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:47:30,485 : INFO : EPOCH 4 - PROGRESS: at 75.65% examples, 417439 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:31,492 : INFO : EPOCH 4 - PROGRESS: at 85.07% examples, 415646 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:32,518 : INFO : EPOCH 4 - PROGRESS: at 94.60% examples, 413055 words/s, in_qsize 3, out_qsize 2
2021-09-29 15:47:32,958 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-29 15:47:32,960 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-29 15:47:32,963 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-29 15:47:32,963 : INFO : EPOCH - 4 : training on 13159108 raw words (9843086 effective words) took 23.8s, 414342 effective words/s
2021-09-29 15:47:33,971 : INFO : EPOCH 5 - PROGRESS: at 1.99% examples, 383961 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:35,017 : INFO : EPOCH 5 - PROGRESS: at 4.26% examples, 397997 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:47:36,020 : INFO : EPOCH 5 - PROGRESS: at 6.59% examples, 408536 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:37,042 : INFO : EPOCH 5 - PROGRESS: at 10.03% examples, 410573 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:38,056 : INFO : EPOCH 5 - PROGRESS: at 14.02% examples, 411903 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:39,097 : INFO : EPOCH 5 - PROGRESS: at 17.85% examples, 411851 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:47:40,109 : INFO : EPOCH 5 - PROGRESS: at 22.68% examples, 413556 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:41,117 : INFO : EPOCH 5 - PROGRESS: at 27.17% examples, 412550 words/s, in_qsize 5, out_qsize 2
2021-09-29 15:47:42,120 : INFO : EPOCH 5 - PROGRESS: at 30.45% examples, 415652 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:43,126 : INFO : EPOCH 5 - PROGRESS: at 36.03% examples, 414700 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:47:44,139 : INFO : EPOCH 5 - PROGRESS: at 39.40% examples, 415714 words/s, in_qsize 5, out_qsize 2
2021-09-29 15:47:45,154 : INFO : EPOCH 5 - PROGRESS: at 41.82% examples, 419029 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:46,168 : INFO : EPOCH 5 - PROGRESS: at 44.10% examples, 419476 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:47,178 : INFO : EPOCH 5 - PROGRESS: at 46.47% examples, 420479 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:48,188 : INFO : EPOCH 5 - PROGRESS: at 49.87% examples, 420060 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:49,208 : INFO : EPOCH 5 - PROGRESS: at 53.91% examples, 420188 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:50,211 : INFO : EPOCH 5 - PROGRESS: at 57.99% examples, 421094 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:47:51,226 : INFO : EPOCH 5 - PROGRESS: at 62.37% examples, 419581 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:47:52,233 : INFO : EPOCH 5 - PROGRESS: at 67.08% examples, 420005 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:47:53,238 : INFO : EPOCH 5 - PROGRESS: at 70.27% examples, 420322 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:54,250 : INFO : EPOCH 5 - PROGRESS: at 77.07% examples, 419710 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:55,259 : INFO : EPOCH 5 - PROGRESS: at 86.77% examples, 418222 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:56,272 : INFO : EPOCH 5 - PROGRESS: at 96.35% examples, 415953 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:56,538 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-29 15:47:56,540 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-29 15:47:56,543 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-29 15:47:56,543 : INFO : EPOCH - 5 : training on 13159108 raw words (9842612 effective words) took 23.6s, 417425 effective words/s
2021-09-29 15:47:57,572 : INFO : EPOCH 6 - PROGRESS: at 1.95% examples, 368284 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:47:58,585 : INFO : EPOCH 6 - PROGRESS: at 4.35% examples, 407792 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:47:59,613 : INFO : EPOCH 6 - PROGRESS: at 6.72% examples, 414457 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:00,625 : INFO : EPOCH 6 - PROGRESS: at 10.03% examples, 410383 words/s, in_qsize 5, out_qsize 2
2021-09-29 15:48:01,630 : INFO : EPOCH 6 - PROGRESS: at 14.07% examples, 413845 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:48:02,636 : INFO : EPOCH 6 - PROGRESS: at 17.99% examples, 415970 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:48:03,638 : INFO : EPOCH 6 - PROGRESS: at 22.59% examples, 415645 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:48:04,646 : INFO : EPOCH 6 - PROGRESS: at 27.17% examples, 415187 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:05,668 : INFO : EPOCH 6 - PROGRESS: at 30.41% examples, 416416 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:06,675 : INFO : EPOCH 6 - PROGRESS: at 35.74% examples, 414745 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:07,703 : INFO : EPOCH 6 - PROGRESS: at 39.27% examples, 414922 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:48:08,714 : INFO : EPOCH 6 - PROGRESS: at 41.70% examples, 417907 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:48:09,741 : INFO : EPOCH 6 - PROGRESS: at 44.06% examples, 419239 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:10,751 : INFO : EPOCH 6 - PROGRESS: at 46.32% examples, 418649 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:48:11,776 : INFO : EPOCH 6 - PROGRESS: at 49.81% examples, 419385 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:12,785 : INFO : EPOCH 6 - PROGRESS: at 53.73% examples, 418925 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:13,795 : INFO : EPOCH 6 - PROGRESS: at 57.59% examples, 419722 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:14,843 : INFO : EPOCH 6 - PROGRESS: at 62.37% examples, 418763 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:48:15,865 : INFO : EPOCH 6 - PROGRESS: at 67.02% examples, 418516 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:48:16,874 : INFO : EPOCH 6 - PROGRESS: at 70.27% examples, 419141 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:17,877 : INFO : EPOCH 6 - PROGRESS: at 76.92% examples, 418475 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:18,882 : INFO : EPOCH 6 - PROGRESS: at 86.44% examples, 416818 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:19,889 : INFO : EPOCH 6 - PROGRESS: at 95.72% examples, 414408 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:20,206 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-29 15:48:20,210 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-29 15:48:20,211 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-29 15:48:20,211 : INFO : EPOCH - 6 : training on 13159108 raw words (9842229 effective words) took 23.7s, 415852 effective words/s
2021-09-29 15:48:21,239 : INFO : EPOCH 7 - PROGRESS: at 2.04% examples, 383807 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:22,245 : INFO : EPOCH 7 - PROGRESS: at 4.31% examples, 405548 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:23,260 : INFO : EPOCH 7 - PROGRESS: at 6.68% examples, 414634 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:24,262 : INFO : EPOCH 7 - PROGRESS: at 9.98% examples, 411450 words/s, in_qsize 5, out_qsize 2
2021-09-29 15:48:25,280 : INFO : EPOCH 7 - PROGRESS: at 14.02% examples, 413722 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:26,284 : INFO : EPOCH 7 - PROGRESS: at 17.99% examples, 417154 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:27,291 : INFO : EPOCH 7 - PROGRESS: at 22.59% examples, 416325 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:28,296 : INFO : EPOCH 7 - PROGRESS: at 27.05% examples, 414165 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:48:29,312 : INFO : EPOCH 7 - PROGRESS: at 30.25% examples, 414970 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:48:30,336 : INFO : EPOCH 7 - PROGRESS: at 35.43% examples, 413615 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:31,360 : INFO : EPOCH 7 - PROGRESS: at 39.20% examples, 414578 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:48:32,367 : INFO : EPOCH 7 - PROGRESS: at 41.65% examples, 417783 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:33,368 : INFO : EPOCH 7 - PROGRESS: at 43.92% examples, 418779 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:34,371 : INFO : EPOCH 7 - PROGRESS: at 46.27% examples, 419496 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:35,419 : INFO : EPOCH 7 - PROGRESS: at 49.67% examples, 418623 words/s, in_qsize 5, out_qsize 2
2021-09-29 15:48:36,431 : INFO : EPOCH 7 - PROGRESS: at 53.76% examples, 419531 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:37,471 : INFO : EPOCH 7 - PROGRESS: at 57.59% examples, 419577 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:48:38,480 : INFO : EPOCH 7 - PROGRESS: at 62.29% examples, 419075 words/s, in_qsize 5, out_qsize 2
2021-09-29 15:48:39,497 : INFO : EPOCH 7 - PROGRESS: at 66.92% examples, 418532 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:40,505 : INFO : EPOCH 7 - PROGRESS: at 70.07% examples, 418480 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:41,507 : INFO : EPOCH 7 - PROGRESS: at 75.96% examples, 417744 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:42,517 : INFO : EPOCH 7 - PROGRESS: at 85.66% examples, 416196 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:48:43,563 : INFO : EPOCH 7 - PROGRESS: at 95.56% examples, 414068 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:43,899 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-29 15:48:43,903 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-29 15:48:43,905 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-29 15:48:43,905 : INFO : EPOCH - 7 : training on 13159108 raw words (9843467 effective words) took 23.7s, 415448 effective words/s
2021-09-29 15:48:44,928 : INFO : EPOCH 8 - PROGRESS: at 1.99% examples, 377955 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:45,937 : INFO : EPOCH 8 - PROGRESS: at 4.31% examples, 405893 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:46,974 : INFO : EPOCH 8 - PROGRESS: at 6.59% examples, 407029 words/s, in_qsize 5, out_qsize 2
2021-09-29 15:48:47,993 : INFO : EPOCH 8 - PROGRESS: at 9.98% examples, 407821 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:49,000 : INFO : EPOCH 8 - PROGRESS: at 13.92% examples, 408767 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:48:50,012 : INFO : EPOCH 8 - PROGRESS: at 17.71% examples, 412424 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:51,037 : INFO : EPOCH 8 - PROGRESS: at 22.51% examples, 412361 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:52,045 : INFO : EPOCH 8 - PROGRESS: at 26.99% examples, 410494 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:53,059 : INFO : EPOCH 8 - PROGRESS: at 30.15% examples, 410878 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:48:54,067 : INFO : EPOCH 8 - PROGRESS: at 35.28% examples, 411428 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:55,087 : INFO : EPOCH 8 - PROGRESS: at 39.20% examples, 413331 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:56,091 : INFO : EPOCH 8 - PROGRESS: at 41.49% examples, 414235 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:48:57,102 : INFO : EPOCH 8 - PROGRESS: at 43.68% examples, 414080 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:48:58,103 : INFO : EPOCH 8 - PROGRESS: at 46.03% examples, 415225 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:48:59,114 : INFO : EPOCH 8 - PROGRESS: at 49.17% examples, 415235 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:49:00,132 : INFO : EPOCH 8 - PROGRESS: at 52.89% examples, 415335 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:01,138 : INFO : EPOCH 8 - PROGRESS: at 56.84% examples, 416398 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:49:02,144 : INFO : EPOCH 8 - PROGRESS: at 61.37% examples, 415376 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:49:03,153 : INFO : EPOCH 8 - PROGRESS: at 66.39% examples, 415937 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:49:04,180 : INFO : EPOCH 8 - PROGRESS: at 69.69% examples, 416193 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:05,185 : INFO : EPOCH 8 - PROGRESS: at 74.62% examples, 415225 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:49:06,210 : INFO : EPOCH 8 - PROGRESS: at 84.05% examples, 413754 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:07,234 : INFO : EPOCH 8 - PROGRESS: at 93.96% examples, 411664 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:07,759 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-29 15:49:07,763 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-29 15:49:07,763 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-29 15:49:07,763 : INFO : EPOCH - 8 : training on 13159108 raw words (9843805 effective words) took 23.9s, 412609 effective words/s
2021-09-29 15:49:08,777 : INFO : EPOCH 9 - PROGRESS: at 1.99% examples, 381786 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:09,786 : INFO : EPOCH 9 - PROGRESS: at 4.26% examples, 403990 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:10,793 : INFO : EPOCH 9 - PROGRESS: at 6.59% examples, 412089 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:49:11,829 : INFO : EPOCH 9 - PROGRESS: at 10.09% examples, 413662 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:12,841 : INFO : EPOCH 9 - PROGRESS: at 14.07% examples, 414397 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:13,856 : INFO : EPOCH 9 - PROGRESS: at 18.23% examples, 418170 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:14,904 : INFO : EPOCH 9 - PROGRESS: at 22.96% examples, 416944 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:15,930 : INFO : EPOCH 9 - PROGRESS: at 27.52% examples, 417280 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:16,941 : INFO : EPOCH 9 - PROGRESS: at 30.66% examples, 417991 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:17,943 : INFO : EPOCH 9 - PROGRESS: at 36.03% examples, 414037 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:49:18,948 : INFO : EPOCH 9 - PROGRESS: at 39.55% examples, 417581 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:49:19,962 : INFO : EPOCH 9 - PROGRESS: at 41.82% examples, 418777 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:20,976 : INFO : EPOCH 9 - PROGRESS: at 44.10% examples, 419284 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:22,005 : INFO : EPOCH 9 - PROGRESS: at 46.47% examples, 419758 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:23,011 : INFO : EPOCH 9 - PROGRESS: at 49.87% examples, 419513 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:49:24,041 : INFO : EPOCH 9 - PROGRESS: at 53.91% examples, 419374 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:25,047 : INFO : EPOCH 9 - PROGRESS: at 57.99% examples, 420194 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:26,070 : INFO : EPOCH 9 - PROGRESS: at 62.38% examples, 418601 words/s, in_qsize 5, out_qsize 2
2021-09-29 15:49:27,071 : INFO : EPOCH 9 - PROGRESS: at 67.02% examples, 418806 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:28,086 : INFO : EPOCH 9 - PROGRESS: at 70.22% examples, 418982 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:29,086 : INFO : EPOCH 9 - PROGRESS: at 76.17% examples, 417522 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:30,088 : INFO : EPOCH 9 - PROGRESS: at 85.48% examples, 415556 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:49:31,118 : INFO : EPOCH 9 - PROGRESS: at 95.05% examples, 413168 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:31,510 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-29 15:49:31,512 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-29 15:49:31,514 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-29 15:49:31,514 : INFO : EPOCH - 9 : training on 13159108 raw words (9843631 effective words) took 23.8s, 414466 effective words/s
2021-09-29 15:49:32,534 : INFO : EPOCH 10 - PROGRESS: at 1.99% examples, 378874 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:33,544 : INFO : EPOCH 10 - PROGRESS: at 4.26% examples, 402401 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:49:34,588 : INFO : EPOCH 10 - PROGRESS: at 6.60% examples, 406266 words/s, in_qsize 5, out_qsize 2
2021-09-29 15:49:35,613 : INFO : EPOCH 10 - PROGRESS: at 10.18% examples, 412125 words/s, in_qsize 3, out_qsize 2
2021-09-29 15:49:36,641 : INFO : EPOCH 10 - PROGRESS: at 14.13% examples, 411918 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:37,645 : INFO : EPOCH 10 - PROGRESS: at 18.20% examples, 415650 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:49:38,663 : INFO : EPOCH 10 - PROGRESS: at 22.86% examples, 415455 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:39,670 : INFO : EPOCH 10 - PROGRESS: at 27.28% examples, 414198 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:40,673 : INFO : EPOCH 10 - PROGRESS: at 30.36% examples, 413964 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:41,686 : INFO : EPOCH 10 - PROGRESS: at 35.28% examples, 411081 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:42,691 : INFO : EPOCH 10 - PROGRESS: at 39.20% examples, 413560 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:43,704 : INFO : EPOCH 10 - PROGRESS: at 41.57% examples, 415343 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:44,729 : INFO : EPOCH 10 - PROGRESS: at 43.76% examples, 414621 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:49:45,769 : INFO : EPOCH 10 - PROGRESS: at 46.12% examples, 414535 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:49:46,778 : INFO : EPOCH 10 - PROGRESS: at 49.43% examples, 415125 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:47,792 : INFO : EPOCH 10 - PROGRESS: at 53.11% examples, 414884 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:48,805 : INFO : EPOCH 10 - PROGRESS: at 57.12% examples, 416177 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:49,834 : INFO : EPOCH 10 - PROGRESS: at 61.68% examples, 415078 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:49:50,849 : INFO : EPOCH 10 - PROGRESS: at 66.57% examples, 415076 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:49:51,867 : INFO : EPOCH 10 - PROGRESS: at 69.69% examples, 414482 words/s, in_qsize 4, out_qsize 2
2021-09-29 15:49:52,881 : INFO : EPOCH 10 - PROGRESS: at 74.93% examples, 414053 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:49:53,888 : INFO : EPOCH 10 - PROGRESS: at 83.68% examples, 411713 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:49:54,893 : INFO : EPOCH 10 - PROGRESS: at 93.99% examples, 410689 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:49:55,509 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-29 15:49:55,515 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-29 15:49:55,515 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-29 15:49:55,515 : INFO : EPOCH - 10 : training on 13159108 raw words (9841531 effective words) took 24.0s, 410050 effective words/s
2021-09-29 15:49:55,515 : INFO : training on a 131591080 raw words (98426762 effective words) took 237.2s, 414988 effective words/s
2021-09-29 15:49:55,515 : INFO : storing 105879x200 projection weights into /media/ye/project2/exp/bilingual-induction/exp1/my/my_corpus.txt_model=word2vec_vectors.vec
Loading corpus: /media/ye/project2/exp/bilingual-induction/exp1/my/my_corpus.txt
Embeddings saved to /media/ye/project2/exp/bilingual-induction/exp1/my/my_corpus.txt_model=word2vec_vectors.vec

real	4m42.363s
user	6m24.838s
sys	0m3.100s
start building a word2vec model for TRG language ...  
2021-09-29 15:50:06,546 : INFO : collecting all words and their counts
2021-09-29 15:50:06,643 : INFO : PROGRESS: at sentence #0, processed 0 words, keeping 0 word types
2021-09-29 15:50:07,812 : INFO : PROGRESS: at sentence #10000, processed 856417 words, keeping 37157 word types
2021-09-29 15:50:08,834 : INFO : PROGRESS: at sentence #20000, processed 1639648 words, keeping 57687 word types
2021-09-29 15:50:11,286 : INFO : PROGRESS: at sentence #30000, processed 2572059 words, keeping 74632 word types
2021-09-29 15:50:12,541 : INFO : PROGRESS: at sentence #40000, processed 3530495 words, keeping 93905 word types
2021-09-29 15:50:13,839 : INFO : PROGRESS: at sentence #50000, processed 4532267 words, keeping 110510 word types
2021-09-29 15:50:14,871 : INFO : PROGRESS: at sentence #60000, processed 5314109 words, keeping 120800 word types
2021-09-29 15:50:15,901 : INFO : PROGRESS: at sentence #70000, processed 6097063 words, keeping 130023 word types
2021-09-29 15:50:17,589 : INFO : PROGRESS: at sentence #80000, processed 7397249 words, keeping 143683 word types
2021-09-29 15:50:18,639 : INFO : PROGRESS: at sentence #90000, processed 8198407 words, keeping 148940 word types
2021-09-29 15:50:19,636 : INFO : PROGRESS: at sentence #100000, processed 8959383 words, keeping 157723 word types
2021-09-29 15:50:20,600 : INFO : PROGRESS: at sentence #110000, processed 9687655 words, keeping 164381 word types
2021-09-29 15:50:21,702 : INFO : PROGRESS: at sentence #120000, processed 10525118 words, keeping 171206 word types
2021-09-29 15:50:22,692 : INFO : PROGRESS: at sentence #130000, processed 11280108 words, keeping 177213 word types
2021-09-29 15:50:23,655 : INFO : PROGRESS: at sentence #140000, processed 12016743 words, keeping 182472 word types
2021-09-29 15:50:24,725 : INFO : PROGRESS: at sentence #150000, processed 12826975 words, keeping 188977 word types
2021-09-29 15:50:26,068 : INFO : PROGRESS: at sentence #160000, processed 13855182 words, keeping 194528 word types
2021-09-29 15:50:27,250 : INFO : PROGRESS: at sentence #170000, processed 14751080 words, keeping 199284 word types
2021-09-29 15:50:28,402 : INFO : PROGRESS: at sentence #180000, processed 15637158 words, keeping 207749 word types
2021-09-29 15:50:29,404 : INFO : PROGRESS: at sentence #190000, processed 16403465 words, keeping 213279 word types
2021-09-29 15:50:30,408 : INFO : PROGRESS: at sentence #200000, processed 17173239 words, keeping 217945 word types
2021-09-29 15:50:31,374 : INFO : PROGRESS: at sentence #210000, processed 17908845 words, keeping 222598 word types
2021-09-29 15:50:32,475 : INFO : PROGRESS: at sentence #220000, processed 18748603 words, keeping 228947 word types
2021-09-29 15:50:34,849 : INFO : PROGRESS: at sentence #230000, processed 20575993 words, keeping 258944 word types
2021-09-29 15:50:38,653 : INFO : PROGRESS: at sentence #240000, processed 23460183 words, keeping 289437 word types
2021-09-29 15:50:42,334 : INFO : PROGRESS: at sentence #250000, processed 26231994 words, keeping 314656 word types
2021-09-29 15:50:43,666 : INFO : PROGRESS: at sentence #260000, processed 27221411 words, keeping 328432 word types
2021-09-29 15:50:44,799 : INFO : PROGRESS: at sentence #270000, processed 28078797 words, keeping 334035 word types
2021-09-29 15:50:45,830 : INFO : PROGRESS: at sentence #280000, processed 28851753 words, keeping 337254 word types
2021-09-29 15:50:47,395 : INFO : PROGRESS: at sentence #290000, processed 30046848 words, keeping 343424 word types
2021-09-29 15:50:49,302 : INFO : PROGRESS: at sentence #300000, processed 31526004 words, keeping 350103 word types
2021-09-29 15:50:50,559 : INFO : PROGRESS: at sentence #310000, processed 32476995 words, keeping 357010 word types
2021-09-29 15:50:51,741 : INFO : PROGRESS: at sentence #320000, processed 33378244 words, keeping 363313 word types
2021-09-29 15:50:52,727 : INFO : PROGRESS: at sentence #330000, processed 34117385 words, keeping 369287 word types
2021-09-29 15:50:53,638 : INFO : PROGRESS: at sentence #340000, processed 34812365 words, keeping 374372 word types
2021-09-29 15:50:54,595 : INFO : PROGRESS: at sentence #350000, processed 35538094 words, keeping 378906 word types
2021-09-29 15:50:55,533 : INFO : PROGRESS: at sentence #360000, processed 36255461 words, keeping 383282 word types
2021-09-29 15:50:56,483 : INFO : PROGRESS: at sentence #370000, processed 36964781 words, keeping 388524 word types
2021-09-29 15:50:57,439 : INFO : PROGRESS: at sentence #380000, processed 37688733 words, keeping 392198 word types
2021-09-29 15:50:58,372 : INFO : PROGRESS: at sentence #390000, processed 38391799 words, keeping 395639 word types
2021-09-29 15:50:59,311 : INFO : PROGRESS: at sentence #400000, processed 39091452 words, keeping 399275 word types
2021-09-29 15:51:00,674 : INFO : PROGRESS: at sentence #410000, processed 40128198 words, keeping 406541 word types
2021-09-29 15:51:01,769 : INFO : PROGRESS: at sentence #420000, processed 40965191 words, keeping 411288 word types
2021-09-29 15:51:02,932 : INFO : PROGRESS: at sentence #430000, processed 41804806 words, keeping 418558 word types
2021-09-29 15:51:04,019 : INFO : PROGRESS: at sentence #440000, processed 42582172 words, keeping 426512 word types
2021-09-29 15:51:05,113 : INFO : PROGRESS: at sentence #450000, processed 43405228 words, keeping 432963 word types
2021-09-29 15:51:06,274 : INFO : PROGRESS: at sentence #460000, processed 44275969 words, keeping 438462 word types
2021-09-29 15:51:07,301 : INFO : PROGRESS: at sentence #470000, processed 45052117 words, keeping 444093 word types
2021-09-29 15:51:08,276 : INFO : PROGRESS: at sentence #480000, processed 45788235 words, keeping 449915 word types
2021-09-29 15:51:09,528 : INFO : PROGRESS: at sentence #490000, processed 46743365 words, keeping 455392 word types
2021-09-29 15:51:10,664 : INFO : PROGRESS: at sentence #500000, processed 47618987 words, keeping 459461 word types
2021-09-29 15:51:11,855 : INFO : PROGRESS: at sentence #510000, processed 48517973 words, keeping 466706 word types
2021-09-29 15:51:12,811 : INFO : PROGRESS: at sentence #520000, processed 49226448 words, keeping 469858 word types
2021-09-29 15:51:15,450 : INFO : PROGRESS: at sentence #530000, processed 51241838 words, keeping 501749 word types
2021-09-29 15:51:16,912 : INFO : PROGRESS: at sentence #540000, processed 52355129 words, keeping 509849 word types
2021-09-29 15:51:19,084 : INFO : PROGRESS: at sentence #550000, processed 54028410 words, keeping 518729 word types
2021-09-29 15:51:21,021 : INFO : PROGRESS: at sentence #560000, processed 55506699 words, keeping 526525 word types
2021-09-29 15:51:22,820 : INFO : PROGRESS: at sentence #570000, processed 56880618 words, keeping 532262 word types
2021-09-29 15:51:24,695 : INFO : PROGRESS: at sentence #580000, processed 58314262 words, keeping 537453 word types
2021-09-29 15:51:26,464 : INFO : PROGRESS: at sentence #590000, processed 59666884 words, keeping 542212 word types
2021-09-29 15:51:28,290 : INFO : PROGRESS: at sentence #600000, processed 61062281 words, keeping 548435 word types
2021-09-29 15:51:29,347 : INFO : PROGRESS: at sentence #610000, processed 61865180 words, keeping 554018 word types
2021-09-29 15:51:30,409 : INFO : PROGRESS: at sentence #620000, processed 62676312 words, keeping 558491 word types
2021-09-29 15:51:31,521 : INFO : PROGRESS: at sentence #630000, processed 63514480 words, keeping 562733 word types
2021-09-29 15:51:32,586 : INFO : PROGRESS: at sentence #640000, processed 64316617 words, keeping 570041 word types
2021-09-29 15:51:33,599 : INFO : PROGRESS: at sentence #650000, processed 65083808 words, keeping 575243 word types
2021-09-29 15:51:34,649 : INFO : PROGRESS: at sentence #660000, processed 65887991 words, keeping 581842 word types
2021-09-29 15:51:35,798 : INFO : PROGRESS: at sentence #670000, processed 66754003 words, keeping 588822 word types
2021-09-29 15:51:37,119 : INFO : PROGRESS: at sentence #680000, processed 67749136 words, keeping 599561 word types
2021-09-29 15:51:38,877 : INFO : PROGRESS: at sentence #690000, processed 69074992 words, keeping 614237 word types
2021-09-29 15:51:39,885 : INFO : PROGRESS: at sentence #700000, processed 69843721 words, keeping 618301 word types
2021-09-29 15:51:40,917 : INFO : PROGRESS: at sentence #710000, processed 70624501 words, keeping 624489 word types
2021-09-29 15:51:41,884 : INFO : PROGRESS: at sentence #720000, processed 71354447 words, keeping 627874 word types
2021-09-29 15:51:42,723 : INFO : PROGRESS: at sentence #730000, processed 71984100 words, keeping 630330 word types
2021-09-29 15:51:43,662 : INFO : PROGRESS: at sentence #740000, processed 72677704 words, keeping 633269 word types
2021-09-29 15:51:44,735 : INFO : PROGRESS: at sentence #750000, processed 73444285 words, keeping 637636 word types
2021-09-29 15:51:45,960 : INFO : PROGRESS: at sentence #760000, processed 74335505 words, keeping 643632 word types
2021-09-29 15:51:47,246 : INFO : PROGRESS: at sentence #770000, processed 75298780 words, keeping 649674 word types
2021-09-29 15:51:48,417 : INFO : PROGRESS: at sentence #780000, processed 76189579 words, keeping 653527 word types
2021-09-29 15:51:49,346 : INFO : PROGRESS: at sentence #790000, processed 76892306 words, keeping 657840 word types
2021-09-29 15:51:50,366 : INFO : PROGRESS: at sentence #800000, processed 77669230 words, keeping 661077 word types
2021-09-29 15:51:51,409 : INFO : PROGRESS: at sentence #810000, processed 78462935 words, keeping 666292 word types
2021-09-29 15:51:52,559 : INFO : PROGRESS: at sentence #820000, processed 79343863 words, keeping 670021 word types
2021-09-29 15:51:53,622 : INFO : PROGRESS: at sentence #830000, processed 80149716 words, keeping 675961 word types
2021-09-29 15:51:54,635 : INFO : PROGRESS: at sentence #840000, processed 80919098 words, keeping 682270 word types
2021-09-29 15:51:55,695 : INFO : PROGRESS: at sentence #850000, processed 81725718 words, keeping 686449 word types
2021-09-29 15:51:56,914 : INFO : PROGRESS: at sentence #860000, processed 82646589 words, keeping 690320 word types
2021-09-29 15:51:57,915 : INFO : PROGRESS: at sentence #870000, processed 83407421 words, keeping 694791 word types
2021-09-29 15:51:58,912 : INFO : PROGRESS: at sentence #880000, processed 84173268 words, keeping 698857 word types
2021-09-29 15:52:00,166 : INFO : PROGRESS: at sentence #890000, processed 85116837 words, keeping 702016 word types
2021-09-29 15:52:01,273 : INFO : PROGRESS: at sentence #900000, processed 85960765 words, keeping 704437 word types
2021-09-29 15:52:02,392 : INFO : PROGRESS: at sentence #910000, processed 86818510 words, keeping 709250 word types
2021-09-29 15:52:03,325 : INFO : PROGRESS: at sentence #920000, processed 87525406 words, keeping 711820 word types
2021-09-29 15:52:04,456 : INFO : PROGRESS: at sentence #930000, processed 88390961 words, keeping 716278 word types
2021-09-29 15:52:05,932 : INFO : PROGRESS: at sentence #940000, processed 89521569 words, keeping 721182 word types
2021-09-29 15:52:07,446 : INFO : PROGRESS: at sentence #950000, processed 90683265 words, keeping 726458 word types
2021-09-29 15:52:08,986 : INFO : PROGRESS: at sentence #960000, processed 91833857 words, keeping 730935 word types
2021-09-29 15:52:10,513 : INFO : PROGRESS: at sentence #970000, processed 92996895 words, keeping 735274 word types
2021-09-29 15:52:11,981 : INFO : PROGRESS: at sentence #980000, processed 94125957 words, keeping 738796 word types
2021-09-29 15:52:13,460 : INFO : PROGRESS: at sentence #990000, processed 95256200 words, keeping 742224 word types
2021-09-29 15:52:14,643 : INFO : PROGRESS: at sentence #1000000, processed 96155404 words, keeping 746900 word types
2021-09-29 15:52:14,746 : INFO : PROGRESS: at sentence #1010000, processed 96225885 words, keeping 749366 word types
2021-09-29 15:52:14,849 : INFO : PROGRESS: at sentence #1020000, processed 96296616 words, keeping 750634 word types
2021-09-29 15:52:14,886 : INFO : collected 752320 word types from a corpus of 96321721 raw words and 1023403 sentences
2021-09-29 15:52:14,886 : INFO : Loading a fresh vocabulary
2021-09-29 15:52:15,444 : INFO : effective_min_count=2 retains 331256 unique words (44% of original 752320, drops 421064)
2021-09-29 15:52:15,444 : INFO : effective_min_count=2 leaves 95900657 word corpus (99% of original 96321721, drops 421064)
2021-09-29 15:52:15,913 : INFO : deleting the raw counts dictionary of 752320 items
2021-09-29 15:52:15,924 : INFO : sample=0.001 downsamples 36 most-common words
2021-09-29 15:52:15,924 : INFO : downsampling leaves estimated 70188603 word corpus (73.2% of prior 95900657)
2021-09-29 15:52:16,431 : INFO : estimated required memory for 331256 words and 200 dimensions: 695637600 bytes
2021-09-29 15:52:16,431 : INFO : resetting layer weights
2021-09-29 15:52:53,653 : INFO : training model with 3 workers on 331256 vocabulary and 200 features, using sg=0 hs=0 sample=0.001 negative=5 window=3
2021-09-29 15:52:54,668 : INFO : EPOCH 1 - PROGRESS: at 0.60% examples, 353233 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:52:55,683 : INFO : EPOCH 1 - PROGRESS: at 1.27% examples, 389152 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:52:56,708 : INFO : EPOCH 1 - PROGRESS: at 1.97% examples, 396269 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:52:57,730 : INFO : EPOCH 1 - PROGRESS: at 2.59% examples, 403605 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:52:58,731 : INFO : EPOCH 1 - PROGRESS: at 3.21% examples, 407308 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:52:59,741 : INFO : EPOCH 1 - PROGRESS: at 3.78% examples, 409099 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:53:00,746 : INFO : EPOCH 1 - PROGRESS: at 4.41% examples, 412563 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:01,753 : INFO : EPOCH 1 - PROGRESS: at 4.94% examples, 413977 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:02,773 : INFO : EPOCH 1 - PROGRESS: at 5.74% examples, 415678 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:03,794 : INFO : EPOCH 1 - PROGRESS: at 6.40% examples, 414278 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:53:04,815 : INFO : EPOCH 1 - PROGRESS: at 7.00% examples, 417390 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:05,818 : INFO : EPOCH 1 - PROGRESS: at 7.34% examples, 419907 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:06,831 : INFO : EPOCH 1 - PROGRESS: at 7.97% examples, 419712 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:53:07,853 : INFO : EPOCH 1 - PROGRESS: at 8.69% examples, 420239 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:53:08,883 : INFO : EPOCH 1 - PROGRESS: at 9.42% examples, 420622 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:53:09,893 : INFO : EPOCH 1 - PROGRESS: at 10.20% examples, 420340 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:10,895 : INFO : EPOCH 1 - PROGRESS: at 10.98% examples, 420227 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:53:11,921 : INFO : EPOCH 1 - PROGRESS: at 11.64% examples, 420232 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:12,951 : INFO : EPOCH 1 - PROGRESS: at 12.37% examples, 419588 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:13,973 : INFO : EPOCH 1 - PROGRESS: at 13.13% examples, 419682 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:53:14,990 : INFO : EPOCH 1 - PROGRESS: at 13.94% examples, 419812 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:53:15,994 : INFO : EPOCH 1 - PROGRESS: at 14.63% examples, 419951 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:17,017 : INFO : EPOCH 1 - PROGRESS: at 15.17% examples, 419728 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:53:18,027 : INFO : EPOCH 1 - PROGRESS: at 15.76% examples, 419996 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:19,031 : INFO : EPOCH 1 - PROGRESS: at 16.37% examples, 419728 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:53:20,035 : INFO : EPOCH 1 - PROGRESS: at 17.04% examples, 420122 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:21,036 : INFO : EPOCH 1 - PROGRESS: at 17.71% examples, 420426 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:22,044 : INFO : EPOCH 1 - PROGRESS: at 18.44% examples, 420254 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:53:23,071 : INFO : EPOCH 1 - PROGRESS: at 19.20% examples, 420307 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:53:24,083 : INFO : EPOCH 1 - PROGRESS: at 19.94% examples, 420029 words/s, in_qsize 5, out_qsize 2
2021-09-29 15:53:25,089 : INFO : EPOCH 1 - PROGRESS: at 20.69% examples, 420376 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:53:26,107 : INFO : EPOCH 1 - PROGRESS: at 21.37% examples, 420412 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:27,121 : INFO : EPOCH 1 - PROGRESS: at 22.01% examples, 420246 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:28,140 : INFO : EPOCH 1 - PROGRESS: at 22.21% examples, 419813 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:53:29,187 : INFO : EPOCH 1 - PROGRESS: at 22.41% examples, 419065 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:53:30,201 : INFO : EPOCH 1 - PROGRESS: at 22.61% examples, 418617 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:53:31,244 : INFO : EPOCH 1 - PROGRESS: at 22.81% examples, 418298 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:53:32,247 : INFO : EPOCH 1 - PROGRESS: at 23.01% examples, 418415 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:33,254 : INFO : EPOCH 1 - PROGRESS: at 23.20% examples, 417597 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:53:34,272 : INFO : EPOCH 1 - PROGRESS: at 23.42% examples, 417578 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:53:35,287 : INFO : EPOCH 1 - PROGRESS: at 23.63% examples, 417397 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:36,303 : INFO : EPOCH 1 - PROGRESS: at 23.82% examples, 416620 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:53:37,338 : INFO : EPOCH 1 - PROGRESS: at 24.03% examples, 416278 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:53:38,355 : INFO : EPOCH 1 - PROGRESS: at 24.26% examples, 416280 words/s, in_qsize 4, out_qsize 2
2021-09-29 15:53:39,362 : INFO : EPOCH 1 - PROGRESS: at 24.52% examples, 416126 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:40,371 : INFO : EPOCH 1 - PROGRESS: at 25.05% examples, 416139 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:41,373 : INFO : EPOCH 1 - PROGRESS: at 25.71% examples, 415985 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:53:42,380 : INFO : EPOCH 1 - PROGRESS: at 26.37% examples, 416459 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:43,425 : INFO : EPOCH 1 - PROGRESS: at 27.13% examples, 416312 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:53:44,430 : INFO : EPOCH 1 - PROGRESS: at 27.86% examples, 416612 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:45,456 : INFO : EPOCH 1 - PROGRESS: at 28.24% examples, 416479 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:53:46,468 : INFO : EPOCH 1 - PROGRESS: at 28.58% examples, 416761 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:47,491 : INFO : EPOCH 1 - PROGRESS: at 28.99% examples, 416669 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:53:48,498 : INFO : EPOCH 1 - PROGRESS: at 29.45% examples, 416891 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:49,507 : INFO : EPOCH 1 - PROGRESS: at 30.01% examples, 416658 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:53:50,522 : INFO : EPOCH 1 - PROGRESS: at 30.68% examples, 416926 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:53:51,548 : INFO : EPOCH 1 - PROGRESS: at 31.30% examples, 416981 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:53:52,561 : INFO : EPOCH 1 - PROGRESS: at 32.08% examples, 417094 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:53:53,581 : INFO : EPOCH 1 - PROGRESS: at 32.91% examples, 417258 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:53:54,600 : INFO : EPOCH 1 - PROGRESS: at 33.70% examples, 417301 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:53:55,602 : INFO : EPOCH 1 - PROGRESS: at 34.50% examples, 417453 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:53:56,621 : INFO : EPOCH 1 - PROGRESS: at 35.32% examples, 417601 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:57,647 : INFO : EPOCH 1 - PROGRESS: at 36.15% examples, 417688 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:53:58,667 : INFO : EPOCH 1 - PROGRESS: at 36.95% examples, 417804 words/s, in_qsize 4, out_qsize 2
2021-09-29 15:53:59,679 : INFO : EPOCH 1 - PROGRESS: at 37.78% examples, 417985 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:00,687 : INFO : EPOCH 1 - PROGRESS: at 38.58% examples, 417955 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:01,692 : INFO : EPOCH 1 - PROGRESS: at 39.31% examples, 418009 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:54:02,698 : INFO : EPOCH 1 - PROGRESS: at 39.85% examples, 417933 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:03,712 : INFO : EPOCH 1 - PROGRESS: at 40.43% examples, 417844 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:54:04,721 : INFO : EPOCH 1 - PROGRESS: at 41.13% examples, 417788 words/s, in_qsize 5, out_qsize 2
2021-09-29 15:54:05,747 : INFO : EPOCH 1 - PROGRESS: at 41.82% examples, 417893 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:54:06,749 : INFO : EPOCH 1 - PROGRESS: at 42.45% examples, 417952 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:54:07,764 : INFO : EPOCH 1 - PROGRESS: at 43.28% examples, 418027 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:08,779 : INFO : EPOCH 1 - PROGRESS: at 43.97% examples, 418161 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:54:09,784 : INFO : EPOCH 1 - PROGRESS: at 44.63% examples, 418049 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:54:10,785 : INFO : EPOCH 1 - PROGRESS: at 45.27% examples, 418358 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:11,793 : INFO : EPOCH 1 - PROGRESS: at 46.07% examples, 418434 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:12,808 : INFO : EPOCH 1 - PROGRESS: at 46.84% examples, 418390 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:54:13,812 : INFO : EPOCH 1 - PROGRESS: at 47.43% examples, 418463 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:14,828 : INFO : EPOCH 1 - PROGRESS: at 48.04% examples, 418603 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:15,843 : INFO : EPOCH 1 - PROGRESS: at 48.69% examples, 418666 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:54:16,858 : INFO : EPOCH 1 - PROGRESS: at 49.24% examples, 418580 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:54:17,863 : INFO : EPOCH 1 - PROGRESS: at 50.00% examples, 418684 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:18,889 : INFO : EPOCH 1 - PROGRESS: at 50.78% examples, 418498 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:54:19,902 : INFO : EPOCH 1 - PROGRESS: at 51.16% examples, 418545 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:20,932 : INFO : EPOCH 1 - PROGRESS: at 51.21% examples, 418463 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:21,962 : INFO : EPOCH 1 - PROGRESS: at 51.68% examples, 418334 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:22,989 : INFO : EPOCH 1 - PROGRESS: at 52.06% examples, 418256 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:24,031 : INFO : EPOCH 1 - PROGRESS: at 52.58% examples, 418013 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:54:25,043 : INFO : EPOCH 1 - PROGRESS: at 52.92% examples, 418019 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:26,049 : INFO : EPOCH 1 - PROGRESS: at 53.21% examples, 418106 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:27,061 : INFO : EPOCH 1 - PROGRESS: at 53.60% examples, 417977 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:54:28,067 : INFO : EPOCH 1 - PROGRESS: at 53.98% examples, 417949 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:54:29,083 : INFO : EPOCH 1 - PROGRESS: at 54.37% examples, 417895 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:54:30,107 : INFO : EPOCH 1 - PROGRESS: at 54.73% examples, 417930 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:31,109 : INFO : EPOCH 1 - PROGRESS: at 55.10% examples, 417916 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:32,123 : INFO : EPOCH 1 - PROGRESS: at 55.53% examples, 417938 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:54:33,152 : INFO : EPOCH 1 - PROGRESS: at 55.99% examples, 417895 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:54:34,171 : INFO : EPOCH 1 - PROGRESS: at 56.39% examples, 417948 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:54:35,201 : INFO : EPOCH 1 - PROGRESS: at 56.74% examples, 417954 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:36,208 : INFO : EPOCH 1 - PROGRESS: at 57.08% examples, 417921 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:54:37,215 : INFO : EPOCH 1 - PROGRESS: at 57.56% examples, 417966 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:38,235 : INFO : EPOCH 1 - PROGRESS: at 58.00% examples, 417888 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:54:39,247 : INFO : EPOCH 1 - PROGRESS: at 58.42% examples, 417944 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:40,255 : INFO : EPOCH 1 - PROGRESS: at 58.95% examples, 417915 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:54:41,263 : INFO : EPOCH 1 - PROGRESS: at 59.66% examples, 418119 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:42,282 : INFO : EPOCH 1 - PROGRESS: at 60.36% examples, 418146 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:43,296 : INFO : EPOCH 1 - PROGRESS: at 61.02% examples, 418198 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:44,300 : INFO : EPOCH 1 - PROGRESS: at 61.70% examples, 418284 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:45,306 : INFO : EPOCH 1 - PROGRESS: at 62.40% examples, 418268 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:46,328 : INFO : EPOCH 1 - PROGRESS: at 63.13% examples, 418331 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:54:47,342 : INFO : EPOCH 1 - PROGRESS: at 63.83% examples, 418170 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:54:48,364 : INFO : EPOCH 1 - PROGRESS: at 64.59% examples, 418318 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:49,398 : INFO : EPOCH 1 - PROGRESS: at 65.27% examples, 418278 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:54:50,404 : INFO : EPOCH 1 - PROGRESS: at 65.84% examples, 418208 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:54:51,425 : INFO : EPOCH 1 - PROGRESS: at 66.41% examples, 418154 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:52,455 : INFO : EPOCH 1 - PROGRESS: at 66.79% examples, 418161 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:54:53,475 : INFO : EPOCH 1 - PROGRESS: at 67.18% examples, 418113 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:54:54,524 : INFO : EPOCH 1 - PROGRESS: at 67.91% examples, 418074 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:54:55,526 : INFO : EPOCH 1 - PROGRESS: at 68.63% examples, 418119 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:56,551 : INFO : EPOCH 1 - PROGRESS: at 69.33% examples, 417968 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:54:57,568 : INFO : EPOCH 1 - PROGRESS: at 70.10% examples, 417891 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:54:58,578 : INFO : EPOCH 1 - PROGRESS: at 71.00% examples, 417959 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:54:59,581 : INFO : EPOCH 1 - PROGRESS: at 71.82% examples, 417865 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:55:00,590 : INFO : EPOCH 1 - PROGRESS: at 72.63% examples, 417913 words/s, in_qsize 4, out_qsize 2
2021-09-29 15:55:01,592 : INFO : EPOCH 1 - PROGRESS: at 73.32% examples, 417926 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:55:02,594 : INFO : EPOCH 1 - PROGRESS: at 73.92% examples, 417874 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:55:03,611 : INFO : EPOCH 1 - PROGRESS: at 74.63% examples, 418036 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:55:04,620 : INFO : EPOCH 1 - PROGRESS: at 75.17% examples, 417976 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:05,633 : INFO : EPOCH 1 - PROGRESS: at 75.68% examples, 417861 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:06,661 : INFO : EPOCH 1 - PROGRESS: at 76.48% examples, 417892 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:55:07,668 : INFO : EPOCH 1 - PROGRESS: at 77.27% examples, 417883 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:08,692 : INFO : EPOCH 1 - PROGRESS: at 78.02% examples, 417955 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:09,703 : INFO : EPOCH 1 - PROGRESS: at 78.75% examples, 417939 words/s, in_qsize 4, out_qsize 2
2021-09-29 15:55:10,710 : INFO : EPOCH 1 - PROGRESS: at 79.42% examples, 418016 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:11,731 : INFO : EPOCH 1 - PROGRESS: at 80.07% examples, 418023 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:55:12,736 : INFO : EPOCH 1 - PROGRESS: at 80.77% examples, 418128 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:13,749 : INFO : EPOCH 1 - PROGRESS: at 81.49% examples, 418089 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:14,759 : INFO : EPOCH 1 - PROGRESS: at 82.26% examples, 418072 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:15,760 : INFO : EPOCH 1 - PROGRESS: at 82.96% examples, 418059 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:16,777 : INFO : EPOCH 1 - PROGRESS: at 83.39% examples, 418006 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:55:17,797 : INFO : EPOCH 1 - PROGRESS: at 84.14% examples, 417949 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:18,848 : INFO : EPOCH 1 - PROGRESS: at 84.89% examples, 417815 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:55:19,848 : INFO : EPOCH 1 - PROGRESS: at 85.70% examples, 417895 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:20,862 : INFO : EPOCH 1 - PROGRESS: at 86.31% examples, 417942 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:21,894 : INFO : EPOCH 1 - PROGRESS: at 86.87% examples, 417820 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:55:22,902 : INFO : EPOCH 1 - PROGRESS: at 87.63% examples, 417943 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:23,920 : INFO : EPOCH 1 - PROGRESS: at 88.31% examples, 417931 words/s, in_qsize 4, out_qsize 2
2021-09-29 15:55:24,933 : INFO : EPOCH 1 - PROGRESS: at 88.92% examples, 417913 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:55:25,946 : INFO : EPOCH 1 - PROGRESS: at 89.77% examples, 418026 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:26,956 : INFO : EPOCH 1 - PROGRESS: at 90.55% examples, 418033 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:55:27,956 : INFO : EPOCH 1 - PROGRESS: at 91.05% examples, 418114 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:28,971 : INFO : EPOCH 1 - PROGRESS: at 91.55% examples, 418101 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:55:29,989 : INFO : EPOCH 1 - PROGRESS: at 92.04% examples, 418121 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:30,998 : INFO : EPOCH 1 - PROGRESS: at 92.53% examples, 418130 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:31,999 : INFO : EPOCH 1 - PROGRESS: at 93.01% examples, 418157 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:55:33,034 : INFO : EPOCH 1 - PROGRESS: at 93.50% examples, 418092 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:55:34,050 : INFO : EPOCH 1 - PROGRESS: at 94.00% examples, 418198 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:55:35,098 : INFO : EPOCH 1 - PROGRESS: at 94.52% examples, 418181 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:36,125 : INFO : EPOCH 1 - PROGRESS: at 95.01% examples, 418171 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:37,172 : INFO : EPOCH 1 - PROGRESS: at 95.50% examples, 418112 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:55:38,196 : INFO : EPOCH 1 - PROGRESS: at 96.05% examples, 418238 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:39,242 : INFO : EPOCH 1 - PROGRESS: at 96.59% examples, 418256 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:40,250 : INFO : EPOCH 1 - PROGRESS: at 97.07% examples, 418303 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:41,283 : INFO : EPOCH 1 - PROGRESS: at 98.49% examples, 418193 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:55:41,340 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-29 15:55:41,343 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-29 15:55:41,347 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-29 15:55:41,347 : INFO : EPOCH - 1 : training on 96321721 raw words (70191398 effective words) took 167.7s, 418570 effective words/s
2021-09-29 15:55:42,374 : INFO : EPOCH 2 - PROGRESS: at 0.64% examples, 377624 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:43,390 : INFO : EPOCH 2 - PROGRESS: at 1.30% examples, 397719 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:55:44,401 : INFO : EPOCH 2 - PROGRESS: at 2.00% examples, 406157 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:55:45,403 : INFO : EPOCH 2 - PROGRESS: at 2.63% examples, 411245 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:46,422 : INFO : EPOCH 2 - PROGRESS: at 3.23% examples, 410538 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:47,434 : INFO : EPOCH 2 - PROGRESS: at 3.81% examples, 412877 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:48,436 : INFO : EPOCH 2 - PROGRESS: at 4.43% examples, 415057 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:49,440 : INFO : EPOCH 2 - PROGRESS: at 4.94% examples, 414408 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:55:50,490 : INFO : EPOCH 2 - PROGRESS: at 5.73% examples, 413898 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:55:51,499 : INFO : EPOCH 2 - PROGRESS: at 6.44% examples, 416063 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:55:52,506 : INFO : EPOCH 2 - PROGRESS: at 7.00% examples, 417600 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:55:53,514 : INFO : EPOCH 2 - PROGRESS: at 7.33% examples, 419298 words/s, in_qsize 4, out_qsize 2
2021-09-29 15:55:54,518 : INFO : EPOCH 2 - PROGRESS: at 7.97% examples, 420022 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:55,539 : INFO : EPOCH 2 - PROGRESS: at 8.63% examples, 418485 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:56,562 : INFO : EPOCH 2 - PROGRESS: at 9.37% examples, 418182 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:55:57,576 : INFO : EPOCH 2 - PROGRESS: at 10.12% examples, 418034 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:55:58,590 : INFO : EPOCH 2 - PROGRESS: at 10.90% examples, 417725 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:55:59,592 : INFO : EPOCH 2 - PROGRESS: at 11.54% examples, 417683 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:56:00,600 : INFO : EPOCH 2 - PROGRESS: at 12.25% examples, 417584 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:01,612 : INFO : EPOCH 2 - PROGRESS: at 13.03% examples, 417981 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:02,633 : INFO : EPOCH 2 - PROGRESS: at 13.81% examples, 417816 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:56:03,661 : INFO : EPOCH 2 - PROGRESS: at 14.53% examples, 417641 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:56:04,668 : INFO : EPOCH 2 - PROGRESS: at 15.09% examples, 417848 words/s, in_qsize 4, out_qsize 2
2021-09-29 15:56:05,684 : INFO : EPOCH 2 - PROGRESS: at 15.66% examples, 417741 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:56:06,701 : INFO : EPOCH 2 - PROGRESS: at 16.28% examples, 417630 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:56:07,722 : INFO : EPOCH 2 - PROGRESS: at 16.93% examples, 417181 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:56:08,733 : INFO : EPOCH 2 - PROGRESS: at 17.59% examples, 418089 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:09,738 : INFO : EPOCH 2 - PROGRESS: at 18.33% examples, 418060 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:10,741 : INFO : EPOCH 2 - PROGRESS: at 19.04% examples, 417767 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:56:11,763 : INFO : EPOCH 2 - PROGRESS: at 19.81% examples, 417838 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:56:12,770 : INFO : EPOCH 2 - PROGRESS: at 20.56% examples, 418051 words/s, in_qsize 4, out_qsize 2
2021-09-29 15:56:13,775 : INFO : EPOCH 2 - PROGRESS: at 21.23% examples, 418316 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:14,827 : INFO : EPOCH 2 - PROGRESS: at 21.95% examples, 417959 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:56:15,858 : INFO : EPOCH 2 - PROGRESS: at 22.18% examples, 417789 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:56:16,884 : INFO : EPOCH 2 - PROGRESS: at 22.38% examples, 417707 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:17,911 : INFO : EPOCH 2 - PROGRESS: at 22.59% examples, 417143 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:56:18,933 : INFO : EPOCH 2 - PROGRESS: at 22.78% examples, 416372 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:56:19,940 : INFO : EPOCH 2 - PROGRESS: at 22.98% examples, 416319 words/s, in_qsize 4, out_qsize 2
2021-09-29 15:56:20,943 : INFO : EPOCH 2 - PROGRESS: at 23.17% examples, 415598 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:21,951 : INFO : EPOCH 2 - PROGRESS: at 23.37% examples, 415225 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:22,962 : INFO : EPOCH 2 - PROGRESS: at 23.57% examples, 414800 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:24,001 : INFO : EPOCH 2 - PROGRESS: at 23.77% examples, 414156 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:56:25,018 : INFO : EPOCH 2 - PROGRESS: at 23.98% examples, 413896 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:56:26,028 : INFO : EPOCH 2 - PROGRESS: at 24.20% examples, 413888 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:56:27,034 : INFO : EPOCH 2 - PROGRESS: at 24.40% examples, 413587 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:28,042 : INFO : EPOCH 2 - PROGRESS: at 24.92% examples, 413748 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:29,056 : INFO : EPOCH 2 - PROGRESS: at 25.51% examples, 413806 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:30,066 : INFO : EPOCH 2 - PROGRESS: at 26.19% examples, 413884 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:56:31,080 : INFO : EPOCH 2 - PROGRESS: at 26.90% examples, 414203 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:32,086 : INFO : EPOCH 2 - PROGRESS: at 27.63% examples, 414233 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:33,131 : INFO : EPOCH 2 - PROGRESS: at 28.16% examples, 414213 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:56:34,156 : INFO : EPOCH 2 - PROGRESS: at 28.45% examples, 414561 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:35,163 : INFO : EPOCH 2 - PROGRESS: at 28.89% examples, 414566 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:36,184 : INFO : EPOCH 2 - PROGRESS: at 29.29% examples, 414632 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:56:37,194 : INFO : EPOCH 2 - PROGRESS: at 29.86% examples, 414784 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:38,223 : INFO : EPOCH 2 - PROGRESS: at 30.51% examples, 414978 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:39,233 : INFO : EPOCH 2 - PROGRESS: at 31.13% examples, 415035 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:40,244 : INFO : EPOCH 2 - PROGRESS: at 31.88% examples, 415196 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:56:41,255 : INFO : EPOCH 2 - PROGRESS: at 32.67% examples, 415354 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:56:42,292 : INFO : EPOCH 2 - PROGRESS: at 33.50% examples, 415430 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:56:43,294 : INFO : EPOCH 2 - PROGRESS: at 34.29% examples, 415609 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:56:44,308 : INFO : EPOCH 2 - PROGRESS: at 35.11% examples, 415821 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:56:45,314 : INFO : EPOCH 2 - PROGRESS: at 35.91% examples, 415840 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:46,330 : INFO : EPOCH 2 - PROGRESS: at 36.69% examples, 415898 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:56:47,357 : INFO : EPOCH 2 - PROGRESS: at 37.51% examples, 416013 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:56:48,359 : INFO : EPOCH 2 - PROGRESS: at 38.32% examples, 416053 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:49,368 : INFO : EPOCH 2 - PROGRESS: at 39.14% examples, 416153 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:50,392 : INFO : EPOCH 2 - PROGRESS: at 39.68% examples, 415977 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:51,399 : INFO : EPOCH 2 - PROGRESS: at 40.22% examples, 415572 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:56:52,428 : INFO : EPOCH 2 - PROGRESS: at 40.93% examples, 415762 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:53,439 : INFO : EPOCH 2 - PROGRESS: at 41.50% examples, 415608 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:56:54,448 : INFO : EPOCH 2 - PROGRESS: at 42.22% examples, 415588 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:56:55,452 : INFO : EPOCH 2 - PROGRESS: at 42.97% examples, 415599 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:56,487 : INFO : EPOCH 2 - PROGRESS: at 43.65% examples, 415340 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:56:57,489 : INFO : EPOCH 2 - PROGRESS: at 44.34% examples, 415567 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:56:58,501 : INFO : EPOCH 2 - PROGRESS: at 44.95% examples, 415554 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:56:59,515 : INFO : EPOCH 2 - PROGRESS: at 45.67% examples, 415630 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:00,528 : INFO : EPOCH 2 - PROGRESS: at 46.48% examples, 415581 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:57:01,537 : INFO : EPOCH 2 - PROGRESS: at 47.09% examples, 415567 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:02,547 : INFO : EPOCH 2 - PROGRESS: at 47.68% examples, 415367 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:57:03,570 : INFO : EPOCH 2 - PROGRESS: at 48.27% examples, 415434 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:57:04,581 : INFO : EPOCH 2 - PROGRESS: at 48.93% examples, 415095 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:57:05,630 : INFO : EPOCH 2 - PROGRESS: at 49.54% examples, 415124 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:57:06,633 : INFO : EPOCH 2 - PROGRESS: at 50.28% examples, 415213 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:57:07,675 : INFO : EPOCH 2 - PROGRESS: at 51.07% examples, 415267 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:57:08,685 : INFO : EPOCH 2 - PROGRESS: at 51.18% examples, 415479 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:57:09,711 : INFO : EPOCH 2 - PROGRESS: at 51.56% examples, 415512 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:57:10,719 : INFO : EPOCH 2 - PROGRESS: at 51.78% examples, 415588 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:11,730 : INFO : EPOCH 2 - PROGRESS: at 52.33% examples, 415488 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:57:12,732 : INFO : EPOCH 2 - PROGRESS: at 52.75% examples, 415545 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:13,733 : INFO : EPOCH 2 - PROGRESS: at 53.07% examples, 415565 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:57:14,754 : INFO : EPOCH 2 - PROGRESS: at 53.40% examples, 415581 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:15,774 : INFO : EPOCH 2 - PROGRESS: at 53.77% examples, 415592 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:57:16,775 : INFO : EPOCH 2 - PROGRESS: at 54.17% examples, 415692 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:17,782 : INFO : EPOCH 2 - PROGRESS: at 54.53% examples, 415619 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:18,790 : INFO : EPOCH 2 - PROGRESS: at 54.89% examples, 415669 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:57:19,797 : INFO : EPOCH 2 - PROGRESS: at 55.29% examples, 415743 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:20,821 : INFO : EPOCH 2 - PROGRESS: at 55.74% examples, 415684 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:57:21,828 : INFO : EPOCH 2 - PROGRESS: at 56.17% examples, 415665 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:22,839 : INFO : EPOCH 2 - PROGRESS: at 56.53% examples, 415564 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:57:23,851 : INFO : EPOCH 2 - PROGRESS: at 56.87% examples, 415666 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:24,859 : INFO : EPOCH 2 - PROGRESS: at 57.20% examples, 415581 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:57:25,869 : INFO : EPOCH 2 - PROGRESS: at 57.77% examples, 415639 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:26,873 : INFO : EPOCH 2 - PROGRESS: at 58.14% examples, 415454 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:57:27,877 : INFO : EPOCH 2 - PROGRESS: at 58.53% examples, 415428 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:28,879 : INFO : EPOCH 2 - PROGRESS: at 59.12% examples, 415324 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:57:29,887 : INFO : EPOCH 2 - PROGRESS: at 59.83% examples, 415412 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:30,888 : INFO : EPOCH 2 - PROGRESS: at 60.50% examples, 415468 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:31,897 : INFO : EPOCH 2 - PROGRESS: at 61.14% examples, 415497 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:57:32,912 : INFO : EPOCH 2 - PROGRESS: at 61.82% examples, 415494 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:57:33,919 : INFO : EPOCH 2 - PROGRESS: at 62.54% examples, 415488 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:34,927 : INFO : EPOCH 2 - PROGRESS: at 63.24% examples, 415439 words/s, in_qsize 4, out_qsize 2
2021-09-29 15:57:35,967 : INFO : EPOCH 2 - PROGRESS: at 63.94% examples, 415339 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:57:36,987 : INFO : EPOCH 2 - PROGRESS: at 64.68% examples, 415461 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:57:38,014 : INFO : EPOCH 2 - PROGRESS: at 65.36% examples, 415524 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:39,040 : INFO : EPOCH 2 - PROGRESS: at 65.92% examples, 415292 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:57:40,041 : INFO : EPOCH 2 - PROGRESS: at 66.45% examples, 415262 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:57:41,062 : INFO : EPOCH 2 - PROGRESS: at 66.84% examples, 415399 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:57:42,106 : INFO : EPOCH 2 - PROGRESS: at 67.24% examples, 415335 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:57:43,134 : INFO : EPOCH 2 - PROGRESS: at 68.02% examples, 415462 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:44,137 : INFO : EPOCH 2 - PROGRESS: at 68.69% examples, 415290 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:57:45,164 : INFO : EPOCH 2 - PROGRESS: at 69.47% examples, 415454 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:57:46,172 : INFO : EPOCH 2 - PROGRESS: at 70.25% examples, 415490 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:47,176 : INFO : EPOCH 2 - PROGRESS: at 71.11% examples, 415528 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:48,183 : INFO : EPOCH 2 - PROGRESS: at 71.99% examples, 415563 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:49,196 : INFO : EPOCH 2 - PROGRESS: at 72.77% examples, 415560 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:57:50,206 : INFO : EPOCH 2 - PROGRESS: at 73.44% examples, 415513 words/s, in_qsize 3, out_qsize 2
2021-09-29 15:57:51,209 : INFO : EPOCH 2 - PROGRESS: at 74.03% examples, 415474 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:57:52,223 : INFO : EPOCH 2 - PROGRESS: at 74.70% examples, 415432 words/s, in_qsize 4, out_qsize 2
2021-09-29 15:57:53,224 : INFO : EPOCH 2 - PROGRESS: at 75.23% examples, 415520 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:57:54,225 : INFO : EPOCH 2 - PROGRESS: at 75.82% examples, 415520 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:55,243 : INFO : EPOCH 2 - PROGRESS: at 76.59% examples, 415543 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:56,254 : INFO : EPOCH 2 - PROGRESS: at 77.37% examples, 415537 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:57:57,262 : INFO : EPOCH 2 - PROGRESS: at 78.09% examples, 415517 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:57:58,277 : INFO : EPOCH 2 - PROGRESS: at 78.81% examples, 415561 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:57:59,282 : INFO : EPOCH 2 - PROGRESS: at 79.48% examples, 415608 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:00,288 : INFO : EPOCH 2 - PROGRESS: at 80.13% examples, 415675 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:58:01,296 : INFO : EPOCH 2 - PROGRESS: at 80.81% examples, 415692 words/s, in_qsize 4, out_qsize 2
2021-09-29 15:58:02,306 : INFO : EPOCH 2 - PROGRESS: at 81.52% examples, 415677 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:03,312 : INFO : EPOCH 2 - PROGRESS: at 82.27% examples, 415531 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:58:04,337 : INFO : EPOCH 2 - PROGRESS: at 82.99% examples, 415668 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:05,355 : INFO : EPOCH 2 - PROGRESS: at 83.44% examples, 415673 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:58:06,356 : INFO : EPOCH 2 - PROGRESS: at 84.21% examples, 415699 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:58:07,390 : INFO : EPOCH 2 - PROGRESS: at 84.94% examples, 415574 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:58:08,402 : INFO : EPOCH 2 - PROGRESS: at 85.75% examples, 415682 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:09,408 : INFO : EPOCH 2 - PROGRESS: at 86.34% examples, 415713 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:10,433 : INFO : EPOCH 2 - PROGRESS: at 86.95% examples, 415678 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:58:11,437 : INFO : EPOCH 2 - PROGRESS: at 87.65% examples, 415675 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:58:12,459 : INFO : EPOCH 2 - PROGRESS: at 88.34% examples, 415670 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:58:13,505 : INFO : EPOCH 2 - PROGRESS: at 88.99% examples, 415727 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:58:14,526 : INFO : EPOCH 2 - PROGRESS: at 89.82% examples, 415777 words/s, in_qsize 5, out_qsize 2
2021-09-29 15:58:15,536 : INFO : EPOCH 2 - PROGRESS: at 90.57% examples, 415759 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:58:16,564 : INFO : EPOCH 2 - PROGRESS: at 91.10% examples, 415920 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:17,577 : INFO : EPOCH 2 - PROGRESS: at 91.61% examples, 415972 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:18,602 : INFO : EPOCH 2 - PROGRESS: at 92.09% examples, 415987 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:58:19,627 : INFO : EPOCH 2 - PROGRESS: at 92.59% examples, 416013 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:20,638 : INFO : EPOCH 2 - PROGRESS: at 93.09% examples, 416075 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:21,648 : INFO : EPOCH 2 - PROGRESS: at 93.58% examples, 416085 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:58:22,680 : INFO : EPOCH 2 - PROGRESS: at 94.08% examples, 416165 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:23,700 : INFO : EPOCH 2 - PROGRESS: at 94.59% examples, 416229 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:58:24,702 : INFO : EPOCH 2 - PROGRESS: at 95.09% examples, 416294 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:58:25,708 : INFO : EPOCH 2 - PROGRESS: at 95.56% examples, 416263 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:26,723 : INFO : EPOCH 2 - PROGRESS: at 96.08% examples, 416286 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:27,728 : INFO : EPOCH 2 - PROGRESS: at 96.61% examples, 416330 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:28,731 : INFO : EPOCH 2 - PROGRESS: at 97.08% examples, 416356 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:29,799 : INFO : EPOCH 2 - PROGRESS: at 98.49% examples, 416127 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:29,875 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-29 15:58:29,883 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-29 15:58:29,886 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-29 15:58:29,886 : INFO : EPOCH - 2 : training on 96321721 raw words (70187353 effective words) took 168.5s, 416448 effective words/s
2021-09-29 15:58:30,897 : INFO : EPOCH 3 - PROGRESS: at 0.61% examples, 361218 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:58:31,907 : INFO : EPOCH 3 - PROGRESS: at 1.27% examples, 390971 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:58:32,914 : INFO : EPOCH 3 - PROGRESS: at 1.98% examples, 402351 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:33,927 : INFO : EPOCH 3 - PROGRESS: at 2.57% examples, 403735 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:58:34,929 : INFO : EPOCH 3 - PROGRESS: at 3.17% examples, 404352 words/s, in_qsize 4, out_qsize 2
2021-09-29 15:58:35,929 : INFO : EPOCH 3 - PROGRESS: at 3.75% examples, 408448 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:36,943 : INFO : EPOCH 3 - PROGRESS: at 4.36% examples, 408558 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:58:37,988 : INFO : EPOCH 3 - PROGRESS: at 4.88% examples, 407548 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:58:38,993 : INFO : EPOCH 3 - PROGRESS: at 5.67% examples, 412080 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:39,996 : INFO : EPOCH 3 - PROGRESS: at 6.37% examples, 413343 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:41,048 : INFO : EPOCH 3 - PROGRESS: at 6.98% examples, 414628 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:42,078 : INFO : EPOCH 3 - PROGRESS: at 7.32% examples, 417075 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:43,085 : INFO : EPOCH 3 - PROGRESS: at 7.93% examples, 417327 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:44,091 : INFO : EPOCH 3 - PROGRESS: at 8.62% examples, 417431 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:45,130 : INFO : EPOCH 3 - PROGRESS: at 9.35% examples, 416297 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:58:46,133 : INFO : EPOCH 3 - PROGRESS: at 10.12% examples, 417398 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:47,149 : INFO : EPOCH 3 - PROGRESS: at 10.91% examples, 417530 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:48,202 : INFO : EPOCH 3 - PROGRESS: at 11.57% examples, 416714 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:58:49,212 : INFO : EPOCH 3 - PROGRESS: at 12.31% examples, 417381 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:50,234 : INFO : EPOCH 3 - PROGRESS: at 13.07% examples, 417222 words/s, in_qsize 4, out_qsize 2
2021-09-29 15:58:51,271 : INFO : EPOCH 3 - PROGRESS: at 13.86% examples, 417101 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:52,284 : INFO : EPOCH 3 - PROGRESS: at 14.55% examples, 416596 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:53,290 : INFO : EPOCH 3 - PROGRESS: at 15.09% examples, 416270 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:58:54,293 : INFO : EPOCH 3 - PROGRESS: at 15.69% examples, 417018 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:55,307 : INFO : EPOCH 3 - PROGRESS: at 16.31% examples, 417247 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:56,329 : INFO : EPOCH 3 - PROGRESS: at 16.98% examples, 417396 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:57,349 : INFO : EPOCH 3 - PROGRESS: at 17.62% examples, 417347 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:58:58,358 : INFO : EPOCH 3 - PROGRESS: at 18.35% examples, 417277 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:58:59,395 : INFO : EPOCH 3 - PROGRESS: at 19.10% examples, 417030 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:59:00,414 : INFO : EPOCH 3 - PROGRESS: at 19.76% examples, 415478 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:59:01,415 : INFO : EPOCH 3 - PROGRESS: at 20.49% examples, 415181 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:59:02,430 : INFO : EPOCH 3 - PROGRESS: at 21.14% examples, 415192 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:59:03,442 : INFO : EPOCH 3 - PROGRESS: at 21.82% examples, 415015 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:04,464 : INFO : EPOCH 3 - PROGRESS: at 22.14% examples, 414776 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:05,471 : INFO : EPOCH 3 - PROGRESS: at 22.33% examples, 414239 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:06,483 : INFO : EPOCH 3 - PROGRESS: at 22.53% examples, 413196 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:59:07,509 : INFO : EPOCH 3 - PROGRESS: at 22.72% examples, 412810 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:59:08,515 : INFO : EPOCH 3 - PROGRESS: at 22.91% examples, 412352 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:09,536 : INFO : EPOCH 3 - PROGRESS: at 23.11% examples, 411918 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:10,544 : INFO : EPOCH 3 - PROGRESS: at 23.29% examples, 410946 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:59:11,548 : INFO : EPOCH 3 - PROGRESS: at 23.50% examples, 411018 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:12,570 : INFO : EPOCH 3 - PROGRESS: at 23.70% examples, 410474 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:59:13,578 : INFO : EPOCH 3 - PROGRESS: at 23.91% examples, 410541 words/s, in_qsize 4, out_qsize 2
2021-09-29 15:59:14,586 : INFO : EPOCH 3 - PROGRESS: at 24.11% examples, 410020 words/s, in_qsize 6, out_qsize 3
2021-09-29 15:59:15,601 : INFO : EPOCH 3 - PROGRESS: at 24.34% examples, 410330 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:16,620 : INFO : EPOCH 3 - PROGRESS: at 24.76% examples, 410275 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:59:17,631 : INFO : EPOCH 3 - PROGRESS: at 25.28% examples, 410402 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:18,655 : INFO : EPOCH 3 - PROGRESS: at 25.95% examples, 410131 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:59:19,660 : INFO : EPOCH 3 - PROGRESS: at 26.63% examples, 410637 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:20,697 : INFO : EPOCH 3 - PROGRESS: at 27.35% examples, 410495 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:59:21,718 : INFO : EPOCH 3 - PROGRESS: at 28.00% examples, 410927 words/s, in_qsize 4, out_qsize 2
2021-09-29 15:59:22,746 : INFO : EPOCH 3 - PROGRESS: at 28.33% examples, 410686 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:59:23,765 : INFO : EPOCH 3 - PROGRESS: at 28.72% examples, 410920 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:59:24,806 : INFO : EPOCH 3 - PROGRESS: at 29.12% examples, 410828 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:59:25,848 : INFO : EPOCH 3 - PROGRESS: at 29.61% examples, 410661 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:59:26,852 : INFO : EPOCH 3 - PROGRESS: at 30.22% examples, 411099 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:27,893 : INFO : EPOCH 3 - PROGRESS: at 30.85% examples, 410754 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:59:28,897 : INFO : EPOCH 3 - PROGRESS: at 31.52% examples, 411177 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:29,909 : INFO : EPOCH 3 - PROGRESS: at 32.29% examples, 411266 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:59:30,920 : INFO : EPOCH 3 - PROGRESS: at 33.13% examples, 411581 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:31,927 : INFO : EPOCH 3 - PROGRESS: at 33.93% examples, 411812 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:32,946 : INFO : EPOCH 3 - PROGRESS: at 34.71% examples, 411821 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:59:33,962 : INFO : EPOCH 3 - PROGRESS: at 35.53% examples, 411975 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:59:34,991 : INFO : EPOCH 3 - PROGRESS: at 36.33% examples, 412098 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:59:36,026 : INFO : EPOCH 3 - PROGRESS: at 37.13% examples, 412098 words/s, in_qsize 6, out_qsize 1
2021-09-29 15:59:37,044 : INFO : EPOCH 3 - PROGRESS: at 37.95% examples, 412328 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:38,063 : INFO : EPOCH 3 - PROGRESS: at 38.78% examples, 412418 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:39,079 : INFO : EPOCH 3 - PROGRESS: at 39.43% examples, 412354 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:59:40,091 : INFO : EPOCH 3 - PROGRESS: at 39.97% examples, 412438 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:41,127 : INFO : EPOCH 3 - PROGRESS: at 40.59% examples, 412239 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:59:42,151 : INFO : EPOCH 3 - PROGRESS: at 41.29% examples, 412578 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:43,161 : INFO : EPOCH 3 - PROGRESS: at 42.01% examples, 412614 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:59:44,188 : INFO : EPOCH 3 - PROGRESS: at 42.67% examples, 412697 words/s, in_qsize 6, out_qsize 0
2021-09-29 15:59:45,190 : INFO : EPOCH 3 - PROGRESS: at 43.48% examples, 412944 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:46,191 : INFO : EPOCH 3 - PROGRESS: at 44.12% examples, 413024 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:47,222 : INFO : EPOCH 3 - PROGRESS: at 44.80% examples, 413046 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:48,228 : INFO : EPOCH 3 - PROGRESS: at 45.44% examples, 413099 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:49,229 : INFO : EPOCH 3 - PROGRESS: at 46.24% examples, 413164 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:59:50,241 : INFO : EPOCH 3 - PROGRESS: at 46.94% examples, 413111 words/s, in_qsize 4, out_qsize 1
2021-09-29 15:59:51,248 : INFO : EPOCH 3 - PROGRESS: at 47.51% examples, 412986 words/s, in_qsize 6, out_qsize 2
2021-09-29 15:59:52,257 : INFO : EPOCH 3 - PROGRESS: at 48.13% examples, 413325 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:53,277 : INFO : EPOCH 3 - PROGRESS: at 48.79% examples, 413366 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:54,286 : INFO : EPOCH 3 - PROGRESS: at 49.35% examples, 413332 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:55,291 : INFO : EPOCH 3 - PROGRESS: at 50.10% examples, 413502 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:56,306 : INFO : EPOCH 3 - PROGRESS: at 50.90% examples, 413529 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:57,320 : INFO : EPOCH 3 - PROGRESS: at 51.17% examples, 413575 words/s, in_qsize 5, out_qsize 1
2021-09-29 15:59:58,341 : INFO : EPOCH 3 - PROGRESS: at 51.26% examples, 413671 words/s, in_qsize 5, out_qsize 0
2021-09-29 15:59:59,344 : INFO : EPOCH 3 - PROGRESS: at 51.69% examples, 413646 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:00,353 : INFO : EPOCH 3 - PROGRESS: at 52.16% examples, 413568 words/s, in_qsize 5, out_qsize 2
2021-09-29 16:00:01,354 : INFO : EPOCH 3 - PROGRESS: at 52.64% examples, 413638 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:02,359 : INFO : EPOCH 3 - PROGRESS: at 52.96% examples, 413658 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:00:03,365 : INFO : EPOCH 3 - PROGRESS: at 53.27% examples, 413709 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:00:04,399 : INFO : EPOCH 3 - PROGRESS: at 53.64% examples, 413757 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:00:05,439 : INFO : EPOCH 3 - PROGRESS: at 54.05% examples, 413634 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:00:06,443 : INFO : EPOCH 3 - PROGRESS: at 54.44% examples, 413815 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:07,452 : INFO : EPOCH 3 - PROGRESS: at 54.77% examples, 413743 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:00:08,472 : INFO : EPOCH 3 - PROGRESS: at 55.16% examples, 413769 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:00:09,473 : INFO : EPOCH 3 - PROGRESS: at 55.59% examples, 413745 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:00:10,484 : INFO : EPOCH 3 - PROGRESS: at 56.02% examples, 413602 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:11,495 : INFO : EPOCH 3 - PROGRESS: at 56.41% examples, 413660 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:12,501 : INFO : EPOCH 3 - PROGRESS: at 56.74% examples, 413589 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:13,516 : INFO : EPOCH 3 - PROGRESS: at 57.07% examples, 413566 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:00:14,531 : INFO : EPOCH 3 - PROGRESS: at 57.55% examples, 413550 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:15,533 : INFO : EPOCH 3 - PROGRESS: at 57.99% examples, 413589 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:16,534 : INFO : EPOCH 3 - PROGRESS: at 58.40% examples, 413591 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:00:17,556 : INFO : EPOCH 3 - PROGRESS: at 58.93% examples, 413615 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:00:18,565 : INFO : EPOCH 3 - PROGRESS: at 59.61% examples, 413716 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:00:19,599 : INFO : EPOCH 3 - PROGRESS: at 60.32% examples, 413791 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:20,606 : INFO : EPOCH 3 - PROGRESS: at 60.97% examples, 413848 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:00:21,608 : INFO : EPOCH 3 - PROGRESS: at 61.68% examples, 413979 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:22,614 : INFO : EPOCH 3 - PROGRESS: at 62.32% examples, 413883 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:23,628 : INFO : EPOCH 3 - PROGRESS: at 63.05% examples, 413926 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:24,628 : INFO : EPOCH 3 - PROGRESS: at 63.75% examples, 413872 words/s, in_qsize 5, out_qsize 2
2021-09-29 16:00:25,637 : INFO : EPOCH 3 - PROGRESS: at 64.46% examples, 413849 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:00:26,661 : INFO : EPOCH 3 - PROGRESS: at 65.17% examples, 413897 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:27,673 : INFO : EPOCH 3 - PROGRESS: at 65.73% examples, 413836 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:00:28,696 : INFO : EPOCH 3 - PROGRESS: at 66.32% examples, 413747 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:00:29,716 : INFO : EPOCH 3 - PROGRESS: at 66.71% examples, 413818 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:30,741 : INFO : EPOCH 3 - PROGRESS: at 67.08% examples, 413686 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:00:31,747 : INFO : EPOCH 3 - PROGRESS: at 67.73% examples, 413835 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:32,747 : INFO : EPOCH 3 - PROGRESS: at 68.43% examples, 413742 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:33,769 : INFO : EPOCH 3 - PROGRESS: at 69.17% examples, 413797 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:34,780 : INFO : EPOCH 3 - PROGRESS: at 69.94% examples, 413781 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:35,800 : INFO : EPOCH 3 - PROGRESS: at 70.75% examples, 413792 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:00:36,826 : INFO : EPOCH 3 - PROGRESS: at 71.64% examples, 413828 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:37,857 : INFO : EPOCH 3 - PROGRESS: at 72.45% examples, 413837 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:00:38,860 : INFO : EPOCH 3 - PROGRESS: at 73.17% examples, 413876 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:00:39,869 : INFO : EPOCH 3 - PROGRESS: at 73.82% examples, 413895 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:00:40,889 : INFO : EPOCH 3 - PROGRESS: at 74.48% examples, 413961 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:00:41,907 : INFO : EPOCH 3 - PROGRESS: at 75.05% examples, 413955 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:00:42,909 : INFO : EPOCH 3 - PROGRESS: at 75.56% examples, 413968 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:00:43,940 : INFO : EPOCH 3 - PROGRESS: at 76.27% examples, 413851 words/s, in_qsize 5, out_qsize 2
2021-09-29 16:00:44,942 : INFO : EPOCH 3 - PROGRESS: at 77.09% examples, 413886 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:45,963 : INFO : EPOCH 3 - PROGRESS: at 77.84% examples, 413938 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:00:47,013 : INFO : EPOCH 3 - PROGRESS: at 78.59% examples, 413845 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:00:48,031 : INFO : EPOCH 3 - PROGRESS: at 79.26% examples, 413962 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:00:49,040 : INFO : EPOCH 3 - PROGRESS: at 79.94% examples, 414101 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:50,056 : INFO : EPOCH 3 - PROGRESS: at 80.58% examples, 414082 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:00:51,068 : INFO : EPOCH 3 - PROGRESS: at 81.32% examples, 414121 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:52,070 : INFO : EPOCH 3 - PROGRESS: at 82.03% examples, 414117 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:00:53,081 : INFO : EPOCH 3 - PROGRESS: at 82.82% examples, 414198 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:54,094 : INFO : EPOCH 3 - PROGRESS: at 83.31% examples, 414235 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:55,095 : INFO : EPOCH 3 - PROGRESS: at 83.99% examples, 414255 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:00:56,101 : INFO : EPOCH 3 - PROGRESS: at 84.75% examples, 414293 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:57,104 : INFO : EPOCH 3 - PROGRESS: at 85.55% examples, 414285 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:58,104 : INFO : EPOCH 3 - PROGRESS: at 86.15% examples, 414333 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:00:59,146 : INFO : EPOCH 3 - PROGRESS: at 86.68% examples, 414273 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:01:00,159 : INFO : EPOCH 3 - PROGRESS: at 87.47% examples, 414414 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:01,180 : INFO : EPOCH 3 - PROGRESS: at 88.13% examples, 414415 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:02,184 : INFO : EPOCH 3 - PROGRESS: at 88.77% examples, 414425 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:01:03,199 : INFO : EPOCH 3 - PROGRESS: at 89.55% examples, 414387 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:01:04,210 : INFO : EPOCH 3 - PROGRESS: at 90.34% examples, 414449 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:01:05,257 : INFO : EPOCH 3 - PROGRESS: at 90.90% examples, 414429 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:01:06,305 : INFO : EPOCH 3 - PROGRESS: at 91.45% examples, 414539 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:07,312 : INFO : EPOCH 3 - PROGRESS: at 91.93% examples, 414613 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:08,314 : INFO : EPOCH 3 - PROGRESS: at 92.41% examples, 414654 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:01:09,322 : INFO : EPOCH 3 - PROGRESS: at 92.90% examples, 414731 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:10,337 : INFO : EPOCH 3 - PROGRESS: at 93.41% examples, 414787 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:11,352 : INFO : EPOCH 3 - PROGRESS: at 93.90% examples, 414828 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:12,362 : INFO : EPOCH 3 - PROGRESS: at 94.39% examples, 414893 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:13,368 : INFO : EPOCH 3 - PROGRESS: at 94.87% examples, 414863 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:14,398 : INFO : EPOCH 3 - PROGRESS: at 95.37% examples, 414865 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:01:15,409 : INFO : EPOCH 3 - PROGRESS: at 95.89% examples, 414959 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:01:16,455 : INFO : EPOCH 3 - PROGRESS: at 96.40% examples, 414912 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:01:17,479 : INFO : EPOCH 3 - PROGRESS: at 96.92% examples, 415066 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:01:18,489 : INFO : EPOCH 3 - PROGRESS: at 97.62% examples, 415124 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:18,832 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-29 16:01:18,836 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-29 16:01:18,842 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-29 16:01:18,842 : INFO : EPOCH - 3 : training on 96321721 raw words (70189014 effective words) took 169.0s, 415429 effective words/s
2021-09-29 16:01:19,848 : INFO : EPOCH 4 - PROGRESS: at 0.62% examples, 370703 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:01:20,872 : INFO : EPOCH 4 - PROGRESS: at 1.29% examples, 396543 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:01:21,884 : INFO : EPOCH 4 - PROGRESS: at 1.99% examples, 402867 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:01:22,887 : INFO : EPOCH 4 - PROGRESS: at 2.58% examples, 405177 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:23,888 : INFO : EPOCH 4 - PROGRESS: at 3.18% examples, 405674 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:24,908 : INFO : EPOCH 4 - PROGRESS: at 3.75% examples, 407101 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:25,929 : INFO : EPOCH 4 - PROGRESS: at 4.37% examples, 407969 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:01:26,946 : INFO : EPOCH 4 - PROGRESS: at 4.90% examples, 410295 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:27,973 : INFO : EPOCH 4 - PROGRESS: at 5.66% examples, 410252 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:01:28,974 : INFO : EPOCH 4 - PROGRESS: at 6.38% examples, 413250 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:30,014 : INFO : EPOCH 4 - PROGRESS: at 6.96% examples, 412347 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:01:31,029 : INFO : EPOCH 4 - PROGRESS: at 7.31% examples, 416130 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:32,073 : INFO : EPOCH 4 - PROGRESS: at 7.91% examples, 415321 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:01:33,100 : INFO : EPOCH 4 - PROGRESS: at 8.63% examples, 416514 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:34,103 : INFO : EPOCH 4 - PROGRESS: at 9.37% examples, 416864 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:35,121 : INFO : EPOCH 4 - PROGRESS: at 10.12% examples, 416652 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:01:36,143 : INFO : EPOCH 4 - PROGRESS: at 10.91% examples, 416704 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:01:37,157 : INFO : EPOCH 4 - PROGRESS: at 11.57% examples, 416802 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:38,167 : INFO : EPOCH 4 - PROGRESS: at 12.31% examples, 417472 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:01:39,172 : INFO : EPOCH 4 - PROGRESS: at 13.04% examples, 416962 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:01:40,184 : INFO : EPOCH 4 - PROGRESS: at 13.85% examples, 417699 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:41,202 : INFO : EPOCH 4 - PROGRESS: at 14.55% examples, 417405 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:01:42,217 : INFO : EPOCH 4 - PROGRESS: at 15.11% examples, 417793 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:43,231 : INFO : EPOCH 4 - PROGRESS: at 15.70% examples, 418013 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:44,231 : INFO : EPOCH 4 - PROGRESS: at 16.31% examples, 417867 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:01:45,235 : INFO : EPOCH 4 - PROGRESS: at 16.99% examples, 418556 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:46,245 : INFO : EPOCH 4 - PROGRESS: at 17.64% examples, 418850 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:47,251 : INFO : EPOCH 4 - PROGRESS: at 18.37% examples, 418768 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:01:48,262 : INFO : EPOCH 4 - PROGRESS: at 19.14% examples, 419112 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:49,269 : INFO : EPOCH 4 - PROGRESS: at 19.89% examples, 419144 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:50,279 : INFO : EPOCH 4 - PROGRESS: at 20.63% examples, 419262 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:51,295 : INFO : EPOCH 4 - PROGRESS: at 21.29% examples, 419135 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:01:52,303 : INFO : EPOCH 4 - PROGRESS: at 21.98% examples, 418863 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:53,312 : INFO : EPOCH 4 - PROGRESS: at 22.18% examples, 418492 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:01:54,361 : INFO : EPOCH 4 - PROGRESS: at 22.38% examples, 417746 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:01:55,365 : INFO : EPOCH 4 - PROGRESS: at 22.59% examples, 417629 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:01:56,379 : INFO : EPOCH 4 - PROGRESS: at 22.78% examples, 417109 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:01:57,410 : INFO : EPOCH 4 - PROGRESS: at 22.98% examples, 416596 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:01:58,426 : INFO : EPOCH 4 - PROGRESS: at 23.17% examples, 416078 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:01:59,431 : INFO : EPOCH 4 - PROGRESS: at 23.39% examples, 416216 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:00,443 : INFO : EPOCH 4 - PROGRESS: at 23.59% examples, 415769 words/s, in_qsize 4, out_qsize 3
2021-09-29 16:02:01,449 : INFO : EPOCH 4 - PROGRESS: at 23.79% examples, 415601 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:02:02,471 : INFO : EPOCH 4 - PROGRESS: at 24.00% examples, 415248 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:03,475 : INFO : EPOCH 4 - PROGRESS: at 24.21% examples, 414799 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:02:04,493 : INFO : EPOCH 4 - PROGRESS: at 24.42% examples, 414524 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:02:05,499 : INFO : EPOCH 4 - PROGRESS: at 24.94% examples, 414564 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:06,523 : INFO : EPOCH 4 - PROGRESS: at 25.55% examples, 414503 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:02:07,551 : INFO : EPOCH 4 - PROGRESS: at 26.23% examples, 414563 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:02:08,585 : INFO : EPOCH 4 - PROGRESS: at 26.93% examples, 414406 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:02:09,622 : INFO : EPOCH 4 - PROGRESS: at 27.67% examples, 414314 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:02:10,662 : INFO : EPOCH 4 - PROGRESS: at 28.18% examples, 414445 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:02:11,681 : INFO : EPOCH 4 - PROGRESS: at 28.45% examples, 414304 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:02:12,682 : INFO : EPOCH 4 - PROGRESS: at 28.89% examples, 414480 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:02:13,710 : INFO : EPOCH 4 - PROGRESS: at 29.28% examples, 414258 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:02:14,717 : INFO : EPOCH 4 - PROGRESS: at 29.84% examples, 414291 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:02:15,729 : INFO : EPOCH 4 - PROGRESS: at 30.49% examples, 414620 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:16,743 : INFO : EPOCH 4 - PROGRESS: at 31.13% examples, 414911 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:17,762 : INFO : EPOCH 4 - PROGRESS: at 31.86% examples, 414888 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:02:18,771 : INFO : EPOCH 4 - PROGRESS: at 32.66% examples, 415069 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:19,788 : INFO : EPOCH 4 - PROGRESS: at 33.47% examples, 415163 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:02:20,788 : INFO : EPOCH 4 - PROGRESS: at 34.28% examples, 415471 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:21,793 : INFO : EPOCH 4 - PROGRESS: at 35.07% examples, 415524 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:02:22,812 : INFO : EPOCH 4 - PROGRESS: at 35.88% examples, 415578 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:02:23,827 : INFO : EPOCH 4 - PROGRESS: at 36.68% examples, 415749 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:24,841 : INFO : EPOCH 4 - PROGRESS: at 37.48% examples, 415837 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:02:25,860 : INFO : EPOCH 4 - PROGRESS: at 38.30% examples, 415877 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:02:26,874 : INFO : EPOCH 4 - PROGRESS: at 39.12% examples, 415949 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:27,881 : INFO : EPOCH 4 - PROGRESS: at 39.68% examples, 415879 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:28,933 : INFO : EPOCH 4 - PROGRESS: at 40.24% examples, 415519 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:02:29,950 : INFO : EPOCH 4 - PROGRESS: at 40.95% examples, 415676 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:02:30,967 : INFO : EPOCH 4 - PROGRESS: at 41.55% examples, 415791 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:31,980 : INFO : EPOCH 4 - PROGRESS: at 42.23% examples, 415446 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:02:32,995 : INFO : EPOCH 4 - PROGRESS: at 43.03% examples, 415697 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:02:34,005 : INFO : EPOCH 4 - PROGRESS: at 43.73% examples, 415971 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:35,021 : INFO : EPOCH 4 - PROGRESS: at 44.43% examples, 416016 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:36,047 : INFO : EPOCH 4 - PROGRESS: at 45.03% examples, 416118 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:37,054 : INFO : EPOCH 4 - PROGRESS: at 45.77% examples, 416198 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:38,071 : INFO : EPOCH 4 - PROGRESS: at 46.60% examples, 416053 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:02:39,078 : INFO : EPOCH 4 - PROGRESS: at 47.15% examples, 415848 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:02:40,079 : INFO : EPOCH 4 - PROGRESS: at 47.81% examples, 416269 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:41,096 : INFO : EPOCH 4 - PROGRESS: at 48.43% examples, 416429 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:42,108 : INFO : EPOCH 4 - PROGRESS: at 49.07% examples, 416197 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:43,120 : INFO : EPOCH 4 - PROGRESS: at 49.68% examples, 416153 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:44,123 : INFO : EPOCH 4 - PROGRESS: at 50.42% examples, 416172 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:45,123 : INFO : EPOCH 4 - PROGRESS: at 51.12% examples, 416365 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:02:46,135 : INFO : EPOCH 4 - PROGRESS: at 51.19% examples, 416480 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:47,153 : INFO : EPOCH 4 - PROGRESS: at 51.66% examples, 416558 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:48,210 : INFO : EPOCH 4 - PROGRESS: at 51.82% examples, 416482 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:02:49,215 : INFO : EPOCH 4 - PROGRESS: at 52.43% examples, 416571 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:50,237 : INFO : EPOCH 4 - PROGRESS: at 52.83% examples, 416605 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:51,255 : INFO : EPOCH 4 - PROGRESS: at 53.14% examples, 416609 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:02:52,258 : INFO : EPOCH 4 - PROGRESS: at 53.48% examples, 416609 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:02:53,260 : INFO : EPOCH 4 - PROGRESS: at 53.86% examples, 416602 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:54,280 : INFO : EPOCH 4 - PROGRESS: at 54.26% examples, 416624 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:55,286 : INFO : EPOCH 4 - PROGRESS: at 54.62% examples, 416616 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:02:56,287 : INFO : EPOCH 4 - PROGRESS: at 54.97% examples, 416608 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:57,288 : INFO : EPOCH 4 - PROGRESS: at 55.38% examples, 416619 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:58,293 : INFO : EPOCH 4 - PROGRESS: at 55.85% examples, 416625 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:02:59,294 : INFO : EPOCH 4 - PROGRESS: at 56.24% examples, 416547 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:03:00,308 : INFO : EPOCH 4 - PROGRESS: at 56.60% examples, 416571 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:03:01,320 : INFO : EPOCH 4 - PROGRESS: at 56.94% examples, 416590 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:03:02,322 : INFO : EPOCH 4 - PROGRESS: at 57.27% examples, 416520 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:03:03,323 : INFO : EPOCH 4 - PROGRESS: at 57.83% examples, 416536 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:03:04,345 : INFO : EPOCH 4 - PROGRESS: at 58.22% examples, 416279 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:03:05,374 : INFO : EPOCH 4 - PROGRESS: at 58.62% examples, 416273 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:03:06,385 : INFO : EPOCH 4 - PROGRESS: at 59.34% examples, 416498 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:03:07,390 : INFO : EPOCH 4 - PROGRESS: at 60.05% examples, 416581 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:03:08,402 : INFO : EPOCH 4 - PROGRESS: at 60.73% examples, 416729 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:03:09,403 : INFO : EPOCH 4 - PROGRESS: at 61.38% examples, 416779 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:03:10,420 : INFO : EPOCH 4 - PROGRESS: at 62.06% examples, 416787 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:03:11,430 : INFO : EPOCH 4 - PROGRESS: at 62.78% examples, 416718 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:03:12,432 : INFO : EPOCH 4 - PROGRESS: at 63.54% examples, 416841 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:03:13,456 : INFO : EPOCH 4 - PROGRESS: at 64.23% examples, 416787 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:03:14,485 : INFO : EPOCH 4 - PROGRESS: at 64.98% examples, 416988 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:03:15,502 : INFO : EPOCH 4 - PROGRESS: at 65.58% examples, 416882 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:03:16,518 : INFO : EPOCH 4 - PROGRESS: at 66.17% examples, 416728 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:03:17,529 : INFO : EPOCH 4 - PROGRESS: at 66.61% examples, 416732 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:03:18,545 : INFO : EPOCH 4 - PROGRESS: at 66.96% examples, 416627 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:03:19,562 : INFO : EPOCH 4 - PROGRESS: at 67.52% examples, 416704 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:03:20,565 : INFO : EPOCH 4 - PROGRESS: at 68.22% examples, 416586 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:03:21,569 : INFO : EPOCH 4 - PROGRESS: at 68.91% examples, 416470 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:03:22,594 : INFO : EPOCH 4 - PROGRESS: at 69.68% examples, 416515 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:03:23,606 : INFO : EPOCH 4 - PROGRESS: at 70.47% examples, 416588 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:03:24,625 : INFO : EPOCH 4 - PROGRESS: at 71.36% examples, 416628 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:03:25,652 : INFO : EPOCH 4 - PROGRESS: at 72.19% examples, 416571 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:03:26,664 : INFO : EPOCH 4 - PROGRESS: at 72.95% examples, 416515 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:03:27,694 : INFO : EPOCH 4 - PROGRESS: at 73.61% examples, 416497 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:03:28,737 : INFO : EPOCH 4 - PROGRESS: at 74.26% examples, 416458 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:03:29,739 : INFO : EPOCH 4 - PROGRESS: at 74.89% examples, 416612 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:03:30,741 : INFO : EPOCH 4 - PROGRESS: at 75.45% examples, 416614 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:03:31,763 : INFO : EPOCH 4 - PROGRESS: at 76.11% examples, 416655 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:03:32,796 : INFO : EPOCH 4 - PROGRESS: at 76.93% examples, 416574 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:03:33,847 : INFO : EPOCH 4 - PROGRESS: at 77.67% examples, 416552 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:03:34,867 : INFO : EPOCH 4 - PROGRESS: at 78.47% examples, 416648 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:03:35,871 : INFO : EPOCH 4 - PROGRESS: at 79.13% examples, 416632 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:03:36,881 : INFO : EPOCH 4 - PROGRESS: at 79.79% examples, 416695 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:03:37,892 : INFO : EPOCH 4 - PROGRESS: at 80.41% examples, 416661 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:03:38,903 : INFO : EPOCH 4 - PROGRESS: at 81.15% examples, 416690 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:03:39,918 : INFO : EPOCH 4 - PROGRESS: at 81.86% examples, 416696 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:03:40,925 : INFO : EPOCH 4 - PROGRESS: at 82.65% examples, 416616 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:03:41,926 : INFO : EPOCH 4 - PROGRESS: at 83.21% examples, 416810 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:03:42,929 : INFO : EPOCH 4 - PROGRESS: at 83.84% examples, 416852 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:03:43,945 : INFO : EPOCH 4 - PROGRESS: at 84.63% examples, 416910 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:03:44,963 : INFO : EPOCH 4 - PROGRESS: at 85.43% examples, 416932 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:03:46,011 : INFO : EPOCH 4 - PROGRESS: at 86.06% examples, 416882 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:03:47,016 : INFO : EPOCH 4 - PROGRESS: at 86.61% examples, 416959 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:03:48,020 : INFO : EPOCH 4 - PROGRESS: at 87.38% examples, 417062 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:03:49,060 : INFO : EPOCH 4 - PROGRESS: at 88.04% examples, 417036 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:03:50,090 : INFO : EPOCH 4 - PROGRESS: at 88.74% examples, 417138 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:03:51,097 : INFO : EPOCH 4 - PROGRESS: at 89.55% examples, 417252 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:03:52,108 : INFO : EPOCH 4 - PROGRESS: at 90.34% examples, 417293 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:03:53,132 : INFO : EPOCH 4 - PROGRESS: at 90.88% examples, 417223 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:03:54,138 : INFO : EPOCH 4 - PROGRESS: at 91.42% examples, 417381 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:03:55,145 : INFO : EPOCH 4 - PROGRESS: at 91.89% examples, 417347 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:03:56,156 : INFO : EPOCH 4 - PROGRESS: at 92.38% examples, 417442 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:03:57,177 : INFO : EPOCH 4 - PROGRESS: at 92.86% examples, 417370 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:03:58,201 : INFO : EPOCH 4 - PROGRESS: at 93.40% examples, 417525 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:03:59,230 : INFO : EPOCH 4 - PROGRESS: at 93.88% examples, 417464 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:04:00,233 : INFO : EPOCH 4 - PROGRESS: at 94.38% examples, 417584 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:04:01,257 : INFO : EPOCH 4 - PROGRESS: at 94.86% examples, 417529 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:04:02,265 : INFO : EPOCH 4 - PROGRESS: at 95.38% examples, 417658 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:04:03,274 : INFO : EPOCH 4 - PROGRESS: at 95.90% examples, 417741 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:04,299 : INFO : EPOCH 4 - PROGRESS: at 96.40% examples, 417642 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:04:05,329 : INFO : EPOCH 4 - PROGRESS: at 96.90% examples, 417674 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:04:06,340 : INFO : EPOCH 4 - PROGRESS: at 97.59% examples, 417757 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:04:06,717 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-29 16:04:06,720 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-29 16:04:06,724 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-29 16:04:06,724 : INFO : EPOCH - 4 : training on 96321721 raw words (70185678 effective words) took 167.9s, 418068 effective words/s
2021-09-29 16:04:07,732 : INFO : EPOCH 5 - PROGRESS: at 0.62% examples, 369631 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:04:08,768 : INFO : EPOCH 5 - PROGRESS: at 1.28% examples, 390281 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:04:09,788 : INFO : EPOCH 5 - PROGRESS: at 2.00% examples, 404728 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:04:10,799 : INFO : EPOCH 5 - PROGRESS: at 2.63% examples, 409245 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:04:11,810 : INFO : EPOCH 5 - PROGRESS: at 3.21% examples, 406698 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:04:12,825 : INFO : EPOCH 5 - PROGRESS: at 3.82% examples, 413043 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:13,846 : INFO : EPOCH 5 - PROGRESS: at 4.43% examples, 413032 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:04:14,848 : INFO : EPOCH 5 - PROGRESS: at 4.96% examples, 414539 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:15,860 : INFO : EPOCH 5 - PROGRESS: at 5.75% examples, 416550 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:04:16,885 : INFO : EPOCH 5 - PROGRESS: at 6.47% examples, 417807 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:04:17,900 : INFO : EPOCH 5 - PROGRESS: at 7.02% examples, 419566 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:18,906 : INFO : EPOCH 5 - PROGRESS: at 7.35% examples, 421186 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:04:19,927 : INFO : EPOCH 5 - PROGRESS: at 8.02% examples, 421152 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:04:20,938 : INFO : EPOCH 5 - PROGRESS: at 8.71% examples, 420856 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:04:21,965 : INFO : EPOCH 5 - PROGRESS: at 9.44% examples, 421281 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:22,970 : INFO : EPOCH 5 - PROGRESS: at 10.23% examples, 421027 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:23,997 : INFO : EPOCH 5 - PROGRESS: at 11.02% examples, 420727 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:04:25,006 : INFO : EPOCH 5 - PROGRESS: at 11.64% examples, 419934 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:26,027 : INFO : EPOCH 5 - PROGRESS: at 12.32% examples, 418356 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:27,030 : INFO : EPOCH 5 - PROGRESS: at 13.05% examples, 417846 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:04:28,056 : INFO : EPOCH 5 - PROGRESS: at 13.85% examples, 417900 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:29,065 : INFO : EPOCH 5 - PROGRESS: at 14.53% examples, 417088 words/s, in_qsize 5, out_qsize 2
2021-09-29 16:04:30,076 : INFO : EPOCH 5 - PROGRESS: at 15.09% examples, 417240 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:31,106 : INFO : EPOCH 5 - PROGRESS: at 15.66% examples, 416926 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:04:32,113 : INFO : EPOCH 5 - PROGRESS: at 16.27% examples, 416714 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:04:33,137 : INFO : EPOCH 5 - PROGRESS: at 16.95% examples, 417086 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:34,152 : INFO : EPOCH 5 - PROGRESS: at 17.58% examples, 417136 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:04:35,161 : INFO : EPOCH 5 - PROGRESS: at 18.31% examples, 417055 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:36,183 : INFO : EPOCH 5 - PROGRESS: at 19.04% examples, 416814 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:04:37,197 : INFO : EPOCH 5 - PROGRESS: at 19.82% examples, 417265 words/s, in_qsize 3, out_qsize 1
2021-09-29 16:04:38,214 : INFO : EPOCH 5 - PROGRESS: at 20.56% examples, 417115 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:39,233 : INFO : EPOCH 5 - PROGRESS: at 21.23% examples, 417242 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:40,240 : INFO : EPOCH 5 - PROGRESS: at 21.91% examples, 416812 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:04:41,245 : INFO : EPOCH 5 - PROGRESS: at 22.16% examples, 416835 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:42,267 : INFO : EPOCH 5 - PROGRESS: at 22.37% examples, 416476 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:43,281 : INFO : EPOCH 5 - PROGRESS: at 22.56% examples, 415889 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:04:44,295 : INFO : EPOCH 5 - PROGRESS: at 22.76% examples, 415409 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:04:45,299 : INFO : EPOCH 5 - PROGRESS: at 22.95% examples, 415057 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:46,312 : INFO : EPOCH 5 - PROGRESS: at 23.15% examples, 414793 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:47,332 : INFO : EPOCH 5 - PROGRESS: at 23.36% examples, 414635 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:48,333 : INFO : EPOCH 5 - PROGRESS: at 23.55% examples, 413861 words/s, in_qsize 4, out_qsize 3
2021-09-29 16:04:49,333 : INFO : EPOCH 5 - PROGRESS: at 23.75% examples, 413613 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:50,338 : INFO : EPOCH 5 - PROGRESS: at 23.95% examples, 413155 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:04:51,351 : INFO : EPOCH 5 - PROGRESS: at 24.17% examples, 412841 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:04:52,363 : INFO : EPOCH 5 - PROGRESS: at 24.37% examples, 412356 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:04:53,386 : INFO : EPOCH 5 - PROGRESS: at 24.85% examples, 412790 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:54,390 : INFO : EPOCH 5 - PROGRESS: at 25.41% examples, 412786 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:55,400 : INFO : EPOCH 5 - PROGRESS: at 26.07% examples, 412583 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:04:56,422 : INFO : EPOCH 5 - PROGRESS: at 26.76% examples, 412882 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:04:57,425 : INFO : EPOCH 5 - PROGRESS: at 27.50% examples, 412959 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:04:58,456 : INFO : EPOCH 5 - PROGRESS: at 28.10% examples, 413237 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:04:59,467 : INFO : EPOCH 5 - PROGRESS: at 28.37% examples, 412942 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:05:00,491 : INFO : EPOCH 5 - PROGRESS: at 28.78% examples, 412783 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:05:01,497 : INFO : EPOCH 5 - PROGRESS: at 29.17% examples, 412843 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:05:02,525 : INFO : EPOCH 5 - PROGRESS: at 29.68% examples, 412772 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:05:03,560 : INFO : EPOCH 5 - PROGRESS: at 30.30% examples, 412952 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:05:04,574 : INFO : EPOCH 5 - PROGRESS: at 30.97% examples, 413399 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:05,596 : INFO : EPOCH 5 - PROGRESS: at 31.65% examples, 413396 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:06,604 : INFO : EPOCH 5 - PROGRESS: at 32.43% examples, 413481 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:05:07,634 : INFO : EPOCH 5 - PROGRESS: at 33.24% examples, 413398 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:05:08,650 : INFO : EPOCH 5 - PROGRESS: at 34.02% examples, 413408 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:05:09,652 : INFO : EPOCH 5 - PROGRESS: at 34.82% examples, 413623 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:10,661 : INFO : EPOCH 5 - PROGRESS: at 35.63% examples, 413669 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:05:11,668 : INFO : EPOCH 5 - PROGRESS: at 36.40% examples, 413696 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:12,708 : INFO : EPOCH 5 - PROGRESS: at 37.22% examples, 413867 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:13,728 : INFO : EPOCH 5 - PROGRESS: at 38.04% examples, 413948 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:05:14,749 : INFO : EPOCH 5 - PROGRESS: at 38.87% examples, 414105 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:05:15,762 : INFO : EPOCH 5 - PROGRESS: at 39.53% examples, 414232 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:16,767 : INFO : EPOCH 5 - PROGRESS: at 40.04% examples, 414113 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:05:17,780 : INFO : EPOCH 5 - PROGRESS: at 40.72% examples, 414148 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:05:18,789 : INFO : EPOCH 5 - PROGRESS: at 41.34% examples, 414343 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:19,804 : INFO : EPOCH 5 - PROGRESS: at 42.08% examples, 414318 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:20,806 : INFO : EPOCH 5 - PROGRESS: at 42.73% examples, 414336 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:21,831 : INFO : EPOCH 5 - PROGRESS: at 43.52% examples, 414433 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:22,840 : INFO : EPOCH 5 - PROGRESS: at 44.17% examples, 414454 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:05:23,857 : INFO : EPOCH 5 - PROGRESS: at 44.83% examples, 414424 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:05:24,867 : INFO : EPOCH 5 - PROGRESS: at 45.50% examples, 414631 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:25,872 : INFO : EPOCH 5 - PROGRESS: at 46.31% examples, 414655 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:05:26,900 : INFO : EPOCH 5 - PROGRESS: at 47.01% examples, 414748 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:05:27,910 : INFO : EPOCH 5 - PROGRESS: at 47.58% examples, 414530 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:05:28,936 : INFO : EPOCH 5 - PROGRESS: at 48.20% examples, 414669 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:29,962 : INFO : EPOCH 5 - PROGRESS: at 48.85% examples, 414541 words/s, in_qsize 5, out_qsize 2
2021-09-29 16:05:30,971 : INFO : EPOCH 5 - PROGRESS: at 49.43% examples, 414522 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:05:31,986 : INFO : EPOCH 5 - PROGRESS: at 50.15% examples, 414545 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:32,987 : INFO : EPOCH 5 - PROGRESS: at 50.95% examples, 414552 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:05:34,018 : INFO : EPOCH 5 - PROGRESS: at 51.17% examples, 414637 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:05:35,028 : INFO : EPOCH 5 - PROGRESS: at 51.32% examples, 414641 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:05:36,032 : INFO : EPOCH 5 - PROGRESS: at 51.70% examples, 414758 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:37,034 : INFO : EPOCH 5 - PROGRESS: at 52.22% examples, 414696 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:38,059 : INFO : EPOCH 5 - PROGRESS: at 52.67% examples, 414569 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:05:39,066 : INFO : EPOCH 5 - PROGRESS: at 53.00% examples, 414812 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:40,077 : INFO : EPOCH 5 - PROGRESS: at 53.32% examples, 414820 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:41,103 : INFO : EPOCH 5 - PROGRESS: at 53.67% examples, 414810 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:05:42,107 : INFO : EPOCH 5 - PROGRESS: at 54.09% examples, 414765 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:05:43,149 : INFO : EPOCH 5 - PROGRESS: at 54.46% examples, 414766 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:44,175 : INFO : EPOCH 5 - PROGRESS: at 54.81% examples, 414686 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:05:45,186 : INFO : EPOCH 5 - PROGRESS: at 55.20% examples, 414740 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:46,201 : INFO : EPOCH 5 - PROGRESS: at 55.64% examples, 414720 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:47,201 : INFO : EPOCH 5 - PROGRESS: at 56.09% examples, 414747 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:48,208 : INFO : EPOCH 5 - PROGRESS: at 56.46% examples, 414817 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:49,230 : INFO : EPOCH 5 - PROGRESS: at 56.80% examples, 414740 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:05:50,253 : INFO : EPOCH 5 - PROGRESS: at 57.14% examples, 414744 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:05:51,294 : INFO : EPOCH 5 - PROGRESS: at 57.71% examples, 414760 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:52,307 : INFO : EPOCH 5 - PROGRESS: at 58.08% examples, 414742 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:05:53,316 : INFO : EPOCH 5 - PROGRESS: at 58.47% examples, 414569 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:05:54,332 : INFO : EPOCH 5 - PROGRESS: at 59.07% examples, 414759 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:55,352 : INFO : EPOCH 5 - PROGRESS: at 59.79% examples, 414875 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:56,353 : INFO : EPOCH 5 - PROGRESS: at 60.47% examples, 414937 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:05:57,354 : INFO : EPOCH 5 - PROGRESS: at 61.12% examples, 415067 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:05:58,374 : INFO : EPOCH 5 - PROGRESS: at 61.80% examples, 415107 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:05:59,384 : INFO : EPOCH 5 - PROGRESS: at 62.53% examples, 415092 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:06:00,421 : INFO : EPOCH 5 - PROGRESS: at 63.26% examples, 415072 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:06:01,435 : INFO : EPOCH 5 - PROGRESS: at 63.97% examples, 415133 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:06:02,468 : INFO : EPOCH 5 - PROGRESS: at 64.71% examples, 415273 words/s, in_qsize 4, out_qsize 3
2021-09-29 16:06:03,485 : INFO : EPOCH 5 - PROGRESS: at 65.38% examples, 415313 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:06:04,498 : INFO : EPOCH 5 - PROGRESS: at 65.97% examples, 415307 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:05,501 : INFO : EPOCH 5 - PROGRESS: at 66.48% examples, 415270 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:06,518 : INFO : EPOCH 5 - PROGRESS: at 66.85% examples, 415243 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:07,547 : INFO : EPOCH 5 - PROGRESS: at 67.25% examples, 415228 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:08,556 : INFO : EPOCH 5 - PROGRESS: at 67.96% examples, 415068 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:09,556 : INFO : EPOCH 5 - PROGRESS: at 68.65% examples, 414905 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:06:10,571 : INFO : EPOCH 5 - PROGRESS: at 69.38% examples, 414936 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:11,576 : INFO : EPOCH 5 - PROGRESS: at 70.11% examples, 414810 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:06:12,590 : INFO : EPOCH 5 - PROGRESS: at 71.00% examples, 414828 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:13,592 : INFO : EPOCH 5 - PROGRESS: at 71.83% examples, 414822 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:14,596 : INFO : EPOCH 5 - PROGRESS: at 72.62% examples, 414804 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:15,597 : INFO : EPOCH 5 - PROGRESS: at 73.30% examples, 414786 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:06:16,604 : INFO : EPOCH 5 - PROGRESS: at 73.92% examples, 414857 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:17,622 : INFO : EPOCH 5 - PROGRESS: at 74.57% examples, 414749 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:06:18,625 : INFO : EPOCH 5 - PROGRESS: at 75.16% examples, 414901 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:19,647 : INFO : EPOCH 5 - PROGRESS: at 75.69% examples, 414894 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:06:20,648 : INFO : EPOCH 5 - PROGRESS: at 76.45% examples, 414927 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:06:21,672 : INFO : EPOCH 5 - PROGRESS: at 77.26% examples, 414939 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:06:22,710 : INFO : EPOCH 5 - PROGRESS: at 77.99% examples, 414887 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:23,749 : INFO : EPOCH 5 - PROGRESS: at 78.71% examples, 414807 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:06:24,792 : INFO : EPOCH 5 - PROGRESS: at 79.38% examples, 414793 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:06:25,818 : INFO : EPOCH 5 - PROGRESS: at 80.06% examples, 414921 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:06:26,827 : INFO : EPOCH 5 - PROGRESS: at 80.73% examples, 414931 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:27,880 : INFO : EPOCH 5 - PROGRESS: at 81.45% examples, 414797 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:06:28,905 : INFO : EPOCH 5 - PROGRESS: at 82.25% examples, 414860 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:29,909 : INFO : EPOCH 5 - PROGRESS: at 82.93% examples, 414757 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:06:30,915 : INFO : EPOCH 5 - PROGRESS: at 83.38% examples, 414810 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:31,928 : INFO : EPOCH 5 - PROGRESS: at 84.12% examples, 414797 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:32,964 : INFO : EPOCH 5 - PROGRESS: at 84.87% examples, 414780 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:33,973 : INFO : EPOCH 5 - PROGRESS: at 85.69% examples, 414857 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:35,015 : INFO : EPOCH 5 - PROGRESS: at 86.29% examples, 414790 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:06:36,029 : INFO : EPOCH 5 - PROGRESS: at 86.90% examples, 414936 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:37,047 : INFO : EPOCH 5 - PROGRESS: at 87.63% examples, 414953 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:38,058 : INFO : EPOCH 5 - PROGRESS: at 88.30% examples, 414934 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:06:39,098 : INFO : EPOCH 5 - PROGRESS: at 88.94% examples, 414961 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:06:40,098 : INFO : EPOCH 5 - PROGRESS: at 89.77% examples, 415078 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:06:41,116 : INFO : EPOCH 5 - PROGRESS: at 90.55% examples, 415134 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:42,130 : INFO : EPOCH 5 - PROGRESS: at 91.03% examples, 415054 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:43,160 : INFO : EPOCH 5 - PROGRESS: at 91.55% examples, 415112 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:44,177 : INFO : EPOCH 5 - PROGRESS: at 92.04% examples, 415152 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:45,199 : INFO : EPOCH 5 - PROGRESS: at 92.54% examples, 415192 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:46,215 : INFO : EPOCH 5 - PROGRESS: at 93.00% examples, 415108 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:06:47,220 : INFO : EPOCH 5 - PROGRESS: at 93.51% examples, 415231 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:48,234 : INFO : EPOCH 5 - PROGRESS: at 93.98% examples, 415177 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:06:49,249 : INFO : EPOCH 5 - PROGRESS: at 94.50% examples, 415309 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:06:50,266 : INFO : EPOCH 5 - PROGRESS: at 95.00% examples, 415389 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:06:51,313 : INFO : EPOCH 5 - PROGRESS: at 95.50% examples, 415392 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:06:52,360 : INFO : EPOCH 5 - PROGRESS: at 96.05% examples, 415473 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:06:53,368 : INFO : EPOCH 5 - PROGRESS: at 96.59% examples, 415603 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:06:54,378 : INFO : EPOCH 5 - PROGRESS: at 97.08% examples, 415702 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:06:55,389 : INFO : EPOCH 5 - PROGRESS: at 98.77% examples, 415717 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:06:55,441 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-29 16:06:55,446 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-29 16:06:55,447 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-29 16:06:55,447 : INFO : EPOCH - 5 : training on 96321721 raw words (70190282 effective words) took 168.7s, 416011 effective words/s
2021-09-29 16:06:56,447 : INFO : EPOCH 6 - PROGRESS: at 0.61% examples, 365033 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:06:57,463 : INFO : EPOCH 6 - PROGRESS: at 1.28% examples, 395600 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:06:58,472 : INFO : EPOCH 6 - PROGRESS: at 1.99% examples, 405053 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:06:59,489 : INFO : EPOCH 6 - PROGRESS: at 2.60% examples, 407109 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:07:00,526 : INFO : EPOCH 6 - PROGRESS: at 3.21% examples, 407206 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:07:01,572 : INFO : EPOCH 6 - PROGRESS: at 3.79% examples, 407824 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:07:02,580 : INFO : EPOCH 6 - PROGRESS: at 4.42% examples, 411269 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:07:03,608 : INFO : EPOCH 6 - PROGRESS: at 4.95% examples, 411707 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:07:04,618 : INFO : EPOCH 6 - PROGRESS: at 5.74% examples, 413247 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:07:05,630 : INFO : EPOCH 6 - PROGRESS: at 6.43% examples, 413987 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:07:06,640 : INFO : EPOCH 6 - PROGRESS: at 7.00% examples, 416185 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:07:07,692 : INFO : EPOCH 6 - PROGRESS: at 7.33% examples, 417077 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:07:08,695 : INFO : EPOCH 6 - PROGRESS: at 7.98% examples, 417964 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:07:09,705 : INFO : EPOCH 6 - PROGRESS: at 8.67% examples, 417921 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:07:10,723 : INFO : EPOCH 6 - PROGRESS: at 9.39% examples, 417803 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:07:11,726 : INFO : EPOCH 6 - PROGRESS: at 10.16% examples, 417905 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:07:12,737 : INFO : EPOCH 6 - PROGRESS: at 10.91% examples, 416916 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:07:13,745 : INFO : EPOCH 6 - PROGRESS: at 11.58% examples, 417526 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:07:14,773 : INFO : EPOCH 6 - PROGRESS: at 12.32% examples, 417771 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:07:15,797 : INFO : EPOCH 6 - PROGRESS: at 13.09% examples, 417926 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:07:16,822 : INFO : EPOCH 6 - PROGRESS: at 13.88% examples, 417642 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:07:17,826 : INFO : EPOCH 6 - PROGRESS: at 14.59% examples, 417913 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:07:18,853 : INFO : EPOCH 6 - PROGRESS: at 15.12% examples, 417445 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:07:19,884 : INFO : EPOCH 6 - PROGRESS: at 15.68% examples, 416489 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:07:20,891 : INFO : EPOCH 6 - PROGRESS: at 16.31% examples, 416870 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:07:21,905 : INFO : EPOCH 6 - PROGRESS: at 16.96% examples, 416604 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:07:22,925 : INFO : EPOCH 6 - PROGRESS: at 17.59% examples, 416573 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:07:23,939 : INFO : EPOCH 6 - PROGRESS: at 18.34% examples, 416719 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:07:24,944 : INFO : EPOCH 6 - PROGRESS: at 19.04% examples, 416206 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:07:25,956 : INFO : EPOCH 6 - PROGRESS: at 19.81% examples, 416458 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:07:26,965 : INFO : EPOCH 6 - PROGRESS: at 20.54% examples, 416230 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:07:27,975 : INFO : EPOCH 6 - PROGRESS: at 21.18% examples, 416060 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:07:28,976 : INFO : EPOCH 6 - PROGRESS: at 21.89% examples, 416191 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:07:30,014 : INFO : EPOCH 6 - PROGRESS: at 22.15% examples, 415666 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:07:31,026 : INFO : EPOCH 6 - PROGRESS: at 22.35% examples, 415053 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:07:32,047 : INFO : EPOCH 6 - PROGRESS: at 22.55% examples, 414603 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:07:33,069 : INFO : EPOCH 6 - PROGRESS: at 22.74% examples, 413876 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:07:34,094 : INFO : EPOCH 6 - PROGRESS: at 22.94% examples, 413527 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:07:35,104 : INFO : EPOCH 6 - PROGRESS: at 23.13% examples, 413163 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:07:36,126 : INFO : EPOCH 6 - PROGRESS: at 23.34% examples, 412859 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:07:37,147 : INFO : EPOCH 6 - PROGRESS: at 23.55% examples, 413073 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:07:38,174 : INFO : EPOCH 6 - PROGRESS: at 23.75% examples, 412432 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:07:39,192 : INFO : EPOCH 6 - PROGRESS: at 23.96% examples, 412197 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:07:40,210 : INFO : EPOCH 6 - PROGRESS: at 24.19% examples, 412448 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:07:41,219 : INFO : EPOCH 6 - PROGRESS: at 24.39% examples, 412168 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:07:42,228 : INFO : EPOCH 6 - PROGRESS: at 24.88% examples, 412157 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:07:43,237 : INFO : EPOCH 6 - PROGRESS: at 25.47% examples, 412438 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:07:44,262 : INFO : EPOCH 6 - PROGRESS: at 26.15% examples, 412416 words/s, in_qsize 5, out_qsize 2
2021-09-29 16:07:45,266 : INFO : EPOCH 6 - PROGRESS: at 26.81% examples, 412412 words/s, in_qsize 5, out_qsize 2
2021-09-29 16:07:46,267 : INFO : EPOCH 6 - PROGRESS: at 27.57% examples, 412793 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:07:47,293 : INFO : EPOCH 6 - PROGRESS: at 28.14% examples, 413093 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:07:48,317 : INFO : EPOCH 6 - PROGRESS: at 28.42% examples, 413207 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:07:49,333 : INFO : EPOCH 6 - PROGRESS: at 28.86% examples, 413197 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:07:50,335 : INFO : EPOCH 6 - PROGRESS: at 29.24% examples, 413319 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:07:51,347 : INFO : EPOCH 6 - PROGRESS: at 29.79% examples, 413406 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:07:52,377 : INFO : EPOCH 6 - PROGRESS: at 30.43% examples, 413627 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:07:53,380 : INFO : EPOCH 6 - PROGRESS: at 31.07% examples, 413877 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:07:54,394 : INFO : EPOCH 6 - PROGRESS: at 31.78% examples, 413921 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:07:55,403 : INFO : EPOCH 6 - PROGRESS: at 32.55% examples, 413994 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:07:56,416 : INFO : EPOCH 6 - PROGRESS: at 33.38% examples, 414135 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:07:57,419 : INFO : EPOCH 6 - PROGRESS: at 34.17% examples, 414316 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:07:58,427 : INFO : EPOCH 6 - PROGRESS: at 34.96% examples, 414378 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:07:59,460 : INFO : EPOCH 6 - PROGRESS: at 35.76% examples, 414256 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:08:00,465 : INFO : EPOCH 6 - PROGRESS: at 36.55% examples, 414508 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:08:01,473 : INFO : EPOCH 6 - PROGRESS: at 37.36% examples, 414650 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:02,504 : INFO : EPOCH 6 - PROGRESS: at 38.19% examples, 414752 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:08:03,533 : INFO : EPOCH 6 - PROGRESS: at 39.01% examples, 414746 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:04,540 : INFO : EPOCH 6 - PROGRESS: at 39.60% examples, 414582 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:05,543 : INFO : EPOCH 6 - PROGRESS: at 40.10% examples, 414462 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:06,545 : INFO : EPOCH 6 - PROGRESS: at 40.76% examples, 414168 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:07,553 : INFO : EPOCH 6 - PROGRESS: at 41.35% examples, 414171 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:08,593 : INFO : EPOCH 6 - PROGRESS: at 42.08% examples, 413912 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:08:09,627 : INFO : EPOCH 6 - PROGRESS: at 42.73% examples, 413755 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:10,670 : INFO : EPOCH 6 - PROGRESS: at 43.52% examples, 413762 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:08:11,670 : INFO : EPOCH 6 - PROGRESS: at 44.20% examples, 414029 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:12,694 : INFO : EPOCH 6 - PROGRESS: at 44.86% examples, 414067 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:13,704 : INFO : EPOCH 6 - PROGRESS: at 45.53% examples, 414188 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:08:14,718 : INFO : EPOCH 6 - PROGRESS: at 46.31% examples, 413980 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:08:15,724 : INFO : EPOCH 6 - PROGRESS: at 46.97% examples, 413755 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:08:16,737 : INFO : EPOCH 6 - PROGRESS: at 47.56% examples, 413788 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:17,741 : INFO : EPOCH 6 - PROGRESS: at 48.16% examples, 413960 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:08:18,749 : INFO : EPOCH 6 - PROGRESS: at 48.84% examples, 414114 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:08:19,753 : INFO : EPOCH 6 - PROGRESS: at 49.41% examples, 414120 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:08:20,768 : INFO : EPOCH 6 - PROGRESS: at 50.14% examples, 414153 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:08:21,778 : INFO : EPOCH 6 - PROGRESS: at 50.96% examples, 414288 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:08:22,778 : INFO : EPOCH 6 - PROGRESS: at 51.17% examples, 414514 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:08:23,825 : INFO : EPOCH 6 - PROGRESS: at 51.39% examples, 414596 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:24,873 : INFO : EPOCH 6 - PROGRESS: at 51.75% examples, 414671 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:25,895 : INFO : EPOCH 6 - PROGRESS: at 52.28% examples, 414686 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:08:26,900 : INFO : EPOCH 6 - PROGRESS: at 52.71% examples, 414660 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:27,939 : INFO : EPOCH 6 - PROGRESS: at 53.04% examples, 414677 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:08:28,958 : INFO : EPOCH 6 - PROGRESS: at 53.37% examples, 414712 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:08:29,964 : INFO : EPOCH 6 - PROGRESS: at 53.71% examples, 414639 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:08:30,980 : INFO : EPOCH 6 - PROGRESS: at 54.13% examples, 414615 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:08:32,001 : INFO : EPOCH 6 - PROGRESS: at 54.50% examples, 414636 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:08:33,016 : INFO : EPOCH 6 - PROGRESS: at 54.85% examples, 414600 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:08:34,026 : INFO : EPOCH 6 - PROGRESS: at 55.23% examples, 414594 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:08:35,041 : INFO : EPOCH 6 - PROGRESS: at 55.68% examples, 414578 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:08:36,045 : INFO : EPOCH 6 - PROGRESS: at 56.12% examples, 414592 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:37,050 : INFO : EPOCH 6 - PROGRESS: at 56.49% examples, 414596 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:08:38,070 : INFO : EPOCH 6 - PROGRESS: at 56.82% examples, 414600 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:08:39,078 : INFO : EPOCH 6 - PROGRESS: at 57.16% examples, 414603 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:40,097 : INFO : EPOCH 6 - PROGRESS: at 57.72% examples, 414565 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:41,099 : INFO : EPOCH 6 - PROGRESS: at 58.09% examples, 414532 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:08:42,108 : INFO : EPOCH 6 - PROGRESS: at 58.50% examples, 414635 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:43,119 : INFO : EPOCH 6 - PROGRESS: at 59.10% examples, 414642 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:44,133 : INFO : EPOCH 6 - PROGRESS: at 59.79% examples, 414645 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:08:45,157 : INFO : EPOCH 6 - PROGRESS: at 60.49% examples, 414759 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:46,175 : INFO : EPOCH 6 - PROGRESS: at 61.14% examples, 414826 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:08:47,190 : INFO : EPOCH 6 - PROGRESS: at 61.83% examples, 414894 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:48,195 : INFO : EPOCH 6 - PROGRESS: at 62.55% examples, 414902 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:49,204 : INFO : EPOCH 6 - PROGRESS: at 63.27% examples, 414911 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:08:50,223 : INFO : EPOCH 6 - PROGRESS: at 63.97% examples, 414894 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:08:51,251 : INFO : EPOCH 6 - PROGRESS: at 64.66% examples, 414801 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:08:52,276 : INFO : EPOCH 6 - PROGRESS: at 65.32% examples, 414691 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:08:53,276 : INFO : EPOCH 6 - PROGRESS: at 65.83% examples, 414303 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:54,281 : INFO : EPOCH 6 - PROGRESS: at 66.36% examples, 413971 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:08:55,281 : INFO : EPOCH 6 - PROGRESS: at 66.72% examples, 413869 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:08:56,284 : INFO : EPOCH 6 - PROGRESS: at 67.10% examples, 413934 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:08:57,318 : INFO : EPOCH 6 - PROGRESS: at 67.73% examples, 413807 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:08:58,340 : INFO : EPOCH 6 - PROGRESS: at 68.48% examples, 413872 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:08:59,350 : INFO : EPOCH 6 - PROGRESS: at 69.15% examples, 413674 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:09:00,365 : INFO : EPOCH 6 - PROGRESS: at 69.95% examples, 413763 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:09:01,395 : INFO : EPOCH 6 - PROGRESS: at 70.77% examples, 413742 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:09:02,430 : INFO : EPOCH 6 - PROGRESS: at 71.64% examples, 413688 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:09:03,457 : INFO : EPOCH 6 - PROGRESS: at 72.39% examples, 413484 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:09:04,460 : INFO : EPOCH 6 - PROGRESS: at 73.08% examples, 413256 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:09:05,491 : INFO : EPOCH 6 - PROGRESS: at 73.72% examples, 413211 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:09:06,505 : INFO : EPOCH 6 - PROGRESS: at 74.33% examples, 413131 words/s, in_qsize 3, out_qsize 2
2021-09-29 16:09:07,536 : INFO : EPOCH 6 - PROGRESS: at 74.90% examples, 412944 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:09:08,587 : INFO : EPOCH 6 - PROGRESS: at 75.45% examples, 412767 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:09:09,601 : INFO : EPOCH 6 - PROGRESS: at 76.11% examples, 412861 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:09:10,605 : INFO : EPOCH 6 - PROGRESS: at 76.90% examples, 412791 words/s, in_qsize 5, out_qsize 2
2021-09-29 16:09:11,629 : INFO : EPOCH 6 - PROGRESS: at 77.64% examples, 412877 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:09:12,636 : INFO : EPOCH 6 - PROGRESS: at 78.41% examples, 412935 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:09:13,646 : INFO : EPOCH 6 - PROGRESS: at 79.10% examples, 412976 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:09:14,671 : INFO : EPOCH 6 - PROGRESS: at 79.76% examples, 413023 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:09:15,711 : INFO : EPOCH 6 - PROGRESS: at 80.39% examples, 412979 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:09:16,726 : INFO : EPOCH 6 - PROGRESS: at 81.15% examples, 413125 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:09:17,728 : INFO : EPOCH 6 - PROGRESS: at 81.86% examples, 413191 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:09:18,734 : INFO : EPOCH 6 - PROGRESS: at 82.67% examples, 413244 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:09:19,750 : INFO : EPOCH 6 - PROGRESS: at 83.20% examples, 413265 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:09:20,753 : INFO : EPOCH 6 - PROGRESS: at 83.83% examples, 413383 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:09:21,766 : INFO : EPOCH 6 - PROGRESS: at 84.62% examples, 413424 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:09:22,779 : INFO : EPOCH 6 - PROGRESS: at 85.36% examples, 413335 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:09:23,796 : INFO : EPOCH 6 - PROGRESS: at 86.03% examples, 413448 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:09:24,818 : INFO : EPOCH 6 - PROGRESS: at 86.57% examples, 413453 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:09:25,831 : INFO : EPOCH 6 - PROGRESS: at 87.33% examples, 413501 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:09:26,847 : INFO : EPOCH 6 - PROGRESS: at 87.98% examples, 413565 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:09:27,848 : INFO : EPOCH 6 - PROGRESS: at 88.65% examples, 413516 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:09:28,851 : INFO : EPOCH 6 - PROGRESS: at 89.39% examples, 413682 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:09:29,864 : INFO : EPOCH 6 - PROGRESS: at 90.20% examples, 413732 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:09:30,865 : INFO : EPOCH 6 - PROGRESS: at 90.81% examples, 413847 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:09:31,889 : INFO : EPOCH 6 - PROGRESS: at 91.32% examples, 413793 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:09:32,914 : INFO : EPOCH 6 - PROGRESS: at 91.81% examples, 413873 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:09:33,918 : INFO : EPOCH 6 - PROGRESS: at 92.31% examples, 414004 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:09:34,933 : INFO : EPOCH 6 - PROGRESS: at 92.81% examples, 414064 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:09:35,940 : INFO : EPOCH 6 - PROGRESS: at 93.32% examples, 414149 words/s, in_qsize 3, out_qsize 2
2021-09-29 16:09:36,963 : INFO : EPOCH 6 - PROGRESS: at 93.80% examples, 414172 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:09:37,975 : INFO : EPOCH 6 - PROGRESS: at 94.31% examples, 414325 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:09:38,983 : INFO : EPOCH 6 - PROGRESS: at 94.80% examples, 414337 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:09:39,989 : INFO : EPOCH 6 - PROGRESS: at 95.30% examples, 414407 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:09:41,023 : INFO : EPOCH 6 - PROGRESS: at 95.83% examples, 414533 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:09:42,039 : INFO : EPOCH 6 - PROGRESS: at 96.33% examples, 414519 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:09:43,064 : INFO : EPOCH 6 - PROGRESS: at 96.85% examples, 414625 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:09:44,081 : INFO : EPOCH 6 - PROGRESS: at 97.48% examples, 414625 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:09:44,616 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-29 16:09:44,625 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-29 16:09:44,626 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-29 16:09:44,626 : INFO : EPOCH - 6 : training on 96321721 raw words (70190327 effective words) took 169.2s, 414887 effective words/s
2021-09-29 16:09:45,643 : INFO : EPOCH 7 - PROGRESS: at 0.56% examples, 330445 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:09:46,644 : INFO : EPOCH 7 - PROGRESS: at 1.20% examples, 369833 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:09:47,654 : INFO : EPOCH 7 - PROGRESS: at 1.87% examples, 375487 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:09:48,677 : INFO : EPOCH 7 - PROGRESS: at 2.46% examples, 383399 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:09:49,686 : INFO : EPOCH 7 - PROGRESS: at 3.04% examples, 385991 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:09:50,696 : INFO : EPOCH 7 - PROGRESS: at 3.64% examples, 393541 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:09:51,705 : INFO : EPOCH 7 - PROGRESS: at 4.27% examples, 398120 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:09:52,728 : INFO : EPOCH 7 - PROGRESS: at 4.80% examples, 399481 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:09:53,739 : INFO : EPOCH 7 - PROGRESS: at 5.48% examples, 401177 words/s, in_qsize 5, out_qsize 2
2021-09-29 16:09:54,759 : INFO : EPOCH 7 - PROGRESS: at 6.24% examples, 404477 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:09:55,777 : INFO : EPOCH 7 - PROGRESS: at 6.90% examples, 405700 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:09:56,805 : INFO : EPOCH 7 - PROGRESS: at 7.23% examples, 408358 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:09:57,837 : INFO : EPOCH 7 - PROGRESS: at 7.76% examples, 408813 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:09:58,854 : INFO : EPOCH 7 - PROGRESS: at 8.47% examples, 410685 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:09:59,878 : INFO : EPOCH 7 - PROGRESS: at 9.22% examples, 411367 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:10:00,901 : INFO : EPOCH 7 - PROGRESS: at 9.97% examples, 411926 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:10:01,910 : INFO : EPOCH 7 - PROGRESS: at 10.72% examples, 410859 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:10:02,937 : INFO : EPOCH 7 - PROGRESS: at 11.41% examples, 411435 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:03,939 : INFO : EPOCH 7 - PROGRESS: at 12.08% examples, 411316 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:10:04,944 : INFO : EPOCH 7 - PROGRESS: at 12.87% examples, 411856 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:05,960 : INFO : EPOCH 7 - PROGRESS: at 13.65% examples, 412420 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:06,973 : INFO : EPOCH 7 - PROGRESS: at 14.38% examples, 412504 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:07,985 : INFO : EPOCH 7 - PROGRESS: at 14.94% examples, 412248 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:10:09,006 : INFO : EPOCH 7 - PROGRESS: at 15.51% examples, 411975 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:10:10,024 : INFO : EPOCH 7 - PROGRESS: at 16.09% examples, 412121 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:10:11,035 : INFO : EPOCH 7 - PROGRESS: at 16.76% examples, 412373 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:12,049 : INFO : EPOCH 7 - PROGRESS: at 17.38% examples, 412286 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:10:13,050 : INFO : EPOCH 7 - PROGRESS: at 18.07% examples, 412722 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:10:14,052 : INFO : EPOCH 7 - PROGRESS: at 18.80% examples, 412648 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:15,087 : INFO : EPOCH 7 - PROGRESS: at 19.52% examples, 412140 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:10:16,103 : INFO : EPOCH 7 - PROGRESS: at 20.27% examples, 412004 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:10:17,108 : INFO : EPOCH 7 - PROGRESS: at 20.96% examples, 412054 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:18,113 : INFO : EPOCH 7 - PROGRESS: at 21.59% examples, 412053 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:19,131 : INFO : EPOCH 7 - PROGRESS: at 22.09% examples, 411801 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:10:20,134 : INFO : EPOCH 7 - PROGRESS: at 22.27% examples, 411567 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:10:21,175 : INFO : EPOCH 7 - PROGRESS: at 22.48% examples, 411184 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:10:22,182 : INFO : EPOCH 7 - PROGRESS: at 22.68% examples, 411391 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:23,200 : INFO : EPOCH 7 - PROGRESS: at 22.87% examples, 410657 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:10:24,206 : INFO : EPOCH 7 - PROGRESS: at 23.07% examples, 410951 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:25,225 : INFO : EPOCH 7 - PROGRESS: at 23.27% examples, 410570 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:10:26,234 : INFO : EPOCH 7 - PROGRESS: at 23.48% examples, 410477 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:27,245 : INFO : EPOCH 7 - PROGRESS: at 23.68% examples, 410332 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:10:28,250 : INFO : EPOCH 7 - PROGRESS: at 23.89% examples, 410276 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:29,301 : INFO : EPOCH 7 - PROGRESS: at 24.10% examples, 409657 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:10:30,319 : INFO : EPOCH 7 - PROGRESS: at 24.32% examples, 409821 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:31,339 : INFO : EPOCH 7 - PROGRESS: at 24.72% examples, 409717 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:32,355 : INFO : EPOCH 7 - PROGRESS: at 25.21% examples, 409820 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:10:33,374 : INFO : EPOCH 7 - PROGRESS: at 25.93% examples, 410056 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:34,421 : INFO : EPOCH 7 - PROGRESS: at 26.60% examples, 410211 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:10:35,426 : INFO : EPOCH 7 - PROGRESS: at 27.35% examples, 410616 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:36,452 : INFO : EPOCH 7 - PROGRESS: at 27.99% examples, 410731 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:10:37,466 : INFO : EPOCH 7 - PROGRESS: at 28.32% examples, 410737 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:10:38,498 : INFO : EPOCH 7 - PROGRESS: at 28.74% examples, 411254 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:39,516 : INFO : EPOCH 7 - PROGRESS: at 29.13% examples, 411228 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:10:40,524 : INFO : EPOCH 7 - PROGRESS: at 29.64% examples, 411567 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:41,543 : INFO : EPOCH 7 - PROGRESS: at 30.21% examples, 411360 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:10:42,554 : INFO : EPOCH 7 - PROGRESS: at 30.88% examples, 411735 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:43,560 : INFO : EPOCH 7 - PROGRESS: at 31.52% examples, 411759 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:10:44,572 : INFO : EPOCH 7 - PROGRESS: at 32.32% examples, 412086 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:10:45,580 : INFO : EPOCH 7 - PROGRESS: at 33.15% examples, 412283 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:10:46,585 : INFO : EPOCH 7 - PROGRESS: at 33.96% examples, 412632 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:10:47,591 : INFO : EPOCH 7 - PROGRESS: at 34.75% examples, 412838 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:48,595 : INFO : EPOCH 7 - PROGRESS: at 35.54% examples, 412816 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:49,596 : INFO : EPOCH 7 - PROGRESS: at 36.32% examples, 412886 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:50,613 : INFO : EPOCH 7 - PROGRESS: at 37.10% examples, 412885 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:10:51,623 : INFO : EPOCH 7 - PROGRESS: at 37.90% examples, 412930 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:52,635 : INFO : EPOCH 7 - PROGRESS: at 38.72% examples, 413048 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:10:53,660 : INFO : EPOCH 7 - PROGRESS: at 39.38% examples, 412831 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:10:54,681 : INFO : EPOCH 7 - PROGRESS: at 39.93% examples, 412850 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:10:55,703 : INFO : EPOCH 7 - PROGRESS: at 40.53% examples, 412813 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:56,731 : INFO : EPOCH 7 - PROGRESS: at 41.22% examples, 412827 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:57,771 : INFO : EPOCH 7 - PROGRESS: at 41.94% examples, 412908 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:58,775 : INFO : EPOCH 7 - PROGRESS: at 42.56% examples, 412913 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:10:59,821 : INFO : EPOCH 7 - PROGRESS: at 43.37% examples, 412708 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:11:00,825 : INFO : EPOCH 7 - PROGRESS: at 44.05% examples, 413068 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:01,828 : INFO : EPOCH 7 - PROGRESS: at 44.73% examples, 413138 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:02,840 : INFO : EPOCH 7 - PROGRESS: at 45.37% examples, 413352 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:11:03,852 : INFO : EPOCH 7 - PROGRESS: at 46.17% examples, 413370 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:11:04,855 : INFO : EPOCH 7 - PROGRESS: at 46.90% examples, 413452 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:05,883 : INFO : EPOCH 7 - PROGRESS: at 47.47% examples, 413200 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:11:06,896 : INFO : EPOCH 7 - PROGRESS: at 48.10% examples, 413605 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:07,901 : INFO : EPOCH 7 - PROGRESS: at 48.74% examples, 413571 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:11:08,908 : INFO : EPOCH 7 - PROGRESS: at 49.29% examples, 413602 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:09,920 : INFO : EPOCH 7 - PROGRESS: at 50.01% examples, 413393 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:11:10,958 : INFO : EPOCH 7 - PROGRESS: at 50.82% examples, 413475 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:11:11,962 : INFO : EPOCH 7 - PROGRESS: at 51.17% examples, 413844 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:11:12,971 : INFO : EPOCH 7 - PROGRESS: at 51.22% examples, 413908 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:13,990 : INFO : EPOCH 7 - PROGRESS: at 51.69% examples, 413977 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:14,995 : INFO : EPOCH 7 - PROGRESS: at 52.11% examples, 413823 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:11:16,019 : INFO : EPOCH 7 - PROGRESS: at 52.64% examples, 413945 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:17,025 : INFO : EPOCH 7 - PROGRESS: at 52.96% examples, 414034 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:18,058 : INFO : EPOCH 7 - PROGRESS: at 53.29% examples, 414186 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:19,063 : INFO : EPOCH 7 - PROGRESS: at 53.64% examples, 414134 words/s, in_qsize 5, out_qsize 2
2021-09-29 16:11:20,089 : INFO : EPOCH 7 - PROGRESS: at 54.07% examples, 414218 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:11:21,099 : INFO : EPOCH 7 - PROGRESS: at 54.44% examples, 414293 words/s, in_qsize 5, out_qsize 2
2021-09-29 16:11:22,113 : INFO : EPOCH 7 - PROGRESS: at 54.80% examples, 414413 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:23,142 : INFO : EPOCH 7 - PROGRESS: at 55.17% examples, 414248 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:11:24,154 : INFO : EPOCH 7 - PROGRESS: at 55.60% examples, 414167 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:25,180 : INFO : EPOCH 7 - PROGRESS: at 56.06% examples, 414175 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:11:26,197 : INFO : EPOCH 7 - PROGRESS: at 56.44% examples, 414206 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:11:27,221 : INFO : EPOCH 7 - PROGRESS: at 56.77% examples, 414056 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:28,254 : INFO : EPOCH 7 - PROGRESS: at 57.11% examples, 414029 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:11:29,284 : INFO : EPOCH 7 - PROGRESS: at 57.61% examples, 413882 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:11:30,318 : INFO : EPOCH 7 - PROGRESS: at 58.04% examples, 413861 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:31,339 : INFO : EPOCH 7 - PROGRESS: at 58.44% examples, 413787 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:32,342 : INFO : EPOCH 7 - PROGRESS: at 58.98% examples, 413824 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:11:33,346 : INFO : EPOCH 7 - PROGRESS: at 59.66% examples, 413874 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:11:34,362 : INFO : EPOCH 7 - PROGRESS: at 60.33% examples, 413815 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:11:35,368 : INFO : EPOCH 7 - PROGRESS: at 61.00% examples, 413939 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:36,374 : INFO : EPOCH 7 - PROGRESS: at 61.70% examples, 414055 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:11:37,382 : INFO : EPOCH 7 - PROGRESS: at 62.37% examples, 414073 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:11:38,394 : INFO : EPOCH 7 - PROGRESS: at 63.10% examples, 414140 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:39,397 : INFO : EPOCH 7 - PROGRESS: at 63.82% examples, 414190 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:11:40,402 : INFO : EPOCH 7 - PROGRESS: at 64.52% examples, 414118 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:11:41,404 : INFO : EPOCH 7 - PROGRESS: at 65.21% examples, 414174 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:11:42,447 : INFO : EPOCH 7 - PROGRESS: at 65.80% examples, 414189 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:11:43,458 : INFO : EPOCH 7 - PROGRESS: at 66.38% examples, 414205 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:11:44,461 : INFO : EPOCH 7 - PROGRESS: at 66.76% examples, 414339 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:45,483 : INFO : EPOCH 7 - PROGRESS: at 67.14% examples, 414261 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:46,497 : INFO : EPOCH 7 - PROGRESS: at 67.82% examples, 414256 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:47,508 : INFO : EPOCH 7 - PROGRESS: at 68.55% examples, 414242 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:11:48,511 : INFO : EPOCH 7 - PROGRESS: at 69.26% examples, 414305 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:11:49,512 : INFO : EPOCH 7 - PROGRESS: at 70.03% examples, 414374 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:50,532 : INFO : EPOCH 7 - PROGRESS: at 70.91% examples, 414435 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:11:51,535 : INFO : EPOCH 7 - PROGRESS: at 71.79% examples, 414543 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:52,541 : INFO : EPOCH 7 - PROGRESS: at 72.58% examples, 414514 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:11:53,559 : INFO : EPOCH 7 - PROGRESS: at 73.28% examples, 414554 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:54,580 : INFO : EPOCH 7 - PROGRESS: at 73.91% examples, 414581 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:11:55,580 : INFO : EPOCH 7 - PROGRESS: at 74.58% examples, 414642 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:56,587 : INFO : EPOCH 7 - PROGRESS: at 75.15% examples, 414675 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:57,593 : INFO : EPOCH 7 - PROGRESS: at 75.65% examples, 414610 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:11:58,594 : INFO : EPOCH 7 - PROGRESS: at 76.39% examples, 414586 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:11:59,608 : INFO : EPOCH 7 - PROGRESS: at 77.17% examples, 414525 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:12:00,626 : INFO : EPOCH 7 - PROGRESS: at 77.89% examples, 414427 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:12:01,670 : INFO : EPOCH 7 - PROGRESS: at 78.60% examples, 414187 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:12:02,683 : INFO : EPOCH 7 - PROGRESS: at 79.23% examples, 414155 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:12:03,698 : INFO : EPOCH 7 - PROGRESS: at 79.87% examples, 414066 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:12:04,701 : INFO : EPOCH 7 - PROGRESS: at 80.50% examples, 414026 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:12:05,723 : INFO : EPOCH 7 - PROGRESS: at 81.21% examples, 413940 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:12:06,748 : INFO : EPOCH 7 - PROGRESS: at 81.95% examples, 414027 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:12:07,776 : INFO : EPOCH 7 - PROGRESS: at 82.72% examples, 413909 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:12:08,780 : INFO : EPOCH 7 - PROGRESS: at 83.22% examples, 413862 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:12:09,781 : INFO : EPOCH 7 - PROGRESS: at 83.81% examples, 413728 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:12:10,791 : INFO : EPOCH 7 - PROGRESS: at 84.56% examples, 413627 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:12:11,799 : INFO : EPOCH 7 - PROGRESS: at 85.26% examples, 413499 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:12:12,822 : INFO : EPOCH 7 - PROGRESS: at 85.94% examples, 413347 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:12:13,845 : INFO : EPOCH 7 - PROGRESS: at 86.51% examples, 413443 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:12:14,889 : INFO : EPOCH 7 - PROGRESS: at 87.19% examples, 413319 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:12:15,895 : INFO : EPOCH 7 - PROGRESS: at 87.83% examples, 413268 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:12:16,943 : INFO : EPOCH 7 - PROGRESS: at 88.53% examples, 413179 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:12:17,961 : INFO : EPOCH 7 - PROGRESS: at 89.18% examples, 413334 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:12:18,991 : INFO : EPOCH 7 - PROGRESS: at 90.02% examples, 413366 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:12:20,042 : INFO : EPOCH 7 - PROGRESS: at 90.72% examples, 413351 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:12:21,092 : INFO : EPOCH 7 - PROGRESS: at 91.25% examples, 413419 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:12:22,103 : INFO : EPOCH 7 - PROGRESS: at 91.77% examples, 413630 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:12:23,118 : INFO : EPOCH 7 - PROGRESS: at 92.24% examples, 413594 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:12:24,123 : INFO : EPOCH 7 - PROGRESS: at 92.77% examples, 413774 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:12:25,161 : INFO : EPOCH 7 - PROGRESS: at 93.27% examples, 413781 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:12:26,174 : INFO : EPOCH 7 - PROGRESS: at 93.76% examples, 413877 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:12:27,202 : INFO : EPOCH 7 - PROGRESS: at 94.26% examples, 413952 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:12:28,209 : INFO : EPOCH 7 - PROGRESS: at 94.75% examples, 414012 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:12:29,220 : INFO : EPOCH 7 - PROGRESS: at 95.25% examples, 414026 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:12:30,230 : INFO : EPOCH 7 - PROGRESS: at 95.74% examples, 413990 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:12:31,244 : INFO : EPOCH 7 - PROGRESS: at 96.25% examples, 414035 words/s, in_qsize 3, out_qsize 1
2021-09-29 16:12:32,272 : INFO : EPOCH 7 - PROGRESS: at 96.75% examples, 414000 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:12:33,294 : INFO : EPOCH 7 - PROGRESS: at 97.26% examples, 413865 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:12:34,106 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-29 16:12:34,108 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-29 16:12:34,114 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-29 16:12:34,114 : INFO : EPOCH - 7 : training on 96321721 raw words (70192569 effective words) took 169.5s, 414148 effective words/s
2021-09-29 16:12:35,131 : INFO : EPOCH 8 - PROGRESS: at 0.62% examples, 366301 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:12:36,183 : INFO : EPOCH 8 - PROGRESS: at 1.28% examples, 385418 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:12:37,191 : INFO : EPOCH 8 - PROGRESS: at 2.00% examples, 400470 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:12:38,199 : INFO : EPOCH 8 - PROGRESS: at 2.60% examples, 404580 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:12:39,206 : INFO : EPOCH 8 - PROGRESS: at 3.22% examples, 407543 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:12:40,241 : INFO : EPOCH 8 - PROGRESS: at 3.80% examples, 408776 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:12:41,256 : INFO : EPOCH 8 - PROGRESS: at 4.41% examples, 409727 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:12:42,262 : INFO : EPOCH 8 - PROGRESS: at 4.92% examples, 409717 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:12:43,263 : INFO : EPOCH 8 - PROGRESS: at 5.64% examples, 408536 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:12:44,289 : INFO : EPOCH 8 - PROGRESS: at 6.38% examples, 411387 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:12:45,304 : INFO : EPOCH 8 - PROGRESS: at 6.96% examples, 412273 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:12:46,315 : INFO : EPOCH 8 - PROGRESS: at 7.30% examples, 414315 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:12:47,334 : INFO : EPOCH 8 - PROGRESS: at 7.88% examples, 414463 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:12:48,368 : INFO : EPOCH 8 - PROGRESS: at 8.58% examples, 414460 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:12:49,372 : INFO : EPOCH 8 - PROGRESS: at 9.33% examples, 415439 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:12:50,375 : INFO : EPOCH 8 - PROGRESS: at 10.05% examples, 414830 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:12:51,380 : INFO : EPOCH 8 - PROGRESS: at 10.84% examples, 414956 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:12:52,392 : INFO : EPOCH 8 - PROGRESS: at 11.49% examples, 414458 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:12:53,406 : INFO : EPOCH 8 - PROGRESS: at 12.17% examples, 414311 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:12:54,416 : INFO : EPOCH 8 - PROGRESS: at 12.96% examples, 414598 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:12:55,421 : INFO : EPOCH 8 - PROGRESS: at 13.70% examples, 414200 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:12:56,442 : INFO : EPOCH 8 - PROGRESS: at 14.43% examples, 414048 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:12:57,442 : INFO : EPOCH 8 - PROGRESS: at 14.99% examples, 414231 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:12:58,465 : INFO : EPOCH 8 - PROGRESS: at 15.56% examples, 413820 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:12:59,466 : INFO : EPOCH 8 - PROGRESS: at 16.13% examples, 413928 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:00,487 : INFO : EPOCH 8 - PROGRESS: at 16.79% examples, 413706 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:13:01,496 : INFO : EPOCH 8 - PROGRESS: at 17.45% examples, 414413 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:13:02,511 : INFO : EPOCH 8 - PROGRESS: at 18.11% examples, 413792 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:13:03,519 : INFO : EPOCH 8 - PROGRESS: at 18.84% examples, 413599 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:13:04,534 : INFO : EPOCH 8 - PROGRESS: at 19.56% examples, 413317 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:13:05,557 : INFO : EPOCH 8 - PROGRESS: at 20.32% examples, 413308 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:13:06,575 : INFO : EPOCH 8 - PROGRESS: at 21.00% examples, 413119 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:07,595 : INFO : EPOCH 8 - PROGRESS: at 21.64% examples, 412907 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:13:08,607 : INFO : EPOCH 8 - PROGRESS: at 22.10% examples, 412849 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:13:09,617 : INFO : EPOCH 8 - PROGRESS: at 22.28% examples, 412297 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:10,629 : INFO : EPOCH 8 - PROGRESS: at 22.49% examples, 411677 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:13:11,680 : INFO : EPOCH 8 - PROGRESS: at 22.67% examples, 410490 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:13:12,691 : INFO : EPOCH 8 - PROGRESS: at 22.87% examples, 410383 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:13,719 : INFO : EPOCH 8 - PROGRESS: at 23.06% examples, 410124 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:14,738 : INFO : EPOCH 8 - PROGRESS: at 23.25% examples, 409095 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:13:15,766 : INFO : EPOCH 8 - PROGRESS: at 23.46% examples, 409175 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:16,803 : INFO : EPOCH 8 - PROGRESS: at 23.66% examples, 408498 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:13:17,825 : INFO : EPOCH 8 - PROGRESS: at 23.87% examples, 408340 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:13:18,876 : INFO : EPOCH 8 - PROGRESS: at 24.08% examples, 408216 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:13:19,891 : INFO : EPOCH 8 - PROGRESS: at 24.30% examples, 408275 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:20,912 : INFO : EPOCH 8 - PROGRESS: at 24.65% examples, 407987 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:13:21,913 : INFO : EPOCH 8 - PROGRESS: at 25.14% examples, 408246 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:13:22,923 : INFO : EPOCH 8 - PROGRESS: at 25.85% examples, 408455 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:13:23,926 : INFO : EPOCH 8 - PROGRESS: at 26.48% examples, 408544 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:13:24,931 : INFO : EPOCH 8 - PROGRESS: at 27.20% examples, 408574 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:13:25,934 : INFO : EPOCH 8 - PROGRESS: at 27.88% examples, 408604 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:13:26,947 : INFO : EPOCH 8 - PROGRESS: at 28.24% examples, 408335 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:27,962 : INFO : EPOCH 8 - PROGRESS: at 28.52% examples, 407937 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:13:28,996 : INFO : EPOCH 8 - PROGRESS: at 28.96% examples, 408076 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:13:30,000 : INFO : EPOCH 8 - PROGRESS: at 29.36% examples, 407936 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:31,006 : INFO : EPOCH 8 - PROGRESS: at 29.90% examples, 407622 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:13:32,016 : INFO : EPOCH 8 - PROGRESS: at 30.54% examples, 407827 words/s, in_qsize 2, out_qsize 0
2021-09-29 16:13:33,046 : INFO : EPOCH 8 - PROGRESS: at 31.12% examples, 407491 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:34,060 : INFO : EPOCH 8 - PROGRESS: at 31.80% examples, 407151 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:13:35,068 : INFO : EPOCH 8 - PROGRESS: at 32.54% examples, 407111 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:36,090 : INFO : EPOCH 8 - PROGRESS: at 33.33% examples, 406951 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:37,096 : INFO : EPOCH 8 - PROGRESS: at 34.10% examples, 407111 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:38,111 : INFO : EPOCH 8 - PROGRESS: at 34.89% examples, 407241 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:39,134 : INFO : EPOCH 8 - PROGRESS: at 35.70% examples, 407293 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:13:40,169 : INFO : EPOCH 8 - PROGRESS: at 36.42% examples, 406912 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:13:41,205 : INFO : EPOCH 8 - PROGRESS: at 37.22% examples, 406996 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:42,213 : INFO : EPOCH 8 - PROGRESS: at 38.00% examples, 406926 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:13:43,236 : INFO : EPOCH 8 - PROGRESS: at 38.82% examples, 407063 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:13:44,250 : INFO : EPOCH 8 - PROGRESS: at 39.38% examples, 406283 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:13:45,264 : INFO : EPOCH 8 - PROGRESS: at 39.89% examples, 406031 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:13:46,280 : INFO : EPOCH 8 - PROGRESS: at 40.46% examples, 405817 words/s, in_qsize 5, out_qsize 2
2021-09-29 16:13:47,290 : INFO : EPOCH 8 - PROGRESS: at 41.15% examples, 405911 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:48,296 : INFO : EPOCH 8 - PROGRESS: at 41.72% examples, 405310 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:49,339 : INFO : EPOCH 8 - PROGRESS: at 42.38% examples, 405158 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:50,380 : INFO : EPOCH 8 - PROGRESS: at 43.11% examples, 404740 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:51,386 : INFO : EPOCH 8 - PROGRESS: at 43.77% examples, 404888 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:52,409 : INFO : EPOCH 8 - PROGRESS: at 44.44% examples, 404863 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:53,436 : INFO : EPOCH 8 - PROGRESS: at 45.01% examples, 404728 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:13:54,454 : INFO : EPOCH 8 - PROGRESS: at 45.69% examples, 404546 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:55,459 : INFO : EPOCH 8 - PROGRESS: at 46.45% examples, 404322 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:56,463 : INFO : EPOCH 8 - PROGRESS: at 47.04% examples, 404221 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:57,477 : INFO : EPOCH 8 - PROGRESS: at 47.63% examples, 404129 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:13:58,485 : INFO : EPOCH 8 - PROGRESS: at 48.26% examples, 404662 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:13:59,497 : INFO : EPOCH 8 - PROGRESS: at 48.95% examples, 404795 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:00,505 : INFO : EPOCH 8 - PROGRESS: at 49.52% examples, 404808 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:14:01,508 : INFO : EPOCH 8 - PROGRESS: at 50.28% examples, 405179 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:14:02,513 : INFO : EPOCH 8 - PROGRESS: at 51.07% examples, 405434 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:03,513 : INFO : EPOCH 8 - PROGRESS: at 51.18% examples, 405648 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:04,523 : INFO : EPOCH 8 - PROGRESS: at 51.46% examples, 405617 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:05,531 : INFO : EPOCH 8 - PROGRESS: at 51.75% examples, 405568 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:06,541 : INFO : EPOCH 8 - PROGRESS: at 52.26% examples, 405571 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:14:07,560 : INFO : EPOCH 8 - PROGRESS: at 52.69% examples, 405415 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:14:08,576 : INFO : EPOCH 8 - PROGRESS: at 53.01% examples, 405636 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:14:09,579 : INFO : EPOCH 8 - PROGRESS: at 53.34% examples, 405765 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:14:10,580 : INFO : EPOCH 8 - PROGRESS: at 53.65% examples, 405594 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:14:11,601 : INFO : EPOCH 8 - PROGRESS: at 54.07% examples, 405562 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:14:12,614 : INFO : EPOCH 8 - PROGRESS: at 54.44% examples, 405639 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:14:13,633 : INFO : EPOCH 8 - PROGRESS: at 54.78% examples, 405686 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:14:14,655 : INFO : EPOCH 8 - PROGRESS: at 55.18% examples, 405928 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:15,667 : INFO : EPOCH 8 - PROGRESS: at 55.59% examples, 405794 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:16,712 : INFO : EPOCH 8 - PROGRESS: at 56.03% examples, 405602 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:14:17,720 : INFO : EPOCH 8 - PROGRESS: at 56.40% examples, 405609 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:14:18,742 : INFO : EPOCH 8 - PROGRESS: at 56.75% examples, 405765 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:14:19,751 : INFO : EPOCH 8 - PROGRESS: at 57.08% examples, 405773 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:20,767 : INFO : EPOCH 8 - PROGRESS: at 57.54% examples, 405695 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:21,780 : INFO : EPOCH 8 - PROGRESS: at 57.99% examples, 405762 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:14:22,782 : INFO : EPOCH 8 - PROGRESS: at 58.40% examples, 405898 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:23,825 : INFO : EPOCH 8 - PROGRESS: at 58.93% examples, 405920 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:14:24,848 : INFO : EPOCH 8 - PROGRESS: at 59.64% examples, 406168 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:14:25,856 : INFO : EPOCH 8 - PROGRESS: at 60.32% examples, 406273 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:14:26,881 : INFO : EPOCH 8 - PROGRESS: at 61.03% examples, 406658 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:14:27,900 : INFO : EPOCH 8 - PROGRESS: at 61.71% examples, 406848 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:14:28,908 : INFO : EPOCH 8 - PROGRESS: at 62.43% examples, 406924 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:29,920 : INFO : EPOCH 8 - PROGRESS: at 63.15% examples, 407059 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:30,970 : INFO : EPOCH 8 - PROGRESS: at 63.89% examples, 407119 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:14:32,000 : INFO : EPOCH 8 - PROGRESS: at 64.64% examples, 407344 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:33,001 : INFO : EPOCH 8 - PROGRESS: at 65.27% examples, 407201 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:14:34,002 : INFO : EPOCH 8 - PROGRESS: at 65.86% examples, 407364 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:35,011 : INFO : EPOCH 8 - PROGRESS: at 66.42% examples, 407380 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:36,038 : INFO : EPOCH 8 - PROGRESS: at 66.80% examples, 407492 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:37,047 : INFO : EPOCH 8 - PROGRESS: at 67.18% examples, 407510 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:14:38,048 : INFO : EPOCH 8 - PROGRESS: at 67.87% examples, 407547 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:14:39,051 : INFO : EPOCH 8 - PROGRESS: at 68.61% examples, 407671 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:14:40,065 : INFO : EPOCH 8 - PROGRESS: at 69.33% examples, 407818 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:41,092 : INFO : EPOCH 8 - PROGRESS: at 70.13% examples, 407906 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:42,111 : INFO : EPOCH 8 - PROGRESS: at 71.00% examples, 407904 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:14:43,138 : INFO : EPOCH 8 - PROGRESS: at 71.91% examples, 408159 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:44,143 : INFO : EPOCH 8 - PROGRESS: at 72.70% examples, 408237 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:14:45,152 : INFO : EPOCH 8 - PROGRESS: at 73.40% examples, 408366 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:14:46,163 : INFO : EPOCH 8 - PROGRESS: at 74.01% examples, 408470 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:47,171 : INFO : EPOCH 8 - PROGRESS: at 74.68% examples, 408553 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:14:48,188 : INFO : EPOCH 8 - PROGRESS: at 75.23% examples, 408641 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:14:49,211 : INFO : EPOCH 8 - PROGRESS: at 75.83% examples, 408738 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:14:50,222 : INFO : EPOCH 8 - PROGRESS: at 76.61% examples, 408833 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:51,225 : INFO : EPOCH 8 - PROGRESS: at 77.38% examples, 408899 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:52,236 : INFO : EPOCH 8 - PROGRESS: at 78.11% examples, 408974 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:14:53,255 : INFO : EPOCH 8 - PROGRESS: at 78.84% examples, 409050 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:54,274 : INFO : EPOCH 8 - PROGRESS: at 79.51% examples, 409153 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:55,285 : INFO : EPOCH 8 - PROGRESS: at 80.18% examples, 409250 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:14:56,287 : INFO : EPOCH 8 - PROGRESS: at 80.79% examples, 409124 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:57,299 : INFO : EPOCH 8 - PROGRESS: at 81.52% examples, 409197 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:14:58,316 : INFO : EPOCH 8 - PROGRESS: at 82.33% examples, 409281 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:14:59,328 : INFO : EPOCH 8 - PROGRESS: at 83.01% examples, 409391 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:00,346 : INFO : EPOCH 8 - PROGRESS: at 83.45% examples, 409343 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:01,354 : INFO : EPOCH 8 - PROGRESS: at 84.16% examples, 409238 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:15:02,357 : INFO : EPOCH 8 - PROGRESS: at 84.87% examples, 409105 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:03,372 : INFO : EPOCH 8 - PROGRESS: at 85.60% examples, 408811 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:15:04,379 : INFO : EPOCH 8 - PROGRESS: at 86.13% examples, 408589 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:05,383 : INFO : EPOCH 8 - PROGRESS: at 86.63% examples, 408533 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:15:06,409 : INFO : EPOCH 8 - PROGRESS: at 87.39% examples, 408535 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:07,444 : INFO : EPOCH 8 - PROGRESS: at 88.00% examples, 408393 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:15:08,455 : INFO : EPOCH 8 - PROGRESS: at 88.69% examples, 408498 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:09,501 : INFO : EPOCH 8 - PROGRESS: at 89.41% examples, 408435 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:15:10,532 : INFO : EPOCH 8 - PROGRESS: at 90.24% examples, 408562 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:15:11,578 : INFO : EPOCH 8 - PROGRESS: at 90.85% examples, 408633 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:15:12,612 : INFO : EPOCH 8 - PROGRESS: at 91.38% examples, 408725 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:15:13,618 : INFO : EPOCH 8 - PROGRESS: at 91.88% examples, 408932 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:14,637 : INFO : EPOCH 8 - PROGRESS: at 92.33% examples, 408827 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:15:15,659 : INFO : EPOCH 8 - PROGRESS: at 92.85% examples, 408988 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:16,667 : INFO : EPOCH 8 - PROGRESS: at 93.34% examples, 408965 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:17,669 : INFO : EPOCH 8 - PROGRESS: at 93.80% examples, 408984 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:18,685 : INFO : EPOCH 8 - PROGRESS: at 94.29% examples, 409072 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:15:19,690 : INFO : EPOCH 8 - PROGRESS: at 94.78% examples, 409122 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:15:20,738 : INFO : EPOCH 8 - PROGRESS: at 95.27% examples, 409076 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:15:21,743 : INFO : EPOCH 8 - PROGRESS: at 95.80% examples, 409258 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:22,747 : INFO : EPOCH 8 - PROGRESS: at 96.30% examples, 409306 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:15:23,750 : INFO : EPOCH 8 - PROGRESS: at 96.80% examples, 409407 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:24,777 : INFO : EPOCH 8 - PROGRESS: at 97.39% examples, 409374 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:15:25,396 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-29 16:15:25,402 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-29 16:15:25,403 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-29 16:15:25,403 : INFO : EPOCH - 8 : training on 96321721 raw words (70186452 effective words) took 171.3s, 409755 effective words/s
2021-09-29 16:15:26,426 : INFO : EPOCH 9 - PROGRESS: at 0.63% examples, 372031 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:27,438 : INFO : EPOCH 9 - PROGRESS: at 1.30% examples, 399400 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:28,457 : INFO : EPOCH 9 - PROGRESS: at 2.01% examples, 406156 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:29,471 : INFO : EPOCH 9 - PROGRESS: at 2.62% examples, 408147 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:15:30,498 : INFO : EPOCH 9 - PROGRESS: at 3.23% examples, 408833 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:31,541 : INFO : EPOCH 9 - PROGRESS: at 3.82% examples, 410490 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:15:32,544 : INFO : EPOCH 9 - PROGRESS: at 4.44% examples, 412879 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:15:33,560 : INFO : EPOCH 9 - PROGRESS: at 4.96% examples, 412816 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:15:34,565 : INFO : EPOCH 9 - PROGRESS: at 5.75% examples, 415317 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:15:35,569 : INFO : EPOCH 9 - PROGRESS: at 6.44% examples, 415330 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:36,590 : INFO : EPOCH 9 - PROGRESS: at 7.01% examples, 417113 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:37,599 : INFO : EPOCH 9 - PROGRESS: at 7.34% examples, 418801 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:38,618 : INFO : EPOCH 9 - PROGRESS: at 7.97% examples, 418504 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:15:39,636 : INFO : EPOCH 9 - PROGRESS: at 8.67% examples, 418675 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:15:40,649 : INFO : EPOCH 9 - PROGRESS: at 9.39% examples, 418692 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:41,659 : INFO : EPOCH 9 - PROGRESS: at 10.16% examples, 418560 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:15:42,664 : INFO : EPOCH 9 - PROGRESS: at 10.95% examples, 418897 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:43,670 : INFO : EPOCH 9 - PROGRESS: at 11.59% examples, 418692 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:44,690 : INFO : EPOCH 9 - PROGRESS: at 12.31% examples, 418320 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:45,699 : INFO : EPOCH 9 - PROGRESS: at 13.07% examples, 418737 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:15:46,701 : INFO : EPOCH 9 - PROGRESS: at 13.85% examples, 418552 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:47,730 : INFO : EPOCH 9 - PROGRESS: at 14.56% examples, 418309 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:15:48,749 : INFO : EPOCH 9 - PROGRESS: at 15.10% examples, 417673 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:15:49,759 : INFO : EPOCH 9 - PROGRESS: at 15.69% examples, 418227 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:50,774 : INFO : EPOCH 9 - PROGRESS: at 16.30% examples, 417853 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:15:51,788 : INFO : EPOCH 9 - PROGRESS: at 16.97% examples, 418076 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:52,828 : INFO : EPOCH 9 - PROGRESS: at 17.60% examples, 417691 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:15:53,848 : INFO : EPOCH 9 - PROGRESS: at 18.35% examples, 417687 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:15:54,881 : INFO : EPOCH 9 - PROGRESS: at 19.11% examples, 417740 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:15:55,882 : INFO : EPOCH 9 - PROGRESS: at 19.86% examples, 417898 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:15:56,915 : INFO : EPOCH 9 - PROGRESS: at 20.61% examples, 417753 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:15:57,925 : INFO : EPOCH 9 - PROGRESS: at 21.29% examples, 418196 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:15:58,974 : INFO : EPOCH 9 - PROGRESS: at 21.98% examples, 417444 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:15:59,989 : INFO : EPOCH 9 - PROGRESS: at 22.19% examples, 417437 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:16:01,001 : INFO : EPOCH 9 - PROGRESS: at 22.38% examples, 416770 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:16:02,024 : INFO : EPOCH 9 - PROGRESS: at 22.59% examples, 416471 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:16:03,045 : INFO : EPOCH 9 - PROGRESS: at 22.78% examples, 415707 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:16:04,049 : INFO : EPOCH 9 - PROGRESS: at 22.98% examples, 415709 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:16:05,101 : INFO : EPOCH 9 - PROGRESS: at 23.18% examples, 415014 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:16:06,102 : INFO : EPOCH 9 - PROGRESS: at 23.39% examples, 415051 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:16:07,138 : INFO : EPOCH 9 - PROGRESS: at 23.59% examples, 414720 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:16:08,162 : INFO : EPOCH 9 - PROGRESS: at 23.80% examples, 414250 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:16:09,192 : INFO : EPOCH 9 - PROGRESS: at 24.00% examples, 413687 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:16:10,196 : INFO : EPOCH 9 - PROGRESS: at 24.22% examples, 413578 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:16:11,207 : INFO : EPOCH 9 - PROGRESS: at 24.42% examples, 413105 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:16:12,225 : INFO : EPOCH 9 - PROGRESS: at 24.96% examples, 413370 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:16:13,225 : INFO : EPOCH 9 - PROGRESS: at 25.56% examples, 413403 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:16:14,252 : INFO : EPOCH 9 - PROGRESS: at 26.25% examples, 413490 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:16:15,267 : INFO : EPOCH 9 - PROGRESS: at 26.94% examples, 413513 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:16:16,286 : INFO : EPOCH 9 - PROGRESS: at 27.68% examples, 413587 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:16:17,301 : INFO : EPOCH 9 - PROGRESS: at 28.17% examples, 413532 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:16:18,323 : INFO : EPOCH 9 - PROGRESS: at 28.43% examples, 413396 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:16:19,351 : INFO : EPOCH 9 - PROGRESS: at 28.88% examples, 413140 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:16:20,365 : INFO : EPOCH 9 - PROGRESS: at 29.26% examples, 413183 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:16:21,415 : INFO : EPOCH 9 - PROGRESS: at 29.82% examples, 413008 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:16:22,422 : INFO : EPOCH 9 - PROGRESS: at 30.44% examples, 413147 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:16:23,444 : INFO : EPOCH 9 - PROGRESS: at 31.09% examples, 413398 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:16:24,471 : INFO : EPOCH 9 - PROGRESS: at 31.83% examples, 413477 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:16:25,487 : INFO : EPOCH 9 - PROGRESS: at 32.61% examples, 413638 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:16:26,506 : INFO : EPOCH 9 - PROGRESS: at 33.43% examples, 413743 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:16:27,517 : INFO : EPOCH 9 - PROGRESS: at 34.22% examples, 413886 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:16:28,535 : INFO : EPOCH 9 - PROGRESS: at 35.03% examples, 413991 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:16:29,544 : INFO : EPOCH 9 - PROGRESS: at 35.83% examples, 414025 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:16:30,545 : INFO : EPOCH 9 - PROGRESS: at 36.61% examples, 414200 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:16:31,561 : INFO : EPOCH 9 - PROGRESS: at 37.40% examples, 414191 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:16:32,600 : INFO : EPOCH 9 - PROGRESS: at 38.21% examples, 414022 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:16:33,619 : INFO : EPOCH 9 - PROGRESS: at 39.07% examples, 414403 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:16:34,647 : INFO : EPOCH 9 - PROGRESS: at 39.64% examples, 414236 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:16:35,678 : INFO : EPOCH 9 - PROGRESS: at 40.18% examples, 413929 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:16:36,698 : INFO : EPOCH 9 - PROGRESS: at 40.88% examples, 413977 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:16:37,727 : INFO : EPOCH 9 - PROGRESS: at 41.47% examples, 414062 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:16:38,777 : INFO : EPOCH 9 - PROGRESS: at 42.22% examples, 414024 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:16:39,791 : INFO : EPOCH 9 - PROGRESS: at 43.02% examples, 414299 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:16:40,795 : INFO : EPOCH 9 - PROGRESS: at 43.70% examples, 414427 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:16:41,823 : INFO : EPOCH 9 - PROGRESS: at 44.39% examples, 414431 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:16:42,877 : INFO : EPOCH 9 - PROGRESS: at 45.01% examples, 414403 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:16:43,888 : INFO : EPOCH 9 - PROGRESS: at 45.76% examples, 414674 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:16:44,891 : INFO : EPOCH 9 - PROGRESS: at 46.60% examples, 414712 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:16:45,901 : INFO : EPOCH 9 - PROGRESS: at 47.15% examples, 414511 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:16:46,929 : INFO : EPOCH 9 - PROGRESS: at 47.81% examples, 414810 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:16:47,932 : INFO : EPOCH 9 - PROGRESS: at 48.43% examples, 415059 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:16:48,959 : INFO : EPOCH 9 - PROGRESS: at 49.08% examples, 414858 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:16:49,994 : INFO : EPOCH 9 - PROGRESS: at 49.69% examples, 414799 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:16:51,001 : INFO : EPOCH 9 - PROGRESS: at 50.51% examples, 415168 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:16:52,011 : INFO : EPOCH 9 - PROGRESS: at 51.12% examples, 415226 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:16:53,045 : INFO : EPOCH 9 - PROGRESS: at 51.19% examples, 415159 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:16:54,050 : INFO : EPOCH 9 - PROGRESS: at 51.66% examples, 415153 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:16:55,052 : INFO : EPOCH 9 - PROGRESS: at 51.83% examples, 415278 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:16:56,102 : INFO : EPOCH 9 - PROGRESS: at 52.44% examples, 415168 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:16:57,148 : INFO : EPOCH 9 - PROGRESS: at 52.83% examples, 415116 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:16:58,175 : INFO : EPOCH 9 - PROGRESS: at 53.15% examples, 415166 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:16:59,229 : INFO : EPOCH 9 - PROGRESS: at 53.52% examples, 415264 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:17:00,229 : INFO : EPOCH 9 - PROGRESS: at 53.91% examples, 415286 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:17:01,241 : INFO : EPOCH 9 - PROGRESS: at 54.30% examples, 415282 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:17:02,260 : INFO : EPOCH 9 - PROGRESS: at 54.65% examples, 415222 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:17:03,272 : INFO : EPOCH 9 - PROGRESS: at 55.01% examples, 415185 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:17:04,282 : INFO : EPOCH 9 - PROGRESS: at 55.42% examples, 415173 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:05,301 : INFO : EPOCH 9 - PROGRESS: at 55.88% examples, 415066 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:17:06,331 : INFO : EPOCH 9 - PROGRESS: at 56.28% examples, 414960 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:17:07,342 : INFO : EPOCH 9 - PROGRESS: at 56.63% examples, 414926 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:08,357 : INFO : EPOCH 9 - PROGRESS: at 56.92% examples, 414397 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:17:09,373 : INFO : EPOCH 9 - PROGRESS: at 57.23% examples, 414154 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:17:10,376 : INFO : EPOCH 9 - PROGRESS: at 57.79% examples, 414049 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:11,416 : INFO : EPOCH 9 - PROGRESS: at 58.20% examples, 414082 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:17:12,418 : INFO : EPOCH 9 - PROGRESS: at 58.59% examples, 414206 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:13,452 : INFO : EPOCH 9 - PROGRESS: at 59.28% examples, 414224 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:17:14,454 : INFO : EPOCH 9 - PROGRESS: at 59.99% examples, 414344 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:15,463 : INFO : EPOCH 9 - PROGRESS: at 60.65% examples, 414382 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:16,476 : INFO : EPOCH 9 - PROGRESS: at 61.31% examples, 414473 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:17,490 : INFO : EPOCH 9 - PROGRESS: at 61.97% examples, 414457 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:18,535 : INFO : EPOCH 9 - PROGRESS: at 62.69% examples, 414148 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:17:19,542 : INFO : EPOCH 9 - PROGRESS: at 63.41% examples, 414155 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:20,556 : INFO : EPOCH 9 - PROGRESS: at 64.02% examples, 413787 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:17:21,579 : INFO : EPOCH 9 - PROGRESS: at 64.71% examples, 413721 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:17:22,580 : INFO : EPOCH 9 - PROGRESS: at 65.35% examples, 413647 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:17:23,598 : INFO : EPOCH 9 - PROGRESS: at 65.94% examples, 413637 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:17:24,601 : INFO : EPOCH 9 - PROGRESS: at 66.45% examples, 413493 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:17:25,602 : INFO : EPOCH 9 - PROGRESS: at 66.83% examples, 413653 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:26,606 : INFO : EPOCH 9 - PROGRESS: at 67.22% examples, 413633 words/s, in_qsize 5, out_qsize 2
2021-09-29 16:17:27,608 : INFO : EPOCH 9 - PROGRESS: at 67.94% examples, 413680 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:17:28,648 : INFO : EPOCH 9 - PROGRESS: at 68.67% examples, 413634 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:17:29,658 : INFO : EPOCH 9 - PROGRESS: at 69.42% examples, 413752 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:17:30,680 : INFO : EPOCH 9 - PROGRESS: at 70.21% examples, 413813 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:17:31,693 : INFO : EPOCH 9 - PROGRESS: at 71.08% examples, 413836 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:17:32,710 : INFO : EPOCH 9 - PROGRESS: at 71.96% examples, 413909 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:33,724 : INFO : EPOCH 9 - PROGRESS: at 72.76% examples, 413967 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:34,741 : INFO : EPOCH 9 - PROGRESS: at 73.44% examples, 413971 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:17:35,784 : INFO : EPOCH 9 - PROGRESS: at 74.09% examples, 414042 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:36,792 : INFO : EPOCH 9 - PROGRESS: at 74.72% examples, 413924 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:37,807 : INFO : EPOCH 9 - PROGRESS: at 75.25% examples, 413973 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:38,825 : INFO : EPOCH 9 - PROGRESS: at 75.83% examples, 413888 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:17:39,826 : INFO : EPOCH 9 - PROGRESS: at 76.56% examples, 413816 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:17:40,863 : INFO : EPOCH 9 - PROGRESS: at 77.35% examples, 413742 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:41,900 : INFO : EPOCH 9 - PROGRESS: at 78.06% examples, 413647 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:42,912 : INFO : EPOCH 9 - PROGRESS: at 78.76% examples, 413554 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:43,922 : INFO : EPOCH 9 - PROGRESS: at 79.40% examples, 413546 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:44,930 : INFO : EPOCH 9 - PROGRESS: at 80.01% examples, 413373 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:45,931 : INFO : EPOCH 9 - PROGRESS: at 80.57% examples, 412994 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:17:46,956 : INFO : EPOCH 9 - PROGRESS: at 81.28% examples, 412904 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:17:47,988 : INFO : EPOCH 9 - PROGRESS: at 82.00% examples, 412870 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:17:48,996 : INFO : EPOCH 9 - PROGRESS: at 82.79% examples, 412922 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:50,000 : INFO : EPOCH 9 - PROGRESS: at 83.28% examples, 412986 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:51,023 : INFO : EPOCH 9 - PROGRESS: at 83.95% examples, 412951 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:17:52,038 : INFO : EPOCH 9 - PROGRESS: at 84.70% examples, 412875 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:53,058 : INFO : EPOCH 9 - PROGRESS: at 85.51% examples, 412878 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:54,067 : INFO : EPOCH 9 - PROGRESS: at 86.06% examples, 412717 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:17:55,072 : INFO : EPOCH 9 - PROGRESS: at 86.58% examples, 412676 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:56,096 : INFO : EPOCH 9 - PROGRESS: at 87.31% examples, 412608 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:17:57,111 : INFO : EPOCH 9 - PROGRESS: at 87.98% examples, 412732 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:17:58,142 : INFO : EPOCH 9 - PROGRESS: at 88.64% examples, 412560 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:17:59,148 : INFO : EPOCH 9 - PROGRESS: at 89.31% examples, 412540 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:00,157 : INFO : EPOCH 9 - PROGRESS: at 90.01% examples, 412265 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:18:01,159 : INFO : EPOCH 9 - PROGRESS: at 90.70% examples, 412340 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:02,171 : INFO : EPOCH 9 - PROGRESS: at 91.20% examples, 412329 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:18:03,189 : INFO : EPOCH 9 - PROGRESS: at 91.68% examples, 412301 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:18:04,208 : INFO : EPOCH 9 - PROGRESS: at 92.17% examples, 412355 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:05,232 : INFO : EPOCH 9 - PROGRESS: at 92.63% examples, 412177 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:18:06,237 : INFO : EPOCH 9 - PROGRESS: at 93.13% examples, 412275 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:07,238 : INFO : EPOCH 9 - PROGRESS: at 93.60% examples, 412290 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:08,243 : INFO : EPOCH 9 - PROGRESS: at 94.08% examples, 412328 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:09,262 : INFO : EPOCH 9 - PROGRESS: at 94.58% examples, 412373 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:18:10,281 : INFO : EPOCH 9 - PROGRESS: at 95.09% examples, 412465 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:18:11,329 : INFO : EPOCH 9 - PROGRESS: at 95.59% examples, 412527 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:12,342 : INFO : EPOCH 9 - PROGRESS: at 96.13% examples, 412581 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:18:13,345 : INFO : EPOCH 9 - PROGRESS: at 96.63% examples, 412611 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:18:14,391 : INFO : EPOCH 9 - PROGRESS: at 97.13% examples, 412641 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:18:15,334 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-29 16:18:15,334 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-29 16:18:15,341 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-29 16:18:15,341 : INFO : EPOCH - 9 : training on 96321721 raw words (70191161 effective words) took 169.9s, 413041 effective words/s
2021-09-29 16:18:16,356 : INFO : EPOCH 10 - PROGRESS: at 0.63% examples, 374600 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:17,378 : INFO : EPOCH 10 - PROGRESS: at 1.30% examples, 398856 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:18:18,392 : INFO : EPOCH 10 - PROGRESS: at 2.00% examples, 406605 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:18:19,392 : INFO : EPOCH 10 - PROGRESS: at 2.63% examples, 411703 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:18:20,407 : INFO : EPOCH 10 - PROGRESS: at 3.22% examples, 409780 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:18:21,420 : INFO : EPOCH 10 - PROGRESS: at 3.82% examples, 414545 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:18:22,449 : INFO : EPOCH 10 - PROGRESS: at 4.45% examples, 415900 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:18:23,463 : INFO : EPOCH 10 - PROGRESS: at 4.98% examples, 416437 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:24,469 : INFO : EPOCH 10 - PROGRESS: at 5.77% examples, 418608 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:25,502 : INFO : EPOCH 10 - PROGRESS: at 6.48% examples, 417767 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:18:26,528 : INFO : EPOCH 10 - PROGRESS: at 7.03% examples, 419768 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:18:27,534 : INFO : EPOCH 10 - PROGRESS: at 7.37% examples, 423232 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:28,549 : INFO : EPOCH 10 - PROGRESS: at 8.06% examples, 423184 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:29,598 : INFO : EPOCH 10 - PROGRESS: at 8.78% examples, 422128 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:18:30,604 : INFO : EPOCH 10 - PROGRESS: at 9.50% examples, 423040 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:18:31,640 : INFO : EPOCH 10 - PROGRESS: at 10.32% examples, 422781 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:32,666 : INFO : EPOCH 10 - PROGRESS: at 11.09% examples, 421994 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:18:33,671 : INFO : EPOCH 10 - PROGRESS: at 11.71% examples, 420820 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:34,684 : INFO : EPOCH 10 - PROGRESS: at 12.45% examples, 420931 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:35,703 : INFO : EPOCH 10 - PROGRESS: at 13.19% examples, 420285 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:18:36,747 : INFO : EPOCH 10 - PROGRESS: at 14.00% examples, 419846 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:18:37,759 : INFO : EPOCH 10 - PROGRESS: at 14.66% examples, 419550 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:38,760 : INFO : EPOCH 10 - PROGRESS: at 15.20% examples, 419410 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:39,766 : INFO : EPOCH 10 - PROGRESS: at 15.76% examples, 419185 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:40,775 : INFO : EPOCH 10 - PROGRESS: at 16.38% examples, 419158 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:18:41,788 : INFO : EPOCH 10 - PROGRESS: at 17.05% examples, 419462 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:42,793 : INFO : EPOCH 10 - PROGRESS: at 17.71% examples, 419466 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:18:43,802 : INFO : EPOCH 10 - PROGRESS: at 18.45% examples, 419568 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:44,802 : INFO : EPOCH 10 - PROGRESS: at 19.19% examples, 419539 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:18:45,810 : INFO : EPOCH 10 - PROGRESS: at 19.93% examples, 419327 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:46,817 : INFO : EPOCH 10 - PROGRESS: at 20.65% examples, 419214 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:47,824 : INFO : EPOCH 10 - PROGRESS: at 21.33% examples, 419446 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:18:48,838 : INFO : EPOCH 10 - PROGRESS: at 22.00% examples, 419513 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:49,857 : INFO : EPOCH 10 - PROGRESS: at 22.20% examples, 419134 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:50,867 : INFO : EPOCH 10 - PROGRESS: at 22.40% examples, 418640 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:18:51,882 : INFO : EPOCH 10 - PROGRESS: at 22.60% examples, 418205 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:18:52,886 : INFO : EPOCH 10 - PROGRESS: at 22.80% examples, 417956 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:53,890 : INFO : EPOCH 10 - PROGRESS: at 22.99% examples, 417712 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:54,903 : INFO : EPOCH 10 - PROGRESS: at 23.18% examples, 416847 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:55,915 : INFO : EPOCH 10 - PROGRESS: at 23.38% examples, 416227 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:56,922 : INFO : EPOCH 10 - PROGRESS: at 23.58% examples, 415664 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:18:57,959 : INFO : EPOCH 10 - PROGRESS: at 23.78% examples, 415033 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:18:59,007 : INFO : EPOCH 10 - PROGRESS: at 24.00% examples, 414924 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:19:00,008 : INFO : EPOCH 10 - PROGRESS: at 24.22% examples, 414823 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:19:01,024 : INFO : EPOCH 10 - PROGRESS: at 24.42% examples, 414573 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:19:02,050 : INFO : EPOCH 10 - PROGRESS: at 24.97% examples, 414604 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:19:03,061 : INFO : EPOCH 10 - PROGRESS: at 25.59% examples, 414665 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:19:04,078 : INFO : EPOCH 10 - PROGRESS: at 26.26% examples, 414809 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:19:05,078 : INFO : EPOCH 10 - PROGRESS: at 26.96% examples, 414914 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:19:06,114 : INFO : EPOCH 10 - PROGRESS: at 27.73% examples, 415125 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:19:07,138 : INFO : EPOCH 10 - PROGRESS: at 28.20% examples, 415356 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:19:08,162 : INFO : EPOCH 10 - PROGRESS: at 28.50% examples, 415412 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:19:09,203 : INFO : EPOCH 10 - PROGRESS: at 28.94% examples, 415505 words/s, in_qsize 3, out_qsize 2
2021-09-29 16:19:10,235 : INFO : EPOCH 10 - PROGRESS: at 29.36% examples, 415392 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:19:11,245 : INFO : EPOCH 10 - PROGRESS: at 29.97% examples, 415828 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:19:12,245 : INFO : EPOCH 10 - PROGRESS: at 30.62% examples, 415958 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:19:13,273 : INFO : EPOCH 10 - PROGRESS: at 31.23% examples, 416003 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:19:14,284 : INFO : EPOCH 10 - PROGRESS: at 32.00% examples, 416151 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:19:15,293 : INFO : EPOCH 10 - PROGRESS: at 32.81% examples, 416293 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:19:16,315 : INFO : EPOCH 10 - PROGRESS: at 33.62% examples, 416455 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:19:17,331 : INFO : EPOCH 10 - PROGRESS: at 34.43% examples, 416647 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:19:18,342 : INFO : EPOCH 10 - PROGRESS: at 35.24% examples, 416743 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:19:19,355 : INFO : EPOCH 10 - PROGRESS: at 36.05% examples, 416819 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:19:20,384 : INFO : EPOCH 10 - PROGRESS: at 36.85% examples, 416891 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:19:21,394 : INFO : EPOCH 10 - PROGRESS: at 37.66% examples, 416984 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:19:22,408 : INFO : EPOCH 10 - PROGRESS: at 38.50% examples, 417151 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:19:23,409 : INFO : EPOCH 10 - PROGRESS: at 39.25% examples, 417152 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:19:24,435 : INFO : EPOCH 10 - PROGRESS: at 39.81% examples, 417174 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:19:25,452 : INFO : EPOCH 10 - PROGRESS: at 40.39% examples, 417182 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:19:26,464 : INFO : EPOCH 10 - PROGRESS: at 41.11% examples, 417301 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:19:27,476 : INFO : EPOCH 10 - PROGRESS: at 41.77% examples, 417297 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:19:28,515 : INFO : EPOCH 10 - PROGRESS: at 42.42% examples, 417166 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:19:29,534 : INFO : EPOCH 10 - PROGRESS: at 43.25% examples, 417411 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:19:30,548 : INFO : EPOCH 10 - PROGRESS: at 43.92% examples, 417351 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:19:31,551 : INFO : EPOCH 10 - PROGRESS: at 44.63% examples, 417648 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:19:32,568 : INFO : EPOCH 10 - PROGRESS: at 45.26% examples, 417779 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:19:33,588 : INFO : EPOCH 10 - PROGRESS: at 46.06% examples, 417800 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:19:34,601 : INFO : EPOCH 10 - PROGRESS: at 46.82% examples, 417681 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:19:35,623 : INFO : EPOCH 10 - PROGRESS: at 47.40% examples, 417674 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:19:36,642 : INFO : EPOCH 10 - PROGRESS: at 48.02% examples, 417806 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:19:37,654 : INFO : EPOCH 10 - PROGRESS: at 48.69% examples, 418073 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:19:38,662 : INFO : EPOCH 10 - PROGRESS: at 49.25% examples, 418025 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:19:39,665 : INFO : EPOCH 10 - PROGRESS: at 50.00% examples, 418062 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:19:40,686 : INFO : EPOCH 10 - PROGRESS: at 50.84% examples, 418345 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:19:41,699 : INFO : EPOCH 10 - PROGRESS: at 51.17% examples, 418456 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:19:42,744 : INFO : EPOCH 10 - PROGRESS: at 51.21% examples, 418290 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:19:43,758 : INFO : EPOCH 10 - PROGRESS: at 51.69% examples, 418409 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:19:44,775 : INFO : EPOCH 10 - PROGRESS: at 52.17% examples, 418474 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:19:45,785 : INFO : EPOCH 10 - PROGRESS: at 52.66% examples, 418520 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:19:46,818 : INFO : EPOCH 10 - PROGRESS: at 52.97% examples, 418364 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:19:47,831 : INFO : EPOCH 10 - PROGRESS: at 53.31% examples, 418560 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:19:48,843 : INFO : EPOCH 10 - PROGRESS: at 53.66% examples, 418580 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:19:49,848 : INFO : EPOCH 10 - PROGRESS: at 54.08% examples, 418559 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:19:50,876 : INFO : EPOCH 10 - PROGRESS: at 54.46% examples, 418577 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:19:51,879 : INFO : EPOCH 10 - PROGRESS: at 54.80% examples, 418553 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:19:52,899 : INFO : EPOCH 10 - PROGRESS: at 55.20% examples, 418604 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:19:53,905 : INFO : EPOCH 10 - PROGRESS: at 55.64% examples, 418581 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:19:54,913 : INFO : EPOCH 10 - PROGRESS: at 56.09% examples, 418536 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:19:55,920 : INFO : EPOCH 10 - PROGRESS: at 56.46% examples, 418566 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:19:56,973 : INFO : EPOCH 10 - PROGRESS: at 56.80% examples, 418397 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:19:57,993 : INFO : EPOCH 10 - PROGRESS: at 57.15% examples, 418519 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:19:59,016 : INFO : EPOCH 10 - PROGRESS: at 57.72% examples, 418494 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:00,029 : INFO : EPOCH 10 - PROGRESS: at 58.10% examples, 418445 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:20:01,037 : INFO : EPOCH 10 - PROGRESS: at 58.50% examples, 418446 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:20:02,063 : INFO : EPOCH 10 - PROGRESS: at 59.12% examples, 418494 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:03,067 : INFO : EPOCH 10 - PROGRESS: at 59.83% examples, 418568 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:20:04,068 : INFO : EPOCH 10 - PROGRESS: at 60.51% examples, 418666 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:20:05,099 : INFO : EPOCH 10 - PROGRESS: at 61.19% examples, 418777 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:06,104 : INFO : EPOCH 10 - PROGRESS: at 61.84% examples, 418646 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:20:07,107 : INFO : EPOCH 10 - PROGRESS: at 62.55% examples, 418565 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:20:08,110 : INFO : EPOCH 10 - PROGRESS: at 63.28% examples, 418629 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:20:09,125 : INFO : EPOCH 10 - PROGRESS: at 63.97% examples, 418531 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:20:10,136 : INFO : EPOCH 10 - PROGRESS: at 64.71% examples, 418715 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:11,151 : INFO : EPOCH 10 - PROGRESS: at 65.35% examples, 418547 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:20:12,169 : INFO : EPOCH 10 - PROGRESS: at 65.96% examples, 418620 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:13,173 : INFO : EPOCH 10 - PROGRESS: at 66.47% examples, 418490 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:20:14,180 : INFO : EPOCH 10 - PROGRESS: at 66.83% examples, 418464 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:20:15,188 : INFO : EPOCH 10 - PROGRESS: at 67.23% examples, 418444 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:20:16,202 : INFO : EPOCH 10 - PROGRESS: at 67.97% examples, 418470 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:17,204 : INFO : EPOCH 10 - PROGRESS: at 68.68% examples, 418394 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:18,204 : INFO : EPOCH 10 - PROGRESS: at 69.42% examples, 418447 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:19,212 : INFO : EPOCH 10 - PROGRESS: at 70.19% examples, 418401 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:20:20,216 : INFO : EPOCH 10 - PROGRESS: at 71.08% examples, 418537 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:21,236 : INFO : EPOCH 10 - PROGRESS: at 71.94% examples, 418503 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:20:22,241 : INFO : EPOCH 10 - PROGRESS: at 72.74% examples, 418558 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:23,263 : INFO : EPOCH 10 - PROGRESS: at 73.43% examples, 418510 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:20:24,265 : INFO : EPOCH 10 - PROGRESS: at 74.01% examples, 418393 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:25,286 : INFO : EPOCH 10 - PROGRESS: at 74.67% examples, 418303 words/s, in_qsize 5, out_qsize 2
2021-09-29 16:20:26,306 : INFO : EPOCH 10 - PROGRESS: at 75.23% examples, 418419 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:27,322 : INFO : EPOCH 10 - PROGRESS: at 75.82% examples, 418354 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:20:28,323 : INFO : EPOCH 10 - PROGRESS: at 76.58% examples, 418353 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:29,329 : INFO : EPOCH 10 - PROGRESS: at 77.36% examples, 418343 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:20:30,337 : INFO : EPOCH 10 - PROGRESS: at 78.11% examples, 418464 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:31,341 : INFO : EPOCH 10 - PROGRESS: at 78.81% examples, 418412 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:32,353 : INFO : EPOCH 10 - PROGRESS: at 79.48% examples, 418416 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:20:33,390 : INFO : EPOCH 10 - PROGRESS: at 80.13% examples, 418373 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:20:34,402 : INFO : EPOCH 10 - PROGRESS: at 80.84% examples, 418461 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:35,432 : INFO : EPOCH 10 - PROGRESS: at 81.57% examples, 418467 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:20:36,442 : INFO : EPOCH 10 - PROGRESS: at 82.38% examples, 418459 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:37,445 : INFO : EPOCH 10 - PROGRESS: at 83.02% examples, 418481 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:20:38,448 : INFO : EPOCH 10 - PROGRESS: at 83.50% examples, 418511 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:20:39,452 : INFO : EPOCH 10 - PROGRESS: at 84.28% examples, 418556 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:20:40,459 : INFO : EPOCH 10 - PROGRESS: at 85.01% examples, 418491 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:20:41,472 : INFO : EPOCH 10 - PROGRESS: at 85.79% examples, 418528 words/s, in_qsize 4, out_qsize 2
2021-09-29 16:20:42,476 : INFO : EPOCH 10 - PROGRESS: at 86.38% examples, 418546 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:43,509 : INFO : EPOCH 10 - PROGRESS: at 87.04% examples, 418564 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:44,526 : INFO : EPOCH 10 - PROGRESS: at 87.74% examples, 418603 words/s, in_qsize 5, out_qsize 1
2021-09-29 16:20:45,539 : INFO : EPOCH 10 - PROGRESS: at 88.46% examples, 418650 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:46,562 : INFO : EPOCH 10 - PROGRESS: at 89.10% examples, 418762 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:47,585 : INFO : EPOCH 10 - PROGRESS: at 89.92% examples, 418729 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:48,600 : INFO : EPOCH 10 - PROGRESS: at 90.66% examples, 418821 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:20:49,617 : INFO : EPOCH 10 - PROGRESS: at 91.18% examples, 418900 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:50,633 : INFO : EPOCH 10 - PROGRESS: at 91.68% examples, 418922 words/s, in_qsize 4, out_qsize 1
2021-09-29 16:20:51,663 : INFO : EPOCH 10 - PROGRESS: at 92.18% examples, 418952 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:20:52,701 : INFO : EPOCH 10 - PROGRESS: at 92.68% examples, 418919 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:20:53,718 : INFO : EPOCH 10 - PROGRESS: at 93.20% examples, 419038 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:20:54,722 : INFO : EPOCH 10 - PROGRESS: at 93.69% examples, 419093 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:20:55,729 : INFO : EPOCH 10 - PROGRESS: at 94.16% examples, 419047 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:20:56,746 : INFO : EPOCH 10 - PROGRESS: at 94.65% examples, 419056 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:20:57,765 : INFO : EPOCH 10 - PROGRESS: at 95.18% examples, 419197 words/s, in_qsize 6, out_qsize 0
2021-09-29 16:20:58,789 : INFO : EPOCH 10 - PROGRESS: at 95.68% examples, 419182 words/s, in_qsize 6, out_qsize 1
2021-09-29 16:20:59,794 : INFO : EPOCH 10 - PROGRESS: at 96.18% examples, 419128 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:21:00,802 : INFO : EPOCH 10 - PROGRESS: at 96.69% examples, 419153 words/s, in_qsize 6, out_qsize 2
2021-09-29 16:21:01,819 : INFO : EPOCH 10 - PROGRESS: at 97.25% examples, 419257 words/s, in_qsize 5, out_qsize 0
2021-09-29 16:21:02,633 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-29 16:21:02,638 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-29 16:21:02,639 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-29 16:21:02,639 : INFO : EPOCH - 10 : training on 96321721 raw words (70191531 effective words) took 167.3s, 419561 effective words/s
2021-09-29 16:21:02,639 : INFO : training on a 963217210 raw words (701895765 effective words) took 1689.0s, 415572 effective words/s
2021-09-29 16:21:02,639 : INFO : storing 331256x200 projection weights into /media/ye/project2/exp/bilingual-induction/exp1/en/en_corpus.txt_model=word2vec_vectors.vec
Loading corpus: /media/ye/project2/exp/bilingual-induction/exp1/en/en_corpus.txt
Embeddings saved to /media/ye/project2/exp/bilingual-induction/exp1/en/en_corpus.txt_model=word2vec_vectors.vec

real	31m22.924s
user	46m33.596s
sys	0m11.100s
check for SRC:  see word2vec and fastext models...
3_all.my.word
corpus2-and-para
data_myn-token.txt.line.rm-lineno
fasttext
my_corpus.txt
my_corpus.txt_model=fasttext_vectors.vec
my_corpus.txt_model=word2vec_vectors.vec
word2vec
check for TRG:  see word2vec and fastext models...
1_all.en.word
big-model
data_eng.txt
en_corpus.txt
en_corpus.txt_model=word2vec_vectors.vec
UMBC_tokenized_1million.txt
word2vec
mkdir word2vec-output10/
mkdir: cannot create directory ‘/media/ye/project2/exp/bilingual-induction/exp1/my-en/word2vec-output10/’: File exists
Processing /media/ye/project2/exp/bilingual-induction/exp1/my/word2vec/my_corpus.txt_model=word2vec_vectors.vec
Processing /media/ye/project2/exp/bilingual-induction/exp1/en/word2vec/en_corpus.txt_model=word2vec_vectors.vec
Source vocab is 56038 tokens
Target vocab is 1887310 tokens

real	0m34.501s
user	0m24.654s
sys	0m1.381s
source_vocab.txt  target_vocab.txt  test_dict.csv  train_dict.csv
Loading source vocab
Source vocab has 56038 words
---
Loading target vocab
Target vocab has 1887310 words
Loading dictionary - Done 1000 of 57326
Loading dictionary - Done 2000 of 57326
Loading dictionary - Done 3000 of 57326
Loading dictionary - Done 4000 of 57326
Loading dictionary - Done 5000 of 57326
Loading dictionary - Done 6000 of 57326
Loading dictionary - Done 7000 of 57326
Loading dictionary - Done 8000 of 57326
Loading dictionary - Done 9000 of 57326
Loading dictionary - Done 10000 of 57326
Loading dictionary - Done 11000 of 57326
Loading dictionary - Done 12000 of 57326
Loading dictionary - Done 13000 of 57326
Loading dictionary - Done 14000 of 57326
Loading dictionary - Done 15000 of 57326
Loading dictionary - Done 16000 of 57326
Loading dictionary - Done 17000 of 57326
Loading dictionary - Done 18000 of 57326
Loading dictionary - Done 19000 of 57326
Loading dictionary - Done 20000 of 57326
Loading dictionary - Done 21000 of 57326
Loading dictionary - Done 22000 of 57326
Loading dictionary - Done 23000 of 57326
Loading dictionary - Done 24000 of 57326
Loading dictionary - Done 25000 of 57326
Loading dictionary - Done 26000 of 57326
Loading dictionary - Done 27000 of 57326
Loading dictionary - Done 28000 of 57326
Loading dictionary - Done 29000 of 57326
Loading dictionary - Done 30000 of 57326
Loading dictionary - Done 31000 of 57326
Loading dictionary - Done 32000 of 57326
Loading dictionary - Done 33000 of 57326
Loading dictionary - Done 34000 of 57326
Loading dictionary - Done 35000 of 57326
Loading dictionary - Done 36000 of 57326
Loading dictionary - Done 37000 of 57326
Loading dictionary - Done 38000 of 57326
Loading dictionary - Done 39000 of 57326
Loading dictionary - Done 40000 of 57326
Loading dictionary - Done 41000 of 57326
Loading dictionary - Done 42000 of 57326
Loading dictionary - Done 43000 of 57326
Loading dictionary - Done 44000 of 57326
Loading dictionary - Done 45000 of 57326
Loading dictionary - Done 46000 of 57326
Loading dictionary - Done 47000 of 57326
Loading dictionary - Done 48000 of 57326
Loading dictionary - Done 49000 of 57326
Loading dictionary - Done 50000 of 57326
Loading dictionary - Done 51000 of 57326
Loading dictionary - Done 52000 of 57326
Loading dictionary - Done 53000 of 57326
Loading dictionary - Done 54000 of 57326
Loading dictionary - Done 55000 of 57326
Loading dictionary - Done 56000 of 57326
Loading dictionary - Done 57000 of 57326
Loaded 12047 entries from the original dictionary, which had: 57326

real	0m1.986s
user	0m1.678s
sys	0m1.052s
source_vocab.txt  target_vocab.txt  test_dict.csv  train_dict.csv
run get_vocab_from_vectors.py ...
Processing /media/ye/project2/exp/bilingual-induction/exp1/my/word2vec/my_corpus.txt_model=word2vec_vectors.vec
Processing /media/ye/project2/exp/bilingual-induction/exp1/en/word2vec/en_corpus.txt_model=word2vec_vectors.vec
Source vocab is 56038 tokens
Target vocab is 1887310 tokens

real	0m25.214s
user	0m22.957s
sys	0m0.995s
mkdir vecmap-output10/
mkdir: cannot create directory ‘/media/ye/project2/exp/bilingual-induction/exp1/my-en/vecmap-output10/’: File exists
run mk-vecmap.sh ...
WARNING: OOV dictionary entry (english - welsh)
WARNING: OOV dictionary entry (အရှုပ်တော်ပုံ - scandalmongering)
WARNING: OOV dictionary entry (မသန်စွမ်း - disenable)
WARNING: OOV dictionary entry (အလွန့်အလွန် - deviously)
WARNING: OOV dictionary entry (ခဲတံ - pennon)
WARNING: OOV dictionary entry (ကစားသူ - playgoer)
WARNING: OOV dictionary entry (အူဝဲ - howlingly)
WARNING: OOV dictionary entry (ဆိုးဆိုးရွားရွား - odiously)
WARNING: OOV dictionary entry (ပါးစပ် - mouthpart)
WARNING: OOV dictionary entry (ပါးရိုး - jag)
WARNING: OOV dictionary entry (သတ်မှတ်ချက် - stipel)
WARNING: OOV dictionary entry (နာရီ - stopclock)
WARNING: OOV dictionary entry (ဆောင်းရာသီ - winterize)
WARNING: OOV dictionary entry (ခိုးဝှက် - burglarize)
WARNING: OOV dictionary entry (လေးထောင့် - quadrivalent)
WARNING: OOV dictionary entry (အရောင်ဖျော့ - paleface)
WARNING: OOV dictionary entry (တော - wilde)
WARNING: OOV dictionary entry (ကျွမ်းကျင်မှု - professionalisation)
WARNING: OOV dictionary entry (သံပုရာသီး - limeade)
WARNING: OOV dictionary entry (ဓာတ်မှန် - heliograph)
WARNING: OOV dictionary entry (လက်လုပ် - handwrought)
WARNING: OOV dictionary entry (အိမ်သာ - toilette)
WARNING: OOV dictionary entry (နောက်ဆုံး - lattermost)
WARNING: OOV dictionary entry (သဲသဲမဲမဲ - unfrock)
WARNING: OOV dictionary entry (ကန်ပေါင် - embank)
WARNING: OOV dictionary entry (မီးတောက် - incandesce)
WARNING: OOV dictionary entry (ချစ်သူ - dearie)
WARNING: OOV dictionary entry (အလှူရှင် - donator)
WARNING: OOV dictionary entry (ကြောက်စရာ - scarer)
WARNING: OOV dictionary entry (ရွက်လှေ - yachtswoman)
WARNING: OOV dictionary entry (တွစ်တာ - twitcher)
WARNING: OOV dictionary entry (အနောက်တောင် - southwester)
WARNING: OOV dictionary entry (လူမိုက် - bumf)
WARNING: OOV dictionary entry (ချိပ် - lac)
WARNING: OOV dictionary entry (ပြပွဲ - exhibitive)
WARNING: OOV dictionary entry (လက်ခံသူ - acceptant)
WARNING: OOV dictionary entry (ချန်ပီယံ - champaign)
WARNING: OOV dictionary entry (ညီညွတ်ခြင်း - unconformity)
WARNING: OOV dictionary entry (ရာသီဥတု - weatherly)
WARNING: OOV dictionary entry (အရွက် - leafage)
WARNING: OOV dictionary entry (နွေရာသီ - summersault)
WARNING: OOV dictionary entry (ရွံ့ရှာ - vixenish)
WARNING: OOV dictionary entry (ပဲပုတ် - cowpea)
WARNING: OOV dictionary entry (ညစာ - truncheon)
WARNING: OOV dictionary entry (ဥရောပ - europium)
WARNING: OOV dictionary entry (အဖွားအို - grandmamma)
WARNING: OOV dictionary entry (ဇိုး - swiftlet)
WARNING: OOV dictionary entry (အထမ်းသမား - porterhouse)
WARNING: OOV dictionary entry (တရားခံ - ullage)
WARNING: OOV dictionary entry (တောင်ဘက် - southland)
WARNING: OOV dictionary entry (အကြောင်းအရင်း - causerie)
WARNING: OOV dictionary entry (အိမ်ထောင်ဖက် - matey)
WARNING: OOV dictionary entry (စားပွဲထိုး - deskman)
WARNING: OOV dictionary entry (အလေးချိန် - weigher)
WARNING: OOV dictionary entry (ပစ်ပေါက် - spick)
WARNING: OOV dictionary entry (သေနတ်သမား - rifleman)
WARNING: OOV dictionary entry (လက်အောက်ငယ်သား - subordinator)
WARNING: OOV dictionary entry (အဆုံး - endmost)
WARNING: OOV dictionary entry (ရူ - rouble)
WARNING: OOV dictionary entry (တရားဝင် - officinal)
WARNING: OOV dictionary entry (လေးပုံတစ်ပုံ - quartette)
WARNING: OOV dictionary entry (ကြမ်း - draff)
WARNING: OOV dictionary entry (ယာဉ်စီးခ - carfare)
WARNING: OOV dictionary entry (သရက်သီး - locknut)
WARNING: OOV dictionary entry (ရှားပါး - rarefy)
WARNING: OOV dictionary entry (ကျင့်ဝတ် - adduct)
WARNING: OOV dictionary entry (အတားအဆီး - obstructiveness)
WARNING: OOV dictionary entry (ပုံပျက်ပန်းပျက် - distortedly)
WARNING: OOV dictionary entry (ကော့ - cox)
WARNING: OOV dictionary entry (ထိထိရောက်ရောက် - effervesce)
WARNING: OOV dictionary entry (ကြောင်ကလေး - kittenish)
WARNING: OOV dictionary entry (အလုပ်အကိုင် - jobbery)
WARNING: OOV dictionary entry (ဟဲဟဲ - heehaw)
WARNING: OOV dictionary entry (ဝန်ဆောင်မှု - serviette)
WARNING: OOV dictionary entry (ခြင်းတောင်း - basketwork)
WARNING: OOV dictionary entry (ပြောင်းပြန် - revers)
WARNING: OOV dictionary entry (စကိတ်စီး - skedaddle)
WARNING: OOV dictionary entry (ဗေဒ - thanatology)
WARNING: OOV dictionary entry (ဘာဘီ - barbie)
WARNING: OOV dictionary entry (ဟောလိဝုဒ် - halliard)
WARNING: OOV dictionary entry (ပေးပါ - gimme)
WARNING: OOV dictionary entry (အိမ်မြှောင် - lurcher)
WARNING: OOV dictionary entry (မယ်ဒလင် - mandolinist)
WARNING: OOV dictionary entry (ကုန်သွယ်ရေး - amerce)
WARNING: OOV dictionary entry (ဆိတ်သား - goatish)
WARNING: OOV dictionary entry (အပျိုစင် - maidenly)
WARNING: OOV dictionary entry (တောက်ပ - glower)
WARNING: OOV dictionary entry (ရှယ်ယာရှင် - shareowner)
WARNING: OOV dictionary entry (ရေဗက္ကာ - rebec)
WARNING: OOV dictionary entry (အလုပ်သင် - interne)
WARNING: OOV dictionary entry (ငါးရံ့ - sylph)
WARNING: OOV dictionary entry (သပ်သပ်ရပ်ရပ် - neaten)
WARNING: OOV dictionary entry (မာဂျရင်း - margarin)
WARNING: OOV dictionary entry (ပြဇာတ် - playsuit)
WARNING: OOV dictionary entry (တွန်းအား - impetuousness)
WARNING: OOV dictionary entry (အပြတ်အသတ် - landslip)
WARNING: OOV dictionary entry (အနီးဆုံး - nethermost)
WARNING: OOV dictionary entry (လူလိမ် - luff)
WARNING: OOV dictionary entry (ပိတုန်း - bumble)
WARNING: OOV dictionary entry (ဆွဲဆောင်မှု - engrossment)
WARNING: OOV dictionary entry (အမှား - mishear)
WARNING: OOV dictionary entry (ချစ်သား - fellah)
WARNING: OOV dictionary entry (ပြိုင်ပွဲဝင် - racegoer)
WARNING: OOV dictionary entry (လက်ရှိ - procumbent)
WARNING: OOV dictionary entry (ဝီရိယ - wiliness)
WARNING: OOV dictionary entry (ငါးပိ - pasteurise)
WARNING: OOV dictionary entry (ကော်မရှင်နာ - commissionaire)
WARNING: OOV dictionary entry (ခြေကျင်း - anklet)
WARNING: OOV dictionary entry (စာရေးဆရာ - clerisy)
WARNING: OOV dictionary entry (အိုး - uhu)
WARNING: OOV dictionary entry (မှုတ်ထုတ် - blowzy)
WARNING: OOV dictionary entry (အံ့မခန်း - umbrageous)
WARNING: OOV dictionary entry (ပိုးကောင် - poulterer)
WARNING: OOV dictionary entry (ငါးပိ - waspish)
WARNING: OOV dictionary entry (မျှော်လင့်ချက် - suppositious)
WARNING: OOV dictionary entry (အထီးကျန် - seclusive)
WARNING: OOV dictionary entry (သိသိသာသာ - viscously)
WARNING: OOV dictionary entry (ဆိတ်သား - goatsucker)
WARNING: OOV dictionary entry (အဖျား - feverfew)
WARNING: OOV dictionary entry (အရှိတရား - factitious)
WARNING: OOV dictionary entry (ဒီမိုကရေစီ - democratism)
WARNING: OOV dictionary entry (ပုဒ်ဖြတ် - punctilio)
WARNING: OOV dictionary entry (မျက်နှာ - tufaceous)
WARNING: OOV dictionary entry (ဆွဲတင် - pullup)
WARNING: OOV dictionary entry (မျက်နှာဖုံး - impanel)
WARNING: OOV dictionary entry (ရေကြောင်း - nautically)
WARNING: OOV dictionary entry (ပြင်းပြင်းထန်ထန် - vivaciously)
WARNING: OOV dictionary entry (ဝီရိယ - wistfulness)
WARNING: OOV dictionary entry (အမှတ်အသား - markedness)
WARNING: OOV dictionary entry (ကွဲကွဲပြားပြား - disunite)
WARNING: OOV dictionary entry (စာကြည့်တိုက် - pressroom)
WARNING: OOV dictionary entry (မုန်တိုင်း - stormer)
WARNING: OOV dictionary entry (တံခါးပေါက် - gateaux)
WARNING: OOV dictionary entry (ဝက်သား - muttonhead)
WARNING: OOV dictionary entry (မျက်ခုံးမွေး - middlebrow)
WARNING: OOV dictionary entry (ကျိန်ဆို - swearword)
WARNING: OOV dictionary entry (စားသုံးမှု - alimentation)
WARNING: OOV dictionary entry (စပျစ်သီး - grapey)
WARNING: OOV dictionary entry (မော်တော်ဆိုင်ကယ် - motorbus)
WARNING: OOV dictionary entry (လှော် - diddle)
WARNING: OOV dictionary entry (ကြက်ကင် - roister)
WARNING: OOV dictionary entry (ဆန့်ကျင် - contuse)
WARNING: OOV dictionary entry (ကျား - tigerish)
WARNING: OOV dictionary entry (ဂုဏ် - splendent)
WARNING: OOV dictionary entry (မချိတင်ကဲ - disconsolately)
WARNING: OOV dictionary entry (ရိုးတွင်းခြင်ဆီ - marrowbone)
WARNING: OOV dictionary entry (လက်ကမ်းစာစောင် - handbill)
WARNING: OOV dictionary entry (မကျေမနပ် - dissonantly)
WARNING: OOV dictionary entry (ဒေါင်လိုက် - vert)
WARNING: OOV dictionary entry (ဆီးအိမ် - pule)
WARNING: OOV dictionary entry (အကျည်းတန် - scummy)
WARNING: OOV dictionary entry (ရုပ်ရှင် - moviedom)
WARNING: OOV dictionary entry (တေးရေးဆရာ - melodist)
WARNING: OOV dictionary entry (အစွမ်းထက် - potful)
WARNING: OOV dictionary entry (အလွန်အကျွံ - oversteer)
WARNING: OOV dictionary entry (သိသိသာသာ - mawkishly)
WARNING: OOV dictionary entry (လုပ်ခ - wagerer)
WARNING: OOV dictionary entry (ခမ်းနား - magnific)
WARNING: OOV dictionary entry (ဒါပဲ - dah)
WARNING: OOV dictionary entry (အမြန်လမ်း - speedwalk)
WARNING: OOV dictionary entry (စပ်ကြား - spic)
WARNING: OOV dictionary entry (ကျောပိုးအိတ် - afterdeck)
WARNING: OOV dictionary entry (မျက်မမြင် - purblind)
WARNING: OOV dictionary entry (ရှေ့ဆောင် - vanguardist)
WARNING: OOV dictionary entry (ချိတ်ပိုး - hookworm)
WARNING: OOV dictionary entry (သိမ်းငှက် - falchion)
WARNING: OOV dictionary entry (ရယ် - faugh)
WARNING: OOV dictionary entry (ယဉ်ကျေးမှု - civilise)
WARNING: OOV dictionary entry (မသိမသာ - witlessly)
WARNING: OOV dictionary entry (အအေးခန်း - refrigerative)
WARNING: OOV dictionary entry (အပူပိုင်းဒေသ - tropism)
WARNING: OOV dictionary entry (သော့ခလောက် - bollocks)
WARNING: OOV dictionary entry (အားမာန် - vigorousness)
WARNING: OOV dictionary entry (ဥယျာဉ်ခြံ - gardenia)
WARNING: OOV dictionary entry (စစ်အစိုးရ - junto)
WARNING: OOV dictionary entry (အထိတ်တလန့် - carious)
WARNING: OOV dictionary entry (လုပ်ပိုင်ခွင့် - mandator)
WARNING: OOV dictionary entry (ခွက် - cupreous)
WARNING: OOV dictionary entry (အသံထွက် - pronunciamento)
WARNING: OOV dictionary entry (မင်္ဂလာဆောင် - wedgelike)
WARNING: OOV dictionary entry (နေရောင်ခြည် - solarize)
WARNING: OOV dictionary entry (အိုကေ - och)
WARNING: OOV dictionary entry (ရောဂါဗေဒ - pedology)
WARNING: OOV dictionary entry (ဌာနခွဲ - compartmentalise)
WARNING: OOV dictionary entry (ဒေဝီ - deva)
WARNING: OOV dictionary entry (နက်ပကျွန်း - neptune)
WARNING: OOV dictionary entry (တရကြမ်း - turbulently)
WARNING: OOV dictionary entry (စိတ်ပညာရှင် - mentalist)
WARNING: OOV dictionary entry (အရောင်တင် - palish)
WARNING: OOV dictionary entry (ကိတ်မုန့် - cakehole)
WARNING: OOV dictionary entry (မြောက်ဘက် - northcountry)
WARNING: OOV dictionary entry (ပန်း - floristry)
WARNING: OOV dictionary entry (ညှိနှိုင်းမှု - convenance)
WARNING: OOV dictionary entry (အနောက်ဘက် - westing)
WARNING: OOV dictionary entry (လုပ်သား - laborite)
WARNING: OOV dictionary entry (အပိုင်းပိုင်း - segmentally)
WARNING: OOV dictionary entry (ဂျီ - gie)
WARNING: OOV dictionary entry (တိတိကျကျ - punctiliously)
WARNING: OOV dictionary entry (ဟေ့ - ahoy)
WARNING: OOV dictionary entry (မိုးခြိမ်းသံ - thunderthighs)
WARNING: OOV dictionary entry (အလုပ်သမား - outworker)
WARNING: OOV dictionary entry (မက်ဒရစ် - madden)
WARNING: OOV dictionary entry (ရေနံဆီ - kerosine)
WARNING: OOV dictionary entry (ကုတင် - bedsit)
WARNING: OOV dictionary entry (ခေါင်းစွပ် - headstand)
WARNING: OOV dictionary entry (ပယ်ဖျက် - cancellate)
WARNING: OOV dictionary entry (ဥယျာဉ်မှူး - orchardist)
WARNING: OOV dictionary entry (ဒေလီယာ - dahlia)
WARNING: OOV dictionary entry (သကြားလုံး - candyfloss)
WARNING: OOV dictionary entry (ရထားထိန်း - trainman)
WARNING: OOV dictionary entry (မျက်မြင် - sightly)
WARNING: OOV dictionary entry (တိတ်တဆိတ် - crawly)
WARNING: OOV dictionary entry (ပေါင်းစပ် - compend)
WARNING: OOV dictionary entry (လွဲချော် - misspend)
WARNING: OOV dictionary entry (ပျက်ပြယ် - voidance)
WARNING: OOV dictionary entry (လက်နက်မဲ့ - unarm)
WARNING: OOV dictionary entry (ဆက်တိုက် - rowdily)
WARNING: OOV dictionary entry (ကြိတ်စက် - lathing)
WARNING: OOV dictionary entry (တီးဝိုင်း - bandsman)
WARNING: OOV dictionary entry (သတ်မှတ်ချက် - stipule)
WARNING: OOV dictionary entry (သုံးကြိမ် - trifocal)
WARNING: OOV dictionary entry (ရောနှော - blench)
WARNING: OOV dictionary entry (ဆေးရည် - potation)
WARNING: OOV dictionary entry (နား - earing)
WARNING: OOV dictionary entry (မသိ - unbeknown)
WARNING: OOV dictionary entry (ကလဲ့စားချေ - venge)
WARNING: OOV dictionary entry (လေပြည် - zephyr)
WARNING: OOV dictionary entry (အမြတ်အစွန်း - profiterole)
WARNING: OOV dictionary entry (တာရာ - tarsus)
WARNING: OOV dictionary entry (ဆရာ - overmaster)
WARNING: OOV dictionary entry (မကျေမနပ် - disgruntle)
WARNING: OOV dictionary entry (ဆောင်ပုဒ် - blotto)
WARNING: OOV dictionary entry (ခွေးသား - dogmeat)
WARNING: OOV dictionary entry (ခုန် - jounce)
WARNING: OOV dictionary entry (ပင်လယ်လှိုင်း - wassail)
WARNING: OOV dictionary entry (လမ်းပန်းဆက်သွယ်ရေး - roadability)
WARNING: OOV dictionary entry (ပညာရေး - educability)
WARNING: OOV dictionary entry (ခေါင်းစီး - towhead)
WARNING: OOV dictionary entry (အမိန့် - delict)
WARNING: OOV dictionary entry (ခလုတ် - keypunch)
WARNING: OOV dictionary entry (အရေးမပါ - quincuncial)
WARNING: OOV dictionary entry (ကူးစက်ရောဂါ - epidiascope)
WARNING: OOV dictionary entry (ခေါင်းစွပ် - headpin)
WARNING: OOV dictionary entry (ဘီလူး - ogress)
WARNING: OOV dictionary entry (အောက်ခြေ - frump)
WARNING: OOV dictionary entry (အိမ်နီးချင်း - weighbridge)
WARNING: OOV dictionary entry (ကျောင်းဆရာမ - schoolmistress)
WARNING: OOV dictionary entry (တရားခံ - vindicatory)
WARNING: OOV dictionary entry (ပြတ်ပြတ်သားသား - indiscrete)
WARNING: OOV dictionary entry (သံလမ်း - railroader)
WARNING: OOV dictionary entry (ဟာဂျီ - hajji)
WARNING: OOV dictionary entry (အဇာတသတ် - patricidal)
WARNING: OOV dictionary entry (ပြင်းပြင်းထန်ထန် - peevishly)
WARNING: OOV dictionary entry (သတ္တု - metalled)
WARNING: OOV dictionary entry (သေတ္တာ - boxroom)
WARNING: OOV dictionary entry (ဆီးအိမ် - saccule)
WARNING: OOV dictionary entry (ကမ်းရိုးတန်း - coastland)
WARNING: OOV dictionary entry (ပန်းပွင့် - flowerer)
WARNING: OOV dictionary entry (အားနည်းချက် - vulnerary)
WARNING: OOV dictionary entry (ထိုသို့ - thitherto)
WARNING: OOV dictionary entry (ပို - soarer)
WARNING: OOV dictionary entry (လိပ်စာ - addresser)
WARNING: OOV dictionary entry (ငါးခူ - filefish)
WARNING: OOV dictionary entry (နိယာမ - intinction)
WARNING: OOV dictionary entry (ကြမ်းပြင် - vulpine)
WARNING: OOV dictionary entry (ပြဇာတ် - playact)
WARNING: OOV dictionary entry (ခြံစောင့် - yardmaster)
WARNING: OOV dictionary entry (အိမ်ရှင် - hostler)
WARNING: OOV dictionary entry (အဆမတန် - overweigh)
WARNING: OOV dictionary entry (အနောက်မြောက် - northwester)
WARNING: OOV dictionary entry (မပြေမလည် - unsmooth)
WARNING: OOV dictionary entry (အကြောင်းပြချက် - ratiocinator)
WARNING: OOV dictionary entry (ခေါင်းလိမ်းဆီ - pomade)
WARNING: OOV dictionary entry (ပေါ့ပေါ့တန်တန် - flashily)
WARNING: OOV dictionary entry (အမှန် - veridical)
WARNING: OOV dictionary entry (နေထိုင်မှု - inhabitancy)
WARNING: OOV dictionary entry (မှို - moult)
WARNING: OOV dictionary entry (နှင်းပေါက် - snowcap)
WARNING: OOV dictionary entry (ရှပ်အင်္ကျီ - shirtwaist)
WARNING: OOV dictionary entry (ရောင်ပြန် - reflectiveness)
WARNING: OOV dictionary entry (ဒေါသစိတ် - ruefulness)
WARNING: OOV dictionary entry (ရုပ်ကလာပ် - cadaverous)
WARNING: OOV dictionary entry (ရေချိုးခန်း - showery)
WARNING: OOV dictionary entry (အသေးစား - miniaturise)
WARNING: OOV dictionary entry (ရည်ရွယ်ချက် - intendance)
WARNING: OOV dictionary entry (အစွယ် - yaws)
WARNING: OOV dictionary entry (ဖြိုဖျက် - dissimilate)
WARNING: OOV dictionary entry (ဂျယ်လီ - geld)
WARNING: OOV dictionary entry (တယ်လီနော - telly)
WARNING: OOV dictionary entry (ပညာရှိ - wiseacre)
WARNING: OOV dictionary entry (မီးခွက် - chandlery)
WARNING: OOV dictionary entry (သဘာဝကျကျ - naturalise)
WARNING: OOV dictionary entry (သတင်းစာဆရာ - newspaperwoman)
WARNING: OOV dictionary entry (ရယ်စရာ - funniness)
WARNING: OOV dictionary entry (အနုပညာသမား - artillerist)
WARNING: OOV dictionary entry (စစ်ဆေးခြင်း - vetchling)
WARNING: OOV dictionary entry (ပါလက်စတိုင်း - palestinian)
WARNING: OOV dictionary entry (ချေဖျက် - detune)
WARNING: OOV dictionary entry (ကြက်လျှာ - pennate)
WARNING: OOV dictionary entry (ဆွတ်ဆွတ် - gloaming)
WARNING: OOV dictionary entry (မိုးကျရွှေကိုယ် - nonpareil)
WARNING: OOV dictionary entry (ကြိုတင်လက်မှတ် - pretermit)
WARNING: OOV dictionary entry (ညစာ - tinner)
WARNING: OOV dictionary entry (ဘက်ထရီ - cattery)
WARNING: OOV dictionary entry (အသစ်အဆန်း - novelize)
WARNING: OOV dictionary entry (သွေးပြန်ကြော - veinal)
WARNING: OOV dictionary entry (လူဆိုး - villainously)
WARNING: OOV dictionary entry (တစ်ဝက် - semiweekly)
WARNING: OOV dictionary entry (ပြူတင်းပေါက် - peeper)
WARNING: OOV dictionary entry (အခိုက်အတန့် - trice)
WARNING: OOV dictionary entry (အသစ် - newel)
WARNING: OOV dictionary entry (ခိုင်ခိုင် - groundsel)
WARNING: OOV dictionary entry (ညဘက် - nighty)
WARNING: OOV dictionary entry (တိုင်းတာ - measurer)
WARNING: OOV dictionary entry (ဝံပုလွေ - werwolf)
WARNING: OOV dictionary entry (အဖုံး - casement)
WARNING: OOV dictionary entry (ဆတ်ဆတ် - snaky)
WARNING: OOV dictionary entry (ပုတီးစိပ် - beadle)
WARNING: OOV dictionary entry (သက်သေ - provenience)
WARNING: OOV dictionary entry (အစာမကြေ - indigested)
WARNING: OOV dictionary entry (လက်တင် - latish)
WARNING: OOV dictionary entry (မှီခို - impend)
WARNING: OOV dictionary entry (တိုတို - foreshorten)
WARNING: OOV dictionary entry (စက်ခေါင်း - locomobile)
WARNING: OOV dictionary entry (တောက်ပ - brill)
WARNING: OOV dictionary entry (သိသိသာသာ - saliently)
WARNING: OOV dictionary entry (လေယာဉ်ပျံ - emplane)
WARNING: OOV dictionary entry (ကျော်ကြား - wame)
WARNING: OOV dictionary entry (လည်ပင်း - ringneck)
WARNING: OOV dictionary entry (အကျပ်အတည်း - trouper)
WARNING: OOV dictionary entry (အထူးပြု - particularise)
WARNING: OOV dictionary entry (ပြဇာတ်ရုံ - portiere)
WARNING: OOV dictionary entry (ဘေဘီ - babel)
WARNING: OOV dictionary entry (ညနေခင်း - evenfall)
WARNING: OOV dictionary entry (ဖန်ခွက် - glassful)
WARNING: OOV dictionary entry (ကျေးလက် - fustic)
WARNING: OOV dictionary entry (အနီးကပ် - appose)
WARNING: OOV dictionary entry (ဘုန်းကြီးကျောင်း - monasterial)
WARNING: OOV dictionary entry (သမားရိုးကျ - conventionalize)
WARNING: OOV dictionary entry (လက်နက် - weaponeer)
WARNING: OOV dictionary entry (ဆောင်းရာသီ - wowser)
WARNING: OOV dictionary entry (နံရံကပ် - wallower)
WARNING: OOV dictionary entry (ပျော်ရွှင်မှု - merriness)
WARNING: OOV dictionary entry (ဓာတ်သတ္တု - mineralogically)
WARNING: OOV dictionary entry (ဘာဘူ - baboo)
WARNING: OOV dictionary entry (အိပ်ရာခင်း - bedpost)
WARNING: OOV dictionary entry (အမျိုးအစား - assort)
WARNING: OOV dictionary entry (ရိုးရှင်း - simp)
WARNING: OOV dictionary entry (စာတန်းထိုး - castellated)
WARNING: OOV dictionary entry (နေ့စေ့လစေ့ - parturient)
WARNING: OOV dictionary entry (ရန်ပွဲ - outre)
WARNING: OOV dictionary entry (မိနစ် - minuend)
WARNING: OOV dictionary entry (ပညာရှိ - witted)
WARNING: OOV dictionary entry (ရံခါ - periphrastically)
WARNING: OOV dictionary entry (လက်သည်း - palmate)
WARNING: OOV dictionary entry (အပ်ငွေ - deposal)
WARNING: OOV dictionary entry (အနည်းငယ် - scantly)
WARNING: OOV dictionary entry (နှစ်ထပ် - quadrantal)
WARNING: OOV dictionary entry (စုရုံး - ingather)
WARNING: OOV dictionary entry (မသိမသာ - uncourtly)
WARNING: OOV dictionary entry (ရက်တို - rackety)
WARNING: OOV dictionary entry (မြေပြင် - groundling)
WARNING: OOV dictionary entry (ငိုကြွေးသံ - weeper)
WARNING: OOV dictionary entry (မင်္ဂလာ - blether)
WARNING: OOV dictionary entry (အဆန်း - oddment)
WARNING: OOV dictionary entry (အိုကေ - oik)
WARNING: OOV dictionary entry (အဋ္ဌမ - absinth)
WARNING: OOV dictionary entry (ရာသီဥတု - weatherworn)
WARNING: OOV dictionary entry (အပိုင်းပိုင်း - sectionally)
WARNING: OOV dictionary entry (အဆင်မပြေ - wady)
WARNING: OOV dictionary entry (တဝဲလည်လည် - lingeringly)
WARNING: OOV dictionary entry (အနီးဆုံး - sternmost)
WARNING: OOV dictionary entry (ခေါင်းစွပ် - headcase)
WARNING: OOV dictionary entry (ပေါင်းစပ် - collimate)
WARNING: OOV dictionary entry (မြောက်ဘက် - northing)
WARNING: OOV dictionary entry (အနောက်တိုင်း - wester)
WARNING: OOV dictionary entry (အနောက်ဘက် - hindquarter)
WARNING: OOV dictionary entry (ဖရန့် - francium)
WARNING: OOV dictionary entry (သန်းကြွယ်သူဌေး - millionairess)
WARNING: OOV dictionary entry (ဝါဒ - demist)
WARNING: OOV dictionary entry (အဆင့် - leveller)
WARNING: OOV dictionary entry (လူသတ်မှု - murderousness)
WARNING: OOV dictionary entry (မူဆလင် - musjid)
WARNING: OOV dictionary entry (ရေမှုတ် - spathe)
WARNING: OOV dictionary entry (ကောင်းစွာ - wally)
WARNING: OOV dictionary entry (တွန်းကန် - propellent)
WARNING: OOV dictionary entry (ကောလိပ် - collegian)
WARNING: OOV dictionary entry (ရည်ရွယ်ချက် - objectiveness)
WARNING: OOV dictionary entry (မိုးကြိုးပစ် - thunderhead)
WARNING: OOV dictionary entry (ဝက်သား - porker)
WARNING: OOV dictionary entry (အဟန့်အတား - determent)
WARNING: OOV dictionary entry (အုတ်ခဲ - briquette)
WARNING: OOV dictionary entry (လူငယ် - juvenilia)
WARNING: OOV dictionary entry (ရေစုပ်စက် - drainer)
WARNING: OOV dictionary entry (ဗိုက်နာ - stomache)
WARNING: OOV dictionary entry (ဒယ်အိုး - reddle)
WARNING: OOV dictionary entry (အလွန်အကျွံ - overexpand)
WARNING: OOV dictionary entry (သင်္ဘောသား - shipman)
WARNING: OOV dictionary entry (မီးကျောက် - firestone)
WARNING: OOV dictionary entry (ချီးကျူး - felicitate)
WARNING: OOV dictionary entry (စာရေး - clerkly)
WARNING: OOV dictionary entry (ဘီယာ - beery)
WARNING: OOV dictionary entry (လည်စည်း - necklet)
WARNING: OOV dictionary entry (နိဂုံးချုပ် - finical)
WARNING: OOV dictionary entry (လှော်ခတ် - unsaddle)
WARNING: OOV dictionary entry (ဆေးပညာ - medico)
WARNING: OOV dictionary entry (လူမျိုးစွဲ - nepotist)
WARNING: OOV dictionary entry (သုံးဆ - threepence)
WARNING: OOV dictionary entry (မြေသား - groundwell)
WARNING: OOV dictionary entry (လက် - handwoven)
WARNING: OOV dictionary entry (ပုရစ် - crick)
WARNING: OOV dictionary entry (ဂျင်မီ - jimmy)
WARNING: OOV dictionary entry (ကျေးလက်တောရွာ - rusticate)
WARNING: OOV dictionary entry (မေတ္တာ - metta)
WARNING: OOV dictionary entry (ဂျာနယ်လစ် - journalese)
WARNING: OOV dictionary entry (အချုပ်ခန်း - cellarage)
WARNING: OOV dictionary entry (အိုး - oof)
WARNING: OOV dictionary entry (မှီခို - impendent)
WARNING: OOV dictionary entry (စွန့်စားခန်း - adventurously)
WARNING: OOV dictionary entry (အသည်းနှလုံး - hardhearted)
WARNING: OOV dictionary entry (သမဂ္ဂ - unionise)
WARNING: OOV dictionary entry (ညှိနှိုင်းမှု - incoordination)
WARNING: OOV dictionary entry (အလျှော့မပေး - unyieldingly)
WARNING: OOV dictionary entry (လူသတ်သမား - maleficent)
WARNING: OOV dictionary entry (သင်္ဘောသား - seamer)
WARNING: OOV dictionary entry (ရန်ဖြစ် - quarreller)
WARNING: OOV dictionary entry (စုဝေး - convolve)
WARNING: OOV dictionary entry (သစ်ပင်ပန်းမန် - florae)
WARNING: OOV dictionary entry (သစ်ကြားသီး - nutmeat)
WARNING: OOV dictionary entry (မှုန်ဝါးဝါး - haziness)
WARNING: OOV dictionary entry (အတင်းအဖျင်း - gossipmonger)
WARNING: OOV dictionary entry (ညဝတ် - nightwear)
WARNING: OOV dictionary entry (သွက်သွက်လက်လက် - fugly)
WARNING: OOV dictionary entry (နိုဘယ်လ်ဆု - nobelium)
WARNING: OOV dictionary entry (ဒဏ်ခတ် - strick)
WARNING: OOV dictionary entry (စစ်အင်အား - militarise)
WARNING: OOV dictionary entry (တရားဝင် - officialese)
WARNING: OOV dictionary entry (ကြားဖြတ် - interstice)
WARNING: OOV dictionary entry (အလံတိုင် - flagellate)
WARNING: OOV dictionary entry (ဂိမ်း - gam)
WARNING: OOV dictionary entry (ရိုက် - whump)
WARNING: OOV dictionary entry (အနာ - ululation)
WARNING: OOV dictionary entry (မလှုပ်မယှက် - motionlessly)
WARNING: OOV dictionary entry (ပိုဒ် - stanzaic)
WARNING: OOV dictionary entry (ပါရီ - paretic)
WARNING: OOV dictionary entry (လက်ထောက် - bailor)
WARNING: OOV dictionary entry (အလှဆင် - ornamentally)
WARNING: OOV dictionary entry (လက်ကောက်ဝတ် - wristlock)
WARNING: OOV dictionary entry (ရာသီဥတု - weatherize)
WARNING: OOV dictionary entry (ကမ်းခြေ - coastward)
WARNING: OOV dictionary entry (တာဝါတိုင် - weir)
WARNING: OOV dictionary entry (နေထိုင်သူ - habitant)
WARNING: OOV dictionary entry (လောင်းကစား - gabble)
WARNING: OOV dictionary entry (ထိပ်တန်း - supernal)
WARNING: OOV dictionary entry (အရေးအသား - mottle)
WARNING: OOV dictionary entry (ဆင်ဆာ - censorial)
WARNING: OOV dictionary entry (သင်းခွေချပ် - pangolin)
WARNING: OOV dictionary entry (ရေအောက် - submerse)
WARNING: OOV dictionary entry (အလုပ် - jobby)
WARNING: OOV dictionary entry (အဘိုးအဘွား - grandpapa)
WARNING: OOV dictionary entry (ငါးဖမ်းသမား - fishwife)
WARNING: OOV dictionary entry (အေးအေးဆေးဆေး - relaxedly)
WARNING: OOV dictionary entry (ဒိုင်ခွက် - dicer)
WARNING: OOV dictionary entry (ကုန်စိမ်း - greengrocery)
WARNING: OOV dictionary entry (အစာ - feedstuff)
WARNING: OOV dictionary entry (သော့ခလောက် - picklock)
WARNING: OOV dictionary entry (အဇာတသတ် - patricide)
WARNING: OOV dictionary entry (အခမဲ့ - freeby)
WARNING: OOV dictionary entry (နောက်ကြောင်းပြန် - retroact)
WARNING: OOV dictionary entry (ဇာတိ - natality)
WARNING: OOV dictionary entry (လမ်းမကြီး - mainroad)
WARNING: OOV dictionary entry (တူးမြောင်း - canalize)
WARNING: OOV dictionary entry (ဂုဏ်သတင်း - prestissimo)
WARNING: OOV dictionary entry (နှင်တံ - whipstitch)
WARNING: OOV dictionary entry (ဆောင်းပါး - tonsorial)
WARNING: OOV dictionary entry (ကစားပွဲ - playgame)
WARNING: OOV dictionary entry (ဘေးတိုက် - sideward)
WARNING: OOV dictionary entry (အာကာသယာဉ် - aerosphere)
WARNING: OOV dictionary entry (ရှေးယခင် - antecede)
WARNING: OOV dictionary entry (ကျားမ - gendermerie)
WARNING: OOV dictionary entry (ဘာဂါ - burgle)
WARNING: OOV dictionary entry (မကျေမနပ် - indolently)
WARNING: OOV dictionary entry (လယ်သမား - fieldsman)
WARNING: OOV dictionary entry (စွယ် - tuskless)
WARNING: OOV dictionary entry (အီစတာ - easterner)
WARNING: OOV dictionary entry (တေးဂီတသံ - melodically)
WARNING: OOV dictionary entry (တင်ပါး - kecks)
WARNING: OOV dictionary entry (ဆေးစာ - prescript)
WARNING: OOV dictionary entry (တစ်ချိန်ချိန် - somewhen)
WARNING: OOV dictionary entry (အပြုအမူ - manneristic)
WARNING: OOV dictionary entry (ပေါင်းစည်း - agglutinate)
WARNING: OOV dictionary entry (လက်ဖက်ရည်ဆိုင် - teacake)
WARNING: OOV dictionary entry (ရင်ဘတ် - chesty)
WARNING: OOV dictionary entry (ပြင်းပြင်းထန်ထန် - vexingly)
WARNING: OOV dictionary entry (ကဗျာဆရာ - poetaster)
WARNING: OOV dictionary entry (တည်ဆောက်ရေး - outbuilding)
WARNING: OOV dictionary entry (အလင်းရောင် - illuminance)
WARNING: OOV dictionary entry (ကြောင် - cunny)
WARNING: OOV dictionary entry (ကြောက်စရာ - dreadfulness)
WARNING: OOV dictionary entry (ဇွန်း - spoony)
WARNING: OOV dictionary entry (သင်ရိုးညွှန်းတမ်း - curricle)
WARNING: OOV dictionary entry (ပြင်းပြင်းထန်ထန် - tussive)
WARNING: OOV dictionary entry (မိုးခြိမ်းသံ - thunderclap)
WARNING: OOV dictionary entry (စိုက်ပျိုးရေး - apiculture)
WARNING: OOV dictionary entry (နောက်ကျော - backsaw)
WARNING: OOV dictionary entry (တွန့်လိမ် - wriggler)
WARNING: OOV dictionary entry (မီးရထားတွဲ - waggon)
WARNING: OOV dictionary entry (တားမြစ်ချက် - tabour)
WARNING: OOV dictionary entry (သီးသန့် - reservedly)
WARNING: OOV dictionary entry (ကုန်လှောင်ရုံ - wareroom)
WARNING: OOV dictionary entry (စကားပြော - talky)
WARNING: OOV dictionary entry (အထိမ်းအမှတ် - memorialise)
WARNING: OOV dictionary entry (တော - queerness)
WARNING: OOV dictionary entry (ပျော်ရွှင်မှု - blissfulness)
WARNING: OOV dictionary entry (ဆန္ဒ - wishfulness)
WARNING: OOV dictionary entry (ကြွက်သား - muscularly)
WARNING: OOV dictionary entry (ရထား - carroty)
WARNING: OOV dictionary entry (ကျောက်ခဲ - whetstone)
WARNING: OOV dictionary entry (လေယာဉ် - aerodyne)
WARNING: OOV dictionary entry (ဂိုးသမား - goalmouth)
WARNING: OOV dictionary entry (အဝတ်လျှော်စက် - rasher)
WARNING: OOV dictionary entry (ဖျင်း - chaffer)
WARNING: OOV dictionary entry (ပညာရှိ - wiseman)
WARNING: OOV dictionary entry (မြန်နှုန်း - speeder)
WARNING: OOV dictionary entry (အင်တာနက် - inearth)
WARNING: OOV dictionary entry (ဖန်ခွက် - glasswork)
WARNING: OOV dictionary entry (ကေဒါ - cadge)
WARNING: OOV dictionary entry (ပြောင် - baldy)
WARNING: OOV dictionary entry (ပညာ - sapience)
WARNING: OOV dictionary entry (ဆေးဒန်း - orpiment)
WARNING: OOV dictionary entry (အစာအိမ် - stomachic)
WARNING: OOV dictionary entry (ရှားပါး - rarebit)
WARNING: OOV dictionary entry (ရောင်းသူ - repeller)
WARNING: OOV dictionary entry (အစေခံ - manservant)
WARNING: OOV dictionary entry (နွားသိုး - cowman)
WARNING: OOV dictionary entry (ဝတ်ဆံ - stamen)
WARNING: OOV dictionary entry (အပယ်ခံ - outcaste)
WARNING: OOV dictionary entry (မီးစက် - wickerwork)
WARNING: OOV dictionary entry (ဝိုးတိုးဝါးတား - hazily)
WARNING: OOV dictionary entry (လူသစ် - rooky)
WARNING: OOV dictionary entry (ဟာဂျီ - haji)
WARNING: OOV dictionary entry (မီလီမီတာ - millilitre)
WARNING: OOV dictionary entry (ငွေ့ - sapor)
WARNING: OOV dictionary entry (ပေါင်းစပ် - confabulate)
WARNING: OOV dictionary entry (ဖြတ်ထုတ် - cutup)
WARNING: OOV dictionary entry (ပတ်လည် - enwrap)
WARNING: OOV dictionary entry (အမှာစကား - gisting)
WARNING: OOV dictionary entry (အစေခံ - subserviently)
WARNING: OOV dictionary entry (လက်အောက်ခံ - subsocial)
WARNING: OOV dictionary entry (ဟုံ - cloy)
WARNING: OOV dictionary entry (လက်သုတ်ပုဝါ - napery)
WARNING: OOV dictionary entry (ထပ်ခါတလဲလဲ - reiterative)
WARNING: OOV dictionary entry (ပိုက်ဆံအိတ် - moneybag)
WARNING: OOV dictionary entry (ကြိုး - ropey)
WARNING: OOV dictionary entry (ကုက္ကုစ္စ - miserliness)
WARNING: OOV dictionary entry (လက်သည်း - nailer)
WARNING: OOV dictionary entry (အမှိုက်ပုံး - litterbug)
WARNING: OOV dictionary entry (ပေါ်ပေါက် - occident)
WARNING: OOV dictionary entry (မက်ထရစ် - metrication)
WARNING: OOV dictionary entry (ပူးပေါင်း - concertize)
WARNING: OOV dictionary entry (ပန်းရန် - plasterer)
WARNING: OOV dictionary entry (မိုးသံ - thuddingly)
WARNING: OOV dictionary entry (အလယ်အလတ် - midrib)
WARNING: OOV dictionary entry (ကစ် - kicky)
WARNING: OOV dictionary entry (အပြန်အလှန် - mutualize)
WARNING: OOV dictionary entry (ဓာတ်ဖို - alchemize)
WARNING: OOV dictionary entry (ရေချိုးကန် - washbasin)
WARNING: OOV dictionary entry (ပြိုင်ပွဲ - raceme)
WARNING: OOV dictionary entry (ထိထိမိမိ - mordantly)
WARNING: OOV dictionary entry (မည်သို့ပင်ဖြစ်စေ - anywise)
WARNING: OOV dictionary entry (ကြက်သမား - poultryman)
WARNING: OOV dictionary entry (မိုးကာ - rainwear)
WARNING: OOV dictionary entry (နှင်းပေါက် - snowdrop)
WARNING: OOV dictionary entry (ဂျာမန် - merman)
WARNING: OOV dictionary entry (အသာတကြည် - nebulously)
WARNING: OOV dictionary entry (ဝါတော် - vasa)
WARNING: OOV dictionary entry (အခက်အခဲ - confliction)
WARNING: OOV dictionary entry (နန်းတော် - vicennial)
WARNING: OOV dictionary entry (ချော့မော့ - sedately)
WARNING: OOV dictionary entry (ဘိလပ်မြေ - cementum)
WARNING: OOV dictionary entry (တူရိယာ - percuss)
WARNING: OOV dictionary entry (သဘောထား - tendance)
WARNING: OOV dictionary entry (ရမယ် - gotta)
WARNING: OOV dictionary entry (အလုပ်ရှင် - workwoman)
WARNING: OOV dictionary entry (ညည်းတွားသံ - whin)
WARNING: OOV dictionary entry (ဒေါသတကြီး - resentfully)
WARNING: OOV dictionary entry (အရှုပ်တော်ပုံ - scandalmonger)
WARNING: OOV dictionary entry (ဖျန်ဖြေ - mediative)
WARNING: OOV dictionary entry (ပန်းကုံး - wreathe)
WARNING: OOV dictionary entry (လက်ကောက် - bangle)
WARNING: OOV dictionary entry (အာဇာနည် - martyrize)
WARNING: OOV dictionary entry (သယ်ဆောင် - carryall)
WARNING: OOV dictionary entry (ညှပ်ဖိနပ် - flipflop)
WARNING: OOV dictionary entry (သေရည် - intoxicate)
WARNING: OOV dictionary entry (သားအိမ်ခေါင်း - cervine)
WARNING: OOV dictionary entry (သစ်သား - woodenly)
WARNING: OOV dictionary entry (ကြက်မောက် - shuttlecock)
WARNING: OOV dictionary entry (ခန္ဓာဗေဒ - anatomize)
WARNING: OOV dictionary entry (ကြမ်းပြင် - granger)
WARNING: OOV dictionary entry (ဝိုင် - wahine)
WARNING: OOV dictionary entry (အထွတ်အထိပ် - pinnace)
WARNING: OOV dictionary entry (ရှက်တယ် - shyster)
WARNING: OOV dictionary entry (ကြာပွတ် - whipper)
WARNING: OOV dictionary entry (အစောင့် - guardsman)
WARNING: OOV dictionary entry (တစ်နှစ် - anear)
WARNING: OOV dictionary entry (ဘေးတိုက် - sidepiece)
WARNING: OOV dictionary entry (ဝုန်းဒိုင်းကြဲ - boisterously)
WARNING: OOV dictionary entry (စုတ်တံ - stipe)
WARNING: OOV dictionary entry (မလှုပ်မယှက် - waggishly)
WARNING: OOV dictionary entry (ဝံသာနု - wain)
WARNING: OOV dictionary entry (ဖယောင်းတိုင် - candlewick)
WARNING: OOV dictionary entry (အာကာသယာဉ်မှူး - spacewoman)
WARNING: OOV dictionary entry (မျက်နှာဖြူ - whiteface)
WARNING: OOV dictionary entry (လက်ချောင်း - handspring)
WARNING: OOV dictionary entry (ကျောင်းနေဖက် - schoolmarmish)
WARNING: OOV dictionary entry (မြန်မာ - quicklime)
WARNING: OOV dictionary entry (အလုပ် - outwork)
WARNING: OOV dictionary entry (မျိုးစိတ် - inbreed)
WARNING: OOV dictionary entry (ရေမွှေး - perfuming)
WARNING: OOV dictionary entry (နေ့လည်စာ - luncheonette)
WARNING: OOV dictionary entry (အိပ်ရာ - bedhead)
WARNING: OOV dictionary entry (လုံခြုံမှု - securement)
WARNING: OOV dictionary entry (အောင်နိုင်သူ - victualer)
WARNING: OOV dictionary entry (အမှိုက်ပုံ - dreg)
WARNING: OOV dictionary entry (ဓမ္မ - ministerially)
WARNING: OOV dictionary entry (ခြေကျင်း - anklebone)
WARNING: OOV dictionary entry (ကုန်းမြင့် - highlander)
WARNING: OOV dictionary entry (ကုန်ကျစရိတ် - costar)
WARNING: OOV dictionary entry (နားစည် - eardrop)
WARNING: OOV dictionary entry (သုံးသူ - treater)
WARNING: OOV dictionary entry (ပိုးကောင် - bedbug)
WARNING: OOV dictionary entry (ဂရမ် - gramme)
WARNING: OOV dictionary entry (အခန်းကျယ် - roomer)
WARNING: OOV dictionary entry (ခရီး - itinerancy)
WARNING: OOV dictionary entry (အဝိုင်း - roundel)
WARNING: OOV dictionary entry (အခွင့်အလမ်း - opponency)
WARNING: OOV dictionary entry (ဟန်နာ - hahnium)
WARNING: OOV dictionary entry (ပါကေး - parquetry)
WARNING: OOV dictionary entry (မျက်တောင် - glim)
WARNING: OOV dictionary entry (စေတနာရှင် - voluntaryist)
WARNING: OOV dictionary entry (သိုးမွေး - woolgrowing)
WARNING: OOV dictionary entry (မီလီမီတာ - millesimal)
WARNING: OOV dictionary entry (အပင် - plantigrade)
WARNING: OOV dictionary entry (တိုးတက်မှု - spence)
WARNING: OOV dictionary entry (လွတ်လွတ်လပ်လပ် - unblushingly)
WARNING: OOV dictionary entry (ချယ်ရီ - charlady)
WARNING: OOV dictionary entry (ဆံပင်ညှပ် - haberdashery)
WARNING: OOV dictionary entry (စကားပြန် - backsword)
WARNING: OOV dictionary entry (တံတွေး - snit)
WARNING: OOV dictionary entry (တန်းတူ - rorqual)
WARNING: OOV dictionary entry (သစ်တော - afforest)
WARNING: OOV dictionary entry (မျက်မမြင် - blindside)
WARNING: OOV dictionary entry (မြေပဲ - earthnut)
WARNING: OOV dictionary entry (သွေးလွန်တုပ်ကွေး - extravasate)
WARNING: OOV dictionary entry (စိတ်ကူးယဉ်သမား - fictionist)
WARNING: OOV dictionary entry (နွေရာသီ - summerset)
WARNING: OOV dictionary entry (ဧည့်သည် - visitant)
WARNING: OOV dictionary entry (လေယာဉ်ပျံ - enplane)
WARNING: OOV dictionary entry (အသံထွက် - intonate)
WARNING: OOV dictionary entry (ရောင်းသူ - vendace)
WARNING: OOV dictionary entry (ကြိုးမျှင် - strandline)
WARNING: OOV dictionary entry (အပြန်အလှန် - mutationally)
WARNING: OOV dictionary entry (ဝတ္ထုတို - novelette)
WARNING: OOV dictionary entry (အဆင့်အတန်း - regality)
WARNING: OOV dictionary entry (ခေါ် - sumach)
WARNING: OOV dictionary entry (ရုန်းရင်းဆန်ခတ် - wamble)
WARNING: OOV dictionary entry (ကိုယ်တွေ့ - unhand)
WARNING: OOV dictionary entry (အလုပ်သင် - internee)
WARNING: OOV dictionary entry (ကြည့်ရှု - spectate)
WARNING: OOV dictionary entry (တံခါး - gateau)
WARNING: OOV dictionary entry (မြောက်ဘက် - northwardly)
WARNING: OOV dictionary entry (အဆက်မပြတ် - continuant)
WARNING: OOV dictionary entry (အလွန်အကျွံ - overset)
WARNING: OOV dictionary entry (အရှိန်အဟုန် - momentariness)
WARNING: OOV dictionary entry (သွေးလွန်တုပ်ကွေး - haemophiliac)
WARNING: OOV dictionary entry (လည်စည်း - manege)
WARNING: OOV dictionary entry (အီလက်ထရောနစ် - electone)
WARNING: OOV dictionary entry (အပြုံး - smirch)
WARNING: OOV dictionary entry (သမားရိုးကျ - conventionalise)
WARNING: OOV dictionary entry (အလယ်အလတ် - middleweight)
WARNING: OOV dictionary entry (ဘုရားရှိခိုးကျောင်း - churchwoman)
WARNING: OOV dictionary entry (ပန်းပုဆရာ - sculptress)
WARNING: OOV dictionary entry (စစ်မှုထမ်း - enlistee)
WARNING: OOV dictionary entry (လုံခြုံမှု - safeness)
WARNING: OOV dictionary entry (ရုပ်ပျက်ဆင်းပျက် - disfiguration)
WARNING: OOV dictionary entry (ကျောင်းနေဖက် - schoolfellow)
WARNING: OOV dictionary entry (ကျောက်တောင် - cliffy)
WARNING: OOV dictionary entry (ညနေ - yesternight)
WARNING: OOV dictionary entry (တော်မီ - tommy)
WARNING: OOV dictionary entry (အဆီပြန် - fatback)
WARNING: OOV dictionary entry (ဘုရားရေ - golosh)
WARNING: OOV dictionary entry (အလယ်ခေတ် - medievally)
WARNING: OOV dictionary entry (ဟဲလို - welch)
WARNING: OOV dictionary entry (အသေအချာ - martially)
WARNING: OOV dictionary entry (အိမ်နောက်ဖေး - backstairs)
WARNING: OOV dictionary entry (နောက်ကျော - thill)
WARNING: OOV dictionary entry (အာကာသယာဉ်မှူး - aeronaut)
WARNING: OOV dictionary entry (မက်ထရစ် - metricate)
WARNING: OOV dictionary entry (သစ်သား - woodpile)
WARNING: OOV dictionary entry (ကြီးကြီးမားမား - bulgy)
WARNING: OOV dictionary entry (ကျောက်မျက်ရတနာ - gemination)
WARNING: OOV dictionary entry (တန်ပြန် - counterpane)
WARNING: OOV dictionary entry (အပြင်အဆင် - outface)
WARNING: OOV dictionary entry (အရသာ - savoriness)
WARNING: OOV dictionary entry (တောင်ပံ - wingover)
WARNING: OOV dictionary entry (အမြန်နှုန်း - quickset)
WARNING: OOV dictionary entry (လူမှုဆက်ဆံရေး - sociality)
WARNING: OOV dictionary entry (ပေါရာဏ - obsoleteness)
WARNING: OOV dictionary entry (တီးတိုး - whispery)
WARNING: OOV dictionary entry (လက်စွပ် - armlet)
WARNING: OOV dictionary entry (ပုဆိုး - sateen)
WARNING: OOV dictionary entry (ကျွဲ - moated)
WARNING: OOV dictionary entry (လူဆိုး - villous)
WARNING: OOV dictionary entry (သုံးဆ - thievish)
WARNING: OOV dictionary entry (ဟန်နီ - hinny)
WARNING: OOV dictionary entry (လူမှုအဖွဲ့အစည်း - socage)
WARNING: OOV dictionary entry (ထိပ်တန်း - topmast)
WARNING: OOV dictionary entry (ကျောထောက်နောက်ခံ - hunchbacked)
WARNING: OOV dictionary entry (သတင်းအချက်အလက် - informativeness)
WARNING: OOV dictionary entry (ပြင်သစ် - frenchy)
WARNING: OOV dictionary entry (သကြားသီး - sugarplum)
WARNING: OOV dictionary entry (မလုံမခြုံ - insobriety)
WARNING: OOV dictionary entry (ပိုးတုံးလုံး - pupa)
WARNING: OOV dictionary entry (မီးသတ်သမား - fireguard)
WARNING: OOV dictionary entry (သွားရေးလာရေး - commutate)
WARNING: OOV dictionary entry (ထွက်ပြေး - runabout)
WARNING: OOV dictionary entry (အံ့ဖွယ် - miraculousness)
WARNING: OOV dictionary entry (အားလပ်ရက် - vacationist)
WARNING: OOV dictionary entry (နှုန်းထား - rateable)
WARNING: OOV dictionary entry (ပိုးစုန်းကြူး - mayfly)
WARNING: OOV dictionary entry (အောင်မြင်မှု - acclivity)
WARNING: OOV dictionary entry (သင်္ဘောသား - marrier)
WARNING: OOV dictionary entry (ဆွဲကြိုး - pend)
WARNING: OOV dictionary entry (ကွာတားဖိုင်နယ် - quarterfinalist)
WARNING: OOV dictionary entry (စုစုပေါင်း - totalize)
WARNING: OOV dictionary entry (လိမ့်မည် - gonna)
WARNING: OOV dictionary entry (ဥပမာ - egad)
WARNING: OOV dictionary entry (လှုပ်ရှားမှု - motional)
WARNING: OOV dictionary entry (မိုးကာအင်္ကျီ - mackintosh)
WARNING: OOV dictionary entry (စွယ်တော် - stupe)
WARNING: OOV dictionary entry (ကတိ - promisee)
WARNING: OOV dictionary entry (လက်သမား - freemasonary)
WARNING: OOV dictionary entry (ပေါင်ချိန် - poundage)
WARNING: OOV dictionary entry (ရေအား - waterpower)
WARNING: OOV dictionary entry (စတိုင် - stymy)
WARNING: OOV dictionary entry (မူးယစ်ဆေး - druggie)
WARNING: OOV dictionary entry (ကြော်ငြာ - advertent)
WARNING: OOV dictionary entry (ခရမ်းနုရောင် - wisteria)
WARNING: OOV dictionary entry (စိတ်ကူးယဉ် - fict)
WARNING: OOV dictionary entry (သရက်သီး - mangosteen)
WARNING: OOV dictionary entry (အမျိုးမျိုး - varietally)
WARNING: OOV dictionary entry (ဘီလီ - billie)
WARNING: OOV dictionary entry (ဖရိုဖရဲ - shamble)
WARNING: OOV dictionary entry (သင်ရိုးညွှန်းတမ်း - syllabary)
WARNING: OOV dictionary entry (အရိုးစု - skeletonize)
WARNING: OOV dictionary entry (မျက်မှန် - eyeshade)
WARNING: OOV dictionary entry (ပါးစပ် - mouthy)
WARNING: OOV dictionary entry (အင်ပါယာ - empyrean)
WARNING: OOV dictionary entry (တေးသံ - sonance)
WARNING: OOV dictionary entry (ကြင်နာမှု - courteousness)
WARNING: OOV dictionary entry (သန်း - jillion)
WARNING: OOV dictionary entry (တံခွန် - moorage)
WARNING: OOV dictionary entry (နွယ်ပင် - bindweed)
WARNING: OOV dictionary entry (ပြန်ပေး - restitute)
WARNING: OOV dictionary entry (ရှောင်ရှား - evanesce)
WARNING: OOV dictionary entry (ပျော်ရွှင်စရာ - merrythought)
WARNING: OOV dictionary entry (မော်နီတာ - monitorship)
WARNING: OOV dictionary entry (လောင်းလှေ - stakeboat)
WARNING: OOV dictionary entry (အရောင်တင် - colorant)
WARNING: OOV dictionary entry (အိမ်မြှောင် - oarlock)
WARNING: OOV dictionary entry (စီမံခန့်ခွဲ - menage)
WARNING: OOV dictionary entry (မောင်းမ - unman)
WARNING: OOV dictionary entry (ပျော့ဆေး - milden)
WARNING: OOV dictionary entry (အနီကတ် - redcap)
WARNING: OOV dictionary entry (ကီလိုဂရမ် - kilogramme)
WARNING: OOV dictionary entry (ဘေးစောင်း - sideslip)
WARNING: OOV dictionary entry (အပေးအယူ - embrocation)
WARNING: OOV dictionary entry (လယ်ယာ - farness)
WARNING: OOV dictionary entry (အိုး - uhf)
WARNING: OOV dictionary entry (ကျောင်းသား - pupillage)
WARNING: OOV dictionary entry (စီးကရက် - cigaret)
WARNING: OOV dictionary entry (ပွဲတော် - aestival)
WARNING: OOV dictionary entry (စည်းမျဉ်းစည်းကမ်း - regulus)
WARNING: OOV dictionary entry (စကား - headword)
WARNING: OOV dictionary entry (မီလီမီတာ - milliampere)
WARNING: OOV dictionary entry (အမွေအနှစ် - heirdom)
WARNING: OOV dictionary entry (ပိုးစာ - mullock)
WARNING: OOV dictionary entry (လက်သမား - pryer)
WARNING: OOV dictionary entry (တောင်ပိုင်းသား - southlander)
WARNING: OOV dictionary entry (အမွှေးတိုင် - joss)
WARNING: OOV dictionary entry (ကိုးကား - quoter)
WARNING: OOV dictionary entry (ဆူပူ - braw)
WARNING: OOV dictionary entry (သဘာဝတရား - naturism)
WARNING: OOV dictionary entry (ရေသူမ - mermen)
WARNING: OOV dictionary entry (အောင်နိုင်သူ - vanquisher)
WARNING: OOV dictionary entry (ခြေကျင်း - footbath)
WARNING: OOV dictionary entry (စိုးရိမ်စိတ် - apprehensiveness)
WARNING: OOV dictionary entry (ဆံပင်ရှည် - longhair)
WARNING: OOV dictionary entry (နုတ် - subtracter)
WARNING: OOV dictionary entry (သစ်သားအိမ် - woodhouse)
WARNING: OOV dictionary entry (နောက်ပိုင်း - afters)
WARNING: OOV dictionary entry (သေနတ်သံ - gunlock)
WARNING: OOV dictionary entry (စင်တီမီတာ - centesimal)
WARNING: OOV dictionary entry (ပုစဉ်း - stonefly)
WARNING: OOV dictionary entry (အညှာ - stalky)
WARNING: OOV dictionary entry (လက်ပတ် - wristlet)
WARNING: OOV dictionary entry (အလွန်အကျွံ - overact)
WARNING: OOV dictionary entry (ကျောက်ဆူး - anchoress)
WARNING: OOV dictionary entry (မဟုတ်ပါ - nonsuch)
WARNING: OOV dictionary entry (အလုံးစုံ - overarch)
WARNING: OOV dictionary entry (ဒေါသတကြီး - irritatedly)
WARNING: OOV dictionary entry (သရုပ်ဖော် - scenarist)
WARNING: OOV dictionary entry (စားပွဲခုံ - deskill)
WARNING: OOV dictionary entry (ခါးစည်း - waistcloth)
WARNING: OOV dictionary entry (လှံတံ - spewer)
WARNING: OOV dictionary entry (ကျောက်တုံး - stonechat)
WARNING: OOV dictionary entry (ဖြည့်စွက် - suppurate)
WARNING: OOV dictionary entry (သံယောဇဉ် - entwine)
WARNING: OOV dictionary entry (အာမခံ - ensilage)
WARNING: OOV dictionary entry (ရေချိုးခန်း - bathysphere)
WARNING: OOV dictionary entry (မင်းဆက် - dynast)
WARNING: OOV dictionary entry (တိုးဂိတ် - tollhouse)
WARNING: OOV dictionary entry (ပန်းခြံ - parky)
WARNING: OOV dictionary entry (ခက်ခက်ခဲခဲ - heddle)
WARNING: OOV dictionary entry (အကွာအဝေး - outdistance)
WARNING: OOV dictionary entry (နေထိုင်မှု - habiliment)
WARNING: OOV dictionary entry (အညှော် - pungency)
WARNING: OOV dictionary entry (သေခြင်းတရား - deadliness)
WARNING: OOV dictionary entry (အိပ်ယာခင်း - bedsitter)
WARNING: OOV dictionary entry (အစုလိုက် - bunchy)
WARNING: OOV dictionary entry (ဈေးဝယ် - pilchard)
WARNING: OOV dictionary entry (တူးမြောင်း - canalise)
WARNING: OOV dictionary entry (ပေါင်းပင် - weediness)
WARNING: OOV dictionary entry (သတင်းမှား - misinformer)
WARNING: OOV dictionary entry (ဓားရှည် - stabile)
WARNING: OOV dictionary entry (ရွရွ - dashingly)
WARNING: OOV dictionary entry (အဖျက်သမား - vesicant)
WARNING: OOV dictionary entry (ကွဲပြားမှု - viceregency)
WARNING: OOV dictionary entry (စောင်း - slantwise)
WARNING: OOV dictionary entry (ရောဂါဘယ - morbidness)
WARNING: OOV dictionary entry (တီဘီ - tubercule)
WARNING: OOV dictionary entry (အကူအညီ - helot)
WARNING: OOV dictionary entry (ကျွမ်းကျင်သူ - aperient)
WARNING: OOV dictionary entry (ကျွဲ - buffaloed)
WARNING: OOV dictionary entry (ကြွေ - enamor)
WARNING: OOV dictionary entry (စိတ်ဝင်စားမှု - interestedness)
WARNING: OOV dictionary entry (ပဋိညာဉ် - coven)
WARNING: OOV dictionary entry (မျက်နှာဖုံး - masque)
WARNING: OOV dictionary entry (ပန်းထိမ် - ironsmith)
WARNING: OOV dictionary entry (အစာအိမ်နာ - ulcerate)
WARNING: OOV dictionary entry (စင်တီမီတာ - centiliter)
WARNING: OOV dictionary entry (ဗီတာမင် - vitamine)
WARNING: OOV dictionary entry (အဆင်မပြေ - malfeasant)
WARNING: OOV dictionary entry (သေနတ်သံ - outgun)
WARNING: OOV dictionary entry (ဟင်းချို - soupspoon)
WARNING: OOV dictionary entry (သရော်စာ - satirically)
WARNING: OOV dictionary entry (အရက်သမား - chocoholic)
WARNING: OOV dictionary entry (ပဲ့တင်သံ - echoic)
WARNING: OOV dictionary entry (ဟိတ်ကြီးဟန်ကြီး - pompously)
WARNING: OOV dictionary entry (အစားထိုး - substituent)
WARNING: OOV dictionary entry (စိတ်ပျက် - deject)
WARNING: OOV dictionary entry (အခန်း - compart)
WARNING: OOV dictionary entry (အားသွန်ခွန်စိုက် - strenously)
WARNING: OOV dictionary entry (ဆိုးဆေး - dyestuff)
WARNING: OOV dictionary entry (တေးသံရှင် - vocalizer)
WARNING: OOV dictionary entry (မဟာသီယာ - maharanee)
WARNING: OOV dictionary entry (မြို့တော်ခန်းမ - townhall)
WARNING: OOV dictionary entry (ပစ္စည်း - confiture)
WARNING: OOV dictionary entry (သမာဓိ - virtuousness)
WARNING: OOV dictionary entry (မတ်တပ်ရပ် - standee)
WARNING: OOV dictionary entry (ငွေထည် - maunder)
WARNING: OOV dictionary entry (ကြိုတင် - prelims)
WARNING: OOV dictionary entry (မျက်ဖြူ - sclera)
WARNING: OOV dictionary entry (ကျောပိုး - backcloth)
WARNING: OOV dictionary entry (ကောင်းစွာ - wellhouse)
WARNING: OOV dictionary entry (ငါး - fishiness)
WARNING: OOV dictionary entry (ချိုချိုသာသာ - mellifluously)
WARNING: OOV dictionary entry (ခေတ်ပြိုင် - extemporary)
WARNING: OOV dictionary entry (ပေါင်းပင် - weeder)
WARNING: OOV dictionary entry (စီဒီ - sinedie)
WARNING: OOV dictionary entry (လရောင် - moonbeam)
WARNING: OOV dictionary entry (ခေါ်သံ - catcall)
WARNING: OOV dictionary entry (အပွင့် - floury)
WARNING: OOV dictionary entry (လင်းယုန်ငှက် - eaglet)
WARNING: OOV dictionary entry (ကြီးကြီးမားမား - gride)
WARNING: OOV dictionary entry (အုတ်တံတိုင်း - curbstone)
WARNING: OOV dictionary entry (ဟောသည် - soothsay)
WARNING: OOV dictionary entry (အရူးမ - madwoman)
WARNING: OOV dictionary entry (တောက်ပ - scintillate)
WARNING: OOV dictionary entry (စာရွက်စာတမ်း - dosser)
WARNING: OOV dictionary entry (ချစ်စဖွယ် - amorously)
WARNING: OOV dictionary entry (တိတ်ဆိတ် - quietus)
WARNING: OOV dictionary entry (ဆွဲဆောင်မှု - emblazonment)
WARNING: OOV dictionary entry (ကျောင်းပိတ်ရက် - schoolmarm)
WARNING: OOV dictionary entry (ခေါင်းစီး - headstream)
WARNING: OOV dictionary entry (ခြံစောင့် - yardman)
WARNING: OOV dictionary entry (အံ့သြဖွယ် - musingly)
WARNING: OOV dictionary entry (အပုပ် - putridity)
WARNING: OOV dictionary entry (လက်စွပ် - handbasket)
WARNING: OOV dictionary entry (တရှုံ့ရှုံ့ - whiffle)
WARNING: OOV dictionary entry (ရေမှုတ် - waterthrush)
WARNING: OOV dictionary entry (အို - oho)
WARNING: OOV dictionary entry (ကန့်သတ် - limitedly)
WARNING: OOV dictionary entry (တရွေ့ရွေ့ - gushingly)

real	0m33.518s
user	0m39.542s
sys	0m5.253s
prepare folders and cp ... 
mkdir: cannot create directory ‘/media/ye/project2/exp/bilingual-induction/exp1/my-en/vecmap-output10/src_super’: File exists
mkdir: cannot create directory ‘/media/ye/project2/exp/bilingual-induction/exp1/my-en/vecmap-output10/trg_super’: File exists
run vecmap_launcher.py script ...
path:  /media/ye/project2/exp/bilingual-induction/exp1/my-en/vecmap-output10/src_super/word2vec_s100_mc2_w3.vec
path:  /media/ye/project2/exp/bilingual-induction/exp1/my-en/vecmap-output10/trg_super/word2vec_s100_mc2_w3.vec
EN:  /media/ye/project2/exp/bilingual-induction/exp1/my-en/vecmap-output10/src_super/word2vec_s100_mc2_w3.vec
WEL:  /media/ye/project2/exp/bilingual-induction/exp1/my-en/vecmap-output10/trg_super/word2vec_s100_mc2_w3.vec
=== CMD ===
python3 vecmap/map_embeddings.py --supervised /media/ye/project2/exp/bilingual-induction/exp1/my-en/word2vec-output10/train_dict.csv "/media/ye/project2/exp/bilingual-induction/exp1/my-en/vecmap-output10/src_super/word2vec_s100_mc2_w3.vec" "/media/ye/project2/exp/bilingual-induction/exp1/my-en/vecmap-output10/trg_super/word2vec_s100_mc2_w3.vec" "/media/ye/project2/exp/bilingual-induction/exp1/my-en/vecmap-output10/src_super/word2vec_s100_mc2_w3.vec_mapped.vec" "/media/ye/project2/exp/bilingual-induction/exp1/my-en/vecmap-output10/trg_super/word2vec_s100_mc2_w3.vec_mapped.vec"
WARNING: OOV dictionary entry (english - welsh)
WARNING: OOV dictionary entry (အရှုပ်တော်ပုံ - scandalmongering)
WARNING: OOV dictionary entry (မသန်စွမ်း - disenable)
WARNING: OOV dictionary entry (အလွန့်အလွန် - deviously)
WARNING: OOV dictionary entry (ခဲတံ - pennon)
WARNING: OOV dictionary entry (ကစားသူ - playgoer)
WARNING: OOV dictionary entry (အူဝဲ - howlingly)
WARNING: OOV dictionary entry (ဆိုးဆိုးရွားရွား - odiously)
WARNING: OOV dictionary entry (ပါးစပ် - mouthpart)
WARNING: OOV dictionary entry (ပါးရိုး - jag)
WARNING: OOV dictionary entry (သတ်မှတ်ချက် - stipel)
WARNING: OOV dictionary entry (နာရီ - stopclock)
WARNING: OOV dictionary entry (ဆောင်းရာသီ - winterize)
WARNING: OOV dictionary entry (ခိုးဝှက် - burglarize)
WARNING: OOV dictionary entry (လေးထောင့် - quadrivalent)
WARNING: OOV dictionary entry (အရောင်ဖျော့ - paleface)
WARNING: OOV dictionary entry (တော - wilde)
WARNING: OOV dictionary entry (ကျွမ်းကျင်မှု - professionalisation)
WARNING: OOV dictionary entry (သံပုရာသီး - limeade)
WARNING: OOV dictionary entry (ဓာတ်မှန် - heliograph)
WARNING: OOV dictionary entry (လက်လုပ် - handwrought)
WARNING: OOV dictionary entry (အိမ်သာ - toilette)
WARNING: OOV dictionary entry (နောက်ဆုံး - lattermost)
WARNING: OOV dictionary entry (သဲသဲမဲမဲ - unfrock)
WARNING: OOV dictionary entry (ကန်ပေါင် - embank)
WARNING: OOV dictionary entry (မီးတောက် - incandesce)
WARNING: OOV dictionary entry (ချစ်သူ - dearie)
WARNING: OOV dictionary entry (အလှူရှင် - donator)
WARNING: OOV dictionary entry (ကြောက်စရာ - scarer)
WARNING: OOV dictionary entry (ရွက်လှေ - yachtswoman)
WARNING: OOV dictionary entry (တွစ်တာ - twitcher)
WARNING: OOV dictionary entry (အနောက်တောင် - southwester)
WARNING: OOV dictionary entry (လူမိုက် - bumf)
WARNING: OOV dictionary entry (ချိပ် - lac)
WARNING: OOV dictionary entry (ပြပွဲ - exhibitive)
WARNING: OOV dictionary entry (လက်ခံသူ - acceptant)
WARNING: OOV dictionary entry (ချန်ပီယံ - champaign)
WARNING: OOV dictionary entry (ညီညွတ်ခြင်း - unconformity)
WARNING: OOV dictionary entry (ရာသီဥတု - weatherly)
WARNING: OOV dictionary entry (အရွက် - leafage)
WARNING: OOV dictionary entry (နွေရာသီ - summersault)
WARNING: OOV dictionary entry (ရွံ့ရှာ - vixenish)
WARNING: OOV dictionary entry (ပဲပုတ် - cowpea)
WARNING: OOV dictionary entry (ညစာ - truncheon)
WARNING: OOV dictionary entry (ဥရောပ - europium)
WARNING: OOV dictionary entry (အဖွားအို - grandmamma)
WARNING: OOV dictionary entry (ဇိုး - swiftlet)
WARNING: OOV dictionary entry (အထမ်းသမား - porterhouse)
WARNING: OOV dictionary entry (တရားခံ - ullage)
WARNING: OOV dictionary entry (တောင်ဘက် - southland)
WARNING: OOV dictionary entry (အကြောင်းအရင်း - causerie)
WARNING: OOV dictionary entry (အိမ်ထောင်ဖက် - matey)
WARNING: OOV dictionary entry (စားပွဲထိုး - deskman)
WARNING: OOV dictionary entry (အလေးချိန် - weigher)
WARNING: OOV dictionary entry (ပစ်ပေါက် - spick)
WARNING: OOV dictionary entry (သေနတ်သမား - rifleman)
WARNING: OOV dictionary entry (လက်အောက်ငယ်သား - subordinator)
WARNING: OOV dictionary entry (အဆုံး - endmost)
WARNING: OOV dictionary entry (ရူ - rouble)
WARNING: OOV dictionary entry (တရားဝင် - officinal)
WARNING: OOV dictionary entry (လေးပုံတစ်ပုံ - quartette)
WARNING: OOV dictionary entry (ကြမ်း - draff)
WARNING: OOV dictionary entry (ယာဉ်စီးခ - carfare)
WARNING: OOV dictionary entry (သရက်သီး - locknut)
WARNING: OOV dictionary entry (ရှားပါး - rarefy)
WARNING: OOV dictionary entry (ကျင့်ဝတ် - adduct)
WARNING: OOV dictionary entry (အတားအဆီး - obstructiveness)
WARNING: OOV dictionary entry (ပုံပျက်ပန်းပျက် - distortedly)
WARNING: OOV dictionary entry (ကော့ - cox)
WARNING: OOV dictionary entry (ထိထိရောက်ရောက် - effervesce)
WARNING: OOV dictionary entry (ကြောင်ကလေး - kittenish)
WARNING: OOV dictionary entry (အလုပ်အကိုင် - jobbery)
WARNING: OOV dictionary entry (ဟဲဟဲ - heehaw)
WARNING: OOV dictionary entry (ဝန်ဆောင်မှု - serviette)
WARNING: OOV dictionary entry (ခြင်းတောင်း - basketwork)
WARNING: OOV dictionary entry (ပြောင်းပြန် - revers)
WARNING: OOV dictionary entry (စကိတ်စီး - skedaddle)
WARNING: OOV dictionary entry (ဗေဒ - thanatology)
WARNING: OOV dictionary entry (ဘာဘီ - barbie)
WARNING: OOV dictionary entry (ဟောလိဝုဒ် - halliard)
WARNING: OOV dictionary entry (ပေးပါ - gimme)
WARNING: OOV dictionary entry (အိမ်မြှောင် - lurcher)
WARNING: OOV dictionary entry (မယ်ဒလင် - mandolinist)
WARNING: OOV dictionary entry (ကုန်သွယ်ရေး - amerce)
WARNING: OOV dictionary entry (ဆိတ်သား - goatish)
WARNING: OOV dictionary entry (အပျိုစင် - maidenly)
WARNING: OOV dictionary entry (တောက်ပ - glower)
WARNING: OOV dictionary entry (ရှယ်ယာရှင် - shareowner)
WARNING: OOV dictionary entry (ရေဗက္ကာ - rebec)
WARNING: OOV dictionary entry (အလုပ်သင် - interne)
WARNING: OOV dictionary entry (ငါးရံ့ - sylph)
WARNING: OOV dictionary entry (သပ်သပ်ရပ်ရပ် - neaten)
WARNING: OOV dictionary entry (မာဂျရင်း - margarin)
WARNING: OOV dictionary entry (ပြဇာတ် - playsuit)
WARNING: OOV dictionary entry (တွန်းအား - impetuousness)
WARNING: OOV dictionary entry (အပြတ်အသတ် - landslip)
WARNING: OOV dictionary entry (အနီးဆုံး - nethermost)
WARNING: OOV dictionary entry (လူလိမ် - luff)
WARNING: OOV dictionary entry (ပိတုန်း - bumble)
WARNING: OOV dictionary entry (ဆွဲဆောင်မှု - engrossment)
WARNING: OOV dictionary entry (အမှား - mishear)
WARNING: OOV dictionary entry (ချစ်သား - fellah)
WARNING: OOV dictionary entry (ပြိုင်ပွဲဝင် - racegoer)
WARNING: OOV dictionary entry (လက်ရှိ - procumbent)
WARNING: OOV dictionary entry (ဝီရိယ - wiliness)
WARNING: OOV dictionary entry (ငါးပိ - pasteurise)
WARNING: OOV dictionary entry (ကော်မရှင်နာ - commissionaire)
WARNING: OOV dictionary entry (ခြေကျင်း - anklet)
WARNING: OOV dictionary entry (စာရေးဆရာ - clerisy)
WARNING: OOV dictionary entry (အိုး - uhu)
WARNING: OOV dictionary entry (မှုတ်ထုတ် - blowzy)
WARNING: OOV dictionary entry (အံ့မခန်း - umbrageous)
WARNING: OOV dictionary entry (ပိုးကောင် - poulterer)
WARNING: OOV dictionary entry (ငါးပိ - waspish)
WARNING: OOV dictionary entry (မျှော်လင့်ချက် - suppositious)
WARNING: OOV dictionary entry (အထီးကျန် - seclusive)
WARNING: OOV dictionary entry (သိသိသာသာ - viscously)
WARNING: OOV dictionary entry (ဆိတ်သား - goatsucker)
WARNING: OOV dictionary entry (အဖျား - feverfew)
WARNING: OOV dictionary entry (အရှိတရား - factitious)
WARNING: OOV dictionary entry (ဒီမိုကရေစီ - democratism)
WARNING: OOV dictionary entry (ပုဒ်ဖြတ် - punctilio)
WARNING: OOV dictionary entry (မျက်နှာ - tufaceous)
WARNING: OOV dictionary entry (ဆွဲတင် - pullup)
WARNING: OOV dictionary entry (မျက်နှာဖုံး - impanel)
WARNING: OOV dictionary entry (ရေကြောင်း - nautically)
WARNING: OOV dictionary entry (ပြင်းပြင်းထန်ထန် - vivaciously)
WARNING: OOV dictionary entry (ဝီရိယ - wistfulness)
WARNING: OOV dictionary entry (အမှတ်အသား - markedness)
WARNING: OOV dictionary entry (ကွဲကွဲပြားပြား - disunite)
WARNING: OOV dictionary entry (စာကြည့်တိုက် - pressroom)
WARNING: OOV dictionary entry (မုန်တိုင်း - stormer)
WARNING: OOV dictionary entry (တံခါးပေါက် - gateaux)
WARNING: OOV dictionary entry (ဝက်သား - muttonhead)
WARNING: OOV dictionary entry (မျက်ခုံးမွေး - middlebrow)
WARNING: OOV dictionary entry (ကျိန်ဆို - swearword)
WARNING: OOV dictionary entry (စားသုံးမှု - alimentation)
WARNING: OOV dictionary entry (စပျစ်သီး - grapey)
WARNING: OOV dictionary entry (မော်တော်ဆိုင်ကယ် - motorbus)
WARNING: OOV dictionary entry (လှော် - diddle)
WARNING: OOV dictionary entry (ကြက်ကင် - roister)
WARNING: OOV dictionary entry (ဆန့်ကျင် - contuse)
WARNING: OOV dictionary entry (ကျား - tigerish)
WARNING: OOV dictionary entry (ဂုဏ် - splendent)
WARNING: OOV dictionary entry (မချိတင်ကဲ - disconsolately)
WARNING: OOV dictionary entry (ရိုးတွင်းခြင်ဆီ - marrowbone)
WARNING: OOV dictionary entry (လက်ကမ်းစာစောင် - handbill)
WARNING: OOV dictionary entry (မကျေမနပ် - dissonantly)
WARNING: OOV dictionary entry (ဒေါင်လိုက် - vert)
WARNING: OOV dictionary entry (ဆီးအိမ် - pule)
WARNING: OOV dictionary entry (အကျည်းတန် - scummy)
WARNING: OOV dictionary entry (ရုပ်ရှင် - moviedom)
WARNING: OOV dictionary entry (တေးရေးဆရာ - melodist)
WARNING: OOV dictionary entry (အစွမ်းထက် - potful)
WARNING: OOV dictionary entry (အလွန်အကျွံ - oversteer)
WARNING: OOV dictionary entry (သိသိသာသာ - mawkishly)
WARNING: OOV dictionary entry (လုပ်ခ - wagerer)
WARNING: OOV dictionary entry (ခမ်းနား - magnific)
WARNING: OOV dictionary entry (ဒါပဲ - dah)
WARNING: OOV dictionary entry (အမြန်လမ်း - speedwalk)
WARNING: OOV dictionary entry (စပ်ကြား - spic)
WARNING: OOV dictionary entry (ကျောပိုးအိတ် - afterdeck)
WARNING: OOV dictionary entry (မျက်မမြင် - purblind)
WARNING: OOV dictionary entry (ရှေ့ဆောင် - vanguardist)
WARNING: OOV dictionary entry (ချိတ်ပိုး - hookworm)
WARNING: OOV dictionary entry (သိမ်းငှက် - falchion)
WARNING: OOV dictionary entry (ရယ် - faugh)
WARNING: OOV dictionary entry (ယဉ်ကျေးမှု - civilise)
WARNING: OOV dictionary entry (မသိမသာ - witlessly)
WARNING: OOV dictionary entry (အအေးခန်း - refrigerative)
WARNING: OOV dictionary entry (အပူပိုင်းဒေသ - tropism)
WARNING: OOV dictionary entry (သော့ခလောက် - bollocks)
WARNING: OOV dictionary entry (အားမာန် - vigorousness)
WARNING: OOV dictionary entry (ဥယျာဉ်ခြံ - gardenia)
WARNING: OOV dictionary entry (စစ်အစိုးရ - junto)
WARNING: OOV dictionary entry (အထိတ်တလန့် - carious)
WARNING: OOV dictionary entry (လုပ်ပိုင်ခွင့် - mandator)
WARNING: OOV dictionary entry (ခွက် - cupreous)
WARNING: OOV dictionary entry (အသံထွက် - pronunciamento)
WARNING: OOV dictionary entry (မင်္ဂလာဆောင် - wedgelike)
WARNING: OOV dictionary entry (နေရောင်ခြည် - solarize)
WARNING: OOV dictionary entry (အိုကေ - och)
WARNING: OOV dictionary entry (ရောဂါဗေဒ - pedology)
WARNING: OOV dictionary entry (ဌာနခွဲ - compartmentalise)
WARNING: OOV dictionary entry (ဒေဝီ - deva)
WARNING: OOV dictionary entry (နက်ပကျွန်း - neptune)
WARNING: OOV dictionary entry (တရကြမ်း - turbulently)
WARNING: OOV dictionary entry (စိတ်ပညာရှင် - mentalist)
WARNING: OOV dictionary entry (အရောင်တင် - palish)
WARNING: OOV dictionary entry (ကိတ်မုန့် - cakehole)
WARNING: OOV dictionary entry (မြောက်ဘက် - northcountry)
WARNING: OOV dictionary entry (ပန်း - floristry)
WARNING: OOV dictionary entry (ညှိနှိုင်းမှု - convenance)
WARNING: OOV dictionary entry (အနောက်ဘက် - westing)
WARNING: OOV dictionary entry (လုပ်သား - laborite)
WARNING: OOV dictionary entry (အပိုင်းပိုင်း - segmentally)
WARNING: OOV dictionary entry (ဂျီ - gie)
WARNING: OOV dictionary entry (တိတိကျကျ - punctiliously)
WARNING: OOV dictionary entry (ဟေ့ - ahoy)
WARNING: OOV dictionary entry (မိုးခြိမ်းသံ - thunderthighs)
WARNING: OOV dictionary entry (အလုပ်သမား - outworker)
WARNING: OOV dictionary entry (မက်ဒရစ် - madden)
WARNING: OOV dictionary entry (ရေနံဆီ - kerosine)
WARNING: OOV dictionary entry (ကုတင် - bedsit)
WARNING: OOV dictionary entry (ခေါင်းစွပ် - headstand)
WARNING: OOV dictionary entry (ပယ်ဖျက် - cancellate)
WARNING: OOV dictionary entry (ဥယျာဉ်မှူး - orchardist)
WARNING: OOV dictionary entry (ဒေလီယာ - dahlia)
WARNING: OOV dictionary entry (သကြားလုံး - candyfloss)
WARNING: OOV dictionary entry (ရထားထိန်း - trainman)
WARNING: OOV dictionary entry (မျက်မြင် - sightly)
WARNING: OOV dictionary entry (တိတ်တဆိတ် - crawly)
WARNING: OOV dictionary entry (ပေါင်းစပ် - compend)
WARNING: OOV dictionary entry (လွဲချော် - misspend)
WARNING: OOV dictionary entry (ပျက်ပြယ် - voidance)
WARNING: OOV dictionary entry (လက်နက်မဲ့ - unarm)
WARNING: OOV dictionary entry (ဆက်တိုက် - rowdily)
WARNING: OOV dictionary entry (ကြိတ်စက် - lathing)
WARNING: OOV dictionary entry (တီးဝိုင်း - bandsman)
WARNING: OOV dictionary entry (သတ်မှတ်ချက် - stipule)
WARNING: OOV dictionary entry (သုံးကြိမ် - trifocal)
WARNING: OOV dictionary entry (ရောနှော - blench)
WARNING: OOV dictionary entry (ဆေးရည် - potation)
WARNING: OOV dictionary entry (နား - earing)
WARNING: OOV dictionary entry (မသိ - unbeknown)
WARNING: OOV dictionary entry (ကလဲ့စားချေ - venge)
WARNING: OOV dictionary entry (လေပြည် - zephyr)
WARNING: OOV dictionary entry (အမြတ်အစွန်း - profiterole)
WARNING: OOV dictionary entry (တာရာ - tarsus)
WARNING: OOV dictionary entry (ဆရာ - overmaster)
WARNING: OOV dictionary entry (မကျေမနပ် - disgruntle)
WARNING: OOV dictionary entry (ဆောင်ပုဒ် - blotto)
WARNING: OOV dictionary entry (ခွေးသား - dogmeat)
WARNING: OOV dictionary entry (ခုန် - jounce)
WARNING: OOV dictionary entry (ပင်လယ်လှိုင်း - wassail)
WARNING: OOV dictionary entry (လမ်းပန်းဆက်သွယ်ရေး - roadability)
WARNING: OOV dictionary entry (ပညာရေး - educability)
WARNING: OOV dictionary entry (ခေါင်းစီး - towhead)
WARNING: OOV dictionary entry (အမိန့် - delict)
WARNING: OOV dictionary entry (ခလုတ် - keypunch)
WARNING: OOV dictionary entry (အရေးမပါ - quincuncial)
WARNING: OOV dictionary entry (ကူးစက်ရောဂါ - epidiascope)
WARNING: OOV dictionary entry (ခေါင်းစွပ် - headpin)
WARNING: OOV dictionary entry (ဘီလူး - ogress)
WARNING: OOV dictionary entry (အောက်ခြေ - frump)
WARNING: OOV dictionary entry (အိမ်နီးချင်း - weighbridge)
WARNING: OOV dictionary entry (ကျောင်းဆရာမ - schoolmistress)
WARNING: OOV dictionary entry (တရားခံ - vindicatory)
WARNING: OOV dictionary entry (ပြတ်ပြတ်သားသား - indiscrete)
WARNING: OOV dictionary entry (သံလမ်း - railroader)
WARNING: OOV dictionary entry (ဟာဂျီ - hajji)
WARNING: OOV dictionary entry (အဇာတသတ် - patricidal)
WARNING: OOV dictionary entry (ပြင်းပြင်းထန်ထန် - peevishly)
WARNING: OOV dictionary entry (သတ္တု - metalled)
WARNING: OOV dictionary entry (သေတ္တာ - boxroom)
WARNING: OOV dictionary entry (ဆီးအိမ် - saccule)
WARNING: OOV dictionary entry (ကမ်းရိုးတန်း - coastland)
WARNING: OOV dictionary entry (ပန်းပွင့် - flowerer)
WARNING: OOV dictionary entry (အားနည်းချက် - vulnerary)
WARNING: OOV dictionary entry (ထိုသို့ - thitherto)
WARNING: OOV dictionary entry (ပို - soarer)
WARNING: OOV dictionary entry (လိပ်စာ - addresser)
WARNING: OOV dictionary entry (ငါးခူ - filefish)
WARNING: OOV dictionary entry (နိယာမ - intinction)
WARNING: OOV dictionary entry (ကြမ်းပြင် - vulpine)
WARNING: OOV dictionary entry (ပြဇာတ် - playact)
WARNING: OOV dictionary entry (ခြံစောင့် - yardmaster)
WARNING: OOV dictionary entry (အိမ်ရှင် - hostler)
WARNING: OOV dictionary entry (အဆမတန် - overweigh)
WARNING: OOV dictionary entry (အနောက်မြောက် - northwester)
WARNING: OOV dictionary entry (မပြေမလည် - unsmooth)
WARNING: OOV dictionary entry (အကြောင်းပြချက် - ratiocinator)
WARNING: OOV dictionary entry (ခေါင်းလိမ်းဆီ - pomade)
WARNING: OOV dictionary entry (ပေါ့ပေါ့တန်တန် - flashily)
WARNING: OOV dictionary entry (အမှန် - veridical)
WARNING: OOV dictionary entry (နေထိုင်မှု - inhabitancy)
WARNING: OOV dictionary entry (မှို - moult)
WARNING: OOV dictionary entry (နှင်းပေါက် - snowcap)
WARNING: OOV dictionary entry (ရှပ်အင်္ကျီ - shirtwaist)
WARNING: OOV dictionary entry (ရောင်ပြန် - reflectiveness)
WARNING: OOV dictionary entry (ဒေါသစိတ် - ruefulness)
WARNING: OOV dictionary entry (ရုပ်ကလာပ် - cadaverous)
WARNING: OOV dictionary entry (ရေချိုးခန်း - showery)
WARNING: OOV dictionary entry (အသေးစား - miniaturise)
WARNING: OOV dictionary entry (ရည်ရွယ်ချက် - intendance)
WARNING: OOV dictionary entry (အစွယ် - yaws)
WARNING: OOV dictionary entry (ဖြိုဖျက် - dissimilate)
WARNING: OOV dictionary entry (ဂျယ်လီ - geld)
WARNING: OOV dictionary entry (တယ်လီနော - telly)
WARNING: OOV dictionary entry (ပညာရှိ - wiseacre)
WARNING: OOV dictionary entry (မီးခွက် - chandlery)
WARNING: OOV dictionary entry (သဘာဝကျကျ - naturalise)
WARNING: OOV dictionary entry (သတင်းစာဆရာ - newspaperwoman)
WARNING: OOV dictionary entry (ရယ်စရာ - funniness)
WARNING: OOV dictionary entry (အနုပညာသမား - artillerist)
WARNING: OOV dictionary entry (စစ်ဆေးခြင်း - vetchling)
WARNING: OOV dictionary entry (ပါလက်စတိုင်း - palestinian)
WARNING: OOV dictionary entry (ချေဖျက် - detune)
WARNING: OOV dictionary entry (ကြက်လျှာ - pennate)
WARNING: OOV dictionary entry (ဆွတ်ဆွတ် - gloaming)
WARNING: OOV dictionary entry (မိုးကျရွှေကိုယ် - nonpareil)
WARNING: OOV dictionary entry (ကြိုတင်လက်မှတ် - pretermit)
WARNING: OOV dictionary entry (ညစာ - tinner)
WARNING: OOV dictionary entry (ဘက်ထရီ - cattery)
WARNING: OOV dictionary entry (အသစ်အဆန်း - novelize)
WARNING: OOV dictionary entry (သွေးပြန်ကြော - veinal)
WARNING: OOV dictionary entry (လူဆိုး - villainously)
WARNING: OOV dictionary entry (တစ်ဝက် - semiweekly)
WARNING: OOV dictionary entry (ပြူတင်းပေါက် - peeper)
WARNING: OOV dictionary entry (အခိုက်အတန့် - trice)
WARNING: OOV dictionary entry (အသစ် - newel)
WARNING: OOV dictionary entry (ခိုင်ခိုင် - groundsel)
WARNING: OOV dictionary entry (ညဘက် - nighty)
WARNING: OOV dictionary entry (တိုင်းတာ - measurer)
WARNING: OOV dictionary entry (ဝံပုလွေ - werwolf)
WARNING: OOV dictionary entry (အဖုံး - casement)
WARNING: OOV dictionary entry (ဆတ်ဆတ် - snaky)
WARNING: OOV dictionary entry (ပုတီးစိပ် - beadle)
WARNING: OOV dictionary entry (သက်သေ - provenience)
WARNING: OOV dictionary entry (အစာမကြေ - indigested)
WARNING: OOV dictionary entry (လက်တင် - latish)
WARNING: OOV dictionary entry (မှီခို - impend)
WARNING: OOV dictionary entry (တိုတို - foreshorten)
WARNING: OOV dictionary entry (စက်ခေါင်း - locomobile)
WARNING: OOV dictionary entry (တောက်ပ - brill)
WARNING: OOV dictionary entry (သိသိသာသာ - saliently)
WARNING: OOV dictionary entry (လေယာဉ်ပျံ - emplane)
WARNING: OOV dictionary entry (ကျော်ကြား - wame)
WARNING: OOV dictionary entry (လည်ပင်း - ringneck)
WARNING: OOV dictionary entry (အကျပ်အတည်း - trouper)
WARNING: OOV dictionary entry (အထူးပြု - particularise)
WARNING: OOV dictionary entry (ပြဇာတ်ရုံ - portiere)
WARNING: OOV dictionary entry (ဘေဘီ - babel)
WARNING: OOV dictionary entry (ညနေခင်း - evenfall)
WARNING: OOV dictionary entry (ဖန်ခွက် - glassful)
WARNING: OOV dictionary entry (ကျေးလက် - fustic)
WARNING: OOV dictionary entry (အနီးကပ် - appose)
WARNING: OOV dictionary entry (ဘုန်းကြီးကျောင်း - monasterial)
WARNING: OOV dictionary entry (သမားရိုးကျ - conventionalize)
WARNING: OOV dictionary entry (လက်နက် - weaponeer)
WARNING: OOV dictionary entry (ဆောင်းရာသီ - wowser)
WARNING: OOV dictionary entry (နံရံကပ် - wallower)
WARNING: OOV dictionary entry (ပျော်ရွှင်မှု - merriness)
WARNING: OOV dictionary entry (ဓာတ်သတ္တု - mineralogically)
WARNING: OOV dictionary entry (ဘာဘူ - baboo)
WARNING: OOV dictionary entry (အိပ်ရာခင်း - bedpost)
WARNING: OOV dictionary entry (အမျိုးအစား - assort)
WARNING: OOV dictionary entry (ရိုးရှင်း - simp)
WARNING: OOV dictionary entry (စာတန်းထိုး - castellated)
WARNING: OOV dictionary entry (နေ့စေ့လစေ့ - parturient)
WARNING: OOV dictionary entry (ရန်ပွဲ - outre)
WARNING: OOV dictionary entry (မိနစ် - minuend)
WARNING: OOV dictionary entry (ပညာရှိ - witted)
WARNING: OOV dictionary entry (ရံခါ - periphrastically)
WARNING: OOV dictionary entry (လက်သည်း - palmate)
WARNING: OOV dictionary entry (အပ်ငွေ - deposal)
WARNING: OOV dictionary entry (အနည်းငယ် - scantly)
WARNING: OOV dictionary entry (နှစ်ထပ် - quadrantal)
WARNING: OOV dictionary entry (စုရုံး - ingather)
WARNING: OOV dictionary entry (မသိမသာ - uncourtly)
WARNING: OOV dictionary entry (ရက်တို - rackety)
WARNING: OOV dictionary entry (မြေပြင် - groundling)
WARNING: OOV dictionary entry (ငိုကြွေးသံ - weeper)
WARNING: OOV dictionary entry (မင်္ဂလာ - blether)
WARNING: OOV dictionary entry (အဆန်း - oddment)
WARNING: OOV dictionary entry (အိုကေ - oik)
WARNING: OOV dictionary entry (အဋ္ဌမ - absinth)
WARNING: OOV dictionary entry (ရာသီဥတု - weatherworn)
WARNING: OOV dictionary entry (အပိုင်းပိုင်း - sectionally)
WARNING: OOV dictionary entry (အဆင်မပြေ - wady)
WARNING: OOV dictionary entry (တဝဲလည်လည် - lingeringly)
WARNING: OOV dictionary entry (အနီးဆုံး - sternmost)
WARNING: OOV dictionary entry (ခေါင်းစွပ် - headcase)
WARNING: OOV dictionary entry (ပေါင်းစပ် - collimate)
WARNING: OOV dictionary entry (မြောက်ဘက် - northing)
WARNING: OOV dictionary entry (အနောက်တိုင်း - wester)
WARNING: OOV dictionary entry (အနောက်ဘက် - hindquarter)
WARNING: OOV dictionary entry (ဖရန့် - francium)
WARNING: OOV dictionary entry (သန်းကြွယ်သူဌေး - millionairess)
WARNING: OOV dictionary entry (ဝါဒ - demist)
WARNING: OOV dictionary entry (အဆင့် - leveller)
WARNING: OOV dictionary entry (လူသတ်မှု - murderousness)
WARNING: OOV dictionary entry (မူဆလင် - musjid)
WARNING: OOV dictionary entry (ရေမှုတ် - spathe)
WARNING: OOV dictionary entry (ကောင်းစွာ - wally)
WARNING: OOV dictionary entry (တွန်းကန် - propellent)
WARNING: OOV dictionary entry (ကောလိပ် - collegian)
WARNING: OOV dictionary entry (ရည်ရွယ်ချက် - objectiveness)
WARNING: OOV dictionary entry (မိုးကြိုးပစ် - thunderhead)
WARNING: OOV dictionary entry (ဝက်သား - porker)
WARNING: OOV dictionary entry (အဟန့်အတား - determent)
WARNING: OOV dictionary entry (အုတ်ခဲ - briquette)
WARNING: OOV dictionary entry (လူငယ် - juvenilia)
WARNING: OOV dictionary entry (ရေစုပ်စက် - drainer)
WARNING: OOV dictionary entry (ဗိုက်နာ - stomache)
WARNING: OOV dictionary entry (ဒယ်အိုး - reddle)
WARNING: OOV dictionary entry (အလွန်အကျွံ - overexpand)
WARNING: OOV dictionary entry (သင်္ဘောသား - shipman)
WARNING: OOV dictionary entry (မီးကျောက် - firestone)
WARNING: OOV dictionary entry (ချီးကျူး - felicitate)
WARNING: OOV dictionary entry (စာရေး - clerkly)
WARNING: OOV dictionary entry (ဘီယာ - beery)
WARNING: OOV dictionary entry (လည်စည်း - necklet)
WARNING: OOV dictionary entry (နိဂုံးချုပ် - finical)
WARNING: OOV dictionary entry (လှော်ခတ် - unsaddle)
WARNING: OOV dictionary entry (ဆေးပညာ - medico)
WARNING: OOV dictionary entry (လူမျိုးစွဲ - nepotist)
WARNING: OOV dictionary entry (သုံးဆ - threepence)
WARNING: OOV dictionary entry (မြေသား - groundwell)
WARNING: OOV dictionary entry (လက် - handwoven)
WARNING: OOV dictionary entry (ပုရစ် - crick)
WARNING: OOV dictionary entry (ဂျင်မီ - jimmy)
WARNING: OOV dictionary entry (ကျေးလက်တောရွာ - rusticate)
WARNING: OOV dictionary entry (မေတ္တာ - metta)
WARNING: OOV dictionary entry (ဂျာနယ်လစ် - journalese)
WARNING: OOV dictionary entry (အချုပ်ခန်း - cellarage)
WARNING: OOV dictionary entry (အိုး - oof)
WARNING: OOV dictionary entry (မှီခို - impendent)
WARNING: OOV dictionary entry (စွန့်စားခန်း - adventurously)
WARNING: OOV dictionary entry (အသည်းနှလုံး - hardhearted)
WARNING: OOV dictionary entry (သမဂ္ဂ - unionise)
WARNING: OOV dictionary entry (ညှိနှိုင်းမှု - incoordination)
WARNING: OOV dictionary entry (အလျှော့မပေး - unyieldingly)
WARNING: OOV dictionary entry (လူသတ်သမား - maleficent)
WARNING: OOV dictionary entry (သင်္ဘောသား - seamer)
WARNING: OOV dictionary entry (ရန်ဖြစ် - quarreller)
WARNING: OOV dictionary entry (စုဝေး - convolve)
WARNING: OOV dictionary entry (သစ်ပင်ပန်းမန် - florae)
WARNING: OOV dictionary entry (သစ်ကြားသီး - nutmeat)
WARNING: OOV dictionary entry (မှုန်ဝါးဝါး - haziness)
WARNING: OOV dictionary entry (အတင်းအဖျင်း - gossipmonger)
WARNING: OOV dictionary entry (ညဝတ် - nightwear)
WARNING: OOV dictionary entry (သွက်သွက်လက်လက် - fugly)
WARNING: OOV dictionary entry (နိုဘယ်လ်ဆု - nobelium)
WARNING: OOV dictionary entry (ဒဏ်ခတ် - strick)
WARNING: OOV dictionary entry (စစ်အင်အား - militarise)
WARNING: OOV dictionary entry (တရားဝင် - officialese)
WARNING: OOV dictionary entry (ကြားဖြတ် - interstice)
WARNING: OOV dictionary entry (အလံတိုင် - flagellate)
WARNING: OOV dictionary entry (ဂိမ်း - gam)
WARNING: OOV dictionary entry (ရိုက် - whump)
WARNING: OOV dictionary entry (အနာ - ululation)
WARNING: OOV dictionary entry (မလှုပ်မယှက် - motionlessly)
WARNING: OOV dictionary entry (ပိုဒ် - stanzaic)
WARNING: OOV dictionary entry (ပါရီ - paretic)
WARNING: OOV dictionary entry (လက်ထောက် - bailor)
WARNING: OOV dictionary entry (အလှဆင် - ornamentally)
WARNING: OOV dictionary entry (လက်ကောက်ဝတ် - wristlock)
WARNING: OOV dictionary entry (ရာသီဥတု - weatherize)
WARNING: OOV dictionary entry (ကမ်းခြေ - coastward)
WARNING: OOV dictionary entry (တာဝါတိုင် - weir)
WARNING: OOV dictionary entry (နေထိုင်သူ - habitant)
WARNING: OOV dictionary entry (လောင်းကစား - gabble)
WARNING: OOV dictionary entry (ထိပ်တန်း - supernal)
WARNING: OOV dictionary entry (အရေးအသား - mottle)
WARNING: OOV dictionary entry (ဆင်ဆာ - censorial)
WARNING: OOV dictionary entry (သင်းခွေချပ် - pangolin)
WARNING: OOV dictionary entry (ရေအောက် - submerse)
WARNING: OOV dictionary entry (အလုပ် - jobby)
WARNING: OOV dictionary entry (အဘိုးအဘွား - grandpapa)
WARNING: OOV dictionary entry (ငါးဖမ်းသမား - fishwife)
WARNING: OOV dictionary entry (အေးအေးဆေးဆေး - relaxedly)
WARNING: OOV dictionary entry (ဒိုင်ခွက် - dicer)
WARNING: OOV dictionary entry (ကုန်စိမ်း - greengrocery)
WARNING: OOV dictionary entry (အစာ - feedstuff)
WARNING: OOV dictionary entry (သော့ခလောက် - picklock)
WARNING: OOV dictionary entry (အဇာတသတ် - patricide)
WARNING: OOV dictionary entry (အခမဲ့ - freeby)
WARNING: OOV dictionary entry (နောက်ကြောင်းပြန် - retroact)
WARNING: OOV dictionary entry (ဇာတိ - natality)
WARNING: OOV dictionary entry (လမ်းမကြီး - mainroad)
WARNING: OOV dictionary entry (တူးမြောင်း - canalize)
WARNING: OOV dictionary entry (ဂုဏ်သတင်း - prestissimo)
WARNING: OOV dictionary entry (နှင်တံ - whipstitch)
WARNING: OOV dictionary entry (ဆောင်းပါး - tonsorial)
WARNING: OOV dictionary entry (ကစားပွဲ - playgame)
WARNING: OOV dictionary entry (ဘေးတိုက် - sideward)
WARNING: OOV dictionary entry (အာကာသယာဉ် - aerosphere)
WARNING: OOV dictionary entry (ရှေးယခင် - antecede)
WARNING: OOV dictionary entry (ကျားမ - gendermerie)
WARNING: OOV dictionary entry (ဘာဂါ - burgle)
WARNING: OOV dictionary entry (မကျေမနပ် - indolently)
WARNING: OOV dictionary entry (လယ်သမား - fieldsman)
WARNING: OOV dictionary entry (စွယ် - tuskless)
WARNING: OOV dictionary entry (အီစတာ - easterner)
WARNING: OOV dictionary entry (တေးဂီတသံ - melodically)
WARNING: OOV dictionary entry (တင်ပါး - kecks)
WARNING: OOV dictionary entry (ဆေးစာ - prescript)
WARNING: OOV dictionary entry (တစ်ချိန်ချိန် - somewhen)
WARNING: OOV dictionary entry (အပြုအမူ - manneristic)
WARNING: OOV dictionary entry (ပေါင်းစည်း - agglutinate)
WARNING: OOV dictionary entry (လက်ဖက်ရည်ဆိုင် - teacake)
WARNING: OOV dictionary entry (ရင်ဘတ် - chesty)
WARNING: OOV dictionary entry (ပြင်းပြင်းထန်ထန် - vexingly)
WARNING: OOV dictionary entry (ကဗျာဆရာ - poetaster)
WARNING: OOV dictionary entry (တည်ဆောက်ရေး - outbuilding)
WARNING: OOV dictionary entry (အလင်းရောင် - illuminance)
WARNING: OOV dictionary entry (ကြောင် - cunny)
WARNING: OOV dictionary entry (ကြောက်စရာ - dreadfulness)
WARNING: OOV dictionary entry (ဇွန်း - spoony)
WARNING: OOV dictionary entry (သင်ရိုးညွှန်းတမ်း - curricle)
WARNING: OOV dictionary entry (ပြင်းပြင်းထန်ထန် - tussive)
WARNING: OOV dictionary entry (မိုးခြိမ်းသံ - thunderclap)
WARNING: OOV dictionary entry (စိုက်ပျိုးရေး - apiculture)
WARNING: OOV dictionary entry (နောက်ကျော - backsaw)
WARNING: OOV dictionary entry (တွန့်လိမ် - wriggler)
WARNING: OOV dictionary entry (မီးရထားတွဲ - waggon)
WARNING: OOV dictionary entry (တားမြစ်ချက် - tabour)
WARNING: OOV dictionary entry (သီးသန့် - reservedly)
WARNING: OOV dictionary entry (ကုန်လှောင်ရုံ - wareroom)
WARNING: OOV dictionary entry (စကားပြော - talky)
WARNING: OOV dictionary entry (အထိမ်းအမှတ် - memorialise)
WARNING: OOV dictionary entry (တော - queerness)
WARNING: OOV dictionary entry (ပျော်ရွှင်မှု - blissfulness)
WARNING: OOV dictionary entry (ဆန္ဒ - wishfulness)
WARNING: OOV dictionary entry (ကြွက်သား - muscularly)
WARNING: OOV dictionary entry (ရထား - carroty)
WARNING: OOV dictionary entry (ကျောက်ခဲ - whetstone)
WARNING: OOV dictionary entry (လေယာဉ် - aerodyne)
WARNING: OOV dictionary entry (ဂိုးသမား - goalmouth)
WARNING: OOV dictionary entry (အဝတ်လျှော်စက် - rasher)
WARNING: OOV dictionary entry (ဖျင်း - chaffer)
WARNING: OOV dictionary entry (ပညာရှိ - wiseman)
WARNING: OOV dictionary entry (မြန်နှုန်း - speeder)
WARNING: OOV dictionary entry (အင်တာနက် - inearth)
WARNING: OOV dictionary entry (ဖန်ခွက် - glasswork)
WARNING: OOV dictionary entry (ကေဒါ - cadge)
WARNING: OOV dictionary entry (ပြောင် - baldy)
WARNING: OOV dictionary entry (ပညာ - sapience)
WARNING: OOV dictionary entry (ဆေးဒန်း - orpiment)
WARNING: OOV dictionary entry (အစာအိမ် - stomachic)
WARNING: OOV dictionary entry (ရှားပါး - rarebit)
WARNING: OOV dictionary entry (ရောင်းသူ - repeller)
WARNING: OOV dictionary entry (အစေခံ - manservant)
WARNING: OOV dictionary entry (နွားသိုး - cowman)
WARNING: OOV dictionary entry (ဝတ်ဆံ - stamen)
WARNING: OOV dictionary entry (အပယ်ခံ - outcaste)
WARNING: OOV dictionary entry (မီးစက် - wickerwork)
WARNING: OOV dictionary entry (ဝိုးတိုးဝါးတား - hazily)
WARNING: OOV dictionary entry (လူသစ် - rooky)
WARNING: OOV dictionary entry (ဟာဂျီ - haji)
WARNING: OOV dictionary entry (မီလီမီတာ - millilitre)
WARNING: OOV dictionary entry (ငွေ့ - sapor)
WARNING: OOV dictionary entry (ပေါင်းစပ် - confabulate)
WARNING: OOV dictionary entry (ဖြတ်ထုတ် - cutup)
WARNING: OOV dictionary entry (ပတ်လည် - enwrap)
WARNING: OOV dictionary entry (အမှာစကား - gisting)
WARNING: OOV dictionary entry (အစေခံ - subserviently)
WARNING: OOV dictionary entry (လက်အောက်ခံ - subsocial)
WARNING: OOV dictionary entry (ဟုံ - cloy)
WARNING: OOV dictionary entry (လက်သုတ်ပုဝါ - napery)
WARNING: OOV dictionary entry (ထပ်ခါတလဲလဲ - reiterative)
WARNING: OOV dictionary entry (ပိုက်ဆံအိတ် - moneybag)
WARNING: OOV dictionary entry (ကြိုး - ropey)
WARNING: OOV dictionary entry (ကုက္ကုစ္စ - miserliness)
WARNING: OOV dictionary entry (လက်သည်း - nailer)
WARNING: OOV dictionary entry (အမှိုက်ပုံး - litterbug)
WARNING: OOV dictionary entry (ပေါ်ပေါက် - occident)
WARNING: OOV dictionary entry (မက်ထရစ် - metrication)
WARNING: OOV dictionary entry (ပူးပေါင်း - concertize)
WARNING: OOV dictionary entry (ပန်းရန် - plasterer)
WARNING: OOV dictionary entry (မိုးသံ - thuddingly)
WARNING: OOV dictionary entry (အလယ်အလတ် - midrib)
WARNING: OOV dictionary entry (ကစ် - kicky)
WARNING: OOV dictionary entry (အပြန်အလှန် - mutualize)
WARNING: OOV dictionary entry (ဓာတ်ဖို - alchemize)
WARNING: OOV dictionary entry (ရေချိုးကန် - washbasin)
WARNING: OOV dictionary entry (ပြိုင်ပွဲ - raceme)
WARNING: OOV dictionary entry (ထိထိမိမိ - mordantly)
WARNING: OOV dictionary entry (မည်သို့ပင်ဖြစ်စေ - anywise)
WARNING: OOV dictionary entry (ကြက်သမား - poultryman)
WARNING: OOV dictionary entry (မိုးကာ - rainwear)
WARNING: OOV dictionary entry (နှင်းပေါက် - snowdrop)
WARNING: OOV dictionary entry (ဂျာမန် - merman)
WARNING: OOV dictionary entry (အသာတကြည် - nebulously)
WARNING: OOV dictionary entry (ဝါတော် - vasa)
WARNING: OOV dictionary entry (အခက်အခဲ - confliction)
WARNING: OOV dictionary entry (နန်းတော် - vicennial)
WARNING: OOV dictionary entry (ချော့မော့ - sedately)
WARNING: OOV dictionary entry (ဘိလပ်မြေ - cementum)
WARNING: OOV dictionary entry (တူရိယာ - percuss)
WARNING: OOV dictionary entry (သဘောထား - tendance)
WARNING: OOV dictionary entry (ရမယ် - gotta)
WARNING: OOV dictionary entry (အလုပ်ရှင် - workwoman)
WARNING: OOV dictionary entry (ညည်းတွားသံ - whin)
WARNING: OOV dictionary entry (ဒေါသတကြီး - resentfully)
WARNING: OOV dictionary entry (အရှုပ်တော်ပုံ - scandalmonger)
WARNING: OOV dictionary entry (ဖျန်ဖြေ - mediative)
WARNING: OOV dictionary entry (ပန်းကုံး - wreathe)
WARNING: OOV dictionary entry (လက်ကောက် - bangle)
WARNING: OOV dictionary entry (အာဇာနည် - martyrize)
WARNING: OOV dictionary entry (သယ်ဆောင် - carryall)
WARNING: OOV dictionary entry (ညှပ်ဖိနပ် - flipflop)
WARNING: OOV dictionary entry (သေရည် - intoxicate)
WARNING: OOV dictionary entry (သားအိမ်ခေါင်း - cervine)
WARNING: OOV dictionary entry (သစ်သား - woodenly)
WARNING: OOV dictionary entry (ကြက်မောက် - shuttlecock)
WARNING: OOV dictionary entry (ခန္ဓာဗေဒ - anatomize)
WARNING: OOV dictionary entry (ကြမ်းပြင် - granger)
WARNING: OOV dictionary entry (ဝိုင် - wahine)
WARNING: OOV dictionary entry (အထွတ်အထိပ် - pinnace)
WARNING: OOV dictionary entry (ရှက်တယ် - shyster)
WARNING: OOV dictionary entry (ကြာပွတ် - whipper)
WARNING: OOV dictionary entry (အစောင့် - guardsman)
WARNING: OOV dictionary entry (တစ်နှစ် - anear)
WARNING: OOV dictionary entry (ဘေးတိုက် - sidepiece)
WARNING: OOV dictionary entry (ဝုန်းဒိုင်းကြဲ - boisterously)
WARNING: OOV dictionary entry (စုတ်တံ - stipe)
WARNING: OOV dictionary entry (မလှုပ်မယှက် - waggishly)
WARNING: OOV dictionary entry (ဝံသာနု - wain)
WARNING: OOV dictionary entry (ဖယောင်းတိုင် - candlewick)
WARNING: OOV dictionary entry (အာကာသယာဉ်မှူး - spacewoman)
WARNING: OOV dictionary entry (မျက်နှာဖြူ - whiteface)
WARNING: OOV dictionary entry (လက်ချောင်း - handspring)
WARNING: OOV dictionary entry (ကျောင်းနေဖက် - schoolmarmish)
WARNING: OOV dictionary entry (မြန်မာ - quicklime)
WARNING: OOV dictionary entry (အလုပ် - outwork)
WARNING: OOV dictionary entry (မျိုးစိတ် - inbreed)
WARNING: OOV dictionary entry (ရေမွှေး - perfuming)
WARNING: OOV dictionary entry (နေ့လည်စာ - luncheonette)
WARNING: OOV dictionary entry (အိပ်ရာ - bedhead)
WARNING: OOV dictionary entry (လုံခြုံမှု - securement)
WARNING: OOV dictionary entry (အောင်နိုင်သူ - victualer)
WARNING: OOV dictionary entry (အမှိုက်ပုံ - dreg)
WARNING: OOV dictionary entry (ဓမ္မ - ministerially)
WARNING: OOV dictionary entry (ခြေကျင်း - anklebone)
WARNING: OOV dictionary entry (ကုန်းမြင့် - highlander)
WARNING: OOV dictionary entry (ကုန်ကျစရိတ် - costar)
WARNING: OOV dictionary entry (နားစည် - eardrop)
WARNING: OOV dictionary entry (သုံးသူ - treater)
WARNING: OOV dictionary entry (ပိုးကောင် - bedbug)
WARNING: OOV dictionary entry (ဂရမ် - gramme)
WARNING: OOV dictionary entry (အခန်းကျယ် - roomer)
WARNING: OOV dictionary entry (ခရီး - itinerancy)
WARNING: OOV dictionary entry (အဝိုင်း - roundel)
WARNING: OOV dictionary entry (အခွင့်အလမ်း - opponency)
WARNING: OOV dictionary entry (ဟန်နာ - hahnium)
WARNING: OOV dictionary entry (ပါကေး - parquetry)
WARNING: OOV dictionary entry (မျက်တောင် - glim)
WARNING: OOV dictionary entry (စေတနာရှင် - voluntaryist)
WARNING: OOV dictionary entry (သိုးမွေး - woolgrowing)
WARNING: OOV dictionary entry (မီလီမီတာ - millesimal)
WARNING: OOV dictionary entry (အပင် - plantigrade)
WARNING: OOV dictionary entry (တိုးတက်မှု - spence)
WARNING: OOV dictionary entry (လွတ်လွတ်လပ်လပ် - unblushingly)
WARNING: OOV dictionary entry (ချယ်ရီ - charlady)
WARNING: OOV dictionary entry (ဆံပင်ညှပ် - haberdashery)
WARNING: OOV dictionary entry (စကားပြန် - backsword)
WARNING: OOV dictionary entry (တံတွေး - snit)
WARNING: OOV dictionary entry (တန်းတူ - rorqual)
WARNING: OOV dictionary entry (သစ်တော - afforest)
WARNING: OOV dictionary entry (မျက်မမြင် - blindside)
WARNING: OOV dictionary entry (မြေပဲ - earthnut)
WARNING: OOV dictionary entry (သွေးလွန်တုပ်ကွေး - extravasate)
WARNING: OOV dictionary entry (စိတ်ကူးယဉ်သမား - fictionist)
WARNING: OOV dictionary entry (နွေရာသီ - summerset)
WARNING: OOV dictionary entry (ဧည့်သည် - visitant)
WARNING: OOV dictionary entry (လေယာဉ်ပျံ - enplane)
WARNING: OOV dictionary entry (အသံထွက် - intonate)
WARNING: OOV dictionary entry (ရောင်းသူ - vendace)
WARNING: OOV dictionary entry (ကြိုးမျှင် - strandline)
WARNING: OOV dictionary entry (အပြန်အလှန် - mutationally)
WARNING: OOV dictionary entry (ဝတ္ထုတို - novelette)
WARNING: OOV dictionary entry (အဆင့်အတန်း - regality)
WARNING: OOV dictionary entry (ခေါ် - sumach)
WARNING: OOV dictionary entry (ရုန်းရင်းဆန်ခတ် - wamble)
WARNING: OOV dictionary entry (ကိုယ်တွေ့ - unhand)
WARNING: OOV dictionary entry (အလုပ်သင် - internee)
WARNING: OOV dictionary entry (ကြည့်ရှု - spectate)
WARNING: OOV dictionary entry (တံခါး - gateau)
WARNING: OOV dictionary entry (မြောက်ဘက် - northwardly)
WARNING: OOV dictionary entry (အဆက်မပြတ် - continuant)
WARNING: OOV dictionary entry (အလွန်အကျွံ - overset)
WARNING: OOV dictionary entry (အရှိန်အဟုန် - momentariness)
WARNING: OOV dictionary entry (သွေးလွန်တုပ်ကွေး - haemophiliac)
WARNING: OOV dictionary entry (လည်စည်း - manege)
WARNING: OOV dictionary entry (အီလက်ထရောနစ် - electone)
WARNING: OOV dictionary entry (အပြုံး - smirch)
WARNING: OOV dictionary entry (သမားရိုးကျ - conventionalise)
WARNING: OOV dictionary entry (အလယ်အလတ် - middleweight)
WARNING: OOV dictionary entry (ဘုရားရှိခိုးကျောင်း - churchwoman)
WARNING: OOV dictionary entry (ပန်းပုဆရာ - sculptress)
WARNING: OOV dictionary entry (စစ်မှုထမ်း - enlistee)
WARNING: OOV dictionary entry (လုံခြုံမှု - safeness)
WARNING: OOV dictionary entry (ရုပ်ပျက်ဆင်းပျက် - disfiguration)
WARNING: OOV dictionary entry (ကျောင်းနေဖက် - schoolfellow)
WARNING: OOV dictionary entry (ကျောက်တောင် - cliffy)
WARNING: OOV dictionary entry (ညနေ - yesternight)
WARNING: OOV dictionary entry (တော်မီ - tommy)
WARNING: OOV dictionary entry (အဆီပြန် - fatback)
WARNING: OOV dictionary entry (ဘုရားရေ - golosh)
WARNING: OOV dictionary entry (အလယ်ခေတ် - medievally)
WARNING: OOV dictionary entry (ဟဲလို - welch)
WARNING: OOV dictionary entry (အသေအချာ - martially)
WARNING: OOV dictionary entry (အိမ်နောက်ဖေး - backstairs)
WARNING: OOV dictionary entry (နောက်ကျော - thill)
WARNING: OOV dictionary entry (အာကာသယာဉ်မှူး - aeronaut)
WARNING: OOV dictionary entry (မက်ထရစ် - metricate)
WARNING: OOV dictionary entry (သစ်သား - woodpile)
WARNING: OOV dictionary entry (ကြီးကြီးမားမား - bulgy)
WARNING: OOV dictionary entry (ကျောက်မျက်ရတနာ - gemination)
WARNING: OOV dictionary entry (တန်ပြန် - counterpane)
WARNING: OOV dictionary entry (အပြင်အဆင် - outface)
WARNING: OOV dictionary entry (အရသာ - savoriness)
WARNING: OOV dictionary entry (တောင်ပံ - wingover)
WARNING: OOV dictionary entry (အမြန်နှုန်း - quickset)
WARNING: OOV dictionary entry (လူမှုဆက်ဆံရေး - sociality)
WARNING: OOV dictionary entry (ပေါရာဏ - obsoleteness)
WARNING: OOV dictionary entry (တီးတိုး - whispery)
WARNING: OOV dictionary entry (လက်စွပ် - armlet)
WARNING: OOV dictionary entry (ပုဆိုး - sateen)
WARNING: OOV dictionary entry (ကျွဲ - moated)
WARNING: OOV dictionary entry (လူဆိုး - villous)
WARNING: OOV dictionary entry (သုံးဆ - thievish)
WARNING: OOV dictionary entry (ဟန်နီ - hinny)
WARNING: OOV dictionary entry (လူမှုအဖွဲ့အစည်း - socage)
WARNING: OOV dictionary entry (ထိပ်တန်း - topmast)
WARNING: OOV dictionary entry (ကျောထောက်နောက်ခံ - hunchbacked)
WARNING: OOV dictionary entry (သတင်းအချက်အလက် - informativeness)
WARNING: OOV dictionary entry (ပြင်သစ် - frenchy)
WARNING: OOV dictionary entry (သကြားသီး - sugarplum)
WARNING: OOV dictionary entry (မလုံမခြုံ - insobriety)
WARNING: OOV dictionary entry (ပိုးတုံးလုံး - pupa)
WARNING: OOV dictionary entry (မီးသတ်သမား - fireguard)
WARNING: OOV dictionary entry (သွားရေးလာရေး - commutate)
WARNING: OOV dictionary entry (ထွက်ပြေး - runabout)
WARNING: OOV dictionary entry (အံ့ဖွယ် - miraculousness)
WARNING: OOV dictionary entry (အားလပ်ရက် - vacationist)
WARNING: OOV dictionary entry (နှုန်းထား - rateable)
WARNING: OOV dictionary entry (ပိုးစုန်းကြူး - mayfly)
WARNING: OOV dictionary entry (အောင်မြင်မှု - acclivity)
WARNING: OOV dictionary entry (သင်္ဘောသား - marrier)
WARNING: OOV dictionary entry (ဆွဲကြိုး - pend)
WARNING: OOV dictionary entry (ကွာတားဖိုင်နယ် - quarterfinalist)
WARNING: OOV dictionary entry (စုစုပေါင်း - totalize)
WARNING: OOV dictionary entry (လိမ့်မည် - gonna)
WARNING: OOV dictionary entry (ဥပမာ - egad)
WARNING: OOV dictionary entry (လှုပ်ရှားမှု - motional)
WARNING: OOV dictionary entry (မိုးကာအင်္ကျီ - mackintosh)
WARNING: OOV dictionary entry (စွယ်တော် - stupe)
WARNING: OOV dictionary entry (ကတိ - promisee)
WARNING: OOV dictionary entry (လက်သမား - freemasonary)
WARNING: OOV dictionary entry (ပေါင်ချိန် - poundage)
WARNING: OOV dictionary entry (ရေအား - waterpower)
WARNING: OOV dictionary entry (စတိုင် - stymy)
WARNING: OOV dictionary entry (မူးယစ်ဆေး - druggie)
WARNING: OOV dictionary entry (ကြော်ငြာ - advertent)
WARNING: OOV dictionary entry (ခရမ်းနုရောင် - wisteria)
WARNING: OOV dictionary entry (စိတ်ကူးယဉ် - fict)
WARNING: OOV dictionary entry (သရက်သီး - mangosteen)
WARNING: OOV dictionary entry (အမျိုးမျိုး - varietally)
WARNING: OOV dictionary entry (ဘီလီ - billie)
WARNING: OOV dictionary entry (ဖရိုဖရဲ - shamble)
WARNING: OOV dictionary entry (သင်ရိုးညွှန်းတမ်း - syllabary)
WARNING: OOV dictionary entry (အရိုးစု - skeletonize)
WARNING: OOV dictionary entry (မျက်မှန် - eyeshade)
WARNING: OOV dictionary entry (ပါးစပ် - mouthy)
WARNING: OOV dictionary entry (အင်ပါယာ - empyrean)
WARNING: OOV dictionary entry (တေးသံ - sonance)
WARNING: OOV dictionary entry (ကြင်နာမှု - courteousness)
WARNING: OOV dictionary entry (သန်း - jillion)
WARNING: OOV dictionary entry (တံခွန် - moorage)
WARNING: OOV dictionary entry (နွယ်ပင် - bindweed)
WARNING: OOV dictionary entry (ပြန်ပေး - restitute)
WARNING: OOV dictionary entry (ရှောင်ရှား - evanesce)
WARNING: OOV dictionary entry (ပျော်ရွှင်စရာ - merrythought)
WARNING: OOV dictionary entry (မော်နီတာ - monitorship)
WARNING: OOV dictionary entry (လောင်းလှေ - stakeboat)
WARNING: OOV dictionary entry (အရောင်တင် - colorant)
WARNING: OOV dictionary entry (အိမ်မြှောင် - oarlock)
WARNING: OOV dictionary entry (စီမံခန့်ခွဲ - menage)
WARNING: OOV dictionary entry (မောင်းမ - unman)
WARNING: OOV dictionary entry (ပျော့ဆေး - milden)
WARNING: OOV dictionary entry (အနီကတ် - redcap)
WARNING: OOV dictionary entry (ကီလိုဂရမ် - kilogramme)
WARNING: OOV dictionary entry (ဘေးစောင်း - sideslip)
WARNING: OOV dictionary entry (အပေးအယူ - embrocation)
WARNING: OOV dictionary entry (လယ်ယာ - farness)
WARNING: OOV dictionary entry (အိုး - uhf)
WARNING: OOV dictionary entry (ကျောင်းသား - pupillage)
WARNING: OOV dictionary entry (စီးကရက် - cigaret)
WARNING: OOV dictionary entry (ပွဲတော် - aestival)
WARNING: OOV dictionary entry (စည်းမျဉ်းစည်းကမ်း - regulus)
WARNING: OOV dictionary entry (စကား - headword)
WARNING: OOV dictionary entry (မီလီမီတာ - milliampere)
WARNING: OOV dictionary entry (အမွေအနှစ် - heirdom)
WARNING: OOV dictionary entry (ပိုးစာ - mullock)
WARNING: OOV dictionary entry (လက်သမား - pryer)
WARNING: OOV dictionary entry (တောင်ပိုင်းသား - southlander)
WARNING: OOV dictionary entry (အမွှေးတိုင် - joss)
WARNING: OOV dictionary entry (ကိုးကား - quoter)
WARNING: OOV dictionary entry (ဆူပူ - braw)
WARNING: OOV dictionary entry (သဘာဝတရား - naturism)
WARNING: OOV dictionary entry (ရေသူမ - mermen)
WARNING: OOV dictionary entry (အောင်နိုင်သူ - vanquisher)
WARNING: OOV dictionary entry (ခြေကျင်း - footbath)
WARNING: OOV dictionary entry (စိုးရိမ်စိတ် - apprehensiveness)
WARNING: OOV dictionary entry (ဆံပင်ရှည် - longhair)
WARNING: OOV dictionary entry (နုတ် - subtracter)
WARNING: OOV dictionary entry (သစ်သားအိမ် - woodhouse)
WARNING: OOV dictionary entry (နောက်ပိုင်း - afters)
WARNING: OOV dictionary entry (သေနတ်သံ - gunlock)
WARNING: OOV dictionary entry (စင်တီမီတာ - centesimal)
WARNING: OOV dictionary entry (ပုစဉ်း - stonefly)
WARNING: OOV dictionary entry (အညှာ - stalky)
WARNING: OOV dictionary entry (လက်ပတ် - wristlet)
WARNING: OOV dictionary entry (အလွန်အကျွံ - overact)
WARNING: OOV dictionary entry (ကျောက်ဆူး - anchoress)
WARNING: OOV dictionary entry (မဟုတ်ပါ - nonsuch)
WARNING: OOV dictionary entry (အလုံးစုံ - overarch)
WARNING: OOV dictionary entry (ဒေါသတကြီး - irritatedly)
WARNING: OOV dictionary entry (သရုပ်ဖော် - scenarist)
WARNING: OOV dictionary entry (စားပွဲခုံ - deskill)
WARNING: OOV dictionary entry (ခါးစည်း - waistcloth)
WARNING: OOV dictionary entry (လှံတံ - spewer)
WARNING: OOV dictionary entry (ကျောက်တုံး - stonechat)
WARNING: OOV dictionary entry (ဖြည့်စွက် - suppurate)
WARNING: OOV dictionary entry (သံယောဇဉ် - entwine)
WARNING: OOV dictionary entry (အာမခံ - ensilage)
WARNING: OOV dictionary entry (ရေချိုးခန်း - bathysphere)
WARNING: OOV dictionary entry (မင်းဆက် - dynast)
WARNING: OOV dictionary entry (တိုးဂိတ် - tollhouse)
WARNING: OOV dictionary entry (ပန်းခြံ - parky)
WARNING: OOV dictionary entry (ခက်ခက်ခဲခဲ - heddle)
WARNING: OOV dictionary entry (အကွာအဝေး - outdistance)
WARNING: OOV dictionary entry (နေထိုင်မှု - habiliment)
WARNING: OOV dictionary entry (အညှော် - pungency)
WARNING: OOV dictionary entry (သေခြင်းတရား - deadliness)
WARNING: OOV dictionary entry (အိပ်ယာခင်း - bedsitter)
WARNING: OOV dictionary entry (အစုလိုက် - bunchy)
WARNING: OOV dictionary entry (ဈေးဝယ် - pilchard)
WARNING: OOV dictionary entry (တူးမြောင်း - canalise)
WARNING: OOV dictionary entry (ပေါင်းပင် - weediness)
WARNING: OOV dictionary entry (သတင်းမှား - misinformer)
WARNING: OOV dictionary entry (ဓားရှည် - stabile)
WARNING: OOV dictionary entry (ရွရွ - dashingly)
WARNING: OOV dictionary entry (အဖျက်သမား - vesicant)
WARNING: OOV dictionary entry (ကွဲပြားမှု - viceregency)
WARNING: OOV dictionary entry (စောင်း - slantwise)
WARNING: OOV dictionary entry (ရောဂါဘယ - morbidness)
WARNING: OOV dictionary entry (တီဘီ - tubercule)
WARNING: OOV dictionary entry (အကူအညီ - helot)
WARNING: OOV dictionary entry (ကျွမ်းကျင်သူ - aperient)
WARNING: OOV dictionary entry (ကျွဲ - buffaloed)
WARNING: OOV dictionary entry (ကြွေ - enamor)
WARNING: OOV dictionary entry (စိတ်ဝင်စားမှု - interestedness)
WARNING: OOV dictionary entry (ပဋိညာဉ် - coven)
WARNING: OOV dictionary entry (မျက်နှာဖုံး - masque)
WARNING: OOV dictionary entry (ပန်းထိမ် - ironsmith)
WARNING: OOV dictionary entry (အစာအိမ်နာ - ulcerate)
WARNING: OOV dictionary entry (စင်တီမီတာ - centiliter)
WARNING: OOV dictionary entry (ဗီတာမင် - vitamine)
WARNING: OOV dictionary entry (အဆင်မပြေ - malfeasant)
WARNING: OOV dictionary entry (သေနတ်သံ - outgun)
WARNING: OOV dictionary entry (ဟင်းချို - soupspoon)
WARNING: OOV dictionary entry (သရော်စာ - satirically)
WARNING: OOV dictionary entry (အရက်သမား - chocoholic)
WARNING: OOV dictionary entry (ပဲ့တင်သံ - echoic)
WARNING: OOV dictionary entry (ဟိတ်ကြီးဟန်ကြီး - pompously)
WARNING: OOV dictionary entry (အစားထိုး - substituent)
WARNING: OOV dictionary entry (စိတ်ပျက် - deject)
WARNING: OOV dictionary entry (အခန်း - compart)
WARNING: OOV dictionary entry (အားသွန်ခွန်စိုက် - strenously)
WARNING: OOV dictionary entry (ဆိုးဆေး - dyestuff)
WARNING: OOV dictionary entry (တေးသံရှင် - vocalizer)
WARNING: OOV dictionary entry (မဟာသီယာ - maharanee)
WARNING: OOV dictionary entry (မြို့တော်ခန်းမ - townhall)
WARNING: OOV dictionary entry (ပစ္စည်း - confiture)
WARNING: OOV dictionary entry (သမာဓိ - virtuousness)
WARNING: OOV dictionary entry (မတ်တပ်ရပ် - standee)
WARNING: OOV dictionary entry (ငွေထည် - maunder)
WARNING: OOV dictionary entry (ကြိုတင် - prelims)
WARNING: OOV dictionary entry (မျက်ဖြူ - sclera)
WARNING: OOV dictionary entry (ကျောပိုး - backcloth)
WARNING: OOV dictionary entry (ကောင်းစွာ - wellhouse)
WARNING: OOV dictionary entry (ငါး - fishiness)
WARNING: OOV dictionary entry (ချိုချိုသာသာ - mellifluously)
WARNING: OOV dictionary entry (ခေတ်ပြိုင် - extemporary)
WARNING: OOV dictionary entry (ပေါင်းပင် - weeder)
WARNING: OOV dictionary entry (စီဒီ - sinedie)
WARNING: OOV dictionary entry (လရောင် - moonbeam)
WARNING: OOV dictionary entry (ခေါ်သံ - catcall)
WARNING: OOV dictionary entry (အပွင့် - floury)
WARNING: OOV dictionary entry (လင်းယုန်ငှက် - eaglet)
WARNING: OOV dictionary entry (ကြီးကြီးမားမား - gride)
WARNING: OOV dictionary entry (အုတ်တံတိုင်း - curbstone)
WARNING: OOV dictionary entry (ဟောသည် - soothsay)
WARNING: OOV dictionary entry (အရူးမ - madwoman)
WARNING: OOV dictionary entry (တောက်ပ - scintillate)
WARNING: OOV dictionary entry (စာရွက်စာတမ်း - dosser)
WARNING: OOV dictionary entry (ချစ်စဖွယ် - amorously)
WARNING: OOV dictionary entry (တိတ်ဆိတ် - quietus)
WARNING: OOV dictionary entry (ဆွဲဆောင်မှု - emblazonment)
WARNING: OOV dictionary entry (ကျောင်းပိတ်ရက် - schoolmarm)
WARNING: OOV dictionary entry (ခေါင်းစီး - headstream)
WARNING: OOV dictionary entry (ခြံစောင့် - yardman)
WARNING: OOV dictionary entry (အံ့သြဖွယ် - musingly)
WARNING: OOV dictionary entry (အပုပ် - putridity)
WARNING: OOV dictionary entry (လက်စွပ် - handbasket)
WARNING: OOV dictionary entry (တရှုံ့ရှုံ့ - whiffle)
WARNING: OOV dictionary entry (ရေမှုတ် - waterthrush)
WARNING: OOV dictionary entry (အို - oho)
WARNING: OOV dictionary entry (ကန့်သတ် - limitedly)
WARNING: OOV dictionary entry (တရွေ့ရွေ့ - gushingly)
path:  /media/ye/project2/exp/bilingual-induction/exp1/my-en/vecmap-output10/trg_super/word2vec_s200_mc2_w3.vec
path:  /media/ye/project2/exp/bilingual-induction/exp1/my-en/vecmap-output10/src_super/word2vec_s200_mc2_w3.vec
path:  /media/ye/project2/exp/bilingual-induction/exp1/my-en/vecmap-output10/trg_super/word2vec_s100_mc2_w3.vec
path:  /media/ye/project2/exp/bilingual-induction/exp1/my-en/vecmap-output10/trg_super/word2vec_s200_mc2_w3.vec
EN:  /media/ye/project2/exp/bilingual-induction/exp1/my-en/vecmap-output10/src_super/word2vec_s200_mc2_w3.vec
WEL:  /media/ye/project2/exp/bilingual-induction/exp1/my-en/vecmap-output10/trg_super/word2vec_s200_mc2_w3.vec
=== CMD ===
python3 vecmap/map_embeddings.py --supervised /media/ye/project2/exp/bilingual-induction/exp1/my-en/word2vec-output10/train_dict.csv "/media/ye/project2/exp/bilingual-induction/exp1/my-en/vecmap-output10/src_super/word2vec_s200_mc2_w3.vec" "/media/ye/project2/exp/bilingual-induction/exp1/my-en/vecmap-output10/trg_super/word2vec_s200_mc2_w3.vec" "/media/ye/project2/exp/bilingual-induction/exp1/my-en/vecmap-output10/src_super/word2vec_s200_mc2_w3.vec_mapped.vec" "/media/ye/project2/exp/bilingual-induction/exp1/my-en/vecmap-output10/trg_super/word2vec_s200_mc2_w3.vec_mapped.vec"
WARNING: OOV dictionary entry (english - welsh)
WARNING: OOV dictionary entry (အရှုပ်တော်ပုံ - scandalmongering)
WARNING: OOV dictionary entry (မသန်စွမ်း - disenable)
WARNING: OOV dictionary entry (အလွန့်အလွန် - deviously)
WARNING: OOV dictionary entry (ခဲတံ - pennon)
WARNING: OOV dictionary entry (ကစားသူ - playgoer)
WARNING: OOV dictionary entry (အူဝဲ - howlingly)
WARNING: OOV dictionary entry (ဆိုးဆိုးရွားရွား - odiously)
WARNING: OOV dictionary entry (ပါးစပ် - mouthpart)
WARNING: OOV dictionary entry (ပါးရိုး - jag)
WARNING: OOV dictionary entry (သတ်မှတ်ချက် - stipel)
WARNING: OOV dictionary entry (နာရီ - stopclock)
WARNING: OOV dictionary entry (ဆောင်းရာသီ - winterize)
WARNING: OOV dictionary entry (ခိုးဝှက် - burglarize)
WARNING: OOV dictionary entry (လေးထောင့် - quadrivalent)
WARNING: OOV dictionary entry (အရောင်ဖျော့ - paleface)
WARNING: OOV dictionary entry (တော - wilde)
WARNING: OOV dictionary entry (ကျွမ်းကျင်မှု - professionalisation)
WARNING: OOV dictionary entry (သံပုရာသီး - limeade)
WARNING: OOV dictionary entry (ဓာတ်မှန် - heliograph)
WARNING: OOV dictionary entry (လက်လုပ် - handwrought)
WARNING: OOV dictionary entry (အိမ်သာ - toilette)
WARNING: OOV dictionary entry (နောက်ဆုံး - lattermost)
WARNING: OOV dictionary entry (သဲသဲမဲမဲ - unfrock)
WARNING: OOV dictionary entry (ကန်ပေါင် - embank)
WARNING: OOV dictionary entry (မီးတောက် - incandesce)
WARNING: OOV dictionary entry (ချစ်သူ - dearie)
WARNING: OOV dictionary entry (အလှူရှင် - donator)
WARNING: OOV dictionary entry (ကြောက်စရာ - scarer)
WARNING: OOV dictionary entry (ရွက်လှေ - yachtswoman)
WARNING: OOV dictionary entry (တွစ်တာ - twitcher)
WARNING: OOV dictionary entry (အနောက်တောင် - southwester)
WARNING: OOV dictionary entry (လူမိုက် - bumf)
WARNING: OOV dictionary entry (ချိပ် - lac)
WARNING: OOV dictionary entry (ပြပွဲ - exhibitive)
WARNING: OOV dictionary entry (လက်ခံသူ - acceptant)
WARNING: OOV dictionary entry (ချန်ပီယံ - champaign)
WARNING: OOV dictionary entry (ညီညွတ်ခြင်း - unconformity)
WARNING: OOV dictionary entry (ရာသီဥတု - weatherly)
WARNING: OOV dictionary entry (အရွက် - leafage)
WARNING: OOV dictionary entry (နွေရာသီ - summersault)
WARNING: OOV dictionary entry (ရွံ့ရှာ - vixenish)
WARNING: OOV dictionary entry (ပဲပုတ် - cowpea)
WARNING: OOV dictionary entry (ညစာ - truncheon)
WARNING: OOV dictionary entry (ဥရောပ - europium)
WARNING: OOV dictionary entry (အဖွားအို - grandmamma)
WARNING: OOV dictionary entry (ဇိုး - swiftlet)
WARNING: OOV dictionary entry (အထမ်းသမား - porterhouse)
WARNING: OOV dictionary entry (တရားခံ - ullage)
WARNING: OOV dictionary entry (တောင်ဘက် - southland)
WARNING: OOV dictionary entry (အကြောင်းအရင်း - causerie)
WARNING: OOV dictionary entry (အိမ်ထောင်ဖက် - matey)
WARNING: OOV dictionary entry (စားပွဲထိုး - deskman)
WARNING: OOV dictionary entry (အလေးချိန် - weigher)
WARNING: OOV dictionary entry (ပစ်ပေါက် - spick)
WARNING: OOV dictionary entry (သေနတ်သမား - rifleman)
WARNING: OOV dictionary entry (လက်အောက်ငယ်သား - subordinator)
WARNING: OOV dictionary entry (အဆုံး - endmost)
WARNING: OOV dictionary entry (ရူ - rouble)
WARNING: OOV dictionary entry (တရားဝင် - officinal)
WARNING: OOV dictionary entry (လေးပုံတစ်ပုံ - quartette)
WARNING: OOV dictionary entry (ကြမ်း - draff)
WARNING: OOV dictionary entry (ယာဉ်စီးခ - carfare)
WARNING: OOV dictionary entry (သရက်သီး - locknut)
WARNING: OOV dictionary entry (ရှားပါး - rarefy)
WARNING: OOV dictionary entry (ကျင့်ဝတ် - adduct)
WARNING: OOV dictionary entry (အတားအဆီး - obstructiveness)
WARNING: OOV dictionary entry (ပုံပျက်ပန်းပျက် - distortedly)
WARNING: OOV dictionary entry (ကော့ - cox)
WARNING: OOV dictionary entry (ထိထိရောက်ရောက် - effervesce)
WARNING: OOV dictionary entry (ကြောင်ကလေး - kittenish)
WARNING: OOV dictionary entry (အလုပ်အကိုင် - jobbery)
WARNING: OOV dictionary entry (ဟဲဟဲ - heehaw)
WARNING: OOV dictionary entry (ဝန်ဆောင်မှု - serviette)
WARNING: OOV dictionary entry (ခြင်းတောင်း - basketwork)
WARNING: OOV dictionary entry (ပြောင်းပြန် - revers)
WARNING: OOV dictionary entry (စကိတ်စီး - skedaddle)
WARNING: OOV dictionary entry (ဗေဒ - thanatology)
WARNING: OOV dictionary entry (ဘာဘီ - barbie)
WARNING: OOV dictionary entry (ဟောလိဝုဒ် - halliard)
WARNING: OOV dictionary entry (ပေးပါ - gimme)
WARNING: OOV dictionary entry (အိမ်မြှောင် - lurcher)
WARNING: OOV dictionary entry (မယ်ဒလင် - mandolinist)
WARNING: OOV dictionary entry (ကုန်သွယ်ရေး - amerce)
WARNING: OOV dictionary entry (ဆိတ်သား - goatish)
WARNING: OOV dictionary entry (အပျိုစင် - maidenly)
WARNING: OOV dictionary entry (တောက်ပ - glower)
WARNING: OOV dictionary entry (ရှယ်ယာရှင် - shareowner)
WARNING: OOV dictionary entry (ရေဗက္ကာ - rebec)
WARNING: OOV dictionary entry (အလုပ်သင် - interne)
WARNING: OOV dictionary entry (ငါးရံ့ - sylph)
WARNING: OOV dictionary entry (သပ်သပ်ရပ်ရပ် - neaten)
WARNING: OOV dictionary entry (မာဂျရင်း - margarin)
WARNING: OOV dictionary entry (ပြဇာတ် - playsuit)
WARNING: OOV dictionary entry (တွန်းအား - impetuousness)
WARNING: OOV dictionary entry (အပြတ်အသတ် - landslip)
WARNING: OOV dictionary entry (အနီးဆုံး - nethermost)
WARNING: OOV dictionary entry (လူလိမ် - luff)
WARNING: OOV dictionary entry (ပိတုန်း - bumble)
WARNING: OOV dictionary entry (ဆွဲဆောင်မှု - engrossment)
WARNING: OOV dictionary entry (အမှား - mishear)
WARNING: OOV dictionary entry (ချစ်သား - fellah)
WARNING: OOV dictionary entry (ပြိုင်ပွဲဝင် - racegoer)
WARNING: OOV dictionary entry (လက်ရှိ - procumbent)
WARNING: OOV dictionary entry (ဝီရိယ - wiliness)
WARNING: OOV dictionary entry (ငါးပိ - pasteurise)
WARNING: OOV dictionary entry (ကော်မရှင်နာ - commissionaire)
WARNING: OOV dictionary entry (ခြေကျင်း - anklet)
WARNING: OOV dictionary entry (စာရေးဆရာ - clerisy)
WARNING: OOV dictionary entry (အိုး - uhu)
WARNING: OOV dictionary entry (မှုတ်ထုတ် - blowzy)
WARNING: OOV dictionary entry (အံ့မခန်း - umbrageous)
WARNING: OOV dictionary entry (ပိုးကောင် - poulterer)
WARNING: OOV dictionary entry (ငါးပိ - waspish)
WARNING: OOV dictionary entry (မျှော်လင့်ချက် - suppositious)
WARNING: OOV dictionary entry (အထီးကျန် - seclusive)
WARNING: OOV dictionary entry (သိသိသာသာ - viscously)
WARNING: OOV dictionary entry (ဆိတ်သား - goatsucker)
WARNING: OOV dictionary entry (အဖျား - feverfew)
WARNING: OOV dictionary entry (အရှိတရား - factitious)
WARNING: OOV dictionary entry (ဒီမိုကရေစီ - democratism)
WARNING: OOV dictionary entry (ပုဒ်ဖြတ် - punctilio)
WARNING: OOV dictionary entry (မျက်နှာ - tufaceous)
WARNING: OOV dictionary entry (ဆွဲတင် - pullup)
WARNING: OOV dictionary entry (မျက်နှာဖုံး - impanel)
WARNING: OOV dictionary entry (ရေကြောင်း - nautically)
WARNING: OOV dictionary entry (ပြင်းပြင်းထန်ထန် - vivaciously)
WARNING: OOV dictionary entry (ဝီရိယ - wistfulness)
WARNING: OOV dictionary entry (အမှတ်အသား - markedness)
WARNING: OOV dictionary entry (ကွဲကွဲပြားပြား - disunite)
WARNING: OOV dictionary entry (စာကြည့်တိုက် - pressroom)
WARNING: OOV dictionary entry (မုန်တိုင်း - stormer)
WARNING: OOV dictionary entry (တံခါးပေါက် - gateaux)
WARNING: OOV dictionary entry (ဝက်သား - muttonhead)
WARNING: OOV dictionary entry (မျက်ခုံးမွေး - middlebrow)
WARNING: OOV dictionary entry (ကျိန်ဆို - swearword)
WARNING: OOV dictionary entry (စားသုံးမှု - alimentation)
WARNING: OOV dictionary entry (စပျစ်သီး - grapey)
WARNING: OOV dictionary entry (မော်တော်ဆိုင်ကယ် - motorbus)
WARNING: OOV dictionary entry (လှော် - diddle)
WARNING: OOV dictionary entry (ကြက်ကင် - roister)
WARNING: OOV dictionary entry (ဆန့်ကျင် - contuse)
WARNING: OOV dictionary entry (ကျား - tigerish)
WARNING: OOV dictionary entry (ဂုဏ် - splendent)
WARNING: OOV dictionary entry (မချိတင်ကဲ - disconsolately)
WARNING: OOV dictionary entry (ရိုးတွင်းခြင်ဆီ - marrowbone)
WARNING: OOV dictionary entry (လက်ကမ်းစာစောင် - handbill)
WARNING: OOV dictionary entry (မကျေမနပ် - dissonantly)
WARNING: OOV dictionary entry (ဒေါင်လိုက် - vert)
WARNING: OOV dictionary entry (ဆီးအိမ် - pule)
WARNING: OOV dictionary entry (အကျည်းတန် - scummy)
WARNING: OOV dictionary entry (ရုပ်ရှင် - moviedom)
WARNING: OOV dictionary entry (တေးရေးဆရာ - melodist)
WARNING: OOV dictionary entry (အစွမ်းထက် - potful)
WARNING: OOV dictionary entry (အလွန်အကျွံ - oversteer)
WARNING: OOV dictionary entry (သိသိသာသာ - mawkishly)
WARNING: OOV dictionary entry (လုပ်ခ - wagerer)
WARNING: OOV dictionary entry (ခမ်းနား - magnific)
WARNING: OOV dictionary entry (ဒါပဲ - dah)
WARNING: OOV dictionary entry (အမြန်လမ်း - speedwalk)
WARNING: OOV dictionary entry (စပ်ကြား - spic)
WARNING: OOV dictionary entry (ကျောပိုးအိတ် - afterdeck)
WARNING: OOV dictionary entry (မျက်မမြင် - purblind)
WARNING: OOV dictionary entry (ရှေ့ဆောင် - vanguardist)
WARNING: OOV dictionary entry (ချိတ်ပိုး - hookworm)
WARNING: OOV dictionary entry (သိမ်းငှက် - falchion)
WARNING: OOV dictionary entry (ရယ် - faugh)
WARNING: OOV dictionary entry (ယဉ်ကျေးမှု - civilise)
WARNING: OOV dictionary entry (မသိမသာ - witlessly)
WARNING: OOV dictionary entry (အအေးခန်း - refrigerative)
WARNING: OOV dictionary entry (အပူပိုင်းဒေသ - tropism)
WARNING: OOV dictionary entry (သော့ခလောက် - bollocks)
WARNING: OOV dictionary entry (အားမာန် - vigorousness)
WARNING: OOV dictionary entry (ဥယျာဉ်ခြံ - gardenia)
WARNING: OOV dictionary entry (စစ်အစိုးရ - junto)
WARNING: OOV dictionary entry (အထိတ်တလန့် - carious)
WARNING: OOV dictionary entry (လုပ်ပိုင်ခွင့် - mandator)
WARNING: OOV dictionary entry (ခွက် - cupreous)
WARNING: OOV dictionary entry (အသံထွက် - pronunciamento)
WARNING: OOV dictionary entry (မင်္ဂလာဆောင် - wedgelike)
WARNING: OOV dictionary entry (နေရောင်ခြည် - solarize)
WARNING: OOV dictionary entry (အိုကေ - och)
WARNING: OOV dictionary entry (ရောဂါဗေဒ - pedology)
WARNING: OOV dictionary entry (ဌာနခွဲ - compartmentalise)
WARNING: OOV dictionary entry (ဒေဝီ - deva)
WARNING: OOV dictionary entry (နက်ပကျွန်း - neptune)
WARNING: OOV dictionary entry (တရကြမ်း - turbulently)
WARNING: OOV dictionary entry (စိတ်ပညာရှင် - mentalist)
WARNING: OOV dictionary entry (အရောင်တင် - palish)
WARNING: OOV dictionary entry (ကိတ်မုန့် - cakehole)
WARNING: OOV dictionary entry (မြောက်ဘက် - northcountry)
WARNING: OOV dictionary entry (ပန်း - floristry)
WARNING: OOV dictionary entry (ညှိနှိုင်းမှု - convenance)
WARNING: OOV dictionary entry (အနောက်ဘက် - westing)
WARNING: OOV dictionary entry (လုပ်သား - laborite)
WARNING: OOV dictionary entry (အပိုင်းပိုင်း - segmentally)
WARNING: OOV dictionary entry (ဂျီ - gie)
WARNING: OOV dictionary entry (တိတိကျကျ - punctiliously)
WARNING: OOV dictionary entry (ဟေ့ - ahoy)
WARNING: OOV dictionary entry (မိုးခြိမ်းသံ - thunderthighs)
WARNING: OOV dictionary entry (အလုပ်သမား - outworker)
WARNING: OOV dictionary entry (မက်ဒရစ် - madden)
WARNING: OOV dictionary entry (ရေနံဆီ - kerosine)
WARNING: OOV dictionary entry (ကုတင် - bedsit)
WARNING: OOV dictionary entry (ခေါင်းစွပ် - headstand)
WARNING: OOV dictionary entry (ပယ်ဖျက် - cancellate)
WARNING: OOV dictionary entry (ဥယျာဉ်မှူး - orchardist)
WARNING: OOV dictionary entry (ဒေလီယာ - dahlia)
WARNING: OOV dictionary entry (သကြားလုံး - candyfloss)
WARNING: OOV dictionary entry (ရထားထိန်း - trainman)
WARNING: OOV dictionary entry (မျက်မြင် - sightly)
WARNING: OOV dictionary entry (တိတ်တဆိတ် - crawly)
WARNING: OOV dictionary entry (ပေါင်းစပ် - compend)
WARNING: OOV dictionary entry (လွဲချော် - misspend)
WARNING: OOV dictionary entry (ပျက်ပြယ် - voidance)
WARNING: OOV dictionary entry (လက်နက်မဲ့ - unarm)
WARNING: OOV dictionary entry (ဆက်တိုက် - rowdily)
WARNING: OOV dictionary entry (ကြိတ်စက် - lathing)
WARNING: OOV dictionary entry (တီးဝိုင်း - bandsman)
WARNING: OOV dictionary entry (သတ်မှတ်ချက် - stipule)
WARNING: OOV dictionary entry (သုံးကြိမ် - trifocal)
WARNING: OOV dictionary entry (ရောနှော - blench)
WARNING: OOV dictionary entry (ဆေးရည် - potation)
WARNING: OOV dictionary entry (နား - earing)
WARNING: OOV dictionary entry (မသိ - unbeknown)
WARNING: OOV dictionary entry (ကလဲ့စားချေ - venge)
WARNING: OOV dictionary entry (လေပြည် - zephyr)
WARNING: OOV dictionary entry (အမြတ်အစွန်း - profiterole)
WARNING: OOV dictionary entry (တာရာ - tarsus)
WARNING: OOV dictionary entry (ဆရာ - overmaster)
WARNING: OOV dictionary entry (မကျေမနပ် - disgruntle)
WARNING: OOV dictionary entry (ဆောင်ပုဒ် - blotto)
WARNING: OOV dictionary entry (ခွေးသား - dogmeat)
WARNING: OOV dictionary entry (ခုန် - jounce)
WARNING: OOV dictionary entry (ပင်လယ်လှိုင်း - wassail)
WARNING: OOV dictionary entry (လမ်းပန်းဆက်သွယ်ရေး - roadability)
WARNING: OOV dictionary entry (ပညာရေး - educability)
WARNING: OOV dictionary entry (ခေါင်းစီး - towhead)
WARNING: OOV dictionary entry (အမိန့် - delict)
WARNING: OOV dictionary entry (ခလုတ် - keypunch)
WARNING: OOV dictionary entry (အရေးမပါ - quincuncial)
WARNING: OOV dictionary entry (ကူးစက်ရောဂါ - epidiascope)
WARNING: OOV dictionary entry (ခေါင်းစွပ် - headpin)
WARNING: OOV dictionary entry (ဘီလူး - ogress)
WARNING: OOV dictionary entry (အောက်ခြေ - frump)
WARNING: OOV dictionary entry (အိမ်နီးချင်း - weighbridge)
WARNING: OOV dictionary entry (ကျောင်းဆရာမ - schoolmistress)
WARNING: OOV dictionary entry (တရားခံ - vindicatory)
WARNING: OOV dictionary entry (ပြတ်ပြတ်သားသား - indiscrete)
WARNING: OOV dictionary entry (သံလမ်း - railroader)
WARNING: OOV dictionary entry (ဟာဂျီ - hajji)
WARNING: OOV dictionary entry (အဇာတသတ် - patricidal)
WARNING: OOV dictionary entry (ပြင်းပြင်းထန်ထန် - peevishly)
WARNING: OOV dictionary entry (သတ္တု - metalled)
WARNING: OOV dictionary entry (သေတ္တာ - boxroom)
WARNING: OOV dictionary entry (ဆီးအိမ် - saccule)
WARNING: OOV dictionary entry (ကမ်းရိုးတန်း - coastland)
WARNING: OOV dictionary entry (ပန်းပွင့် - flowerer)
WARNING: OOV dictionary entry (အားနည်းချက် - vulnerary)
WARNING: OOV dictionary entry (ထိုသို့ - thitherto)
WARNING: OOV dictionary entry (ပို - soarer)
WARNING: OOV dictionary entry (လိပ်စာ - addresser)
WARNING: OOV dictionary entry (ငါးခူ - filefish)
WARNING: OOV dictionary entry (နိယာမ - intinction)
WARNING: OOV dictionary entry (ကြမ်းပြင် - vulpine)
WARNING: OOV dictionary entry (ပြဇာတ် - playact)
WARNING: OOV dictionary entry (ခြံစောင့် - yardmaster)
WARNING: OOV dictionary entry (အိမ်ရှင် - hostler)
WARNING: OOV dictionary entry (အဆမတန် - overweigh)
WARNING: OOV dictionary entry (အနောက်မြောက် - northwester)
WARNING: OOV dictionary entry (မပြေမလည် - unsmooth)
WARNING: OOV dictionary entry (အကြောင်းပြချက် - ratiocinator)
WARNING: OOV dictionary entry (ခေါင်းလိမ်းဆီ - pomade)
WARNING: OOV dictionary entry (ပေါ့ပေါ့တန်တန် - flashily)
WARNING: OOV dictionary entry (အမှန် - veridical)
WARNING: OOV dictionary entry (နေထိုင်မှု - inhabitancy)
WARNING: OOV dictionary entry (မှို - moult)
WARNING: OOV dictionary entry (နှင်းပေါက် - snowcap)
WARNING: OOV dictionary entry (ရှပ်အင်္ကျီ - shirtwaist)
WARNING: OOV dictionary entry (ရောင်ပြန် - reflectiveness)
WARNING: OOV dictionary entry (ဒေါသစိတ် - ruefulness)
WARNING: OOV dictionary entry (ရုပ်ကလာပ် - cadaverous)
WARNING: OOV dictionary entry (ရေချိုးခန်း - showery)
WARNING: OOV dictionary entry (အသေးစား - miniaturise)
WARNING: OOV dictionary entry (ရည်ရွယ်ချက် - intendance)
WARNING: OOV dictionary entry (အစွယ် - yaws)
WARNING: OOV dictionary entry (ဖြိုဖျက် - dissimilate)
WARNING: OOV dictionary entry (ဂျယ်လီ - geld)
WARNING: OOV dictionary entry (တယ်လီနော - telly)
WARNING: OOV dictionary entry (ပညာရှိ - wiseacre)
WARNING: OOV dictionary entry (မီးခွက် - chandlery)
WARNING: OOV dictionary entry (သဘာဝကျကျ - naturalise)
WARNING: OOV dictionary entry (သတင်းစာဆရာ - newspaperwoman)
WARNING: OOV dictionary entry (ရယ်စရာ - funniness)
WARNING: OOV dictionary entry (အနုပညာသမား - artillerist)
WARNING: OOV dictionary entry (စစ်ဆေးခြင်း - vetchling)
WARNING: OOV dictionary entry (ပါလက်စတိုင်း - palestinian)
WARNING: OOV dictionary entry (ချေဖျက် - detune)
WARNING: OOV dictionary entry (ကြက်လျှာ - pennate)
WARNING: OOV dictionary entry (ဆွတ်ဆွတ် - gloaming)
WARNING: OOV dictionary entry (မိုးကျရွှေကိုယ် - nonpareil)
WARNING: OOV dictionary entry (ကြိုတင်လက်မှတ် - pretermit)
WARNING: OOV dictionary entry (ညစာ - tinner)
WARNING: OOV dictionary entry (ဘက်ထရီ - cattery)
WARNING: OOV dictionary entry (အသစ်အဆန်း - novelize)
WARNING: OOV dictionary entry (သွေးပြန်ကြော - veinal)
WARNING: OOV dictionary entry (လူဆိုး - villainously)
WARNING: OOV dictionary entry (တစ်ဝက် - semiweekly)
WARNING: OOV dictionary entry (ပြူတင်းပေါက် - peeper)
WARNING: OOV dictionary entry (အခိုက်အတန့် - trice)
WARNING: OOV dictionary entry (အသစ် - newel)
WARNING: OOV dictionary entry (ခိုင်ခိုင် - groundsel)
WARNING: OOV dictionary entry (ညဘက် - nighty)
WARNING: OOV dictionary entry (တိုင်းတာ - measurer)
WARNING: OOV dictionary entry (ဝံပုလွေ - werwolf)
WARNING: OOV dictionary entry (အဖုံး - casement)
WARNING: OOV dictionary entry (ဆတ်ဆတ် - snaky)
WARNING: OOV dictionary entry (ပုတီးစိပ် - beadle)
WARNING: OOV dictionary entry (သက်သေ - provenience)
WARNING: OOV dictionary entry (အစာမကြေ - indigested)
WARNING: OOV dictionary entry (လက်တင် - latish)
WARNING: OOV dictionary entry (မှီခို - impend)
WARNING: OOV dictionary entry (တိုတို - foreshorten)
WARNING: OOV dictionary entry (စက်ခေါင်း - locomobile)
WARNING: OOV dictionary entry (တောက်ပ - brill)
WARNING: OOV dictionary entry (သိသိသာသာ - saliently)
WARNING: OOV dictionary entry (လေယာဉ်ပျံ - emplane)
WARNING: OOV dictionary entry (ကျော်ကြား - wame)
WARNING: OOV dictionary entry (လည်ပင်း - ringneck)
WARNING: OOV dictionary entry (အကျပ်အတည်း - trouper)
WARNING: OOV dictionary entry (အထူးပြု - particularise)
WARNING: OOV dictionary entry (ပြဇာတ်ရုံ - portiere)
WARNING: OOV dictionary entry (ဘေဘီ - babel)
WARNING: OOV dictionary entry (ညနေခင်း - evenfall)
WARNING: OOV dictionary entry (ဖန်ခွက် - glassful)
WARNING: OOV dictionary entry (ကျေးလက် - fustic)
WARNING: OOV dictionary entry (အနီးကပ် - appose)
WARNING: OOV dictionary entry (ဘုန်းကြီးကျောင်း - monasterial)
WARNING: OOV dictionary entry (သမားရိုးကျ - conventionalize)
WARNING: OOV dictionary entry (လက်နက် - weaponeer)
WARNING: OOV dictionary entry (ဆောင်းရာသီ - wowser)
WARNING: OOV dictionary entry (နံရံကပ် - wallower)
WARNING: OOV dictionary entry (ပျော်ရွှင်မှု - merriness)
WARNING: OOV dictionary entry (ဓာတ်သတ္တု - mineralogically)
WARNING: OOV dictionary entry (ဘာဘူ - baboo)
WARNING: OOV dictionary entry (အိပ်ရာခင်း - bedpost)
WARNING: OOV dictionary entry (အမျိုးအစား - assort)
WARNING: OOV dictionary entry (ရိုးရှင်း - simp)
WARNING: OOV dictionary entry (စာတန်းထိုး - castellated)
WARNING: OOV dictionary entry (နေ့စေ့လစေ့ - parturient)
WARNING: OOV dictionary entry (ရန်ပွဲ - outre)
WARNING: OOV dictionary entry (မိနစ် - minuend)
WARNING: OOV dictionary entry (ပညာရှိ - witted)
WARNING: OOV dictionary entry (ရံခါ - periphrastically)
WARNING: OOV dictionary entry (လက်သည်း - palmate)
WARNING: OOV dictionary entry (အပ်ငွေ - deposal)
WARNING: OOV dictionary entry (အနည်းငယ် - scantly)
WARNING: OOV dictionary entry (နှစ်ထပ် - quadrantal)
WARNING: OOV dictionary entry (စုရုံး - ingather)
WARNING: OOV dictionary entry (မသိမသာ - uncourtly)
WARNING: OOV dictionary entry (ရက်တို - rackety)
WARNING: OOV dictionary entry (မြေပြင် - groundling)
WARNING: OOV dictionary entry (ငိုကြွေးသံ - weeper)
WARNING: OOV dictionary entry (မင်္ဂလာ - blether)
WARNING: OOV dictionary entry (အဆန်း - oddment)
WARNING: OOV dictionary entry (အိုကေ - oik)
WARNING: OOV dictionary entry (အဋ္ဌမ - absinth)
WARNING: OOV dictionary entry (ရာသီဥတု - weatherworn)
WARNING: OOV dictionary entry (အပိုင်းပိုင်း - sectionally)
WARNING: OOV dictionary entry (အဆင်မပြေ - wady)
WARNING: OOV dictionary entry (တဝဲလည်လည် - lingeringly)
WARNING: OOV dictionary entry (အနီးဆုံး - sternmost)
WARNING: OOV dictionary entry (ခေါင်းစွပ် - headcase)
WARNING: OOV dictionary entry (ပေါင်းစပ် - collimate)
WARNING: OOV dictionary entry (မြောက်ဘက် - northing)
WARNING: OOV dictionary entry (အနောက်တိုင်း - wester)
WARNING: OOV dictionary entry (အနောက်ဘက် - hindquarter)
WARNING: OOV dictionary entry (ဖရန့် - francium)
WARNING: OOV dictionary entry (သန်းကြွယ်သူဌေး - millionairess)
WARNING: OOV dictionary entry (ဝါဒ - demist)
WARNING: OOV dictionary entry (အဆင့် - leveller)
WARNING: OOV dictionary entry (လူသတ်မှု - murderousness)
WARNING: OOV dictionary entry (မူဆလင် - musjid)
WARNING: OOV dictionary entry (ရေမှုတ် - spathe)
WARNING: OOV dictionary entry (ကောင်းစွာ - wally)
WARNING: OOV dictionary entry (တွန်းကန် - propellent)
WARNING: OOV dictionary entry (ကောလိပ် - collegian)
WARNING: OOV dictionary entry (ရည်ရွယ်ချက် - objectiveness)
WARNING: OOV dictionary entry (မိုးကြိုးပစ် - thunderhead)
WARNING: OOV dictionary entry (ဝက်သား - porker)
WARNING: OOV dictionary entry (အဟန့်အတား - determent)
WARNING: OOV dictionary entry (အုတ်ခဲ - briquette)
WARNING: OOV dictionary entry (လူငယ် - juvenilia)
WARNING: OOV dictionary entry (ရေစုပ်စက် - drainer)
WARNING: OOV dictionary entry (ဗိုက်နာ - stomache)
WARNING: OOV dictionary entry (ဒယ်အိုး - reddle)
WARNING: OOV dictionary entry (အလွန်အကျွံ - overexpand)
WARNING: OOV dictionary entry (သင်္ဘောသား - shipman)
WARNING: OOV dictionary entry (မီးကျောက် - firestone)
WARNING: OOV dictionary entry (ချီးကျူး - felicitate)
WARNING: OOV dictionary entry (စာရေး - clerkly)
WARNING: OOV dictionary entry (ဘီယာ - beery)
WARNING: OOV dictionary entry (လည်စည်း - necklet)
WARNING: OOV dictionary entry (နိဂုံးချုပ် - finical)
WARNING: OOV dictionary entry (လှော်ခတ် - unsaddle)
WARNING: OOV dictionary entry (ဆေးပညာ - medico)
WARNING: OOV dictionary entry (လူမျိုးစွဲ - nepotist)
WARNING: OOV dictionary entry (သုံးဆ - threepence)
WARNING: OOV dictionary entry (မြေသား - groundwell)
WARNING: OOV dictionary entry (လက် - handwoven)
WARNING: OOV dictionary entry (ပုရစ် - crick)
WARNING: OOV dictionary entry (ဂျင်မီ - jimmy)
WARNING: OOV dictionary entry (ကျေးလက်တောရွာ - rusticate)
WARNING: OOV dictionary entry (မေတ္တာ - metta)
WARNING: OOV dictionary entry (ဂျာနယ်လစ် - journalese)
WARNING: OOV dictionary entry (အချုပ်ခန်း - cellarage)
WARNING: OOV dictionary entry (အိုး - oof)
WARNING: OOV dictionary entry (မှီခို - impendent)
WARNING: OOV dictionary entry (စွန့်စားခန်း - adventurously)
WARNING: OOV dictionary entry (အသည်းနှလုံး - hardhearted)
WARNING: OOV dictionary entry (သမဂ္ဂ - unionise)
WARNING: OOV dictionary entry (ညှိနှိုင်းမှု - incoordination)
WARNING: OOV dictionary entry (အလျှော့မပေး - unyieldingly)
WARNING: OOV dictionary entry (လူသတ်သမား - maleficent)
WARNING: OOV dictionary entry (သင်္ဘောသား - seamer)
WARNING: OOV dictionary entry (ရန်ဖြစ် - quarreller)
WARNING: OOV dictionary entry (စုဝေး - convolve)
WARNING: OOV dictionary entry (သစ်ပင်ပန်းမန် - florae)
WARNING: OOV dictionary entry (သစ်ကြားသီး - nutmeat)
WARNING: OOV dictionary entry (မှုန်ဝါးဝါး - haziness)
WARNING: OOV dictionary entry (အတင်းအဖျင်း - gossipmonger)
WARNING: OOV dictionary entry (ညဝတ် - nightwear)
WARNING: OOV dictionary entry (သွက်သွက်လက်လက် - fugly)
WARNING: OOV dictionary entry (နိုဘယ်လ်ဆု - nobelium)
WARNING: OOV dictionary entry (ဒဏ်ခတ် - strick)
WARNING: OOV dictionary entry (စစ်အင်အား - militarise)
WARNING: OOV dictionary entry (တရားဝင် - officialese)
WARNING: OOV dictionary entry (ကြားဖြတ် - interstice)
WARNING: OOV dictionary entry (အလံတိုင် - flagellate)
WARNING: OOV dictionary entry (ဂိမ်း - gam)
WARNING: OOV dictionary entry (ရိုက် - whump)
WARNING: OOV dictionary entry (အနာ - ululation)
WARNING: OOV dictionary entry (မလှုပ်မယှက် - motionlessly)
WARNING: OOV dictionary entry (ပိုဒ် - stanzaic)
WARNING: OOV dictionary entry (ပါရီ - paretic)
WARNING: OOV dictionary entry (လက်ထောက် - bailor)
WARNING: OOV dictionary entry (အလှဆင် - ornamentally)
WARNING: OOV dictionary entry (လက်ကောက်ဝတ် - wristlock)
WARNING: OOV dictionary entry (ရာသီဥတု - weatherize)
WARNING: OOV dictionary entry (ကမ်းခြေ - coastward)
WARNING: OOV dictionary entry (တာဝါတိုင် - weir)
WARNING: OOV dictionary entry (နေထိုင်သူ - habitant)
WARNING: OOV dictionary entry (လောင်းကစား - gabble)
WARNING: OOV dictionary entry (ထိပ်တန်း - supernal)
WARNING: OOV dictionary entry (အရေးအသား - mottle)
WARNING: OOV dictionary entry (ဆင်ဆာ - censorial)
WARNING: OOV dictionary entry (သင်းခွေချပ် - pangolin)
WARNING: OOV dictionary entry (ရေအောက် - submerse)
WARNING: OOV dictionary entry (အလုပ် - jobby)
WARNING: OOV dictionary entry (အဘိုးအဘွား - grandpapa)
WARNING: OOV dictionary entry (ငါးဖမ်းသမား - fishwife)
WARNING: OOV dictionary entry (အေးအေးဆေးဆေး - relaxedly)
WARNING: OOV dictionary entry (ဒိုင်ခွက် - dicer)
WARNING: OOV dictionary entry (ကုန်စိမ်း - greengrocery)
WARNING: OOV dictionary entry (အစာ - feedstuff)
WARNING: OOV dictionary entry (သော့ခလောက် - picklock)
WARNING: OOV dictionary entry (အဇာတသတ် - patricide)
WARNING: OOV dictionary entry (အခမဲ့ - freeby)
WARNING: OOV dictionary entry (နောက်ကြောင်းပြန် - retroact)
WARNING: OOV dictionary entry (ဇာတိ - natality)
WARNING: OOV dictionary entry (လမ်းမကြီး - mainroad)
WARNING: OOV dictionary entry (တူးမြောင်း - canalize)
WARNING: OOV dictionary entry (ဂုဏ်သတင်း - prestissimo)
WARNING: OOV dictionary entry (နှင်တံ - whipstitch)
WARNING: OOV dictionary entry (ဆောင်းပါး - tonsorial)
WARNING: OOV dictionary entry (ကစားပွဲ - playgame)
WARNING: OOV dictionary entry (ဘေးတိုက် - sideward)
WARNING: OOV dictionary entry (အာကာသယာဉ် - aerosphere)
WARNING: OOV dictionary entry (ရှေးယခင် - antecede)
WARNING: OOV dictionary entry (ကျားမ - gendermerie)
WARNING: OOV dictionary entry (ဘာဂါ - burgle)
WARNING: OOV dictionary entry (မကျေမနပ် - indolently)
WARNING: OOV dictionary entry (လယ်သမား - fieldsman)
WARNING: OOV dictionary entry (စွယ် - tuskless)
WARNING: OOV dictionary entry (အီစတာ - easterner)
WARNING: OOV dictionary entry (တေးဂီတသံ - melodically)
WARNING: OOV dictionary entry (တင်ပါး - kecks)
WARNING: OOV dictionary entry (ဆေးစာ - prescript)
WARNING: OOV dictionary entry (တစ်ချိန်ချိန် - somewhen)
WARNING: OOV dictionary entry (အပြုအမူ - manneristic)
WARNING: OOV dictionary entry (ပေါင်းစည်း - agglutinate)
WARNING: OOV dictionary entry (လက်ဖက်ရည်ဆိုင် - teacake)
WARNING: OOV dictionary entry (ရင်ဘတ် - chesty)
WARNING: OOV dictionary entry (ပြင်းပြင်းထန်ထန် - vexingly)
WARNING: OOV dictionary entry (ကဗျာဆရာ - poetaster)
WARNING: OOV dictionary entry (တည်ဆောက်ရေး - outbuilding)
WARNING: OOV dictionary entry (အလင်းရောင် - illuminance)
WARNING: OOV dictionary entry (ကြောင် - cunny)
WARNING: OOV dictionary entry (ကြောက်စရာ - dreadfulness)
WARNING: OOV dictionary entry (ဇွန်း - spoony)
WARNING: OOV dictionary entry (သင်ရိုးညွှန်းတမ်း - curricle)
WARNING: OOV dictionary entry (ပြင်းပြင်းထန်ထန် - tussive)
WARNING: OOV dictionary entry (မိုးခြိမ်းသံ - thunderclap)
WARNING: OOV dictionary entry (စိုက်ပျိုးရေး - apiculture)
WARNING: OOV dictionary entry (နောက်ကျော - backsaw)
WARNING: OOV dictionary entry (တွန့်လိမ် - wriggler)
WARNING: OOV dictionary entry (မီးရထားတွဲ - waggon)
WARNING: OOV dictionary entry (တားမြစ်ချက် - tabour)
WARNING: OOV dictionary entry (သီးသန့် - reservedly)
WARNING: OOV dictionary entry (ကုန်လှောင်ရုံ - wareroom)
WARNING: OOV dictionary entry (စကားပြော - talky)
WARNING: OOV dictionary entry (အထိမ်းအမှတ် - memorialise)
WARNING: OOV dictionary entry (တော - queerness)
WARNING: OOV dictionary entry (ပျော်ရွှင်မှု - blissfulness)
WARNING: OOV dictionary entry (ဆန္ဒ - wishfulness)
WARNING: OOV dictionary entry (ကြွက်သား - muscularly)
WARNING: OOV dictionary entry (ရထား - carroty)
WARNING: OOV dictionary entry (ကျောက်ခဲ - whetstone)
WARNING: OOV dictionary entry (လေယာဉ် - aerodyne)
WARNING: OOV dictionary entry (ဂိုးသမား - goalmouth)
WARNING: OOV dictionary entry (အဝတ်လျှော်စက် - rasher)
WARNING: OOV dictionary entry (ဖျင်း - chaffer)
WARNING: OOV dictionary entry (ပညာရှိ - wiseman)
WARNING: OOV dictionary entry (မြန်နှုန်း - speeder)
WARNING: OOV dictionary entry (အင်တာနက် - inearth)
WARNING: OOV dictionary entry (ဖန်ခွက် - glasswork)
WARNING: OOV dictionary entry (ကေဒါ - cadge)
WARNING: OOV dictionary entry (ပြောင် - baldy)
WARNING: OOV dictionary entry (ပညာ - sapience)
WARNING: OOV dictionary entry (ဆေးဒန်း - orpiment)
WARNING: OOV dictionary entry (အစာအိမ် - stomachic)
WARNING: OOV dictionary entry (ရှားပါး - rarebit)
WARNING: OOV dictionary entry (ရောင်းသူ - repeller)
WARNING: OOV dictionary entry (အစေခံ - manservant)
WARNING: OOV dictionary entry (နွားသိုး - cowman)
WARNING: OOV dictionary entry (ဝတ်ဆံ - stamen)
WARNING: OOV dictionary entry (အပယ်ခံ - outcaste)
WARNING: OOV dictionary entry (မီးစက် - wickerwork)
WARNING: OOV dictionary entry (ဝိုးတိုးဝါးတား - hazily)
WARNING: OOV dictionary entry (လူသစ် - rooky)
WARNING: OOV dictionary entry (ဟာဂျီ - haji)
WARNING: OOV dictionary entry (မီလီမီတာ - millilitre)
WARNING: OOV dictionary entry (ငွေ့ - sapor)
WARNING: OOV dictionary entry (ပေါင်းစပ် - confabulate)
WARNING: OOV dictionary entry (ဖြတ်ထုတ် - cutup)
WARNING: OOV dictionary entry (ပတ်လည် - enwrap)
WARNING: OOV dictionary entry (အမှာစကား - gisting)
WARNING: OOV dictionary entry (အစေခံ - subserviently)
WARNING: OOV dictionary entry (လက်အောက်ခံ - subsocial)
WARNING: OOV dictionary entry (ဟုံ - cloy)
WARNING: OOV dictionary entry (လက်သုတ်ပုဝါ - napery)
WARNING: OOV dictionary entry (ထပ်ခါတလဲလဲ - reiterative)
WARNING: OOV dictionary entry (ပိုက်ဆံအိတ် - moneybag)
WARNING: OOV dictionary entry (ကြိုး - ropey)
WARNING: OOV dictionary entry (ကုက္ကုစ္စ - miserliness)
WARNING: OOV dictionary entry (လက်သည်း - nailer)
WARNING: OOV dictionary entry (အမှိုက်ပုံး - litterbug)
WARNING: OOV dictionary entry (ပေါ်ပေါက် - occident)
WARNING: OOV dictionary entry (မက်ထရစ် - metrication)
WARNING: OOV dictionary entry (ပူးပေါင်း - concertize)
WARNING: OOV dictionary entry (ပန်းရန် - plasterer)
WARNING: OOV dictionary entry (မိုးသံ - thuddingly)
WARNING: OOV dictionary entry (အလယ်အလတ် - midrib)
WARNING: OOV dictionary entry (ကစ် - kicky)
WARNING: OOV dictionary entry (အပြန်အလှန် - mutualize)
WARNING: OOV dictionary entry (ဓာတ်ဖို - alchemize)
WARNING: OOV dictionary entry (ရေချိုးကန် - washbasin)
WARNING: OOV dictionary entry (ပြိုင်ပွဲ - raceme)
WARNING: OOV dictionary entry (ထိထိမိမိ - mordantly)
WARNING: OOV dictionary entry (မည်သို့ပင်ဖြစ်စေ - anywise)
WARNING: OOV dictionary entry (ကြက်သမား - poultryman)
WARNING: OOV dictionary entry (မိုးကာ - rainwear)
WARNING: OOV dictionary entry (နှင်းပေါက် - snowdrop)
WARNING: OOV dictionary entry (ဂျာမန် - merman)
WARNING: OOV dictionary entry (အသာတကြည် - nebulously)
WARNING: OOV dictionary entry (ဝါတော် - vasa)
WARNING: OOV dictionary entry (အခက်အခဲ - confliction)
WARNING: OOV dictionary entry (နန်းတော် - vicennial)
WARNING: OOV dictionary entry (ချော့မော့ - sedately)
WARNING: OOV dictionary entry (ဘိလပ်မြေ - cementum)
WARNING: OOV dictionary entry (တူရိယာ - percuss)
WARNING: OOV dictionary entry (သဘောထား - tendance)
WARNING: OOV dictionary entry (ရမယ် - gotta)
WARNING: OOV dictionary entry (အလုပ်ရှင် - workwoman)
WARNING: OOV dictionary entry (ညည်းတွားသံ - whin)
WARNING: OOV dictionary entry (ဒေါသတကြီး - resentfully)
WARNING: OOV dictionary entry (အရှုပ်တော်ပုံ - scandalmonger)
WARNING: OOV dictionary entry (ဖျန်ဖြေ - mediative)
WARNING: OOV dictionary entry (ပန်းကုံး - wreathe)
WARNING: OOV dictionary entry (လက်ကောက် - bangle)
WARNING: OOV dictionary entry (အာဇာနည် - martyrize)
WARNING: OOV dictionary entry (သယ်ဆောင် - carryall)
WARNING: OOV dictionary entry (ညှပ်ဖိနပ် - flipflop)
WARNING: OOV dictionary entry (သေရည် - intoxicate)
WARNING: OOV dictionary entry (သားအိမ်ခေါင်း - cervine)
WARNING: OOV dictionary entry (သစ်သား - woodenly)
WARNING: OOV dictionary entry (ကြက်မောက် - shuttlecock)
WARNING: OOV dictionary entry (ခန္ဓာဗေဒ - anatomize)
WARNING: OOV dictionary entry (ကြမ်းပြင် - granger)
WARNING: OOV dictionary entry (ဝိုင် - wahine)
WARNING: OOV dictionary entry (အထွတ်အထိပ် - pinnace)
WARNING: OOV dictionary entry (ရှက်တယ် - shyster)
WARNING: OOV dictionary entry (ကြာပွတ် - whipper)
WARNING: OOV dictionary entry (အစောင့် - guardsman)
WARNING: OOV dictionary entry (တစ်နှစ် - anear)
WARNING: OOV dictionary entry (ဘေးတိုက် - sidepiece)
WARNING: OOV dictionary entry (ဝုန်းဒိုင်းကြဲ - boisterously)
WARNING: OOV dictionary entry (စုတ်တံ - stipe)
WARNING: OOV dictionary entry (မလှုပ်မယှက် - waggishly)
WARNING: OOV dictionary entry (ဝံသာနု - wain)
WARNING: OOV dictionary entry (ဖယောင်းတိုင် - candlewick)
WARNING: OOV dictionary entry (အာကာသယာဉ်မှူး - spacewoman)
WARNING: OOV dictionary entry (မျက်နှာဖြူ - whiteface)
WARNING: OOV dictionary entry (လက်ချောင်း - handspring)
WARNING: OOV dictionary entry (ကျောင်းနေဖက် - schoolmarmish)
WARNING: OOV dictionary entry (မြန်မာ - quicklime)
WARNING: OOV dictionary entry (အလုပ် - outwork)
WARNING: OOV dictionary entry (မျိုးစိတ် - inbreed)
WARNING: OOV dictionary entry (ရေမွှေး - perfuming)
WARNING: OOV dictionary entry (နေ့လည်စာ - luncheonette)
WARNING: OOV dictionary entry (အိပ်ရာ - bedhead)
WARNING: OOV dictionary entry (လုံခြုံမှု - securement)
WARNING: OOV dictionary entry (အောင်နိုင်သူ - victualer)
WARNING: OOV dictionary entry (အမှိုက်ပုံ - dreg)
WARNING: OOV dictionary entry (ဓမ္မ - ministerially)
WARNING: OOV dictionary entry (ခြေကျင်း - anklebone)
WARNING: OOV dictionary entry (ကုန်းမြင့် - highlander)
WARNING: OOV dictionary entry (ကုန်ကျစရိတ် - costar)
WARNING: OOV dictionary entry (နားစည် - eardrop)
WARNING: OOV dictionary entry (သုံးသူ - treater)
WARNING: OOV dictionary entry (ပိုးကောင် - bedbug)
WARNING: OOV dictionary entry (ဂရမ် - gramme)
WARNING: OOV dictionary entry (အခန်းကျယ် - roomer)
WARNING: OOV dictionary entry (ခရီး - itinerancy)
WARNING: OOV dictionary entry (အဝိုင်း - roundel)
WARNING: OOV dictionary entry (အခွင့်အလမ်း - opponency)
WARNING: OOV dictionary entry (ဟန်နာ - hahnium)
WARNING: OOV dictionary entry (ပါကေး - parquetry)
WARNING: OOV dictionary entry (မျက်တောင် - glim)
WARNING: OOV dictionary entry (စေတနာရှင် - voluntaryist)
WARNING: OOV dictionary entry (သိုးမွေး - woolgrowing)
WARNING: OOV dictionary entry (မီလီမီတာ - millesimal)
WARNING: OOV dictionary entry (အပင် - plantigrade)
WARNING: OOV dictionary entry (တိုးတက်မှု - spence)
WARNING: OOV dictionary entry (လွတ်လွတ်လပ်လပ် - unblushingly)
WARNING: OOV dictionary entry (ချယ်ရီ - charlady)
WARNING: OOV dictionary entry (ဆံပင်ညှပ် - haberdashery)
WARNING: OOV dictionary entry (စကားပြန် - backsword)
WARNING: OOV dictionary entry (တံတွေး - snit)
WARNING: OOV dictionary entry (တန်းတူ - rorqual)
WARNING: OOV dictionary entry (သစ်တော - afforest)
WARNING: OOV dictionary entry (မျက်မမြင် - blindside)
WARNING: OOV dictionary entry (မြေပဲ - earthnut)
WARNING: OOV dictionary entry (သွေးလွန်တုပ်ကွေး - extravasate)
WARNING: OOV dictionary entry (စိတ်ကူးယဉ်သမား - fictionist)
WARNING: OOV dictionary entry (နွေရာသီ - summerset)
WARNING: OOV dictionary entry (ဧည့်သည် - visitant)
WARNING: OOV dictionary entry (လေယာဉ်ပျံ - enplane)
WARNING: OOV dictionary entry (အသံထွက် - intonate)
WARNING: OOV dictionary entry (ရောင်းသူ - vendace)
WARNING: OOV dictionary entry (ကြိုးမျှင် - strandline)
WARNING: OOV dictionary entry (အပြန်အလှန် - mutationally)
WARNING: OOV dictionary entry (ဝတ္ထုတို - novelette)
WARNING: OOV dictionary entry (အဆင့်အတန်း - regality)
WARNING: OOV dictionary entry (ခေါ် - sumach)
WARNING: OOV dictionary entry (ရုန်းရင်းဆန်ခတ် - wamble)
WARNING: OOV dictionary entry (ကိုယ်တွေ့ - unhand)
WARNING: OOV dictionary entry (အလုပ်သင် - internee)
WARNING: OOV dictionary entry (ကြည့်ရှု - spectate)
WARNING: OOV dictionary entry (တံခါး - gateau)
WARNING: OOV dictionary entry (မြောက်ဘက် - northwardly)
WARNING: OOV dictionary entry (အဆက်မပြတ် - continuant)
WARNING: OOV dictionary entry (အလွန်အကျွံ - overset)
WARNING: OOV dictionary entry (အရှိန်အဟုန် - momentariness)
WARNING: OOV dictionary entry (သွေးလွန်တုပ်ကွေး - haemophiliac)
WARNING: OOV dictionary entry (လည်စည်း - manege)
WARNING: OOV dictionary entry (အီလက်ထရောနစ် - electone)
WARNING: OOV dictionary entry (အပြုံး - smirch)
WARNING: OOV dictionary entry (သမားရိုးကျ - conventionalise)
WARNING: OOV dictionary entry (အလယ်အလတ် - middleweight)
WARNING: OOV dictionary entry (ဘုရားရှိခိုးကျောင်း - churchwoman)
WARNING: OOV dictionary entry (ပန်းပုဆရာ - sculptress)
WARNING: OOV dictionary entry (စစ်မှုထမ်း - enlistee)
WARNING: OOV dictionary entry (လုံခြုံမှု - safeness)
WARNING: OOV dictionary entry (ရုပ်ပျက်ဆင်းပျက် - disfiguration)
WARNING: OOV dictionary entry (ကျောင်းနေဖက် - schoolfellow)
WARNING: OOV dictionary entry (ကျောက်တောင် - cliffy)
WARNING: OOV dictionary entry (ညနေ - yesternight)
WARNING: OOV dictionary entry (တော်မီ - tommy)
WARNING: OOV dictionary entry (အဆီပြန် - fatback)
WARNING: OOV dictionary entry (ဘုရားရေ - golosh)
WARNING: OOV dictionary entry (အလယ်ခေတ် - medievally)
WARNING: OOV dictionary entry (ဟဲလို - welch)
WARNING: OOV dictionary entry (အသေအချာ - martially)
WARNING: OOV dictionary entry (အိမ်နောက်ဖေး - backstairs)
WARNING: OOV dictionary entry (နောက်ကျော - thill)
WARNING: OOV dictionary entry (အာကာသယာဉ်မှူး - aeronaut)
WARNING: OOV dictionary entry (မက်ထရစ် - metricate)
WARNING: OOV dictionary entry (သစ်သား - woodpile)
WARNING: OOV dictionary entry (ကြီးကြီးမားမား - bulgy)
WARNING: OOV dictionary entry (ကျောက်မျက်ရတနာ - gemination)
WARNING: OOV dictionary entry (တန်ပြန် - counterpane)
WARNING: OOV dictionary entry (အပြင်အဆင် - outface)
WARNING: OOV dictionary entry (အရသာ - savoriness)
WARNING: OOV dictionary entry (တောင်ပံ - wingover)
WARNING: OOV dictionary entry (အမြန်နှုန်း - quickset)
WARNING: OOV dictionary entry (လူမှုဆက်ဆံရေး - sociality)
WARNING: OOV dictionary entry (ပေါရာဏ - obsoleteness)
WARNING: OOV dictionary entry (တီးတိုး - whispery)
WARNING: OOV dictionary entry (လက်စွပ် - armlet)
WARNING: OOV dictionary entry (ပုဆိုး - sateen)
WARNING: OOV dictionary entry (ကျွဲ - moated)
WARNING: OOV dictionary entry (လူဆိုး - villous)
WARNING: OOV dictionary entry (သုံးဆ - thievish)
WARNING: OOV dictionary entry (ဟန်နီ - hinny)
WARNING: OOV dictionary entry (လူမှုအဖွဲ့အစည်း - socage)
WARNING: OOV dictionary entry (ထိပ်တန်း - topmast)
WARNING: OOV dictionary entry (ကျောထောက်နောက်ခံ - hunchbacked)
WARNING: OOV dictionary entry (သတင်းအချက်အလက် - informativeness)
WARNING: OOV dictionary entry (ပြင်သစ် - frenchy)
WARNING: OOV dictionary entry (သကြားသီး - sugarplum)
WARNING: OOV dictionary entry (မလုံမခြုံ - insobriety)
WARNING: OOV dictionary entry (ပိုးတုံးလုံး - pupa)
WARNING: OOV dictionary entry (မီးသတ်သမား - fireguard)
WARNING: OOV dictionary entry (သွားရေးလာရေး - commutate)
WARNING: OOV dictionary entry (ထွက်ပြေး - runabout)
WARNING: OOV dictionary entry (အံ့ဖွယ် - miraculousness)
WARNING: OOV dictionary entry (အားလပ်ရက် - vacationist)
WARNING: OOV dictionary entry (နှုန်းထား - rateable)
WARNING: OOV dictionary entry (ပိုးစုန်းကြူး - mayfly)
WARNING: OOV dictionary entry (အောင်မြင်မှု - acclivity)
WARNING: OOV dictionary entry (သင်္ဘောသား - marrier)
WARNING: OOV dictionary entry (ဆွဲကြိုး - pend)
WARNING: OOV dictionary entry (ကွာတားဖိုင်နယ် - quarterfinalist)
WARNING: OOV dictionary entry (စုစုပေါင်း - totalize)
WARNING: OOV dictionary entry (လိမ့်မည် - gonna)
WARNING: OOV dictionary entry (ဥပမာ - egad)
WARNING: OOV dictionary entry (လှုပ်ရှားမှု - motional)
WARNING: OOV dictionary entry (မိုးကာအင်္ကျီ - mackintosh)
WARNING: OOV dictionary entry (စွယ်တော် - stupe)
WARNING: OOV dictionary entry (ကတိ - promisee)
WARNING: OOV dictionary entry (လက်သမား - freemasonary)
WARNING: OOV dictionary entry (ပေါင်ချိန် - poundage)
WARNING: OOV dictionary entry (ရေအား - waterpower)
WARNING: OOV dictionary entry (စတိုင် - stymy)
WARNING: OOV dictionary entry (မူးယစ်ဆေး - druggie)
WARNING: OOV dictionary entry (ကြော်ငြာ - advertent)
WARNING: OOV dictionary entry (ခရမ်းနုရောင် - wisteria)
WARNING: OOV dictionary entry (စိတ်ကူးယဉ် - fict)
WARNING: OOV dictionary entry (သရက်သီး - mangosteen)
WARNING: OOV dictionary entry (အမျိုးမျိုး - varietally)
WARNING: OOV dictionary entry (ဘီလီ - billie)
WARNING: OOV dictionary entry (ဖရိုဖရဲ - shamble)
WARNING: OOV dictionary entry (သင်ရိုးညွှန်းတမ်း - syllabary)
WARNING: OOV dictionary entry (အရိုးစု - skeletonize)
WARNING: OOV dictionary entry (မျက်မှန် - eyeshade)
WARNING: OOV dictionary entry (ပါးစပ် - mouthy)
WARNING: OOV dictionary entry (အင်ပါယာ - empyrean)
WARNING: OOV dictionary entry (တေးသံ - sonance)
WARNING: OOV dictionary entry (ကြင်နာမှု - courteousness)
WARNING: OOV dictionary entry (သန်း - jillion)
WARNING: OOV dictionary entry (တံခွန် - moorage)
WARNING: OOV dictionary entry (နွယ်ပင် - bindweed)
WARNING: OOV dictionary entry (ပြန်ပေး - restitute)
WARNING: OOV dictionary entry (ရှောင်ရှား - evanesce)
WARNING: OOV dictionary entry (ပျော်ရွှင်စရာ - merrythought)
WARNING: OOV dictionary entry (မော်နီတာ - monitorship)
WARNING: OOV dictionary entry (လောင်းလှေ - stakeboat)
WARNING: OOV dictionary entry (အရောင်တင် - colorant)
WARNING: OOV dictionary entry (အိမ်မြှောင် - oarlock)
WARNING: OOV dictionary entry (စီမံခန့်ခွဲ - menage)
WARNING: OOV dictionary entry (မောင်းမ - unman)
WARNING: OOV dictionary entry (ပျော့ဆေး - milden)
WARNING: OOV dictionary entry (အနီကတ် - redcap)
WARNING: OOV dictionary entry (ကီလိုဂရမ် - kilogramme)
WARNING: OOV dictionary entry (ဘေးစောင်း - sideslip)
WARNING: OOV dictionary entry (အပေးအယူ - embrocation)
WARNING: OOV dictionary entry (လယ်ယာ - farness)
WARNING: OOV dictionary entry (အိုး - uhf)
WARNING: OOV dictionary entry (ကျောင်းသား - pupillage)
WARNING: OOV dictionary entry (စီးကရက် - cigaret)
WARNING: OOV dictionary entry (ပွဲတော် - aestival)
WARNING: OOV dictionary entry (စည်းမျဉ်းစည်းကမ်း - regulus)
WARNING: OOV dictionary entry (စကား - headword)
WARNING: OOV dictionary entry (မီလီမီတာ - milliampere)
WARNING: OOV dictionary entry (အမွေအနှစ် - heirdom)
WARNING: OOV dictionary entry (ပိုးစာ - mullock)
WARNING: OOV dictionary entry (လက်သမား - pryer)
WARNING: OOV dictionary entry (တောင်ပိုင်းသား - southlander)
WARNING: OOV dictionary entry (အမွှေးတိုင် - joss)
WARNING: OOV dictionary entry (ကိုးကား - quoter)
WARNING: OOV dictionary entry (ဆူပူ - braw)
WARNING: OOV dictionary entry (သဘာဝတရား - naturism)
WARNING: OOV dictionary entry (ရေသူမ - mermen)
WARNING: OOV dictionary entry (အောင်နိုင်သူ - vanquisher)
WARNING: OOV dictionary entry (ခြေကျင်း - footbath)
WARNING: OOV dictionary entry (စိုးရိမ်စိတ် - apprehensiveness)
WARNING: OOV dictionary entry (ဆံပင်ရှည် - longhair)
WARNING: OOV dictionary entry (နုတ် - subtracter)
WARNING: OOV dictionary entry (သစ်သားအိမ် - woodhouse)
WARNING: OOV dictionary entry (နောက်ပိုင်း - afters)
WARNING: OOV dictionary entry (သေနတ်သံ - gunlock)
WARNING: OOV dictionary entry (စင်တီမီတာ - centesimal)
WARNING: OOV dictionary entry (ပုစဉ်း - stonefly)
WARNING: OOV dictionary entry (အညှာ - stalky)
WARNING: OOV dictionary entry (လက်ပတ် - wristlet)
WARNING: OOV dictionary entry (အလွန်အကျွံ - overact)
WARNING: OOV dictionary entry (ကျောက်ဆူး - anchoress)
WARNING: OOV dictionary entry (မဟုတ်ပါ - nonsuch)
WARNING: OOV dictionary entry (အလုံးစုံ - overarch)
WARNING: OOV dictionary entry (ဒေါသတကြီး - irritatedly)
WARNING: OOV dictionary entry (သရုပ်ဖော် - scenarist)
WARNING: OOV dictionary entry (စားပွဲခုံ - deskill)
WARNING: OOV dictionary entry (ခါးစည်း - waistcloth)
WARNING: OOV dictionary entry (လှံတံ - spewer)
WARNING: OOV dictionary entry (ကျောက်တုံး - stonechat)
WARNING: OOV dictionary entry (ဖြည့်စွက် - suppurate)
WARNING: OOV dictionary entry (သံယောဇဉ် - entwine)
WARNING: OOV dictionary entry (အာမခံ - ensilage)
WARNING: OOV dictionary entry (ရေချိုးခန်း - bathysphere)
WARNING: OOV dictionary entry (မင်းဆက် - dynast)
WARNING: OOV dictionary entry (တိုးဂိတ် - tollhouse)
WARNING: OOV dictionary entry (ပန်းခြံ - parky)
WARNING: OOV dictionary entry (ခက်ခက်ခဲခဲ - heddle)
WARNING: OOV dictionary entry (အကွာအဝေး - outdistance)
WARNING: OOV dictionary entry (နေထိုင်မှု - habiliment)
WARNING: OOV dictionary entry (အညှော် - pungency)
WARNING: OOV dictionary entry (သေခြင်းတရား - deadliness)
WARNING: OOV dictionary entry (အိပ်ယာခင်း - bedsitter)
WARNING: OOV dictionary entry (အစုလိုက် - bunchy)
WARNING: OOV dictionary entry (ဈေးဝယ် - pilchard)
WARNING: OOV dictionary entry (တူးမြောင်း - canalise)
WARNING: OOV dictionary entry (ပေါင်းပင် - weediness)
WARNING: OOV dictionary entry (သတင်းမှား - misinformer)
WARNING: OOV dictionary entry (ဓားရှည် - stabile)
WARNING: OOV dictionary entry (ရွရွ - dashingly)
WARNING: OOV dictionary entry (အဖျက်သမား - vesicant)
WARNING: OOV dictionary entry (ကွဲပြားမှု - viceregency)
WARNING: OOV dictionary entry (စောင်း - slantwise)
WARNING: OOV dictionary entry (ရောဂါဘယ - morbidness)
WARNING: OOV dictionary entry (တီဘီ - tubercule)
WARNING: OOV dictionary entry (အကူအညီ - helot)
WARNING: OOV dictionary entry (ကျွမ်းကျင်သူ - aperient)
WARNING: OOV dictionary entry (ကျွဲ - buffaloed)
WARNING: OOV dictionary entry (ကြွေ - enamor)
WARNING: OOV dictionary entry (စိတ်ဝင်စားမှု - interestedness)
WARNING: OOV dictionary entry (ပဋိညာဉ် - coven)
WARNING: OOV dictionary entry (မျက်နှာဖုံး - masque)
WARNING: OOV dictionary entry (ပန်းထိမ် - ironsmith)
WARNING: OOV dictionary entry (အစာအိမ်နာ - ulcerate)
WARNING: OOV dictionary entry (စင်တီမီတာ - centiliter)
WARNING: OOV dictionary entry (ဗီတာမင် - vitamine)
WARNING: OOV dictionary entry (အဆင်မပြေ - malfeasant)
WARNING: OOV dictionary entry (သေနတ်သံ - outgun)
WARNING: OOV dictionary entry (ဟင်းချို - soupspoon)
WARNING: OOV dictionary entry (သရော်စာ - satirically)
WARNING: OOV dictionary entry (အရက်သမား - chocoholic)
WARNING: OOV dictionary entry (ပဲ့တင်သံ - echoic)
WARNING: OOV dictionary entry (ဟိတ်ကြီးဟန်ကြီး - pompously)
WARNING: OOV dictionary entry (အစားထိုး - substituent)
WARNING: OOV dictionary entry (စိတ်ပျက် - deject)
WARNING: OOV dictionary entry (အခန်း - compart)
WARNING: OOV dictionary entry (အားသွန်ခွန်စိုက် - strenously)
WARNING: OOV dictionary entry (ဆိုးဆေး - dyestuff)
WARNING: OOV dictionary entry (တေးသံရှင် - vocalizer)
WARNING: OOV dictionary entry (မဟာသီယာ - maharanee)
WARNING: OOV dictionary entry (မြို့တော်ခန်းမ - townhall)
WARNING: OOV dictionary entry (ပစ္စည်း - confiture)
WARNING: OOV dictionary entry (သမာဓိ - virtuousness)
WARNING: OOV dictionary entry (မတ်တပ်ရပ် - standee)
WARNING: OOV dictionary entry (ငွေထည် - maunder)
WARNING: OOV dictionary entry (ကြိုတင် - prelims)
WARNING: OOV dictionary entry (မျက်ဖြူ - sclera)
WARNING: OOV dictionary entry (ကျောပိုး - backcloth)
WARNING: OOV dictionary entry (ကောင်းစွာ - wellhouse)
WARNING: OOV dictionary entry (ငါး - fishiness)
WARNING: OOV dictionary entry (ချိုချိုသာသာ - mellifluously)
WARNING: OOV dictionary entry (ခေတ်ပြိုင် - extemporary)
WARNING: OOV dictionary entry (ပေါင်းပင် - weeder)
WARNING: OOV dictionary entry (စီဒီ - sinedie)
WARNING: OOV dictionary entry (လရောင် - moonbeam)
WARNING: OOV dictionary entry (ခေါ်သံ - catcall)
WARNING: OOV dictionary entry (အပွင့် - floury)
WARNING: OOV dictionary entry (လင်းယုန်ငှက် - eaglet)
WARNING: OOV dictionary entry (ကြီးကြီးမားမား - gride)
WARNING: OOV dictionary entry (အုတ်တံတိုင်း - curbstone)
WARNING: OOV dictionary entry (ဟောသည် - soothsay)
WARNING: OOV dictionary entry (အရူးမ - madwoman)
WARNING: OOV dictionary entry (တောက်ပ - scintillate)
WARNING: OOV dictionary entry (စာရွက်စာတမ်း - dosser)
WARNING: OOV dictionary entry (ချစ်စဖွယ် - amorously)
WARNING: OOV dictionary entry (တိတ်ဆိတ် - quietus)
WARNING: OOV dictionary entry (ဆွဲဆောင်မှု - emblazonment)
WARNING: OOV dictionary entry (ကျောင်းပိတ်ရက် - schoolmarm)
WARNING: OOV dictionary entry (ခေါင်းစီး - headstream)
WARNING: OOV dictionary entry (ခြံစောင့် - yardman)
WARNING: OOV dictionary entry (အံ့သြဖွယ် - musingly)
WARNING: OOV dictionary entry (အပုပ် - putridity)
WARNING: OOV dictionary entry (လက်စွပ် - handbasket)
WARNING: OOV dictionary entry (တရှုံ့ရှုံ့ - whiffle)
WARNING: OOV dictionary entry (ရေမှုတ် - waterthrush)
WARNING: OOV dictionary entry (အို - oho)
WARNING: OOV dictionary entry (ကန့်သတ် - limitedly)
WARNING: OOV dictionary entry (တရွေ့ရွေ့ - gushingly)
/media/ye/project2/exp/bilingual-induction/exp1/my-en/vecmap-output10/
├── src_mapped_supervised.emb
├── src_super
│   ├── word2vec_s100_mc2_w3.vec
│   ├── word2vec_s100_mc2_w3.vec_mapped.vec
│   ├── word2vec_s200_mc2_w3.vec
│   └── word2vec_s200_mc2_w3.vec_mapped.vec
├── trg_mapped_supervised.emb
└── trg_super
    ├── word2vec_s100_mc2_w3.vec
    ├── word2vec_s100_mc2_w3.vec_mapped.vec
    ├── word2vec_s200_mc2_w3.vec
    └── word2vec_s200_mc2_w3.vec_mapped.vec

2 directories, 10 files
Evaluation ... 
--retrieval nn:
Coverage: 92.64%  Accuracy:  3.28%

real	0m11.332s
user	0m15.702s
sys	0m4.351s
--retrieval invnn:

```
