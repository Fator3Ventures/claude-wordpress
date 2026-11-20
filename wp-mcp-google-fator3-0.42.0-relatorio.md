# Entrega — Fator3 MCP Google 0.42.0

Revisão 1 · 20/11/2026 · Correção e homologação · **com-pendencias**

## 1. De onde esta versão entra

Instalação limpa ou atualização direta da 0.41.0. A referência anterior tem instalador SHA-256 `47dea7ac080799dfd41cf7583c97a1959daefa0d50b0da490d8219c315bd4d76` e fonte `be55b406d34dca1fefa84b1393a6420e82621e82c67d0cacc1dfac506a670f28`. O retorno do Core 1.99.0, revisão 3, encerra a implementação do contrato do **Pedido MCP Google 59**. A revisão da entrega revelou uma falha adicional reproduzível no produtor Google quando um lote de avisos fica ocupado. Essa correção interna motivou a 0.42.0. A última lista de pedidos localizada identifica o número 60 como próximo disponível.

Foram lidos `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos na revisão 5 de 02/11/2026, a regra comum, o padrão Google, o pedido 59, a entrega 0.41.0 e o relatório e retorno do Core 1.99.0. O cabeçalho exige WordPress 7.1.4 e PHP 8.3. A bancada usou WordPress 7.1.4 e PHP 8.4.27. A validação no Site-Teste usou WordPress 7.1.5 e PHP 8.3.37.

## 2. Convivência e encaminhamentos

| Pacote | Versão e identidade de referência | Convivência comprovada |
|---|---|---|
| Fator3 Site Core | 1.99.0 · instalador `3509e2736dfdedd98c2fa142d99028eb629f112ba1c863138850c3f3ee5e7155` · fonte `9ab280444550f8c785b5f3c0cc69bb451b460e6a2da58cda569fbc91c0b2cc33` | Reproduzimos a retomada de avisos pelo Core oficial. O mesmo contrato atende à 0.41.0 e à 0.42.0. A operação pode atualizar o Core e, em seguida, o Google. Fechamentos que já aguardavam o Core são retomados. |
| Fator3 MCP | 0.53.0 em bancada · instalador `8403d4b5ce901bb3261d00823508b3c7f12507e2283a4d42c5d9822a7463c2a7` | Consultas de prontidão, permissões e leitura integral da documentação por HTTP autenticado. O Site-Teste atualizou o seu MCP para 0.54.0 por outra operação antes da instalação do Google. Reconfirmamos o contrato de instalação, a saúde do canal e as consultas usadas neste ensaio. |
| Meta, LinkedIn e Pipedrive | 0.31.0, 0.26.0 e 0.12.0 no Site-Teste | Inventário observado durante a homologação. A paginação corrigida pertence exclusivamente ao Google. |

O catálogo permanece com 311 habilidades, 123 de leitura, 188 de escrita e 46 definições de configuração. As versões dos contratos são configuração 4.0.0, catálogo 3.0.0, execução 2.0.0 e armazenamento 2.0.0. A correção lê as reservas e os recibos existentes. Não exige alteração de schema público, do MCP ou do Core.

O documento recebido do mantenedor foi preservado no fonte em `impacts/042/retorno-core-1.99.0-revisao-3.md`. A revisão 2 da proposta inicial continua em `impacts/041/`. O filtro `f3base_incidente_acesso_encerrar_v1` está implementado e testado no Core oficial. O impacto de desenvolvimento está **resolvido**. A adoção nos sites segue na seção 6.

## 3. Mudanças e evidências

**Falha reproduzida na 0.41.0.** O despachante consultava sempre os 100 avisos mais recentes de cada estado. Na bancada foram criados 102 avisos ordinários e 102 encerramentos que aguardavam o Core. Em cada fila havia 100 registros intermediários com reservas reais e dois registros livres nos extremos. Na base, o mais recente foi aceito. O mais antigo continuou pendente após três passagens, embora pudesse ser processado desde a primeira.

**Correção na 0.42.0.** O executor percorre até 100 registros por estado e guarda a sequência do próximo registro. Cada estado tem sua própria posição. Trabalhadores concorrentes respeitam as reservas por aviso e coordenam a mudança de página. O fim da fila libera a posição para a próxima varredura, incluindo as novas entradas e as que aguardavam uma reserva.

| Prova | Resultado observado |
|---|---|
| Atualização sobre a mesma fila | Os dois avisos livres mais antigos foram aceitos na segunda passagem. As reservas ativas foram respeitadas. Após liberar as reservas, o Core devolveu os 204 recibos e o produtor esvaziou as filas de cada registro. |
| Instalação limpa | O mesmo cenário produziu 204 recibos e zero tentativas de e-mail dentro da janela controlada do ensaio. |
| Retomada em outro processo | Um novo processo de PHP recuperou a posição persistida. Um aviso que chegou depois da primeira página aguardou o próximo ciclo e recebeu seu recibo. Ao final, os 102 avisos estavam aceitos e a posição havia sido removida. |
| Contrato do pedido 59 | Rodamos as 3 verificações de origem e as 7 de retenção da prova entregue pelo Core. Na fase final, ajustamos apenas a versão esperada do Google e repetimos as 20 verificações com os instaladores oficiais Core 1.99.0 e Google 0.42.0. Os encerramentos administrativos geraram zero mensagens. Uma abertura ordinária e sua recuperação genuína geraram uma tentativa de e-mail cada. |

Os testes usam WordPress, banco e reservas reais em loopback. O e-mail foi interceptado e as chamadas a fornecedores foram bloqueadas. Os arquivos `fila-*.json`, `cursor-*.json` e `contrato-*.json` em `evidence/042/` contêm os resultados. O cenário de contenção foi reproduzido em bancada. A sua ocorrência na frota não foi demonstrada.

## 4. Instalação e prova da troca

No Site-Teste, o instalador recebido em quatro partes foi confirmado pelo SHA-256 antes da troca. Mantivemos cópias privadas das duas tabelas do Google, totalizando 2.595 linhas, e das 28 opções do plugin. O instalador confirmou a cópia de código anterior. Foram conferidos dois inventários estáveis com MCP 0.54.0 antes de atualizar exclusivamente o Google. A versão antiga estava ativa e a 0.42.0 permaneceu ativa após a substituição. O diário terminou em `complete`. O arquivo temporário foi removido e a consulta de saúde terminou positiva, com zero recuperações pendentes. O arquivo principal e o arquivo PHP do despachante, relidos no site, coincidiram com os do ZIP.

| Verificação | Evidência e resultado |
|---|---|
| Prontidão | `google/status` confirmou `plugin_version=0.42.0`, 311 habilidades e zero incidentes abertos no Site-Teste. `google/integration-status` com `compact=true` confirmou `read_success=true` e `google/storage-status` confirmou `storage.ready=true`. Ver `campo.json`. |
| Google isolado | Na bancada limpa, o Google ativou sozinho. A consulta administrativa ao índice devolveu 26 documentos e o armazenamento estava pronto. As 37 verificações isoladas passaram. Ver `primeira-leitura.json` e `isolado.json`. |
| Documentação e autorização | Na bancada limpa e na atualizada, descobrimos a operação e o schema por MCP, lemos os 26 documentos, em 90 páginas, e verificamos seus hashes. Foram 124 verificações por instalação. O assinante recebeu 403 em `google/status` e `google/configure-alerts`, e o painel recusou seu acesso. No Site-Teste, lemos o guia 0.42.0 e o manual de avisos integralmente, em três páginas cada, com igualdade dos bytes e rejeição de caminho fora do índice. |
| Suíte e integridade | 1.389 testes, 16.549 asserções, zero falhas e zero omissões no executor compatível em PHP 8.4.27. Os 209 PHP do instalador passaram no lint. O ZIP tem 213 arquivos. Duas compilações geraram bytes idênticos. |

A bancada final contém os três plugins ativos, armazenamento pronto e 26 documentos legíveis. O inventário registrou zero jobs, incidentes, agendas, avisos técnicos e senhas de aplicação. As três bases de ensaio foram descartadas. Os roteiros estão em `tests/native/` e `reproducao/LEIA-ME.md`.

## 5. Banco, migração e recuperação

A atualização preserva os registros da 0.41.0 e dispensa migração de tabelas. Apenas durante uma varredura com mais de uma página são usadas as opções operacionais `f3_mcp_google_notice_cursor_pending` e `f3_mcp_google_notice_cursor_awaiting_access_core`. São posições por site e estado, sem cargas de eventos ou credenciais, e são removidas no fim da varredura. O destino, a geração e o recibo de cada aviso permanecem no registro original. Uma interrupção antes de salvar a posição permite rever a página. Os registros já aceitos deixam de ser elegíveis.

Para recuperação, preservar a cópia consistente do banco e da configuração. Conciliar reservas incertas com o transporte antes de repetir um envio. A troca de arquivos não desfaz mensagens já aceitas. Uma falha posterior de implementação exige nova versão.

## 6. O que permanece pendente

- **Frota.** Na consulta de 20/11, Pauta e Prática, Desenvolvimento de Softwares e Taberium ainda estavam em Google 0.40.0 e Core 1.98.0. Os seis registros do pedido 59 foram identificados pelo site e pelo instante original de abertura. Todos já constavam como recuperados antes da implantação desses novos pacotes. Depois de distribuir o conjunto, conferir motivos, referências e reservas da central nos episódios aplicáveis. O histórico continua distinguindo a recuperação anterior de um encerramento administrativo novo.
- **Titular da credencial de teste.** O Site-Teste está sem credencial Google. A autorização real no provedor e a entrega efetiva em caixa postal permanecem fora do aceite desta rodada. O teste de congestionamento usou registros sintéticos em bancada. A suíte completa rodou em PHP 8.4.27. No PHP 8.3.37 foram comprovados a atualização e os diagnósticos do Site-Teste.
- **Operação do CTO Office.** O acompanhamento anterior dos pedidos 57 e 58 tem janela até 22/11/2026 às 02h20 de Brasília. Esta rodada não fez uma nova medição de conversão real.

Para distribuir à frota, publicar segundo o procedimento do projeto e conferir o SHA-256 servido pelo raw antes de chamar `plugins/upload` com `expected_slug=wp-mcp-google-fator3` e `expected_sha256`. O endereço previsto é [o instalador 0.42.0 no repositório da frota](https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-google-fator3-0.42.0-instalador.zip). A instalação efetuada nesta rodada foi exclusiva de homologação.

## 7. Credenciais e configuração do dono

A correção opera no executor já configurado. Ela dispensa credencial nova e ajuste do intervalo. Em **Ferramentas → Fator3 MCP Google → Incidentes**, o responsável consulta o estado local. Na central do Core, `f3base/incidentes-tecnicos-ler` informa a referência, a condição do episódio e as fases de e-mail. Um recibo aceito pelo Core indica que a central reconheceu a transição. A comprovação de entrega de mensagem depende do transporte.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-google-fator3-0.42.0-instalador.zip](wp-mcp-google-fator3-0.42.0-instalador.zip) | 1011895 | `5de445dbbaf6afa1ec48cc97171a5d5c6ef2c502623a45f9fc930e713ec59aeb` |
| Fonte | [wp-mcp-google-fator3-0.42.0-fonte.zip](wp-mcp-google-fator3-0.42.0-fonte.zip) | 23313954 | `a466b7a25cf2204c2a4d32dbbd5d65331d2ac8bf5a133c02666dbc577e420ab7` |

Este é o relatório externo canônico. A cópia no fonte antecede o cálculo da identidade definitiva desse ZIP.
