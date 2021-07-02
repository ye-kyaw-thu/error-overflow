# git lfs Installation and Usage

git, github ကို သုံးပြီးတော့ ကိုယ် develop လုပ်ထားတဲ့ source code, data တွေကို upload လုပ်တဲ့အခါမှာ filesize က 50 mb ကျော်လာတဲ့အခါမှာ ပုံမှန်အတိုင်း git push လုပ်တာမျိုး လုပ်လို့ မရပါဘူး။ ထိုနည်းလည်းကောင်းပဲ browser ကနေလည်း upload ပေးမလုပ်ပါဘူး။ အကြောင်းအရင်းကတော့ git ဆိုတာက သိကြတဲ့အတိုင်း version control system ဖြစ်ပြီး developer တွေအများကြီးနဲ့ system တစ်ခုကို framework တစ်ခုကို အတူတူ develop လုပ်ကြရတာမို့ ဖိုင်အရွယ်အစားတွေက ကြီးလာတဲ့အခါမှာ push, pull တစ်ယောက်ချင်းစီက လုပ်ကြတဲ့အခါမှာ download/upload တွေကြောင့် git repository ကို up-to-date လုပ်တဲ့အခါမှာ လေးကုန်တာတို့လိုမျိုး ပြဿနာတွေ ဖြစ်တတ်တာမို့ပါ။  

အဲဒီအတွက် solution တစ်ခုက git lfs ကို သုံးပြီး filesize ကြီးတဲ့ ဖိုင်တွေကို compress လုပ်ပြီးမှ လိုအပ်တဲ့အခါမှသာ local နဲ့ remote repository အကြားမှာ အပြောင်းအလဲ လုပ်တဲ့ပုံစံပါ။  

myPOS version 3.0 မှာ NCRF++ model တွေပါတော့ အဲဒီထဲက ".dset" နဲ့ ဆုံးတဲ့ ဖိုင်တွေက ဖိုင်ဆိုက်ကြီးတာမို့ git lfs ကို သုံးပြီး github ပေါ်ကို တင်ဖြစ်ခဲ့လို့ practical git lfs usage ဥပမာကောင်းမို့လို့ error-overflow မှာ log ဖိုင်ကို တင်ပေးထားလိုက်ပါတယ်။  

## Download git lfs


Download link: https://git-lfs.github.com/

## Move tar.gz File

After you download the git-ltfs...
Move tar.gz file to your installation path...

```
mkdir git-lfs (under your installation path)
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/git-lfs/$ mv ~/Downloads/git-lfs-linux-amd64-v2.13.3.tar.gz .
```

## Unzip tar.gz file

Unzipping...

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/git-lfs$ tar -xzvf ./git-lfs-linux-amd64-v2.13.3.tar.gz 
README.md
CHANGELOG.md
man/
man/git-lfs-clean.1
man/git-lfs-track.1
man/git-lfs-fetch.1.html
man/git-lfs-post-merge.1.html
man/git-lfs-env.1
man/git-lfs-uninstall.1.html
man/git-lfs-push.1.html
man/git-lfs-lock.1
man/git-lfs-clean.1.html
man/git-lfs-smudge.1
man/git-lfs-install.1.html
man/git-lfs-install.1
man/git-lfs-locks.1.html
man/git-lfs.1.html
man/git-lfs-prune.1
man/git-lfs-post-checkout.1.html
man/git-lfs-smudge.1.html
man/git-lfs-untrack.1
man/git-lfs-locks.1
man/git-lfs-migrate.1.html
man/git-lfs-env.1.html
man/git-lfs-fsck.1
man/git-lfs-migrate.1
man/git-lfs-ls-files.1.html
man/git-lfs-post-commit.1
man/git-lfs-ext.1
man/git-lfs-status.1.html
man/git-lfs-fetch.1
man/git-lfs-pull.1
man/git-lfs-untrack.1.html
man/git-lfs-prune.1.html
man/git-lfs-ls-files.1
man/git-lfs-pre-push.1.html
man/git-lfs.1
man/git-lfs-pointer.1
man/git-lfs-post-commit.1.html
man/git-lfs-track.1.html
man/git-lfs-logs.1.html
man/git-lfs-uninstall.1
man/git-lfs-config.5
man/git-lfs-update.1.html
man/git-lfs-update.1
man/git-lfs-clone.1
man/git-lfs-pointer.1.html
man/git-lfs-checkout.1.html
man/git-lfs-post-merge.1
man/git-lfs-clone.1.html
man/git-lfs-post-checkout.1
man/git-lfs-config.5.html
man/git-lfs-fsck.1.html
man/git-lfs-status.1
man/git-lfs-unlock.1.html
man/git-lfs-filter-process.1
man/git-lfs-lock.1.html
man/git-lfs-ext.1.html
man/git-lfs-push.1
man/git-lfs-pre-push.1
man/git-lfs-checkout.1
man/git-lfs-filter-process.1.html
man/git-lfs-pull.1.html
man/git-lfs-unlock.1
man/git-lfs-logs.1
git-lfs
install.sh
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/git-lfs$ 
```

## Installation

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/git-lfs$ ./install.sh 
install: cannot create regular file '/usr/local/bin/git-lfs': Permission denied
```

sudo ကို command ရှေ့က ခံပေးဖိုလိုအပ်တယ်...

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/git-lfs$ sudo ./install.sh 
[sudo] password for ye: 
Git LFS initialized.
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/git-lfs$ 
```

## Usage of git lfs

copy large experiment folder of NCRF++ to current repository:
```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/myPOS2/corpus-ver-2.0/git/myPOS/corpus-ver-3.0/iSAI-NLP2020-paper-experiment$ cp -r ../../../../iSAI-NLP2020-paper-experiment/4_NCRFPP .
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/myPOS2/corpus-ver-2.0/git/myPOS/corpus-ver-3.0/iSAI-NLP2020-paper-experiment$ ls
1_RDR  2_CRF  3_HMM  4_NCRFPP  README.md
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/myPOS2/corpus-ver-2.0/git/myPOS/corpus-ver-3.0/iSAI-NLP2020-paper-experiment$
```

## run git add

git command ရဲ့ အလုပ်လုပ်ပုံကိုတော့ သိပြီးသားလို့ ယူဆပါတယ်။  
git add, git commit, git push စတဲ့ command တွေကို မသိသေးရင် အရင်လေ့လာပါ။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/myPOS2/corpus-ver-2.0/git/myPOS/corpus-ver-3.0/iSAI-NLP2020-paper-experiment$ git add ./4_NCRFPP/
```

## check bigger files

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/myPOS2/corpus-ver-2.0/git/myPOS/corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/1_Report_wordCNN-CRF-charLSTM_myPOS_V2_with_100%_ASEAN/sample_data$ ll  -h
total 128M
drwxr-xr-x 2 ye ye 4.0K ဇူ     2 08:50 ./
drwxr-xr-x 3 ye ye 4.0K ဇူ     2 08:50 ../
-rwxr-xr-x 1 ye ye 3.7M ဇူ     2 08:50 dev.bmes*
-rwxr-xr-x 1 ye ye 6.6M ဇူ     2 08:50 lstmcrf.0.model*
-rwxr-xr-x 1 ye ye 101M ဇူ     2 08:50 lstmcrf.dset*
-rwxr-xr-x 1 ye ye 7.4M ဇူ     2 08:50 raw.bmes*
-rwxr-xr-x 1 ye ye 1.8M ဇူ     2 08:50 test.bmes*
-rwxr-xr-x 1 ye ye 7.4M ဇူ     2 08:50 train.bmes*
```

NCRF++ မော်ဒယ်တွေကို သိမ်းထားတဲ့ ဖိုလ်ဒါတိုင်းကို ဝင်ကြည့်တော့ .dset ဖိုင်တွေက 100MB ကျော်တာတွေကိုလည်း တွေ့ရပါတယ်။ ဒါတောင် အခုရောက်နေတဲ့ path က myPOS version 2.0 ကိုပဲ သုံးထားတဲ့ experiment ဖိုလ်ဒါပါ။ iSAI-NLP 2020 conference အတွက် ပြင်ခဲ့စဉ်က run ထားခဲ့တဲ့ ဖိုလ်ဒါပါ။ myPOS version 3.0 အတွက်ဆိုရင်တော့ လက်ရှိ filesize ထက် ပိုကြီးမယ့်ပုံရှိတယ်...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/myPOS2/corpus-ver-2.0/git/myPOS/corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/4_Report_wordLSTM-CRF-charCNN_myPOS_V2_100%ASEAN/sample_data$ ll -h
total 127M
drwxr-xr-x 2 ye ye 4.0K ဇူ     2 08:50 ./
drwxr-xr-x 3 ye ye 4.0K ဇူ     2 08:50 ../
-rwxr-xr-x 1 ye ye 3.7M ဇူ     2 08:50 dev.bmes*
-rwxr-xr-x 1 ye ye 5.3M ဇူ     2 08:50 lstmcrf.0.model*
-rwxr-xr-x 1 ye ye 101M ဇူ     2 08:50 lstmcrf.dset*
-rwxr-xr-x 1 ye ye 7.4M ဇူ     2 08:50 raw.bmes*
-rwxr-xr-x 1 ye ye 1.8M ဇူ     2 08:50 test.bmes*
-rwxr-xr-x 1 ye ye 7.4M ဇူ     2 08:50 train.bmes*
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/myPOS2/corpus-ver-2.0/git/myPOS/corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/4_Report_wordLSTM-CRF-charCNN_myPOS_V2_100%ASEAN/sample_data$ 
```

အထက်မှာ မြင်ရတဲ့အတိုင်းပဲ NCRF++ ရဲ့ ".dset" extension ရှိတဲ့ ဖိုင်တွေက ဆိုက်တွေက ကြီးတာကို တွေ့ရတယ်။  

## Prepare git lfs for *.dset files

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/myPOS2/corpus-ver-2.0/git/myPOS/corpus-ver-3.0/iSAI-NLP2020-paper-experiment$ git lfs install
Updated git hooks.
Git LFS initialized.
```

ကိုယ်က track လုပ်စေချင်တဲ့ file extension ကို git lfs track ဆိုတဲ့ command ကိုသုံးပြီးတော့ track လုပ်ခိုင်းထားရပါလိမ့်မယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/myPOS2/corpus-ver-2.0/git/myPOS/corpus-ver-3.0/iSAI-NLP2020-paper-experiment$ git lfs track "*.dset"
Tracking "*.dset"
```

သေချာအောင်လို့ .gitattributes ဆိုတဲ့ hidden file ကိုလည်း add လုပ်ထားပါ။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/myPOS2/corpus-ver-2.0/git/myPOS/corpus-ver-3.0/iSAI-NLP2020-paper-experiment$ git add .gitattributes 
```

4_NCRFPP/ ဖိုလ်ဒါ တစ်ခုလုံးကို git index ထဲကို ထည့်ပါမယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/myPOS2/corpus-ver-2.0/git/myPOS/corpus-ver-3.0/iSAI-NLP2020-paper-experiment$ git add ./4_NCRFPP/
```

commit လုပ်ကြည့်ရအောင် အဆင်ပြေရဲ့လားလို့...  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/myPOS2/corpus-ver-2.0/git/myPOS/corpus-ver-3.0/iSAI-NLP2020-paper-experiment$ git commit -m "4_NCRFPP/ for iSAI-NLP2020 Experiments"
[master 6df62a6] 4_NCRFPP/ for iSAI-NLP2020 Experiments
 213 files changed, 14970841 insertions(+)
 create mode 100644 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/.gitattributes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/1_Report_wordCNN-CRF-charLSTM_myPOS_V2_with_50%_ASEAN/note_terminal.txt
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/1_Report_wordCNN-CRF-charLSTM_myPOS_V2_with_50%_ASEAN/sample_data/dev.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/1_Report_wordCNN-CRF-charLSTM_myPOS_V2_with_50%_ASEAN/sample_data/lstmcrf.0.model
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/1_Report_wordCNN-CRF-charLSTM_myPOS_V2_with_50%_ASEAN/sample_data/lstmcrf.dset
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/1_Report_wordCNN-CRF-charLSTM_myPOS_V2_with_50%_ASEAN/sample_data/raw.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/1_Report_wordCNN-CRF-charLSTM_myPOS_V2_with_50%_ASEAN/sample_data/test.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/1_Report_wordCNN-CRF-charLSTM_myPOS_V2_with_50%_ASEAN/sample_data/train.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/1_Report_wordCNN-CRF-charLSTM_myPOS_V2_with_50%_ASEAN/wordCNN-CRF-charLSTM.train.config
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/2_Report_wordLSTM-charCNN_myPOS_V2_50%_ASEAN/note_terminal.txt
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/2_Report_wordLSTM-charCNN_myPOS_V2_50%_ASEAN/sample_data/dev.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/2_Report_wordLSTM-charCNN_myPOS_V2_50%_ASEAN/sample_data/lstmcrf.0.model
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/2_Report_wordLSTM-charCNN_myPOS_V2_50%_ASEAN/sample_data/lstmcrf.dset
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/2_Report_wordLSTM-charCNN_myPOS_V2_50%_ASEAN/sample_data/raw.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/2_Report_wordLSTM-charCNN_myPOS_V2_50%_ASEAN/sample_data/test.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/2_Report_wordLSTM-charCNN_myPOS_V2_50%_ASEAN/sample_data/train.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/2_Report_wordLSTM-charCNN_myPOS_V2_50%_ASEAN/wordLSTM-charCNN.train.config
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/3_Report_wordLSTM-CRF_myPOS_V2_50%_ASEAN/note_terminal.txt
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/3_Report_wordLSTM-CRF_myPOS_V2_50%_ASEAN/sample_data/dev.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/3_Report_wordLSTM-CRF_myPOS_V2_50%_ASEAN/sample_data/lstmcrf.0.model
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/3_Report_wordLSTM-CRF_myPOS_V2_50%_ASEAN/sample_data/lstmcrf.dset
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/3_Report_wordLSTM-CRF_myPOS_V2_50%_ASEAN/sample_data/raw.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/3_Report_wordLSTM-CRF_myPOS_V2_50%_ASEAN/sample_data/test.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/3_Report_wordLSTM-CRF_myPOS_V2_50%_ASEAN/sample_data/train.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/3_Report_wordLSTM-CRF_myPOS_V2_50%_ASEAN/wordLSTM-CRF.train.config
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/4_Report_wordLSTM-CRF-charCNN_myPOS_V2_50%_ASEAN/note_terminal.txt
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/4_Report_wordLSTM-CRF-charCNN_myPOS_V2_50%_ASEAN/sample_data/dev.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/4_Report_wordLSTM-CRF-charCNN_myPOS_V2_50%_ASEAN/sample_data/lstmcrf.0.model
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/4_Report_wordLSTM-CRF-charCNN_myPOS_V2_50%_ASEAN/sample_data/lstmcrf.dset
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/4_Report_wordLSTM-CRF-charCNN_myPOS_V2_50%_ASEAN/sample_data/raw.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/4_Report_wordLSTM-CRF-charCNN_myPOS_V2_50%_ASEAN/sample_data/test.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/4_Report_wordLSTM-CRF-charCNN_myPOS_V2_50%_ASEAN/sample_data/train.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/4_Report_wordLSTM-CRF-charCNN_myPOS_V2_50%_ASEAN/wordLSTM-CRF-charCNN.train.config
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/1__Report_NCRFPP_POS_1-3/note.txt
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/LICENCE
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/changeToColumn/ch2col-4all.sh
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/changeToColumn/ch2col.pl
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/changeToColumn/ctest1.nopipe.col
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/changeToColumn/data/ctest1 (50% of train1)
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/changeToColumn/data/otest
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/changeToColumn/data/otest_100%_ASEAN
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/changeToColumn/data/otest_50%_ASEAN
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/changeToColumn/data/train1 (Updatedmypos+10K+KoreanCorpus)
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/changeToColumn/otest.nopipe.col_1(50% ASEAN)
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/changeToColumn/otest.nopipe.col_2(100%)
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/changeToColumn/pipe2space-all.sh
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/changeToColumn/train1.nopipe.col
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/main.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/main_parse.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/__init__.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/__pycache__/__init__.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/__pycache__/__init__.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/__pycache__/charbigru.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/__pycache__/charbigru.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/__pycache__/charbilstm.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/__pycache__/charbilstm.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/__pycache__/charcnn.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/__pycache__/charcnn.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/__pycache__/crf.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/__pycache__/crf.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/__pycache__/sentclassifier.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/__pycache__/sentclassifier.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/__pycache__/seqlabel.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/__pycache__/seqlabel.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/__pycache__/wordrep.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/__pycache__/wordrep.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/__pycache__/wordsequence.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/__pycache__/wordsequence.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/charbigru.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/charbilstm.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/charcnn.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/crf.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/sentclassifier.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/seqlabel.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/wordrep.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/model/wordsequence.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/note.txt
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/other/demo.train.config
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/other/not_used___wordCNN-CRF-charLSTM.decode.config
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/other/note.txt
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/other/note_terminal.txt
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/sample_data/dev.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/sample_data/lstmcrf.0.model
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/sample_data/lstmcrf.dset
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/sample_data/raw.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/sample_data/test.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/sample_data/train.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/utils/__init__.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/utils/__pycache__/__init__.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/utils/__pycache__/__init__.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/utils/__pycache__/alphabet.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/utils/__pycache__/alphabet.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/utils/__pycache__/data.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/utils/__pycache__/data.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/utils/__pycache__/functions.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/utils/__pycache__/functions.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/utils/__pycache__/metric.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/utils/__pycache__/metric.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/utils/alphabet.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/utils/data.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/utils/functions.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/utils/metric.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/utils/tagSchemeConverter.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/wordCNN-CRF-charLSTM.train.config
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/wordLSTM-CRF-charCNN.train.config
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/wordLSTM-CRF.train.config
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/1_NCRFPP_with_otest_50%_ASEAN/wordLSTM-charCNN.train.config
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/1_Report_wordCNN-CRF-charLSTM_myPOS_V2_with_100%_ASEAN/note_terminal.txt
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/1_Report_wordCNN-CRF-charLSTM_myPOS_V2_with_100%_ASEAN/sample_data/dev.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/1_Report_wordCNN-CRF-charLSTM_myPOS_V2_with_100%_ASEAN/sample_data/lstmcrf.0.model
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/1_Report_wordCNN-CRF-charLSTM_myPOS_V2_with_100%_ASEAN/sample_data/lstmcrf.dset
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/1_Report_wordCNN-CRF-charLSTM_myPOS_V2_with_100%_ASEAN/sample_data/raw.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/1_Report_wordCNN-CRF-charLSTM_myPOS_V2_with_100%_ASEAN/sample_data/test.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/1_Report_wordCNN-CRF-charLSTM_myPOS_V2_with_100%_ASEAN/sample_data/train.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/1_Report_wordCNN-CRF-charLSTM_myPOS_V2_with_100%_ASEAN/wordCNN-CRF-charLSTM.train.config
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/2_Report_wordLSTM-charCNN_myPOS_V2_100%_ASEAN/note_terminal.txt
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/2_Report_wordLSTM-charCNN_myPOS_V2_100%_ASEAN/sample_data/dev.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/2_Report_wordLSTM-charCNN_myPOS_V2_100%_ASEAN/sample_data/lstmcrf.0.model
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/2_Report_wordLSTM-charCNN_myPOS_V2_100%_ASEAN/sample_data/lstmcrf.dset
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/2_Report_wordLSTM-charCNN_myPOS_V2_100%_ASEAN/sample_data/raw.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/2_Report_wordLSTM-charCNN_myPOS_V2_100%_ASEAN/sample_data/test.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/2_Report_wordLSTM-charCNN_myPOS_V2_100%_ASEAN/sample_data/train.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/2_Report_wordLSTM-charCNN_myPOS_V2_100%_ASEAN/wordLSTM-charCNN.train.config
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/3_Report_wordLSTM-CRF_myPOS_V2_100%_ASEAN/note_terminal.txt
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/3_Report_wordLSTM-CRF_myPOS_V2_100%_ASEAN/sample_data/dev.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/3_Report_wordLSTM-CRF_myPOS_V2_100%_ASEAN/sample_data/lstmcrf.0.model
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/3_Report_wordLSTM-CRF_myPOS_V2_100%_ASEAN/sample_data/lstmcrf.dset
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/3_Report_wordLSTM-CRF_myPOS_V2_100%_ASEAN/sample_data/raw.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/3_Report_wordLSTM-CRF_myPOS_V2_100%_ASEAN/sample_data/test.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/3_Report_wordLSTM-CRF_myPOS_V2_100%_ASEAN/sample_data/train.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/3_Report_wordLSTM-CRF_myPOS_V2_100%_ASEAN/wordLSTM-CRF.train.config
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/4_Report_wordLSTM-CRF-charCNN_myPOS_V2_100%ASEAN/note_terminal.txt
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/4_Report_wordLSTM-CRF-charCNN_myPOS_V2_100%ASEAN/sample_data/dev.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/4_Report_wordLSTM-CRF-charCNN_myPOS_V2_100%ASEAN/sample_data/lstmcrf.0.model
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/4_Report_wordLSTM-CRF-charCNN_myPOS_V2_100%ASEAN/sample_data/lstmcrf.dset
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/4_Report_wordLSTM-CRF-charCNN_myPOS_V2_100%ASEAN/sample_data/raw.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/4_Report_wordLSTM-CRF-charCNN_myPOS_V2_100%ASEAN/sample_data/test.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/4_Report_wordLSTM-CRF-charCNN_myPOS_V2_100%ASEAN/sample_data/train.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/4_Report_wordLSTM-CRF-charCNN_myPOS_V2_100%ASEAN/wordLSTM-CRF-charCNN.train.config
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/1__Report_NCRFPP_POS_1-3/note.txt
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/LICENCE
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/changeToColumn/ch2col-4all.sh
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/changeToColumn/ch2col.pl
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/changeToColumn/ctest1.nopipe.col
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/changeToColumn/data/ctest1 (50% of train1)
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/changeToColumn/data/otest
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/changeToColumn/data/otest_100%_ASEAN
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/changeToColumn/data/otest_50%_ASEAN
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/changeToColumn/data/train1 (Updatedmypos+10K+KoreanCorpus)
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/changeToColumn/otest.nopipe.col_1(50% ASEAN)
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/changeToColumn/otest.nopipe.col_2(100%)
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/changeToColumn/pipe2space-all.sh
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/changeToColumn/train1.nopipe.col
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/main.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/main_parse.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/__init__.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/__pycache__/__init__.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/__pycache__/__init__.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/__pycache__/charbigru.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/__pycache__/charbigru.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/__pycache__/charbilstm.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/__pycache__/charbilstm.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/__pycache__/charcnn.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/__pycache__/charcnn.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/__pycache__/crf.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/__pycache__/crf.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/__pycache__/sentclassifier.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/__pycache__/sentclassifier.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/__pycache__/seqlabel.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/__pycache__/seqlabel.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/__pycache__/wordrep.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/__pycache__/wordrep.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/__pycache__/wordsequence.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/__pycache__/wordsequence.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/charbigru.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/charbilstm.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/charcnn.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/crf.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/sentclassifier.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/seqlabel.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/wordrep.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/model/wordsequence.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/note.txt
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/other/demo.train.config
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/other/not_used___wordCNN-CRF-charLSTM.decode.config
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/other/note.txt
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/other/note_terminal.txt
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/sample_data/dev.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/sample_data/lstmcrf.0.model
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/sample_data/lstmcrf.dset
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/sample_data/raw.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/sample_data/test.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/sample_data/train.bmes
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/utils/__init__.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/utils/__pycache__/__init__.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/utils/__pycache__/__init__.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/utils/__pycache__/alphabet.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/utils/__pycache__/alphabet.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/utils/__pycache__/data.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/utils/__pycache__/data.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/utils/__pycache__/functions.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/utils/__pycache__/functions.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/utils/__pycache__/metric.cpython-36.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/utils/__pycache__/metric.cpython-37.pyc
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/utils/alphabet.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/utils/data.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/utils/functions.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/utils/metric.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/utils/tagSchemeConverter.py
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/wordCNN-CRF-charLSTM.train.config
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/wordLSTM-CRF-charCNN.train.config
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/wordLSTM-CRF.train.config
 create mode 100755 corpus-ver-3.0/iSAI-NLP2020-paper-experiment/4_NCRFPP/2_NCRFPP_with_otest_100%_ASEAN/wordLSTM-charCNN.train.config
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/myPOS2/corpus-ver-2.0/git/myPOS/corpus-ver-3.0/iSAI-NLP2020-paper-experiment$ 
```

commit လုပ်တာတော့ အထက်မှာ မြင်ရတဲ့အတိုင်း အဆင်ပြေပုံရှိပါတယ်။   
push မလုပ်ခင်မှာ online မှာ ရှိနေတဲ့ myPOS ရဲ့ repository ကို ကြိုကြည့်ထားကြရအောင်...  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/before-push.png" />  
</p>  
<div align="center">
  Fig. Before running "git push" command or before updating the remote repository  
</div>   


## git push 

git push လုပ်ပြီး အထက်မှာ ကြည့်ခဲ့တဲ့ remote repository ကို update လုပ်ကြည့်ရအောင်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/myPOS2/corpus-ver-2.0/git/myPOS/corpus-ver-3.0/iSAI-NLP2020-paper-experiment$ git push
Username for 'https://github.com': ye-kyaw-thu
Password for 'https://ye-kyaw-thu@github.com': 
Username for 'https://github.com': ye-kyaw-thu
Password for 'https://ye-kyaw-thu@github.com': 
Uploading LFS objects: 100% (8/8), 816 MB | 8.9 MB/s, done.                                                                                                                            
Enumerating objects: 125, done.
Counting objects: 100% (125/125), done.
Delta compression using up to 8 threads
Compressing objects: 100% (116/116), done.
Writing objects: 100% (122/122), 44.38 MiB | 3.62 MiB/s, done.
Total 122 (delta 26), reused 14 (delta 4), pack-reused 0
remote: Resolving deltas: 100% (26/26), completed with 2 local objects.
To https://github.com/ye-kyaw-thu/myPOS
   ae0ca00..6df62a6  master -> master
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/4github/myPOS2/corpus-ver-2.0/git/myPOS/corpus-ver-3.0/iSAI-NLP2020-paper-experiment$
```

filesize ကြီးတဲ့ ဖိုင်တွေအားလုံးကို အောင်အောင်မြင်မြင်နဲ့ upload လုပ်သွားတယ်လို့ ထင်ပါတယ်။  
သေချာအောင် browser ကို refresh လုပ်ပြီး mypos repository ကို ဝင်ကြည့်တဲ့အခါမှာ အောက်ပါပုံအတိုင်း 4_NCRFPP ဖိုလ်ဒါအသစ်ပေါ်လာတာကို တွေ့ရပါလိမ့်မယ်။  
The End! :P  

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/after-push.png" />  
</p>  
<div align="center">
  Fig. After running "git push" command  
</div>   
