# Harbor on Labs

## Pre-requisitos

- docker 17.10 ou superior
- docker-compose instalado
- openssl


## 1. Configurações iniciais



Faça o Download do Harbor:

```
$ wget https://github.com/goharbor/harbor/releases/download/v2.6.0/harbor-online-installer-v2.6.0.tgz

```

Descompacte o arquivo:

```
$ tar xzvf harbor-online-installer-v2.6.0.tgz
```

Gere os certificados:

```
$ openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout registry.4labs.example.key -out registry.4labs.example.crt -subj "/CN=registry/O=4Labs/OU=DevOps" -addext "subjectAltName = DNS:registry.4labs.example"

```

Gere um PEM do certificado:

```
$ openssl x509 -inform PEM -in registry.4labs.example.crt -out registry.4labs.example.cert
```

Crie o diretório que vai armezenar o certificado

```
$ sudo mkdir -p /data/certs

```

Realize a cópia dos arquivos gerados:

```
$ sudo cp registry.4labs.example.* /data/certs
```

Crie o diretório para seu Registry no Docker:

```
$ sudo mkdir -p /etc/docker/certs.d/registry.4labs.example/

```

Copie os arquivos gerados para o o diretório criado:

```
sudo cp registry.4labs.example.cert /etc/docker/certs.d/registry.4labs.example/
sudo cp registry.4labs.example.key /etc/docker/certs.d/registry.4labs.example/
sudo cp registry.4labs.example.crt /etc/docker/certs.d/registry.4labs.example/ca.crt
```

## 2. Inicializando o Harbor

Realize o clone do repositório harbor-labs e copie o arquivo harbor.yml para o diretório do harbor

```
git clone https://github.com/silvemerson/harbor-labs.git 
```

```
cp harbor-labs/harbor/harbor.yml ~/harbor

```

Execute os scrips abaixo e aguarde o Harbor inicializar:

```
sudo ./prepare
```

```
sudo ./install.sh
```

Mapeie no seu /etc/hosts a seguinte linha:

```
172.16.0.103 registry registry.4labs.example
```

Por fim, acesse o Harbor pelo navegador:

https://registry.4labs.example

usuário: admin

senha: 4linux
