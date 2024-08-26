---
layout: post
title: Usando docker com proxy local.
date: 2024-08-22
categories: ["proxy", "linux", "local", "docker"]
---
![Dummy Image 1](https://picsum.photos/1366/768)

Para usar uma configuração de proxy local, ou socks proxy para Docker, você precisa de uma configuração como esta usando um arquivo _.docker/config.json_ em seu /home, se não existir o arquivo pode criá-lo. Segue o exemplo de configuração que eu utilizo no dia a dia.

```sh
vim ~/.docker/config.json
```


```json
{
        "auths": {
                "ghcr.io": {
                        "auth": "chave do github"
                }
        },
        "proxies": {
                "default": {
                        "httpProxy": "socks://172.0.0.1:10337",
                        "httpsProxy": "socks://127.0.0.1:10337",
                        "noProxy": " "
                }
        }
}% 
```
No exemplo acima eu utilizo alguns pacotes docker do github, e em alguns casos para acessar preciso da chave para poder realizar o download. Já no segmento mais abaixo, estou usando **socks** para configurar o docker, é só salvar:

```sh
docker pull alpine
```
```sh
Using default tag: latest
latest: Pulling from library/alpine
c6a83fedfae6: Pull complete 
Digest: sha256:0a4eaa0eecf5f8c050e5bba433f58c052be7587ee8af3e8b3910ef9ab5fbe9f5
Status: Downloaded newer image for alpine:latest
docker.io/library/alpine:latest
```

