# Introduction to tldr

for someone who love linux but weak at long-term memory  ...  

## Installation with pip

```
(base) ye@ykt-pro:~$ pip install tldr
Collecting tldr
  Downloading tldr-3.1.0-py3-none-any.whl (11 kB)
Requirement already satisfied: termcolor in ./tool/anaconda3/lib/python3.7/site-packages (from tldr) (1.1.0)
Collecting shtab>=1.3.10
  Downloading shtab-1.6.1-py3-none-any.whl (13 kB)
Requirement already satisfied: colorama in ./tool/anaconda3/lib/python3.7/site-packages (from tldr) (0.4.1)
Installing collected packages: shtab, tldr
Successfully installed shtab-1.6.1 tldr-3.1.0
(base) ye@ykt-pro:~$ 
```

## Testing

```
(base) ye@ykt-pro:~$ tldr tar

  tar

  Archiving utility.
  Often combined with a compression method, such as gzip or bzip2.
  More information: https://www.gnu.org/software/tar.

  - [c]reate an archive and write it to a [f]ile:
    tar cf path/to/target.tar path/to/file1 path/to/file2 ...

  - [c]reate a g[z]ipped archive and write it to a [f]ile:
    tar czf path/to/target.tar.gz path/to/file1 path/to/file2 ...

  - [c]reate a g[z]ipped archive from a directory using relative paths:
    tar czf path/to/target.tar.gz --directory=path/to/directory .

  - E[x]tract a (compressed) archive [f]ile into the current directory [v]erbosely:
    tar xvf path/to/source.tar[.gz|.bz2|.xz]

  - E[x]tract a (compressed) archive [f]ile into the target directory:
    tar xf path/to/source.tar[.gz|.bz2|.xz] --directory=path/to/directory

  - [c]reate a compressed archive and write it to a [f]ile, using [a]rchive suffix to determine the compression program:
    tar caf path/to/target.tar.xz path/to/file1 path/to/file2 ...

  - Lis[t] the contents of a tar [f]ile [v]erbosely:
    tar tvf path/to/source.tar

  - E[x]tract files matching a pattern from an archive [f]ile:
    tar xf path/to/source.tar --wildcards "*.html"

(base) ye@ykt-pro:~$
```

```
(base) ye@ykt-pro:~$ tldr ls

  ls

  List directory contents.
  More information: https://www.gnu.org/software/coreutils/ls.

  - List files one per line:
    ls -1

  - List all files, including hidden files:
    ls -a

  - List all files, with trailing `/` added to directory names:
    ls -F

  - Long format list (permissions, ownership, size, and modification date) of all files:
    ls -la

  - Long format list with size displayed using human-readable units (KiB, MiB, GiB):
    ls -lh

  - Long format list sorted by size (descending):
    ls -lS

  - Long format list of all files, sorted by modification date (oldest first):
    ls -ltr

  - Only list directories:
    ls -d */

(base) ye@ykt-pro:~$
```

```
(base) ye@ykt-pro:~$ tldr top

  top

  Display dynamic real-time information about running processes.
  More information: https://manned.org/top.

  - Start top:
    top

  - Do not show any idle or zombie processes:
    top -i

  - Show only processes owned by given user:
    top -u username

  - Sort processes by a field:
    top -o field_name

  - Show the individual threads of a given process:
    top -Hp process_id

  - Show only the processes with the given PID(s), passed as a comma-separated list. (Normally you wouldn't know PIDs off hand. This example picks the PIDs from the process name):
    top -p $(pgrep -d ',' process_name)

  - Get help about interactive commands:
    ?

(base) ye@ykt-pro:~$
```

```
(base) ye@ykt-pro:~$ tldr ssh

  ssh

  Secure Shell is a protocol used to securely log onto remote systems.
  It can be used for logging or executing commands on a remote server.
  More information: https://man.openbsd.org/ssh.

  - Connect to a remote server:
    ssh username@remote_host

  - Connect to a remote server with a specific identity (private key):
    ssh -i path/to/key_file username@remote_host

  - Connect to a remote server using a specific port:
    ssh username@remote_host -p 2222

  - Run a command on a remote server with a [t]ty allocation allowing interaction with the remote command:
    ssh username@remote_host -t command command_arguments

  - SSH tunneling: Dynamic port forwarding (SOCKS proxy on `localhost:1080`):
    ssh -D 1080 username@remote_host

  - SSH tunneling: Forward a specific port (`localhost:9999` to `example.org:80`) along with disabling pseudo-[T]ty allocation and executio[N] of remote commands:
    ssh -L 9999:example.org:80 -N -T username@remote_host

  - SSH jumping: Connect through a jumphost to a remote server (Multiple jump hops may be specified separated by comma characters):
    ssh -J username@jump_host username@remote_host

  - Agent forwarding: Forward the authentication information to the remote machine (see `man ssh_config` for available options):
    ssh -A username@remote_host

(base) ye@ykt-pro:~$ 
```

## for PDF Book

https://tldr.sh/assets/tldr-book.pdf

