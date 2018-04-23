# Invisible Characters Problem

# In English:  
Display and removing invisible characters.  

# In Myanmar Language:  
ဖိုင်ထဲမှာ ရှိနေတဲ့ ပုံမှန်အားဖြင့် မမြင်ရတဲ့ စာလုံးတွေက ကျွန်တော်တို့ရဲ့ အလုပ်တွေကို ပုံစံအမျိုးမျိုးနဲ့ ဒုက္ခပေးတတ်ပါတယ်။  
ဒီနေ့ လက်တွေ့ကြုံရတဲ့ပြဿနာတစ်ခုကို ဥပမာတစ်ခုကိုအနေနဲ့ ပေးပါမယ်။  

Website တစ်ခုကနေ Python ပရိုဂရမ် တစ်ပုဒ်ကို selection မှတ်၊ ကော်ပီကူးပြီး ကိုယ်ရဲ့ notebook ထဲမှာ run တဲ့အခါမှာ ပုံမှန်မဟုတ်တဲ့ error တွေ  
အများကြီးတက်တာကို တွေ့လိုက်ရပါတယ်။ ပရိုဂရမ်ဖိုင်ကို ဖွင့်ကြည့်တော့လဲ syntax error, coding error စတာမျိုးကို တစ်ခုမှ မတွေ့ရပါဘူး။  
အတွေ့အကြုံအရ မသင်္ကာလို့ hidden (or) invisible characters တွေကို cat command -A option နဲ့ ပရင့်ထုတ်လိုက်တော့ ပြဿနာကို သိလိုက်ရပါတယ်။  
ကျွန်တော် copy ကူးပြီး run ဖို့ ကြိုးစားတဲ့ ပရိုဂရမ်က လိုင်းတွေအများကြီးမို့လို့ မြင်သာအောင် လိုင်းတချို့ကိုပဲ ဥပမာအနေနဲ့ ပြရရင် အောက်ပါအတိုင်း ဖြစ်ပါတယ်။   

```bash
class DiagramScene(QGraphicsScene):$
M-BM- M-BM- M-BM- M-BM- InsertItem, InsertLine, InsertText, MoveItemM-BM-  = range(4)$
M-BM- M-BM- $
M-BM- M-BM- M-BM- M-BM- itemInserted = pyqtSignal(DiagramItem)$
M-BM- M-BM- $
M-BM- M-BM- M-BM- M-BM- textInserted = pyqtSignal(QGraphicsTextItem)$
M-BM- M-BM- $
M-BM- M-BM- M-BM- M-BM- itemSelected = pyqtSignal(QGraphicsItem)$
M-BM- M-BM- $
M-BM- M-BM- M-BM- M-BM- def __init__(self, itemMenu, parent=None):$
M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- super(DiagramScene, self).__init__(parent)$
M-BM- M-BM- $
M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- self.myItemMenu = itemMenu$
M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- self.myMode = self.MoveItem$
M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- self.myItemType = DiagramItem.Step$
M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- self.line = None$
M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- self.textItem = None$
M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- self.myItemColor = Qt.white$
M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- self.myTextColor = Qt.black$
M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- self.myLineColor = Qt.black$
M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- M-BM- self.myFont = QFont()$
M-BM- M-BM- $
```

ဒီလိုပြဿနာက လွယ်မလိုလိုနဲ့ အတွေ့အကြုံမရှိရင် မလိုအပ်ပဲနဲ့ အချိန်အကြာကြီး ယူပြီး ဖြေရှင်းရတတ်ပါတယ်။  
ဖြေရှင်းပုံ ဖြေရှင်းနည်းက အမျိုးမျိုး ရှိပေမဲ့ ဒီနေ့တော့ Linux OS ရဲ့ အသုံးဝင်တဲ့ cat နဲ့ sed command ၂ခုကို သုံးပြီး ဖြေရှင်းပြပါမယ်။  
အရင်ဆုံး invisible characters "M-BM-" ကို ရိုက်ထည့်ထားတဲ့ cosine, sine တွက်ပေးတဲ့ Python ပရိုဂရမ်ကို ပုံမှန်အတိုင်း  
cat command နဲ့ ရိုက်ကြည့်ရင် အောက်ပါအတိုင်း မြင်ရပါလိမ့်မယ်။  

```bash
$ cat cosine-sine.py
import sys
from math import cos, sin, radians

#      <--- Invisible characters! 

input_radians = float(sys.argv[1])

def calc_cos_sine(r):
    print("Cosine of radians ", input_radians, ":", cos(radians (r)))
    print("Sine of radians ", input_radians, ":", sin(radians (r)))

calc_cos_sine(input_radians)
```

အဲဒီ ပရိုဂရမ်ကို run ကြည့်ရင်တော့ အောက်ပါအတိုင်း error ပေးပါလိမ့်မယ်။  

```bash
$ python ./cosine-sine.py 
  File "./cosine-sine.py", line 9
        print("Cosine of radians ", input_radians, ":", cos(radians (r)))
            ^
SyntaxError: invalid character in identifier
```
မမြင်ရတဲ့ စာလုံးတွေကိုပါ python က interpret လုပ်ဖို့ ကြိုးစားတာကြောင့် ပေးတဲ့ error ဖြစ်ပါတယ်။  
မမြင်ရတဲ့ စာလုံးတွေကို လွယ်လွယ်နဲ့ ကြည့်လို့ ရတာကတော့ cat command ကို  
-A (--show-all) သို့မဟုတ် -v (--show-nonprinting) option တွေကို သုံးပြီးတော့  
ကြည့်နိုင်ပါတယ်။ cosine-sine.py ပရိုဂရမ်ကို cat -A နဲ ရိုက်ခိုင်းတဲ့အခါမှာတော့ အောက်ပါအတိုင်း M-BM- စာလုံးတွေကို ရိုက်ပြပေးပါလိမ့်မယ်။  

```bash
$ cat -A ./cosine-sine.py 
import sys$
from math import cos, sin, radians$
$
#M-BM- M-BM- M-BM- M-BM- M-BM-  <--- Invisible characters! $
$
input_radians = float(sys.argv[1])$
$
def calc_cos_sine(r):$
M-BM- M-BM- M-BM- M-BM- print("Cosine of radians ", input_radians, ":", cos(radians (r)))$
    print("Sine of radians ", input_radians, ":", sin(radians (r)))$
$
calc_cos_sine(input_radians)$
```

ဒီနေရာမှာ ပရိုဂရမ် run လို့ မရအောင်ဒုက္ခပေးနေတဲ့ -M-BM- စာလုံးတွေက ASCII byte sequence နဲ့ ပြောရရင် 0xc2 0xa0 နံပါတ်တွေ ဖြစ်ပါတယ်။  
Unicode (UTF-8) နဲ့ပြောရင်တော့ U+00A0 (a non-breaking space character) ဖြစ်ပါတယ်။ အတိုကောက်အနေနဲ့ NBSP လို့လဲ သုံးကြပါတယ်။  
ကောင်းပါပြီ။ အဲဒီ ပရိုဂရမ်ထဲက M-BM- စာလုံးတွေကို ဘယ်လိုဖယ်ကြမလဲ။  
Linux ရဲ့ powerful command တစ်ခုဖြစ်တဲ့ sed command ကို သုံးပြီး M-BM- စာလုံးတွေအားလုံးကို ဘာမှမရှိတဲ့ စာလုံးနဲ့ အစားထိုးခိုင်းပြီး ဖျက်ပစ်လို့ ရပါတယ်။  

```bash
cat -v ./cosine-sine.py | sed s/M-BM-//g > ./cosine-sine-clean.py
```
ဒီနေရာမှ သတိထားစေချင်တာက -A option ကို မသုံးမိစေပါနဲ့။ ဘာ့ကြောင့်ဆိုရင် -A option ဆိုရင် စာကြောင်းအဆုံးတွေကိုပါ $ သင်္ကေတနဲ့ ရိုက်ပြတော့  
အဲဒီ $ သင်္ကေတတွေကိုပါ cosine-sine-clean.py ဆိုတဲ့ ဖိုင်ထဲမှာ သိမ်းပေးမှာစိုးလို့ပါ။ အဲဒါကြောင့် မမြင်ရတဲ့ စာလုံးတွေကိုပဲ ရိုက်ပြပေးတဲ့ -v option ကိုပဲ သုံးပါ။  

ဖိုင်အသစ်အဖြစ် သိမ်းထားတဲ့ ./cosine-sine-clean.py ပရိုဂရမ်ကို cat -A နဲ့ ရိုက်ကြည့်ရင် M-BM- စာလုံးတွေ မရှိတော့တာကို တွေ့ရပါလိမ့်မယ်။  

```bash
```

clean လုပ်ထားပြီးသား python ပရိုဂရမ်ကို run လို့လည်း ရပါပြီ။  

```bash

```


