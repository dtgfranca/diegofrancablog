---
_advads_ad_settings:
  disable_ads: 0
_b2s_post_meta:
  card_desc: 'Faaala galera, blz? Hoje venho com uma dica sobre como ter padrão nas mensagens de commits em nossos projetos. As vezes quando se tem mais de um desenvolvedor '
  card_image: http://diegofranca.dev/wp-content/uploads/2020/08/demo-4-compressed.png
  card_title: GIT- Conventional Commits
  og_desc: 'Faaala galera, blz? Hoje venho com uma dica sobre como ter padrão nas mensagens de commits em nossos projetos. As vezes quando se tem mais de um desenvolvedor '
  og_image: http://diegofranca.dev/wp-content/uploads/2020/08/demo-4-compressed.png
  og_image_alt: ""
  og_title: GIT- Conventional Commits
_edit_last: "1"
_thumbnail_id: "304"
_yoast_wpseo_content_score: "30"
_yoast_wpseo_primary_category: "38"
author: diego.tg.franca@gmail.com
categories:
  - angular
  - dicas
  - git
  - javascript
cover:
  alt: demo-4-compressed
  image: /wp-content/uploads/2020/08/demo-4-compressed.png
date: "2020-08-11T14:36:05+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
fw_options:
  page-builder:
    builder_active: false
    json: '[]'
guid: http://diegofranca.dev/?p=266
parent_post_id: null
post_id: "266"
summary: Faaala galera, blz? Hoje venho com uma dica sobre como ter padrão nas mensagens de commits em nossos projetos. As vezes quando se tem mais de um desenvolvedor no projeto e a correria do dia a dia acabamos que as mensagens não ficam tão legais. É muito comum ter os famosos "AD" (Alterações diversas) ou o "VA" (Várias alterações), com isso dificulta muito a nossa vida de dev, que já não é fácil :D.
tags:
  - angular
  - conventional-commits
  - git
title: GIT- Conventional Commits
url: /2020/08/11/git-conventional-commits/

---
Faaala galera, blz? Hoje venho com uma dica sobre como ter padrão nas mensagens de commits em nossos projetos. As vezes quando se tem mais de um desenvolvedor no projeto e a correria do dia a dia acabamos que as mensagens não ficam tão legais. É muito comum ter os famosos "AD" (Alterações diversas) ou o "VA" (Várias alterações), com isso dificulta muito a nossa vida de dev, que já não é fácil :D.

O Conventional commit foi inspirado no  [Angular Commit Guidelines](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines), nos fornece um conjunto de regras para criação de um histórico de commits; o que torna mais fácil de escrever com ferramentas automatizadas. Essa convenção se encaixa com o [Sem Ver](https://semver.org/), descrevendo recursos, correções e alterações importantes feitas.

A mensagem de commit deve ser estruturada da seguinte maneira:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

O commit contem os elementos estruturais , para comunicar a intenção de quem consumir sua biblioteca:

1. **Fix**: um commit do tipo fix corrige um bug em sua base de código(isso se correlaciona com PATCH no controle de versão semântico);
1. **Feat**: O tipo de commit feat introduz um novo recurso para a base de código (Isso se correlaciona com o MINOR no versionamento semântico).
1. **BREAKING** **CHANGE**: Esse tipo de commit que tem o o rodapé BREAKING CHANGE ou anexado o ! após o tipo/ escopo introduz uma alteração de API de interrupção(Correlacionado com o MAJOR no controle semântico). A BREAKING CHANGE pode ser parte de commits de qualquer tipo
1. Tipos diferentes de _fix_ e _feat_ são permitidos, como por exemplo [@commitlint/config-conventional](https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional)  recomenda build:, chore:, ci: docs:, style:, refactor:, perf: test:, e outros.

**INSTALANDO O GIT COMMIT MSG LINTER**

Para nossa sorte alguns desenvolvedores criaram um package que nos ajuda a manter o padrão de commit de forma automática.

Para nosso teste irei utilizar o [package git-commit-linter](https://www.npmjs.com/package/git-commit-msg-linter)

Irei criar um projeto simples para testarmos o plugin. Crie um diretório com o o nome commit-conventional:

```
mkdir commit-conventional
```

Após executar o comando acima entre no dirétorio:

```
cd commit-contenvencional
```

Temos que inicializar o git :

```
git init
```

Agora vamos criar o arquivo package.json, para isso execute o comando, você tem quer o nodejs instalado em sua máquina :

```
npm init -y
```

Agora que temos o nosso package.json criado, vamos instalar o package:

```
npm install git-commit-msg-linter --save-dev
```

Crie um arquivo de texto qualquer:

```
touch teste.php
```

Vamos adicionar as mudanças na nossa stage área:

```
git add .
```

Se você ainda possui dificuldades com os comandos do git [clique aqui](/2020/08/05/comandos-basicos-do-git/) que explico alguns comandos básicos.

Para fazermos o teste execute:

```
git commit -m 'ADD a new file in project'
```

Será gerado o erro como na imagem abaixo, mostrando que o nosso commit está fora do padrão


{{< gallery cols="1" >}}  
{{< figure src="/wp-content/uploads/2020/08/Captura-de-Tela-2020-08-11-às-11.13.03.png" alt="" caption="" >}}  
{{< /gallery >}}  

Agora vamos commitar novamente mas agora seguindo o conventional commits:

```
git commit -m "feat: add new file into project"
```

{{< figure src="/wp-content/uploads/2020/08/Captura-de-Tela-2020-08-11-às-11.14.04.png" alt="" caption="" >}}

Agora sim, tudo perfeito com o nosso commit , você pode ver o log do commit fica muito mais claro e organizado nossas mensagens de commit

{{< figure src="/wp-content/uploads/2020/08/Captura-de-Tela-2020-08-11-às-11.14.42.png" alt="" caption="" >}}

Espero que tenha gostado dessa dica. Caso possui alguma dúvida ou sugestão ou crítica deixe nos comentários

**FONTE:**

[https://www.conventionalcommits.org/en/v1.0.0/](https://www.conventionalcommits.org/en/v1.0.0/)

[https://www.npmjs.com/package/git-commit-msg-linter](https://www.npmjs.com/package/git-commit-msg-linter)
