# OllamaDockerLLM
An easy way to run [Ollama LLM](https://ollama.ai) models inside a Docker container. Optionally, you can use **Open WebUI** to create a chat interface.

---

## 🚀 Start Ollama
```bash
docker compose up -d
```
---

## 🤖 Select and Run a Model
*(pulling may require Cloudflare VPN)*
```bash
docker exec -it ollama_docker-ollama-1 ollama run llama3.1:latest
docker exec -it ollama_docker-ollama-1 ollama run meditron
docker exec -it ollama_docker-ollama-1 ollama run meditron:70b   # ~40GB model
```
Or whichever model you want.




## 📜 Show Logs
```bash
docker logs ollama
```



## 🗑 Stop and Remove a Model
```bash
docker exec -it ollama_docker-ollama-1 ollama rm medllama2:latest
```


## 🛑 Stop and Remove Ollama
```bash
docker stop ollama
docker rm ollama
```



## 🌐 Access via Network
Change `localhost` to your server’s IP if accessing remotely.
```bash
(Invoke-WebRequest -Method POST -Body '{"model":"meditron", "prompt":"What is an EEG?", "stream": false}' -Uri http://localhost:11434/api/generate).Content | ConvertFrom-Json
(Invoke-WebRequest -Method POST -Body '{"model":"llama3.1:latest", "prompt":"What is an EEG?", "stream": false}' -Uri http://localhost:11434/api/generate).Content | ConvertFrom-Json
(Invoke-WebRequest -Method POST -Body '{"model":"meditron:70b", "prompt":"What is an EEG?", "stream": false}' -Uri http://localhost:11434/api/generate).Content | ConvertFrom-Json
```


## 💻 Start Open WebUI
If you don't want the web interface, comment `open-webui` and its dependencies to your `compose.yml` file and run



## 📊 Check NVIDIA GPU Usage
```bash
nvidia-smi
nvidia-smi -l 1
```



## 📝 Use a Modelfile
1. Copy the model SHA into `.ollama/models/blobs`  
2. Create your `Modelfile` and place it in the same path  
3. Inside the container, run:
```bash
docker exec -it ollama_docker-ollama-1 ollama create MyModelname -f models/Modelfile
docker exec -it ollama_docker-ollama-1 ollama run MyModelname
```


## 🧹 Stop and Remove **All** Docker Containers
```bash
docker stop $(docker ps -q) || true && docker rm $(docker ps -aq) || true
```