## Log of Running ViT with Keras

Create a new Anaconda environment ...  

```
(base) yekyaw.thu@gpu:~$ conda create -n vit python=3.8
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 22.9.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/vit

  added / updated specs:
    - python=3.8


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    ca-certificates-2022.10.11 |       h06a4308_0         124 KB
    certifi-2022.9.24          |   py38h06a4308_0         154 KB
    libffi-3.4.2               |       h295c915_4         124 KB
    openssl-1.1.1s             |       h7f8727e_0         3.6 MB
    pip-22.2.2                 |   py38h06a4308_0         2.3 MB
    python-3.8.15              |       h3fd9d12_0        20.1 MB
    setuptools-65.5.0          |   py38h06a4308_0         1.1 MB
    ------------------------------------------------------------
                                           Total:        27.5 MB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-5.1-1_gnu
  ca-certificates    pkgs/main/linux-64::ca-certificates-2022.10.11-h06a4308_0
  certifi            pkgs/main/linux-64::certifi-2022.9.24-py38h06a4308_0
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.38-h1181459_1
  libffi             pkgs/main/linux-64::libffi-3.4.2-h295c915_4
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-11.2.0-h1234567_1
  libgomp            pkgs/main/linux-64::libgomp-11.2.0-h1234567_1
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-11.2.0-h1234567_1
  ncurses            pkgs/main/linux-64::ncurses-6.3-h5eee18b_3
  openssl            pkgs/main/linux-64::openssl-1.1.1s-h7f8727e_0
  pip                pkgs/main/linux-64::pip-22.2.2-py38h06a4308_0
  python             pkgs/main/linux-64::python-3.8.15-h3fd9d12_0
  readline           pkgs/main/linux-64::readline-8.2-h5eee18b_0
  setuptools         pkgs/main/linux-64::setuptools-65.5.0-py38h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.39.3-h5082296_0
  tk                 pkgs/main/linux-64::tk-8.6.12-h1ccaba5_0
  wheel              pkgs/main/noarch::wheel-0.37.1-pyhd3eb1b0_0
  xz                 pkgs/main/linux-64::xz-5.2.6-h5eee18b_0
  zlib               pkgs/main/linux-64::zlib-1.2.13-h5eee18b_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
certifi-2022.9.24    | 154 KB    | ################################################################################### | 100%
pip-22.2.2           | 2.3 MB    | ################################################################################### | 100%
openssl-1.1.1s       | 3.6 MB    | ################################################################################### | 100%
ca-certificates-2022 | 124 KB    | ################################################################################### | 100%
setuptools-65.5.0    | 1.1 MB    | ################################################################################### | 100%
python-3.8.15        | 20.1 MB   | ################################################################################### | 100%
libffi-3.4.2         | 124 KB    | ################################################################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate vit
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) yekyaw.thu@gpu:~$
```

Entering into the new enviornment named "vit":   

```
(base) yekyaw.thu@gpu:~$ conda activate vit
(vit) yekyaw.thu@gpu:~$
```

Install Jupyter Notebook on GPU server:   

```
(vit) yekyaw.thu@gpu:~$ conda install jupyter
Collecting package metadata (current_repodata.json): done
Solving environment: |
The environment is inconsistent, please check the package plan carefully
The following packages are causing the inconsistency:

  - defaults/linux-64::tk==8.6.12=h1ccaba5_0
  - defaults/linux-64::ncurses==6.3=h5eee18b_3
  - defaults/linux-64::setuptools==65.5.0=py38h06a4308_0
  - defaults/linux-64::xz==5.2.6=h5eee18b_0
  - defaults/linux-64::libffi==3.4.2=h295c915_4
  - defaults/linux-64::python==3.8.15=h3fd9d12_0
  - defaults/linux-64::pip==22.2.2=py38h06a4308_0
  - defaults/linux-64::zlib==1.2.13=h5eee18b_0
  - defaults/linux-64::libgcc-ng==11.2.0=h1234567_1
  - defaults/linux-64::openssl==1.1.1s=h7f8727e_0
  - defaults/linux-64::readline==8.2=h5eee18b_0
  - defaults/linux-64::sqlite==3.39.3=h5082296_0
  - defaults/linux-64::certifi==2022.9.24=py38h06a4308_0
  - defaults/linux-64::libstdcxx-ng==11.2.0=h1234567_1
  - defaults/noarch::wheel==0.37.1=pyhd3eb1b0_0
done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 22.9.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/vit

  added / updated specs:
    - jupyter


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    anyio-3.5.0                |   py38h06a4308_0         165 KB
    argon2-cffi-21.3.0         |     pyhd3eb1b0_0          15 KB
    argon2-cffi-bindings-21.2.0|   py38h7f8727e_0          33 KB
    asttokens-2.0.5            |     pyhd3eb1b0_0          20 KB
    attrs-21.4.0               |     pyhd3eb1b0_0          51 KB
    babel-2.9.1                |     pyhd3eb1b0_0         5.5 MB
    backcall-0.2.0             |     pyhd3eb1b0_0          13 KB
    beautifulsoup4-4.11.1      |   py38h06a4308_0         185 KB
    bleach-4.1.0               |     pyhd3eb1b0_0         123 KB
    brotlipy-0.7.0             |py38h27cfd23_1003         323 KB
    cffi-1.15.1                |   py38h74dc2b5_0         228 KB
    charset-normalizer-2.0.4   |     pyhd3eb1b0_0          35 KB
    cryptography-38.0.1        |   py38h9ce1e76_0         1.3 MB
    dbus-1.13.18               |       hb2f20db_0         504 KB
    debugpy-1.5.1              |   py38h295c915_0         1.7 MB
    decorator-5.1.1            |     pyhd3eb1b0_0          12 KB
    defusedxml-0.7.1           |     pyhd3eb1b0_0          23 KB
    entrypoints-0.4            |   py38h06a4308_0          16 KB
    executing-0.8.3            |     pyhd3eb1b0_0          18 KB
    expat-2.4.9                |       h6a678d5_0         156 KB
    fontconfig-2.13.1          |       hef1e5e3_1         260 KB
    freetype-2.12.1            |       h4a9f257_0         626 KB
    giflib-5.2.1               |       h7b6447c_0          78 KB
    glib-2.69.1                |       h4ff587b_1         1.7 MB
    gst-plugins-base-1.14.0    |       h8213a91_2         4.9 MB
    gstreamer-1.14.0           |       h28cd5cc_2         3.2 MB
    icu-58.2                   |       he6710b0_3        10.5 MB
    idna-3.4                   |   py38h06a4308_0          93 KB
    importlib-metadata-4.11.3  |   py38h06a4308_0          40 KB
    importlib_resources-5.2.0  |     pyhd3eb1b0_1          21 KB
    ipykernel-6.15.2           |   py38h06a4308_0         190 KB
    ipython-8.6.0              |   py38h06a4308_0         1.0 MB
    ipython_genutils-0.2.0     |     pyhd3eb1b0_1          27 KB
    ipywidgets-7.6.5           |     pyhd3eb1b0_1         105 KB
    jedi-0.18.1                |   py38h06a4308_1         982 KB
    jinja2-3.1.2               |   py38h06a4308_0         211 KB
    jpeg-9e                    |       h7f8727e_0         240 KB
    json5-0.9.6                |     pyhd3eb1b0_0          21 KB
    jsonschema-4.16.0          |   py38h06a4308_0         128 KB
    jupyter-1.0.0              |   py38h06a4308_8           7 KB
    jupyter_client-7.3.5       |   py38h06a4308_0         192 KB
    jupyter_console-6.4.3      |     pyhd3eb1b0_0          23 KB
    jupyter_core-4.11.2        |   py38h06a4308_0          80 KB
    jupyter_server-1.18.1      |   py38h06a4308_0         356 KB
    jupyterlab-3.4.4           |   py38h06a4308_0         3.7 MB
    jupyterlab_pygments-0.1.2  |             py_0           8 KB
    jupyterlab_server-2.15.2   |   py38h06a4308_0          75 KB
    jupyterlab_widgets-1.0.0   |     pyhd3eb1b0_1         109 KB
    krb5-1.19.2                |       hac12032_0         1.2 MB
    lerc-3.0                   |       h295c915_0         196 KB
    libclang-10.0.1            |default_hb85057a_2        10.8 MB
    libdeflate-1.8             |       h7f8727e_5          51 KB
    libedit-3.1.20210910       |       h7f8727e_0         166 KB
    libevent-2.1.12            |       h8f2d780_0         425 KB
    libllvm10-10.0.1           |       hbcb73fb_5        22.1 MB
    libpq-12.9                 |       h16c4e8d_3         2.1 MB
    libsodium-1.0.18           |       h7b6447c_0         244 KB
    libtiff-4.4.0              |       hecacb30_2         526 KB
    libuuid-1.41.5             |       h5eee18b_0          27 KB
    libwebp-1.2.4              |       h11a3e52_0          79 KB
    libwebp-base-1.2.4         |       h5eee18b_0         347 KB
    libxcb-1.15                |       h7f8727e_0         505 KB
    libxkbcommon-1.0.1         |       hfa300c1_0         483 KB
    libxml2-2.9.14             |       h74e7548_0         718 KB
    libxslt-1.1.35             |       h4e12654_0         453 KB
    lxml-4.9.1                 |   py38h1edc446_0         1.3 MB
    lz4-c-1.9.3                |       h295c915_1         185 KB
    markupsafe-2.1.1           |   py38h7f8727e_0          21 KB
    matplotlib-inline-0.1.6    |   py38h06a4308_0          16 KB
    mistune-0.8.4              |py38h7b6447c_1000          55 KB
    nbclassic-0.4.8            |   py38h06a4308_0         5.8 MB
    nbclient-0.5.13            |   py38h06a4308_0          91 KB
    nbconvert-6.5.4            |   py38h06a4308_0         513 KB
    nbformat-5.5.0             |   py38h06a4308_0         128 KB
    nest-asyncio-1.5.5         |   py38h06a4308_0          16 KB
    notebook-6.5.2             |   py38h06a4308_0         510 KB
    notebook-shim-0.2.2        |   py38h06a4308_0          22 KB
    nspr-4.33                  |       h295c915_0         222 KB
    nss-3.74                   |       h0370c37_0         1.9 MB
    packaging-21.3             |     pyhd3eb1b0_0          36 KB
    pandocfilters-1.5.0        |     pyhd3eb1b0_0          11 KB
    parso-0.8.3                |     pyhd3eb1b0_0          70 KB
    pcre-8.45                  |       h295c915_0         207 KB
    pexpect-4.8.0              |     pyhd3eb1b0_3          53 KB
    pickleshare-0.7.5          |  pyhd3eb1b0_1003          13 KB
    pkgutil-resolve-name-1.3.10|   py38h06a4308_0           9 KB
    ply-3.11                   |           py38_0          81 KB
    prometheus_client-0.14.1   |   py38h06a4308_0          90 KB
    prompt-toolkit-3.0.20      |     pyhd3eb1b0_0         259 KB
    prompt_toolkit-3.0.20      |       hd3eb1b0_0          12 KB
    psutil-5.9.0               |   py38h5eee18b_0         330 KB
    ptyprocess-0.7.0           |     pyhd3eb1b0_2          17 KB
    pure_eval-0.2.2            |     pyhd3eb1b0_0          14 KB
    pycparser-2.21             |     pyhd3eb1b0_0          94 KB
    pygments-2.11.2            |     pyhd3eb1b0_0         759 KB
    pyopenssl-22.0.0           |     pyhd3eb1b0_0          50 KB
    pyparsing-3.0.9            |   py38h06a4308_0         152 KB
    pyqt-5.15.7                |   py38h6a678d5_1         5.1 MB
    pyqt5-sip-12.11.0          |   py38h6a678d5_1          87 KB
    pyrsistent-0.18.0          |   py38heee7806_0          94 KB
    pysocks-1.7.1              |   py38h06a4308_0          31 KB
    python-3.8.13              |       haa1d7c7_1        20.2 MB
    python-dateutil-2.8.2      |     pyhd3eb1b0_0         233 KB
    python-fastjsonschema-2.16.2|   py38h06a4308_0         230 KB
    pytz-2022.1                |   py38h06a4308_0         196 KB
    pyzmq-23.2.0               |   py38h6a678d5_0         448 KB
    qt-main-5.15.2             |       h327a75a_7        45.1 MB
    qt-webengine-5.15.9        |       hd2b0992_4        47.1 MB
    qtconsole-5.3.2            |   py38h06a4308_0         176 KB
    qtpy-2.2.0                 |   py38h06a4308_0          84 KB
    qtwebkit-5.212             |       h4eab89a_4        14.3 MB
    requests-2.28.1            |   py38h06a4308_0          92 KB
    send2trash-1.8.0           |     pyhd3eb1b0_1          19 KB
    sip-6.6.2                  |   py38h6a678d5_0         425 KB
    six-1.16.0                 |     pyhd3eb1b0_1          18 KB
    sniffio-1.2.0              |   py38h06a4308_1          15 KB
    soupsieve-2.3.2.post1      |   py38h06a4308_0          65 KB
    stack_data-0.2.0           |     pyhd3eb1b0_0          22 KB
    terminado-0.13.1           |   py38h06a4308_0          30 KB
    tinycss2-1.2.1             |   py38h06a4308_0          40 KB
    toml-0.10.2                |     pyhd3eb1b0_0          20 KB
    tornado-6.2                |   py38h5eee18b_0         590 KB
    traitlets-5.1.1            |     pyhd3eb1b0_0          84 KB
    typing-extensions-4.3.0    |   py38h06a4308_0           9 KB
    typing_extensions-4.3.0    |   py38h06a4308_0          42 KB
    urllib3-1.26.12            |   py38h06a4308_0         182 KB
    wcwidth-0.2.5              |     pyhd3eb1b0_0          26 KB
    webencodings-0.5.1         |           py38_1          20 KB
    websocket-client-0.58.0    |   py38h06a4308_4          66 KB
    widgetsnbextension-3.5.2   |   py38h06a4308_0         651 KB
    zeromq-4.3.4               |       h2531618_0         331 KB
    zipp-3.8.0                 |   py38h06a4308_0          15 KB
    zstd-1.5.2                 |       ha4553b6_0         488 KB
    ------------------------------------------------------------
                                           Total:       228.9 MB

The following NEW packages will be INSTALLED:

  anyio              pkgs/main/linux-64::anyio-3.5.0-py38h06a4308_0
  argon2-cffi        pkgs/main/noarch::argon2-cffi-21.3.0-pyhd3eb1b0_0
  argon2-cffi-bindi~ pkgs/main/linux-64::argon2-cffi-bindings-21.2.0-py38h7f8727e_0
  asttokens          pkgs/main/noarch::asttokens-2.0.5-pyhd3eb1b0_0
  attrs              pkgs/main/noarch::attrs-21.4.0-pyhd3eb1b0_0
  babel              pkgs/main/noarch::babel-2.9.1-pyhd3eb1b0_0
  backcall           pkgs/main/noarch::backcall-0.2.0-pyhd3eb1b0_0
  beautifulsoup4     pkgs/main/linux-64::beautifulsoup4-4.11.1-py38h06a4308_0
  bleach             pkgs/main/noarch::bleach-4.1.0-pyhd3eb1b0_0
  brotlipy           pkgs/main/linux-64::brotlipy-0.7.0-py38h27cfd23_1003
  cffi               pkgs/main/linux-64::cffi-1.15.1-py38h74dc2b5_0
  charset-normalizer pkgs/main/noarch::charset-normalizer-2.0.4-pyhd3eb1b0_0
  cryptography       pkgs/main/linux-64::cryptography-38.0.1-py38h9ce1e76_0
  dbus               pkgs/main/linux-64::dbus-1.13.18-hb2f20db_0
  debugpy            pkgs/main/linux-64::debugpy-1.5.1-py38h295c915_0
  decorator          pkgs/main/noarch::decorator-5.1.1-pyhd3eb1b0_0
  defusedxml         pkgs/main/noarch::defusedxml-0.7.1-pyhd3eb1b0_0
  entrypoints        pkgs/main/linux-64::entrypoints-0.4-py38h06a4308_0
  executing          pkgs/main/noarch::executing-0.8.3-pyhd3eb1b0_0
  expat              pkgs/main/linux-64::expat-2.4.9-h6a678d5_0
  fontconfig         pkgs/main/linux-64::fontconfig-2.13.1-hef1e5e3_1
  freetype           pkgs/main/linux-64::freetype-2.12.1-h4a9f257_0
  giflib             pkgs/main/linux-64::giflib-5.2.1-h7b6447c_0
  glib               pkgs/main/linux-64::glib-2.69.1-h4ff587b_1
  gst-plugins-base   pkgs/main/linux-64::gst-plugins-base-1.14.0-h8213a91_2
  gstreamer          pkgs/main/linux-64::gstreamer-1.14.0-h28cd5cc_2
  icu                pkgs/main/linux-64::icu-58.2-he6710b0_3
  idna               pkgs/main/linux-64::idna-3.4-py38h06a4308_0
  importlib-metadata pkgs/main/linux-64::importlib-metadata-4.11.3-py38h06a4308_0
  importlib_resourc~ pkgs/main/noarch::importlib_resources-5.2.0-pyhd3eb1b0_1
  ipykernel          pkgs/main/linux-64::ipykernel-6.15.2-py38h06a4308_0
  ipython            pkgs/main/linux-64::ipython-8.6.0-py38h06a4308_0
  ipython_genutils   pkgs/main/noarch::ipython_genutils-0.2.0-pyhd3eb1b0_1
  ipywidgets         pkgs/main/noarch::ipywidgets-7.6.5-pyhd3eb1b0_1
  jedi               pkgs/main/linux-64::jedi-0.18.1-py38h06a4308_1
  jinja2             pkgs/main/linux-64::jinja2-3.1.2-py38h06a4308_0
  jpeg               pkgs/main/linux-64::jpeg-9e-h7f8727e_0
  json5              pkgs/main/noarch::json5-0.9.6-pyhd3eb1b0_0
  jsonschema         pkgs/main/linux-64::jsonschema-4.16.0-py38h06a4308_0
  jupyter            pkgs/main/linux-64::jupyter-1.0.0-py38h06a4308_8
  jupyter_client     pkgs/main/linux-64::jupyter_client-7.3.5-py38h06a4308_0
  jupyter_console    pkgs/main/noarch::jupyter_console-6.4.3-pyhd3eb1b0_0
  jupyter_core       pkgs/main/linux-64::jupyter_core-4.11.2-py38h06a4308_0
  jupyter_server     pkgs/main/linux-64::jupyter_server-1.18.1-py38h06a4308_0
  jupyterlab         pkgs/main/linux-64::jupyterlab-3.4.4-py38h06a4308_0
  jupyterlab_pygmen~ pkgs/main/noarch::jupyterlab_pygments-0.1.2-py_0
  jupyterlab_server  pkgs/main/linux-64::jupyterlab_server-2.15.2-py38h06a4308_0
  jupyterlab_widgets pkgs/main/noarch::jupyterlab_widgets-1.0.0-pyhd3eb1b0_1
  krb5               pkgs/main/linux-64::krb5-1.19.2-hac12032_0
  lerc               pkgs/main/linux-64::lerc-3.0-h295c915_0
  libclang           pkgs/main/linux-64::libclang-10.0.1-default_hb85057a_2
  libdeflate         pkgs/main/linux-64::libdeflate-1.8-h7f8727e_5
  libedit            pkgs/main/linux-64::libedit-3.1.20210910-h7f8727e_0
  libevent           pkgs/main/linux-64::libevent-2.1.12-h8f2d780_0
  libllvm10          pkgs/main/linux-64::libllvm10-10.0.1-hbcb73fb_5
  libpng             pkgs/main/linux-64::libpng-1.6.37-hbc83047_0
  libpq              pkgs/main/linux-64::libpq-12.9-h16c4e8d_3
  libsodium          pkgs/main/linux-64::libsodium-1.0.18-h7b6447c_0
  libtiff            pkgs/main/linux-64::libtiff-4.4.0-hecacb30_2
  libuuid            pkgs/main/linux-64::libuuid-1.41.5-h5eee18b_0
  libwebp            pkgs/main/linux-64::libwebp-1.2.4-h11a3e52_0
  libwebp-base       pkgs/main/linux-64::libwebp-base-1.2.4-h5eee18b_0
  libxcb             pkgs/main/linux-64::libxcb-1.15-h7f8727e_0
  libxkbcommon       pkgs/main/linux-64::libxkbcommon-1.0.1-hfa300c1_0
  libxml2            pkgs/main/linux-64::libxml2-2.9.14-h74e7548_0
  libxslt            pkgs/main/linux-64::libxslt-1.1.35-h4e12654_0
  lxml               pkgs/main/linux-64::lxml-4.9.1-py38h1edc446_0
  lz4-c              pkgs/main/linux-64::lz4-c-1.9.3-h295c915_1
  markupsafe         pkgs/main/linux-64::markupsafe-2.1.1-py38h7f8727e_0
  matplotlib-inline  pkgs/main/linux-64::matplotlib-inline-0.1.6-py38h06a4308_0
  mistune            pkgs/main/linux-64::mistune-0.8.4-py38h7b6447c_1000
  nbclassic          pkgs/main/linux-64::nbclassic-0.4.8-py38h06a4308_0
  nbclient           pkgs/main/linux-64::nbclient-0.5.13-py38h06a4308_0
  nbconvert          pkgs/main/linux-64::nbconvert-6.5.4-py38h06a4308_0
  nbformat           pkgs/main/linux-64::nbformat-5.5.0-py38h06a4308_0
  nest-asyncio       pkgs/main/linux-64::nest-asyncio-1.5.5-py38h06a4308_0
  notebook           pkgs/main/linux-64::notebook-6.5.2-py38h06a4308_0
  notebook-shim      pkgs/main/linux-64::notebook-shim-0.2.2-py38h06a4308_0
  nspr               pkgs/main/linux-64::nspr-4.33-h295c915_0
  nss                pkgs/main/linux-64::nss-3.74-h0370c37_0
  packaging          pkgs/main/noarch::packaging-21.3-pyhd3eb1b0_0
  pandocfilters      pkgs/main/noarch::pandocfilters-1.5.0-pyhd3eb1b0_0
  parso              pkgs/main/noarch::parso-0.8.3-pyhd3eb1b0_0
  pcre               pkgs/main/linux-64::pcre-8.45-h295c915_0
  pexpect            pkgs/main/noarch::pexpect-4.8.0-pyhd3eb1b0_3
  pickleshare        pkgs/main/noarch::pickleshare-0.7.5-pyhd3eb1b0_1003
  pkgutil-resolve-n~ pkgs/main/linux-64::pkgutil-resolve-name-1.3.10-py38h06a4308_0
  ply                pkgs/main/linux-64::ply-3.11-py38_0
  prometheus_client  pkgs/main/linux-64::prometheus_client-0.14.1-py38h06a4308_0
  prompt-toolkit     pkgs/main/noarch::prompt-toolkit-3.0.20-pyhd3eb1b0_0
  prompt_toolkit     pkgs/main/noarch::prompt_toolkit-3.0.20-hd3eb1b0_0
  psutil             pkgs/main/linux-64::psutil-5.9.0-py38h5eee18b_0
  ptyprocess         pkgs/main/noarch::ptyprocess-0.7.0-pyhd3eb1b0_2
  pure_eval          pkgs/main/noarch::pure_eval-0.2.2-pyhd3eb1b0_0
  pycparser          pkgs/main/noarch::pycparser-2.21-pyhd3eb1b0_0
  pygments           pkgs/main/noarch::pygments-2.11.2-pyhd3eb1b0_0
  pyopenssl          pkgs/main/noarch::pyopenssl-22.0.0-pyhd3eb1b0_0
  pyparsing          pkgs/main/linux-64::pyparsing-3.0.9-py38h06a4308_0
  pyqt               pkgs/main/linux-64::pyqt-5.15.7-py38h6a678d5_1
  pyqt5-sip          pkgs/main/linux-64::pyqt5-sip-12.11.0-py38h6a678d5_1
  pyrsistent         pkgs/main/linux-64::pyrsistent-0.18.0-py38heee7806_0
  pysocks            pkgs/main/linux-64::pysocks-1.7.1-py38h06a4308_0
  python-dateutil    pkgs/main/noarch::python-dateutil-2.8.2-pyhd3eb1b0_0
  python-fastjsonsc~ pkgs/main/linux-64::python-fastjsonschema-2.16.2-py38h06a4308_0
  pytz               pkgs/main/linux-64::pytz-2022.1-py38h06a4308_0
  pyzmq              pkgs/main/linux-64::pyzmq-23.2.0-py38h6a678d5_0
  qt-main            pkgs/main/linux-64::qt-main-5.15.2-h327a75a_7
  qt-webengine       pkgs/main/linux-64::qt-webengine-5.15.9-hd2b0992_4
  qtconsole          pkgs/main/linux-64::qtconsole-5.3.2-py38h06a4308_0
  qtpy               pkgs/main/linux-64::qtpy-2.2.0-py38h06a4308_0
  qtwebkit           pkgs/main/linux-64::qtwebkit-5.212-h4eab89a_4
  requests           pkgs/main/linux-64::requests-2.28.1-py38h06a4308_0
  send2trash         pkgs/main/noarch::send2trash-1.8.0-pyhd3eb1b0_1
  sip                pkgs/main/linux-64::sip-6.6.2-py38h6a678d5_0
  six                pkgs/main/noarch::six-1.16.0-pyhd3eb1b0_1
  sniffio            pkgs/main/linux-64::sniffio-1.2.0-py38h06a4308_1
  soupsieve          pkgs/main/linux-64::soupsieve-2.3.2.post1-py38h06a4308_0
  stack_data         pkgs/main/noarch::stack_data-0.2.0-pyhd3eb1b0_0
  terminado          pkgs/main/linux-64::terminado-0.13.1-py38h06a4308_0
  tinycss2           pkgs/main/linux-64::tinycss2-1.2.1-py38h06a4308_0
  toml               pkgs/main/noarch::toml-0.10.2-pyhd3eb1b0_0
  tornado            pkgs/main/linux-64::tornado-6.2-py38h5eee18b_0
  traitlets          pkgs/main/noarch::traitlets-5.1.1-pyhd3eb1b0_0
  typing-extensions  pkgs/main/linux-64::typing-extensions-4.3.0-py38h06a4308_0
  typing_extensions  pkgs/main/linux-64::typing_extensions-4.3.0-py38h06a4308_0
  urllib3            pkgs/main/linux-64::urllib3-1.26.12-py38h06a4308_0
  wcwidth            pkgs/main/noarch::wcwidth-0.2.5-pyhd3eb1b0_0
  webencodings       pkgs/main/linux-64::webencodings-0.5.1-py38_1
  websocket-client   pkgs/main/linux-64::websocket-client-0.58.0-py38h06a4308_4
  widgetsnbextension pkgs/main/linux-64::widgetsnbextension-3.5.2-py38h06a4308_0
  zeromq             pkgs/main/linux-64::zeromq-4.3.4-h2531618_0
  zipp               pkgs/main/linux-64::zipp-3.8.0-py38h06a4308_0
  zstd               pkgs/main/linux-64::zstd-1.5.2-ha4553b6_0

The following packages will be DOWNGRADED:

  libffi                                   3.4.2-h295c915_4 --> 3.3-he6710b0_2
  python                                  3.8.15-h3fd9d12_0 --> 3.8.13-haa1d7c7_1


Proceed ([y]/n)? y


Downloading and Extracting Packages
websocket-client-0.5 | 66 KB     | ################################################################################### | 100%
json5-0.9.6          | 21 KB     | ################################################################################### | 100%
qtwebkit-5.212       | 14.3 MB   | ################################################################################### | 100%
toml-0.10.2          | 20 KB     | ################################################################################### | 100%
pygments-2.11.2      | 759 KB    | ################################################################################### | 100%
jpeg-9e              | 240 KB    | ################################################################################### | 100%
ipython_genutils-0.2 | 27 KB     | ################################################################################### | 100%
prompt_toolkit-3.0.2 | 12 KB     | ################################################################################### | 100%
soupsieve-2.3.2.post | 65 KB     | ################################################################################### | 100%
jupyterlab_server-2. | 75 KB     | ################################################################################### | 100%
argon2-cffi-bindings | 33 KB     | ################################################################################### | 100%
dbus-1.13.18         | 504 KB    | ################################################################################### | 100%
python-dateutil-2.8. | 233 KB    | ################################################################################### | 100%
pycparser-2.21       | 94 KB     | ################################################################################### | 100%
pyrsistent-0.18.0    | 94 KB     | ################################################################################### | 100%
psutil-5.9.0         | 330 KB    | ################################################################################### | 100%
mistune-0.8.4        | 55 KB     | ################################################################################### | 100%
jupyter_core-4.11.2  | 80 KB     | ################################################################################### | 100%
libwebp-1.2.4        | 79 KB     | ################################################################################### | 100%
zeromq-4.3.4         | 331 KB    | ################################################################################### | 100%
pyqt-5.15.7          | 5.1 MB    | ################################################################################### | 100%
executing-0.8.3      | 18 KB     | ################################################################################### | 100%
packaging-21.3       | 36 KB     | ################################################################################### | 100%
urllib3-1.26.12      | 182 KB    | ################################################################################### | 100%
sniffio-1.2.0        | 15 KB     | ################################################################################### | 100%
pkgutil-resolve-name | 9 KB      | ################################################################################### | 100%
jupyterlab_widgets-1 | 109 KB    | ################################################################################### | 100%
nbformat-5.5.0       | 128 KB    | ################################################################################### | 100%
importlib_resources- | 21 KB     | ################################################################################### | 100%
jinja2-3.1.2         | 211 KB    | ################################################################################### | 100%
gstreamer-1.14.0     | 3.2 MB    | ################################################################################### | 100%
stack_data-0.2.0     | 22 KB     | ################################################################################### | 100%
qtpy-2.2.0           | 84 KB     | ################################################################################### | 100%
backcall-0.2.0       | 13 KB     | ################################################################################### | 100%
matplotlib-inline-0. | 16 KB     | ################################################################################### | 100%
pandocfilters-1.5.0  | 11 KB     | ################################################################################### | 100%
libpq-12.9           | 2.1 MB    | ################################################################################### | 100%
jupyterlab-3.4.4     | 3.7 MB    | ################################################################################### | 100%
pexpect-4.8.0        | 53 KB     | ################################################################################### | 100%
nss-3.74             | 1.9 MB    | ################################################################################### | 100%
jupyter_console-6.4. | 23 KB     | ################################################################################### | 100%
pyopenssl-22.0.0     | 50 KB     | ################################################################################### | 100%
entrypoints-0.4      | 16 KB     | ################################################################################### | 100%
anyio-3.5.0          | 165 KB    | ################################################################################### | 100%
libsodium-1.0.18     | 244 KB    | ################################################################################### | 100%
nspr-4.33            | 222 KB    | ################################################################################### | 100%
freetype-2.12.1      | 626 KB    | ################################################################################### | 100%
jsonschema-4.16.0    | 128 KB    | ################################################################################### | 100%
idna-3.4             | 93 KB     | ################################################################################### | 100%
libxslt-1.1.35       | 453 KB    | ################################################################################### | 100%
jupyter_client-7.3.5 | 192 KB    | ################################################################################### | 100%
pytz-2022.1          | 196 KB    | ################################################################################### | 100%
libllvm10-10.0.1     | 22.1 MB   | ################################################################################### | 100%
pure_eval-0.2.2      | 14 KB     | ################################################################################### | 100%
libxkbcommon-1.0.1   | 483 KB    | ################################################################################### | 100%
nest-asyncio-1.5.5   | 16 KB     | ################################################################################### | 100%
libdeflate-1.8       | 51 KB     | ################################################################################### | 100%
cffi-1.15.1          | 228 KB    | ################################################################################### | 100%
qt-main-5.15.2       | 45.1 MB   | ################################################################################### | 100%
expat-2.4.9          | 156 KB    | ################################################################################### | 100%
send2trash-1.8.0     | 19 KB     | ################################################################################### | 100%
notebook-shim-0.2.2  | 22 KB     | ################################################################################### | 100%
importlib-metadata-4 | 40 KB     | ################################################################################### | 100%
libxcb-1.15          | 505 KB    | ################################################################################### | 100%
libxml2-2.9.14       | 718 KB    | ################################################################################### | 100%
nbclassic-0.4.8      | 5.8 MB    | ################################################################################### | 100%
asttokens-2.0.5      | 20 KB     | ################################################################################### | 100%
debugpy-1.5.1        | 1.7 MB    | ################################################################################### | 100%
argon2-cffi-21.3.0   | 15 KB     | ################################################################################### | 100%
gst-plugins-base-1.1 | 4.9 MB    | ################################################################################### | 100%
decorator-5.1.1      | 12 KB     | ################################################################################### | 100%
brotlipy-0.7.0       | 323 KB    | ################################################################################### | 100%
libuuid-1.41.5       | 27 KB     | ################################################################################### | 100%
widgetsnbextension-3 | 651 KB    | ################################################################################### | 100%
pickleshare-0.7.5    | 13 KB     | ################################################################################### | 100%
typing_extensions-4. | 42 KB     | ################################################################################### | 100%
zipp-3.8.0           | 15 KB     | ################################################################################### | 100%
terminado-0.13.1     | 30 KB     | ################################################################################### | 100%
lz4-c-1.9.3          | 185 KB    | ################################################################################### | 100%
parso-0.8.3          | 70 KB     | ################################################################################### | 100%
pysocks-1.7.1        | 31 KB     | ################################################################################### | 100%
nbclient-0.5.13      | 91 KB     | ################################################################################### | 100%
tinycss2-1.2.1       | 40 KB     | ################################################################################### | 100%
bleach-4.1.0         | 123 KB    | ################################################################################### | 100%
libtiff-4.4.0        | 526 KB    | ################################################################################### | 100%
requests-2.28.1      | 92 KB     | ################################################################################### | 100%
prompt-toolkit-3.0.2 | 259 KB    | ################################################################################### | 100%
libclang-10.0.1      | 10.8 MB   | ################################################################################### | 100%
nbconvert-6.5.4      | 513 KB    | ################################################################################### | 100%
cryptography-38.0.1  | 1.3 MB    | ################################################################################### | 100%
babel-2.9.1          | 5.5 MB    | ################################################################################### | 100%
libedit-3.1.20210910 | 166 KB    | ################################################################################### | 100%
pyparsing-3.0.9      | 152 KB    | ################################################################################### | 100%
prometheus_client-0. | 90 KB     | ################################################################################### | 100%
ipykernel-6.15.2     | 190 KB    | ################################################################################### | 100%
typing-extensions-4. | 9 KB      | ################################################################################### | 100%
charset-normalizer-2 | 35 KB     | ################################################################################### | 100%
lxml-4.9.1           | 1.3 MB    | ################################################################################### | 100%
six-1.16.0           | 18 KB     | ################################################################################### | 100%
webencodings-0.5.1   | 20 KB     | ################################################################################### | 100%
ipython-8.6.0        | 1.0 MB    | ################################################################################### | 100%
sip-6.6.2            | 425 KB    | ################################################################################### | 100%
python-fastjsonschem | 230 KB    | ################################################################################### | 100%
libevent-2.1.12      | 425 KB    | ################################################################################### | 100%
pcre-8.45            | 207 KB    | ################################################################################### | 100%
glib-2.69.1          | 1.7 MB    | ################################################################################### | 100%
jupyter-1.0.0        | 7 KB      | ################################################################################### | 100%
beautifulsoup4-4.11. | 185 KB    | ################################################################################### | 100%
krb5-1.19.2          | 1.2 MB    | ################################################################################### | 100%
ipywidgets-7.6.5     | 105 KB    | ################################################################################### | 100%
pyzmq-23.2.0         | 448 KB    | ################################################################################### | 100%
wcwidth-0.2.5        | 26 KB     | ################################################################################### | 100%
libwebp-base-1.2.4   | 347 KB    | ################################################################################### | 100%
jupyterlab_pygments- | 8 KB      | ################################################################################### | 100%
fontconfig-2.13.1    | 260 KB    | ################################################################################### | 100%
qt-webengine-5.15.9  | 47.1 MB   | ################################################################################### | 100%
lerc-3.0             | 196 KB    | ################################################################################### | 100%
giflib-5.2.1         | 78 KB     | ################################################################################### | 100%
ptyprocess-0.7.0     | 17 KB     | ################################################################################### | 100%
python-3.8.13        | 20.2 MB   | ################################################################################### | 100%
markupsafe-2.1.1     | 21 KB     | ################################################################################### | 100%
defusedxml-0.7.1     | 23 KB     | ################################################################################### | 100%
notebook-6.5.2       | 510 KB    | ################################################################################### | 100%
traitlets-5.1.1      | 84 KB     | ################################################################################### | 100%
tornado-6.2          | 590 KB    | ################################################################################### | 100%
pyqt5-sip-12.11.0    | 87 KB     | ################################################################################### | 100%
icu-58.2             | 10.5 MB   | ################################################################################### | 100%
ply-3.11             | 81 KB     | ################################################################################### | 100%
attrs-21.4.0         | 51 KB     | ################################################################################### | 100%
jupyter_server-1.18. | 356 KB    | ################################################################################### | 100%
qtconsole-5.3.2      | 176 KB    | ################################################################################### | 100%
zstd-1.5.2           | 488 KB    | ################################################################################### | 100%
jedi-0.18.1          | 982 KB    | ################################################################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(vit) yekyaw.thu@gpu:~$
```

Keep doing installation ...   

```
(vit) yekyaw.thu@gpu:~$ conda install -n base nb_conda_kernels
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /opt/anaconda/anaconda3

  added / updated specs:
    - nb_conda_kernels


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    nb_conda_kernels-2.3.1     |   py37h06a4308_0          27 KB
    ------------------------------------------------------------
                                           Total:          27 KB

The following NEW packages will be INSTALLED:

  nb_conda_kernels   pkgs/main/linux-64::nb_conda_kernels-2.3.1-py37h06a4308_0

The following packages will be UPDATED:

  conda                                        4.8.2-py37_0 --> 22.9.0-py37h06a4308_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
nb_conda_kernels-2.3 | 27 KB     | ################################################################################### | 100%
Preparing transaction: done
Verifying transaction: failed

EnvironmentNotWritableError: The current user does not have write permissions to the target environment.
  environment location: /opt/anaconda/anaconda3
  uid: 804601154
  gid: 804600513


(vit) yekyaw.thu@gpu:~$
```

Got error as shown in above!   

## Running Jupyter on Remote Server

On GPU server side:  

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

Actual running command is as follows:  
  
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

Access with my local browser:    

http://localhost:8080/tree  


## Install Python Libraries

Install numpy ...   

```
(vit) yekyaw.thu@gpu:~$ pip install numpy
Collecting numpy
  Downloading numpy-1.23.4-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (17.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 17.1/17.1 MB 1.1 MB/s eta 0:00:00
Installing collected packages: numpy
Successfully installed numpy-1.23.4
(vit) yekyaw.thu@gpu:~$
```

Install matplotlib ...  

```
(vit) yekyaw.thu@gpu:~$ pip install matplotlib
Collecting matplotlib
  Downloading matplotlib-3.6.2-cp38-cp38-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (9.4 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 9.4/9.4 MB 1.2 MB/s eta 0:00:00
Requirement already satisfied: pyparsing>=2.2.1 in ./.conda/envs/vit/lib/python3.8/site-packages (from matplotlib) (3.0.9)
Requirement already satisfied: packaging>=20.0 in ./.conda/envs/vit/lib/python3.8/site-packages (from matplotlib) (21.3)
Requirement already satisfied: python-dateutil>=2.7 in ./.conda/envs/vit/lib/python3.8/site-packages (from matplotlib) (2.8.2)
Collecting cycler>=0.10
  Using cached cycler-0.11.0-py3-none-any.whl (6.4 kB)
Requirement already satisfied: numpy>=1.19 in ./.conda/envs/vit/lib/python3.8/site-packages (from matplotlib) (1.23.4)
Collecting fonttools>=4.22.0
  Using cached fonttools-4.38.0-py3-none-any.whl (965 kB)
Collecting contourpy>=1.0.1
  Downloading contourpy-1.0.6-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (295 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 296.0/296.0 kB 1.1 MB/s eta 0:00:00
Collecting pillow>=6.2.0
  Downloading Pillow-9.3.0-cp38-cp38-manylinux_2_28_x86_64.whl (3.3 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.3/3.3 MB 598.5 kB/s eta 0:00:00
Collecting kiwisolver>=1.0.1
  Downloading kiwisolver-1.4.4-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.whl (1.2 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.2/1.2 MB 557.4 kB/s eta 0:00:00
Requirement already satisfied: six>=1.5 in ./.conda/envs/vit/lib/python3.8/site-packages (from python-dateutil>=2.7->matplotlib) (1.16.0)
Installing collected packages: pillow, kiwisolver, fonttools, cycler, contourpy, matplotlib
Successfully installed contourpy-1.0.6 cycler-0.11.0 fonttools-4.38.0 kiwisolver-1.4.4 matplotlib-3.6.2 pillow-9.3.0
(vit) yekyaw.thu@gpu:~$
```

Upgrading the pip ...  

```
(vit) yekyaw.thu@gpu:~$ pip install --upgrade pip
Requirement already satisfied: pip in ./.conda/envs/vit/lib/python3.8/site-packages (22.2.2)
Collecting pip
  Downloading pip-22.3.1-py3-none-any.whl (2.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.1/2.1 MB 1.4 MB/s eta 0:00:00
Installing collected packages: pip
  Attempting uninstall: pip
    Found existing installation: pip 22.2.2
    Uninstalling pip-22.2.2:
      Successfully uninstalled pip-22.2.2
Successfully installed pip-22.3.1
(vit) yekyaw.thu@gpu:~$
```

Tensorflow Installation:  

```
(vit) yekyaw.thu@gpu:~$ pip install tensorflow
Collecting tensorflow
  Downloading tensorflow-2.10.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (578.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 578.1/578.1 MB 150.6 kB/s eta 0:00:00
Collecting opt-einsum>=2.3.2
  Downloading opt_einsum-3.3.0-py3-none-any.whl (65 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 65.5/65.5 kB 39.2 kB/s eta 0:00:00
Collecting tensorflow-io-gcs-filesystem>=0.23.1
  Downloading tensorflow_io_gcs_filesystem-0.27.0-cp38-cp38-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (2.4 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.4/2.4 MB 710.6 kB/s eta 0:00:00
Requirement already satisfied: packaging in ./.conda/envs/vit/lib/python3.8/site-packages (from tensorflow) (21.3)
Collecting absl-py>=1.0.0
  Downloading absl_py-1.3.0-py3-none-any.whl (124 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 124.6/124.6 kB 190.6 kB/s eta 0:00:00
Collecting wrapt>=1.11.0
  Downloading wrapt-1.14.1-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (81 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 81.0/81.0 kB 123.5 kB/s eta 0:00:00
Collecting protobuf<3.20,>=3.9.2
  Downloading protobuf-3.19.6-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.1/1.1 MB 541.8 kB/s eta 0:00:00
Collecting tensorflow-estimator<2.11,>=2.10.0
  Downloading tensorflow_estimator-2.10.0-py2.py3-none-any.whl (438 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 438.7/438.7 kB 515.1 kB/s eta 0:00:00
Collecting keras<2.11,>=2.10.0
  Downloading keras-2.10.0-py2.py3-none-any.whl (1.7 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.7/1.7 MB 655.6 kB/s eta 0:00:00
Collecting h5py>=2.9.0
  Downloading h5py-3.7.0-cp38-cp38-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (4.5 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4.5/4.5 MB 957.1 kB/s eta 0:00:00
Requirement already satisfied: setuptools in ./.conda/envs/vit/lib/python3.8/site-packages (from tensorflow) (65.5.0)
Collecting gast<=0.4.0,>=0.2.1
  Downloading gast-0.4.0-py3-none-any.whl (9.8 kB)
Collecting grpcio<2.0,>=1.24.3
  Downloading grpcio-1.50.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (4.7 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4.7/4.7 MB 1.2 MB/s eta 0:00:00
Requirement already satisfied: six>=1.12.0 in ./.conda/envs/vit/lib/python3.8/site-packages (from tensorflow) (1.16.0)
Collecting astunparse>=1.6.0
  Downloading astunparse-1.6.3-py2.py3-none-any.whl (12 kB)
Collecting tensorboard<2.11,>=2.10
  Downloading tensorboard-2.10.1-py3-none-any.whl (5.9 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 5.9/5.9 MB 775.7 kB/s eta 0:00:00
Requirement already satisfied: numpy>=1.20 in ./.conda/envs/vit/lib/python3.8/site-packages (from tensorflow) (1.23.4)
Collecting termcolor>=1.1.0
  Downloading termcolor-2.1.0-py3-none-any.whl (5.8 kB)
Collecting flatbuffers>=2.0
  Downloading flatbuffers-22.10.26-py2.py3-none-any.whl (26 kB)
Collecting libclang>=13.0.0
  Downloading libclang-14.0.6-py2.py3-none-manylinux2010_x86_64.whl (14.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 14.1/14.1 MB 766.0 kB/s eta 0:00:00
Requirement already satisfied: typing-extensions>=3.6.6 in ./.conda/envs/vit/lib/python3.8/site-packages (from tensorflow) (4.3.0)
Collecting google-pasta>=0.1.1
  Downloading google_pasta-0.2.0-py3-none-any.whl (57 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 57.5/57.5 kB 36.1 kB/s eta 0:00:00
Collecting keras-preprocessing>=1.1.1
  Downloading Keras_Preprocessing-1.1.2-py2.py3-none-any.whl (42 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42.6/42.6 kB 24.1 kB/s eta 0:00:00
Requirement already satisfied: wheel<1.0,>=0.23.0 in ./.conda/envs/vit/lib/python3.8/site-packages (from astunparse>=1.6.0->tensorflow) (0.37.1)
Requirement already satisfied: requests<3,>=2.21.0 in ./.conda/envs/vit/lib/python3.8/site-packages (from tensorboard<2.11,>=2.10->tensorflow) (2.28.1)
Collecting markdown>=2.6.8
  Downloading Markdown-3.4.1-py3-none-any.whl (93 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 93.3/93.3 kB 55.4 kB/s eta 0:00:00
Collecting werkzeug>=1.0.1
  Downloading Werkzeug-2.2.2-py3-none-any.whl (232 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 232.7/232.7 kB 486.9 kB/s eta 0:00:00
Collecting google-auth-oauthlib<0.5,>=0.4.1
  Downloading google_auth_oauthlib-0.4.6-py2.py3-none-any.whl (18 kB)
Collecting google-auth<3,>=1.6.3
  Downloading google_auth-2.14.1-py2.py3-none-any.whl (175 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 175.4/175.4 kB 110.7 kB/s eta 0:00:00
Collecting tensorboard-plugin-wit>=1.6.0
  Downloading tensorboard_plugin_wit-1.8.1-py3-none-any.whl (781 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 781.3/781.3 kB 1.1 MB/s eta 0:00:00
Collecting tensorboard-data-server<0.7.0,>=0.6.0
  Downloading tensorboard_data_server-0.6.1-py3-none-manylinux2010_x86_64.whl (4.9 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4.9/4.9 MB 1.1 MB/s eta 0:00:00
Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in ./.conda/envs/vit/lib/python3.8/site-packages (from packaging->tensorflow) (3.0.9)
Collecting rsa<5,>=3.1.4
  Downloading rsa-4.9-py3-none-any.whl (34 kB)
Collecting cachetools<6.0,>=2.0.0
  Downloading cachetools-5.2.0-py3-none-any.whl (9.3 kB)
Collecting pyasn1-modules>=0.2.1
  Downloading pyasn1_modules-0.2.8-py2.py3-none-any.whl (155 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 155.3/155.3 kB 441.5 kB/s eta 0:00:00
Collecting requests-oauthlib>=0.7.0
  Downloading requests_oauthlib-1.3.1-py2.py3-none-any.whl (23 kB)
Requirement already satisfied: importlib-metadata>=4.4 in ./.conda/envs/vit/lib/python3.8/site-packages (from markdown>=2.6.8->tensorboard<2.11,>=2.10->tensorflow) (4.11.3)
Requirement already satisfied: idna<4,>=2.5 in ./.conda/envs/vit/lib/python3.8/site-packages (from requests<3,>=2.21.0->tensorboard<2.11,>=2.10->tensorflow) (3.4)
Requirement already satisfied: certifi>=2017.4.17 in ./.conda/envs/vit/lib/python3.8/site-packages (from requests<3,>=2.21.0->tensorboard<2.11,>=2.10->tensorflow) (2022.9.24)
Requirement already satisfied: charset-normalizer<3,>=2 in ./.conda/envs/vit/lib/python3.8/site-packages (from requests<3,>=2.21.0->tensorboard<2.11,>=2.10->tensorflow) (2.0.4)
Requirement already satisfied: urllib3<1.27,>=1.21.1 in ./.conda/envs/vit/lib/python3.8/site-packages (from requests<3,>=2.21.0->tensorboard<2.11,>=2.10->tensorflow) (1.26.12)
Requirement already satisfied: MarkupSafe>=2.1.1 in ./.conda/envs/vit/lib/python3.8/site-packages (from werkzeug>=1.0.1->tensorboard<2.11,>=2.10->tensorflow) (2.1.1)
Requirement already satisfied: zipp>=0.5 in ./.conda/envs/vit/lib/python3.8/site-packages (from importlib-metadata>=4.4->markdown>=2.6.8->tensorboard<2.11,>=2.10->tensorflow) (3.8.0)
Collecting pyasn1<0.5.0,>=0.4.6
  Downloading pyasn1-0.4.8-py2.py3-none-any.whl (77 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 77.1/77.1 kB 100.5 kB/s eta 0:00:00
Collecting oauthlib>=3.0.0
  Downloading oauthlib-3.2.2-py3-none-any.whl (151 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 151.7/151.7 kB 95.5 kB/s eta 0:00:00
Installing collected packages: tensorboard-plugin-wit, pyasn1, libclang, keras, flatbuffers, wrapt, werkzeug, termcolor, tensorflow-io-gcs-filesystem, tensorflow-estimator, tensorboard-data-server, rsa, pyasn1-modules, protobuf, opt-einsum, oauthlib, keras-preprocessing, h5py, grpcio, google-pasta, gast, cachetools, astunparse, absl-py, requests-oauthlib, markdown, google-auth, google-auth-oauthlib, tensorboard, tensorflow
Successfully installed absl-py-1.3.0 astunparse-1.6.3 cachetools-5.2.0 flatbuffers-22.10.26 gast-0.4.0 google-auth-2.14.1 google-auth-oauthlib-0.4.6 google-pasta-0.2.0 grpcio-1.50.0 h5py-3.7.0 keras-2.10.0 keras-preprocessing-1.1.2 libclang-14.0.6 markdown-3.4.1 oauthlib-3.2.2 opt-einsum-3.3.0 protobuf-3.19.6 pyasn1-0.4.8 pyasn1-modules-0.2.8 requests-oauthlib-1.3.1 rsa-4.9 tensorboard-2.10.1 tensorboard-data-server-0.6.1 tensorboard-plugin-wit-1.8.1 tensorflow-2.10.1 tensorflow-estimator-2.10.0 tensorflow-io-gcs-filesystem-0.27.0 termcolor-2.1.0 werkzeug-2.2.2 wrapt-1.14.1
(vit) yekyaw.thu@gpu:~$
```

Installation of scikit-learn ...  

```
(vit) yekyaw.thu@gpu:~$ pip install scikit-learn
Collecting scikit-learn
  Downloading scikit_learn-1.1.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (31.2 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 31.2/31.2 MB 1.4 MB/s eta 0:00:00
Collecting scipy>=1.3.2
  Downloading scipy-1.9.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (33.8 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 33.8/33.8 MB 1.6 MB/s eta 0:00:00
Collecting threadpoolctl>=2.0.0
  Using cached threadpoolctl-3.1.0-py3-none-any.whl (14 kB)
Requirement already satisfied: numpy>=1.17.3 in ./.conda/envs/vit/lib/python3.8/site-packages (from scikit-learn) (1.23.4)
Collecting joblib>=1.0.0
  Using cached joblib-1.2.0-py3-none-any.whl (297 kB)
Installing collected packages: threadpoolctl, scipy, joblib, scikit-learn
Successfully installed joblib-1.2.0 scikit-learn-1.1.3 scipy-1.9.3 threadpoolctl-3.1.0
(vit) yekyaw.thu@gpu:~$ python
Python 3.8.13 (default, Oct 21 2022, 23:50:54)
[GCC 11.2.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import sklearn
>>> exit()
(vit) yekyaw.thu@gpu:~$
```

Installation of pydot ...  

```
(vit) yekyaw.thu@gpu:~$ pip install pydot
Collecting pydot
  Downloading pydot-1.4.2-py2.py3-none-any.whl (21 kB)
Requirement already satisfied: pyparsing>=2.1.4 in ./.conda/envs/vit/lib/python3.8/site-packages (from pydot) (3.0.9)
Installing collected packages: pydot
```

Installation of graphviz ...  

```
Successfully installed pydot-1.4.2
(vit) yekyaw.thu@gpu:~$ pip install graphviz
Collecting graphviz
  Downloading graphviz-0.20.1-py3-none-any.whl (47 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 47.0/47.0 kB 1.0 MB/s eta 0:00:00
Installing collected packages: graphviz
Successfully installed graphviz-0.20.1
(vit) yekyaw.thu@gpu:~$
```

Although, I installed above two libraries, not able to import inside Jupyter.  
And thus, I tried with git clone and install ...  

```
(vit) yekyaw.thu@gpu:~/tool$ git clone https://gitlab.com/graphviz/graphviz.git
Cloning into 'graphviz'...
remote: Enumerating objects: 124966, done.
remote: Counting objects: 100% (1690/1690), done.
remote: Compressing objects: 100% (438/438), done.
remote: Total 124966 (delta 1286), reused 1633 (delta 1251), pack-reused 123276
Receiving objects: 100% (124966/124966), 180.04 MiB | 17.67 MiB/s, done.
Resolving deltas: 100% (96109/96109), done.
(vit) yekyaw.thu@gpu:~/tool$ cd graphviz/
(vit) yekyaw.thu@gpu:~/tool/graphviz$ ls
AUTHORS         config-cmake.h.in  doc               graphviz.appdata.xml      m4           requirements.txt
autogen.sh      configure.ac       dot.demo          graphviz-centos.repo      macosx       rpm_notes.txt
ChangeLog       contrib            Doxyfile.in       graphviz-fedora.repo      Makefile.am  share
CHANGELOG.md    CONTRIBUTING.md    epl_inserter.tcl  graphviz.sln              NEWS         tclpkg
ci              COPYING            epl-v10.html      graphviz.spec             plugin       tests
cmake           cpl1.0.txt         epl-v10.txt       graphviz_version.h.cmake  plugin.demo  windows
CMakeLists.txt  debian             gen_version.py    lib                       README
cmd             developers         graphs            LICENSE                   README.md
config          DEVELOPERS.md      graphviz.7        loadimage_test.sh         redhat
(vit) yekyaw.thu@gpu:~/tool/graphviz$
```

Like normal installation in Linux ...  

```
(vit) yekyaw.thu@gpu:~/tool/graphviz$ ./autogen.sh
Graphviz: version date is based on time of last commit: 20221117.0557
Graphviz: abbreviated hash of last commit: c30618657
autoreconf: Entering directory `.'
autoreconf: configure.ac: not using Gettext
autoreconf: running: aclocal --force -I m4
autoreconf: configure.ac: tracing
autoreconf: configure.ac: subdirectory libltdl not present
autoreconf: running: libtoolize --copy --force --ltdl
libtoolize: putting auxiliary files in AC_CONFIG_AUX_DIR, 'config'.
libtoolize: copying file 'config/compile'
libtoolize: copying file 'config/config.guess'
libtoolize: copying file 'config/config.sub'
libtoolize: copying file 'config/depcomp'
libtoolize: copying file 'config/install-sh'
libtoolize: copying file 'config/missing'
libtoolize: copying file 'config/ltmain.sh'
libtoolize: putting macros in AC_CONFIG_MACRO_DIRS, 'm4'.
libtoolize: copying file 'm4/libtool.m4'
libtoolize: copying file 'm4/ltargz.m4'
libtoolize: copying file 'm4/ltdl.m4'
libtoolize: copying file 'm4/ltoptions.m4'
libtoolize: copying file 'm4/ltsugar.m4'
libtoolize: copying file 'm4/ltversion.m4'
libtoolize: copying file 'm4/lt~obsolete.m4'
libtoolize: putting libltdl files in LT_CONFIG_LTDL_DIR, 'libltdl'.
libtoolize: copying file 'libltdl/COPYING.LIB'
libtoolize: creating file 'libltdl/Makefile.am'
libtoolize: copying file 'libltdl/README'
libtoolize: creating file 'libltdl/configure.ac'
libtoolize: copying file 'libltdl/aclocal.m4'
libtoolize: creating file 'libltdl/Makefile.in'
libtoolize: copying file 'libltdl/config-h.in'
libtoolize: creating file 'libltdl/configure'
libtoolize: copying file 'libltdl/libltdl/lt__alloc.h'
libtoolize: copying file 'libltdl/libltdl/lt__argz_.h'
libtoolize: copying file 'libltdl/libltdl/lt__dirent.h'
libtoolize: copying file 'libltdl/libltdl/lt__glibc.h'
libtoolize: copying file 'libltdl/libltdl/lt__private.h'
libtoolize: copying file 'libltdl/libltdl/lt__strl.h'
libtoolize: copying file 'libltdl/libltdl/lt_dlloader.h'
libtoolize: copying file 'libltdl/libltdl/lt_error.h'
libtoolize: copying file 'libltdl/libltdl/lt_system.h'
libtoolize: copying file 'libltdl/libltdl/slist.h'
libtoolize: copying file 'libltdl/loaders/dld_link.c'
libtoolize: copying file 'libltdl/loaders/dlopen.c'
libtoolize: copying file 'libltdl/loaders/dyld.c'
libtoolize: copying file 'libltdl/loaders/load_add_on.c'
libtoolize: copying file 'libltdl/loaders/loadlibrary.c'
libtoolize: copying file 'libltdl/loaders/preopen.c'
libtoolize: copying file 'libltdl/loaders/shl_load.c'
libtoolize: copying file 'libltdl/lt__alloc.c'
libtoolize: copying file 'libltdl/lt__argz.c'
libtoolize: copying file 'libltdl/lt__dirent.c'
libtoolize: copying file 'libltdl/lt__strl.c'
libtoolize: copying file 'libltdl/lt_dlloader.c'
libtoolize: copying file 'libltdl/lt_error.c'
libtoolize: copying file 'libltdl/ltdl.c'
libtoolize: copying file 'libltdl/ltdl.h'
libtoolize: copying file 'libltdl/slist.c'
autoreconf: running: /usr/bin/autoconf --force
autoreconf: running: /usr/bin/autoheader --force
autoreconf: running: automake --add-missing --copy --force-missing
Makefile.am: installing './INSTALL'
configure.ac: installing 'config/ylwrap'
parallel-tests: installing 'config/test-driver'
autoreconf: Leaving directory `.'
(vit) yekyaw.thu@gpu:~/tool/graphviz$
```

Check the output "./configure" file ...  

```
(vit) yekyaw.thu@gpu:~/tool/graphviz$ ./config
config/    configure
(vit) yekyaw.thu@gpu:~/tool/graphviz$
```

Run ./configure  

```
(vit) yekyaw.thu@gpu:~/tool/graphviz$ ./configure
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /usr/bin/mkdir -p
checking for gawk... gawk
checking whether make sets $(MAKE)... yes
checking whether make supports nested variables... yes
checking whether UID '804601154' is supported by ustar format... no
checking whether GID '804600513' is supported by ustar format... no
checking how to create a ustar tar archive... none
checking whether make supports nested variables... (cached) yes
checking whether make supports the include directive... yes (GNU style)
checking for gcc... gcc
checking whether the C compiler works... yes
checking for C compiler default output file name... a.out
checking for suffix of executables...
checking whether we are cross compiling... no
checking for suffix of object files... o
checking whether we are using the GNU C compiler... yes
checking whether gcc accepts -g... yes
checking for gcc option to accept ISO C89... none needed
checking whether gcc understands -c and -o together... yes
checking dependency style of gcc... gcc3
checking for flex... no
checking for lex... no
checking for bison... no
checking for byacc... no
checking for a sed that does not truncate output... /usr/bin/sed
checking for grep that handles long lines and -e... /usr/bin/grep
checking for egrep... /usr/bin/grep -E
checking whether ln -s works... yes
checking how to print strings... printf
checking for a sed that does not truncate output... (cached) /usr/bin/sed
checking for fgrep... /usr/bin/grep -F
checking for ld used by gcc... /usr/bin/ld
checking if the linker (/usr/bin/ld) is GNU ld... yes
checking for BSD- or MS-compatible name lister (nm)... /usr/bin/nm -B
checking the name lister (/usr/bin/nm -B) interface... BSD nm
checking the maximum length of command line arguments... 1572864
checking how to convert x86_64-pc-linux-gnu file names to x86_64-pc-linux-gnu format... func_convert_file_noop
checking how to convert x86_64-pc-linux-gnu file names to toolchain format... func_convert_file_noop
checking for /usr/bin/ld option to reload object files... -r
checking for objdump... objdump
checking how to recognize dependent libraries... pass_all
checking for dlltool... no
checking how to associate runtime and link libraries... printf %s\n
checking for ar... ar
checking for archiver @FILE support... @
checking for strip... strip
checking for ranlib... ranlib
checking command to parse /usr/bin/nm -B output from gcc object... ok
checking for sysroot... no
checking for a working dd... /usr/bin/dd
checking how to truncate binary pipes... /usr/bin/dd bs=4096 count=1
checking for mt... mt
checking if mt is a manifest tool... no
checking how to run the C preprocessor... gcc -E
checking for ANSI C header files... yes
checking for sys/types.h... yes
checking for sys/stat.h... yes
checking for stdlib.h... yes
checking for string.h... yes
checking for memory.h... yes
checking for strings.h... yes
checking for inttypes.h... yes
checking for stdint.h... yes
checking for unistd.h... yes
checking for dlfcn.h... yes
checking for objdir... .libs
checking if gcc supports -fno-rtti -fno-exceptions... no
checking for gcc option to produce PIC... -fPIC -DPIC
checking if gcc PIC flag -fPIC -DPIC works... yes
checking if gcc static flag -static works... yes
checking if gcc supports -c -o file.o... yes
checking if gcc supports -c -o file.o... (cached) yes
checking whether the gcc linker (/usr/bin/ld -m elf_x86_64) supports shared libraries... yes
checking whether -lc should be explicitly linked in... no
checking dynamic linker characteristics... GNU/Linux ld.so
checking how to hardcode library paths into programs... immediate
checking whether stripping libraries is possible... yes
checking if libtool supports shared libraries... yes
checking whether to build shared libraries... yes
checking whether to build static libraries... no
checking for groff... groff
checking for ps2pdf... ps2pdf
checking for pkg-config... /usr/bin/pkg-config
checking pkg-config is at least version 0.9.0... yes
checking for tclsh8.6... no
checking for tclsh8.5... no
checking for tclsh8.4... no
checking for tclsh8.3... no
checking for tclsh... no
checking for gcc option to accept ISO C99... none needed
checking for g++... g++
checking whether we are using the GNU C++ compiler... yes
checking whether g++ accepts -g... yes
checking dependency style of g++... gcc3
checking how to run the C++ preprocessor... g++ -E
checking for ld used by g++... /usr/bin/ld -m elf_x86_64
checking if the linker (/usr/bin/ld -m elf_x86_64) is GNU ld... yes
checking whether the g++ linker (/usr/bin/ld -m elf_x86_64) supports shared libraries... yes
checking for g++ option to produce PIC... -fPIC -DPIC
checking if g++ PIC flag -fPIC -DPIC works... yes
checking if g++ static flag -static works... yes
checking if g++ supports -c -o file.o... yes
checking if g++ supports -c -o file.o... (cached) yes
checking whether the g++ linker (/usr/bin/ld -m elf_x86_64) supports shared libraries... yes
checking dynamic linker characteristics... (cached) GNU/Linux ld.so
checking how to hardcode library paths into programs... immediate
checking whether g++ supports C++11 features with -std=c++11... yes
checking for gcc... gcc
checking whether we are using the GNU Objective C compiler... no
checking whether gcc accepts -g... no
checking dependency style of gcc... gcc3
checking for inline... inline
checking whether C compiler accepts -Wtrampolines... yes
checking whether C compiler accepts -Wlogical-op... yes
checking for windres... no
checking for x86_64-pc-linux-gnu-windres... no
checking for pid_t... yes
checking for ssize_t... yes
checking for uid_t in sys/types.h... yes
checking for off64_t... no
checking for struct stat64... no
checking for ... no
checking fcntl.h usability... yes
checking fcntl.h presence... yes
checking for fcntl.h... yes
checking search.h usability... yes
checking search.h presence... yes
checking for search.h... yes
checking stropts.h usability... no
checking stropts.h presence... no
checking for stropts.h... no
checking termios.h usability... yes
checking termios.h presence... yes
checking for termios.h... yes
checking sys/time.h usability... yes
checking sys/time.h presence... yes
checking for sys/time.h... yes
checking for sys/types.h... (cached) yes
checking sys/select.h usability... yes
checking sys/select.h presence... yes
checking for sys/select.h... yes
checking sys/socket.h usability... yes
checking sys/socket.h presence... yes
checking for sys/socket.h... yes
checking for sys/stat.h... (cached) yes
checking sys/mman.h usability... yes
checking sys/mman.h presence... yes
checking for sys/mman.h... yes
checking sys/ioctl.h usability... yes
checking sys/ioctl.h presence... yes
checking for sys/ioctl.h... yes
checking sys/inotify.h usability... yes
checking sys/inotify.h presence... yes
checking for sys/inotify.h... yes
checking for main in -lm... yes
checking for sincos... yes
checking for lrand48... yes
checking for drand48... yes
checking for srand48... yes
checking for setmode... no
checking for setenv... yes
checking for ftruncate... yes
checking for lseek64... yes
checking for stat64... yes
checking for select... yes
checking for dl_iterate_phdr... yes
checking for strcasestr... yes
checking what extension is used for runtime loadable modules... .so
checking what variable specifies run-time module search path... LD_LIBRARY_PATH
checking for the default library search path... /lib /usr/lib /usr/local/cuda/targets/x86_64-linux/lib /usr/local/cuda-11/targets/x86_64-linux/lib /usr/lib/x86_64-linux-gnu/libfakeroot /usr/local/cuda-11.4/targets/x86_64-linux/lib /opt/intel/lib/intel64 /opt/intel/mkl/lib/intel64 /usr/local/lib /usr/local/lib/x86_64-linux-gnu /lib/x86_64-linux-gnu /usr/lib/x86_64-linux-gnu
checking for library containing dlopen... -ldl
checking for dlerror... yes
checking for shl_load... no
checking for shl_load in -ldld... no
checking for dld_link in -ldld... no
checking for _ prefix in compiled symbols... no
checking whether deplibs are loaded by dlopen... yes
checking for argz.h... yes
checking for error_t... yes
checking for argz_add... yes
checking for argz_append... yes
checking for argz_count... yes
checking for argz_create_sep... yes
checking for argz_insert... yes
checking for argz_next... yes
checking for argz_stringify... yes
checking if argz actually works... yes
checking whether libtool supports -dlopen/-dlpreopen... yes
checking for ltdl.h... yes
checking whether lt_dlinterface_register is declared... yes
checking for lt_dladvise_preload in -lltdl... yes
checking where to find libltdl headers...
checking where to find libltdl library... -lltdl
checking for unistd.h... (cached) yes
checking for dl.h... no
checking for sys/dl.h... no
checking for dld.h... no
checking for mach-o/dyld.h... no
checking for dirent.h... yes
checking for closedir... yes
checking for opendir... yes
checking for readdir... yes
checking for strlcat... no
checking for strlcpy... no
checking for lt_dladvise_init in -lltdl... yes
checking for X... libraries , headers
checking for gethostbyname... yes
checking for connect... yes
checking for remove... yes
checking for shmat... yes
checking for IceConnectionNumber in -lICE... no
checking for XRENDER... no
checking for swig... no
checking tcl.h usability... no
checking tcl.h presence... no
checking for tcl.h... no
configure: WARNING: Unable to find header tcl.h. The Tcl packages will not be built
checking for connect... (cached) yes
checking for gethostbyname... (cached) yes
checking for expat-config... no
checking expat.h usability... yes
checking expat.h presence... yes
checking for expat.h... yes
checking for main in -lexpat... yes
checking IL/il.h usability... no
checking IL/il.h presence... no
checking for IL/il.h... no
configure: WARNING: Optional DevIL library not available - missing headers
checking for main in -lIL... no
configure: WARNING: Optional DevIL library not available
checking zlib.h usability... yes
checking zlib.h presence... yes
checking for zlib.h... yes
checking for main in -lz... yes
checking for WEBP... no
checking for POPPLER... no
checking for RSVG... no
checking for PANGOCAIRO... no
checking for FREETYPE2... no
configure: WARNING: pkg-config did not find a freetype2.pc.  Looking for freetype-config.
checking for freetype-config... /home/yekyaw.thu/.conda/envs/vit/bin/freetype-config
Package freetype2 was not found in the pkg-config search path.
Perhaps you should add the directory containing `freetype2.pc'
to the PKG_CONFIG_PATH environment variable
No package 'freetype2' found
Package freetype2 was not found in the pkg-config search path.
Perhaps you should add the directory containing `freetype2.pc'
to the PKG_CONFIG_PATH environment variable
No package 'freetype2' found
Package freetype2 was not found in the pkg-config search path.
Perhaps you should add the directory containing `freetype2.pc'
to the PKG_CONFIG_PATH environment variable
No package 'freetype2' found
Package freetype2 was not found in the pkg-config search path.
Perhaps you should add the directory containing `freetype2.pc'
to the PKG_CONFIG_PATH environment variable
No package 'freetype2' found
Package freetype2 was not found in the pkg-config search path.
Perhaps you should add the directory containing `freetype2.pc'
to the PKG_CONFIG_PATH environment variable
No package 'freetype2' found
Package freetype2 was not found in the pkg-config search path.
Perhaps you should add the directory containing `freetype2.pc'
to the PKG_CONFIG_PATH environment variable
No package 'freetype2' found
Package freetype2 was not found in the pkg-config search path.
Perhaps you should add the directory containing `freetype2.pc'
to the PKG_CONFIG_PATH environment variable
No package 'freetype2' found
Package freetype2 was not found in the pkg-config search path.
Perhaps you should add the directory containing `freetype2.pc'
to the PKG_CONFIG_PATH environment variable
No package 'freetype2' found
sed: -e expression #1, char 0: no previous regular expression
sed: -e expression #1, char 0: no previous regular expression
Package freetype2 was not found in the pkg-config search path.
Perhaps you should add the directory containing `freetype2.pc'
to the PKG_CONFIG_PATH environment variable
No package 'freetype2' found
Package freetype2 was not found in the pkg-config search path.
Perhaps you should add the directory containing `freetype2.pc'
to the PKG_CONFIG_PATH environment variable
No package 'freetype2' found
Package freetype2 was not found in the pkg-config search path.
Perhaps you should add the directory containing `freetype2.pc'
to the PKG_CONFIG_PATH environment variable
No package 'freetype2' found
Package freetype2 was not found in the pkg-config search path.
Perhaps you should add the directory containing `freetype2.pc'
to the PKG_CONFIG_PATH environment variable
No package 'freetype2' found
Package freetype2 was not found in the pkg-config search path.
Perhaps you should add the directory containing `freetype2.pc'
to the PKG_CONFIG_PATH environment variable
No package 'freetype2' found
Package freetype2 was not found in the pkg-config search path.
Perhaps you should add the directory containing `freetype2.pc'
to the PKG_CONFIG_PATH environment variable
No package 'freetype2' found
Package freetype2 was not found in the pkg-config search path.
Perhaps you should add the directory containing `freetype2.pc'
to the PKG_CONFIG_PATH environment variable
No package 'freetype2' found
Package freetype2 was not found in the pkg-config search path.
Perhaps you should add the directory containing `freetype2.pc'
to the PKG_CONFIG_PATH environment variable
No package 'freetype2' found
sed: -e expression #1, char 0: no previous regular expression
sed: -e expression #1, char 0: no previous regular expression
sed: -e expression #1, char 0: no previous regular expression
checking for FONTCONFIG... no
configure: WARNING: pkg-config did not find a fontconfig.pc.  Looking for fontconfig-config.
checking for fontconfig-config... no
configure: WARNING: fontconfig library not available
checking for GDK... no
checking for GDK_PIXBUF... no
checking for GTK... no
checking for GTKGL... no
checking for GTKGLEXT... no
checking for GTS... no
checking for ANN... no
checking for GLADE... no
checking for qmake-qt5... no
checking for qmake5... no
checking for qmake... qmake
checking for QTCORE... no
checking for GDLIB... no
checking for gdlib-config... no
configure: WARNING: GD neither gdlib pkgconfig nor gdlib-config was found
checking gd.h usability... no
checking gd.h presence... no
checking for gd.h... no
configure: WARNING: Optional GD library not available - no gd.h
checking GL/glut.h usability... no
checking GL/glut.h presence... no
checking for GL/glut.h... no
configure: WARNING: Optional glut library not available - no GL/glut.h
configure: WARNING: SMYRNA requires GTK
configure: WARNING: SMYRNA requires GTKGLEXT
configure: WARNING: SMYRNA requires GLADE
configure: WARNING: SMYRNA requires GTS
configure: WARNING: SMYRNA requires GLUT
checking if FILE struct contains _cnt... no
checking if FILE struct contains _r... no
checking if FILE struct contains _next... no
checking if FILE struct contains _IO_read_end... yes
checking if intptr_t is declared... yes
checking for main in -lcriterion... no
configure: WARNING: Criterion unit testing framework not installed
checking that generated files are newer than configure... done
configure: creating ./config.status
config.status: creating Makefile
config.status: creating debian/changelog
config.status: creating doc/Makefile
config.status: creating doc/info/Makefile
config.status: creating doc/schema/Makefile
config.status: creating contrib/Makefile
config.status: creating contrib/prune/Makefile
config.status: creating contrib/diffimg/Makefile
config.status: creating graphs/Makefile
config.status: creating graphs/directed/Makefile
config.status: creating graphs/undirected/Makefile
config.status: creating lib/Makefile
config.status: creating lib/cdt/Makefile
config.status: creating lib/cdt/libcdt.pc
config.status: creating lib/cgraph/Makefile
config.status: creating lib/cgraph/libcgraph.pc
config.status: creating lib/rbtree/Makefile
config.status: creating lib/pathplan/Makefile
config.status: creating lib/pathplan/libpathplan.pc
config.status: creating lib/ast/Makefile
config.status: creating lib/sfio/Makefile
config.status: creating lib/sfio/Sfio_f/Makefile
config.status: creating lib/vmalloc/Makefile
config.status: creating lib/dotgen/Makefile
config.status: creating lib/neatogen/Makefile
config.status: creating lib/fdpgen/Makefile
config.status: creating lib/sparse/Makefile
config.status: creating lib/mingle/Makefile
config.status: creating lib/label/Makefile
config.status: creating lib/sfdpgen/Makefile
config.status: creating lib/sfdpgen/libsfdp.pc
config.status: creating lib/osage/Makefile
config.status: creating lib/edgepaint/Makefile
config.status: creating lib/edgepaint/liblab_gamut.pc
config.status: creating lib/gvpr/Makefile
config.status: creating lib/gvpr/libgvpr.pc
config.status: creating lib/circogen/Makefile
config.status: creating lib/twopigen/Makefile
config.status: creating lib/patchwork/Makefile
config.status: creating lib/pack/Makefile
config.status: creating lib/ortho/Makefile
config.status: creating lib/expr/Makefile
config.status: creating lib/expr/libexpr.pc
config.status: creating lib/common/Makefile
config.status: creating lib/ingraphs/Makefile
config.status: creating lib/vpsc/Makefile
config.status: creating lib/gvc/Makefile
config.status: creating lib/gvc/libgvc.pc
config.status: creating lib/xdot/Makefile
config.status: creating lib/xdot/libxdot.pc
config.status: creating lib/topfish/Makefile
config.status: creating lib/glcomp/Makefile
config.status: creating macosx/Info.plist
config.status: creating macosx/build/graphviz.pmdoc/01local.xml
config.status: creating macosx/build/graphviz.pmdoc/02graphviz.xml
config.status: creating windows/build/graphviz.wxs
config.status: creating windows/Properties/AssemblyInfo.cs
config.status: creating plugin/Makefile
config.status: creating plugin/core/Makefile
config.status: creating plugin/devil/Makefile
config.status: creating plugin/gd/Makefile
config.status: creating plugin/gdk/Makefile
config.status: creating plugin/gdiplus/Makefile
config.status: creating plugin/gs/Makefile
config.status: creating plugin/gtk/Makefile
config.status: creating plugin/lasi/Makefile
config.status: creating plugin/pango/Makefile
config.status: creating plugin/poppler/Makefile
config.status: creating plugin/quartz/Makefile
config.status: creating plugin/rsvg/Makefile
config.status: creating plugin/visio/Makefile
config.status: creating plugin/webp/Makefile
config.status: creating plugin/xlib/Makefile
config.status: creating plugin/dot_layout/Makefile
config.status: creating plugin/neato_layout/Makefile
config.status: creating cmd/Makefile
config.status: creating cmd/dot/Makefile
config.status: creating cmd/tools/Makefile
config.status: creating cmd/gvpr/Makefile
config.status: creating cmd/gvpr/lib/Makefile
config.status: creating cmd/smyrna/Makefile
config.status: creating cmd/gvmap/Makefile
config.status: creating cmd/mingle/Makefile
config.status: creating cmd/edgepaint/Makefile
config.status: creating cmd/gvedit/Makefile
config.status: creating cmd/gvedit/gvedit.pro
config.status: creating cmd/gvedit/ui/Makefile
config.status: creating cmd/gvedit/images/Makefile
config.status: creating tclpkg/Makefile
config.status: creating tclpkg/tclstubs/Makefile
config.status: creating tclpkg/tclhandle/Makefile
config.status: creating tclpkg/gdtclft/Makefile
config.status: creating tclpkg/gdtclft/demo/Makefile
config.status: creating tclpkg/tcldot/Makefile
config.status: creating tclpkg/tcldot/demo/Makefile
config.status: creating tclpkg/tclpathplan/Makefile
config.status: creating tclpkg/tclpathplan/demo/Makefile
config.status: creating tclpkg/tclpathplan/demo/pathplan_data/Makefile
config.status: creating tclpkg/gv/Makefile
config.status: creating tclpkg/gv/demo/Makefile
config.status: creating tclpkg/gv/META.gv
config.status: creating tests/graphs/Makefile
config.status: creating tests/linux.x86/Makefile
config.status: creating tests/Makefile
config.status: creating tests/unit_tests/Makefile
config.status: creating tests/unit_tests/lib/Makefile
config.status: creating tests/unit_tests/lib/common/Makefile
config.status: creating tests/regression_tests/Makefile
config.status: creating tests/regression_tests/shapes/Makefile
config.status: creating tests/regression_tests/shapes/reference/Makefile
config.status: creating tests/regression_tests/vuln/Makefile
config.status: creating tests/regression_tests/vuln/input/Makefile
config.status: creating tests/regression_tests/vuln/reference/Makefile
config.status: creating share/Makefile
config.status: creating share/examples/Makefile
config.status: creating share/gui/Makefile
config.status: creating redhat/graphviz.spec.fedora
config.status: creating redhat/graphviz.spec.rhel
config.status: creating Doxyfile
config.status: creating config.h
config.status: executing depfiles commands
config.status: executing libtool commands
=== configuring in libltdl (/home/yekyaw.thu/tool/graphviz/libltdl)
configure: running /bin/bash ./configure --disable-option-checking '--prefix=/usr/local'  --cache-file=/dev/null --srcdir=.
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /usr/bin/mkdir -p
checking for gawk... gawk
checking whether make sets $(MAKE)... yes
checking whether make supports nested variables... yes
checking whether make supports nested variables... (cached) yes
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking how to print strings... printf
checking whether make supports the include directive... yes (GNU style)
checking for gcc... gcc
checking whether the C compiler works... yes
checking for C compiler default output file name... a.out
checking for suffix of executables...
checking whether we are cross compiling... no
checking for suffix of object files... o
checking whether we are using the GNU C compiler... yes
checking whether gcc accepts -g... yes
checking for gcc option to accept ISO C89... none needed
checking whether gcc understands -c and -o together... yes
checking dependency style of gcc... gcc3
checking for a sed that does not truncate output... /usr/bin/sed
checking for grep that handles long lines and -e... /usr/bin/grep
checking for egrep... /usr/bin/grep -E
checking for fgrep... /usr/bin/grep -F
checking for ld used by gcc... /usr/bin/ld
checking if the linker (/usr/bin/ld) is GNU ld... yes
checking for BSD- or MS-compatible name lister (nm)... /usr/bin/nm -B
checking the name lister (/usr/bin/nm -B) interface... BSD nm
checking whether ln -s works... yes
checking the maximum length of command line arguments... 1572864
checking how to convert x86_64-pc-linux-gnu file names to x86_64-pc-linux-gnu format... func_convert_file_noop
checking how to convert x86_64-pc-linux-gnu file names to toolchain format... func_convert_file_noop
checking for /usr/bin/ld option to reload object files... -r
checking for objdump... objdump
checking how to recognize dependent libraries... pass_all
checking for dlltool... no
checking how to associate runtime and link libraries... printf %s\n
checking for ar... ar
checking for archiver @FILE support... @
checking for strip... strip
checking for ranlib... ranlib
checking command to parse /usr/bin/nm -B output from gcc object... ok
checking for sysroot... no
checking for a working dd... /usr/bin/dd
checking how to truncate binary pipes... /usr/bin/dd bs=4096 count=1
checking for mt... mt
checking if mt is a manifest tool... no
checking how to run the C preprocessor... gcc -E
checking for ANSI C header files... yes
checking for sys/types.h... yes
checking for sys/stat.h... yes
checking for stdlib.h... yes
checking for string.h... yes
checking for memory.h... yes
checking for strings.h... yes
checking for inttypes.h... yes
checking for stdint.h... yes
checking for unistd.h... yes
checking for dlfcn.h... yes
checking for objdir... .libs
checking if gcc supports -fno-rtti -fno-exceptions... no
checking for gcc option to produce PIC... -fPIC -DPIC
checking if gcc PIC flag -fPIC -DPIC works... yes
checking if gcc static flag -static works... yes
checking if gcc supports -c -o file.o... yes
checking if gcc supports -c -o file.o... (cached) yes
checking whether the gcc linker (/usr/bin/ld -m elf_x86_64) supports shared libraries... yes
checking whether -lc should be explicitly linked in... no
checking dynamic linker characteristics... GNU/Linux ld.so
checking how to hardcode library paths into programs... immediate
checking for shl_load... no
checking for shl_load in -ldld... no
checking for dlopen... no
checking for dlopen in -ldl... yes
checking whether a program can dlopen itself... yes
checking whether a statically linked program can dlopen itself... no
checking whether stripping libraries is possible... yes
checking if libtool supports shared libraries... yes
checking whether to build shared libraries... yes
checking whether to build static libraries... yes
checking what extension is used for runtime loadable modules... .so
checking what variable specifies run-time module search path... LD_LIBRARY_PATH
checking for the default library search path... /lib /usr/lib /usr/local/cuda/targets/x86_64-linux/lib /usr/local/cuda-11/targets/x86_64-linux/lib /usr/lib/x86_64-linux-gnu/libfakeroot /usr/local/cuda-11.4/targets/x86_64-linux/lib /opt/intel/lib/intel64 /opt/intel/mkl/lib/intel64 /usr/local/lib /usr/local/lib/x86_64-linux-gnu /lib/x86_64-linux-gnu /usr/lib/x86_64-linux-gnu
checking for library containing dlopen... -ldl
checking for dlerror... yes
checking for shl_load... (cached) no
checking for shl_load in -ldld... (cached) no
checking for dld_link in -ldld... no
checking for _ prefix in compiled symbols... no
checking whether deplibs are loaded by dlopen... yes
checking for argz.h... yes
checking for error_t... yes
checking for argz_add... yes
checking for argz_append... yes
checking for argz_count... yes
checking for argz_create_sep... yes
checking for argz_insert... yes
checking for argz_next... yes
checking for argz_stringify... yes
checking if argz actually works... yes
checking whether libtool supports -dlopen/-dlpreopen... yes
checking for unistd.h... (cached) yes
checking for dl.h... no
checking for sys/dl.h... no
checking for dld.h... no
checking for mach-o/dyld.h... no
checking for dirent.h... yes
checking for closedir... yes
checking for opendir... yes
checking for readdir... yes
checking for strlcat... no
checking for strlcpy... no
checking that generated files are newer than configure... done
configure: creating ./config.status
config.status: creating Makefile
config.status: creating config.h
config.status: executing depfiles commands
config.status: executing libtool commands

----------------------------------------------------------------

graphviz-7.0.2~dev.20221117.0557 will be compiled with the following:

options:
  cgraph:        Yes (always enabled)
  digcola:       Yes
  expat:         Yes
  fontconfig:    No (missing fontconfig-config)
  freetype:      Yes
  glut:          No (missing GL/glut.h)
  ann:           No (no ann.pc found)
  gts:           No (gts library not available)
  ipsepcola:     Yes
  ltdl:          Yes
  ortho:         Yes
  sfdp:          Yes
  swig:          No (swig not available) (  )
  shared:        Yes
  static:        No (disabled by default)
  qt:            No (QtCore not available)
  x:             Yes

commands:
  dot:           Yes (always enabled)
  neato:         Yes (always enabled)
  fdp:           Yes (always enabled)
  circo:         Yes (always enabled)
  twopi:         Yes (always enabled)
  gvpr:          Yes (always enabled)
  gvmap:         Yes (always enabled)
  smyrna:        No (requires: gtk+ gtkglext glade gts glut)
  gvedit:        No (QtCore not available)

plugin libraries:
  dot_layout:    Yes (always enabled)
  neato_layout:  Yes (always enabled)
  core:          Yes (always enabled)
  devil:         No (missing library)
  gd:            No (gd headers not found)
  gdiplus:       No (disabled by default - Windows only)
  gdk:           No (gdk library not available)
  gdk_pixbuf:    No (gdk_pixbuf library not available)
  ghostscript:   No (missing Xrender)
  gtk:           No (gtk library not available)
  lasi:          No (missing pangocairo support)
  pangocairo:    No (pangocairo library not available)
  poppler:       No (poppler library not available)
  quartz:        No (disabled by default - Mac only)
  rsvg:          No (rsvg library not available)
  visio:         Yes
  webp:          No (webp library not available)
  xlib:          Yes

language extensions:
  gv_sharp:      No (swig not available)
  gv_d:          No (disabled by default - incomplete)
  gv_go:         No (swig not available)
  gv_guile:      No (swig not available)
  gv_io:         No (disabled by default - no swig support yet)
  gv_java:       No (swig not available)
  gv_javascript: No (disabled by default - incomplete)
  gv_lua:        No (swig not available)
  gv_ocaml:      No (swig not available)
  gv_perl:       No (swig not available)
  gv_php:        No (swig not available)
  gv_python:     No (swig not available)
  gv_python3:    No (swig not available)
  gv_R:          No (swig not available)
  gv_ruby:       No (swig not available)
  gv_tcl:        No (tcl not available)

  tcldot:        No (tcl not available)
  tclpathplan:   No (tcl not available)
  gdtclft:       No (tcl not available)

Testing utilities:
  criterion:     No (Criterion unit testing framework not installed)
(vit) yekyaw.thu@gpu:~/tool/graphviz$
```

When I run "make", I got following errors:    

```
xdot.c:941:18: warning: conversion from ‘double’ to ‘float’ may change value [-Wfloat-conversion]
  941 |  stops[i].frac = d;
      |                  ^
  CCLD     libxdot.la
  CCLD     libxdot_C.la
rm -f xdot.3.pdf; pdffile=xdot.3.pdf; psfile=${pdffile%pdf}ps; \
groff -Tps -man xdot.3 > $psfile || { rm -f $psfile; exit 1; }; \
ps2pdf $psfile && rm -f $psfile || { rm -f $psfile; exit 1; }
make[3]: Leaving directory '/home/yekyaw.thu/tool/graphviz/lib/xdot'
Making all in cgraph
make[3]: Entering directory '/home/yekyaw.thu/tool/graphviz/lib/cgraph'
  CC       agerror.lo
  CC       apply.lo
  CC       attr.lo
  CC       edge.lo
  CC       flatten.lo
  CC       graph.lo
yacc -Wno-yacc -dv --output=grammar.c ../../lib/cgraph/grammar.y
/bin/bash: yacc: command not found
make[3]: *** [Makefile:1154: grammar.c] Error 127
make[3]: Leaving directory '/home/yekyaw.thu/tool/graphviz/lib/cgraph'
make[2]: *** [Makefile:582: all-recursive] Error 1
make[2]: Leaving directory '/home/yekyaw.thu/tool/graphviz/lib'
make[1]: *** [Makefile:798: all-recursive] Error 1
make[1]: Leaving directory '/home/yekyaw.thu/tool/graphviz'
make: *** [Makefile:627: all] Error 2
(vit) yekyaw.thu@gpu:~/tool/graphviz$
```

This error ===> "/bin/bash: yacc: command not found" ?!   

```

Install bison with conda ...  

```
(vit) yekyaw.thu@gpu:~/tool/graphviz$ conda install bison
Collecting package metadata (current_repodata.json): done
Solving environment: -
The environment is inconsistent, please check the package plan carefully
The following packages are causing the inconsistency:

  - defaults/linux-64::libxml2==2.9.14=h74e7548_0
  - defaults/noarch::argon2-cffi==21.3.0=pyhd3eb1b0_0
  - defaults/linux-64::tornado==6.2=py38h5eee18b_0
  - defaults/noarch::bleach==4.1.0=pyhd3eb1b0_0
  - defaults/noarch::send2trash==1.8.0=pyhd3eb1b0_1
  - defaults/linux-64::pysocks==1.7.1=py38h06a4308_0
  - defaults/noarch::prompt-toolkit==3.0.20=pyhd3eb1b0_0
  - defaults/linux-64::freetype==2.12.1=h4a9f257_0
  - defaults/linux-64::sniffio==1.2.0=py38h06a4308_1
  - defaults/linux-64::libedit==3.1.20210910=h7f8727e_0
  - defaults/linux-64::libwebp-base==1.2.4=h5eee18b_0
  - defaults/noarch::pygments==2.11.2=pyhd3eb1b0_0
  - defaults/linux-64::entrypoints==0.4=py38h06a4308_0
  - defaults/linux-64::jpeg==9e=h7f8727e_0
  - defaults/linux-64::brotlipy==0.7.0=py38h27cfd23_1003
  - defaults/linux-64::qt-webengine==5.15.9=hd2b0992_4
  - defaults/linux-64::idna==3.4=py38h06a4308_0
  - defaults/linux-64::argon2-cffi-bindings==21.2.0=py38h7f8727e_0
  - defaults/linux-64::typing_extensions==4.3.0=py38h06a4308_0
  - defaults/linux-64::qtconsole==5.3.2=py38h06a4308_0
  - defaults/noarch::prompt_toolkit==3.0.20=hd3eb1b0_0
  - defaults/linux-64::tk==8.6.12=h1ccaba5_0
  - defaults/linux-64::gst-plugins-base==1.14.0=h8213a91_2
  - defaults/noarch::pexpect==4.8.0=pyhd3eb1b0_3
  - defaults/noarch::six==1.16.0=pyhd3eb1b0_1
  - defaults/noarch::toml==0.10.2=pyhd3eb1b0_0
  - defaults/linux-64::soupsieve==2.3.2.post1=py38h06a4308_0
  - defaults/noarch::ipython_genutils==0.2.0=pyhd3eb1b0_1
  - defaults/linux-64::libxcb==1.15=h7f8727e_0
  - defaults/linux-64::ncurses==6.3=h5eee18b_3
  - defaults/linux-64::jinja2==3.1.2=py38h06a4308_0
  - defaults/linux-64::cryptography==38.0.1=py38h9ce1e76_0
  - defaults/noarch::pandocfilters==1.5.0=pyhd3eb1b0_0
  - defaults/noarch::jupyter_console==6.4.3=pyhd3eb1b0_0
  - defaults/linux-64::mistune==0.8.4=py38h7b6447c_1000
  - defaults/linux-64::pyzmq==23.2.0=py38h6a678d5_0
  - defaults/linux-64::nbconvert==6.5.4=py38h06a4308_0
  - defaults/linux-64::matplotlib-inline==0.1.6=py38h06a4308_0
  - defaults/linux-64::notebook==6.5.2=py38h06a4308_0
  - defaults/linux-64::nbformat==5.5.0=py38h06a4308_0
  - defaults/noarch::babel==2.9.1=pyhd3eb1b0_0
  - defaults/linux-64::icu==58.2=he6710b0_3
  - defaults/linux-64::sip==6.6.2=py38h6a678d5_0
  - defaults/noarch::jupyterlab_pygments==0.1.2=py_0
  - defaults/linux-64::requests==2.28.1=py38h06a4308_0
  - defaults/noarch::parso==0.8.3=pyhd3eb1b0_0
  - defaults/linux-64::notebook-shim==0.2.2=py38h06a4308_0
  - defaults/linux-64::ipython==8.6.0=py38h06a4308_0
  - defaults/linux-64::zeromq==4.3.4=h2531618_0
  - defaults/linux-64::beautifulsoup4==4.11.1=py38h06a4308_0
  - defaults/linux-64::psutil==5.9.0=py38h5eee18b_0
  - defaults/linux-64::websocket-client==0.58.0=py38h06a4308_4
  - defaults/linux-64::gstreamer==1.14.0=h28cd5cc_2
  - defaults/linux-64::nbclassic==0.4.8=py38h06a4308_0
  - defaults/linux-64::setuptools==65.5.0=py38h06a4308_0
  - defaults/noarch::jupyterlab_widgets==1.0.0=pyhd3eb1b0_1
  - defaults/noarch::packaging==21.3=pyhd3eb1b0_0
  - defaults/linux-64::markupsafe==2.1.1=py38h7f8727e_0
  - defaults/noarch::ptyprocess==0.7.0=pyhd3eb1b0_2
  - defaults/noarch::pure_eval==0.2.2=pyhd3eb1b0_0
  - defaults/linux-64::qtwebkit==5.212=h4eab89a_4
  - defaults/linux-64::libclang==10.0.1=default_hb85057a_2
  - defaults/linux-64::nest-asyncio==1.5.5=py38h06a4308_0
  - defaults/linux-64::libuuid==1.41.5=h5eee18b_0
  - defaults/linux-64::pyrsistent==0.18.0=py38heee7806_0
  - defaults/linux-64::cffi==1.15.1=py38h74dc2b5_0
  - defaults/linux-64::nspr==4.33=h295c915_0
  - defaults/linux-64::libwebp==1.2.4=h11a3e52_0
  - defaults/linux-64::nbclient==0.5.13=py38h06a4308_0
  - defaults/linux-64::pyparsing==3.0.9=py38h06a4308_0
  - defaults/linux-64::python-fastjsonschema==2.16.2=py38h06a4308_0
  - defaults/noarch::stack_data==0.2.0=pyhd3eb1b0_0
  - defaults/linux-64::fontconfig==2.13.1=hef1e5e3_1
  - defaults/linux-64::xz==5.2.6=h5eee18b_0
  - defaults/linux-64::jupyterlab_server==2.15.2=py38h06a4308_0
  - defaults/noarch::defusedxml==0.7.1=pyhd3eb1b0_0
  - defaults/linux-64::giflib==5.2.1=h7b6447c_0
  - defaults/linux-64::pcre==8.45=h295c915_0
  - defaults/linux-64::pip==22.2.2=py38h06a4308_0
  - defaults/linux-64::libpng==1.6.37=hbc83047_0
  - defaults/noarch::pyopenssl==22.0.0=pyhd3eb1b0_0
  - defaults/linux-64::zlib==1.2.13=h5eee18b_0
  - defaults/linux-64::dbus==1.13.18=hb2f20db_0
  - defaults/linux-64::jupyter==1.0.0=py38h06a4308_8
  - defaults/linux-64::zstd==1.5.2=ha4553b6_0
  - defaults/noarch::traitlets==5.1.1=pyhd3eb1b0_0
  - defaults/linux-64::tinycss2==1.2.1=py38h06a4308_0
  - defaults/linux-64::libgcc-ng==11.2.0=h1234567_1
  - defaults/linux-64::libllvm10==10.0.1=hbcb73fb_5
  - defaults/linux-64::lxml==4.9.1=py38h1edc446_0
  - defaults/noarch::pycparser==2.21=pyhd3eb1b0_0
  - defaults/linux-64::libtiff==4.4.0=hecacb30_2
  - defaults/linux-64::jsonschema==4.16.0=py38h06a4308_0
  - defaults/linux-64::ply==3.11=py38_0
  - defaults/linux-64::libxkbcommon==1.0.1=hfa300c1_0
  - defaults/linux-64::pytz==2022.1=py38h06a4308_0
  - defaults/linux-64::ipykernel==6.15.2=py38h06a4308_0
  - defaults/noarch::attrs==21.4.0=pyhd3eb1b0_0
  - defaults/linux-64::pkgutil-resolve-name==1.3.10=py38h06a4308_0
  - defaults/linux-64::zipp==3.8.0=py38h06a4308_0
  - defaults/linux-64::openssl==1.1.1s=h7f8727e_0
  - defaults/linux-64::pyqt==5.15.7=py38h6a678d5_1
  - defaults/noarch::asttokens==2.0.5=pyhd3eb1b0_0
  - defaults/linux-64::jupyter_client==7.3.5=py38h06a4308_0
  - defaults/linux-64::prometheus_client==0.14.1=py38h06a4308_0
  - defaults/linux-64::qtpy==2.2.0=py38h06a4308_0
  - defaults/noarch::wcwidth==0.2.5=pyhd3eb1b0_0
  - defaults/linux-64::jedi==0.18.1=py38h06a4308_1
  - defaults/linux-64::jupyter_core==4.11.2=py38h06a4308_0
  - defaults/linux-64::pyqt5-sip==12.11.0=py38h6a678d5_1
  - defaults/linux-64::nss==3.74=h0370c37_0
  - defaults/linux-64::libevent==2.1.12=h8f2d780_0
  - defaults/noarch::charset-normalizer==2.0.4=pyhd3eb1b0_0
  - defaults/linux-64::typing-extensions==4.3.0=py38h06a4308_0
  - defaults/linux-64::python==3.8.13=haa1d7c7_1
  - defaults/noarch::executing==0.8.3=pyhd3eb1b0_0
  - defaults/linux-64::lerc==3.0=h295c915_0
  - defaults/linux-64::readline==8.2=h5eee18b_0
  - defaults/linux-64::krb5==1.19.2=hac12032_0
  - defaults/noarch::backcall==0.2.0=pyhd3eb1b0_0
  - defaults/noarch::decorator==5.1.1=pyhd3eb1b0_0
  - defaults/noarch::pickleshare==0.7.5=pyhd3eb1b0_1003
  - defaults/linux-64::importlib-metadata==4.11.3=py38h06a4308_0
  - defaults/linux-64::glib==2.69.1=h4ff587b_1
  - defaults/linux-64::widgetsnbextension==3.5.2=py38h06a4308_0
  - defaults/linux-64::libsodium==1.0.18=h7b6447c_0
  - defaults/linux-64::lz4-c==1.9.3=h295c915_1
  - defaults/noarch::json5==0.9.6=pyhd3eb1b0_0
  - defaults/linux-64::libffi==3.3=he6710b0_2
  - defaults/linux-64::terminado==0.13.1=py38h06a4308_0
  - defaults/noarch::python-dateutil==2.8.2=pyhd3eb1b0_0
  - defaults/linux-64::webencodings==0.5.1=py38_1
  - defaults/linux-64::libxslt==1.1.35=h4e12654_0
  - defaults/linux-64::libpq==12.9=h16c4e8d_3
  - defaults/linux-64::anyio==3.5.0=py38h06a4308_0
  - defaults/linux-64::libdeflate==1.8=h7f8727e_5
  - defaults/linux-64::urllib3==1.26.12=py38h06a4308_0
  - defaults/noarch::ipywidgets==7.6.5=pyhd3eb1b0_1
  - defaults/linux-64::sqlite==3.39.3=h5082296_0
  - defaults/linux-64::certifi==2022.9.24=py38h06a4308_0
  - defaults/linux-64::expat==2.4.9=h6a678d5_0
  - defaults/linux-64::libstdcxx-ng==11.2.0=h1234567_1
  - defaults/noarch::wheel==0.37.1=pyhd3eb1b0_0
  - defaults/linux-64::qt-main==5.15.2=h327a75a_7
  - defaults/noarch::importlib_resources==5.2.0=pyhd3eb1b0_1
  - defaults/linux-64::debugpy==1.5.1=py38h295c915_0
  - defaults/linux-64::jupyter_server==1.18.1=py38h06a4308_0
  - defaults/linux-64::jupyterlab==3.4.4=py38h06a4308_0
done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 22.9.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/vit

  added / updated specs:
    - bison


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    bison-3.7.5                |       h2531618_1         708 KB
    flex-2.6.4                 |       ha10e3a4_1         308 KB
    m4-1.4.18                  |       h4e445db_0         182 KB
    ------------------------------------------------------------
                                           Total:         1.2 MB

The following NEW packages will be INSTALLED:

  bison              pkgs/main/linux-64::bison-3.7.5-h2531618_1
  flex               pkgs/main/linux-64::flex-2.6.4-ha10e3a4_1
  m4                 pkgs/main/linux-64::m4-1.4.18-h4e445db_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
m4-1.4.18            | 182 KB    | ############################################################################# | 100%
bison-3.7.5          | 708 KB    | ############################################################################# | 100%
flex-2.6.4           | 308 KB    | ############################################################################# | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(vit) yekyaw.thu@gpu:~/tool/graphviz$
```

Install flex with conda ...  

```
(vit) yekyaw.thu@gpu:~/tool/graphviz$ conda install flex
Collecting package metadata (current_repodata.json): done
Solving environment: -
The environment is inconsistent, please check the package plan carefully
The following packages are causing the inconsistency:

  - defaults/linux-64::libxml2==2.9.14=h74e7548_0
  - defaults/noarch::argon2-cffi==21.3.0=pyhd3eb1b0_0
  - defaults/linux-64::m4==1.4.18=h4e445db_0
  - defaults/linux-64::tornado==6.2=py38h5eee18b_0
  - defaults/noarch::bleach==4.1.0=pyhd3eb1b0_0
  - defaults/noarch::send2trash==1.8.0=pyhd3eb1b0_1
  - defaults/linux-64::pysocks==1.7.1=py38h06a4308_0
  - defaults/noarch::prompt-toolkit==3.0.20=pyhd3eb1b0_0
  - defaults/linux-64::freetype==2.12.1=h4a9f257_0
  - defaults/linux-64::sniffio==1.2.0=py38h06a4308_1
  - defaults/linux-64::libedit==3.1.20210910=h7f8727e_0
  - defaults/linux-64::libwebp-base==1.2.4=h5eee18b_0
  - defaults/noarch::pygments==2.11.2=pyhd3eb1b0_0
  - defaults/linux-64::entrypoints==0.4=py38h06a4308_0
  - defaults/linux-64::jpeg==9e=h7f8727e_0
  - defaults/linux-64::brotlipy==0.7.0=py38h27cfd23_1003
  - defaults/linux-64::qt-webengine==5.15.9=hd2b0992_4
  - defaults/linux-64::idna==3.4=py38h06a4308_0
  - defaults/linux-64::argon2-cffi-bindings==21.2.0=py38h7f8727e_0
  - defaults/linux-64::typing_extensions==4.3.0=py38h06a4308_0
  - defaults/linux-64::qtconsole==5.3.2=py38h06a4308_0
  - defaults/noarch::prompt_toolkit==3.0.20=hd3eb1b0_0
  - defaults/linux-64::tk==8.6.12=h1ccaba5_0
  - defaults/linux-64::gst-plugins-base==1.14.0=h8213a91_2
  - defaults/noarch::pexpect==4.8.0=pyhd3eb1b0_3
  - defaults/noarch::six==1.16.0=pyhd3eb1b0_1
  - defaults/noarch::toml==0.10.2=pyhd3eb1b0_0
  - defaults/linux-64::soupsieve==2.3.2.post1=py38h06a4308_0
  - defaults/noarch::ipython_genutils==0.2.0=pyhd3eb1b0_1
  - defaults/linux-64::libxcb==1.15=h7f8727e_0
  - defaults/linux-64::bison==3.7.5=h2531618_1
  - defaults/linux-64::ncurses==6.3=h5eee18b_3
  - defaults/linux-64::jinja2==3.1.2=py38h06a4308_0
  - defaults/linux-64::cryptography==38.0.1=py38h9ce1e76_0
  - defaults/noarch::pandocfilters==1.5.0=pyhd3eb1b0_0
  - defaults/noarch::jupyter_console==6.4.3=pyhd3eb1b0_0
  - defaults/linux-64::mistune==0.8.4=py38h7b6447c_1000
  - defaults/linux-64::pyzmq==23.2.0=py38h6a678d5_0
  - defaults/linux-64::nbconvert==6.5.4=py38h06a4308_0
  - defaults/linux-64::matplotlib-inline==0.1.6=py38h06a4308_0
  - defaults/linux-64::notebook==6.5.2=py38h06a4308_0
  - defaults/linux-64::nbformat==5.5.0=py38h06a4308_0
  - defaults/noarch::babel==2.9.1=pyhd3eb1b0_0
  - defaults/linux-64::icu==58.2=he6710b0_3
  - defaults/linux-64::sip==6.6.2=py38h6a678d5_0
  - defaults/noarch::jupyterlab_pygments==0.1.2=py_0
  - defaults/linux-64::requests==2.28.1=py38h06a4308_0
  - defaults/noarch::parso==0.8.3=pyhd3eb1b0_0
  - defaults/linux-64::notebook-shim==0.2.2=py38h06a4308_0
  - defaults/linux-64::ipython==8.6.0=py38h06a4308_0
  - defaults/linux-64::zeromq==4.3.4=h2531618_0
  - defaults/linux-64::beautifulsoup4==4.11.1=py38h06a4308_0
  - defaults/linux-64::psutil==5.9.0=py38h5eee18b_0
  - defaults/linux-64::websocket-client==0.58.0=py38h06a4308_4
  - defaults/linux-64::gstreamer==1.14.0=h28cd5cc_2
  - defaults/linux-64::nbclassic==0.4.8=py38h06a4308_0
  - defaults/linux-64::setuptools==65.5.0=py38h06a4308_0
  - defaults/noarch::jupyterlab_widgets==1.0.0=pyhd3eb1b0_1
  - defaults/noarch::packaging==21.3=pyhd3eb1b0_0
  - defaults/linux-64::markupsafe==2.1.1=py38h7f8727e_0
  - defaults/noarch::ptyprocess==0.7.0=pyhd3eb1b0_2
  - defaults/noarch::pure_eval==0.2.2=pyhd3eb1b0_0
  - defaults/linux-64::qtwebkit==5.212=h4eab89a_4
  - defaults/linux-64::libclang==10.0.1=default_hb85057a_2
  - defaults/linux-64::nest-asyncio==1.5.5=py38h06a4308_0
  - defaults/linux-64::libuuid==1.41.5=h5eee18b_0
  - defaults/linux-64::pyrsistent==0.18.0=py38heee7806_0
  - defaults/linux-64::cffi==1.15.1=py38h74dc2b5_0
  - defaults/linux-64::nspr==4.33=h295c915_0
  - defaults/linux-64::libwebp==1.2.4=h11a3e52_0
  - defaults/linux-64::nbclient==0.5.13=py38h06a4308_0
  - defaults/linux-64::pyparsing==3.0.9=py38h06a4308_0
  - defaults/linux-64::python-fastjsonschema==2.16.2=py38h06a4308_0
  - defaults/noarch::stack_data==0.2.0=pyhd3eb1b0_0
  - defaults/linux-64::fontconfig==2.13.1=hef1e5e3_1
  - defaults/linux-64::xz==5.2.6=h5eee18b_0
  - defaults/linux-64::jupyterlab_server==2.15.2=py38h06a4308_0
  - defaults/noarch::defusedxml==0.7.1=pyhd3eb1b0_0
  - defaults/linux-64::giflib==5.2.1=h7b6447c_0
  - defaults/linux-64::pcre==8.45=h295c915_0
  - defaults/linux-64::pip==22.2.2=py38h06a4308_0
  - defaults/linux-64::libpng==1.6.37=hbc83047_0
  - defaults/noarch::pyopenssl==22.0.0=pyhd3eb1b0_0
  - defaults/linux-64::zlib==1.2.13=h5eee18b_0
  - defaults/linux-64::dbus==1.13.18=hb2f20db_0
  - defaults/linux-64::jupyter==1.0.0=py38h06a4308_8
  - defaults/linux-64::zstd==1.5.2=ha4553b6_0
  - defaults/noarch::traitlets==5.1.1=pyhd3eb1b0_0
  - defaults/linux-64::tinycss2==1.2.1=py38h06a4308_0
  - defaults/linux-64::libgcc-ng==11.2.0=h1234567_1
  - defaults/linux-64::libllvm10==10.0.1=hbcb73fb_5
  - defaults/linux-64::lxml==4.9.1=py38h1edc446_0
  - defaults/noarch::pycparser==2.21=pyhd3eb1b0_0
  - defaults/linux-64::libtiff==4.4.0=hecacb30_2
  - defaults/linux-64::jsonschema==4.16.0=py38h06a4308_0
  - defaults/linux-64::ply==3.11=py38_0
  - defaults/linux-64::libxkbcommon==1.0.1=hfa300c1_0
  - defaults/linux-64::pytz==2022.1=py38h06a4308_0
  - defaults/linux-64::ipykernel==6.15.2=py38h06a4308_0
  - defaults/noarch::attrs==21.4.0=pyhd3eb1b0_0
  - defaults/linux-64::pkgutil-resolve-name==1.3.10=py38h06a4308_0
  - defaults/linux-64::zipp==3.8.0=py38h06a4308_0
  - defaults/linux-64::openssl==1.1.1s=h7f8727e_0
  - defaults/linux-64::pyqt==5.15.7=py38h6a678d5_1
  - defaults/noarch::asttokens==2.0.5=pyhd3eb1b0_0
  - defaults/linux-64::jupyter_client==7.3.5=py38h06a4308_0
  - defaults/linux-64::prometheus_client==0.14.1=py38h06a4308_0
  - defaults/linux-64::qtpy==2.2.0=py38h06a4308_0
  - defaults/noarch::wcwidth==0.2.5=pyhd3eb1b0_0
  - defaults/linux-64::jedi==0.18.1=py38h06a4308_1
  - defaults/linux-64::jupyter_core==4.11.2=py38h06a4308_0
  - defaults/linux-64::pyqt5-sip==12.11.0=py38h6a678d5_1
  - defaults/linux-64::nss==3.74=h0370c37_0
  - defaults/linux-64::libevent==2.1.12=h8f2d780_0
  - defaults/noarch::charset-normalizer==2.0.4=pyhd3eb1b0_0
  - defaults/linux-64::typing-extensions==4.3.0=py38h06a4308_0
  - defaults/linux-64::python==3.8.13=haa1d7c7_1
  - defaults/noarch::executing==0.8.3=pyhd3eb1b0_0
  - defaults/linux-64::lerc==3.0=h295c915_0
  - defaults/linux-64::readline==8.2=h5eee18b_0
  - defaults/linux-64::krb5==1.19.2=hac12032_0
  - defaults/noarch::backcall==0.2.0=pyhd3eb1b0_0
  - defaults/noarch::decorator==5.1.1=pyhd3eb1b0_0
  - defaults/noarch::pickleshare==0.7.5=pyhd3eb1b0_1003
  - defaults/linux-64::importlib-metadata==4.11.3=py38h06a4308_0
  - defaults/linux-64::glib==2.69.1=h4ff587b_1
  - defaults/linux-64::widgetsnbextension==3.5.2=py38h06a4308_0
  - defaults/linux-64::flex==2.6.4=ha10e3a4_1
  - defaults/linux-64::libsodium==1.0.18=h7b6447c_0
  - defaults/linux-64::lz4-c==1.9.3=h295c915_1
  - defaults/noarch::json5==0.9.6=pyhd3eb1b0_0
  - defaults/linux-64::libffi==3.3=he6710b0_2
  - defaults/linux-64::terminado==0.13.1=py38h06a4308_0
  - defaults/noarch::python-dateutil==2.8.2=pyhd3eb1b0_0
  - defaults/linux-64::webencodings==0.5.1=py38_1
  - defaults/linux-64::libxslt==1.1.35=h4e12654_0
  - defaults/linux-64::libpq==12.9=h16c4e8d_3
  - defaults/linux-64::anyio==3.5.0=py38h06a4308_0
  - defaults/linux-64::libdeflate==1.8=h7f8727e_5
  - defaults/linux-64::urllib3==1.26.12=py38h06a4308_0
  - defaults/noarch::ipywidgets==7.6.5=pyhd3eb1b0_1
  - defaults/linux-64::sqlite==3.39.3=h5082296_0
  - defaults/linux-64::certifi==2022.9.24=py38h06a4308_0
  - defaults/linux-64::expat==2.4.9=h6a678d5_0
  - defaults/linux-64::libstdcxx-ng==11.2.0=h1234567_1
  - defaults/noarch::wheel==0.37.1=pyhd3eb1b0_0
  - defaults/linux-64::qt-main==5.15.2=h327a75a_7
  - defaults/noarch::importlib_resources==5.2.0=pyhd3eb1b0_1
  - defaults/linux-64::debugpy==1.5.1=py38h295c915_0
  - defaults/linux-64::jupyter_server==1.18.1=py38h06a4308_0
  - defaults/linux-64::jupyterlab==3.4.4=py38h06a4308_0
done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 22.9.0

Please update conda by running

    $ conda update -n base -c defaults conda



# All requested packages already installed.

(vit) yekyaw.thu@gpu:~/tool/graphviz$
```

Run "make" again and for this time no error! Great! :)  

```
(vit) yekyaw.thu@gpu:~/tool/graphviz$ make
...
...
...
make[3]: Leaving directory '/home/yekyaw.thu/tool/graphviz/share'
make[2]: Leaving directory '/home/yekyaw.thu/tool/graphviz/share'
Making all in graphs
make[2]: Entering directory '/home/yekyaw.thu/tool/graphviz/graphs'
Making all in directed
make[3]: Entering directory '/home/yekyaw.thu/tool/graphviz/graphs/directed'
make[3]: Nothing to be done for 'all'.
make[3]: Leaving directory '/home/yekyaw.thu/tool/graphviz/graphs/directed'
Making all in undirected
make[3]: Entering directory '/home/yekyaw.thu/tool/graphviz/graphs/undirected'
make[3]: Nothing to be done for 'all'.
make[3]: Leaving directory '/home/yekyaw.thu/tool/graphviz/graphs/undirected'
make[3]: Entering directory '/home/yekyaw.thu/tool/graphviz/graphs'
make[3]: Nothing to be done for 'all-am'.
make[3]: Leaving directory '/home/yekyaw.thu/tool/graphviz/graphs'
make[2]: Leaving directory '/home/yekyaw.thu/tool/graphviz/graphs'
Making all in tests
make[2]: Entering directory '/home/yekyaw.thu/tool/graphviz/tests'
Making all in graphs
make[3]: Entering directory '/home/yekyaw.thu/tool/graphviz/tests/graphs'
make[3]: Nothing to be done for 'all'.
make[3]: Leaving directory '/home/yekyaw.thu/tool/graphviz/tests/graphs'
Making all in linux.x86
make[3]: Entering directory '/home/yekyaw.thu/tool/graphviz/tests/linux.x86'
make[3]: Nothing to be done for 'all'.
make[3]: Leaving directory '/home/yekyaw.thu/tool/graphviz/tests/linux.x86'
Making all in unit_tests
make[3]: Entering directory '/home/yekyaw.thu/tool/graphviz/tests/unit_tests'
Making all in lib
make[4]: Entering directory '/home/yekyaw.thu/tool/graphviz/tests/unit_tests/lib'
Making all in common
make[5]: Entering directory '/home/yekyaw.thu/tool/graphviz/tests/unit_tests/lib/common'
make[5]: Nothing to be done for 'all'.
make[5]: Leaving directory '/home/yekyaw.thu/tool/graphviz/tests/unit_tests/lib/common'
make[5]: Entering directory '/home/yekyaw.thu/tool/graphviz/tests/unit_tests/lib'
make[5]: Nothing to be done for 'all-am'.
make[5]: Leaving directory '/home/yekyaw.thu/tool/graphviz/tests/unit_tests/lib'
make[4]: Leaving directory '/home/yekyaw.thu/tool/graphviz/tests/unit_tests/lib'
make[4]: Entering directory '/home/yekyaw.thu/tool/graphviz/tests/unit_tests'
make[4]: Nothing to be done for 'all-am'.
make[4]: Leaving directory '/home/yekyaw.thu/tool/graphviz/tests/unit_tests'
make[3]: Leaving directory '/home/yekyaw.thu/tool/graphviz/tests/unit_tests'
Making all in regression_tests
make[3]: Entering directory '/home/yekyaw.thu/tool/graphviz/tests/regression_tests'
Making all in shapes
make[4]: Entering directory '/home/yekyaw.thu/tool/graphviz/tests/regression_tests/shapes'
Making all in reference
make[5]: Entering directory '/home/yekyaw.thu/tool/graphviz/tests/regression_tests/shapes/reference'
make[5]: Nothing to be done for 'all'.
make[5]: Leaving directory '/home/yekyaw.thu/tool/graphviz/tests/regression_tests/shapes/reference'
make[5]: Entering directory '/home/yekyaw.thu/tool/graphviz/tests/regression_tests/shapes'
make[5]: Nothing to be done for 'all-am'.
make[5]: Leaving directory '/home/yekyaw.thu/tool/graphviz/tests/regression_tests/shapes'
make[4]: Leaving directory '/home/yekyaw.thu/tool/graphviz/tests/regression_tests/shapes'
Making all in vuln
make[4]: Entering directory '/home/yekyaw.thu/tool/graphviz/tests/regression_tests/vuln'
Making all in input
make[5]: Entering directory '/home/yekyaw.thu/tool/graphviz/tests/regression_tests/vuln/input'
make[5]: Nothing to be done for 'all'.
make[5]: Leaving directory '/home/yekyaw.thu/tool/graphviz/tests/regression_tests/vuln/input'
Making all in reference
make[5]: Entering directory '/home/yekyaw.thu/tool/graphviz/tests/regression_tests/vuln/reference'
make[5]: Nothing to be done for 'all'.
make[5]: Leaving directory '/home/yekyaw.thu/tool/graphviz/tests/regression_tests/vuln/reference'
make[5]: Entering directory '/home/yekyaw.thu/tool/graphviz/tests/regression_tests/vuln'
make[5]: Nothing to be done for 'all-am'.
make[5]: Leaving directory '/home/yekyaw.thu/tool/graphviz/tests/regression_tests/vuln'
make[4]: Leaving directory '/home/yekyaw.thu/tool/graphviz/tests/regression_tests/vuln'
make[4]: Entering directory '/home/yekyaw.thu/tool/graphviz/tests/regression_tests'
make[4]: Nothing to be done for 'all-am'.
make[4]: Leaving directory '/home/yekyaw.thu/tool/graphviz/tests/regression_tests'
make[3]: Leaving directory '/home/yekyaw.thu/tool/graphviz/tests/regression_tests'
make[3]: Entering directory '/home/yekyaw.thu/tool/graphviz/tests'
make[3]: Nothing to be done for 'all-am'.
make[3]: Leaving directory '/home/yekyaw.thu/tool/graphviz/tests'
make[2]: Leaving directory '/home/yekyaw.thu/tool/graphviz/tests'
make[2]: Entering directory '/home/yekyaw.thu/tool/graphviz'
make[2]: Leaving directory '/home/yekyaw.thu/tool/graphviz'
make[1]: Leaving directory '/home/yekyaw.thu/tool/graphviz'
(vit) yekyaw.thu@gpu:~/tool/graphviz$
```

now time for running "make install" ...  

```
make[3]: Entering directory '/home/yekyaw.thu/tool/graphviz/libltdl'
make[4]: Entering directory '/home/yekyaw.thu/tool/graphviz/libltdl'
make[4]: Leaving directory '/home/yekyaw.thu/tool/graphviz/libltdl'
make[3]: Leaving directory '/home/yekyaw.thu/tool/graphviz/libltdl'
make[2]: Leaving directory '/home/yekyaw.thu/tool/graphviz/libltdl'
Making install in lib
make[2]: Entering directory '/home/yekyaw.thu/tool/graphviz/lib'
Making install in cdt
make[3]: Entering directory '/home/yekyaw.thu/tool/graphviz/lib/cdt'
make[4]: Entering directory '/home/yekyaw.thu/tool/graphviz/lib/cdt'
 /usr/bin/mkdir -p '/usr/local/lib'
 /bin/bash ../../libtool   --mode=install /usr/bin/install -c   libcdt.la '/usr/local/lib'
libtool: install: /usr/bin/install -c .libs/libcdt.so.5.0.0 /usr/local/lib/libcdt.so.5.0.0
/usr/bin/install: cannot create regular file '/usr/local/lib/libcdt.so.5.0.0': Permission denied
make[4]: *** [Makefile:637: install-libLTLIBRARIES] Error 1
make[4]: Leaving directory '/home/yekyaw.thu/tool/graphviz/lib/cdt'
make[3]: *** [Makefile:950: install-am] Error 2
make[3]: Leaving directory '/home/yekyaw.thu/tool/graphviz/lib/cdt'
make[2]: *** [Makefile:582: install-recursive] Error 1
make[2]: Leaving directory '/home/yekyaw.thu/tool/graphviz/lib'
make[1]: *** [Makefile:798: install-recursive] Error 1
make[1]: Leaving directory '/home/yekyaw.thu/tool/graphviz'
make: *** [Makefile:1101: install] Error 2
(vit) yekyaw.thu@gpu:~/tool/graphviz$
```

No sudo right ... and thus ... confirm again ...  

```
(vit) yekyaw.thu@gpu:~/tool/graphviz$ pip3 install pydot graphviz
Requirement already satisfied: pydot in /home/yekyaw.thu/.conda/envs/vit/lib/python3.8/site-packages (1.4.2)
Requirement already satisfied: graphviz in /home/yekyaw.thu/.conda/envs/vit/lib/python3.8/site-packages (0.20.1)
Requirement already satisfied: pyparsing>=2.1.4 in /home/yekyaw.thu/.conda/envs/vit/lib/python3.8/site-packages (from pydot) (3.0.9)
(vit) yekyaw.thu@gpu:~/tool/graphviz$
```

I also did "pip uninstall pydot", "pip uninstall graphivz" and reinstall both libraries and also run "pip install pydotplus". However, still give following errors inside Jupyter when I run "tf.keras.utils.plot_model(ViT_model, rankdir='TB')":  

```
You must install pydot (`pip install pydot`) and install graphviz (see instructions at https://graphviz.gitlab.io/download/) for plot_model to work.
```

I run "conda install pydot" and "conda install graphviz".  
And restart Jupyter kernel and now draw the graph. OK!!! :)  

Now training the ViT model ...  

```
Every 2.0s: nvidia-smi                                                               gpu.cadt.edu.kh: Thu Nov 17 18:11:10 2022
Thu Nov 17 18:11:10 2022
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 470.141.03   Driver Version: 470.141.03   CUDA Version: 11.4     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:0A:00.0 Off |                  N/A |
| 81%   76C    P2   206W / 300W |  10602MiB / 11019MiB |     67%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  NVIDIA GeForce ...  Off  | 00000000:42:00.0 Off |                  N/A |
|  0%   52C    P8    15W / 257W |    330MiB / 11019MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   2  NVIDIA GeForce ...  Off  | 00000000:43:00.0 Off |                  N/A |
| 30%   43C    P8    30W / 250W |    330MiB / 11016MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A    318073      C   ...conda/envs/vit/bin/python    10599MiB |
|    1   N/A  N/A    318073      C   ...conda/envs/vit/bin/python      327MiB |
|    2   N/A  N/A    318073      C   ...conda/envs/vit/bin/python      327MiB |
+-----------------------------------------------------------------------------+
```

I think the model finished between 20 min to 30 min.  

Installation of seaborn library ...  

```
(vit) yekyaw.thu@gpu:~/tool/graphviz$ pip install seaborn
Collecting seaborn
  Using cached seaborn-0.12.1-py3-none-any.whl (288 kB)
Requirement already satisfied: matplotlib!=3.6.1,>=3.1 in /home/yekyaw.thu/.conda/envs/vit/lib/python3.8/site-packages (from seaborn) (3.6.2)
Collecting pandas>=0.25
  Downloading pandas-1.5.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (12.2 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 12.2/12.2 MB 987.1 kB/s eta 0:00:00
Requirement already satisfied: numpy>=1.17 in /home/yekyaw.thu/.conda/envs/vit/lib/python3.8/site-packages (from seaborn) (1.23.4)
Requirement already satisfied: kiwisolver>=1.0.1 in /home/yekyaw.thu/.conda/envs/vit/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (1.4.4)
Requirement already satisfied: python-dateutil>=2.7 in /home/yekyaw.thu/.conda/envs/vit/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (2.8.2)
Requirement already satisfied: fonttools>=4.22.0 in /home/yekyaw.thu/.conda/envs/vit/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (4.38.0)
Requirement already satisfied: pyparsing>=2.2.1 in /home/yekyaw.thu/.conda/envs/vit/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (3.0.9)
Requirement already satisfied: pillow>=6.2.0 in /home/yekyaw.thu/.conda/envs/vit/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (9.3.0)
Requirement already satisfied: contourpy>=1.0.1 in /home/yekyaw.thu/.conda/envs/vit/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (1.0.6)
Requirement already satisfied: cycler>=0.10 in /home/yekyaw.thu/.conda/envs/vit/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (0.11.0)
Requirement already satisfied: packaging>=20.0 in /home/yekyaw.thu/.conda/envs/vit/lib/python3.8/site-packages (from matplotlib!=3.6.1,>=3.1->seaborn) (21.3)
Requirement already satisfied: pytz>=2020.1 in /home/yekyaw.thu/.conda/envs/vit/lib/python3.8/site-packages (from pandas>=0.25->seaborn) (2022.1)
Requirement already satisfied: six>=1.5 in /home/yekyaw.thu/.conda/envs/vit/lib/python3.8/site-packages (from python-dateutil>=2.7->matplotlib!=3.6.1,>=3.1->seaborn) (1.16.0)
Installing collected packages: pandas, seaborn
Successfully installed pandas-1.5.1 seaborn-0.12.1
(vit) yekyaw.thu@gpu:~/tool/graphviz$
```

I run following code:  

```
pred_class_resnet50 = ViT_model.predict(x_test)

conf_matrix(pred_class_resnet50)
```

got following results:  

```
313/313 [==============================] - 4s 9ms/step
Classification Report:

              precision    recall  f1-score   support

    airplane       0.64      0.68      0.66      1000
  automobile       0.67      0.78      0.72      1000
        bird       0.52      0.54      0.53      1000
         cat       0.45      0.47      0.46      1000
        deer       0.56      0.53      0.55      1000
         dog       0.54      0.53      0.54      1000
        frog       0.72      0.65      0.68      1000
       horse       0.66      0.64      0.65      1000
        ship       0.73      0.73      0.73      1000
       truck       0.71      0.63      0.67      1000

    accuracy                           0.62     10000
   macro avg       0.62      0.62      0.62     10000
weighted avg       0.62      0.62      0.62     10000
```

checked the output heatmap.png file under current running folder:  

```
(vit) yekyaw.thu@gpu:~$ ls
4github  authorized_keys  example.txt  exp  heatmap.png  model.png  tool  vit-model-testing1.ipynb
(vit) yekyaw.thu@gpu:~$
```

Successfully testing ViT model building on Keras with CIFAR-10 dataset!!!  

## Reference

1. https://docs.anaconda.com/anaconda/user-guide/tasks/remote-jupyter-notebook/  
2. https://towardsdatascience.com/remote-computing-with-jupyter-notebooks-5b2860f761e8  

