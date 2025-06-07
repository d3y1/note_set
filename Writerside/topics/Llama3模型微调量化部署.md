# Llama3模型微调量化及部署应用

![11-Llama3模型微调量化部署.jpg](11-Llama3模型微调量化部署.jpg)

```shell
# 环境
➜  ~ conda create --name envllamafactory python=3.11
➜  ~ conda activate envllamafactory
(envllamafactory) ➜ ~ pip install torch transformers datasets
(envllamafactory) ➜ ~ pip install scikit-learn numpy pandas

# 微调
➜ ~ git clone https://github.com/hiyouga/LLaMA-Factory.git
➜ ~ cd LLaMA-Factory
➜ ~ LLaMA-Factory pip install -e ".[metrics,modelscope,qwen]"
➜ ~ LLaMA-Factory pip install torch torchvision torchaudio
➜ ~ LLaMA-Factory pip install bitsandbytes tensorboard
➜ ~ LLaMA-Factory GRADIO_SHARE=1 llamafactory-cli webui
https://3c4fc7cc3dfaa34357.gradio.live/

# 量化
➜ ~ git clone https://github.com/ggml-org/llama.cpp.git
➜ ~ cd llama.cpp
➜ llama.cpp git:(master) conda create --name envllamacpp python=3.11 -y
➜ llama.cpp git:(master) conda activate envllamacpp
(envllamacpp) ➜ llama.cpp git:(master) pip install -r requirements/requirements-convert_hf_to_gguf.txt
(envllamacpp) ➜ llama.cpp git:(master) cmake -B build
(envllamacpp) ➜ llama.cpp git:(master) cmake --build build --config Release
(envllamacpp) ➜ llama.cpp git:(master) python convert_hf_to_gguf.py /opt/model/2025-xx-xx-14-42-42 --outtype f16 - -outfile /opt/2025-xx-xx-14-42-42-llama3_2-zh.gguf
(envllamacpp) ➜ llama.cpp git:(master) ./build/bin/llama-quantize /opt/2025-xx-xx-14-42-42-llama3_2-zh.gguf /opt/model/2025-xx-xx-14-42-42-llama3_2-zh.gguf q4_0

# 部署
➜ deploy vi Modelfile
➜ deploy cat Modelfile
FROM /opt/model/2025-xx-xx-14-42-42-llama3_2-zh.gguf
➜ deploy ollama create llama3.2-chinese:8b -f Modelfile
➜ deploy ollama run llama3.2-chinese:8b

# 应用
WebUI run on Docker(自带RAG)
➜ deploy docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
http://localhost:3000/

AnythingLLM(可配置知识库)
```