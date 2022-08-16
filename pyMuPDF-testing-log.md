# Testing pyMuPDF Library

ရုံးက အလုပ်ကိစ္စတစ်ခုနဲ့ စာမျက်နှာ ၄၅ မျက်နှာ ရှိတဲ့ PDF ဖိုင်ရဲ့ စာမျက်နှာတိုင်းမှာ digital signing လုပ်ဖို့ လိုအပ်လာလို့ pyMuPDF library ကို သုံးပြီး လက်မှတ်ရဲ့ image ဖိုင်ကို PDF page တိုင်းမှာ ဝင် insert လုပ်တာကို စမ်းကြည့်ထားတဲ့ log ဖိုင်ပါ။  

## Installing pyMuPDF

```
(base) ye@ykt-pro:/media/ye/project2/NECTEC/contract-and-documents/new-contract-2022$ pip install --upgrade pymupdf
Collecting pymupdf
  Downloading https://files.pythonhosted.org/packages/4a/09/6afe87a8ea7acb6e4709223a704270ffe9929497add4d06b12305e229ba8/PyMuPDF-1.20.2.tar.gz (90.4MB)
     |████████████████████████████████| 90.4MB 141kB/s 
Building wheels for collected packages: pymupdf
  Building wheel for pymupdf (setup.py) ... done
  Created wheel for pymupdf: filename=PyMuPDF-1.20.2-cp37-cp37m-linux_x86_64.whl size=8807600 sha256=454b16cb9fc686aae703fbf7b94a1e11dfdd6b5e889e2c5317d14aae3235b88e
  Stored in directory: /home/ye/.cache/pip/wheels/70/da/1d/2b5e4079ae913fb21f3009a37064f84488f4611aa32e0f0617
Successfully built pymupdf
Installing collected packages: pymupdf
Successfully installed pymupdf-1.20.2
(base) ye@ykt-pro:/media/ye/project2/NECTEC/contract-and-documents/new-contract-2022$ 
```

Run ကြည့်တော့ အောက်ပါအတိုင်း error ပေးတယ်  

```
(base) ye@ykt-pro:/media/ye/project2/NECTEC/contract-and-documents/new-contract-2022$ python ./add-sign.py 
Traceback (most recent call last):
  File "./add-sign.py", line 17, in <module>
    first_page.insertImage(image_rectangle, fileName=barcode_file)
  File "/home/ye/tool/anaconda3/lib/python3.7/site-packages/fitz/fitz.py", line 5539, in <lambda>
    __getattr__ = lambda self, name: _swig_getattr(self, Page, name)
  File "/home/ye/tool/anaconda3/lib/python3.7/site-packages/fitz/fitz.py", line 84, in _swig_getattr
    raise AttributeError("'%s' object has no attribute '%s'" % (class_type.__name__, name))
AttributeError: 'Page' object has no attribute 'insertImage'
(base) ye@ykt-pro:/media/ye/project2/NECTEC/contract-and-documents/new-contract-2022$
```

Debugging ...  

```
(base) ye@ykt-pro:/media/ye/project2/NECTEC/contract-and-documents/new-contract-2022$ python
Python 3.7.4 (default, Aug 13 2019, 20:35:49) 
[GCC 7.3.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import fitz
>>> input_file = "NCR-NT-2022-17333-EN.pdf"
>>> output_file = "output.pdf"
>>> barcode_file = "sign.png"
>>> image_rectangle = fitz.Rect(450,20,550,120)
>>> file_handle = fitz.open(input_file)
>>> first_page = file_handle[0]
>>> dir(first_page)
['__class__', '__del__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattr__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__swig_destroy__', '__swig_getmethods__', '__swig_setmethods__', '__weakref__', '_addAnnot_FromString', '_addWidget', '_add_caret_annot', '_add_file_annot', '_add_freetext_annot', '_add_ink_annot', '_add_line_annot', '_add_multiline', '_add_redact_annot', '_add_square_or_circle', '_add_stamp_annot', '_add_text_annot', '_add_text_marker', '_annot_refs', '_apply_redactions', '_erase', '_forget_annot', '_get_optional_content', '_get_resource_properties', '_get_textpage', '_insertFont', '_insert_image', '_load_annot', '_makePixmap', '_other_box', '_reset_annot_refs', '_set_opacity', '_set_pagebox', '_set_resource_property', '_show_pdf_page', 'add_caret_annot', 'add_circle_annot', 'add_file_annot', 'add_freetext_annot', 'add_highlight_annot', 'add_ink_annot', 'add_line_annot', 'add_polygon_annot', 'add_polyline_annot', 'add_rect_annot', 'add_redact_annot', 'add_squiggly_annot', 'add_stamp_annot', 'add_strikeout_annot', 'add_text_annot', 'add_underline_annot', 'add_widget', 'annot_names', 'annot_xrefs', 'annots', 'apply_redactions', 'artbox', 'bleedbox', 'bound', 'clean_contents', 'cropbox', 'cropbox_position', 'delete_annot', 'delete_link', 'delete_widget', 'derotation_matrix', 'draw_bezier', 'draw_circle', 'draw_curve', 'draw_line', 'draw_oval', 'draw_polyline', 'draw_quad', 'draw_rect', 'draw_sector', 'draw_squiggle', 'draw_zigzag', 'extend_textpage', 'first_annot', 'first_link', 'first_widget', 'get_bboxlog', 'get_cdrawings', 'get_contents', 'get_displaylist', 'get_drawings', 'get_fonts', 'get_image_bbox', 'get_image_info', 'get_image_rects', 'get_images', 'get_label', 'get_links', 'get_oc_items', 'get_pixmap', 'get_svg_image', 'get_text', 'get_text_blocks', 'get_text_selection', 'get_text_words', 'get_textbox', 'get_textpage', 'get_textpage_ocr', 'get_texttrace', 'get_xobjects', 'insert_font', 'insert_image', 'insert_link', 'insert_text', 'insert_textbox', 'is_wrapped', 'language', 'links', 'load_annot', 'load_links', 'load_widget', 'mediabox', 'mediabox_size', 'new_shape', 'number', 'parent', 'read_contents', 'rect', 'refresh', 'rotation', 'rotation_matrix', 'run', 'search_for', 'set_artbox', 'set_bleedbox', 'set_contents', 'set_cropbox', 'set_language', 'set_mediabox', 'set_rotation', 'set_trimbox', 'show_pdf_page', 'this', 'transformation_matrix', 'trimbox', 'update_link', 'widgets', 'wrap_contents', 'write_text', 'xref']
>>> 
```

အထက်ပါအတိုင်း insert_image လို့ update လုပ်ထားတယ် ထင်လို့ အောက်ပါအတိုင်း ပြောင်းရေးခဲ့ ...  

```python
# add the image

#first_page.insertImage(image_rectangle, fileName=barcode_file)
first_page.insert_image(image_rectangle, fileName=barcode_file)
```

သို့သော် အောက်ပါလိုမျိုး error ပေးနေ  

```
>>> first_page.insert_image(image_rectangle, fileName=barcode_file)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/home/ye/tool/anaconda3/lib/python3.7/site-packages/fitz/utils.py", line 290, in insert_image
    raise ValueError("bad key argument(s) %s" % s)
ValueError: bad key argument(s) {'fileName'}
```

Ref: https://stackoverflow.com/questions/60711402/pymupdf-insert-image-at-bottom  

```
>>> img = open("sign.png", "rb").read()
>>> first_page.insert_image(image_rectangle, stream=img)
413
>>> file_handle.save(output_file)
```

အထက်ပါအတိုင်း ပြင်ရေးလိုက်တော့ error တော့ မပေးတော့ဘူး။   


## Splitting Page by Page

```
(base) ye@ykt-pro:/media/ye/project2/NECTEC/contract-and-documents/new-contract-2022/sign-work$ cat ./split-page-by-page.sh 
#!/bin/bash

for i in {1..45}
do
   pdftk ./NCR-NT-2022-17333-EN.pdf cat $i output $i.pdf
done
```

```
(base) ye@ykt-pro:/media/ye/project2/NECTEC/contract-and-documents/new-contract-2022/sign-work$ ./split-page-by-page.sh 

(base) ye@ykt-pro:/media/ye/project2/NECTEC/contract-and-documents/new-contract-2022/sign-work$ ls
10.pdf  14.pdf  18.pdf  21.pdf  25.pdf  29.pdf  32.pdf  36.pdf  3.pdf   43.pdf  5.pdf  9.pdf
11.pdf  15.pdf  19.pdf  22.pdf  26.pdf  2.pdf   33.pdf  37.pdf  40.pdf  44.pdf  6.pdf  NCR-NT-2022-17333-EN.pdf
12.pdf  16.pdf  1.pdf   23.pdf  27.pdf  30.pdf  34.pdf  38.pdf  41.pdf  45.pdf  7.pdf  split-page-by-page.sh
13.pdf  17.pdf  20.pdf  24.pdf  28.pdf  31.pdf  35.pdf  39.pdf  42.pdf  4.pdf   8.pdf
(base) ye@ykt-pro:/media/ye/project2/NECTEC/contract-and-documents/new-contract-2022/sign-work$ 
```

## Signing Digital Signature

တချို့ စာမျက်နှာတွေက scanner ဖတ်ထားတဲ့ အပေါ်ကို မူတည်ပြီးတော့ coordinate ကို ဖမ်းလို့ မရဘူး။  
ခွဲထားတဲ့ တစ်ဖိုင်ချင်းစီကို x, y coordinate ကို manual ညှိပြီး insert image လုပ်ခဲ့။  

```
(base) ye@ykt-pro:/media/ye/project2/NECTEC/contract-and-documents/new-contract-2022/sign-work$ evince ./42.sign.pdf 
(base) ye@ykt-pro:/media/ye/project2/NECTEC/contract-and-documents/new-contract-2022/sign-work$ python ./sign.py 43.pdf 43.sign.pdf
(base) ye@ykt-pro:/media/ye/project2/NECTEC/contract-and-documents/new-contract-2022/sign-work$ evince ./43.sign.pdf 
(base) ye@ykt-pro:/media/ye/project2/NECTEC/contract-and-documents/new-contract-2022/sign-work$ python ./sign.py 44.pdf 44.sign.pdf
(base) ye@ykt-pro:/media/ye/project2/NECTEC/contract-and-documents/new-contract-2022/sign-work$ evince ./44.sign.pdf 
(base) ye@ykt-pro:/media/ye/project2/NECTEC/contract-and-documents/new-contract-2022/sign-work$ python ./sign.py 44.pdf 44.sign.pdf
```

## Combine

```
(base) ye@ykt-pro:/media/ye/project2/NECTEC/contract-and-documents/new-contract-2022/sign-work$ pdftk 1.sign.pdf 2.sign.pdf 3.sign.pdf 4.sign.pdf 5.sign.pdf 6.sign.pdf 7.sign.pdf 8.sign.pdf 9.sign.pdf 10.sign.pdf 11.sign.pdf 12.sign.pdf 13.sign.pdf 14.sign.pdf 15.sign.pdf 16.sign.pdf 17.sign.pdf 18.sign.pdf 19.sign.pdf 20.sign.pdf 21.sign.pdf 22.sign.pdf 23.sign.pdf 24.sign.pdf 25.sign.pdf 26.sign.pdf 27.sign.pdf 28.sign.pdf 29.sign.pdf 30.sign.pdf 31.sign.pdf 32.sign.pdf 33.sign.pdf 34.sign.pdf 35.sign.pdf 36.sign.pdf 37.sign.pdf 38.sign.pdf 39.sign.pdf 40.sign.pdf 41.sign.pdf 42.sign.pdf 43.sign.pdf 44.sign.pdf 45.sign.pdf cat output final.pdf
```

## Python Code FYI

ဒီဖိုင်နဲ့က PDF ဖိုင်ရဲ့ page အားလုံးကို looping ပတ်ပြီး insert-image လုပ်ကြည့်တာ။  
သို့သော် လက်တွေ့မှာက အဆင်မပြေခဲ့ဘူး။ ဘာကြောင့်လဲ ဆိုတေါ့ တချို့ စာမျက်နှာတွေက scan ဖတ်ထားတဲ့ direction က မတူတာနဲ့ function အနေနဲ့က x, y coordinate တွေကို တွက်တဲ့အခါမှာ လွဲကုန်တာ။ ကိုယ်လိုချင်တဲ့ နေရာကို ချဖို့ ခက်တယ်။ နောက်တစ်ချက်က တချို့ စာမျက်နှာမှာ sign ထိုးရတာက ညာဘက်ထောင့် အောက်ဆုံး အပိုင်း မဟုတ်ပဲနဲ့ သတ်မှတာထားတဲ့ နေရာ (နာမည်ရေးပေးထားတဲ့ နေရာမျိုး) မှာ sign image ကို ဝင် insert လုပ်ရတာမို့လို့။  
တကယ်လို့ sing ထိုးရတာက PDF ဖိုင်ရဲ့ စာမျက်နှာ အားလုံးရဲ့ တနေရာထဲဆိုရင်တော့ အောက်ပါ code က အသုံးဝင်ပါလိမ့်မယ်။  

filename: add-sign.py  

```python
# !/usr/bin/python

import fitz

#input_file = "NCR-NT-2022-17333-EN.pdf"
pdf = fitz.open("NCR-NT-2022-17333-EN.pdf")
output_file = "output.pdf"
img = open("sign.png", "rb").read()
#barcode_file = "sign.png"

# define the position (upper-right corner)
#image_rectangle = fitz.Rect(450,20,550,120)
# define lower-rightcorner
image_rectangle = fitz.Rect(450,700,650,800)

# retrieve the first page of the PDF
#file_handle = fitz.open(input_file)

for i in range(0, pdf.page_count):
   page_no = pdf[i]
   page_no.insert_image(image_rectangle, stream=img)


# add the image
#first_page.insertImage(image_rectangle, fileName=barcode_file)
#first_page.insert_image(image_rectangle, stream=img)

pdf.save(output_file)
```

filename: add-sign-onepage.py  

```python
# !/usr/bin/python

# signing for page no. 2
# usage: python ./add-sign-onepage.py 1

import sys
import fitz

pdf = fitz.open("NCR-NT-2022-17333-EN.pdf")
output_file = "output.pdf"
img = open("sign.png", "rb").read()

# define the position (upper-right corner)
#image_rectangle = fitz.Rect(450,20,550,120)
# define lower-rightcorner
image_rectangle = fitz.Rect(450,700,650,800)

target_page = int(sys.argv[1])
page_no = pdf[target_page]
page_no.insert_image(image_rectangle, stream=img)

pdf.save(output_file)
```

လက်တွေ့မှာ အပင်ပန်းခံပြီး စာမျက်နှာ တစ်ခုချင်းစီ ခွဲထားတဲ့ 1-page PDF ဖိုင်တွေကို x, y coordinate တွေညှိပြီး sign-image ကို ဝင်ထည့်ခဲ့ပါတယ်။  

filename: sign.py  

```python
# !/usr/bin/python

# usage: python ./sign.py 1.pdf 1.sign.pdf

import sys
import fitz

pdf = fitz.open(sys.argv[1])
output_file = sys.argv[2]
img = open("sign.png", "rb").read()

# define the position (upper-right corner)
#image_rectangle = fitz.Rect(450,20,550,120)
# define lower-rightcorner
#image_rectangle = fitz.Rect(420,750,620,850)

# for page no. 2
#image_rectangle = fitz.Rect(380,280,580,380)

# for page no. 9
#image_rectangle = fitz.Rect(450,700,650,800)

# for page no. 10, 29
image_rectangle = fitz.Rect(420,700,620,800)

# for page no. 34, 35, 36, 37
#image_rectangle = fitz.Rect(20,700,220,800)

#image_rectangle = fitz.Rect(120,700,320,800)

# for page no. 14, 15, 16
#image_rectangle = fitz.Rect(420,735,620,835)

# for page no. 39, 40, 44
#image_rectangle = fitz.Rect(30,500,230,600)

# for page no. 41, 42, 43
#image_rectangle = fitz.Rect(420,700,620,800)

page_no = pdf[0]
page_no.insert_image(image_rectangle, stream=img)

pdf.save(output_file)

```

## Reference

[1] https://github.com/pymupdf/PyMuPDF  
[2] https://stackoverflow.com/questions/60711402/pymupdf-insert-image-at-bottom  
