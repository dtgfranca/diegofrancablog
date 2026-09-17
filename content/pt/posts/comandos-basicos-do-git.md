---
categories:
  - dicas
  - git
cover:
  alt: q7uy4yxekcljpr70p2xk-1
  image: /wp-content/uploads/2020/08/q7uy4yxekcljpr70p2xk-1.png
date: "2020-08-14T23:32:58+00:00"
title: Comandos básicos do Git
aliases:
  - /2020/08/05/comandos-basicos-do-git/

---
Fala galera, beleza? Então, estou aqui para ajudar aquelas pessoas que começaram a utilizar o Git e ainda encontra dificuldades com os comandos. Nesse tutorial irei demonstrar alguns comandos que irá facilitar muito na sua jornada de aprendizagem.

**ENTENDENDO O WORKFLOW DO GIT**

O GIT é um VCS (Version control system) open source mais utilizado no mundo na qual permite você acompanhar as mudanças no arquivo. Empresas e programadores ao redor do mundo utiliza o GIT para colaboração em desenvolvimento de sistemas e aplicações.

O GIT consiste em três seções: o **working directory, staging area** e **git directory**.

O **Working directory** é onde você adiciona, remove, edita seus arquivos. Então as mudanças ficam indexadas na **Staging area**. Depois que você commita suas mudanças, o snapshot das mudanças irão ser salvas no **Git Directory**.

**COMANDO BÁSICOS**

Aqui estam alguns comandos básicos do git, caso você queira se aprofundar mais nos comandos é so clicar no link no final desse artigo:

`git init` irá criar um repositório local

`git clone` é utilizado para fazer clone ou de um reposítorio remoto ou local. Exemplo.:  
Remoto: `git clone username@host:/path/to/repository`  
Local: `git clone /path/to/repository`

`git add` é usado para adicionar arquivos ao stage area. Exemplo.:  
`git add <arquivo.txt>`

`git commit ` irá criar um snapshot de mudanças que será salvo no git directory. Exemplo:  
` git commit -m" mensagem que será adicionado ao commit"`

`git config` Usado para configurar informações de umdeterminado usuário como por exemplo e-mail, username e etc. Exemplo prático:  
`git config --global user.email youremail@example.com`

**Fontes**:

[https://education.github.com/git-cheat-sheet-education.pdf](https://education.github.com/git-cheat-sheet-education.pdf)

[htt](https://www.hostinger.com/tutorials/basic-git-commands) [ps://www.hostinger.com/tutorials/basic-git-commands](https://www.hostinger.com/tutorials/basic-git-commands)
