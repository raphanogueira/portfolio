---
title: "Em constante evolução: minha jornada atual no Hapvida"
description: "Especialista em Engenharia de Software no Hapvida, responsável por projetar e implementar soluções de alta performance com .NET e Engenharia de Plataforma. Meu foco é resolver desafios complexos, otimizando a tecnologia para impulsionar o impacto positivo que geramos juntos."
slug: hapvida
date: 2025-09-23 20:00:00+0000
image: capa.png
categories:
    - Carreira
tags:
    - carreira
weight: 1
---

# Meu Diário de Bordo Profissional

Bem-vindo ao meu diário de bordo, um espaço onde documento os projetos, desafios e aprendizados mais marcantes da minha carreira como Especialista em Engenharia de Software e as vezes um Engenheiro de Plataforma.

## Diário de Bordo de um Engenharo de Plataforma

### Como a importação de 45 mil catálogos para o Backstage revelou um limite não documentado.

#### O Desafio: Mapeando o Legado com um IDP

Após a intensidade do projeto anterior, nosso foco retornou para a construção da nossa Plataforma de Desenvolvedor Interno (IDP). A missão era clara, mas monumental: importar e mapear os catálogos de todo o nosso sistema legado para o Backstage. O objetivo era finalmente trazer visibilidade sobre as dependências de cada componente dentro do Oracle, algo que até então não estava documentado. O principal obstáculo era o volume: aproximadamente 45 mil catálogos registrados em um repositório Git, com todos os seus relacionamentos.

#### A Investigação: O Mistério dos Erros 400

O processo de importação para o Backstage começou a falhar de forma consistente, retornando erros `400 Bad Request` sem uma causa clara. Após dias investigando logs e configurações, a frustração começou a crescer. As tentativas convencionais não funcionavam, e a documentação oficial não oferecia pistas.

Foi nesse ponto que decidi adotar uma abordagem mais drástica: em vez de apenas usar o plugin de *discovery* do Azure, eu iria reescrevê-lo. Meu objetivo era entender, linha por linha, como ele se comunicava com a API e por que nossas requisições estavam sendo rejeitadas.

#### A Descoberta: O Limite Oculto da API

Ao mergulhar no código e recriar as chamadas, a causa do problema finalmente apareceu. O *code search* do Azure possui um limite rígido e não documentado: **a API não permite uma combinação de `skip` e `take` superior a 2.000 registros**. Em outras palavras, era impossível paginar além do registro de número 2.000, o que tornava inviável a descoberta dos nossos 45 mil catálogos através de uma única consulta paginada.

#### A Solução Aplicada

Com a causa raiz identificada, a solução foi estratégica: segmentamos os 45 mil arquivos em múltiplas pastas. Agrupamos os catálogos por tipo e garantimos que cada pasta contivesse no máximo 2.000 itens, respeitando o limite da API. A nova abordagem funcionou. Notavelmente, enquanto a incorporação final das `Entities` no Backstage foi um processo gradual, a criação das `Locations` (os pontos de descoberta) foi praticamente instantânea, validando nossa estratégia e desbloqueando o processo.

#### Impacto e Próximos Passos

Essa descoberta não apenas resolveu nosso problema interno, mas também revelou uma falha crítica de documentação que poderia afetar inúmeros outros engenheiros. Como próximos passos, meu objetivo é duplo:

1.  **Contribuir com a comunidade:** Aprimorar os logs do plugin de *discovery* do Azure para que erros como este sejam mais claros e fáceis de diagnosticar.
2.  **Documentar a limitação:** Tornar pública a informação sobre o limite do `skip` e `take` para que outros usuários da ferramenta não percam tempo investigando o mesmo problema.

Essa experiência reforçou uma lição fundamental: às vezes, para resolver um problema complexo, é preciso ir além da documentação e mergulhar no código-fonte.

---

## Diário de Bordo de um Tech Lead

### Como superamos a incerteza e entregamos o projeto crítico.

Minha jornada no Hapvida começou com um batismo de fogo: o projeto HomeCare. Em julho de 2025, nosso time de Engenharia recebeu a missão de entregar, em 45 dias, uma aplicação complexa que estava em espera há mais de seis meses. Este post é um diário de bordo dessa experiência, detalhando os desafios, as soluções e, mais importante, os aprendizados que tirei ao assumir uma liderança técnica em um cenário de alta pressão.

#### O Ponto de Partida: Planejamento e Estimativa

O primeiro passo foi entender o tamanho do monstro. Dedicamos quatro dias inteiros a uma *Planning*, quebrando a especificação funcional em *Features* e estimando cada tarefa. Foi um processo intenso de imersão que nos deu o prazo final: 45 dias. A partir daí, organizei nosso *board* em Épicos e Histórias, assumindo a responsabilidade não só de codificar, mas de orquestrar o time de desenvolvimento e ser a ponte com a equipe de QA.

#### Sprint 1: A Prova de Fogo e a Primeira Vitória

Logo na primeira *sprint*, a realidade se impôs. Encontramos divergências claras entre a documentação e as informações que recebíamos. Cada dia parecia trazer uma nova mudança de escopo. Apesar disso, o time se manteve focado. Entregar aquela primeira parte e enviá-la para homologação foi crucial. Não era apenas código; era uma injeção de confiança de que, apesar dos problemas, éramos capazes.

#### Sprint 2: O Caos Organizado

A segunda *sprint* foi, sem dúvida, o clímax da nossa saga. Estávamos lidando com o fluxo mais complexo da aplicação, envolvendo consultas pesadas em um banco de dados Oracle e requisitos que surgiam no meio do caminho. O golpe veio no último dia: descobrimos que um fluxo central estava funcionalmente errado, invalidando metade do nosso trabalho. A sensação foi de um soco no estômago. Tivemos que, em uma corrida contra o tempo, refazer tudo em apenas dois dias. Foi aqui que a resiliência e a sinergia do time foram postas à prova.

#### Sprint 3: A Reta Final

Na última *sprint*, o caminho estava mais claro. Os incêndios das semanas anteriores nos fortaleceram e nos deram mais contexto sobre o projeto. Ainda que algumas inconsistências de informação persistissem, conseguíamos contorná-las com mais agilidade. Após muitas reuniões, trabalho focado e algumas horas extras inevitáveis, a linha de chegada apareceu. Entregamos o projeto.

#### Lições Aprendidas na Trincheira

Essa experiência foi uma aceleração de carreira compactada em 45 dias. Saí dela com uma visão muito mais clara sobre o papel de uma liderança técnica e sobre gestão de projetos em ambientes de alta incerteza. Meus principais aprendizados foram:

* **O Conhecimento é Cumulativo:** O time ao final do projeto não é o mesmo do início. Se tivéssemos o conhecimento do último dia no primeiro, teríamos sido ainda mais rápidos.
* **Estimativa sem Margem de Erro é Ilusão:** Nenhuma tarefa é "simples". Subestimar a complexidade é o caminho mais curto para atrasos. Sempre considere uma margem para o inesperado.
* **O Tech Lead é um Facilitador:** Meu papel mais importante não foi escrever o código mais brilhante, mas sim garantir que cada desenvolvedor tivesse o que precisava para fazer o seu melhor. Resolver um problema de acesso, por exemplo, era tão prioritário quanto corrigir um bug crítico.
* **A Liderança Inspira pelo Exemplo:** Em momentos de crise, a equipe olha para o líder. Transmitir calma e confiança de que o objetivo é alcançável é fundamental para manter a moral e o desempenho do time elevados.

### Agradecimentos e Trabalho em Equipe

Tive de trabalhar ao lado de pessoas que são referencia e nos apoiaram nessa entrega.

* **[Matheus Ulisses](https://www.linkedin.com/in/matheus-ulisses) (Gerente do time de Engenharia de Software)**
* **[Guilherme Ferreira]() (Especialista em Engenharia de Software para React Mobile)**
* **[Leonardo Oliveira]() (Especialista em Engenharia de Software para .NET)**
* **[Daniel Alvez Paezani]() (Especialista em Engenharia de Software para Java)**
* **[Ricardo Tanaka](https://www.linkedin.com/in/ricardo-takahiro-tanaka) (Especialista em Engenharia de Software para Java)**
* **[Thalya Oliveira](https://www.linkedin.com/in/thalyaoliveira25) (Desenvolvedora .NET)**

O projeto foi muito mais do que uma entrega no Hapvida. Foi a prova de que com um time com habilidades, experiência, maturidade, comunicação e muita resiliência, até os prazos mais impossíveis podem ser cumpridos.