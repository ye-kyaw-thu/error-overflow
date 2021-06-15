# Singularity Version 3.6.3 Installation

Singularity site က ညွှန်ကြားထားတဲ့ အောက်ပါ quick-start အတိုင်း installation လုပ်ပေမဲ့ error တက်လာတာကို ဖြေရှင်းတဲ့ note ပါ။  
[https://sylabs.io/guides/3.0/user-guide/quick_start.html](https://sylabs.io/guides/3.0/user-guide/quick_start.html)

***Error ကို မလေ့လာချင်ပဲ အဆင်ပြေတဲ့ installation step တွေကိုပဲ တန်းသွားချင်ရင်တော့ Page Down တော်တော်လေး လုပ်သွားပြီး ERROR!!! နောက်ပိုင်းက အဆင့်တွေကနေပဲ စလုပ်သွားပါ။***  

## Installation of Go

https://golang.org/doc/install  
Download go tar file.  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/Downloads$ sudo rm -rf /usr/local/go
[sudo] password for ye: 
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/Downloads$ sudo tar -C /usr/local -xzf go1.16.5.linux-amd64.tar.gz
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/Downloads$ export PATH=$PATH:/usr/local/go/bin
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/Downloads$ go version
go version go1.16.5 linux/amd64
```

## Installation of Singularity

https://sylabs.io/guides/3.0/user-guide/quick_start.html  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/Downloads$ which go
/usr/local/go/bin/go
```

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/Downloads$ cd /usr/local/go/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/usr/local/go$ ls
api  AUTHORS  bin  CONTRIBUTING.md  CONTRIBUTORS  doc  favicon.ico  lib  LICENSE  misc  PATENTS  pkg  README.md  robots.txt  SECURITY.md  src  test  VERSION
```

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/usr/local/go$ cd src
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/usr/local/go/src$ ls
all.bash  bootstrap.bash  bytes       cmd        context   embed     flag    go.sum  index     make.bash  math  path       README.vendor  run.bat  strconv  testdata  unicode
all.bat   bufio           clean.bash  cmp.bash   crypto    encoding  fmt     hash    internal  make.bat   mime  plugin     reflect        run.rc   strings  testing   unsafe
all.rc    buildall.bash   clean.bat   compress   database  errors    go      html    io        Make.dist  net   race.bash  regexp         runtime  sync     text      vendor
archive   builtin         clean.rc    container  debug     expvar    go.mod  image   log       make.rc    os    race.bat   run.bash       sort     syscall  time
```

## Clone the Singularity repository

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/usr/local/go/src$ sudo mkdir -p github.com/sylabs
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/usr/local/go/src$ cd github.com/sylabs/

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/usr/local/go/src/github.com/sylabs$ sudo git clone https://github.com/sylabs/singularity.git
Cloning into 'singularity'...
remote: Enumerating objects: 95087, done.
remote: Counting objects: 100% (786/786), done.
remote: Compressing objects: 100% (387/387), done.
remote: Total 95087 (delta 380), reused 742 (delta 350), pack-reused 94301
Receiving objects: 100% (95087/95087), 30.84 MiB | 14.27 MiB/s, done.
Resolving deltas: 100% (60565/60565), done.
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/usr/local/go/src/github.com/sylabs$

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/usr/local/go/src/github.com/sylabs$ cd singularity/
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/usr/local/go/src/github.com/sylabs/singularity$ ls
CHANGELOG.md  CONTRIBUTING.md  COPYRIGHT.md  docs  etc       go.mod  INSTALL.md  LICENSE-APACHE-2.0  LICENSE.md  mconfig  NOTICE-APACHE-2.0  README.md  SUPPORT.md
cmd           CONTRIBUTORS.md  dist          e2e   examples  go.sum  internal    LICENSE-LBNL.md     makeit      mlocal   pkg                scripts
```

## Install Go dependencies

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/usr/local/go/src/github.com/sylabs/singularity$ go get -u -v github.com/golang/dep/cmd/dep
go: downloading github.com/golang/dep v0.5.4
go: downloading github.com/pkg/errors v0.9.1
go: downloading golang.org/x/sync v0.0.0-20210220032951-036812b2e83c
go: downloading github.com/armon/go-radix v0.0.0-20180808171621-7fddfc383310
go: downloading github.com/pelletier/go-toml v1.9.2
go: downloading github.com/golang/protobuf v1.5.2
go: downloading golang.org/x/sys v0.0.0-20210514084401-e8d321eab015
go: downloading gopkg.in/yaml.v2 v2.4.0
go: downloading google.golang.org/protobuf v1.26.0
go: downloading github.com/pelletier/go-toml v1.9.3
go: downloading golang.org/x/sys v0.0.0-20210615035016-665e8c7367d1
go: downloading github.com/armon/go-radix v1.0.0
go: downloading github.com/boltdb/bolt v1.3.1
go: downloading github.com/Masterminds/semver v1.5.0
go: downloading github.com/Masterminds/vcs v1.13.1
go: downloading github.com/jmank88/nuts v0.4.0
go: downloading github.com/sdboyer/constext v0.0.0-20170321163424-836a14457353
go: downloading github.com/nightlyone/lockfile v1.0.0
google.golang.org/protobuf/internal/flags
google.golang.org/protobuf/internal/set
golang.org/x/sys/internal/unsafeheader
google.golang.org/protobuf/internal/pragma
github.com/armon/go-radix
github.com/golang/dep/gps/paths
github.com/sdboyer/constext
golang.org/x/sync/errgroup
github.com/Masterminds/semver
golang.org/x/sys/unix
github.com/boltdb/bolt
google.golang.org/protobuf/internal/detrand
google.golang.org/protobuf/internal/version
github.com/Masterminds/vcs
github.com/pkg/errors
google.golang.org/protobuf/internal/errors
github.com/golang/dep/gps/pkgtree
github.com/nightlyone/lockfile
github.com/pelletier/go-toml
google.golang.org/protobuf/encoding/protowire
github.com/golang/dep/internal/fs
google.golang.org/protobuf/reflect/protoreflect
gopkg.in/yaml.v2
github.com/jmank88/nuts
google.golang.org/protobuf/internal/encoding/messageset
google.golang.org/protobuf/internal/genid
google.golang.org/protobuf/internal/strs
google.golang.org/protobuf/runtime/protoiface
google.golang.org/protobuf/internal/order
google.golang.org/protobuf/internal/encoding/text
google.golang.org/protobuf/reflect/protoregistry
google.golang.org/protobuf/internal/descfmt
google.golang.org/protobuf/internal/descopts
google.golang.org/protobuf/proto
google.golang.org/protobuf/internal/encoding/defval
google.golang.org/protobuf/encoding/prototext
google.golang.org/protobuf/internal/filedesc
google.golang.org/protobuf/internal/encoding/tag
google.golang.org/protobuf/internal/impl
google.golang.org/protobuf/internal/filetype
google.golang.org/protobuf/runtime/protoimpl
google.golang.org/protobuf/types/descriptorpb
google.golang.org/protobuf/reflect/protodesc
github.com/golang/protobuf/proto
github.com/golang/dep/gps/internal/pb
github.com/golang/dep/gps
# github.com/golang/dep/gps
/home/ye/go/pkg/mod/github.com/golang/dep@v0.5.4/gps/constraint.go:103:21: cannot use sv (type *semver.Version) as type semver.Version in field value
/home/ye/go/pkg/mod/github.com/golang/dep@v0.5.4/gps/constraint.go:122:16: invalid type assertion: c.(semver.Version) (non-interface type *semver.Constraints on left)
/home/ye/go/pkg/mod/github.com/golang/dep@v0.5.4/gps/constraint.go:149:4: undefined: semver.Constraint
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/usr/local/go/src/github.com/sylabs/singularity$
```

## Compile the Singularity binary

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/usr/local/go/src/github.com/sylabs/singularity$ sudo ./mconfig 
Configuring for project `singularity-ce' with languages: C, Golang
=> running pre-basechecks project specific checks ...
=> running base system checks ...
 checking: host C compiler... cc
 checking: host C++ compiler... c++
 checking: host Go compiler (at least version 1.13)... not found!
mconfig: could not complete configuration
```

Checking ...  
version က 1.13 ထက် မြင့်နေလို့ ပေးတဲ့ message ပဲလို့ ထင်တယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/usr/local/go/src/github.com/sylabs/singularity$ go version
go version go1.16.5 linux/amd64
```

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/usr/local/go/src/github.com/sylabs/singularity$ make -C builddir
make: Entering directory '/usr/local/go/src/github.com/sylabs/singularity/builddir'
make: *** No targets specified and no makefile found.  Stop.
make: Leaving directory '/usr/local/go/src/github.com/sylabs/singularity/builddir'
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:/usr/local/go/src/github.com/sylabs/singularity$ sudo make -C builddir install
make: Entering directory '/usr/local/go/src/github.com/sylabs/singularity/builddir'
make: *** No rule to make target 'install'.  Stop.
make: Leaving directory '/usr/local/go/src/github.com/sylabs/singularity/builddir'
```
ERROR!!!  ERROR!!!   ERROR!!!    

==============


(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~$ sudo apt-get update && \
> sudo apt-get install -y build-essential \
> libseccomp-dev pkg-config squashfs-tools cryptsetup
Get:1 http://dl.google.com/linux/chrome/deb stable InRelease [1,811 B]
Get:2 http://dl.google.com/linux/chrome/deb stable/main amd64 Packages [1,101 B]                                                                  
Hit:3 https://packages.microsoft.com/repos/ms-teams stable InRelease                                                                                                                  
Hit:4 http://ppa.launchpad.net/sylvain-pineau/kazam/ubuntu groovy InRelease                                                                                                           
Get:5 http://security.ubuntu.com/ubuntu groovy-security InRelease [110 kB]                          
Hit:6 http://mm.archive.ubuntu.com/ubuntu groovy InRelease                                               
Ign:7 http://ppa.launchpad.net/videolan/stable-daily/ubuntu groovy InRelease                             
Get:8 http://mm.archive.ubuntu.com/ubuntu groovy-updates InRelease [115 kB]    
Err:9 http://ppa.launchpad.net/videolan/stable-daily/ubuntu groovy Release                                           
  404  Not Found [IP: 91.189.95.85 80]
Get:10 http://mm.archive.ubuntu.com/ubuntu groovy-backports InRelease [101 kB]                                       
Get:11 http://security.ubuntu.com/ubuntu groovy-security/main amd64 DEP-11 Metadata [18.8 kB]
Get:12 http://mm.archive.ubuntu.com/ubuntu groovy-updates/main i386 Packages [217 kB]
Get:13 http://security.ubuntu.com/ubuntu groovy-security/universe amd64 DEP-11 Metadata [4,620 B]
Get:14 http://mm.archive.ubuntu.com/ubuntu groovy-updates/main amd64 Packages [492 kB]
Get:15 http://mm.archive.ubuntu.com/ubuntu groovy-updates/main Translation-en [124 kB]
Get:16 http://mm.archive.ubuntu.com/ubuntu groovy-updates/main amd64 DEP-11 Metadata [55.6 kB]
Get:17 http://mm.archive.ubuntu.com/ubuntu groovy-updates/main amd64 c-n-f Metadata [8,224 B]
Get:18 http://mm.archive.ubuntu.com/ubuntu groovy-updates/universe i386 Packages [107 kB]
Get:19 http://mm.archive.ubuntu.com/ubuntu groovy-updates/universe amd64 Packages [198 kB]
Get:20 http://mm.archive.ubuntu.com/ubuntu groovy-updates/universe amd64 DEP-11 Metadata [111 kB]
Get:21 http://mm.archive.ubuntu.com/ubuntu groovy-updates/universe DEP-11 64x64 Icons [176 kB]
Get:22 http://mm.archive.ubuntu.com/ubuntu groovy-updates/universe amd64 c-n-f Metadata [6,324 B]
Get:23 http://mm.archive.ubuntu.com/ubuntu groovy-updates/multiverse amd64 DEP-11 Metadata [2,468 B]
Get:24 http://mm.archive.ubuntu.com/ubuntu groovy-backports/universe amd64 DEP-11 Metadata [600 B]
Reading package lists... Done                           
E: The repository 'http://ppa.launchpad.net/videolan/stable-daily/ubuntu groovy Release' does not have a Release file.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~$ 

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~$ sudo rm -r /usr/local/go
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~$ export VERSION=1.13.15 OS=linux ARCH=amd64
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~$ wget -O /tmp/go${VERSION}.${OS}-${ARCH}.tar.gz https://dl.google.com/go/go${VERSION}.${OS}-${ARCH}.tar.gz && \
> sudo tar -C /usr/local -xzf /tmp/go${VERSION}.${OS}-${ARCH}.tar.gz
--2021-06-15 15:55:45--  https://dl.google.com/go/go1.13.15.linux-amd64.tar.gz
Resolving dl.google.com (dl.google.com)... 74.125.24.136, 74.125.24.93, 74.125.24.190, ...
Connecting to dl.google.com (dl.google.com)|74.125.24.136|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 120173208 (115M) [application/octet-stream]
Saving to: ‘/tmp/go1.13.15.linux-amd64.tar.gz’

/tmp/go1.13.15.linux-amd64.tar.gz             100%[================================================================================================>] 114.61M  38.1MB/s    in 3.0s    

2021-06-15 15:55:48 (38.1 MB/s) - ‘/tmp/go1.13.15.linux-amd64.tar.gz’ saved [120173208/120173208]

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~$

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~$ echo 'export GOPATH=${HOME}/go' >> ~/.bashrc && \
> echo 'export PATH=/usr/local/go/bin:${PATH}:${GOPATH}/bin' >> ~/.bashrc && \
> source ~/.bashrc
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~$ echo $PATH
/usr/local/go/bin:/home/ye/.local/bin:/home/ye/anaconda3/bin:/home/ye/anaconda3/condabin:/home/ye/.local/bin:/home/ye/.local/bin:/usr/share/maven/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/home/ye/tool/ELAN_6-0/opt/elan-6.0/bin:/home/ye/tool/kenlm/build/bin:/home/ye/tool/SCTK/bin:/home/tool/node-v8.17.0-linux-x64/bin:home/ye/tool/srilm-1.7.3/bin/i686-m64:/home/ye/tool/htk/bin.cpu:/home/ye/tool/julius/julius:/home/ye/tool/subword-nmt:/home/ye/tool/marian/build:/home/ye/tool/mteval/build/bin:/home/ye/tool/NiuTrans.SMT/bin:/usr/local/go/bin:/home/ye/tool/ELAN_6-0/opt/elan-6.0/bin:/home/ye/tool/kenlm/build/bin:/home/ye/tool/SCTK/bin:/home/tool/node-v8.17.0-linux-x64/bin:home/ye/tool/srilm-1.7.3/bin/i686-m64:/home/ye/tool/htk/bin.cpu:/home/ye/tool/julius/julius:/home/ye/tool/subword-nmt:/home/ye/tool/marian/build:/home/ye/tool/mteval/build/bin:/home/ye/tool/NiuTrans.SMT/bin:/home/ye/go/bin
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~$

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~$ curl -sfL https://install.goreleaser.com/github.com/golangci/golangci-lint.sh |
> sh -s -- -b $(go env GOPATH)/bin v1.21.0
golangci/golangci-lint info checking GitHub for tag 'v1.21.0'
golangci/golangci-lint info found version: 1.21.0 for v1.21.0/linux/amd64
golangci/golangci-lint info installed /home/ye/go/bin/golangci-lint
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~$ 

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~$ mkdir -p ${GOPATH}/src/github.com/sylabs && \
> cd ${GOPATH}/src/github.com/sylabs && \
> git clone https://github.com/sylabs/singularity.git && \
> cd singularity
Cloning into 'singularity'...
remote: Enumerating objects: 95087, done.
remote: Counting objects: 100% (786/786), done.
remote: Compressing objects: 100% (386/386), done.
remote: Total 95087 (delta 381), reused 742 (delta 351), pack-reused 94301
Receiving objects: 100% (95087/95087), 30.84 MiB | 6.24 MiB/s, done.
Resolving deltas: 100% (60566/60566), done.


(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/go/src/github.com/sylabs/singularity$ git checkout v3.6.3
Note: switching to 'v3.6.3'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 98ad49a3d Merge pull request #5575 from dctrud/3.6.3-security-local
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/go/src/github.com/sylabs/singularity$

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/go/src/github.com/sylabs/singularity$ cd ${GOPATH}/src/github.com/sylabs/singularity && \
> ./mconfig && \
> cd ./builddir && \
> make && \
> sudo make install
Configuring for project `singularity' with languages: C, Golang
=> running pre-basechecks project specific checks ...
=> running base system checks ...
 checking: host C compiler... cc
 checking: host C++ compiler... c++
 checking: host Go compiler (at least version 1.13)... /usr/local/go/bin/go
 checking: host C compiler option -Wall... yes
 checking: host C compiler option -Werror... yes
 checking: host C compiler option -Wfatal-errors... yes
 checking: host C compiler option -Wno-unknown-warning-option... yes
 checking: host C compiler option -Wstrict-prototypes... yes
 checking: host C compiler option -Wpointer-arith... yes
 checking: host C compiler option -Wbad-function-cast... yes
 checking: host C compiler option -Woverlength-strings... yes
 checking: host C compiler option -Wframe-larger-than=2047... yes
 checking: host C compiler option -Wno-sign-compare... yes
 checking: host C compiler option -Wclobbered... yes
 checking: host C compiler option -Wempty-body... yes
 checking: host C compiler option -Wmissing-parameter-type... yes
 checking: host C compiler option -Wtype-limits... yes
 checking: host C compiler option -Wunused-parameter... yes
 checking: host C compiler option -Wunused-but-set-parameter... yes
 checking: host C compiler option -Wno-discarded-qualifiers... yes
 checking: host C compiler option -Wno-incompatible-pointer-types... yes
 checking: host C compiler option -pipe... yes
 checking: host C compiler option -fmessage-length=0... yes
 checking: host C compiler option -fPIC... yes
 checking: host `ar' path... ar
 checking: host `ld' path... ld
 checking: host `ranlib' path... ranlib
 checking: host `objcopy' path... objcopy
 checking: target C compiler... cc
 checking: target C++ compiler... c++
 checking: target `ar' path... ar
 checking: target `ld' path... ld
 checking: target `ranlib' path... ranlib
 checking: target `objcopy' path... objcopy
 checking: host compiles static binaries... yes
 checking: target compiles static binaries... yes
 checking: host os type... unix
 checking: host architecture... x86_64
 checking: target architecture... x86_64
 checking: host architecture word size... 64
 checking: target architecture word size... 64
 checking: project version... 3.6.3
 checking: project short version... 3.6.3
=> running post-basechecks project specific checks ...
 checking: namespace: CLONE_NEWPID... yes
 checking: namespace: CLONE_FS... yes
 checking: namespace: CLONE_NEWNS... yes
 checking: namespace: CLONE_NEWUSER... yes
 checking: namespace: CLONE_NEWIPC... yes
 checking: namespace: CLONE_NEWNET... yes
 checking: namespace: CLONE_NEWUTS... yes
 checking: namespace: CLONE_NEWCGROUP... yes
 checking: feature: NO_NEW_PRIVS... yes
 checking: feature: MS_SLAVE... yes
 checking: feature: MS_REC... yes
 checking: feature: MS_PRIVATE... yes
 checking: user capabilities... yes
 checking: header linux/securebits.h... yes
 checking: header linux/capability.h... yes
 checking: libseccomp+headers... no
 checking: cryptsetup... no

unable to find the cryptsetup program, is the package cryptsetup-bin installed?

=> generating fragments ...
=> building Makefile ...
=> generating singularity.spec ...
=> project singularity setup with :
    - host arch: x86_64
    - host wordsize: 64-bit
    - host C compiler: cc
    - host Go compiler: /usr/local/go/bin/go
    - host system: unix
      ---
    - target arch: x86_64
    - target wordsize: 64-bit
    - target C compiler: cc
      ---
    - config profile: release
      ---
    - SUID install: yes
    - Network plugins: yes
      ---
    - verbose: no
      ---
    - cryptsetup: 
      ---
    - version: 3.6.3
=> /home/ye/go/src/github.com/sylabs/singularity/builddir/Makefile ready, try:
   $ cd /home/ye/go/src/github.com/sylabs/singularity/builddir
   $ make
 GEN GO DEP /home/ye/go/src/github.com/sylabs/singularity/builddir/starter.d
go: downloading golang.org/x/sys v0.0.0-20200720211630-cb9d2d5c5666
go: downloading github.com/opencontainers/runtime-spec v1.0.3-0.20200710190001-3e4195d92445
go: downloading github.com/pelletier/go-toml v1.8.0
go: downloading mvdan.cc/sh/v3 v3.1.2
go: downloading github.com/sylabs/sif v1.2.1
go: downloading github.com/kr/pty v1.1.8
go: downloading github.com/sylabs/golang-x-crypto v0.0.0-20181006204705-4bce89e8e9a9
go: downloading github.com/satori/go.uuid v1.2.0
go: extracting github.com/kr/pty v1.1.8
go: downloading github.com/sylabs/json-resp v0.7.0
go: extracting github.com/satori/go.uuid v1.2.0
go: downloading github.com/sylabs/scs-key-client v0.5.1
go: extracting github.com/pelletier/go-toml v1.8.0
go: extracting github.com/sylabs/json-resp v0.7.0
go: extracting github.com/opencontainers/runtime-spec v1.0.3-0.20200710190001-3e4195d92445
go: downloading github.com/seccomp/containers-golang v0.6.0
go: downloading github.com/blang/semver v3.5.1+incompatible
go: extracting github.com/blang/semver v3.5.1+incompatible
go: extracting github.com/seccomp/containers-golang v0.6.0
go: downloading github.com/blang/semver/v4 v4.0.0
go: downloading github.com/containerd/cgroups v0.0.0-20200116170754-a8908713319d
go: extracting mvdan.cc/sh/v3 v3.1.2
go: downloading github.com/creack/pty v1.1.9
go: downloading golang.org/x/term v0.0.0-20191110171634-ad39bd3f0407
go: extracting github.com/sylabs/scs-key-client v0.5.1
go: downloading github.com/containernetworking/plugins v0.8.6
go: extracting github.com/sylabs/golang-x-crypto v0.0.0-20181006204705-4bce89e8e9a9
go: extracting github.com/blang/semver/v4 v4.0.0
go: extracting github.com/creack/pty v1.1.9
go: downloading golang.org/x/sync v0.0.0-20200317015054-43a5402ce75a
go: extracting golang.org/x/sys v0.0.0-20200720211630-cb9d2d5c5666
go: extracting github.com/containerd/cgroups v0.0.0-20200116170754-a8908713319d
go: extracting golang.org/x/term v0.0.0-20191110171634-ad39bd3f0407
go: downloading github.com/containernetworking/cni v0.8.0
go: extracting github.com/sylabs/sif v1.2.1
go: extracting github.com/containernetworking/plugins v0.8.6
go: downloading github.com/docker/go-units v0.4.0
go: downloading github.com/godbus/dbus v4.1.0+incompatible
go: extracting golang.org/x/sync v0.0.0-20200317015054-43a5402ce75a
go: downloading github.com/opencontainers/selinux v1.6.0
go: downloading github.com/gogo/protobuf v1.3.1
go: downloading github.com/coreos/go-iptables v0.4.5
go: extracting github.com/containernetworking/cni v0.8.0
go: downloading github.com/coreos/go-systemd v0.0.0-20190321100706-95778dfbb74e
go: downloading golang.org/x/xerrors v0.0.0-20191204190536-9bdfabe68543
go: downloading github.com/vishvananda/netlink v1.0.1-0.20190618143317-99a56c251ae6
go: downloading github.com/safchain/ethtool v0.0.0-20190326074333-42ed695e3de8
go: extracting github.com/docker/go-units v0.4.0
go: extracting github.com/godbus/dbus v4.1.0+incompatible
go: downloading github.com/godbus/dbus/v5 v5.0.3
go: extracting github.com/coreos/go-iptables v0.4.5
go: extracting github.com/safchain/ethtool v0.0.0-20190326074333-42ed695e3de8
go: extracting golang.org/x/xerrors v0.0.0-20191204190536-9bdfabe68543
go: extracting github.com/opencontainers/selinux v1.6.0
go: extracting github.com/godbus/dbus/v5 v5.0.3
go: extracting github.com/coreos/go-systemd v0.0.0-20190321100706-95778dfbb74e
go: downloading github.com/willf/bitset v1.1.11-0.20200630133818-d5bec3311243
go: extracting github.com/vishvananda/netlink v1.0.1-0.20190618143317-99a56c251ae6
go: downloading github.com/coreos/go-systemd/v22 v22.0.0-20191111152658-2d78030078ef
go: downloading github.com/vishvananda/netns v0.0.0-20180720170159-13995c7128cc
go: extracting github.com/willf/bitset v1.1.11-0.20200630133818-d5bec3311243
go: extracting github.com/coreos/go-systemd/v22 v22.0.0-20191111152658-2d78030078ef
go: extracting github.com/vishvananda/netns v0.0.0-20180720170159-13995c7128cc
go: extracting github.com/gogo/protobuf v1.3.1
go: finding github.com/opencontainers/runtime-spec v1.0.3-0.20200710190001-3e4195d92445
go: finding golang.org/x/sys v0.0.0-20200720211630-cb9d2d5c5666
go: finding github.com/satori/go.uuid v1.2.0
go: finding github.com/sylabs/sif v1.2.1
go: finding github.com/blang/semver/v4 v4.0.0
go: finding github.com/containerd/cgroups v0.0.0-20200116170754-a8908713319d
go: finding github.com/gogo/protobuf v1.3.1
go: finding github.com/coreos/go-systemd/v22 v22.0.0-20191111152658-2d78030078ef
go: finding github.com/godbus/dbus/v5 v5.0.3
go: finding github.com/docker/go-units v0.4.0
go: finding github.com/kr/pty v1.1.8
go: finding github.com/creack/pty v1.1.9
go: finding github.com/pelletier/go-toml v1.8.0
go: finding github.com/seccomp/containers-golang v0.6.0
go: finding github.com/opencontainers/selinux v1.6.0
go: finding github.com/willf/bitset v1.1.11-0.20200630133818-d5bec3311243
go: finding github.com/sylabs/golang-x-crypto v0.0.0-20181006204705-4bce89e8e9a9
go: finding mvdan.cc/sh/v3 v3.1.2
go: finding golang.org/x/sync v0.0.0-20200317015054-43a5402ce75a
go: finding golang.org/x/term v0.0.0-20191110171634-ad39bd3f0407
go: finding golang.org/x/xerrors v0.0.0-20191204190536-9bdfabe68543
go: finding github.com/containernetworking/cni v0.8.0
go: finding github.com/containernetworking/plugins v0.8.6
go: finding github.com/coreos/go-iptables v0.4.5
go: finding github.com/safchain/ethtool v0.0.0-20190326074333-42ed695e3de8
go: finding github.com/vishvananda/netlink v1.0.1-0.20190618143317-99a56c251ae6
go: finding github.com/vishvananda/netns v0.0.0-20180720170159-13995c7128cc
go: finding github.com/sylabs/json-resp v0.7.0
go: finding github.com/sylabs/scs-key-client v0.5.1
 GEN GO DEP /home/ye/go/src/github.com/sylabs/singularity/builddir/singularity.d
go: downloading github.com/fatih/color v1.9.0
go: downloading github.com/go-log/log v0.2.0
go: downloading github.com/opencontainers/image-spec v1.0.2-0.20191218002246-9ea04d1f37d7
go: downloading github.com/sylabs/scs-library-client v0.5.5
go: downloading github.com/containerd/containerd v1.4.0
go: downloading github.com/deislabs/oras v0.8.1
go: downloading github.com/containers/image/v5 v5.5.2
go: extracting github.com/fatih/color v1.9.0
go: downloading github.com/gorilla/websocket v1.4.2
go: extracting github.com/sylabs/scs-library-client v0.5.5
go: downloading github.com/spf13/cobra v1.0.0
go: extracting github.com/deislabs/oras v0.8.1
go: extracting github.com/go-log/log v0.2.0
go: downloading gopkg.in/yaml.v2 v2.3.0
go: extracting github.com/opencontainers/image-spec v1.0.2-0.20191218002246-9ea04d1f37d7
go: extracting github.com/gorilla/websocket v1.4.2
go: downloading github.com/vbauerster/mpb/v4 v4.12.2
go: downloading github.com/mattn/go-isatty v0.0.12
go: extracting github.com/spf13/cobra v1.0.0
go: extracting github.com/mattn/go-isatty v0.0.12
go: downloading github.com/mattn/go-colorable v0.1.6
go: extracting gopkg.in/yaml.v2 v2.3.0
go: downloading github.com/opencontainers/go-digest v1.0.0
go: extracting github.com/vbauerster/mpb/v4 v4.12.2
go: extracting github.com/containers/image/v5 v5.5.2
go: extracting github.com/mattn/go-colorable v0.1.6
go: extracting github.com/opencontainers/go-digest v1.0.0
go: downloading github.com/opencontainers/umoci v0.4.6-0.20200622135030-30d116059d97
go: downloading github.com/docker/docker v1.4.2-0.20200203170920-46ec8731fbce
go: downloading github.com/spf13/pflag v1.0.5
go: extracting github.com/containerd/containerd v1.4.0
go: extracting github.com/spf13/pflag v1.0.5
go: downloading github.com/docker/go-connections v0.4.0
go: extracting github.com/docker/go-connections v0.4.0
go: downloading golang.org/x/net v0.0.0-20200602114024-627f9648deb9
go: downloading github.com/vbauerster/mpb/v5 v5.2.2
go: downloading github.com/sirupsen/logrus v1.6.0
go: downloading google.golang.org/grpc v1.27.0
go: downloading github.com/apex/log v1.9.0
go: downloading github.com/klauspost/compress v1.10.9
go: extracting github.com/sirupsen/logrus v1.6.0
go: extracting github.com/opencontainers/umoci v0.4.6-0.20200622135030-30d116059d97
go: downloading github.com/containers/ocicrypt v1.0.2
go: downloading github.com/sylabs/scs-build-client v0.1.4
go: downloading github.com/golang/protobuf v1.4.2
go: extracting github.com/apex/log v1.9.0
go: extracting github.com/docker/docker v1.4.2-0.20200203170920-46ec8731fbce
go: extracting google.golang.org/grpc v1.27.0
go: extracting github.com/sylabs/scs-build-client v0.1.4
go: extracting github.com/containers/ocicrypt v1.0.2
go: extracting github.com/vbauerster/mpb/v5 v5.2.2
go: downloading github.com/ulikunitz/xz v0.5.7
go: downloading github.com/docker/distribution v2.7.1+incompatible
go: extracting github.com/golang/protobuf v1.4.2
go: downloading github.com/VividCortex/ewma v1.1.1
go: downloading github.com/ghodss/yaml v1.0.0
go: extracting golang.org/x/net v0.0.0-20200602114024-627f9648deb9
go: downloading google.golang.org/protobuf v1.24.0
go: downloading github.com/klauspost/pgzip v1.2.4
go: downloading github.com/mattn/go-runewidth v0.0.9
go: downloading github.com/vbatts/go-mtree v0.5.0
go: extracting github.com/VividCortex/ewma v1.1.1
go: extracting github.com/ghodss/yaml v1.0.0
go: extracting github.com/mattn/go-runewidth v0.0.9
go: extracting github.com/ulikunitz/xz v0.5.7
go: extracting github.com/docker/distribution v2.7.1+incompatible
go: downloading github.com/acarl005/stripansi v0.0.0-20180116102854-5a71ef0e047d
go: extracting github.com/klauspost/pgzip v1.2.4
go: downloading google.golang.org/genproto v0.0.0-20200526211855-cb27e3aa2013
go: extracting github.com/vbatts/go-mtree v0.5.0
go: extracting github.com/acarl005/stripansi v0.0.0-20180116102854-5a71ef0e047d
go: downloading github.com/fullsailor/pkcs7 v0.0.0-20190404230743-d7302db945fa
go: downloading github.com/containers/storage v1.20.2
go: downloading github.com/rootless-containers/proto v0.1.0
go: extracting github.com/fullsailor/pkcs7 v0.0.0-20190404230743-d7302db945fa
go: downloading github.com/urfave/cli v1.22.4
go: extracting google.golang.org/protobuf v1.24.0
go: extracting github.com/rootless-containers/proto v0.1.0
go: extracting github.com/urfave/cli v1.22.4
go: downloading github.com/cyphar/filepath-securejoin v0.2.2
go: downloading gopkg.in/square/go-jose.v2 v2.3.1
go: downloading github.com/cpuguy83/go-md2man v1.0.10
go: downloading github.com/gorilla/mux v1.7.4
go: downloading github.com/docker/docker-credential-helpers v0.6.3
go: downloading github.com/docker/go-metrics v0.0.1
go: extracting github.com/cyphar/filepath-securejoin v0.2.2
go: downloading github.com/containers/libtrust v0.0.0-20190913040956-14b96171aa3b
go: extracting github.com/cpuguy83/go-md2man v1.0.10
go: downloading github.com/cpuguy83/go-md2man/v2 v2.0.0
go: extracting github.com/gorilla/mux v1.7.4
go: extracting github.com/docker/docker-credential-helpers v0.6.3
go: extracting github.com/docker/go-metrics v0.0.1
go: downloading github.com/BurntSushi/toml v0.3.1
go: downloading github.com/prometheus/client_golang v1.1.0
go: extracting github.com/containers/storage v1.20.2
go: extracting gopkg.in/square/go-jose.v2 v2.3.1
go: downloading go.etcd.io/bbolt v1.3.4
go: extracting github.com/containers/libtrust v0.0.0-20190913040956-14b96171aa3b
go: extracting github.com/cpuguy83/go-md2man/v2 v2.0.0
go: downloading github.com/russross/blackfriday v1.5.2
go: extracting github.com/BurntSushi/toml v0.3.1
go: downloading github.com/opencontainers/runc v1.0.0-rc90
go: downloading github.com/pquerna/ffjson v0.0.0-20190813045741-dac163c6c0a9
go: extracting github.com/prometheus/client_golang v1.1.0
go: downloading github.com/prometheus/client_model v0.0.0-20190812154241-14fe0d1b01d4
go: downloading github.com/prometheus/procfs v0.0.5
go: extracting go.etcd.io/bbolt v1.3.4
go: downloading github.com/prometheus/common v0.6.0
go: extracting github.com/russross/blackfriday v1.5.2
go: downloading github.com/russross/blackfriday/v2 v2.0.1
go: extracting github.com/pquerna/ffjson v0.0.0-20190813045741-dac163c6c0a9
go: extracting github.com/prometheus/client_model v0.0.0-20190812154241-14fe0d1b01d4
go: downloading github.com/beorn7/perks v1.0.1
go: extracting github.com/prometheus/procfs v0.0.5
go: extracting github.com/russross/blackfriday/v2 v2.0.1
go: extracting github.com/beorn7/perks v1.0.1
go: extracting github.com/prometheus/common v0.6.0
go: downloading github.com/shurcooL/sanitized_anchor_name v1.0.0
go: downloading github.com/matttproud/golang_protobuf_extensions v1.0.1
go: extracting github.com/opencontainers/runc v1.0.0-rc90
go: extracting github.com/shurcooL/sanitized_anchor_name v1.0.0
go: extracting github.com/matttproud/golang_protobuf_extensions v1.0.1
go: extracting google.golang.org/genproto v0.0.0-20200526211855-cb27e3aa2013
go: extracting github.com/klauspost/compress v1.10.9
go: finding github.com/containers/image/v5 v5.5.2
go: finding github.com/opencontainers/go-digest v1.0.0
go: finding github.com/opencontainers/image-spec v1.0.2-0.20191218002246-9ea04d1f37d7
go: finding github.com/fatih/color v1.9.0
go: finding github.com/mattn/go-colorable v0.1.6
go: finding github.com/mattn/go-isatty v0.0.12
go: finding github.com/go-log/log v0.2.0
go: finding github.com/spf13/cobra v1.0.0
go: finding github.com/spf13/pflag v1.0.5
go: finding github.com/sylabs/scs-library-client v0.5.5
go: finding gopkg.in/yaml.v2 v2.3.0
go: finding github.com/vbauerster/mpb/v4 v4.12.2
go: finding github.com/VividCortex/ewma v1.1.1
go: finding github.com/acarl005/stripansi v0.0.0-20180116102854-5a71ef0e047d
go: finding github.com/apex/log v1.9.0
go: finding github.com/klauspost/compress v1.10.9
go: finding github.com/klauspost/pgzip v1.2.4
go: finding github.com/sirupsen/logrus v1.6.0
go: finding github.com/ulikunitz/xz v0.5.7
go: finding github.com/containers/libtrust v0.0.0-20190913040956-14b96171aa3b
go: finding github.com/containers/ocicrypt v1.0.2
go: finding github.com/docker/docker v1.4.2-0.20200203170920-46ec8731fbce
go: finding go.etcd.io/bbolt v1.3.4
go: finding github.com/containers/storage v1.20.2
go: finding gopkg.in/square/go-jose.v2 v2.3.1
go: finding github.com/fullsailor/pkcs7 v0.0.0-20190404230743-d7302db945fa
go: finding github.com/vbauerster/mpb/v5 v5.2.2
go: finding github.com/mattn/go-runewidth v0.0.9
go: finding github.com/docker/docker-credential-helpers v0.6.3
go: finding github.com/BurntSushi/toml v0.3.1
go: finding github.com/docker/go-connections v0.4.0
go: finding golang.org/x/net v0.0.0-20200602114024-627f9648deb9
go: finding github.com/docker/distribution v2.7.1+incompatible
go: finding github.com/gorilla/mux v1.7.4
go: finding github.com/docker/go-metrics v0.0.1
go: finding github.com/prometheus/client_golang v1.1.0
go: finding github.com/beorn7/perks v1.0.1
go: finding github.com/golang/protobuf v1.4.2
go: finding google.golang.org/protobuf v1.24.0
go: finding github.com/prometheus/client_model v0.0.0-20190812154241-14fe0d1b01d4
go: finding github.com/prometheus/common v0.6.0
go: finding github.com/matttproud/golang_protobuf_extensions v1.0.1
go: finding github.com/prometheus/procfs v0.0.5
go: finding github.com/ghodss/yaml v1.0.0
go: finding github.com/containerd/containerd v1.4.0
go: finding google.golang.org/grpc v1.27.0
go: finding google.golang.org/genproto v0.0.0-20200526211855-cb27e3aa2013
go: finding github.com/opencontainers/runc v1.0.0-rc90
go: finding github.com/pquerna/ffjson v0.0.0-20190813045741-dac163c6c0a9
go: finding github.com/opencontainers/umoci v0.4.6-0.20200622135030-30d116059d97
go: finding github.com/cyphar/filepath-securejoin v0.2.2
go: finding github.com/vbatts/go-mtree v0.5.0
go: finding github.com/rootless-containers/proto v0.1.0
go: finding github.com/urfave/cli v1.22.4
go: finding github.com/cpuguy83/go-md2man/v2 v2.0.0
go: finding github.com/russross/blackfriday/v2 v2.0.1
go: finding github.com/shurcooL/sanitized_anchor_name v1.0.0
go: finding github.com/deislabs/oras v0.8.1
go: finding github.com/gorilla/websocket v1.4.2
go: finding github.com/sylabs/scs-build-client v0.1.4
 GEN /home/ye/go/src/github.com/sylabs/singularity/scripts/go-generate
 GO singularity
    [+] GO_TAGS "containers_image_openpgp sylog oci_engine singularity_engine fakeroot_engine apparmor selinux"
 GEN etc/bash_completion.d/singularity
 GEN singularity.conf from /usr/local/etc/singularity/singularity.conf
 CNI PLUGIN dhcp
go: downloading github.com/d2g/dhcp4 v0.0.0-20170904100407-a1d1b6c41b1c
go: downloading github.com/d2g/dhcp4client v1.0.0
go: extracting github.com/d2g/dhcp4 v0.0.0-20170904100407-a1d1b6c41b1c
go: extracting github.com/d2g/dhcp4client v1.0.0
go: finding github.com/coreos/go-systemd v0.0.0-20190321100706-95778dfbb74e
go: finding github.com/d2g/dhcp4 v0.0.0-20170904100407-a1d1b6c41b1c
go: finding github.com/d2g/dhcp4client v1.0.0
 CNI PLUGIN host-local
go: downloading github.com/alexflint/go-filemutex v0.0.0-20171028004239-d358565f3c3f
go: extracting github.com/alexflint/go-filemutex v0.0.0-20171028004239-d358565f3c3f
go: finding github.com/alexflint/go-filemutex v0.0.0-20171028004239-d358565f3c3f
 CNI PLUGIN static
 CNI PLUGIN bridge
go: downloading github.com/j-keck/arping v0.0.0-20160618110441-2cf9dc699c56
go: extracting github.com/j-keck/arping v0.0.0-20160618110441-2cf9dc699c56
go: finding github.com/j-keck/arping v0.0.0-20160618110441-2cf9dc699c56
 CNI PLUGIN host-device
 CNI PLUGIN ipvlan
 CNI PLUGIN loopback
 CNI PLUGIN macvlan
 CNI PLUGIN ptp
 CNI PLUGIN vlan
 CNI PLUGIN bandwidth
 CNI PLUGIN firewall
go: finding github.com/godbus/dbus v4.1.0+incompatible
 CNI PLUGIN flannel
 CNI PLUGIN portmap
go: downloading github.com/mattn/go-shellwords v1.0.10
go: extracting github.com/mattn/go-shellwords v1.0.10
go: finding github.com/mattn/go-shellwords v1.0.10
 CNI PLUGIN tuning
 GO clean -cache
 GO cmd/starter/c/starter
 GO cmd/starter/c/starter-suid
    [+] GO_TAGS "containers_image_openpgp sylog singularity_engine fakeroot_engine apparmor selinux"
 GEN /home/ye/go/src/github.com/sylabs/singularity/scripts/go-test
 INSTALL /usr/local/bin/singularity
 INSTALL /usr/local/etc/bash_completion.d/singularity
 INSTALL /usr/local/etc/singularity/singularity.conf
 INSTALL /usr/local/etc/singularity/remote.yaml
 INSTALL CNI PLUGIN /usr/local/libexec/singularity/cni/dhcp
 INSTALL CNI PLUGIN /usr/local/libexec/singularity/cni/host-local
 INSTALL CNI PLUGIN /usr/local/libexec/singularity/cni/static
 INSTALL CNI PLUGIN /usr/local/libexec/singularity/cni/bridge
 INSTALL CNI PLUGIN /usr/local/libexec/singularity/cni/host-device
 INSTALL CNI PLUGIN /usr/local/libexec/singularity/cni/ipvlan
 INSTALL CNI PLUGIN /usr/local/libexec/singularity/cni/loopback
 INSTALL CNI PLUGIN /usr/local/libexec/singularity/cni/macvlan
 INSTALL CNI PLUGIN /usr/local/libexec/singularity/cni/ptp
 INSTALL CNI PLUGIN /usr/local/libexec/singularity/cni/vlan
 INSTALL CNI PLUGIN /usr/local/libexec/singularity/cni/bandwidth
 INSTALL CNI PLUGIN /usr/local/libexec/singularity/cni/firewall
 INSTALL CNI PLUGIN /usr/local/libexec/singularity/cni/flannel
 INSTALL CNI PLUGIN /usr/local/libexec/singularity/cni/portmap
 INSTALL CNI PLUGIN /usr/local/libexec/singularity/cni/tuning
 INSTALL CNI CONFIGURATION FILES
 INSTALL /usr/local/libexec/singularity/bin/starter
 INSTALL /usr/local/var/singularity/mnt/session
 INSTALL /usr/local/bin/run-singularity
 INSTALL /usr/local/etc/singularity/capability.json
 INSTALL /usr/local/etc/singularity/ecl.toml
 INSTALL /usr/local/etc/singularity/seccomp-profiles/default.json
 INSTALL /usr/local/etc/singularity/nvliblist.conf
 INSTALL /usr/local/etc/singularity/rocmliblist.conf
 INSTALL /usr/local/etc/singularity/cgroups/cgroups.toml
 INSTALL SUID /usr/local/libexec/singularity/bin/starter-suid
 DONE
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/go/src/github.com/sylabs/singularity/builddir$

(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/go/src/github.com/sylabs/singularity/builddir$ singularity version
3.6.3



## Reference

https://github.com/hpcng/singularity/issues/5099
