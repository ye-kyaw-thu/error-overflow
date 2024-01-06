# Machine Translation with ChatGPT Log

ChatGPT ရဲ့ machine translation က Google Translate ထက် သာတယ်ဆိုပြီး ရေးထားတဲ့ post တွေကို ဖတ်ဖူးတယ်။   
စာပိုဒ်ကိုလည်း ဘာသာပြန်ခိုင်းလို့ ရတယ် ဆိုပြီး ညွှန်းကြတယ်။ ကိုယ်တိုင်လည်း ChatGPT ရဲ့ လုပ်ပေးနိုင်တာတွေကို ကောင်းကောင်းနားလည်တယ်။   
သို့သော် လက်တွေ့ စာကြောင်းတွေအများကြီးကို ဘာသာပြန်ခိုင်းပြီးတော့ parallel corpus ဆောက်ကြည့်တဲ့အခါမှာတော့ တွေ့ရတဲ့ အခက်အခဲတွေက အများကြီးပါပဲ။  
အားလုံးကို ရှင်းပြဖို့ ခက်ပေမဲ့ တချို့အမှားတွေကိုတော့ ဒီနေရာမှာ log လုပ်ထားမယ်။ နောက်ပိုင်း လိုအပ်တဲ့အခါမှာ ရှင်းပြနိုင်အောင်လို့ ...   

## Error-1
## Prompt

ရှေ့မှာ လည်း လုပ်စေချင်တဲ့ ပုံစံကို prompt နဲ့ရှင်းပြထားပြီးသား၊ အဆင်ပြေပြေနဲ့ ဘာသာပြန်နေပြီးတော့ ၁၀ခေါက်လောက်လည်း ဘာ instruction မှာ ထပ်မပေးတော့ပဲ အင်္ဂလိပ်စာကြောင်းကိုပဲ prompt အနေနဲ့ ပေးတဲ့အခါမှာ ဖြစ်တတ်တဲ့အမှားမျိုး။ သေသေချာချာ မကြည့်ပဲ copy/paste လုပ်မိရင်တော့ လွဲပြီ။  

```
You walk your dog every day for five to ten minutes .
You were advised to follow lifestyle modifications to control your diabetes , but you are not very compliant with this .
What is diabetic retinopathy ?
Will my children get it ?
Can you cure this condition ?
Why did I get it ?
Will I go blind ?
How does alcohol or smoking affect the eyes ?
This is a condition in which your longstanding high blood sugar condition has now affected your eyes .
It has caused damage to the small blood vessels at the back of your eyes .
Swelling of blood vessels ( blow out , microaneurysm )
Small leaks of fluid from damaged blood vessels : exudates ( hard or soft ) 
Small bleeds ( dot and blot haemorrhage )
If this is left untreated the damage may progress to more severe problems like losing your vision .
The majority of people with diabetic retinopathy do not lose their vision .
However , without treatment , diabetic retinopathy can become worse and lead to visual problems or even blindness .
But if you follow our advice , the chances of you losing your vision are very low .
You need to control your blood sugar levels very well , as advised by the diabetic team .
We will also refer you to a diabetic nurse .
Have regular eye checks so that if there are any problems you can start treatment as soon as possible .
We will refer you to an ophthalmologist .
Control and monitor your blood pressure .
We will measure your blood pressure and if required we will start you on some medication .
Smoking causes spasm of the small vessels at the back of your eye and compromises the blood flow to eye .
This may increase the risk of developing diabetic complications of your eye .
```

## Reply

```
Diabetic retinopathy is a condition where your longstanding high blood sugar condition has now affected your eyes.|||ภาวะแทรกซ้อนของเบาหวานที่จอประสาทตาคือสภาวะที่ภาวะน้ำตาลในเลือดสูงของคุณที่มีมายาวนานได้ส่งผลกระทบต่อดวงตาของคุณ
It has caused damage to the small blood vessels at the back of your eyes.|||สภาวะนี้ได้ทำให้เส้นเลือดขนาดเล็กที่ด้านหลังของดวงตาของคุณเสียหาย
Swelling of blood vessels (blow out, microaneurysm)|||การบวมของเส้นเลือด (การแตก, การเกิดลิ่มเลือดขนาดเล็ก)
Small leaks of fluid from damaged blood vessels: exudates (hard or soft)|||รั่วของของเหลวจากเส้นเลือดที่เสียหาย: การสะสมของของเหลว (แข็งหรือนุ่ม)
Small bleeds (dot and blot hemorrhage)|||เลือดออกเล็กน้อย (เลือดออกรูปจุดและแผลเปื้อน)
If left untreated, the damage may progress to more severe problems like losing your vision.|||ถ้าไม่ได้รับการรักษา ความเสียหายอาจลุกลามไปสู่ปัญหาที่รุนแรงขึ้น เช่น การสูญเสียการมองเห็น
The majority of people with diabetic retinopathy do not lose their vision.|||ส่วนใหญ่ของผู้ป่วยที่มีภาวะแทรกซ้อนของเบาหวานที่จอประสาทตาไม่สูญเสียการมองเห็น
However, without treatment, diabetic retinopathy can worsen, leading to visual problems or even blindness.|||อย่างไรก็ตาม หากไม่ได้รับการรักษา ภาวะแทรกซ้อนของเบาหวานที่จอประสาทตาอาจแย่ลง นำไปสู่ปัญหาทางการมองเห็นหรือแม้กระทั่งตาบอด
But if you follow our advice, the chances of you losing your vision are very low.|||แต่ถ้าคุณปฏิบัติตามคำแนะนำของเรา โอกาสที่คุณจะสูญเสียการมองเห็นนั้นต่ำมาก
You need to control your blood sugar levels very well, as advised by the diabetic team.|||คุณต้องควบคุมระดับน้ำตาลในเลือดของคุณได้ดีมาก ตามคำแนะนำของทีมดูแลผู้ป่วยเบาหวาน
We will also refer you to a diabetic nurse.|||เรายังจะส่งต่อคุณไปหาพยาบาลที่เชี่ยวชาญเกี่ยวกับเบาหวาน
Have regular eye checks so that if there are any problems, you can start treatment as soon as possible.|||มีการตร

วจตาเป็นประจำเพื่อว่าหากมีปัญหาใดๆ คุณสามารถเริ่มการรักษาได้โดยเร็วที่สุด
We will refer you to an ophthalmologist.|||เราจะส่งต่อคุณไปหาจักษุแพทย์
Control and monitor your blood pressure.|||ควบคุมและติดตามความดันโลหิตของคุณ
We will measure your blood pressure and if required, we will start you on some medication.|||เราจะวัดความดันโลหิตของคุณ และถ้าจำเป็น เราจะเริ่มให้ยากับคุณ
Smoking causes spasm of the small vessels at the back of your eye and compromises blood flow to the eye.|||การสูบบุหรี่ทำให้เส้นเลือดขนาดเล็กที่ด้านหลังของดวงตาของคุณหดตัวและลดการไหลเวียนของเลือดไปยังดวงตา
This may increase the risk of developing diabetic complications of your eye.|||สิ่งนี้อาจเพิ่มความเสี่ยงของการเกิดภาวะแทรกซ้อนของเบาหวานที่ดวงตาของคุณ
```

## Error-2

ဒီလိုမျိုးအမှားက Google Translate ကို သုံးရင်လည်း ကြုံရတတ်ပါတယ်။  
တချို့နေရာတွေမှာ စာကြောင်းမပြီးခင် line break ဖြစ်သွားတဲ့ error မျိုးပါ။  

```
The majority of people with diabetic retinopathy do not lose their vision.|||ส่วนใหญ่ของผู้ป่วยที่มีโรคจอประสาทตาเบาหวานไม่สูญเสียการมองเห็น
However, without treatment, diabetic retinopathy can become worse and lead to visual problems or even blindness.|||อย่างไรก็ตาม หากไม่ได้รับการรักษา โรคจอประสาทตาเบาหวานสามารถทำให้รุนแรงขึ้นและนำไปสู่ปัญหา

การมองเห็นหรือแม้แต่การตาบอด
But if you follow our advice, the chances of you losing your vision are very low.|||แต่ถ้าคุณปฏิบัติตามคำแนะนำของเรา โอกาสที่คุณจะสูญเสียการมองเห็นนั้นต่ำมาก
You need to control your blood sugar levels very well, as advised by the diabetic team.|||คุณจำเป็นต้องควบคุมระดับน้ำตาลในเลือดของคุณอย่างดีตามคำแนะนำของทีมดูแลเบาหวาน
```

## Error-3

time limite ကြောင့်လည်း ဖြစ်နိုင်တယ်။ တချို့ reply တွေမှာက ခိုင်းထားတဲ့ စာကြောင်း အကုန်မပြီးပဲ ဖြတ်ချလိုက်တာမျိုးလည်း ရှိတယ်။ အောက်ပါဥပမာ လိုမျိုး ...  

```
...
...
...
Depression (low mood, loss of interest in daily activities)|||ภาวะซึมเศร้า (อารมณ์ต่ำ, สูญเสียความสนใจในกิจกรรมประจำวัน)
Polymyalgia rheumatica (weakness of muscles of the big joints i.e. shoulder pain and girdle muscles)|||โพลิมัยอัลเจียรูมาติกา (ความอ่อนแอของกล้ามเนื้อของข้อต่อใหญ่ เช่น ปวดบ่าและกล้ามเนื้อเอว)
Connective tissue disease (e.g. SLE, RA. There will be polyarthritis, symmetrical or asymmetrical)|||โรคเนื้อเยื่อเกี่ยวพัน (เช่น โรคลูปัส, โรคข้ออักเสบรูมาตอยด์ จะมีการอักเสบของข้อต่อหลายข้อ, ความสมมาตรหรือไม่สมมาตร)
Chronic renal failure (anuria, anaemia, tiredness)|||โรคไตเรื้อรัง (ไม่มีปัสสาวะ, โลหิตจาง, อ่อนเพลีย)
Myeloencephalitis (confusion, headaches)|||โรคอักเสบของไขสันหลังและสมอง (สับสน, ปวดหัว)
Shift workers (night shifts, poor sleep)|||ผู้ทำงานกะ (ก
```

## Error-4
## Prompt

```
System: You are a machine translation system. Output Format: "Source_Language_Sentence|||Target_Language_Sentence" and no blank line each sentence translation. User: Please provide the Thai translation for the following sentences. No explanation!:

The fact that you are anaemic tells us that your kidneys have not been working properly for a long time , which means that there is ongoing damage to your kidneys .
Therefore , the anaemia is because of the kidneys which are not functioning properly .
It will progressively get worse , but there are a few things we can do to try and slow down the damage .
I was wondering what the cause could be of the damage to your kidneys .
Can I ask you a few questions ?
Drug history ? NSAIDs , ACE inhibitor , antibiotics etc .
Renal stones ?
Family history of kidney disease or polycystic kidney disease ?
Urinary tract infections ( pyelonephritis ) ?
Diabetes mellitus or hypertension ?
Malignancy ?
Autoimmune ( SLE )
Ask for symptoms of anaemia ( light-headedness , dizziness , tiredness )
From what you have told me , it is difficult to know the cause .
We now need to perform some blood tests to find out what could have been the cause of this .
We will also perform a scan of your kidneys and check the blood pressure and blood sugar levels .
There are a few things that might need to be addressed in order to cope better with this condition :
How is your diet ?
Do you do regular exercise ?
Please advise the patient accordingly .
```

## Reply

လိုချင်တာက Source|||Target, ChatGPT4 ကနေ reply လုပ်ပြီးထွက်လာတာက Target|||Source ဆိုတဲ့ အမှားမျိုး ...   
မင်း ငါပြောနေတာကို တကယ်ကော နားလည်ရဲ့လား ChatGPT? :)  

```
ความจริงที่คุณเป็นโรคโลหิตจางบอกเราว่าไตของคุณทำงานไม่ดีมานานแล้ว ซึ่งหมายความว่ามีความเสียหายต่อไตของคุณอย่างต่อเนื่อง|||The fact that you are anaemic tells us that your kidneys have not been working properly for a long time, which means that there is ongoing damage to your kidneys.
ดังนั้น โรคโลหิตจางเกิดขึ้นเพราะไตที่ทำงานไม่ดี|||Therefore, the anaemia is because of the kidneys which are not functioning properly.
มันจะแย่ลงเรื่อยๆ แต่มีสิ่งหนึ่งที่เราทำได้เพื่อพยายามชะลอความเสียหาย|||It will progressively get worse, but there are a few things we can do to try and slow down the damage.
ฉันสงสัยว่าสาเหตุของความเสียหายที่ไตของคุณอาจเกิดจากอะไร|||I was wondering what the cause could be of the damage to your kidneys.
ฉันขอถามคุณสองสามคำถามได้ไหม?|||Can I ask you a few questions?
ประวัติการใช้ยา? ยาแก้ปวดอักเสบ, ยายับยั้ง ACE, ยาปฏิชีวนะ เป็นต้น|||Drug history? NSAIDs, ACE inhibitor, antibiotics etc.
มีนิ่วในไตหรือไม่?|||Renal stones?
ประวัติครอบครัวเป็นโรคไตหรือโรคไตพองน้ำ?|||Family history of kidney disease or polycystic kidney disease?
การติดเชื้อทางเดินปัสสาวะ (ไตอักเสบ)?|||Urinary tract infections (pyelonephritis)?
เป็นโรคเบาหวานหรือความดันโลหิตสูงหรือไม่?|||Diabetes mellitus or hypertension?
มะเร็ง?|||Malignancy?
โรคภูมิต้านทาน (SLE)|||Autoimmune (SLE)
ถามอาการของโรคโลหิตจาง (วิงเวียนศีรษะ, มึนงง, อ่อนเพลีย)|||Ask for symptoms of anaemia (light-headedness, dizziness, tiredness)
จากสิ่งที่คุณบอกผมมา มันยากที่จะรู้สาเหตุ|||From what you have told me, it is difficult to know the cause.
ตอนนี้เราต้องทำการตรวจเลือดเพื่อหาสาเหตุที่อาจเป็นไปได้|||We now need to perform some blood tests to find out what could have been the cause of this.
เราจะทำการสแกนไตของคุณและตรวจวัดความดันโลหิตและระดับน้ำตาลในเลือด|||We will also perform a scan of your kidneys and check the blood pressure and blood sugar levels.
มีสิ่งหนึ่งที่อาจต้องจัดการเพื่อให้รับมือกับสภ
```

## Error-5
## Prompt
```
Indications of surgical management if all these criteria are fulfilled
BMI ≥ 40 or ≥ 35 with significant co-morbidities that could improve with weight reduction
```

အထက်ပါ နှစ်ကြောင်းကို၊ ထိုင်းဘာသာဘက် ဘာသာပြန်တဲ့အခါမှာ တစ်ကြောင်းတည်းပေါင်းလိုက်တဲ့ ပြဿနာ ...  

```
Indications of surgical management if all these criteria are fulfilled: BMI ≥ 40 or ≥ 35 with significant co-morbidities that could improve with weight reduction.|||ตัวชี้วัดของการจัดการทางการผ่าตัดหากเงื่อนไขเหล่านี้ได้รับการเติมเต็ม: BMI ≥ 40 หรือ ≥ 35 พร้อมกับโรคร่วมที่สำคัญซึ่งสามารถปรับปรุงได้ด้วยการลดน้ำหนัก
```

## Error-6

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

```

```

```



