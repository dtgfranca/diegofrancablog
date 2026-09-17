---
title: "Guia Definitivo: Como Configurar o Mullvad Corretamente"
date: 2026-08-21T08:11:37-03:00
draft: false
description: "Um guia honesto sobre privacidade sem ilusões"
tags: ["VPN", "Privacidade", "Mullvad", "Segurança"]
categories: ["Segurança Digital"]
---

## Introdução: VPN não é anonimato

É comum pensar que uma VPN resolve o problema de privacidade sozinha. Eu também tinha essa impressão: ligou a VPN, pronto, ninguém mais consegue ver nada.

Na prática, não é bem assim.

Uma VPN esconde seu endereço IP e impede que seu provedor veja diretamente quais sites você acessa. Ela também é útil em redes Wi-Fi públicas. Mas isso não significa que você ficou anônimo.

Este guia mostra o que eu considero uma configuração razoável para usar o Mullvad e quais cuidados fazem sentido além da VPN.

---

## Parte 1: Quando usar VPN

### Onde faz sentido

| Situação | Por quê |
|-----------|---------|
| Wi-Fi público | Protege o tráfego contra pessoas na mesma rede |
| Evitar throttling do ISP | Pode ajudar quando o provedor limita determinados tipos de tráfego |
| Serviços geobloqueados | Permite usar um servidor em outro país |
| Privacidade básica | Seu ISP deixa de ver diretamente os sites que você acessa |
| Assuntos sensíveis | Adiciona uma camada de proteção |

### Onde pode causar problemas

| Situação | Problema |
|-----------|----------|
| Bancos | Alguns podem considerar o IP da VPN suspeito |
| Chamadas de vídeo | Pode aumentar a latência |
| Jogos online | Um servidor distante pode aumentar o ping |
| Torrents | É preciso verificar se a VPN permite P2P |

### E usar VPN o tempo todo?

Não existe uma regra dizendo que você precisa ficar conectado à VPN 24 horas por dia.

Se você está usando uma conta Google, Facebook ou Amazon, por exemplo, a VPN não impede que o serviço saiba quem você é. O login continua sendo um identificador.

Também não faz muito sentido usar VPN só porque "VPN é mais segura", sem considerar o que você está tentando proteger.

Para mim, o mais importante é entender **qual problema a VPN está resolvendo naquele momento**.

---

## Parte 2: Configurando o Mullvad

O Mullvad é interessante principalmente pela forma como trata as contas.

Não é necessário informar nome, telefone ou e-mail para criar uma conta. A conta é identificada por um número.

Também existe bastante documentação pública sobre o serviço, além de auditorias independentes.

### Passo 1: Instalação

Baixe o aplicativo diretamente pelo site oficial:

[mullvad.net/download](https://mullvad.net/download)

Ao abrir o aplicativo, crie uma conta. Ele vai gerar um número que você precisa guardar.

Esse número é importante. Não perca.

### Passo 2: Kill Switch

O kill switch é uma das configurações que eu considero mais importantes.

A ideia é simples: se a VPN cair, o aplicativo bloqueia o tráfego em vez de deixar sua conexão voltar automaticamente para o IP normal.

Depois de ativar, caso já não esteja ativado, faça um teste: conecte à VPN, derrube a conexão e tente abrir um site.

Se a internet continuar funcionando normalmente, vale investigar a configuração.

### Passo 3: DNS

Em **Settings → DNS**, você pode usar o DNS do próprio Mullvad.

Também existem opções para bloquear anúncios e rastreadores.

Eu evitaria configurar um DNS externo sem uma razão específica. Quanto mais serviços diferentes você coloca no caminho, mais difícil fica entender exatamente por onde seu tráfego está passando.

### Passo 4: Protocolo e anti-censura

- **Protocolo:** WireGuard é a melhor opção para uso normal.
- **Porta:** deixe em **Automático**. Só altere se você estiver enfrentando algum problema específico de conexão.
- **Em redes que bloqueiam ou dificultam VPNs:** vá em **VPN settings → Anti-censorship** e experimente opções como **Shadowsocks**.

O **Shadowsocks** adiciona uma camada de ofuscação que pode dificultar a identificação e o bloqueio da conexão VPN.

Se a VPN funciona normalmente na sua rede, não há motivo para ativar a anti-censura.

### Passo 5: Multihop

O Multihop envia a conexão por mais de um servidor antes de chegar ao destino.

Isso pode ser interessante em situações onde você quer dificultar a correlação entre o servidor de entrada e o de saída.

O problema é simples: mais servidores também significam mais latência.

Para navegar normalmente ou usar Wi-Fi público, eu não vejo necessidade de ativar isso.

Faz mais sentido para situações específicas em que você realmente precisa dessa camada adicional.

### Passo 6: IPv6

Se você não utiliza IPv6 na sua rede, pode considerar desativá-lo no aplicativo.

O importante aqui é evitar uma configuração em que o IPv6 acabe seguindo um caminho diferente do restante do tráfego.

Depois de configurar, teste. Não confie apenas no que aparece no aplicativo.

---

## Parte 3: A VPN não é suficiente

### 1. Vazamento de WebRTC

O WebRTC pode expor informações de rede que você talvez não queira compartilhar.

No desktop, as possibilidades dependem do navegador:

| Navegador | Opção |
|-----------|-------|
| Firefox | `about:config` → `media.peerconnection.enabled = false` |
| Chrome/Edge | Usar uma extensão que ofereça proteção contra vazamentos de WebRTC |
| Mullvad Browser | Possui configurações de privacidade mais restritivas por padrão |

No celular, a situação é diferente.

Se você estiver usando o Chrome no Android, por exemplo, não existe o mesmo controle sobre WebRTC disponível no Firefox ou em algumas versões de navegadores desktop.

Mesmo quando um navegador móvel permite instalar extensões, isso não significa necessariamente que o WebRTC esteja completamente desativado.

Se a atividade for mais sensível, eu prefiro usar um navegador pensado para privacidade em vez de tentar transformar um navegador comum em um navegador privado usando várias extensões.

### 2. Cookies e rastreamento

A VPN não impede que um site reconheça você por cookies ou pelo login.

Algumas ferramentas que podem ajudar:

- **uBlock Origin**
- **Privacy Badger**
- **ClearURLs**
- Firefox Multi-Account Containers

Também vale separar atividades quando isso fizer sentido. Usar a mesma conta em todos os lugares facilita bastante a criação de um perfil sobre você.

### 3. Teste de vazamentos

Depois de configurar a VPN, faça alguns testes.

| Site | O que verificar |
|------|-----------------|
| [dnsleaktest.com](https://dnsleaktest.com) | Vazamento de DNS |
| [browserleaks.com](https://browserleaks.com) | IP, DNS e WebRTC |
| [ipleak.net](https://ipleak.net) | Endereço IP e outras informações de rede |

Faça os testes primeiro **sem VPN** e depois **com VPN**.

O resultado esperado é que, conectado à VPN, os sites vejam o IP do servidor da VPN e não o seu IP público normal.

---

## Parte 4: Perguntas frequentes

### A VPN deixa a internet mais lenta?

Pode deixar.

Você está adicionando um servidor entre seu dispositivo e a internet, então existe um custo de latência e processamento.

A diferença depende principalmente da distância até o servidor, da qualidade da sua conexão e da carga da rede.

O WireGuard costuma ter um desempenho muito bom e é uma das razões para eu preferi-lo.

### Posso confiar no Mullvad?

Nenhum provedor de VPN deveria ser tratado como alguém em quem você precisa confiar cegamente.

O que eu considero positivo no Mullvad é a transparência, a política de não registro de determinados dados e as auditorias independentes.

Ainda assim, uma VPN não substitui outras medidas de segurança.

### Por que não usar uma VPN grátis?

Porque manter uma infraestrutura de VPN custa dinheiro.

Algumas VPNs gratuitas utilizam publicidade ou outras formas de monetização. Isso não significa que toda VPN grátis seja ruim, mas eu teria bastante cuidado antes de entregar todo o meu tráfego para um serviço desconhecido só porque ele não cobra nada.

### O Mullvad grava meus logs?

Segundo a política do próprio serviço, ele não registra atividades como histórico de navegação e os endereços IP de origem para identificar o que você está fazendo.

Isso não significa que uma VPN seja capaz de tornar alguém invisível.

A VPN é apenas uma parte da cadeia.

---

## Conclusão

Depois de configurar uma VPN, ainda existem várias maneiras de uma pessoa ser identificada.

O navegador pode entregar informações. Cookies podem identificar você. Uma conta pode associar toda a atividade ao seu nome. E, obviamente, uma VPN não protege contra phishing, malware ou uma senha fraca.

Por isso, eu vejo a privacidade como uma combinação de várias coisas:

1. Uma VPN confiável quando ela fizer sentido.
2. Um navegador com boas proteções de privacidade.
3. Senhas únicas para cada serviço.
4. Autenticação de dois fatores.
5. Cuidado com links e arquivos.
6. Testes para verificar se a configuração realmente está funcionando.

Não existe uma configuração perfeita.

A ideia é simplesmente deixar mais difícil coletar informações sobre você do que seria usando tudo no padrão.
```