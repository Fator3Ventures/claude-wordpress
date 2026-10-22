# Entrega — Fator3 Site Core 1.47.0

Revisão 1 · 2026-10-22T19:09:57+00:00 · Rodada: implementação dos pedidos 284–287.
Slug: base-site-core-fator3 · versão/build: 1.47.0 · contrato administrativo 8.12.0.
Status: **com-pendencias de fornecedor e aceite na frota**. Implementação e homologação do Core concluídas no escopo testado. Perfil piso-padrao-3.6 (92 condições) mantido; 138 abilities; ciclo de 18 etapas.

## 1. De onde esta versão entra

Instalação nova ou atualização direta da **1.46.1**, última entrega aceita pela frota. O instalador-base imutável tem 2.185.721 bytes e SHA-256 2e834ba27728a32a22fa588cc05863d1d69ccc2e09b0c05e016d88404eaadc76; fonte-base 3.201.244 bytes, SHA-256 add385d393dca6afe7c095a73b0476369fee658d0eca0e29cc66a4b2bc0f92e0. Nenhuma intermediária é exigida. Os pedidos 274–283 já estavam aceitos; não foram reabertos nesta release.

Entradas: Pedidos — Fator3 Site Core de 22/10, anexos atuais dos quatro acompanhantes e padrão comum revisão 4 de 16/10. A implementação limita-se a 284–287 e ajustes indispensáveis de documentação, schema, migração e testes. Não altera plugins acompanhantes, formulários ou temas da frota automaticamente.

Validado: WordPress 7.1.3; PHP 8.3.6/MySQL 8.0.36 no laboratório e PHP 8.3.36 no Site-Teste; Chromium 153.0.0. Não há declaração de execução de matriz completa nas versões mínimas do cabeçalho.

## 2. Convivência e encaminhamentos

| Acompanhante | Versão examinada e ativa no teste | Resultado |
|---|---|---|
| Fator3 MCP | 0.26.1 | Instalação, descoberta, execução e documentação pelo MCP funcionaram |
| Fator3 MCP Google | 0.17.0 | Schema real de medição 1.0.0 validou o novo slot; sem mudança exigida |
| Fator3 MCP LinkedIn | 0.5.0 | Convivência aprovada; ainda não oferece o adaptador CAPI necessário |
| Fator3 MCP Meta | 0.4.1 | Ativo em conjunto; contrato existente preservado |

Também ativos no Site-Teste: WP Super Cache 3.1.4 e Yoast 28.7. As cópias de teste dos acompanhantes estão em companions/ no fonte; não entram no instalador. Não foram feitas chamadas comerciais para fabricar aceite.

| Destinatário com impacto relevante | Classificação / situação | Pedido | Documento |
|---|---|---|---|
| MCP LinkedIn 0.5.0 | acao-necessaria / aberto | Core 285; LinkedIn 8 | base-site-core-fator3-1.47.0-impacto-wp-mcp-linkedin-fator3.md, revisão 2 |
| Implantador, fonte atual não recebido | acao-necessaria / aberto | Core 286/287; complemento Implantador 21 | base-site-core-fator3-1.47.0-impacto-implantador-base.md, revisão 2 |

Os dois impactos nasceram no planejamento, antes da fronteira afetada, e foram atualizados com contrato e provas. O consumidor Core foi implementado sem aguardar o LinkedIn. Não se identificou consequência técnica que exigisse novo impacto para MCP, Google ou Meta; por isso não há documentos de simples aviso de versão. Os impactos são entregues ao dono, sem envio a terceiros.

## 3. Mudanças e evidência

| Pedido | Problema | Mudança | Prova e limite |
|---|---|---|---|
| 284 | Atividade do e-mail automático aparecia como histórico independente na eliminação | Prova HMAC de criação junto a atividade_id; exclusão somente do objeto próprio inalterado; IDs/tipos do histórico restante; cópia SmartBCC explícita; cancelamento serializado com trabalhador de e-mail | 39 verificações locais com API/SMTP simulados. Objetos legados sem prova e objetos alterados ficam para revisão. Aceite real em CTO Office pendente |
| 285 | LinkedIn somente no navegador, sem event_id comum | ID aleatório do servidor único e congelado; lintrk com ID/regra; consumidor CAPI, fila, códigos/HTTP/retry, prévia sem envio, diagnósticos e procedência honesta | 38 verificações do consumidor, oito em Chromium; schema Google 0.17.0; prévia administrativa no Site-Teste. Adaptador e aceite externo pendentes |
| 286 | Campo único dependia de JavaScript e hidden do tema | papel contato em text; presença/grupo; servidor reconhece e-mail ou telefone livre; original e classificação preservados; somente identidade válida nas integrações | 32 verificações locais e POSTs nativos no Site-Teste: e-mail, +5511912345678, abc inválido; empresa no fallback da segunda etapa. Migração do popup/tema da frota pendente |
| 287 | Confirmação interna saía por wp_die sem tema | Template WordPress e conteúdo principal, blocos, mensagem única, um botão Core WhatsApp com continuar_whatsapp; privacidade preservada | HTTP local após duas etapas e quatro confirmações no Site-Teste com cabeçalho/rodapé/blocos/headers. Página Segunda Opinião em CTO Office não foi alterada nem testada nesta rodada |

**Eliminação.** A prova de atividade é aditiva e só nasce na criação confirmada. Não fabrica prova usando o estado atual de registros antigos. O journal traz historico_restante com tipo/id, sem assunto ou texto. copias_externas.email_smart_bcc explica que o Core não tem ID individual da mensagem. A API Mailbox documenta exclusão de conversa inteira, não da mensagem isolada; não se apaga conversa cuja exclusividade não esteja comprovada. Contagem de mensagens independentes na pessoa continua protegida. concluida comprova os objetos autorizados, não o desaparecimento dessa cópia externa.

**Conversão LinkedIn.** f3base_conversoes_transporte admite linkedin=navegador|ambos, padrão ambos condicionado a partner_id e conversion_id configurados. Só novos formulários aceitos capturam a intenção; eventos antigos mantêm seu ID. A regra da resposta aceita prevalece ao HTML em cache. O registro congela evento e instante ms. Payload site-linkedin-conversion/1.0.0: e-mail normalizado SHA-256, li_fat_id observado, nome/sobrenome e empresa/cargo/país disponíveis; userInfo exige o par nome/sobrenome. Valor/moeda são opcionais pelo filtro confiável f3base_linkedin_valor_conversao; não são inferidos de texto do visitante.

A fila guarda estado, identidade local, referência opaca, datas, code simbólico e HTTP, sem payload/PII no journal. Recusa comprovada permite retry até 10 tentativas, máximo 90 dias; incerto não repete às cegas. Troca de conta/regra, consentimento, teste/homologação/spam, lixeira/eliminação e audiência excluída bloqueiam envio. Recuperação exige confirmação de não entrega e vínculo à regra original, sem transferência automática para provedor que aparece depois.

Nova ability f3base/linkedin-conversao-previa recebe record_id e exige manage_options **e** f3base_ler_leads. É prévia, inclusive de teste, sem enfileirar/enviar. medicao-contexto-ler mantém o schema público 1.0.0, mostra ambos/core_server e detalha bloqueio em linkedin_server_<motivo>. Gravação dos IDs pelo configurador registra procedência atual; datas diferentes no mesmo canal confirmado não geram falsa origem mista. Partner legado desconhecido precisa ser reafirmado pela frota com revisão esperada; não se inventa autoria histórica nem se esconde ausência de prova.

**Contato e confirmação.** papel contato aceita somente text na etapa 1; obrigatório/grupo exigem preenchimento, sem recusa de formato. Um contato preenchido prevalece sobre hidden legado. O original fica em campos e contato_normalizacao; telefone tem valido/sem_ddd/invalido. Campos separados continuam compatíveis. Confirmacao_url deve ser página pública interna com the_content normal; referência dura 10 minutos, ligada ao caminho. Expiração retorna 410 e caminho divergente 404. Mantém DONOTCACHEPAGE, private/no-store, noindex/nofollow/noarchive e no-referrer. Só WhatsApp HTTPS permitido recebe botão; botões editoriais do autor não são removidos.

Referências primárias consultadas: [LinkedIn Conversions API schema](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api-schema?view=li-lms-2026-07), [LinkedIn Conversions API](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api?view=li-lms-2026-07), [Pipedrive Mailbox](https://developers.pipedrive.com/docs/api/v1/Mailbox).

## 4. Instalação e prova da troca

Instalador separado, raiz única base-site-core-fator3. Instalar com expected_slug=base-site-core-fator3 e expected_sha256 da seção 8. Publicação raw não realizada; a URL final será a da publicação autorizada pelo dono. No Site-Teste, plugins/upload recebeu o arquivo local transferido e o mesmo SHA-256 final. Operação de pacote 4be74070573ccd629fb9aff8078dee1c; backup de arquivos 2cd58d497e8202eb426aabe4. HTTP inicial e REST responderam 200 antes/depois, com bypass assinado de cache.

Prontidão: executar f3base/saude-ler com {} e verificar atualizacao.versao=1.47.0, estado=concluida, falhas=0, 18 etapas e finalizacao_em preenchido. Observado no Site-Teste: ciclo b7ddcf1a-940c-403e-9a61-a07a1f7c6143, finalizacao_em=1792695356; Core operacional, pausa false, geração 6. O código novo só verifica as colunas aditivas depois da etapa integracoes; instalação limpa e upgrade passaram no instalador final.

| ID | Ambiente / cenário | Resultado | Evidência e limite |
|---|---|---|---|
| L1 | Lint / pacote | 229 arquivos PHP válidos; ZIP determinístico | installer.json; PHP 8.3.6 |
| L2 | WordPress novo, Core isolado | 18 etapas, estrutura pronta, finalização, repetição idempotente | native-cycles-1470.json; espera acelerada só no estado descartável |
| L3 | Upgrade nativo 1.46.1 → 1.47.0 | Mesmo ZIP final; dados/opções/segredos/callback/cursor preservados | native-cycles-1470.json; novas requisições |
| L4 | Funcionalidades 284/285/286 | 39 / 38 / 32 verificações aprovadas | pipedrive-1470.json, linkedin-1470.json, forms-1470.json; fornecedores simulados |
| L5 | Bundle JavaScript real | Oito verificações, nenhum erro JS | linkedin-browser-1470.json; Chromium 153 |
| L6 | Confirmação no tema | Duas etapas e WhatsApp, blocos e headers; com/sem botão | confirmation-fixture-1470.json e confirmation-http-1470.json |
| L7 | Documentação e convivência | 79 e 11 verificações aprovadas | docs-1470.json e coexistence-1470.json |
| R1 | Troca e ciclo Site-Teste | Ativo, 18 etapas, zero falhas | site-teste-1470.json |
| R2 | POST HTTP nativo sem JS | Quatro envios aceitos; original/classificação/identidade confirmados no banco | site-http-1470.json, site-teste-1470.json; campos de etapa 2 juntos no fallback |
| R3 | LinkedIn prévia administrativa | Mesmo ID e ms, SHA256_EMAIL/li_fat_id e userInfo; envio false, trafego_suprimido | site-teste-1470.json; IDs fictícios só no callback, sem alterar IDs do site |
| R4 | Limpeza | Cinco contatos eliminados pela ability; zero páginas, leads e filas ativas temporárias | site-teste-1470.json |

Documentação instalada descoberta e lida integralmente por f3base/documentacao-ler, arquivo/linha/limite, versão 1.47.0 e proxima_linha null. RELEASE-1.47.0.md (41 linhas): SHA-256 b89e02682d9588cf783af34443f399889a3ea163560083ee7ef055f8e9bf877c. AGENTES-1.47.0.md (11 linhas): bf2b68f67e37acb024d0a205e625f370c001a3e554bd7e4e7e9f276c92e73066. Índice DOCUMENTACAO.md (40 linhas): 9d18041c55b0462f94bc1a31c067f4ed20d7625d816dd1f2d48d793e07012ac6. Schema e catálogo gerados do runtime acompanham o instalador.

Estado final: Core 1.47.0 e quatro acompanhantes nas versões da seção 2, ativos. Dois formulários temporários e política de teste restaurados às revisões originais; duas páginas, MU fixture, cron de teste e ZIP remoto removidos. Registros eliminados por f3base/leads-eliminar-registro; diário de conversão cancelado sem payload preserva auditoria. Referências de confirmação expiram em 10 minutos. Backup privado e logs administrativos de operação permanecem no servidor. Piloto de cache 20 páginas/h e 7 dias preservado. Nenhum dado ou configuração alheia foi removido.

## 5. Banco e volta de versão

Adições: f3base_email_novo_lead.atividade_prova longtext anulável e f3base_conversoes_servidor.http smallint unsigned padrão 0. Schema atualizado na etapa integracoes, verificado no fechamento; ciclo continua com 18 etapas. Nova finalidade linkedin usa o journal existente e os dados originais do lead. Sem backfill de prova de criação nem transferência de eventos históricos.

Backup privado completo antes da troca, após preparar/drenar o Core: artefato 60f916bda103e39176b0aa3d65a0f39f, 22.627.850 bytes, SHA-256 d84b3a4289b7e34d33de717206fcd029fec3e283f21ebf3eb9ea64c4534aab18. O conteúdo do banco não foi incluído na entrega. A operação foi retomada com guarda atual antes da troca, e o Core terminou sem pausa.

Para reversão, preparar/drenar o Core e usar backup de arquivos/banco consistente, conferindo filas e efeitos posteriores antes de restaurar. Voltar somente arquivos não remove colunas nem desfaz exclusões, mensagens ou conversões externas. Não substituir banco antigo sobre filas vivas; reconciliar resultado incerto. Google e MCP possuem procedimentos próprios de recuperação. Não foi executado rollback no Site-Teste.

## 6. O que permanece pendente

1. **Pipedrive 284:** homologar em CTO Office, com contato de teste e e-mail automático, a remoção do lead, pessoa, nota e duas atividades. A prova local passou; não foi enviada mensagem SMTP nem criado objeto comercial real nesta rodada. Registros antigos sem prova e cópia SmartBCC podem exigir revisão; não declarar exclusão de mensagem que a API não comprovou.
2. **LinkedIn 285:** responsável pelo plugin entrega adaptador/concessão CAPI; aplicativo obtém rw_conversions, acesso de conta e regra com fonte API. Com ordem do dono, frota homologa regra 31692506 em CTO Office e deduplicação real no Campaign Manager. A procedência do partner legado deve ser reafirmada com a revisão corrente.
3. **Implantador/frota 286/287:** migrar schema e popup/contato.js somente nos sites com Core novo; testar o popup real e a confirmação Segunda Opinião em CTO Office. Fonte atual do Implantador não foi recebido; não há teste afirmado sobre ele.
4. Publicação e implantação na frota são decisão do dono. Não foi feito push, alterado repositório público nem instalado Core em produção. Pendências históricas de conta/aparelho/tempo do estado da frota continuam fora desta rodada.

Nenhuma falha conhecida permaneceu nos testes do Core descritos acima. Estas pendências externas impedem declarar os aceites comerciais completos, sem bloquear a entrega do consumidor e dos demais pedidos.

## 7. Credenciais e configuração do dono

Nenhuma nova credencial é cadastrada no Core. Configuração de transporte e IDs permanece em Fator3 Site Core/Medição; conexão, conta, regra, token manual, escopos e concessão ao consumer site-core-conversions são responsabilidade do MCP LinkedIn. Não reutilizar autorização de Lead Sync. Testes e homologação sempre suprimem conversões comerciais.

Para campo único: em f3base_formularios, tipo=text/papel=contato; obrigatório ou grupo exigir_um_de, país do telefone e mensagens.continuar_whatsapp. Publicação/configuração requer administrador e revisão esperada. Prévia com dados do contato exige também f3base_ler_leads. Nenhum segredo, dump ou dado pessoal real está nos pacotes/evidências; valores de teste são identificados como sintéticos.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | base-site-core-fator3-1.47.0-instalador.zip | 2195818 | dd16cb720e57c2d448e78a744eb0fd761d6aff04aadeeed8309b6b5003b417c1 |
| Fonte | base-site-core-fator3-1.47.0-fonte.zip | 4264186 | 7082123036ee6470c18407f5da29a9969b96617ebf4b7dbcb106ac9041c18c8c |

O instalador contém apenas o plugin, assets, dependências próprias e documentação. O fonte tem uma raiz, work/plugin com o mesmo runtime, ferramentas de reprodução, acompanhantes de teste, evidências saneadas e histórico da base; nenhum ZIP aninhado. Fonte não é instalável.

Relatório externo canônico. A cópia no fonte é anterior ao fechamento e não tenta conter o próprio hash. Complementos entregues: impactos LinkedIn e Implantador, ambos revisão 2; plano da rodada incluído no fonte. Evidências antigas não foram contadas como reexecução desta versão.
