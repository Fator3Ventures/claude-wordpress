# Entrega — Fator3 MCP LinkedIn 0.25.0

Revisão 1 · 2026-11-17T11:49:54-03:00 · Implementação · **apta-no-escopo-testado**. Slug: `wp-mcp-linkedin-fator3`. O instalador está ativo no Site-Teste. O aceite operacional nos sites da frota depende da distribuição e da observação pela frota.

## 1. De onde esta versão entra

Instalação limpa ou atualização direta da **0.24.0**, identificada pelo fonte e instalador oficiais e pelo inventário antes da troca. Instalador-base: 452765 bytes, SHA-256 `0836ea7805e16671a5ef33cd0a5152fd6a78e96862f9296616bd5f8d8205dcc9`; fonte-base: 9660303 bytes, SHA-256 `8ec04cc497165b18235948c4eb0187a9829734eab0e50efabdaee8eb5d957ce1`. WordPress mínimo 7.1.4; PHP mínimo 8.3 de 64 bits. Laboratório: WordPress 7.1.4 e PHP 8.4.24. No Site-Teste: WordPress 7.1.4 e PHP 8.3.36; as provas específicas de cada ambiente estão na seção 4.

Lidos: `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, revisão 5 de 02/11/2026, além da Regra comum, da aba do LinkedIn, da última entrega e do pedido/impacto do Core. O pedido visual **Pedidos MCP LinkedIn 26** já integra a base. O pedido novo identificado é **Pedidos core 423(e)**; atribuído ao número original, sem criar um pedido LinkedIn 27.

## 2. Convivência e encaminhamentos

| Pacote | Versão no inventário final e na prova de integração | SHA-256 do instalador de laboratório |
|---|---|---|
| Fator3 Site Core | 1.91.0 | `5d0358f62d42a9232ee1bce216bd8ea2b41ea284bc16ef454ad8f9c103aa3e41` |
| Fator3 MCP | 0.46.0 | `0c595a473dc9edd1b97e5be206a904b0afa79d8d9ee5553490a2ca6a5b7d5da8` |
| Fator3 MCP Google | 0.36.0 | `b066ed24418a1eccaa3c93504e5d817c1e06cf2e4993787fae68201e6a35ac27` |
| Fator3 MCP Meta | 0.28.0 | `4c43ae254e2ad31797e7c83962aa6da6ea75b7d64587d17280e654ea3f35108b` |
| Fator3 MCP Pipedrive | 0.11.1 | `02fc0692722488de17174a59b58b80217a5609f2c8a4a586ca6016951532dcc5` |
| WP Activity Log | 5.7.0 | `3722caffd456971710ade04ab296c7e95bec1c40a00cd8567e93a2f006c530f1` |

**Impacto recebido:** `base-site-core-fator3-1.91.0-impacto-wp-mcp-linkedin-fator3.md`, revisão 1, no diretório `inputs/0.25.0/` do fonte. O Core entregou um patch experimental (SHA-256 `f43111193287139547024c62ac335e6c58ee0b3f09123fd637082904627a8738`) com dez verificações controladas relatadas pelo emissor. Foi incorporada uma solução equivalente na release oficial LinkedIn e ampliada para a remoção nativa. **Ação do mantenedor LinkedIn atendida.** A cópia do documento do emissor permanece a original. Recibos e reprodução próprios: `evidence/release0250/cron2.json`, `prior2.json` e `matrix.json`. O aceite de campo da frota permanece em aberto. Nenhuma alteração correspondente precisa ser implementada pelo Core, MCP ou por outro pacote; não há novo impacto individual de saída.

O Meta 0.27.0 estava ativo no inventário inicial. O mantenedor do Meta instalou a 0.28.0 durante a rodada; o inventário final a mostra ativa, e a integração, cron, documentação e migração foram revalidados em laboratório com essa versão. A troca dos pacotes não exige ordem específica para a correção do LinkedIn. A seleção do cliente Lead Sync continua explícita por integração. Callbacks, deduplicação, contatos e efeitos comerciais permanecem no Core.

## 3. Mudanças por pedido e evidência

**Pedidos core 423(e): `f3_linkedin_worker` e `f3_linkedin_lead_discovery`.** Fixado o horário da tentativa; a confirmação usa hook, argumentos vazios e timestamp. Se a API informar `could_not_set`, só o evento exato permite declarar sucesso. Uma ocorrência já conhecida continua reaproveitável; se houver uma duplicata concorrente em outro horário, somente o worker conserva a convenção anterior de reaproveitá-la. A rotina de descoberta passou a solicitar o erro nativo explicitamente. Uma falha de outra natureza ou um retorno positivo sem evento verificável não confirmam uma nova gravação.

Na remoção nativa, o sensor pode apagar o retorno de um filtro que já persistiu a exclusão. O observador do LinkedIn reconhece a passagem da ocorrência exata de existente para ausente. Se o filtro preservou um resultado, o pacote o respeita; recusas observadas antes do sensor tardio também são preservadas. O observador cobre exclusivamente os dois hooks próprios com argumentos vazios. Não altera o sensor, a opção cron diretamente nem o mecanismo global de log. Código em `includes/CronOccurrences.php`, `Query.php`, `LeadDiscovery.php` e `Worker.php`; registro em `wp_loaded`.

| Ocorrência | 0.24.0, com gravador antecipado e sensor real | 0.25.0, mesmo cenário | Recibo do processamento |
|---|---|---|---|
| Worker | Nativo informou `could_not_set` após remover | Remoção confirmada, sem evento de erro | 1 callback, lote vazio, 0 itens processados; a segunda passagem não repetiu o callback |
| Descoberta | Nativo informou `could_not_set` após remover | Remoção confirmada, sem evento de erro | 1 callback, tarefa ainda não vencida, cursor preservado, novo tick agendado. Em prova separada com tarefa vencida e conexão sintética ausente: 1 tentativa, 1 erro, cursor preservado |

`linkedin/status` separa a agenda em `data.cron_worker` e `data.cron_lead_discovery`: tentativa, código original, confirmação, próxima ocorrência, remoção reconciliada e última execução. O diagnóstico só lê. Foram preservados os hooks, os locks, as 100 operações, os três schemas JSON, as rotas, os nomes das opções preexistentes, a capacidade administrativa e o contrato de `linkedin/save-connection`. A UI e seus assets permanecem idênticos aos da 0.24.0. Guias instalados: `WORKER.md`, `MIGRATION.md` e `RELEASE-0.25.0.md`.

## 4. Instalação, prontidão e provas

No [Site-Teste](https://fator3-teste-mcp-1.dreamhosters.com/), a atualização autorizada usou o ZIP da seção 8 via `plugins/upload-base64`, com `expected_slug=wp-mcp-linkedin-fator3`, SHA-256, chave de idempotência, ativação e sobrescrita. Operação `9c4d0a7c06b34c34a45e320761b5bd32`, cópia prévia de arquivos `79a9be81acfd1e51fe3d1869`. Confirmada a passagem 0.24.0 → 0.25.0. O inventário final mostra os pacotes da seção 2 ativos. Página inicial e `/wp-json/`: HTTP 200 antes e depois. `linkedin/status {}` devolveu `ok`, zero conexões; sem worker ou descoberta necessários. `system/health`: saudável. `linkedin/selftest`: 9/9. Nenhuma fixture nem credencial foi criada no ambiente compartilhado.

| Teste próprio | Verificações aprovadas | Evidência em `evidence/release0250/` |
|---|---:|---|
| Instalação limpa, pacote isolado, funções próprias, administração e autorização | 135/135 | iso.json |
| Funções e contratos com os acompanhantes vigentes | 141/141 | int.json |
| Migração direta e preservação de dez registros sintéticos | 8/8 | mig.json |
| Documentação pelo executor MCP em instalação limpa e após atualização | 78/78 + 78/78 | docsnew.json, docs.json |
| Cron: criação, remoção, identidade, recusa, processamento e retomada | 44/44 | cron2.json |
| **Total da 0.25.0 em laboratório** | **484/484** | matrix.json |

Controle de reprodução na base: 17 verificações confirmaram os resultados esperados, incluindo **dois erros nativos** no log. Na candidata, nenhum dos dois ocorreu; nenhum aviso PHP atribuído ao LinkedIn nas provas finais. O teste executou duas vezes o arquivo **wp-cron.php do WordPress**, em processos novos, com o WP Activity Log 5.7.0 ativo e os dois callbacks reais de remoção observados. Um gravador de teste no WordPress descartável reproduziu a persistência antecipada; outros cenários injetaram respostas controladas para exercitar os limites. Isso reproduz o mecanismo e o resultado; não identifica qual componente executou a primeira gravação em cada site da frota.

O leitor MCP entregou **52 documentos em 63 páginas** em cada instalação do laboratório, com conteúdo comparado à árvore instalada. No Site-Teste, a descoberta e o schema da operação foram consultados; os 52 hashes do índice corresponderam ao ZIP e o guia do worker e as notas 0.25.0 foram lidos por inteiro e comparados byte a byte. Instalação verificada contra a árvore de runtime: 98 arquivos, 97 hashes no manifesto que exclui a si próprio, lint de 39 PHP e três schemas JSON idênticos à base. Reprodução na raiz do fonte, em README.md.

Na frota, publicar o instalador e relatório conforme o fluxo autorizado, conferir o hash dos bytes servidos em `https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-linkedin-fator3-0.25.0-instalador.zip` e só então usar `plugins/upload` com `expected_sha256` e `expected_slug`. Não se verificou uma publicação raw nesta rodada.

## 5. Banco, migração e correção por nova versão

Schema físico 2 inalterado. Nenhuma migração estrutural ou reativação do que estava pausado. A conferência da migração comparou chaves, revisões, carga cifrada e validade de dez registros. Os novos recibos operacionais gravam horários, estados e códigos no momento pertinente, sem novos dados pessoais ou credenciais. Uma remoção reconciliada não comprova entrega ao fornecedor. Em falha, preservar dados, salts, filas, cursores e recibos; controlar o fluxo afetado e corrigir em nova versão, sem downgrade nem repetição de efeitos incertos.

## 6. Pendências e limites

A frota deve distribuir e verificar, em sites com trabalho elegível, que os dois hooks não gerem o erro espúrio e que itens avancem conforme seus recibos. O Site-Teste tem zero conexões; não comprova tráfego sob carga representativa da frota. A matriz de falhas de cron rodou no laboratório em PHP 8.4.24; no PHP 8.3.36 do Site-Teste foram validados instalação, status, documentação e autoteste. Conta real, aprovação de Lead Sync, desafio/assinatura de webhook, lead, anúncios e conversões reais não foram exercitados. Nenhuma produção foi alterada.

## 7. Credenciais e configuração do dono

Nenhuma nova credencial. Em **Ferramentas → Fator3 MCP LinkedIn → Conexões**, o dono informa token e, se aplicável, segredo da aplicação e token de renovação. O operador configura ID do aplicativo, seleção de ativos/formulários e concessões. Produtos, escopos e papéis devem estar aprovados pelo LinkedIn para o ativo. O cliente Lead Sync depende da escolha explícita, webhook e assinatura válidos; a renovação de acesso mantém suas guardas. Não é necessário preencher campos para consultar a documentação ou diagnosticar a agenda local.

## 8. Identidade dos arquivos

| Artefato | Arquivo | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador WordPress | [wp-mcp-linkedin-fator3-0.25.0-instalador.zip](wp-mcp-linkedin-fator3-0.25.0-instalador.zip) | 456330 | `81bc69ed098198b056d93549dd5fa0317adfef2edc0937d33cdd0d0c21f801bb` |
| Fonte | [wp-mcp-linkedin-fator3-0.25.0-fonte.zip](wp-mcp-linkedin-fator3-0.25.0-fonte.zip) | 9749568 | `71f58d4757f6b847ac0ab413e1b1eb4c8399cfb6b9f89b3211c1eb8e31918a4a` |

Relatório externo canônico. A cópia congelada no fonte foi gerada antes do fechamento desse ZIP.
