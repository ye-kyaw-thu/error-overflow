#NLLB Experiments Log

## NLLB API

https://github.com/winstxnhdw/nllb-api  

```
curl -N 'https://winstxnhdw-nllb-api.hf.space/api/v3/translate' \
     -H 'Content-Type: application/json' \
     -d \
     '{
         "text": "Hello world!",
         "source": "eng_Latn",
         "target": "spa_Latn"
      }'
```

test result

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ curl -N 'https://winstxnhdw-nllb-api.hf.space/api/v3/translate' \
text": "Hello world!",
         ">      -H 'Content-Type: application/json' \
>      -d \
>      '{
>          "text": "Hello world!",
>          "source": "eng_Latn",
>          "target": "spa_Latn"
>       }'
{"result":"¡Hola mundo!"}
```

## Testing for Myanmar to English

```
curl -N 'https://winstxnhdw-nllb-api.hf.space/api/v3/translate' \
     -H 'Content-Type: application/json' \
     -d \
     '{
         "text": "လက်ရှိ နိုင်ငံရေး အခြေအနေကြောင့် လူတိုင်းဟာ တရက် တရက် စိတ်ပင်ပန်းနေရတယ်",
         "source": "mya_Mymr",
         "target": "eng_Latn"
      }'
```

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ curl -N 'https://winstxnhdw-nllb-api.hf.space/api/v3/translate' \
>      -H 'Content-Type: application/json' \
>      -d \
>      '{
>          "text": "လက်ရှိ နိုင်ငံရေး အခြေအနေကြောင့် လူတိုင်းဟာ တရက် တရက် စိတ်ပင်ပန်းနေရတယ်",
>          "source": "mya_Mymr",
>          "target": "eng_Latn"
>       }'
{"result":"Everyone is exhausted by the current political climate."}
```

## Testing with Input File

(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ cat nllb-translate.sh

```bash
#!/bin/bash

## NLLB Lib based Translation
## Written by Ye Kyaw Thu, NECTEC, Thailand.
## Usage:
## ./translate.sh --input input.txt --source eng_Latn --target spa_Latn
## ./translate.sh --input input.txt --source eng_Latn --target spa_Latn --output output.txt
## time ./nllb-translate.sh --input data/
## baseline/ref_baseline.txt --source tha_Thai --target mya_Mymr --output output_th-my.txt


# Function to display usage
usage() {
    echo "Usage: $0 --input <inputfile> --source <source_lang> --target <target_lang> [--output <outputfile>]"
    exit 1
}

# Parse command line arguments
INPUT=""
OUTPUT=""
SOURCE=""
TARGET=""

while [[ "$#" -gt 0 ]]; do
    case $1 in
        --input) INPUT="$2"; shift ;;
        --output) OUTPUT="$2"; shift ;;
        --source) SOURCE="$2"; shift ;;
        --target) TARGET="$2"; shift ;;
        *) echo "Unknown parameter passed: $1"; usage ;;
    esac
    shift
done

# Check if input file is provided
if [[ -z "$INPUT" || -z "$SOURCE" || -z "$TARGET" ]]; then
    echo "Error: Input file, source language, and target language are required."
    usage
fi

# Check if input file exists
if [[ ! -f "$INPUT" ]]; then
    echo "Error: Input file does not exist."
    exit 1
fi

# Function to translate text
translate() {
    local text="$1"
    curl -s -N 'https://winstxnhdw-nllb-api.hf.space/api/v3/translate' \
         -H 'Content-Type: application/json' \
         -d "{\"text\": \"$text\", \"source\": \"$SOURCE\", \"target\": \"$TARGET\"}" | jq -r '.result'
}

# Read input file and process each line
if [[ -z "$OUTPUT" ]]; then
    # Output to screen
    while IFS= read -r line; do
        translate "$line"
    done < "$INPUT"
else
    # Output to file
    while IFS= read -r line; do
        translate "$line" >> "$OUTPUT"
    done < "$INPUT"
fi

```

time ./nllb-translate.sh --input data/
baseline/ref_baseline.txt --source tha_Thai --target mya_Mymr --output output_th-my.txt  

```
...
...
...
parse error: Invalid numeric literal at line 1, column 9
parse error: Invalid numeric literal at line 1, column 9
parse error: Invalid numeric literal at line 1, column 9
parse error: Invalid numeric literal at line 1, column 9

parse error: Invalid numeric literal at line 1, column 9
parse error: Invalid numeric literal at line 1, column 9
parse error: Invalid numeric literal at line 1, column 9
parse error: Invalid numeric literal at line 1, column 9
parse error: Invalid numeric literal at line 1, column 9
parse error: Invalid numeric literal at line 1, column 9

real    274m27.019s
user    18m25.834s
sys     1m9.167s
(py3.8) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$
```

Check the translated output file:  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ wc ./output_th-my.txt
  7996  23377 785875 ./output_th-my.txt
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ wc ./data/baseline/ref_baseline.txt
  8063  56900 661580 ./data/baseline/ref_baseline.txt
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$
```

တချို့လိုင်းတွေကိုတော့ ဘာသာပြန်မပေးနိုင်ဘူး ...  
ဒါပေမဲ့ ဒီလောက် စာကြောင်းရေ အများကြီးကို တခါတည်း ဘာသာပြန်ပေးနိုင်တာကတော့ အရမ်းကောင်းတဲ့ API service ပါပဲ။ အသုံးဝင်တယ်။  

ဘာသာပြန်ထားတဲ့ output တချို့ကို လေ့လာကြည့်ခဲ့...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ head -n 30 ./output_th-my.txt
နောက်တစ်ခါ အတိအကျပြောဖို့ စောင့်ပါ။
ဆေးကုသမှုကို လက်ခံလိုက်ပါ
ဟုတ်ပါတယ်၊ ဒါက လစဉ် ဝေဒနာရဲ့ အစပဲဖြစ်ပေမဲ့ ဒီကိစ္စမှာတော့ လစဉ် ဝေဒနာနဲ့ မသက်မသာဖြစ်မှု အပါအဝင် စိတ်ဖိစီးမှု အပိုင်းကို လစဉ် ဝေဒနာနဲ့ မသက်မသာဖြစ်မှု အပိုင်းကို Dimadnolia လို့ခေါ်ပါတယ်။
မျက်လုံးတွေက အနက်ရောင်ပါ။
ဆရာဝန်က သွားတွေထဲမှာ ဘယ်လိုရှိလဲဆိုတာ သိချင်တယ်။
ဓာတ်မှန်ကနေ
လက်ခံလိုက်ပါတယ်။
ကာကွယ်ဆေးတွေလည်း COVID ကို ကာကွယ်ပေးတယ်။
ရုပ်ရှင်ကို ပြန်ကြည့်ပါ
အစ်မ၊ ဟုတ်တယ်၊ အရောင်တောက်တောက်နဲ့ မြင်ရတယ်
လမ်းလျှောက်လိုက်ရင်လည်း နာကျင်တယ် ဆရာ။
သွားတွေကို ချွတ်လိုက်ပါ
ဟုတ်တယ်၊ ဆရာ။
Turnix ကို အပြုသဘော စစ်ဆေးတယ်။
အရောင်တွေ
ဆရာဝန်များရဲ့ သမိုင်းဝင် ဆေးကုသမှု
ကုသမှုမရှိသေးတာ တွေ့ရတယ်
ဒါက နာကျင်ပါတယ်။ ကျေးဇူးပြုပြီး စိတ်ရှည်ပါဦး။
ဒါပေမဲ့ မင်းက မရပ်နိုင်ဘူးလေ။
ကိုယ်ဝန်မတိုင်ခင်မှာ အသားတင်ရောဂါ ရှိတယ်ဆိုပါစို့။ ဟုတ်တယ်နော်။
ကောင်းပြီ၊
ကျွန်မ အိပ်ရာဝင်ခင် နာကျင်နေခဲ့တယ်။
ဟုတ်တယ်နော် ဆရာ။
အင်း၊ အမြဲတမ်းပါ။
ဘာဖြစ်နေတာလဲ။
ဆီးကို သိမ်းထားနိုင်တယ်
အသက်ရှူတာနဲ့ နှလုံးခုန်သံကို ချက်ချင်း စစ်ဆေးပါ။
အေးဆေးပါ။
အတင်းအဓမ္မဖြစ်သူတွေမှာ အခြားလက္ခဏာတွေလည်းရှိတယ်။
ဆရာဝန်ရေ၊ ခင်ဗျား ဘယ်ကိုမဆို သွားလို့ရပါတယ်။
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$
```

tail command နဲ့လည်း ကြည့်ခဲ့ ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ tail -n 30 ./output_th-my.txt
ဒီမှာ နာကျင်နေတယ်၊
ဟုတ်တယ်၊ နှာခေါင်းနဲ့ လည်ပင်းနာတာ ရှိမယ်။
Coyote က ဘာလုပ်နိုင်လဲဆိုတာ ကျွန်မခံစားမိတယ်။
ဒီတော့ သွေးကို စုပ်ယူပါဦး။ အပြင်မှာ စောင့်ပါဦး။
တစ်ကြိမ်မှာ ထွက်တဲ့ ပမာဏက များလွန်းလား။
အပူချိန်လည်း အမြဲတမ်းမြင့်တယ်။
သွေးလွန်တုပ်ကွေးဟာ သွေးလွန်တုပ်ကွေး ဗိုင်းရပ်စ်ကြောင့် ကူးစက်ရောဂါပါ။
ဥပမာ စိတ်ဖိစီးမှု။
ဒဏ်ရာရနေတဲ့နေရာကနေ သံကို ဖယ်ရှားပေးတယ်။
နောက်တော့ ဆရာဝန်က လက်ချောင်းကို ထည့်ပြီး ကြည့်တယ်။
ဒါဆို ဒီဒဏ်ရာက ဘာကိုဆိုလိုတာလဲ ဆရာဝန်တွေက ပြောတာက ဒီဒဏ်ရာက ဘူရီဂျီလိုမျိုးပါ
ကလေးမွေးခန်း။
အားမရှိပါဘူး ဆရာ။
ကျွန်မက "ဟေး"။
အခြေခံတွေချဖို့
ဓာတ်ရောင်ခြည်အဝတ်အစားတွေ ဝတ်လိုက်ပါ
ဒီစိတ်ကူးက အများကြီး ကူညီနိုင်တယ်လို့ ထင်တယ်။
ကိုယ်လက်လှုပ်ရှားမှု အပိုလုပ်တာ
"အဲဒါက ဘာလဲ၊ ငါဘာကိုစားတာလဲ"
ဒါမှမဟုတ် ဆေးဆေးရည်ကို မလိုအပ်ဘဲ သုံးတယ်။
မျက်လုံးတွေထဲမှာ အစက်တွေ မြင်ရတယ်။
ကိုယ်ဝန်ရှိတယ်၊ သေချာတယ်။
မဟုတ်ဘူး၊ ဟုတ်တယ်။
မီးရှို့လိုက်တာလား။
COVID-19 ရောဂါကို တွေ့ရှိရခြင်း (သို့) စစ်ဆေးခြင်းအကြောင်း မိသားစုဝင်တွေကို ပြောဖူးလား။
အတွင်းပိုင်း စစ်ဆေးမှု
စိတ်နဲ့ အပြုအမူကို ကုသခြင်း
ဒါက နာကျင်စရာပါ။
ခင်ဗျားတို့ရဲ့ ဘယ်ဘက်နဲ့ ညာဘက်မှာ မှန်ဘီလူးနဲ့ မှန်ဘီလူးတွေ မတူကြပါဘူး။
ဆွေမျိုးတွေကို ခေါ်လိုက်ပါ ပရော်မုန်းမင်းကို ခေါ်လိုက်ပါ
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$
```

## To Do  

- shell script ကို input, output sentence ကို pair အနေနဲ့ ထုတ်ပေးအောင် ပြင်ရေးလိုက်ရင် တကယ်တမ်း သုံးလို့ ရတဲ့ script ဖြစ်သွားပြီ။ လောလောဆယ် ဗားရှင်းက အထက်မှာ တွေ့ခဲ့ရတဲ့ အတိုင်းပဲ ဘာသာပြန်မပေးနိုင်တဲ့ စာကြောင်းတွေကို ပြန်စစ်ဆေးဖို့ လိုအပ်တာမို့...  

(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ cat ./nllb-translate.sh  

```bash
#!/bin/bash

## NLLB Lib based Translation
## Written by Ye Kyaw Thu, NECTEC, Thailand.
## Usage:
## ./translate.sh --input input.txt --source eng_Latn --target spa_Latn
## ./translate.sh --input input.txt --source eng_Latn --target spa_Latn --output output.txt
## time ./nllb-translate.sh --input data/
## baseline/ref_baseline.txt --source tha_Thai --target mya_Mymr --output output_th-my.txt


# Function to display usage
usage() {
    echo "Usage: $0 --input <inputfile> --source <source_lang> --target <target_lang> [--output <outputfile>] [--delimiter <delimiter>]"
    exit 1
}

# Parse command line arguments
INPUT=""
OUTPUT=""
SOURCE=""
TARGET=""
DELIMITER=$'\t'  # Default delimiter is a tab character

while [[ "$#" -gt 0 ]]; do
    case $1 in
        --input) INPUT="$2"; shift ;;
        --output) OUTPUT="$2"; shift ;;
        --source) SOURCE="$2"; shift ;;
        --target) TARGET="$2"; shift ;;
        --delimiter) DELIMITER="$2"; shift ;;
        *) echo "Unknown parameter passed: $1"; usage ;;
    esac
    shift
done

# Check if input file, source language, and target language are provided
if [[ -z "$INPUT" || -z "$SOURCE" || -z "$TARGET" ]]; then
    echo "Error: Input file, source language, and target language are required."
    usage
fi

# Check if input file exists
if [[ ! -f "$INPUT" ]]; then
    echo "Error: Input file does not exist."
    exit 1
fi

# Function to translate text
translate() {
    local text="$1"
    curl -s -N 'https://winstxnhdw-nllb-api.hf.space/api/v3/translate' \
         -H 'Content-Type: application/json' \
         -d "{\"text\": \"$text\", \"source\": \"$SOURCE\", \"target\": \"$TARGET\"}" | jq -r '.result'
}

# Read input file and process each line
if [[ -z "$OUTPUT" ]]; then
    # Output to screen
    while IFS= read -r line; do
        translated=$(translate "$line")
        echo -e "${line}${DELIMITER}${translated:-$line}"
    done < "$INPUT"
else
    # Output to file
    while IFS= read -r line; do
        translated=$(translate "$line")
        echo -e "${line}${DELIMITER}${translated:-$line}" >> "$OUTPUT"
    done < "$INPUT"
fi

```

```
parse error: Invalid numeric literal at line 1, column 9
parse error: Invalid numeric literal at line 1, column 9
parse error: Invalid numeric literal at line 1, column 9
parse error: Invalid numeric literal at line 1, column 9
parse error: Invalid numeric literal at line 1, column 9
parse error: Invalid numeric literal at line 1, column 9
parse error: Invalid numeric literal at line 1, column 9
parse error: Invalid numeric literal at line 1, column 9
parse error: Invalid numeric literal at line 1, column 9
parse error: Invalid numeric literal at line 1, column 9
parse error: Invalid numeric literal at line 1, column 9

real    268m9.166s
user    18m25.707s
sys     1m8.573s
(py3.8) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$
```

Check the output filesize:  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ wc ./output_th-my.txt
   8063   80883 1452528 ./output_th-my.txt
```

Check the content:  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ head output_th-my.txt
รอ คุย รายละเอียด กับ แพทย์ ผู้ ตรวจ อีก ครั้ง นะ คะ    နောက်တစ်ခါ အတိအကျပြောဖို့ စောင့်ပါ။
ยินยอม เข้า รับ การ รักษา คะ    ဆေးကုသမှုကို လက်ခံလိုက်ပါ
ครับ มัน เพิ่ง เริ่ม มี อาการ ปวด ประจำ เดือน แต่ ใน กรณี ของ คุณ เรียก ว่า ความ เครียด ก่อน มี ประจำ เดือน และ ช่วง เวลา ที่ มา พร้อม กับ ความ เจ็บปวด และ ความ รู้สึก ไม่ สบาย นั้น เรียก ว่า ประจำ เดือน ดิมัดโนลียา     ဟုတ်ပါတယ်၊ ဒါက လစဉ် ဝေဒနာရဲ့ အစပဲဖြစ်ပေမဲ့ ဒီကိစ္စမှာတော့ လစဉ် ဝေဒနာနဲ့ မသက်မသာဖြစ်မှု အပါအဝင် စိတ်ဖိစီးမှု အပိုင်းကို လစဉ် ဝေဒနာနဲ့ မသက်မသာဖြစ်မှု အပိုင်းကို Dimadnolia လို့ခေါ်ပါတယ်။
ตา เป็น สี แดง  မျက်လုံးတွေက အနက်ရောင်ပါ။
พี่ หมอ อยาก เห็น ว่า ข้าง ใน ฟัน มัน เป็น ยัง ไง       ဆရာဝန်က သွားတွေထဲမှာ ဘယ်လိုရှိလဲဆိုတာ သိချင်တယ်။
จาก ภาพ x- ray  ဓာတ်မှန်ကနေ
ยินยอม  လက်ခံလိုက်ပါတယ်။
และ ฉีด วัคซีน ป้องกัน โควิด ครับ       ကာကွယ်ဆေးတွေလည်း COVID ကို ကာကွယ်ပေးတယ်။
เดี๋ยว film ซ้ำ ดู ตำแหน่ง หน่อย        ရုပ်ရှင်ကို ပြန်ကြည့်ပါ
น้อง ใช่ เจอ แบบ ใน รูป สี ใส ๆ အစ်မ၊ ဟုတ်တယ်၊ အရောင်တောက်တောက်နဲ့ မြင်ရတယ်
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$
```

tail command ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ tail ./output_th-my.txt
ฉัน เห็น จุด ๆ ใน ดวง ตา ของ ฉัน        မျက်လုံးတွေထဲမှာ အစက်တွေ မြင်ရတယ်။
ท้อง แน่น       ကိုယ်ဝန်ရှိတယ်၊ သေချာတယ်။
ไม่ มี ค่ะ      မဟုတ်ဘူး၊ ဟုတ်တယ်။
เผา ไป เยอะ ไหม คะ      မီးရှို့လိုက်တာလား။
คุณ ได้ บอก ใคร ใน ครอบครัว เกี่ยว กับ การ วินิจฉัย หรือ การ ตรวจ COVID -19 ของ คุณ     COVID-19 ရောဂါကို တွေ့ရှိရခြင်း (သို့) စစ်ဆေးခြင်းအကြောင်း မိသားစုဝင်တွေကို ပြောဖူးလား။
การ ตรวจ ภาย ใน အတွင်းပိုင်း စစ်ဆေးမှု
การ บำบัด ความ คิด และ พฤติกรรม စိတ်နဲ့ အပြုအမူကို ကုသခြင်း
เจ็บ มาก เลย    ဒါက နာကျင်စရာပါ။
คุณ จะ มี เลนส์ และ แว่นตา ที่ แตกต่าง กัน ทั้ง ด้าน ซ้าย และ ด้าน ขวา ของ คุณ  ခင်ဗျားတို့ရဲ့ ဘယ်ဘက်နဲ့ ညာဘက်မှာ မှန်ဘီလူးနဲ့ မှန်ဘီလူးတွေ မတူကြပါဘူး။
เรียก ญาติ คุณปราโมท เข้า มา ให้ หน่อย ค่ะ      ဆွေမျိုးတွေကို ခေါ်လိုက်ပါ ပရော်မုန်းမင်းကို ခေါ်လိုက်ပါ
```

## Translate Whole Mahidol Corpus

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ time ./nllb-translate.sh --input data/mahidol/th-mahidol.txt --source tha_Thai --target mya_Mymr --output output_th-my_mahidol.txt
```

Running time ...  

```

```



```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ head output_th-my_mahidol.txt
th      th
ทำ ความ สะอาด ริม ขอบ แผล       ဒဏ်ရာရဲ့ အနားကို သန့်ရှင်းအောင်လုပ်ပါ။
ผม เล่น น้ำ ใน ทะเล ครับ        ကျွန်မက ရေထဲမှာ ကစားတယ်။
โรค จมูก อักเสบ จาก ภูมิ แพ้    ဒေသတွင်းက နှာခေါင်းရောင်ရောဂါတွေ
มี อาการ เมื่อ 2 วัน ที่ แล้ว   လွန်ခဲ့တဲ့ နှစ်ရက်က ရောဂါလက္ခဏာတွေ ရှိခဲ့တယ်။
แก้ม ของ เขา บวม และ เจ็บ       သူ့လည်ပင်းက ဝလာပြီး နာနေတယ်၊
ถ้า ส่ง ไม่ ทัน จะ ไม่ ได้ เงิน ครับ    မပို့ရင် ငွေမရဘူး
ต้อง แกว่ง แบบ นี้ กี่ ครั้ง คะ ဒီနည်းနဲ့ ဘယ်နှစ်ကြိမ် လုပ်ရမလဲ။
ใน ทารก หรือ เด็ก จะ ไม่ เจอ อาการ ไอ   ကလေးတွေမှာ အစာအိမ်ရောဂါ မရှိဘူး။
หมอ ใส่ ท่อ ช่วย หายใจ ให้      ဆရာဝန်၊ အသက်ရှူဖို့ ကူညီပါ။
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$
```

during translation check the output:  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ tail ./output_th-my_mahidol.txt
ถ้า ภรรยา จะ คลอด       မိန်းမက ကလေးမွေးရင်
มี ไข้ มา ได้ สี่ห้า วัน แล้ว ใช่ ไหม คะ        ကြက်ဥတွေ ၄-၅ ရက်ကြာလာပြီမို့လား။
คุณ ใช้ ยา ปฏิชีวนะ หรือ ไม่ หาก กิน ยา เข้า ไป อาจ เกิด แผล ใน กระเพาะ ได้     ဆေးတွေ သောက်သင့်သလား မသောက်သင့်ဘူး ဆေးတွေ သောက်လိုက်ရင် အစာအိမ်မှာ အနာတွေ ဖြစ်နိုင်ပါတယ်။
มี อาการ ซึมเศร้า       စိတ်ဓာတ်ကျရောဂါ ရှိတယ်။
เขาม มี แผล นอก ไหม     အပြင်ဘက်က ဒဏ်ရာရှိလား။
สัญญาณ ชีพ ทั่วไป ปกติ ดี       ရောဂါလက္ခဏာများ ပုံမှန်အားဖြင့် ကောင်းမွန်ပါတယ်
อุณหภูมิ สูง กว่า ปกติ มา สิบ สอง หรือ สิบ สาม วัน แล้ว หาก อุณหภูมิ สูง หลัง รอบ เดือน มี โอกาส สูง ที่ คุณ จะ ตั้ง ครรภ์        ၁၂ ရက်၊ ၁၃ ရက်အတွင်း ပုံမှန်ထက် ပိုပူလာရင် ကိုယ်ဝန်ရဖို့ အခွင့်ကောင်းရှိတယ်
เพื่อน ๆ ของ เขา เป็น โรค หัด ไหม       သူ့မိတ်ဆွေတွေ နာမကျန်းလား။
ส่วน อัน นี้ พาสปอร์ต ค่ะ GA 012345678910       ဒီအပိုင်းက နိုင်ငံကူးလက်မှတ်ပါ GA 012345678910
ช่วง ที่ ผ่าน มา ดื่ม น้ำ จาก ที่ ไหน ครับ      မကြာသေးခင်က ရေဘယ်က ရခဲ့လဲ။
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$
```

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ wc output_th-my_mahidol.txt
  4377  44181 793630 output_th-my_mahidol.txt
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ tail ./output_th-my_mahidol.txt
จะ มี สาย น้ำ เกลือ คา ไว้  ရေကြြိုးတွေ ကပ်ထားမယ်။
เลย ไม่ ได้ กิน เลย        ဒီတော့ စားလလိလို့မရဘူး။
แต่ เหมือน มี เป็น มูก ๆ บาง ครรั้ง     ဒါပေမမဲ့ တစ်ခါတစ်လေတော့ အူမကြီးတွေလလိုမျျိုးပေါ့။
งงั้น เดดี๋ยว วัน นนี้    ဒီတော့ ဒီနေ့ပဲလေ။
ตตั้งแต่ เมมื่อ วาน ขณะ ทที่ ผม อยยู่ ห่าง จาก บ้าน ตา ก็ เรริ่ม น้ำ ตา ไหล ตา ของ ผม บวม และ เมมื่อ ผม กลับ ถึง บ้าน ผม พบ ว่า ตา แดง       မနေ့က အိမ်ကထွက်နေတုန်း မျက်ရည်တွေစပြီး ကျလာတယ်၊ အိမ်ပြန်တော့ မျက်လလုံးတွေ မှောင်နေတယ်။
ผม คิด ว่า เธอ ปกติ        သူမဟာ ပပုံမှန်လလိုပဲ
มึน ไป หมด       အားလလုံးကကို မေ့ပစ်လလိုက်ပါ
ถ้า ฉัน อ่าน หนังสือ มัก จะ ถือ หนังสือ ไว้ ใต้ จมูก        စာအုပ်တွေဖတ်နေရင် အမြဲတမ်း နှာခေါင်းအောက်မှာ ထားတယ်။
ตรวจตา ทุก วัน ด้วย        မျက်လလုံးတွေကကိုလည်း နေ့စဉ် စစ်ဆေးပါ။
ก็ อาจ ส่ง ผล ให้ ทารก ใน ครรภ์ ติด เชชื้อ ได้   ကလေးတွေကကို ကူးစက်နနိုင်တယ်
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$
```

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ wc output_th-my_mahidol.txt
   6549   65745 1181542 output_th-my_mahidol.txt
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ tail ./output_th-my_mahidol.txt
เรียก เขา ก็ ไม่ ตอบ    သူ့ကိုခေါ်တယ်၊ သူက မဖြေဘူး။
เคย แท้ง ไหม    ဘယ်တုန်းကမှ စိတ်မပျက်ခဲ့ဘူးလား။
หมอ เข้าใจ ค่ะ  ဆရာ။ သိတယ်နော်
เพื่อ ลด ความ เสี่ยง ของ การ เกิด โรค นะ ครับ   ရောဂါဖြစ်ပွားမှု အန္တရာယ်ကို လျှော့ချဖို့ပါ။
ไม่ เคย มี ใคร รับฟัง หนู จริง ๆ เลย สัก คน     ဘယ်သူမှ ကျွန်မကို တကယ်နားမထောင်ခဲ့ဘူး။
ละองฝอย ของ เสมหะ       အချိုရည်တွေ အမြဲတမ်း
สวัสดี ครับ     မင်္ဂလာပါ။
วัด ส่วน สูง    ဗိမာန်ကြီးရဲ့ အထက်ပိုင်း
ของ โรค นี้ และ เป็น สาเหตุ ทำ ให้ เสีย ชีวิต ได้       ဒီရောဂါရဲ့ အဓိက အကြောင်းရင်းက သေဆုံးမှုပါ။
ฉัน เป็น โรค หอบหืด เรื้อรัง ซึ่ง มี ความ รุนแรง มาก กว่า ปกรติ ကျွန်မမှာ နာတာရှည် ဝေဒနာရှိတယ်၊ ပုံမှန်ထက် ပိုပြင်းထန်တယ်။
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$
```

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ wc output_th-my_mahidol.txt
   7351   73871 1326665 output_th-my_mahidol.txt
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ tail ./output_th-my_mahidol.txt
และ ก่อน มื้อ อาหาร     မစားခင်မှာလည်း
ต่อ ขวด ICD ให้ หมอ แบบ 3 ขวด เลย ค่ะ   ICD တစ်ဘူးကို ဆရာဝန်သုံးဘူးနဲ့ပဲ ပေးလိုက်တာလေ။
นั่น แหละ คุณ ป้า       ဟုတ်ကဲ့၊ အဒေါ်။
ถ้า ฉัน ยืด หลัง ก็ เจ็บ        ကျွန်မ ဆွဲဆန့်လိုက်ရင် ကျောက နာပါတယ်။
ไม่ มี . ดิฉัน สังเกต เห็น อุณหภูมิ ร่างกาย ขอ เปลี่ยน ไป       အပူချိန်ကို စောင့်ကြည့်နေတယ်၊ ပြောင်းလိုက်ပါ
ก่อน การ เดินทาง ไป ยัง ประเทศ ใน แถบ เอเชีย    အာရှတိုက်ကို မသွားခင်
อุจจาระมี มูกเลือด ปน มั้ย ครับ အူဂျာဟာ နှာခေါင်း သွေးထွက်နေလား။
กิน นม แล้ว อ้วก เมื่อ เช้า     နို့သောက်ပြီး မနက်မှာ အန်တယ်။
ผม ตัว สั่น และ ไม่ มี แรง      ကျွန်မ တုန်ခါပြီး အားနည်းနေတယ်။
แล้ว กด ท้อง ให้ ดัน มา ทาง ด้าน ยอ ดอก ဒီနောက်မှာ အပေါ်ဘက်ကို တွန်းပေးပါ။
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$
```

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ tail ./output_th-my_mahidol.txt
ไม่ ควร เสีย เวลา กับ การ พยายาม เอา น้ำ ออก จาก ปอด หรือ กระเพาะ อาหาร ใน ระหว่าง CPR  CPR လုပ်နေစဉ် အဆုတ်နဲ့ အစာအိမ်ထဲက ရေကို ထုတ်ဖို့ အချိန်မကုန်ပါနဲ့
งั้น เดี๋ยว วัน นี้     ဒီတော့ ဒီနေ့ပဲလေ။
เวลา แปรง ให้ หัน ปลาย แปรง เอียง เข้า หา ขอบ เหงือก    အပြင်ကို လှည့်လိုက်၊ အနားကို လှည့်လိုက်၊ အနားကို လှည့်လိုက်။
ขอ ดู โรค เก๊าท์ ด้วย เลย       ဂိတ်ရောဂါကို ကြည့်ပါ။
ความ พิการ ตั้งแต่ กำเนิด อย่าง รุนแรง  အချစ်ဟာ မွေးရာပါ အဓမ္မဖြစ်စဉ်ပါ။
เป็น อะไร มา ครับ วัน นี้       ဒီနေ့က ဘာလဲ။
มี ไข้ สูง ตั้งแต่ 38 องศา เซลเซียส ขึ้น ไป โดย ไม่ ลด ลง       အပူချိန်က ၃၈ ဒီဂရီ စင်တီဂရိတ်ထက် ပိုမြင့်ပြီး မကျဆင်းဘူး။
หรือ อีก วิธี นึง ให้ เข้า ด้าน หลัง    နောက်တစ်ဖက်ကို ဝင်ဖို့ နည်းလမ်းတစ်ခုရှိလား။
หรือ เข้า ปาก   ဒါမှမဟုတ် ပါးစပ်ထဲ ထည့်လိုက်တာမျိုးပေါ့။
ดูด ผิด วิธี    ဘယ်လိုလုပ်ပြီး
```

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ wc output_th-my_mahidol.txt
  10243  102481 1841622 output_th-my_mahidol.txt
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ tail ./output_th-my_mahidol.txt
ก็ กัน ไว้ ก่อน ဒါဆို အရင်ထားလိုက်ပါဦး။
ได้ ใช้ อุปกรณ์ อะไร ร่วม กับ ผู้ อื่น รึ เปล่า ได้ ใช้ อุปกรณ์ อะไร ร่วม กับ ผู้ อื่น รึ เปล่า
หรือ ปวด ด้าน ล่าง ซ้าย หรือ ขวา แบบ นี้        ဒါမှမဟုတ် ဘယ်ဘက်၊ ညာဘက် အောက်ဘက်မှာ နာကျင်မှုမျိုးပေါ့။
มี อะไร ให้ หมอ ช่วย คะ ဆရာဝန်က ဘာကူညီပေးနိုင်လဲ။
เลย จะ ขอ นัด กลับ มา ดู ใหม่ อีก 1 เดือน ครับ  ဒီတော့ နောက်တစ်လလောက် ပြန်လာဖို့ တောင်းဆိုပါတယ်။
ระหว่าง นี้ ก็ รักษา ตาม อาการ ไป ก่อน  ဒီကာလအတွင်းမှာ ရောဂါလက္ခဏာတွေကို ကုသဖို့ပါ။
อัน นั้น ต้อง ไป คุย กับ หมอ ทำ ครอบ ต่างหาก ค่า        အဲဒါဟာ မိသားစု ဆရာဝန်နဲ့ တွေ့ဆုံဖို့ စျေးကြီးပါတယ်။
แผล นี่ เจอ หลาย แผล เลย นะ ครับ        ဒီဒဏ်ရာတွေက အများကြီးပါ။
ที่ นี้ เอา ลิ้น ไป แตะ แก้ม ซ้าย       ဒီမှာ လက်သည်းကို ဘယ်ဘက်ပါးစပ်မှာ ရိုက်လိုက်ပါ။
หรือ ทำ อะไร ไหม ครับ หมอ       ဒါမှမဟုတ် ဘာလုပ်မလဲ။
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$
```

keep checking ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ wc output_th-my_mahidol.txt
  33372  332691 5982409 output_th-my_mahidol.txt
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ tail ./output_th-my_mahidol.txt
ห้าม หยุด ไป เอง นะ ครับ        မရပ်ပါနဲ့၊ မရပ်ပါနဲ့။
อันตราย ครับ    အန္တရာယ်များပါတယ်။
ตอน ล้ม ကျသွားတဲ့အခါ
ช่วง นี้ อยู่ บ้าน คุณ ยาย ทาน อาหาร ได้ ปกติ ดี ไหม ค่ะ        အခု အိမ်မှာနေတုန်း၊ အဖိုးက ပုံမှန်ကျွေးတာ ကောင်းလား။
ชื่อ บุษกร ค่ะ  ဘူးဂဲလို့ခေါ်တယ်။
นอน ไม่ ค่อย หลับ       အိပ်မပျော်ဘူး။
ที่ ทำ งาน จะ โอเค ไหม ครับ     အလုပ်မှာ အဆင်ပြေမလား
บาง ครั้ง หกล้ม แล้ว เคย มี แผล ครับ    တစ်ခါတစ်လေမှာ အမာရွတ်တွေ ရှိခဲ့တယ်။
มัน ไม่ สบาย ท้อง มาก กว่า ครับ ဒါက ပိုမသက်သာပါဘူး။
ส่วน สูง ของ คุณ คือ 170 เซนติเมตร นะ คะ        ခင်ဗျားရဲ့ အမြင့်က ၁၇၀ စင်တီမီတာပါ။
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$
```

Confirmation with Google Translate:  

```
Don't stop by yourself.
It's dangerous.
When I fell
I'm at my grandmother's house right now. Can I eat normally?
My name is Busakorn.
I can't sleep well.
Is the workplace okay?
Sometimes I fall down and get wounds.
It's more uncomfortable for my stomach.
Your height is 170 centimeters.
```

မဆိုးဘူး ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ wc output_th-my_mahidol.txt
  39906  397124 7143580 output_th-my_mahidol.txt
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ tail output_th-my_mahidol.txt
มี ไข้  ကြက်ဥတွေရှိတယ်
เหมือน จุก เสียด แน่น อ่ะหมอ    ဒါက စိတ်ဖိစီးမှုလိုမျိုးပေါ့။
ความ เข้มข้น ของ เลือด สูง ขึ้น จาก เดิม 5 - 10 %       သွေးဓာတ်ဟာ ၅ ရာခိုင်နှုန်းကနေ ၁၀ ရာခိုင်နှုန်းအထိ မြင့်တက်လာပါတယ်။
แผล เปิด บาดเจ็บ        အပေါက်ဖွင့်၊ ဒဏ်ရာ။
การ ใช้ ไหม ขัด ฟัน     အသားအရေကို ချည်နှောင်ခြင်း
มี คน รอบ ตัว เป็น ไข้ เลือด ออก ไหม ครับ       လူတစ်ယောက်က သွေးထွက်နေတဲ့ ကြက်ဥတွေ ဝန်းရံထားလား။
ญาติ ทำ อะไร ไม่ ถูก เลย ค่ะ    ဆွေမျိုးတွေက ဘာလုပ်တာ မှားနေလဲ
ไม่ มี ครับ หมอ မဟုတ်ပါဘူး၊ ဟုတ်ပါတယ် ဆရာ။
ว่า แต่ ส่วน อื่น โดน อะไร ไหม ครับ     ဒါပေမဲ့ အခြားအပိုင်းတွေက ဘာလဲ။
ยาย มา กับ ใคร คะ วัน นี้       ဒီနေ့ ဘယ်သူနဲ့လာလဲ။
```

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ wc ./output_th-my_mahidol.txt
  52293  520873 9370016 ./output_th-my_mahidol.txt
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ tail ./output_th-my_mahidol.txt
เขา ไม่ รู้ เขา กลืน ลง ไป เลย ค่ะ      သူ မသိဘူး၊ သူ မျိုချလိုက်တာလေ။
เป็น ยัง ไง บ้าง คะ     ဘယ်လိုလဲ၊ ဘာလဲ၊ ဘာလဲ၊
3 . หลีกเลี่ยง การ ใช้ สาร เสพ ติด      (၃) ဆေးဝါးတွေ မသုံးပါနဲ့
มี เลือด ออก ไหม        သွေးထွက်နေတာလား။
ถ้า ไม่ รักษา อาจ ถึง ขั้น เสีย ชีวิต ได้       ကုသမှုမပြုရင် သေလောက်တယ်။
หรือ การ ซื้อ บริการ ทาง เพศ ครับ       ဒါမှမဟုတ် လိင်ဝန်ဆောင်မှု ဝယ်တာမျိုးပေါ့။
เพราะ ผู้ ป่วย ชรา มาก แล้ว     လူနာတွေဟာ အသက်ကြီးလာကြလို့ပါ။
จะ ได้ วินิจฉัย โรค ได้ แม่นยำ ค่ะ      ရောဂါကို တိကျစွာ ရှာဖွေနိုင်တယ်
เกิด จาก การ มี คู่ นอน หลาย คน ครับ    အိပ်စက်မှု အများအပြားကြောင့်ပါ။
และ ให้ ความ ชุ่มชื้น แก่ เนื้อเยื่อ    တစ်ရှူးတွေကို စိုပြေစေပါတယ်။
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$
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
## Prepare SCB Th-My Corpus 

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020$ ls
apdf.csv                          generated_reviews_yn.csv  paracrawl.csv
assorted_government.csv           mozilla_common_voice.csv  task_master_1.csv
generated_reviews_crowd.csv       msr_paraphrase.csv        thai_websites.csv
generated_reviews_translator.csv  nus_sms.csv               wikipedia.csv
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020$ wc *
    13504    681315  14897284 apdf.csv
    25399   1920530  35866098 assorted_government.csv
    24588    413188   7044457 generated_reviews_crowd.csv
   133331   1999051  34088348 generated_reviews_translator.csv
   280209   4119639  71364652 generated_reviews_yn.csv
    33798    282410   5209522 mozilla_common_voice.csv
    10372    237180   4245376 msr_paraphrase.csv
    43751    516900   8503200 nus_sms.csv
    60040   1782344  31001894 paracrawl.csv
   222734   2510145  37536949 task_master_1.csv
   120281  11860714 186814672 thai_websites.csv
    33757   1773040  33898791 wikipedia.csv
  1001764  28096456 470471243 total
```

(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre$ cat split_src_tgt.py  

```python
"""

For splitting source and target files.
Written by Ye Kyaw Thu, LST Lab., Myanmar.
Last updated: 2 June 2024
Usage: python split_src_tgt.py --input wikipedia.csv

"""
import argparse
import csv
import os

def split_src_tgt(input_file):
    # Extract the base name without the extension
    base_name = os.path.splitext(input_file)[0]

    # Define output file names
    src_file = f"{base_name}.src"
    tgt_file = f"{base_name}.tgt"

    print(f"Input file: {input_file}")  # Debug print
    print(f"Source file: {src_file}")   # Debug print
    print(f"Target file: {tgt_file}")   # Debug print

    # Open the input file and the two output files
    with open(input_file, 'r', encoding='utf-8') as infile, \
         open(src_file, 'w', encoding='utf-8') as src_outfile, \
         open(tgt_file, 'w', encoding='utf-8') as tgt_outfile:

        reader = csv.reader(infile)
        next(reader)  # Skip the header

        for row in reader:
            if len(row) != 2:
                continue
            src_outfile.write(row[0] + '\n')
            tgt_outfile.write(row[1] + '\n')

def main():
    parser = argparse.ArgumentParser(description="Split source and target languages into separate files.")
    parser.add_argument('--input', required=True, help="Input CSV file")

    args = parser.parse_args()

    split_src_tgt(args.input)

if __name__ == "__main__":
    main()

```

(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre$ cat run_split.sh  

```bash
#!/bin/bash

# Directory containing the CSV files
DIR="/home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre"

# Absolute path to the Python script
PYTHON_SCRIPT="$DIR/split_src_tgt.py"

# Iterate over each CSV file in the directory
for FILE in "$DIR"/*.csv; do
    # Print the file being processed (for debugging)
    echo "Processing file: $FILE"
    # Run the Python script for each file
    python "$PYTHON_SCRIPT" --input "$FILE"
done

```

Running shell script for splitting all .csv files as follows:  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre$ time ./run_split.sh
Processing file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/apdf.csv
Input file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/apdf.csv
Source file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/apdf.src
Target file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/apdf.tgt
Processing file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/assorted_government.csv
Input file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/assorted_government.csv
Source file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/assorted_government.src
Target file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/assorted_government.tgt
Processing file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/generated_reviews_crowd.csv
Input file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/generated_reviews_crowd.csv
Source file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/generated_reviews_crowd.src
Target file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/generated_reviews_crowd.tgt
Processing file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/generated_reviews_translator.csv
Input file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/generated_reviews_translator.csv
Source file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/generated_reviews_translator.src
Target file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/generated_reviews_translator.tgt
Processing file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/generated_reviews_yn.csv
Input file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/generated_reviews_yn.csv
Source file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/generated_reviews_yn.src
Target file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/generated_reviews_yn.tgt
Processing file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/mozilla_common_voice.csv
Input file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/mozilla_common_voice.csv
Source file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/mozilla_common_voice.src
Target file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/mozilla_common_voice.tgt
Processing file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/msr_paraphrase.csv
Input file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/msr_paraphrase.csv
Source file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/msr_paraphrase.src
Target file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/msr_paraphrase.tgt
Processing file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/nus_sms.csv
Input file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/nus_sms.csv
Source file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/nus_sms.src
Target file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/nus_sms.tgt
Processing file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/paracrawl.csv
Input file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/paracrawl.csv
Source file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/paracrawl.src
Target file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/paracrawl.tgt
Processing file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/task_master_1.csv
Input file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/task_master_1.csv
Source file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/task_master_1.src
Target file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/task_master_1.tgt
Processing file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/thai_websites.csv
Input file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/thai_websites.csv
Source file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/thai_websites.src
Target file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/thai_websites.tgt
Processing file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/wikipedia.csv
Input file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/wikipedia.csv
Source file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/wikipedia.src
Target file: /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/wikipedia.tgt

real    0m6.765s
user    0m5.967s
sys     0m0.799s
```

check the splitted source, target files:  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre$ wc *.src
    13503    576073   3743814 apdf.src
    25398   1491273   9436962 assorted_government.src
    24587    381682   2054783 generated_reviews_crowd.src
   133330   1850739   9956384 generated_reviews_translator.src
   280208   3839707  20714928 generated_reviews_yn.src
    33797    269883   1488739 mozilla_common_voice.src
    10371    196263   1209239 msr_paraphrase.src
    43750    439827   2222243 nus_sms.src
    60039   1476155   8786155 paracrawl.src
   222733   2134082  11209611 task_master_1.src
   120280   8589467  51897517 thai_websites.src
    33756   1392779   8826986 wikipedia.src
  1001752  22637930 131547361 total
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre$ wc *.tgt
    13503    118744  11128630 apdf.tgt
    25398    454654  26379539 assorted_government.tgt
    24587     56092   4963984 generated_reviews_crowd.tgt
   133330    281641  24029289 generated_reviews_translator.tgt
   280208    560139  50417061 generated_reviews_yn.tgt
    33797     46323   3701273 mozilla_common_voice.tgt
    10371     51287   3011626 msr_paraphrase.tgt
    43750    120822   6265828 nus_sms.tgt
    60039    366227  22126733 paracrawl.tgt
   222733    598795  26143691 task_master_1.tgt
   120280   3391092 134849854 thai_websites.tgt
    33756    414016  24960385 wikipedia.tgt
  1001752   6459832 337977893 total
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre$
```

ဖိုင်ရဲ့ content ကိုလည်း စစ်ကြည့်ခဲ့ ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre$ head -n 3 wikipedia.src
Palestine at the 2004 Summer Olympics
Palestine competed at the 2004 Summer Olympics in Athens, Greece, from 13 to 29 August 2004.
Pakistan at the 2004 Summer Olympics
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre$
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre$ head -n 3 wikipedia.tgt
ปาเลสไตน์ในโอลิมปิกฤดูร้อน 2004
ปาเลสไตน์ในโอลิมปิกฤดูร้อน 2004 ปาเลสไตน์ เข้าร่วมแข่งขันกีฬาโอลิมปิกฤดูร้อนครั้งที่ 28 ค.ศ. 2004 (พ.ศ. 2547) ณ กรุงเอเธนส์ ประเทศกรีซระหว่างวันที่ 13 – 29 สิงหาคม พ.ศ. 2547
ประเทศปากีสถานในโอลิมปิกฤดูร้อน 2004
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre$
```

## Translation of SCB Corpus into Myanmar (from English)  

Reference:  
time ./nllb-translate.sh --input ./data/scb/scb-mt-en-th-2020/pre/apdf.src --source eng_Latn --target mya_Mymr --output ./scb-my/from_en/apdf.my

I have to run following command:  

time ./nllb-translate.sh --input ./data/scb/scb-mt-en-th-2020/pre/generated_reviews_yn.src --source eng_Latn --target mya_Mymr --output ./scb-my/from_en/generated_reviews_yn.my


Prepare a shell script as follows:  

(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ cat ./run4scb.sh  

```bash
#!/bin/bash

# Base directory for input files
INPUT_DIR="/home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre"

# Directory for output files
OUTPUT_DIR="/home/ye/ye/exp/gpt-mt/nllb/scb-my/from_en"

# Create the output directory if it doesn't exist
mkdir -p "$OUTPUT_DIR"

# Iterate over each .src file in the input directory
for FILE in "$INPUT_DIR"/*.src; do
    # Extract the base filename without the extension
    BASENAME=$(basename "$FILE" .src)

    # Define the output file name
    OUTPUT_FILE="$OUTPUT_DIR/$BASENAME.my"

    # Print the command being executed (for debugging)
    echo "Running nllb-translate.sh for $FILE"

    # Run the translation command
    time ./nllb-translate.sh --input "$FILE" --source eng_Latn --target mya_Mymr --output "$OUTPUT_FILE"
done

```

Running the shell script ... 

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ time ./run4scb.sh
Running nllb-translate.sh for /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/apdf.src
parse error: Invalid numeric literal at line 1, column 9
parse error: Invalid numeric literal at line 1, column 9
parse error: Invalid numeric literal at line 1, column 9
```

Checking ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my/from_en$ cat apdf.my
FAR LEFT: Indonesian National Police Chief Tito Karnavian, from left, Philippine National Police Chief Ronald Dela Rosa and Royal Malaysian Police Inspector General Khalid Abu Bakar link arms before the Trilateral Security Meeting in Pasay city, southeast of Manila, Philippines, in June 2017. [THE ASSOCIATED PRESS]  FAR LEFT: Indonesian National Police Chief Tito Karnavian, from left, Philippine National Police Chief Ronald Dela Rosa and Royal Malaysian Police Inspector General Khalid Abu Bakar link arms before the Trilateral Security Meeting in Pasay city, southeast of Manila, Philippines, in June 2017. [THE ASSOCIATED PRESS]
(Pictured: A rocket believed to be a Hwasong missile such as the one used in a May 2017 North Korean test is displayed at a military parade in Pyongyang in April 2017.)To deter such conflict, Wee emphasized that the regular deployment of U.S. strategic assets was discussed at KIDD and that both sides “highlighted the importance of the deployment of the Terminal High Altitude Area Defense (THAAD) system.” (ဓာတ်ပုံတွင်: ၂၀၁၇ ခုနှစ် မေလတွင် မြောက်ကိုရီးယားက စမ်းသပ်မှုတွင် အသုံးပြုခဲ့သည့် Hwasong ဒုံးကျည်ကဲ့သို့သော ဒုံးကျည်ကို ၂၀၁၇ ခုနှစ် ဧပြီလတွင် ပယင်းယန်းမြို့ရှိ စစ်ရေးပြပွဲတွင် ပြသထားသည်။) ထိုသို့သော ပဋိပက္ခကို တားဆီးရန်အတွက် အမေရိကန်၏ မဟာဗျူဟာဆိုင်ရာ အရင်းအမြစ်များကို ပုံမှန် တပ်ဆင်ရန် KIDD တွင် ဆွေးနွေးခဲ့ကြောင်း၊ နှစ်ဖက်စလုံးက Terminal High Altitude Area Defense (THAAD) စနစ်ကို တပ်ဆင်ရန် အရေးကြီးကြောင်း <unk> အလေးပေးပြောကြားခဲ့သည်။
(Pictured: From left, Indian Air Commander Ak Chourasia; South Korean Capt. Won Seok Kang; Indonesian Lt. Col. Luhut Bernandus Sidabariba; Thai Maj. Gen. Jaras Panyadee, chief of staff of 3rd Army Area; Thai Lt. Gen. Siravuth Wongkantee, director of Joint Civil Affair Royal Thai Armed Forces; Joseph Martin, director of the Center for Excellence in Disaster Management and Humanitarian Assistance; Singaporean Lt. Col. Ho Wan Huo; Japanese Col. Masanori Koide; and Chinese Lt. Col. Zhou Ming pose for a photo during the second annual Humanitarian Assistance and Disaster Relief Tabletop Exercise as part of the 38th annual Thai-U.S. co-sponsored Cobra Gold Exercise in February 2019.) (Pictured: From left, Indian Air Commander Ak Chourasia; South Korean Capt. Won Seok Kang; Indonesian Lt. Col. Luhut Bernandus Sidabariba; Thai Maj. Gen. Jaras Panyadee, chief of staff of 3rd Army Area; Thai Lt. Gen. Siravuth Wongkantee, director of Joint Civil Affair Royal Thai Armed Forces; Joseph Martin, director of the Center for Excellence in Disaster Management and Humanitarian Assistance; Singaporean Lt. Col. Ho Wan Huo; Japanese Col. Masanori Koide; and Chinese Lt. Col. Zhou Ming pose for a photo during the second annual Humanitarian Assistance and Disaster Relief Tabletop Exercise as part of the 38th annual Thai-U.S. co-sponsored Cobra Gold Exercise in February 2019.)
(Pictured: Left to right, Australia’s Defence Minister Marise Payne, Malaysia’s Defence Minister Hishammuddin Tun Hussein, Singapore’s Defence Minister Ng Eng Hen, New Zealand’s Defence Minister Mark Mitchell and Britain’s High Commissioner to Singapore Scott Wightman attend the Five Power Defence Arrangement news conference in Singapore on June 2, 2017.) (Pictured: Left to right, Australia’s Defence Minister Marise Payne, Malaysia’s Defence Minister Hishammuddin Tun Hussein, Singapore’s Defence Minister Ng Eng Hen, New Zealand’s Defence Minister Mark Mitchell and Britain’s High Commissioner to Singapore Scott Wightman attend the Five Power Defence Arrangement news conference in Singapore on June 2, 2017.)
(Pictured: A man watches the live-stream transmission of released Indian pilot Wing Cmdr. Abhinandan Varthaman at Wagah border crossing in Punjab on March 1, 2019.)      (ဓာတ်ပုံ - ၂၀၁၉ ခုနှစ် မတ်လ ၁ ရက်နေ့တွင် ပန်ဂျပ်ပြည်နယ် ဝဂါနယ်စပ်ဂိတ်တွင် လွတ်မြောက်လာသော အိန္ဒိယလေယာဉ်မှူး ဗိုလ်မှူးကြီး အဗိနန္ဒန်ဗာထမန်၏ တိုက်ရိုက်လွှင့်လွှင့်မှုကို ကြည့်ရှုနေသော အမျိုးသားတစ်ဦး)
(Pictured: Rohingya Muslims, who left Burma for Bangladesh, make their way to a refugee camp in Bangladesh in mid-November 2017.) (ဓာတ်ပုံ- ၂၀၁၇ ခုနှစ် နိုဝင်ဘာလလယ်ပိုင်းတွင် မြန်မာနိုင်ငံမှ ဘင်္ဂလားဒေ့ရှ်နိုင်ငံသို့ ထွက်ခွာလာသော ရိုဟင်ဂျာ မွတ်စလင်များ ဘင်္ဂလားဒေ့ရှ်နိုင်ငံရှိ ဒုက္ခသည်စခန်းသို့ သွားရောက်နေစဉ်)
(Pictured: A lab technician holds a gene-edited macaque, which was used to make five cloned monkeys, at the Institute of Neuroscience of the Chinese Academy of Sciences in Shanghai, China, in January 2019.)      (ဓာတ်ပုံ- ၂၀၁၉ ခုနှစ် ဇန်နဝါရီလတွင် တရုတ်နိုင်ငံ ရှန်ဟိုင်းမြို့ရှိ တရုတ်သိပ္ပံတက္ကသိုလ် အာရုံကြောသိပ္ပံဌာနတွင် ဗီဇပြုပြင်ထားသော မျောက်ငါးကောင်ကို လက်ကိုင်ကိုင်ထားသော ဓာတ်ခွဲခန်းနည်းပညာရှင်)
(Pictured: South Korean Army Soldiers talk in front of a UAV at an aviation school in Nonsan, South Korea.)The new systems, set to roll out sometime in 2017, have been years in development.       (ဓာတ်ပုံ - တောင်ကိုရီးယား စစ်တပ်သားများ တောင်ကိုရီးယားနိုင်ငံ နွန်ဆန်မြို့ရှိ လေကြောင်းသင်တန်းကျောင်းတွင် UAV ရှေ့တွင် စကားပြောဆိုနေသည်)
(Pictured: Papua New Guinea Defence Force Soldiers, foreground, stand with U.S. Marines and Sailors during Exercise Koa Moana in June 2016.)      (ဓာတ်ပုံ: ၂၀၁၆ ဇွန်လတွင် ပြုလုပ်သော ကိုအိုအိုနားလေ့ကျင့်ခန်းအတွင်း အမေရိကန်ရေတပ်သားများနှင့်အတူ ရှေ့တန်းတွင် ရပ်နေသော ပပူအာနယူးဂီနီ ကာကွယ်ရေးတပ်ဖွဲ့ဝင်များ)
(Pictured: U.S. Navy Capt. Randy Van Rossum, left, Pacific Partnership 2019 (PP19) mission commander, receives a gift from Philippine Navy Rear Adm. Samuel Felix, Armed Forces of the Philippines, J9, deputy chief of staff, during the PP19 closing ceremony to conclude the Philippines mission stop.)    (ဓာတ်ပုံတွင် အမေရိကန်ရေတပ်မှူး Randy Van Rossum၊ ဘယ်ဘက်၊ ပစိဖိတ်ပူးပေါင်းဆောင်ရွက်မှု ၂၀၁၉ (PP19) တာဝန်မှူး၊ ဖိလစ်ပိုင်ရေတပ်မှ ဗိုလ်မှူးချုပ်ကြီး Samuel Felix၊ ဖိလစ်ပိုင်တပ်မတော်၊ J9, ဒုဗိုလ်ချုပ်မှူးကြီးမှူးကြီးမှ လက်ဆောင်တစ်လက်ကို PP19 ပိတ်သိမ်းပွဲအခမ်းအနားတွင် လက်ခံရရှိသည်။)
(Pictured: South Korean elementary schoolchildren wear gas masks during a civil defense drill at a Seoul shelter.)        (ဓာတ်ပုံ: တောင်ကိုရီးယား အခြေခံပညာကျောင်းသားများက ဆူးလ်မြို့ရှိ ခိုလှုံရာတစ်ခုတွင် ပြည်သူ့ကာကွယ်ရေးလေ့ကျင့်မှုတစ်ခုအတွင်း ဓာတ်ငွေ့မျက်နှာဖုံးများ ဝတ်ဆင်ထားသည်။)
(Pictured: EU Trade Commissioner Cecilia Malmstrom links arms with Philippine Trade Secretary Ramon Lopez, second from left, Vietnamese Minister of Industry and Trade Tran Tuan Anh, left, and ASEAN Secretary-General Le Luong Minh at a news briefing in the Philippines.)
(ဓာတ်ပုံတွင်- အီးယူကုန်သွယ်ရေးကော်မရှင်ဝင် Cecilia Malmstrom သည် ဖိလစ်ပိုင်ကုန်သွယ်ရေးဝန်ကြီး Ramon Lopez နှင့် လက်တွဲလက်တွဲသည်။
(Pictured: Australian Defense Minister Marise Payne, left, speaks as Foreign Minister Julie Bishop listens during their news conference at the border village of Panmunjom in Paju, South Korea, in October 2017.)  (ဓာတ်ပုံတွင်: ဩစတြေးလျ ကာကွယ်ရေးဝန်ကြီး မရီဇက် ပင်း (ဘယ်) သည် ၂၀၁၇ ခုနှစ် အောက်တိုဘာလတွင် တောင်ကိုရီးယားနိုင်ငံ ပါဂျူးမြို့နယ်ရှိ ပန်မွန်ဂျုံနယ်စပ်ကျေးရွာတွင် သတင်းစာရှင်းလင်းပွဲတွင် နိုင်ငံခြားရေးဝန်ကြီး ဂျူလီဘစ်ရှပ်၏ စကားပြောဆိုမှုကို နားထောင်နေစဉ်)
```

checking ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my/from_en$ wc apdf.my
   49  2552 38434 apdf.my
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my/from_en$ tail ./apdf.my
(Pictured: A U.S. Air Force B-52 Stratofortress bomber prepares for takeoff from Andersen Air Force Base in Guam in March 2018.)  (ဓာတ်ပုံ: ၂၀၁၈ မတ်လတွင် ဂွမ်ရှိ အန်ဒါဆန်လေတပ်စခန်းမှ စတင်ပျံသန်းရန် ပြင်ဆင်နေသော အမေရိကန်လေတပ် B-52 Stratofortress ဗုံးခွဲရေးလေယာဉ်)
(Pictured: The Philippine Navy’s frigate BRP Gregorio del Pilar, right, and another ship are shown anchored near the island of Thitu in the disputed Spratly Islands.)    (ဓာတ်ပုံတွင် - ဖိလစ်ပိုင်ရေတပ်၏ BRP Gregorio del Pilar ရေယာဉ်ငယ်နှင့် အခြားသင်္ဘောတစ်စင်းသည် အငြင်းပွားဖွယ်ရှိသော စပရတ်လီကျွန်းများရှိ Thitu ကျွန်းအနီးတွင် မြစ်ဆုံထားသည်။)
(Pictured: In this May 21, 2019, photo, staff monitor fishing vessels in real time at a state-of-the-art surveillance center in Bangkok, one of seven in the Indo-Pacific region.) (ဓာတ်ပုံ: ၂၀၁၉ ခုနှစ် မေလ ၂၁ ရက်နေ့က ရိုက်ထားသော ဓာတ်ပုံတွင် အိန္ဒိယ-ပစိဖိတ်ဒေသရှိ ၇ ခုအနက် တစ်ခုဖြစ်သော ဘန်ကောက်မြို့ရှိ အဆင့်မြင့် စောင့်ကြည့်ရေးစင်တာတွင် ငါးဖမ်းသင်္ဘောများကို အချိန်နှင့်တပြေးညီ စောင့်ကြည့်နေသည်။)
(Pictured: Australian Prime Minister Scott Morrison, right, meets with NATO Secretary-General Jens Stoltenberg in Sydney, Australia, on August 7, 2019.)  (ဓာတ်ပုံ - ဩစတြေးလျဝန်ကြီးချုပ် စကော့ မော်ရစ်ဆင်၊ ညာဘက်၊ ၂၀၁၉ ခုနှစ် သြဂုတ်လ ၇ ရက်နေ့က သြစတြေးလျနိုင်ငံ၊ ဆီဒနီမြို့တွင် နိုတာအို အထွေထွေအတွင်းရေးမှူး ဂျင်စ်စတိုလ်တင်ဘတ်နှင့် တွေ့ဆုံစဉ်)
(Pictured, Buddhist monks prepare portraits of the king for a ritual ceremony in Bangkok.)[စာမျက်နှာ ၂၇ ပါ ရုပ်ပုံ]
Foodnavigator-asia.com says the rice is specifically engineered for cultivation in countries such as Indonesia, the Philippines and Bangladesh to reduce vitamin A deficiencies.  အိန္ဒိယ၊ ဖိလစ်ပိုင်နှင့် ဘင်္ဂလားဒေ့ရှ်နိုင်ငံများတွင် ဗီတာမင်အေ ချို့တဲ့မှု လျော့နည်းစေရန် ဆန်ကို သီးသန့် ပြုပြင်ထုတ်လုပ်ထားကြောင်း Foodnavigator-asia.com က ဆိုသည်။
Footnote: Japanese Prime Minister Shinzo Abe delivered this speech during the opening session of the Sixth Tokyo International Conference on African Development in Nairobi, Kenya, in August 2016. It has been edited for publication.     အောက်ခြေမှတ်ချက်: ဂျပန်ဝန်ကြီးချုပ် ရှင်ဇိုအာဘေးသည် ၂၀၁၆ ခုနှစ် သြဂုတ်လတွင် ကင်ညာနိုင်ငံ နိုင်ရိုဘီမြို့တွင် ကျင်းပခဲ့သော အာဖရိကဖွံ့ဖြိုးတိုးတက်ရေးဆိုင်ရာ ဆဌမ တိုကျိုနိုင်ငံတကာညီလာခံ၏ ဖွင့်ပွဲအစည်းအဝေးတွင် ဤဟောပြောချက်ကို ပြုလုပ်ခဲ့သည်။
GetUp! said in a prepared statement that only 0.5 percent of its donations come from overseas. It criticized the proposed laws as an attempt to avoid scrutiny of government policies and for failing to curtail donations from multinational corporations. "အဲဒီဥပဒေကို အစိုးရက ချမှတ်ထားပြီး နိုင်ငံခြားက လှူဒါန်းမှု ၅.၅ ရာခိုင်နှုန်းပဲ ရတယ်" လို့ GetUp! က ထုတ်ပြန်ချက်မှာ ရေးသားထားပါတယ်။ အစိုးရရဲ့ မူဝါဒတွေကို စစ်ဆေးမှုကနေ ရှောင်ရှားဖို့ ကြိုးစားပြီး နိုင်ငံတကာကုမ္ပဏီတွေက လှူဒါန်းမှုတွေကို လျှော့ချဖို့ ပျက်ကွက်တာလို့ ဥပဒေကြမ်းကို ဝေဖန်ခဲ့ပါတယ်။
Within days of the U.S. announcement, North Korean military members gathered for a ceremony to pledge their readiness to fight and win any battle to protect their homeland, Newsweek.com reported. အမေရိကန် ကြေညာချက်၏ ရက်ပိုင်းအတွင်း မြောက်ကိုရီးယား စစ်တပ်ဝင်များသည် ၎င်းတို့၏ ဇာတိမြေကို ကာကွယ်ရန် မည်သည့်တိုက်ပွဲကိုမဆို တိုက်ခိုက်ရန်နှင့် နိုင်ရန် အသင့်ရှိကြောင်း ကတိပြုရန် အခမ်းအနားတစ်ခုတွင် စုဝေးခဲ့ကြကြောင်း Newsweek.com သတင်းတွင် ဖော်ပြထားသည်။
To meet these new and emerging challenges, PACOM has begun an operationalization of its headquarters, and the command’s BMD division performing the dual role of regional and homeland defense epitomizes this transformation. This specifically refers to the “process of adapting or transforming the combatant command’s people, processes and products to support, effectively and timely, decision-making by the commander in the execution of assigned objectives and end states,” according to PACOM operations planners.  To meet these new and emerging challenges, PACOM has begun an operationalization of its headquarters, and the command’s BMD division performing the dual role of regional and homeland defense epitomizes this transformation. This specifically refers to the “process of adapting or transforming the combatant command’s people, processes and products to support, effectively and timely, decision-making by the commander in the execution of assigned objectives and end states,” according to PACOM operations planners.
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my/from_en$
```

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my/from_en$ wc ./apdf.my
   478  31245 453134 ./apdf.my
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my/from_en$ tail ./apdf.my
The U.S. Navy conducted the FONOP after Russia’s aggressive actions in the Black Sea culminated in in the seizure of three Ukrainian vessels in the Kerch Strait in November 2018. The Ukrainian ships were sailing off the coast of Crimea when they were seized. Russian vessels opened fire before their special forces rammed and stormed the vessels, according to a BBC News report.      အမေရိကန် ရေတပ်သည် FONOP ကို ၂၀၁၈ ခုနှစ် နိုဝင်ဘာလတွင် ကရက်ချ်ဆိပ်ကမ်းတွင် ယူကရိန်းသင်္ဘောသုံးစင်းကို သိမ်းပိုက်ခြင်းဖြင့် အဆုံးသတ်ခဲ့သောနောက်တွင် ပြုလုပ်ခဲ့သည်။ ယူကရိန်းသင်္ဘောများသည် သိမ်းပိုက်ခံရချိန်တွင် ခရိုင်းမီးယားကမ်းရိုးတန်းအနီးတွင် သင်္ဘောစီးနေစဉ်ဖြစ်သည်။ ရုရှားသင်္ဘောများသည် ၎င်းတို့၏ အထူးတပ်ဖွဲ့များက သင်္ဘောများကို မတိုက်မိခင် ပစ်ခတ်ခဲ့သည်။
The U.S. Navy regularly conducts FONOPs, but it usually conducts them in the South China Sea to challenge maritime claims by the People’s Republic of China. In early December 2018, the U.S. sent the guided-missile cruiser USS Chancellorsville near the Paracel Islands in the South China Sea.   အမေရိကန်ရေတပ်သည် FONOP များကို ပုံမှန်ပြုလုပ်သော်လည်း တရုတ်ပြည်သူ့သမ္မတနိုင်ငံ၏ ပင်လယ်ပိုင်ခွင့်များကို စိန်ခေါ်ရန်အတွက် တောင်တရုတ်ပင်လယ်တွင် ပြုလုပ်လေ့ရှိသည်။ ၂၀၁၈ ခုနှစ် ဒီဇင်ဘာလ အစောပိုင်းတွင် အမေရိကန်သည် တောင်တရုတ်ပင်လယ်ရှိ ပါရာစဲလ်ကျွန်းများအနီးသို့ လမ်းညွှန်ဒုံးကျည်သင်္ဘော USS Chancellorsville ကို စေလွှတ်ခဲ့သည်။
The U.S. Navy has deployed five ships as well as fighter jets and maritime patrol planes for the drills, which include live fire and anti-submarine warfare exercises.    အမေရိကန် ရေတပ်သည် စစ်သင်္ဘောငါးစင်း၊ တိုက်လေယာဉ်များနှင့် ပင်လယ်စောင့်လေယာဉ်များကို လေ့ကျင့်မှုများအတွက် တပ်ဆင်ထားပြီး ၎င်းတို့တွင် ပစ်ခတ်မှုနှင့် ရေငုပ်သင်္ဘောတိုက်ခိုက်မှု လေ့ကျင့်မှုများ ပါဝင်သည်။
The U.S. Navy said it was not immediately able to comment. NATO declined to comment.    အမေရိကန် ရေတပ်က ချက်ချင်း မှတ်ချက်မပြုနိုင်ဘူးလို့ ပြောပါတယ်။ NATO ကတော့ မှတ်ချက်မပြုလိုပါဘူး။
The U.S. Navy has angered China by sending warships close to artificial islands built by Beijing that include airstrips and radar stations. The U.S. lays no claims to the waters, but says it has an interest in ensuring freedom of navigation and overflight and peaceful resolution of ownership disputes.        အမေရိကန် ရေတပ်သည် ဘေဂျင်းက တည်ဆောက်ထားသော လေယာဉ်လမ်းကြောင်းများနှင့် ရေဒါစခန်းများပါဝင်သော လူလုပ်ကျွန်းများအနီးသို့ စစ်သင်္ဘောများ ပို့ပေးခြင်းဖြင့် တရုတ်နိုင်ငံကို ဒေါသထွက်စေခဲ့သည်။ အမေရိကန်သည် ရေပြင်များအပေါ် မည်သည့်အဆိုပါအခွင့်အလမ်းကိုမှ မယူဆသော်လည်း ရေကြောင်းနှင့် လေကြောင်းပျံသန်းမှု လွတ်လပ်မှုနှင့် ပိုင်ဆိုင်မှု အငြင်းပွားမှုများကို ငြိမ်းချမ်းစွာ ဖြေရှင်းရန် စိတ်ဝင်စားကြောင်း ပြောသည်။
The U.S. Navy has been the world’s leader in undersea technology for years. In 2004, the Navy released a report that said UUVs could be used for everything from surveillance, intelligence and reconnaissance to anti-submarine warfare. While investing more money in this technology, the Navy also is heralding progress on the scientific front. အမေရိကန်ရေတပ်သည် နှစ်ပေါင်းများစွာ ရေအောက်နည်းပညာတွင် ကမ္ဘာ့အကြီးဆုံးဖြစ်ခဲ့သည်။ ၂၀၀၄ ခုနှစ်တွင် ရေတပ်က UUV များကို စောင့်ကြည့်မှု၊ ထောက်လှမ်းရေးနှင့် ထောက်လှမ်းရေးမှ စ၍ ရေအောက်စစ်ဆင်ရေးအထိ အရာရာအတွက် အသုံးပြုနိုင်ကြောင်း အစီရင်ခံစာတစ်ခု ထုတ်ပြန်ခဲ့သည်။
The U.S. Navy said it wanted to demonstrate the principle of freedom of navigation.     US ရေတပ်က ၎င်းဟာ ရေကြောင်း လွတ်လပ်မှု မူကို ပြသချင်တယ်လို့ ပြောပါတယ်။
The U.S. Navy and others continue to sail their ships close to Chinese-occupied islands to assert the right to freedom of navigation. Beijing also has installed advanced weapons systems at several disputed locations, including seven islands it built by piling sand and concrete on top of coral atolls. တရုတ်နိုင်ငံက ထိန်းချုပ်ထားသော ကျွန်းများအနီးသို့ အမေရိကန် ရေတပ်နှင့် အခြားနိုင်ငံများက ၎င်းတို့၏ သင်္ဘောများကို ဆက်လက်စီးဆင်းလျက်ရှိကာ ရေကြောင်းခရီးသွားလာခွင့် လွတ်လပ်ခွင့်ကို အာမခံနေသည်။ ဘေဂျင်းသည် သန္တာကျွန်းစုများအထက်တွင် သဲနှင့် ကွန်ကရစ်ကို စုစည်း၍ တည်ဆောက်ထားသော ကျွန်းခုနစ်ခုအပါအဝင် အငြင်းပွားဖွယ်နေရာများစွာတွင် အဆင့်မြင့်လက်နက်စနစ်များကိုလည်း တပ်ဆင်ထားသည်။
The U.S. and New Zealand navies haven’t sailed together in New Zealand’s waters since shortly after a 1984 election in which David Lange’s Labour government was elected on a platform of making New Zealand a nuclear-free nation. အမေရိကန်နဲ့ နယူးဇီလန် ရေတပ်တွေဟာ နယူးဇီလန်ကို နျူကလီးယားကင်းတဲ့ နိုင်ငံတစ်ခုအဖြစ် ဖန်တီးဖို့ အစီအစဉ်တစ်ခုနဲ့ David Lange ရဲ့ အလုပ်သမားအစိုးရ ရွေးကောက်ခံခဲ့တဲ့ ၁၉၈၄ ရွေးကောက်ပွဲအပြီး မကြာခင်ကတည်းက နယူးဇီလန်ရေထဲမှာ အတူတူ မပျံသန်းခဲ့ဘူး။
The U.S. Navy conducted a similar exercise in October 2015 near one of China’s artificial islands in the Spratlys.        အမေရိကန် ရေတပ်သည် ၂၀၁၅ အောက်တိုဘာလတွင် Spratlys ကျွန်းစုရှိ တရုတ်နိုင်ငံ၏ အတုကျွန်းတစ်ခုအနီးတွင် အလားတူလေ့ကျင့်မှုတစ်ခု ပြုလုပ်ခဲ့သည်။
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my/from_en$
```

တချို့ အရမ်းရှည်တဲ့ စာကြောင်းတွေကိုတော့ ဘာသာပြန်မပေးနိုင်ဘူး ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my/from_en$ wc ./apdf.my
   690  45530 644797 ./apdf.my
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my/from_en$
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my/from_en$ tail ./apdf.my
Policing social media content has become a massive global problem, with no template for consistently preventing fake news online or eliminating it.       လူမှုမီဒီယာ အကြောင်းအရာကို ထိန်းချုပ်မှုဟာ ကမ္ဘာအနှံ့မှာ ကြီးမားတဲ့ ပြဿနာတစ်ခုဖြစ်လာပြီး အွန်လိုင်း သတင်းတုတွေကို အစဉ်အလာအတိုင်း တားဆီးဖို့ (သို့) ဖယ်ရှားဖို့ ပုံစံမရှိဘူး။
More stringent customs checks and patrols by Chinese border police have also made it harder to smuggle goods across the border, according to the traders, who declined to be named due to the subject’s sensitivity.        တရုတ်နယ်စပ်ရဲတပ်ဖွဲ့၏ ပိုမိုတင်းကျပ်သော အဂတိလိုက်စားမှု စစ်ဆေးမှုများနှင့် ကင်းလှည့်မှုများကြောင့် ကုန်ပစ္စည်းများကို နယ်စပ်တလျှောက်မှ တိမ်းရှောင်ရန် ခက်ခဲလာသည်ဟု ကုန်သည်များက ပြောသည်။
A holistic U.S. response should exploit the gaps in China’s strategy and sew up seams in the U.S. approach. At least three U.S. policy recommendations stand out in this regard. First, the United States should ratify the U.N. Convention on the Law of the Sea. Such a move would be an important signal of Washington’s enduring commitment to an international rules-based order. Second, Washington’s Free and Open Indo-Pacific Strategy, introduced in 2017and still under formulation, should articulate a positive counterpoint to Beijing’s vision for global governance in the maritime domain. It should reinforce economic, environmental, diplomatic, legal and security concepts that have served U.S., regional, global and Chinese interests for decades. It should draw attention to China’s efforts to reshape these concepts according to its own preferences and values. These largely rhetorical efforts should be matched by sustained U.S. military presence, maritime security cooperation, and diplomatic engagement with allies and partners — not only in the Indo-Pacific but also globally as the reach of China’s maritime strategy expands. Third, the U.S. should propose maritime strategy and law as topics for future high-level U.S.-China talks. TheU.S.-China Law Enforcement and Cybersecurity Dialogue is one possible venue. Washington should use these exchanges to understand the maritime legal concepts Beijing is promoting and to push back where these concepts are at odds with longstanding international rules and norms. The U.S. aim should be to shape Chinese legal concepts as they emerge — before they are ratified in a Chinese basic law of the sea.       A holistic U.S. response should exploit the gaps in China’s strategy and sew up seams in the U.S. approach. At least three U.S. policy recommendations stand out in this regard. First, the United States should ratify the U.N. Convention on the Law of the Sea. Such a move would be an important signal of Washington’s enduring commitment to an international rules-based order. Second, Washington’s Free and Open Indo-Pacific Strategy, introduced in 2017and still under formulation, should articulate a positive counterpoint to Beijing’s vision for global governance in the maritime domain. It should reinforce economic, environmental, diplomatic, legal and security concepts that have served U.S., regional, global and Chinese interests for decades. It should draw attention to China’s efforts to reshape these concepts according to its own preferences and values. These largely rhetorical efforts should be matched by sustained U.S. military presence, maritime security cooperation, and diplomatic engagement with allies and partners — not only in the Indo-Pacific but also globally as the reach of China’s maritime strategy expands. Third, the U.S. should propose maritime strategy and law as topics for future high-level U.S.-China talks. TheU.S.-China Law Enforcement and Cybersecurity Dialogue is one possible venue. Washington should use these exchanges to understand the maritime legal concepts Beijing is promoting and to push back where these concepts are at odds with longstanding international rules and norms. The U.S. aim should be to shape Chinese legal concepts as they emerge — before they are ratified in a Chinese basic law of the sea.
The task force’s asymmetric response served as a model for how to respond to real-life events in the future.      Task Force ရဲ့ asymmetric တုံ့ပြန်မှုက အနာဂတ်မှာ လက်တွေ့ဘဝ အဖြစ်အပျက်တွေကို တုံ့ပြန်ဖို့ ပုံစံတစ်ခုအဖြစ် လုပ်ဆောင်ခဲ့တယ်။
China’s response to North Korea’s last declared nuclear test, in the spring of 2013, was considered something of a watershed in degree of harshness. China swiftly joined the international community in condemning the action, called in the North Korean ambassador to protest, and, according to some indications, slowed the flow of goods across their border.   ၂၀၁၃ ခုနှစ် နွေဦးတွင် မြောက်ကိုရီးယား၏ နောက်ဆုံး ကြေညာထားသော နျူကလီးယား စမ်းသပ်မှုအပေါ် တရုတ်၏ တုံ့ပြန်မှုသည် ပြင်းထန်မှုအဆင့်တွင် ရေပိုင်းဖြတ်မှုတစ်ခုအဖြစ် သတ်မှတ်ခဲ့သည်။ တရုတ်သည် နိုင်ငံတကာအသိုင်းအဝိုင်းနှင့် ချက်ချင်းအတူ ထိုလုပ်ဆောင်မှုကို ပြစ်တင်ရှုတ်ချခဲ့ပြီး ဆန္ဒပြရန် မြောက်ကိုရီးယားသံအမတ်ကြီးကို ခေါ်ယူခဲ့ပြီး အချို့အချက်များအရ ၎င်းတို့နယ်စပ်မှ ကုန်ပစ္စည်းစီးဆင်းမှုကို နှေးကွေးစေခဲ့သည်။
China’s economic retaliation against South Korea regarding the planned deployment of a U.S. missile defense system is raising the ire of Korean government officials and conglomerates.     အမေရိကန် ဒုံးကျည်ကာကွယ်ရေးစနစ်ကို စီစဉ်တင်ပြမှုနှင့် ပတ်သက်၍ တောင်ကိုရီးယားကို တရုတ်၏ စီးပွားရေးတုံ့ပြန်မှုသည် ကိုရီးယားအစိုးရအရာရှိများနှင့် ကုမ္ပဏီများ၏ ဒေါသကို နှိုးဆွနေသည်။
This kind of judgment is often difficult to make, especially in areas such as Southeast Asia that have been populated for millennia. The claimants to the land features in the South China Sea (China and Taiwan, Vietnam, the Philippines, Malaysia and Brunei) are primarily interested in this territorial aspect of the dispute. Some claimants, though China in particular, base their maritime claims on history rather than contemporary law of the sea, which is why the discussion about the historical record in the region is so deeply politicized.     This kind of judgment is often difficult to make, especially in areas such as Southeast Asia that have been populated for millennia. The claimants to the land features in the South China Sea (China and Taiwan, Vietnam, the Philippines, Malaysia and Brunei) are primarily interested in this territorial aspect of the dispute. Some claimants, though China in particular, base their maritime claims on history rather than contemporary law of the sea, which is why the discussion about the historical record in the region is so deeply politicized.
The decision to expand the Malabar exercises that the U.S. and India conduct each year to include Japan comes days after a Pentagon official said it was considering sailing warships close to China’s artificial islands in the South China Sea. India has kept away from the tensions in the South China Sea, but has stood with the U.S. in calling for freedom of navigation in the region. အမေရိကန်နှင့် အိန္ဒိယတို့ နှစ်စဉ်ကျင်းပသည့် မာလာဘာလေ့ကျင့်ခန်းများကို ဂျပန်နိုင်ငံအပါအဝင် ကျင်းပရန် ဆုံးဖြတ်ချက်သည် တောင်တရုတ်ပင်လယ်တွင် တရုတ်နိုင်ငံ၏ အတုကျွန်းများအနီးသို့ သင်္ဘောများ စီးဆင်းရန် စဉ်းစားနေကြောင်း ပင်တဂွန်အရာရှိတစ်ဦးက ပြောကြားပြီး ရက်ပိုင်းအကြာတွင် ဖြစ်ပေါ်လာသည်။ အိန္ဒိယနိုင်ငံသည် တောင်တရုတ်ပင်လယ်တွင် တင်းမာမှုများမှ ဝေးကွာနေသော်လည်း ဒေသတွင်း ရေကြောင်း လွတ်လပ်ခွင့်အတွက် တောင်းဆိုရာတွင် အမေရိကန်နိုင်ငံနှင့်အတူ ရပ်တည်ခဲ့သည်။
The APG’s decisions are closely followed by the 37 members of the broader Financial Action Task Force (FATF), including the United States and China, Tsai added.  APG ၏ ဆုံးဖြတ်ချက်များကို အမေရိကန်နှင့် တရုတ်အပါအဝင် ကျယ်ပြန့်သော ငွေကြေးလုပ်ဆောင်မှု လုပ်ငန်းအဖွဲ့ (FATF) ၏ အဖွဲ့ဝင် ၃၇ နိုင်ငံက အနီးကပ်လိုက်နာနေကြောင်း Tsai က ထပ်မံပြောကြားသည်။
China’s decision to send air force bombers to disputed territory in the South China Sea drew immediate criticism from the governments of the Philippines and the United States, who say Beijing’s ruling party is destabilizing the region. တောင်တရုတ်ပင်လယ်တွင် အငြင်းပွားဖွယ် နယ်မြေများသို့ လေတပ်ဗုံးကြဲရေးယာဉ်များ ပေးပို့ရန် တရုတ်၏ ဆုံးဖြတ်ချက်သည် ဖိလစ်ပိုင်နှင့် အမေရိကန်အစိုးရတို့မှ ချက်ချင်း ဝေဖန်မှုများ ရရှိခဲ့ပြီး ပေကျင်း၏ အုပ်ချုပ်ရေးပါတီသည် ဒေသကို မတည်ငြိမ်စေသည်ဟု ဆိုသည်။
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my/from_en$
```

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ wc ./output_th-my_mahidol.txt
   58445   582837 10464114 ./output_th-my_mahidol.txt
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ tail ./output_th-my_mahidol.txt
ถ้า คุณ ไม่ ระวัง มัน จะ เกิด ขึ้น อีก และ อย่าง นี้ ไม่ หาย แผล หรอก   သတိမထားမိရင် ထပ်ဖြစ်သွားပြီး ဒီဒဏ်ရာက မပျောက်တော့ဘူး။
ผม กิน น้ำ เย็น แล้ว ปวด ครับ   ရေအေးသောက်လိုက်တယ်၊ နာကျင်တယ်။
ทำไม จะ ไม่ ล่ะ ဘာလို့ မဖြစ်တာလဲ။
ตอน นี้ เบื้อง ต้น ดี แล้ว นะ คะ        အခု သစ်ပင်တွေ စိုက်ပျိုးနေပြီ
น้ำ กรด กัด กระจก ?     น้ำ กรด กัด กระจก ?
แก ยัง รู้สึก ตัว ดี ไหม ค่ะ    မင်းက ကောင်းနေတုန်းလား။
นั่ง นิ่ง เชียว ထိုင်လိုက်၊ မတ်တပ်ရပ်လိုက်။
แต่ เนื่อง จาก ไม่ ได้ มี อาการ แทรกซ้อน        ဒါပေမဲ့ ရောဂါလက္ခဏာတွေ မရှိတော့
แต่ ผม พยายาม ที่ จะ ใช้ โลชั่น แล แป้ง สำหรับ ใบ หน้าที่ ไม่ ให้ มัน   ဒါပေမဲ့ မျက်နှာအတွက် အသားအရေလိမ်းဆေးကို မသုံးဖို့ ကြိုးစားတယ်။
แล้ว ให้ พยาบาล ติดต่อ ญาติ คน ไหน ดี คะ        ဒီတော့ ဘယ်သူတွေကို ဆက်သွယ်ဖို့ ပိုကောင်းလဲ။
```

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ wc output_th-my_mahidol.txt
   63137   632715 11290848 output_th-my_mahidol.txt
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ tail ./output_th-my_mahidol.txt
และ ทำ ให้ อวัยวะ ข้างเคียง บาดเจ็บ เพิ่ม       နောက်ပိုင်းမှာ အနားမှာ ဒဏ်ရာတွေ ပိုများလာတယ်
มัน ปวด มาก ฉัน จึง นอน ไม่ หลับ ตอน กลาง คืน   နာကျင်လွန်းလို့ ညဘက်မှာ အိပ်မရနိုင်ခဲ့ဘူး။
ผม แคะ จมูก     ကျွန်မက "ဟေး"။
แต่ พอ มา เช้า วัน นี้ เขา บ่น ปวด ที่ ตำแหน่ง ท้องขวา ล่าง     ဒါပေမဲ့ ဒီမနက်မှာ သူက သူ့အညာအောက်ပိုင်းမှာ နာကျင်နေတယ်လို့ တိုင်ကြားခဲ့တယ်။
รู้สึก มัน กด ตำแหน่ง ไหน เยอะ ๆ มั้ย   ခံစားချက်တွေက ဘယ်နေရာကို ဖိနေလဲ
ทำ งาน มา กี่ ปี แล้ว นะ ครับ   အလုပ်မှာ ဘယ်လောက်ကြာပြီလဲ
แน่น หน้าอก     ရင်ဘတ်ကို တင်းထားပါ။
รบกวน ถอด รองเท้า       ဖိနပ်တွေချွတ်လိုက်ပါ
เชิญ นั่ง เลย ค่ะ       ထိုင်ပါဦး။
คุณ มี คำ ถาม อะไร สำหรับ ผม    คุณ มี คำ ถาม อะไร สำหรับ ผม
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$
```

အထက်မှာ မြင်ရတဲ့ နောက်ဆုံး စာကြောင်းအတိုင်းပဲ ဒီ မဟီဒေါ corpus မှာလည်း တချို့ စာကြောင်းတွေကို ဘာသာပြန်မပေးနိုင်ဘူးလို့ နားလည်တယ်။  
 
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

## From Thai to Myanmar Translation  

preparing a new shell script ...  

(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ cat run4scb_fromThai.sh  

```bash
#!/bin/bash

# Base directory for input files
INPUT_DIR="/home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre"

# Directory for output files
OUTPUT_DIR="/home/ye/ye/exp/gpt-mt/nllb/scb-my/from_th"

# Create the output directory if it doesn't exist
mkdir -p "$OUTPUT_DIR"

# Iterate over each .src file in the input directory
for FILE in "$INPUT_DIR"/*.tgt; do
    # Extract the base filename without the extension
    BASENAME=$(basename "$FILE" .src)

    # Define the output file name
    OUTPUT_FILE="$OUTPUT_DIR/$BASENAME.my"

    # Print the command being executed (for debugging)
    echo "Running nllb-translate.sh for $FILE"

    # Run the translation command
    time ./nllb-translate.sh --input "$FILE" --source tha_Thai --target mya_Mymr --output "$OUTPUT_FILE"
done

```

Run the shell script ...  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ time ./run4scb_fromThai.sh
Running nllb-translate.sh for /home/ye/ye/exp/gpt-mt/nllb/data/scb/scb-mt-en-th-2020/pre/apdf.tgt
```

check the translated output ...  
အရမ်းရှည်တဲ့ ထိုင်းစာကြောင်းတွေ ဆိုရင် ဘာသာပြန်မပေးနိုင်တာကို တွေ့ရတယ်။  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my/from_th$ cat apdf.my
(ซ้ายสุด) นายติโต คาร์นาเวียน ผู้บัญชาการตำรวจแห่งชาติอินโดนีเซีย (จากซ้าย) นายโรนัลด์ เดลา โรซา ผู้บัญชาการตำรวจแห่งชาติฟิลิปปินส์ และนายคาลิด อาบู บาการ์ ผู้บัญชาการตํารวจแห่งชาติมาเลเซีย ไขว้แขนกันก่อนเริ่มการประชุมความมั่นคงไตรภาคีในเมืองปาเซย์ ซึ่งอยู่ทางตะวันออกเฉียงใต้ของกรุงมะนิลา ประเทศฟิลิปปินส์ ในเดือนมิถุนายน พ.ศ. 2560 ดิแอสโซซิเอทเต็ด เพรส    (ซ้ายสุด) นายติโต คาร์นาเวียน ผู้บัญชาการตำรวจแห่งชาติอินโดนีเซีย (จากซ้าย) นายโรนัลด์ เดลา โรซา ผู้บัญชาการตำรวจแห่งชาติฟิลิปปินส์ และนายคาลิด อาบู บาการ์ ผู้บัญชาการตํารวจแห่งชาติมาเลเซีย ไขว้แขนกันก่อนเริ่มการประชุมความมั่นคงไตรภาคีในเมืองปาเซย์ ซึ่งอยู่ทางตะวันออกเฉียงใต้ของกรุงมะนิลา ประเทศฟิลิปปินส์ ในเดือนมิถุนายน พ.ศ. 2560 ดิแอสโซซิเอทเต็ด เพรส
(ภาพ: จรวดซึ่งเชื่อว่าเป็นขีปนาวุธฮวาซองเช่นเดียวกับที่เกาหลีเหนือใช้ในการทดสอบเมื่อเดือนพฤษภาคม พ.ศ. 2560 ได้ถูกจัดแสดงในการสวนสนามทางทหารที่กรุงเปียงยางเมื่อเดือนเมษายน พ.ศ. 2560)เพื่อยับยั้งความขัดแย้งดังกล่าว พล.ท. วีเน้นย้ำว่า การเจรจาด้านกลาโหมแบบบูรณาการระหว่างเกาหลี-สหรัฐฯ ได้แลกเปลี่ยนความคิดเห็นในเรื่องการเคลื่อนกำลังยุทโธปกรณ์ด้านยุทธศาสตร์ของสหรัฐฯ โดยปกติ และทั้งสองฝ่าย “มุ่งให้ความสำคัญกับการเคลื่อนกำลังระบบป้องกันขีปนาวุธในบริเวณพิกัดตำแหน่งสูง”  (ภาพ: จรวดซึ่งเชื่อว่าเป็นขีปนาวุธฮวาซองเช่นเดียวกับที่เกาหลีเหนือใช้ในการทดสอบเมื่อเดือนพฤษภาคม พ.ศ. 2560 ได้ถูกจัดแสดงในการสวนสนามทางทหารที่กรุงเปียงยางเมื่อเดือนเมษายน พ.ศ. 2560)เพื่อยับยั้งความขัดแย้งดังกล่าว พล.ท. วีเน้นย้ำว่า การเจรจาด้านกลาโหมแบบบูรณาการระหว่างเกาหลี-สหรัฐฯ ได้แลกเปลี่ยนความคิดเห็นในเรื่องการเคลื่อนกำลังยุทโธปกรณ์ด้านยุทธศาสตร์ของสหรัฐฯ โดยปกติ และทั้งสองฝ่าย “มุ่งให้ความสำคัญกับการเคลื่อนกำลังระบบป้องกันขีปนาวุธในบริเวณพิกัดตำแหน่งสูง”
(ภาพ: จากซ้าย นายอัค โชราเชีย ผู้บัญชาการทางอากาศจากอินเดีย ร.อ. วอน ซอก คัง จากเกาหลีใต้ พ.ท. ลุหุต เบอร์นานดัส สิดาบาริบา จากอินโดนีเซีย พล.ต. จรัส ปัญญาดี เสนาธิการกองทัพภาคที่ 3 พล.ท.ศิราวุฒิ วงศ์ขันตี เจ้ากรมกิจการพลเรือนทหาร นายโจเซฟ มาร์ติน ผู้อำนวยการศูนย์เพื่อความเป็นเลิศด้านการจัดการภัยพิบัติและการช่วยเหลือด้านมนุษยธรรม พ.ท. โฮ วาน โฮว จากสิงคโปร์ พ.อ. มาซาโนริ โคอิเดะ จากญี่ปุ่น และพ.ท. โจว หมิง จากจีน ยืนถ่ายภาพระหว่างการฝึกซ้อมแผนบนโต๊ะเพื่อช่วยเหลือด้านมนุษยธรรมและการบรรเทาภัยพิบัติประจำปีครั้งที่สอง โดยเป็นส่วนหนึ่งของการฝึกคอบร้าโกลด์ประจำปีครั้งที่ 38 ในเดือนกุมภาพันธ์ พ.ศ. 2562 ซึ่งไทยและสหรัฐฯ ร่วมกันสนับสนุน)  (ภาพ: จากซ้าย นายอัค โชราเชีย ผู้บัญชาการทางอากาศจากอินเดีย ร.อ. วอน ซอก คัง จากเกาหลีใต้ พ.ท. ลุหุต เบอร์นานดัส สิดาบาริบา จากอินโดนีเซีย พล.ต. จรัส ปัญญาดี เสนาธิการกองทัพภาคที่ 3 พล.ท.ศิราวุฒิ วงศ์ขันตี เจ้ากรมกิจการพลเรือนทหาร นายโจเซฟ มาร์ติน ผู้อำนวยการศูนย์เพื่อความเป็นเลิศด้านการจัดการภัยพิบัติและการช่วยเหลือด้านมนุษยธรรม พ.ท. โฮ วาน โฮว จากสิงคโปร์ พ.อ. มาซาโนริ โคอิเดะ จากญี่ปุ่น และพ.ท. โจว หมิง จากจีน ยืนถ่ายภาพระหว่างการฝึกซ้อมแผนบนโต๊ะเพื่อช่วยเหลือด้านมนุษยธรรมและการบรรเทาภัยพิบัติประจำปีครั้งที่สอง โดยเป็นส่วนหนึ่งของการฝึกคอบร้าโกลด์ประจำปีครั้งที่ 38 ในเดือนกุมภาพันธ์ พ.ศ. 2562 ซึ่งไทยและสหรัฐฯ ร่วมกันสนับสนุน)
(ภาพ: จากซ้ายไปขวา นางมารีส เพย์น รัฐมนตรีว่าการกระทรวงกลาโหมออสเตรเลีย นายฮิชามุดดิน ตัน ฮุสเซน รัฐมนตรีว่าการกระทรวงกลาโหมมาเลเซีย นายอึ้ง เอ็ง เฮ็น รัฐมนตรีว่าการกระทรวงกลาโหมสิงคโปร์ นายมาร์ค มิทเชล รัฐมนตรีว่าการกระทรวงกลาโหมนิวซีแลนด์ และนายสก็อตต์ ไวท์แมน ข้าหลวงใหญ่สหราชอาณาจักรประจำสิงคโปร์เข้าร่วมการแถลงข่าวความตกลงด้านกลาโหมของสมาชิกห้าประเทศที่สิงคโปร์เมื่อวันที่ 2 มิถุนายน พ.ศ. 2560) (ภาพ: จากซ้ายไปขวา นางมารีส เพย์น รัฐมนตรีว่าการกระทรวงกลาโหมออสเตรเลีย นายฮิชามุดดิน ตัน ฮุสเซน รัฐมนตรีว่าการกระทรวงกลาโหมมาเลเซีย นายอึ้ง เอ็ง เฮ็น รัฐมนตรีว่าการกระทรวงกลาโหมสิงคโปร์ นายมาร์ค มิทเชล รัฐมนตรีว่าการกระทรวงกลาโหมนิวซีแลนด์ และนายสก็อตต์ ไวท์แมน ข้าหลวงใหญ่สหราชอาณาจักรประจำสิงคโปร์เข้าร่วมการแถลงข่าวความตกลงด้านกลาโหมของสมาชิกห้าประเทศที่สิงคโปร์เมื่อวันที่ 2 มิถุนายน พ.ศ. 2560)
(ภาพ: ชายคนหนึ่งชมการแพร่ภาพออกอากาศสดการปล่อยตัวนักบินอินเดีย น.ท. อภินันทาน วาร์ธามัน ที่จุดผ่านแดนวาร์กาในรัฐปัญจาบ เมื่อวันที่ 1 มีนาคม พ.ศ. 2562)    (ဓာတ်ပုံ- မတ်လ ၁ ရက်နေ့တွင် ပန်ဂျပ်ပြည်နယ်ရှိ ဒန်ဝားဂါနယ်စပ်တွင် အိန္ဒိယလေယာဉ်မှူး N.T. Abhinandan Warthaman လွတ်မြောက်ခြင်း၏ တိုက်ရိုက်လွှင့်လွှင့်မှုကို ကြည့်ရှုနေသော အမျိုးသား)
(ภาพ: ชาวมุสลิมโรฮีนจาซึ่งเดินทางออกจากพม่าไปยังบังกลาเทศ เดินทางไปยังค่ายผู้ลี้ภัยในบังกลาเทศเมื่อกลางเดือนพฤศจิกายน พ.ศ. 2560)  (ဓာတ်ပုံ- မြန်မာနိုင်ငံမှ ဘင်္ဂလားဒေ့ရှ်သို့ ခရီးထွက်လာသော ရိုဟင်ဂျာ မွတ်စလင်များ၊ ဘင်္ဂလားဒေ့ရှ် ဒုက္ခသည်စခန်းသို့ သွားရောက်နေစဉ်၊ နိုဝင်ဘာလလယ် ၂၅၆၀)
(ภาพ: ช่างเทคนิคห้องปฏิบัติการอุ้มลิงแสมที่ได้รับการตัดต่อพันธุกรรม ซึ่งนำไปใช้สร้างลิงจากการโคลนจำนวน 5 ตัว ที่สถาบันประสาทวิทยาศาสตร์ของสถาบันวิทยาศาสตร์จีนในเซี่ยงไฮ้ ประเทศจีน เมื่อเดือนมกราคม พ.ศ. 2562)     (ဓာတ်ပုံ- ဇန်နဝါရီ ၂၆၆၂၊ တရုတ်နိုင်ငံ ရှန်ဟိုင်းမြို့ရှိ တရုတ်သိပ္ပံတက္ကသိုလ်ရဲ့ အာရုံကြောသိပ္ပံဌာနမှာ မျောက်ငါးကောင်ကို ဗီဇပြောင်းပြီး မျောက်မွှားတွေကို ဖန်တီးတဲ့ မျောက်ဗီဇပြောင်းထားတဲ့ စမ်းသပ်ခန်း နည်းပညာပညာရှင်)
(ภาพ: ทหารของกองทัพเกาหลีใต้ยืนพูดคุยตรงด้านหน้าอากาศยานไร้คนขับที่โรงเรียนการบินแห่งหนึ่งในเมืองนันซัง ประเทศเกาหลีใต้)ระบบใหม่เหล่านี้ได้รับการพัฒนามานานหลายปี โดยมีกำหนดการนำมาใช้ในปี พ.ศ. 2560        (ภาพ: ทหารของกองทัพเกาหลีใต้ยืนพูดคุยตรงด้านหน้าอากาศยานไร้คนขับที่โรงเรียนการบินแห่งหนึ่งในเมืองนันซัง ประเทศเกาหลีใต้)ระบบใหม่เหล่านี้ได้รับการพัฒนามานานหลายปี โดยมีกำหนดการนำมาใช้ในปี พ.ศ. 2560
(ภาพ: ทหารจากกองทัพปาปัวนิวกินี (ด้านหน้า) ยืนร่วมกับนาวิกโยธินและลูกเรือสหรัฐฯ ในระหว่างการฝึกปฏิบัติการโคอาโมอานาเมื่อเดือนมิถุนายน พ.ศ. 2559)  (ภาพ: ทหารจากกองทัพปาปัวนิวกินี (ด้านหน้า) ยืนร่วมกับนาวิกโยธินและลูกเรือสหรัฐฯ ในระหว่างการฝึกปฏิบัติการโคอาโมอานาเมื่อเดือนมิถุนายน พ.ศ. 2559)
(ภาพ: น.อ. แรนดี แวน รอสซัม แห่งกองทัพเรือสหรัฐฯ (ซ้าย) ผู้บัญชาการภารกิจความร่วมมือแปซิฟิก พ.ศ. 2562 (พีพี 19) รับของขวัญจาก พล.ร.ต. ซามูเอล ฟีลิกซ์ แห่งกองทัพฟิลิปปินส์ เจ9 รองผู้บัญชาการทหารสูงสุด ในระหว่างพิธีปิดงานความร่วมมือแปซิฟิก พ.ศ. 2562 เพื่อปิดการแวะร่วมภารกิจในฟิลิปปินส์) (ภาพ: น.อ. แรนดี แวน รอสซัม แห่งกองทัพเรือสหรัฐฯ (ซ้าย) ผู้บัญชาการภารกิจความร่วมมือแปซิฟิก พ.ศ. 2562 (พีพี 19) รับของขวัญจาก พล.ร.ต. ซามูเอล ฟีลิกซ์ แห่งกองทัพฟิลิปปินส์ เจ9 รองผู้บัญชาการทหารสูงสุด ในระหว่างพิธีปิดงานความร่วมมือแปซิฟิก พ.ศ. 2562 เพื่อปิดการแวะร่วมภารกิจในฟิลิปปินส์)
(ภาพ: นักเรียนชั้นประถมชาวเกาหลีใต้สวมหน้ากากป้องกันก๊าซในระหว่างการฝึกซ้อมการป้องกันพลเรือนในที่หลบภัยแห่งหนึ่งในกรุงโซล)        (ဓာတ်ပုံ - တောင်ကိုရီးယား မူလတန်းကျောင်းသားတစ်ဦးသည် ဆော်လ်မြို့ရှိ အန္တရာယ်ကင်းစင်ရေးနေရာတစ်ခုတွင် အရပ်သားကာကွယ်ရေး လေ့ကျင့်ခန်းတစ်ခုတွင် ဓာတ်ငွေ့ကာကွယ်ရေး မျက်နှာဖုံးကို ဝတ်ဆင်နေစဉ်)
(ภาพ: นางซีซิเลีย มัลม์สตรอม กรรมาธิการการค้าสหภาพยุโรปคล้องแขนกับนายรามอน โลเปซ รัฐมนตรีว่าการกระทรวงพาณิชย์ฟิลิปปินส์ (ที่สองจากซ้าย) นายตรัน ตวน อันห์ รัฐมนตรีว่าการกระทรวงอุตสาหกรรมและการพาณิชย์เวียดนาม (ซ้าย) และนายเล เลือง มินห์ เลขาธิการอาเซียน ในงานแถลงข่าวที่ฟิลิปปินส์)       (ဓာတ်ပုံ- EU ကုန်သွယ်ရေးဝန်ကြီး Cecilia Malmstrom နှင့် ဖိလစ်ပိုင်စီးပွားရေးဝန်ကြီး Ramon Lopez လက်တွဲထားသည် (ဘယ်ဘက်မှ ဒုတိယ) ဗီယက်နမ်နိုင်ငံ ကုန်သွယ်ရေးနှင့် စက်မှုဝန်ကြီး Tran Tuan Anh (ဘယ်) နှင့် ဖိလစ်ပိုင်နိုင်ငံ သတင်းစာရှင်းလင်းပွဲတွင် အာဆီယံအတွင်းရေးမှူးချုပ် Liang Minh)
(ภาพ: นางมารีส เพย์น รัฐมนตรีว่าการกระทรวงกลาโหมออสเตรเลีย (ซ้าย) กล่าวขณะที่นางจูลี บิชอป รัฐมนตรีว่าการกระทรวงต่างประเทศฟัง ในระหว่างการแถลงข่าวที่หมู่บ้านชายแดนปันมุนจอมในเมืองพาจู ประเทศเกาหลีใต้ เมื่อเดือนตุลาคม พ.ศ. 2560) (ဓာတ်ပုံ- သြစတြေးလျ ကာကွယ်ရေးဝန်ကြီး မယ်ရီစ် ပဲန (ဘယ်) က နိုင်ငံခြားရေးဝန်ကြီး ဂျူလီ ဘီရှော့ပ်ကို ကြားနေစဉ် သတင်းစာရှင်းလင်းပွဲတစ်ခုမှာ ပြောကြားစဉ်၊ တောင်ကိုရီးယားနိုင်ငံ၊ ပဂျူးမြို့နယ်၊ ပင်မောင်ဂျုံ နယ်စပ်ကျေးရွာ၊ အောက်တိုဘာ ၂၅၆၀)
(ภาพ: นายคิม จองอึน (ซ้าย) ผู้นำเกาหลีเหนือ และนายมุน แจ-อิน ประธานาธิบดีเกาหลีใต้ ชูมือหลังการลงชื่อในแถลงการณ์ร่วม)     (ဓာတ်ပုံ- မြောက်ကိုရီးယားခေါင်းဆောင် Kim Jong-un (ဘယ်) နှင့် တောင်ကိုရီးယားသမ္မတ Moon Jae-in တို့ လက်တွဲကြေညာချက်တွင် လက်မှတ်ထိုးပြီးနောက်)
(ภาพ: นายจอร์จ แบรนดิส อัยการสูงสุดของออสเตรเลีย (ซ้าย) และพล.อ. วิแรนโต รัฐมนตรีประสานงานด้านการเมือง กฎหมายและกิจการความมั่นคงของอินโดนีเซีย กล่าวกับผู้สื่อข่าวหลังการประชุมระดับรัฐมนตรีเกี่ยวกับกฎหมายและความมั่นคงที่กรุงจาการ์ตา เมื่อเดือนกุมภาพันธ์ พ.ศ. 2560)     (ภาพ: นายจอร์จ แบรนดิส อัยการสูงสุดของออสเตรเลีย (ซ้าย) และพล.อ. วิแรนโต รัฐมนตรีประสานงานด้านการเมือง กฎหมายและกิจการความมั่นคงของอินโดนีเซีย กล่าวกับผู้สื่อข่าวหลังการประชุมระดับรัฐมนตรีเกี่ยวกับกฎหมายและความมั่นคงที่กรุงจาการ์ตา เมื่อเดือนกุมภาพันธ์ พ.ศ. 2560)
(ภาพ: นายจัสติน ทรูโด นายกรัฐมนตรีแคนาดา (ซ้าย) และนายโรดริโก ดูเตอร์เต ประธานาธิบดีฟิลิปปินส์ ทักทายกันในกรุงมะนิลาเมื่อเดือนพฤศจิกายน พ.ศ. 2560)        (ဓာတ်ပုံ- ကနေဒါ ဝန်ကြီးချုပ် Justin Trudeau (ဘယ်) နှင့် ဖိလစ်ပိုင်သမ္မတ Rodrigo Duterte တို့ မနီလာမြို့တွင် နှုတ်ဆက်စဉ်၊ နိုဝင်ဘာ ၂၅၆၀)
(ภาพ: นายชินโซ อะเบะ นายกรัฐมนตรีญี่ปุ่น (ซ้าย) พร้อมด้วยนายโดนัลด์ ทรัมป์ ประธานาธิบดีสหรัฐฯ (กลาง) และนายแมลคัม เทิร์นบุลล์ นายกรัฐมนตรีออสเตรเลีย พูดคุยในระหว่างการประชุมสุดยอดสมาคมประชาชาติเอเชียตะวันออกเฉียงใต้เมื่อเดือนพฤศจิกายน พ.ศ. 2560)       (ဓာတ်ပုံ- ဂျပန်ဝန်ကြီးချုပ် Shinzo Abe (ဘယ်) နှင့် အမေရိကန်သမ္မတ Donald Trump (လယ်) နှင့် သြစတြေးလျဝန်ကြီးချုပ် Malcolm Turnbull တို့ ၂၅၆၀ ခုနှစ် နိုဝင်ဘာလတွင် ကျင်းပသည့် အရှေ့တောင်အာရှ အမျိုးသားညီလာခံတွင် ဆွေးနွေးနေစဉ်)
(ภาพ: นายมุน แจ-อิน ประธานาธิบดีเกาหลีใต้ (ขวา) และนายซอง ยัง-มู รัฐมนตรีว่าการกระทรวงกลาโหม ตรวจกองทหารในระหว่างพิธีเฉลิมฉลองวันกองทัพเกาหลีใต้เมื่อวันที่ 1 ตุลาคม พ.ศ. 2560)   (ဓာတ်ပုံ - တောင်ကိုရီးယားနိုင်ငံ သမ္မတ မွန်ဂျာအင်း (ညာ) နှင့် ကာကွယ်ရေးဝန်ကြီးဌာန ဝန်ကြီး ဆွန်ယန်းမူးတို့ အောက်တိုဘာ ၁ ရက်နေ့တွင် ကျင်းပသည့် တပ်မတော်နေ့ အခမ်းအနားတွင် စစ်တပ်ကို စစ်ဆေးနေစဉ်)
(ภาพ: นายมูนาตะเข้าร่วมพิธีการเปลี่ยนชื่อของสถานทูตญี่ปุ่นโดยพฤตินัยเมื่อต้นเดือนมกราคม พ.ศ. 2560 ในกรุงไทเป ประเทศไต้หวัน)       (ဓာတ်ပုံ- ဦးမောင်တင့်သည် ထိုင်ဝမ်နိုင်ငံ ထိုင်းပင်မြို့တွင် ဇန်နဝါရီလဆန်းပိုင်းက ဂျပန်သံရုံး၏ အမည်ပြောင်းပွဲတွင် တက်ရောက်နေစဉ်)
(ภาพ: นายสี จิ้นผิง ประธานาธิบดีแห่งสาธารณรัฐประชาชนจีน (ขวา) จับมือกับนายโรดริโก ดูเตอร์เต ประธานาธิบดีฟิลิปปินส์ที่มหาศาลาประชาชนในกรุงปักกิ่งเมื่อวันที่ 15 พฤษภาคม พ.ศ. 2560 ก่อนการประชุมแบบทวิภาคีในโครงการ “หนึ่งแถบ หนึ่งเส้นทาง”)  (ဓာတ်ပုံ- တရုတ်ပြည်သူ့သမ္မတ ဒေါ်အောင်ဆန်းစုကြည် လက်ကို ဖိလစ်ပိုင်သမ္မတ ဒေါ်အောင်ဆန်းစုကြည် လက်ဆွဲကိုင်ထားသည်) မေလ ၁၅ ရက်နေ့တွင် ဘေဂျင်းမြို့ရှိ လူထုဆွေးနွေးပွဲတွင်
(ภาพ: นายหวังยี่ รัฐมนตรีว่าการกระทรวงการต่างประเทศจีนสรุปการแถลงข่าวเมื่อเดือนสิงหาคม พ.ศ. 2560 หลังการประกาศเกี่ยวกับข้อพิพาทด้านพรมแดนกับอินเดียที่ได้รับการแก้ไข)     (ဓာတ်ပုံ - တရုတ်နိုင်ငံခြားရေးဝန်ကြီး ဦးဟောင်းယီသည် အိန္ဒိယနိုင်ငံနှင့် နယ်စပ်အငြင်းပွားမှု ဖြေရှင်းခြင်းနှင့် ပတ်သက်၍ ထုတ်ပြန်ချက် ထုတ်ပြန်ပြီးနောက် သြဂုတ်လ ၂၅၆၀ တွင် သတင်းစာရှင်းလင်းပွဲကို နိဂုံးချုပ်သည်။)
(ภาพ: นายเรย์โนลด์ บี. ออยเลาช์ รองประธานาธิบดีปาเลาขึ้นเรือบรันสวิกของกองทัพเรือสหรัฐฯ ระหว่างพิธีปิดโครงการความร่วมมือในแปซิฟิก พ.ศ. 2561 ที่ปาเลาเมื่อเดือนเมษายน พ.ศ. 2561)   (ภาพ: นายเรย์โนลด์ บี. ออยเลาช์ รองประธานาธิบดีปาเลาขึ้นเรือบรันสวิกของกองทัพเรือสหรัฐฯ ระหว่างพิธีปิดโครงการความร่วมมือในแปซิฟิก พ.ศ. 2561 ที่ปาเลาเมื่อเดือนเมษายน พ.ศ. 2561)
(ภาพ: นายโช แต-ยูล เอกอัครราชทูตเกาหลีใต้ประจำสหประชาชาติ (กลาง) นายโคโระ เบสโช เอกอัครราชทูตญี่ปุ่น (ขวา) และนางนิกกี เฮลีย์ เอกอัครราชทูตสหรัฐฯ กล่าวกับผู้สื่อข่าวก่อนการประชุมเกี่ยวกับสถานการณ์ในเกาหลีเหนือของคณะมนตรีความมั่นคงที่สำนักงานใหญ่องค์การสหประชาชาติเมื่อวันที่ 16 พฤษภาคม พ.ศ. 2560)      (ภาพ: นายโช แต-ยูล เอกอัครราชทูตเกาหลีใต้ประจำสหประชาชาติ (กลาง) นายโคโระ เบสโช เอกอัครราชทูตญี่ปุ่น (ขวา) และนางนิกกี เฮลีย์ เอกอัครราชทูตสหรัฐฯ กล่าวกับผู้สื่อข่าวก่อนการประชุมเกี่ยวกับสถานการณ์ในเกาหลีเหนือของคณะมนตรีความมั่นคงที่สำนักงานใหญ่องค์การสหประชาชาติเมื่อวันที่ 16 พฤษภาคม พ.ศ. 2560)
(ภาพ: นาวิกโยธินสหรัฐฯ ส.ต. ไอแซก เพซเคดา ผู้เชี่ยวชาญด้านการสนับสนุนการยกพลขึ้นบก พร้อมด้วยกองพันส่งกำลังบำรุงการรบที่ 7 กองกำลังนาวิกโยธินเฉพาะกิจอากาศ-พื้นดินวัตถุประสงค์พิเศษที่ 7 บอกที่ตั้งของเป้าหมายให้กับคู่ซ้อมระหว่างการซ้อมยิงด้วยกระสุนจริง ซึ่งเป็นส่วนหนึ่งของการซ้อมรบนอร์ทเทิร์นเอดจ์ 2019) (ဓာတ်ပုံ- US Navy SEAL Isaac Pescada၊ လေယာဉ်ပေါ်တက်ရေး ထောက်ပံ့ရေး ကျွမ်းကျင်သူ၊ ၇ ကြိမ်မြောက် တိုက်ပွဲ ထိန်းသိမ်းရေး တပ်မတော်မှူး၊ ၇ ကြိမ်မြောက် ပင်လယ်ရေတပ် အထူး လေ-မြေ ရည်ရွယ်ချက် တပ်မတော်မှူး၊ ၂၀၁၉ မြောက်ပိုင်းအကမ်းအနား စစ်ဆင်ရေး အစိတ်အပိုင်းအဖြစ် ပစ်မှတ်စစ်ဆင်ရေး လေ့ကျင့်ခန်းအတွင်း ပစ်မှတ်နေရာကို လေ့ကျင့်ရေး ပူးပေါင်းဆောင်ရွက်သူအား ပြောကြား)
(ภาพ: ผู้อยู่อาศัยซึ่งกลับจากศูนย์อพยพเดินผ่านบ้านซึ่งได้รับความเสียหายจากกระสุนปืนที่เชื่อว่าถูกเช่าโดยนายอิสนิลอน ฮาปิลอน และนายโอมาร์ เมาท์ ผู้นำกลุ่มหัวรุนแรงที่สนับสนุนรัฐอิสลาม)     (ဓာတ်ပုံ- အီစိန်လန် ဟက်ပလိုန်နှင့် အစ္စလာမ်မစ် နိုင်ငံကို ထောက်ခံသည့် အစွန်းရောက် ခေါင်းဆောင် အိုမာ မတ်တို့ ငှားရမ်းထားသည်ဟု ယူဆရသည့် ကျည်ဆံများကြောင့် ပျက်စီးနေသော အိမ်တစ်လုံးမှ အဝင်အထွက်စခန်းမှ ပြန်လာနေသူတစ်ဦး လမ်းလျှောက်နေစဉ်)
(ภาพ: ผู้เข้าร่วมพูดคุยกันในงานระบบและเทคโนโลยีทางทะเล/อากาศเอเชีย พ.ศ. 2562 ในกรุงโตเกียว)       (ဓာတ်ပုံ- ၂၅၆၂ ခုနှစ်၊ တိုကျိုမြို့ရှိ အာရှလေကြောင်းနှင့်ရေကြောင်းစနစ်များနှင့် နည်းပညာများ ဆွေးနွေးပွဲတွင် ပါဝင်သူများ)
(ภาพ: พ.อ. คีธ เลมมอน ผู้ปฏิบัติหน้าที่กุมารแพทย์ที่ศูนย์การแพทย์ทหารบกเมดิแกน ฐานทัพร่วมลูอิส-แม็กคอร์ด ให้นักเรียนคนหนึ่งฟังเสียงหัวใจของตัวเองในระหว่างการมีส่วนร่วมด้านสุขภาพระดับโลก ที่โรงเรียนประถมศึกษาเปเลลิว รัฐเปเลลิว ประเทศปาเลา ในระหว่างการฝึกปาเลาซึ่งเป็นส่วนหนึ่งของการฝึกแปซิฟิกพาทเวย์)   (ဓာတ်ပုံ- P.O. Keith Lemmon၊ မက်ဒစ်ဂန် စစ်ဆေးရေးဌာန၊ Louis-McChord တပ်ရင်းအခြေစိုက် ဆေးရုံမှ ဆေးဝန်ထမ်း၊ Pacific Pathway Exercise အစိတ်အပိုင်းအဖြစ် Pellae မှာရှိတဲ့ Pellae Elementary School မှာ ကမ္ဘာ့ကျန်းမာရေးဆိုင်ရာ ပါဝင်မှုတစ်ခုအတွင်း ကျောင်းသားတစ်ဦးရဲ့ နှလုံးသံကို နားထောင်ပေးတယ်။)
(ภาพ: พล.ร.อ. แฮร์รี บี. แฮร์ริส จูเนียร์ ผู้บัญชาการกองบัญชาการสหรัฐฯ ภาคพื้นแปซิฟิก (ด้านหน้าตรงกลาง) ตอบคำถามผู้สื่อข่าวที่ฐานทัพอากาศโอซานในเกาหลีใต้ เมื่อเดือนสิงหาคม พ.ศ. 2560)      (ဓာတ်ပုံ- US Pacific Command ဗိုလ်ချုပ်ကြီး Harry B. Harris Jr. (အရှေ့ အလယ်) တောင်ကိုရီးယား အိုဇန် လေတပ်စခန်းမှာ သတင်းထောက်တွေကို မေးမြန်းနေစဉ်၊ သြဂုတ် ၂၅၆၀)
(ภาพ: พล.อ. คิม ยองวู ผู้บัญชาการทหารบกสาธารณรัฐเกาหลีและ พล.อ. มาร์ก เอ. มิลลี เสนาธิการกองทัพบกสหรัฐฯ เข้าสู่พิธีเปิดการประชุมผู้บัญชาการกองทัพบกภาคพื้นแปซิฟิกครั้งที่ 10 การสัมมนาการจัดการกองทัพบกภาคพื้นแปซิฟิกครั้งที่ 41 และการประชุมแลกเปลี่ยนความคิดเห็นของนายทหารประทวนอาวุโสครั้งที่สามในกรุงโซล ประเทศเกาหลีใต้ เมื่อวันที่ 18 กันยายน พ.ศ. 2560)        (ภาพ: พล.อ. คิม ยองวู ผู้บัญชาการทหารบกสาธารณรัฐเกาหลีและ พล.อ. มาร์ก เอ. มิลลี เสนาธิการกองทัพบกสหรัฐฯ เข้าสู่พิธีเปิดการประชุมผู้บัญชาการกองทัพบกภาคพื้นแปซิฟิกครั้งที่ 10 การสัมมนาการจัดการกองทัพบกภาคพื้นแปซิฟิกครั้งที่ 41 และการประชุมแลกเปลี่ยนความคิดเห็นของนายทหารประทวนอาวุโสครั้งที่สามในกรุงโซล ประเทศเกาหลีใต้ เมื่อวันที่ 18 กันยายน พ.ศ. 2560)
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my/from_th$
```

တကယ်တမ်း ထိုင်းကနေ မြန်မာကို ဘာသာပြန်တာက ဘယ်လောက်ထိ ကောင်းကောင်း လုပ်ပေးနိုင်မလဲ ဆိုတာ မသေချာဘူး။ လက်ရှိ အနေအထားက အောက်ပါအတိုင်း...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my/from_th$ wc ./apdf.my
   127   3236 188973 ./apdf.my
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my/from_th$ tail ./apdf.my
กรณีพิพาทในทะเลจีนใต้ที่มักจะถูกกล่าวถึงนั้น ความจริงแล้วคือศูนย์รวมของความขัดแย้งหลายประการ โดยมีฝ่ายต่าง ๆ เข้าไปเกี่ยวข้องกับพื้นที่ต่าง ๆ ในท้องทะเลเดียวกัน ตัวอย่างเช่น ขณะที่จีน ไต้หวันและเวียดนามล้วนอ้างสิทธิในหมู่เกาะพาราเซล แต่มาเลเซีย ฟิลิปปินส์ และบรูไนเข้าไปเกี่ยวข้องกับกรณีพิพาทแค่ในส่วนของพื้นที่รอบหมู่เกาะสแปรตลีซึ่งอยู่ทางตะวันออกเฉียงใต้เท่านั้น อินโดนีเซียไม่มีข้อพิพาทเกี่ยวกับดินแดนในทะเลจีนใต้ แต่อ้างสิทธิในเขตทางทะเลที่ทับซ้อนกับจีนและไต้หวันที่อ้างสิทธิในพื้นที่ภายในเส้นประ นับตั้งแต่ปี พ.ศ. 2552 เป็นต้นมา จีนได้อ้างสิทธิในเขตแดนทางทะเลที่ระบุในแผนที่ที่มีเส้นประ 10 เส้นเรียงรายเป็นรูปตัวยู นอกจากนี้ ไต้หวันยังอ้างสิทธิในพื้นที่ภายในเส้นประ 11 เส้นที่เริ่มจากอ่าวตังเกี๋ยไปจนถึงชายฝั่งทะเลตะวันออกของไต้หวันตามแผนที่เดิมที่จัดทำในปี พ.ศ. 2490 ซึ่งเป็นปีที่จีนเริ่มอ้างสิทธิแต่ไม่สามารถอธิบายความเป็นมาของสิทธิดังกล่าวหรือมูลฐานทางกฎหมายได้     กรณีพิพาทในทะเลจีนใต้ที่มักจะถูกกล่าวถึงนั้น ความจริงแล้วคือศูนย์รวมของความขัดแย้งหลายประการ โดยมีฝ่ายต่าง ๆ เข้าไปเกี่ยวข้องกับพื้นที่ต่าง ๆ ในท้องทะเลเดียวกัน ตัวอย่างเช่น ขณะที่จีน ไต้หวันและเวียดนามล้วนอ้างสิทธิในหมู่เกาะพาราเซล แต่มาเลเซีย ฟิลิปปินส์ และบรูไนเข้าไปเกี่ยวข้องกับกรณีพิพาทแค่ในส่วนของพื้นที่รอบหมู่เกาะสแปรตลีซึ่งอยู่ทางตะวันออกเฉียงใต้เท่านั้น อินโดนีเซียไม่มีข้อพิพาทเกี่ยวกับดินแดนในทะเลจีนใต้ แต่อ้างสิทธิในเขตทางทะเลที่ทับซ้อนกับจีนและไต้หวันที่อ้างสิทธิในพื้นที่ภายในเส้นประ นับตั้งแต่ปี พ.ศ. 2552 เป็นต้นมา จีนได้อ้างสิทธิในเขตแดนทางทะเลที่ระบุในแผนที่ที่มีเส้นประ 10 เส้นเรียงรายเป็นรูปตัวยู นอกจากนี้ ไต้หวันยังอ้างสิทธิในพื้นที่ภายในเส้นประ 11 เส้นที่เริ่มจากอ่าวตังเกี๋ยไปจนถึงชายฝั่งทะเลตะวันออกของไต้หวันตามแผนที่เดิมที่จัดทำในปี พ.ศ. 2490 ซึ่งเป็นปีที่จีนเริ่มอ้างสิทธิแต่ไม่สามารถอธิบายความเป็นมาของสิทธิดังกล่าวหรือมูลฐานทางกฎหมายได้
กรมการจัดซื้อจัดจ้างด้านกลาโหมของอินเดียได้ระบุว่า สิ่งที่สำคัญของการท้าทายในครั้งนี้ ได้แก่ การช่วยสร้างแม่แบบของผลิตภัณฑ์ที่เกี่ยวเนื่องกับความมั่นคงแห่งชาติและนำไปใช้งานได้จริง การส่งเสริมนวัตกรรมที่เคลื่อนตัวเร็วในภาคส่วนกลาโหม และการช่วยหาตลาดสำหรับเทคโนโลยีใหม่ ๆ ในวงการกลาโหมอินเดีย    กรมการจัดซื้อจัดจ้างด้านกลาโหมของอินเดียได้ระบุว่า สิ่งที่สำคัญของการท้าทายในครั้งนี้ ได้แก่ การช่วยสร้างแม่แบบของผลิตภัณฑ์ที่เกี่ยวเนื่องกับความมั่นคงแห่งชาติและนำไปใช้งานได้จริง การส่งเสริมนวัตกรรมที่เคลื่อนตัวเร็วในภาคส่วนกลาโหม และการช่วยหาตลาดสำหรับเทคโนโลยีใหม่ ๆ ในวงการกลาโหมอินเดีย
กรมงานการเมืองมีหน้าที่สร้างแรงบันดาลใจด้านแนวคิดทางการเมืองและทำการตัดสินใจด้านบุคลากรทหาร นายซู ไคเฮา เคยเป็นอธิบดีกรมงานการเมือง ซึ่งถูกกล่าวหาพร้อมกับเพื่อนร่วมงานคือ นายเกา โบเซียง อดีตรองประธานคณะกรรมาธิการทหารส่วนกลางว่ารับสินบนเพื่อแลกเปลี่ยนกับการเลื่อนตำแหน่ง นายเกาถูกตัดสินจำคุกตลอดชีวิตในปี พ.ศ. 2559 ในขณะที่นายซูเสียชีวิตด้วยโรคมะเร็งในปี พ.ศ. 2558 ก่อนที่จะถูกพิจารณาคดี      กรมงานการเมืองมีหน้าที่สร้างแรงบันดาลใจด้านแนวคิดทางการเมืองและทำการตัดสินใจด้านบุคลากรทหาร นายซู ไคเฮา เคยเป็นอธิบดีกรมงานการเมือง ซึ่งถูกกล่าวหาพร้อมกับเพื่อนร่วมงานคือ นายเกา โบเซียง อดีตรองประธานคณะกรรมาธิการทหารส่วนกลางว่ารับสินบนเพื่อแลกเปลี่ยนกับการเลื่อนตำแหน่ง นายเกาถูกตัดสินจำคุกตลอดชีวิตในปี พ.ศ. 2559 ในขณะที่นายซูเสียชีวิตด้วยโรคมะเร็งในปี พ.ศ. 2558 ก่อนที่จะถูกพิจารณาคดี
กรมอุตุนิยมวิทยาออสเตรเลียและเครือข่ายห้างสรรพสินค้าเคมาร์ท ออสเตรเลีย จำกัด ซึ่งบริษัทเวสฟาร์เมอร์ส จำกัด เป็นเจ้าของ ทั้งสองประสบความเสียหายจากการโจมตีทางออนไลน์ในปี พ.ศ. 2558 นายเทิร์นบุลล์ระบุ        กรมอุตุนิยมวิทยาออสเตรเลียและเครือข่ายห้างสรรพสินค้าเคมาร์ท ออสเตรเลีย จำกัด ซึ่งบริษัทเวสฟาร์เมอร์ส จำกัด เป็นเจ้าของ ทั้งสองประสบความเสียหายจากการโจมตีทางออนไลน์ในปี พ.ศ. 2558 นายเทิร์นบุลล์ระบุ
กรอบการกำกับดูแลปัญญาประดิษฐ์ความหนา 50 หน้าซึ่งผลิตโดยคณะกรรมาธิการคุ้มครองข้อมูลส่วนบุคคลของสิงคโปร์ และเผยแพร่ที่เวทีเศรษฐกิจโลกในเมืองดาวอส ประเทศสวิตเซอร์แลนด์ เมื่อเดือนมกราคม พ.ศ. 2562 ในรูปแบบเครื่องมือที่พร้อมใช้งานเพื่อช่วยองค์กรต่าง ๆ ในการนำปัญญาประดิษฐ์มาใช้งานอย่างมีความรับผิดชอบ        ဆင်ကာပူနိုင်ငံရဲ့ ပုဂ္ဂိုလ်ရေးအချက်အလက်များ ကာကွယ်ရေး ကော်မတီက ထုတ်ပြန်ခဲ့တဲ့ စာမျက်နှာ ၅၀ အထူရှိတဲ့ AI ထိန်းချုပ်မှု မူကြမ်းကို ဇန်နဝါရီ ၂၆၆၂ မှာ ဆွစ်ဇာလန်နိုင်ငံ ဒါဝော့စ်မြို့က ကမ္ဘာ့စီးပွားရေးဖိုရမ်မှာ ထုတ်ပြန်ခဲ့ပါတယ်။
กรอบการทำงานการแบ่งปันข้อมูลข่าวกรอง อาวร์ อายส์ ซึ่งเปิดตัวเมื่อปีที่ผ่านมาโดยอินโดนีเซียและสมาชิกอีกห้าประเทศของสมาคมประชาชาติแห่งเอเชียตะวันออกเฉียงใต้ หรืออาเซียน กำลังขยายตัวเพื่อต่อต้านภัยคุกคามจากกลุ่มหัวรุนแรงสุดโต่ง    အရှေ့တောင်အာရှ အဖွဲ့အစည်း (သို့) ASEAN အဖွဲ့ဝင် ငါးနိုင်ငံတို့က မနှစ်က စတင်ခဲ့တဲ့ Our Eyes ထောက်လှမ်းရေး ပူးပေါင်းဆောင်ရွက်မှုဟာ အစွန်းရောက် အစွန်းရောက် အဖွဲ့အစည်းတွေရဲ့ ခြိမ်းခြောက်မှုကို တုံ့ပြန်ဖို့ တိုးချဲ့နေပါတယ်။
กรอบดังกล่าวมาจากแนวคิดพื้นฐานสองข้อ ประกอบด้วยการตัดสินใจที่เกิดจากปัญญาประดิษฐ์จะต้อง “อธิบายได้ โปร่งใส และยุติธรรม” และระบบปัญญาประดิษฐ์ หุ่นยนต์ รวมทั้งการตัดสินใจที่ใช้ปัญญาประดิษฐ์จะต้อง “ยึดมนุษย์เป็นศูนย์กลาง”  กรอบดังกล่าวมาจากแนวคิดพื้นฐานสองข้อ ประกอบด้วยการตัดสินใจที่เกิดจากปัญญาประดิษฐ์จะต้อง “อธิบายได้ โปร่งใส และยุติธรรม” และระบบปัญญาประดิษฐ์ หุ่นยนต์ รวมทั้งการตัดสินใจที่ใช้ปัญญาประดิษฐ์จะต้อง “ยึดมนุษย์เป็นศูนย์กลาง”
กระทรวงกลาโหมกล่าวว่า จีนกำลังเสริมสร้างการแสดงตนทางทหารในทะเลจีนใต้ด้วยการเคลื่อนพลระบบต่อต้านขีปนาวุธ โดรน และเรือขีปนาวุธเร็วในพื้นที่ดังกล่าว กระทรวงกลาโหมกล่าวว่า จีนกำลังเสริมสร้างการแสดงตนทางทหารในทะเลจีนใต้ด้วยการเคลื่อนพลระบบต่อต้านขีปนาวุธ โดรน และเรือขีปนาวุธเร็วในพื้นที่ดังกล่าว
กระทรวงกลาโหมกล่าวว่า เงินเพิ่มเติมจะถูกนำมาใช้ในการจัดหาขีปนาวุธโจมตีร่วมซึ่งมีพิสัยประมาณ 500 กิโลเมตร และจะได้รับการติดตั้งบนเครื่องบินโจมตีล่องหนเอฟ-35 ของกองกำลังป้องกันตนเองทางอากาศญี่ปุ่นจากบริษัทคองสเบิร์ก ดีเฟนซ์ แอนด์ แอโรสเปซ ในนอร์เวย์ รวมทั้งขีปนาวุธเจเอเอสเอสเอ็ม-อีอาร์ และขีปนาวุธแอลอาร์เอเอสเอ็มจากบริษัทล็อคฮีดมาร์ติน คอร์ปอเรชัน ซึ่งขีปนาวุธทั้งสองลูกมีพิสัยประมาณ 900 กิโลเมตร และมีแนวโน้มที่จะปล่อยจากเครื่องบินโจมตีเอฟ-15 เกียวโดนิวส์รายงาน    กระทรวงกลาโหมกล่าวว่า เงินเพิ่มเติมจะถูกนำมาใช้ในการจัดหาขีปนาวุธโจมตีร่วมซึ่งมีพิสัยประมาณ 500 กิโลเมตร และจะได้รับการติดตั้งบนเครื่องบินโจมตีล่องหนเอฟ-35 ของกองกำลังป้องกันตนเองทางอากาศญี่ปุ่นจากบริษัทคองสเบิร์ก ดีเฟนซ์ แอนด์ แอโรสเปซ ในนอร์เวย์ รวมทั้งขีปนาวุธเจเอเอสเอสเอ็ม-อีอาร์ และขีปนาวุธแอลอาร์เอเอสเอ็มจากบริษัทล็อคฮีดมาร์ติน คอร์ปอเรชัน ซึ่งขีปนาวุธทั้งสองลูกมีพิสัยประมาณ 900 กิโลเมตร และมีแนวโน้มที่จะปล่อยจากเครื่องบินโจมตีเอฟ-15 เกียวโดนิวส์รายงาน
กระทรวงกลาโหมกล่าวว่ากองกำลังทางอากาศญี่ปุ่นส่งสัญญาณรบกวนเครื่องบินขับไล่จำนวน999 ครั้งใน พ.ศ. 2561 ซึ่งเป็นจำนวนที่สูงเป็นอันดับสองนับตั้งแต่เริ่มป้องกันน่านฟ้าเมื่อ พ.ศ. 2501 โดยร้อยละ 64 จากจำนวนดังกล่าวเป็นการตอบโต้อากาศยานจีน     ဂျပန်လေတပ်က ၂၅၆၁ ခုနှစ်မှာ လေယာဉ်တိုက်ဖျက်ရေး အတားအဆီး ၉၉၉ ကြိမ် ထုတ်ပြန်ခဲ့တယ်လို့ ကာကွယ်ရေးဝန်ကြီးဌာနက ပြောပါတယ်။ ၂၅၆၁ ခုနှစ်က စပြီး ဒုတိယအကြိမ်မြောက် အမြင့်ဆုံးဖြစ်ခဲ့ပြီး ၄၀ ရာခိုင်နှုန်းက တရုတ်လေယာဉ်တွေကို တုံ့ပြန်မှုဖြစ်တယ်လို့ ဆိုပါတယ်။
```

သို့သော်လည်း run ထားပြီး scb corpus တစ်ခုလုံးအတွက် nllb မော်ဒယ်က ဘယ်လောက်ထိ ဘာသာပြန်ပေးနိုင်သလဲ ဆိုတာကို လေ့လာမယ်။ အဲဒါမှလည်း စာတမ်းထဲမှာ အကျိုးအကြောင်း ပြောပြလို့ ရမှာမို့ ...  

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

## Banglanmt Dataset Preparation

```
(base) ye@lst-gpu-server-197:~/ye/exp/banglanmt/hasan-etal-2020-low/2.75M$ wc *
  2753069  30140674 503884078 original_corpus.bn
  2753069  33206583 205362832 original_corpus.en
  5506138  63347257 709246910 total
(base) ye@lst-gpu-server-197:~/ye/exp/banglanmt/hasan-etal-2020-low/2.75M$
```

```
(base) ye@lst-gpu-server-197:~/ye/exp/banglanmt/hasan-etal-2020-low/data$ ls
corpus.train.bn      sipcdevtest.valid.bn    sipcdev.valid.en.0  sipc.test.en.1
corpus.train.en      sipcdevtest.valid.en.0  sipcdev.valid.en.1  sipc.test.en.2
RisingNews.test.bn   sipcdevtest.valid.en.1  sipcdev.valid.en.2  sipc.test.en.3
RisingNews.test.en   sipcdevtest.valid.en.2  sipcdev.valid.en.3
RisingNews.valid.bn  sipcdevtest.valid.en.3  sipc.test.bn
RisingNews.valid.en  sipcdev.valid.bn        sipc.test.en.0
```

```
(base) ye@lst-gpu-server-197:~/ye/exp/banglanmt/hasan-etal-2020-low/data$ wc corpus.train.en
  2659723  31028180 186987971 corpus.train.en
(base) ye@lst-gpu-server-197:~/ye/exp/banglanmt/hasan-etal-2020-low/data$ wc corpus.train.bn
  2659723  28004328 477655605 corpus.train.bn
```

```
(base) ye@lst-gpu-server-197:~/ye/exp/banglanmt/hasan-etal-2020-low/data$ cat -n ./corpus.train.en | head
     1  better o . Guaranteeing that every individual will be free to do as he wishes inevitably short-changes equality.
     2  trump
     3  overrides
     4  "They warm the heart and ease the daily load.
     5  I love you.
     6  Port Company Limited - KPCL
     7  commotions
     8  Clemenceau also expressed skepticism and frustration with Wilson's Fourteen Points: "Mr. Wilson bores me with his fourteen points", complained Clemenceau.
     9  Other Twitter users went on commenting on Jalloud's interview for Al-Jazeera and his attitude:
    10  Club.
(base) ye@lst-gpu-server-197:~/ye/exp/banglanmt/hasan-etal-2020-low/data$
```

check with tail command ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/banglanmt/hasan-etal-2020-low/data$ cat -n ./corpus.train.en | tail
2659714 You should get bigger size
2659715 Twitter users also commented on the politics related to the earthquake and the presidential transition.
2659716 Notice that if we choose another vector w, then this approximate equation determines another approximate equation by substituting w for v.
2659717 Avani Davda
2659718 What are you doing?
2659719 He also cites an incident where the Ecuadorian television channels had presented information inaccurately about a crime that affected a personal friend of his.
2659720 Hue
2659721 Satan 'has means to cause death'?
2659722 Such mating contradicts the will of Nature towards the selective improvements of life in general. The favourable preliminary to this improvement is not to mate individuals of higher and lower orders of being but rather to allow the complete triumph of the higher order.
2659723 A 1% provision was taken for all non-classified outstanding loans while the rates of provision for loans classified as substandard was 10%, for those classified as doubtful 50%, and for bad loans 100%.
(base) ye@lst-gpu-server-197:~/ye/exp/banglanmt/hasan-etal-2020-low/data$
```

ကြည့်ရတာ စာကြောင်းတွေထဲမှာ စာလုံးတစ်လုံးနဲ့ စာကြောင်း ဖြစ်နေတာတွေလည်း ပါတယ်။  
ဘင်္ဂါလီဘက် ကြည့်ကြည့်မယ် ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/banglanmt/hasan-etal-2020-low/data$ cat -n ./corpus.train.bn | head
     1  আবার সবাইকে যার যার ইচ্ছামতো চলতে দিলে সমতা রক্ষা করা অসম্ভব হয়ে যায়।
     2  তুরুপ
     3  পদদলিত করা
     4  "সেগুলো হৃদয়কে উষ্ণ করে এবং রোজকার বোঝাগুলোকে হালকা করে।
     5  আমি ভালোবাসি তোমাকে ।
     6  পোর্ট কোম্পানি লিমিটেড - কেপিসিএল
     7  তোলপাড়
     8  এছাড়াও ক্লেমঁসো উইলসনের ১৪ দফার ব্যাপারে সংশয়ী এবং হতাশ ছিলেন। তিনি অভিযোগ করে বলেন, "মিস্টার উইলসনের ১৪ দফা বিরক্তিকর।
     9  আল-জাজিরার সঙ্গে জালুদের সাক্ষাতকার এবং তার দৃষ্টিভঙ্গীর বিষয়ে অন্যান্য টুইটার ব্যবহারকারীরা মন্তব্য করেন:
    10  ক্লাব.
(base) ye@lst-gpu-server-197:~/ye/exp/banglanmt/hasan-etal-2020-low/data$
```

```
(base) ye@lst-gpu-server-197:~/ye/exp/banglanmt/hasan-etal-2020-low/data$ cat -n ./corpus.train.bn | tail
2659714 তোমার আরো বড়টা দরকার
2659715 টুইটার ব্যবহারকারীরা ভূমিকম্প সম্পর্কিত রাজনীতি এবং রাষ্ট্রপতির পরিবর্তনের উপর মন্তব্য করেছে।
2659716 লক্ষ্য করুন যদি আমারা একটি ভেক্টর ডব্লিউ নিই তবে ভি কে ডব্লিউ দ্বারা প্রতিস্থাপন করার মাধ্যমে এই আনুমানিক সমীকরণ আরেকটি আনুমানিক সমীকরণ নির্ণয় করে।
2659717 আভানি দাভাডা
2659718 ওই ব্যাটা কি করিস?
2659719 তিনি একটি ঘটনার কথাও বলেছেন যেখানে ইকুয়েডরিয়ান টেলিভিশন চ্যানেল একটি অপরাধের সম্বন্ধে ভুল তথ্য উপস্থাপন করেছিল যা তার একজন ব্যক্তিগত বন্ধুকে প্রভাবিত করেছিল।
2659720 হিউ
2659721 শয়তান 'মৃত্যুর কর্ত্তৃত্ববিশিষ্ট ব্যক্তি'?
2659722 এ কারণেই ভিন্ন জাতীয় দুই প্রাণীর সহবাস প্রাণধারার নির্বাচন যুক্ত বিবর্তন সম্পর্কিত প্রকৃতির ইচ্ছার সম্পূর্ণ বিরোধী; বলবান প্রাণীও দুর্বল দুই ভিন্ন জাতীয় প্রাণীর মিলন প্রাণের উন্নত বিবর্তনধারার পরিপন্থী।
2659723 নিম্নমান, সন্দেহজনক এবং মন্দ শ্রেণির ঋণের জন্য যথাক্রমে ১০%, ৫০% এবং ১০০% হারে সঞ্চয় সংরক্ষণ করার নিয়ম ছিল। এ ছাড়া ব্যাংকগুলির জন্য অশ্রেণীবিন্যাসকৃত ঋণের ওপর ১% হারে সাধারণ সঞ্চয় সংরক্ষণ করা বাধ্যতামূলক ছিল।
(base) ye@lst-gpu-server-197:~/ye/exp/banglanmt/hasan-etal-2020-low/data$
```

Full path info:  

```
(base) ye@lst-gpu-server-197:~/ye/exp/banglanmt/hasan-etal-2020-low/data$ pwd
/home/ye/ye/exp/banglanmt/hasan-etal-2020-low/data
```

nllb folder အောက်ကို ကော်ပီကူးထည့်ခဲ့...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/banglanmt/en$ wc *
  2659723  31028180 186987971 corpus.train.en
     1000     18356    115004 RisingNews.test.en
      597     11072     70090 RisingNews.valid.en
  2661320  31057608 187173065 total
```

## Translation for BanglaNMT (from English)

အရင်ဆုံး shell script ကို ပြင်ဆင်ခဲ့တယ်။  

(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ cat run4banglanmt_fromEn.sh  

```bash
#!/bin/bash

# Base directory for input files
INPUT_DIR="/home/ye/ye/exp/gpt-mt/nllb/banglanmt/en"

# Directory for output files
OUTPUT_DIR="/home/ye/ye/exp/gpt-mt/nllb/banglanmt/my"

# Create the output directory if it doesn't exist
mkdir -p "$OUTPUT_DIR"

# Iterate over each .src file in the input directory
for FILE in "$INPUT_DIR"/*.en; do
    # Extract the base filename without the extension
    BASENAME=$(basename "$FILE" .en)

    # Define the output file name
    OUTPUT_FILE="$OUTPUT_DIR/$BASENAME.my"

    # Print the command being executed (for debugging)
    echo "Running nllb-translate.sh for $FILE"

    # Run the translation command
    time ./nllb-translate.sh --input "$FILE" --source eng_Latn --target mya_Mymr --output "$OUTPUT_FILE"
done
```

start translation ...  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ time ./run4banglanmt_fromEn.sh
Running nllb-translate.sh for /home/ye/ye/exp/gpt-mt/nllb/banglanmt/en/corpus.train.en
```

checking translated output ... 
Run ထားရင်းနဲ့ ဘာသာပြန်ပြီး ထွက်လာတဲ့ မြန်မာစာ စာကြောင်းတွေကို စစ်ကြည့်ခဲ့...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/banglanmt/my$ cat -n ./corpus.train.my | tail
    29  holes   အပေါက်များ
    30  Build up yourself and other faithful family members.    Build up yourself and other faithful family members.
    31  Still, this marvelous system continues to amaze scientists for its complexity - much of it perhaps still undiscovered.    [စာမျက်နှာ ၂၇ ပါ ရုပ်ပုံ]
    32  (1 Ki. 17:3-6) We have faith that Jehovah can maneuver matters so that we too have what we need.  ၁၃။ ယေဟောဝါသည် ကျွန်ုပ်တို့အား အဘယ်အရာကို ပေးနိုင်သနည်း။
    33  PUBLISHERS      ထုတ်ဝေသူများ
    34  gentler gentler
    35  The commandments of his Heavenly Father, Jehovah, are not burdensome either.- Deuteronomy 30:11; 1 John 5:3.      [စာမျက်နှာ ၂၇ ပါ ရုပ်ပုံ]
    36  I promised Mom I wouldn't tell  I promised Mom I wouldn't tell
    37  of aristocrat birth.    မင်းသားမျိုးနွယ်ပါ။
    38  All the four rulers of the Husain Shahi dynasty - Alauddin Husain Shah (1493-1519 AD), Nasiruddin Nusrat Shah (1519-1532 AD) Alauddin Firuz Shah (1532 AD) and Ghiyasuddin Mahmud Shah (1532-1538 AD) struck gold and silver coins, which have been found.  ဟူစိုင်းရှားမင်းဆက်၏ အုပ်ချုပ်သူ လေးပါးလုံး - အလာအူဒင် ဟူစိုင်းရှား (၁၄၉၃-၁၅၁၉ AD), နာစီရတ်ဒင်နူစရက်ရှား (၁၅၁၉-၁၅၃၂ AD), အလာအူဒင်ဖီးရုတ်ရှား (၁၅၃၂ AD) နှင့် ဂီယာဆူဒင်မဟာမူဒ်ရှား (၁၅၃၂-၁၅၃၈ AD) တို့က ရွှေနှင့် ငွေစက္ကူများကို ထိုးထုတ်ခဲ့သည်၊ ၎င်းတို့တွေ့ရှိခဲ့သည်။
```

checking ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/banglanmt/my$ cat -n ./corpus.train.my | tail
   281  Trinidad &amp; Tobago (1973 only)       ထရီနီဒါဒ်နှင့် တိုဘာဂို (၁၉၇၃ ခုနှစ်မှသာ)
   282  Anastasia, hush.        Anastasia၊ တိတ်နေပါ။
   283  She imagined this chamber at night, filled with masked people, chanting by torchlight, all witnessing a "sacred communion" in the center of the room.     null
   284  Historian Will Durant relates: "An army of Babylonians under Nabopolassar united with an army of Medes under Cyaxares and a horde of Scythians from the Caucasus, and with amazing ease and swiftness captured the citadels of the north....        null
   285  I was shocked.  ကျွန်မ လန့်သွားခဲ့တယ်။
   286  15 Why does Jehovah exercise long-suffering?    [စာမျက်နှာ ၁၆ ပါ ရုပ်ပုံ]
   287  According to a local participant with the alias Losgi Athenford:        Losgi Athenford ဆိုတဲ့ အမည်မဲ့ အမည်နဲ့ ဒေသခံ ပါဝင်သူတစ်ဦးရဲ့ အဆိုအရ
   288  Beheshti got arrested last week in his home.    Beheshti ကို ပြီးခဲ့တဲ့ သီတင်းပတ်က သူ့အိမ်မှာ ဖမ်းဆီးခဲ့တယ်။
   289  (Job 17:10) As to some who rejected the knowledge of God, the apostle Paul wrote: "Although asserting they were wise, they became foolish."       null
   290  We were sent from orphanage to orphanage, and at the age of 12, I ended up in one in Thessalonica, where I served an apprenticeship as a mechanic.        [စာမျက်နှာ ၂၇ ပါ ရုပ်ပုံ]
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/banglanmt/my$
```

checking ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/banglanmt/my$ cat -n ./corpus.train.my | tail
  1786  In 1949, Ginzton and Marvin Chodorow developed the 1 BeV 220 accelerator in the at Stanford University.   In 1949, Ginzton and Marvin Chodorow developed the 1 BeV 220 accelerator in the at Stanford University.
  1787  Swat refugees, Image courtesy Dr. Awab Alvi (teeth.com.pk/blog) Swat refugees, Image courtesy Dr. Awab Alvi (teeth.com.pk/blog)
  1788  Call an ambulance.      Call an ambulance.
  1789  "We enjoy our time so much that our study usually lasts longer than an hour," says one of them.   "We enjoy our time so much that our study usually lasts longer than an hour," says one of them.
  1790  Cancer 2        Cancer 2
  1791  oracular        oracular
  1792  The preaching work.     The preaching work.
  1793  A grand hoax saw a majority of the Indian newspaper media being fooled by the claim that a Nazi war criminal was caught in Goa.   A grand hoax saw a majority of the Indian newspaper media being fooled by the claim that a Nazi war criminal was caught in Goa.
  1794  Ripping off foreign travelers is nothing new to the Italian people, unfortunately.Ripping off foreign travelers is nothing new to the Italian people, unfortunately.
  1795  or (b) which is, with a view to making it coloured, coated or stained, mixed excessively with such amount of ingredients that impairs the food and diminishes the food value or nutritive qualities of such food;   or (b) which is, with a view to making it coloured, coated or stained, mixed excessively with such amount of ingredients that impairs the food and diminishes the food value or nutritive qualities of such food;
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/banglanmt/my$
```

## Preparing ReMeDi Corpus

original corpus ဖိုင်တွေက json ဖိုင်တွေပါ။ အဲဒီထဲကနေ text ဖိုင်အဖြစ် ဆွဲထုတ်ထားတဲ့ ဖိုင်တွေက အောက်ပါအတိုင်း ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/data/ReMeDi-large$ ls *.txt
0.txt   11.txt  13.txt  15.txt  17.txt  1.txt  3.txt  5.txt  8.txt
10.txt  12.txt  14.txt  16.txt  18.txt  2.txt  4.txt  6.txt  9.txt
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/data/ReMeDi-large$
```

format က အောက်ပါအတိုင်း conversation အသွားအပြန်နဲ့ ရေးထားတယ်။  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/data/ReMeDi-large$ head -n 20 0.txt
Dialogue 0:
patient: 感冒能做普通的胃镜吗（男，24岁）
doctor: 你好，有没有发烧？扁桃体肿大吗？
patient: 发烧倒是没有喉咙上面有点疼痛
doctor: 那就晚些时间再做吧。
patient: 不能做是吗
doctor: 是的，因为胃镜的管子会通过咽喉部的。

Dialogue 1:
patient: 前列腺增生可以服用仁青芒觉吗（男，51岁）
doctor: 你好         可以的
patient: 我服用温肾前列胶囊和仁青芒觉
doctor: 可以
doctor: 这两个都属于中成药
doctor: 一般性情比较温和
patient: 没付作用吧
patient: 我是轻微的前列腺增生
doctor: 嗯嗯   排尿费力症状明显吗
patient: 排尿没问题现在就是小腹坠胀和夜尿多一夜尿四次
doctor: 哦
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/data/ReMeDi-large$
```

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/data/ReMeDi-large$ head -n 20 9.txt
Dialogue 0:
patient: 中药配方颗粒，治胃炎效果好吗（男，16岁）
doctor: 你好，请问有什么症状吗？
patient: 就是每次服用过之后小腹就难受
doctor: 中药颗粒剂是有效方便的！建议您饭后用！
doctor: 小腹难受是什么表现？
patient: 但是每次服用后肚子和下腹就好像在翻滚，咕咕叫了
doctor: 多数中医有此反应！
patient: 这是怎么了
doctor: 属中药增加了胃肠蠕动！有的是通过促进排便来降火和治便秘！属中医八法中的下法
patient: 哦
patient: 那什么时候才会没有这种症状
doctor: 如果确定是药引起，可以少量多次用或症状消失后停药

Dialogue 1:
patient: 请问手淫造成的肾虚吃什么药补补（（男，47岁）
doctor: 肯可以，但是你这个年纪恢复起来非常缓慢，时间比较久，金匮肾气丸和补中益气丸再加上五子衍宗丸
doctor: 中途还需要来根据反应调整药物

Dialogue 2:
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/data/ReMeDi-large$
```

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/data/ReMeDi-large$ wc *.txt
  101039   202847  5185636 0.txt
  101089   202363  5172408 10.txt
  103199   206415  5270628 11.txt
  103166   205533  5280823 12.txt
  103354   207188  5331683 13.txt
  101510   203623  5182255 14.txt
  102206   205985  5270099 15.txt
  102725   205247  5299837 16.txt
  100958   202043  5174686 17.txt
  111322   222930  5721487 18.txt
  106035   211990  5384760 1.txt
  102608   205703  5292356 2.txt
  103511   207796  5301225 3.txt
  102413   204818  5243722 4.txt
  101859   204419  5189478 5.txt
  103480   207350  5336408 6.txt
  103607   207374  5301209 8.txt
  102890   205747  5276866 9.txt
 1856971  3719371 95215566 total
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/data/ReMeDi-large$
```

zh_Hans ကနေ mya_Myan ကို တိုက်ရိုက် ဘာသာပြန်ခိုင်းတဲ့အခါမှာ အောက်ပါလိုမျိုး format သတ်မှတ်ခဲ့တယ်။ အဲဒါမှ field 2, 3 ကို ဆွဲထုတ်လိုက်ရင် parallel corpus အလွယ်တကူ ဆွဲထုတ်လို့ ရတာမို့လို့ ...   

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/ReMeDi/from_zh$ cat 0.my
Dialogue 0:
patient: 感冒能做普通的胃镜吗（男，24岁）       感冒能做普通的胃镜吗（男，24岁）        အအေးမိရင် ပုံမှန် အစာအိမ်မှန်ကြည့်လို့ရလား (အမျိုးသား၊ ၂၄ နှစ်)
doctor: 你好，有没有发烧？扁桃体肿大吗？        你好，有没有发烧？扁桃体肿大吗？        ဟိုင်း၊ အဖျားရှိလား။ tonsils များများများကြီးကြီးရှိလား။
patient: 发烧倒是没有喉咙上面有点疼痛   发烧倒是没有喉咙上面有点疼痛    အဖျားမရှိပေမဲ့ လည်ချောင်းမှာ နည်းနည်းနာပါတယ်။
doctor: 那就晚些时间再做吧。    那就晚些时间再做吧。    ဒီကိစ္စကို နောက်ပိုင်းမှာ ပြန်လုပ်ကြရအောင်။
patient: 不能做是吗     不能做是吗      မလုပ်နိုင်ဘူးလား။
doctor: 是的，因为胃镜的管子会通过咽喉部的。    是的，因为胃镜的管子会通过咽喉部的。    အစာအိမ်ထဲမှာ အစာအိမ်အမြင်မှန်တွေ ရှိတယ်

Dialogue 1:
patient: 前列腺增生可以服用仁青芒觉吗（男，51岁）       前列腺增生可以服用仁青芒觉吗（男，51岁）  前列腺增生可以服用仁青芒觉吗（男，51岁）
doctor: 你好         可以的     你好         可以的     ဟိုင်း၊ အဆင်ပြေတယ်
patient: 我服用温肾前列胶囊和仁青芒觉   我服用温肾前列胶囊和仁青芒觉    ကျွန်မက နူးညံ့တဲ့ ရှေ့ပိုင်း အသားတင်ဆေးပြားတွေနဲ့ အင်းစိန်ကို သောက်တယ်။
doctor: 可以    可以    ဟုတ်တယ်
doctor: 这两个都属于中成药      这两个都属于中成药      ဒီနှစ်ယောက်စလုံးဟာ ဆေးဝါးသုံးစွဲမှု အပါအဝင်ပါ။
doctor: 一般性情比较温和        一般性情比较温和        ယေဘုယျအားဖြင့်တော့ စိတ်ဓာတ်သိမ်မွေ့တယ်။
patient: 没付作用吧     没付作用吧      မဖြစ်မနေ လုပ်နေတာပါ။
patient: 我是轻微的前列腺增生   我是轻微的前列腺增生    ကျွန်မမှာ prostate ပမာဏနည်းနည်း တိုးလာတယ်
doctor: 嗯嗯   排尿费力症状明显吗       嗯嗯   排尿费力症状明显吗       ဆီးချို၊ ဆီးချိုနဲ့ ဆီးချိုရောဂါတွေ ရှိလား။
patient: 排尿没问题现在就是小腹坠胀和夜尿多一夜尿四次   排尿没问题现在就是小腹坠胀和夜尿多一夜尿四次      အခုဆို အစာအိမ်ဖောင်းတာ၊ ညဘက်မှာ ညဘက်မှာ လေးကြိမ်လောက် ပို urinate လုပ်တာပဲ
doctor: 哦      哦      ဟေး
doctor: 可以先通过这两个药物改善        可以先通过这两个药物改善        ဒီဆေးနှစ်ခုနဲ့ အရင်ဆုံး တိုးတက်လာနိုင်တယ်
doctor: 如果效果不明显可以改服坦索罗辛缓释胶囊  如果效果不明显可以改服坦索罗辛缓释胶囊  အကျိုးဆက် မထင်ရှားရင် ထန်ဆာရိုဆင် ဖြုတ်ချမှု ကပ်စွပ်ကို ပြောင်းနိုင်ပါတယ်။

Dialogue 2:
patient: 先兆流产孩子保得住吗（女，25岁）       先兆流产孩子保得住吗（女，25岁）        အီရန်နိုင်ငံတွင် ကလေးငယ်များအတွက် အစာအိမ်များ ဖွင့်လှစ်ထား
doctor: 你好，只能说先用上保胎药试下    你好，只能说先用上保胎药试下    你好，只能说先用上保胎药试下
patient: 吃了一个星期的保胎药了 吃了一个星期的保胎药了  ကလေးမွေးဖို့ တစ်ပတ်စာ သောက်လိုက်တဲ့ ကလေးမွေးဆေး
patient: 我就下面有点褐色分泌物 躺床上就没有时间上厕所会带出来一点      我就下面有点褐色分泌物 躺床上就没有时间上厕所会带出来一点 ကျွန်မအောက်မှာ လိမ္မော်ရောင် သုတ်ရည်တွေ နည်းနည်းရှိတယ်၊ အိပ်ရာမှာ အိပ်ဖို့ အချိန်မရှိဘူး၊ အိမ်သာကို သွားရင် နည်းနည်းထွက်လာမယ်။
doctor: 那还可以，褐色分泌物是积存的，不要紧张  那还可以，褐色分泌物是积存的，不要紧张  ဒါလည်းကောင်းတယ်၊ လိမ္မော်ရောင်သွေးတွေ စုစည်းထားတယ်၊ စိတ်မပူပါနဲ့။
patient: 吃了保胎药好很多了 我就是想问下我最后一次月经是3月1号 怀孕多久了啊     吃了保胎药好很多了 我就是想问下我最后一次月经是3月1号 怀孕多久了啊        ကျွန်မက ကလေးမွေးဖို့ ဆေးတွေ အများကြီးသောက်ပြီး ကျွန်မ မေးချင်တာက ကျွန်မ နောက်ဆုံး ရာသီလာတာက မတ်လ ၁ ရက်နေ့၊ ကိုယ်ဝန်ရှိတာ ဘယ်လောက်ကြာပြီလဲ။
patient: 什么时候能看到胎心     什么时候能看到胎心      ကလေးရဲ့ နှလုံးသားကို ဘယ်တော့ မြင်နိုင်လဲ။
patient: 我去医院看的阴超 单子上是先兆流产      我去医院看的阴超 单子上是先兆流产       ဆေးရုံကိုသွားပြီး တွေ့လိုက်ရတဲ့ သားအိမ်က သားမွားတာရဲ့ ရှေ့ပြေးဖြစ်နေလို့
doctor: 52天左右能看到胎心，现在这个阶段流血或者腹痛就是先兆流产的诊断  52天左右能看到胎心，现在这个阶段流血或者腹痛就是先兆流产的诊断    ၅၂ ရက်လောက်မှာ သားအိမ်ရဲ့ နှလုံးသားကို မြင်နိုင်ပြီး အခုအချိန်မှာ သွေးယိုတာ၊ ဝမ်းဗိုက်နာတာတွေဟာ ဝမ်းပျက်ခြင်းရဲ့ ရှေ့ပြေး ရောဂါလက္ခဏာတွေပါ။
patient: 那能保的住吗   那能保的住吗    လုံခြုံတဲ့ နေရာတစ်ခုလား။
patient: 保的住吗       保的住吗        အိုးအိမ်လား။
doctor: 这个我没法给你肯定答案，但根据你的描述，并不严重        这个我没法给你肯定答案，但根据你的描述，并不严重  ဒီမေးခွန်းကို အသေအချာ မဖြေနိုင်ပေမဲ့ ခင်ဗျားပြောသလိုတော့ မဆိုးပါဘူး။
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/ReMeDi/from_zh$
```

checking ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/ReMeDi/from_zh$ tail 0.my
patient: 那能查出别的吗 那能查出别的吗  ဒါက အခြားအရာတွေကို ရှာဖွေနိုင်လား။
doctor: 20号以后查      20号以后查      ၂၀ နောက်မှာ စစ်ဆေးပါ
patient: 我现在肚子有点疼 像来月经一样 但是没流血       我现在肚子有点疼 像来月经一样 但是没流血  အခု ကျွန်မမှာ ဝမ်းဗိုက်နာကျင်မှု နည်းနည်းရှိတယ်၊ ရာသီလာသလိုမျိုးပါ၊ ဒါပေမဲ့ သွေးမထွက်ဘူး။
doctor: 先多休息        先多休息        အနားယူပါ။
patient: 我这个能保住吗 我这个能保住吗  ဒါကို ကျွန်မ ထိန်းထားနိုင်မလား။
doctor: 放松心情        放松心情        စိတ်အေးဆေးမှု
patient: 好的 谢谢      好的 谢谢       ကောင်းပါတယ် ကျေးဇူးတင်ပါတယ်။
doctor: 不客气  不客气  不客气

Dialogue 3:
```

checking ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/ReMeDi/from_zh$ cat -n ./0.my | tail
   115  doctor: 按说明吃就行    按说明吃就行    按说明吃就行
   116  doctor: 饮食清淡一些    饮食清淡一些    饮食清淡一些
   117  patient: 还有宝宝大便每次都是前面一节硬结后面软，一天一次，正常吗？跟大人一样   还有宝宝大便每次都是前面一节硬结后面软，一天一次，正常吗？跟大人一样      还有宝宝大便每次都是前面一节硬结后面软，一天一次，正常吗？跟大人一样
   118  doctor: 跟感冒都有关系  跟感冒都有关系  跟感冒都有关系
   119  patient: 平时没有感冒也是       平时没有感冒也是        平时没有感冒也是
   120  patient: 每次大便脸赠的通红     每次大便脸赠的通红      每次大便脸赠的通红
   121  patient: 感觉很用劲     感觉很用劲      感觉很用劲
   122  patient: 有两三个月了   有两三个月了    有两三个月了
   123  patient: 吃了小儿七星茶和益生菌也没有什么效果   吃了小儿七星茶和益生菌也没有什么效果      吃了小儿七星茶和益生菌也没有什么效果
   124  doctor: 那就去检查一下  那就去检查一下  那就去检查一下
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/ReMeDi/from_zh$
```

ဘာသာပြန်မပေးနိုင်တဲ့ စာကြောင်းတွေ အများကြီးရှိတယ် ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/ReMeDi/from_zh$ cut -f3 ./0.my
Dialogue 0:
အအေးမိရင် ပုံမှန် အစာအိမ်မှန်ကြည့်လို့ရလား (အမျိုးသား၊ ၂၄ နှစ်)
ဟိုင်း၊ အဖျားရှိလား။ tonsils များများများကြီးကြီးရှိလား။
အဖျားမရှိပေမဲ့ လည်ချောင်းမှာ နည်းနည်းနာပါတယ်။
ဒီကိစ္စကို နောက်ပိုင်းမှာ ပြန်လုပ်ကြရအောင်။
မလုပ်နိုင်ဘူးလား။
အစာအိမ်ထဲမှာ အစာအိမ်အမြင်မှန်တွေ ရှိတယ်

Dialogue 1:
前列腺增生可以服用仁青芒觉吗（男，51岁）
ဟိုင်း၊ အဆင်ပြေတယ်
ကျွန်မက နူးညံ့တဲ့ ရှေ့ပိုင်း အသားတင်ဆေးပြားတွေနဲ့ အင်းစိန်ကို သောက်တယ်။
ဟုတ်တယ်
ဒီနှစ်ယောက်စလုံးဟာ ဆေးဝါးသုံးစွဲမှု အပါအဝင်ပါ။
ယေဘုယျအားဖြင့်တော့ စိတ်ဓာတ်သိမ်မွေ့တယ်။
မဖြစ်မနေ လုပ်နေတာပါ။
ကျွန်မမှာ prostate ပမာဏနည်းနည်း တိုးလာတယ်
ဆီးချို၊ ဆီးချိုနဲ့ ဆီးချိုရောဂါတွေ ရှိလား။
အခုဆို အစာအိမ်ဖောင်းတာ၊ ညဘက်မှာ ညဘက်မှာ လေးကြိမ်လောက် ပို urinate လုပ်တာပဲ
ဟေး
ဒီဆေးနှစ်ခုနဲ့ အရင်ဆုံး တိုးတက်လာနိုင်တယ်
အကျိုးဆက် မထင်ရှားရင် ထန်ဆာရိုဆင် ဖြုတ်ချမှု ကပ်စွပ်ကို ပြောင်းနိုင်ပါတယ်။

Dialogue 2:
အီရန်နိုင်ငံတွင် ကလေးငယ်များအတွက် အစာအိမ်များ ဖွင့်လှစ်ထား
你好，只能说先用上保胎药试下
ကလေးမွေးဖို့ တစ်ပတ်စာ သောက်လိုက်တဲ့ ကလေးမွေးဆေး
ကျွန်မအောက်မှာ လိမ္မော်ရောင် သုတ်ရည်တွေ နည်းနည်းရှိတယ်၊ အိပ်ရာမှာ အိပ်ဖို့ အချိန်မရှိဘူး၊ အိမ်သာကို သွားရင် နည်းနည်းထွက်လာမယ်။
ဒါလည်းကောင်းတယ်၊ လိမ္မော်ရောင်သွေးတွေ စုစည်းထားတယ်၊ စိတ်မပူပါနဲ့။
ကျွန်မက ကလေးမွေးဖို့ ဆေးတွေ အများကြီးသောက်ပြီး ကျွန်မ မေးချင်တာက ကျွန်မ နောက်ဆုံး ရာသီလာတာက မတ်လ ၁ ရက်နေ့၊ ကိုယ်ဝန်ရှိတာ ဘယ်လောက်ကြာပြီလဲ။
ကလေးရဲ့ နှလုံးသားကို ဘယ်တော့ မြင်နိုင်လဲ။
ဆေးရုံကိုသွားပြီး တွေ့လိုက်ရတဲ့ သားအိမ်က သားမွားတာရဲ့ ရှေ့ပြေးဖြစ်နေလို့
၅၂ ရက်လောက်မှာ သားအိမ်ရဲ့ နှလုံးသားကို မြင်နိုင်ပြီး အခုအချိန်မှာ သွေးယိုတာ၊ ဝမ်းဗိုက်နာတာတွေဟာ ဝမ်းပျက်ခြင်းရဲ့ ရှေ့ပြေး ရောဂါလက္ခဏာတွေပါ။
လုံခြုံတဲ့ နေရာတစ်ခုလား။
အိုးအိမ်လား။
ဒီမေးခွန်းကို အသေအချာ မဖြေနိုင်ပေမဲ့ ခင်ဗျားပြောသလိုတော့ မဆိုးပါဘူး။
好的 我现在我卧床休息了 下面就没有 就上厕所有一点
ကိုယ်ဝန်ဆောင်တုန်းက ဝမ်းဗိုက်မကောင်းတာ၊ ဝမ်းမိုက်တာ၊ ဝမ်း vomiting တွေက ပိုဆိုးတယ်
ကျွန်မက ပုံမှန်လား။
ပုံမှန်ပါ။
အမ်ဳိးသားသားအခ်စ္ေရးအဖြဲ႔ခ်ဳပ္က ေဒၚေအာင္ဆန္းစုၾကည္ကို ေထာက္ခံဖို႔ ေမွ်ာ္လင့္ထားပါတယ္။
နောက်ဆုံး ရာသီလာခဲ့တာ ဘယ်တုန်းကလဲ။
မတ်လ ၁ ရက်
ဧပြီလလယ်လောက်မှာ လုပ်လို့ရပါပြီ။
ကောင်းပြီ၊ နည်းနည်းလေး နှေးပါ။
我15号去检查应该就知道好不好了吧
去做B超
ဟုတ်တယ်
做B超能查出什么
胎心
15号查的出胎心吗
နည်းနည်း စောနေပြီ။
ဒါက အခြားအရာတွေကို ရှာဖွေနိုင်လား။
၂၀ နောက်မှာ စစ်ဆေးပါ
အခု ကျွန်မမှာ ဝမ်းဗိုက်နာကျင်မှု နည်းနည်းရှိတယ်၊ ရာသီလာသလိုမျိုးပါ၊ ဒါပေမဲ့ သွေးမထွက်ဘူး။
အနားယူပါ။
ဒါကို ကျွန်မ ထိန်းထားနိုင်မလား။
စိတ်အေးဆေးမှု
ကောင်းပါတယ် ကျေးဇူးတင်ပါတယ်။
不客气

Dialogue 3:
交感神经型颈椎病可以吃颈复康吗?（男，36岁）
你好，具体有什么症状表现？
头皮发麻 眼睛干 嗓子不舒服 还有胃肠
现在
现在做牵引哪
可以用
还配合什么药物  别刺激性太大的
头皮发麻可以口服弥可保
做牵引  就不麻了
那就不用服药了
头皮  还脸都是用手一模就好像有小虫子爬是的
颈复康能行吗
ဟုတ်တယ်
哪行吧谢谢了大夫
就吃这一种就可以呗
အထက်ပါအတိုင်း လုပ်နိုင်ပါတယ် ။
မသမာမှု
ကျေးဇူးတင်ပါတယ်။
😊

Dialogue 4:
အီရတ်နိုင်ငံက အီရတ်နိုင်ငံသားတစ်ဦးက အီရတ်နိုင်ငံက အီရတ်နိုင်ငံသားတစ်ဦးဖြစ်သူ ကိုဗစ်-၁၉ ရောဂါရှိသူတစ်ဦးကို ဆေးကုသမှုခံယူနေစဉ်က တွေ့ရှိခဲ့ပါတယ်
မင်္ဂလာပါ မသောက်သင့်ပါဘူး အသေအချာ မသောက်သင့်ပါဘူး
ဒီမှာလား။
အင်း
治愈4年
အနည်းငယ် သောက်လို့ရလား။
၅ ကနေ ၆ ခွက်လောက် သောက်ခဲ့တယ်။
အဆင်ပြေပါတယ်။
ဘီယာ
"အဲဒီလိုပြောတာ ရှင်းနေပြီ ဆရာဝန်အနေနဲ့ ခင်ဗျားလိုလူနာတွေကို အရက်မသောက်ဖို့ တိုက်တွန်းပါတယ်"
အီရန်နိုင်ငံက အီရန်နိုင်ငံသား ၁၄ ဦးကို ဖမ်းဆီးထား

Dialogue 5:
အူမကြီး၊ နှာခေါင်းပေါက်၊ နှာခေါင်းပိတ်၊ ကျေးဇူးပြု၍ မေးပါ (မိန်းကလေး၊ ၁ နှစ် ၁ လ)
你好，宝宝出现这种情况多久了？
昨天出现的
家里有桔贝配合个什么药啊
考虑感冒
可以用上感冒药
现在主要咳嗽流鼻涕鼻塞
晚上睡觉鼻子咕噜咕噜
你看哪种药配合桔贝合剂效果好，
感冒药就是缓解这些症状的
氨酚黄那敏
小儿氨酚黄那敏吗
对吗
对
好的
一次喝多少
昨天就不咳嗽，今天早上起来咳嗽连声，是不是我吃鸡蛋的原因
是不是不没吃鸡蛋
按说明吃就行
饮食清淡一些
还有宝宝大便每次都是前面一节硬结后面软，一天一次，正常吗？跟大人一样
跟感冒都有关系
平时没有感冒也是
每次大便脸赠的通红
感觉很用劲
有两三个月了
吃了小儿七星茶和益生菌也没有什么效果
那就去检查一下
看看胃肠道有没有问题
检查什么
先验个大便
做了腹部彩超
大便化验过也正常
那就应该是胃肠功能不太好
慢慢调理
没特别好的办法
但是七八个月前又好着
这个跟饮食也有关系
就是从吃颗粒食物出现的
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/ReMeDi/from_zh$
```

## ReMeDi Translation into English 

အင်္ဂလိပ်လို ပြန်ထားလိုက်ပြီး အဲဒီကနေ မြန်မာလို ပြန်ခိုင်းကြည့်မယ် စိတ်ကူး...  

(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ cat run4ReMeDi_toEn.sh  

```bash
#!/bin/bash

# Base directory for input files
INPUT_DIR="/home/ye/ye/exp/gpt-mt/nllb/data/ReMeDi-large"

# Directory for output files
OUTPUT_DIR="/home/ye/ye/exp/gpt-mt/nllb/ReMeDi/to_en"

# Create the output directory if it doesn't exist
mkdir -p "$OUTPUT_DIR"

# Function to translate Chinese sentences
translate_sentence() {
    local sentence="$1"
    local temp_input_file=$(mktemp)
    local temp_output_file=$(mktemp)

    echo "$sentence" > "$temp_input_file"
    ./nllb-translate.sh --input "$temp_input_file" --source zho_Hans --target eng_Latn  --output "$temp_output_file"

    local translated_output
    translated_output=$(cat "$temp_output_file")

    rm "$temp_input_file" "$temp_output_file"

    echo "$translated_output"
}

# Iterate over each .txt file in the input directory
for FILE in "$INPUT_DIR"/*.txt; do
    # Extract the base filename without the extension
    BASENAME=$(basename "$FILE" .txt)

    # Define the output file name
    OUTPUT_FILE="$OUTPUT_DIR/$BASENAME.my"

    # Create/empty the output file
    : > "$OUTPUT_FILE"

    # Read the input file line by line
    while IFS= read -r line || [[ -n "$line" ]]; do
        # Check if the line is a dialogue marker, blank line, or a Chinese sentence
        if [[ "$line" =~ ^Dialogue\ [0-9]+: ]] || [[ -z "$line" ]]; then
            echo "$line" >> "$OUTPUT_FILE"
        else
            # Extract the prefix (e.g., "doctor: ", "patient: ") and the actual sentence
            prefix=$(echo "$line" | grep -o '^[^:]*: ')
            sentence=$(echo "$line" | sed 's/^[^:]*: //')

            #echo "Prefix: $prefix";
            #echo "senence: $sentence";
            # Translate Chinese sentences
            translated_sentence=$(translate_sentence "$sentence")

            # Format the translated output
            formatted_line="${prefix}${sentence}\t${translated_sentence}"
            echo -e "$formatted_line" >> "$OUTPUT_FILE"
        fi
    done < "$FILE"
done

```

training model ပေါ်မူတည်နေလား မပြောတတ် တရုပ်ကနေ မြန်မာကို တိုက်ရိုက်ပြန်တာကမှ အလုပ်လုပ်သေးတယ်။ တရုပ်ကနေ အင်္ဂလိပ်ကို ပြန်ခိုင်းတာမှာ အောက်ပါအတိုင်း ရတယ်။ ဘာသာပြန်မပေးနိုင်ဘူး .... 

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/ReMeDi/to_en$ cat 0.my
Dialogue 0:
patient: 感冒能做普通的胃镜吗（男，24岁）       感冒能做普通的胃镜吗（男，24岁）        Can you do a normal GastroLens for a cold?
doctor: 你好，有没有发烧？扁桃体肿大吗？        你好，有没有发烧？扁桃体肿大吗？        你好，有没有发烧？扁桃体肿大吗？
patient: 发烧倒是没有喉咙上面有点疼痛   发烧倒是没有喉咙上面有点疼痛    发烧倒是没有喉咙上面有点疼痛
doctor: 那就晚些时间再做吧。    那就晚些时间再做吧。    那就晚些时间再做吧。
patient: 不能做是吗     不能做是吗      不能做是吗
doctor: 是的，因为胃镜的管子会通过咽喉部的。    是的，因为胃镜的管子会通过咽喉部的。    是的，因为胃镜的管子会通过咽喉部的。

Dialogue 1:
patient: 前列腺增生可以服用仁青芒觉吗（男，51岁）       前列腺增生可以服用仁青芒觉吗（男，51岁）  前列腺增生可以服用仁青芒觉吗（男，51岁）
doctor: 你好         可以的     你好         可以的     你好         可以的
patient: 我服用温肾前列胶囊和仁青芒觉   我服用温肾前列胶囊和仁青芒觉    我服用温肾前列胶囊和仁青芒觉
doctor: 可以    可以    可以
doctor: 这两个都属于中成药      这两个都属于中成药      这两个都属于中成药
doctor: 一般性情比较温和        一般性情比较温和        一般性情比较温和
patient: 没付作用吧     没付作用吧      没付作用吧
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/ReMeDi/to_en$
```

confirmation ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/ReMeDi/to_en$ cat -n ./0.my | tail
    42  doctor: 你最后一次月经是什么时候        你最后一次月经是什么时候        你最后一次月经是什么时候
    43  patient: 3月1号 3月1号  3月1号
    44  doctor: 四月中就可以了  四月中就可以了  四月中就可以了
    45  patient: 好吧 挺慢的    好吧 挺慢的     好吧 挺慢的
    46  patient: 我15号去检查应该就知道好不好了吧       我15号去检查应该就知道好不好了吧  我15号去检查应该就知道好不好了吧
    47  patient: 去做B超        去做B超 去做B超
    48  doctor: 是的    是的    是的
    49  patient: 做B超能查出什么        做B超能查出什么 做B超能查出什么
    50  doctor: 胎心    胎心    胎心
    51  patient: 15号查的出胎心吗       15号查的出胎心吗        15号查的出胎心吗
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/ReMeDi/to_en$
```

## Checking All Current Translation Outputs

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my/from_en$ cat -n ./apdf.my | tail
 10335  At the time, Chinese Foreign Ministry spokesperson Hong Lei said at a news conference that the ship’s equipment was “standard” and “no different from international practice,” Reuters reported.    At the time, Chinese Foreign Ministry spokesperson Hong Lei said at a news conference that the ship’s equipment was “standard” and “no different from international practice,” Reuters reported.
 10336  Meanwhile FBI Director James Comey noted that while there has been a drop in people traveling to join ISIL, the militants retain the ability to “motivate troubled souls.” Meanwhile FBI Director James Comey noted that while there has been a drop in people traveling to join ISIL, the militants retain the ability to “motivate troubled souls.”
 10337  Meanwhile, U.S. Secretary of State Rex Tillerson urged Southeast Asian foreign ministers to eliminate funding streams for North Korea’s missile and nuclear programs and to limit diplomatic relations with Pyongyang. (Pictured: U.S. Secretary of State Rex Tillerson, center, meets with Southeast Asian foreign ministers at a lunch in Washington, D.C.) Meanwhile, U.S. Secretary of State Rex Tillerson urged Southeast Asian foreign ministers to eliminate funding streams for North Korea’s missile and nuclear programs and to limit diplomatic relations with Pyongyang. (Pictured: U.S. Secretary of State Rex Tillerson, center, meets with Southeast Asian foreign ministers at a lunch in Washington, D.C.)
 10338  Jokowi, meanwhile, seeks to transform Indonesia into a maritime power and is passionate about maritime sovereignty for his country. Hence, repeated assertions about protecting freedom of navigation are unmistakably targeted at the PRC, which is engaged in hotly contested territorial disputes in the South and East China seas. Jakarta claims it is not a party to any territorial disputes with Beijing in the South China Sea; however, Indonesia has not hesitated in clashing with the PRC over fishing rights around the Natuna Islands. Jokowi’s dramatic gesture of holding a cabinet meeting aboard a warship off the Natunas just days after a Sino-Indonesian naval skirmish in 2016 was seen as a show of resolve toward the PRC.    Jokowi, meanwhile, seeks to transform Indonesia into a maritime power and is passionate about maritime sovereignty for his country. Hence, repeated assertions about protecting freedom of navigation are unmistakably targeted at the PRC, which is engaged in hotly contested territorial disputes in the South and East China seas. Jakarta claims it is not a party to any territorial disputes with Beijing in the South China Sea; however, Indonesia has not hesitated in clashing with the PRC over fishing rights around the Natuna Islands. Jokowi’s dramatic gesture of holding a cabinet meeting aboard a warship off the Natunas just days after a Sino-Indonesian naval skirmish in 2016 was seen as a show of resolve toward the PRC.
 10339  Meanwhile, Japan said in December 2016 it would ban any ships that call to port in North Korea and freeze assets of additional groups and individuals tied to North Korea’s nuclear and missile activities, Chief Cabinet Secretary Yoshihide Suga said during a news conference.     Meanwhile, Japan said in December 2016 it would ban any ships that call to port in North Korea and freeze assets of additional groups and individuals tied to North Korea’s nuclear and missile activities, Chief Cabinet Secretary Yoshihide Suga said during a news conference.
 10340  Meanwhile, the GDP of Indonesia, which is Southeast Asia’s largest economy already, will exceed U.S. $1 trillion by 2020, and surpass U.S. $3.7 trillion by 2030. “This will significantly increase Indonesia’ global geopolitical influence as a leading emerging market,” Biswas said.      Meanwhile, the GDP of Indonesia, which is Southeast Asia’s largest economy already, will exceed U.S. $1 trillion by 2020, and surpass U.S. $3.7 trillion by 2030. “This will significantly increase Indonesia’ global geopolitical influence as a leading emerging market,” Biswas said.
 10341  Meanwhile, New Zealand security experts have reported attempts by China to access sensitive public and private information, CNBC reported. Chinese funding has also been linked to the Peaceful Reunification of China Association in New Zealand. The interest group “engages in a range of activities which support Chinese foreign policy goals, including block-voting and fundraising for ethnic Chinese political candidates who agree to support their organization’s agenda,” said Anne-Marie Brady, a professor at the University of Canterbury, according to CNBC.        Meanwhile, New Zealand security experts have reported attempts by China to access sensitive public and private information, CNBC reported. Chinese funding has also been linked to the Peaceful Reunification of China Association in New Zealand. The interest group “engages in a range of activities which support Chinese foreign policy goals, including block-voting and fundraising for ethnic Chinese political candidates who agree to support their organization’s agenda,” said Anne-Marie Brady, a professor at the University of Canterbury, according to CNBC.
 10342  Meanwhile, Japanese sales of air purifiers and nuclear shelters have been brisk, according to Reuters.    Meanwhile, Japanese sales of air purifiers and nuclear shelters have been brisk, according to Reuters.
 10343  Pyongyang, meanwhile, called for the GSOMIA to be scrapped. Its government mouthpiece, the Korean Central News Agency, dubbed it, “an extremely dangerous and treacherous war agreement” in a May 2018 column.      Pyongyang, meanwhile, called for the GSOMIA to be scrapped. Its government mouthpiece, the Korean Central News Agency, dubbed it, “an extremely dangerous and treacherous war agreement” in a May 2018 column.
 10344  Hanoi, meanwhile, claims ownership of the Paracels, a group of islands and reefs in the South China Sea between Vietnam and China. The PRC seized the Parcels from Vietnam in a naval battle in 1974 and has been steadily building outposts on artificial islands constructed near the Paracels in recent years. The PRC is staking claims to the surrounding waters that Vietnam claims as part of its exclusive economic zone. The PRC pressured Vietnam to abandon oil drilling in the waters in 2018. Hanoi and Beijing also clash over possession of the Spratly Islands in the South China Sea.      Hanoi, meanwhile, claims ownership of the Paracels, a group of islands and reefs in the South China Sea between Vietnam and China. The PRC seized the Parcels from Vietnam in a naval battle in 1974 and has been steadily building outposts on artificial islands constructed near the Paracels in recent years. The PRC is staking claims to the surrounding waters that Vietnam claims as part of its exclusive economic zone. The PRC pressured Vietnam to abandon oil drilling in the waters in 2018. Hanoi and Beijing also clash over possession of the Spratly Islands in the South China Sea.
(base)
```

``` ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my/from_en$ cd ..
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my$ cd from_th/
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my/from_th$ ls
apdf.my
(base)
```

``` ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my/from_th$ cat -n ./apdf.my | tail
  5968  ฝูงเฮลิคอปเตอร์อาปาเช 36 ลำที่ติดตั้งขีปนาวุธเฮลไฟร์จำนวนที่เพียงพอในการทำลายรถถังหลายร้อยคัน เป็นหนึ่งยุทโธปกรณ์เพิ่มเติมล่าสุดในคลังสรรพาวุธของกองทัพสาธารณรัฐเกาหลี    ฝูงเฮลิคอปเตอร์อาปาเช 36 ลำที่ติดตั้งขีปนาวุธเฮลไฟร์จำนวนที่เพียงพอในการทำลายรถถังหลายร้อยคัน เป็นหนึ่งยุทโธปกรณ์เพิ่มเติมล่าสุดในคลังสรรพาวุธของกองทัพสาธารณรัฐเกาหลี
  5969  ฝ่ายค้านแสดงความกังวลว่า นายดูแตร์เตอาจทำให้ทั้งประเทศตกอยู่ภายใต้กฎอัยการศึกในท้ายที่สุด แต่ทางการได้เมินเฉยต่อความกังวลนี้      ฝ่ายค้านแสดงความกังวลว่า นายดูแตร์เตอาจทำให้ทั้งประเทศตกอยู่ภายใต้กฎอัยการศึกในท้ายที่สุด แต่ทางการได้เมินเฉยต่อความกังวลนี้
  5970  ฝ่ายทหารเห็นว่าตนเป็นผู้นำด้านการปกครองแบบขาวสะอาด ซึ่งต่างจากนักการเมืองพลเรือนและกลุ่มคนใกล้ชิดในวงการธุรกิจที่มักจะเป็นพวกทุจริต แม้ฝ่ายทหารเองจะมีผลประโยชน์อย่างกว้างขวางในหลายส่วนของเศรษฐกิจ ฝ่ายทหารเห็นว่าตนเป็นผู้นำด้านการปกครองแบบขาวสะอาด ซึ่งต่างจากนักการเมืองพลเรือนและกลุ่มคนใกล้ชิดในวงการธุรกิจที่มักจะเป็นพวกทุจริต แม้ฝ่ายทหารเองจะมีผลประโยชน์อย่างกว้างขวางในหลายส่วนของเศรษฐกิจ
  5971  ฝ่ายทหารได้รับการรับประกันที่นั่งในรัฐสภาร้อยละ 25 ตามรัฐธรรมนูญ รวมทั้งตำแหน่งสำคัญ ๆ ด้านความมั่นคงและข้าราชการ ซึ่งอาจทำให้การบริหารของรัฐบาลจากพรรคสันนิบาตแห่งชาติเพื่อประชาธิปไตยหยุดชะงักได้ ฝ่ายทหารได้รับการรับประกันที่นั่งในรัฐสภาร้อยละ 25 ตามรัฐธรรมนูญ รวมทั้งตำแหน่งสำคัญ ๆ ด้านความมั่นคงและข้าราชการ ซึ่งอาจทำให้การบริหารของรัฐบาลจากพรรคสันนิบาตแห่งชาติเพื่อประชาธิปไตยหยุดชะงักได้
  5972  ฝ่ายบริหารของนายบารัก โอบามา ประธานาธิบดีสหรัฐฯ ได้แจ้งแก่รัฐสภาอย่างเป็นทางการเมื่อเดือนธันวาคม พ.ศ. 2558 เกี่ยวกับแพ็คเกจการขายอาวุธมูลค่า 1.83 พันล้านดอลลาร์สหรัฐฯ (ประมาณ 6.4 หมื่นล้านบาท) ให้กับไต้หวัน ซึ่งประกอบด้วยเรือรบขนาดกลางสองลำ ขีปนาวุธต่อต้านรถถัง ยานโจมตีสะเทินน้ำสะเทินบก และยุทโธปกรณ์อื่น ๆ ซึ่งทำให้เกิดการตอบโต้อย่างโกรธเคืองจากจีน ฝ่ายบริหารของนายบารัก โอบามา ประธานาธิบดีสหรัฐฯ ได้แจ้งแก่รัฐสภาอย่างเป็นทางการเมื่อเดือนธันวาคม พ.ศ. 2558 เกี่ยวกับแพ็คเกจการขายอาวุธมูลค่า 1.83 พันล้านดอลลาร์สหรัฐฯ (ประมาณ 6.4 หมื่นล้านบาท) ให้กับไต้หวัน ซึ่งประกอบด้วยเรือรบขนาดกลางสองลำ ขีปนาวุธต่อต้านรถถัง ยานโจมตีสะเทินน้ำสะเทินบก และยุทโธปกรณ์อื่น ๆ ซึ่งทำให้เกิดการตอบโต้อย่างโกรธเคืองจากจีน
  5973  ฝ่ายเศรษฐกิจของกลุ่มราษฏรียสวยัมเสวกสังฆ์รณรงค์ให้ตัดบริษัทหัวเว่ย เทคโนโลยีออกจากแผนของอินเดียที่จะติดตั้งเครือข่ายโทรศัพท์เคลื่อนที่ 5จี รุ่นถัดไป      ฝ่ายเศรษฐกิจของกลุ่มราษฏรียสวยัมเสวกสังฆ์รณรงค์ให้ตัดบริษัทหัวเว่ย เทคโนโลยีออกจากแผนของอินเดียที่จะติดตั้งเครือข่ายโทรศัพท์เคลื่อนที่ 5จี รุ่นถัดไป
  5974  พ.ต. นิทินโจชิจากสถาบันการฝึกร่างกายของกองทัพเห็นด้วยหลังจากได้ใช้เวลาสองสัปดาห์ในโคอิมบาทอร์     พ.ต. นิทินโจชิจากสถาบันการฝึกร่างกายของกองทัพเห็นด้วยหลังจากได้ใช้เวลาสองสัปดาห์ในโคอิมบาทอร์
  5975  พ.ต. อามินกล่าวว่า เรือรบได้ยิงปืนไปที่ท้ายเรือของเรือประมงกุย เบ ยู-27088 หลังจากที่เพิกเฉยต่อการเตือนซ้ำแล้วซ้ำเล่าเพื่อให้หยุดจับปลา พ.ต. อามินกล่าวว่าไม่มีผู้ใดได้รับบาดเจ็บ   พ.ต. อามินกล่าวว่า เรือรบได้ยิงปืนไปที่ท้ายเรือของเรือประมงกุย เบ ยู-27088 หลังจากที่เพิกเฉยต่อการเตือนซ้ำแล้วซ้ำเล่าเพื่อให้หยุดจับปลา พ.ต. อามินกล่าวว่าไม่มีผู้ใดได้รับบาดเจ็บ
  5976  พ.ต.หญิง จินกานเป็นผู้หญิงคนแรกที่เข้ารับราชการในกองทัพบกอินเดียในฐานะนักเรียนทหารในปี พ.ศ. 2536 ในขณะที่เป็นเจ้าหน้าที่อายุน้อย พ.ต.หญิง จินกานศึกษาด้านกฎหมายทหารและทำหน้าที่ตุลาการในศาลทหารของกรมพระธรรมนูญขณะมียศพันตรีหญิงในปี พ.ศ. 2541      พ.ต.หญิง จินกานเป็นผู้หญิงคนแรกที่เข้ารับราชการในกองทัพบกอินเดียในฐานะนักเรียนทหารในปี พ.ศ. 2536 ในขณะที่เป็นเจ้าหน้าที่อายุน้อย พ.ต.หญิง จินกานศึกษาด้านกฎหมายทหารและทำหน้าที่ตุลาการในศาลทหารของกรมพระธรรมนูญขณะมียศพันตรีหญิงในปี พ.ศ. 2541
  5977  พ.ต.หญิง จินกานเล่าถึงความไม่น่าเป็นไปได้เมื่อเธอพยายามที่จะเป็นเจ้าหน้าที่ทหารประจำการ “ดิฉันเป็นหนึ่งในผู้สมัครหญิงจำนวน 25,000 คน” พ.ต.หญิง จินกานกล่าว “จากจำนวนทั้งหมดนี้ 250 คนถูกเรียกตัวสัมภาษณ์ และ 25 คนได้รับคัดเลือกเข้ารับราชการในกองทัพบก 25 คนแรกที่ได้รับคัดเลือกนี้ได้ติดยศร้อยตรีหลังจากเสร็จสิ้นการฝึก สองคนลาออกหลังจากห้าปีแรก เมื่อครบกำหนดออกจากราชการในปี พ.ศ. 2556 ก็เหลือเพียงเจ็ดคนที่ปฏิบัติงานในกองทัพบก”  พ.ต.หญิง จินกานเล่าถึงความไม่น่าเป็นไปได้เมื่อเธอพยายามที่จะเป็นเจ้าหน้าที่ทหารประจำการ “ดิฉันเป็นหนึ่งในผู้สมัครหญิงจำนวน 25,000 คน” พ.ต.หญิง จินกานกล่าว “จากจำนวนทั้งหมดนี้ 250 คนถูกเรียกตัวสัมภาษณ์ และ 25 คนได้รับคัดเลือกเข้ารับราชการในกองทัพบก 25 คนแรกที่ได้รับคัดเลือกนี้ได้ติดยศร้อยตรีหลังจากเสร็จสิ้นการฝึก สองคนลาออกหลังจากห้าปีแรก เมื่อครบกำหนดออกจากราชการในปี พ.ศ. 2556 ก็เหลือเพียงเจ็ดคนที่ปฏิบัติงานในกองทัพบก”
(base)
```

``` ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my/from_th$ cd ..
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my$ ls
from_en  from_th
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb/scb-my$ cd ..
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ ls
banglanmt  nllb-translate.sh         ReMeDi                   run4ReMeDi_toEn.sh   scb-my
bk         output_th-my_mahidol.txt  run4banglanmt_fromEn.sh  run4scb_fromThai.sh  tmp
data       output_th-my.txt          run4ReMeDi_fromZh.sh     run4scb.sh
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ wc output_th-my*
   67597   681559 12085835 output_th-my_mahidol.txt
    8063    80883  1452528 output_th-my.txt
   75660   762442 13538363 total
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ wc output_th-my*
   67597   681559 12085835 output_th-my_mahidol.txt
    8063    80883  1452528 output_th-my.txt
   75660   762442 13538363 total
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ wc output_th-my*
   67598   681577 12086063 output_th-my_mahidol.txt
    8063    80883  1452528 output_th-my.txt
   75661   762460 13538591 total
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ wc output_th-my*
   67598   681577 12086063 output_th-my_mahidol.txt
    8063    80883  1452528 output_th-my.txt
   75661   762460 13538591 total
```

```
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$ cat -n ./output_th-my_mahidol.txt | tail
 67590  แสบ ตา มาก ลืม ตา ไม่ ขึ้น เลย  မျက်လုံးတွေ မမြင်နိုင်အောင် မေ့နေတတ်တယ်။
 67591  ซึ่ง ใน กรณี ที่ ครรภ์ น้อย กว่า 34 สัปดาห์     ซึ่ง ใน กรณี ที่ ครรภ์ น้อย กว่า 34 สัปดาห์
 67592  ใน แนวทาง การ ป้องกัน   ใน แนวทาง การ ป้องกัน
 67593  กัน ไว้ เผื่อ ติด เชื้อ ค่ะ     กัน ไว้ เผื่อ ติด เชื้อ ค่ะ
 67594  มา ส่ง ที่ รพ. เลย ค่ะ  มา ส่ง ที่ รพ. เลย ค่ะ
 67595  ถ่าย เหลว ไหม   ถ่าย เหลว ไหม
 67596  ติด นิ้ว เท้า ไว้ และ ยืด หลัง  ติด นิ้ว เท้า ไว้ และ ยืด หลัง
 67597  เขา 2 ปี แล้ว   เขา 2 ปี แล้ว
 67598  แต่ มี ปัญหา เกี่ยว กับ การ หายใจ เป็น หลัก     แต่ มี ปัญหา เกี่ยว กับ การ หายใจ เป็น หลัก
 67599  มอง ด้าน บน ค่ะ มอง ด้าน บน ค่ะ
(base) ye@lst-gpu-server-197:~/ye/exp/gpt-mt/nllb$
```

