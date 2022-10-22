# Khmer Spelling Checking with NMT Experiment-2

Previous experiment, I did with word level and for this time, I wanna try with sentence level.  

## Thinking for the Test Data

We already have manually collected spelling mistake data and I am considering to use that whole data as a test-set.  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ ls dataall*
dataall.normal  dataall.normal.clean  dataall.normal.parallel  dataall.parallel  dataall.txt
```

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ wc ./dataall.normal.clean
   7734   33250 3369917 ./dataall.normal.clean
```
   
```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ head ./dataall.normal.clean
<អញ្ចឹង>ក៏ថតគ្នាដែរគ្រាន់តែគ្នារកស៊ីមកពស់រស់មួយខ្លួន|||(អ៊ីចឹង/dia)ក៏ថតគ្នាដែរគ្រាន់តែគ្នារកស៊ីមកពស់រស់មួយខ្លួន
សម័យផ្តាច់សង្គរាមខ្មែរយើងរៀនអក្ខរកម្ម<នឹង>អក្សរ<បារាំ>|||សម័យផ្តាច់សង្គរាមខ្មែរយើងរៀនអក្ខរកម្ម(និង/vow)អក្សរ(បារាំង/typo)
ចង់មានបារាំងជួយ<ស្ទួច>ត្រីដូចលោកយាយដែរ|||ចង់មានបារាំងជួយ(ស្ទូច/vow)ត្រីដូចលោកយាយដែរ
<សំរាប់>ខ្ញុំវិញសុំឆ្លើយថាទេហើយ អ្នកណាថាប្រុសកំសាក<អី>ក៏ថាទៅ|||(សម្រាប់/cphotyp)ខ្ញុំវិញសុំឆ្លើយថាទេហើយ អ្នកណាថាប្រុសកំសាក(អ្វី/typo)ក៏ថាទៅ
បាតនឹងហើយបងជួយfollowed <នឹង>ស៊ែមួយផងបង|||បាតនឹងហើយបងជួយfollowed (និង/vow)ស៊ែមួយផងបង
ម្តាយដើម្បីកូនហានធ្វើគ្រប់យ៉ាងសុំ<សរសើ>|||ម្តាយដើម្បីកូនហានធ្វើគ្រប់យ៉ាងសុំ(សរសើរ/cons)
កូនមើលចុះ<មើប្បី>កូនចុះកូនៗវិញ|||កូនមើលចុះ(ដើម្បី/typo)កូនចុះកូនៗវិញ
ខ្ញុំវិញក៏ដូចជា<គាត><តែ>|||ខ្ញុំវិញក៏ដូចជា(គាត់/typo)(ដែរ/typo)
<មែន>ទេពស់ត្រី|||(មិនមែន/pho)ទេពស់ត្រី
ចំណាស់<ហឹង>ហើយទៅរកត្រី<ទឿត><អុំ>អើយ|||ចំណាស់(ហ្នឹង/typo)ហើយទៅរកត្រី(ទៀត/vow)(អ៊ុំ/typo)អើយ
```

## Thinking for the Training Data

Decided to use "all-train-data.line.shuf" file.  
Vichet and I used this file for Khmer word segmentation experiment at NICT.  

I replaced following symbols with NULL to become a normal Khmer sentences.  

- "_" symbol found 165124  
- "~" symbol found 42491
- "^" symbol found 4933  

And thus, after replacing ...  

```
តើ អ្នក ទទួល_យក ការ~ពាណិជ្ជ^កម្ម ជំនួយ ?  
តើ អ្នក ទទួលយក ការពាណិជ្ជកម្ម ជំនួយ ?  
```

## Thinking for the Closed Test Data

I plan to use the test data of the Khmer word segmentation experiment.  

## Preparing Training and Test Data for Sentence Level Spelling Checking 

I replaced symbols with NULL for Training Data  

- "_" 156201
- "~" 40039
- "^" 4653

I replaced following symbols with NULL for Test Data  

- "_" 8573
- "~" 2182
- "^" 238

## Data Information

After I uploaded to the Server, checked the datasize information ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell$ wc *
    5000    70465   986531 5000-test-data.line.shuf
   90000  1271438 17857860 90000-train-data.line.shuf
   95210  1345277 18889815 all-train-data.line-no-symbol
  190210  2687180 37734206 total
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell$
```

Copy manually collected spelling data ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/preprocessing$ cp dataall.normal.clean ../kh-segment/4khspell/
```

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ wc *
    5000    70465   986531 5000-test-data.line.shuf
   90000  1271438 17857860 90000-train-data.line.shuf
    7734    33250  3369917 dataall.normal.clean
  102734  1375153 22214308 total
```

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ head -n 3 *
==> 5000-test-data.line.shuf <==
អ្នក អាច បិទ កាតាប
លោកស្រី ឈាន អ៊ីញ
នេះ ជា បន្ទប់ បី សែសិប ប្រាំ

==> 90000-train-data.line.shuf <==
អ្នក អាច បិទ កាតាប
លោកស្រី ឈាន អ៊ីញ
នេះ ជា បន្ទប់ បី សែសិប ប្រាំ

==> dataall.normal.clean <==
<អញ្ចឹង>ក៏ថតគ្នាដែរគ្រាន់តែគ្នារកស៊ីមកពស់រស់មួយខ្លួន|||(អ៊ីចឹង/dia)ក៏ថតគ្នាដែរគ្រាន់តែគ្នារកស៊ីមកពស់រស់មួយខ្លួន
សម័យផ្តាច់សង្គរាមខ្មែរយើងរៀនអក្ខរកម្ម<នឹង>អក្សរ<បារាំ>|||សម័យផ្តាច់សង្គរាមខ្មែរយើងរៀនអក្ខរកម្ម(និង/vow)អក្សរ(បារាំង/typo)
ចង់មានបារាំងជួយ<ស្ទួច>ត្រីដូចលោកយាយដែរ|||ចង់មានបារាំងជួយ(ស្ទូច/vow)ត្រីដូចលោកយាយដែរ
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$
```

## Perl Script for Removing Brackets and Tags

I wrote a perl script for cleaning brackets (i.e. \(, \), \<, \>) and tags (e.g. /vow, /dia).  

```perl 
#!/usr/bin/env perl

# for cleaning (, ), <, > and spelling error type tags
# Written by Ye Kyaw Thu, Affiliate Professor, IDRI, CADT, Cambodia
# Preparation for Khmer Spelling Checking with NMT model experiment
# Input file format is as follows:
# <អញ្ចឹង>ក៏ថតគ្នាដែរគ្រាន់តែគ្នារកស៊ីមកពស់រស់មួយខ្លួន|||(អ៊ីចឹង/dia)ក៏ថតគ្នាដែរគ្រាន់តែគ្នារកស៊ីមកពស់រស់មួយខ្លួន
#សម័យផ្តាច់សង្គរាមខ្មែរយើងរៀនអក្ខរកម្ម<នឹង>អក្សរ<បារាំ>|||សម័យផ្តាច់សង្គរាមខ្មែរយើងរៀនអក្ខរកម្ម(និង/vow)អក្សរ(បារាំង/typo)
#ចង់មានបារាំងជួយ<ស្ទួច>ត្រីដូចលោកយាយដែរ|||ចង់មានបារាំងជួយ(ស្ទូច/vow)ត្រីដូចលោកយាយដែរ
#
# Last updated: 22 Oct 2022
# How to run:
# e.g. $ perl clean-brackets-tags.pl <input-file>

use strict;
#use warnings;
use utf8;
no warnings 'uninitialized';

binmode(STDIN, ":utf8");
binmode(STDOUT, ":utf8");
binmode(STDERR, ":utf8");

open (my $inputFILE,"<:encoding(utf8)", $ARGV[0]) or die "Couldn't open input file $ARGV[0]!, $!\n";

while (!eof($inputFILE)) {

    my $line = <$inputFILE>;
    if (($line ne '') & ($line !~ /^ *$/)) {
        chomp($line);
       (my $cleaned_line = $line) =~ s/\((.*?)\/.*?\)|\<(.*?)\>/$1/g;
       print "$line\n";
       print "$cleaned_line\n";
    }

}

close ($inputFILE);
```

## Test Run Perl Script

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ perl ./clean-brackets-tags.pl ./10lines.txt
<អញ្ចឹង>ក៏ថតគ្នាដែរគ្រាន់តែគ្នារកស៊ីមកពស់រស់មួយខ្លួន|||(អ៊ីចឹង/dia)ក៏ថតគ្នាដែរគ្រាន់តែគ្នារកស៊ីមកពស់រស់មួយខ្លួន
ក៏ថតគ្នាដែរគ្រាន់តែគ្នារកស៊ីមកពស់រស់មួយខ្លួន|||អ៊ីចឹងក៏ថតគ្នាដែរគ្រាន់តែគ្នារកស៊ីមកពស់រស់មួយខ្លួន
សម័យផ្តាច់សង្គរាមខ្មែរយើងរៀនអក្ខរកម្ម<នឹង>អក្សរ<បារាំ>|||សម័យផ្តាច់សង្គរាមខ្មែរយើងរៀនអក្ខរកម្ម(និង/vow)អក្សរ(បារាំង/typo)
សម័យផ្តាច់សង្គរាមខ្មែរយើងរៀនអក្ខរកម្មអក្សរ|||សម័យផ្តាច់សង្គរាមខ្មែរយើងរៀនអក្ខរកម្មនិងអក្សរបារាំង
ចង់មានបារាំងជួយ<ស្ទួច>ត្រីដូចលោកយាយដែរ|||ចង់មានបារាំងជួយ(ស្ទូច/vow)ត្រីដូចលោកយាយដែរ
ចង់មានបារាំងជួយត្រីដូចលោកយាយដែរ|||ចង់មានបារាំងជួយស្ទូចត្រីដូចលោកយាយដែរ
<សំរាប់>ខ្ញុំវិញសុំឆ្លើយថាទេហើយ អ្នកណាថាប្រុសកំសាក<អី>ក៏ថាទៅ|||(សម្រាប់/cphotyp)ខ្ញុំវិញសុំឆ្លើយថាទេហើយ អ្នកណាថាប្រុសកំសាក(អ្វី/typo)ក៏ថាទៅ
ខ្ញុំវិញសុំឆ្លើយថាទេហើយ អ្នកណាថាប្រុសកំសាកក៏ថាទៅ|||សម្រាប់ខ្ញុំវិញសុំឆ្លើយថាទេហើយ អ្នកណាថាប្រុសកំសាកអ្វីក៏ថាទៅ
បាតនឹងហើយបងជួយfollowed <នឹង>ស៊ែមួយផងបង|||បាតនឹងហើយបងជួយfollowed (និង/vow)ស៊ែមួយផងបង
បាតនឹងហើយបងជួយfollowed ស៊ែមួយផងបង|||បាតនឹងហើយបងជួយfollowed និងស៊ែមួយផងបង
ម្តាយដើម្បីកូនហានធ្វើគ្រប់យ៉ាងសុំ<សរសើ>|||ម្តាយដើម្បីកូនហានធ្វើគ្រប់យ៉ាងសុំ(សរសើរ/cons)
ម្តាយដើម្បីកូនហានធ្វើគ្រប់យ៉ាងសុំ|||ម្តាយដើម្បីកូនហានធ្វើគ្រប់យ៉ាងសុំសរសើរ
កូនមើលចុះ<មើប្បី>កូនចុះកូនៗវិញ|||កូនមើលចុះ(ដើម្បី/typo)កូនចុះកូនៗវិញ
កូនមើលចុះកូនចុះកូនៗវិញ|||កូនមើលចុះដើម្បីកូនចុះកូនៗវិញ
ខ្ញុំវិញក៏ដូចជា<គាត><តែ>|||ខ្ញុំវិញក៏ដូចជា(គាត់/typo)(ដែរ/typo)
ខ្ញុំវិញក៏ដូចជា|||ខ្ញុំវិញក៏ដូចជាគាត់ដែរ
<មែន>ទេពស់ត្រី|||(មិនមែន/pho)ទេពស់ត្រី
ទេពស់ត្រី|||មិនមែនទេពស់ត្រី
ចំណាស់<ហឹង>ហើយទៅរកត្រី<ទឿត><អុំ>អើយ|||ចំណាស់(ហ្នឹង/typo)ហើយទៅរកត្រី(ទៀត/vow)(អ៊ុំ/typo)អើយ
ចំណាស់ហើយទៅរកត្រីអើយ|||ចំណាស់ហ្នឹងហើយទៅរកត្រីទៀតអ៊ុំអើយ
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$
```
It looks work ...  

## Preprocessing

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ perl ./clean-brackets-tags.pl ./dataall.normal.clean > ./dataall.normal.clean.rm
```

Before removing tags and brackets ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ tail -n 3 ./dataall.normal.clean
តែ<ឈ្ងល់>អ្នកអត់គូរ ពេលដើរលេងបានអ្នកណាជូនទៅ ||| តែ(ឆ្ងល់/cons)អ្នកអត់គូរ ពេលដើរលេងបានអ្នកណាជូនទៅ
តើ<បុរស់>ៗសុទ្ធតែនិយាយចឹងទាំងអស់មែនទេ? ||| តើ(បុរស/vow)ៗសុទ្ធតែនិយាយចឹងទាំងអស់មែនទេ?
សូមអ្នកជំនាន់ក្រោយកុំយក<តំរាប់>តាមអី ||| សូមអ្នកជំនាន់ក្រោយកុំយក(តម្រាប់/pho)តាមអី
```

After removing ...   

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ tail -n 3 ./dataall.normal.clean.rm
តែអ្នកអត់គូរ ពេលដើរលេងបានអ្នកណាជូនទៅ ||| តែឆ្ងល់អ្នកអត់គូរ ពេលដើរលេងបានអ្នកណាជូនទៅ
តើៗសុទ្ធតែនិយាយចឹងទាំងអស់មែនទេ? ||| តើបុរសៗសុទ្ធតែនិយាយចឹងទាំងអស់មែនទេ?
សូមអ្នកជំនាន់ក្រោយកុំយកតាមអី ||| សូមអ្នកជំនាន់ក្រោយកុំយកតម្រាប់តាមអី
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$
```

```

```



