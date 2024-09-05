---
layout: post
title: Poetry, uma alternativa ao pip python.
date: 2024-08-22
categories: ["python", "linux", "poetry", "pip"]
---
![Dummy Image 1](https://picsum.photos/1366/768)



O Poetry é uma ferramenta moderna para o gerenciamento de pacotes e ambientes em Python, que visa simplificar o fluxo de trabalho de desenvolvimento. Este tutorial fornecerá uma visão abrangente do uso do Poetry, cobrindo desde a instalação até a migração de projetos existentes usando pip.

### Instalando o Poetry

A instalação do Poetry é simples e pode ser feita com um único comando:

```sh
curl -sSL https://install.python-poetry.org | python3 -
```

Após a instalação, adicione o Poetry ao seu PATH (se necessário) e verifique se ele foi instalado corretamente:


```sh
poetry --version
```


### Configurando o Poetry

Depois de instalar, é possível configurar algumas opções, como o local onde os ambientes virtuais serão criados. Para verificar as configurações padrão, execute:

```sh
poetry config --list
```
Para mudar o local dos ambientes virtuais para o diretório do projeto:

```sh
poetry config virtualenvs.in-project true
```

### Iniciando um Projeto com Poetry

Para iniciar um novo projeto, utilize o comando:

```sh
poetry new my-project
```

Isso criará uma nova estrutura de diretório com arquivos como pyproject.toml e README.md.


Se você já tem um projeto Python, pode iniciar o Poetry nele:

```sh
cd my-existing-project
poetry init
```

O comando interativo poetry init permite adicionar as dependências já utilizadas no seu projeto ao pyproject.toml.

### Instalando Pacotes

Para instalar pacotes, use o comando poetry add:

```sh
poetry add requests
```
Para instalar uma versão específica de um pacote:

``` sh
poetry add requests@2.25.1
```


O Poetry cria um arquivo poetry.lock para garantir que todos os desenvolvedores usem as mesmas versões de pacotes. Para instalar as dependências com base no poetry.lock, use:

```shell
poetry install
```


O arquivo pyproject.toml é o coração de um projeto gerenciado pelo Poetry. Ele contém as configurações do projeto, incluindo dependências, versão do Python, scripts, entre outros.

Aqui está um exemplo de como adicionar um script customizado:

```toml
[tool.poetry.scripts]
myscript = "mypackage.module:main_function"
```
Para adicionar dependências de desenvolvimento:

```sh
poetry add --dev pytest
```
### Como Usar Diferentes Versões do Python

Se você precisar usar uma versão específica do Python, especifique no pyproject.toml:

```toml
[tool.poetry.dependencies]
python = "^3.9"
```

Para alternar entre versões do Python, é possível usar o pyenv ou outra ferramenta de gerenciamento de versões. Ou com o gerenciador de pacotes do seu GNU/Linux.

### Gerenciando Ambientes Virtuais

Listando ambientes virtuais

```sh
poetry env list
```

outup:
```sh
test-O3eWbxRl-py3.6
test-O3eWbxRl-py3.7 (Activated)
```

escolhendo versão:
```sh
poetry env use test-O3eWbxRl-py3.6
```
Excutando dentro do ambiente virtual:
```sh
poetry run
```
exemplo, como excutar jupyter notebook ou jupyter lab

```sh
poetry new mynotebook
cd mynotebook
poetry add jupyter ou poetry add jupyterlab
poetry run jupyter notebook ou poetry run jupyter lab
```

### Gerenciando Ambientes Virtuais com poetry shell

O Poetry gerencia ambientes virtuais automaticamente, mas você pode ativar o ambiente manualmente com:

```sh
poetry shell
```
Para sair do ambiente:

```sh
exit
```

### Migrando de pip para Poetry

Se você já tem um projeto que usa pip e requirements.txt, migrar para Poetry é simples:

```sh
poetry init
poetry add $(cat requirements.txt)
```
ou
```sh
cat requirements.txt | grep -E '^[^# ]' | cut -d= -f1 | xargs -n 1 poetry add
```
Isso converterá as dependências do requirements.txt para o formato pyproject.toml do Poetry.
O Poetry é uma ferramenta poderosa que simplifica o desenvolvimento e gerenciamento de projetos Python. Com suas funcionalidades para instalação de pacotes, gerenciamento de dependências, configuração de ambientes e suporte a múltiplas versões do Python, ele é uma excelente escolha tanto para novos projetos quanto para migração de projetos existentes.

