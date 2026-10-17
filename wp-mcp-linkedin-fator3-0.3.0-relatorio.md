# Entrega — Fator3 MCP LinkedIn 0.3.0

Data: 17/10/2026. Rodada: implementação. Base 0.2.0 → alvo 0.3.0 (incremento minor). Estado: apta no escopo do Pedido 1; homologação externa não executada nesta rodada.

**Relatório externo definitivo, emitido após o fechamento do fonte.** A cópia interna permanece identificada como anterior ao fechamento.

## 1. Bases aceitas

Base autêntica recuperada e conferida: `wp-mcp-linkedin-fator3-0.2.0-instalador.zip` — 79625 bytes — SHA-256 `64da9956452d3943546758690cf5cb5ff6508cbf502780bbcc1ca1492e6e8324`. Fonte de referência: `wp-mcp-linkedin-fator3-0.2.0-fonte.zip` — 198591 bytes — SHA-256 `a5b16da0d8c46fa2c09996b71b448a731a05db96d1657770b15786f689fd2b46`. O trabalho parte do código dessa base; não se reconstruiu um plugin paralelo.

Pedidos recebidos: MCP LinkedIn 1, na aba Fator3 MCP LinkedIn(2).md. Aplicadas as instruções comuns e o padrão de entrega revisão 4, de 16/10/2026. Essas entradas e seus hashes estão em inputs/. Relatórios recebidos dos acompanhantes foram lidos como contexto; evidências próprias desta rodada ficam em evidence/.

Identidade: `wp-mcp-linkedin-fator3/wp-mcp-linkedin-fator3.php`, provider `wp-mcp-linkedin-fator3`, prefixo `linkedin/*`, REST `f3-linkedin/v1`. GPL-2.0-or-later; nome exibido Fator3 MCP LinkedIn; autor Fator3. WordPress mínimo 6.4 e PHP mínimo **8.1.2 de 64 bits**, comprovados conjuntamente. O cabeçalho anterior declarava apenas 8.1; a precisão 8.1.2 evita prometer patches não executados. Abilities dependem da API disponível; painel e REST permanecem independentes do transporte.

## 2. Convivência e encaminhamentos

| Acompanhante testado | Versão | SHA-256 do instalador recebido |
|---|---|---|
| Fator3 Site Core | 1.35.0 | `1368395e6c5842c21e822010310c1d544000ed7d72b2f6ee234491d18c686f20` |
| Fator3 MCP | 0.24.0 | `e2c78fcf0e99da55237808bc51fe408405e367fd76a71172b497707996f8aa95` |
| Fator3 MCP Google | 0.11.0 | `d181deaeee8ef365ac4d6a08884d9fa3d3a3164b21f0538d8ed5d56722536bf9` |

Testado também com Fator3 MCP Meta 0.3.0. Ordem local: sociais antes do trio na atualização; trio antes dos sociais na instalação limpa. No teste remoto, só os dois sociais foram substituídos, Meta primeiro e LinkedIn depois. Não há requisito de troca simultânea nem dependência artificial de Core/Google para relatórios locais.

Não foi identificado novo impacto técnico sobre Core, MCP, Google, Meta ou Implantador nesta alteração de cabeçalho/documentação; nenhum arquivo individual artificial foi criado. A prova de convivência de carregamento com Core 1.35.0 não equivale à homologação real de Lead Sync Core → LinkedIn. O Core recebido já implementa o consumidor SDK 1.1; não se repetiu a afirmação antiga de ausência desse consumidor.

Core: medição/consentimento/contatos; MCP: transporte/administração; Google: suas APIs. Não alterados nesta rodada. Implantador: pacote não disponibilizado, portanto não-avaliado por execução; nenhuma mudança de contrato para ele foi introduzida. Não houve publicação no repositório, distribuição na frota ou envio de encaminhamentos a terceiros.

## 3. Mudanças por pedido e evidências

| Pedido | Implementação | Evidência própria |
|---|---|---|
| MCP LinkedIn 1 | Description exatamente como recebida; explicita Pages, Ads, Lead Sync, exportações e responsabilidade do Core sobre contatos | Comparação exata no teste nativo e plugins/list após atualização |
| Entrega 0.3.0 | Versão, documentação instalada e mínimo PHP comprovado; identidades públicas preservadas | Build reproduzível, hashes do runtime e leitura integral pelo MCP |

Adapter, LeadReader, SDK 1.0/1.1, autorização de grants, diário de assinaturas, coletas, exportações e funcionalidades de Pages/Ads permanecem byte a byte iguais à base 0.2.0. O diff funcional de includes se limita a Config.php e à documentação compilada. Os itens funcionais retirados da aba não foram reabertos. Nenhuma assinatura, formulário remoto, campanha ou contato real foi criado.

`evidence/runtime-diff.json` identifica os arquivos alterados. Build executa lint PHP, gera schemas e documentação compilada e fecha ZIP com metadados determinísticos. `evidence/build-reproduction.json` prova a reconstrução byte a byte deste instalador a partir do fonte autônomo.

| Prova própria com ambos os sociais | Ambiente | Resultado |
|---|---|---|
| Atualização direta com registros 0.2.0 | WP 7.1.2 / PHP 8.3.6 / MySQL 8.0.46; sociais antes do trio | 68 verificações, 0 falhas |
| Instalação limpa | WP 7.1.2 / PHP 8.3.6 / MySQL 8.0.46; trio primeiro | 65 verificações, 0 falhas |
| Mínimo declarado, sem acompanhantes | WP 6.4 / PHP 8.1.2 / MySQL 8.0.46 | 63 verificações, 0 falhas |

Total conjunto: **196 execuções de verificações**, com cenários repetidos entre ambientes, não 196 casos distintos por plugin. Relatórios nativos em evidence/lab-upgrade/, lab-clean/ e lab-minimum/. Incluem autorização de editor negada mesmo em allowlist, REST 403, projeção sem credenciais, cifra, revisão concorrente, jobs/exportações e leitura documental sem HTTP/escrita; no Meta, histórico/backfill e novos diagnósticos; no LinkedIn, SDK/grants/timeout/concorrência de assinaturas. Fixtures interceptam HTTP do fornecedor: são testes em WordPress real local, sem homologação remota. Testes do executor MCP usam PHP nativo e perfil configurado pelo serviço administrativo público, sem bypass de autorização.

## 4. Instalação e prontidão

Site autorizado: https://fator3-teste-mcp-1.dreamhosters.com/ — WP 7.1.3/PHP 8.3.30. Atualização real 0.2.0 → 0.3.0 por plugins/upload-base64 com expected_slug, expected_sha256 e chave idempotente. Operação `ad14aa3df48d11deaf72ffc6`; package_operation_id `5675530a3977a63e46cd6857d3265b1a`; backup de arquivos `cbeda144e5720295037106fc`. Resultado applied=true, recovery_status=applied, ativo antes e depois.

Sondas internas da home e /wp-json/: HTTP 200 antes/depois, fresh PHP e cache_bypass_verified=true. Reativação silenciosa não executou ciclo de activation hook; esse ciclo foi coberto nas instalações limpas locais. O instalador não declarou business_readiness_verified: essa prontidão externa não é inferida de HTTP 200.

Conferidos **30/30 arquivos** por SHA-256 contra o ZIP entregue, incluindo documentação compilada; 64/64 na entrega conjunta. Description e versão conferidas novamente por plugins/list. Core 1.35.0, MCP 0.24.0 e Google 0.11.0 continuaram ativos e nas mesmas versões. system/health saudável, zero recuperações não resolvidas; selftest local deste plugin: 8 checks ok, external_checks=not_run e remote_homologated=false. Status: storage_ready/crypto_ready=true, connection_count=0. Nenhuma credencial ou fixture social foi instalada no site.

Documentação instalada descoberta e lida integralmente por `linkedin/documentation`: **11 documentos / 13 páginas**, UTF-8 concatenado idêntico ao instalador; guard da revisão antiga retornou revision_conflict, caminho fora da allowlist retornou not_found. Índice inclui configuração, operação, contratos/schemas, SDK, segurança, migração, diagnóstico e changelog. Evidências em evidence/documentation-validation.json e site-validation.json. No site, a sonda meta/create-job com conexão inexistente retornou not_configured, provando passagem da chave de domínio pelo MCP 0.24.0 sem criar job; não reproduziu o bloqueio antigo da 0.22.

Sem mudanças de layout nesta rodada: não repetido QA visual em navegador. Renderização administrativa e autorização foram exercitadas nativamente. Todos os laboratórios foram encerrados; nenhum serviço de teste ficou ativo. O site ficou com ambos os sociais 0.3.0 ativos.

## 5. Banco, atualização e reversão

Sem mudança de schema/tabelas, formato de cifra ou migração destrutiva. A atualização preserva conexões cifradas, opções, seleção de ativos, grants, agendas, páginas de resultado, histórico e diário. A prova de atualização usa registros reais semeados na 0.2.0, incluindo pais expirados e progresso; não é só ativação vazia. Dados históricos não ganham diagnósticos novos retroativamente.

Backup do instalador é pré-imagem de **arquivos**, não snapshot do banco; database_effects_reversible=false é reportado pelo MCP. Para reverter, interromper novas coletas, preservar banco e salts compatíveis, restaurar a pré-imagem ou instalador 0.2.0 de hash acima pela mesma pasta e conferir status/REST. Não executar uninstall como forma de atualização. A 0.3.0 não desfaz efeitos externos executados durante operação; restauração de arquivos não desfaz assinatura, publicação ou dados já coletados. Nesta rodada não houve esses efeitos reais. Reversão efetiva não foi acionada, pois as sondas passaram; não é declarada como teste executado.

## 6. Pendências e limites

Não há pendência de implementação do Pedido MCP LinkedIn 1. Acesso real a Pages/Ads/Lead Sync continua dependente de token, produto, ativos e permissões liberados ao app. O bloqueio externo já registrado na rodada anterior não foi transformado em novo requisito de código. Responsável por essa homologação: administrador do app/contas, com o mantenedor do fluxo Core quando houver recepção de leads. Nenhuma operação externa foi tentada para contornar esse bloqueio.


Não executados: homologação de API real, ensaio dedicado de HTTP 429 nesta rodada, rede/infraestrutura de todas as variantes MariaDB/multisite e QA visual completo. O mínimo foi comprovado no ambiente declarado, não em todas as combinações possíveis. A prova mínima não inclui o trio atual, que possui requisitos próprios mais altos. Leitura pública da documentação Meta teve bloqueio HTTP 429; não se usou isso como prova da causa do vazio. Causa/semântica de dados reais permanecem sujeitas ao aceite externo indicado. Mantenedor social responde por eventual ajuste após evidência; administrador do ambiente por acesso/configuração; dono da frota pela decisão de distribuição.

## 7. Configuração e credenciais

Em **Ferramentas → Fator3 MCP LinkedIn**, cadastrar token manual, versão mensal da API (padrão implementado 202609), Pages e contas de Ads/Lead Sync selecionadas separadamente. Client ID/application ID servem à identificação local; client_secret é usado no challenge/notificação e não substitui token. Lead Sync depende do produto/permissão específica e de formulários explicitamente concedidos.

O administrador concede metadata/responses/verify/subscriptions ao consumidor e ao callback HTTPS permitido. Registrar um consumidor não lhe concede acesso. Grants, seleção de formulários, revisão, diário e trava por fluxo permanecem os da 0.2.0. No Core, manter seleção explícita por integração e um cliente ativo por fluxo; não trocar automaticamente nem apagar o diário para resolver timeout.

Entradas humanas de configuração, consulta e ajuda exigem manage_options validado no servidor. Nenhum token/segredo real aparece neste relatório, no fonte ou em respostas de configuração; fixtures usam valores sintéticos identificados. Requer banco com InnoDB/bloqueios nomeados, sodium ou AES-256-GCM, HTTPS de saída e WP-Cron/cron real. Nenhuma nova exportação para Sheets, migração Porter ou BigQuery foi incluída. A comparação com Porter é critério de aceite, não migração de dados.

## 8. Artefatos finais

| Artefato | Bytes | SHA-256 |
|---|---:|---|
| `wp-mcp-linkedin-fator3-0.3.0-instalador.zip` | 79465 | `b6d20998379236baf46ac5ae0181646e8a15fb75bbb4f37a88a68be01d2d768a` |
| `wp-mcp-linkedin-fator3-0.3.0-fonte.zip` | 228685 | `a7e104ec20bd238e9227546acd888895562a95c452394dd633e52e1e3ae54d18` |

Relatório externo: `wp-mcp-linkedin-fator3-0.3.0-relatorio.md`. Não há impacto individual novo nesta rodada.

Somente o instalador é instalável no WordPress, com raiz `wp-mcp-linkedin-fator3/`. O fonte tem raiz única `wp-mcp-linkedin-fator3-0.3.0-fonte/`, runtime em plugin/wp-mcp-linkedin-fator3/, templates/build, testes, evidências sanitizadas, entradas e relatório anterior ao fechamento. Nenhum ZIP contém outro ZIP. Sem credenciais, banco do laboratório, cookies ou dependências binárias. README.md explica reconstrução e matriz de testes. O relatório externo fornece a identidade definitiva do fonte sem circularidade.
