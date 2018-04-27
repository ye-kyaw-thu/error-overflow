# Unmet Dependencies Error

# in English:
Relating to unmet dependencies error when trying to install a program or a libray ...
You know, sometimes we have to read the error message carefully.
You can solve with **sudo apt --fix-broken instal**

# in Myanmar language:
Linux OS မှာ application တစ်ခုခု သို့မဟုတ် library တစ်ခုခုကို installation လုပ်တဲ့ အခါမှာ Unmet dependencies error ဆိုတာမျိုး ဖြစ်တဲ့အခါ ဖြေရှင်းပုံဖြေရှင်းနည်း တစ်ခု ကို မိတ်ဆက်ပေးပါမယ်။ ဒီ error က ကိုယ် install လုပ်ချင်တဲ့ application သို့မဟုတ် library က  


```bash
$ sudo apt-get install librubberband-dev
Reading package lists... Done
Building dependency tree       
Reading state information... Done
You might want to run 'apt-get -f install' to correct these:
The following packages have unmet dependencies:
 librubberband-dev : Depends: librubberband2v5 (= 1.8.1-6ubuntu2) but it is not going to be installed
 sonic-visualiser : Depends: libfishsound1 but it is not going to be installed
                    Depends: jackd but it is not going to be installed
                    Depends: liblo7 but it is not going to be installed
                    Depends: liblrdf0 but it is not going to be installed
                    Depends: liboggz2 but it is not going to be installed
                    Depends: librubberband2v5 but it is not going to be installed
                    Depends: libsord-0-0 but it is not going to be installed
E: Unmet dependencies. Try 'apt-get -f install' with no packages (or specify a solution).
```

