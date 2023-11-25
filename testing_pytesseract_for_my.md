# Testing for Myanmar Language OCR

လက်ရှိ Google ရဲ့ Tesseract OCR Engine က မြန်မာစာအတွက် ဘယ်လောက်ထိ မှန်မှန်ကန်ကန် လုပ်ပေးနိုင်သလဲ ဆိုတာကို testing ပြန်လုပ်ကြည့်ခဲ့တာ။  

## Downloading Myanmar Language Data

```
(base) ye@lst-gpu-3090:~/tool/tesseract/tessdata$ wget https://github.com/tesseract-ocr/tessdata/raw/main/mya.traineddata -P /home/ye/tool/tesseract/tessdata/
--2023-11-25 16:27:04--  https://github.com/tesseract-ocr/tessdata/raw/main/mya.traineddata
Resolving github.com (github.com)... 20.205.243.166
Connecting to github.com (github.com)|20.205.243.166|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://raw.githubusercontent.com/tesseract-ocr/tessdata/main/mya.traineddata [following]
--2023-11-25 16:27:05--  https://raw.githubusercontent.com/tesseract-ocr/tessdata/main/mya.traineddata
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.111.133, 185.199.110.133, 185.199.109.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.111.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 4640591 (4.4M) [application/octet-stream]
Saving to: ‘/home/ye/tool/tesseract/tessdata/mya.traineddata’

mya.traineddata        100%[==========================>]   4.42M  11.6MB/s    in 0.4s

2023-11-25 16:27:06 (11.6 MB/s) - ‘/home/ye/tool/tesseract/tessdata/mya.traineddata’ saved [4640591/4640591]

(base) ye@lst-gpu-3090:~/tool/tesseract/tessdata$
```

## Updated Python Code

```python
## Written by Ye Kyaw Thu, LU Lab., Myanmar
## for testing English and Burmese OCR
## last updated: 25 Nov 2023

import argparse
import pytesseract
from PIL import Image

def perform_ocr(image_path, language='eng'):
    """
    Perform OCR on an image file and return the extracted text.

    :param image_path: Path to the image file.
    :param language: Language code for OCR.
    :return: Extracted text as a string.
    """
    try:
        # Load the image from the given path
        image = Image.open(image_path)

        # Perform OCR using Tesseract
        extracted_text = pytesseract.image_to_string(image, lang=language)

        return extracted_text
    except Exception as e:
        return f"An error occurred: {str(e)}"

def main():
    # Create the parser
    parser = argparse.ArgumentParser(description='OCR Script to extract text from an image.')

    # Add the arguments
    parser.add_argument('image_path', type=str, help='Path to the image file.')
    parser.add_argument('-o', '--output', type=str, help='Output file to save the extracted text.')
    parser.add_argument('-l', '--language', type=str, default='eng', help='Language for OCR (default: eng).')

    # Execute the parse_args() method
    args = parser.parse_args()

    extracted_text = perform_ocr(args.image_path, args.language)

    if args.output:
        # If output file is specified, write the text to the file
        with open(args.output, 'w') as file:
            file.write(extracted_text)
        print(f"Extracted text written to {args.output}")
    else:
        # Otherwise, print the text
        print("Extracted Text:\n", extracted_text)

if __name__ == "__main__":
    main()

```

## Called --help

```
(base) ye@lst-gpu-3090:~/tool/tesseract/y$ python ./tesseract_ocr.py --help
usage: tesseract_ocr.py [-h] [-o OUTPUT] [-l LANGUAGE] image_path

OCR Script to extract text from an image.

positional arguments:
  image_path            Path to the image file.

optional arguments:
  -h, --help            show this help message and exit
  -o OUTPUT, --output OUTPUT
                        Output file to save the extracted text.
  -l LANGUAGE, --language LANGUAGE
                        Language for OCR (default: eng).
(base) ye@lst-gpu-3090:~/tool/tesseract/y$
```

## Testing for English

အင်္ဂလိပ်စာ OCR အတွက် သုံးခဲ့တဲ့ input ဖိုင်က အောက်ပါအတိုင်းပါ။  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/tesseract_test/ws_program.png" alt="input file for English OCR" width="800"/>  
</p>  
<div align="center">
  Fig.1 Input file for Testing English OCR  
</div> 

<br />

အင်္ဂလိပ်စာ အတွက် စမ်းကြည့်ပြီး ရလာတဲ့ ရလဒ်က အောက်ပါအတိုင်းပါ။ ရလဒ်က တော်တော်လေး ကောင်းပါတယ်။  

```
(base) ye@lst-gpu-3090:~/tool/tesseract/y$ time python ./tesseract_ocr.py ./ws_program.png -l eng
Extracted Text:
 WS2 : Development of Synthesized Speech with a Focus on The Issue of
Prosodic Elongation

Aphiwich Sangpet and Natthapol Kritsuthikul

WS3 : Myanmar Hate Speech Generation Using GPT-2: A Novel Technique for
Corpus Expansion

Nang Aeindray Kyaw, Ye Kyaw Thu, Thazin Myint Oo, Hutchatai Chanlekha,
Manabu Okumura

WS4 : myNER9: Development, Manual Annotation, and Evaluation of a 9-Tag
Myanmar NER Corpus via XGBoost and Bi-LSTM

Kaung Lwin Thant, Ye Kyaw Thu, Thazin Myint Oo, Kwankamol Nongpong

WS5 : Myanmar Spelling Error Classification: An Empirical Study of Tsetlin
Machine Techniques

Ei Thandar Phyu, Ye Kyaw Thu, Thazin Myint Oo, Hutchatai Chanlekha



real    0m0.506s
user    0m1.662s
sys     0m1.946s
(base) ye@lst-gpu-3090:~/tool/tesseract/y$
```

## Testing for Burmese

အကြမ်း testing လုပ်ဖို့အတွက် သုံးခဲ့တဲ့ မြန်မာစာပါတဲ့ ပုံဖိုင်က အောက်ပါအတိုင်း ...  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/tesseract_test/comment_to_student.png" alt="input file for Myanmar language OCR testing" width="800"/>  
</p>  
<div align="center">
  Fig.2 Input file for Testing Myanmar language OCR 
</div> 

<br />

Google's Tesseract က trained လုပ်ပေးထားတဲ့ မော်ဒယ်ကို သုံးပြီး ရလာတဲ့ ရလဒ်က အောက်ပါအတိုင်းပါ။  

```
(base) ye@lst-gpu-3090:~/tool/tesseract/y$ python ./tesseract_ocr.py ./comment_to_student.png -l mya
Extracted Text:
 319 လက်ရိုမှာ [၅၁၈၉ ၁ ၉၉ တအားနည်းနေသေးတယ်# စာတမ်း တစ်စောင်အနေနဲ့ ထပ်ဖြ သင်တယ်!
| | ဂ စြ ၀ ဤ ဝ
320
321 နောက်ပြီးတော့ နေအေဒေင တွေကို ] အေး မှာထည့်တဲ့အခါမှာ အောက်ပါလိုမျိုး နံပါတ်တွေကို
ငြ ဂ | | ၀. ၀ | | ဂ |!

ကိုယ့်ဖာသာကိုယ် ထိုးစရာမလိုပါဘူး1
၆၇ ၁၀၂ ၂၀၂ င. ၂၂ 4၉၅ ၅၂၅၂
323
၁၁4 5 115*ဒေး ဖိုင်ဆောက်ပြီးတော့ အဲဒီအထဲမှာ ) ၅“ 5၀7 နဲ့ စဒေဒေဒေငဓ ရေးတာမျိုးကို လုပ်လို့

ရတယ်#
၂ စ င ' ၀၀. လှု လူ ဝ
၁၁၈ တချို့ ဇဝ? . /၅ ၀၅ ပေါ်မှုတည်ပြီး 179111 ) ၅ ဖိုင်ထဲမှာပဲ ဓေ တွေကို

| |
၉၅၂ ချရေးပြီးတော့ စာပိုဒ်ထဲကနေ ဒေ လုပ်ချင်တဲ့အခါမှာ လး} ဆိုတဲ့ ~ နဲ့
ခေါ်တာမျိုးလုပ်ကြရတာ႔ ဒစ 5၀7, 71၀11 တွေက ႕၀2၅1 / ဝ. က
င္လ င္လ လူ ၀၀ ချ င္လ ၂) ဒါ င္လ င္လ င္လ လူ ခါ
သတဓမုတထားတ့ ပုစအတှုငႈး ဝ လုပပေးသွားမုာပၢ[ အဒါက တကယတမး စာတမႈရေးတံ့အခ|မှာ
ရျစေချ၂ င္လ

အရမ်းအဆင်ပြေပါတယ်# လောလောဆယ် မြင်နိုင်ဦးမှာ မဟုတ်ပေမဲ့ ၁ ၅ဝှ လုပ်သွားပါ မြင်လာပါလိမ့်မယ်

326
327 ဖိုင်အတွင်းထဲမှာ ၂၂၂၀၇၈ က ရေးတဲ့ ပုံစံမိလိ

328 ဥပမာ ~ ~


(base) ye@lst-gpu-3090:~/tool/tesseract/y$
```

အထက်မှာ မြင်ရတဲ့ အတိုင်းပါပဲ။ မြန်မာစာ OCR အတွက်က R&D အနေနဲ့ လုပ်စရာတွေ ကျန်ပါသေးတယ်။   

