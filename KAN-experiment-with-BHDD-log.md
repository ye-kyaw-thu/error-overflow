# Kolmogorov-Arnold Networks (KAN) Experiment Log with Myanmar MNIST Dataset (BHDD)  

Data Path:
/home/ye/ye/exp/cpp-mnist/cpp/data/BHDD/mnist2img/data/  


```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/cpp-mnist/cpp/data/BHDD/mnist2img/data$ ls
raw  test  train
```

## fastKAN Testing

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp$ git clone https://github.com/ZiyaoLi/fast-kan
Cloning into 'fast-kan'...
remote: Enumerating objects: 202, done.
remote: Counting objects: 100% (78/78), done.
remote: Compressing objects: 100% (32/32), done.
remote: Total 202 (delta 52), reused 62 (delta 44), pack-reused 124 (from 1)
Receiving objects: 100% (202/202), 420.57 KiB | 3.86 MiB/s, done.
Resolving deltas: 100% (91/91), done.
(py3.8) ye@lst-gpu-server-197:~/ye/exp$
```

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp$ cd fast-kan/
(py3.8) ye@lst-gpu-server-197:~/ye/exp/fast-kan$ ls
efficient_kan  examples  fastkan  img  LICENSE  notebooks  README.md  setup.py  tests
(py3.8) ye@lst-gpu-server-197:~/ye/exp/fast-kan$
```

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/fast-kan$ python -m pip install .
Processing /home/ye/ye/exp/fast-kan
  Preparing metadata (setup.py) ... done
Requirement already satisfied: numpy in /home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages (from fastkan==0.0.1) (1.24.3)
Building wheels for collected packages: fastkan
  Building wheel for fastkan (setup.py) ... done
  Created wheel for fastkan: filename=fastkan-0.0.1-py3-none-any.whl size=11559 sha256=0afe08d4725f16b7db46be39f3d9347bcd03752e924b272eda406d15438cdcec
  Stored in directory: /home/ye/.cache/pip/wheels/32/59/a1/9c68636747d3dc40982fe9f461d1db3688a4124e5e3ac0b9d3
Successfully built fastkan
Installing collected packages: fastkan
Successfully installed fastkan-0.0.1
(py3.8) ye@lst-gpu-server-197:~/ye/exp/fast-kan$
```

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/fast-kan$ time python examples/train_mnist.py
Traceback (most recent call last):
  File "examples/train_mnist.py", line 24, in <module>
    import torchvision
ModuleNotFoundError: No module named 'torchvision'

real    0m2.463s
user    0m3.240s
sys     0m2.166s
(py3.8) ye@lst-gpu-server-197:~/ye/exp/fast-kan$
```

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/fast-kan$ python -m pip install torchvision
...
...
...
Downloading torchvision-0.19.1-cp38-cp38-manylinux1_x86_64.whl (7.0 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 7.0/7.0 MB 27.6 MB/s eta 0:00:00
Downloading torch-2.4.1-cp38-cp38-manylinux1_x86_64.whl (797.1 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 797.1/797.1 MB 7.6 MB/s eta 0:00:00
Downloading nvidia_cudnn_cu12-9.1.0.70-py3-none-manylinux2014_x86_64.whl (664.8 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 664.8/664.8 MB 6.9 MB/s eta 0:00:00
Downloading triton-3.0.0-1-cp38-cp38-manylinux2014_x86_64.manylinux_2_17_x86_64.whl (209.4 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 209.4/209.4 MB 18.4 MB/s eta 0:00:00
Downloading typing_extensions-4.12.2-py3-none-any.whl (37 kB)
Installing collected packages: typing-extensions, triton, nvidia-cudnn-cu12, torch, torchvision
  Attempting uninstall: typing-extensions
    Found existing installation: typing_extensions 4.5.0
    Uninstalling typing_extensions-4.5.0:
      Successfully uninstalled typing_extensions-4.5.0
  Attempting uninstall: triton
    Found existing installation: triton 2.3.0
    Uninstalling triton-2.3.0:
      Successfully uninstalled triton-2.3.0
  Attempting uninstall: nvidia-cudnn-cu12
    Found existing installation: nvidia-cudnn-cu12 8.9.2.26
    Uninstalling nvidia-cudnn-cu12-8.9.2.26:
      Successfully uninstalled nvidia-cudnn-cu12-8.9.2.26
  Attempting uninstall: torch
    Found existing installation: torch 2.3.0
    Uninstalling torch-2.3.0:
      Successfully uninstalled torch-2.3.0
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
tensorflow 2.13.1 requires typing-extensions<4.6.0,>=3.6.6, but you have typing-extensions 4.12.2 which is incompatible.
Successfully installed nvidia-cudnn-cu12-9.1.0.70 torch-2.4.1 torchvision-0.19.1 triton-3.0.0 typing-extensions-4.12.2

```

Example code နဲ့ English MNIST digit data ကိုသုံး training လုပ်ကြည့်ခဲ့တယ်။  
 
```
Epoch 8, Val Loss: 0.09376249749344702, Val Accuracy: 0.9720342356687898
100%|████████████████████████████████████████████████| 938/938 [00:21<00:00, 44.44it/s, accuracy=1, loss=0.00535, lr=0.000168]
Epoch 9, Val Loss: 0.08869310630564015, Val Accuracy: 0.9747213375796179
100%|██████████████████████████████████████████████████| 938/938 [00:20<00:00, 45.53it/s, accuracy=1, loss=0.026, lr=0.000134]
Epoch 10, Val Loss: 0.09233270373412669, Val Accuracy: 0.9732285031847133
100%|████████████████████████████████████████████████| 938/938 [00:20<00:00, 45.82it/s, accuracy=1, loss=0.00103, lr=0.000107]
Epoch 11, Val Loss: 0.09045734236031329, Val Accuracy: 0.9737261146496815
100%|█████████████████████████████████████████████████| 938/938 [00:20<00:00, 45.64it/s, accuracy=1, loss=0.00179, lr=8.59e-5]
Epoch 12, Val Loss: 0.0873389472976582, Val Accuracy: 0.9751194267515924
100%|█████████████████████████████████████████████████| 938/938 [00:21<00:00, 43.54it/s, accuracy=1, loss=0.00741, lr=6.87e-5]
Epoch 13, Val Loss: 0.08844012664161084, Val Accuracy: 0.976015127388535
100%|██████████████████████████████████████████████████| 938/938 [00:21<00:00, 44.43it/s, accuracy=1, loss=0.00246, lr=5.5e-5]
Epoch 14, Val Loss: 0.08800038928884359, Val Accuracy: 0.9746218152866242
100%|█████████████████████████████████████████████████| 938/938 [00:20<00:00, 45.16it/s, accuracy=1, loss=0.000144, lr=4.4e-5]
Epoch 15, Val Loss: 0.09144832917132636, Val Accuracy: 0.9751194267515924
100%|██████████████████████████████████████████████████| 938/938 [00:20<00:00, 44.87it/s, accuracy=1, loss=0.0111, lr=3.52e-5]
Epoch 16, Val Loss: 0.08884847140792204, Val Accuracy: 0.9754179936305732
100%|█████████████████████████████████████████████████| 938/938 [00:23<00:00, 39.77it/s, accuracy=1, loss=0.00569, lr=2.81e-5]
Epoch 17, Val Loss: 0.08928039368246846, Val Accuracy: 0.9755175159235668
100%|█████████████████████████████████████████████████| 938/938 [00:20<00:00, 46.24it/s, accuracy=1, loss=0.00278, lr=2.25e-5]
Epoch 18, Val Loss: 0.08915415901168336, Val Accuracy: 0.9761146496815286
100%|███████████████████████████████████████████████████| 938/938 [00:21<00:00, 44.49it/s, accuracy=1, loss=0.0023, lr=1.8e-5]
Epoch 19, Val Loss: 0.08968261664610573, Val Accuracy: 0.9757165605095541
100%|█████████████████████████████████████████████████| 938/938 [00:21<00:00, 44.55it/s, accuracy=1, loss=0.00473, lr=1.44e-5]
Epoch 20, Val Loss: 0.08969042365603107, Val Accuracy: 0.9758160828025477

real    8m24.890s
user    60m36.322s
sys     0m23.066s
(py3.8) ye@lst-gpu-server-197:~/ye/exp/fast-kan$ time python examples/train_mnist.py | tee train1.log
```

training မလုပ်ခင် download လုပ်ပြီး အောက်ပါ path မှာ MNIST data ကိုသိမ်းတယ်။  

```
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST/raw$ ls
t10k-images-idx3-ubyte     t10k-labels-idx1-ubyte     train-images-idx3-ubyte     train-labels-idx1-ubyte
t10k-images-idx3-ubyte.gz  t10k-labels-idx1-ubyte.gz  train-images-idx3-ubyte.gz  train-labels-idx1-ubyte.gz
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST/raw$
```

## Data Preparation with BHDD

```
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST/my_raw$ cp ../../../../cpp-mnist/cpp/data/BHDD/*ubyte .
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST/my_raw$ ls
t10k-images.idx3-ubyte  t10k-labels.idx1-ubyte  train-images.idx3-ubyte  train-labels.idx1-ubyte
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST/my_raw$
```

Change filename ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST/my_raw$ mv t10k-images.idx3-ubyte t10k-images-idx3-ubyte
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST/my_raw$ mv t10k-labels.idx1-ubyte t10k-labels-idx1-ubyte
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST/my_raw$ mv train-images.idx3-ubyte train-images-idx3-ubyte
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST/my_raw$ mv train-labels.idx1-ubyte train-labels-idx1-ubyte
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST/my_raw$ ls
t10k-images-idx3-ubyte  t10k-labels-idx1-ubyte  train-images-idx3-ubyte  train-labels-idx1-ubyte
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST/my_raw$
```

ကုဒ်ကို ဝင်ကြည့်တော့ အင်္ဂလိပ်စာ MNIST dataset နဲ့ ပတ်သက်ပြီး torchvision library ကို သုံးထားတာမို့လို့ အလွယ်ဆုံးအနေနဲ့ အင်္ဂလိပ်စာ ဒေတာကို ဖိုလ်ဒါ အသစ်အောက်ကို ရွှေ့လိုက်ပြီး မြန်မာဒေတာကို သတ်မှတ်ထားတဲ့ path အောက်ကိုပဲ ရွှေ့လိုက်တာကောင်းတာမို့လို့ အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့တယ်။   


```
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST/raw$ ls
t10k-images-idx3-ubyte     t10k-labels-idx1-ubyte     train-images-idx3-ubyte     train-labels-idx1-ubyte
t10k-images-idx3-ubyte.gz  t10k-labels-idx1-ubyte.gz  train-images-idx3-ubyte.gz  train-labels-idx1-ubyte.gz
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST/raw$ cd ..
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST$ mv raw en_raw
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST$ ls
en_raw  my_raw
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST$ mv my_raw raw
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST$ cd raw
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST/raw$ ls
t10k-images-idx3-ubyte  t10k-labels-idx1-ubyte  train-images-idx3-ubyte  train-labels-idx1-ubyte
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST/raw$
```

confirmation ...  
မြန်မာစာ ဒေတာရဲ့ filesize က အောက်ပါအတိုင်း ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST/raw$ wc *
   58093   230240 21607840 t10k-images-idx3-ubyte
       0        1    27569 t10k-labels-idx1-ubyte
  121880   484576 47040016 train-images-idx3-ubyte
       0        1    60008 train-labels-idx1-ubyte
  179973   714818 68735433 total
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST/raw$
```

အင်္ဂလိပ်စာ အော်ရဂျင်နယ် MNIST ဒေတာရဲ့ filesize က အောက်ပါအတိုင်း ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST/raw$ cd ../en_raw/
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST/en_raw$ wc *
    6055    30268  7840016 t10k-images-idx3-ubyte
    6121    34683  1648877 t10k-images-idx3-ubyte.gz
       0        1    10008 t10k-labels-idx1-ubyte
      19       92     4542 t10k-labels-idx1-ubyte.gz
   35282   180029 47040016 train-images-idx3-ubyte
   36468   207693  9912422 train-images-idx3-ubyte.gz
       0        1    60008 train-labels-idx1-ubyte
      94      656    28881 train-labels-idx1-ubyte.gz
   84039   453423 66544770 total
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan/data/MNIST/en_raw$
```

## Updatin the Script  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/fast-kan/examples$ cp train_mnist.py train_mydigit_mnist.py
(py3.8) ye@lst-gpu-server-197:~/ye/exp/fast-kan/examples$ nano train_mydigit_mnist.py
```

I updated followings:  

```python
# Load MNIST
transform = transforms.Compose(
    [transforms.ToTensor(), transforms.Normalize((0.5,), (0.5,))]
)
trainset = torchvision.datasets.MNIST(
    root="./data", train=True, download=False, transform=transform
)
valset = torchvision.datasets.MNIST(
    root="./data", train=False, download=False, transform=transform
)
```

## Training with Myanmar MNIST Dataset 

```
Epoch 7, Val Loss: 0.037458339687527306, Val Accuracy: 0.9904654872389791
100%|████████████████████████████████████████████████| 938/938 [00:21<00:00, 43.30it/s, accuracy=1, loss=0.000382, lr=0.00021]
Epoch 8, Val Loss: 0.038301448164123654, Val Accuracy: 0.9907555104408353
100%|████████████████████████████████████████████████| 938/938 [00:20<00:00, 46.14it/s, accuracy=1, loss=0.00295, lr=0.000168]
Epoch 9, Val Loss: 0.037093662324259806, Val Accuracy: 0.9912993039443155
100%|████████████████████████████████████████████████| 938/938 [00:20<00:00, 45.25it/s, accuracy=1, loss=0.00198, lr=0.000134]
Epoch 10, Val Loss: 0.03809450199049176, Val Accuracy: 0.9912993039443155
100%|████████████████████████████████████████████████| 938/938 [00:20<00:00, 45.01it/s, accuracy=1, loss=7.37e-5, lr=0.000107]
Epoch 11, Val Loss: 0.03672503804713512, Val Accuracy: 0.9916255800464037
100%|████████████████████████████████████████████████| 938/938 [00:20<00:00, 46.50it/s, accuracy=1, loss=0.000642, lr=8.59e-5]
Epoch 12, Val Loss: 0.03771172020712105, Val Accuracy: 0.9914080626450116
100%|████████████████████████████████████████████████| 938/938 [00:20<00:00, 44.95it/s, accuracy=1, loss=0.000716, lr=6.87e-5]
Epoch 13, Val Loss: 0.037647917602307665, Val Accuracy: 0.9915168213457076
100%|█████████████████████████████████████████████████| 938/938 [00:20<00:00, 45.42it/s, accuracy=1, loss=0.000235, lr=5.5e-5]
Epoch 14, Val Loss: 0.03777014072525447, Val Accuracy: 0.9918793503480279
100%|█████████████████████████████████████████████████| 938/938 [00:24<00:00, 38.35it/s, accuracy=1, loss=0.000128, lr=4.4e-5]
Epoch 15, Val Loss: 0.03821655411558776, Val Accuracy: 0.9916255800464037
100%|████████████████████████████████████████████████| 938/938 [00:22<00:00, 41.35it/s, accuracy=1, loss=0.000122, lr=3.52e-5]
Epoch 16, Val Loss: 0.03791082280821285, Val Accuracy: 0.992169373549884
100%|█████████████████████████████████████████████████| 938/938 [00:20<00:00, 45.56it/s, accuracy=1, loss=4.92e-5, lr=2.81e-5]
Epoch 17, Val Loss: 0.03883025325582743, Val Accuracy: 0.9917343387470998
100%|████████████████████████████████████████████████| 938/938 [00:22<00:00, 41.16it/s, accuracy=1, loss=0.000562, lr=2.25e-5]
Epoch 18, Val Loss: 0.03919304565681957, Val Accuracy: 0.9914080626450116
100%|█████████████████████████████████████████████████| 938/938 [00:22<00:00, 42.21it/s, accuracy=1, loss=0.000416, lr=1.8e-5]
Epoch 19, Val Loss: 0.03834315259555634, Val Accuracy: 0.992133120649652
100%|████████████████████████████████████████████████| 938/938 [00:20<00:00, 45.76it/s, accuracy=1, loss=0.000186, lr=1.44e-5]
Epoch 20, Val Loss: 0.03913216256687667, Val Accuracy: 0.99227813225058

real    9m36.818s
user    69m50.400s
sys     0m22.097s
(py3.8) ye@lst-gpu-server-197:~/ye/exp/fast-kan$ time python examples/train_mydigit_mnist.py | tee train_my1.log
```

မြန်မာစာအတွက် အလုပ်လုပ်တယ်။  

## Log for Training with English MNIST Dataset  

အင်္ဂလိပ်စာနဲ့ မြန်မာစာ MNIST အကြား နှိုင်းယှဉ်ကြည့်ချင်လို့ log ဖိုင် တစ်ခုလုံးကို copy/paste လုပ်ခဲ့...  

```
Downloading http://yann.lecun.com/exdb/mnist/train-images-idx3-ubyte.gz
Failed to download (trying next):
<urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: certificate has expired (_ssl.c:1131)>

Downloading https://ossci-datasets.s3.amazonaws.com/mnist/train-images-idx3-ubyte.gz
Downloading https://ossci-datasets.s3.amazonaws.com/mnist/train-images-idx3-ubyte.gz to ./data/MNIST/raw/train-images-idx3-ubyte.gz
Extracting ./data/MNIST/raw/train-images-idx3-ubyte.gz to ./data/MNIST/raw

Downloading http://yann.lecun.com/exdb/mnist/train-labels-idx1-ubyte.gz
Failed to download (trying next):
<urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: certificate has expired (_ssl.c:1131)>

Downloading https://ossci-datasets.s3.amazonaws.com/mnist/train-labels-idx1-ubyte.gz
Downloading https://ossci-datasets.s3.amazonaws.com/mnist/train-labels-idx1-ubyte.gz to ./data/MNIST/raw/train-labels-idx1-ubyte.gz
Extracting ./data/MNIST/raw/train-labels-idx1-ubyte.gz to ./data/MNIST/raw

Downloading http://yann.lecun.com/exdb/mnist/t10k-images-idx3-ubyte.gz
Failed to download (trying next):
<urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: certificate has expired (_ssl.c:1131)>

Downloading https://ossci-datasets.s3.amazonaws.com/mnist/t10k-images-idx3-ubyte.gz
Downloading https://ossci-datasets.s3.amazonaws.com/mnist/t10k-images-idx3-ubyte.gz to ./data/MNIST/raw/t10k-images-idx3-ubyte.gz
Extracting ./data/MNIST/raw/t10k-images-idx3-ubyte.gz to ./data/MNIST/raw

Downloading http://yann.lecun.com/exdb/mnist/t10k-labels-idx1-ubyte.gz
Failed to download (trying next):
<urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: certificate has expired (_ssl.c:1131)>

Downloading https://ossci-datasets.s3.amazonaws.com/mnist/t10k-labels-idx1-ubyte.gz
Downloading https://ossci-datasets.s3.amazonaws.com/mnist/t10k-labels-idx1-ubyte.gz to ./data/MNIST/raw/t10k-labels-idx1-ubyte.gz
Extracting ./data/MNIST/raw/t10k-labels-idx1-ubyte.gz to ./data/MNIST/raw

Epoch 1, Val Loss: 0.20898432871860684, Val Accuracy: 0.9375
Epoch 2, Val Loss: 0.1651415440556445, Val Accuracy: 0.9489450636942676
Epoch 3, Val Loss: 0.12208067421403945, Val Accuracy: 0.9623805732484076
Epoch 4, Val Loss: 0.1070858940265622, Val Accuracy: 0.9659633757961783
Epoch 5, Val Loss: 0.10388810640708158, Val Accuracy: 0.9684514331210191
Epoch 6, Val Loss: 0.0937126829225131, Val Accuracy: 0.9699442675159236
Epoch 7, Val Loss: 0.09094872543993139, Val Accuracy: 0.972531847133758
Epoch 8, Val Loss: 0.09376249749344702, Val Accuracy: 0.9720342356687898
Epoch 9, Val Loss: 0.08869310630564015, Val Accuracy: 0.9747213375796179
Epoch 10, Val Loss: 0.09233270373412669, Val Accuracy: 0.9732285031847133
Epoch 11, Val Loss: 0.09045734236031329, Val Accuracy: 0.9737261146496815
Epoch 12, Val Loss: 0.0873389472976582, Val Accuracy: 0.9751194267515924
Epoch 13, Val Loss: 0.08844012664161084, Val Accuracy: 0.976015127388535
Epoch 14, Val Loss: 0.08800038928884359, Val Accuracy: 0.9746218152866242
Epoch 15, Val Loss: 0.09144832917132636, Val Accuracy: 0.9751194267515924
Epoch 16, Val Loss: 0.08884847140792204, Val Accuracy: 0.9754179936305732
Epoch 17, Val Loss: 0.08928039368246846, Val Accuracy: 0.9755175159235668
Epoch 18, Val Loss: 0.08915415901168336, Val Accuracy: 0.9761146496815286
Epoch 19, Val Loss: 0.08968261664610573, Val Accuracy: 0.9757165605095541
Epoch 20, Val Loss: 0.08969042365603107, Val Accuracy: 0.9758160828025477
```

## Log for Training with Myanmar MNIST Dataset  

Fast-Kan နဲ့ training လုပ်ထားတာကို မှတ်ထားတဲ့ log file တစ်ခုလုံးကို copy/paste လုပ်။  

```
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan$ cat ./train_my1.log
Epoch 1, Val Loss: 0.07868036464193788, Val Accuracy: 0.9778653939196239
Epoch 2, Val Loss: 0.052181660259799416, Val Accuracy: 0.9861876450116009
Epoch 3, Val Loss: 0.07161760457095598, Val Accuracy: 0.9808018788384174
Epoch 4, Val Loss: 0.047251841728359445, Val Accuracy: 0.9869852088167054
Epoch 5, Val Loss: 0.04743943436005371, Val Accuracy: 0.9870214617169374
Epoch 6, Val Loss: 0.035625352558355486, Val Accuracy: 0.9913355568445475
Epoch 7, Val Loss: 0.037458339687527306, Val Accuracy: 0.9904654872389791
Epoch 8, Val Loss: 0.038301448164123654, Val Accuracy: 0.9907555104408353
Epoch 9, Val Loss: 0.037093662324259806, Val Accuracy: 0.9912993039443155
Epoch 10, Val Loss: 0.03809450199049176, Val Accuracy: 0.9912993039443155
Epoch 11, Val Loss: 0.03672503804713512, Val Accuracy: 0.9916255800464037
Epoch 12, Val Loss: 0.03771172020712105, Val Accuracy: 0.9914080626450116
Epoch 13, Val Loss: 0.037647917602307665, Val Accuracy: 0.9915168213457076
Epoch 14, Val Loss: 0.03777014072525447, Val Accuracy: 0.9918793503480279
Epoch 15, Val Loss: 0.03821655411558776, Val Accuracy: 0.9916255800464037
Epoch 16, Val Loss: 0.03791082280821285, Val Accuracy: 0.992169373549884
Epoch 17, Val Loss: 0.03883025325582743, Val Accuracy: 0.9917343387470998
Epoch 18, Val Loss: 0.03919304565681957, Val Accuracy: 0.9914080626450116
Epoch 19, Val Loss: 0.03834315259555634, Val Accuracy: 0.992133120649652
Epoch 20, Val Loss: 0.03913216256687667, Val Accuracy: 0.99227813225058
(base) ye@lst-gpu-server-197:~/ye/exp/fast-kan$
```

အင်္ဂလိပ်စာထက် စာရင် မြန်မာစာ ဒေတာနဲ့ ရလဒ်က ပိုတောင်ကောင်းနေတာကို တွေ့ရှိရတယ်။  

## Efficient-KAN

နောက်ထပ် approach တမျိုးဖြစ်တဲ့ Efficient-KAN နဲ့ပါ စမ်းကြည့်ချင်တယ်။ အရင်ဆုံး Git Clone လုပ်...  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp$ git clone https://github.com/Blealtan/efficient-kan
Cloning into 'efficient-kan'...
remote: Enumerating objects: 90, done.
remote: Counting objects: 100% (29/29), done.
remote: Compressing objects: 100% (15/15), done.
remote: Total 90 (delta 22), reused 14 (delta 14), pack-reused 61 (from 1)
Receiving objects: 100% (90/90), 33.26 KiB | 16.63 MiB/s, done.
Resolving deltas: 100% (33/33), done.
(py3.8) ye@lst-gpu-server-197:~/ye/exp$
```

Check file/folder ...  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/efficient-kan$ ls
examples  LICENSE  pdm.lock  pyproject.toml  README.md  src  tests
(py3.8) ye@lst-gpu-server-197:~/ye/exp/efficient-kan$
```

English MNIST နဲ့ training စမ်းလုပ်ကြည့်ခဲ့...  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/efficient-kan/examples$ time python ./mnist.py | tee train1.log
...
...
...
IDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
Extracting ./data/MNIST/raw/t10k-labels-idx1-ubyte.gz to ./data/MNIST/raw

100%|█████████████████████████████████████████████████| 938/938 [00:24<00:00, 38.17it/s, accuracy=0.812, loss=0.369, lr=0.001]
Epoch 1, Val Loss: 0.22909986963910853, Val Accuracy: 0.9344148089171974
100%|███████████████████████████████████████████████████| 938/938 [00:24<00:00, 38.26it/s, accuracy=1, loss=0.0286, lr=0.0008]
Epoch 2, Val Loss: 0.16067659008393811, Val Accuracy: 0.9544187898089171
100%|███████████████████████████████████████████████| 938/938 [00:24<00:00, 38.29it/s, accuracy=0.969, loss=0.196, lr=0.00064]
Epoch 3, Val Loss: 0.13655136651389158, Val Accuracy: 0.9606886942675159
100%|█████████████████████████████████████████████| 938/938 [00:22<00:00, 40.84it/s, accuracy=0.969, loss=0.0751, lr=0.000512]
Epoch 4, Val Loss: 0.11711364034133234, Val Accuracy: 0.9645700636942676
100%|███████████████████████████████████████████████| 938/938 [00:24<00:00, 37.95it/s, accuracy=0.938, loss=0.183, lr=0.00041]
Epoch 5, Val Loss: 0.1061655233456949, Val Accuracy: 0.9686504777070064
100%|█████████████████████████████████████████████| 938/938 [00:24<00:00, 38.52it/s, accuracy=0.938, loss=0.0745, lr=0.000328]
Epoch 6, Val Loss: 0.09962393853896458, Val Accuracy: 0.9692476114649682
100%|█████████████████████████████████████████████████| 938/938 [00:24<00:00, 38.19it/s, accuracy=1, loss=0.0362, lr=0.000262]
Epoch 7, Val Loss: 0.0967597441501607, Val Accuracy: 0.9710390127388535
100%|█████████████████████████████████████████████████| 938/938 [00:23<00:00, 40.01it/s, accuracy=1, loss=0.00855, lr=0.00021]
Epoch 8, Val Loss: 0.0942270915045486, Val Accuracy: 0.9718351910828026
100%|█████████████████████████████████████████████████| 938/938 [00:23<00:00, 39.32it/s, accuracy=1, loss=0.0143, lr=0.000168]
Epoch 9, Val Loss: 0.09375342491504018, Val Accuracy: 0.9708399681528662
100%|█████████████████████████████████████████████████| 938/938 [00:24<00:00, 37.77it/s, accuracy=1, loss=0.0146, lr=0.000134]
Epoch 10, Val Loss: 0.0922346300750253, Val Accuracy: 0.972531847133758

real    5m6.434s
user    40m32.814s
sys     0m25.259s
```

5 min ဆိုတာက MNIST dataset ကို download လုပ်ယူတဲ့ အချိန်ပါ အပါအဝင်။  

## Preparing Myanmar MNIST Data for Training with Efficient-KAN  

ပြီးတာနဲ့ မြန်မာစာ ဒေတာနဲ့ training လုပ်ဖို့ အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့...  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/efficient-kan/examples/data/MNIST$ mv raw en_raw
(py3.8) ye@lst-gpu-server-197:~/ye/exp/efficient-kan/examples/data/MNIST$ cp ../../../../fast-kan/data/MNIST/
en_raw/ raw/
```

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/efficient-kan/examples/data/MNIST$ cp -r ../../../../fast-kan/data/MNIST/raw/ .
(py3.8) ye@lst-gpu-server-197:~/ye/exp/efficient-kan/examples/data/MNIST$ ls
en_raw  raw
(py3.8) ye@lst-gpu-server-197:~/ye/exp/efficient-kan/examples/data/MNIST$
```

## Copy/Update Efficient-KAN Script

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/efficient-kan/examples$ cp mnist.py ef_kan_my_mnist.py
(py3.8) ye@lst-gpu-server-197:~/ye/exp/efficient-kan/examples$ ls
data  ef_kan_my_mnist.py  mnist.py  train1.log
(py3.8) ye@lst-gpu-server-197:~/ye/exp/efficient-kan/examples$
```

Edited not for download MNIST dataset as follows:  

```python
# Load MNIST
transform = transforms.Compose(
    [transforms.ToTensor(), transforms.Normalize((0.5,), (0.5,))]
)
trainset = torchvision.datasets.MNIST(
    root="./data", train=True, download=False, transform=transform
)
valset = torchvision.datasets.MNIST(
    root="./data", train=False, download=False, transform=transform
)
```

## Efficient-KAN Training with My Digit MNIST Dataset

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/efficient-kan/examples$ time python ./ef_kan_my_mnist.py | tee train_efkan_my1.log
/home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages/torch/cuda/__init__.py:128: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
100%|████████████████████████████████████████████████████| 938/938 [00:23<00:00, 39.91it/s, accuracy=1, loss=0.0508, lr=0.001]
Epoch 1, Val Loss: 0.06939179582949166, Val Accuracy: 0.9835411832946636
100%|██████████████████████████████████████████████████| 938/938 [00:24<00:00, 38.44it/s, accuracy=1, loss=0.00952, lr=0.0008]
Epoch 2, Val Loss: 0.056717616133175774, Val Accuracy: 0.9848100348027842
100%|██████████████████████████████████████████████████| 938/938 [00:23<00:00, 39.53it/s, accuracy=1, loss=0.0278, lr=0.00064]
Epoch 3, Val Loss: 0.0458505556588072, Val Accuracy: 0.9890878770301624
100%|██████████████████████████████████████████████| 938/938 [00:27<00:00, 33.63it/s, accuracy=0.969, loss=0.274, lr=0.000512]
Epoch 4, Val Loss: 0.05100669243195788, Val Accuracy: 0.9870577146171694
100%|█████████████████████████████████████████████████| 938/938 [00:25<00:00, 36.98it/s, accuracy=1, loss=0.00885, lr=0.00041]
Epoch 5, Val Loss: 0.04656715092833722, Val Accuracy: 0.9883787349869093
100%|████████████████████████████████████████████████| 938/938 [00:25<00:00, 36.64it/s, accuracy=1, loss=0.00171, lr=0.000328]
Epoch 6, Val Loss: 0.04261726121582402, Val Accuracy: 0.9896113335947979
100%|████████████████████████████████████████████████| 938/938 [00:23<00:00, 39.42it/s, accuracy=1, loss=0.00335, lr=0.000262]
Epoch 7, Val Loss: 0.038725778167708634, Val Accuracy: 0.9907714264022225
100%|███████████████████████████████████████████████| 938/938 [00:24<00:00, 38.20it/s, accuracy=0.969, loss=0.079, lr=0.00021]
Epoch 8, Val Loss: 0.038430296594580624, Val Accuracy: 0.9909164380031507
100%|████████████████████████████████████████████████| 938/938 [00:24<00:00, 38.18it/s, accuracy=1, loss=0.00341, lr=0.000168]
Epoch 9, Val Loss: 0.03747679092035372, Val Accuracy: 0.9906989206017585
100%|████████████████████████████████████████████████| 938/938 [00:23<00:00, 40.19it/s, accuracy=1, loss=0.00348, lr=0.000134]
Epoch 10, Val Loss: 0.03666539092547111, Val Accuracy: 0.9908439322026865

real    5m45.985s
user    48m58.446s
sys     0m10.384s
(py3.8) ye@lst-gpu-server-197:~/ye/exp/efficient-kan/examples$
```

## Comparison Between Efficient-KAN and Fast-KAN for Myanmar MNIST

| **Epoch** | **Efficient-KAN Val Accuracy** | **Fast-KAN Val Accuracy** |
|-----------|--------------------------------|---------------------------|
| 1         | 0.9835                         | 0.9779                    |
| 2         | 0.9848                         | 0.9862                    |
| 3         | 0.9891                         | 0.9808                    |
| 4         | 0.9871                         | 0.9870                    |
| 5         | 0.9884                         | 0.9870                    |
| 6         | 0.9896                         | 0.9913                    |
| 7         | 0.9908                         | 0.9905                    |
| 8         | 0.9909                         | 0.9908                    |
| 9         | 0.9907                         | 0.9913                    |
| 10        | 0.9908                         | 0.9913                    |

## Comparison Between Efficient-KAN and Fast-KAN for English MNIST

| **Epoch** | **Efficient-KAN Val Accuracy** | **Fast-KAN Val Accuracy** |
|-----------|--------------------------------|---------------------------|
| 1         | 0.9344                         | 0.9375                    |
| 2         | 0.9544                         | 0.9489                    |
| 3         | 0.9607                         | 0.9624                    |
| 4         | 0.9646                         | 0.9660                    |
| 5         | 0.9687                         | 0.9685                    |
| 6         | 0.9692                         | 0.9699                    |
| 7         | 0.9710                         | 0.9725                    |
| 8         | 0.9718                         | 0.9720                    |
| 9         | 0.9708                         | 0.9747                    |
| 10        | 0.9725                         | 0.9732                    |


## Baseline Preparation  

CPP code နဲ့ ရေးထားတာကို နောက်တစ်ခေါက် ပြန် run ကြည့်ဖို့ ပြင်ဆင်ခဲ့...  
VOA-Burmese အင်တာဗျူးအတွက် run ခဲ့တဲ့ model ဖိုင်တွေကို ဖျက်ခဲ့ ... 

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/cpp-mnist/cpp_run-again$ ls
BHDD.model.dat  BHDD.test.verbose.hyp  chk-hyp.sh  hyp.txt           mnist_classifier.cpp     model.dat  test-output.txt
BHDD.test.hyp   bk                     data        mnist_classifier  mnist_classifier.cpp.bk  nn-archi
(py3.8) ye@lst-gpu-server-197:~/ye/exp/cpp-mnist/cpp_run-again$ ls *.dat
BHDD.model.dat  model.dat
(py3.8) ye@lst-gpu-server-197:~/ye/exp/cpp-mnist/cpp_run-again$ rm *.dat
(py3.8) ye@lst-gpu-server-197:~/ye/exp/cpp-mnist/cpp_run-again$ ls
BHDD.test.hyp          bk          data     mnist_classifier      mnist_classifier.cpp.bk  test-output.txt
BHDD.test.verbose.hyp  chk-hyp.sh  hyp.txt  mnist_classifier.cpp  nn-archi
(py3.8) ye@lst-gpu-server-197:~/ye/exp/cpp-mnist/cpp_run-again$
```

Check --help Information:  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/cpp-mnist/cpp_run-again$ ./mnist_classifier -h
Usage: ./mnist_classifier [options]
Options:
  -t                  Test mode
  -v [verbose]        Enable verbose output in test mode
  -m [model_file]     Specify model file (default: model.dat)
  -e [epochs]         Number of training epochs (default: 20)
  -r [learning_rate]  Learning rate (default: 0.001)
  -x [train_img_file]  Train image file (default: train-images.idx3-ubyte)
  -i [test_img_file]  Test image file (default: t10k-images.idx3-ubyte)
  -y [train_lbl_file]  Train label file (default: train-labels.idx1-ubyte)
  -l [test_lbl_file]  Test label file (default: t10k-labels.idx1-ubyte)
  -o [hyp_file]       Hypothesis output file (default: hyp.txt)
  -h, --help          Display this help message
```

## Example Runnings

Example Commands:  
Training Mode (default):  

```bash
./mnist_classifier
```

Training with custom epochs and learning rate:  

```bash
./mnist_classifier -e 30 -r 0.002
```

Testing Mode:  

```bash
./mnist_classifier -t
```

Testing with custom test files and hypothesis output:  

```bash
./mnist_classifier -t -i custom_test_images.idx3-ubyte -l custom_test_labels.idx1-ubyte -o custom_hyp.txt
```

## Training CPP NN with Myanmar Digit MNIST

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/cpp-mnist/cpp_run-again$ time ./mnist_classifier -e 10 -m BHDD.e10.model.dat
Running in training mode...
Epoch 1: Loss = 0.469699, Accuracy = 0.87955
Epoch 2: Loss = 0.249069, Accuracy = 0.930683
Epoch 3: Loss = 0.194124, Accuracy = 0.944833
Epoch 4: Loss = 0.159204, Accuracy = 0.955233
Epoch 5: Loss = 0.134712, Accuracy = 0.96275
Epoch 6: Loss = 0.117076, Accuracy = 0.968033
Epoch 7: Loss = 0.103041, Accuracy = 0.9718
Epoch 8: Loss = 0.0919852, Accuracy = 0.974917
Epoch 9: Loss = 0.0832072, Accuracy = 0.9774
Epoch 10: Loss = 0.0758721, Accuracy = 0.9792
Model saved to BHDD.e10.model.dat

real    103m6.788s
user    103m3.867s
sys     0m2.424s
(py3.8) ye@lst-gpu-server-197:~/ye/exp/cpp-mnist/cpp_run-again$
```

Testing with BHDD.e10.model.dat model  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/cpp-mnist/cpp_run-again$ (py3.8) ye@lst-gpu-server-197:~/ye/exp/cpp-mnist/cpp_run-again$ time ./mnist_classifier -t -m ./BHDD.e10.model.dat
Running in testing mode...
Accuracy = 0.9743
Hypothesis results saved to hyp.txt

real    0m28.115s
user    0m28.067s
sys     0m0.044s
(py3.8) ye@lst-gpu-server-197:~/ye/exp/cpp-mnist/cpp_run-again$
```

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/cpp-mnist/cpp_run-again$ head hyp.txt
7       7
2       2
1       1
0       0
4       4
1       1
4       4
9       9
5       6
9       9
(py3.8) ye@lst-gpu-server-197:~/ye/exp/cpp-mnist/cpp_run-again$
```

## Training with MLP Python  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/fast-kan$ time python ./examples/train_mlp_mydigit_mnist.py | tee mlp_my_train1.log
...
...
...
Epoch 7, Val Loss: 0.055633266083139864, Val Accuracy: 0.9868039443155452
100%|█████████████████████████████████████████████████| 938/938 [00:16<00:00, 56.70it/s, accuracy=1, loss=0.0214, lr=0.000478]
Epoch 8, Val Loss: 0.06667835194360369, Val Accuracy: 0.9820910672853829
100%|█████████████████████████████████████████████████| 938/938 [00:16<00:00, 56.93it/s, accuracy=1, loss=0.00317, lr=0.00043]
Epoch 9, Val Loss: 0.0506974748393041, Val Accuracy: 0.9872027262180975
100%|█████████████████████████████████████████████████| 938/938 [00:16<00:00, 56.61it/s, accuracy=1, loss=0.0166, lr=0.000387]
Epoch 10, Val Loss: 0.054061157238862005, Val Accuracy: 0.9872027262180975
100%|█████████████████████████████████████████████████| 938/938 [00:16<00:00, 55.57it/s, accuracy=1, loss=0.0352, lr=0.000349]
Epoch 11, Val Loss: 0.04700624127129499, Val Accuracy: 0.9889791183294664
100%|█████████████████████████████████████████████████| 938/938 [00:16<00:00, 56.00it/s, accuracy=1, loss=0.0109, lr=0.000314]
Epoch 12, Val Loss: 0.0526707608887781, Val Accuracy: 0.9880365429234339
100%|█████████████████████████████████████████████████| 938/938 [00:16<00:00, 57.02it/s, accuracy=1, loss=0.0213, lr=0.000282]
Epoch 13, Val Loss: 0.05192317082271144, Val Accuracy: 0.98814530162413
100%|█████████████████████████████████████████████████| 938/938 [00:17<00:00, 54.69it/s, accuracy=1, loss=0.0345, lr=0.000254]
Epoch 14, Val Loss: 0.04522583544405022, Val Accuracy: 0.9893779002320185
100%|█████████████████████████████████████████████████| 938/938 [00:19<00:00, 46.93it/s, accuracy=1, loss=0.0127, lr=0.000229]
Epoch 15, Val Loss: 0.04995414942294724, Val Accuracy: 0.98814530162413
100%|█████████████████████████████████████████████| 938/938 [00:19<00:00, 47.89it/s, accuracy=0.969, loss=0.0367, lr=0.000206]
Epoch 16, Val Loss: 0.0488798811875355, Val Accuracy: 0.9890516241299304
100%|█████████████████████████████████████████████████| 938/938 [00:19<00:00, 48.57it/s, accuracy=1, loss=0.0353, lr=0.000185]
Epoch 17, Val Loss: 0.04369963246698571, Val Accuracy: 0.9897766821345708
100%|██████████████████████████████████████████████| 938/938 [00:19<00:00, 47.94it/s, accuracy=0.969, loss=0.155, lr=0.000167]
Epoch 18, Val Loss: 0.04229766064865856, Val Accuracy: 0.990139211136891
100%|██████████████████████████████████████████████████| 938/938 [00:18<00:00, 49.44it/s, accuracy=1, loss=0.0225, lr=0.00015]
Epoch 19, Val Loss: 0.0473802957838842, Val Accuracy: 0.9891241299303944
100%|██████████████████████████████████████████████| 938/938 [00:16<00:00, 56.44it/s, accuracy=0.969, loss=0.151, lr=0.000135]
Epoch 20, Val Loss: 0.04367011838903615, Val Accuracy: 0.990284222737819

real    8m16.909s
user    45m14.405s
sys     0m6.674s
```

The whole log of training with traditional MLP on BHDD dataset:  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/fast-kan$ cat ./mlp_my_train1.log
Epoch 1, Val Loss: 0.13543184886399112, Val Accuracy: 0.96111213289668
Epoch 2, Val Loss: 0.08219111166686995, Val Accuracy: 0.9792995939675174
Epoch 3, Val Loss: 0.08235773212857665, Val Accuracy: 0.978010405520552
Epoch 4, Val Loss: 0.08208220629151176, Val Accuracy: 0.9782279229219442
Epoch 5, Val Loss: 0.06638461599459228, Val Accuracy: 0.9841212296983759
Epoch 6, Val Loss: 0.05296029206087138, Val Accuracy: 0.9875290023201856
Epoch 7, Val Loss: 0.055633266083139864, Val Accuracy: 0.9868039443155452
Epoch 8, Val Loss: 0.06667835194360369, Val Accuracy: 0.9820910672853829
Epoch 9, Val Loss: 0.0506974748393041, Val Accuracy: 0.9872027262180975
Epoch 10, Val Loss: 0.054061157238862005, Val Accuracy: 0.9872027262180975
Epoch 11, Val Loss: 0.04700624127129499, Val Accuracy: 0.9889791183294664
Epoch 12, Val Loss: 0.0526707608887781, Val Accuracy: 0.9880365429234339
Epoch 13, Val Loss: 0.05192317082271144, Val Accuracy: 0.98814530162413
Epoch 14, Val Loss: 0.04522583544405022, Val Accuracy: 0.9893779002320185
Epoch 15, Val Loss: 0.04995414942294724, Val Accuracy: 0.98814530162413
Epoch 16, Val Loss: 0.0488798811875355, Val Accuracy: 0.9890516241299304
Epoch 17, Val Loss: 0.04369963246698571, Val Accuracy: 0.9897766821345708
Epoch 18, Val Loss: 0.04229766064865856, Val Accuracy: 0.990139211136891
Epoch 19, Val Loss: 0.0473802957838842, Val Accuracy: 0.9891241299303944
Epoch 20, Val Loss: 0.04367011838903615, Val Accuracy: 0.990284222737819
(py3.8) ye@lst-gpu-server-197:~/ye/exp/fast-kan$
```

## Experiment with FasterKAN

Efficient < Fast-KAN < Faster-KAN ဆိုပြီး Faster-KAN က အမြန်ဆုံး ပိုပြီး efficient ဖြစ်တယ်လို့ claim လုပ်ထားတာကြောင့် Faster-KAN နဲ့လည်း စမ်းကြည့်ဖို့ ပြင်ဆင်...  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp$ git clone https://github.com/AthanasiosDelis/faster-kan
Cloning into 'faster-kan'...
remote: Enumerating objects: 356, done.
remote: Counting objects: 100% (146/146), done.
remote: Compressing objects: 100% (86/86), done.
remote: Total 356 (delta 86), reused 112 (delta 58), pack-reused 210 (from 1)
Receiving objects: 100% (356/356), 955.13 KiB | 6.77 MiB/s, done.
Resolving deltas: 100% (167/167), done.
(py3.8) ye@lst-gpu-server-197:~/ye/exp$
```

အောက်ပါအတိုင်း Faster-KAN က Efficient-KAN ရော Fast-KAN ရော ပါနေပြီးသား... 

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/faster-kan$ ls
benchmark.py  draw_spline_basis.ipynb  fastkan      pdm.lock        test_running_time.ipynb  torchkan
cuda          efficient_kan            img          pyproject.toml  tests                    train_cifar10.py
cu_fasterkan  fasterkan                LICENSE.txt  README.md       times.txt                train_mnist.py
(py3.8) ye@lst-gpu-server-197:~/ye/exp/faster-kan$
```

Training Faster-KAN  with English MNIST ... 

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/faster-kan$ time python ./train_mnist.py | tee faster-kan-train-en-mnist.log
Traceback (most recent call last):
  File "./train_mnist.py", line 19, in <module>
    from torchsummary import summary
ModuleNotFoundError: No module named 'torchsummary'

real    0m3.203s
user    0m4.368s
sys     0m2.099s
(py3.8) ye@lst-gpu-server-197:~/ye/exp/faster-kan$
```

အထက်ပါအတိုင်း Error ပေးလို့ library ကို install လုပ်ခဲ့...  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/faster-kan$ python -m pip install torchsummary
Collecting torchsummary
  Using cached torchsummary-1.5.1-py3-none-any.whl.metadata (296 bytes)
Using cached torchsummary-1.5.1-py3-none-any.whl (2.8 kB)
Installing collected packages: torchsummary
Successfully installed torchsummary-1.5.1
(py3.8) ye@lst-gpu-server-197:~/ye/exp/faster-kan$
```

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/faster-kan$ time python ./train_mnist.py | tee faster-kan-train-en-mnist.log
Traceback (most recent call last):
  File "./train_mnist.py", line 21, in <module>
    import optuna
ModuleNotFoundError: No module named 'optuna'

real    0m3.179s
user    0m4.354s
sys     0m2.118s
(py3.8) ye@lst-gpu-server-197:~/ye/exp/faster-kan$
```

optuna ကို install လုပ်...  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/faster-kan$ python -m pip install optuna
...
...
  Downloading SQLAlchemy-2.0.36-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (9.7 kB)
Requirement already satisfied: tqdm in /home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages (from optuna) (4.66.4)
Requirement already satisfied: PyYAML in /home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages (from optuna) (6.0.1)
Collecting Mako (from alembic>=1.5.0->optuna)
  Downloading Mako-1.3.6-py3-none-any.whl.metadata (2.9 kB)
Requirement already satisfied: typing-extensions>=4 in /home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages (from alembic>=1.5.0->optuna) (4.12.2)
Requirement already satisfied: importlib-metadata in /home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages (from alembic>=1.5.0->optuna) (7.1.0)
Requirement already satisfied: importlib-resources in /home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages (from alembic>=1.5.0->optuna) (6.4.0)
Collecting greenlet!=0.4.17 (from sqlalchemy>=1.3.0->optuna)
  Downloading greenlet-3.1.1-cp38-cp38-manylinux_2_24_x86_64.manylinux_2_28_x86_64.whl.metadata (3.8 kB)
Requirement already satisfied: zipp>=0.5 in /home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages (from importlib-metadata->alembic>=1.5.0->optuna) (3.18.1)
Requirement already satisfied: MarkupSafe>=0.9.2 in /home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages (from Mako->alembic>=1.5.0->optuna) (2.1.5)
Downloading optuna-4.0.0-py3-none-any.whl (362 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 362.8/362.8 kB 4.4 MB/s eta 0:00:00
Downloading alembic-1.14.0-py3-none-any.whl (233 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 233.5/233.5 kB 34.8 MB/s eta 0:00:00
Downloading SQLAlchemy-2.0.36-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (3.1 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.1/3.1 MB 37.4 MB/s eta 0:00:00
Downloading colorlog-6.9.0-py3-none-any.whl (11 kB)
Downloading greenlet-3.1.1-cp38-cp38-manylinux_2_24_x86_64.manylinux_2_28_x86_64.whl (605 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 606.0/606.0 kB 92.7 MB/s eta 0:00:00
Downloading Mako-1.3.6-py3-none-any.whl (78 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 78.6/78.6 kB 32.4 MB/s eta 0:00:00
Installing collected packages: Mako, greenlet, colorlog, sqlalchemy, alembic, optuna
Successfully installed Mako-1.3.6 alembic-1.14.0 colorlog-6.9.0 greenlet-3.1.1 optuna-4.0.0 sqlalchemy-2.0.36
```

training with English MNIST data:  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/faster-kan$ time python ./train_mnist.py | tee faster-kan-train-en-mnist.log
```

epoch က ၁၀၀ ထိ ထားထားတာမို့ Ctrl+C နဲ့ ရပ်ပြီး code checking လုပ်ခဲ့...  
running log output က အောက်ပါအတိုင်း တွေ့ရ...  

```
Downloading http://yann.lecun.com/exdb/mnist/train-images-idx3-ubyte.gz
Failed to download (trying next):
<urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: certificate has expired (_ssl.c:1131)>

Downloading https://ossci-datasets.s3.amazonaws.com/mnist/train-images-idx3-ubyte.gz
Downloading https://ossci-datasets.s3.amazonaws.com/mnist/train-images-idx3-ubyte.gz to ./data/MNIST/raw/train-images-idx3-ubyte.gz
Extracting ./data/MNIST/raw/train-images-idx3-ubyte.gz to ./data/MNIST/raw

Downloading http://yann.lecun.com/exdb/mnist/train-labels-idx1-ubyte.gz
Failed to download (trying next):
<urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: certificate has expired (_ssl.c:1131)>

Downloading https://ossci-datasets.s3.amazonaws.com/mnist/train-labels-idx1-ubyte.gz
Downloading https://ossci-datasets.s3.amazonaws.com/mnist/train-labels-idx1-ubyte.gz to ./data/MNIST/raw/train-labels-idx1-ubyte.gz
Extracting ./data/MNIST/raw/train-labels-idx1-ubyte.gz to ./data/MNIST/raw

Downloading http://yann.lecun.com/exdb/mnist/t10k-images-idx3-ubyte.gz
Failed to download (trying next):
<urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: certificate has expired (_ssl.c:1131)>

Downloading https://ossci-datasets.s3.amazonaws.com/mnist/t10k-images-idx3-ubyte.gz
Downloading https://ossci-datasets.s3.amazonaws.com/mnist/t10k-images-idx3-ubyte.gz to ./data/MNIST/raw/t10k-images-idx3-ubyte.gz
Extracting ./data/MNIST/raw/t10k-images-idx3-ubyte.gz to ./data/MNIST/raw

Downloading http://yann.lecun.com/exdb/mnist/t10k-labels-idx1-ubyte.gz
Failed to download (trying next):
<urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: certificate has expired (_ssl.c:1131)>

Downloading https://ossci-datasets.s3.amazonaws.com/mnist/t10k-labels-idx1-ubyte.gz
Downloading https://ossci-datasets.s3.amazonaws.com/mnist/t10k-labels-idx1-ubyte.gz to ./data/MNIST/raw/t10k-labels-idx1-ubyte.gz
Extracting ./data/MNIST/raw/t10k-labels-idx1-ubyte.gz to ./data/MNIST/raw

Total parameters: 408242
Trainable parameters: 408242
Total parameters: 254410
Trainable parameters: 254410
Total parameters: 508160
Trainable parameters: 508160
Total parameters: 5128744
Trainable parameters: 5128744
Total parameters: 1427534
Trainable parameters: 1427489
----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Conv2d-1           [-1, 32, 28, 28]             320
              ReLU-2           [-1, 32, 28, 28]               0
       BatchNorm2d-3           [-1, 32, 28, 28]              64
         MaxPool2d-4           [-1, 32, 14, 14]               0
           Dropout-5           [-1, 32, 14, 14]               0
            Conv2d-6           [-1, 64, 14, 14]           2,048
       BatchNorm2d-7           [-1, 64, 14, 14]             128
            Conv2d-8           [-1, 64, 14, 14]          18,432
       BatchNorm2d-9           [-1, 64, 14, 14]             128
           Conv2d-10           [-1, 64, 14, 14]          36,864
      BatchNorm2d-11           [-1, 64, 14, 14]             128
           Conv2d-10           [-1, 64, 14, 14]          36,864
      BatchNorm2d-11           [-1, 64, 14, 14]             128
    BasicResBlock-12           [-1, 64, 14, 14]               0
AdaptiveAvgPool2d-13             [-1, 64, 1, 1]               0
           Linear-14                    [-1, 4]             256
             ReLU-15                    [-1, 4]               0
           Linear-16                   [-1, 64]             256
          Sigmoid-17                   [-1, 64]               0
          SEBlock-18           [-1, 64, 14, 14]               0
        MaxPool2d-19             [-1, 64, 7, 7]               0
          Dropout-20             [-1, 64, 7, 7]               0
           Conv2d-21             [-1, 64, 5, 5]             640
           Conv2d-22            [-1, 128, 5, 5]           8,320
DepthwiseSeparableConv-23            [-1, 128, 5, 5]               0
             ReLU-24            [-1, 128, 5, 5]               0
           Conv2d-25            [-1, 256, 5, 5]          32,768
      BatchNorm2d-26            [-1, 256, 5, 5]             512
           Conv2d-27            [-1, 256, 5, 5]         294,912
      BatchNorm2d-28            [-1, 256, 5, 5]             512
           Conv2d-29            [-1, 256, 5, 5]         589,824
      BatchNorm2d-30            [-1, 256, 5, 5]             512
    BasicResBlock-31            [-1, 256, 5, 5]               0
AdaptiveAvgPool2d-32            [-1, 256, 1, 1]               0
           Linear-33                   [-1, 16]           4,096
             ReLU-34                   [-1, 16]               0
           Linear-35                  [-1, 256]           4,096
          Sigmoid-36                  [-1, 256]               0
          SEBlock-37            [-1, 256, 5, 5]               0
        MaxPool2d-38            [-1, 256, 2, 2]               0
          Dropout-39            [-1, 256, 2, 2]               0
        MaxPool2d-38            [-1, 256, 2, 2]               0
          Dropout-39            [-1, 256, 2, 2]               0
           Conv2d-40             [-1, 32, 2, 2]           8,224
           Conv2d-41             [-1, 32, 2, 2]           8,224
           Conv2d-42            [-1, 256, 2, 2]          65,792
    SelfAttention-43            [-1, 256, 2, 2]               0
AdaptiveAvgPool2d-44            [-1, 256, 1, 1]               0
EnhancedFeatureExtractor-45                  [-1, 256]               0
        LayerNorm-46                  [-1, 256]             512
ReflectionalSwitchFunction-47               [-1, 256, 8]               0
     SplineLinear-48                  [-1, 128]         262,144
   FasterKANLayer-49                  [-1, 128]               0
        LayerNorm-50                  [-1, 128]             256
ReflectionalSwitchFunction-51               [-1, 128, 8]               0
     SplineLinear-52                   [-1, 64]          65,536
   FasterKANLayer-53                   [-1, 64]               0
        LayerNorm-54                   [-1, 64]             128
ReflectionalSwitchFunction-55                [-1, 64, 8]               0
     SplineLinear-56                   [-1, 32]          16,384
   FasterKANLayer-57                   [-1, 32]               0
        LayerNorm-58                   [-1, 32]              64
ReflectionalSwitchFunction-59                [-1, 32, 8]               0
     SplineLinear-60                   [-1, 16]           4,096
   FasterKANLayer-61                   [-1, 16]               0
        LayerNorm-62                   [-1, 16]              32
ReflectionalSwitchFunction-63                [-1, 16, 8]               0
     SplineLinear-64                   [-1, 10]           1,280
   FasterKANLayer-65                   [-1, 10]               0
================================================================
Total params: 1,427,488
Trainable params: 1,427,488
Non-trainable params: 0
----------------------------------------------------------------
Input size (MB): 0.00
Forward/backward pass size (MB): 2.04
Params size (MB): 5.45
Estimated Total Size (MB): 7.49
----------------------------------------------------------------
None
----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
         LayerNorm-1               [-1, 1, 784]           1,568
ReflectionalSwitchFunction-2            [-1, 1, 784, 8]               0
      SplineLinear-3                   [-1, 64]         401,408
    FasterKANLayer-4                   [-1, 64]               0
         LayerNorm-5                   [-1, 64]             128
ReflectionalSwitchFunction-6                [-1, 64, 8]               0
      SplineLinear-7                   [-1, 10]           5,120
    FasterKANLayer-8                   [-1, 10]               0
================================================================
Total params: 408,224
Trainable params: 408,224
Non-trainable params: 0
----------------------------------------------------------------
Input size (MB): 0.00
Forward/backward pass size (MB): 0.06
Params size (MB): 1.56
Estimated Total Size (MB): 1.62
----------------------------------------------------------------

None
Epoch 1, Val Loss: 0.4665191798073471, Val Accuracy: 0.875
Current Learning Rate: 0.001
Epoch 2, Val Loss: 0.28100106793983726, Val Accuracy: 0.9181926751592356
Current Learning Rate: 0.001
Epoch 3, Val Loss: 3.0564316275772776, Val Accuracy: 0.01910828025477707
Current Learning Rate: 0.001
Epoch 4, Val Loss: 2.313056102983511, Val Accuracy: 0.10071656050955415
Current Learning Rate: 0.0006
Epoch 5, Val Loss: 2.3109417174272475, Val Accuracy: 0.10260748407643312
Current Learning Rate: 0.0006
Epoch 6, Val Loss: 2.305247252154502, Val Accuracy: 0.12151671974522293
Current Learning Rate: 0.00035999999999999997
Epoch 7, Val Loss: 2.3062571431421173, Val Accuracy: 0.09394904458598727
Current Learning Rate: 0.00035999999999999997
Epoch 8, Val Loss: 2.302017170912141, Val Accuracy: 0.11355493630573249
Current Learning Rate: 0.00021599999999999996
Epoch 9, Val Loss: 2.3056234250402756, Val Accuracy: 0.11355493630573249
Current Learning Rate: 0.00021599999999999996
Epoch 10, Val Loss: 2.303111855391484, Val Accuracy: 0.11355493630573249
Current Learning Rate: 0.00012959999999999998
Epoch 11, Val Loss: 2.3037563144781026, Val Accuracy: 0.10151273885350319
Current Learning Rate: 0.00012959999999999998
Epoch 12, Val Loss: 2.3031081394025477, Val Accuracy: 0.11355493630573249
Current Learning Rate: 7.775999999999999e-05
Epoch 13, Val Loss: 2.3015594953184673, Val Accuracy: 0.11355493630573249
Current Learning Rate: 7.775999999999999e-05
Epoch 14, Val Loss: 2.3023030833833538, Val Accuracy: 0.11355493630573249
Current Learning Rate: 4.665599999999999e-05
Epoch 15, Val Loss: 2.3015168350972948, Val Accuracy: 0.11355493630573249
Current Learning Rate: 4.665599999999999e-05
Epoch 16, Val Loss: 2.3011455748491225, Val Accuracy: 0.11355493630573249
Current Learning Rate: 2.7993599999999992e-05
Epoch 17, Val Loss: 2.301439394616777, Val Accuracy: 0.11355493630573249
Current Learning Rate: 2.7993599999999992e-05
Epoch 18, Val Loss: 2.3009819938878344, Val Accuracy: 0.11355493630573249
Current Learning Rate: 1.6796159999999994e-05
Epoch 19, Val Loss: 2.301255329399352, Val Accuracy: 0.11355493630573249
Current Learning Rate: 1.6796159999999994e-05
Epoch 20, Val Loss: 2.301102885774746, Val Accuracy: 0.11355493630573249
Current Learning Rate: 1.0077695999999996e-05
Epoch 21, Val Loss: 2.3010246146256756, Val Accuracy: 0.11355493630573249
Current Learning Rate: 1.0077695999999996e-05
Epoch 22, Val Loss: 2.3010808874847024, Val Accuracy: 0.11355493630573249
Current Learning Rate: 6.046617599999998e-06
Epoch 23, Val Loss: 2.301036043531576, Val Accuracy: 0.11355493630573249
Current Learning Rate: 6.046617599999998e-06
Epoch 24, Val Loss: 2.3010723287132895, Val Accuracy: 0.11355493630573249
Current Learning Rate: 3.6279705599999985e-06
Epoch 25, Val Loss: 2.301019320822066, Val Accuracy: 0.11355493630573249
Current Learning Rate: 3.6279705599999985e-06
Epoch 26, Val Loss: 2.3010019770093786, Val Accuracy: 0.11355493630573249
Current Learning Rate: 2.176782335999999e-06
Epoch 27, Val Loss: 2.3010125160217285, Val Accuracy: 0.11355493630573249
Current Learning Rate: 2.176782335999999e-06
Epoch 28, Val Loss: 2.3010185083765893, Val Accuracy: 0.11355493630573249
Current Learning Rate: 1.3060694015999993e-06
Epoch 29, Val Loss: 2.301008833441765, Val Accuracy: 0.11355493630573249
Current Learning Rate: 1.3060694015999993e-06
Epoch 30, Val Loss: 2.3010346479476635, Val Accuracy: 0.11355493630573249
Current Learning Rate: 7.836416409599996e-07
Epoch 31, Val Loss: 2.301038201447505, Val Accuracy: 0.11355493630573249
Current Learning Rate: 7.836416409599996e-07
Epoch 32, Val Loss: 2.3010295788953257, Val Accuracy: 0.11355493630573249
Current Learning Rate: 4.7018498457599973e-07
Epoch 33, Val Loss: 2.301029124837013, Val Accuracy: 0.11355493630573249
Current Learning Rate: 4.7018498457599973e-07
Epoch 34, Val Loss: 2.301025862906389, Val Accuracy: 0.11355493630573249
Current Learning Rate: 2.821109907455998e-07
Epoch 35, Val Loss: 2.3010257596422914, Val Accuracy: 0.11355493630573249
Current Learning Rate: 2.821109907455998e-07
Epoch 36, Val Loss: 2.301029619897247, Val Accuracy: 0.11355493630573249
Current Learning Rate: 1.6926659444735988e-07
```

Result တွေက မကောင်းဘူး။ တစ်ခုရှိတာက ခုချိန်ထိ cuda library က အဆင်မပြေလို့ CPU ပေါ်မှာပဲ run နေတာ...  

## Faster-KAN with BHDD  

သေချာအောင် မြန်မာစာနဲ့ ဒေတာနဲ့ epoch 10 ပဲ ထားပြီး run ကြည်မယ်။  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/faster-kan/data/MNIST$ mv raw en_raw
(py3.8) ye@lst-gpu-server-197:~/ye/exp/faster-kan/data/MNIST$ ls
en_raw
(py3.8) ye@lst-gpu-server-197:~/ye/exp/faster-kan/data/MNIST$
```

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/faster-kan/data/MNIST$ cp ../../../fast-kan/data/MNIST/raw . -r
(py3.8) ye@lst-gpu-server-197:~/ye/exp/faster-kan/data/MNIST$ ls ./raw
t10k-images-idx3-ubyte  t10k-labels-idx1-ubyte  train-images-idx3-ubyte  train-labels-idx1-ubyte
(py3.8) ye@lst-gpu-server-197:~/ye/exp/faster-kan/data/MNIST$ wc ./raw/*
   58093   230240 21607840 ./raw/t10k-images-idx3-ubyte
       0        1    27569 ./raw/t10k-labels-idx1-ubyte
  121880   484576 47040016 ./raw/train-images-idx3-ubyte
       0        1    60008 ./raw/train-labels-idx1-ubyte
  179973   714818 68735433 total
(py3.8) ye@lst-gpu-server-197:~/ye/exp/faster-kan/data/MNIST$
```

Python code ကို ဝင်ဖတ်ကြည့်တော့ model ကို တစ်ခုထက်မက define လုပ်ထားတာတွေ့လို့ သေချာအောင် model_0 = Faster-KAN ကိုပဲ run အောင် ပြင်ဆင်ခဲ့...  

မပြင်ခင်က အောက်ပါအတိုင်း ...  

```
#print(summary(model,(1,28,28)))
#print(summary(model_1,(1,28,28)))
#print(summary(model_2,(1,28,28)))
#print(summary(model_3,(1,28,28)))
print(summary(model_4,(1,784)))

model_last = model = model_0
print(summary(model_0,(1,784)))
model_last.to(device)

epochs = 100
```

Updated the script:  

```python
#print(summary(model_0, (1,28,28)))
#print(summary(model_1,(1,28,28)))
#print(summary(model_2,(1,28,28)))
#print(summary(model_3,(1,28,28)))
#print(summary(model_4,(1,784)))

model_last = model = model_0
#print(summary(model_0,(1,28,28)))
print(summary(model_0,(1,784)))
model_last.to(device)

#epochs = 100
epochs = 10
```

training Faster-KAN with BHDD dataset ...  

```
Total parameters: 408242
Trainable parameters: 408242
Total parameters: 254410
Trainable parameters: 254410
Total parameters: 508160
Trainable parameters: 508160
Total parameters: 5128744
Trainable parameters: 5128744
Total parameters: 1427534
Trainable parameters: 1427489
----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
         LayerNorm-1               [-1, 1, 784]           1,568
ReflectionalSwitchFunction-2            [-1, 1, 784, 8]               0
      SplineLinear-3                   [-1, 64]         401,408
    FasterKANLayer-4                   [-1, 64]               0
         LayerNorm-5                   [-1, 64]             128
ReflectionalSwitchFunction-6                [-1, 64, 8]               0
      SplineLinear-7                   [-1, 10]           5,120
    FasterKANLayer-8                   [-1, 10]               0
================================================================
Total params: 408,224
Trainable params: 408,224
Non-trainable params: 0
----------------------------------------------------------------
Input size (MB): 0.00
Forward/backward pass size (MB): 0.06
Params size (MB): 1.56
Estimated Total Size (MB): 1.62
----------------------------------------------------------------
...
...
...
100%|█████████████████████████████████████████████████| 938/938 [00:39<00:00, 23.48it/s, accuracy=0.938, loss=0.326, lr=0.001]
Epoch 2, Val Loss: 0.10560400375184492, Val Accuracy: 0.9762499292322765
Current Learning Rate: 0.001
100%|█████████████████████████████████████████████████| 938/938 [00:39<00:00, 23.60it/s, accuracy=0.0312, loss=2.59, lr=0.001]
Epoch 3, Val Loss: 3.145326301835806, Val Accuracy: 0.0023564385150812066
Current Learning Rate: 0.001
100%|██████████████████████████████████████████████████| 938/938 [00:42<00:00, 22.23it/s, accuracy=0.281, loss=2.31, lr=0.001]
Epoch 4, Val Loss: 2.320426436422043, Val Accuracy: 0.2155049233038298
Current Learning Rate: 0.0006
100%|██████████████████████████████████████████████████| 938/938 [00:47<00:00, 19.92it/s, accuracy=0.188, loss=2.3, lr=0.0006]
Epoch 5, Val Loss: 2.338414534615253, Val Accuracy: 0.07781198714144545
Current Learning Rate: 0.0006
100%|████████████████████████████████████████████████| 938/938 [00:41<00:00, 22.77it/s, accuracy=0.0625, loss=2.36, lr=0.0006]
Epoch 6, Val Loss: 2.2892897400114762, Val Accuracy: 0.08119942278983698
Current Learning Rate: 0.00035999999999999997
100%|███████████████████████████████████████████████| 938/938 [00:40<00:00, 23.24it/s, accuracy=0.0625, loss=2.32, lr=0.00036]
Epoch 7, Val Loss: 2.3695402847918445, Val Accuracy: 0.01812645011600928
Current Learning Rate: 0.00035999999999999997
100%|████████████████████████████████████████████████████| 938/938 [00:45<00:00, 20.50it/s, accuracy=0, loss=2.32, lr=0.00036]
Epoch 8, Val Loss: 2.2986296927016183, Val Accuracy: 0.07848045527243559
Current Learning Rate: 0.00021599999999999996
100%|████████████████████████████████████████████████| 938/938 [00:39<00:00, 23.81it/s, accuracy=0.125, loss=2.3, lr=0.000216]
Epoch 9, Val Loss: 2.2996470441397823, Val Accuracy: 0.12633870465987795
Current Learning Rate: 0.00021599999999999996
100%|███████████████████████████████████████████████| 938/938 [00:39<00:00, 23.60it/s, accuracy=0.0625, loss=2.3, lr=0.000216]
Epoch 10, Val Loss: 2.304354469626796, Val Accuracy: 0.020684490122955528
Current Learning Rate: 0.00012959999999999998

real    8m12.916s
user    37m33.078s
sys     0m10.138s
(py3.8) ye@lst-gpu-server-197:~/ye/exp/faster-kan$ time python ./train_my_mnist.py | tee faster-kan-train-my-mnist.log1
```

From log file ...  

```
Epoch 1, Val Loss: 0.1950947013780855, Val Accuracy: 0.9581597320164993
Current Learning Rate: 0.001
Epoch 2, Val Loss: 0.10560400375184492, Val Accuracy: 0.9762499292322765
Current Learning Rate: 0.001
Epoch 3, Val Loss: 3.145326301835806, Val Accuracy: 0.0023564385150812066
Current Learning Rate: 0.001
Epoch 4, Val Loss: 2.320426436422043, Val Accuracy: 0.2155049233038298
Current Learning Rate: 0.0006
Epoch 5, Val Loss: 2.338414534615253, Val Accuracy: 0.07781198714144545
Current Learning Rate: 0.0006
Epoch 6, Val Loss: 2.2892897400114762, Val Accuracy: 0.08119942278983698
Current Learning Rate: 0.00035999999999999997
Epoch 7, Val Loss: 2.3695402847918445, Val Accuracy: 0.01812645011600928
Current Learning Rate: 0.00035999999999999997
Epoch 8, Val Loss: 2.2986296927016183, Val Accuracy: 0.07848045527243559
Current Learning Rate: 0.00021599999999999996
Epoch 9, Val Loss: 2.2996470441397823, Val Accuracy: 0.12633870465987795
Current Learning Rate: 0.00021599999999999996
Epoch 10, Val Loss: 2.304354469626796, Val Accuracy: 0.020684490122955528
Current Learning Rate: 0.00012959999999999998
```

တဖြည်းဖြည်းနဲ့ Validation Accuracy က နည်းသွားတာကို မြင်ရတယ်။  


code updating ...  

```python
# Define optimizer and scheduler
#optimizer = optim.AdamW(model.parameters(), lr=1e-3, weight_decay=1e-5)
optimizer = optim.AdamW(model.parameters(), lr=1e-3, weight_decay=1e-4)

#scheduler = optim.lr_scheduler.ReduceLROnPlateau(optimizer, mode='min', factor=0.6, patience=1, verbose=True)
scheduler = optim.lr_scheduler.ExponentialLR(optimizer, gamma=0.8)
```

train again:  

```
Epoch 2, Val Loss: 2.368625472703832, Val Accuracy: 0.01109338747099768
Current Learning Rate: 0.0005894628976204361
100%|███████████████████████████████████████████████████| 938/938 [00:39<00:00, 23.87it/s, accuracy=0, loss=2.37, lr=0.000589]
Epoch 3, Val Loss: 2.2994718833755177, Val Accuracy: 0.1275624610881241
Current Learning Rate: 0.0005986295484393364
100%|██████████████████████████████████████████████| 938/938 [00:38<00:00, 24.18it/s, accuracy=0.0625, loss=2.32, lr=0.000599]
Epoch 4, Val Loss: 2.314823500241592, Val Accuracy: 0.12786132646962275
Current Learning Rate: 0.0005965823828959761
100%|███████████████████████████████████████████████| 938/938 [00:39<00:00, 23.59it/s, accuracy=0.0938, loss=2.3, lr=0.000597]
Epoch 5, Val Loss: 2.3104697485257746, Val Accuracy: 0.12630245175964594
Current Learning Rate: 0.0005971622512417029
100%|██████████████████████████████████████████████| 938/938 [00:42<00:00, 21.88it/s, accuracy=0.0938, loss=2.35, lr=0.000597]
Epoch 6, Val Loss: 2.362928440288712, Val Accuracy: 0.022114269141531324
Current Learning Rate: 0.0005902127324073953
100%|███████████████████████████████████████████████| 938/938 [00:39<00:00, 23.52it/s, accuracy=0.0625, loss=2.32, lr=0.00059]
Epoch 7, Val Loss: 2.3046746016101882, Val Accuracy: 0.15742335605095822
Current Learning Rate: 0.0005979349709191455
100%|███████████████████████████████████████████████| 938/938 [00:39<00:00, 23.63it/s, accuracy=0.219, loss=2.29, lr=0.000598]
Epoch 8, Val Loss: 2.35131315344171, Val Accuracy: 0.12630245175964594
Current Learning Rate: 0.0005917444750201037
100%|██████████████████████████████████████████████| 938/938 [00:39<00:00, 23.78it/s, accuracy=0.0625, loss=2.33, lr=0.000592]
Epoch 9, Val Loss: 2.312111715706208, Val Accuracy: 0.01812645011600928
Current Learning Rate: 0.0005969434944223346
100%|███████████████████████████████████████████████| 938/938 [00:39<00:00, 23.98it/s, accuracy=0.125, loss=2.31, lr=0.000597]
Epoch 10, Val Loss: 2.3323640353165205, Val Accuracy: 0.01410237819025522
Current Learning Rate: 0.0005942518890903347

real    7m52.289s
user    36m41.922s
sys     0m11.990s
(py3.8) ye@lst-gpu-server-197:~/ye/exp/faster-kan$ time python ./train_my_mnist.py | tee faster-kan-train-my-mnist.log2
```

code ပြောင်းလိုက်တာ ပိုတောင် အဆင်မပြေ ဖြစ်သွားတယ်။  

```
Epoch 1, Val Loss: 0.15311720569697998, Val Accuracy: 0.9645764953575665
Current Learning Rate: 0.0009664099875588936
Epoch 2, Val Loss: 2.368625472703832, Val Accuracy: 0.01109338747099768
Current Learning Rate: 0.0005894628976204361
Epoch 3, Val Loss: 2.2994718833755177, Val Accuracy: 0.1275624610881241
Current Learning Rate: 0.0005986295484393364
Epoch 4, Val Loss: 2.314823500241592, Val Accuracy: 0.12786132646962275
Current Learning Rate: 0.0005965823828959761
Epoch 5, Val Loss: 2.3104697485257746, Val Accuracy: 0.12630245175964594
Current Learning Rate: 0.0005971622512417029
Epoch 6, Val Loss: 2.362928440288712, Val Accuracy: 0.022114269141531324
Current Learning Rate: 0.0005902127324073953
Epoch 7, Val Loss: 2.3046746016101882, Val Accuracy: 0.15742335605095822
Current Learning Rate: 0.0005979349709191455
Epoch 8, Val Loss: 2.35131315344171, Val Accuracy: 0.12630245175964594
Current Learning Rate: 0.0005917444750201037
Epoch 9, Val Loss: 2.312111715706208, Val Accuracy: 0.01812645011600928
Current Learning Rate: 0.0005969434944223346
Epoch 10, Val Loss: 2.3323640353165205, Val Accuracy: 0.01410237819025522
Current Learning Rate: 0.0005942518890903347
(py3.8) ye@lst-gpu-server-197:~/ye/exp/faster-kan$
```

## Bench Mark Code  

benchmark.py ဆိုတဲ့ code ရှိတာနဲ့ အဲဒါနဲ့ run ကြည့်တော့ အောက်ပါအတိုင်း error ပေး...  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/faster-kan$ time python ./benchmark.py --method all | tee benchmark.log
...
...
...
/home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages/numpy/core/fromnumeric.py:3464: RuntimeWarning: Mean of empty slice.
  return _methods._mean(a, axis=axis, dtype=dtype,
/home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages/numpy/core/_methods.py:192: RuntimeWarning: invalid value encountered in scalar divide
  ret = ret.dtype.type(ret / rcount)
Traceback (most recent call last):
  File "./benchmark.py", line 303, in <module>
    main()
  File "./benchmark.py", line 243, in main
    model.to('cuda')
  File "/home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1174, in to
    return self._apply(convert)
  File "/home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages/torch/nn/modules/module.py", line 780, in _apply
    module._apply(fn)
  File "/home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages/torch/nn/modules/module.py", line 780, in _apply
    module._apply(fn)
  File "/home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages/torch/nn/modules/module.py", line 780, in _apply
    module._apply(fn)
  File "/home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages/torch/nn/modules/module.py", line 805, in _apply
    param_applied = fn(param)
  File "/home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1160, in convert
    return t.to(
  File "/home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages/torch/cuda/__init__.py", line 314, in _lazy_init
    torch._C._cuda_init()
RuntimeError: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver.

real    0m8.068s
user    1m25.300s
sys     0m14.014s
```


```

```

## Model Archi Visualization

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/efficient-kan/examples$ python -m pip install torchviz
...
...
...
Requirement already satisfied: nvidia-cusolver-cu12==11.4.5.107 in /home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages (from torch->torchviz) (11.4.5.107)
Requirement already satisfied: nvidia-cusparse-cu12==12.1.0.106 in /home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages (from torch->torchviz) (12.1.0.106)
Requirement already satisfied: nvidia-nccl-cu12==2.20.5 in /home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages (from torch->torchviz) (2.20.5)
Requirement already satisfied: nvidia-nvtx-cu12==12.1.105 in /home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages (from torch->torchviz) (12.1.105)
Requirement already satisfied: triton==3.0.0 in /home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages (from torch->torchviz) (3.0.0)
Requirement already satisfied: nvidia-nvjitlink-cu12 in /home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages (from nvidia-cusolver-cu12==11.4.5.107->torch->torchviz) (12.4.99)
Requirement already satisfied: MarkupSafe>=2.0 in /home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages (from jinja2->torch->torchviz) (2.1.5)
Requirement already satisfied: mpmath>=0.19 in /home/ye/anaconda3/envs/py3.8/lib/python3.8/site-packages (from sympy->torch->torchviz) (1.3.0)
Building wheels for collected packages: torchviz
  Building wheel for torchviz (setup.py) ... done
  Created wheel for torchviz: filename=torchviz-0.0.2-py3-none-any.whl size=4130 sha256=8a18fedae36b903e36c599374acd54ca8e70bae0f9fcb035f8c288c03e6c5834
  Stored in directory: /home/ye/.cache/pip/wheels/05/7d/1b/8306781244e42ede119edbb053bdcda1c1f424ca226165a417
Successfully built torchviz
Installing collected packages: torchviz
Successfully installed torchviz-0.0.2
```

```python
from torchviz import make_dot  # Import torchviz's make_dot function

# Visualize model architecture
dummy_input = torch.randn(1, 28 * 28).to(device)  # Example input for visualization
output = model(dummy_input)  # Forward pass to create the graph
dot = make_dot(output, params=dict(model.named_parameters()))
#dot.format = 'png'  # Save as PNG; change to 'jpg' if needed
dot.format = 'svg'
dot.render("fastKAN_model_architecture")  # Saves as 'KAN_model_architecture.png'
```

အထက်ပါအတိုင်း ပြင်လိုက်ရင်တော့ network architecture graph ကို ထုတ်ပေးနိုင်တယ်။  
pykan နဲ့ ဆိုရင်တော့ model.plot() ဆိုတဲ့ attribute ပါလို့ ပိုအဆင်ပြေတယ်။  

## KAN Experiment with GPU

လက်ရှိအချိန်ထိ library ပြဿနာကြောင့် KAN experiment တွေကို CPU ပေါ်မှာပဲ စမ်းဖြစ်ခဲ့တယ်။ GPU မှာ စမ်းဖို့ ကြိုးစားကြည့်မယ်။  

### Efficient KAN  

Efficient KAN က Lab ခန်းထဲက စက်မှာ ငါစမ်းဖူးတယ်။  

```
(opennmt) ye@lst-hpc3090:~/exp/efficient-kan/src/data/MNIST$ mv raw en_raw
(opennmt) ye@lst-hpc3090:~/exp/efficient-kan/src/data/MNIST$
```

အရင် ဆာဗာက ဒေတာကို zip လုပ်...  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/efficient-kan/examples/data/MNIST$ zip -r raw.zip ./raw
  adding: raw/ (stored 0%)
  adding: raw/t10k-images-idx3-ubyte (deflated 54%)
  adding: raw/train-labels-idx1-ubyte (deflated 51%)
  adding: raw/t10k-labels-idx1-ubyte (deflated 56%)
  adding: raw/train-images-idx3-ubyte (deflated 55%)
(py3.8) ye@lst-gpu-server-197:~/ye/exp/efficient-kan/examples/data/MNIST$
```

local စက်ပေါ်ကို ကော်ပီကူး...  

```
C:\Users\801680>scp  ye@10.99.5.197:/home/ye/ye/exp/efficient-kan/examples/data/MNIST/raw.zip .\Downloads
ye@10.99.5.197's password:
raw.zip                                                                                     100%   30MB   3.9MB/s   00:07

C:\Users\801680>
```

local machine ကနေ Lab ခန်းထဲက ဆာဗာပေါ်ကို ကော်ပီကူး...  

```
C:\Users\801680>scp .\Downloads\raw.zip ye@10.222.47.165:/home/ye/exp/efficient-kan/src/data/MNIST/
ye@10.222.47.165's password:
raw.zip                                                                                     100%   30MB  11.4MB/s   00:02

```

ဆာဗာပေါ်မှာ zip ဖိုင်ကို ဖြေ...  

```
(opennmt) ye@lst-hpc3090:~/exp/efficient-kan/src/data/MNIST$ unzip ./raw.zip
Archive:  ./raw.zip
   creating: raw/
  inflating: raw/t10k-images-idx3-ubyte
  inflating: raw/train-labels-idx1-ubyte
  inflating: raw/t10k-labels-idx1-ubyte
  inflating: raw/train-images-idx3-ubyte
(opennmt) ye@lst-hpc3090:~/exp/efficient-kan/src/data/MNIST$ ls
en_raw  raw  raw.zip
(opennmt) ye@lst-hpc3090:~/exp/efficient-kan/src/data/MNIST$
```

### Efficient KAN With BHDD on GPU


```
(opennmt) ye@lst-hpc3090:~/exp/efficient-kan/src$ time /home/ye/miniforge3/envs/opennmt/bin/python ./mnist.py | tee mnist-BHDD-train-test.log
Traceback (most recent call last):
  File "./mnist.py", line 7, in <module>
    import torchvision
ModuleNotFoundError: No module named 'torchvision'

real    0m3.678s
user    0m2.180s
sys     0m2.420s
```

Installation of torchvision ...  

```
(opennmt) ye@lst-hpc3090:~/exp/efficient-kan/src$ /home/ye/miniforge3/envs/opennmt/bin/python -m pip install torchvision
...
...
...
>torch==2.4.1->torchvision) (1.3.0)
Downloading torchvision-0.19.1-cp38-cp38-manylinux1_x86_64.whl (7.0 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 7.0/7.0 MB 80.2 MB/s eta 0:00:00
Downloading torch-2.4.1-cp38-cp38-manylinux1_x86_64.whl (797.1 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 797.1/797.1 MB 23.9 MB/s eta 0:00:00
Using cached nvidia_cudnn_cu12-9.1.0.70-py3-none-manylinux2014_x86_64.whl (664.8 MB)
Using cached nvidia_nccl_cu12-2.20.5-py3-none-manylinux2014_x86_64.whl (176.2 MB)
Downloading triton-3.0.0-1-cp38-cp38-manylinux2014_x86_64.manylinux_2_17_x86_64.whl (209.4 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 209.4/209.4 MB 99.6 MB/s eta 0:00:00
Installing collected packages: triton, nvidia-nccl-cu12, nvidia-cudnn-cu12, torch, torchvision
  Attempting uninstall: triton
    Found existing installation: triton 2.2.0
    Uninstalling triton-2.2.0:
      Successfully uninstalled triton-2.2.0
  Attempting uninstall: nvidia-nccl-cu12
    Found existing installation: nvidia-nccl-cu12 2.19.3
    Uninstalling nvidia-nccl-cu12-2.19.3:
      Successfully uninstalled nvidia-nccl-cu12-2.19.3
  Attempting uninstall: nvidia-cudnn-cu12
    Found existing installation: nvidia-cudnn-cu12 8.9.2.26
    Uninstalling nvidia-cudnn-cu12-8.9.2.26:
      Successfully uninstalled nvidia-cudnn-cu12-8.9.2.26
  Attempting uninstall: torch
    Found existing installation: torch 2.2.2
    Uninstalling torch-2.2.2:
      Successfully uninstalled torch-2.2.2
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
opennmt-py 3.5.0 requires torch<2.3,>=2.0.1, but you have torch 2.4.1 which is incompatible.
Successfully installed nvidia-cudnn-cu12-9.1.0.70 nvidia-nccl-cu12-2.20.5 torch-2.4.1 torchvision-0.19.1 triton-3.0.0
```

BHDD နဲ့ training result က အောက်ပါအတိုင်း...  

```
(opennmt) ye@lst-hpc3090:~/exp/efficient-kan/src$ time /home/ye/miniforge3/envs/opennmt/bin/python ./mnist.py | tee mnist-BHDD-train-test.log
100%|████████████████████████████████████████████████| 938/938 [00:04<00:00, 216.05it/s, accuracy=0.969, loss=0.107, lr=0.001]
Epoch 1, Val Loss: 0.08495114284746885, Val Accuracy: 0.9813819251038359
100%|██████████████████████████████████████████████████| 938/938 [00:03<00:00, 248.84it/s, accuracy=1, loss=0.0278, lr=0.0008]
Epoch 2, Val Loss: 0.0548279026897058, Val Accuracy: 0.9868923659391027
100%|█████████████████████████████████████████████| 938/938 [00:03<00:00, 249.72it/s, accuracy=0.969, loss=0.0303, lr=0.00064]
Epoch 3, Val Loss: 0.04538187946045983, Val Accuracy: 0.9893053942932607
100%|████████████████████████████████████████████████| 938/938 [00:03<00:00, 249.03it/s, accuracy=1, loss=0.0112, lr=0.000512]
Epoch 4, Val Loss: 0.050390004171188184, Val Accuracy: 0.9869489557781794
100%|█████████████████████████████████████████████████| 938/938 [00:03<00:00, 248.19it/s, accuracy=1, loss=0.0119, lr=0.00041]
Epoch 5, Val Loss: 0.042926808358105265, Val Accuracy: 0.9895229116946528
100%|███████████████████████████████████████████████| 938/938 [00:03<00:00, 240.91it/s, accuracy=1, loss=0.00499, lr=0.000328]
Epoch 6, Val Loss: 0.04221727922067193, Val Accuracy: 0.9903160545222998
100%|████████████████████████████████████████████████| 938/938 [00:03<00:00, 249.35it/s, accuracy=1, loss=0.0335, lr=0.000262]
Epoch 7, Val Loss: 0.038987839509400254, Val Accuracy: 0.9906830045020774
100%|████████████████████████████████████████████████| 938/938 [00:04<00:00, 208.53it/s, accuracy=1, loss=0.00725, lr=0.00021]
Epoch 8, Val Loss: 0.035385586051788966, Val Accuracy: 0.9916618328083419
100%|███████████████████████████████████████████████| 938/938 [00:03<00:00, 247.58it/s, accuracy=1, loss=0.00151, lr=0.000168]
Epoch 9, Val Loss: 0.03845145885647316, Val Accuracy: 0.9904088972616085
100%|███████████████████████████████████████████████| 938/938 [00:03<00:00, 243.47it/s, accuracy=1, loss=0.00137, lr=0.000134]
Epoch 10, Val Loss: 0.036535589627569365, Val Accuracy: 0.9911339552662489

real    0m55.070s
user    0m57.522s
sys     0m2.793s
(opennmt) ye@lst-hpc3090:~/exp/efficient-kan/src$
```

During Training Time, GPU Usage is as follows:  

```
(base) ye@lst-hpc3090:~$ nvidia-smi
Sat Nov  9 14:12:54 2024
+---------------------------------------------------------------------------------------+
| NVIDIA-SMI 535.171.04             Driver Version: 535.171.04   CUDA Version: 12.2     |
|-----------------------------------------+----------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |         Memory-Usage | GPU-Util  Compute M. |
|                                         |                      |               MIG M. |
|=========================================+======================+======================|
|   0  NVIDIA GeForce RTX 3090 Ti     Off | 00000000:01:00.0 Off |                  Off |
|  0%   54C    P2             130W / 480W |    575MiB / 24564MiB |     15%      Default |
|                                         |                      |                  N/A |
+-----------------------------------------+----------------------+----------------------+

+---------------------------------------------------------------------------------------+
| Processes:                                                                            |
|  GPU   GI   CI        PID   Type   Process name                            GPU Memory |
|        ID   ID                                                             Usage      |
|=======================================================================================|
|    0   N/A  N/A     38513      G   /usr/lib/xorg/Xorg                           16MiB |
|    0   N/A  N/A    114721      G   /usr/lib/xorg/Xorg                           33MiB |
|    0   N/A  N/A    114934      G   /usr/bin/gnome-shell                         15MiB |
|    0   N/A  N/A    239190      C   .../miniforge3/envs/opennmt/bin/python      370MiB |
+---------------------------------------------------------------------------------------+
(base) ye@lst-hpc3090:~$
```

## Confirmation with English MNIST Dataset

English MNIST data အဖြစ် ပြန်ပြောင်းထားခဲ့...  

```
(opennmt) ye@lst-hpc3090:~/exp/efficient-kan/src/data/MNIST$ mv raw my_raw
(opennmt) ye@lst-hpc3090:~/exp/efficient-kan/src/data/MNIST$ mv en_raw raw
(opennmt) ye@lst-hpc3090:~/exp/efficient-kan/src/data/MNIST$ ls
my_raw  raw  raw.zip
(opennmt) ye@lst-hpc3090:~/exp/efficient-kan/src/data/MNIST$
```

Training Efficient-KAN with English MNIST Dataset ...  

```
(opennmt) ye@lst-hpc3090:~/exp/efficient-kan/src$ time /home/ye/miniforge3/envs/opennmt/bin/python ./mnist.py | tee mnist-English-train-test.log
100%|████████████████████████████████████████████████| 938/938 [00:04<00:00, 212.91it/s, accuracy=0.938, loss=0.134, lr=0.001]
Epoch 1, Val Loss: 0.23149173268989012, Val Accuracy: 0.9305334394904459
100%|██████████████████████████████████████████████████| 938/938 [00:04<00:00, 230.07it/s, accuracy=1, loss=0.0425, lr=0.0008]
Epoch 2, Val Loss: 0.15703222488652274, Val Accuracy: 0.9559116242038217
100%|█████████████████████████████████████████████| 938/938 [00:03<00:00, 249.18it/s, accuracy=0.969, loss=0.0809, lr=0.00064]
Epoch 3, Val Loss: 0.13109625447511816, Val Accuracy: 0.9628781847133758
100%|████████████████████████████████████████████████| 938/938 [00:03<00:00, 251.65it/s, accuracy=1, loss=0.0831, lr=0.000512]
Epoch 4, Val Loss: 0.1170542825778626, Val Accuracy: 0.9664609872611465
100%|█████████████████████████████████████████████████| 938/938 [00:03<00:00, 253.70it/s, accuracy=1, loss=0.0177, lr=0.00041]
Epoch 5, Val Loss: 0.1070147171834555, Val Accuracy: 0.9684514331210191
100%|████████████████████████████████████████████| 938/938 [00:03<00:00, 239.73it/s, accuracy=0.969, loss=0.0989, lr=0.000328]
Epoch 6, Val Loss: 0.10197272744685246, Val Accuracy: 0.9695461783439491
100%|█████████████████████████████████████████████████| 938/938 [00:05<00:00, 178.52it/s, accuracy=1, loss=0.064, lr=0.000262]
Epoch 7, Val Loss: 0.09723629575640937, Val Accuracy: 0.9701433121019108
100%|█████████████████████████████████████████████████| 938/938 [00:06<00:00, 151.43it/s, accuracy=1, loss=0.0153, lr=0.00021]
Epoch 8, Val Loss: 0.09497544086489317, Val Accuracy: 0.9722332802547771
100%|████████████████████████████████████████████████| 938/938 [00:04<00:00, 200.47it/s, accuracy=1, loss=0.0387, lr=0.000168]
Epoch 9, Val Loss: 0.0926320428513643, Val Accuracy: 0.9726313694267515
100%|████████████████████████████████████████████████| 938/938 [00:04<00:00, 230.20it/s, accuracy=1, loss=0.0073, lr=0.000134]
Epoch 10, Val Loss: 0.09276304267136273, Val Accuracy: 0.9718351910828026

real    0m50.358s
user    0m53.022s
sys     0m2.639s
(opennmt) ye@lst-hpc3090:~/exp/efficient-kan/src$
```

During training with English Dataset, GPU usage log:  

```
(base) ye@lst-hpc3090:~$ nvidia-smi
Sat Nov  9 14:16:26 2024
+---------------------------------------------------------------------------------------+
| NVIDIA-SMI 535.171.04             Driver Version: 535.171.04   CUDA Version: 12.2     |
|-----------------------------------------+----------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |         Memory-Usage | GPU-Util  Compute M. |
|                                         |                      |               MIG M. |
|=========================================+======================+======================|
|   0  NVIDIA GeForce RTX 3090 Ti     Off | 00000000:01:00.0 Off |                  Off |
|  0%   53C    P2             128W / 480W |    575MiB / 24564MiB |     16%      Default |
|                                         |                      |                  N/A |
+-----------------------------------------+----------------------+----------------------+

+---------------------------------------------------------------------------------------+
| Processes:                                                                            |
|  GPU   GI   CI        PID   Type   Process name                            GPU Memory |
|        ID   ID                                                             Usage      |
|=======================================================================================|
|    0   N/A  N/A     38513      G   /usr/lib/xorg/Xorg                           16MiB |
|    0   N/A  N/A    114721      G   /usr/lib/xorg/Xorg                           33MiB |
|    0   N/A  N/A    114934      G   /usr/bin/gnome-shell                         15MiB |
|    0   N/A  N/A    239375      C   .../miniforge3/envs/opennmt/bin/python      370MiB |
+---------------------------------------------------------------------------------------+
(base) ye@lst-hpc3090:~$
```

Log file ...  

```
(opennmt) ye@lst-hpc3090:~/exp/efficient-kan/src$ cat ./mnist-BHDD-train-test.log
Epoch 1, Val Loss: 0.08495114284746885, Val Accuracy: 0.9813819251038359
Epoch 2, Val Loss: 0.0548279026897058, Val Accuracy: 0.9868923659391027
Epoch 3, Val Loss: 0.04538187946045983, Val Accuracy: 0.9893053942932607
Epoch 4, Val Loss: 0.050390004171188184, Val Accuracy: 0.9869489557781794
Epoch 5, Val Loss: 0.042926808358105265, Val Accuracy: 0.9895229116946528
Epoch 6, Val Loss: 0.04221727922067193, Val Accuracy: 0.9903160545222998
Epoch 7, Val Loss: 0.038987839509400254, Val Accuracy: 0.9906830045020774
Epoch 8, Val Loss: 0.035385586051788966, Val Accuracy: 0.9916618328083419
Epoch 9, Val Loss: 0.03845145885647316, Val Accuracy: 0.9904088972616085
Epoch 10, Val Loss: 0.036535589627569365, Val Accuracy: 0.9911339552662489
(opennmt) ye@lst-hpc3090:~/exp/efficient-kan/src$
```

### Fast-KAN with BHDD on GPU  

```
(opennmt) ye@lst-hpc3090:~/exp$ git clone https://github.com/ZiyaoLi/fast-kan
Cloning into 'fast-kan'...
remote: Enumerating objects: 202, done.
remote: Counting objects: 100% (78/78), done.
remote: Compressing objects: 100% (32/32), done.
remote: Total 202 (delta 52), reused 62 (delta 44), pack-reused 124 (from 1)
Receiving objects: 100% (202/202), 420.57 KiB | 3.66 MiB/s, done.
Resolving deltas: 100% (91/91), done.
(opennmt) ye@lst-hpc3090:~/exp$
```

```
(opennmt) ye@lst-hpc3090:~/exp/fast-kan$ ls
efficient_kan  examples  fastkan  img  LICENSE  notebooks  README.md  setup.py  tests
(opennmt) ye@lst-hpc3090:~/exp/fast-kan$
```

copy ကူးဖို့ လိုအပ်...   

```
(opennmt) ye@lst-hpc3090:~/exp/fast-kan$ cp ./examples/train_mnist.py .
(opennmt) ye@lst-hpc3090:~/exp/fast-kan$
```

Training with English MNIST Dataset... 

```
(opennmt) ye@lst-hpc3090:~/exp/fast-kan$ time /home/ye/miniforge3/envs/opennmt/bin/python ./train_mnist.py | tee train_English_mnist.log
...
...
...
Epoch 10, Val Loss: 0.08998527625912302, Val Accuracy: 0.9727308917197452
100%|███████████████████████████████████████████████| 938/938 [00:03<00:00, 237.15it/s, accuracy=1, loss=0.00116, lr=0.000107]
Epoch 11, Val Loss: 0.08984881206760391, Val Accuracy: 0.9734275477707006
100%|████████████████████████████████████████████████| 938/938 [00:03<00:00, 279.89it/s, accuracy=1, loss=0.00584, lr=8.59e-5]
Epoch 12, Val Loss: 0.0890594897438141, Val Accuracy: 0.9742237261146497
100%|████████████████████████████████████████████████| 938/938 [00:03<00:00, 276.04it/s, accuracy=1, loss=0.00128, lr=6.87e-5]
Epoch 13, Val Loss: 0.08954361526421227, Val Accuracy: 0.9735270700636943
100%|█████████████████████████████████████████████████| 938/938 [00:03<00:00, 287.19it/s, accuracy=1, loss=0.00817, lr=5.5e-5]
Epoch 14, Val Loss: 0.090049656978217, Val Accuracy: 0.9736265923566879
100%|█████████████████████████████████████████████████| 938/938 [00:03<00:00, 287.39it/s, accuracy=1, loss=0.00221, lr=4.4e-5]
  0%|                                                                                                 | 0/938 [00:00<?, ?it/s]Epoch 15, Val Loss: 0.08959306947402003, Val Accuracy: 0.9740246815286624
100%|████████████████████████████████████████████████| 938/938 [00:03<00:00, 286.46it/s, accuracy=1, loss=0.00492, lr=3.52e-5]
Epoch 16, Val Loss: 0.09025520194551921, Val Accuracy: 0.9734275477707006
100%|████████████████████████████████████████████████| 938/938 [00:03<00:00, 284.76it/s, accuracy=1, loss=0.00316, lr=2.81e-5]
Epoch 17, Val Loss: 0.09018310692221013, Val Accuracy: 0.9740246815286624
100%|█████████████████████████████████████████████████| 938/938 [00:03<00:00, 286.56it/s, accuracy=1, loss=0.0059, lr=2.25e-5]
Epoch 18, Val Loss: 0.09139047024921632, Val Accuracy: 0.9730294585987261
100%|█████████████████████████████████████████████████| 938/938 [00:03<00:00, 283.11it/s, accuracy=1, loss=0.00477, lr=1.8e-5]
Epoch 19, Val Loss: 0.09105467818705046, Val Accuracy: 0.9732285031847133
100%|████████████████████████████████████████████████| 938/938 [00:03<00:00, 263.60it/s, accuracy=1, loss=0.00525, lr=1.44e-5]
Epoch 20, Val Loss: 0.09166254324212972, Val Accuracy: 0.9735270700636943

real    1m50.408s
user    1m24.361s
sys     0m2.857s
```

GPU Usage with English MNIST ...  

```
(base) ye@lst-hpc3090:~$ nvidia-smi
Sat Nov  9 14:24:20 2024
+---------------------------------------------------------------------------------------+
| NVIDIA-SMI 535.171.04             Driver Version: 535.171.04   CUDA Version: 12.2     |
|-----------------------------------------+----------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |         Memory-Usage | GPU-Util  Compute M. |
|                                         |                      |               MIG M. |
|=========================================+======================+======================|
|   0  NVIDIA GeForce RTX 3090 Ti     Off | 00000000:01:00.0 Off |                  Off |
|  0%   53C    P2             124W / 480W |    572MiB / 24564MiB |     10%      Default |
|                                         |                      |                  N/A |
+-----------------------------------------+----------------------+----------------------+

+---------------------------------------------------------------------------------------+
| Processes:                                                                            |
|  GPU   GI   CI        PID   Type   Process name                            GPU Memory |
|        ID   ID                                                             Usage      |
|=======================================================================================|
|    0   N/A  N/A     38513      G   /usr/lib/xorg/Xorg                           16MiB |
|    0   N/A  N/A    114721      G   /usr/lib/xorg/Xorg                           33MiB |
|    0   N/A  N/A    114934      G   /usr/bin/gnome-shell                         13MiB |
|    0   N/A  N/A    239549      C   .../miniforge3/envs/opennmt/bin/python      368MiB |
+---------------------------------------------------------------------------------------+
(base) ye@lst-hpc3090:~$
```

The whole log file is as follows:  

```
Downloading http://yann.lecun.com/exdb/mnist/train-images-idx3-ubyte.gz
Failed to download (trying next):
<urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: certificate has expired (_ssl.c:1135)>

Downloading https://ossci-datasets.s3.amazonaws.com/mnist/train-images-idx3-ubyte.gz
Downloading https://ossci-datasets.s3.amazonaws.com/mnist/train-images-idx3-ubyte.gz to ./data/MNIST/raw/train-images-idx3-ubyte.gz
Extracting ./data/MNIST/raw/train-images-idx3-ubyte.gz to ./data/MNIST/raw

Downloading http://yann.lecun.com/exdb/mnist/train-labels-idx1-ubyte.gz
Failed to download (trying next):
<urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: certificate has expired (_ssl.c:1135)>

Downloading https://ossci-datasets.s3.amazonaws.com/mnist/train-labels-idx1-ubyte.gz
Downloading https://ossci-datasets.s3.amazonaws.com/mnist/train-labels-idx1-ubyte.gz to ./data/MNIST/raw/train-labels-idx1-ubyte.gz
Extracting ./data/MNIST/raw/train-labels-idx1-ubyte.gz to ./data/MNIST/raw

Downloading http://yann.lecun.com/exdb/mnist/t10k-images-idx3-ubyte.gz
Failed to download (trying next):
<urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: certificate has expired (_ssl.c:1135)>

Downloading https://ossci-datasets.s3.amazonaws.com/mnist/t10k-images-idx3-ubyte.gz
Downloading https://ossci-datasets.s3.amazonaws.com/mnist/t10k-images-idx3-ubyte.gz to ./data/MNIST/raw/t10k-images-idx3-ubyte.gz
Extracting ./data/MNIST/raw/t10k-images-idx3-ubyte.gz to ./data/MNIST/raw

Downloading http://yann.lecun.com/exdb/mnist/t10k-labels-idx1-ubyte.gz
Failed to download (trying next):
<urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: certificate has expired (_ssl.c:1135)>

Downloading https://ossci-datasets.s3.amazonaws.com/mnist/t10k-labels-idx1-ubyte.gz
Downloading https://ossci-datasets.s3.amazonaws.com/mnist/t10k-labels-idx1-ubyte.gz to ./data/MNIST/raw/t10k-labels-idx1-ubyte.gz
Extracting ./data/MNIST/raw/t10k-labels-idx1-ubyte.gz to ./data/MNIST/raw

Epoch 1, Val Loss: 0.18595961844667222, Val Accuracy: 0.9438694267515924
Epoch 2, Val Loss: 0.14020418560586181, Val Accuracy: 0.9586982484076433
Epoch 3, Val Loss: 0.1224803649390318, Val Accuracy: 0.9620820063694268
Epoch 4, Val Loss: 0.10825259722865656, Val Accuracy: 0.9656648089171974
Epoch 5, Val Loss: 0.11732093348359884, Val Accuracy: 0.9655652866242038
Epoch 6, Val Loss: 0.09823838575275252, Val Accuracy: 0.9713375796178344
Epoch 7, Val Loss: 0.09461021216850947, Val Accuracy: 0.9729299363057324
Epoch 8, Val Loss: 0.0938278902292394, Val Accuracy: 0.9720342356687898
Epoch 9, Val Loss: 0.0887563416775491, Val Accuracy: 0.9728304140127388
Epoch 10, Val Loss: 0.08998527625912302, Val Accuracy: 0.9727308917197452
Epoch 11, Val Loss: 0.08984881206760391, Val Accuracy: 0.9734275477707006
Epoch 12, Val Loss: 0.0890594897438141, Val Accuracy: 0.9742237261146497
Epoch 13, Val Loss: 0.08954361526421227, Val Accuracy: 0.9735270700636943
Epoch 14, Val Loss: 0.090049656978217, Val Accuracy: 0.9736265923566879
Epoch 15, Val Loss: 0.08959306947402003, Val Accuracy: 0.9740246815286624
Epoch 16, Val Loss: 0.09025520194551921, Val Accuracy: 0.9734275477707006
Epoch 17, Val Loss: 0.09018310692221013, Val Accuracy: 0.9740246815286624
Epoch 18, Val Loss: 0.09139047024921632, Val Accuracy: 0.9730294585987261
Epoch 19, Val Loss: 0.09105467818705046, Val Accuracy: 0.9732285031847133
Epoch 20, Val Loss: 0.09166254324212972, Val Accuracy: 0.9735270700636943
```

### Fast-KAN with BHDD on GPU  

အရင်ဆုံး ဒေတာပြင်ဆင် ...  

```
(opennmt) ye@lst-hpc3090:~/exp/fast-kan/data/MNIST$ cp ../../../efficient-kan/src/data/MNIST/my_raw . -r
(opennmt) ye@lst-hpc3090:~/exp/fast-kan/data/MNIST$ ls
en_raw  my_raw
(opennmt) ye@lst-hpc3090:~/exp/fast-kan/data/MNIST$
(opennmt) ye@lst-hpc3090:~/exp/fast-kan/data/MNIST$ mv my_raw raw
(opennmt) ye@lst-hpc3090:~/exp/fast-kan/data/MNIST$ ls
en_raw  raw
(opennmt) ye@lst-hpc3090:~/exp/fast-kan/data/MNIST$
```

epoch 10 နဲ့ပဲ သွားချင်တယ်၊ ဒေတာ download လုပ်တာကိုလည်း off လုပ်ပြီး သေချာ စမ်းချင်လို့ code ကိုလည်း ကော်ပီကူးပြီး update လုပ်ခဲ့...  

```
(opennmt) ye@lst-hpc3090:~/exp/fast-kan$ cp train_mnist.py train_my_mnist.py
```

```python
# Load MNIST
transform = transforms.Compose(
    [transforms.ToTensor(), transforms.Normalize((0.5,), (0.5,))]
)
trainset = torchvision.datasets.MNIST(
    root="./data", train=True, download=False, transform=transform
)
valset = torchvision.datasets.MNIST(
    root="./data", train=False, download=False, transform=transform
)
```

```Python
# Define loss
criterion = nn.CrossEntropyLoss()
for epoch in range(10):
```

Training with BHDD, on GPU ...  

```
(opennmt) ye@lst-hpc3090:~/exp/fast-kan$ time /home/ye/miniforge3/envs/opennmt/bin/python ./train_my_mnist.py | tee train_BHDD_mnist.log
100%|████████████████████████████████████████████████| 938/938 [00:04<00:00, 201.94it/s, accuracy=0.938, loss=0.133, lr=0.001]
Epoch 1, Val Loss: 0.0767766577775078, Val Accuracy: 0.9787354633868985
100%|██████████████████████████████████████████████████| 938/938 [00:03<00:00, 244.66it/s, accuracy=1, loss=0.0161, lr=0.0008]
Epoch 2, Val Loss: 0.08314050491704776, Val Accuracy: 0.9735512986537199
100%|█████████████████████████████████████████████| 938/938 [00:04<00:00, 216.83it/s, accuracy=0.969, loss=0.0762, lr=0.00064]
Epoch 3, Val Loss: 0.05083695841680892, Val Accuracy: 0.9868923659391027
100%|███████████████████████████████████████████████| 938/938 [00:03<00:00, 261.19it/s, accuracy=1, loss=0.00535, lr=0.000512]
Epoch 4, Val Loss: 0.04287047465947692, Val Accuracy: 0.9890153710914046
100%|█████████████████████████████████████████████████| 938/938 [00:03<00:00, 260.73it/s, accuracy=1, loss=0.0218, lr=0.00041]
Epoch 5, Val Loss: 0.045805742793442066, Val Accuracy: 0.987544918143279
100%|███████████████████████████████████████████████| 938/938 [00:03<00:00, 281.75it/s, accuracy=1, loss=0.00239, lr=0.000328]
Epoch 6, Val Loss: 0.03711042078902022, Val Accuracy: 0.9916414958694971
100%|██████████████████████████████████████████████| 938/938 [00:03<00:00, 280.08it/s, accuracy=1, loss=0.000702, lr=0.000262]
Epoch 7, Val Loss: 0.04008149352675415, Val Accuracy: 0.9899738624588242
100%|█████████████████████████████████████████████████| 938/938 [00:03<00:00, 281.68it/s, accuracy=1, loss=0.0111, lr=0.00021]
Epoch 8, Val Loss: 0.041992473485818825, Val Accuracy: 0.9896475863567361
100%|██████████████████████████████████████████████| 938/938 [00:03<00:00, 280.12it/s, accuracy=1, loss=0.000203, lr=0.000168]
Epoch 9, Val Loss: 0.03732495593329651, Val Accuracy: 0.991315219767409
100%|██████████████████████████████████████████████| 938/938 [00:03<00:00, 278.61it/s, accuracy=1, loss=0.000329, lr=0.000134]
Epoch 10, Val Loss: 0.03880443601592391, Val Accuracy: 0.9910817864046296

real    0m50.572s
user    0m52.738s
sys     0m2.594s
(opennmt) ye@lst-hpc3090:~/exp/fast-kan$
```

GPU usage က 3% ကနေ 10% လောက်ထိ ရှိတယ်...  

```
(base) ye@lst-hpc3090:~$ nvidia-smi
Sat Nov  9 14:34:17 2024
+---------------------------------------------------------------------------------------+
| NVIDIA-SMI 535.171.04             Driver Version: 535.171.04   CUDA Version: 12.2     |
|-----------------------------------------+----------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |         Memory-Usage | GPU-Util  Compute M. |
|                                         |                      |               MIG M. |
|=========================================+======================+======================|
|   0  NVIDIA GeForce RTX 3090 Ti     Off | 00000000:01:00.0 Off |                  Off |
|  0%   54C    P2             127W / 480W |    572MiB / 24564MiB |     10%      Default |
|                                         |                      |                  N/A |
+-----------------------------------------+----------------------+----------------------+

+---------------------------------------------------------------------------------------+
| Processes:                                                                            |
|  GPU   GI   CI        PID   Type   Process name                            GPU Memory |
|        ID   ID                                                             Usage      |
|=======================================================================================|
|    0   N/A  N/A     38513      G   /usr/lib/xorg/Xorg                           16MiB |
|    0   N/A  N/A    114721      G   /usr/lib/xorg/Xorg                           33MiB |
|    0   N/A  N/A    114934      G   /usr/bin/gnome-shell                         13MiB |
|    0   N/A  N/A    239898      C   .../miniforge3/envs/opennmt/bin/python      368MiB |
+---------------------------------------------------------------------------------------+
(base) ye@lst-hpc3090:~$
```

log ဖိုင်အနေနဲ့လည်း သိမ်းထားတယ်။  

```
(opennmt) ye@lst-hpc3090:~/exp/fast-kan$ cat ./train_BHDD_mnist.log
Epoch 1, Val Loss: 0.0767766577775078, Val Accuracy: 0.9787354633868985
Epoch 2, Val Loss: 0.08314050491704776, Val Accuracy: 0.9735512986537199
Epoch 3, Val Loss: 0.05083695841680892, Val Accuracy: 0.9868923659391027
Epoch 4, Val Loss: 0.04287047465947692, Val Accuracy: 0.9890153710914046
Epoch 5, Val Loss: 0.045805742793442066, Val Accuracy: 0.987544918143279
Epoch 6, Val Loss: 0.03711042078902022, Val Accuracy: 0.9916414958694971
Epoch 7, Val Loss: 0.04008149352675415, Val Accuracy: 0.9899738624588242
Epoch 8, Val Loss: 0.041992473485818825, Val Accuracy: 0.9896475863567361
Epoch 9, Val Loss: 0.03732495593329651, Val Accuracy: 0.991315219767409
Epoch 10, Val Loss: 0.03880443601592391, Val Accuracy: 0.9910817864046296
(opennmt) ye@lst-hpc3090:~/exp/fast-kan$
```

## MLP Training with BHDD on GPU

Training result:  

```
(opennmt) ye@lst-hpc3090:~/exp/fast-kan$ time /home/ye/miniforge3/envs/opennmt/bin/python ./train_mlp_mydigit_mnist.py | tee train_mlp_my_mnist.log
...
...
...
Epoch 8, Val Loss: 0.0507286353477843, Val Accuracy: 0.9878552782839799
100%|██████████████████████████████████████████████| 938/938 [00:06<00:00, 142.27it/s, accuracy=0.938, loss=0.125, lr=0.00043]
Epoch 9, Val Loss: 0.052350924623330075, Val Accuracy: 0.9869127028779474
100%|████████████████████████████████████████████████| 938/938 [00:07<00:00, 130.96it/s, accuracy=1, loss=0.0132, lr=0.000387]
Epoch 10, Val Loss: 0.05195265141582622, Val Accuracy: 0.9869127028779474
100%|████████████████████████████████████████████████| 938/938 [00:07<00:00, 125.32it/s, accuracy=1, loss=0.0322, lr=0.000349]
Epoch 11, Val Loss: 0.0462392206798608, Val Accuracy: 0.9890153710914046
100%|████████████████████████████████████████████████| 938/938 [00:05<00:00, 182.56it/s, accuracy=1, loss=0.0101, lr=0.000314]
Epoch 12, Val Loss: 0.0459311623210001, Val Accuracy: 0.9891603826923326
100%|███████████████████████████████████████████████| 938/938 [00:04<00:00, 190.33it/s, accuracy=1, loss=0.00499, lr=0.000282]
Epoch 13, Val Loss: 0.046083818829949004, Val Accuracy: 0.9889428652909406
100%|████████████████████████████████████████████████| 938/938 [00:04<00:00, 192.37it/s, accuracy=1, loss=0.0277, lr=0.000254]
Epoch 14, Val Loss: 0.04589189210039047, Val Accuracy: 0.9892328884927967
100%|█████████████████████████████████████████████| 938/938 [00:05<00:00, 185.87it/s, accuracy=0.938, loss=0.118, lr=0.000229]
Epoch 15, Val Loss: 0.045461541470388715, Val Accuracy: 0.9897766819962769
100%|███████████████████████████████████████████████| 938/938 [00:04<00:00, 189.05it/s, accuracy=1, loss=0.00417, lr=0.000206]
Epoch 16, Val Loss: 0.04390160738300908, Val Accuracy: 0.9901754638988292
100%|███████████████████████████████████████████████| 938/938 [00:05<00:00, 166.96it/s, accuracy=1, loss=0.00757, lr=0.000185]
Epoch 17, Val Loss: 0.04456612090557206, Val Accuracy: 0.9898491877967409
100%|████████████████████████████████████████████████| 938/938 [00:05<00:00, 157.91it/s, accuracy=1, loss=0.0216, lr=0.000167]
Epoch 18, Val Loss: 0.04330025613415995, Val Accuracy: 0.9904654871006853
100%|█████████████████████████████████████████████████| 938/938 [00:05<00:00, 176.92it/s, accuracy=1, loss=0.0194, lr=0.00015]
Epoch 19, Val Loss: 0.04605526185540208, Val Accuracy: 0.9896679232955808
100%|███████████████████████████████████████████████| 938/938 [00:07<00:00, 121.44it/s, accuracy=1, loss=0.00293, lr=0.000135]
Epoch 20, Val Loss: 0.04234921921814658, Val Accuracy: 0.9906104987016133

real    2m45.505s
user    2m49.766s
sys     0m2.534s
```

```
(base) ye@lst-hpc3090:~$ nvidia-smi
Sat Nov  9 16:02:45 2024
+---------------------------------------------------------------------------------------+
| NVIDIA-SMI 535.171.04             Driver Version: 535.171.04   CUDA Version: 12.2     |
|-----------------------------------------+----------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |         Memory-Usage | GPU-Util  Compute M. |
|                                         |                      |               MIG M. |
|=========================================+======================+======================|
|   0  NVIDIA GeForce RTX 3090 Ti     Off | 00000000:01:00.0 Off |                  Off |
| 40%   68C    P2             228W / 480W |  14064MiB / 24564MiB |     60%      Default |
|                                         |                      |                  N/A |
+-----------------------------------------+----------------------+----------------------+

+---------------------------------------------------------------------------------------+
| Processes:                                                                            |
|  GPU   GI   CI        PID   Type   Process name                            GPU Memory |
|        ID   ID                                                             Usage      |
|=======================================================================================|
|    0   N/A  N/A     38513      G   /usr/lib/xorg/Xorg                           16MiB |
|    0   N/A  N/A    114721      G   /usr/lib/xorg/Xorg                           33MiB |
|    0   N/A  N/A    114934      G   /usr/bin/gnome-shell                         15MiB |
|    0   N/A  N/A    250997      C   python                                    13510MiB |
|    0   N/A  N/A    262404      C   .../miniforge3/envs/opennmt/bin/python      346MiB |
+---------------------------------------------------------------------------------------+
(base) ye@lst-hpc3090:~$
```

```
(base) ye@lst-hpc3090:~$ nvidia-smi
Sat Nov  9 16:04:35 2024
+---------------------------------------------------------------------------------------+
| NVIDIA-SMI 535.171.04             Driver Version: 535.171.04   CUDA Version: 12.2     |
|-----------------------------------------+----------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |         Memory-Usage | GPU-Util  Compute M. |
|                                         |                      |               MIG M. |
|=========================================+======================+======================|
|   0  NVIDIA GeForce RTX 3090 Ti     Off | 00000000:01:00.0 Off |                  Off |
| 44%   72C    P2             292W / 480W |  12696MiB / 24564MiB |     98%      Default |
|                                         |                      |                  N/A |
+-----------------------------------------+----------------------+----------------------+

+---------------------------------------------------------------------------------------+
| Processes:                                                                            |
|  GPU   GI   CI        PID   Type   Process name                            GPU Memory |
|        ID   ID                                                             Usage      |
|=======================================================================================|
|    0   N/A  N/A     38513      G   /usr/lib/xorg/Xorg                           16MiB |
|    0   N/A  N/A    114721      G   /usr/lib/xorg/Xorg                           33MiB |
|    0   N/A  N/A    114934      G   /usr/bin/gnome-shell                         15MiB |
|    0   N/A  N/A    250997      C   python                                    12142MiB |
|    0   N/A  N/A    262404      C   .../miniforge3/envs/opennmt/bin/python      346MiB |
+---------------------------------------------------------------------------------------+
(base) ye@lst-hpc3090:~$
```

The whole log ...  

```
(opennmt) ye@lst-hpc3090:~/exp/fast-kan$ cat ./train_mlp_my_mnist.log
Epoch 1, Val Loss: 0.11971162100972958, Val Accuracy: 0.9632554749878266
Epoch 2, Val Loss: 0.08309285057030116, Val Accuracy: 0.977156251738077
Epoch 3, Val Loss: 0.08929499804005546, Val Accuracy: 0.9740225863567361
Epoch 4, Val Loss: 0.06953242195666424, Val Accuracy: 0.9831424012538176
Epoch 5, Val Loss: 0.06144784629564266, Val Accuracy: 0.9847737817642583
Epoch 6, Val Loss: 0.057038711576523765, Val Accuracy: 0.9853900810682027
Epoch 7, Val Loss: 0.06414103208665073, Val Accuracy: 0.9835774360566018
Epoch 8, Val Loss: 0.0507286353477843, Val Accuracy: 0.9878552782839799
Epoch 9, Val Loss: 0.052350924623330075, Val Accuracy: 0.9869127028779474
Epoch 10, Val Loss: 0.05195265141582622, Val Accuracy: 0.9869127028779474
Epoch 11, Val Loss: 0.0462392206798608, Val Accuracy: 0.9890153710914046
Epoch 12, Val Loss: 0.0459311623210001, Val Accuracy: 0.9891603826923326
Epoch 13, Val Loss: 0.046083818829949004, Val Accuracy: 0.9889428652909406
Epoch 14, Val Loss: 0.04589189210039047, Val Accuracy: 0.9892328884927967
Epoch 15, Val Loss: 0.045461541470388715, Val Accuracy: 0.9897766819962769
Epoch 16, Val Loss: 0.04390160738300908, Val Accuracy: 0.9901754638988292
Epoch 17, Val Loss: 0.04456612090557206, Val Accuracy: 0.9898491877967409
Epoch 18, Val Loss: 0.04330025613415995, Val Accuracy: 0.9904654871006853
Epoch 19, Val Loss: 0.04605526185540208, Val Accuracy: 0.9896679232955808
Epoch 20, Val Loss: 0.04234921921814658, Val Accuracy: 0.9906104987016133
(opennmt) ye@lst-hpc3090:~/exp/fast-kan$
```

## ChebyKAN

```
(opennmt) ye@lst-hpc3090:~/exp$ git clone https://github.com/SynodicMonth/ChebyKAN
Cloning into 'ChebyKAN'...
remote: Enumerating objects: 45, done.
remote: Counting objects: 100% (45/45), done.
remote: Compressing objects: 100% (37/37), done.
remote: Total 45 (delta 18), reused 30 (delta 7), pack-reused 0 (from 0)
Receiving objects: 100% (45/45), 1.96 MiB | 2.90 MiB/s, done.
Resolving deltas: 100% (18/18), done.
(opennmt) ye@lst-hpc3090:~/exp$
```

```
Epoch 23, Train Loss: 0.0231, Test Loss: 0.1156, Test Acc: 0.97
Epoch 24, Train Loss: 0.0261, Test Loss: 0.1218, Test Acc: 0.97
Epoch 25, Train Loss: 0.0240, Test Loss: 0.1254, Test Acc: 0.97
Epoch 26, Train Loss: 0.0244, Test Loss: 0.1255, Test Acc: 0.97
Epoch 27, Train Loss: 0.0192, Test Loss: 0.1307, Test Acc: 0.97
Epoch 28, Train Loss: 0.0202, Test Loss: 0.1283, Test Acc: 0.97
Epoch 29, Train Loss: 0.0162, Test Loss: 0.1375, Test Acc: 0.96
Epoch 30, Train Loss: 0.0214, Test Loss: 0.1273, Test Acc: 0.97

real    2m18.388s
user    2m8.082s
sys     0m3.150s
(opennmt) ye@lst-hpc3090:~/exp/ChebyKAN$ time /home/ye/miniforge3/envs/opennmt/bin/python ./chebyKan-mnist.py | tee chebyKan-en-MNIST.log
```

Check the whole log:  

```
(opennmt) ye@lst-hpc3090:~/exp/ChebyKAN$ cat ./chebyKan-en-MNIST.log
...
...
...
Downloading https://ossci-datasets.s3.amazonaws.com/mnist/t10k-labels-idx1-ubyte.gz to ./data/MNIST/raw/t10k-labels-idx1-ubyte.gz
Extracting ./data/MNIST/raw/t10k-labels-idx1-ubyte.gz to ./data/MNIST/raw

Total trainable parameters: 128896
Epoch 1, Train Loss: 1.0977, Test Loss: 0.4405, Test Acc: 0.92
Epoch 2, Train Loss: 0.3236, Test Loss: 0.2533, Test Acc: 0.94
Epoch 3, Train Loss: 0.2066, Test Loss: 0.2107, Test Acc: 0.95
Epoch 4, Train Loss: 0.1637, Test Loss: 0.1779, Test Acc: 0.95
Epoch 5, Train Loss: 0.1363, Test Loss: 0.1383, Test Acc: 0.96
Epoch 6, Train Loss: 0.1166, Test Loss: 0.1395, Test Acc: 0.96
Epoch 7, Train Loss: 0.1010, Test Loss: 0.1543, Test Acc: 0.96
Epoch 8, Train Loss: 0.0904, Test Loss: 0.1296, Test Acc: 0.96
Epoch 9, Train Loss: 0.0808, Test Loss: 0.1230, Test Acc: 0.96
Epoch 10, Train Loss: 0.0745, Test Loss: 0.1232, Test Acc: 0.96
Epoch 11, Train Loss: 0.0666, Test Loss: 0.1317, Test Acc: 0.96
Epoch 12, Train Loss: 0.0600, Test Loss: 0.1228, Test Acc: 0.97
Epoch 13, Train Loss: 0.0555, Test Loss: 0.1346, Test Acc: 0.96
Epoch 14, Train Loss: 0.0508, Test Loss: 0.1306, Test Acc: 0.96
Epoch 15, Train Loss: 0.0456, Test Loss: 0.1168, Test Acc: 0.97
Epoch 16, Train Loss: 0.0434, Test Loss: 0.1237, Test Acc: 0.97
Epoch 17, Train Loss: 0.0389, Test Loss: 0.1129, Test Acc: 0.97
Epoch 18, Train Loss: 0.0367, Test Loss: 0.1271, Test Acc: 0.96
Epoch 19, Train Loss: 0.0369, Test Loss: 0.1386, Test Acc: 0.96
Epoch 20, Train Loss: 0.0350, Test Loss: 0.1270, Test Acc: 0.96
Epoch 21, Train Loss: 0.0284, Test Loss: 0.1291, Test Acc: 0.96
Epoch 22, Train Loss: 0.0280, Test Loss: 0.1123, Test Acc: 0.97
Epoch 23, Train Loss: 0.0231, Test Loss: 0.1156, Test Acc: 0.97
Epoch 24, Train Loss: 0.0261, Test Loss: 0.1218, Test Acc: 0.97
Epoch 25, Train Loss: 0.0240, Test Loss: 0.1254, Test Acc: 0.97
Epoch 26, Train Loss: 0.0244, Test Loss: 0.1255, Test Acc: 0.97
Epoch 27, Train Loss: 0.0192, Test Loss: 0.1307, Test Acc: 0.97
Epoch 28, Train Loss: 0.0202, Test Loss: 0.1283, Test Acc: 0.97
Epoch 29, Train Loss: 0.0162, Test Loss: 0.1375, Test Acc: 0.96
Epoch 30, Train Loss: 0.0214, Test Loss: 0.1273, Test Acc: 0.97
(opennmt) ye@lst-hpc3090:~/exp/ChebyKAN$
```

## Preparing for Cheby-KAN experiment with BHDD Dataset  

```
(opennmt) ye@lst-hpc3090:~/exp/ChebyKAN/data/MNIST$ mv raw eng_raw
(opennmt) ye@lst-hpc3090:~/exp/ChebyKAN/data/MNIST$ cp ../../../fast-kan/data/MNIST/raw . -r
(opennmt) ye@lst-hpc3090:~/exp/ChebyKAN/data/MNIST$
```

Make confirmation ...  

```
(opennmt) ye@lst-hpc3090:~/exp/ChebyKAN/data/MNIST$ ls
eng_raw  raw
(opennmt) ye@lst-hpc3090:~/exp/ChebyKAN/data/MNIST$ ls ./raw/
t10k-images-idx3-ubyte  t10k-labels-idx1-ubyte  train-images-idx3-ubyte  train-labels-idx1-ubyte
(opennmt) ye@lst-hpc3090:~/exp/ChebyKAN/data/MNIST$ wc ./raw/*ubyte
   58093   230240 21607840 ./raw/t10k-images-idx3-ubyte
       0        1    27569 ./raw/t10k-labels-idx1-ubyte
  121880   484576 47040016 ./raw/train-images-idx3-ubyte
       0        1    60008 ./raw/train-labels-idx1-ubyte
  179973   714818 68735433 total
(opennmt) ye@lst-hpc3090:~/exp/ChebyKAN/data/MNIST$
(opennmt) ye@lst-hpc3090:~/exp/ChebyKAN/data/MNIST$ wc ./eng_raw/*ubyte
    6055    30268  7840016 ./eng_raw/t10k-images-idx3-ubyte
       0        1    10008 ./eng_raw/t10k-labels-idx1-ubyte
   35282   180029 47040016 ./eng_raw/train-images-idx3-ubyte
       0        1    60008 ./eng_raw/train-labels-idx1-ubyte
   41337   210299 54950048 total
(opennmt) ye@lst-hpc3090:~/exp/ChebyKAN/data/MNIST$
```

## Cheby-KAN with BHDD, GPU 

Training, testing ...  

```
(opennmt) ye@lst-hpc3090:~/exp/ChebyKAN$ time /home/ye/miniforge3/envs/opennmt/bin/python ./chebyKan-mnist.py | tee chebyKan-my-MNIST.log
...
...
...
Epoch 20, Train Loss: 0.0089, Test Loss: 0.0484, Test Acc: 0.99
Epoch 21, Train Loss: 0.0056, Test Loss: 0.0377, Test Acc: 0.99
Epoch 22, Train Loss: 0.0041, Test Loss: 0.0449, Test Acc: 0.99
Epoch 23, Train Loss: 0.0052, Test Loss: 0.0363, Test Acc: 0.99
Epoch 24, Train Loss: 0.0062, Test Loss: 0.0328, Test Acc: 0.99
Epoch 25, Train Loss: 0.0013, Test Loss: 0.0811, Test Acc: 0.98
Epoch 26, Train Loss: 0.0066, Test Loss: 0.0427, Test Acc: 0.99
Epoch 27, Train Loss: 0.0016, Test Loss: 0.0362, Test Acc: 0.99
Epoch 28, Train Loss: 0.0053, Test Loss: 0.0345, Test Acc: 0.99
Epoch 29, Train Loss: 0.0043, Test Loss: 0.0358, Test Acc: 0.99
Epoch 30, Train Loss: 0.0053, Test Loss: 0.0805, Test Acc: 0.98

real    2m35.907s
user    2m42.217s
sys     0m2.970s
```

Check the whole training log file:  

```
(opennmt) ye@lst-hpc3090:~/exp/ChebyKAN$ cat ./chebyKan-my-MNIST.log
Total trainable parameters: 128896
Epoch 1, Train Loss: 0.9244, Test Loss: 0.2245, Test Acc: 0.98
Epoch 2, Train Loss: 0.1351, Test Loss: 0.0776, Test Acc: 0.99
Epoch 3, Train Loss: 0.0660, Test Loss: 0.0622, Test Acc: 0.99
Epoch 4, Train Loss: 0.0458, Test Loss: 0.0673, Test Acc: 0.98
Epoch 5, Train Loss: 0.0352, Test Loss: 0.0531, Test Acc: 0.99
Epoch 6, Train Loss: 0.0266, Test Loss: 0.0497, Test Acc: 0.99
Epoch 7, Train Loss: 0.0223, Test Loss: 0.0403, Test Acc: 0.99
Epoch 8, Train Loss: 0.0210, Test Loss: 0.0442, Test Acc: 0.99
Epoch 9, Train Loss: 0.0163, Test Loss: 0.0738, Test Acc: 0.98
Epoch 10, Train Loss: 0.0175, Test Loss: 0.0714, Test Acc: 0.98
Epoch 11, Train Loss: 0.0135, Test Loss: 0.0387, Test Acc: 0.99
Epoch 12, Train Loss: 0.0130, Test Loss: 0.0428, Test Acc: 0.99
Epoch 13, Train Loss: 0.0089, Test Loss: 0.0412, Test Acc: 0.99
Epoch 14, Train Loss: 0.0110, Test Loss: 0.0764, Test Acc: 0.98
Epoch 15, Train Loss: 0.0104, Test Loss: 0.0506, Test Acc: 0.99
Epoch 16, Train Loss: 0.0085, Test Loss: 0.0372, Test Acc: 0.99
Epoch 17, Train Loss: 0.0043, Test Loss: 0.0630, Test Acc: 0.98
Epoch 18, Train Loss: 0.0111, Test Loss: 0.0438, Test Acc: 0.99
Epoch 19, Train Loss: 0.0052, Test Loss: 0.0488, Test Acc: 0.99
Epoch 20, Train Loss: 0.0089, Test Loss: 0.0484, Test Acc: 0.99
Epoch 21, Train Loss: 0.0056, Test Loss: 0.0377, Test Acc: 0.99
Epoch 22, Train Loss: 0.0041, Test Loss: 0.0449, Test Acc: 0.99
Epoch 23, Train Loss: 0.0052, Test Loss: 0.0363, Test Acc: 0.99
Epoch 24, Train Loss: 0.0062, Test Loss: 0.0328, Test Acc: 0.99
Epoch 25, Train Loss: 0.0013, Test Loss: 0.0811, Test Acc: 0.98
Epoch 26, Train Loss: 0.0066, Test Loss: 0.0427, Test Acc: 0.99
Epoch 27, Train Loss: 0.0016, Test Loss: 0.0362, Test Acc: 0.99
Epoch 28, Train Loss: 0.0053, Test Loss: 0.0345, Test Acc: 0.99
Epoch 29, Train Loss: 0.0043, Test Loss: 0.0358, Test Acc: 0.99
Epoch 30, Train Loss: 0.0053, Test Loss: 0.0805, Test Acc: 0.98
(opennmt) ye@lst-hpc3090:~/exp/ChebyKAN$
```

### Code Edited

Test Acc ကို တခြား Efficient, Fast တို့နဲ့ နှိုင်းယှဉ်တဲ့အခါမှာ ညီအောင်လို့ decimal ၄နေရာထားဖို့ နဲ့ 10 epoch နဲ့ ပဲ run ဖို့ code ကို ဝင်ပြင်ခဲ့...  

```
(opennmt) ye@lst-hpc3090:~/exp/ChebyKAN$ time /home/ye/miniforge3/envs/opennmt/bin/python ./chebyKan-mnist-edited.py | tee che
byKan-my-MNIST.log2
Total trainable parameters: 128896
Epoch 1, Train Loss: 0.8835, Test Loss: 0.2178, Test Acc: 0.9762
Epoch 2, Train Loss: 0.1360, Test Loss: 0.1011, Test Acc: 0.9823
Epoch 3, Train Loss: 0.0706, Test Loss: 0.0743, Test Acc: 0.9827
Epoch 4, Train Loss: 0.0460, Test Loss: 0.0614, Test Acc: 0.9845
Epoch 5, Train Loss: 0.0376, Test Loss: 0.0655, Test Acc: 0.9814
Epoch 6, Train Loss: 0.0306, Test Loss: 0.0896, Test Acc: 0.9734
Epoch 7, Train Loss: 0.0247, Test Loss: 0.0698, Test Acc: 0.9797
Epoch 8, Train Loss: 0.0234, Test Loss: 0.0409, Test Acc: 0.9888
Epoch 9, Train Loss: 0.0210, Test Loss: 0.0460, Test Acc: 0.9872
Epoch 10, Train Loss: 0.0161, Test Loss: 0.0474, Test Acc: 0.9868

real    0m46.137s
user    0m48.701s
sys     0m2.818s
(opennmt) ye@lst-hpc3090:~/exp/ChebyKAN$
```

## Summary of Experiment Results

## Runnning Time Log  

(py3.8) ye@lst-gpu-server-197:~/ye/exp/fast-kan$ time python ./examples/train_mlp_mydigit_mnist.py | tee mlp_my_train1.log  

MLP, CPU: 8m16.909s  

Efficient-KAN, CPU: 5m45.985s  
Fast-KAN, CPU: 9m36.818s  

Efficient-KAN, GPU: 0m55.070s  
Fast-KAN, GPU: 0m50.572s  


### Comparison Between Efficient-KAN and Fast-KAN for Myanmar MNIST (BHDD) on CPU  

| **Epoch** | **Efficient-KAN Val Accuracy** | **Fast-KAN Val Accuracy** |
|-----------|--------------------------------|---------------------------|
| 1         | 0.9835                         | 0.9779                    |
| 2         | 0.9848                         | 0.9862                    |
| 3         | 0.9891                         | 0.9808                    |
| 4         | 0.9871                         | 0.9870                    |
| 5         | 0.9884                         | 0.9870                    |
| 6         | 0.9896                         | 0.9913                    |
| 7         | 0.9908                         | 0.9905                    |
| 8         | 0.9909                         | 0.9908                    |
| 9         | 0.9907                         | 0.9913                    |
| 10        | 0.9908                         | 0.9913                    |

### Comparison Between Efficient-KAN and Fast-KAN for Myanmar MNIST (BHDD) on GPU  

| **Epoch** | **Efficient-KAN Val Accuracy** | **Fast-KAN Val Accuracy** |
|-----------|--------------------------------|---------------------------|
| 1         | 0.9814                         | 0.9787                    |
| 2         | 0.9869                         | 0.9736                    |
| 3         | 0.9893                         | 0.9869                    |
| 4         | 0.9869                         | 0.9890                    |
| 5         | 0.9895                         | 0.9875                    |
| 6         | 0.9903                         | 0.9916                    |
| 7         | 0.9907                         | 0.9900                    |
| 8         | 0.9917                         | 0.9896                    |
| 9         | 0.9904                         | 0.9913                    |
| 10        | 0.9911                         | 0.9911                    |

## MLP Results

| Epoch | MLP on CPU - Val Loss | MLP on CPU - Val Accuracy | MLP on GPU - Val Loss | MLP on GPU - Val Accuracy |
|-------|------------------------|---------------------------|------------------------|---------------------------|
| 1     | 0.1354                | 0.9611                    | 0.1197                | 0.9633                    |
| 2     | 0.0822                | 0.9793                    | 0.0831                | 0.9772                    |
| 3     | 0.0824                | 0.9780                    | 0.0893                | 0.9740                    |
| 4     | 0.0821                | 0.9782                    | 0.0695                | 0.9831                    |
| 5     | 0.0664                | 0.9841                    | 0.0614                | 0.9848                    |
| 6     | 0.0530                | 0.9875                    | 0.0570                | 0.9854                    |
| 7     | 0.0556                | 0.9868                    | 0.0641                | 0.9836                    |
| 8     | 0.0667                | 0.9821                    | 0.0507                | 0.9879                    |
| 9     | 0.0507                | 0.9872                    | 0.0524                | 0.9869                    |
| 10    | 0.0541                | 0.9872                    | 0.0520                | 0.9869                    |

## Validation Accuracy of MLP, Efficient-KAN and Fast-KAN Results

| **Epoch** | **MLP** | **Efficient-KAN** | **Fast-KAN** | **Cheby-KAN** |
|-----------|-----------------------|--------------------------------|---------------------------|---------------------------|
| 1         | 0.9633               | 0.9814                         | 0.9787                    | 0.9762                    |
| 2         | 0.9772               | 0.9869                         | 0.9736                    | 0.9823                    |
| 3         | 0.9740               | 0.9893                         | 0.9869                    | 0.9827                    |
| 4         | 0.9831               | 0.9869                         | 0.9890                    | 0.9845                    |
| 5         | 0.9848               | 0.9895                         | 0.9875                    | 0.9814                    |
| 6         | 0.9854               | 0.9903                         | 0.9916                    | 0.9734                    |
| 7         | 0.9836               | 0.9907                         | 0.9900                    | 0.9797                    |
| 8         | 0.9879               | 0.9917                         | 0.9896                    | 0.9888                    |
| 9         | 0.9869               | 0.9904                         | 0.9913                    | 0.9872                    |
| 10        | 0.9869               | 0.9911                         | 0.9911                    | 0.9868                    |

## Run Efficient-KAN and Fast-Kan Again for Drawing Loss Graph

```python

```

Training/Testing again with updated code for Efficient-KAN ...  

```
(opennmt) ye@lst-hpc3090:~/exp/efficient-kan/src$ time /home/ye/miniforge3/envs/opennmt/bin/python ./mnist-graph.py | tee efficientKan-my-MNIST.log2
100%|███████████████████████████████████████████████████| 938/938 [00:05<00:00, 184.46it/s, accuracy=1, loss=0.0281, lr=0.001]
Epoch 1, Val Loss: 0.08466717604928047, Val Accuracy: 0.9795126902531581
100%|██████████████████████████████████████████████████| 938/938 [00:04<00:00, 201.02it/s, accuracy=1, loss=0.0148, lr=0.0008]
  0%|                                                                                                 | 0/938 [00:00<?, ?it/s]Epoch 2, Val Loss: 0.058215294191030366, Val Accuracy: 0.9857888629707549
100%|██████████████████████████████████████████████| 938/938 [00:04<00:00, 210.31it/s, accuracy=0.938, loss=0.148, lr=0.00064]
Epoch 3, Val Loss: 0.05016020489608104, Val Accuracy: 0.9874927492816598
100%|███████████████████████████████████████████████| 938/938 [00:03<00:00, 248.01it/s, accuracy=1, loss=0.00325, lr=0.000512]
Epoch 4, Val Loss: 0.04975095358752838, Val Accuracy: 0.9875811710435111
100%|█████████████████████████████████████████████████| 938/938 [00:03<00:00, 249.93it/s, accuracy=1, loss=0.0032, lr=0.00041]
Epoch 5, Val Loss: 0.0430363102507045, Val Accuracy: 0.9901029580983651
100%|████████████████████████████████████████████████| 938/938 [00:03<00:00, 250.23it/s, accuracy=1, loss=0.0083, lr=0.000328]
Epoch 6, Val Loss: 0.03907314038296876, Val Accuracy: 0.9904292342004533
100%|████████████████████████████████████████████| 938/938 [00:03<00:00, 249.89it/s, accuracy=0.969, loss=0.0313, lr=0.000262]
Epoch 7, Val Loss: 0.0437598306955251, Val Accuracy: 0.9891400457534879
100%|████████████████████████████████████████████████| 938/938 [00:03<00:00, 249.61it/s, accuracy=1, loss=0.00913, lr=0.00021]
Epoch 8, Val Loss: 0.038671318704846885, Val Accuracy: 0.9906830045020774
100%|███████████████████████████████████████████████| 938/938 [00:03<00:00, 249.90it/s, accuracy=1, loss=0.00109, lr=0.000168]
Epoch 9, Val Loss: 0.038683194557033056, Val Accuracy: 0.9906467516018453
100%|███████████████████████████████████████████████| 938/938 [00:03<00:00, 245.48it/s, accuracy=1, loss=0.00811, lr=0.000134]
Epoch 10, Val Loss: 0.03851887913436462, Val Accuracy: 0.9903567283999892

real    0m55.702s
user    0m59.113s
sys     0m2.653s
(opennmt) ye@lst-hpc3090:~/exp/efficient-kan/src$
```

Code updated. Training/Testing again for fast-KAN ...  

```
(opennmt) ye@lst-hpc3090:~/exp/fast-kan$ time /home/ye/miniforge3/envs/opennmt/bin/python ./train_my_mnist_graph.py | tee fastKan-my-MNIST.log
100%|██████████████████████████████████████████████████| 938/938 [00:04<00:00, 228.44it/s, accuracy=1, loss=0.00978, lr=0.001]
Epoch 1, Val Loss: 0.08710137164985152, Val Accuracy: 0.9727740717874602
100%|██████████████████████████████████████████████████| 938/938 [00:03<00:00, 269.33it/s, accuracy=1, loss=0.0591, lr=0.0008]
Epoch 2, Val Loss: 0.07874783435555525, Val Accuracy: 0.9773419372166946
100%|█████████████████████████████████████████████████| 938/938 [00:03<00:00, 282.00it/s, accuracy=1, loss=0.0128, lr=0.00064]
Epoch 3, Val Loss: 0.07185747377032073, Val Accuracy: 0.9798433873327038
100%|███████████████████████████████████████████████| 938/938 [00:03<00:00, 282.52it/s, accuracy=1, loss=0.00113, lr=0.000512]
Epoch 4, Val Loss: 0.043615318760772834, Val Accuracy: 0.9878915311842119
100%|████████████████████████████████████████████████| 938/938 [00:03<00:00, 283.80it/s, accuracy=1, loss=0.00106, lr=0.00041]
Epoch 5, Val Loss: 0.047340849164620544, Val Accuracy: 0.9875290021818918
100%|████████████████████████████████████████████████| 938/938 [00:03<00:00, 284.59it/s, accuracy=1, loss=0.0107, lr=0.000328]
Epoch 6, Val Loss: 0.04776951485124942, Val Accuracy: 0.9878190253837479
100%|██████████████████████████████████████████████| 938/938 [00:03<00:00, 269.15it/s, accuracy=1, loss=0.000399, lr=0.000262]
Epoch 7, Val Loss: 0.04081620575311559, Val Accuracy: 0.9899941993976691
100%|███████████████████████████████████████████████| 938/938 [00:03<00:00, 282.03it/s, accuracy=1, loss=0.000147, lr=0.00021]
Epoch 8, Val Loss: 0.03648368091546804, Val Accuracy: 0.9906467516018453
100%|███████████████████████████████████████████████| 938/938 [00:03<00:00, 284.93it/s, accuracy=1, loss=9.83e-5, lr=0.000168]
Epoch 9, Val Loss: 0.038033672739875075, Val Accuracy: 0.9905742458013813
100%|███████████████████████████████████████████████| 938/938 [00:03<00:00, 284.33it/s, accuracy=1, loss=4.73e-5, lr=0.000134]
Epoch 10, Val Loss: 0.03722145387833574, Val Accuracy: 0.9906830045020774

real    0m48.116s
user    0m51.046s
sys     0m2.709s
(opennmt) ye@lst-hpc3090:~/exp/fast-kan$
```

## Running Again for MLP to Draw Loss Graph

```
(opennmt) ye@lst-hpc3090:~/exp/fast-kan$ time /home/ye/miniforge3/envs/opennmt/bin/python ./train_mlp_mydigit_mnist_graph.py | tee mlp_my_mnist.log2
100%|████████████████████████████████████████████████| 938/938 [00:03<00:00, 250.69it/s, accuracy=0.875, loss=0.384, lr=0.001]
Epoch 1, Val Loss: 0.12013111482622867, Val Accuracy: 0.964664916981124
100%|███████████████████████████████████████████████| 938/938 [00:03<00:00, 281.50it/s, accuracy=0.969, loss=0.106, lr=0.0009]
Epoch 2, Val Loss: 0.08532989450585607, Val Accuracy: 0.9763427719715853
100%|█████████████████████████████████████████████████| 938/938 [00:03<00:00, 303.11it/s, accuracy=1, loss=0.0306, lr=0.00081]
Epoch 3, Val Loss: 0.07429119747827853, Val Accuracy: 0.9809990591626709
100%|████████████████████████████████████████████████| 938/938 [00:03<00:00, 239.55it/s, accuracy=1, loss=0.0471, lr=0.000729]
Epoch 4, Val Loss: 0.06044211336967952, Val Accuracy: 0.9847375288640263
100%|████████████████████████████████████████████| 938/938 [00:03<00:00, 274.40it/s, accuracy=0.969, loss=0.0734, lr=0.000656]
  0%|                                                                                                 | 0/938 [00:00<?, ?it/s]Epoch 5, Val Loss: 0.06170507169300539, Val Accuracy: 0.9836658578184531
100%|█████████████████████████████████████████████████| 938/938 [00:03<00:00, 269.24it/s, accuracy=1, loss=0.0313, lr=0.00059]
Epoch 6, Val Loss: 0.062107068660459425, Val Accuracy: 0.9841733984217013
100%|█████████████████████████████████████████████| 938/938 [00:03<00:00, 277.72it/s, accuracy=0.969, loss=0.162, lr=0.000531]
Epoch 7, Val Loss: 0.062496583417204925, Val Accuracy: 0.983557099117757
100%|████████████████████████████████████████████████| 938/938 [00:03<00:00, 310.19it/s, accuracy=1, loss=0.0604, lr=0.000478]
Epoch 8, Val Loss: 0.057975258996111625, Val Accuracy: 0.9849912991656504
100%|█████████████████████████████████████████████| 938/938 [00:03<00:00, 310.13it/s, accuracy=0.969, loss=0.0575, lr=0.00043]
Epoch 9, Val Loss: 0.05984460091647279, Val Accuracy: 0.9848622035261096
100%|█████████████████████████████████████████████| 938/938 [00:03<00:00, 295.83it/s, accuracy=0.969, loss=0.281, lr=0.000387]
Epoch 10, Val Loss: 0.04803686592297892, Val Accuracy: 0.9886165891888523

real    0m46.878s
user    0m49.217s
sys     0m2.777s
(opennmt) ye@lst-hpc3090:~/exp/fast-kan$
```

## Loss Graphs

<br />

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/KAN-exp-BHDD/mlp-my-mnist-loss.png" alt="MLP" width="450"/>  
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/KAN-exp-BHDD/chebyKAN-my-mnist.png" alt="Cheby-KAN" width="450"/>
</p>  
<div align="center">
  Fig.1 Loss graph <br />
  (Left: for MLP, Right: Cheby-KAN)
</div> 


## Reference Link

Quick Intro to KAN:  
https://kindxiaoming.github.io/pykan/intro.html 

Original Implementation:  
https://github.com/KindXiaoming/pykan  

Efficient-KAN:  
https://github.com/Blealtan/efficient-kan  

Fast-KAN:  
https://github.com/ZiyaoLi/fast-kan  

FasterKAN:  
https://github.com/AthanasiosDelis/faster-kan  

benchmarking-KAN:  
https://github.com/eleonorapoeta/benchmarking-KAN  


Very Slow Information:  
https://github.com/ale93111/pykan_mnist

Ziming Liu Homepage:  
https://kindxiaoming.github.io/  

MNIST and PyKan:  
https://www.kaggle.com/code/minsithu/mnist-and-pykan  

Dissecting Kolmogorov-Arnold Network:  
https://feicheung2016.medium.com/dissecting-kolmogorov-arnold-network-f1bee719d949

## Lectures/Talks

KAN: Kolmogorov-Arnold Networks, Ziming Liu, MIT 2024  
(About 10 min)   
https://www.youtube.com/watch?v=ljgaYuYAQyY  

"KAN: Kolmogorov-Arnold Networks" by Ziming Liu    
(about 58 min)  
https://www.youtube.com/watch?v=uupyXjSnZiA  

https://www.youtube.com/watch?v=AUDHb-tnlB0  

## Some Previous Works

https://github.com/hereisamara/Burmese-Handwriting-Digit-Recognizer  

How Resilient Are Kolmogorov–Arnold Networks in Classification Tasks? A Robustness Investigation
by Ahmed Dawod Mohammed IbrahumORCID,Zhengyu Shang andJang-Eui Hong:  

https://www.mdpi.com/2076-3417/14/22/10173

KAN: Kolmogorov-Arnold Networks:    
https://arxiv.org/abs/2404.19756  

Kolmogorov-Arnold Network Autoencoders:  
https://arxiv.org/abs/2410.02077  
