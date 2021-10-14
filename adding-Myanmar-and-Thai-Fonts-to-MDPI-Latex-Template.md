# Adding Myanmar and Thai Fonts to MDIP Journal Template

ကျောင်းသူ တစ်ယောက်က ဂျာနယ်တစ်စောင်ရေးဖို့ ပြင်ဆင်တဲ့အခါမှာ သူတင်ချင်တဲ့ ဂျာနယ်ရဲ့ latex template မှာ မြန်မာစာ နဲ့ ထိုင်းစာ ဖောင့်တွေက ထည့်လို့မရဘူး။ အဲဒီ ဂျာနယ်ရဲ့ template က pdftex ကို သုံးထားတယ်၊ ဘယ်လိုလုပ်ရမလဲ ဆရာဆိုတဲ့ မေးခွန်းက တက်လာလို့ ကိုယ်တိုင် ဖြေရှင်းပေးခဲ့တဲ့ log file ပါ။  
နောက်ပိုင်း ကျောင်းသားတွေအတွက် reference အဖြစ် အသုံးဝင်ပါလိမ့်မယ်။  

y  
14 Oct 2021  

## Compile with Xelatex

xelatex နဲ့ compile လုပ်လို့ ရသလား ပထမဆုံး MDPI Journal template tex ဖိုင်ကို စမ်းကြည့်ခဲ့တော့ color နဲ့ ပတ်သက်ပြီး error ပေးတာကို တွေ့ရတယ်။  
နောက်ဆက်တွဲ error တွေကိုလည်း ENTER ခေါက်ပြီး ကျော်ပြီးသွားကြည့်ပေမဲ့ ရှင်းရမှာတွေ တော်တော်များများရှိသလို တွေ့ရတယ်။  

```
(base) ye@:/media/ye/project1/paper/zzh-journal/11Oct2021/1_MDPI_template-xelatex$ xelatex ./mdpi-fnmt-2021.tex 
This is XeTeX, Version 3.14159265-2.6-0.999992 (TeX Live 2020/Debian) (preloaded format=xelatex)
 restricted \write18 enabled.
entering extended mode
(./mdpi-fnmt-2021.tex
LaTeX2e <2020-02-02> patch level 5
L3 programming layer <2020-07-17> (./Definitions/mdpi.cls
Document Class: Definitions/mdpi 26/08/2021 MDPI paper class
(/usr/share/texlive/texmf-dist/tex/latex/base/article.cls
Document Class: article 2019/12/20 v1.4l Standard LaTeX document class
(/usr/share/texlive/texmf-dist/tex/latex/base/size10.clo))
(/usr/share/texlive/texmf-dist/tex/latex/base/fontenc.sty
(/usr/share/texmf/tex/latex/lm/t1lmr.fd))
(/usr/share/texlive/texmf-dist/tex/latex/base/inputenc.sty

Package inputenc Warning: inputenc package ignored with utf8 based engines.

) (/usr/share/texlive/texmf-dist/tex/latex/tools/calc.sty)
(/usr/share/texlive/texmf-dist/tex/latex/tools/indentfirst.sty)
(/usr/share/texlive/texmf-dist/tex/latex/fancyhdr/fancyhdr.sty)
(/usr/share/texlive/texmf-dist/tex/latex/graphics/graphicx.sty
(/usr/share/texlive/texmf-dist/tex/latex/graphics/keyval.sty)
(/usr/share/texlive/texmf-dist/tex/latex/graphics/graphics.sty
(/usr/share/texlive/texmf-dist/tex/latex/graphics/trig.sty)
(/usr/share/texlive/texmf-dist/tex/latex/graphics-cfg/graphics.cfg)
(/usr/share/texlive/texmf-dist/tex/latex/graphics-def/pdftex.def)))
(/usr/share/texlive/texmf-dist/tex/latex/epstopdf-pkg/epstopdf.sty
(/usr/share/texlive/texmf-dist/tex/generic/infwarerr/infwarerr.sty)
(/usr/share/texlive/texmf-dist/tex/latex/grfext/grfext.sty
(/usr/share/texlive/texmf-dist/tex/generic/kvdefinekeys/kvdefinekeys.sty))
(/usr/share/texlive/texmf-dist/tex/latex/kvoptions/kvoptions.sty
(/usr/share/texlive/texmf-dist/tex/generic/ltxcmds/ltxcmds.sty)
(/usr/share/texlive/texmf-dist/tex/generic/kvsetkeys/kvsetkeys.sty))
(/usr/share/texlive/texmf-dist/tex/generic/pdftexcmds/pdftexcmds.sty
(/usr/share/texlive/texmf-dist/tex/generic/iftex/iftex.sty))
(/usr/share/texlive/texmf-dist/tex/latex/epstopdf-pkg/epstopdf-base.sty
(/usr/share/texlive/texmf-dist/tex/latex/latexconfig/epstopdf-sys.cfg)))
(/usr/share/texlive/texmf-dist/tex/latex/lastpage/lastpage.sty)
(/usr/share/texlive/texmf-dist/tex/latex/base/ifthen.sty)
(/usr/share/texlive/texmf-dist/tex/latex/lineno/lineno.sty)
(/usr/share/texlive/texmf-dist/tex/latex/float/float.sty)
(/usr/share/texlive/texmf-dist/tex/latex/amsmath/amsmath.sty
For additional information on amsmath, use the `?' option.
(/usr/share/texlive/texmf-dist/tex/latex/amsmath/amstext.sty
(/usr/share/texlive/texmf-dist/tex/latex/amsmath/amsgen.sty))
(/usr/share/texlive/texmf-dist/tex/latex/amsmath/amsbsy.sty)
(/usr/share/texlive/texmf-dist/tex/latex/amsmath/amsopn.sty))
(/usr/share/texlive/texmf-dist/tex/latex/amsfonts/amssymb.sty
(/usr/share/texlive/texmf-dist/tex/latex/amsfonts/amsfonts.sty))
(/usr/share/texlive/texmf-dist/tex/latex/setspace/setspace.sty)
(/usr/share/texlive/texmf-dist/tex/latex/enumitem/enumitem.sty)
(/usr/share/texlive/texmf-dist/tex/latex/psnfss/mathpazo.sty)
(/usr/share/texlive/texmf-dist/tex/latex/booktabs/booktabs.sty)
(/usr/share/texlive/texmf-dist/tex/latex/titlesec/titlesec.sty)
(/usr/share/texlive/texmf-dist/tex/latex/etoolbox/etoolbox.sty)
(/usr/share/texlive/texmf-dist/tex/latex/tabto-ltx/tabto.sty)
(/usr/share/texlive/texmf-dist/tex/latex/xcolor/xcolor.sty
(/usr/share/texlive/texmf-dist/tex/latex/graphics-cfg/color.cfg)
! Undefined control sequence.
\set@color ->\pdfcolorstack 
                            \@pdfcolorstack push{\current@color }\aftergroup...
l.1457 \color{black}
                    
?  

! LaTeX Error: Missing \begin{document}.

See the LaTeX manual or LaTeX Companion for explanation.
Type  H <return>  for immediate help.
 ...                                              
                                                  
l.1457 \color{black}
                    
? 
) (/usr/share/texlive/texmf-dist/tex/latex/colortbl/colortbl.sty
(/usr/share/texlive/texmf-dist/tex/latex/tools/array.sty))
(/usr/share/texlive/texmf-dist/tex/latex/soul/soul.sty)
(/usr/share/texlive/texmf-dist/tex/latex/multirow/multirow.sty)
(/usr/share/texlive/texmf-dist/tex/latex/microtype/microtype.sty
(/usr/share/texlive/texmf-dist/tex/latex/microtype/microtype-xetex.def)
(/usr/share/texlive/texmf-dist/tex/latex/microtype/microtype.cfg))
(/usr/share/texlive/texmf-dist/tex/latex/pgf/frontendlayer/tikz.sty
(/usr/share/texlive/texmf-dist/tex/latex/pgf/basiclayer/pgf.sty
(/usr/share/texlive/texmf-dist/tex/latex/pgf/utilities/pgfrcs.sty
(/usr/share/texlive/texmf-dist/tex/generic/pgf/utilities/pgfutil-common.tex
(/usr/share/texlive/texmf-dist/tex/generic/pgf/utilities/pgfutil-common-lists.t
ex)) (/usr/share/texlive/texmf-dist/tex/generic/pgf/utilities/pgfutil-latex.def
(/usr/share/texlive/texmf-dist/tex/latex/ms/everyshi.sty))
(/usr/share/texlive/texmf-dist/tex/generic/pgf/utilities/pgfrcs.code.tex
(/usr/share/texlive/texmf-dist/tex/generic/pgf/pgf.revision.tex)))
(/usr/share/texlive/texmf-dist/tex/latex/pgf/basiclayer/pgfcore.sty
(/usr/share/texlive/texmf-dist/tex/latex/pgf/systemlayer/pgfsys.sty
(/usr/share/texlive/texmf-dist/tex/generic/pgf/systemlayer/pgfsys.code.tex
(/usr/share/texlive/texmf-dist/tex/generic/pgf/utilities/pgfkeys.code.tex
(/usr/share/texlive/texmf-dist/tex/generic/pgf/utilities/pgfkeysfiltered.code.t
ex)) (/usr/share/texlive/texmf-dist/tex/generic/pgf/systemlayer/pgf.cfg)
(/usr/share/texlive/texmf-dist/tex/generic/pgf/systemlayer/pgfsys-pdftex.def
(/usr/share/texlive/texmf-dist/tex/generic/pgf/systemlayer/pgfsys-common-pdf.de
f)
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ->\pdfobj 
                                           reserveobjnum \edef \pgf@sys@pdf@...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 

! LaTeX Error: Missing \begin{document}.

See the LaTeX manual or LaTeX Companion for explanation.
Type  H <return>  for immediate help.
 ...                                              
                                                  
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...e \pdflastobj 
                                                  } \pdfobj reserveobjnum \e...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! You can't use `end-group character }' after \the.
\pgf@sys@setuppdfresources@plain ... \pdflastobj }
                                                   \pdfobj reserveobjnum \ed...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...obj } \pdfobj 
                                                  reserveobjnum \edef \pgf@s...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...attern@objnum 
                                                  {\the \pdflastobj } \pdfob...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...e \pdflastobj 
                                                  } \pdfobj reserveobjnum \e...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! You can't use `end-group character }' after \the.
\pgf@sys@setuppdfresources@plain ... \pdflastobj }
                                                   \pdfobj reserveobjnum \ed...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...obj } \pdfobj 
                                                  reserveobjnum \edef \pgf@s...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...spaces@objnum 
                                                  {\the \pdflastobj } \def \...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...e \pdflastobj 
                                                  } \def \pgf@sys@pdf@possib...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! You can't use `end-group character }' after \the.
\pgf@sys@setuppdfresources@plain ... \pdflastobj }
                                                   \def \pgf@sys@pdf@possibl...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...ble@resources 
                                                  {/ColorSpace \pgf@sys@pdf@...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...spaces@objnum 
                                                  \space 0 R /Pattern \pgf@s...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...attern@objnum 
                                                  \space 0 R /ExtGState \pgf...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...@extgs@objnum 
                                                  \space 0 R } \let \pgf@sys...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...eck@resources 
                                                  =\relax \def \pgf@sys@pdf@...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...pageresources 
                                                  { { \edef \temp { \pgf@sys...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...{ \edef \temp 
                                                  { \pgf@sys@pdf@possible@re...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...ble@resources 
                                                  } \expandafter \global \ex...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...dafter {\temp 
                                                  } } } \pgf@sys@pdf@install...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
<recently read> \pdfpageresources 
                                  
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...pageresources 
                                                  \expandafter \pgfutil@ever...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...diate \pdfobj 
                                                  useobjnum \pgf@sys@pdf@ext...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...@extgs@objnum 
                                                  {<<\pgf@sys@pgf@resource@l...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...ce@list@extgs 
                                                  >>}\immediate \pdfobj useo...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...diate \pdfobj 
                                                  useobjnum \pgf@sys@pdf@pat...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...attern@objnum 
                                                  {<<\pgf@sys@pgf@resource@l...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...list@patterns 
                                                  >>}\immediate \pdfobj useo...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...diate \pdfobj 
                                                  useobjnum \pgf@sys@pdf@col...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...spaces@objnum 
                                                  {<<\pgf@sys@pgf@resource@l...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...t@colorspaces 
                                                  >>}} \let \pgf@sys@pgf@res...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...ce@list@extgs 
                                                  =\pgfutil@empty \let \pgf@...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...list@patterns 
                                                  =\pgfutil@empty \let \pgf@...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...t@colorspaces 
                                                  =\pgfutil@empty \def \pgf@...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...e@extgs@plain 
                                                  ##1{\xdef \pgf@sys@pgf@res...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Illegal parameter number in definition of \pgf@sys@pdf@extgs@objnum.
<to be read again> 
                   1
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...ce@list@extgs 
                                                  {\pgf@sys@pgf@resource@lis...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...ce@list@extgs 
                                                  \space ##1}} \def \pgf@sys...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Illegal parameter number in definition of \pgf@sys@pdf@extgs@objnum.
<to be read again> 
                   1
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...atterns@plain 
                                                  ##1{\xdef \pgf@sys@pgf@res...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Illegal parameter number in definition of \pgf@sys@pdf@extgs@objnum.
<to be read again> 
                   1
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...list@patterns 
                                                  {\pgf@sys@pgf@resource@lis...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...list@patterns 
                                                  \space ##1}} \def \pgf@sys...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Illegal parameter number in definition of \pgf@sys@pdf@extgs@objnum.
<to be read again> 
                   1
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...rspaces@plain 
                                                  ##1{\xdef \pgf@sys@pgf@res...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Illegal parameter number in definition of \pgf@sys@pdf@extgs@objnum.
<to be read again> 
                   1
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...t@colorspaces 
                                                  {\pgf@sys@pgf@resource@lis...
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgf@sys@setuppdfresources@plain ...t@colorspaces 
                                                  \space ##1}} 
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Illegal parameter number in definition of \pgf@sys@pdf@extgs@objnum.
<to be read again> 
                   1
l.385 \pgfutil@setuppdfresources
                                 % possibly call the above
? 
! Undefined control sequence.
\pgfutil@addpdfresource@colorspaces ...aces@plain 
                                                  {#1}
l.387 ...rspaces{ /pgfprgb [/Pattern /DeviceRGB] }
                                                  
? 
! Undefined control sequence.
l.390     \pdfliteral
                     {\csname\string\color@#1\endcsname}%
? x
No pages of output.
Transcript written on mdpi-fnmt-2021.log.
(base) ye@:/media/ye/project1/paper/zzh-journal/11Oct2021/1_MDPI_template-xelatex$
```

## Changed Defined Latex Engine of MDPI Journal Template

သို့သော် MDPI Journal template tex ဖိုင်ကို ဝင်ဖတ်ကြည့်တော့ သူက documentclass ရဲ့ parameter အနေနဲ့ latex engine ကို passing လုပ်လို့ ရတာကို တွေ့ရတယ်။ အဲဒါနဲ့ အဲဒီ original parameter ဖြစ်တဲ့ pdftex ကို မသုံးပဲ အဲဒီနေရာမှာ xelatex ကို pass လုပ်ခဲ့တယ်။  
အောက်ပါအတိုင်း...  

```
%=================================================================
%\documentclass[journal,article,submit,moreauthors,pdftex]{Definitions/mdpi} 
\documentclass[journal,article,submit,moreauthors,xelatex]{Definitions/mdpi} 
% For posting an early version of this manuscript as a preprint, you may use "preprints" as the journal and change "submit" to "accept". The document class line would be, e.g., \documentclass[preprints,article,accept,moreauthors,pdftex]{mdpi}. This is especially recommended for submission to arXiv, where line numbers should be removed before posting. For preprints.org, the editorial staff will make this change immediately prior to posting.
```

အဲဒီလို လုပ်ပြီး xelatex နဲ့ compile လုပ်ကြည့်ခဲ့တော့ အဆင်ပြေပြေနဲ့ (i.e. no error message) compile လုပ်ပေးပြီးတော့ output ဖြစ်တဲ့ PDF ဖိုင်ကိုလည်း ထုတ်ပေးနိုင်တာ တွေ့ရတယ်။ ထွက်လာတဲ့ PDF ဖိုင်ကိုလည်း ဖွင့်ကြည့်တော့ အဆင်ပြေတယ်။ ထူးထူးခြားခြား ပြောင်းလဲမှုကိုတော့ မတွေ့ရဘူး။  

အဲဒါနဲ့  လုပ်နေကြအတိုင်း xelatex မှာ မြန်မာဖောင့်ကို သုံးဖို့ ကြိုးစားကြည့်ခဲ့တယ်...  

## Check Installed Myanmar Fonts

ကျောင်းသူက ဘယ်မြန်မာစာ font ကို သုံးချင်တာမှန်းမသိတော့ ကိုယ့်စက်ထဲမှာ install လုပ်ထားတဲ့ မြန်မာစာဖောင့် တွေကို ရှာကြည့်ခဲ့တယ်။  
အောက်ပါအတိုင်း Myanamr3, Padauk နဲ့ Pyidaungsu ဖောင့်တွေက ရှိနေတာကို confirm လုပ်ခဲ့တယ်။  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/find-installed-Myanmar-fonts.png" alt="find installed Myanmar fonts" width="1400"/>  
</p>  
<div align="center">
  Fig.1 grep output for "Myanmar" or "Padauk" and "Pyidaungsu" 
</div> 

<br />

တကယ်လို့ ကိုယ့်စက်ထဲမှာ install လုပ်ထားတဲ့ ttf font တွေကိုပဲရှာမယ်ဆိုရင်တော့ locate ဆိုတဲ့ command ကိုလည်း သုံးလို့ ရပါတယ်။  
ဥပမာ။ ။  

```
$locate --regexp "\\.ttf$"
```

## Preparing for Using Fontspec Package

"fontspec" package ကို သုံးဖို့အတွက် အောက်ပါအတိုင်း \usepackage နဲ့ package ကို assign လုပ်ခဲ့ပြီး...  
\newfontfamily ဆိုတဲ့ tag နဲ့ မြန်မာစာဖောင့် တစ်ခုချင်းစီအတွက် tag အသစ်တွေကို သတ်မှတ်ခဲ့တယ်။  

```
%added by Ye
\usepackage{fontspec}
%for typing Myanmar text, you can also used with Myanmar3 font
\newfontfamily {\padauktext}[Script=Myanmar]{Padauk}
\newfontfamily {\myanmartext}[Script=Myanmar]{Myanmar3}
\newfontfamily {\pyidaungsutext}[Script=Myanmar]{Pyidaungsu}
```

title ကို အသစ် သတ်မှတ်ထားခဲ့တဲ့ \pyidaungsutext ဆိုတဲ့ tag ကို သုံးပြီးတော့ မြန်မာလိုခေါင်းစဉ် တစ်ခု စမ်းပေးကြည့်ခဲ့တယ်။  

```
% Full title of the paper (Capitalized)
\Title{Title: {\pyidaungsutext မြန်မာလို ခေါင်းစဉ်တပ်ကြည့်ခြင်း}}
```

ပြီးတော့... abstract နေရာမှာ Myanmar3 ဖောင့်နဲ့ ပိတောက်ဖောင့် နှစ်မျိုးကို စမ်းသုံးကြည့်ခဲ့တယ်။  

```% Abstract (Do not insert blank lines, i.e. \\) 
\abstract{Myanmar3 font testing: {\myanmartext မြန်မာ၃ ဖောင့် နဲ့ ရေးထားတဲ့ စာကြောင်း} 
Padauk font testing: {\padauktext ပိတောက် ဖောင့် နဲ့ ရေးထားတဲ့ စာကြောင်း} 
Linguistic features such as part-of-speech (POS) tags
```

xelatex နဲ့ compile လုပ်ကြည့်ပြီး ထွက်လာတဲ့ PDF ဖိုင်မှာ မြန်မာစာ စာကြောင်းတွေက font မှန်ကန်စွာနဲ့ typing order ကိုလည်း မှန်မှန်ကန်ကန် ရိုက်ထုတ်ပေးနိုင်ကြောင်းကို အောက်ပါအတိုင်း တွေ့ရတယ်။  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myanmar-fonts-testing.png" alt="compiled-pdf-with-Myanmar-fonts" width="1000"/>  
</p>  
<div align="center">
  Fig.2 Compiled PDF file after adding Myanmar fonts: "Myanmar3", "Padauk" and "PyiDaungSu" fonts 
</div> 

<br />


## Trying for Thai Font

လက်ရှိသုံးနေတဲ့ စက်ထဲမှာ ရှိတဲ့ ထိုင်းဖောင့်ကို ရှာကြည့်တော့ အောက်ပါအတိုင်း တွေ့ရ...  
(အခုလို ရှာတာက ဖောင့်နာမည်မှာ "Thai" ဆိုတဲ့ စာလုံးပါတဲ့ filename တွေကိုပဲ ရှာကြည့်တာပါ။)  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/find-installed-Thai-fonts.png" alt="find installed Thai fonts" width="1200"/>  
</p>  
<div align="center">
  Fig.3 grep output for "Thai" 
</div> 

<br />

စောစောက ရေးထားတဲ့ abstract ကို အောက်ပါအတိုင်း ထိုင်းဖောင့်ကို စမ်းထားတဲ့ စာကြောင်းပါ ဖြည့်ခဲ့တယ်။  

```
% Abstract (Do not insert blank lines, i.e. \\) 
\abstract{Myanmar3 font testing: {\myanmartext မြန်မာ၃ ဖောင့် နဲ့ ရေးထားတဲ့ စာကြောင်း} 
Padauk font testing: {\padauktext ပိတောက် ဖောင့် နဲ့ ရေးထားတဲ့ စာကြောင်း} 
Thai font testing: {\thaitext ดีใจที่ได้พบคุณ ฉันเป็นคนพม่า} Linguistic features such as part-of-speech (POS) tags 
have been widely used in
```

xelatex နဲ့ compile လုပ်ခဲ့တယ်။  

```
$ xelatex ./mdpi-fnmt-2021.tex
```

ထွက်လာတဲ့ output မှာ ထိုင်းဖောင့်လည်း ပေါ်ပါတယ်။ အောက်ပါ ပုံမှာမြင်ရတဲ့အတိုင်းပါ...   

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/myanmar-and-thai-fonts-testing.png" alt="compiled PDF with Thai fonts" width="1200"/>  
</p>  
<div align="center">
  Fig.4 Compiled PDF file output with Thai font 
</div> 

<br />

## Testing Myanmar Font Adding With Overleaf Online Latex Editor

ကျောင်းသား တချို့က online latex editor ဖြစ်တဲ့ OverLeaf ကိုလည်း သုံးကြတာမို့ အဲဒီ editor မှာလည်း xelatex engine ကိုရွေးပြီး compile လုပ်ခိုင်းလို့ ရတာမို့လို့ Myanmar3 ဖောင့်ဖိုင်ကို Definitions/ ဆိုတဲ့ ဖိုလ်ဒါအောက်ကို upload လုပ်လိုက်ပြီး၊ tex ဖိုင်မှာလည်း ```\usepackage{fontspec}``` ဆိုတဲ့ စာကြောင်းဝင်ဖြည့်တာ ```\newfontfamily {\myanmartext}[Script=Myanmar]{Myanmar3}``` စတဲ့ tag အသစ်ဆောက်တာတွေလုပ်ခဲ့ပြီး Title နေရာမှာ မြန်မာစာနဲ့ရေးထားတဲ့ ခေါင်းစဉ်ကို ဝင်ထည့်ပြီး compile လုပ်ကြည့်တော့ error တော့ မပေးပဲ compile လုပ်သွားတယ်။ သို့သော် အောက်ပါ ပုံမှာမြင်ရတဲ့အတိုင်း Title: ရဲ့ နောက်မှာ မြန်မာစာစာကြောင်းက ပေါ်မလာတဲ့ PDF ဖိုင်ကိုပဲ ထုတ်ပေးတာကို တွေ့ရတယ်။  


<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/adding-Myanmar-font-testing-with-Overleaf.png" alt="Testing-with-Overleaf-editor" width="1200"/>  
</p>  
<div align="center">
  Fig.4 Compiled output with online latex editor named "OverLeaf" 
</div> 

<br />

- လုပ်လို့ ရနိုင်တာက pdftex က နားလည်တဲ့ metafont အဖြစ်ပြောင်းပြီး compile လုပ်ကြည့်တာမျိုး...  
- သို့သော် မြန်မာစာ font တွေကို metafont ပြောင်းဖို့က လက်တော့ဝင်မယ်လို့ ထင်တယ်။ map ဖိုင်တွေက သေသေချာချာ ထွက်မထွက် မပြောနိုင်...  

## To Do

- အချိန်ရတဲ့အခါမှာ pdflatex က သုံးတဲ့ metafont အဖြစ်ပြောင်းထားတဲ့ ဖိုင်တွေနဲ့ Overleaf မှာ စမ်းကြည့်ရန်

## References

- https://www.overleaf.com/learn/latex/Questions/I_have_a_custom_font_I%27d_like_to_load_to_my_document._How_can_I_do_this%3F
- https://www.overleaf.com/project/6167c2cff78b6d07ac052ec3

