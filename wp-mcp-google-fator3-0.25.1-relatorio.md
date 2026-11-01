# Entrega — Fator3 MCP Google 0.25.1

2026-10-31T20:22:13-03:00 · rodada Google 0.25 · base publicada 0.24.0 · pedido Google47 · relatório externo final.

**0.25.1 implementada e ativa no Site-Teste.** O aviso de renovação aguarda a sequência de retentativas ou a proximidade do vencimento; recuperação só avisa quando houve atenção aceita. O patch0.25.1 inclui o novo manual no índice instalado, omissão encontrada no candidato0.25.0 antes de fechar o fonte. Foram aprovadas775 verificações nativas da versão final e15 verificações específicas no Site-Teste. Há uma incompatibilidade preexistente do SDK Core1.65.1: a correção está implementada e entregue para incorporação pelo mantenedor; não foi instalada no Core compartilhado.

## 1. Bases e entradas consideradas

Base Google0.24.0 imutável: instalador886260 bytes, SHA256`803fa058182b9f43625352f2b4a1572a3cd4b728f8c07fd58314a9a111d41849`; fonte6789039 bytes, SHA256`6e2dd4f447404b9610b091288be2841105c1c016e3eee034caa7fd31e903af0f`. Foram lidos o relatório da base, o pedido anexado de31/10/2026 e as normas r5 preservadas. O pedido47 é a novidade;43–46 permanecem entregues e a numeração seguinte é48. A lista central não foi reescrita.

| Pacote recebido | Versão | SHA256 do instalador |
|---|---|---|
| Site Core |1.65.1|`059d7da03484eb3d9eb7327f49787144466f451fcf51730ea0357d92c03f168a`|
| MCP |0.38.0|`bc550c6573527a0d71bfa560036f83e7c8aec546f49d70b8e0095da5d303c1a5`|
| Meta |0.17.0|`a360feff0bdb723c7f3c2a240b288bc1c3af917e851cb798d905e31a95b4162d`|
| LinkedIn |0.13.0|`1c45738322f4901aeacdc36615789ae961e8b9d521ba321a27de0aea76c13502`|
| Pipedrive |0.5.0|`59e8c99d5bb8a54fcfeaba06c56d816b940a1fe97a7d6b473d13a252c6e5042a`|

Core/MCP/Meta/Pipedrive: fontes, instaladores e relatórios anexados examinados; LinkedIn0.13: instalador exato da matriz anterior recuperado. ZIPs tiveram integridade/identidade conferidas. `reproducao/entradas025/inputs.json` identifica os demais arquivos e hashes, sem ZIPs aninhados. Não houve atualização de bibliotecas de produção nem uso de um pacote inventado como base.

## 2. Convivência e encaminhamento ao Core

| Pacote | Prova própria desta rodada |
|---|---|
| Core1.65.1 original | Ativação, inventário,14 verificações de integração e85 de acervos Ads/GSC. SDK de medição ilegível reproduzido. |
| Core1.65.1 com correção proposta | Matriz de renovação e atualização,57 verificações específicas da política e35 de upgrade/rollback. Um arquivo alterado somente em laboratórios identificados. |
| MCP0.38.0 | Descoberta e execução autenticada das novas habilidades, documentos paginados, atualização, guarda de rollback, reversão e reaplicação. |
| Meta0.17.0 e LinkedIn0.13.0 | Instalação/ativação exatas nos laboratórios; registros cifrados e cron preservados durante upgrade/rollback Google. |
| Pipedrive0.5.0 | Código/relatório considerados e inventário ativo remoto. Exige PHP8.3.36; não ativado na bancada PHP8.3.6. |
| Meta0.18.0 e LinkedIn0.14.0 | Surgiram no Site-Teste durante a rodada. Inventário, status/changelogs instalados lidos. Meta26 altera a indicação de erro histórico; LinkedIn16–17 tratam OAuth/avisos. Não exigem adaptação Google declarada. Não receberam homologação local integral por esta rodada. |

**Impacto técnico novo: Core.** `F3Base_Medicao_Contexto::politica()` emite campos que o schema fechado1.0.0 não admite: ga4/google_ads/gtm em destination_loading.destinations, além de clock/accelerate_conversion. O próprio produtor rejeita a fotografia com `unreadable`; a validação reproduzida informa `ga4 is not a valid property of Object`. A falha também estava presente no Site-Teste antes da troca Google e bloqueia a leitura do Measurement ID/verificação GA4.

Foi implementada, sem esperar resposta do Core, a correção mínima da projeção para o contrato já publicado. Configurações e execução das tags não mudam. Google continua consumindo exclusivamente o SDK público, sem acesso a opções privadas ou contorno da recusa. Entrega: `wp-mcp-google-fator3-0.25.1-impacto-core.md`; arquivo completo, patch e hashes em `reproducao/core1651-fix/`. A incorporação e versão Core estão pendentes com seu mantenedor. Não há novo contrato exigido nem patch Core instalado no Site-Teste nesta rodada.

Também foi observado notice do Core ao atribuir defer ao alias f3base-tracking sem src, durante a tela administrativa; está registrado no mesmo encaminhamento, separado da correção de contrato. Nenhum outro impacto técnico novo que exija adaptação foi identificado no escopo examinado. Os impactos históricos e as confirmações de entregas anteriores ficam registrados como contexto, sem reemissão apenas de status.

## 3. Alterações e evidências

O incidente aparece na primeira falha. A atenção é elegível na sexta falha consecutiva (inicial mais cinco retentativas, intervalos5/10/20/40/60 minutos) **ou** quando a prova sem renovação chega à janela configurada. As retentativas continuam a cada hora depois da sequência. O contador existente inclui verificações manuais falhas; somente o executor envia a atenção. Sem prova anterior, a condição de esgotamento é necessária.

A janela é por conexão, inteira de0 a24 horas, padrão6; zero significa no vencimento. O executor avalia a janela entre tentativas. Se uma tentativa já estiver vencida, tenta renovar antes de avisar, evitando alerta quando a recuperação é imediata. Leituras e simulação/aplicação do prazo não enviam mensagens nem consultam Google.

`google/plan-renewal-notifications` retorna prévia, revisão e hash vinculados a usuário/conexão. `google/configure-renewal-notifications` exige os valores exatos da prévia sob a trava de entrega. A tela Conversões usa o mesmo serviço, com nonce, campos tipados e confirmação da simulação. Ajustar o prazo preserva credenciais, concessões, prova e destino.

Cada ciclo tem recibos persistentes por conexão/destino/tipo. Uma reserva anterior ao correio impede duplicidade por concorrência, repetição ou interrupção. Recuperação resolve o incidente e envia uma única mensagem apenas se a atenção foi aceita pelo transporte. Incidentes antigos abertos com atenção aceita não repetem atenção; os já resolvidos permanecem intactos. `accepted` não comprova entrega na caixa postal; `failed`/`unknown` não autorizam reenvio automático de correio. A verificação continua tentando.

São300 habilidades:115 leitura/185 escrita;42 opções. Configuração4.0.0, execução/armazenamento/manutenção2.0.0 e contratos Core/Google Ads/GSC preservados. Diagnóstico notification é aditivo e opcional na renovação de aquisição; conversões por etapa não ganharam e-mail. O módulo de aviso compartilha o arquivo/trava de ConversionDelivery. Runtime final172 arquivos,168 PHP;11 arquivos modificados contra0.24, nenhum caminho de runtime adicionado/removido. O diff está em reproducao/diff-runtime025.json.

| Matriz final0.25.1 | Ambiente | Verificações | Falhas |
|---|---|---:|---:|
| Mínimos, Google isolado | WP7.1.2/PHP8.3.6/MySQL8.0.46 |94|0|
| Atual, acompanhantes originais | WP7.1.4, Core1.65.1/MCP0.38/Meta0.17/LinkedIn0.13 |218|0|
| Consumidores Ads/GSC Core original | WP7.1.4, mesmos originais |103|0|
| Renovação com correção Core proposta | WP7.1.4, variante explicitamente identificada |188|0|
| Upgrade0.24→0.25.1 e rollback | WP7.1.4, mesma variante Core |172|0|
| **Total de execuções** | **WordPress real, fornecedores sintéticos** |**775**|**0**|

Os totais incluem123 verificações documentais em cada uma de três matrizes; não são775 requisitos distintos. O caso renovação contém57 verificações próprias: falha/recuperação silenciosa, limiar inclusivo, esgotamento, recuperação única, novo ciclo, Ads, ausência de prova, zero, erro/exceção de correio, reserva após interrupção, persistência falha, legado, simulação, revisão, conexão, autorização, UI real e MCP. Concorrência: executor reentrante durante a trava; não se declara teste de dois workers de correio independentes. Tempos são acelerados por timestamps sintéticos, sem esperar horas reais.

Lint dos168 PHP, catálogos, geradores, schemas/documentos e inventários exatos aprovados. Gate corrente `tools/release025.py`; provas finais somente `evidence/025/closed/`, com hashes do candidato e identidade de fontes/testes preservada. Casos anteriores, de diagnóstico e candidatos descartados não integram os totais. PHPUnit integral não executado: PHAR oficial retornou HTTP403. Não se reaproveitam resultados unitários antigos. Avisos WordPress de atualização externa no laboratório decorrem do bloqueio deliberado de rede; a análise não afirma ausência de notices em todos os acompanhantes.

A revisão preliminar corrigiu a ausência de carregamento da nova classe e a cobertura do índice documental. Um ensaio preliminar de rollback detectou arquivo novo residual; a lógica foi consolidada no módulo já existente e o inventário da reversão final passou byte a byte. O candidato0.25.0 foi usado no aceite remoto; a omissão documental motivou0.25.1 e nova matriz com o mesmo ZIP final. Não se distribui0.25.0 como versão corrente.

## 4. Instalação e estado do Site-Teste

Destino autorizado: https://fator3-teste-mcp-1.dreamhosters.com/ . Somente Google foi instalado. O Site-Teste encerra com Google0.25.1, Core1.65.1, MCP0.38.0, Meta0.18.0, LinkedIn0.14.0 e Pipedrive0.5.0 ativos. Os acompanhantes mantiveram as versões observadas imediatamente antes da troca final; Meta/LinkedIn foram atualizados por outras rodadas durante a execução.

Rota `plugins/upload-base64`, expected_slug=wp-mcp-google-fator3, expected_sha256=bdd860d479e9813246f8fd2828728ff0cc0c969c2b1e85ddb28a7c9a041d6b30, overwrite=true, activate=true, sondas30s. Operação final`653d8a928bdde353e56f176f6124cb85`; backup imediato`aa87b3d7f18f458cdebb7370`. Versão anterior imediata0.25.0 do candidato; a primeira troca0.24→0.25.0 teve operação`893f3a39b944bf7194600e90b7abebc0`, backup`ce234f4c9fb4ad15a4dae79e`. Ativação em PHP novo e sondas internas home/REST retornaram200 antes/depois. Isso não prova acesso externo geral ou cache público.

Status final confirma0.25.1 e armazenamento pronto. Configuração administrativa:41 entradas anteriores idênticas na visão da API, mais a nova opção com padrão6; segredos continuam redigidos. Configuração e revisão de entrega preservadas; nenhum incidente sintético restante. `plugins/rollback` com dry_run=true confirmou prontidão do backup imediato, sem aplicar reversão remota.

Aceite47 no Site-Teste:15 verificações aprovadas no motor de notificações com registros exclusivos e correio interceptado. Falha seguida de recuperação:zero mensagem. Janela de validade:uma atenção; repetição:sem duplicata; recuperação:uma; novo ciclo esgotado:uma atenção. Três chamadas de correio interceptadas,zero mensagens reais ezero HTTP fornecedor. Configuração preservada, registros/recibos removidos. A sonda administrativa temporária foi removida com backup obrigatório e files/stat confirmou ausência. As verificações e a rotina de renovação foram executadas diretamente nos laboratórios com transporte sintético; não é uma falha induzida numa conta Google real nem observação do WP-Cron por horas reais.

Documentação instalada:24 documentos,85 páginas,4350643 bytes lidos integralmente por google/documentation com revisão/offset. Cada página foi comparada ao SHA256 dos bytes compilados e ao índice; todos coincidem. O novo AVISOS-RENOVACAO.md está acessível. Evidências sanitizadas: `evidence/025/remote/`.

## 5. Banco, preservação e volta de versão

Sem migração, nova tabela ou reescrita de credenciais. Política em uma opção não autoload por conexão; padrão lido sem materialização automática. Incidentes/recibos usam o repositório corrente. Não removemos prova ainda válida por uma falha de renovação; a validade normal e os gates de pausa/autorização continuam vigentes.

Upgrade nativo preservou ciphertexts, seleção, concessões/provas, acervo cifrado, tarefas concluídas, agendas pausadas, auditoria, conexões e sentinelas dos acompanhantes. Reversão local restaurou exatamente o instalador0.24 e reaplicou0.25.1. Guarda recusou arquivo deliberadamente editado. Correção Core permaneceu uma variante declarada durante esse teste, não parte do ZIP Google.

Rollback de arquivos não desfaz banco nem correio aceito. Para voltar à base0.24, use o instalador íntegro0.24 sem desinstalar; preserve banco e salts. No Site-Teste, os dois backups formam uma sequência: backup imediato volta ao candidato0.25.0; após nova prévia e identidade235c88c4…, o backup anterior pode voltar à0.24. Não aplicar o backup antigo diretamente sobre pós-imagem diferente. A versão0.24 restaura o comportamento de aviso imediato; não promete deduplicação entre algoritmos de versões diferentes.

## 6. Pendências e limites

- Core: incorporar/versionar a correção fornecida e validar/distribuir pelo fluxo do seu mantenedor. Enquanto o Core1.65.1 original retornar unreadable, a verificação GA4 continua bloqueada. O notice do alias tracking também requer revisão Core.
- Fornecedor real: aceites Ads/GSC/Service Account já pendentes na frota e contas ctooffice não foram substituídos por fixtures. Esta rodada não enviou conversão, não consumiu verba, não publicou tags e não alterou consentimento.
- Correio real e cron por horas reais: não comprovados. Aceitação do transporte não garante caixa postal; resultados incertos permanecem explícitos e sem replay automático.
- Matriz local: Pipedrive0.5 não ativado por mínimo PHP; Meta0.18/LinkedIn0.14 tiveram leitura documental/inventário remoto, sem repetir sua homologação funcional completa. PHPUnit integral indisponível.
- Distribuição além do Site-Teste, publicação externa e atualização das listas centrais permanecem com o dono. Nenhum repositório público ou site de produção foi alterado.

## 7. Credenciais e configuração do dono

Não há nova credencial. Em Ferramentas → Fator3 MCP Google → Conversões → Avisos da renovação, informar0–24 horas, Simular alteração e Aplicar prazo simulado. Destinatário: e-mail administrativo do WordPress. Padrão6 horas. Para agentes, usar plan-renewal-notifications e configure-renewal-notifications com configuration, expected_revision e expected_plan_hash. Uma prévia obsoleta requer nova simulação; não remove a guarda.

As credenciais Google e os destinos já configurados são mantidos. O Core permanece responsável por IDs/tags/consentimento e transporte selecionado. Renovação automática exige concessão administrativa válida e os acessos reais ao destino. Nenhum token, chave privada, cookie, senha de aplicação ou dump de banco está nesta entrega. Não há envio de mensagem externa ao mantenedor; o encaminhamento técnico com patch é entregue ao dono.

## 8. Identidade dos arquivos e fechamento

| Artefato | Nome final | Bytes | SHA256 |
|---|---|---:|---|
| Instalador | wp-mcp-google-fator3-0.25.1-instalador.zip |895748|`bdd860d479e9813246f8fd2828728ff0cc0c969c2b1e85ddb28a7c9a041d6b30`|
| Fonte | wp-mcp-google-fator3-0.25.1-fonte.zip |7043091|`9b496df1ceb3786439db79bc1e7dac29ccf78bf31e9d99468011f2cc51502429`|
| Impacto Core | wp-mcp-google-fator3-0.25.1-impacto-core.md |5862|`f98a5c39c489c0c7075c0eec6db1dc8fb3357bb107031410165bdbe6dbc4afea`|

Relatório principal: wp-mcp-google-fator3-0.25.1-relatorio.md. O instalador é o único ZIP instalável, raiz wp-mcp-google-fator3/. Fonte inclui código completo, testes, geradores, schemas, evidências finais sanitizadas, entradas e correção proposta Core; não contém ZIPs aninhados/dependências binárias/bancos. A cópia interna deste relatório antecede o fechamento do fonte e conserva o placeholder. O fonte é fechado uma única vez; identidade final preenchida apenas no relatório externo. A reconstrução do instalador a partir do fonte fechado deve reproduzir os bytes testados e instalados.

Reconstrução executada após o fechamento: instalador byte a byte idêntico ao candidato validado e instalado (`bdd860d479e9813246f8fd2828728ff0cc0c969c2b1e85ddb28a7c9a041d6b30`). CRC do fonte íntegro e nenhum ZIP aninhado. O fonte não foi reaberto/reempacotado.
