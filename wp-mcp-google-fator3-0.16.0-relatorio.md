# Entrega — Fator3 MCP Google 0.16.0

Revisão 1 · 2026-10-21T01:44:59-03:00 · Rodada: implementação · Status: **com-pendencias**; apta no escopo local testado. Pedidos MCP Google 30, 31 e 32 implementados. Aceites remotos não encerrados.
Slug/basename: `wp-mcp-google-fator3/wp-mcp-google-fator3.php`; provider, namespaces, Text Domain e Update URI preservados.

## 1. Bases aceitas

Instalação limpa e atualização direta Google 0.15.0 → 0.16.0. Base: `wp-mcp-google-fator3-0.15.0-instalador.zip`, 742908 bytes, SHA-256 `a7014e419c1a1a79d9a9e02112fd8f5b285fed131b50e10ea26f588d2179b169`. Fonte-base: 3142995 bytes, SHA-256 `3d2be60367a25c649462fdd913303a6d69d12a2079c7924994174e71544e34ef`. ZIPs fechados da base não foram alterados.

Pedidos recebidos: Fator3 MCP Google(6).md, situação 21/10/2026. Normas Fator3 r4 de 16/10/2026. Core recebido: fonte 1.42.0, SHA-256 `219399346190d57c804a273cdff9be3076f5b494ebf90843f69be6b525a078f0`; instalador 1.42.0, SHA-256 `280f54f8afb58301fb686a659003d432195c62dbfb5b52d055a022335cf3aeac`. O relatório externo Core anexado não ficou disponível; foi lida a cópia interna anterior ao fechamento, sem tratá-la como o relatório externo faltante. A prova de comportamento desta rodada é própria, sobre código e instaladores recebidos.

## 2. Convivência e encaminhamento pertinente

Validados WordPress 7.1.2, PHP 8.3.6 e MySQL 8.0.46, MCP 0.24.0, Core 1.42.0 original e acrescido da dependência implementada. Meta/LinkedIn 0.3.0 participaram como sentinelas de preservação no upgrade. Google isolado mantém funções próprias e ajuda administrativa local.

**Há modificação necessária no Core:** consultar recibos Ads de linhas incertas, sem executar nova ingestão. Código entregue em `wp-mcp-google-fator3-0.16.0-dependencia-base-site-core-fator3.zip`; impacto único `wp-mcp-google-fator3-0.16.0-impacto-base-site-core-fator3.md`, revisão 2, acao-necessaria, integração do responsável Core pendente. Foi implementado sobre a base exata, sem aguardar retorno do Core. O pacote é fonte de dependência, não uma release Core instalável. O Core deve incorporá-lo em sua própria próxima versão. Não alterar o instalador 1.42.0 já publicado.

Ads fica indisponível no Core original com `core_async_unsupported`; GA4 continua utilizável. A leitura do ID de medição GA4 usa contrato Core existente, sem nova alteração nesse ponto. Nenhum encaminhamento foi criado apenas para avisar versão; não houve modificação MCP/Meta/LinkedIn nem envio a terceiros.

## 3. Mudanças por pedido e evidência

**30 — administração:** menu único com Conexão, Conversões, Search Console, GTM, Incidentes e Avançado; navegação em pílulas. ID GA4 lido do Core, sem campo próprio na tela. Listas por nome para conta/ação Ads, propriedade/fluxo e conta/contêiner GTM, carregadas explicitamente e sem escolha automática. Rótulos em português, permissões em caixas de seleção, incidentes com nome e orientação, perfis GA4 estruturados por linhas e seletores. JSON concentrado em Avançado, com consulta por opção. Campo Request ID removido da configuração. Renderização das seis abas e POST administrativo de perfil com nonce exercitados; aceite visual em navegador pendente.

**31 — renovação:** executor existente tenta renovar após 12 horas uma prova de 24 horas, com concessão administrativa persistida e as mesmas consultas manuais. GA4 confere fluxo/segredo na Admin API e debug sem coletar evento; Ads faz leitura da ação e validateOnly. Falhas preservam a prova até expirar, registram incidente, avisam admin_email e repetem em 5/10/20/40/60 minutos. Alteração de identidade, segredo, destino ou autorização exige nova verificação. Status expõe última tentativa, resultado e próxima. Testes cobrem execução pelo cron, falha, espera crescente, aviso único aceito por wp_mail, recuperação e segredo alterado. Aceitação de e-mail no teste não é entrega à caixa postal; dois dias reais não foram simulados como aceite.

**32 — Data Manager:** ingestão de um evento e um destino por request, gclid/gbraid/wbraid, transactionId igual ao record_id, consentimento e valor/moeda da ação na última verificação. Mantidos sendBound, prontidão e vínculo ao destino. Intenção persistida antes do HTTP, recibo durável e nenhuma reingestão automática de resultado incerto. Consulta posterior requestStatus, começando após 30 minutos; SUCCESS com destino e contagem igual a um confirma o único evento daquele request. Essa identificação decorre da cardinalidade controlada: a API não devolve vetor por evento. Parcial, duplicidade, timeout, divergência ou falta de recibo ficam incertos; recusa exige prova de não entrega. Verificação usa validateOnly e aceita resposta vazia bem-sucedida, sem exigir recibo legado. Método upload-click-conversions é bloqueado antes do HTTP quando falta prova vigente de elegibilidade legada. Selftest e guia distinguem credenciais/escope Data Manager da consulta Google Ads API.

Permanecem 286 abilities (111 leitura/175 escrita), 36 opções, configuração 4.0.0 e execução/armazenamento 2.0.0. `site-conversion-delivery/1.0.0` preservado; extensão aditiva `site-conversion-reconcile/1.0.0`. Schema de status recebe campos opcionais de renovação/reconciliação. Entradas legadas measurement_id e eligibility_receipt são aceitas por compatibilidade, respectivamente substituída pelo valor Core e desnecessária na nova verificação. Não há nova ability de envio público, captura comercial paralela ou transferência de tags/consentimento.

## 4. Instalação e prova de prontidão

**553 verificações aprovadas: 493 em WordPress nativo e 60 puras; zero falhas na matriz final.** Lint aprovado em 154 arquivos PHP de runtime; instalador com 158 arquivos. Adicionalmente, quatro verificações do aplicador Core, lint do arquivo Core e reprodução exata do acompanhante exclusivo de bancada.

| Grupo | Percurso | Verificações WordPress |
|---|---|---:|
| clean | clean / mcp-first | 221 |
| upgrade | upgrade / mcp-first | 195 |
| core142 | clean / google-first | 55 |
| isolated | clean / google-only | 22 |

Evidência: `plugin/wp-mcp-google-fator3/evidence/016/validation016.json`, SHA-256 `684483dc3b166a27a0d970fdcf4e4bd5e76cd51eca97d8aac588c25b794e369e`. `tools/release016.py` vincula bytes do candidato, runtime, testes, ferramentas e inventários finais. Não equivale ao gate integral histórico PHPUnit/tools/validate.py nem aos gates completos do Core. Todas as respostas Google e e-mails da matriz são simulados; WordPress, banco, POST administrativo e transporte HTTP MCP são reais em laboratório descartável.

Upgrade por MCP local autenticado, com hash/slug, preservou configurações, segredo cifrado, conexões, registros, jobs, agendas e sentinelas sociais. Rollback restaurou inventário exato da 0.15.0; reaplicação devolveu o candidato exato. A primeira tentativa encontrou três arquivos novos que o rollback MCP não removia. As classes foram consolidadas nos módulos existentes, conservando o teste estrito; toda a matriz final foi repetida. Nenhuma alteração MCP foi necessária. Todos os processos de laboratório foram encerrados.

Documentação instalada: 20 documentos por `google/documentation`; schema, índice, paginação UTF-8, leitura integral/hash/tamanho e recusas de acesso/travessia/revisão foram exercitados pelo HTTP MCP. Leitura estática não chama Google. Guia atual `GUIA-0.16.0.md`; contrato detalhado `CONVERSION-DELIVERY-CORE-140.md` mantém nome histórico para compatibilidade.

Observações remotas somente de leitura em 21/10/2026: Site-Teste com Google 0.15.0, Core 1.42.0 e MCP 0.24.0 ativos (request `b30af6fd445fc96040b2f844`). ctooffice com GA4 pronto e Ads sem destino (request `6422cf866077c558fc3f9b5a`). Consulta de ações UPLOAD_CLICKS/ENABLED em 5347668213 retornou zero linhas (request `e380591e44ae5995a7dc5a58`); é necessário selecionar/criar a ação autorizada antes do aceite. Nenhuma conversão, configuração ou instalação remota executada nesta rodada.

Frota: publicar instalador/relatório na raiz raw autorizada, conferir o SHA-256 servido e instalar com `expected_slug=wp-mcp-google-fator3`, `expected_sha256` da seção 8, overwrite e activate, conforme schema MCP real. Atualizar Core com a extensão antes de habilitar Ads. Em seguida consultar google/status, google/selftest, google/documentation e configurar/verificar destinos pela tela ou abilities com revisão atual. Prontidão técnica não comprova atribuição comercial.

## 5. Banco e volta de versão

Sem nova tabela ou migração de schema. Metadados de renovação ficam na configuração existente por conexão; recibos mínimos no repositório indexado, tipo conversion; incidentes no repositório existente. Recibos guardam referência, identidade técnica e requestId, sem click ID, nome, e-mail, telefone ou payload comercial. São preservados para deduplicação; não apagar para tentar novo envio. Core preserva sua fila, registro e referência histórica.

Backup coerente de arquivos, banco e material de cifra é necessário antes da troca. Rollback de arquivos não desfaz banco nem conversões externas. A restauração de pré-imagem foi comprovada localmente, mas não é autorização para voltar com trabalho ativo/incerto. Ao voltar à 0.15.0, o adaptador Data Manager e sua renovação deixam de existir; suspenda o transporte Ads e preserve recibos/diários para reconciliação. Não reabra linhas incertas para forçar upload.

## 6. Pendências e responsáveis

- Core: integrar a dependência fornecida, repetir seus gates e fechar sua própria release. Não se declara concluído o trabalho desse responsável.
- Frota: publicação, instalação no Site-Teste/ctooffice, estado antes/depois e aceite de navegação em navegador. Chromium não estava disponível e o download falhou; somente HTML e POST nativo foram validados.
- Dono dos ativos/frota: habilitar API/escopo/acesso, selecionar ação importada e obter Ads ready true. Homologar registros 113 e 125 individualmente, uma conversão por registro, sem duplicação, respeitando os limites de 16/01/2027 e 18/01/2027 informados no pedido; depois primeiro contato real com gclid entregue. Não inferir record_id pelo número visual.
- Frota: dois dias contínuos de renovação em Site-Teste e ctooffice sem as tarefas externas de 08:41/20:41, depois ensaio autorizado de segredo revogado com incidente/e-mail antes da expiração. Essas tarefas não foram desativadas nesta entrega.
- Relatório externo Core 1.42.0 faltante permanece não avaliado; código, instalador e relatório interno foram examinados. Não há prova comercial, navegador/WebView, PHP-FPM, multisite/CDN ou runtimes diferentes dos declarados.

## 7. Credenciais, sem valores secretos

Conexão: conta de serviço ou OAuth, serviços/perfis de escrita e permissões por recurso. GA4: ID no Core, propriedade/fluxo na lista e segredo da API do fluxo; vazio preserva segredo, remoção é explícita. Ads: conta e ação Site — Importação de cliques ativa, com valor/moeda; token de desenvolvedor para descoberta/leitura Google Ads API, escopo adwords e projeto com acesso adequado à produção.

Data Manager: API habilitada, escopo https://www.googleapis.com/auth/datamanager, acesso Padrão ou Administrador da credencial à conta Ads; conta de serviço com Service Usage Consumer no projeto. OAuth existente requer novo consentimento se faltar escopo. Ingestão Data Manager não envia developer token nem depende do nível Explorer da Google Ads API. Verificação inicial e mudanças relevantes continuam administrativas. Nenhuma credencial de produção foi coletada ou incluída nos pacotes.

## 8. Identidade final dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | wp-mcp-google-fator3-0.16.0-instalador.zip | 756123 | `e0dfee63fbd9ad9fcc6b5ab9a3b9d492d7e497822154e0572589a45f3116248c` |
| Fonte | wp-mcp-google-fator3-0.16.0-fonte.zip | 3240644 | `3d3495b6959b42ff1b005d84c6b6a30bef4273105dcec35f1381489aae43b37d` |
| Dependência Core, não instalável | wp-mcp-google-fator3-0.16.0-dependencia-base-site-core-fator3.zip | 32811 | `9f4542b810b6b9817312beb236c782507a8bd589f182f19d83adbb525f630822` |

O relatório externo é canônico. A cópia interna é marcada como anterior ao fechamento do fonte e omite o hash do próprio ZIP, evitando circularidade. Fonte contém runtime idêntico ao instalador, documentação editável, build, testes, evidências sanitizadas, plano e impacto atualizado, além da dependência Core em fonte. Nenhum ZIP contém outro ZIP. Manifesto e checksums são complementares. Publicação e instalação remota continuam com a frota.
