# Entrega — Fator3 MCP LinkedIn 0.2.0

Revisão: 1 · Data/hora: 2026-10-16T13:00:13+00:00 · Rodada: implementação da próxima versão planejada
Slug: `wp-mcp-linkedin-fator3` · Versão/build: 0.2.0 / release-20261016
Status: **com-pendencias** — apto para instalação, administração, REST e funções locais no escopo testado; homologação de fornecedor e escritas idempotentes pelo MCP 0.22 têm pendências explícitas.

## 1. De onde esta versão entra

Instalação limpa e atualização direta da 0.1.0; nenhuma versão intermediária exigida. Base imutável: `wp-mcp-linkedin-fator3-0.1.0-instalador.zip`, SHA-256 `6112381105bd60de42c61b47b7831aaefe94fbb88971eb79a4c7f6315a6c8999`. Os fontes 0.1.0 e o planejamento recebido foram usados como referência, sem sobrescrever seus arquivos.

Requisitos mínimos comprovados: **WordPress 6.4 e PHP 8.1.2-1ubuntu2.26 de 64 bits**. Ambiente atual local: WordPress 7.1.2/PHP 8.3.6/MySQL 8.0.46. Site fator3-teste: WordPress 7.1.3/PHP 8.3.30/MySQL 8.0.41. Criptografia autenticada e bloqueios InnoDB verificados. As entradas humanas exigem manage_options.

## 2. Convivência e encaminhamentos

Core 1.33.0, MCP 0.22.0 e Google 0.10.0 conviveram no laboratório; Google 0.9.0 foi preservado no fator3-teste. Ambos os plugins 0.2.0 estão ativos no site. Não foi alterado código de acompanhantes. Instalação e funções próprias não dependem da ordem nem da presença dos outros plugins; o transporte MCP é opcional.

| Destinatário | Versão examinada | Classificação | Ticket | Impacto individual |
|---|---|---|---|---|
| base-site-core-fator3 | 1.33.0 | acao-necessaria | R3-LI-01/02/03; I02/I03; S05 | [wp-mcp-linkedin-fator3-0.2.0-impacto-base-site-core-fator3.md](wp-mcp-linkedin-fator3-0.2.0-impacto-base-site-core-fator3.md) |
| wp-mcp-fator3 | 0.22.0 | bloqueio | Pedidos MCP 60; MCP-221-09; S01/S04/S06 | [wp-mcp-linkedin-fator3-0.2.0-impacto-wp-mcp-fator3.md](wp-mcp-linkedin-fator3-0.2.0-impacto-wp-mcp-fator3.md) |
| wp-mcp-google-fator3 | 0.10.0 no laboratório | sem-acao | S01/S04/S06 — fronteiras | [wp-mcp-linkedin-fator3-0.2.0-impacto-wp-mcp-google-fator3.md](wp-mcp-linkedin-fator3-0.2.0-impacto-wp-mcp-google-fator3.md) |
| wp-mcp-meta-fator3 | 0.2.0 | informativo | Pedidos 1/2 de ambos; retenção pai/filho | [wp-mcp-linkedin-fator3-0.2.0-impacto-wp-mcp-meta-fator3.md](wp-mcp-linkedin-fator3-0.2.0-impacto-wp-mcp-meta-fator3.md) |
| implantador-base | binário/versão atual não disponibilizados | nao-avaliado | Publicação e instalação da 0.2.0; decisão 89 | [wp-mcp-linkedin-fator3-0.2.0-impacto-implantador-base.md](wp-mcp-linkedin-fator3-0.2.0-impacto-implantador-base.md) |

Os cinco impactos são arquivos próprios e não foram enviados. O MCP 0.22 exige correção de transporte para operações que precisam receber idempotency_key; isso não impede painel/REST nem a instalação do plugin.

## 3. Mudanças e evidência

| Pedido exato | Problema | Mudança | Resultado e evidência |
|---|---|---|---|
| Pedidos MCP LinkedIn 1 | Documentação/identidade incompletas | Cabeçalho específico, artefatos próprios, 11 documentos/schemas e operação integral paginada | implementado; validado-wordpress e MCP |
| Pedidos MCP LinkedIn 2 | Entrada humana permissiva | manage_options e revalidação de usuário/tarefas; SDK concedido com usuário zero preservado | editor negado, consumidor autorizado testado |
| R3-LI-01 | Timeout contornável com nova chave/conexão | Diário persistido por recurso, migração de intenções antigas e bloqueio nomeado global por site | um POST após timeout; outras chaves/conexões/consumidores recusadas; dois processos testados |
| R3-LI-02 | Revogação entre pré-consulta e mutação | Guarda de grant/seleção/callback/principal imediatamente antes de POST/DELETE; recibo persistido antes da revalidação posterior | revogação prévia produz zero mutações; mudança em voo conserva efeito confirmado |
| R3-LI-03 | Sem consulta/reconciliação pública | SDK 1.1 negociado, get_subscription_operation/reconcile_subscription, revisão do diário e reatrelamento explícito | provider validado; I02/I03 do Core permanecem pendentes |
| Especificação Core §3 | Listagem limitada às primeiras concessões | list-grants/next_offset, get-grant, get-connection e estado efetivo | 106 grants percorridos; projeção precisa e isolamento verificados |
| Achado compartilhado com Meta 7 | Retenção do manifesto menor que as páginas | Job não removido enquanto restarem resultados; leitura offline continua autenticada | atualização com resultado de 100 dias preservado |
| MCP 60; S01/S04/S05/S06 | Fronteiras e transporte | Pages/Ads mantidos, nenhuma ingestão comercial; dependência do transporte explicitada | regressão CTR/CPC/CPM passou; chave retirada pelo MCP 0.22 reproduzida |

LinkedIn mantém social-reporting/1.0.0 e linkedin-lead-reader/1.0.0; acrescenta linkedin-lead-reader/1.1.0 por negociação. Entrypoint: Fator3\LinkedIn\PublicApi; registro via f3_linkedin_register_consumers. Registro não concede acesso. O consumidor precisa de grant ativo com revisão da conexão, formulários, permissões e callback exatos.

O diário considera owner/SPONSORED/formulário versionado e não usa conexão/consumidor/chave para liberar intenção equivalente. Um recibo confirmado sobrevive à mudança de autorização em voo. Sem ID, GET vazio não libera reenvio. Operação prepared comprovadamente sem despacho pode ser encerrada como rejected_before_dispatch. Reatrelamento com ID exige autorização explícita, aplicativo configurado preservado, grant atual e conferência do objeto remoto. Legado sem prova suficiente fica bloqueado para revisão; não há adoção automática.

O contrato 1.0 conserva falha de replay incerto. No 1.1, uma leitura bem-sucedida do diário pode indicar state=uncertain, o que não confirma criação. delivery_verified permanece false até homologação externa do consumidor. Callback, recibo antes de ACK, deduplicação, contatos e efeitos continuam no Core. Nenhum lead foi ingerido e nenhuma assinatura real foi criada nesta rodada.

Todos os schemas de entrada são fechados. Saídas conservam envelope success/code/data e erros estáveis; paginação, revisões e limites estão nos documentos instalados. CSV neutraliza fórmulas. HTTP usa host/caminho permitido, TLS, nenhuma redireção, limites de bytes/tempo e quota. Segredos não são projetados nem registrados em auditoria.

## 4. Instalação e prova da troca

No site autorizado, foi usado `plugins/upload-base64`, com `activate:true`, `overwrite:true`, `probe_timeout_seconds:30`, `expected_slug:"wp-mcp-linkedin-fator3"`, chave idempotente de instalação e SHA-256 da seção 8. Houve staging, pré-imagem, reativação em PHP novo e sondas anônimas de `/` e `/wp-json/` antes/depois: HTTP 200. A verificação de prontidão foi complementada por `linkedin/selftest`, documentação integral e inventário de arquivos; ativação isolada não foi tratada como homologação comercial.

O instalador final usa ZIP determinístico e seus bytes são os entregues. A URL prevista para a frota, **ainda não publicada nem testada**, é `https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-linkedin-fator3-0.2.0-instalador.zip`. Conferir hash e slug antes de instalar por raw. Esta rodada não publicou no GitHub e não certifica o fluxo de download raw.

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

Preserva `f3_linkedin_records`, opções e identidades existentes. Adiciona buckets de guarda por recurso e checkpoint da migração do diário em lotes de 50; não remove grants ou recibos legados. Estado incerto continua bloqueando novas intenções. Desativação/desinstalação da 0.2.0 conservam dados cifrados e removem apenas seus eventos cron.

Antes da atualização no site foi criado dump privado das duas tabelas sociais e options: artefato `fffeedf4848b9c1c77f5c877d931d249`, SHA-256 `841e49b8b2446336c341566e23feaeedc93921df2e8a26dca715bd8627e25203`. O dump contém dados originais e **não integra a entrega**. Pré-imagens 0.1.0: Meta `262babac5e4c204737f30d48`; LinkedIn `e2bdabf2bcfaa9a66f86e4f2`. Recibos posteriores estão em evidence/site-final-release.json.

Rollback precisa coordenar código, banco e salts do mesmo ponto, pausando cron/consumidores. Restaurar ZIP não desfaz migração nem efeito externo. Restaurar options inteiro pode reverter configurações de acompanhantes: revisar o escopo e mudanças posteriores antes de fazê-lo. Nunca executar uninstall da 0.1.0 como atualização/downgrade: ele apaga dados. Fonte/evidências não incluem wp-config, salts, dumps ou tokens reais.

## 6. O que permanece pendente

1. Homologar Pages/Ads e Lead Sync com aplicativo, produtos, escopos e ativos reais. Nenhuma conexão LinkedIn real estava cadastrada no fator3-teste (connection_count=0).
2. O Core deve integrar/selecionar o provedor e homologar I02/I03: challenge, assinatura, notificação, persistência antes do ACK, deduplicação, reconciliação e ingestão. Esta entrega implementa o lado do provider; não declara o Core alterado.
3. Intenções legadas incertas sem ID e sem prova de contexto permanecem bloqueadas. A resolução operacional precisa de evidência do fornecedor; apagar o diário ou trocar chave não é solução.
4. Corrigir MCP 60/MCP-221-09 para transportar a chave de domínio, depois repetir as escritas pelo MCP. Não foi modificado o MCP nesta entrega.
5. Revisão visual do painel em navegador real (bloqueio EPERM do ambiente); fluxos funcionais JavaScript/REST passaram.
6. Publicação raw, prova operacional do Implantador e decisão sobre publicação do fonte (89). Não foram presumidas autorizações de publicação ou envio.

Nenhum item é classificado como homologado-fornecedor. Fixtures e HTTP 200 do WordPress não demonstram escopo/aprovação comercial externa.

## 7. Credenciais e configuração do dono

Ferramentas > Fator3 MCP LinkedIn. Preencher connection_id, label, token, api_version, expires_at e ativos explícitos. Token vazio mantém o salvo; ativos vazios não concedem acesso. Somente administrador configura e consulta. Para Lead Sync: client_id, application_id, client_secret, contas/formulários e grant do consumidor registrado, com permissões e callback HTTPS exatos. Versão mensal padrão 202609. Produtos Pages/Ads e Lead Sync têm autorizações próprias; r_ads/rw_ads não concedem automaticamente respostas de leads.

Configuração local não é homologação de API. Não inserir segredos em relatórios, URLs de publicação ou tickets.

## 8. Identidade dos arquivos

| Artefato | Nome final e link | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-linkedin-fator3-0.2.0-instalador.zip](wp-mcp-linkedin-fator3-0.2.0-instalador.zip) | 79625 | `64da9956452d3943546758690cf5cb5ff6508cbf502780bbcc1ca1492e6e8324` |
| Fonte | [wp-mcp-linkedin-fator3-0.2.0-fonte.zip](wp-mcp-linkedin-fator3-0.2.0-fonte.zip) | 198591 | `a5b16da0d8c46fa2c09996b71b448a731a05db96d1657770b15786f689fd2b46` |

Relatório externo canônico: `wp-mcp-linkedin-fator3-0.2.0-relatorio.md`. O fonte contém uma **cópia anterior ao fechamento do fonte**: nela, tamanho/hash do próprio fonte ficam como “a preencher no relatório externo após empacotamento”. O conteúdo funcional/evidências é o mesmo; somente a identidade final do fonte é completada fora do ZIP. Cada fonte tem uma raiz `wp-mcp-linkedin-fator3-0.2.0-fonte/`, runtime em `plugin/wp-mcp-linkedin-fator3/`, build, testes e evidências. Nenhum ZIP contém outro ZIP.

Complementos: `entrega-meta-linkedin-0.2.0.md` (índice dos 16 arquivos obrigatórios) e `checksums-meta-linkedin-0.2.0.json`. Os cinco impactos individuais estão referenciados na seção 2. O fonte permite reconstruir o instalador com hashes idênticos; dependências de laboratório são declaradas, não instaladas no servidor do dono.
