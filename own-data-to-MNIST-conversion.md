## Data Download Path


Data that we used for CADT internship project.
GoogleDrive Link:
https://drive.google.com/drive/folders/1QtAqiLMOWCJig0hMjJmJH99sqzL1DxL5

## Copy Command

```
C:\Users\801680\Downloads>scp -P 2250  -i C:\Users\801680\.ssh\id_rsa-for-cadt-gpu-server Consonants-20230118T112820Z-001.zip yekyaw.thu@103.16.63.233:/home/yekyaw.thu/exp/sl-mnist/preprocess/
Enter passphrase for key 'C:/Users/801680/.ssh/id_rsa-for-cadt-gpu-server':
Consonants-20230118T112820Z-001.zip                                    100%  211MB   4.5MB/s   00:46

C:\Users\801680\Downloads>
```

## Git Clone

```
(base) yekyaw.thu@gpu:~/tool$ git clone https://github.com/Arlen0615/Convert-own-data-to-MNIST-format
Cloning into 'Convert-own-data-to-MNIST-format'...
remote: Enumerating objects: 37, done.
remote: Total 37 (delta 0), reused 0 (delta 0), pack-reused 37
Unpacking objects: 100% (37/37), 36.34 KiB | 323.00 KiB/s, done.
(base) yekyaw.thu@gpu:~/tool$ cd Convert-own-data-to-MNIST-format/
(base) yekyaw.thu@gpu:~/tool/Convert-own-data-to-MNIST-format$ ls
convert_to_mnist_format.py  LICENSE  mnist2  readme  README.md
(base) yekyaw.thu@gpu:~/tool/Convert-own-data-to-MNIST-format$
```

## Unzipping

```
(base) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist/Consonants$ ls
ក  ខ  គ  ឃ  ង  ច  ឆ  ជ  ឈ  ញ  ដ  ឋ  ឌ  ឍ  ណ  ត  ថ  ទ  ធ  ន  ប  ផ  ព  ភ  ម  យ  រ  ល  វ  ស  ហ  ឡ  អ
(base) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist/Consonants$
```

## Library Installation

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist/Consonants$ pip install imageio
Collecting imageio
  Downloading imageio-2.24.0-py3-none-any.whl (3.4 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.4/3.4 MB 5.2 MB/s eta 0:00:00
Requirement already satisfied: pillow>=8.3.2 in /home/yekyaw.thu/.conda/envs/sl-mnist/lib/python3.8/site-packages (from imageio) (9.4.0)
Requirement already satisfied: numpy in /home/yekyaw.thu/.local/lib/python3.8/site-packages (from imageio) (1.24.1)
Installing collected packages: imageio
Successfully installed imageio-2.24.0
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist/Consonants$
```

Note: glob is a part of Python standard library.  
I confirmed as follows:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist/Consonants$ python
Python 3.8.15 (default, Nov 24 2022, 15:19:38)
[GCC 11.2.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import glob
>>>
```

## Conversion into MNIST Format


1st time running got following error:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist/Consonants$ time python /home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format.py kh-sl-mnist-format 10
/home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format.py:192: SyntaxWarning: "is" with a literal. Did you mean "=="?
  if len(argv) is 3:
/home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format.py:194: SyntaxWarning: "is" with a literal. Did you mean "=="?
  elif len(argv) is 4:
Traceback (most recent call last):
  File "/home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format.py", line 215, in <module>
    main(sys.argv)
  File "/home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format.py", line 193, in main
    labelsAndFiles = get_labels_and_files(argv[1])
  File "/home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format.py", line 82, in get_labels_and_files
    subdir = get_subdir(folder)
  File "/home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format.py", line 75, in get_subdir
    listDir.sort()
AttributeError: 'NoneType' object has no attribute 'sort'

real    0m0.120s
user    0m0.414s
sys     0m1.474s
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist/Consonants$
```

Note: the code looks old (last 5 years is the latest updating date)  

## Update the Code

```python
192     if len(argv) == 3:
193         labelsAndFiles = get_labels_and_files(argv[1])
194     elif len(argv) == 4:
195         labelsAndFiles = get_labels_and_files(argv[1], int(argv[3]))
196     random.shuffle(labelsAndFiles)
```

## Run Again

I got following error:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist/Consonants$ time python /home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format2.py kh-sl-mnist-format 10
Traceback (most recent call last):
  File "/home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format2.py", line 215, in <module>
    main(sys.argv)
  File "/home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format2.py", line 193, in main
    labelsAndFiles = get_labels_and_files(argv[1])
  File "/home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format2.py", line 82, in get_labels_and_files
    subdir = get_subdir(folder)
  File "/home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format2.py", line 75, in get_subdir
    listDir.sort()
AttributeError: 'NoneType' object has no attribute 'sort'

real    0m0.119s
user    0m0.445s
sys     0m1.443s
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist/Consonants$
```

Note: I just noticed that "target_folder = your data folder"

## Run Again

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist$ time python /home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format2.py Consonants 10
Traceback (most recent call last):
  File "/home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format2.py", line 215, in <module>
    main(sys.argv)
  File "/home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format2.py", line 198, in main
    trainImagedata, trainLabeldata, testImagedata, testLabeldata = make_arrays(
  File "/home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format2.py", line 115, in make_arrays
    imShape = imageio.imread(labelsAndFiles[0][1]).shape
IndexError: list index out of range

real    0m0.110s
user    0m0.409s
sys     0m1.216s
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist$
```

## Download notMNIST_small Data

for the folder structure confirmation:

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist$ wget http://yaroslavvb.com/upload/notMNIST/notMNIST_small.tar.gz
--2023-01-18 19:11:21--  http://yaroslavvb.com/upload/notMNIST/notMNIST_small.tar.gz
Resolving yaroslavvb.com (yaroslavvb.com)... 129.121.4.193
Connecting to yaroslavvb.com (yaroslavvb.com)|129.121.4.193|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 8458043 (8.1M) [application/x-gzip]
Saving to: ‘notMNIST_small.tar.gz’

notMNIST_small.tar.gz      100%[=====================================>]   8.07M  3.39MB/s    in 2.4s

2023-01-18 19:11:24 (3.39 MB/s) - ‘notMNIST_small.tar.gz’ saved [8458043/8458043]
```

Check the folder structure:  

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist/notMNIST_small$ ls
A  B  C  D  E  F  G  H  I  J
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist/notMNIST_small$ ls ./A/* | head
./A/MDEtMDEtMDAudHRm.png
./A/MDRiXzA4LnR0Zg==.png
./A/MjAwcHJvb2Ztb29uc2hpbmUgcmVtaXgudHRm.png
./A/MlJlYmVsc0RldXgtQmxhY2sub3Rm.png
./A/MlRvb24gU2hhZG93LnR0Zg==.png
./A/MlRvb24yIFNoYWRvdy50dGY=.png
./A/MTAuMTUgU2F0dXJkYXkgTmlnaHQgQlJLLnR0Zg==.png
./A/MTFTMDEgQmxhY2sgVHVlc2RheSBPZmZzZXQudHRm.png
./A/MTggSG9sZXMgQlJLLnR0Zg==.png
./A/MTh0aENlbnR1cnkudHRm.png
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist/notMNIST_small$
```

Check the file format:   

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist/notMNIST_small/J$ file 'SWNvbmUgTFQgUmVndWxhciBJdGFsaWMgT3NGLnR0Zg==.png'
SWNvbmUgTFQgUmVndWxhciBJdGFsaWMgT3NGLnR0Zg==.png: PNG image data, 28 x 28, 8-bit grayscale, non-interlaced
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist/notMNIST_small/J$
```

## Check Our Data

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist/Consonants/ក$ ls
PXL_20220920_072005229.jpg  PXL_20220920_072049953.jpg  PXL_20220920_072938873.jpg
PXL_20220920_072016601.jpg  PXL_20220920_072124546.jpg  PXL_20220920_072953982.jpg
PXL_20220920_072023804.jpg  PXL_20220920_072833131.jpg  PXL_20220920_073056935.jpg
PXL_20220920_072026171.jpg  PXL_20220920_072847356.jpg  PXL_20220920_073105755.jpg
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist/Consonants/ក$
```

## Run Again

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist$ time python /home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format2.py Consonants 10 0
Traceback (most recent call last):
  File "/home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format2.py", line 215, in <module>
    main(sys.argv)
  File "/home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format2.py", line 198, in main
    trainImagedata, trainLabeldata, testImagedata, testLabeldata = make_arrays(
  File "/home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format2.py", line 115, in make_arrays
    imShape = imageio.imread(labelsAndFiles[0][1]).shape
IndexError: list index out of range

real    0m0.124s
user    0m0.441s
sys     0m1.397s
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist$
```

## Googling

The error might be related to JPEG format.  

I updated the code as follows:  

```
 87         for file in os.listdir(dirname):
 88             if (file.endswith('.png') or file.endswith('.jpg')):
```

Reference:  https://github.com/Arlen0615/Convert-own-data-to-MNIST-format/issues/2

## Run Again

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist$ time python /home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format2.py Consonants 10 0
/home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format2.py:115: DeprecationWarning: Starting with ImageIO v3 the behavior of this function will switch to that of iio.v3.imread. To keep the current behavior (and make this warning disappear) use `import imageio.v2 as imageio` or call `imageio.v2.imread` directly.
  imShape = imageio.imread(labelsAndFiles[0][1]).shape
0% complete/home/yekyaw.thu/tool/Convert-own-data-to-MNIST-format/convert_to_mnist_format2.py:130: DeprecationWarning: Starting with ImageIO v3 the behavior of this function will switch to that of iio.v3.imread. To keep the current behavior (and make this warning disappear) use `import imageio.v2 as imageio` or call `imageio.v2.imread` directly.
  image = imageio.imread(filename)
81% complete


real    0m11.641s
user    0m7.992s
sys     0m5.258s
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist$
```

I hope converted well!   


## Check the Converted Files

```
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist/convert_MNIST$ ls -lh *
-rw-r--r-- 1 yekyaw.thu domain users 361M Jan 18 19:31 t10k-images-idx3-ubyte
-rw-r--r-- 1 yekyaw.thu domain users   33 Jan 18 19:31 t10k-labels-idx1-ubyte
-rw-r--r-- 1 yekyaw.thu domain users 3.1G Jan 18 19:31 train-images-idx3-ubyte
-rw-r--r-- 1 yekyaw.thu domain users  227 Jan 18 19:31 train-labels-idx1-ubyte
(sl-mnist) yekyaw.thu@gpu:~/exp/sl-mnist/preprocess/convert-mnist/convert_MNIST$
```

