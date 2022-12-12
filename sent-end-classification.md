# စာကြောင်း အဆုံးပိုင်းကို classification problem အနေနဲ့ လုပ်ကြည့်ခဲ့တဲ့ experiment log

## preprocessing

```
(base) ye@ykt-pro:~/exp/mySent/data/clean-data-rdy2train/data-sent$ ls
test.my  test.tg  train.my  train.tg  valid.my  valid.tg
(base) ye@ykt-pro:~/exp/mySent/data/clean-data-rdy2train/data-sent$ cat train.my valid.my > ../../pre-process/train-valid.sent.my
(base) ye@ykt-pro:~/exp/mySent/data/clean-data-rdy2train/data-sent$ cp test.my ../../pre-process/test.sent.my
(base) ye@ykt-pro:~/exp/mySent/data/clean-data-rdy2train/data-sent$ cd ../data-sent
data-sent/      data-sent+para/ 
(base) ye@ykt-pro:~/exp/mySent/data/clean-data-rdy2train/data-sent$ cd ../data-sent+para/
(base) ye@ykt-pro:~/exp/mySent/data/clean-data-rdy2train/data-sent+para$ ls
test.my  test.tg  train.my  train.tg  valid.my  valid.tg
(base) ye@ykt-pro:~/exp/mySent/data/clean-data-rdy2train/data-sent+para$ cat train.my valid.my > ../../pre-process/train-valid.para.my
(base) ye@ykt-pro:~/exp/mySent/data/clean-data-rdy2train/data-sent+para$ cp test.my > ../../pre-process/test.para.my
cp: missing destination file operand after 'test.my'
Try 'cp --help' for more information.
(base) ye@ykt-pro:~/exp/mySent/data/clean-data-rdy2train/data-sent+para$ cp test.my ../../pre-process/test.para.my
(base) ye@ykt-pro:~/exp/mySent/data/clean-data-rdy2train/data-sent+para$ cd ..
(base) ye@ykt-pro:~/exp/mySent/data/clean-data-rdy2train$ cd ..
(base) ye@ykt-pro:~/exp/mySent/data$ ls
clean-data-rdy2train  clean-data-rdy2train.zip  pre-process
(base) ye@ykt-pro:~/exp/mySent/data$ cd pre-process/
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ ls
test.para.my  test.sent.my  train-valid.para.my  train-valid.sent.my
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ chmod -x test.sent.my 
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ ls
test.para.my  test.sent.my  train-valid.para.my  train-valid.sent.my
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ wc *
    5512    96632  1380183 test.para.my
    4712    63622   919423 test.sent.my
   50081   896025 12821847 train-valid.para.my
   42414   575856  8335164 train-valid.sent.my
  102719  1632135 23456617 total
(base) ye@ykt-pro:~/exp/mySent/data/pre-process$ 
```
