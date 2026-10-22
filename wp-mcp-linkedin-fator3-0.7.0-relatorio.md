# Entrega — Fator3 MCP LinkedIn 0.7.0

Revisão 1 · 22/10/2026 · America/Sao_Paulo · Rodada de implementação · **com-pendencias**.

**Relatório externo canônico.** Fonte fechado uma única vez; a cópia interna é identificada como anterior ao fechamento e omite somente a identidade circular do próprio ZIP. Esta revisão informa os bytes e SHA-256 finais sem alterar o arquivo fonte.

A 0.7.0 implementa a parte do LinkedIn no registro de conversões executadas por serviço: identidade opaca, descritor e introspector PHP, evento local e leitura administrativa protegida. Está instalada e validada no Site-Teste. O **MCP 0.27.0 ainda não implementa o consumidor central**; por isso Pedidos MCP LinkedIn 8(d) permanece aberto para confirmação do detalhamento proposto, implementação do canal e aceite conjunto. Código de domínio entregue não equivale a registro central de serviço disponível.

## 1. Bases aceitas e identidade

Instalação nova em WordPress e atualização direta **0.6.0 → 0.7.0**, sem intermediária. Base aceita: entrega anterior desta tarefa, confirmada pela aba recebida `Fator3 MCP LinkedIn(6).md`, que registra a 0.6.0 nos 12 sites. A 0.6.0 original foi preservada sem alteração:

| Base | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-linkedin-fator3-0.6.0-instalador.zip | 189130 | edfed426b2e0e4fce14a5c5c6241b12bed25186ab1da2102da96b2032a8af45e |
| wp-mcp-linkedin-fator3-0.6.0-fonte.zip | 517114 | 466381c50c8b00599e00d24eec36b2f6df61d88257c24fbb3f8438585acb0a96 |

Preservados nome Fator3 MCP LinkedIn, slug/pasta/provider `wp-mcp-linkedin-fator3`, basename `wp-mcp-linkedin-fator3/wp-mcp-linkedin-fator3.php`, Text Domain, Update URI, namespaces, opções, tabelas e operações existentes. Incremento minor conforme as normas revisão 4. A nova ability soma-se às 79 existentes, sem renomeá-las.

Runtime testado: WordPress **7.1.3**, PHP **8.3.6** de 64 bits, MySQL **8.0.46**, em laboratório nativo descartável; WordPress **7.1.3/PHP 8.3.36** no Site-Teste. Os mínimos herdados WordPress 6.4/PHP 8.1.2 continuam no cabeçalho, mas **não foram exercitados nesta rodada e não constituem suporte comprovado por esta entrega**.

Referências atuais constam de `inputs/manifest.json`: instruções comuns e padrão revisão 4, aba de pedidos atual, MCP 0.27.0 fonte/instalador/relatório e impacto para LinkedIn revisão 2, base 0.6.0 e acompanhantes recebidos. Anexos de versões anteriores foram mantidos como histórico, sem substituir os pedidos atuais. Nenhuma aba central de governança foi alterada.

## 2. Convivência e encaminhamento

| Pacote | Laboratório de atualização | Site-Teste ao instalar e ao encerrar |
|---|---|---|
| Fator3 Site Core | 1.47.0 | 1.47.0 |
| Fator3 MCP | 0.27.0 | 0.27.0 |
| Fator3 MCP Google | 0.17.0 | 0.17.0 |
| Fator3 MCP Meta | 0.4.1, pacote recebido | 0.5.0, versão observada no site |
| Fator3 MCP LinkedIn | 0.6.0 → 0.7.0 | 0.6.0 → 0.7.0 |

O Meta era 0.4.1 na primeira leitura e já estava em 0.5.0 na reconferência imediatamente anterior à instalação do LinkedIn. Sua atualização ocorreu por outra atividade e foi preservada. Não se atribui a esta rodada o build ou a homologação completa do Meta 0.5.0. A prova compartilhada comprova a convivência observada, enquanto o laboratório usa os bytes recebidos de Meta 0.4.1.

MCP 0.27.0 recebido: instalador de 846316 bytes, SHA-256 `fcf5ad0099b9490abfb8e9ea6ef83c769cad053e2ee75712efce50e219f62bc1`; fonte de 3376082 bytes, SHA-256 `c541e4cbe93b9fbef6608cf048fcb6abce69e844c32da0d6adba23af130d743d`. Relatório, impacto e inspeção de código confirmam que `mutation-service-audit/1.0.0` é proposta sem consumidor implementado nessa versão.

Único impacto técnico novo: **`wp-mcp-linkedin-fator3-0.7.0-impacto-wp-mcp-fator3.md`**, revisão 3, etapa entrega, situação `aberto`, classificações `acao-necessaria` e `validacao-coordenada`, vinculado a Pedidos MCP LinkedIn 8(d) e Pedidos MCP 65. Foi preparado no planejamento, atualizado na implementação e fechado documentalmente com esta entrega. Descreve o handshake/recibo proposto e os critérios de aceite; não houve confirmação do destinatário nesta rodada.

Core conserva `site-conversion-delivery/1.0.0` e seu consumidor `site-core-conversions`; não recebe obrigação de emitir auditoria, assumir usuário ou mudar fila/payload. Não há alteração nova de contrato com Google, Meta ou Implantador. A decisão anterior sobre Insight Tag/regra API segue com dono/Core, sem novo impacto meramente informativo. Apenas LinkedIn foi atualizado por esta tarefa; nenhum pacote alheio, repositório ou site da frota foi modificado/publicado por esta entrega.

## 3. Mudanças por pedido e evidência

### Pedidos MCP LinkedIn 8(d) — implementado no domínio; aceite central pendente

Antes, o despacho SDK de serviço ficava somente no diário local, sem interface de serviço que permitisse validação e leitura pelo futuro Registro. Agora o domínio fornece:

- `f3_linkedin_service_audit_descriptor(): array`, PHP local, com seis campos fechados: contrato `mutation-service-audit/1.0.0`, provider, contrato de evento `linkedin-service-mutation/1.0.0`, hook `f3_linkedin_service_mutation_recorded`, reader `linkedin/get-service-write-operation` e introspector `f3_linkedin_introspect_service_grant`.
- `f3_linkedin_introspect_service_grant(array $identity): array`, somente PHP local, utilizável como usuário zero, sem rede nem gravação. Valida o diário, identidade, concessão e revisão atuais, autoridade do administrador concedente/perfil MCP original, conexão/ativo/regra API e prova local de escopos `rw_conversions` e `r_ads`. Devolve projeção técnica do evento e hash, ou recusa simbólica sem dados da conta.
- `linkedin/get-service-write-operation`, leitura administrativa com esquema fechado de cinco campos: provider, consumer_id, principal_ref, grant_revision e operation_id. Exige `manage_options`, propriedade vigente da concessão, ativo e perfil MCP permitidos. Outro administrador não herda acesso por conhecer a referência. Rota administrativa correspondente: `/wp-json/f3-linkedin/v1/get-service-write-operation`.
- Identidade de serviço opaca por HMAC, com separação de domínio/site/consumidor/destino; revisão vinculada à concessão persistida. É congelada em `conversion_event.service_identity` antes do POST e revalidada no preflight. SDK continua sendo serviço com usuário zero ou incidental; não emite evento humano usando identidade inventada.
- Evento local de dez campos após persistir o resultado: contrato, provider, operação/estado, hashes técnicos antes/depois, consumidor, principal e revisão opacos. Sem snapshot, payload, dado de contato, hash de e-mail, click ID ou segredo no evento. Leitor mostra somente estado e recibo técnico; `after=null` representa incerteza.
- `service_audit` em `linkedin/status` e `linkedin/capabilities`: separa implementação do domínio, registro do provedor e confirmação de cada evento. Falha de auditoria não transforma entrega confirmada em permissão para reenviar conversão.

Revogação, mudança de concessão/revisão/ativo ou perda de autorização bloqueia detalhes sem apagar o diário. Reconfirmar a concessão invalida referências da revisão anterior mesmo com destino igual. Leituras não consultam o LinkedIn: revogação remota só é conhecida depois de observada por introspecção/alteração local. Sem prova local válida, a interface recusa.

Replay confirmado/incerto não repete POST nem evento. Nova tentativa após recusa comprovada pode atualizar a mesma referência, sob os controles existentes. Não há backfill, outbox, importação ou reemissão automática de históricos. Diários 0.6.0 sem vínculo permanecem preservados e não recebem identidade nova silenciosamente. O leitor humano existente mantém seu contrato e delega os novos diários de serviço à proteção específica.

**Contraproposta concreta ao MCP:** bootstrap local chama `f3_mcp_register_mutation_service_audit` com contrato e dois callables de registro/consulta; descritor não transporta callbacks pela rede. O LinkedIn só anuncia `central_audit=recorded` quando o consumidor admitido confirma a persistência do hash exato do evento. O handshake e recibo estão implementados na metade LinkedIn e documentados em `docs/SERVICE-AUDIT.md`, mas continuam sujeitos à confirmação/adaptação pelo responsável MCP. O consumidor de teste `ServiceAuditContractFixture` existe somente no laboratório.

| Dimensão | Resultado |
|---|---|
| Interfaces, identidade e evento do domínio | implementado; validado-localmente; validado-wordpress |
| Registro/recibo com consumidor central simulado | validado-localmente; não é implementação MCP |
| Ausência real do consumidor no MCP 0.27.0 | validado-wordpress; `central_registered=false`, `service_principal_unsupported` |
| Registro central humano com antes/depois | regressão validada no Site-Teste, via ability MCP e rota administrativa |
| Registro central real com principal de serviço | pendente do responsável MCP e aceite conjunto |
| Conversão entregue/contada pelo LinkedIn real | pendente; não exercitada nesta rodada |

### Itens já aceitos na aba recebida

8(a,b,c,e), 9, 10 e 11 permanecem aceitos conforme o documento atual. A aba registra seguidores 14 na Página CTO Office e 9831 na Página fator3, iguais às telas às 18:43 −03 de 22/10/2026; isso é **evidência recebida**, não nova consulta realizada nesta rodada. O descritor humano, enum de seguidores, ajuda de campos, CAPI, permissões e deduplicação passaram por regressões pertinentes. Não se reabre o aceite anterior nem se apresenta teste simulado como nova homologação externa.

## 4. Instalação, provas e estado final

O instalador final tem **207524 bytes**, SHA-256 **`85b1cc8d16ab972e9acc2ad90bf81f0806b30a66e0833be311e33bf4a6b1d515`**. Os mesmos bytes foram usados em ambas as matrizes locais e no Site-Teste. Reconstrução posterior produziu ZIP byte a byte idêntico; fonte/runtime e manifesto foram conferidos. Sintaxe dos 26 arquivos PHP aprovada; 53 arquivos de runtime, incluindo 21 documentos. O instalador não contém QA, testes, fonte de desenvolvimento ou outro ZIP.

| Prova | Ambiente e limite | Resultado |
|---|---|---|
| Instalação limpa | WordPress nativo, somente LinkedIn, rede/e-mail interceptados | 105 verificações, zero falhas |
| Atualização direta | Base 0.6.0, acompanhantes da matriz local | 139 verificações, zero falhas |
| Cenários Site-Teste | WordPress real, provedor simulado, MCP real sem consumidor de serviço | 18 verificações aprovadas; 3 POST sintéticos; zero chamadas reais ao fornecedor |
| Autoteste instalado | `linkedin/selftest`, testes locais | 8 verificações aprovadas; externo não executado |
| Catálogo e documentação | Descoberta/esquema/leitura via MCP 0.27.0 | 80 abilities; 21 documentos, 22 páginas, bytes/hashes idênticos ao instalador |

As contagens de cenários têm regressões comuns e **não são casos únicos somáveis**. A matriz de atualização inclui preservação exata de concessão CAPI, prova de token, prévia e diário 0.6.0, antes das mutações de QA. As 19 verificações novas da release incluem recusas de editor/usuário zero no leitor, outro administrador/perfil, identidade falsa/campos extras/diário humano, escopo ausente/expiração/revogação, alteração de revisão durante preflight, troca de ativo, replay confirmado/incerto e falhas/recibos divergentes do central simulado. Introspecção e leitura foram observadas sem HTTP nem escritas SQL.

Instalação autorizada em `https://fator3-teste-mcp-1.dreamhosters.com/` via `plugins/upload-base64`, com `expected_slug=wp-mcp-linkedin-fator3` e `expected_sha256` acima, substituindo somente seu pacote. Operação **`319535c63509678fa12ba912`**, pacote `b8239e74957322a1b0602ce784f73232`, backup da 0.6.0 **`f34fbc0e5945e69f2f079813`**. Resultado `applied=true`, plugin ativo antes/depois, reativação silenciosa em nova requisição PHP. Página `/` e `/wp-json/` passaram com HTTP 200 antes/depois e sondas sem cache. O resultado não certifica prontidão comercial: `business_readiness_verified=false`, corretamente.

`tools/site-qa-070.php` foi instalado temporariamente apenas nesse ambiente, com configuração LinkedIn inicialmente vazia. Exigiu administrador, interceptou rede/e-mail e removeu seus dados próprios ao encerrar. A exclusão do arquivo ocorreu na operação **`d206afd8d2d72f4e4b4a15b3`**, backup `1d87cd2bd4f57c16fac58222`; sondas posteriores aprovadas e descoberta `linkedin-qa/` com **zero operações**. Configurações/conexões sintéticas remanescentes: zero. Referências centrais humanas sintéticas e backups do MCP permanecem como evidência de auditoria; nenhum simulador de consumidor central foi instalado no site.

Estado final: LinkedIn 0.7.0 ativo, armazenamento/criptografia prontos, auditoria local `ok`, `system/health.healthy=true`, oito autotestes locais aprovados e zero conexões. Descritor humano registrado pelo MCP sem erros. `service_audit.domain_implemented=true`, `central_registered=false`. Manutenção de credenciais preservada, `next_maintenance=1792710184`; sem coleta agendada (`cron.next=null`). Isso não prova execução futura de cron nem autorização externa.

Todos os documentos foram recuperados com revisão esperada, incluindo as duas páginas de `input-schemas.json`, concatenados sem separadores e comparados ao instalador. Evidências completas sanitizadas: `evidence/clean`, `evidence/upgrade`, `evidence/site-teste-070.json`, `evidence/mcp-documentation-070.json`, `evidence/package-review-070.json` e `evidence/log-review-070.json` no fonte.

Não houve mudança de fluxo visual ou JavaScript; regressões HTML passaram, e navegador não foi repetido nesta release. Testes da base em Chromium não entram nas contagens atuais. Logs finais não mostraram fatal/warning/deprecation ou erro LinkedIn; o laboratório integrado registrou três notices de tradução antecipada do domínio `f3base`, sem falhar testes. Isso não foi corrigido em pacote alheio nem tratado como nova regressão LinkedIn. Não foi feita revisão integral dos logs privados do site.

## 5. Banco, preservação e reversão

Schema SQL permanece **1**. Não há tabela, migração, concessão, credencial, agenda, cron ou fila novos. Há metadados aditivos de serviço no diário das novas conversões; a mesma retenção existente continua aplicável. Configuração, ciphertexts, concessões, comprovantes, progresso e diários anteriores são preservados, com prova de atualização direta. Nenhuma conta foi selecionada ou autorizada automaticamente.

Backup do MCP protege os arquivos da 0.6.0, não reverte banco nem efeitos externos (`database_effects_reversible=false`). Antes de eventual rollback, preservar banco e salts do WordPress junto das credenciais cifradas. Voltar aos arquivos 0.6.0 remove as novas interfaces/eventos e conserva o diário; leitores de um futuro central devem falhar fechados quando a interface não existir. O contrato de serviço não foi homologado sob downgrade. Reverter código ou excluir metadados não desfaz uma conversão já entregue e não autoriza reenvio. Não usar desinstalação para simular rollback.

## 6. Pendências, responsáveis e limites

| Pendência | Responsável e próximo aceite |
|---|---|
| Pedidos MCP LinkedIn 8(d) / Pedidos MCP 65 | Mantenedor MCP confirma/adapta handshake/recibo, implementa consumidor e Registro/leitor central com gates. Depois, validação conjunta no Site-Teste: envio simulado do adaptador real como usuário zero/incidental gera referência de serviço; leitura antes/depois autorizada; revogação/perfil nega sem apagar referência; replay/incerteza não repete envio. |
| Conversão real e produto/escopos | Dono/LinkedIn/Core, pendências 20/92 da frota: credencial e regra API autorizadas, conversão entregue e contada. Nenhuma credencial nem envio real foi usado nesta rodada. |
| Conexão nova pela tela e segredo incorreto | Dono, aceite manual externo ainda pendente nas referências 20/92; automação/rota interna não substitui esse aceite. |
| Regra 31692506 e separação Insight Tag/API | Dono/Core, pendência 116: decidir IDs/fontes. Regra de Insight Tag não é aceita como regra CONVERSIONS_API; nenhuma decisão foi tomada pelo mantenedor LinkedIn nesta rodada. |
| Mínimos de runtime | Mantenedor LinkedIn: matriz WordPress 6.4/PHP 8.1.2 não executada; versão testada é a informada na seção 1. |
| Publicação e frota | Dono/frota: distribuir os bytes com verificação de hash. Demais sites não atualizados por esta tarefa; fonte fica com o dono conforme decisão 89. |

O domínio está apto ao escopo comprovado, mas o pedido de Registro central de serviço não está encerrado. Ausência do consumidor no MCP não bloqueia instalação nem as funções existentes; continua explicitamente diagnosticada. Implementação completa de acompanhantes, UI autenticada atual do fornecedor e novas permissões remotas não foram avaliadas como parte desta release.

## 7. Credenciais e configuração

Sem campo secreto novo. Ferramentas → Fator3 MCP LinkedIn, aba Conexão: Access Token, Client ID, Primary Client Secret e, quando autorizado pelo produto, Refresh Token/validade. Token manual continua padrão; autorização OAuth pelo navegador é opcional. Credenciais reais não acompanham artefatos, evidências ou respostas de configuração.

Para CAPI, selecionar conta Ads, comprovar `rw_conversions` e `r_ads` por introspecção e usar regra ativa da conta com `conversionMethod=CONVERSIONS_API`. Concessão específica de `site-core-conversions` é explícita, administrativa e separada do Lead Sync. O dono decide/preenche seus ativos e autoriza uso real; a atualização não concede acesso. O novo leitor exige a concessão e sua revisão vigentes. Documentação instalada `CONVERSIONS.md`, `CREDENTIALS.md`, `FIELD-HELP.md` e `SERVICE-AUDIT.md` contém passos, erros, exemplos e limites sem valores secretos.

## 8. Arquivos finais e integridade

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-linkedin-fator3-0.7.0-instalador.zip | 207524 | 85b1cc8d16ab972e9acc2ad90bf81f0806b30a66e0833be311e33bf4a6b1d515 |
| wp-mcp-linkedin-fator3-0.7.0-fonte.zip | 583713 | 070dc8488219a5282036e8bb6a077a62c845f97d5f37e0d83ce5a1a36e3fcdde |

Artefatos da rodada:

- [wp-mcp-linkedin-fator3-0.7.0-instalador.zip](wp-mcp-linkedin-fator3-0.7.0-instalador.zip), único ZIP instalável, raiz estável `wp-mcp-linkedin-fator3/`.
- [wp-mcp-linkedin-fator3-0.7.0-fonte.zip](wp-mcp-linkedin-fator3-0.7.0-fonte.zip), raiz `wp-mcp-linkedin-fator3-0.7.0-fonte/`, código/build/testes/evidências/referências e a cópia interna anterior ao fechamento.
- `wp-mcp-linkedin-fator3-0.7.0-relatorio.md`, relatório externo canônico com identidade completa após fechamento.
- [wp-mcp-linkedin-fator3-0.7.0-impacto-wp-mcp-fator3.md](wp-mcp-linkedin-fator3-0.7.0-impacto-wp-mcp-fator3.md), revisão 3, encaminhamento técnico preparado para o dono, sem envio externo.

O fonte é fechado uma vez, sem ZIP aninhado. Seu relatório interno não tenta conter o hash do próprio arquivo que o inclui. A versão/hash do instalador entregue corresponde às evidências locais e à instalação compartilhada; o fonte não inclui dependências binárias, credenciais reais, banco, logs pessoais ou capturas de navegador.
