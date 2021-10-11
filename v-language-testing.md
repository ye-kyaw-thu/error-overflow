
## git clone v language

```
(base) ye@:~/tool$ git clone https://github.com/vlang/v
Cloning into 'v'...
remote: Enumerating objects: 101871, done.
remote: Counting objects: 100% (13/13), done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 101871 (delta 3), reused 2 (delta 0), pack-reused 101858
Receiving objects: 100% (101871/101871), 41.95 MiB | 1.93 MiB/s, done.
Resolving deltas: 100% (72797/72797), done.
(base) ye@:~/tool$ cd v
(base) ye@:~/tool/v$ ls
CHANGELOG.md  CODE_OF_CONDUCT.md  doc         Dockerfile.alpine  examples     LICENSE   Makefile   ROADMAP.md  thirdparty  vlib
cmd           CONTRIBUTING.md     Dockerfile  Dockerfile.cross   GNUmakefile  make.bat  README.md  TESTS.md    tutorials   v.mod
(base) ye@:~/tool/v$ 
```

```
(base) ye@:~/tool/v$ make
make fresh_vc
make[1]: Entering directory '/home/ye/tool/v'
rm -rf ./vc
git clone --depth 1 --quiet --single-branch https://github.com/vlang/vc ./vc
make[1]: Leaving directory '/home/ye/tool/v'
cd ./vc && git clean -xf && git pull --quiet
make fresh_tcc
make[1]: Entering directory '/home/ye/tool/v'
rm -rf ./thirdparty/tcc
git clone --depth 1 --quiet --single-branch --branch thirdparty-linux-amd64 https://github.com/vlang/tccbin ./thirdparty/tcc
make[1]: Leaving directory '/home/ye/tool/v'
cd ./thirdparty/tcc && git clean -xf && git pull --quiet
cc  -std=gnu99 -w -I ./thirdparty/stdatomic/nix -o v1.exe ./vc/v.c -lm -lpthread 
./v1.exe -no-parallel -o v2.exe  cmd/v
./v2.exe -o ./v  cmd/v
rm -rf v1.exe v2.exe
V has been successfully built
V 0.2.4 1831ecc
(base) ye@:~/tool/v$ 
```

## Export v-path


```
(base) ye@:~/tool/v$ pwd
/home/ye/tool/v
(base) ye@:~/tool/v$ sudo gedit ~/.bashrc
```

```bash
# for v programming language
export PATH=$PATH:/home/ye/tool/v
```

```
(base) ye@:~/tool/v$ v --help
v: command not found
```

source ဆိုတဲ့ command ကို run ပေးမှ export လုပ်ထားတဲ့ path က active ဖြစ်လိမ့်မယ်။ source လုပ်ပြီးရင်တော့ v compiler ကို ဘယ် path အောက်ကပဲ ခေါ်ခေါ် ရပြီ...  

```
(base) ye@:~/tool/v$ source ~/.bashrc
(base) ye@:~/tool/v$ v --help
V is a tool for managing V source code.

Usage:
   v [options] [command] [arguments]

Examples:
   v hello.v                 Compile the file `hello.v` and output it as `hello` or `hello.exe`.
   v run hello.v             Same as above but also run the produced executable immediately after compilation.
   v -cg run hello.v         Same as above, but make debugging easier (in case your program crashes).
   v -o h.c hello.v          Translate `hello.v` to `h.c`. Do not compile further.
   v -o - hello.v            Translate `hello.v` and output the C source code to stdout. Do not compile further.

   v watch hello.v           Re-does the same compilation, when a source code change is detected.
                             The program is only compiled, not run.
   v watch run hello.v       Re-runs the same `hello.v` file, when a source code change is detected.

V supports the following commands:
* New project scaffolding:
   new               Setup the file structure for a V project (in a sub folder).
   init              Setup the file structure for an already existing V project.

* Ordinary development:
   run               Compile and run a V program.
   test              Run all test files in the provided directory.
   fmt               Format the V code provided.
   vet               Report suspicious code constructs.
   doc               Generate the documentation for a V module.
   vlib-docs         Generate and open the documentation of all the vlib modules.
   repl              Run the REPL.
   watch             Re-compile/re-run a source file, each time it is changed.

* Installation/self updating:
   symlink           Create a symbolic link for V.
   up                Run the V self-updater.
   self [-prod]      Run the V self-compiler, use -prod to optimize compilation.
   version           Print the version text and exits.

* Module/package management:
   install           Install a module from VPM.
   remove            Remove a module that was installed from VPM.
   search            Search for a module from VPM.
   update            Update an installed module from VPM.
   upgrade           Upgrade all the outdated modules.
   list              List all installed modules.
   outdated          List installed modules that need updates.
   show              Display information about a module on vpm

* Others:
   doctor            Display some useful info about your system to help reporting bugs.
   translate         Translate C code to V (coming soon in 0.3).
   tracev            Produce a tracing version of the v compiler.
                     Use `tracev yourfile.v` when the compiler panics.
                     NB: `tracev` is much slower and more verbose than ordinary `v`

Use "v help <command>" for more information about a command, example: `v help build`, `v help build-c`, `v help build-native`
Use "v help other" to see less frequently used commands.
Use "v help topics" to see a list of all known help topics.

Note: Help is required to write more help topics.
Only build, new, init, doc, fmt, vet, run, test, watch, search, install, remove, update, bin2v, check-md are properly documented currently.

(base) ye@:~/tool/v$
```

အထက်မှာ လုပ်ပြခဲ့တာက Linux  OS မှာ ပုံမှန် program အသစ် တစ်ခုကို install လုပ်ပြီးရင် ဘယ်နေရာကနေ ခေါ်ခေါ် သိအောင် လုပ်တဲ့ ပုံစံပါ။  
တကယ်က v မှာက ပိုပြီး လွယ်တဲ့ လုပ်တဲ့နည်းရှိပါတယ်။ အဲဒါက အောက်ပါ command ကို run ယုံပါပဲ...  

```
sudo ./v symlink
```

## Testing v compiler

self compile လုပ်တဲ့ feature ပါတယ်။  

```
(base) ye@:~/tool/v$ v self
V self compiling ...
V built successfully!
(base) ye@:~/tool/v$ 
```

OK တယ်!!!  

Check the version...  

```
(base) ye@:~/tool/v/examples/ttf_font$ v version
V 0.2.4 1831ecc
```

## write a Hello-World! program with v language

```
(base) ye@:~/tool/v$ cat > nay-kaung-lar.v
println('နေကောင်းလား။')          
(base) ye@:~/tool/v$
```

```
(base) ye@:~/tool/v$ v run ./nay-kaung-lar.v 
နေကောင်းလား။
```

## Runing some examples of v

```
(base) ye@:~/tool/v/examples/game_of_life$ v run ./life.v 
```

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/game-of-life-with-v.png" alt="game-of-life terminal screen" width="800"/>  
</p>  
<div align="center">
  Fig.1 Game of Life running with v  
</div> 

<br />

```
(base) ye@:~/tool/v/examples/gg$ v run ./mandelbrot.v
```

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/mandelbrot-with-v-language.png" alt="mandelbrot-with-v-language" width="800"/>  
</p>  
<div align="center">
  Fig.1 Mandelbrot with v language  
</div> 

<br />

```
(base) ye@:~/tool/v/examples/ttf_font$ cp /usr/share/fonts/truetype/padauk/Padauk-Regular.ttf .
```

```
const (
	win_width  = 600
	win_height = 700
	bg_color   = gx.white
	font_paths = [
		os.resource_abs_path('Padauk-Regular.ttf'),
		os.resource_abs_path('Padauk-Regular.ttf'),
	]
)
```

```
		block_txt:= "နေကောင်းလား!
I don't know the problem!
Why? ဘာဖြစ်တာလဲ?
Frame: $app.frame_c
Let's debug!!! :)
"
```

```
(base) ye@:~/tool/v/examples/ttf_font$ v run ./myfont_ttf.v 
```

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/testing-with-myanmar-font.png" alt="Padauk-font-testing-with-v-language" width="800"/>  
</p>  
<div align="center">
  Fig.1 Myanmar font (Padauk) testing with v language  
</div> 

<br />

```
(base) ye@:~/tool/v/examples/sokol/sounds$ v run ./wav_player.v 
Usage: play_wav file1.wav file2.wav ...
> play_wav_file: /home/ye/tool/v/examples/sokol/sounds/uhoh.wav
```

```
(base) ye@:~/tool/v/examples$ time v run ./fibonacci.v 
2
1
2
3
5
8
13
21
34
55
89
144
233
377
610
987
1597
2584
4181
6765
10946
17711
28657
46368

real	0m0.097s
user	0m0.094s
sys	0m0.029s
(base) ye@:~/tool/v/examples$ 
```

## V for Bash script developers

```
(base) ye@:~/tool/v/examples$ cat ./tst.vsh
#!/usr/local/bin/v run

for _ in 0 .. 3 {
	println('Hello! V script')
}

(base) ye@:~/tool/v/examples$ chmod +x ./tst.vsh
(base) ye@:~/tool/v/examples$ ./tst.vsh 
bash: ./tst.vsh: /usr/local/bin/v: bad interpreter: No such file or directory
(base) ye@:~/tool/v/examples$ which v
/home/ye/tool/v/v
```

```
(base) ye@:~/tool/v$ sudo ./v symlink
[sudo] password for ye: 
(base) ye@:~/tool/v$ cd examples/
(base) ye@:~/tool/v/examples$ ./tst.vsh 
Hello! V script
Hello! V script
Hello! V script
(base) ye@:~/tool/v/examples$
```
