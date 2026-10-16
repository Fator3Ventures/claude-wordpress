# Entrega — Fator3 Site Core 1.34.0

Revisão: 1 · Data/hora: 2026-10-16T13:20:00-03:00 · Rodada: implementação e validação
Slug: `base-site-core-fator3` · Versão/build: `1.34.0` / `1340-3d3d3ffa0840`
Status: **com-pendencias**. Implementado, empacotado e instalado no Site-Teste; homologação externa e parte da matriz de aceites permanecem abertas. Não significa liberação integral da frota.

## 1. De onde esta versão entra

Aceita instalação nova e atualização direta da base 1.33.0, sem intermediária nem trava global por acompanhante. Base recebida: `base-site-core-fator3-1.33.0(5).zip`, bytes originais, SHA-256 `de427cb219be769d9e44ae9aaf5e6f31055990b3d8f9b8664ac0faa596f61364`.

Implementação orientada pelo plano revisão 4, especificação do consumidor LinkedIn revisão 3 e normas comuns revisão 4. Os arquivos integrais estão em `plugin/docs/PLANO-1.34.0-REVISAO-4.md`, `ESPECIFICACAO-LINKEDIN-REVISAO-3.md` e `NORMA-*.md`. A regra nova de impactos relevantes prevalece sobre a menção antiga a cinco impactos no plano.

Ambientes efetivamente validados: laboratório WordPress 7.1.2, PHP 8.3.6 de 64 bits, MySQL 8.0.46; Site-Teste WordPress 7.1.3/PHP 8.3.30. Os mínimos herdados do cabeçalho (WP 6.4/PHP 8.1) não receberam uma nova matriz nesta rodada; sua comprovação permanece pendente. Multisite não foi validado.

## 2. Convivência e encaminhamentos

| Destinatário | Versão examinada | Classificação / situação | Ticket | Impacto individual / revisão |
|---|---|---|---|---|
| Fator3 MCP LinkedIn | 0.2.0 | validacao-coordenada / aberto | CORE-SOC-01 / I02 / S05 / R3-LI-01 / R3-LI-02 | [base-site-core-fator3-1.34.0-impacto-wp-mcp-linkedin-fator3.md](base-site-core-fator3-1.34.0-impacto-wp-mcp-linkedin-fator3.md), r1 |
| Fator3 MCP Google | 0.10.0 | validacao-coordenada / aberto | CORE-01/02 / I01 / P01–P03 | [base-site-core-fator3-1.34.0-impacto-wp-mcp-google-fator3.md](base-site-core-fator3-1.34.0-impacto-wp-mcp-google-fator3.md), r1 |
| Fator3 MCP | 0.23.0 | validacao-coordenada / aberto | N12 / N24 / N25 / N49 | [base-site-core-fator3-1.34.0-impacto-wp-mcp-fator3.md](base-site-core-fator3-1.34.0-impacto-wp-mcp-fator3.md), r1 |
| Fator3 Implantador | 2.8.0 (identidade recebida; não executado) | acao-necessaria / aberto | P06 / P13 / P15 / N15 / N44 / N48 | [base-site-core-fator3-1.34.0-impacto-implantador-base.md](base-site-core-fator3-1.34.0-impacto-implantador-base.md), r1 |

Meta 0.2.0 real participou da ativação conjunta local e permaneceu ativo no Site-Teste. Não foi identificado impacto técnico novo na API do plugin Meta nas fronteiras examinadas; alertas Meta alterados pertencem ao Core. Não há quinto arquivo de mero aviso. A matriz completa de isolamento/pausas social ainda não foi executada e não é certificada por esta conclusão.

O SDK de medição permanece **1.0.0 / schema 1 / seis slots**. Apenas o contrato administrativo muda para **8.0.0**. Google 0.10.0 foi usado na bancada; Google 0.9.0 permaneceu no Site-Teste. LinkedIn 0.2.0/API pública 1.1 e MCP 0.23.0 foram usados sem modificar seus pacotes. Não há novo código, stub, tela ou preparo de Sheets social.

## 3. Mudanças e evidência

| Pedido | Problema e mudança | Resultado / evidência própria |
|---|---|---|
| P01/P03 — GSC | Diagnóstico comum separa SDK, grant, conexão, prontidão estrutural, tentativa, próxima execução, publicação e cobertura; leitura não coleta. | `google-sdk-1340.json`: 23 verificações; publicação e falha SQL com SDK real/HTTP simulado. |
| P02 — contratos | Preservados SDK de medição, catálogo, revisões e seis slots. | `medicao-sdk-1330.json` declara plugin 1.34.0: 46 verificações. Nome histórico do teste preservado. |
| P04/P05 — instalação/docs | Ciclo alvo 1.34, migração antes de defaults, prontidão em requisição nova; docs/schema/fixtures completos e paginados. | Ciclos nativos, MCP 0.23 e Site-Teste; 365 verificações de páginas/hash/permissões. |
| P06 — Lead Sync | Coleção por integração, UUID estável, principal/Core legado, cliente/conexão explícitos, dois adaptadores públicos, leases e estado separados. | Migração 14; Core 57; SDK 24; transições 14 verificações. Provedor simulado. |
| P07 — transporte/homologação | Diário público de assinaturas, POST incerto sem novo intento, guardas de grant/ownership e recibo em voo; preservação do erro MCP. | Binários reais LinkedIn 0.2 e MCP 0.23. I02 local parcial; I03 externo pendente. |
| P08 / core 194(b)/(e) | Slack ignora verbatim somente em mrkdwn e emoji somente em plain_text. Texto/link/tipo/ordem continuam significativos; docs distinguem principal de thread. | Testes de equivalência/divergência locais; exclusão real pendente. |
| P09 / core 209(b) | Qualidade distribui consultas por confirmação/tentativa, respeita orçamento e encerra polling terminal após três confirmações espaçadas. | 17 registros; tetos 600/3000; cadência acelerada. Sem prova de 24h reais. |
| P10 / core 212(a) | Memória editorial medida com limite bruto/efetivo, reserva, contagem e estimativa; lote adaptável e agregação exata. | 41 verificações editoriais e casos operacionais de memória. 28 dias; vazio/erro/insuficiência distintos. |
| P11 / core 213(b) | Ajuda e impacto da conversão LinkedIn descrevem aceite do contato conforme consentimento, sem novo evento por clique. | Inspeção de fluxo; teste de emissão no navegador pendente. |
| P12 / core 215 | Identidade de catálogo Pipedrive separada de orçamento/homologação/defaults; troca de conta/token invalida; guarda integral do lote mantida. | Nove verificações de identidade e migração. |
| P13 / core 216 | Alertas operacionais Meta/Pipedrive vão a admin_email; sem fallback comercial. Estados de falha/incerteza/destinatário inválido explícitos. | Interceptação local de correio comprova roteamento, não recebimento. |
| P14 / core 217 | GTM vazio encerra espera esgotada, retira agenda e retorna nada_a_verificar sem HTTP; ação própria com revisão/auditoria. | Concorrência/reinserção/outros módulos e duas passagens simuladas; Site-Teste sem agenda GTM. |
| P15 / core 218 | Menu de recuperação Site Core; nomes e raízes canônicos, fonte completo e relatórios pertinentes. | Pacotes/manifesto de conteúdo e checklist. |

**Limite funcional entregue no LinkedIn:** troca com histórico de assinatura anterior permanece pausada e explicitamente bloqueada quando Core/SDK não podem provar drenagem de notificações em trânsito. Não se troca dono, reutiliza cursor/grant antigo, apaga diário nem declara drenagem por tempo arbitrário. Troca nos dois sentidos sem esse histórico foi comprovada. Esta proteção não é homologação integral de P06/I02.

### Matriz N01–N49

“Comprovado local” significa WordPress/banco reais e serviços externos simulados, salvo indicação de Site-Teste. “Parcial” não encerra o aceite completo.

| ID | Situação | Prova e limite |
|---|---|---|
| N01 | Comprovado | Instalação limpa e upgrade nativo/MCP 1.33→1.34; também Site-Teste. native-cycles, mcp-cycle e site-teste. |
| N02 | Parcial | Valores vazios, procedência, segredo, callback, cursor e lead preservados; idempotência. Filas sintéticas vazias não provam toda fila não vazia. |
| N03 | Parcial | SDK medição 1.0.0/schema 1, seis slots e 46 verificações; Google real 0.10.0 no laboratório. Vínculo positivo completo do consumidor Google no Site-Teste pendente. |
| N04 | Pendente de regressão completa | Zero/um/vários streams e retenção de binding têm evidência recebida da base; matriz própria integral do candidato não executada. |
| N05 | Parcial | Projeção GSC comum implementada; ausência, resolução por grant e erro estrutural exercitados. Matriz visual inteira pendente. |
| N06 | Parcial | Resumo sem HTTP/escrita comprovado; teclado e largura estreita não executados em navegador. |
| N07 | Parcial | SDK Google real, usuário zero e conexão não padrão comprovados. Revogação/quota/troca entre páginas não reexecutadas integralmente. |
| N08 | Comprovado local | Resposta válida do SDK real seguida de falha SQL; snapshot publicado e cursor preservados. Provedor HTTP simulado. |
| N09 | Comprovado local | Consulta não fabrica execução Google; desligamento remove agendas Core. google-sdk-1340. |
| N10 | Parcial | Site-Teste com Yoast/cache reais: HIT anônimo 1.34 após invalidação do upgrade. Nova matriz escrita/HTML/Markdown/noindex não executada; prova Yoast anterior recebida. |
| N11 | Pendente no candidato | Exclusões mantidas; assets herdados. Nova prova de navegador 404/editor/teste e emissão não realizada. |
| N12 | Comprovado no escopo | Ativação separada de prontidão; requisições novas; inventário local de todos os arquivos igual ao ZIP final após parar PHP. MCP 0.23.0 substitui base mínima 0.22 do plano. Remoto: upload por hash e inventário, sem comparação remota integral dos bytes. |
| N13 | Comprovado local/remoto | Documentação catalogada e paginada, 365 verificações de leitura/hash/permissões; AGENTES 1.34 lido integralmente por MCP no Site-Teste. |
| N14 | Comprovado documental | Origens separadas abaixo; hash final vinculado aos ciclos nativos e ao upload remoto. Provas históricas não recertificadas. |
| N15 | Comprovado local | Migração única para principal/Core, preservação de bytes/procedência/callback/cursor, contrato 8.0.0; escrita antiga recusada. migration-1340 e native-cycles. |
| N16 | Comprovado local | Duas integrações com clientes distintos, recursos e grants próprios; deduplicação/identidade. Lista vazia não expande recursos. |
| N17 | Parcial | Sobreposição recusada, revogação sem fallback e cliente Core exercitados. Todas as ordens físicas de desativação não cobertas. |
| N18 | Parcial | SDK LinkedIn real 0.2.0/API 1.1, usuário zero, quota e revogação. Ausência/incompatibilidade tratadas; matriz completa de versões não executada. |
| N19 | Parcial | Troca nos dois sentidos, lease concorrente, replay, queda antes do commit/retomada comprovados. Queda depois do commit implementada, sem injeção específica. Histórico de assinatura mantém troca bloqueada por falta de prova de drenagem. |
| N20 | Parcial | Corpo original/HMAC, callback pelo contexto, repetição e persistência exercitados. Perda de credencial e todas as notificações tardias não homologadas externamente. |
| N21 | Comprovado local no conjunto | Suíte Core 57 verificações: recibos, CREATED/DELETED, submissão posterior, 404, paginação e falha SQL; sem sessão inventada. Provedor simulado. |
| N22 | Parcial | Lista/seletor/estado/preflight e edição por integração implementados. Navegação por teclado e layout estreito pendentes. |
| N23 | Pendente externa | I03: não foram fornecidos recursos LinkedIn/destino dedicados para lead real e efeitos externos. Nenhum aceite remoto alegado. |
| N24 | Parcial | HTTP MCP 0.23 real preserva booleano e diagnóstico. Redação sintética exercitada no SDK; matriz integral de contagens/campos sensíveis no transporte não repetida. |
| N25 | Comprovado local | HTTP MCP mantém revision_conflict, conflict=true e data=null no envelope de domínio; callback e transporte ensaiados. |
| N26 | Comprovado no código/docs | Modelo, grants, limites e retomada publicados; SDK medição preservado. Fronteira LinkedIn usa API pública sem leitura privada cruzada. |
| N27 | Parcial | Acompanhantes reais ativados e fronteiras SDK exercitadas; S01/S04/S06 completos (ordens, bridge aninhada, todas as pausas) não reexecutados. Nenhum preparo Sheets social adicionado. |
| N28 | Comprovado documental | I02 local parcial separado de I03 remoto pendente; limites e responsáveis explícitos. |
| N29 | Comprovado local no conjunto | Registro real por integração, UUID/descriptor e grants independentes, sem impersonação; migration/linkedin-sdk. |
| N30 | Parcial | Janelas de 30 dias, páginas de 50, IDs/ms e cursor vinculados implementados/testados no conjunto. forms_remaining tem complemento por get_form; fixture dedicada >5 formulários e latência total real pendentes. |
| N31 | Comprovado local | POST incerto + GET vazio não permite outra criação; diário público preserva operação. Produtor real 0.2.0 e HTTP simulado. |
| N32 | Parcial | Revogação na pré-consulta impede POST/DELETE; POST em voo preserva recibo; DELETE com autoria confirmado. Revogação em voo de DELETE não recebeu injeção específica. |
| N33 | Parcial | Callback 1.33 preservada e ownership/revisões guardadas. Sem prova pública de ausência de notificação em trânsito, troca com histórico não promove; não há timeout arbitrário de drenagem. |
| N34 | Parcial | Preflight público confere conta/formulários/grants/conexão; faltas viram motivo. Recursos reais e fixture extensa de metadados pendentes. |
| N35 | Parcial | Equivalência ignora verbatim/mrkdwn e emoji/plain_text; divergência de texto/ordem testada. Todas as flags, raiz/resposta/paginação não combinadas em suíte exaustiva. |
| N36 | Documentado; externa pendente | Sem inferir limpeza da thread por ausência da principal; recibo e ausência separados. Exclusão Slack real não realizada. |
| N37 | Comprovado local no conjunto | 17 registros, tetos 600/3000, reserva e rodízio sem inanição; esgotamento sem HTTP. Não equivale a observar 24h reais. |
| N38 | Parcial | Três confirmações terminais com cadência simulada; repetição curta/404/won não encerram. Reabertura e erros guardados no código; observação real prolongada pendente. |
| N39 | Comprovado local | Limite bruto/efetivo, uso/reserva/estimativa; inválido, zero e -1 distintos. operational/editorial. |
| N40 | Comprovado local | Aquisição/resumo 28 dias, baixa carga e sessões entre dias exatas; insuficiência/erro SQL não viram zero. Alvo CTO Office não validado. |
| N41 | Parcial | Descrição e impacto corrigidos para aceite do contato e inspecionados contra JavaScript. Prova de uma emissão no navegador e recebimento LinkedIn pendentes. |
| N42 | Comprovado local no conjunto | Orçamento/homologação preservam identidade; token invalida; guarda integral de lote mantida. pipedrive-identity. |
| N43 | Parcial | Catálogo legado só migra com prova, sem prova fica pendente. Falhas de SQL/paginação do catálogo completo não reinjetadas nesta rodada. |
| N44 | Parcial | Roteador operacional comum admin_email e ausência de fallback exercitados. Chamadores Meta/Pipedrive migrados; todos os cenários remotos de recuperação pendentes. |
| N45 | Parcial | Falha e destinatário inválido legíveis; aceite do wp_mail não afirma recebimento. Incerto/supressão/dedupe implementados; chegada real de e-mail não comprovada. |
| N46 | Comprovado local | GTM vazio sem HTTP/agenda, upgrade e duas passagens simuladas não recriam evento; ID inválido distinto. Dois dias reais CTO Office pendentes. |
| N47 | Comprovado local/remoto | Espera esgotada encerrada, revisão/reserva/reinserção e outro módulo preservados. Site-Teste: GTM sem agendamento, encerrada_sem_configuracao. |
| N48 | Comprovado com norma r4 | Nomes/raízes/hash/cópia interna e menu Site Core. Quatro impactos pertinentes; norma r4 elimina a antiga quantidade fixa de cinco. |
| N49 | Comprovado no escopo | Normas completas instaladas; docs paginadas/hash; administrador autorizado e traversal recusado via MCP; usuário zero recusado localmente; checklist abaixo. |

### Origem das provas

Próprias desta rodada: implementação, inspeção, 208 arquivos PHP com lint aprovado, suites listadas, instalação nativa/MCP e leitura pública no Site-Teste. `evidence/final-run.txt` registra todas as execuções finais com exit 0; `evidence/installer.json`, `native-cycles.json`, `mcp-cycle-1340.json` e `site-teste-1340.json` vinculam o instalador fechado. As 365 verificações documentais incluem paginação; não são 365 funcionalidades diferentes.

Recebidas: 21 verificações estáticas da revisão 1, seis observações MCP da revisão 2, quatro observações unitárias LinkedIn da revisão 3, 30 casos sociais dos produtores e inspeções/inventário documental da revisão 4. Permanecem com sua origem no plano integral; não contam como execuções próprias do candidato. Prova Yoast/cache e do consumidor Google na 1.33 não certifica automaticamente a 1.34.

## 4. Instalação e prova da troca

Pacote WordPress: `base-site-core-fator3-1.34.0-instalador.zip`; `expected_slug=base-site-core-fator3`; `expected_sha256=3d3d3ffa084026a0f36e3badf852cba8aeb30620503878534328bddb9a260be1`. A entrega não foi publicada em GitHub/raw nem aplicada à frota. No Site-Teste foi utilizado `plugins/upload-base64`, sobrescrita da pasta estável e conferência do hash. URL raw final: não emitida nesta rodada; não se inventa endereço de distribuição.

Após ativação, consultar `f3base/saude-ler` em nova requisição. Esperado: versão 1.34.0, ciclo atual, 14 etapas completas, `estado=concluida`, `finalizacao_em>0`, falhas zero. Não usar apenas `active_after=true` como prova de prontidão.

| Ambiente | Cenário | Resultado | Limite |
|---|---|---|---|
| WP local | Novo e upgrade direto | Estrutura 1.34/contrato 8; dados/segredo/callback preservados; reexecução sem duplicação | Janela de confirmação acelerada apenas no banco descartável |
| WP local + MCP 0.23 | Upload real HTTP, nova requisição, erro/null/booleano | Aprovado; todos os arquivos iguais ao ZIP final depois de parar processos PHP | Provedores bloqueados/simulados |
| Site-Teste compartilhado | 1.33→1.34, ativo antes/depois | Operação `420488813b3427f207122ec2`; ciclo `80fe7e0e-22d8-4eff-8c8d-01eae3d18b7e`; 14 etapas e confirmação real em 2026-10-16T16:12:44Z, falhas zero | Dois checkpoints sem confirmação de escrita recuperados automaticamente; sem limpeza manual de sentinela |
| Site-Teste público | Cabeçalhos após invalidação da atualização | HIT anônimo, sem bypass, plugin_version=1.34.0, persisted=true; geração `812e935e-2f93-4c4a-b374-dc0472bd2dc2` | Não substitui matriz inteira de edição/noindex/Markdown |

Documentação: `f3base/documentacao-ler {}` descobre índice; parâmetros `arquivo`, `linha`, `limite` (máximo 200) fazem leitura paginada. `docs/AGENTES-1.34.0.md` foi lido até a linha 27 via MCP; SHA-256 `ba6b281f64bea5c4b10bd166080547ca590c57405bac35c5906c9fa6d2a03a1a`. `../wp-config.php` foi recusado como documento não catalogado. Catálogo/schema são gerados do registro; 125 options, 54 tabelas, 10 transients e 129 abilities inventariadas.

Estado final: Core 1.34.0 ativo no Site-Teste; MCP 0.23.0, Google 0.9.0, LinkedIn/Meta 0.2.0, Yoast 28.7 e WP Super Cache 3.1.4 mantidos. Migração concluída; GTM vazio sem agenda e espera encerrada. Laboratório separado, com dados sintéticos e provedores bloqueados; servidor HTTP/MySQL encerrados e senha de aplicação de teste removida. Não se criaram contatos remotos, mensagens, assinaturas ou configurações de fornecedor no Site-Teste. Backups administrativos da troca permanecem privados para reversão. Não foi usado reset de banco compartilhado.

## 5. Banco e volta de versão

Configuração LinkedIn passa da forma singular para a coleção administrativa 8.0.0. Diário de migração guarda identidade/callback antes da gravação; migração idempotente preserva referência às credenciais e procedência. UUID e contexto não podem ser reconstruídos por defaults em falha. A fila Pipedrive recebe `qualidade_confirmada`, `qualidade_encerrada`, `qualidade_terminal_em`, `qualidade_terminal_contagem` e `qualidade_contexto`. Identidade de catálogo e estado/recuperação GTM são reconciliados. Novos dados não são removidos pelo simples rollback de arquivos.

Antes do upgrade remoto foi criado backup SQL gzip privado: artifact_id `4b5f83786c308223c2903e37c2f33e54`, 16.134.108 bytes, 43.630 linhas, SHA-256 `0ccfcbc36c709a59c62391954e37030d62e7638e5d5ec044274999a5fd354feb`. Backup de arquivos da operação: `bc652c4ffb2bc49c0bd734b0`. O dump contém valores sensíveis e não integra os artefatos entregues.

**Reversão:** somente substituir arquivos por 1.33 não desfaz a coleção 8.0.0 e não foi certificado como seguro. Coordenar parada de executores, backup compatível de banco/arquivos privados, guardas independentes dos acompanhantes e reconciliação de efeitos ocorridos depois do backup. Não restaurar banco antigo sobre filas/assinaturas ativas nem apagar histórico para aparentar sucesso. A restauração efetiva do Site-Teste não foi ensaiada nesta rodada.

## 6. O que permanece pendente

- **Dono dos recursos/Core/LinkedIn:** I03 com conta/app/formulários/destinos explicitamente autorizados, ambos os clientes, challenge/callback, polling/deduplicação e entrega real. Prova pública de drenagem é necessária para liberar troca com histórico de assinatura.
- **Core/Google:** vínculo positivo de medição no Site-Teste; matriz completa streams/bindings e GSC quota/revogação/troca entre páginas.
- **Core/social/MCP:** S01/S04/S06 completos, todas as ordens de ativação/pausa e bridge aninhada; campos/redação MCP completos; injeção após commit e DELETE em voo; >5 metadados e latência total do lote sob fornecedor real.
- **Core/interface:** teclado/largura estreita, emissão JS de aceite/consentimento, exclusões 404/editor/teste. Tentativa local de navegador bloqueada por ausência do executável Chromium Playwright; não se produziu prova visual fictícia.
- **Core/frota:** 24h reais Pipedrive em CTO Office/Korvena e dois dias reais GTM/CTO Office; confirmar formulário atual em korvena.com.br antes do ensaio. Não usar korvena.net.br como substituto. Memória editorial no alvo que originou o relato pendente.
- **Core/dono dos canais:** recebimento real de e-mail operacional e ausência de efeito no Slack comercial; exclusão Slack raiz/resposta/thread com recursos autorizados. Interceptação local não prova chegada.
- **Core/entrega:** nova execução em WP 6.4/PHP 8.1 para confirmar mínimos herdados; matriz completa de escrita/noindex/Markdown com cache/Yoast; inventário remoto byte a byte e ensaio de reversão real não realizados.
- **Implantador:** validar schema 8.0.0 e instalação com seu binário real. Fonte e instalador não publicados em repositório/frota nesta rodada.

### Checklist do padrão revisão 4

| Item | Resultado |
|---|---|
| Base/alvo/minor, três artefatos próprios, docs completas | Atendido |
| Impactos relevantes e continuidade dos encaminhamentos | Quatro documentos, sem arquivo de mero aviso Meta |
| Raízes/nomes/hash, fonte singular, sem ZIP aninhado | Atendido; cópia interna anterior ao fechamento |
| Permissões/identidades administrativas | Conferidas no código/testes; usabilidade de navegador pendente |
| Instalação limpa, upgrade direto, expected_slug/hash | Comprovado local e upload no Site-Teste; URL raw não publicada |
| Dados/credenciais/filas/preservação | Provas delimitadas N02/N15; não certificar toda fila não vazia |
| Segredos, fixtures ativas e isolamento | Instalador sem bancada/segredos; evidências sintéticas ou sanitizadas |
| Acessos externos e matriz completa | Pendências acima; entrega classificada com-pendencias |
| Estado final e atuação em outros plugins | Registrado; nenhum acompanhante modificado nem relatório enviado |

## 7. Credenciais e configuração do dono

Em Site Core, selecionar a integração LinkedIn, cliente Core ou plugin, conexão pública, conta/formulários e grant correspondente. Cliente Core usa referências do cofre existente; cliente externo usa o cofre/grant do produtor. Não copiar token entre plugins. A lista vazia permite zero recursos. Prévia/troca exige revisão e contexto verificados; alteração não contorna pausas ou incerteza. Recursos de I03 exigem autorização concreta antes de efeitos externos.

GSC depende da conexão/grant Google para a propriedade selecionada. Pipedrive conserva domínio/conta/instalação/revisão física de credencial na identidade. Alertas operacionais dependem de `admin_email` válido e transporte de correio; destinos comerciais permanecem em suas configurações próprias. Nenhuma credencial real, cookie, dump ou chave privada é entregue. Credenciais sintéticas dos scripts servem exclusivamente ao laboratório descartável.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [base-site-core-fator3-1.34.0-instalador.zip](base-site-core-fator3-1.34.0-instalador.zip) | 1930387 | `3d3d3ffa084026a0f36e3badf852cba8aeb30620503878534328bddb9a260be1` |
| Fonte | [base-site-core-fator3-1.34.0-fonte.zip](base-site-core-fator3-1.34.0-fonte.zip) | 2061225 | `a524d0f0e32435b4dd19ac26bb074a28c45e6d1dbffae6908da5369dd83ade4f` |

Relatório externo canônico, fechado após o fonte. A cópia interna foi identificada como anterior ao fechamento e não tenta registrar o próprio hash.
Os quatro impactos da seção 2 são complementos encaminháveis. O fonte inclui código completo, assets editáveis/minificados, documentação, scripts de build, testes selecionados executados, evidências próprias sanitizadas e instruções de reprodução. Dependências WordPress/PHP/MySQL e instaladores acompanhantes não são embutidos; hashes/origens e caminhos esperados estão documentados.
