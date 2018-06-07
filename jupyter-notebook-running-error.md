Today, I installed caffe and updated some Python libraries ...  
After that, when I run jupyter I got following error:

```bash
(py3.6.2) lar@lar-air:~/ss2018$ jupyter notebook Deep\ Learning\ Notebook.ipynb 
Traceback (most recent call last):
  File "/home/lar/anaconda3/envs/py3.6.2/bin/jupyter-notebook", line 4, in <module>
    import notebook.notebookapp
  File "/home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages/notebook/notebookapp.py", line 78, in <module>
    from .services.kernels.kernelmanager import MappingKernelManager
  File "/home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages/notebook/services/kernels/kernelmanager.py", line 19, in <module>
    from jupyter_client.session import Session
  File "/home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages/jupyter_client/session.py", line 61, in <module>
    from jupyter_client.jsonutil import extract_dates, squash_dates, date_default
  File "/home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages/jupyter_client/jsonutil.py", line 11, in <module>
    from dateutil.parser import parse as _dateutil_parse
  File "/home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages/dateutil/parser.py", line 158
    l.append("%s=%s" % (attr, `value`))
                              ^
SyntaxError: invalid syntax
```

The solution is just install jupyter again:

```bash
(py3.6.2) lar@lar-air:~/ss2018$ pip3 install jupyter
Requirement already satisfied: jupyter in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (1.0.0)
Requirement already satisfied: ipykernel in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from jupyter) (4.8.2)
Requirement already satisfied: ipywidgets in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from jupyter) (7.2.1)
Requirement already satisfied: notebook in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from jupyter) (5.4.1)
Requirement already satisfied: jupyter-console in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from jupyter) (5.2.0)
Requirement already satisfied: nbconvert in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from jupyter) (5.3.1)
Requirement already satisfied: qtconsole in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from jupyter) (4.3.1)
Requirement already satisfied: tornado>=4.0 in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from ipykernel->jupyter) (5.0.2)
Requirement already satisfied: traitlets>=4.1.0 in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from ipykernel->jupyter) (4.3.2)
Requirement already satisfied: jupyter-client in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from ipykernel->jupyter) (5.2.3)
Requirement already satisfied: ipython>=4.0.0 in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from ipykernel->jupyter) (6.4.0)
Requirement already satisfied: widgetsnbextension~=3.2.0 in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from ipywidgets->jupyter) (3.2.1)
Requirement already satisfied: nbformat>=4.2.0 in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from ipywidgets->jupyter) (4.4.0)
Requirement already satisfied: terminado>=0.8.1 in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from notebook->jupyter) (0.8.1)
Requirement already satisfied: jupyter-core>=4.4.0 in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from notebook->jupyter) (4.4.0)
Requirement already satisfied: Send2Trash in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from notebook->jupyter) (1.5.0)
Requirement already satisfied: ipython-genutils in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from notebook->jupyter) (0.2.0)
Requirement already satisfied: jinja2 in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from notebook->jupyter) (2.10)
Requirement already satisfied: pygments in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from jupyter-console->jupyter) (2.2.0)
Requirement already satisfied: prompt-toolkit<2.0.0,>=1.0.0 in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from jupyter-console->jupyter) (1.0.15)
Requirement already satisfied: mistune>=0.7.4 in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from nbconvert->jupyter) (0.8.3)
Requirement already satisfied: pandocfilters>=1.4.1 in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from nbconvert->jupyter) (1.4.2)
Requirement already satisfied: bleach in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from nbconvert->jupyter) (1.5.0)
Requirement already satisfied: entrypoints>=0.2.2 in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from nbconvert->jupyter) (0.2.3)
Requirement already satisfied: testpath in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from nbconvert->jupyter) (0.3.1)
Requirement already satisfied: six in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from traitlets>=4.1.0->ipykernel->jupyter) (1.11.0)
Requirement already satisfied: decorator in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from traitlets>=4.1.0->ipykernel->jupyter) (4.3.0)
Collecting python-dateutil>=2.1 (from jupyter-client->ipykernel->jupyter)
  Downloading https://files.pythonhosted.org/packages/cf/f5/af2b09c957ace60dcfac112b669c45c8c97e32f94aa8b56da4c6d1682825/python_dateutil-2.7.3-py2.py3-none-any.whl (211kB)
    100% |████████████████████████████████| 215kB 796kB/s 
Requirement already satisfied: pyzmq>=13 in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from jupyter-client->ipykernel->jupyter) (17.0.0)
Requirement already satisfied: setuptools>=18.5 in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages/setuptools-27.2.0-py3.6.egg (from ipython>=4.0.0->ipykernel->jupyter) (27.2.0)
Requirement already satisfied: jedi>=0.10 in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from ipython>=4.0.0->ipykernel->jupyter) (0.12.0)
Requirement already satisfied: pickleshare in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from ipython>=4.0.0->ipykernel->jupyter) (0.7.4)
Requirement already satisfied: simplegeneric>0.8 in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from ipython>=4.0.0->ipykernel->jupyter) (0.8.1)
Requirement already satisfied: backcall in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from ipython>=4.0.0->ipykernel->jupyter) (0.1.0)
Requirement already satisfied: pexpect in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from ipython>=4.0.0->ipykernel->jupyter) (4.5.0)
Requirement already satisfied: jsonschema!=2.5.0,>=2.4 in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from nbformat>=4.2.0->ipywidgets->jupyter) (2.6.0)
Requirement already satisfied: MarkupSafe>=0.23 in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from jinja2->notebook->jupyter) (1.0)
Requirement already satisfied: wcwidth in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from prompt-toolkit<2.0.0,>=1.0.0->jupyter-console->jupyter) (0.1.7)
Requirement already satisfied: html5lib!=0.9999,!=0.99999,<0.99999999,>=0.999 in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from bleach->nbconvert->jupyter) (0.9999999)
Requirement already satisfied: parso>=0.2.0 in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from jedi>=0.10->ipython>=4.0.0->ipykernel->jupyter) (0.2.0)
Requirement already satisfied: ptyprocess>=0.5 in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (from pexpect->ipython>=4.0.0->ipykernel->jupyter) (0.5.2)
Installing collected packages: python-dateutil
  Found existing installation: python-dateutil 1.5
    Uninstalling python-dateutil-1.5:
      Successfully uninstalled python-dateutil-1.5
Successfully installed python-dateutil-2.7.3
```

Now OK! as follow :)

```bash
(py3.6.2) lar@lar-air:~/ss2018$ jupyter notebook ./Deep\ Learning\ Notebook.ipynb
[I 08:52:25.542 NotebookApp] [nb_conda_kernels] enabled, 9 kernels found
[I 08:52:25.954 NotebookApp] The port 8888 is already in use, trying another port.
[I 08:52:26.480 NotebookApp] [nb_conda] enabled
[I 08:52:26.486 NotebookApp] Serving notebooks from local directory: /home/lar/ss2018
[I 08:52:26.486 NotebookApp] 0 active kernels
[I 08:52:26.486 NotebookApp] The Jupyter Notebook is running at:
[I 08:52:26.487 NotebookApp] http://localhost:8889/?token=f5c053846a8e6f8ca8a772fdb894572c96ebc2676ad49a71
[I 08:52:26.487 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 08:52:26.491 NotebookApp] 
    
    Copy/paste this URL into your browser when you connect for the first time,
    to login with a token:
        http://localhost:8889/?token=f5c053846a8e6f8ca8a772fdb894572c96ebc2676ad49a71
[I 08:52:27.121 NotebookApp] Accepting one-time-token-authenticated connection from 127.0.0.1
[27760:27804:0608/085227.151529:ERROR:browser_gpu_channel_host_factory.cc(120)] Failed to launch GPU process.
Created new window in existing browser session.
[I 08:52:30.491 NotebookApp] Kernel started: b7c4eccb-bc4b-45ac-ae23-a1d8c388c963
[I 08:52:32.187 NotebookApp] Adapting to protocol v5.1 for kernel b7c4eccb-bc4b-45ac-ae23-a1d8c388c963
[I 08:52:35.203 NotebookApp] Starting buffering for b7c4eccb-bc4b-45ac-ae23-a1d8c388c963:8f23d07f45ea44f4b892ecdcbbd80d30
```
