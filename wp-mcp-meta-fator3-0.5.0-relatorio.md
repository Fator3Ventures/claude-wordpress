# Entrega — Fator3 MCP Meta 0.5.0

Revisão 1 · Data/hora: 2026-10-22T19:29:00-03:00 · Rodada: implementação.
Slug/basename: `wp-mcp-meta-fator3` / `wp-mcp-meta-fator3.php`.
Status: **com-pendencias de reexecução dos runtimes mínimos**. Pedido MCP Meta 12 implementado e validado no WordPress local e no Site-Teste. O aceite editorial da aba central permanece com o dono/revisor.

## 1. De onde esta versão entra

Instalação nova ou atualização direta da **0.4.1**, base recebida e instalada no Site-Teste. Não exige versão intermediária. O incremento minor para 0.5.0 segue as normas revisão 4, de 16/10/2026, lidas integralmente: `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`. Esta rodada não regrava nenhuma entrega anterior.

| Base imutável | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-meta-fator3-0.4.1-instalador.zip | 114664 | 719e3db7bb55f58cd08c2e78420e06374a6a4b08fad693e849677783ddc82de2 |
| wp-mcp-meta-fator3-0.4.1-fonte.zip | 317219 | 79fb3d75075fe2cadc8b9b58b0dfe1a1f56901f7677ad8c9e4537e4109c6ecc7 |

Foram lidos a aba `Fator3 MCP Meta(4).md`, os relatórios recebidos e os contratos/fontes pertinentes dos acompanhantes. Os sufixos de cópia dos anexos não alteram sua identidade; inventário integral em `evidence/inputs.json`.

Ambientes executados: WordPress **7.1.3**, PHP **8.3.6 de 64 bits**, MySQL **8.0.46** no laboratório; WordPress **7.1.3**, PHP **8.3.36** no Site-Teste. Os mínimos WordPress 6.4/PHP 8.1.2 foram preservados do cabeçalho e têm prova recebida da 0.4.1, mas não foram reexecutados nesta versão. Não se afirma nova homologação dessa matriz mínima.

## 2. Convivência e encaminhamentos

| Acompanhante recebido e ativo | SHA-256 do instalador | Escopo validado nesta rodada |
|---|---|---|
| Core 1.47.0 | dd16cb720e57c2d448e78a744eb0fd761d6aff04aadeeed8309b6b5003b417c1 | ativação, coexistência e preservação |
| MCP 0.27.0 | fcf5ad0099b9490abfb8e9ea6ef83c769cad053e2ee75712efce50e219f62bc1 | registro, descoberta, execução, documentação e listas administrativas |
| Google 0.17.0 | 42bd11080b518c82e0960753fa7b08d7adae28743cfcd3e96f9b83bf3f4709b0 | ativação e coexistência |
| LinkedIn 0.6.0 | edfed426b2e0e4fce14a5c5c6241b12bed25186ab1da2102da96b2032a8af45e | ativação e coexistência |

A análise anterior ao código está em `PLAN.md`. **Zero relatórios de impacto:** não foi identificada adaptação, quebra de contrato, conflito de dados ou dependência nova em outro pacote. O MCP já consome os rótulos/descrições do registro nativo, inclusive nas telas. Não se criou uma segunda tradução no transporte. Os IDs usados por perfis e integrações permanecem iguais; não há ordem adicional de atualização dos acompanhantes.

Foram examinados registro de providers/abilities, metadados de execução, schemas, autorização, tabelas/options, bootstrap e renderização das listas. Core conserva medição, contatos e Meta Lead Ads/Pixel/CAPI; Google e LinkedIn conservam seus domínios. Meta Ads permanece fora deste pacote. Implantador não foi fornecido: `nao-avaliado`, sem risco técnico concreto identificado para encaminhamento nesta mudança de textos. Não foram modificados pacotes alheios, enviados documentos a terceiros ou publicados arquivos no repositório da frota.

## 3. Mudanças e evidência

**Causa identificada:** `Api::abilities()` montava cada rótulo com o nome do plugin seguido do identificador em inglês. O método de descrição usava uma mensagem genérica para 29 das 33 operações. O MCP exibia corretamente esses metadados defeituosos de origem. A introdução histórica dos pedidos descreve 23 operações da 0.1.0; a base efetiva 0.4.1 registra 33, todas cobertas aqui.

| Pedido exato | Mudança | Estado e evidência |
|---|---|---|
| Pedidos MCP Meta 12(a) | 33 rótulos em português, com ação e objeto; sem repetir o identificador | implementado / validado-wordpress; catálogo e listas de Clientes conectados e Registro, 33/33 em cada |
| Pedidos MCP Meta 12(b) | 33 descrições curtas específicas, com efeitos e limites pertinentes | implementado / validado-wordpress; iguais no registro, descoberta MCP e catálogo documental |
| Pedidos MCP Meta 12(c) | preservação dos 33 IDs `meta/*`, schemas e semântica | validado-localmente / validado-wordpress; comparação integral antes/depois |
| Documentação e manutenção | fonte única `includes/AbilityLabels.php`; `docs/abilities-pt-br.json` gerado; build recusa mapa incompleto ou rótulos duplicados | build reproduzido; documentação instalada conferida por hash |

Exemplos: `meta/save-schedule` → “Meta: salvar agenda de coleta”; `meta/create-backfill` → “Meta: criar carga retroativa”; `meta/rotate-token` → “Meta: renovar credencial preservando as agendas”. Identificadores técnicos continuam visíveis ao lado dos rótulos no MCP.

A comparação do código comprova que despacho, callbacks, permissões e classificações de leitura/escrita não mudaram. Os schemas JSON de entrada e saída são idênticos à base. Não houve alteração em clientes HTTP, métricas, rotação, coletas, retenção, exportações, banco ou interface gráfica própria do Meta. O acréscimo é exclusivamente o catálogo textual e sua ligação ao registro, além de versão e documentação.

Meta 10 e Meta 11 permanecem aceitos conforme a aba vigente de 21/10/2026. O relatório antigo ainda apontava comparação Porter pendente; a documentação corrente foi conciliada com o aceite posterior recebido. Esse aceite externo não é apresentado como execução própria desta rodada.

## 4. Instalação e prova da troca

Use o instalador da seção 8, `expected_slug=wp-mcp-meta-fator3` e o SHA-256 exato. Faça backup; substitua a pasta existente sem desinstalar. O fonte não é instalável. A publicação raw e a distribuição à frota ficam com o dono/frota; não houve push nesta rodada.

No Site-Teste autorizado, `plugins/upload-base64` aplicou os bytes locais do instalador final com `activate:true`, `overwrite:true`, slug/hash esperados e idempotência. Estado inicial **0.4.1 ativo**; final **0.5.0 ativo**. Operação do pacote `9c2739406b65b6362209564ca4d55e6d`; operação administrativa `fd644be1ca2c58da0993eca9`; backup recuperável de arquivos `9287d26dd5cf7cca66e500d3`. Resposta `applied:true`, `active_after:true`; sondas `/` e `/wp-json/` **200 antes/depois**, com PHP novo e desvio de cache assinado.

A reativação remota foi silenciosa, em worker independente; `activation_hook_cycle_completed=false`. O ciclo de ativação limpa foi executado no laboratório. Não se confunde a troca remota com instalação limpa ou homologação comercial.

| ID | Ambiente / cenário | Resultado | Evidência / limite |
|---|---|---|---|
| L1 | instalação limpa, Meta isolado | 97 verificações da release + 48 regressões, zero falhas | `evidence/clean/`; WordPress/PHP/MySQL reais, fornecedor simulado |
| L2 | atualização direta 0.4.1 com quatro acompanhantes vigentes | 133 verificações da release + 51 regressões, zero falhas | `evidence/upgrade/`; estado persistido comparado antes de qualquer teste do candidato |
| B1 | sintaxe, schemas, execução e build | 19 PHP válidos; despacho e schemas preservados; instalador reproduzido byte a byte | `evidence/release-verification.json` |
| S1 | atualização nativa do Site-Teste | 0.4.1 → 0.5.0, ativo e saudável | `evidence/site-tests.json`; mesmo SHA-256 dos laboratórios |
| S2 | descoberta e listas MCP | 33 habilidades exatas; 33/33 em Clientes conectados e Registro | catálogo remoto e HTML/DOM renderizado pelo WordPress; não é revisão visual de layout em navegador |
| S3 | estado, contratos e autoteste | hashes de dados/contratos iguais; oito verificações locais do autoteste aprovadas | mesma evidência; zero conexões reais antes/depois |
| D1 | documentação pelo MCP | 16 documentos, 18 páginas, bytes/hash iguais ao instalador | `evidence/site-documents.json` |
| A1 | autorização e leitura documental | 33 recusas de habilidade e quatro REST 403 para assinante por cenário; confinamento/revisão documental aprovados; zero HTTP da leitura | laboratório; não encerra a pendência da frota 20 com perfil humano real |

Total local: **329 execuções de verificações**, não 329 casos distintos. Os resultados do autoteste remoto e as páginas documentais não são somados novamente a esse total. Regressões incluem criptografia/CAS, retenção, rotação com identidade simulada, coletas, retomada, consultas diárias, exportação, administração e diagnóstico de Página.

Documentação: descubra `meta/documentation`; peça `{"document":"index"}`. Leia cada ID com `offset:0`, `limit_bytes:16384` e continue com `next_offset`/`expected_revision`. `input-schemas.json` exigiu três páginas. Catálogo português: SHA-256 `de58cad7e4d040522800cf5b087e1bc6ac95222a9fd62c46a107610ad425d080`; índice README: `b6a014b9a0d18743136dc9faa8250d63b7c0be3aaf95ae2f5bad436d8c749f06`. A ajuda local exige administrador, usa allowlist, não chama fornecedor nem grava dados.

Estado final: Meta 0.5.0, Core 1.47.0, MCP 0.27.0, Google 0.17.0 e LinkedIn 0.6.0 ativos; WP Super Cache 3.1.4, Yoast 28.7 e DreamHost Panel Login 1.0.0 preservados. `system/health` retornou `healthy:true`. A sonda MU temporária foi removida com guarda de SHA-256 e sondas; catálogo voltou a exatamente 33 habilidades, sem a operação temporária. Permanecem backups recuperáveis e registros de auditoria administrativos. Não houve fixture comercial, credencial nova, lead, anúncio, publicação ou assinatura remota.

## 5. Banco e volta de versão

Nenhuma migração ou schema novo. Conexões cifradas, agendas, histórico, resultados, opções e autorização permanecem no mesmo formato. No laboratório, a atualização preservou os bytes de registros/opções/ciphertext da base antes de exercitar funcionalidades. No Site-Teste, o digest dos dados Meta não administrativos e o digest dos contratos funcionais foram idênticos antes/depois; agenda vazia permaneceu vazia. Chamadas de diagnóstico deixam apenas a auditoria prevista pela base.

O backup de instalação cobre arquivos, não um snapshot transacional do banco; o instalador informou `database_effects_reversible=false`. Como não há migração, a volta para 0.4.1 restaura os textos antigos. Ela não apaga auditoria nem desfaz coletas ou efeitos posteriores. Preserve banco/salts e reconcilie trabalho em andamento; não restaure um banco antigo sobre filas vivas. Rollback remoto não foi aplicado.

## 6. O que permanece pendente

| Pendência | Motivo e ação | Responsável |
|---|---|---|
| Runtimes mínimos | Reexecutar WordPress 6.4/PHP 8.1.2 com a 0.5.0; prova recebida da 0.4.1 não foi contada como nova execução | manutenção/QA |
| Aceite editorial do Meta 12 | Conferir entrega e retirar o item na aba central; documento central não foi editado | dono/revisor |
| Exercícios reais anteriores da frota 20 | Rotação real, exportação do histórico, Story após expirar e 403 de assinante humano continuam sem homologação própria nesta rodada | dono/frota |
| Distribuição | Publicar/conferir instalador e relatório na raiz raw e atualizar os demais sites, com SHA-256 e slug | dono/frota |
| Implantador | Fonte não recebido; nenhuma conclusão sobre sua implementação | responsável Implantador |

Não há falha conhecida nas verificações executadas. APIs sociais reais não foram chamadas; o Site-Teste está sem conexões Meta. A mudança de textos não depende de nova credencial. Não se declara concluído trabalho ou homologação de outro responsável.

## 7. Credenciais e configuração do dono

Nenhum campo novo. Permanecem token manual, ID do aplicativo, chave secreta quando necessária e seleção explícita das Páginas/contas, em Ferramentas → Fator3 MCP Meta. Versionamento Graph, autorização por ativo, revisão esperada e proteção de segredos mantidos. Não recadastre credenciais nem recrie perfis para aplicar a tradução. Reabra as telas do MCP ou repita a descoberta para ler os metadados novos.

Painel, REST e MCP continuam exigindo `manage_options`; a lista legada de usuários não amplia essa permissão. Nenhum valor secreto, sessão, banco de laboratório ou captura pessoal acompanha a entrega.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-meta-fator3-0.5.0-instalador.zip](wp-mcp-meta-fator3-0.5.0-instalador.zip) | 122178 | 4198554e74d828609cbbe3477c569c71c86a6e7d68b7c15a2a7c77a63be116dc |
| Fonte | [wp-mcp-meta-fator3-0.5.0-fonte.zip](wp-mcp-meta-fator3-0.5.0-fonte.zip) | 365624 | c4af40c964a65561eac618bbdde9019613968afbb16cab1995ef739e4e003b91 |

Relatório externo canônico: `wp-mcp-meta-fator3-0.5.0-relatorio.md`. A cópia incluída no fonte está marcada como **anterior ao fechamento do fonte** e não contém o hash do próprio ZIP. Este relatório externo completa sua identidade sem reabrir o fonte.

Instalador com raiz única `wp-mcp-meta-fator3/`; fonte com raiz `wp-mcp-meta-fator3-0.5.0-fonte/`, runtime, build reproduzível, testes, evidências, planejamento e relatório. Nenhum ZIP contém outro ZIP. O relatório referencia somente evidências desta rodada; informações recebidas estão identificadas.

Checklist de encerramento da revisão 4 conferido em `evidence/checklist.json`: implementação, artefatos, identidades, documentação, preservação, instalação limpa/atualização, autorização e limpeza comprovadas no escopo descrito; mínimos e exercícios externos permanecem explícitos. Não se declara conformidade sem ressalvas.
