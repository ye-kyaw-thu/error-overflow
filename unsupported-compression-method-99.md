
```
$ unzip ./Repair.zip 
Archive:  ./Repair.zip
   skipping: Repair/error/detail-error-report.txt  unsupported compression method 99
   skipping: Repair/error/fixed-this-error.txt  unsupported compression method 99
   creating: Repair/
   creating: Repair/error/
```

```
$ tree ./Repair
./Repair
└── error

1 directory, 0 files
```

```
$ 7z x -pcorrect-312 ./Repair.zip 

7-Zip [64] 9.20  Copyright (c) 1999-2010 Igor Pavlov  2010-11-18
p7zip Version 9.20 (locale=en_US.utf8,Utf16=on,HugeFiles=on,4 CPUs)

Processing archive: ./Repair.zip

Extracting  Repair
Extracting  Repair/error
Extracting  Repair/error/detail-error-report.txt
Extracting  Repair/error/fixed-this-error.txt

Everything is Ok

Folders: 2
Files: 2
Size:       171975
Compressed: 31534
```
