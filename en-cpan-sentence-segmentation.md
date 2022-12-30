# Testing CPAN English Sentence Segmentation Log

## Install Lingua::EN::Sentence Module

perl မှာက module တွေကို install လုပ်ဖို့ဆိုရင် CPAN ကို သုံးတယ်။  

```
(base) ye@ykt-pro:~/tmp$ cpan
Terminal does not support AddHistory.

cpan shell -- CPAN exploration and modules installation (v2.18)
Enter 'h' for help.

cpan[1]> install Lingua::EN::Sentence
Reading '/home/ye/.local/share/.cpan/Metadata'
  Database was generated on Fri, 27 Nov 2020 04:17:03 GMT
Fetching with LWP:
http://www.cpan.org/authors/01mailrc.txt.gz
Reading '/home/ye/.local/share/.cpan/sources/authors/01mailrc.txt.gz'
............................................................................DONE
Fetching with LWP:
http://www.cpan.org/modules/02packages.details.txt.gz
Reading '/home/ye/.local/share/.cpan/sources/modules/02packages.details.txt.gz'
  Database was generated on Fri, 30 Dec 2022 06:17:01 GMT
..............
  New CPAN.pm version (v2.34) available.
  [Currently running version is v2.18]
  You might want to try
    install CPAN
    reload cpan
  to both upgrade CPAN.pm and run the new version without leaving
  the current session.


..............................................................DONE
Fetching with LWP:
http://www.cpan.org/modules/03modlist.data.gz
Reading '/home/ye/.local/share/.cpan/sources/modules/03modlist.data.gz'
DONE
Writing /home/ye/.local/share/.cpan/Metadata
Running install for module 'Lingua::EN::Sentence'
Fetching with LWP:
http://www.cpan.org/authors/id/K/KI/KIMRYAN/Lingua-EN-Sentence-0.33.tar.gz
Fetching with LWP:
http://www.cpan.org/authors/id/K/KI/KIMRYAN/CHECKSUMS
Checksum for /home/ye/.local/share/.cpan/sources/authors/id/K/KI/KIMRYAN/Lingua-EN-Sentence-0.33.tar.gz ok
Scanning cache /home/ye/.local/share/.cpan/build for sizes
............................................................................DONE
'YAML' not installed, will not store persistent state
---- Unsatisfied dependencies detected during ----
----  KIMRYAN/Lingua-EN-Sentence-0.33.tar.gz  ----
    Module::Build [build_requires]
Running install for module 'Module::Build'
Fetching with LWP:
http://www.cpan.org/authors/id/L/LE/LEONT/Module-Build-0.4232.tar.gz
Fetching with LWP:
http://www.cpan.org/authors/id/L/LE/LEONT/CHECKSUMS
Checksum for /home/ye/.local/share/.cpan/sources/authors/id/L/LE/LEONT/Module-Build-0.4232.tar.gz ok
Configuring L/LE/LEONT/Module-Build-0.4232.tar.gz with Makefile.PL
# running Build.PL --installdirs site

Checking optional features...
inc_bundling_support....disabled
  requires:
    ! inc::latest is not installed

ERRORS/WARNINGS FOUND IN PREREQUISITES.  You may wish to install the versions
of the modules indicated above before proceeding with this installation

Created MYMETA.yml and MYMETA.json
Creating new 'Build' script for 'Module-Build' version '0.4232'
  LEONT/Module-Build-0.4232.tar.gz
  /usr/bin/perl Makefile.PL INSTALLDIRS=site -- OK
Running make for L/LE/LEONT/Module-Build-0.4232.tar.gz
/usr/bin/perl Build --makefile_env_macros 1
Building Module-Build
  LEONT/Module-Build-0.4232.tar.gz
  /usr/bin/make -- OK
Running make test
/usr/bin/perl Build --makefile_env_macros 1 test
t/00-compile.t ................. ok     
t/PL_files.t ................... ok   
t/actions/installdeps.t ........ ok   
t/actions/manifest_skip.t ...... ok   
t/add_property.t ............... ok     
t/add_property_array.t ......... ok   
t/add_property_hash.t .......... ok   
t/basic.t ...................... ok     
t/bundle_inc.t ................. skipped: $ENV{MB_TEST_EXPERIMENTAL} is not set
t/compat.t ..................... ok     
t/compat/exit.t ................ ok   
t/debug.t ...................... ok   
t/destinations.t ............... ok       
t/ext.t ........................ ok       
t/extend.t ..................... ok     
t/files.t ...................... ok   
t/help.t ....................... ok     
t/install.t .................... ok     
t/install_extra_target.t ....... ok   
t/manifypods.t ................. ok     
t/manifypods_with_utf8.t ....... ok   
t/metadata.t ................... ok     
t/metadata2.t .................. ok     
t/mymeta.t ..................... ok     
t/new_from_context.t ........... ok   
t/notes.t ...................... ok     
t/par.t ........................ skipped: PAR::Dist 0.17 or up not installed to check .par's.
t/parents.t .................... ok     
t/perl_mb_opt.t ................ ok   
t/pod_parser.t ................. ok     
t/ppm.t ........................ ok    
t/properties/dist_suffix.t ..... ok   
t/properties/license.t ......... ok   
t/properties/module_name.t ..... ok   
t/properties/needs_compiler.t .. ok     
t/properties/release_status.t .. ok    
t/properties/requires.t ........ ok   
t/properties/share_dir.t ....... ok     
t/resume.t ..................... ok   
t/runthrough.t ................. ok     
t/sample.t ..................... ok   
t/script_dist.t ................ ok   
t/signature.t .................. ok     
t/test_file_exts.t ............. ok   
t/test_reqs.t .................. ok   
t/test_type.t .................. ok   
t/test_types.t ................. ok     
t/tilde.t ...................... ok     
t/unit_run_test_harness.t ...... ok   
t/use_tap_harness.t ............ ok   
t/versions.t ................... ok   
t/write_default_maniskip.t ..... ok   
t/xs.t ......................... ok    
All tests successful.
Files=53, Tests=1167, 63 wallclock secs ( 0.33 usr  0.11 sys + 40.88 cusr 10.53 csys = 51.85 CPU)
Result: PASS
  LEONT/Module-Build-0.4232.tar.gz
  /usr/bin/make test -- OK
Running make install
/usr/bin/perl Build --makefile_env_macros 1 install
Building Module-Build
Installing /home/ye/perl5/man/man1/config_data.1p
Installing /home/ye/perl5/lib/perl5/Module/Build.pm
Installing /home/ye/perl5/lib/perl5/Module/Build/Config.pm
Installing /home/ye/perl5/lib/perl5/Module/Build/ConfigData.pm
Installing /home/ye/perl5/lib/perl5/Module/Build/Authoring.pod
Installing /home/ye/perl5/lib/perl5/Module/Build/Compat.pm
Installing /home/ye/perl5/lib/perl5/Module/Build/Base.pm
Installing /home/ye/perl5/lib/perl5/Module/Build/Dumper.pm
Installing /home/ye/perl5/lib/perl5/Module/Build/Cookbook.pm
Installing /home/ye/perl5/lib/perl5/Module/Build/Bundling.pod
Installing /home/ye/perl5/lib/perl5/Module/Build/PPMMaker.pm
Installing /home/ye/perl5/lib/perl5/Module/Build/API.pod
Installing /home/ye/perl5/lib/perl5/Module/Build/PodParser.pm
Installing /home/ye/perl5/lib/perl5/Module/Build/Notes.pm
Installing /home/ye/perl5/lib/perl5/Module/Build/Platform/Windows.pm
Installing /home/ye/perl5/lib/perl5/Module/Build/Platform/aix.pm
Installing /home/ye/perl5/lib/perl5/Module/Build/Platform/darwin.pm
Installing /home/ye/perl5/lib/perl5/Module/Build/Platform/VMS.pm
Installing /home/ye/perl5/lib/perl5/Module/Build/Platform/cygwin.pm
Installing /home/ye/perl5/lib/perl5/Module/Build/Platform/Unix.pm
Installing /home/ye/perl5/lib/perl5/Module/Build/Platform/MacOS.pm
Installing /home/ye/perl5/lib/perl5/Module/Build/Platform/VOS.pm
Installing /home/ye/perl5/lib/perl5/Module/Build/Platform/Default.pm
Installing /home/ye/perl5/lib/perl5/Module/Build/Platform/os2.pm
Installing /home/ye/perl5/man/man3/Module::Build::Platform::aix.3pm
Installing /home/ye/perl5/man/man3/Module::Build::PPMMaker.3pm
Installing /home/ye/perl5/man/man3/Module::Build::API.3pm
Installing /home/ye/perl5/man/man3/Module::Build::Platform::MacOS.3pm
Installing /home/ye/perl5/man/man3/Module::Build::Authoring.3pm
Installing /home/ye/perl5/man/man3/Module::Build::Platform::Windows.3pm
Installing /home/ye/perl5/man/man3/Module::Build::Platform::VMS.3pm
Installing /home/ye/perl5/man/man3/Module::Build::Base.3pm
Installing /home/ye/perl5/man/man3/Module::Build::ConfigData.3pm
Installing /home/ye/perl5/man/man3/Module::Build::Cookbook.3pm
Installing /home/ye/perl5/man/man3/Module::Build::Compat.3pm
Installing /home/ye/perl5/man/man3/Module::Build::Notes.3pm
Installing /home/ye/perl5/man/man3/Module::Build::Platform::darwin.3pm
Installing /home/ye/perl5/man/man3/Module::Build::Platform::os2.3pm
Installing /home/ye/perl5/man/man3/Module::Build::Platform::VOS.3pm
Installing /home/ye/perl5/man/man3/Module::Build::Platform::Unix.3pm
Installing /home/ye/perl5/man/man3/Module::Build.3pm
Installing /home/ye/perl5/man/man3/Module::Build::Bundling.3pm
Installing /home/ye/perl5/man/man3/Module::Build::Platform::cygwin.3pm
Installing /home/ye/perl5/man/man3/Module::Build::Platform::Default.3pm
Installing /home/ye/perl5/bin/config_data
  LEONT/Module-Build-0.4232.tar.gz
  /usr/bin/make install  -- OK
  KIMRYAN/Lingua-EN-Sentence-0.33.tar.gz
  Has already been unwrapped into directory /home/ye/.local/share/.cpan/build/Lingua-EN-Sentence-0.33-0
Configuring K/KI/KIMRYAN/Lingua-EN-Sentence-0.33.tar.gz with Build.PL
Created MYMETA.yml and MYMETA.json
Creating new 'Build' script for 'Lingua-EN-Sentence' version '0.33'
  KIMRYAN/Lingua-EN-Sentence-0.33.tar.gz
  /usr/bin/perl Build.PL --installdirs site -- OK
Running Build for K/KI/KIMRYAN/Lingua-EN-Sentence-0.33.tar.gz
Building Lingua-EN-Sentence
  KIMRYAN/Lingua-EN-Sentence-0.33.tar.gz
  ./Build -- OK
Running Build test
t/main.t .. ok   
All tests successful.
Files=1, Tests=3,  0 wallclock secs ( 0.02 usr  0.01 sys +  0.07 cusr  0.01 csys =  0.11 CPU)
Result: PASS
  KIMRYAN/Lingua-EN-Sentence-0.33.tar.gz
  ./Build test -- OK
Running Build install
Building Lingua-EN-Sentence
Installing /home/ye/perl5/lib/perl5/Lingua/EN/Sentence.pm
Installing /home/ye/perl5/man/man3/Lingua::EN::Sentence.3pm
  KIMRYAN/Lingua-EN-Sentence-0.33.tar.gz
  ./Build install  -- OK

cpan[2]> 
```

## Test Run

I copy/paste the following programs from the CPAN library website ([https://metacpan.org/pod/Lingua::EN::Sentence](https://metacpan.org/pod/Lingua::EN::Sentence)).  

```perl 
use Lingua::EN::Sentence qw( get_sentences add_acronyms );
 
add_acronyms('lt','gen');               ## adding support for 'Lt. Gen.'
my $text = q{
A sentence usually ends with a dot, exclamation or question mark optionally followed by a space!
A string followed by 2 carriage returns denotes a sentence, even though it doesn't end in a dot
 
Dots after single letters such as U.S.A. or in numbers like -12.34 will not cause a split
as well as common abbreviations such as Dr. I. Smith, Ms. A.B. Jones, Apr. Calif. Esq.
and (some text) ellipsis such as ... or . . are ignored.
Some valid cases canot be deteected, such as the answer is X. It cannot easily be
differentiated from the single letter-dot sequence to abbreviate a person's given name.
Numbered points within a sentence will not cause a split 1. Like this one.
See the code for all the rules that apply.
This string has 7 sentences.
};
 
my $sentences=get_sentences($text);     # Get the sentences.
foreach my $sent (@$sentences)
{
        $i++;
        print("SENTENCE $i:$sent\n");
}
```

Run above program and the output is as follows:  

```
(base) ye@ykt-pro:~/tmp$ perl split-eg.pl 
SENTENCE 1:A sentence usually ends with a dot, exclamation or question mark optionally followed by a space!
SENTENCE 2:A string followed by 2 carriage returns denotes a sentence, even though it doesn't end in a dot
SENTENCE 3:Dots after single letters such as U.S.A. or in numbers like -12.34 will not cause a split
as well as common abbreviations such as Dr. I. Smith, Ms. A.B. Jones, Apr. Calif. Esq.
and (some text) ellipsis such as ... or . . are ignored.
SENTENCE 4:Some valid cases canot be deteected, such as the answer is X. It cannot easily be
differentiated from the single letter-dot sequence to abbreviate a person's given name.
SENTENCE 5:Numbered points within a sentence will not cause a split 1. Like this one.
SENTENCE 6:See the code for all the rules that apply.
SENTENCE 7:This string has 7 sentences.
(base) ye@ykt-pro:~/tmp$ 
```

## Test Run 2

I update/wrote a perl program based on the above example as follows:  

```perl
#!/usr/bin/env perl

# English sentence splitting program with Lingua::EN::Sentence Perl Module
# Ye Kyaw Thu, 
# Visiting Professor, LST, NECTEC, Thailand
# Ref: https://www.perl.com/article/21/2013/4/21/Read-an-entire-file-into-a-string/
#
# Demo program for my undergrad student Thura Aung.
# e.g. $ perl eng-sentence-split.pl <input-file>

use Lingua::EN::Sentence qw( get_sentences add_acronyms );
add_acronyms('lt','gen');               ## adding support for 'Lt. Gen.'

use strict;
use warnings;
use utf8;

binmode(STDIN, ":utf8");
binmode(STDOUT, ":utf8");
binmode(STDERR, ":utf8");

open (my $inputFILE,"<:encoding(utf8)", $ARGV[0]) or die "Couldn't open input file $ARGV[0]!, $!\n";

# Slurping: read an entire file into a string
my $file_content = do { local $/; <$inputFILE> };
close ($inputFILE);
 
my $sentences=get_sentences($file_content);     # Get the sentences.
foreach my $sent (@$sentences)
{
        print("$sent\n");
}

```

Prepared the English text file (i.e. the one shown in the 1st example program) ...  
For this time, I concatinated all sentences as one line.  

```
(base) ye@ykt-pro:~/tmp$ cat ./7sentences.txt 
A sentence usually ends with a dot, exclamation or question mark optionally followed by a space! A string followed by 2 carriage returns denotes a sentence, even though it doesn't end in a dot Dots after single letters such as U.S.A. or in numbers like -12.34 will not cause a split as well as common abbreviations such as Dr. I. Smith, Ms. A.B. Jones, Apr. Calif. Esq. and (some text) ellipsis such as ... or . . are ignored. Some valid cases canot be deteected, such as the answer is X. It cannot easily be differentiated from the single letter-dot sequence to abbreviate a person's given name. Numbered points within a sentence will not cause a split 1. Like this one. See the code for all the rules that apply. This string has 7 sentences.
(base) ye@ykt-pro:~/tmp$ 
```

Test run with the updated perl script and for this time, I got 6 lines in total:  

```
(base) ye@ykt-pro:~/tmp$ perl ./eng-sentence-split.pl ./7sentences.txt | cat -n
     1	A sentence usually ends with a dot, exclamation or question mark optionally followed by a space!
     2	A string followed by 2 carriage returns denotes a sentence, even though it doesn't end in a dot Dots after single letters such as U.S.A. or in numbers like -12.34 will not cause a split as well as common abbreviations such as Dr. I. Smith, Ms. A.B. Jones, Apr. Calif. Esq. and (some text) ellipsis such as ... or . . are ignored.
     3	Some valid cases canot be deteected, such as the answer is X. It cannot easily be differentiated from the single letter-dot sequence to abbreviate a person's given name.
     4	Numbered points within a sentence will not cause a split 1. Like this one.
     5	See the code for all the rules that apply.
     6	This string has 7 sentences.
(base) ye@ykt-pro:~/tmp$
```

## Test Run 3  

For this time, I wanna try with different English text sentences and I used the abstract of Thura Aung paper (draft version) ...  

```
In recent years, text segmentation for the Myanmar language has been widely studied in the field of natural language processing (NLP). Myanmar word segmentation is an essential basis of preprocessing step for NLP tasks. There are several studies on Myanmar word segmentation. Most text segmentation problems have been approached as sequence tagging task. In this study, we approached Myanmar sentence segmentation not only from machine learning based sequence tagging but also from machine translation approach. Supervised machine learning algorithms namely Conditional Random Fields (CRFs), Hidden Markov Model (HMM), Ripple Down Rules based (RDR) and neural Machine Translation (NMT) models with Sequence-to-Sequence and Transformer architectures were used for conducting the experiments. We trained the models either on training data that includes only sentence-level data or on training data that contains both sentence-level and paragraph-level data. \textit{Machine Learning based sequence tagging} models were used as baseline models compared to \textit{neural machine translation} approach. Two different types of test data, i.e., one with only sentence-level data and the other with both sentence-level and paragraph-level data, were also used to evaluate our proposed models. The accuracies were measured in terms of Bilingual Evaluation Understudy (BLEU) and character n-gram F-score (chrF++) scores. Word Error Rate (WER) is also used to find the error rate. The experimental results show that Neural Machine Translation approach with the sequence-to-sequence architecture trained on both sentence-level and paragraph-level data achieved better BLEU and chrF++ scores than other models.
```

Sentence segmentation with cpan library is as follows:  

```
(base) ye@ykt-pro:~/tmp$ perl ./eng-sentence-split.pl ./abstract-draft.txt | cat -n
     1	In recent years, text segmentation for the Myanmar language has been widely studied in the field of natural language processing (NLP).
     2	Myanmar word segmentation is an essential basis of preprocessing step for NLP tasks.
     3	There are several studies on Myanmar word segmentation.
     4	Most text segmentation problems have been approached as sequence tagging task.
     5	In this study, we approached Myanmar sentence segmentation not only from machine learning based sequence tagging but also from machine translation approach.
     6	Supervised machine learning algorithms namely Conditional Random Fields (CRFs), Hidden Markov Model (HMM), Ripple Down Rules based (RDR) and neural Machine Translation (NMT) models with Sequence-to-Sequence and Transformer architectures were used for conducting the experiments.
     7	We trained the models either on training data that includes only sentence-level data or on training data that contains both sentence-level and paragraph-level data.
     8	\textit{Machine Learning based sequence tagging} models were used as baseline models compared to \textit{neural machine translation} approach.
     9	Two different types of test data, i.e., one with only sentence-level data and the other with both sentence-level and paragraph-level data, were also used to evaluate our proposed models.
    10	The accuracies were measured in terms of Bilingual Evaluation Understudy (BLEU) and character n-gram F-score (chrF++) scores.
    11	Word Error Rate (WER) is also used to find the error rate.
    12	The experimental results show that Neural Machine Translation approach with the sequence-to-sequence architecture trained on both sentence-level and paragraph-level data achieved better BLEU and chrF++ scores than other models.
(base) ye@ykt-pro:~/tmp$
```

Not so bad ...  

## Check the Module 

အရင်ဆုံး pm ဖိုင် သို့မဟုတ် module ဖိုင်ရှိတဲ့ path ကို cpan command နဲ့ ရှာကြည့်ခဲ့ ...  

```
(base) ye@ykt-pro:~/tmp$ cpan -D Lingua::EN::Sentence
CPAN: Storable loaded ok (v2.62)
Reading '/home/ye/.local/share/.cpan/Metadata'
  Database was generated on Fri, 30 Dec 2022 06:17:01 GMT
Lingua::EN::Sentence
-------------------------------------------------------------------------
	CPAN: Module::CoreList loaded ok (v5.20170922_26)
(no description)
	K/KI/KIMRYAN/Lingua-EN-Sentence-0.33.tar.gz
	/home/ye/perl5/lib/perl5/Lingua/EN/Sentence.pm
	Installed: 0.33
	CPAN:      0.33  up to date
	Kim Ryan (KIMRYAN)
	kimryan nospam@cpan.org

(base) ye@ykt-pro:~/tmp$
```

check the code inside:  

```perl
...
...
our $EOS = "\001"; #"__EOS__";
our $EOA = '__EOA__';

our $P = q/[\.!?]/;			    # PUNCTUATION

$AP =  q/(?:'|"|\?|\)|\]|\})?/;	# AFTER PUNCTUATION
our $PAP = $P.$AP;

# ACRONYMS AND ABBREVIATIONS
my @PEOPLE = qw( Mr Mrs Ms Dr Prof Mme Ms?gr Sens? Reps? Gov Attys? Supt Insp Const Det Revd? Ald Rt Hon);
my @TITLE_SUFFIXES = qw(PhD Jn?r Sn?r Esq MD LLB);
my @MILITARY = qw( Col Gen Lt Cm?dr Adm Capt Sgt Cpl Maj Pte);
my @INSTITUTES = qw( Dept Univ Assn Bros);
my @COMPANIES = qw( Inc Pty Ltd Co Corp);
my @PLACES =
qw(
	Arc Al Ave Blv?d Cl Ct Cres Dr Expy? Fw?y Hwa?y La Pde? Pl Plz Rd St Tce 
	dist mt km in ft 	
	Ala  Ariz Ark Cal Calif Col Colo Conn Del Fed  Fla Ga Ida Id Ill Ind Ia Kan Kans Ken Ky
	La Me Md Is Mass Mich Minn Miss Mo Mont Neb Nebr Nev Mex Okla Ok Ore Penna Penn Pa Dak 
	Tenn Tex Ut Vt Va Wash Wis Wisc Wy Wyo USAFA Alta Man Ont Qu? Sask Yuk
	Aust Vic Qld Tas
);
my @MONTHS = qw(Jan Feb Mar Apr May Jun Jul Aug Sept? Oct Nov Dec);
my @MISC = qw(no esp est);  # Established
my @LATIN = qw(vs etc al ibid sic);
my @MATH = qw(fig eq sec cf Thm Def Conj resp);

our @ABBREVIATIONS = (@PEOPLE, @TITLE_SUFFIXES, @MILITARY, @INSTITUTES, @COMPANIES, @PLACES, @MONTHS, @MISC,@LATIN, @MATH);
```

check the splitting function ...  

```perl
#------------------------------------------------------------------------------
# get_sentences - takes text input and splits it into sentences.
# A regular expression viciously cuts the text into sentences, 
# and then a list of rules (some of them consist of a list of abbreviations)
# are applied on the marked text in order to fix end-of-sentence markings in 
# places which are not indeed end-of-sentence.
#------------------------------------------------------------------------------
sub get_sentences {
	my ($text) = @_;
	return [] unless defined $text;
	$VERBOSE and print("ORIGINAL\n$text\n");
	
	$text = mark_up_abbreviations($text);
	$VERBOSE and print("mark_up_abbreviations\n$text\n");
	
	$text = first_sentence_breaking($text);
	$VERBOSE and print("first_sentence_breaking\n$text\n");
	
	$text = remove_false_end_of_sentence($text);
	$VERBOSE and print("remove_false_end_of_sentence\n$text\n");
	
	$text = split_unsplit_stuff($text);
	$VERBOSE and print("split_unsplit_stuff\n$text\n");
	
	my @sentences = split(/$EOS/,$text);
	my $cleaned_sentences = clean_sentences(\@sentences);
	if ($VERBOSE) {
		my $i;
		foreach my $sent (@$cleaned_sentences) {
			$i++;
			print("SENTENCE $i >>>$sent<<<\n");
		}
	}
	return $cleaned_sentences;
}
```

ပထမဆုံး example program မှာလည်း ပါသလိုပဲ User က အတိုကောက် စာလုံးတွေကို အသစ်ထပ်ထည့်ဖို့လည်း ခွင့်ပြုထားတယ် ... 

```
#------------------------------------------------------------------------------
# add_acronyms - user can add a list of acronyms/abbreviations.
#------------------------------------------------------------------------------
sub add_acronyms {
	push @ABBREVIATIONS, @_;
}

#------------------------------------------------------------------------------
# get_acronyms - get list of defined acronyms.
#------------------------------------------------------------------------------
sub get_acronyms {
	return @ABBREVIATIONS;
}

#------------------------------------------------------------------------------
# set_acronyms - replace the predefined acronyms list with your own list.
#------------------------------------------------------------------------------
sub set_acronyms {
	@ABBREVIATIONS=@_;
}
```

## Reference

1. https://metacpan.org/release/KIMRYAN/Lingua-EN-Sentence-0.29/view/lib/Lingua/EN/Sentence.pm
2. https://metacpan.org/pod/Lingua::EN::Sentence
3. https://www.perl.com/article/21/2013/4/21/Read-an-entire-file-into-a-string/

