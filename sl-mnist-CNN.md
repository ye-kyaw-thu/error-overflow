# SL-MNIST with CNN

## Prepare Data

Data downloaded from Kaggle site and the link is as follows:  
[https://www.kaggle.com/datasets/datamunge/sign-language-mnist?resource=download](https://www.kaggle.com/datasets/datamunge/sign-language-mnist?resource=download)  


```
(base) yekyaw.thu@gpu:~/exp/sl-mnist/data$ ls
archive.zip
```

Unzip the data file:  

```
(base) yekyaw.thu@gpu:~/exp/sl-mnist/data$ unzip archive.zip
Archive:  archive.zip
  inflating: amer_sign2.png
  inflating: amer_sign3.png
  inflating: american_sign_language.PNG
  inflating: sign_mnist_test.csv
  inflating: sign_mnist_test/sign_mnist_test.csv
  inflating: sign_mnist_train.csv
  inflating: sign_mnist_train/sign_mnist_train.csv
(base) yekyaw.thu@gpu:~/exp/sl-mnist/data$
```

Note: movement contain fingerspelling signs, "J" and "Z" are not included in this dataset.  
Let's check filesize of CSV files.  

```
(base) yekyaw.thu@gpu:~/exp/sl-mnist/data$ wc sign_mnist_train.csv
   27456    27456 83281065 sign_mnist_train.csv
(base) yekyaw.thu@gpu:~/exp/sl-mnist/data$ wc sign_mnist_test.csv
    7173     7173 21777485 sign_mnist_test.csv
(base) yekyaw.thu@gpu:~/exp/sl-mnist/data$ wc ./sign_mnist_train/sign_mnist_train.csv
   27456    27456 83281065 ./sign_mnist_train/sign_mnist_train.csv
(base) yekyaw.thu@gpu:~/exp/sl-mnist/data$ wc ./sign_mnist_test/sign_mnist_test.csv
    7173     7173 21777485 ./sign_mnist_test/sign_mnist_test.csv
(base) yekyaw.thu@gpu:~/exp/sl-mnist/data$
```

It looks same files in terms of filesize.  
Let's see the CSV file inside.  

```
(base) yekyaw.thu@gpu:~/exp/sl-mnist/data$ cat -n sign_mnist_train.csv | head -n 3
     1  label,pixel1,pixel2,pixel3,pixel4,pixel5,pixel6,pixel7,pixel8,pixel9,pixel10,pixel11,pixel12,pixel13,pixel14,pixel15,pixel16,pixel17,pixel18,pixel19,pixel20,pixel21,pixel22,pixel23,pixel24,pixel25,pixel26,pixel27,pixel28,pixel29,pixel30,pixel31,pixel32,pixel33,pixel34,pixel35,pixel36,pixel37,pixel38,pixel39,pixel40,pixel41,pixel42,pixel43,pixel44,pixel45,pixel46,pixel47,pixel48,pixel49,pixel50,pixel51,pixel52,pixel53,pixel54,pixel55,pixel56,pixel57,pixel58,pixel59,pixel60,pixel61,pixel62,pixel63,pixel64,pixel65,pixel66,pixel67,pixel68,pixel69,pixel70,pixel71,pixel72,pixel73,pixel74,pixel75,pixel76,pixel77,pixel78,pixel79,pixel80,pixel81,pixel82,pixel83,pixel84,pixel85,pixel86,pixel87,pixel88,pixel89,pixel90,pixel91,pixel92,pixel93,pixel94,pixel95,pixel96,pixel97,pixel98,pixel99,pixel100,pixel101,pixel102,pixel103,pixel104,pixel105,pixel106,pixel107,pixel108,pixel109,pixel110,pixel111,pixel112,pixel113,pixel114,pixel115,pixel116,pixel117,pixel118,pixel119,pixel120,pixel121,pixel122,pixel123,pixel124,pixel125,pixel126,pixel127,pixel128,pixel129,pixel130,pixel131,pixel132,pixel133,pixel134,pixel135,pixel136,pixel137,pixel138,pixel139,pixel140,pixel141,pixel142,pixel143,pixel144,pixel145,pixel146,pixel147,pixel148,pixel149,pixel150,pixel151,pixel152,pixel153,pixel154,pixel155,pixel156,pixel157,pixel158,pixel159,pixel160,pixel161,pixel162,pixel163,pixel164,pixel165,pixel166,pixel167,pixel168,pixel169,pixel170,pixel171,pixel172,pixel173,pixel174,pixel175,pixel176,pixel177,pixel178,pixel179,pixel180,pixel181,pixel182,pixel183,pixel184,pixel185,pixel186,pixel187,pixel188,pixel189,pixel190,pixel191,pixel192,pixel193,pixel194,pixel195,pixel196,pixel197,pixel198,pixel199,pixel200,pixel201,pixel202,pixel203,pixel204,pixel205,pixel206,pixel207,pixel208,pixel209,pixel210,pixel211,pixel212,pixel213,pixel214,pixel215,pixel216,pixel217,pixel218,pixel219,pixel220,pixel221,pixel222,pixel223,pixel224,pixel225,pixel226,pixel227,pixel228,pixel229,pixel230,pixel231,pixel232,pixel233,pixel234,pixel235,pixel236,pixel237,pixel238,pixel239,pixel240,pixel241,pixel242,pixel243,pixel244,pixel245,pixel246,pixel247,pixel248,pixel249,pixel250,pixel251,pixel252,pixel253,pixel254,pixel255,pixel256,pixel257,pixel258,pixel259,pixel260,pixel261,pixel262,pixel263,pixel264,pixel265,pixel266,pixel267,pixel268,pixel269,pixel270,pixel271,pixel272,pixel273,pixel274,pixel275,pixel276,pixel277,pixel278,pixel279,pixel280,pixel281,pixel282,pixel283,pixel284,pixel285,pixel286,pixel287,pixel288,pixel289,pixel290,pixel291,pixel292,pixel293,pixel294,pixel295,pixel296,pixel297,pixel298,pixel299,pixel300,pixel301,pixel302,pixel303,pixel304,pixel305,pixel306,pixel307,pixel308,pixel309,pixel310,pixel311,pixel312,pixel313,pixel314,pixel315,pixel316,pixel317,pixel318,pixel319,pixel320,pixel321,pixel322,pixel323,pixel324,pixel325,pixel326,pixel327,pixel328,pixel329,pixel330,pixel331,pixel332,pixel333,pixel334,pixel335,pixel336,pixel337,pixel338,pixel339,pixel340,pixel341,pixel342,pixel343,pixel344,pixel345,pixel346,pixel347,pixel348,pixel349,pixel350,pixel351,pixel352,pixel353,pixel354,pixel355,pixel356,pixel357,pixel358,pixel359,pixel360,pixel361,pixel362,pixel363,pixel364,pixel365,pixel366,pixel367,pixel368,pixel369,pixel370,pixel371,pixel372,pixel373,pixel374,pixel375,pixel376,pixel377,pixel378,pixel379,pixel380,pixel381,pixel382,pixel383,pixel384,pixel385,pixel386,pixel387,pixel388,pixel389,pixel390,pixel391,pixel392,pixel393,pixel394,pixel395,pixel396,pixel397,pixel398,pixel399,pixel400,pixel401,pixel402,pixel403,pixel404,pixel405,pixel406,pixel407,pixel408,pixel409,pixel410,pixel411,pixel412,pixel413,pixel414,pixel415,pixel416,pixel417,pixel418,pixel419,pixel420,pixel421,pixel422,pixel423,pixel424,pixel425,pixel426,pixel427,pixel428,pixel429,pixel430,pixel431,pixel432,pixel433,pixel434,pixel435,pixel436,pixel437,pixel438,pixel439,pixel440,pixel441,pixel442,pixel443,pixel444,pixel445,pixel446,pixel447,pixel448,pixel449,pixel450,pixel451,pixel452,pixel453,pixel454,pixel455,pixel456,pixel457,pixel458,pixel459,pixel460,pixel461,pixel462,pixel463,pixel464,pixel465,pixel466,pixel467,pixel468,pixel469,pixel470,pixel471,pixel472,pixel473,pixel474,pixel475,pixel476,pixel477,pixel478,pixel479,pixel480,pixel481,pixel482,pixel483,pixel484,pixel485,pixel486,pixel487,pixel488,pixel489,pixel490,pixel491,pixel492,pixel493,pixel494,pixel495,pixel496,pixel497,pixel498,pixel499,pixel500,pixel501,pixel502,pixel503,pixel504,pixel505,pixel506,pixel507,pixel508,pixel509,pixel510,pixel511,pixel512,pixel513,pixel514,pixel515,pixel516,pixel517,pixel518,pixel519,pixel520,pixel521,pixel522,pixel523,pixel524,pixel525,pixel526,pixel527,pixel528,pixel529,pixel530,pixel531,pixel532,pixel533,pixel534,pixel535,pixel536,pixel537,pixel538,pixel539,pixel540,pixel541,pixel542,pixel543,pixel544,pixel545,pixel546,pixel547,pixel548,pixel549,pixel550,pixel551,pixel552,pixel553,pixel554,pixel555,pixel556,pixel557,pixel558,pixel559,pixel560,pixel561,pixel562,pixel563,pixel564,pixel565,pixel566,pixel567,pixel568,pixel569,pixel570,pixel571,pixel572,pixel573,pixel574,pixel575,pixel576,pixel577,pixel578,pixel579,pixel580,pixel581,pixel582,pixel583,pixel584,pixel585,pixel586,pixel587,pixel588,pixel589,pixel590,pixel591,pixel592,pixel593,pixel594,pixel595,pixel596,pixel597,pixel598,pixel599,pixel600,pixel601,pixel602,pixel603,pixel604,pixel605,pixel606,pixel607,pixel608,pixel609,pixel610,pixel611,pixel612,pixel613,pixel614,pixel615,pixel616,pixel617,pixel618,pixel619,pixel620,pixel621,pixel622,pixel623,pixel624,pixel625,pixel626,pixel627,pixel628,pixel629,pixel630,pixel631,pixel632,pixel633,pixel634,pixel635,pixel636,pixel637,pixel638,pixel639,pixel640,pixel641,pixel642,pixel643,pixel644,pixel645,pixel646,pixel647,pixel648,pixel649,pixel650,pixel651,pixel652,pixel653,pixel654,pixel655,pixel656,pixel657,pixel658,pixel659,pixel660,pixel661,pixel662,pixel663,pixel664,pixel665,pixel666,pixel667,pixel668,pixel669,pixel670,pixel671,pixel672,pixel673,pixel674,pixel675,pixel676,pixel677,pixel678,pixel679,pixel680,pixel681,pixel682,pixel683,pixel684,pixel685,pixel686,pixel687,pixel688,pixel689,pixel690,pixel691,pixel692,pixel693,pixel694,pixel695,pixel696,pixel697,pixel698,pixel699,pixel700,pixel701,pixel702,pixel703,pixel704,pixel705,pixel706,pixel707,pixel708,pixel709,pixel710,pixel711,pixel712,pixel713,pixel714,pixel715,pixel716,pixel717,pixel718,pixel719,pixel720,pixel721,pixel722,pixel723,pixel724,pixel725,pixel726,pixel727,pixel728,pixel729,pixel730,pixel731,pixel732,pixel733,pixel734,pixel735,pixel736,pixel737,pixel738,pixel739,pixel740,pixel741,pixel742,pixel743,pixel744,pixel745,pixel746,pixel747,pixel748,pixel749,pixel750,pixel751,pixel752,pixel753,pixel754,pixel755,pixel756,pixel757,pixel758,pixel759,pixel760,pixel761,pixel762,pixel763,pixel764,pixel765,pixel766,pixel767,pixel768,pixel769,pixel770,pixel771,pixel772,pixel773,pixel774,pixel775,pixel776,pixel777,pixel778,pixel779,pixel780,pixel781,pixel782,pixel783,pixel784
     2  3,107,118,127,134,139,143,146,150,153,156,158,160,163,165,159,166,168,170,170,171,171,171,172,171,171,170,170,169,111,121,129,135,141,144,148,151,154,157,160,163,164,170,119,152,171,171,170,171,172,172,172,172,172,171,171,170,113,123,131,137,142,145,150,152,155,158,161,163,164,172,105,142,170,171,171,171,172,172,173,173,172,171,171,171,116,125,133,139,143,146,151,153,156,159,162,163,167,167,95,144,171,172,172,172,172,172,173,173,173,172,172,171,117,126,134,140,145,149,153,156,158,161,163,164,175,156,87,154,172,173,173,173,173,173,174,174,174,173,172,172,119,128,136,142,146,150,153,156,159,163,165,164,184,148,89,164,172,174,174,174,174,175,175,174,175,174,173,173,122,130,138,143,147,150,154,158,162,165,166,172,181,128,94,170,173,175,174,175,176,177,177,177,177,175,175,174,122,132,139,145,149,152,156,160,163,165,166,181,172,103,113,175,176,178,178,179,179,179,179,178,179,177,175,174,125,134,141,147,150,153,157,161,164,167,168,184,179,116,126,165,176,179,180,180,181,180,180,180,179,178,177,176,128,135,142,148,152,154,158,162,165,168,170,187,180,156,161,124,143,179,178,178,181,182,181,180,181,180,179,179,129,136,144,150,153,155,159,163,166,169,172,187,184,153,102,117,110,175,169,154,182,183,183,182,182,181,181,179,131,138,145,150,155,157,161,165,168,174,190,189,175,146,94,97,113,151,158,129,184,184,184,184,183,183,182,180,131,139,146,151,155,159,163,167,175,182,179,171,159,114,102,89,121,136,136,96,172,186,186,185,185,184,182,181,131,140,147,154,157,160,164,179,186,191,187,180,157,100,88,84,108,111,126,90,120,186,187,187,186,185,184,182,133,141,149,155,158,160,174,201,189,165,151,143,146,120,87,78,87,76,108,98,96,181,188,187,186,186,185,183,133,141,150,156,160,161,179,197,174,135,99,72,95,134,97,72,74,68,116,105,108,187,189,187,187,186,186,185,134,143,151,156,161,163,179,194,156,110,74,42,52,139,94,67,75,75,118,106,129,189,191,190,188,188,187,186,135,144,152,158,163,163,177,193,161,122,84,43,71,134,81,57,71,88,112,98,157,193,193,192,190,190,189,188,136,144,152,158,162,163,176,192,164,128,98,62,60,100,71,76,96,101,105,95,174,195,194,194,194,193,191,190,137,145,152,159,164,165,178,191,164,135,113,82,59,87,98,111,120,108,97,108,190,196,195,195,194,193,193,192,139,146,154,160,164,165,175,186,163,139,112,85,67,102,126,133,126,105,104,176,197,198,197,196,195,195,194,193,138,147,155,161,165,167,172,186,163,137,107,87,76,106,122,125,117,96,156,199,199,200,198,196,196,195,195,194,139,148,156,163,166,168,172,180,158,131,108,99,86,108,118,116,103,107,191,202,201,200,200,200,199,197,198,196,140,149,157,164,168,167,177,178,155,131,118,105,87,100,106,100,96,164,202,202,202,202,202,201,200,199,199,198,140,150,157,165,167,170,181,175,152,130,115,98,82,85,90,99,165,202,203,204,203,203,202,202,201,201,200,200,142,150,159,165,170,191,173,157,144,119,97,84,79,79,91,172,202,203,203,205,204,204,204,203,202,202,201,200,142,151,160,165,188,190,187,150,119,109,85,79,79,78,137,203,205,206,206,207,207,206,206,204,205,204,203,202,142,151,160,172,196,188,188,190,135,96,86,77,77,79,176,205,207,207,207,207,207,207,206,206,206,204,203,202
     3  6,155,157,156,156,156,157,156,158,158,157,158,156,154,154,153,152,151,149,149,148,147,146,144,142,143,138,92,108,158,159,159,159,160,160,160,160,160,160,160,159,158,157,155,154,153,152,151,150,149,149,147,147,146,142,116,143,161,161,161,161,162,161,162,162,162,162,161,161,161,160,159,158,156,155,154,153,152,152,151,150,147,147,125,140,165,164,164,165,165,165,165,165,164,164,164,165,163,163,162,161,159,159,158,156,156,155,152,153,154,151,124,126,166,167,166,167,167,166,167,167,167,167,166,167,165,165,164,163,162,162,161,160,156,151,154,176,145,122,144,100,168,169,168,169,169,168,169,170,170,170,169,168,167,166,167,165,162,159,159,156,151,165,171,146,94,130,159,111,171,171,170,171,171,171,172,171,171,171,172,169,169,170,166,165,160,157,170,177,171,153,124,96,125,157,155,146,172,172,172,173,173,173,173,173,173,173,174,174,171,167,169,175,171,164,165,157,129,112,121,148,164,158,155,152,175,174,174,174,175,174,174,174,174,177,178,174,170,178,182,171,154,127,120,126,138,159,168,165,162,161,158,157,176,176,176,176,177,176,176,177,177,175,169,170,178,169,158,163,139,119,155,171,172,168,165,165,163,162,160,158,177,177,177,178,177,178,178,177,171,159,167,173,157,142,163,152,133,167,177,171,170,170,168,167,166,164,161,159,178,178,179,179,180,178,164,141,137,145,150,141,134,150,154,151,177,181,175,172,173,172,170,167,167,165,163,161,180,179,180,182,180,180,170,156,151,148,151,154,153,153,148,153,147,140,171,176,173,173,171,170,168,167,165,163,182,181,181,182,179,164,149,156,159,153,153,166,173,169,169,163,151,105,141,182,174,175,173,171,171,168,166,165,183,183,183,182,171,159,130,125,135,134,130,137,146,147,164,165,147,103,151,182,176,176,175,173,172,170,167,166,184,185,185,176,174,163,147,145,142,141,141,133,125,125,135,135,112,105,181,179,176,177,175,174,173,171,169,166,185,186,182,170,161,132,125,134,130,144,157,159,152,141,132,121,72,142,176,175,182,177,177,177,175,172,169,168,186,186,173,168,159,128,115,119,109,111,140,154,156,153,140,118,64,67,121,148,160,181,177,177,176,173,169,177,189,178,165,173,163,138,128,128,124,117,111,106,118,139,133,93,40,53,109,146,119,174,179,176,175,174,177,168,186,168,169,169,155,151,145,139,135,130,121,112,104,95,101,61,39,71,99,114,103,177,180,178,178,176,130,171,168,166,163,163,158,149,139,137,138,132,122,116,107,72,66,57,55,63,77,95,155,189,186,177,158,115,86,159,162,162,159,168,170,135,106,97,82,83,103,111,87,68,65,54,89,144,155,173,182,157,165,147,109,134,153,145,165,156,162,169,151,101,73,55,54,65,94,98,71,64,53,114,189,183,177,159,147,142,149,126,160,172,130,92,164,169,171,155,114,82,69,52,62,75,91,82,69,62,139,191,154,120,118,137,147,163,145,159,180,126,87,88,162,170,162,135,98,79,66,58,67,68,66,64,79,146,189,148,132,136,133,144,154,184,139,130,121,93,102,100,162,159,145,112,85,75,68,65,64,62,79,123,192,198,183,126,81,123,137,129,154,217,133,87,87,91,101,94,153,139,115,89,77,72,65,77,106,137,174,185,146,121,111,112,100,78,120,157,168,107,99,121,133,97,95,120,135,116,95,79,69,86,139,173,200,185,175,198,124,118,94,140,133,84,69,149,128,87,94,163,175,103,135,149
(base) yekyaw.thu@gpu:~/exp/sl-mnist/data$
```

Let's check the test file:  

```
(base) yekyaw.thu@gpu:~/exp/sl-mnist/data$ cat -n sign_mnist_test.csv | head -n 3
     1  label,pixel1,pixel2,pixel3,pixel4,pixel5,pixel6,pixel7,pixel8,pixel9,pixel10,pixel11,pixel12,pixel13,pixel14,pixel15,pixel16,pixel17,pixel18,pixel19,pixel20,pixel21,pixel22,pixel23,pixel24,pixel25,pixel26,pixel27,pixel28,pixel29,pixel30,pixel31,pixel32,pixel33,pixel34,pixel35,pixel36,pixel37,pixel38,pixel39,pixel40,pixel41,pixel42,pixel43,pixel44,pixel45,pixel46,pixel47,pixel48,pixel49,pixel50,pixel51,pixel52,pixel53,pixel54,pixel55,pixel56,pixel57,pixel58,pixel59,pixel60,pixel61,pixel62,pixel63,pixel64,pixel65,pixel66,pixel67,pixel68,pixel69,pixel70,pixel71,pixel72,pixel73,pixel74,pixel75,pixel76,pixel77,pixel78,pixel79,pixel80,pixel81,pixel82,pixel83,pixel84,pixel85,pixel86,pixel87,pixel88,pixel89,pixel90,pixel91,pixel92,pixel93,pixel94,pixel95,pixel96,pixel97,pixel98,pixel99,pixel100,pixel101,pixel102,pixel103,pixel104,pixel105,pixel106,pixel107,pixel108,pixel109,pixel110,pixel111,pixel112,pixel113,pixel114,pixel115,pixel116,pixel117,pixel118,pixel119,pixel120,pixel121,pixel122,pixel123,pixel124,pixel125,pixel126,pixel127,pixel128,pixel129,pixel130,pixel131,pixel132,pixel133,pixel134,pixel135,pixel136,pixel137,pixel138,pixel139,pixel140,pixel141,pixel142,pixel143,pixel144,pixel145,pixel146,pixel147,pixel148,pixel149,pixel150,pixel151,pixel152,pixel153,pixel154,pixel155,pixel156,pixel157,pixel158,pixel159,pixel160,pixel161,pixel162,pixel163,pixel164,pixel165,pixel166,pixel167,pixel168,pixel169,pixel170,pixel171,pixel172,pixel173,pixel174,pixel175,pixel176,pixel177,pixel178,pixel179,pixel180,pixel181,pixel182,pixel183,pixel184,pixel185,pixel186,pixel187,pixel188,pixel189,pixel190,pixel191,pixel192,pixel193,pixel194,pixel195,pixel196,pixel197,pixel198,pixel199,pixel200,pixel201,pixel202,pixel203,pixel204,pixel205,pixel206,pixel207,pixel208,pixel209,pixel210,pixel211,pixel212,pixel213,pixel214,pixel215,pixel216,pixel217,pixel218,pixel219,pixel220,pixel221,pixel222,pixel223,pixel224,pixel225,pixel226,pixel227,pixel228,pixel229,pixel230,pixel231,pixel232,pixel233,pixel234,pixel235,pixel236,pixel237,pixel238,pixel239,pixel240,pixel241,pixel242,pixel243,pixel244,pixel245,pixel246,pixel247,pixel248,pixel249,pixel250,pixel251,pixel252,pixel253,pixel254,pixel255,pixel256,pixel257,pixel258,pixel259,pixel260,pixel261,pixel262,pixel263,pixel264,pixel265,pixel266,pixel267,pixel268,pixel269,pixel270,pixel271,pixel272,pixel273,pixel274,pixel275,pixel276,pixel277,pixel278,pixel279,pixel280,pixel281,pixel282,pixel283,pixel284,pixel285,pixel286,pixel287,pixel288,pixel289,pixel290,pixel291,pixel292,pixel293,pixel294,pixel295,pixel296,pixel297,pixel298,pixel299,pixel300,pixel301,pixel302,pixel303,pixel304,pixel305,pixel306,pixel307,pixel308,pixel309,pixel310,pixel311,pixel312,pixel313,pixel314,pixel315,pixel316,pixel317,pixel318,pixel319,pixel320,pixel321,pixel322,pixel323,pixel324,pixel325,pixel326,pixel327,pixel328,pixel329,pixel330,pixel331,pixel332,pixel333,pixel334,pixel335,pixel336,pixel337,pixel338,pixel339,pixel340,pixel341,pixel342,pixel343,pixel344,pixel345,pixel346,pixel347,pixel348,pixel349,pixel350,pixel351,pixel352,pixel353,pixel354,pixel355,pixel356,pixel357,pixel358,pixel359,pixel360,pixel361,pixel362,pixel363,pixel364,pixel365,pixel366,pixel367,pixel368,pixel369,pixel370,pixel371,pixel372,pixel373,pixel374,pixel375,pixel376,pixel377,pixel378,pixel379,pixel380,pixel381,pixel382,pixel383,pixel384,pixel385,pixel386,pixel387,pixel388,pixel389,pixel390,pixel391,pixel392,pixel393,pixel394,pixel395,pixel396,pixel397,pixel398,pixel399,pixel400,pixel401,pixel402,pixel403,pixel404,pixel405,pixel406,pixel407,pixel408,pixel409,pixel410,pixel411,pixel412,pixel413,pixel414,pixel415,pixel416,pixel417,pixel418,pixel419,pixel420,pixel421,pixel422,pixel423,pixel424,pixel425,pixel426,pixel427,pixel428,pixel429,pixel430,pixel431,pixel432,pixel433,pixel434,pixel435,pixel436,pixel437,pixel438,pixel439,pixel440,pixel441,pixel442,pixel443,pixel444,pixel445,pixel446,pixel447,pixel448,pixel449,pixel450,pixel451,pixel452,pixel453,pixel454,pixel455,pixel456,pixel457,pixel458,pixel459,pixel460,pixel461,pixel462,pixel463,pixel464,pixel465,pixel466,pixel467,pixel468,pixel469,pixel470,pixel471,pixel472,pixel473,pixel474,pixel475,pixel476,pixel477,pixel478,pixel479,pixel480,pixel481,pixel482,pixel483,pixel484,pixel485,pixel486,pixel487,pixel488,pixel489,pixel490,pixel491,pixel492,pixel493,pixel494,pixel495,pixel496,pixel497,pixel498,pixel499,pixel500,pixel501,pixel502,pixel503,pixel504,pixel505,pixel506,pixel507,pixel508,pixel509,pixel510,pixel511,pixel512,pixel513,pixel514,pixel515,pixel516,pixel517,pixel518,pixel519,pixel520,pixel521,pixel522,pixel523,pixel524,pixel525,pixel526,pixel527,pixel528,pixel529,pixel530,pixel531,pixel532,pixel533,pixel534,pixel535,pixel536,pixel537,pixel538,pixel539,pixel540,pixel541,pixel542,pixel543,pixel544,pixel545,pixel546,pixel547,pixel548,pixel549,pixel550,pixel551,pixel552,pixel553,pixel554,pixel555,pixel556,pixel557,pixel558,pixel559,pixel560,pixel561,pixel562,pixel563,pixel564,pixel565,pixel566,pixel567,pixel568,pixel569,pixel570,pixel571,pixel572,pixel573,pixel574,pixel575,pixel576,pixel577,pixel578,pixel579,pixel580,pixel581,pixel582,pixel583,pixel584,pixel585,pixel586,pixel587,pixel588,pixel589,pixel590,pixel591,pixel592,pixel593,pixel594,pixel595,pixel596,pixel597,pixel598,pixel599,pixel600,pixel601,pixel602,pixel603,pixel604,pixel605,pixel606,pixel607,pixel608,pixel609,pixel610,pixel611,pixel612,pixel613,pixel614,pixel615,pixel616,pixel617,pixel618,pixel619,pixel620,pixel621,pixel622,pixel623,pixel624,pixel625,pixel626,pixel627,pixel628,pixel629,pixel630,pixel631,pixel632,pixel633,pixel634,pixel635,pixel636,pixel637,pixel638,pixel639,pixel640,pixel641,pixel642,pixel643,pixel644,pixel645,pixel646,pixel647,pixel648,pixel649,pixel650,pixel651,pixel652,pixel653,pixel654,pixel655,pixel656,pixel657,pixel658,pixel659,pixel660,pixel661,pixel662,pixel663,pixel664,pixel665,pixel666,pixel667,pixel668,pixel669,pixel670,pixel671,pixel672,pixel673,pixel674,pixel675,pixel676,pixel677,pixel678,pixel679,pixel680,pixel681,pixel682,pixel683,pixel684,pixel685,pixel686,pixel687,pixel688,pixel689,pixel690,pixel691,pixel692,pixel693,pixel694,pixel695,pixel696,pixel697,pixel698,pixel699,pixel700,pixel701,pixel702,pixel703,pixel704,pixel705,pixel706,pixel707,pixel708,pixel709,pixel710,pixel711,pixel712,pixel713,pixel714,pixel715,pixel716,pixel717,pixel718,pixel719,pixel720,pixel721,pixel722,pixel723,pixel724,pixel725,pixel726,pixel727,pixel728,pixel729,pixel730,pixel731,pixel732,pixel733,pixel734,pixel735,pixel736,pixel737,pixel738,pixel739,pixel740,pixel741,pixel742,pixel743,pixel744,pixel745,pixel746,pixel747,pixel748,pixel749,pixel750,pixel751,pixel752,pixel753,pixel754,pixel755,pixel756,pixel757,pixel758,pixel759,pixel760,pixel761,pixel762,pixel763,pixel764,pixel765,pixel766,pixel767,pixel768,pixel769,pixel770,pixel771,pixel772,pixel773,pixel774,pixel775,pixel776,pixel777,pixel778,pixel779,pixel780,pixel781,pixel782,pixel783,pixel784
     2  6,149,149,150,150,150,151,151,150,151,152,152,152,152,152,153,153,151,152,152,153,152,152,151,151,150,150,150,149,150,150,150,152,152,151,152,152,152,152,152,153,154,153,154,154,153,154,153,154,153,153,152,152,152,151,150,151,150,151,151,152,152,152,153,153,152,152,152,153,154,154,155,155,154,154,155,155,155,155,154,153,153,151,151,152,150,151,151,152,152,152,154,154,154,154,154,153,154,155,156,157,157,156,155,156,155,154,154,155,152,154,153,153,151,152,152,152,154,154,154,154,154,155,157,156,156,156,154,150,146,147,146,147,143,137,126,126,142,139,152,154,152,153,153,154,154,155,154,155,155,154,153,150,144,143,145,139,142,144,157,157,147,139,128,119,130,113,147,156,151,153,153,155,155,156,155,152,145,139,141,141,141,153,153,143,135,137,139,133,121,107,101,104,110,127,157,156,151,152,153,155,155,154,151,146,139,131,130,134,137,132,125,111,101,94,95,105,113,122,133,145,153,157,156,156,152,152,154,152,151,150,149,149,139,122,104,98,92,82,81,81,85,114,145,157,160,162,161,159,157,156,156,156,151,151,150,146,145,147,148,147,145,132,97,71,62,66,88,116,145,162,160,159,157,155,156,157,157,156,155,155,151,145,144,145,147,145,147,150,150,124,92,68,63,67,86,159,163,155,158,157,156,156,157,156,156,156,155,154,143,144,145,145,143,147,152,152,128,90,79,68,64,70,67,84,147,164,157,158,157,157,157,156,157,156,156,155,145,146,143,145,145,150,149,149,139,118,85,62,62,75,73,62,67,140,164,157,158,158,158,158,157,157,156,156,150,147,144,147,149,148,149,158,158,136,94,63,58,69,85,82,67,70,156,160,159,160,159,158,157,156,156,156,147,148,147,145,148,152,151,160,153,119,86,66,64,63,69,75,78,57,130,165,158,159,158,159,158,157,157,157,149,148,146,145,147,149,146,151,144,110,78,65,66,66,58,59,64,79,150,165,162,162,162,162,161,161,158,156,151,146,143,141,138,140,142,146,144,121,84,56,62,70,71,68,57,117,144,144,147,149,152,150,146,146,154,160,147,144,143,142,140,142,146,151,154,131,85,59,51,60,85,69,64,76,75,79,81,79,76,83,112,141,163,163,144,148,147,145,145,148,150,155,151,119,74,62,63,55,62,72,73,77,74,73,68,88,113,138,162,162,168,168,146,146,142,141,141,138,134,142,124,96,75,67,65,63,62,78,87,76,84,96,126,162,172,155,144,149,151,161,142,136,132,134,127,119,118,119,103,87,77,73,70,62,64,72,93,134,155,160,166,156,150,151,143,136,145,149,130,132,127,120,114,110,109,105,91,77,74,75,74,65,73,113,166,177,170,161,152,141,134,136,140,133,127,130,113,116,115,106,101,95,86,84,85,77,78,74,76,103,152,179,170,157,155,151,140,129,126,126,133,130,122,125,81,86,85,83,76,72,73,76,77,79,71,101,151,178,177,170,161,152,147,151,133,115,121,121,124,126,122,122,61,61,67,69,70,75,78,78,81,68,113,165,174,169,162,157,149,148,148,148,126,100,113,117,113,122,118,115,69,69,77,78,75,76,78,79,67,120,173,157,159,148,155,150,138,143,148,149,123,91,101,111,111,116,113,118,74,75,76,75,75,76,75,68,124,172,152,146,146,146,152,142,131,134,144,147,125,87,87,103,107,110,116,113,75,74,74,74,76,74,82,134,168,155,146,137,145,146,149,135,124,125,138,148,127,89,82,96,106,112,120,107
     3  5,126,128,131,132,133,134,135,135,136,138,137,137,138,138,139,137,142,140,138,139,137,137,136,135,134,133,134,132,129,132,134,135,135,137,139,139,139,140,141,141,142,143,142,142,116,138,141,140,141,140,139,138,137,136,136,134,133,135,138,139,139,141,142,143,142,143,145,145,143,145,145,158,94,118,151,143,144,144,142,141,141,140,139,138,137,139,142,142,142,144,146,146,146,147,147,147,148,117,128,168,101,98,157,146,147,146,146,145,144,143,142,141,140,142,145,146,147,148,149,149,149,151,151,149,161,114,99,174,99,84,162,149,151,149,148,147,146,146,145,144,143,145,149,150,150,151,153,153,154,153,154,152,167,126,88,169,99,87,164,152,153,152,151,150,149,148,148,147,145,147,151,152,153,155,155,155,151,154,158,155,170,130,79,166,111,93,166,156,157,156,155,153,152,152,152,150,149,150,153,155,155,158,157,163,129,120,166,156,171,140,82,162,102,97,168,158,160,158,162,160,154,154,154,152,151,152,156,158,159,159,158,164,139,91,165,159,174,144,71,156,96,100,171,161,161,158,128,145,162,156,155,155,152,155,159,160,161,161,160,168,158,76,159,164,172,142,63,155,117,100,174,159,164,164,126,103,162,161,158,157,153,157,160,162,162,162,164,167,158,78,158,167,167,156,73,133,129,102,172,157,148,130,156,132,129,163,161,159,157,159,162,164,164,165,166,167,173,89,139,172,162,163,79,98,132,111,170,160,142,54,125,150,102,150,167,162,159,161,166,165,167,167,167,168,178,118,112,175,164,167,82,91,129,110,160,156,130,96,157,130,106,169,165,164,159,162,166,167,168,168,170,169,164,168,132,141,162,153,103,113,117,96,133,143,107,147,172,99,139,174,165,166,161,164,167,170,171,171,170,173,160,173,162,129,132,132,109,109,108,99,135,142,111,163,154,77,156,172,167,167,165,167,168,171,172,173,173,174,169,170,182,150,125,124,100,106,103,102,130,138,124,178,130,64,168,172,170,169,165,168,170,171,172,174,175,174,175,172,195,170,114,110,94,89,98,105,127,134,124,182,126,80,180,171,171,171,166,169,171,172,173,174,175,176,177,174,197,179,119,86,87,81,94,118,136,123,116,177,127,94,183,172,173,173,169,172,172,174,175,174,177,178,178,175,192,176,126,87,86,82,109,130,147,159,128,164,128,100,184,174,173,173,169,172,173,173,176,178,179,178,181,175,189,171,126,89,80,90,121,137,164,175,141,140,108,95,184,176,175,173,171,173,174,175,177,179,179,179,181,174,189,171,134,91,80,98,134,159,164,167,153,114,73,82,185,176,177,177,172,173,174,177,178,179,180,180,183,174,186,172,138,93,82,97,143,172,169,160,132,89,44,108,189,176,178,178,171,173,177,178,179,180,181,182,185,178,179,170,137,95,88,90,152,180,167,141,112,65,64,176,183,179,179,178,173,174,178,179,179,180,182,183,186,175,165,168,137,100,96,88,149,168,147,122,92,50,144,193,181,181,180,179,173,174,177,179,180,180,183,182,187,177,158,161,130,111,101,91,136,150,135,112,62,87,192,183,185,183,181,180,173,174,177,178,179,179,181,182,184,179,156,151,124,116,96,88,128,138,126,81,49,164,190,184,185,184,182,181,172,174,177,178,178,178,180,182,184,177,160,154,128,114,97,78,114,112,89,48,133,194,182,185,184,184,182,181,172,174,177,178,178,179,181,183,187,175,165,154,118,107,100,75,96,83,47,104,194,183,186,184,184,184,182,180
(base) yekyaw.thu@gpu:~/exp/sl-mnist/data$
```

## Cloning the GitHub Code

```
(base) yekyaw.thu@gpu:~/exp/sl-mnist$ git clone https://github.com/mg343/Sign-Language-Detection
Cloning into 'Sign-Language-Detection'...
remote: Enumerating objects: 73, done.
remote: Counting objects: 100% (73/73), done.
remote: Compressing objects: 100% (55/55), done.
remote: Total 73 (delta 23), reused 52 (delta 14), pack-reused 0
Unpacking objects: 100% (73/73), 16.35 KiB | 1.26 MiB/s, done.
(base) yekyaw.thu@gpu:~/exp/sl-mnist$ cd Sign-Language-Detection/
(base) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ ls
camerahands.py  model.py  README.md
(base) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

At 1st learn the model building python code:  

```python
(base) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ cat model.py
import matplotlib.pyplot as plt
import seaborn as sns
import keras
from keras.models import Sequential
from keras.layers import Dense, Conv2D , MaxPool2D , Flatten , Dropout , BatchNormalization
from keras.preprocessing.image import ImageDataGenerator
from sklearn.model_selection import train_test_split
from sklearn.metrics import classification_report,confusion_matrix
from keras.callbacks import ReduceLROnPlateau
import pandas as pd

train_df = pd.read_csv("sign_mnist_train.csv")
test_df = pd.read_csv("sign_mnist_test.csv")

y_train = train_df['label']
y_test = test_df['label']
del train_df['label']
del test_df['label']

from sklearn.preprocessing import LabelBinarizer
label_binarizer = LabelBinarizer()
y_train = label_binarizer.fit_transform(y_train)
y_test = label_binarizer.fit_transform(y_test)

x_train = train_df.values
x_test = test_df.values

x_train = x_train / 255
x_test = x_test / 255

x_train = x_train.reshape(-1,28,28,1)
x_test = x_test.reshape(-1,28,28,1)

datagen = ImageDataGenerator(
        featurewise_center=False,  # set input mean to 0 over the dataset
        samplewise_center=False,  # set each sample mean to 0
        featurewise_std_normalization=False,  # divide inputs by std of the dataset
        samplewise_std_normalization=False,  # divide each input by its std
        zca_whitening=False,  # apply ZCA whitening
        rotation_range=10,  # randomly rotate images in the range (degrees, 0 to 180)
        zoom_range = 0.1, # Randomly zoom image
        width_shift_range=0.1,  # randomly shift images horizontally (fraction of total width)
        height_shift_range=0.1,  # randomly shift images vertically (fraction of total height)
        horizontal_flip=False,  # randomly flip images
        vertical_flip=False)  # randomly flip images

datagen.fit(x_train)

learning_rate_reduction = ReduceLROnPlateau(monitor='val_accuracy', patience = 2, verbose=1,factor=0.5, min_lr=0.00001)

model = Sequential()
model.add(Conv2D(75 , (3,3) , strides = 1 , padding = 'same' , activation = 'relu' , input_shape = (28,28,1)))
model.add(BatchNormalization())
model.add(MaxPool2D((2,2) , strides = 2 , padding = 'same'))
model.add(Conv2D(50 , (3,3) , strides = 1 , padding = 'same' , activation = 'relu'))
model.add(Dropout(0.2))
model.add(BatchNormalization())
model.add(MaxPool2D((2,2) , strides = 2 , padding = 'same'))
model.add(Conv2D(25 , (3,3) , strides = 1 , padding = 'same' , activation = 'relu'))
model.add(BatchNormalization())
model.add(MaxPool2D((2,2) , strides = 2 , padding = 'same'))
model.add(Flatten())
model.add(Dense(units = 512 , activation = 'relu'))
model.add(Dropout(0.3))
model.add(Dense(units = 24 , activation = 'softmax'))
model.compile(optimizer = 'adam' , loss = 'categorical_crossentropy' , metrics = ['accuracy'])
model.summary()

history = model.fit(datagen.flow(x_train,y_train, batch_size = 128) ,epochs = 20 , validation_data = (x_test, y_test) , callbacks = [learning_rate_reduction])

model.save('smnist.h5')(base) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$

```

Let's learn the online testing python code:  

```python
(base) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ cat camerahands.py
import os
os.environ['TF_CPP_MIN_LOG_LEVEL'] = '3'
import tensorflow as tf
import cv2
import mediapipe as mp
from keras.models import load_model
import numpy as np
import time
import pandas as pd

model = load_model('smnist.h5')

mphands = mp.solutions.hands
hands = mphands.Hands()
mp_drawing = mp.solutions.drawing_utils
cap = cv2.VideoCapture(0)

_, frame = cap.read()

h, w, c = frame.shape

img_counter = 0
analysisframe = ''
letterpred = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y']
while True:
    _, frame = cap.read()

    k = cv2.waitKey(1)
    if k%256 == 27:
        # ESC pressed
        print("Escape hit, closing...")
        break
    elif k%256 == 32:
        # SPACE pressed
        analysisframe = frame
        showframe = analysisframe
        cv2.imshow("Frame", showframe)
        framergbanalysis = cv2.cvtColor(analysisframe, cv2.COLOR_BGR2RGB)
        resultanalysis = hands.process(framergbanalysis)
        hand_landmarksanalysis = resultanalysis.multi_hand_landmarks
        if hand_landmarksanalysis:
            for handLMsanalysis in hand_landmarksanalysis:
                x_max = 0
                y_max = 0
                x_min = w
                y_min = h
                for lmanalysis in handLMsanalysis.landmark:
                    x, y = int(lmanalysis.x * w), int(lmanalysis.y * h)
                    if x > x_max:
                        x_max = x
                    if x < x_min:
                        x_min = x
                    if y > y_max:
                        y_max = y
                    if y < y_min:
                        y_min = y
                y_min -= 20
                y_max += 20
                x_min -= 20
                x_max += 20

        analysisframe = cv2.cvtColor(analysisframe, cv2.COLOR_BGR2GRAY)
        analysisframe = analysisframe[y_min:y_max, x_min:x_max]
        analysisframe = cv2.resize(analysisframe,(28,28))


        nlist = []
        rows,cols = analysisframe.shape
        for i in range(rows):
            for j in range(cols):
                k = analysisframe[i,j]
                nlist.append(k)

        datan = pd.DataFrame(nlist).T
        colname = []
        for val in range(784):
            colname.append(val)
        datan.columns = colname

        pixeldata = datan.values
        pixeldata = pixeldata / 255
        pixeldata = pixeldata.reshape(-1,28,28,1)
        prediction = model.predict(pixeldata)
        predarray = np.array(prediction[0])
        letter_prediction_dict = {letterpred[i]: predarray[i] for i in range(len(letterpred))}
        predarrayordered = sorted(predarray, reverse=True)
        high1 = predarrayordered[0]
        high2 = predarrayordered[1]
        high3 = predarrayordered[2]
        for key,value in letter_prediction_dict.items():
            if value==high1:
                print("Predicted Character 1: ", key)
                print('Confidence 1: ', 100*value)
            elif value==high2:
                print("Predicted Character 2: ", key)
                print('Confidence 2: ', 100*value)
            elif value==high3:
                print("Predicted Character 3: ", key)
                print('Confidence 3: ', 100*value)
        time.sleep(5)

    framergb = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)
    result = hands.process(framergb)
    hand_landmarks = result.multi_hand_landmarks
    if hand_landmarks:
        for handLMs in hand_landmarks:
            x_max = 0
            y_max = 0
            x_min = w
            y_min = h
            for lm in handLMs.landmark:
                x, y = int(lm.x * w), int(lm.y * h)
                if x > x_max:
                    x_max = x
                if x < x_min:
                    x_min = x
                if y > y_max:
                    y_max = y
                if y < y_min:
                    y_min = y
            y_min -= 20
            y_max += 20
            x_min -= 20
            x_max += 20
            cv2.rectangle(frame, (x_min, y_min), (x_max, y_max), (0, 255, 0), 2)
    cv2.imshow("Frame", frame)

cap.release()
cv2.destroyAllWindows()(base) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```