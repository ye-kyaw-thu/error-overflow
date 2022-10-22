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

```

```

```

```
