README.md

Ollama uses a Modelfile, similar to a Dockerfile or good old Make. 

I use Ollama workflow, I have NVIDIA Docker running CUDA GPU enabled containers on my Ubuntu 24 Dell XPS for experiments, research and development. 

There was no Sky-T1-Flash model on Ollama so I begged, borrowed and stole prior art (is it stealing if its open source? perhaps not).

Sourcing Sky-T1 model from Huggingface via a Github support question from the project lead at UC Berkeley https://github.com/ollama/ollama/issues/8768

cross checked the Modelfile from the Huggingface source. 

```ollama show --modelfile hf.co/bartowski/Sky-T1-32B-Flash-G```

I wanted to customize the model, and I have heard good things about Cline regarding creating files and working with VS Code. 

So I viewed the Modelfile for Sky-T1-Preview-Cline, thank you rashakol, I couldn't find you online, but Thanks! 

```ollama show --modelfile rashakol/sky-t1-32B-preview-cline:latest```

I manually merged the two Modelfiles, using this ```hf.co/bartowski/Sky-T1-32B-Flash-G``` core Ollama sections and just copied the entire preloaded prompt from ```rashakol```

Then I created the Ollama release of my shim for the model in my personal namespace.

```ollama create niccolox/sky-t1-flash-cline -f Modelfile
gathering model components 
using existing layer sha256:ab0cd5e7898d841131b3f2ea2197ab8b7bbfb0b4f2846d32798fd725c63d845f 
using existing layer sha256:e94a8ecb9327ded799604a2e478659bc759230fe316c50d686358f932f52776c 
using existing layer sha256:2f2dc07cdac061ce795891f782213df34c0fdf85962f11602429f4ba317bfa12 
using existing layer sha256:359e3a98a89b1ff6ca8b2b32f16b61f522db8e51afc214a701def5d4fec52111 
writing manifest 
success 
```


Show model

```
ollama show niccolox/sky-t1-flash-cline
  Model
    architecture        qwen2     
    parameters          32.8B     
    context length      32768     
    embedding length    5120      
    quantization        Q4_K_M    

  Parameters
    num_ctx        40000    
    temperature    0.3      

  System
    You are an advanced AI coding assistant, specifically designed to help with complex programming         
      tasks, tool use, code analysis, and software architecture design. Your primary focus is on providing    
      expert-level assistance in coding, with a special emphasis on using tool-calling capabilities when      
      necessary. Here are your key characteristics and instructions:                                          
    1. Coding Expertise:                                                                                    

```


then push to ollama

```
 ollama push niccolox/sky-t1-flash-cline
retrieving manifest 
pushing ab0cd5e7898d... 100% ▕███████████████████████████████████████████████████████████████████████████████████▏  19 GB                         
pushing e94a8ecb9327... 100% ▕███████████████████████████████████████████████████████████████████████████████████▏ 1.6 KB                         
pushing 2f2dc07cdac0... 100% ▕███████████████████████████████████████████████████████████████████████████████████▏ 2.9 KB                         
pushing 359e3a98a89b... 100% ▕███████████████████████████████████████████████████████████████████████████████████▏   36 B                         
pushing dbc14ce28634... 100% ▕███████████████████████████████████████████████████████████████████████████████████▏  488 B                         
pushing manifest 
success 

You can find your model at:

	https://ollama.com/niccolox/sky-t1-flash-cline


```



Docs
https://github.com/ollama/ollama/blob/main/README.md
https://github.com/ollama/ollama/blob/main/docs/modelfile.md


Inspiration

https://otmaneboughaba.com/posts/local-llm-ollama-huggingface/
