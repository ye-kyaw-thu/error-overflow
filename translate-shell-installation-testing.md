## Installation

```
lar@lar-air:~/tool$ git clone https://github.com/soimort/translate-shell
Cloning into 'translate-shell'...
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 4579 (delta 0), reused 1 (delta 0), pack-reused 4575
Receiving objects: 100% (4579/4579), 2.41 MiB | 260.00 KiB/s, done.
Resolving deltas: 100% (2929/2929), done.
Checking connectivity... done.
lar@lar-air:~/tool$ cd translate-shell/
lar@lar-air:~/tool/translate-shell$ make
[OK] Task build completed.
lar@lar-air:~/tool/translate-shell$ sudo make install
[sudo] password for lar: 
[OK] Task build completed.
[OK] translate-shell installed.
```

## Testing

```
lar@lar-air:~/tool/translate-shell$ trans နေကောင်းလား
နေကောင်းလား
(naykaungglarr)

How are you

Translations of နေကောင်းလား
[ မြန်မာစာ -> English ]

နေကောင်းလား
    How are you, how are u
```

## ဘာသာ နှစ်ဘာသာကို ပြန်ခိုင်းတာ

```
lar@lar-air:~/tool/translate-shell$ trans :my+zh 俺は自然言語処理の研究者です
俺は自然言語処理の研究者です
(Ore wa shizen gengo shori no kenkyūshadesu)

ငါကသဘာဝဘာသာစကားအပြောင်းအလဲနဲ့သုတေသီတစ်ယောက်ပါ
(ngar k sabharw bharsarhcakarr aapyaunggaalellnae sutayse taityout par)

Translations of 俺は自然言語処理の研究者です
[ 日本語 -> မြန်မာစာ ]

俺は自然言語処理の研究者です
    ငါကသဘာဝဘာသာစကားအပြောင်းအလဲနဲ့သုတေသီတစ်ယောက်ပါ, ငါကသဘာဝဘာသာစကားအပြောင်းအလဲနဲ့တစ်သုတေသီဖြစ်ပါသည်

俺は自然言語処理の研究者です
(Ore wa shizen gengo shori no kenkyūshadesu)

我是自然语言处理研究员
(Wǒ shì zìrán yǔyán chǔlǐ yánjiùyuán)

Translations of 俺は自然言語処理の研究者です
[ 日本語 -> 简体中文 ]

俺は自然言語処理の研究者です
    我是自然语言处理研究员, 我是自然语言处理的研究
lar@lar-air:~/tool/translate-shell$ 
```

## ဘာသာ သုံးဘာသာ တခါတည်း ပြန်ခိုင်းတာ

```
lar@lar-air:~/tool/translate-shell$ trans :ko+th+fr 俺は自然言語処理の研究者です
俺は自然言語処理の研究者です
(Ore wa shizen gengo shori no kenkyūshadesu)

나는 자연 언어 처리의 연구원입니다
(naneun jayeon eon-eo cheoliui yeonguwon-ibnida)

Translations of 俺は自然言語処理の研究者です
[ 日本語 -> 한국어 ]

俺 は
    나는, 난
自然
    자연, 자연스럽게, 천연, 자연스러운, 자연적
言語
    언어, 언어들
処理
    처리, 작업, 가공, 과정, 처리하는
の
    의, 를, 에 대한, 과, 대한
研究 者 です
    연구원입니다

俺は自然言語処理の研究者です
(Ore wa shizen gengo shori no kenkyūshadesu)

ฉันเป็นนักวิจัยการประมวลผลภาษาธรรมชาติ
(C̄hạn pĕn nạk wicạy kār pramwl p̄hl p̣hās̄ʹā ṭhrrmchāti)

Translations of 俺は自然言語処理の研究者です
[ 日本語 -> ไทย ]

俺は自然言語処理の研究者です
    ฉันเป็นนักวิจัยการประมวลผลภาษาธรรมชาติ, ฉันเป็นนักวิจัยของการประมวลผลภาษาธรรมชาติ

俺は自然言語処理の研究者です
(Ore wa shizen gengo shori no kenkyūshadesu)

Je suis chercheur en traitement du langage naturel

Translations of 俺は自然言語処理の研究者です
[ 日本語 -> Français ]

俺は自然言語処理の研究者です
    Je suis chercheur en traitement du langage naturel, I est un chercheur de traitement du langage naturel
lar@lar-air:~/tool/translate-shell$
```

## တချို့ဘာသာစကားတွေကြတော့ target language ကို သေသေချာချာ ခွဲခြားပေးဖို့လိုအပ်

```
တယ်။ ဥပမာ ဂျပန်နဲ့ တရုပ်က စာလုံးတွေ တူကြပေမဲ့ အဓိပ္ပါယ် မတူတဲ့ အခါမျိုး ရှိတယ်လေ။

lar@lar-air:~/tool/translate-shell$ trans ja: 手紙
手紙
(Tegami)

letter

Definitions of 手紙
[ 日本語 -> English ]

noun
    letter
        文字, レター, 手紙, 書簡, 文書, 書面

手紙
    letter, The letter
lar@lar-air:~/tool/translate-shell$ trans zh: 手紙
手紙
(Shǒuzhǐ)

Toilet paper

Translations of 手紙
[ 简体中文 -> English ]

手紙
    Toilet paper
```

## စာလုံး တစ်လုံးချင်းစီကို ဘာသာပြန်ခိုင်းတာ

```
lar@lar-air:~/tool/translate-shell$ trans en:ja word processor
word
/wərd/

語
(Go)

Definitions of word
[ English -> 日本語 ]

noun
    ワード
        word
    単語
        word, vocabulary, separate word, single-character word
    語
        word, language
    言葉
        word, language, speech
    語句
        phrase, word
    伝言
        message, verbal message, word, rumor, gossip, scandal
    一言半句
        word
    口舌
        tongue, talking recklessly, word, curtain lecture, quarreling

word
    語, ワード, 一言, 単語
```

## Multiple words တွေ သို့မဟုတ် phrase ကို ဘာသာပြန်ခိုင်းတာ

```
lar@lar-air:~/tool/translate-shell$ trans en:ja "word processor"
word processor

ワードプロセッサ
(Wādopurosessa)

Definitions of word processor
[ English -> 日本語 ]

noun
    ワードプロセッサー
        word processor

word processor
    ワードプロセッサ, ワードプロセッサー
```

## Multiple lines ကို ပြန်ခိုင်းတာ

```
lar@lar-air:~/tool/translate-shell$ trans my:ja "ငါ ဂျပန်မှာ ၁၇နှစ် နေခဲ့တယ် ။
> ပြီးတော့  ထိုင်းမှာ ၂နှစ် နေခဲ့တယ်။"
ငါ ဂျပန်မှာ ၁၇နှစ် နေခဲ့တယ် ။
 ပြီးတော့  ထိုင်းမှာ ၂နှစ် နေခဲ့တယ်။
(ngar gyapaanmhar  1 7nhait nayhkaetaal  .
pyeetot  htinemhar  2nhait  nayhkaetaal .)

私は日本に17年間住んでいます。
そして、私はタイで2年間過ごしました。
(Watashi wa Nihon ni 17-nenkan sunde imasu. Soshite, watashi wa Tai de 2-nenkan sugoshimashita.)

Translations of ငါ ဂျပန်မှာ ၁၇နှစ် နေခဲ့တယ် ။
 ပြီးတော့  ထိုင်းမှာ ၂နှစ် နေခဲ့တယ်။
[ မြန်မာစာ -> 日本語 ]

ငါ ဂျပန်မှာ ၁၇နှစ် နေခဲ့တယ် ။
    私は日本に17年間住んでいます。, 私は日本で17年間に行ってきました。

    
ပြီးတော့  ထိုင်းမှာ ၂နှစ် နေခဲ့တယ်။
    そして、私はタイで2年間過ごしました。, 私はタイで2年でした。
lar@lar-air:~/tool/translate-shell$ 
```

## Brief mode

```
lar@lar-air:~/tool/translate-shell$ trans -b my:ja "ငါ ဂျပန်မှာ ၁၇နှစ် နေခဲ့တယ် ။
ပြီးတော့  ထိုင်းမှာ ၂နှစ် နေခဲ့တယ်။"
私は日本に17年間住んでいます。
そして、私はタイで2年間過ごしました。
```

## Brief mode မှာ phonetic notation ကိုပါ ပြစေချင်ရင်

```
lar@lar-air:~/tool/translate-shell$ trans -b my:@ja "ငါ ဂျပန်မှာ ၁၇နှစ် နေခဲ့တယ် ။
ပြီးတော့  ထိုင်းမှာ ၂နှစ် နေခဲ့တယ်။"
Watashi wa Nihon ni 17-nenkan sunde imasu. Soshite, watashi wa Tai de 2-nenkan sugoshimashita.
```

### Dictionary mode အနေနဲ့လည်း Google Translate ကို သုံးနိုင်တယ်

```
lar@lar-air:~/tool/translate-shell$ trans -d fr:my mot
mot

စကားလုံး
(hcakarrlone)

Translations of mot
[ Français -> မြန်မာစာ ]

noun
    Groupe de lettres formant une ou plusieurs syllabes et exprimant une idée.
        - "Le mot oui est un mot de trois lettres ."

    Courte lettre.
        - "J’ai reçu un mot de lui qui m’apprenait son départ ."

Synonyms
    noun
        - discussion, parole, délibération, propos
        - parole, terme
        - bon mot, mot d'esprit, bon
        - parole, mot de passe
        - parole, dire, terme

Examples
    - J’ai reçu un ot de lui qui m’apprenait son départ .
```

## Dictionary + brief mode

```
lar@lar-air:~/tool/translate-shell$ trans -d -b fr:my mot
စကားလုံး
```

## Language Identification

```
lar@lar-air:~/tool/translate-shell$ trans -id 言葉
日本語
Name                  Japanese
Family                Japonic
Writing system        Japanese (Han + Hiragana + Katakana)
Code                  ja
ISO 639-3             jpn
SIL                   http://www-01.sil.org/iso639-3/documentation.asp?id=jpn
Glottolog             http://glottolog.org/resource/languoid/id/nucl1643
Wikipedia             http://en.wikipedia.org/wiki/Japanese_language
lar@lar-air:~/tool/translate-shell$ trans -id ပါပါ
မြန်မာစာ
Name                  Myanmar
Family                Sino-Tibetan
Writing system        Myanmar
Code                  my
ISO 639-3             mya
SIL                   http://www-01.sil.org/iso639-3/documentation.asp?id=mya
Glottolog             http://glottolog.org/resource/languoid/id/nucl1310
Wikipedia             http://en.wikipedia.org/wiki/Myanmar_language
```

## TTS

```
lar@lar-air:~/tool/translate-shell$ trans -b -p :my "I miss you my dear."
ငါနင့်ကိုချစ်တယ်

lar@lar-air:~/tool/translate-shell$ trans -b -p :ja "I miss you my dear."
愛しい人、私はあなたに会いたいです。

lar@lar-air:~/tool/translate-shell$ trans -p :ja "I miss you my dear."
I miss you my dear.

愛しい人、私はあなたに会いたいです。
(Itoshī hito, watashi wa anata ni aitaidesu.)

Translations of I miss you my dear.
[ English -> 日本語 ]

I miss you my dear.
    愛しい人、私はあなたに会いたいです。, あなたが恋しいです。, あなたがいなくて寂しいです。, 私はあなたに私の愛するを欠場します。
```

## Interactive Translation Shell

```
lar@lar-air:~/tool/translate-shell$ trans -shell en:ja
Translate Shell
(:q to quit)
English> text editor
text editor

テキストエディタ
(Tekisutoedita)

Translations of text editor
[ English -> 日本語 ]

text editor
    テキストエディタ, テキストエディター

English> National Geographic
National Geographic

ナショナル・ジオグラフィック
(Nashonaru jiogurafikku)

Translations of National Geographic
[ English -> 日本語 ]

National Geographic
    ナショナル・ジオグラフィック, ナショナルジオグラフィック

English> 
```

## Interactive shell + TTS

```
lar@lar-air:~/tool/translate-shell$ trans -shell -p -b en:ja
Translate Shell
(:q to quit)
English> COVID-19 is a virus.
COVID-19はウイルスです。
English> I miss Thai foods.
タイ料理が恋しいです。
English> I might kick you. Are you OK my friend? Look at me!!!
キックするかもしれません。大丈夫？私を見て！！！
English> 
```

## Integration with Text Editor

```
https://github.com/VincentCordobes/vim-translate
```

## Testing with emacs

```
lar@lar-air:~/tool/translate-shell$ trans -emacs

Translate Shell
(:q to quit)
> hello
hello
/heˈlō,həˈlō/

noun
    an utterance of “hello”; a greeting.
        - "Colin Spencer still stood by the desk no one signed in at; and he still smiled and nodded his hellos and goodbyes to every oblivious face that passed him by as though he was host to this year's biggest A-list birthday bash."

exclamation
    used as a greeting or to begin a telephone conversation.
        - "But instead of a normal greeting like saying hello or something, they hugged."
    Synonyms: hi, howdy, hey, hiya, ciao, aloha

verb
    say or shout “hello”; greet someone.
        - "After all the helloing and such, he would sit down and talk to me in a gruff, military kind of way."

Synonyms
    noun
        - hullo, hi, how-do-you-do, howdy

    exclamation
        - hi, howdy, hey, hiya, ciao, aloha

Examples
    - She is living a more fortunate life than (most of) you, hello?

    - My second thought is, hello, it's still snowing!

    - The girl is finding love on the telephone, hello!

    - ‘Oh, hello,’ she said acting surprised to see the four boys staring at her.

    - hello, is anybody in?

    - It was a pleasant surprise when Sheila Sheridan came over to say hello.

    - I mean - hello- this is just kind of a witty, fun movie.

    - Over the last two days I have been flooded with porn site IMs… hello!

    - If you haven't met Joy yet, pop over to her site and say hello!

    - When their eyes met, she grinned wickedly in an informal hello.

    - Logan didn't say hello, but I hadn't expected a greeting.

    - Umm… hello, the world just ended, everyone seems bizarrely unaffected, like the predicted deep freeze has already reached their brains.

    - We didn't get the chance to get together this visit, but we had nice phone conversation and a waved hello.

    - I thought it summed up what I wanted to say and it also is a way to say hello!

    - ‘Oh, hello,’ she'd said to Brett, evidently surprised to see him standing in her kitchen with her daughter.

    - They sit in classrooms and cannot hear the teachers so, hello, it is no surprise that we are unable to get good outcomes from our education system.

    - She turned down the offer to sing the theme to the TV show… hello!

    - She must have been really stupid to have mimicked me… I mean, hello!

    - My local Chinese shop owner always greets me with a big smile and a friendly hello!

    - hello! did you even get what the play was about?

    - But instead of a normal greeting like saying hello or something, they hugged.

    - Every gathering she beds another partner who isn't her husband, hello!

    - You are supposed to be able to keep up with my voice, hello!

    - hello, what's this?

    - Tlingit people do not use such greetings as hello, good-bye, good afternoon, or good evening.

    - hello, what's all this then?

    - Ships' horns toot, children wave and call hello, and every morning you're awakened by the haunting call of the muezzin from some distant village mosque.

    - I have wanted to re-watch it like a DVD or something, but I couldn't because, hello!

    - It is extraordinary how much can be achieved when you put enthusiasm into a routine task, a special project or a simple hello or conversation.

    - Excuse him for picking that awful blue hue - I had always told him to let me pick the color to match with his chestnut-blondish hair, but hello!
```

```
> en:my
English> Please go away my friend
Please go away my friend

ကျေးဇူးပြုပြီးသူငယ်ချင်း
(kyaayyjuupyupyee suungaalhkyinn)

Translations of Please go away my friend
[ English -> မြန်မာစာ ]

Please go away my friend
    ကျေးဇူးပြုပြီးသူငယ်ချင်း, ကြှနျတေျာ့မိတျဆှေသွား ကျေးဇူးပြု.

English> Get out!
Get out!

ထွက်သွား!
(htwatswarr!)

Translations of Get out!
[ English -> မြန်မာစာ ]

Get out!
    ထွက်သွား!, ထွက်သွားပါ!, ထွက်ကြ!, ထွက်ရယူပါ!

English> So do I
So do I

ကျွန်တော်လဲထိုအတိုင်းပဲ
(kyawantawlell hto aatinepell)

Translations of So do I
[ English -> မြန်မာစာ ]

So do I
    ကျွန်တော်လဲထိုအတိုင်းပဲ, ငါလည်းလုပ်တယ်, ဒါနဲ့ပြုပါ

English> come to me
come to me

ကျွန်တော့်ဆီလာပါ
(kyawantaw se larpar)

Translations of come to me
[ English -> မြန်မာစာ ]

come to me
    ကျွန်တော့်ဆီလာပါ, ငါ့ထံသို့လာကြ, ငါ့ထံသို့လာ

English> 
```

## testing with emacs

```
မြန်မာစာ> မောင်မောင် နဲ့ အောင်အောင် က ညီအကို တွေ ဖြစ်ကြပါသည်
မောင်မောင် နဲ့ အောင်အောင် က ညီအကို တွေ ဖြစ်ကြပါသည်
(maungmaung nae aaungaaung k nyeaako tway  hpyitkyaparsai)

マウンマウンとアウンアウンは兄弟です
(Maunmaun to aun'aun wa kyōdaidesu)

Translations of မောင်မောင် နဲ့ အောင်အောင် က ညီအကို တွေ ဖြစ်ကြပါသည်
[ မြန်မာစာ -> 日本語 ]

မောင်မောင် နဲ့ အောင်အောင် က ညီအကို တွေ ဖြစ်ကြပါသည်
    マウンマウンとアウンアウンは兄弟です, マウン・マウンとしている成功した同胞

မြန်မာစာ> 

```

## Testing with Bing and Yandex Engines

TTS မှာ ပြောတဲ့ အသံရဲ့ male, female ရွေးတာ လုပ်လို့ရတယ်။

```
lar@lar-air:~/tool/translate-shell$ trans -e yandex "Ничего, были бы кости, а мясо будет" -sp -n f
Ничего, были бы кости, а мясо будет
(nichego, by`li by` kosti, a myaso budet)

Nothing, there would be bones, but meat will be

[ Русский -> English ]
lar@lar-air:~/tool/translate-shell$ trans -e yandex "Ничего, были бы кости, а мясо будет" -sp -n f
Ничего, были бы кости, а мясо будет
(nichego, by`li by` kosti, a myaso budet)

Nothing, there would be bones, but meat will be

[ Русский -> English ]
lar@lar-air:~/tool/translate-shell$ trans -e yandex "Ничего, были бы кости, а мясо будет" -sp -n f
[ERROR] Oops! Something went wrong and I can't translate it for you :(
lar@lar-air:~/tool/translate-shell$ trans -e yandex "Ничего, были бы кости, а мясо будет" -sp -n f
[ERROR] Oops! Something went wrong and I can't translate it for you :(
lar@lar-air:~/tool/translate-shell$ trans -e yandex "Ничего, были бы кости, а мясо будет" -sp -n m
[ERROR] Oops! Something went wrong and I can't translate it for you :(
lar@lar-air:~/tool/translate-shell$ trans -e yandex "Ничего, были бы кости, а мясо будет" -sp -n jane
[ERROR] Oops! Something went wrong and I can't translate it for you :(
lar@lar-air:~/tool/translate-shell$ trans -e bing "Why not test this thing" -sp -n US,m
Why not test this thing



[  -> English ]

lar@lar-air:~/tool/translate-shell$ trans -e bing "Why not test this thing" :yue -p -n m
Why not test this thing



[  -> 粵語 ]

lar@lar-air:~/tool/translate-shell$ trans -e bing "Why not test this thing" :yue -p -n f
[WARNING] Connection timed out. Retrying IPv4 connection.
Why not test this thing



[  -> 粵語 ]
```


**Google ထက်စာရင် Bing ရော Yandex ကောက translation လုပ်ပေးတာ နှေးတယ်။  
**Yandex က ပထမ ၃ခါလောက် ရပြီးတော့ နောက်ပိုင်း မရတော့ဘူး ?!?!  

```
lar@lar-air:~/tool/translate-shell$ trans -e google -b "Ничего, были бы кости, а мясо будет"  -sp -n f
Nothing, there would be bones, but meat would be
```

