# Entrega — Fator3 MCP Pipedrive 0.8.0

Revisão 1 · 2026-11-06T13:54:21-03:00 · Rodada: implementação do Pedido MCP Pipedrive 11.  
Slug: `wp-mcp-pipedrive-fator3` · Build: SHA-256 do instalador na seção 8.  
Status: **com-pendencias** — implementada e ativa no Site-Teste, aprovada no escopo sintético executado; falta o aceite comercial do Pedido 11 em korvena.com.br.

## 1. De onde esta versão entra

Instalação limpa ou atualização direta **0.7.0 → 0.8.0**. A base é o instalador próprio publicado anteriormente, 118.218 bytes, SHA-256 `8f58b26c8408c02604c16bcfd30fcb92e3bbae308ebc107defad21555e5b5779`. Antes da troca, todos os 35 arquivos instalados no Site-Teste correspondiam à base. O fonte-base e os relatórios recebidos estão identificados em `inputs/README.md`; os ZIPs de entrada não são duplicados no fonte.

Lidos integralmente: **instrucoes-agentes-plugins-fator3.md** e **padrao-desenvolvimento-plugins-fator3.md**, ambos revisão **5, 02/11/2026**. Aplicada a precedência do padrão. Plano e decisões no arquivo `PLAN.md` do fonte.

Requisitos: WordPress ≥ 7.1.4, PHP ≥ 8.3 de 64 bits, OpenSSL/mbstring, InnoDB e instalação de site único. Runtime remoto efetivamente exercitado: **WordPress 7.1.4, PHP 8.3.36, MySQL 8.4.11**. Validação sintática local: PHP 8.3.6. Navegador: Chromium 152.0.7940.0. Não foram testadas combinações inferiores ou migração reversa.

## 2. Convivência e encaminhamentos

| Plugin | Matriz inicial congelada | Matriz final testada e observada no Site-Teste |
|---|---|---|
| Site Core | 1.72.1 | **1.73.0** |
| MCP | 0.41.0 | 0.41.0 |
| Google | 0.30.0 | 0.30.0 |
| Meta | 0.21.0 | 0.21.0 |
| LinkedIn | 0.19.0 | 0.19.0 |
| Pipedrive | 0.7.0, base da troca | **0.8.0** |

Todos permaneceram ativos. Esta rodada substituiu somente o Pipedrive. Outro trabalho atualizou o Core durante o encerramento; isso motivou nova análise e repetição dos testes da fronteira afetada. O Core 1.73.0 tem instalador de 4.332.427 bytes, SHA-256 `6675c1e7436e1195f6f7559a9baf62e049d871d145c84f19c04ac67f8d25655e`. Seus 939 arquivos foram conferidos, junto aos outros acompanhantes: **1.768 arquivos em paridade** na matriz final. Os arquivos de implementação Pipedrive no Core não mudaram. Evidências iniciais em `matrix1721-*`; finais em `current-integrated`, `current-core`, `current-core-report` e `current-core-workflows`.

Os guias do instalador congelado identificam 1.72.1 como referência inicial; esta seção registra a prova complementar com o Core vigente 1.73.0. O cliente público continua `pipedrive-api-client/1.0.0`. As 19 operações públicas, seus schemas de entrada, permissões e 12 IDs documentais foram preservados. Nenhuma alteração obrigatória em Core, MCP, Google, Meta ou LinkedIn foi identificada no escopo examinado; não se emitiu relatório de impacto individual sem providência técnica. Os fluxos comerciais completos dos acompanhantes não foram rehomologados.

## 3. Mudanças e evidência

| Pedido exato | Problema | Mudança | Resultado e evidência |
|---|---|---|---|
| MCP Pipedrive 11, parte 1 | Marcador de progresso aparecia na nota da atividade | Progresso cifrado e local, confirmado na mesma transação do recibo; novos registros acrescentam somente a linha configurada | `requests080` e `restart080`: nota limpa, próximo toque, idempotência, expiração do diário, novo processo PHP e falha de persistência |
| MCP Pipedrive 11, parte 2 | Atividade criada sem pessoa/participante principal | Usa a pessoa do lead em `participants`, com `primary:true`, no POST v2; releitura confere pessoa e participante | Fixture v2 e encoder real do Core; divergência mantém pendência e impede repetição |
| Manutenção do painel e guias | Administrador precisa saber onde fica o progresso e por que a pessoa é necessária | Textos do painel explicam participante, nota, progresso local e conservação; guias detalham erros e recuperação | Navegador desktop/móvel, leitura integral dos 12 documentos via MCP |

Na API v2, o parâmetro de escrita é `primary`; `primary_flag` é aceito na releitura do objeto retornado. Referências primárias conferidas em 06/11/2026: [Activities](https://developers.pipedrive.com/docs/api/v1/Activities) e [guia de migração v2](https://pipedrive.readme.io/docs/pipedrive-api-v2-migration-guide). Usar o nome correto do endpoint atende ao vínculo solicitado.

Os marcadores antigos continuam legíveis e permanecem no histórico já existente. A configuração de prefixo da nota, inclusive vazio ou `[IA]`, é preservada. Não houve limpeza retroativa em massa. Atividades existentes mantêm seus participantes. Na criação sem pessoa válida, `lead_sem_pessoa` recusa antes do envio. Alteração textual, exclusão ou substituição de atividade com progresso local exige reconciliação; normalização de HTML/espaços é tolerada.

**550 asserções aprovadas**, sendo 512 PHP/WordPress e 38 no navegador. As suítes novas do Pedido 11 somam 41. As repetições da mesma fronteira nas duas versões do Core não são somadas novamente ao total.

| Grupo | Asserções |
|---|---:|
| Operações nativas, relatório e retenção | 172 |
| Regressões de workflows, regras, qualidade, recibos e auditoria | 195 |
| Pedido 11 e persistência em novo processo PHP | 41 |
| Integração MCP, paridade de pacotes e cliente original do Core | 70 |
| Atualização da base e reinício | 17 |
| Documentação no runtime instalado | 17 |
| Navegador, permissões, confirmação e responsividade | 38 |

O verificador final aprovou **109 verificações de integridade/encerramento**, incluindo lint de **46 arquivos PHP**, schemas publicados, reprodução do ZIP e correspondência dos **36 arquivos de runtime**. Esses checks não são adicionados às 550 asserções funcionais. Um teste da bancada ainda comparava a versão com 0.7.0; sua expectativa foi corrigida para 0.8.0 e a suíte repetida. Não houve alteração do instalador após sua primeira instalação nativa.

## 4. Instalação e prova da troca

Site: https://fator3-teste-mcp-1.dreamhosters.com/ . Instalador transferido por pacote de bancada privado e validado pelo SHA-256 da seção 8. Troca compartilhada por `plugins/upload-base64`, com `zip_path`, `expected_slug=wp-mcp-pipedrive-fator3`, `expected_sha256`, `activate=true`, `overwrite=true` e chave de idempotência. Não houve publicação GitHub/raw nesta rodada; a publicação pela frota permanece separada.

Operação concluída: `3cd9a2d66d002860b95f53d1cb77dc81`; pré-imagem `805bd87f9a05c251f06c8221`. O recibo confirmou 0.7.0 → 0.8.0, ativa, processo PHP independente, `applied=true`. A atualização de plugin já ativo usa reativação silenciosa; o recibo não afirma execução do hook de ativação. A instalação limpa em bancada comprovou o ciclo nativo completo.

A primeira tentativa retornou `resource_busy` e nenhuma troca foi constatada. A repetição da mesma chave retornou o mesmo recibo. Após conferir a versão e ausência de diário de instalação dessa tentativa, iniciou-se outra intenção, que concluiu. Evidências `shared-install-busy`, `shared-install-retry` e `shared-install` preservam a sequência. Não houve downgrade.

| ID | Ambiente/cenário | Resultado | Evidência | Limite |
|---|---|---|---|---|
| A | WordPress limpo, somente Pipedrive | Instalação 0.8.0; bootstrap carrega um arquivo; testes próprios aprovados | `current-install`, `current-bootstrap080`, suítes funcionais | CRM sintético |
| B | WordPress com a 0.7.0 | 4 operações, 3 linhas de diário, regras, prazos e marcador preservados; replay sem escrita | `upgrade-*` | Dados sintéticos |
| C | Cinco acompanhantes ativos | Versões e bytes conferidos; executor e encoder originais exercitados | `current-integrated/core/core-report/core-workflows` | HTTP de fornecedor interceptado |
| D | Painel real do plugin via ponte de bancada | 38 asserções, 31 requisições, sem erro de cliente; largura de 360 px conferida | `browser.json`, captura sintética | Não é login no wp-admin compartilhado |
| E | Site-Teste compartilhado | 0.8.0 ativa; tabelas, regras, prazos e autorização preservados; HTTP 200 antes/depois | `shared-*`, `health-final`, `plugins-final` | Conta comercial permaneceu desautorizada |

Documentação: 12 IDs, reconstruídos em 72 páginas na integração (limite 2.048 bytes) e 16 páginas no site compartilhado (limite 16.000), com conteúdo e hash iguais aos arquivos locais. Descoberta final: 19 abilities Pipedrive, todas 0.8.0, sem os controladores desta rodada. As sondas de `/` e `/wp-json/` retornaram HTTP 200, cache contornado e PHP novo; são sondas internas de mesma origem, sem prova de acesso externo.

Limpeza: as três bancadas e a repetição da matriz atual foram removidas, com zero tabelas restantes em seus prefixos. ZIP de bancada e dois controladores temporários foram removidos por hash; ausência confirmada. Backups e recibos do MCP foram preservados. `system/health` final: saudável, recuperação sem pendências. Core 1.73.0 e demais versões da tabela estão ativos.

## 5. Banco, migração e correção por nova versão

Schema **1**, sem tabela nova e sem reescrita dos registros anteriores. Cada conta/lead passa a ter uma linha interna `state=progress` na tabela de operações, consultada por chave primária HMAC. Ela guarda, cifrados: identidade, ID da atividade, código/instante do toque, digest da nota e ID do recibo. Não contém mensagem. Não é uma prévia executável e pode ser consultada pela cadência entre administradores autorizados na mesma conta.

Recibo, diário e progresso são persistidos na mesma transação InnoDB. Se a gravação local falhar depois do efeito remoto, permanece a operação em execução e a trava para reconciliação. A mesma chave não reenvia a escrita. A limpeza finita do diário conserva os recibos de WhatsApp e o último progresso. Não há cron nem migração em leituras. Backup deve incluir tabelas próprias e salts. A troca preservou bytes/revisão das regras, tabelas, política de retenção e autorização comercial.

Qualquer correção posterior à instalação deve partir deste estado em uma nova versão. Confirme os efeitos no fornecedor e preserve recibos/travas antes de retomar; não apague o progresso para repetir mensagens já registradas. Não foi implementado downgrade, restauração automática de CRM ou reinício automático de cadência.

## 6. O que permanece pendente

**Aceite comercial do Pedido MCP Pipedrive 11 em korvena.com.br:** criar e excluir um lead de teste no mesmo trabalho, com pessoa vinculada; confirmar na conta real a nota limpa, a pessoa como participante principal e o replay sem nova escrita. Essa prova não foi executada: a autorização existente nesta rodada abrange o Site-Teste, cujo Core mantém a operação comercial desautorizada; o contexto disponível aponta o aceite de conta ao SDR/frota. Os testes sintéticos não substituem o comportamento da API e da interface reais. Nenhum lead, pessoa ou atividade real foi criado por esta rodada.

Publicação/implantação em outros sites não foi executada. O pacote entregue está pronto para essa homologação, preservando a decisão e os ativos de cada site. A implementação foi validada nos runtimes e combinações descritos; testes completos de outros plugins, faturamento, envio real de WhatsApp e integrações comerciais externas estão fora da prova.

## 7. Credenciais e configuração do dono

Token e autorização continuam no Site Core. Nenhuma credencial foi lida ou incluída nos artefatos. Não é exigido token novo. No site-porta autorizado, conferir o status do consumidor, conta e orçamento pelo Core. O Pipedrive não habilita a operação automaticamente.

No WordPress: Ferramentas → Fator3 MCP Pipedrive. Para criar atividades, o lead deve ter pessoa vinculada; manter o código do tipo WhatsApp e as regras aprovadas. Alterações de regras passam por simulação, revisão e confirmação já existentes. Não houve mudança de textos comerciais, prefixo, calendários ou motivos reais.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `wp-mcp-pipedrive-fator3-0.8.0-instalador.zip` | 122083 | `89e41f2f7a2124eb1a5961fe06d6aff60fd168b8d6dd2ea1b21a272772ff7f30` |
| Fonte | `wp-mcp-pipedrive-fator3-0.8.0-fonte.zip` | 507256 | `b4ae837c77c84c4e31a21b5a34b9f5d479189e10e02508026e4b41c2e74cc93b` |

Somente o instalador é instalável: raiz `wp-mcp-pipedrive-fator3/`, 36 arquivos de runtime. O fonte contém código, testes, build, plano, documentos de entrada, evidências sanitizadas e cópia do relatório; raiz `wp-mcp-pipedrive-fator3-0.8.0-fonte/`. Nenhum ZIP contém outro ZIP. Não há dependência Composer/npm de runtime, credencial, banco, controlador ativo ou fixture no instalador.

Relatório externo canônico: `wp-mcp-pipedrive-fator3-0.8.0-relatorio.md`. A cópia no fonte está identificada como anterior ao fechamento e não contém o tamanho/hash do próprio ZIP. Esses campos foram preenchidos somente aqui após empacotamento; o ZIP fonte permanece congelado.

Checklist da seção 14 conferido: normas e precedência; identidade/base/alvo; requisitos; contratos; impactos; preservação; instalação limpa e atualização; documentação integral pelo MCP; testes e limites; estado final; limpeza; nomes, hashes e conteúdo dos artefatos. O item de aceite comercial permanece pendente conforme a seção 6; não se declara conformidade de uma prova não executada.
