# Automatic Formating of your Python Code

Python code တွေကို အဖွဲ့လိုက်စုရေးကြတဲ့အခါမှာ၊ code အကြောင်းအရေအတွက် အများကြီး ရေးတဲ့အခါမှာ formatting ကို ညီအောင် ညှိကြရပါတယ်။   
ဒီ black ဆိုတဲ့ python library က formatting ကို ညီအောင်ညှိပေးတဲ့ library ပါ။  

## Installation of black

```
(base) ye@ykt-pro:/media/ye/project1/tool$ pip install black
Collecting black
  Downloading https://files.pythonhosted.org/packages/dc/7b/5a6bbe89de849f28d7c109f5ea87b65afa5124ad615f3419e71beb29dc96/black-20.8b1.tar.gz (1.1MB)
     |████████████████████████████████| 1.1MB 497kB/s 
  Installing build dependencies ... done
  Getting requirements to build wheel ... done
    Preparing wheel metadata ... done
Requirement already satisfied: regex>=2020.1.8 in /home/ye/.local/lib/python3.7/site-packages (from black) (2020.5.14)
Collecting appdirs (from black)
  Downloading https://files.pythonhosted.org/packages/3b/00/2344469e2084fb287c2e0b57b72910309874c3245463acd6cf5e3db69324/appdirs-1.4.4-py2.py3-none-any.whl
Requirement already satisfied: mypy-extensions>=0.4.3 in /home/ye/tool/anaconda3/lib/python3.7/site-packages (from black) (0.4.3)
Collecting typed-ast>=1.4.0 (from black)
  Downloading https://files.pythonhosted.org/packages/5d/10/0c1e8aa723a2b0c4032e048d8e511df82c8a1262f0e1df5e4c54eb2613e9/typed_ast-1.4.1-cp37-cp37m-manylinux1_x86_64.whl (737kB)
     |████████████████████████████████| 747kB 450kB/s 
Collecting click>=7.1.2 (from black)
  Using cached https://files.pythonhosted.org/packages/d2/3d/fa76db83bf75c4f8d338c2fd15c8d33fdd7ad23a9b5e57eb6c5de26b430e/click-7.1.2-py2.py3-none-any.whl
Collecting pathspec<1,>=0.6 (from black)
  Downloading https://files.pythonhosted.org/packages/29/29/a465741a3d97ea3c17d21eaad4c64205428bde56742360876c4391f930d4/pathspec-0.8.1-py2.py3-none-any.whl
Requirement already satisfied: typing-extensions>=3.7.4 in /home/ye/tool/anaconda3/lib/python3.7/site-packages (from black) (3.7.4.3)
Requirement already satisfied: toml>=0.10.1 in /home/ye/tool/anaconda3/lib/python3.7/site-packages (from black) (0.10.1)
Building wheels for collected packages: black
  Building wheel for black (PEP 517) ... done
  Created wheel for black: filename=black-20.8b1-cp37-none-any.whl size=124184 sha256=3d4adc78b705e0b24e38166d1c156e59a88d56901105ee83f46a3c33286e7112
  Stored in directory: /home/ye/.cache/pip/wheels/6e/10/b5/edf7359c2edd0305cce7e3f96e07daf7ce55dceac9d3ce3373
Successfully built black
Installing collected packages: appdirs, typed-ast, click, pathspec, black
  Found existing installation: Click 7.0
    Uninstalling Click-7.0:
      Successfully uninstalled Click-7.0
Successfully installed appdirs-1.4.4 black-20.8b1 click-7.1.2 pathspec-0.8.1 typed-ast-1.4.1
(base) ye@ykt-pro:/media/ye/project1/tool$
```

## Test

ဥပမာအနေနဲ့ chk-token.py ပရိုဂရမ်မှာ equal sign နေရာတို့ for loop နေရာတို့မှာ တမင်တာက alignment လွဲနေအောင် လုပ်ထားပါတယ်။   
Python programming မှာက indenting က လုပ်ရတာမို့ indenting မှန်ပေမဲ့ ပရိုဂရမ်ကလည်း run လို့ ရပေမယ့် ကြည့်ရတာမှာ ရုပ်ဆိုးအောင် တမင်တကာလုပ်ထားတာဖြစ်ပါတယ်။  

```
(base) ye@ykt-pro:/media/ye/project1/tool/black-tst$ cat ./chk-token.py 
import sys

# for checking no of tokens difference between parallel sentences
# written by Ye Kyaw Thu
# How to run: python ./chk-token.py <filename1> <filename2>
# eg 1: python ./chk-token.py ./writing.txt ./reading.txt $'\t'
# eg 2: python ./chk-token.py ./writing.txt ./reading.txt $'\n'

f1=sys.argv[1]
f2  = sys.argv[2]
sp = sys.argv[3]

fp1=open(f1,"r")
fp2=open(f2,"r")

for line1, line2 in zip(fp1, 
        fp2):
   if line1.count(' ')!=line2.count(' '):
      print(line1.strip() + sp + line2.strip())
        
fp1.close(   )
fp2.close()
```

အထက်ပါ ပရိုဂရမ်ကို black နဲ့ပြင်မယ်ဆိုရင် အောက်ပါအတိုင်း $black <python-program-filename> ဆိုတဲ့ ပုံစံနဲ့ run ပါ။  

```
(base) ye@ykt-pro:/media/ye/project1/tool/black-tst$ black ./chk-token.py 
reformatted chk-token.py
All done! ✨ 🍰 ✨
1 file reformatted.
```

format ကို ပြင်ပြီးထွက်လာတဲ့ ဖိုင်ကို cat လုပ်ကြည့်ရင်အောက်ပါအတိုင်းမြင်ရပါလိမ့်မယ်။ အဆင်ပြေတယ်နော်။  

```
(base) ye@ykt-pro:/media/ye/project1/tool/black-tst$ cat ./chk-token.py 
import sys

# for checking no of tokens difference between parallel sentences
# written by Ye Kyaw Thu
# How to run: python ./chk-token.py <filename1> <filename2>
# eg 1: python ./chk-token.py ./writing.txt ./reading.txt $'\t'
# eg 2: python ./chk-token.py ./writing.txt ./reading.txt $'\n'

f1 = sys.argv[1]
f2 = sys.argv[2]
sp = sys.argv[3]

fp1 = open(f1, "r")
fp2 = open(f2, "r")

for line1, line2 in zip(fp1, fp2):
    if line1.count(" ") != line2.count(" "):
        print(line1.strip() + sp + line2.strip())

fp1.close()
fp2.close()
```
