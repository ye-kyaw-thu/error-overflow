## git clone

```
(base) ye@ykt-pro:~/tool$ git clone https://gitlab.com/kidbright/kbide --recursive
Cloning into 'kbide'...
warning: redirecting to https://gitlab.com/kidbright/kbide.git/
remote: Enumerating objects: 840, done.
remote: Counting objects: 100% (840/840), done.
remote: Compressing objects: 100% (461/461), done.
remote: Total 7343 (delta 403), reused 761 (delta 347), pack-reused 6503
Receiving objects: 100% (7343/7343), 166.69 MiB | 698.00 KiB/s, done.
Resolving deltas: 100% (2695/2695), done.
```

## run npm run build

```
(base) ye@ykt-pro:~/tool$ cd kbide/
(base) ye@ykt-pro:~/tool/kbide$ npm run build

Command 'npm' not found, but can be installed with:

sudo apt install npm
```

## Check nodejs, if not you need to install

```
(base) ye@ykt-pro:~/tool/kbide$ sudo apt install nodejs
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
nodejs is already the newest version (8.10.0~dfsg-2ubuntu0.4).
nodejs set to manually installed.
The following packages were automatically installed and are no longer required:
  audacity-data libarchive-cpio-perl libfile-stripnondeterminism-perl libflac++6v5 libid3tag0 libkf5attica5 libkf5bookmarks-data
  libkf5kdelibs4support-data libkf5parts-data libkf5sane-data libkf5xmlgui-bin libkf5xmlgui-data liblilv-0-0 libmail-sendmail-perl libportsmf0v5
  libserd-0-0 libsord-0-0 libsoundtouch1 libsratom-0-0 libsys-hostname-long-perl libvamp-hostsdk3v5 linux-hwe-5.4-headers-5.4.0-45
  linux-hwe-5.4-headers-5.4.0-47 linux-hwe-5.4-headers-5.4.0-48 linux-hwe-5.4-headers-5.4.0-51 linux-hwe-5.4-headers-5.4.0-52
  linux-hwe-5.4-headers-5.4.0-53 linux-hwe-5.4-headers-5.4.0-56 linux-hwe-5.4-headers-5.4.0-58 po-debconf python-cliapp python-markdown
  python-ttystatus
Use 'sudo apt autoremove' to remove them.
0 upgraded, 0 newly installed, 0 to remove and 73 not upgraded.
```

nojs က လက်ရှိ စက်မှာ ရှိပြီးသား

## install npm

```
(base) ye@ykt-pro:~/tool/kbide$ sudo apt install npm
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  audacity-data libarchive-cpio-perl libfile-stripnondeterminism-perl libflac++6v5 libid3tag0 libkf5attica5 libkf5bookmarks-data
  libkf5kdelibs4support-data libkf5parts-data libkf5sane-data libkf5xmlgui-bin libkf5xmlgui-data liblilv-0-0 libmail-sendmail-perl libportsmf0v5
  libserd-0-0 libsord-0-0 libsoundtouch1 libsratom-0-0 libsys-hostname-long-perl libvamp-hostsdk3v5 linux-hwe-5.4-headers-5.4.0-45
  linux-hwe-5.4-headers-5.4.0-47 linux-hwe-5.4-headers-5.4.0-48 linux-hwe-5.4-headers-5.4.0-51 linux-hwe-5.4-headers-5.4.0-52
  linux-hwe-5.4-headers-5.4.0-53 linux-hwe-5.4-headers-5.4.0-56 linux-hwe-5.4-headers-5.4.0-58 po-debconf python-cliapp python-markdown
  python-ttystatus
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  gyp libjs-async libjs-inherits libjs-node-uuid libjs-underscore libssl1.0-dev libuv1-dev node-abbrev node-ansi node-ansi-color-table node-archy
  node-async node-balanced-match node-block-stream node-brace-expansion node-builtin-modules node-combined-stream node-concat-map node-cookie-jar
  node-delayed-stream node-forever-agent node-form-data node-fs.realpath node-fstream node-fstream-ignore node-github-url-from-git node-glob
  node-graceful-fs node-gyp node-hosted-git-info node-inflight node-inherits node-ini node-is-builtin-module node-isexe node-json-stringify-safe
  node-lockfile node-lru-cache node-mime node-minimatch node-mkdirp node-mute-stream node-node-uuid node-nopt node-normalize-package-data node-npmlog
  node-once node-osenv node-path-is-absolute node-pseudomap node-qs node-read node-read-package-json node-request node-retry node-rimraf node-semver
  node-sha node-slide node-spdx-correct node-spdx-expression-parse node-spdx-license-ids node-tar node-tunnel-agent node-underscore
  node-validate-npm-package-license node-which node-wrappy node-yallist nodejs-dev
Suggested packages:
  node-hawk node-aws-sign node-oauth-sign node-http-signature debhelper
The following packages will be REMOVED:
  libssl-dev
The following NEW packages will be installed:
  gyp libjs-async libjs-inherits libjs-node-uuid libjs-underscore libssl1.0-dev libuv1-dev node-abbrev node-ansi node-ansi-color-table node-archy
  node-async node-balanced-match node-block-stream node-brace-expansion node-builtin-modules node-combined-stream node-concat-map node-cookie-jar
  node-delayed-stream node-forever-agent node-form-data node-fs.realpath node-fstream node-fstream-ignore node-github-url-from-git node-glob
  node-graceful-fs node-gyp node-hosted-git-info node-inflight node-inherits node-ini node-is-builtin-module node-isexe node-json-stringify-safe
  node-lockfile node-lru-cache node-mime node-minimatch node-mkdirp node-mute-stream node-node-uuid node-nopt node-normalize-package-data node-npmlog
  node-once node-osenv node-path-is-absolute node-pseudomap node-qs node-read node-read-package-json node-request node-retry node-rimraf node-semver
  node-sha node-slide node-spdx-correct node-spdx-expression-parse node-spdx-license-ids node-tar node-tunnel-agent node-underscore
  node-validate-npm-package-license node-which node-wrappy node-yallist nodejs-dev npm
0 upgraded, 71 newly installed, 1 to remove and 73 not upgraded.
Need to get 4,177 kB of archives.
After this operation, 15.8 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 gyp all 0.1+20150913git1f374df9-1ubuntu1 [265 kB]
Get:2 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 libjs-async all 0.8.0-3 [25.4 kB]
Get:3 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 libjs-node-uuid all 1.4.7-5 [11.5 kB]
Get:4 http://mm.archive.ubuntu.com/ubuntu bionic/main amd64 libjs-underscore all 1.8.3~dfsg-1 [59.9 kB]
Get:5 http://mm.archive.ubuntu.com/ubuntu bionic-updates/main amd64 libssl1.0-dev amd64 1.0.2n-1ubuntu5.5 [1,366 kB]
Get:6 http://mm.archive.ubuntu.com/ubuntu bionic/main amd64 libuv1-dev amd64 1.18.0-3 [82.0 kB]
Get:7 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-async all 0.8.0-3 [2,840 B]
Get:8 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-builtin-modules all 1.1.1-1 [3,338 B]
Get:9 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-fs.realpath all 1.0.0-1 [5,572 B]
Get:10 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-hosted-git-info all 2.5.0-1 [6,756 B]
Get:11 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-wrappy all 1.0.2-1 [3,162 B]
Get:12 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-once all 1.4.0-2ubuntu1 [3,588 B]
Get:13 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-inflight all 1.0.6-1 [3,382 B]
Get:14 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-is-builtin-module all 1.0.0-1 [2,906 B]
Get:15 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-isexe all 2.0.0-3 [4,376 B]
Get:16 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-node-uuid all 1.4.7-5 [2,844 B]
Get:17 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-path-is-absolute all 1.0.0-1 [3,310 B]
Get:18 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-pseudomap all 1.0.2-1 [3,534 B]
Get:19 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-spdx-license-ids all 1.2.2-1 [4,792 B]
Get:20 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-spdx-correct all 1.0.2-1 [3,718 B]
Get:21 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-spdx-expression-parse all 1.0.4-1 [12.1 kB]
Get:22 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-underscore all 1.8.3~dfsg-1 [3,790 B]
Get:23 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-validate-npm-package-license all 3.0.1-1 [3,488 B]
Get:24 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-yallist all 2.0.0-1 [5,398 B]
Get:25 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 libjs-inherits all 2.0.3-1 [2,792 B]
Get:26 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-abbrev all 1.0.9-1 [3,708 B]
Get:27 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-ansi all 0.3.0-2ubuntu1 [8,720 B]
Get:28 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-ansi-color-table all 1.0.0-1 [4,478 B]
Get:29 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-archy all 1.0.0-1ubuntu1 [4,264 B]
Get:30 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-balanced-match all 0.4.2-1 [4,030 B]
Get:31 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-inherits all 2.0.3-1 [3,092 B]
Get:32 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-block-stream all 0.0.9-1ubuntu1 [4,736 B]
Get:33 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-concat-map all 0.0.1-1 [3,502 B]
Get:34 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-brace-expansion all 1.1.8-1 [5,840 B]
Get:35 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-delayed-stream all 0.0.5-1 [4,750 B]
Get:36 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-combined-stream all 0.0.5-1 [4,958 B]
Get:37 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-cookie-jar all 0.3.1-1 [3,746 B]
Get:38 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-forever-agent all 0.5.1-1 [3,194 B]
Get:39 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-mime all 1.3.4-1 [11.9 kB]
Get:40 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-form-data all 0.1.0-1 [6,412 B]
Get:41 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-minimatch all 3.0.4-3 [13.5 kB]
Get:42 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-glob all 7.1.2-4 [17.7 kB]
Get:43 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-rimraf all 2.6.2-1 [8,152 B]
Get:44 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-mkdirp all 0.5.1-1 [4,848 B]                                                    
Get:45 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-graceful-fs all 4.1.11-1 [10.8 kB]                                              
Get:46 http://mm.archive.ubuntu.com/ubuntu bionic-updates/universe amd64 node-fstream all 1.0.10-1ubuntu0.18.04.1 [18.4 kB]                           
Get:47 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-fstream-ignore all 0.0.6-2 [5,586 B]                                            
Get:48 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-github-url-from-git all 1.4.0-1 [3,782 B]                                       
Get:49 http://mm.archive.ubuntu.com/ubuntu bionic-updates/universe amd64 nodejs-dev amd64 8.10.0~dfsg-2ubuntu0.4 [351 kB]                             
Get:50 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-nopt all 3.0.6-3 [9,572 B]                                                      
Get:51 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-npmlog all 0.0.4-1 [5,844 B]                                                    
Get:52 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-osenv all 0.1.4-1 [4,212 B]                                                     
Get:53 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-tunnel-agent all 0.3.1-1 [4,018 B]                                              
Get:54 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-json-stringify-safe all 5.0.0-1 [3,544 B]                                       
Get:55 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-qs all 2.2.4-1ubuntu1 [7,680 B]                                                 
Get:56 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-request all 2.26.1-1 [14.5 kB]                                                  
Get:57 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-semver all 5.4.1-1 [22.6 kB]                                                    
Get:58 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-tar all 2.2.1-1 [17.7 kB]                                                       
Get:59 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-which all 1.3.0-1 [4,504 B]                                                     
Get:60 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-gyp all 3.6.2-1ubuntu1 [29.4 kB]                                                
Get:61 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-ini all 1.3.4-1 [5,588 B]                                                       
Get:62 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-lockfile all 0.4.1-1 [5,450 B]                                                  
Get:63 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-lru-cache all 4.1.1-1 [8,228 B]                                                 
Get:64 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-mute-stream all 0.0.7-1 [4,372 B]                                               
Get:65 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-normalize-package-data all 2.3.5-2 [10.6 kB]                                    
Get:66 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-read all 1.0.7-1 [4,572 B]                                                      
Get:67 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-read-package-json all 1.2.4-1 [7,780 B]                                         
Get:68 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-retry all 0.10.1-1 [8,016 B]                                                    
Get:69 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-sha all 1.2.3-1 [4,272 B]                                                       
Get:70 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 node-slide all 1.1.6-1 [6,212 B]                                                     
Get:71 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 npm all 3.5.2-0ubuntu4 [1,586 kB]                                                    
Fetched 4,177 kB in 10s (438 kB/s)                                                                                                                    
Extracting templates from packages: 100%
(Reading database ... 532055 files and directories currently installed.)
Removing libssl-dev:amd64 (1.1.1-1ubuntu2.1~18.04.7) ...
Selecting previously unselected package gyp.
(Reading database ... 531939 files and directories currently installed.)
Preparing to unpack .../00-gyp_0.1+20150913git1f374df9-1ubuntu1_all.deb ...
Unpacking gyp (0.1+20150913git1f374df9-1ubuntu1) ...
Selecting previously unselected package libjs-async.
Preparing to unpack .../01-libjs-async_0.8.0-3_all.deb ...
Unpacking libjs-async (0.8.0-3) ...
Selecting previously unselected package libjs-node-uuid.
Preparing to unpack .../02-libjs-node-uuid_1.4.7-5_all.deb ...
Unpacking libjs-node-uuid (1.4.7-5) ...
Selecting previously unselected package libjs-underscore.
Preparing to unpack .../03-libjs-underscore_1.8.3~dfsg-1_all.deb ...
Unpacking libjs-underscore (1.8.3~dfsg-1) ...
Selecting previously unselected package libssl1.0-dev:amd64.
Preparing to unpack .../04-libssl1.0-dev_1.0.2n-1ubuntu5.5_amd64.deb ...
Unpacking libssl1.0-dev:amd64 (1.0.2n-1ubuntu5.5) ...
Selecting previously unselected package libuv1-dev:amd64.
Preparing to unpack .../05-libuv1-dev_1.18.0-3_amd64.deb ...
Unpacking libuv1-dev:amd64 (1.18.0-3) ...
Selecting previously unselected package node-async.
Preparing to unpack .../06-node-async_0.8.0-3_all.deb ...
Unpacking node-async (0.8.0-3) ...
Selecting previously unselected package node-builtin-modules.
Preparing to unpack .../07-node-builtin-modules_1.1.1-1_all.deb ...
Unpacking node-builtin-modules (1.1.1-1) ...
Selecting previously unselected package node-fs.realpath.
Preparing to unpack .../08-node-fs.realpath_1.0.0-1_all.deb ...
Unpacking node-fs.realpath (1.0.0-1) ...
Selecting previously unselected package node-hosted-git-info.
Preparing to unpack .../09-node-hosted-git-info_2.5.0-1_all.deb ...
Unpacking node-hosted-git-info (2.5.0-1) ...
Selecting previously unselected package node-wrappy.
Preparing to unpack .../10-node-wrappy_1.0.2-1_all.deb ...
Unpacking node-wrappy (1.0.2-1) ...
Selecting previously unselected package node-once.
Preparing to unpack .../11-node-once_1.4.0-2ubuntu1_all.deb ...
Unpacking node-once (1.4.0-2ubuntu1) ...
Selecting previously unselected package node-inflight.
Preparing to unpack .../12-node-inflight_1.0.6-1_all.deb ...
Unpacking node-inflight (1.0.6-1) ...
Selecting previously unselected package node-is-builtin-module.
Preparing to unpack .../13-node-is-builtin-module_1.0.0-1_all.deb ...
Unpacking node-is-builtin-module (1.0.0-1) ...
Selecting previously unselected package node-isexe.
Preparing to unpack .../14-node-isexe_2.0.0-3_all.deb ...
Unpacking node-isexe (2.0.0-3) ...
Selecting previously unselected package node-node-uuid.
Preparing to unpack .../15-node-node-uuid_1.4.7-5_all.deb ...
Unpacking node-node-uuid (1.4.7-5) ...
Selecting previously unselected package node-path-is-absolute.
Preparing to unpack .../16-node-path-is-absolute_1.0.0-1_all.deb ...
Unpacking node-path-is-absolute (1.0.0-1) ...
Selecting previously unselected package node-pseudomap.
Preparing to unpack .../17-node-pseudomap_1.0.2-1_all.deb ...
Unpacking node-pseudomap (1.0.2-1) ...
Selecting previously unselected package node-spdx-license-ids.
Preparing to unpack .../18-node-spdx-license-ids_1.2.2-1_all.deb ...
Unpacking node-spdx-license-ids (1.2.2-1) ...
Selecting previously unselected package node-spdx-correct.
Preparing to unpack .../19-node-spdx-correct_1.0.2-1_all.deb ...
Unpacking node-spdx-correct (1.0.2-1) ...
Selecting previously unselected package node-spdx-expression-parse.
Preparing to unpack .../20-node-spdx-expression-parse_1.0.4-1_all.deb ...
Unpacking node-spdx-expression-parse (1.0.4-1) ...
Selecting previously unselected package node-underscore.
Preparing to unpack .../21-node-underscore_1.8.3~dfsg-1_all.deb ...
Unpacking node-underscore (1.8.3~dfsg-1) ...
Selecting previously unselected package node-validate-npm-package-license.
Preparing to unpack .../22-node-validate-npm-package-license_3.0.1-1_all.deb ...
Unpacking node-validate-npm-package-license (3.0.1-1) ...
Selecting previously unselected package node-yallist.
Preparing to unpack .../23-node-yallist_2.0.0-1_all.deb ...
Unpacking node-yallist (2.0.0-1) ...
Selecting previously unselected package libjs-inherits.
Preparing to unpack .../24-libjs-inherits_2.0.3-1_all.deb ...
Unpacking libjs-inherits (2.0.3-1) ...
Selecting previously unselected package node-abbrev.
Preparing to unpack .../25-node-abbrev_1.0.9-1_all.deb ...
Unpacking node-abbrev (1.0.9-1) ...
Selecting previously unselected package node-ansi.
Preparing to unpack .../26-node-ansi_0.3.0-2ubuntu1_all.deb ...
Unpacking node-ansi (0.3.0-2ubuntu1) ...
Selecting previously unselected package node-ansi-color-table.
Preparing to unpack .../27-node-ansi-color-table_1.0.0-1_all.deb ...
Unpacking node-ansi-color-table (1.0.0-1) ...
Selecting previously unselected package node-archy.
Preparing to unpack .../28-node-archy_1.0.0-1ubuntu1_all.deb ...
Unpacking node-archy (1.0.0-1ubuntu1) ...
Selecting previously unselected package node-balanced-match.
Preparing to unpack .../29-node-balanced-match_0.4.2-1_all.deb ...
Unpacking node-balanced-match (0.4.2-1) ...
Selecting previously unselected package node-inherits.
Preparing to unpack .../30-node-inherits_2.0.3-1_all.deb ...
Unpacking node-inherits (2.0.3-1) ...
Selecting previously unselected package node-block-stream.
Preparing to unpack .../31-node-block-stream_0.0.9-1ubuntu1_all.deb ...
Unpacking node-block-stream (0.0.9-1ubuntu1) ...
Selecting previously unselected package node-concat-map.
Preparing to unpack .../32-node-concat-map_0.0.1-1_all.deb ...
Unpacking node-concat-map (0.0.1-1) ...
Selecting previously unselected package node-brace-expansion.
Preparing to unpack .../33-node-brace-expansion_1.1.8-1_all.deb ...
Unpacking node-brace-expansion (1.1.8-1) ...
Selecting previously unselected package node-delayed-stream.
Preparing to unpack .../34-node-delayed-stream_0.0.5-1_all.deb ...
Unpacking node-delayed-stream (0.0.5-1) ...
Selecting previously unselected package node-combined-stream.
Preparing to unpack .../35-node-combined-stream_0.0.5-1_all.deb ...
Unpacking node-combined-stream (0.0.5-1) ...
Selecting previously unselected package node-cookie-jar.
Preparing to unpack .../36-node-cookie-jar_0.3.1-1_all.deb ...
Unpacking node-cookie-jar (0.3.1-1) ...
Selecting previously unselected package node-forever-agent.
Preparing to unpack .../37-node-forever-agent_0.5.1-1_all.deb ...
Unpacking node-forever-agent (0.5.1-1) ...
Selecting previously unselected package node-mime.
Preparing to unpack .../38-node-mime_1.3.4-1_all.deb ...
Unpacking node-mime (1.3.4-1) ...
Selecting previously unselected package node-form-data.
Preparing to unpack .../39-node-form-data_0.1.0-1_all.deb ...
Unpacking node-form-data (0.1.0-1) ...
Selecting previously unselected package node-minimatch.
Preparing to unpack .../40-node-minimatch_3.0.4-3_all.deb ...
Unpacking node-minimatch (3.0.4-3) ...
Selecting previously unselected package node-glob.
Preparing to unpack .../41-node-glob_7.1.2-4_all.deb ...
Unpacking node-glob (7.1.2-4) ...
Selecting previously unselected package node-rimraf.
Preparing to unpack .../42-node-rimraf_2.6.2-1_all.deb ...
Unpacking node-rimraf (2.6.2-1) ...
Selecting previously unselected package node-mkdirp.
Preparing to unpack .../43-node-mkdirp_0.5.1-1_all.deb ...
Unpacking node-mkdirp (0.5.1-1) ...
Selecting previously unselected package node-graceful-fs.
Preparing to unpack .../44-node-graceful-fs_4.1.11-1_all.deb ...
Unpacking node-graceful-fs (4.1.11-1) ...
Selecting previously unselected package node-fstream.
Preparing to unpack .../45-node-fstream_1.0.10-1ubuntu0.18.04.1_all.deb ...
Unpacking node-fstream (1.0.10-1ubuntu0.18.04.1) ...
Selecting previously unselected package node-fstream-ignore.
Preparing to unpack .../46-node-fstream-ignore_0.0.6-2_all.deb ...
Unpacking node-fstream-ignore (0.0.6-2) ...
Selecting previously unselected package node-github-url-from-git.
Preparing to unpack .../47-node-github-url-from-git_1.4.0-1_all.deb ...
Unpacking node-github-url-from-git (1.4.0-1) ...
Selecting previously unselected package nodejs-dev.
Preparing to unpack .../48-nodejs-dev_8.10.0~dfsg-2ubuntu0.4_amd64.deb ...
Unpacking nodejs-dev (8.10.0~dfsg-2ubuntu0.4) ...
Selecting previously unselected package node-nopt.
Preparing to unpack .../49-node-nopt_3.0.6-3_all.deb ...
Unpacking node-nopt (3.0.6-3) ...
Selecting previously unselected package node-npmlog.
Preparing to unpack .../50-node-npmlog_0.0.4-1_all.deb ...
Unpacking node-npmlog (0.0.4-1) ...
Selecting previously unselected package node-osenv.
Preparing to unpack .../51-node-osenv_0.1.4-1_all.deb ...
Unpacking node-osenv (0.1.4-1) ...
Selecting previously unselected package node-tunnel-agent.
Preparing to unpack .../52-node-tunnel-agent_0.3.1-1_all.deb ...
Unpacking node-tunnel-agent (0.3.1-1) ...
Selecting previously unselected package node-json-stringify-safe.
Preparing to unpack .../53-node-json-stringify-safe_5.0.0-1_all.deb ...
Unpacking node-json-stringify-safe (5.0.0-1) ...
Selecting previously unselected package node-qs.
Preparing to unpack .../54-node-qs_2.2.4-1ubuntu1_all.deb ...
Unpacking node-qs (2.2.4-1ubuntu1) ...
Selecting previously unselected package node-request.
Preparing to unpack .../55-node-request_2.26.1-1_all.deb ...
Unpacking node-request (2.26.1-1) ...
Selecting previously unselected package node-semver.
Preparing to unpack .../56-node-semver_5.4.1-1_all.deb ...
Unpacking node-semver (5.4.1-1) ...
Selecting previously unselected package node-tar.
Preparing to unpack .../57-node-tar_2.2.1-1_all.deb ...
Unpacking node-tar (2.2.1-1) ...
Selecting previously unselected package node-which.
Preparing to unpack .../58-node-which_1.3.0-1_all.deb ...
Unpacking node-which (1.3.0-1) ...
Selecting previously unselected package node-gyp.
Preparing to unpack .../59-node-gyp_3.6.2-1ubuntu1_all.deb ...
Unpacking node-gyp (3.6.2-1ubuntu1) ...
Selecting previously unselected package node-ini.
Preparing to unpack .../60-node-ini_1.3.4-1_all.deb ...
Unpacking node-ini (1.3.4-1) ...
Selecting previously unselected package node-lockfile.
Preparing to unpack .../61-node-lockfile_0.4.1-1_all.deb ...
Unpacking node-lockfile (0.4.1-1) ...
Selecting previously unselected package node-lru-cache.
Preparing to unpack .../62-node-lru-cache_4.1.1-1_all.deb ...
Unpacking node-lru-cache (4.1.1-1) ...
Selecting previously unselected package node-mute-stream.
Preparing to unpack .../63-node-mute-stream_0.0.7-1_all.deb ...
Unpacking node-mute-stream (0.0.7-1) ...
Selecting previously unselected package node-normalize-package-data.
Preparing to unpack .../64-node-normalize-package-data_2.3.5-2_all.deb ...
Unpacking node-normalize-package-data (2.3.5-2) ...
Selecting previously unselected package node-read.
Preparing to unpack .../65-node-read_1.0.7-1_all.deb ...
Unpacking node-read (1.0.7-1) ...
Selecting previously unselected package node-read-package-json.
Preparing to unpack .../66-node-read-package-json_1.2.4-1_all.deb ...
Unpacking node-read-package-json (1.2.4-1) ...
Selecting previously unselected package node-retry.
Preparing to unpack .../67-node-retry_0.10.1-1_all.deb ...
Unpacking node-retry (0.10.1-1) ...
Selecting previously unselected package node-sha.
Preparing to unpack .../68-node-sha_1.2.3-1_all.deb ...
Unpacking node-sha (1.2.3-1) ...
Selecting previously unselected package node-slide.
Preparing to unpack .../69-node-slide_1.1.6-1_all.deb ...
Unpacking node-slide (1.1.6-1) ...
Selecting previously unselected package npm.
Preparing to unpack .../70-npm_3.5.2-0ubuntu4_all.deb ...
Unpacking npm (3.5.2-0ubuntu4) ...
Setting up node-lockfile (0.4.1-1) ...
Setting up node-spdx-expression-parse (1.0.4-1) ...
Setting up node-qs (2.2.4-1ubuntu1) ...
Setting up node-osenv (0.1.4-1) ...
Setting up node-ansi (0.3.0-2ubuntu1) ...
Setting up libjs-node-uuid (1.4.7-5) ...
Setting up node-hosted-git-info (2.5.0-1) ...
Setting up libjs-underscore (1.8.3~dfsg-1) ...
Setting up node-delayed-stream (0.0.5-1) ...
Setting up libjs-inherits (2.0.3-1) ...
Setting up node-tunnel-agent (0.3.1-1) ...
Setting up node-balanced-match (0.4.2-1) ...
Setting up node-node-uuid (1.4.7-5) ...
Setting up node-yallist (2.0.0-1) ...
Setting up node-slide (1.1.6-1) ...
Setting up node-github-url-from-git (1.4.0-1) ...
Setting up node-pseudomap (1.0.2-1) ...
Setting up libssl1.0-dev:amd64 (1.0.2n-1ubuntu5.5) ...
Setting up node-spdx-license-ids (1.2.2-1) ...
Setting up node-combined-stream (0.0.5-1) ...
Setting up node-wrappy (1.0.2-1) ...
Setting up node-mime (1.3.4-1) ...
Setting up node-abbrev (1.0.9-1) ...
Setting up node-semver (5.4.1-1) ...
Setting up node-retry (0.10.1-1) ...
Setting up node-forever-agent (0.5.1-1) ...
Setting up node-underscore (1.8.3~dfsg-1) ...
Setting up gyp (0.1+20150913git1f374df9-1ubuntu1) ...
Setting up node-json-stringify-safe (5.0.0-1) ...
Setting up node-inherits (2.0.3-1) ...
Setting up node-graceful-fs (4.1.11-1) ...
Setting up node-archy (1.0.0-1ubuntu1) ...
Setting up node-path-is-absolute (1.0.0-1) ...
Setting up node-builtin-modules (1.1.1-1) ...
Setting up node-isexe (2.0.0-3) ...
Setting up node-spdx-correct (1.0.2-1) ...
Setting up node-cookie-jar (0.3.1-1) ...
Setting up node-mute-stream (0.0.7-1) ...
Setting up libjs-async (0.8.0-3) ...
Setting up node-concat-map (0.0.1-1) ...
Setting up node-ini (1.3.4-1) ...
Setting up node-mkdirp (0.5.1-1) ...
Setting up node-once (1.4.0-2ubuntu1) ...
Setting up node-sha (1.2.3-1) ...
Setting up node-fs.realpath (1.0.0-1) ...
Setting up libuv1-dev:amd64 (1.18.0-3) ...
Setting up node-brace-expansion (1.1.8-1) ...
Setting up node-ansi-color-table (1.0.0-1) ...
Setting up node-npmlog (0.0.4-1) ...
Setting up node-is-builtin-module (1.0.0-1) ...
Setting up node-nopt (3.0.6-3) ...
Setting up node-which (1.3.0-1) ...
Setting up node-lru-cache (4.1.1-1) ...
Setting up node-block-stream (0.0.9-1ubuntu1) ...
Setting up node-validate-npm-package-license (3.0.1-1) ...
Setting up node-inflight (1.0.6-1) ...
Setting up node-read (1.0.7-1) ...
Setting up node-async (0.8.0-3) ...
Setting up node-form-data (0.1.0-1) ...
Setting up node-request (2.26.1-1) ...
Setting up node-minimatch (3.0.4-3) ...
Setting up nodejs-dev (8.10.0~dfsg-2ubuntu0.4) ...
Setting up node-normalize-package-data (2.3.5-2) ...
Setting up node-glob (7.1.2-4) ...
Setting up node-rimraf (2.6.2-1) ...
Setting up node-read-package-json (1.2.4-1) ...
Setting up node-fstream (1.0.10-1ubuntu0.18.04.1) ...
Setting up node-fstream-ignore (0.0.6-2) ...
Setting up node-tar (2.2.1-1) ...
Setting up node-gyp (3.6.2-1ubuntu1) ...
Setting up npm (3.5.2-0ubuntu4) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
(base) ye@ykt-pro:~/tool/kbide$ 
```

## npm run build

```
(base) ye@ykt-pro:~/tool/kbide$ npm run build

> kidbrightide@1.6.0 build /home/ye/tool/kbide
> npm install gulp && gulp build

npm WARN deprecated gulp-util@3.0.8: gulp-util is deprecated - replace it, following the guidelines at https://medium.com/gulpjs/gulp-util-ca3b1f9f9ac5
npm WARN deprecated resolve-url@0.2.1: https://github.com/lydell/resolve-url#deprecated
npm WARN deprecated urix@0.1.0: Please see https://github.com/lydell/urix#deprecated
npm WARN deprecated minimatch@2.0.10: Please update to minimatch 3.0.2 or higher to avoid a RegExp DoS issue
npm WARN deprecated minimatch@0.2.14: Please update to minimatch 3.0.2 or higher to avoid a RegExp DoS issue
npm WARN deprecated graceful-fs@1.2.3: please upgrade to graceful-fs 4 for compatibility with current and future versions of Node.js
npm WARN deprecated natives@1.1.6: This module relies on Node.js's internals and will break at some point. Do not use it, and update to graceful-fs@4.x.
kidbrightide@1.6.0 /home/ye/tool/kbide
└─┬ gulp@3.9.1 
  ├── archy@1.0.0 
  ├─┬ chalk@1.1.3 
  │ ├── ansi-styles@2.2.1 
  │ ├── escape-string-regexp@1.0.5 
  │ ├─┬ has-ansi@2.0.0 
  │ │ └── ansi-regex@2.1.1 
  │ ├── strip-ansi@3.0.1 
  │ └── supports-color@2.0.0 
  ├── deprecated@0.0.1 
  ├─┬ gulp-util@3.0.8 
  │ ├── array-differ@1.0.0 
  │ ├── array-uniq@1.0.3 
  │ ├── beeper@1.1.1 
  │ ├── dateformat@2.2.0 
  │ ├─┬ fancy-log@1.3.3 
  │ │ ├─┬ ansi-gray@0.1.1 
  │ │ │ └── ansi-wrap@0.1.0 
  │ │ ├── color-support@1.1.3 
  │ │ ├── parse-node-version@1.0.1 
  │ │ └── time-stamp@1.1.0 
  │ ├─┬ gulplog@1.0.0 
  │ │ └── glogg@1.0.2 
  │ ├─┬ has-gulplog@0.1.0 
  │ │ └── sparkles@1.0.1 
  │ ├── lodash._reescape@3.0.0 
  │ ├── lodash._reevaluate@3.0.0 
  │ ├── lodash._reinterpolate@3.0.0 
  │ ├─┬ lodash.template@3.6.2 
  │ │ ├── lodash._basecopy@3.0.1 
  │ │ ├── lodash._basetostring@3.0.1 
  │ │ ├── lodash._basevalues@3.0.0 
  │ │ ├── lodash._isiterateecall@3.0.9 
  │ │ ├─┬ lodash.escape@3.2.0 
  │ │ │ └── lodash._root@3.0.1 
  │ │ ├─┬ lodash.keys@3.1.2 
  │ │ │ ├── lodash._getnative@3.9.1 
  │ │ │ ├── lodash.isarguments@3.1.0 
  │ │ │ └── lodash.isarray@3.0.4 
  │ │ ├── lodash.restparam@3.6.1 
  │ │ └── lodash.templatesettings@3.1.1 
  │ ├─┬ multipipe@0.1.2 
  │ │ └─┬ duplexer2@0.0.2 
  │ │   └── readable-stream@1.1.14 
  │ ├── object-assign@3.0.0 
  │ ├── replace-ext@0.0.1 
  │ ├─┬ through2@2.0.5 
  │ │ ├─┬ readable-stream@2.3.7 
  │ │ │ ├── core-util-is@1.0.2 
  │ │ │ ├── inherits@2.0.4 
  │ │ │ ├── isarray@1.0.0 
  │ │ │ ├── process-nextick-args@2.0.1 
  │ │ │ ├── safe-buffer@5.1.2 
  │ │ │ ├── string_decoder@1.1.1 
  │ │ │ └── util-deprecate@1.0.2 
  │ │ └── xtend@4.0.2 
  │ └─┬ vinyl@0.5.3 
  │   ├── clone@1.0.4 
  │   └── clone-stats@0.0.1 
  ├── interpret@1.4.0 
  ├─┬ liftoff@2.5.0 
  │ ├── extend@3.0.2 
  │ ├─┬ findup-sync@2.0.0 
  │ │ ├── detect-file@1.0.0 
  │ │ ├─┬ is-glob@3.1.0 
  │ │ │ └── is-extglob@2.1.1 
  │ │ ├─┬ micromatch@3.1.10 
  │ │ │ ├── arr-diff@4.0.0 
  │ │ │ ├── array-unique@0.3.2 
  │ │ │ ├─┬ braces@2.3.2 
  │ │ │ │ ├── arr-flatten@1.1.0 
  │ │ │ │ ├─┬ extend-shallow@2.0.1 
  │ │ │ │ │ └── is-extendable@0.1.1 
  │ │ │ │ ├─┬ fill-range@4.0.0 
  │ │ │ │ │ ├── extend-shallow@2.0.1 
  │ │ │ │ │ ├─┬ is-number@3.0.0 
  │ │ │ │ │ │ └─┬ kind-of@3.2.2 
  │ │ │ │ │ │   └── is-buffer@1.1.6 
  │ │ │ │ │ ├── repeat-string@1.6.1 
  │ │ │ │ │ └── to-regex-range@2.1.1 
  │ │ │ │ ├── repeat-element@1.1.3 
  │ │ │ │ ├─┬ snapdragon-node@2.1.1 
  │ │ │ │ │ ├─┬ define-property@1.0.0 
  │ │ │ │ │ │ └─┬ is-descriptor@1.0.2 
  │ │ │ │ │ │   ├── is-accessor-descriptor@1.0.0 
  │ │ │ │ │ │   └── is-data-descriptor@1.0.0 
  │ │ │ │ │ └─┬ snapdragon-util@3.0.1 
  │ │ │ │ │   └── kind-of@3.2.2 
  │ │ │ │ └── split-string@3.1.0 
  │ │ │ ├─┬ define-property@2.0.2 
  │ │ │ │ └─┬ is-descriptor@1.0.2 
  │ │ │ │   ├── is-accessor-descriptor@1.0.0 
  │ │ │ │   └── is-data-descriptor@1.0.0 
  │ │ │ ├─┬ extend-shallow@3.0.2 
  │ │ │ │ ├── assign-symbols@1.0.0 
  │ │ │ │ └── is-extendable@1.0.1 
  │ │ │ ├─┬ extglob@2.0.4 
  │ │ │ │ ├─┬ define-property@1.0.0 
  │ │ │ │ │ └─┬ is-descriptor@1.0.2 
  │ │ │ │ │   ├── is-accessor-descriptor@1.0.0 
  │ │ │ │ │   └── is-data-descriptor@1.0.0 
  │ │ │ │ ├─┬ expand-brackets@2.1.4 
  │ │ │ │ │ ├── define-property@0.2.5 
  │ │ │ │ │ ├── extend-shallow@2.0.1 
  │ │ │ │ │ └── posix-character-classes@0.1.1 
  │ │ │ │ └── extend-shallow@2.0.1 
  │ │ │ ├── fragment-cache@0.2.1 
  │ │ │ ├── kind-of@6.0.3 
  │ │ │ ├─┬ nanomatch@1.2.13 
  │ │ │ │ └── is-windows@1.0.2 
  │ │ │ ├─┬ regex-not@1.0.2 
  │ │ │ │ └─┬ safe-regex@1.1.0 
  │ │ │ │   └── ret@0.1.15 
  │ │ │ ├─┬ snapdragon@0.8.2 
  │ │ │ │ ├─┬ base@0.11.2 
  │ │ │ │ │ ├─┬ cache-base@1.0.1 
  │ │ │ │ │ │ ├─┬ collection-visit@1.0.0 
  │ │ │ │ │ │ │ ├── map-visit@1.0.0 
  │ │ │ │ │ │ │ └── object-visit@1.0.1 
  │ │ │ │ │ │ ├── get-value@2.0.6 
  │ │ │ │ │ │ ├─┬ has-value@1.0.0 
  │ │ │ │ │ │ │ └─┬ has-values@1.0.0 
  │ │ │ │ │ │ │   └── kind-of@4.0.0 
  │ │ │ │ │ │ ├─┬ set-value@2.0.1 
  │ │ │ │ │ │ │ └── extend-shallow@2.0.1 
  │ │ │ │ │ │ ├─┬ to-object-path@0.3.0 
  │ │ │ │ │ │ │ └── kind-of@3.2.2 
  │ │ │ │ │ │ ├── union-value@1.0.1 
  │ │ │ │ │ │ └─┬ unset-value@1.0.0 
  │ │ │ │ │ │   └─┬ has-value@0.3.1 
  │ │ │ │ │ │     ├── has-values@0.1.4 
  │ │ │ │ │ │     └─┬ isobject@2.1.0 
  │ │ │ │ │ │       └── isarray@1.0.0 
  │ │ │ │ │ ├─┬ class-utils@0.3.6 
  │ │ │ │ │ │ ├── arr-union@3.1.0 
  │ │ │ │ │ │ ├── define-property@0.2.5 
  │ │ │ │ │ │ └─┬ static-extend@0.1.2 
  │ │ │ │ │ │   ├── define-property@0.2.5 
  │ │ │ │ │ │   └─┬ object-copy@0.1.0 
  │ │ │ │ │ │     ├── copy-descriptor@0.1.1 
  │ │ │ │ │ │     ├── define-property@0.2.5 
  │ │ │ │ │ │     └── kind-of@3.2.2 
  │ │ │ │ │ ├── component-emitter@1.3.0 
  │ │ │ │ │ ├─┬ define-property@1.0.0 
  │ │ │ │ │ │ └─┬ is-descriptor@1.0.2 
  │ │ │ │ │ │   ├── is-accessor-descriptor@1.0.0 
  │ │ │ │ │ │   └── is-data-descriptor@1.0.0 
  │ │ │ │ │ ├─┬ mixin-deep@1.3.2 
  │ │ │ │ │ │ └── is-extendable@1.0.1 
  │ │ │ │ │ └── pascalcase@0.1.1 
  │ │ │ │ ├─┬ debug@2.6.9 
  │ │ │ │ │ └── ms@2.0.0 
  │ │ │ │ ├─┬ define-property@0.2.5 
  │ │ │ │ │ └─┬ is-descriptor@0.1.6 
  │ │ │ │ │   ├─┬ is-accessor-descriptor@0.1.6 
  │ │ │ │ │   │ └── kind-of@3.2.2 
  │ │ │ │ │   ├─┬ is-data-descriptor@0.1.4 
  │ │ │ │ │   │ └── kind-of@3.2.2 
  │ │ │ │ │   └── kind-of@5.1.0 
  │ │ │ │ ├── extend-shallow@2.0.1 
  │ │ │ │ ├── source-map@0.5.7 
  │ │ │ │ ├─┬ source-map-resolve@0.5.3 
  │ │ │ │ │ ├── atob@2.1.2 
  │ │ │ │ │ ├── decode-uri-component@0.2.0 
  │ │ │ │ │ ├── resolve-url@0.2.1 
  │ │ │ │ │ ├── source-map-url@0.4.0 
  │ │ │ │ │ └── urix@0.1.0 
  │ │ │ │ └── use@3.1.1 
  │ │ │ └── to-regex@3.0.2 
  │ │ └─┬ resolve-dir@1.0.1 
  │ │   └─┬ global-modules@1.0.0 
  │ │     └─┬ global-prefix@1.0.2 
  │ │       ├── ini@1.3.8 
  │ │       └─┬ which@1.3.1 
  │ │         └── isexe@2.0.0 
  │ ├─┬ fined@1.2.0 
  │ │ ├─┬ expand-tilde@2.0.2 
  │ │ │ └─┬ homedir-polyfill@1.0.3 
  │ │ │   └── parse-passwd@1.0.0 
  │ │ ├─┬ object.defaults@1.1.0 
  │ │ │ ├── array-each@1.0.1 
  │ │ │ └── array-slice@1.1.0 
  │ │ ├── object.pick@1.3.0 
  │ │ └─┬ parse-filepath@1.0.2 
  │ │   ├─┬ is-absolute@1.0.0 
  │ │   │ └─┬ is-relative@1.0.0 
  │ │   │   └─┬ is-unc-path@1.0.0 
  │ │   │     └── unc-path-regex@0.1.2 
  │ │   ├── map-cache@0.2.2 
  │ │   └─┬ path-root@0.1.1 
  │ │     └── path-root-regex@0.1.2 
  │ ├── flagged-respawn@1.0.1 
  │ ├─┬ is-plain-object@2.0.4 
  │ │ └── isobject@3.0.1 
  │ ├─┬ object.map@1.0.1 
  │ │ ├─┬ for-own@1.0.0 
  │ │ │ └── for-in@1.0.2 
  │ │ └── make-iterator@1.0.1 
  │ ├── rechoir@0.6.2 
  │ └─┬ resolve@1.19.0 
  │   ├─┬ is-core-module@2.2.0 
  │   │ └─┬ has@1.0.3 
  │   │   └── function-bind@1.1.1 
  │   └── path-parse@1.0.6 
  ├── minimist@1.2.5 
  ├─┬ orchestrator@0.3.8 
  │ ├─┬ end-of-stream@0.1.5 
  │ │ └─┬ once@1.3.3 
  │ │   └── wrappy@1.0.2 
  │ ├── sequencify@0.0.7 
  │ └── stream-consume@0.1.1 
  ├── pretty-hrtime@1.0.3 
  ├── semver@4.3.6 
  ├─┬ tildify@1.2.0 
  │ └── os-homedir@1.0.2 
  ├─┬ v8flags@2.1.1 
  │ └── user-home@1.1.1 
  └─┬ vinyl-fs@0.3.14 
    ├── defaults@1.0.3 
    ├─┬ glob-stream@3.1.18 
    │ ├─┬ glob@4.5.3 
    │ │ └── inflight@1.0.6 
    │ ├─┬ glob2base@0.0.12 
    │ │ └── find-index@0.1.1 
    │ ├─┬ minimatch@2.0.10 
    │ │ └─┬ brace-expansion@1.1.11 
    │ │   ├── balanced-match@1.0.0 
    │ │   └── concat-map@0.0.1 
    │ ├── ordered-read-streams@0.1.0 
    │ ├─┬ through2@0.6.5 
    │ │ └── readable-stream@1.0.34 
    │ └── unique-stream@1.0.0 
    ├─┬ glob-watcher@0.0.6 
    │ └─┬ gaze@0.5.2 
    │   └─┬ globule@0.1.0 
    │     ├─┬ glob@3.1.21 
    │     │ ├── graceful-fs@1.2.3 
    │     │ └── inherits@1.0.2 
    │     ├── lodash@1.0.2 
    │     └─┬ minimatch@0.2.14 
    │       ├── lru-cache@2.7.3 
    │       └── sigmund@1.0.1 
    ├─┬ graceful-fs@3.0.12 
    │ └── natives@1.1.6 
    ├── mkdirp@0.5.5 
    ├─┬ strip-bom@1.0.0 
    │ ├── first-chunk-stream@1.0.0 
    │ └── is-utf8@0.2.1 
    ├─┬ through2@0.6.5 
    │ └─┬ readable-stream@1.0.34 
    │   ├── isarray@0.0.1 
    │   └── string_decoder@0.10.31 
    └─┬ vinyl@0.4.6 
      └── clone@0.2.0 

module.js:549
    throw err;
    ^

Error: Cannot find module 'gulp-download'
    at Function.Module._resolveFilename (module.js:547:15)
    at Function.Module._load (module.js:474:25)
    at Module.require (module.js:596:17)
    at require (internal/module.js:11:18)
    at Object.<anonymous> (/home/ye/tool/kbide/gulpfile.js:4:18)
    at Module._compile (module.js:652:30)
    at Object.Module._extensions..js (module.js:663:10)
    at Module.load (module.js:565:32)
    at tryModuleLoad (module.js:505:12)
    at Function.Module._load (module.js:497:3)

npm ERR! Linux 5.4.0-62-generic
npm ERR! argv "/usr/bin/node" "/usr/bin/npm" "run" "build"
npm ERR! node v8.10.0
npm ERR! npm  v3.5.2
npm ERR! code ELIFECYCLE
npm ERR! kidbrightide@1.6.0 build: `npm install gulp && gulp build`
npm ERR! Exit status 1
npm ERR! 
npm ERR! Failed at the kidbrightide@1.6.0 build script 'npm install gulp && gulp build'.
npm ERR! Make sure you have the latest version of node.js and npm installed.
npm ERR! If you do, this is most likely a problem with the kidbrightide package,
npm ERR! not with npm itself.
npm ERR! Tell the author that this fails on your system:
npm ERR!     npm install gulp && gulp build
npm ERR! You can get information on how to open an issue for this project with:
npm ERR!     npm bugs kidbrightide
npm ERR! Or if that isn't available, you can get their info via:
npm ERR!     npm owner ls kidbrightide
npm ERR! There is likely additional logging output above.

npm ERR! Please include the following file with any support request:
npm ERR!     /home/ye/tool/kbide/npm-debug.log
(base) ye@ykt-pro:~/tool/kbide$ 
```

## Remove node_modules/

Solution က KidBright နဲ့ အတူပါလာတဲ့ node_modules/ ဖိုလ်ဒါတစ်ခုလုံးကို ဖျက်ပစ်ပြီး npm install ပြန်လုပ်တာပါ။  
အဲဒါကြောင့် အရင်ဆုံး ဖျက်ရအောင်...  

```
(base) ye@ykt-pro:~/tool/kbide$ ls
app  archive  docs  esp32  gulpfile.js  index.js  node_modules  npm-debug.log  package.json  package-lock.json  plugins  README.md
(base) ye@ykt-pro:~/tool/kbide$ rm -rf node_modules/
```

## install npm

```
(base) ye@ykt-pro:~/tool/kbide$ npm install
npm WARN deprecated request@2.88.2: request has been deprecated, see https://github.com/request/request/issues/3142
npm WARN deprecated gulp-util@3.0.8: gulp-util is deprecated - replace it, following the guidelines at https://medium.com/gulpjs/gulp-util-ca3b1f9f9ac5
npm WARN deprecated har-validator@5.1.5: this library is no longer supported
npm WARN deprecated urix@0.1.0: Please see https://github.com/lydell/urix#deprecated
npm WARN deprecated resolve-url@0.2.1: https://github.com/lydell/resolve-url#deprecated
npm WARN deprecated minimatch@2.0.10: Please update to minimatch 3.0.2 or higher to avoid a RegExp DoS issue
npm WARN deprecated minimatch@0.2.14: Please update to minimatch 3.0.2 or higher to avoid a RegExp DoS issue
npm WARN deprecated graceful-fs@1.2.3: please upgrade to graceful-fs 4 for compatibility with current and future versions of Node.js
npm WARN deprecated natives@1.1.6: This module relies on Node.js's internals and will break at some point. Do not use it, and update to graceful-fs@4.x.
kidbrightide@1.6.0 /home/ye/tool/kbide
├─┬ del@3.0.0 
│ ├─┬ globby@6.1.0 
│ │ ├── array-union@1.0.2 
│ │ ├─┬ glob@7.1.6 
│ │ │ ├── fs.realpath@1.0.0 
│ │ │ ├─┬ inflight@1.0.6 
│ │ │ │ └── wrappy@1.0.2 
│ │ │ ├── inherits@2.0.4 
│ │ │ ├─┬ minimatch@3.0.4 
│ │ │ │ └─┬ brace-expansion@1.1.11 
│ │ │ │   ├── balanced-match@1.0.0 
│ │ │ │   └── concat-map@0.0.1 
│ │ │ ├── once@1.4.0 
│ │ │ └── path-is-absolute@1.0.1 
│ │ ├── object-assign@4.1.1 
│ │ ├── pify@2.3.0 
│ │ └─┬ pinkie-promise@2.0.1 
│ │   └── pinkie@2.0.4 
│ ├── is-path-cwd@1.0.0 
│ ├─┬ is-path-in-cwd@1.0.1 
│ │ └─┬ is-path-inside@1.0.1 
│ │   └── path-is-inside@1.0.2 
│ ├── p-map@1.2.0 
│ ├── pify@3.0.0 
│ └── rimraf@2.7.1 
├─┬ gulp@3.9.1 
│ ├── archy@1.0.0 
│ ├─┬ chalk@1.1.3 
│ │ ├── ansi-styles@2.2.1 
│ │ ├── escape-string-regexp@1.0.5 
│ │ ├─┬ has-ansi@2.0.0 
│ │ │ └── ansi-regex@2.1.1 
│ │ ├── strip-ansi@3.0.1 
│ │ └── supports-color@2.0.0 
│ ├── deprecated@0.0.1 
│ ├─┬ gulp-util@3.0.8 
│ │ ├── array-differ@1.0.0 
│ │ ├── array-uniq@1.0.3 
│ │ ├── beeper@1.1.1 
│ │ ├── dateformat@2.2.0 
│ │ ├─┬ fancy-log@1.3.3 
│ │ │ ├── ansi-gray@0.1.1 
│ │ │ ├── color-support@1.1.3 
│ │ │ ├── parse-node-version@1.0.1 
│ │ │ └── time-stamp@1.1.0 
│ │ ├─┬ gulplog@1.0.0 
│ │ │ └── glogg@1.0.2 
│ │ ├─┬ has-gulplog@0.1.0 
│ │ │ └── sparkles@1.0.1 
│ │ ├── lodash._reescape@3.0.0 
│ │ ├── lodash._reevaluate@3.0.0 
│ │ ├── lodash._reinterpolate@3.0.0 
│ │ ├─┬ lodash.template@3.6.2 
│ │ │ ├── lodash._basecopy@3.0.1 
│ │ │ ├── lodash._basetostring@3.0.1 
│ │ │ ├── lodash._basevalues@3.0.0 
│ │ │ ├── lodash._isiterateecall@3.0.9 
│ │ │ ├─┬ lodash.escape@3.2.0 
│ │ │ │ └── lodash._root@3.0.1 
│ │ │ ├─┬ lodash.keys@3.1.2 
│ │ │ │ ├── lodash._getnative@3.9.1 
│ │ │ │ ├── lodash.isarguments@3.1.0 
│ │ │ │ └── lodash.isarray@3.0.4 
│ │ │ ├── lodash.restparam@3.6.1 
│ │ │ └── lodash.templatesettings@3.1.1 
│ │ ├─┬ multipipe@0.1.2 
│ │ │ └─┬ duplexer2@0.0.2 
│ │ │   └── readable-stream@1.1.14 
│ │ ├── object-assign@3.0.0 
│ │ ├── replace-ext@0.0.1 
│ │ └─┬ vinyl@0.5.3 
│ │   ├── clone@1.0.4 
│ │   └── clone-stats@0.0.1 
│ ├── interpret@1.4.0 
│ ├─┬ liftoff@2.5.0 
│ │ ├── extend@3.0.2 
│ │ ├─┬ findup-sync@2.0.0 
│ │ │ ├── detect-file@1.0.0 
│ │ │ ├─┬ is-glob@3.1.0 
│ │ │ │ └── is-extglob@2.1.1 
│ │ │ ├─┬ micromatch@3.1.10 
│ │ │ │ ├── arr-diff@4.0.0 
│ │ │ │ ├── array-unique@0.3.2 
│ │ │ │ ├─┬ braces@2.3.2 
│ │ │ │ │ ├─┬ extend-shallow@2.0.1 
│ │ │ │ │ │ └── is-extendable@0.1.1 
│ │ │ │ │ ├─┬ fill-range@4.0.0 
│ │ │ │ │ │ ├── extend-shallow@2.0.1 
│ │ │ │ │ │ ├─┬ is-number@3.0.0 
│ │ │ │ │ │ │ └─┬ kind-of@3.2.2 
│ │ │ │ │ │ │   └── is-buffer@1.1.6 
│ │ │ │ │ │ ├── repeat-string@1.6.1 
│ │ │ │ │ │ └── to-regex-range@2.1.1 
│ │ │ │ │ ├── repeat-element@1.1.3 
│ │ │ │ │ ├─┬ snapdragon-node@2.1.1 
│ │ │ │ │ │ ├─┬ define-property@1.0.0 
│ │ │ │ │ │ │ └─┬ is-descriptor@1.0.2 
│ │ │ │ │ │ │   ├── is-accessor-descriptor@1.0.0 
│ │ │ │ │ │ │   ├── is-data-descriptor@1.0.0 
│ │ │ │ │ │ │   └── kind-of@6.0.3 
│ │ │ │ │ │ └─┬ snapdragon-util@3.0.1 
│ │ │ │ │ │   └── kind-of@3.2.2 
│ │ │ │ │ └─┬ split-string@3.1.0 
│ │ │ │ │   └─┬ extend-shallow@3.0.2 
│ │ │ │ │     └── is-extendable@1.0.1 
│ │ │ │ ├─┬ define-property@2.0.2 
│ │ │ │ │ └─┬ is-descriptor@1.0.2 
│ │ │ │ │   ├── is-accessor-descriptor@1.0.0 
│ │ │ │ │   ├── is-data-descriptor@1.0.0 
│ │ │ │ │   └── kind-of@6.0.3 
│ │ │ │ ├─┬ extend-shallow@3.0.2 
│ │ │ │ │ ├── assign-symbols@1.0.0 
│ │ │ │ │ └── is-extendable@1.0.1 
│ │ │ │ ├─┬ extglob@2.0.4 
│ │ │ │ │ ├─┬ define-property@1.0.0 
│ │ │ │ │ │ └─┬ is-descriptor@1.0.2 
│ │ │ │ │ │   ├── is-accessor-descriptor@1.0.0 
│ │ │ │ │ │   ├── is-data-descriptor@1.0.0 
│ │ │ │ │ │   └── kind-of@6.0.3 
│ │ │ │ │ ├─┬ expand-brackets@2.1.4 
│ │ │ │ │ │ ├── define-property@0.2.5 
│ │ │ │ │ │ ├── extend-shallow@2.0.1 
│ │ │ │ │ │ └── posix-character-classes@0.1.1 
│ │ │ │ │ └── extend-shallow@2.0.1 
│ │ │ │ ├── fragment-cache@0.2.1 
│ │ │ │ ├── kind-of@6.0.3 
│ │ │ │ ├─┬ nanomatch@1.2.13 
│ │ │ │ │ ├── arr-diff@4.0.0 
│ │ │ │ │ ├─┬ extend-shallow@3.0.2 
│ │ │ │ │ │ └── is-extendable@1.0.1 
│ │ │ │ │ ├── is-windows@1.0.2 
│ │ │ │ │ └── kind-of@6.0.3 
│ │ │ │ ├─┬ regex-not@1.0.2 
│ │ │ │ │ ├─┬ extend-shallow@3.0.2 
│ │ │ │ │ │ └── is-extendable@1.0.1 
│ │ │ │ │ └─┬ safe-regex@1.1.0 
│ │ │ │ │   └── ret@0.1.15 
│ │ │ │ ├─┬ snapdragon@0.8.2 
│ │ │ │ │ ├─┬ base@0.11.2 
│ │ │ │ │ │ ├─┬ cache-base@1.0.1 
│ │ │ │ │ │ │ ├─┬ collection-visit@1.0.0 
│ │ │ │ │ │ │ │ ├── map-visit@1.0.0 
│ │ │ │ │ │ │ │ └── object-visit@1.0.1 
│ │ │ │ │ │ │ ├── get-value@2.0.6 
│ │ │ │ │ │ │ ├─┬ has-value@1.0.0 
│ │ │ │ │ │ │ │ └─┬ has-values@1.0.0 
│ │ │ │ │ │ │ │   └── kind-of@4.0.0 
│ │ │ │ │ │ │ ├─┬ set-value@2.0.1 
│ │ │ │ │ │ │ │ └── extend-shallow@2.0.1 
│ │ │ │ │ │ │ ├─┬ to-object-path@0.3.0 
│ │ │ │ │ │ │ │ └── kind-of@3.2.2 
│ │ │ │ │ │ │ ├─┬ union-value@1.0.1 
│ │ │ │ │ │ │ │ └── arr-union@3.1.0 
│ │ │ │ │ │ │ └─┬ unset-value@1.0.0 
│ │ │ │ │ │ │   └─┬ has-value@0.3.1 
│ │ │ │ │ │ │     ├── has-values@0.1.4 
│ │ │ │ │ │ │     └─┬ isobject@2.1.0 
│ │ │ │ │ │ │       └── isarray@1.0.0 
│ │ │ │ │ │ ├─┬ class-utils@0.3.6 
│ │ │ │ │ │ │ ├── arr-union@3.1.0 
│ │ │ │ │ │ │ ├── define-property@0.2.5 
│ │ │ │ │ │ │ └─┬ static-extend@0.1.2 
│ │ │ │ │ │ │   ├── define-property@0.2.5 
│ │ │ │ │ │ │   └─┬ object-copy@0.1.0 
│ │ │ │ │ │ │     ├── copy-descriptor@0.1.1 
│ │ │ │ │ │ │     ├── define-property@0.2.5 
│ │ │ │ │ │ │     └── kind-of@3.2.2 
│ │ │ │ │ │ ├── component-emitter@1.3.0 
│ │ │ │ │ │ ├─┬ define-property@1.0.0 
│ │ │ │ │ │ │ └─┬ is-descriptor@1.0.2 
│ │ │ │ │ │ │   ├── is-accessor-descriptor@1.0.0 
│ │ │ │ │ │ │   ├── is-data-descriptor@1.0.0 
│ │ │ │ │ │ │   └── kind-of@6.0.3 
│ │ │ │ │ │ ├─┬ mixin-deep@1.3.2 
│ │ │ │ │ │ │ └── is-extendable@1.0.1 
│ │ │ │ │ │ └── pascalcase@0.1.1 
│ │ │ │ │ ├─┬ debug@2.6.9 
│ │ │ │ │ │ └── ms@2.0.0 
│ │ │ │ │ ├─┬ define-property@0.2.5 
│ │ │ │ │ │ └─┬ is-descriptor@0.1.6 
│ │ │ │ │ │   ├─┬ is-accessor-descriptor@0.1.6 
│ │ │ │ │ │   │ └── kind-of@3.2.2 
│ │ │ │ │ │   ├─┬ is-data-descriptor@0.1.4 
│ │ │ │ │ │   │ └── kind-of@3.2.2 
│ │ │ │ │ │   └── kind-of@5.1.0 
│ │ │ │ │ ├── extend-shallow@2.0.1 
│ │ │ │ │ ├── source-map@0.5.7 
│ │ │ │ │ ├─┬ source-map-resolve@0.5.3 
│ │ │ │ │ │ ├── atob@2.1.2 
│ │ │ │ │ │ ├── decode-uri-component@0.2.0 
│ │ │ │ │ │ ├── resolve-url@0.2.1 
│ │ │ │ │ │ ├── source-map-url@0.4.0 
│ │ │ │ │ │ └── urix@0.1.0 
│ │ │ │ │ └── use@3.1.1 
│ │ │ │ └─┬ to-regex@3.0.2 
│ │ │ │   └─┬ extend-shallow@3.0.2 
│ │ │ │     └── is-extendable@1.0.1 
│ │ │ └─┬ resolve-dir@1.0.1 
│ │ │   └─┬ global-modules@1.0.0 
│ │ │     └─┬ global-prefix@1.0.2 
│ │ │       ├── ini@1.3.8 
│ │ │       └─┬ which@1.3.1 
│ │ │         └── isexe@2.0.0 
│ │ ├─┬ fined@1.2.0 
│ │ │ ├─┬ expand-tilde@2.0.2 
│ │ │ │ └─┬ homedir-polyfill@1.0.3 
│ │ │ │   └── parse-passwd@1.0.0 
│ │ │ ├─┬ object.defaults@1.1.0 
│ │ │ │ ├── array-each@1.0.1 
│ │ │ │ └── array-slice@1.1.0 
│ │ │ ├── object.pick@1.3.0 
│ │ │ └─┬ parse-filepath@1.0.2 
│ │ │   ├─┬ is-absolute@1.0.0 
│ │ │   │ └─┬ is-relative@1.0.0 
│ │ │   │   └─┬ is-unc-path@1.0.0 
│ │ │   │     └── unc-path-regex@0.1.2 
│ │ │   ├── map-cache@0.2.2 
│ │ │   └─┬ path-root@0.1.1 
│ │ │     └── path-root-regex@0.1.2 
│ │ ├── flagged-respawn@1.0.1 
│ │ ├─┬ is-plain-object@2.0.4 
│ │ │ └── isobject@3.0.1 
│ │ ├─┬ object.map@1.0.1 
│ │ │ ├─┬ for-own@1.0.0 
│ │ │ │ └── for-in@1.0.2 
│ │ │ └─┬ make-iterator@1.0.1 
│ │ │   └── kind-of@6.0.3 
│ │ ├── rechoir@0.6.2 
│ │ └─┬ resolve@1.19.0 
│ │   ├─┬ is-core-module@2.2.0 
│ │   │ └─┬ has@1.0.3 
│ │   │   └── function-bind@1.1.1 
│ │   └── path-parse@1.0.6 
│ ├── minimist@1.2.5 
│ ├─┬ orchestrator@0.3.8 
│ │ ├─┬ end-of-stream@0.1.5 
│ │ │ └── once@1.3.3 
│ │ ├── sequencify@0.0.7 
│ │ └── stream-consume@0.1.1 
│ ├── pretty-hrtime@1.0.3 
│ ├── semver@4.3.6 
│ ├─┬ tildify@1.2.0 
│ │ └── os-homedir@1.0.2 
│ ├─┬ v8flags@2.1.1 
│ │ └── user-home@1.1.1 
│ └─┬ vinyl-fs@0.3.14 
│   ├── defaults@1.0.3 
│   ├─┬ glob-stream@3.1.18 
│   │ ├── glob@4.5.3 
│   │ ├─┬ glob2base@0.0.12 
│   │ │ └── find-index@0.1.1 
│   │ ├── minimatch@2.0.10 
│   │ ├── ordered-read-streams@0.1.0 
│   │ ├─┬ through2@0.6.5 
│   │ │ └── readable-stream@1.0.34 
│   │ └── unique-stream@1.0.0 
│   ├─┬ glob-watcher@0.0.6 
│   │ └─┬ gaze@0.5.2 
│   │   └─┬ globule@0.1.0 
│   │     ├─┬ glob@3.1.21 
│   │     │ ├── graceful-fs@1.2.3 
│   │     │ └── inherits@1.0.2 
│   │     ├── lodash@1.0.2 
│   │     └─┬ minimatch@0.2.14 
│   │       ├── lru-cache@2.7.3 
│   │       └── sigmund@1.0.1 
│   ├─┬ graceful-fs@3.0.12 
│   │ └── natives@1.1.6 
│   ├── mkdirp@0.5.5 
│   ├─┬ strip-bom@1.0.0 
│   │ ├── first-chunk-stream@1.0.0 
│   │ └── is-utf8@0.2.1 
│   ├─┬ through2@0.6.5 
│   │ └─┬ readable-stream@1.0.34 
│   │   ├── isarray@0.0.1 
│   │   └── string_decoder@0.10.31 
│   └─┬ vinyl@0.4.6 
│     └── clone@0.2.0 
├─┬ gulp-download@0.0.1 
│ ├─┬ request@2.88.2 
│ │ ├── aws-sign2@0.7.0 
│ │ ├── aws4@1.11.0 
│ │ ├── caseless@0.12.0 
│ │ ├─┬ combined-stream@1.0.8 
│ │ │ └── delayed-stream@1.0.0 
│ │ ├── forever-agent@0.6.1 
│ │ ├─┬ form-data@2.3.3 
│ │ │ └── asynckit@0.4.0 
│ │ ├─┬ har-validator@5.1.5 
│ │ │ ├─┬ ajv@6.12.6 
│ │ │ │ ├── fast-deep-equal@3.1.3 
│ │ │ │ ├── fast-json-stable-stringify@2.1.0 
│ │ │ │ ├── json-schema-traverse@0.4.1 
│ │ │ │ └── uri-js@4.4.1 
│ │ │ └── har-schema@2.0.0 
│ │ ├─┬ http-signature@1.2.0 
│ │ │ ├── assert-plus@1.0.0 
│ │ │ ├─┬ jsprim@1.4.1 
│ │ │ │ ├── extsprintf@1.3.0 
│ │ │ │ ├── json-schema@0.2.3 
│ │ │ │ └── verror@1.10.0 
│ │ │ └─┬ sshpk@1.16.1 
│ │ │   ├── asn1@0.2.4 
│ │ │   ├── bcrypt-pbkdf@1.0.2 
│ │ │   ├── dashdash@1.14.1 
│ │ │   ├── ecc-jsbn@0.1.2 
│ │ │   ├── getpass@0.1.7 
│ │ │   ├── jsbn@0.1.1 
│ │ │   ├── safer-buffer@2.1.2 
│ │ │   └── tweetnacl@0.14.5 
│ │ ├── is-typedarray@1.0.0 
│ │ ├── isstream@0.1.2 
│ │ ├── json-stringify-safe@5.0.1 
│ │ ├─┬ mime-types@2.1.28 
│ │ │ └── mime-db@1.45.0 
│ │ ├── oauth-sign@0.9.0 
│ │ ├── performance-now@2.1.0 
│ │ ├── qs@6.5.2 
│ │ ├── safe-buffer@5.1.2 
│ │ ├─┬ tough-cookie@2.5.0 
│ │ │ ├── psl@1.8.0 
│ │ │ └── punycode@2.1.1 
│ │ ├── tunnel-agent@0.6.0 
│ │ └── uuid@3.4.0 
│ ├─┬ request-progress@3.0.0 
│ │ └── throttleit@1.0.0 
│ └── through@2.3.8 
└─┬ gulp-exec@3.0.2 
  ├─┬ lodash.template@4.5.0 
  │ └── lodash.templatesettings@4.2.0 
  ├─┬ plugin-error@0.1.2 
  │ ├─┬ ansi-cyan@0.1.1 
  │ │ └── ansi-wrap@0.1.0 
  │ ├── ansi-red@0.1.1 
  │ ├─┬ arr-diff@1.1.0 
  │ │ ├── arr-flatten@1.1.0 
  │ │ └── array-slice@0.2.3 
  │ ├── arr-union@2.1.0 
  │ └─┬ extend-shallow@1.1.4 
  │   └── kind-of@1.1.0 
  └─┬ through2@2.0.5 
    ├─┬ readable-stream@2.3.7 
    │ ├── core-util-is@1.0.2 
    │ ├── isarray@1.0.0 
    │ ├── process-nextick-args@2.0.1 
    │ ├── string_decoder@1.1.1 
    │ └── util-deprecate@1.0.2 
    └── xtend@4.0.2 

(base) ye@ykt-pro:~/tool/kbide$ 
```

## npm run build

```
(base) ye@ykt-pro:~/tool/kbide$ npm run build

> kidbrightide@1.6.0 build /home/ye/tool/kbide
> npm install gulp && gulp build

npm WARN deprecated urix@0.1.0: Please see https://github.com/lydell/urix#deprecated
npm WARN deprecated resolve-url@0.2.1: https://github.com/lydell/resolve-url#deprecated
npm WARN deprecated minimatch@2.0.10: Please update to minimatch 3.0.2 or higher to avoid a RegExp DoS issue
npm WARN deprecated minimatch@0.2.14: Please update to minimatch 3.0.2 or higher to avoid a RegExp DoS issue
npm WARN deprecated graceful-fs@1.2.3: please upgrade to graceful-fs 4 for compatibility with current and future versions of Node.js
npm WARN deprecated natives@1.1.6: This module relies on Node.js's internals and will break at some point. Do not use it, and update to graceful-fs@4.x.
- once@1.3.3 node_modules/end-of-stream/node_modules/once
kidbrightide@1.6.0 /home/ye/tool/kbide
└─┬ del@3.0.0
  └─┬ globby@6.1.0
    └─┬ glob@7.1.6
      └── once@1.3.3 

[04:13:20] Using gulpfile ~/tool/kbide/gulpfile.js
[04:13:20] Starting 'install'...
[04:14:09] Finished 'install' after 49 s
[04:14:09] Starting 'download_xtensa'...
xtensa-esp32-elf-linux64-1.22.0-80-g6c4433a-5.2.0.tar
[gulp] Downloading https://dl.espressif.com/dl/xtensa-esp32-elf-linux64-1.22.0-80-g6c4433a-5.2.0.tar.gz... 0.020369927416218514% 0.039636892712464775% 0.05556919093820687% 0.07224252629072767% 0.09002741733341653% 0.10781230837610538% 0.12411512516523683% 0.1419000162079257% 0.15709127730688907% 0.17302357553263117% 0.19006742944854133% 0.20822283905461952% 0.22711928578747645% 0.24453365826677595% 0.25935440080235% 0.2752866990280921% 0.29233055294400223% 0.3108564811134698% 0.32790033502937993% 0.3456852260720688% 0.3601354500442535% 0.37643826683338494% 0.3927410836225164% 0.4116375303553733% 0.4297929399614515% 0.4464662753139723% 0.4623985735397144% 0.47796035320206715% 0.4942631699911986% 0.5120480610338874% 0.5313150263301337% 0.5487293988094332% 0.5646616970351753% 0.5798529581341387% 0.5965262934866595% 0.6135701474025697% 0.6332076312622053% 0.648769410924558% 0.6672953390940256% 0.6802634888126529% 0.6910085271509441% 0.7039766768695713% 0.7191679379685347% 0.7351002361942768% 0.7536261643637444% 0.7728931296599907% 0.7906780207026795% 0.8043872075480855% 0.8195784686470489% 0.835510766872791% 0.8540366950422585% 0.8725626232117261% 0.8899769956910256% 0.9081324052971038% 0.9236941849594565% 0.939997001748588% 0.9574113742278875% 0.9759373023973551% 0.9914990820597078% Done
[04:15:10] Finished 'download_xtensa' after 1.02 min
[04:15:10] Starting 'download_esptool'...
[gulp] Downloading https://raw.githubusercontent.com/espressif/esptool/master/esptool.py... Done
[04:15:11] Finished 'download_esptool' after 796 ms
[04:15:11] Starting 'decompress'...
[04:15:12] Finished 'decompress' after 1 s
[04:15:12] Starting 'chmod_linux'...
[04:15:12] Finished 'chmod_linux' after 12 ms
[04:15:12] Starting 'del'...
[04:15:12] Finished 'del' after 13 ms
[04:15:12] Starting 'build'...
[04:15:12] Finished 'build' after 31 μs
(base) ye@ykt-pro:~/tool/kbide$ 
```

## start

```
(base) ye@ykt-pro:~/tool/kbide$ npm start

> kidbrightide@1.6.0 start /home/ye/tool/kbide
> node index.js

2021-01-31 04:18:06	info	webserver listening on port 8000
```

## open server page

```
From your browser:
http://localhost:8000/home
```



## Reference

https://stackoverflow.com/questions/21406738/cant-get-gulp-to-run-cannot-find-module-gulp-util

