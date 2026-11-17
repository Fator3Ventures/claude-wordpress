# Entrega — Fator3 Site Core 1.91.0

Revisão 1 · 17/11/2026 · Retomada da implementação dos pedidos 421 a 425 · `base-site-core-fator3`

**Status da entrega: com-pendencias.** O instalador está ativo no Site-Teste. O executor confirmou a atualização, com zero falhas. O aceite de frota continua aberto. A revisão seguiu `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos na revisão 5 de 02/11/2026, além da regra comum e do padrão específico do Core.

## 1. De onde esta versão entra

Base de migração vigente: 1.90.0, recuperada da rodada anterior e confirmada no WordPress antes da instalação. Seu ZIP tem 5.622.059 bytes e SHA-256 `84a978143955df3803a6724fe5e967e1114b89476e198a52b594d6dc599c660f`. A 1.91.0 agrega funcionalidade nova. Destina-se a instalação nova em site único ou troca direta da base vigente. Requisitos declarados no cabeçalho e na documentação: WordPress 7.1.4+, PHP 8.3+ de 64 bits. A atualização foi exercitada em WordPress 7.1.4 e PHP 8.3.36. A instalação sem estado anterior permanece pendente.

## 2. Convivência e encaminhamentos

Site-Teste com MCP 0.46.0, Google 0.36.0, Meta 0.27.0, LinkedIn 0.24.0, Pipedrive 0.11.1, WP Activity Log 5.7.0, WP Super Cache 3.1.5 e Yoast 28.8. O Implantador não estava ativo. O envelope das 197 abilities manteve o conjunto de nomes da base. O catálogo de configuração tem 104 opções. O contrato administrativo é 8.43.0, o dicionário de dados é 8.39.0 e a referência de configuração é `piso-padrao-3.6`. Configuração, catálogo e diagnóstico continuam disponíveis ao consumidor MCP.

| Destinatário | Efeito e situação | Documento da entrega |
|---|---|---|
| Meta 0.27.0 | Pedido 423(e), ação necessária em `f3_meta_worker`, patch experimental validado, incorporação aberta | `base-site-core-fator3-1.91.0-impacto-wp-mcp-meta-fator3.md` |
| LinkedIn 0.24.0 | Pedido 423(e), ação necessária em `f3_linkedin_worker` e `f3_linkedin_lead_discovery`, patch experimental validado, incorporação aberta | `base-site-core-fator3-1.91.0-impacto-wp-mcp-linkedin-fator3.md` |

Os dois patches aplicaram na árvore exata do destinatário. Em WordPress real, 15 verificações com a API de agenda simulada confirmaram os resultados dos métodos alterados. A prova e os diffs estão em `tests/191/impactos/`. O Core já implementa a sua parte. As versões oficiais dos destinatários continuam as mesmas. Nenhuma mudança de contrato exigida do MCP principal, Google, Pipedrive ou Implantador foi identificada nos cinco pedidos. Uma operação de fornecedor não foi homologada.

## 3. Mudanças e evidência

### Pedidos core 421 · Continuação do GA4

A 1.90.0 podia reabrir após 24 h um recorte histórico vazio e usava outra passagem para descobrir o fim. A 1.91.0 trata o histórico concluído ou vazio como terminal. A janela recente pode ser revisitada no próximo dia local. O coletor agenda a continuação num quarto de hora UTC, considera quota e próxima coleta diária e não agenda outra passagem quando o próximo recorte é inelegível. Em um lote com N páginas elegíveis, N ≥ 1, são uma coleta inicial e N − 1 continuações, salvo cota, falha ou retentativa. Não existe uma contagem diária fixa para todas as propriedades.

Prova `validado-wordpress`: com seis recortes históricos vazios e quatro páginas recentes sintéticas nas tabelas do acervo, o seletor passou pelas quatro páginas, encerrou após três continuações e ignorou os seis históricos. Foram verificados os minutos UTC 00, 15, 30 e 45. Dados revertidos na transação. O ensaio não consumiu cota externa nem executou um dia de cron real.

### Pedidos core 422 · Identificação de aparelhos

O índice compara nomes publicados para fabricante e Device, ignora diferenças só de região ou grafia e usa a frequência no Device para desempatar alternativas substantivas. Empates e conflitos mantêm o código técnico. O LG Q60 usa a identificação brasileira expressamente pedida para LM-X525.

| Model | Nome retornado pelo índice Google no WordPress |
|---|---|
| LM-X525 | LG Q60 |
| RMX3834 | realme Note 50 |
| RMX3933 | realme Note 60 |
| CPH1903 | AX7 |
| ZTE 7060 | ZTE Blade A73 |

Auditoria independente da fonte congelada de 15/11/2026: 44.528 códigos, 256 blocos, 43.001 `nome_google`, 802 `modelo_sem_nome_publicado` e 725 `modelo_ambiguo`. O levantamento percorreu toda a base, inclusive casos além dos 785 apontados no pedido. Dos 826 candidatos com alternativa, 453 receberam nome comercial, 272 conservaram o código por região/grafia e 101 por ambiguidade. O ensaio verificou que nenhum candidato com alternativa substantiva inequívoca conservou o código. A lista nominal das exceções está em `reference/422/auditoria.csv`. As 30 fichas embarcadas da frota ficaram idênticas campo a campo. As 1.350 linhas da base comercial têm preço positivo em reais e o CSV é idêntico ao da 1.90.0. Não houve nova pesquisa de preços nesta rodada. Evidências em `evidence/1910/{catalogo,integridade-google,frota-catalogo}.json`.

### Pedidos core 423 · Agenda de seis filas

O WP Activity Log pode apagar, no fim da prioridade `PHP_INT_MAX`, a confirmação devolvida pelo filtro do Core. Nesse caso o WordPress tenta gravar de novo a mesma lista de eventos. A agenda inicia antes da escolha do perfil e reposiciona seus callbacks nos três filtros de agendamento, reagendamento e remoção. Para o reagendamento calcula o próximo horário como o núcleo. A remoção da antecipação vencida requer executor presente. O diagnóstico de aplicabilidade identifica origem, perfil, registro dos filtros e plugins posteriores ou reposicionados.

Ensaio A/B no Site-Teste com os callbacks reais do WP Activity Log colocados na ordem observada na frota e uma tabela de opções temporária. Em cada versão foram invocados os mesmos seis ganchos pela API pública do cron.

| Resultado | 1.90.0 | 1.91.0 |
|---|---:|---:|
| Agendamentos confirmados pela API | 0/6 | 6/6 |
| Reagendamentos confirmados pela API | 0/6 | 6/6 |
| Remoções confirmadas pela API | 6/6 | 6/6 |
| Retornos `could_not_set` | 12 | 0 |

Na nova versão, seis avulsas também foram confirmadas. Para uma ocorrência vencida, o processo cron sem callback recebeu `fila_sem_executor` e a ocorrência continuou presente. Com o trabalhador registrado, a remoção foi confirmada. O ensaio isola a ordem dos filtros e o retorno da gravação. A janela de 24 h, a concorrência B/C/E e a frequência do cron da frota têm critérios separados na seção 6.

### Pedidos core 424 · Diálogo, telemetria e saída para WhatsApp

A interação captura o instante e os dados que dependem do elemento. O Core desloca o trabalho de análise, fila, armazenamento e envio ligado à interação para uma tarefa depois de `requestAnimationFrame`. Preserva a ordem, esvazia trabalho pendente em `pagehide` e ao ocultar o documento, consulta o consentimento vigente e envia com `keepalive`. O texto do link usa `textContent`. O adaptador mantém a abertura imediata, controle de foco e teclado. A invalidação no consentimento e na troca de modo de teste evita entregar trabalho do contexto anterior. Não houve alteração de CSS do tema. Referência técnica: [Otimizar o INP](https://web.dev/articles/optimize-inp).

| Medida do navegador no Site-Teste | 1.90.0 | 1.91.0 |
|---|---:|---:|
| Cliques em páginas independentes | 10 | 10 |
| Duração do clique em Event Timing, mediana | 16 ms | 16 ms |
| Processamento do clique, mediana | 3,95 ms | 1,65 ms |
| Páginas com algum quadro longo (LoAF) | 9/10 | 10/10 |
| Leituras do cookie por rodada, intervalo | 141–145 | 155–180 |
| Tempo acumulado nessas leituras, intervalo | 3,2–6,5 ms | 5,9–8,8 ms |

Chrome desktop com cliques reais, formulário instrumentado e confirmações de eventos locais para as 20 medições. As 20 sequências mantiveram a ordem e não registraram erro JavaScript. O navegador não forneceu atribuição por script para os quadros longos observados. A dispersão das leituras inclui a sequência de eventos do ensaio. A decisão de guardar consentimento em memória depende da medição em aparelho físico pedida pelo dono. O custo acumulado não caiu neste teste. Não há estimativa do INP p75 móvel nem reprodução do teclado virtual ou do tema do CTO Office.

Uma segunda prova usou o formulário registrado `contato`, sessão anônima, segmento `teste`, token público e o coletor real do Site-Teste. Cada um dos dois caminhos, fechamento normal e saída imediata para `https://wa.me/`, persistiu dez eventos. Nos dois, `clique_link → oferta_aberta → form_dialogo → form_inicio → form_aceito → oferta_fechada` apareceram uma única vez, na ordem. A leitura em `f3base/eventos-ler` verificou o clique nos dois caminhos canônicos. A tabela de análise confirmou os demais eventos. A consulta autenticada de editor havia sido recusada pelo controle de medição; a prova usou o contexto anônimo. O teste verificou o recebimento no WordPress durante a saída, sem envio de mensagem WhatsApp. Valores das 20 rodadas em `evidence/1910/navegador.json`; recibos em `evidence/1910/wordpress.json`.

### Pedidos core 425 · Recibos de wp_mail e incidente histórico

A fila persiste assunto sanitizado, processo, gancho/chamador, destinos mascarados e indicador de destino igual à caixa. A UI/ability administrativa lê esses campos depois da limpeza do conteúdo cifrado. A fase de preparo distingue endereço vazio, sintaxe e recusas da configuração do servidor. Quando o servidor SMTP fornece um retorno no envelope, são distinguidos domínio sem entrega (5.1.2) e política (5.7.x). O envio à própria caixa é identificado como tal. A contingência reserva uma notificação por ciclo, com recibo do canal.

Teste em WordPress com fila e opções temporárias: duas chamadas nativas a `wp_mail` no gancho de teste geraram dois recibos de `destinatario_sintaxe` na fase de preparo, com processo, gancho e assunto. Houve um aviso de contingência interceptado em `pre_wp_mail` e aceite local registrado. Em caso separado, endereço vazio produziu `destinatario_vazio`, endereços válidos ficaram mascarados e um número no assunto foi suprimido. Envio ao provedor e chegada à caixa final ficaram fora do teste.

Na 1.90.0, `smtp_destino_invalido` em `preparo` vem da validação do **servidor SMTP**. O código agrupava porta/TLS, sintaxe de host, política de URL e resolução de rede. Os registros disponíveis não discriminam qual condição falhou nem guardam o assunto ou o destinatário mascarado. Em sete sites confirmamos, por leitura, o padrão histórico do mesmo minuto de 16/11/2026: Fator3, Twinia, Engagia, Conselar, Fator3 Ventures, Fator3 Capital e Desenvolvimento de Softwares. Na Fator3 a consulta ao log de auditoria na janela não encontrou registro que identificasse a mensagem. A coincidência com a passagem CLI situa o incidente, mas não identifica qual tarefa chamou `wp_mail`. A revisão automática de acesso recusou a leitura da fila de produção do Fator3 Grupo por sensibilidade e falta de autorização específica para a fonte e a operação. AWN Ventures não tinha conector disponível. Não há base para preencher retrospectivamente o conteúdo ou o destinatário das nove mensagens.

## 4. Instalação e prova de prontidão

1. Conferimos SHA-256, os 1.265 arquivos do instalador contra a árvore fonte e a análise sintática de 609 arquivos PHP pelo PHP 8.3.36 do WordPress. Na reconstrução de assets, 85 arquivos ficaram idênticos. A distribuição contém apenas `base-site-core-fator3/` com seu runtime e documentação.
2. Com o MCP do Site-Teste, o ZIP integral foi preparado na área temporária e instalado pela ability `plugins/upload-base64` a partir do arquivo preparado, verificando slug e SHA-256. A operação `06832592c16be129d3b2cac8d35fab3f` registrou versão anterior 1.90.0, nova 1.91.0 e plugin ativo antes e depois. As sondas de `/` e `/wp-json/` retornaram HTTP 200 antes e depois.
3. A leitura de prontidão em novo processo confirmou `estado=concluida`, `falhas=0`, `confirmada_no_executor_em=1794923947` (17/11/2026 às 10h59min07s de Brasília). Depois da verificação pendente de robots, foram registrados zero módulos degradados, zero tarefas com última falha e zero esperas pendentes. Essa observação corresponde ao instante da leitura.
4. O índice documental e a ability de leitura do Core permitiram recuperar `docs/RELEASE-1.91.0.md` e o documento canônico `docs/DOCUMENTACAO.md`. Este foi lido em seis páginas até o fim. O SHA-256 remoto reconstruído, `d80a2841e547557a09c68edc4beaf6a92f197d122783e9f1893cc3709de55804`, coincidiu com o arquivo do instalador. O cabeçalho e a declaração do menu foram conferidos no código: “Fator3 Site Core”, menu “Site Core”, permissão administrativa `manage_options`.
5. Retiramos os dois MU-plugins e as duas páginas temporárias do teste. A releitura individual dos quatro caminhos confirmou ausência. O ZIP de transferência também foi removido. Restaram os recibos dos dois cenários anônimos no segmento de teste para auditoria, sujeitos à retenção normal. Fila e tabelas temporárias das outras provas não permanecem ativas. Nenhuma instalação de produção recebeu a 1.91.0 nesta rodada.

## 5. Banco, migração e correção por nova versão

A fila `{prefixo}f3base_wp_mail` recebe a coluna anulável `diagnostico`; linhas antigas continuam legíveis e a UI identifica a família de erro legada. O conteúdo sensível da mensagem continua cifrado e é limpo após o processamento. O Core conserva as opções operacionais, o histórico e os checkpoints do acervo. A correção de cron grava sobre o estado vigente da opção `cron` e confere o resultado para preservar eventos alheios. As provas de agenda e de e-mail usaram opções temporárias. O Site-Teste continuou com as suas configurações, sem solicitação de nova credencial. Não foi feita comparação integral de cada registro e segredo da instalação. Manter o backup operacional de banco/arquivos e os recibos do instalador; em caso de nova falha, corrigir por versão posterior e retomar pelos checkpoints registrados.

## 6. Pendências de validação

| Pedido/escopo | Critério em aberto | Responsável / condição |
|---|---|---|
| Instalação limpa e Core isolado | Primeira ativação em banco vazio e sem acompanhantes | QA do Core. O kit do laboratório recuperado não continha os executáveis PHP, WP-CLI e MariaDB. A atualização real foi exercitada no WordPress compartilhado. |
| 421 | Perfis A/C, cron de servidor de 15 min, WP-Cron por visita, cron/list a cada 5 min até terminar o lote. Na frota, três horários entre 09h e 21h UTC nos seis sites do 405, sem atraso superior a 60 s nem espera por escopo divergente | QA do Core e frota após a troca |
| 423 | Matriz de visitas concorrentes em B/C/E. Em CTO Office, 24 h com WP Activity Log ativo, menos de dez erros nos seis ganchos, nenhuma ocorrência duplicada ou consumida sem executar e CAPI antecipada só com item novo | QA e operação CTO Office. A conferência das primeiras 24 h do **Site-Teste** está agendada para 18/11/2026 às 11h05 de Brasília. O laboratório da 1.90.0 é histórico. |
| 424 | Repetir a medição com CPU móvel 4× e em aparelho real para consentimento. Em CTO Office, sete dias com mediana do processamento do botão abaixo de 378 ms e relação de aberturas/cliques preservada | QA de desempenho e operação CTO Office. Os tempos desta entrega são de desktop, sem atribuição LoAF por script. |
| 425 | Migração especial 1.89.2 → 1.91.0 nos perfis A a E e duas horas de recibos. Após a troca na frota, 48 h nos 12 sites sem nova falha legada | QA do Core e frota. A identificação histórica depende de registro contemporâneo independente. |
| Meta e LinkedIn | Incorporar patch ou alternativa e validar o log nativo, inclusive remoção de avulsas | Mantenedores dos dois pacotes. Os relatórios individuais incluem critério, diff e hash. |

## 7. Credenciais

O Core não introduz credencial, escopo OAuth nem mudança de permissão nesta versão. O dono mantém a conta GA4 e a caixa SMTP já configuradas no Site Core. Os testes de recebimento usaram o token público emitido pelo site para o navegador. Os arquivos não incluem seu valor. A contingência foi interceptada antes do transporte.

## 8. Identidade dos arquivos

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| [base-site-core-fator3-1.91.0-instalador.zip](base-site-core-fator3-1.91.0-instalador.zip) | 5.640.204 | `5d0358f62d42a9232ee1bce216bd8ea2b41ea284bc16ef454ad8f9c103aa3e41` |
| [base-site-core-fator3-1.91.0-fonte.zip](base-site-core-fator3-1.91.0-fonte.zip) | 7.526.655 | `f780f372f3ffe1417a240eb94f9f2aa7329f5a1d0fb3e270ff6c600d40758f77` |

A cópia interna `RELATORIO-PRE-FECHAMENTO.md` antecede o fechamento do ZIP fonte. O manifesto cobre o conteúdo interno. A verificação final abrangeu todos os registros e hashes do manifesto e a igualdade entre cada arquivo do runtime no fonte e no instalador. O ZIP instalador é o único destinado à instalação no WordPress.

Complementos desta entrega:

- [base-site-core-fator3-1.91.0-catalogo-aparelhos.csv](base-site-core-fator3-1.91.0-catalogo-aparelhos.csv)
- [base-site-core-fator3-1.91.0-impacto-wp-mcp-linkedin-fator3.md](base-site-core-fator3-1.91.0-impacto-wp-mcp-linkedin-fator3.md)
- [base-site-core-fator3-1.91.0-impacto-wp-mcp-meta-fator3.md](base-site-core-fator3-1.91.0-impacto-wp-mcp-meta-fator3.md)
