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

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```
