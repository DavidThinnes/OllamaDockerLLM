# OllamaDockerLLM
An easy way to run Ollama LLM () models inside a docker container.Open Web UI can be used to create a chat interface.

**start ollama**

==============================================

docker compose up -d



**select and run model (pull with cloudflare(vpn))**

================================================

docker exec -it ollama_docker-ollama-1 ollama run llama3.1:latest

docker exec -it ollama_docker-ollama-1 ollama run meditron

docker exec -it ollama_docker-ollama-1 ollama run meditron:70b   (that's the big one ~40Gb)



(or whichever model you want)



**show the logs**

==============================================

docker logs ollama



**stop and remove models**

=============================================

docker exec -it ollama_docker-ollama-1 ollama rm medllama2:latest





**stop and remove ollama**

==============================

docker stop ollama

docker rm ollama





**access from same network should be possible**

=============================================== 



(Invoke-WebRequest -method POST -Body '{"model":"meditron", "prompt":"What is an EEG?", "stream": false}' -uri http://localhost:11434/api/generate ).Content | ConvertFrom-json



(Invoke-WebRequest -method POST -Body '{"model":"llama3.1:latest", "prompt":"What is an EEG?", "stream": false}' -uri http://localhost:11434/api/generate ).Content | ConvertFrom-json



(Invoke-WebRequest -method POST -Body '{"model":"meditron:70b", "prompt":"What is an EEG?", "stream": false}' -uri http://localhost:11434/api/generate ).Content | ConvertFrom-json



change IP address to the one of your Server





**start open webui if needed**

============================================



if not, command webui and dependencies in the docker-compose yml file









**check nvidia gpu usage**

=============================================

nvidia-smi

nvidia-smi -l 1







**Use a modelfile**

===============================================

.copy the sha into .ollama/models/blobs

create modefile and copy it to the same path



Inside the container run:

docker exec -it ollama_docker-ollama-1 ollama create  MyModelname -f models/Modelfile



docker exec -it ollama_docker-ollama-1 ollama run MyModelname









**Stop and remove all docker containers**

==================================================

docker stop $(docker ps -a) && docker rm $(docker ps -aq)





