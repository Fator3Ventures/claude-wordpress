# Entrega — Fator3 MCP Meta 0.26.0

Revisão 1 · 2026-11-14T02:30:40-03:00 · Implementação e homologação do pedido MCP Meta 29 / CTO-1311, item 3.  
Slug: wp-mcp-meta-fator3 · Build público: 0.26.0 · **apta-no-escopo-testado**.

## 1. De onde esta versão entra

Instalação limpa e atualização direta da versão corrente 0.25.0. Base conferida: instalador de 268364 bytes, SHA-256 `8ff54d9ec66f29c78982b6c15577436a51b934c54c73cebe88227449580ea530`; fonte de 876790 bytes, SHA-256 `397153c833f2a80101174c1371073a5aa0cdfd282eb1eee57ea59ad9ed54dc70`. Requisitos: WordPress ≥ 7.1.4, PHP ≥ 8.3 de 64 bits. Teste nativo: WordPress 7.1.4, PHP 8.3.6 de 64 bits, MySQL 8.0.46. As duas normas do projeto foram lidas na revisão 5 de 02/11/2026. O pedido 29 recebido em 14/11 está em inputs/pedido-mcp-meta-29.md.

## 2. Convivência e encaminhamentos

Conjunto ativo confirmado no Site-Teste e exercitado em WordPress isolado: Core 1.85.1, MCP 0.45.0, Google 0.34.0, LinkedIn 0.22.0, Pipedrive 0.10.0 e Meta 0.26.0. Apenas o Meta foi substituído. O Core registra seus leitores nos mesmos ganchos e mantém a responsabilidade por contatos e atribuição. O pedido 29 altera a validação de uma concessão local do Meta; a autorização de gravações pelo MCP continua em vigor. Nenhuma alteração identificada como necessária nos acompanhantes. Nenhum novo relatório de impacto.

| Instalador acompanhante | SHA-256 |
|---|---|
| base-site-core-fator3-1.85.1-instalador.zip | `1fe1ba76880e7b6535af564a0fb702b823555d6307fb70d857b7081f64a4bfbd` |
| wp-mcp-fator3-0.45.0-instalador.zip | `3659bebf22155807d12f4559cf3d9e7ef7403aec0da45fc661ad90c577c7eab9` |
| wp-mcp-linkedin-fator3-0.22.0-instalador.zip | `b15cd0806b52303aa4023087ad15dfdb17709271ccdf3704f67fa63dc5b583a4` |
| wp-mcp-pipedrive-fator3-0.10.0-instalador.zip | `7d021e6117c3dd10d8b64059fefced863736ecf90f30e89942e6e32b4569ceb4` |
| wp-mcp-google-fator3-0.34.0-instalador.zip | `9a5f52f35a4a7c34e21e08d12099dacb05dfdfc99d3d0cc335bde95a2676135c` |

O fonte do Core fornecido corresponde ao SHA-256 `7500da4e768b73d5e6d1b05fd8b3d08e6a316b8366ce6262ba246e104e135855`. Os pedidos 400/401 do Core tratam da normalização do telefone/e-mail na captura; o relatório recebido mantém inalterados os formatos de chamada desses plugins. A prova própria desta rodada se restringe aos fluxos exercitados.

## 3. Mudanças e evidência

| Pedido 29 | Implementação | Evidência |
|---|---|---|
| 1 · Concessão sobrevive à troca do conector | O transporte é validado ao salvar, inclusive antes da persistência. A leitura do consumidor registrado revalida o administrador WordPress responsável e o escopo da concessão, sem exigir a antiga credencial MCP. Novas concessões não armazenam a política de transporte; as existentes são interpretadas sem regravação. | Na 0.25.0, a rotação derrubou os dois leitores; 12 das 20 asserções do novo comportamento falharam. As mesmas 20 passaram na 0.26.0, incluindo leitura de linhas de anúncios, de atividade e de dataset em histórico não vazio. |
| 2 · Aviso enquanto persistir a dependência | A dependência foi eliminada para os dois leitores, inclusive registros antigos. A condição para criar aviso de rotação no Slack e no admin_email deixou de existir. Não há envio externo novo. | A credencial A efetivamente revogada deixou de autenticar, as leituras continuaram, e a concessão não precisou de reparo. |
| 3 · Estado por concessão | meta/health lista consumer_grants com consumidor, conexão, conta, recurso, revisão, enabled, estado, motivo e operação de reparo. Concessões ativas e impedidas degradam o estado geral; desligadas não degradam. O Diagnóstico informa o número de ativas prontas. | Situações ready, blocked e disabled verificadas. Divergência de revisão observada nos dois leitores do Site-Teste. Retirada de manage_options do responsável bloqueou as leituras em laboratório. |

A validação de escopo, dataset e permissão separada para anúncio de origem permanece. Jobs, exportações, agendas e gerenciamento de credenciais mantêm suas próprias regras. A resposta de saúde não contém o usuário gravador, segredo ou identificação da credencial de transporte. Detalhes: manuais instalados SDK-PHP, CORE-MONITORING, META-ADS-READER, MIGRATION e CHANGELOG.

## 4. Instalação e prova da troca

No Site-Teste usamos plugins/upload-base64, com o ZIP da seção 8, sobrescrita, ativação, expected_slug=wp-mcp-meta-fator3 e seu expected_sha256. Trata-se de instalação direta autorizada no teste; nenhuma URL raw foi usada. Distribuição raw pela frota não executada. Recibo `8ba9906e6c5925640a0b2056db99315a`: 0.25.0 ativa → 0.26.0 ativa, operação complete. Página inicial e /wp-json/ retornaram 200 antes e depois.

| Ambiente | Teste | Resultado |
|---|---|---|
| WordPress isolado com MCP oficial | Rotação de concessão OAuth de teste; histórico não vazio, privilégios atuais, concessões anteriores e negativas | 20/20 na candidata |
| WordPress isolado | Migração direta, instalação limpa, origem de anúncio com Core, conjunto completo de acompanhantes, navegador, regressões de coletas, permissões, documentação, build | 400/400; inclui 18 de migração, 38 do leitor de origem e 7 no navegador |
| Site-Teste | Autenticar A, conceder as duas leituras pela política MCP, autenticar B, revogar A, conferir B e consultar os dois históricos sem regravar; mudar a revisão do consumidor e testar revogação explícita | 11/11. Senhas de aplicativo WordPress reais e políticas MCP temporárias de escopo limitado; consumidor, conta e seleção sintéticos. O histórico dessa conta de teste estava vazio. |
| Site-Teste | meta/health, meta/selftest, ajuda via meta/documentation, plugins/list e plugins/operation-status | Saúde ok; autoteste local aprovado; os 32 documentos foram reconstruídos em 40 páginas, 303449 bytes. Em todos os casos: revisão, bytes e SHA-256 iguais aos do instalador. |

Total: **420 verificações no laboratório + 11 no aceite do Site-Teste**. O auxiliar e as concessões do teste foram removidos. Não restaram conexões Meta, concessões de consumidor nem senhas temporárias ativas; as entradas de política MCP eliminadas deixam o marcador técnico deleted e a auditoria é preservada. A primeira execução do auxiliar interpretou esse marcador como resíduo ativo: corrigiu-se a verificação do auxiliar e repetiu-se o aceite. Isso não alterou o Meta instalado. O plugin auxiliar não integra o instalador. Evidências em evidence/026, particularmente grant-base.json, grant.json, migration.json, site-teste.json e documentacao-mcp.json.

## 5. Banco, migração e correção por nova versão

Sem alteração de esquema, retenção ou prazo de credenciais. Concessões já salvas preservam responsável, revisão, ativos e decisão explícita sobre consulta por ID. A eventual política de transporte gravada no valor antigo não é consultada na leitura do SDK. Ao salvar novamente o registro, o Meta grava apenas a identidade administrativa necessária. Um cursor antigo vinculado à identidade de transporte pode exigir reinício da paginação. Não se revivem concessões desativadas. A atualização com dados conservou registros, histórico, opções e concessões; a base sintética foi descartada. No Site-Teste, exportaram-se as duas tabelas do Meta (586 linhas) e 8 opções antes da instalação. Backups ficam no ambiente; nenhum valor secreto integra a entrega. Correção após instalação será feita por nova versão, sem downgrade.

## 6. O que permanece pendente

O aceite do pedido 29 no Site-Teste foi concluído. A implantação nos sites de produção, inclusive CTO Office, cabe à frota. Nenhuma alteração nessa rodada foi feita em produção. Não houve chamada à Graph para homologar o pedido 29, que trata exclusivamente da leitura e da autorização locais. A pendência histórica do pedido 28 (conferir a ficha e a mídia atuais da Korvena) é independente; não foi reaberta nem declarada atendida por estes testes.

## 7. Credenciais e configuração do dono

Em Ferramentas → Fator3 MCP Meta → Suporte → Diagnóstico, confira o estado das concessões antes de agir. Em meta/health, filtre consumer_grants por consumidor, conta e recurso. ready indica leitura local pronta; disabled indica revogação; blocked indica concessão habilitada com pré-condição inválida. Para not_authorized, confira se o responsável ainda é administrador. Se houver mudança intencional de responsável ou de seleção, confira o escopo e use meta/save-ads-grant ou meta/save-monitoring-grant com a revisão atual; habilite consulta externa por ID somente quando necessária. Uma simples troca de credencial do conector administrativo não exige regravação.

## 8. Identidade dos arquivos

| Artefato | Nome | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-meta-fator3-0.26.0-instalador.zip](wp-mcp-meta-fator3-0.26.0-instalador.zip) | 270792 | `f1b2fc7b10dd7824c63cd4d67221d32e2b50eb2136d774dc589078d706e8a0a7` |
| Fonte | [wp-mcp-meta-fator3-0.26.0-fonte.zip](wp-mcp-meta-fator3-0.26.0-fonte.zip) | 931503 | `6fad93bdefb3dc67404fa21340bf3253750aa4ee5c25bc7234b3823ae9ed94f3` |

Relatório externo canônico. A cópia no fonte foi congelada antes do empacotamento; os valores definitivos estão nesta tabela.
