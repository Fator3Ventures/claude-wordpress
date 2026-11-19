# Entrega — Fator3 MCP Google 0.40.0

Revisão 1 · 2026-11-19T03:41:28-03:00 · Implementação e verificação em WordPress · **com-pendencias**

## 1. De onde esta versão entra

Instalação limpa ou atualização direta da 0.39.0. A correção surgiu durante a leitura de campo dos **Pedidos MCP Google 57 e 58**. A revisão de 19/11 do arquivo de pedidos acrescentou a situação do aceite aos dois itens. O número 59 continua disponível.

A base foi a entrega Google 0.39.0 do projeto, com instalador SHA-256 `9a8cadb240e6398f1a85a833fcce46bb7b1bfa251d74c5111984547a5c453fce` e fonte `69b6e25e450d4fcc2be6ffe60d66c01a77b727e186e84788f4b4d60270946489`. Requisitos do pacote são WordPress a partir de 7.1.4 e PHP a partir de 8.3. A bancada executou WordPress 7.1.4, PHP 8.3.6 e MariaDB 11.8.6. O PHP 8.4.27 executou a suíte unitária e o lint.

Conferidos integralmente `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos revisão 5 de 02/11/2026, a regra comum, a aba Google e o retorno do Core 1.96.0.

## 2. Convivência e encaminhamentos

| Pacote | Versão na bancada | Escopo |
|---|---|---|
| Fator3 MCP Google | 0.40.0 | Filtros, permissões, documentação e conversões |
| Fator3 Site Core | 1.96.0 | Contrato do produtor e as duas filas Ads no instalador oficial |
| Fator3 MCP | 0.51.0 | Consultas autenticadas e documentação paginada |
| Meta, LinkedIn e Pipedrive | 0.29.0, 0.26.0 e 0.12.0 | Convivência e ativação |

Foram conferidos os 210 arquivos do Google, os 1.280 do Core e os 481 do MCP contra seus ZIPs oficiais. O inventário em `evidence/040/installed.json` identifica os seis plugins. As identidades estão em `evidence/040/parity.json`. O instalador do Core recebido tem SHA-256 `dde2feadefdf08ab7973e7ea1be588b73709b723a088ef5549e43394aa7f73a5` e o fonte `632b51fe0124a1008474268f82e2edf4820305954221d2613c7e199ce2738afd`.

**Encerramento do impacto da 0.39.0.** O mantenedor do Core incorporou a retomada da mesma transação nas filas de aquisição e etapas comerciais e ajustou a leitura de vencimento das provas. A revisão 3 do impacto original registra a incorporação. O retorno do Core e o histórico do Google estão em `impacts/039/`. Nesta rodada, o ensaio integrado usou a 1.96.0 oficial. A correção do filtro é interna ao Google. Os consumidores seguem usando as mesmas operações e campos. O conjunto de campo já dispõe do MCP 0.51.0 e do Core 1.96.0 nos dois sites consultados. Para a troca do Google, basta instalar a 0.40.0 e conferir a prontidão.

Catálogo de 311 habilidades, com 123 leituras, 188 escritas e 46 definições de configuração. Contratos de configuração 4.0.0, catálogo 3.0.0, execução 2.0.0 e armazenamento 2.0.0. A extensão de conversões usa os contratos vigentes de aquisição e etapas.

## 3. Mudanças e evidências

| Item | Resultado |
|---|---|
| Consulta para o aceite dos pedidos 57 e 58 | No CTO Office, `google/audit` da 0.39.0 recusou a data final terminada em `.000Z` com `INVALID_ARGUMENT`. A consulta idêntica, com o mesmo instante expresso em segundos, funcionou. A falha também foi reproduzida em `google/list-jobs` na instalação de base. A fração de segundo é prevista na seção 5.6 do [RFC 3339](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). |
| Correção na 0.40.0 | As duas consultas passam a comparar os instantes com suas frações e a selecionar os registros de precisão inteira que caem dentro da janela inclusiva. Fração zero equivale ao segundo exato. Um início com fração positiva exclui o registro do segundo cheio anterior. Um intervalo válido que não contém segundo inteiro retorna uma página vazia. Datas invertidas, inválidas ou horários sem fuso continuam gerando erro. O filtro aceita datas de calendário no dia UTC. |
| Pedidos MCP Google 57 | Na bancada, o GA4 continuou pronto após falhas temporárias prolongadas com a mesma revisão. Falha conclusiva bloqueou o envio e uma nova verificação o recuperou. A verificação periódica do GA4 continua a cada 12 h. |
| Pedidos MCP Google 58 | Na bancada, Ads permaneceu pronto sem nova prova periódica. Uma aquisição de 45 dias retomou após 503, e uma etapa de 45 dias retomou após recusa de termos e nova prova. O ensaio cobriu revisão, referência, consentimento e a proteção contra repetição em incerteza genérica. |

O código da correção está em `includes/Storage/DateFilter.php`, compartilhado pelas duas leituras. Os schemas descritivos e o guia instalado mostram os limites. A paginação, o isolamento por conexão e os critérios de retenção continuam em vigor. A correção não grava nem dispara conversões.

## 4. Instalação e prova da troca

Usar o instalador da seção 8. No fluxo da frota, conferir o SHA-256 dos bytes publicados antes de usar `plugins/upload` com `expected_slug=wp-mcp-google-fator3` e `expected_sha256`. O endereço previsto para publicação é [o ZIP da 0.40.0 no repositório da frota](https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-google-fator3-0.40.0-instalador.zip). A publicação e a troca na frota cabem à operação.

| Prova própria | Resultado | Evidência no fonte, em `evidence/040/` |
|---|---|---|
| Base e atualização direta | 15 verificações na 0.39.0, incluindo as duas recusas. As 21 verificações após a troca preservaram os IDs e consultaram os mesmos seis registros em SQL via MCP HTTP. Cobertura de frações, fusos, intervalos vazios, duas páginas e recusa a credenciais inválidas. | `base.json`, `upgrade.json` |
| Instalação limpa | O Google foi ativado sozinho em banco novo. Passaram 37 verificações funcionais. Com o MCP ativo, passaram as 27 verificações do histórico. | `isolated.json`, `clean.json` |
| Prontidão e autorização | Nova requisição a `google/status` confirmou a versão 0.40.0 e 311 habilidades. `google/integration-status` com `compact=true` confirmou `read_success=true` e `google/storage-status` devolveu `storage.ready=true`. O assinante foi recusado nas consultas, na configuração e no painel. | `access.json`, `upgrade.json` |
| Documentação MCP | Na instalação limpa e na atualizada, 26 documentos lidos integralmente em 90 páginas, 120 verificações por instalação, incluindo identidade por SHA-256 e recusa de caminho fora do índice. Consulte `google/documentation` e o guia `GUIA-0.40.0.md`. | `docs-clean.json`, `docs-upgrade.json` |
| Regressão integrada | 51 verificações com o teste fornecido no fonte oficial do Core 1.96.0. Filas e recibos persistiram em WordPress real. Respostas Google e correio foram simulados. | `core196.json`, `parity.json` |
| PHP e build | 1.372 testes e 16.410 asserções em cada PHP, sem falhas ou pulos, no executor compatível do projeto. Os 206 arquivos PHP instaláveis passaram no lint em ambos. | `unit83.json`, `unit84.json`, `lint.json`, `docs-build.txt` |

**Campo em 19/11, horário de Brasília.** A pauta recebida registra implantação da 0.39.0 nos 12 sites às 02h12. As consultas próprias confirmaram Google 0.39.0, MCP 0.51.0 e Core 1.96.0 ativos em CTO Office e Site-Teste. Em CTO Office às 03h30min20s, GA4 estava pronto, com renovação às 02h00 e próxima às 14h00, zero falhas. Ads estava pronto, `valid_until_rejected`, sem expiração ou próxima tentativa. Havia zero incidentes abertos no diagnóstico Google. Entre 02h20 e 03h30min20s, a auditoria completa da conexão padrão devolveu zero eventos `conversion:verification` a partir da revisão 48583 anterior ao início. Às 03h32, a fila Ads do Core mostrou zero registros na consulta de um dia. O estado da frota inteira foi informado no anexo. A consulta direta abrangeu dois sites. Evidência sanitizada em `sites.json`.

**Encerramento da bancada.** Seis plugins oficiais ativos, zero senhas de aplicação e zero jobs. Os dados de ensaio, o usuário de teste e o bloqueador HTTP temporário foram removidos. Os sites remotos receberam somente consultas nesta rodada.

## 5. Banco, migração e recuperação

A atualização usa os timestamps inteiros e os índices existentes. As opções, credenciais, destinos, provas e filas dispensam conversão de dados. A leitura de períodos não dispara reenvio nem altera a revisão. A atualização direta foi exercitada com registros gravados pelo pacote anterior. Para recuperação operacional, preserve cópia coerente do banco e das chaves e concilie entregas com seus recibos antes de qualquer repetição. Uma correção posterior à instalação exige nova versão.

## 6. O que permanece pendente

- A frota e o titular da conta acompanham o CTO Office até **22/11/2026 às 02h20 de Brasília** para o aceite de 72 horas dos pedidos 57 e 58. Conferir GA4 sem bloqueio, Ads pronto sem verificação periódica do executor e uma conversão real com o resultado individual. Registrar a versão e o horário de qualquer troca durante a janela. A amostra desta rodada cobre os primeiros 70 minutos.
- A 0.40.0 foi validada em bancada. A distribuição da nova versão e a verificação remota dos seus bytes cabem à frota. A leitura em CTO Office e Site-Teste foi feita com a 0.39.0.
- Reconhecimento em conta Google, entrega real de e-mail, Sheets, campanhas e Cloud Shell não foram exercitados. O código de painel não mudou. A verificação do painel nesta rodada cobriu a autorização do assinante. A suíte executada usou o runner compatível, sem o PHAR oficial PHPUnit e sem a matriz histórica completa de promoção.

## 7. Credenciais e configuração do dono

A consulta exige acesso administrativo ao WordPress e a conexão Google selecionada. Em Ferramentas → Fator3 MCP Google → Conversões, a operação mantém a identidade e os destinos de GA4 e Ads já configurados. A mudança do filtro não exige nova credencial nem nova prova. O guia instalado inclui um exemplo com milissegundos, filtro por ação e conferência do indicador de cobertura.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-google-fator3-0.40.0-instalador.zip](wp-mcp-google-fator3-0.40.0-instalador.zip) | 997556 | `dedded6ec02dbed38bb75f028720a222ec9b6f9335b80e3aa600b44d284da030` |
| Fonte | [wp-mcp-google-fator3-0.40.0-fonte.zip](wp-mcp-google-fator3-0.40.0-fonte.zip) | 23198375 | `800d0fbaa35a2c00085e0356605d05925697b9741dc30685b3b39401e788dd89` |

Este é o relatório externo canônico. A cópia no fonte antecede o cálculo da identidade definitiva desse ZIP.
