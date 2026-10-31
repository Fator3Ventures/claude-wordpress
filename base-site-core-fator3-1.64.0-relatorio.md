# Entrega — Fator3 Site Core 1.64.0

Revisão 1 · 31/10/2026 UTC · implementação e validação WordPress · contrato administrativo **8.29.0**.

**Status: com-pendencias.** Instalador funcional e validado no escopo descrito, instalado no Site-Teste; pedidos 357, 358 e 359 implementados e validados em WordPress. Pedido 360 implementado com validação técnica parcial e aceite de frota pendente. O pedido 354 continua parcial: o login atende ao limite comparativo, mas a página ainda apresenta diferença de 130,460 ms, acima dos 100 ms pedidos. A medição não instrumentada também não atende ao teto de 20 ms.

## 1. De onde a versão entra

Entrada comprovada em WordPress limpo e **atualização direta de 1.63.0 para 1.64.0**, sem versão intermediária. Base canônica recebida e conferida:

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| base-site-core-fator3-1.63.0-instalador.zip | 2986868 | afd99c56edc9445f7498e010d3123d8497fd0dd335b3cc283b5156c7de855c5b |
| base-site-core-fator3-1.63.0-fonte.zip | 6154936 | 85d71ef5885e6a6a0fb6abb381d3edfc250d067f8b9d584ec557aab019479d7f |

Referências: documento `Fator3 Site Core(20261030-225821).md`, relatório e instalador do MCP 0.38.0, instruções comuns e padrão de desenvolvimento revisão 4. O fonte conserva os documentos recebidos, o plano e a evidência histórica. O runtime entregue deriva da fonte canônica 1.63.0.

Mínimos comprovados para o Core: **WordPress 7.1.2 e PHP 8.3.6**. Também validado com WordPress 7.1.4/PHP 8.3.6 em bancada e WordPress 7.1.4/PHP 8.3.36 no Site-Teste. Os ciclos de instalação limpa, atualização, repetição, desativação/desinstalação preservadora e reativação usaram o ZIP final nos dois WordPress locais.

## 2. Convivência

| Pacote | Versão verificada | Evidência |
|---|---|---|
| Fator3 MCP | 0.38.0 | Canal nativo, documentação paginada, controle de permissões e recibos |
| Fator3 MCP Google | 0.24.0 | SDK, concessões, revogação e leituras com respostas sintéticas |
| Fator3 MCP Meta | 0.17.0 | SDK e contratos de configuração/leitura com respostas sintéticas |
| Fator3 MCP LinkedIn | 0.13.0 | Registro, identidade e convivência no carregamento público |
| Fator3 MCP Pipedrive | 0.5.0 | Ativo no PHP 8.3.36; registro e bloqueio de recuperação, inclusive processo novo |

Os cinco estavam e permanecem ativos no Site-Teste. Yoast SEO 28.8 e WP Super Cache 3.1.4 também permaneceram ativos. A bancada local não comprova ativação do Pipedrive: PHP 8.3.6 é inferior ao mínimo 8.3.36 desse acompanhante; sua prova foi feita no Site-Teste.

Não foi identificado impacto que exija alteração em outro pacote nas fronteiras examinadas. Os contratos SDK foram preservados; callbacks de configuração passam a ser resolvidos quando usados. `f3base_cron_rotina` é adesão opcional: tarefas dos acompanhantes não são reclassificadas automaticamente. Nenhum acompanhante foi modificado e não há relatório individual de impacto nesta entrega. Não há nova ordem obrigatória de troca além de usar os contratos disponíveis; a combinação comprovada inclui MCP 0.38.0. Chamadas comerciais a fornecedores e concessões reais adicionais não foram homologadas.

## 3. Mudanças e evidência

### Pedidos core 357 — spam por sinal

Adicionada a opção booleana `spam`, padrão falso, em cada regra de `f3base_formularios_sinais`. Um sinal marcado como spam prevalece sobre os avisos. A captura e o complemento da segunda etapa persistem suspeita e atendimento spam antes das entregas; avisos, conversão, intenção de Pipedrive e e-mail automático ficam suprimidos. Complemento que passa a spam cancela saídas pendentes. A revisão de suspeitos exclui spam; a interface apresenta a coluna própria e contagens de 7/30 dias. Restauração administrativa explícita continua possível.

**Estado:** implementado, validado-localmente, validado-wordpress. Provas: 30 verificações conjuntas dos pedidos 357–359; 20 da captura real no banco isolado, incluindo sinais simultâneos, ausência de saídas, complemento, contagens, restauração e 30 checkboxes na interface. Não houve entrega de contato real.

### Pedidos core 358 — persistência do alerta de robots

`f3base_avisos_tecnicos.robots_sem_confirmacao_minutos` aceita 15–1440 minutos, padrão 120. O ciclo registra tentativas, última falha/código e duração. Uma falha transitória dentro da janela não dispara atenção; após o prazo, a reserva impede duplicação. Recuperação só avisa depois de atenção aceita pelo transporte. O diagnóstico está em `robots_retomada`, em `f3base/saude-ler`.

**Estado:** implementado, validado-localmente, validado-wordpress. Foram exercitados janela, atenção única, recuperação condicionada e ausência de duplicação. Aceitação por `wp_mail` não comprova recebimento na caixa postal.

### Pedidos core 359 — e-mails nativos do WordPress

Nova política `f3base_email_wordpress`, com nove escolhas booleanas: mensagens de sucesso automáticas desligadas no padrão; falhas, atualização crítica/manual e recuperação de erro fatal preservadas. O filtro mantém falhas em lote misto, não desliga o mecanismo de atualização e não suprime outros e-mails do site. Configuração segue schema, simulação, revisão/CAS e permissões administrativas.

**Estado:** implementado, validado-localmente, validado-wordpress. Testes usam o fluxo nativo e transportes interceptados. A próxima atualização automática real e sua entrega postal permanecem pendentes.

### Pedidos core 354 e 360 — carregamento, cron, estrutura e desempenho

- Descoberta Markdown usa `f3base_llms_mapa` compacto, com autoload, e `f3base_llms_assinatura`; a visita não monta a seleção completa nem consulta Yoast por item. Alteração de publicação, senha, exclusão e noindex remove o item do mapa imediatamente. Geração posterior o recompõe. Treze verificações locais cobrem retirada imediata, elegibilidade, equivalência do vínculo e entrada na geração seguinte, em seleção de 50 itens, dos quais 48 criados pela fixture.
- `f3base_esquema` registra versões e donos por tabela. Consultas de estrutura ficam na instalação, migração e reparo; uma escrita recusada por tabela/coluna ausente registra a falha, avisa e agenda reparo. Foram conferidas 70 tabelas e seus 70 donos, sem omissões, além de 11 verificações da falha e duas do reparo em novo processo.
- Zelador único com 63 tarefas classificadas e 51 condições nomeadas. Conferências de agenda e retomada saíram da página pública. Rotinas do Core e do WordPress ficam na passagem CLI enquanto há heartbeat recente; urgentes mantêm o despertar por visita. Após uma hora sem CLI, a reserva reativa rotinas e avisa; a CLI seguinte restabelece a proteção. As intenções urgentes e de rotina têm despertadores separados. Nove verificações WordPress cobrem filtro, urgência, reserva e recomposição de agenda. Seis verificações locais adicionais cobrem o despacho CLI e o registro nativo no diário; o lançador `wp-cli` real não foi executado nesta rodada.
- Perfil público com hooks em texto, configuração normalizada e catálogos sob demanda. Login carrega somente o necessário. O marcador do cache usa leituras públicas sem abrir o catálogo. Formulários deixam de carregar repositório, auditoria e configuração de tentativas apenas para imprimir campos; hash, antispam e telefone foram preservados em dez verificações específicas.
- A análise de HTML de ações de contato evita blocos sem candidatos. Sessenta e quatro comparações com o algoritmo anterior preservaram HTML em casos de menu, cabeçalho, WhatsApp, entidades codificadas, botões, classes próprias e destino inválido.
- Recuperação e geração do cache são memorizadas na requisição. Cache de schema tem chave por página/configuração/geração/grafo original, TTL de 300 s e 32 slots de até 256 KiB; escrita em arquivo protegido, sem SQL de escrita na página. Quatro verificações cobrem reutilização após limpeza do cache de memória e ausência de entrada na recuperação.
- `f3base/desempenho-ler` e `GET /f3base/v1/desempenho` mantêm autorização administrativa. Medem os sete hooks solicitados, funções anônimas e, adicionalmente, filtros de conteúdo/blocos, enqueue, menus e schema Yoast. Expõem tempo próprio/inclusivo, consultas sem valores literais, classes, OPcache, realpath cache e janela não instrumentada. Configuração escrita informa `efeito_ate` e `efeitos_imediatos`.
- Correção de bootstrap da atualização: a migração pode criar seu mapa de estrutura antes de depender do diário de execuções. A atualização direta 1.63.0 foi exercitada pelo executor, além da instalação limpa.

**Estado:** implementado, validado-localmente, validado-wordpress no escopo abaixo; aceite integral dos pedidos 354/360 pendente.

### Medições do ZIP final, após a retirada dos auxiliares

Site-Teste, todos os pacotes ativos, sondas internas sem cache, três amostras. A página real tem formulário, Yoast e WP Super Cache. A medição termina no footer; transporte e callbacks posteriores ficam fora dela.

| Métrica | Página | Login | Critério |
|---|---|---|---|
| Tempo próprio Core | 85,888 / 98,097 / 92,898 ms | 9,886 / 8,643 / 9,876 ms | Atende 100 / 50 ms nesta amostragem |
| Classes Core | 60 / 60 / 60 | 11 / 11 / 11 | Lista fechada; página atende máximo 60 |
| Consultas instrumentadas | 3 / 3 / 3 | 0 / 0 / 0 | Atende máximo 5 |
| Consulta de estrutura ou UPDATE | Nenhuma | Nenhuma | Atende |
| Descoberta Markdown | 0,048 / 0,048 / 0,047 ms | Não aplicável | Atende máximo 5 ms |
| Tempo não instrumentado | 332,850 / 318,969 / 319,170 ms | 242,182 / 244,873 / 260,801 ms | Página **não atende** 20 ms |

O tempo não instrumentado é a janela total do arquivo principal ao relatório menos o tempo medido; inclui WordPress, tema e acompanhantes. Não foi renomeado nem reduzido artificialmente para atribuir toda essa janela ao Core. As três consultas incluem callbacks de conteúdo agora medidos, além do marcador do cache. Nenhuma amostra abriu o catálogo completo.

**Comparação solicitada no pedido 354:** `system/probe`, bypass, três amostras por condição, menor valor. Um auxiliar temporário com autorização efêmera retirou somente Core e Pipedrive da lista de carregamento de cada requisição comparativa, sem alterar a opção de plugins ativos; o cabeçalho da condição foi conferido. O cron por visita foi impedido igualmente nas duas condições. O auxiliar foi removido.

| Caminho | Com Core + Pipedrive | Sem Core + Pipedrive | Diferença | Aceite de 100 ms |
|---|---:|---:|---:|---|
| `/` | 428,839 ms | 298,379 ms | **130,460 ms** | Pendente |
| `/wp-login.php` | 266,571 ms | 244,425 ms | **22,146 ms** | Atende |

As condições também diferem no HTML funcional produzido, como se espera ao retirar o Core. Trata-se de diferença observada, sujeita à carga da hospedagem; não é decomposição causal perfeita. Depois da limpeza, nova sonda normal teve mínimos de 412,460 ms na página, 252,937 ms no login e 598,480 ms em `/wp-json/`, todos HTTP 200. A bancada de 50 itens, sem Yoast/Pipedrive ativos, teve página aquecida de 4,725–5,213 ms próprios; essa bancada não substitui o ambiente da frota.

## 4. Instalação e prova de prontidão

1. Conferir o SHA-256 e instalar apenas `base-site-core-fator3-1.64.0-instalador.zip`, preservando o basename `base-site-core-fator3/base-site-core-fator3.php`. Guardar backup de arquivos e banco.
2. No Site-Teste foi usado `plugins/upload-base64`, com `zip_path` local temporário, `expected_slug: base-site-core-fator3`, `expected_sha256` da tabela final, `overwrite: true`, `activate: true` e chave de idempotência. O canal confirmou bytes, ativação e probes HTTP. Não houve publicação em Git nem distribuição aos outros sites.
3. Conferir `f3base/executar-pendentes`: primeiro `simular: true`, tarefas específicas e limite; executar com `simular: false` e a `revisao` devolvida. A migração foi confirmada pelo executor, ciclo `8bff040a-13b5-4d4e-b963-606bea8e277f`, e a leitura final mostrou `estado: concluida`, versão anterior 1.63.0. A geração llms também teve resultado de módulo confirmado. Outras pendências operacionais do site não foram executadas indiscriminadamente.
4. Ler a documentação instalada por `f3base/documentacao-ler`, por exemplo `{"arquivo":"docs/RELEASE-1.64.0.md","linha":1,"limite":200}`. A chamada pelo MCP retornou versão 1.64.0. Documentação completa foi percorrida no WordPress isolado pelo canal nativo: 167 documentos, 778 páginas, 2021 verificações; 189 abilities Core.
5. Conferir `f3base/desempenho-ler {"contexto":"pagina","amostras":3}` e repetir com `login`; interpretar os limites acima. A frota deve conferir sua execução real de `wp cron event run --due-now` a cada 15 minutos e o heartbeat do diário.

**Provas finais:** 589 arquivos PHP passaram no lint; ZIP contém 827 arquivos. Ciclos nativos com o ZIP final em WP 7.1.2 e 7.1.4, incluindo atualização pelo executor, repetição, preservação de dados e reativação. No ambiente isolado do Site-Teste, **2316 verificações** passaram, incluindo documentação, permissões/revogação, recuperação do Pipedrive em novo processo e regressões dos SDKs. HTTP e correio externos foram bloqueados nas fixtures. As comprovações de integração usaram respostas sintéticas; não equivalem a homologação de fornecedor.

A leitura da instalação compartilhada preservou revisões de configuração, verificou telas de e-mail/antispam/GA4 e confirmou os 827 arquivos byte a byte pelo manifesto ordenado SHA-256 `780af8ff9bc32d2722e3f7ffab20bebd08464fa24521fb72388a8896abdfcc0f`. Os nove plugins finais continuam ativos. Limpeza confirmada: 101 tabelas exclusivamente da fixture, diretório e registro temporários removidos; dois MU auxiliares, arquivo de trace e quatro ZIPs temporários removidos. Sondas normais depois da limpeza retornaram HTTP 200. Backups operacionais do canal permanecem sob gestão do próprio canal.

Evidências atuais estão em `evidence/1640/`; `site-clean-*.json` identifica a medição final sem auxiliares e `site-install-final.json` o ZIP final. Evidências anteriores com o mesmo número de versão registram candidatos internos e não substituem esses arquivos. Os dois arquivos `native-cycles-1640.json` registram o SHA final.

## 5. Banco e volta de versão

A versão não acrescenta tabela ou coluna SQL: reutiliza estruturas existentes e adiciona configuração, índices compactos, versão por tabela e estado de cron. `spam` é aditivo nas regras; marcas de atendimento utilizam o estado já existente. Migração completa padrões sem reescrever autoria/configuração deliberada. As tabelas comerciais e cinco conjuntos sintéticos de dados sobreviveram aos ciclos de atualização, repetição e desinstalação/reativação testados.

O mapa `f3base_esquema` é uma declaração de prontidão, não prova contínua do banco físico. Falha real de escrita aciona reparo e aviso; não há sondagem de estrutura em cada visita. O mapa Markdown remove de imediato conteúdo tornado inelegível, e geração posterior trata sua recomposição.

Para voltar, usar backup coerente de arquivos e banco após avaliar os dados gravados pela 1.64.0. Restaurar só arquivos não desfaz opções, atendimento spam, migração, filas, avisos nem efeitos externos. Os ciclos testados comprovam repetição e preservação, **não certificam downgrade sem restauração**. A indisponibilidade temporária do diário durante a atualização é tratada pelo bootstrap de migração. A desinstalação continua preservadora conforme o contrato existente.

## 6. Pendências de validação

| Pendência | Responsável / próxima prova |
|---|---|
| Diferença pública de 130,460 ms, acima dos 100 ms do pedido 354 | Agente Core e frota: continuar a análise de filtros/renderização e repetir comparação controlada |
| Janela não instrumentada acima de 20 ms | Core/frota: separar custos remanescentes com evidência; não atribuir WordPress/tema/acompanhantes integralmente ao Core |
| Aceite de 48/47 itens em korvena.com.br e fator3.com.br | Frota: medir pacote final nesses sites; nenhum deles foi modificado nesta rodada |
| Queda diária dos POST `/wp-cron.php`, rotina sem origem `http_cron`, próximo cron real | Frota: conferir logs de um dia e o diário CLI; o lançador real não foi testado aqui |
| Lead entregue em segundos aos canais reais | Homologação autorizada do fornecedor/frota; captura, supressão e filas foram exercitadas com dados sintéticos e rede comercial bloqueada |
| Próxima atualização automática e entrega dos e-mails nativos; falha robots real e recuperação | Frota: acompanhar eventos reais, sem provocar falhas em produção |
| Aceites anteriores 352, 353 e 356 | Permanecem os 7 dias em `/mvp`, o Lead real com `em`/`ph` e a próxima resposta IMAP transitória; esta release não inventa essas provas |

Não foi feita rodada completa de navegador visual nesta entrega; a preservação de HTML foi comparada e os testes de servidor/canal foram executados. Não há claim de homologação integral da frota, de APIs reais ou de entrega na caixa postal. A publicação/distribuição permanece com a frota sob sua autorização operacional.

## 7. Credenciais

Nenhuma credencial nova é necessária para instalar a versão. As configurações existentes foram preservadas; segredos não foram incluídos nos artefatos. Na tela de conexões, SMTP/IMAP continuam em `f3base_email_site` e segredo em `f3base_email_site_senha`; tokens OAuth, contas, ativos e concessões dos serviços Google/Meta/LinkedIn pertencem aos acompanhantes. Pipedrive mantém sua conexão/token e concessão do consumidor. O dono só deve preencher ou renovar campos realmente pendentes, por tela/ability autorizada, sem copiar tokens para o relatório. A nova política de e-mails WordPress e o prazo de robots são opções locais, não credenciais.

## 8. Identidade dos arquivos

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| [base-site-core-fator3-1.64.0-instalador.zip](base-site-core-fator3-1.64.0-instalador.zip) | 3020630 | e8c34d1cfbd347f6947e4e208fed92c11579c735f843d6c2e002c4fe29ce6588 |
| [base-site-core-fator3-1.64.0-fonte.zip](base-site-core-fator3-1.64.0-fonte.zip) | 6357649 | 651725d756e30c022d3460f17d03da7161fc833138e8659ec2869b9ce2fe3df5 |

Relatório externo canônico: **base-site-core-fator3-1.64.0-relatorio.md**. O fonte contém uma cópia identificada como anterior ao fechamento; nessa cópia, a identidade do próprio ZIP fica “a preencher no relatório externo após empacotamento”, evitando circularidade. O runtime no fonte é idêntico ao instalador final. Fonte e instalador têm uma única raiz e não contêm ZIPs aninhados, laboratórios, dumps ou dependências de desenvolvimento instaladas. Nenhum commit de publicação foi criado nesta rodada.
