# Entrega — Fator3 MCP Meta 0.28.0

17/11/2026 · Revisão 1 · **Apta no escopo testado**. Pedidos core **423(e)**, impacto do Core 1.91.0 em Meta, revisão 1. Esta é a release do destinatário.

## 1. Entrada

Instalação limpa e atualização direta da versão vigente **0.27.0**, sem intermediária. Slug e basename preservados: `wp-mcp-meta-fator3/wp-mcp-meta-fator3.php`. SHA-256 do instalador-base: `77e2364a471c41399b6fa5d11feecebabcc1d2722bd5bca89eacbee803733ca6`. Requisitos: WordPress ≥ 7.1.4 e PHP ≥ 8.3 de 64 bits. Laboratório: WordPress 7.1.4, PHP 8.4.24 de 64 bits, MariaDB 11.8.6. Site-Teste: WordPress 7.1.4, PHP 8.3.36. Padrão de desenvolvimento e instruções de agentes na revisão 5 de 02/11/2026; regra comum e aba do Meta consultadas.

## 2. Convivência, escopo e impacto recebido

Core 1.91.0, MCP 0.46.0, Google 0.36.0, LinkedIn 0.24.0 e Pipedrive 0.11.1 passaram na matriz de seis plugins com o Meta 0.28.0. No ensaio de cron, o **WP Activity Log 5.7.0 oficial** estava ativo junto com o Core e o Meta. O Site-Teste também tinha esse conjunto instalado. Hashes de entrada em `evidence/028/pacotes.json`.

O Core corrige suas próprias filas. Esta entrega corrige o worker do Meta; não exige nova alteração no Core, no LinkedIn nem nos demais pacotes. A recomendação recebida foi conferida contra a base e incorporada com validação mais estrita da identidade e tratamento da remoção nativa. A prova deste mantenedor está em `evidence/028/`; o encaminhamento recebido está preservado em `inputs/core-191-impacto-meta.md`. Nenhum novo pedido a outro plugin foi identificado. As leituras de Instagram, Facebook e Meta Ads continuam no escopo do Meta. Pixel, CAPI, contatos e escrita de campanhas não mudaram.

## 3. Mudanças e evidências — Pedidos core 423(e)

A tentativa de agendamento fixa o timestamp antes da escrita. Para um retorno normal de gravação ou `could_not_set`, a releitura deve encontrar o hook `f3_meta_worker`, aquele timestamp, argumentos vazios e uma ocorrência avulsa. A existência de outro evento, inclusive uma recorrência no mesmo horário, não confirma a tentativa. O código de veto continua sendo devolvido. Um worker pré-existente ou um evento efetivamente encontrado após `duplicate_event` continua sendo reaproveitado.

Os observadores anônimos de cron do sensor de sistema do WP Activity Log 5.7.0 podem devolver nulo depois que outro callback já gravou, removeu ou vetou o evento. O Meta preserva a decisão anterior para a criação e a remoção do seu próprio worker sem argumentos. O observador original continua sendo executado; sua chave, sua prioridade e os arquivos do plugin são mantidos. Se um observador passou por uma resposta positiva de remoção, a recuperação desse retorno verifica que a ocorrência exata já não existe. A falha real continua visível. Não há supressão do log do WordPress, troca do agendador ou nova escrita direta na opção cron.

| Prova com WordPress e sensor reais | Meta 0.27.0 | Meta 0.28.0 |
|---|---|---|
| `could_not_set` após criação avulsa comprovada | não reconhecia a gravação | reconhece e registra o código nativo |
| Evento ausente, em outro timestamp, com outros argumentos, ou recorrente | referência histórica nos recibos | quatro casos recusados |
| Retorno de veto antes do observador tardio | o sensor perdeu vetos na cadeia | veto preservado; remoção recusada conserva a ocorrência |
| Remoção já persistida antes do observador | 1 erro nativo `could_not_set` no log de wp-cron.php | 0 erros desse tipo no mesmo cenário |
| Duas chamadas a wp-cron.php para uma ocorrência devida | uma passagem; o erro de remoção não provava falha da coleta | uma passagem, um item concluído, uma página e uma linha gravadas |
| Recuperação com a fila pendente e o worker ausente | não usada como critério de aceite da base | diagnóstico detecta ausência, status rearma, duas chamadas executam a coleta uma vez |

Provas em `cron-base-returns.json`, `cron-returns.json`, `log-nativo.json`, `cron-*-dispatch.json` e `cron-recovery-seed.json`. Os filtros do sensor, a API de cron, a tabela de opções, o executor e a persistência da coleta são reais no laboratório. Um callback anterior controlado reproduz a ordem de gravação observada na investigação do Core; a resposta da Graph para a coleta é sintética. O evento de outro argumento foi preservado. O recibo da agenda não informa sucesso do item. As duas passagens por wp-cron.php são processos PHP separados.

**601 verificações automatizadas aprovadas**, além das sondas do Site-Teste. A contagem inclui 200 verificações em Chromium e 44 da matriz integrada; exclui falhas esperadas da base e a repetição de build. Contagem por suíte em `evidence/028/resumo.json`. As dez abas e três subvisões foram capturadas a 360, 768 e 1440 px (39 PNG). O ZIP das capturas contém o índice HTML. O pacote continua expondo 47 operações. A interface, as permissões e a política de retenção não mudaram.

## 4. Instalação e prova de prontidão

Conferir o hash e a raiz do instalador. No Site-Teste, o MCP aplicou o ZIP com `expected_slug` e `expected_sha256`, preservando o estado ativo. As sondas do instalador em / e /wp-json/ passaram antes e depois. Em novo processo, `meta/status` e `meta/health` retornaram versão 0.28.0 e estado ok; `meta/selftest` passou; `system/health` confirmou WordPress saudável. Os 32 documentos da ajuda foram lidos integralmente pela rota `meta/documentation` e comparados byte a byte com o instalador; hashes e paginação em `evidence/028/docs-site.json`.

No Site-Teste, com zero conexões, fila sem trabalho e sem evento pendente, foi criada uma ocorrência identificada do worker e executada via `cron/run` usando a revisão lida da agenda. A releitura confirmou zero eventos do worker, estado ok, zero itens processados e zero erros. Esse teste comprova acionamento e retirada no site compartilhado. O ensaio com coleta e entrada direta por wp-cron.php ocorreu no laboratório. Nenhum auxiliar temporário foi instalado no site e nenhuma mensagem comercial foi enviada. Produção não foi alterada.

## 5. Banco, retenção e recuperação

Nenhuma tabela, migração, opção de configuração ou credencial nova. A próxima gravação na opção de recibo existente acrescenta o timestamp solicitado, o código nativo e a indicação de correspondência exata. Os registros antigos continuam legíveis. A última falha histórica e a última passagem do executor continuam em campos distintos. A migração da 0.27.0 preservou os 15 registros, quatro linhas de histórico e a opção monitorada da base sintética. No Site-Teste foi feito backup prévio das duas tabelas do Meta (668 linhas) e de 8 opções. O pacote não distribui o backup. A reversão de arquivos não desfaz o processamento; correções posteriores requerem nova versão e retomada pelo checkpoint.

## 6. Limites da homologação

Não foi exercitada conta comercial real, entrega de webhook, nova autorização nem chamada externa à Graph. A prova do cron foi feita no laboratório e no Site-Teste, sem reproduzir a carga dos sites de produção. A observação de 24 horas e das métricas de frota do pedido 423 permanece com a operação e o mantenedor do Core. Os resultados aqui apresentados não encerram esse critério. A validação do sensor refere-se à versão 5.7.0.

## 7. Credenciais

Nenhuma credencial nova para esta atualização. Para conexão nova, o responsável informa o token e o segredo do aplicativo em Ferramentas → Fator3 MCP Meta → Conexão; o administrador seleciona App ID, versão da API, conta, ativos e permissões conforme CONFIGURATION.md. A Graph padrão continua v24.0. Nenhum dado secreto integra os arquivos.

## 8. Identidade

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-meta-fator3-0.28.0-instalador.zip | 275382 | `4c43ae254e2ad31797e7c83962aa6da6ea75b7d64587d17280e654ea3f35108b` |
| wp-mcp-meta-fator3-0.28.0-fonte.zip | 9481097 | `b11f21b07bf23e873228b73014e3461b98377e4a7f5a57ba5d7baa754935dcd5` |
| wp-mcp-meta-fator3-0.28.0-capturas.zip | 4107874 | `d5f76583bcc406d6fb396ccca6ac279e8c5b7c40266710ee90c36212a5a84655` |

A fonte inclui testes, evidências, documentação, código de build e uma cópia do runtime conferida contra o instalador. Os ZIPs têm raízes próprias e o instalador é reprodutível. Apenas o arquivo terminado em `-instalador.zip` é destinado ao WordPress.
