# Instalação do docker na  EC2 (Ubuntu)

Nessa documentação, você encontrará todo passo a passo para instalar e configuração o docker na sua instância EC2, utilizando o **UBUNTU**

## 👉🏼 Passo a passo

### Atualizar ubuntu package

`sudo apt update && sudo apt upgrade -y`

### Adicionar repositório de pacotes do docker

`sudo apt install ca-certificates curl gnupg lsb-release`

### Adicionar chave de GPC do docker

`sudo mkdir -p /etc/apt/keyrings`

```jsx
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

### Adicionar repositório oficial

```jsx
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Atualizar novamente

`sudo apt update`

### Instalar docker CE

```jsx
sudo apt-get install docker-ce docker-ce-cli [containerd.io](http://containerd.io/) docker-buildx-plugin docker-compose-plugin
```

### Adicionar usuário ubuntu ao docker grupo

`sudo usermod -aG docker $USER`