# Revisiting Nagisa

## Installation

```
(base) ye@lst-gpu-server-197:~/tool$ /home/ye/anaconda3/bin/python -m pip install nagisa
WARNING: Keyring is skipped due to an exception: Failed to unlock the collection!
Collecting nagisa
  Downloading nagisa-0.2.11-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (21.6 MB)
     |████████████████████████████████| 21.6 MB 152 kB/s
Requirement already satisfied: numpy in /home/ye/anaconda3/lib/python3.8/site-packages (from nagisa) (1.24.3)
Requirement already satisfied: six in /home/ye/anaconda3/lib/python3.8/site-packages (from nagisa) (1.15.0)
Collecting DyNet38
  Downloading dyNET38-2.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (6.7 MB)
     |████████████████████████████████| 6.7 MB 417 kB/s
Requirement already satisfied: cython in /home/ye/anaconda3/lib/python3.8/site-packages (from DyNet38->nagisa) (0.29.21)
Installing collected packages: DyNet38, nagisa
Successfully installed DyNet38-2.2 nagisa-0.2.11
(base) ye@lst-gpu-server-197:~/tool$
```

## Python Code  

```python
import nagisa

text = 'Pythonで簡単に使えるツールです'
words = nagisa.tagging(text)
print(words)
#=> Python/名詞 で/助詞 簡単/形状詞 に/助動詞 使える/動詞 ツール/名詞 です/助動詞

# Get a list of words
print(words.words)
#=> ['Python', 'で', '簡単', 'に', '使える', 'ツール', 'です']

# Get a list of POS-tags
print(words.postags)
#=> ['名詞', '助詞', '形状詞', '助動詞', '動詞', '名詞', '助動詞']
```

running ...  

```
(base) ye@lst-gpu-server-197:~/tool$ python ./tst-nagisa.py
Python/名詞 で/助詞 簡単/形状詞 に/助動詞 使える/動詞 ツール/名詞 です/助動詞
['Python', 'で', '簡単', 'に', '使える', 'ツール', 'です']
['名詞', '助詞', '形状詞', '助動詞', '動詞', '名詞', '助動詞']
(base) ye@lst-gpu-server-197:~/tool$
```

## Post-processing with Nagisa

```python
import nagisa

text = 'Pythonで簡単に使えるツールです'
words = nagisa.tagging(text)

# Filter the words of the specific POS tags.
words = nagisa.filter(text, filter_postags=['助詞', '助動詞'])
print(words)
#=> Python/名詞 簡単/形状詞 使える/動詞 ツール/名詞

# Extarct only nouns.
words = nagisa.extract(text, extract_postags=['名詞'])
print(words)
#=> Python/名詞 ツール/名詞

# This is a list of available POS-tags in nagisa.
print(nagisa.tagger.postags)
#=> ['補助記号', '名詞', ... , 'URL']
```

```
(base) ye@lst-gpu-server-197:~/tool$ python ./tst-nagisa-filter.py
Python/名詞 簡単/形状詞 使える/動詞 ツール/名詞
Python/名詞 ツール/名詞
['oov', '補助記号', '名詞', '空白', '助詞', '接尾辞', '動詞', '連体詞', '助動詞', '形容詞', '感動詞', '接頭辞', '記号', '接続詞', '副詞', '代名詞', '形状詞', 'web誤脱', 'URL', '英 単語', '漢文', '未知語', '言いよどみ', 'ローマ字文']
(base) ye@lst-gpu-server-197:~/tool$
```

## Testing Adding User Dictionary  

```python
import nagisa

# default
text = "3月に見た「3月のライオン」"
print(nagisa.tagging(text))
#=> 3/名詞 月/名詞 に/助詞 見/動詞 た/助動詞 「/補助記号 3/名詞 月/名詞 の/助詞 ライオン/ 名詞 」/補助記号

# If a word ("3月のライオン") is included in the single_word_list, it is recognized as a single word.
new_tagger = nagisa.Tagger(single_word_list=['3月のライオン'])
print(new_tagger.tagging(text))
#=> 3/名詞 月/名詞 に/助詞 見/動詞 た/助動詞 「/補助記号 3月のライオン/名詞 」/補助記号
```

```
(base) ye@lst-gpu-server-197:~/tool$ python ./tst-nagisa-user-dict.py
3/名詞 月/名詞 に/助詞 見/動詞 た/助動詞 「/補助記号 3/名詞 月/名詞 の/助詞 ライオン/名詞 」/補助記号
3/名詞 月/名詞 に/助詞 見/動詞 た/助動詞 「/補助記号 3月のライオン/名詞 」/補助記号
(base) ye@lst-gpu-server-197:~/tool$
```

## Big Data Info

```
(base) ye@lst-gpu-server-197:~/tool$ git clone https://github.com/UniversalDependencies/UD_Japanese-GSD
Cloning into 'UD_Japanese-GSD'...
remote: Enumerating objects: 411, done.
remote: Counting objects: 100% (36/36), done.
remote: Compressing objects: 100% (25/25), done.
remote: Total 411 (delta 21), reused 25 (delta 11), pack-reused 375
Receiving objects: 100% (411/411), 35.48 MiB | 12.97 MiB/s, done.
Resolving deltas: 100% (249/249), done.
(base) ye@lst-gpu-server-197:~/tool$
```

```
(base) ye@lst-gpu-server-197:~/tool/UD_Japanese-GSD$ head -n 100 ./ja_gsd-ud-train.conllu
# newdoc id = train-s1
# sent_id = train-s1
# text = ホッケーにはデンジャラスプレーの反則があるので、膝より上にボールを浮かすことは基 本的に反則になるが、その例外の一つがこのスクープである。
1       ホッケー        ホッケー        NOUN    名詞-普通名詞-一般      _       9       obl       _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=名詞-普 通名詞-一般|SpaceAfter=No|UnidicInfo=,ホッケー,ホッケー,ホッケー,ホッケー,,,ホッケー,ホッ ケー,ホッケー
2       に      に      ADP     助詞-格助詞     _       1       case    _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助詞-格助詞|SpaceAfter=No|UnidicInfo=,に,に,に,ニ,,,ニ,ニ,に
3       は      は      ADP     助詞-係助詞     _       1       case    _       BunsetuBILabel=I|BunsetuPositionType=FUNC|LUWBILabel=B|LUWPOS=助詞-係助詞|SpaceAfter=No|UnidicInfo=,は,は,は,ワ,,,ハ,ハ,は
4       デンジャラス    デンジャラス    NOUN    名詞-普通名詞-一般      _       5       compound  _       BunsetuBILabel=B|BunsetuPositionType=CONT|LUWBILabel=B|LUWPOS=名詞-普通名 詞-一般|SpaceAfter=No|UnidicInfo=,デンジャラス,デンジャラス,デンジャラス,デンジャラス,,,デンジャラス,デンジャラスプレー,デンジャラスプレー
5       プレー  プレー  NOUN    名詞-普通名詞-サ変可能  _       7       nmod    _       BunsetuBILabel=I|BunsetuPositionType=SEM_HEAD|LUWBILabel=I|LUWPOS=名詞-普通名詞-一般|SpaceAfter=No|UnidicInfo=,プレー,プレー,プレー,プレー,,,プレー,デンジャラスプレー,デンジャラスプ レー
6       の      の      ADP     助詞-格助詞     _       5       case    _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助詞-格助詞|SpaceAfter=No|UnidicInfo=,の,の,の,ノ,,,ノ,ノ,の
7       反則    反則    NOUN    名詞-普通名詞-サ変可能  _       9       nsubj   _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=名詞-普通名詞-一般|SpaceAfter=No|UnidicInfo=,反則,反則,反則,ハンソク,,,ハンソク,ハンソク,反則
8       が      が      ADP     助詞-格助詞     _       7       case    _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助詞-格助詞|SpaceAfter=No|UnidicInfo=,が,が,が,ガ,,,ガ,ガ,が
9       ある    有る    VERB    動詞-非自立可能-五段-ラ行       _       19      advcl   _
BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=動詞-一般-五段-ラ行|PrevUDLemma=ある|SpaceAfter=No|UnidicInfo=,有る,ある,ある,アル,,,アル,アル,有る
10      の      の      SCONJ   助詞-準体助詞   _       9       mark    _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助動詞-助動詞-ダ|SpaceAfter=No|UnidicInfo=,の,の,の,ノ,,,ノ,ノダ,のだ
11      で      だ      AUX     助動詞-助動詞-ダ        _       10      fixed   _       BunsetuBILabel=I|BunsetuPositionType=FUNC|LUWBILabel=I|LUWPOS=助動詞-助動詞-ダ|SpaceAfter=No|UnidicInfo=,だ,で,だ,デ,,,ダ,ノダ,のだ
12      、      、      PUNCT   補助記号-読点   _       9       punct   _       BunsetuBILabel=I|BunsetuPositionType=CONT|LUWBILabel=B|LUWPOS=補助記号-読点|SpaceAfter=No|UnidicInfo=,、,、,、,,,,,,、
13      膝      膝      NOUN    名詞-普通名詞-一般      _       15      nmod    _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=名詞-普通名詞-一般|SpaceAfter=No|UnidicInfo=,膝,膝,膝,ヒザ,,,ヒザ,ヒザ,膝
14      より    より    ADP     助詞-格助詞     _       13      case    _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助詞-格助詞|SpaceAfter=No|UnidicInfo=,より,より,より,ヨリ,,,ヨリ,ヨリ,より
15      上      上      NOUN    名詞-普通名詞-副詞可能  _       19      obl     _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=名詞-普通名詞-一般|SpaceAfter=No|UnidicInfo=,上,上,上,ウエ,,,ウエ,ウエ,上
16      に      に      ADP     助詞-格助詞     _       15      case    _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助詞-格助詞|SpaceAfter=No|UnidicInfo=,に,に,に,ニ,,,ニ,ニ,に
17      ボール  ボール  NOUN    名詞-普通名詞-一般      _       19      obj     _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=名詞-普通名詞-一般|SpaceAfter=No|UnidicInfo=,ボール,ボール,ボール,ボール,,,ボール,ボール,ボール
18      を      を      ADP     助詞-格助詞     _       17      case    _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助詞-格助詞|SpaceAfter=No|UnidicInfo=,を,を,を,オ,,,ヲ,ヲ,を
19      浮かす  浮かす  VERB    動詞-一般-五段-サ行     _       20      acl     _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=動詞-一般-五段-サ行|SpaceAfter=No|UnidicInfo=,浮かす,浮かす,浮かす,ウカス,,,ウカス,ウカス,浮かす
20      こと    事      NOUN    名詞-普通名詞-一般      _       27      nsubj   _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=名詞-普通名詞-一般|SpaceAfter=No|UnidicInfo=,事,こと,こと,コト,,,コト,コト,事
21      は      は      ADP     助詞-係助詞     _       20      case    _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助詞-係助詞|SpaceAfter=No|UnidicInfo=,は,は,は,ワ,,,ハ,ハ,は
22      基本    基本    NOUN    名詞-普通名詞-一般      _       27      advcl   _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=形状詞-一般|SpaceAfter=No|UnidicInfo=,基本,基本,基本,キホン,,,キホン,キホンテキ,基本的
23      的      的      PART    接尾辞-形状詞的 _       22      mark    _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=I|LUWPOS=形状詞-一般|SpaceAfter=No|UnidicInfo=,的,的,的,テキ,,,テキ,キホンテキ,基本的
24      に      だ      AUX     助動詞-助動詞-ダ        _       22      cop     _       BunsetuBILabel=I|BunsetuPositionType=FUNC|LUWBILabel=B|LUWPOS=助動詞-助動詞-ダ|SpaceAfter=No|UnidicInfo=,だ,に,だ,ニ,,,ダ,ダ,だ
25      反則    反則    NOUN    名詞-普通名詞-サ変可能  _       27      obl     _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=名詞-普通名詞-一般|SpaceAfter=No|UnidicInfo=,反則,反則,反則,ハンソク,,,ハンソク,ハンソク,反則
26      に      に      ADP     助詞-格助詞     _       25      case    _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助詞-格助詞|SpaceAfter=No|UnidicInfo=,に,に,に,ニ,,,ニ,ニ,に
27      なる    成る    VERB    動詞-非自立可能-五段-ラ行       _       37      acl     _
BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=動詞-一般-五段-ラ行|PrevUDLemma=なる|SpaceAfter=No|UnidicInfo=,成る,なる,なる,ナル,,,ナル,ナル,成る
28      が      が      SCONJ   助詞-接続助詞   _       27      mark    _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助詞-接続助詞|SpaceAfter=No|UnidicInfo=,が,が,が,ガ,,,ガ,ガ,が
29      、      、      PUNCT   補助記号-読点   _       27      punct   _       BunsetuBILabel=I|BunsetuPositionType=CONT|LUWBILabel=B|LUWPOS=補助記号-読点|SpaceAfter=No|UnidicInfo=,、,、,、,,,,,,、
30      その    其の    DET     連体詞  _       31      det     _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=連体詞|SpaceAfter=No|UnidicInfo=,其の,その,その,ソノ,,,ソノ,ソノ,其の
31      例外    例外    NOUN    名詞-普通名詞-一般      _       34      nmod    _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=名詞-普通名詞-一般|SpaceAfter=No|UnidicInfo=,例外,例外,例外,レーガイ,,,レイガイ,レイガイ,例外
32      の      の      ADP     助詞-格助詞     _       31      case    _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助詞-格助詞|SpaceAfter=No|UnidicInfo=,の,の,の,ノ,,,ノ,ノ,の
33      一      一      NUM     名詞-数詞       _       34      nummod  _       BunsetuBILabel=B|BunsetuPositionType=CONT|LUWBILabel=B|LUWPOS=名詞-数詞|SpaceAfter=No|UnidicInfo=,一,一,一,ヒト,,,ヒト,ヒトツ,一つ
34      つ      つ      NOUN    接尾辞-名詞的-助数詞    _       37      nsubj   _       BunsetuBILabel=I|BunsetuPositionType=SEM_HEAD|LUWBILabel=I|LUWPOS=名詞-数詞|SpaceAfter=No|UnidicInfo=,つ,つ,つ,ツ,,,ツ,ヒトツ,一つ
35      が      が      ADP     助詞-格助詞     _       34      case    _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助詞-格助詞|SpaceAfter=No|UnidicInfo=,が,が,が,ガ,,,ガ,ガ,が
36      この    此の    DET     連体詞  _       37      det     _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=連体詞|SpaceAfter=No|UnidicInfo=,此の,この,この,コノ,,,コノ,コノ,此の
37      スクープ        スクープ        NOUN    名詞-普通名詞-サ変可能  _       0       root      _       BunsetuBILabel=B|BunsetuPositionType=ROOT|LUWBILabel=B|LUWPOS=名詞-普通名 詞-一般|SpaceAfter=No|UnidicInfo=,スクープ,スクープ,スクープ,スクープ,,,スクープ,スクープ,スクープ
38      で      だ      AUX     助動詞-助動詞-ダ        _       37      cop     _       BunsetuBILabel=I|BunsetuPositionType=FUNC|LUWBILabel=B|LUWPOS=助動詞-五段-ラ行|SpaceAfter=No|UnidicInfo=,だ,で,だ,デ,,,ダ,デアル,である
39      ある    有る    VERB    動詞-非自立可能-五段-ラ行       _       38      fixed   _
BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=I|LUWPOS=助動詞-五段-ラ行|PrevUDLemma=ある|SpaceAfter=No|UnidicInfo=,有る,ある,ある,アル,,,アル,デアル,である
40      。      。      PUNCT   補助記号-句点   _       37      punct   _       BunsetuBILabel=I|BunsetuPositionType=CONT|LUWBILabel=B|LUWPOS=補助記号-句点|UnidicInfo=,。,。,。,,,,,,。

# newdoc id = train-s2
# sent_id = train-s2
# text = また行きたい、そんな気持ちにさせてくれるお店です。
1       また    又      ADV     副詞    _       2       advmod  _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=副詞|SpaceAfter=No|UnidicInfo=,又,また,ま た,マタ,,,マタ,マタ,又
2       行き    行く    VERB    動詞-非自立可能-五段-カ行       _       13      acl     _
BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=動詞-一般-五段-カ行|SpaceAfter=No|UnidicInfo=,行く,行き,行く,イキ,,,イク,イク,行く
3       たい    たい    AUX     助動詞-助動詞-タイ      _       2       aux     _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助動詞-助動詞-タイ|SpaceAfter=No|UnidicInfo=,たい,たい,たい,タイ,,,タイ,タイ,たい
4       、      、      PUNCT   補助記号-読点   _       2       punct   _       BunsetuBILabel=I|BunsetuPositionType=CONT|LUWBILabel=B|LUWPOS=補助記号-読点|SpaceAfter=No|UnidicInfo=,、,、,、,,,,,,、
5       そんな  そんな  PRON    連体詞  _       6       nmod    _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=連体詞|SpaceAfter=No|UnidicInfo=,そんな,そんな,そんな,ソンナ,,,ソンナ,ソンナ,そんな
6       気持ち  気持ち  NOUN    名詞-普通名詞-一般      _       8       obl     _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=名詞-普通名詞-一般|SpaceAfter=No|UnidicInfo=,気持ち,気持ち,気持ち,キモチ,,,キモチ,キモチ,気持ち
7       に      に      ADP     助詞-格助詞     _       6       case    _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助詞-格助詞|SpaceAfter=No|UnidicInfo=,に,に,に,ニ,,,ニ,ニ,に
8       さ      為る    VERB    動詞-非自立可能-サ行変格        _       13      acl     _
BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=動詞-一般-サ行変格|PrevUDLemma=する|SpaceAfter=No|UnidicInfo=,為る,さ,する,サ,,,スル,スル,する
9       せ      せる    AUX     助動詞-下一段-サ行      _       8       aux     _       BunsetuBILabel=I|BunsetuPositionType=FUNC|LUWBILabel=B|LUWPOS=助動詞-下一段-サ行|SpaceAfter=No|UnidicInfo=,せる,せ,せる,セ,,,セル,セル,せる
10      て      て      SCONJ   助詞-接続助詞   _       8       mark    _       BunsetuBILabel=I|BunsetuPositionType=FUNC|LUWBILabel=B|LUWPOS=助動詞-下一段-ラ行|SpaceAfter=No|UnidicInfo=,て,て,て,テ,,,テ,テクレル,てくれる
11      くれる  呉れる  VERB    動詞-非自立可能-下一段-ラ行     _       10      fixed   _
BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=I|LUWPOS=助動詞-下一段-ラ行|SpaceAfter=No|UnidicInfo=,呉れる,くれる,くれる,クレル,,,クレル,テクレル,てくれる
12      お      御      NOUN    接頭辞  _       13      compound        _       BunsetuBILabel=B|BunsetuPositionType=CONT|LUWBILabel=B|LUWPOS=名詞-普通名詞-一般|SpaceAfter=No|UnidicInfo=,御,お,お,オ,,,オ,オミセ,御店
13      店      店      NOUN    名詞-普通名詞-一般      _       0       root    _       BunsetuBILabel=I|BunsetuPositionType=ROOT|LUWBILabel=I|LUWPOS=名詞-普通名詞-一般|SpaceAfter=No|UnidicInfo=,店,店,店,ミセ,,,ミセ,オミセ,御店
14      です    です    AUX     助動詞-助動詞-デス      _       13      cop     _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助動詞-助動詞-デス|PrevUDLemma=だ|SpaceAfter=No|UnidicInfo=,です,です,です,デス,,,デス,デス,です
15      。      。      PUNCT   補助記号-句点   _       13      punct   _       BunsetuBILabel=I|BunsetuPositionType=CONT|LUWBILabel=B|LUWPOS=補助記号-句点|UnidicInfo=,。,。,。,,,,,,。

# newdoc id = train-s3
# sent_id = train-s3
# text = 手に持った特殊な刃物を使ったアクロバティックな体術や、揚羽と薄羽同様にクナイや忍 具を使って攻撃してくる。
1       手      手      NOUN    名詞-普通名詞-助数詞可能        _       3       obl     _
BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=名詞-普通名詞-一般|SpaceAfter=No|UnidicInfo=,手,手,手,テ,,,テ,テ,手
2       に      に      ADP     助詞-格助詞     _       1       case    _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助詞-格助詞|SpaceAfter=No|UnidicInfo=,に,に,に,ニ,,,ニ,ニ,に
3       持っ    持つ    VERB    動詞-一般-五段-タ行     _       7       acl     _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=動詞-一般-五段-タ行|SpaceAfter=No|UnidicInfo=,持つ,持っ,持つ,モッ,,,モツ,モツ,持つ
4       た      た      AUX     助動詞-助動詞-タ        _       3       aux     _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助動詞-助動詞-タ|SpaceAfter=No|UnidicInfo=,た,た,た,タ,,,タ,タ,た
5       特殊    特殊    ADJ     形状詞-一般     _       7       acl     _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=形状詞-一般|SpaceAfter=No|UnidicInfo=,特殊,特殊,特殊,トクシュ,,,トクシュ,トクシュ,特殊
6       な      だ      AUX     助動詞-助動詞-ダ        _       5       aux     _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助動詞-助動詞-ダ|SpaceAfter=No|UnidicInfo=,だ,な,だ,ナ,,,ダ,ダ,だ
7       刃物    刃物    NOUN    名詞-普通名詞-一般      _       9       obj     _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=名詞-普通名詞-一般|SpaceAfter=No|UnidicInfo=,刃物,刃物,刃物,ハモノ,,,ハモノ,ハモノ,刃物
8       を      を      ADP     助詞-格助詞     _       7       case    _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助詞-格助詞|SpaceAfter=No|UnidicInfo=,を,を,を,オ,,,ヲ,ヲ,を
9       使っ    使う    VERB    動詞-一般-五段-ワア行   _       13      acl     _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=動詞-一般-五段-ワア行|SpaceAfter=No|UnidicInfo=,使う,使っ,使う,ツカッ,,,ツカウ,ツカウ,使う
10      た      た      AUX     助動詞-助動詞-タ        _       9       aux     _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助動詞-助動詞-タ|SpaceAfter=No|UnidicInfo=,た,た,た,タ,,,タ,タ,た
11      アクロバティック        アクロバチック  ADJ     形状詞-一般     _       13      acl       _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=形状詞- 一般|SpaceAfter=No|UnidicInfo=,アクロバチック,アクロバティック,アクロバティック,アクロバティック,,,アクロバティック,アクロバティック,アクロバティック
12      な      だ      AUX     助動詞-助動詞-ダ        _       11      aux     _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助動詞-助動詞-ダ|SpaceAfter=No|UnidicInfo=,だ,な,だ,ナ,,,ダ,ダ,だ
13      体術    体術    NOUN    名詞-普通名詞-一般      _       23      nmod    _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=名詞-普通名詞-一般|SpaceAfter=No|UnidicInfo=,体術,体術,体術,タイジュツ,,,タイジュツ,タイジュツ,体術
14      や      や      ADP     助詞-副助詞     _       13      case    _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助詞-副助詞|SpaceAfter=No|UnidicInfo=,や,や,や,ヤ,,,ヤ,ヤ,や
15      、      、      PUNCT   補助記号-読点   _       13      punct   _       BunsetuBILabel=I|BunsetuPositionType=CONT|LUWBILabel=B|LUWPOS=補助記号-読点|SpaceAfter=No|UnidicInfo=,、,、,、,,,,,,、
16      揚羽    揚羽    PROPN   名詞-固有名詞-人名-一般 _       19      obl     _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=名詞-固有名詞-人名-一般|SpaceAfter=No|UnidicInfo=,アゲハ,揚羽,揚羽,アゲハ,,,アゲハ,アゲハ,揚羽
17      と      と      ADP     助詞-格助詞     _       16      case    _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助詞-格助詞|SpaceAfter=No|UnidicInfo=,と,と,と,ト,,,ト,ト,と
18      薄羽    薄羽    PROPN   名詞-固有名詞-人名-一般 _       19      compound        _
BunsetuBILabel=B|BunsetuPositionType=CONT|LUWBILabel=B|LUWPOS=形状詞-一般|SpaceAfter=No|UnidicInfo=,ウスバ,薄羽,薄羽,ウスバ,,,ウスバ,ウスバドウヨウ,薄羽同様
19      同様    同様    ADJ     形状詞-一般     _       25      advcl   _       BunsetuBILabel=I|BunsetuPositionType=SEM_HEAD|LUWBILabel=I|LUWPOS=形状詞-一般|SpaceAfter=No|UnidicInfo=,同様,同様,同様,ドーヨー,,,ドウヨウ,ウスバドウヨウ,薄羽同様
20      に      だ      AUX     助動詞-助動詞-ダ        _       19      aux     _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助動詞-助動詞-ダ|SpaceAfter=No|UnidicInfo=,だ,に,だ,ニ,,,ダ,ダ,だ
21      クナイ  苦無    NOUN    名詞-普通名詞-一般      _       23      nmod    _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=名詞-普通名詞-一般|SpaceAfter=No|UnidicInfo=,苦無,クナイ,クナイ,クナイ,,,クナイ,クナイ,苦無
22      や      や      ADP     助詞-副助詞     _       21      case    _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助詞-副助詞|SpaceAfter=No|UnidicInfo=,や,や,や,ヤ,,,ヤ,ヤ,や
23      忍具    忍具    NOUN    名詞-普通名詞-一般      _       25      obj     _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=名詞-普通名詞-一般|SpaceAfter=No|UnidicInfo=,忍具,忍具,忍具,ニング,,,ニング,ニング,忍具
24      を      を      ADP     助詞-格助詞     _       23      case    _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助詞-格助詞|SpaceAfter=No|UnidicInfo=,を,を,を,オ,,,ヲ,ヲ,を
25      使っ    使う    VERB    動詞-一般-五段-ワア行   _       27      advcl   _       BunsetuBILabel=B|BunsetuPositionType=SEM_HEAD|LUWBILabel=B|LUWPOS=動詞-一般-五段-ワア行|SpaceAfter=No|UnidicInfo=,使う,使っ,使う,ツカッ,,,ツカウ,ツカウ,使う
26      て      て      SCONJ   助詞-接続助詞   _       25      mark    _       BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=B|LUWPOS=助詞-接続助詞|SpaceAfter=No|UnidicInfo=,て,て,て,テ,,,テ,テ,て
27      攻撃    攻撃    VERB    名詞-普通名詞-サ変可能  _       0       root    _       BunsetuBILabel=B|BunsetuPositionType=ROOT|LUWBILabel=B|LUWPOS=動詞-一般-サ行変格|SpaceAfter=No|UnidicInfo=,攻撃,攻撃,攻撃,コーゲキ,,,コウゲキ,コウゲキスル,攻撃する
28      し      為る    AUX     動詞-非自立可能-サ行変格        _       27      aux     _
BunsetuBILabel=I|BunsetuPositionType=FUNC|LUWBILabel=I|LUWPOS=動詞-一般-サ行変格|PrevUDLemma=する|SpaceAfter=No|UnidicInfo=,為る,し,する,シ,,,スル,コウゲキスル,攻撃する
29      て      て      SCONJ   助詞-接続助詞   _       27      mark    _       BunsetuBILabel=I|BunsetuPositionType=FUNC|LUWBILabel=B|LUWPOS=助動詞-カ行変格|SpaceAfter=No|UnidicInfo=,て,て,て,テ,,,テ,テクル,てくる
30      くる    来る    VERB    動詞-非自立可能-カ行変格        _       29      fixed   _
BunsetuBILabel=I|BunsetuPositionType=SYN_HEAD|LUWBILabel=I|LUWPOS=助動詞-カ行変格|SpaceAfter=No|UnidicInfo=,来る,くる,くる,クル,,,クル,テクル,てくる
31      。      。      PUNCT   補助記号-句点   _       27      punct   _       BunsetuBILabel=I|BunsetuPositionType=CONT|LUWBILabel=B|LUWPOS=補助記号-句点|UnidicInfo=,。,。,。,,,,,,。

# newdoc id = train-s4
# sent_id = train-s4
(base) ye@lst-gpu-server-197:~/tool/UD_Japanese-GSD$
```

## Test Training with Small Data  

I wann get sample dataset and wish to learn the training, prediction python code. And thus, cloning repository ...  

```
(base) ye@lst-gpu-server-197:~/tool$ git clone https://github.com/taishi-i/nagisa
Cloning into 'nagisa'...
remote: Enumerating objects: 848, done.
remote: Counting objects: 100% (265/265), done.
remote: Compressing objects: 100% (71/71), done.
remote: Total 848 (delta 209), reused 242 (delta 189), pack-reused 583
Receiving objects: 100% (848/848), 40.39 MiB | 15.00 MiB/s, done.
Resolving deltas: 100% (525/525), done.
(base) ye@lst-gpu-server-197:~/tool$ cd nagisa
(base) ye@lst-gpu-server-197:~/tool/nagisa$
```

```
(base) ye@lst-gpu-server-197:~/tool/nagisa/nagisa/data/sample_datasets$ wc sample*
  20   39  348 sample.dev
   7   14   87 sample.dict
   6   87 1661 sample.emb
  29   55  352 sample.pred
  26   49  328 sample.test
  33   62  429 sample.train
 121  306 3205 total
```

I tried training with sample data and got following error message:  

```
$ time python ./tutorial_train_ud.py
Traceback (most recent call last):
  File "./tutorial_train_ud.py", line 56, in <module>
    write_file(fn_in_train, fn_out_train)
  File "./tutorial_train_ud.py", line 16, in write_file
    postag = tokens[3]
IndexError: list index out of range
```

Update the code for debugging ...  

```python
import nagisa

def write_file(fn_in, fn_out):
    with open(fn_in, "r") as f:
        data = []
        words = []
        postags = []
        line_number = 0  # Add line number counter for debugging
        for line in f:
            line_number += 1
            line = line.strip()

            if len(line) > 0:
                prefix = line[0]
                if prefix != "#":
                    tokens = line.split("\t")
                    if len(tokens) >= 4:  # Check if there are enough tokens
                        word = tokens[1]
                        postag = tokens[3]
                        words.append(word)
                        postags.append(postag)
                    else:
                        print(f"Line {line_number} has insufficient tokens: {line}")
            else:
                if (len(words) > 0) and (len(postags) > 0):
                    data.append([words, postags])
                    words = []
                    postags = []

    with open(fn_out, "w") as f:
        for words, postags in data:
            for word, postag in zip(words, postags):
                f.write("\t".join([word, postag]) + "\n")
            f.write("EOS\n")
```

When I did debugging, Got followings:  

```
$ python ./tutorial_train_ud.py
Line 1 has insufficient tokens: RNN     名詞
Line 2 has insufficient tokens: を      助詞
Line 3 has insufficient tokens: 用い    動詞
Line 4 has insufficient tokens: た      助動詞
Line 5 has insufficient tokens: 日本    名詞
Line 6 has insufficient tokens: 語      名詞
Line 7 has insufficient tokens: 単語    名詞
Line 8 has insufficient tokens: 分割    名詞
Line 9 has insufficient tokens: /       補助記号
Line 10 has insufficient tokens: 品詞   名詞
Line 11 has insufficient tokens: タグ   名詞
Line 12 has insufficient tokens: 付け   動詞
Line 13 has insufficient tokens: ツール 名詞
Line 14 has insufficient tokens: の     助詞
Line 15 has insufficient tokens: 紹介   名詞
Line 16 has insufficient tokens: EOS
Line 17 has insufficient tokens: 唯一   名詞
Line 18 has insufficient tokens: の     助詞
Line 19 has insufficient tokens: 趣味   名詞
Line 20 has insufficient tokens: は     助詞
Line 21 has insufficient tokens: 料理   名詞
Line 22 has insufficient tokens: EOS
Line 23 has insufficient tokens: とても 副詞
Line 24 has insufficient tokens: おいしかっ     形容詞
Line 25 has insufficient tokens: た     助動詞
Line 26 has insufficient tokens: です   助動詞
Line 27 has insufficient tokens: 。     補助記号
Line 28 has insufficient tokens: EOS
Line 29 has insufficient tokens: ドル   名詞
Line 30 has insufficient tokens: は     助詞
Line 31 has insufficient tokens: 主要   形状詞
Line 32 has insufficient tokens: 通貨   名詞
Line 33 has insufficient tokens: EOS
Line 1 has insufficient tokens: ニューラル      名詞
Line 2 has insufficient tokens: ネットワーク    名詞
Line 3 has insufficient tokens: を      助詞
Line 4 has insufficient tokens: 使っ    動詞
Line 5 has insufficient tokens: て      助動詞
Line 6 has insufficient tokens: ます    助動詞
Line 7 has insufficient tokens: 。      補助記号
Line 8 has insufficient tokens: EOS
Line 9 has insufficient tokens: (人•ᴗ•♡)       補助記号
Line 10 has insufficient tokens: こんばんは     感動詞
Line 11 has insufficient tokens: ♪     補助記号
Line 12 has insufficient tokens: EOS
Line 13 has insufficient tokens: https://github.com/taishi-i/nagisa     URL
Line 14 has insufficient tokens: で     助詞
Line 15 has insufficient tokens: コード 名詞
Line 16 has insufficient tokens: を     助詞
Line 17 has insufficient tokens: 公開   名詞
Line 18 has insufficient tokens: 中     接尾辞
Line 19 has insufficient tokens: (๑　̄ω　̄๑)   補助記号
Line 20 has insufficient tokens: EOS
Line 1 has insufficient tokens: 福岡    名詞
Line 2 has insufficient tokens: ・      補助記号
Line 3 has insufficient tokens: 博多    名詞
Line 4 has insufficient tokens: の      助詞
Line 5 has insufficient tokens: 観光    名詞
Line 6 has insufficient tokens: 情報    名詞
Line 7 has insufficient tokens: EOS
Line 8 has insufficient tokens: Python  名詞
Line 9 has insufficient tokens: で      助詞
Line 10 has insufficient tokens: 簡単   形状詞
Line 11 has insufficient tokens: に     助動詞
Line 12 has insufficient tokens: 使える 動詞
Line 13 has insufficient tokens: ツール 名詞
Line 14 has insufficient tokens: です   助動詞
Line 15 has insufficient tokens: EOS
Line 16 has insufficient tokens: 顔     名詞
Line 17 has insufficient tokens: 文字   名詞
Line 18 has insufficient tokens: や     助詞
Line 19 has insufficient tokens: URL    名詞
Line 20 has insufficient tokens: に     助詞
Line 21 has insufficient tokens: 対し   動詞
Line 22 has insufficient tokens: て     助詞
Line 23 has insufficient tokens: 頑健   名詞
Line 24 has insufficient tokens: な     助動詞
Line 25 has insufficient tokens: 解析   名詞
Line 26 has insufficient tokens: EOS
[nagisa] LAYERS: 1
[nagisa] THRESHOLD: 2
[nagisa] DECAY: 1
[nagisa] EPOCH: 10
[nagisa] WINDOW_SIZE: 3
[nagisa] DIM_UNI: 32
[nagisa] DIM_BI: 16
[nagisa] DIM_WORD: 16
[nagisa] DIM_CTYPE: 8
[nagisa] DIM_TAGEMB: 16
[nagisa] DIM_HIDDEN: 100
[nagisa] LEARNING_RATE: 0.1
[nagisa] DROPOUT_RATE: 0.3
[nagisa] SEED: 1234
[nagisa] TRAINSET: sample.train.out
[nagisa] TESTSET: sample.test.out
[nagisa] DEVSET: sample.dev.out
[nagisa] DICTIONARY: None
[nagisa] EMBEDDING: None
[nagisa] HYPERPARAMS: sample.model.hp
[nagisa] MODEL: sample.model.params
[nagisa] VOCAB: sample.model.vocabs
[nagisa] EPOCH_MODEL: sample.model_epoch.params
[nagisa] NUM_TRAIN: 0
[nagisa] NUM_TEST: 0
[nagisa] NUM_DEV: 0
[nagisa] VOCAB_SIZE_UNI: 2
[nagisa] VOCAB_SIZE_BI: 2
[nagisa] VOCAB_SIZE_WORD: 2
[nagisa] VOCAB_SIZE_POSTAG: 1
Epoch   LR      Loss    Time_m  DevWS_f1        DevPOS_f1       TestWS_f1       TestPOS_f1
Traceback (most recent call last):
  File "./tutorial_train_ud.py", line 64, in <module>
    nagisa.fit(train_file=fn_out_train, dev_file=fn_out_dev,
  File "/home/ye/anaconda3/lib/python3.8/site-packages/nagisa/train.py", line 136, in fit
    _start(hp, model=_model, train_data=TrainData, test_data=TestData, dev_data=DevData)
  File "/home/ye/anaconda3/lib/python3.8/site-packages/nagisa/train.py", line 214, in _start
    dev_ws_f, dev_pos_f = _evaluation(hp, fn_model=hp['EPOCH_MODEL'], data=dev_data)
  File "/home/ye/anaconda3/lib/python3.8/site-packages/nagisa/train.py", line 167, in _evaluation
    _, _, ws_f, _, _, pos_f = mecab_system_eval.calculate_fvalues(r)
  File "/home/ye/anaconda3/lib/python3.8/site-packages/nagisa/mecab_system_eval.py", line 92, in calculate_fvalues
    ws_p = round(100*ws_c/prec, 4)
ZeroDivisionError: division by zero

```

## Training ja_usd_ud Data

And thus, using the Japanese UD data and using the exact sample training code and it looks OK ...  

```
(base) ye@lst-gpu-server-197:~/tool/nagisa/nagisa/ytest$ time python ./tutorial_train_ud.p
y | tee train.log
[nagisa] LAYERS: 1
[nagisa] THRESHOLD: 2
[nagisa] DECAY: 1
[nagisa] EPOCH: 10
[nagisa] WINDOW_SIZE: 3
[nagisa] DIM_UNI: 32
[nagisa] DIM_BI: 16
[nagisa] DIM_WORD: 16
[nagisa] DIM_CTYPE: 8
[nagisa] DIM_TAGEMB: 16
[nagisa] DIM_HIDDEN: 100
[nagisa] LEARNING_RATE: 0.1
[nagisa] DROPOUT_RATE: 0.3
[nagisa] SEED: 1234
[nagisa] TRAINSET: ja_gsd_ud.train
[nagisa] TESTSET: ja_gsd_ud.test
[nagisa] DEVSET: ja_gsd_ud.dev
[nagisa] DICTIONARY: None
[nagisa] EMBEDDING: None
[nagisa] HYPERPARAMS: ja_gsd_ud.hp
[nagisa] MODEL: ja_gsd_ud.params
[nagisa] VOCAB: ja_gsd_ud.vocabs
[nagisa] EPOCH_MODEL: ja_gsd_ud_epoch.params
[nagisa] NUM_TRAIN: 7050
[nagisa] NUM_TEST: 543
[nagisa] NUM_DEV: 507
[nagisa] VOCAB_SIZE_UNI: 2340
[nagisa] VOCAB_SIZE_BI: 24792
[nagisa] VOCAB_SIZE_WORD: 8724
[nagisa] VOCAB_SIZE_POSTAG: 17
Epoch   LR      Loss    Time_m  DevWS_f1        DevPOS_f1       TestWS_f1       TestPOS_f1
1       0.100   11.31   2.191   96.53           92.48           96.97           92.38
2       0.100   4.717   2.206   96.96           93.65           97.44           93.70
3       0.100   3.581   2.194   97.29           94.35           97.75           94.77
4       0.050   3.005   2.118   97.22           94.61           97.75           94.77
5       0.050   2.189   2.199   97.69           95.15           98.14           95.58
6       0.025   1.889   2.122   97.59           95.09           98.14           95.58
7       0.012   1.541   2.125   97.68           95.36           98.14           95.58
8       0.012   1.358   2.203   97.74           95.34           98.05           95.59
9       0.006   1.287   2.123   97.66           95.36           98.05           95.59
10      0.003   1.217   2.127   97.66           95.35           98.05           95.59

real    21m47.005s
user    21m45.817s
sys     0m4.480s
(base) ye@lst-gpu-server-197:~/tool/nagisa/nagisa/ytest$
```

## Testing 

```
import nagisa

if __name__ == "__main__":
    # Build the tagger by loading the trained model files.
    ud_tagger = nagisa.Tagger(vocabs='ja_gsd_ud.vocabs',
                              params='ja_gsd_ud.params',
                              hp='ja_gsd_ud.hp')

    text = "福岡・博多の観光情報"
    words = ud_tagger.tagging(text)
    print(words)
    #> 福岡/PROPN ・/SYM 博多/PROPN の/ADP 観光/NOUN 情報/NOUN
```

```
(base) ye@lst-gpu-server-197:~/tool/nagisa/nagisa/ytest$ time python ./tutorial_predict_ud.py
福岡/PROPN ・/SYM 博多/PROPN の/ADP 観光/NOUN 情報/NOUN

real    0m3.779s
user    0m4.942s
sys     0m2.179s
(base) ye@lst-gpu-server-197:~/tool/nagisa/nagisa/ytest$
```

## Error Analysis

```python
import nagisa
import pandas as pd

from sklearn.metrics import confusion_matrix


def load_file(filename):
    X = []
    Y = []
    words = []
    tags = []
    with open(filename, "r") as f:
        for line in f:
            line = line.rstrip()
            if line == "EOS":
                assert(len(words) == len(tags))
                X.append(words)
                Y.append(tags)
                words = []
                tags = []
            else:
                line = line.split("\t")
                word = " ".join(line[:-1])
                tag = line[-1]
                words.append(word)
                tags.append(tag)
    return X, Y


def create_confusion_matrix(tagger, X, Y):
    true_cm = []
    pred_cm = []
    label2id = {}
    for i in range(len(X)):
        words = X[i]
        true_tags = Y[i]
        pred_tags = tagger.decode(words) # decoding

        if true_tags != pred_tags:
            for true_tag, pred_tag in zip(true_tags, pred_tags):
                if true_tag != pred_tag:
                    if true_tag not in label2id:
                        label2id[true_tag] = len(label2id)

                    if pred_tag not in label2id:
                        label2id[pred_tag] = len(label2id)

                    true_cm.append(label2id[true_tag])
                    pred_cm.append(label2id[pred_tag])

    cm = confusion_matrix(true_cm, pred_cm)
    labels = list(label2id.keys())
    cm_labeled = pd.DataFrame(cm, columns=labels, index=labels)
    return cm_labeled


if __name__ == "__main__":
    # load the testset
    test_X, test_Y = load_file("ja_gsd_ud.test")

    # build the tagger for UD
    ud_tagger = nagisa.Tagger(vocabs='ja_gsd_ud.vocabs',
                              params='ja_gsd_ud.params',
                              hp='ja_gsd_ud.hp')

    # create a confusion matrix if tagger make a mistake in prediction.
    cm_labeled = create_confusion_matrix(ud_tagger, test_X, test_Y)
    print(cm_labeled)
```

Error analysis result ...  

```
(base) ye@lst-gpu-server-197:~/tool/nagisa/nagisa/ytest$ time python ./tutorial_error_anal
ysis_ud.py
Note: NumExpr detected 32 cores but "NUMEXPR_MAX_THREADS" not set, so enforcing safe limit of 8.
NumExpr defaulting to 8 threads.
/home/ye/anaconda3/lib/python3.8/site-packages/pandas/core/computation/expressions.py:20: UserWarning: Pandas requires version '2.7.3' or newer of 'numexpr' (version '2.7.1' currently installed).
  from pandas.core.computation.check import NUMEXPR_INSTALLED
/home/ye/anaconda3/lib/python3.8/site-packages/numpy/core/getlimits.py:518: UserWarning: The value of the smallest subnormal for <class 'numpy.float64'> type is zero.
  setattr(self, word, getattr(machar, word).flat[0])
/home/ye/anaconda3/lib/python3.8/site-packages/numpy/core/getlimits.py:89: UserWarning: The value of the smallest subnormal for <class 'numpy.float64'> type is zero.
  return self._float_to_str(self.smallest_subnormal)
/home/ye/anaconda3/lib/python3.8/site-packages/numpy/core/getlimits.py:518: UserWarning: The value of the smallest subnormal for <class 'numpy.float32'> type is zero.
  setattr(self, word, getattr(machar, word).flat[0])
/home/ye/anaconda3/lib/python3.8/site-packages/numpy/core/getlimits.py:89: UserWarning: The value of the smallest subnormal for <class 'numpy.float32'> type is zero.
  return self._float_to_str(self.smallest_subnormal)
       AUX  VERB  ADJ  ADV  NOUN  PROPN  PART  ...  CCONJ  SCONJ  PRON  PUNCT  NUM  INTJ  SYM
AUX      0     3    4    0     2      0     1  ...      0      2     0      0    0     0    0
VERB     6     0    4    2    15      0     0  ...      0      1     0      0    1     0    0
ADJ      8     3    0    2    32      2     1  ...      0      0     0      0    0     0    0
ADV      0     2    5    0    20      2     0  ...      1      0     0      0    0     0    0
NOUN     3    13   13    6     0     98     0  ...      1      1     0      0    1     0    0
PROPN    0     0    0    0    37      0     0  ...      0      0     0      0    1     0    0
PART     1     1    1    0     4      0     0  ...      0      0     0      0    0     0    0
DET      0     2    0    0     0      0     0  ...      0      0     0      0    0     0    0
ADP     13     0    0    3     2      0     4  ...      0      3     0      0    0     0    0
CCONJ    0     1    0    0     0      0     0  ...      0      0     0      0    0     0    0
SCONJ    5     1    0    0     1      0     0  ...      0      0     0      0    0     0    0
PRON     0     1    0    1     4      0     0  ...      0      0     0      0    0     1    0
PUNCT    0     0    0    0     2      0     0  ...      0      0     0      0    0     0    0
NUM      0     0    0    0     2      0     0  ...      0      0     0      0    0     0    0
INTJ     0     0    0    0     0      0     0  ...      0      1     0      0    0     0    0
SYM      0     0    1    0     0      0     0  ...      0      0     0      0    0     0    0

[16 rows x 16 columns]

real    0m6.260s
user    0m7.236s
sys     0m2.294s
(base) ye@lst-gpu-server-197:~/tool/nagisa/nagisa/ytest$
```

## Reference

https://nagisa.readthedocs.io/en/latest/tutorial.html  
https://github.com/taishi-i/nagisa-tutorial-pycon2019  

