---
title: Descobrimento De Catálogos Através Do Azure
description: "Melhorias na documentação de descoberta de catálogos do azure"
date: 2025-08-23 21:00:00+0000
image: capa.png
slug: azure-discovey
weight: 3
categories:
    - Contribuição
tags:
    - Cloud Native
    - Backstage.io
---

## Análise de Erro 400 na Descoberta de Catálogo do Azure e Proposta de Melhoria

### Resumo do Problema

Durante a execução do processo de descoberta de entidades (`discovery`) para popular o catálogo do Backstage a partir do Azure, foi observado um erro `400 Bad Request` genérico. A falta de detalhes na resposta da API tornou a identificação da causa raiz um desafio.

### Análise e Causa Raiz

Após uma investigação aprofundada, foi necessário replicar o código do `AzureDevOpsDiscoveryProcessor` para adicionar logs detalhados, capturando o cabeçalho (*header*) e o corpo (*body*) da resposta da API do Azure. Com isso, conseguimos identificar o problema:

A API de **Code Search do Azure DevOps** possui uma limitação que não permite o uso de parâmetros de paginação (`$skip` e `$take`) em consultas cujo resultado exceda 2.000 itens. Quando essa condição ocorre, a API retorna o erro `400 Bad Request` com uma mensagem específica sobre o limite, que não era capturada pelo plugin.

Esta limitação não está documentada nas seguintes fontes oficiais:
1.  **Documentação da API REST do Azure DevOps:** [Fetch Code Search Results](https://learn.microsoft.com/en-us/rest/api/azure/devops/search/code-search-results/fetch-code-search-results?view=azure-devops-rest-7.1&tabs=HTTP)
2.  **Documentação do Plugin:** [Azure Catalog Module](https://github.com/backstage/backstage/blob/master/plugins/catalog-backend-module-azure/README.md)

### Ações Propostas

Com base na análise, tomei a iniciativa de propor as seguintes melhorias na comunidade do Backstage:

1.  **Atualizar a documentação do plugin:** Adicionar uma nota sobre a limitação de 2.000 itens da API do Azure Search para alertar os usuários sobre possíveis falhas em repositórios muito grandes.
2.  **Melhorar os Logs de Erro:** Revisar o código do *processor* para garantir que, em caso de falha, o corpo da resposta da API seja incluído no log de erro. Isso fornecerá um feedback mais claro e relevante para quem estiver depurando problemas semelhantes no futuro.

---

### Próximos Passos

O plano de ação para implementar esta contribuição está detalhado abaixo e será atualizado conforme o andamento:

-   [ ] **Fork do Projeto:** Criar um *fork* do repositório oficial `backstage/backstage`.
-   [ ] **Desenvolvimento:** Aplicar as alterações necessárias na documentação e no código-fonte do plugin `catalog-backend-module-azure`.
-   [ ] **Pull Request:** Abrir um Pull Request com as melhorias propostas para revisão da comunidade.
-   [ ] **Acompanhamento:** Monitorar o feedback do PR e realizar os ajustes necessários até que a contribuição seja aceita e integrada (*merged*).