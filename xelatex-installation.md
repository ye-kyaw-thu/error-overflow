## apt-get texlive-xetex

သိရသလောက်ကတော့ ဗမာပြည်မှာလက်ရှိလုပ်တဲ့ conference တွေမှာတော့ latex ကို မသုံးကြသေးပေမဲ့ နာမည်ကြီး conference တွေ journal တွေမှာတော့ latex ကို သုံးကြတာမို့ သုတေသန စာတမ်းရေးကြတဲ့အခါမှာ latex template ကို သုံးကြပါတယ်။ pdflatex, MiKTeX, TeX Live, MacTeX စတဲ့ latex compiler အမျိုးမျိုးရှိပေမဲ့ ဒီနေရာမှာတော့ ကျွန်တော်သုံးတဲ့ xelatex installation နဲ့ ပတ်သက်တဲ့ note ပါ။ ပထမဆုံး installation လုပ်ကြတဲ့ သူတွေအတွက် အသုံးဝင်ပါလိမ့်မယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ sudo apt-get install texlive-xetex
[sudo] password for ye: 
Reading package lists...
Building dependency tree...
Reading state information...
The following additional packages will be installed:
  dvisvgm fonts-lato fonts-lmodern fonts-texgyre libapache-pom-java
  libcommons-logging-java libcommons-parent-java libfontbox-java libjs-jquery
  libpdfbox-java libptexenc1 libruby2.7 libteckit0 libtexlua53 libtexluajit2
  libtk8.6 libzzip-0-13 lmodern node-jquery preview-latex-style rake ruby
  ruby-minitest ruby-net-telnet ruby-power-assert ruby-test-unit ruby-xmlrpc
  ruby2.7 rubygems-integration t1utils tcl teckit tex-common tex-gyre
  texlive-base texlive-binaries texlive-fonts-recommended texlive-latex-base
  texlive-latex-extra texlive-latex-recommended texlive-pictures
  texlive-plain-generic tipa tk tk8.6
Suggested packages:
  libavalon-framework-java libcommons-logging-java-doc
  libexcalibur-logkit-java liblog4j1.2-java ri ruby-dev bundler debhelper
  perl-tk xzdec texlive-fonts-recommended-doc texlive-latex-base-doc
  python3-pygments icc-profiles libfile-which-perl
  libspreadsheet-parseexcel-perl texlive-latex-extra-doc
  texlive-latex-recommended-doc texlive-luatex texlive-pstricks dot2tex prerex
  ruby-tcltk | libtcltk-ruby texlive-pictures-doc vprerex
The following NEW packages will be installed:
  dvisvgm fonts-lato fonts-lmodern fonts-texgyre libapache-pom-java
  libcommons-logging-java libcommons-parent-java libfontbox-java libjs-jquery
  libpdfbox-java libptexenc1 libruby2.7 libteckit0 libtexlua53 libtexluajit2
  libtk8.6 libzzip-0-13 lmodern node-jquery preview-latex-style rake ruby
  ruby-minitest ruby-net-telnet ruby-power-assert ruby-test-unit ruby-xmlrpc
  ruby2.7 rubygems-integration t1utils tcl teckit tex-common tex-gyre
  texlive-base texlive-binaries texlive-fonts-recommended texlive-latex-base
  texlive-latex-extra texlive-latex-recommended texlive-pictures
  texlive-plain-generic texlive-xetex tipa tk tk8.6
0 upgraded, 46 newly installed, 0 to remove and 79 not upgraded.
Need to get 157 MB of archives.
After this operation, 499 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 fonts-lato all 2.0-2 [2,698 kB]
Get:2 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 tex-common all 6.15 [33.0 kB]
Get:3 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 dvisvgm amd64 2.10-1 [1,105 kB]
Get:4 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 fonts-lmodern all 2.004.5-6 [4,532 kB]
Get:5 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 fonts-texgyre all 20180621-3 [10.2 MB]
Get:6 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libapache-pom-java all 18-1 [4,720 B]
Get:7 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libcommons-parent-java all 43-1 [10.8 kB]
Get:8 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libcommons-logging-java all 1.2-2 [60.3 kB]
Get:9 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 node-jquery all 3.5.1+dfsg-4 [309 kB]
Get:10 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 libjs-jquery all 3.5.1+dfsg-4 [2,308 B]
Get:11 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 libptexenc1 amd64 2020.20200327.54578-4build1 [36.0 kB]
Get:12 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 rubygems-integration all 1.17.2 [5,284 B]
Get:13 http://mm.archive.ubuntu.com/ubuntu groovy-updates/main amd64 ruby2.7 amd64 2.7.1-3ubuntu1.1 [95.7 kB]
Get:14 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 ruby amd64 1:2.7+1 [5,412 B]
Get:15 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 rake all 13.0.1-4 [61.6 kB]
Get:16 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 ruby-minitest all 5.13.0-1 [40.9 kB]
Get:17 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 ruby-net-telnet all 0.1.1-2 [12.6 kB]
Get:18 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 ruby-power-assert all 1.1.7-1 [11.4 kB]
Get:19 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 ruby-test-unit all 3.3.5-1 [73.2 kB]
Get:20 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 ruby-xmlrpc all 0.3.0-2 [23.8 kB]
Get:21 http://mm.archive.ubuntu.com/ubuntu groovy-updates/main amd64 libruby2.7 amd64 2.7.1-3ubuntu1.1 [3,544 kB]
Get:22 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libteckit0 amd64 2.5.8+ds2-5ubuntu2 [320 kB]
Get:23 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 libtexlua53 amd64 2020.20200327.54578-4build1 [108 kB]
Get:24 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 libtexluajit2 amd64 2020.20200327.54578-4build1 [243 kB]
Get:25 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 libtk8.6 amd64 8.6.10-1 [714 kB]
Get:26 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libzzip-0-13 amd64 0.13.62-3.2ubuntu1 [26.2 kB]
Get:27 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 lmodern all 2.004.5-6 [9,474 kB]
Get:28 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 preview-latex-style all 11.91-2ubuntu2 [184 kB]
Get:29 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 t1utils amd64 1.41-4 [56.0 kB]
Get:30 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 tcl amd64 8.6.9+1 [5,112 B]
Get:31 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 teckit amd64 2.5.8+ds2-5ubuntu2 [687 kB]
Get:32 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 tex-gyre all 20180621-3 [6,209 kB]
Get:33 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 texlive-binaries amd64 2020.20200327.54578-4build1 [10.1 MB]
Get:34 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 texlive-base all 2020.20200804-2 [21.4 MB]
Get:35 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 texlive-fonts-recommended all 2020.20200804-2 [4,974 kB]
Get:36 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 texlive-latex-base all 2020.20200804-2 [1,036 kB]
Get:37 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libfontbox-java all 1:1.8.16-2 [207 kB]
Get:38 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 libpdfbox-java all 1:1.8.16-2 [5,199 kB]
Get:39 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 texlive-latex-recommended all 2020.20200804-2 [14.5 MB]
Get:40 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 texlive-pictures all 2020.20200804-2 [4,655 kB]
Get:41 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 texlive-latex-extra all 2020.20200804-3 [12.8 MB]
Get:42 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 texlive-plain-generic all 2020.20200804-3 [26.2 MB]
Get:43 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 tipa all 2:1.3-20 [2,978 kB]
Get:44 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 texlive-xetex all 2020.20200804-2 [12.0 MB]
Get:45 http://mm.archive.ubuntu.com/ubuntu groovy/main amd64 tk8.6 amd64 8.6.10-1 [12.5 kB]
Get:46 http://mm.archive.ubuntu.com/ubuntu groovy/universe amd64 tk amd64 8.6.9+1 [3,240 B]
Extracting templates from packages: 100%
Preconfiguring packages ...
Fetched 157 MB in 5min 55s (442 kB/s)
                                     Selecting previously unselected package fonts-lato.
(Reading database ... 228679 files and directories currently installed.)
Preparing to unpack .../00-fonts-lato_2.0-2_all.deb ...
Unpacking fonts-lato (2.0-2) ...
Selecting previously unselected package tex-common.
Preparing to unpack .../01-tex-common_6.15_all.deb ...
Unpacking tex-common (6.15) ...
Selecting previously unselected package dvisvgm.
Preparing to unpack .../02-dvisvgm_2.10-1_amd64.deb ...
Unpacking dvisvgm (2.10-1) ...
Selecting previously unselected package fonts-lmodern.
Preparing to unpack .../03-fonts-lmodern_2.004.5-6_all.deb ...
Unpacking fonts-lmodern (2.004.5-6) ...
Selecting previously unselected package fonts-texgyre.
Preparing to unpack .../04-fonts-texgyre_20180621-3_all.deb ...
Unpacking fonts-texgyre (20180621-3) ...
Selecting previously unselected package libapache-pom-java.
Preparing to unpack .../05-libapache-pom-java_18-1_all.deb ...
Unpacking libapache-pom-java (18-1) ...
Selecting previously unselected package libcommons-parent-java.
Preparing to unpack .../06-libcommons-parent-java_43-1_all.deb ...
Unpacking libcommons-parent-java (43-1) ...
Selecting previously unselected package libcommons-logging-java.
Preparing to unpack .../07-libcommons-logging-java_1.2-2_all.deb ...
Unpacking libcommons-logging-java (1.2-2) ...
Selecting previously unselected package node-jquery.
Preparing to unpack .../08-node-jquery_3.5.1+dfsg-4_all.deb ...
Unpacking node-jquery (3.5.1+dfsg-4) ...
Selecting previously unselected package libjs-jquery.
Preparing to unpack .../09-libjs-jquery_3.5.1+dfsg-4_all.deb ...
Unpacking libjs-jquery (3.5.1+dfsg-4) ...
Selecting previously unselected package libptexenc1:amd64.
Preparing to unpack .../10-libptexenc1_2020.20200327.54578-4build1_amd64.deb ...
Unpacking libptexenc1:amd64 (2020.20200327.54578-4build1) ...
Selecting previously unselected package rubygems-integration.
Preparing to unpack .../11-rubygems-integration_1.17.2_all.deb ...
Unpacking rubygems-integration (1.17.2) ...
Selecting previously unselected package ruby2.7.
Preparing to unpack .../12-ruby2.7_2.7.1-3ubuntu1.1_amd64.deb ...
Unpacking ruby2.7 (2.7.1-3ubuntu1.1) ...
Selecting previously unselected package ruby.
Preparing to unpack .../13-ruby_1%3a2.7+1_amd64.deb ...
Unpacking ruby (1:2.7+1) ...
Selecting previously unselected package rake.
Preparing to unpack .../14-rake_13.0.1-4_all.deb ...
Unpacking rake (13.0.1-4) ...
Selecting previously unselected package ruby-minitest.
Preparing to unpack .../15-ruby-minitest_5.13.0-1_all.deb ...
Unpacking ruby-minitest (5.13.0-1) ...
Selecting previously unselected package ruby-net-telnet.
Preparing to unpack .../16-ruby-net-telnet_0.1.1-2_all.deb ...
Unpacking ruby-net-telnet (0.1.1-2) ...
Selecting previously unselected package ruby-power-assert.
Preparing to unpack .../17-ruby-power-assert_1.1.7-1_all.deb ...
Unpacking ruby-power-assert (1.1.7-1) ...
Selecting previously unselected package ruby-test-unit.
Preparing to unpack .../18-ruby-test-unit_3.3.5-1_all.deb ...
Unpacking ruby-test-unit (3.3.5-1) ...
Selecting previously unselected package ruby-xmlrpc.
Preparing to unpack .../19-ruby-xmlrpc_0.3.0-2_all.deb ...
Unpacking ruby-xmlrpc (0.3.0-2) ...
Selecting previously unselected package libruby2.7:amd64.
Preparing to unpack .../20-libruby2.7_2.7.1-3ubuntu1.1_amd64.deb ...
Unpacking libruby2.7:amd64 (2.7.1-3ubuntu1.1) ...
Selecting previously unselected package libteckit0:amd64.
Preparing to unpack .../21-libteckit0_2.5.8+ds2-5ubuntu2_amd64.deb ...
Unpacking libteckit0:amd64 (2.5.8+ds2-5ubuntu2) ...
Selecting previously unselected package libtexlua53:amd64.
Preparing to unpack .../22-libtexlua53_2020.20200327.54578-4build1_amd64.deb ...
Unpacking libtexlua53:amd64 (2020.20200327.54578-4build1) ...
Selecting previously unselected package libtexluajit2:amd64.
Preparing to unpack .../23-libtexluajit2_2020.20200327.54578-4build1_amd64.deb ...
Unpacking libtexluajit2:amd64 (2020.20200327.54578-4build1) ...
Selecting previously unselected package libtk8.6:amd64.
Preparing to unpack .../24-libtk8.6_8.6.10-1_amd64.deb ...
Unpacking libtk8.6:amd64 (8.6.10-1) ...
Selecting previously unselected package libzzip-0-13:amd64.
Preparing to unpack .../25-libzzip-0-13_0.13.62-3.2ubuntu1_amd64.deb ...
Unpacking libzzip-0-13:amd64 (0.13.62-3.2ubuntu1) ...
Selecting previously unselected package lmodern.
Preparing to unpack .../26-lmodern_2.004.5-6_all.deb ...
Unpacking lmodern (2.004.5-6) ...
Selecting previously unselected package preview-latex-style.
Preparing to unpack .../27-preview-latex-style_11.91-2ubuntu2_all.deb ...
Unpacking preview-latex-style (11.91-2ubuntu2) ...
Selecting previously unselected package t1utils.
Preparing to unpack .../28-t1utils_1.41-4_amd64.deb ...
Unpacking t1utils (1.41-4) ...
Selecting previously unselected package tcl.
Preparing to unpack .../29-tcl_8.6.9+1_amd64.deb ...
Unpacking tcl (8.6.9+1) ...
Selecting previously unselected package teckit.
Preparing to unpack .../30-teckit_2.5.8+ds2-5ubuntu2_amd64.deb ...
Unpacking teckit (2.5.8+ds2-5ubuntu2) ...
Selecting previously unselected package tex-gyre.
Preparing to unpack .../31-tex-gyre_20180621-3_all.deb ...
Unpacking tex-gyre (20180621-3) ...
Selecting previously unselected package texlive-binaries.
Preparing to unpack .../32-texlive-binaries_2020.20200327.54578-4build1_amd64.deb ...
Unpacking texlive-binaries (2020.20200327.54578-4build1) ...
Selecting previously unselected package texlive-base.
Preparing to unpack .../33-texlive-base_2020.20200804-2_all.deb ...
Unpacking texlive-base (2020.20200804-2) ...
Selecting previously unselected package texlive-fonts-recommended.
Preparing to unpack .../34-texlive-fonts-recommended_2020.20200804-2_all.deb ...
Unpacking texlive-fonts-recommended (2020.20200804-2) ...
Selecting previously unselected package texlive-latex-base.
Preparing to unpack .../35-texlive-latex-base_2020.20200804-2_all.deb ...
Unpacking texlive-latex-base (2020.20200804-2) ...
Selecting previously unselected package libfontbox-java.
Preparing to unpack .../36-libfontbox-java_1%3a1.8.16-2_all.deb ...
Unpacking libfontbox-java (1:1.8.16-2) ...
Selecting previously unselected package libpdfbox-java.
Preparing to unpack .../37-libpdfbox-java_1%3a1.8.16-2_all.deb ...
Unpacking libpdfbox-java (1:1.8.16-2) ...
Selecting previously unselected package texlive-latex-recommended.
Preparing to unpack .../38-texlive-latex-recommended_2020.20200804-2_all.deb ...
Unpacking texlive-latex-recommended (2020.20200804-2) ...
Selecting previously unselected package texlive-pictures.
Preparing to unpack .../39-texlive-pictures_2020.20200804-2_all.deb ...
Unpacking texlive-pictures (2020.20200804-2) ...
Selecting previously unselected package texlive-latex-extra.
Preparing to unpack .../40-texlive-latex-extra_2020.20200804-3_all.deb ...
Unpacking texlive-latex-extra (2020.20200804-3) ...
Selecting previously unselected package texlive-plain-generic.
Preparing to unpack .../41-texlive-plain-generic_2020.20200804-3_all.deb ...
Unpacking texlive-plain-generic (2020.20200804-3) ...
Selecting previously unselected package tipa.
Preparing to unpack .../42-tipa_2%3a1.3-20_all.deb ...
Unpacking tipa (2:1.3-20) ...
Selecting previously unselected package texlive-xetex.
Preparing to unpack .../43-texlive-xetex_2020.20200804-2_all.deb ...
Unpacking texlive-xetex (2020.20200804-2) ...
Selecting previously unselected package tk8.6.
Preparing to unpack .../44-tk8.6_8.6.10-1_amd64.deb ...
Unpacking tk8.6 (8.6.10-1) ...
Selecting previously unselected package tk.
Preparing to unpack .../45-tk_8.6.9+1_amd64.deb ...
Unpacking tk (8.6.9+1) ...
Setting up fonts-lato (2.0-2) ...
Setting up ruby-power-assert (1.1.7-1) ...
Setting up libtexlua53:amd64 (2020.20200327.54578-4build1) ...
Setting up libtk8.6:amd64 (8.6.10-1) ...
Setting up libtexluajit2:amd64 (2020.20200327.54578-4build1) ...
Setting up libfontbox-java (1:1.8.16-2) ...
Setting up dvisvgm (2.10-1) ...
Setting up rubygems-integration (1.17.2) ...
Setting up libzzip-0-13:amd64 (0.13.62-3.2ubuntu1) ...
Setting up ruby-minitest (5.13.0-1) ...
Setting up tex-common (6.15) ...
update-language: texlive-base not installed and configured, doing nothing!
Setting up libptexenc1:amd64 (2020.20200327.54578-4build1) ...
Setting up ruby-test-unit (3.3.5-1) ...
Setting up libteckit0:amd64 (2.5.8+ds2-5ubuntu2) ...
Setting up libapache-pom-java (18-1) ...
Setting up ruby-net-telnet (0.1.1-2) ...
Setting up t1utils (1.41-4) ...
Setting up fonts-texgyre (20180621-3) ...
Setting up texlive-binaries (2020.20200327.54578-4build1) ...
update-alternatives: using /usr/bin/xdvi-xaw to provide /usr/bin/xdvi.bin (xdvi.bin) in auto mode
update-alternatives: using /usr/bin/bibtex.original to provide /usr/bin/bibtex (bibtex) in auto mode
Setting up tcl (8.6.9+1) ...
Setting up fonts-lmodern (2.004.5-6) ...
Setting up texlive-base (2020.20200804-2) ...
mktexlsr: Updating /var/lib/texmf/ls-R-TEXLIVEDIST... 
mktexlsr: Updating /var/lib/texmf/ls-R-TEXMFMAIN... 
mktexlsr: Updating /var/lib/texmf/ls-R... 
mktexlsr: Done.
tl-paper: setting paper size for dvips to a4: /var/lib/texmf/dvips/config/config-paper.ps
tl-paper: setting paper size for dvipdfmx to a4: /var/lib/texmf/dvipdfmx/dvipdfmx-paper.cfg
tl-paper: setting paper size for xdvi to a4: /var/lib/texmf/xdvi/XDvi-paper
tl-paper: setting paper size for pdftex to a4: /var/lib/texmf/tex/generic/config/pdftexconfig.tex
Setting up ruby-xmlrpc (0.3.0-2) ...
Setting up tex-gyre (20180621-3) ...
Setting up node-jquery (3.5.1+dfsg-4) ...
Setting up teckit (2.5.8+ds2-5ubuntu2) ...
Setting up tk8.6 (8.6.10-1) ...
Setting up libpdfbox-java (1:1.8.16-2) ...
Setting up preview-latex-style (11.91-2ubuntu2) ...
Setting up libcommons-parent-java (43-1) ...
Setting up texlive-plain-generic (2020.20200804-3) ...
Setting up libcommons-logging-java (1.2-2) ...
Setting up texlive-latex-base (2020.20200804-2) ...
Setting up texlive-latex-recommended (2020.20200804-2) ...
Setting up texlive-pictures (2020.20200804-2) ...
Setting up lmodern (2.004.5-6) ...
Setting up texlive-fonts-recommended (2020.20200804-2) ...
Setting up tipa (2:1.3-20) ...
Regenerating '/var/lib/texmf/fmtutil.cnf-DEBIAN'... done.
Regenerating '/var/lib/texmf/fmtutil.cnf-TEXLIVEDIST'... done.
update-fmtutil has updated the following file(s):
	/var/lib/texmf/fmtutil.cnf-DEBIAN
	/var/lib/texmf/fmtutil.cnf-TEXLIVEDIST
If you want to activate the changes in the above file(s),
you should run fmtutil-sys or fmtutil.
Setting up libjs-jquery (3.5.1+dfsg-4) ...
Setting up tk (8.6.9+1) ...
Setting up texlive-latex-extra (2020.20200804-3) ...
Setting up texlive-xetex (2020.20200804-2) ...
Setting up libruby2.7:amd64 (2.7.1-3ubuntu1.1) ...
Setting up ruby2.7 (2.7.1-3ubuntu1.1) ...
Setting up ruby (1:2.7+1) ...
Setting up rake (13.0.1-4) ...
Processing triggers for install-info (6.7.0.dfsg.2-5) ...
install-info: warning: no info dir entry in `/usr/share/info/automake-history.info.gz'
Processing triggers for fontconfig (2.13.1-2ubuntu3) ...
Processing triggers for desktop-file-utils (0.24-1ubuntu4) ...
Processing triggers for mime-support (3.64ubuntu1) ...
Processing triggers for gnome-menus (3.36.0-1ubuntu1) ...
Processing triggers for libc-bin (2.32-0ubuntu3) ...
Processing triggers for man-db (2.9.3-2) ...
Processing triggers for tex-common (6.15) ...
Running updmap-sys. This may take some time... done.
Running mktexlsr /var/lib/texmf ... done.
Building format(s) --all.
	This may take some time... done.
```

## check with --help

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ xelatex --help
Usage: xetex [OPTION]... [TEXNAME[.tex]] [COMMANDS]
   or: xetex [OPTION]... \FIRST-LINE
   or: xetex [OPTION]... &FMT ARGS
  Run XeTeX on TEXNAME, usually creating TEXNAME.pdf.
  Any remaining COMMANDS are processed as XeTeX input, after TEXNAME is read.
  If the first line of TEXNAME is %&FMT, and FMT is an existing .fmt file,
  use it.  Else use `NAME.fmt', where NAME is the program invocation name,
  most commonly `xetex'.

  Alternatively, if the first non-option argument begins with a backslash,
  interpret all non-option arguments as a line of XeTeX input.

  Alternatively, if the first non-option argument begins with a &, the
  next word is taken as the FMT to read, overriding all else.  Any
  remaining arguments are processed as above.

  If no arguments or options are specified, prompt for input.

-cnf-line=STRING        parse STRING as a configuration file line
-etex                   enable e-TeX extensions
[-no]-file-line-error   disable/enable file:line:error style messages
-fmt=FMTNAME            use FMTNAME instead of program name or a %& line
-halt-on-error          stop processing at the first error
-ini                    be xeinitex, for dumping formats; this is implicitly
                          true if the program name is `xeinitex'
-interaction=STRING     set interaction mode (STRING=batchmode/nonstopmode/
                          scrollmode/errorstopmode)
-jobname=STRING         set the job name to STRING
-kpathsea-debug=NUMBER  set path searching debugging flags according to
                          the bits of NUMBER
[-no]-mktex=FMT         disable/enable mktexFMT generation (FMT=tex/tfm)
-mltex                  enable MLTeX extensions such as \charsubdef
-output-comment=STRING  use STRING for XDV file comment instead of date
-output-directory=DIR   use existing DIR as the directory to write files in
-output-driver=CMD      use CMD as the XDV-to-PDF driver instead of xdvipdfmx
-no-pdf                 generate XDV (extended DVI) output rather than PDF
[-no]-parse-first-line  disable/enable parsing of first line of input file
-papersize=STRING       set PDF media size to STRING
-progname=STRING        set program (and fmt) name to STRING
-recorder               enable filename recorder
[-no]-shell-escape      disable/enable \write18{SHELL COMMAND}
-shell-restricted       enable restricted \write18
-src-specials           insert source specials into the XDV file
-src-specials=WHERE     insert source specials in certain places of
                          the XDV file. WHERE is a comma-separated value
                          list: cr display hbox math par parend vbox
-synctex=NUMBER         generate SyncTeX data for previewers according to
                          bits of NUMBER (`man synctex' for details)
-translate-file=TCXNAME (ignored)
-8bit                   make all characters printable, don't use ^^X sequences
-help                   display this help and exit
-version                output version information and exit

Email bug reports to xetex@tug.org.
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$
```

## Prepare Makefile

တကယ်တမ်း စာတမ်းကို ရေးတဲ့အခါမှာတော့ gedit လို text editor ပေါ်မှာ စာတမ်းရေးလိုက် xelatex နဲ့ compile လုပ်လိုက် အကြိမ်ကြိမ်အခါခါ လုပ်ရတာမို့...
Makefile ကို အောက်ပါအတိုင်း ပြင်ပြီး သုံးပါတယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/paper/ACL2021/wfst-mt/paper/latex$ cat Makefile 
.PHONY: all clean view

FILE=wfst-mt

all: $(FILE).pdf

clean:
	rm $(FILE).pdf *.aux *.log *.blg *.bbl

view:
	evince $(FILE).pdf
	#qpdfview $(FILE).pdf

$(FILE).pdf: $(FILE).tex
	xelatex $(FILE).tex
	xelatex $(FILE).tex
	#bibtex $(FILE)
	evince $(FILE).pdf
```

## File Information


Here, I used ACL conf. template  
Link: [https://2021.aclweb.org/calls/papers/#call-for-papers---main-conference](https://2021.aclweb.org/calls/papers/#call-for-papers---main-conference)  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/paper/ACL2021/wfst-mt/paper/latex$ ls
acl2021.bib  acl2021.sty  acl2021.tex  acl_natbib.bst  anthology.bib  Makefile  wfst-mt.tex
```

## run make command

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/paper/ACL2021/wfst-mt/paper/latex$ make
xelatex wfst-mt.tex
This is XeTeX, Version 3.14159265-2.6-0.999992 (TeX Live 2020/Debian) (preloaded format=xelatex)
 restricted \write18 enabled.
entering extended mode
(./wfst-mt.tex
LaTeX2e <2020-02-02> patch level 5
L3 programming layer <2020-07-17>
(/usr/share/texlive/texmf-dist/tex/latex/base/article.cls
Document Class: article 2019/12/20 v1.4l Standard LaTeX document class
(/usr/share/texlive/texmf-dist/tex/latex/base/size11.clo)) (./acl2021.sty
(/usr/share/texlive/texmf-dist/tex/latex/hyperref/hyperref.sty
(/usr/share/texlive/texmf-dist/tex/generic/ltxcmds/ltxcmds.sty)
(/usr/share/texlive/texmf-dist/tex/generic/iftex/iftex.sty)
(/usr/share/texlive/texmf-dist/tex/generic/pdftexcmds/pdftexcmds.sty
(/usr/share/texlive/texmf-dist/tex/generic/infwarerr/infwarerr.sty))
(/usr/share/texlive/texmf-dist/tex/latex/graphics/keyval.sty)
(/usr/share/texlive/texmf-dist/tex/generic/kvsetkeys/kvsetkeys.sty)
(/usr/share/texlive/texmf-dist/tex/generic/kvdefinekeys/kvdefinekeys.sty)
(/usr/share/texlive/texmf-dist/tex/generic/pdfescape/pdfescape.sty)
(/usr/share/texlive/texmf-dist/tex/latex/hycolor/hycolor.sty)
(/usr/share/texlive/texmf-dist/tex/latex/letltxmacro/letltxmacro.sty)
(/usr/share/texlive/texmf-dist/tex/latex/auxhook/auxhook.sty)
(/usr/share/texlive/texmf-dist/tex/latex/kvoptions/kvoptions.sty)
(/usr/share/texlive/texmf-dist/tex/latex/hyperref/pd1enc.def)
(/usr/share/texlive/texmf-dist/tex/generic/intcalc/intcalc.sty)
(/usr/share/texlive/texmf-dist/tex/generic/etexcmds/etexcmds.sty)
(/usr/share/texlive/texmf-dist/tex/latex/url/url.sty)
(/usr/share/texlive/texmf-dist/tex/generic/bitset/bitset.sty
(/usr/share/texlive/texmf-dist/tex/generic/bigintcalc/bigintcalc.sty))
(/usr/share/texlive/texmf-dist/tex/generic/atbegshi/atbegshi.sty))
(/usr/share/texlive/texmf-dist/tex/latex/hyperref/hxetex.def
(/usr/share/texlive/texmf-dist/tex/latex/hyperref/puenc.def)
(/usr/share/texlive/texmf-dist/tex/generic/stringenc/stringenc.sty)
(/usr/share/texlive/texmf-dist/tex/latex/rerunfilecheck/rerunfilecheck.sty
(/usr/share/texlive/texmf-dist/tex/latex/atveryend/atveryend.sty)
(/usr/share/texlive/texmf-dist/tex/generic/uniquecounter/uniquecounter.sty)))
(/usr/share/texlive/texmf-dist/tex/latex/xcolor/xcolor.sty
(/usr/share/texlive/texmf-dist/tex/latex/graphics-cfg/color.cfg)
(/usr/share/texlive/texmf-dist/tex/latex/graphics-def/xetex.def))
Conference Style for ACL-IJCNLP 2021
(/usr/share/texlive/texmf-dist/tex/latex/caption/caption.sty
(/usr/share/texlive/texmf-dist/tex/latex/caption/caption3.sty))
(/usr/share/texlive/texmf-dist/tex/latex/natbib/natbib.sty)
(/usr/share/texlive/texmf-dist/tex/latex/etoolbox/etoolbox.sty))
(/usr/share/texlive/texmf-dist/tex/latex/psnfss/times.sty)
(/usr/share/texlive/texmf-dist/tex/latex/base/latexsym.sty)
(/usr/share/texlive/texmf-dist/tex/latex/microtype/microtype.sty
(/usr/share/texlive/texmf-dist/tex/latex/microtype/microtype-xetex.def)
(/usr/share/texlive/texmf-dist/tex/latex/microtype/microtype.cfg))
(/usr/share/texlive/texmf-dist/tex/latex/l3backend/l3backend-xdvipdfmx.def)
No file wfst-mt.aux.
(/usr/share/texlive/texmf-dist/tex/latex/base/ts1cmr.fd)

LaTeX Font Warning: Font shape `TU/ptm/m/n' undefined
(Font)              using `TU/lmr/m/n' instead on input line 53.

(/usr/share/texlive/texmf-dist/tex/latex/hyperref/nameref.sty
(/usr/share/texlive/texmf-dist/tex/latex/refcount/refcount.sty)
(/usr/share/texlive/texmf-dist/tex/generic/gettitlestring/gettitlestring.sty))

Package hyperref Warning: Rerun to get /PageLabels entry.

ABD: EveryShipout initializing macros
(/usr/share/texlive/texmf-dist/tex/latex/microtype/mt-ptm.cfg)

LaTeX Font Warning: Font shape `TU/ptm/b/n' undefined
(Font)              using `TU/ptm/m/n' instead on input line 54.

(/usr/share/texlive/texmf-dist/tex/latex/microtype/mt-cmr.cfg)
(/usr/share/texlive/texmf-dist/tex/latex/base/ulasy.fd)

LaTeX Font Warning: Font shape `TU/ptm/m/it' undefined
(Font)              using `TU/ptm/m/n' instead on input line 82.


Underfull \hbox (badness 1270) in paragraph at lines 64--83
\TU/ptm/m/it/10.95 Moore, Simone Teufel, James Allan, and

LaTeX Font Warning: Font shape `TU/pcr/m/n' undefined
(Font)              using `TU/lmr/m/n' instead on input line 96.

(/usr/share/texlive/texmf-dist/tex/latex/microtype/mt-LatinModernRoman.cfg)
Underfull \hbox (badness 10000) in paragraph at lines 96--97
[][][]$[][][][][] [] [] [] [][][][] [] [][][][][][] [] [][][] [] [][][][][] []
(/usr/share/texlive/texmf-dist/tex/generic/stringenc/se-ascii-print.def)
[1]

LaTeX Warning: Reference `sec:supplementary' on page 2 undefined on input line 
121.


Package natbib Warning: Citation `Gusfield:97' on page 2 undefined on input lin
e 130.


Package natbib Warning: Citation `Gusfield:97' on page 2 undefined on input lin
e 134.


Underfull \hbox (badness 1286) in paragraph at lines 148--150
 []\TU/pcr/m/n/10.95 L[]T[]X-specific details: For an anonymized

Underfull \hbox (badness 1831) in paragraph at lines 148--150
\TU/pcr/m/n/10.95 top of this document is commented out,

LaTeX Warning: Reference `ssec:title-authors' on page 2 undefined on input line
 162.


LaTeX Warning: Reference `sec:length' on page 2 undefined on input line 165.

[2]
Underfull \hbox (badness 10000) in paragraph at lines 175--184
\TU/pcr/m/n/10.95 For the production of the electronic

Underfull \hbox (badness 1796) in paragraph at lines 190--194
 []\TU/pcr/m/n/10.95 L[]T[]X-specific details: PDF files are usu-

Underfull \hbox (badness 1442) in paragraph at lines 190--194
\TU/ptm/m/n/9 tex \TU/pcr/m/n/10.95 command. If your version of L[]T[]X

Underfull \hbox (badness 2020) in paragraph at lines 190--194
\TU/pcr/m/n/10.95 produces Postscript files, \TU/ptm/m/n/9 ps2pdf \TU/pcr/m/n/1
0.95 or \TU/ptm/m/n/9 dvipdf

Underfull \hbox (badness 5924) in paragraph at lines 190--194
\TU/pcr/m/n/10.95 can convert these to PDF. To ensure

Underfull \hbox (badness 2903) in paragraph at lines 190--194
\TU/pcr/m/n/10.95 A4 format in L[]T[]X, use the command

LaTeX Warning: Reference `font-table' on page 3 undefined on input line 219.

[3]
Underfull \hbox (badness 1721) in paragraph at lines 278--280
[]\TU/pcr/m/n/10.95 The title, author names and addresses

LaTeX Warning: Reference `ssec:accessibility' on page 4 undefined on input line
 315.

[4]

LaTeX Warning: Reference `font-table' on page 5 undefined on input line 323.


LaTeX Warning: Reference `tab:accents' on page 5 undefined on input line 324.


LaTeX Font Warning: Font shape `TU/ptm/m/sc' undefined
(Font)              using `TU/ptm/m/n' instead on input line 353.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 365.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 365.


Package natbib Warning: Citation `Aho:72' on page 5 undefined on input line 367
.


Package natbib Warning: Citation `Chandra:81' on page 5 undefined on input line
 367.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 367.


Package natbib Warning: Citation `Aho:72' on page 5 undefined on input line 367
.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 372.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 376.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 385.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 386.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 387.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 388.


LaTeX Warning: Reference `citation-guide' on page 5 undefined on input line 399
.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 401.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 402.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 403.


Package natbib Warning: Citation `APA:83' on page 5 undefined on input line 411
.


Underfull \hbox (badness 2884) in paragraph at lines 414--418
[]\TU/pcr/m/n/10.95 Submissions should accurately reference

Package natbib Warning: Citation `Ando2005' on page 5 undefined on input line 4
21.


Package natbib Warning: Citation `borschinger-johnson-2011-particle' on page 5 
undefined on input line 422.


Package natbib Warning: Citation `andrew2007scalable' on page 5 undefined on in
put line 423.


Package natbib Warning: Citation `rasooli-tetrault-2015' on page 5 undefined on
 input line 424.


Underfull \hbox (badness 10000) in paragraph at lines 429--431
 []\TU/pcr/m/n/10.95 L[]T[]X-specific details: The L[]T[]X and
[5]

Package natbib Warning: Citation `goodman-etal-2016-noise' on page 6 undefined 
on input line 449.


Package natbib Warning: Citation `harper-2014-learning' on page 6 undefined on 
input line 450.

[6]
No file wfst-mt.bbl.

Package natbib Warning: There were undefined citations.

[7] (./wfst-mt.aux)

Package rerunfilecheck Warning: File `wfst-mt.out' has changed.
(rerunfilecheck)                Rerun to get outlines right
(rerunfilecheck)                or use package `bookmark'.


LaTeX Font Warning: Some font shapes were not available, defaults substituted.


LaTeX Warning: There were undefined references.


LaTeX Warning: Label(s) may have changed. Rerun to get cross-references right.

 )
(\end occurred when \iffalse on line 352 was incomplete)
(see the transcript file for additional information)
Output written on wfst-mt.pdf (7 pages).
Transcript written on wfst-mt.log.
xelatex wfst-mt.tex
This is XeTeX, Version 3.14159265-2.6-0.999992 (TeX Live 2020/Debian) (preloaded format=xelatex)
 restricted \write18 enabled.
entering extended mode
(./wfst-mt.tex
LaTeX2e <2020-02-02> patch level 5
L3 programming layer <2020-07-17>
(/usr/share/texlive/texmf-dist/tex/latex/base/article.cls
Document Class: article 2019/12/20 v1.4l Standard LaTeX document class
(/usr/share/texlive/texmf-dist/tex/latex/base/size11.clo)) (./acl2021.sty
(/usr/share/texlive/texmf-dist/tex/latex/hyperref/hyperref.sty
(/usr/share/texlive/texmf-dist/tex/generic/ltxcmds/ltxcmds.sty)
(/usr/share/texlive/texmf-dist/tex/generic/iftex/iftex.sty)
(/usr/share/texlive/texmf-dist/tex/generic/pdftexcmds/pdftexcmds.sty
(/usr/share/texlive/texmf-dist/tex/generic/infwarerr/infwarerr.sty))
(/usr/share/texlive/texmf-dist/tex/latex/graphics/keyval.sty)
(/usr/share/texlive/texmf-dist/tex/generic/kvsetkeys/kvsetkeys.sty)
(/usr/share/texlive/texmf-dist/tex/generic/kvdefinekeys/kvdefinekeys.sty)
(/usr/share/texlive/texmf-dist/tex/generic/pdfescape/pdfescape.sty)
(/usr/share/texlive/texmf-dist/tex/latex/hycolor/hycolor.sty)
(/usr/share/texlive/texmf-dist/tex/latex/letltxmacro/letltxmacro.sty)
(/usr/share/texlive/texmf-dist/tex/latex/auxhook/auxhook.sty)
(/usr/share/texlive/texmf-dist/tex/latex/kvoptions/kvoptions.sty)
(/usr/share/texlive/texmf-dist/tex/latex/hyperref/pd1enc.def)
(/usr/share/texlive/texmf-dist/tex/generic/intcalc/intcalc.sty)
(/usr/share/texlive/texmf-dist/tex/generic/etexcmds/etexcmds.sty)
(/usr/share/texlive/texmf-dist/tex/latex/url/url.sty)
(/usr/share/texlive/texmf-dist/tex/generic/bitset/bitset.sty
(/usr/share/texlive/texmf-dist/tex/generic/bigintcalc/bigintcalc.sty))
(/usr/share/texlive/texmf-dist/tex/generic/atbegshi/atbegshi.sty))
(/usr/share/texlive/texmf-dist/tex/latex/hyperref/hxetex.def
(/usr/share/texlive/texmf-dist/tex/latex/hyperref/puenc.def)
(/usr/share/texlive/texmf-dist/tex/generic/stringenc/stringenc.sty)
(/usr/share/texlive/texmf-dist/tex/latex/rerunfilecheck/rerunfilecheck.sty
(/usr/share/texlive/texmf-dist/tex/latex/atveryend/atveryend.sty)
(/usr/share/texlive/texmf-dist/tex/generic/uniquecounter/uniquecounter.sty)))
(/usr/share/texlive/texmf-dist/tex/latex/xcolor/xcolor.sty
(/usr/share/texlive/texmf-dist/tex/latex/graphics-cfg/color.cfg)
(/usr/share/texlive/texmf-dist/tex/latex/graphics-def/xetex.def))
Conference Style for ACL-IJCNLP 2021
(/usr/share/texlive/texmf-dist/tex/latex/caption/caption.sty
(/usr/share/texlive/texmf-dist/tex/latex/caption/caption3.sty))
(/usr/share/texlive/texmf-dist/tex/latex/natbib/natbib.sty)
(/usr/share/texlive/texmf-dist/tex/latex/etoolbox/etoolbox.sty))
(/usr/share/texlive/texmf-dist/tex/latex/psnfss/times.sty)
(/usr/share/texlive/texmf-dist/tex/latex/base/latexsym.sty)
(/usr/share/texlive/texmf-dist/tex/latex/microtype/microtype.sty
(/usr/share/texlive/texmf-dist/tex/latex/microtype/microtype-xetex.def)
(/usr/share/texlive/texmf-dist/tex/latex/microtype/microtype.cfg))
(/usr/share/texlive/texmf-dist/tex/latex/l3backend/l3backend-xdvipdfmx.def)
(./wfst-mt.aux) (/usr/share/texlive/texmf-dist/tex/latex/base/ts1cmr.fd)

LaTeX Font Warning: Font shape `TU/ptm/m/n' undefined
(Font)              using `TU/lmr/m/n' instead on input line 53.

(/usr/share/texlive/texmf-dist/tex/latex/hyperref/nameref.sty
(/usr/share/texlive/texmf-dist/tex/latex/refcount/refcount.sty)
(/usr/share/texlive/texmf-dist/tex/generic/gettitlestring/gettitlestring.sty))
(./wfst-mt.out) (./wfst-mt.out) ABD: EveryShipout initializing macros
(/usr/share/texlive/texmf-dist/tex/latex/microtype/mt-ptm.cfg)

LaTeX Font Warning: Font shape `TU/ptm/b/n' undefined
(Font)              using `TU/ptm/m/n' instead on input line 54.

(/usr/share/texlive/texmf-dist/tex/latex/microtype/mt-cmr.cfg)
(/usr/share/texlive/texmf-dist/tex/latex/base/ulasy.fd)

LaTeX Font Warning: Font shape `TU/ptm/m/it' undefined
(Font)              using `TU/ptm/m/n' instead on input line 82.


Underfull \hbox (badness 1270) in paragraph at lines 64--83
\TU/ptm/m/it/10.95 Moore, Simone Teufel, James Allan, and

LaTeX Font Warning: Font shape `TU/pcr/m/n' undefined
(Font)              using `TU/lmr/m/n' instead on input line 96.

(/usr/share/texlive/texmf-dist/tex/latex/microtype/mt-LatinModernRoman.cfg)
Underfull \hbox (badness 10000) in paragraph at lines 96--97
[][][]$[][][][][] [] [] [] [][][][] [] [][][][][][] [] [][][] [] [][][][][] []
(/usr/share/texlive/texmf-dist/tex/generic/stringenc/se-ascii-print.def)
[1]

Package natbib Warning: Citation `Gusfield:97' on page 2 undefined on input lin
e 130.


Package natbib Warning: Citation `Gusfield:97' on page 2 undefined on input lin
e 134.


Underfull \hbox (badness 1286) in paragraph at lines 148--150
 []\TU/pcr/m/n/10.95 L[]T[]X-specific details: For an anonymized

Underfull \hbox (badness 1831) in paragraph at lines 148--150
\TU/pcr/m/n/10.95 top of this document is commented out,
[2]
Underfull \hbox (badness 10000) in paragraph at lines 175--184
\TU/pcr/m/n/10.95 For the production of the electronic

Underfull \hbox (badness 1796) in paragraph at lines 190--194
 []\TU/pcr/m/n/10.95 L[]T[]X-specific details: PDF files are usu-

Underfull \hbox (badness 1442) in paragraph at lines 190--194
\TU/ptm/m/n/9 tex \TU/pcr/m/n/10.95 command. If your version of L[]T[]X

Underfull \hbox (badness 2020) in paragraph at lines 190--194
\TU/pcr/m/n/10.95 produces Postscript files, \TU/ptm/m/n/9 ps2pdf \TU/pcr/m/n/1
0.95 or \TU/ptm/m/n/9 dvipdf

Underfull \hbox (badness 5924) in paragraph at lines 190--194
\TU/pcr/m/n/10.95 can convert these to PDF. To ensure

Underfull \hbox (badness 2903) in paragraph at lines 190--194
\TU/pcr/m/n/10.95 A4 format in L[]T[]X, use the command
[3]
Underfull \hbox (badness 1721) in paragraph at lines 278--280
[]\TU/pcr/m/n/10.95 The title, author names and addresses
[4]

LaTeX Font Warning: Font shape `TU/ptm/m/sc' undefined
(Font)              using `TU/ptm/m/n' instead on input line 353.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 365.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 365.


Package natbib Warning: Citation `Aho:72' on page 5 undefined on input line 367
.


Package natbib Warning: Citation `Chandra:81' on page 5 undefined on input line
 367.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 367.


Package natbib Warning: Citation `Aho:72' on page 5 undefined on input line 367
.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 372.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 376.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 385.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 386.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 387.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 388.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 401.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 402.


Package natbib Warning: Citation `Gusfield:97' on page 5 undefined on input lin
e 403.


Package natbib Warning: Citation `APA:83' on page 5 undefined on input line 411
.


Underfull \hbox (badness 2884) in paragraph at lines 414--418
[]\TU/pcr/m/n/10.95 Submissions should accurately reference

Package natbib Warning: Citation `Ando2005' on page 5 undefined on input line 4
21.


Package natbib Warning: Citation `borschinger-johnson-2011-particle' on page 5 
undefined on input line 422.


Package natbib Warning: Citation `andrew2007scalable' on page 5 undefined on in
put line 423.


Package natbib Warning: Citation `rasooli-tetrault-2015' on page 5 undefined on
 input line 424.


Underfull \hbox (badness 10000) in paragraph at lines 429--431
 []\TU/pcr/m/n/10.95 L[]T[]X-specific details: The L[]T[]X and
[5]

Package natbib Warning: Citation `goodman-etal-2016-noise' on page 6 undefined 
on input line 449.


Package natbib Warning: Citation `harper-2014-learning' on page 6 undefined on 
input line 450.

[6]
No file wfst-mt.bbl.

Package natbib Warning: There were undefined citations.

[7] (./wfst-mt.aux)

LaTeX Font Warning: Some font shapes were not available, defaults substituted.

 )
(\end occurred when \iffalse on line 352 was incomplete)
(see the transcript file for additional information)
Output written on wfst-mt.pdf (7 pages).
Transcript written on wfst-mt.log.
#bibtex wfst-mt
evince wfst-mt.pdf
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/paper/ACL2021/wfst-mt/paper/latex$
```

## Output PDF file

Makefile က အဆင်ပြေပြေနဲ့ compile error မဖြစ်ခဲ့ဘူး ကိုယ့်စက်ထဲမှာ PDF viewer တစ်ခုဖြစ်တဲ့ evince ကိုလည်း install လုပ်ထားတယ်ဆိုရင် compile လုပ်ပြီးထွက်လာတဲ့ PDF ဖိုင်ကို ဖွင့်ပေးပါလိမ့်မယ်။  
compile လုပ်ပြီးတဲ့အခါမှာ wfst-mt.pdf ကိုအောက်ပါအတိုင်း တွေ့ရပါလိမ့်မယ်။  

```
(base) ye@administrator-HP-Z2-Tower-G4-Workstation:~/paper/ACL2021/wfst-mt/paper/latex$ ls
acl2021.bib  acl2021.sty  acl2021.tex  acl_natbib.bst  anthology.bib  Makefile  wfst-mt.aux  wfst-mt.log  wfst-mt.out  wfst-mt.pdf  wfst-mt.tex
```

## Reference

[https://tex.stackexchange.com/questions/179778/xelatex-under-ubuntu](https://tex.stackexchange.com/questions/179778/xelatex-under-ubuntu)  


