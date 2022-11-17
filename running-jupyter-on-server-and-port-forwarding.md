# Running Jupyter Notebook on Server and Port Forwarding

## Installation of Jupyter Notebook Under the Anaconda Environment

If you haven't install Jupyter Notebook yet ...  

```
(vit) yekyaw.thu@gpu:~$ conda install jupyter
(vit) yekyaw.thu@gpu:~$ conda install -n base nb_conda_kernels
```

## Running Jupyter on Remote Server


```
jupyter notebook --no-browser --port=8080
```

output screen is as follows:  

```
(vit) yekyaw.thu@gpu:~$ jupyter notebook --no-browser --port=8080
[I 13:05:37.316 NotebookApp] Writing notebook server cookie secret to /home/yekyaw.thu/.local/share/jupyter/runtime/notebook_cookie_secret
[W 2022-11-17 13:05:37.699 LabApp] 'port' has moved from NotebookApp to ServerApp. This config will be passed to ServerApp. Be sure to update your config before our next release.
[W 2022-11-17 13:05:37.699 LabApp] 'port' has moved from NotebookApp to ServerApp. This config will be passed to ServerApp. Be sure to update your config before our next release.
[W 2022-11-17 13:05:37.699 LabApp] 'port' has moved from NotebookApp to ServerApp. This config will be passed to ServerApp. Be sure to update your config before our next release.
[I 2022-11-17 13:05:37.708 LabApp] JupyterLab extension loaded from /home/yekyaw.thu/.conda/envs/vit/lib/python3.8/site-packages/jupyterlab
[I 2022-11-17 13:05:37.708 LabApp] JupyterLab application directory is /home/yekyaw.thu/.conda/envs/vit/share/jupyter/lab
[I 13:05:37.713 NotebookApp] Serving notebooks from local directory: /home/yekyaw.thu
[I 13:05:37.713 NotebookApp] Jupyter Notebook 6.5.2 is running at:
[I 13:05:37.713 NotebookApp] http://localhost:8080/?token=e6c91440cde3b109caa2f82912b4fcd177a263ce54123fb3
[I 13:05:37.713 NotebookApp]  or http://127.0.0.1:8080/?token=e6c91440cde3b109caa2f82912b4fcd177a263ce54123fb3
[I 13:05:37.713 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 13:05:37.717 NotebookApp]

    To access the notebook, open this file in a browser:
        file:///home/yekyaw.thu/.local/share/jupyter/runtime/nbserver-215462-open.html
    Or copy and paste one of these URLs:
        http://localhost:8080/?token=e6c91440cde3b109caa2f82912b4fcd177a263ce54123fb3
     or http://127.0.0.1:8080/?token=e6c91440cde3b109caa2f82912b4fcd177a263ce54123fb3
[I 13:11:49.239 NotebookApp] 302 GET /tree (127.0.0.1) 1.220000ms
[W 13:12:35.006 NotebookApp] 401 POST /login?next=%2Ftree (127.0.0.1) 1.550000ms referer=http://localhost:8080/login?next=%2Ftree
[W 13:12:38.577 NotebookApp] 401 POST /login?next=%2Ftree (127.0.0.1) 1.430000ms referer=http://localhost:8080/login?next=%2Ftree
[I 13:13:18.248 NotebookApp] 302 POST /login?next=%2Ftree (127.0.0.1) 1.080000ms
```

Note following information is the token to access from your local machine:    

```
        http://localhost:8080/?token=e6c91440cde3b109caa2f82912b4fcd177a263ce54123fb3
     or http://127.0.0.1:8080/?token=e6c91440cde3b109caa2f82912b4fcd177a263ce54123fb3
```

open a new terminal and run like following command pattern:    

ssh -L 8080:localhost:<PORT> <REMOTE_USER>@<REMOTE_HOST>    
Note: replace the "xxxx" with your server port number and you might not need the "-i" option.    

```
C:\Users\801680>ssh -p xxxx -L localhost:8080:localhost:8080 -i C:\Users\801680\.ssh\id_rsa-for-cadt-gpu-server yekyaw.thu@103.16.63.233   
Enter passphrase for key 'C:\Users\801680\.ssh\id_rsa-for-cadt-gpu-server':
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.4.0-131-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Thu 17 Nov 2022 01:11:12 PM +07

  System load:    8.93              Processes:                587
  Usage of /home: 46.0% of 1.79TB   Users logged in:          1
  Memory usage:   12%               IPv4 address for docker0: 172.17.0.1
  Swap usage:     0%                IPv4 address for enp8s0:  10.5.5.50

 * Strictly confined Kubernetes makes edge and IoT secure. Learn how MicroK8s
   just raised the bar for easy, resilient and secure K8s cluster deployment.

   https://ubuntu.com/engage/secure-kubernetes-at-the-edge

184 updates can be applied immediately.
11 of these updates are standard security updates.
To see these additional updates run: apt list --upgradable

New release '22.04.1 LTS' available.
Run 'do-release-upgrade' to upgrade to it.


Last login: Thu Nov 17 13:08:43 2022 from 172.23.21.121
yekyaw.thu@gpu:~$
```

Access the Jupyter notebook with local browser:    

http://localhost:8080/tree


## Example Screenshots  
  
<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/access-remote-jupyter-notebook-screen1.png" alt="screenshot of accessing Jupyter Notebook from the local machine" width="1200"/>  
</p>  
<div align="center">
  Fig.1 Screenshot of running remote Jupyter notebook on your local machine.     
</div> 

<br />
    
After your create a new notebook ...  
    
<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/access-remote-jupyter-notebook-screen2.png" alt="screenshot of accessing Jupyter Notebook from the local machine" width="1500"/>  
</p>  
<div align="center">
  Fig.2 Screenshot of running remote Jupyter notebook. Running "nvidia-smi" command for checking number of GPU on the server.   
</div> 

<br />   
    

## Reference

1. https://learn.g2.com/port-forwarding
2. https://docs.anaconda.com/anaconda/user-guide/tasks/remote-jupyter-notebook/
3. https://towardsdatascience.com/remote-computing-with-jupyter-notebooks-5b2860f761e8

