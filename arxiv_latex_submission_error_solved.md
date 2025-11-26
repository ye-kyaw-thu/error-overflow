# Notes on arXiv Submission Error Fixing

I submitted latex source code that used Burmese font named Padauk and compiled with XeLatex.  

## Reply from arXiv Technical Support

```
Dear arXiv User,

your submission has two problems:

First, the font you are using with

\newfontfamily{\padauktext }[Script=Myanmar]{Padauk}
is not available. You have to provide the font. Please copy the file Padauk-Regular.ttf into the submission, and then use

\newfontfamily\padauktext[Script=Myanmar]{Padauk-Regular.ttf}
Second, your use
}} in the {{\author field which is not supported. Overleaf might compile it because Overleaf ignores errors, but arXiv does not ignore errors. You cannot use
}} in {{\author settings.

Best regards
```

## Actions

Added Padauk-Regular.ttf to latex source folder.  
You can get Padauk font from following link:  
[https://software.sil.org/padauk/](https://software.sil.org/padauk/)  

Updated followings:  

```
% Define new font family
%\newfontfamily{\padauktext }[Script=Myanmar]{Padauk}
\newfontfamily\padauktext[Script=Myanmar]{Padauk-Regular.ttf}
```

One more updating:  

```
%\author{
%{
%    Thura Aung$^{1,2}$,
%    Eaint Kay Khaing Kyaw$^{1,2}$,
%    Ye Kyaw Thu$^{1,3*}$,
%    Thazin Myint Oo$^{1}$,
%    Thepchai Supnithi$^{3*}$
%    \\[4pt]
%    \textit{$^{1}$Language Understanding Laboratory, Myanmar}\\
%    \textit{$^{2}$Department of Computer Engineering, KMITL, Bangkok, Thailand}\\
%    \textit{$^{3}$Language and Semantic Technology Research Team, NECTEC, Bangkok, Thailand}\\[3pt]
%    \normalsize
%    Emails:
%    \texttt{66011606@kmitl.ac.th},
%    \texttt{66011533@kmitl.ac.th},\\
%    \texttt{\{yekyaw.thu,thepchai.supnithi\}@nectec.or.th},
%    \texttt{queenofthazin@gmail.com}\\[2pt]
%    }
%    \thanks{$^{*}$Corresponding author.}
%    \vspace{-5mm}
%}
```

```
\author{
Thura Aung$^{1,2}$,
Eaint Kay Khaing Kyw$^{1,2}$,
Ye Kyaw Thu$^{1,3,\ast}$,
Thazin Myint Oo$^{1}$,
Thepchai Supnithi$^{3,\ast}$
\\
$^{1}$Language Understanding Laboratory, Myanmar
\\
$^{2}$Department of Computer Engineering, KMITL, Bangkok, Thailand  
\\
$^{3}$Language and Semantic Technology Research Team, NECTEC, Bangkok, Thailand
\\
\emph{Corresponding authors:} \texttt{yekyaw.thu@nectec.or.th}, \texttt{thepchai.supnithi@nectec.or.th}
\\
\emph{Emails:} \texttt{66011606@kmitl.ac.th}, \texttt{66011533@kmitl.ac.th}, \texttt{queenofthazin@gmail.com}
}
```



