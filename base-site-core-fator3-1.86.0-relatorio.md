# Entrega — Fator3 Site Core 1.86.0

Revisão 1 · 2026-11-14T19:34:00Z · Implementação e homologação dos pedidos 402 a 406. Slug `base-site-core-fator3`. Versão de distribuição 1.86.0. Contrato de configuração 8.41.0.

**Status da entrega — com-pendencias.** Implementação concluída e instalada no Site-Teste. O aceite em campo do pedido 405 exige dois ciclos de cron nos seis sites afetados.

Relatório externo canônico. A cópia no fonte foi gerada antes do empacotamento.

## 1. De onde esta versão entra

A conversa compartilhada “Plugin Core” fixou a base 1.85.1 e o alvo 1.86.0. A última atualização localizou o efeito do contato malformado nos relatórios. Recuperamos o fonte 1.85.1 (SHA-256 `7500da4e768b73d5e6d1b05fd8b3d08e6a316b8366ce6262ba246e104e135855`), o instalador 1.85.1 (`1fe1ba76880e7b6535af564a0fb702b823555d6307fb70d857b7081f64a4bfbd`), os três instaladores de mídia e o documento de 14/11 às 15h25. O candidato intermediário da conversa não estava entre os artefatos recuperados. As alterações foram reconstruídas sobre esse fonte e testadas nesta rodada. Os pedidos integrais constam de `reference/pedidos-402-406.md`.

Foram lidos integralmente `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos na revisão 5 de 02/11/2026. Requisitos do instalador e do projeto são WordPress 7.1.4 ou superior e PHP 8.3 de 64 bits ou superior. O laboratório executou WordPress 7.1.4, PHP 8.3.6 e 8.4.24 e MariaDB 11.8.6. O Site-Teste informou WordPress 7.1.4 e PHP 8.3.36. Os caminhos exercitados foram instalação limpa e atualização de 1.85.1 para 1.86.0.

## 2. Convivência e encaminhamentos

O Site-Teste confirmou ativos MCP 0.45.0, Google 0.35.0, Meta 0.26.0, LinkedIn 0.23.0 e Pipedrive 0.10.0, além do Core 1.86.0. A troca é somente do Core. No laboratório, com os três instaladores oficiais, o leitor Google registrou `google-ads-reader/1.0.0`, o Meta respondeu ao contrato `meta-ads-reader/1.0.0` com configuração pendente e o SDK do LinkedIn anunciou `linkedin-lead-reader/1.2.0`, com o seletor local em Core. Os resultados estão em `evidence/1860/leitores.json`.

Na revisão dos pedidos, as mudanças de interface, a preparação dos dados de leitura e a agenda foram localizadas no Core. Os contratos, seletores de conta, permissões e solicitações aos módulos acompanhantes conservam a interface vigente. Não se identificou ação de desenvolvimento, alteração de schema ou validação coordenada que justificasse relatório de impacto para outro pacote. Acompanhamento de operação da frota na seção 6.

## 3. Mudanças e evidência

| Pedido | Problema | Implementação | Prova |
|---|---|---|---|
| 402 · Erro fatal em Contatos | A apresentação decodificava de novo um array de Google Ads. Um valor histórico inesperado interrompia a lista e três relatórios. | O leitor aceita JSON e array. Revalida captura, revisão, conta, campanha e concessão antes de exibir o nome. A apresentação isola a linha ilegível. A preparação dos relatórios normaliza campos estruturados na leitura. | Na 1.85.1, seis capturas reproduziram o erro. Na 1.86.0, a mesma massa abriu a lista, o detalhe do registro, o CSV e Resultados, Campanhas e Métodos. Com o SDK controlado, os dois formatos autorizados retornaram o nome e cinco cenários de divergência ou ausência de concessão o omitiram. |
| 403 · Contatos | Filtros dispersos, linhas de aviso extensas e ausência de total/paginação. | Cabeçalho, abas Contatos/Testes/Lixeira, grade de filtros, campanha recolhível, remoção individual dos filtros e selos por estado. Contagem e paginação do mesmo recorte no servidor. A API mantém o cursor. | 55 registros sintéticos, com 53 contatos comuns, um teste e um na lixeira. O navegador mostrou 50 + 3, abriu o detalhe com aviso, voltou à página 2, removeu só o filtro de campanha e exportou os 53 registros. |
| 404 · Padrão das telas | Formulários, relatórios e outras áreas tinham navegação e tabelas inconsistentes. | Cabeçalho com orientação e versão, navegação que quebra em linhas e tabelas com rolagem local. Nas tabelas de dados já carregadas, busca e paginação locais. | 54 capturas das áreas principais, 150 de subabas e 3 da recuperação. As 207 retornaram HTTP 200, sem texto de erro crítico e sem exceder a largura da página em 360, 768 e 1440 px. Pausa e retomada exercitadas apenas no laboratório. |
| 405 · Continuação GA4 | Uma coleta bem-sucedida deixava espera antiga esgotada e gancho vencido. | O coletor automático guarda o instante até o qual cobriu o trabalho. O encerramento verifica tarefa, gancho, argumentos, ocorrência, cobertura, última atualização e reserva. A agenda remove o gancho vencido compatível e preserva o futuro. | A entrada normal do coletor publicou um dia no acervo real do laboratório com resposta de SDK sintética, concluiu a espera antiga, removeu o gancho vencido e manteve o próximo. Cenários com argumentos diferentes, reserva ativa e ocorrência futura foram preservados. |
| 406 · Histórico de e-mail/Pipedrive | O módulo inativo mantinha conferências pendentes. | A política de histórico, o CRM e a operação Pipedrive precisam estar ativos. O zelador encerra esperas elegíveis e remove o agendamento quando a conferência é inaplicável. A reativação retoma o agendamento. | Com a operação desligada, o processamento retornou `nao_aplicavel`. A espera antiga passou a concluída. Ao ativar, a conferência voltou à agenda. O teste também cobriu CRM ligado com a operação desligada. |

A suíte de domínio executou 30 verificações em cada uma das três execuções documentadas. O navegador conferiu mais dez interações. O manifesto e o ZIP conferiram por conteúdo nos 978 arquivos. Os 604 PHP passaram pela análise de sintaxe nas séries 8.3 e 8.4. O JavaScript administrativo passou por `node --check`. O ZIP reconstruído teve os mesmos bytes que o instalado. O diff do runtime contém três arquivos novos e 39 alterados. As imagens, os scripts, o stack da versão-base e os resultados ficam no fonte, em `evidence/1860` e `tests`.

## 4. Instalação e prova da troca

No laboratório, os mesmos dados de Contatos atravessaram a atualização a partir da 1.85.1. O segundo banco recebeu somente a 1.86.0 em WordPress limpo. Para a instalação homologada, o ZIP foi servido temporariamente em `https://fator3-teste-mcp-1.dreamhosters.com/wp-content/uploads/core-1860-homolog-0864ad1ef02caf6102.zip`. Conferimos os bytes servidos antes da troca. A chamada a `plugins/upload` usou esse endereço raw, `expected_slug=base-site-core-fator3` e o SHA-256 da seção 8, com sobrescrita e ativação.

| Ambiente | Verificação | Resultado |
|---|---|---|
| Site-Teste | Recibo e releitura independente por plugins/list | Operação `aa469a7e150f7fc639c0587c91410899`. 1.85.1 ativa → 1.86.0 ativa. |
| Site-Teste | Sondas da própria origem antes e depois, com bypass de cache confirmado | HTTP 200 na página inicial e em /wp-json/. Saúde geral lida como saudável. A amostra verifica disponibilidade. |
| Site-Teste | Índice e leitura integral por f3base/documentacao-ler | RELEASE-1.86.0.md (19 linhas), AGENTES-1.86.0.md (5) e GUIA-PAINEL.md (83). Todos os SHA-256 coincidiram com os arquivos do instalador. Leitura paginada e recusa ao usuário anônimo também exercitadas no laboratório. |
| Site-Teste | Consulta somente leitura de contatos e relatórios | Com limite 1, o segmento de testes devolveu um registro, e o segmento comum devolveu zero. Resultados, Campanhas e Métodos responderam com sucesso no recorte de testes de 14/11 e lista vazia. A prova com um registro malformado está no laboratório. |
| Site-Teste | Limpeza após a instalação | Remoção do ZIP temporário condicionada ao seu hash. A releitura retornou arquivo inexistente. Nenhuma fixture foi implantada no Site-Teste. |

O índice documental aceita uma consulta sem parâmetros. Para ler um arquivo, use `arquivo`, `linha` e `limite`, e prossiga enquanto houver `proxima_linha`. Os recibos sanitizados e os hashes dos três documentos estão em `evidence/1860/site-teste.json`.

## 5. Banco, migração e correção por nova versão

O pacote usa as tabelas e opções vigentes. Os contatos são normalizados em memória para apresentação. A atualização não regrava os registros históricos. O coletor grava o marcador `continuacoes_cobertas_ate` e atualiza somente intenções elegíveis. A operação pode repetir o encerramento. As verificações de cobertura, atualização e reserva protegem ocorrências independentes. O agendamento inativo do histórico de e-mail termina sem alterar os recibos individuais de e-mail. Falta de credencial em integração ativada continua distinguível de integração desligada. Correções posteriores à instalação exigem nova versão. A versão instalada no Site-Teste permanece 1.86.0.

## 6. O que permanece pendente

O responsável pela frota faz a implantação de produção. O aceite do pedido 405 exige observar dois ciclos consecutivos de `cron_24h` após a implantação e uma coleta concluída em fator3.com.br, ctooffice.com.br, engagia.com.br, conselar.com.br, fator3capital.com.br e desenvolvimentodesoftwares.com.br. Em cada site, conferir zero esperas GA4 esgotadas por `escopo_divergente` e zero ocorrências vencidas de `f3base_ga4_continuar`, sem chamar `reconciliar_esperas`. No portal desenvolvimentodesoftwares.com.br, a frota também pode conferir o pedido 406 com a operação Pipedrive já desligada.

As chamadas reais às contas comerciais do Google e do Pipedrive ficaram fora da homologação. A resposta GA4 e a concessão Google usadas na prova isolada são sintéticas. A rodada comprovou o reagendamento de histórico, sem buscar uma mensagem em uma caixa comercial. Sintaxe, resposta HTTP e largura das telas são evidências distintas da leitura de conteúdo ou de desempenho de campo.

## 7. Credenciais e configuração do dono

A versão dispensa nova credencial, escopo de acesso ou alteração de configuração pelo dono. O estado efetivo combina `f3base_email_historico.ativo`, `f3base_pipedrive.ativo` e `f3base_pipedrive_operacao.ativo`. A seleção de conta e a concessão vigentes do leitor Google são reaproveitadas. O modo de recuperação foi exercitado em WordPress descartável. A instalação no Site-Teste preservou o plugin ativo. A trilha de homologação contém dados sintéticos ou resultados operacionais agregados.

## 8. Identidade dos arquivos

| Artefato | Arquivo | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [base-site-core-fator3-1.86.0-instalador.zip](https://chatgpt.com/library?file_id=libfile_fde3_f-c5f9d5b29ce88191b3a6395644a1f85b_32706b9c47908191baafe72f89b6caee&account_id=personal) | 4.480.591 | `0864ad1ef02caf6102e8f6294b42816ab7bd884081c1a3518ab08fc20b9e7f46` |
| Fonte | [base-site-core-fator3-1.86.0-fonte.zip](https://chatgpt.com/library?file_id=libfile_fde3_f-3c6b8aadabd4819183012950ad2e538a_32706b9c47908191baafe72f89b6caee&account_id=personal) | 84.746.155 | `9c27ba8ff701238850b094b13a5df41cf47cd619076e75016c6b62736a9fb62e` |
