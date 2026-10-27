# Entrega — Fator3 Site Core 1.57.0

Revisão 1 · Data: 26/10/2026, America/Sao_Paulo · Rodada: implementação e homologação.
Slug: `base-site-core-fator3` · Versão: **1.57.0** · Contrato administrativo: **8.22.0** · Status: **com-pendencias de homologação GA4 real**.

Implementada e ativa no Site-Teste. Pedidos 312 e 313 incorporados, com documentação instalada, 164 abilities e ciclo de 17 etapas concluído. O aceite de 30 dias com dados reais GA4 permanece pendente; não confundir a comparação controlada aprovada com uma propriedade real consultada. Não houve implantação na frota, publicação no GitHub ou envio a clientes.

## 1. De onde esta versão entra

Base direta aceita: Core **1.56.0**. Instalador de base: 2667464 bytes, SHA-256 `e9dd77379d64706ad37de2428dc91a02bdaeb0649f68b38d3024ffcaac4ebed9`; fonte de base: 3950523 bytes, SHA-256 `36b54c1711c39aaeb8e32c1ab1b77d84d58bc5c82de905b2699b50ae38aa9b85`. Não instalar versão intermediária.

Foram lidos o pedido `Fator3 Site Core(20261027-010228).md`, os relatórios/impactos recebidos e as normas comuns revisão 5, de 23/10/2026. As cópias do projeto ainda indicavam revisão 4; prevaleceu a revisão 5 já recebida, preservada em `inputs/1510`. O planejamento desta rodada está em `history/1570/PLANO.md`; entradas atuais em `inputs/1570`.

Piso declarado e testado: WordPress **7.1.2**, PHP **8.3.6 de 64 bits**. Também testados WordPress 7.1.3/PHP 8.3.6 no laboratório e WordPress 7.1.3/PHP **8.3.36** no Site-Teste. Banco local MySQL 8.0.46. Instalação limpa e atualização direta foram realizadas com o instalador final, por `Plugin_Upgrader` nativo, em bancos/conteúdos descartáveis separados.

## 2. Convivência e encaminhamentos

| Acompanhante ativo no Site-Teste | Versão | Fronteira examinada e prova |
|---|---|---|
| Fator3 MCP | 0.33.0 | Instalação, sondas, decorador original, autorização, documentação pelo canal |
| Fator3 MCP Google | 0.20.0 | `ga4-reader/1.0.0`; SDK e concessão reais em fixture isolada; Data API controlada; GSC não perde o cliente |
| Fator3 MCP Meta | 0.12.0 | `instagram-first-message/1.0.0` e `instagram-message-erasure/1.0.0`; consumidor Core, recibos e exclusão locais reais; Graph controlado |
| Fator3 MCP LinkedIn | 0.11.0 | Coexistência e análise dos contratos/relatório; nenhuma mudança no acompanhante ou nova prova de fornecedor |
| Fator3 MCP Pipedrive | 0.2.0 | Coexistência e relatório; `pipedrive-api-client/1.0.0` preservado; regressão CRM Core com transporte controlado |

Também permaneceram ativos DreamHost 1.0.0, WP Super Cache 3.1.4 e Yoast SEO 28.7. Nenhum acompanhante foi atualizado nesta rodada. Runtimes originais e suas identidades para reprodução estão em `build/COMPANIONS.md`; não são republicados dentro do fonte Core.

### Impactos e pedidos emitidos nesta rodada

Nenhum novo impacto técnico dirigido a outro pacote foi identificado no escopo 312/313. Os contratos necessários já foram entregues por Meta 0.12.0 e Google 0.20.0. A correção de descoberta GSC pertence ao Core. Não foi produzido arquivo de impacto para simples resposta ou encerramento, conforme revisão 5 das normas.

### Tratamento de impactos recebidos e anteriores

| Documento/pedido de origem | Responsável | Tratamento nesta 1.57.0 | Evidência e pendência |
|---|---|---|---|
| `wp-mcp-google-fator3-0.20.0-impacto-base-site-core-fator3.md`, revisão 1, Google 38 / Core 313 | Core | Implementado consumidor público, registro filtrado por contrato, callback `{property,revision,ready}`, concessão explícita, coletor/acervo próprios, cotas, retomada e metadados; sem ler opções ou segredos Google no runtime | `request-313.json` e `site-request-313.json`: 95 verificações. Comparação real depende de credencial/concessão; contrato entregue não equivale a aceite real |
| `base-site-core-fator3-1.56.0-impacto-wp-mcp-meta-fator3.md`, planejamento da 1.56.0; resposta do relatório Meta 0.12.0, seções 2/6; Core 312 | Meta entregou SDK; Core implementa consumo | O SDK recebido substitui a antiga indisponibilidade. Core preserva alvo cifrado antes da eliminação, chama exclusão após a persistência local e confere o recibo. Nenhuma alteração solicitada ao Meta nesta rodada | `request-312.json` e `site-request-312.json`: 25 verificações. Alvos já perdidos por versões anteriores não podem ser reconstruídos |
| Relatórios LinkedIn 0.11.0 e Pipedrive 0.2.0, retenção ampliada nos próprios namespaces | Respectivos mantenedores; Core na fronteira consumidora | Contratos Core preservados; não copiar políticas privadas nem declarar reimplementada a retenção dos acompanhantes | Coexistência instalada e regressões próprias. Não houve nova homologação de APIs LinkedIn/Pipedrive |

## 3. Mudanças e evidência

| Pedido exato | Problema anterior | Mudança | Resultado observado |
|---|---|---|---|
| 312(a–d) | A eliminação de Instagram limpava o contato Core e ficava sem alvo/SDK para apagar identificadores Meta | Outbox cifrado antes do expurgo; chave sem dado pessoal; SDK público de exclusão, revisão e conferência do recibo; alvo temporário destruído somente após recibo persistido; estado incluído na leitura do tombstone | Contato criado pelo consumidor real, eliminado nos dois componentes, `privacyStatus.local_identifiers_present=false`, reimportação bloqueada e mesmo recibo na repetição. Falha/transação aberta e retomada comprovadas |
| 313(a,b,f,g) | Ausência de acervo GA4 local e risco de misturar dimensão/cota com GSC | Sete recortes diários independentes, SDK Google 0.20.0, uma página por passagem, cursor cifrado, retroatividade configurável, reconsulta dos três dias recentes, cotas/backoff e registro de qualidade | 30 dias sintéticos iguais ao `ga/run-report` no mesmo recorte; paginação opaca real; vazio registrado como lacuna e recuperado; 429 e revogação sem novas linhas |
| 313(c,i) | Sem política de guarda nem inventário do acervo | `retencao_ga4_meses=0` por padrão; 1–120 meses apenas por escolha explícita; tamanho/índices no inventário | Guarda ilimitada e expurgo finito de cabeçalhos/linhas testados; pendências preservadas; Site-Teste vazio com 98304 bytes estimados incluindo índices |
| 313(d,h) | Dados GA4 não disponíveis ao lado da medição própria | Leitura, comparação e exportação MCP; painel Medição → Acervo GA4; relatório integrado `visao=ga4`, fontes separadas | Séries diárias e métricas brutas identificadas como GA4; nenhuma soma de usuários entre dias ou de fontes; CSV/JSON paginados com revisão e SHA-256 |

Configuração própria `f3base_ga4_acervo`: inativa por padrão; `propriedade`, `inicio`, `horario`, `fuso` e `recortes`. O horário da agenda usa o fuso do site; o fuso configurado delimita os dias da propriedade e deve corresponder ao GA4. Sem credencial própria, BigQuery ou chamada HTTP direta ao Google.

Recortes: resumo; página × dia; origem/mídia/campanha × dia; dispositivo × dia; país × dia; país/cidade × dia; evento × dia, incluindo eventos-chave. Métricas variam por recorte: usuários, sessões, sessões engajadas, duração do engajamento, visualizações, eventos e eventos-chave. Tipos/valores originais são preservados. Metadados de amostragem, thresholding, `(other)`, fuso, moeda, cobertura, cota e origem acompanham dia/página.

Novas abilities: `ga4-status`, `ga4-coletar`, `ga4-historico`, `ga4-lacunas-ler`, `ga4-acervo-ler`, `ga4-comparar`, `ga4-exportar`, todas no namespace `f3base/`, com autorização administrativa. Consulta/exportação: até 366 dias e 100 linhas por página; relatórios integrados com medição própria conservam sua janela de até 90 dias. Exportação detecta mudança da publicação durante a paginação e neutraliza fórmulas no CSV.

O acervo publica uma fotografia apenas ao concluir toda a paginação em persistência atômica. Fotografia parcial, falha e vazio não substituem a publicada. Transação SQL aberta pelo chamador é recusada, sem commit implícito. O coletor não interfere nas agendas/cotas do GSC. Falhas/ausência do SDK e concessão ausente ficam explícitas.

Instagram mantém retomada pela `f3base/leads-eliminar-registro` existente, com `simular=false` e revisão esperada. Execução sem administrador não assume identidade alheia: pendência Meta requer retomada administrativa. A exclusão é local no SDK Meta; não afirma apagar cópias no Instagram, Graph, backups ou terceiros.

## 4. Instalação e prova da troca

Site: `https://fator3-teste-mcp-1.dreamhosters.com/`. Troca direta 1.56.0 → **1.57.0**, ativa antes/depois, com `expected_slug=base-site-core-fator3` e SHA-256 da seção 8. O pacote foi transferido para arquivo temporário por partes verificadas e instalado por `plugins/upload-base64` com `zip_path`; o arquivo temporário foi removido. As duas tentativas anteriores de envio integral foram interrompidas sem confirmação; a auditoria e a versão foram consultadas antes da retomada. Não houve instalação duplicada observada.

Operação MCP `44a2cff40cab02bd00d87817`; operação de pacote `721ffd95af922d59e4eed0dc7740aae8`; pré-imagem de arquivos `501567f86d7b06f2d86d7790`. Home e `/wp-json/` retornaram 200 antes/depois, com bypass de cache verificado em sondas internas da mesma origem. Isso não certifica conectividade externa ou todas as páginas públicas.

Ciclo de instalação `5edf4a90-0a85-4970-9630-7c954e2482fc`: **17 etapas concluídas, zero falhas**, confirmação do executor e finalização observadas. O acionamento silencioso do instalador, isoladamente, não foi usado como prova dessa prontidão; a leitura posterior confirmou `estado=concluida`.

| Prova | Ambiente/cenário | Resultado | Evidência no fonte | Limite |
|---|---|---|---|---|
| Sintaxe/ZIP | PHP 8.3.6 | 541 PHP válidos; 743 arquivos de runtime | `evidence/1570/installer.json` | Não certifica comportamento por si só |
| Instalação limpa e upgrade | WP 7.1.3 e 7.1.2/PHP 8.3.6, quatro ciclos isolados | Instalador final; dados/escolhas/procedência preservados; tabelas novas prontas, GA4 desligado e retenção 0; repetição sem nova migração | `native-cycles-1570.json` e `min/native-cycles-1570.json` | Atraso de confirmação acelerado apenas no laboratório |
| Instagram 312 | WP real local e fixture isolada no Site-Teste/PHP 8.3.36, Meta 0.12.0 | 25 verificações em cada ambiente | `request-312.json`, `site-request-312.json` | Graph interceptado; exclusão local e SDK reais |
| GA4 313 | Google 0.20.0 real, transporte controlado, local e Site-Teste | 95 verificações em cada ambiente | `request-313.json`, `site-request-313.json` | Sem dados reais da propriedade |
| Persistência/UI/retenção | Local e Site-Teste | 16 verificações em cada ambiente | `review-1570.json`, `site-review-1570.json` | HTML renderizado pelo WordPress; sem validação visual em navegador |
| SDK indisponível | Local e fixture Site-Teste | 6 verificações; pendência explícita e alvo cifrado preservado | `sdk-unavailable-1570.json`, `site-sdk-unavailable-1570.json` | SDK desativado somente na fixture |
| Autorização | WordPress nativo, MCP 0.33.0 local e Site-Teste isolado | 16 verificações por cenário; revogação efetiva e acesso negado | `permissions-native-1570.json`, `permissions-mcp-1570.json`, `site-permissions-1570.json` | Sem alteração de permissões da instalação compartilhada |
| Regressões | Contatos externos, formulários, CRM Core | 69 + 32 + 39 verificações | `request-302.json`, `forms-1470.json`, `pipedrive-1470.json` | Transportes controlados |
| Documentação final | Runtime final copiado da instalação do Site-Teste, MCP original ativo | **132 documentos, 625 páginas, 915 verificações**, hashes/leitura integral, aliases, confinamento e recusas de acesso | `site-docs-1570.json` | Sem chamar fornecedor |
| Documentação pelo conector | Sessão MCP compartilhada | Índice, release, agentes, acervo GA4 e exclusão Instagram lidos integralmente, versão/hash 1.57.0 | `site-documentacao-mcp.json` | Leitura autenticada |
| Paridade instalada | Manifesto dos 743 arquivos | Exatamente igual ao runtime/instalador entregue | `runtime-parity.json`, `site-read.json` | Manifesto SHA-256 `5cc453c584ad2490131f2e18e3ebd05195b59c3804edc7a4b7b618101d292176` |

Uma repetição opcional da documentação no laboratório local, após a interrupção de sessão, não iniciou: o armazenamento descartável perdeu um arquivo de redo do MySQL. Isso ocorreu antes do bootstrap WordPress. A prova completa dos bytes finais foi concluída no Site-Teste; não se atribui aprovação à tentativa local não executada (`local-repeat-infrastructure.json`).

Documentação: `docs/DOCUMENTACAO.md` e `f3base/documentacao-ler` (`arquivo`, `linha`, `limite`), versão/hash e continuação. Especificações atuais: `RELEASE-1.57.0.md`, `AGENTES-1.57.0.md`, `ACERVO-GA4-1.57.md`, `INSTAGRAM-EXCLUSAO-1.57.md`; catálogo e schemas regenerados em `docs/dados`.

Estado final: Core 1.57.0 e acompanhantes da seção 2 ativos. Configurações compartilhadas conferidas sem alteração durante a leitura; captação WhatsApp/Instagram continua desligada, configurações de e-mail existentes preservadas. GA4 inativo, sem propriedade e sem concessão. **89 tabelas de fixture removidas**, pasta privada e manifesto removidos, controlador temporário removido e ability de QA não mais encontrada; ZIP temporário removido. Backups privados de recuperação permanecem no servidor. Sondas finais home/REST aprovadas.

## 5. Banco e volta de versão

Três tabelas novas: `{prefix}f3base_instagram_exclusoes`, `{prefix}f3base_ga4_coletas` e `{prefix}f3base_ga4_linhas`. Alteração aditiva, com configurações e inventário próprios; sem expurgo na atualização. A retenção GA4 padrão é 0 (sem prazo). Prazo positivo elimina dias anteriores ao corte mensal em lotes limitados e preserva coletas em curso/aguardando.

Outbox Instagram mantém apenas alvo cifrado enquanto pendente; após recibo verificado, limpa o alvo e preserva recibo mínimo junto ao tombstone. Esses recibos/pendências permanecem na desinstalação, acompanhando os registros comerciais. A desinstalação explícita remove o acervo analítico GA4, seguindo o desenho do GSC; não é uma rotina de expiração. Backups são necessários para restaurá-lo.

Antes da troca foi criado **backup privado integral no próprio servidor**, sem download do conteúdo: artefato `61e8c0659c6d50a07ed589acf7296b8e`, 28320538 bytes, 97 tabelas, 85955 linhas, SHA-256 `11f0a50093c11cbf47a4a0f51616cf104bf6c810912feb8e2bef78e472b034e2`. A primeira revisão automática bloqueou a operação por interpretar envio externo; após comprovação no código de que a operação grava cópia privada local, a criação foi permitida. Nenhum dump ou segredo entrou nos entregáveis.

A pré-imagem do instalador cobre arquivos, não desfaz banco ou efeitos externos. Reverter somente arquivos para 1.56.0 não remove tabelas novas nem reconstrói identificadores eliminados; a versão anterior não entende a outbox de exclusão. Prefira correção adiante. Para uma restauração completa, suspender os coletores, manter banco/arquivos e salts coerentes, preservar a guarda operacional corrente e reconciliar o estado antes de retomar. Uma restauração de backup pode reintroduzir identificadores que haviam sido apagados. Não foi executado downgrade real no Site-Teste.

## 6. O que permanece pendente

1. **Aceite GA4 real do pedido 313 / Google 38:** dono/mantenedor do site deve configurar credencial Google com acesso à propriedade, conceder o contrato ao Core e habilitar a coleta. No Site-Teste, `google/status` local retornou uma conexão `default`, `auth.configured=false`; `ga4-status` mostrou `not_granted`. Não foram fabricadas credenciais, alteradas concessões reais ou usado outro site para contornar isso. Após configuração, executar 30 dias, comparar com `ga/run-report` no mesmo recorte, conferir lacuna/recuperação e qualidade. A prova sintética aprovada não encerra esse aceite.
2. **Qualidade real de fator3.com.br:** ausência de `(other)` nas dimensões principais, ou agrupamento explicitamente informado, depende de consulta autorizada dessa propriedade. Metadados e agrupamento foram preservados nos testes controlados; a propriedade real não foi consultada nesta rodada.
3. **Instagram histórico:** contato eliminado antes de preservar o alvo pode mostrar `alvo_anterior_indisponivel`; a 1.57.0 não recupera dados apagados. Pendências com alvo cifrado são retomáveis por administrador. Homologações anteriores com conversa real, App Review e ativos Meta continuam separadas do aceite local de exclusão 312.
4. **Frota/publicação:** responsável pela frota deve conferir hash/slug e publicar os artefatos conforme as normas, quando autorizado. Esta entrega não publicou em `main` nem aplicou aos demais sites. Fonte permanece com o dono; nenhum encaminhamento foi enviado a terceiros.

## 7. Credenciais e configuração do dono

No Core: Configurações → Medição e anúncios → Acervo GA4; informar propriedade canônica `properties/123`, início retroativo, recortes, horário e fuso. No pacote Google: configurar OAuth/Service Account apropriado, serviço GA de leitura e concessão revogável `google/configure-consumer` para `contract=ga4-reader/1.0.0`, `consumer_id=base-site-core-fator3`, propriedade e conexão corretas, com `expected_revision` vigente. Só então ativar o coletor Core. Para manter a guarda ilimitada, deixar `f3base_retencoes_tecnicas.retencao_ga4_meses=0`.

Para Instagram, manter Meta 0.12.0 compatível; configurações de captura de ambos os lados continuam exigidas para contatos novos. A eliminação local exige `manage_options` e `f3base_gerir_leads`; leitura privada mantém a permissão de leads. Nenhum valor secreto foi incluído nos ZIPs ou neste relatório.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `base-site-core-fator3-1.57.0-instalador.zip` | 2696212 | `5a829a78b3a2265560a88a0dde969fd435fd502ea2072e21ae8f47aeabf13ca6` |
| Fonte | `base-site-core-fator3-1.57.0-fonte.zip` | 4066204 | `205bc18523b271afc76b76dbe5ce1e0fb19231ac5f31f19ae2ac3524ab54c758` |

Somente o instalador é instalável. Raiz do instalador: `base-site-core-fator3/`. Raiz do fonte: `base-site-core-fator3-1.57.0-fonte/`; runtime em `work/plugin/base-site-core-fator3/`, com build, testes, entradas e evidências sanitizadas. Nenhum ZIP da entrega contém outro ZIP.

Relatório externo canônico: `base-site-core-fator3-1.57.0-relatorio.md`. A cópia dentro do fonte é identificada como anterior ao fechamento; tamanho/hash finais do fonte são preenchidos apenas neste relatório externo para evitar circularidade. Não foram emitidos arquivos de impacto nesta rodada.
