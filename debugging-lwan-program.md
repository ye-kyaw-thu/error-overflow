# Debugging Lwan (Miss you) Program Log

ပရိုဂရမ်းမင်းကို တကယ် သိချင်လို့ မေးတာလား... တော့ မသိပါ။  
အောက်ပါ C++ code နဲ့ တူသော coding ကို debug လုပ်ပေးပါဆိုတဲ့ request ကို လက်ခံရရှိ...  

```c++
(base) ye@:~/4github$ cat ./lwan-err.cpp 
for(l=0;l<1500;l++)
Love=လွမ်းတယ်
{ cout<<Love;}
```

## Debugging lwan-err.cpp program

ကိုယ်တိုင်ကလည်း error ကိုတွေ့ရင် run လို့ရတဲ့အထိ debug လုပ်တဲ့ အကျင့်က ဖြစ်နေတော့... အမှားတွေကို ရှာကြည့်တဲ့အခါ အောက်ပါအတိုင်း တွေ့ရ...

- main function မပါတာ
- C++ မှာက variable type ကို အတိအကျ သတ်မှတ်ပေးရတယ် (e.g. string Love;)
- မြန်မာစာလုံး လွမ်းတယ် ကိုလည်း assignment လုပ်မယ် ဆိုရင် double quote အထဲမှာ ထည့်ပေးရမယ်။ (e.g. string Love="လွမ်းတယ်";)
- statement တိုင်းမှာ semicolon နဲ့ ပိတ်ပေးရမယ်
- for loop ပတ်တဲ့ လိုင်းမှာလည်း l ဆိုတာကို int ဆိုပြီးတော့ variable type အတိအကျ သတ်မှတ်ပေးရမယ်
- cout ကိုလည်း ဒီအတိုင်း ခေါ်သုံးချင်ရင် ပရိုဂရမ်ရဲ့ ထိပ်ဆုံးမှာ "using namespace std;" ဆိုတဲ့ စာကြောင်းကို C++ မှာက ထည့်ပေးရတယ်။
- တကယ်က cout ဆိုတဲ့ object ကို သုံးဖို့အတွက်က iostream header ကို ထိ်ပဆုံးမှာ declare လုပ်ထားမှ သုံးလို့ ရမှာမို့ "#include <iostream>" ဆိုတဲ့ header declaration လုပ်ဖို့ လိုအပ်ပါတယ်
- string တစ်ခုကို ရိုက်ထုတ်တဲ့အခါမှာ Enter ခေါက်ပေးဖို့အတွက် "\n" သို့မဟုတ် endl (C++ မှာ std::endl ဆိုတာက "\n" ကိုပါ ရိုက်ထုတ်ပေးတဲ့အပြင် output buffer ကိုပါ clear လုပ်ပေးတယ်)
- တကယ် C, C++ programmer အနေနဲ့က function အဆုံးမှာ return တစ်ခုခုလုပ်ကို လုပ်ပေးလေ့ရှိတယ်။ လက်ရှိ case မှာဆိုရင်တော့ "return 0;" ဆိုတာကို ရေးထည့်မှာ သေချာပါတယ်

အထက်ပါ အချက်တွေကြောင့် g++ နဲ့ lwan.cpp ကို compile လုပ်တဲ့အခါမှာ အောက်ပါလိုမျိုး error တွေ အများကြီး ထွက်လာပါလိမ့်မယ်။  

```bash
(base) ye@:~/4github$ g++ ./lwan.cpp 
./lwan.cpp: In function ‘int main()’:
./lwan.cpp:6:4: error: ‘string’ was not declared in this scope
    string Love="လွမ်းတယ်";
    ^~~~~~
./lwan.cpp:6:4: note: suggested alternative: ‘struct’
    string Love="လွမ်းတယ်";
    ^~~~~~
    struct
./lwan.cpp:9:7: error: ‘cout’ was not declared in this scope
       cout<<Love << endl;
       ^~~~
./lwan.cpp:9:13: error: ‘Love’ was not declared in this scope
       cout<<Love << endl;
             ^~~~
./lwan.cpp:9:21: error: ‘endl’ was not declared in this scope
       cout<<Love << endl;
                     ^~~~
./lwan.cpp:9:21: note: suggested alternative: ‘enum’
       cout<<Love << endl;
                     ^~~~
                     enum
(base) ye@:~/4github$ g++ ./lwan-err.cpp 
./lwan-err.cpp:2:6: error: stray ‘\341’ in program
 Love=���ွမ်းတယ်
      ^
./lwan-err.cpp:2:7: error: stray ‘\200’ in program
 Love=���ွမ်းတယ်
       ^
./lwan-err.cpp:2:8: error: stray ‘\234’ in program
 Love=��ွမ်းတယ်
        ^
./lwan-err.cpp:2:9: error: stray ‘\341’ in program
 Love=လ���မ်းတယ်
         ^
./lwan-err.cpp:2:10: error: stray ‘\200’ in program
 Love=လ���မ်းတယ်
          ^
./lwan-err.cpp:2:11: error: stray ‘\275’ in program
 Love=လ��မ်းတယ်
           ^
./lwan-err.cpp:2:12: error: stray ‘\341’ in program
 Love=လွ���်းတယ်
            ^
./lwan-err.cpp:2:13: error: stray ‘\200’ in program
 Love=လွ���်းတယ်
             ^
./lwan-err.cpp:2:14: error: stray ‘\231’ in program
 Love=လွ��်းတယ်
              ^
./lwan-err.cpp:2:15: error: stray ‘\341’ in program
 Love=လွမ���းတယ်
               ^
./lwan-err.cpp:2:16: error: stray ‘\200’ in program
 Love=လွမ���းတယ်
                ^
./lwan-err.cpp:2:17: error: stray ‘\272’ in program
 Love=လွမ��းတယ်
                 ^
./lwan-err.cpp:2:18: error: stray ‘\341’ in program
 Love=လွမ်���တယ်
                  ^
./lwan-err.cpp:2:19: error: stray ‘\200’ in program
 Love=လွမ်���တယ်
                   ^
./lwan-err.cpp:2:20: error: stray ‘\270’ in program
 Love=လွမ်��တယ်
                    ^
./lwan-err.cpp:2:21: error: stray ‘\341’ in program
 Love=လွမ်း���ယ်
                     ^
./lwan-err.cpp:2:22: error: stray ‘\200’ in program
 Love=လွမ်း���ယ်
                      ^
./lwan-err.cpp:2:23: error: stray ‘\220’ in program
 Love=လွမ်း��ယ်
                       ^
./lwan-err.cpp:2:24: error: stray ‘\341’ in program
 Love=လွမ်းတ���်
                        ^
./lwan-err.cpp:2:25: error: stray ‘\200’ in program
 Love=လွမ်းတ���်
                         ^
./lwan-err.cpp:2:26: error: stray ‘\232’ in program
 Love=လွမ်းတ��်
                          ^
./lwan-err.cpp:2:27: error: stray ‘\341’ in program
 Love=လွမ်းတယ���
                           ^
./lwan-err.cpp:2:28: error: stray ‘\200’ in program
 Love=လွမ်းတယ���
                            ^
./lwan-err.cpp:2:29: error: stray ‘\272’ in program
 Love=လွမ်းတယ��
                             ^
./lwan-err.cpp:1:1: error: expected unqualified-id before ‘for’
 for(l=0;l<1500;l++)
 ^~~
./lwan-err.cpp:1:9: error: ‘l’ does not name a type
 for(l=0;l<1500;l++)
         ^
./lwan-err.cpp:1:16: error: ‘l’ does not name a type
 for(l=0;l<1500;l++)
                ^
(base) ye@:~/4github$
```

## The Correct "lwan.cpp" C++ Code
                     
တကယ်တမ်း လွမ်းတယ်ဆိုတဲ့ စာကြောင်းကို အခါ ၁၅၀၀ ပေါ်ချင်ရင် C++ မှာဆိုရင် အောက်ပါအတိုင်း coding လုပ်ရပါလိမ့်မယ်။  
                     
```cpp
#include <iostream>
using namespace std;

int main() {

   string Love="လွမ်းတယ်";
   
   for(int l=0; l<1500; l++) {
      cout<<Love << endl;
   }
   return 0;
   
}                  
```
                        
## Compile and Run lwan.cpp
                    
အထက်ပါ ပြင်ထားတဲ့ code ကို compile လုပ်ပြီး run ကြည့်ရင် လွမ်းတယ်ဆိုတဲ့ စာကြောင်း အများကြီး ရိုက်ထုတ်ပေးတာကို တွေ့ရပါလိမ့်မယ်။  
                        
```sh
(base) ye@:~/4github$ g++ ./lwan.cpp 
(base) ye@:~/4github$ ./a.out | head
လွမ်းတယ်
လွမ်းတယ်
လွမ်းတယ်
လွမ်းတယ်
လွမ်းတယ်
လွမ်းတယ်
လွမ်းတယ်
လွမ်းတယ်
လွမ်းတယ်
လွမ်းတယ်
(base) ye@:~/4github$                     
```
                        
တကယ်က "လွမ်းတယ်" ဆိုတဲ့ စာကြောင်းကို အခါ ၁၅၀၀ ရိုက်ပေးသွားမှာပါ။ wc နဲ့ line count လုပ်ကြည့်ပြီး confirmation လုပ်လို့ရပါလိမ့်မယ်။  
                        
```sh
(base) ye@:~/4github$ ./a.out | wc
   1500    1500   37500
(base) ye@:~/4github$                       
```
