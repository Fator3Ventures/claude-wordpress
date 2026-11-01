# Entrega — Fator3 MCP LinkedIn 0.14.0

Revisão 1 · 2026-10-31T20:15:21-03:00 · Rodada: implementação dos Pedidos MCP LinkedIn 16 e 17.
Slug/basename preservados: `wp-mcp-linkedin-fator3` / `wp-mcp-linkedin-fator3/wp-mcp-linkedin-fator3.php`.
**Status: com-pendencias de homologação na conta real.** Código implementado e validado em WordPress; 0.14.0 ativa no Site-Teste e corrente para continuidade do desenvolvimento.

> Relatório externo canônico. A cópia incluída no fonte foi congelada antes do empacotamento, sem o hash do próprio ZIP.

## 1. De onde esta versão entra

Instalação limpa e atualização direta **0.13.0 → 0.14.0**, sem intermediária. Base imutável: instalador 0.13.0, 314596 bytes, SHA-256 `1c45738322f4901aeacdc36615789ae961e8b9d521ba321a27de0aea76c13502`; fonte 0.13.0, 2038497 bytes, SHA-256 `9eab181f679458b9fc27ae2d93144a800d63a1f0e8aa0760eae4ec2d35135760`. Ambos foram recuperados e conferidos, e o Site-Teste estava na 0.13.0 antes da troca.

Entrada funcional: `Fator3 MCP LinkedIn(20261031-224258).md`, 7333 bytes, SHA-256 `c11cd7562d9d4a1dabe4bbe8fa9705745b7890d2937d828bb74fee0b4bc19e1e`. O documento registra0.13.0 nos 12 sites como informação recebida; a frota não foi atualizada por esta rodada. Aplicadas as normas comuns revisão5 preservadas na base, o plano `planning/RELEASE-0140.md` anterior à implementação e a regra do dono de configuração com simulação/revisão. Os documentos originais de pedidos, Core e MCP não foram alterados.

Mínimos próprios exercitados: WordPress 6.4 e PHP 8.1.2 de 64 bits, MySQL 8.0.46, criptografia autenticada e travas nomeadas. Matriz atual: WordPress 7.1.4/PHP 8.3.6/MySQL 8.0.46. Site-Teste: WordPress 7.1.4/PHP 8.3.36/banco8.4.11-0ubuntu0.26.04.1. O transporte abilities/MCP depende da API disponível; no WordPress 6.4, painel/REST e funções próprias continuam independentes.

## 2. Convivência e encaminhamentos

Os16 anexos da rodada tiveram bytes/SHA-256 reconferidos após o trabalho. Os cinco instaladores acompanhantes permaneceram originais, incluindo todos os arquivos instalados nas duas bancadas integradas. Evidências: `received-artifacts-unchanged.json`, `companion-integrity.json` e inventários em `evidence/release0140/`.

| Pacote recebido | SHA-256 do instalador | Escopo da prova própria |
|---|---|---|
| Core 1.65.1 | `059d7da03484eb3d9eb7327f49787144466f451fcf51730ea0357d92c03f168a` | Consumidor/fila comercial real em WordPress, concessões, referências e incerteza; HTTP LinkedIn sintético. |
| MCP 0.38.0 | `bc550c6573527a0d71bfa560036f83e7c8aec546f49d70b8e0095da5d303c1a5` | Executor original, diagnóstico OAuth, configuração, revogação, acervo, auditoria de serviço e documentação. |
| Google 0.24.0 | `803fa058182b9f43625352f2b4a1572a3cd4b728f8c07fd58314a9a111d41849` | Ativação/convivência e integridade; sem chamadas reais Google. |
| Meta 0.17.0 | `a 360feff0bdb723c7f3c2a240b288bc1c3af917e851cb798d905e31a95b4162d` | Ativação/convivência e integridade; sem chamadas reais Meta. |
| Pipedrive 0.5.0 | `59e8c99d5bb8a54fcfeaba06c56d816b940a1fe97a7d6b473d13a252c6e5042a` | Arquivos preservados; inativo no PHP 8.3.6 por exigir8.3.36. Presença ativa observada remotamente; sem homologação comercial. |

No Site-Teste, Meta já estava em 0.18.0 antes da instalação e Google passou de 0.24.0 para 0.25.0 durante a janela de outro trabalho. Esta rodada instalou somente LinkedIn. Não se atribuem essas mudanças ao LinkedIn nem se anunciam provas locais dessas duas versões novas: o inventário remoto registra a convivência observada, com saúde LinkedIn positiva. Core 1.65.1/MCP 0.38.0/Pipedrive 0.5.0 permaneceram nas versões observadas.

**Impactos e pedidos emitidos:** nenhum. A análise cobriu esquemas/envelopes, credenciais, notificações, auditoria, transporte, concessões e contratos de aquisição/etapas. As mudanças são internas/aditivas no LinkedIn; não apareceu necessidade nova de código, configuração ou ordem de troca de um acompanhante. Não há arquivo de impacto para simples anúncio de versão ou encerramento.

**Tratamento dos recebidos/anteriores:**

- `wp-mcp-linkedin-fator3-0.12.0-impacto-wp-mcp-fator3.md`, revisão1, SHA-256 `ea8cc39c32dc65ab2b7a3443ed0d3680195ccab869737db3b6de34a3f9c9b843`: LinkedIn→MCP, Pedido Core 323/consumidor `site-core-quality`. Mantido o atendimento histórico informado no MCP 0.35.0 e comprovado na 0.13.0. A prova própria agora com MCP 0.38.0/Core 1.65.1 repetiu aquisição, duas etapas, recibos centrais, revogação e replay: `stages012.json` (24 casos) e `mcp-stages012.json` (5) em cada bancada integrada. Sem reenvio retroativo ou reemissão do impacto.
- Relatório Core 1.65.1: alterações354/362 de carga/carimbo/publicação preservam contratos comerciais; não traz pedido técnico novo ao LinkedIn. Pendências de desempenho/frota pertencem ao Core e aos respectivos responsáveis, sem encerramento aqui.
- Relatório MCP 0.38.0 e referência recebida ao impacto Core 1.63.0 r1/Core 354: inicialização e auditoria sob demanda foram tratadas pelo mantenedor MCP. O executor e os recibos LinkedIn passaram nesta rodada. Isso não encerra desempenho global do Core.
- Relatórios Google 0.24.0, Meta 0.17.0 e Pipedrive 0.5.0: lidos, com suas bases/limites considerados; nenhum pedido dirigido ao LinkedIn foi identificado. O atendimento Google ao impacto Core 1.61.1 r2/337/340/342 e os aceites comerciais dos demais continuam sob seus responsáveis. Presença de código recebido não foi convertida em homologação própria.

## 3. Mudanças e evidência

| Pedido exato | Problema e implementação | Prova e limite |
|---|---|---|
| Pedidos MCP LinkedIn 16 | Retorno agora registra `oauth-finish`, transporte `oauth_callback`, com operation_id, conexão, escopos solicitados, HTTP por etapa, active, Client ID, validade, status, escopos conferidos e motivo local. Tela mostra motivo e diagnóstico escapado, reabrindo a conexão. Vínculo do aplicativo/URI é conservado desde o início. Opções OAuth incluem openid/profile e conservam a seleção conferida; nenhuma permissão é adicionada automaticamente. | Base reproduzida sem diagnóstico. Candidata usa exatamente código/token novo/par/URI esperados. Testados token antigo revogado, inatividade, divergência, vencimento, ausência de campos, escopo, tipos inválidos, HTTP400/401, falhas de transporte, cancelamento, sessão, CAS, replay e preservação da salva. Aceite com conta real permanece pendente. |
| Pedidos MCP LinkedIn 17 | Refresh manual não verificado abre incidente visível, sem e-mail na gravação; manutenção aguarda primeira renovação/confirmação. Com atividade conferida e prazo maior que a janela, não avisa. Dentro da janela, uma tentativa por ID estável de incidente, independente de mudança do vencimento. Texto orienta **Renovar agora**, **Usar autorização candidata**, simular e confirmar. | Casos de 60 dias, bordas14 dias, janela7 dias, repetição, troca de validade/token, recibo legado, correio recusado/exceção, resolução e novo incidente aprovados. Mail e HTTP interceptados; nenhuma entrega real de e-mail alegada. |
| Regra do dono de 28/10, aplicada ao17 | `credential_notice_days`, inteiro1–365, padrão14 por conexão; alteração exige dry_run e confirmação da mesma candidata/revisão. Prévia exibe antes/depois. Recibo guarda connection_revision e notice_days usados. | Gravação direta, tipo inválido, limite, revisão antiga e candidata alterada recusados; confirmação preservada pelo MCP e painel. |

Os38 testes dirigidos estão em `request01617.php`; o executor MCP acrescenta10 e o painel completo38 verificações DOM/REST. Retorno OAuth não grava code, state, token, segredo, cookies, corpo bruto ou mensagens livres do fornecedor. Recibo é reservado antes de wp_mail; false/exceção não reabre automaticamente a tentativa. `sent=true` indica aceitação pelo transporte, não entrega na caixa postal. A atividade utilizada pela janela vem da última prova válida ligada à credencial, sem consulta ao fornecedor a cada status/manutenção.

**Causa do token histórico inativo:** não determinada. O caminho local testado troca primeiro o código e introspecta o token recém-emitido com o par correto. HTTP200/active=false também pode ocorrer quando o token não pertence ao aplicativo consultado; portanto, ausência de oauth_rejected não prova esse vínculo. A nova auditoria fornece dados para a próxima reprodução real. Não foi acrescentada repetição cega de código nem relaxada a exigência de token ativo. Referência primária consultada em 31/10/2026: [LinkedIn Token Introspection](https://learn.microsoft.com/en-us/linkedin/shared/authentication/token-introspection).

Permanecem **93 operações**. Somente os esquemas de `save-connection` (campo aditivo) e `oauth-start` (máximo11 escopos, coerente com a enumeração existente) diferem. Cifra, autorização administrativa, state de uso único, CAS, candidata temporária, confirmação, ativos/concessões e contratos comerciais continuam protegidos. A renovação com vínculo já confirmado continua automática; o bloqueio automático é específico do incidente que aguarda confirmação humana.

A revisão também corrigiu a aceitação de string numérica no novo campo, preservou o nome exato Primary Client Secret na mensagem e eliminou instruções antigas de versão corrente nos manuais LinkedIn. Ensaios intermediários e ajustes de fixture estão registrados em `development/`; não são resultados finais nem versões instaladas.

## 4. Instalação e prova da troca

Instalador final: **325350 bytes**, SHA-256 `91b49ab4aaac5487657496d22d2d1e3a31334a4afa2547dd7946ebdf1d9868ef`;73 arquivos,33 PHP aprovados no lint. Runtime e documentação foram fechados antes da instalação. O rebuild determinístico e a cópia `plugin/` correspondem ao instalador.

| Ambiente/cenário | Aprovadas / não aplicáveis / falhas | Evidência e limite |
|---|---|---|
| Base0.13.0, WordPress 7.1.4/PHP 8.3.6 | 2 reproduções /0/0 | `baseline/request01617.json`: ausência de auditoria e aviso imediato com 60 dias; fornecedor sintético. |
| Limpo integrado, WordPress 7.1.4/PHP 8.3.6 | 375 funcionais /1/0;34 documentais;38 DOM | `clean/`; os 38 casos dirigidos16/17 e10 via MCP estão incluídos nas 375. |
| Upgrade direto0.13.0→0.14.0, mesmos acompanhantes | 386 funcionais /1/0;34 documentais | `upgrade/`, instalador final.11 verificações específicas de preservação, incluindo ambas as tabelas byte a byte e recibos legados. |
| Limpo isolado, WordPress 6.4/PHP 8.1.2 | 333 funcionais /4/0 | `minimum/`; sem MCP/Abilities API. Funções próprias, autorização, credenciais e regressão comercial local. |
| Site-Teste, WordPress 7.1.4/PHP 8.3.36 | Instalação completa;9 autotestes;33 documentos/35 páginas | `site-summary.json` e `site-documentation.json`; sem conexão LinkedIn, sem aceite de fornecedor. |

São **1094 verificações funcionais aprovadas entre ambientes**,6 não aplicáveis e0 falhas finais; adicionalmente68 documentais locais e38 DOM, além das 2 reproduções da base. Contagens são execuções, não requisitos distintos. A não aplicabilidade da fixture histórica0.10.1 não substitui o upgrade0.13.0, que foi efetivamente executado. Nos mínimos, também não se aplicam três verificações dependentes de MCP/Abilities. Nenhuma entrada de log PHP própria ou de acompanhantes apareceu nas matrizes finais.

A instalação limpa, o mínimo e o DOM usaram a candidata funcional `cd22fcc19b31dacb3aa74a25e597733295a0fc70f698144648958125d4207190`. O fechamento posterior mudou somente manuais, sua cópia PHP compilada e manifesto. **Todo PHP funcional e JavaScript permaneceu byte a byte igual**, conforme `documentation-only-closure.json`. A matriz completa de upgrade e a leitura documental foram repetidas com o ZIP final91b49ab4; o mesmo ZIP foi instalado remotamente. Não se apresenta a candidata intermediária como outro instalador entregue.

O painel foi exercitado por **jsdom27.4.0**, carregando HTML/JavaScript reais do WordPress e REST autenticada: nomes, escopos, avisos, política simulada/confirmada, incidente após salvar refresh, candidata após renovar, preservação da identidade, histórico e concessões comerciais. Isso não é inspeção visual em Chrome/Safari nem consentimento no site LinkedIn.

### Site-Teste

URL: https://fator3-teste-mcp-1.dreamhosters.com/ . A ability nativa `plugins/upload-base64` recebeu o ZIP fechado, activate/overwrite=true, expected_slug=`wp-mcp-linkedin-fator3`, expected_sha256 da seção8 e chave idempotente própria. Operação `9ea0bfdac0dd83252bf07653d88e6ce8`; pré-imagem de arquivos `e69ea49a8481cd6720233f6c`. Resultado:0.13.0→0.14.0 ativa, applied=true, recovery_status=applied. A releitura `plugins/operation-status` confirmou complete, file_state=candidate e verification_reason=verified. Sondas internas de `/` e `/wp-json/`: HTTP200 antes/depois. Reativação silenciosa em PHP novo; o recibo não afirma ciclo completo de activation hook nem prontidão comercial. A prontidão local foi conferida separadamente.

`linkedin/status {}`:0.14.0, state=ok, storage_ready/crypto_ready=true, issues=[], migration_pending=false, zero conexões e agendas ativas. `linkedin/selftest {}`:9 testes locais positivos, external_checks=not_run e remote_homologated=false. Nenhuma conexão/credencial foi criada, helper remoto instalado ou recurso comercial disparado. O backup nativo e a auditoria da instalação são os resíduos operacionais esperados.

Documentação descoberta pelo MCP com schema real; índice e **33 documentos em 35 páginas** lidos integralmente com expected_revision, bytes e SHA-256 iguais ao instalador. CREDENTIALS.md foi lido antes/depois. Caminho fora da allowlist foi recusado e revisão documental errada retornou revision_conflict. Localmente também foram exercitados leitura sem HTTP/efeitos e gates de permissão. Evidência: `site-documentation.json`, com hash de cada documento.

Inventário remoto final observado: LinkedIn 0.14.0, Core 1.65.1, MCP 0.38.0, Google 0.25.0, Meta 0.18.0, Pipedrive 0.5.0, DreamHost 1.0.0, WP Super Cache 3.1.4 e Yoast 28.8, todos ativos. Não se afirma imutabilidade dos arquivos remotos dos acompanhantes; duas versões mudaram por outros trabalhos, conforme seção2. Não houve publicação no GitHub/raw nem distribuição nos 12 sites.

Para a frota, entregar este ZIP/relatório ao responsável; publicar a URL prevista `https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-linkedin-fator3-0.14.0-instalador.zip` somente no fluxo autorizado, conferir bytes servidos e SHA-256 antes de `plugins/upload`. Essa URL é destino previsto, **não publicação realizada/verificada nesta rodada**. Fonte permanece com o dono conforme decisão 89.

## 5. Banco e volta de versão

Mantidos schema de registros 2 e histórico 1. Nenhuma tabela/coluna nova, importação ou limpeza destrutiva. `credential_notice_days=14` é default de leitura e não regrava conexões na ativação. Atualização preservou ciphertexts, revisões, retenção finita, agendas, concessões, referências, eventos confirmados/incertos e saúde/recibos antigos. O teste conferiu as duas tabelas completas antes do primeiro teste funcional da candidata.

No uso, gravação explícita atualiza a conexão em transação; início/retorno OAuth mantém state/candidata temporários cifrados e auditoria sanitizada; saúde grava ID do incidente e recibo da tentativa de aviso com revisão/janela usadas. Reservar antes do correio evita repetição após resultado incerto. Conexões pausadas permanecem pausadas.

Preserve banco, arquivos e salts/chaves. A pré-imagem nativa cobre arquivos/ativação; não reverte banco, autorização no LinkedIn ou mensagens já enviadas. Voltar arquivos para 0.13.0 remove o diagnóstico e a nova política de avisos, podendo voltar aos avisos por validade. Não apague recibos, filas ou concessões para repetir operações. Antes de rollback operacional, planeje a credencial vigente e avalie a política de notificação. Desinstalação continua preservando os dados conforme o contrato existente.

## 6. O que permanece pendente

| Responsável / item | Prova que falta |
|---|---|
| Dono da conta/frota — Pedido 16 | Executar autorização pela tela com aplicativo/conta reais e a lista vigente; conferir nova auditoria, token ativo e persistência após a confirmação exigida. O Site-Teste tem zero conexões. A causa histórica de active=false continua não determinada. |
| Dono da conta/frota — Pedido 17 | Em conexão autorizada, salvar Access/Refresh Token reais e comprovar incidente visível sem e-mail com mais de 14 dias. Janela, deduplicação e correio foram testados somente com interceptação local. |
| Dono da conta — Pedido 15 histórico | A implementação anterior permanece e70 regressões foram repetidas. Token real válido com espaço final continua dependente do aceite do dono; retirada do item da lista não foi tratada como nova prova remota. |
| Dono/frota e integrações | Aceites reais20/92/116, Lead Sync, conversões, Ads/publicações e acervo não foram refeitos. Sem gastos, publicações, leads, assinaturas ou conversões reais nesta rodada. |
| Homologação de interface/permissões | Fluxo DOM/REST passou; inspeção visual em navegador real e conta remota sem manage_options não foram executadas. Negativas de autorização foram comprovadas localmente. |
| Mantenedores acompanhantes | Google 0.25.0/Meta 0.18.0 foram observados remotamente, sem novos ZIPs na bancada. Pipedrive 0.5.0 não foi ativado no PHP 8.3.6 local. Sem produto cartesiano, multisite ou outros runtimes/caches. |

Não foram encontradas regressões ou novos impactos no escopo final executado. Isso não significa ausência absoluta de impacto fora das combinações/provas descritas. Os pedidos16/17 estão implementados e validados em WordPress, **não encerrados como homologados no fornecedor**; o mantenedor da lista registra o aceite final.

## 7. Credenciais e configuração do dono

Ferramentas → Fator3 MCP LinkedIn → Conexões. Token manual continua padrão. Campos: Access Token, Client ID, Primary Client Secret, Refresh Token opcional e validade; nenhum valor secreto é incluído nesta entrega. Configure o callback exato exibido no painel no aplicativo LinkedIn. São necessários os escopos de leitura r_ads, r_ads_reporting, r_organization_admin e r_organization_social; openid/profile só quando já aprovados/concedidos e desejados. Escritas, Lead Sync e Conversions API exigem seus produtos, escopos e concessões próprios.

Para a primeira renovação manual: **Renovar agora**; se houver candidata, marcar **Usar autorização candidata conferida**, **Simular alterações**, conferir identidade/concessões e **Confirmar alterações**. A credencial salva continua ativa até a conclusão. Para mudar a antecedência, informar1–365 dias e usar a mesma simulação/confirmação; padrão14. Uma conexão nova não herda escopos da anterior. Status não faz chamada remota e informa o estado da última conferência.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-linkedin-fator3-0.14.0-instalador.zip](wp-mcp-linkedin-fator3-0.14.0-instalador.zip) | 325350 | `91b49ab4aaac5487657496d22d2d1e3a31334a4afa2547dd7946ebdf1d9868ef` |
| Fonte | [wp-mcp-linkedin-fator3-0.14.0-fonte.zip](wp-mcp-linkedin-fator3-0.14.0-fonte.zip) | 2204332 | `91b485c5a64ce4dc2fb8e5fba030f9abba76221d8cd9c2c66d55e7c46c0246fe` |

Terceiro artefato: `wp-mcp-linkedin-fator3-0.14.0-relatorio.md`. Somente o instalador é instalável. Fonte tem raiz versionada, runtime idêntico, build, testes, entradas e evidências sanitizadas; não contém outro ZIP, banco, dependências locais, credenciais reais, cookies ou logs privados. Impactos históricos são mantidos como histórico, sem encaminhamento novo. O fechamento do fonte é único; seu hash final fica neste relatório externo para evitar circularidade.
