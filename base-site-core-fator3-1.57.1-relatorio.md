# Entrega — Fator3 Site Core 1.57.1

Revisão documental 1 · 27/10/2026 (America/Sao_Paulo). Natureza: correção e consolidação das duas implementações 1.57.0, por solicitação explícita do dono. Slug: `base-site-core-fator3`. Contrato administrativo: **8.22.1**, **164 abilities**, ciclo de instalação de **17 etapas**. Normas aplicadas: instruções dos agentes revisão 4 e padrão de desenvolvimento/entrega revisão 5.

**Status: `com-pendencias`; apta no escopo testado.** A versão foi implementada, testada em WordPress limpo e em atualização nativa e instalada no Site-Teste. Preserva o banco e os contratos públicos da base canônica e incorpora as melhores proteções do candidato paralelo. O aceite GA4 com 30 dias de uma propriedade real permanece pendente de credencial/concessão. A exclusão local Core/Meta foi comprovada com SDKs originais e dados de teste; essa prova não homologa captura real de mensagens nem App Review. Não houve distribuição à frota ou publicação em GitHub.

## 1. De onde a versão entra

São caminhos validados: instalação nova em WordPress limpo e atualização direta **1.57.0 canônica → 1.57.1**. Não existe versão intermediária a instalar. O patch 1.57.1 foi expressamente solicitado pelo dono.

| Base examinada | Identidade e uso |
|---|---|
| Core 1.57.0 canônica instalada | Instalador 2696212 bytes; SHA-256 `5a829a78b3a2265560a88a0dde969fd435fd502ea2072e21ae8f47aeabf13ca6`. Base de runtime, schema e atualização. Fonte 4066204 bytes, SHA-256 `205bc18523b271afc76b76dbe5ce1e0fb19231ac5f31f19ae2ac3524ab54c758`. Anexos conferidos entre si e arquivos principais comparados à instalação. |
| Implementação paralela 1.57.0 não publicada | Instalador 2702843 bytes; SHA-256 `a7781197c291f50a859475a8e91f58bac3d6f87e8277400935c53cd34deaa4ab`. Fonte de ideias/proteções adaptadas. **Não é base suportada de migração**: apesar do mesmo número, tinha schema GA4 e formatos diferentes. |

Evidências no fonte: `inputs/1571/BASES.md`, `evidence/1571/installed-base-hashes.json`, `initial-differences.json` e plano prévio `history/1571/PLANO.md`. A comparação detalhada dos arquivos foi preservada; o candidato paralelo não é reentregue como instalável.

## 2. Convivência e encaminhamentos

| Pacote | Versão efetivamente observada | Escopo validado nesta rodada |
|---|---|---|
| Fator3 MCP | 0.33.0 | Decorador original, autorização nativa/MCP, documentação e instalação no Site-Teste. |
| Fator3 MCP Google | 0.20.0 | SDK original `ga4-reader/1.0.0`, concessão, paginação, cota, auditoria, revogação e paridade sintética de 30 dias. |
| Fator3 MCP Meta | 0.12.0 | SDK original `instagram-message-erasure/1.0.0`, consumidor de mensagens, exclusão local, recibo, falha parcial e retomada. |
| Fator3 MCP LinkedIn | 0.11.0 | Ativo no Site-Teste, sem alteração; preservação das configurações/cursor sem teste de API real. |
| Fator3 MCP Pipedrive | 0.2.0 | Ativo no Site-Teste; contrato `pipedrive-api-client/1.0.0` preservado. API real não exercitada. Requer PHP 8.3.36, portanto não integra a prova de ativação no piso Core 8.3.6. |
| DreamHost Panel Login / WP Super Cache / Yoast SEO | 1.0.0 / 3.1.4 / 28.7 | Permaneceram ativos no Site-Teste; sondas home/REST antes e depois aprovadas. Não equivale a teste funcional completo desses produtos. |

Nenhum acompanhante foi modificado. Não há nova ordem de troca entre versões já instaladas; Google compatível e concessão explícita são necessários antes de habilitar GA4, Meta compatível para concluir sua exclusão local. **Nenhum impacto técnico relevante ou pedido novo dirigido a outro mantenedor foi identificado** nas fronteiras examinadas; por isso não foram emitidos relatórios individuais de simples aviso. A alteração aditiva do contrato administrativo pertence ao Core. APIs externas não exercitadas permanecem declaradas na seção 6.

### Tratamento de pedidos e impactos recebidos

| Referência original recebida | Responsável e resultado | Evidência e limite |
|---|---|---|
| `wp-mcp-google-fator3-0.20.0-impacto-base-site-core-fator3(1).md`, revisão 1; Pedidos MCP Google 38 / **Pedidos core 313** | Mantenedor Core: consumidor filtrado por contrato, callback público `{property, revision, ready}`, concessão por propriedade, acervo e agenda próprios implementados e preservados. Sem leitura de segredos privados Google ou BigQuery. | `request-313.json` e `site-request-313.json`: 95 verificações em cada ambiente. Atendimento do consumidor comprovado; aceite real coordenado de 30 dias continua pendente. Não foi revisado o impacto apenas para comunicar esse resultado. |
| `wp-mcp-meta-fator3-0.12.0-relatorio(4).md`, seções de atendimento Core 309/Meta18(b) e exclusão; **Pedidos core 312** | Mantenedor Core: exclusão integrada ao SDK, alvo cifrado antes da remoção, recibo junto ao tombstone e pendência retomável. A 1.57.1 também conserva a requisição cifrada exata em falha parcial. | `request-312-1571.json` e `site-request-312-1571.json`: 32 verificações em cada ambiente. Exclusão local e repetição comprovadas; conversa/credencial real não foi homologada. |

Os relatórios recebidos de LinkedIn/Pipedrive e os contratos públicos vigentes foram considerados na convivência. Não houve encerramento editorial da lista central de pedidos nem alteração de documentos externos; o revisor da frota conserva essa atribuição.

## 3. Mudanças e evidência

### Escolhas entre as duas implementações

| Tema | Melhor preservado da canônica instalada | Melhor adaptado da paralela / resultado 1.57.1 |
|---|---|---|
| Persistência GA4 | Tabelas `coletas`/`linhas`, dimensões/métricas, estado `f3base_ga4_estado`, sete recortes, fuso, filtros e dados existentes. | Validação estrita do envelope, colunas obrigatórias e mecanismo InnoDB; rejeição explícita de schema incompatível. |
| Fotografias e exportação | Cursor cifrado, publicação atômica, exportação base64 com SHA-256 e períodos explícitos. | Rejeita cursor repetido, contagens divergentes, métricas inválidas e falha de cifragem; dados publicados antes da falha continuam disponíveis. |
| Histórico e agenda | Retenção ilimitada por padrão, habilitação e concessão explícitas. | Âncora inicial durável, alternância histórico/recente, política finita aplicada também à seleção e horário calculado no fuso da propriedade. |
| Exclusão Instagram | Outbox, chave idempotente aleatória, alvo cifrado, tombstone e formato de pendência/recibo. | Guarda de transação antes de qualquer remoção local; trava por contato; requisição cifrada estável; validação do contrato/recibo/estado final. |
| Operação e interface | Nomes públicos, permissões, inventário, opções e defaults efetivos existentes. | Qualidade paginável, revisão na navegação, revisão anterior na comparação e filtros GA4 explícitos nos relatórios integrados. Rótulos GA4 em português. |

Não foram incorporados o schema incompatível da paralela, cursor em claro, teto arbitrário de dez anos, renomeações de APIs, supressão de fuso/recortes, alteração dos defaults efetivos ou uma exigência adicional de operador sobre a concessão Google já existente.

### Pedidos core 312 — exclusão Instagram

Estado: `implementado`, `validado-localmente`, `validado-wordpress`.

A nova guarda compartilhada `F3Base_Transacao` verifica autocommit/transação sem confirmar ou desfazer transação do chamador. A exclusão Instagram verifica essa condição **antes de alterar qualquer dado local**. Uma trava por registro serializa eliminações concorrentes.

A coluna aditiva `pedido LONGTEXT NULL` da outbox armazena cifrada a requisição entregue a `eraseLocalData`, inclusive `expected_revision`, antes da chamada. Interrupção/falha parcial reutiliza exatamente essa requisição e a mesma chave. `revision_conflict` só permite capturar uma revisão nova quando o estado público comprova que a supressão não começou; em estado parcial ou incerto conserva a requisição original. Esse caso foi reproduzido com falha SQL parcial no SDK Meta e revisão alterada.

Contrato, recibo e estado público final são conferidos. Só depois da confirmação são limpos `alvo` e `pedido`; o recibo técnico mínimo permanece. Falta de SDK/autorização/recibo deixa pendência explícita. A disponibilidade do contrato é agora verificada pelos quatro métodos públicos. A operação não apaga mensagens na plataforma Meta, CRM, Slack ou backups: trata as cópias locais Core/Meta. Não cria uma identidade administrativa em cron.

### Pedidos core 313 — acervo GA4

Estado: `implementado`, `validado-localmente`, `validado-wordpress`; homologação de fornecedor real `pendente`.

Mantidos os sete recortes `resumo`, `paginas`, `aquisicao`, `dispositivos`, `paises`, `cidades` e `eventos`. Cada resposta exige contrato, auditoria, propriedade/revisão, cabeçalhos, dia, timestamp inteiro, linhas e métricas válidos, cobertura de paginação e cursor consistente. Resultados inválidos não publicam nova fotografia. A integridade do schema inclui colunas esperadas e InnoDB; tabelas novas são criadas nesse mecanismo.

Quando `inicio` está vazio, a primeira coleta fixa `inicio_efetivo`/propriedade em `f3base_ga4_estado`; ao atualizar aproveita o dia mais antigo já conhecido. Não há limite arbitrário de dez anos. Pendências têm prioridade; depois alternam-se histórico e reconciliação recente. Retenção positiva impede recolher automaticamente dados já fora da política; dia manual vencido retorna `dia_fora_da_retencao`. Retenção padrão continua `0`, sem prazo.

Campos opcionais em `f3base_ga4_acervo`: `revisitar_dias=3` (1–90) e `limite_pagina=1000` (1–1000). Preservam os defaults efetivos da canônica. A migração não reinicia estado/backoff apenas por materializar esses defaults; a prova nativa de preservação cobre isso. A agenda diária é recalculada como evento único no fuso configurado, inclusive mudanças de horário de verão. Não ativa coleta nem concede acesso automaticamente.

A barreira de recuperação cobre a coleta. A invalidação de recuperação inventaria o efeito, limpa cursores de coletas pendentes e pede reinício. Consultas/exportações aceitam `pagina_qualidade`, dez registros de qualidade por página; sem esse campo, mantém-se o formato completo anterior dentro do orçamento. `ga4-historico` aceita `coleta`/`limite`. O painel transporta a revisão entre páginas. `ga4-comparar` aceita `revisao_anterior`. `relatorios-integrados-ler` acrescenta `ga4_propriedade`, `ga4_recorte`, `ga4_revisao` e `ga4_revisao_anterior`; métricas próprias continuam separadas das GA4.

Contrato administrativo 8.22.1 e schemas gerados refletem esses campos aditivos. Não há alteração de versão dos SDKs Google/Meta/Pipedrive, do slug ou dos nomes de abilities. Documentação instalada atualizada, inclusive inventário da coluna `pedido`, configuração, recovery e changelog.

## 4. Instalação e prova de prontidão

### Ambientes e resultados

| Prova | Ambiente e resultado | Evidência em `evidence/1571` |
|---|---|---|
| Lint integral | 542 arquivos PHP, PHP 8.3.6; aprovado. | `installer.json` |
| Instalação limpa e atualização direta | WordPress **7.1.3 e 7.1.2**, PHP **8.3.6**, MySQL 8.0.46. ZIP exato, `Plugin_Upgrader`, processos novos por etapa, ciclo concluído, segunda migração `atual`, hashes de dados/configurações legadas preservados. | `native-cycles-1571.json`, `min/native-cycles-1571.json` |
| Pedidos core 312 | 32 verificações locais e 32 no laboratório isolado do Site-Teste. SDK Meta original/Graph controlado. | `request-312-1571.json`, `site-request-312-1571.json` |
| Pedidos core 313 | 95 verificações locais e 95 no Site-Teste isolado. SDK Google original/Data API controlada; paridade de 30 dias sintéticos. | `request-313.json`, `site-request-313.json` |
| Regressões de persistência/interface | 16 verificações em cada ambiente: fotografia, CSV, retenção, transação, interface e recibos. | `review-1571.json`, `site-review-1571.json` |
| Proteções acrescentadas | 32 verificações em cada ambiente: respostas inválidas, paginação, retenção, âncora, fuso, schema e transação externa. | `hardening-1571.json`, `site-hardening-1571.json` |
| Permissões | 16 verificações nativas e 16 com MCP em cada ambiente, incluindo revogação atual e cache. Nos registros Site-Teste, contagem comprovada por stdout/exit code; campo `evidence` está nulo. | `permissions-native-1571.json`, `permissions-mcp-1571.json`, `site-permissions-1571-native.json`, `site-permissions-1571-mcp.json` |
| Ausência de SDKs | 6 verificações em cada ambiente; Core mantém diagnóstico explícito. | `sdk-unavailable-1571.json`, `site-sdk-unavailable-1571.json` |
| Documentação integral | **928 verificações**, **136 documentos**, **630 páginas**, conteúdo/hash/autorizações, local e com decorador MCP real no laboratório isolado do Site-Teste. | `docs-1571.json`, `site-docs-1571.json` |
| Leitura pelo conector MCP compartilhado | `f3base/documentacao-ler`, `arquivo=docs/RELEASE-1.57.1.md`, `linha=1`, `limite=200`: 25 linhas completas, próxima linha nula, hash correto. | `site-documentation-mcp.json` |

Aceleração do atraso de confirmação ocorreu somente nos bancos descartáveis dos ciclos nativos. O ciclo compartilhado concluiu normalmente. As suites locais e de Site-Teste usaram dados de fixture próprios, sem autorizar consultas a contas reais. Interfaces foram renderizadas e verificadas no servidor; não foi feita inspeção manual completa em navegador.

### Troca observada no Site-Teste

Site: `https://fator3-teste-mcp-1.dreamhosters.com`, WordPress 7.1.3/PHP 8.3.36. Sequência executada: confirmar base 1.57.0 e hashes, criar backup privado integral, enviar o ZIP em partes, conferir seu SHA-256, instalar via **`plugins/upload-base64`** com `zip_path=wp-content/upgrade/f3-core1571-ee1c0eb8.zip`, verificar versão/atividade/ciclo/prontidão/documentação e limpar os auxiliares. O ZIP foi testado pelos bytes locais; não se declara instalação a partir de URL pública da frota.

Operação de instalação `3155e6bfdc8248963c0c08f9`; operação do pacote `66ac1ebdabd2048b10a652add5bd40f0`; backup de arquivos `38e7df3432ce43d97e96b235`. Atualização de 1.57.0 para 1.57.1 confirmada, plugin ativo. O transporte usou reativação silenciosa; a prova completa de instalação/ativação nativa está nos ciclos descartáveis acima, não é inferida apenas desse retorno.

Ciclo compartilhado **`25b96e73-317c-413e-bc23-21120650326e`**: 17 etapas concluídas, **0 falhas**, finalização confirmada no executor. Os **748 arquivos** instalados correspondem ao instalador e ao runtime do fonte. Manifesto SHA-256 de caminhos relativos ordenados e hashes individuais: `4b73c89e1de161a09a20259c3d719e83d520fe6ad64c13b6e226e59754f18e26`. Provas: `site-install.json`, `site-site-read.json`, `runtime-parity.json` e `site-final-plugins.json`.

Home e REST responderam 200 com bypass de cache comprovado antes/depois. Opções foram preservadas durante as leituras/renderizações. GA4 permaneceu inativo, sem propriedade e com serviço `not_granted`, sem coleta agendada. Os acompanhantes continuaram nas versões da seção 2. O teste não enviou comunicação comercial nem alterou concessões reais.

Limpeza confirmada: **89 tabelas** de fixture removidas, zero restantes, diretório privado e manifesto removidos. Controlador temporário removido com guarda de hash. O ZIP temporário foi consumido pelo instalador; a tentativa posterior de exclusão encontrou ausência e a leitura confirmou `not_found`. Não há pendência de limpeza desse ZIP. Backups privados de recuperação foram deliberadamente mantidos. Evidências: `site-cleanup.json`, `removed-qa.json`, `site-temporary-zip-status.json`; `removed-zip.json` registra a tentativa já sem arquivo.

## 5. Banco, recuperação e volta de versão

Sobre a 1.57.0 canônica, a mudança de schema é aditiva: **`{prefix}f3base_instagram_exclusoes.pedido LONGTEXT NULL`**. Mantêm-se as tabelas GA4 e suas colunas, tombstones e outbox. A instalação limpa cria a estrutura completa. Configuração recebe dois defaults opcionais; estado GA4 recebe âncora durável quando aplicável. A migração não expurga fotografias nem reinicia backoff por defaults equivalentes.

A atualização nativa semeou e comparou fotografia GA4, pendência Instagram cifrada, contatos, credenciais de teste, procedência e cursor/configurações LinkedIn. Os hashes dos campos legados e do estado foram preservados. Retenção ilimitada continua padrão; expurgo depende de política positiva escolhida pelo dono. Desinstalação explícita mantém recibos/pendências de exclusão, mas remove o acervo analítico GA4 conforme o desenho existente; não equivale a expiração automática.

Backup privado integral criado no servidor antes da troca, sem download do conteúdo: artefato **`1e350b00a2dd5b39ca200b6eb1cbe4c9`**, **29639983 bytes**, **100 tabelas**, **88385 linhas**, SHA-256 **`b45b8dacd2aa180e1f6bfeb124427034db982243170349c69a103266426747d1`**, operação `28950a6652c7dd2e279f68f3`. Apenas metadados foram incluídos em `site-backup.json`; nenhum dump integra a entrega.

Restaurar arquivos não desfaz banco nem exclusões já confirmadas no Meta. A 1.57.0 não conhece a nova requisição cifrada persistida; não se declara seguro reverter com exclusões pendentes. Prefira correção adiante. Uma restauração coordenada exige pausar coletores/ingestão, manter banco, arquivos, salts e guarda operacional coerentes e reconciliar exclusões antes da retomada. Backup antigo pode reintroduzir identificadores já apagados; bloqueios e recibos precisam ser preservados/reconciliados. Downgrade real não foi executado no Site-Teste.

## 6. Pendências de validação

| Item | Situação e motivo | Responsável / próximo passo |
|---|---|---|
| Aceite real Pedidos core 313 / Google 38 | `pendente`: propriedade vazia e concessão `not_granted` no Site-Teste. A comparação de 30 dias aprovada foi sintética. | Dono/operador Google: configurar conexão com acesso à propriedade e conceder leitura ao Core. Mantenedor Core/frota: coletar 30 dias, comparar com `ga/run-report` no mesmo recorte, validar lacuna/recuperação, auditoria, revogação e qualidade real. |
| Qualidade real de fator3.com.br | `pendente`: propriedade não consultada nesta rodada. | Dono/frota: conferir ausência de `(other)` nas dimensões principais ou agrupamento informado, em propriedade autorizada. |
| Captura real Instagram, App Review e ativos | `pendente`, herdada: Graph simulado nos testes. Exclusão de diário local com SDK real foi comprovada; não exige token novo para apagar dados locais. | Dono/operador Meta: homologar conversa real, produtos, permissões e ativos. |
| Tombstones anteriores sem alvo | Limitação conhecida: `alvo_anterior_indisponivel`; identificadores apagados não são reconstruídos. | Operador: tratar caso a caso sem inventar conexão/conta. Pendências com alvo cifrado continuam retomáveis com autorização atual. |
| Navegador completo, APIs reais de acompanhantes e downgrade | Não exercitados nesta rodada; não são certificados pela renderização/convivência. Instalação limpa, atualização e mínimos de runtime foram exercitados. | Mantenedor/frota, conforme o fluxo a homologar. Pipedrive real somente nos sites definidos pelo dono, não no Site-Teste. |
| Publicação e demais sites | Não executadas. | Dono/frota: autorizar distribuição, conferir nome/slug/hash contra este relatório e seguir o fluxo de publicação. Nenhum pedido foi enviado a terceiros. |

## 7. Credenciais e configuração do dono

**GA4:** no Core, Configurações → Medição e anúncios → Acervo GA4, informar `propriedade` canônica (exemplo de formato: `properties/123`), `inicio`, `horario`, `fuso` da propriedade e `recortes`. Os novos campos `revisitar_dias`/`limite_pagina` são opcionais. Deixar `f3base_retencoes_tecnicas.retencao_ga4_meses=0` para retenção sem prazo.

No pacote Google, configurar a conexão OAuth/Service Account apropriada para o serviço GA de leitura, com acesso à propriedade. Conceder explicitamente `google/configure-consumer`: `contract=ga4-reader/1.0.0`, `consumer_id=base-site-core-fator3`, propriedade e conexão selecionadas, `enabled=true` e `expected_revision` vigente. Só então habilitar `ativo` no coletor Core. O Core não recebe token próprio, não lê opções privadas Google e não pede credencial BigQuery. Campos/escopos específicos de autenticação continuam sendo os publicados pelo pacote Google.

**Instagram:** a eliminação local exige autorização administrativa atual (`manage_options` e gestão de leads); leitura privada conserva a permissão de leads, e uma concessão MCP revogada não é contornada. Não há token novo para essa exclusão. Para receber contatos reais, manter os opt-ins de ambos os pacotes e configurar conexão, token/ativos e permissões de mensagens em Ferramentas → Fator3 MCP Meta, conforme os campos do pacote e a aprovação do aplicativo. Nenhum valor secreto é incluído no relatório ou nos ZIPs.

## 8. Identidade dos arquivos

| Artefato | Nome final / link relativo | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [base-site-core-fator3-1.57.1-instalador.zip](base-site-core-fator3-1.57.1-instalador.zip) | 2707842 | `ee1c0eb8f46b7640a69e6b4e71697d5fc43bc9cd77f147c6219de1a410c5af62` |
| Fonte | [base-site-core-fator3-1.57.1-fonte.zip](base-site-core-fator3-1.57.1-fonte.zip) | 4145747 | `0600d83f31389055593645daf366465472c165b4a8ab2f85720da112e0b9aeb5` |

Relatório externo canônico: `base-site-core-fator3-1.57.1-relatorio.md`. Somente o instalador é destinado ao upload de plugins WordPress; o fonte contém runtime idêntico, build, testes, documentos de referência e evidências. Nenhum ZIP contém outro ZIP de entrega. Binários de laboratório, bancos, dumps e credenciais operacionais não integram os pacotes.

A cópia do relatório dentro do fonte está marcada **“cópia anterior ao fechamento do fonte”**. Tem a mesma evidência funcional e identidade final do instalador, mas remete a este relatório externo para tamanho/hash do próprio fonte, evitando circularidade. O fonte não foi reaberto para inserir seu próprio hash. Referências a versões/relatórios anteriores dentro do fonte são histórico identificado, não substituem esta entrega.
