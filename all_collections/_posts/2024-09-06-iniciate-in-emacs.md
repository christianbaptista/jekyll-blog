
---
layout: post
title: Iniciando Emacs, comecei com o básico... Ep. 01
date: 2024-09-06
categories: ["terminal", "linux", "emacs", "editor", "ide", "IDE"]
---
![Dummy Image 1](https://picsum.photos/1366/768)

Eu a muito tempo venho procurado uma ide, que mesmo que houvesse uma curva de aprendizagem, mas que fosse ligeiramente fácil de usar.
Venho a algum tempo olhando o VIM e suas variantes, mas tem alguns LSP's que não funcionam corretamente, como o de Golang, por exemplo.
Mas a minha maior preocupação é como sempre mudo de máquina e de SO, eu necessito algo mais fácil de configurar depois de pronto. Um amigo me indicou **doom emacs**, mas decidi entrar no universo do emacs stock.

Primeiro, instale o emacs de acordo com a sua distro.

```sh
sudo apt install emacs
```

Para abrir um arquivo:
```sh
emacs file.txt
```
ou simplesmente execute:
```sh
emacs
```
Para fechar o emacs é


ou abre o emacs e usa as teclas **ctrl + c + ctrl + f**
Em muitos tutoriais o control (ctrl) vai ser representado por um **C**, no caso seria C-x C-f
E agora para salvar?
Minha aventura no vim foi relativamente fácil, mas no emacs precisei desvendar, tudo foi reaprender como usar um editor de forma diferente, existe um emacs com atalhos do vim, sim sei que existe, mas preferi iniciar a jornada com ele default.
Aprendi que o primeiro **C** geralmente maiúsculo representa ctrl, então C-x C-s.

Pronto aprendi o basico, abrir e salvar um arquivo, e agora preciso aprofundar ainda mais. Gerenciar os pacotes e instalar algumas coisas, como um syntax highlight, fechar o arquivo ou buffer sem sair do emacs e criar assim nosso arquivo de configuração.
O emacs usa 3 lugares de configuração mas eu prefiro manter tudo dentro de _.config_ então vai ser:
```sh
emacs ~/.config/emacs/init.el
```
Vamos configurar o repositório principal:

```el
;: config repo melpa
(require 'package)
(add-to-list 'package-archives '("melpa" . "https://melpa.org/packages/"))
(package-initialize)
```
Salvamos C-x C-s e enfim o reload no arquivo com C-x C-e.
Agora temos o executar os comandos necessários para instalar qualquer pacote com **M** representa a tecla alt então Alt + x pack(tab):
```sh
M-x package-install
M-x package-delete
```
Ou inserir no init.el que fica mais fácil a configuração.

adicionando suporte a Markdown:
```el
(use-package markdown-mode
  :ensure t
  :mode ("README\\.md\\'" . gfm-mode)
  :init (setq markdown-command "multimarkdown"))
```
