# Entrega — Fator3 MCP Google 0.10.0

Revisão: 1 · Data/hora: 2026-10-16T04:37:47-03:00 · Rodada: implementação e validação local
Slug/basename: `wp-mcp-google-fator3` / `wp-mcp-google-fator3.php`
Versão/build: **0.10.0** / identidade reproduzível no `validation.json`, vinculada ao SHA-256 do instalador.
Status: **com-pendencias** — código e gates locais aprovados; homologação remota, visual e dos candidatos acompanhantes permanece aberta.

## 1. De onde esta versão entra

Percurso validado: WordPress limpo ou atualização direta **0.9.0 → 0.10.0**, sem versão intermediária. Base recebida: `wp-mcp-google-fator3-0.9.0.zip`, 546927 bytes, SHA-256 `333e3f177be1095ac9e568e66d4d8cab9b4dfbd4d6a86505e8b7a02583182b32`. Os arquivos da base não foram alterados.

Ambiente executado: WordPress **7.1.2**, PHP **8.3.6**, MySQL **8.0.46**, PHP-FPM com quatro workers e HTTP local. PHPUnit **9.6.17**, WP-CLI **2.12.0** e insumos com hash declarado. O cabeçalho preserva os mínimos históricos WP 6.4/PHP 8.0; esses mínimos **não foram comprovados nesta matriz** e ficam pendentes, sem alegação de suporte validado por inferência.

Foram aplicados os dois normativos Fator3, revisão 3 de 16/10/2026, e a revisão 2 do plano 0.10.0. IDs G91-01–06, M91-01/02 e A01–A21 foram preservados. O incremento é minor; configuração 4.0.0, execução 2.0.0, catálogo 3.0.0, armazenamento/manutenção 2.0.0 e SDKs públicos existentes não foram renumerados.

## 2. Convivência e encaminhamentos

Pacotes reais usados: MCP **0.22.0**, Core **1.33.0**, Meta **0.1.0** e LinkedIn **0.1.0**. Instalação própria continua independente da presença, número e ordem dos acompanhantes. Os cenários de troca reaplicam os mesmos binários MCP/Core; não representam atualização para versões futuras.

| Destinatário | Versão examinada | Classificação | Ticket/recorte | Impacto individual |
|---|---|---|---|---|
| `wp-mcp-fator3` | 0.22.0 | `acao-necessaria` | M91-01/M91-02; MCP-221-03 | [wp-mcp-google-fator3-0.10.0-impacto-wp-mcp-fator3.md](sandbox:/workspace/scratch/ad9b0df8e636/output/0.10.0/wp-mcp-google-fator3-0.10.0-impacto-wp-mcp-fator3.md) |
| `base-site-core-fator3` | 1.33.0 | `informativo` | I01/GSC; Core 212/216/217 | [wp-mcp-google-fator3-0.10.0-impacto-base-site-core-fator3.md](sandbox:/workspace/scratch/ad9b0df8e636/output/0.10.0/wp-mcp-google-fator3-0.10.0-impacto-base-site-core-fator3.md) |
| `wp-mcp-meta-fator3` | 0.1.0 | `informativo` | S01/S04/S06 | [wp-mcp-google-fator3-0.10.0-impacto-wp-mcp-meta-fator3.md](sandbox:/workspace/scratch/ad9b0df8e636/output/0.10.0/wp-mcp-google-fator3-0.10.0-impacto-wp-mcp-meta-fator3.md) |
| `wp-mcp-linkedin-fator3` | 0.1.0 | `informativo` | S01/S04/S06; S05 fora do Google | [wp-mcp-google-fator3-0.10.0-impacto-wp-mcp-linkedin-fator3.md](sandbox:/workspace/scratch/ad9b0df8e636/output/0.10.0/wp-mcp-google-fator3-0.10.0-impacto-wp-mcp-linkedin-fator3.md) |
| `implantador-base` | não disponível | `nao-avaliado` | Pedido MCP Google 24; A20 | [wp-mcp-google-fator3-0.10.0-impacto-implantador-base.md](sandbox:/workspace/scratch/ad9b0df8e636/output/0.10.0/wp-mcp-google-fator3-0.10.0-impacto-implantador-base.md) |

Os impactos estão preparados para encaminhamento, sem envio a outros responsáveis. O runtime dos outros plugins não foi modificado. MCP 0.23.0 e Core 1.34.0 não foram encontrados como instaladores nos insumos consultados; sua homologação conjunta permanece pendente.

## 3. Mudanças e evidência

| Pedido | Problema e mudança entregue | Prova e limite |
|---|---|---|
| G91-01 / A01–A05 | Envelope Google limitado a **1.048.576 bytes JSON**, após os campos da operação. Consultas grandes retornam `f3_google_result_delivery_limit` e instrução para job explícito, sem criar job ou cortar strings. | Fronteira exata do teto, Unicode escapado, ausência de job implícito e execução HTTP real. Dados Google nas provas são sintéticos. |
| G91-01 / A02–A04 | Jobs paginam `rows`, `coverage`, `quality_pages`, `quality_changes`, `page_changes` e `results` de inspeção. Manifesto informa total/retornado/omitido e parâmetros. `next_offset` usa a quantidade entregue. | Recuperação integral, chunks 0.9.0, item/cabeçalho/parâmetros excessivos, seção inaplicável e guardas de ator/grant/retencão. Coleta e exportações internas mantêm seus dados completos. |
| G91-02 / A06 | Canal habilitado, credencial legível, candidata, ativação pendente e falhas de leitura/cifra são estados separados. Cache antigo não é reclassificado; reteste é explícito. | Testes de estado e painel/HTTP; abertura de ajuda e renderização não consultam Google. |
| G91-02 / A06/A21 | Instantes operacionais aparecem no fuso WordPress. UTC técnico e datas do relatório GSC permanecem com sua semântica. Filtro de capacidade passa a ser restrição adicional à administração, inclusive jobs, agendas e retorno OAuth. | Perfil com apenas `read` recusado; teste com fuso America/Sao_Paulo. Ensaio visual/teclado ainda pendente. |
| G91-03 / A08–A11 | SDKs e fronteiras Core/MCP preservados. Não há compensação Google para redaction do MCP. | Core 1.33.0 e SDKs reais no laboratório; MCP 0.22.0 ainda muda tipos na apresentação de erros. Candidatos futuros pendentes. |
| G91-04 / A12/A13 | Pacotes sociais reais ativados; bridge Google recusa alvos `meta/*` e `linkedin/*`. Manutenção, pausa, desativação/reativação e troca Google preservam sentinelas sociais. | Opções, tabelas cifradas e cron comparados. `meta/status` funciona com Google inativo. Não homologa consultas/CSV/JSON sociais remotos nem fluxo comercial S05. |
| G91-05 / A14/A15 | Instalação limpa, atualização da base, rollback válido, recusa de pós-imagem alterada e reaplicação do candidato. | Inventários finais exatos depois de encerrar processos: Google 151 arquivos, MCP 455, Core 356 em ambas as ordens. |
| G91-06 / A18/A19 | Nova `google/documentation`: índice, allowlist, SHA-256 integral, revisão de continuação, paginação UTF-8 e gate estático `manage_options`. Painel e MCP usam a mesma fonte compilada. | **15 documentos**, **53 páginas** na leitura completa HTTP de cada cenário pertinente, inclusive após atualizar. Catálogo regenerado: **282 operações** (109 leituras/173 escritas). |
| Pedido MCP Google 24 / G91-05 / A20 | Fonte, instalador e relatório com identidade final; cinco impactos individuais. | Sequência de fechamento e comparação de runtime descritas nas seções 4 e 8. |

O contrato de entrega é `1.0.0`. `delivery.bytes` mede o objeto job; há reserva de 32768 bytes para campos externos. `collection.complete` continua sendo estado de extração, não de transferência. Se um item não cabe, a resposta identifica seção/offset/motivo, sem continuação que repita indefinidamente o mesmo offset. Em falha de entrega após escrita, `operation_outcome` permanece preservado; não se autoriza repetir a escrita.

No ensaio de payload grande, o maior `structuredContent` observado teve **1006362 bytes** e o corpo HTTP completo **2332841 bytes**, com HTTP 200. São medidas diferentes: o MCP duplica a representação em texto e conteúdo estruturado. O limite MCP 0.22.0 de 2097152 bytes incide no conteúdo estruturado; não se afirma que o corpo HTTP completo caiba em 1 ou 2 MiB.

A fixture de erro do MCP confirma `checks_passed:false`, `all_checks_passed:false`, `passed:0` e objeto público `credential` convertidos em strings redigidas; o segredo aninhado continua oculto. Isso sustenta **M91-01**. A fixture simplificada `success:false/error_code:revision_conflict/data:null` preservou o código; ela **não encerra M91-02**, que exige o produtor Core e sua forma real de erro, inclusive com Core 1.34.0.

## 4. Instalação e prova da troca

| Cenário | Verificações | Resultado | Evidência no fonte |
|---|---:|---|---|
| Instalação limpa, MCP primeiro | 627 | Aprovado; processos encerrados | `evidence/010/native-clean.json` |
| Instalação limpa, Google primeiro, bancada paralela independente | 627 | Aprovado; processos encerrados | `evidence/010/native-repro.json` |
| Upload/primeira ativação por HTTP MCP | 16 | Aprovado; processos encerrados | `evidence/010/native-install.json` |
| 0.9.0 → 0.10.0; acompanhantes reaplicados primeiro | 516 | Aprovado; processos encerrados | `evidence/010/native-upgrade.json` |
| 0.9.0 → 0.10.0; Google atualizado primeiro | 167 | Aprovado; processos encerrados | `evidence/010/native-upgrade-google-first.json` |
| WordPress limpo, somente Google | 9 | Aprovado; processos encerrados | `evidence/010/native-no-companions.json` |

A suíte unitária concluiu **1160 testes / 13993 asserções**, sem falhas. Os cenários nativos somam **1962 verificações executadas**; esse total inclui repetição deliberada em ambientes/ordens independentes, não casos únicos. Gates adicionais: 11 controles do laboratório, 132 verificações de sintaxe/pacote e 17 controles negativos de liberação. Nenhum total de testes de terceiros foi usado como prova própria.

`build/build.py verify` conferiu hashes, árvores, relatórios, JUnit, insumos, processos encerrados e a independência das duas bancadas paralelas. `promote` copiou os bytes validados; não recompilou. A tabela da seção 8 corresponde a esse instalador.

Na bancada descartável, a instalação/atualização usa HTTP autenticado `plugins/upload-base64` com `expected_slug: "wp-mcp-google-fator3"`, SHA-256 do candidato e ativação explícita. Nova requisição comprova versão, armazenamento pronto e documentação atual antes de manutenção. Esse caminho de laboratório não substitui o fluxo de publicação da frota.

Para o site compartilhado: a frota publica **instalador e relatório**, verifica os bytes servidos pela URL raw e usa `plugins/upload` com `expected_slug` e `expected_sha256` da seção 8. **URL raw efetiva: ainda indisponível; não houve publicação nesta rodada.** Não usar o fonte como instalador. O fonte não foi publicado no repositório público, conforme decisão 89 pendente.

Prontidão: consultar `google/status` com `{}`, `google/storage-status` e `google/documentation` com `{}`. `compact:true` pertence somente a `google/integration-status`. Para documento longo, continuar com `next_offset` e `expected_revision`, concatenar `content` sem separadores e conferir SHA-256. O leitor recusa paths/URLs, revisão divergente e perfil sem administração; abrir documentação não cria conexão/job, renova token ou repara cron.

Estado final: seis bancadas locais encerradas; fixtures não entram no instalador. O site compartilhado foi consultado somente em leitura: **saudável**, WP **7.1.3**, PHP **8.3.30**, Google **0.9.0**, MCP **0.22.0**, Core **1.33.0**, Meta/LinkedIn **0.1.0**, observado em **2026-10-16T07:34:27Z**. A candidata 0.10.0 não foi instalada nesse site. A ausência de `google/documentation` ali é esperada na base 0.9.0.

## 5. Banco e volta de versão

Não há mudança de schema SQL. A base atual de registros e cron é mantida. Jobs novos podem externalizar também cobertura e qualidade em registros `result`, além de linhas e mudanças de página. Jobs antigos com esses campos inline continuam legíveis sem regravação durante consulta. Exclusão/retenção permanece no domínio Google.

A atualização preservou ciphertexts, bindings, seleção, conexão adicional, job concluído, agenda pausada e auditoria de teste. Sentinelas sociais de opções/cron e registros cifrados também foram preservadas, inclusive após rollback/reaplicação. Isso não equivale a homologar todos os estados de produção, grants futuros ou configurações de todos os sites.

O rollback de arquivos foi aplicado no laboratório e recusou uma pós-imagem deliberadamente alterada. Depois, o candidato foi reaplicado e o inventário final comparado. **Restaurar arquivos não reverte banco, credenciais, filas nem efeitos Google.** O ensaio de rollback usou estado compatível com a base; não certifica consumo na 0.9.0 de novos metadados externalizados pela 0.10.0. Antes de retornar em operação, preservar backup coerente e consumir/exportar os resultados ou restaurar o conjunto coerente. Nunca forçar retorno sobre arquivos alterados.

## 6. O que permanece pendente

- **A07:** navegador real, telas estreitas e teclado. A instalação do Chromium 151.0.7922.34 falhou com ZIP inválido/truncado (`End of central directory record signature not found`). DOM e admin-post HTTP foram exercitados, mas não substituem prova visual.
- **A08/A09/A10:** candidato MCP 0.23.0, Core 1.34.0, selftest nos quatro estados através das fronteiras finais e conflito real Core. M91-01 foi reproduzido; M91-02 não foi encerrado pela fixture simplificada.
- **A13 parcial:** consultas/exportações sociais reais sob indisponibilidade cruzada e todos os fluxos comerciais não foram homologados. S05 e seletor Lead Sync pertencem a Core/LinkedIn. Não há nova exportação social Sheets.
- **A16/A17:** GA4/GSC com métricas positivas e paginação em contas reais; Sheets em destino autorizado, completude, recibo e replay. APIs Google são fixtures nos testes locais; nenhum gasto Ads ou efeito comercial real foi provocado.
- **A19 no destino compartilhado:** a leitura integral por MCP passou localmente e após upgrade. Falta repetir com os bytes publicados pela frota e a candidata instalada no site compartilhado.
- **A21 parcial:** mínimos históricos WP 6.4/PHP 8.0, multisite, cache distribuído, CDN e cron externo não foram testados. Identidade, título e autorização administrativa foram conferidos.
- Publicação raw, verificação do download público e instalação pela frota não foram executadas. Nenhuma destas pendências é convertida em bloqueio numérico de ativação no plugin.

BigQuery, migração Porter, clientes sociais, mensagens a terceiros e alteração de outros plugins continuam fora desta rodada. A soma de testes aprovados não transforma esses limites em homologação integral.

## 7. Credenciais e configuração do dono

Configurar em **Ferramentas → Fator3 MCP Google**, escolhendo a conexão. Service Account permanece o padrão; importar o JSON como candidata, revisar identidade, conceder acesso aos ativos e ativar explicitamente. OAuth continua em área própria. Nunca colocar segredo em job, mensagem ou relatório.

Habilitar os serviços e bindings necessários, conferir política por ativo e executar o diagnóstico explicitamente. Canal habilitado e credencial legível são estados locais; não comprovam acesso ao recurso. GA4/GSC exigem os escopos e permissões dos ativos; Ads também exige developer token e acesso à conta. Não há alegação de homologação Ads nesta entrega. Schemas, valores padrão e procedimentos completos estão nos 15 documentos instalados e no catálogo da versão.

## 8. Identidade dos arquivos

| Artefato | Nome final e link | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-google-fator3-0.10.0-instalador.zip](sandbox:/workspace/scratch/ad9b0df8e636/output/0.10.0/wp-mcp-google-fator3-0.10.0-instalador.zip) | 703838 | `3e30634b1d1f87b9b4fdeba2a37ac382b1394a1ec7f7235166aa15d107ef8b52` |
| Fonte | [wp-mcp-google-fator3-0.10.0-fonte.zip](sandbox:/workspace/scratch/ad9b0df8e636/output/0.10.0/wp-mcp-google-fator3-0.10.0-fonte.zip) | 2615432 | `c8a31a7ecedab64d222fb28bf2335f686540572384214f01f65fb5c8a80d0450` |

O instalador tem raiz única `wp-mcp-google-fator3/`, **151 arquivos**, sem testes, relatórios, Markdown bruto ou dependências de laboratório. A documentação é PHP protegida e há índice silencioso em cada diretório de runtime. O fonte tem raiz `wp-mcp-google-fator3-0.10.0-fonte/`, árvore completa em `plugin/wp-mcp-google-fator3/`, scripts, documentos editáveis, testes e evidências. Arquivos comuns são idênticos; índices e notices gerados também estão presentes no fonte. Nenhum ZIP contém outro ZIP.

Este é o relatório externo canônico. A cópia dentro do fonte é identificada como **cópia anterior ao fechamento do fonte**: o tamanho/hash desse próprio ZIP só é preenchido aqui depois do empacotamento, sem reabrir o fonte. Os cinco impactos da seção 2 integram a entrega de oito arquivos.
