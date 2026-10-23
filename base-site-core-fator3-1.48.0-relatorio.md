# Entrega — Fator3 Site Core 1.48.0

Revisão: 1 · Data: 2026-10-22T22:55:37-03:00 · Rodada: implementação e homologação.
Slug: `base-site-core-fator3` · Versão: `1.48.0` · Contrato administrativo: `8.13.0`.
Status: `com-pendencias` de aceite em produção e de matriz mínima; implementação apta no escopo testado abaixo. O Site-Teste está atualizado e operacional. A frota não foi atualizada nesta rodada.

## 1. De onde esta versão entra

Instalação limpa e atualização direta de **1.47.0** validadas com o instalador final, pelo fluxo nativo do WordPress. Não há versão intermediária a instalar. Base recuperada da entrega anterior, confrontada com os pedidos atuais do documento “Fator3 Site Core”, anexo de 22/10/2026. Pedidos abertos desta rodada: **288, 289 e 290**; funcionalidades históricas, incluindo 263 e 283, permanecem na base, sem reabertura de escopo.

Instalador-base: `base-site-core-fator3-1.47.0-instalador.zip`, 2.195.818 bytes, SHA-256 `dd16cb720e57c2d448e78a744eb0fd761d6aff04aadeeed8309b6b5003b417c1`. Fonte-base: 4.264.186 bytes, SHA-256 `7082123036ee6470c18407f5da29a9969b96617ebf4b7dbcb106ac9041c18c8c`.

Ambiente local comprovado: **WordPress 7.1.3, PHP 8.3.6 de 64 bits e MySQL 8.0.36**, instalação única. O mínimo WordPress 7.1.2 herdado do cabeçalho não foi reexecutado nesta rodada; não se certifica aqui essa combinação. PHP 8.3.6 foi efetivamente usado. Não houve teste multisite.

## 2. Convivência e encaminhamentos

As quatro versões atuais foram examinadas e ativadas em conjunto no laboratório e permaneceram ativas no Site-Teste. Seus fontes não foram alterados e não entram no instalador do Core.

| Plugin | Versão | Bytes do instalador examinado | SHA-256 |
|---|---|---:|---|
| `wp-mcp-fator3` | 0.28.0 | 853885 | `d1d297d8aaee0e5188b92fe9eae20a9dcc07e79d639baae25f267bf64f7243b0` |
| `wp-mcp-google-fator3` | 0.17.0 | 767299 | `42bd11080b518c82e0960753fa7b08d7adae28743cfcd3e96f9b83bf3f4709b0` |
| `wp-mcp-linkedin-fator3` | 0.7.0 | 207524 | `85b1cc8d16ab972e9acc2ad90bf81f0806b30a66e0833be311e33bf4a6b1d515` |
| `wp-mcp-meta-fator3` | 0.6.0 | 134999 | `36f5cfe9a20db272fc80d3cdd8fd46da823c4eeac856e31d911e41754fd19f69` |

| Destinatário | Pedido | Efeito relevante e resultado | Impacto |
|---|---|---|---|
| MCP LinkedIn 0.7.0 | 289 | O consumidor passa a fornecer exclusivamente a regra de servidor. O adaptador existente já oferece o contrato necessário; validação local com adaptador real, HTTP interceptado e auditoria MCP 0.28.0 passou. Nenhuma alteração no fornecedor é exigida. | `base-site-core-fator3-1.48.0-impacto-wp-mcp-linkedin-fator3.md`, revisão 2, entrega |

O impacto LinkedIn foi aberto durante o planejamento e atualizado com a implementação e as evidências. Não houve envio de mensagem ao mantenedor nesta rodada; o arquivo é entregue ao dono para encaminhamento. Não foi preciso aguardar outra implementação.

O SDK `site-measurement-context/1.0.0` conserva a forma de snapshot, capabilities e eventos utilizada pelo Google 0.17.0. A ampliação administrativa está declarada separadamente em `extensoes.linkedin_conversoes`, contrato `site-linkedin-destinations/1.0.0`. O schema real do Google validou o snapshot. Não há impacto que exija ação nos outros três pacotes dentro das interfaces examinadas; não foram criados relatórios individuais de ausência de ação. As novas rotas seguem o catálogo de abilities existente do MCP. Nenhuma nova ordem de troca dos acompanhantes é necessária no conjunto testado.

## 3. Mudanças e evidência

| Pedido | Problema | Mudança | Resultado e evidência |
|---|---|---|---|
| 288 — Gestão das mensagens do Slack | Sem listagem; limpeza bloqueada após eliminar o contato; falta de remoção conjunta e de classificação posterior como teste. | Listagem local paginada, remoção com simulação/revisão/autoria, classificação como teste e integração à eliminação do contato. | `implementado`, `validado-localmente`, `validado-wordpress`; exclusão real no fornecedor de 13 avisos e 78 respostas do Site-Teste, com ausência confirmada. Cinco avisos do CTO Office ainda pendentes. |
| 289 — Regra LinkedIn própria do servidor | ID do Insight Tag reutilizado no servidor, incompatível com regra CONVERSIONS_API. | Nova opção de servidor, IDs distintos na prévia, mesmo event_id, bloqueio explícito quando a regra falta e ajuda na tela. | `implementado`, `validado-localmente`, `validado-wordpress`; adaptador real 0.7.0 com HTTP simulado. Conversão comercial e contagem no LinkedIn pendentes. |
| 290 — Disputa de reserva neutra | Concorrência de uma ocorrência registrada como falha de checkpoint/exceção. | Prova da passagem dona; resultado neutro e contagem separada; falha real sem dona mantém diagnóstico e contador. | `implementado`, `validado-localmente`, `validado-wordpress`; concorrência e falha SQL exercitadas. Observação de sete dias em produção pendente. |

### 288 — Slack

- `f3base/avisos-slack-listar` lê somente o registro local: id, referência ao contato, tipo, teste, estado, canal, ts, datas, presença conhecida e quantidade de respostas próprias. Filtros por contato, período Unix inclusivo, teste, estado e tipo; paginação por cursor. Não devolve o conteúdo da mensagem nem consulta o Slack.
- `f3base/avisos-slack-apagar` aceita id, ids ou filtro, com `simular: true` por padrão, revisão, `chave_operacao`, motivo e limite de seleção entre 1 e 50. A simulação inclui as respostas próprias conhecidas. Aviso não marcado como teste exige `confirmar_nao_teste: true`. Seleção que ultrapassa o limite pede um recorte menor.
- A execução confere site, workspace, destino e autoria remota do bot; apaga respostas próprias antes da principal e preserva mensagens humanas ou de outro aplicativo. Resultado por mensagem: `apagada`, `ausente_antes`, `nao_propria` ou `falhou`, com o código correspondente. Após apagar, verifica a ausência. A idempotência evita repetir uma operação já registrada. Limite de chamadas do Slack retorna diagnóstico e prazo para nova tentativa.
- `f3base/avisos-slack-testes-apagar` usa o mesmo caminho, aceita filtros e continua funcionando quando o contato já foi eliminado. A prova na tabela de manutenção basta, sem reconstruir o contato.
- `f3base/leads-marcar-teste` permite classificação posterior, com simulação, revisão e motivo; atualiza o contato e seus avisos de forma atômica, sem reenviar nada.
- `f3base/leads-eliminar-registro` aceita `apagar_slack`: padrão true para teste e false nos demais. A simulação mostra o que sairia; a execução tenta apagar antes da remoção local e devolve `copias_externas.slack`. Uma falha externa não bloqueia a eliminação local. Para contato já eliminado, use as rotas dedicadas de avisos.
- A remoção elimina payloads da manutenção e das partes e preserva a prova técnica necessária. A nova coluna `aviso_tipo` usa o contato sobrevivente para classificar registros anteriores; quando não há evidência, fica `desconhecido`.

### 289 — LinkedIn

`f3base_linkedin_server_conversion_id` é uma opção pública de identificador, com schema, sanitizador, procedência e verificação. `f3base_linkedin_conversion_id` continua sendo a regra do Insight Tag. A tela de Medição identifica as duas fontes e explica o caminho no Campaign Manager. Nenhum token novo é armazenado no Core.

A fotografia do contato registra os dois IDs. O adaptador `site-core-conversions` recebe apenas o ID de servidor; o `lintrk` mantém o ID do navegador, com o mesmo `event_id`. A prévia administrativa identifica cada destino. Regra vazia bloqueia o servidor com `regra_ausente`, e a leitura de medição apresenta `linkedin_server_regra_ausente`. Não há fallback ao ID do navegador, nem preenchimento ou reenvio automático de registros anteriores sem a regra de servidor. Divergência entre a regra configurada e a concessão do fornecedor impede a entrega.

O verificador comprova a vinculação local à concessão; não afirma recebimento comercial. A extensão administrativa contém IDs e procedência sem alterar o SDK utilizado pelo Google. Conversão de material continua somente no navegador: o item condicional de material no servidor é `nao-aplicavel` nesta arquitetura.

### 290 — Agendador

A disputa só é neutra quando há prova de uma passagem dona da mesma tarefa, hook, argumentos e ocorrência, com reserva válida ou execução concluída sem falha. A prova vem do diário ou da trava de arquivo; a metadata de arquivo tem guarda PHP. O resultado `reserva_ocupada` inclui `dados.dona`, run_id e origem, não executa o callback e grava sucesso SQL nulo, sem incrementar falhas consecutivas nem alterar a intenção da dona.

Sem outra passagem dona, uma gravação que não confirma continua `checkpoint_nao_persistido`, com código interno, erro do banco quando disponível, registro de falha e recuperação. A disputa não vira `tarefa_lancou_excecao`. Falha real de tarefa filha não é encoberta por uma passagem pai neutra. Disputas aparecem separadas, por dia UTC e origem, nas leituras de execução e saúde, na janela de 30 dias. O histórico não é reclassificado retroativamente.

Contrato administrativo 8.13.0: **141 abilities**, três novas; **75 opções operáveis**, **138 opções inventariadas**, **57 tabelas** e **10 famílias de transientes**. Perfil `piso-padrao-3.6`, 92 condições, preservado. O runtime tem 446 arquivos, com **35 adicionados ou alterados e nenhum removido** frente à base. A lista por arquivo e SHA-256 está em `evidence/changed-files-1480.json`. Não houve mudança em JavaScript nesta versão.

## 4. Instalação e prova da troca

No laboratório, o instalador final foi usado em WordPress limpo e no upgrade direto de 1.47.0 por `Plugin_Upgrader`, com novas requisições e repetição idempotente. Ambos concluíram as 18 etapas. Preservaram-se opções explicitamente false/vazias, procedência, dados de contato, segredos sintéticos, callback e cursor.

No **https://fator3-teste-mcp-1.dreamhosters.com**, a operação de troca foi `77a68c664fc5e94b0c01345c`, operação de pacote `677f05680d69cd99a5804db7e42e7d8b`, backup privado `00197fef41f91003213a2ee7`. O instalador corresponde ao SHA-256 da seção 8. O Core foi drenado para a troca e retomado. O ciclo `9fa9d1a3-0a57-481d-81a6-ab407dfdada8` concluiu 18 etapas, zero falhas e finalização confirmada. Home e REST responderam HTTP 200 em probes com PHP fresco; isso complementa, sem substituir, os testes funcionais.

A leitura administrativa de saúde confirmou a versão e o ciclo concluído. O índice e `f3base/documentacao-ler` permitem consultar `arquivo`, `linha` e `limite`, seguindo `proxima_linha` até null. Documentos instalados lidos integralmente por paginação autenticada:

| Documento | Páginas | SHA-256 igual ao runtime local |
|---|---:|---|
| `docs/RELEASE-1.48.0.md` | 2 | `7e2f17254178ffe8b53b2267cbe467ef00916e58db4f956a5e06e54b47db17b8` |
| `docs/AGENTES-1.48.0.md` | 1 | `d1fae44e8e522cd906387fa634f444bf4b655fae5b35631ebd2b3e5bbb731544` |

| Prova | Ambiente e resultado | Evidência no fonte | Limite |
|---|---|---|---|
| Lint do instalador | 230 PHP aprovados | `evidence/installer.json` | PHP 8.3.6 |
| LinkedIn consumidor | 48 verificações aprovadas | `linkedin-1480.json` | HTTP externo simulado |
| LinkedIn fornecedor | 10 verificações aprovadas com adaptador 0.7.0: IDs distintos, HTTP 201 simulado, deduplicação, auditoria de serviço MCP 0.28.0 | `provider-linkedin-1480.json` | Não é recibo comercial LinkedIn |
| Slack local | 20 verificações aprovadas: filtros/cursor, simulação, guardas, reclassificação, eliminação, autoria humana/estrangeira, idempotência | `slack-1480.json` | Transporte simulado |
| Agendador local | Cinco verificações aprovadas: cli/http_cron, http_cron/http_cron, repetição após conclusão e falha sem callback | `scheduler-1480.json` | Processos PHP reais; origens controladas pelo fixture |
| Convivência | 11 verificações aprovadas com os quatro acompanhantes atuais | `coexistence-1480.json` | Não é homologação completa de cada fornecedor |
| Documentação e permissões | 79 verificações aprovadas, paginação e hashes | `docs-1480.json` | Leitura administrativa |
| Regressões de formulários e Pipedrive | 32 e 39 verificações aprovadas contra 1.48.0 | `forms-1470.json`, `pipedrive-1470.json` | Nomes herdados; transporte externo simulado |
| Instalação e upgrade | Dois ciclos nativos concluídos e repetição idempotente | `native-cycles-1480.json` | WordPress 7.1.3 |
| Site-Teste Slack/LinkedIn | 19 verificações Slack e cinco LinkedIn; configurar ID com simulação, escrita, releitura e restauração | `site-teste-1480.json` | Fixtures e contatos sintéticos, sem evento comercial |
| Site-Teste concorrência | Dois workers simultâneos: uma execução, outra neutra com dona; casos cli/http_cron e http_cron/http_cron | `site-teste-1480.json` | Workers HTTP locais reais; rótulos de origem simulados, sem afirmar disparo por crontab real |
| Site-Teste checkpoint | SQL realmente recusado no fixture; erro do banco, contador 1, callback não executado | `site-teste-1480.json` | Entrega externa de alerta não testada |
| Site-Teste Slack real | **13 principais + 78 respostas = 91 mensagens apagadas e ausentes** | `site-teste-1480.json` | Recorte de teste indicado no pedido 288 |

As evidências da tabela ficam em `evidence/`. `scheduler-setup-1480.json` registra preparação de schemas ainda com metadata da base 1.47.0; não deve ser usado como certificação adicional do instalador final. Os relatórios anteriores incluídos em `history/` são históricos.

Na limpeza real do Slack, os contatos correspondentes já estavam eliminados. As rotas funcionaram com a prova remanescente. Após atingir o limite do Slack, a execução foi retomada respeitando a espera indicada, com novas simulações e chaves. Todas as 91 mensagens terminaram com estado apagada e presença ausente confirmada. Não foram criadas mensagens de teste no canal para esta validação; a preservação de resposta humana foi exercitada com transporte simulado.

**Estado final:** Core 1.48.0 e os quatro acompanhantes ativos; operação retomada; opções temporárias restauradas, inclusive ID LinkedIn de servidor vazio; nenhum contato QA nem ticket/resultado temporário restante. MU fixture e ZIP remoto removidos. O backup privado de atualização e registros técnicos de execução foram preservados. A intenção de falha sintética foi encerrada após a prova. O helper de homologação está somente no fonte, fora do instalador.

Para a frota, publicar este instalador e o relatório canônico no fluxo autorizado e conferir os bytes servidos antes de instalar. Caminho previsto, **ainda não publicado nesta rodada**: `https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/base-site-core-fator3-1.48.0-instalador.zip`. Usar `expected_slug: base-site-core-fator3` e o SHA-256 da seção 8, consultando o schema vigente de upload. Confirmar versão ativa, conclusão das etapas, saúde e documentação na leitura instalada. Não foi feito push nem instalação em outros sites.

## 5. Banco e volta de versão

A evolução é aditiva: coluna `aviso_tipo` na manutenção Slack; nova opção pública LinkedIn; provas de concorrência no diário e metadata da trava. As mesmas 57 tabelas permanecem inventariadas. As etapas de atualização são repetíveis e a troca não redefine opções do dono nem reenvia conversões anteriores. O teste de upgrade comparou dados e segredos sintéticos antes/depois.

Voltar somente os arquivos não desfaz gravações, classificações como teste, configuração de servidor nem exclusões de mensagens. Mensagens já apagadas do Slack não são recuperadas por rollback. Para restauração integral, usar backup coerente de arquivos e banco, preservando eventos posteriores que precisem ser conciliados. A versão anterior não oferece a separação segura de IDs nem as novas rotas; não usar downgrade como forma de reprocessar conversões. O backup privado informado acima permanece disponível no Site-Teste.

## 6. O que permanece pendente

1. **CTO Office — pedido 288:** implantar a release naquele site e limpar os cinco avisos antigos citados. A rota geral exige confirmação explícita para aviso não marcado como teste, ou classificação prévia do contato. Nenhuma ação foi feita nesse site nesta rodada.
2. **CTO Office — pedido 289:** autorização `rw_conversions`, regra ativa de fonte `CONVERSIONS_API` na conta 558431216 e concessão ao consumidor `site-core-conversions`; depois, contato real recebido e contado uma única vez. Prévia, testes com HTTP simulado e auditoria local não comprovam esse aceite comercial.
3. **Pedido 290:** observar sete dias após a troca na frota/CTO Office, procurando checkpoint/exceção com outra dona da mesma ocorrência. Não se declara esse período cumprido. A rota de alerta de falha foi preservada; entrega a Slack/e-mail não foi provocada neste ensaio de falha.
4. **Matriz de suporte:** WordPress 7.1.2 declarado no cabeçalho não foi reexecutado nesta rodada; ambiente comprovado foi 7.1.3. Não houve nova rodada de navegador/JavaScript, pois os bundles não mudaram.

O pacote pode ser usado no conjunto comprovado e para a implantação necessária aos aceites restantes. Não se marca aceite completo de produção nem se altera o quadro externo de pedidos nesta entrega.

## 7. Credenciais e configuração do dono

Na tela **Medição**, manter o campo Insight Tag com a regra do navegador e preencher o novo campo de **Conversions API** com a regra própria do servidor. Quando o transporte LinkedIn usa servidor, a configuração deve corresponder à concessão existente no MCP LinkedIn. A permissão `rw_conversions`, os ativos e a regra API são administrados pelo fornecedor; nenhum segredo consta nesta entrega. No Site-Teste, todos os IDs sintéticos foram retirados ou limitados ao fixture, e o novo campo foi devolvido ao vazio original.

As novas rotas Slack reutilizam o bot e o destino já configurados, com as permissões de leitura/remoção das mensagens próprias. A comprovação remota de autoria é obrigatória; mensagens de outro aplicativo ou pessoa não passam por esse caminho. Não é necessário copiar tokens para o relatório ou para novas opções do Core.

## 8. Identidade dos arquivos

| Artefato | Nome final e link relativo | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [base-site-core-fator3-1.48.0-instalador.zip](base-site-core-fator3-1.48.0-instalador.zip) | 2217146 | `91097a3819cce15fcc66adfa5d8503537cacdb51cfd3ad04ba73e5f7c27a18de` |
| Fonte | [base-site-core-fator3-1.48.0-fonte.zip](base-site-core-fator3-1.48.0-fonte.zip) | 4388255 | `29ef4cdb623f22a63ae833eaa81eda6753144bf227ca9b7fc6a4abf61811cd0b` |

Relatório externo canônico: `base-site-core-fator3-1.48.0-relatorio.md`. A cópia dentro do fonte é **anterior ao fechamento do fonte**; os campos de tamanho/hash do próprio fonte são preenchidos somente neste relatório externo após empacotamento. O conteúdo funcional e as evidências são os mesmos. O runtime do fonte foi comparado byte a byte com o instalador final homologado. Nenhum ZIP contém outro ZIP.

Complemento pertinente: `base-site-core-fator3-1.48.0-impacto-wp-mcp-linkedin-fator3.md`. Plano de escopo: `base-site-core-fator3-1.48.0-plano.md`, incluído no fonte. O fonte também contém ferramentas de build, testes, evidências saneadas, acompanhantes intactos usados em laboratório e histórico da base; não contém banco, runtime baixado, logs de sessão nem credenciais reais.
