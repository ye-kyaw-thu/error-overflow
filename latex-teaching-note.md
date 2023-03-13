(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/latex/13mar$ ls
doc1.tex
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/latex/13mar$ cat doc1.tex 
\documentclass{article}
\begin{document}
This is our 1st Latex document.
\end{document}
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/latex/13mar$ pdflatex ./doc1.tex 
This is pdfTeX, Version 3.14159265-2.6-1.40.18 (TeX Live 2017/Debian) (preloaded format=pdflatex)
 restricted \write18 enabled.
entering extended mode
(./doc1.tex
LaTeX2e <2017-04-15>
Babel <3.18> and hyphenation patterns for 84 language(s) loaded.
(/usr/share/texlive/texmf-dist/tex/latex/base/article.cls
Document Class: article 2014/09/29 v1.4h Standard LaTeX document class
(/usr/share/texlive/texmf-dist/tex/latex/base/size10.clo))
No file doc1.aux.
[1{/var/lib/texmf/fonts/map/pdftex/updmap/pdftex.map}] (./doc1.aux) )</usr/shar
e/texlive/texmf-dist/fonts/type1/public/amsfonts/cm/cmr10.pfb>
Output written on doc1.pdf (1 page, 13789 bytes).
Transcript written on doc1.log.
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/latex/13mar$ ls
doc1.aux  doc1.log  doc1.pdf  doc1.tex
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/latex/13mar$ 

## Converting images into PDF file

(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/latex/13mar/fig$ ls
universe.jpg
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/latex/13mar/fig$ convert ./universe.jpg ./universe.pdf
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/latex/13mar/fig$ ls
universe.jpg  universe.pdf

## Embedding pdf file inside your latex source 

\documentclass{article}
\usepackage{graphicx}% LaTeX package to import graphics
\graphicspath{{images/}} % configuring the graphicx package
 
\begin{document}
The universe is immense and it seems to be homogeneous, 
on a large scale, everywhere we look.

% The \includegraphcs command is 
% provided (implemented) by the 
% graphicx package
\includegraphics{./fig/universe.pdf}  
 \documentclass{article}
\usepackage{graphicx}
\graphicspath{{images/}}
 
There's a picture of a galaxy above.
\end{document}

## Adding One more figure and usage of \ref{}

\begin{document}

Now I will add one more figure.  \\

\begin{figure}[h]
    \centering
    \includegraphics[width=0.75\textwidth]{./fig/universe.jpg}
    \caption{beautiful universe}
    \label{fig:universe}
\end{figure}

Calling figure label here: See Fig\ref{fig:universe} and give comment to me. Beautiful right? \\

\begin{figure}[h]
    \centering
    \includegraphics[width=0.75\textwidth]{./fig/mesh.png}
    \caption{A nice plot.}
    \label{fig:mesh1}
\end{figure}
 
As you can see in figure \ref{fig:mesh1}, the function grows near the origin. This example is on page \pageref{fig:mesh1}.


\end{document}

**** if you manually compile, you need to compile 2 times. Don't forget it!


## How to Add Myanmar Font with Xelatex compiler

% You have to declare the fontspec package
%added by Ye
\usepackage{fontspec}

%for typing Myanmar text, you can also used with Myanmar3 font
\newfontfamily {\padauktext}[Script=Myanmar]{Padauk}
%\newfontinstance {\padauktext}[Script=Myanmar]{Padauk}

## How to find Khmer fonts 

(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/latex/paper1$ fc-list | grep "Khmer"
/usr/share/fonts/truetype/noto/NotoSansKhmer-Bold.ttf: Noto Sans Khmer:style=Bold
/usr/share/fonts/truetype/noto/NotoSerifKhmer-Regular.ttf: Noto Serif Khmer:style=Regular
/home/ye/.local/share/fonts/Khmer OS Siemreap.ttf: Khmer OS Siemreap:style=Regular
/usr/share/fonts/truetype/noto/NotoSansKhmerUI-Bold.ttf: Noto Sans Khmer UI:style=Bold
/usr/share/fonts/truetype/ttf-khmeros-core/KhmerOS.ttf: Khmer OS:style=Regular
/usr/share/fonts/truetype/ttf-khmeros-core/KhmerOSsys.ttf: Khmer OS System:style=Regular
/usr/share/fonts/truetype/noto/NotoSansKhmerUI-Regular.ttf: Noto Sans Khmer UI:style=Regular
/usr/share/fonts/truetype/noto/NotoSerifKhmer-Bold.ttf: Noto Serif Khmer:style=Bold
/usr/share/fonts/truetype/noto/NotoSansKhmer-Regular.ttf: Noto Sans Khmer:style=Regular
(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/latex/paper1$ 

## Math Equation Alignment Example


\documentclass[12pt, letterpaper]{article}
\usepackage{amsmath,amssymb,amsfonts}

\title{Demo of How to Write Math Formulae with Latex}
\author{Ye Kyaw Thu \thanks{Funded by ITC}}
\date{\today}

% I am now teaching latex usage to my students ... 
\begin{document}
\maketitle
Here some math formulae within a text paragraph: $\Hat{e}=argmax_e \mathbf {P}(e|f)$. \\

However, you want to type math formulae as a group or you need math equation auto number etc., we used equation tag as follows:  \\

\begin{equation} \label{eq:1}
\Hat{e}=argmax_e \mathbf {P}(e|f)
\end{equation}
Applying the Bayes’ rule, we can factorized into three parts.
\begin{equation} \label{eq:2}
P(e|f)=\frac{\mathbf{P}(e)}{\mathbf{P}(f)}\mathbf{P}(f|e)
\end{equation}
The final mathematical formulation of phrase-based model is  as follows:
\begin{equation} \label{eq:3}
argmax_e \mathbf {P}(e|f)=argmax_e \mathbf {P}(f|e) \mathbf{P}(e)
\end{equation}

Sometimes, we need to make alignment when we type more than one math formula as shown in here:  \\

\begin{align}
\Hat{e}&=argmax_e \mathbf {P}(e|f) \\
P(e|f)&=\frac{\mathbf{P}(e)}{\mathbf{P}(f)}\mathbf{P}(f|e) \\ 
argmax_e \mathbf {P}(e|f)&=argmax_e \mathbf {P}(f|e) \mathbf{P}(e) \\
\end{align}

\end{document}

## Some More Math Equation Example 


\documentclass[12pt, letterpaper]{article}
\usepackage{amsmath,amssymb,amsfonts}
\usepackage{bigints}

\title{Demo of How to Write Math Formulae with Latex}
\author{Ye Kyaw Thu \thanks{Funded by NECTEC}}
\date{\today}

% I am now teaching latex usage to my students ... 
\begin{document}
\maketitle

This is an example of how to add some math equations:  \\

\begin{equation}
\sum_{n=1}^{\infty} 2^{-n} = 1
\end{equation}

Here, I wanna show how \_ and \^~symbols works, for example: $2^{e}$, one more example: $X_{i}^{j}$, $E=mc^{2}$ \\

$\begin{pmatrix}
1 & 2 & 3 \\
a & b & c
\end{pmatrix}$

Let's try some more integral equations: \\

\begin{align}
 \int& f(x) dx  \\
 \int& \frac{\tan^{-1}x}{x(x^2+1)}dx \\
 \bigintssss& f(x)dx ,\bigintsss f'(x)dx ,\bigintss f''(x)dx,\bigints \frac{f(x)}{g(x)}dx,\bigint \frac{f'(x)}{g'(x)}dx
\end{align}

\end{document}

## Relating to Adding Reference

One Format:  

\begin{thebibliography}{00}

\bibitem{b1} Koehn, Philipp and Och, Franz Josef and Marcu, Daniel, ``Statistical phrase-based translation,'' Proceedings of the 2003 Conference of the North American Chapter of the Association for Computational Linguistics on Human Language Technology - Volume 1, 2003, pp. 48–54.
\bibitem{b2} Koehn, Philipp and Hoang, Hieu and Birch, Alexandra and Callison-Burch, Chris and Federico, Marcello and Bertoldi, Nicola and Cowan, Brooke and Shen, Wade and Moran, Christine and Zens, Richard and Dyer, Chris and Bojar, Ond\v{r}ej and Constantin, Alexandra and Herbst, Evan, A. Constantin, and E. Herbst, ``Moses: Open source toolkit for statistical machine translation,'' Proceedings of the 45th Annual Meeting of the ACL on Interactive Poster and Demonstration Sessions, 2007, pp. 177–180.

Another Format:  

You need to prepare bib file as follows:

(base) ye@ykt-pro:/media/ye/project1/cadt/student/internship/demo/latex/13mar/bib-demo2$ cat mybib.bib 
@misc{ Nobody06,
       author = "Nobody Jr",
       title = "My Article",
       year = "2006" }

@inproceedings{Thu2015HMMBM,
  title={HMM based myanmar text to speech system},
  author={Ye Kyaw Thu and Win Pa Pa and Jinfu Ni and Yoshinori Shiga and Andrew M. Finch and Chiori Hori and Hisashi Kawai and Eiichiro Sumita},
  booktitle={Interspeech},
  year={2015}
}


Then call inside from your latex source file:

\documentclass[11pt]{article}
\usepackage{cite}

\begin{document}

\title{My Article}
\author{Nobody Jr.}
\date{Today}
\maketitle

Blablabla said Nobody ~\cite{Nobody06}. HMM based Myanmar language TTS was prposed by~\cite{Thu2015HMMBM}. 

\bibliography{mybib}{}
\bibliographystyle{plain}
\end{document}

## Typing Unicode Asian Languages

% latex document မှာ မြန်မာစာ၊ ထိုင်း၊ ခမာ နဲ့ CJK စာတွေကို ပေါ်ဖို့ ဘယ်လို လုပ်ရသလဲ ဆိုတဲ့ example latex ပါ
% Ye Kyaw Thu @LST, NECTEC, Thailand
% Last Updated: 28 July 2022

\documentclass[12pt]{article}

\usepackage{fontspec}
\usepackage[utf8]{inputenc}
%\inputencoding{latin1}
\inputencoding{utf8}

% if you want to setup Khmer font as the main font
%\newcommand{\kh}{\setmainfont{Khmer OS}}

% setting the main font of this latex document
\setmainfont{Times New Roman}

% example usage of Courier New and Times New Roman
\newcommand{\courier}{\setmainfont{Courier New}\textbf}
\newcommand{\vsp}{\fontencoding{T3}\fontfamily{cmr}\selectfont\textvisiblespace\setmainfont{Times New Roman}}

%for writing Khmer text
% old approach
%\newfontinstance {\kh}[Script=Khmer]{Khmer OS Siemreap}
%\newfontinstance {\khs}[Script=Khmer,Scale=0.9]{Khmer OS Siemreap}

\newfontfamily {\kh}[Script=Khmer]{Khmer OS Siemreap}
\newfontfamily {\khs}[Script=Khmer,Scale=0.9]{Khmer OS Siemreap}

% for writing Thai text
\newfontfamily {\thaitext}[Script=Thai]{Noto Sans Thai}

%for writing Myanmar text, you can also used with Myanmar3 font
\newfontfamily {\padauktext}[Script=Myanmar]{Padauk}
\newfontfamily {\myanmartext}[Script=Myanmar]{Myanmar3}
%\newfontfamily {\zawgyionetext}[Script=Myanmar]{Zawgyi-One}
%\newfontinstance {\padauktext}[Script=Myanmar]{Padauk}
\newfontfamily {\pdstext}[Script=Myanmar]{Pyidaungsu}

% for Chinese Japanese and Korean
\usepackage{xeCJK}
\setCJKmainfont{UnGungseo.ttf}
\setCJKsansfont{UnGungseo.ttf}
\setCJKmonofont{gulim.ttf}

\usepackage{CJKutf8}

\newcommand{\quotes}[1]{``#1''}

\begin{document}

\section*{Khmer Font Using Example}

For example: //

{\kh - \small{ខ្ញុំ ចង់ឱ្យ \textlangle{} អ្នកស្តាប់ \textrangle{} យល់ ពី បញ្ហា នេះ}}

- I want listener to understand this problem\\

{\kh - \small{ខ្ញុំ ចង់ឱ្យ \textlangle{} អ្នក \textrangle{} \textlangle{} ស្តាប់ \textrangle{} យល់ ពី បញ្ហា នេះ}}

- I want you to listen in order to understand this problem\\

\section*{Thai Font Using Example}

{\thaitext ประเทศไทยคือบ้านหลังที่สามของฉัน}

\section*{Myanmar Font Using Example}

{\padauktext ဗမာစာ၊ ဗမာစကား ကို} \quotes{{\padauktext ပိတောက်ဖောင့်}} {\padauktext ဖြင့် ရိုက်ကြည့်ခြင်း}\\
{\myanmartext ဗမာစာ၊ ဗမာစကား ကို} \quotes{{\padauktext Myanmar3ဖောင့်}}  {\padauktext နဲ့ ရိုက်ကြည့်ခြင်း}\\
{\pdstext ဗမာစာ၊ ဗမာစကား ကို} \quotes{{\padauktext ပြည်ထောင်စုဖောင့်}} {\padauktext ဖြင့် ရိုက်ကြည့်ခြင်း}\\

\section*{Typing Chinese, Japanese and Korean}

我去过北京。\\
京都に行ったことがあります。\\
서울에 다녀왔습니다. \\

\end{document}


