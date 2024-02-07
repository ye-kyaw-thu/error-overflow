# Log File for WER calculation for my2thai

The log file for WER calculation for my2thai, medical domain.  

## Check the Files

Check the filesize:  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ wc *
   32259   368780  3887603 1_baseline.txt
   32259   344017  3604377 2_finetuned_tagged.txt
   32259   360512  3791401 3_finetuned-notagged.txt
   96777  1073309 11283381 total
(base) ye@lst-gpu-3090:~/exp/wer-calc$
```

check the file content of 1_baseline.txt:  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ head -n 11 ./1_baseline.txt
source: translate Myanmar to Thai: ဆ ရာ ဝန် နဲ့ အ သေး စိတ် ဆွေး နွေး လိုက် ကောင်း ပါ တယ် ရှင်
target: รอ คุย รายละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ
prediction:  รอ คุย รายละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ โดย ตรง นะ คะ คุณ หมอ ปรึกษา คุณ หมอ

source: translate Myanmar to Thai: ရော ဂါ ကု သ မှာ ကို လက် ခံ ပါ တယ် ဒေါက် တာ
target: ยินยอม เข้า รับ การ รักษา คะ
prediction:  ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า

source: translate Myanmar to Thai: ဟုတ် တယ် ။ ဓမ္မ တာ နာ ကျင် ကိုက် ခဲ မှု က ရိုး ရိုး ရှင်း ရှင်း စ တင် တာ ဖြစ် တတ် တယ် ၊ ဒါ ပေ မ ယ့် မင်း ရဲ့ အ ခြေ အ နေ က ဓမ္မ တာ မ လာ ခင် စိတ် ဖိ စီး မှု လို့ ခေါ် တယ် ပြီး ရင် နာ ကျင် မှု တွေ ဖြစ် တယ် သက် တော င့် သက် သာ မ ရှိ တဲ့ ဖြစ် တဲ့ ရာ သီ လာ ခြင်း ကို ဒစ် မန် နို ရီး ယား လို့ ခေါ် တယ် ။
target: ครับ มัน เพิ่ง เริ่ม มี อาการ ปวด ประจำ เดือน แต่ ใน กรณี ของ คุณ เรียก ว่า ความ เครียด ก่อน มี ประจำ เดือน และ ช่วง เวลา ที่ มา พร้อม กับ ความ เจ็บปวด และ ความ รู้สึก ไม่ สบาย นั้น เรียก ว่า ประจำ เดือน ดิมัดโนลียา
prediction:  ครับ มัน เพิ่ง เริ่ม มี อาการ ปวด ประจํา เดือน แต่ ใน กรณี ของ คุณ เรียก ว่า ความ เครียด ก่อน มี ประจํา เดือน และ ช่วง เวลา ที่ มา พร้อม กับ ความ เจ็บปวด และ
(base) ye@lst-gpu-3090:~/exp/wer-calc$
```

Check the file content of ./2_finetuned_tagged.txt:  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ head -n 11 ./2_finetuned_tagged.txt
source: translate Myanmar to Thai: ဆ ရာ ဝန် နဲ့ အ သေး စိတ် ဆွေး နွေး လိုက် ကောင်း ပါ တယ် ရှင်
target: รอ คุย รายละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ
prediction:  รอ คุย รายละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ รอ คุย กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ

source: translate Myanmar to Thai: ရော ဂါ ကု သ မှာ ကို လက် ခံ ပါ တယ် ဒေါက် တာ
target: ยินยอม เข้า รับ การ รักษา คะ
prediction:  ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า รับ การ รักษา คะ

source: translate Myanmar to Thai: ဟုတ် တယ် ။ ဓမ္မ တာ နာ ကျင် ကိုက် ခဲ မှု က ရိုး ရိုး ရှင်း ရှင်း စ တင် တာ ဖြစ် တတ် တယ် ၊ ဒါ ပေ မ ယ့် မင်း ရဲ့ အ ခြေ အ နေ က ဓမ္မ တာ မ လာ ခင် စိတ် ဖိ စီး မှု လို့ ခေါ် တယ် ပြီး ရင် နာ ကျင် မှု တွေ ဖြစ် တယ် သက် တော င့် သက် သာ မ ရှိ တဲ့ ဖြစ် တဲ့ ရာ သီ လာ ခြင်း ကို ဒစ် မန် နို ရီး ယား လို့ ခေါ် တယ် ။
target: ครับ มัน เพิ่ง เริ่ม มี อาการ ปวด ประจำ เดือน แต่ ใน กรณี ของ คุณ เรียก ว่า ความ เครียด ก่อน มี ประจำ เดือน และ ช่วง เวลา ที่ มา พร้อม กับ ความ เจ็บปวด และ ความ รู้สึก ไม่ สบาย นั้น เรียก ว่า ประจำ เดือน ดิมัดโนลียา
prediction:  ครับ มัน เพิ่ง เริ่ม มี อาการ ปวด ประจํา เดือน แต่ ใน กรณี ของ คุณ เรียก ว่า ความ เครียด ก่อน มี ประจํา เดือน และ ช่วง เวลา ที่ มา พร้อม กับ ความ รู้สึก ไม่ สบาย
(base) ye@lst-gpu-3090:~/exp/wer-calc$
```

Check the file content of 3_finetuned-notagged.txt:  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ head -n 11 ./3_finetuned-notagged.txt
source: translate Myanmar to Thai: ဆ ရာ ဝန် နဲ့ အ သေး စိတ် ဆွေး နွေး လိုက် ကောင်း ပါ တယ် ရှင်
target: รอ คุย รายละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ
prediction:  รอ คุย รายละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ โดย ละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ นะ คะ

source: translate Myanmar to Thai: ရော ဂါ ကု သ မှာ ကို လက် ခံ ပါ တယ် ဒေါက် တာ
target: ยินยอม เข้า รับ การ รักษา คะ
prediction:  ยินยอม ทํา การ รักษา ตาม คํา สั่ง แพทย์

source: translate Myanmar to Thai: ဟုတ် တယ် ။ ဓမ္မ တာ နာ ကျင် ကိုက် ခဲ မှု က ရိုး ရိုး ရှင်း ရှင်း စ တင် တာ ဖြစ် တတ် တယ် ၊ ဒါ ပေ မ ယ့် မင်း ရဲ့ အ ခြေ အ နေ က ဓမ္မ တာ မ လာ ခင် စိတ် ဖိ စီး မှု လို့ ခေါ် တယ် ပြီး ရင် နာ ကျင် မှု တွေ ဖြစ် တယ် သက် တော င့် သက် သာ မ ရှိ တဲ့ ဖြစ် တဲ့ ရာ သီ လာ ခြင်း ကို ဒစ် မန် နို ရီး ယား လို့ ခေါ် တယ် ။
target: ครับ มัน เพิ่ง เริ่ม มี อาการ ปวด ประจำ เดือน แต่ ใน กรณี ของ คุณ เรียก ว่า ความ เครียด ก่อน มี ประจำ เดือน และ ช่วง เวลา ที่ มา พร้อม กับ ความ เจ็บปวด และ ความ รู้สึก ไม่ สบาย นั้น เรียก ว่า ประจำ เดือน ดิมัดโนลียา
prediction:  ครับ มัน เพิ่ง เริ่ม มี อาการ ปวด ประจํา เดือน แต่ ใน กรณี ของ คุณ เรียก ว่า ความ เครียด ก่อน มี ประจํา เดือน และ ช่วง เวลา ที่ มา พร้อม กับ ความ รู้สึก ไม่ สบาย
(base) ye@lst-gpu-3090:~/exp/wer-calc$
```

## Write a Python Code

Python script name: extract_src_ref_hyp.py  

```python
"""

for extraction of source, target (i.e. reference) and prediction (i.e. hypothesis).
Written by Ye Kyaw Thu, LU Lab., Myanmar.
Last updated: 7 Feb 2024

How to run:
$ python ./extract_src_ref_hyp.py --help
$ python ./extract_src_ref_hyp.py --input ./1_baseline.txt --output baseline

Input file format:
$ head -n 7 ./1_baseline.txt
source: translate Myanmar to Thai: ဆ ရာ ဝန် နဲ့ အ သေး စိတ် ဆွေး နွေး လိုက် ကောင်း ပါ တယ် ရှင်
target: รอ คุย รายละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ
prediction:  รอ คุย รายละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ โดย ตรง นะ คะ คุณ หมอ ปรึกษา คุณ หมอ

source: translate Myanmar to Thai: ရော ဂါ ကု သ မှာ ကို လက် ခံ ပါ တယ် ဒေါက် တာ
target: ยินยอม เข้า รับ การ รักษา คะ
prediction:  ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า


"""

import argparse
import os

def extract_sentences(input_file, output_folder, src_filename, tgt_filename, hyp_filename):
    with open(input_file, 'r', encoding='utf-8') as f:
        lines = f.readlines()

    # Initialize lists to hold the extracted sentences
    sources = []
    targets = []
    predictions = []

    # Extract sentences
    for line in lines:
        if line.startswith("source: translate Myanmar to Thai: "):
            sources.append(line.replace("source: translate Myanmar to Thai: ", "").strip())
        elif line.startswith("target: "):
            targets.append(line.replace("target: ", "").strip())
        elif line.startswith("prediction: "):
            predictions.append(line.replace("prediction: ", "").strip())

    # Save the extracted sentences
    if not os.path.exists(output_folder):
        os.makedirs(output_folder)

    with open(os.path.join(output_folder, src_filename), 'w', encoding='utf-8') as src_file:
        src_file.write('\n'.join(sources) + '\n')

    with open(os.path.join(output_folder, tgt_filename), 'w', encoding='utf-8') as tgt_file:
        tgt_file.write('\n'.join(targets) + '\n')

    with open(os.path.join(output_folder, hyp_filename), 'w', encoding='utf-8') as hyp_file:
        hyp_file.write('\n'.join(predictions) + '\n')

def main():
    parser = argparse.ArgumentParser(description="Extract source, target, and prediction sentences from translation files.")
    parser.add_argument("-i", "--input", required=True, help="Input file path.")
    parser.add_argument("-o", "--output", required=True, help="Output folder path.")

    args = parser.parse_args()

    input_file = args.input
    output_folder = args.output

    # Determine the file type and set the output filenames accordingly
    if "baseline" in input_file:
        extract_sentences(input_file, output_folder, "src_baseline.txt", "ref_baseline.txt", "hyp_baseline.txt")
    elif "finetuned_tagged" in input_file:
        extract_sentences(input_file, output_folder, "src_ft_tag.txt", "ref_ft_tag.txt", "hyp_ft_tag.txt")
    elif "finetuned-notagged" in input_file:
        extract_sentences(input_file, output_folder, "src_ft_notag.txt", "ref_ft_notag.txt", "hyp_ft_notag.txt")
    else:
        print("Unrecognized file type. Please ensure the file name contains either 'baseline', 'finetuned_tagged', or 'finetuned-notagged'.")

if __name__ == "__main__":
    main()

```

## Check --help

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ python ./extract_src_ref_hyp.py --help
usage: extract_src_ref_hyp.py [-h] -i INPUT -o OUTPUT

Extract source, target, and prediction sentences from translation files.

optional arguments:
  -h, --help            show this help message and exit
  -i INPUT, --input INPUT
                        Input file path.
  -o OUTPUT, --output OUTPUT
                        Output folder path.
```

## Cut Source, Target and Prediction


```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ time python ./extract_src_ref_hyp.py --input ./1_baseline.txt --output baseline

real    0m0.036s
user    0m0.032s
sys     0m0.004s
```

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ time python ./extract_src_ref_hyp.py --input ./2_finetuned_tagged.txt --output ft_tag

real    0m0.034s
user    0m0.023s
sys     0m0.011s
```

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ time python ./extract_src_ref_hyp.py --input ./3_finetuned-notagged.txt --output ft_no_tag

real    0m0.036s
user    0m0.032s
sys     0m0.004s
```

## Check the Output Folders and Files

Three new folders as follows:  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ ls
1_baseline.txt          3_finetuned-notagged.txt  extract.py  ft_tag
2_finetuned_tagged.txt  baseline                  ft_no_tag
```

Check the ./baseline/ folder:  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ tree ./baseline/
./baseline/
├── hyp_baseline.txt
├── ref_baseline.txt
└── src_baseline.txt

0 directories, 3 files
```

Check the ./ft_tag/ folder:  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ tree ./ft_tag/
./ft_tag/
├── hyp_ft_tag.txt
├── ref_ft_tag.txt
└── src_ft_tag.txt

0 directories, 3 files
```

Check the ./ft_no_tag/ folder:  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ tree ./ft_no_tag/
./ft_no_tag/
├── hyp_ft_notag.txt
├── ref_ft_notag.txt
└── src_ft_notag.txt

0 directories, 3 files
```

Check no. of sentences:  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ wc ./baseline/*
   8063  155222 1802632 ./baseline/hyp_baseline.txt
   8063   56900  661580 ./baseline/ref_baseline.txt
   8063  100145  930383 ./baseline/src_baseline.txt
  24189  312267 3394595 total
```

Check no. of sentences:  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ wc ./ft_tag/*
   8063  130459 1519421 ./ft_tag/hyp_ft_tag.txt
   8063   56900  661580 ./ft_tag/ref_ft_tag.txt
   8063  100145  930383 ./ft_tag/src_ft_tag.txt
  24189  287504 3111384 total
```

Check no. of sentences:  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ wc ./ft_no_tag/*
   8063  146954 1706467 ./ft_no_tag/hyp_ft_notag.txt
   8063   56900  661580 ./ft_no_tag/ref_ft_notag.txt
   8063  100145  930383 ./ft_no_tag/src_ft_notag.txt
  24189  303999 3298430 total
```

Check the extracted file content for baseline approach:  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ cd baseline/
(base) ye@lst-gpu-3090:~/exp/wer-calc/baseline$ head *
==> hyp_baseline.txt <==
รอ คุย รายละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ โดย ตรง นะ คะ คุณ หมอ ปรึกษา คุณ หมอ
ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า
ครับ มัน เพิ่ง เริ่ม มี อาการ ปวด ประจํา เดือน แต่ ใน กรณี ของ คุณ เรียก ว่า ความ เครียด ก่อน มี ประจํา เดือน และ ช่วง เวลา ที่ มา พร้อม กับ ความ เจ็บปวด และ
ตา แดง ตา ของ ฉัน แดง ตา ตา ตา ตา ตา
พี่ หมอ อยาก เห็น ว่า ข้าง ใน ฟัน มัน เป็น ยัง ไง คือ คือ พี่ หมอ คือ พี่ หมอ พี่ หมอ พี่ หมอ พี่ หมอ อยาก เห็น พี่ หมอ พี่ หมอ พี่ หมอ พี่ หมอ พี่
จาก ภาพ x- ray จาก ภาพ ray จาก ภาพ ray จาก ภาพ ray จาก ภาพ ray จาก
ยินยอม ครับ ยินยอม ยินยอม ยินยอม ยินยอม ยินยอม ยินยอม ยินยอม ยินยอม ยินยอม ยินยอม ยินยอม
และ ฉีด วัคซีน ป้องกัน โควิด ครับ และ ฉีด วัคซีน ครับ ครับ ครับ ครับ ครับ และ ฉีด วัคซีน ครับ ครับ ครับ ครับ ครับ ครับ ครับ ครับ ครับ ครับ ครับ
เดี๋ยว
น้อง ใช่ เจอ แบบ ใน รูป สี ใส ๆ น้อง ใช่ ไหม น้อง ใช่ ไหม น้อง ใช่ ไหม น้อง ใช่ ไหม น้อง ใช่ ไหม น้อง ใช่ ไหม น้อง ใช่ ไหม น้อง ใช่ ไหม น้อง ใช่ ไหม น้อง ใช่

==> ref_baseline.txt <==
รอ คุย รายละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ
ยินยอม เข้า รับ การ รักษา คะ
ครับ มัน เพิ่ง เริ่ม มี อาการ ปวด ประจำ เดือน แต่ ใน กรณี ของ คุณ เรียก ว่า ความ เครียด ก่อน มี ประจำ เดือน และ ช่วง เวลา ที่ มา พร้อม กับ ความ เจ็บปวด และ ความ รู้สึก ไม่ สบาย นั้น เรียก ว่า ประจำ เดือน ดิมัดโนลียา
ตา เป็น สี แดง
พี่ หมอ อยาก เห็น ว่า ข้าง ใน ฟัน มัน เป็น ยัง ไง
จาก ภาพ x- ray
ยินยอม
และ ฉีด วัคซีน ป้องกัน โควิด ครับ
เดี๋ยว film ซ้ำ ดู ตำแหน่ง หน่อย
น้อง ใช่ เจอ แบบ ใน รูป สี ใส ๆ

==> src_baseline.txt <==
ဆ ရာ ဝန် နဲ့ အ သေး စိတ် ဆွေး နွေး လိုက် ကောင်း ပါ တယ် ရှင်
ရော ဂါ ကု သ မှာ ကို လက် ခံ ပါ တယ် ဒေါက် တာ
ဟုတ် တယ် ။ ဓမ္မ တာ နာ ကျင် ကိုက် ခဲ မှု က ရိုး ရိုး ရှင်း ရှင်း စ တင် တာ ဖြစ် တတ် တယ် ၊ ဒါ ပေ မ ယ့် မင်း ရဲ့ အ ခြေ အ နေ က ဓမ္မ တာ မ လာ ခင် စိတ် ဖိ စီး မှု လို့ ခေါ် တယ် ပြီး ရင် နာ ကျင် မှု တွေ ဖြစ် တယ် သက် တော င့် သက် သာ မ ရှိ တဲ့ ဖြစ် တဲ့ ရာ သီ လာ ခြင်း ကို ဒစ် မန် နို ရီး ယား လို့ ခေါ် တယ် ။
မျက် လုံး တွေ က နီ နေ ခဲ့ တယ် ။
ဒေါက် တာ က လေ သွား အ ထဲ က အ ပိုင်း တွေ ဘယ် လို ဖြစ် နေ လဲ ဆို တာ သိ ချင် လို့
ဓါတ် ပုံ အ ရ တော့
လက် ခံ ပါ တယ် ဗျ
ဒါ့ အ ပြင် ကို ဗစ် ဆေး လည်း ထိုး သေး တယ် ဗျ ။
ဓာတ် မှန် ထဲ က အ နေ အ ထား ကို ပြန် ကြ ည့် ပါ ။
ပုံ ထဲ က လို မျိုး အ ရောင် ကြည် ကြည် မြင် လိုက် ရ သ လား ။
(base) ye@lst-gpu-3090:~/exp/wer-calc/baseline$
```

Check the extracted output files for the ft_tag approach:  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc/ft_tag$ head *
==> hyp_ft_tag.txt <==
รอ คุย รายละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ รอ คุย กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ
ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า รับ การ รักษา คะ
ครับ มัน เพิ่ง เริ่ม มี อาการ ปวด ประจํา เดือน แต่ ใน กรณี ของ คุณ เรียก ว่า ความ เครียด ก่อน มี ประจํา เดือน และ ช่วง เวลา ที่ มา พร้อม กับ ความ รู้สึก ไม่ สบาย
ตา แดง ตา ตา ตา มัว ตา ตา ตา ตา ตา ตา ตา ตา ตา ตา
พี่ หมอ อยาก เห็น ว่า ข้าง ใน ฟัน มัน เป็น ยัง ไง คือ พี่ หมอ คือ พี่ หมอ คือ พี่ หมอ พี่ หมอ พี่ หมอ คือ พี่ หมอ พี่ หมอ พี่ หมอ
จาก ภาพ x- ray จาก การ ตรวจ ร่างกาย
ยินยอม ครับ ยินยอม ครับ ยินยอม ครับ ยินยอม ครับ
และ ฉีด วัคซีน ป้องกัน โควิด ครับ และ ฉีด วัคซีน ครับ
เดี๋ยว
น้อง ใช่ เจอ แบบ ใน รูป สี ใส ๆ ใช่ ไหม ครับ ต้อง ใส่

==> ref_ft_tag.txt <==
รอ คุย รายละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ
ยินยอม เข้า รับ การ รักษา คะ
ครับ มัน เพิ่ง เริ่ม มี อาการ ปวด ประจำ เดือน แต่ ใน กรณี ของ คุณ เรียก ว่า ความ เครียด ก่อน มี ประจำ เดือน และ ช่วง เวลา ที่ มา พร้อม กับ ความ เจ็บปวด และ ความ รู้สึก ไม่ สบาย นั้น เรียก ว่า ประจำ เดือน ดิมัดโนลียา
ตา เป็น สี แดง
พี่ หมอ อยาก เห็น ว่า ข้าง ใน ฟัน มัน เป็น ยัง ไง
จาก ภาพ x- ray
ยินยอม
และ ฉีด วัคซีน ป้องกัน โควิด ครับ
เดี๋ยว film ซ้ำ ดู ตำแหน่ง หน่อย
น้อง ใช่ เจอ แบบ ใน รูป สี ใส ๆ

==> src_ft_tag.txt <==
ဆ ရာ ဝန် နဲ့ အ သေး စိတ် ဆွေး နွေး လိုက် ကောင်း ပါ တယ် ရှင်
ရော ဂါ ကု သ မှာ ကို လက် ခံ ပါ တယ် ဒေါက် တာ
ဟုတ် တယ် ။ ဓမ္မ တာ နာ ကျင် ကိုက် ခဲ မှု က ရိုး ရိုး ရှင်း ရှင်း စ တင် တာ ဖြစ် တတ် တယ် ၊ ဒါ ပေ မ ယ့် မင်း ရဲ့ အ ခြေ အ နေ က ဓမ္မ တာ မ လာ ခင် စိတ် ဖိ စီး မှု လို့ ခေါ် တယ် ပြီး ရင် နာ ကျင် မှု တွေ ဖြစ် တယ် သက် တော င့် သက် သာ မ ရှိ တဲ့ ဖြစ် တဲ့ ရာ သီ လာ ခြင်း ကို ဒစ် မန် နို ရီး ယား လို့ ခေါ် တယ် ။
မျက် လုံး တွေ က နီ နေ ခဲ့ တယ် ။
ဒေါက် တာ က လေ သွား အ ထဲ က အ ပိုင်း တွေ ဘယ် လို ဖြစ် နေ လဲ ဆို တာ သိ ချင် လို့
ဓါတ် ပုံ အ ရ တော့
လက် ခံ ပါ တယ် ဗျ
ဒါ့ အ ပြင် ကို ဗစ် ဆေး လည်း ထိုး သေး တယ် ဗျ ။
ဓာတ် မှန် ထဲ က အ နေ အ ထား ကို ပြန် ကြ ည့် ပါ ။
ပုံ ထဲ က လို မျိုး အ ရောင် ကြည် ကြည် မြင် လိုက် ရ သ လား ။
(base) ye@lst-gpu-3090:~/exp/wer-calc/ft_tag$
```

Check the extracted output files for the ft_no_tag approach:  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc/ft_no_tag$ head *
==> hyp_ft_notag.txt <==
รอ คุย รายละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ โดย ละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ นะ คะ
ยินยอม ทํา การ รักษา ตาม คํา สั่ง แพทย์
ครับ มัน เพิ่ง เริ่ม มี อาการ ปวด ประจํา เดือน แต่ ใน กรณี ของ คุณ เรียก ว่า ความ เครียด ก่อน มี ประจํา เดือน และ ช่วง เวลา ที่ มา พร้อม กับ ความ รู้สึก ไม่ สบาย
ตา แดง ด้วย ค่ะ ตา แดง ตา แดง ตา แดง ตา ของ ฉัน แดง ตา ตา ตา แดง ตา
พี่ หมอ อยาก เห็น ว่า ข้าง ใน ฟัน มัน เป็น ยัง ไง พี่ พี่ พี่ หมอ พี่ พี่ พี่ พี่ พี่ พี่ พี่ พี่ หมอ พี่ พี่ พี่ หมอ พี่ พี่ พี่
จาก ภาพ x- ray จาก การ ตรวจ ร่างกาย
ยินยอม ครับ ยินยอม ยินยอม ยินยอม ครับ ยินยอม ยินยอม ยินยอม ครับ ยินยอม ยินยอม ยินยอม ยินยอม ครับ ยิน
และ ฉีด วัคซีน ป้องกัน โควิด ครับ และ ฉีด วัคซีน ครับ ครับ และ ฉีด วัคซีน ครับ ครับ ครับ ครับ ครับ ครับ และ ฉีด วัคซีน ครับ ครับ ครับ ครับ ครับ ครับ
เดี๋ยว
น้อง ใช่ เจอ แบบ ใน รูป สี ใส ๆ ต้อง มอง เห็น ไหม ครับ น้อง ต้อง ใส่

==> ref_ft_notag.txt <==
รอ คุย รายละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ
ยินยอม เข้า รับ การ รักษา คะ
ครับ มัน เพิ่ง เริ่ม มี อาการ ปวด ประจำ เดือน แต่ ใน กรณี ของ คุณ เรียก ว่า ความ เครียด ก่อน มี ประจำ เดือน และ ช่วง เวลา ที่ มา พร้อม กับ ความ เจ็บปวด และ ความ รู้สึก ไม่ สบาย นั้น เรียก ว่า ประจำ เดือน ดิมัดโนลียา
ตา เป็น สี แดง
พี่ หมอ อยาก เห็น ว่า ข้าง ใน ฟัน มัน เป็น ยัง ไง
จาก ภาพ x- ray
ยินยอม
และ ฉีด วัคซีน ป้องกัน โควิด ครับ
เดี๋ยว film ซ้ำ ดู ตำแหน่ง หน่อย
น้อง ใช่ เจอ แบบ ใน รูป สี ใส ๆ

==> src_ft_notag.txt <==
ဆ ရာ ဝန် နဲ့ အ သေး စိတ် ဆွေး နွေး လိုက် ကောင်း ပါ တယ် ရှင်
ရော ဂါ ကု သ မှာ ကို လက် ခံ ပါ တယ် ဒေါက် တာ
ဟုတ် တယ် ။ ဓမ္မ တာ နာ ကျင် ကိုက် ခဲ မှု က ရိုး ရိုး ရှင်း ရှင်း စ တင် တာ ဖြစ် တတ် တယ် ၊ ဒါ ပေ မ ယ့် မင်း ရဲ့ အ ခြေ အ နေ က ဓမ္မ တာ မ လာ ခင် စိတ် ဖိ စီး မှု လို့ ခေါ် တယ် ပြီး ရင် နာ ကျင် မှု တွေ ဖြစ် တယ် သက် တော င့် သက် သာ မ ရှိ တဲ့ ဖြစ် တဲ့ ရာ သီ လာ ခြင်း ကို ဒစ် မန် နို ရီး ယား လို့ ခေါ် တယ် ။
မျက် လုံး တွေ က နီ နေ ခဲ့ တယ် ။
ဒေါက် တာ က လေ သွား အ ထဲ က အ ပိုင်း တွေ ဘယ် လို ဖြစ် နေ လဲ ဆို တာ သိ ချင် လို့
ဓါတ် ပုံ အ ရ တော့
လက် ခံ ပါ တယ် ဗျ
ဒါ့ အ ပြင် ကို ဗစ် ဆေး လည်း ထိုး သေး တယ် ဗျ ။
ဓာတ် မှန် ထဲ က အ နေ အ ထား ကို ပြန် ကြ ည့် ပါ ။
ပုံ ထဲ က လို မျိုး အ ရောင် ကြည် ကြည် မြင် လိုက် ရ သ လား ။
(base) ye@lst-gpu-3090:~/exp/wer-calc/ft_no_tag$
```

## Preparing a Python Script for Speaker-ID Tagging

I prepared a Python script: tag_speaker_id.py  

```python
"""

for tagging speaker ID.
Written by Ye Kyaw Thu, LU Lab., Myanmar.
Last updated date: 7 Feb 2024.

How to run:
    $ python ./tag_speaker_id.py --help


"""

import argparse
import sys

def tag_lines(input_stream, tag_prefix, output_stream):
    line_count = 1
    for line in input_stream:
        tagged_line = f"{line.strip()} ({tag_prefix}_{line_count})\n"
        output_stream.write(tagged_line)
        line_count += 1

def main():
    parser = argparse.ArgumentParser(description="Tag each line of the input with a unique identifier.")
    parser.add_argument("--tag", type=str, default="ye", help="Prefix for the tag to be added to each line.")
    parser.add_argument("-i", "--input", type=str, help="Input filename. If not provided, reads from stdin.")
    parser.add_argument("-o", "--output", type=str, help="Output filename. If not provided, prints to stdout.")
    args = parser.parse_args()

    # Handling input
    if args.input:
        try:
            input_stream = open(args.input, 'r', encoding='utf-8')
        except FileNotFoundError:
            print(f"Error: The file {args.input} was not found.")
            sys.exit(1)
    else:
        input_stream = sys.stdin

    # Handling output
    if args.output:
        output_stream = open(args.output, 'w', encoding='utf-8')
    else:
        output_stream = sys.stdout

    # Tagging process
    tag_lines(input_stream, args.tag, output_stream)

    # Closing files if needed
    if args.input:
        input_stream.close()
    if args.output:
        output_stream.close()

if __name__ == "__main__":
    main()

```

## Preparing a BASH Shell Script  

I wrote a Bash shell script: tag_all_ref_hyp.sh  

```bash
#!/bin/bash

# Function to display help message
show_help() {
    echo "Usage: $0 --folder <input_folder> [--output <output_folder>] [--tag <tag_prefix>]"
    echo "Options:"
    echo "  -f, --folder    Specify the folder containing files to be processed."
    echo "  -o, --output    (Optional) Specify the folder where output files should be saved."
    echo "  -t, --tag       (Optional) Specify the tag prefix to be used with the Python script."
    echo "  --help          Display this help message."
}

# Default values
tag="zen" # Default tag value

# Parse command-line arguments
while [[ "$#" -gt 0 ]]; do
    case $1 in
        -f|--folder) input_folder="$2"; shift ;;
        -o|--output) output_folder="$2"; shift ;;
        -t|--tag) tag="$2"; shift ;;
        --help) show_help; exit 0 ;;
        *) echo "Unknown parameter: $1"; show_help; exit 1 ;;
    esac
    shift
done

# Check if input folder is specified
if [[ -z "$input_folder" ]]; then
    echo "Error: Input folder is not specified."
    show_help
    exit 1
fi

# Default output folder to input folder if not specified
if [[ -z "$output_folder" ]]; then
    output_folder="$input_folder"
else
    # Check if the output folder exists, create it if not
    if [[ ! -d "$output_folder" ]]; then
        echo "Output folder does not exist, creating it..."
        mkdir -p "$output_folder"
    fi
fi

# Process files
for file in "$input_folder"/*; do
    if [[ $file =~ ref|hyp ]] && [[ ! $file =~ \.tag$ ]]; then
        filename=$(basename "$file")
        output="${filename%.*}.tag"
        echo "Processing $file with tag $tag..."
        python ./tag_speaker_id.py --input "$file" --output "$output_folder/$output" --tag "$tag"
    fi
done

echo "Processing completed."

```

Call --help ...  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ ./tag_all_ref_hyp.sh --help
Usage: ./tag_all_ref_hyp.sh --folder <input_folder> [--output <output_folder>] [--tag <tag_prefix>]
Options:
  -f, --folder    Specify the folder containing files to be processed.
  -o, --output    (Optional) Specify the folder where output files should be saved.
  -t, --tag       (Optional) Specify the tag prefix to be used with the Python script.
  --help          Display this help message.
(base) ye@lst-gpu-3090:~/exp/wer-calc$
```

## Tagging for Baseline Reference and Hypothesis Files

Run shell script for Baseline ...  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ ./tag_all_ref_hyp.sh --folder ./baseline --tag "zen"
Processing ./baseline/hyp_baseline.txt with tag zen...
Processing ./baseline/ref_baseline.txt with tag zen...
Processing completed.
```

Check the output files ...  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ ls ./baseline/
hyp_baseline.tag  hyp_baseline.txt  ref_baseline.tag  ref_baseline.txt  src_baseline.txt
```

Check the tagged reference files ...  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ head -n 5 ./baseline/ref_baseline.tag
รอ คุย รายละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ (zen_1)
ยินยอม เข้า รับ การ รักษา คะ (zen_2)
ครับ มัน เพิ่ง เริ่ม มี อาการ ปวด ประจำ เดือน แต่ ใน กรณี ของ คุณ เรียก ว่า ความ เครียด ก่อน มี ประจำ เดือน และ ช่วง เวลา ที่ มา พร้อม กับ ความ เจ็บปวด และ ความ รู้สึก ไม่ สบาย นั้น เรียก ว่า ประจำ เดือน ดิมัดโนลียา (zen_3)
ตา เป็น สี แดง (zen_4)
พี่ หมอ อยาก เห็น ว่า ข้าง ใน ฟัน มัน เป็น ยัง ไง (zen_5)
```

Check the tagged hypothesis files ...  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ head -n 5 ./baseline/hyp_baseline.tag
รอ คุย รายละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ โดย ตรง นะ คะ คุณ หมอ ปรึกษา คุณ หมอ (zen_1)
ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า (zen_2)
ครับ มัน เพิ่ง เริ่ม มี อาการ ปวด ประจํา เดือน แต่ ใน กรณี ของ คุณ เรียก ว่า ความ เครียด ก่อน มี ประจํา เดือน และ ช่วง เวลา ที่ มา พร้อม กับ ความ เจ็บปวด และ (zen_3)
ตา แดง ตา ของ ฉัน แดง ตา ตา ตา ตา ตา (zen_4)
พี่ หมอ อยาก เห็น ว่า ข้าง ใน ฟัน มัน เป็น ยัง ไง คือ คือ พี่ หมอ คือ พี่ หมอ พี่ หมอ พี่ หมอ พี่ หมอ อยาก เห็น พี่ หมอ พี่ หมอ พี่ หมอ พี่ หมอ พี่ (zen_5)
(base) ye@lst-gpu-3090:~/exp/wer-calc$
```

Check with tail command ...  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ tail -n 5 ./baseline/ref_baseline.tag
การ ตรวจ ภาย ใน (zen_8059)
การ บำบัด ความ คิด และ พฤติกรรม (zen_8060)
เจ็บ มาก เลย (zen_8061)
คุณ จะ มี เลนส์ และ แว่นตา ที่ แตกต่าง กัน ทั้ง ด้าน ซ้าย และ ด้าน ขวา ของ คุณ (zen_8062)
เรียก ญาติ คุณปราโมท เข้า มา ให้ หน่อย ค่ะ (zen_8063)
(base) ye@lst-gpu-3090:~/exp/wer-calc$
```

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ tail -n 5 ./baseline/hyp_baseline.tag
ตรวจ ภาย ใน (zen_8059)
เดี๋ยว รอ คุย กับ แพทย์ เฉพาะ ทาง ต่อ ไป ค่ะ วิธี การ รักษา (zen_8060)
เจ็บ จี๊ด มา เลย อ่ะ เจ็บ มาก (zen_8061)
คุณ จะ มี เลนส์ และ แว่นตา ที่ แตกต่าง กัน ทั้ง ด้าน ซ้าย และ ด้าน ขวา ของ คุณ คุณ คุณ คุณ คุณ คุณ คุณ คุณ คุณ คุณ คุณ คุณ คุณ (zen_8062)
เรียก ญาติ คุณปราโมท เข้า มา ให้ หน่อย ค่ะ ญาติ ค่ะ ญาติ ค่ะ ญาติ ค่ะ ญาติ ค่ะ ญาติ ค่ะ ญาติ ค่ะ ญาติ คุณปราโมท เข้า มา ให้ หน่อย ค่ะ ญาติ ค่ะ (zen_8063)
(base) ye@lst-gpu-3090:~/exp/wer-calc$
```

## Tagging for ft_tag/ Reference and Hypothesis Files

Run bash shell script for tagging ./ft_tag/ folder:  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ ./tag_all_ref_hyp.sh --folder ./ft_tag --tag "zen"
Processing ./ft_tag/hyp_ft_tag.txt with tag zen...
Processing ./ft_tag/ref_ft_tag.txt with tag zen...
Processing completed.
(base) ye@lst-gpu-3090:~/exp/wer-calc$
```

Check the output ...  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ ls ./ft_tag
hyp_ft_tag.tag  hyp_ft_tag.txt  ref_ft_tag.tag  ref_ft_tag.txt  src_ft_tag.txt
(base) ye@lst-gpu-3090:~/exp/wer-calc$
```

Check the tagged files ...  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc/ft_tag$ head *.tag
==> hyp_ft_tag.tag <==
รอ คุย รายละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ รอ คุย กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ (zen_1)
ยินยอม เข้า รับ การ รักษา คะ ยินยอม เข้า รับ การ รักษา คะ (zen_2)
ครับ มัน เพิ่ง เริ่ม มี อาการ ปวด ประจํา เดือน แต่ ใน กรณี ของ คุณ เรียก ว่า ความ เครียด ก่อน มี ประจํา เดือน และ ช่วง เวลา ที่ มา พร้อม กับ ความ รู้สึก ไม่ สบาย (zen_3)
ตา แดง ตา ตา ตา มัว ตา ตา ตา ตา ตา ตา ตา ตา ตา ตา (zen_4)
พี่ หมอ อยาก เห็น ว่า ข้าง ใน ฟัน มัน เป็น ยัง ไง คือ พี่ หมอ คือ พี่ หมอ คือ พี่ หมอ พี่ หมอ พี่ หมอ คือ พี่ หมอ พี่ หมอ พี่ หมอ (zen_5)
จาก ภาพ x- ray จาก การ ตรวจ ร่างกาย (zen_6)
ยินยอม ครับ ยินยอม ครับ ยินยอม ครับ ยินยอม ครับ (zen_7)
และ ฉีด วัคซีน ป้องกัน โควิด ครับ และ ฉีด วัคซีน ครับ (zen_8)
เดี๋ยว (zen_9)
น้อง ใช่ เจอ แบบ ใน รูป สี ใส ๆ ใช่ ไหม ครับ ต้อง ใส่ (zen_10)

==> ref_ft_tag.tag <==
รอ คุย รายละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ (zen_1)
ยินยอม เข้า รับ การ รักษา คะ (zen_2)
ครับ มัน เพิ่ง เริ่ม มี อาการ ปวด ประจำ เดือน แต่ ใน กรณี ของ คุณ เรียก ว่า ความ เครียด ก่อน มี ประจำ เดือน และ ช่วง เวลา ที่ มา พร้อม กับ ความ เจ็บปวด และ ความ รู้สึก ไม่ สบาย นั้น เรียก ว่า ประจำ เดือน ดิมัดโนลียา (zen_3)
ตา เป็น สี แดง (zen_4)
พี่ หมอ อยาก เห็น ว่า ข้าง ใน ฟัน มัน เป็น ยัง ไง (zen_5)
จาก ภาพ x- ray (zen_6)
ยินยอม (zen_7)
และ ฉีด วัคซีน ป้องกัน โควิด ครับ (zen_8)
เดี๋ยว film ซ้ำ ดู ตำแหน่ง หน่อย (zen_9)
น้อง ใช่ เจอ แบบ ใน รูป สี ใส ๆ (zen_10)
(base) ye@lst-gpu-3090:~/exp/wer-calc/ft_tag$
```

## Tagging for ft_no_tag/ Reference and Hypothesis Files

Run a Bash Shell script for tagging ...  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ ./tag_all_ref_hyp.sh --folder ./ft_no_tag/ --tag "z
en"
Processing ./ft_no_tag//hyp_ft_notag.txt with tag zen...
Processing ./ft_no_tag//ref_ft_notag.txt with tag zen...
Processing completed.
(base) ye@lst-gpu-3090:~/exp/wer-calc$
```

Check the speaker-ID tagged output files ...  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc/ft_no_tag$ head *.tag
==> hyp_ft_notag.tag <==
รอ คุย รายละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ โดย ละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ นะ คะ (zen_1)
ยินยอม ทํา การ รักษา ตาม คํา สั่ง แพทย์ (zen_2)
ครับ มัน เพิ่ง เริ่ม มี อาการ ปวด ประจํา เดือน แต่ ใน กรณี ของ คุณ เรียก ว่า ความ เครียด ก่อน มี ประจํา เดือน และ ช่วง เวลา ที่ มา พร้อม กับ ความ รู้สึก ไม่ สบาย (zen_3)
ตา แดง ด้วย ค่ะ ตา แดง ตา แดง ตา แดง ตา ของ ฉัน แดง ตา ตา ตา แดง ตา (zen_4)
พี่ หมอ อยาก เห็น ว่า ข้าง ใน ฟัน มัน เป็น ยัง ไง พี่ พี่ พี่ หมอ พี่ พี่ พี่ พี่ พี่ พี่ พี่ พี่ หมอ พี่ พี่ พี่ หมอ พี่ พี่ พี่ (zen_5)
จาก ภาพ x- ray จาก การ ตรวจ ร่างกาย (zen_6)
ยินยอม ครับ ยินยอม ยินยอม ยินยอม ครับ ยินยอม ยินยอม ยินยอม ครับ ยินยอม ยินยอม ยินยอม ยินยอม ครับ ยิน (zen_7)
และ ฉีด วัคซีน ป้องกัน โควิด ครับ และ ฉีด วัคซีน ครับ ครับ และ ฉีด วัคซีน ครับ ครับ ครับ ครับ ครับ ครับ และ ฉีด วัคซีน ครับ ครับ ครับ ครับ ครับ ครับ (zen_8)
เดี๋ยว (zen_9)
น้อง ใช่ เจอ แบบ ใน รูป สี ใส ๆ ต้อง มอง เห็น ไหม ครับ น้อง ต้อง ใส่ (zen_10)

==> ref_ft_notag.tag <==
รอ คุย รายละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ (zen_1)
ยินยอม เข้า รับ การ รักษา คะ (zen_2)
ครับ มัน เพิ่ง เริ่ม มี อาการ ปวด ประจำ เดือน แต่ ใน กรณี ของ คุณ เรียก ว่า ความ เครียด ก่อน มี ประจำ เดือน และ ช่วง เวลา ที่ มา พร้อม กับ ความ เจ็บปวด และ ความ รู้สึก ไม่ สบาย นั้น เรียก ว่า ประจำ เดือน ดิมัดโนลียา (zen_3)
ตา เป็น สี แดง (zen_4)
พี่ หมอ อยาก เห็น ว่า ข้าง ใน ฟัน มัน เป็น ยัง ไง (zen_5)
จาก ภาพ x- ray (zen_6)
ยินยอม (zen_7)
และ ฉีด วัคซีน ป้องกัน โควิด ครับ (zen_8)
เดี๋ยว film ซ้ำ ดู ตำแหน่ง หน่อย (zen_9)
น้อง ใช่ เจอ แบบ ใน รูป สี ใส ๆ (zen_10)
(base) ye@lst-gpu-3090:~/exp/wer-calc/ft_no_tag$
```

## Check the SCLITE Command  

I already installed on my machine and thus, just checked able to run or not as follows:  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc/ft_no_tag$ sclite
sclite: <OPTIONS>
sclite Version: 2.10, SCTK Version: 1.3
Input Options:
    -r reffile [ <rfmt> ]
                Define the reference file, and it's format
    -h hypfile [ <hfmt> <title> ]
                Define the hypothesis file, it's format, and a 'title' used
                for reports.  The default title is 'hypfile'.  This option
                may be used more than once.
    -i <ids>    Set the utterance id type.   (for transcript mode only)
    -P          Accept the piped input from another utility.
    -e gb|euc|utf-8 [ case-conversion-localization ]
                Interpret characters as GB, EUC, utf-8, or the default, 8-bit ASCII.
                Optionally, case conversion localization can be set to either 'generic',
                'babel_turkish', or 'babel_vietnamese', 'ukranian'
Alignment Options:
    -s          Do Case-sensitive alignments.
    -d          Use GNU diff for alignments.
    -c [ NOASCII DH ]
                Do the alignment on characters not on words as usual by split-
                ting words into chars. The optional argument NOASCII does not
                split ASCII words and the optional arg. DH deletes hyphens from
                both the ref and hyp before alingment.   Exclusive with -d.
    -L LM       CMU-Cambridge SLM Language model file to use in alignment and scoring.
    -S algo1 lexicon [ ASCIITOO ]
    -S algo2 lexicon [ ASCIITOO ]
                Instead of performing word alignments, infer the word segmenta-
                tion using algo1 or algo2.  See sclite(1) for algorithm details.
    -F          Score fragments as correct.  Options -F and -d are exclusive.
    -D          Score words marked optionally deletable as correct if deleted.
                Options -D and -d are exclusive.
    -T          Use time information, (if available), to calculated word-to-
                word distances based on times. Options -F and -d are exlc.
    -w wwl      Perform Word-Weight Mediated alignments, using the WWL file 'wwl'.
                IF wwl is 'unity' use weight 1.o for all words.
    -m [ ref | hyp ]
                Only used for scoring a hyp/ctm file, against a ref/stm file.
                When the 'ref' option is used, reduce the reference segments
                to time range of the hyp file's words.  When the 'hyp' option
                is used, reduce the hyp words to the time range of the ref
                segments.  The two may be used together.  The argument -m
                by itself defaults to '-m ref'.  Exclusive with -d.
Output Options:
    -O output_dir
                Writes all output files into output_dir. Defaults to the
                hypfile's directory.
    -f level    Defines feedback mode, default is 1
    -l width    Defines the line width.
    -p          Pipe the alignments to another sclite utility.  Sets -f to 0.
Scoring Report Options:
    -o [ sum | rsum | pralign | all | sgml | stdout | lur | snt | spk |
         dtl | prf | wws | nl.sgml | none ]
                Defines the output reports. Default: 'sum stdout'
    -C [ det | bhist | sbhist | hist | none ]
                Defines the output formats for analysis of confidence scores.
                Default: 'none'
    -n name     Writes all outputs using 'name' as a root filename instead of
                'hypfile'.  For multiple hypothesis files, the root filename
                is 'name'.'hypfile'

sclite: Error, Arguments reguired

(base) ye@lst-gpu-3090:~/exp/wer-calc/ft_no_tag$
```

## Preparing a Bash Script For WER Calculations

I wrote a shell script named: wer_calc.sh.  

```bash
#!/bin/bash

echo "## WER Calculation for Baseline";
echo "See some SYSTEM SUMMARY PERCENTAGES on screen ...";
sclite -r ./baseline/ref_baseline.tag -h ./baseline/hyp_baseline.tag -i spu_id;
echo -e "==========\n";

echo "Running with pra option ...";
sclite -r ./baseline/ref_baseline.tag -h ./baseline/hyp_baseline.tag -i spu_id -o pra;
echo -e "==========\n";

echo "Running with dtl option ...";
sclite -r ./baseline/ref_baseline.tag -h ./baseline/hyp_baseline.tag -i spu_id -o dtl;
echo -e "==========\n";

echo "## WER Calculation for Finetuned with Tag";
echo "See some SYSTEM SUMMARY PERCENTAGES on screen ...";
sclite -r ./ft_tag/ref_ft_tag.tag -h ./ft_tag/hyp_ft_tag.tag -i spu_id;
echo -e "==========\n";

echo "Running with pra option ...";
sclite -r ./ft_tag/ref_ft_tag.tag -h ./ft_tag/hyp_ft_tag.tag -i spu_id -o pra;
echo -e "==========\n";

echo "Running with dtl option ...";
sclite -r ./ft_tag/ref_ft_tag.tag -h ./ft_tag/hyp_ft_tag.tag -i spu_id -o dtl;
echo -e "==========\n";

echo "## WER Calculation for Finetuned with No-Tag";
echo "See some SYSTEM SUMMARY PERCENTAGES on screen ...";
sclite -r ./ft_no_tag/ref_ft_notag.tag -h ./ft_no_tag/hyp_ft_notag.tag -i spu_id;
echo -e "==========\n";

echo "Running with pra option ...";
sclite -r ./ft_no_tag/ref_ft_notag.tag -h ./ft_no_tag/hyp_ft_notag.tag -i spu_id -o pra;
echo -e "==========\n";

echo "Running with dtl option ...";
sclite -r ./ft_no_tag/ref_ft_notag.tag -h ./ft_no_tag/hyp_ft_notag.tag -i spu_id -o dtl;
echo -e "==========\n";

```

## WER Calculations for All Three Approaches

I run as follows and saved the running log with tee command.  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ ./wer_calc.sh | tee wer_calc_running.log
## WER Calculation for Baseline
See some SYSTEM SUMMARY PERCENTAGES on screen ...
Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ฉีด ยาชา* (zen_441)

Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ตรวจ ใน ช่อง ปาก * (zen_2654)

Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ผ่า ฟัน ออก * (zen_7097)

sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './baseline/ref_baseline.tag' and Hyp File: './baseline/hyp_baseline.tag'
    Alignment# 8063 for speaker zen




                     SYSTEM SUMMARY PERCENTAGES by SPEAKER

     ,-------------------------------------------------------------------.
     |                    ./baseline/hyp_baseline.tag                    |
     |-------------------------------------------------------------------|
     | SPKR   | # Snt   # Wrd  | Corr    Sub    Del    Ins    Err  S.Err |
     |--------+----------------+-----------------------------------------|
     | zen    |  8063   56900  | 92.2    5.7    2.1  174.9  182.7   88.5 |
     |===================================================================|
     | Sum/Avg|  8063   56900  | 92.2    5.7    2.1  174.9  182.7   88.5 |
     |===================================================================|
     |  Mean  |8063.0  56900.0 | 92.2    5.7    2.1  174.9  182.7   88.5 |
     |  S.D.  |  0.0      0.0  |  0.0    0.0    0.0    0.0    0.0    0.0 |
     | Median |8063.0  56900.0 | 92.2    5.7    2.1  174.9  182.7   88.5 |
     `-------------------------------------------------------------------'

Successful Completion
==========

Running with pra option ...
Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ฉีด ยาชา* (zen_441)

Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ตรวจ ใน ช่อง ปาก * (zen_2654)

Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ผ่า ฟัน ออก * (zen_7097)

sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './baseline/ref_baseline.tag' and Hyp File: './baseline/hyp_baseline.tag'
    Alignment# 8063 for speaker zen

    Writing string alignments to './baseline/hyp_baseline.tag.pra'

Successful Completion
==========

Running with dtl option ...
Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ฉีด ยาชา* (zen_441)

Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ตรวจ ใน ช่อง ปาก * (zen_2654)

Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ผ่า ฟัน ออก * (zen_7097)

sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './baseline/ref_baseline.tag' and Hyp File: './baseline/hyp_baseline.tag'
    Alignment# 8063 for speaker zen

    Writing overall detailed scoring report './baseline/hyp_baseline.tag.dtl'

Successful Completion
==========

## WER Calculation for Finetuned with Tag
See some SYSTEM SUMMARY PERCENTAGES on screen ...
Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ฉีด ยาชา* (zen_441)

Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ตรวจ ใน ช่อง ปาก * (zen_2654)

Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ผ่า ฟัน ออก * (zen_7097)

sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ft_tag/ref_ft_tag.tag' and Hyp File: './ft_tag/hyp_ft_tag.tag'
    Alignment# 8063 for speaker zen




                     SYSTEM SUMMARY PERCENTAGES by SPEAKER

     ,-------------------------------------------------------------------.
     |                      ./ft_tag/hyp_ft_tag.tag                      |
     |-------------------------------------------------------------------|
     | SPKR   | # Snt   # Wrd  | Corr    Sub    Del    Ins    Err  S.Err |
     |--------+----------------+-----------------------------------------|
     | zen    |  8063   56900  | 90.8    6.8    2.5  131.7  140.9   81.8 |
     |===================================================================|
     | Sum/Avg|  8063   56900  | 90.8    6.8    2.5  131.7  140.9   81.8 |
     |===================================================================|
     |  Mean  |8063.0  56900.0 | 90.8    6.8    2.5  131.7  140.9   81.8 |
     |  S.D.  |  0.0      0.0  |  0.0    0.0    0.0    0.0    0.0    0.0 |
     | Median |8063.0  56900.0 | 90.8    6.8    2.5  131.7  140.9   81.8 |
     `-------------------------------------------------------------------'

Successful Completion
==========

Running with pra option ...
Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ฉีด ยาชา* (zen_441)

Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ตรวจ ใน ช่อง ปาก * (zen_2654)

Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ผ่า ฟัน ออก * (zen_7097)

sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ft_tag/ref_ft_tag.tag' and Hyp File: './ft_tag/hyp_ft_tag.tag'
    Alignment# 8063 for speaker zen

    Writing string alignments to './ft_tag/hyp_ft_tag.tag.pra'

Successful Completion
==========

Running with dtl option ...
Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ฉีด ยาชา* (zen_441)

Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ตรวจ ใน ช่อง ปาก * (zen_2654)

Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ผ่า ฟัน ออก * (zen_7097)

sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ft_tag/ref_ft_tag.tag' and Hyp File: './ft_tag/hyp_ft_tag.tag'
    Alignment# 8063 for speaker zen

    Writing overall detailed scoring report './ft_tag/hyp_ft_tag.tag.dtl'

Successful Completion
==========

## WER Calculation for Finetuned with No-Tag
See some SYSTEM SUMMARY PERCENTAGES on screen ...
Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ฉีด ยาชา* (zen_441)

Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ตรวจ ใน ช่อง ปาก * (zen_2654)

Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ผ่า ฟัน ออก * (zen_7097)

sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ft_no_tag/ref_ft_notag.tag' and Hyp File: './ft_no_tag/hyp_ft_notag.tag'
    Alignment# 8063 for speaker zen




                     SYSTEM SUMMARY PERCENTAGES by SPEAKER

     ,-------------------------------------------------------------------.
     |                   ./ft_no_tag/hyp_ft_notag.tag                    |
     |-------------------------------------------------------------------|
     | SPKR   | # Snt   # Wrd  | Corr    Sub    Del    Ins    Err  S.Err |
     |--------+----------------+-----------------------------------------|
     | zen    |  8063   56900  | 90.9    6.8    2.3  160.6  169.7   86.5 |
     |===================================================================|
     | Sum/Avg|  8063   56900  | 90.9    6.8    2.3  160.6  169.7   86.5 |
     |===================================================================|
     |  Mean  |8063.0  56900.0 | 90.9    6.8    2.3  160.6  169.7   86.5 |
     |  S.D.  |  0.0      0.0  |  0.0    0.0    0.0    0.0    0.0    0.0 |
     | Median |8063.0  56900.0 | 90.9    6.8    2.3  160.6  169.7   86.5 |
     `-------------------------------------------------------------------'

Successful Completion
==========

Running with pra option ...
Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ฉีด ยาชา* (zen_441)

Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ตรวจ ใน ช่อง ปาก * (zen_2654)

Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ผ่า ฟัน ออก * (zen_7097)

sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ft_no_tag/ref_ft_notag.tag' and Hyp File: './ft_no_tag/hyp_ft_notag.tag'
    Alignment# 8063 for speaker zen

    Writing string alignments to './ft_no_tag/hyp_ft_notag.tag.pra'

Successful Completion
==========

Running with dtl option ...
Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ฉีด ยาชา* (zen_441)

Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ตรวจ ใน ช่อง ปาก * (zen_2654)

Warning: The comment designation is now **, the line below
         has only one comment info character, this may be an error
         * ผ่า ฟัน ออก * (zen_7097)

sclite: 2.10 TK Version 1.3
Begin alignment of Ref File: './ft_no_tag/ref_ft_notag.tag' and Hyp File: './ft_no_tag/hyp_ft_notag.tag'
    Alignment# 8063 for speaker zen

    Writing overall detailed scoring report './ft_no_tag/hyp_ft_notag.tag.dtl'

Successful Completion
==========

(base) ye@lst-gpu-3090:~/exp/wer-calc$
```

## Analysis Roughly on Top Confusion Pairs of the Baseline  

Here, you have to check .dtl file for analysis on top errors or confusion pairs.  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc/baseline$ ls
hyp_baseline.tag      hyp_baseline.tag.pra  ref_baseline.tag  src_baseline.txt
hyp_baseline.tag.dtl  hyp_baseline.txt      ref_baseline.txt
(base) ye@lst-gpu-3090:~/exp/wer-calc/baseline$
```

Let's check top 30 errors for the baseline approach:  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc/baseline$ awk '/^[[:space:]]*([1-9]|1[0-9]|2[0-9]|30):/ { if (!seen[$1]++) print }' ./hyp_baseline.tag.dtl
   1:  316  ->  ทำ ==> ทํา
   2:  126  ->  น้ำ ==> น้ํา
   3:   69  ->  ประจำ ==> ประจํา
   4:   36  ->  กำลัง ==> กําลัง
   5:   35  ->  น้ำหนัก ==> น้ําหนัก
   6:   28  ->  แนะนำ ==> แนะนํา
   7:   26  ->  ลำ ==> ลํา
   8:   20  ->  ครับ ==> ค่ะ
   9:   20  ->  ค่ะ ==> ครับ
  10:   19  ->  สำหรับ ==> สําหรับ
  11:   17  ->  คำ ==> คํา
  12:   17  ->  จำ ==> จํา
  13:   16  ->  นำ ==> นํา
  14:   16  ->  น้ำมูก ==> น้ํามูก
  15:   16  ->  หมอ ==> ครับ
  16:   15  ->  จำเป็น ==> จําเป็น
  17:   14  ->  น้ำลาย ==> น้ําลาย
  18:   14  ->  หมอ ==> ค่ะ
  19:   13  ->  ต่ำ ==> ต่ํา
  20:   13  ->  สำคัญ ==> สําคัญ
  21:   12  ->  คะ ==> ค่ะ
  22:   12  ->  คุณ ==> ค่ะ
  23:   12  ->  ตำแหน่ง ==> ตําแหน่ง
  24:   11  ->  ซ้ำ ==> ซ้ํา
  25:   11  ->  ลำบาก ==> ลําบาก
  26:   11  ->  โอเค ==> ครับ
  27:   11  ->  โอเค ==> ค่ะ
  28:    9  ->  ได้ ==> ค่ะ
  29:    9  ->  ๆ ==> ค่ะ
  30:    8  ->  กำหนด ==> กําหนด
(base) ye@lst-gpu-3090:~/exp/wer-calc/baseline$
```

Note: You should check the whole ./hyp_baseline.tag.dtl for detail analysis.  

## Analysis Roughly on Top Confusion Pairs of Finetuned without Tags  

Let's see the top 30 errors for the Finetuned without Tags approach:  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc/ft_no_tag$ awk '/^[[:space:]]*([1-9]|1[0-9]|2[0-9]|30):/ { if (!seen[$1]++) print }' ./hyp_ft_notag.tag.dtl
   1:  310  ->  ทำ ==> ทํา
   2:  127  ->  น้ำ ==> น้ํา
   3:   63  ->  ประจำ ==> ประจํา
   4:   35  ->  กำลัง ==> กําลัง
   5:   35  ->  น้ำหนัก ==> น้ําหนัก
   6:   28  ->  ค่ะ ==> ครับ
   7:   28  ->  แนะนำ ==> แนะนํา
   8:   24  ->  ลำ ==> ลํา
   9:   20  ->  สำหรับ ==> สําหรับ
  10:   17  ->  คำ ==> คํา
  11:   17  ->  จำ ==> จํา
  12:   17  ->  น้ำมูก ==> น้ํามูก
  13:   16  ->  นำ ==> นํา
  14:   16  ->  หมอ ==> ครับ
  15:   15  ->  จำเป็น ==> จําเป็น
  16:   14  ->  น้ำลาย ==> น้ําลาย
  17:   13  ->  ครับ ==> ค่ะ
  18:   13  ->  ต่ำ ==> ต่ํา
  19:   12  ->  ค่ะ ==> คะ
  20:   12  ->  ตำแหน่ง ==> ตําแหน่ง
  21:   12  ->  สำคัญ ==> สําคัญ
  22:   11  ->  ลำบาก ==> ลําบาก
  23:   11  ->  ใช่ ==> ครับ
  24:   10  ->  คะ ==> ครับ
  25:   10  ->  คุณ ==> ครับ
  26:   10  ->  ซ้ำ ==> ซ้ํา
  27:   10  ->  ดำ ==> ดํา
  28:   10  ->  ได้ ==> ครับ
  29:    8  ->  ครับ ==> คะ
  30:    8  ->  ผม ==> ฉัน
(base) ye@lst-gpu-3090:~/exp/wer-calc/ft_no_tag$
```

## Analysis Roughly on Top Confusion Pairs of Finetuned with Tags

Let's see top 30 errors of the Finetuned with Tags approach:  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc/ft_tag$ awk '/^[[:space:]]*([1-9]|1[0-9]|2[0-9]|30):/ { if (!seen[$1]++) print }' ./hyp_ft_tag.tag.dtl
   1:  315  ->  ทำ ==> ทํา
   2:  135  ->  น้ำ ==> น้ํา
   3:   67  ->  ประจำ ==> ประจํา
   4:   34  ->  น้ำหนัก ==> น้ําหนัก
   5:   33  ->  กำลัง ==> กําลัง
   6:   29  ->  แนะนำ ==> แนะนํา
   7:   27  ->  ค่ะ ==> ครับ
   8:   26  ->  หมอ ==> ครับ
   9:   25  ->  ลำ ==> ลํา
  10:   21  ->  สำหรับ ==> สําหรับ
  11:   18  ->  จำ ==> จํา
  12:   18  ->  น้ำมูก ==> น้ํามูก
  13:   17  ->  คำ ==> คํา
  14:   17  ->  นำ ==> นํา
  15:   15  ->  ค่ะ ==> คะ
  16:   15  ->  จำเป็น ==> จําเป็น
  17:   14  ->  ลำบาก ==> ลําบาก
  18:   13  ->  ครับ ==> ค่ะ
  19:   13  ->  น้ำลาย ==> น้ําลาย
  20:   13  ->  สำคัญ ==> สําคัญ
  21:   12  ->  ต่ำ ==> ต่ํา
  22:   11  ->  ซ้ำ ==> ซ้ํา
  23:   11  ->  ตำแหน่ง ==> ตําแหน่ง
  24:   11  ->  โอเค ==> ครับ
  25:   10  ->  คุณ ==> ครับ
  26:   10  ->  หมอ ==> ค่ะ
  27:    9  ->  ทำลาย ==> ทําลาย
  28:    8  ->  ครับ ==> คะ
  29:    8  ->  คะ ==> ครับ
  30:    8  ->  คุณ ==> ค่ะ
(base) ye@lst-gpu-3090:~/exp/wer-calc/ft_tag$
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
