# compare-mt Running Demo

compare-mt ကို သုံးပြီးတော့ machine translation system နှစ်ခုအကြား significantly difference ဖြစ်မဖြစ်ကို တိုင်းတာပြထားတာပါ။ 
ဗမာစာ အပါအဝင် တိုင်းရင်းသား ဘာသာစကားတွေအကြား ကွန်ပျူတာကိုသုံးပြီး အော်တိုဘာသာပြန်နိုင်အောင် Statistical Machine Translation, Neural Machine Translation စတဲ့ experiment တွေကို အများကြီး လုပ်ခဲ့ပါတယ်။ Researcher အနေနဲ့ ဒီနေရာမှာ အရေးကြီးတဲ့မေးခွန်းတစ်ခုက system နှစ်ခုအကြားမှာ ဘယ် machine translation system or approach က ပိုသာတာလဲ၊ ပိုကောင်းတာလဲ ဆိုတဲ့ မေးခွန်းပါ။  

လက်တွေ့မှာက parallel corpus ဒေတာကလည်း အထူးသဖြင့် ဗမာစာနဲ့ တိုင်းရင်းသား ဘာသာစကားတွေအတွက်ဆိုရင် ဒေတာက မရှိလို့ ကိုယ်ဖာသာကိုယ်ဆောက်ရတာနဲ့ Test-set တစ်ခုကိုပဲသုံးပြီး evaluation လုပ်ကြရပါတယ်။ အဲဒါကြောင့် သုံးထားတဲ့ test-set အပေါ်မှာ အရမ်းမူတည်နေလို့... ကံကောင်းသွားလို့ system-1 က system-2 ထက် သာသွားတယ်ဆိုတဲ့ case လည်း ဖြစ်နိုင်ပါတယ်။  

အဲဒါကြောင့် ဘယ် approach က သာတယ်ဆိုတာကို prove လုပ်ဖို့ ဆိုရင် လုပ်လို့ ရတဲ့ နည်းလမ်းတစ်ခုက statistical test လုပ်တာ တနည်းအားဖြင့် bootstrap resampling လုပ်ပြီး machine translation evaluation တာပါ (Philipp Koehn, 2004)။ 
အဲဒီလို လုပ်ရင် test-data က နည်းရင်တောင် (e.g. 300 sentences) system နှစ်ခုအကြားမှာ ဘယ် system က ပိုသာတယ်ဆိုတာကို evaluation လုပ်ပြီးတော့ စာတမ်းမှာ confidence ရှိစွာနဲ့ဖော်ပြလို့ရပါတယ်။ 
အဲဒီလို လုပ်ဖို့အတွက် ဆိုရင် moses (SMT tool) မှာဆိုရင် bootstrap-hypothesis-difference-significance.pl (moses/scripts/analysis) ဆိုတဲ့ perl program ရှိပါတယ်။ 
ဒီနေရာမှာတော့ ပိုပြီးတော့ visualize လုပ်ပေးတဲ့ compare-mt ကို သုံးပြီး လုပ်ပြထားပါတယ်။ ယူသုံးထားတဲ့ experiment က ဒေါက်တာတန်း ကျောင်းသူ သဇင်မြင့်ဦး နဲ့အတူလေ့လာနေတဲ့ Pivot Machine Translation ကပါ။
အဓိက အသစ်လုပ်ကြည့်ခဲ့တဲ့ approach က နှစ်မျိုးပါ Transfer Pivot နဲ့ Triangulation Pivot ပါ။ 
Run ထားတာတွေ အများကြီးထဲကနေ Beik-Burmese-Rakhine (baseline vs triangulation) နဲ့ Beik-Burmese-Rakhine (Transfer vs Triangulation) အတွက် compare-mt ကို run ထားတဲ့ ရလဒ်တွေကို folder အလိုက် တင်ပေးထားပါတယ်။ 
ဂျာနယ်စာတမ်း publish လုပ်ပြီးသွားရင် ဒီနေရာမှာလည်း အဲဒီ စာတမ်းရဲ့ link ကို ဖြည့်ပေးထားပါမယ်။  

1 Jan 2022  
y@Lab  


## Bootstrap Resampling Results with compare-mt

[compare-mt-demo/](https://github.com/ye-kyaw-thu/error-overflow/tree/master/compare-mt-demo) ဖိုလ်ဒါအောက်မှာ html report နှစ်ခုရဲ့ ဖိုလ်ဒါတွေကို upload လုပ်ပေးထားပါတယ်။ ပထမ ဖိုလ်ဒါက ဘိတ်ကနေ ရခိုင်ဘာသာကို SMT လုပ်တာကို pivot language အနေနဲ့ ဗမာစာကို ထားထားပြီး လုပ်ခဲ့တဲ့ Triangulation-Pivot experiment ပါ။ ဒီနေရာမှာ baseline (i.e. normal PBSMT translation) ထက် Triangulation-Pivot experiment ရဲ့ ရလဒ်တွေက statistically significance (p <= 0.05) ဖြစ်တယ်ဆိုတာကို လေ့လာနိုင်ပါတယ်။   

1. [Bootstrap Resampling for Baseline-vs-Triangulation, Beik-Myanmar-Rakhine](https://htmlpreview.github.io/?https://github.com/ye-kyaw-thu/error-overflow/blob/master/compare-mt-demo/bk-my-rk-baseline-vs-triangulation/index.html)  

Transfer-Pivot နဲ့ Triangulation-Pivot နည်းလမ်းနှစ်ခုအကြား bootstrap resampling လုပ်ထားတာကိုလည်း အောက်ပါ လင့်ကနေလေ့လာနိုင်ပါတယ်။ ဒီနေရာမှာ Triangulation-Pivot က Transfer-Pivot က statistically significance ဖြစ်တယ်ဆိုတာကို တွေ့ကြရပါလိမ့်မယ်။  

2. [Beik-Burmese-Rakhine (Transfer vs Triangulation)](https://htmlpreview.github.io/?https://github.com/ye-kyaw-thu/error-overflow/blob/master/compare-mt-demo/bk-my-rk-transfer-vs-triangulation/index.html)  

## Example Shell Script for Running compare-mt

ဘိတ်-မြန်မာ-ရခိုင် နဲ့ ရခိုင်-မြန်မာ-ဘိတ် pivot machine translation ရလဒ်တွေအတွက် compare-mt ကို သုံးပြီး bootstrap resampling လုပ်ဖို့အတွက် ရေးထားတဲ့ shell script ပါ။ ဒီ script ကို run လိုက်ရင် final/ ဆိုတဲ့ ဖိုလ်ဒါအောက်မှာ အောက်ပါ နာမည်တွေနဲ့ sub-folder ၈ခု ထွက်လာပြီးတော့ အဲဒီအောက်မှာ HTML report တစ်ခုချင်းစီကို output အနေနဲ့ ထုတ်ပေးမှာဖြစ်ပါတယ်။ ပုံတွေကိုလည်း png ဖိုင်အနေနဲ့ရော pdf ဖိုင်အနေနဲ့ရော သိမ်းပေးမှာ ဖြစ်ပါတယ်။ ပြီးတော့ HTML report မှာက latex script ပါ တွဲထုတ်ပေးတာမို့ သုတေသနစာတမ်းရေးတဲ့အခါမှာလည်း အသုံးဝင်ပါလိမ့်မယ်။  

Output folders:  

1. bk-my-rk-baseline-transfer-triangulation/
2. bk-my-rk-baseline-vs-transfer/
3. bk-my-rk-baseline-vs-triangulation/
4. bk-my-rk-transfer-vs-triangulation/
5. rk-my-bk-baseline-transfer-triangulation/
6. rk-my-bk-baseline-vs-transfer/
7. rk-my-bk-baseline-vs-triangulation/
8. rk-my-bk-transfer-vs-traingulation/

[compare-mt-demo/](https://github.com/ye-kyaw-thu/error-overflow/tree/master/compare-mt-demo) ဖိုလ်ဒါအောက်မှာက statistically significant clearly ဖြစ်တဲ့  ```3. bk-my-rk-baseline-vs-triangulation/``` နဲ့ ```4. bk-my-rk-transfer-vs-triangulation/``` ဖိုလ်ဒါနှစ်ခုကိုပဲ လေ့လာနိုင်အောင် upload လုပ်ပေးထားတာ ဖြစ်ပါတယ်။  

```bash
#!/bin/bash

# final running for paper
# Written by Ye Kyaw Thu, LST, NECTEC, Thailand
# Last updated 26 Dec 2021
# baseline path
#/media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/rk-bk/10/baseline/bk-rk/evaluation/test.cleaned.1

# make a big report for Beik-Burmese-Rakhine (Transfer vs Triangulation)
# Note: RIBES score calculation give an error ... 

echo "### Report between Transfer and Triangulation";
echo "";
# Report between Transfer and Triangulation
#--compare_sentence_buckets score_measure=sentbleu
compare-mt /media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/rk-my/10/test.rk /media/ye/project1/exp/rk-bk-my-word-pivot/exp/ssentence/bk-my-rk/10/hypo-sentence.myrk.rk /media/ye/project1/exp/rk-bk-my-word-pivot/triangulation-tz/demo/10/bk-my-rk/hypo.rk --compare_scores score_type=bleu,bootstrap=1000,prob_thresh=0.05 score_type=chrf,bootstrap=1000,prob_thresh=0.05 score_type=wer,bootstrap=1000,prob_thresh=0.05  --compare_word_accuracies bucket_type=freq,freq_corpus_file=/media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/rk-my/10/train.rk  --report_title "Comparison Result for Beik-Burmese-Rakhine (Transfer vs Triangulation)" --sys_names "Transfer-Pivot" "Triangulation-Pivot" --output_directory ./final/bk-my-rk-transfer-vs-triangulation
echo "####################";

# make a big report for Rakhine-Burmese-Beik (Transfer vs Triangulation)
compare-mt /media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/my-bk/10/test.bk  /media/ye/project1/exp/rk-bk-my-word-pivot/exp/ssentence/rk-my-bk/10/hypo-sentence.mybk.bk /media/ye/project1/exp/rk-bk-my-word-pivot/triangulation-tz/demo/10/rk-my-bk/hypo.bk --compare_scores score_type=bleu,bootstrap=1000,prob_thresh=0.05 score_type=chrf,bootstrap=1000,prob_thresh=0.05 score_type=wer,bootstrap=1000,prob_thresh=0.05 --compare_word_accuracies bucket_type=freq,freq_corpus_file=/media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/my-bk/10/train.bk --report_title "Comparison Result for Rakhine-Burmese-Beik (Transfer vs Triangulation)" --sys_names "Transfer-Pivot" "Triangulation-Pivot" --output_directory ./final/rk-my-bk-transfer-vs-traingulation
echo "####################";

##########################
#Report for Baseline vs Transfer
echo "### Report for Baseline vs Transfer";
echo "";
compare-mt /media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/rk-my/10/test.rk /media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/rk-bk/10/baseline/bk-rk/evaluation/test.cleaned.1 /media/ye/project1/exp/rk-bk-my-word-pivot/exp/ssentence/bk-my-rk/10/hypo-sentence.myrk.rk --compare_scores score_type=bleu,bootstrap=1000,prob_thresh=0.05 score_type=chrf,bootstrap=1000,prob_thresh=0.05 score_type=wer,bootstrap=1000,prob_thresh=0.05  --compare_word_accuracies bucket_type=freq,freq_corpus_file=/media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/rk-my/10/train.rk  --report_title "Comparison Result for Beik-Burmese-Rakhine  (baseline vs transfer)" --sys_names "Direct-Translation" "Transfer-Pivot" --output_directory ./final/bk-my-rk-baseline-vs-transfer
echo "####################";

compare-mt /media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/my-bk/10/test.bk /media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/rk-bk/10/baseline/rk-bk/evaluation/test.cleaned.1 /media/ye/project1/exp/rk-bk-my-word-pivot/exp/ssentence/rk-my-bk/10/hypo-sentence.mybk.bk --compare_scores score_type=bleu,bootstrap=1000,prob_thresh=0.05 score_type=chrf,bootstrap=1000,prob_thresh=0.05 score_type=wer,bootstrap=1000,prob_thresh=0.05 --compare_word_accuracies bucket_type=freq,freq_corpus_file=/media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/my-bk/10/train.bk --report_title "Comparison Result for Rakhine-Burmese-Beik (baseline vs transfer)" --sys_names "Direct-Translation"  "Transfer-Pivot" --output_directory ./final/rk-my-bk-baseline-vs-transfer
echo "####################";

############################
# Report for Baseline vs Triangulation
echo "### Report for Baseline vs Triangulation";
echo "";
compare-mt /media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/rk-my/10/test.rk /media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/rk-bk/10/baseline/bk-rk/evaluation/test.cleaned.1 /media/ye/project1/exp/rk-bk-my-word-pivot/triangulation-tz/demo/10/bk-my-rk/hypo.rk --compare_scores score_type=bleu,bootstrap=1000,prob_thresh=0.05 score_type=chrf,bootstrap=1000,prob_thresh=0.05 score_type=wer,bootstrap=1000,prob_thresh=0.05  --compare_word_accuracies bucket_type=freq,freq_corpus_file=/media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/rk-my/10/train.rk  --report_title "Comparison Result for Beik-Burmese-Rakhine  (baseline vs triangulation)" --sys_names "Direct-Translation" "Triangulation-Pivot" --output_directory ./final/bk-my-rk-baseline-vs-triangulation
echo "####################";

compare-mt /media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/my-bk/10/test.bk /media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/rk-bk/10/baseline/rk-bk/evaluation/test.cleaned.1 /media/ye/project1/exp/rk-bk-my-word-pivot/triangulation-tz/demo/10/rk-my-bk/hypo.bk --compare_scores score_type=bleu,bootstrap=1000,prob_thresh=0.05 score_type=chrf,bootstrap=1000,prob_thresh=0.05 score_type=wer,bootstrap=1000,prob_thresh=0.05 --compare_word_accuracies bucket_type=freq,freq_corpus_file=/media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/my-bk/10/train.bk --report_title "Comparison Result for Rakhine-Burmese-Beik (baseline vs triangulation)" --sys_names "Direct-Translation"  "Triangulation-Pivot" --output_directory ./final/rk-my-bk-baseline-vs-triangulation
echo "####################";

############################

# Report for Baseline, Transfer and Triangulation
echo "### Report for Baseline, Transfer and Triangulation";
echo "";
compare-mt /media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/rk-my/10/test.rk /media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/rk-bk/10/baseline/bk-rk/evaluation/test.cleaned.1 /media/ye/project1/exp/rk-bk-my-word-pivot/exp/ssentence/bk-my-rk/10/hypo-sentence.myrk.rk /media/ye/project1/exp/rk-bk-my-word-pivot/triangulation-tz/demo/10/bk-my-rk/hypo.rk --compare_scores score_type=bleu,bootstrap=1000,prob_thresh=0.05 score_type=chrf,bootstrap=1000,prob_thresh=0.05 score_type=wer,bootstrap=1000,prob_thresh=0.05  --compare_word_accuracies bucket_type=freq,freq_corpus_file=/media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/rk-my/10/train.rk --report_title "Comparison Result for Beik-Burmese-Rakhine  (baseline, Transfer and Triangulation)" --sys_names "Direct-Translation" "Transfer-Pivot" "Triangulation-Pivot" --output_directory ./final/bk-my-rk-baseline-transfer-triangulation
echo "####################";

compare-mt /media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/my-bk/10/test.bk /media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/rk-bk/10/baseline/rk-bk/evaluation/test.cleaned.1 /media/ye/project1/exp/rk-bk-my-word-pivot/exp/ssentence/rk-my-bk/10/hypo-sentence.mybk.bk /media/ye/project1/exp/rk-bk-my-word-pivot/triangulation-tz/demo/10/rk-my-bk/hypo.bk --compare_scores score_type=bleu,bootstrap=1000,prob_thresh=0.05 score_type=chrf,bootstrap=1000,prob_thresh=0.05 score_type=wer,bootstrap=1000,prob_thresh=0.05 --compare_word_accuracies bucket_type=freq,freq_corpus_file=/media/ye/project1/exp/rk-bk-my-word-pivot/exp/rk-bk-my/data/my-bk/10/train.bk --report_title "Comparison Result for Rakhine-Burmese-Beik (baseline, transfer and triangulation)" --sys_names "Direct-Translation" "Transfer-Pivot" "Triangulation-Pivot" --output_directory ./final/rk-my-bk-baseline-transfer-triangulation
echo "####################";

```

## Reference

1. [https://en.wikipedia.org/wiki/P-value](https://en.wikipedia.org/wiki/P-value)
2. [https://en.wikipedia.org/wiki/Statistical_significance](https://en.wikipedia.org/wiki/Statistical_significance)
3. Koehn, Philipp. “Statistical Significance Tests for Machine Translation Evaluation.” EMNLP (2004). [Paper](https://aclanthology.org/W04-3250.pdf) 
4. [Github link of moses SMT Decoder](https://github.com/moses-smt/mosesdecoder)

