# eigen Cloning Error

git cloning လုပ်တဲ့အခါမှာ တစ်ခါတလေ https နဲ့ အဆင်မပြေတာမျိုးဖြစ်တတ်ပါတယ်။  
ဥပမာအနေနဲ့ eigen ကို cloning လုပ်တဲ့အခါမှာ တွေ့ရတဲ့ error ကိုပြထားပါတယ်။  
```
(base) ye@ykt-pro:/media/ye/project1/tool$ git clone https://gitlab.com/libeigen/eigen.git
Cloning into 'eigen'...
remote: Enumerating objects: 14, done.
remote: Counting objects: 100% (14/14), done.
remote: Compressing objects: 100% (14/14), done.
error: RPC failed; curl 56 GnuTLS recv error (-110): The TLS connection was non-properly terminated.
fatal: The remote end hung up unexpectedly
fatal: early EOF
fatal: index-pack failed
```

Solution ကတော့ရှင်းပါတယ်။  
https ကို http အဖြစ်ပြောင်းပေးလိုက်ပါ။  
```
(base) ye@ykt-pro:/media/ye/project1/tool$ git clone http://gitlab.com/libeigen/eigen.git
Cloning into 'eigen'...
warning: redirecting to https://gitlab.com/libeigen/eigen.git/
remote: Enumerating objects: 14, done.
remote: Counting objects: 100% (14/14), done.
remote: Compressing objects: 100% (14/14), done.
remote: Total 107301 (delta 4), reused 0 (delta 0), pack-reused 107287
Receiving objects: 100% (107301/107301), 101.69 MiB | 517.00 KiB/s, done.
Resolving deltas: 100% (87836/87836), done.
Checking out files: 100% (1768/1768), done.
(base) ye@ykt-pro:/media/ye/project1/tool$ 
```

## Reference

http://eigen.tuxfamily.org/index.php?title=Main_Page
https://stackoverflow.com/questions/38378914/how-to-fix-git-error-rpc-failed-curl-56-gnutls

