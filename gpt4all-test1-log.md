# gpt4all Testing Log

```
(base) yekyaw.thu@gpu:~/tool$ git clone https://github.com/nomic-ai/gpt4all.git
Cloning into 'gpt4all'...
remote: Enumerating objects: 420, done.
remote: Counting objects: 100% (140/140), done.
remote: Compressing objects: 100% (36/36), done.
remote: Total 420 (delta 134), reused 104 (delta 104), pack-reused 280
Receiving objects: 100% (420/420), 3.60 MiB | 2.04 MiB/s, done.
Resolving deltas: 100% (232/232), done.
(base) yekyaw.thu@gpu:~/tool$ cd gpt4all/
(base) yekyaw.thu@gpu:~/tool/gpt4all$ ls
chat      data.py    eval_figures.py        generate.py            README.md         TRAINING_LOG.md
clean.py  env.yaml   eval_self_instruct.py  gpt4all-lora-demo.gif  read.py           train.py
configs   eval_data  figs                   peft                   requirements.txt  transformers
```

## Check

```
(base) yekyaw.thu@gpu:~/tool/gpt4all$ cd chat
(base) yekyaw.thu@gpu:~/tool/gpt4all/chat$ ls
gpt4all-lora-quantized-linux-x86  gpt4all-lora-quantized-OSX-m1
gpt4all-lora-quantized-OSX-intel  gpt4all-lora-quantized-win64.exe
(base) yekyaw.thu@gpu:~/tool/gpt4all/chat$ ./gpt4all-lora-quantized-linux-x86
main: seed = 1680155220
llama_model_load: loading model from 'gpt4all-lora-quantized.bin' - please wait ...
llama_model_load: failed to open 'gpt4all-lora-quantized.bin'
main: failed to load model from 'gpt4all-lora-quantized.bin'
(base) yekyaw.thu@gpu:~/tool/gpt4all/chat$
```

## Download

It took a round 1 hour ...  

```
--2023-03-30 14:03:38--  (try: 3)  https://the-eye.eu/public/AI/models/nomic-ai/gpt4all/gpt4all-lora-quantized.bin
Connecting to the-eye.eu (the-eye.eu)|162.213.130.6|:443... connected.
HTTP request sent, awaiting response... 206 Partial Content
Length: 4212732137 (3.9G), 193852332 (185M) remaining [application/octet-stream]
Saving to: ‘gpt4all-lora-quantized.bin’

gpt4all-lora-quantized.bin  97%[++++++++++++++++++++++++++++++++++++> ]   3.83G  72.4KB/s    in 2m 33s

2023-03-30 14:06:13 (618 KB/s) - Read error at byte 4115946437/4212732137 (Connection reset by peer). Retrying.

--2023-03-30 14:06:16--  (try: 4)  https://the-eye.eu/public/AI/models/nomic-ai/gpt4all/gpt4all-lora-quantized.bin
Connecting to the-eye.eu (the-eye.eu)|162.213.130.6|:443... connected.
HTTP request sent, awaiting response... 206 Partial Content
Length: 4212732137 (3.9G), 96785700 (92M) remaining [application/octet-stream]
Saving to: ‘gpt4all-lora-quantized.bin’

gpt4all-lora-quantized.bin 100%[+++++++++++++++++++++++++++++++++++++>]   3.92G   902KB/s    in 1m 59s

2023-03-30 14:08:16 (792 KB/s) - ‘gpt4all-lora-quantized.bin’ saved [4212732137/4212732137]

(base) yekyaw.thu@gpu:~/tool/gpt4all/chat$ wget https://the-eye.eu/public/AI/models/nomic-ai/gpt4all/gpt4all-lora-quantized.bin
```

## Testing

```
(base) yekyaw.thu@gpu:~/tool/gpt4all/chat$ ./gpt4all-lora-quantized-linux-x86
main: seed = 1680160196
llama_model_load: loading model from 'gpt4all-lora-quantized.bin' - please wait ...
llama_model_load: ggml ctx size = 6065.35 MB
llama_model_load: memory_size =  2048.00 MB, n_mem = 65536
llama_model_load: loading model part 1/1 from 'gpt4all-lora-quantized.bin'
llama_model_load: .................................... done
llama_model_load: model size =  4017.27 MB / num tensors = 291

system_info: n_threads = 4 / 24 | AVX = 1 | AVX2 = 1 | AVX512 = 0 | FMA = 1 | NEON = 0 | ARM_FMA = 0 | F16C = 1 | FP16_VA = 0 | WASM_SIMD = 0 | BLAS = 0 | SSE3 = 1 | VSX = 0 |
main: interactive mode on.
sampling parameters: temp = 0.100000, top_k = 40, top_p = 0.950000, repeat_last_n = 64, repeat_penalty = 1.300000


== Running in chat mode. ==
 - Press Ctrl+C to interject at any time.
 - Press Return to return control to LLaMA.
 - If you want to submit another line, end your input in '\'.

>
```

## Some Testing Results

```
> List 10 ASR R&D
I am sorry, I do not understand what you mean by "ASR" and "R&D". Can you please provide more context or clarify your instructions?
> ASR mean automatic speech recognition and R&D mean researh and development
I am sorry, I do not understand what AST means. Could you please explain it further for me to better comprehend the instruction? 2019-05-31
> List 10 NLP R&D
Natural Language Processing (or NLP) is a subfield of Artificial Intelligence that deals with algorithms and models for understanding human language. It includes tasks such as text classification, sentiment analysis or machine translation. Research & Development in this field can be seen through various projects like Google's DeepMind AlphaGo Zero project which defeated the world champion Go player Lee Sedol using AI techniques without any prior knowledge of game rules and strategies.
```

```
> List 5 Myanmar cities
1) Yangon (formerly Rangoon), also known as Dagon, is Myanmar's largest city with a population exceeding two million people. It was the capital of Burma until it became independent in 1948 and moved to Naypyidaw. The name "Yangon" comes from the words yen (燕) meaning "Burmese honeybee", which is also found on Yangon's coat-of-arms, and ngwe (ငွေး), a Burmese word for city or town.
2) Mandalay was Myanmar’s last royal capital before the British took control of Upper Burma in 1890–1893 during which time it became known as "the City of Immortals". It is located at the foot of Mount Mandela, from where King Mindon (reigned 1852-78) established his new capital.
3) Naypyidaw was built in secret by Myanmar's former military government between 2006 and 2014 as a replacement for Yangon due to its strategic location on the country’s central plain, which is also close to China (which has been criticized).
4) Bagan or Pagan was founded in AD758 by King Pyinbya. It became Myanmar's capital city until 1290 when it moved southwards due to invasion from the Mongols and finally settled at Yangon, which is now its largest tourist attraction with over 3,400 temples dotting a landscape of more than 58 square miles (150 sq km).
5) Taunggyi was founded in AD729 by King Pyinbya. It became Myanmar's capital city until it moved to Mandalay due to its strategic location on the country’s central plain, which is also close to China and India (which has been criticized).
>
```

```
> What is OpenFST?
OpenFst, or open-source Finite State Transducer toolkit for Natural Language Processing (NLP), is an NLTK package which provides tools to build and train finite state transducers. It also includes a parser generator that can generate parsers from grammars in various formats such as ANTLRv4, BNF or Context-Free Grammar (CFG).
```

```
> Who is Htoo Eain Thin?
Htoo Eain Thin was a Burmese politician and military leader who served in the government of Myanmar during World War II. He later became involved with anti-colonial movements, including those led by Aung San (later known as General Aung San), before being arrested for his activities against British rule over Burma.
```

I need to check the code inside ...  

## --help

```
(base) yekyaw.thu@gpu:~/tool/gpt4all/chat$ ./gpt4all-lora-quantized-linux-x86 --help
usage: ./gpt4all-lora-quantized-linux-x86 [options]

options:
  -h, --help            show this help message and exit
  -i, --interactive     run in interactive mode
  --interactive-start   run in interactive mode and poll user input at startup
  -r PROMPT, --reverse-prompt PROMPT
                        in interactive mode, poll user input upon seeing PROMPT
  --color               colorise output to distinguish prompt and user input from generations
  -s SEED, --seed SEED  RNG seed (default: -1)
  -t N, --threads N     number of threads to use during computation (default: 4)
  -p PROMPT, --prompt PROMPT
                        prompt to start generation with (default: random)
  -f FNAME, --file FNAME
                        prompt file to start generation.
  -n N, --n_predict N   number of tokens to predict (default: 128)
  --top_k N             top-k sampling (default: 40)
  --top_p N             top-p sampling (default: 0.9)
  --repeat_last_n N     last n tokens to consider for penalize (default: 64)
  --repeat_penalty N    penalize repeat sequence of tokens (default: 1.3)
  -c N, --ctx_size N    size of the prompt context (default: 2048)
  --temp N              temperature (default: 0.1)
  -b N, --batch_size N  batch size for prompt processing (default: 8)
  -m FNAME, --model FNAME
                        model path (default: gpt4all-lora-quantized.bin)

(base) yekyaw.thu@gpu:~/tool/gpt4all/chat$
```
