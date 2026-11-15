# Entrega — Fator3 Site Core 1.87.3

Revisão 1 · 14/11/2026, horário de Brasília · Implementação dos Pedidos core 407–412 e adequação ao padrão visual do Pedido core 404. Situação da entrega: **com-pendencias** de aceite na frota. O instalador está ativo e pronto no Site-Teste. Os critérios por ambiente e o responsável pela validação posterior aparecem na seção 7.

## 1. Bases aceitas

Instalação em WordPress limpo ou atualização direta da **1.86.0**. Os sites que já executam a **1.87.0**, **1.87.1** ou **1.87.2** podem atualizar diretamente. As três versões intermediárias serviram à homologação desta rodada. A frota instala apenas a 1.87.3.

A base oficial de desenvolvimento foi o fonte 1.86.0, SHA-256 `9c27ba8ff701238850b094b13a5df41cf47cd619076e75016c6b62736a9fb62e`, com instalador `0864ad1ef02caf6102e8f6294b42816ab7bd884081c1a3518ab08fc20b9e7f46`. O insumo disponível foi um ZIP de fonte. O mínimo de execução é **WordPress 7.1.4 e PHP 8.3 de 64 bits**, em instalação única. WordPress 7.1.4 foi exercitado com PHP 8.3.6 e 8.4.24 em laboratório e 8.3.36 no Site-Teste.

Foram lidos integralmente `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, revisão 5 de 02/11/2026. A rodada incorporou também a Regra comum e o Padrão de entrega — Fator3 Site Core fornecidos pelo dono, incluindo a diretriz visual de 14/11/2026 e a distribuição dos três arquivos. O fonte inclui os pedidos e as duas referências recebidas em `reference/`.

## 2. Configuração e catálogo de operações

| Contrato | Valor comprovado |
|---|---|
| Contrato administrativo | 8.41.0 |
| Perfil de piso vigente | piso-padrao-3.6 |
| Opções operáveis | 103, contadas no catálogo executável com operavel verdadeiro |
| Abilities f3base/* | 196, geradas do registro de WordPress |
| Variação desde 1.86.0 | +1, f3base/aplicabilidade-ler. Nenhuma remoção. Total anterior 195. |
| Variação desde 1.87.0, 1.87.1 e 1.87.2 | Mesmo conjunto de 196 nomes |
| Acesso | Configuração, saúde, documentação e aplicabilidade exigem manage_options. Os caminhos delegados de Contatos e Formulários conservam as capacidades específicas existentes. |

## 3. Convivência e ordem de troca

No Site-Teste estavam ativos Fator3 MCP 0.45.0, Google 0.35.0, Meta 0.26.0, LinkedIn 0.23.0 e Pipedrive 0.10.0. Somente o Core foi atualizado. O MCP descobriu e executou a operação nova. Os leitores Google Ads, Meta Ads e LinkedIn foram carregados em WordPress. O registro local Google e o contrato LinkedIn foram confirmados. O Meta indicou configuração pendente. Em instalação limpa, o Core executou com os acompanhantes ausentes.

O contrato de configuração e as APIs de fornecedores preservam seus schemas. A frota deve ler o compacto pelas novas contagens e consultar a rota de detalhe indicada. Essa mudança operacional e a referência de uso seguem neste relatório e no instalador. No escopo de MCP, Google, Meta, LinkedIn, Pipedrive e Implantador, a entrega dispensa alteração de código ou release coordenada dos acompanhantes.

## 4. Mudanças, pedidos e evidências

| Pedido | Implementação | Evidência |
|---|---|---|
| Pedidos core 404 | Selo com versão, identificação do pacote, grupos e subabas com quebra de linha, faixa paginada de Contatos e menu Medição. Conexões separa canais e CRM de operação e acesso. As três telas de Operação têm navegação comum. | Chromium com WordPress e registros sintéticos. 240 capturas a 360, 768 e 1440 px. Em 360 px, Avisos e Qualidade passaram de 553 e 394 px de largura de página na 1.87.2 para 360 px na 1.87.3, com rolagem restrita às tabelas. As 13 interações verificam paginação, CSV, histórico, filtros, lixeira, menu e compatibilidade do endereço antigo. |
| Pedidos core 407 | O histórico de e-mails depende de f3base_email_historico.ativo e f3base_pipedrive.ativo. | Cinco perfis reproduzidos. Mesma mensagem, participantes e thread correspondente produziram confirmado com transporte simulado. Thread de outro lead manteve a conferência aberta. No Site-Teste a regra retornou verdadeira e o hook foi observado. |
| Pedidos core 408 | A nova ability f3base/aplicabilidade-ler e a seção de como-usar descrevem opções, condições, revisões, efeitos, eventos e esperas. | 48 regras exercitadas. Conferência de resultado e agenda nos perfis A–E e teste de permissão administrativa. |
| Pedidos core 409 | 123 chamadas ao leitor comum em 53 arquivos. Campos JSON nulos, já decodificados e inválidos são tratados na leitura. Os três campos cifrados mantêm autenticação. link_destino continua texto. | Exercitados os 11 nomes do pedido, projeções de tela, relatório e tarefa, erros de forma e recibos. Auditoria estática de chamadas diretas em linha do banco e inspeção de variáveis intermediárias. |
| Pedidos core 410 | A estimativa consulta quantidade e tamanho dos campos no banco antes de materializar. A leitura usa lotes de 32 para medição própria e ofertas, reserva memória e limita a população a 8.000 linhas. | No Site-Teste, resultados retornou dados para 1 e 7 dias. As 21 visões a 90 dias responderam limite_memoria. Em resultados, a previsão foi 156.268.032 bytes para 37.748.736 disponíveis. Em laboratório o painel e a API recusaram uma linha sintética de 4 MiB sob limite de 128 MiB. |
| Pedidos core 411 | Os compactos consultam contagens e mostram onde ler cada detalhe, com recibo de prontidão. | No Site-Teste como-usar caiu de 76.540 para 1.958 bytes e saúde de 3.025 para 1.958 bytes. Medição no objeto de dados MCP em JSON UTF-8, com metadados da chamada. Teto do pedido 16.384 bytes. |
| Pedidos core 412 | As seis filas mantêm a passagem recorrente, deduplicam a forma avulsa antiga e antecipam somente quando o trabalho tem prazo anterior. | Em cada trabalhador, 12 passagens ociosas preservaram a agenda. Duas solicitações urgentes geraram uma antecipação e mantiveram a recorrência. A leitura de cron por gancho do Site-Teste está em evidence/1873/site-teste.json. |

### Resultado por perfil

A 1.86.0 ainda não publicava a rota. A coluna anterior foi reconstituída da condição de seu fonte e das opções do pedido. A coluna 1.87.3 foi lida da rota em WordPress com os cinco perfis reproduzidos.

| Perfil | Site de referência | Histórico 1.86.0 | Histórico 1.87.3, revisão 2 |
|---|---|---|---|
| A | awnventures, fator3.com.br, twinia, engagia, conselar, fator3ventures, fator3capital e fator3grupo | Inativo | Ativo |
| B | korvena.com.br | Ativo | Ativo |
| C | ctooffice.com.br | Inativo | Ativo |
| D | desenvolvimentodesoftwares.com.br | Inativo | Inativo |
| E | Site-Teste | Inativo | Ativo |

As seis mudanças de agenda introduzem revisão de agenda 2 para as políticas correspondentes. A condição comercial de entrada de cada fila é preservada. Com aptidão local, wp_mail, Pipedrive e notificações LinkedIn passaram a cinco minutos. E-mail de novo lead e conversões passaram a uma hora, inclusive nos perfis com a política de nova entrega desligada. A recuperação CAPI é diária com a estrutura disponível.

| Trabalhador regular | A | B | C | D | E |
|---|---|---|---|---|---|
| Pipedrive | Sim | Sim | Sim | Não | Sim |
| Notificações LinkedIn | Não | Não | Sim | Não | Não |
| Novo lead / conversões | Sim | Sim | Sim | Sim | Sim |
| Recuperação CAPI | Com tabela pronta | Com tabela pronta | Com tabela pronta | Com tabela pronta | Sim, observado |
| wp_mail | Depende da opção de transporte | Depende da opção de transporte | Depende da opção de transporte | Depende da opção de transporte | Sim, observado |

O inventário das opções ativo que definiu os perfis não determina email_site.wp_mail_pela_caixa. O valor concreto é divulgado pela regra wp_mail. A atividade de anúncios e o estado do CRM não comprovam disponibilidade de um fornecedor. A rota distingue a política do site, os pré-requisitos adicionais expostos e os eventos realmente observados.

## 5. Instalação e prova de prontidão

Use o instalador com a pasta única `base-site-core-fator3/` e o arquivo principal de mesmo slug. Para a distribuição, a frota compara os dois SHA-256 da seção 9, publica instalador, fonte e relatório na raiz de main e confere o instalador servido por HTTP antes do primeiro uso. A rota de instalação é `plugins/upload`, com `expected_slug=base-site-core-fator3`, `expected_sha256=d8f8c05aa3220e5dea01723211718932ca54b13e644d70cdb95dc51ccc760fed`, ativação e sobrescrita da versão anterior. Ao efetivar a troca da frota, os três arquivos anteriores saem do main e continuam no histórico. [Endereço do instalador após a publicação pela frota](https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/base-site-core-fator3-1.87.3-instalador.zip).

Na homologação, o ZIP foi servido temporariamente pelo próprio Site-Teste. O download foi comparado byte a byte antes de `plugins/upload`. O recibo `e5ec8fc6eb855250900b2f9d79c05222` confirmou a troca de 1.87.2 ativa para 1.87.3 ativa. As sondas de / e /wp-json/ obtiveram HTTP 200 antes e depois, com desvio de cache verificado. O pacote temporário foi removido pelo hash, com ausência confirmada.

A confirmação depende da execução do ciclo e de uma nova passagem do executor. Logo após a instalação pode aparecer atualizacao_pendente, em_andamento ou aguardando_confirmacao. A leitura de `f3base/como-usar` com `compacto=true` deve mostrar os quatro campos abaixo. No Site-Teste transcorreram **7 segundos** entre o início gravado do ciclo e a confirmação. Esse intervalo depende da agenda e do volume local.

| Campo | Observado no Site-Teste |
|---|---|
| versao_alvo | 1.87.3 |
| estado | concluida |
| falhas | 0 |
| confirmada_no_executor_em | 1794705377 · 15/11/2026 01:16:17 UTC |

Foram comparados os 989 arquivos do runtime e executado lint em 607 PHP nas duas versões de PHP de laboratório. Cada um dos cinco caminhos (limpa, 1.86.0, 1.87.0, 1.87.1 e 1.87.2) passou por 263 verificações com o ZIP final. As capturas, os índices por largura, as leituras de contrato, o comprovante de preservação e os testes reproduzíveis acompanham o fonte. Na área administrativa foram testadas navegação, recuperação e retomada. Os cenários de navegador utilizaram contas e dados sintéticos em Chromium.

O índice, o guia de agentes, as notas correntes e o guia de painel foram lidos por `f3base/documentacao-ler` no Site-Teste e conferidos com o pacote. Para repetir, indique arquivo, linha e limite e continue por proxima_linha. A sondagem de saúde retornou saudável. A leitura dos registros de fatal após a troca retornou 0 grupos entre 2026-11-15T01:15:55+00:00 e 2026-11-15T01:18:23+00:00. O diagnóstico específico de robots.txt reportou **degradado**. Entrega pública aguardando verificação atual. O WP-Cron verifica automaticamente e atualiza este diagnóstico; sem execução do cron a confirmação permanece pendente.

## 6. Banco, recuperação e correção por nova versão

Opções de configuração novas: zero. Tabelas novas: zero. O executor registra revisão, etapa e confirmação no estado de instalação existente. A reconciliação converte as ocorrências antigas dos seis ganchos e grava o estado de cron. Recibos, opções e filas mantêm suas identidades. As 20 etapas observadas foram:

retencoes_mensais, linkedin_integracoes, identidade_pipedrive, intencoes_estrutura, consentimento_capi, leads_analise, formularios_tentativas, integracoes, conversoes_conteudo, editorial, acervos, replay_cedo, padroes, diagnosticos_configuracao, manutencao_local, pasta_privada, verificacao, agendas, perfil_publico, ativos_publicos.

Uma passagem interrompida retoma pelo estado persistido e requer confirmação do executor. A atualização direta e o caminho do patch preservaram os 55 contatos sintéticos e o SHA-256 agregado de seus identificadores e hashes de payload, `0149dca7c5e04e77d08606c6677a902f3bd9a6f7f1434ae633ef38a0730c5957`. O instalador no Site-Teste registrou uma cópia dos arquivos substituídos. A volta de arquivos não desfaz ajustes de agenda, dados ou opções já escritos. Para dados, vale o backup do banco. A política do projeto exige nova versão para correções após instalação.

## 7. Aceite pendente em produção

- **407 e 408 — frota.** Em CTO Office conferir o próximo e-mail real até confirmado. No portal de desenvolvimento, observar a ausência de gancho e espera indevidos. Comparar as regras nos 12 sites. A matriz tem cinco perfis simulados e a leitura real do Site-Teste.
- **410 e 411 — frota.** Repetir as 21 visões de 90 dias e a consulta de fatais em ctooffice.com.br, e medir os compactos em cada site. A atribuição do fatal histórico a esta rota permanece provável. O registro anterior não identifica sua visão nem o período.
- **412 — frota.** Após a instalação no CTO Office, observar ao menos 24 horas com cron HTTP e CLI. O critério é menos de dez registros could_not_set por dia nos seis ganchos, com esperas vazias e sem evento vencido. O teste de idempotência local mede gravações controladas.
- **Fornecedores e interface.** A rodada não realizou envio comercial nem criou lead em conta real. A configuração do leitor Meta permaneceu pendente. Safari, Firefox e aparelhos físicos não foram homologados. A produção depende da distribuição da frota.

## 8. Credenciais

O dono não precisa cadastrar segredos novos nesta atualização. As chaves vigentes de CRM, e-mail e mídia continuam nos campos correspondentes em Site Core → Configurações → Conexões e entregas. A ativação de conta ou de envio continua sob decisão do dono.

## 9. Identidade dos arquivos

| Artefato | Nome | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [base-site-core-fator3-1.87.3-instalador.zip](https://chatgpt.com/library?file_id=libfile_fde3_f-cf3f226d960481919057fc4ec24cf073_32706b9c47908191baafe72f89b6caee&account_id=personal) | 4.505.176 | `d8f8c05aa3220e5dea01723211718932ca54b13e644d70cdb95dc51ccc760fed` |
| Fonte | [base-site-core-fator3-1.87.3-fonte.zip](https://chatgpt.com/library?file_id=libfile_fde3_f-3066b4e1aefc81918d060fb0f82ae2a7_32706b9c47908191baafe72f89b6caee&account_id=personal) | 76.451.932 | `584c297fc8ca3f63fc4549455d236dbdc58fb115aadc4b76fa9038e417e500d0` |

Relatório canônico externo: `base-site-core-fator3-1.87.3-relatorio.md`. A cópia interna em `RELATORIO-PRE-FECHAMENTO.md` identifica o instalador. O tamanho, o hash e o link do próprio fonte são inseridos no relatório externo depois de empacotar. O fonte tem pasta própria e não contém o instalador nem ZIP aninhado.
