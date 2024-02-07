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

```python
"""

for extraction of source, target (i.e. reference) and prediction (i.e. hypothesis).
Written by Ye Kyaw Thu, LU Lab., Myanmar.
Last updated: 7 Feb 2024

How to run:
$ python ./extract_src_tgt_hyp.py --help
$ python ./extract_src_tgt_hyp.py --input ./1_baseline.txt --output baseline

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
        extract_sentences(input_file, output_folder, "src_ft_tag.txt", "tgt_ft_tag.txt", "hyp_ft_tag.txt")
    elif "finetuned-notagged" in input_file:
        extract_sentences(input_file, output_folder, "src_ft_notag.txt", "tgt_ft_notag.txt", "hyp_ft_notag.txt")
    else:
        print("Unrecognized file type. Please ensure the file name contains either 'baseline', 'finetuned_tagged', or 'finetuned-notagged'.")

if __name__ == "__main__":
    main()

```

## Check --help

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ python ./extract.py --help
usage: extract.py [-h] -i INPUT -o OUTPUT

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
(base) ye@lst-gpu-3090:~/exp/wer-calc$ time python ./extract.py --input ./1_baseline.txt --output baseline

real    0m0.036s
user    0m0.032s
sys     0m0.004s
```

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ time python ./extract.py --input ./2_finetuned_tagged.txt --output ft_tag

real    0m0.034s
user    0m0.023s
sys     0m0.011s
```

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ time python ./extract.py --input ./3_finetuned-notagged.txt --output ft_no_tag

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
├── src_ft_tag.txt
└── tgt_ft_tag.txt

0 directories, 3 files
```

Check the ./ft_no_tag/ folder:  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ tree ./ft_no_tag/
./ft_no_tag/
├── hyp_ft_notag.txt
├── src_ft_notag.txt
└── tgt_ft_notag.txt

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
   8063  100145  930383 ./ft_tag/src_ft_tag.txt
   8063   56900  661580 ./ft_tag/tgt_ft_tag.txt
  24189  287504 3111384 total
```

Check no. of sentences:  

```
(base) ye@lst-gpu-3090:~/exp/wer-calc$ wc ./ft_no_tag/*
   8063  146954 1706467 ./ft_no_tag/hyp_ft_notag.txt
   8063  100145  930383 ./ft_no_tag/src_ft_notag.txt
   8063   56900  661580 ./ft_no_tag/tgt_ft_notag.txt
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

==> tgt_ft_tag.txt <==
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

==> tgt_ft_notag.txt <==
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
(base) ye@lst-gpu-3090:~/exp/wer-calc/ft_no_tag$
```

## Check the SCLITE Command  

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
