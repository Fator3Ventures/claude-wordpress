# Entrega — Fator3 MCP LinkedIn 0.23.0

Revisão 1 · 2026-11-14 · Implementação do Pedido MCP LinkedIn 25 (CTO-1311, item 3).
Slug: `wp-mcp-linkedin-fator3` · Versão: 0.23.0 · **apta-no-escopo-testado**. Ativa no Site-Teste. O comportamento de autorização foi comprovado em WordPress, com rede do LinkedIn simulada; a operação nos ativos reais do CTO Office aguarda implantação.

## 1. De onde esta versão entra

Entrada em WordPress limpo ou atualização direta do instalador vigente 0.22.0, 442167 bytes, SHA-256 `b15cd0806b52303aa4023087ad15dfdb17709271ccdf3704f67fa63dc5b583a4`. Fonte usado como base: SHA-256 `da4ea667277a5f966a167505bf358c587bc2fae294c8199713d8536b359d77c2`. Nome, slug, basename, cabeçalho administrativo e identificadores públicos mantidos. Requisitos: WordPress ≥ 7.1.4 e PHP ≥ 8.3 de 64 bits. Runtimes efetivos do laboratório: WordPress 7.1.4, PHP 8.3.6 e MySQL 8.0.46.

Bases da rodada: instrucoes-agentes-plugins-fator3.md e padrao-desenvolvimento-plugins-fator3.md, ambas rev. 5 de 02/11/2026; regra comum, entrega da 0.22.0, Pedido 25 de 14/11, relatório e pacotes do Site Core 1.85.1. As ocorrências e horários do CTO Office citados no pedido são informações recebidas. A prova própria está na seção 4.

## 2. Convivência e encaminhamentos

| Pacote | Versão corrente testada | SHA-256 do instalador |
|---|---|---|
| Fator3 Site Core | 1.85.1 | `1fe1ba76880e7b6535af564a0fb702b823555d6307fb70d857b7081f64a4bfbd` |
| Fator3 MCP | 0.45.0 | `3659bebf22155807d12f4559cf3d9e7ef7403aec0da45fc661ad90c577c7eab9` |
| Fator3 MCP Google | 0.34.0 | `9a5f52f35a4a7c34e21e08d12099dacb05dfdfc99d3d0cc335bde95a2676135c` |
| Fator3 MCP Meta | 0.26.0 | `f1b2fc7b10dd7824c63cd4d67221d32e2b50eb2136d774dc589078d706e8a0a7` |
| Fator3 MCP Pipedrive | 0.10.0 | `7d021e6117c3dd10d8b64059fefced863736ecf90f30e89942e6e32b4569ceb4` |

A troca necessária é a do LinkedIn. O Meta estava em 0.25.0 na abertura; as notas do instalador identificam a referência usada durante o build. O inventário final e a repetição das sete suítes integradas registram 0.26.0, sem alteração no instalador LinkedIn. O teste isolado independe dos acompanhantes. Não se exige combinação com versões históricas.

A interface PHP usada pelo Core para leads e conversões e o transporte, a autenticação e o diário do MCP mantêm os seus contratos. O adaptador `includes/class-f3base-linkedin-cliente.php` coincide no fonte e no instalador oficial do Core (SHA-256 `a585e45d1f6fe5f3f0bf9fe11b019205c7305d2a64a9033b77714f1af3dac047`); a integração foi exercitada sem patch. O impacto histórico da origem dos anúncios, encerrado na 0.22.0, segue coberto pela suíte específica. A alteração atual no diagnóstico é aditiva. Não há ação técnica nova a encaminhar a outro mantenedor nem alteração em documento oficial de Core ou MCP.

## 3. Mudanças e evidência

| Pedido 25 | Comportamento entregue | Evidência |
|---|---|---|
| 1. Continuidade da concessão | O serviço revalida o administrador WordPress original e o acesso aos recursos; a troca da credencial de transporte usada para gravar a concessão não interrompe o uso. Vale para concessões anteriores e novas, inclusive no cron. A autoria completa continua gravada. | Controle negativo na 0.22.0, migração sem regravação, quatro formulários e duas modalidades de conversão. |
| 2. Aviso enquanto existir a dependência | A causa condicional foi removida. A rotação não dispara aviso Slack nem e-mail. | No aceite, nenhuma das quatro leituras autorizadas parou após a revogação. Não foram acionados destinos externos. |
| 3. Estado por consumidor | `linkedin/status` apresenta `data.consumer_grants.items`: consumidor, finalidade, conexão, recurso, revisão, estado, motivo e operação de regravação. Estados: `ready`, `blocked` e `disabled`. | Prontidão, administrador inválido, concessão desabilitada e paginação testados. `remote_checked:false`: o estado é local. |

A implementação comum está em `ConsumerGrants::authorize`. LeadReader, descoberta de formulários, conversões de aquisição e de etapas do CRM e a introspecção do serviço usam essa regra. Permanecem as verificações do administrador concedente e das permissões, conta, seleção de formulários, conexão, regras de destino e revisões. Não há transferência automática de titular, aumento de escopo nem troca de cliente Lead Sync. As operações humanas, jobs e acesso a detalhes privados mantêm seus controles de identidade. A continuação desses serviços após revogar a credencial do conector é intencional: para suspender o serviço, desabilite a concessão ou pause a conexão.

A consulta de status exige administrador e não chama o fornecedor nem grava configuração. O limite é por tipo de concessão, padrão 20 e máximo 50; usar o `next_offset` retornado para percorrer as páginas. Os contratos e as situações que exigem revisão do dono estão documentados em `CONCESSOES.md`.

## 4. Instalação e prova da troca

No [Site-Teste](https://fator3-teste-mcp-1.dreamhosters.com/) foi aplicado o ZIP da seção 8 por `plugins/upload-base64`, com `expected_slug`, `expected_sha256`, substituição e ativação. Operação `a18748a17f5a5620ab41fd0d065fb6f7`, backup de arquivos `3152104d31fba0fae9dd16f4`. LinkedIn ativo na 0.22.0 antes e na 0.23.0 depois. No encerramento: `linkedin/status {}` = `ok`, zero conexões e concessões; autoteste local 9/9; página inicial e `/wp-json/` responderam HTTP 200 na sonda de mesma origem.

**Aceite compartilhado – 17/17.** O auxiliar temporário criou uma conexão e um consumidor descartáveis, gravou a concessão pelo executor nativo com o primeiro registro OAuth do MCP, revogou esse registro e abriu um segundo. Sem sessão humana, o consumidor leu os quatro formulários autorizados sem alterar a revisão. Um quinto formulário foi recusado antes do HTTP. O ensaio também confirmou o bloqueio com titular inválido, o estado desabilitado e a recusa ao uso humano do transporte revogado. Foram cinco leituras HTTP simuladas (uma antes, quatro depois), com páginas vazias; não houve consulta a contatos reais nem login OAuth interativo. As credenciais de manutenção do site não foram rotacionadas. O resultado foi lido pela opção temporária administrativa após erro no callback auxiliar de leitura; o mesmo resultado registra 17 testes e zero falhas. As conexões e concessões de teste foram removidas, os registros MCP receberam marcas normais de exclusão e o plugin e sua opção ficaram ausentes. Permanecem apenas os registros de auditoria/backup sujeitos à retenção habitual.

| Prova em WordPress descartável | Resultado |
|---|---:|
| Regressão funcional integrada | 141/141 |
| Instalação limpa, LinkedIn isolado | 135/135 |
| Anúncio de origem, leitores e adaptador oficial do Core | 51/51 |
| Documentação completa via MCP: instalação limpa + atualização | 76/76 + 76/76 |
| Preservação de dados e recuperação de concessão anterior | 8/8 |
| Rotação e diagnóstico por consumidor | 17/17 |
| Aquisição, etapas do CRM, auditoria, autorização e paginação | 25/25 |
| **Total da matriz final** | **529/529** |

Na 0.22.0, as quatro leituras após a rotação e as três verificações do novo diagnóstico falharam: **7/17** falhas esperadas. Na 0.23.0, passaram os 17 casos. Para as suítes de liberação, nenhum aviso foi encontrado no log nativo; 38 arquivos PHP passaram no lint. A matriz final não soma repetições. A rede do LinkedIn foi interceptada; WordPress, banco, MCP e componentes integrados são reais.

**Documentação.** O laboratório percorreu todos os 50 documentos em 61 páginas por instalação, verificando conteúdo e revisão. No Site-Teste, os hashes dos 50 itens expostos pelo MCP coincidem com o instalador; `CONCESSOES.md`, `CONFIGURATION.md` e `RELEASE-0.23.0.md` foram lidos integralmente em cinco páginas e comparados byte a byte. Evidências sanitizadas: `evidence/release0230/`; comandos: README do fonte.

A frota, após autorização de publicação, confere os bytes servidos na URL prevista `https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-linkedin-fator3-0.23.0-instalador.zip` e instala com `expected_slug: wp-mcp-linkedin-fator3` e o SHA da seção 8. Não houve publicação pública nem implantação em produção nesta rodada.

## 5. Banco, migração e correção por nova versão

A mudança é de autorização durante a execução. Não há alteração de schema, regravação dos registros antigos, emissão de eventos nem aumento da revisão. Na migração direta foram preservados os bytes e as revisões de dez registros de referência, incluindo política, fila pausada, cursor, agendamento e recibo incerto. Uma concessão gravada na 0.22.0 com a credencial original já revogada retomou a leitura após a troca. A atualização não reprocessa automaticamente o período da falha. Para recuperar um fluxo real, o operador confere a última coleta, os cursores e a deduplicação do Core antes de qualquer repetição. Falhas posteriores à instalação exigem nova versão, sem downgrade.

## 6. O que permanece pendente

- **Operador do CTO Office:** instalar a 0.23.0 na janela autorizada e consultar `linkedin/status`; verificar os quatro formulários em `f3base/anuncios-verificar` e acompanhar a próxima coleta, o cursor e eventual lacuna do período. Se houver `blocked`, agir sobre o motivo indicado antes de regravar. A recuperação desse ambiente não está comprovada.
- **Administrador do ativo:** o Site-Teste não dispõe de conta LinkedIn de homologação configurada. Aprovações de produto, validade do token remoto e leitura de respostas reais continuam dependentes do fornecedor. Não houve disparo de conversão real, publicação de anúncio nem mensagem. A alteração não modifica telas e não recebeu nova inspeção visual de navegador.

## 7. Credenciais e configuração do dono

Nenhuma nova credencial é exigida nesta atualização. Em **Ferramentas → Fator3 MCP LinkedIn**, conferir a conexão, a conta e a seleção dos formulários ou ações de conversão. O administrador original deve continuar ativo no site com `manage_options`. Se ele perder o acesso, outro administrador precisa revisar a seleção e conceder expressamente na operação indicada no status; uma simples rotação do transporte não exige essa ação. Não copiar tokens de produção para o Site-Teste.

## 8. Identidade dos arquivos

- Instalador: `wp-mcp-linkedin-fator3-0.23.0-instalador.zip` · 448442 bytes · SHA-256 `7f4b6d131081169894fe73f550aa317305e60d2b64ee5aaf7ca02735dd6fc201`. Raiz única; 95 arquivos, 94 entradas no manifesto que não inclui o próprio manifesto. Rebuild reproduziu o hash aplicado ao Site-Teste, e os arquivos do runtime do fonte coincidem integralmente com o ZIP.
- Fonte: `wp-mcp-linkedin-fator3-0.23.0-fonte.zip`. 3846008 bytes · SHA-256 `7bbd20a3dc765eb8f551ec9e286eb4c3cbfe9566927da8eefe51af22ff18e8b1`. Este relatório externo é canônico; a cópia interna precede o fechamento do fonte.
