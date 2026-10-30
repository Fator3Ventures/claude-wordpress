# Entrega — Fator3 MCP Meta 0.17.0

30/10/2026 — America/Sao_Paulo. Pedido Meta 25. Base direta: 0.16.0. Nova rodada minor; nenhuma versão candidata desta rodada havia sido entregue antes desta 0.17.0.

## Bases aceitas

Foram considerados o documento de pedidos Fator3 MCP Meta(20261030-172612).md, os pacotes e relatórios Core 1.62.0 e Google 0.24.0, a entrega Meta 0.16.0 e os impactos históricos que ela incorporou. As regras comuns recebidas r4 foram aplicadas com as correções r5 e instruções expressas do usuário: impactos servem para consequências técnicas/pedidos novos; respostas, resultados e encerramentos ficam no relatório próprio. Retenção ampliada permanece vigente.

A base Meta foi recuperada sem alterações: fonte 3.268.614 bytes, SHA-256 826875296447fe946cda3944dd481b199f3927a48cdb92277435785dc0386ab6; instalador 315.170 bytes, SHA-256 a49f3e8ae9e60814ab55cf1bd4b3277e859a477347d02f664353c1268fda0b6b; relatório 15.240 bytes, SHA-256 cbff9ff1a37e023fa8c5488d2c15c7697750a5d5f6667e1df625074b6318e975. Inputs atuais, bytes e hashes estão em inputs/0.17.0/packages.json, reproduzidos abaixo. Relatos recebidos não são contabilizados como novas provas executadas nesta rodada.

| Entrada recebida | Bytes | SHA-256 |
| --- | ---: | --- |
| Fator3 MCP Meta(20261030-172612).md | 6530 | a9bd28133adeb34cccd1309b2940658751bc77bcb9d7e6c4b06bdff534f1ec77 |
| base-site-core-fator3-1.62.0-fonte(1).zip | 5859483 | dd6f4dd466a57ec2cdcbf72492a98678a966dc38e96123c5f8fa1255b61cbe0a |
| base-site-core-fator3-1.62.0-instalador(1).zip | 2948015 | 3dcbae9b1e22b915ac32ae3074cec1ed15706d4a475a9cf5d5b9e12663922646 |
| base-site-core-fator3-1.62.0-relatorio(1).md | 15923 | c847279970938155d4f9977254e428f0e514d23698d6cb30eb3b582c7ccd40d2 |
| wp-mcp-google-fator3-0.24.0-fonte(4).zip | 6789039 | 6e2dd4f447404b9610b091288be2841105c1c016e3eee034caa7fd31e903af0f |
| wp-mcp-google-fator3-0.24.0-instalador(4).zip | 886260 | 803fa058182b9f43625352f2b4a1572a3cd4b728f8c07fd58314a9a111d41849 |
| wp-mcp-google-fator3-0.24.0-relatorio(4).md | 18768 | 413d25327c2ded1b8602a1987af3f6a7cb55e89c499470ff382153d8f747c061 |

## Convivência e encaminhamentos

| Pacote | Versão verificada | Prova própria desta rodada |
| --- | --- | --- |
| Site Core | 1.62.0 | 804 arquivos iguais ao fonte recebido; SDK Ads, monitoramento, campanha local e leitura de ontem recém-coletado |
| MCP | 0.37.0 | Políticas de transporte, perfis, revogação, filtro, idempotência e documentação remota |
| Google | 0.24.0 | Convivência e integridade dos 172 arquivos; APIs Google reais não executadas |
| LinkedIn | 0.13.0 | Convivência, capabilities independente e integridade dos 72 arquivos; fornecedor LinkedIn não chamado |
| Pipedrive | 0.4.0 e 0.5.0 | Convivência e status sem concessão/envio; 30 e 31 arquivos respectivamente |

Pipedrive foi atualizado externamente para 0.5.0 durante esta rodada. A mudança foi detectada pelo digest e pela versão; release/contratos instalados foram lidos, e as 27 verificações de integração foram repetidas em laboratório novo com a 0.5.0. Nenhuma alteração nesse pacote foi feita por esta entrega. A captura imediatamente anterior à instalação final já contém a 0.5.0 e coincide com o estado posterior.

Pedido Core 349 continua consumindo o SDK existente para nome de campanha. Pedidos Core 348/350/351 e a atualização documental Google 0.24.0 não exigiram mudança adicional no Meta. Os contratos meta-ads-reader/1.0.0, meta-ads-monitoring/1.0.0 e instagram-message-erasure/1.0.0, as 47 entradas públicas, políticas de concessão e retenção permanecem. Arquivos dos SDKs, Messaging, MessagePrivacy, Retention e input-schemas.json são idênticos aos da base; diagnóstico de saída é aditivo.

Nenhum novo pedido técnico a outro mantenedor foi identificado no escopo verificado; portanto, não foi emitido arquivo de impacto nesta rodada. Esta conclusão não encerra trabalho de outro responsável nem substitui o aceite real da frota. LinkedIn não sofreu modificação nem regressão observada nos testes de convivência; suas operações remotas não foram re-homologadas.

## Mudanças por pedido e evidência

**25(a) — orçamento e diagnóstico.** Corrigida a herança do contador/prazo estático de Http no despacho das agendas Ads/dataset. A 0.16.0 consultava o fuso da conta antes de alocar orçamento para essa fase; com contador esgotado ou prazo vencido, falhava antes de gerar o job, mesmo sem fila executável. Os dois caminhos foram reproduzidos na base, sem chamadas à Meta. Isso comprova a causa reproduzível no código; não reconstrói o estado histórico das execuções de produção relatadas pela frota.

Na 0.17.0, despacho e página recebem orçamento próprio: 40 chamadas/25 segundos, respeitando o prazo de 22 segundos do passe do worker. Não existe quota diária local por conexão/agenda. As chamadas são contabilizadas ao chegar ao transporte, não em recusas locais de quota. Health e list-schedules expõem limite, consumo observado, restante, início/prazo, motivo, primeiro bloqueio e próxima reposição estimada. A estimativa depende de execução efetiva do worker. Quota remota por conexão/Retry-After aparece separadamente; saldo completo do fornecedor não medido fica null.

**25(b) — prioridade.** As últimas coletas de agendas habilitadas entram antes dos backfills, inclusive quando as primeiras 20 posições da fila já estão ocupadas por cargas antigas. O trabalho restante usa capacidade disponível, com seleção limitada, locks e checkpoint preservados. Não inicia novo job depois do segundo 19 do passe. Jobs pausados permanecem pausados; falhas locais recuperáveis aguardam cinco minutos e não são definitivamente pausadas apenas por ultrapassar seis tentativas. Carga contínua de agendas pode reduzir a capacidade retroativa; não há garantia de prazo de conclusão do backlog.

**25(c) — alerta.** Primeiro bloqueio local é preservado entre tentativas. Duração estritamente superior a 86.400 segundos gera schedule_budget_exhausted; o mecanismo existente reserva recibo persistente e tenta e-mail ao admin_email, sem duplicar tentativa enquanto ativo. Health/list-schedules não enviam nem coletam. Página persistida com progresso ou erro de outra natureza encerra esse bloqueio específico. Aceitação por wp_mail não comprova entrega na caixa postal.

**Aceite funcional sintético.** Três agendas diárias campaign/adset/ad concluíram antes de 24 cargas antigas, com last_success_at atualizado e ontem no fuso da conta no histórico. Backfills avançaram, preservando cursores; um job pausado não mudou. Core leu a linha diária recém-coletada e seu nome de campanha pelo SDK local; revogar o grant bloqueou a leitura. Nenhuma concessão foi criada no WordPress compartilhado.

## Instalação, testes e prontidão

**395 verificações aprovadas na candidata**, contabilizadas por execução/ambiente, mais **2 reproduções aprovadas da falha da base**. Não são 397 casos exclusivos. Build repetido produziu o mesmo SHA-256; lint de 33 arquivos PHP; runtime do fonte idêntico ao instalador. Principais suítes finais:

| Suíte | Verificações aprovadas |
| --- | ---: |
| upgrade | 12 |
| current-smoke | 36 |
| budget | 29 |
| corefresh | 5 |
| coreads0170 | 46 |
| coremonitor0170 | 19 |
| core3490170 | 38 |
| integration0170 | 27 |
| review071 | 11 |
| release0130-clean | 44 |
| release0170-clean | 36 |
| minimum-smoke | 36 |
| minimum-budget | 29 |
| pd05-integration | 27 |

As suítes cobrem orçamento por chamadas e tempo; prioridade; recuperação após seis tentativas; bloqueio menor/maior que 24 horas; leitura sem efeitos; e-mail interceptado/deduplicado/recuperação; quota remota; concorrência real de locks MySQL; permissões; integridade; Ads nos quatro níveis e 30 dias; dados parciais; retenção; SDK/revogação; atividade/EMQ; transporte MCP e convivência. HTTP dos fornecedores e e-mails foram interceptados nos laboratórios; zero chamadas reais a fornecedores e zero e-mails reais enviados pelos testes.

Duas primeiras execuções de regressão falharam por condições do harness: release0130 ainda exigia literalmente 0.15.0, e release0170 encontrou incidente de dataset de outra suíte no mesmo laboratório. O primeiro teste passou a usar a versão explícita do laboratório; a suíte de monitoramento foi repetida em instalação limpa. As repetições finais aprovaram 44 e 36 verificações. O runtime não precisou de correção após esses achados de teste. As evidências iniciais e finais foram preservadas, sem contabilizar as execuções iniciais como aprovações.

Ambiente principal observado: WordPress 7.1.4, PHP 8.3.36 de 64 bits, MySQL 8.4.11. Piso próprio: instalação limpa WordPress 6.4 e PHP 8.1.2-1ubuntu2.28 de 64 bits, com pacotes oficiais pinados por hash; 36 verificações de instalação/documentação/REST e 29 do Pedido 25 aprovadas. Na versão 6.4 sem Abilities API nativa, REST e funções próprias operaram; não se presume integração MCP nativa nesse piso. Ambiente final integrado e mínimo sem erros registrados do pacote.

O instalador final foi instalado por upload-base64 no Site-Teste, de 0.16.0 para 0.17.0, ativo antes/depois. Operação 4525e0006373760d69439fd91969b3ca; pré-imagem nativa 58f389041ab8db3f50446b50. Probes de / e /wp-json/ retornaram HTTP 200 antes/depois, com bypass de cache. A ativação da troca foi silenciosa, em processo independente; a instalação limpa com activation hook foi exercitada nos laboratórios. Probes técnicos não comprovam prontidão comercial.

Documentação pós-instalação: 28 documentos/31 páginas lidos por meta/documentation, inclusive input-schemas.json paginado em quatro partes, usando expected_revision. Todos os bytes e SHA-256 correspondem ao pacote 0.17.0. Descoberta final: 47 operações, todas 0.17.0, sem habilidades temporárias. Health final: state=ok, storage_ready=true, crypto_ready=true, zero conexões/zero agendas no compartilhado, sem incidentes. Portanto, prontidão estrutural comprovada; prontidão para coletar ativos reais não comprovada neste site sem conexão.

Foram removidos cinco laboratórios (14, 101, 14, 14 e 101 tabelas exclusivas respectivamente), todos com zero tabela restante, diretório e manifesto eliminados. Controlador/bundle temporários foram excluídos com hash esperado e backup nativo. Nenhum banco compartilhado foi apagado.

## Banco, retenção e reversão

Sem DDL/migração de tabela nesta versão; schemas de registros 2 e histórico 1 preservados. Novos campos de orçamento são aditivos em registros cifrados e só aparecem nas execuções seguintes. Não há backfill de consumo inventado, limpeza de dados ou troca automática de credencial, seleção, grant ou pausa.

Na atualização isolada, 13 registros e quatro linhas históricas foram preservados byte a byte, incluindo ciphertext, políticas unlimited e finite explícitas, agenda habilitada, quatro eventos de mensagens, relatório Ads/dataset e grant de monitoramento. Após a instalação compartilhada, dois registros de negócio, histórico vazio, sete opções Meta e configuração Core de monitoramento conservaram seus hashes. Auditoria técnica é excluída do digest de negócio; registrar chamadas administrativas é comportamento existente.

Todos os cinco acompanhantes mantiveram versão, ativação, quantidade de arquivos e digest entre as capturas imediatamente anterior/posterior à instalação. A única mudança externa observada durante a rodada inteira foi Pipedrive 0.4.0 → 0.5.0, tratada acima. Runtime Meta instalado: 65 arquivos, árvore SHA-256 bf530cd149e42eb214826fa6e6e855ced4b46e4c1800a6980b5aaf37cbae05cb, exatamente igual ao instalador.

Rollback: preservar banco, salts/chaves, concessões e recibos e repor somente o instalador-base 0.16.0 ou a pré-imagem nativa identificada. Campos aditivos podem ficar; a base os ignora, mas também volta ao defeito de orçamento herdado e à seleção antiga. Rollback de arquivos não desfaz coletas/e-mails já realizados. Não apagar recibos para repetir efeitos. Desativação/desinstalação preservam dados. Não voltar a versões anteriores à 0.12.0 com mensagens habilitadas.

## Pendências e responsáveis

- **Frota/operador dos sites reais:** instalar o ZIP validado em korvena.com.br/ctooffice, conferir permissões/credenciais e observar três agendas atualizando last_success_at e ontem no histórico/Core com retroativos elegíveis. As seis pausas deliberadas relatadas no pedido não são desfeitas automaticamente; retomada exige controle explícito com revisão atual. Produção não foi alterada nesta rodada.
- **Operador de e-mail:** verificar entrega real ao admin_email em incidente operacional autorizado. Testes comprovaram chamada interceptada, recibo e deduplicação, sem envio real.
- **Mantenedor Meta:** acompanhar consumo e tempo sob latência/carga reais. Os limites são deliberados; uma página que exceda continuamente a janela continua exigindo diagnóstico/redução de recorte. O teste não é benchmark de grande frota nem garantia de SLA.
- **Dono/frota:** publicação dos artefatos e atualização de main seguem a governança existente. Nenhum push, publicação ou envio a terceiros foi feito.

Não há bloqueio técnico observado para a entrega. Aceite de fornecedor/frota permanece pendente; sem alegação de ausência absoluta de impacto fora das fronteiras testadas. Interface administrativa visual não foi alterada nem re-homologada por navegador nesta rodada; diagnóstico público foi validado via PHP/REST/MCP. APIs remotas Google/LinkedIn/Pipedrive e entrega de mensagens comerciais não foram exercitadas.

## Credenciais e segurança

Nenhuma credencial nova necessária, criada ou substituída no site compartilhado. Laboratórios utilizaram tokens sintéticos e prefixos privados; acesso ao banco existente ficou no servidor e não integra evidências. Não foram gerados contatos reais, gastos de anúncios ou mensagens reais. Autorização administrativa, transporte revogado, grants e isolamento por consumidor permanecem verificados. Não há segredo, cookie, banco de laboratório ou runtime binário nos artefatos.

## Arquivos finais e integridade

Somente wp-mcp-meta-fator3-0.17.0-instalador.zip é instalável. Raiz wp-mcp-meta-fator3/, basename e identidades preservados. Fonte tem raiz wp-mcp-meta-fator3-0.17.0-fonte/, código de build, runtime, testes, documentação, inputs, histórico, planejamento, evidências sanitizadas e este relatório interno. Nenhum ZIP contém outro ZIP. Histórico no fonte não representa reexecução de todas as suítes antigas.

| Arquivo | Bytes | SHA-256 |
| --- | ---: | --- |
| wp-mcp-meta-fator3-0.17.0-instalador.zip | 327384 | a360feff0bdb723c7f3c2a240b288bc1c3af917e851cb798d905e31a95b4162d |
| wp-mcp-meta-fator3-0.17.0-fonte.zip | 3546251 | 84fe2092cf2f5312dbd0609bdae795bee9a2dd4c9076a0118d4c3fa022bcb7ca |

Relatório externo final: wp-mcp-meta-fator3-0.17.0-relatorio.md. O fonte contém cópia anterior ao fechamento, explicitamente identificada, para evitar circularidade de hashes. Evidências primárias em evidence/suite-summary.json, budget.json, baseline.json, upgrade.json, corefresh.json, shared-integrity.json, documentation-integrity.json, install.json e discovery-final.json.
