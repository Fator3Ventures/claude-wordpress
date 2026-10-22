# Entrega — Fator3 MCP LinkedIn 0.6.0

Revisão: 1 · Data: 2026-10-22 · Rodada: evolução funcional e correções, Pedidos MCP LinkedIn 8 a 11.
Slug/basename: `wp-mcp-linkedin-fator3` / `wp-mcp-linkedin-fator3.php` · Versão/build: 0.6.0.
Status: **com-pendencias**. Implementação e atualização aprovadas no escopo testado; integração CAPI real e rastreamento combinado Insight Tag/servidor ainda não homologados.

**Relatório externo canônico, posterior ao fechamento do fonte.** A cópia interna permanece identificada como anterior ao fechamento, sem o hash circular do próprio ZIP. Este relatório registra a identidade final; o fonte não foi reaberto para incorporar esses dados.

## 1. De onde esta versão entra

A 0.6.0 instala em WordPress limpo e atualiza diretamente a **0.5.0** aceita, sem versão intermediária. A base foi o fonte entregue da 0.5.0, SHA-256 `00c7a230d61f85e43e69c9d0e3c0f31a88fa6dab4f4174ae6ce25c29fbf55486`; o instalador anterior tem 155689 bytes e SHA-256 `dcef9a7b236bdb84055baa4aa6db73ba2fcd3bdd9a7cea30905c2e771a563199`. Esses artefatos anteriores foram preservados.

Foram considerados os documentos normativos do projeto, os pedidos atualizados de 22/10/2026 e os pacotes recebidos Core 1.47.0, MCP 0.26.1, Google 0.17.0 e Meta 0.4.1. Os documentos e suas identidades estão em `inputs/`; o planejamento e os impactos foram iniciados antes do código das fronteiras e atualizados na implementação e na entrega.

Ambientes realmente executados: WordPress **7.1.3**, PHP **8.3.6 de 64 bits**, MySQL **8.0.46** no laboratório; WordPress **7.1.3**, PHP **8.3.36** no Site-Teste. Interface exercitada em Chromium **153.0.8010.0**. Os mínimos declarados herdados — WordPress 6.4 e PHP 8.1.2 de 64 bits — **não foram exercitados nesta rodada**, portanto seu suporte não está comprovado por esta entrega. São necessárias travas nomeadas no banco.

## 2. Convivência e encaminhamentos

A atualização integrada usou os instaladores recebidos, sem reconstruí-los: Core 1.47.0 (`dd16cb720e57c2d448e78a744eb0fd761d6aff04aadeeed8309b6b5003b417c1`), MCP 0.26.1 (`ed8035e6e326ac3c2021bac1ae9c11fde39c26686e1763299b445c3992cb5384`), Google 0.17.0 (`42bd11080b518c82e0960753fa7b08d7adae28743cfcd3e96f9b83bf3f4709b0`) e Meta 0.4.1 (`719e3db7bb55f58cd08c2e78420e06374a6a4b08fad693e849677783ddc82de2`). As mesmas versões permaneceram ativas no Site-Teste. A instalação limpa isolada comprovou a autonomia do LinkedIn sem os acompanhantes.

| Destinatário | Versão | Classificação / situação | Pedido | Impacto vigente |
|---|---|---|---|---|
| base-site-core-fator3 | 1.47.0 | validacao-coordenada / decisao-necessaria; implementação do adaptador comprovada, decisão de IDs aberta | Pedidos MCP LinkedIn 8 / Pedidos core 285 | `wp-mcp-linkedin-fator3-0.6.0-impacto-base-site-core-fator3.md`, revisão 4, entrega |
| wp-mcp-fator3 | 0.26.1 | validacao-coordenada / acao-necessaria; descritor humano comprovado, principal de serviço pendente | Pedidos MCP LinkedIn 10 e 8(d) | `wp-mcp-linkedin-fator3-0.6.0-impacto-wp-mcp-fator3.md`, revisão 3, entrega |

O descritor explícito elimina, para a 0.6.0, a dependência do adaptador legado do MCP limitado ao LinkedIn 0.5.0. Para usar o Registro central no escopo validado, mantenha MCP 0.26.1; para o consumidor de conversões, Core 1.47.0. Não foi estabelecida necessidade de nova ordem entre Google, Meta e LinkedIn. Google/Meta foram avaliados na coexistência, bootstrap e regressões integradas: não se identificou mudança relevante de contrato com eles. Suas APIs remotas não foram homologadas nesta rodada. Nenhum pacote acompanhante foi editado, nenhum encaminhamento foi enviado a terceiros e não houve publicação/distribuição à frota.

## 3. Mudanças e evidência

| Pedido exato | Problema e mudança entregue | Evidência e estado |
|---|---|---|
| Pedidos MCP LinkedIn 8(a), 8(b), acréscimo Core 1.47.0 | Serviço PHP, adaptador do consumidor `site-core-conversions`, envio unitário/lote e introspecção obrigatória; concessão independente do Lead Sync | implementado / validado-wordpress: fixtures de recusa, prévia, envio, lote, erro, replay e consumidor Core real; não homologado-fornecedor |
| Pedidos MCP LinkedIn 8(c), 8(e) | Regras da conta selecionada listadas por nome; seleção e concessão explícitas; escopos na Conexão; fonte API exigida | implementado e validado-wordpress para regras API existentes. Alteração da regra Insight Tag 31692506 para a mesma regra API bloqueada pela divergência descrita abaixo |
| Pedidos MCP LinkedIn 8(d) | Recibos com código/HTTP, diário técnico sem PII; Registro central nas execuções humanas | validado-wordpress para MCP/rota administrativa. Registro central de todos os envios em segundo plano permanece pendente de contrato do MCP |
| Pedidos MCP LinkedIn 9 | `follower_total` usa `COMPANY_FOLLOWED_BY_MEMBER`; erros HTTP incluem mensagem sanitizada e `serviceErrorCode` | implementado / validado-wordpress com resposta simulada. Comparação real com as duas Páginas permanece pendente |
| Pedidos MCP LinkedIn 10 | Descritor público `mutation-audit/1.0.0`, diagnóstico de admissão real e leitor com gates preservados | implementado / validado-wordpress: antes/depois por MCP e rota administrativa no Site-Teste; provedor registrado sem adaptador legado |
| Pedidos MCP LinkedIn 11 | Nomes exatos de credenciais, ajuda ao lado dos campos, caminhos/links, callback copiável, tabela Ajuda e erros OAuth contextualizados | implementado / validado-wordpress e navegador local; conferência autenticada de Developers/Campaign Manager e preenchimento pelo dono pendentes |

### Conversões e segurança operacional

Foram acrescentadas seis abilities, mantendo as 73 anteriores: `linkedin/list-conversion-rules`, `linkedin/get-conversion-grant`, `linkedin/save-conversion-grant`, `linkedin/conversion-capabilities`, `linkedin/send-conversion-event` e `linkedin/send-conversion-events`. O catálogo atual possui **79**, com rótulos em português e schemas fechados. Chamadas humanas de administração exigem `manage_options`.

O filtro público `f3base_conversoes_adaptador` atende somente destino `linkedin`, contrato `site-conversion-delivery/1.0.0` e consumidor `site-core-conversions`, sem substituir adaptador já fornecido. `capabilities()` faz leitura local e devolve contrato, prontidão/motivo, `destination_ref` opaco e ID de conversão textual. `sendBound()` exige o vínculo correto; `send()` sem vínculo é recusado. Troca de conexão, revisão, conta, regra, principal ou revogação invalida o vínculo. A concessão exige introspecção com `rw_conversions` e `r_ads`, papel autorizado na conta e regra pertencente à conta, ativa, com `conversionMethod=CONVERSIONS_API`. O envio revalida essas condições; concessão de Lead Sync não concede CAPI.

O payload `site-linkedin-conversion/1.0.0` preserva `eventId` e `conversionHappenedAt` originais. Aceita `conversionValue` opcional, identificadores `SHA256_EMAIL`/`LINKEDIN_FIRST_PARTY_ADS_TRACKING_UUID` e `userInfo` validado. Nome e sobrenome devem aparecer juntos; campos desconhecidos são recusados. Apenas campos oficiais seguem para `/rest/conversionEvents`: `contract`, `record_id` e `event_id` não seguem. Lotes de 1 a 100 itens usam a operação nativa de lote quando há mais de um evento novo, com recibo individual.

O código efetivo do Core 1.47.0 conserva `record_id` do contato, que pode diferir de `event_id`/`eventId`, apesar da redação do impacto recebido. A implementação aceita essa referência interna distinta e exige igualdade entre os dois IDs de evento; a prova usa `F3Base_Linkedin_Conversoes::montar()` e `F3Base_Conversoes_Servidor::adaptador()` reais, sem modificar o Core. A correção documental foi encaminhada no impacto.

O diário de idempotência vincula conta/regra/evento por HMAC, com trava nomeada e gravação do estado antes do POST. Guarda digest e metadados técnicos, sem payload pessoal. Replay confirmado ou incerto não repete envio; mesmo ID com payload diferente é recusado. Timeout, 408, 5xx ou recibo não conclusivo resultam em `incerto`, sem nova tentativa automática. Recusa comprovada devolve `non_delivery_proven`; decisão de retry, fila e consentimento continuam no Core. Não foi implementada a reconciliação opcional. A operação humana usa prévia por padrão, confirmação explícita e comprovante vinculado ao contexto, válido por dez minutos.

**Limite da regra 31692506:** a documentação oficial vigente orienta uma regra por fonte navegador/servidor, com deduplicação pelo mesmo ID de evento. O Core recebido exige o ID do adaptador igual ao ID configurado para o navegador. Não se encontrou contrato oficial que permita converter silenciosamente a regra Insight Tag existente em duas fontes com o mesmo ID. A 0.6.0 exige uma regra API existente e não executa essa transformação nem cria outra regra comercial automaticamente. O responsável Core/dono deve decidir o vínculo de IDs; o aceite original nessa regra permanece bloqueado. Fonte consultada em 22/10/2026: [Conversions API Use Cases](https://learn.microsoft.com/en-us/linkedin/marketing/conversions/conversions-usecase?view=li-lms-2026-09).

### Auditoria, diagnóstico e interface

O evento `f3_linkedin_mutation_recorded` e o leitor `linkedin/get-write-operation` foram preservados. O descritor declara os quatro campos públicos exigidos; `central_audit` informa a admissão real. O leitor continua exigindo administrador, principal proprietário e ativo selecionado. O evento CAPI transporta referências e estados técnicos, sem payload, segredo, texto de comentário ou URL assinada.

O MCP 0.26.1 exige principal humano com `manage_options` no contrato de auditoria. O Core despacha também como usuário zero; a 0.6.0 não assume a identidade do administrador que concedeu o acesso. Nessa execução há diário local e `central_audit=service_principal_unsupported`, sem afirmar Registro central concluído. Essa parte do Pedido 8(d) requer evolução do contrato público do MCP.

O total de seguidores usa `/rest/networkSizes/{URN codificada}` com o enum corrigido. Recusas HTTP preservam `details.provider_message`, `details.serviceErrorCode` e indicação de sanitização; mensagens removem valores da requisição, credenciais, e-mails, URLs e identificadores sensíveis detectáveis, com limite de tamanho. Não se devolve o corpo bruto. `oauth_rejected` distingue o Access Token do par Client ID/Primary Client Secret da introspecção. Cabeçalhos e códigos de limite/retentativa permanecem disponíveis quando pertinentes.

As abas Conexão, Ativos e Formulários e concessões receberam ajuda contextual. Campos do WordPress são identificados como locais. Os nomes e caminhos são baseados na documentação oficial e no pedido recebido; não há alegação de inspeção autenticada do LinkedIn nesta rodada. A aba Ajuda consolida campo → nome no LinkedIn → local. O endereço completo de callback tem botão de copiar. O navegador comprovou listagem pelo nome da regra, concessão/revogação persistentes e ausência de erro JavaScript.

## 4. Instalação e prova da troca

Instale `wp-mcp-linkedin-fator3-0.6.0-instalador.zip` por substituição normal do plugin existente, preservando a pasta `wp-mcp-linkedin-fator3`. Confira o SHA-256 da seção 8 e use `expected_slug=wp-mcp-linkedin-fator3` em um instalador que aceite esse parâmetro. Mantenha backup antes da troca. Não instale o ZIP fonte nem os auxiliares de teste. Não há URL raw publicada desta entrega: distribuição ao repositório da frota permanece com seu responsável.

No Site-Teste autorizado, a atualização por `plugins/upload-base64` trocou 0.5.0→0.6.0, retornando `applied=true`, plugin ativo antes/depois e sondas de página e REST 200. Operação `b98c3847d8786819df03dd21`, operação de pacote `b249f25877291a8fd6de0f78e1cd386f`, backup dos arquivos anteriores `c64573832964365650cc0e40`. O pacote instalado tem o mesmo hash entregue e testado no laboratório. O agendamento de manutenção anterior foi preservado, sem ciclo forçado de desativação/ativação.

| ID | Ambiente / cenário | Resultado | Evidência no fonte | Limite |
|---|---|---|---|---|
| L1 | WordPress limpo, somente LinkedIn | 86 verificações, zero falhas | `evidence/clean/native-tests.json` | fornecedor simulado |
| L2 | Atualização direta 0.5.0 com Core/MCP/Google/Meta vigentes | 119 verificações, zero falhas | `evidence/upgrade/native-tests.json` | fornecedor simulado; inclui regressões repetidas de L1 |
| UI | Chromium real sobre WordPress local | 8 verificações, zero falhas | `evidence/clean/ui-tests.json` | não substitui aceite do dono no LinkedIn autenticado |
| S1 | Site-Teste, rodada final de CAPI/auditoria/seguidores | 11 verificações, zero falhas; 3 POSTs sintéticos, zero chamadas reais ao fornecedor | `evidence/site-teste-060.json` | REST administrativa chamada internamente com usuário autorizado |
| S2 | `linkedin/selftest` com `{}` | 8 verificações locais aprovadas | mesma evidência | não valida conta real |
| D1 | Documentação instalada via MCP | 19 documentos / 20 páginas, bytes e SHA-256 íntegros | `evidence/mcp-documentation-060.json` | leitura local ao plugin |
| B1 | Build reproduzido após os testes | mesmo ZIP de 189130 bytes; lint de 24 PHP; 49 arquivos runtime idênticos | manifesto do plugin e ambientes L1/L2 | sintaxe no PHP exercitado |

Os testes cobrem scopes e papéis revogados, regra de outra conta/fonte, vínculo obsoleto, revogação durante preflight, colisão de evento, replay confirmado/incerto, lote parcial, 429, payload, ausência de PII, credenciais e regressões anteriores. Contagens são execuções por cenário, não casos únicos somáveis. O log local registrou avisos do WordPress ao tentar consultar atualizações externas e notices de tradução antecipada do domínio `f3base` no cenário integrado; não foram identificados erros PHP atribuídos ao LinkedIn nesses logs. Os acompanhantes não foram alterados para remover esses avisos.

Prontidão observada: `linkedin/status` com `{}` devolve versão 0.6.0, `storage_ready=true`, `crypto_ready=true`, `audit_health=ok` e `access_lifecycle.next_maintenance=1792702984`. Não há coleta agendada, coerente com configuração de coleta vazia. `system/health` mostra o descritor LinkedIn admitido em `environment.mutation_audit`, sem erro de registro. Descoberta `prefix=linkedin/`, `per_page=100`, `compact=true` retorna 79 abilities, todas da 0.6.0, sem próxima página; hash de catálogo `3aad58c310cdf43f6d3fe56df3dc95c1c15dd78ba32c9c10dea15641e2184b7f`.

Documentação: `linkedin/documentation` com `{}` fornece índice. Para leitura use `document`, `offset=0`, `limit_bytes=65536`, e nas continuações `next_offset`/`expected_revision`. Concatenar `content` sem separador. Os 19 documentos foram lidos integralmente pelo MCP e comparados aos bytes do instalador; `input-schemas.json` exigiu duas páginas. Schemas de entrada têm 116034 bytes e SHA-256 `533d62659c17b1067b5410636eb2d56b03d5488aedad819fcee60f4b4a3972c0`. O laboratório também exercitou páginas pequenas e revisão/UTF-8, sem HTTP externo ou mutação documental.

Estado final: LinkedIn 0.6.0 ativo no Site-Teste, demais plugins mantidos. Os dois arquivos MU temporários foram removidos com guardas de hash e sondas 200. Catálogo `linkedin-qa/` vazio; nenhuma conexão, concessão, prévia ou diário sintético de conversão permaneceu. Permanecem referências centrais da auditoria simulada e backups dessas operações, sem dados pessoais; as referências cujo diário de teste foi limpo não são recibos de produção. A segunda limpeza foi `e13b7c9fba7b3026fbca6166`, backup `4326db531660ca65d706ef27`. Não foram alterados sites da frota ou enviadas conversões reais.

## 5. Banco e volta de versão

Mantidos identidade do plugin, namespace, tabela/store e schema estrutural existente. A 0.6.0 utiliza os novos buckets lógicos `conversion_grant`, `conversion_preview` e `conversion_event` dentro do armazenamento do LinkedIn. Não há migração destrutiva, alteração da tabela de outro plugin ou importação de opções privadas do Core/MCP. As conexões, tokens cifrados, grants Lead Sync, históricos e agendas existentes são preservados; a prova de atualização validou a manutenção da base 0.5.0.

Grants e comprovantes usam controle de revisão; o diário guarda referências/digests técnicos, sem payload pessoal. Jobs e consentimento de conversão continuam pertencendo ao Core. Nenhum novo job entrega conversões por iniciativa própria do LinkedIn. O ciclo de manutenção das credenciais permanece o já existente.

Para retornar, restaure o instalador 0.5.0 e o backup adequado dos dados quando necessário, coordenando antes a fila de conversão do Core. A 0.5.0 não conhece o adaptador CAPI nem os novos buckets: a troca de arquivos desativa esse serviço, mas não desfaz dados gravados nem eventos eventualmente aceitos pelo fornecedor. Não apagar o histórico de idempotência para provocar reenvio. O backup de arquivos criado pelo instalador **não é backup transacional do banco** e informou `database_effects_reversible=false`. As referências centrais já gravadas também não são removidas pela volta do plugin.

## 6. O que permanece pendente

| Pendência | Motivo / próximo aceite | Responsável |
|---|---|---|
| Conversão real em ctooffice e contagem única | Aguardar aprovação `rw_conversions`, token habilitado, consentimento/contexto corretos e ordem do dono; conferir fila entregue e métrica no Campaign Manager | LinkedIn, dono e frota |
| Regra 31692506 e duas fontes | Resolver IDs navegador/servidor no contrato Core ou demonstrar contrato oficial de regra única; não basta marcar concessão local | responsável Core e dono, impacto revisão 4 |
| Registro central de serviço | MCP 0.26.1 exige principal humano; definir contrato de serviço autorizado e leitor adequado | responsável MCP, impacto revisão 3 |
| `follower_total` real | Consultar Páginas 143789907 e 40774077 em seus sites e comparar com a tela do LinkedIn | frota/dono com acesso real |
| Aceite completo do Pedido 11 | Conferir caminhos em sessão autenticada do Developers/Campaign Manager; dono preencher conexão nova com a tela e validar erro de segredo real controlado | dono/frota |
| Mínimos de runtime | Executar matriz WordPress 6.4/PHP 8.1.2; cabeçalho herdado não é prova | manutenção/QA |
| Pendências reais anteriores de gestão/renovação | Não homologadas novamente: escopos de gestão e refresh dependem de produto/token aprovado; não confundir regressão simulada com aceite real | dono/fornecedor/frota |

Não há autorização implícita nesta entrega para provocar conversão real, criar regra comercial, alterar o Core/MCP ou distribuir a toda a frota. Esses limites não impedem a instalação e o uso das funções já configuradas no escopo testado; impedem declarar encerrado o aceite completo do Pedido 8 e os aceites externos de 9/11.

## 7. Credenciais e configuração do dono

Em WordPress → Ferramentas → Fator3 MCP LinkedIn, a aba Conexão solicita somente os campos necessários ao caso. Nenhum valor secreto foi incluído nesta entrega.

| Campo | Nome no LinkedIn / onde obter | Uso |
|---|---|---|
| ID do cliente | **Client ID**; [LinkedIn Developers](https://www.linkedin.com/developers/apps) → app → Auth → Application credentials / Authentication keys | par da introspecção/OAuth; não é o número do app |
| Chave secreta do aplicativo | **Primary Client Secret**, mesma seção, copiar pelo botão ao lado do valor | introspecção e OAuth; armazenado cifrado |
| Token de acesso | **Access Token**; ferramentas OAuth do app, com produtos/escopos aprovados | leitura, gestão ou CAPI conforme permissões reais |
| Validade do acesso | expiração apresentada na emissão/introspecção; campo local UTC | diagnóstico e manutenção |
| Token de renovação | **Refresh Token**, somente quando a aprovação do app permite renovação programática | opcional; não é outro Client Secret |
| Validade da renovação | prazo do refresh na resposta OAuth; campo local UTC | não inventar validade se não fornecida |
| Número do aplicativo | **Application ID**, número no endereço da página do app | contexto de notificações; distinto de Client ID |
| Retorno OAuth | **Authorized redirect URLs for your app**; Auth → OAuth 2.0 settings | copiar o endereço mostrado pelo WordPress, terminado em `admin-post.php?action=f3_linkedin_oauth_callback` |
| Página / conta / formulário | **Organization ID**, **Ad Account ID**, **Lead Gen Form ID**; seleção descoberta e endereços das telas correspondentes | selecionar explicitamente os ativos; não inferir acesso por colar um ID |
| Regra de conversão | **Conversion ID**; Campaign Manager → Measurement → Conversion tracking | escolher regra ativa da conta com fonte Direct API/Conversions API |

Leitura usa os escopos aprovados pertinentes, como `r_ads`, `r_ads_reporting`, `r_organization_admin` e `r_organization_social`. Gestão requer os escopos correspondentes, como `rw_ads`/`w_organization_social`; Lead Sync requer sua autorização própria. CAPI exige `rw_conversions` e leitura de conta/regra com `r_ads`. A autorização opcional pelo navegador só pede permissões: não concede produto que o LinkedIn ainda não aprovou. Depois da conexão e ativos, conceder separadamente o consumidor `site-core-conversions`; `ready=true` representa vínculo local válido, não homologação comercial da entrega.

Referências técnicas primárias consultadas em 22/10/2026: [Conversions API](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api?view=li-lms-2026-09), [schema](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api-schema?view=li-lms-2026-09), [workflow](https://learn.microsoft.com/en-us/linkedin/marketing/conversions/conversions-workflow?view=li-lms-2026-09), [organizações](https://learn.microsoft.com/pt-br/linkedin/marketing/community-management/organizations/organization-lookup-api?view=li-lms-2026-03) e [credenciais do aplicativo](https://learn.microsoft.com/en-us/linkedin/shared/api-guide/best-practices/secure-applications). URLs ajudam a localizar o contrato; não substituem o aceite das telas autenticadas.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `wp-mcp-linkedin-fator3-0.6.0-instalador.zip` | 189130 | `edfed426b2e0e4fce14a5c5c6241b12bed25186ab1da2102da96b2032a8af45e` |
| Fonte | `wp-mcp-linkedin-fator3-0.6.0-fonte.zip` | 517114 | `466381c50c8b00599e00d24eec36b2f6df61d88257c24fbb3f8438585acb0a96` |

Complementos: este relatório `wp-mcp-linkedin-fator3-0.6.0-relatorio.md` e os impactos individuais Core revisão 4 / MCP revisão 3 relacionados na seção 2. O fonte tem uma pasta raiz `wp-mcp-linkedin-fator3-0.6.0-fonte/`; o instalador tem somente `wp-mcp-linkedin-fator3/`. Nenhum ZIP contém ZIP aninhado. O fonte inclui código completo, runtime exato, build, testes, documentação, entradas documentais e evidências sanitizadas, sem ambientes de banco, cookies, credenciais reais ou capturas de navegador.

Este relatório externo registra os bytes/hash finais e os links dos dois ZIPs. Sua revisão final não altera retroativamente a cópia interna anterior ao fechamento. Instalador e relatório são os artefatos de distribuição operacional; a publicação no repositório da frota não foi realizada nesta rodada.

Arquivos da entrega: [wp-mcp-linkedin-fator3-0.6.0-instalador.zip](wp-mcp-linkedin-fator3-0.6.0-instalador.zip) e [wp-mcp-linkedin-fator3-0.6.0-fonte.zip](wp-mcp-linkedin-fator3-0.6.0-fonte.zip).
