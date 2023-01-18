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

## Prepareing a New Conda Environment

No information relating to Python libraries ...  
Anyway, plan to run in an new Conda environment. Let's create a new environment at first ...  

```
(base) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ python --version
Python 3.7.6
(base) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ conda create --name sl-mnist
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 22.11.1

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/sl-mnist



Proceed ([y]/n)? y

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate sl-mnist
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

Entering to the sl-mnist conda environment ...  

```
(base) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ conda activate sl-mnist
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

## Python Library INstallation  

I installed some libraries based on the above two python code and some screen logs are as follows:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ pip install matplotlib
Collecting matplotlib
  Downloading matplotlib-3.6.3-cp38-cp38-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (9.4 MB)
     |████████████████████████████████| 9.4 MB 531 kB/s
Collecting cycler>=0.10
  Using cached cycler-0.11.0-py3-none-any.whl (6.4 kB)
Collecting python-dateutil>=2.7
  Using cached python_dateutil-2.8.2-py2.py3-none-any.whl (247 kB)
Collecting pyparsing>=2.2.1
  Using cached pyparsing-3.0.9-py3-none-any.whl (98 kB)
Requirement already satisfied: pillow>=6.2.0 in /usr/lib/python3/dist-packages (from matplotlib) (7.0.0)
Collecting fonttools>=4.22.0
  Using cached fonttools-4.38.0-py3-none-any.whl (965 kB)
Collecting packaging>=20.0
  Downloading packaging-23.0-py3-none-any.whl (42 kB)
     |████████████████████████████████| 42 kB 302 kB/s
Collecting contourpy>=1.0.1
  Downloading contourpy-1.0.7-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (300 kB)
     |████████████████████████████████| 300 kB 54.6 MB/s
Collecting numpy>=1.19
  Downloading numpy-1.24.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (17.3 MB)
     |████████████████████████████████| 17.3 MB 73.3 MB/s
Collecting kiwisolver>=1.0.1
  Using cached kiwisolver-1.4.4-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.whl (1.2 MB)
Requirement already satisfied: six>=1.5 in /usr/lib/python3/dist-packages (from python-dateutil>=2.7->matplotlib) (1.14.0)
Installing collected packages: cycler, python-dateutil, pyparsing, fonttools, packaging, numpy, contourpy, kiwisolver, matplotlib
  WARNING: The scripts fonttools, pyftmerge, pyftsubset and ttx are installed in '/home/yekyaw.thu/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  WARNING: The scripts f2py, f2py3 and f2py3.8 are installed in '/home/yekyaw.thu/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
Successfully installed contourpy-1.0.7 cycler-0.11.0 fonttools-4.38.0 kiwisolver-1.4.4 matplotlib-3.6.3 numpy-1.24.1 packaging-23.0 pyparsing-3.0.9 python-dateutil-2.8.2
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

Installing the seaborn library ...  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ pip install seaborn
Collecting seaborn
  Downloading seaborn-0.12.2-py3-none-any.whl (293 kB)
     |████████████████████████████████| 293 kB 482 kB/s
Requirement already satisfied: numpy!=1.24.0,>=1.17 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from seaborn) (1.24.1)
Collecting pandas>=0.25
  Downloading pandas-1.5.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (12.2 MB)
     |████████████████████████████████| 12.2 MB 57 kB/s
Requirement already satisfied: matplotlib!=3.6.1,>=3.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from seaborn) (3.6.3)
Collecting pytz>=2020.1
  Downloading pytz-2022.7.1-py2.py3-none-any.whl (499 kB)
     |████████████████████████████████| 499 kB 72.5 MB/s
Requirement already satisfied: python-dateutil>=2.8.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from pandas>=0.25->seaborn) (2.8.2)
Requirement already satisfied: contourpy>=1.0.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (1.0.7)
Requirement already satisfied: fonttools>=4.22.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (4.38.0)
Requirement already satisfied: pillow>=6.2.0 in /usr/lib/python3/dist-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (7.0.0)
Requirement already satisfied: kiwisolver>=1.0.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (1.4.4)
Requirement already satisfied: packaging>=20.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (23.0)
Requirement already satisfied: pyparsing>=2.2.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (3.0.9)
Requirement already satisfied: cycler>=0.10 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (0.11.0)
Requirement already satisfied: six>=1.5 in /usr/lib/python3/dist-packages (from python-dateutil>=2.8.1->pandas>=0.25->seaborn) (1.14.0)
Installing collected packages: pytz, pandas, seaborn
Successfully installed pandas-1.5.2 pytz-2022.7.1 seaborn-0.12.2
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

Checking the Keras framework:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ pip install keras
Requirement already satisfied: keras in /usr/local/lib/python3.8/dist-packages (2.9.0)
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

Installing the sklearn library ...  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ pip install sklearn
Collecting sklearn
  Using cached sklearn-0.0.post1.tar.gz (3.6 kB)
Building wheels for collected packages: sklearn
  Building wheel for sklearn (setup.py) ... done
  Created wheel for sklearn: filename=sklearn-0.0.post1-py3-none-any.whl size=2342 sha256=ed2785c160d9e36ec0d1cd9647b555c4a1d42880b0e9ce374f5294e36ac2fec5
  Stored in directory: /home/yekyaw.thu/.cache/pip/wheels/14/25/f7/1cc0956978ae479e75140219088deb7a36f60459df242b1a72
Successfully built sklearn
Installing collected packages: sklearn
Successfully installed sklearn-0.0.post1
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

Checking the pandas library:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ pip install sklearn
Collecting sklearn
  Using cached sklearn-0.0.post1.tar.gz (3.6 kB)
Building wheels for collected packages: sklearn
  Building wheel for sklearn (setup.py) ... done
  Created wheel for sklearn: filename=sklearn-0.0.post1-py3-none-any.whl size=2342 sha256=ed2785c160d9e36ec0d1cd9647b555c4a1d42880b0e9ce374f5294e36ac2fec5
  Stored in directory: /home/yekyaw.thu/.cache/pip/wheels/14/25/f7/1cc0956978ae479e75140219088deb7a36f60459df242b1a72
Successfully built sklearn
Installing collected packages: sklearn
Successfully installed sklearn-0.0.post1
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

I think necessary libraries are already installed and want to make confirmation by training the model ...  

## Training the CNN Model with SL-MNIST Dataset

before training copied the training/testing CSV files to the current path as follows:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ pip install sklearn
Collecting sklearn
  Using cached sklearn-0.0.post1.tar.gz (3.6 kB)
Building wheels for collected packages: sklearn
  Building wheel for sklearn (setup.py) ... done
  Created wheel for sklearn: filename=sklearn-0.0.post1-py3-none-any.whl size=2342 sha256=ed2785c160d9e36ec0d1cd9647b555c4a1d42880b0e9ce374f5294e36ac2fec5
  Stored in directory: /home/yekyaw.thu/.cache/pip/wheels/14/25/f7/1cc0956978ae479e75140219088deb7a36f60459df242b1a72
Successfully built sklearn
Installing collected packages: sklearn
Successfully installed sklearn-0.0.post1
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

start training and got following error:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ time python ./model.py | tee train1.log
Traceback (most recent call last):
  File "./model.py", line 1, in <module>
    import matplotlib.pyplot as plt
ImportError: No module named matplotlib.pyplot

real    0m0.012s
user    0m0.013s
sys     0m0.000s
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

Doubting on Python versions and checked the current active python versions:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ python --version
Python 2.7.18
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ python3 --version
Python 3.8.10
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

Training with Python3 and got tensorflow not exist error:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ time python3 ./model.py | tee train1.lo
g
Traceback (most recent call last):
  File "./model.py", line 5, in <module>
    import keras
  File "/usr/local/lib/python3.8/dist-packages/keras/__init__.py", line 21, in <module>
    from tensorflow.python import tf2
ModuleNotFoundError: No module named 'tensorflow'

real    0m0.927s
user    0m0.934s
sys     0m1.505s
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

OK. I will install tensorflow ...  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ pip install tensorflow
Collecting tensorflow
  Using cached tensorflow-2.11.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (588.3 MB)
Requirement already satisfied: six>=1.12.0 in /usr/lib/python3/dist-packages (from tensorflow) (1.14.0)
Collecting tensorflow-io-gcs-filesystem>=0.23.1; platform_machine != "arm64" or platform_system != "Darwin"
  Downloading tensorflow_io_gcs_filesystem-0.29.0-cp38-cp38-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (2.4 MB)
     |████████████████████████████████| 2.4 MB 531 kB/s
Collecting grpcio<2.0,>=1.24.3
  Downloading grpcio-1.51.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (4.8 MB)
     |████████████████████████████████| 4.8 MB 4.3 MB/s
Collecting protobuf<3.20,>=3.9.2
  Using cached protobuf-3.19.6-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.1 MB)
Collecting tensorflow-estimator<2.12,>=2.11.0
  Using cached tensorflow_estimator-2.11.0-py2.py3-none-any.whl (439 kB)
Collecting libclang>=13.0.0
  Downloading libclang-15.0.6.1-py2.py3-none-manylinux2010_x86_64.whl (21.5 MB)
     |████████████████████████████████| 21.5 MB 2.8 MB/s
Collecting astunparse>=1.6.0
  Using cached astunparse-1.6.3-py2.py3-none-any.whl (12 kB)
Collecting h5py>=2.9.0
  Using cached h5py-3.7.0-cp38-cp38-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (4.5 MB)
Requirement already satisfied: setuptools in /usr/lib/python3/dist-packages (from tensorflow) (45.2.0)
Requirement already satisfied: numpy>=1.20 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (1.24.1)
Collecting tensorboard<2.12,>=2.11
  Downloading tensorboard-2.11.2-py3-none-any.whl (6.0 MB)
     |████████████████████████████████| 6.0 MB 2.2 MB/s
Collecting termcolor>=1.1.0
  Downloading termcolor-2.2.0-py3-none-any.whl (6.6 kB)
Collecting absl-py>=1.0.0
  Downloading absl_py-1.4.0-py3-none-any.whl (126 kB)
     |████████████████████████████████| 126 kB 2.6 MB/s
Collecting wrapt>=1.11.0
  Using cached wrapt-1.14.1-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (81 kB)
Collecting opt-einsum>=2.3.2
  Using cached opt_einsum-3.3.0-py3-none-any.whl (65 kB)
Requirement already satisfied: packaging in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (23.0)
Collecting google-pasta>=0.1.1
  Using cached google_pasta-0.2.0-py3-none-any.whl (57 kB)
Collecting flatbuffers>=2.0
  Downloading flatbuffers-23.1.4-py2.py3-none-any.whl (26 kB)
Collecting gast<=0.4.0,>=0.2.1
  Using cached gast-0.4.0-py3-none-any.whl (9.8 kB)
Collecting typing-extensions>=3.6.6
  Using cached typing_extensions-4.4.0-py3-none-any.whl (26 kB)
Collecting keras<2.12,>=2.11.0
  Using cached keras-2.11.0-py2.py3-none-any.whl (1.7 MB)
Requirement already satisfied: wheel<1.0,>=0.23.0 in /usr/lib/python3/dist-packages (from astunparse>=1.6.0->tensorflow) (0.34.2)
Collecting google-auth-oauthlib<0.5,>=0.4.1
  Using cached google_auth_oauthlib-0.4.6-py2.py3-none-any.whl (18 kB)
Collecting werkzeug>=1.0.1
  Using cached Werkzeug-2.2.2-py3-none-any.whl (232 kB)
Collecting tensorboard-data-server<0.7.0,>=0.6.0
  Using cached tensorboard_data_server-0.6.1-py3-none-manylinux2010_x86_64.whl (4.9 MB)
Collecting markdown>=2.6.8
  Using cached Markdown-3.4.1-py3-none-any.whl (93 kB)
Collecting tensorboard-plugin-wit>=1.6.0
  Using cached tensorboard_plugin_wit-1.8.1-py3-none-any.whl (781 kB)
Collecting google-auth<3,>=1.6.3
  Downloading google_auth-2.16.0-py2.py3-none-any.whl (177 kB)
     |████████████████████████████████| 177 kB 2.5 MB/s
Requirement already satisfied: requests<3,>=2.21.0 in /usr/lib/python3/dist-packages (from tensorboard<2.12,>=2.11->tensorflow) (2.22.0)
Collecting requests-oauthlib>=0.7.0
  Using cached requests_oauthlib-1.3.1-py2.py3-none-any.whl (23 kB)
Collecting MarkupSafe>=2.1.1
  Downloading MarkupSafe-2.1.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (25 kB)
Collecting importlib-metadata>=4.4; python_version < "3.10"
  Downloading importlib_metadata-6.0.0-py3-none-any.whl (21 kB)
Collecting cachetools<6.0,>=2.0.0
  Downloading cachetools-5.2.1-py3-none-any.whl (9.3 kB)
Requirement already satisfied: pyasn1-modules>=0.2.1 in /usr/lib/python3/dist-packages (from google-auth<3,>=1.6.3->tensorboard<2.12,>=2.11->tensorflow) (0.2.1)
Collecting rsa<5,>=3.1.4; python_version >= "3.6"
  Using cached rsa-4.9-py3-none-any.whl (34 kB)
Requirement already satisfied: oauthlib>=3.0.0 in /usr/lib/python3/dist-packages (from requests-oauthlib>=0.7.0->google-auth-oauthlib<0.5,>=0.4.1->tensorboard<2.12,>=2.11->tensorflow) (3.1.0)
Requirement already satisfied: zipp>=0.5 in /usr/lib/python3/dist-packages (from importlib-metadata>=4.4; python_version < "3.10"->markdown>=2.6.8->tensorboard<2.12,>=2.11->tensorflow) (1.0.0)
Requirement already satisfied: pyasn1>=0.1.3 in /usr/lib/python3/dist-packages (from rsa<5,>=3.1.4; python_version >= "3.6"->google-auth<3,>=1.6.3->tensorboard<2.12,>=2.11->tensorflow) (0.4.2)
Installing collected packages: tensorflow-io-gcs-filesystem, grpcio, protobuf, tensorflow-estimator, libclang, astunparse, h5py, requests-oauthlib, cachetools, rsa, google-auth, google-auth-oauthlib, MarkupSafe, werkzeug, tensorboard-data-server, importlib-metadata, markdown, tensorboard-plugin-wit, absl-py, tensorboard, termcolor, wrapt, opt-einsum, google-pasta, flatbuffers, gast, typing-extensions, keras, tensorflow
  WARNING: The scripts pyrsa-decrypt, pyrsa-encrypt, pyrsa-keygen, pyrsa-priv2pub, pyrsa-sign and pyrsa-verify are installed in '/home/yekyaw.thu/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  WARNING: The script google-oauthlib-tool is installed in '/home/yekyaw.thu/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  WARNING: The script markdown_py is installed in '/home/yekyaw.thu/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  WARNING: The script tensorboard is installed in '/home/yekyaw.thu/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  WARNING: The scripts estimator_ckpt_converter, import_pb_to_tensorboard, saved_model_cli, tensorboard, tf_upgrade_v2, tflite_convert, toco and toco_from_protos are installed in '/home/yekyaw.thu/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
Successfully installed MarkupSafe-2.1.1 absl-py-1.4.0 astunparse-1.6.3 cachetools-5.2.1 flatbuffers-23.1.4 gast-0.4.0 google-auth-2.16.0 google-auth-oauthlib-0.4.6 google-pasta-0.2.0 grpcio-1.51.1 h5py-3.7.0 importlib-metadata-6.0.0 keras-2.11.0 libclang-15.0.6.1 markdown-3.4.1 opt-einsum-3.3.0 protobuf-3.19.6 requests-oauthlib-1.3.1 rsa-4.9 tensorboard-2.11.2 tensorboard-data-server-0.6.1 tensorboard-plugin-wit-1.8.1 tensorflow-2.11.0 tensorflow-estimator-2.11.0 tensorflow-io-gcs-filesystem-0.29.0 termcolor-2.2.0 typing-extensions-4.4.0 werkzeug-2.2.2 wrapt-1.14.1
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

After installed tensorflow, train again and got following error:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ pip install tensorflow
Collecting tensorflow
  Using cached tensorflow-2.11.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (588.3 MB)
Requirement already satisfied: six>=1.12.0 in /usr/lib/python3/dist-packages (from tensorflow) (1.14.0)
Collecting tensorflow-io-gcs-filesystem>=0.23.1; platform_machine != "arm64" or platform_system != "Darwin"
  Downloading tensorflow_io_gcs_filesystem-0.29.0-cp38-cp38-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (2.4 MB)
     |████████████████████████████████| 2.4 MB 531 kB/s
Collecting grpcio<2.0,>=1.24.3
  Downloading grpcio-1.51.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (4.8 MB)
     |████████████████████████████████| 4.8 MB 4.3 MB/s
Collecting protobuf<3.20,>=3.9.2
  Using cached protobuf-3.19.6-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.1 MB)
Collecting tensorflow-estimator<2.12,>=2.11.0
  Using cached tensorflow_estimator-2.11.0-py2.py3-none-any.whl (439 kB)
Collecting libclang>=13.0.0
  Downloading libclang-15.0.6.1-py2.py3-none-manylinux2010_x86_64.whl (21.5 MB)
     |████████████████████████████████| 21.5 MB 2.8 MB/s
Collecting astunparse>=1.6.0
  Using cached astunparse-1.6.3-py2.py3-none-any.whl (12 kB)
Collecting h5py>=2.9.0
  Using cached h5py-3.7.0-cp38-cp38-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (4.5 MB)
Requirement already satisfied: setuptools in /usr/lib/python3/dist-packages (from tensorflow) (45.2.0)
Requirement already satisfied: numpy>=1.20 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (1.24.1)
Collecting tensorboard<2.12,>=2.11
  Downloading tensorboard-2.11.2-py3-none-any.whl (6.0 MB)
     |████████████████████████████████| 6.0 MB 2.2 MB/s
Collecting termcolor>=1.1.0
  Downloading termcolor-2.2.0-py3-none-any.whl (6.6 kB)
Collecting absl-py>=1.0.0
  Downloading absl_py-1.4.0-py3-none-any.whl (126 kB)
     |████████████████████████████████| 126 kB 2.6 MB/s
Collecting wrapt>=1.11.0
  Using cached wrapt-1.14.1-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (81 kB)
Collecting opt-einsum>=2.3.2
  Using cached opt_einsum-3.3.0-py3-none-any.whl (65 kB)
Requirement already satisfied: packaging in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (23.0)
Collecting google-pasta>=0.1.1
  Using cached google_pasta-0.2.0-py3-none-any.whl (57 kB)
Collecting flatbuffers>=2.0
  Downloading flatbuffers-23.1.4-py2.py3-none-any.whl (26 kB)
Collecting gast<=0.4.0,>=0.2.1
  Using cached gast-0.4.0-py3-none-any.whl (9.8 kB)
Collecting typing-extensions>=3.6.6
  Using cached typing_extensions-4.4.0-py3-none-any.whl (26 kB)
Collecting keras<2.12,>=2.11.0
  Using cached keras-2.11.0-py2.py3-none-any.whl (1.7 MB)
Requirement already satisfied: wheel<1.0,>=0.23.0 in /usr/lib/python3/dist-packages (from astunparse>=1.6.0->tensorflow) (0.34.2)
Collecting google-auth-oauthlib<0.5,>=0.4.1
  Using cached google_auth_oauthlib-0.4.6-py2.py3-none-any.whl (18 kB)
Collecting werkzeug>=1.0.1
  Using cached Werkzeug-2.2.2-py3-none-any.whl (232 kB)
Collecting tensorboard-data-server<0.7.0,>=0.6.0
  Using cached tensorboard_data_server-0.6.1-py3-none-manylinux2010_x86_64.whl (4.9 MB)
Collecting markdown>=2.6.8
  Using cached Markdown-3.4.1-py3-none-any.whl (93 kB)
Collecting tensorboard-plugin-wit>=1.6.0
  Using cached tensorboard_plugin_wit-1.8.1-py3-none-any.whl (781 kB)
Collecting google-auth<3,>=1.6.3
  Downloading google_auth-2.16.0-py2.py3-none-any.whl (177 kB)
     |████████████████████████████████| 177 kB 2.5 MB/s
Requirement already satisfied: requests<3,>=2.21.0 in /usr/lib/python3/dist-packages (from tensorboard<2.12,>=2.11->tensorflow) (2.22.0)
Collecting requests-oauthlib>=0.7.0
  Using cached requests_oauthlib-1.3.1-py2.py3-none-any.whl (23 kB)
Collecting MarkupSafe>=2.1.1
  Downloading MarkupSafe-2.1.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (25 kB)
Collecting importlib-metadata>=4.4; python_version < "3.10"
  Downloading importlib_metadata-6.0.0-py3-none-any.whl (21 kB)
Collecting cachetools<6.0,>=2.0.0
  Downloading cachetools-5.2.1-py3-none-any.whl (9.3 kB)
Requirement already satisfied: pyasn1-modules>=0.2.1 in /usr/lib/python3/dist-packages (from google-auth<3,>=1.6.3->tensorboard<2.12,>=2.11->tensorflow) (0.2.1)
Collecting rsa<5,>=3.1.4; python_version >= "3.6"
  Using cached rsa-4.9-py3-none-any.whl (34 kB)
Requirement already satisfied: oauthlib>=3.0.0 in /usr/lib/python3/dist-packages (from requests-oauthlib>=0.7.0->google-auth-oauthlib<0.5,>=0.4.1->tensorboard<2.12,>=2.11->tensorflow) (3.1.0)
Requirement already satisfied: zipp>=0.5 in /usr/lib/python3/dist-packages (from importlib-metadata>=4.4; python_version < "3.10"->markdown>=2.6.8->tensorboard<2.12,>=2.11->tensorflow) (1.0.0)
Requirement already satisfied: pyasn1>=0.1.3 in /usr/lib/python3/dist-packages (from rsa<5,>=3.1.4; python_version >= "3.6"->google-auth<3,>=1.6.3->tensorboard<2.12,>=2.11->tensorflow) (0.4.2)
Installing collected packages: tensorflow-io-gcs-filesystem, grpcio, protobuf, tensorflow-estimator, libclang, astunparse, h5py, requests-oauthlib, cachetools, rsa, google-auth, google-auth-oauthlib, MarkupSafe, werkzeug, tensorboard-data-server, importlib-metadata, markdown, tensorboard-plugin-wit, absl-py, tensorboard, termcolor, wrapt, opt-einsum, google-pasta, flatbuffers, gast, typing-extensions, keras, tensorflow
  WARNING: The scripts pyrsa-decrypt, pyrsa-encrypt, pyrsa-keygen, pyrsa-priv2pub, pyrsa-sign and pyrsa-verify are installed in '/home/yekyaw.thu/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  WARNING: The script google-oauthlib-tool is installed in '/home/yekyaw.thu/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  WARNING: The script markdown_py is installed in '/home/yekyaw.thu/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  WARNING: The script tensorboard is installed in '/home/yekyaw.thu/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  WARNING: The scripts estimator_ckpt_converter, import_pb_to_tensorboard, saved_model_cli, tensorboard, tf_upgrade_v2, tflite_convert, toco and toco_from_protos are installed in '/home/yekyaw.thu/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
Successfully installed MarkupSafe-2.1.1 absl-py-1.4.0 astunparse-1.6.3 cachetools-5.2.1 flatbuffers-23.1.4 gast-0.4.0 google-auth-2.16.0 google-auth-oauthlib-0.4.6 google-pasta-0.2.0 grpcio-1.51.1 h5py-3.7.0 importlib-metadata-6.0.0 keras-2.11.0 libclang-15.0.6.1 markdown-3.4.1 opt-einsum-3.3.0 protobuf-3.19.6 requests-oauthlib-1.3.1 rsa-4.9 tensorboard-2.11.2 tensorboard-data-server-0.6.1 tensorboard-plugin-wit-1.8.1 tensorflow-2.11.0 tensorflow-estimator-2.11.0 tensorflow-io-gcs-filesystem-0.29.0 termcolor-2.2.0 typing-extensions-4.4.0 werkzeug-2.2.2 wrapt-1.14.1
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

## Recreating the Conda Environment with Python3

1st removed the current Conda Env with Python 2.7:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ conda deactivate
(base) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ conda env remove --name sl-mnist

Remove all packages in environment /home/yekyaw.thu/.conda/envs/sl-mnist:

(base) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

creating a new Conda environment with specified Python version ...  

```
(base) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ conda create --name sl-mnist python=3.8
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 22.11.1

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/sl-mnist

  added / updated specs:
    - python=3.8


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    certifi-2022.12.7          |   py38h06a4308_0         150 KB
    libffi-3.4.2               |       h6a678d5_6         136 KB
    python-3.8.15              |       h7a1cb2a_2        20.1 MB
    setuptools-65.6.3          |   py38h06a4308_0         1.1 MB
    sqlite-3.40.1              |       h5082296_0         1.2 MB
    ------------------------------------------------------------
                                           Total:        22.7 MB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-5.1-1_gnu
  ca-certificates    pkgs/main/linux-64::ca-certificates-2022.10.11-h06a4308_0
  certifi            pkgs/main/linux-64::certifi-2022.12.7-py38h06a4308_0
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.38-h1181459_1
  libffi             pkgs/main/linux-64::libffi-3.4.2-h6a678d5_6
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-11.2.0-h1234567_1
  libgomp            pkgs/main/linux-64::libgomp-11.2.0-h1234567_1
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-11.2.0-h1234567_1
  ncurses            pkgs/main/linux-64::ncurses-6.3-h5eee18b_3
  openssl            pkgs/main/linux-64::openssl-1.1.1s-h7f8727e_0
  pip                pkgs/main/linux-64::pip-22.3.1-py38h06a4308_0
  python             pkgs/main/linux-64::python-3.8.15-h7a1cb2a_2
  readline           pkgs/main/linux-64::readline-8.2-h5eee18b_0
  setuptools         pkgs/main/linux-64::setuptools-65.6.3-py38h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.40.1-h5082296_0
  tk                 pkgs/main/linux-64::tk-8.6.12-h1ccaba5_0
  wheel              pkgs/main/noarch::wheel-0.37.1-pyhd3eb1b0_0
  xz                 pkgs/main/linux-64::xz-5.2.8-h5eee18b_0
  zlib               pkgs/main/linux-64::zlib-1.2.13-h5eee18b_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
sqlite-3.40.1        | 1.2 MB    | ############################################################## | 100%
certifi-2022.12.7    | 150 KB    | ############################################################## | 100%
python-3.8.15        | 20.1 MB   | ############################################################## | 100%
libffi-3.4.2         | 136 KB    | ############################################################## | 100%
setuptools-65.6.3    | 1.1 MB    | ############################################################## | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate sl-mnist
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

Entering to the new env:  

```
(base) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ conda activate sl-mnist
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

Check the python version under current environment:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ python --version
Python 3.8.15
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

## Library Installations  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ pip install matplotlib
Requirement already satisfied: matplotlib in /home/yekyaw.thu/.local/lib/python3.8/site-packages (3.6.3)
Requirement already satisfied: contourpy>=1.0.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib) (1.0.7)
Requirement already satisfied: packaging>=20.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib) (23.0)
Requirement already satisfied: kiwisolver>=1.0.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib) (1.4.4)
Collecting pillow>=6.2.0
  Downloading Pillow-9.4.0-cp38-cp38-manylinux_2_28_x86_64.whl (3.4 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.4/3.4 MB 5.1 MB/s eta 0:00:00
Requirement already satisfied: numpy>=1.19 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib) (1.24.1)
Requirement already satisfied: cycler>=0.10 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib) (0.11.0)
Requirement already satisfied: pyparsing>=2.2.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib) (3.0.9)
Requirement already satisfied: fonttools>=4.22.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib) (4.38.0)
Requirement already satisfied: python-dateutil>=2.7 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib) (2.8.2)
Collecting six>=1.5
  Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
Installing collected packages: six, pillow
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
google-auth 2.16.0 requires pyasn1-modules>=0.2.1, which is not installed.
Successfully installed pillow-9.4.0 six-1.16.0
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

Because of the above error message, I installed pyans1-module as follows:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ pip install pyasn1-modules
Collecting pyasn1-modules
  Using cached pyasn1_modules-0.2.8-py2.py3-none-any.whl (155 kB)
Collecting pyasn1<0.5.0,>=0.4.6
  Using cached pyasn1-0.4.8-py2.py3-none-any.whl (77 kB)
Installing collected packages: pyasn1, pyasn1-modules
Successfully installed pyasn1-0.4.8 pyasn1-modules-0.2.8
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

Recheck/reinstall matplotlib ...  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ pip install matplotlib
Requirement already satisfied: matplotlib in /home/yekyaw.thu/.local/lib/python3.8/site-packages (3.6.3)
Requirement already satisfied: cycler>=0.10 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib) (0.11.0)
Requirement already satisfied: contourpy>=1.0.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib) (1.0.7)
Requirement already satisfied: python-dateutil>=2.7 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib) (2.8.2)
Requirement already satisfied: numpy>=1.19 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib) (1.24.1)
Requirement already satisfied: kiwisolver>=1.0.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib) (1.4.4)
Requirement already satisfied: packaging>=20.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib) (23.0)
Requirement already satisfied: fonttools>=4.22.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib) (4.38.0)
Requirement already satisfied: pillow>=6.2.0 in /home/yekyaw.thu/.conda/envs/sl-mnist/lib/python3.8/site-packages (from matplotlib) (9.4.0)
Requirement already satisfied: pyparsing>=2.2.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib) (3.0.9)
Requirement already satisfied: six>=1.5 in /home/yekyaw.thu/.conda/envs/sl-mnist/lib/python3.8/site-packages (from python-dateutil>=2.7->matplotlib) (1.16.0)
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

Installation of seaborn:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ pip install seaborn
Requirement already satisfied: seaborn in /home/yekyaw.thu/.local/lib/python3.8/site-packages (0.12.2)
Requirement already satisfied: pandas>=0.25 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from seaborn) (1.5.2)
Requirement already satisfied: numpy!=1.24.0,>=1.17 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from seaborn) (1.24.1)
Requirement already satisfied: matplotlib!=3.6.1,>=3.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from seaborn) (3.6.3)
Requirement already satisfied: kiwisolver>=1.0.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (1.4.4)
Requirement already satisfied: cycler>=0.10 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (0.11.0)
Requirement already satisfied: contourpy>=1.0.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (1.0.7)
Requirement already satisfied: python-dateutil>=2.7 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (2.8.2)
Requirement already satisfied: packaging>=20.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (23.0)
Requirement already satisfied: fonttools>=4.22.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (4.38.0)
Requirement already satisfied: pyparsing>=2.2.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (3.0.9)
Requirement already satisfied: pillow>=6.2.0 in /home/yekyaw.thu/.conda/envs/sl-mnist/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (9.4.0)
Requirement already satisfied: pytz>=2020.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from pandas>=0.25->seaborn) (2022.7.1)
Requirement already satisfied: six>=1.5 in /home/yekyaw.thu/.conda/envs/sl-mnist/lib/python3.8/site-packages (from python-dateutil>=2.7->matplotlib!=3.6.1,>=3.1->seaborn) (1.16.0)
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

Check the keras ...  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ pip install keras
Requirement already satisfied: keras in /home/yekyaw.thu/.local/lib/python3.8/site-packages (2.11.0)
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

Check/Install Sklearn:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ pip install sklearn
Requirement already satisfied: sklearn in /home/yekyaw.thu/.local/lib/python3.8/site-packages (0.0.post1)
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

Check/Install pandas library ...  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ pip install sklearn
Requirement already satisfied: sklearn in /home/yekyaw.thu/.local/lib/python3.8/site-packages (0.0.post1)
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

Installing the tensorflow framework ...  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ pip install tensorflow
Requirement already satisfied: tensorflow in /home/yekyaw.thu/.local/lib/python3.8/site-packages (2.11.0)
Requirement already satisfied: h5py>=2.9.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (3.7.0)
Requirement already satisfied: keras<2.12,>=2.11.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (2.11.0)
Requirement already satisfied: six>=1.12.0 in /home/yekyaw.thu/.conda/envs/sl-mnist/lib/python3.8/site-packages (from tensorflow) (1.16.0)
Requirement already satisfied: tensorboard<2.12,>=2.11 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (2.11.2)
Requirement already satisfied: protobuf<3.20,>=3.9.2 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (3.19.6)
Requirement already satisfied: wrapt>=1.11.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (1.14.1)
Requirement already satisfied: gast<=0.4.0,>=0.2.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (0.4.0)
Requirement already satisfied: packaging in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (23.0)
Requirement already satisfied: flatbuffers>=2.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (23.1.4)
Requirement already satisfied: tensorflow-estimator<2.12,>=2.11.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (2.11.0)
Requirement already satisfied: libclang>=13.0.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (15.0.6.1)
Requirement already satisfied: setuptools in /home/yekyaw.thu/.conda/envs/sl-mnist/lib/python3.8/site-packages (from tensorflow) (65.6.3)
Requirement already satisfied: astunparse>=1.6.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (1.6.3)
Requirement already satisfied: opt-einsum>=2.3.2 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (3.3.0)
Requirement already satisfied: grpcio<2.0,>=1.24.3 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (1.51.1)
Requirement already satisfied: numpy>=1.20 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (1.24.1)
Requirement already satisfied: termcolor>=1.1.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (2.2.0)
Requirement already satisfied: tensorflow-io-gcs-filesystem>=0.23.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (0.29.0)
Requirement already satisfied: typing-extensions>=3.6.6 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (4.4.0)
Requirement already satisfied: google-pasta>=0.1.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (0.2.0)
Requirement already satisfied: absl-py>=1.0.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorflow) (1.4.0)
Requirement already satisfied: wheel<1.0,>=0.23.0 in /home/yekyaw.thu/.conda/envs/sl-mnist/lib/python3.8/site-packages (from astunparse>=1.6.0->tensorflow) (0.37.1)
Requirement already satisfied: markdown>=2.6.8 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorboard<2.12,>=2.11->tensorflow) (3.4.1)
Requirement already satisfied: google-auth-oauthlib<0.5,>=0.4.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorboard<2.12,>=2.11->tensorflow) (0.4.6)
Requirement already satisfied: werkzeug>=1.0.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorboard<2.12,>=2.11->tensorflow) (2.2.2)
Requirement already satisfied: google-auth<3,>=1.6.3 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorboard<2.12,>=2.11->tensorflow) (2.16.0)
Requirement already satisfied: tensorboard-plugin-wit>=1.6.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorboard<2.12,>=2.11->tensorflow) (1.8.1)
Collecting requests<3,>=2.21.0
  Downloading requests-2.28.2-py3-none-any.whl (62 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 62.8/62.8 kB 339.1 kB/s eta 0:00:00
Requirement already satisfied: tensorboard-data-server<0.7.0,>=0.6.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from tensorboard<2.12,>=2.11->tensorflow) (0.6.1)
Requirement already satisfied: rsa<5,>=3.1.4 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from google-auth<3,>=1.6.3->tensorboard<2.12,>=2.11->tensorflow) (4.9)
Requirement already satisfied: cachetools<6.0,>=2.0.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from google-auth<3,>=1.6.3->tensorboard<2.12,>=2.11->tensorflow) (5.2.1)
Requirement already satisfied: pyasn1-modules>=0.2.1 in /home/yekyaw.thu/.conda/envs/sl-mnist/lib/python3.8/site-packages (from google-auth<3,>=1.6.3->tensorboard<2.12,>=2.11->tensorflow) (0.2.8)
Requirement already satisfied: requests-oauthlib>=0.7.0 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from google-auth-oauthlib<0.5,>=0.4.1->tensorboard<2.12,>=2.11->tensorflow) (1.3.1)
Requirement already satisfied: importlib-metadata>=4.4 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from markdown>=2.6.8->tensorboard<2.12,>=2.11->tensorflow) (6.0.0)
Collecting idna<4,>=2.5
  Using cached idna-3.4-py3-none-any.whl (61 kB)
Requirement already satisfied: certifi>=2017.4.17 in /home/yekyaw.thu/.conda/envs/sl-mnist/lib/python3.8/site-packages (from requests<3,>=2.21.0->tensorboard<2.12,>=2.11->tensorflow) (2022.12.7)
Collecting urllib3<1.27,>=1.21.1
  Downloading urllib3-1.26.14-py2.py3-none-any.whl (140 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 140.6/140.6 kB 900.0 kB/s eta 0:00:00
Collecting charset-normalizer<4,>=2
  Downloading charset_normalizer-3.0.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (195 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 195.4/195.4 kB 2.7 MB/s eta 0:00:00
Requirement already satisfied: MarkupSafe>=2.1.1 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from werkzeug>=1.0.1->tensorboard<2.12,>=2.11->tensorflow) (2.1.1)
Collecting zipp>=0.5
  Downloading zipp-3.11.0-py3-none-any.whl (6.6 kB)
Requirement already satisfied: pyasn1<0.5.0,>=0.4.6 in /home/yekyaw.thu/.conda/envs/sl-mnist/lib/python3.8/site-packages (from pyasn1-modules>=0.2.1->google-auth<3,>=1.6.3->tensorboard<2.12,>=2.11->tensorflow) (0.4.8)
Collecting oauthlib>=3.0.0
  Using cached oauthlib-3.2.2-py3-none-any.whl (151 kB)
Installing collected packages: charset-normalizer, zipp, urllib3, oauthlib, idna, requests
Successfully installed charset-normalizer-3.0.1 idna-3.4 oauthlib-3.2.2 requests-2.28.2 urllib3-1.26.14 zipp-3.11.0
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

## Training CNN Model with SL-MNIST Dataset

I hope for this time, the training program will work ...  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ time python ./model.py | tee train1.log
2023-01-17 17:15:22.521463: I tensorflow/core/platform/cpu_feature_guard.cc:193] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
2023-01-17 17:15:23.131300: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libnvinfer.so.7'; dlerror: libnvinfer.so.7: cannot open shared object file: No such file or directory
2023-01-17 17:15:23.131355: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libnvinfer_plugin.so.7'; dlerror: libnvinfer_plugin.so.7: cannot open shared object file: No such file or directory
2023-01-17 17:15:23.131364: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Cannot dlopen some TensorRT libraries. If you would like to use Nvidia GPU with TensorRT, please make sure the missing libraries mentioned above are installed properly.
Traceback (most recent call last):
  File "./model.py", line 9, in <module>
    from sklearn.model_selection import train_test_split
ModuleNotFoundError: No module named 'sklearn'

real    0m1.933s
user    0m2.071s
sys     0m1.589s
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

Updating the pip library with conda:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ conda install -c anaconda pip
Collecting package metadata (current_repodata.json): done
Solving environment: |
The environment is inconsistent, please check the package plan carefully
The following packages are causing the inconsistency:

  - defaults/linux-64::sqlite==3.40.1=h5082296_0
  - defaults/linux-64::pip==22.3.1=py38h06a4308_0
  - defaults/linux-64::tk==8.6.12=h1ccaba5_0
  - defaults/linux-64::ncurses==6.3=h5eee18b_3
  - defaults/linux-64::zlib==1.2.13=h5eee18b_0
  - defaults/linux-64::libgcc-ng==11.2.0=h1234567_1
  - defaults/linux-64::xz==5.2.8=h5eee18b_0
  - defaults/linux-64::setuptools==65.6.3=py38h06a4308_0
  - defaults/linux-64::certifi==2022.12.7=py38h06a4308_0
  - defaults/linux-64::openssl==1.1.1s=h7f8727e_0
  - defaults/linux-64::readline==8.2=h5eee18b_0
  - defaults/linux-64::libffi==3.4.2=h6a678d5_6
  - defaults/linux-64::python==3.8.15=h7a1cb2a_2
  - defaults/linux-64::libstdcxx-ng==11.2.0=h1234567_1
  - defaults/noarch::wheel==0.37.1=pyhd3eb1b0_0
done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 22.11.1

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/sl-mnist

  added / updated specs:
    - pip


The following packages will be SUPERSEDED by a higher-priority channel:

  ca-certificates    pkgs/main::ca-certificates-2022.10.11~ --> anaconda::ca-certificates-2022.07.19-h06a4308_0


Proceed ([y]/n)? y

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

Installation with specific command as follows:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ python3 -m pip install scikit-learn
Collecting scikit-learn
  Downloading scikit_learn-1.2.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (9.7 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 9.7/9.7 MB 10.2 MB/s eta 0:00:00
Collecting scipy>=1.3.2
  Downloading scipy-1.10.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (34.5 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 34.5/34.5 MB 11.6 MB/s eta 0:00:00
Collecting joblib>=1.1.1
  Using cached joblib-1.2.0-py3-none-any.whl (297 kB)
Collecting threadpoolctl>=2.0.0
  Using cached threadpoolctl-3.1.0-py3-none-any.whl (14 kB)
Requirement already satisfied: numpy>=1.17.3 in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from scikit-learn) (1.24.1)
Installing collected packages: threadpoolctl, scipy, joblib, scikit-learn
Successfully installed joblib-1.2.0 scikit-learn-1.2.0 scipy-1.10.0 threadpoolctl-3.1.0
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

Training again ...  
Now training and check the GPU status ...  

```
(base) yekyaw.thu@gpu:~$ (base) yekyaw.thu@gpu:~$ nvidia-smi
Tue Jan 17 17:28:19 2023
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 470.161.03   Driver Version: 470.161.03   CUDA Version: 11.4     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:0A:00.0 Off |                  N/A |
| 46%   53C    P2    73W / 300W |  10604MiB / 11019MiB |     17%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  NVIDIA GeForce ...  Off  | 00000000:42:00.0 Off |                  N/A |
| 39%   51C    P8    21W / 257W |    332MiB / 11019MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   2  NVIDIA GeForce ...  Off  | 00000000:43:00.0 Off |                  N/A |
| 36%   52C    P8    30W / 250W |    332MiB / 11016MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A    691161      C   python                          10601MiB |
|    1   N/A  N/A    691161      C   python                            329MiB |
|    2   N/A  N/A    691161      C   python                            329MiB |
+-----------------------------------------------------------------------------+
(base) yekyaw.thu@gpu:~$
```

Training log is as follows:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ time python ./model.py | tee train1.log
2023-01-17 17:26:59.920643: I tensorflow/core/platform/cpu_feature_guard.cc:193] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
2023-01-17 17:27:00.521122: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libnvinfer.so.7'; dlerror: libnvinfer.so.7: cannot open shared object file: No such file or directory
2023-01-17 17:27:00.521172: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libnvinfer_plugin.so.7'; dlerror: libnvinfer_plugin.so.7: cannot open shared object file: No such file or directory
2023-01-17 17:27:00.521182: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Cannot dlopen some TensorRT libraries. If you would like to use Nvidia GPU with TensorRT, please make sure the missing libraries mentioned above are installed properly.
2023-01-17 17:27:03.975568: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-17 17:27:03.976268: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-17 17:27:04.036288: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-17 17:27:04.037529: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-17 17:27:04.039544: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-17 17:27:04.040538: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-17 17:27:04.041811: I tensorflow/core/platform/cpu_feature_guard.cc:193] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
2023-01-17 17:27:04.235717: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-17 17:27:04.236416: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-17 17:27:04.237758: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-17 17:27:04.238452: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-17 17:27:04.239778: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-17 17:27:04.240439: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-17 17:27:05.202207: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-17 17:27:05.202931: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-17 17:27:05.204273: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-17 17:27:05.204964: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-17 17:27:05.206241: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1613] Created device /job:localhost/replica:0/task:0/device:GPU:0 with 9637 MB memory:  -> device: 0, name: NVIDIA GeForce RTX 2080 Ti, pci bus id: 0000:0a:00.0, compute capability: 7.5
2023-01-17 17:27:05.206679: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-17 17:27:05.207349: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1613] Created device /job:localhost/replica:0/task:0/device:GPU:1 with 9637 MB memory:  -> device: 1, name: NVIDIA GeForce RTX 2080 Ti, pci bus id: 0000:42:00.0, compute capability: 7.5
2023-01-17 17:27:05.207588: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:981] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2023-01-17 17:27:05.208258: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1613] Created device /job:localhost/replica:0/task:0/device:GPU:2 with 9634 MB memory:  -> device: 2, name: NVIDIA GeForce RTX 2080 Ti, pci bus id: 0000:43:00.0, compute capability: 7.5
Model: "sequential"
_________________________________________________________________
 Layer (type)                Output Shape              Param #
=================================================================
 conv2d (Conv2D)             (None, 28, 28, 75)        750

 batch_normalization (BatchN  (None, 28, 28, 75)       300
 ormalization)

 max_pooling2d (MaxPooling2D  (None, 14, 14, 75)       0
 )

 conv2d_1 (Conv2D)           (None, 14, 14, 50)        33800

 dropout (Dropout)           (None, 14, 14, 50)        0

 batch_normalization_1 (Batc  (None, 14, 14, 50)       200
 hNormalization)

 max_pooling2d_1 (MaxPooling  (None, 7, 7, 50)         0
 2D)

 conv2d_2 (Conv2D)           (None, 7, 7, 25)          11275

 batch_normalization_2 (Batc  (None, 7, 7, 25)         100
 hNormalization)

 max_pooling2d_2 (MaxPooling  (None, 4, 4, 25)         0
 2D)

 flatten (Flatten)           (None, 400)               0

 dense (Dense)               (None, 512)               205312

 dropout_1 (Dropout)         (None, 512)               0

 dense_1 (Dense)             (None, 24)                12312

=================================================================
Total params: 264,049
Trainable params: 263,749
Non-trainable params: 300
_________________________________________________________________
Epoch 1/20
2023-01-17 17:27:06.287942: E tensorflow/core/grappler/optimizers/meta_optimizer.cc:954] layout failed: INVALID_ARGUMENT: Size of values 0 does not match size of permutation 4 @ fanin shape insequential/dropout/dropout/SelectV2-2-TransposeNHWCToNCHW-LayoutOptimizer
2023-01-17 17:27:07.438560: I tensorflow/compiler/xla/stream_executor/cuda/cuda_dnn.cc:428] Loaded cuDNN version 8204
2023-01-17 17:27:08.511631: W tensorflow/compiler/xla/stream_executor/gpu/asm_compiler.cc:115] *** WARNING *** You are using ptxas 10.1.243, which is older than 11.1. ptxas before 11.1 is known to miscompile XLA code, leading to incorrect results or invalid-address errors.

You may not need to update to CUDA 11.1; cherry-picking the ptxas binary is often sufficient.
2023-01-17 17:27:09.742436: I tensorflow/compiler/xla/service/service.cc:173] XLA service 0x7f94848e0030 initialized for platform CUDA (this does not guarantee that XLA will be used). Devices:
2023-01-17 17:27:09.742467: I tensorflow/compiler/xla/service/service.cc:181]   StreamExecutor device (0): NVIDIA GeForce RTX 2080 Ti, Compute Capability 7.5
2023-01-17 17:27:09.742472: I tensorflow/compiler/xla/service/service.cc:181]   StreamExecutor device (1): NVIDIA GeForce RTX 2080 Ti, Compute Capability 7.5
2023-01-17 17:27:09.742476: I tensorflow/compiler/xla/service/service.cc:181]   StreamExecutor device (2): NVIDIA GeForce RTX 2080 Ti, Compute Capability 7.5
2023-01-17 17:27:09.745992: I tensorflow/compiler/mlir/tensorflow/utils/dump_mlir_util.cc:268] disabling MLIR crash reproducer, set env var `MLIR_CRASH_REPRODUCER_DIRECTORY` to enable.
2023-01-17 17:27:09.808758: W tensorflow/compiler/xla/stream_executor/gpu/asm_compiler.cc:115] *** WARNING *** You are using ptxas 10.1.243, which is older than 11.1. ptxas before 11.1 is known to miscompile XLA code, leading to incorrect results or invalid-address errors.

You may not need to update to CUDA 11.1; cherry-picking the ptxas binary is often sufficient.
2023-01-17 17:27:09.848809: I tensorflow/compiler/jit/xla_compilation_cache.cc:477] Compiled cluster using XLA!  This line is logged at most once for the lifetime of the process.
2023-01-17 17:27:09.909103: W tensorflow/compiler/xla/stream_executor/gpu/asm_compiler.cc:115] *** WARNING *** You are using ptxas 10.1.243, which is older than 11.1. ptxas before 11.1 is known to miscompile XLA code, leading to incorrect results or invalid-address errors.

You may not need to update to CUDA 11.1; cherry-picking the ptxas binary is often sufficient.
2023-01-17 17:27:10.068346: W tensorflow/compiler/xla/stream_executor/gpu/asm_compiler.cc:115] *** WARNING *** You are using ptxas 10.1.243, which is older than 11.1. ptxas before 11.1 is known to miscompile XLA code, leading to incorrect results or invalid-address errors.

You may not need to update to CUDA 11.1; cherry-picking the ptxas binary is often sufficient.
2023-01-17 17:27:10.174470: W tensorflow/compiler/xla/stream_executor/gpu/asm_compiler.cc:115] *** WARNING *** You are using ptxas 10.1.243, which is older than 11.1. ptxas before 11.1 is known to miscompile XLA code, leading to incorrect results or invalid-address errors.

You may not need to update to CUDA 11.1; cherry-picking the ptxas binary is often sufficient.
2023-01-17 17:27:10.616927: W tensorflow/compiler/xla/stream_executor/gpu/asm_compiler.cc:115] *** WARNING *** You are using ptxas 10.1.243, which is older than 11.1. ptxas before 11.1 is known to miscompile XLA code, leading to incorrect results or invalid-address errors.

You may not need to update to CUDA 11.1; cherry-picking the ptxas binary is often sufficient.
2023-01-17 17:27:10.776867: W tensorflow/compiler/xla/stream_executor/gpu/asm_compiler.cc:115] *** WARNING *** You are using ptxas 10.1.243, which is older than 11.1. ptxas before 11.1 is known to miscompile XLA code, leading to incorrect results or invalid-address errors.

You may not need to update to CUDA 11.1; cherry-picking the ptxas binary is often sufficient.
2023-01-17 17:27:10.963754: W tensorflow/compiler/xla/stream_executor/gpu/asm_compiler.cc:115] *** WARNING *** You are using ptxas 10.1.243, which is older than 11.1. ptxas before 11.1 is known to miscompile XLA code, leading to incorrect results or invalid-address errors.

You may not need to update to CUDA 11.1; cherry-picking the ptxas binary is often sufficient.
2023-01-17 17:27:11.122934: W tensorflow/compiler/xla/stream_executor/gpu/asm_compiler.cc:115] *** WARNING *** You are using ptxas 10.1.243, which is older than 11.1. ptxas before 11.1 is known to miscompile XLA code, leading to incorrect results or invalid-address errors.

You may not need to update to CUDA 11.1; cherry-picking the ptxas binary is often sufficient.
2023-01-17 17:27:11.299162: W tensorflow/compiler/xla/stream_executor/gpu/asm_compiler.cc:115] *** WARNING *** You are using ptxas 10.1.243, which is older than 11.1. ptxas before 11.1 is known to miscompile XLA code, leading to incorrect results or invalid-address errors.

You may not need to update to CUDA 11.1; cherry-picking the ptxas binary is often sufficient.
215/215 [==============================] - 12s 28ms/step - loss: 1.0641 - accuracy: 0.6691 - val_loss: 3.4412 - val_accuracy: 0.1789 - lr: 0.0010
Epoch 2/20
215/215 [==============================] - 6s 26ms/step - loss: 0.2056 - accuracy: 0.9319 - val_loss: 1.5670 - val_accuracy: 0.5618 - lr: 0.0010
Epoch 3/20
215/215 [==============================] - 6s 26ms/step - loss: 0.0984 - accuracy: 0.9672 - val_loss: 0.1545 - val_accuracy: 0.9441 - lr: 0.0010
Epoch 4/20
215/215 [==============================] - 6s 26ms/step - loss: 0.0619 - accuracy: 0.9808 - val_loss: 0.0464 - val_accuracy: 0.9884 - lr: 0.0010
Epoch 5/20
215/215 [==============================] - 6s 26ms/step - loss: 0.0423 - accuracy: 0.9867 - val_loss: 0.0735 - val_accuracy: 0.9731 - lr: 0.0010
Epoch 6/20
214/215 [============================>.] - ETA: 0s - loss: 0.0379 - accuracy: 0.9885
Epoch 6: ReduceLROnPlateau reducing learning rate to 0.0005000000237487257.
215/215 [==============================] - 6s 27ms/step - loss: 0.0378 - accuracy: 0.9886 - val_loss: 0.1312 - val_accuracy: 0.9495 - lr: 0.0010
Epoch 7/20
215/215 [==============================] - 6s 26ms/step - loss: 0.0219 - accuracy: 0.9930 - val_loss: 0.0175 - val_accuracy: 0.9929 - lr: 5.0000e-04
Epoch 8/20
215/215 [==============================] - 6s 26ms/step - loss: 0.0164 - accuracy: 0.9954 - val_loss: 0.0049 - val_accuracy: 0.9992 - lr: 5.0000e-04
Epoch 9/20
215/215 [==============================] - 6s 26ms/step - loss: 0.0137 - accuracy: 0.9956 - val_loss: 0.0044 - val_accuracy: 0.9993 - lr: 5.0000e-04
Epoch 10/20
215/215 [==============================] - 6s 26ms/step - loss: 0.0132 - accuracy: 0.9959 - val_loss: 0.0271 - val_accuracy: 0.9881 - lr: 5.0000e-04
Epoch 11/20
214/215 [============================>.] - ETA: 0s - loss: 0.0127 - accuracy: 0.9962
Epoch 11: ReduceLROnPlateau reducing learning rate to 0.0002500000118743628.
215/215 [==============================] - 6s 26ms/step - loss: 0.0126 - accuracy: 0.9962 - val_loss: 0.0227 - val_accuracy: 0.9943 - lr: 5.0000e-04
Epoch 12/20
215/215 [==============================] - 6s 26ms/step - loss: 0.0096 - accuracy: 0.9972 - val_loss: 0.0129 - val_accuracy: 0.9939 - lr: 2.5000e-04
Epoch 13/20
215/215 [==============================] - ETA: 0s - loss: 0.0083 - accuracy: 0.9975
Epoch 13: ReduceLROnPlateau reducing learning rate to 0.0001250000059371814.
215/215 [==============================] - 5s 25ms/step - loss: 0.0083 - accuracy: 0.9975 - val_loss: 0.0047 - val_accuracy: 0.9993 - lr: 2.5000e-04
Epoch 14/20
215/215 [==============================] - 6s 26ms/step - loss: 0.0063 - accuracy: 0.9985 - val_loss: 0.0030 - val_accuracy: 0.9996 - lr: 1.2500e-04
Epoch 15/20
215/215 [==============================] - 6s 26ms/step - loss: 0.0067 - accuracy: 0.9982 - val_loss: 0.0010 - val_accuracy: 1.0000 - lr: 1.2500e-04
Epoch 16/20
215/215 [==============================] - 6s 26ms/step - loss: 0.0061 - accuracy: 0.9983 - val_loss: 0.0010 - val_accuracy: 1.0000 - lr: 1.2500e-04
Epoch 17/20
214/215 [============================>.] - ETA: 0s - loss: 0.0050 - accuracy: 0.9986
Epoch 17: ReduceLROnPlateau reducing learning rate to 6.25000029685907e-05.
215/215 [==============================] - 5s 25ms/step - loss: 0.0050 - accuracy: 0.9986 - val_loss: 0.0055 - val_accuracy: 0.9983 - lr: 1.2500e-04
Epoch 18/20
215/215 [==============================] - 6s 26ms/step - loss: 0.0044 - accuracy: 0.9989 - val_loss: 0.0012 - val_accuracy: 1.0000 - lr: 6.2500e-05
Epoch 19/20
215/215 [==============================] - ETA: 0s - loss: 0.0042 - accuracy: 0.9991
Epoch 19: ReduceLROnPlateau reducing learning rate to 3.125000148429535e-05.
215/215 [==============================] - 6s 26ms/step - loss: 0.0042 - accuracy: 0.9991 - val_loss: 0.0014 - val_accuracy: 1.0000 - lr: 6.2500e-05
Epoch 20/20
215/215 [==============================] - 6s 26ms/step - loss: 0.0042 - accuracy: 0.9989 - val_loss: 0.0013 - val_accuracy: 1.0000 - lr: 3.1250e-05

real    2m7.374s
user    2m37.461s
sys     0m9.880s
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

Check the output model:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ ls
camerahands.py  model.py  README.md  sign_mnist_test.csv  sign_mnist_train.csv  smnist.h5  train1.log
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ wc smnist.h5
  10114   58513 3244748 smnist.h5
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$ ls -lh ./smnist.h5
-rw-r--r-- 1 yekyaw.thu domain users 3.1M Jan 17 17:29 ./smnist.h5
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/Sign-Language-Detection$
```

## Preparing for Online Testing

I wanna try on Windows OS and thus I installed Anaconda on my Windows machine and then work under Anaconda Terminal.  

```
(base) C:\Users\801680>mkdir exp
(base) C:\Users\801680>cd exp
(base) C:\Users\801680\exp>
```

Prepare camerahands.py source code ...  

```
(base) C:\Users\801680\exp>move ..\Downloads\camerahands.py .
        1 file(s) moved.
(base) C:\Users\801680\exp>
```

Crearing a new conda environment ...  

```
(base) C:\Users\801680\exp>conda create --name sl-mnist python=3.8
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 22.9.0
  latest version: 22.11.1

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: C:\Users\801680\Anaconda3\envs\sl-mnist

  added / updated specs:
    - python=3.8


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    ca-certificates-2022.10.11 |       haa95532_0         125 KB
    certifi-2022.12.7          |   py38haa95532_0         148 KB
    libffi-3.4.2               |       hd77b12b_6         109 KB
    openssl-1.1.1s             |       h2bbff1b_0         5.5 MB
    pip-22.3.1                 |   py38haa95532_0         2.7 MB
    python-3.8.15              |       h6244533_2        18.9 MB
    setuptools-65.6.3          |   py38haa95532_0         1.1 MB
    sqlite-3.40.1              |       h2bbff1b_0         889 KB
    wincertstore-0.2           |   py38haa95532_2          15 KB
    ------------------------------------------------------------
                                           Total:        29.5 MB

The following NEW packages will be INSTALLED:

  ca-certificates    pkgs/main/win-64::ca-certificates-2022.10.11-haa95532_0 None
  certifi            pkgs/main/win-64::certifi-2022.12.7-py38haa95532_0 None
  libffi             pkgs/main/win-64::libffi-3.4.2-hd77b12b_6 None
  openssl            pkgs/main/win-64::openssl-1.1.1s-h2bbff1b_0 None
  pip                pkgs/main/win-64::pip-22.3.1-py38haa95532_0 None
  python             pkgs/main/win-64::python-3.8.15-h6244533_2 None
  setuptools         pkgs/main/win-64::setuptools-65.6.3-py38haa95532_0 None
  sqlite             pkgs/main/win-64::sqlite-3.40.1-h2bbff1b_0 None
  vc                 pkgs/main/win-64::vc-14.2-h21ff451_1 None
  vs2015_runtime     pkgs/main/win-64::vs2015_runtime-14.27.29016-h5e58377_2 None
  wheel              pkgs/main/noarch::wheel-0.37.1-pyhd3eb1b0_0 None
  wincertstore       pkgs/main/win-64::wincertstore-0.2-py38haa95532_2 None


Proceed ([y]/n)? y


Downloading and Extracting Packages
wincertstore-0.2     | 15 KB     | ############################################################################ | 100%
openssl-1.1.1s       | 5.5 MB    | ############################################################################ | 100%
libffi-3.4.2         | 109 KB    | ############################################################################ | 100%
sqlite-3.40.1        | 889 KB    | ############################################################################ | 100%
certifi-2022.12.7    | 148 KB    | ############################################################################ | 100%
setuptools-65.6.3    | 1.1 MB    | ############################################################################ | 100%
pip-22.3.1           | 2.7 MB    | ############################################################################ | 100%
ca-certificates-2022 | 125 KB    | ############################################################################ | 100%
python-3.8.15        | 18.9 MB   | ############################################################################ | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate sl-mnist
#
# To deactivate an active environment, use
#
#     $ conda deactivate

Retrieving notices: ...working... done

(base) C:\Users\801680\exp>conda activate sl-mnist

(sl-mnist) C:\Users\801680\exp>
```

Installation of tensorflow-cpu ...  

```
(sl-mnist) C:\Users\801680\exp>pip install tensorflow-cpu
Collecting tensorflow-cpu
  Downloading tensorflow_cpu-2.11.0-cp38-cp38-win_amd64.whl (1.9 kB)
Collecting tensorflow-intel==2.11.0
  Downloading tensorflow_intel-2.11.0-cp38-cp38-win_amd64.whl (266.3 MB)
     ---------------------------------------- 266.3/266.3 MB 2.2 MB/s eta 0:00:00
Collecting typing-extensions>=3.6.6
  Downloading typing_extensions-4.4.0-py3-none-any.whl (26 kB)
Collecting protobuf<3.20,>=3.9.2
  Downloading protobuf-3.19.6-cp38-cp38-win_amd64.whl (896 kB)
     ---------------------------------------- 896.1/896.1 kB 7.1 MB/s eta 0:00:00
Collecting gast<=0.4.0,>=0.2.1
  Downloading gast-0.4.0-py3-none-any.whl (9.8 kB)
Collecting tensorboard<2.12,>=2.11
  Downloading tensorboard-2.11.2-py3-none-any.whl (6.0 MB)
     ---------------------------------------- 6.0/6.0 MB 3.0 MB/s eta 0:00:00
Collecting numpy>=1.20
  Downloading numpy-1.24.1-cp38-cp38-win_amd64.whl (14.9 MB)
     ---------------------------------------- 14.9/14.9 MB 1.5 MB/s eta 0:00:00
Collecting packaging
  Downloading packaging-23.0-py3-none-any.whl (42 kB)
     ---------------------------------------- 42.7/42.7 kB ? eta 0:00:00
Collecting grpcio<2.0,>=1.24.3
  Downloading grpcio-1.51.1-cp38-cp38-win_amd64.whl (3.7 MB)
     ---------------------------------------- 3.7/3.7 MB 3.5 MB/s eta 0:00:00
Collecting opt-einsum>=2.3.2
  Downloading opt_einsum-3.3.0-py3-none-any.whl (65 kB)
     ---------------------------------------- 65.5/65.5 kB 3.7 MB/s eta 0:00:00
Collecting google-pasta>=0.1.1
  Downloading google_pasta-0.2.0-py3-none-any.whl (57 kB)
     ---------------------------------------- 57.5/57.5 kB 3.1 MB/s eta 0:00:00
Collecting astunparse>=1.6.0
  Downloading astunparse-1.6.3-py2.py3-none-any.whl (12 kB)
Collecting keras<2.12,>=2.11.0
  Downloading keras-2.11.0-py2.py3-none-any.whl (1.7 MB)
     ---------------------------------------- 1.7/1.7 MB 4.5 MB/s eta 0:00:00
Collecting termcolor>=1.1.0
  Downloading termcolor-2.2.0-py3-none-any.whl (6.6 kB)
Collecting libclang>=13.0.0
  Downloading libclang-15.0.6.1-py2.py3-none-win_amd64.whl (23.2 MB)
     ---------------------------------------- 23.2/23.2 MB 2.5 MB/s eta 0:00:00
Requirement already satisfied: setuptools in c:\users\801680\anaconda3\envs\sl-mnist\lib\site-packages (from tensorflow-intel==2.11.0->tensorflow-cpu) (65.6.3)
Collecting h5py>=2.9.0
  Downloading h5py-3.7.0-cp38-cp38-win_amd64.whl (2.6 MB)
     ---------------------------------------- 2.6/2.6 MB 3.2 MB/s eta 0:00:00
Collecting six>=1.12.0
  Downloading six-1.16.0-py2.py3-none-any.whl (11 kB)
Collecting tensorflow-estimator<2.12,>=2.11.0
  Downloading tensorflow_estimator-2.11.0-py2.py3-none-any.whl (439 kB)
     ---------------------------------------- 439.2/439.2 kB 5.5 MB/s eta 0:00:00
Collecting wrapt>=1.11.0
  Downloading wrapt-1.14.1-cp38-cp38-win_amd64.whl (35 kB)
Collecting flatbuffers>=2.0
  Downloading flatbuffers-23.1.4-py2.py3-none-any.whl (26 kB)
Collecting tensorflow-io-gcs-filesystem>=0.23.1
  Downloading tensorflow_io_gcs_filesystem-0.29.0-cp38-cp38-win_amd64.whl (1.5 MB)
     ---------------------------------------- 1.5/1.5 MB 5.5 MB/s eta 0:00:00
Collecting absl-py>=1.0.0
  Downloading absl_py-1.4.0-py3-none-any.whl (126 kB)
     ---------------------------------------- 126.5/126.5 kB ? eta 0:00:00
Requirement already satisfied: wheel<1.0,>=0.23.0 in c:\users\801680\anaconda3\envs\sl-mnist\lib\site-packages (from astunparse>=1.6.0->tensorflow-intel==2.11.0->tensorflow-cpu) (0.37.1)
Collecting requests<3,>=2.21.0
  Downloading requests-2.28.2-py3-none-any.whl (62 kB)
     ---------------------------------------- 62.8/62.8 kB 3.5 MB/s eta 0:00:00
Collecting google-auth-oauthlib<0.5,>=0.4.1
  Downloading google_auth_oauthlib-0.4.6-py2.py3-none-any.whl (18 kB)
Collecting tensorboard-data-server<0.7.0,>=0.6.0
  Downloading tensorboard_data_server-0.6.1-py3-none-any.whl (2.4 kB)
Collecting markdown>=2.6.8
  Downloading Markdown-3.4.1-py3-none-any.whl (93 kB)
     ---------------------------------------- 93.3/93.3 kB 5.5 MB/s eta 0:00:00
Collecting google-auth<3,>=1.6.3
  Downloading google_auth-2.16.0-py2.py3-none-any.whl (177 kB)
     ---------------------------------------- 177.8/177.8 kB 5.4 MB/s eta 0:00:00
Collecting werkzeug>=1.0.1
  Downloading Werkzeug-2.2.2-py3-none-any.whl (232 kB)
     ---------------------------------------- 232.7/232.7 kB 7.2 MB/s eta 0:00:00
Collecting tensorboard-plugin-wit>=1.6.0
  Downloading tensorboard_plugin_wit-1.8.1-py3-none-any.whl (781 kB)
     ---------------------------------------- 781.3/781.3 kB 5.5 MB/s eta 0:00:00
Collecting cachetools<6.0,>=2.0.0
  Downloading cachetools-5.2.1-py3-none-any.whl (9.3 kB)
Collecting rsa<5,>=3.1.4
  Downloading rsa-4.9-py3-none-any.whl (34 kB)
Collecting pyasn1-modules>=0.2.1
  Downloading pyasn1_modules-0.2.8-py2.py3-none-any.whl (155 kB)
     ---------------------------------------- 155.3/155.3 kB 1.0 MB/s eta 0:00:00
Collecting requests-oauthlib>=0.7.0
  Downloading requests_oauthlib-1.3.1-py2.py3-none-any.whl (23 kB)
Collecting importlib-metadata>=4.4
  Downloading importlib_metadata-6.0.0-py3-none-any.whl (21 kB)
Collecting charset-normalizer<4,>=2
  Downloading charset_normalizer-3.0.1-cp38-cp38-win_amd64.whl (95 kB)
     ---------------------------------------- 95.8/95.8 kB 5.3 MB/s eta 0:00:00
Collecting idna<4,>=2.5
  Downloading idna-3.4-py3-none-any.whl (61 kB)
     ---------------------------------------- 61.5/61.5 kB ? eta 0:00:00
Collecting urllib3<1.27,>=1.21.1
  Downloading urllib3-1.26.14-py2.py3-none-any.whl (140 kB)
     ---------------------------------------- 140.6/140.6 kB 4.2 MB/s eta 0:00:00
Requirement already satisfied: certifi>=2017.4.17 in c:\users\801680\anaconda3\envs\sl-mnist\lib\site-packages (from requests<3,>=2.21.0->tensorboard<2.12,>=2.11->tensorflow-intel==2.11.0->tensorflow-cpu) (2022.12.7)
Collecting MarkupSafe>=2.1.1
  Downloading MarkupSafe-2.1.1-cp38-cp38-win_amd64.whl (17 kB)
Collecting zipp>=0.5
  Downloading zipp-3.11.0-py3-none-any.whl (6.6 kB)
Collecting pyasn1<0.5.0,>=0.4.6
  Downloading pyasn1-0.4.8-py2.py3-none-any.whl (77 kB)
     ---------------------------------------- 77.1/77.1 kB 285.9 kB/s eta 0:00:00
Collecting oauthlib>=3.0.0
  Downloading oauthlib-3.2.2-py3-none-any.whl (151 kB)
     ---------------------------------------- 151.7/151.7 kB 1.5 MB/s eta 0:00:00
Installing collected packages: tensorboard-plugin-wit, pyasn1, libclang, flatbuffers, charset-normalizer, zipp, wrapt, urllib3, typing-extensions, termcolor, tensorflow-io-gcs-filesystem, tensorflow-estimator, tensorboard-data-server, six, rsa, pyasn1-modules, protobuf, packaging, oauthlib, numpy, MarkupSafe, keras, idna, grpcio, gast, cachetools, absl-py, werkzeug, requests, opt-einsum, importlib-metadata, h5py, google-pasta, google-auth, astunparse, requests-oauthlib, markdown, google-auth-oauthlib, tensorboard, tensorflow-intel, tensorflow-cpu
Successfully installed MarkupSafe-2.1.1 absl-py-1.4.0 astunparse-1.6.3 cachetools-5.2.1 charset-normalizer-3.0.1 flatbuffers-23.1.4 gast-0.4.0 google-auth-2.16.0 google-auth-oauthlib-0.4.6 google-pasta-0.2.0 grpcio-1.51.1 h5py-3.7.0 idna-3.4 importlib-metadata-6.0.0 keras-2.11.0 libclang-15.0.6.1 markdown-3.4.1 numpy-1.24.1 oauthlib-3.2.2 opt-einsum-3.3.0 packaging-23.0 protobuf-3.19.6 pyasn1-0.4.8 pyasn1-modules-0.2.8 requests-2.28.2 requests-oauthlib-1.3.1 rsa-4.9 six-1.16.0 tensorboard-2.11.2 tensorboard-data-server-0.6.1 tensorboard-plugin-wit-1.8.1 tensorflow-cpu-2.11.0 tensorflow-estimator-2.11.0 tensorflow-intel-2.11.0 tensorflow-io-gcs-filesystem-0.29.0 termcolor-2.2.0 typing-extensions-4.4.0 urllib3-1.26.14 werkzeug-2.2.2 wrapt-1.14.1 zipp-3.11.0

(sl-mnist) C:\Users\801680\exp>
```

Installing cv2 ...  

```
(sl-mnist) C:\Users\801680\exp>pip install opencv-python
Collecting opencv-python
  Downloading opencv_python-4.7.0.68-cp37-abi3-win_amd64.whl (38.2 MB)
     ---------------------------------------- 38.2/38.2 MB 2.5 MB/s eta 0:00:00
Requirement already satisfied: numpy>=1.17.0 in c:\users\801680\anaconda3\envs\sl-mnist\lib\site-packages (from opencv-python) (1.24.1)
Installing collected packages: opencv-python
Successfully installed opencv-python-4.7.0.68
```

check cv2 library by module loading ...  

```
(sl-mnist) C:\Users\801680\exp>python
Python 3.8.15 (default, Nov 24 2022, 14:38:14) [MSC v.1916 64 bit (AMD64)] :: Anaconda, Inc. on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> import cv2
>>> print(cv2.__version__)
4.7.0
>>> exit()

(sl-mnist) C:\Users\801680\exp>
```

It looks OK.  
Installation of the mediapipe library ...  

```
(sl-mnist) C:\Users\801680\exp>pip install mediapipe
Collecting mediapipe
  Downloading mediapipe-0.9.0.1-cp38-cp38-win_amd64.whl (49.8 MB)
     ---------------------------------------- 49.8/49.8 MB 2.5 MB/s eta 0:00:00
Requirement already satisfied: absl-py in c:\users\801680\anaconda3\envs\sl-mnist\lib\site-packages (from mediapipe) (1.4.0)
Collecting opencv-contrib-python
  Downloading opencv_contrib_python-4.7.0.68-cp37-abi3-win_amd64.whl (44.9 MB)
     ---------------------------------------- 44.9/44.9 MB 2.5 MB/s eta 0:00:00
Requirement already satisfied: protobuf<4,>=3.11 in c:\users\801680\anaconda3\envs\sl-mnist\lib\site-packages (from mediapipe) (3.19.6)
Requirement already satisfied: numpy in c:\users\801680\anaconda3\envs\sl-mnist\lib\site-packages (from mediapipe) (1.24.1)
Collecting matplotlib
  Downloading matplotlib-3.6.3-cp38-cp38-win_amd64.whl (7.2 MB)
     ---------------------------------------- 7.2/7.2 MB 2.8 MB/s eta 0:00:00
Collecting attrs>=19.1.0
  Downloading attrs-22.2.0-py3-none-any.whl (60 kB)
     ---------------------------------------- 60.0/60.0 kB 3.1 MB/s eta 0:00:00
Requirement already satisfied: flatbuffers>=2.0 in c:\users\801680\anaconda3\envs\sl-mnist\lib\site-packages (from mediapipe) (23.1.4)
Collecting contourpy>=1.0.1
  Downloading contourpy-1.0.7-cp38-cp38-win_amd64.whl (162 kB)
     ---------------------------------------- 163.0/163.0 kB ? eta 0:00:00
Collecting cycler>=0.10
  Downloading cycler-0.11.0-py3-none-any.whl (6.4 kB)
Collecting python-dateutil>=2.7
  Downloading python_dateutil-2.8.2-py2.py3-none-any.whl (247 kB)
     ---------------------------------------- 247.7/247.7 kB 15.8 MB/s eta 0:00:00
Requirement already satisfied: packaging>=20.0 in c:\users\801680\anaconda3\envs\sl-mnist\lib\site-packages (from matplotlib->mediapipe) (23.0)
Collecting kiwisolver>=1.0.1
  Downloading kiwisolver-1.4.4-cp38-cp38-win_amd64.whl (55 kB)
     ---------------------------------------- 55.4/55.4 kB ? eta 0:00:00
Collecting pyparsing>=2.2.1
  Downloading pyparsing-3.0.9-py3-none-any.whl (98 kB)
     ---------------------------------------- 98.3/98.3 kB ? eta 0:00:00
Collecting pillow>=6.2.0
  Downloading Pillow-9.4.0-cp38-cp38-win_amd64.whl (2.5 MB)
     ---------------------------------------- 2.5/2.5 MB 4.1 MB/s eta 0:00:00
Collecting fonttools>=4.22.0
  Downloading fonttools-4.38.0-py3-none-any.whl (965 kB)
     ---------------------------------------- 965.4/965.4 kB 4.4 MB/s eta 0:00:00
Requirement already satisfied: six>=1.5 in c:\users\801680\anaconda3\envs\sl-mnist\lib\site-packages (from python-dateutil>=2.7->matplotlib->mediapipe) (1.16.0)
Installing collected packages: python-dateutil, pyparsing, pillow, opencv-contrib-python, kiwisolver, fonttools, cycler, contourpy, attrs, matplotlib, mediapipe
Successfully installed attrs-22.2.0 contourpy-1.0.7 cycler-0.11.0 fonttools-4.38.0 kiwisolver-1.4.4 matplotlib-3.6.3 mediapipe-0.9.0.1 opencv-contrib-python-4.7.0.68 pillow-9.4.0 pyparsing-3.0.9 python-dateutil-2.8.2

(sl-mnist) C:\Users\801680\exp>
```

check for keras and numpy  ...  

```
(sl-mnist) C:\Users\801680\exp>pip install keras
Requirement already satisfied: keras in c:\users\801680\anaconda3\envs\sl-mnist\lib\site-packages (2.11.0)

(sl-mnist) C:\Users\801680\exp>pip install numpy
Requirement already satisfied: numpy in c:\users\801680\anaconda3\envs\sl-mnist\lib\site-packages (1.24.1)

(sl-mnist) C:\Users\801680\exp>
```

Pandas library installation ...  

```
(sl-mnist) C:\Users\801680\exp>pip install pandas
Collecting pandas
  Downloading pandas-1.5.2-cp38-cp38-win_amd64.whl (11.0 MB)
     ---------------------------------------- 11.0/11.0 MB 2.7 MB/s eta 0:00:00
Requirement already satisfied: numpy>=1.20.3 in c:\users\801680\anaconda3\envs\sl-mnist\lib\site-packages (from pandas) (1.24.1)
Requirement already satisfied: python-dateutil>=2.8.1 in c:\users\801680\anaconda3\envs\sl-mnist\lib\site-packages (from pandas) (2.8.2)
Collecting pytz>=2020.1
  Downloading pytz-2022.7.1-py2.py3-none-any.whl (499 kB)
     ---------------------------------------- 499.4/499.4 kB 5.2 MB/s eta 0:00:00
Requirement already satisfied: six>=1.5 in c:\users\801680\anaconda3\envs\sl-mnist\lib\site-packages (from python-dateutil>=2.8.1->pandas) (1.16.0)
Installing collected packages: pytz, pandas
Successfully installed pandas-1.5.2 pytz-2022.7.1

(sl-mnist) C:\Users\801680\exp>
```

Copied trained CNN model to the local path:  

```
scp -P xxxx -i C:\Users\801680\.ssh\id_rsa-for-cadt-gpu-server yekyaw.thu@103.16.63.233:/home/yekyaw.thu//exp/sl-mnist/Sign-Language-Detection/smnist.h5 .
```

Check the current path ...  

```
(sl-mnist) C:\Users\801680\exp>dir
 Volume in drive C has no label.
 Volume Serial Number is 9C54-A208

 Directory of C:\Users\801680\exp

01/17/2023  07:17 PM    <DIR>          .
01/17/2023  07:17 PM    <DIR>          ..
01/17/2023  06:53 PM             4,296 camerahands.py
01/17/2023  07:17 PM         3,244,748 smnist.h5
               2 File(s)      3,249,044 bytes
               2 Dir(s)  75,203,239,936 bytes free

(sl-mnist) C:\Users\801680\exp>
```

## Online Testing 

```
(sl-mnist) C:\Users\801680\exp>python camerahands.py
INFO: Created TensorFlow Lite XNNPACK delegate for CPU.
Escape hit, closing...

(sl-mnist) C:\Users\801680\exp>
```

If you want to quit, press "Escape" key.  
For the image classification, press "Space bar".  
Testing with American SL output are as follows:  

```
(base) C:\Users\801680\exp>conda activate sl-mnist

(sl-mnist) C:\Users\801680\exp>python ./camerahands.py
INFO: Created TensorFlow Lite XNNPACK delegate for CPU.
1/1 [==============================] - 0s 119ms/step
Predicted Character 3:  B
Confidence 3:  0.004512211307883263
Predicted Character 2:  H
Confidence 2:  5.307730287313461
Predicted Character 1:  P
Confidence 1:  94.68284845352173
1/1 [==============================] - 0s 15ms/step
Predicted Character 1:  B
Confidence 1:  49.81687664985657
Predicted Character 2:  F
Confidence 2:  42.01692044734955
Predicted Character 3:  P
Confidence 3:  5.600017681717873
1/1 [==============================] - 0s 15ms/step
Predicted Character 1:  H
Confidence 1:  99.98621940612793
Predicted Character 2:  P
Confidence 2:  0.013711376232095063
Predicted Character 3:  Q
Confidence 3:  6.605231419598567e-05
1/1 [==============================] - 0s 17ms/step
Predicted Character 3:  G
Confidence 3:  27.6007741689682
Predicted Character 2:  H
Confidence 2:  29.149499535560608
Predicted Character 1:  P
Confidence 1:  40.616557002067566
1/1 [==============================] - 0s 15ms/step
Predicted Character 3:  B
Confidence 3:  1.3087017461657524
Predicted Character 1:  H
Confidence 1:  71.47443294525146
Predicted Character 2:  P
Confidence 2:  26.61367654800415
1/1 [==============================] - 0s 16ms/step
Predicted Character 2:  H
Confidence 2:  1.3375685550272465
Predicted Character 3:  L
Confidence 3:  0.05046534934081137
Predicted Character 1:  P
Confidence 1:  98.56514930725098
Escape hit, closing...

(sl-mnist) C:\Users\801680\exp>
```

For your reference:  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/sl-sw/b.png" alt="ASL online testing from Windows OS local machine" width="800"/>  
</p>  
<div align="center">
  Fig. An example of ASL online testing from Windows OS local machine (signing of ASL "B" fingerspelling character)  
</div> 

<br />

You can also get the code from [https://github.com/mg343/Sign-Language-Detection/blob/main/camerahands.py](https://github.com/mg343/Sign-Language-Detection/blob/main/camerahands.py)  
Students must study on following online testing code for your experiments:  

```python
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
cv2.destroyAllWindows()
```

## To Do

[1] testing for Khmer Fingerspelling  
[2] testing for Myanmar Fingerspelling  
[3] teaching formal evaluation procedures  

## Reference

[1] https://github.com/mg343/Sign-Language-Detection  
[2] https://www.kaggle.com/datasets/datamunge/sign-language-mnist?resource=download
