# Docker Ollama

## Introduction

- Docker Ollama is a containerized environment for running large-scale language models like LLaMA and Gemma for various AI-powered tasks such as text generation, chatbots, and more.

## System Requirements

- This project requires a machine with at least 8GB of RAM. For optimal performance, a machine with GPU support is recommended.

## Environment Setup

- Ensure Docker is installed on your machine, and if you're using GPU support, make sure NVIDIA drivers and Docker GPU support are properly configured.

## Provisioning Docker Container

### Step 1: Pull the Docker Image

To pull the Ollama Docker image, run the following command:

``` 
docker pull ollama/ollama
```

### Step 2: Create the Docker Container

Create the Docker container with the following command. If your machine does not support GPUs, you may need to remove
the --gpus=all flag:

``` 
docker run -d --gpus=all -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
```

### Step 3: Run a Model Inside the Container

Important: The llama3 model is very large and requires significant resources to run. It is recommended to start with a
lighter model, such as gemma2:2b, to ensure smooth operation and avoid potential performance issues:

```
docker exec -it ollama ollama run gemma2:2b
```

Once you've confirmed the container is running smoothly, you can try heavier models if needed.

### Available Models

<table border="1">
  <thead>
    <tr>
      <th>Model</th>
      <th>Parameters</th>
      <th>Size</th>
      <th>Download</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Llama 3.1</td>
      <td>8B</td>
      <td>4.7GB</td>
      <td>ollama run llama3.1</td>
    </tr>
    <tr>
      <td>Llama 3.1</td>
      <td>70B</td>
      <td>40GB</td>
      <td>ollama run llama3.1:70b</td>
    </tr>
    <tr>
      <td>Llama 3.1</td>
      <td>405B</td>
      <td>231GB</td>
      <td>ollama run llama3.1:405b</td>
    </tr>
    <tr>
      <td>Phi 3 Mini</td>
      <td>3.8B</td>
      <td>2.3GB</td>
      <td>ollama run phi3</td>
    </tr>
    <tr>
      <td>Phi 3 Medium</td>
      <td>14B</td>
      <td>7.9GB</td>
      <td>ollama run phi3:medium</td>
    </tr>
    <tr>
      <td>Gemma 2</td>
      <td>2B</td>
      <td>1.6GB</td>
      <td>ollama run gemma2:2b</td>
    </tr>
    <tr>
      <td>Gemma 2</td>
      <td>9B</td>
      <td>5.5GB</td>
      <td>ollama run gemma2</td>
    </tr>
    <tr>
      <td>Gemma 2</td>
      <td>27B</td>
      <td>16GB</td>
      <td>ollama run gemma2:27b</td>
    </tr>
    <tr>
      <td>Mistral</td>
      <td>7B</td>
      <td>4.1GB</td>
      <td>ollama run mistral</td>
    </tr>
    <tr>
      <td>Moondream 2</td>
      <td>1.4B</td>
      <td>829MB</td>
      <td>ollama run moondream</td>
    </tr>
    <tr>
      <td>Neural Chat</td>
      <td>7B</td>
      <td>4.1GB</td>
      <td>ollama run neural-chat</td>
    </tr>
    <tr>
      <td>Starling</td>
      <td>7B</td>
      <td>4.1GB</td>
      <td>ollama run starling-lm</td>
    </tr>
    <tr>
      <td>Code Llama</td>
      <td>7B</td>
      <td>3.8GB</td>
      <td>ollama run codellama</td>
    </tr>
    <tr>
      <td>Llama 2 Uncensored</td>
      <td>7B</td>
      <td>3.8GB</td>
      <td>ollama run llama2-uncensored</td>
    </tr>
    <tr>
      <td>LLaVA</td>
      <td>7B</td>
      <td>4.5GB</td>
      <td>ollama run llava</td>
    </tr>
    <tr>
      <td>Solar</td>
      <td>10.7B</td>
      <td>6.1GB</td>
      <td>ollama run solar</td>
    </tr>
  </tbody>
</table>

## Consuming the Container's API for Chat

You can interact with the container using the API by sending POST requests. Use Insomnia collection (./insomnia) or the
following curl command
as an example:

```
curl --request POST \
  --url http://localhost:11434/api/chat \
  --header 'Content-Type: application/json' \
  --header 'User-Agent: insomnia/9.3.3' \
  --data '{
	"model": "gemma2:2b",
	"messages": [
    { "role": "user", "content": "Hello Ollama!" }
  ],
	"stream": false
}'
```

This will send a message to the model gemma2:2b and retrieve the generated content.