# Entrega — Fator3 MCP Meta 0.18.0

31/10/2026 — America/Sao_Paulo. Pedido Meta 26. Base direta: 0.17.0. Nova rodada minor; nenhuma candidata desta rodada havia sido entregue anteriormente. A 0.18.0 é a versão corrente desta entrega.

## Bases aceitas

Lidos integralmente os pedidos Fator3 MCP Meta(20261031-224150).md, os relatórios atuais e o código relevante dos pacotes Core 1.65.1/MCP 0.38.0, além da entrega Meta 0.17.0 e das instruções comuns de desenvolvimento e agentes recebidas. Aplicadas as correções r5 e instruções expressas do usuário sobre impactos e retenção: impactos comunicam consequências técnicas ou pedidos novos; resultados, respostas e encerramentos pertencem ao relatório próprio. O histórico incorporado à base foi preservado, sem tratar suas provas como novas execuções.

Base Meta 0.17.0 íntegra: fonte 3.546.251 bytes, SHA-256 84fe2092cf2f5312dbd0609bdae795bee9a2dd4c9076a0118d4c3fa022bcb7ca; instalador 327.384 bytes, SHA-256 a360feff0bdb723c7f3c2a240b288bc1c3af917e851cb798d905e31a95b4162d; relatório 15.429 bytes, SHA-256 c62220c034bab5e702e558c265b893bf18dffbfe619f14eb0282c93c0dde60e8. Entradas atuais preservadas em inputs/0.18.0; seus arquivos ZIP não são aninhados no fonte.

| Entrada recebida | Bytes | SHA-256 |
| --- | ---: | --- |
| Fator3 MCP Meta(20261031-224150).md | 5353 | f8eb69dee8899dbf25a41500463e565a3c8345d43abb305d7364b317ee322b56 |
| base-site-core-fator3-1.65.1-fonte(1).zip | 8035411 | 279b11eea6e273a0a42c93434fd44b3b6b75a21745139b30581672358eadadf5 |
| base-site-core-fator3-1.65.1-instalador(1).zip | 4206718 | 059d7da03484eb3d9eb7327f49787144466f451fcf51730ea0357d92c03f168a |
| base-site-core-fator3-1.65.1-relatorio(1).md | 20146 | dbedc8213bb04cf6e873a967b417f9eaef6089f37e7ba92c8b7bbe3c89510cde |
| wp-mcp-fator3-0.38.0-fonte(3).zip | 6041317 | cdf50f0d75c1dba5dbea1a6f1d687fad04bea67a43ddc98fd24c6ff526c9a7f1 |
| wp-mcp-fator3-0.38.0-instalador(3).zip | 913547 | bc550c6573527a0d71bfa560036f83e7c8aec546f49d70b8e0095da5d303c1a5 |
| wp-mcp-fator3-0.38.0-relatorio(3).md | 14630 | 145d9176627d0a7e3aba52943e26c3cc54c3d918a19b4752a4dae0ff3838bb37 |

O documento recebido informa implantação da 0.17.0 em 12 sites e retirada do Pedido 25 da lista de pendências do pacote. Isso é evidência recebida da frota, não uma implantação ou homologação de produção executada nesta rodada. O Pedido 26 é o novo trabalho solicitado: três agendas Ads de korvena.com.br completam com last_code=null e último sucesso recente, mas mantêm last_error de budget_exhausted sem sinalização histórica.

## Convivência e encaminhamentos

| Pacote | Versão observada | Verificação própria |
| --- | --- | --- |
| Site Core | 1.65.1 | 907 arquivos iguais ao instalador recebido; suítes originais de Ads e monitoramento adaptadas ao laboratório, com procedência documentada |
| MCP | 0.38.0 | 467 arquivos iguais ao instalador recebido; transporte, perfis, autorização, idempotência e novas propriedades do diagnóstico preservadas pela decoração |
| Google | 0.24.0 | 172 arquivos preservados; convivência local |
| LinkedIn | 0.13.0 | 72 arquivos preservados; capabilities independentes e convivência local |
| Pipedrive | 0.5.0 | 31 arquivos preservados; estado sem concessão e ausência de envio |

Core 1.65.1 altera módulos front-end, estado de formulários, cache de CTA e publicação de assets; MCP 0.38.0 torna preguiçoso o catálogo de auditoria de mutações fora do bootstrap público/login. Os contratos consumidos pelo Meta permanecem compatíveis. Os relatórios recebidos mantêm limites próprios, inclusive validação de desempenho e aceite de frota; esta entrega não os declara concluídos.

Os SDKs meta-ads-reader/1.0.0, meta-ads-monitoring/1.0.0 e instagram-message-erasure/1.0.0, seus grants, os schemas de entrada, as 47 operações, os rótulos em português, Messaging, MessagePrivacy, Retention, HTTP e fila permanecem iguais à base. Alteração funcional limitada a CollectionState, leitura de agendas em Query e resumo de Worker; Config, bootstrap e catálogo documental mudam a versão/conteúdo gerado. O diagnóstico de saída ganha campos aditivos. A árvore instalada tem os mesmos 65 nomes de arquivos da base.

Nenhum novo pedido técnico a outro mantenedor foi identificado: não foi emitido arquivo de impacto. LinkedIn não foi modificado e não apresentou regressão nos testes locais de convivência; sua API remota não foi chamada. Nenhuma alteração foi feita em pacotes acompanhantes ou na lista central de pedidos.

## Mudanças por pedido e evidências

**Pedido 26 — distinguir falha atual de diagnóstico histórico.** CollectionState já conservava intencionalmente o erro anterior depois de uma coleta completa. A 0.18.0 mantém esse dado e projeta três propriedades junto do estado existente em meta/list-schedules.data.schedules[] e meta/health.data.schedules[]:

| Campo | Semântica |
| --- | --- |
| last_error_at | Data Unix inteira positiva de last_error.observed_at, ou null se não existe data confiável |
| last_error_superseded | true quando a evidência disponível comprova que o erro guardado foi superado |
| last_error_state | none sem objeto de erro; superseded para histórico superado; current com falha/parcial ou código atual; unknown quando a ordem não pode ser provada |

last_error continua integral, sem remoção ou regravação. O resultado complete com last_code=null comprova superação, inclusive para coleta vazia e registro legado sem timestamp. Fora desse caso, a data de sucesso precisa ser estritamente posterior à do erro e não pode haver falha/parcial nem código atual. Dados úteis parciais também atualizam last_success_at, portanto esse timestamp isolado nunca esconde uma falha atual. Empate de segundos, data ausente e erro posterior ao sucesso ficam unknown. last_error_superseded=false sozinho não significa falha atual; consumidores devem usar last_error_state e os campos de execução. none significa ausência do objeto de erro, não uma declaração geral de saúde.

Health passa a expor o mesmo diagnóstico mínimo por agenda, incluindo as desabilitadas, dentro da leitura já limitada às primeiras 100 agendas. Seus contadores, incidentes, orçamento, notificações e critérios existentes não mudam. A projeção não coleta, não reexecuta, não migra nem grava a agenda; a auditoria administrativa normal da operação permanece. O erro histórico superado não cria um novo incidente.

**Reprodução e aceite sintético.** Na base, um job realmente executado no laboratório recebeu HTTP 503 simulado, foi retomado e concluiu; o diagnóstico antigo permaneceu sem marcação. Na candidata, esse fluxo mantém o erro, data e flag explícita de superação nas duas leituras. Uma falha nova volta a ser current. A matriz cobre 12 estados legados/temporais, agenda desabilitada, coleta vazia, parcial útil, datas ausentes/empatadas e combinações conservadoras de código/status. Leituras preservaram os bytes do registro e não acrescentaram HTTP ou e-mail. Assinantes sem capacidade administrativa foram recusados.

Atualização direta 0.17.0 → 0.18.0 mostrou uma agenda legada completa com antigo budget_exhausted como superseded na primeira leitura, sem nova coleta. As mesmas propriedades foram conferidas via abilities efetivamente decoradas pelo MCP, além do despacho nativo Meta. Os 28 documentos foram atualizados onde necessário, incluindo exemplos, migração, diagnóstico, contratos e caminho correto do envelope data.schedules[].

## Instalação, testes e prontidão

**394 verificações aprovadas na candidata**, contadas por execução/ambiente, mais **3 verificações aprovadas da reprodução na base**. Não são 397 casos exclusivos. Lint aprovado em 33 arquivos PHP. Builds repetidos geraram o mesmo instalador, SHA-256 5aef6b8fe85e69478285a84ed5d12c623d7834108928c911ca0e54aaf46d95f8. O runtime do fonte é idêntico ao ZIP instalado.

| Suíte | Verificações aprovadas |
| --- | ---: |
| upgrade | 14 |
| current-smoke | 36 |
| diagnostics | 58 |
| budget0180 | 29 |
| review071 | 11 |
| integration | 27 |
| diagnostics-integrated | 60 |
| coreads | 46 |
| coremonitor | 19 |
| minimum-smoke | 36 |
| minimum-diagnostics | 58 |

As regressões cobrem orçamento por chamadas/tempo, prioridade sobre backfills, alertas interceptados, retomada, fila/quarentena, concorrência de locks MySQL, grants e permissões, leitura Core Ads e monitoramento, perfis/transporte MCP, idempotência e integridade dos acompanhantes. As suítes Core usadas provêm do pacote 1.65.1 recebido; adaptações de bootstrap, versão, caminho de evidência e capacidade sintética estão registradas no fonte. Não se presume reexecução de todas as funcionalidades históricas nem dos testes de front-end/desempenho próprios dos acompanhantes.

A primeira execução da reprodução na base falhou no harness após duas verificações: o teste tratava list-schedules.data como lista, embora o envelope real seja data.schedules. O teste e as referências documentais equivocadas foram corrigidos; o laboratório inicial foi removido e a reprodução passou em instalação nova. O erro não exigiu mudança no runtime funcional da candidata. A execução inicial está preservada em baseline-reproduction.json e não integra a contagem de aprovações.

Ambiente principal: WordPress 7.1.4, PHP 8.3.36 de 64 bits, MySQL 8.4.11. Piso: instalação limpa WordPress 6.4 com PHP 8.1.2-1ubuntu2.28 de 64 bits, runtime oficial pinado por hash; 36 verificações de instalação e 58 do Pedido 26 aprovadas. No piso sem Abilities API nativa, REST e funções do Meta operaram; não se presume disponibilidade nativa do transporte MCP. Ambientes final integrado e mínimo sem erros registrados do pacote. HTTP de fornecedores e e-mail foram interceptados: zero chamadas reais aos fornecedores e zero e-mails reais enviados pelos testes.

Instalador final aplicado no Site-Teste de 0.17.0 para 0.18.0, ativo antes/depois. Operação e001d5b65aec492861cd5b62379643a2; pré-imagem nativa f79b232d25fd0eaa12649853. Probes de / e /wp-json/ retornaram HTTP 200 antes/depois, com bypass de cache. A troca fez reativação silenciosa em processo independente; o ciclo de ativação limpa foi testado nos laboratórios. Os probes não comprovam prontidão comercial, acesso externo ou entrega de e-mail.

Pós-instalação: 28 documentos/31 páginas lidos por meta/documentation com expected_revision, inclusive input-schemas.json em quatro partes; todos os bytes/SHA-256 iguais ao pacote final. Descoberta final: 47 operações, todas 0.18.0, sem abilities temporárias. Health final: state=ok, storage_ready=true, crypto_ready=true, sem incidentes, zero conexões/agendas no WordPress compartilhado. Isso comprova prontidão estrutural, não coleta real nesse site sem conexão.

Cinco laboratórios removidos: 14, 14, 14, 101 e 14 tabelas exclusivas, respectivamente; todos com zero tabela restante, diretório e manifesto eliminados. Controlador e bundle temporários removidos com SHA-256 esperado e backup nativo. A remoção do controlador passou probes PHP antes/depois. Nenhuma tabela compartilhada foi apagada.

## Banco, retenção e reversão

Sem DDL, migração ou novos campos persistidos. A marcação é calculada durante a leitura a partir dos valores já existentes. Preservados schemas de registros 2 e histórico 1, retenção máxima, ciphertext, registros de coleta, erros e recibos. Nenhuma limpeza, concessão, seleção, retomada de pausa ou troca de credencial automática.

Na atualização isolada, 13 registros, quatro linhas históricas e opções da fixture permaneceram byte a byte iguais, incluindo políticas de retenção e agenda legada. Na instalação compartilhada, dois registros de negócio, histórico vazio, sete opções Meta e configuração Core de monitoramento preservaram seus hashes. Auditoria técnica é excluída do digest de negócio: registrar as operações administrativas é comportamento existente.

Os cinco acompanhantes conservaram versão, ativação, número de arquivos e digest desde a captura inicial até a imediatamente posterior à instalação. Runtime Meta instalado: 65 arquivos, árvore SHA-256 d9c62bda08e2f0bd154d19818e4247878dbaa2cfb6b5343e80f5811f344f25f0, igual ao instalador. Evidência detalhada em shared-integrity.json, runtime-diff.json e nas capturas anteriores/posteriores.

Rollback: preservar banco, salts/chaves, concessões e recibos e repor somente o instalador 0.17.0 ou a pré-imagem nativa indicada. A base volta a exibir erro histórico sem a marcação nova; nenhum dado precisa ser convertido. Reversão de arquivos não desfaz coletas ou e-mails já realizados. Desativação/desinstalação preservam os dados. Não apagar recibos para repetir efeitos e não voltar a versões anteriores à 0.12.0 com mensagens habilitadas.

## Pendências e responsáveis

- **Frota/operador de korvena.com.br:** instalar o ZIP final e confirmar nas três agendas Ads completas a indicação superseded, last_error_superseded=true e data histórica quando disponível, tanto em list-schedules quanto health. Confirmar que incidentes novos continuam current. Nenhum site de produção foi alterado nesta rodada.
- **Frota/operador dos demais sites:** o documento recebido mantém aceite operacional de dados diários/Ads/EMQ do Pedido 20 e informa Twinia sem conexão. Essas pendências não são encerradas por testes sintéticos desta entrega. O encerramento recebido do Pedido 25 não é declarado como nova prova própria.
- **Operador responsável por fornecedores/e-mail:** permissões, ativos, latência real, dados do dia, EMQ e entrega na caixa postal exigem observação autorizada no ambiente real. Não houve gasto de anúncios nem envio comercial.
- **Dono/frota:** distribuir os artefatos e atualizar main conforme a governança existente. Nenhum push, publicação de produção ou mensagem a terceiros foi realizado.

Não há bloqueio técnico observado para entregar a 0.18.0. O aceite específico de produção do Pedido 26 permanece pendente. A interface visual não foi alterada nem re-homologada por navegador nesta rodada; os diagnósticos foram exercitados via PHP, REST e MCP. Não há alegação de ausência absoluta de impacto fora dessas fronteiras.

## Credenciais e segurança

Nenhuma credencial nova necessária, criada ou substituída no WordPress compartilhado. Laboratórios usaram tokens sintéticos, diretórios/prefixos privados e isolamento de HTTP/mail; acesso ao banco ficou no servidor. Não foram criados contatos reais, gastos ou mensagens externas. Pacotes não incluem segredos, cookies, banco dos laboratórios nem o runtime binário PHP utilizado nas provas. Autorização administrativa e grants permanecem independentes.

## Arquivos finais e integridade

Somente o ZIP instalador é instalável. Raiz wp-mcp-meta-fator3/, basename, prefixos e identidades preservados. Fonte com raiz wp-mcp-meta-fator3-0.18.0-fonte/, build, runtime, testes, documentação, inputs, histórico, planejamento, evidências e relatório interno. Nenhum ZIP aninhado. Evidências históricas não significam reexecução na rodada atual.

| Arquivo | Bytes | SHA-256 |
| --- | ---: | --- |
| wp-mcp-meta-fator3-0.18.0-instalador.zip | 332343 | 5aef6b8fe85e69478285a84ed5d12c623d7834108928c911ca0e54aaf46d95f8 |
| wp-mcp-meta-fator3-0.18.0-fonte.zip | 3834792 | 3696598305259aac5defa52a3ab6940cdf5b5bba29a003ced15dff775100b75c |

Este é o relatório externo final. O fonte contém cópia interna anterior ao fechamento, explicitamente identificada, evitando circularidade de hashes. Evidências primárias em evidence/suite-summary.json, diagnostics.json, diagnostics-integrated.json, baseline2-reproduction.json, upgrade.json, minimum-diagnostics.json, shared-integrity.json, documentation-integrity.json, install.json e discovery-final.json.
