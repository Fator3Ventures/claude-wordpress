# Entrega — Fator3 MCP LinkedIn 0.26.0

18/11/2026 · Base 0.25.0 → 0.26.0 · Pedido MCP LinkedIn 27(a–g). **Implementado, instalado e ativo no Site-Teste. Estado da entrega: com-pendencias para homologação operacional em produção.** Os dados de fornecedor e os destinatários do laboratório eram sintéticos. Não houve instalação ou rotação de credenciais em produção.

## 1. Origem e versões

Regras aplicadas: instrucoes-agentes-plugins-fator3.md e padrao-desenvolvimento-plugins-fator3.md, ambas revisão 5 de 02/11/2026, além do padrão do LinkedIn e da regra comum. Entradas em inputs/0.26.0. O pedido de 18/11 descreve o incidente em CTO Office; a reprodução do defeito foi independente, em WordPress descartável.

| Pacote | Referência efetiva na validação integrada e no Site-Teste |
|---|---|
| LinkedIn | 0.25.0, origem; 0.26.0, alvo |
| Site Core | 1.93.0 |
| MCP | 0.48.0 |
| Google / Meta / Pipedrive | 0.36.0 / 0.28.0 / 0.11.1 |

Mínimos declarados: WordPress 7.1.4 e PHP 8.3 de 64 bits. Laboratório: WordPress 7.1.4, PHP 8.4.27, MariaDB. Site-Teste: WordPress 7.1.4, PHP 8.3.36. Os hashes dos pacotes usados estão em tools/lab-release0260.example.json. O SHA-256 do instalador LinkedIn de origem é 81bc69ed098198b056d93549dd5fa0317adfef2edc0937d33cdd0d0c21f801bb.

## 2. Convivência e encaminhamentos

Foi considerado o impacto recebido do Core 1.93.0, revisão 2, e o relatório do MCP 0.48.0. Há um impacto emitido pelo LinkedIn para o Core: validação coordenada do e-mail, com diagnóstico, ensaio contra o receptor oficial e critério para aceite na frota. A solução funciona com o Core fornecido. O domínio de credenciais/concessões LinkedIn permanece no plugin; a autorização da sessão atual continua no MCP. Não foi identificado ajuste técnico para o MCP, Meta, Google, Pipedrive ou instalador da frota. Nenhum documento oficial ou distribuição de outro pacote foi alterado. O aceite de 24 h do pedido Core 423(e) pertence à rodada anterior; aqui há somente regressão dos hooks com o sensor.

## 3. O que mudou e como foi verificado

| Pedido | Resultado observável |
|---|---|
| 27(a–b): dono e leitura | O worker usa a conexão ativa, o ativo selecionado e um administrador vigente do site. O concedente e o transporte originais permanecem como registro de auditoria. Um segundo administrador leu o job e resultados de A e confirmou o SHA-256 de uma exportação anterior. Após revogar A, sem rebaixar o autor, a 0.25.0 negou o job a B, desligou a agenda e subiu a revisão; sob a 0.26.0, o mesmo cenário concluiu a coleta e preservou a revisão. |
| 27(c): atualização | Na atualização real da base, o usuário de A foi também rebaixado. A agenda ativa e a que estava parada por not_authorized rodaram, a pausa manual sem erro permaneceu, a carga pendente e uma carga parada pelo erro anterior concluíram. B leu métricas, cobertura, exportação pronta e outra pendente; retomou ainda uma exportação anterior com cursor e parte já gravados. A tabela legada cifrada ficou idêntica byte a byte. |
| 27(d): revisão de edição | Execuções, falhas e retomadas usam o controle interno de concorrência. A revisão exposta para editar agenda, inclusive na prévia de alteração da conexão, só avança na edição; “conexão pausada” voltou a bloquear a execução sem subir essa revisão. |
| 27(e): incidente de agenda | Falha de autorização, conexão ou credencial é publicada para o destino técnico. O teste verificou abertura, repetição, recuperação, fila sem Core e entrega em ordem quando o contrato voltou. Nenhuma chamada ao Slack. |
| 27(f): serviços | Lead Sync leu um lead após o rebaixamento. O teste de conversões verificou prontidão de aquisição e envio sintético de etapa na mesma condição. A renovação automática atualizou a geração da credencial mantendo o processo sem usuário logado; o diário de serviço passou a ser legível por outro administrador. Concessões desabilitadas, ativos alheios, recibos humanos privados e leitores sem capacidade continuam protegidos. |
| 27(g): credenciais | Token e refresh têm prazos independentes. Testamos as faixas 30/14/3, repetição, data desconhecida e extensão. Para dois tokens, seis aberturas e seis recuperações no destino técnico. O observador do Core estava ativo. A falha de renovação conserva o token, registra o motivo, usa espera entre tentativas e abre um único episódio de credencial. |

No painel da conexão, o texto e o rótulo distinguem o indicador visual configurável dos marcos de e-mail. Revistos guias de credenciais, operação, concessões, diário, acervo e migração. O índice do pacote expõe 53 documentos; os 53 foram lidos integralmente pelo MCP local em 63 páginas. No Site-Teste, os 53 hashes do índice batem com o ZIP e os manuais de credenciais, histórico e notas de versão foram lidos com a revisão esperada.

## 4. Instalação e prova da troca

| Cenário em WordPress | Resultado |
|---|---|
| Instalação limpa isolada / integrada | 136 / 142 verificações aprovadas, sem erros PHP do plugin |
| Atualização integrada / isolada com dados operados | 20 / 19 verificações aprovadas |
| Autorização de conversões / rotação de transporte para Lead Sync | 26 / 17 verificações aprovadas |
| Cron LinkedIn com WP Activity Log 5.7.0 | 44 verificações aprovadas |
| E-mail técnico | Transporte interceptado no limite de wp_mail, destinatário e ordem conferidos |
| Painel | DOM de wp-admin: agrupamento, texto, rótulo, limites e máscara da credencial. Não há nova evidência visual em navegador; Chromium não abriu o socket local necessário nesta execução. |

Os cenários descartaram suas bases e não adicionaram fixtures no site compartilhado. O diff das duas distribuições, os resultados por teste e o recibo remoto sanitizado estão em evidence/release0260. O verificador de instalador conferiu CRC, raiz, cabeçalho, manifestos e igualdade de todos os 100 arquivos com a árvore de fonte; a sintaxe PHP foi validada.

Em Site-Teste, o envio do ZIP com slug e SHA-256 esperados substituiu a 0.25.0 pela 0.26.0 ativa. Operação 4233223c202b5392ea9baa9e6e9ac15f; pré-imagem 7b3c41716f6e9a7778c75ce0. As sondas / e /wp-json/ retornaram 200 antes e depois. Em novas requisições: system/health saudável, criptografia e armazenamento prontos, nove verificações locais do autoteste aprovadas, história schema 2 com projeção pronta. O site tinha zero conexões, zero agendas e zero linhas históricas antes e depois.

## 5. Dados e recuperação

A atualização cria a projeção por site e reconcilia em lotes sem remover a tabela anterior. Em métricas repetidas entre partições, usa a observação mais recente da mesma identidade diária e conserva a primeira data. Enquanto incompleta, a consulta nova devolve migration_pending. Verifique site_projection_ready, site_projection e unmapped em linkedin/history-status. Se um recibo de cobertura legado não tiver métrica, página, job nem outra associação verificável ao ativo, ele fica cifrado no original, contabilizado à parte. Não é tratado como dado de outra conta.

Agendas e cargas antigas com pausa not_authorized são retomadas; pausas sem esse código são preservadas. A 0.25.0 podia conservar um código antigo mesmo depois de salvar uma pausa manual. Se isso ocorreu, essa pausa é indistinguível no registro e será retomada: confira list-schedules e reaplique apenas as pausas intencionais nessa condição. Não se exige recriar jobs, regravar concessões, reautorizar o LinkedIn ou substituir tokens. A perda real do domínio da conexão/ativo/concessão ainda exige correção. Eventual correção de código posterior exige nova versão.

## 6. Pendências e responsáveis

Frota/CTO Office: em janela autorizada, reautorizar o conector, retirar a concessão anterior e observar as quatro agendas ligadas e sem not_authorized, a execução seguinte, os consumer_grants prontos e a leitura de acervo anterior, sem regravação. Usar uma conexão autorizada para verificar datas reais dos tokens e o recebimento da abertura e da recuperação no e-mail técnico. Não houve envio comercial, OAuth real, entrega SMTP ou confirmação de caixa postal nesta rodada. A prova de runtime PHP 8.3 é a homologação no Site-Teste sem conta LinkedIn; a matriz funcional com dados foi executada no PHP 8.4.27.

## 7. Configuração do dono

Manter na integração o aplicativo, token e ativos já autorizados; pelo menos um administrador com manage_options e a concessão de negócio correta são necessários. No Site Core, configurar o e-mail em Avisos técnicos. Se faltar o destino ou o receptor estiver temporariamente indisponível, a entrega fica pendente. LinkedIn não escolhe destinatário substituto nem envia a Slack. Prazos adicionais expressamente configurados no Core permanecem aplicáveis.

## 8. Identidade dos arquivos

Instalador oficial: wp-mcp-linkedin-fator3-0.26.0-instalador.zip — 460375 bytes — SHA-256 607a7b432bcf974047cc648506087690ba46998aaf0dc931662f9ecadf2e02bd.

Fonte oficial: wp-mcp-linkedin-fator3-0.26.0-fonte.zip — 9854399 bytes — SHA-256 57a02b6d6f40df3796b9893d34254b1993071a937c6c05106dff22157eac2424. A cópia interna do relatório antecede o cálculo do hash do fonte.
