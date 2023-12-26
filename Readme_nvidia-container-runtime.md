Aqui está o procedimento para instalar o driver NVIDIA e o Container Runtime no Ubuntu 22.04, formatado em Markdown:

---
### Instalação do Container Runtime

#### Observações

- Analise a necessidade do uso do Container Runtime e do driver NVIDIA.
- O NVIDIA Container Runtime é parte do NVIDIA Container Toolkit, permitindo que aplicativos em contêineres acessem a GPU do host.

#### Adicionando Repositório NVIDIA

```bash
distribution=$( . /etc/os-release; echo $ID$VERSION_ID )
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
```

#### Atualização e Instalação de Pacotes

```bash
sudo apt update
sudo apt install -y nvidia-docker2
```

#### Configuração do Docker

- Adicione as seguintes configurações ao arquivo `/etc/docker/daemon.json`:

  ```json
  {
    "runtimes": {
      "nvidia": {
        "path": "nvidia-container-runtime",
        "runtimeArgs": []
      }
    },
    "default-runtime": "nvidia"
  }
  ```

- Reinicie o Docker:

  ```bash
  sudo systemctl restart docker
  ```

## Baixar container para teste

 ```bash
sudo docker run --rm --runtime=nvidia --gpus all ubuntu nvidia-smi
 ```