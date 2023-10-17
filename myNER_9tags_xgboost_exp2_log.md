# myNER 9 Tags, XGBoost Experiment 2

ဒီတစ်ခါတော့ test set မှာ စာကြောင်းရေ တစ်ထောင် အတိဖြစ်အောင် ဒေတာကို update လုပ်ပြီး ပြန် run ထားတာပါ။  

## Bash Shell Script

Training data ကနေ နောက်ဆုံး တစ်ကြောင်းကို test data ထဲကို ရွှေ့ဖို့အတွက် shell script ကို အောက်ပါအတိုင်း ရေးခဲ့တယ်။  

```bash
#!/bin/bash

# Extract the last line of train.txt
last_line=$(tail -n 1 train.txt)

# Delete the last line from train.txt
sed -i '$d' train.txt

# Append the last line to test.txt
echo "$last_line" >> test.txt
```

run လို့ရအောင် chmod command နဲ့ executable file အဖြစ်ပြောင်း ...  

```
(base) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$ chmod +x ./add_one_line_to_test_data.sh
```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

