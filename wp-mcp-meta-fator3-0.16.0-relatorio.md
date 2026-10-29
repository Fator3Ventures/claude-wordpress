# Entrega — Fator3 MCP Meta 0.16.0

29/10/2026 — referência America/Sao_Paulo. Base direta: 0.15.0. Versão corrente entregue e instalada no Site-Teste: **0.16.0**.

**Natureza desta versão:** atualização da documentação operacional distribuída no plugin e validação coordenada com Core 1.61.1. O novo guia resolve instruções instaladas que ainda tratavam o consumidor Core como pendente. Não há nova implementação de coleta, mudança de contratos ou redução de retenção. A solicitação expressa desta rodada é gerar uma nova versão; o incremento minor identifica o novo conteúdo instalado. O número não representa nova funcionalidade de coleta.

## 1. Bases aceitas

Foram examinados o código e a documentação da base Meta 0.15.0 e os quatro artefatos Core 1.61.1 recebidos. A base Meta foi recuperada pela identidade dos artefatos e conferida por SHA-256. O impacto Core revisão 2 trata dos pedidos Core 340/341 e Meta 23/24, informa o consumidor implementado e solicita validação coordenada e aceite real, sem exigir mudança de runtime Meta. Não há outro pedido funcional novo demonstrado pelas entradas desta rodada.

As instruções comuns recebidas são revisão 4. A orientação explícita do usuário — impactos apresentam consequências/pedidos, não respostas ou encerramentos — e a revisão 5 preservada na base prevalecem nesse ponto. Não foram editadas regras centrais, documentos recebidos ou código de outro pacote. A ampliação anterior de retenção foi preservada. Fontes e decisões históricas permanecem identificadas no fonte.

| Artefato de entrada | Bytes | SHA-256 |
| --- | ---: | --- |
| base-site-core-fator3-1.61.1-fonte.zip | 5723729 | `94617ef804d05bad17c4f68d8e62300b38b0e0145856f5925b6a4aefe1fcd08e` |
| base-site-core-fator3-1.61.1-impacto-wp-mcp-meta-fator3.md | 2613 | `0a0e174066daa4a137b4279fe5907666673799dbf4fdb592442ef765b0ab7c2c` |
| base-site-core-fator3-1.61.1-instalador.zip | 2933589 | `9cfbab0b667c877c3c14b9d6704c827665d20d7b34ff4c9b9d915d6b3c9bd6d3` |
| base-site-core-fator3-1.61.1-relatorio.md | 17700 | `e6189a52f4cfec506f58cf058ee0c2f474583349cd530221d47dcc88e0772584` |
| wp-mcp-meta-fator3-0.15.0-instalador.zip | 305286 | `521e8f83a8c6fad12497e7c9f40ec6cf8cb129060c6a56e89955257ca22f81f3` |
| wp-mcp-meta-fator3-0.15.0-fonte.zip | 3047277 | `9b4caec4772004b11e0789e0f3cb5de954409d5798d198c8f3d403f5c03c97c2` |
| wp-mcp-meta-fator3-0.15.0-relatorio.md | 23024 | `00841fcf887bb9c73edd4ca3cdcac5572311e245b8c58a43c332ce312b21df16` |

## 2. Convivência e encaminhamentos

| Pacote | Versão examinada no Site-Teste | Resultado pertinente |
| --- | --- | --- |
| Fator3 Site Core | 1.61.1 | Consumidor público de monitoramento registrado; 800 arquivos conferidos contra o fonte recebido; testes próprios de monitoramento e performance aprovados. |
| Fator3 MCP | 0.37.0 | Autorização, idempotência, saída segura, instalação e leitura documental exercitadas. |
| Fator3 MCP Google | 0.23.0 | Convivência/ativação e integridade; APIs Google não homologadas nesta rodada. |
| Fator3 MCP LinkedIn | 0.13.0 | Capabilities chamada com sucesso na bancada; arquivos preservados. Nenhum impacto identificado nesta fronteira. |
| Fator3 MCP Pipedrive | 0.4.0 | Provider registrado; operação não autorizada recusada sem chamada externa. Arquivos preservados. |
| Fator3 MCP Meta | 0.15.0 → 0.16.0 | Único pacote substituído no site compartilhado. |

O contrato adicional continua `meta-ads-monitoring/1.0.0`, independente de `meta-ads-reader/1.0.0`. Também permanece `instagram-message-erasure/1.0.0`. Configuração Core, concessão Meta e autorização de notificações continuam separadas. A revisão da configuração do consumidor invalida a concessão anterior; reautorizar exige ato explícito. Com MCP ativo, o job também precisa da autorização efetiva de sua identidade para a leitura pública `meta/health`.

**Impacto recebido:** a prova própria reproduziu a integração declarada pelo Core. O aceite com contas reais continua com o dono/frota; esta entrega não o encerra. **Nenhum novo relatório de impacto foi emitido**, pois não surgiu alteração de contrato, regressão ou novo pedido de implementação para outro pacote. Resultados da validação estão neste relatório, sem gerar um arquivo de resposta ao Core. Nenhuma mensagem foi enviada a outros responsáveis.

## 3. Mudanças por pedido e evidência

### Core 340/341 e Meta 23/24

Novo documento instalado `CORE-MONITORING.md`: configuração pública e simulação no Core; conexão/conta/datasets/relatórios explícitos; leitura e concessão com revisão; coleta separada da autorização; paginação; permissões de autoria; contagens e EMQ datada; prova adicional de atividade; configuração do canal; recibos e deduplicação; diagnóstico e roteiro de aceite real.

README, configuração, administração, contratos, guia de agentes, diagnóstico, migração e changelog apontam para o fluxo atual. Foi corrigida a indicação de que o Core ainda precisava implementar o consumidor. A documentação registra a diferença entre `account_id` da coleta de dataset e a conta de anúncios no SDK, evitando configurar a concessão com o identificador errado. Também explica que uma concessão SDK válida não substitui a política MCP da chamada pública feita pelo job.

O código Core foi revisado na fronteira de autorização, leitura local, ocultação de autoria, prova do incidente, canal e reserva de recibo. Os testes usaram as classes reais dos dois plugins, sem substituir o leitor SDK. O Core preservou valores antigo/novo, ocultou autoria sem capacidade pessoal, separou contagens e EMQ, recusou falso zero, distinguiu pixels navegador/CAPI e bloqueou leitura/aviso após revogação. Houve exatamente uma tentativa interceptada de aviso para um incidente elegível e nenhuma duplicação.

### Comparação com Meta 0.15.0

`evidence/runtime-diff.json` registra todas as diferenças do instalador: documentos, documentação compilada, cabeçalho/constante de versão, readme e manifesto. As funções de negócio PHP e os arquivos JavaScript/CSS são idênticos à base. Cabeçalho e Config diferem apenas pela versão. Os 47 schemas de entrada e os schemas de saída/privacidade são idênticos byte a byte. Não há tabela, hook funcional, rota, concessão, permissão, fornecedor ou fluxo de coleta novo.

A retenção ilimitada de atividades, contagens, EMQ, histórico e demais funcionalidades já ampliadas continua igual. A atualização não apaga nem reexpira dados; escolhas finitas explícitas que já eram respeitadas continuam respeitadas. Tokens e cursores mantêm seus prazos de segurança. Exclusão explícita e controles de privacidade permanecem vigentes. Nenhum anúncio, contato real ou ativo remoto foi alterado.

## 4. Instalação, testes e prontidão

### Prova própria nesta rodada

| Prova | Ambiente / escopo | Resultado |
| --- | --- | --- |
| Build repetido e lint | Python 3.12.14; PHP CLI 8.3.6; lock oficial Ubuntu em tools/build-runtime0160.json | 32 PHP sem erro; ZIP determinístico e hashes iguais entre builds. |
| Instalação limpa final | WordPress 7.1.4 / PHP 8.3.36 / MySQL 8.0.41; apenas Meta | 35/35 asserções, incluindo manifestos, documentos, REST e recusa de subscriber. |
| Coletor, acervo e SDK | Mesmo laboratório limpo, Graph sintética | 36/36: paginação, dados parciais/erros, zero, vínculo conta/dataset, EMQ, concessão/revogação, revisão e retenção cifrada. |
| Monitoramento Core 340/341 | Todos os acompanhantes reais; Graph e transporte de aviso interceptados | 19/19 asserções, 17 nomes distintos; três coletas compartilham um nome. 14 chamadas Graph sintéticas, uma tentativa de e-mail interceptada, zero chamadas reais ao fornecedor. |
| Performance Core/Meta | SDK real, histórico e contatos sintéticos isolados | 46/46: 30 dias, moedas, paginação, associação, revisão, concessão, ausência de HTTP/e-mail. |
| Transporte e convivência | MCP 0.37.0 e cinco acompanhantes | 27/27: permissões, revogação sem fallback, idempotência, saída segura, LinkedIn, Pipedrive e hashes dos acompanhantes. |
| Atualização direta 0.15.0 → 0.16.0 | Bancada com dados semeados na base | 12/12: 13 registros e quatro linhas históricas preservados byte a byte; concessão de monitoramento continua válida; agenda, retenção, mensagens e Story preservados. |
| Mínimos próprios | WordPress 6.4 / PHP 8.1.2-1ubuntu2.28 / MySQL 8.0.41; instalação refeita do zero no PHP exato | 35/35; sem Abilities API, REST disponível e autorização conferida. |
| Site-Teste após troca | WordPress 7.1.4 / PHP 8.3.36 | Health `ok`, oito controles selftest `ok`, 47 operações 0.16.0; conteúdo integral dos 27 documentos igual ao instalador. Guia lido também em duas páginas e hash final conferido. |

As sete suítes funcionais totalizam **210 asserções finais aprovadas**; os oito controles do selftest compartilhado e as verificações de build/documentação são adicionais. Os testes Core foram adaptados do fonte recebido, com hashes de origem e mudanças de bootstrap/versão/saída registradas em `tests/core0160-test-provenance.json`. Os testes Core/convivência rodaram antes do último acréscimo textual sobre política MCP; a lógica comparada é idêntica ao pacote final. Instalação limpa, coletor, atualização, mínimos e verificação documental usaram o conteúdo final.

### Falhas de preparação e repetições

O primeiro teste de monitoramento parou em `leitura_recusada`: a preparação do laboratório omitira a identidade técnica MCP criada pelo instalador de testes original do Core. Essa identidade foi adicionada somente à bancada e a suíte passou. Nenhuma permissão foi ampliada no site compartilhado.

O primeiro teste do coletor foi executado depois do teste Core e encontrou o incidente de zero sintético deixado por ele. Sua asserção global de ausência de incidentes pressupunha uma bancada limpa. A suíte foi repetida em uma instalação nova, com 36/36. Não foi removido nenhum controle para obter aprovação e não se alterou a lógica do plugin. Ambos os resultados intermediários permanecem nas evidências, com instrução de ordem/isolamento para reprodução.

### Estado final do Site-Teste

`https://fator3-teste-mcp-1.dreamhosters.com/`: Meta **0.16.0 ativo**. Instalação pública com slug e SHA-256 esperados, pré-imagem preservada e sondagens HTTP em requisições PHP novas aprovadas antes/depois. A árvore instalada corresponde aos 63 arquivos do instalador final, SHA-256 da árvore `f75a432ad8cdc0dcbb56cf28733732e66e0d21cbc660caf63af16dba16cc81c0`.

Os dois registros Meta existentes, histórico vazio e sete opções observadas permaneceram com os mesmos hashes antes/depois; auditoria técnica é excluída dessa comparação. A configuração de monitoramento Core permaneceu idêntica. As cinco árvores de acompanhantes permaneceram byte a byte iguais e ativas. O site compartilhado tem zero conexões Meta e zero agendas; o consumidor Core 1.61.1 está registrado como `consumer_not_ready`, sem concessão, como antes. Saúde local não equivale a prontidão de conta real.

Os quatro laboratórios tiveram tabelas, diretórios e manifestos removidos: os recibos registram zero tabelas restantes. Os dois arquivos MU temporários foram removidos; a descoberta final retorna só as 47 operações Meta, sem QA. Auditorias/backups normais do MCP foram preservados. Nenhum banco compartilhado foi apagado, e nenhum pacote alheio foi reinstalado no ambiente compartilhado.

## 5. Banco, retenção e reversão

Mantidos schema de registros 2 e schema histórico 1. Nenhuma migração nova ou destrutiva. Atualizar o instalador sobre o mesmo basename `wp-mcp-meta-fator3/wp-mcp-meta-fator3.php`, preservando banco, salts, chaves e backups. O ZIP fonte não é instalável.

Rollback para 0.15.0 consiste em restaurar os arquivos do instalador-base com banco e chaves preservados; ele já compreende os relatórios e concessões de monitoramento. Não desfaz configuração, renovação/revogação de credenciais ou avisos já enviados. Não apagar recibos para forçar repetição. Não voltar a versões anteriores à 0.12.0 com mensagens habilitadas. Desinstalação continua conservando dados conforme a política existente.

## 6. Pendências e responsáveis

- **Dono/frota:** aceite com ativos reais em korvena/ctooffice, como pede o impacto Core recebido: identidade/permissões, conta/dataset, janela remota efetiva, coleta de dia completo, alterações, contagens, EMQ e próximo incidente natural. Não forçar zero em campanhas. Esta rodada não operou esses sites.
- **Operador autorizado:** selecionar configuração e concessão e habilitar canal apenas no escopo aprovado. Conferir a identidade usada pelo job e reautorizar a concessão depois de mudar a configuração. Não houve envio real de e-mail ou Slack; entrega do canal permanece não homologada nesta rodada.
- **Dono/frota:** decidir distribuição/publicação dos artefatos. Nenhum push, publicação de repositório ou envio a terceiros foi executado.
- **Limites da prova:** APIs e credenciais reais não foram usadas; App Review e disponibilidade por versão/ativo não foram homologadas. Cron foi exercitado pela chamada do job, sem aguardar o relógio. Interface visual não foi reavaliada em navegador, pois JS/CSS e fluxo de tela não mudaram; documentação instalada foi conferida pelo MCP. Não se afirma teste de todas as funcionalidades de outros plugins.

Não ficou falha funcional reproduzível pendente nas fronteiras testadas. A prova sintética não encerra o aceite remoto solicitado pelo Core.

## 7. Credenciais e configuração

Foram usados somente valores sintéticos no banco isolado. Nenhum token real, segredo de aplicativo, cookie, senha de banco, conteúdo pessoal ou dump foi incluído na entrega. Credenciais do WordPress usadas internamente pelo controlador não são retornadas nem empacotadas. Testes de contatos ficaram apenas nas tabelas isoladas. Nenhuma concessão, ativo, agenda ou aviso foi habilitado automaticamente no site compartilhado.

## 8. Artefatos e identidade final

Instalador final: `wp-mcp-meta-fator3-0.16.0-instalador.zip` — **315170 bytes**, SHA-256 **`a49f3e8ae9e60814ab55cf1bd4b3277e859a477347d02f664353c1268fda0b6b`**. Único ZIP instalável; raiz `wp-mcp-meta-fator3/`.

Fonte: `wp-mcp-meta-fator3-0.16.0-fonte.zip` — raiz única com código, runtime exato do instalador, build, testes, instruções, evidências sanitizadas e relatório. Nenhum ZIP aninhado. O fonte é fechado depois desta cópia interna do relatório; tamanho e SHA-256 finais são acrescentados somente ao relatório externo, evitando circularidade.

Relatório externo: `wp-mcp-meta-fator3-0.16.0-relatorio.md`.

**Fechamento final do fonte:** `wp-mcp-meta-fator3-0.16.0-fonte.zip` — **3268614 bytes**, SHA-256 **`826875296447fe946cda3944dd481b199f3927a48cdb92277435785dc0386ab6`**. A cópia dentro do fonte foi preservada como anterior ao fechamento. Fonte e instalador foram conferidos; o runtime do fonte corresponde exatamente aos bytes instaláveis.
