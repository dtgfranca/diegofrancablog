---
title: "Migrei Do Wordpress Para Hugo"
date: 2025-09-24T16:33:47-03:00
draft: true
---

Bom, creio que vocês reparam que o blog teve um mudança no seu layout. Vou explicar para vocês o porquê
de eu fazer essa mudança radical do meu site. Vou contar a história desde o inicio.

Em 2019, eu estava, vamos dizer num platô,  de não conseguir terminar nenhum projeto, tudo que começava
eu parava de fazer e isso estava me frustando muito. Foi então que tive a ideia de criar um blog onde eu poderia subir de
maneira rápida que não demorasse muito a ser publicado para que eu não desanimasse durante o processo. Foi entao que eu escolhi o Wordpress e comprei um tema
que eu gostava. Eu fiz o deploy e o blog estava pronto e em poucos minutos já estava publicado e em produção, fiquei muito feliz com isso.
Demorei mais uns 7 meses para escrever o primeiro post, mas pelo menos eu conseguir terminar um projeto depois de vários anos. Eu estava  sem ideia do que escrever
foi entao que comecei a desenvolver algo para empresa na qual eu trabalhar , um docker para instalar o mysql e o oracle e foi um desafio e então eu não sabia onde colcoar para que ficasse posteriormente para consulta
lembrei do site e escrevi o post , pubiquei e fiquei muito feliz com isso. O blog apartir dali se transformou em algo onde eu adicionava as coisas que eu queria  pesquisar novamente , caso precisasse.

Essa foi a história do meu blog, mas depois de alguns anos eu comecei  a não gostar do layout do meu site e do seu desempenho, principalmente na parte mobile, não estava legal.
Adicionava plugins, para melhorar o cache, plugis para reduzir o css e o js, e ainda mais plugins para melhorar o desempenho, mas isso só ocasionou que meu wordpress ficou muito pesado com tantos plugins
o menu lateral ja estava tão grande que minha tela não aparecia todas as opções srsr, queria algo limpo e simples. Procurei um design para melhorar o layout e deixá-lo mais simples, fiz as mudanças , mas algo dentro de mim ainda não estava legal, queria algo mais simples ainda
um layout sem muitas firulas , somente algo que ficasse comfortavel de ler e fácil de gerenciar os posts.
Uma das coisas que não deixava eu sair do wordpress era o fato de poder agendar a publicaçao, colocar em rascunho, eram coisas simples mas para mim eu não via em outra plataforma. 

Comecei a ler sobre os sites estátics como o Hugo , Jekkil entre outros, mas fazia buscas superficiais e via que era em markdown e isso me deixava com um pé atrás , pensava omo seria dificil fazer o gerenciamento dessas páginas. Foi então que 
comecei a acompanhar o blog do akita(akita.com.br) e em uma publicação tinha algo falando sobre como ele tinha feito o seu novo blog, li, gostei foi entao que entrei no site do hugo comecei a ler e depois pensei: "Posso fazer um teste com meu blo para ver se vou gostar".
Ahhh não teve outro assim que li a documentação e vi que tem como eu configurar meus posts para uma data futura , facil de configurar, fácil de fazer o deploy o githubpage e netfly e o layout limpo, sem firulas de css e js foi amor a priimeira instalaçao sr, já fiz a migração do meu blog em wordpress para o hugo.

Agora vou mostar um passo a passo de como eu fiz a migração, mas no site do próprio hugo tem outras formas de fazer isso.
Instalando o Hugo:
Essa instalação estou fazendo em minha máquina pessoal com o Ubuntu 24.04.3 LTS, nessa parte eu tive um problema instalando o hugo via snap. Eu recomendo que a instalação, caso esteja utilizando o linux, que você acesse o repositorio 
do github:
https://github.com/gohugoio/hugo/releases
Procure pelo formato que vocês acharem mais conveniente, no meu caso foi o .dev,  e baixe o arquivo e faça a instalação.

Para conferir se está tudo certo, abra o terminal e digite:
hugo version

Exportando dados do wordpress:
1 - Acesse o wordpress e na opção ferramentas, selecione a o opção exportar e selecione todos os posts, com isso o wordpress vai gerar um arquivo com a extensão xml

Ocnvertendo para o Hugo 
Em posse desse arquivo, nós iremos agora converter esse arquivo para o formato do hugo. Com isso vamos instalar uma ferramenta CLI chamada wp2hugo.

Primerio fazemos o clone:
$ git clone git@github.com:ashishb/wp2hugo.git

Entramos no diretório:
$ cd wp2hugo/src/wp2hugo

Agora fazemos o build:
$ make build_prod

Com isso dentro desse diretório wp2hugo/src/wp2hugo/bin, vamos ter um arquivo chamado wp2hugo. Agora podemos executar esse arquivo:
./bin/wp2hugo --source wordpress-export.xml --download-media

Esse comando ele irá gerar um arquivo  com todos os posts do wordpress já no formato do hugo. Entre dentro do diretorio gerado e execute o comando:
hugo server 
E você verá todo o seu site já no padrão hugo, pronto para ser publicado. Nesse post não vou mostrar o passo a passo para a publicação, creio que para quem
já mantem um wordpress seja mais tranquilo para fazer um deploy no netfly ou no githubpage, vou deixar o link aqui desse dois, mas no site existem várias outras formas do deploy :

Netifly
https://gohugo.io/host-and-deploy/host-on-netlify/#article
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


Para mim, a migração foi libertadora: agora tenho um site mais leve, simples e rápido. Se você também sente que o WordPress está pesado, recomendo testar o Hugo.

