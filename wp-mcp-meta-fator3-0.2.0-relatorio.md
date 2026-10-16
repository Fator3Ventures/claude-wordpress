# Entrega — Fator3 MCP Meta 0.2.0

Revisão: 1 · Data/hora: 2026-10-16T13:00:13+00:00 · Rodada: implementação da próxima versão planejada
Slug: `wp-mcp-meta-fator3` · Versão/build: 0.2.0 / release-20261016
Status: **com-pendencias** — apto para instalação, administração, REST e funções locais no escopo testado; homologação de fornecedor e escritas idempotentes pelo MCP 0.22 têm pendências explícitas.

## 1. De onde esta versão entra

Instalação limpa e atualização direta da 0.1.0; nenhuma versão intermediária exigida. Base imutável: `wp-mcp-meta-fator3-0.1.0-instalador.zip`, SHA-256 `4ce0a3446a55f634bb109662c2aacd83759c7d0a9b467d6a8706b17b917fb378`. Os fontes 0.1.0 e o planejamento recebido foram usados como referência, sem sobrescrever seus arquivos.

Requisitos mínimos comprovados: **WordPress 6.4 e PHP 8.1.2-1ubuntu2.26 de 64 bits**. Ambiente atual local: WordPress 7.1.2/PHP 8.3.6/MySQL 8.0.46. Site fator3-teste: WordPress 7.1.3/PHP 8.3.30/MySQL 8.0.41. Criptografia autenticada e bloqueios InnoDB verificados. As entradas humanas exigem manage_options.

## 2. Convivência e encaminhamentos

Core 1.33.0, MCP 0.22.0 e Google 0.10.0 conviveram no laboratório; Google 0.9.0 foi preservado no fator3-teste. Ambos os plugins 0.2.0 estão ativos no site. Não foi alterado código de acompanhantes. Instalação e funções próprias não dependem da ordem nem da presença dos outros plugins; o transporte MCP é opcional.

| Destinatário | Versão examinada | Classificação | Ticket | Impacto individual |
|---|---|---|---|---|
| base-site-core-fator3 | 1.33.0 | informativo | Pedidos MCP Meta 1/4/8; Core 216 | [wp-mcp-meta-fator3-0.2.0-impacto-base-site-core-fator3.md](wp-mcp-meta-fator3-0.2.0-impacto-base-site-core-fator3.md) |
| wp-mcp-fator3 | 0.22.0 | bloqueio | Pedidos MCP 60; MCP-221-09; S01/S04/S06 | [wp-mcp-meta-fator3-0.2.0-impacto-wp-mcp-fator3.md](wp-mcp-meta-fator3-0.2.0-impacto-wp-mcp-fator3.md) |
| wp-mcp-google-fator3 | 0.10.0 no laboratório | sem-acao | S01/S04/S06 — fronteiras | [wp-mcp-meta-fator3-0.2.0-impacto-wp-mcp-google-fator3.md](wp-mcp-meta-fator3-0.2.0-impacto-wp-mcp-google-fator3.md) |
| wp-mcp-linkedin-fator3 | 0.2.0 | informativo | Pedidos 1/2 de ambos; retenção pai/filho | [wp-mcp-meta-fator3-0.2.0-impacto-wp-mcp-linkedin-fator3.md](wp-mcp-meta-fator3-0.2.0-impacto-wp-mcp-linkedin-fator3.md) |
| implantador-base | binário/versão atual não disponibilizados | nao-avaliado | Publicação e instalação da 0.2.0; decisão 89 | [wp-mcp-meta-fator3-0.2.0-impacto-implantador-base.md](wp-mcp-meta-fator3-0.2.0-impacto-implantador-base.md) |

Os cinco impactos são arquivos próprios e não foram enviados. O MCP 0.22 exige correção de transporte para operações que precisam receber idempotency_key; isso não impede painel/REST nem a instalação do plugin.

## 3. Mudanças e evidência

| Pedido exato | Problema | Mudança | Resultado e evidência |
|---|---|---|---|
| Pedidos MCP Meta 1 | Cabeçalho e documentação genéricos | Identidade preservada; 11 documentos/schemas instalados, compilados da mesma fonte, índice e paginação UTF-8 com hash | implementado; validado-wordpress; leitura integral MCP |
| Pedidos MCP Meta 2 | Delegação a usuário não administrador | manage_options em painel/REST/abilities/arquivos/tarefas; revalidação do principal e ativo | implementado; editor na allowlist continua recusado |
| Pedidos MCP Meta 3 | Timeframe inválido e catálogo sem contexto | Catálogo por versão/canal/conexão; engaged_audience_demographics v24 recusa last_30_days antes do HTTP, publica this_month/this_week | validado-wordpress por fixture; catálogo completo real permanece pendente |
| Pedidos MCP Meta 4 | Ausência de Facebook | Canal facebook; page_profile/page_insights/page_posts/post_insights/page_videos/video_insights/page_audience/page_ratings; token privado de Página e proprietário de objeto | implementado; transporte/escopo testados; comparação real da Página CTO pendente |
| Pedidos MCP Meta 5 | Total de intervalo apresentado como série | Opt-in granularity=day; um dia por janela, grupos compatíveis; zero preservado e ausência explícita | 14 dias × 10 métricas = 140 linhas em duas páginas no cenário simulado |
| Pedidos MCP Meta 6 | Falta de backfill retomável | Plano com início explícito, final congelado em ontem UTC, checkpoint/retry/controle e limite declarado | dois anos completos simulados: 731 dias × 2 métricas = 1.462 linhas; aceite externo parcial |
| Pedidos MCP Meta 7 | Job expirava antes dos resultados | Pai preservado, histórico cifrado independente, deduplicação, retenção finita/ilimitada e CSV/JSON por partes | atualização de dados >90 dias, leitura offline e exportação verificadas |
| Pedidos MCP Meta 8 | Falta de captura periódica e rotação segura | Inventário+insights de mídia/Stories; snapshots com última observação bem-sucedida; revisão de autorização separada da geração de token; prova /me + /debug_token e escopos para rotação | fixtures, cron e propriedade testados; expiração/cron/quotas reais pendentes |

Meta mantém social-reporting/1.0.0 sem opt-in e anuncia social-reporting/1.1.0 para diário/Facebook/capturas. Namespaces, prefixos, REST e basename permanecem. Novas operações incluem rotate-token, history-status/history-migrate/history-query, create-backfill e history-export/history-export-step/history-export-read. O histórico não exige job_id, mas continua isolado pelo principal, conexão, conta e ativo autorizado. Mudança do conjunto invalida cursor/exportação com history_changed.

Retenção sem prazo vale para o histórico existente e próximas páginas; não ressuscita dados já removidos. Snapshot preserva o último valor por dia e a última observação bem-sucedida. Não arquiva binários. Rotação assistida requer Meta App ID/client_secret, prova do mesmo app/principal/escopos e até 12 ativos; save-connection trocando token invalida a autorização dos planos antigos. Não há deriva automática de data inicial quando o horizonte remoto é desconhecido.

Catálogo Facebook é conjunto fechado de candidatos, não equivalência com 276 campos Porter. A disponibilidade por versão/ativo e o inventário comparativo completo não foram homologados. Campos legados de demografia podem ser recusados pela origem. As famílias novas usam nomes prefixados page_* para conservar os nomes Instagram existentes. Nenhuma equivalência views/impressions foi presumida.

Todos os schemas de entrada são fechados. Saídas conservam envelope success/code/data e erros estáveis; paginação, revisões e limites estão nos documentos instalados. CSV neutraliza fórmulas. HTTP usa host/caminho permitido, TLS, nenhuma redireção, limites de bytes/tempo e quota. Segredos não são projetados nem registrados em auditoria.

## 4. Instalação e prova da troca

No site autorizado, foi usado `plugins/upload-base64`, com `activate:true`, `overwrite:true`, `probe_timeout_seconds:30`, `expected_slug:"wp-mcp-meta-fator3"`, chave idempotente de instalação e SHA-256 da seção 8. Houve staging, pré-imagem, reativação em PHP novo e sondas anônimas de `/` e `/wp-json/` antes/depois: HTTP 200. A verificação de prontidão foi complementada por `meta/selftest`, documentação integral e inventário de arquivos; ativação isolada não foi tratada como homologação comercial.

O instalador final usa ZIP determinístico e seus bytes são os entregues. A URL prevista para a frota, **ainda não publicada nem testada**, é `https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-meta-fator3-0.2.0-instalador.zip`. Conferir hash e slug antes de instalar por raw. Esta rodada não publicou no GitHub e não certifica o fluxo de download raw.

| ID | Ambiente | Cenário | Resultado | Evidência no fonte | Limite |
|---|---|---|---|---|---|
| QA-01 | WP 7.1.2/PHP 8.3.6 | Atualização 0.1.0 → runtime final, sociais antes do trio | 49 verificações passaram | evidence/native/lab-final-ui/native-tests.json e runtime-inventory.json | HTTP Meta/LinkedIn simulado |
| QA-02 | WP 6.4/PHP 8.1.2 | Instalação limpa no mínimo declarado | 46 verificações passaram | evidence/native/lab-minimum-release/ | Sem fornecedor real |
| QA-03 | WP 7.1.2/PHP 8.3.6 | Instalação limpa dos dois e fluxos de painel | 46 verificações nativas + 7 JavaScript/REST passaram | evidence/native/lab-ui-dom-final/ | DOM executado com jsdom; sem certificação visual |
| QA-04 | WP 7.1.2/PHP 8.3.6 | Meta sozinho e LinkedIn sozinho | 23 + 21 verificações passaram | evidence/native/lab-meta-alone/ e lab-linkedin-alone/ | Antes do último endurecimento; versão final revalidada em QA-01/02/03 |
| QA-05 | WP 7.1.2/PHP 8.3.6 | Trio antes dos sociais | 44 verificações passaram | evidence/native/lab-trio-01/ | Prova de ordem/isolamento, não de fornecedor |
| QA-06 | fator3-teste | Instalação e inventário final | 63/63 arquivos idênticos, sem extras ou symlinks | evidence/site-runtime-inventory.json e site-final-inventory.json | 33 Meta + 30 LinkedIn |
| QA-07 | fator3-teste/MCP | Documentação instalada | 22 documentos completos, conteúdo/hash iguais ao runtime; schemas em múltiplas páginas | evidence/site-documentation.json | Leitura local administrativa |
| QA-08 | fator3-teste/MCP 0.22 | Encaminhamento de chave idempotente | Bloqueio rest_property_required reproduzido com conexão inexistente; nenhuma coleta criada | evidence/site-final-release.json | Requer ação do MCP |
| QA-09 | Dois processos PHP/MySQL | Exclusão concorrente de assinaturas | Segundo worker recusado como busy, zero POST | teste LinkedIn concurrent worker em QA-01/02/03 | Concorrência local simulada, sem assinatura real |

O navegador Chromium foi impedido pelo host de criar seu socket (EPERM). A alternativa funcional carregou HTML/JavaScript servidos pelo WordPress, autenticou usuário de laboratório, salvou configuração via REST, leu ajuda, verificou seletor Facebook/histórico e diagnóstico. **A revisão visual em navegador real continua pendente.**

Estado final: Meta 0.2.0, LinkedIn 0.2.0, Core 1.33.0, MCP 0.22.0 e Google 0.9.0 ativos no fator3-teste; nenhuma conexão real foi adicionada. Dados sintéticos ficaram nos laboratórios locais e não foram enviados a fornecedores. Não há plugin QA temporário no site. Backups privados de banco/pacote foram mantidos para recuperação; a migração histórica vazia foi concluída.

## 5. Banco e volta de versão

Preserva `f3_meta_records`, opções e identidades existentes. Adiciona f3_meta_history e índices; migra páginas retidas em lotes de 25, sem depender do job pai e sem ressuscitar páginas expiradas. Chaves lógicas e geração de visão mantêm deduplicação/paginação consistente. Desativação/desinstalação da 0.2.0 conservam dados cifrados e removem apenas seus eventos cron.

Antes da atualização no site foi criado dump privado das duas tabelas sociais e options: artefato `fffeedf4848b9c1c77f5c877d931d249`, SHA-256 `841e49b8b2446336c341566e23feaeedc93921df2e8a26dca715bd8627e25203`. O dump contém dados originais e **não integra a entrega**. Pré-imagens 0.1.0: Meta `262babac5e4c204737f30d48`; LinkedIn `e2bdabf2bcfaa9a66f86e4f2`. Recibos posteriores estão em evidence/site-final-release.json.

Rollback precisa coordenar código, banco e salts do mesmo ponto, pausando cron/consumidores. Restaurar ZIP não desfaz migração nem efeito externo. Restaurar options inteiro pode reverter configurações de acompanhantes: revisar o escopo e mudanças posteriores antes de fazê-lo. Nunca executar uninstall da 0.1.0 como atualização/downgrade: ele apaga dados. Fonte/evidências não incluem wp-config, salts, dumps ou tokens reais.

## 6. O que permanece pendente

1. Homologar métricas e timeframes em ativos reais, incluindo Página CTO 1365937263259106 e comparação de 14 dias com mesma definição/fuso/escopo. O catálogo de 276 campos Porter e equivalências não está certificado; não preencher lacunas por inferência.
2. Demonstrar disponibilidade diária real de dois anos. O motor executou dois anos simulados, mas a API pode impor horizonte, supressão ou remoção. Pedido 6 permanece com aceite externo parcial; não declarar histórico integral recuperável.
3. Validar Stories/mídias após expiração, cron real, quota e rotação de token/app real. Nenhum token Meta real estava cadastrado no fator3-teste (connection_count=0).
4. Corrigir MCP 60/MCP-221-09 para transportar a chave de domínio, depois repetir as escritas pelo MCP. Não foi modificado o MCP nesta entrega.
5. Revisão visual do painel em navegador real (bloqueio EPERM do ambiente); fluxos funcionais JavaScript/REST passaram.
6. Publicação raw, prova operacional do Implantador e decisão sobre publicação do fonte (89). Não foram presumidas autorizações de publicação ou envio.

Nenhum item é classificado como homologado-fornecedor. Fixtures e HTTP 200 do WordPress não demonstram escopo/aprovação comercial externa.

## 7. Credenciais e configuração do dono

Ferramentas > Fator3 MCP Meta. Preencher connection_id, label, token, api_version, expires_at e ativos explícitos. Token vazio mantém o salvo; ativos vazios não concedem acesso. Somente administrador configura e consulta. Para preservar agendas na rotação: client_id (Meta App ID) e client_secret; validar app/principal/escopos e ativos. Definir retention_mode/retention_days, datas e cron conforme o uso. Graph padrão v24.0, sem promessa de todas as métricas para todos os ativos.

Configuração local não é homologação de API. Não inserir segredos em relatórios, URLs de publicação ou tickets.

## 8. Identidade dos arquivos

| Artefato | Nome final e link | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-meta-fator3-0.2.0-instalador.zip](wp-mcp-meta-fator3-0.2.0-instalador.zip) | 81332 | `f5cb81781038e487741adc3a1d82791f149d37a5219f7d4747b0acf9ae27d57f` |
| Fonte | [wp-mcp-meta-fator3-0.2.0-fonte.zip](wp-mcp-meta-fator3-0.2.0-fonte.zip) | 202590 | `e875060089708acbac061e617944b704829d3df618f80537a8a457f64f08b362` |

Relatório externo canônico: `wp-mcp-meta-fator3-0.2.0-relatorio.md`. O fonte contém uma **cópia anterior ao fechamento do fonte**: nela, tamanho/hash do próprio fonte ficam como “a preencher no relatório externo após empacotamento”. O conteúdo funcional/evidências é o mesmo; somente a identidade final do fonte é completada fora do ZIP. Cada fonte tem uma raiz `wp-mcp-meta-fator3-0.2.0-fonte/`, runtime em `plugin/wp-mcp-meta-fator3/`, build, testes e evidências. Nenhum ZIP contém outro ZIP.

Complementos: `entrega-meta-linkedin-0.2.0.md` (índice dos 16 arquivos obrigatórios) e `checksums-meta-linkedin-0.2.0.json`. Os cinco impactos individuais estão referenciados na seção 2. O fonte permite reconstruir o instalador com hashes idênticos; dependências de laboratório são declaradas, não instaladas no servidor do dono.
