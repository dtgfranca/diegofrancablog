---
title: "Migrei Do WordPress Para Hugo"
date: 2025-09-24T16:33:47-03:00
draft: false
---

Bom, creio que vocês reparam que o blog teve um mudança no seu layout. Vou explicar para vocês o porquê
eu fiz essa mudança radical no meu blog, mas antes vou contar a história desde o início.

## Porque decidir criar um blog
Em 2019, eu estava, digamos, num platô: não conseguia terminar nenhum projeto.
Foi então que tive a ideia de criar um blog, algo que eu pudesse concluir rapidamente, para não desanimar durante o processo de criação.
Escolhi o WordPress, comprei um tema e a hospedagem. Fiz a instalação e em poucas horas já estava tudo configurado e publicado. Fiquei muito feliz, pois finalmente tinha concluído um projeto.

Demorei mais uns 7 meses para escrever o primeiro post. Eu estava  sem ideia do que escrever. Na época, trabalhava em uma migração entre banco de dados na empresa. Eu estava criando  um Docker para instalar o MySQL e o Oracle, o que foi um  grande desafio, principalmente com a Oracle.
Após terminar a configuração, queria guardar o passo a passo para futuras consultas. Então lembrei do blog, escrevi o primeiro post [colocar link do post aqui], publiquei e fiquei muito feliz com isso. A partir daquele momento, o blog se transformou em um espaço onde eu registrava tudo o que aprendia e não queria esquecer.

## Minha frustração com o wordpress
Essa foi uma breve história do porquê eu decidir criar um blog, mas depois de alguns anos eu comecei  a não gostar do layout do meu site e do seu desempenho , principalmente na parte mobile, não estava legal.
Nos testes da pagespeed sempre gerava notas baixas e isso me frustava, então eu tentava otimizar: adicionava plugins para gerenciar cache, plugins para reduzir o css e o js, e ainda mais plugins para melhorar o desempenho, plugins para configurar formulário, plugin para gerenciar o adsense e o Analytics.
Enfim, eu estava programando "orientado a plugin", com tantos plugins instalados no  wordpress, o blog começou a  ficar muito pesado o 
o menu lateral ja estava tão grande que minha tela não aparecia todas as opções.

Queria um site que fosse simples, rápido. Procurei um design para melhorar o layout e deixá-lo mais simples possível, fiz as mudanças , mas algo dentro de mim ainda gritava que não estava legal, queria algo mais simples ainda:
um layout sem muitas firulas, pois meu objetivo é só escrever o que venho praticando.

Uma das funcionalidades que não me deixava sair do wordpress era o fato de poder agendar a publicaçao, colocar em rascunho, pré-visualizar os posts, eram funcionalidade simples, mas para mim eu não via alternativa em outra plataforma.
Vi algumas pessoas falando de ferramentas de geração de sites estáticos, estudei muito superficialmente e descartei logo de cara essa opção, pois quando lia que os posts eram criados em markdown e eu tinha que fazer o deploy usando o git, na minha cabeça era um retrocesso e logo pensava:
"Tenho um ambiente muito robusto com o wordpress que automatiza tudo".

## Aprofundando em ferramentas de geração de site estáticos
Foi então que comecei a acompanhar o blog do [Akita](https://akitaonrails.com/2025/09/10/meu-novo-blog-como-eu-fiz/) e em um de seus posts falava sobre como ele tinha feito o seu novo blog com o [Hugo](https://gohugo.io/hugo-modules/) e o [Hextra](https://themes.gohugo.io/themes/hextra/), li, gostei do que vi em seu blog
Como gosto muito do Akita resolvi então fazer alguns testes com a ferramenta e avaliar, aliás era o AKita utilizando essa ferramenta, então deveria ser boa.

Instalei em minha máquina, fiz alguns testes, gostei muito do layout simples, praticamente só html, vi que tinha tudo aquilo que eu precisava para gerenciar um blog pessoal e o mais importante: eu queria converter os meus antigos posts para essa nova ferramenta sem muito trabalho. 
Procurei e vi no próprio site eles ensinam a fazer essa migração com várias ferramentas, depois de ter feito todos esses testes agora estava pronto para a migração.

Fiz toda a migração e foi mais simples do que eu esperava, não gastei 5 horas para fazer a migração e o deploy no githubpages.

Agora que contei minha experiência, vou mostrar como fiz a migração passo a passo:

## Iniciando a migração
Instalando o Hugo:
Essa instalação estou fazendo em minha máquina pessoal com o Ubuntu 24.04.3 LTS, nessa parte eu tive um problema instalando o hugo via snap. Eu recomendo que a instalação, caso esteja utilizando o linux, que você acesse o repositorio 
do github:
https://github.com/gohugoio/hugo/releases
Procure pelo formato que vocês acharem mais conveniente, no meu caso foi o .deb, baixe o arquivo e faça a instalação.

Para conferir se está tudo certo, abra o terminal e digite:
```
 hugo version
```

### Exportando dados do wordpress:
1 - Acesse o WordPress e, no menu **Ferramentas**, selecione **Exportar**. Escolha a opção **Todos os posts**. O WordPress irá gerar um arquivo no formato .xml contendo todos os seus posts.
[Link da documentação  WordPress](https://wordpress.org/documentation/article/tools-export-screen/)

### Convertendo para o Hugo 
Em posse desse arquivo, nós iremos agora converter esse arquivo para o formato do Hugo. Com isso vamos instalar uma ferramenta CLI chamada wp2hugo.
Minha decisão por utilizar essa ferramenta foi simplesmente porque ela é uma ferramenta CLI e não precisa de muita configuração e facil utilização

### Primeiro fazemos o clone:
```
 $ git clone git@github.com:ashishb/wp2hugo.git  
```

Entramos no diretório:
```
$ cd wp2hugo/src/wp2hugo 

```

Agora fazemos o build:
```
$ make build_prod 

```


Depois de compilado dentro desse diretório wp2hugo/src/wp2hugo/bin, vamos ter um arquivo chamado wp2hugo. Agora podemos executar esse arquivo:
```
$ ./bin/wp2hugo --source wordpress-export.xml --download-media
```

- --source : Caminho do seu arquivo xml gerado pelo WordPress
- --download-media :  Esse parâmetro ele faz o download de todas as imagens dos seus posts, caso nao passar ele nao faz o download das imagens. 

Esse comando ele irá gerar um arquivo  com todos os posts do wordpress já no formato do hugo. Entre dentro do diretorio gerado e execute o comando:

```
hugo server
```

E você verá todo o seu site já no padrão hugo, pronto para ser publicado. Nesse post não vou mostrar o passo a passo para a publicação, creio que para quem
já mantém um site/blog em  wordpress seja mais tranquilo para fazer um deploy no Netlify ou no GitHub Pages, vou deixar o link aqui desse dois, mas no site existem várias outras formas do deploy :

Netifly:

https://gohugo.io/host-and-deploy/host-on-netlify/#article

Github Pages:

https://gohugo.io/host-and-deploy/host-on-github-pages/

Vou deixar uma tabela de comparativo entre o Hugo e o Wordpress para que vocês possam avaliar com mais calma:

### WordPress vs Hugo: o que muda?

| **Critério**            | **WordPress**                                                                 | **Hugo**                                                                 |
|--------------------------|-------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **Performance**          | Depende de banco de dados, PHP e plugins. Pode ficar pesado.                 | Gera páginas estáticas, super rápidas e leves.                           |
| **Complexidade**         | Muitos plugins, temas e configurações.                                        | Estrutura simples, posts em Markdown, foco no conteúdo.                   |
| **Manutenção**           | Requer atualizações de plugins, temas e segurança.                            | Sem banco de dados nem plugins: quase zero manutenção.                    |
| **Flexibilidade**        | Ecossistema enorme (plugins para tudo).                                       | Flexível via código e templates, mas sem “instalar e usar” facilmente.    |
| **Facilidade de uso**    | Painel amigável, bom para quem não programa.                                  | Precisa lidar com CLI e Git, mais técnico.                                |
| **Deploy**               | Necessita servidor (PHP/MySQL).                                               | Pode ser hospedado grátis no GitHub Pages, Netlify ou Vercel.             |
| **Agendamento de posts** | Nativo, muito prático.                                                        | Também suporta datas futuras via configuração no front matter.             |
| **Custo**                | Hospedagem + possíveis temas/premium/plugins.                                 | Hospedagem gratuita ou muito barata.                                      |

Fazendo o teste no Pagespeed:

Celular
{{< figure src="/images/2025/9/pagespeedcelular.png" alt="Descrição da imagem" caption="Legenda da imagem" >}}

Desktop
{{< figure src="/images/2025/9/pagespeeddesktop.png" alt="Descrição da imagem" caption="Legenda da imagem" >}}


Para mim, a migração foi libertadora: agora tenho um site mais leve, simples e rápido. Se você também sente que o WordPress está pesado, recomendo testar o Hugo.

