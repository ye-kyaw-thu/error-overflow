# Data Preparation of nl2bash

## Make setup

```
(base) ye@lst-hpc3090:~/exp/nl2bash$ (base) ye@lst-hpc3090:~/exp/nl2bash$ make setup
# Set up nlp tools
tar xf nlp_tools/spellcheck/most_common.tar.xz --directory nlp_tools/spellcheck/
# Install Python packages
pip3 install -r requirements.txt
Collecting nltk==3.4.5 (from -r requirements.txt (line 1))
  Downloading nltk-3.4.5.zip (1.5 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.5/1.5 MB 4.7 MB/s eta 0:00:00
  Preparing metadata (setup.py) ... done
Requirement already satisfied: tqdm>=4.9.0 in /home/ye/miniforge3/lib/python3.10/site-packages (from -r requirements.txt (line 2)) (4.66.2)
Collecting nose>=1.1.2 (from -r requirements.txt (line 3))
  Downloading nose-1.3.7-py3-none-any.whl.metadata (1.7 kB)
Requirement already satisfied: numpy>=1.7 in /home/ye/miniforge3/lib/python3.10/site-packages (from -r requirements.txt (line 4)) (2.1.0)
Requirement already satisfied: scipy>0.13.3 in /home/ye/miniforge3/lib/python3.10/site-packages (from -r requirements.txt (line 5)) (1.14.1)
Requirement already satisfied: six>=1.8 in /home/ye/miniforge3/lib/python3.10/site-packages (from -r requirements.txt (line 6)) (1.16.0)
Collecting matplotlib (from -r requirements.txt (line 8))
  Downloading matplotlib-3.9.2-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (11 kB)
Collecting contourpy>=1.0.1 (from matplotlib->-r requirements.txt (line 8))
  Downloading contourpy-1.3.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (5.4 kB)
Collecting cycler>=0.10 (from matplotlib->-r requirements.txt (line 8))
  Downloading cycler-0.12.1-py3-none-any.whl.metadata (3.8 kB)
Collecting fonttools>=4.22.0 (from matplotlib->-r requirements.txt (line 8))
  Downloading fonttools-4.53.1-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (162 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 162.6/162.6 kB 15.1 MB/s eta 0:00:00
Collecting kiwisolver>=1.3.1 (from matplotlib->-r requirements.txt (line 8))
  Downloading kiwisolver-1.4.7-cp310-cp310-manylinux_2_12_x86_64.manylinux2010_x86_64.whl.metadata (6.3 kB)
Requirement already satisfied: packaging>=20.0 in /home/ye/miniforge3/lib/python3.10/site-packages (from matplotlib->-r requirements.txt (line 8)) (24.0)
Requirement already satisfied: pillow>=8 in /home/ye/miniforge3/lib/python3.10/site-packages (from matplotlib->-r requirements.txt (line 8)) (8.4.0)
Collecting pyparsing>=2.3.1 (from matplotlib->-r requirements.txt (line 8))
  Downloading pyparsing-3.1.4-py3-none-any.whl.metadata (5.1 kB)
Collecting python-dateutil>=2.7 (from matplotlib->-r requirements.txt (line 8))
  Using cached python_dateutil-2.9.0.post0-py2.py3-none-any.whl.metadata (8.4 kB)
Downloading nose-1.3.7-py3-none-any.whl (154 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 154.7/154.7 kB 29.2 MB/s eta 0:00:00
Downloading matplotlib-3.9.2-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (8.3 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 8.3/8.3 MB 81.2 MB/s eta 0:00:00
Downloading contourpy-1.3.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (322 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 322.0/322.0 kB 36.0 MB/s eta 0:00:00
Downloading cycler-0.12.1-py3-none-any.whl (8.3 kB)
Downloading fonttools-4.53.1-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (4.6 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4.6/4.6 MB 75.4 MB/s eta 0:00:00
Downloading kiwisolver-1.4.7-cp310-cp310-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (1.6 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.6/1.6 MB 69.6 MB/s eta 0:00:00
Downloading pyparsing-3.1.4-py3-none-any.whl (104 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 104.1/104.1 kB 15.1 MB/s eta 0:00:00
Using cached python_dateutil-2.9.0.post0-py2.py3-none-any.whl (229 kB)
Building wheels for collected packages: nltk
  Building wheel for nltk (setup.py) ... done
  Created wheel for nltk: filename=nltk-3.4.5-py3-none-any.whl size=1449905 sha256=52a46d34076425ae5b06df071477abdb4be5d8bb1893196ed5962da6f16f74c0
  Stored in directory: /home/ye/.cache/pip/wheels/83/0e/2a/08f80a9e3723178619f265be5170918056411e8d9d8c1bfecc
Successfully built nltk
Installing collected packages: nose, python-dateutil, pyparsing, nltk, kiwisolver, fonttools, cycler, contourpy, matplotlib
Successfully installed contourpy-1.3.0 cycler-0.12.1 fonttools-4.53.1 kiwisolver-1.4.7 matplotlib-3.9.2 nltk-3.4.5 nose-1.3.7 pyparsing-3.1.4 python-dateutil-2.9.0.post0
(base) ye@lst-hpc3090:~/exp/nl2bash$
```

## make data

```
(base) ye@lst-hpc3090:~/exp/nl2bash/scripts$ (base) ye@lst-hpc3090:~/exp/nl2bash/scripts$ make data
# Filter raw parallel corpus and split to train/dev/test
cd ../data/scripts && \
python3 filter_data.py bash && \
python3 split_data.py bash && \
cd ../../scripts
Traceback (most recent call last):
  File "/home/ye/exp/nl2bash/data/scripts/filter_data.py", line 14, in <module>
    from bashlint import bash, data_tools
  File "/home/ye/exp/nl2bash/data/scripts/../../bashlint/__init__.py", line 5, in <module>
    from bashlint import bparser, tokenizer
  File "/home/ye/exp/nl2bash/data/scripts/../../bashlint/bparser.py", line 3, in <module>
    from bashlint import yacc, tokenizer, state, bast, subst, flags, errors, heredoc
  File "/home/ye/exp/nl2bash/data/scripts/../../bashlint/yacc.py", line 93, in <module>
    from bashlint import butils
  File "/home/ye/exp/nl2bash/data/scripts/../../bashlint/butils.py", line 3, in <module>
    class typedset(collections.MutableSet):
                   ^^^^^^^^^^^^^^^^^^^^^^
AttributeError: module 'collections' has no attribute 'MutableSet'
make: *** [Makefile:11: data] Error 1
(base) ye@lst-hpc3090:~/exp/nl2bash/scripts$
```

## Manual splitting

```
(base) ye@lst-hpc3090:~/exp/nl2bash/data$ pip install bashlint
Collecting bashlint
  Downloading bashlint-0.1.1.tar.gz (3.5 kB)
  Preparing metadata (setup.py) ... done
Building wheels for collected packages: bashlint
  Building wheel for bashlint (setup.py) ... done
  Created wheel for bashlint: filename=bashlint-0.1.1-py3-none-any.whl size=3794 sha256=fed37f43145b967110f57022019aafad1dd9ca10626f8b77d85d82a29144cb0e
  Stored in directory: /home/ye/.cache/pip/wheels/17/0e/68/0a3c155d98e037783777c139269e4648f2378b17c84dae9410
Successfully built bashlint
Installing collected packages: bashlint
Successfully installed bashlint-0.1.1
(base) ye@lst-hpc3090:~/exp/nl2bash/data$
```

Change server ...

```
(base) ye@lst-gpu-server-197:~/ye/exp/nl2bash/data$ pip install bashlint
Defaulting to user installation because normal site-packages is not writeable
Collecting bashlint
  Downloading bashlint-0.1.1.tar.gz (3.5 kB)
  Preparing metadata (setup.py) ... done
Building wheels for collected packages: bashlint
  Building wheel for bashlint (setup.py) ... done
  Created wheel for bashlint: filename=bashlint-0.1.1-py3-none-any.whl size=3796 sha256=71528b94983f9aab1871644c485c0f2e1c72a525713e00ad180e2c9297fda0d1
  Stored in directory: /home/ye/.cache/pip/wheels/17/0e/68/0a3c155d98e037783777c139269e4648f2378b17c84dae9410
Successfully built bashlint
Installing collected packages: bashlint
Successfully installed bashlint-0.1.1

[notice] A new release of pip is available: 24.0 -> 24.2
[notice] To update, run: /usr/bin/python3 -m pip install --upgrade pip
(base) ye@lst-gpu-server-197:~/ye/exp/nl2bash/data$
```

Facing error ...  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/nl2bash/data$ which python
/home/ye/anaconda3/envs/py3.8/bin/python
(py3.8) ye@lst-gpu-server-197:~/ye/exp/nl2bash/data$ /home/ye/anaconda3/envs/py3.8/bin/python -m pip install bashlint
Collecting bashlint
  Using cached bashlint-0.1.1.tar.gz (3.5 kB)
  Preparing metadata (setup.py) ... done
Building wheels for collected packages: bashlint
  Building wheel for bashlint (setup.py) ... done
  Created wheel for bashlint: filename=bashlint-0.1.1-py3-none-any.whl size=3793 sha256=e2ed55887835dcd8d43b2a308dd084a6fcf3c265a42d17f44c0fc5581ea8f885
  Stored in directory: /home/ye/.cache/pip/wheels/b1/64/46/b614e212a1452ef98e0ee8891cb45daa575a836065e9f7ea69
Successfully built bashlint
Installing collected packages: bashlint
Successfully installed bashlint-0.1.1
(py3.8) ye@lst-gpu-server-197:~/ye/exp/nl2bash/data$
```

Finally, I can splitted filtered data into train, dev and test as follows:  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/nl2bash/data$ python scripts/split_data.py bash
9507 1042 997
265 pairs moved from dev to train
256 pairs moved from test to train
/home/ye/ye/exp/nl2bash/data/bash/train.nl.filtered saved
/home/ye/ye/exp/nl2bash/data/bash/train.cm.filtered saved
/home/ye/ye/exp/nl2bash/data/bash/dev.nl.filtered saved
/home/ye/ye/exp/nl2bash/data/bash/dev.cm.filtered saved
/home/ye/ye/exp/nl2bash/data/bash/test.nl.filtered saved
/home/ye/ye/exp/nl2bash/data/bash/test.cm.filtered saved
(py3.8) ye@lst-gpu-server-197:~/ye/exp/nl2bash/data$
```

## Check the Splitted Data

train, dev, test ခွဲပြီးထွက်လာတဲ့ filesize ကို ကြည့်ကြည့်တယ်။  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/nl2bash/data/bash$ wc train.*
  10028   77386  436938 train.cm.filtered
  10028  130646  813003 train.nl.filtered
  20056  208032 1249941 total
(py3.8) ye@lst-gpu-server-197:~/ye/exp/nl2bash/data/bash$ wc dev.*
   777   6320  36761 dev.cm.filtered
   777  10059  63811 dev.nl.filtered
  1554  16379 100572 total
(py3.8) ye@lst-gpu-server-197:~/ye/exp/nl2bash/data/bash$ wc test.*
   741   6187  35815 test.cm.filtered
   741  10317  64854 test.nl.filtered
  1482  16504 100669 total
(py3.8) ye@lst-gpu-server-197:~/ye/exp/nl2bash/data/bash$
```

Check nl, test file:  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/nl2bash/data/bash$ head test.nl.filtered
Add "new." to the beginning of the name of "original.filename", renaming it to "new.original.filename".
Add "new." to the beginning of the name of "original.filename", renaming it to "new.original.filename".
Add "prefix_" to every non-blank line in "a.txt"
Add a date time stamp to every line of output in "ping host"
Archive "./dir" to "user@host:/path" via ssh on port 2222 and display progress
Archive "/home/path" to "path" on host "server" showing progress and statistics and remove files in the destination not found in the source
Archive "/local/path/some_file" to "/some/path" on host "server.com" authenticating as user "usr", compress data during transmission, show progress details.
Archive "/top/a/b/c/d" to host "remote" using relative path names
Archive "/usr/local/" to "/BackUp/usr/local/" on host "XXX.XXX.XXX.XXX" via ssh and show progress
Archive "source" to "destination" via ssh with "rwX" permissions
(py3.8) ye@lst-gpu-server-197:~/ye/exp/nl2bash/data/bash$
```

Check command test file:  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/nl2bash/data/bash$ head test.cm.filtered
rename 's/(.*)$/new.$1/' original.filename
rename 's/^/new./' original.filename
nl -s "prefix_" a.txt | cut -c7-
ping host | perl -nle 'print scalar(localtime), " ", $_'
rsync -rvz -e 'ssh -p 2222' --progress ./dir user@host:/path
rsync -a --stats --progress --delete /home/path server:path
rsync -avz --progress local/path/some_file usr@server.com:"/some/path/"
rsync -a --relative /top/a/b/c/d remote:/
rsync --progress -avhe ssh /usr/local/  XXX.XXX.XXX.XXX:/BackUp/usr/local/
rsync -rvz --chmod=ugo=rwX -e ssh source destination
(py3.8) ye@lst-gpu-server-197:~/ye/exp/nl2bash/data/bash$
```

Check nl dev file:  

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/nl2bash/data/bash$ head dev.nl.filtered
Adds execution permissions on a script ./etc/bash_completion within Homebrew home folder path.
Add execute permission to "ComputeDate", "col", and "printdirections" for all users
Add read and execute permission to command "node"
Adjust the timestamp of 'filename' by subtracting 2 hours from it.
Adjust the timestamp of file $filename by subtracting 2 hours from it
Answer "1" repeatedly until "command" exits
Archive "/path/to/application.ini" on host "source_host" to current directory.
Archive "/path/to/sfolder" to "name@remote.server:/path/to/remote/dfolder" preserving hard links and compressing the data during transmission
Archive "foo/bar/baz.c" to "remote:/tmp/" preserving the relative path of "foo/bar/baz.c"
archive all files in a current directory modified in the last 30 days
(py3.8) ye@lst-gpu-server-197:~/ye/exp/nl2bash/data/bash$
```

```
(py3.8) ye@lst-gpu-server-197:~/ye/exp/nl2bash/data/bash$ head dev.cm.filtered
chmod +x $(brew --prefix)/etc/bash_completion
chmod a+x ComputeDate col printdirections
sudo chmod +rx $(which node)
touch -d "$(date -r filename) - 2 hours" filename
touch -d "$(date -r "$filename") - 2 hours" "$filename"
yes 1 | command
rsync -avv source_host:path/to/application.ini ./application.ini
rsync -aHvz /path/to/sfolder name@remote.server:/path/to/remote/dfolder
rsync -avR foo/bar/baz.c remote:/tmp/
tar czvf mytarfile.tgz `find . -mtime -30`
(py3.8) ye@lst-gpu-server-197:~/ye/exp/nl2bash/data/bash$
```

