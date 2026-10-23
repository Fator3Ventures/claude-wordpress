# Entrega — Fator3 Site Core 1.49.1

23/10/2026 · revisão 1 · horários em America/Sao_Paulo (−03).

A revisão encontrou correções necessárias. A versão corrente entregue passa a ser **1.49.1**, com o pedido **291** e dois achados da revisão. A 1.49.0 recebida foi mantida intacta como base; não foi renomeada. Nenhuma regressão adicional foi observada no escopo testado. Isso não constitui prova de todos os fornecedores ou de todos os sites.

## 1. Bases aceitas

- Base direta: Core 1.49.0, instalador de 2233046 bytes, SHA-256 `64a80ede90d8cc4a555ba39a016eae217898191a6275cb9cdaaed71388af8657`; fonte de 4501923 bytes, SHA-256 `34fbadfac67541ad67da64b9777049a2e07b6110a7b5a69492498e8f9063d0a6`. Conferidos ZIP e equivalência dos 451 arquivos do runtime entre fonte e instalador.
- Comparação 1.48.0→1.49.0: 28 arquivos modificados, 5 adicionados, nenhum removido. A suíte recebida M1–M11 passou novamente na base 1.49.0; testes negativos específicos revelaram os defeitos que não estavam cobertos.
- Comparação 1.49.0→1.49.1: 27 arquivos modificados e 2 documentos adicionados; nenhuma remoção. Dez classes PHP e o cabeçalho mudaram; demais mudanças são documentação/inventário gerados. Os diffs estão em `evidence/1491/`.
- Pedidos: documento `Fator3 Site Core(20261023-151954).md`, com 291. Os pedidos 288–290 já estavam entregues; não foram reabertos. Pelas evidências atuais desse documento, os 12 sites chegaram à 1.48.0 em 22/10, substituindo a informação anterior de 11 sites ainda na 1.47.0. A leitura própria do Site-Teste confirmou 1.48.0 antes da troca.
- Normas recebidas: instruções e padrão dos plugins, revisão 4 de 16/10/2026. Patch autorizado expressamente pelo dono para correções da revisão. Nenhuma norma, documento externo, repositório público ou pacote alheio foi editado.

## 2. Convivência e encaminhamentos

| Pacote | Versão atual examinada e testada localmente | Resultado |
|---|---|---|
| Fator3 MCP | 0.29.1 | Descoberta, guardas de contexto e auditoria de serviço compatíveis. |
| MCP Google | 0.18.1 | CoreContext valida o snapshot com o schema próprio e observa alteração/restauração na mesma requisição. |
| MCP LinkedIn | 0.8.1 | Adaptador real, regras separadas, envio HTTP simulado, deduplicação e auditoria MCP passaram. |
| MCP Meta | 0.7.1 | Ativação e convivência sem conflito observado. |

Identidades dos quatro instaladores em `evidence/1491/companions.json`; cópias usadas localmente permanecem intactas em `companions/`, fora do instalador Core. A convivência produziu 26 verificações booleanas positivas, além de metadados explicativos.

Impactos recebidos considerados: Implantador 2.11.0→Core revisão 4; MCP 0.29.1→Core revisão 2; relatórios atuais Google 0.18.1, LinkedIn 0.8.1 e Meta 0.7.1; impactos históricos LinkedIn→MCP e Meta→MCP. O alerta de schema do Implantador foi confirmado e corrigido no Core. As guardas MCP de nonce/contexto permanecem; o Core não contorna o canal. Não houve mudança dos SDKs de medição/conversão nem das seis cópias partilhadas.

Único encaminhamento tecnicamente necessário: `base-site-core-fator3-1.49.1-impacto-implantador-base.md`, revisão 2, validação coordenada. Criado no planejamento e atualizado nesta entrega. Não foi enviado a terceiros. Os demais impactos examinados não exigiram mudança adicional do Core nem novos documentos de simples aviso de versão.

## 3. Mudanças por pedido e evidência

### 291 — nomes, fontes e Campanha do Pipedrive

Antes, os campos de nome podiam conter `mapa_da_origem` ou `mapa_do_site`; a nota imprimia esses códigos como nomes. O campo Campanha do CRM priorizava `utm_campaign_original` e ainda tinha fallback para ID.

Agora:

- Nome e procedência são separados: `nome_campanha_origem`/`nome_campanha_fonte`, `nome_anuncio_origem`/`nome_anuncio_fonte`, `conta_origem`/`conta_fonte`. Nome desconhecido fica vazio. IDs e parâmetro original permanecem em campos próprios.
- Nota, Slack, contingência por e-mail e resumo comum exibem o nome disponível e rotulam as fontes. O campo Campanha do Pipedrive recebe o nome já resolvido ou UTM textual; ID/macros sem resolução são omitidos.
- Leitura de registro antigo e novas apresentações corrigem os códigos legados em memória. Banco, cifra, hash original e janela de comportamento congelada são preservados. O hash efetivo da apresentação é separado quando necessário.
- Mapas continuam restritos à conta/plataforma, nomes do link são preservados e reduções de consentimento continuam aplicadas. Relatórios incluem as fontes em campos próprios. Nenhum evento novo em GA4/Meta/Clarity.

Prova: 46 verificações locais, com/sem nome, mapa do site/origem, conta divergente, IDs preservados, leitor privado, Slack montado, nota e campo CRM, legado sem regravação, resumo congelado e ausência de HTTP. No Site-Teste, os 42 casos aplicáveis passaram. Mensagens e objetos já enviados não foram alterados; partes de transporte já serializadas não são reiniciadas, evitando repetir entregas incertas.

### R1 — schema incompleto de contato e consentimento

Reproduzido na 1.49.0: quatro avisos do validador WordPress, pois os dois schemas de entrada tinham `properties` sem `type`. Os extensores agora montam primeiro o schema base integral e depois acrescentam textos. Defaults e escrita parcial válidos passam; raiz/tipo inválidos são recusados. Perfil de 92 condições avaliado sem avisos. Defeito preexistente na base, também apontado pelo Implantador; não atribuído indevidamente às melhorias M1–M11.

### R2 — falso sucesso na fila nova da 1.49.0

Reproduzido: falha SQL na leitura de vencidas ou contagem de reavaliação devolvia `ok=true` com zeros. A revisão também identificou agendamento com sucesso presumido e horário apenas solicitado.

Todas as consultas afetadas agora conferem o erro. Falha de leitura retorna `fila_indisponivel`. Após a escrita, uma agenda não confirmada retorna `ok=false`, `persisted=true` e detalhe do efeito parcial. A data retornada é a efetivamente observada. No sucesso, `codigo` mantém o filtro publicado. Testes injetam falha em quatro consultas e ocupação da trava da agenda, além de provar sucesso e timestamp real; nenhum envio ocorre pela reavaliação.

## 4. Instalação, prontidão e testes

Ambiente próprio: WordPress 7.1.3 e 7.1.2, PHP 8.3.6/64 bits e MySQL 8.0.46. Nenhum mínimo não testado foi elevado ou prometido. Lint dos **233 PHP** passou.

| Prova executada | Resultado |
|---|---|
| Melhorias M1–M11 recebidas | 58 verificações booleanas positivas e metadados; passaram na base 1.49.0 e na 1.49.1. |
| Pedido 291, schemas e falhas SQL | 46 verificações positivas. |
| Perfil/agenda/autorização | 11 verificações positivas; inclui 92 condições do perfil e bloqueio anônimo. |
| Formulários / Pipedrive / LinkedIn / Slack herdados | 32 / 39 / 48 / 20 verificações positivas. |
| Adaptador LinkedIn atual com HTTP simulado | 10 verificações positivas, incluindo deduplicação e auditoria central. |
| DOM da configuração | 7 verificações positivas; motivo acionável e fallback preservados. |
| Documentação nativa integral | 162 documentos, 623 páginas, 972 verificações; hashes, confinamento e recusa de assinante/anônimo. |
| WordPress mínimo 7.1.2 | Instalação, M1–M11, 46 casos novos e 8 casos iniciais de perfil/agenda passaram. |
| Instalação limpa e atualização 1.49.0→1.49.1 | Plugin_Upgrader real, preservação de dados/configuração/segredos sintéticos, etapas e repetição idempotente passaram. |
| Atualização adicional 1.48.0→1.49.1 | Mesmo instalador final, preservação e repetição idempotente passaram. |

Site-Teste: atualizado de **1.48.0 para 1.49.1** pelo fluxo nativo com slug e SHA-256 conferidos, pré-imagem `caef1ae13ea07ab501dedbeb` e operação `ef4cd2a768a2ad8a4ce1484dab614348`. Home e REST responderam 200 antes/depois. Ciclo concluído, zero falhas, confirmação do executor em **23/10/2026 12:47:22 −03**. Isso prova a instalação; não é comprovação de credenciais comerciais.

Acompanhantes efetivos no Site-Teste, preservados: MCP 0.29.1, Google 0.17.0, LinkedIn 0.8.1, Meta 0.7.1. A versão Google 0.18.1 foi testada localmente; o Google do Site-Teste não foi atualizado nesta tarefa.

Homologação remota: 42 verificações sintéticas passaram, zero HTTP externo, opções apenas na requisição, sem Pipedrive/Slack/e-mail/Ads real. Os dois registros foram removidos; `leads-registros-ler` com formulário `qa1491` retornou vazio. Fixture e ZIP temporários removidos com hash esperado; backups do canal preservados. Leitura operacional da fila passou.

Documentação MCP: índice de 162 documentos; RELEASE-1.49.1, AGENTES-1.49.1, DOCUMENTACAO e README lidos integralmente em sete páginas de até 20 linhas; texto e SHA-256 iguais ao instalador. A leitura integral de todos os demais documentos foi feita pela ability nativa local, não repetida remotamente. Provas sanitizadas em `evidence/1491/site-teste.json`.

## 5. Banco e reversão

Sem tabela, coluna, opção ou migração destrutiva nova. As fontes são campos aditivos em atribuição; a apresentação legada não regrava linhas. Nenhuma varredura de atualização histórica, limpeza de produção ou alteração de agenda da frota foi feita.

Rollback de arquivos para 1.49.0 restaura o código anterior e seus defeitos, preservando os dados; não desfaz entregas externas. Para qualquer restauração operacional, usar a pré-imagem e as guardas documentadas do Core/MCP. Não repetir estados incertos. Na falha de agenda com `persisted=true`, a antecipação das linhas já ocorreu e deve ser conferida antes de nova ação.

## 6. Pendências e limites

- **Frota/dono:** publicar e distribuir o instalador final conforme seu processo, conferindo SHA-256. Nenhum push nem atualização dos outros sites foi feito.
- **Aceite 291 em produção:** acompanhar o próximo contato real e conferir o nome no Pipedrive/Slack. A prova desta rodada cobre montagem local e Site-Teste; não criou objetos em fornecedor. Nenhum novo acesso/segredo é necessário para instalar o Core.
- **Implantador:** repetir o aceite integrado com Core 1.49.1 conforme o único impacto. Correção própria e provas do Core concluídas; aceite do outro responsável não declarado concluído.
- Pendências anteriores continuam com seus responsáveis: exclusão definitiva das mensagens Slack do item 115 (dono); concessão LinkedIn real `rw_conversions`/regra API; observação de sete dias do executor até 29/10 (frota, item 20). Nenhuma dessas ações foi executada por esta revisão.
- Não foi repetida toda a matriz histórica de navegador, HTTP administrativo e fornecedores. A suíte DOM, regressões dos módulos, contratos atuais e provas nativas/remotas acima são o escopo efetivamente realizado. Falhas esperadas de injeção SQL e de contexto CLI do MCP foram distinguidas de regressões.

## 7. Credenciais

Nenhum segredo real criado, copiado para artefatos ou alterado. Transporte remoto usou a conexão autorizada existente. Tokens dos testes de fornecedor são sintéticos, interceptados localmente. Fonte exclui banco, cookies, logs, runtime e arquivos de autenticação. Não há credenciais a entregar.

## 8. Artefatos finais

| Artefato | Bytes | SHA-256 |
|---|---:|---|
| `base-site-core-fator3-1.49.1-instalador.zip` | 2230721 | `4ad3be4159310578a2db47cf179d02fa061fb98021e2f66ca933b59e7db4fb40` |
| `base-site-core-fator3-1.49.1-fonte.zip` | 4664837 | `065cad9b9f82f62432ae5c9c87662bb8213a1db3b42b84309ce9409dd69602cc` |

O instalador contém 453 arquivos sob `base-site-core-fator3/`; apenas ele é instalável. O fonte tem raiz `base-site-core-fator3-1.49.1-fonte/`, runtime idêntico byte a byte, build/testes/evidências e cópia deste relatório identificada como anterior ao fechamento. Sem ZIP aninhado.

Complemento entregue: `base-site-core-fator3-1.49.1-impacto-implantador-base.md`. O plano encerrado está no fonte. O relatório externo é a referência canônica da identidade final do fonte.
