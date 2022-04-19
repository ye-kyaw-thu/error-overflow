## NMT Ensemble Experiment for MuHaung Translation

ဒီတစ်ခါတော့ seq2seq နဲ့ transformer architecture နှစ်မျိုးကိုနဲ့ ဆောက်ထားတဲ့ မော်ဒယ်တွေကို သုံးပြီး ensemble experiment လုပ်ကြည့်မယ်။  

### Ensemble Decoding Script for Seq2Seq and Transformer

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, Visiting Professor, LST, NECTEC, Thailand
# Last Updated: 19 April 2022
# Ensemble decoding with s2s+transformer:


# my-br, seq2seq အတွက် best model က model.iter65000.npz
# my-br, transformer အတွက် best model က model0-mybr.iter95000.npz

# --weights 0.4 0.6
time marian-decoder \
    --models ./model.s2s-mybr/model.iter65000.npz ./model.transformer/model0-mybr.iter95000.npz \
    --weights 0.4 0.6 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble/hyp.0.4-0.6.br \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my | tee my-br.ensemble.0.4-0.6.log
    
# --weights 0.5 0.5
time marian-decoder \
    --models ./model.s2s-mybr/model.iter65000.npz ./model.transformer/model0-mybr.iter95000.npz \
    --weights 0.5 0.5 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble/hyp.0.5-0.5.br \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my | tee my-br.ensemble.0.5-0.5.log
    
# --weights 0.6 0.4
time marian-decoder \
    --models ./model.s2s-mybr/model.iter65000.npz ./model.transformer/model0-mybr.iter95000.npz \
    --weights 0.6 0.4 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble/hyp.0.6-0.4.br \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my | tee my-br.ensemble.0.6-0.4.log
    
# br-my အတွက် best model က model.iter55000.npz
# br-my အတွက် best model က 

# --weights 0.4 0.6
time marian-decoder \
    --models ./model.s2s-brmy/model.iter55000.npz ./model.transformer-brmy/model0-brmy.iter80000.npz \
    --weights 0.4 0.6 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble/hyp.0.4-0.6.my \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br | tee br-my.ensemble.0.4-0.6.log

# --weights 0.5 0.5
time marian-decoder \
    --models ./model.s2s-brmy/model.iter55000.npz ./model.transformer-brmy/model0-brmy.iter80000.npz \
    --weights 0.5 0.5 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble/hyp.0.5-0.5.my \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br | tee br-my.ensemble.0.5-0.5.log
    
# --weights 0.6 0.4
time marian-decoder \
    --models ./model.s2s-brmy/model.iter55000.npz ./model.transformer-brmy/model0-brmy.iter80000.npz \
    --weights 0.6 0.4 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble/hyp.0.6-0.4.my \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br | tee br-my.ensemble.0.6-0.4.log

```

Ensemble Decoding ...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt$ time ./ensemble-exp.sh 
...
...
...
[2022-04-19 18:13:13] Best translation 2052 : ⠍⠪⠆⠱⠝ ⠅⠣⠇⠱⠆ ⠅ ⠡⠭ ⠏ ⠲
[2022-04-19 18:13:13] Best translation 2053 : ⠡⠭ ⠙⠻⠨⠔ ⠊ ⠃⠥⠆⠹⠪⠆⠟⠻ ⠰⠣⠁ ⠞⠣⠿⠓⠱⠆⠿⠓⠱⠆ ⠡⠭ ⠇⠁⠯ ⠟⠻ ⠝ ⠹⠣⠓⠾⠣ ⠅⠉ ⠹⠻⠆ ⠓⠥ ⠊ ⠲
[2022-04-19 18:13:13] Best translation 2054 : ⠍⠣⠓⠻⠹⠣⠙⠁ ⠹⠥⠂⠨⠣⠍⠢ ⠹ ⠼ ⠹⠥⠚ ⠎⠣⠅⠁⠆ ⠅ ⠟⠁⠆ ⠿⠪⠆ ⠧ ⠹⠔⠚ ⠌ ⠊ ⠣⠈⠉⠆⠣⠿⠓⠣⠞ ⠫ ⠞⠪ ⠟⠣ ⠍ ⠇⠻⠆ ⠓ ⠍⠱⠆ ⠊ ⠲
[2022-04-19 18:13:13] Best translation 2055 : ⠼⠙ ⠲
[2022-04-19 18:13:13] Best translation 2056 : ⠺⠊⠙⠱⠓⠣⠗⠭ ⠍⠔⠆⠟⠪⠆ ⠇⠆ ⠪ ⠿⠑⠹⠣⠝⠁ ⠅ ⠣⠃⠮⠹⠥ ⠿⠓⠱ ⠎⠪⠗⠔ ⠹⠝ ⠓ ⠍⠱⠆ ⠊ ⠲
[2022-04-19 18:13:13] Best translation 2057 : ⠟⠞⠚ ⠗⠴ ⠝⠱ ⠎⠔ ⠅⠋⠏⠶ ⠗ ⠗⠱ ⠗ ⠅⠋ ⠏⠪⠏⠪ ⠾⠔ ⠗⠣ ⠏⠱ ⠹⠱⠆ ⠹ ⠲
[2022-04-19 18:13:13] Best translation 2058 : ⠹⠁⠙⠣⠅⠣ ⠲ ⠲ ⠇⠥⠅⠶⠆ ⠰⠶ ⠇⠥⠅⠶⠆ ⠲
[2022-04-19 18:13:13] Best translation 2059 : ⠡⠔ ⠝ ⠈⠱⠆ ⠿⠓⠋⠆ ⠏ ⠲
[2022-04-19 18:13:13] Best translation 2060 : ⠟⠁⠆ ⠹ ⠅⠶⠆ ⠅⠣⠎⠁⠆ ⠗⠣⠹⠻⠆ ⠅⠣⠎⠁⠆⠝⠪⠆ ⠭ ⠹ ⠲
[2022-04-19 18:13:13] Best translation 2061 : ⠹⠣⠝⠣⠞ ⠓ ⠗⠱⠆ ⠰⠣⠣ ⠣⠹⠪⠆ ⠎⠣⠹ ⠚ ⠅ ⠈⠪ ⠒ ⠡⠭ ⠒ ⠌⠣⠗⠦⠹⠪⠆ ⠎⠣⠹ ⠚ ⠗ ⠗⠻⠆ ⠞⠓⠁⠆ ⠹⠻⠆ ⠎⠁⠆⠘⠺⠮ ⠞⠭ ⠾⠕⠆ ⠓ ⠣⠙⠱⠅⠏⠮ ⠗⠣ ⠇⠍ ⠲
[2022-04-19 18:13:13] Best translation 2062 : ⠼⠁ ⠲ ⠇⠥⠂⠇⠔ ⠰⠶ ⠿⠕⠗⠺⠮ ⠹⠻⠆ ⠽⠴⠟⠁⠆ ⠲
[2022-04-19 18:13:13] Best translation 2063 : ⠥⠂⠏⠣⠍⠁ ⠈⠔ ⠫ ⠡⠪ ⠅⠣⠇⠱⠆ ⠞⠭ ⠓⠾⠔ ⠅ ⠨⠣⠞ ⠘⠕⠂ ⠗⠋ ⠅⠶⠆ ⠹⠥ ⠓ ⠇⠑ ⠅⠣⠇⠆ ⠇⠱⠆ ⠌⠁⠆ ⠡⠑ ⠇⠴ ⠋ ⠗⠣ ⠊ ⠲
[2022-04-19 18:13:13] Best translation 2064 : ⠍⠊⠨⠔ ⠰⠣⠁ ⠹⠣⠃⠔ ⠏⠔⠷⠁⠹⠮ ⠾⠕⠆⠗⠕⠆ ⠭ ⠹ ⠲
[2022-04-19 18:13:13] Best translation 2065 : ⠹⠣⠞⠏⠉ ⠹⠋⠏⠴ ⠅⠣⠃⠽⠁ ⠅ ⠈⠕ ⠟ ⠗⠣⠶ ⠲
[2022-04-19 18:13:13] Best translation 2066 : ⠾⠑ ⠞⠭ ⠨⠣⠞ ⠒ ⠡⠭ ⠅⠮ ⠞⠭ ⠃⠪⠵⠣⠝⠁ ⠓⠾⠣ ⠲
[2022-04-19 18:13:13] Best translation 2067 : ⠺⠥⠞⠁⠥⠂ ⠅⠁⠍⠣⠛⠉ ⠒ ⠌⠺⠱⠎⠣ ⠗ ⠟⠉ ⠹⠻⠆⠣⠨⠁ ⠒ ⠁⠗⠉ ⠅ ⠿⠓⠣⠞ ⠝ ⠨⠮⠂ ⠸⠣⠣ ⠏ ⠹ ⠩⠺⠱⠝⠋⠆⠩⠔ ⠿ ⠲
[2022-04-19 18:13:13] Best translation 2068 : ⠣⠃⠕⠆⠟⠪⠆ ⠗⠻⠆ ⠅⠶⠍⠣⠇⠱⠆ ⠗⠻⠆ ⠹⠣⠞⠃⠔⠷⠥⠂ ⠿ ⠚ ⠒ ⠁⠝⠋⠙⠁ ⠿ ⠚ ⠒ ⠋ ⠶ ⠅⠋⠞⠻⠂⠏⠣⠇⠔ ⠶ ⠚ ⠸⠽⠴ ⠘⠥⠆ ⠗⠣⠶ ⠝⠱⠂⠇⠮ ⠅⠣⠞⠮⠆ ⠅⠣ ⠸⠣⠮⠆ ⠝⠮⠂ ⠁⠺⠑ ⠟ ⠞⠮ ⠲
[2022-04-19 18:13:13] Best translation 2069 : ⠓⠋ ⠣⠍⠥⠣⠽ ⠝⠮⠂ ⠈⠕ ⠝ ⠟⠣ ⠗⠮⠂⠇⠁⠆ ⠲
[2022-04-19 18:13:13] Best translation 2070 : ⠗⠺⠁ ⠁⠮⠆ ⠰⠣⠁ ⠣⠷⠢⠂ ⠏⠺⠮⠆ ⠩ ⠹⠇ ⠲
[2022-04-19 18:13:13] Best translation 2071 : ⠅⠺⠁ ⠵⠋⠃⠥⠙⠪⠏⠁ ⠰⠣⠁ ⠾⠋⠍⠁ ⠅ ⠝ ⠍⠂ ⠇⠥ ⠋ ⠏⠻ ⠹⠱⠆ ⠏⠁ ⠃⠥⠆ ⠓ ⠙ ⠞ ⠍⠥ ⠊ ⠲
[2022-04-19 18:13:13] Best translation 2072 : ⠼⠉ ⠲
[2022-04-19 18:13:13] Best translation 2073 : ⠼⠋ ⠲ ⠣⠟⠱ ⠰⠶ ⠾⠋⠍⠁ ⠿⠪ ⠋ ⠙⠱⠹⠣ ⠲
[2022-04-19 18:13:13] Best translation 2074 : ⠅⠮⠂⠗⠮⠂ ⠒ ⠡⠪⠆⠍⠥⠝⠆ ⠒ ⠎⠁⠗⠔⠆ ⠒ ⠹⠑⠹⠱ ⠒ ⠣⠟⠔⠂ ⠒ ⠦⠎⠁ ⠲
[2022-04-19 18:13:13] Best translation 2075 : ⠩⠱⠆ ⠹⠻⠆⠣⠨⠁ ⠃⠁⠗⠁⠝⠣⠹⠪ ⠍⠔⠆ ⠞⠭⠏⠁⠆ ⠊ ⠹⠁⠆⠞ ⠹ ⠞⠑⠅⠣⠹⠕ ⠿⠪ ⠫ ⠏⠔⠷⠁ ⠹⠔⠟⠁⠆ ⠝⠱⠎⠔ ⠞⠭ ⠝⠱⠂ ⠫ ⠣⠍⠮⠕ ⠞⠭ ⠽⠴ ⠸⠣⠋⠆ ⠞⠓⠁⠆ ⠹⠻⠆ ⠠⠣⠋⠆ ⠅ ⠎⠁⠆ ⠇⠕ ⠹ ⠗ ⠞⠭ ⠈⠦ ⠽⠥⠯ ⠎⠁⠆ ⠊ ⠲
[2022-04-19 18:13:13] Best translation 2076 : ⠎⠢⠂ ⠟⠪⠆ ⠾⠖ ⠟⠪⠆ ⠒ ⠗⠱⠅ ⠟⠪⠆ ⠞⠻⠆ ⠞⠶ ⠲
[2022-04-19 18:13:13] Best translation 2077 : ⠏⠁⠇⠊ ⠎⠁⠏⠱ ⠟⠋⠆⠛⠋⠾ ⠅⠣⠃⠽⠁ ⠇⠔⠅⠁⠾ ⠅ ⠇⠮⠞⠪ ⠈⠣⠗⠁⠞ ⠁⠋ ⠞⠺ ⠈⠑⠇⠑ ⠈⠪⠆⠏⠥⠆ ⠿⠪⠆ ⠹⠑⠅⠣⠞⠣ ⠎⠁⠏⠱⠾ ⠅ ⠋ ⠈⠣⠗⠁⠞ ⠁⠋ ⠞⠺ ⠈⠑⠇⠑ ⠈⠪⠆⠏⠥⠆ ⠹ ⠲
[2022-04-19 18:13:13] Best translation 2078 : ⠼⠉ ⠲ ⠦ ⠞⠋⠞⠖⠆ ⠅⠁⠗⠋ ⠹⠻⠆ ⠡⠋ ⠟⠮ ⠟⠪⠆⠾ ⠞⠺ ⠞⠓⠁⠆⠩ ⠹⠂ ⠞⠊⠗⠭⠈⠋⠾ ⠊ ⠣⠍ ⠅ ⠘⠻⠿⠣ ⠏ ⠲ ⠣⠃⠮⠳ ⠁⠕⠙ ⠞⠓⠁⠆ ⠗⠣ ⠹⠝ ⠲
[2022-04-19 18:13:13] Best translation 2079 : ⠪ ⠅⠣⠃⠽⠁ ⠅ ⠗⠱⠆⠹⠥ ⠥⠆⠟⠔⠥⠂ ⠹ ⠾⠋⠍⠁ ⠠⠣⠭ ⠼⠁ ⠁ ⠉ ⠑ ⠤ ⠼⠁ ⠃ ⠚ ⠚ ⠶ ⠅⠗ ⠠⠣⠭ ⠼⠁ ⠛ ⠛ ⠉ ⠤ ⠼⠁ ⠓ ⠉ ⠓ ⠶ ⠣⠞⠺⠑ ⠏⠻⠏⠴ ⠨⠮⠂ ⠹⠻⠆ ⠎⠁⠈⠕ ⠭ ⠹ ⠲
[2022-04-19 18:13:13] Best translation 2080 : ⠼⠉ ⠁ ⠲ ⠴⠍⠱⠂ ⠰⠶ ⠈⠔⠡⠔ ⠎⠔⠆⠎⠁⠆ ⠹ ⠲ ⠠⠣⠣⠇⠉⠆⠹⠺⠔⠆ ⠹ ⠲
[2022-04-19 18:13:13] Best translation 2081 : ⠼⠁ ⠲ ⠣⠞⠁⠅⠥⠆ ⠡ ⠈⠕⠹ ⠰⠣⠁ ⠣⠃⠮ ⠝⠪⠆ ⠲
[2022-04-19 18:13:13] Best translation 2082 : ⠪ ⠹⠥ ⠊ ⠝⠺⠁⠆⠾ ⠋⠓⠦ ⠏ ⠲
[2022-04-19 18:13:13] Best translation 2083 : ⠼⠉ ⠲ ⠴⠏⠁ ⠣⠇⠔⠅⠁ ⠚ ⠹ ⠍⠙ ⠹⠻⠆ ⠣⠟ ⠗ ⠈⠑⠎⠣⠞ ⠹⠉⠆ ⠞⠓⠁⠆ ⠿⠪⠆ ⠣⠃⠮⠳ ⠼ ⠣⠇⠔⠅⠁ ⠾⠴ ⠟⠶⠆ ⠩⠔⠆⠿⠣ ⠏ ⠲
[2022-04-19 18:13:13] Best translation 2084 : ⠾⠕⠂ ⠞⠶ ⠾⠑⠠⠣⠁ ⠅⠣ ⠗⠱ ⠗⠶⠆ ⠍⠢⠆⠍⠣ ⠁⠺⠑ ⠈⠕ ⠗⠋ ⠎⠣⠅⠁⠆ ⠰⠣⠁ ⠲
[2022-04-19 18:13:13] Best translation 2085 : ⠎⠁ ⠣⠗⠱⠆⠣⠹⠁⠆ ⠣⠇⠱⠆⠞⠓⠁⠆ ⠏ ⠲
[2022-04-19 18:13:13] Best translation 2086 : ⠟⠬⠁⠪⠆⠗⠕⠆ ⠎⠱⠞⠪⠞ ⠹ ⠾⠣⠞⠎⠿ ⠊ ⠈⠋⠞⠩⠔ ⠅ ⠞⠓⠁⠏⠣⠝⠁⠯ ⠞⠮ ⠞⠓⠁⠆ ⠵ ⠞⠋⠨⠕⠆ ⠟⠪⠆ ⠹ ⠓ ⠽⠉⠟⠪ ⠅⠕⠆⠅⠺⠮ ⠟ ⠹ ⠲
[2022-04-19 18:13:13] Best translation 2087 : ⠅⠺⠮⠇⠥⠝ ⠹⠂ ⠣⠡⠢ ⠣⠁⠊ ⠣⠈⠑⠍⠣⠿⠣⠞ ⠎⠁ ⠗⠱⠆ ⠨⠮⠂ ⠹⠥ ⠭ ⠹ ⠲
[2022-04-19 18:13:13] Best translation 2088 : ⠼⠃ ⠚ ⠁ ⠚ ⠤ ⠼⠃ ⠚ ⠁ ⠁ ⠏⠔⠷⠁⠹⠔ ⠠⠣⠭ ⠲
[2022-04-19 18:13:13] Best translation 2089 : ⠎⠣ ⠲
[2022-04-19 18:13:13] Best translation 2090 : ⠼⠛ ⠲ ⠹⠪⠞⠔⠆⠟⠥⠞ ⠞⠺ ⠒ ⠏⠣⠇⠔ ⠈⠱⠆ ⠍⠕⠆ ⠒ ⠗⠺⠁⠹⠥⠝⠆⠿⠓⠕⠆ ⠲
[2022-04-19 18:13:13] Best translation 2091 : ⠼⠉ ⠊ ⠲ ⠽⠣⠞⠍⠁⠆ ⠰⠶ ⠝⠋⠆⠞⠺⠔⠆ ⠹⠉⠆ ⠣⠗⠕⠆ ⠩⠱ ⠽⠣⠞ ⠟⠪⠆ ⠲
[2022-04-19 18:13:13] Best translation 2092 : ⠙⠦⠨⠣ ⠏⠁ ⠏⠮⠆ ⠹⠥⠌⠮⠡⠔⠆ ⠗⠱ ⠨⠮⠆⠞⠋ ⠓⠌⠁⠆ ⠏ ⠕⠝⠆ ⠇⠕⠂ ⠿⠻⠆ ⠿⠪⠆ ⠣⠅⠥⠣⠷⠪ ⠞⠶⠆ ⠗⠣ ⠞⠮ ⠲
[2022-04-19 18:13:13] Best translation 2093 : ⠙⠗⠁ ⠞⠺ ⠼ ⠿⠪ ⠅⠣⠇⠱⠆ ⠅⠣ ⠎⠭ ⠋ ⠞⠬ ⠃⠮⠆ ⠟⠞⠚ ⠃⠥⠂⠗⠔ ⠅ ⠘⠋⠆ ⠹⠺⠁⠆ ⠏ ⠲
[2022-04-19 18:13:13] Best translation 2094 : ⠅⠣⠇⠣⠞⠑⠹⠋ ⠗⠣⠞⠥ ⠏⠯ ⠇⠁ ⠹⠻⠆ ⠣⠙⠱⠅⠏⠮ ⠞⠭ ⠾⠕⠆ ⠇⠆ ⠩ ⠹⠱⠆ ⠊ ⠲
[2022-04-19 18:13:13] Best translation 2095 : ⠣⠩ ⠍⠔⠆⠟⠪⠆ ⠒ ⠟⠥ ⠊ ⠣⠍ ⠅⠁⠆ ⠹⠥⠂⠺⠥⠝⠝⠣⠹⠁⠍⠣ ⠞⠪⠆ ⠲
[2022-04-19 18:13:13] Best translation 2096 : ⠋ ⠅⠥⠂⠹⠕⠩⠔ ⠇⠥⠿⠕⠟⠪⠆ ⠎⠥⠝ ⠡⠔ ⠩⠁ ⠵ ⠟⠻⠷⠁ ⠅⠋⠆ ⠞⠓⠁⠆ ⠓⠋ ⠞⠥ ⠹ ⠲
[2022-04-19 18:13:13] Best translation 2097 : ⠾⠴⠃⠑ ⠈⠪ ⠙ ⠨⠣⠗⠪⠆ ⠠⠣⠔ ⠞⠺⠱⠂ ⠇⠢⠂ ⠝⠮ ⠅⠣⠡⠔ ⠏⠣⠇⠺⠱ ⠹⠋⠇⠺⠔ ⠕⠆⠎⠪ ⠠⠣⠻⠆ ⠁⠶⠅⠁ ⠝⠮⠂ ⠍⠣⠝⠻⠆ ⠲
[2022-04-19 18:13:13] Best translation 2098 : ⠾⠋⠍⠁ ⠃⠥⠂⠗⠔ ⠚ ⠅⠕⠂ ⠁⠪⠆ ⠅⠕⠂ ⠝⠋⠆ ⠣⠭ ⠝⠴⠈⠉⠆ ⠞⠪⠁⠶ ⠎⠋⠾⠋⠆ ⠨⠮⠂ ⠟⠣ ⠹⠂ ⠝⠋⠆⠞⠻ ⠟⠪⠆ ⠇⠆ ⠭ ⠹ ⠲
[2022-04-19 18:13:13] Best translation 2099 : ⠻⠆ ⠻⠂ ⠻ ⠲
[2022-04-19 18:13:13] Best translation 2100 : ⠼⠉ ⠲ ⠅⠋⠙⠣ ⠰⠶ ⠣⠏⠖⠆ ⠒ ⠣⠨⠋⠆ ⠲
[2022-04-19 18:13:13] Best translation 2101 : ⠞⠔ ⠏ ⠹ ⠿ ⠲
[2022-04-19 18:13:13] Best translation 2102 : ⠏⠋⠆⠅⠣⠇⠱⠆⠾ ⠏⠺⠔⠂ ⠞⠻⠂ ⠍ ⠘⠥⠆⠞⠋ ⠡⠭ ⠡⠪ ⠒ ⠝⠱⠡⠪ ⠰⠣⠁ ⠩⠺⠱⠗⠪ ⠇⠶⠆ ⠌⠁ ⠚ ⠎⠁⠹⠔⠟⠶⠆ ⠲
[2022-04-19 18:13:13] Best translation 2103 : ⠇⠱⠂⠟⠔⠂⠨⠋⠆ ⠲
[2022-04-19 18:13:13] Best translation 2104 : ⠼⠋ ⠲ ⠾⠋⠍⠁⠂ ⠗⠕⠆⠗⠁ ⠡ ⠅⠣⠎⠁⠆ ⠝⠪⠆ ⠹ ⠾⠋⠍⠁ ⠚ ⠣⠞⠺⠑ ⠛⠉⠽⠥ ⠘⠺⠮⠗⠁ ⠭ ⠏ ⠹⠇ ⠲
[2022-04-19 18:13:13] Best translation 2105 : ⠣⠗⠱⠆ ⠋⠓⠦ ⠓ ⠸⠽⠴ ⠹ ⠅ ⠟⠬ ⠞ ⠋ ⠍⠥ ⠲
[2022-04-19 18:13:13] Best translation 2106 : ⠟⠋⠆⠍⠁ ⠰⠣⠥⠂ ⠒ ⠋ ⠇⠱⠆⠎⠁⠆ ⠣⠞⠏⠱ ⠒ ⠚⠍⠱⠍⠱ ⠲
[2022-04-19 18:13:13] Best translation 2107 : ⠈⠱⠆⠟⠻⠆ ⠲
[2022-04-19 18:13:13] Best translation 2108 : ⠼ ⠹⠥⠂ ⠝⠺⠁⠆ ⠋⠓⠦ ⠓ ⠈⠕ ⠊ ⠲
[2022-04-19 18:13:13] Best translation 2109 : ⠹⠥ ⠊ ⠏⠁⠆ ⠅⠣⠇⠱⠆⠾ ⠒ ⠡⠱ ⠿⠓⠁⠆ ⠇⠑ ⠿⠓⠁⠆ ⠅⠣⠇⠱⠆⠾ ⠒ ⠝⠁⠆⠗⠺⠑ ⠅⠣⠇⠱⠆⠾ ⠰⠣⠁ ⠺⠁⠯ ⠇⠁ ⠟ ⠃ ⠹ ⠲
[2022-04-19 18:13:13] Best translation 2110 : ⠶ ⠎⠣ ⠶ ⠣⠍⠊ ⠣⠘⠣ ⠚ ⠅ ⠇⠦⠟⠺⠱⠆ ⠡ ⠿⠓ ⠍⠙ ⠹⠻⠆ ⠣⠟⠕⠆⠟⠵ ⠚ ⠅ ⠗⠣⠩ ⠝ ⠹⠝ ⠲
[2022-04-19 18:13:13] Best translation 2111 : ⠼⠋ ⠲ ⠲ ⠇⠣⠿⠱⠂ ⠟⠻ ⠼⠋ ⠗⠑ ⠏ ⠘⠱⠘⠱ ⠲
[2022-04-19 18:13:19] Best translation 2112 : ⠡⠖ ⠡⠖⠂ ⠡⠖⠆ ⠲
[2022-04-19 18:13:19] Best translation 2113 : ⠹⠥ ⠹ ⠝⠍ ⠗ ⠇⠬ ⠶ ⠿⠓⠥ ⠹ ⠒ ⠡⠻⠆ ⠹ ⠒ ⠸⠣⠣ ⠹ ⠒ ⠡⠻⠆ ⠹ ⠸⠣⠣ ⠹ ⠗ ⠣⠓⠾⠣ ⠋ ⠇⠔ ⠌⠮ ⠱ ⠞⠣⠞ ⠹⠥ ⠲
[2022-04-19 18:13:19] Best translation 2114 : ⠼⠃ ⠲ ⠇⠱⠆ ⠍⠶⠂ ⠎⠋⠟⠶⠆ ⠞⠺ ⠡⠭ ⠾⠕⠆ ⠚ ⠹ ⠍⠙ ⠹⠻⠆ ⠝⠱⠗⠁ ⠣⠹⠪⠆⠹⠪⠆ ⠫ ⠏⠴ ⠝⠱ ⠞⠋⠎⠓⠁⠈⠔ ⠱ ⠟ ⠹⠝ ⠲
[2022-04-19 18:13:19] Best translation 2115 : ⠣⠾⠕⠆ ⠨⠥⠂⠝⠭ ⠈⠑ ⠞⠖⠶ ⠋ ⠿⠑ ⠹⠻⠆ ⠡⠭ ⠡ ⠹ ⠭ ⠃ ⠹⠞ ⠲
[2022-04-19 18:13:19] Best translation 2116 : ⠟⠁⠆ ⠹⠔⠟⠋ ⠲
[2022-04-19 18:13:19] Best translation 2117 : ⠼⠣⠨⠁ ⠏⠥⠂⠎⠥⠝ ⠅⠣ ⠣⠈⠺⠱ ⠃⠽⠖⠆ ⠣⠃⠮⠳ ⠣⠟⠥ ⠅ ⠖ ⠫ ⠋ ⠸⠣⠥⠞ ⠃⠮⠆ ⠪ ⠨⠋⠞⠑⠏⠔ ⠙ ⠈⠶⠽⠥ ⠨⠮⠂ ⠹⠝ ⠓ ⠍⠱⠆ ⠃ ⠊ ⠲
[2022-04-19 18:13:19] Best translation 2118 : ⠣⠍ ⠙⠣⠁⠺⠱⠆ ⠲
[2022-04-19 18:13:19] Best translation 2119 : ⠍⠋⠞⠣⠇⠱⠆ ⠞⠑⠅⠣⠹⠕ ⠰⠣⠣ ⠇⠱⠂⠇⠁ ⠗⠱⠆ ⠣⠘⠺⠮⠂ ⠲
[2022-04-19 18:13:19] Best translation 2120 : ⠓⠦⠅⠮⠂ ⠒ ⠇⠱⠆ ⠈⠮ ⠇⠴ ⠈⠕ ⠏ ⠞⠻⠂ ⠲
[2022-04-19 18:13:19] Best translation 2121 : ⠹⠥ ⠸ ⠌⠁⠆ ⠘⠋⠆ ⠁⠺⠑ ⠹⠣⠞⠣⠞ ⠶ ⠹⠣ ⠞⠮⠂ ⠶ ⠲
[2022-04-19 18:13:19] Best translation 2122 : ⠪ ⠇⠆ ⠿⠇⠶⠆ ⠁⠆ ⠅⠶⠆⠡⠪⠆ ⠍⠔⠛⠣⠇⠁ ⠞⠭ ⠟⠢ ⠭ ⠹⠞ ⠲
[2022-04-19 18:13:19] Best translation 2123 : ⠥⠂⠏⠮ ⠒ ⠕⠆⠎⠁⠆⠘⠑ ⠒ ⠽⠥⠝⠆⠍⠣ ⠒ ⠣⠏⠁ ⠡⠣ ⠒ ⠾⠔⠆ ⠰⠣⠁ ⠉⠆⠨⠥⠝ ⠒ ⠙⠁⠆ ⠰⠣⠁ ⠍⠕⠆⠟⠕⠆ ⠲
[2022-04-19 18:13:19] Best translation 2124 : ⠗⠣⠺⠱ ⠒ ⠃⠪⠵⠣⠝⠁ ⠒ ⠃⠽⠁⠈⠉ ⠒ ⠇⠱⠅⠿⠁ ⠱⠆ ⠒ ⠗⠣⠞⠥⠂ ⠲
[2022-04-19 18:13:19] Best translation 2125 : ⠅⠣⠞⠞⠪⠏⠁ ⠗ ⠲
[2022-04-19 18:13:19] Best translation 2126 : ⠾⠋⠍⠁ ⠃⠥⠂⠗⠔ ⠏⠁ ⠞⠍ ⠹⠻⠆⠣⠨⠁ ⠞⠺ ⠇⠆ ⠩⠺⠱ ⠈⠪⠆⠿⠓⠥ ⠹⠣⠃⠻⠆ ⠙ ⠒ ⠸⠣⠮⠂⠿⠓⠁⠆ ⠗ ⠸⠣⠢⠂ ⠹⠣⠇⠕ ⠓⠥⠯ ⠰⠣⠣⠞⠞⠋⠆⠞⠔ ⠨⠮⠂ ⠹ ⠲
[2022-04-19 18:13:19] Best translation 2127 : ⠨⠺⠱ ⠋ ⠨⠺⠱⠆ ⠲
[2022-04-19 18:13:19] Best translation 2128 : ⠥⠆⠊ ⠹ ⠣⠍⠣⠗⠣⠏⠥⠗⠣ ⠾⠕⠂ ⠋ ⠰⠣⠣ ⠏⠕⠆ ⠁⠮ ⠒ ⠡⠪ ⠁⠮ ⠚ ⠅ ⠣⠗⠶⠆⠣⠺⠮ ⠿⠥⠂ ⠹⠻⠆ ⠏⠕⠆ ⠋ ⠭⠗⠁ ⠏⠭⠎⠪⠆ ⠦⠎⠁ ⠟⠺⠮⠺⠣ ⠡⠋⠆⠹⠁ ⠹ ⠲
[2022-04-19 18:13:19] Best translation 2129 : ⠨⠑⠈⠭ ⠣⠘⠺⠔⠂ ⠲
[2022-04-19 18:13:19] Best translation 2130 : ⠼⠉ ⠲ ⠘⠺⠁ ⠗⠣ ⠗⠁ ⠰⠶ ⠎⠥⠂⠎⠪⠆ ⠡ ⠋ ⠩ ⠒ ⠅⠺⠮⠆ ⠿⠓⠁ ⠁⠺⠑ ⠑ ⠲
[2022-04-19 18:13:19] Best translation 2131 : ⠍⠊⠍⠊ ⠅⠕⠞⠖ ⠣⠹⠋⠝⠱⠣⠹⠋⠞⠓⠁⠆ ⠿⠓ ⠗⠥⠞⠈⠕ ⠇⠱⠂⠟⠔⠂ ⠏ ⠲
[2022-04-19 18:13:19] Best translation 2132 : ⠶ ⠨⠣ ⠶ ⠞⠭⠥⠂⠞⠥⠂ ⠸ ⠤⠤⠤⠤⠤⠤ ⠎⠪ ⠟⠁⠾⠔⠂ ⠏ ⠹ ⠲
[2022-04-19 18:13:19] Best translation 2133 : ⠷⠶⠏⠔⠹⠁⠗⠺⠁ ⠿⠓⠥⠆ ⠾⠕⠂⠝⠮ ⠼⠁ ⠉ ⠙ ⠑ ⠨⠥⠂ ⠒ ⠞⠋⠨⠥⠆ ⠇⠣⠈⠋⠆ ⠼⠁ ⠗⠑ ⠹⠥⠌⠮⠡⠔⠆ ⠋ ⠹⠥⠌⠮⠡⠔⠆ ⠁⠋⠙ ⠓⠮ ⠎⠁⠗⠱⠆⠇⠬ ⠏ ⠹ ⠲
[2022-04-19 18:13:19] Best translation 2134 : ⠼⠓ ⠲ ⠁⠆⠹⠋ ⠰⠶ ⠋ ⠗⠣ ⠋ ⠝⠱ ⠋ ⠭ ⠋ ⠝⠱ ⠁⠆⠁⠦ ⠟⠕⠆⠏⠋⠆ ⠹ ⠲
[2022-04-19 18:13:19] Best translation 2135 : ⠿⠁⠆⠗⠪ ⠹⠁ ⠈⠶⠽⠥ ⠟⠣ ⠡⠱ ⠓ ⠈⠕⠯ ⠿⠁⠆⠗⠪ ⠅ ⠈⠶⠽⠥ ⠎ ⠿⠪⠆ ⠧ ⠏⠣⠞⠞⠣⠾⠁⠆ ⠫ ⠣⠏⠴⠺⠣ ⠠⠣⠭ ⠘⠑ ⠅ ⠇⠢⠆⠹⠦ ⠿⠪⠆ ⠰⠣⠣ ⠝⠥⠆⠷⠋⠂ ⠹⠢⠍⠺⠱⠂ ⠸⠣⠣⠎ ⠹⠻⠆ ⠅⠋⠃⠣⠇⠁ ⠡⠪ ⠟⠕⠆ ⠅ ⠟⠭ ⠿⠪⠆⠸ ⠼ ⠅⠋⠃⠣⠇⠁ ⠟⠕⠆ ⠎⠣ ⠫ ⠿⠁⠆⠗⠪ ⠿⠓ ⠞⠣⠹⠪⠆⠞⠣⠡⠁⠆ ⠅⠋⠃⠣⠇⠁ ⠟⠕⠆ ⠎⠣ ⠅ ⠏⠣⠞⠞⠣⠾⠁⠆ ⠏⠴ ⠺⠣ ⠟⠕⠆ ⠓⠶⠆ ⠎⠣ ⠞⠭⠘⠑ ⠗ ⠞⠱⠂ ⠿⠪⠆ ⠎⠔⠆⠌⠮ ⠹⠺⠔⠆⠯ ⠞⠓⠁⠆ ⠿⠪⠆ ⠧ ⠏⠣⠞⠞⠣⠾⠁⠆ ⠺⠣ ⠞⠭⠘⠑ ⠅⠣ ⠏⠥⠂⠗⠺⠑ ⠒ ⠏⠕⠆⠗⠺⠣ ⠒ ⠶⠕⠅ ⠅ ⠎⠁⠆⠹⠴ ⠎ ⠡ ⠓⠌⠁ ⠏⠥⠂⠗⠺⠑ ⠒ ⠟⠔⠝⠪ ⠒ ⠞⠉⠏⠉ ⠚ ⠝⠱⠗⠁ ⠫ ⠫ ⠞⠱⠂ ⠑ ⠏⠣⠞⠞⠣⠾⠁⠆ ⠅ ⠞⠓⠁⠆ ⠊ ⠲
[2022-04-19 18:13:19] Best translation 2136 : ⠟⠞⠚ ⠗ ⠗⠔⠆⠠⠣⠪⠆ ⠹⠻⠆ ⠣⠟⠣⠽ ⠏⠔ ⠭ ⠇⠔⠂ ⠅⠣⠎⠁⠆ ⠒ ⠟⠞⠚ ⠋ ⠰⠣⠣ ⠋ ⠗⠱⠆ ⠗⠣ ⠒ ⠟⠞⠚ ⠟⠪⠂⠾⠔ ⠨⠋⠎⠁⠆ ⠹⠣⠇⠕ ⠋ ⠗⠱⠆ ⠗⠣ ⠒ ⠟⠶⠆ ⠿⠁⠞⠁ ⠟⠪⠆ ⠊ ⠋ ⠰⠣⠣ ⠗⠱⠆ ⠗⠣ ⠍ ⠲
[2022-04-19 18:13:19] Best translation 2137 : ⠎⠣⠅⠁⠆⠇⠉⠆ ⠅⠣⠇⠱⠆ ⠞⠺⠱ ⠎⠪ ⠅⠁ ⠗⠮ ⠗⠥⠞⠈⠕ ⠗⠱⠆ ⠟⠪⠂ ⠍⠮ ⠲
[2022-04-19 18:13:19] Best translation 2138 : ⠍⠣⠾⠣⠗⠔ ⠚ ⠣⠷⠢⠂ ⠅⠣ ⠹⠂ ⠨⠭ ⠅⠣ ⠅⠶⠆ ⠋ ⠏⠻ ⠹⠱⠆ ⠏⠁ ⠣⠷⠢⠂ ⠍⠔⠆⠹⠣⠍⠪⠆⠾ ⠹ ⠏⠺⠮⠆⠨⠔⠆ ⠅ ⠏⠴ ⠶ ⠍⠊⠍⠊ ⠊ ⠏⠔⠅ ⠣⠹⠋ ⠗ ⠟⠕⠆⠎⠁⠆⠯ ⠈⠕ ⠟⠣ ⠗⠣ ⠹ ⠲
[2022-04-19 18:13:19] Best translation 2139 : ⠰⠣⠪⠷⠋⠆⠿⠥⠂ ⠺⠥⠞⠁⠥⠂⠾ ⠒ ⠃⠁⠹⠁⠿⠋ ⠺⠥⠞⠁⠥⠂⠾ ⠅⠶⠆ ⠗⠁ ⠋ ⠟⠁⠆ ⠒ ⠡⠭ ⠒ ⠡⠭ ⠒ ⠙⠁⠆⠩⠣ ⠒ ⠡⠭ ⠒ ⠡⠭ ⠒ ⠡⠭ ⠎⠣⠹ ⠚ ⠰⠣⠁ ⠁⠔⠩⠁⠆ ⠹⠻⠆ ⠰⠣⠪⠷⠋⠆⠿⠥⠂ ⠺⠥⠞⠁⠥⠂⠾ ⠭ ⠹ ⠲
[2022-04-19 18:13:19] Best translation 2140 : ⠩⠱⠆⠨⠭ ⠎⠭⠹⠪ ⠞⠭ ⠥⠆ ⠊ ⠃⠣⠺⠣ ⠞⠭ ⠎⠱⠅ ⠞⠭ ⠏⠖⠆ ⠅ ⠁⠔⠓⠣⠞ ⠹⠻⠆ ⠖⠆⠡⠔⠆ ⠭ ⠹ ⠲
[2022-04-19 18:13:19] Best translation 2141 : ⠇⠱⠅⠿⠁ ⠞⠺ ⠇⠆ ⠣⠡⠁⠆ ⠹⠻⠆ ⠅⠶⠆ ⠅⠹ ⠥⠆⠨⠶⠆ ⠏⠖⠆ ⠒ ⠗⠔ ⠏⠖⠆ ⠒ ⠺⠋⠆⠃⠬ ⠏⠖⠆ ⠓⠥⠯ ⠩ ⠹ ⠲
[2022-04-19 18:13:19] Best translation 2142 : ⠅⠁⠞⠥⠝⠆ ⠈⠣⠗⠁⠟⠪⠆ ⠥⠆⠃⠣⠚⠋⠆ ⠲
[2022-04-19 18:13:19] Best translation 2143 : ⠵⠣⠾⠔⠆⠈⠺⠮⠆ ⠲
[2022-04-19 18:13:19] Best translation 2144 : ⠹⠺⠱⠆⠞⠥⠍⠺⠱⠆⠞⠥ ⠝⠺⠁⠆⠾ ⠅ ⠡⠥⠾ ⠒ ⠣⠈⠔⠞⠋⠎⠓⠁⠾ ⠈⠔ ⠿⠪⠆⠸ ⠸⠣⠮⠆⠽⠔ ⠞⠺ ⠍⠥⠞⠮⠯ ⠍⠶⠆ ⠇⠱⠂ ⠩ ⠹ ⠲
[2022-04-19 18:13:19] Best translation 2145 : ⠩⠔ ⠒ ⠨⠔⠃⠽⠁ ⠓ ⠁⠥⠆ ⠰⠣ ⠽⠔⠟⠱⠆⠹ ⠲
[2022-04-19 18:13:19] Best translation 2146 : ⠼⠊ ⠉ ⠙ ⠨⠥⠂ ⠞⠺ ⠏⠻⠏⠴ ⠨⠮⠂ ⠹⠻⠆ ⠡⠭ ⠹⠻⠆ ⠹ ⠣⠗⠱⠆ ⠞⠺ ⠅⠁⠆ ⠍⠔⠆⠞⠽⠟⠪⠆ ⠅⠣ ⠃⠣⠷⠁⠆⠙⠣⠇⠣ ⠣⠏⠻ ⠣⠾⠑ ⠞ ⠩⠯ ⠡⠭ ⠓⠥⠹⠻⠆ ⠽⠕⠆⠙⠣⠽⠁⠆ ⠟⠱⠆⠗⠺⠁ ⠞⠺ ⠟⠥⠝ ⠌⠁⠆ ⠽⠴ ⠗ ⠞⠓⠁⠆ ⠞ ⠍⠥ ⠹ ⠲
[2022-04-19 18:13:19] Best translation 2147 : ⠼⠁ ⠚ ⠲ ⠺⠁⠹⠣⠝⠁ ⠰⠶ ⠎⠺⠮⠆⠾⠮⠆ ⠝⠱ ⠹⠻⠆ ⠣⠇⠱⠂⠣⠟⠔⠂ ⠲
[2022-04-19 18:13:19] Best translation 2148 : ⠍⠶⠘⠕⠆⠎⠢ ⠹ ⠵⠣⠞⠹⠣⠃⠔⠏⠔⠷⠁ ⠅ ⠣⠡⠱⠨⠋ ⠰⠣⠣ ⠎⠣⠯ ⠹⠔⠽⠥ ⠇⠱⠂⠇⠁ ⠨⠮⠂ ⠹ ⠲
[2022-04-19 18:13:19] Best translation 2149 : ⠗⠣⠞⠥⠂ ⠒ ⠞⠱⠆⠁⠣⠞ ⠚ ⠞⠺ ⠝⠋⠆ ⠍⠥ ⠝⠋⠆ ⠗⠁ ⠅ ⠞⠺⠱⠂ ⠝ ⠹ ⠲
[2022-04-19 18:13:19] Best translation 2150 : ⠪ ⠣⠨⠁ ⠌⠣⠞⠁ ⠅⠣ ⠃⠁⠳ ⠏ ⠇⠮⠆ ⠿ ⠓ ⠸⠽⠴ ⠗⠁ ⠝⠋⠆⠞⠻ ⠅⠣ ⠝⠔ ⠰⠣⠣ ⠎⠁ ⠋ ⠞⠣⠞ ⠃⠮⠆ ⠝⠮⠂ ⠌⠁ ⠗⠱⠆ ⠞⠮⠂ ⠎⠁ ⠞⠺⠱ ⠡⠪⠆⠍⠥⠝⠆ ⠏⠁⠸ ⠌ ⠏⠁ ⠏⠭⠗⠣ ⠝⠱ ⠰⠣⠁ ⠏⠻⠂ ⠲
[2022-04-19 18:13:19] Best translation 2151 : ⠝⠱⠂⠞⠖⠆ ⠰⠣⠁ ⠅⠁⠆ ⠡⠭ ⠹ ⠣⠎⠁ ⠩⠁⠯ ⠿⠋ ⠹ ⠩ ⠧ ⠈⠱⠅ ⠹⠁⠆⠌⠮ ⠚ ⠹ ⠣⠍⠊ ⠾⠑⠠⠣⠁ ⠅ ⠟⠪⠂ ⠅⠉ ⠑ ⠇⠬ ⠹⠅⠹ ⠌⠣ ⠹⠁⠆ ⠒ ⠌⠣ ⠹⠣⠍⠪⠆ ⠚ ⠹ ⠾⠱⠰⠣⠉⠂ ⠣⠇⠢⠆⠇⠢⠆ ⠅⠣⠞ ⠹⠻⠆ ⠅⠕ ⠿⠓ ⠣⠍⠊ ⠙ ⠅⠣⠞⠯ ⠱ ⠊ ⠲
[2022-04-19 18:13:19] Best translation 2152 : ⠪ ⠁⠑ ⠇⠥⠝⠯ ⠈⠋⠆⠟⠮ ⠇⠽⠴⠏⠣⠞ ⠹⠻⠆ ⠣⠽ ⠅ ⠟⠥ ⠋ ⠞⠣⠞ ⠛ ⠓ ⠈⠕ ⠊ ⠲
[2022-04-19 18:13:19] Best translation 2153 : ⠹⠥⠌⠮⠡⠔⠆ ⠏⠱⠆ ⠞⠮⠂ ⠿⠱ ⠍⠥⠞⠮ ⠿⠪⠆ ⠿⠋ ⠗⠱⠆ ⠟ ⠗⠣⠶ ⠲
[2022-04-19 18:13:19] Best translation 2154 : ⠟⠥⠚ ⠹ ⠪ ⠍⠊⠞⠣⠈⠕⠆ ⠩⠔⠿⠥⠂ ⠅ ⠣⠇⠥⠝ ⠹⠣⠝⠁⠆ ⠎⠞⠝ ⠩ ⠇⠁ ⠟⠣ ⠹ ⠗ ⠥⠆⠎⠋⠩⠺⠱ ⠗ ⠞⠖⠏⠔ ⠅⠁ ⠣⠸⠣⠥ ⠱⠝ ⠞⠺ ⠷⠣ ⠱⠅⠯ ⠞⠣⠞ ⠝ ⠹⠣⠓⠾⠣ ⠡⠭ ⠈⠉⠆⠿⠓⠣⠞ ⠇⠬ ⠟ ⠃ ⠹ ⠲
[2022-04-19 18:13:19] Best translation 2155 : ⠟⠑⠥⠂ ⠿⠦ ⠹ ⠲
[2022-04-19 18:13:19] Best translation 2156 : ⠽⠨ ⠏⠔ ⠣⠈⠱⠅ ⠇⠥⠆ ⠹⠻⠆ ⠾⠁⠆ ⠿⠓ ⠏⠭ ⠹⠣⠞ ⠋⠂ ⠲
[2022-04-19 18:13:19] Best translation 2157 : ⠺⠋⠆⠹⠁⠁⠆⠗⠣ ⠒ ⠍⠣⠽⠁⠆ ⠅⠣ ⠞⠭ ⠹⠺⠮ ⠲
[2022-04-19 18:13:19] Best translation 2158 : ⠺⠱ ⠺⠱⠂ ⠺⠱⠆ ⠲
[2022-04-19 18:13:19] Best translation 2159 : ⠿⠋⠯ ⠹⠉⠆⠹⠣⠞ ⠟⠪⠂ ⠏ ⠸ ⠾⠋⠍⠁ ⠃⠁⠹⠁⠎⠣⠅⠁⠆ ⠞⠺ ⠣⠗⠱⠆ ⠑⠨⠣⠗⠁ ⠩ ⠞⠓⠁⠆ ⠿⠪⠆ ⠭ ⠹⠿ ⠣⠗⠱⠆ ⠗ ⠣⠘⠣⠞ ⠓⠥⠯ ⠠⠣⠭ ⠾⠕⠆ ⠩ ⠱ ⠹ ⠲
[2022-04-19 18:13:19] Best translation 2160 : ⠋ ⠇⠆ ⠋ ⠁⠖ ⠗⠣ ⠲
[2022-04-19 18:13:19] Best translation 2161 : ⠼⠁ ⠲ ⠴⠏⠁ ⠎⠣⠅⠁⠆⠇⠉⠆ ⠚ ⠊ ⠣⠝⠑ ⠣⠙⠱⠅⠏⠮ ⠅ ⠣⠃⠊⠙⠋ ⠞⠺ ⠩⠁ ⠏ ⠲
[2022-04-19 18:13:19] Best translation 2162 : ⠹⠔⠨⠋⠆⠎⠁ ⠣⠟⠔⠆ ⠲
[2022-04-19 18:13:19] Best translation 2163 : ⠡⠭⠸⠣⠣⠎ ⠹⠻⠆ ⠹⠁⠆ ⠲
[2022-04-19 18:13:19] Best translation 2164 : ⠓⠕ ⠩⠱⠂ ⠅⠣ ⠈⠥⠷⠋ ⠈⠥⠷⠋ ⠒ ⠃⠁ ⠹⠋ ⠇⠕⠂ ⠍⠱⠆ ⠲
[2022-04-19 18:13:19] Best translation 2165 : ⠍⠔⠛⠣⠇⠁⠏⠁ ⠲
[2022-04-19 18:13:19] Best translation 2166 : ⠍⠊⠍⠊ ⠞⠪ ⠹⠻⠆ ⠿ ⠡⠭ ⠒ ⠸⠣⠥ ⠨⠮⠂ ⠹⠻⠆ ⠟⠥⠝ ⠗ ⠺⠥⠞⠁⠥⠂ ⠏⠭⠎⠪⠆ ⠣⠎⠥⠂⠎⠥⠂ ⠅ ⠠⠣⠶⠆⠇⠥ ⠚ ⠿⠓⠑⠈⠪⠆ ⠠⠣⠱⠅⠎⠑ ⠍⠂ ⠗⠋ ⠰⠣⠣ ⠅⠁⠅⠺⠮ ⠇⠕ ⠡ ⠭ ⠹ ⠲
[2022-04-19 18:13:19] Total time: 190.24965s wall

real	3m13.030s
user	6m19.106s
sys	0m3.193s
[2022-04-19 18:13:19] [marian] Marian v1.10.0 6f6d4846 2021-02-06 15:35:16 -0800
[2022-04-19 18:13:19] [marian] Running on administrator-HP-Z2-Tower-G4-Workstation as process 544172 with command line:
[2022-04-19 18:13:19] [marian] marian-decoder --models ./model.s2s-brmy/model.iter55000.npz ./model.transformer-brmy/model0-brmy.iter80000.npz --weights 0.4 0.6 --max-length 200 --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml --maxi-batch 64 --workspace 500 --output ./model.ensemble/hyp.0.4-0.6.my --devices 0 1
[2022-04-19 18:13:19] [config] alignment: ""
[2022-04-19 18:13:19] [config] allow-unk: false
[2022-04-19 18:13:19] [config] authors: false
[2022-04-19 18:13:19] [config] beam-size: 12
[2022-04-19 18:13:19] [config] bert-class-symbol: "[CLS]"
[2022-04-19 18:13:19] [config] bert-mask-symbol: "[MASK]"
[2022-04-19 18:13:19] [config] bert-masking-fraction: 0.15
[2022-04-19 18:13:19] [config] bert-sep-symbol: "[SEP]"
[2022-04-19 18:13:19] [config] bert-train-type-embeddings: true
[2022-04-19 18:13:19] [config] bert-type-vocab-size: 2
[2022-04-19 18:13:19] [config] best-deep: false
[2022-04-19 18:13:19] [config] build-info: ""
[2022-04-19 18:13:19] [config] cite: false
[2022-04-19 18:13:19] [config] cpu-threads: 0
[2022-04-19 18:13:19] [config] dec-cell: lstm
[2022-04-19 18:13:19] [config] dec-cell-base-depth: 2
[2022-04-19 18:13:19] [config] dec-cell-high-depth: 2
[2022-04-19 18:13:19] [config] dec-depth: 2
[2022-04-19 18:13:19] [config] devices:
[2022-04-19 18:13:19] [config]   - 0
[2022-04-19 18:13:19] [config]   - 1
[2022-04-19 18:13:19] [config] dim-emb: 512
[2022-04-19 18:13:19] [config] dim-rnn: 1024
[2022-04-19 18:13:19] [config] dim-vocabs:
[2022-04-19 18:13:19] [config]   - 18364
[2022-04-19 18:13:19] [config]   - 18602
[2022-04-19 18:13:19] [config] dump-config: ""
[2022-04-19 18:13:19] [config] enc-cell: lstm
[2022-04-19 18:13:19] [config] enc-cell-depth: 2
[2022-04-19 18:13:19] [config] enc-depth: 2
[2022-04-19 18:13:19] [config] enc-type: alternating
[2022-04-19 18:13:19] [config] ignore-model-config: false
[2022-04-19 18:13:19] [config] input:
[2022-04-19 18:13:19] [config]   - stdin
[2022-04-19 18:13:19] [config] input-types:
[2022-04-19 18:13:19] [config]   []
[2022-04-19 18:13:19] [config] interpolate-env-vars: false
[2022-04-19 18:13:19] [config] layer-normalization: true
[2022-04-19 18:13:19] [config] lemma-dim-emb: 0
[2022-04-19 18:13:19] [config] log: ""
[2022-04-19 18:13:19] [config] log-level: info
[2022-04-19 18:13:19] [config] log-time-zone: ""
[2022-04-19 18:13:19] [config] max-length: 200
[2022-04-19 18:13:19] [config] max-length-crop: false
[2022-04-19 18:13:19] [config] max-length-factor: 3
[2022-04-19 18:13:19] [config] maxi-batch: 64
[2022-04-19 18:13:19] [config] maxi-batch-sort: none
[2022-04-19 18:13:19] [config] mini-batch: 1
[2022-04-19 18:13:19] [config] mini-batch-words: 0
[2022-04-19 18:13:19] [config] models:
[2022-04-19 18:13:19] [config]   - ./model.s2s-brmy/model.iter55000.npz
[2022-04-19 18:13:19] [config]   - ./model.transformer-brmy/model0-brmy.iter80000.npz
[2022-04-19 18:13:19] [config] n-best: false
[2022-04-19 18:13:19] [config] no-spm-decode: false
[2022-04-19 18:13:19] [config] normalize: 0
[2022-04-19 18:13:19] [config] num-devices: 0
[2022-04-19 18:13:19] [config] output: ./model.ensemble/hyp.0.4-0.6.my
[2022-04-19 18:13:19] [config] output-approx-knn:
[2022-04-19 18:13:19] [config]   []
[2022-04-19 18:13:19] [config] output-omit-bias: false
[2022-04-19 18:13:19] [config] output-sampling: false
[2022-04-19 18:13:19] [config] precision:
[2022-04-19 18:13:19] [config]   - float32
[2022-04-19 18:13:19] [config] quiet: false
[2022-04-19 18:13:19] [config] quiet-translation: false
[2022-04-19 18:13:19] [config] relative-paths: false
[2022-04-19 18:13:19] [config] right-left: false
[2022-04-19 18:13:19] [config] seed: 0
[2022-04-19 18:13:19] [config] shortlist:
[2022-04-19 18:13:19] [config]   []
[2022-04-19 18:13:19] [config] skip: true
[2022-04-19 18:13:19] [config] skip-cost: false
[2022-04-19 18:13:19] [config] tied-embeddings: true
[2022-04-19 18:13:19] [config] tied-embeddings-all: false
[2022-04-19 18:13:19] [config] tied-embeddings-src: false
[2022-04-19 18:13:19] [config] transformer-aan-activation: swish
[2022-04-19 18:13:19] [config] transformer-aan-depth: 2
[2022-04-19 18:13:19] [config] transformer-aan-nogate: false
[2022-04-19 18:13:19] [config] transformer-decoder-autoreg: self-attention
[2022-04-19 18:13:19] [config] transformer-depth-scaling: false
[2022-04-19 18:13:19] [config] transformer-dim-aan: 2048
[2022-04-19 18:13:19] [config] transformer-dim-ffn: 2048
[2022-04-19 18:13:19] [config] transformer-ffn-activation: swish
[2022-04-19 18:13:19] [config] transformer-ffn-depth: 2
[2022-04-19 18:13:19] [config] transformer-guided-alignment-layer: last
[2022-04-19 18:13:19] [config] transformer-heads: 8
[2022-04-19 18:13:19] [config] transformer-no-projection: false
[2022-04-19 18:13:19] [config] transformer-pool: false
[2022-04-19 18:13:19] [config] transformer-postprocess: dan
[2022-04-19 18:13:19] [config] transformer-postprocess-emb: d
[2022-04-19 18:13:19] [config] transformer-postprocess-top: ""
[2022-04-19 18:13:19] [config] transformer-preprocess: ""
[2022-04-19 18:13:19] [config] transformer-tied-layers:
[2022-04-19 18:13:19] [config]   []
[2022-04-19 18:13:19] [config] transformer-train-position-embeddings: false
[2022-04-19 18:13:19] [config] tsv: false
[2022-04-19 18:13:19] [config] tsv-fields: 0
[2022-04-19 18:13:19] [config] type: s2s
[2022-04-19 18:13:19] [config] ulr: false
[2022-04-19 18:13:19] [config] ulr-dim-emb: 0
[2022-04-19 18:13:19] [config] ulr-trainable-transformation: false
[2022-04-19 18:13:19] [config] version: v1.10.0 6f6d4846 2021-02-06 15:35:16 -0800
[2022-04-19 18:13:19] [config] vocabs:
[2022-04-19 18:13:19] [config]   - /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml
[2022-04-19 18:13:19] [config]   - /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml
[2022-04-19 18:13:19] [config] weights:
[2022-04-19 18:13:19] [config]   - 0.4
[2022-04-19 18:13:19] [config]   - 0.6
[2022-04-19 18:13:19] [config] word-penalty: 0
[2022-04-19 18:13:19] [config] word-scores: false
[2022-04-19 18:13:19] [config] workspace: 500
[2022-04-19 18:13:19] [config] Loaded model has been created with Marian v1.10.0 6f6d4846 2021-02-06 15:35:16 -0800
[2022-04-19 18:13:19] [data] Loading vocabulary from JSON/Yaml file /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml
[2022-04-19 18:13:19] [data] Loading vocabulary from JSON/Yaml file /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml
[2022-04-19 18:13:20] [memory] Extending reserved space to 512 MB (device gpu0)
[2022-04-19 18:13:20] [memory] Extending reserved space to 512 MB (device gpu1)
[2022-04-19 18:13:20] Loading scorer of type s2s as feature F0
[2022-04-19 18:13:20] Loading scorer of type s2s as feature F0
[2022-04-19 18:13:20] Loading scorer of type transformer as feature F1
[2022-04-19 18:13:20] Loading scorer of type transformer as feature F1
[2022-04-19 18:13:20] Loading model from ./model.s2s-brmy/model.iter55000.npz
[2022-04-19 18:13:20] Loading model from ./model.s2s-brmy/model.iter55000.npz
[2022-04-19 18:13:24] Loading model from ./model.transformer-brmy/model0-brmy.iter80000.npz
[2022-04-19 18:13:24] Loading model from ./model.transformer-brmy/model0-brmy.iter80000.npz
[2022-04-19 18:13:26] [memory] Reserving 536 MB, device gpu0
[2022-04-19 18:13:26] [memory] Reserving 536 MB, device gpu1
[2022-04-19 18:13:26] [gpu] 16-bit TensorCores enabled for float32 matrix operations
[2022-04-19 18:13:31] Best translation 0 : ၂ ။ အောက်ပါ စကားလုံးများ ဖြင့် ဝါကျ ဖွဲ့ပြ ပါ ။
[2022-04-19 18:13:31] Best translation 1 : ထိုအခါ ဗျိုင်း သည် ငါး တို့ ကို တစ် ကောင် စီ ချီ၍ အိုင် ၏ အနီး ၌ ရှိ သော ဦးနှောက် ၏ သလွန်တော် ၌ မြင်မြော် စား ပြီးသော် အရိုး တို့ ကို စေ့စေ့စပ်စပ် ပင်ရင်း သို့ ပစ်ချ လေ ၏ ။
[2022-04-19 18:13:31] Best translation 2 : ( ဆ ) သင်တို့ သည် နိုင်ငံတော်အလံ ကို အဘယ်ကြောင့် အလေးပြု ကြ သနည်း ။
[2022-04-19 18:13:31] Best translation 3 : ၂ ။ ဒေါက်တို က ညီနောင် လေး ဦး ကို ဘယ်လို ပြော သလဲ ။
[2022-04-19 18:13:31] Best translation 4 : ထို့ပြင် ကျောက်စာ စ၍ ၊ ကြင် စာရေး ၊ သတင်းစာတိုက် စာရေး စသည် ဖြင့် လည်း ဘဝ မျိုးစုံ ကျင်လည် ဖူး သည် ။
[2022-04-19 18:13:31] Best translation 5 : ဤသို့ဖြင့် မီးရထား သည် ဘူတာရုံ အနီး ကို ချဉ်းကပ် လာ လေ သည် ။
[2022-04-19 18:13:31] Best translation 6 : ပြိုက် ရှိုက် ။
[2022-04-19 18:13:31] Best translation 7 : ၁ ၄ ။ ကျီစား = ကစား သည် ။ ပြက်ရယ် ပြု သည် ။
[2022-04-19 18:13:31] Best translation 8 : ၁ ။ ချိုင့်ဝှမ်း = မြေ မြင့် နှစ် ခု အကြား ရှိ လဟာပြင်ကျယ် သော အရပ် ။
[2022-04-19 18:13:31] Best translation 9 : အောက်ပါ စကားလုံးများ ၏ စာလုံးပေါင်း သတ်ပုံ ကို လေ့ကျင့် ပါ ။
[2022-04-19 18:13:31] Best translation 10 : ၄ ။ ပေးစာ ကို ဖတ် ပြီးနောက် သင့် တွင် မည်သည့် စိတ်ခံစား မှုများ ဖြစ်ပေါ် လာ သနည်း ။
[2022-04-19 18:13:31] Best translation 11 : ဗူဒီး နင် ခါနာ မ စား ဘူး ။
[2022-04-19 18:13:31] Best translation 12 : တည်း ။
...
...
...
[2022-04-19 18:23:01] Best translation 2130 : ၃ ။ ဖွာ ရ ရာ = စုစည်း ခြင်း မ ရှိ ၊ ကွဲ ဖျာ ထွက် လျက် ။
[2022-04-19 18:23:01] Best translation 2131 : မိမိ ကိုယ်တိုင် အသံနေအသံထား ဖြင့် ရွတ်ဆို လေ့ကျင့် ပါ ။
[2022-04-19 18:23:01] Best translation 2132 : ( ခ ) တစ်ဥတု လျှင် ------ စီ ကြာမြင့် ပါ သည် ။
[2022-04-19 18:23:01] Best translation 2133 : ညောင်ပင်သာရွာ ဖြူး မြို့နယ် ၁ ၃ ၄ ၅ ခု ၊ တန်ခူး လဆန်း ၁ ရက် သူငယ်ချင်း စ၍ သူငယ်ချင်း ထံသို့ စွန့်ပစ်၍ စာရေးလိုက် ပါ သည် ။
[2022-04-19 18:23:01] Best translation 2134 : ၈ ။ အားသန် = မ ရ မ နေ မ ဖြစ် မ နေ အားထုတ် ကြိုးပမ်း သည် ။
[2022-04-19 18:23:01] Best translation 2135 : ပျားရည် သာ ဆောင်ယူ ကြ ချေ ဟု ဆို၍ ပျားရည် ကို ဆောင်ယူ စေ ပြီး သော် ပတ္တမြား ၌ အပေါက်ဝ နှစ် ဖက် ကို လိမ်းသုတ် ပြီး မှ နူးညံ့ သိမ်မွေ့ လှစွာ သော ကမ္ဗလာ ချည် ကြိုး ကို ကျစ် ပြီးလျှင် ထို ကမ္ဗလာ ကြိုး စ ၌ ပျားရည် ဖြင့် စိတ်ဖြာ ကမ္ဗလာ ကြိုး စ ကို ပတ္တမြား ပေါက် ဝ ကြိုး ဟောင်း စ တစ်ဖက် နှင့် တေ့ ပြီး စဉ်းငယ် သွင်း၍ ထား ပြီး သော် ပတ္တမြား ဝ တစ်ဖက် က ပုရွက် ၊ ပိုးရွ ၊ စီခြား ကို စားသောက် စေ ခြင်း ငှာ ပုရွက် ၊ ကျဉ်နီ ၊ စုဖုရားလတ် တို့ နေရာ တို့ ၌ တေ့ လျက် ပတ္တမြား ထား ၏ ။
[2022-04-19 18:23:01] Best translation 2136 : ကျွန်တော်တို့ နှင့် ရင်းနှီး သော အကြောင်းအရာ ပင် ဖြစ် လင့် ကစား ၊ ကျွန်တော်တို့ ရယ် မှ မ ရေး ရ ၊ ကျွန်တော်တို့ ကြည့်မြင် ခံစား သလို မ ရေး ရ ၊ ကျောင်း ပြာတာ ကြီး ၏ ရန်သူကြီး မှ ရေး ရ မည် ။
[2022-04-19 18:23:01] Best translation 2137 : စကားလုံး ကလေး တွေ စီ ကာ ရယ် ရွတ်ဆို ရေး ကြည့် မယ် ။
[2022-04-19 18:23:01] Best translation 2138 : မမြရင် တို့ အငြိမ့် က သည့် ခေတ် က စ၍ မ ပေါ် သေး ပါ အငြိမ့် မင်းသမီးများ သည် ပွဲခင်း ကို ပေါက် အောင် မိမိ ၏ ပင်ကို အသံ နှင့် ကြိုးစား၍ ဆို ကြ ရ သည် ။
[2022-04-19 18:23:01] Best translation 2139 : မှီငြမ်းပြု ဝတ္ထုများ ၊ ဘာသာပြန် ဝတ္ထုများ ကို ရာ တကြောင်း သည် ၊ မုခ်တံကဲများ ၊ ဦးငွေကိုင် ၊ ကြမ်းတိုက် ၊ သု ၊ ဦးငွေကိုင် ၊ လူလုံးပြ စသည် တို့ မှာ ထင်ရှား သော မှီငြမ်းပြု ဝတ္ထုများ ဖြစ် သည် ။
[2022-04-19 18:23:01] Best translation 2140 : ရှေးခေတ် စစ်သည် တစ် ဦး ၏ ဘဝ တစ် စိတ် တစ် ပိုင်း ကို ထင်ဟပ် သော အိုင်းချင်း ဖြစ် သည် ။
[2022-04-19 18:23:01] Best translation 2141 : လိပ်ပြာ တွင် လည်း အခြား သော သတ္ထု ကဲ့သို့ ဦးခေါင်း ပိုင်း ၊ ရင် ပိုင်း ၊ ဝမ်းဗိုက် ပိုင်း ဟူ၍ ရှိ သည် ။
[2022-04-19 18:23:01] Best translation 2142 : ကာတွန်း ဆရာကြီး ဦးဘဂျမ်း ။
[2022-04-19 18:23:01] Best translation 2143 : ဈမျဉ်းဆွဲ ။
[2022-04-19 18:23:01] Best translation 2144 : သွေးတူမွေးတူ နွားများ ကို ချူများ ၊ အဆင်တန်ဆာများ ဆင် ပြီးလျှင် လှည်းယဉ် တွင် အထက်ဆုံး မောင်း လေ့ ရှိ သည် ။
[2022-04-19 18:23:01] Best translation 2145 : ရှင် ၊ ခင်ဗျာ ဟု ထူး မှ ယဉ်ကျေးသည် ။
[2022-04-19 18:23:01] Best translation 2146 : ၉ ၃ ၄ ခု တွင် ပေါ်ပေါက် ခဲ့ သော အသားရောင် စီ သည် အရေး တွင် ကား မင်းတရားကြီး က ဗညားဒလ အပေါ် အမျက် တော် ရှိ၍ စ၍ ဟူသော ယိုးဒယား ကျေးရွာ တွင် ကျွန် ငါး ယောက် နှင့် ထား တော် မူ သည် ။
[2022-04-19 18:23:01] Best translation 2147 : ၁ ၀ ။ ဝါသနာ = စွဲမြဲ နေ သော အလေ့အကျင့် ။
[2022-04-19 18:23:01] Best translation 2148 : မောင်ဖိုးစိန် သည် ဇာတ်သဘင်ပညာ ကို အခြေခံ မှ စ၍ သင်ယူ လေ့လာ ခဲ့ သည် ။
[2022-04-19 18:23:01] Best translation 2149 : ရတု ၊ တေးထပ် တို့ တွင် နန်း မူ နန်း ရာ ကို တွေ့ နိုင် သည် ။
[2022-04-19 18:23:01] Best translation 2150 : ဤ အခါ ငတာ က ဘာကြောင့် ပါ လည်း ဘုရား ဟု လျှောက် ရာ အရှင့် က နင် မှ စာ မ တတ် ဘဲ နဲ့ ငါ ရေး တဲ့ စာ တွေ ချီးမွမ်း ပါလျှင် ငါ ပါ ပစ်ရ နေ မှာ ပေါ့ ။
[2022-04-19 18:23:01] Best translation 2151 : နေ့တိုင်း မှာ ကား တောသူတောင်သား သည် အစာ ရှာ၍ ပြန် သည် ရှိ သော် ဆိတ် သားငယ် တို့ သည် အမိ မျက်နှာ ကို ကြည့် ကုန် လျက် လိုက် သကဲ့သို့ ငါ့ သား ၊ ငါ့ သမီး တို့ သည် မြေမှုန့် အလိမ်းလိမ်း ကပ် သော ကိုယ် ဖြင့် အမိ သို့ ကပ်၍ နေ ၏ ။
[2022-04-19 18:23:01] Best translation 2152 : ဤ ထက် လွန်၍ ဆန်းကြယ် လျောက်ပတ် သော အရာ ကို ကျွန်ုပ် မ တတ် ပြီ ဟု ဆို ၏ ။
[2022-04-19 18:23:01] Best translation 2153 : သူငယ်ချင်း ပေး တဲ့ ဦးဖိုးနု မူတည် ပြီး ပြန် ရေး ကြ ရအောင် ။
[2022-04-19 18:23:01] Best translation 2154 : ကျွန်ုပ်တို့ သည် ဤ မိတဆိုး ရှင်ပြု ကို အလွန် သနား စေတနာ ရှိ လာ ကြ သည် နှင့် ဦးစံရွှေ နှင့် တိုင်ပင် ကာ အလှူ အိမ် တွင် ည အိပ်၍ တတ် နိုင် သမျှ လေ့ကျင့် ဆုံးဖြတ် လိုက် ကြ လေ သည် ။
[2022-04-19 18:23:01] Best translation 2155 : ကြက်ဥ ပြုတ် သည် ။
[2022-04-19 18:23:01] Best translation 2156 : ယခု ပင် အဆိပ် လူး သော မြား ဖြင့် ပစ် သတ် အံ့ ။
[2022-04-19 18:23:01] Best translation 2157 : ဝမ်းသာအားရ ၊ မယား က တစ် သွယ် ။
[2022-04-19 18:23:01] Best translation 2158 : ဝေ ဝေ့ ဝေး ။
[2022-04-19 18:23:01] Best translation 2159 : ပြန်၍ သုံးသပ် ကြည့် ပါ လျှင် မြန်မာ ဘာသာစကား တွင် အရေး အက္ခရာ ရှိ ထား ပြီး ဖြစ် သဖြင့် အရေး နှင့် အဖတ် ဟူ၍ နှစ် မျိုး ရှိ နေ သည် ။
[2022-04-19 18:23:01] Best translation 2160 : လေ့ကျင့် လည်း မ ထိုင် ရ ။
[2022-04-19 18:23:01] Best translation 2161 : ၁ ။ အောက်ပါ စကားလုံး တို့ ၏ အနက် အဓိပ္ပာယ် ကို အဘိဓာန် တွင် ရှာ ပါ ။
[2022-04-19 18:23:01] Best translation 2162 : သင်ခန်းစာ အကျဉ်း ။
[2022-04-19 18:23:01] Best translation 2163 : ချစ်လှစွာ သော သား ။
[2022-04-19 18:23:01] Best translation 2164 : ဟို ရှေ့ က ဆူညံ ဆူညံ ၊ ဘာ သံ လို့ မေး ။
[2022-04-19 18:23:01] Best translation 2165 : စွတ် ။
[2022-04-19 18:23:01] Best translation 2166 : မိမိ တည် သော ဘုရား ကိုးဆူ ၊ လှူ ခဲ့ သော ကျွန် နှင့် ဝတ္ထု ပစ္စည်း အစုစု ကို နှောင်းလူ တို့ ဖျက်ဆီး နှိပ်စက် မည့် ရန် မှ ကာကွယ် လို ခြင်း ဖြစ် သည် ။
[2022-04-19 18:23:01] Total time: 190.54654s wall

real	3m12.139s
user	6m19.695s
sys	0m2.973s

real	19m40.644s
user	38m9.828s
sys	0m21.457s
```

output folder ကို ကြည့်တော့ အဆင်ပြေပြေနဲ့ decode လုပ်သွားတဲ့ပုံရှိတယ်။  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.ensemble$ wc *
   2167   28719  275248 hyp.0.4-0.6.br
   2167   28681  376482 hyp.0.4-0.6.my
   2167   28719  272346 hyp.0.5-0.5.br
   2167   28676  375116 hyp.0.5-0.5.my
   2167   28721  270899 hyp.0.6-0.4.br
   2167   28680  373681 hyp.0.6-0.4.my
  13002  172196 1943772 total
(base) ye@:/media/ye/project2/exp/braille-nmt/model.ensemble$
```

translated ဖိုင်တွေကို head command နဲ့ စစ်ကြည့်ခဲ့...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.ensemble$ head -3 *.br
==> hyp.0.4-0.6.br <==
⠼⠃ ⠲ ⠴⠏ ⠎⠣⠅⠁⠆⠇⠉⠆⠾ ⠿⠓ ⠺⠁⠟⠣ ⠘⠺⠮⠂⠿⠣ ⠏ ⠲
⠼⠣⠨⠁ ⠃⠽⠖⠆ ⠹ ⠌⠁⠆ ⠚ ⠅ ⠞⠭ ⠅⠶ ⠎⠪ ⠡⠪⠯ ⠖ ⠊ ⠣⠝⠪⠆ ⠫ ⠩ ⠹⠻⠆ ⠡⠭ ⠊ ⠹⠣⠇⠥⠝⠞⠻ ⠫ ⠍⠢⠂ ⠎⠁⠆ ⠿⠪⠆⠧ ⠣⠗⠕⠆ ⠚ ⠅ ⠁⠆⠟⠣⠯ ⠏⠔⠗⠔⠆ ⠙ ⠏⠭⠡⠣ ⠃ ⠊ ⠲
⠶ ⠈⠣ ⠶ ⠹⠔⠚ ⠹ ⠝⠌⠞⠣⠇⠋ ⠅ ⠣⠃⠮⠳ ⠣⠇⠱⠆⠿⠥⠂ ⠟ ⠹⠝ ⠲

==> hyp.0.5-0.5.br <==
⠼⠃ ⠲ ⠴⠏ ⠎⠣⠅⠁⠆⠇⠉⠆⠾ ⠿⠓ ⠺⠁⠟⠣ ⠘⠺⠮⠂⠿⠣ ⠏ ⠲
⠼⠣⠨⠁ ⠃⠽⠖⠆ ⠹ ⠌⠁⠆ ⠚ ⠅ ⠞⠭ ⠅⠶ ⠎⠪ ⠡⠪⠯ ⠖ ⠊ ⠣⠝⠪⠆ ⠫ ⠩ ⠹⠻⠆ ⠡⠭ ⠊ ⠹⠣⠇⠥⠝⠞⠻ ⠫ ⠍⠢⠂ ⠎⠁⠆ ⠿⠪⠆⠧ ⠣⠗⠕⠆ ⠚ ⠅ ⠁⠆⠟⠣⠯ ⠏⠔⠗⠔⠆ ⠙ ⠏⠭⠡⠣ ⠃ ⠊ ⠲
⠶ ⠈⠣ ⠶ ⠹⠔⠚ ⠹ ⠝⠌⠞⠣⠇⠋ ⠅ ⠣⠃⠮⠳ ⠣⠇⠱⠆⠿⠥⠂ ⠟ ⠹⠝ ⠲

==> hyp.0.6-0.4.br <==
⠼⠃ ⠲ ⠴⠏ ⠎⠣⠅⠁⠆⠇⠉⠆⠾ ⠿⠓ ⠺⠁⠟⠣ ⠘⠺⠮⠂⠿⠣ ⠏ ⠲
⠼⠣⠨⠁ ⠃⠽⠖⠆ ⠹ ⠌⠁⠆ ⠚ ⠅ ⠞⠭ ⠅⠶ ⠎⠪ ⠡⠪⠯ ⠖ ⠊ ⠣⠝⠪⠆ ⠫ ⠩ ⠹⠻⠆ ⠡⠭ ⠊ ⠋ ⠫ ⠡⠭ ⠎⠁⠆ ⠿⠪⠆⠧ ⠣⠗⠕⠆ ⠚ ⠅ ⠋ ⠏⠔⠗⠔⠆ ⠙ ⠏⠭⠡⠣ ⠃ ⠊ ⠲
⠶ ⠈⠣ ⠶ ⠹⠔⠚ ⠹ ⠝⠌⠞⠣⠇⠋ ⠅ ⠣⠃⠮⠳ ⠣⠇⠱⠆⠿⠥⠂ ⠟ ⠹⠝ ⠲
(base) ye@:/media/ye/project2/exp/braille-nmt/model.ensemble$ head -3 *.my
==> hyp.0.4-0.6.my <==
၂ ။ အောက်ပါ စကားလုံးများ ဖြင့် ဝါကျ ဖွဲ့ပြ ပါ ။
ထိုအခါ ဗျိုင်း သည် ငါး တို့ ကို တစ် ကောင် စီ ချီ၍ အိုင် ၏ အနီး ၌ ရှိ သော ဦးနှောက် ၏ သလွန်တော် ၌ မြင်မြော် စား ပြီးသော် အရိုး တို့ ကို စေ့စေ့စပ်စပ် ပင်ရင်း သို့ ပစ်ချ လေ ၏ ။
( ဆ ) သင်တို့ သည် နိုင်ငံတော်အလံ ကို အဘယ်ကြောင့် အလေးပြု ကြ သနည်း ။

==> hyp.0.5-0.5.my <==
၂ ။ အောက်ပါ စကားလုံးများ ဖြင့် ဝါကျ ဖွဲ့ပြ ပါ ။
ထိုအခါ ဗျိုင်း သည် ငါး တို့ ကို တစ် ကောင် စီ ချီ၍ အိုင် ၏ အနီး ၌ ရှိ သော ဦးနှောက် ၏ သလွန်တော် ၌ မြင်မြော် စား ပြီးသော် အရိုး တို့ ကို အမွှေးနံ့သာရည် ပင်ရင်း သို့ ပစ်ချ လေ ၏ ။
( ဆ ) သင်တို့ သည် နိုင်ငံတော်အလံ ကို အဘယ်ကြောင့် အလေးပြု ကြ သနည်း ။

==> hyp.0.6-0.4.my <==
၂ ။ အောက်ပါ စကားလုံးများ ဖြင့် ဝါကျ ဖွဲ့ပြ ပါ ။
ထိုအခါ ဗျိုင်း သည် ငါး တို့ ကို တစ် ကောင် စီ ချီ၍ အိုင် ၏ အနီး ၌ ရှိ သော ဦးနှောက် ၏ သလွန်တော် ၌ မြင်မြော် စား ပြီးသော် အရိုး တို့ ကို စ၍ ပင်ရင်း သို့ ပစ်ချ လေ ၏ ။
( ဆ ) သင်တို့ သည် နိုင်ငံတော်အလံ ကို အဘယ်ကြောင့် အလေးပြု ကြ သနည်း ။
```

tail command နဲ့လည်း တချက် file content ကို confirm လုပ်ခဲ့တယ်...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.ensemble$ tail -n 3 *.br
==> hyp.0.4-0.6.br <==
⠓⠕ ⠩⠱⠂ ⠅⠣ ⠈⠥⠷⠋ ⠈⠥⠷⠋ ⠒ ⠃⠁ ⠹⠋ ⠇⠕⠂ ⠍⠱⠆ ⠲
⠍⠔⠛⠣⠇⠁⠏⠁ ⠲
⠍⠊⠍⠊ ⠞⠪ ⠹⠻⠆ ⠿ ⠅⠶⠆ ⠒ ⠸⠣⠥ ⠨⠮⠂ ⠹⠻⠆ ⠟⠥⠝ ⠗ ⠺⠥⠞⠁⠥⠂ ⠏⠭⠎⠪⠆ ⠣⠎⠥⠂⠎⠥⠂ ⠅ ⠠⠣⠶⠆⠇⠥ ⠚ ⠿⠓⠑⠈⠪⠆ ⠠⠣⠱⠅⠎⠑ ⠍⠂ ⠗⠋ ⠰⠣⠣ ⠅⠁⠅⠺⠮ ⠇⠕ ⠡ ⠭ ⠹ ⠲

==> hyp.0.5-0.5.br <==
⠓⠕ ⠩⠱⠂ ⠅⠣ ⠈⠥⠷⠋ ⠈⠥⠷⠋ ⠒ ⠃⠁ ⠹⠋ ⠇⠕⠂ ⠍⠱⠆ ⠲
⠍⠔⠛⠣⠇⠁⠏⠁ ⠲
⠍⠊⠍⠊ ⠞⠪ ⠹⠻⠆ ⠿ ⠡⠭ ⠒ ⠸⠣⠥ ⠨⠮⠂ ⠹⠻⠆ ⠟⠥⠝ ⠗ ⠺⠥⠞⠁⠥⠂ ⠏⠭⠎⠪⠆ ⠣⠎⠥⠂⠎⠥⠂ ⠅ ⠠⠣⠶⠆⠇⠥ ⠚ ⠿⠓⠑⠈⠪⠆ ⠠⠣⠱⠅⠎⠑ ⠍⠂ ⠗⠋ ⠰⠣⠣ ⠅⠁⠅⠺⠮ ⠇⠕ ⠡ ⠭ ⠹ ⠲

==> hyp.0.6-0.4.br <==
⠓⠕ ⠩⠱⠂ ⠅⠣ ⠈⠥⠷⠋ ⠈⠥⠷⠋ ⠒ ⠃⠁ ⠹⠋ ⠇⠕⠂ ⠍⠱⠆ ⠲
⠍⠔⠛⠣⠇⠁⠏⠁ ⠲
⠍⠊⠍⠊ ⠞⠪ ⠹⠻⠆ ⠿ ⠡⠭ ⠒ ⠸⠣⠥ ⠨⠮⠂ ⠹⠻⠆ ⠟⠥⠝ ⠗ ⠺⠥⠞⠁⠥⠂ ⠏⠭⠎⠪⠆ ⠣⠎⠥⠂⠎⠥⠂ ⠅ ⠠⠣⠶⠆⠇⠥ ⠚ ⠿⠓⠑⠈⠪⠆ ⠠⠣⠱⠅⠎⠑ ⠍⠂ ⠗⠋ ⠰⠣⠣ ⠅⠁⠅⠺⠮ ⠇⠕ ⠡ ⠭ ⠹ ⠲
(base) ye@:/media/ye/project2/exp/braille-nmt/model.ensemble$ tail -n 3 *.my
==> hyp.0.4-0.6.my <==
ဟို ရှေ့ က ဆူညံ ဆူညံ ၊ ဘာ သံ လို့ မေး ။
ျ ။
မိမိ တည် သော ဘုရား ကိုးဆူ ၊ လှူ ခဲ့ သော ကျွန် နှင့် ဝတ္ထု ပစ္စည်း အစုစု ကို နှောင်းလူ တို့ ဖျက်ဆီး နှိပ်စက် မည့် ရန် မှ ကာကွယ် လို ခြင်း ဖြစ် သည် ။

==> hyp.0.5-0.5.my <==
ဟို ရှေ့ က ဆူညံ ဆူညံ ၊ ဘာ သံ လို့ မေး ။
ျ ။
မိမိ တည် သော ဘုရား ကိုးဆူ ၊ လှူ ခဲ့ သော ကျွန် နှင့် ဝတ္ထု ပစ္စည်း အစုစု ကို နှောင်းလူ တို့ ဖျက်ဆီး နှိပ်စက် မည့် ရန် မှ ကာကွယ် လို ခြင်း ဖြစ် သည် ။

==> hyp.0.6-0.4.my <==
ဟို ရှေ့ က ဆူညံ ဆူညံ ၊ ဘာ သံ လို့ မေး ။
စွတ် ။
မိမိ တည် သော ဘုရား ကိုးဆူ ၊ လှူ ခဲ့ သော ကျွန် နှင့် ဝတ္ထု ပစ္စည်း အစုစု ကို နှောင်းလူ တို့ ဖျက်ဆီး နှိပ်စက် မည့် ရန် မှ ကာကွယ် လို ခြင်း ဖြစ် သည် ။
(base) ye@:/media/ye/project2/exp/braille-nmt/model.ensemble$
```

## Evaluation

evaluation process အတွက် အရင်ဆုံး bash script ရေးရမှာမို့ ရေးခဲ့...  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, Visiting Professor, LST, NECTEC, Thailand
# Last updated: 19 April 2022
# BLEU score evaluation on s2s+transformer ensemble results:

# for my-br
for file in {hyp.0.4-0.6.br,hyp.0.5-0.5.br,hyp.0.6-0.4.br}
do
   echo "Evaluation with $file, ensemble, my-br translation:" >> test-ensemble-results.txt;
   perl ~/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br < ./$file >> test-ensemble-results.txt;
done
echo "==========" >> test-ensemble-results.txt;

# for br-my
for file in {hyp.0.4-0.6.my,hyp.0.5-0.5.my,hyp.0.6-0.4.my}
do
   echo "Evaluation with $file, ensemble, br-my translation:" >> test-ensemble-results.txt;
   perl ~/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my < ./$file  >> test-ensemble-results.txt;
done

cat ./test-ensemble-results.txt;

```

## Results

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.ensemble$ time ./ensemble-eval.sh 
Evaluation with hyp.0.4-0.6.br, ensemble, my-br translation:
BLEU = 88.13, 95.3/90.6/86.2/82.0 (BP=0.997, ratio=0.997, hyp_len=28719, ref_len=28803)
Evaluation with hyp.0.5-0.5.br, ensemble, my-br translation:
BLEU = 88.25, 95.4/90.7/86.4/82.1 (BP=0.997, ratio=0.997, hyp_len=28719, ref_len=28803)
Evaluation with hyp.0.6-0.4.br, ensemble, my-br translation:
BLEU = 88.34, 95.4/90.8/86.5/82.3 (BP=0.997, ratio=0.997, hyp_len=28721, ref_len=28803)
==========
Evaluation with hyp.0.4-0.6.my, ensemble, br-my translation:
BLEU = 88.39, 95.4/90.8/86.7/82.7 (BP=0.996, ratio=0.996, hyp_len=28681, ref_len=28803)
Evaluation with hyp.0.5-0.5.my, ensemble, br-my translation:
BLEU = 88.52, 95.5/90.9/86.8/82.9 (BP=0.996, ratio=0.996, hyp_len=28676, ref_len=28803)
Evaluation with hyp.0.6-0.4.my, ensemble, br-my translation:
BLEU = 88.55, 95.5/91.0/86.8/82.9 (BP=0.996, ratio=0.996, hyp_len=28680, ref_len=28803)

real	0m0.974s
user	0m0.961s
sys	0m0.013s
(base) ye@:/media/ye/project2/exp/braille-nmt/model.ensemble$
```

## Adding Additional Weights for Ensemble Experiment

Ensemble အတွက် 0.2 0.8, 0.3 0.7, 0.7 0.3, 0.8 0.2 weight တွေကို ထပ်ဖြည့် run ဖို့ ဆုံးဖြတ်ခဲ့...  
အကြောင်းအရင်းက လက်ရှိမှာက seq2seq architecture ရဲ့ ရလဒ်က ပိုကောင်းနေလို့... နည်းနည်း ဘက်လိုက်မှုက ရှိနေတယ်။ ensemble လုပ်တာက ရလဒ်တက်လာပေမဲ့ ပိုပြီးတော့ ဘယ်လောက်အထိ အများဆုံးထိ တက်နိုင်မလဲ၊ seq2seq ထက် ပိုတက်နိုင်မလား ဆိုတာကို ကွဲကွဲပြားပြား သိချင်လို့ weight ကို ပိုတိုးပြီး experiment လုပ်ကြည့်တာ။  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, Visiting Professor, LST, NECTEC, Thailand
# Last Updated: 19 April 2022
# Ensemble decoding with s2s+transformer, additional experiment for 0.2 0.8, 0.3 0.7, 0.7 0.3, 0.8 0.2


# my-br, seq2seq အတွက် best model က model.iter65000.npz
# my-br, transformer အတွက် best model က model0-mybr.iter95000.npz

# --weights 0.2 0.8
time marian-decoder \
    --models ./model.s2s-mybr/model.iter65000.npz ./model.transformer/model0-mybr.iter95000.npz \
    --weights 0.2 0.8 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble/hyp.0.2-0.8.br \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my | tee my-br.ensemble.0.2-0.8.log
    
# --weights 0.3 0.7
time marian-decoder \
    --models ./model.s2s-mybr/model.iter65000.npz ./model.transformer/model0-mybr.iter95000.npz \
    --weights 0.3 0.7 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble/hyp.0.3-0.7.br \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my | tee my-br.ensemble.0.3-0.7.log
    
# --weights 0.7 0.3
time marian-decoder \
    --models ./model.s2s-mybr/model.iter65000.npz ./model.transformer/model0-mybr.iter95000.npz \
    --weights 0.7 0.3 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble/hyp.0.7-0.3.br \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my | tee my-br.ensemble.0.7-0.3.log

# --weights 0.8 0.2
time marian-decoder \
    --models ./model.s2s-mybr/model.iter65000.npz ./model.transformer/model0-mybr.iter95000.npz \
    --weights 0.8 0.2 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble/hyp.0.8-0.2.br \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my | tee my-br.ensemble.0.8-0.2.log
    
# br-my အတွက် best model က model.iter55000.npz
# br-my အတွက် best model က 

# --weights 0.2 0.8
time marian-decoder \
    --models ./model.s2s-brmy/model.iter55000.npz ./model.transformer-brmy/model0-brmy.iter80000.npz \
    --weights 0.2 0.8 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble/hyp.0.2-0.8.my \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br | tee br-my.ensemble.0.2-0.8.log

# --weights 0.3 0.7
time marian-decoder \
    --models ./model.s2s-brmy/model.iter55000.npz ./model.transformer-brmy/model0-brmy.iter80000.npz \
    --weights 0.3 0.7 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble/hyp.0.3-0.7.my \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br | tee br-my.ensemble.0.3-0.7.log
    
# --weights 0.7 0.3
time marian-decoder \
    --models ./model.s2s-brmy/model.iter55000.npz ./model.transformer-brmy/model0-brmy.iter80000.npz \
    --weights 0.7 0.3 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble/hyp.0.7-0.3.my \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br | tee br-my.ensemble.0.7-0.3.log

# --weights 0.8 0.2
time marian-decoder \
    --models ./model.s2s-brmy/model.iter55000.npz ./model.transformer-brmy/model0-brmy.iter80000.npz \
    --weights 0.8 0.2 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble/hyp.0.8-0.2.my \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br | tee br-my.ensemble.0.8-0.2.log
    
```

Ensemble Decoding ကို my-br အတွက်ကော br-my အတွက်ကော၊ ထပ်တိုးထားတဲ့ weight တွေနဲ့ (weights:0.2 0.8, 0.3 0.7, 0.7 0.3, 0.8 0.2) လုပ်ခဲ့...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt$ time ./ensemble-addition-exp.sh
...
...
...
[2022-04-19 19:55:22] Best translation 2144 : သွေးတူမွေးတူ နွားများ ကို ချူများ ၊ အဆင်တန်ဆာများ ဆင် ပြီးလျှင် လှည်းယဉ် တွင် သစ် မောင်း လေ့ ရှိ သည် ။
[2022-04-19 19:55:22] Best translation 2145 : ရှင် ၊ ခင်ဗျာ ဟု ထူး မှ ယဉ်ကျေးသည် ။
[2022-04-19 19:55:22] Best translation 2146 : ၉ ၃ ၄ ခု တွင် ပေါ်ပေါက် ခဲ့ သော အဟုန် ပြင်း သည် အရေး တွင် ကား မင်းတရားကြီး က ဗညားဒလ အပေါ် အမျက် တော် ရှိ၍ စ၍ ဟူသော ယိုးဒယား ကျေးရွာ တွင် ကျွန် ငါး ယောက် နှင့် ထား တော် မူ သည် ။
[2022-04-19 19:55:22] Best translation 2147 : ၁ ၀ ။ ဝါသနာ = စွဲမြဲ နေ သော အလေ့အကျင့် ။
[2022-04-19 19:55:22] Best translation 2148 : မောင်ဖိုးစိန် သည် ဇာတ်သဘင်ပညာ ကို အခြေခံ မှ စ၍ သင်ယူ လေ့လာ ခဲ့ သည် ။
[2022-04-19 19:55:22] Best translation 2149 : ရတု ၊ တေးထပ် တို့ တွင် နန်း မူ နန်း ရာ ကို တွေ့ နိုင် သည် ။
[2022-04-19 19:55:22] Best translation 2150 : ဤ အခါ ငတာ က ဘာကြောင့် ပါ လည်း ဘုရား ဟု လျှောက် ရာ စ၍ က နင် မှ စာ မ တတ် ဘဲ နဲ့ ငါ ရေး တဲ့ စာ တွေ ချီးမွမ်း ပါလျှင် ငါ ပါ ပစ်ရ နေ မှာ ပေါ့ ။
[2022-04-19 19:55:22] Best translation 2151 : နေ့တိုင်း မှာ ကား ဥစ္စာရှင် သည် အစာ ရှာ၍ ပြန် သည် ရှိ သော် ဆိတ် သားငယ် တို့ သည် အမိ မျက်နှာ ကို ကြည့် ကုန် လျက် လိုက် သကဲ့သို့ ငါ့ သား ၊ ငါ့ သမီး တို့ သည် မြေမှုန့် အလိမ်းလိမ်း ကပ် သော ကိုယ် ဖြင့် အမိ သို့ ကပ်၍ နေ ၏ ။
[2022-04-19 19:55:22] Best translation 2152 : ဤ ထက် လွန်၍ ဆန်းကြယ် လျောက်ပတ် သော အရာ ကို ကျွန်ုပ် မ တတ် ပြီ ဟု ဆို ၏ ။
[2022-04-19 19:55:22] Best translation 2153 : သူငယ်ချင်း ပေး တဲ့ ကုသိုလ် မူတည် ပြီး ပြန် ရေး ကြ ရအောင် ။
[2022-04-19 19:55:22] Best translation 2154 : ကျွန်ုပ်တို့ သည် ဤ မိတဆိုး ရှင်ပြု ကို အလွန် သနား စေတနာ ရှိ လာ ကြ သည် နှင့် ဦးစံရွှေ နှင့် တိုင်ပင် ကာ အလှူ အိမ် တွင် ည အိပ်၍ တတ် နိုင် သမျှ လေ့ကျင့် ဆုံးဖြတ် လိုက် ကြ လေ သည် ။
[2022-04-19 19:55:22] Best translation 2155 : ကြက်ဥ ပြုတ် သည် ။
[2022-04-19 19:55:22] Best translation 2156 : ယခု ပင် အဆိပ် လူး သော မြား ဖြင့် ပစ် သတ် အံ့ ။
[2022-04-19 19:55:22] Best translation 2157 : ဝမ်းသာအားရ ၊ မယား က တစ် သွယ် ။
[2022-04-19 19:55:22] Best translation 2158 : ဝေ ဝေ့ ဝေး ။
[2022-04-19 19:55:22] Best translation 2159 : ပြန်၍ သုံးသပ် ကြည့် ပါ လျှင် မြန်မာ ဘာသာစကား တွင် အရေး အက္ခရာ ရှိ ထား ပြီး ဖြစ် သဖြင့် အရေး နှင့် အဖတ် ဟူ၍ နှစ် မျိုး ရှိ နေ သည် ။
[2022-04-19 19:55:22] Best translation 2160 : လေ့ကျင့် လည်း မ ထိုင် ရ ။
[2022-04-19 19:55:22] Best translation 2161 : ၁ ။ အောက်ပါ စကားလုံး တို့ ၏ အနက် အဓိပ္ပာယ် ကို အဘိဓာန် တွင် ရှာ ပါ ။
[2022-04-19 19:55:22] Best translation 2162 : သင်ခန်းစာ အကျဉ်း ။
[2022-04-19 19:55:22] Best translation 2163 : ချစ်လှစွာ သော သား ။
[2022-04-19 19:55:22] Best translation 2164 : ဟို ရှေ့ က ဆူညံ ဆူညံ ၊ ဘာ သံ လို့ မေး ။
[2022-04-19 19:55:22] Best translation 2165 : စွတ် ။
[2022-04-19 19:55:22] Best translation 2166 : မိမိ တည် သော ဘုရား ကိုးဆူ ၊ လှူ ခဲ့ သော ကျွန် နှင့် ဝတ္ထု ပစ္စည်း အစုစု ကို နှောင်းလူ တို့ ဖျက်ဆီး နှိပ်စက် မည့် ရန် မှ ကာကွယ် လို ခြင်း ဖြစ် သည် ။
[2022-04-19 19:55:22] Total time: 193.41224s wall

real	3m14.992s
user	6m25.053s
sys	0m3.146s

real	26m2.549s
user	51m20.952s
sys	0m28.453s

```

output အဖြစ်ထွက်လာတဲ့ hyp ဖိုင်တွေကို စစ်ကြည့်ခဲ့...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.ensemble$ wc *.my
   2167   28764  379284 hyp.0.2-0.8.my
   2167   28717  378795 hyp.0.3-0.7.my
   2167   28681  376482 hyp.0.4-0.6.my
   2167   28676  375116 hyp.0.5-0.5.my
   2167   28680  373681 hyp.0.6-0.4.my
   2167   28680  372329 hyp.0.7-0.3.my
   2167   28732  372143 hyp.0.8-0.2.my
  15169  200930 2627830 total
(base) ye@:/media/ye/project2/exp/braille-nmt/model.ensemble$ wc *.br
   2167   28782  282249 hyp.0.2-0.8.br
   2167   28747  279460 hyp.0.3-0.7.br
   2167   28719  275248 hyp.0.4-0.6.br
   2167   28719  272346 hyp.0.5-0.5.br
   2167   28721  270899 hyp.0.6-0.4.br
   2167   28719  270381 hyp.0.7-0.3.br
   2167   28720  270058 hyp.0.8-0.2.br
  15169  201127 1920641 total
(base) ye@:/media/ye/project2/exp/braille-nmt/model.ensemble$
```

တိုးထားတဲ့ weight တွေရဲ့ translated output တွေကိုပါထည့်ပြီး evaluation လုပ်ဖို့အတွက် bash script ကိုအောက်ပါအတိုင်း update လုပ်ခဲ့...  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, Visiting Professor, LST, NECTEC, Thailand
# Last updated: 19 April 2022
# BLEU score evaluation on s2s+transformer ensemble results:

# for my-br
for file in {hyp.0.2-0.8.br,hyp.0.3-0.7.br,hyp.0.4-0.6.br,hyp.0.5-0.5.br,hyp.0.6-0.4.br,hyp.0.7-0.3.br,hyp.0.8-0.2.br}
do
   echo "Evaluation with $file, ensemble, my-br translation:" >> test-ensemble-results.txt;
   perl ~/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br < ./$file >> test-ensemble-results.txt;
done
echo "==========" >> test-ensemble-results.txt;

# for br-my
for file in {hyp.0.2-0.8.my,hyp.0.3-0.7.my,hyp.0.4-0.6.my,hyp.0.5-0.5.my,hyp.0.6-0.4.my,hyp.0.7-0.3.my,hyp.0.8-0.2.my}
do
   echo "Evaluation with $file, ensemble, br-my translation:" >> test-ensemble-results.txt;
   perl ~/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my < ./$file  >> test-ensemble-results.txt;
done

cat ./test-ensemble-results.txt;
```

## Result After Adding Additional Weights

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.ensemble$ time ./ensemble-eval2.sh 
Evaluation with hyp.0.2-0.8.br, ensemble, my-br translation:
BLEU = 87.89, 95.2/90.2/85.7/81.3 (BP=0.999, ratio=0.999, hyp_len=28782, ref_len=28803)
Evaluation with hyp.0.3-0.7.br, ensemble, my-br translation:
BLEU = 87.99, 95.2/90.4/85.9/81.6 (BP=0.998, ratio=0.998, hyp_len=28747, ref_len=28803)
Evaluation with hyp.0.4-0.6.br, ensemble, my-br translation:
BLEU = 88.13, 95.3/90.6/86.2/82.0 (BP=0.997, ratio=0.997, hyp_len=28719, ref_len=28803)
Evaluation with hyp.0.5-0.5.br, ensemble, my-br translation:
BLEU = 88.25, 95.4/90.7/86.4/82.1 (BP=0.997, ratio=0.997, hyp_len=28719, ref_len=28803)
Evaluation with hyp.0.6-0.4.br, ensemble, my-br translation:
BLEU = 88.34, 95.4/90.8/86.5/82.3 (BP=0.997, ratio=0.997, hyp_len=28721, ref_len=28803)
Evaluation with hyp.0.7-0.3.br, ensemble, my-br translation:
BLEU = 88.29, 95.4/90.8/86.4/82.2 (BP=0.997, ratio=0.997, hyp_len=28719, ref_len=28803)
Evaluation with hyp.0.8-0.2.br, ensemble, my-br translation:
BLEU = 88.27, 95.3/90.7/86.4/82.2 (BP=0.997, ratio=0.997, hyp_len=28720, ref_len=28803)
==========
Evaluation with hyp.0.2-0.8.my, ensemble, br-my translation:
BLEU = 88.12, 95.2/90.4/86.0/82.0 (BP=0.999, ratio=0.999, hyp_len=28764, ref_len=28803)
Evaluation with hyp.0.3-0.7.my, ensemble, br-my translation:
BLEU = 88.19, 95.2/90.5/86.3/82.3 (BP=0.997, ratio=0.997, hyp_len=28717, ref_len=28803)
Evaluation with hyp.0.4-0.6.my, ensemble, br-my translation:
BLEU = 88.39, 95.4/90.8/86.7/82.7 (BP=0.996, ratio=0.996, hyp_len=28681, ref_len=28803)
Evaluation with hyp.0.5-0.5.my, ensemble, br-my translation:
BLEU = 88.52, 95.5/90.9/86.8/82.9 (BP=0.996, ratio=0.996, hyp_len=28676, ref_len=28803)
Evaluation with hyp.0.6-0.4.my, ensemble, br-my translation:
BLEU = 88.55, 95.5/91.0/86.8/82.9 (BP=0.996, ratio=0.996, hyp_len=28680, ref_len=28803)
Evaluation with hyp.0.7-0.3.my, ensemble, br-my translation:
BLEU = 88.57, 95.5/91.0/86.9/82.9 (BP=0.996, ratio=0.996, hyp_len=28680, ref_len=28803)
Evaluation with hyp.0.8-0.2.my, ensemble, br-my translation:
BLEU = 88.65, 95.5/90.9/86.8/82.8 (BP=0.998, ratio=0.998, hyp_len=28732, ref_len=28803)

real	0m2.117s
user	0m2.091s
sys	0m0.027s
(base) ye@:/media/ye/project2/exp/braille-nmt/model.ensemble$
```

## Comparison of Seq2Seq, Transformer and Ensemble Model Results

လက်ရှိရထားတဲ့ seq2seq, transformer နဲ့ အဲဒီနှစ်ခုကိုပေါင်းထားတဲ့ ensemble decoding ရလဒ်တွေကို နှိုင်းယှဉ်ကြည့်တဲ့အခါမှာ အောက်ပါဇယားကို ရတယ်။   

<div align="center">  
 
Table 1. Performance comparison of Seq2Seq, Transformer and Ensemble Model  

| Source-Target | Seq2Seq | Transformer | 0.2-0.8 | 0.3-0.7 | 0.4-0.6 | 0.5-0.5 | 0.6-0.4 | 0.7-0.3 | 0.8-0.2 | 
|----------:|----------:|----------:|----------:|----------:|----------:|----------:|----------:|----------:|----------:|
| my-br | 88.33 | 86.73 | 87.89 | 87.99 | 88.13 | 88.25 | **88.34** | 88.29 | 88.27 |
| br-my | **88.75** | 87.54 | 88.12 | 88.19 | 88.39 | 88.52 |  88.55 | 88.57 | 88.65 |

 </div>  

## Ensemble Decoding of Seq2Seq Models

အကောင်းဆုံး seq2seq မော်ဒယ် နှစ်ခုကို ပေါင်းပြီးတော့ ensemble decoding လုပ်ဖို့အတွက် shell script ကို အောက်ပါအတိုင်း ရေးခဲ့...  

```bash
#!/bin/bash

# Written by Ye Kyaw Thu, Visiting Professor, LST, NECTEC, Thailand
# Last Updated: 19 April 2022
# Ensemble decoding with two s2s models
# Note: ဒီနေရာမှာ တိုက်ဆိုင်မှုက ဒုတိယအကောင်းဆုံး မော်ဒယ်တွေက my-br အတွက်ရော br-my အတွက်ရော iter45000 ဖြစ်နေတာ

# my-br, seq2seq အတွက် best model က model.iter65000.npz
# my-br, transformer အတွက် best model က model0-mybr.iter95000.npz

# --weights 0.4 0.6
time marian-decoder \
    --models ./model.s2s-mybr/model.iter65000.npz ./model.s2s-mybr/model.iter45000.npz \
    --weights 0.4 0.6 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble.seq2seq/hyp.0.4-0.6.br \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my | tee ensemble.two-seq2seq.log
    
# --weights 0.5 0.5
time marian-decoder \
    --models ./model.s2s-mybr/model.iter65000.npz ./model.s2s-mybr/model.iter45000.npz \
    --weights 0.5 0.5 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble.seq2seq/hyp.0.5-0.5.br \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my | tee ensemble.two-seq2seq.log
    
# --weights 0.6 0.4
time marian-decoder \
    --models ./model.s2s-mybr/model.iter65000.npz ./model.s2s-mybr/model.iter45000.npz \
    --weights 0.6 0.4 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble.seq2seq/hyp.0.6-0.4.br \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my | tee ensemble.two-seq2seq.log
    
## Additional Experiment for my-br

# --weights 0.2 0.8
time marian-decoder \
    --models ./model.s2s-mybr/model.iter65000.npz ./model.s2s-mybr/model.iter45000.npz \
    --weights 0.2 0.8 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble.seq2seq/hyp.0.2-0.8.br \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my | tee ensemble.two-seq2seq.log
    
# --weights 0.3 0.7
time marian-decoder \
    --models ./model.s2s-mybr/model.iter65000.npz ./model.s2s-mybr/model.iter45000.npz \
    --weights 0.3 0.7 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble.seq2seq/hyp.0.3-0.7.br \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my | tee ensemble.two-seq2seq.log
    
# --weights 0.7 0.3
time marian-decoder \
    --models ./model.s2s-mybr/model.iter65000.npz ./model.s2s-mybr/model.iter45000.npz \
    --weights 0.7 0.3 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble.seq2seq/hyp.0.7-0.3.br \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my | tee ensemble.two-seq2seq.log

# --weights 0.8 0.2
time marian-decoder \
    --models ./model.s2s-mybr/model.iter65000.npz ./model.s2s-mybr/model.iter45000.npz\
    --weights 0.8 0.2 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble.seq2seq/hyp.0.8-0.2.br \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my | tee ensemble.two-seq2seq.log

# br-my အတွက် best model က model.iter55000.npz
# br-my အတွက် best model က 

# --weights 0.4 0.6
time marian-decoder \
    --models ./model.s2s-brmy/model.iter55000.npz ./model.s2s-brmy/model.iter45000.npz  \
    --weights 0.4 0.6 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble.seq2seq/hyp.0.4-0.6.my \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br | tee ensemble.two-seq2seq.log

# --weights 0.5 0.5
time marian-decoder \
    --models ./model.s2s-brmy/model.iter55000.npz ./model.s2s-brmy/model.iter45000.npz \
    --weights 0.5 0.5 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble.seq2seq/hyp.0.5-0.5.my \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br | tee ensemble.two-seq2seq.log
    
# --weights 0.6 0.4
time marian-decoder \
    --models ./model.s2s-brmy/model.iter55000.npz ./model.s2s-brmy/model.iter45000.npz  \
    --weights 0.6 0.4 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble.seq2seq/hyp.0.6-0.4.my \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br | tee ensemble.two-seq2seq.log

## Additional Experiment for br-my

# --weights 0.2 0.8
time marian-decoder \
    --models ./model.s2s-brmy/model.iter55000.npz ./model.s2s-brmy/model.iter45000.npz \
    --weights 0.2 0.8 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble.seq2seq/hyp.0.2-0.8.my \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br | tee ensemble.two-seq2seq.log

# --weights 0.3 0.7
time marian-decoder \
    --models ./model.s2s-brmy/model.iter55000.npz ./model.s2s-brmy/model.iter45000.npz \
    --weights 0.3 0.7 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble.seq2seq/hyp.0.3-0.7.my \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br | tee ensemble.two-seq2seq.log
    
# --weights 0.7 0.3
time marian-decoder \
    --models ./model.s2s-brmy/model.iter55000.npz ./model.s2s-brmy/model.iter45000.npz \
    --weights 0.7 0.3 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble.seq2seq/hyp.0.7-0.3.my \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br | tee ensemble.two-seq2seq.log

# --weights 0.8 0.2
time marian-decoder \
    --models ./model.s2s-brmy/model.iter55000.npz ./model.s2s-brmy/model.iter45000.npz \
    --weights 0.8 0.2 --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
   --maxi-batch 64  --workspace 500 \
   --output ./model.ensemble.seq2seq/hyp.0.8-0.2.my \
    --devices 0 1 < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br | tee ensemble.two-seq2seq.log
   
```

run above shell script ...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt$ time ./ensemble-seq2seq.sh 
...
...
...
[2022-04-19 21:38:43] Best translation 2144 : သွေးတူမွေးတူ နွားများ ကို ချူများ ၊ အဆင်တန်ဆာများ ဆင် ပြီးလျှင် လှည်းယဉ် တွင် သစ် မောင်း လေ့ ရှိ သည် ။
[2022-04-19 21:38:43] Best translation 2145 : ရှင် ၊ ခင်ဗျာ ဟု ထူး မှ ယဉ်ကျေးသည် ။
[2022-04-19 21:38:43] Best translation 2146 : ၉ ၃ ၄ ခု တွင် ပေါ်ပေါက် ခဲ့ သော အနုပညာ သည် သည် အရေး တွင် ကား မင်းတရားကြီး က ဗညားဒလ အပေါ် အမျက် တော် ရှိ၍ စ၍ ဟူသော ယိုးဒယား ကျေးရွာ တွင် ကျွန် ငါး ယောက် နှင့် ထား တော် မူ သည် ။
[2022-04-19 21:38:43] Best translation 2147 : ၁ ၀ ။ ဝါသနာ = စွဲမြဲ နေ သော အလေ့အကျင့် ။
[2022-04-19 21:38:43] Best translation 2148 : မောင်ဖိုးစိန် သည် ဇာတ်သဘင်ပညာ ကို အခြေခံ မှ စ၍ သင်ယူ လေ့လာ ခဲ့ သည် ။
[2022-04-19 21:38:43] Best translation 2149 : ရတု ၊ တေးထပ် တို့ တွင် နန်း မူ နန်း ရာ ကို တွေ့ နိုင် သည် ။
[2022-04-19 21:38:43] Best translation 2150 : ဤ အခါ ငတာ က ဘာကြောင့် ပါ လည်း ဘုရား ဟု လျှောက် ရာ စ၍ က နင် မှ စာ မ တတ် ဘဲ နဲ့ ငါ ရေး တဲ့ စာ တွေ ချီးမွမ်း ပါလျှင် ငါ ပါ ပစ်ရ နေ မှာ ပေါ့ ။
[2022-04-19 21:38:43] Best translation 2151 : နေ့တိုင်း မှာ ကား စ၍ သည် အစာ ရှာ၍ ပြန် သည် ရှိ သော် ဆိတ် သားငယ် တို့ သည် အမိ မျက်နှာ ကို ကြည့် ကုန် လျက် လိုက် သကဲ့သို့ ငါ့ သား ၊ ငါ့ သမီး တို့ သည် မြေမှုန့် အလိမ်းလိမ်း ကပ် သော ကိုယ် ဖြင့် အမိ သို့ ကပ်၍ နေ ၏ ။
[2022-04-19 21:38:43] Best translation 2152 : ဤ ထက် လွန်၍ ဆန်းကြယ် လျောက်ပတ် သော အရာ ကို ကျွန်ုပ် မ တတ် ပြီ ဟု ဆို ၏ ။
[2022-04-19 21:38:43] Best translation 2153 : သူငယ်ချင်း ပေး တဲ့ ပျူ မူတည် ပြီး ပြန် ရေး ကြ ရအောင် ။
[2022-04-19 21:38:43] Best translation 2154 : ကျွန်ုပ်တို့ သည် ဤ မိတဆိုး ရှင်ပြု ကို အလွန် သနား စေတနာ ရှိ လာ ကြ သည် နှင့် ဦးစံရွှေ နှင့် တိုင်ပင် ကာ အလှူ အိမ် တွင် ည အိပ်၍ တတ် နိုင် သမျှ လေ့ကျင့် ဆုံးဖြတ် လိုက် ကြ လေ သည် ။
[2022-04-19 21:38:43] Best translation 2155 : ကြက်ဥ ပြုတ် သည် ။
[2022-04-19 21:38:43] Best translation 2156 : ယခု ပင် အဆိပ် လူး သော မြား ဖြင့် ပစ် သတ် အံ့ ။
[2022-04-19 21:38:43] Best translation 2157 : ဝမ်းသာအားရ ၊ မယား က တစ် သွယ် ။
[2022-04-19 21:38:43] Best translation 2158 : ဝေ ဝေ့ ဝေး ။
[2022-04-19 21:38:43] Best translation 2159 : ပြန်၍ သုံးသပ် ကြည့် ပါ လျှင် မြန်မာ ဘာသာစကား တွင် အရေး အက္ခရာ ရှိ ထား ပြီး ဖြစ် သဖြင့် အရေး နှင့် အဖတ် ဟူ၍ နှစ် မျိုး ရှိ နေ သည် ။
[2022-04-19 21:38:43] Best translation 2160 : လေ့ကျင့် လည်း မ ထိုင် ရ ။
[2022-04-19 21:38:43] Best translation 2161 : ၁ ။ အောက်ပါ စကားလုံး တို့ ၏ အနက် အဓိပ္ပာယ် ကို အဘိဓာန် တွင် ရှာ ပါ ။
[2022-04-19 21:38:43] Best translation 2162 : သင်ခန်းစာ အကျဉ်း ။
[2022-04-19 21:38:43] Best translation 2163 : ချစ်လှစွာ သော သား ။
[2022-04-19 21:38:43] Best translation 2164 : ဟို ရှေ့ က ဆူညံ ဆူညံ ၊ ဘာ သံ လို့ မေး ။
[2022-04-19 21:38:43] Best translation 2165 : ။ ။
[2022-04-19 21:38:43] Best translation 2166 : မိမိ တည် သော ဘုရား ကိုးဆူ ၊ လှူ ခဲ့ သော ကျွန် နှင့် ဝတ္ထု ပစ္စည်း အစုစု ကို နှောင်းလူ တို့ ဖျက်ဆီး နှိပ်စက် မည့် ရန် မှ ကာကွယ် လို ခြင်း ဖြစ် သည် ။
[2022-04-19 21:38:43] Total time: 268.48316s wall

real	4m30.630s
user	8m56.303s
sys	0m3.280s

real	64m26.813s
user	126m24.234s
sys	0m54.913s
```

Evaluation script က ensemble-eval2.sh ကိုပဲ သုံးခဲ့တယ်။ ရလဒ်တွေက အောက်ပါအတိုင်းပါ...  

```

```



## Ensemble Decoding of Transformer Models

အကောင်းဆုံး transformer မော်ဒယ်နှစ်ခုကို ensemble decoding လုပ်နိုင်ဖို့အတွက် shell script ကို အောက်ပါအတိုင်း ရေးခဲ့...  

```bash

```

