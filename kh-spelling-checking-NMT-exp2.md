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

Character segmentation for manual data:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char$ cd manual
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/manual$ ls
normalized  test.cr  test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/manual$ ../char-segmentation.sh ./test.cr > out
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/manual$ mv out test.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/manual$ ../char-segmentation.sh ./test.er > out
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/manual$ mv out test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/manual$ head -n 3 *
==> normalized <==
head: error reading 'normalized': Is a directory

==> test.cr <==
អ ៊ ី ច ឹ ង ក ៏ ថ ត គ ្ ន ា ដ ែ រ គ ្ រ ា ន ់ ត ែ គ ្ ន ា រ ក ស ៊ ី ម ក ព ស ់ រ ស ់ ម ួ យ ខ ្ ល ួ ន
ស ម ័ យ ផ ្ ត ា ច ់ ស ង ្ គ រ ា ម ខ ្ ម ែ រ យ ើ ង រ ៀ ន អ ក ្ ខ រ ក ម ្ ម ន ិ ង អ ក ្ ស រ ប ា រ ា ំ ង
ច ង ់ ម ា ន ប ា រ ា ំ ង ជ ួ យ ស ្ ទ ូ ច ត ្ រ ី ដ ូ ច ល ោ ក យ ា យ ដ ែ រ

==> test.er <==
ក ៏ ថ ត គ ្ ន ា ដ ែ រ គ ្ រ ា ន ់ ត ែ គ ្ ន ា រ ក ស ៊ ី ម ក ព ស ់ រ ស ់ ម ួ យ ខ ្ ល ួ ន
ស ម ័ យ ផ ្ ត ា ច ់ ស ង ្ គ រ ា ម ខ ្ ម ែ រ យ ើ ង រ ៀ ន អ ក ្ ខ រ ក ម ្ ម អ ក ្ ស រ
ច ង ់ ម ា ន ប ា រ ា ំ ង ជ ួ យ ត ្ រ ី ដ ូ ច ល ោ ក យ ា យ ដ ែ រ
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/manual$
```

Character segmentation for the manual/normalized data:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/manual$ cd normalized/
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/manual/normalized$ ls
test.cr  test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/manual/normalized$ ../../char-segmentation.sh ./test.cr > out
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/manual/normalized$ mv out test.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/manual/normalized$ ../../char-segmentation.sh ./test.er > out
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/manual/normalized$ mv out test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/manual/normalized$
```

Checked/Confirmed the character segmented data:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/manual/normalized$ head -n 3 *
==> test.cr <==
អ ៊ ី ច ឹ ង ក ៏ ថ ត គ ្ ន ា ដ ែ រ គ ្ រ ា ន ់ ត ែ គ ្ ន ា រ ក ស ៊ ី ម ក ព ស ់ រ ស ់ ម ួ យ ខ ្ ល ួ ន
ស ម ័ យ ផ ្ ត ា ច ់ ស ង ្ គ រ ា ម ខ ្ ម ែ រ យ ើ ង រ ៀ ន អ ក ្ ខ រ ក ម ្ ម ន ិ ង អ ក ្ ស រ ប ា រ ា ំ ង
ច ង ់ ម ា ន ប ា រ ា ំ ង ជ ួ យ ស ្ ទ ូ ច ត ្ រ ី ដ ូ ច ល ោ ក យ ា យ ដ ែ រ

==> test.er <==
ក ៏ ថ ត គ ្ ន ា ដ ែ រ គ ្ រ ា ន ់ ត ែ គ ្ ន ា រ ក ស ៊ ី ម ក ព ស ់ រ ស ់ ម ួ យ ខ ្ ល ួ ន
ស ម ័ យ ផ ្ ត ា ច ់ ស ង ្ គ រ ា ម ខ ្ ម ែ រ យ ើ ង រ ៀ ន អ ក ្ ខ រ ក ម ្ ម អ ក ្ ស រ
ច ង ់ ម ា ន ប ា រ ា ំ ង ជ ួ យ ត ្ រ ី ដ ូ ច ល ោ ក យ ា យ ដ ែ រ
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/manual/normalized$
```

## Checked the Parallel Data

I should check no. of lines ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ wc *
wc: normalized: Is a directory
       0        0        0 normalized
    5000   306542  1227528 test.cr
    4997   612988  2459679 test.er
   90000  5550114 22225205 train.cr
   89981 11099873 44538949 train.er
  189978 17569517 70451361 total
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ cd ../edit2/; wc *
wc: normalized: Is a directory
       0        0        0 normalized
    5000   306542  1227528 test.cr
    4998   613048  2459905 test.er
   90000  5550114 22225205 train.cr
   89978 11099462 44537272 train.er
  189976 17569166 70449910 total
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2$ cd ../manual; wc *
wc: normalized: Is a directory
      0       0       0 normalized
   7734  531058 2127990 test.cr
   7734  441784 1768641 test.er
  15468  972842 3896631 total
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/manual$
```

OH! not parallel as shown in above ...  
Something wrong ... I have to check ...  

## Found Error Reason

I found the error reason and as shown below ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1$ ls
normalized  test.cr  test.er  train.cr  train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1$ head test.er
អ្នក អាច បិទ កាតាប       អ្នក អាច បិទ ាតាប
លោកស្រី ឈាន អ៊ីញ         លោកស្រីឈាន អ៊ីញ
នេះ ជា បន្ទប់ បី សែសិប ប្រាំ     នេះ ជា បន្ទ ់ បី សែសិប ប្រាំ
តើ ចំណាយ រួមទាំងអស់ សម្រាប់ សំភារៈ ថ្លៃ ប៉ុន្មាន ?       តើ ចំណាយ រួមទាំងអស់ សម្រាប់ សំភារៈថ្លៃ ប៉ុន្មាន ?
លោក វណ្ណ រ៉ុង    លោក វ្ណ រ៉ុង
រូប ៩ . ៣៩ ស្មៅ រពាក់ ទឹក ខ. ជម្រក និង សារសំខាន់ ស្មៅ រពាក់ ទឹក ជា ជម្រក សត្វ ល្អិត និង ជំងឺ មួយចំនួន លើ ដំណាំ ស្រូវ ដូចជា ដង្កូវ បាក់ ខ្នង ខ្ញុង បន្លា មេអំបៅ ដង្កូវ ភ្នែក ឆ្មា ដង្កូវ មូរ ស្លឹក ជំងឺ តឿ លឿង ណេម៉ាតូត លើ ឫស ខ្យង ស៊ី ស្រូវ ពណ៌ មាស ជាដើម    រូប ៩ . ៣៩ ស្មៅ រពាក់ ទឹក ខ. ជម្រក និង សារសំខាន់ ស្មៅ រពាក់ ទឹកម ជា ជម្រក សត្វ ល្អិត និង ជំងឺ មួយចំនួន លើ ដំណាំ ស្រូវ ដូចជា ដង្កូវ បាក់ ខ្នង ខ្ញុង បន្លា មេអំបៅ ដង្កូវ ភ្នែក ឆ្មា ដង្កូវ មូរ ស្លឹក ជំងឺ តឿ លឿង ណេម៉ាតូត លើ ឫស ខ្យង ស៊ី ស្រូវ ពណ៌ មាស ជាដើម
ក្រុម ឃ្លាំមើល នេះ បាន និយាយ ថា ក្នុង តំបន់ ជាច្រើន នៃ ខេត្ត អាឡិបប៉ូ គ្រប់គ្រង ដោយ ក្រុម ឧទ្ទាម ក្នុង នោះ មាន ក្រុង នោះ ផ្ទាល់ ផង « ជន ស៊ីវិល យ៉ាងតិច ៧១ នាក់ ត្រូវបាន សម្លាប់ »R និង រាប់ សិប នាក់ បាន រងរបួស នៅពេល ឧទ្ធម្ភាគចក្រ របប នេះ បាន ទម្លាក់ គ្រាប់បែក ធុង »R ។   ក្រុម ឃ្លាំមើល នេះ បាន និយាយ ថា ក្នុង តំបន់ ជាច្រើន នៃ ខេត្ត អាឡិបប៉ូ គ្រប់គ្រង ដោយ ក្រុម ឧទ្ទាម ក្នុង នោះ មាន ក្រុង នោះ ផ្ទាល់ ផង « ជន ស៊ីវិល យ៉ាងតិច ៧១ នកាក់ ត្រូវបាន សម្លាប់ »R និង រាប់ សិប នាក់ បាន រងរបួស នៅពេល ឧទ្ធម្ភាគចក្រ របប នេះ បាន ទម្លាក់ គ្រាប់បែក ធុង »R ។
តើ បូករួមបញ្ចូល ទាំង អាជ្ញាបណ្ណ ដែរ ទេ ?         តើ បូករួមបញ្ចូល ទាង អាជ្ញាបណ្ណ ដែរ ទេ ?
ខ្ញុំ ចង់ ទូរស័ព្ទ ស្ថានីយ៍ ទៅ ស្ថានីយ៍ ទៅ ប្រទេស ជប៉ុន          ខ្ញុំ ចង់ ទូរស័ព្ទ  ស្ថានីយ៍ ទៅ ស្ថានីយ៍ ទៅ ប្រទេស ជប៉ុន
តើ ណាមួយ ដែល អ្នក ចង់បាន តែ រឺ កាហ្វេ ?          តើ ណាមួយ ដែល អ្នក ចង់បាន តែ រ ឺកាហ្វេ ?
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1$
```

After simulation of edit1 and edit2, I should get the training data from the output file or error file.   

## Recreating .cr Files for Word/  

Recreating .cr files for edit1 and edit2 data ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1$ ls
normalized  test.cr  test.er  train.cr  train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1$ rm *.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1$ ls
normalized  test.er  train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1$ mkdir original-err
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1$ mv *.er ./original-err/
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1$ cut -f1 ./original-err/test.er > ./test.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1$ cut -f2 ./original-err/tes
t.er > ./test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1$
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1$ cut -f1 ./original-err/train.er > ./train.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1$ cut -f2 ./original-err/tra
in.er > ./train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1$ wc *
wc: normalized: Is a directory
       0        0        0 normalized
wc: original-err: Is a directory
       0        0        0 original-err
    4997    70463   991519 test.cr
    4997    70307   991292 test.er
   89981  1271358 17946793 train.cr
   89981  1267963 17946779 train.er
  189956  2680091 37876383 total
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1$
```

recreating correct parallel data for edit1/normalized/ folder:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1/normalized$ mkdir original-err
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1/normalized$ mv *.er ./original-err/
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1/normalized$ ls
original-err
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1/normalized$ cut -f1 ./original-err/test.er > ./test.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1/normalized$ cut -f2 ./origi
nal-err/test.er > ./test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1/normalized$ cut -f1 ./original-err/train.er > ./train.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1/normalized$ cut -f2 ./origi
nal-err/train.er > ./train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1/normalized$ wc *
wc: original-err: Is a directory
       0        0        0 original-err
    4997   140770  1976107 test.cr
    4997   140770  1976107 test.er
   89981  2539404 35774429 train.cr
   89981  2539404 35774429 train.er
  189956  5360348 75501072 total
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit1/normalized$
```

recreating correct parallel data for edit2/ folder:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word$ cd edit2
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ ls
normalized  test.cr  test.er  train.cr  train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ rm *.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ mkdir original-err
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ mv *.er ./original-err/
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ cut -f1 ./original-err/test.er > ./test.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ cut -f2 ./original-err/tes
t.er > ./test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ cut -f1 ./original-err/train.er > ./train.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ cut -f2 ./original-err/tra
in.er > ./train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ wc *
wc: normalized: Is a directory
       0        0        0 normalized
wc: original-err: Is a directory
       0        0        0 original-err
    4998    70464   991524 test.cr
    4998    70141   991542 test.er
   89978  1271356 17946782 train.cr
   89978  1265162 17946344 train.er
  189952  2677123 37876192 total
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$
```

recreating correct parallel data for edit2/normalized/ folder data:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word$ cd edit2
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ ls
normalized  test.cr  test.er  train.cr  train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ rm *.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ mkdir original-err
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ mv *.er ./original-err/
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ cut -f1 ./original-err/test.er > ./test.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ cut -f2 ./original-err/tes
t.er > ./test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ cut -f1 ./original-err/train.er > ./train.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ cut -f2 ./original-err/tra
in.er > ./train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$ wc *
wc: normalized: Is a directory
       0        0        0 normalized
wc: original-err: Is a directory
       0        0        0 original-err
    4998    70464   991524 test.cr
    4998    70141   991542 test.er
   89978  1271356 17946782 train.cr
   89978  1265162 17946344 train.er
  189952  2677123 37876192 total
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/word/edit2$
```

## Recreating .cr Files for char/

Actually, recreating both cr and er files ... to make correct pairs ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ ls
normalized  original-err  test.cr  test.er  train.cr  train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ rm *.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ ls
normalized  original-err  test.er  train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ mv *.er ./original-err/
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ ls
normalized  original-err
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ cut -f1 ./original-err/test.er > ./test.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ cut -f2 ./original-err/tes
t.er > ./test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ cut -f1 ./original-err/train.er > ./train.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ cut -f2 ./original-err/tra
in.er > ./train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$ wc *
wc: normalized: Is a directory
       0        0        0 normalized
wc: original-err: Is a directory
       0        0        0 original-err
    4997   306540  1227517 test.cr
    4997   306448  1232162 test.er
   89981  5549794 22223901 train.cr
   89981  5549679 22313432 train.er
  189956 11712461 46997012 total
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1$
```

for char/edit1/normalized:  

```

ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1/normalized$ ls
test.cr  test.er  train.cr  train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1/normalized$ mkdir original-err
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1/normalized$ rm *.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1/normalized$ mv *.er ./original-err/
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1/normalized$ cut -f1 ./original-err/test.er > ./test.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1/normalized$ cut -f2 ./origi
nal-err/test.er > ./test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1/normalized$ cut -f1 ./original-err/train.er > ./train.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1/normalized$ cut -f2 ./origi
nal-err/train.er > ./train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1/normalized$ wc *
wc: original-err: Is a directory
       0        0        0 original-err
    4997   612419  2447409 test.cr
    4997   612419  2447409 test.er
   89981 11089727 44318373 train.cr
   89981 11089727 44318373 train.er
  189956 23404292 93531564 total
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit1/normalized$
```

for char/edit2/:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2$ ls
normalized  test.cr  test.er  train.cr  train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2$ mkdir original-err
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2$ rm *.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2$ mv *.er ./original-err/
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2$ cut -f1 ./original-err/test.er > ./test.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2$ cut -f2 ./original-err/tes
t.er > ./test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2$ cut -f1 ./original-err/train.er > ./train.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2$ cut -f2 ./original-err/tra
in.er > ./train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2$ wc *
wc: normalized: Is a directory
       0        0        0 normalized
wc: original-err: Is a directory
       0        0        0 original-err
    4998   306541  1227522 test.cr
    4998   306507  1232383 test.er
   89978  5549793 22223891 train.cr
   89978  5549269 22311765 train.er
  189952 11712110 46995561 total
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2$

```

for char/edit2/normalized:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2$ ls
normalized  original-err  test.cr  test.er  train.cr  train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2$ cd normalized/
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2/normalized$ ls
test.cr  test.er  train.cr  train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2/normalized$ mkdir original-err
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2/normalized$ rm *.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2/normalized$ mv *.er ./original-err/
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2/normalized$ cut -f1 ./original-err/test.er > ./test.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2/normalized$ cut -f2 ./origi
nal-err/test.er > ./test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2/normalized$ cut -f1 ./original-err/train.er > ./train.cr
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2/normalized$ cut -f2 ./origi
nal-err/train.er > ./train.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/edit2/normalized$ wc *
wc: original-err: Is a directory
       0        0        0 original-err
    4998   612428  2447429 test.cr
    4998   612428  2447429 test.er
   89978 11088314 44312694 train.cr
   89978 11088314 44312694 train.er
  189952 23401484 93520246 total

```

## Check the Data Again  

See the char/ folder structure:   

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char$ ls *
char-segmentation.sh

edit1:
normalized  original-err  test.cr  test.er  train.cr  train.er

edit2:
normalized  original-err  test.cr  test.er  train.cr  train.er

manual:
normalized  test.cr  test.er
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char$

```

Actually, I have to used normalized data only and move to a new folder for easy to access:  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char$ mkdir char-final
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char$ cp -r ./edit1/normalized/ ./char-final/edit1
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char$ cp -r ./edit2/normalized/ ./char
-final/edit2
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char$ cp -r ./manual/normalized/ ./cha
r-final/manual
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char$
```

check ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char$ tree ./char-final/
./char-final/
├── edit1
│   ├── original-err
│   │   ├── test.er
│   │   └── train.er
│   ├── test.cr
│   ├── test.er
│   ├── train.cr
│   └── train.er
├── edit2
│   ├── original-err
│   │   ├── test.er
│   │   └── train.er
│   ├── test.cr
│   ├── test.er
│   ├── train.cr
│   └── train.er
└── manual
    ├── test.cr
    └── test.er

5 directories, 14 files
```
Important!!!  
Path of the final character segmented and also Normalized Data (in Preprocessing Step):  
/home/ye/exp/kh-spell/data/kh-segment/4khspell/preprocessing/data-sent/char/char-final  

copy above folders to the NMT experiment folder:  

```
ye@lst-gpu-3090:~/exp/kh-spell/transformer$ sudo cp -r /home/ye/exp/kh-spell/data/kh-segment/4khspell/preprocessing/da
ta-sent/char/char-final/ .
```

## Adding Validation Data

for edit1/  

```
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit1# head -n 80000 ./train-valid/train.cr > ./train.cr
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit1# tail -n 9981 ./train-valid/train.cr > ./valid.cr
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit1# head -n 80000 ./train-valid/train.er > ./train.e
r
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit1# tail -n 9981 ./train-valid/train.er > ./valid.er
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit1#
```

Final data size for edit1/  

```
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit1# wc {train,valid,test}.{cr,er}
   80000    54660 39293638 train.cr
   80000    54660 39293638 train.er
    9981     6911  5024735 valid.cr
    9981     6911  5024735 valid.er
    4997     3416  2447409 test.cr
    4997     3416  2447409 test.er
  189956   129974 93531564 total
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit1#
```

adding validation data for edit2/  

```
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit2# wc ./train-valid/*
   89978    61584 44312694 ./train-valid/train.cr
   89978    61584 44312694 ./train-valid/train.er
  179956   123168 88625388 total
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit2# head -n 80000 ./train-valid/train.cr > ./train.cr
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit2# tail -n 9978 ./train-valid/train.cr > ./valid.cr
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit2# head -n 80000 ./train-valid/train.er > ./train.e
r
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit2# tail -n 9978 ./train-valid/train.er > ./valid.er
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit2#
```

check data size for edit2/  

```
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit2# wc {train,valid,test}.{cr,er}
   80000    54677 39289177 train.cr
   80000    54677 39289177 train.er
    9978     6907  5023517 valid.cr
    9978     6907  5023517 valid.er
    4998     3424  2447429 test.cr
    4998     3424  2447429 test.er
  189952   130016 93520246 total
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit2#
```

manual test data:  

```
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/manual# wc *
   7734    3204 2127990 test.cr
   7734    3135 1768641 test.er
  15468    6339 3896631 total
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/manual# head -n 2 *
==> test.cr <==
អ ៊ ី ច ឹ ង ក ៏ ថ ត គ ្ ន ា ដ ែ រ គ ្ រ ា ន ់ ត ែ គ ្ ន ា រ ក ស ៊ ី ម ក ព ស ់ រ ស ់ ម ួ យ ខ ្ ល ួ ន
ស ម ័ យ ផ ្ ត ា ច ់ ស ង ្ គ រ ា ម ខ ្ ម ែ រ យ ើ ង រ ៀ ន អ ក ្ ខ រ ក ម ្ ម ន ិ ង អ ក ្ ស រ ប ា រ ា ំ ង

==> test.er <==
ក ៏ ថ ត គ ្ ន ា ដ ែ រ គ ្ រ ា ន ់ ត ែ គ ្ ន ា រ ក ស ៊ ី ម ក ព ស ់ រ ស ់ ម ួ យ ខ ្ ល ួ ន
ស ម ័ យ ផ ្ ត ា ច ់ ស ង ្ គ រ ា ម ខ ្ ម ែ រ យ ើ ង រ ៀ ន អ ក ្ ខ រ ក ម ្ ម អ ក ្ ស រ
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/manual#
```

## Experimental Setting

I will train two models. One is training with edit-distance 1 errors and another is edit-distance 2 errors.  
For the testing, I will use three test-sets. They are as follows:  

- edit-1 test-set (test set of Khmer word segmented data with edit-1)
- edit-2 test-set (test set of Khmer word segmented data with edit-2)
- manual test-set (the whole data that manually prepared)


## Make Vocab

for edit1/  

```
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit1# cd vocab/
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit1/vocab# marian-vocab < ./all.cr > vocab.cr.yml
[2022-10-22 15:57:28] Creating vocabulary...
[2022-10-22 15:57:28] [data] Creating vocabulary stdout from stdin
[2022-10-22 15:57:29] Finished
```

```
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit1/vocab# marian-vocab < ./all.er > vocab.er.yml
[2022-10-22 15:57:50] Creating vocabulary...
[2022-10-22 15:57:50] [data] Creating vocabulary stdout from stdin
[2022-10-22 15:57:51] Finished
```


for edit2/  

```
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit2# ls
original-err  test.cr  test.er  train-valid  train.cr  train.er  valid.cr  valid.er
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit2# mkdir vocab
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit2# cat train.cr valid.cr test.cr ../edit1/test.cr ../manual/test.cr > ./vocab/all.cr
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit2# cat train.er valid.er test.er ../edit1/test.er .
./manual/test.er > ./vocab/all.er
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit2#
```

```
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit2/vocab# ls
all.cr  all.er
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit2/vocab# marian-vocab < all.cr > vocab.cr.yml
[2022-10-22 16:01:06] Creating vocabulary...
[2022-10-22 16:01:06] [data] Creating vocabulary stdout from stdin
[2022-10-22 16:01:07] Finished
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit2/vocab# marian-vocab < all.er > vocab.er.yml
[2022-10-22 16:01:16] Creating vocabulary...
[2022-10-22 16:01:16] [data] Creating vocabulary stdout from stdin
[2022-10-22 16:01:17] Finished
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit2/vocab#
```

check vocab file:  

```
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit2/vocab# head vocab.*
==> vocab.cr.yml <==
</s>: 0
<unk>: 1                                                                                                              ្
: 2
ា: 3
ន: 4
រ: 5
ក: 6
ប: 7
ម: 8
ស: 9

==> vocab.er.yml <==
</s>: 0
<unk>: 1                                                                                                              ្
: 2
ា: 3
ន: 4
រ: 5
ក: 6
ប: 7
ម: 8
ស: 9
root@2541295674c9:/home/ye/exp/kh-spell/transformer/char-final/edit2/vocab#
```

## Prepare Shell Script for Edit1 Model

Data Path:  
/home/ye/exp/kh-spell/transformer/char-final/edit1  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, LST, NECTEC, Thailand
## Experiments for Khmer Spelling Correction with NMT model, Sentence Level Experiment 1
## Training with Edit Distance 1
## Last updated: 22 Oct 2022

mkdir model.transformer.sent.edit1;

marian \
    --model model.transformer.sent.edit1/model.npz --type transformer \
    --train-sets char-final/edit1/train.er char-final/edit1/train.cr \
    --max-length 300 \
    --vocabs char-final/edit1/vocab/vocab.er.yml char-final/edit1/vocab/vocab.cr.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets char-final/edit1/valid.er char-final/edit1/valid.cr \
    --valid-translation-output model.transformer.sent.edit1/valid.er-cr.output --quiet-translation \
    --valid-mini-batch 64 \
    --beam-size 6 --normalize 0.6 \
    --log model.transformer.sent.edit1/train.log --valid-log model.transformer.sent.edit1/valid.log \
    --enc-depth 2 --dec-depth 2 \
    --transformer-heads 8 \
    --transformer-postprocess-emb d \
    --transformer-postprocess dan \
    --transformer-dropout 0.3 --label-smoothing 0.1 \
    --learn-rate 0.0003 --lr-warmup 0 --lr-decay-inv-sqrt 16000 --lr-report \
    --clip-norm 5 \
    --tied-embeddings \
    --devices 0 --sync-sgd --seed 1111 \
    --exponential-smoothing \
    --dump-config > model.transformer.sent.edit1/config.yml

time marian -c model.transformer.sent.edit1/config.yml  2>&1 | tee transformer.sent.edit1.log
```

## Training edit-1 Model

```
ye@lst-gpu-3090:~/exp/kh-spell/transformer$ nvidia-smi
Sat Oct 22 23:13:28 2022
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 515.65.07    Driver Version: 515.65.07    CUDA Version: 11.7     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  On   | 00000000:01:00.0 Off |                  Off |
| 39%   59C    P2   138W / 480W |   9030MiB / 24564MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A      1700      G   /usr/lib/xorg/Xorg                 59MiB |
|    0   N/A  N/A      2469      G   /usr/bin/gnome-shell               11MiB |
|    0   N/A  N/A     38105      C   marian                           8955MiB |
+-----------------------------------------------------------------------------+
```

Check again after some minutes ...  

```
ye@lst-gpu-3090:~/exp/kh-spell/transformer$ nvidia-smi
Sat Oct 22 23:16:37 2022
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 515.65.07    Driver Version: 515.65.07    CUDA Version: 11.7     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  On   | 00000000:01:00.0 Off |                  Off |
| 35%   60C    P2   145W / 480W |  14534MiB / 24564MiB |    100%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A      1700      G   /usr/lib/xorg/Xorg                 59MiB |
|    0   N/A  N/A      2469      G   /usr/bin/gnome-shell               11MiB |
|    0   N/A  N/A     38105      C   marian                          14459MiB |
+-----------------------------------------------------------------------------+
```

For this time, I noted slow ... because of sentence level + character segmentation ...  

```
[2022-10-22 16:10:47] Ep. 1 : Up. 2000 : Sen. 55,937 : Cost 1.20876622 * 1,250,415 @ 2,803 after 5,001,838 : Time 8.51s : 146867.69 words/s : gNorm 0.9901 : L.r. 3.0000e-04
[2022-10-22 16:10:55] Ep. 1 : Up. 2500 : Sen. 69,831 : Cost 0.99243867 * 1,248,123 @ 2,847 after 6,249,961 : Time 8.51s : 146588.79 words/s : gNorm 0.6245 : L.r. 3.0000e-04
[2022-10-22 16:10:57] Seen 72,083 samples
[2022-10-22 16:10:57] Starting data epoch 2 in logical epoch 2
[2022-10-22 16:10:57] [data] Shuffling data
[2022-10-22 16:10:57] [data] Done reading 80,000 sentences
[2022-10-22 16:10:57] [data] Done shuffling 80,000 sentences to temp files
[2022-10-22 16:11:04] Ep. 2 : Up. 3000 : Sen. 11,650 : Cost 0.91625762 * 1,248,821 @ 2,564 after 7,498,782 : Time 8.73s : 143006.84 words/s : gNorm 0.5931 : L.r. 3.0000e-04
[2022-10-22 16:11:13] Ep. 2 : Up. 3500 : Sen. 25,832 : Cost 0.89091688 * 1,250,325 @ 2,215 after 8,749,107 : Time 8.54s : 146408.82 words/s : gNorm 0.5270 : L.r. 3.0000e-04
[2022-10-22 16:11:21] Ep. 2 : Up. 4000 : Sen. 39,606 : Cost 0.88055176 * 1,248,212 @ 2,408 after 9,997,319 : Time 8.53s : 146349.93 words/s : gNorm 0.4775 : L.r. 3.0000e-04
[2022-10-22 16:11:30] Ep. 2 : Up. 4500 : Sen. 53,582 : Cost 0.87474698 * 1,253,839 @ 2,821 after 11,251,158 : Time 8.55s : 146646.13 words/s : gNorm 0.4261 : L.r. 3.0000e-04
[2022-10-22 16:11:38] Ep. 2 : Up. 5000 : Sen. 67,454 : Cost 0.87188166 * 1,247,536 @ 2,483 after 12,498,694 : Time 8.52s : 146409.83 words/s : gNorm 0.4728 : L.r. 3.0000e-04
[2022-10-22 16:11:38] Saving model weights and runtime parameters to model.transformer.sent.edit1/model.iter5000.npz
[2022-10-22 16:11:38] Saving model weights and runtime parameters to model.transformer.sent.edit1/model.npz
[2022-10-22 16:11:38] Saving Adam parameters
[2022-10-22 16:11:39] [training] Saving training checkpoint to model.transformer.sent.edit1/model.npz and model.transformer.sent.edit1/model.npz.optimizer.npz
[2022-10-22 16:12:26] [valid] Ep. 2 : Up. 5000 : cross-entropy : 77.4693 : new best
[2022-10-22 16:12:30] [valid] Ep. 2 : Up. 5000 : perplexity : 1.84213 : new best
```

Anyway, for today, I did my best ... I should enjoy my late dinner ... :)  

## Training Finished for Edit-1

Training finished with ./transformer.sent.edit1.sh ...  

```
[2022-10-22 19:35:36] Ep. 25 : Up. 64500 : Sen. 71,273 : Cost 0.85035706 * 1,252,505 @ 2,727 after 161,220,923 : Time 8.63s : 145114.49 words/s : gNorm 0.1926 : L.r. 1.4942e-04
[2022-10-22 19:35:37] Seen 72,083 samples
[2022-10-22 19:35:37] Starting data epoch 26 in logical epoch 26
[2022-10-22 19:35:37] [data] Shuffling data
[2022-10-22 19:35:37] [data] Done reading 80,000 sentences
[2022-10-22 19:35:37] [data] Done shuffling 80,000 sentences to temp files
[2022-10-22 19:35:45] Ep. 26 : Up. 65000 : Sen. 12,802 : Cost 0.85032624 * 1,243,154 @ 2,063 after 162,464,077 : Time 8.90s : 139713.63 words/s : gNorm 0.2408 : L.r. 1.4884e-04
[2022-10-22 19:35:45] Saving model weights and runtime parameters to model.transformer.sent.edit1/model.iter65000.npz
[2022-10-22 19:35:45] Saving model weights and runtime parameters to model.transformer.sent.edit1/model.npz
[2022-10-22 19:35:46] Saving Adam parameters
[2022-10-22 19:35:46] [training] Saving training checkpoint to model.transformer.sent.edit1/model.npz and model.transformer.sent.edit1/model.npz.optimizer.npz
[2022-10-22 19:35:52] [valid] Ep. 26 : Up. 65000 : cross-entropy : 88.5425 : stalled 10 times (last best: 77.1247)
[2022-10-22 19:35:57] [valid] Ep. 26 : Up. 65000 : perplexity : 2.01022 : stalled 10 times (last best: 1.83713)
[2022-10-22 19:54:50] [valid] Ep. 26 : Up. 65000 : bleu : 84.2957 : stalled 3 times (last best: 89.5234)
[2022-10-22 19:54:50] Training finished
[2022-10-22 19:54:50] Saving model weights and runtime parameters to model.transformer.sent.edit1/model.npz
[2022-10-22 19:54:51] Saving Adam parameters
[2022-10-22 19:54:51] [training] Saving training checkpoint to model.transformer.sent.edit1/model.npz and model.transformer.sent.edit1/model.npz.optimizer.npz

real    224m42.879s
user    219m2.983s
sys     5m57.986s
```

## Check the Validation Results

```
[2022-10-22 16:12:26] [valid] Ep. 2 : Up. 5000 : cross-entropy : 77.4693 : new best
[2022-10-22 16:12:30] [valid] Ep. 2 : Up. 5000 : perplexity : 1.84213 : new best
[2022-10-22 16:18:29] [valid] First sentence's tokens as scored:
[2022-10-22 16:18:29] [valid] DefaultVocab keeps original segments for scoring
[2022-10-22 16:18:29] [valid]   Hyp: �~^~@ �~_~R �~^~S �~^� �~^~D �~^~@ �~^~Z �~^~N �~^� �~^~J �~_~B �~^~[ �~^~_ �~^~O �~_~R �~^~\ �~^~@ �~^~D �~_~R �~^~@ �~_~B �~^~T �~^� �~^� �~^~E �~^~_ �~^� �~^~X �~^~B �~_~R �~^~B �~^� �~^~B �~_~R �~^~S �~^� �~^~R �~_~R �~^~\ �~^� �~^~G �~^� �~^~S �~^� �~^� �~^� �~^~@ �~^� �~^~J �~^� �~^~X �~_~R �~^~T �~^� �~^~J �~^� �~^~_ �~_~K �~^~O �~^� �~^~S �~^~V �~^~I �~_~R �~^~I �~^� �~^~@ �~_~K �~^~_ �~_~R �~^~X �~^� �~^~Z �~^~O �~^� �~^~X �~^~S �~^� �~^~_ �~_~R �~^~_ �~^~_ �~^~O �~_~R �~^~\ �~^~J �~^~Q �~_~C �~^� �~_~D �~^~Y �~^~X �~^~@ �~^~_ �~^~X �~_~R �~^~[ �~^� �~^~D �~^~X �~^� �~^~[ �~^~_ �~_~D �~^~W �~_~P �~^~N �~^~J �~_~O �~^~_ �~_~D �~^~W �~^� �~^~Z �~^~T �~^~_ �~_~K �~^~X �~_~A �~^~C �~^~S �~^� �~^~D �~^~W �~^~V �~^~U �~_~B �~^~S �~^~J �~^� �~^~@ �~_~R �~^~Z �~_~D �~^~Y �~^~V �~_~A �~^~[ �~^~W �~_~R �~^~[ �~_~@ �~^~D �~^~T �~^� �~^~S �~^~E �~^� �~_~G �~^~Y �~^� �~^~D �~^~Q �~^� �~_~F �~^~D �~^� �~^� �~^~Y �~^~J �~_~B �~^~[ �~^~G �~^� �~^~X �~^~S �~^� �~^~_ �~_~R �~^~_ �~^~J �~_~O �~^~X �~^� �~^~S �~^~_ �~^~O �~^� �~^~T �~_~R �~^~Z �~^� �~^~G �~_~R �~^~I �~^� �~^~_ �~_~R �~^~X �~^� �~^~Z �~^~O �~^� �~^~Y �~_~I �~^� �~^~D �~^~V �~^~N �~_~R �~^~N �~^~Z �~^� �~^~Y �~^|  �~_~A �~^~O �~^� �~^� �~_~R �~^~\ �~^� �~^~@ �~_~O �~^~S �~^� �~_~F �~^~B �~_~R �~^~S �~^� �~^~_ �~^� �~^~D �~^~Q �~^~J �~_~R �~^~K �~^� �~^~_ �~_~B �~^~S �~^~E �~^~D �~_~R �~^� �~_~@ �~^~O �~^~E �~^~D �~_~R �~^� �~^~[ �~_~K �~^~J �~_~@ �~^~[ �~^~O �~_~R �~^~X �~_~G �~^~_ �~^~O �~_~R �~^~\ �~^~@ �~^~D �~_~R �~^~@ �~_~B �~^~T �~^~X �~^� �~^~S �~^~H �~^~T �~_~K �~^~H �~^~Z �~^~P �~^� �~^~G �~^� �~^~_ �~^~O �~_~R �~^~\ �~^~X �~^� �~^~S �~^~T �~_~R �~^~Z �~^� �~^~G �~_~R �~^~[ �~_~@ �~^~D �~^~T �~^� �~^~S
[2022-10-22 16:18:29] [valid]   Ref: �~^~@ �~_~R �~^~S �~^� �~^~D �~^~@ �~^~Z �~^~N �~^� �~^~J �~_~B �~^~[ �~^~_ �~^~O �~_~R �~^~\ �~^~@ �~^~D �~_~R �~^~@ �~_~B �~^~T �~^� �~^� �~^~E �~^~_ �~^� �~^~X �~^~B �~_~R �~^~B �~^� �~^~B �~_~R �~^~S �~^� �~^~R �~_~R �~^~\ �~^� �~^~G �~^� �~^~S �~^� �~^� �~^� �~^~@ �~^� �~^~J �~^� �~^~X �~_~R �~^~T �~^� �~^~J �~^� �~^~_ �~_~K �~^~O �~^� �~^~S �~^~V �~^~I �~_~R �~^~I �~^� �~^~@ �~_~K �~^~_ �~_~R �~^~X �~^� �~^~Z �~^~O �~^� �~^~X �~^~S �~^� �~^~_ �~_~R �~^~_ �~^~_ �~^~O �~_~R �~^~\ �~^~J �~^~Q �~_~C �~^� �~_~D �~^~Y �~^~X �~^~@ �~^~_ �~^~X �~_~R �~^~[ �~^� �~^~D �~^~X �~^� �~^~[ �~^~_ �~_~D �~^~W �~_~P �~^~N �~^~J �~_~O �~^~_ �~_~D �~^~W �~^� �~^~Z �~^~T �~^~_ 
...
...
[2022-10-22 16:31:33] [valid] Ep. 2 : Up. 5000 : bleu : 88.4342 : new best
[2022-10-22 16:33:07] [valid] Ep. 4 : Up. 10000 : cross-entropy : 78.1191 : stalled 1 times (last best: 77.4693)
[2022-10-22 16:33:11] [valid] Ep. 4 : Up. 10000 : perplexity : 1.85159 : stalled 1 times (last best: 1.84213)
[2022-10-22 16:45:30] [valid] Ep. 4 : Up. 10000 : bleu : 88.5898 : new best
[2022-10-22 16:47:05] [valid] Ep. 6 : Up. 15000 : cross-entropy : 77.1247 : new best
[2022-10-22 16:47:09] [valid] Ep. 6 : Up. 15000 : perplexity : 1.83713 : new best
[2022-10-22 16:59:34] [valid] Ep. 6 : Up. 15000 : bleu : 88.777 : new best
[2022-10-22 17:01:08] [valid] Ep. 8 : Up. 20000 : cross-entropy : 79.2297 : stalled 1 times (last best: 77.1247)
[2022-10-22 17:01:13] [valid] Ep. 8 : Up. 20000 : perplexity : 1.86788 : stalled 1 times (last best: 1.83713)
[2022-10-22 17:13:47] [valid] Ep. 8 : Up. 20000 : bleu : 89.3499 : new best
[2022-10-22 17:15:22] [valid] Ep. 10 : Up. 25000 : cross-entropy : 82.8781 : stalled 2 times (last best: 77.1247)
[2022-10-22 17:15:26] [valid] Ep. 10 : Up. 25000 : perplexity : 1.9224 : stalled 2 times (last best: 1.83713)
[2022-10-22 17:31:49] [valid] Ep. 10 : Up. 25000 : bleu : 83.9386 : stalled 1 times (last best: 89.3499)
[2022-10-22 17:33:24] [valid] Ep. 12 : Up. 30000 : cross-entropy : 84.0787 : stalled 3 times (last best: 77.1247)
[2022-10-22 17:33:28] [valid] Ep. 12 : Up. 30000 : perplexity : 1.94069 : stalled 3 times (last best: 1.83713)
[2022-10-22 17:49:01] [valid] Ep. 12 : Up. 30000 : bleu : 85.6595 : stalled 2 times (last best: 89.3499)
[2022-10-22 17:50:35] [valid] Ep. 14 : Up. 35000 : cross-entropy : 85.9204 : stalled 4 times (last best: 77.1247)
[2022-10-22 17:50:40] [valid] Ep. 14 : Up. 35000 : perplexity : 1.96908 : stalled 4 times (last best: 1.83713)
[2022-10-22 18:10:21] [valid] Ep. 14 : Up. 35000 : bleu : 71.2703 : stalled 3 times (last best: 89.3499)
[2022-10-22 18:11:56] [valid] Ep. 16 : Up. 40000 : cross-entropy : 86.5205 : stalled 5 times (last best: 77.1247)
[2022-10-22 18:12:00] [valid] Ep. 16 : Up. 40000 : perplexity : 1.97842 : stalled 5 times (last best: 1.83713)
[2022-10-22 18:30:10] [valid] Ep. 16 : Up. 40000 : bleu : 78.3775 : stalled 4 times (last best: 89.3499)
[2022-10-22 18:31:44] [valid] Ep. 18 : Up. 45000 : cross-entropy : 87.0469 : stalled 6 times (last best: 77.1247)
[2022-10-22 18:31:49] [valid] Ep. 18 : Up. 45000 : perplexity : 1.98665 : stalled 6 times (last best: 1.83713)
[2022-10-22 18:45:56] [valid] Ep. 18 : Up. 45000 : bleu : 89.4992 : new best
[2022-10-22 18:47:30] [valid] Ep. 20 : Up. 50000 : cross-entropy : 87.7445 : stalled 7 times (last best: 77.1247)
[2022-10-22 18:31:49] [valid] Ep. 18 : Up. 45000 : perplexity : 1.98665 : stalled 6 times (last best: 1.83713)
[2022-10-22 18:45:56] [valid] Ep. 18 : Up. 45000 : bleu : 89.4992 : new best
[2022-10-22 18:47:30] [valid] Ep. 20 : Up. 50000 : cross-entropy : 87.7445 : stalled 7 times (last best: 77.1247)
[2022-10-22 18:47:35] [valid] Ep. 20 : Up. 50000 : perplexity : 1.99761 : stalled 7 times (last best: 1.83713)
[2022-10-22 19:02:34] [valid] Ep. 20 : Up. 50000 : bleu : 89.5234 : new best
[2022-10-22 19:04:09] [valid] Ep. 22 : Up. 55000 : cross-entropy : 88.1542 : stalled 8 times (last best: 77.1247)
[2022-10-22 19:04:13] [valid] Ep. 22 : Up. 55000 : perplexity : 2.00407 : stalled 8 times (last best: 1.83713)
[2022-10-22 19:17:05] [valid] Ep. 22 : Up. 55000 : bleu : 89.277 : stalled 1 times (last best: 89.5234)
[2022-10-22 19:18:39] [valid] Ep. 24 : Up. 60000 : cross-entropy : 88.562 : stalled 9 times (last best: 77.1247)
[2022-10-22 19:18:44] [valid] Ep. 24 : Up. 60000 : perplexity : 2.01053 : stalled 9 times (last best: 1.83713)
[2022-10-22 19:34:18] [valid] Ep. 24 : Up. 60000 : bleu : 89.3829 : stalled 2 times (last best: 89.5234)
[2022-10-22 19:35:52] [valid] Ep. 26 : Up. 65000 : cross-entropy : 88.5425 : stalled 10 times (last best: 77.1247)
[2022-10-22 19:35:57] [valid] Ep. 26 : Up. 65000 : perplexity : 2.01022 : stalled 10 times (last best: 1.83713)
[2022-10-22 19:54:50] [valid] Ep. 26 : Up. 65000 : bleu : 84.2957 : stalled 3 times (last best: 89.5234)
```

## Recheck the Data Folder Structure

```
.
|-- edit1
|   |-- original-err
|   |   |-- test.er
|   |   `-- train.er
|   |-- test.cr
|   |-- test.er
|   |-- train-valid
|   |   |-- train.cr
|   |   `-- train.er
|   |-- train.cr
|   |-- train.er
|   |-- valid.cr
|   |-- valid.er
|   `-- vocab
|       |-- all.cr
|       |-- all.er
|       |-- vocab.cr.yml
|       `-- vocab.er.yml
|-- edit2
|   |-- original-err
|   |   |-- test.er
|   |   `-- train.er
|   |   |-- test.er
|   |   `-- train.er
|   |-- test.cr
|   |-- test.er
|   |-- train-valid
|   |   |-- train.cr
|   |   `-- train.er
|   |-- train.cr
|   |-- train.er
|   |-- valid.cr
|   |-- valid.er
|   `-- vocab
|       |-- all.cr
|       |-- all.er
|       |-- vocab.cr.yml
|       `-- vocab.er.yml
|-- folder-struct.txt
`-- manual
    |-- test.cr
    `-- test.er

9 directories, 31 files
```

## Testing with Edit-1 NMT Model

Data folder path: /home/ye/exp/kh-spell/transformer/char-final  
Preparing test-eval-best.sh bash sript ...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliate Professor, CADT, Cambodia
## for NMT Experiments for Khmer Spelling Checking with NMT Model
## preparing to run with edit-distance 1 model
## used Marian NMT Framework for training
## Last updated: 23 Oct 2022

data_path="/home/ye/exp/kh-spell/transformer/char-final/edit1";
src="er"; tgt="cr";

marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml \
--devices 0 --output hyp.best.manual.${tgt} < /home/ye/exp/kh-spell/transformer/char-final/manual/test.${src};
echo "Evaluation with hyp.best.manual.${tgt}, Transformer sent, edit1 model:" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl /home/ye/exp/kh-spell/transformer/char-final/manual/test.${tgt} \
< ./hyp.best.manual.${tgt} >> eval-best-result.txt;

echo "=" >> eval-best-result.txt;

marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml \
--devices 0 --output hyp.best.edit1.${tgt} < ${data_path}/test.${src};
echo "Evaluation with hyp.best.edit1.${tgt}, Transformer sent, edit1 model:" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl ${data_path}/test.${tgt} < ./hyp.best.edit1.${tgt} >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl ${data_path}/test.${tgt} < ./hyp.best.edit1.${tgt} >> eval-best-result.txt;

echo "=" >> eval-best-result.txt;

marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml \
--devices 0 --output hyp.best.edit2.${tgt} < /home/ye/exp/kh-spell/transformer/char-final/edit2/test.${src};
echo "Evaluation with hyp.best.edit2.${tgt}, Transformer sent, edit1 model:" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl /home/ye/exp/kh-spell/transformer/char-final/edit2/test.${tgt} \
< ./hyp.best.edit2.${tgt} >> eval-best-result.txt;
```

Running testing ...  

```
[2022-10-23 02:09:28] Best translation 4918 : អ ្ វ ី ដ ែ ល ជ ា ក ា រ ព េ ញ ន ិ យ ម ន ៅ ក ្ ន ុ ង ស ម ្ ល ៀ ក ប ំ ព ា ក ់ រ ប ស ់ ប ុ រ ស ? អ វ ្ ី ដ ែ ល ា ក ា រ ព េ ញ ន ិ យ ម ន ៅ ក ្ ន ុ ង ស ម ្ ល ៀ ក ប ំ ព ា ក ់ រ ប ស ់ ប ុ រ ស ?
[2022-10-23 02:09:28] Best translation 4919 : ខ ្ ញ ុ ំ ច ង ់ ក ុ ម ្ ម ៉ ង ់ អ ា ហ ា រ ព េ ល ព ្ រ ឹ ក ស ំ រ ា ប ់  ្ ង ៃ ស ្ អ ែ ក ខ ្ ញ ុ ំ ច ់ ក ុ ម ្ ម ៉ ង ់ អ ា ហ ា រ ព េ ល ព ្ រ ឹ ក ស ំ រ ា ប ់ ្ ង ៃ ស ្ អ ែ ក
[2022-10-23 02:09:29] Best translation 4920 : ខ ្ ញ ុ ំ ម ិ ន ប ា ន ហ ៅ ល េ ខ ន េ ះ ទ េ ខ ្ ញ ុ ំ ម ិ ន ប ា ន ហ ៅ ល េ ខ ន េ ះ េ េ
[2022-10-23 02:09:29] Best translation 4921 : ក ្ រ ព ើ ថ ា “ ន ៅ ! ព ុ ំ ទ ា ន ់ ស ្ ម ើ ច ង ម ុ ន ន ោ ះ ទ េ ” R ។  ្ រ ព ើ ថ ា “ ន ៅ ! ព ុ ំ ទ ា ន ់ ម ស ្ ម ើ ច ង ម ុ ន ន ោ ះ ទ េ ” R ។
[2022-10-23 02:09:29] Best translation 4922 : ត ើ ន ៅ ហ ា វ ៉ ៃ ម ៉ ោ ង ជ ា ថ ្ ង ៃ អ ្ វ ី ? ត ើ ន ៅ ហ ៉ វ ៉ ៃ ម ៉ ោ ង ជ ា ថ                                                                                                               ្                                                                                                                     ្ ង ៃ អ ្ វ ី ? ្
[2022-10-23 02:09:29] Best translation 4923 : ច ំ ណ ែ ក ព ្ រ ះ ន ា ង វ ិ ញ ម ិ ន ម ា ន ព ្ រ ះ ស ុ វ ណ ្ ណ ី ស ូ ម ្ ប ី ម ួ យ ម                                                                                                           ៉                                                                                                                     ៉ ា ត ់ ន ិ ង ម ា ន ព ្ រ ះ ភ ក ្ ត រ ភ ិ ត ភ ័ យ ជ ា ខ ្ ល ា ំ ង ច ំ ណ ែ ក ព ្ រ ះ ន ា ង វ ិ ញ ម ិ ន ម ា ន ព ្ រ ះ  ុ វ ណ ្ ណ ី ស ម ្ ប ូ ី ម ួ យ ម ៉ ា ត ់ ន ិ ង ម ា ន ព ្ រ ះ ភ ក ្ ត រ ភ ិ ត ភ ័ យ ជ ា ខ ្ ល ី ា ង
[2022-10-23 02:09:29] Total time: 977.98775s wall
It is not advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.

real    38m57.998s
user    38m51.370s
sys     0m11.418s
root@2541295674c9:/home/ye/exp/kh-spell/transformer/model.transformer.sent.edit1# time ./test-eval-best.sh
```

Results are as follows:  

```
root@2541295674c9:/home/ye/exp/kh-spell/transformer/model.transformer.sent.edit1# cat eval-best-result.txt
Evaluation with hyp.best.manual.cr, Transformer sent, edit1 model:
BLEU = 77.47, 99.5/96.5/93.2/90.0 (BP=0.818, ratio=0.833, hyp_len=442201, ref_len=531058)
==========
Evaluation with hyp.best.edit1.cr, Transformer sent, edit1 model:
BLEU = 90.27, 95.4/94.4/93.9/93.6 (BP=0.957, ratio=0.958, hyp_len=576401, ref_len=601627)
==========
Evaluation with hyp.best.edit2.cr, Transformer sent, edit1 model:
BLEU = 89.95, 97.0/96.2/95.8/95.5 (BP=0.936, ratio=0.938, hyp_len=564081, ref_len=601640)
root@2541295674c9:/home/ye/exp/kh-spell/transformer/model.transformer.sent.edit1#
```

## Preparing a Bash Script for Edit-2 Model 

Training script is as follows:  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliate Professor, IDRI, CADT, Cambodia
## Experiments for Khmer Spelling Correction with NMT model, Sentence Level Experiment 1
## Training with Edit Distance 2
## Last updated: 23 Oct 2022

mkdir model.transformer.sent.edit2;

marian \
    --model model.transformer.sent.edit2/model.npz --type transformer \
    --train-sets char-final/edit2/train.er char-final/edit2/train.cr \
    --max-length 300 \
    --vocabs char-final/edit2/vocab/vocab.er.yml char-final/edit2/vocab/vocab.cr.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets char-final/edit2/valid.er char-final/edit2/valid.cr \
    --valid-translation-output model.transformer.sent.edit2/valid.er-cr.output --quiet-translation \
    --valid-mini-batch 64 \
    --beam-size 6 --normalize 0.6 \
    --log model.transformer.sent.edit2/train.log --valid-log model.transformer.sent.edit2/valid.log \
    --enc-depth 2 --dec-depth 2 \
    --transformer-heads 8 \
    --transformer-postprocess-emb d \
    --transformer-postprocess dan \
    --transformer-dropout 0.3 --label-smoothing 0.1 \
    --learn-rate 0.0003 --lr-warmup 0 --lr-decay-inv-sqrt 16000 --lr-report \
    --clip-norm 5 \
    --tied-embeddings \
    --devices 0 --sync-sgd --seed 1111 \
    --exponential-smoothing \
    --dump-config > model.transformer.sent.edit2/config.yml

time marian -c model.transformer.sent.edit2/config.yml  2>&1 | tee transformer.sent.edit2.log
```

## Training Edit-2 Model 

start training Edit-2 model ...  

```
root@e69e52f4554e:/home/ye/exp/kh-spell/transformer# ./transformer.sent.edit2.sh
...
...
...
[2022-10-23 07:07:32] Ep. 25 : Up. 64500 : Sen. 70,046 : Cost 0.85009700 * 1,252,575 @ 1,529 after 161,199,345 : Time 8.63s : 145184.49 words/s : gNorm 0.1438 : L.r. 1.4942e-04
[2022-10-23 07:07:33] Seen 72,097 samples
[2022-10-23 07:07:33] Starting data epoch 26 in logical epoch 26
[2022-10-23 07:07:33] [data] Shuffling data
[2022-10-23 07:07:33] [data] Done reading 80,000 sentences
[2022-10-23 07:07:33] [data] Done shuffling 80,000 sentences to temp files
[2022-10-23 07:07:41] Ep. 26 : Up. 65000 : Sen. 11,967 : Cost 0.85020041 * 1,250,798 @ 2,485 after 162,450,143 : Time 8.86s : 141109.38 words/s : gNorm 0.1253 : L.r. 1.4884e-04
[2022-10-23 07:07:41] Saving model weights and runtime parameters to model.transformer.sent.edit2/model.iter65000.npz
[2022-10-23 07:07:41] Saving model weights and runtime parameters to model.transformer.sent.edit2/model.npz
[2022-10-23 07:07:41] Saving Adam parameters
[2022-10-23 07:07:41] [training] Saving training checkpoint to model.transformer.sent.edit2/model.npz and model.transformer.sent.edit2/model.npz.optimizer.npz
[2022-10-23 07:07:48] [valid] Ep. 26 : Up. 65000 : cross-entropy : 84.9929 : stalled 10 times (last best: 71.2531)
[2022-10-23 07:07:52] [valid] Ep. 26 : Up. 65000 : perplexity : 1.95465 : stalled 10 times (last best: 1.75394)
[2022-10-23 07:31:53] [valid] Ep. 26 : Up. 65000 : bleu : 66.6193 : stalled 10 times (last best: 88.3613)
[2022-10-23 07:31:53] Training finished
[2022-10-23 07:31:53] Saving model weights and runtime parameters to model.transformer.sent.edit2/model.npz
[2022-10-23 07:31:53] Saving Adam parameters
[2022-10-23 07:31:54] [training] Saving training checkpoint to model.transformer.sent.edit2/model.npz and model.transformer.sent.edit2/model.npz.optimizer.npz

real    272m34.139s
user    266m16.627s
sys     6m32.492s
```

## Preparing a Testing Bash Script

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliate Professor, CADT, Cambodia
## for NMT Experiments for Khmer Spelling Checking with NMT Model
## preparing to run with edit-distance 1 model
## used Marian NMT Framework for training
## Last updated: 23 Oct 2022
data_path="/home/ye/exp/kh-spell/transformer/char-final/edit2";
src="er"; tgt="cr";

marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml \
--devices 0 --output hyp.best.manual.${tgt} < /home/ye/exp/kh-spell/transformer/char-final/manual/test.${src};
echo "Evaluation with hyp.best.manual.${tgt}, Transformer sent, edit2 model:" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl /home/ye/exp/kh-spell/transformer/char-final/manual/test.${tgt} \
< ./hyp.best.manual.${tgt} >> eval-best-result.txt;

echo "=" >> eval-best-result.txt;

marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml \
--devices 0 --output hyp.best.edit1.${tgt} < /home/ye/exp/kh-spell/transformer/char-final/edit1/test.${src};
echo "Evaluation with hyp.best.edit1.${tgt}, Transformer sent, edit2 model:" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl /home/ye/exp/kh-spell/transformer/char-final/edit1/test.${tgt} < ./hyp.best.edit1.>

echo "=" >> eval-best-result.txt;

marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml \
--devices 0 --output hyp.best.edit2.${tgt} < ${data_path}/test.${src};
echo "Evaluation with hyp.best.edit2.${tgt}, Transformer sent, edit2 model:" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl ${data_path}/test.${tgt} < ./hyp.best.edit2.${tgt} >> eval-best-result.txt;
```

## Results with Edit-2 Model  

```
ye@lst-gpu-3090:~/exp/kh-spell/transformer/model.transformer.sent.edit2$ cat eval-best-result.txt
Evaluation with hyp.best.manual.cr, Transformer sent, edit2 model:
BLEU = 77.51, 99.4/96.4/93.1/89.9 (BP=0.819, ratio=0.834, hyp_len=442668, ref_len=531058)
==========
Evaluation with hyp.best.edit1.cr, Transformer sent, edit2 model:
BLEU = 88.88, 90.2/89.1/88.3/87.9 (BP=1.000, ratio=1.023, hyp_len=615576, ref_len=601627)
==========
Evaluation with hyp.best.edit2.cr, Transformer sent, edit2 model:
BLEU = 87.14, 88.6/87.4/86.6/86.0 (BP=1.000, ratio=1.046, hyp_len=629305, ref_len=601640)
```

## Recheck the Data

Date: 22 Dec 2022  
After I run Seq2Seq Models for journal paper writing, I noticed that there is an encoding error on our "word level data" as follows:  

```
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt# head -n3 *.cr
==> test.cr <==
� � � � � � � � � � � � � � � � � � � � �
� � � � � � � � � � � � � � � � � � � � � � � �
� � � � � � � � � � � �

==> train.cr <==
� � � � � � � � � � � � � � �
� � � � � � � � � � � � � � �
� � � � � � � � � � � � � � � � � �

==> valid.cr <==
� � � � � � � � � � � � � � � � � � � � � � � � � � � � � �
� � � � � � � � � � � � � � � � � � � � � � � �
� � � � � � � � � � � � � � � � � � � � � � � �
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt#
```

```
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/edit1# head -n3 *
==> test.cr <==
� � � � � � � � � � � � � � � � � �
� � � � � � � � �
� � � � � � � � � � � � � � � � � �

==> test.er <==
 � � � � � � � � � � � � � � � � � �
 � � � � � � � � �
 � � � � � � � � � � � � � � � � � �
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/edit1#
```

```
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/edit2# head -3 *
==> test.cr <==
� � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � �
� � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � �
� � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � �

==> test.er <==
 � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � �
 � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � �
 � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � � �
                                                               root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/edit2#
```

Vocab file also:  

```
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/vocab# head all.cr
� � � � � � � � � � � � � � �
� � � � � � � � � � � � � � �
� � � � � � � � � � � � � � � � � �
� � � � � �
� � � � � � � � � � � � � � � � � � � � �
� � � � � � � � � � � � � � � � � �
� � � � � � � � � � � �
� � � � � �
� � � � � � � � �
� � � � � �
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/vocab# head all.er
� � � � � � � � � � � � � � � � � �
� � � � � � � � � � � � � � �
� � � � � � � � �
� � � � � � � � � � � � � � �
� � � � � � � � � � � � � � � � � �
� � � � � � � � � � � �
� � � � � � � � � � � � � � �
� � � � � �
� � � � � � � � �
� � �
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/vocab#
```

Unsugmented data looks OK:  

```
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/no-segment# head -n2 *.er
==> test.er <==
រុស្សស៊ី
បប៉ុនហ្នឹង

==> train.er <==
ក្រោយយ
កំបត់

==> valid.er <==
 ក្ហហមឆឆ្ិន
 គន្ថនចនរា
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/no-segment# head -n 2 *.cr
==> test.cr <==
រុស្សស៊ី
បប៉ុណ្នឹង

==> train.cr <==
ក្រោយ
កំបុត

==> valid.cr <==
ក្រហមឆ្អិន
គន្ថចរនា
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/no-segment#
```

check for unsugmented edit1:  

```
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/no-segment/edit1# head -n3 *
==> test.cr <==
ក្រសារ
វិត
ក្របែល

==> test.er <==
 កករសារ
 វតត
 ក្ របែល
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/no-segment/edit1#
```

checked for edit2 data:  

```
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/no-segment/edit2# head -n3 *
==> test.cr <==
បញ្ហាផ្ទៃក្នុង
ច្រុងមិនឡើង
ផលិតផលចេញពីទឹកដោះគោ

==> test.er <==
 បនញហ្ាផ្ទៃក្នុង
 ចររ្ុងមិនឡើងិ
 ផលិផតផលចេញពីលទឹកដោះគោ
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/no-segment/edit2#
```

check unsegmented vocab file:  

```
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/no-segment/vocab# head *
==> vocab.cr.yml <==
ក្រោយ
កំបុត
អអ៊ីចឹង
ទៅ
សម្រាប់
ម្ល៉េះ
ស្មើ
ក៏
 ចុយ
ក៏

 ==> vocab.er.yml <==
ក្រោយយ
កំបត់
ចឹង
ទទ៊ទ៊៊៊ៅ
សំរាប់
ម៉េស
ស្មើេ
ក៍
 ចិយ
ក
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/no-segment/vocab#
```

The problem is because of sed command based character segmentation shell script. I haven't check the current machine environmental setting ...  

```
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/char-segment# ./char-segmentation.sh ./tmp.txt
� � � � � � � � � � � � � � � � � � � � �
� � � � � � � � � � � � � � � � � � � � � � � �
� � � � � � � � � � � �
� � � � � � � � � � � � � � �
� � � � � � � � � � � �
� � � � � � � � � � � � � � � � � �
� � � � � � � � � � � �
� � � � � � � � � � � � � � �
� � � � � � � � � � � � � � � � � � � � � � � �
� � � � � � � � � � � � � � � � � � � � �
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/char-segment#
```

When I checked with another shell script, it is also not working:  

```
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/char-segment# cat print-char.sh
#!/bin/bash

# for printing character by character
# Written by Ye Kyaw Thu, LST Lab., NECTEC, Thailand
# How to run: ./print-char.sh <input-filename>

inputFile=$1;

while read -n1 char;
do
   echo $char;
done < $inputFile
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/char-segment#
```               
                 
**I am running NMT models under container env that cause the encoding input/output errors.  
And thus, if I quit the container environment and run under my home folder looks OK as follows:  

```
ye@lst-gpu-3090:~/char-segment$ ./char-segmentation.sh ./tmp.txt
រ ុ ស ្ ស ៊ ី
ប ៉ ុ ណ ្ ន ឹ ង
រ ប ស ់
ឆ ្ ក ួ ត
អ ្ វ ី
ស ា ម ញ ្ ញ
អ ្ វ ី
ខ ្ ទ ើ យ
ឧ ប ត ្ ថ ម ្ ភ
ន ិ ស ្ ស ិ ត
ye@lst-gpu-3090:~/char-segment$
```

## Character Segmentation

I need to do character segmentation again (i.e. not under container env) and then train Transformer model for dictionary again.  
1st things 1st, the followings are making character segmentation process log:  


### character segmentation for original dictionary (i.e. word level) data 

```
ye@lst-gpu-3090:~/char-segment$ ./char-segmentation.sh ./train.cr > train.cr.char
ye@lst-gpu-3090:~/char-segment$ ./char-segmentation.sh ./train.er > train.er.char
ye@lst-gpu-3090:~/char-segment$ ./char-segmentation.sh ./valid.cr > valid.cr.char
ye@lst-gpu-3090:~/char-segment$ ./char-segmentation.sh ./valid.er > valid.er.char
ye@lst-gpu-3090:~/char-segment$ ./char-segmentation.sh ./test.cr > test.cr.char
ye@lst-gpu-3090:~/char-segment$ ./char-segmentation.sh ./test.er > test.er.char
```

check the char files:  

```
ye@lst-gpu-3090:~/char-segment$ head -n 3 ./*.char
==> ./test.cr.char <==
រ ុ ស ្ ស ៊ ី
ប ៉ ុ ណ ្ ន ឹ ង
រ ប ស ់

==> ./test.er.char <==
រ ុ ស ្ ស ៊ ី
ប ៉ ុ ន ហ ្ ន ឹ ង
ផ ស ់

==> ./train.cr.char <==
ក ្ រ ោ យ
ក ំ ប ុ ត
អ ៊ ី ច ឹ ង

==> ./train.er.char <==
ក ្ រ ោ យ យ
ក ំ ប ត ់
ច ឹ ង

==> ./valid.cr.char <==
ក ្ រ ហ ម ឆ ្ អ ិ ន
គ ន ្ ថ ច រ ន ា
ស ា ស ន ិ ក ជ ន

==> ./valid.er.char <==
 ក ្ ហ ហ ម ឆ ្ ិ ន
 គ ន ្ ថ ន ច ន រ ា
 ា ស ស ិ ន ិ ក ជ ន
ye@lst-gpu-3090:~/char-segment$
```

I need to make space cleaning also:  

```
ye@lst-gpu-3090:~/char-segment$ perl ./clean-space.pl ./train.cr.char > ./train.cr.char.clean
ye@lst-gpu-3090:~/char-segment$ perl ./clean-space.pl ./train.er.char > ./train.er.char.clean
ye@lst-gpu-3090:~/char-segment$ perl ./clean-space.pl ./valid.cr.char > ./valid.cr.char.clean
ye@lst-gpu-3090:~/char-segment$ perl ./clean-space.pl ./valid.er.char > ./valid.er.char.clean
ye@lst-gpu-3090:~/char-segment$ perl ./clean-space.pl ./test.cr.char > ./test.cr.char.clean
ye@lst-gpu-3090:~/char-segment$ perl ./clean-space.pl ./test.er.char > ./test.er.char.clean
```

check the cleaned files:  

```
ye@lst-gpu-3090:~/char-segment$ head -n3 *.clean
==> test.cr.char.clean <==
រ ុ ស ្ ស ៊ ី
ប ៉ ុ ណ ្ ន ឹ ង
រ ប ស ់

==> test.er.char.clean <==
រ ុ ស ្ ស ៊ ី
ប ៉ ុ ន ហ ្ ន ឹ ង
ផ ស ់

==> train.cr.char.clean <==
ក ្ រ ោ យ
ក ំ ប ុ ត
អ ៊ ី ច ឹ ង

==> train.er.char.clean <==
ក ្ រ ោ យ យ
ក ំ ប ត ់
ច ឹ ង

==> valid.cr.char.clean <==
ក ្ រ ហ ម ឆ ្ អ ិ ន
គ ន ្ ថ ច រ ន ា
ស ា ស ន ិ ក ជ ន

==> valid.er.char.clean <==
ក ្ ហ ហ ម ឆ ្ ិ ន
គ ន ្ ថ ន ច ន រ ា
ា ស ស ិ ន ិ ក ជ ន
ye@lst-gpu-3090:~/char-segment$
```

file renaming:  

```
ye@lst-gpu-3090:~/char-segment$ mv test.cr.char.clean test.cr
ye@lst-gpu-3090:~/char-segment$ mv test.er.char.clean test.er
ye@lst-gpu-3090:~/char-segment$ mv train.cr.char.clean train.cr
ye@lst-gpu-3090:~/char-segment$ mv train.er.char.clean train.er
ye@lst-gpu-3090:~/char-segment$ mv valid.cr.char.clean valid.cr
ye@lst-gpu-3090:~/char-segment$ mv valid.er.char.clean valid.er
```

Finished character segmentation for original dictionary data!!!  

### character segmentation for dictionary or word level edit1 data  

```
ye@lst-gpu-3090:~/char-segment/edit1$ ../char-segmentation.sh ./test.cr > test.cr.char
ye@lst-gpu-3090:~/char-segment/edit1$ ../char-segmentation.sh ./test.er > test.er.char
ye@lst-gpu-3090:~/char-segment/edit1$ perl ../clean-space.pl ./test.cr.char > test.cr.char.clean
ye@lst-gpu-3090:~/char-segment/edit1$ perl ../clean-space.pl ./test.er.char > test.er.char.clean
ye@lst-gpu-3090:~/char-segment/edit1$ head -n 3 *.clean
==> test.cr.char.clean <==
ក ្ រ ស ា រ
វ ិ ត
ក ្ រ ប ែ ល

==> test.er.char.clean <==
ក ក រ ស ា រ
វ ត ត
ក ្ រ ប ែ ល
ye@lst-gpu-3090:~/char-segment/edit1$
```

after removing preprocessing files, I did file renaming:  

```
ye@lst-gpu-3090:~/char-segment/edit1$ mv test.cr.char.clean test.cr
ye@lst-gpu-3090:~/char-segment/edit1$ mv test.er.char.clean test.er
ye@lst-gpu-3090:~/char-segment/edit1$ ls
test.cr  test.er
```

### character segmentation for the dictionary or word level edit2 data

```
ye@lst-gpu-3090:~/char-segment/edit2$ ls
test.cr  test.er
ye@lst-gpu-3090:~/char-segment/edit2$ ../char-segmentation.sh ./test.cr > test.cr.char
ye@lst-gpu-3090:~/char-segment/edit2$ ../char-segmentation.sh ./test.er > test.er.char
ye@lst-gpu-3090:~/char-segment/edit2$ perl ../clean-space.pl ./test.cr.char > test.cr.char.clean
ye@lst-gpu-3090:~/char-segment/edit2$ perl ../clean-space.pl ./test.er.char > test.er.char.clean
ye@lst-gpu-3090:~/char-segment/edit2$ head -n 3 ./*.clean
==> ./test.cr.char.clean <==
ប ញ ្ ហ ា ផ ្ ទ ៃ ក ្ ន ុ ង
ច ្ រ ុ ង ម ិ ន ឡ ើ ង
ផ ល ិ ត ផ ល ច េ ញ ព ី ទ ឹ ក ដ ោ ះ គ ោ

==> ./test.er.char.clean <==
ប ន ញ ហ ្ ា ផ ្ ទ ៃ ក ្ ន ុ ង
ច រ ្ ុ ង ម ិ ន ឡ ើ ង ិ
ផ ល ិ ផ ត ផ ល ច េ ញ ព ី ល ទ ឹ ក ដ ោ ះ គ ោ
ye@lst-gpu-3090:~/char-segment/edit2$
```

after removing the preprocessing files, I rename the cleaned files as follows:  

```
ye@lst-gpu-3090:~/char-segment/edit2$ ls
test.cr  test.cr.char  test.cr.char.clean  test.er  test.er.char  test.er.char.clean
ye@lst-gpu-3090:~/char-segment/edit2$ rm *.er
ye@lst-gpu-3090:~/char-segment/edit2$ rm *.cr
ye@lst-gpu-3090:~/char-segment/edit2$ rm *.char
ye@lst-gpu-3090:~/char-segment/edit2$ ls
test.cr.char.clean  test.er.char.clean
ye@lst-gpu-3090:~/char-segment/edit2$ mv test.cr.char.clean test.cr
ye@lst-gpu-3090:~/char-segment/edit2$ mv test.er.char.clean test.er
```

Check the filesize of all prepared data (i.e. character segmented data):  
for original dictionary data:  

```
ye@lst-gpu-3090:~/char-segment$ wc *.cr
   1500    6900   27600 test.cr
 151075 1251873 5007132 train.cr
  16000  140424  561644 valid.cr
 168575 1399197 5596376 total
ye@lst-gpu-3090:~/char-segment$ wc *.er
   1500    6134   24528 test.er
 151042 1239487 4957534 train.er
  15992  139971  559826 valid.er
 168534 1385592 5541888 total
ye@lst-gpu-3090:~/char-segment$
```

filesize info for edit-1 test data:  

```
ye@lst-gpu-3090:~/char-segment$ wc *.cr
   1500    6900   27600 test.cr
 151075 1251873 5007132 train.cr
  16000  140424  561644 valid.cr
 168575 1399197 5596376 total
ye@lst-gpu-3090:~/char-segment$ wc *.er
   1500    6134   24528 test.er
 151042 1239487 4957534 train.er
  15992  139971  559826 valid.er
 168534 1385592 5541888 total
ye@lst-gpu-3090:~/char-segment$
```

filesize info for edit-2 test data:  

```
ye@lst-gpu-3090:~/char-segment/edit2$ wc *
 1000  8964 35854 test.cr
 1000  8880 35518 test.er
 2000 17844 71372 total
ye@lst-gpu-3090:~/char-segment/edit2$
```

### Moved to Transformer Model Training Folder

copied char segmented data from the container root account:  

```
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt# cp -r /home/ye/char-segment/ .
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt# ls
char-segment  no-segment
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt#
```

## Make Vocab Files for Word Level or Dictionary Data

```
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/char-segment# cat train.cr valid.cr test.cr > ./vocab/all.cr
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/char-segment# cat train.er valid.er test.er > ./vocab/all.er
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/char-segment# cd vocab/
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/char-segment/vocab# marian-vocab < all.cr > ./vocab.cr.yml
[2022-12-22 06:24:05] Creating vocabulary...
[2022-12-22 06:24:05] [data] Creating vocabulary stdout from stdin
[2022-12-22 06:24:05] Finished
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/char-segment/vocab# marian-vocab < all.er > ./vocab.er.yml
[2022-12-22 06:24:12] Creating vocabulary...
[2022-12-22 06:24:12] [data] Creating vocabulary stdout from stdin
[2022-12-22 06:24:12] Finished
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/char-segment/vocab#
```

## Training Transformer Model for Word Level or Dictionary Data

I updated the data paths ...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, LST, NECTEC, Thailand
## Experiments for Khmer Spelling Correction with NMT models
## this script is used for character segmented, word level or dictionary data model training
## architecture is transformer model
## Last updated: 22 December 2022

mkdir model.transformer.dict1;

marian \
    --model model.transformer.dict1/model.npz --type transformer \
    --train-sets 4nmt/char-segment/train.er 4nmt/char-segment/train.cr \
    --max-length 100 \
    --vocabs 4nmt/char-segment/vocab/vocab.er.yml 4nmt/char-segment/vocab/vocab.cr.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets 4nmt/char-segment/valid.er 4nmt/char-segment/valid.cr \
    --valid-translation-output model.transformer.dict1/valid.er-cr.output --quiet-translation \
    --valid-mini-batch 64 \
    --beam-size 6 --normalize 0.6 \
    --log model.transformer.dict1/train.log --valid-log model.transformer.dict1/valid.log \
    --enc-depth 2 --dec-depth 2 \
    --transformer-heads 8 \
    --transformer-postprocess-emb d \
    --transformer-postprocess dan \
    --transformer-dropout 0.3 --label-smoothing 0.1 \
    --learn-rate 0.0003 --lr-warmup 0 --lr-decay-inv-sqrt 16000 --lr-report \
    --clip-norm 5 \
    --tied-embeddings \
    --devices 0 --sync-sgd --seed 1111 \
    --exponential-smoothing \
    --dump-config > model.transformer.dict1/config.yml

time marian -c model.transformer.dict1/config.yml  2>&1 | tee transformer.dict1.log 

```

After checking the GPU status, I trained as follows:  

```
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer# ./transformer.dict1.sh | tee transformer.dict1.2ndtime.log
...
...
...
[2022-12-22 06:28:33] [memory] Extending reserved space to 1024 MB (device gpu0)
[2022-12-22 06:28:33] [comm] Using NCCL 2.8.3 for GPU communication
[2022-12-22 06:28:33] [comm] Using global sharding
[2022-12-22 06:28:33] [comm] NCCLCommunicators constructed successfully
[2022-12-22 06:28:33] [training] Using 1 GPUs
[2022-12-22 06:28:33] [logits] Applying loss function for 1 factor(s)
[2022-12-22 06:28:33] [memory] Reserving 56 MB, device gpu0
[2022-12-22 06:28:33] [gpu] 16-bit TensorCores enabled for float32 matrix operations
[2022-12-22 06:28:33] [memory] Reserving 56 MB, device gpu0
[2022-12-22 06:28:34] [batching] Done. Typical MB size is 3,134 target words
[2022-12-22 06:28:34] [memory] Extending reserved space to 1024 MB (device gpu0)
[2022-12-22 06:28:34] [comm] Using NCCL 2.8.3 for GPU communication
[2022-12-22 06:28:34] [comm] Using global sharding
[2022-12-22 06:28:34] [comm] NCCLCommunicators constructed successfully
[2022-12-22 06:28:34] [training] Using 1 GPUs
[2022-12-22 06:28:34] Training started
[2022-12-22 06:28:34] [data] Shuffling data
[2022-12-22 06:28:34] Error: Not all input files have the same number of lines
[2022-12-22 06:28:34] Error: Aborted from void marian::data::Corpus::shuffleData(const std::vector<std::__cxx11::basic_string<char> >&) in /temp/marian/src/data/corpus.cpp:241

[CALL STACK]
[0x56185c1c281a]    marian::data::Corpus::  shuffleData  (std::vector<std::__cxx11::basic_string<char,std::char_traits<char>,std::allocator<char>>,std::allocator<std::__cxx11::basic_string<char,std::char_traits<char>,std::allocator<char>>>> const&) + 0x17ea
[0x56185c09bed1]    marian::Train<marian::SyncGraphGroup>::  run  ()   + 0x1251
[0x56185bfca347]    mainTrainer  (int,  char**)                        + 0x147
[0x7f5e59fd5d90]                                                       + 0x29d90
[0x7f5e59fd5e40]    __libc_start_main                                  + 0x80
[0x56185bfc3995]    _start                                             + 0x25
```

I got above error ...   
I think because of this error message "Not all input files have the same number of lines"    

## Character Segmentation Again

```
ye@lst-gpu-3090:~/no-segment$ ./char-segmentation.sh ./train.cr > train.cr.char
ye@lst-gpu-3090:~/no-segment$ head -n3 ./train.cr.char
ក ្ រ ោ យ
ក ំ ប ុ ត
អ ៊ ី ច ឹ ង
ye@lst-gpu-3090:~/no-segment$ ./char-segmentation.sh ./train.er > train.er.char
ye@lst-gpu-3090:~/no-segment$ ./char-segmentation.sh ./valid.cr > valid.cr.char
ye@lst-gpu-3090:~/no-segment$ ./char-segmentation.sh ./valid.er > valid.er.char
ye@lst-gpu-3090:~/no-segment$ ./char-segmentation.sh ./test.cr > test.cr.char
ye@lst-gpu-3090:~/no-segment$ ./char-segmentation.sh ./test.er > test.er.char
ye@lst-gpu-3090:~/no-segment$ wc *.char
    1500     6900    29100 test.cr.char
    1500     6134    26028 test.er.char
  151075  1251873  5158211 train.cr.char
  151075  1239487  5242134 train.er.char
   16000   140424   577644 valid.cr.char
   16000   139971   591826 valid.er.char
  337150  2784789 11624943 total
```

```
ye@lst-gpu-3090:~/no-segment$ head -n 3 *.cr
==> test.cr <==
រ ុ ស ្ ស ៊ ី
ប ៉ ុ ណ ្ ន ឹ ង
រ ប ស ់

==> train.cr <==
ក ្ រ ោ យ
ក ំ ប ុ ត
អ ៊ ី ច ឹ ង

==> valid.cr <==
ក ្ រ ហ ម ឆ ្ អ ិ ន
គ ន ្ ថ ច រ ន ា
ស ា ស ន ិ ក ជ ន
ye@lst-gpu-3090:~/no-segment$ head -n 3 *.er
==> test.er <==
រ ុ ស ្ ស ៊ ី
ប ៉ ុ ន ហ ្ ន ឹ ង
ផ ស ់

==> train.er <==
ក ្ រ ោ យ យ
ក ំ ប ត ់
ច ឹ ង

==> valid.er <==
 ក ្ ហ ហ ម ឆ ្ ិ ន
 គ ន ្ ថ ន ច ន រ ា
 ា ស ស ិ ន ិ ក ជ ន
ye@lst-gpu-3090:~/no-segment$
```

for edit1  

```
ye@lst-gpu-3090:~/no-segment/edit1$ head -n 3 *
==> test.cr <==
ក ្ រ ស ា រ
វ ិ ត
ក ្ រ ប ែ ល

==> test.er <==
ក ក រ ស ា រ
វ ត ត
ក ្ រ ប ែ ល
ye@lst-gpu-3090:~/no-segment/edit1$
```

for edit2

```
ye@lst-gpu-3090:~/no-segment/edit2$ wc *
 1000  8964 35854 test.cr
 1000  8880 35518 test.er
 2000 17844 71372 total
ye@lst-gpu-3090:~/no-segment/edit2$ head -n 3 *
==> test.cr <==
ប ញ ្ ហ ា ផ ្ ទ ៃ ក ្ ន ុ ង
ច ្ រ ុ ង ម ិ ន ឡ ើ ង
ផ ល ិ ត ផ ល ច េ ញ ព ី ទ ឹ ក ដ ោ ះ គ ោ

==> test.er <==
ប ន ញ ហ ្ ា ផ ្ ទ ៃ ក ្ ន ុ ង
ច រ ្ ុ ង ម ិ ន ឡ ើ ង ិ
ផ ល ិ ផ ត ផ ល ច េ ញ ព ី ល ទ ឹ ក ដ ោ ះ គ ោ
ye@lst-gpu-3090:~/no-segment/edit2$
```

copied to container folder and make vocab as follows:  

```
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/char-segment/vocab# marian-vocab < all.cr > vocab.cr.yml
[2022-12-22 07:43:54] Creating vocabulary...
[2022-12-22 07:43:54] [data] Creating vocabulary stdout from stdin
[2022-12-22 07:43:54] Finished
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/char-segment/vocab# marian-vocab < all.er > vocab.er.yml
[2022-12-22 07:44:01] Creating vocabulary...
[2022-12-22 07:44:01] [data] Creating vocabulary stdout from stdin
[2022-12-22 07:44:01] Finished
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/char-segment/vocab#
```

vocab file info:  

```
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/char-segment/vocab# wc vocab.*
 104  210  832 vocab.cr.yml
 113  228  908 vocab.er.yml
 217  438 1740 total
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer/4nmt/char-segment/vocab#
```


## Training Transformer Model for Dictionary (i.e. word level) Data

start training ...  

```
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer# ./transformer.dict1.sh
...
...
...
[2022-12-22 07:48:50] [logits] Applying loss function for 1 factor(s)
[2022-12-22 07:48:50] [memory] Reserving 56 MB, device gpu0
[2022-12-22 07:48:50] [gpu] 16-bit TensorCores enabled for float32 matrix operations
[2022-12-22 07:48:50] [memory] Reserving 56 MB, device gpu0
[2022-12-22 07:48:51] [batching] Done. Typical MB size is 3,134 target words
[2022-12-22 07:48:51] [memory] Extending reserved space to 1024 MB (device gpu0)
[2022-12-22 07:48:51] [comm] Using NCCL 2.8.3 for GPU communication
[2022-12-22 07:48:51] [comm] Using global sharding
[2022-12-22 07:48:51] [comm] NCCLCommunicators constructed successfully
[2022-12-22 07:48:51] [training] Using 1 GPUs
[2022-12-22 07:48:51] Training started
[2022-12-22 07:48:51] [data] Shuffling data
[2022-12-22 07:48:51] [data] Done reading 151,075 sentences
[2022-12-22 07:48:51] [data] Done shuffling 151,075 sentences to temp files
[2022-12-22 07:48:51] [training] Batches are processed as 1 process(es) x 1 devices/process
[2022-12-22 07:48:51] [memory] Reserving 56 MB, device gpu0
[2022-12-22 07:48:51] [memory] Reserving 56 MB, device gpu0
[2022-12-22 07:48:51] Parameter type float32, optimization type float32, casting types false
[2022-12-22 07:48:51] Allocating memory for general optimizer shards
[2022-12-22 07:48:51] [memory] Reserving 56 MB, device gpu0
[2022-12-22 07:48:51] Allocating memory for Adam-specific shards
[2022-12-22 07:48:51] [memory] Reserving 113 MB, device gpu0
[2022-12-22 07:48:59] Ep. 1 : Up. 500 : Sen. 112,814 : Cost 1.98056638 * 1,053,097 @ 2,664 after 1,053,097 : Time 7.84s : 134373.04 words/s : gNorm 1.2921 : L.r. 3.0000e-04
[2022-12-22 07:49:02] Seen 151,075 samples
[2022-12-22 07:49:02] Starting data epoch 2 in logical epoch 2
[2022-12-22 07:49:02] [data] Shuffling data
[2022-12-22 07:49:02] [data] Done reading 151,075 sentences
[2022-12-22 07:49:02] [data] Done shuffling 151,075 sentences to temp files
[2022-12-22 07:49:07] Ep. 2 : Up. 1000 : Sen. 74,740 : Cost 1.40057039 * 1,046,129 @ 1,382 after 2,099,226 : Time 7.77s : 134716.12 words/s : gNorm 0.8533 : L.r. 3.0000e-04
...
...
...
[2022-12-22 08:10:15] [data] Shuffling data
[2022-12-22 08:10:15] [data] Done reading 151,075 sentences
[2022-12-22 08:10:15] [data] Done shuffling 151,075 sentences to temp files
[2022-12-22 08:10:18] Ep. 111 : Up. 74000 : Sen. 47,840 : Cost 0.84302610 * 1,045,712 @ 2,052 after 154,769,004 : Time 7.94s : 131667.92 words/s : gNorm 0.4355 : L.r. 1.3950e-04
[2022-12-22 08:10:25] Seen 151,075 samples
[2022-12-22 08:10:25] Starting data epoch 112 in logical epoch 112
[2022-12-22 08:10:25] [data] Shuffling data
[2022-12-22 08:10:25] [data] Done reading 151,075 sentences
[2022-12-22 08:10:26] [data] Done shuffling 151,075 sentences to temp files
[2022-12-22 08:10:26] Ep. 112 : Up. 74500 : Sen. 9,788 : Cost 0.84251571 * 1,048,834 @ 1,527 after 155,817,838 : Time 7.94s : 132075.48 words/s : gNorm 0.4170 : L.r. 1.3903e-04
[2022-12-22 08:10:34] Ep. 112 : Up. 75000 : Sen. 122,448 : Cost 0.84183943 * 1,048,840 @ 1,991 after 156,866,678 : Time 7.72s : 135833.76 words/s : gNorm 0.4380 : L.r. 1.3856e-04
[2022-12-22 08:10:34] Saving model weights and runtime parameters to model.transformer.dict1/model.iter75000.npz
[2022-12-22 08:10:34] Saving model weights and runtime parameters to model.transformer.dict1/model.npz
[2022-12-22 08:10:35] Saving Adam parameters
[2022-12-22 08:10:35] [training] Saving training checkpoint to model.transformer.dict1/model.npz and model.transformer.dict1/model.npz.optimizer.npz
[2022-12-22 08:10:37] [valid] Ep. 112 : Up. 75000 : cross-entropy : 4.21014 : stalled 10 times (last best: 3.81616)
[2022-12-22 08:10:38] [valid] Ep. 112 : Up. 75000 : perplexity : 1.53824 : stalled 10 times (last best: 1.47748)
[2022-12-22 08:10:43] [valid] Ep. 112 : Up. 75000 : bleu : 81.0422 : stalled 1 times (last best: 81.0566)
[2022-12-22 08:10:43] Training finished
[2022-12-22 08:10:43] Saving model weights and runtime parameters to model.transformer.dict1/model.npz
[2022-12-22 08:10:44] Saving Adam parameters
[2022-12-22 08:10:44] [training] Saving training checkpoint to model.transformer.dict1/model.npz and model.transformer.dict1/model.npz.optimizer.npz

real    21m55.733s
user    22m49.127s
sys     0m55.830s
root@41bd19a2fd56:/home/ye/exp/kh-spell/transformer#
```

## Testing on Transformer Dictionary Model

copied old shell test-eval script to current Transformer model folder:  

```
root@36ae92f960d5:/home/ye/exp/kh-spell/transformer# cp ./error-data/model.transformer.dict1/test-eval-best.sh ./model.transformer.dict1/
root@36ae92f960d5:/home/ye/exp/kh-spell/transformer#
```

preparing a shell script for testing/evaluation ... 

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments for Myanmar language sentence segmentation
## used Marian NMT Framework for training
## Last updated: 22 December 2022

data_path="/home/ye/exp/kh-spell/transformer/4nmt/char-segment/";
src="er"; tgt="cr";

marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml --devices 0 --output>
echo "Evaluation with hyp.best.manual.${tgt}, Transformer dictionary model (2dn time running):" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl ${data_path}/test.${tgt} < ./hyp.best.manual.${tgt} >> eval-best-result.txt;

echo "=" >> eval-best-result.txt;

marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml --devices 0 --output>
echo "Evaluation with hyp.best.edit1.${tgt}, Transformer dictionary model (2nd time running):" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl ${data_path}/edit1/test.${tgt} < ./hyp.best.edit1.${tgt} >> eval-best-result.txt;

echo "=" >> eval-best-result.txt;

marian-decoder -m ./model.npz -v ${data_path}/vocab/vocab.${src}.yml ${data_path}/vocab/vocab.${tgt}.yml --devices 0 --output>
echo "Evaluation with hyp.best.edit2.${tgt}, Transformer dictionary model (2nd time running):" >> eval-best-result.txt;
perl /home/ye/tool/multi-bleu.perl ${data_path}/edit2/test.${tgt} < ./hyp.best.edit2.${tgt} >> eval-best-result.txt;
```

testing/evaluation ...   

```
root@0d441b235700:/home/ye/exp/kh-spell/transformer/model.transformer.dict1# ./test-eval-best.sh | tee ./test.log
...
...
...
[2022-12-22 11:08:50] Best translation 978 : ច ង ្ អ ា ម
[2022-12-22 11:08:50] Best translation 979 : ផ ្ ល ូ វ ប ែ វ ក ា ប ួ ន
[2022-12-22 11:08:50] Best translation 980 : ដ ា ក ់ ស ំ ញ ៉ ែ
[2022-12-22 11:08:50] Best translation 981 : ជ ក ្ ម េ ង
[2022-12-22 11:08:50] Best translation 982 : យ ុ ត ្ ត វ ា ទ ី
[2022-12-22 11:08:50] Best translation 983 : ដ ា ក ់ ថ ្ ន ា ំ ខ ្ ល ា ំ ង
[2022-12-22 11:08:50] Best translation 984 : ស ូ ម ៉ ា
[2022-12-22 11:08:50] Best translation 985 : ភ ្ ញ ច ់
[2022-12-22 11:08:50] Best translation 986 : ន ិ យ ា យ ប ៉ ប ៉ ា ច ់
[2022-12-22 11:08:50] Best translation 987 : ក ្ ត ឿ ង ស ញ ្ ញ ី
[2022-12-22 11:08:50] Best translation 988 : ច ំ ទ ែ ង
[2022-12-22 11:08:50] Best translation 989 : ល ល ា ម
[2022-12-22 11:08:50] Best translation 990 : ប ច ្ ជ ិ ម យ ា ម
[2022-12-22 11:08:50] Best translation 991 : ល ែ ង ខ ្ ម ៅ
[2022-12-22 11:08:50] Best translation 992 : អ ា ហ ា រ ប ្ រ អ ប ់
[2022-12-22 11:08:50] Best translation 993 : រ ូ ប ព ូ ហ ្ ម
[2022-12-22 11:08:50] Best translation 994 : អ ហ ិ ត ក ៈ
[2022-12-22 11:08:51] Best translation 995 : ស ្ រ ម ក
[2022-12-22 11:08:51] Best translation 996 : ប ៉ ប ៉ ិ ក ប ៉ ប ា ក ់
[2022-12-22 11:08:51] Best translation 997 : ក ែ វ វ ែ ន ត ា
[2022-12-22 11:08:51] Best translation 998 : ឧ ប ្ ប ត ្ ត ិ ភ ូ ម ិ
[2022-12-22 11:08:51] Best translation 999 : ឡ េ ស ៊ ូ
[2022-12-22 11:08:51] Total time: 9.22031s wall

real    0m9.521s
user    0m8.612s
sys     0m0.936s
It is not advisable to publish scores from multi-bleu.perl.  The scores depend on your tokenizer, which is unlikely to be reproducible from your paper or consistent across research groups.  Instead you should detokenize then use mteval-v14.pl, which has a standard tokenization.  Scores from multi-bleu.perl can still be used for internal purposes when you have a consistent tokenizer.
```

check the results:  

```
root@0d441b235700:/home/ye/exp/kh-spell/transformer/model.transformer.dict1# cat eval-best-result.txt
Evaluation with hyp.best.manual.cr, Transformer dictionary model (2dn time running):
BLEU = 85.90, 93.0/87.6/84.1/80.3 (BP=0.997, ratio=0.997, hyp_len=6880, ref_len=6900)
==========
Evaluation with hyp.best.edit1.cr, Transformer dictionary model (2nd time running):
BLEU = 90.19, 96.5/91.6/88.4/85.8 (BP=0.997, ratio=0.997, hyp_len=8822, ref_len=8851)
==========
Evaluation with hyp.best.edit2.cr, Transformer dictionary model (2nd time running):
BLEU = 79.94, 93.5/83.7/77.7/73.0 (BP=0.979, ratio=0.980, hyp_len=8781, ref_len=8964)
root@0d441b235700:/home/ye/exp/kh-spell/transformer/model.transformer.dict1#
```

## Result Summary

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

```

```

```
