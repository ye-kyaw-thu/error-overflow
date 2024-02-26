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

fst, fsa ပုံတွေကို ထုတ်ဖို့အတွက်က graphviz library က လိုအပ်တယ်။ အရင်ဆုံး pip နဲ့ပဲ အဆင်ပြေမလားလို့ install လုပ်ကြည့်ခဲ့တယ်။  

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

pip နဲ့ installation လုပ်တဲ့အခါမှာ အထက်မှာ မြင်ခဲ့ရတဲ့အတိုင်းပဲ ဘာ error မှ မပြခဲ့ပေမဲ့ တကယ်တမ်း python code ကို run တဲ့အခါမှာ dot ဖိုင် မထုတ်ပေးနိုင်ခဲ့ ...  

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

pip နဲ့ အဆင်မပြေတာနဲ့ source ကိုပဲ download လုပ်ယူပြီး၊ source ကနေပဲ အောက်ပါအတိုင်း installation လုပ်ခဲ့တယ်။  
--prefix ထည့်ရတာက လက်ရှိ သုံးနေတဲ့ linux server မှာက sudo right မရှိလို့ ...  

```
ye@lst-gpu-server-197:~/ye/tool/graphviz-10.0.1/bin$ ./configure --prefix=$HOME/ye/tool/graphviz-10.0.1
make
make install

ye@lst-gpu-server-197:~/ye/tool/graphviz-10.0.1/bin$ nano ../../../../.bashrc

export PATH=/home/ye/ye/tool/graphviz-10.0.1/bin;$PATH;
```

## Test Run

အရင်ဆုံး example program နံပါတ် ၂ ကို run ကြည့်ခဲ့တယ်။  

ye@lst-gpu-server-197:~/ye/exp/kaldifst$ cat string2fst.py  

```python
#!/usr/bin/env python3

import graphviz

import kaldifst


def main():
    s = """
        0 1 a x 0.5
        0 1 b y 1.5
        1 2 c z 2.5
        2 3.5
    """
    isym = kaldifst.SymbolTable.from_str(
        """
        a 1
        b 2
        c 3
    """
    )

    osym = kaldifst.SymbolTable.from_str(
        """
        x 1
        y 2
        z 3
    """
    )

    fst = kaldifst.compile(
        s=s,
        acceptor=False,
        isymbols=isym,
        osymbols=osym,
        keep_isymbols=True,
        keep_osymbols=True,
    )
    fst.write("binary-2.fst")

    fst_dot = kaldifst.draw(fst, acceptor=False, portrait=True)
    source = graphviz.Source(fst_dot)
    source.render(outfile="quick-start-2.svg")


if __name__ == "__main__":
    main()
```

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

ye@lst-gpu-server-197:~/ye/exp/kaldifst$ cat constructors-and-mutators.py  

```python
#!/usr/bin/env python3

import graphviz

import kaldifst


def main():
    # A vector FST is a general mutable FST
    fst = kaldifst.StdVectorFst()

    # Adds state 0 to the initially empty FST and make it the start state.
    s0 = fst.add_state()  # 1st state will be state 0 (returned by add_state)
    assert s0 == 0
    fst.start = 0  # set the start state to 0

    # Adds two arcs exiting state 0.
    # Arc constructor args: ilabel, olabel, weight, dest state ID.
    fst.add_arc(
        state=0,
        arc=kaldifst.StdArc(ilabel=1, olabel=1, weight=0.5, nextstate=1),
    )

    fst.add_arc(
        state=0,
        arc=kaldifst.StdArc(ilabel=2, olabel=2, weight=1.5, nextstate=1),
    )

    # Adds state 1 and its arc.
    fst.add_state()
    fst.add_arc(
        state=1,
        arc=kaldifst.StdArc(ilabel=3, olabel=3, weight=2.5, nextstate=2),
    )

    # Adds state 2 and set its final weight.
    fst.add_state()
    fst.set_final(state=2, weight=3.5)  # 1st arg is state ID, 2nd arg weight

    # Add an input symbol table
    isym = kaldifst.SymbolTable()
    isym.add_symbol(symbol="a", key=1)
    isym.add_symbol("b", 2)
    isym.add_symbol("c", 3)
    fst.input_symbols = isym

    # Add an output symbol table
    osym = kaldifst.SymbolTable()
    osym.add_symbol("x", 1)
    osym.add_symbol("y", 2)
    osym.add_symbol("z", 3)
    fst.output_symbols = osym

    # We can save this FST to a file with
    fst.write(filename="binary.fst")

    # We can read it back
    fst2 = kaldifst.StdVectorFst.read("binary.fst")
    print(fst2)
    print(fst2.to_str())

    # Get a dot format of the FST for visualization
    fst_dot = kaldifst.draw(fst, acceptor=False, portrait=True)
    print(fst_dot)
    # You can use
    # https://dreampuf.github.io/GraphvizOnline
    # to visualize it and share the link to others

    # Alternatively, you can use graphviz to visualize it
    source = graphviz.Source(fst_dot)
    source.render(outfile="quick-start.svg")
    # Done. quick-start.svg is the figure we showed at the start of this section


if __name__ == "__main__":
    main()
```

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

ye@lst-gpu-server-197:~/ye/exp/kaldifst$ cat iterating.py  

```python
#!/usr/bin/env python3

import graphviz

import kaldifst


def main():
    fst = kaldifst.StdVectorFst.read("binary.fst")
    for state in kaldifst.StateIterator(fst):
        for arc in kaldifst.ArcIterator(fst, state):

            # Note: We can change the attribute of the arc if we want
            if arc.weight == 0.5:
                arc.weight = 0.6
            elif arc.weight == 1.5:
                arc.weight = 1.8
            elif arc.weight == 2.5:
                arc.weight = 1.25

            print(state, arc)

    fst_dot = kaldifst.draw(fst, acceptor=False, portrait=True)
    source = graphviz.Source(fst_dot)
    source.render(outfile="quick-start-3.svg")


if __name__ == "__main__":
    main()
"""
Output of this file:

0 (ilabel: 1, olabel: 1, weight: 0.6, nextstate: 1)
0 (ilabel: 2, olabel: 2, weight: 1.8, nextstate: 1)
1 (ilabel: 3, olabel: 3, weight: 1.25, nextstate: 2)
"""
```

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

1. https://github.com/k2-fsa/kaldifst
2. https://graphviz.org/download/source/

## To Do

- I plan to do something ... :)  
  

