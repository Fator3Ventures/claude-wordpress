# Entrega — Fator3 MCP Meta 0.6.0

Revisão 2 · 22/10/2026 · America/Sao_Paulo · Implementação e validação no Site-Teste · **com-pendencias**.

**Pedidos MCP Meta 13 e 14 implementados, instalados e aprovados nas verificações técnicas do Site-Teste.** Atualização direta 0.5.0 → 0.6.0 concluída após autorização explícita do dono: 30 verificações remotas, zero falhas; 17 documentos lidos integralmente pelo MCP e conferidos com o instalador. O site terminou saudável, com Meta 0.6.0 ativo. Permanecem as limitações de matriz mínima, homologação externa, entrega real de e-mail e cron de servidor descritas na seção 6.

Relatório externo canônico. Esta revisão substitui o estado de implantação da revisão 1. A cópia interna no fonte é o registro anterior ao fechamento e à autorização remota; permanece histórica, sem hash circular do próprio ZIP fonte. Instalador e fonte foram preservados byte a byte. As evidências posteriores de Site-Teste estão no suplemento de validação, sem reabrir o ZIP fonte.

## 1. Bases aceitas e identidade

Normas `01-instrucoes-agentes-plugins-fator3.md` e `02-padrao-desenvolvimento-plugins-fator3.md`, ambas revisão 4 de 16/10/2026; pedidos atuais `Fator3 MCP Meta(5).md`. Bases e relatórios novos foram lidos, e os fontes MCP 0.28.0/LinkedIn 0.7.0 foram considerados na fronteira de integração. Documentos centrais não foram alterados.

Base imediata **0.5.0**, aceita no documento recebido e preservada byte a byte:

| Artefato-base | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-meta-fator3-0.5.0-instalador.zip | 122178 | 4198554e74d828609cbbe3477c569c71c86a6e7d68b7c15a2a7c77a63be116dc |
| wp-mcp-meta-fator3-0.5.0-fonte.zip | 365624 | c4af40c964a65561eac618bbdde9019613968afbb16cab1995ef739e4e003b91 |

Preservados nome Fator3 MCP Meta, slug/pasta/provider `wp-mcp-meta-fator3`, basename `wp-mcp-meta-fator3/wp-mcp-meta-fator3.php`, namespaces, Text Domain, Update URI, endpoints, dados cifrados, identidades e 33 IDs públicos. Incremento minor por novo ciclo. Os 33 schemas de entrada do domínio permanecem idênticos; a mudança de efeitos/perfil de `meta/status` está explícita abaixo. No catálogo efetivo, MCP 0.28.0 acrescenta a esse status mutante o campo opcional `idempotency_key` (string de 1 a 128 caracteres); a entrada `{}` continua válida. Para observação atual do estado, omitir a chave evita reuso de resposta anterior pelo transporte.

Runtime comprovado nesta rodada: **WordPress 7.1.3, PHP 8.3.6 de 64 bits, MySQL 8.0.46**. Cabeçalhos mantêm mínimos herdados WordPress 6.4/PHP 8.1.2; **não foram reexecutados e não constituem suporte comprovado por esta rodada**. Travas nomeadas no banco permanecem necessárias. No Site-Teste, a atualização e as 30 verificações foram executadas em WordPress 7.1.3/PHP 8.3.36, com Meta 0.6.0 e banco real. A versão exata do servidor de banco remoto não foi usada como evidência de matriz mínima.

## 2. Convivência e encaminhamentos

| Pacote | Versão recebida e usada no laboratório integrado | Site-Teste antes/depois |
|---|---|---|
| Fator3 Site Core | 1.47.0 | 1.47.0, ativo |
| Fator3 MCP | 0.28.0 | 0.28.0, ativo |
| Fator3 MCP Google | 0.17.0 | 0.17.0, ativo |
| Fator3 MCP LinkedIn | 0.7.0 | 0.7.0, ativo |
| Fator3 MCP Meta | base 0.5.0 → entrega 0.6.0 | 0.5.0 → 0.6.0, ativo antes e depois |

A evidência mais recente do MCP 0.28.0 informa o consumidor central de serviço LinkedIn já integrado, superando a pendência histórica do relatório LinkedIn 0.7.0 com MCP 0.27.0. Esse canal não muda as responsabilidades ou exige código de serviço no Meta.

Único encaminhamento pertinente: **wp-mcp-meta-fator3-0.6.0-impacto-wp-mcp-fator3.md**, revisão 3, `validacao-coordenada`/`alerta-tecnico`, validado tecnicamente no Site-Teste; a revisão dos perfis da frota continua com o dono. Revisão 1 foi emitida no planejamento antes da mudança de contrato. A política atual do MCP foi validada: perfil read recusa o novo status mutante; maintenance permite; custom precisa incluir meta/status. Nenhum perfil é ampliado automaticamente, e não se identificou mudança de código necessária no MCP.

Não há impacto técnico novo identificado em Core/Google/LinkedIn nas fronteiras examinadas. Implantador não recebido: não avaliado. Nenhum pacote alheio, repositório, documento central ou outro site da frota foi alterado. WP Super Cache 3.1.4, Yoast 28.7 e DreamHost Panel Login 1.0.0 permanecem ativos no Site-Teste.

## 3. Mudanças por pedido e evidência

### Pedido 13 — recuperação, diagnóstico e aviso

Antes, uma exceção ou perda da gravação do evento único interrompia a cadeia; a manutenção apenas fazia retenção. Agora manutenção horária e status recuperam o evento quando há agenda ativa, job queued/retry ou migração pendente. Jobs futuros mantêm a cadeia. O worker pré-agenda a próxima passagem, confere novamente em finally e usa trava de banco para impedir passagens concorrentes. Retenção não antecede a primeira tentativa de recuperação.

O retorno de `wp_schedule_single_event(..., true)` e a presença do evento são verificados; últimas tentativa/falha são persistidas com códigos seguros. Falha histórica permanece consultável após recuperação. Uma exceção não apaga a necessidade de reagendamento. WP-Cron ainda depende de tráfego/agendador; a manutenção garante uma oportunidade de recuperação na próxima passagem efetiva, não um prazo de relógio se o cron inteiro estiver parado. Escritores alheios da lista global do WordPress ainda podem apagar evento após a conferência; o watchdog trata a ausência observada.

`meta/status` agora declara **mode=write, readonly=false, local_effect=write, remote_effect=none**. O pedido explícito de recuperação é exceção à norma geral de diagnóstico sem reparo. `state/issues` e `cron.observed_next` mostram o estado anterior; `recovery` e `cron.next`, o resultado da tentativa. A primeira resposta pode permanecer degradada mesmo com recuperação bem-sucedida, evitando ocultar o incidente. Status não executa coleta, não consulta fornecedor e não envia e-mail. Documentação estática continua sem efeitos.

Diagnóstico carrega esse estado automaticamente. Agenda com next_at vencido há mais de duas vezes seu intervalo aparece degradada. Falha de autorização na agenda ou na última coleta também mostra nome, código e ação de conferir a conexão e salvar a agenda pela concessão atual autorizada. Revogação nunca transfere propriedade ou acesso aos resultados anteriores. `audit_health` mantém seu significado de auditoria; saúde operacional aparece separadamente em `state`.

Worker/manutenção enviam aviso ao `admin_email` do WordPress, com nome/ID da agenda e ação, sem token, concessão opaca, payload ou dados coletados. Uma trava e reserva persistida limitam a uma tentativa por hora por site, inclusive se falhar. `notification.state=accepted` significa aceitação por wp_mail, não entrega na caixa postal. Os testes interceptaram todos os avisos; nenhum e-mail real foi enviado nesta rodada.

### Pedido 14 — fila executável indexada

Antes, o worker examinava 20 registros históricos por passagem e só então identificava quais eram executáveis. Agora schema 2 acrescenta `queue_state`, `queue_next` e índice `runnable(bucket,queue_state,queue_next,record_key)` na mesma tabela. A mesma instrução SQL CAS atualiza payload cifrado e projeção. A alternativa de tabela separada foi descartada para não introduzir inconsistência entre gravações em tabelas diferentes.

São duas buscas limitadas por índice, uma por estado queued/retry, com prazo vencido; os candidatos são combinados por next_at/chave, até 20 por passagem. A seleção não percorre jobs concluídos. Agendas são materializadas antes da seleção, e cada job revalida estado/prazo/autoridade sob trava. Permanecem o orçamento de tempo e a retenção limitada de registros expirados, que é independente da seleção executável.

`queue.oldest_due_lag_seconds` informa o atraso da coleta vencida mais antiga; sem vencidas retorna zero e oldest_due_at=null. Registros da base são projetados em lotes de 100, preservando ciphertext, revisão, timestamps e retenção. Durante a migração, jobs novos já são indexados; `migration_pending=true` informa que o atraso cobre apenas a parte já migrada. Falhas de leitura/cifra não são tratadas como migração concluída.

Prova local e repetição no Site-Teste: com **2.000 jobs concluídos ordenados antes do novo job**, a agenda horária criou e concluiu a coleta **na primeira passagem**; processed=1. EXPLAIN confirmou índice runnable sem filesort. Foram exercitados retry futuro/vencido, pausa entre seleção e execução, CAS recusado, concorrência, migração limitada e preservação. Fontes da prova local: `tests/native/worker-cases.php` e `evidence/*/release060.json`; prova remota: `tests/meta060-qa.php` e `evidence/qa-result.json` no suplemento de validação.

## 4. Instalação, validação e estado final

**Instalador final: 134999 bytes, SHA-256 `36f5cfe9a20db272fc80d3cdd8fd46da823c4eeac856e31d911e41754fd19f69`.** Esses mesmos bytes foram instalados nos laboratórios e no Site-Teste; reconstrução local produziu arquivo idêntico. São 41 arquivos de runtime, 20 PHP com sintaxe válida e 17 documentos. Sem QA/testes/desenvolvimento ou ZIP aninhado no instalador. Árvore `plugin/` do fonte é igual ao ZIP.

| Prova própria | Resultado | Limite |
|---|---|---|
| Instalação limpa, Meta isolado | 98 verificações de metadados/documentos/permissões; 27 novas de worker/fila; 48 regressões; zero falhas | WordPress nativo com MySQL real, fornecedor simulado |
| Upgrade direto 0.5.0 com acompanhantes atuais | 133 verificações de metadados/preservação; 30 novas; 51 regressões; zero falhas | Preserva registros, histórico, opções de negócio e ciphertext exatos; novos marcadores/projeções excluídos da comparação |
| Executor MCP 0.28.0 real, laboratório | 18 verificações; 17 documentos completos em 19 páginas; hashes/bytes iguais ao instalador | Executor nativo, não sessão HTTP MCP remota |
| Interface administrativa | 10 verificações DOM/JS e REST autenticado; zero falhas | Inclui diagnóstico automático, nome/ação, degradação, atraso e ajuda; jsdom, sem prova visual de navegador |
| Sintaxe e empacotamento | PHP, JS, manifesto, runtime/fonte e reconstrução aprovados | Não substituem testes funcionais |
| Upgrade 0.5.0 → 0.6.0 no Site-Teste | Aplicado, ativo; home e REST HTTP 200 antes/depois; 30 verificações de worker/fila/perfis, zero falhas | WordPress e banco reais; fornecedor e e-mail interceptados; reativação silenciosa, sem ciclo completo de hook de ativação |
| Documentação no MCP remoto | 17 documentos completos, 19 páginas; todos os bytes e SHA-256 iguais ao instalador | Paginação com revisão esperada; nenhum documento truncado |
| Estado final no Site-Teste | healthy=true, Meta state=ok; 8 verificações de selftest aprovadas; QA removida | Sem conexões/agendas/jobs sintéticos remanescentes no Meta; sem homologação do fornecedor externo |

Contagens são execuções por suíte e têm cenários comuns; não representam casos únicos somáveis. Os 33 gates de abilities e recusas REST 403 de assinante foram exercitados localmente. A concessão de teste foi criada/revogada pelo armazenamento real do MCP; o worker recusou a autorização e o aviso foi capturado. Fornecedores, tokens e usuários de teste são sintéticos. Testes antigos incluídos no fonte não são provas adicionais desta rodada.

Leitura documental local e remota: índice, continuidade com revisão esperada, conteúdo integral, tamanho e SHA-256. A conexão MCP remota leu os 17 documentos da versão 0.6.0 em 19 páginas; o comparador confirmou igualdade byte a byte com o instalador em todos. O documento WORKER.md descreve contrato, operação, migração e recuperação. A descoberta final contém os 33 IDs públicos, sem a ability temporária de QA; o catálogo confirma o efeito de escrita local de status e o parâmetro opcional de idempotência acrescentado pelo MCP.

**Implantação autorizada e concluída:** o dono autorizou instalar os pacotes e alterar livremente o WordPress de teste. A recusa automática registrada na revisão 1 foi superada por essa autorização. A instalação via `plugins/upload-base64`, com slug e SHA-256 esperados, retornou `applied=true`, `active_before=true`, `active_after=true`, versão anterior 0.5.0 e atual 0.6.0. Site: https://fator3-teste-mcp-1.dreamhosters.com/.

| Marco remoto | Identidade / evidência |
|---|---|
| Atualização | operation_id `c3556e3401c6e13a763240d7`; package_operation_id `15bf0e297a7e8f06b6c68a15dd360c65` |
| Backup dos arquivos anteriores | `66598de66505cd1b4ca195f5`; não é backup de banco |
| Escrita da sonda temporária | operation_id `e8e618a756a67645d5a90f75`; `wp-content/mu-plugins/f3-meta-060-qa.php`, 15928 bytes, SHA-256 `8e4b12e81a4add73f6444813b5fc422a57f70aa479ae8fb3ef25404c77aaf39b` |
| Execução de QA | operation_id `93159a05bb7b8c1d420e6214`; 30 verificações, 0 falhas |
| Remoção da sonda | operation_id `20a5d29e0f425932ad624417`; backup `f99ea6a645aca8d280a822f2`; exclusão com hash esperado |

A reativação ocorreu em nova requisição PHP por worker independente, em modo `silent_reactivation`. O retorno declara `activation_hook_cycle_completed=false`, `business_readiness_verified=false` e `database_effects_reversible=false`. As sondas internas de home e REST retornaram HTTP 200 antes e depois, com nonce PHP assinado e cache bypass verificado. Isso comprova resposta interna atual, sem afirmar acesso externo público ou invalidação de todos os caches. Instalação limpa foi provada no laboratório, não repetida remotamente.

A QA usou WordPress/banco reais, dois acessos ao banco para a trava concorrente e grant sintético persistido/revogado no MCP. Confirmou ausência e recuperação do evento, falha de agendamento visível, degradação por atraso e revogação, prioridades queued/retry, CAS consistente e migração em lotes de 100 preservando ciphertext/revisão. A agenda horária concluiu um job na primeira passagem apesar de 2.000 jobs completos anteriores; EXPLAIN selecionou `runnable`, sem filesort. Os gates do MCP recusaram read e permitiram maintenance. Houve 1 chamada ao fixture HTTP e 2 mensagens interceptadas, nenhuma chamada real à Meta ou envio real de e-mail.

A sonda foi removida após a execução, e a consulta subsequente a `meta/qa-release060` retornou ability não encontrada. Estado final: Meta 0.6.0 ativo, os outros sete plugins nas mesmas versões e ativações; `healthy=true`; Meta `state=ok`, storage/crypto prontos, `issues=[]`, zero conexões e agendas, lista de jobs vazia, `worker_required=false`, atraso da fila zero e `migration_pending=false`. Selftest: 8 checks ok, `external_checks=not_run` e `remote_homologated=false`. Backups, auditoria e tombstones da concessão sintética permanecem como rastros operacionais; não há concessão sintética ativa ou dados de negócio de QA no Meta.

Logs locais: nenhum fatal/warning/deprecation atribuído ao Meta. Integrado registra cinco notices herdados de tradução antecipada de `f3base`; DOM registra três warnings do WordPress ao consultar atualizações com rede bloqueada. Não foram alterados acompanhantes para suprimir esses avisos. Logs privados remotos não foram revisados integralmente.

## 5. Banco, preservação e reversão

Migração aditiva schema 1 → 2 na tabela de registros; histórico mantém seu schema. O índice contém somente estado/prazo técnicos. Consultas, resultados, tokens e identidade permanecem cifrados com a chave existente. Há novas opções de progresso do índice, reagendamento, manutenção e aviso. Sem seleção de ativo, troca de credencial, concessão ou destino comercial novo.

Backup de arquivos não é backup do banco. Preservar banco e salts antes da troca; não desinstalar para simular rollback. Planejar uma janela sem workers da versão anterior em execução durante a substituição e verificar migração/evento após o bootstrap. Voltar à 0.5.0 conserva colunas extras, mas perde recuperação, alertas e prioridade indexada. A 0.5.0 redefine schema=1 no bootstrap; um retorno posterior à 0.6.0 reconstrói as projeções. Downgrade operacional não foi ensaiado nesta rodada. Código revertido não desfaz coletas/avisos já realizados nem recupera dados removidos por retenção.

Agendas com concessão revogada precisam ser salvas explicitamente pela identidade autorizada atual. O alerta é limpo pela próxima passagem bem-sucedida, não pelo simples mascaramento do erro. Resultados vinculados à identidade anterior permanecem protegidos. Não se faz reautorização automática.

## 6. Pendências e responsáveis

| Pendência | Responsável / ação |
|---|---|
| Fechamento editorial dos Pedidos 13 e 14 | Verificações técnicas no Site-Teste concluídas com sucesso; dono/revisor registra o aceite nos documentos centrais conforme seu processo. Não há autorização remota pendente para esta execução. |
| Distribuição na frota | Dono/frota/revisor: publicar/instalar com expected_slug e SHA-256 segundo a janela de cada site. Nenhum push ou implantação nos outros sites nesta tarefa. |
| Perfis MCP que usavam status como leitura | Dono revisa e autoriza maintenance ou custom com meta/status quando desejar recuperação. Sem ampliação automática; impacto anexo. |
| Mínimos WordPress 6.4/PHP 8.1.2 | Mantenedor: repetir matriz específica antes de alegar suporte mínimo comprovado por esta versão. |
| Homologação externa e pendência 20 recebida | Dono/frota: rotação real, exportação de histórico real e Story expirada com insight guardado permanecem sem novo aceite externo. Recusa de assinante foi testada localmente; não encerra o item de frota. |
| Entrega de e-mail e cron de servidor | Dono/operação: conferir entrega real e disparo do cron de servidor no site. Testes provam comportamento com wp_mail interceptado e hooks acionados, não entrega postal nem relógio do servidor. |
| Revisão visual de navegador e Implantador | Não executada/não recebido nesta rodada; DOM e fronteiras examinadas estão descritos. |

O aceite técnico sintético no Site-Teste foi concluído; não se declara homologação externa da Meta nem encerramento editorial ou trabalho de outro mantenedor. Não foram introduzidos gastos, publicações, assinaturas sociais, conversões comerciais ou mensagens reais.

## 7. Credenciais e configuração

Nenhum segredo novo. Tokens sociais manuais e seleção explícita de ativos continuam em Ferramentas → Fator3 MCP Meta. Não recriar credenciais apenas para atualizar. O destinatário operacional é o e-mail de administração já configurado em Configurações → Geral; nenhuma lista de clientes é usada. Diagnóstico informa tentativa/aceitação de envio, sem afirmar recebimento.

Instalador, fonte e evidências não contêm segredo real, cookie, banco, sessão ou captura pessoal. Grants/IDs de QA no laboratório e no Site-Teste são sintéticos; os testes deixam tombstones de revogação no MCP, não concessões sintéticas ativas. A sonda remota foi instalada, executada e removida. O suplemento contém respostas técnicas, documentação pública e código da sonda, sem credenciais reais.

## 8. Arquivos finais e integridade

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-meta-fator3-0.6.0-instalador.zip | 134999 | 36f5cfe9a20db272fc80d3cdd8fd46da823c4eeac856e31d911e41754fd19f69 |
| wp-mcp-meta-fator3-0.6.0-fonte.zip | 405780 | 7f5454c7b7fe9f66f080a602d7fad69c5cd2bc051a41933b243fad057af8c7da |
| wp-mcp-meta-fator3-0.6.0-validacao-site-teste.zip | 41447 | a80f1520ead2f27b6b4ef0a3d910e4383743456cf5a13e3561723c80a2fb595b |

Apenas o instalador é instalável, raiz wp-mcp-meta-fator3/. Fonte tem raiz wp-mcp-meta-fator3-0.6.0-fonte/, código/build/testes/evidências/referências e relatório interno anterior ao fechamento. Nenhum ZIP contém outro ZIP. Complementos: este relatório externo canônico (revisão 2), `wp-mcp-meta-fator3-0.6.0-impacto-wp-mcp-fator3.md` (revisão 3) e `wp-mcp-meta-fator3-0.6.0-validacao-site-teste.zip` (evidências posteriores). O suplemento é documental/de teste, não instalável; não contém outro ZIP. Fonte fechado uma vez; hash e tamanho finais preenchidos somente no relatório externo. Nenhum código ou byte dos pacotes instalador/fonte mudou após o aceite remoto.
