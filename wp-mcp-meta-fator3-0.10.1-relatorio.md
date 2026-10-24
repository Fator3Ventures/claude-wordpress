# Entrega — Fator3 MCP Meta 0.10.1

Revisão: 1 · Data: 24/10/2026 (America/Sao_Paulo) · Rodada: implementação dos Pedidos MCP Meta 16 e 17 e revisão final.

Slug/pasta/provider: `wp-mcp-meta-fator3` · Basename: `wp-mcp-meta-fator3/wp-mcp-meta-fator3.php` · Versão/build: **0.10.1**.

Status: **apta-no-escopo-testado, com pendências de homologação externa**. Instalada e ativa no Site-Teste. A versão corrente desta entrega é 0.10.1.

**Relatório externo canônico.** Fonte fechado e verificado. A cópia dentro do fonte é identificada como anterior ao fechamento e mantém os campos de identidade do próprio ZIP pendentes para evitar circularidade.

## 1. De onde esta versão entra

Base aceita: **Meta 0.9.0**, conforme a aba recebida `Fator3 MCP Meta(9).md`. Instalador: 173724 bytes, SHA-256 `e26aede1591426e06b8a69b5ad405cf13cb70c28d41b607346188c9d21a15662`. Fonte: 1218318 bytes, SHA-256 `2c80d2e290c2ef453c1d92d9b7cea6f5f0bf77a8585bc46cd77f7ba0f4023e65`. A implementação partiu desse fonte; os ZIPs aceitos não foram alterados.

Foram considerados os pedidos 16 e 17, fontes/instaladores/relatórios atuais dos acompanhantes, impactos recebidos e instruções do projeto na **revisão 5, de 23/10/2026**. A revisão 4 reanexada não substitui a revisão 5. A lista central de pedidos permanece sob seu responsável; nenhum ID foi criado nem item central encerrado por esta entrega.

A 0.10.0 implementou os pedidos e foi instalada no Site-Teste nesta rodada. Na conferência documental posterior foi encontrada uma orientação antiga contraditória sobre a gravação do nome. A correção gerou **0.10.1**, sem sobrescrever o instalador 0.10.0. Também foram esclarecidos o catálogo atual e textos históricos de recuperação/reversão. O patch não muda código funcional, JavaScript ou schemas: 20 arquivos PHP funcionais idênticos; bootstrap e Config alteram apenas a versão. Evidência: `evidence/0.10.1/patch-diff.json`.

**Entrada direta 0.9.0 → 0.10.1 comprovada; não é necessário instalar 0.10.0.** Instalação limpa comprovada no mínimo declarado: WordPress **6.4**, PHP **8.1.2-1ubuntu2.28**, 64 bits, MySQL **8.0.41**, criptografia disponível. Ambiente atual: WordPress **7.1.3**, PHP **8.3.36**, MySQL **8.0.41**. MariaDB, multisite e outras combinações não foram exercitados nesta rodada; a restrição de ativação individual permanece.

## 2. Convivência e encaminhamentos

As versões abaixo estavam ativas conjuntamente no laboratório integrado e foram preservadas no Site-Teste. Os runtimes integrados corresponderam a **1214 arquivos** dos pacotes fornecidos/aceitos, incluindo os 45 arquivos do Meta final.

| Pacote | Versão | Bytes do instalador | SHA-256 do instalador | Prova própria pertinente |
|---|---|---:|---|---|
| Fator3 Site Core | 1.51.0 | 2270123 | `7d6c9b8391e8f3a83a85dacbabea56cf93da6f6b04e7e195fcdceb4774f9f192` | Ativação conjunta, runtime exato e registro do cliente Pipedrive |
| Fator3 MCP | 0.30.1 | 879690 | `4dbe9ea5e3c9c2bc6ef5aaa574800e482226f0f1406e87a4fd818c68aa7260da` | Política, idempotência, redação de segredos, descoberta e leitura documental |
| Fator3 MCP Google | 0.19.0 | 809436 | `d15868915e3fdf886d7e883a82d9d302df7242808fc94d45bf3e1857234759d1` | Runtime aceito e ativação conjunta; sem operação Google externa |
| Fator3 MCP LinkedIn | 0.10.1 | 254066 | `6182ea63bff6788f5d2637467e7ab29d58568e37283d6ece82d3e58ee41c13bc` | Runtime exato e capabilities independente, registro central preservado |
| Fator3 MCP Pipedrive | 0.1.0 | 42095 | `3366d83ca8908e407a0736812d30b8fa1506a8c1458a28cfb47eda6fd8f3c54f` | Registro presente; gate retorna `operacao_nao_autorizada`, sem chamada externa |

Fontes/relatórios recebidos foram examinados; seus resultados não são convertidos em provas próprias. Identidades dos ZIPs novos estão em `inputs/0.10.0/packages.json`; o Google usa a base aceita da rodada anterior. Não foi alterado código, configuração comercial ou credencial de outro pacote. Nenhuma ordem de atualização conjunta nova é exigida.

**Impactos e pedidos emitidos nesta rodada:** nenhum. Foram examinados descoberta, autorização, idempotência, redação do MCP, isolamento dos builds, convivência com Core/Google/LinkedIn e gate do Pipedrive. Não foi encontrada consequência técnica relevante ou solicitação a outro mantenedor que justificasse um arquivo de impacto. Nas interfaces verificadas, **não foi identificada regressão no LinkedIn**. Isso não equivale à homologação de todos os fluxos comerciais dos acompanhantes.

**Tratamento de impactos recebidos e anteriores:**

| Documento / revisão | Pedido e responsável | Resultado nesta rodada | Evidência / limite |
|---|---|---|---|
| `impacto-mcp-0.29.1-para-wp-mcp-meta-fator3.md`, revisão 2 | R1: não repetir mutação com efeitos incertos; fronteira read/maintenance de health/status. Mantenedores MCP e Meta, cada qual no próprio domínio. | Contrato conservador preservado: `retryable` não prova ausência de efeitos; ausência/null de `applied` conserva o recibo. Read permite health e recusa status; maintenance permite status. | Suíte integrada final, 23 verificações, usando o MCP 0.30.1 real. Sem reenvio externo. |
| `wp-mcp-linkedin-fator3-0.8.1-impacto-wp-mcp-meta-fator3.md`, revisão 2 | R1/R2: isolamento de job ilegível e diagnóstico legível. Responsável Meta. | Correções anteriores mantidas. Isolamento não reescreve ciphertext/revisões/datas; health continua legível. | 11 regressões executadas na etapa 0.10.0, no ambiente atual e no mínimo. Arquivos funcionais idênticos na 0.10.1; não se afirma execução nova desses 11 no patch. |
| Encaminhamentos Core/Pipedrive presentes nos relatórios novos | Contrato `pipedrive-api-client/1.0.0`; responsáveis Core e Pipedrive. | Registro disponível e recusa administrativa esperada confirmados. Nenhuma adaptação identificada no Meta. | `integration.json` e `site-final.json` da 0.10.1; autorização comercial e envio Pipedrive não foram exercitados. |

Esses registros são acompanhamento no relatório principal, conforme a revisão 5. Os documentos históricos permanecem preservados como entradas; não foram revisados, reemitidos ou entregues como novos impactos para anunciar atendimento/encerramento. O encerramento editorial de pedidos centrais cabe ao responsável pela lista.

## 3. Mudanças e evidência

| Pedido exato | Problema | Implementação | Evidência e limite |
|---|---|---|---|
| Pedidos MCP Meta **16(a–c)** | Prévia do formulário Editar ficava dentro do bloco de renovação recolhido; recusa distante do botão. | Prévia própria junto de cada formulário; renovação abre seu bloco; foco programático e anúncio acessível; recusa local orienta o botão de troca. Respostas assíncronas obsoletas são descartadas e alterações invalidam a confirmação. | 25 verificações DOM; HTML renderizado pelo WordPress, respostas REST simuladas. Inspeção visual em navegador permanece pendente. |
| Pedidos MCP Meta **16(d)** | Nome digitado se perdia na troca. | `label` opcional, até 120 caracteres, em `meta/switch-identity`; prévia retorna `connection_label`. Nome participa da confirmação e é gravado com credencial/conexão/agendas na mesma transação e revisão. Sem `label`, preserva nome salvo. | Prévia sem mutação, alteração de nome invalida confirmação, troca e rebase de todas as agendas conferidos nas 41 verificações finais. Duas identidades sintéticas; aceite com contas reais pendente. |
| Pedidos MCP Meta **17(a–b)** | Recusa de Story poderia parecer perda de autorização da conexão. | `story_expired` exige recusa do fornecedor e timestamp de pelo menos 24 h; `story_insights_unavailable` cobre indisponibilidade sem prova de expiração. Resposta válida não é descartada pela idade. Falha de recurso só vira `not_authorized` global se `/me?fields=id`, com a mesma credencial, também confirmar recusa de autorização. | Story vencido, recusado, ausente, sem métrica e validação inconclusiva não enviam aviso de autorização. Token revogado confirmado marca todas as agendas da conexão, incluindo pausadas. Rede/quota mantêm retry. Testes nativos com HTTP sintético. |
| Pedidos MCP Meta **17(c)** | Código Graph não ficava disponível na auditoria das coletas. | `last_error` durável em agendas, auditoria e cobertura: código, HTTP, código/subcódigo Graph e instante; dados desconhecidos ficam null. Eventos `collection-run` e `schedule-dispatch` incluem origem, agenda/job/conexão e diagnóstico sanitizado. | Códigos preservados na consulta, continuação e auditoria; assinante recusado; mensagens brutas/segredos ausentes. Integração comprova que o redator MCP preserva o diagnóstico medido. |
| Pedidos MCP Meta **17(d)** e regra de incidente da solicitação | E-mail não distinguia a causa e podia repetir o mesmo incidente. | Aviso informa causa medida e ação adequada. Uma tentativa por incidente ativo, inclusive envio falho/incerto. Recuperação encerra o incidente antes de avisar; nova ocorrência posterior pode gerar novo aviso. | Persistência além de uma hora não repete; recuperação não envia alerta antigo; novo incidente pode avisar. Entrega real de correio não foi testada. |
| Revisão final desta rodada, sem novo ID de pedido | Manual ainda descrevia comportamento anterior ao pedido 16. | Patch 0.10.1 corrige CONFIGURATION, WORKER e TROUBLESHOOTING, organiza changelog e atualiza metadados de versão. | Comparação de bytes, lint, suites finais e leitura integral dos 18 documentos pelo MCP. |

As **35 operações** foram preservadas. Comparação dos schemas de entrada com 0.9.0: apenas `switch-identity` muda, pela adição opcional de `label`; os outros 34 são iguais. Saídas de agendas acrescentam `last_error`/`last_success_at`; cobertura acrescenta `last_error`. Não há renomeação de slug, basename, namespace, hooks públicos, permissões ou concessões.

Falha de conexão confirmada é vinculada a `authorization_revision` e `credential_generation`; job antigo não pode diagnosticar a nova credencial. São preservados seleção, principal, pausa e revisão de autorização das agendas. Falha local de administrador/concessão continua recusada e não se propaga a outros principais. Recusa isolada de ativo não-Story permanece `asset_access_denied`. Métrica ausente continua null, nunca zero. Recusa do inventário pausa o job atual e conserva a agenda para a próxima execução.

O último erro permanece após sucesso para investigação; `last_code=null` e `last_success_at`/`last_recovered_at` indicam recuperação. Apenas resultado novo confirma recuperação remota, não cache antigo. A auditoria tem retenção de 30 dias e não guarda token, corpo bruto Graph, URLs ou headers. A causa histórica dos e-mails de produção continua **hipótese**, pois seus códigos não foram capturados à época.

Comparação do runtime final com 0.9.0: **2 arquivos adicionados, 25 alterados, 18 idênticos e nenhum removido**. Os adicionados são CollectionState e seu documento de diagnóstico. Evidência completa em `evidence/0.10.1/runtime-diff.json`.

## 4. Instalação e prova da troca

Site autorizado: **https://fator3-teste-mcp-1.dreamhosters.com/**. Instalado o ZIP final pela operação MCP `plugins/upload-base64`, com `activate=true`, `overwrite=true`, `expected_slug=wp-mcp-meta-fator3` e SHA-256 exato da seção 8. Não há URL raw publicada nesta rodada: o pacote foi enviado diretamente, sem Git/frota.

Troca compartilhada **0.10.0 → 0.10.1**: operação `e56f3056b427e8a28fd1b362`, operação de pacote `bcdee4a004dbe4460802f43352c5703e`, backup de arquivos `2d8bba13e2553184b702ad7c`; `applied=true`, ativo antes/depois e hash confirmado. Home e `/wp-json/` responderam 200 antes/depois, em processo PHP novo e com bypass de cache verificado. São sondas internas de mesma origem: não comprovam acesso público externo nem limpeza de cache público. A reativação foi silenciosa; ciclo de ativação limpa foi provado separadamente no laboratório.

A troca inicial 0.9.0 → 0.10.0 nesta mesma rodada tem operação `5862414280f61af45f628a97` e backup de arquivos da base aceita `df41d3d04d6a0615f591ea56`. A prova de atualização **direta 0.9.0 → 0.10.1** foi executada em banco isolado, trocando o runtime exato e iniciando novo PHP. São provas distintas; não se apresenta a troca do laboratório como execução do uploader.

| ID | Ambiente / versão efetiva | Cenário | Resultado | Evidência no fonte |
|---|---|---|---|---|
| T1 | Local, PHP 8.3.6 / Meta 0.10.1 | Build, lint de 23 PHP, catálogo e sintaxe JS | Aprovado | `evidence/0.10.1/build-check.json`, `patch-diff.json`, `runtime-diff.json` |
| T2 | WP 7.1.3 / PHP 8.3.36 / Meta 0.10.1 | Atualização direta da base, preservação exata | **5/5**: 5 registros, 1 histórico e 1 option de negócio; ciphertext, revisões, projeções e datas iguais | `evidence/0.10.1/upgrade-preservation.json` |
| T3 | Mesmo laboratório após atualização | Documentação, metadados, efeitos e autorização | **104/104** | `metadata-upgrade.json` |
| T4 | Mesmo laboratório após atualização | Pedidos 16/17 | **41/41** | `request16-17-upgrade.json` |
| T5 | WP 7.1.3 / PHP 8.3.36, seis pacotes ativos | Integração real do MCP, gates, recibos, redação, acompanhantes | **23/23** | `integration.json` |
| T6 | WP 6.4 / PHP 8.1.2 de 64 bits / Meta 0.10.1 | Instalação limpa no mínimo; docs/REST/smoke | **25/25** | `minimum-clean-install.json`, `minimum-php-enable.json`, `minimum-smoke.json` |
| T7 | Mesmo mínimo exato | Pedidos 16/17 e credenciais do pedido 15 | **41/41 + 55/55** | `minimum-request16-17.json`, `minimum-credentials.json` |
| T8 | jsdom 27.4.0, JS final idêntico | Prévia, bloco recolhido, foco/aria, nome e confirmação | **25/25** | `dom.json`; fixture de HTML nativo renderizada na etapa 0.10.0 |
| T9 | Site-Teste, Meta 0.10.1 | Health, selftest, descoberta, docs e convivência | Saúde ok; **8/8** checks; **35** operações; **18** docs exatos | `site-final.json`, `mcp-discovery.json`, `mcp-documents.json` |

Na etapa 0.10.0 também passaram: 55 testes de credenciais, 27 de worker, 23 de health, 11 de corrupção e 104 de metadados no ambiente atual; 158 verificações no mínimo exato (41+55+25+26+11), além de preservação e integração. Essas execuções ficam em `evidence/0.10.0` e são identificadas como etapa anterior. O patch preserva seus arquivos funcionais; as repetições efetivas na 0.10.1 são as listadas acima. Não se somam repetições como se fossem casos independentes.

Observações preliminares e correções estão em `evidence/0.10.0/preliminary-observations.md`: colisão de janela no relógio do harness, expectativas antigas de versão/mensagem e contexto MCP do teste integrado foram ajustados. Um caso adicional identificou o código legado `not_configured` ao remover conexão durante a vida do job; corrigido antes do primeiro instalador compartilhado e coberto nas 41 verificações finais. MySQL local não iniciou; nenhuma prova funcional local de banco é alegada. Os testes de banco usaram o laboratório autorizado no host de teste.

**Documentação MCP:** `meta/documentation {}` fornece o índice; cada documento foi lido com `offset`, `limit_bytes=16384` e `expected_revision=sha256`, até `next_offset=null`. Na 0.10.1: **18 documentos, 144362 bytes UTF-8, 20 páginas mais 1 índice**, todos idênticos ao runtime final em bytes/hash/versão. `input-schemas.json` exigiu 3 páginas. A suíte nativa também verifica paginação curta, autorização e ausência de efeitos de negócio da leitura documental. Outras operações continuam com sua auditoria usual.

**Estado final:** Meta 0.10.1 ativo, `meta/health {}` com `state=ok`, `issues=[]`, armazenamento/cifra disponíveis, 0 conexões, 0 agendas ativas e 0 jobs ilegíveis; `meta/selftest {}` com `local_checks_ok=true`, `external_checks=not_run`. LinkedIn 0.10.1 responde normalmente. Pipedrive retorna a recusa administrativa esperada, com `registro_cliente=registrado` e `chamada_externa=false`. Acompanhantes preservados conforme seção 2; DreamHost Panel Login 1.0.0, WP Super Cache 3.1.4 e Yoast SEO 28.7 também permanecem ativos.

Laboratórios removidos: etapa 0.10.0, 87+14+14 tabelas próprias; etapa 0.10.1, 87+14. Em cada limpeza: 0 tabelas restantes, diretório e manifesto removidos. Controlador `meta-lab0101.php` excluído com guarda de hash, operação `87ec9297505985067fc96a91`, backup `92460edad496ca6b28fc7a3f`. Catálogo final sem ability de QA. A lista final de MU plugins contém somente os quatro arquivos de recuperação preexistentes. Backups/auditorias normais do MCP permanecem; nenhum segredo real foi usado nos testes.

## 5. Banco e volta de versão

Sem tabela, coluna ou migração de schema nova. `collection_failure` é um bucket adicional cifrado na tabela existente. As agendas recebem campos diagnósticos no payload cifrado. A option já existente `f3_meta_operation_notice` passa a guardar o mapa de incidentes ativos; formato anterior é aceito sem mapa. Conexão, nome e agendas continuam protegidos por revisão, travas e transação. A instalação no site compartilhado, sem conexões, não gravou dados de negócio de fornecedor.

A prova de atualização preservou exatamente as linhas/configurações semeadas; não é backup do site inteiro. Antes de voltar em ambiente com dados, preservar banco e salts, suspender o processamento durante a troca e conferir estado depois. O backup do uploader cobre arquivos; `database_effects_reversible=false` e `business_readiness_verified=false` foram reportados corretamente.

Voltar da 0.10.1 à 0.10.0 reintroduz a inconsistência documental. Voltar à 0.9.0 perde classificação de Stories, diagnóstico novo e deduplicação por incidente; não desfaz coletas, transações, auditoria, retenção ou e-mails já efetuados. Restaurar arquivos não restaura o banco. Não foi executado downgrade em produção; nenhum site de frota foi alterado.

## 6. O que permanece pendente

| Pendência / limite | Motivo e ação | Responsável |
|---|---|---|
| Homologação com credenciais Meta reais e duas identidades | Site-Teste terminou sem conexão. Provar a troca guiada e relatórios com ativos/escopos reais; os testes desta rodada interceptam HTTP. | Dono/operador com credenciais autorizadas e mantenedor Meta |
| Story real indisponível e token real revogado | Fixtures demonstram a classificação e supressão de aviso. A hipótese dos e-mails históricos não está confirmada sem códigos medidos; não revogar credencial compartilhada apenas para testar. | Dono/operador Meta |
| Entrega de e-mail ao admin_email | Testes contaram chamadas interceptadas. `accepted` significa aceitação por wp_mail; uma tentativa por incidente não garante entrega. | Administrador do WordPress/correio |
| Inspeção visual completa do painel em navegador | DOM comprova interação/foco/aria; não cobre layout visual real, leitor de tela ou todos os navegadores. | Homologador do painel |
| Pendências históricas da frota 20, 88 e demais aceites externos | A nova implementação não encerra os aceites reais já registrados, nem configura sites sem conexão. | Dono/orquestrador da frota |
| Fluxos comerciais completos dos acompanhantes | `nao-avaliado` nesta rodada além das fronteiras listadas. Sem risco concreto identificado que exija novo impacto. | Mantenedores dos respectivos pacotes |
| Publicação raw e implantação na frota | Não executadas; entrega dos três artefatos ao dono. Conferir hash antes de instalar, validar por site e manter regras de publicação vigentes. | Responsável pela frota |

Não há falha conhecida pendente nas verificações executadas do código final. Os limites acima não são convertidos em aceites concluídos.

## 7. Credenciais e configuração do dono

Não há credencial nova exigida pela 0.10.1. Tela: **Ferramentas → Fator3 MCP Meta → Conexão**. Campos existentes: nome, ID do aplicativo, chave secreta, token do usuário do sistema, validade, retenção e usuários autorizados; ativos Instagram profissional/Páginas são selecionados na aba Ativos. Valores secretos permanecem cifrados e não são preenchidos de volta no navegador.

As regras locais do pedido 15 permanecem: App ID de 15–17 dígitos, App Secret hexadecimal de 32 caracteres e token iniciado em EAA com pelo menos 100 caracteres. São política solicitada para este pacote, não regra universal de todos os tokens Meta. A mudança de política mencionada no Pedido Core 295 não foi transferida automaticamente ao Meta. Permissões de leitura orientadas no pacote: `pages_show_list`, `pages_read_engagement`, `read_insights`, `instagram_basic`, `instagram_manage_insights`; escopos extras são exibidos, sem revogação automática.

O dono deve preencher o par de app e token compatíveis, autorizar os ativos e validar os relatórios reais. A validação prévia existente consulta identidade/app/validade e ativos antes de persistir. Não revogar token compartilhado com o Site Core como parte da atualização. O novo `label` é dado não secreto e opcional na troca guiada; nome não informado preserva o salvo. Recarregar abas administrativas antigas para usar o JavaScript da versão corrente.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-meta-fator3-0.10.1-instalador.zip](wp-mcp-meta-fator3-0.10.1-instalador.zip) | 192114 | `f80d934fe1851bc887a0174190b42d73b36a8637f2f4824bdb5cfeb7a674ee95` |
| Fonte | [wp-mcp-meta-fator3-0.10.1-fonte.zip](wp-mcp-meta-fator3-0.10.1-fonte.zip) | 1476729 | `e333d22a82599e08c015002bb2ea6536a98ddacbfc68ede82a422733e135e908` |

Relatório: `wp-mcp-meta-fator3-0.10.1-relatorio.md`. Instalador com raiz `wp-mcp-meta-fator3/`, 45 arquivos, 23 PHP e 18 documentos. Fonte com raiz `wp-mcp-meta-fator3-0.10.1-fonte/`, código, runtime idêntico ao instalador, build, testes, evidências sanitizadas, entradas históricas e a cópia anterior ao fechamento deste relatório. Nenhum ZIP contém outro ZIP da entrega. Somente o instalador deve ser enviado ao WordPress.

São três artefatos principais. Não há relatório de impacto novo nesta rodada. O relatório externo é o canônico para a identidade final do fonte; diferenças de fechamento não alteram o instalador testado.
