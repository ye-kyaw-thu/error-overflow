# SRILM Installation Note

Download from the following site:
http://www.speech.sri.com/projects/srilm/download.html

# Unzip with tar command

root@2223cfe7eb4a:/home/yekyawthu/tool/srilm# tar -xzvf srilm-1.7.2.tar.gz
./misc/src/SRILMversion.h
./misc/src/fcheck.h
./misc/src/testFile.cc
./misc/src/zio.h
./misc/doc/
./misc/doc/tmac.sprite
./misc/doc/Opt.man
./misc/doc/Opt.doc

# Check inside srilm folder

root@2223cfe7eb4a:/home/yekyawthu/tool/srilm# ls
ACKNOWLEDGEMENTS  INSTALL   README   doc      go.build-android       lattice  man   srilm-1.7.2.tar.gz  zlib
CHANGES           License   RELEASE  dstruct  go.build-android-hard  lib      misc  utils
Copyright         Makefile  common   flm      go.build-android-v8    lm       sbin  visual_studio

# Read INSTALL file

root@2223cfe7eb4a:/home/yekyawthu/tool/srilm# vi INSTALL 

# Update Makefile
root@2223cfe7eb4a:/home/yekyawthu/tool/srilm# nano Makefile 

# SRILM = /home/speech/stolcke/project/srilm/devel
# Add your path here, for example
SRILM = /usr/share/srilm/

# Check tcsh

root@2223cfe7eb4a:/home/yekyawthu/tool/srilm# tcsh --help
-su: tcsh: command not found

# We need to install tcsh

Here, I am running on a docker env with root user account.

For your case, use "sudo" command:

root@2223cfe7eb4a:/home/yekyawthu/tool/srilm# apt-get install tcsh
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following NEW packages will be installed:
  tcsh
0 upgraded, 1 newly installed, 0 to remove and 85 not upgraded.
Need to get 410 kB of archives.
After this operation, 1310 kB of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu xenial/universe amd64 tcsh amd64 6.18.01-5 [410 kB]
Fetched 410 kB in 1s (219 kB/s)                      
debconf: delaying package configuration, since apt-utils is not installed
Selecting previously unselected package tcsh.
(Reading database ... 37958 files and directories currently installed.)
Preparing to unpack .../tcsh_6.18.01-5_amd64.deb ...
Unpacking tcsh (6.18.01-5) ...
Setting up tcsh (6.18.01-5) ...
update-alternatives: using /bin/tcsh to provide /bin/csh (csh) in auto mode

# Now "tcsh --help" command work (i.e. your installation of tcsh success):

root@2223cfe7eb4a:/home/yekyawthu/tool/srilm# tcsh --help
tcsh 6.18.01 (Astron) 2012-02-14 (x86_64-unknown-linux) options wide,nls,dl,al,kan,rh,nd,color,filec

-b file		batch mode, read and execute commands from `file' 
-c command	run `command' from next argument 
-d		load directory stack from `~/.cshdirs' 
-Dname[=value]	define environment variable `name' to `value' (DomainOS only) 
-e		exit on any error 
-f		start faster by ignoring the start-up file 
-F		use fork() instead of vfork() when spawning (ConvexOS only) 
-i		interactive, even when input is not from a terminal 
-l		act as a login shell, must be the only option specified 
-m		load the start-up file, whether or not owned by effective user 
-n file		no execute mode, just check syntax of the following `file' 
-q		accept SIGQUIT for running under a debugger 
-s		read commands from standard input 
-t		read one line from standard input 
-v		echo commands after history substitution 
-V		like -v but including commands read from the start-up file 
-x		echo commands immediately before execution 
-X		like -x but including commands read from the start-up file 
--help		print this message and exit 
--version	print the version shell variable and exit 

See the tcsh(1) manual page for detailed information.


# make

root@2223cfe7eb4a:/home/yekyawthu/tool/srilm# make SRILM=/home/yekyawthu/tool/srilm World

/home/yekyawthu/tool/srilm/sbin/decipher-install 0555 compute-sclite ../../bin
/home/yekyawthu/tool/srilm/sbin/decipher-install 0555 compute-sclite-nbest ../../bin
/home/yekyawthu/tool/srilm/sbin/decipher-install 0555 compare-sclite ../../bin
/home/yekyawthu/tool/srilm/sbin/decipher-install 0555 cumbin ../../bin
make[2]: Leaving directory '/home/yekyawthu/tool/srilm/utils/src'
make[2]: Entering directory '/home/yekyawthu/tool/srilm/zlib/src'
make[2]: Nothing to be done for 'release-scripts'.
make[2]: Leaving directory '/home/yekyawthu/tool/srilm/zlib/src'
make[1]: Leaving directory '/home/yekyawthu/tool/srilm'

# Browse the folder:

root@2223cfe7eb4a:/home/yekyawthu/tool/srilm/bin/i686-m64# ls
add-classes-to-pfsg        continuous-ngram-count     lattice-tool        metadb            pfsg-to-fsm                 sort-lm
add-dummy-bows             de-vq-lm                   log10-to-bytelog    multi-ngram       pfsg-vocab                  split-tagged-ngrams
add-pauses-to-pfsg         disambig                   make-abs-discount   nbest-lattice     ppl-from-log                subset-context-ngrams
add-ppls                   extract-skip-probs         make-diacritic-map  nbest-mix         prettify                    subtract-ppls
anti-ngram                 filter-event-counts        make-google-ngrams  nbest-optimize    remove-lowprob-ngrams       tolower-ngram-counts
bytelog-to-log10           find-reference-posteriors  make-gt-discounts   nbest-posteriors  replace-unk-words           uniform-classes
classes-to-fsm             fix-ctm                    make-hiddens-lm     nbest-pron-score  replace-words-with-classes  uniq-ngram-counts
combine-acoustic-scores    fngram                     make-kn-counts      nbest-vocab       reverse-lm                  vp2text
combine-rover-controls     fngram-count               make-kn-discounts   nbest-words       reverse-ngram-counts        wlat-stats
compare-ppls               fsm-to-pfsg                make-lm-subset      nbest2-to-nbest1  reverse-text                wlat-to-dot
compute-best-mix           get-gt-counts              make-nbest-pfsg     ngram             segment                     wlat-to-pfsg
compute-best-rover-mix     get-unigram-probs          make-ngram-pfsg     ngram-class       segment-nbest               wordlat-to-lisp
compute-best-sentence-mix  hidden-ngram               make-sub-lm         ngram-count       select-vocab
compute-oov-rate           hits-from-log              maxalloc            ngram-merge       sentid-to-ctm
context-ngrams             htklat-vocab               merge-nbest         pfsg-to-dot       sentid-to-sclite

# Update your PATH:

vi ~/.bashrc
export PATH="/home/yekyawthu/tool/srilm/bin/i686-m64:$PATH"

source ~/.bashrc


# Confirm SRILM installation is success or not:

root@2223cfe7eb4a:/home/yekyawthu/tool/srilm# ngram-count -help
Usage of command "ngram-count"
 -version:                 print version information
 -order:                   max ngram order
		Default value: 3
 -varprune:                pruning threshold for variable order ngrams
		Default value: 0
 -debug:                   debugging level for LM
		Default value: 0
 -recompute:               recompute lower-order counts by summation
 -sort:                    sort ngrams output
 -write-order:             output ngram counts order
		Default value: 0
 -tag:                     file tag to use in messages
 -text:                    text file to read
 -text-has-weights:        text file contains count weights
 -no-sos:                  don't insert start-of-sentence tokens
 -no-eos:                  don't insert end-of-sentence tokens
 -read:                    counts file to read
 -intersect:               intersect counts with this file
 -read-with-mincounts:     apply minimum counts when reading counts file
 -read-google:             Google counts directory to read
 -write:                   counts file to write
 -write1:                  1gram counts file to write
 -write2:                  2gram counts file to write
 -write3:                  3gram counts file to write
 -write4:                  4gram counts file to write
 -write5:                  5gram counts file to write
 -write6:                  6gram counts file to write
 -write7:                  7gram counts file to write
 -write8:                  8gram counts file to write
 -write9:                  9gram counts file to write
 -write-binary:            binary counts file to write
 -gtmin:                   lower GT discounting cutoff
		Default value: 1
 -gtmax:                   upper GT discounting cutoff
		Default value: 5
 -gt1min:                  lower 1gram discounting cutoff
		Default value: 1
 -gt1max:                  upper 1gram discounting cutoff
		Default value: 1
 -gt2min:                  lower 2gram discounting cutoff
		Default value: 1
 -gt2max:                  upper 2gram discounting cutoff
		Default value: 7
 -gt3min:                  lower 3gram discounting cutoff
		Default value: 2
 -gt3max:                  upper 3gram discounting cutoff
		Default value: 7
 -gt4min:                  lower 4gram discounting cutoff
		Default value: 2
 -gt4max:                  upper 4gram discounting cutoff
		Default value: 7
 -gt5min:                  lower 5gram discounting cutoff
		Default value: 2
 -gt5max:                  upper 5gram discounting cutoff
		Default value: 7
 -gt6min:                  lower 6gram discounting cutoff
		Default value: 2
 -gt6max:                  upper 6gram discounting cutoff
		Default value: 7
 -gt7min:                  lower 7gram discounting cutoff
		Default value: 2
 -gt7max:                  upper 7gram discounting cutoff
		Default value: 7
 -gt8min:                  lower 8gram discounting cutoff
		Default value: 2
 -gt8max:                  upper 8gram discounting cutoff
		Default value: 7
 -gt9min:                  lower 9gram discounting cutoff
		Default value: 2
 -gt9max:                  upper 9gram discounting cutoff
		Default value: 7
 -gt:                      Good-Turing discount parameter file
 -gt1:                     Good-Turing 1gram discounts
 -gt2:                     Good-Turing 2gram discounts
 -gt3:                     Good-Turing 3gram discounts
 -gt4:                     Good-Turing 4gram discounts
 -gt5:                     Good-Turing 5gram discounts
 -gt6:                     Good-Turing 6gram discounts
 -gt7:                     Good-Turing 7gram discounts
 -gt8:                     Good-Turing 8gram discounts
 -gt9:                     Good-Turing 9gram discounts
 -cdiscount:               discounting constant
		Default value: -1
 -cdiscount1:              1gram discounting constant
		Default value: -1
 -cdiscount2:              2gram discounting constant
		Default value: -1
 -cdiscount3:              3gram discounting constant
		Default value: -1
 -cdiscount4:              4gram discounting constant
		Default value: -1
 -cdiscount5:              5gram discounting constant
		Default value: -1
 -cdiscount6:              6gram discounting constant
		Default value: -1
 -cdiscount7:              7gram discounting constant
		Default value: -1
 -cdiscount8:              8gram discounting constant
		Default value: -1
 -cdiscount9:              9gram discounting constant
		Default value: -1
 -ndiscount:               use natural discounting
 -ndiscount1:              1gram natural discounting
 -ndiscount2:              2gram natural discounting
 -ndiscount3:              3gram natural discounting
 -ndiscount4:              4gram natural discounting
 -ndiscount5:              5gram natural discounting
 -ndiscount6:              6gram natural discounting
 -ndiscount7:              7gram natural discounting
 -ndiscount8:              8gram natural discounting
 -ndiscount9:              9gram natural discounting
 -addsmooth:               additive smoothing constant
		Default value: -1
 -addsmooth1:              1gram additive smoothing constant
		Default value: -1
 -addsmooth2:              2gram additive smoothing constant
		Default value: -1
 -addsmooth3:              3gram additive smoothing constant
		Default value: -1
 -addsmooth4:              4gram additive smoothing constant
		Default value: -1
 -addsmooth5:              5gram additive smoothing constant
		Default value: -1
 -addsmooth6:              6gram additive smoothing constant
		Default value: -1
 -addsmooth7:              7gram additive smoothing constant
		Default value: -1
 -addsmooth8:              8gram additive smoothing constant
		Default value: -1
 -addsmooth9:              9gram additive smoothing constant
		Default value: -1
 -wbdiscount:              use Witten-Bell discounting
 -wbdiscount1:             1gram Witten-Bell discounting
 -wbdiscount2:             2gram Witten-Bell discounting
 -wbdiscount3:             3gram Witten-Bell discounting
 -wbdiscount4:             4gram Witten-Bell discounting
 -wbdiscount5:             5gram Witten-Bell discounting
 -wbdiscount6:             6gram Witten-Bell discounting
 -wbdiscount7:             7gram Witten-Bell discounting
 -wbdiscount8:             8gram Witten-Bell discounting
 -wbdiscount9:             9gram Witten-Bell discounting
 -kndiscount:              use modified Kneser-Ney discounting
 -kndiscount1:             1gram modified Kneser-Ney discounting
 -kndiscount2:             2gram modified Kneser-Ney discounting
 -kndiscount3:             3gram modified Kneser-Ney discounting
 -kndiscount4:             4gram modified Kneser-Ney discounting
 -kndiscount5:             5gram modified Kneser-Ney discounting
 -kndiscount6:             6gram modified Kneser-Ney discounting
 -kndiscount7:             7gram modified Kneser-Ney discounting
 -kndiscount8:             8gram modified Kneser-Ney discounting
 -kndiscount9:             9gram modified Kneser-Ney discounting
 -ukndiscount:             use original Kneser-Ney discounting
 -ukndiscount1:            1gram original Kneser-Ney discounting
 -ukndiscount2:            2gram original Kneser-Ney discounting
 -ukndiscount3:            3gram original Kneser-Ney discounting
 -ukndiscount4:            4gram original Kneser-Ney discounting
 -ukndiscount5:            5gram original Kneser-Ney discounting
 -ukndiscount6:            6gram original Kneser-Ney discounting
 -ukndiscount7:            7gram original Kneser-Ney discounting
 -ukndiscount8:            8gram original Kneser-Ney discounting
 -ukndiscount9:            9gram original Kneser-Ney discounting
 -kn:                      Kneser-Ney discount parameter file
 -kn1:                     Kneser-Ney 1gram discounts
 -kn2:                     Kneser-Ney 2gram discounts
 -kn3:                     Kneser-Ney 3gram discounts
 -kn4:                     Kneser-Ney 4gram discounts
 -kn5:                     Kneser-Ney 5gram discounts
 -kn6:                     Kneser-Ney 6gram discounts
 -kn7:                     Kneser-Ney 7gram discounts
 -kn8:                     Kneser-Ney 8gram discounts
 -kn9:                     Kneser-Ney 9gram discounts
 -kn-counts-modified:      input counts already modified for KN smoothing
 -kn-modify-counts-at-end: modify counts after discount estimation rather than before
 -interpolate:             use interpolated estimates
 -interpolate1:            use interpolated 1gram estimates
 -interpolate2:            use interpolated 2gram estimates
 -interpolate3:            use interpolated 3gram estimates
 -interpolate4:            use interpolated 4gram estimates
 -interpolate5:            use interpolated 5gram estimates
 -interpolate6:            use interpolated 6gram estimates
 -interpolate7:            use interpolated 7gram estimates
 -interpolate8:            use interpolated 8gram estimates
 -interpolate9:            use interpolated 9gram estimates
 -lm:                      LM to estimate
 -write-binary-lm:         output LM in binary format
 -init-lm:                 initial LM for EM estimation
 -unk:                     keep <unk> in LM
 -map-unk:                 word to map unknown words to
 -meta-tag:                meta tag used to input count-of-count information
 -float-counts:            use fractional counts
 -tagged:                  build a tagged LM
 -count-lm:                train a count-based LM
 -skip:                    build a skip N-gram LM
 -skip-init:               default initial skip probability
		Default value: 0.5
 -em-iters:                max number of EM iterations
		Default value: 100
 -em-delta:                min log likelihood delta for EM
		Default value: 0.001
 -stop-words:              stop-word vocabulary for stop-Ngram LM
 -maxent:                  Estimate maximum entropy model
 -maxent-alpha:            The L1 regularisation constant for max-ent estimation
		Default value: 0.5
 -maxent-sigma2:           The L2 regularisation constant for max-ent estimation (default: 6 for estimation, 0.5 for adaptation)
		Default value: 0
 -maxent-convert-to-arpa:  Save estimated max-ent model as a regular ARPA backoff model
 -tolower:                 map vocabulary to lowercase
 -trust-totals:            trust lower-order counts for estimation
 -prune:                   prune redundant probs
		Default value: 0
 -minprune:                prune only ngrams at least this long
		Default value: 2
 -vocab:                   vocab file
 -vocab-aliases:           vocab alias file
 -nonevents:               non-event vocabulary
 -limit-vocab:             limit count reading to specified vocabulary
 -write-vocab:             write vocab to file
 -write-vocab-index:       write vocab index map to file
 -write-text:              write input text to file (for validation)
 -memuse:                  show memory usage
 the default action is to write counts to stdout
 -help:                    Print this message

OK. From now on, you can start working on language model building with SRILM toolkit!
