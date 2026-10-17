# Entrega — Fator3 MCP Meta 0.3.0

Data: 17/10/2026. Rodada: implementação. Base 0.2.0 → alvo 0.3.0 (incremento minor). Estado: com-pendencias de homologação externa do Pedido 9; implementação e instalação aprovadas no escopo testado.

**Relatório externo definitivo, emitido após o fechamento do fonte.** A cópia interna permanece identificada como anterior ao fechamento.

## 1. Bases aceitas

Base autêntica recuperada e conferida: `wp-mcp-meta-fator3-0.2.0-instalador.zip` — 81332 bytes — SHA-256 `f5cb81781038e487741adc3a1d82791f149d37a5219f7d4747b0acf9ae27d57f`. Fonte de referência: `wp-mcp-meta-fator3-0.2.0-fonte.zip` — 202590 bytes — SHA-256 `e875060089708acbac061e617944b704829d3df618f80537a8a457f64f08b362`. O trabalho parte do código dessa base; não se reconstruiu um plugin paralelo.

Pedidos recebidos: MCP Meta 1 e 9, na aba Fator3 MCP Meta(2).md. Aplicadas as instruções comuns e o padrão de entrega revisão 4, de 16/10/2026. Essas entradas e seus hashes estão em inputs/. Relatórios recebidos dos acompanhantes foram lidos como contexto; evidências próprias desta rodada ficam em evidence/.

Identidade: `wp-mcp-meta-fator3/wp-mcp-meta-fator3.php`, provider `wp-mcp-meta-fator3`, prefixo `meta/*`, REST `f3-meta/v1`. GPL-2.0-or-later; nome exibido Fator3 MCP Meta; autor Fator3. WordPress mínimo 6.4 e PHP mínimo **8.1.2 de 64 bits**, comprovados conjuntamente. O cabeçalho anterior declarava apenas 8.1; a precisão 8.1.2 evita prometer patches não executados. Abilities dependem da API disponível; painel e REST permanecem independentes do transporte.

## 2. Convivência e encaminhamentos

| Acompanhante testado | Versão | SHA-256 do instalador recebido |
|---|---|---|
| Fator3 Site Core | 1.35.0 | `1368395e6c5842c21e822010310c1d544000ed7d72b2f6ee234491d18c686f20` |
| Fator3 MCP | 0.24.0 | `e2c78fcf0e99da55237808bc51fe408405e367fd76a71172b497707996f8aa95` |
| Fator3 MCP Google | 0.11.0 | `d181deaeee8ef365ac4d6a08884d9fa3d3a3164b21f0538d8ed5d56722536bf9` |

Testado também com Fator3 MCP LinkedIn 0.3.0. Ordem local: sociais antes do trio na atualização; trio antes dos sociais na instalação limpa. No teste remoto, só os dois sociais foram substituídos, Meta primeiro e LinkedIn depois. Não há requisito de troca simultânea nem dependência artificial de Core/Google para relatórios locais.

Impacto pertinente: `wp-mcp-meta-fator3-0.3.0-impacto-wp-mcp-fator3.md`, aberto na revisão 1 do planejamento e encerrado na revisão 2 da entrega. A preservação dos novos diagnósticos pelo MCP 0.24.0 foi provada com suas classes reais SafeOutput e ExecuteAbilityAbility em WordPress nativo. Não se alterou filtro de segredos nem código do transporte.

Core: medição/consentimento/contatos; MCP: transporte/administração; Google: suas APIs. Não alterados nesta rodada. Implantador: pacote não disponibilizado, portanto não-avaliado por execução; nenhuma mudança de contrato para ele foi introduzida. Não houve publicação no repositório, distribuição na frota ou envio de encaminhamentos a terceiros.

## 3. Mudanças por pedido e evidências

| Pedido | Implementação | Evidência própria |
|---|---|---|
| MCP Meta 1 | Description exatamente como recebida; nome, slug, basename, prefixos, Text Domain e Update URI preservados | Comparação exata no teste nativo e plugins/list após atualização |
| MCP Meta 9 — erros | Http preserva somente HTTP, code, error_subcode e is_transient com tipos estritos. Descarta mensagem, URL e conteúdo arbitrário da Graph. Envelope error mesmo com HTTP 200 é recusa | Fixtures de códigos 100/10/190, subcódigo 33, token, permissão e tentativa de exfiltração na mensagem |
| MCP Meta 9 — dados vazios | Grupo Page vazio ou com valores ausentes recebe uma tentativa individual por métrica, dentro do orçamento HTTP existente. Vazio persistente fica cause=undetermined; zero verdadeiro é mantido | Grupo vazio, recuperação individual, zero, vazio genuíno e mistura de métrica válida/inválida |
| MCP Meta 9 — permissões | validate-connection inspeciona o token derivado da Página selecionada e devolve page_permissions. Verifica identidade/app quando presentes, read_insights, pages_read_engagement e concessões granulares por Página | Token da Página confirmado na fixture, escopo ausente=false, inspeção indisponível=null, outro ativo/app recusado, seleção anterior ao HTTP |
| MCP Meta 9 — continuidade | Jobs pausados expõem last_error sanitizado; cobertura mantém erro por métrica. Múltiplos buckets da origem permanecem em source_values e não viram um valor supostamente disponível | Pausa por token, persistência, cobertura parcial e múltiplos buckets |

Não foi demonstrado erro de calendário na origem real. Mantidos period=day e limites since/until existentes; o teste prova que o fallback usa os mesmos limites. Não se atribuiu causa ao vazio de produção por inferência a partir de seguidores. O código legado unsupported_for_asset_or_version permanece para compatibilidade, acompanhado de cause e diagnóstico; não é prova autônoma de métrica descontinuada.

Pedido 9: implementação concluída; aceite externo ainda pendente. O documento PAGE-DIAGNOSTICS.md contém a sequência de validação. Pedidos 2–8 foram retirados pelo dono após validação da 0.2.0 e não foram reabertos. Nenhuma nova permissão é concedida automaticamente.

`evidence/runtime-diff.json` identifica os arquivos alterados. Build executa lint PHP, gera schemas e documentação compilada e fecha ZIP com metadados determinísticos. `evidence/build-reproduction.json` prova a reconstrução byte a byte deste instalador a partir do fonte autônomo.

| Prova própria com ambos os sociais | Ambiente | Resultado |
|---|---|---|
| Atualização direta com registros 0.2.0 | WP 7.1.2 / PHP 8.3.6 / MySQL 8.0.46; sociais antes do trio | 68 verificações, 0 falhas |
| Instalação limpa | WP 7.1.2 / PHP 8.3.6 / MySQL 8.0.46; trio primeiro | 65 verificações, 0 falhas |
| Mínimo declarado, sem acompanhantes | WP 6.4 / PHP 8.1.2 / MySQL 8.0.46 | 63 verificações, 0 falhas |

Total conjunto: **196 execuções de verificações**, com cenários repetidos entre ambientes, não 196 casos distintos por plugin. Relatórios nativos em evidence/lab-upgrade/, lab-clean/ e lab-minimum/. Incluem autorização de editor negada mesmo em allowlist, REST 403, projeção sem credenciais, cifra, revisão concorrente, jobs/exportações e leitura documental sem HTTP/escrita; no Meta, histórico/backfill e novos diagnósticos; no LinkedIn, SDK/grants/timeout/concorrência de assinaturas. Fixtures interceptam HTTP do fornecedor: são testes em WordPress real local, sem homologação remota. Testes do executor MCP usam PHP nativo e perfil configurado pelo serviço administrativo público, sem bypass de autorização.

## 4. Instalação e prontidão

Site autorizado: https://fator3-teste-mcp-1.dreamhosters.com/ — WP 7.1.3/PHP 8.3.30. Atualização real 0.2.0 → 0.3.0 por plugins/upload-base64 com expected_slug, expected_sha256 e chave idempotente. Operação `fc9207d755af8136293e7148`; package_operation_id `e044e35fcdad6e16057f5a750d083e5a`; backup de arquivos `ce5bbfda59fe9358e427dacd`. Resultado applied=true, recovery_status=applied, ativo antes e depois.

Sondas internas da home e /wp-json/: HTTP 200 antes/depois, fresh PHP e cache_bypass_verified=true. Reativação silenciosa não executou ciclo de activation hook; esse ciclo foi coberto nas instalações limpas locais. O instalador não declarou business_readiness_verified: essa prontidão externa não é inferida de HTTP 200.

Conferidos **34/34 arquivos** por SHA-256 contra o ZIP entregue, incluindo documentação compilada; 64/64 na entrega conjunta. Description e versão conferidas novamente por plugins/list. Core 1.35.0, MCP 0.24.0 e Google 0.11.0 continuaram ativos e nas mesmas versões. system/health saudável, zero recuperações não resolvidas; selftest local deste plugin: 8 checks ok, external_checks=not_run e remote_homologated=false. Status: storage_ready/crypto_ready=true, connection_count=0. Nenhuma credencial ou fixture social foi instalada no site.

Documentação instalada descoberta e lida integralmente por `meta/documentation`: **12 documentos / 14 páginas**, UTF-8 concatenado idêntico ao instalador; guard da revisão antiga retornou revision_conflict, caminho fora da allowlist retornou not_found. Índice inclui configuração, operação, contratos/schemas, SDK, segurança, migração, diagnóstico e changelog. Evidências em evidence/documentation-validation.json e site-validation.json. No site, a sonda meta/create-job com conexão inexistente retornou not_configured, provando passagem da chave de domínio pelo MCP 0.24.0 sem criar job; não reproduziu o bloqueio antigo da 0.22.

Sem mudanças de layout nesta rodada: não repetido QA visual em navegador. Renderização administrativa e autorização foram exercitadas nativamente. Todos os laboratórios foram encerrados; nenhum serviço de teste ficou ativo. O site ficou com ambos os sociais 0.3.0 ativos.

## 5. Banco, atualização e reversão

Sem mudança de schema/tabelas, formato de cifra ou migração destrutiva. A atualização preserva conexões cifradas, opções, seleção de ativos, grants, agendas, páginas de resultado, histórico e diário. A prova de atualização usa registros reais semeados na 0.2.0, incluindo pais expirados e progresso; não é só ativação vazia. Dados históricos não ganham diagnósticos novos retroativamente.

Backup do instalador é pré-imagem de **arquivos**, não snapshot do banco; database_effects_reversible=false é reportado pelo MCP. Para reverter, interromper novas coletas, preservar banco e salts compatíveis, restaurar a pré-imagem ou instalador 0.2.0 de hash acima pela mesma pasta e conferir status/REST. Não executar uninstall como forma de atualização. A 0.3.0 não desfaz efeitos externos executados durante operação; restauração de arquivos não desfaz assinatura, publicação ou dados já coletados. Nesta rodada não houve esses efeitos reais. Reversão efetiva não foi acionada, pois as sondas passaram; não é declarada como teste executado.

## 6. Pendências e limites

| Pendência | Motivo/estado | Responsável e aceite |
|---|---|---|
| MCP Meta 9: Página Fator3 372814976700025, conexão instagram-fator3tech | Não configurada no fator3-teste; nenhuma chamada à Graph com essa credencial foi feita | Dono da conexão: executar 14 dias de page_follows e comparar datas/semântica com Porter, ou registrar recusa precisa com HTTP/code/subcode; mantenedor Meta analisa o resultado |
| CTO Page 1365937263259106 e demais Páginas autorizadas | Sem prova de fornecedor nesta rodada | Dono da conexão: repetir validate-connection por Página selecionada; seguidores zero ou não zero não comprovam escopo |
| Recusa de debug_token | Implementação retorna unknown/null, preservando recusa numérica, sem concluir permissão negada | Administrador do app: conferir token, app e escopos no ambiente autorizado; reenviar somente evidência sanitizada |


Não executados: homologação de API real, ensaio dedicado de HTTP 429 nesta rodada, rede/infraestrutura de todas as variantes MariaDB/multisite e QA visual completo. O mínimo foi comprovado no ambiente declarado, não em todas as combinações possíveis. A prova mínima não inclui o trio atual, que possui requisitos próprios mais altos. Leitura pública da documentação Meta teve bloqueio HTTP 429; não se usou isso como prova da causa do vazio. Causa/semântica de dados reais permanecem sujeitas ao aceite externo indicado. Mantenedor social responde por eventual ajuste após evidência; administrador do ambiente por acesso/configuração; dono da frota pela decisão de distribuição.

## 7. Configuração e credenciais

Em **Ferramentas → Fator3 MCP Meta**, cadastrar conexão com token manual do Facebook Login, versão Graph (padrão implementado v24.0) e seleção explícita de Instagram/Páginas. App ID e app secret existentes são usados na inspeção quando fornecidos; o token de Página é derivado e permanece privado. Sem App ID/secret, a inspeção usa a credencial de origem e pode ser recusada; isso retorna estado desconhecido, não autorização fictícia.

Executar meta/validate-connection para cada Página selecionada com connection_id, channel=facebook e account_id. Conferir page_permissions.permissions_verified, is_valid, read_insights_granted e pages_read_engagement_granted; booleano false e null têm significados distintos. Concessão granular para outra Página não atende o ativo consultado. Depois executar a coleta com nova chave idempotente: resultados antigos não recebem códigos retroativamente. Repetir configuração não implica aquisição automática de escopos.

Pixel/CAPI e captação comercial permanecem no Core. A descrição exata foi mantida como solicitada; gestão de anúncios Meta/Instagram permanece no MCP oficial da Meta, conforme fronteira do projeto. Este plugin não incorpora essa gestão.

Entradas humanas de configuração, consulta e ajuda exigem manage_options validado no servidor. Nenhum token/segredo real aparece neste relatório, no fonte ou em respostas de configuração; fixtures usam valores sintéticos identificados. Requer banco com InnoDB/bloqueios nomeados, sodium ou AES-256-GCM, HTTPS de saída e WP-Cron/cron real. Nenhuma nova exportação para Sheets, migração Porter ou BigQuery foi incluída. A comparação com Porter é critério de aceite, não migração de dados.

## 8. Artefatos finais

| Artefato | Bytes | SHA-256 |
|---|---:|---|
| `wp-mcp-meta-fator3-0.3.0-instalador.zip` | 89768 | `0f77360b0afca8c1040c411d7bd8b56a431428993f78b9d1504384fce8b6dd03` |
| `wp-mcp-meta-fator3-0.3.0-fonte.zip` | 257148 | `6d7d55fae3734f2b9fbcbb86f1e7d936601629b76d05b08525acd8ad8365dc39` |

Relatório externo: `wp-mcp-meta-fator3-0.3.0-relatorio.md`. Encaminhamento: `wp-mcp-meta-fator3-0.3.0-impacto-wp-mcp-fator3.md` (revisão 2).

Somente o instalador é instalável no WordPress, com raiz `wp-mcp-meta-fator3/`. O fonte tem raiz única `wp-mcp-meta-fator3-0.3.0-fonte/`, runtime em plugin/wp-mcp-meta-fator3/, templates/build, testes, evidências sanitizadas, entradas e relatório anterior ao fechamento. Nenhum ZIP contém outro ZIP. Sem credenciais, banco do laboratório, cookies ou dependências binárias. README.md explica reconstrução e matriz de testes. O relatório externo fornece a identidade definitiva do fonte sem circularidade.
