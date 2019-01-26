
# Error for extracting .tar.gz file

```bash
$ tar -xzvf ./ngramtool-20040530.tar.gz 

gzip: stdin: not in gzip format
tar: Child returned status 1
tar: Error is not recoverable: exiting now
```

# check file type

```bash
$ file ./ngramtool-20040530.tar.gz 
./ngramtool-20040530.tar.gz: POSIX tar archive (GNU)
```

# Solution

$ tar -xvf ./ngramtool-20040530.tar.gz 
ngramtool-20040530/
ngramtool-20040530/src/
ngramtool-20040530/src/Jamfile
ngramtool-20040530/src/extractngram.cpp
ngramtool-20040530/src/extractngram.ggo
ngramtool-20040530/src/extractngram_cmdline.c
ngramtool-20040530/src/extractngram_cmdline.h
ngramtool-20040530/src/iconvert.cpp
...
...
...

