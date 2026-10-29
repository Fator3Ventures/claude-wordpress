# Entrega — Fator3 MCP LinkedIn 0.13.0

Revisão: 1 · Data: 2026-10-29 · Fuso: America/Sao_Paulo · Rodada: implementação
Slug: `wp-mcp-linkedin-fator3` · Basename: `wp-mcp-linkedin-fator3/wp-mcp-linkedin-fator3.php` · Versão: `0.13.0`
Status: **com-pendencias** — implementação e testes do escopo aprovados; aceitação com token real válido depende do dono da conta.

**Relatório externo canônico.** A cópia interna foi incluída antes do fechamento do fonte. Este relatório registra sua identidade final; o ZIP fonte não foi reaberto ou alterado.

## 1. De onde esta versão entra

Atualização direta da **0.12.0**, sem versão intermediária, e instalação em WordPress limpo. Base aceita: `wp-mcp-linkedin-fator3-0.12.0-instalador.zip`, 304948 bytes, SHA-256 `19748e788190f371809db469a6de052a645e25f39fad1672606dc776234ec54c`; fonte-base de 1713239 bytes, SHA-256 `15c182cc89605cb1fc18121d8db81fd9008daa06cb787f7224a973d18f4f65d1`. Ambos preservados. A base também foi observada ativa no Site-Teste antes da troca.

Pedido específico: **Pedidos MCP LinkedIn 15**, em `Fator3 MCP LinkedIn(10).md`, 4429 bytes, SHA-256 `c15cd62f0d17eab2512f38b15a5e49b04515e7100379e4921308d8c83a467146`. Considerada a regra do dono de 28/10/2026 recebida na aba Core. A cópia dessa regra em `inputs/0.13.0/` é referência imutável, não edição da documentação central. Normas comuns revisão 5 de 23/10/2026, preservadas da base e corroboradas pelos relatórios novos, prevalecem sobre avulsos revisão 4.

A nova rodada incrementa minor: 0.12.0 → 0.13.0. Identidades públicas, namespace, provider, basename, prefixos, menu, Text Domain e Update URI permanecem. Cabeçalho conserva autor Fator3, licença GPL-2.0-or-later e mínimos WordPress 6.4/PHP 8.1.2, comprovados no laboratório. PHP precisa ser de 64 bits; criptografia autenticada e travas nomeadas do banco continuam obrigatórias. MySQL testado: 8.0.46.

## 2. Convivência e encaminhamentos

Foram considerados fonte, instalador e relatório novos de Core 1.60.0, MCP 0.36.0 e Meta 0.14.0, além de Google 0.22.0 e Pipedrive 0.3.0 identificados nas entregas. `inputs/0.13.0/packages.json` registra nomes recebidos, bytes e SHA-256. Os dez anexos desta rodada foram reconferidos sem alteração. As cinco árvores fonte recebidas e os cinco runtimes acompanhantes em cada laboratório integrado final permanecem idênticos aos ZIPs originais.

| Acompanhante | SHA-256 do instalador examinado | Prova e limite |
|---|---|---|
| Core 1.60.0 | `1dc4e94305ea55394024d6527bc06b46209f0ae51a55f734853763bcb232e27c` | Ativo nas matrizes integradas; adaptador, prévia, fila comercial, duas etapas, deduplicação e incerteza com fornecedor sintético. Ativo antes/depois no Site-Teste. |
| MCP 0.36.0 | `97648853e16d7c7fca811c6be22323244c5f2ebc3e296c22564ce7b2739cb98b` | Executor original: avisos, concessões, revogação, histórico, auditoria e documentação. Transporte remoto e instalação no Site-Teste. |
| Google 0.22.0 | `a84754409f89b7b9c7367c1d261c44ef93c2f6039b379c3ec5c6242ec7188ebd` | Convivência ativa local e remota, contratos preservados; nenhuma homologação nova das APIs Google. |
| Meta 0.14.0 | `43e8947ac0ffaf3da52c62b0515db826e6df266553d64f5561c0d3b87b7eb318` | Convivência ativa local e remota; nenhuma homologação nova das APIs Meta. |
| Pipedrive 0.3.0 | `30fc784a552a89351900c169fad7300759163fb886b842f45ba807bb0977f657` | Instalado, mas não ativado localmente: exige PHP 8.3.36 e o laboratório integrado usa 8.3.6. Observado ativo no Site-Teste; API Pipedrive não testada. |

Somente o LinkedIn foi modificado e instalado. Não foram atualizados código ou documentos de Core, MCP, Google, Meta ou Pipedrive. As cópias recebidas servem de insumo. Evidências: `companion-integrity.json`, `received-source-integrity.json` e `site-test.json` em `evidence/release0130/`.

**Impactos e pedidos emitidos nesta rodada:** nenhum. A análise no planejamento examinou credenciais, envelope de resultados, autorização, transporte MCP, auditoria central e contratos de aquisição/etapas. Avisos são aditivos no envelope existente; nenhum acompanhante exige mudança nova de contrato, configuração ou ordem de instalação. Não há documento de impacto apenas para anunciar versão ou encerramento.

**Tratamento de impactos anteriores:** `wp-mcp-linkedin-fator3-0.12.0-impacto-wp-mcp-fator3.md`, revisão 1, SHA-256 `ea8cc39c32dc65ab2b7a3443ed0d3680195ccab869737db3b6de34a3f9c9b843`, emitido pelo LinkedIn ao mantenedor MCP, relativo ao Pedido Core 323 e ao consumidor comercial `site-core-quality`. O documento recebido informa atendimento no MCP 0.35.0. Nesta rodada, prova própria com MCP 0.36.0 original e Core 1.60.0 confirmou recibos `central_audit=recorded`, aquisição preservada, introspecção válida e controles de identidade, concessão, revogação e replay. `clean/stages012.json` e `upgrade/stages012.json` registram 24 verificações por matriz; `mcp-stages012.json`, cinco por matriz. O impedimento de auditoria central está atendido na combinação testada; não equivale a provar conversões comerciais reais no fornecedor. O impacto original fica preservado como histórico e não é reemitido. Não há reenvio retroativo de eventos por este encerramento.

O relatório Google 0.22.0 tinha referência a ajuste do Core posteriormente incorporado na 1.59.0; o Core examinado é 1.60.0. Essa pendência antiga não é transferida como bloqueio novo do LinkedIn. Pendências de conta real informadas pela frota seguem na seção 6.

## 3. Mudanças e evidência

| Pedido/evidência | Problema confirmado na base | Implementação e resultado |
|---|---|---|
| Pedidos MCP LinkedIn 15 — espaços externos | Access Token, Primary Client Secret e Refresh Token com espaço eram recusados antes do HTTP. | Normalização de espaços Unicode da categoria Zs nas pontas dos quatro campos manuais, incluindo Client ID; aviso `credential_spaces_trimmed`, antes da introspecção. O sucesso persiste o valor aparado. |
| Pedidos MCP LinkedIn 15 — espaços internos | A validação misturava espaço comum com controle. | Preserva espaços internos e gera `credential_internal_spaces`. A decisão remota, identidade, app, escopos e expiração continuam sendo conferidos. |
| Regra do dono de 28/10/2026 — demais formatos | A afirmação do pedido de que não havia outros validadores não correspondia ao código: `ConnectionChanges::formats` também recusava token curto, Client ID numérico/não alfanumérico, segredo atípico/cruzado e refresh igual ao access. | Heurísticas de credenciais manuais passam a avisos com campo, código e motivo. Application ID é identificador de ativo e conserva validação numérica. Não foi alterado o documento recebido para esconder a divergência. |
| Segurança e atomicidade | Remover todos os bloqueios locais permitiria entradas inseguras e perda de credencial salva. | Controles Unicode Cc, UTF-8 inválido, tipos não textuais, entradas só com espaços e tamanho bruto acima do limite continuam recusados. Campos obrigatórios, endpoints permitidos, permissão administrativa, CAS, travas e transação preservados. Recusa remota não altera o registro salvo. |
| Aviso compreensível na tela e na API | O usuário precisava receber a razão por campo mesmo quando o fornecedor recusasse o candidato. | `data.warnings` em sucesso/prévia e `details.warnings` em erro; interface mostra aviso junto ao campo, inclusive após limpar senha salva. Editar o campo limpa aviso obsoleto. Avisos não contêm valor, fragmento, hash nem comprimento da credencial. |

Arquivos funcionais alterados: `build/common/Connections.php`, `build/linkedin/ConnectionChanges.php`, `build/linkedin/FieldHelp.php` e `build/assets/admin.js`, além de versão e documentação própria. `Connections::save` acumula avisos e encapsula a rotina de gravação; normalização ocorre dentro da proteção existente, inclusive para candidato OAuth pendente. Entrada aparada dispara nova introspecção mesmo quando resulta no mesmo token já salvo. Identidade diferente continua exigindo prévia/confirmação válida, sem perder CAS ou rebase de agendas e concessões.

Limites são verificados em **bytes brutos antes de aparar**: 16384 para token/segredos e 160 para Client ID. Senha exatamente vazia conserva a credencial existente; entrada só com espaços é inválida; remoção usa os controles explícitos já existentes. Não se declara que a introspecção do Access Token validou o Refresh Token: o refresh manual continua sem vínculo verificado até uso legítimo no fluxo de renovação. O validador estrutural das respostas emitidas pelo fornecedor em OAuth permanece no escopo anterior.

O instalador contém 72 arquivos, 33 PHP e 32 documentos. Comparação contra 0.12.0: 25 arquivos novos/alterados, incluindo a nova nota `RELEASE-0.13.0.md`; a lista e o diff completos estão em `runtime-changes.json` e `runtime-0120-0130.diff`. Os 93 schemas de entrada e o schema de saída são byte a byte idênticos aos da base. Não há nova tabela, migração, ability, dependência obrigatória, mudança de retenção ou habilitação automática de fluxo.

## 4. Instalação e prova da troca

O instalador final foi reconstruído com bytes idênticos ao artefato das quatro matrizes (`build-reproduction.json`). A prova de sintaxe aprovou os 33 PHP em PHP 8.1 e 8.3 e `node --check` no JavaScript administrativo. Os cinco testes de reprodução sobre a 0.12.0 confirmam a recusa antiga antes do fornecedor; não são contados como testes da versão nova.

| Matriz final | Ambiente | Total funcional | Aprovados | Não aplicáveis | Falhas |
|---|---|---:|---:|---:|---:|
| Limpa integrada | WP 7.1.3, PHP 8.3.6, MySQL 8.0.46 | 328 | 327 | 1 | 0 |
| Atualização direta 0.12.0 → 0.13.0 | WP 7.1.3, PHP 8.3.6, MySQL 8.0.46 | 338 | 337 | 1 | 0 |
| Mínimos, LinkedIn independente | WP 6.4, PHP 8.1.2-1ubuntu2.28, MySQL 8.0.46 | 299 | 295 | 4 | 0 |
| Atual, LinkedIn independente | WP 7.1.3, PHP 8.3.6, MySQL 8.0.46 | 299 | 297 | 2 | 0 |
| **Total de execuções** | **WordPress real, fornecedor sintético** | **1264** | **1256** | **8** | **0** |

Adicionalmente: **66 verificações documentais locais** (32 documentos/40 páginas por matriz integrada mais a prova de não chamar fornecedor), **30 verificações DOM** com jsdom 27.4.0 sobre HTML/JavaScript reais e REST autenticado, e **9 autotestes no Site-Teste**. Não são testes visuais de navegador nem 1256 requisitos distintos. Os casos não aplicáveis são a fixture de upgrade 0.10.1 fora da base atual, fronteiras integradas ausentes no modo independente e Abilities API ausente no WordPress mínimo; a atualização atual tem dez provas próprias em `upgrade0130.json`.

As 70 verificações de `request015.php` por matriz cobrem os quatro campos, espaços externos/internos, controles, UTF-8/tipos/limites, heurísticas, recusa remota e conservação de dados, reintrospecção, confirmação de identidade, semântica vazio/remover, permissões e avisos sem segredos. Os cinco testes MCP específicos por matriz integrada comprovam normalização, transporte dos avisos, recusa sem mutação e revogação. Regressão inclui credenciais cifradas, migração, concorrência com conexão SQL independente, agendas, histórico, exportações, grants e conversões comerciais/aquisição com HTTP sintético. Não há novas entradas de warning/deprecation/fatal nos logs finais de nenhum pacote.

Tentativas preliminares não entram no total: corrigiu-se o seed de concessão comercial para incluir `grant_key` antes de validar a base; a matriz atual usa testes de preservação próprios em vez de supor origem histórica 0.7/0.8; e a espera DOM foi corrigida para não confundir a mensagem de um save anterior. As matrizes afetadas foram executadas novamente, integralmente, sobre o instalador final. Essas ocorrências estão em `preliminary-observations.json`; não foram bugs novos do runtime. O metadado literal `MCP 0.33.0` de `mcp-history011.json` é rótulo legado do teste: `environment.json` e `companion-integrity.json` comprovam o MCP 0.36.0 original usado. A evidência original foi preservada, sem reescrever resultado de teste.

**Site-Teste:** `https://fator3-teste-mcp-1.dreamhosters.com/`, via **WP MCP fator3-teste**, somente com abilities existentes. Troca serializada pela ability `plugins/upload-base64`, `activate=true`, `overwrite=true`, `expected_slug=wp-mcp-linkedin-fator3` e SHA-256 da seção 8. Idempotência `linkedin-0130-1c45738322f4-20261029`. Recibo: `applied=true`, 0.12.0 → 0.13.0, ativo antes/depois; operação `37853f2e7d817b2e35fe17d240a4f4f6`, backup `09674b9c36f42b9da794e8d0`. O hash recebido coincide com o instalador testado.

Home e `/wp-json/` retornaram 200 antes e depois. O instalador confirmou novo processo PHP e worker independente, com reativação silenciosa. A prova é `internal_same_origin`, com nonce novo e bypass de cache; não prova acesso externo geral, cache público ou prontidão comercial. Não houve ciclo completo de hook de ativação remoto; instalação limpa foi provada localmente. Nenhuma URL raw nova foi publicada: publicação na frota cabe ao dono/frota, com `expected_slug` e hash desta entrega.

`linkedin/status` retornou 0.13.0, `state=ok`, armazenamento/criptografia prontos, sem issues, zero conexões, zero agendas ativas, zero jobs ilegíveis e migração concluída. `linkedin/self-test` retornou nove checks `ok`, `external_checks=not_run`, `remote_homologated=false`. Listagem antes/depois preservou os outros oito plugins, suas versões e estado ativo, incluindo Core/MCP/Google/Meta/Pipedrive, DreamHost 1.0.0, Super Cache 3.1.4 e Yoast 28.8.

**Prova remota específica do pedido:** o mesmo candidato sintético com espaço final, em `dry_run=true`, retornou `invalid_input` na 0.12.0. Na 0.13.0 alcançou a introspecção real do LinkedIn e retornou `oauth_rejected`, HTTP 400, mantendo `credential_spaces_trimmed` no erro MCP. Nenhuma conexão foi criada. Isso comprova a remoção do bloqueio indevido e a comunicação do aviso, mas não satisfaz sozinho a gravação de um token real válido. Gravação aparada após resposta válida foi comprovada localmente com fornecedor sintético.

**Documentação instalada:** índice `linkedin/documentation` e leitura de todos os 32 documentos, com `expected_revision`, `offset`, `limit_bytes=65536` e continuação até `next_offset=null`. Foram lidas **34 páginas, 281811 bytes**, comparados integralmente contra os documentos do instalador. Todos os hashes coincidem; `input-schemas.json` exigiu três páginas. Evidência por documento, bytes, SHA-256 e request IDs: `site-docs.json`. A leitura usa os arquivos locais e não consulta o LinkedIn.

**Estado final:** LinkedIn 0.13.0 ativo e saudável no Site-Teste; nenhuma conexão ou agenda sintética persistida; nenhum helper/MU plugin de QA enviado ao servidor. Bancos locais de laboratório são descartáveis e não integram a entrega. Operações de publicação social, gasto Ads, envio comercial, assinatura real, envio de mensagens e distribuição nos outros sites não foram executadas.

## 5. Banco e volta de versão

Não há migração nova nem reescrita em massa de credenciais. Na atualização direta, dez provas verificaram todos os registros e históricos byte a byte, incluindo ciphertexts, retenção finita, conexão, referência de aquisição, concessão comercial e diários confirmado/incerto de aquisição e etapas. A validade da fixture foi conferida na base 0.12.0 antes da troca. A limpeza posterior das concessões sintéticas é exclusiva do laboratório para isolar os testes seguintes; não é comportamento de produção.

A gravação explícita de credencial continua cifrada, sob trava, revisão esperada e transação, depois da comprovação remota aplicável. Avisos são metadados de resposta; não criam registros paralelos com segredos. Falhas locais/remotas e conflitos preservam o estado anterior.

Para voltar os arquivos, usar o instalador íntegro 0.12.0 ou o backup de arquivos da operação, preservando banco, salts/chaves e diários. O recibo de instalação informa `database_effects_reversible=false`: restaurar arquivos não desfaz alterações posteriores no banco. A versão antiga volta a aplicar os bloqueios de formato antigos em entradas futuras. Reversão efetiva após novos dados não foi executada nesta rodada; não apagar diários nem reenviar conversão para tentar compensar auditoria.

## 6. O que permanece pendente

| Pendência | Motivo/limite | Responsável e aceite |
|---|---|---|
| Aceite completo do Pedido MCP LinkedIn 15 com token real no Site-Teste | Não havia conexão nem credencial real válida disponível. O preflight real foi recusado pelo fornecedor; o sucesso local é sintético. | Dono da conta/frota: colar token válido com espaço final, conferir aviso, introspecção bem-sucedida e persistência aparada, sem expor segredo. |
| Operações reais de gestão, conversão de contato/etapa, Lead Sync e acervo com dados reais | Pendências 20, 92 e 116 citadas no estado recebido da frota. A regra Insight Tag mencionada não substitui regra com fonte Conversions API; faltam permissões/ativos apropriados. | Dono/frota e responsáveis das integrações: homologar com contas e efeitos autorizados. Esta entrega não encerra essas pendências. |
| Inspeção visual em navegador | Cobertura da tela foi DOM/REST autenticado, sem inspeção visual manual. | Dono/revisor: conferir avisos junto aos campos no navegador de uso. |
| Integração nativa Pipedrive 0.3.0 em runtime compatível | Pacote ficou inativo localmente por mínimo PHP 8.3.36; o fluxo comercial Core→LinkedIn foi testado com entradas sintéticas. | Responsável Pipedrive/Core: homologação nativa e conta real, se necessária ao aceite de frota. |
| Publicação/distribuição e verificação externa | Instalação limitada ao Site-Teste; não houve push nem validação de cache público/acesso externo geral. | Dono/frota: publicar instalador e relatório, conferir hashes, distribuir conforme sua autorização. Fonte permanece com o dono até decisão 89. |

Não foram encontradas regressões ou novos impactos no escopo executado; essa conclusão não cobre as lacunas acima. A revisão do documento de pedidos permanece com seu mantenedor; o item 15 não é marcado como homologado remotamente antes do aceite real.

## 7. Credenciais e configuração do dono

Tela: **Ferramentas → Fator3 MCP LinkedIn → Conexões**. Campos manuais: Access Token, Client ID, Primary Client Secret e Refresh Token opcional. O dono obtém os dados em LinkedIn Developers, aplicativo correto, Auth/Application credentials, com produtos e permissões aprovados. Application ID, contas, Páginas, formulários e regras de conversão continuam identificadores de ativos separados. Ajuda de cada campo foi atualizada no próprio LinkedIn.

Colar token/segredo exatamente vazio em conexão existente preserva o salvo; usar a opção explícita para remover. Espaços externos são aparados com aviso; internos ficam no valor e geram aviso; tabulação, quebra de linha e outros controles são recusados. Os limites são 16384 bytes para segredos e 160 para Client ID, antes da normalização. Heurística de formato não constitui comprovação de validade.

Introspecção determina atividade, aplicação, escopos e vencimento do Access Token; troca de identidade continua sujeita à confirmação. Refresh Token manual não é validado pela introspecção do Access Token e conserva a proteção de vínculo. Conversions API exige escopos e regra API próprios; avisos não concedem permissão nem habilitam fluxo. `manage_options` ou o gate administrativo existente continua obrigatório na tela, REST e MCP. Nenhum valor secreto integra este relatório.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `wp-mcp-linkedin-fator3-0.13.0-instalador.zip` | 314596 | `1c45738322f4901aeacdc36615789ae961e8b9d521ba321a27de0aea76c13502` |
| Fonte | `wp-mcp-linkedin-fator3-0.13.0-fonte.zip` | 2038497 | `9eab181f679458b9fc27ae2d93144a800d63a1f0e8aa0760eae4ec2d35135760` |

Relatório principal: `wp-mcp-linkedin-fator3-0.13.0-relatorio.md`. São três artefatos nesta rodada; nenhum impacto novo é emitido. O instalador é o único ZIP instalável, com raiz `wp-mcp-linkedin-fator3/`. Fonte com raiz `wp-mcp-linkedin-fator3-0.13.0-fonte/`, código, build, testes, evidências sanitizadas e a cópia interna anterior ao fechamento, sem ZIPs aninhados, dependências externas, banco, cookies ou logs privados. `plugin/` deve coincidir byte a byte com o instalador. O fechamento do fonte é único; sua identidade final foi preenchida somente neste relatório externo.
