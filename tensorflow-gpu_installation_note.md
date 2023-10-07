# Tensorflow-GPU Installation

တခါတလေ Python library ကို installation လုပ်လို့ မရတာက ကိုယ်သုံးနေတဲ့ server ရဲ့ network condition နဲ့လည်း ဆိုင်တတ်တယ်။  
ဒီ log မှာ ဖြစ်နေတဲ့ tensorflow-gpu installation နဲ့ ပတ်သက်တဲ့ error ကိုတော့ နောက်ဆုံးမှာ တွေ့ရတဲ့အတိုင်းပါပဲ pip command ရဲ့ option တစ်ခုဖြစ်တဲ့ `--default-timeout=1000` နဲ့ ပြေလည်သွားပါတယ်။  

## Create New Conda Environment

```
(base) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$ conda create --name bi_lstm_ner python=3.8
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.12.0
  latest version: 23.9.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/ye/anaconda3/envs/bi_lstm_ner

  added / updated specs:
    - python=3.8


The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-5.1-1_gnu
  ca-certificates    pkgs/main/linux-64::ca-certificates-2023.08.22-h06a4308_0
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.38-h1181459_1
  libffi             pkgs/main/linux-64::libffi-3.4.4-h6a678d5_0
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-11.2.0-h1234567_1
  libgomp            pkgs/main/linux-64::libgomp-11.2.0-h1234567_1
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-11.2.0-h1234567_1
  ncurses            pkgs/main/linux-64::ncurses-6.4-h6a678d5_0
  openssl            pkgs/main/linux-64::openssl-3.0.11-h7f8727e_2
  pip                pkgs/main/linux-64::pip-23.2.1-py38h06a4308_0
  python             pkgs/main/linux-64::python-3.8.18-h955ad1f_0
  readline           pkgs/main/linux-64::readline-8.2-h5eee18b_0
  setuptools         pkgs/main/linux-64::setuptools-68.0.0-py38h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.41.2-h5eee18b_0
  tk                 pkgs/main/linux-64::tk-8.6.12-h1ccaba5_0
  wheel              pkgs/main/linux-64::wheel-0.41.2-py38h06a4308_0
  xz                 pkgs/main/linux-64::xz-5.4.2-h5eee18b_0
  zlib               pkgs/main/linux-64::zlib-1.2.13-h5eee18b_0


Proceed ([y]/n)? y

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate bi_lstm_ner
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```

```
(base) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$ conda activate bi_lstm_ner
```

## Start Error of tensorflow-gpu Installation

```
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$ pip install tensorfow-gpu
ERROR: Could not find a version that satisfies the requirement tensorfow-gpu (from versions: none)
ERROR: No matching distribution found for tensorfow-gpu
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$ pip install tensorflow-gpu
Collecting tensorflow-gpu
  Using cached tensorflow-gpu-2.12.0.tar.gz (2.6 kB)
  Preparing metadata (setup.py) ... error
  error: subprocess-exited-with-error

  × python setup.py egg_info did not run successfully.
  │ exit code: 1
  ╰─> [39 lines of output]
      Traceback (most recent call last):
        File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/setuptools/_vendor/packaging/requirements.py", line 35, in __init__
          parsed = _parse_requirement(requirement_string)
        File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/setuptools/_vendor/packaging/_parser.py", line 64, in parse_requirement
          return _parse_requirement(Tokenizer(source, rules=DEFAULT_RULES))
        File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/setuptools/_vendor/packaging/_parser.py", line 82, in _parse_requirement
          url, specifier, marker = _parse_requirement_details(tokenizer)
        File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/setuptools/_vendor/packaging/_parser.py", line 126, in _parse_requirement_details
          marker = _parse_requirement_marker(
        File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/setuptools/_vendor/packaging/_parser.py", line 147, in _parse_requirement_marker
          tokenizer.raise_syntax_error(
        File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/setuptools/_vendor/packaging/_tokenizer.py", line 165, in raise_syntax_error
          raise ParserSyntaxError(
      setuptools.extern.packaging._tokenizer.ParserSyntaxError: Expected end or semicolon (after name and no valid version specifier)
          python_version>"3.7"
                        ^

      The above exception was the direct cause of the following exception:

      Traceback (most recent call last):
        File "<string>", line 2, in <module>
        File "<pip-setuptools-caller>", line 34, in <module>
        File "/tmp/pip-install-6n_e0_8g/tensorflow-gpu_11caafec6b39409fb35822a2f395a573/setup.py", line 40, in <module>
          setuptools.setup()
        File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/setuptools/__init__.py", line 106, in setup
          _install_setup_requires(attrs)
        File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/setuptools/__init__.py", line 77, in _install_setup_requires
          dist.parse_config_files(ignore_option_errors=True)
        File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/setuptools/dist.py", line 900, in parse_config_files
          self._finalize_requires()
        File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/setuptools/dist.py", line 597, in _finalize_requires
          self._move_install_requirements_markers()
        File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/setuptools/dist.py", line 637, in _move_install_requirements_markers
          inst_reqs = list(_reqs.parse(spec_inst_reqs))
        File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/setuptools/_vendor/packaging/requirements.py", line 37, in __init__
          raise InvalidRequirement(str(e)) from e
      setuptools.extern.packaging.requirements.InvalidRequirement: Expected end or semicolon (after name and no valid version specifier)
          python_version>"3.7"
                        ^
      [end of output]

  note: This error originates from a subprocess, and is likely not a problem with pip.
error: metadata-generation-failed

× Encountered error while generating package metadata.
╰─> See above for output.

note: This is an issue with the package mentioned above, not pip.
hint: See above for details.
```

## Try Again with Assigning Exact Version Numbers

```
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$ pip install tensorflow-gpu==2.5.0
Collecting tensorflow-gpu==2.5.0
  Downloading tensorflow_gpu-2.5.0-cp38-cp38-manylinux2010_x86_64.whl (454.4 MB)
     ━━━━╸━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 54.5/454.4 MB 4.8 MB/s eta 0:01:24
ERROR: Exception:
Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_vendor/urllib3/response.py", line 438, in _error_catcher
    yield
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_vendor/urllib3/response.py", line 561, in read
    data = self._fp_read(amt) if not fp_closed else b""
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_vendor/urllib3/response.py", line 527, in _fp_read
    return self._fp.read(amt) if amt is not None else self._fp.read()
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_vendor/cachecontrol/filewrapper.py", line 90, in read
    data = self.__fp.read(amt)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/http/client.py", line 459, in read
    n = self.readinto(b)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/http/client.py", line 503, in readinto
    n = self.fp.readinto(b)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/socket.py", line 669, in readinto
    return self._sock.recv_into(b)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/ssl.py", line 1274, in recv_into
    return self.read(nbytes, buffer)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/ssl.py", line 1132, in read
    return self._sslobj.read(len, buffer)
socket.timeout: The read operation timed out

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/cli/base_command.py", line 180, in exc_logging_wrapper
    status = run_func(*args)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/cli/req_command.py", line 248, in wrapper
    return func(self, options, args)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/commands/install.py", line 377, in run
    requirement_set = resolver.resolve(
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/resolution/resolvelib/resolver.py", line 92, in resolve
    result = self._result = resolver.resolve(
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_vendor/resolvelib/resolvers.py", line 546, in resolve
    state = resolution.resolve(requirements, max_rounds=max_rounds)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_vendor/resolvelib/resolvers.py", line 397, in resolve
    self._add_to_criteria(self.state.criteria, r, parent=None)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_vendor/resolvelib/resolvers.py", line 173, in _add_to_criteria
    if not criterion.candidates:
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_vendor/resolvelib/structs.py", line 156, in __bool__
    return bool(self._sequence)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/resolution/resolvelib/found_candidates.py", line 155, in __bool__
    return any(self)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/resolution/resolvelib/found_candidates.py", line 143, in <genexpr>
    return (c for c in iterator if id(c) not in self._incompatible_ids)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/resolution/resolvelib/found_candidates.py", line 47, in _iter_built
    candidate = func()
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/resolution/resolvelib/factory.py", line 206, in _make_candidate_from_link
    self._link_candidate_cache[link] = LinkCandidate(
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/resolution/resolvelib/candidates.py", line 293, in __init__
    super().__init__(
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/resolution/resolvelib/candidates.py", line 156, in __init__
    self.dist = self._prepare()
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/resolution/resolvelib/candidates.py", line 225, in _prepare
    dist = self._prepare_distribution()
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/resolution/resolvelib/candidates.py", line 304, in _prepare_distribution
    return preparer.prepare_linked_requirement(self._ireq, parallel_builds=True)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/operations/prepare.py", line 538, in prepare_linked_requirement
    return self._prepare_linked_requirement(req, parallel_builds)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/operations/prepare.py", line 609, in _prepare_linked_requirement
    local_file = unpack_url(
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/operations/prepare.py", line 166, in unpack_url
    file = get_http_url(
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/operations/prepare.py", line 107, in get_http_url
    from_path, content_type = download(link, temp_dir.path)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/network/download.py", line 147, in __call__
    for chunk in chunks:
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/cli/progress_bars.py", line 53, in _rich_progress_bar
    for chunk in iterable:
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/network/utils.py", line 63, in response_chunks
    for chunk in response.raw.stream(
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_vendor/urllib3/response.py", line 622, in stream
    data = self.read(amt=amt, decode_content=decode_content)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_vendor/urllib3/response.py", line 587, in read
    raise IncompleteRead(self._fp_bytes_read, self.length_remaining)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/contextlib.py", line 131, in __exit__
    self.gen.throw(type, value, traceback)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_vendor/urllib3/response.py", line 443, in _error_catcher
    raise ReadTimeoutError(self._pool, None, "Read timed out.")
pip._vendor.urllib3.exceptions.ReadTimeoutError: HTTPSConnectionPool(host='files.pythonhosted.org', port=443): Read timed out.
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$
```

## Try Again with --trusted-host

```
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$ pip install tensorflow-gpu==2.5.0 --trusted-host pypi.org --trusted-host files.pythonhosted.org

Collecting tensorflow-gpu==2.5.0
  Downloading tensorflow_gpu-2.5.0-cp38-cp38-manylinux2010_x86_64.whl (454.4 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╺━━━━━━━━ 353.4/454.4 MB 15.6 MB/s eta 0:00:07
ERROR: Exception:
Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_vendor/urllib3/response.py", line 438, in _error_catcher
    yield
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_vendor/urllib3/response.py", line 561, in read
    data = self._fp_read(amt) if not fp_closed else b""
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_vendor/urllib3/response.py", line 527, in _fp_read
    return self._fp.read(amt) if amt is not None else self._fp.read()
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_vendor/cachecontrol/filewrapper.py", line 90, in read
    data = self.__fp.read(amt)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/http/client.py", line 459, in read
    n = self.readinto(b)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/http/client.py", line 503, in readinto
    n = self.fp.readinto(b)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/socket.py", line 669, in readinto
    return self._sock.recv_into(b)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/ssl.py", line 1274, in recv_into
    return self.read(nbytes, buffer)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/ssl.py", line 1132, in read
    return self._sslobj.read(len, buffer)
socket.timeout: The read operation timed out

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/cli/base_command.py", line 180, in exc_logging_wrapper
    status = run_func(*args)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/cli/req_command.py", line 248, in wrapper
    return func(self, options, args)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/commands/install.py", line 377, in run
    requirement_set = resolver.resolve(
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/resolution/resolvelib/resolver.py", line 92, in resolve
    result = self._result = resolver.resolve(
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_vendor/resolvelib/resolvers.py", line 546, in resolve
    state = resolution.resolve(requirements, max_rounds=max_rounds)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_vendor/resolvelib/resolvers.py", line 397, in resolve
    self._add_to_criteria(self.state.criteria, r, parent=None)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_vendor/resolvelib/resolvers.py", line 173, in _add_to_criteria
    if not criterion.candidates:
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_vendor/resolvelib/structs.py", line 156, in __bool__
    return bool(self._sequence)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/resolution/resolvelib/found_candidates.py", line 155, in __bool__
    return any(self)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/resolution/resolvelib/found_candidates.py", line 143, in <genexpr>
    return (c for c in iterator if id(c) not in self._incompatible_ids)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/resolution/resolvelib/found_candidates.py", line 47, in _iter_built
    candidate = func()
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/resolution/resolvelib/factory.py", line 206, in _make_candidate_from_link
    self._link_candidate_cache[link] = LinkCandidate(
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/resolution/resolvelib/candidates.py", line 293, in __init__
    super().__init__(
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/resolution/resolvelib/candidates.py", line 156, in __init__
    self.dist = self._prepare()
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/resolution/resolvelib/candidates.py", line 225, in _prepare
    dist = self._prepare_distribution()
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/resolution/resolvelib/candidates.py", line 304, in _prepare_distribution
    return preparer.prepare_linked_requirement(self._ireq, parallel_builds=True)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/operations/prepare.py", line 538, in prepare_linked_requirement
    return self._prepare_linked_requirement(req, parallel_builds)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/operations/prepare.py", line 609, in _prepare_linked_requirement
    local_file = unpack_url(
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/operations/prepare.py", line 166, in unpack_url
    file = get_http_url(
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/operations/prepare.py", line 107, in get_http_url
    from_path, content_type = download(link, temp_dir.path)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/network/download.py", line 147, in __call__
    for chunk in chunks:
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/cli/progress_bars.py", line 53, in _rich_progress_bar
    for chunk in iterable:
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_internal/network/utils.py", line 63, in response_chunks
    for chunk in response.raw.stream(
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_vendor/urllib3/response.py", line 622, in stream
    data = self.read(amt=amt, decode_content=decode_content)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_vendor/urllib3/response.py", line 587, in read
    raise IncompleteRead(self._fp_bytes_read, self.length_remaining)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/contextlib.py", line 131, in __exit__
    self.gen.throw(type, value, traceback)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/pip/_vendor/urllib3/response.py", line 443, in _error_catcher
    raise ReadTimeoutError(self._pool, None, "Read timed out.")
pip._vendor.urllib3.exceptions.ReadTimeoutError: HTTPSConnectionPool(host='files.pythonhosted.org', port=443): Read timed out.
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$ pip install ./tensorflow_gpu-2.5.0-cp38-cp38-manylinux2010_x86_64.whl
WARNING: Requirement './tensorflow_gpu-2.5.0-cp38-cp38-manylinux2010_x86_64.whl' looks like a filename, but the file does not exist
Processing ./tensorflow_gpu-2.5.0-cp38-cp38-manylinux2010_x86_64.whl
ERROR: Could not install packages due to an OSError: [Errno 2] No such file or directory: '/home/ye/exp/myNER/bi-LSTM/tensorflow_gpu-2.5.0-cp38-cp38-manylinux2010_x86_64.whl'
```

## Try Again with --default-timeout Setting

```
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$ pip --default-timeout=1000 install tensorflow-gpu==2.5.0
Collecting tensorflow-gpu==2.5.0

  Downloading tensorflow_gpu-2.5.0-cp38-cp38-manylinux2010_x86_64.whl (454.4 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 454.4/454.4 MB 1.9 MB/s eta 0:00:00
Collecting numpy~=1.19.2 (from tensorflow-gpu==2.5.0)
  Downloading numpy-1.19.5-cp38-cp38-manylinux2010_x86_64.whl (14.9 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 14.9/14.9 MB 32.6 MB/s eta 0:00:00
Collecting absl-py~=0.10 (from tensorflow-gpu==2.5.0)
  Using cached absl_py-0.15.0-py3-none-any.whl (132 kB)
Collecting astunparse~=1.6.3 (from tensorflow-gpu==2.5.0)
  Using cached astunparse-1.6.3-py2.py3-none-any.whl (12 kB)
Collecting flatbuffers~=1.12.0 (from tensorflow-gpu==2.5.0)
  Using cached flatbuffers-1.12-py2.py3-none-any.whl (15 kB)
Collecting google-pasta~=0.2 (from tensorflow-gpu==2.5.0)
  Using cached google_pasta-0.2.0-py3-none-any.whl (57 kB)
Collecting h5py~=3.1.0 (from tensorflow-gpu==2.5.0)
  Downloading h5py-3.1.0-cp38-cp38-manylinux1_x86_64.whl (4.4 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4.4/4.4 MB 28.4 MB/s eta 0:00:00
Collecting keras-preprocessing~=1.1.2 (from tensorflow-gpu==2.5.0)
  Using cached Keras_Preprocessing-1.1.2-py2.py3-none-any.whl (42 kB)
Collecting opt-einsum~=3.3.0 (from tensorflow-gpu==2.5.0)
  Using cached opt_einsum-3.3.0-py3-none-any.whl (65 kB)
Collecting protobuf>=3.9.2 (from tensorflow-gpu==2.5.0)
  Obtaining dependency information for protobuf>=3.9.2 from https://files.pythonhosted.org/packages/c8/2c/03046cac73f46bfe98fc846ef629cf4f84c2f59258216aa2cc0d22bfca8f/protobuf-4.24.4-cp37-abi3-manylinux2014_x86_64.whl.metadata
  Using cached protobuf-4.24.4-cp37-abi3-manylinux2014_x86_64.whl.metadata (540 bytes)
Collecting six~=1.15.0 (from tensorflow-gpu==2.5.0)
  Using cached six-1.15.0-py2.py3-none-any.whl (10 kB)
Collecting termcolor~=1.1.0 (from tensorflow-gpu==2.5.0)
  Using cached termcolor-1.1.0.tar.gz (3.9 kB)
  Preparing metadata (setup.py) ... done
Collecting typing-extensions~=3.7.4 (from tensorflow-gpu==2.5.0)
  Using cached typing_extensions-3.7.4.3-py3-none-any.whl (22 kB)
Requirement already satisfied: wheel~=0.35 in /home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages (from tensorflow-gpu==2.5.0) (0.41.2)
Collecting wrapt~=1.12.1 (from tensorflow-gpu==2.5.0)
  Using cached wrapt-1.12.1.tar.gz (27 kB)
  Preparing metadata (setup.py) ... done
Collecting gast==0.4.0 (from tensorflow-gpu==2.5.0)
  Using cached gast-0.4.0-py3-none-any.whl (9.8 kB)
Collecting tensorboard~=2.5 (from tensorflow-gpu==2.5.0)
  Obtaining dependency information for tensorboard~=2.5 from https://files.pythonhosted.org/packages/bc/a2/ff5f4c299eb37c95299a76015da3f30211468e29d8d6f1d011683279baee/tensorboard-2.14.0-py3-none-any.whl.metadata
  Using cached tensorboard-2.14.0-py3-none-any.whl.metadata (1.8 kB)
Collecting tensorflow-estimator<2.6.0,>=2.5.0rc0 (from tensorflow-gpu==2.5.0)
  Downloading tensorflow_estimator-2.5.0-py2.py3-none-any.whl (462 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 462.4/462.4 kB 8.3 MB/s eta 0:00:00
Collecting keras-nightly~=2.5.0.dev (from tensorflow-gpu==2.5.0)
  Downloading keras_nightly-2.5.0.dev2021032900-py2.py3-none-any.whl (1.2 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.2/1.2 MB 15.8 MB/s eta 0:00:00
Collecting grpcio~=1.34.0 (from tensorflow-gpu==2.5.0)
  Downloading grpcio-1.34.1-cp38-cp38-manylinux2014_x86_64.whl (4.0 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 4.0/4.0 MB 27.6 MB/s eta 0:00:00
INFO: pip is looking at multiple versions of tensorboard to determine which version is compatible with other requirements. This could take a while.
Collecting tensorboard~=2.5 (from tensorflow-gpu==2.5.0)
  Using cached tensorboard-2.13.0-py3-none-any.whl (5.6 MB)
  Using cached tensorboard-2.12.3-py3-none-any.whl (5.6 MB)
  Using cached tensorboard-2.12.2-py3-none-any.whl (5.6 MB)
  Downloading tensorboard-2.12.1-py3-none-any.whl (5.6 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 5.6/5.6 MB 34.6 MB/s eta 0:00:00
  Using cached tensorboard-2.12.0-py3-none-any.whl (5.6 MB)
  Using cached tensorboard-2.11.2-py3-none-any.whl (6.0 MB)
Collecting google-auth<3,>=1.6.3 (from tensorboard~=2.5->tensorflow-gpu==2.5.0)
  Obtaining dependency information for google-auth<3,>=1.6.3 from https://files.pythonhosted.org/packages/d7/88/1826b0c047c48763b36ed854a984127b430a16b70003155d7b19975f1d59/google_auth-2.23.2-py2.py3-none-any.whl.metadata
  Using cached google_auth-2.23.2-py2.py3-none-any.whl.metadata (4.2 kB)
Collecting google-auth-oauthlib<0.5,>=0.4.1 (from tensorboard~=2.5->tensorflow-gpu==2.5.0)
  Using cached google_auth_oauthlib-0.4.6-py2.py3-none-any.whl (18 kB)
Collecting markdown>=2.6.8 (from tensorboard~=2.5->tensorflow-gpu==2.5.0)
  Obtaining dependency information for markdown>=2.6.8 from https://files.pythonhosted.org/packages/bb/c1/50caaec6cadc1c6adc8fe351e03bd646d6e4dd17f55fca0f4c8d7ea8d3e9/Markdown-3.5-py3-none-any.whl.metadata
  Using cached Markdown-3.5-py3-none-any.whl.metadata (7.1 kB)
Collecting protobuf>=3.9.2 (from tensorflow-gpu==2.5.0)
  Downloading protobuf-3.20.3-cp38-cp38-manylinux_2_5_x86_64.manylinux1_x86_64.whl (1.0 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.0/1.0 MB 18.9 MB/s eta 0:00:00
Collecting requests<3,>=2.21.0 (from tensorboard~=2.5->tensorflow-gpu==2.5.0)
  Obtaining dependency information for requests<3,>=2.21.0 from https://files.pythonhosted.org/packages/70/8e/0e2d847013cb52cd35b38c009bb167a1a26b2ce6cd6965bf26b47bc0bf44/requests-2.31.0-py3-none-any.whl.metadata
  Using cached requests-2.31.0-py3-none-any.whl.metadata (4.6 kB)
Requirement already satisfied: setuptools>=41.0.0 in /home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages (from tensorboard~=2.5->tensorflow-gpu==2.5.0) (68.0.0)
Collecting tensorboard-data-server<0.7.0,>=0.6.0 (from tensorboard~=2.5->tensorflow-gpu==2.5.0)
  Using cached tensorboard_data_server-0.6.1-py3-none-manylinux2010_x86_64.whl (4.9 MB)
Collecting tensorboard-plugin-wit>=1.6.0 (from tensorboard~=2.5->tensorflow-gpu==2.5.0)
  Using cached tensorboard_plugin_wit-1.8.1-py3-none-any.whl (781 kB)
Collecting werkzeug>=1.0.1 (from tensorboard~=2.5->tensorflow-gpu==2.5.0)
  Obtaining dependency information for werkzeug>=1.0.1 from https://files.pythonhosted.org/packages/b6/a5/54b01f663d60d5334f6c9c87c26274e94617a4fd463d812463626423b10d/werkzeug-3.0.0-py3-none-any.whl.metadata
  Using cached werkzeug-3.0.0-py3-none-any.whl.metadata (4.1 kB)
Collecting cachetools<6.0,>=2.0.0 (from google-auth<3,>=1.6.3->tensorboard~=2.5->tensorflow-gpu==2.5.0)
  Obtaining dependency information for cachetools<6.0,>=2.0.0 from https://files.pythonhosted.org/packages/a9/c9/c8a7710f2cedcb1db9224fdd4d8307c9e48cbddc46c18b515fefc0f1abbe/cachetools-5.3.1-py3-none-any.whl.metadata
  Using cached cachetools-5.3.1-py3-none-any.whl.metadata (5.2 kB)
Collecting pyasn1-modules>=0.2.1 (from google-auth<3,>=1.6.3->tensorboard~=2.5->tensorflow-gpu==2.5.0)
  Using cached pyasn1_modules-0.3.0-py2.py3-none-any.whl (181 kB)
Collecting rsa<5,>=3.1.4 (from google-auth<3,>=1.6.3->tensorboard~=2.5->tensorflow-gpu==2.5.0)
  Using cached rsa-4.9-py3-none-any.whl (34 kB)
Collecting requests-oauthlib>=0.7.0 (from google-auth-oauthlib<0.5,>=0.4.1->tensorboard~=2.5->tensorflow-gpu==2.5.0)
  Using cached requests_oauthlib-1.3.1-py2.py3-none-any.whl (23 kB)
Collecting importlib-metadata>=4.4 (from markdown>=2.6.8->tensorboard~=2.5->tensorflow-gpu==2.5.0)
  Obtaining dependency information for importlib-metadata>=4.4 from https://files.pythonhosted.org/packages/cc/37/db7ba97e676af155f5fcb1a35466f446eadc9104e25b83366e8088c9c926/importlib_metadata-6.8.0-py3-none-any.whl.metadata
  Using cached importlib_metadata-6.8.0-py3-none-any.whl.metadata (5.1 kB)
Collecting charset-normalizer<4,>=2 (from requests<3,>=2.21.0->tensorboard~=2.5->tensorflow-gpu==2.5.0)
  Obtaining dependency information for charset-normalizer<4,>=2 from https://files.pythonhosted.org/packages/1e/c8/fd52271326c052f95f47ef718b018aa2bc3fd097d9bac44d7d48894c6130/charset_normalizer-3.3.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata
  Downloading charset_normalizer-3.3.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (32 kB)
Collecting idna<4,>=2.5 (from requests<3,>=2.21.0->tensorboard~=2.5->tensorflow-gpu==2.5.0)
  Using cached idna-3.4-py3-none-any.whl (61 kB)
Collecting urllib3<3,>=1.21.1 (from requests<3,>=2.21.0->tensorboard~=2.5->tensorflow-gpu==2.5.0)
  Obtaining dependency information for urllib3<3,>=1.21.1 from https://files.pythonhosted.org/packages/26/40/9957270221b6d3e9a3b92fdfba80dd5c9661ff45a664b47edd5d00f707f5/urllib3-2.0.6-py3-none-any.whl.metadata
  Using cached urllib3-2.0.6-py3-none-any.whl.metadata (6.6 kB)
Collecting certifi>=2017.4.17 (from requests<3,>=2.21.0->tensorboard~=2.5->tensorflow-gpu==2.5.0)
  Obtaining dependency information for certifi>=2017.4.17 from https://files.pythonhosted.org/packages/4c/dd/2234eab22353ffc7d94e8d13177aaa050113286e93e7b40eae01fbf7c3d9/certifi-2023.7.22-py3-none-any.whl.metadata
  Using cached certifi-2023.7.22-py3-none-any.whl.metadata (2.2 kB)
Collecting MarkupSafe>=2.1.1 (from werkzeug>=1.0.1->tensorboard~=2.5->tensorflow-gpu==2.5.0)
  Obtaining dependency information for MarkupSafe>=2.1.1 from https://files.pythonhosted.org/packages/de/e2/32c14301bb023986dff527a49325b6259cab4ebb4633f69de54af312fc45/MarkupSafe-2.1.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata
  Using cached MarkupSafe-2.1.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (3.0 kB)
Collecting zipp>=0.5 (from importlib-metadata>=4.4->markdown>=2.6.8->tensorboard~=2.5->tensorflow-gpu==2.5.0)
  Obtaining dependency information for zipp>=0.5 from https://files.pythonhosted.org/packages/d9/66/48866fc6b158c81cc2bfecc04c480f105c6040e8b077bc54c634b4a67926/zipp-3.17.0-py3-none-any.whl.metadata
  Using cached zipp-3.17.0-py3-none-any.whl.metadata (3.7 kB)
Collecting pyasn1<0.6.0,>=0.4.6 (from pyasn1-modules>=0.2.1->google-auth<3,>=1.6.3->tensorboard~=2.5->tensorflow-gpu==2.5.0)
  Using cached pyasn1-0.5.0-py2.py3-none-any.whl (83 kB)
Collecting oauthlib>=3.0.0 (from requests-oauthlib>=0.7.0->google-auth-oauthlib<0.5,>=0.4.1->tensorboard~=2.5->tensorflow-gpu==2.5.0)
  Using cached oauthlib-3.2.2-py3-none-any.whl (151 kB)
Using cached google_auth-2.23.2-py2.py3-none-any.whl (181 kB)
Using cached Markdown-3.5-py3-none-any.whl (101 kB)
Using cached requests-2.31.0-py3-none-any.whl (62 kB)
Using cached werkzeug-3.0.0-py3-none-any.whl (226 kB)
Using cached cachetools-5.3.1-py3-none-any.whl (9.3 kB)
Using cached certifi-2023.7.22-py3-none-any.whl (158 kB)
Downloading charset_normalizer-3.3.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (137 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 137.9/137.9 kB 4.4 MB/s eta 0:00:00
Using cached importlib_metadata-6.8.0-py3-none-any.whl (22 kB)
Using cached MarkupSafe-2.1.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (25 kB)
Using cached urllib3-2.0.6-py3-none-any.whl (123 kB)
Using cached zipp-3.17.0-py3-none-any.whl (7.4 kB)
Building wheels for collected packages: termcolor, wrapt
  Building wheel for termcolor (setup.py) ... done
  Created wheel for termcolor: filename=termcolor-1.1.0-py3-none-any.whl size=4832 sha256=6b078b5acc963aa316ad2cad62e6cd8134bc84b1afeec8900229216d117349af
  Stored in directory: /home/ye/.cache/pip/wheels/a0/16/9c/5473df82468f958445479c59e784896fa24f4a5fc024b0f501
  Building wheel for wrapt (setup.py) ... done
  Created wheel for wrapt: filename=wrapt-1.12.1-cp38-cp38-linux_x86_64.whl size=75910 sha256=e7319c2553a732fc75bf32c44fe682b9d36d4d90457f2b489ecee0463c7d0a1b
  Stored in directory: /home/ye/.cache/pip/wheels/5f/fd/9e/b6cf5890494cb8ef0b5eaff72e5d55a70fb56316007d6dfe73
Successfully built termcolor wrapt
Installing collected packages: wrapt, typing-extensions, termcolor, tensorflow-estimator, tensorboard-plugin-wit, keras-nightly, flatbuffers, zipp, urllib3, tensorboard-data-server, six, pyasn1, protobuf, oauthlib, numpy, MarkupSafe, idna, gast, charset-normalizer, certifi, cachetools, werkzeug, rsa, requests, pyasn1-modules, opt-einsum, keras-preprocessing, importlib-metadata, h5py, grpcio, google-pasta, astunparse, absl-py, requests-oauthlib, markdown, google-auth, google-auth-oauthlib, tensorboard, tensorflow-gpu
Successfully installed MarkupSafe-2.1.3 absl-py-0.15.0 astunparse-1.6.3 cachetools-5.3.1 certifi-2023.7.22 charset-normalizer-3.3.0 flatbuffers-1.12 gast-0.4.0 google-auth-2.23.2 google-auth-oauthlib-0.4.6 google-pasta-0.2.0 grpcio-1.34.1 h5py-3.1.0 idna-3.4 importlib-metadata-6.8.0 keras-nightly-2.5.0.dev2021032900 keras-preprocessing-1.1.2 markdown-3.5 numpy-1.19.5 oauthlib-3.2.2 opt-einsum-3.3.0 protobuf-3.20.3 pyasn1-0.5.0 pyasn1-modules-0.3.0 requests-2.31.0 requests-oauthlib-1.3.1 rsa-4.9 six-1.15.0 tensorboard-2.11.2 tensorboard-data-server-0.6.1 tensorboard-plugin-wit-1.8.1 tensorflow-estimator-2.5.0 tensorflow-gpu-2.5.0 termcolor-1.1.0 typing-extensions-3.7.4.3 urllib3-2.0.6 werkzeug-3.0.0 wrapt-1.12.1 zipp-3.17.0
(bi_lstm_ner) ye@lst-gpu-3090:~/exp/myNER/bi-LSTM$
```

Finally, installation OK!


