# PSFU to BMP/txt Conversion

## Git Clone

ဒီတစ်ခါတော့ rw-psf perl script ကို သုံးကြည့်မယ်။  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev$ git clone https://github.com/talamus/rw-psf
Cloning into 'rw-psf'...
remote: Enumerating objects: 8, done.
remote: Total 8 (delta 0), reused 0 (delta 0), pack-reused 8
Unpacking objects: 100% (8/8), done.
```

## PSFU File Preparation

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/rw-psf/test-conv$ cp ../../ttf-console-fonts-20170403_abc5771/ye-x.psfu* .
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/rw-psf/test-conv$ ls
ye-x.psfu  ye-x.psfu.txt
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/rw-psf/test-conv$ 
```

## Convert to BMP File

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/rw-psf/test-conv$ perl ./readpsf ./ye-x.psfu bmp
Possible precedence issue with control flow operator at ./readpsf line 466.
Possible precedence issue with control flow operator at ./readpsf line 472.
Reading './ye-x.psfu'...
Version 2 PSF file.
Font has an unicode table. Use 'psfgettable' command to extract it.
PSF file suggests 512 glyphs of size 16 x 32.
512 glyphs found.

Creating an image.

'./ye-x.16x32.bmp' written. All Ok.
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/rw-psf/test-conv$ 
```

output file ကို fig folder အောက်မှာ သိမ်းထားတယ်။  
[https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/psf2bmp/ye-x.16x32.bmp](https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/psf2bmp/ye-x.16x32.bmp)  

ပုံကတော့ အောက်ပါအတိုင်းမို့လို့ ttf ဖိုင်ကနေ psfu ပြောင်းတဲ့ နေရာမှာပဲ error ရှိသလားလို့ ... ?!  

![converted bmp file](https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/psf2bmp/ye-x.16x32.bmp "converted bmp file for Myanmar3")

## Check PSF/PSFU Files 

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/rw-psf/test-conv$ find /usr/ -name '*.psf*' > psf-file-info.txt
```

စုစုပေါင်း psf ဖိုင် ၃၀၀ ကို အောက်ပါအတိုင်း တွေ့ရ ...  

```
/usr/share/doc/texlive-doc/fonts/musixtex-fonts/CHANGES.psfonts
/usr/share/doc/texlive-doc/fonts/musixtex-fonts/README.psfonts.gz
/usr/share/consolefonts/Armenian-Fixed15.psf.gz
/usr/share/consolefonts/Lat2-TerminusBold24x12.psf.gz
/usr/share/consolefonts/Ethiopian-Fixed18.psf.gz
/usr/share/consolefonts/Lat15-Terminus22x11.psf.gz
/usr/share/consolefonts/Lat15-VGA16.psf.gz
/usr/share/consolefonts/Lat15-TerminusBoldVGA16.psf.gz
/usr/share/consolefonts/Lat2-Fixed15.psf.gz
/usr/share/consolefonts/Uni3-TerminusBold20x10.psf.gz
/usr/share/consolefonts/CyrKoi-TerminusBold22x11.psf.gz
/usr/share/consolefonts/Uni1-VGA8.psf.gz
/usr/share/consolefonts/Uni2-Fixed14.psf.gz
/usr/share/consolefonts/Lat38-VGA28x16.psf.gz
/usr/share/consolefonts/Lat15-TerminusBold22x11.psf.gz
/usr/share/consolefonts/CyrAsia-TerminusBold32x16.psf.gz
/usr/share/consolefonts/Uni3-Terminus22x11.psf.gz
/usr/share/consolefonts/Uni2-Terminus16.psf.gz
/usr/share/consolefonts/CyrAsia-Fixed15.psf.gz
/usr/share/consolefonts/CyrKoi-Fixed18.psf.gz
/usr/share/consolefonts/Lat7-Fixed18.psf.gz
/usr/share/consolefonts/Lat7-VGA28x16.psf.gz
/usr/share/consolefonts/Hebrew-Fixed15.psf.gz
/usr/share/consolefonts/CyrKoi-TerminusBold32x16.psf.gz
/usr/share/consolefonts/CyrKoi-Terminus14.psf.gz
/usr/share/consolefonts/Arabic-Fixed16.psf.gz
/usr/share/consolefonts/CyrAsia-Fixed16.psf.gz
/usr/share/consolefonts/Lat7-Fixed16.psf.gz
/usr/share/consolefonts/CyrKoi-Fixed14.psf.gz
/usr/share/consolefonts/Vietnamese-Fixed18.psf.gz
/usr/share/consolefonts/Uni3-Terminus20x10.psf.gz
/usr/share/consolefonts/Lat7-TerminusBoldVGA16.psf.gz
/usr/share/consolefonts/Vietnamese-Fixed16.psf.gz
/usr/share/consolefonts/Lat7-TerminusBold14.psf.gz
/usr/share/consolefonts/Lat38-VGA16.psf.gz
/usr/share/consolefonts/Lat38-Fixed13.psf.gz
/usr/share/consolefonts/Greek-Fixed16.psf.gz
/usr/share/consolefonts/Ethiopian-GohaClassic16.psf.gz
/usr/share/consolefonts/CyrAsia-Fixed14.psf.gz
/usr/share/consolefonts/Lat7-TerminusBold28x14.psf.gz
/usr/share/consolefonts/Uni3-TerminusBoldVGA16.psf.gz
/usr/share/consolefonts/Greek-Terminus32x16.psf.gz
/usr/share/consolefonts/Lat15-VGA8.psf.gz
/usr/share/consolefonts/Georgian-Fixed14.psf.gz
/usr/share/consolefonts/Armenian-Fixed14.psf.gz
/usr/share/consolefonts/Lao-Fixed14.psf.gz
/usr/share/consolefonts/CyrKoi-VGA28x16.psf.gz
/usr/share/consolefonts/Lat2-TerminusBold14.psf.gz
/usr/share/consolefonts/Uni2-TerminusBold28x14.psf.gz
/usr/share/consolefonts/CyrSlav-Terminus20x10.psf.gz
/usr/share/consolefonts/CyrSlav-VGA32x16.psf.gz
/usr/share/consolefonts/Lat7-VGA14.psf.gz
/usr/share/consolefonts/CyrSlav-TerminusBold20x10.psf.gz
/usr/share/consolefonts/Greek-TerminusBold32x16.psf.gz
/usr/share/consolefonts/Lat2-TerminusBold32x16.psf.gz
/usr/share/consolefonts/Lat7-VGA16.psf.gz
/usr/share/consolefonts/Lat2-Fixed18.psf.gz
/usr/share/consolefonts/Uni3-TerminusBold24x12.psf.gz
/usr/share/consolefonts/Uni3-Terminus24x12.psf.gz
/usr/share/consolefonts/CyrSlav-Fixed16.psf.gz
/usr/share/consolefonts/Lat7-Terminus28x14.psf.gz
/usr/share/consolefonts/Uni2-Terminus22x11.psf.gz
/usr/share/consolefonts/Lat2-Terminus32x16.psf.gz
/usr/share/consolefonts/CyrAsia-Fixed18.psf.gz
/usr/share/consolefonts/Greek-Terminus28x14.psf.gz
/usr/share/consolefonts/CyrSlav-Fixed13.psf.gz
/usr/share/consolefonts/CyrSlav-Terminus28x14.psf.gz
/usr/share/consolefonts/Greek-VGA8.psf.gz
/usr/share/consolefonts/Lat2-VGA8.psf.gz
/usr/share/consolefonts/Lat2-VGA28x16.psf.gz
/usr/share/consolefonts/CyrKoi-Terminus22x11.psf.gz
/usr/share/consolefonts/Lat7-Fixed15.psf.gz
/usr/share/consolefonts/Arabic-VGA8.psf.gz
/usr/share/consolefonts/Lat2-TerminusBoldVGA14.psf.gz
/usr/share/consolefonts/CyrAsia-TerminusBold16.psf.gz
/usr/share/consolefonts/Hebrew-VGA8.psf.gz
/usr/share/consolefonts/Lat7-Terminus12x6.psf.gz
/usr/share/consolefonts/Lat7-Fixed14.psf.gz
/usr/share/consolefonts/CyrSlav-Fixed15.psf.gz
/usr/share/consolefonts/Uni2-Fixed15.psf.gz
/usr/share/consolefonts/Greek-TerminusBold28x14.psf.gz
/usr/share/consolefonts/CyrKoi-Terminus20x10.psf.gz
/usr/share/consolefonts/Uni3-TerminusBold14.psf.gz
/usr/share/consolefonts/Lao-Fixed16.psf.gz
/usr/share/consolefonts/Lat2-Terminus12x6.psf.gz
/usr/share/consolefonts/Lat15-Terminus12x6.psf.gz
/usr/share/consolefonts/Greek-Terminus16.psf.gz
/usr/share/consolefonts/CyrAsia-TerminusBold22x11.psf.gz
/usr/share/consolefonts/Lat7-Terminus22x11.psf.gz
/usr/share/consolefonts/Uni2-TerminusBold16.psf.gz
/usr/share/consolefonts/Uni2-Terminus28x14.psf.gz
/usr/share/consolefonts/CyrKoi-VGA16.psf.gz
/usr/share/consolefonts/CyrSlav-Terminus22x11.psf.gz
/usr/share/consolefonts/Greek-TerminusBoldVGA16.psf.gz
/usr/share/consolefonts/CyrAsia-TerminusBold28x14.psf.gz
/usr/share/consolefonts/Greek-Terminus20x10.psf.gz
/usr/share/consolefonts/Ethiopian-Goha12.psf.gz
/usr/share/consolefonts/Lat15-Terminus14.psf.gz
/usr/share/consolefonts/Ethiopian-Goha14.psf.gz
/usr/share/consolefonts/CyrAsia-Fixed13.psf.gz
/usr/share/consolefonts/CyrSlav-TerminusBold22x11.psf.gz
/usr/share/consolefonts/CyrAsia-TerminusBoldVGA16.psf.gz
/usr/share/consolefonts/CyrKoi-TerminusBoldVGA14.psf.gz
/usr/share/consolefonts/CyrKoi-Terminus32x16.psf.gz
/usr/share/consolefonts/Uni3-TerminusBold16.psf.gz
/usr/share/consolefonts/Greek-VGA14.psf.gz
/usr/share/consolefonts/Lat2-TerminusBold28x14.psf.gz
/usr/share/consolefonts/Uni2-VGA14.psf.gz
/usr/share/consolefonts/Greek-TerminusBold14.psf.gz
/usr/share/consolefonts/CyrKoi-Terminus12x6.psf.gz
/usr/share/consolefonts/CyrSlav-VGA14.psf.gz
/usr/share/consolefonts/Lat7-TerminusBold32x16.psf.gz
/usr/share/consolefonts/Uni2-VGA28x16.psf.gz
/usr/share/consolefonts/Lat7-TerminusBoldVGA14.psf.gz
/usr/share/consolefonts/CyrKoi-TerminusBold20x10.psf.gz
/usr/share/consolefonts/Hebrew-VGA16.psf.gz
/usr/share/consolefonts/Armenian-Fixed13.psf.gz
/usr/share/consolefonts/Arabic-VGA14.psf.gz
/usr/share/consolefonts/Lat15-Terminus20x10.psf.gz
/usr/share/consolefonts/CyrAsia-Terminus28x14.psf.gz
/usr/share/consolefonts/Lat7-TerminusBold20x10.psf.gz
/usr/share/consolefonts/Lat15-TerminusBold14.psf.gz
/usr/share/consolefonts/Lat15-TerminusBold24x12.psf.gz
/usr/share/consolefonts/Georgian-Fixed18.psf.gz
/usr/share/consolefonts/Greek-VGA28x16.psf.gz
/usr/share/consolefonts/Georgian-Fixed13.psf.gz
/usr/share/consolefonts/CyrKoi-TerminusBold28x14.psf.gz
/usr/share/consolefonts/Armenian-Fixed18.psf.gz
/usr/share/consolefonts/Greek-TerminusBold22x11.psf.gz
/usr/share/consolefonts/Uni2-VGA32x16.psf.gz
/usr/share/consolefonts/CyrAsia-TerminusBold24x12.psf.gz
/usr/share/consolefonts/CyrSlav-VGA16.psf.gz
/usr/share/consolefonts/Ethiopian-GohaClassic14.psf.gz
/usr/share/consolefonts/Lat15-TerminusBold16.psf.gz
/usr/share/consolefonts/Lat38-VGA14.psf.gz
/usr/share/consolefonts/Greek-Fixed13.psf.gz
/usr/share/consolefonts/Lat2-Fixed16.psf.gz
/usr/share/consolefonts/Uni2-Fixed16.psf.gz
/usr/share/consolefonts/Lat7-Fixed13.psf.gz
/usr/share/consolefonts/Lat38-VGA8.psf.gz
/usr/share/consolefonts/Uni1-VGA28x16.psf.gz
/usr/share/consolefonts/Lat38-Fixed14.psf.gz
/usr/share/consolefonts/Greek-TerminusBold16.psf.gz
/usr/share/consolefonts/Uni2-TerminusBold20x10.psf.gz
/usr/share/consolefonts/Lat7-Terminus24x12.psf.gz
/usr/share/consolefonts/Uni3-Fixed16.psf.gz
/usr/share/consolefonts/Uni2-Terminus24x12.psf.gz
/usr/share/consolefonts/CyrAsia-TerminusBold14.psf.gz
/usr/share/consolefonts/Greek-Fixed14.psf.gz
/usr/share/consolefonts/Thai-Fixed18.psf.gz
/usr/share/consolefonts/Georgian-Fixed16.psf.gz
/usr/share/consolefonts/Thai-Fixed15.psf.gz
/usr/share/consolefonts/CyrKoi-VGA8.psf.gz
/usr/share/consolefonts/Greek-TerminusBold24x12.psf.gz
/usr/share/consolefonts/Lat38-Fixed15.psf.gz
/usr/share/consolefonts/CyrKoi-TerminusBoldVGA16.psf.gz
/usr/share/consolefonts/Lat7-VGA32x16.psf.gz
/usr/share/consolefonts/Lat7-Terminus20x10.psf.gz
/usr/share/consolefonts/Ethiopian-Fixed15.psf.gz
/usr/share/consolefonts/Lat15-Fixed15.psf.gz
/usr/share/consolefonts/CyrKoi-Terminus28x14.psf.gz
/usr/share/consolefonts/Uni3-Terminus16.psf.gz
/usr/share/consolefonts/Uni2-Terminus12x6.psf.gz
/usr/share/consolefonts/Hebrew-Fixed14.psf.gz
/usr/share/consolefonts/Arabic-VGA32x16.psf.gz
/usr/share/consolefonts/Lat15-TerminusBoldVGA14.psf.gz
/usr/share/consolefonts/Uni2-Fixed18.psf.gz
/usr/share/consolefonts/Uni2-VGA16.psf.gz
/usr/share/consolefonts/Vietnamese-Fixed13.psf.gz
/usr/share/consolefonts/Ethiopian-GohaClassic12.psf.gz
/usr/share/consolefonts/Lat15-Fixed18.psf.gz
/usr/share/consolefonts/CyrKoi-VGA14.psf.gz
/usr/share/consolefonts/Uni1-Fixed15.psf.gz
/usr/share/consolefonts/Lao-Fixed15.psf.gz
/usr/share/consolefonts/CyrAsia-Terminus24x12.psf.gz
/usr/share/consolefonts/CyrKoi-Terminus16.psf.gz
/usr/share/consolefonts/Uni3-Fixed18.psf.gz
/usr/share/consolefonts/Greek-Terminus24x12.psf.gz
/usr/share/consolefonts/CyrSlav-Terminus24x12.psf.gz
/usr/share/consolefonts/Hebrew-Fixed16.psf.gz
/usr/share/consolefonts/Uni2-Fixed13.psf.gz
/usr/share/consolefonts/CyrSlav-Terminus14.psf.gz
/usr/share/consolefonts/Ethiopian-Goha16.psf.gz
/usr/share/consolefonts/Lat2-Terminus22x11.psf.gz
/usr/share/consolefonts/CyrKoi-Fixed16.psf.gz
/usr/share/consolefonts/Uni2-TerminusBoldVGA14.psf.gz
/usr/share/consolefonts/Lat7-VGA8.psf.gz
/usr/share/consolefonts/CyrKoi-VGA32x16.psf.gz
/usr/share/consolefonts/CyrSlav-TerminusBold16.psf.gz
/usr/share/consolefonts/CyrKoi-TerminusBold14.psf.gz
/usr/share/consolefonts/Uni3-Terminus14.psf.gz
/usr/share/consolefonts/Uni1-Fixed16.psf.gz
/usr/share/consolefonts/Hebrew-VGA14.psf.gz
/usr/share/consolefonts/Georgian-Fixed15.psf.gz
/usr/share/consolefonts/Uni2-TerminusBold24x12.psf.gz
/usr/share/consolefonts/Lat2-TerminusBold22x11.psf.gz
/usr/share/consolefonts/CyrSlav-TerminusBold32x16.psf.gz
/usr/share/consolefonts/Uni2-Terminus20x10.psf.gz
/usr/share/consolefonts/CyrAsia-Terminus12x6.psf.gz
/usr/share/consolefonts/Lat2-Terminus16.psf.gz
/usr/share/consolefonts/Greek-Fixed15.psf.gz
/usr/share/consolefonts/CyrSlav-TerminusBoldVGA14.psf.gz
/usr/share/consolefonts/Uni3-Terminus28x14.psf.gz
/usr/share/consolefonts/Lat2-VGA32x16.psf.gz
/usr/share/consolefonts/Greek-Terminus22x11.psf.gz
/usr/share/consolefonts/CyrKoi-TerminusBold24x12.psf.gz
/usr/share/consolefonts/Uni2-Terminus32x16.psf.gz
/usr/share/consolefonts/CyrSlav-Terminus16.psf.gz
/usr/share/consolefonts/CyrKoi-Fixed13.psf.gz
/usr/share/consolefonts/Lat38-Fixed18.psf.gz
/usr/share/consolefonts/Lat2-Fixed14.psf.gz
/usr/share/consolefonts/Thai-Fixed14.psf.gz
/usr/share/consolefonts/Uni2-TerminusBold14.psf.gz
/usr/share/consolefonts/Uni2-VGA8.psf.gz
/usr/share/consolefonts/Lat15-Fixed16.psf.gz
/usr/share/consolefonts/Greek-Fixed18.psf.gz
/usr/share/consolefonts/Hebrew-VGA32x16.psf.gz
/usr/share/consolefonts/Lat15-TerminusBold32x16.psf.gz
/usr/share/consolefonts/Lat7-Terminus16.psf.gz
/usr/share/consolefonts/CyrAsia-Terminus22x11.psf.gz
/usr/share/consolefonts/CyrAsia-Terminus14.psf.gz
/usr/share/consolefonts/Uni3-Fixed15.psf.gz
/usr/share/consolefonts/CyrSlav-Fixed18.psf.gz
/usr/share/consolefonts/CyrAsia-Terminus32x16.psf.gz
/usr/share/consolefonts/Lat2-TerminusBold20x10.psf.gz
/usr/share/consolefonts/CyrSlav-Terminus12x6.psf.gz
/usr/share/consolefonts/CyrAsia-TerminusBoldVGA14.psf.gz
/usr/share/consolefonts/Uni1-VGA32x16.psf.gz
/usr/share/consolefonts/Uni2-TerminusBoldVGA16.psf.gz
/usr/share/consolefonts/Lat15-VGA32x16.psf.gz
/usr/share/consolefonts/Greek-VGA32x16.psf.gz
/usr/share/consolefonts/Lat7-TerminusBold16.psf.gz
/usr/share/consolefonts/CyrSlav-TerminusBold24x12.psf.gz
/usr/share/consolefonts/Arabic-VGA28x16.psf.gz
/usr/share/consolefonts/Greek-VGA16.psf.gz
/usr/share/consolefonts/Uni3-Terminus32x16.psf.gz
/usr/share/consolefonts/CyrAsia-Terminus20x10.psf.gz
/usr/share/consolefonts/Uni1-VGA16.psf.gz
/usr/share/consolefonts/Lat2-Terminus14.psf.gz
/usr/share/consolefonts/Lat7-Terminus14.psf.gz
/usr/share/consolefonts/CyrSlav-TerminusBold28x14.psf.gz
/usr/share/consolefonts/CyrSlav-TerminusBold14.psf.gz
/usr/share/consolefonts/Lat15-VGA28x16.psf.gz
/usr/share/consolefonts/Uni2-TerminusBold22x11.psf.gz
/usr/share/consolefonts/Hebrew-VGA28x16.psf.gz
/usr/share/consolefonts/Lat2-Terminus24x12.psf.gz
/usr/share/consolefonts/CyrKoi-Terminus24x12.psf.gz
/usr/share/consolefonts/CyrAsia-TerminusBold20x10.psf.gz
/usr/share/consolefonts/Lat2-VGA16.psf.gz
/usr/share/consolefonts/Lat7-TerminusBold22x11.psf.gz
/usr/share/consolefonts/Uni3-Fixed13.psf.gz
/usr/share/consolefonts/Hebrew-Fixed18.psf.gz
/usr/share/consolefonts/Lat7-TerminusBold24x12.psf.gz
/usr/share/consolefonts/CyrKoi-TerminusBold16.psf.gz
/usr/share/consolefonts/Lat15-Fixed13.psf.gz
/usr/share/consolefonts/Lat2-Terminus20x10.psf.gz
/usr/share/consolefonts/Uni3-TerminusBold22x11.psf.gz
/usr/share/consolefonts/Greek-TerminusBold20x10.psf.gz
/usr/share/consolefonts/Uni2-Terminus14.psf.gz
/usr/share/consolefonts/Uni3-Fixed14.psf.gz
/usr/share/consolefonts/Greek-Terminus14.psf.gz
/usr/share/consolefonts/Lat15-TerminusBold20x10.psf.gz
/usr/share/consolefonts/Uni1-VGA14.psf.gz
/usr/share/consolefonts/Lat38-Fixed16.psf.gz
/usr/share/consolefonts/Uni3-TerminusBold28x14.psf.gz
/usr/share/consolefonts/Lat15-Terminus24x12.psf.gz
/usr/share/consolefonts/CyrAsia-Terminus16.psf.gz
/usr/share/consolefonts/CyrSlav-VGA8.psf.gz
/usr/share/consolefonts/Lat2-VGA14.psf.gz
/usr/share/consolefonts/Hebrew-Fixed13.psf.gz
/usr/share/consolefonts/CyrSlav-Terminus32x16.psf.gz
/usr/share/consolefonts/Armenian-Fixed16.psf.gz
/usr/share/consolefonts/Lat38-VGA32x16.psf.gz
/usr/share/consolefonts/Lat15-Fixed14.psf.gz
/usr/share/consolefonts/CyrSlav-VGA28x16.psf.gz
/usr/share/consolefonts/Lat7-Terminus32x16.psf.gz
/usr/share/consolefonts/CyrSlav-TerminusBoldVGA16.psf.gz
/usr/share/consolefonts/Lat2-Fixed13.psf.gz
/usr/share/consolefonts/Arabic-Fixed15.psf.gz
/usr/share/consolefonts/Arabic-VGA16.psf.gz
/usr/share/consolefonts/Vietnamese-Fixed14.psf.gz
/usr/share/consolefonts/Uni2-TerminusBold32x16.psf.gz
/usr/share/consolefonts/CyrKoi-Fixed15.psf.gz
/usr/share/consolefonts/Uni3-TerminusBold32x16.psf.gz
/usr/share/consolefonts/Lat15-Terminus32x16.psf.gz
/usr/share/consolefonts/Thai-Fixed16.psf.gz
/usr/share/consolefonts/Uni3-Terminus12x6.psf.gz
/usr/share/consolefonts/Lat2-TerminusBold16.psf.gz
/usr/share/consolefonts/Lat15-Terminus16.psf.gz
/usr/share/consolefonts/Greek-TerminusBoldVGA14.psf.gz
/usr/share/consolefonts/Lat2-Terminus28x14.psf.gz
/usr/share/consolefonts/Thai-Fixed13.psf.gz
/usr/share/consolefonts/CyrSlav-Fixed14.psf.gz
/usr/share/consolefonts/Lat15-VGA14.psf.gz
/usr/share/consolefonts/Lat15-TerminusBold28x14.psf.gz
/usr/share/consolefonts/Uni3-TerminusBoldVGA14.psf.gz
/usr/share/consolefonts/Vietnamese-Fixed15.psf.gz
/usr/share/consolefonts/Lat2-TerminusBoldVGA16.psf.gz
/usr/share/consolefonts/Greek-Terminus12x6.psf.gz
/usr/share/consolefonts/Lat15-Terminus28x14.psf.gz
```

## Test Conversion for Thai Font

လက်ရှိ စက်မှာ ထိုင်းနဲ့ ပတ်သက်တဲ့ သို့မဟုတ် ဖိုင်နာမည်မှာ Thai ပါတဲ့ psf ဖိုင်က အောက်ပါအတိုင်း ၅ ဖိုင်ကို တွေ့ခဲ့ရ ...  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/rw-psf/test-conv$ cat ./psf-file-info.txt | grep "Thai"
/usr/share/consolefonts/Thai-Fixed18.psf.gz
/usr/share/consolefonts/Thai-Fixed15.psf.gz
/usr/share/consolefonts/Thai-Fixed14.psf.gz
/usr/share/consolefonts/Thai-Fixed16.psf.gz
/usr/share/consolefonts/Thai-Fixed13.psf.gz
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/rw-psf/test-conv$
```

တစ်ဖိုင်ကို ကော်ပီကူး ...  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/rw-psf/test-conv$ cp /usr/share/consolefonts/Thai-Fixed16.psf.gz .
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/rw-psf/test-conv$ gunzip ./Thai-Fixed16.psf.gz 
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/rw-psf/test-conv$ ls
psf-file-info.txt  readpsf  Thai-Fixed16.psf  writepsf  ye-x.16x32.bmp  ye-x.psfu  ye-x.psfu.txt
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/rw-psf/test-conv$ 
```

psf to bmp conversion လုပ်ကြည့် ...  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/rw-psf/test-conv$ perl ./readpsf ./Thai-Fixed16.psf bmp
Possible precedence issue with control flow operator at ./readpsf line 466.
Possible precedence issue with control flow operator at ./readpsf line 472.
Reading './Thai-Fixed16.psf'...
Version 1 PSF file.
Font has an unicode table. Use 'psfgettable' command to extract it.
PSF file suggests 256 glyphs of size 8 x 16.
256 glyphs found.

Creating an image.

'./Thai-Fixed16.8x16.bmp' written. All Ok.
```

check the converted bmp file:  

ထွက်လာတဲ့ output bmp ဖိုင်က အောက်ပါအတိုင်း ...  

![converted bmp file for Thai-Fixed16.psf](https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/psf2bmp/Thai-Fixed16.8x16.bmp "converted bmp file for Thai-Fixed16.psf")

## PSF to TXT Converion

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/code/console-font-dev/rw-psf/test-conv$ perl ./readpsf ./Thai-Fixed16.psf txt
Possible precedence issue with control flow operator at ./readpsf line 466.
Possible precedence issue with control flow operator at ./readpsf line 472.
Reading './Thai-Fixed16.psf'...
Version 1 PSF file.
Font has an unicode table. Use 'psfgettable' command to extract it.
PSF file suggests 256 glyphs of size 8 x 16.
256 glyphs found.

'./Thai-Fixed16.8x16.txt' written. All Ok.
```

## Font Metrics Information

Referene link: [https://gitlab.com/bztsrc/scalable-font/blob/master/docs/API.md](https://gitlab.com/bztsrc/scalable-font/blob/master/docs/API.md)  

```
   (0,0)................._______
        .................      ^
     ___.................      | bearing top
     ^  ,,,,,,,,,,,,,,,,,______v
     |  ....:.XXX.XX:....  ^ ^ ^
size |  ....:XX..XX.:....  | | |
     |  ....:XX..XX.:....  | | | horizontal baseline
     |  ....:XX..XX.:....  | | |
     |  ....:XX..XX.:....  | | |
     |  ....:XX..XX.:....  | | |
     v__,,,,;.XXXXX,;,,,,__|_|_v
        ....:....XX.:....  | |
        ....|XX..XX.:....  | | glyph height
        ....:.XXXX..:....__|_v
        ....:...:...:....  |
        ....:...:...:....  | advance y
        ....:...:...:....__v
        |   |   |   | |  (font width, font height)
        |   |   |   | |
        |   |<->|   | |  vertical baseline (center of the glyph, always width / 2)
        |   |<----->| |  glyph width
        |   |<------->|  advance x
        |   |<---->|     advance x with kerning x
        |<->|            bearing left
```

## Console Font Info

```
(base) ye@ykt-pro:~/tool/scalable-font/sfnconv$ whereis consolefonts
consolefonts: /usr/share/consolefonts
(base) ye@ykt-pro:~/tool/scalable-font/sfnconv$ 
```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

## Reference

- [Into the Mist: How Linux Console Fonts Work By En D Loozzr](https://linuxgazette.net/issue91/loozzr.html)
- [Fonts & Encodings by Yannis Haralambous](https://hal.science/hal-02112942/document)
- [Simple font rendering library](https://forum.osdev.org/viewtopic.php?t=33719&p=290150)
- [Scalable Font](https://gitlab.com/bztsrc/scalable-font)
- [Scalable Screen Font Ecosystem](https://gitlab.com/bztsrc/scalable-font/blob/master/docs/ecosystem.md)
- [Problem in ttf2sfn.c compilation](https://gitlab.com/bztsrc/scalable-font/-/issues/1)
- [PC Screen Font](https://wiki.osdev.org/PC_Screen_Font)
- [Simon Tatham's Fonts Page](https://www.chiark.greenend.org.uk/~sgtatham/fonts/)
- [monobit: Tools for working with monochrome bitmap fonts.](https://pypi.org/project/monobit/0.30.0/)
