# Testing Command-line ChatGPT Note

## Add API-key in Your Environment

```
(base) ye@lst-gpu-3090:~$ env | grep OPENAI
OPENAI_API_KEY=skxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

## Installation

```
(base) ye@lst-gpu-3090:~$ pip3 install shell-gpt
Collecting shell-gpt
  Downloading shell_gpt-0.9.4-py3-none-any.whl (23 kB)
Collecting requests<3.0.0,>=2.28.2
  Using cached requests-2.31.0-py3-none-any.whl (62 kB)
Requirement already satisfied: click<9.0.0,>=7.1.1 in ./anaconda3/lib/python3.9/site-packages (from shell-gpt) (8.0.4)
Collecting typer<1.0.0,>=0.7.0
  Using cached typer-0.9.0-py3-none-any.whl (45 kB)
Collecting distro<2.0.0,>=1.8.0
  Downloading distro-1.8.0-py3-none-any.whl (20 kB)
Collecting rich<14.0.0,>=13.1.0
  Downloading rich-13.5.3-py3-none-any.whl (239 kB)
     |████████████████████████████████| 239 kB 2.2 MB/s 
Requirement already satisfied: certifi>=2017.4.17 in ./anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.28.2->shell-gpt) (2021.10.8)
Requirement already satisfied: charset-normalizer<4,>=2 in ./anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.28.2->shell-gpt) (2.0.4)
Requirement already satisfied: urllib3<3,>=1.21.1 in ./anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.28.2->shell-gpt) (1.26.9)
Requirement already satisfied: idna<4,>=2.5 in ./anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.28.2->shell-gpt) (3.3)
Collecting markdown-it-py>=2.2.0
  Downloading markdown_it_py-3.0.0-py3-none-any.whl (87 kB)
     |████████████████████████████████| 87 kB 1.3 MB/s 
Collecting pygments<3.0.0,>=2.13.0
  Downloading Pygments-2.16.1-py3-none-any.whl (1.2 MB)
     |████████████████████████████████| 1.2 MB 20.9 MB/s 
Collecting mdurl~=0.1
  Downloading mdurl-0.1.2-py3-none-any.whl (10.0 kB)
Requirement already satisfied: typing-extensions>=3.7.4.3 in ./anaconda3/lib/python3.9/site-packages (from typer<1.0.0,>=0.7.0->shell-gpt) (4.1.1)
Installing collected packages: mdurl, pygments, markdown-it-py, typer, rich, requests, distro, shell-gpt
  Attempting uninstall: pygments
    Found existing installation: Pygments 2.11.2
    Uninstalling Pygments-2.11.2:
      Successfully uninstalled Pygments-2.11.2
  Attempting uninstall: requests
    Found existing installation: requests 2.27.1
    Uninstalling requests-2.27.1:
      Successfully uninstalled requests-2.27.1
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
spyder 5.1.5 requires pyqt5<5.13, which is not installed.
spyder 5.1.5 requires pyqtwebengine<5.13, which is not installed.
conda-repo-cli 1.0.4 requires pathlib, which is not installed.
anaconda-project 0.10.2 requires ruamel-yaml, which is not installed.
Successfully installed distro-1.8.0 markdown-it-py-3.0.0 mdurl-0.1.2 pygments-2.16.1 requests-2.31.0 rich-13.5.3 shell-gpt-0.9.4 typer-0.9.0
(base) ye@lst-gpu-3090:~$
```

## Help of sgpt

```
(base) ye@lst-gpu-3090:~$ sgpt --help
                                                                                                                              
 Usage: sgpt [OPTIONS] [PROMPT]                                                                                               
                                                                                                                              
╭─ Arguments ────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│   prompt      [PROMPT]  The prompt to generate completions for.                                                            │
╰────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
╭─ Options ──────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ --model                             TEXT                       Large language model to use. [default: gpt-3.5-turbo]       │
│ --temperature                       FLOAT RANGE [0.0<=x<=2.0]  Randomness of generated output. [default: 0.1]              │
│ --top-probability                   FLOAT RANGE [0.1<=x<=1.0]  Limits highest probable tokens (words). [default: 1.0]      │
│ --editor             --no-editor                               Open $EDITOR to provide a prompt. [default: no-editor]      │
│ --cache              --no-cache                                Cache completion results. [default: cache]                  │
│ --help                                                         Show this message and exit.                                 │
╰────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
╭─ Assistance Options ───────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ --shell           -s                 Generate and execute shell commands.                                                  │
│ --describe-shell  -d                 Describe a shell command.                                                             │
│ --code                --no-code      Generate only code. [default: no-code]                                                │
╰────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
╭─ Chat Options ─────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ --chat                             TEXT  Follow conversation with id, use "temp" for quick session. [default: None]        │
│ --repl                             TEXT  Start a REPL (Read–eval–print loop) session. [default: None]                      │
│ --show-chat                        TEXT  Show all messages from provided chat id. [default: None]                          │
│ --list-chats    --no-list-chats          List all existing chat ids. [default: no-list-chats]                              │
╰────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
╭─ Role Options ─────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ --role                              TEXT  System role for GPT model. [default: None]                                       │
│ --create-role                       TEXT  Create role. [default: None]                                                     │
│ --show-role                         TEXT  Show role. [default: None]                                                       │
│ --list-roles     --no-list-roles          List roles. [default: no-list-roles]                                             │
╰────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯

(base) ye@lst-gpu-3090:~$ 
```

## Testing Commandline ChatGPT

```
(base) ye@lst-gpu-3090:~$ sgpt "Area of the country Myanmar?"
╭─────────────────────────────── Traceback (most recent call last) ────────────────────────────────╮
│ /home/ye/anaconda3/lib/python3.9/site-packages/sgpt/app.py:167 in main                           │
│                                                                                                  │
│   164 │   │   │   caching=cache,                                                                 │
│   165 │   │   )                                                                                  │
│   166 │   else:                                                                                  │
│ ❱ 167 │   │   full_completion = DefaultHandler(role_class).handle(                               │
│   168 │   │   │   prompt,                                                                        │
│   169 │   │   │   model=model,                                                                   │
│   170 │   │   │   temperature=temperature,                                                       │
│                                                                                                  │
│ ╭─────────────────────────────── locals ────────────────────────────────╮                        │
│ │               cache = True                                            │                        │
│ │                chat = None                                            │                        │
│ │                code = False                                           │                        │
│ │         create_role = None                                            │                        │
│ │      describe_shell = False                                           │                        │
│ │              editor = False                                           │                        │
│ │ install_integration = None                                            │                        │
│ │          list_chats = None                                            │                        │
│ │          list_roles = None                                            │                        │
│ │               model = 'gpt-3.5-turbo'                                 │                        │
│ │              prompt = 'Area of the country Myanmar?'                  │                        │
│ │                repl = None                                            │                        │
│ │                role = None                                            │                        │
│ │          role_class = <sgpt.role.SystemRole object at 0x7f3aafde5b50> │                        │
│ │               shell = False                                           │                        │
│ │           show_chat = None                                            │                        │
│ │           show_role = None                                            │                        │
│ │        stdin_passed = False                                           │                        │
│ │         temperature = 0.1                                             │                        │
│ │     top_probability = 1.0                                             │                        │
│ ╰───────────────────────────────────────────────────────────────────────╯                        │
│                                                                                                  │
│ /home/ye/anaconda3/lib/python3.9/site-packages/sgpt/handlers/handler.py:33 in handle             │
│                                                                                                  │
│   30 │   │   stream = cfg.get("DISABLE_STREAMING") == "false"                                    │
│   31 │   │   if not stream:                                                                      │
│   32 │   │   │   typer.echo("Loading...\r", nl=False)                                            │
│ ❱ 33 │   │   for word in self.get_completion(messages=messages, **kwargs):                       │
│   34 │   │   │   typer.secho(word, fg=self.color, bold=True, nl=False)                           │
│   35 │   │   │   full_completion += word                                                         │
│   36 │   │   typer.echo("\033[K" if not stream else "")  # Overwrite "loading..."                │
│                                                                                                  │
│ ╭─────────────────────────────────────────── locals ───────────────────────────────────────────╮ │
│ │ full_completion = ''                                                                         │ │
│ │          kwargs = {                                                                          │ │
│ │                   │   'model': 'gpt-3.5-turbo',                                              │ │
│ │                   │   'temperature': 0.1,                                                    │ │
│ │                   │   'top_probability': 1.0,                                                │ │
│ │                   │   'caching': True                                                        │ │
│ │                   }                                                                          │ │
│ │        messages = [                                                                          │ │
│ │                   │   {                                                                      │ │
│ │                   │   │   'role': 'user',                                                    │ │
│ │                   │   │   'content': '###\nRole name: default\nYou are Command Line App      │ │
│ │                   ShellGPT, a programming and syst'+346                                      │ │
│ │                   │   }                                                                      │ │
│ │                   ]                                                                          │ │
│ │          prompt = 'Area of the country Myanmar?'                                             │ │
│ │            self = <sgpt.handlers.default_handler.DefaultHandler object at 0x7f3aafde5700>    │ │
│ │          stream = True                                                                       │ │
│ ╰──────────────────────────────────────────────────────────────────────────────────────────────╯ │
│                                                                                                  │
│ /home/ye/anaconda3/lib/python3.9/site-packages/sgpt/handlers/handler.py:25 in get_completion     │
│                                                                                                  │
│   22 │   │   raise NotImplementedError                                                           │
│   23 │                                                                                           │
│   24 │   def get_completion(self, **kwargs: Any) -> Generator[str, None, None]:                  │
│ ❱ 25 │   │   yield from self.client.get_completion(**kwargs)                                     │
│   26 │                                                                                           │
│   27 │   def handle(self, prompt: str, **kwargs: Any) -> str:                                    │
│   28 │   │   messages = self.make_messages(self.make_prompt(prompt))                             │
│                                                                                                  │
│ ╭─────────────────────────────────────────── locals ───────────────────────────────────────────╮ │
│ │ kwargs = {                                                                                   │ │
│ │          │   'messages': [                                                                   │ │
│ │          │   │   {                                                                           │ │
│ │          │   │   │   'role': 'user',                                                         │ │
│ │          │   │   │   'content': '###\nRole name: default\nYou are Command Line App ShellGPT, │ │
│ │          a programming and syst'+346                                                         │ │
│ │          │   │   }                                                                           │ │
│ │          │   ],                                                                              │ │
│ │          │   'model': 'gpt-3.5-turbo',                                                       │ │
│ │          │   'temperature': 0.1,                                                             │ │
│ │          │   'top_probability': 1.0,                                                         │ │
│ │          │   'caching': True                                                                 │ │
│ │          }                                                                                   │ │
│ │   self = <sgpt.handlers.default_handler.DefaultHandler object at 0x7f3aafde5700>             │ │
│ ╰──────────────────────────────────────────────────────────────────────────────────────────────╯ │
│                                                                                                  │
│ /home/ye/anaconda3/lib/python3.9/site-packages/sgpt/client.py:98 in get_completion               │
│                                                                                                  │
│    95 │   │   :param caching: Boolean value to enable/disable caching.                           │
│    96 │   │   :return: String generated completion.                                              │
│    97 │   │   """                                                                                │
│ ❱  98 │   │   yield from self._request(                                                          │
│    99 │   │   │   messages,                                                                      │
│   100 │   │   │   model,                                                                         │
│   101 │   │   │   temperature,                                                                   │
│                                                                                                  │
│ ╭─────────────────────────────────────────── locals ───────────────────────────────────────────╮ │
│ │         caching = True                                                                       │ │
│ │        messages = [                                                                          │ │
│ │                   │   {                                                                      │ │
│ │                   │   │   'role': 'user',                                                    │ │
│ │                   │   │   'content': '###\nRole name: default\nYou are Command Line App      │ │
│ │                   ShellGPT, a programming and syst'+346                                      │ │
│ │                   │   }                                                                      │ │
│ │                   ]                                                                          │ │
│ │           model = 'gpt-3.5-turbo'                                                            │ │
│ │            self = <sgpt.client.OpenAIClient object at 0x7f3aae234400>                        │ │
│ │     temperature = 0.1                                                                        │ │
│ │ top_probability = 1.0                                                                        │ │
│ ╰──────────────────────────────────────────────────────────────────────────────────────────────╯ │
│                                                                                                  │
│ /home/ye/anaconda3/lib/python3.9/site-packages/sgpt/cache.py:39 in wrapper                       │
│                                                                                                  │
│   36 │   │   │   │   yield cache_file.read_text()                                                │
│   37 │   │   │   │   return                                                                      │
│   38 │   │   │   result = ""                                                                     │
│ ❱ 39 │   │   │   for i in func(*args, **kwargs):                                                 │
│   40 │   │   │   │   result += i                                                                 │
│   41 │   │   │   │   yield i                                                                     │
│   42 │   │   │   cache_file.write_text(result)                                                   │
│                                                                                                  │
│ ╭─────────────────────────────────────────── locals ───────────────────────────────────────────╮ │
│ │       args = (                                                                               │ │
│ │              │   <sgpt.client.OpenAIClient object at 0x7f3aae234400>,                        │ │
│ │              │   [                                                                           │ │
│ │              │   │   {                                                                       │ │
│ │              │   │   │   'role': 'user',                                                     │ │
│ │              │   │   │   'content': '###\nRole name: default\nYou are Command Line App       │ │
│ │              ShellGPT, a programming and syst'+346                                           │ │
│ │              │   │   }                                                                       │ │
│ │              │   ],                                                                          │ │
│ │              │   'gpt-3.5-turbo',                                                            │ │
│ │              │   0.1,                                                                        │ │
│ │              │   1.0                                                                         │ │
│ │              )                                                                               │ │
│ │ cache_file = PosixPath('/tmp/cache/ab8f266178fa07496efc25591b57f981')                        │ │
│ │  cache_key = 'ab8f266178fa07496efc25591b57f981'                                              │ │
│ │       func = <function OpenAIClient._request at 0x7f3aae1c3700>                              │ │
│ │     kwargs = {}                                                                              │ │
│ │     result = ''                                                                              │ │
│ │       self = <sgpt.cache.Cache object at 0x7f3aaed07b50>                                     │ │
│ ╰──────────────────────────────────────────────────────────────────────────────────────────────╯ │
│                                                                                                  │
│ /home/ye/anaconda3/lib/python3.9/site-packages/sgpt/client.py:61 in _request                     │
│                                                                                                  │
│    58 │   │   │   timeout=REQUEST_TIMEOUT,                                                       │
│    59 │   │   │   stream=stream,                                                                 │
│    60 │   │   )                                                                                  │
│ ❱  61 │   │   response.raise_for_status()                                                        │
│    62 │   │   # TODO: Optimise.                                                                  │
│    63 │   │   # https://github.com/openai/openai-python/blob/237448dc072a2c062698da3f9f512fae3   │
│    64 │   │   if not stream:                                                                     │
│                                                                                                  │
│ ╭─────────────────────────────────────────── locals ───────────────────────────────────────────╮ │
│ │            data = {                                                                          │ │
│ │                   │   'messages': [                                                          │ │
│ │                   │   │   {                                                                  │ │
│ │                   │   │   │   'role': 'user',                                                │ │
│ │                   │   │   │   'content': '###\nRole name: default\nYou are Command Line App  │ │
│ │                   ShellGPT, a programming and syst'+346                                      │ │
│ │                   │   │   }                                                                  │ │
│ │                   │   ],                                                                     │ │
│ │                   │   'model': 'gpt-3.5-turbo',                                              │ │
│ │                   │   'temperature': 0.1,                                                    │ │
│ │                   │   'top_p': 1.0,                                                          │ │
│ │                   │   'stream': True                                                         │ │
│ │                   }                                                                          │ │
│ │        endpoint = 'https://api.openai.com/v1/chat/completions'                               │ │
│ │        messages = [                                                                          │ │
│ │                   │   {                                                                      │ │
│ │                   │   │   'role': 'user',                                                    │ │
│ │                   │   │   'content': '###\nRole name: default\nYou are Command Line App      │ │
│ │                   ShellGPT, a programming and syst'+346                                      │ │
│ │                   │   }                                                                      │ │
│ │                   ]                                                                          │ │
│ │           model = 'gpt-3.5-turbo'                                                            │ │
│ │        response = <Response [429]>                                                           │ │
│ │            self = <sgpt.client.OpenAIClient object at 0x7f3aae234400>                        │ │
│ │          stream = True                                                                       │ │
│ │     temperature = 0.1                                                                        │ │
│ │ top_probability = 1.0                                                                        │ │
│ ╰──────────────────────────────────────────────────────────────────────────────────────────────╯ │
│                                                                                                  │
│ /home/ye/anaconda3/lib/python3.9/site-packages/requests/models.py:1021 in raise_for_status       │
│                                                                                                  │
│   1018 │   │   │   )                                                                             │
│   1019 │   │                                                                                     │
│   1020 │   │   if http_error_msg:                                                                │
│ ❱ 1021 │   │   │   raise HTTPError(http_error_msg, response=self)                                │
│   1022 │                                                                                         │
│   1023 │   def close(self):                                                                      │
│   1024 │   │   """Releases the connection back to the pool. Once this method has been            │
│                                                                                                  │
│ ╭─────────────────────────────────────────── locals ───────────────────────────────────────────╮ │
│ │ http_error_msg = '429 Client Error: Too Many Requests for url:                               │ │
│ │                  https://api.openai.com/v1/chat/comp'+7                                      │ │
│ │         reason = 'Too Many Requests'                                                         │ │
│ │           self = <Response [429]>                                                            │ │
│ ╰──────────────────────────────────────────────────────────────────────────────────────────────╯ │
╰──────────────────────────────────────────────────────────────────────────────────────────────────╯
HTTPError: 429 Client Error: Too Many Requests for url: https://api.openai.com/v1/chat/completions
(base) ye@lst-gpu-3090:~$
```

## Reinstall with --user Option

```
(base) ye@lst-gpu-3090:~$ pip3 install shell-gpt --user
Requirement already satisfied: shell-gpt in ./anaconda3/lib/python3.9/site-packages (0.9.4)
Requirement already satisfied: rich<14.0.0,>=13.1.0 in ./anaconda3/lib/python3.9/site-packages (from shell-gpt) (13.5.3)
Requirement already satisfied: distro<2.0.0,>=1.8.0 in ./anaconda3/lib/python3.9/site-packages (from shell-gpt) (1.8.0)
Requirement already satisfied: click<9.0.0,>=7.1.1 in ./anaconda3/lib/python3.9/site-packages (from shell-gpt) (8.0.4)
Requirement already satisfied: requests<3.0.0,>=2.28.2 in ./anaconda3/lib/python3.9/site-packages (from shell-gpt) (2.31.0)
Requirement already satisfied: typer<1.0.0,>=0.7.0 in ./anaconda3/lib/python3.9/site-packages (from shell-gpt) (0.9.0)
Requirement already satisfied: certifi>=2017.4.17 in ./anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.28.2->shell-gpt) (2021.10.8)
Requirement already satisfied: idna<4,>=2.5 in ./anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.28.2->shell-gpt) (3.3)
Requirement already satisfied: charset-normalizer<4,>=2 in ./anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.28.2->shell-gpt) (2.0.4)
Requirement already satisfied: urllib3<3,>=1.21.1 in ./anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.28.2->shell-gpt) (1.26.9)
Requirement already satisfied: markdown-it-py>=2.2.0 in ./anaconda3/lib/python3.9/site-packages (from rich<14.0.0,>=13.1.0->shell-gpt) (3.0.0)
Requirement already satisfied: pygments<3.0.0,>=2.13.0 in ./anaconda3/lib/python3.9/site-packages (from rich<14.0.0,>=13.1.0->shell-gpt) (2.16.1)
Requirement already satisfied: mdurl~=0.1 in ./anaconda3/lib/python3.9/site-packages (from markdown-it-py>=2.2.0->rich<14.0.0,>=13.1.0->shell-gpt) (0.1.2)
Requirement already satisfied: typing-extensions>=3.7.4.3 in ./anaconda3/lib/python3.9/site-packages (from typer<1.0.0,>=0.7.0->shell-gpt) (4.1.1)
(base) ye@lst-gpu-3090:~$ 
```

## Testing CommandLine ChatGPT Again

I got the same ERROR!  

```
(base) ye@lst-gpu-3090:~$ sgpt --chat test "Let me know the area of the country Myanmar?"
```

```
(base) ye@lst-gpu-3090:~$ sgpt --repl test --no-cache
Entering REPL mode, press Ctrl+C to exit.
>>> I wanna know area of the country Myanmar.
╭─────────────────────────────── Traceback (most recent call last) ────────────────────────────────╮
│ /home/ye/anaconda3/lib/python3.9/site-packages/sgpt/app.py:148 in main                           │
│                                                                                                  │
│   145 │                                                                                          │
│   146 │   if repl:                                                                               │
│   147 │   │   # Will be in infinite loop here until user exits with Ctrl+C.                      │
│ ❱ 148 │   │   ReplHandler(repl, role_class).handle(                                              │
│   149 │   │   │   prompt,                                                                        │
│   150 │   │   │   model=model,                                                                   │
│   151 │   │   │   temperature=temperature,                                                       │
│                                                                                                  │
│ ╭─────────────────────────────── locals ────────────────────────────────╮                        │
│ │               cache = False                                           │                        │
│ │                chat = None                                            │                        │
│ │                code = False                                           │                        │
│ │         create_role = None                                            │                        │
│ │      describe_shell = False                                           │                        │
│ │              editor = False                                           │                        │
│ │ install_integration = None                                            │                        │
│ │          list_chats = None                                            │                        │
│ │          list_roles = None                                            │                        │
│ │               model = 'gpt-3.5-turbo'                                 │                        │
│ │              prompt = None                                            │                        │
│ │                repl = 'test'                                          │                        │
│ │                role = None                                            │                        │
│ │          role_class = <sgpt.role.SystemRole object at 0x7f619ddab040> │                        │
│ │               shell = False                                           │                        │
│ │           show_chat = None                                            │                        │
│ │           show_role = None                                            │                        │
│ │        stdin_passed = False                                           │                        │
│ │         temperature = 0.1                                             │                        │
│ │     top_probability = 1.0                                             │                        │
│ ╰───────────────────────────────────────────────────────────────────────╯                        │
│                                                                                                  │
│ /home/ye/anaconda3/lib/python3.9/site-packages/sgpt/handlers/repl_handler.py:54 in handle        │
│                                                                                                  │
│   51 │   │   │   │   │   caching=kwargs.get("caching"),                                          │
│   52 │   │   │   │   )                                                                           │
│   53 │   │   │   else:                                                                           │
│ ❱ 54 │   │   │   │   full_completion = super().handle(prompt, **kwargs)                          │
│   55                                                                                             │
│                                                                                                  │
...
...
...
│ ❱ 1021 │   │   │   raise HTTPError(http_error_msg, response=self)                                │
│   1022 │                                                                                         │
│   1023 │   def close(self):                                                                      │
│   1024 │   │   """Releases the connection back to the pool. Once this method has been            │
│                                                                                                  │
│ ╭─────────────────────────────────────────── locals ───────────────────────────────────────────╮ │
│ │ http_error_msg = '429 Client Error: Too Many Requests for url:                               │ │
│ │                  https://api.openai.com/v1/chat/comp'+7                                      │ │
│ │         reason = 'Too Many Requests'                                                         │ │
│ │           self = <Response [429]>                                                            │ │
│ ╰──────────────────────────────────────────────────────────────────────────────────────────────╯ │
╰──────────────────────────────────────────────────────────────────────────────────────────────────╯
HTTPError: 429 Client Error: Too Many Requests for url: https://api.openai.com/v1/chat/completions
(base) ye@lst-gpu-3090:~$ 
```

## Checking the Configuration File


I updated the default DEFAULT_MODEL=gpt-4 and I also added the OPENAI_API_KEY as follows:  

```
(base) ye@lst-gpu-3090:~$ cat ~/.config/shell_gpt/.sgptrc
CHAT_CACHE_PATH=/tmp/chat_cache
CACHE_PATH=/tmp/cache
CHAT_CACHE_LENGTH=100
CACHE_LENGTH=100
REQUEST_TIMEOUT=60
#DEFAULT_MODEL=gpt-3.5-turbo
DEFAULT_MODEL=gpt-4
OPENAI_API_HOST=https://api.openai.com
DEFAULT_COLOR=magenta
ROLE_STORAGE_PATH=/home/ye/.config/shell_gpt/roles
SYSTEM_ROLES=false
DEFAULT_EXECUTE_SHELL_CMD=false
DISABLE_STREAMING=false
OPENAI_API_KEY=sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

## Test Again

Still got the same ERROR:  

```
HTTPError: 429 Client Error: Too Many Requests for url: https://api.openai.com/v1/chat/completions
```

## Check the issues of Shell-GPT

The reason may be that paid account not containing API fees:  

Reference Link: https://github.com/TheR1D/shell_gpt/issues/301  

```
 excellentsport commented Aug 14, 2023 •

I was getting similar errors. Turns out my free credit had expired. I started a paid plan for the API and it works fine now.

I did find learn that access to the API is not included in the ChatGPTplus subscription. You have to set up paid API access separately. Per their pricing page for the API: "Is the ChatGPT API included in the ChatGPT Plus subscription? No, the ChatGPT API and ChatGPT Plus subscription are billed separately. The API has its own pricing, which can be found at https://openai.com/pricing. The ChatGPT Plus subscription covers usage on chat.openai.com only and costs $20/month."
```

## Reference

1. https://github.com/TheR1D/shell_gpt
2. https://medium.com/@abraaorl/using-chatgpt-in-the-terminal-f992815d7ab0  
3. https://beebom.com/how-use-chatgpt-linux-terminal/

