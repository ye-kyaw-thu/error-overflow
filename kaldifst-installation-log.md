# KaldiFST

## Installation with pip

```
ye@lst-gpu-server-197:~/ye/exp/kaldifst$ pip install --verbose kaldifst
Using pip 24.0 from /home/ye/.local/lib/python3.10/site-packages/pip (python 3.10)
Defaulting to user installation because normal site-packages is not writeable
Collecting kaldifst
  Obtaining dependency information for kaldifst from https://files.pythonhosted.org/packages/2c/0b/dda2084873621bc77041ed7d595af1eb406cba9a178e889b164a77a142c7/kaldifst-1.7.10-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata
  Downloading kaldifst-1.7.10-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (840 bytes)
Downloading kaldifst-1.7.10-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (9.5 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 9.5/9.5 MB 36.7 MB/s eta 0:00:00
Installing collected packages: kaldifst
Successfully installed kaldifst-1.7.10
ye@lst-gpu-server-197:~/ye/exp/kaldifst$
```

## Installation of graphviz

```
ye@lst-gpu-server-197:~/ye/exp/kaldifst$ pip install graphviz
Defaulting to user installation because normal site-packages is not writeable
Collecting graphviz
  Downloading graphviz-0.20.1-py3-none-any.whl.metadata (12 kB)
Downloading graphviz-0.20.1-py3-none-any.whl (47 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 47.0/47.0 kB 1.4 MB/s eta 0:00:00
Installing collected packages: graphviz
Successfully installed graphviz-0.20.1
ye@lst-gpu-server-197:~/ye/exp/kaldifst$
```

## Facing Eror Even I Installed Graphviz

```
ye@lst-gpu-server-197:~/ye/exp/kaldifst$ pip show graphviz
Name: graphviz
Version: 0.20.1
Summary: Simple Python interface for Graphviz
Home-page: https://github.com/xflr6/graphviz
Author: Sebastian Bank
Author-email: sebastian.bank@uni-leipzig.de
License: MIT
Location: /home/ye/.local/lib/python3.10/site-packages
Requires:
Required-by:
ye@lst-gpu-server-197:~/ye/exp/kaldifst$
```

## I Have To Install Graphviz From Source

```
ye@lst-gpu-server-197:~/ye/tool/graphviz-10.0.1/bin$ ./configure --prefix=$HOME/ye/tool/graphviz-10.0.1
make
make install

ye@lst-gpu-server-197:~/ye/tool/graphviz-10.0.1/bin$ nano ../../../../.bashrc

export PATH=/home/ye/ye/tool/graphviz-10.0.1/bin;$PATH;
```

## Test Run

```
ye@lst-gpu-server-197:~/ye/exp/kaldifst$ python3 ./string2fst.py
ye@lst-gpu-server-197:~/ye/exp/kaldifst$ ls
binary-2.fst  note.txt  quick-start-2.gv  quick-start-2.svg  string2fst.py
ye@lst-gpu-server-197:~/ye/exp/kaldifst$

Now OK. I got SVG file.
```

Output:  
<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/quick-start-2.svg" alt="output quick-start-2.svg" width="500"/>  
</p>  
<div align="center">
  Fig.1 quick-start-2.svg  
</div> 

<br />

## Making FST with Constructors and Mutators

```
ye@lst-gpu-server-197:~/ye/exp/kaldifst$ python3 constructors-and-mutators.py
0      1      a      x      0.5
0      1      b      y      1.5
1      2      c      z      2.5
2      3.5

0      1      a      x      0.5
0      1      b      y      1.5
1      2      c      z      2.5
2      3.5

digraph FST {
rankdir = LR;
size = "8.5,11";
center = 1;
orientation = Portrait;
ranksep = "0.4";
nodesep = "0.25";
0 [label = "0", shape = circle, style = bold, fontsize = 14]
        0 -> 1 [label = "a:x/0.5", fontsize = 14];
        0 -> 1 [label = "b:y/1.5", fontsize = 14];
1 [label = "1", shape = circle, style = solid, fontsize = 14]
        1 -> 2 [label = "c:z/2.5", fontsize = 14];
2 [label = "2/3.5", shape = doublecircle, style = solid, fontsize = 14]
}

ye@lst-gpu-server-197:~/ye/exp/kaldifst$
```

Output:  
<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/quick-start-2.svg" alt="output quick-start.svg" width="500"/>  
</p>  
<div align="center">
  Fig.2 quick-start.svg  
</div> 

<br />

## Testing Iterating Code

```
ye@lst-gpu-server-197:~/ye/exp/kaldifst$ python3 ./iterating.py
0 (ilabel: 1, olabel: 1, weight: 0.6, nextstate: 1)
0 (ilabel: 2, olabel: 2, weight: 1.8, nextstate: 1)
1 (ilabel: 3, olabel: 3, weight: 1.25, nextstate: 2)
ye@lst-gpu-server-197:~/ye/exp/kaldifst$
```

Output:  
<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/quick-start-2.svg" alt="output quick-start-3.svg" width="500"/>  
</p>  
<div align="center">
  Fig.3 quick-start-3.svg  
</div> 

<br />

## Reference

https://graphviz.org/download/source/

