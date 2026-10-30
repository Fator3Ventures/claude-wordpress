# Entrega — Fator3 MCP 0.38.0

30/10/2026. Base direta 0.37.0. **Versão corrente: 0.38.0, instalada e ativa no Site-Teste. Situação: com-pendencias de aceite coordenado.**

A auditoria de serviço passa a descobrir o catálogo quando necessário. O login e a página pública deixam de abrir o catálogo de habilidades apenas pelo bootstrap do MCP. Primeiro recibo, leitor administrativo, revogação e contratos foram preservados nos testes. Nenhuma regressão foi observada nos cenários executados.

O Pedido Core 354 permanece parcialmente atendido: a comparação com/sem Core e Pipedrive ficou dentro de 100 ms no login, mas ainda excedeu o limite na página pública. Esse resultado não bloqueia a correção MCP nem encerra o trabalho do Core.

## 1. Bases aceitas e entradas

| Entrada | Identidade aceita |
|---|---|
| MCP 0.37.0 instalador | 912702 bytes; SHA-256 `cbece53fc479d9fe3963b111e49e789d92609c5462102877244dcaebcf7cf3ec` |
| MCP 0.37.0 fonte | 5074415 bytes; SHA-256 `e2654b93a9bababb283cb870b4f5f94ac17ad9a188ea23bb2cd3a8b77f7bb49c` |
| Core 1.63.0 instalador | 2986868 bytes; SHA-256 `afd99c56edc9445f7498e010d3123d8497fd0dd335b3cc283b5156c7de855c5b` |
| Google 0.24.0 instalador | 886260 bytes; SHA-256 `803fa058182b9f43625352f2b4a1572a3cd4b728f8c07fd58314a9a111d41849` |
| Meta 0.17.0 instalador | 327384 bytes; SHA-256 `a360feff0bdb723c7f3c2a240b288bc1c3af917e851cb798d905e31a95b4162d` |
| LinkedIn 0.13.0 instalador | 314596 bytes; SHA-256 `1c45738322f4901aeacdc36615789ae961e8b9d521ba321a27de0aea76c13502` |
| Pipedrive 0.5.0 instalador | 95019 bytes; SHA-256 `59e8c99d5bb8a54fcfeaba06c56d816b940a1fe97a7d6b473d13a252c6e5042a` |

Foram considerados os fontes e relatórios recebidos de Core, Google, Meta e Pipedrive, além do impacto `base-site-core-fator3-1.63.0-impacto-wp-mcp-fator3.md`, revisão 1, relacionado ao Pedido Core 354 (3488 bytes; SHA-256 `2ab159b8f69e241fcf8a9807e56ff73e314718ac4941e629f7afe0f150d8ffe0`). A base MCP e o instalador LinkedIn foram recuperados e conferidos; não se presume um fonte LinkedIn separado recebido nesta rodada. Identidades completas dos anexos: `evidencias/0380/inputs.json` e `recovered-inputs.json`.

Normas comuns revisão 5, preservadas em `docs/entradas/0330/`, aplicadas. O plano foi registrado antes da implementação em `docs/PLANO-0380.md`. Não foi inventado número de pedido MCP para a demanda Core 354.

## 2. Convivência e encaminhamentos

| Fronteira | Resultado desta rodada |
|---|---|
| Impacto Core 1.63.0 r1 / Core 354 → MCP | Atendida a mudança no caminho de inicialização do MCP. Catálogo não aberto no bootstrap público/login; descoberta administrativa e recibos confirmados. Critério de desempenho global ainda não aceito na página pública. Resposta registrada neste relatório, sem reemitir impacto para encerramento. |
| MCP 0.37.0 → Core, r1 / Core 334 | O Core 1.63.0 já fornece `itens` com revisão opaca, mantendo o alias legado `credenciais`. Onze testes próprios locais por MCP HTTP confirmaram ajuda/estado/revisão, prévia com revisão obtida pelo transporte, recusa de revisão obsoleta/perfil e ausência de segredo. Atendimento do contrato observado na bancada; a prova remota com credencial privada não foi repetida. |
| Google 0.24.0 | 298 abilities mantidas; código e relatório atual considerados, inclusive domínio do acervo Ads no Core. Não exige alteração de transporte nesta rodada. |
| Meta 0.17.0 | 47 abilities mantidas; orçamento de trabalho e prioridade de coletas permanecem responsabilidade Meta. Provas recebidas não são contadas como testes próprios MCP. |
| LinkedIn 0.13.0 | 93 abilities e produtor real do instalador usados na bancada; aquisição e ações comerciais com HTTP sintético, primeiro evento, replay, revogação e leitor administrativo comprovados. |
| Pipedrive 0.5.0 | Dezenove abilities descobertas no Site-Teste; versão/ativação confirmadas. Não ativado na bancada PHP 8.3.6, pois exige PHP 8.3.36/WordPress 7.1.3. Sem operações comerciais de Pipedrive executadas para homologação. |

Nenhum código de acompanhante foi modificado. Não há novo impacto técnico que exija encaminhamento separado. A pendência de desempenho já pertence ao impacto recebido e continua sob Core/MCP e responsável pela homologação coordenada. A versão preserva os aceites históricos MCP 70/74 e o encerramento B22/CIMD; não os reabre.

## 3. Mudanças por pedido e evidência

Mudança funcional restrita a `includes/MutationServiceAudit.php`:

- Listener de eventos permanece instalado no bootstrap.
- Preparação por `wp_loaded` limitada a administração, cron e contexto WP-CLI; API REST, catálogo solicitado por outro consumidor, consulta e primeiro evento também inicializam quando necessário.
- Guarda de reentrada e recusa de inicialização anterior a `init` evitam catálogo parcial/registro antecipado.
- Validação de descritor, origem PHP, leitor decorado, concessão, identidade, permissões, digest e persistência permanece intacta.

Quatro arquivos distribuídos diferem da base: o arquivo funcional, cabeçalho/constante de versão e dois guias compilados. Nenhum arquivo distribuído foi acrescentado ou removido. Sem novo schema, opção, tabela, migração, concessão ou contrato.

**282 verificações funcionais aprovadas em 14 resultados, zero falhas no fechamento.** Asserções de ensaio não equivalem a 282 integrações comerciais independentes.

| Grupo | Verificações |
|---|---:|
| Contextos públicos, login, admin, cron, CLI, REST, catálogo, uso inicial e reentrada | 35 |
| Catálogo e schemas por HTTP com acompanhantes | 9 |
| Preparação isolada e primeiro evento de aquisição/comercial | 17 |
| Auditoria de serviço, privacidade, replay, permissões e revogação | 45 |
| Regressão UTF-8 em logs / MCP 75 | 75 |
| Documentação completa por MCP HTTP | 40 |
| Retorno neutro de metadados / Core 334, somente local | 11 |
| Atualização direta 0.37.0 → 0.38.0 | 24 |
| Instalações limpas WordPress 7.1.2 e 7.1.4 | 26 |

Separadamente: 39 verificações da base, paridade exata de **801 schemas/anotações/publicação/providers**, e 15 gates de pacote incluindo lint de 456 arquivos PHP. Não somar os lints novamente aos gates. Os dois problemas iniciais do roteiro (nome inexistente `google/health` e chamada anterior a `init` na base) foram diagnosticadas: o roteiro usa a ability publicada `google/status`; o cenário anterior a `init` é validado na candidata com a nova guarda. Os resultados finais registrados não apresentam falhas.

Bancada: WordPress 7.1.4, PHP 8.3.6 CLI/FPM, MySQL 8.0.46 e lighttpd 1.4.74; acompanhantes originais da tabela, exceto Pipedrive. Mínimo MCP comprovado com WordPress 7.1.2/PHP 8.3.6, sem acompanhantes. O teste CLI cobre o contexto de bootstrap com stub de registro de comandos, não a execução do wp-cli.phar. Fornecedores simulados e correio interceptado. Reprodução: `tools/release0380/README.md`; resultados: `evidencias/0380/validation-summary.json`.

### Desempenho observado

No Site-Teste, o profiler Core passou de 172 para 86 arquivos no login; na página, de 219 para 179–181. O rótulo `catalogo-completo` do profiler Core descreve configuração interna do Core e não comprova inicialização do registro global WordPress. Nos processos novos da bancada, `wp_abilities_api_init` passou de uma execução na base para zero no bootstrap público/login; demanda posterior cria o catálogo uma vez.

Métrica de aceite: menor `generation_ms` entre três amostras de cada rota, cache bypass comprovado por nonce PHP, `contexto_teste:true`, origem interna no mesmo site. Não é TTFB, nem uma medição isolada do custo do MCP.

| Rota | 0.38 com Core/Pipedrive | 0.38 sem os dois | Diferença | Limite 100 ms |
|---|---:|---:|---:|---|
| `/` | 715,181 ms | 331,558 ms | 383,623 ms | Não atende |
| `/wp-login.php` | 331,991 ms | 263,157 ms | 68,834 ms | Atende |

Após reativação: mínimos 691,530 ms na página e 320,996 ms no login, diferenças 359,972 e 57,839 ms perante a série sem os dois. A conclusão não muda. Antes da atualização MCP, nesta rodada, mínimos com o conjunto ativo eram 1154,209 ms e 453,226 ms; a variação da hospedagem impede atribuir toda a redução à mudança. A sonda anterior embutida na instalação teve outra amostra e não é mesclada às séries de três. Todos os valores brutos e o cálculo estão em `remote-probe-*.json` e `performance-summary.json`.

## 4. Instalação, documentação e prontidão

**Site-Teste:** https://fator3-teste-mcp-1.dreamhosters.com/ — WordPress 7.1.4/PHP 8.3.36. Operação `e7e36fa67e71d45cac5a0efbf77278e0`, de 0.37.0 para 0.38.0, concluída; versão ativa observada em nova requisição PHP. ZIP recebido com o hash do instalador final. `system/health` saudável, 11 checks verdadeiros e contrato de auditoria de serviço registrado sem erro.

Inventário remoto: 467 arquivos, nomes e tamanhos iguais ao ZIP, hashes dos quatro arquivos alterados iguais, verificador nativo da operação identifica a árvore completa como `candidate`. Prévia de rollback confirmou pré-imagem. Sondas finais `/`, `/wp-login.php` e `/wp-json/` passaram com 200 e bypass comprovado. O instalador usou `silent_reactivation`; não se declara ciclo completo do hook de ativação ou prontidão comercial universal.

Documentação: 37 documentos instalados lidos integralmente em 40 páginas por MCP HTTP na bancada, com conteúdo/hash iguais ao compilado; cursor divergente e caminho arbitrário recusados. `release-0380` também lido completo no Site-Teste, SHA-256 `bfeeb33e7ee8cb05f40f7f9217319870316322969d0ff657f6a1fc24ad6e82a0`.

Para a comparação coordenada, Core e Pipedrive foram temporariamente desativados e reativados por suas operações nativas, em sequência. Os nove plugins voltaram às mesmas versões/estados ativos de antes; os demais não foram desativados. O ciclo nativo renovou horários de agenda e a geração de cache, sem pretensão de preservar esses timestamps byte a byte. Após a retomada, Core operacional, mesma geração de recuperação 7, mesmo ciclo de atualização concluído, robots com entrega confirmada, llms próprio/ativo sem pendência e cache novamente `verified` (`cabecalhos_comprovados`). O cache foi confirmado pelo ciclo natural; não foi executado cron genérico nem job comercial para produzir essa prova.

## 5. Banco, reversão e preservação

A implementação não altera tabelas, opções, credenciais, concessões ou formato dos registros. O upgrade local preservou senha de aplicativo, OAuth/perfil/expiração/refresh, opções falsas/vazias, backups, recibos concluídos/incertos, idempotência e confirmação SQL pendente. Os testes SQL ficaram no banco descartável, usando duas fases.

Pré-imagem remota da base: `23962692c7fec37a867f2602`. Rollback simulado: `rollback_ready:true`, `preimage_verified:true`, `applied:false`. Reverter arquivos restauraria também a inicialização antecipada da 0.37.0. Não desfaz operações comerciais, registros ou efeitos externos. A operação de instalação e o ciclo temporário dos acompanhantes geraram seus recibos e efeitos normais de lifecycle; não houve reset do banco compartilhado nem edição direta de agendas/opções para mascarar resultados.

## 6. Pendências e limites

- **Core / homologação coordenada — Pedido 354:** reduzir e medir o trabalho restante na página pública; critério global segue aberto. A causa MCP indicada no impacto foi tratada; não se atribui automaticamente todo o custo restante ao Core ou ao Pipedrive.
- **Frota:** implantação desta versão nos demais sites e aceite específico MCP 75 em ctooffice permanecem fora desta rodada. Os aceites 70/74 já recebidos não foram reabertos.
- **Core 334 / credenciais:** contrato atualizado comprovado em laboratório sintético. Não repetida leitura remota de credencial privada; a rejeição automática da rodada anterior continua respeitada. Nenhuma rota indireta foi usada. Homologação com contas reais pertence aos responsáveis autorizados.
- **B22/CIMD:** encerramento histórico de 21/10/2026, registrado na 0.25.0 r3, preservado. A conexão OAuth existente e o upgrade foram exercitados; não houve novo consentimento externo do zero nem repetição integral da suíte CIMD nesta rodada.
- **Não comprovado:** multisite, Redis/Memcached, navegador visual, comandos WP-CLI reais, outros runtimes, SMTP/IMAP e fornecedores reais, CDN/acesso externo e observação prolongada. Pipedrive tem prova remota de descoberta/ativação, sem regressão comercial local no mínimo PHP MCP.

Não há correção MCP conhecida pendente no escopo testado. A ausência de regressão observada se limita às provas descritas. Testes/relatórios recebidos dos outros mantenedores não são declarados como executados nesta sessão.

## 7. Credenciais e operação

Não são necessários segredo, perfil ou concessão novos para atualizar. Evidências distribuídas não incluem credenciais reais, cookies, banco do laboratório, logs pessoais brutos ou helpers de transferência. Valores de credenciais usados nos testes locais são sintéticos. A proteção `fator3-redaction/1` foi mantida; o retorno neutro é fornecido pelo Core, sem exceção MCP para revelar segredos.

Não houve publicação GitHub/feed, implantação em frota, mensagem a terceiros, homologação por envio comercial real, rota de PHP arbitrário ou SQL remoto de contorno. Nenhum arquivo de pacote alheio foi editado. A retomada dos acompanhantes deixou seus ciclos operacionais normais ativos; isso não é prova de cada job comercial em segundo plano.

## 8. Artefatos finais e estado da entrega

Instalar exclusivamente o ZIP instalador. O fonte contém código, ferramentas, documentação, evidências sanitizadas e cópia identificada deste relatório anterior ao fechamento; nenhum ZIP inclui outro ZIP da entrega.

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| `wp-mcp-fator3-0.38.0-instalador.zip` | 913547 | `bc550c6573527a0d71bfa560036f83e7c8aec546f49d70b8e0095da5d303c1a5` |
| `wp-mcp-fator3-0.38.0-fonte.zip` | 6041317 | `cdf50f0d75c1dba5dbea1a6f1d687fad04bea67a43ddc98fd24c6ff526c9a7f1` |

O instalador foi congelado antes da instalação remota; nenhum byte foi alterado depois. O fonte foi empacotado uma vez após as evidências e o relatório interno. A extração do fonte e o rebuild reproduziram exatamente o instalador entregue. O hash final do fonte fica somente neste relatório externo, evitando circularidade. Não há arquivo de impacto novo nesta rodada.
