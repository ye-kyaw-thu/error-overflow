# SwitchOut Experiment with Transformer Architecture

## Git clone

```
(base) ye@ye-System-Product-Name:~/tool$ git clone https://github.com/nsapru/SwitchOut
Cloning into 'SwitchOut'...
remote: Enumerating objects: 121, done.
remote: Total 121 (delta 0), reused 0 (delta 0), pack-reused 121
Receiving objects: 100% (121/121), 38.20 KiB | 1.47 MiB/s, done.
Resolving deltas: 100% (60/60), done.
(base) ye@ye-System-Product-Name:~/tool$ cd SwitchOut/
(base) ye@ye-System-Product-Name:~/tool/SwitchOut$ ls
early_stopping.py  LICENSE  README.md  train.py  transformer.py
```

## Anaconda Env Preparation

```
(base) ye@ye-System-Product-Name:~/tool$ conda create -n switchout_venv python=3.6 anaconda
Collecting package metadata (current_repodata.json): done
Solving environment: failed with repodata from current_repodata.json, will retry with next repodata source.
Collecting package metadata (repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/ye/anaconda3/envs/switchout_venv

  added / updated specs:
    - anaconda
    - python=3.6


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    alabaster-0.7.12           |           py36_0          18 KB
    anaconda-2020.07           |           py36_0          17 KB
    anaconda-client-1.7.2      |           py36_0         147 KB
    argh-0.26.2                |           py36_0          36 KB
    asn1crypto-1.3.0           |           py36_0         164 KB
    astroid-2.4.2              |           py36_0         279 KB
    astropy-4.0.1.post1        |   py36h7b6447c_1         6.1 MB
    atomicwrites-1.4.0         |             py_0          11 KB
    autopep8-1.5.3             |             py_0          45 KB
    backcall-0.2.0             |             py_0          15 KB
    backports.shutil_get_terminal_size-1.0.0|           py36_2           8 KB
    beautifulsoup4-4.9.1       |           py36_0         172 KB
    bitarray-1.4.0             |   py36h7b6447c_0          89 KB
    bkcharts-0.2               |           py36_0         133 KB
    bleach-3.1.5               |             py_0         116 KB
    blosc-1.19.0               |       hd408876_0          71 KB
    bokeh-2.1.1                |           py36_0         5.4 MB
    boto-2.49.0                |           py36_0         1.2 MB
    bottleneck-1.3.2           |   py36heb32a55_1         124 KB
    brotlipy-0.7.0             |py36h7b6447c_1000         323 KB
    ca-certificates-2020.6.24  |                0         125 KB
    certifi-2020.6.20          |           py36_0         156 KB
    cffi-1.14.0                |   py36he30daa8_1         225 KB
    chardet-3.0.4              |        py36_1003         180 KB
    click-7.1.2                |             py_0          71 KB
    cloudpickle-1.5.0          |             py_0          22 KB
    clyent-1.2.2               |           py36_1          19 KB
    contextvars-2.4            |             py_0          12 KB
    cryptography-2.9.2         |   py36h1ba5d50_0         556 KB
    curl-7.71.1                |       hbc83047_1         140 KB
    cycler-0.10.0              |           py36_0          13 KB
    cython-0.29.21             |   py36he6710b0_0         1.9 MB
    cytoolz-0.10.1             |   py36h7b6447c_0         377 KB
    dask-2.20.0                |             py_0           4 KB
    dask-core-2.20.0           |             py_0         590 KB
    dbus-1.13.16               |       hb2f20db_0         501 KB
    decorator-4.4.2            |             py_0          14 KB
    diff-match-patch-20200713  |             py_0          36 KB
    distributed-2.20.0         |           py36_0        1011 KB
    docutils-0.16              |           py36_1         669 KB
    entrypoints-0.3            |           py36_0          12 KB
    et_xmlfile-1.0.1           |          py_1001          12 KB
    expat-2.2.9                |       he6710b0_2         156 KB
    fastcache-1.1.0            |   py36h7b6447c_0          31 KB
    flake8-3.8.3               |             py_0         134 KB
    flask-1.1.2                |             py_0          78 KB
    freetype-2.10.2            |       h5ab3b9f_0         608 KB
    fribidi-1.0.9              |       h7b6447c_0         104 KB
    fsspec-0.7.4               |             py_0          63 KB
    future-0.18.2              |           py36_1         639 KB
    gevent-20.6.2              |   py36h7b6447c_0         1.6 MB
    glib-2.65.0                |       h3eb4bd4_0         2.9 MB
    gmpy2-2.0.8                |   py36h10f8cd9_2         150 KB
    graphite2-1.3.14           |       h23475e2_0          99 KB
    greenlet-0.4.16            |   py36h7b6447c_0          24 KB
    gstreamer-1.14.0           |       hb31296c_0         3.1 MB
    h5py-2.10.0                |   py36h7918eee_0         1.0 MB
    harfbuzz-2.4.0             |       hca77d97_1         850 KB
    html5lib-1.1               |             py_0          93 KB
    icu-58.2                   |       he6710b0_3        10.5 MB
    idna-2.10                  |             py_0          50 KB
    imageio-2.9.0              |             py_0         3.0 MB
    immutables-0.14            |   py36h7b6447c_0          70 KB
    importlib-metadata-1.7.0   |           py36_0          51 KB
    importlib_metadata-1.7.0   |                0          11 KB
    intel-openmp-2020.1        |              217         780 KB
    intervaltree-3.0.2         |             py_1          24 KB
    ipykernel-5.3.2            |   py36h5ca1d4c_0         179 KB
    ipython-7.16.1             |   py36h5ca1d4c_0         999 KB
    ipython_genutils-0.2.0     |           py36_0          39 KB
    isort-4.3.21               |           py36_0          69 KB
    itsdangerous-1.1.0         |           py36_0          28 KB
    jedi-0.17.1                |           py36_0         921 KB
    jeepney-0.4.3              |             py_0          21 KB
    jinja2-2.11.2              |             py_0         103 KB
    joblib-0.16.0              |             py_0         210 KB
    json5-0.9.5                |             py_0          22 KB
    jsonschema-3.2.0           |           py36_0          95 KB
    jupyter-1.0.0              |           py36_7           6 KB
    jupyter_client-6.1.6       |             py_0          84 KB
    jupyter_core-4.6.3         |           py36_0          71 KB
    jupyterlab-2.1.5           |             py_0         3.3 MB
    jupyterlab_server-1.2.0    |             py_0          25 KB
    keyring-21.2.1             |           py36_0          57 KB
    kiwisolver-1.2.0           |   py36hfd86e86_0          84 KB
    krb5-1.18.2                |       h173b8e3_0         1.3 MB
    lazy-object-proxy-1.4.3    |   py36h7b6447c_0          29 KB
    lcms2-2.11                 |       h396b838_0         307 KB
    libarchive-3.4.2           |       h62408e4_0         796 KB
    libcurl-7.71.1             |       h20c2e04_1         305 KB
    libedit-3.1.20191231       |       h14c3975_1         116 KB
    liblief-0.10.1             |       he6710b0_0         1.7 MB
    libllvm9-9.0.1             |       h4a3c616_1        21.0 MB
    libsodium-1.0.18           |       h7b6447c_0         244 KB
    libssh2-1.9.0              |       h1ba5d50_1         269 KB
    libtiff-4.1.0              |       h2733197_1         449 KB
    libxcb-1.14                |       h7b6447c_0         505 KB
    libxml2-2.9.10             |       he19cac6_1         1.2 MB
    libxslt-1.1.34             |       hc22bd24_0         432 KB
    llvmlite-0.33.0            |   py36hc6ec683_1        17.3 MB
    locket-0.2.0               |           py36_1           9 KB
    lxml-4.5.2                 |   py36hefd8a0e_0         1.2 MB
    lz4-c-1.9.2                |       he6710b0_0         191 KB
    lzo-2.10                   |       h7b6447c_2         184 KB
    markupsafe-1.1.1           |   py36h7b6447c_0          29 KB
    matplotlib-3.2.2           |                0          21 KB
    matplotlib-base-3.2.2      |   py36hef1b27d_0         5.4 MB
    mccabe-0.6.1               |           py36_1          14 KB
    mistune-0.8.4              |   py36h7b6447c_0          55 KB
    mkl-2020.1                 |              217       129.0 MB
    mkl-service-2.3.0          |   py36he904b0f_0         219 KB
    mkl_fft-1.1.0              |   py36h23d657b_0         144 KB
    mkl_random-1.1.1           |   py36h0573a6f_0         327 KB
    mock-4.0.2                 |             py_0          32 KB
    more-itertools-8.4.0       |             py_0          42 KB
    mpfr-4.0.2                 |       hb69a4c5_1         487 KB
    mpmath-1.1.0               |           py36_0         776 KB
    msgpack-python-1.0.0       |   py36hfd86e86_1          90 KB
    multipledispatch-0.6.0     |           py36_0          22 KB
    nbconvert-5.6.1            |           py36_0         460 KB
    nbformat-5.0.7             |             py_0          89 KB
    ncurses-6.2                |       he6710b0_1         817 KB
    networkx-2.4               |             py_1         1.1 MB
    nltk-3.5                   |             py_0         976 KB
    nose-1.3.7                 |           py36_2         217 KB
    notebook-6.0.3             |           py36_0         4.0 MB
    numba-0.50.1               |   py36h0573a6f_1         3.1 MB
    numexpr-2.7.1              |   py36h423224d_0         186 KB
    numpy-1.18.5               |   py36ha1c710e_0           5 KB
    numpy-base-1.18.5          |   py36hde5b4d6_0         4.1 MB
    numpydoc-1.1.0             |             py_0          42 KB
    olefile-0.46               |           py36_0          48 KB
    openpyxl-3.0.4             |             py_0         157 KB
    openssl-1.1.1g             |       h7b6447c_0         2.5 MB
    packaging-20.4             |             py_0          36 KB
    pandas-1.0.5               |   py36h0573a6f_0         7.8 MB
    pandoc-2.10                |                0        12.4 MB
    pandocfilters-1.4.2        |           py36_1          13 KB
    pango-1.45.3               |       hd140c19_0         361 KB
    parso-0.7.0                |             py_0          72 KB
    patchelf-0.11              |       he6710b0_0          75 KB
    path-13.1.0                |           py36_0          35 KB
    pathlib2-2.3.5             |           py36_0          37 KB
    patsy-0.5.1                |           py36_0         274 KB
    pcre-8.44                  |       he6710b0_0         212 KB
    pep8-1.7.1                 |           py36_0          53 KB
    pexpect-4.8.0              |           py36_0          82 KB
    pickleshare-0.7.5          |           py36_0          13 KB
    pillow-7.2.0               |   py36hb39fc2d_0         619 KB
    pip-20.1.1                 |           py36_1         1.8 MB
    pixman-0.40.0              |       h7b6447c_0         370 KB
    pkginfo-1.5.0.1            |           py36_0          44 KB
    pluggy-0.13.1              |           py36_0          33 KB
    ply-3.11                   |           py36_0          81 KB
    prometheus_client-0.8.0    |             py_0          47 KB
    prompt-toolkit-3.0.5       |             py_0         245 KB
    prompt_toolkit-3.0.5       |                0          11 KB
    psutil-5.7.0               |   py36h7b6447c_0         315 KB
    ptyprocess-0.6.0           |           py36_0          23 KB
    py-1.9.0                   |             py_0          79 KB
    py-lief-0.10.1             |   py36h403a769_0         921 KB
    pycodestyle-2.6.0          |             py_0          43 KB
    pycosat-0.6.3              |   py36h7b6447c_0          82 KB
    pycparser-2.20             |             py_2          94 KB
    pycrypto-2.6.1             |  py36h7b6447c_10         385 KB
    pycurl-7.43.0.5            |   py36h1ba5d50_0          68 KB
    pydocstyle-5.0.2           |             py_0          37 KB
    pyflakes-2.2.0             |             py_0          61 KB
    pygments-2.6.1             |             py_0         654 KB
    pylint-2.5.3               |           py36_0         443 KB
    pyodbc-4.0.30              |   py36he6710b0_0          71 KB
    pyopenssl-19.1.0           |             py_1          48 KB
    pyparsing-2.4.7            |             py_0          65 KB
    pyqt-5.9.2                 |   py36h05f1152_2         4.5 MB
    pyrsistent-0.16.0          |   py36h7b6447c_0          94 KB
    pysocks-1.7.1              |           py36_0          30 KB
    pytables-3.6.1             |   py36h71ec239_0         1.3 MB
    pytest-5.4.3               |           py36_0         387 KB
    python-3.6.10              |       h7579374_2        29.7 MB
    python-jsonrpc-server-0.3.4|             py_1          11 KB
    python-language-server-0.34.1|           py36_0          81 KB
    python-libarchive-c-2.9    |             py_0          46 KB
    pytz-2020.1                |             py_0         184 KB
    pywavelets-1.1.1           |   py36h7b6447c_0         3.5 MB
    pyyaml-5.3.1               |   py36h7b6447c_1         180 KB
    pyzmq-19.0.1               |   py36he6710b0_1         460 KB
    qdarkstyle-2.8.1           |             py_0         176 KB
    qtawesome-0.7.2            |             py_0         724 KB
    qtconsole-4.7.5            |             py_0          96 KB
    readline-8.0               |       h7b6447c_0         356 KB
    regex-2020.6.8             |   py36h7b6447c_0         326 KB
    requests-2.24.0            |             py_0          56 KB
    rope-0.17.0                |             py_0         127 KB
    rtree-0.9.4                |           py36_1          47 KB
    ruamel_yaml-0.15.87        |   py36h7b6447c_1         244 KB
    scikit-image-0.16.2        |   py36h0573a6f_0        23.1 MB
    scikit-learn-0.23.1        |   py36h423224d_0         5.1 MB
    scipy-1.5.0                |   py36h0b6359f_0        14.4 MB
    seaborn-0.10.1             |             py_0         163 KB
    secretstorage-3.1.2        |           py36_0          25 KB
    send2trash-1.5.0           |           py36_0          16 KB
    setuptools-49.2.0          |           py36_0         748 KB
    simplegeneric-0.8.1        |           py36_2          10 KB
    singledispatch-3.4.0.3     |           py36_0          16 KB
    sip-4.19.8                 |   py36hf484d3e_0         274 KB
    six-1.15.0                 |             py_0          13 KB
    snappy-1.1.8               |       he6710b0_0          40 KB
    sortedcollections-1.2.1    |             py_0          13 KB
    sortedcontainers-2.2.2     |             py_0          29 KB
    soupsieve-2.0.1            |             py_0          33 KB
    sphinx-3.1.2               |             py_0         1.1 MB
    sphinxcontrib-1.0          |           py36_1           4 KB
    sphinxcontrib-applehelp-1.0.2|             py_0          27 KB
    sphinxcontrib-devhelp-1.0.2|             py_0          22 KB
    sphinxcontrib-htmlhelp-1.0.3|             py_0          27 KB
    sphinxcontrib-qthelp-1.0.3 |             py_0          25 KB
    sphinxcontrib-serializinghtml-1.1.4|             py_0          24 KB
    sphinxcontrib-websupport-1.2.3|             py_0          36 KB
    spyder-4.1.4               |           py36_0         5.6 MB
    spyder-kernels-1.9.2       |           py36_0          97 KB
    sqlalchemy-1.3.18          |   py36h7b6447c_0         1.5 MB
    sqlite-3.32.3              |       h62c20be_0         1.1 MB
    statsmodels-0.11.1         |   py36h7b6447c_0         7.9 MB
    sympy-1.6.1                |           py36_0         8.5 MB
    terminado-0.8.3            |           py36_0          26 KB
    threadpoolctl-2.1.0        |     pyh5ca1d4c_0          17 KB
    tk-8.6.10                  |       hbc83047_0         3.0 MB
    toml-0.10.1                |             py_0          20 KB
    tornado-6.0.4              |   py36h7b6447c_1         597 KB
    tqdm-4.47.0                |             py_0          62 KB
    traitlets-4.3.3            |           py36_0         140 KB
    typed-ast-1.4.1            |   py36h7b6447c_0         187 KB
    typing_extensions-3.7.4.2  |             py_0          27 KB
    ujson-1.35                 |   py36h14c3975_0          25 KB
    unicodecsv-0.14.1          |           py36_0          25 KB
    urllib3-1.25.9             |             py_0         103 KB
    watchdog-0.10.3            |           py36_0          93 KB
    wcwidth-0.2.5              |             py_0          29 KB
    webencodings-0.5.1         |           py36_1          19 KB
    werkzeug-1.0.1             |             py_0         240 KB
    wheel-0.34.2               |           py36_0          51 KB
    widgetsnbextension-3.5.1   |           py36_0         862 KB
    wrapt-1.11.2               |   py36h7b6447c_0          49 KB
    wurlitzer-2.0.1            |           py36_0          14 KB
    xlrd-1.2.0                 |           py36_0         176 KB
    xlsxwriter-1.2.9           |             py_0         112 KB
    xlwt-1.3.0                 |           py36_0         159 KB
    yaml-0.2.5                 |       h7b6447c_0          75 KB
    yapf-0.30.0                |             py_0         127 KB
    zeromq-4.3.2               |       he6710b0_2         510 KB
    zict-2.0.0                 |             py_0          13 KB
    zipp-3.1.0                 |             py_0          13 KB
    zope-1.0                   |           py36_1           4 KB
    zope.event-4.4             |           py36_0          10 KB
    zope.interface-4.7.1       |   py36h7b6447c_0         204 KB
    zstd-1.4.5                 |       h0b5b093_0         464 KB
    ------------------------------------------------------------
                                           Total:       402.6 MB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  alabaster          pkgs/main/linux-64::alabaster-0.7.12-py36_0
  anaconda           pkgs/main/linux-64::anaconda-2020.07-py36_0
  anaconda-client    pkgs/main/linux-64::anaconda-client-1.7.2-py36_0
  anaconda-project   pkgs/main/noarch::anaconda-project-0.8.4-py_0
  argh               pkgs/main/linux-64::argh-0.26.2-py36_0
  asn1crypto         pkgs/main/linux-64::asn1crypto-1.3.0-py36_0
  astroid            pkgs/main/linux-64::astroid-2.4.2-py36_0
  astropy            pkgs/main/linux-64::astropy-4.0.1.post1-py36h7b6447c_1
  atomicwrites       pkgs/main/noarch::atomicwrites-1.4.0-py_0
  attrs              pkgs/main/noarch::attrs-19.3.0-py_0
  autopep8           pkgs/main/noarch::autopep8-1.5.3-py_0
  babel              pkgs/main/noarch::babel-2.8.0-py_0
  backcall           pkgs/main/noarch::backcall-0.2.0-py_0
  backports          pkgs/main/noarch::backports-1.0-py_2
  backports.shutil_~ pkgs/main/linux-64::backports.shutil_get_terminal_size-1.0.0-py36_2
  beautifulsoup4     pkgs/main/linux-64::beautifulsoup4-4.9.1-py36_0
  bitarray           pkgs/main/linux-64::bitarray-1.4.0-py36h7b6447c_0
  bkcharts           pkgs/main/linux-64::bkcharts-0.2-py36_0
  blas               pkgs/main/linux-64::blas-1.0-mkl
  bleach             pkgs/main/noarch::bleach-3.1.5-py_0
  blosc              pkgs/main/linux-64::blosc-1.19.0-hd408876_0
  bokeh              pkgs/main/linux-64::bokeh-2.1.1-py36_0
  boto               pkgs/main/linux-64::boto-2.49.0-py36_0
  bottleneck         pkgs/main/linux-64::bottleneck-1.3.2-py36heb32a55_1
  brotlipy           pkgs/main/linux-64::brotlipy-0.7.0-py36h7b6447c_1000
  bzip2              pkgs/main/linux-64::bzip2-1.0.8-h7b6447c_0
  ca-certificates    pkgs/main/linux-64::ca-certificates-2020.6.24-0
  cairo              pkgs/main/linux-64::cairo-1.14.12-h8948797_3
  certifi            pkgs/main/linux-64::certifi-2020.6.20-py36_0
  cffi               pkgs/main/linux-64::cffi-1.14.0-py36he30daa8_1
  chardet            pkgs/main/linux-64::chardet-3.0.4-py36_1003
  click              pkgs/main/noarch::click-7.1.2-py_0
  cloudpickle        pkgs/main/noarch::cloudpickle-1.5.0-py_0
  clyent             pkgs/main/linux-64::clyent-1.2.2-py36_1
  colorama           pkgs/main/noarch::colorama-0.4.3-py_0
  contextlib2        pkgs/main/noarch::contextlib2-0.6.0.post1-py_0
  contextvars        pkgs/main/noarch::contextvars-2.4-py_0
  cryptography       pkgs/main/linux-64::cryptography-2.9.2-py36h1ba5d50_0
  curl               pkgs/main/linux-64::curl-7.71.1-hbc83047_1
  cycler             pkgs/main/linux-64::cycler-0.10.0-py36_0
  cython             pkgs/main/linux-64::cython-0.29.21-py36he6710b0_0
  cytoolz            pkgs/main/linux-64::cytoolz-0.10.1-py36h7b6447c_0
  dask               pkgs/main/noarch::dask-2.20.0-py_0
  dask-core          pkgs/main/noarch::dask-core-2.20.0-py_0
  dbus               pkgs/main/linux-64::dbus-1.13.16-hb2f20db_0
  decorator          pkgs/main/noarch::decorator-4.4.2-py_0
  defusedxml         pkgs/main/noarch::defusedxml-0.6.0-py_0
  diff-match-patch   pkgs/main/noarch::diff-match-patch-20200713-py_0
  distributed        pkgs/main/linux-64::distributed-2.20.0-py36_0
  docutils           pkgs/main/linux-64::docutils-0.16-py36_1
  entrypoints        pkgs/main/linux-64::entrypoints-0.3-py36_0
  et_xmlfile         pkgs/main/noarch::et_xmlfile-1.0.1-py_1001
  expat              pkgs/main/linux-64::expat-2.2.9-he6710b0_2
  fastcache          pkgs/main/linux-64::fastcache-1.1.0-py36h7b6447c_0
  filelock           pkgs/main/noarch::filelock-3.0.12-py_0
  flake8             pkgs/main/noarch::flake8-3.8.3-py_0
  flask              pkgs/main/noarch::flask-1.1.2-py_0
  fontconfig         pkgs/main/linux-64::fontconfig-2.13.0-h9420a91_0
  freetype           pkgs/main/linux-64::freetype-2.10.2-h5ab3b9f_0
  fribidi            pkgs/main/linux-64::fribidi-1.0.9-h7b6447c_0
  fsspec             pkgs/main/noarch::fsspec-0.7.4-py_0
  future             pkgs/main/linux-64::future-0.18.2-py36_1
  get_terminal_size  pkgs/main/linux-64::get_terminal_size-1.0.0-haa9412d_0
  gevent             pkgs/main/linux-64::gevent-20.6.2-py36h7b6447c_0
  glib               pkgs/main/linux-64::glib-2.65.0-h3eb4bd4_0
  glob2              pkgs/main/noarch::glob2-0.7-py_0
  gmp                pkgs/main/linux-64::gmp-6.1.2-h6c8ec71_1
  gmpy2              pkgs/main/linux-64::gmpy2-2.0.8-py36h10f8cd9_2
  graphite2          pkgs/main/linux-64::graphite2-1.3.14-h23475e2_0
  greenlet           pkgs/main/linux-64::greenlet-0.4.16-py36h7b6447c_0
  gst-plugins-base   pkgs/main/linux-64::gst-plugins-base-1.14.0-hbbd80ab_1
  gstreamer          pkgs/main/linux-64::gstreamer-1.14.0-hb31296c_0
  h5py               pkgs/main/linux-64::h5py-2.10.0-py36h7918eee_0
  harfbuzz           pkgs/main/linux-64::harfbuzz-2.4.0-hca77d97_1
  hdf5               pkgs/main/linux-64::hdf5-1.10.4-hb1b8bf9_0
  heapdict           pkgs/main/noarch::heapdict-1.0.1-py_0
  html5lib           pkgs/main/noarch::html5lib-1.1-py_0
  icu                pkgs/main/linux-64::icu-58.2-he6710b0_3
  idna               pkgs/main/noarch::idna-2.10-py_0
  imageio            pkgs/main/noarch::imageio-2.9.0-py_0
  imagesize          pkgs/main/noarch::imagesize-1.2.0-py_0
  immutables         pkgs/main/linux-64::immutables-0.14-py36h7b6447c_0
  importlib-metadata pkgs/main/linux-64::importlib-metadata-1.7.0-py36_0
  importlib_metadata pkgs/main/noarch::importlib_metadata-1.7.0-0
  intel-openmp       pkgs/main/linux-64::intel-openmp-2020.1-217
  intervaltree       pkgs/main/noarch::intervaltree-3.0.2-py_1
  ipykernel          pkgs/main/linux-64::ipykernel-5.3.2-py36h5ca1d4c_0
  ipython            pkgs/main/linux-64::ipython-7.16.1-py36h5ca1d4c_0
  ipython_genutils   pkgs/main/linux-64::ipython_genutils-0.2.0-py36_0
  ipywidgets         pkgs/main/noarch::ipywidgets-7.5.1-py_0
  isort              pkgs/main/linux-64::isort-4.3.21-py36_0
  itsdangerous       pkgs/main/linux-64::itsdangerous-1.1.0-py36_0
  jbig               pkgs/main/linux-64::jbig-2.1-hdba287a_0
  jdcal              pkgs/main/noarch::jdcal-1.4.1-py_0
  jedi               pkgs/main/linux-64::jedi-0.17.1-py36_0
  jeepney            pkgs/main/noarch::jeepney-0.4.3-py_0
  jinja2             pkgs/main/noarch::jinja2-2.11.2-py_0
  joblib             pkgs/main/noarch::joblib-0.16.0-py_0
  jpeg               pkgs/main/linux-64::jpeg-9b-h024ee3a_2
  json5              pkgs/main/noarch::json5-0.9.5-py_0
  jsonschema         pkgs/main/linux-64::jsonschema-3.2.0-py36_0
  jupyter            pkgs/main/linux-64::jupyter-1.0.0-py36_7
  jupyter_client     pkgs/main/noarch::jupyter_client-6.1.6-py_0
  jupyter_console    pkgs/main/noarch::jupyter_console-6.1.0-py_0
  jupyter_core       pkgs/main/linux-64::jupyter_core-4.6.3-py36_0
  jupyterlab         pkgs/main/noarch::jupyterlab-2.1.5-py_0
  jupyterlab_server  pkgs/main/noarch::jupyterlab_server-1.2.0-py_0
  keyring            pkgs/main/linux-64::keyring-21.2.1-py36_0
  kiwisolver         pkgs/main/linux-64::kiwisolver-1.2.0-py36hfd86e86_0
  krb5               pkgs/main/linux-64::krb5-1.18.2-h173b8e3_0
  lazy-object-proxy  pkgs/main/linux-64::lazy-object-proxy-1.4.3-py36h7b6447c_0
  lcms2              pkgs/main/linux-64::lcms2-2.11-h396b838_0
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.33.1-h53a641e_7
  libarchive         pkgs/main/linux-64::libarchive-3.4.2-h62408e4_0
  libcurl            pkgs/main/linux-64::libcurl-7.71.1-h20c2e04_1
  libedit            pkgs/main/linux-64::libedit-3.1.20191231-h14c3975_1
  libffi             pkgs/main/linux-64::libffi-3.3-he6710b0_2
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-9.1.0-hdf63c60_0
  libgfortran-ng     pkgs/main/linux-64::libgfortran-ng-7.3.0-hdf63c60_0
  liblief            pkgs/main/linux-64::liblief-0.10.1-he6710b0_0
  libllvm9           pkgs/main/linux-64::libllvm9-9.0.1-h4a3c616_1
  libpng             pkgs/main/linux-64::libpng-1.6.37-hbc83047_0
  libsodium          pkgs/main/linux-64::libsodium-1.0.18-h7b6447c_0
  libspatialindex    pkgs/main/linux-64::libspatialindex-1.9.3-he6710b0_0
  libssh2            pkgs/main/linux-64::libssh2-1.9.0-h1ba5d50_1
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-9.1.0-hdf63c60_0
  libtiff            pkgs/main/linux-64::libtiff-4.1.0-h2733197_1
  libtool            pkgs/main/linux-64::libtool-2.4.6-h7b6447c_5
  libuuid            pkgs/main/linux-64::libuuid-1.0.3-h1bed415_2
  libxcb             pkgs/main/linux-64::libxcb-1.14-h7b6447c_0
  libxml2            pkgs/main/linux-64::libxml2-2.9.10-he19cac6_1
  libxslt            pkgs/main/linux-64::libxslt-1.1.34-hc22bd24_0
  llvmlite           pkgs/main/linux-64::llvmlite-0.33.0-py36hc6ec683_1
  locket             pkgs/main/linux-64::locket-0.2.0-py36_1
  lxml               pkgs/main/linux-64::lxml-4.5.2-py36hefd8a0e_0
  lz4-c              pkgs/main/linux-64::lz4-c-1.9.2-he6710b0_0
  lzo                pkgs/main/linux-64::lzo-2.10-h7b6447c_2
  markupsafe         pkgs/main/linux-64::markupsafe-1.1.1-py36h7b6447c_0
  matplotlib         pkgs/main/linux-64::matplotlib-3.2.2-0
  matplotlib-base    pkgs/main/linux-64::matplotlib-base-3.2.2-py36hef1b27d_0
  mccabe             pkgs/main/linux-64::mccabe-0.6.1-py36_1
  mistune            pkgs/main/linux-64::mistune-0.8.4-py36h7b6447c_0
  mkl                pkgs/main/linux-64::mkl-2020.1-217
  mkl-service        pkgs/main/linux-64::mkl-service-2.3.0-py36he904b0f_0
  mkl_fft            pkgs/main/linux-64::mkl_fft-1.1.0-py36h23d657b_0
  mkl_random         pkgs/main/linux-64::mkl_random-1.1.1-py36h0573a6f_0
  mock               pkgs/main/noarch::mock-4.0.2-py_0
  more-itertools     pkgs/main/noarch::more-itertools-8.4.0-py_0
  mpc                pkgs/main/linux-64::mpc-1.1.0-h10f8cd9_1
  mpfr               pkgs/main/linux-64::mpfr-4.0.2-hb69a4c5_1
  mpmath             pkgs/main/linux-64::mpmath-1.1.0-py36_0
  msgpack-python     pkgs/main/linux-64::msgpack-python-1.0.0-py36hfd86e86_1
  multipledispatch   pkgs/main/linux-64::multipledispatch-0.6.0-py36_0
  nbconvert          pkgs/main/linux-64::nbconvert-5.6.1-py36_0
  nbformat           pkgs/main/noarch::nbformat-5.0.7-py_0
  ncurses            pkgs/main/linux-64::ncurses-6.2-he6710b0_1
  networkx           pkgs/main/noarch::networkx-2.4-py_1
  nltk               pkgs/main/noarch::nltk-3.5-py_0
  nose               pkgs/main/linux-64::nose-1.3.7-py36_2
  notebook           pkgs/main/linux-64::notebook-6.0.3-py36_0
  numba              pkgs/main/linux-64::numba-0.50.1-py36h0573a6f_1
  numexpr            pkgs/main/linux-64::numexpr-2.7.1-py36h423224d_0
  numpy              pkgs/main/linux-64::numpy-1.18.5-py36ha1c710e_0
  numpy-base         pkgs/main/linux-64::numpy-base-1.18.5-py36hde5b4d6_0
  numpydoc           pkgs/main/noarch::numpydoc-1.1.0-py_0
  olefile            pkgs/main/linux-64::olefile-0.46-py36_0
  openpyxl           pkgs/main/noarch::openpyxl-3.0.4-py_0
  openssl            pkgs/main/linux-64::openssl-1.1.1g-h7b6447c_0
  packaging          pkgs/main/noarch::packaging-20.4-py_0
  pandas             pkgs/main/linux-64::pandas-1.0.5-py36h0573a6f_0
  pandoc             pkgs/main/linux-64::pandoc-2.10-0
  pandocfilters      pkgs/main/linux-64::pandocfilters-1.4.2-py36_1
  pango              pkgs/main/linux-64::pango-1.45.3-hd140c19_0
  parso              pkgs/main/noarch::parso-0.7.0-py_0
  partd              pkgs/main/noarch::partd-1.1.0-py_0
  patchelf           pkgs/main/linux-64::patchelf-0.11-he6710b0_0
  path               pkgs/main/linux-64::path-13.1.0-py36_0
  path.py            pkgs/main/noarch::path.py-12.4.0-0
  pathlib2           pkgs/main/linux-64::pathlib2-2.3.5-py36_0
  pathtools          pkgs/main/noarch::pathtools-0.1.2-py_1
  patsy              pkgs/main/linux-64::patsy-0.5.1-py36_0
  pcre               pkgs/main/linux-64::pcre-8.44-he6710b0_0
  pep8               pkgs/main/linux-64::pep8-1.7.1-py36_0
  pexpect            pkgs/main/linux-64::pexpect-4.8.0-py36_0
  pickleshare        pkgs/main/linux-64::pickleshare-0.7.5-py36_0
  pillow             pkgs/main/linux-64::pillow-7.2.0-py36hb39fc2d_0
  pip                pkgs/main/linux-64::pip-20.1.1-py36_1
  pixman             pkgs/main/linux-64::pixman-0.40.0-h7b6447c_0
  pkginfo            pkgs/main/linux-64::pkginfo-1.5.0.1-py36_0
  pluggy             pkgs/main/linux-64::pluggy-0.13.1-py36_0
  ply                pkgs/main/linux-64::ply-3.11-py36_0
  prometheus_client  pkgs/main/noarch::prometheus_client-0.8.0-py_0
  prompt-toolkit     pkgs/main/noarch::prompt-toolkit-3.0.5-py_0
  prompt_toolkit     pkgs/main/noarch::prompt_toolkit-3.0.5-0
  psutil             pkgs/main/linux-64::psutil-5.7.0-py36h7b6447c_0
  ptyprocess         pkgs/main/linux-64::ptyprocess-0.6.0-py36_0
  py                 pkgs/main/noarch::py-1.9.0-py_0
  py-lief            pkgs/main/linux-64::py-lief-0.10.1-py36h403a769_0
  pycodestyle        pkgs/main/noarch::pycodestyle-2.6.0-py_0
  pycosat            pkgs/main/linux-64::pycosat-0.6.3-py36h7b6447c_0
  pycparser          pkgs/main/noarch::pycparser-2.20-py_2
  pycrypto           pkgs/main/linux-64::pycrypto-2.6.1-py36h7b6447c_10
  pycurl             pkgs/main/linux-64::pycurl-7.43.0.5-py36h1ba5d50_0
  pydocstyle         pkgs/main/noarch::pydocstyle-5.0.2-py_0
  pyflakes           pkgs/main/noarch::pyflakes-2.2.0-py_0
  pygments           pkgs/main/noarch::pygments-2.6.1-py_0
  pylint             pkgs/main/linux-64::pylint-2.5.3-py36_0
  pyodbc             pkgs/main/linux-64::pyodbc-4.0.30-py36he6710b0_0
  pyopenssl          pkgs/main/noarch::pyopenssl-19.1.0-py_1
  pyparsing          pkgs/main/noarch::pyparsing-2.4.7-py_0
  pyqt               pkgs/main/linux-64::pyqt-5.9.2-py36h05f1152_2
  pyrsistent         pkgs/main/linux-64::pyrsistent-0.16.0-py36h7b6447c_0
  pysocks            pkgs/main/linux-64::pysocks-1.7.1-py36_0
  pytables           pkgs/main/linux-64::pytables-3.6.1-py36h71ec239_0
  pytest             pkgs/main/linux-64::pytest-5.4.3-py36_0
  python             pkgs/main/linux-64::python-3.6.10-h7579374_2
  python-dateutil    pkgs/main/noarch::python-dateutil-2.8.1-py_0
  python-jsonrpc-se~ pkgs/main/noarch::python-jsonrpc-server-0.3.4-py_1
  python-language-s~ pkgs/main/linux-64::python-language-server-0.34.1-py36_0
  python-libarchive~ pkgs/main/noarch::python-libarchive-c-2.9-py_0
  pytz               pkgs/main/noarch::pytz-2020.1-py_0
  pywavelets         pkgs/main/linux-64::pywavelets-1.1.1-py36h7b6447c_0
  pyxdg              pkgs/main/noarch::pyxdg-0.26-py_0
  pyyaml             pkgs/main/linux-64::pyyaml-5.3.1-py36h7b6447c_1
  pyzmq              pkgs/main/linux-64::pyzmq-19.0.1-py36he6710b0_1
  qdarkstyle         pkgs/main/noarch::qdarkstyle-2.8.1-py_0
  qt                 pkgs/main/linux-64::qt-5.9.7-h5867ecd_1
  qtawesome          pkgs/main/noarch::qtawesome-0.7.2-py_0
  qtconsole          pkgs/main/noarch::qtconsole-4.7.5-py_0
  qtpy               pkgs/main/noarch::qtpy-1.9.0-py_0
  readline           pkgs/main/linux-64::readline-8.0-h7b6447c_0
  regex              pkgs/main/linux-64::regex-2020.6.8-py36h7b6447c_0
  requests           pkgs/main/noarch::requests-2.24.0-py_0
  ripgrep            pkgs/main/linux-64::ripgrep-11.0.2-he32d670_0
  rope               pkgs/main/noarch::rope-0.17.0-py_0
  rtree              pkgs/main/linux-64::rtree-0.9.4-py36_1
  ruamel_yaml        pkgs/main/linux-64::ruamel_yaml-0.15.87-py36h7b6447c_1
  scikit-image       pkgs/main/linux-64::scikit-image-0.16.2-py36h0573a6f_0
  scikit-learn       pkgs/main/linux-64::scikit-learn-0.23.1-py36h423224d_0
  scipy              pkgs/main/linux-64::scipy-1.5.0-py36h0b6359f_0
  seaborn            pkgs/main/noarch::seaborn-0.10.1-py_0
  secretstorage      pkgs/main/linux-64::secretstorage-3.1.2-py36_0
  send2trash         pkgs/main/linux-64::send2trash-1.5.0-py36_0
  setuptools         pkgs/main/linux-64::setuptools-49.2.0-py36_0
  simplegeneric      pkgs/main/linux-64::simplegeneric-0.8.1-py36_2
  singledispatch     pkgs/main/linux-64::singledispatch-3.4.0.3-py36_0
  sip                pkgs/main/linux-64::sip-4.19.8-py36hf484d3e_0
  six                pkgs/main/noarch::six-1.15.0-py_0
  snappy             pkgs/main/linux-64::snappy-1.1.8-he6710b0_0
  snowballstemmer    pkgs/main/noarch::snowballstemmer-2.0.0-py_0
  sortedcollections  pkgs/main/noarch::sortedcollections-1.2.1-py_0
  sortedcontainers   pkgs/main/noarch::sortedcontainers-2.2.2-py_0
  soupsieve          pkgs/main/noarch::soupsieve-2.0.1-py_0
  sphinx             pkgs/main/noarch::sphinx-3.1.2-py_0
  sphinxcontrib      pkgs/main/linux-64::sphinxcontrib-1.0-py36_1
  sphinxcontrib-app~ pkgs/main/noarch::sphinxcontrib-applehelp-1.0.2-py_0
  sphinxcontrib-dev~ pkgs/main/noarch::sphinxcontrib-devhelp-1.0.2-py_0
  sphinxcontrib-htm~ pkgs/main/noarch::sphinxcontrib-htmlhelp-1.0.3-py_0
  sphinxcontrib-jsm~ pkgs/main/noarch::sphinxcontrib-jsmath-1.0.1-py_0
  sphinxcontrib-qth~ pkgs/main/noarch::sphinxcontrib-qthelp-1.0.3-py_0
  sphinxcontrib-ser~ pkgs/main/noarch::sphinxcontrib-serializinghtml-1.1.4-py_0
  sphinxcontrib-web~ pkgs/main/noarch::sphinxcontrib-websupport-1.2.3-py_0
  spyder             pkgs/main/linux-64::spyder-4.1.4-py36_0
  spyder-kernels     pkgs/main/linux-64::spyder-kernels-1.9.2-py36_0
  sqlalchemy         pkgs/main/linux-64::sqlalchemy-1.3.18-py36h7b6447c_0
  sqlite             pkgs/main/linux-64::sqlite-3.32.3-h62c20be_0
  statsmodels        pkgs/main/linux-64::statsmodels-0.11.1-py36h7b6447c_0
  sympy              pkgs/main/linux-64::sympy-1.6.1-py36_0
  tbb                pkgs/main/linux-64::tbb-2020.0-hfd86e86_0
  tblib              pkgs/main/noarch::tblib-1.6.0-py_0
  terminado          pkgs/main/linux-64::terminado-0.8.3-py36_0
  testpath           pkgs/main/noarch::testpath-0.4.4-py_0
  threadpoolctl      pkgs/main/noarch::threadpoolctl-2.1.0-pyh5ca1d4c_0
  tk                 pkgs/main/linux-64::tk-8.6.10-hbc83047_0
  toml               pkgs/main/noarch::toml-0.10.1-py_0
  toolz              pkgs/main/noarch::toolz-0.10.0-py_0
  tornado            pkgs/main/linux-64::tornado-6.0.4-py36h7b6447c_1
  tqdm               pkgs/main/noarch::tqdm-4.47.0-py_0
  traitlets          pkgs/main/linux-64::traitlets-4.3.3-py36_0
  typed-ast          pkgs/main/linux-64::typed-ast-1.4.1-py36h7b6447c_0
  typing_extensions  pkgs/main/noarch::typing_extensions-3.7.4.2-py_0
  ujson              pkgs/main/linux-64::ujson-1.35-py36h14c3975_0
  unicodecsv         pkgs/main/linux-64::unicodecsv-0.14.1-py36_0
  unixodbc           pkgs/main/linux-64::unixodbc-2.3.7-h14c3975_0
  urllib3            pkgs/main/noarch::urllib3-1.25.9-py_0
  watchdog           pkgs/main/linux-64::watchdog-0.10.3-py36_0
  wcwidth            pkgs/main/noarch::wcwidth-0.2.5-py_0
  webencodings       pkgs/main/linux-64::webencodings-0.5.1-py36_1
  werkzeug           pkgs/main/noarch::werkzeug-1.0.1-py_0
  wheel              pkgs/main/linux-64::wheel-0.34.2-py36_0
  widgetsnbextension pkgs/main/linux-64::widgetsnbextension-3.5.1-py36_0
  wrapt              pkgs/main/linux-64::wrapt-1.11.2-py36h7b6447c_0
  wurlitzer          pkgs/main/linux-64::wurlitzer-2.0.1-py36_0
  xlrd               pkgs/main/linux-64::xlrd-1.2.0-py36_0
  xlsxwriter         pkgs/main/noarch::xlsxwriter-1.2.9-py_0
  xlwt               pkgs/main/linux-64::xlwt-1.3.0-py36_0
  xz                 pkgs/main/linux-64::xz-5.2.5-h7b6447c_0
  yaml               pkgs/main/linux-64::yaml-0.2.5-h7b6447c_0
  yapf               pkgs/main/noarch::yapf-0.30.0-py_0
  zeromq             pkgs/main/linux-64::zeromq-4.3.2-he6710b0_2
  zict               pkgs/main/noarch::zict-2.0.0-py_0
  zipp               pkgs/main/noarch::zipp-3.1.0-py_0
  zlib               pkgs/main/linux-64::zlib-1.2.11-h7b6447c_3
  zope               pkgs/main/linux-64::zope-1.0-py36_1
  zope.event         pkgs/main/linux-64::zope.event-4.4-py36_0
  zope.interface     pkgs/main/linux-64::zope.interface-4.7.1-py36h7b6447c_0
  zstd               pkgs/main/linux-64::zstd-1.4.5-h0b5b093_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
libssh2-1.9.0        | 269 KB    | ################################################################################### | 100% 
prompt_toolkit-3.0.5 | 11 KB     | ################################################################################### | 100% 
click-7.1.2          | 71 KB     | ################################################################################### | 100% 
ipykernel-5.3.2      | 179 KB    | ################################################################################### | 100% 
cryptography-2.9.2   | 556 KB    | ################################################################################### | 100% 
nltk-3.5             | 976 KB    | ################################################################################### | 100% 
zope-1.0             | 4 KB      | ################################################################################### | 100% 
bitarray-1.4.0       | 89 KB     | ################################################################################### | 100% 
joblib-0.16.0        | 210 KB    | ################################################################################### | 100% 
json5-0.9.5          | 22 KB     | ################################################################################### | 100% 
zstd-1.4.5           | 464 KB    | ################################################################################### | 100% 
path-13.1.0          | 35 KB     | ################################################################################### | 100% 
cycler-0.10.0        | 13 KB     | ################################################################################### | 100% 
python-3.6.10        | 29.7 MB   | ################################################################################### | 100% 
pyodbc-4.0.30        | 71 KB     | ################################################################################### | 100% 
wurlitzer-2.0.1      | 14 KB     | ################################################################################### | 100% 
pygments-2.6.1       | 654 KB    | ################################################################################### | 100% 
mkl-2020.1           | 129.0 MB  | ################################################################################### | 100% 
markupsafe-1.1.1     | 29 KB     | ################################################################################### | 100% 
python-libarchive-c- | 46 KB     | ################################################################################### | 100% 
immutables-0.14      | 70 KB     | ################################################################################### | 100% 
sqlite-3.32.3        | 1.1 MB    | ################################################################################### | 100% 
backcall-0.2.0       | 15 KB     | ################################################################################### | 100% 
cloudpickle-1.5.0    | 22 KB     | ################################################################################### | 100% 
docutils-0.16        | 669 KB    | ################################################################################### | 100% 
nose-1.3.7           | 217 KB    | ################################################################################### | 100% 
pyflakes-2.2.0       | 61 KB     | ################################################################################### | 100% 
ipython_genutils-0.2 | 39 KB     | ################################################################################### | 100% 
pluggy-0.13.1        | 33 KB     | ################################################################################### | 100% 
numba-0.50.1         | 3.1 MB    | ################################################################################### | 100% 
qtconsole-4.7.5      | 96 KB     | ################################################################################### | 100% 
blosc-1.19.0         | 71 KB     | ################################################################################### | 100% 
xlwt-1.3.0           | 159 KB    | ################################################################################### | 100% 
isort-4.3.21         | 69 KB     | ################################################################################### | 100% 
kiwisolver-1.2.0     | 84 KB     | ################################################################################### | 100% 
jupyter_core-4.6.3   | 71 KB     | ################################################################################### | 100% 
sphinxcontrib-serial | 24 KB     | ################################################################################### | 100% 
mccabe-0.6.1         | 14 KB     | ################################################################################### | 100% 
cytoolz-0.10.1       | 377 KB    | ################################################################################### | 100% 
pillow-7.2.0         | 619 KB    | ################################################################################### | 100% 
terminado-0.8.3      | 26 KB     | ################################################################################### | 100% 
py-lief-0.10.1       | 921 KB    | ################################################################################### | 100% 
matplotlib-3.2.2     | 21 KB     | ################################################################################### | 100% 
ujson-1.35           | 25 KB     | ################################################################################### | 100% 
more-itertools-8.4.0 | 42 KB     | ################################################################################### | 100% 
jsonschema-3.2.0     | 95 KB     | ################################################################################### | 100% 
olefile-0.46         | 48 KB     | ################################################################################### | 100% 
distributed-2.20.0   | 1011 KB   | ################################################################################### | 100% 
intervaltree-3.0.2   | 24 KB     | ################################################################################### | 100% 
entrypoints-0.3      | 12 KB     | ################################################################################### | 100% 
matplotlib-base-3.2. | 5.4 MB    | ################################################################################### | 100% 
clyent-1.2.2         | 19 KB     | ################################################################################### | 100% 
pkginfo-1.5.0.1      | 44 KB     | ################################################################################### | 100% 
mock-4.0.2           | 32 KB     | ################################################################################### | 100% 
py-1.9.0             | 79 KB     | ################################################################################### | 100% 
dask-core-2.20.0     | 590 KB    | ################################################################################### | 100% 
mkl-service-2.3.0    | 219 KB    | ################################################################################### | 100% 
widgetsnbextension-3 | 862 KB    | ################################################################################### | 100% 
numexpr-2.7.1        | 186 KB    | ################################################################################### | 100% 
pysocks-1.7.1        | 30 KB     | ################################################################################### | 100% 
pcre-8.44            | 212 KB    | ################################################################################### | 100% 
argh-0.26.2          | 36 KB     | ################################################################################### | 100% 
icu-58.2             | 10.5 MB   | ################################################################################### | 100% 
webencodings-0.5.1   | 19 KB     | ################################################################################### | 100% 
libarchive-3.4.2     | 796 KB    | ################################################################################### | 100% 
alabaster-0.7.12     | 18 KB     | ################################################################################### | 100% 
xlsxwriter-1.2.9     | 112 KB    | ################################################################################### | 100% 
dask-2.20.0          | 4 KB      | ################################################################################### | 100% 
six-1.15.0           | 13 KB     | ################################################################################### | 100% 
pydocstyle-5.0.2     | 37 KB     | ################################################################################### | 100% 
pyqt-5.9.2           | 4.5 MB    | ################################################################################### | 100% 
gstreamer-1.14.0     | 3.1 MB    | ################################################################################### | 100% 
contextvars-2.4      | 12 KB     | ################################################################################### | 100% 
chardet-3.0.4        | 180 KB    | ################################################################################### | 100% 
simplegeneric-0.8.1  | 10 KB     | ################################################################################### | 100% 
decorator-4.4.2      | 14 KB     | ################################################################################### | 100% 
parso-0.7.0          | 72 KB     | ################################################################################### | 100% 
typing_extensions-3. | 27 KB     | ################################################################################### | 100% 
pytz-2020.1          | 184 KB    | ################################################################################### | 100% 
pyrsistent-0.16.0    | 94 KB     | ################################################################################### | 100% 
seaborn-0.10.1       | 163 KB    | ################################################################################### | 100% 
krb5-1.18.2          | 1.3 MB    | ################################################################################### | 100% 
fastcache-1.1.0      | 31 KB     | ################################################################################### | 100% 
toml-0.10.1          | 20 KB     | ################################################################################### | 100% 
liblief-0.10.1       | 1.7 MB    | ################################################################################### | 100% 
pip-20.1.1           | 1.8 MB    | ################################################################################### | 100% 
sphinx-3.1.2         | 1.1 MB    | ################################################################################### | 100% 
diff-match-patch-202 | 36 KB     | ################################################################################### | 100% 
sphinxcontrib-htmlhe | 27 KB     | ################################################################################### | 100% 
pickleshare-0.7.5    | 13 KB     | ################################################################################### | 100% 
expat-2.2.9          | 156 KB    | ################################################################################### | 100% 
locket-0.2.0         | 9 KB      | ################################################################################### | 100% 
pycparser-2.20       | 94 KB     | ################################################################################### | 100% 
fsspec-0.7.4         | 63 KB     | ################################################################################### | 100% 
pytest-5.4.3         | 387 KB    | ################################################################################### | 100% 
graphite2-1.3.14     | 99 KB     | ################################################################################### | 100% 
pycosat-0.6.3        | 82 KB     | ################################################################################### | 100% 
multipledispatch-0.6 | 22 KB     | ################################################################################### | 100% 
pyopenssl-19.1.0     | 48 KB     | ################################################################################### | 100% 
lzo-2.10             | 184 KB    | ################################################################################### | 100% 
snappy-1.1.8         | 40 KB     | ################################################################################### | 100% 
ply-3.11             | 81 KB     | ################################################################################### | 100% 
setuptools-49.2.0    | 748 KB    | ################################################################################### | 100% 
glib-2.65.0          | 2.9 MB    | ################################################################################### | 100% 
pycrypto-2.6.1       | 385 KB    | ################################################################################### | 100% 
idna-2.10            | 50 KB     | ################################################################################### | 100% 
send2trash-1.5.0     | 16 KB     | ################################################################################### | 100% 
msgpack-python-1.0.0 | 90 KB     | ################################################################################### | 100% 
patchelf-0.11        | 75 KB     | ################################################################################### | 100% 
prometheus_client-0. | 47 KB     | ################################################################################### | 100% 
jupyter-1.0.0        | 6 KB      | ################################################################################### | 100% 
libsodium-1.0.18     | 244 KB    | ################################################################################### | 100% 
numpydoc-1.1.0       | 42 KB     | ################################################################################### | 100% 
sphinxcontrib-appleh | 27 KB     | ################################################################################### | 100% 
numpy-1.18.5         | 5 KB      | ################################################################################### | 100% 
pep8-1.7.1           | 53 KB     | ################################################################################### | 100% 
pylint-2.5.3         | 443 KB    | ################################################################################### | 100% 
mkl_fft-1.1.0        | 144 KB    | ################################################################################### | 100% 
curl-7.71.1          | 140 KB    | ################################################################################### | 100% 
pycodestyle-2.6.0    | 43 KB     | ################################################################################### | 100% 
rope-0.17.0          | 127 KB    | ################################################################################### | 100% 
mkl_random-1.1.1     | 327 KB    | ################################################################################### | 100% 
h5py-2.10.0          | 1.0 MB    | ################################################################################### | 100% 
imageio-2.9.0        | 3.0 MB    | ################################################################################### | 100% 
jinja2-2.11.2        | 103 KB    | ################################################################################### | 100% 
llvmlite-0.33.0      | 17.3 MB   | ################################################################################### | 100% 
python-jsonrpc-serve | 11 KB     | ################################################################################### | 100% 
python-language-serv | 81 KB     | ################################################################################### | 100% 
networkx-2.4         | 1.1 MB    | ################################################################################### | 100% 
sortedcollections-1. | 13 KB     | ################################################################################### | 100% 
libcurl-7.71.1       | 305 KB    | ################################################################################### | 100% 
readline-8.0         | 356 KB    | ################################################################################### | 100% 
pandocfilters-1.4.2  | 13 KB     | ################################################################################### | 100% 
importlib_metadata-1 | 11 KB     | ################################################################################### | 100% 
jupyterlab_server-1. | 25 KB     | ################################################################################### | 100% 
freetype-2.10.2      | 608 KB    | ################################################################################### | 100% 
beautifulsoup4-4.9.1 | 172 KB    | ################################################################################### | 100% 
spyder-4.1.4         | 5.6 MB    | ################################################################################### | 100% 
anaconda-2020.07     | 17 KB     | ################################################################################### | 100% 
numpy-base-1.18.5    | 4.1 MB    | ################################################################################### | 100% 
threadpoolctl-2.1.0  | 17 KB     | ################################################################################### | 100% 
sphinxcontrib-devhel | 22 KB     | ################################################################################### | 100% 
packaging-20.4       | 36 KB     | ################################################################################### | 100% 
qdarkstyle-2.8.1     | 176 KB    | ################################################################################### | 100% 
prompt-toolkit-3.0.5 | 245 KB    | ################################################################################### | 100% 
flake8-3.8.3         | 134 KB    | ################################################################################### | 100% 
requests-2.24.0      | 56 KB     | ################################################################################### | 100% 
greenlet-0.4.16      | 24 KB     | ################################################################################### | 100% 
sphinxcontrib-websup | 36 KB     | ################################################################################### | 100% 
brotlipy-0.7.0       | 323 KB    | ################################################################################### | 100% 
fribidi-1.0.9        | 104 KB    | ################################################################################### | 100% 
psutil-5.7.0         | 315 KB    | ################################################################################### | 100% 
urllib3-1.25.9       | 103 KB    | ################################################################################### | 100% 
importlib-metadata-1 | 51 KB     | ################################################################################### | 100% 
nbconvert-5.6.1      | 460 KB    | ################################################################################### | 100% 
sphinxcontrib-1.0    | 4 KB      | ################################################################################### | 100% 
bottleneck-1.3.2     | 124 KB    | ################################################################################### | 100% 
typed-ast-1.4.1      | 187 KB    | ################################################################################### | 100% 
libxml2-2.9.10       | 1.2 MB    | ################################################################################### | 100% 
flask-1.1.2          | 78 KB     | ################################################################################### | 100% 
yaml-0.2.5           | 75 KB     | ################################################################################### | 100% 
gevent-20.6.2        | 1.6 MB    | ################################################################################### | 100% 
bokeh-2.1.1          | 5.4 MB    | ################################################################################### | 100% 
openpyxl-3.0.4       | 157 KB    | ################################################################################### | 100% 
patsy-0.5.1          | 274 KB    | ################################################################################### | 100% 
regex-2020.6.8       | 326 KB    | ################################################################################### | 100% 
secretstorage-3.1.2  | 25 KB     | ################################################################################### | 100% 
sqlalchemy-1.3.18    | 1.5 MB    | ################################################################################### | 100% 
gmpy2-2.0.8          | 150 KB    | ################################################################################### | 100% 
jeepney-0.4.3        | 21 KB     | ################################################################################### | 100% 
sortedcontainers-2.2 | 29 KB     | ################################################################################### | 100% 
singledispatch-3.4.0 | 16 KB     | ################################################################################### | 100% 
pandas-1.0.5         | 7.8 MB    | ################################################################################### | 100% 
pytables-3.6.1       | 1.3 MB    | ################################################################################### | 100% 
statsmodels-0.11.1   | 7.9 MB    | ################################################################################### | 100% 
zeromq-4.3.2         | 510 KB    | ################################################################################### | 100% 
libxcb-1.14          | 505 KB    | ################################################################################### | 100% 
autopep8-1.5.3       | 45 KB     | ################################################################################### | 100% 
qtawesome-0.7.2      | 724 KB    | ################################################################################### | 100% 
intel-openmp-2020.1  | 780 KB    | ################################################################################### | 100% 
tk-8.6.10            | 3.0 MB    | ################################################################################### | 100% 
future-0.18.2        | 639 KB    | ################################################################################### | 100% 
html5lib-1.1         | 93 KB     | ################################################################################### | 100% 
harfbuzz-2.4.0       | 850 KB    | ################################################################################### | 100% 
astroid-2.4.2        | 279 KB    | ################################################################################### | 100% 
ncurses-6.2          | 817 KB    | ################################################################################### | 100% 
ptyprocess-0.6.0     | 23 KB     | ################################################################################### | 100% 
libtiff-4.1.0        | 449 KB    | ################################################################################### | 100% 
pyparsing-2.4.7      | 65 KB     | ################################################################################### | 100% 
itsdangerous-1.1.0   | 28 KB     | ################################################################################### | 100% 
jupyterlab-2.1.5     | 3.3 MB    | ################################################################################### | 100% 
pexpect-4.8.0        | 82 KB     | ################################################################################### | 100% 
sympy-1.6.1          | 8.5 MB    | ################################################################################### | 100% 
cffi-1.14.0          | 225 KB    | ################################################################################### | 100% 
pathlib2-2.3.5       | 37 KB     | ################################################################################### | 100% 
wrapt-1.11.2         | 49 KB     | ################################################################################### | 100% 
boto-2.49.0          | 1.2 MB    | ################################################################################### | 100% 
watchdog-0.10.3      | 93 KB     | ################################################################################### | 100% 
sphinxcontrib-qthelp | 25 KB     | ################################################################################### | 100% 
traitlets-4.3.3      | 140 KB    | ################################################################################### | 100% 
pycurl-7.43.0.5      | 68 KB     | ################################################################################### | 100% 
notebook-6.0.3       | 4.0 MB    | ################################################################################### | 100% 
tqdm-4.47.0          | 62 KB     | ################################################################################### | 100% 
keyring-21.2.1       | 57 KB     | ################################################################################### | 100% 
lxml-4.5.2           | 1.2 MB    | ################################################################################### | 100% 
pandoc-2.10          | 12.4 MB   | ################################################################################### | 100% 
wheel-0.34.2         | 51 KB     | ################################################################################### | 100% 
zict-2.0.0           | 13 KB     | ################################################################################### | 100% 
lz4-c-1.9.2          | 191 KB    | ################################################################################### | 100% 
pixman-0.40.0        | 370 KB    | ################################################################################### | 100% 
libllvm9-9.0.1       | 21.0 MB   | ################################################################################### | 100% 
lcms2-2.11           | 307 KB    | ################################################################################### | 100% 
pyyaml-5.3.1         | 180 KB    | ################################################################################### | 100% 
spyder-kernels-1.9.2 | 97 KB     | ################################################################################### | 100% 
xlrd-1.2.0           | 176 KB    | ################################################################################### | 100% 
dbus-1.13.16         | 501 KB    | ################################################################################### | 100% 
nbformat-5.0.7       | 89 KB     | ################################################################################### | 100% 
astropy-4.0.1.post1  | 6.1 MB    | ################################################################################### | 100% 
ipython-7.16.1       | 999 KB    | ################################################################################### | 100% 
yapf-0.30.0          | 127 KB    | ################################################################################### | 100% 
jupyter_client-6.1.6 | 84 KB     | ################################################################################### | 100% 
lazy-object-proxy-1. | 29 KB     | ################################################################################### | 100% 
cython-0.29.21       | 1.9 MB    | ################################################################################### | 100% 
mistune-0.8.4        | 55 KB     | ################################################################################### | 100% 
zipp-3.1.0           | 13 KB     | ################################################################################### | 100% 
pywavelets-1.1.1     | 3.5 MB    | ################################################################################### | 100% 
libedit-3.1.20191231 | 116 KB    | ################################################################################### | 100% 
certifi-2020.6.20    | 156 KB    | ################################################################################### | 100% 
scikit-learn-0.23.1  | 5.1 MB    | ################################################################################### | 100% 
jedi-0.17.1          | 921 KB    | ################################################################################### | 100% 
ruamel_yaml-0.15.87  | 244 KB    | ################################################################################### | 100% 
anaconda-client-1.7. | 147 KB    | ################################################################################### | 100% 
mpfr-4.0.2           | 487 KB    | ################################################################################### | 100% 
sip-4.19.8           | 274 KB    | ################################################################################### | 100% 
scikit-image-0.16.2  | 23.1 MB   | ################################################################################### | 100% 
unicodecsv-0.14.1    | 25 KB     | ################################################################################### | 100% 
ca-certificates-2020 | 125 KB    | ################################################################################### | 100% 
wcwidth-0.2.5        | 29 KB     | ################################################################################### | 100% 
et_xmlfile-1.0.1     | 12 KB     | ################################################################################### | 100% 
tornado-6.0.4        | 597 KB    | ################################################################################### | 100% 
atomicwrites-1.4.0   | 11 KB     | ################################################################################### | 100% 
zope.interface-4.7.1 | 204 KB    | ################################################################################### | 100% 
mpmath-1.1.0         | 776 KB    | ################################################################################### | 100% 
scipy-1.5.0          | 14.4 MB   | ################################################################################### | 100% 
bleach-3.1.5         | 116 KB    | ################################################################################### | 100% 
libxslt-1.1.34       | 432 KB    | ################################################################################### | 100% 
openssl-1.1.1g       | 2.5 MB    | ################################################################################### | 100% 
pango-1.45.3         | 361 KB    | ################################################################################### | 100% 
backports.shutil_get | 8 KB      | ################################################################################### | 100% 
zope.event-4.4       | 10 KB     | ################################################################################### | 100% 
soupsieve-2.0.1      | 33 KB     | ################################################################################### | 100% 
bkcharts-0.2         | 133 KB    | ################################################################################### | 100% 
asn1crypto-1.3.0     | 164 KB    | ################################################################################### | 100% 
rtree-0.9.4          | 47 KB     | ################################################################################### | 100% 
pyzmq-19.0.1         | 460 KB    | ################################################################################### | 100% 
werkzeug-1.0.1       | 240 KB    | ################################################################################### | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate switchout_venv
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) ye@ye-System-Product-Name:~/tool$ conda activate switchout_venv
(switchout_venv) ye@ye-System-Product-Name:~/tool$
```

## pytorch Installation

recommend လုပ်ထားတဲ့ whl ကိုပဲ သုံးပြီးတော့ installation လုပ်ခဲ့တယ်။  

```
pip install http://download.pytorch.org/whl/cu90/torch-0.3.0.post4-cp36-cp36m-linux_x86_64.whl
```

pytorch installation လုပ်တာက အောက်ပါအတိုင်း အဆင်ပြေပြေနဲ့ ပြီးသွားတယ်လို့ ထင်ပါတယ်။  

(switchout_venv) ye@ye-System-Product-Name:~/tool$ pip install http://download.pytorch.org/whl/cu90/torch-0.3.0.post4-cp36-cp36m-linux_x86_64.whl
Collecting torch==0.3.0.post4
  Downloading http://download.pytorch.org/whl/cu90/torch-0.3.0.post4-cp36-cp36m-linux_x86_64.whl (633.1 MB)
     |████████████████████████████████| 633.1 MB 62.8 MB/s 
Requirement already satisfied: pyyaml in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (from torch==0.3.0.post4) (5.3.1)
Requirement already satisfied: numpy in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (from torch==0.3.0.post4) (1.18.5)
Installing collected packages: torch
Successfully installed torch-0.3.0.post4
(switchout_venv) ye@ye-System-Product-Name:~/tool$```
```

## Other Packages Installation

```
(switchout_venv) ye@ye-System-Product-Name:~/tool$ pip install numpy matplotlib spacy torchtext
Requirement already satisfied: numpy in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (1.18.5)
Requirement already satisfied: matplotlib in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (3.2.2)
Collecting spacy
  Downloading spacy-3.3.0-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (6.2 MB)
     |████████████████████████████████| 6.2 MB 1.8 MB/s 
Collecting torchtext
  Downloading torchtext-0.11.2-cp36-cp36m-manylinux1_x86_64.whl (8.0 MB)
     |████████████████████████████████| 8.0 MB 15.3 MB/s 
Requirement already satisfied: python-dateutil>=2.1 in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (from matplotlib) (2.8.1)
Requirement already satisfied: kiwisolver>=1.0.1 in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (from matplotlib) (1.2.0)
Requirement already satisfied: pyparsing!=2.0.4,!=2.1.2,!=2.1.6,>=2.0.1 in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (from matplotlib) (2.4.7)
Requirement already satisfied: cycler>=0.10 in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (from matplotlib) (0.10.0)
Requirement already satisfied: setuptools in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (from spacy) (49.2.0.post20200714)
Collecting blis<0.8.0,>=0.4.0
  Downloading blis-0.7.7-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (9.9 MB)
     |████████████████████████████████| 9.9 MB 102.2 MB/s 
Collecting catalogue<2.1.0,>=2.0.6
  Downloading catalogue-2.0.7-py3-none-any.whl (17 kB)
Collecting spacy-loggers<2.0.0,>=1.0.0
  Downloading spacy_loggers-1.0.2-py3-none-any.whl (7.2 kB)
Collecting thinc<8.1.0,>=8.0.14
  Downloading thinc-8.0.15-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (655 kB)
     |████████████████████████████████| 655 kB 83.3 MB/s 
Collecting preshed<3.1.0,>=3.0.2
  Downloading preshed-3.0.6-cp36-cp36m-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (127 kB)
     |████████████████████████████████| 127 kB 94.2 MB/s 
Collecting srsly<3.0.0,>=2.4.3
  Downloading srsly-2.4.3-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (456 kB)
     |████████████████████████████████| 456 kB 71.1 MB/s 
Requirement already satisfied: typing-extensions<4.0.0.0,>=3.7.4; python_version < "3.8" in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (from spacy) (3.7.4.2)
Requirement already satisfied: packaging>=20.0 in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (from spacy) (20.4)
Collecting murmurhash<1.1.0,>=0.28.0
  Downloading murmurhash-1.0.7-cp36-cp36m-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (21 kB)
Requirement already satisfied: requests<3.0.0,>=2.13.0 in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (from spacy) (2.24.0)
Collecting spacy-legacy<3.1.0,>=3.0.9
  Downloading spacy_legacy-3.0.9-py2.py3-none-any.whl (20 kB)
Collecting pydantic!=1.8,!=1.8.1,<1.9.0,>=1.7.4
  Downloading pydantic-1.8.2-cp36-cp36m-manylinux2014_x86_64.whl (10.2 MB)
     |████████████████████████████████| 10.2 MB 28.3 MB/s 
Requirement already satisfied: tqdm<5.0.0,>=4.38.0 in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (from spacy) (4.47.0)
Collecting wasabi<1.1.0,>=0.9.1
  Downloading wasabi-0.9.1-py3-none-any.whl (26 kB)
Collecting langcodes<4.0.0,>=3.2.0
  Downloading langcodes-3.3.0-py3-none-any.whl (181 kB)
     |████████████████████████████████| 181 kB 104.9 MB/s 
Collecting pathy>=0.3.5
  Downloading pathy-0.6.1-py3-none-any.whl (42 kB)
     |████████████████████████████████| 42 kB 252 kB/s 
Requirement already satisfied: jinja2 in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (from spacy) (2.11.2)
Collecting typer<0.5.0,>=0.3.0
  Downloading typer-0.4.1-py3-none-any.whl (27 kB)
Collecting cymem<2.1.0,>=2.0.2
  Downloading cymem-2.0.6-cp36-cp36m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (35 kB)
Collecting torch==1.10.2
  Downloading torch-1.10.2-cp36-cp36m-manylinux1_x86_64.whl (881.9 MB)
     |████████████████████████████████| 881.9 MB 12 kB/s 
Requirement already satisfied: six>=1.5 in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (from python-dateutil>=2.1->matplotlib) (1.15.0)
Requirement already satisfied: zipp>=0.5; python_version < "3.8" in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (from catalogue<2.1.0,>=2.0.6->spacy) (3.1.0)
Collecting dataclasses<1.0,>=0.6; python_version < "3.7"
  Using cached dataclasses-0.8-py3-none-any.whl (19 kB)
Requirement already satisfied: contextvars<3,>=2.4; python_version < "3.7" in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (from thinc<8.1.0,>=8.0.14->spacy) (2.4)
Requirement already satisfied: idna<3,>=2.5 in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (from requests<3.0.0,>=2.13.0->spacy) (2.10)
Requirement already satisfied: urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1 in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (from requests<3.0.0,>=2.13.0->spacy) (1.25.9)
Requirement already satisfied: certifi>=2017.4.17 in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (from requests<3.0.0,>=2.13.0->spacy) (2020.6.20)
Requirement already satisfied: chardet<4,>=3.0.2 in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (from requests<3.0.0,>=2.13.0->spacy) (3.0.4)
Collecting smart-open<6.0.0,>=5.0.0
  Downloading smart_open-5.2.1-py3-none-any.whl (58 kB)
     |████████████████████████████████| 58 kB 276 kB/s 
Requirement already satisfied: MarkupSafe>=0.23 in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (from jinja2->spacy) (1.1.1)
Requirement already satisfied: click<9.0.0,>=7.1.1 in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (from typer<0.5.0,>=0.3.0->spacy) (7.1.2)
Requirement already satisfied: immutables>=0.9 in /home/ye/anaconda3/envs/switchout_venv/lib/python3.6/site-packages (from contextvars<3,>=2.4; python_version < "3.7"->thinc<8.1.0,>=8.0.14->spacy) (0.14)
ERROR: pydantic 1.8.2 has requirement typing-extensions>=3.7.4.3, but you'll have typing-extensions 3.7.4.2 which is incompatible.
Installing collected packages: blis, catalogue, wasabi, spacy-loggers, cymem, murmurhash, preshed, dataclasses, pydantic, srsly, thinc, spacy-legacy, langcodes, typer, smart-open, pathy, spacy, torch, torchtext
  Attempting uninstall: torch
    Found existing installation: torch 0.3.0.post4
    Uninstalling torch-0.3.0.post4:
      Successfully uninstalled torch-0.3.0.post4
Successfully installed blis-0.7.7 catalogue-2.0.7 cymem-2.0.6 dataclasses-0.8 langcodes-3.3.0 murmurhash-1.0.7 pathy-0.6.1 preshed-3.0.6 pydantic-1.8.2 smart-open-5.2.1 spacy-3.3.0 spacy-legacy-3.0.9 spacy-loggers-1.0.2 srsly-2.4.3 thinc-8.0.15 torch-1.10.2 torchtext-0.11.2 typer-0.4.1 wasabi-0.9.1
(switchout_venv) ye@ye-System-Product-Name:~/tool$
```

အထက်ပါအတိုင်းပဲ package တစ်ခုအတွက် version မတူဘူးဆိုတဲ့ error message တော့ ပေးနေတယ်။  

```
ERROR: pydantic 1.8.2 has requirement typing-extensions>=3.7.4.3, but you'll have typing-extensions 3.7.4.2 which is incompatible.
```




## Reference

- https://github.com/nsapru/SwitchOut

