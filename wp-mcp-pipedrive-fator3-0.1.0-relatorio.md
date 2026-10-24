# Entrega — Fator3 MCP Pipedrive 0.1.0

Revisão: 1 · Data/hora: 2026-10-24T01:30:00Z · Rodada: implementação inicial, análise de contratos e validação isolada.
Slug: `wp-mcp-pipedrive-fator3` · Versão/build: `0.1.0` / `20261024` · Commit: não aplicável, sem publicação em Git nesta rodada.
Status: **com-pendencias**. Pacote implementado e instalável; 98 verificações funcionais/integradas aprovadas no escopo descrito. A operação comercial está **bloqueada pelo contrato ausente no Core 1.50.0**. Não há homologação com o Core futuro ou com o fornecedor real.

**Relatório externo canônico**, concluído após o empacotamento do fonte.

## 1. De onde esta versão entra

Primeira versão do pacote, sem instalador Pipedrive anterior recebido ou versão intermediária necessária. A entrada comprovada é uma instalação limpa pelo ZIP final, usando `Plugin_Upgrader`, seguida de ativação e nova execução PHP no WordPress descartável. Reexecutar o instalador de schema preservou o recibo existente; isso não equivale a atualização nativa a partir de uma versão anterior.

Requisitos validados funcionalmente: **WordPress 7.1.3, PHP 8.3.36 de 64 bits, MySQL 8.0.41/InnoDB**, OpenSSL e mbstring no ambiente de prova. Esses são os mínimos declarados no cabeçalho; não há alegação de suporte a versões menores ou multisite. PHP 8.3.6 foi usado somente no lint local e na exportação de schemas. Build: Python 3.12.14, biblioteca padrão, sem Composer/npm ou download de dependências.

Foram lidos o pedido inicial, a aba Fator3 MCP Pipedrive, a aba Site Core, os relatórios recebidos e os contratos pertinentes nos fontes dos cinco acompanhantes. As instruções e o padrão centrais foram lidos integralmente: primeiro revisão 4 nas fontes avulsas; depois revisão **5, de 23/10/2026**, encontrada no fonte Meta 0.9.0 e aplicada como vigente. Os documentos centrais não foram alterados. As entradas com nome original, bytes e SHA-256 estão em `evidence/inputs.json`; os pedidos e normas usados estão em `inputs/`.

## 2. Convivência e encaminhamentos

As cinco versões abaixo foram ativadas juntas no WordPress isolado, em processo novo, com configuração vazia e saída HTTP/e-mail bloqueada. Os hashes identificam os instaladores recebidos para análise; a prova de convivência identificou as versões carregadas no servidor. Não foi feita uma auditoria byte a byte de todos os acompanhantes instalados, nem a homologação comercial de suas APIs.

| Pacote | Versão | SHA-256 do instalador recebido |
|---|---|---|
| `base-site-core-fator3` | 1.50.0 | `7021163d158b1a353e012823e14b611c17cb45d82125d3230784eb84f2b6b8ea` |
| `wp-mcp-fator3` | 0.29.1 | `1b627aec5c24dc88f52eaf6a0d34367437d7f9e7b599f9f07850567fd57610e6` |
| `wp-mcp-google-fator3` | 0.19.0 | `d15868915e3fdf886d7e883a82d9d302df7242808fc94d45bf3e1857234759d1` |
| `wp-mcp-meta-fator3` | 0.9.0 | `e26aede1591426e06b8a69b5ad405cf13cb70c28d41b607346188c9d21a15662` |
| `wp-mcp-linkedin-fator3` | 0.10.1 | `6182ea63bff6788f5d2637467e7ab29d58568e37283d6ece82d3e58ee41c13bc` |

O MCP 0.29.1 já oferece o registro genérico de provider e a política necessários. O teste utilizou seu executor e sua política originais, sem modificar esse plugin. Não foi identificado pedido técnico de mudança para MCP, Google, Meta ou LinkedIn no escopo analisado. Eles não são dependências da operação de domínio Pipedrive; somente o MCP é necessário para o canal remoto.

### Impacto emitido nesta rodada

| Destinatário | Classificação / situação | Pedido | Documento |
|---|---|---|---|
| `base-site-core-fator3` 1.50.0; alvo solicitado 1.51.0 | `acao-necessaria` / `demanda-aberta` | Pedidos core 294, C1–C8; confirmar assinatura e envelopes do contrato | [wp-mcp-pipedrive-fator3-0.1.0-impacto-base-site-core-fator3.md](wp-mcp-pipedrive-fator3-0.1.0-impacto-base-site-core-fator3.md), revisão 1, planejamento |

Esse impacto foi elaborado antes da implementação e mantém sua revisão: não houve mudança substantiva que exigisse outra edição. O status de atendimento fica neste relatório, conforme a revisão 5 da norma. O documento é entregue ao dono para encaminhamento; nenhum relatório foi enviado a outra pessoa por ferramenta.

### Tratamento do pedido recebido

Documento `Pedido — Fator3 MCP Pipedrive e contrato no Site Core.md`, de 23/10/2026, emissor Orquestrador/Geral: **Pedidos MCP Pipedrive 1** foi implementado na parte deste pacote. **Pedidos core 294 C1–C8** permanece com o mantenedor Core, sem afirmar seu atendimento. Não foi recebido instalador Core 1.51.0 nem confirmação da assinatura proposta. O contrato consumidor e a fixture estão documentados; podem precisar de ajuste após essa confirmação.

Ordem de implantação: Core com contrato confirmado primeiro; seleção do site-porta pelo dono/frota; Pipedrive nesse site; autorização explícita do provider e da conexão MCP; A1–A16 coordenados pela frota. A entrega não altera Core, Google, Meta, LinkedIn ou MCP.

## 3. Mudanças e evidência

| Pedido exato | Resultado implementado | Prova e limite |
|---|---|---|
| Pedidos MCP Pipedrive 1 — identidade e tela | Slug, basename, Text Domain, Update URI, descrição e menu Ferramentas → Fator3 MCP Pipedrive conforme pedido; nome começa por Fator3 | Instalação nativa e renderização PHP; aparência em navegador pendente |
| Pedidos MCP Pipedrive 1 — cinco operações | `status`, `api-ler`, `api-previa`, `api-aplicar`, `registro-ler`; schemas e REST `f3-pipedrive/v1` | Registro e execução com Abilities API/REST nativas; teste integrado do executor MCP |
| NORMA-02 — documentação instalada | `pipedrive/documentacao-ler`, sexta operação, índice e nove documentos paginados com SHA-256 e guarda de continuação | Nove leituras integrais em 18 páginas pelo executor MCP; hashes iguais aos arquivos instalados; zero HTTP |
| Pedidos MCP Pipedrive 1 — lista fechada | Métodos/caminhos/query/corpos permitidos, IDs numéricos ou UUID conforme recurso, limite de corpo 64 KiB; recusa URLs absolutas, mailbox, merge, ids em massa e parâmetros desconhecidos | Fixtures em WordPress real; nenhum executor arbitrário ou HTTP próprio |
| Pedidos MCP Pipedrive 1 — duas fases | Prévia cifrada de 15 minutos; consulta do registro atual; classe, reversão, custo e novo corpo; vínculo a usuário/site/conta/revisão | Expiração, alteração de conta/revisão/estado e acesso por outro administrador testados |
| Pedidos MCP Pipedrive 1 — aplicação única | Aquisição transacional e auditoria durável antes do despacho; recibo cifrado relido; repetição devolve recibo sem nova escrita | Dois processos PHP concorrentes, reentrada, timeout e falha injetada de auditoria testados; resultado incerto nunca libera reenvio |
| Pedidos MCP Pipedrive 1 — estrutura | Frase literal com data/resumo/digest; comparação dos IDs de opções; exclusão exige lista exata `remover_opcoes`, retirada antes do envio | Ausência/frase divergente/omissão de opção bloqueadas; confirmação e retirada explícita testadas com fixture |
| Pedidos MCP Pipedrive 1 — auditoria | UTC, caminho/IDs, classe, chaves, status, saldo; estrutura anterior e nomes/opções autorizados; sem valores pessoais no diário | Recibo separado e cifrado; leitura paginada; retenção padrão 180 dias sob demanda |
| Pedidos MCP Pipedrive 1 — permissões/ciclo de vida | `manage_options` no dispatcher, abilities, REST e painel; política da conexão MCP; sem cron, fila ou webhook; uninstall preserva dados | Seis operações recusam usuário sem permissão; perfil MCP de leitura recusa prévia; ausência de cron e preservação de recibo testadas |
| Pedidos core 294 C1–C8 — consumo do contrato | Somente objeto cliente público proposto; status antes de cada chamada e revisão esperada no contexto; propagação segura de códigos | Cliente simulado, ausência real no Core 1.50.0; guardas e transporte do Core futuro pendentes |

As listas foram comparadas com a documentação oficial de Leads, LeadLabels, DealFields, Notes e Filters, referenciada em `docs/CONTRACTS.md`. Etiquetas usam UUID e são consultadas pela coleção; campos existentes são procurados em catálogo paginado, até 20 páginas de 500 itens. Mantida a API v1 de campos pedida; não foi presumida equivalência operacional da API v2 na conta. As exclusões trazem orientação de reversão condicionada à lixeira e às capacidades reais da conta, sem garantia de recuperação.

### Critérios A1–A16

Os estados abaixo distinguem implementação, prova própria e o aceite integrado exigido pelo pedido. **Nenhum item foi marcado `homologado-fornecedor`.** Fixtures não substituem a prova no Core futuro/conta real.

| ID | Estado e evidência desta rodada | Aceite restante / responsável |
|---|---|---|
| A1 | `implementado`, `validado-wordpress`: cliente simulado não autorizado retorna código; zero despacho | `bloqueado`: option/registro/autorização reais no Core; mantenedor Core + frota |
| A2 | `implementado`, `validado-wordpress`: status local do contrato proposto e orçamento; Core 1.50.0 degrada com `core_indisponivel` | `bloqueado`: conferir conta esperada e teto 3.000 no Core compatível; frota |
| A3 | `implementado`, `validado-wordpress`: consulta de catálogo pelo cliente simulado e saldo no envelope | `bloqueado`: GET real e persistência de saldo pelo Core; Core + frota |
| A4 | `implementado`, `validado-wordpress`: URLs absolutas, mailbox e outros caminhos vedados recusados antes do cliente | Repetir na homologação integrada; frota |
| A5 | `implementado`, `validado-wordpress`: prévia/patch/estado simulado/recibo/diário sem valor pessoal | `bloqueado`: lead de homologação e campo Perfil (ICP) 152 na conta real; frota |
| A6 | `implementado`, `validado-wordpress`: recibo idêntico, uma linha e uma escrita; dois processos só adquirem uma vez | `bloqueado`: repetir após mutação real com Core compatível; frota |
| A7 | `implementado`, `validado-wordpress`: prévia vencida retorna `previa_expirada` | Repetir no aceite integrado; frota |
| A8 | `implementado`, `validado-wordpress`: frase ausente/divergente bloqueia e frase exata permite no cliente simulado | `bloqueado`: criar e excluir etiqueta de homologação real; frota |
| A9 | `implementado`, `validado-wordpress`: opção omitida recusada; lista explícita exata validada e flag não enviada | `bloqueado`: catálogo real/contrato Core confirmado; frota |
| A10 | `implementado`, `validado-wordpress`: ids em query/corpo recusados no pacote | `bloqueado`: recusa pelo cliente direto Core C2; mantenedor Core |
| A11 | `implementado`, `validado-wordpress`: fixture de teto 40 recusa terceira leitura | `bloqueado`: reserva real e independência de entregas; Core + frota |
| A12 | `implementado`, `validado-wordpress`: código `saldo_conta_baixo` preservado pela fixture | `bloqueado`: saldo oficial e segregação dos consumidores no Core; Core + frota |
| A13 | `implementado`, `validado-wordpress`: código de recuperação da fixture propagado sem mutação | `bloqueado`: preparar/retomar na barreira real; Core + frota |
| A14 | `validado-wordpress` no escopo local: acompanhantes coexistem; hospedeiro mantém oito plugins ativos e saúde normal após limpeza | `pendente`: formulário, entrega de lead e `f3base/pipedrive-verificar` reais com Core novo e pacote desativado; frota |
| A15 | `implementado`, `validado-wordpress`: marcadores sintéticos redigidos/omitidos em exceções, erros e executor; runtime sem acesso ao token/HTTP | `pendente`: sanitização do cliente real em todos os canais; Core + frota |
| A16 | `nao-aplicavel` para registros CRM: nenhum lead/pessoa/organização/etiqueta real criado, nenhum ID remoto a excluir; `validado-wordpress` para limpeza do laboratório | Na homologação futura, excluir todos os registros criados e entregar IDs; frota |

## 4. Instalação e prova da troca

O instalador final foi instalado por `Plugin_Upgrader` num WordPress isolado; a ativação e os testes rodaram em processos novos. **Todos os 20 arquivos instalados têm SHA-256 igual ao fonte e ao ZIP entregue.** O build reproduziu o instalador byte a byte. Evidências estruturais e lint: 29 verificações, incluindo 16 arquivos PHP do runtime/build/testes; não estão somadas às 98 verificações funcionais.

| Prova | Resultado | Evidência no fonte |
|---|---|---|
| Instalação limpa pelo ZIP | Instalado, ativo, schema 1, stderr vazio | `evidence/qa-install.json`; requisição `c5c40603152141692b198132` |
| Bateria WordPress | 74 aprovadas, zero falhas, 31 chamadas de fixture/6 escritas de fixture, zero HTTP real | `evidence/qa-run.json`; requisição `b28bdab84aa9a53f88571646` |
| Integração com os cinco acompanhantes | 24 aprovadas, zero falhas, seis operações descobertas, documentação integral e permissão verificada | `evidence/qa-integrate.json` e `qa-integrated.json`; requisição `61adfc7c6a3fd3371423332a` |
| Lint/build/identidade | 29 verificações aprovadas; schemas gerados iguais aos instalados | `evidence/static-build.json`; `build/verify.py` |
| Limpeza e hospedeiro | 87 tabelas exclusivas do laboratório e diretório removidos; controller/bundle removidos; ability temporária ausente; saúde normal | `evidence/environment-cleanup.json` e `cleanup-independent-read.json` (zero tabelas e diretório ausente); limpeza `8ad0e148a8f36e6eb1808645` |

Documentação instalada: `docs/README.md`; chamada `pipedrive/documentacao-ler` com `{}` retorna o índice. Usar `documento`, `offset`, `limite_bytes` e `sha256_esperado` conforme o schema retornado. A página seguinte exige o hash anterior. A leitura integral e reconstituição dos nove documentos foi comprovada pelo **executor original MCP executado dentro do WordPress**, não por uma sessão HTTP MCP externa própria deste provider. A chamada `pipedrive/status` com `{}` foi executada e devolveu `core_indisponivel` de forma segura com o Core atual.

Para a frota: conferir o SHA-256 da seção 8; publicar instalador e relatório no destino autorizado; conferir os bytes efetivamente servidos; consultar o schema real de `plugins/upload`; usar `expected_slug=wp-mcp-pipedrive-fator3` e o `expected_sha256` da seção 8. URL raw prevista, **não publicada nem validada nesta rodada**: `https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-pipedrive-fator3-0.1.0-instalador.zip`. O teste isolado usou os bytes locais e não equivale ao fluxo de distribuição raw pela frota.

Estado final: Pipedrive **não foi instalado no WordPress compartilhado** nem autorizado na conta real. O hospedeiro continua com Core 1.50.0, MCP 0.29.1, Google 0.19.0, Meta 0.9.0, LinkedIn 0.10.1, DreamHost Panel Login 1.0.0, WP Super Cache 3.1.4 e Yoast 28.7, todos ativos, iguais ao inventário inicial. As sondas internas de `/` e `/wp-json/` retornaram 200 antes/depois da remoção do controlador; isso não comprova acesso externo. O diagnóstico `system/health` retornou `healthy=true` e todas as verificações locais verdadeiras. Permanecem somente backups e auditoria normais das operações de arquivo do MCP; nenhum controlador de QA ativo, configuração do laboratório ou tabela de teste permanece.

Tentativas preliminares ajustaram o bootstrap do laboratório e dois problemas do harness, descritos em `tests/README.md`; não são provas aprovadas nem foram adicionadas à contagem final. A tentativa local de banco não pôde iniciar o socket no executor, por isso as provas funcionais foram realizadas no laboratório privado do servidor autorizado. Não se alegou execução local de MySQL inexistente.

## 5. Banco e volta de versão

Ativação cria `{prefix}f3_pipedrive_operations` e `{prefix}f3_pipedrive_journal`, ambas InnoDB, e `f3_pipedrive_schema=1`. Não migra tabelas/options de outro plugin. O recibo privado e o corpo da prévia usam AES-256-GCM com chave derivada dos salts WordPress e do blog. O diário contém metadados e estrutura, sem valores pessoais; recibos privados podem conter a resposta do fornecedor, cifrada, para repetição exata.

Prévia vale 900 segundos; auditoria/recibo têm retenção padrão de 180 dias. Limpeza é acionada por escrita, sem cron: sem novas operações, dados vencidos podem permanecer fisicamente. Operações `running` são preservadas para reconciliação mesmo além desse prazo; seu payload expirado é esvaziado na limpeza. Consultar status/documentação/registro não limpa nem repara banco. Desativar/desinstalar preserva tabelas e não chama fornecedor.

Aquisição `ready → running` e inserção única de auditoria são confirmadas antes do despacho. Resultado e diário são concluídos em outra transação e relidos. Falha incerta bloqueia nova execução daquela prévia; não há reset automático, fila ou retry de escrita. A revisão da conta também precisa ser revalidada pelo Core imediatamente antes do transporte, conforme o impacto emitido.

Antes de implantação, preservar banco e salts. Voltar arquivos ou desativar o pacote não desfaz exclusões, alterações externas, consumo de orçamento ou efeitos de outro plugin. Não existe versão anterior Pipedrive recebida para rollback de código; desativação é a saída conservadora, mantendo os dados para diagnóstico. Remoção definitiva de tabelas exige decisão administrativa separada.

## 6. O que permanece pendente

1. **Mantenedor Core:** implementar C1–C8 e confirmar o contrato proposto, incluindo autorização por provider, revisão esperada, reserva atômica, saldo oficial, recuperação, sanitização e evidência de despacho. O alvo pedido é Core 1.51.0/contrato administrativo 8.16.0; esses artefatos não foram recebidos nem produzidos por este agente.
2. **Mantenedor Pipedrive + Core:** comparar o contrato efetivo com `docs/CONTRACTS.md`, ajustar se necessário e repetir os testes afetados. O nome do contrato, isoladamente, não comprova compatibilidade dos envelopes.
3. **Frota/dono:** escolher site-porta, publicar/verificar o raw, configurar provider e política MCP, testar A1–A16 no Site-Teste com o Core compatível, conferir conta e limpar registros reais de teste. Até lá, uso comercial permanece bloqueado.
4. **Frota:** prova HTTP MCP externa do provider, instalação por `plugins/upload` com hash/slug, inspeção visual em navegador e regressão do formulário/entrega de lead. A renderização PHP e a convivência de plugins não substituem essas provas.
5. **Não aplicável nesta primeira versão:** atualização nativa a partir de Pipedrive anterior. **Não comprovado:** runtime menor que os mínimos declarados, MariaDB específico, multisite ou APIs não incluídas na lista. Multisite está explicitamente recusado.

As pendências não foram convertidas em sucesso por testes sintéticos. O pacote serve para revisão, instalação controlada e validação do consumidor; a integração comercial exige a coordenação acima.

## 7. Credenciais e configuração do dono

O token de API existente continua exclusivamente no Site Core, campo `f3base_pipedrive_token`, pela tela/configuração oficial do Core e sua verificação. O Pipedrive não oferece campo de token, não lê a option privada, não monta header e não faz HTTP. Nenhum segredo precisa ser fornecido no chat ou está incluído nos arquivos.

Após o Core compatível: consultar os schemas efetivos de configuração, habilitar `f3base_pipedrive_operacao.ativo` e autorizar somente `wp-mcp-pipedrive-fator3` em `consumidores` no site-porta. Conferir conta/domínio/usuário esperados no status e orçamento `operacao`, saldo e instante. O alvo comercial citado no pedido não é codificado no runtime. Conceder explicitamente as operações na conexão MCP; registro de provider não concede acesso. Todas continuam exigindo `manage_options` no servidor.

## 8. Identidade dos arquivos

| Artefato | Nome final e link | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-pipedrive-fator3-0.1.0-instalador.zip](wp-mcp-pipedrive-fator3-0.1.0-instalador.zip) | 42095 | `3366d83ca8908e407a0736812d30b8fa1506a8c1458a28cfb47eda6fd8f3c54f` |
| Fonte | [wp-mcp-pipedrive-fator3-0.1.0-fonte.zip](wp-mcp-pipedrive-fator3-0.1.0-fonte.zip) | 159941 | `bb06315b60a5b0a36c0458d9dcb000505e52b5f444278a3effb26414186a3f2c` |

Relatório canônico: `wp-mcp-pipedrive-fator3-0.1.0-relatorio.md`. A cópia interna é anterior ao fechamento do fonte e deixa o tamanho/hash do próprio ZIP para este relatório externo, evitando circularidade. Runtime e evidências funcionais são iguais nas duas cópias. Nenhum ZIP contém outro ZIP; somente o instalador é instalável. O fonte inclui build, testes, documentação, evidências sanitizadas e os pedidos, sem configuração privada, banco ou dependências de laboratório.

Complemento: `wp-mcp-pipedrive-fator3-0.1.0-impacto-base-site-core-fator3.md`, revisão 1, pedido técnico ainda aberto. Não foram gerados impactos de simples aviso de versão ou de encerramento.
