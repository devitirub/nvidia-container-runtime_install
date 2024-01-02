# instalação do drive nvia T4
Para outras placas deve ser similar
Para instalar o driver NVIDIA no Ubuntu, com pacote `.deb` do driver, como no caso do `nvidia-driver-local-repo-ubuntu2204-525.147.05_1.0-1_amd64.deb`, você pode seguir os seguintes passos

## Link para downliad

```bash
https://www.nvidia.com/Download/Find.aspx?lang=en-us
```
### 1. Preparação do Sistema


Antes de instalar o novo driver, é uma boa prática atualizar a lista de pacotes e o próprio sistema para garantir que todas as dependências estejam atualizadas:

```bash
sudo apt update
sudo apt upgrade
```

### 2. Desabilitando Nouveau (Driver Open Source)

O Nouveau é o driver open source para GPUs NVIDIA que vem pré-instalado em muitas distribuições Linux. Pode ser necessário desativá-lo antes de instalar o driver proprietário da NVIDIA.

Para desabilitar o Nouveau, crie ou edite o arquivo de configuração do modprobe:

```bash
sudo bash -c "echo blacklist nouveau > /etc/modprobe.d/blacklist-nvidia-nouveau.conf"
sudo bash -c "echo options nouveau modeset=0 >> /etc/modprobe.d/blacklist-nvidia-nouveau.conf"
```

Após isso, gere um novo initramfs:

```bash
sudo update-initramfs -u
```

Reinicie o computador para que as mudanças entrem em vigor.

### 3. Instalando o Driver

Agora, você vai instalar o driver que possui em formato `.deb`. Navegue até o diretório onde o arquivo `.deb` está localizado e execute:

```bash
cd /caminho/para/o/diretório
sudo dpkg -i nvidia-driver-local-repo-ubuntu2204-525.147.05_1.0-1_amd64.deb
```

Este comando irá instalar o repositório local do driver NVIDIA.

### 4. Atualizando a Lista de Pacotes e Instalando o Driver

Após adicionar o repositório, atualize a lista de pacotes:

```bash
sudo apt update
```

E então instale o driver propriamente dito:

```bash
sudo apt install nvidia-driver-525
```

### 5. Verificando a Instalação

Após a instalação, você pode verificar se o driver foi instalado corretamente com:

```bash
nvidia-smi
```

Este comando deve mostrar informações sobre a GPU e o driver instalado.

### 6. Reiniciar o Computador

Por fim, reinicie o computador para garantir que todas as mudanças entrem em vigor e o driver seja carregado corretamente.

```bash
sudo reboot
```
