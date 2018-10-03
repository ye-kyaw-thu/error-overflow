# Notes relating to installation of sndpeek

## in English:
Just note of how I fixed installation error of sndpeek.
Link of sndpeek: 
http://soundlab.cs.princeton.edu/software/sndpeek/

## in Myanmar language:
sndpeek ပရိုဂရမ်ကို installation လုပ်စဉ်မှာ တွေ့ရတဲ့ error ကို ဘယ်လိုပုံစံနဲ့ ဖြေရှင်းခဲ့ရတယ်ဆိုတဲ့ note ပါ။


make linux-alsa လုပ်စဉ်မှာ တွေ့ရတဲ့ error တွေဖြစ်ပါတယ်။  
အောက်ပါအတိုင်းပါ။  

``` bash
#I also tried with adding LDFLAG as follows:

(py3.6.5) lar@lar-air:~/experiment/audio-image-classification/tool/sndpeek-1.4/src/sndpeek$ make linux-alsa 'LDFLAG=-L/usr/lib/x86_64-linux-gnu/'
make -f makefile.alsa
make[1]: Entering directory '/home/lar/experiment/audio-image-classification/tool/sndpeek-1.4/src/sndpeek'
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c chuck_fft.c
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c RtAudio.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c Thread.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c sndpeek.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c Stk.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/Centroid.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/DownSampler.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/Flux.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/LPC.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/MFCC.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/RMS.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/Rolloff.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/System.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/fvec.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/AutoCorrelation.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/Communicator.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/Hamming.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/MagFFT.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/NormRMS.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/MarSignal.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/fmatrix.cpp
g++ -o sndpeek chuck_fft.o RtAudio.o Thread.o sndpeek.o Stk.o Centroid.o DownSampler.o Flux.o LPC.o MFCC.o RMS.o Rolloff.o System.o fvec.o AutoCorrelation.o Communicator.o Hamming.o MagFFT.o NormRMS.o MarSignal.o fmatrix.o -L/usr/X11R6/lib -lglut -lGL -lGLU -lasound -lXmu -lX11 -lXext -lXi -lm -lsndfile
/usr/bin/ld: cannot find -lsndfile
collect2: error: ld returned 1 exit status
makefile.alsa:15: recipe for target 'sndpeek' failed
make[1]: *** [sndpeek] Error 1
make[1]: Leaving directory '/home/lar/experiment/audio-image-classification/tool/sndpeek-1.4/src/sndpeek'
makefile:20: recipe for target 'linux-alsa' failed
make: [linux-alsa] Error 2 (ignored)
```

```bash
(py3.6.5) lar@lar-air:~/experiment/audio-image-classification/tool/sndpeek-1.4/src/sndpeek$ sudo apt-get install libsndfile-dev
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Note, selecting 'libsndfile1-dev' instead of 'libsndfile-dev'
The following packages were automatically installed and are no longer required:
  linux-headers-4.15.0-33 linux-headers-4.15.0-33-generic linux-image-4.15.0-33-generic linux-modules-4.15.0-33-generic
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  libflac-dev libflac8 libogg-dev libvorbis-dev
The following NEW packages will be installed:
  libflac-dev libogg-dev libsndfile1-dev libvorbis-dev
The following packages will be upgraded:
  libflac8
1 upgraded, 4 newly installed, 0 to remove and 199 not upgraded.
Need to get 1,616 kB of archives.
After this operation, 7,286 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://ppa.launchpad.net/jonathonf/ffmpeg-3/ubuntu xenial/main amd64 libflac8 amd64 1.3.2-1~16.04.york0 [220 kB]
Get:2 http://jp.archive.ubuntu.com/ubuntu xenial/main amd64 libogg-dev amd64 1.3.2-1 [156 kB]
Get:3 http://jp.archive.ubuntu.com/ubuntu xenial-updates/main amd64 libvorbis-dev amd64 1.3.5-3ubuntu0.2 [322 kB]                                     
Err:3 http://security.ubuntu.com/ubuntu xenial-security/main amd64 libvorbis-dev amd64 1.3.5-3ubuntu0.2                                               
  Connection failed
Get:4 http://jp.archive.ubuntu.com/ubuntu xenial-updates/main amd64 libsndfile1-dev amd64 1.0.25-10ubuntu0.16.04.1 [647 kB]                           
Get:3 http://security.ubuntu.com/ubuntu xenial-security/main amd64 libvorbis-dev amd64 1.3.5-3ubuntu0.2 [322 kB]                                      
Get:5 http://ppa.launchpad.net/jonathonf/ffmpeg-3/ubuntu xenial/main amd64 libflac-dev amd64 1.3.2-1~16.04.york0 [270 kB]                             
Fetched 1,465 kB in 3min 58s (6,145 B/s)                                                                                                              
(Reading database ... 362771 files and directories currently installed.)
Preparing to unpack .../libflac8_1.3.2-1~16.04.york0_amd64.deb ...
Unpacking libflac8:amd64 (1.3.2-1~16.04.york0) over (1.3.1-4) ...
Selecting previously unselected package libogg-dev:amd64.
Preparing to unpack .../libogg-dev_1.3.2-1_amd64.deb ...
Unpacking libogg-dev:amd64 (1.3.2-1) ...
Selecting previously unselected package libflac-dev:amd64.
Preparing to unpack .../libflac-dev_1.3.2-1~16.04.york0_amd64.deb ...
Unpacking libflac-dev:amd64 (1.3.2-1~16.04.york0) ...
Selecting previously unselected package libvorbis-dev:amd64.
Preparing to unpack .../libvorbis-dev_1.3.5-3ubuntu0.2_amd64.deb ...
Unpacking libvorbis-dev:amd64 (1.3.5-3ubuntu0.2) ...
Selecting previously unselected package libsndfile1-dev.
Preparing to unpack .../libsndfile1-dev_1.0.25-10ubuntu0.16.04.1_amd64.deb ...
Unpacking libsndfile1-dev (1.0.25-10ubuntu0.16.04.1) ...
Processing triggers for libc-bin (2.23-0ubuntu10) ...
Processing triggers for doc-base (0.10.7) ...
Processing 2 added doc-base files...
Setting up libflac8:amd64 (1.3.2-1~16.04.york0) ...
Setting up libogg-dev:amd64 (1.3.2-1) ...
Setting up libflac-dev:amd64 (1.3.2-1~16.04.york0) ...
Setting up libvorbis-dev:amd64 (1.3.5-3ubuntu0.2) ...
Setting up libsndfile1-dev (1.0.25-10ubuntu0.16.04.1) ...
Processing triggers for libc-bin (2.23-0ubuntu10) ...

```

I got one more Error Message:  
(နောက်ထပ် error တစ်ခု ရှင်းဖို့ကျန်)  

```bash
(py3.6.5) lar@lar-air:~/experiment/audio-image-classification/tool/sndpeek-1.4/src/sndpeek$ make linux-alsa
make -f makefile.alsa
make[1]: Entering directory '/home/lar/experiment/audio-image-classification/tool/sndpeek-1.4/src/sndpeek'
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c chuck_fft.c
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c RtAudio.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c Thread.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c sndpeek.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c Stk.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/Centroid.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/DownSampler.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/Flux.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/LPC.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/MFCC.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/RMS.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/Rolloff.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/System.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/fvec.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/AutoCorrelation.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/Communicator.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/Hamming.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/MagFFT.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/NormRMS.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/MarSignal.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/fmatrix.cpp
g++ -o sndpeek chuck_fft.o RtAudio.o Thread.o sndpeek.o Stk.o Centroid.o DownSampler.o Flux.o LPC.o MFCC.o RMS.o Rolloff.o System.o fvec.o AutoCorrelation.o Communicator.o Hamming.o MagFFT.o NormRMS.o MarSignal.o fmatrix.o -L/usr/X11R6/lib -lglut -lGL -lGLU -lasound -lXmu -lX11 -lXext -lXi -lm -lsndfile
/usr/bin/ld: Thread.o: undefined reference to symbol 'pthread_cancel@@GLIBC_2.2.5'
//lib/x86_64-linux-gnu/libpthread.so.0: error adding symbols: DSO missing from command line
collect2: error: ld returned 1 exit status
makefile.alsa:15: recipe for target 'sndpeek' failed
make[1]: *** [sndpeek] Error 1
make[1]: Leaving directory '/home/lar/experiment/audio-image-classification/tool/sndpeek-1.4/src/sndpeek'
makefile:20: recipe for target 'linux-alsa' failed
make: [linux-alsa] Error 2 (ignored)

```

I edited makefile.alsa as follows:
(makefile.als ကို အောက်ပါအတိုင်း ဝင်ပြင်ခဲ့တယ်)

```bash
(py3.6.5) lar@lar-air:~/experiment/audio-image-classification/tool/sndpeek-1.4/src/sndpeek$ vi makefile.alsa

#LIBS=-L/usr/X11R6/lib -lglut -lGL -lGLU -lasound -lXmu -lX11 -lXext -lXi -lm -lsndfile
LIBS=-L/usr/X11R6/lib -lglut -lGL -lGLU -lasound -lXmu -lX11 -lXext -lXi -lm -lsndfile -lusb-1.0 -l pthread
```

Error fixed!!! :)
(ဒီတစ်ခါတော့ make linux-alsa က error မပေးတော့ပိုင်း compile လုပ်သွားပါပြီ)

```bash
(py3.6.5) lar@lar-air:~/experiment/audio-image-classification/tool/sndpeek-1.4/src/sndpeek$ make clean
rm -f *.o 
(py3.6.5) lar@lar-air:~/experiment/audio-image-classification/tool/sndpeek-1.4/src/sndpeek$ make linux-alsa
make -f makefile.alsa
make[1]: Entering directory '/home/lar/experiment/audio-image-classification/tool/sndpeek-1.4/src/sndpeek'
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c chuck_fft.c
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c RtAudio.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c Thread.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c sndpeek.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c Stk.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/Centroid.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/DownSampler.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/Flux.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/LPC.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/MFCC.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/RMS.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/Rolloff.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/System.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/fvec.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/AutoCorrelation.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/Communicator.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/Hamming.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/MagFFT.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/NormRMS.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/MarSignal.cpp
gcc -D__LINUX_ALSA__ -D__LITTLE_ENDIAN__ -I../marsyas/ -O3 -c ../marsyas/fmatrix.cpp
g++ -o sndpeek chuck_fft.o RtAudio.o Thread.o sndpeek.o Stk.o Centroid.o DownSampler.o Flux.o LPC.o MFCC.o RMS.o Rolloff.o System.o fvec.o AutoCorrelation.o Communicator.o Hamming.o MagFFT.o NormRMS.o MarSignal.o fmatrix.o -L/usr/X11R6/lib -lglut -lGL -lGLU -lasound -lXmu -lX11 -lXext -lXi -lm -lsndfile -lusb-1.0 -l pthread
make[1]: Leaving directory '/home/lar/experiment/audio-image-classification/tool/sndpeek-1.4/src/sndpeek'

```

Yae! I got sndpeek!
(sndpeek ကို run လို့ရပါပြီ)

```bash

(py3.6.5) lar@lar-air:~/experiment/audio-image-classification/tool/sndpeek-1.4/src/sndpeek$ ls
AutoCorrelation.o  Communicator.o  Hamming.o      makefile.jack   MFCC.o       RtAudio.h    sndpeek.dsw  Stk.o       util_sndfile.c
Centroid.o         DownSampler.o   LPC.o          makefile.oss    NormRMS.o    RtAudio.o    sndpeek.o    System.o    util_sndfile.h
chuck_fft.c        Flux.o          MagFFT.o       makefile.osx    RMS.o        sndpeek      sndpeek.opt  Thread.cpp
chuck_fft.h        fmatrix.o       makefile       makefile.win32  Rolloff.o    sndpeek.cpp  Stk.cpp      Thread.h
chuck_fft.o        fvec.o          makefile.alsa  MarSignal.o     RtAudio.cpp  sndpeek.dsp  Stk.h        Thread.o

```
```
./sndpeek
```

<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/Arr-sound-of-Myanmar-language.png" alt="Visualization of sylbreak RE" width="1440x900"/>
<p align="center"> Fig. Realtime 3D animated Myanmar syllable "အား" (a:) </p>  
