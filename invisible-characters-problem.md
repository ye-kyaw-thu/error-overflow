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
(py3.6.2) lar@lar-air:~/experiment/pyqt/example/paint-draw/diagramscene/M-BM-problem$ cat cosine-sine.py
import sys
from math import cos, sin, radians

#      <--- Invisible characters! 

input_radians = float(sys.argv[1])

def calc_cos_sine(r):
    print("Cosine of radians ", input_radians, ":", cos(radians (r)))
    print("Sine of radians ", input_radians, ":", sin(radians (r)))

calc_cos_sine(input_radians)
```



