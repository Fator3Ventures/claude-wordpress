# Entrega — Fator3 MCP LinkedIn 0.17.1

Revisão 1 · 02/11/2026 · nova rodada funcional, com patch documental de fechamento. **Versão corrente da entrega: 0.17.1.** Código validado e ativo no Site-Teste; aceites com fornecedor real em ctooffice permanecem pendentes.

**Relatório externo canônico.** A cópia congelada dentro do fonte é identificada como anterior ao fechamento; seu conteúdo funcional e suas evidências são os mesmos. Tamanho/SHA-256 final do fonte foram acrescentados somente a este relatório externo, sem reabrir o ZIP.

## 1. Bases aceitas e entrada da versão

Base direta aceita: **0.16.0**, instalador de 363060 bytes, SHA-256 `beb018c0e89a6fcc25beff7d5e2955f606c78ea1cbc8148c17666dd4e9c50bc8`. Fonte recebido: 2466061 bytes, SHA-256 `5218e5d7603e4e755ebba7bdd0cfbbfa175546d22b76d149ca1b42199675a3a1`. Foram examinados os pedidos do arquivo de 02/11/2026 13:50:04, os relatórios/impactos recebidos e as normas comuns revisão 5 de 23/10/2026. Entradas imutáveis e procedência estão em `inputs/0.17.1/manifest.json`.

Entradas suportadas nesta rodada: WordPress limpo e atualização direta **0.16.0 → 0.17.1**. A 0.17.0 foi uma intermediária de validação instalada apenas no Site-Teste nesta rodada, sem distribuição à frota. A leitura de sua documentação instalada revelou referência corrente antiga e cabeçalhos desatualizados; o patch 0.17.1 corrige isso. Não é necessário instalar a intermediária. Seu instalador não foi reescrito: 377660 bytes, SHA-256 `60644b994b483b56320b0812e2080bb55d0906878d597852d53d625877070ca1`.

O plano revisão 1 e o impacto inicial antecedem a implementação e foram preservados. A revisão 5 das normas, recuperada durante a conferência final, substitui a revisão 4 inicial e foi aplicada ao fechamento: respostas e desfechos ficam neste relatório, não em impactos reemitidos apenas para comunicar atendimento.

## 2. Convivência e encaminhamentos

| Pacote original examinado | Versão | Prova desta rodada |
|---|---|---|
| Fator3 Site Core | 1.68.0 | Ativo na bancada integrada; 37 verificações de consumidor e testes de stages; ativo no Site-Teste |
| Fator3 MCP | 0.38.0 | Executor nativo, permissões, auditoria de serviço, documentação e transporte do Site-Teste |
| Fator3 MCP Google | 0.26.0 | Bootstrap integrado local e preservação no Site-Teste |
| Fator3 MCP Meta | 0.19.0 | Bootstrap integrado local e preservação no Site-Teste |
| Fator3 MCP Pipedrive | 0.5.0 | Instalador identificado/extraído localmente; não ativado na bancada PHP 8.3.6, pois exige PHP 8.3.36; ativo no Site-Teste |

Os instaladores originais são identificados por SHA-256 nos manifestos de laboratório e nas evidências. Não houve alteração em runtime, relatório central ou lista de pedidos de outro pacote. A prova de convivência de Google/Meta/Pipedrive não equivale a retestar todas as funções comerciais desses plugins. Não há ordem obrigatória de atualização dos acompanhantes para instalar esta entrega.

### Impactos e pedidos emitidos nesta rodada

Um encaminhamento técnico pertinente: `wp-mcp-linkedin-fator3-0.17.1-impacto-base-site-core-fator3.md`, revisão 2, `validacao-coordenada`, demanda aberta ao responsável Core/dono/frota. Detalha a persistência da `ownership_key` canônica de assinatura adotada, ausência de novo POST, processamento de eventos em lote e retomada das janelas após fallback de leitura. A revisão acrescenta a semântica efetiva de alias e a orientação ao consumidor à proposta emitida antes do código. Arquivo preparado, sem envio a pessoas.

Foram avaliados os contratos Lead Reader/CAPI, auditoria de serviço MCP, registro das abilities, bootstrap e isolamento dos provedores. Não foi identificado novo pedido técnico dirigido a MCP, Google, Meta ou Pipedrive; não foram gerados arquivos vazios de impacto para eles.

### Tratamento de impactos recebidos e anteriores

- **Core → LinkedIn:** `base-site-core-fator3-1.68.0-impacto-wp-mcp-linkedin-fator3.md`, revisão 2, Pedidos core 369(d). A extensão pública `linkedin-lead-campaign/1.0.0`, `resolve_campaign` e `campaign_lookup` entregues na base 0.16.0 são preservadas. Esta rodada corrige a projeção/fallback que bloqueava a leitura, com vínculo, autorização e orçamento comprovados em bancada. O produtor disponibiliza o contrato; o Core 1.68.0 consome a decoração e mantém a importação sem nome. A adoção adicional do método opcional continua responsabilidade Core, sem declaração de conclusão alheia.
- **LinkedIn → Core anterior:** `wp-mcp-linkedin-fator3-0.16.0-impacto-base-site-core-fator3.md`. O pedido de adoção do lookup opcional permanece aberto. Não foi revisado nem reentregue apenas para registrar esta resposta; a cópia recebida é histórica. As provas próprias desta rodada estão em `evidence/release0171/core` e `regression/request369d.json`.
- **Descoberta 1.2:** recebida a informação de adoção pelo Core 1.68.0 e de aceites parciais em ctooffice. A bancada confirmou o consumidor original; a nova adoção de assinaturas próprias 1.1 resolve a lacuna do produtor em código. O aceite real de formulário novo/webhook continua do dono/frota. Os itens 19 e 20, retirados da lista recebida, não foram reabertos.

## 3. Mudanças por pedido e evidência

### Pedidos MCP LinkedIn 18(g/h), preservando 18(a–f)

Nova operação administrativa **`linkedin/list-write-operations`**, local e somente leitura: exige conexão, aceita filtro de estado, limite de 1 a 50 e cursor assinado vinculado ao principal, conexão, revisão, filtro e limite. Projeta ID completo de 64 caracteres, operação, conta/Página, data, estado, revisão e efeito remoto; não retorna corpo, credenciais ou payloads do diário. Aplica a mesma propriedade/seleção do leitor existente. Não migra nem reconcilia registros durante a listagem. O painel oferece filtro, continuação e consulta pelo ID completo.

Mantidos classificação conservadora das criações recusadas, rota de encerramento explícito, revisão concorrente, validação de início e migração delimitada das intenções antigas. Testes cobrem estados, paginação, alteração de filtro, principal/conexão/ativo estrangeiro e ausência de gravação/HTTP. As duas intenções de ctooffice não foram consultadas nesta rodada; os prefixos recebidos não foram convertidos em IDs inventados.

### Pedidos MCP LinkedIn 21(d/e/f)

Descoberta inicial processa até cinco formulários por passagem, dentro do teto de 12 chamadas/20 segundos por tarefa, com checkpoint por formulário e continuação. Evento e avanço são persistidos atomicamente; sete formulários exercitam retomada. Os quatro conhecidos podem emitir seus eventos na primeira passagem quando houver orçamento.

Assinatura própria já confirmada pelo SDK 1.1 pode ser adotada: mesmo consumidor, conexão, aplicativo, conta, formulário/versão e callback; releitura remota confirma o objeto e o ID. Um alias local liga a nova intenção à `ownership_key` canônica antiga. O retorno é confirmado/adotado, sem POST duplicado. Intenção incerta, propriedade estrangeira, callback diferente ou ausência de prova permanecem bloqueadas. Upgrade real local operou primeiro a 0.16.0 pelo SDK 1.1, criou quatro recibos sintéticos, preservou seus dados e os adotou após a troca.

### Pedidos MCP LinkedIn 22(a/b/c)

O efeito da alteração é calculado por concessão e recursos usados. Mudanças apenas de formulários, opção de todos os formulários, rótulo, intervalo ou ativos alheios preservam concessões CAPI correntes, `destination_ref` e identidade de serviço. Mudanças de Ads/Pages preservam Lead Sync quando não atingem sua autorização; `campaign_lookup` continua dependente da conta Ads autorizada. Inclui concessões de etapas comerciais.

Prévia/resultado/auditoria/painel identificam `preserved`, `requires_reconfirmation`, `already_stale`, `blocked` ou `reconfirmed`, com ação. `reconfirm_conversions` e `reconfirm_leads` podem reconfirmar no mesmo commit, com prévia válida, autorização e validação remota pertinentes. Credencial, conta, regra, principal e permissões afetados continuam exigindo a proteção correspondente. Concessão já obsoleta não revive numa gravação benigna. Falha SQL/CAS reverte conexão e concessões juntas.

Os testes verificam preservação do recibo de serviço, alterações benignas, retirada da conta usada, revisão obsoleta, reconfirmação explícita e rollback. Uma expectativa histórica que invalidava a concessão ao acrescentar conta não usada foi ajustada ao pedido 22; a negativa de remoção da conta usada foi mantida e ampliada.

### Pedidos MCP LinkedIn 23(a/b/c)

A projeção solicita o caminho documentado de `leadMetadataInfo` e elimina projeções auxiliares desnecessárias. `get_response` e `read_responses` fazem **uma única repetição GET sem `fields`**, exclusivamente após HTTP 400 com a mensagem de campo projetado ausente no schema. Preservam conexão, principal, conta, formulário, versão, janela, paginação e revisão; revogação entre chamadas impede o retry. Sem decoração, campanha permanece `not_provided` e o lead continua legível.

`creation_rejected` fica restrito a transporte de criação; não aparece em GET, DELETE, atualização parcial ou evento de conversão. Outros 400, 401, 403, 404, 422, 429, 5xx e timeout não desencadeiam o fallback indiscriminadamente. O orçamento de `resolve_campaign` contempla até três GET/25 segundos quando precisa desse retry.

A forma da fixture foi conferida nas fontes primárias: [Lead Sync schema 202609](https://learn.microsoft.com/en-us/linkedin/marketing/lead-sync/lead-sync-schema?view=li-lms-2026-09), [guia Lead Sync](https://learn.microsoft.com/en-us/linkedin/marketing/lead-sync/lead-sync-api-migration-guide?view=li-lms-2026-09) e [projeções](https://learn.microsoft.com/en-us/linkedin/shared/api-guide/concepts/projections?view=li-lms-2026-09). Isso é prova de contrato documental e HTTP sintético estrito, não chamada bem-sucedida à conta real. A mensagem recebida redigia o nome do campo: não é possível atribuir com certeza a um único campo a rejeição real.

### Patch 0.17.1

Corrige a identificação da release corrente no README e cabeçalhos dos manuais. Teste documental passa a conferir essa coerência. Comparação dos instaladores: diferenças apenas em versão, documentação, catálogo documental gerado e manifesto; código funcional restante idêntico à intermediária validada. Prova em `evidence/release0171/patch-scope.json`. Total público: **99 operações**; contratos Lead Reader 1.0/1.1/1.2 e CAPI existentes preservados.

## 4. Instalação e prova de prontidão

### Matriz local

| Cenário | Resultado |
|---|---|
| Build/lint | 35 arquivos PHP válidos; build determinístico; runtime fonte igual ao instalador |
| Limpa integrada, WP 7.1.4/PHP 8.3.6 | 47 casos dirigidos, zero falhas |
| Upgrade direto 0.16.0 → 0.17.1 | 49 casos, zero falhas; quatro recibos 1.1 preservados/adotados, zero novo POST |
| Regressão integrada | 443 verificações declaradas, zero falhas; caso histórico específico de upgrade 0.10.1 marcado não aplicável à instalação limpa |
| Consumidor Core 1.68.0 original | 37 verificações, zero falhas |
| Mínimo isolado WP 6.4/PHP 8.1.2 | 46 casos dirigidos, zero falhas; Abilities API ausente no WordPress mínimo |
| Regressão mínima complementar na intermediária 0.17.0 | 135 verificações declaradas, zero falhas, duas não aplicáveis; código funcional comprovadamente igual no patch |
| Interface final | 54 verificações, zero falhas; HTML/JS reais, REST autenticado, jsdom 27.4.0; não é inspeção visual em navegador |
| Documentação por MCP nativo local | 40 documentos, 48 páginas, 61 verificações, zero falhas; conteúdo/hash/bytes, versão corrente e ausência de HTTP |

Todos os ambientes finais conferiram byte a byte os arquivos instalados contra o instalador 0.17.1; logs do pacote e dos acompanhantes sem entradas de erro nas execuções finais. Evidências completas em `evidence/release0171`. Runtimes e WordPress externos têm hash nos manifestos. Fixtures usam respostas sintéticas; não enviam conversões, publicações, anúncios ou assinaturas reais.

Os cenários de concessões e o consumidor Core executam em bancos descartáveis separados para evitar colisão intencional do guard global de assinaturas entre fixtures. Na revisão dos testes foram corrigidas expectativas de versão e identificação de cabeçalho de contrato como versão do plugin. As execuções finais citadas usam as correções e não mascaram falhas de runtime.

### Site-Teste

Destino autorizado: `https://fator3-teste-mcp-1.dreamhosters.com/`, via **WP MCP fator3-teste**. Inventário e estado foram lidos antes de cada alteração; as duas trocas foram sequenciais, restritas ao slug LinkedIn, com `plugins/upload-base64`, `overwrite:true`, `activate:true`, `expected_slug`, SHA-256 exato e chave idempotente própria. Sem limpeza de banco compartilhado.

| Passagem | Recibo da operação | Backup de arquivos |
|---|---|---|
| 0.16.0 → intermediária 0.17.0 | `ac0ce400faa4e1a59a6cb2ba89c6255a` | `3507116a65e71ac822098593` |
| 0.17.0 → final 0.17.1 | `237b66a39db3d7cfc8be4ff7a2582dba` | `d4cc716782f5a639aceb51fc` |

Ambas retornaram `applied:true`, `recovery_status:applied`, plugin ativo e sondas da raiz e `/wp-json/` com HTTP 200 antes/depois, em requisições PHP frescas com bypass de cache. São sondas internas da mesma origem; não certificam acesso público externo nem prontidão comercial.

Conferência independente final: **82 arquivos esperados** do pacote correspondem ao instalador — 41 de código/ativos, 40 documentos e o manifesto. Os 40 documentos foram lidos integralmente por `linkedin/documentation` em **42 páginas**; conteúdo UTF-8, bytes e SHA-256 coincidem com o ZIP. A diferença de páginas para a bancada decorre do limite de 65536 versus 16384 bytes. A nova ability está registrada na versão 0.17.1 como somente leitura.

Estado final: versão **0.17.1**, `state:ok`, armazenamento/criptografia/auditoria prontos, provedor de auditoria de serviço registrado, `issues:[]`, zero conexões, zero agendas ativas e fila sem pendência de migração. Core/MCP/Google/Meta/Pipedrive mantiveram versão, estado ativo e hash do arquivo principal entre antes/depois; não se afirma inspeção integral de seus arquivos. Evidências em `site-teste.json` e `installed-documentation.json`.

## 5. Banco, preservação e reversão

Schema SQL 2 e tabela própria preservados; sem tabela nova ou mudança de schema de outro pacote. São adicionados registros `subscription_alias` no armazenamento próprio e metadados de efeito/concessão no fluxo existente. Checkpoints de descoberta e rebases usam revisão/locks/transação. A leitura do diário não altera registros. Migrações conservadoras anteriores permanecem.

O upgrade comparou primeiro as identidades de conexão, grant, recibo e guard antes de operar a nova descoberta. A adoção depois atualiza somente o vínculo autorizado e cria alias, sem fabricar autoria ou refazer POST.

O backup do instalador é de arquivos; `database_effects_reversible:false` foi explicitado pelo MCP. Voltar arquivos não desfaz concessões, cursores, outbox, aliases ou efeitos remotos. Para reversão fiel, coordenar pausa dos workers, backup/restauração correspondente do banco e salts/chaves, além dos arquivos. A versão 0.16.0 não entende os aliases novos e pode voltar a bloquear a descoberta; não reexecutar criação para contornar essa situação. Nenhum rollback foi aplicado no Site-Teste.

## 6. Pendências e responsáveis

| Pendência | Responsável / aceite necessário |
|---|---|
| 18(c), intenções `ea7838f5…` e `66c4c78e…` | Dono/frota em ctooffice: localizar IDs completos pela nova lista e conferir `rejected`, ou encerrar explicitamente pela rota existente; sem apagar recibos |
| 21, formulário novo e webhook real | Dono/frota/Core: quatro recibos existentes adotados sem duplicação; novo formulário entra sem seleção manual e lead autorizado chega uma vez |
| 22, CAPI real após edição só de leads | Dono/frota: `linkedin/diagnose-conversions` permanece `ready:true` na conexão autorizada |
| 23, leitura real e recuperação das quatro janelas | Dono/frota: as duas rotas da resposta informada retornam 200; Core retoma quatro formulários com `falhas:0`; confirmar comportamento real da projeção |
| Lookup opcional de campanha | Responsável Core: adoção complementar conforme impacto 0.16.0 e 369(d), sem ampliação implícita de privilégio |
| Aceites antigos com conta real | Dono/frota: autorização por tela, nova gravação manual sem e-mail, conversões de aquisição/etapas, Lead Sync e acervo real; pendências 20/92/116 recebidas permanecem fora desta homologação |

O Site-Teste não tem conexão LinkedIn configurada; por isso não foi usado como prova de fornecedor. Não houve instalação em ctooffice ou nos demais sites, push ao repositório público, criação de contato comercial sintético, gasto Ads, publicação ou envio real de conversão. A entrega à frota deve conferir o SHA-256 do artefato servido antes de instalar; essa publicação é do responsável pela frota.

## 7. Credenciais

Nenhum valor secreto é necessário no relatório ou nos ZIPs. Tokens/client secret/refresh continuam cifrados e não aparecem nas projeções; o painel não devolve valores salvos. A bancada usa exclusivamente identidades e credenciais sintéticas. Acesso real depende das concessões/contas/produtos do aplicativo e da aprovação do LinkedIn. A entrega não concede novos escopos ou `campaign_lookup` automaticamente.

## 8. Artefatos finais

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| `wp-mcp-linkedin-fator3-0.17.1-instalador.zip` | 379078 | `e3a6c06d2c254a50af60e434a0575424e552ed4f62422ea1aabcff6bd591f1f9` |
| `wp-mcp-linkedin-fator3-0.17.1-fonte.zip` | 2682300 | `a7a96acae25a6d4003548677b5b14ff7c8769f216c4440178558cf948002c163` |

Complementam a entrega este `wp-mcp-linkedin-fator3-0.17.1-relatorio.md` e `wp-mcp-linkedin-fator3-0.17.1-impacto-base-site-core-fator3.md`. Apenas o instalador é instalável. Raízes ZIP: `wp-mcp-linkedin-fator3/` e `wp-mcp-linkedin-fator3-0.17.1-fonte/`. Fonte inclui código/build, runtime igual ao instalador, testes, evidências sanitizadas, entradas e esta cópia anterior ao fechamento; não contém ZIPs aninhados, banco, dependências externas ou segredos. O hash final do fonte pertence somente ao relatório externo canônico.
