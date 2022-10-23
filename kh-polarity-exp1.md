# Khmer Polarity Classification Experiment-1

## Checking on Manually Created Polarity Corpus

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/rerun/805-chk$ perl ../cut-column.pl ./805.txt 1 > 805.col1.txt
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/rerun/805-chk$ perl ../cut-column.pl ./805.txt 2 > 805.col2.txt
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/rerun/805-chk$ perl ../cut-column.pl ./805.txt 3 > 805.col3.txt
Use of uninitialized value $col3 in substitution (s///) at ../cut-column.pl line 35, <$inputFILE> line 168.
Use of uninitialized value $col3 in concatenation (.) or string at ../cut-column.pl line 36, <$inputFILE> line 168.
Use of uninitialized value $col3 in substitution (s///) at ../cut-column.pl line 35, <$inputFILE> line 217.
Use of uninitialized value $col3 in concatenation (.) or string at ../cut-column.pl line 36, <$inputFILE> line 217.
Use of uninitialized value $col3 in substitution (s///) at ../cut-column.pl line 35, <$inputFILE> line 222.
Use of uninitialized value $col3 in concatenation (.) or string at ../cut-column.pl line 36, <$inputFILE> line 222.
```

## Cleaned Data Information

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final$ ls700.txt  805.txt  8.5k.txt
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final$ cat 8.5k.txt 700.txt 805.txt > ./kh-polar.txt
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final$ wc ./kh-polar.txt 
  10015  101462 5705194 ./kh-polar.txt
```

## Shuffle the Corpus

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final$ shuf kh-polar.txt > kh-polar.txt.shuf
```

Checked the content ...  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final$ head ./kh-polar.txt.shuf 
បារមី​មិន​ដល់ កុំ​លេង។​ ||| បារមី​មិន​ដល់ ||| negative
ពុកម្តាយឬអាណាព្យាបាលយើងពួកគាត់ក៏កាន់តែចម្រើនវ័យទៅជាចាស់ទៅៗបន្តិចម្តងៗ ក្នុងនាមយើងជាកូនពិតប្រាកដណាស់ថាមានក្តីស្រឡាញ់ទៅលើពួកគាត់ដែលបានចិញ្ចឹមបីបាច់យើងតាំងពីតូចរហូតដល់ពេញវ័យ ||| ក្តីស្រឡាញ់ ||| positive
រដ្ឋាភិបាល​ កំពុង​រៀបចំ​សៀវភៅ​ណែនាំ​អំពី​លទ្ធកម្ម​របស់​ភាព​ជា​ដៃគូ​រវាង​វិស័យ​ឯកជន​ និង​សារ​ធារ​ណៈ​ ដែល​ពេល​នេះ​សៀវភៅ​នេះ​នៅ​ជា​ឯកសារ​ព្រាង​នៅឡើយ​។ ||| ​រៀបចំ ||| neutral
គេមើលទៅហាក់ដូចជាគ្រាំគ្រាខ្លាំងណាស់។ ||| គ្រាំគ្រាខ្លាំងណាស់ ||| negative
កន្លងមកទៀត៥ផែនដី រហូតមកដល់រាជព្រះបាទសេណករាជ ប្រទេសខូចរបស់វិសេសទាំង ៥ ប្រការគឺ ព្រះកែវមរកតមួយ ព្រះត្រៃបិដក ជាមង្គលព្រះនគរមួយ គ្រឿងព្រះបញ្ចក្សេត្រ ២១ មុខ ជាសិរីសួស្ដីព្រះនគរមួយ ព្រះរាជគ្រូបុរោហិតទាំង៧នាក់ សម្រាប់ប្រក់ព្រំព្រះនគរ ជម្រះឧត្បាទមួយ សម្ដេចព្រះឥន្ទ្រគោរពការហោរា ជាភ្នែក ជាត្រចៀក ព្រះនគរមួយ។ ||| សិរីសួស្ដី ||| positive
ដូច្នេះហើយ បញ្ហាហ្នឹង វាជា​កត្តាសំខាន់មួយដែរ ពីនយោបាយកម្ពុជា ក្នុងការផ្ទេរអំណាចហ្នឹង។​ ||| វាជា​កត្តាសំខាន់ ||| positive 
មិនមែនជាបញ្ហានយោបាយ ហើយក៏មិនមែនជារឿងសន្តិសុខដែរ តែវីរុសកូវីដបានវាយលុករដ្ឋមន្រ្តីការបរទេសវៀតណាម បង្ខំឲ្យគាត់ចូលរួមប្រជុំតាមអនឡាញពីក្នុងបន្ទប់សណ្ឋាគារសូហ្វីតែលក្បែរផ្សារអ៊ីអន១ ដែលជាកន្លែងប្រជុំនេះតែម្ដង។ ||| បង្ខំ ||| negative
លោក Koh Kok Meng ថ្លែងថា «​ខ្ញុំ​សូម​អរគុណ​ដល់​បុគ្គលិក​ទាំងអស់​, នេះ​គឺជា​មោទន​​ភាព​មួយ​សម្រាប់​ពួកយើង ដែលជា​បុគ្គលិក​​ដា​ណន់ A Proud Danoner!»​។​ ||| ខ្ញុំ​សូម​អរគុណ​ដល់​បុគ្គលិក​ទាំងអស់/​មោទន​​ភាព​ ||| positive 
ផែនទីនេះហើយដែលកម្ពុជា យកធ្វើជាផែនទីឧបសម្ព័ន្ធ ក្នុងសំណុំរឿងប្រាសាទព្រះវិហារ នៅតុលាការ ICJ ដែលស្គាល់ជាទូទៅថា ផែនទីឧបសម្ព័ន្ធ១ (Annex I Map) និងជាមូលដ្ឋានច្បាប់មួយយ៉ាងសំខាន់ដែលធ្វើឲ្យកម្ពុជាឈ្នះកី្តនៅឆ្នាំ១៩៦២។ ||| មូលដ្ឋានច្បាប់មួយយ៉ាងសំខាន់/កម្ពុជាឈ្នះកី្ត ||| positive
លោក សួន ឆាន បន្ថែម​ថា កន្លង​មក​នៅ​តំបន់​ពួក​គាត់​រស់នៅ​មិន​ដែល​ទទួល​បាន​ការ​ប្រឹក្សា​ពី​មន្ទីរ​កសិកម្ម​អំពី​របៀប​ចិញ្ចឹម​សត្វ​ឡើយ ដោយ​ពួក​លោក​តែង​រក​ពេទ្យ​សត្វ​ក្នុង​ភូមិ ឬ​ទិញ​ថ្នាំ​មក​ព្យាបាល​គោ​ក្របី​ដោយ​ខ្លួន​ឯង៖ «អា​រឿង​វា​ឈឺ​ជំងឺ​សារ​បង កាល​ពី​ឈឺ​ជំងឺ​សារ​ចាប់​មួយ​មិន​បាច់​ឆ្លង​ទេ​អា​នេះ ចាប់​ក្រោល​ណា ចាប់​ក្រោល​នោះ​តែ​ម្ដង អា​ជំងឺ​សារ​ទឹក​យើង​ហាស។​ ||| មិន​ដែល​ទទួល​បាន​ការ​ប្រឹក្សា​ពី​មន្ទីរ​កសិកម្ម​ ||| negative
```

## Normalization 

For Khmer NLP tasks, I do suggest to make normalization ...  
We used the khnormal.2.py of IDRI, CADT.   
Slight modification of the original normalization code:  
https://github.com/sillsdev/khmer-character-specification/blob/master/python/scripts/khnormal

Run normalization on our polarity corpus as follows:  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final$ python ./khnormal.2.py ./kh-polar.txt.shuf ./kh-polar.txt.shuf.normalized
```

Check the filesize after we did normalization ...  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final$ wc kh-polar.txt.shuf
  10015  101462 5705194 kh-polar.txt.shuf
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final$ wc kh-polar.txt.shuf.normalized 
  10015  101461 5700021 kh-polar.txt.shuf.normalized
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final$
```

## Check the Classes

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final$ cat ./kh-polar.txt.shuf.normalized | grep positive | wc
   5825   61511 3503873
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final$ cat ./kh-polar.txt.shuf.normalized | grep negative | wc
   3244   31588 1794956
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final$ cat ./kh-polar.txt.shuf.normalized | grep neutral | wc
    919    8176  387966
```

Check the total number lines:  

Not equal to 10015 ...  

```
5825+3244+919 = 9988
```

## Fixing the No. of Class Error

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final$ perl ../rerun/cut-column.pl ./kh-polar.txt.shuf.normalized 3 | sort | uniq -c
     20 
      1 ​
      1 negataive
   3199 negative
      2 ​negative
     20 ​ negative
      1 ​​​ negative
      3 negative ​
      1 negative ​​
      8 negative​
      2 negatives
    918 neutral
      1 ​neutral
      1 positiv
   5617 positive
      1 ​positive
     27 ​ positive
      1 ​ ​​positive
      3 ​​ positive
      1 ​​​ positive
     18 positive ​
      4 positive ​​
    138 positive​
      3 positive​ ​
      2 positive​​
      1 positive​​ ​
      1 positiveនិយាយអោយចំគឺពួកគេអាចទទួលបានផលប្រយោជន៍ពីសម្មភាពទាំងនោះ។
      8 positive negative
```

We have to fixed manually.  
For example:  

```
គោលគំនិតរបស់វីដេអូខាងលើគឺចង់ឆ្លុះបញ្ចាំងអំពីភាពខ្វះចន្លោះនៃការគិតរបស់បុគ្គលណាម្នាក់ចំពោះសកម្មភាពណាមួយនៅក្នងជីវិត ដោយពួកគេយល់ឃើញថាទង្វើទាំងនោះ អាចធ្វើអោយគេរីករាយ និងផ្តល់ផលចំណេញដល់រូបគេក្នុងរូបភាពណាមួយ។ |||  ||| positiveនិយាយអោយចំគឺពួកគេអាចទទួលបានផលប្រយោជន៍ពីសម្មភាពទាំងនោះ។ |||  ||| positive

into

គោលគំនិតរបស់វីដេអូខាងលើគឺចង់ឆ្លុះបញ្ចាំងអំពីភាពខ្វះចន្លោះនៃការគិតរបស់បុគ្គលណាម្នាក់ចំពោះសកម្មភាពណាមួយនៅក្នងជីវិត ដោយពួកគេយល់ឃើញថាទង្វើទាំងនោះ អាចធ្វើអោយគេរីករាយ និងផ្តល់ផលចំណេញដល់រូបគេក្នុងរូបភាពណាមួយ។ ||| ភាពខ្វះចន្លោះ ||| negative

និយាយអោយចំគឺពួកគេអាចទទួលបានផលប្រយោជន៍ពីសម្មភាពទាំងនោះ។ ||| ទទួលបានផលប្រយោជន៍ ||| positive
```

After fixing above error, removed shuf.normalized, make normalization on the original file and re-check ...  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final$ perl ../rerun/cut-column.pl ./kh-polar.txt.normalized 3 | sort | uniq -c
     20 
      1 ​
      1 negataive
   3200 negative
      2 ​negative
     20 ​ negative
      1 ​​​ negative
      3 negative ​
      1 negative ​​
      8 negative​
      2 negatives
    918 neutral
      1 ​neutral
      1 positiv
   5618 positive
      1 ​positive
     27 ​ positive
      1 ​ ​​positive
      3 ​​ positive
      1 ​​​ positive
     18 positive ​
      4 positive ​​
    138 positive​
      3 positive​ ​
      2 positive​​
      1 positive​​ ​
      8 positive negative
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final$
```

Above error, I think I can fixed it. first find "|||\s\s" and replaced with "|||\s" and check again. Some more example manual tagging errors for our/your reference:  

```
1227
តំបន់ទេសចរណ៍សំខាន់ៗក្នុងខេត្តនេះមានភាគច្រើនជាទីតាំងប្រវត្តិសាស្តរ ដូចជា ប្រាសាទបុរាណជាដើម ដែលធ្វើឱ្យទេសចរចូលចិត្តមកធ្វើការសិក្សាស្រាវជ្រាវ ព្រមទាំងទទួលនូវអារម្មណ៍បរិសុទ្ធ ពីទេសភាពប្រណីតៗជុំវិញតំបន់ ប្រាសាទបុរាណនោះផងដែរ។ ||| ធ្វើឱ្យទេសចរចូលចិត្ត/ទទួលនូវអារម្មណ៍បរិសុទ្ធ ||| positive negative

1751
បញ្ហាល្អបំផុតដែលត្រូវធ្វើនោះគឺ ត្រូវពិគ្រោះយោបល់ជាមួយគ្រូពេទ្យ និង ទទួលយកនូវវេជ្ជបញ្ជាដើម្បីបន្ថយរមាស់ ទន្ទឹមនឹងនេះ ត្រូវសម្គាល់មើលថាតើវាកើតឡើងនៅពេលណា និង ដោយរបៀបណា ដូចនេះអ្នកអាចបំបាត់ជំងឺរមាស់ចេញពីជីវិតរបស់អ្នកបានហើយ។ ||| ||| positive negative

1802
មិនថាជនជាតិឥណ្ឌា ម៉ាឡេស៊ី ឬចិននោះទេ ម្ហូបមួយចំនួនរបស់ពួកគេ គឺល្បីល្បាញពីធាតុផ្សំដែលផ្ទុកនូវអាហារូបត្ថម្ភជាច្រើន។ ||| ||| positive negative

1869
អង្គការសុខភាពពិភពលោកបានព្យាករណ៍ថាតួលេខនេះនឹងកើនឡើងគួរឱ្យកត់សម្គាល់ក្នុងរយៈពេលប៉ុន្មានឆ្នាំខាងមុខនេះ។ ||| ព្យាករណ៍ ||| positive negative

1949
មនុស្សជាច្រើនបរាជ័យយ៉ាងងាយដោយការចាប់ផ្តើមជាមួយគម្រោងមិនល្អ ហើយក៏ធ្វើអោយយើងមិនបានធ្វើការបានច្រើន ហើយថែមទាំងហត់នឿយពេញមួយថ្ងៃ។ ||| បរាជ័យ/មិនល្អ/មិនបានធ្វើការ/ហត់នឿយ ||| positive negative

1951
កិច្ចការតូចតាច អាចរឹតតែស្មុគស្មាញនៅពេលអារម្មណ៍អ្នកមិននឹងនរ និងមួម៉ៅនៅពេលព្រឹក។ ||| ស្មុគស្មាញ/មួម៉ៅ ||| positive negative

1970
អ្នកស្រាវជ្រាវជាច្រើនរកឃើញថា អ្នកហាត់ប្រាណទៀងទាត់ទទួលបានអត្ថប្រយោជន៍ជាច្រើនចំពោះសុខភាព។ ||| ទទួលបានអត្ថប្រយោជន៍ ||| positive negative
```

Some error are difficult to find/replace with gedit editor and thus, I used perl one liner as follows:  

```
(base) ye@ykt-pro:/media/ye/project1/cadt/student/Sokheang/data/demo2/kh-data/preprocessing/final$ perl -i -p -e "s/positive​/positive/g" ./kh-polar.txt.normalized.c1
```

Now reduced errors as follows:  

```
     20 
   3239 negative
      1 ​​ negative
    920 neutral
   5798 positive
      3 ​ positive
      1 ​ ​​positive
      1 ​​ positive
     17 positive ​
      4 positive 
```

Totally invisible 20 ... what are they?!   


      

## Split Training and Testing 

```

```

perl -i -p -e "s/positive​/positive/g"

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

```

```
