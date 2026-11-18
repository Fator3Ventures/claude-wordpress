# Entrega — Fator3 MCP Google 0.38.0

Revisão 1 · 2026-11-18T20:02:07-03:00 · Implementação de **Pedidos MCP Google 56**  
Slug `wp-mcp-google-fator3` · Versão 0.38.0 · Build reproduzível identificado pelo SHA-256 da seção 8  
Status **com-pendencias**. A correção foi verificada em WordPress. O aceite em conta real e a incorporação do detalhe no e-mail oficial do Site Core permanecem abertos.

## 1. De onde esta versão entra

Instalação nova ou atualização direta do Fator3 MCP Google 0.37.0. A base é a última entrega do projeto, com instalador SHA-256 `2b3695f8d477c593a80c5a91cffac27761d14ed4d50d3d3454b625c6dda85ab5` e fonte SHA-256 `68decffc801a1e1a388914f883fdedef5b01dcbc38a59cfcd9fd449b58f02b12`. O avanço de minor segue o padrão do projeto. Slug, pasta, basename `wp-mcp-google-fator3/wp-mcp-google-fator3.php`, provider e identificadores públicos existentes foram preservados.

Requisitos declarados e exercitados na série mínima são WordPress 7.1.4 e PHP 8.3. O ensaio de instalação e atualização usou PHP 8.3.6 e MariaDB 11.8.6. O ensaio com a extensão experimental do Core também usou PHP 8.4.27. Documentos centrais lidos integralmente: `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos revisão 5 de 02/11/2026. A regra comum, o padrão Google, os relatórios acompanhantes e o pedido 56 de 18/11/2026 orientaram esta rodada.

## 2. Convivência e encaminhamentos

| Pacote ensaiado | Versão | Origem e verificação |
|---|---|---|
| Fator3 Site Core | 1.94.0 | Instalador e fonte recebidos nesta rodada. Inventário instalado conferido com o ZIP. |
| Fator3 MCP | 0.49.0 | Instalador e fonte recebidos nesta rodada. Transporte MCP HTTP autenticado usado nos testes. |
| MCP LinkedIn / Meta / Pipedrive | 0.26.0 / 0.29.0 / 0.12.0 | Instaladores disponíveis no projeto e na bancada, conferidos contra as pastas ativas. |
| Fator3 MCP Google | 0.38.0 | 209 arquivos do instalador conferidos após instalação. |

O conjunto tem 311 habilidades Google, 123 de leitura e 188 de escrita, e 46 definições de configuração. Versões de contrato: configuração 4.0.0, catálogo 3.0.0, execução 2.0.0 e armazenamento 2.0.0. Sem nova habilidade ou campo obrigatório de entrada. A atualização adiciona `metadata_state`, `required_permission`, `project_id` e `action` ao diagnóstico da chave.

| Destinatário | Classificação e situação | Referência | Encaminhamento |
|---|---|---|---|
| Site Core 1.94.0 | Desenvolvimento de contrato · acao-necessaria · aberto | Pedidos MCP Google 56 | `wp-mcp-google-fator3-0.38.0-impacto-base-site-core-fator3.md`, revisão 2 |

Com Core 1.94.0 e MCP 0.49.0 ativos, o Google 0.38.0 já entrega o diagnóstico correto e o Core registra uma única autorização recusada. O detalhe pode ser lido no painel Google, em `google/alerts`, `google/readiness-status` e `google/service-account-key-status`. Este material inclui uma proposta testada para o mantenedor do Core para exibir a permissão e o projeto no próprio registro e na mensagem. A proposta de planejamento e sua evolução constam de `planning/038.md` e `impacts/038/` no fonte. Nenhuma alteração de transporte foi requerida do MCP. A mudança de diagnóstico não altera APIs comerciais de Meta, LinkedIn ou Pipedrive.

## 3. Mudanças e evidência

| Pedido | Sintoma ou condição | Comportamento entregue e observado |
|---|---|---|
| Pedidos MCP Google 56 | Na 0.37.0, o mesmo HTTP 403 na consulta de metadados gerava `credencial_invalida` e `integracao_indisponivel`. | Os dois incidentes foram reproduzidos com a base original. A 0.38.0 registra “Validade da chave não consultável”, indica `iam.serviceAccountKeys.get` e o projeto da conta. No Core oficial fica um episódio aberto com `autorizacao_recusada`. |
| Pedidos MCP Google 56 | Atualizar um site com os dois falsos positivos já abertos. | O executor reconsulta o estado legado e encerra os episódios antigos correspondentes. O histórico é preservado. A repetição do mesmo 403, incluindo a passagem do coletor do Core, manteve um único episódio. |
| Pedidos MCP Google 56 | GA4 autorizado e metadados IAM inacessíveis. | A chamada nativa de relatório GA4 com token válido recebeu uma linha do provedor simulado. Uma leitura IAM posterior bem-sucedida encerrou o episódio. A última validade conhecida sobreviveu a uma falha posterior de consulta. |
| Pedidos MCP Google 56 | Distinguir falha IAM de rejeição da identidade. | O ensaio diferenciou API desabilitada, indisponibilidade 503 e `invalid_grant` na troca de token. Este último abriu `credencial_invalida` e impediu a chamada IAM. Um novo token válido com consulta bem-sucedida encerrou o episódio. |

A observação mudou apenas para o endpoint de metadados da chave da conta de serviço. O publicador mantém o destino técnico sob controle do Site Core. A consulta local da validade lê o estado salvo. O identificador de projeto vem do campo público da conexão. Se estiver ausente ou inválido, a orientação indica o projeto da conta e o campo estruturado fica nulo.

## 4. Instalação e prova da troca

Instalar o ZIP da seção 8 no WordPress. Na atualização, substituir o plugin de mesmo slug. Em requisição nova, `google/status` retornou `plugin_version=0.38.0` e `abilities_registered.total=311`. `google/integration-status`, com `compact=true`, retornou `read_success=true`. `google/storage-status` retornou `storage.ready=true`, `state=ready`, e as tabelas lógicas `records` e `cron` disponíveis. O MCP do laboratório retornou `metadata_state=permission_denied`, a permissão e `lab-038` para a chave sintética.

Para distribuição pela frota, usar `plugins/upload` com `expected_slug=wp-mcp-google-fator3`, `expected_sha256` da seção 8, `overwrite=true` e `activate=true`. URL raw prevista, pendente de publicação autorizada: `https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-google-fator3-0.38.0-instalador.zip`. O fonte é entregue separadamente e fica fora da publicação pública conforme decisão 89. O estado de publicação não foi atestado.

| ID | Prova | Resultado | Evidência em `evidence/038/` |
|---|---|---|---|
| 38-01 | WP 7.1.4, base 0.37.0 e atualização via instalador nativo | 3 verificações na base e 14 na atualização. Bytes da credencial preservados e falsos positivos encerrados. | `base.json`, `upgrade.json` |
| 38-02 | Instalação limpa Google sozinho e junto aos acompanhantes oficiais | 37 verificações isoladas e 14 verificações do pedido com Core original. | `isolated.json`, `clean.json` |
| 38-03 | Aceite da leitura `f3base/incidentes-tecnicos-ler` via MCP HTTP | Core oficial retornou só `autorizacao_recusada` em aberto para Google. A cópia ajustada também expôs permissão/projeto. Papel assinante recusado na leitura e na atualização de chave. | `core-http-oficial.json`, `core-http-experimental.json` |
| 38-04 | Cópia de teste Core e conteúdo do e-mail interceptado | 16 verificações. Abertura com permissão/projeto e enriquecimento de registro já aberto sem novo envio. | `patch.json`, `core-backfill.txt` |
| 38-05 | Documentação instalada pelo MCP HTTP | Em instalação limpa e após atualização, 26 documentos lidos em 89 páginas por instalação, 119 verificações cada. Bytes, revisão e SHA-256 recompostos e caminho fora do índice recusado. | `docs-clean.json`, `docs-upgrade.json` |
| 38-06 | Chromium com sessão administrativa nas larguras 360, 768 e 1440 px | 48 visitas a seções ou subpainéis, três capturas adicionais do cartão de validade. O texto com a ação e o projeto foi verificado nas três larguras. | `ui/cases.json`, `ui/iam-*.png` |
| 38-07 | Build e regressão | 1.366 testes, 16.367 asserções, zero falhas ou pulos no executor compatível. Lint dos 205 arquivos PHP instalados em cada um dos dois runtimes. 54 exemplos no verificador documental. | `unit.json`, `lint.json`, `documentation-build.txt` |
| 38-08 | Prontidão e paridade | 6 pastas conferidas contra os ZIPs oficiais da bancada, incluindo restauração do Core original. Nova geração determinística do instalador resultou no SHA-256 da seção 8. | `readiness.json`, `package-parity.json`, `local-plugins.json` |

**Estado final.** No laboratório, WordPress limpo com seis pacotes ativos, Core oficial restaurado, zero credenciais Google configuradas, zero tarefas de teste e zero senhas de aplicação. As sessões e os interceptadores temporários foram descartados. No Site-Teste compartilhado, a consulta de inventário mostrou Google 0.37.0, Core 1.94.0, MCP 0.49.0, Meta 0.29.0, LinkedIn 0.26.0 e Pipedrive 0.12.0. A conexão consultada retornou `applicable=false`, `known=false`, e a leitura de incidentes estava sem episódio Google aberto. O site foi consultado e continuou na versão anterior.

## 5. Banco, migração e correção por nova versão

O banco mantém o contrato de armazenamento 2.0.0. A mudança reutiliza a opção de estado IAM e as tabelas existentes de registros e cron. O monitor identifica a chave ativa, mantém a última validade conhecida e distingue o resultado da observação atual. A transição encerra somente classificações antigas correlacionadas à URL IAM de metadados. O processamento dos registros de acesso antigos é limitado a 100 candidatos por passagem. A atualização não concede papéis IAM nem rotaciona chaves.

Antes da instalação real, preservar banco, estado persistente e chaves de cifra do site. Na retomada, conferir o executor, a última consulta, os incidentes abertos e as notificações já aceitas pelo Core. Uma notificação entregue antes da atualização continua no histórico da caixa postal. Qualquer correção após instalação exige versão nova.

## 6. O que permanece pendente

1. **Frota e dono do projeto Google.** Selecionar um dos sites afetados que ainda esteja sem `iam.serviceAccountKeys.get` e tenha acesso funcional ao GA4. Instalar o artefato identificado, consultar a validade, executar uma leitura GA4 autorizada e consultar `f3base/incidentes-tecnicos-ler`. Para esse episódio, o resultado esperado é um aberto com `autorizacao_recusada` e zero abertos com `credencial_invalida` ou a indisponibilidade antiga. Conservar os registros recuperados no histórico. Os 11 sites são a abrangência informada pelo pedido; a rodada não os inspecionou individualmente.
2. **Mantenedor do Core.** Incorporar e versionar o tratamento do contexto IAM do impacto revisão 2. A emissão do lado Google e a prova local já estão prontas. O e-mail oficial da 1.94.0 ainda é genérico. A operação deve verificar o recebimento no destino técnico após a incorporação.
3. **Operação.** Publicação raw e troca compartilhada via hash/slug pendentes. O Site-Teste consultado estava sem conta de serviço configurada para este aceite. O teste em bancada interceptou as respostas Google e o correio no WordPress. OAuth, Google IAM, GA4 e SMTP externos não foram acionados; Ads, Sheets e Cloud Shell reais também ficaram fora dos ensaios.
4. **Limites da prova.** Regressão pelo executor de asserções compatíveis, sem o PHAR PHPUnit ou a matriz histórica completa de promoção. A verificação visual abrange um navegador e o cartão alterado. Não se aferiu acessibilidade integral nem os fluxos comerciais completos dos acompanhantes. A interface de implantação remota ficou sem ensaio do candidato até que exista a URL raw.

## 7. Credenciais e configuração do dono

No WordPress, abrir **Ferramentas → Fator3 MCP Google → Conexão → Identidade** e selecionar a conexão. A atualização aproveita a credencial já cifrada. Para a prova solicitada, observar a recusa antes de alterar as permissões. A permissão de consulta de metadados é `iam.serviceAccountKeys.get`. Depois de concluir o aceite e, se o dono autorizar, conceder essa permissão no âmbito da conta de serviço e consultar novamente. O cartão deve apresentar o dado atualizado e o incidente deve recuperar. Verificar o destino de e-mail técnico no Site Core. Não é necessário inserir uma nova chave para corrigir a classificação.

## 8. Identidade dos arquivos

| Artefato | Nome | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `wp-mcp-google-fator3-0.38.0-instalador.zip` | 992089 | `1ddeb8ef6aa734a3f8c6a95baadd2c3b6256d84e4bbbdb55d781300b8f407e33` |
| Fonte | `wp-mcp-google-fator3-0.38.0-fonte.zip` | 23125927 | `c2653ba3331dd2de55249966e486b2dc6f1e968fed9f31d54e2057fcbfc60716` |

Este é o relatório externo canônico. A cópia no fonte antecede seu fechamento; o tamanho e o hash definitivos acima foram calculados a partir do ZIP entregue.

O instalador tem raiz `wp-mcp-google-fator3/`. O fonte tem raiz `wp-mcp-google-fator3-0.38.0-fonte/`, código, build, roteiro, testes, evidências sanitizadas e relatório. O relatório individual para o Core está identificado na seção 2 e inclui o diff experimental integral.
