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

## Split into 2 Columns

We need to split manually collected data into two files. I wrote a perl script as follows:  

```perl 
#!/usr/bin/env perl

# Split column1, column2 and write into two output files
# Ye Kyaw Thu, IDRI, CADT, Cambodia
#
# Last updated: 22 Oct 2022
# Preparation for 4th NLP/AI Workshop 2022
# e.g. $ perl split-col1-col2.pl <input-file> <column1-output-file> <column2-output-file2>

use strict;
use warnings;
use utf8;

binmode(STDIN, ":utf8");
binmode(STDOUT, ":utf8");
binmode(STDERR, ":utf8");

open (my $inputFILE,"<:encoding(utf8)", $ARGV[0]) or die "Couldn't open input file $ARGV[0]!, $!\n";
open (my $outputFILE1,">:encoding(utf8)", $ARGV[1]) or die "Couldn't open input file $ARGV[1]!, $!\n";
open (my $outputFILE2,">:encoding(utf8)", $ARGV[2]) or die "Couldn't open input file $ARGV[2]!, $!\n";

while (!eof($inputFILE)) {

    my $line = <$inputFILE>;
    if (($line ne '') & ($line !~ /^ *$/)) {
        chomp($line);
        my ($col1, $col2) = split(/\|\|\|/, $line);
        print $outputFILE1 "$col1\n";
        print $outputFILE2 "$col2\n";
    }

}

close ($inputFILE);
close ($outputFILE1);
close ($outputFILE2);
```

Prepare a small test file:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ cat 10-clean.txt
ក៏ថតគ្នាដែរគ្រាន់តែគ្នារកស៊ីមកពស់រស់មួយខ្លួន|||អ៊ីចឹងក៏ថតគ្នាដែរគ្រាន់តែគ្នារកស៊ីមកពស់រស់មួយខ្លួន
សម័យផ្តាច់សង្គរាមខ្មែរយើងរៀនអក្ខរកម្មអក្សរ|||សម័យផ្តាច់សង្គរាមខ្មែរយើងរៀនអក្ខរកម្មនិងអក្សរបារាំង
ចង់មានបារាំងជួយត្រីដូចលោកយាយដែរ|||ចង់មានបារាំងជួយស្ទូចត្រីដូចលោកយាយដែរ
ខ្ញុំវិញសុំឆ្លើយថាទេហើយ អ្នកណាថាប្រុសកំសាកក៏ថាទៅ|||សម្រាប់ខ្ញុំវិញសុំឆ្លើយថាទេហើយ អ្នកណាថាប្រុសកំសាកអ្វីក៏ថាទៅ
បាតនឹងហើយបងជួយfollowed ស៊ែមួយផងបង|||បាតនឹងហើយបងជួយfollowed និងស៊ែមួយផងបង
ម្តាយដើម្បីកូនហានធ្វើគ្រប់យ៉ាងសុំ|||ម្តាយដើម្បីកូនហានធ្វើគ្រប់យ៉ាងសុំសរសើរ
កូនមើលចុះកូនចុះកូនៗវិញ|||កូនមើលចុះដើម្បីកូនចុះកូនៗវិញ
ខ្ញុំវិញក៏ដូចជា|||ខ្ញុំវិញក៏ដូចជាគាត់ដែរ
ទេពស់ត្រី|||មិនមែនទេពស់ត្រី
ចំណាស់ហើយទៅរកត្រីអើយ|||ចំណាស់ហ្នឹងហើយទៅរកត្រីទៀតអ៊ុំអើយ
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$
```

Test run ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ perl ./split-col1-col2.pl ./10-clean.txt col1 col2
```

Checked the output files and it looks OK ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ cat col1
ក៏ថតគ្នាដែរគ្រាន់តែគ្នារកស៊ីមកពស់រស់មួយខ្លួន
សម័យផ្តាច់សង្គរាមខ្មែរយើងរៀនអក្ខរកម្មអក្សរ
ចង់មានបារាំងជួយត្រីដូចលោកយាយដែរ
ខ្ញុំវិញសុំឆ្លើយថាទេហើយ អ្នកណាថាប្រុសកំសាកក៏ថាទៅ
បាតនឹងហើយបងជួយfollowed ស៊ែមួយផងបង
ម្តាយដើម្បីកូនហានធ្វើគ្រប់យ៉ាងសុំ
កូនមើលចុះកូនចុះកូនៗវិញ
ខ្ញុំវិញក៏ដូចជា
ទេពស់ត្រី
ចំណាស់ហើយទៅរកត្រីអើយ
```

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ cat col2
អ៊ីចឹងក៏ថតគ្នាដែរគ្រាន់តែគ្នារកស៊ីមកពស់រស់មួយខ្លួន
សម័យផ្តាច់សង្គរាមខ្មែរយើងរៀនអក្ខរកម្មនិងអក្សរបារាំង
ចង់មានបារាំងជួយស្ទូចត្រីដូចលោកយាយដែរ
សម្រាប់ខ្ញុំវិញសុំឆ្លើយថាទេហើយ អ្នកណាថាប្រុសកំសាកអ្វីក៏ថាទៅ
បាតនឹងហើយបងជួយfollowed និងស៊ែមួយផងបង
ម្តាយដើម្បីកូនហានធ្វើគ្រប់យ៉ាងសុំសរសើរ
កូនមើលចុះដើម្បីកូនចុះកូនៗវិញ
ខ្ញុំវិញក៏ដូចជាគាត់ដែរ
មិនមែនទេពស់ត្រី
ចំណាស់ហ្នឹងហើយទៅរកត្រីទៀតអ៊ុំអើយ
```

Split the whole file of manually prepared data:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ perl ./split-col1-col2.pl ./dataall.normal.clean.rm col1 col2
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ wc dataall.normal.clean.rm col1 col2
   7734   32952 2968174 dataall.normal.clean.rm
   7734   17558 1339555 col1
   7734   17957 1607162 col2
  23202   68467 5914891 total
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$
```

Check the col1 file:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ tail ./col1
ប្រជាពលរដ្ឋទៅមើលតំបន់បំផ្លាញក្នុងតាមដានការពារ
តែគាត់ទៅគាត់និយាយមិនដែលការពិតទេ​
អរគុណ សន្តិភាព
បដិសេដថាគ្មានរឿងកើតឡើងដូចចោទប្រកាន់ពីប្រជាពលរដ្ឋ
ពេលខ្លះចាប់បានទាំងនៅជាថានេះជាជនក្លែងបន្លំ
បាត់មុខៗមេសផុសរាល់ថ្ងៃមកបងខ្ញុំចាំ
មិចមកងងុយតែដេកចឹង
តែអ្នកអត់គូរ ពេលដើរលេងបានអ្នកណាជូនទៅ
តើៗសុទ្ធតែនិយាយចឹងទាំងអស់មែនទេ?
សូមអ្នកជំនាន់ក្រោយកុំយកតាមអី
```

Check the col2 file:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ tail ./col2
 ប្រជាពលរដ្ឋទៅមើលតំបន់បំផ្លាញក្នុងបំណងតាមដានការពារ
 ជឿតែគាត់ទៅគាត់និយាយមិនដែលការពិតទេ
 អរគុណបិតា សន្តិភាព
 បដិសេដថាគ្មានរឿងកើតឡើងដូចការចោទប្រកាន់ពីប្រជាពលរដ្ឋ
 ពេលខ្លះចាប់បានទាំងនៅឯកសណ្ឋានបែរជាថាបុគ្គលនេះជាជនក្លែងបន្លំ
 បាត់មុខយូរៗមេសផុសរាល់ថ្ងៃមកបងខ្ញុំចាំ
 មិចមករៀនងងុយតែដេកចឹង
 តែឆ្ងល់អ្នកអត់គូរ ពេលដើរលេងបានអ្នកណាជូនទៅ
 តើបុរសៗសុទ្ធតែនិយាយចឹងទាំងអស់មែនទេ?
 សូមអ្នកជំនាន់ក្រោយកុំយកតម្រាប់តាមអី
```

For the error analysis with spelling error type, I keep with the original sentences...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ perl ./split-col1-col2.pl ./dataall.normal.clean col3 col4
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ wc dataall.normal.clean col3 col4
   7734   33250 3369917 dataall.normal.clean
   7734   17885 1614672 col3
   7734   17959 1733256 col4
  23202   69094 6717845 total
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$
```

paste col1, col2, col3 and col4 as one file...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ paste col1 col2 col3 col4 > dataall.normal.clean.4columns
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ head dataall.normal.clean.4columns
ក៏ថតគ្នាដែរគ្រាន់តែគ្នារកស៊ីមកពស់រស់មួយខ្លួន    អ៊ីចឹងក៏ថតគ្នាដែរគ្រាន់តែគ្នារកស៊ីមកពស់រស់មួយខ្លួន      <អញ្ចឹង>ក៏ថតគ្នាដែរគ្រាន់តែគ្នារកស៊ីមកពស់រស់មួយខ្លួន  (អ៊ីចឹង/dia)ក៏ថតគ្នាដែរគ្រាន់តែគ្នារកស៊ីមកពស់រស់មួយខ្លួន
សម័យផ្តាច់សង្គរាមខ្មែរយើងរៀនអក្ខរកម្មអក្សរ      សម័យផ្តាច់សង្គរាមខ្មែរយើងរៀនអក្ខរកម្មនិងអក្សរបារាំង     សម័យផ្តាច់សង្គរាមខ្មែរយើងរៀនអក្ខរកម្ម<នឹង>អក្សរ<បារាំ>        សម័យផ្តាច់សង្គរាមខ្មែរយើងរៀនអក្ខរកម្ម(និង/vow)អក្សរ(បារាំង/typo)
ចង់មានបារាំងជួយត្រីដូចលោកយាយដែរ ចង់មានបារាំងជួយស្ទូចត្រីដូចលោកយាយដែរ    ចង់មានបារាំងជួយ<ស្ទួច>ត្រីដូចលោកយាយដែរ  ចង់មានបារាំងជួយ(ស្ទូច/vow)ត្រីដូចលោកយាយដែរ
ខ្ញុំវិញសុំឆ្លើយថាទេហើយ អ្នកណាថាប្រុសកំសាកក៏ថាទៅ        សម្រាប់ខ្ញុំវិញសុំឆ្លើយថាទេហើយ អ្នកណាថាប្រុសកំសាកអ្វីក៏ថាទៅ  <សំរាប់>ខ្ញុំវិញសុំឆ្លើយថាទេហើយ អ្នកណាថាប្រុសកំសាក<អី>ក៏ថាទៅ     (សម្រាប់/cphotyp)ខ្ញុំវិញសុំឆ្លើយថាទេហើយ អ្នកណាថាប្រុសកំសាក(អ្វី/typo)ក៏ថាទៅ
បាតនឹងហើយបងជួយfollowed ស៊ែមួយផងបង       បាតនឹងហើយបងជួយfollowed និងស៊ែមួយផងបង    បាតនឹងហើយបងជួយfollowed <នឹង>ស៊ែមួយផងបងបាតនឹងហើយបងជួយfollowed (និង/vow)ស៊ែមួយផងបង
ម្តាយដើម្បីកូនហានធ្វើគ្រប់យ៉ាងសុំ       ម្តាយដើម្បីកូនហានធ្វើគ្រប់យ៉ាងសុំសរសើរ  ម្តាយដើម្បីកូនហានធ្វើគ្រប់យ៉ាងសុំ<សរសើ>       ម្តាយដើម្បីកូនហានធ្វើគ្រប់យ៉ាងសុំ(សរសើរ/cons)
កូនមើលចុះកូនចុះកូនៗវិញ  កូនមើលចុះដើម្បីកូនចុះកូនៗវិញ    កូនមើលចុះ<មើប្បី>កូនចុះកូនៗវិញ  កូនមើលចុះ(ដើម្បី/typo)កូនចុះកូនៗវិញ
ខ្ញុំវិញក៏ដូចជា ខ្ញុំវិញក៏ដូចជាគាត់ដែរ  ខ្ញុំវិញក៏ដូចជា<គាត><តែ>        ខ្ញុំវិញក៏ដូចជា(គាត់/typo)(ដែរ/typo)
ទេពស់ត្រី       មិនមែនទេពស់ត្រី <មែន>ទេពស់ត្រី  (មិនមែន/pho)ទេពស់ត្រី
ចំណាស់ហើយទៅរកត្រីអើយ    ចំណាស់ហ្នឹងហើយទៅរកត្រីទៀតអ៊ុំអើយ        ចំណាស់<ហឹង>ហើយទៅរកត្រី<ទឿត><អុំ>អើយ     ចំណាស់(ហ្នឹង/typo)ហើយទៅរកត្រី(ទៀត/vow)(អ៊ុំ/typo)អើយ
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$
```

## Prepare Training/Valid/Test Dataset

First I prepared test set from manually collected spelling error data:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ cp col1 ./data-sent/manual/test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ cp col2 ./data-sent/manual/test.cr
```

Make edit-1 error simulation for edit-1 test data from the word segmented test-data ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ python3 ./make-edit-error.py ./5000-test-data.l
ine.shuf 1 > ./data-sent/edit1/test.er
```

Make edit-2 error simulation for edit-2 test data from word segmented test-data ...  
```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ python3 ./make-edit-error.py ./5000-test-data.line.shuf 2 > ./data-sent/edit2/test.er
```

Prepare target files for edit1 and edit2, from the word segmented test data ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ cp 5000-test-data.line.shuf ./data-sent/edit1/test.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ cp 5000-test-data.line.shuf ./data-sent/edit2/t
est.cr
```

Prepareing Training data-set for NMT model building ...  
for edit-distance 1:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ time python3 ./make-edit-error.py ./90000-train
-data.line.shuf 1 > ./data-sent/edit1/train.er

real    0m2.858s
user    0m2.635s
sys     0m0.028s
```

for edit-distance 2:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ time python3 ./make-edit-error.py ./90000-train-data.line.shuf 2 > ./data-sent/edit2/train.er

real    7m34.801s
user    7m1.377s
sys     0m33.351s
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$
```

Preparing Training data for edit1 and edit2, the same ...   
I hope you can follow the process ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ cp ./90000-train-data.line.shuf ./data-sent/edit1/train.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ cp ./90000-train-data.line.shuf ./data-sent/edit2/train.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$
```

Let's see once on current folder and file structure ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$ tree ./data-sent/
./data-sent/
├── edit1
│   ├── test.cr
│   ├── test.er
│   ├── train.cr
│   └── train.er
├── edit2
│   ├── test.cr
│   ├── test.er
│   ├── train.cr
│   └── train.er
└── manual
    ├── test.cr
    └── test.er

3 directories, 10 files
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing$
```

The experimental setting is NMT model will be train with edit-1 error only and edit-2 error only.   
Testing will be done with two test-sets. They are edit-x test-set and manual test-set.  
   
## Normalization

Note: We have to do normalization ...  (i.e adjusting typing order and other errors based on the Unicode Rules)  


Normalization for word level edit-1 data:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1$ mkdir normalized
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1$ ls
normalized  test.cr  test.er  train.cr  train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1$ python3 ../../khnormal2.py test.cr ./normalized/test.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1$ python3 ../../khnormal2.py test.er ./normalized/test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1$ python3 ../../khnormal2.py train.cr ./normalized/train.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1$ python3 ../../khnormal2.py train.er ./normalized/train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1$
```

Normalization for word level edit-2 data:
```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ ls
test.cr  test.er  train.cr  train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ mkdir normalized
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ python3 ../../khnormal2.py test.cr ./normalized/test.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ python3 ../../khnormal2.py test.er ./normalized/test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ cp ../edit1/normalized/train.cr ./normalized/train.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ python3 ../../khnormal2.py ./train.er ./normalized/train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$
```

Normalization for the manual data:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/manual$ ls
test.cr  test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/manual$ mkdir normalized
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/manual$ python3 ../../khnormal2.py test.cr ./normalized/test.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/manual$ python3 ../../khnormal2.py test.er ./normalized/test.er
```

Let's check the current folder structure ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent$ tree ./word/
./word/
├── edit1
│   ├── normalized
│   │   ├── test.cr
│   │   ├── test.er
│   │   ├── train.cr
│   │   └── train.er
│   ├── test.cr
│   ├── test.er
│   ├── train.cr
│   └── train.er
├── edit2
│   ├── normalized
│   │   ├── test.cr
│   │   ├── test.er
│   │   ├── train.cr
│   │   └── train.er
│   ├── test.cr
│   ├── test.er
│   ├── train.cr
│   └── train.er
└── manual
    ├── normalized
    │   ├── test.cr
    │   └── test.er
    ├── test.cr
    └── test.er

6 directories, 20 files
```

Above folder is for future usages ...  
Note, current edit1 and edit2 data are word segmented data.  
We wanna train with character segmentation because of spelling mistakes are generally happen among characters ... 
For character level data, just copied normalized data into char/ folder ...  

## Character Segmentation

We will work with character segmented data for NMT model training/testing. And thus, we have to make character segmentation ...  

I used my old shell script named "char-segmentation.sh" under my GitHub, Tool/ ...  

```bash
#!/bin/bash

# character segmentation
# Written by Ye, LST Lab., NECTEC, Thailand
# How to run: char-segmentation.sh <input-filename>
# For example:
# cat chk.tmp
# နန် ကော်ဖီ သော့-က့့့််် ဟှို့လား ဆိုဟှီး ငါ  ပြော ဇာ ။
#
# ./char-segmentation.sh ./chk.tmp
# န န ် က ေ ာ ် ဖ ီ သ ေ ာ ့ - က ် ့ ် ့ ် ့ ဟ ှ ိ ု ့ လ ာ း ဆ ိ ု ဟ ှ ီ း င ါ ပ ြ ေ ာ ဇ ာ ။ 
# By using ./char-segmentation.sh, now you can clearly seen "three athat and auk-ka-myint" typing mistake of a Dawei sentence

sed 's/\(.\)/\1 /g' $1 | sed 's/ \+/ /g';
```

Character segmentation ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ chmod +x ../char-segmentation.sh
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ ../char-segmentation.sh ./test.cr > out
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ mv out test.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ head test.cr
អ ្ ន ក អ ា ច ប ិ ទ ក ា ត ា ប
ល ោ ក ស ្ រ ី ឈ ា ន អ ៊ ី ញ
ន េ ះ ជ ា ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ
ត ើ ច ំ ណ ា យ រ ួ ម ទ ា ំ ង អ ស ់ ស ម ្ រ ា ប ់ ស ំ ភ ា រ ៈ ថ ្ ល ៃ ប ៉ ុ ន ្ ម ា ន ?
ល ោ ក វ ណ ្ ណ រ ៉ ុ ង
រ ូ ប ៩ . ៣ ៩ ស ្ ម ៅ រ ព ា ក ់ ទ ឹ ក ខ . ជ ម ្ រ ក ន ិ ង ស ា រ ស ំ ខ ា ន ់ ស ្ ម ៅ រ ព ា ក ់ ទ ឹ ក ជ ា ជ ម ្ រ ក ស ត ្ វ ល ្ អ ិ ត ន ិ ង ជ ំ ង ឺ ម ួ យ ច ំ ន ួ ន ល ើ ដ ំ ណ ា ំ ស ្ រ ូ វ ដ ូ ច ជ ា ដ ង ្ ក ូ វ ប ា ក ់ ខ ្ ន ង ខ ្ ញ ុ ង ប ន ្ ល ា ម េ អ ំ ប ៅ ដ ង ្ ក ូ វ ភ ្ ន ែ ក ឆ ្ ម ា ដ ង ្ ក ូ វ ម ូ រ ស ្ ល ឹ ក ជ ំ ង ឺ ត ឿ ល ឿ ង ណ េ ម ៉ ា ត ូ ត ល ើ ឫ ស ខ ្ យ ង ស ៊ ី ស ្ រ ូ វ ព ណ ៌ ម ា ស ជ ា ដ ើ ម
ក ្ រ ុ ម ឃ ្ ល ា ំ ម ើ ល ន េ ះ ប ា ន ន ិ យ ា យ ថ ា ក ្ ន ុ ង ត ំ ប ន ់ ជ ា ច ្ រ ើ ន ន ៃ ខ េ ត ្ ត អ ា ឡ ិ ប ប ៉ ូ គ ្ រ ប ់ គ ្ រ ង ដ ោ យ ក ្ រ ុ ម ឧ ទ ្ ទ ា ម ក ្ ន ុ ង ន ោ ះ ម ា ន ក ្ រ ុ ង ន ោ ះ ផ ្ ទ ា ល ់ ផ ង « ជ ន ស ៊ ី វ ិ ល យ ៉ ា ង ត ិ ច ៧ ១ ន ា ក ់ ត ្ រ ូ វ ប ា ន ស ម ្ ល ា ប ់ » R ន ិ ង រ ា ប ់ ស ិ ប ន ា ក ់ ប ា ន រ ង រ ប ួ ស ន ៅ ព េ ល ឧ ទ ្ ធ ម ្ ភ ា គ ច ក ្ រ រ ប ប ន េ ះ ប ា ន ទ ម ្ ល ា ក ់ គ ្ រ ា ប ់ ប ែ ក ធ ុ ង » R ។
ត ើ ប ូ ក រ ួ ម ប ញ ្ ច ូ ល ទ ា ំ ង អ ា ជ ្ ញ ា ប ណ ្ ណ ដ ែ រ ទ េ ?
ខ ្ ញ ុ ំ ច ង ់ ទ ូ រ ស ័ ព ្ ទ ស ្ ថ ា ន ី យ ៍ ទ ៅ ស ្ ថ ា ន ី យ ៍ ទ ៅ ប ្ រ ទ េ ស ជ ប ៉ ុ ន
ត ើ ណ ា ម ួ យ ដ ែ ល អ ្ ន ក ច ង ់ ប ា ន ត ែ រ ឺ ក ា ហ ្ វ េ ?
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$
```

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ ../char-segmentation.sh ./test.er > out
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ mv ./out ./test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ ../char-segmentation.sh ./train.cr > out
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ mv ./out train.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ ../char-segmentation.sh ./train.er > out
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ mv ./out train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$
```

check all files under edit-1/   

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ head -3 *
==> normalized <==
head: error reading 'normalized': Is a directory

==> test.cr <==
អ ្ ន ក អ ា ច ប ិ ទ ក ា ត ា ប
ល ោ ក ស ្ រ ី ឈ ា ន អ ៊ ី ញ
ន េ ះ ជ ា ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ

==> test.er <==
អ ្ ន ក អ ា ច ប ិ ទ ក ា ត ា ប    អ ្ ន ក អ ា ច ប ិ ទ ា ត ា ប
ល ោ ក ស ្ រ ី ឈ ា ន អ ៊ ី ញ      ល ោ ក ស ្ រ ី ឈ ា ន អ ៊ ី ញ
ន េ ះ ជ ា ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ    ន េ ះ ជ ា ប ន ្ ទ ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ

==> train.cr <==
អ ្ ន ក អ ា ច ប ិ ទ ក ា ត ា ប
ល ោ ក ស ្ រ ី ឈ ា ន អ ៊ ី ញ
ន េ ះ ជ ា ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ

==> train.er <==
អ ្ ន ក អ ា ច ប ិ ទ ក ា ត ា ប    អ ្ ន ្ អ ា ច ប ិ ទ ក ា ត ា ប
ល ោ ក ស ្ រ ី ឈ ា ន អ ៊ ី ញ      ល ោ ក ស ្ ី ឈ ា ន អ ៊ ី ញ
ន េ ះ ជ ា ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ    ន េ ះ ជ ា ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ រ ំ
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$
```

For edit-1, normalized/ folder ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1/normalized$ ls
test.cr  test.er  train.cr  train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1/normalized$ ../../char-segmentation.sh ./test.cr > out
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1/normalized$ mv out test.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1/normalized$ ../../char-segmentation.sh ./test.er > out
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1/normalized$ mv out test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1/normalized$ ../../char-segmentation.sh train.cr > out
mye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1/normalized$ mv out train.r
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1/normalized$ ../../char-segmentation.sh train.er > out
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1/normalized$ mv out train.er
```

Checked the character segmented data with my eyeball: 

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1/normalized$ head -n 3 *
==> test.cr <==
អ ្ ន ក អ ា ច ប ិ ទ ក ា ត ា ប
ល ោ ក ស ្ រ ី ឈ ា ន អ ៊ ី ញ
ន េ ះ ជ ា ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ

==> test.er <==
អ ្ ន ក អ ា ច ប ិ ទ ក ា ត ា ប អ ្ ន ក អ ា ច ប ិ ទ ា ត ា ប
ល ោ ក ស ្ រ ី ឈ ា ន អ ៊ ី ញ ល ោ ក ស ្ រ ី ឈ ា ន អ ៊ ី ញ
ន េ ះ ជ ា ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ ន េ ះ ជ ា ប ន ្ ទ ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ

==> train.cr <==
អ ្ ន ក អ ា ច ប ិ ទ ក ា ត ា ប
ល ោ ក ស ្ រ ី ឈ ា ន អ ៊ ី ញ
ន េ ះ ជ ា ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ

==> train.er <==
អ ្ ន ក អ ា ច ប ិ ទ ក ា ត ា ប អ ្ ន ្ អ ា ច ប ិ ទ ក ា ត ា ប
ល ោ ក ស ្ រ ី ឈ ា ន អ ៊ ី ញ ល ោ ក ស ្ ី ឈ ា ន អ ៊ ី ញ
ន េ ះ ជ ា ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ ា ំ ន េ ះ ជ ា ប ន ្ ទ ប ់ ប ី ស ែ ស ិ ប ប ្ រ រ ំ
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1/normalized$
```

Character segmentation for edit-2 data:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2$ ls
normalized  test.cr  test.er  train.cr  train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2$ ../char-segmentation.sh ./test.cr > out
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2$ mv out test.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2$ ../char-segmentation.sh ./test.er > out
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2$ mv out test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2$ ../char-segmentation.sh ./train.cr > out
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2$ mv out train.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2$ ../char-segmentation.sh ./train.er > out
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2$ mv out train.er
```

Character segmentation for edit-2, normalized data:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2/normalized$ ls
test.cr  test.er  train.cr  train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2/normalized$ ../../char-segmentation.sh ./test.cr > out
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2/normalized$ mv out test.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2/normalized$ ../../char-segmentation.sh test.er > out
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2/normalized$ mv out test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2/normalized$ ../../char-segmentation.sh ./train.cr > out
mye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2/normalized$ mv out train.r
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2/normalized$ ../../char-segmentation.sh ./train.er > out
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2/normalized$ mv out train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2/normalized$ ls
test.cr  test.er  train.cr  train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2/normalized$
```

for training, I will used under normalized folder. And thus check with my eyeball :)  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2/normalized$ tail -n 3 *
==> test.cr <==
អ ្ ន ក អ ា ច ម ក ជ ួ យ ស ្ ទ ូ ច ទ ៅ ប ា ន ទ េ ?
ស ូ ម យ ក ព ួ ក យ ើ ង ទ ៅ ជ ួ ប វ េ ជ ្ ជ ប ណ ្ ឌ ិ ត ន ិ យ ា យ ភ ា ស ា ជ ប ៉ ុ ន
អ ្ ន ក ត ្ រ ូ វ ត ែ ប ំ ព េ ញ ក ន ្ ល ែ ង ដ ែ ល ខ ្ វ ះ ខ ា ត

==> test.er <==
អ ្ ន ក អ ា ច ម ក ជ ួ យ ស ្ ទ ូ ច ទ ៅ ប ា ន ទ េ ? អ ្ ន ក ា អ ា ច ម ក ជ ួ យ ស ្ ទ ូ ច ទ ៅ ប ន ា ទ េ ?
ស ូ ម យ ក ព ួ ក យ ើ ង ទ ៅ ជ ួ ប វ េ ជ ្ ជ ប ណ ្ ឌ ិ ត ន ិ យ ា យ ភ ា ស ា ជ ប ៉ ុ ន ស ូ ម យ ក ព ួ ក យ ើ ង ទ ៅ ជ ួ ប វ េ ជ ្ ជ ប ណ ្ ឌ ិ ត ន ិ យ ា យ ា ភ ស ា ជ ឌ ៉ ុ ន
អ ្ ន ក ត ្ រ ូ វ ត ែ ប ំ ព េ ញ ក ន ្ ល ែ ង ដ ែ ល ខ ្ វ ះ ខ ា ត អ ្ ន ក ត ្ រ ូ វ ត ែ ប ំ ព េ ញ ក ន ្ ែ ល ង ដ ែ ល ខ ្ វ ះ ខ ា ្

==> train.cr <==
ជ ា ម ួ យ គ ្ ន ា ន េ ះ ដ ែ រ ក ្ រ ុ ម រ ដ ្ ឋ អ ៊ ិ ស ្ ល ា ម ជ ្ រ ុ ល ន ិ យ ម ប ា ន ជ ំ រ ុ ញ ក ា រ វ ា យ ប ្ រ ហ ា រ រ ប ស ់ ខ ្ ល ួ ន ល ើ ក ្ រ ុ ង ស ៊ ី រ ី ភ ា គ ឦ ស ា ន ដ ោ យ ប ំ ផ ្ ទ ុ ះ គ ្ រ ា ប ់ ប ែ ក ក ្ ន ុ ង រ ថ យ ន ្ ត យ ៉ ា ង ត ិ ច ៥ គ ្ រ ឿ ង ខ ណ ៈ ព េ ល ខ ្ ល ួ ន ប ា ន រ ុ ល ទ ៅ ម ុ ខ ស ំ ដ ៅ ច ូ ល ក ្ រ ុ ង ។
ក ា ល ប ុ រ ស ទ ា ំ ង ៤ ន ា ក ់ យ ក ឈ ើ ម ក ធ ្ វ ើ ឲ ្ យ ក ើ ត ជ ា រ ូ ប ម ន ុ ស ្ ស ស ្ ត រ ី ប ា ន ស ្ រ េ ច ហ ើ យ ក ៏ ដ ណ ្ ត ើ ម គ ្ ន ា យ ក ស ្ ត រ ី ន ោ ះ ធ ្ វ ើ ជ ា ភ រ ិ យ ា ត ែ រ ៀ ង ខ ្ ល ួ ន ប ្ រ ក ែ ក គ ្ ន ា ទ ៅ វ ិ ញ ទ ៅ ម ក គ ្ ម ា ន អ ្ ន ក ណ ា ជ ំ ន ុ ំ ជ ម ្ រ ះ ស ម ្ រ េ ច ឲ ្ យ ស ោ ះ ទ ើ ប ន ា ំ គ ្ ន ា ទ ៅ ប ្ ត ឹ ង ច ៅ ក ្ រ ម ត ា ម ដ ំ ណ ើ រ ទ ី ទ ៃ ៗ ។
ខ ្ ញ ុ ំ ន ឹ ង យ ក ជ េ អ េ អ ែ ល

==> train.er <==
ជ ា ម ួ យ គ ្ ន ា ន េ ះ ដ ែ រ ក ្ រ ុ ម រ ដ ្ ឋ អ ៊ ិ ស ្ ល ា ម ជ ្ រ ុ ល ន ិ យ ម ប ា ន ជ ំ រ ុ ញ ក ា រ វ ា យ ប ្ រ ហ ា រ រ ប ស ់ ខ ្ ល ួ ន ល ើ ក ្ រ ុ ង ស ៊ ី រ ី ភ ា គ ឦ ស ា ន ដ ោ យ ប ំ ផ ្ ទ ុ ះ គ ្ រ ា ប ់ ប ែ ក ក ្ ន ុ ង រ ថ យ ន ្ ត យ ៉ ា ង ត ិ ច ៥ គ ្ រ ឿ ង ខ ណ ៈ ព េ ល ខ ្ ល ួ ន ប ា ន រ ុ ល ទ ៅ ម ុ ខ ស ំ ដ ៅ ច ូ ល ក ្ រ ុ ង ។ ជ ា ម ួ យ គ ្ ន ា ន េ ះ ដ ែ រ ក ្ រ ុ ម រ ដ ្ ឋ អ ៊ ិ ស ្ ល ា ម ជ ្ រ ុ ល ន ិ យ ម ប ា ន ជ ំ រ ុ ញ ក ា រ វ ា យ ប ្ រ ហ ា រ រ ប ស ់ ខ ្ ល ួ ន ល ើ ក ្ រ ុ ង ស ៊ ី រ ី ភ ា គ ឦ ស ា ន ដ ោ យ ប ំ ផ ្ ទ ុ ះ គ ្ រ ា ប ់ ប ែ ក ក ្ ន ុ ង រ ថ យ ន ្ ត យ ៉ ា ង ត ិ ច ៥ គ ្ រ ឿ ង ខ ណ ៈ ព េ ល ខ ្ ល ួ ន ប ា ន រ ុ ល ទ ៅ ម ុ ខ ស ំ ដ ៅ ច ូ ល ក ្ រ ុ ង ។
ក ា ល ប ុ រ ស ទ ា ំ ង ៤ ន ា ក ់ យ ក ឈ ើ ម ក ធ ្ វ ើ ឲ ្ យ ក ើ ត ជ ា រ ូ ប ម ន ុ ស ្ ស ស ្ ត រ ី ប ា ន ស ្ រ េ ច ហ ើ យ ក ៏ ដ ណ ្ ត ើ ម គ ្ ន ា យ ក ស ្ ត រ ី ន ោ ះ ធ ្ វ ើ ជ ា ភ រ ិ យ ា ត ែ រ ៀ ង ខ ្ ល ួ ន ប ្ រ ក ែ ក គ ្ ន ា ទ ៅ វ ិ ញ ទ ៅ ម ក គ ្ ម ា ន អ ្ ន ក ណ ា ជ ំ ន ុ ំ ជ ម ្ រ ះ ស ម ្ រ េ ច ឲ ្ យ ស ោ ះ ទ ើ ប ន ា ំ គ ្ ន ា ទ ៅ ប ្ ត ឹ ង ច ៅ ក ្ រ ម ត ា ម ដ ំ ណ ើ រ ទ ី ទ ៃ ៗ ។ ក ា ល ប ុ រ ស ទ ា ំ ង ៤ ន ា ក ក ់ យ ក ឈ ើ ម ក ធ ្ វ ើ ឲ ្ យ ក ើ ត ជ ា រ ូ ប ម ន ុ ស ្ ស ស ្ ត រ ី ប ា ន ស ្ រ េ ច ហ ើ យ ក ៏ ដ ណ ្ ត ើ ម គ ្ ន ា យ ក ស ្ ត រ ី ន ោ ះ ្ ធ វ ើ ជ ា ភ រ ិ យ ា ត ែ រ ៀ ង ខ ្ ល ួ ន ប ្ រ ក ែ ក គ ្ ន ា ទ ៅ វ ិ ញ ទ ៅ ម ក គ ្ ម ា ន អ ្ ន ក ណ ា ជ ំ ន ុ ំ ជ ម ្ រ ះ ស ម ្ រ េ ច ឲ ្ យ ស ោ ះ ទ ើ ប ន ា ំ គ ្ ន ា ទ ៅ ប ្ ត ឹ ង ច ៅ ក ្ រ ម ត ា ម ដ ំ ណ ើ រ ទ ី ទ ៃ ៗ ។
ខ ្ ញ ុ ំ ន ឹ ង យ ក ជ េ អ េ អ ែ ល ខ ្ ញ ុ ំ ន ឹ ង ក យ ជ េ អ េ អ ែ ល
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2/normalized$
```

```

```

```

```

```

```

```

```

```

```
