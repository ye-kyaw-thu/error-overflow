# ipynb to latex Conversion  

မြန်မာစာလုံးတွေပါတဲ့ jupyter notebook တွေကို pdf ဖိုင်အဖြစ် ပြောင်းတဲ့အခါမှာ မြန်မာစာတွေ မပေါ်တဲ့ ပြဿနာ ဖြစ်လေ့ရှိပါတယ်။  
အဲဒီအတွက် solution တခုကို လက်တွေ လုပ်ပြထားပါတယ်။  

```
ye@lst-hpc3090:~/exp/myTokenizer$ jupyter nbconvert --to latex ./baselines.ipynb
[NbConvertApp] Converting notebook ./baselines.ipynb to latex
[NbConvertApp] Writing 126732 bytes to baselines.tex
ye@lst-hpc3090:~/exp/myTokenizer$ jupyter nbconvert --to latex ./oppaWord.ipynb
[NbConvertApp] Converting notebook ./oppaWord.ipynb to latex
[NbConvertApp] Writing 99261 bytes to oppaWord.tex
ye@lst-hpc3090:~/exp/myTokenizer$ jupyter nbconvert --to latex ./exp_with_Dictionary.ipynb
[NbConvertApp] Converting notebook ./exp_with_Dictionary.ipynb to latex
[NbConvertApp] Writing 75538 bytes to exp_with_Dictionary.tex
ye@lst-hpc3090:~/exp/myTokenizer$ jupyter nbconvert --to latex ./WER_Calculation_example.ipynb
[NbConvertApp] Converting notebook ./WER_Calculation_example.ipynb to latex
[NbConvertApp] Writing 556288 bytes to WER_Calculation_example.tex
ye@lst-hpc3090:~/exp/myTokenizer$
```

## Editing Tex Files

```
ye@lst-hpc3090:~/exp/myTokenizer$ nano ./baselines.tex
ye@lst-hpc3090:~/exp/myTokenizer$ ye@lst-hpc3090:~/exp/myTokenizer$ nano ./oppaWord.tex
ye@lst-hpc3090:~/exp/myTokenizer$ ye@lst-hpc3090:~/exp/myTokenizer$ nano ./exp_with_Dictionary.tex
ye@lst-hpc3090:~/exp/myTokenizer$ ye@lst-hpc3090:~/exp/myTokenizer$ nano ./oppaWord.update.tex
```

ထွက်လာတဲ့ output text ဖိုင်တွေမှာ ဝင်ရေးတာမျိုး လုပ်ပါ။    

```
    \usepackage{fontspec}

    \newcommand\myfontsize{\fontsize{7pt}{10pt}\selectfont}
    \newfontfamily{\burmesefont }[Script=Myanmar]{Myanmar3}
    %\newfontfamily{\burmesefont}{Noto Sans Myanmar}
    %\newfontfamily{\burmesefont}{Padauk}
```

မြန်မာစာ ပါတဲ့ စာကြောင်းတွေကို \burmesefont{} နှင့်ဝင်ဖြည့်ပေးဖို့ ./modify_text.py နဲ့ ဝင်ပြင်ပါ။  

```
ye@lst-hpc3090:~/exp/myTokenizer$ python ./modify_tex.py -i ./baselines.tex -o ./baselines.update.tex
ye@lst-hpc3090:~/exp/myTokenizer$ python ./modify_tex.py -i ./oppaWord.tex -o ./oppaWord.update.tex
ye@lst-hpc3090:~/exp/myTokenizer$ python ./modify_tex.py -i ./exp_with_Dictionary.tex -o ./exp_with_Dictionary.update.tex
ye@lst-hpc3090:~/exp/myTokenizer$
```

## Compile with Xelaex  

နောက်ဆုံး အဆင့်အနေနဲ့ xelatex နဲ့ ပြင်ထားတဲ့ tex ဖိုင်တွေကို compile လုပ်ပါ။  

```
$xelatex ./baselines.update.tex
$xelatex ./oppaWord.update.tex
$xelatex ./exp_with_Dictionary.update.tex
```

```
ye@lst-hpc3090:~/exp/myTokenizer$ ls *.pdf
baselines.update.pdf  exp_with_Dictionary.update.pdf  oppaWord.update.pdf
```
