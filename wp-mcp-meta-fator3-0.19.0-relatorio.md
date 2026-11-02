# Fator3 MCP Meta 0.19.0 — relatório de entrega

Data: 01/11/2026, America/Sao_Paulo. Base direta: 0.18.0. Escopo novo: Pedido MCP Meta 27. Versão corrente entregue: **0.19.0**. Incremento minor para este ciclo, conforme os normativos do projeto; ajustes da candidata foram incorporados antes da primeira entrega. Instalado e ativo no Site-Teste. Aceite real do Pedido27 continua pendente nos dois sites indicados abaixo.

## 1. Bases, instruções e rastreabilidade

Aplicados integralmente `01-instrucoes-agentes-plugins-fator3.md` e `02-padrao-desenvolvimento-plugins-fator3.md`, revisão4, e as decisões do dono: retenção máxima; relatório de impacto apenas para consequências técnicas novas/pedidos a outro mantenedor; teste livre no Site-Teste. Plano anterior à implementação: `planning/RELEASE-0190.md`. Documentos recebidos e identidades dos pacotes: `inputs/0.19.0/`. Histórico de entregas anteriores é mantido em `history/` e não implica reexecução.

Base recuperada e conferida:

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-meta-fator3-0.18.0-instalador.zip | 332343 | `5aef6b8fe85e69478285a84ed5d12c623d7834108928c911ca0e54aaf46d95f8` |
| wp-mcp-meta-fator3-0.18.0-fonte.zip | 3834792 | `3696598305259aac5defa52a3ab6940cdf5b5bba29a003ced15dff775100b75c` |
| wp-mcp-meta-fator3-0.18.0-relatorio.md | 15985 | `4501fff474b25bb247f260ded02d773c95686eb8631dd1d401cc987df3a4939a` |

Entradas deste ciclo:

| Arquivo recebido | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-google-fator3-0.25.1-fonte(2).zip | 7043091 | `9b496df1ceb3786439db79bc1e7dac29ccf78bf31e9d99468011f2cc51502429` |
| wp-mcp-google-fator3-0.25.1-relatorio(2).md | 16499 | `1228296e021f2e77064ecba2538cedb0e2272584233e2648046475133e8c0273` |
| Fator3 MCP Meta(20261101-213443).md | 5333 | `dbc2fcda02360e09acf848dafe0a7bd97f8a8a3985a7d5d94b999f17d72ae89f` |
| base-site-core-fator3-1.66.0-fonte(1).zip | 8187553 | `280a7fa4e706c5f1af3034bd1d11dc8dd466cf33958a4a33ebb4a24ad16b3b0c` |
| base-site-core-fator3-1.66.0-instalador(1).zip | 4218989 | `0f796b2001478fe32e5ce47b5851f79148e6a1eebac7087c39a603a587692830` |
| base-site-core-fator3-1.66.0-relatorio(1).md | 17349 | `c6eaafb4c8e8292189f1122160c50d11bf50bc38f91d47ea955d2b7c39c860ba` |
| wp-mcp-google-fator3-0.25.1-instalador(2).zip | 895748 | `bdd860d479e9813246f8fd2828728ff0cc0c969c2b1e85ddb28a7c9a041d6b30` |

O documento recebido confirma o aceite de frota do Pedido26 na0.18.0: 12 sites e marcação histórica conferida em korvena.com.br, mantendo como corrente o parcial de ctooffice. Essa confirmação é evidência recebida, não nova execução desta manutenção. O Pedido27 identifica HTTP400/código100 sem mensagem/chamada na coleta de datasets; não fornece informação suficiente para determinar a causa histórica.

## 2. Convivência e encaminhamentos

| Pacote | Versões examinadas/testadas | Resultado e fronteira |
|---|---|---|
| Meta | 0.18.0 → 0.19.0 | Reprodução na base, atualização direta, instalação independente e integrada. |
| Core | 1.66.0 | 909 arquivos conferidos com o pacote recebido; SDK e leitor de monitoramento recebem os parciais efetivos. Zero exige cobertura, dois zeros explícitos e otimização conhecida. |
| MCP | 0.38.0 | 467 arquivos fixados; execução decorada mantém diagnóstico sanitizado, autorizações e os47 IDs. |
| Google | 0.25.1 recebido; 0.26.0 observado durante a rodada | 0.25.1 conferido com172 hashes recebidos em laboratório próprio. 0.26.0 copiado do Site-Teste e conferido pelo digest observado. Ambas as matrizes integradas passaram. |
| LinkedIn | 0.14.0 | 73 arquivos intactos; capabilities executada pelo MCP. Não exige mudança decorrente desta entrega. |
| Pipedrive | 0.5.0 | 31 arquivos intactos; status local preserva registro/negação sem concessão nem envio. |

Google0.26.0 apareceu no Site-Teste enquanto os testes eram preparados; não foi substituído no site compartilhado. Seu guia instalado (`inputs/0.19.0/google0260-guide-live.json`) informa ajuste do contrato de conversões ao Core1.66.0, sem mudança de identidade do schema. O teste de0.25.1 ocorreu somente na cópia isolada. Não se atribui a atualização Google a este trabalho.

Core1.66.0 já incorpora o tratamento de medição/projeção pedido pelo Google0.25.1. Os documentos recebidos não exigem nova alteração no Meta por esse tema. Contratos Meta `meta-ads-reader/1.0.0`, `meta-ads-monitoring/1.0.0` e Messaging permanecem. Nenhum pacote de terceiro foi editado.

Não foi identificado encaminhamento técnico novo a outro mantenedor. Por isso não acompanha relatório de impacto: confirmação de compatibilidade e situação da entrega pertencem a este relatório, conforme a instrução do dono. Não há alteração solicitada ao LinkedIn.

## 3. Mudanças e provas

### 3.1 Pedido27: chamada identificada, texto sanitizado

`ProviderDiagnostic.php` projeta provider_message, provider_error_user_msg, provider_message_redacted, provider_type e fbtrace_id. `provider_call` é modelo fixo de rota sem IDs, URL ou token; `request_stage` distingue conta, vínculo, stats_browser, stats_server, optimization, emq e validação da conexão. A versão da API é preservada quando válida. Campos inexistentes não são inventados.

`Http.php` agrega a chamada aos Faults. `CollectionState.php` propaga a projeção ao job-status, last_error da agenda, auditoria e health. `last_errors` da agenda e `errors` da auditoria acrescentam até oito diagnósticos distintos de dataset_quality; são amostras, sem substituição do acervo/páginas dos jobs. `health.datasets.diagnostics` inclui falhas de jobs autorizados mesmo sem linhas. `Query.php` conserva a amostra ao salvar a agenda. O diagnóstico aditivo também acompanha os demais relatórios HTTP, sem mudança de IDs ou gates.

A mensagem é decodificada antes da remoção de segredos; só permanece vocabulário técnico permitido. URLs, e-mails, IPs, identificadores/números e palavras desconhecidas são redigidos. Limite de512 bytes; flag indica alteração. Tipo e rastreio têm validação própria. Não se persiste corpo bruto, headers ou credenciais. Vocabulário desconhecido pode ser removido, inclusive termos úteis: código, chamada e rastreio complementam a investigação. Testes cobrem sete valores privados sintéticos e segredo codificado em entidade HTML.

Código100 continua causa indeterminada. Para10/200 ou HTTP403, a ação orienta conferir o acesso “Usar conjunto de dados de eventos”, atribuição ao negócio/conta e os escopos pertinentes com a mesma credencial. Não concede acesso, muda a seleção ou afirma uma permissão ausente sem evidência. Outro token do conector oficial não valida o token salvo no plugin.

### 3.2 Consulta de dataset e dados independentes

A confirmação de vínculo passa de `dataset/adaccounts` para `act_conta/adspixels`, coerente com a descoberta que funciona no pedido. Confirmação continua obrigatória; ausência/recusa não autoriza ler o ativo. A base foi reproduzida com HTTP400 nessa etapa: parava antes de stats/EMQ, pausava o job sem linhas e perdia mensagem/chamada. Esse caminho reproduzível não prova que foi a causa específica nos sites reais.

Stats usa `aggregation=event` com WEB_ONLY e SERVER_ONLY em consultas separadas. Soma somente buckets horários distintos dentro do dia/fuso solicitado, sem tratar os dois canais como eventos únicos. Cobertura exige todas as horas e o evento explicitamente presente em cada hora; lacuna permanece desconhecida. Duplicatas, dados fora da janela, valores negativos e overflow não confirmam cobertura/zero. Dias de23/25 horas são testados. Dados devolvidos fora do horizonte conservador de sete dias permanecem armazenados sem declaração de cobertura completa. Paginação mantém cursor seguro, 10 páginas/3000 registros por aresta; vínculo/conjuntos permanecem limitados a cinco páginas.

EMQ pede `web{event_name,event_match_quality}`; projeta composite_score e feedback conhecido. Vazio, null, nota inválida ou entrada defeituosa ficam diagnosticados. Uma entrada inválida não descarta as demais. EMQ continua fotografia atual separada, com observed_at; backfill de contagens não inventa notas históricas.

Falhas de stats de uma fonte, conjuntos ativos ou EMQ não descartam os demais resultados úteis. Inclui falha de transporte, resposta inválida, quota e orçamento. Resultado útil com lacunas é parcial; não se promete retry automático da subchamada faltante. Nova execução/backfill explícito pode revisitar após resolver a causa; próximas agendas continuam seguindo o cron. Revogação/conflito local, revisão concorrente e falha de persistência continuam impedindo operações. Zero requer ambos valores explícitos, ambas coberturas por evento, dia completo mais recente e conjunto ativo conhecido.

O leitor real do Core recebeu resultados criados pela coleta: contagens quando EMQ falha e EMQ quando contagens falham. Não houve HTTP extra nem correio na leitura. Retenção cifrada sem prazo, revisões, grants e seleção explícita permanecem.

### 3.3 Referências e limites da investigação

Consultados SDK oficial Python (`https://github.com/facebook/facebook-python-business-sdk/blob/main/facebook_business/adobjects/adspixel.py`) e metadados do conector Meta oficial, cujo contrato de stats restringe event_source à agregação event. O SDK lista parâmetros/endpoint; isso não comprova aceitação de cada combinação pelo token de produção. As páginas oficiais de stats e Dataset Quality listadas em MONITORING.md retornaram HTTP429 durante esta rodada. Não foram usadas como evidência de resposta válida nesta data. Nenhuma chamada ao fornecedor Meta real foi executada.

Não existe resposta histórica completa dos dois sites para atribuir a origem do HTTP400 com certeza. Consulta corrigida e tratamento parcial estão testados com fixtures; o aceite externo abaixo continua necessário. Ausência de buckets/eventos poderá manter cobertura parcial, deliberadamente sem inferir zero.

### 3.4 Matriz executada

WordPress real, banco MySQL8.4.11, tabelas/pasta/salts próprios por laboratório. Processos CLI bloqueiam saída de rede; HTTP Meta é interceptado por fixtures. Correio é interceptado antes do envio. O teste de orçamento conta uma tentativa de e-mail sintética, sem envio. Não houve gasto Ads, publicação, contato, notificação real ou alteração de produção.

Matriz final: **629 verificações, 0 falhas**, sem contar repetições intermediárias ou as quatro verificações de reprodução na base.

| Evidência em evidence/ | Verificações | Falhas |
|---|---:|---:|
| `upgrade-final.json` | 14 | 0 |
| `current-smoke-final.json` | 36 | 0 |
| `current-dataset-final.json` | 77 | 0 |
| `live-final-dataset0190.json` | 85 | 0 |
| `live-final-integration0190.json` | 27 | 0 |
| `live-final-diagnostics0190.json` | 60 | 0 |
| `live-final-coreads0190.json` | 46 | 0 |
| `live-final-coremonitor0190.json` | 19 | 0 |
| `received-clean-dataset-final.json` | 85 | 0 |
| `received-clean-integration-final.json` | 27 | 0 |
| `minimum-dataset-final.json` | 77 | 0 |
| `minimum-smoke-final.json` | 36 | 0 |
| `budget-final.json` | 29 | 0 |
| `review-final.json` | 11 | 0 |

Instalação independente/final, atualização e convivência: WordPress7.1.4/PHP8.3.36 observados. Piso: WordPress6.4 e PHP8.1.2-1ubuntu2.28, 64 bits, pacotes oficiais com hashes fixados; instalação limpa no runtime exato e revalidação da candidata final. As adaptações das fixtures Core trocam a direção do vínculo e fornecem24 buckets event, preservando asserções do consumidor. Lint:34 PHP. ZIP determinístico recompilado com mesmo SHA. Fonte runtime e instalador são idênticos.

Duas tentativas intermediárias da fixture integrada ficaram registradas: `received-dataset.json` consultava a primeira agenda, corrigido para identificar a própria; `received-final-dataset.json` examinou apenas os100 primeiros registros de auditoria após várias suítes. Store::list ordena por chave, portanto essa amostra não garante conter o job novo. A matriz Google0.25.1 foi refeita em laboratório próprio, conforme o isolamento da suíte, e passou85+27. Não houve falha de runtime demonstrada nessas duas ocorrências. tests/README-0190.md declara a precondição de laboratório próprio. Elas não são ocultadas nem incluídas no total final.

Além da matriz:28 documentos instalados lidos integralmente pelo MCP em31 páginas com expected_revision, bytes e SHA conferidos contra o ZIP; catálogo final com47 operações0.19.0 e sem operações de laboratório. `changes.diff`, `changed-files.json` e `final-test-matrix.json` permitem revisão.

## 4. Instalação efetiva e prontidão

Destino autorizado: https://fator3-teste-mcp-1.dreamhosters.com/ . Instalador final enviado por plugins/upload-base64 com SHA/slug/idempotência; atualização0.18.0→0.19.0, ativo antes/depois. Operação `ffe251601de27360f1300ec6d26fcd3b`; backup de pré-imagem `5a9db353cde0dcd70c2b0911`. Sondas internas `/` e `/wp-json/` passaram comHTTP200 e cache bypass antes/depois. Ativação silenciosa em processo novo; o recibo não comprova prontidão comercial nem ciclo de activation hook. Instalação limpa foi validada separadamente.

Após instalação: health0.19.0 ok, storage/crypto prontos, audit_health ok, sem issues, conexão_count0 e active_schedules0. Logo não há credencial real ou coleta comercial a homologar nesse site. Não foi criada conexão no site compartilhado.

Integridade medida antes/depois:

- Dois registros de negócio idênticos, inclusive ciphertext/revisões; histórico vazio permaneceu vazio.
- Sete opções Meta idênticas e configuração de monitoramento do Core com mesmo digest.
- Core/MCP/Google/LinkedIn/Pipedrive com mesmas versões, estado ativo, contagem e hashes de arquivos.
- Meta final com66 arquivos, tree SHA `bb717b14c78c202b4c648c5fed5a7c5f23bcd256410a06c2192a6741f04c77dd`, igual ao instalador.
- Comparação de upgrade isolado preservou13 registros e quatro linhas históricas byte a byte, grants prontos e retenção; a coleta antiga complete/null já aparece superseded sem recolher.

Evidências: shared-before, shared-preinstall, shared-install, shared-post-0, shared-comparison, final-health, final-discovery e mcp-documents-verified. Auditoria técnica das próprias operações MCP não entra no digest de registros de negócio. A verificação não é garantia universal de ausência de regressões fora dos cenários exercitados.

Laboratórios foram encerrados com zero tabelas remanescentes, pasta e manifesto removidos. Controller, bundle e ZIP auxiliar Google foram removidos com guarda de hash e backup; nenhum componente QA compõe o instalador. Backups técnicos do MCP permanecem disponíveis para reversão.

## 5. Banco, retenção e reversão

Sem nova tabela/coluna, DDL, nova option de negócio ou regravação em massa. Diagnósticos aditivos entram nos registros cifrados existentes em novas execuções. Mensagens antigas ausentes não podem ser reconstruídas. O último erro histórico permanece com a classificação do Pedido26. Não há diminuição de retenção, limpeza automática, mudança de salts/credenciais, grants, agendas ou ativação de notificações.

Para atualização: fazer backup de arquivos, banco e salts; instalar o ZIP sobre o mesmo slug `wp-mcp-meta-fator3`, basename `wp-mcp-meta-fator3/wp-mcp-meta-fator3.php`, sem desinstalar. Conferir versão47 IDs/health/documentação e, com credencial válida, nova coleta e leitura do Core. Requisitos permanecem WordPress6.4/PHP8.1.2 de64 bits, criptografia e travas nomeadas no banco.

Rollback: restaurar pré-imagem ou instalador0.18.0 preservando banco e salts. Isso restaura consultas/diagnóstico anteriores; não desfaz o histórico já persistido nem efeitos externos. Não usar desinstalação para reverter. Se restauração integral de dados for necessária, deve usar backup consistente com as mesmas chaves. Nenhuma alteração irreversível no esquema foi introduzida; o recibo genérico do MCP não promete reversão de banco.

## 6. Pendências e aceite externo

| Item | Situação nesta entrega | Verificação restante |
|---|---|---|
| Pedido27 | Implementado e validado localmente/integrado; aceite real pendente | Em korvena.com.br e ctooffice, atualizar, conferir a agenda dataset-qualidade-diario concluída/parcial e linhas em f3base/meta-monitoramento-ler, ou recusa de permissão legível com ação. Usar o token salvo nesses sites, não substituí-lo pelo conector oficial como prova. |
| Pedido26 | Aceite de frota informado no documento recebido; regressão passou | Sem reabertura por este ciclo. |
| Pendência20 da frota | Mantida | Monitoramento com alteração real, contagens/EMQ/próximo incidente;30 dias Ads comparados ao Gerenciador nas duas contas; Pedido22 com credencial real fora do padrão. |
| Pendência88 | Mantida | Twinia sem conexão, conforme documento recebido. |

A causa histórica do código100 continua não determinada. Os novos campos tornam a próxima recusa investigável; não se declara solução comprovada em produção nem se remove o Pedido27 do documento da frota nesta entrega.

## 7. Credenciais e ações do operador

Nenhum segredo real coletado, lido do navegador ou incluído na entrega. Fixtures usam valores declaradamente sintéticos e ficam somente na fonte. A instalação compartilhada não contém conexão Meta. Laboratórios não enviam mensagens nem chamam fornecedores reais.

Novos erros podem ser consultados por meta/job-status, meta/list-schedules, meta/audit e meta/health. Releia revisão/estado antes de repetir mutação incerta; health e documentação são somente leitura. Para jobs já pausados, revisar a causa e criar nova coleta/backfill conforme necessidade; a atualização não reautoriza nem retoma planos automaticamente.

## 8. Artefatos e integridade

| Artefato | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-meta-fator3-0.19.0-instalador.zip | 342993 | `f7629f48fffb774542a480fb55f29a151762b06a27b34c9a0c3188da3599451b` |
| wp-mcp-meta-fator3-0.19.0-fonte.zip | 4132426 | `21d13446e4b18cec279bfaf8c0bde0d3f93008e9832fe0b7f560ee1095c95ead` |

O instalador contém somente runtime/documentação; a fonte inclui build, runtime idêntico, testes, plano, entradas textuais, evidências, histórico e este relatório. Não contém ZIP aninhado. O relatório interno é a cópia de pré-fechamento: os campos SOURCE_BYTES/SOURCE_SHA256 são preenchidos somente no relatório externo após fechar uma única vez a fonte, evitando autorreferência. Identidade do próprio relatório é calculada após esse preenchimento e registrada no recibo externo de entrega.
