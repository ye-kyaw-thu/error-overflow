# Text Classification on Unlabeled Data Running Log

Is it possible to do Text Classification on unlabeled data? (Feat. Zero-Shot Classification) [Experiment] ဆိုတဲ့ experiment ကို ကိုယ်စက်မှာ စမ်းကြည့်ထားတဲ့ log ဖိုင်  
Reference Link: https://pub.towardsai.net/is-it-possible-to-do-text-classification-on-unlabeled-data-feat-zero-shot-classification-8caa584a1661

```
(base) ye@:~/4github/4students/zero-shot-classification$ python ./zero-shot-clf.py 
Downloading: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████| 1.15k/1.15k [00:00<00:00, 505kB/s]
HTTPSConnectionPool(host='cdn-lfs.huggingface.co', port=443): Max retries exceeded with url: /facebook/bart-large-mnli/ce253627f98f9db22af6a86efee6e905f001f7d8dc02dd14a8b4b4710c302b17 (Caused by SSLError(SSLError("bad handshake: SysCallError(104, 'ECONNRESET')")))
Downloading: 100%|█████████████████████████████████████████████████████████████████████████████████████████████████| 1.63G/1.63G [00:27<00:00, 60.3MB/s]
Downloading: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████| 26.0/26.0 [00:00<00:00, 10.1kB/s]
Downloading: 100%|████████████████████████████████████████████████████████████████████████████████████████████████████| 899k/899k [00:01<00:00, 672kB/s]
Downloading: 100%|████████████████████████████████████████████████████████████████████████████████████████████████████| 456k/456k [00:01<00:00, 423kB/s]
Downloading: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████| 1.36M/1.36M [00:02<00:00, 644kB/s]
{'sequence': 'The movie was so boring, I actually fell sleep in the first 20 minutes.', 'labels': ['negative', 'positive'], 'scores': [0.988088846206665, 0.011911189183592796]}
(base) ye@:~/4github/4students/zero-shot-classification$ 
```

စာကြောင်းထဲမှာ မြန်မာရုပ်ရှင်ကား နာမည်ထည့် run ကြည့်ခဲ့တယ်။ အဆင်ပြေတယ်။  

```
(base) ye@:~/4github/4students/zero-shot-classification$ python ./zero-shot-clf.py 
{'sequence': 'I love သင်္ကြန်မိုး movie and watched many times.', 'labels': ['positive', 'negative'], 'scores': [0.9331490993499756, 0.06685090065002441]}
(base) ye@:~/4github/4students/zero-shot-classification$ 
```

စာကြောင်း တစ်ကြောင်းလုံးကို မြန်မာစာ စာကြောင်းနဲ့ အစားထိုးခဲ့တယ်။ positive ကို မျှော်လင့်တယ်။

```
(base) ye@:~/4github/4students/zero-shot-classification$ python ./zero-shot-clf.py 
{'sequence': 'သင်္ကြန်မိုး ကို ငါ အရမ်းကြိုက်တယ်', 'labels': ['positive', 'negative'], 'scores': [0.5568084120750427, 0.4431915879249573]}
```

စာကြောင်းကို ပြောင်းတယ်။ negative ကို မျှော်လင့်တယ်။ ရလဒ်က သိပ်မကွာဘူး။ သိလိုက်ရတာက အလုပ်မလုပ်ဘူး...  

```
(base) ye@:~/4github/4students/zero-shot-classification$ python ./zero-shot-clf.py 
{'sequence': 'သင်္ကြန်မိုး ကို ငါ လုံးဝ မကြိုက်ဘူး', 'labels': ['negative', 'positive'], 'scores': [0.5567457675933838, 0.4432542026042938]}
(base) ye@:~/4github/4students/zero-shot-classification$ 
```

```
(base) ye@:~/4github/4students/zero-shot-classification$ python ./zero-shot-clf.py 
{'sequence': 'The movie was so boring, I actually fell sleep in the first 20 minutes.', 'labels': ['negative', 'positive'], 'scores': [0.988088846206665, 0.011911189183592796]}
Traceback (most recent call last):
  File "./zero-shot-clf.py", line 31, in <module>
    for idx, item in tqdm(test_set_df.iterrows()):
TypeError: 'module' object is not callable

```

အထက်ပါ error က from tqdm import tqdm လုပ်ပေးရင် အဆင်ပြေတယ်...  

## Zero Shot Inference with the Testset

တစ်ကြောင်းချင်းစီ စမ်းတာ မဟုတ်ပဲ testset နဲ့စမ်းမယ်ဆိုရင် အောက်ပါအတိုင်း coding လုပ်လို့ ရတယ်  

```python
from sklearn.metrics import accuracy_score

results = []
targets = []

for idx, item in tqdm(test_set_df.iterrows()):
  
  res = classifier(item['review'], the_labels)

  results.append( res['labels'][0] )
  targets.append( item['sentiment'] )
  
accuracy = accuracy_score(results, targets)
```

Run ရင် နှစ်နာရီကျော်ကြာတယ်။ testset တစ်ခုလုံးအတွက် evaluation လုပ်ကြည့်တော့ Accuracy က 0.88 ရတယ်။  

```
(base) ye@:~/4github/4students/zero-shot-classification$ python ./zero-shot-clf.py 
{'sequence': 'The movie was so boring, I actually fell sleep in the first 20 minutes.', 'labels': ['negative', 'positive'], 'scores': [0.988088846206665, 0.011911189183592796]}
5000it [2:21:50,  1.70s/it]
Accuracy:  0.8828
(base) ye@:~/4github/4students/zero-shot-classification$
```

hypothesis template ပြောင်းရင် accuracy ပိုတက်တာမို့ template ပြောင်းမယ် ဆိုရင် အောက်ပါအတိုင်း ပြောင်းလို့ရကြောင်း လေ့လာခဲ့ရ...  

```
hypothesis_template = "The sentiment of this review is {}."
res = classifier(item['review'], the_labels, hypothesis_template = hypothesis_template)
```

တကယ်လို့ hypothesis template ပြောင်းပြီး run ရင် 91.7 ထိ (i.e. 3.5%↑) တက်နိုင်တယ်လို့ blog မှာရေးထား။  
အချိန်ကြာလို့ အဲဒီအဆင့်တော့ မလုပ်ကြည့်ခဲ့...  

## To Do

- Training with Myanmar data (it will require GPU and huge memory)


