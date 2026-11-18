# Entrega — Fator3 MCP Meta 0.29.0

Revisão 1 · 2026-11-18T17:28:13-03:00 · Implementação · `wp-mcp-meta-fator3` · **Apta no escopo testado; aceite da frota pendente.**

## 1. De onde esta versão entra

Instalação limpa ou atualização direta **0.28.0 → 0.29.0**. Instalador-base oficial: SHA-256 `4c43ae254e2ad31797e7c83962aa6da6ea75b7d64587d17280e654ea3f35108b`. Cabeçalho, pasta, basename, rotas e Text Domain preservados. Requisitos: WordPress ≥ 7.1.4, PHP ≥ 8.3 de 64 bits. Instalação limpa, atualização e provas de domínio em WordPress 7.1.4, PHP 8.4.27, MariaDB 11.8.6. Instalação compartilhada em WordPress 7.1.5 e PHP 8.3.36. Instruções comuns e padrão completo lidos na revisão 5 de 02/11/2026; aplicadas também a regra comum e a aba do Meta.

## 2. Convivência e encaminhamentos

| Pacote | Matriz local ativa | Site-Teste |
|---|---|---|
| Core | 1.93.0 | 1.93.0 |
| MCP | 0.48.0 | 0.48.0 |
| Google | 0.36.0 | 0.36.0 |
| LinkedIn | 0.26.0 | 0.26.0 |
| Pipedrive | 0.12.0 | 0.11.1 |

Foram conferidos os cabeçalhos, hashes dos novos ZIPs fonte/instalador e seus relatórios (evidence/029/inputs.json). O Pipedrive 0.12.0 foi exercitado na matriz local; não é dependência das coletas do Meta. A única atualização nesta rodada no Site-Teste foi a do Meta. O Core 1.93.0 já implementa o contrato público de incidentes recebido no Pedido Core 430 (impacto de entrada, revisão 2). Para entrega imediata dos avisos, instalar o Core e configurar o e-mail técnico antes da troca do Meta. Sem central disponível, o Meta conserva as transições para a próxima notificação. Nenhuma mudança de código, configuração específica nova ou novo encaminhamento para LinkedIn, MCP, Pipedrive ou Google foi identificado. A publicação e escrita de anúncios, Pixel/CAPI e leads nativos permanecem fora desta mudança.

## 3. Mudanças e evidência

| Pedidos MCP Meta 31 | Mudança | Evidência própria |
|---|---|---|
| (a–b) Agenda, job, carga retroativa, resultado e exportação | O site executa com um administrador atual, revalidando a conexão e os ativos. A identidade MCP original conserva sua função de auditoria. Se faltar capacidade ao autor, outro administrador assume e o Core recebe um aviso. A leitura de objetos privados usa o acesso atual; conjuntos de dados exigem também a conta de anúncios. | A foi revogada no MCP, B leu o job, os bytes exportados e o histórico antigos; o job e a carga completaram; outro administrador leu os resultados. Acesso por usuário rebaixado, concessão revogada e ativo removido foi recusado. |
| (c) Atualização sem regravação | Adoção dos objetos existentes; coletas pausadas por recusa local de autorização voltam à fila. Checkpoints, arquivos concluídos, seleção e pausas explícitas são preservados. A leitura reúne o acervo orgânico anterior por conexão, canal e ativo. | Reproduzido `not_authorized` na 0.28.0. A agenda executou na próxima passagem da 0.29.0 sem salvar de novo. Uma exportação com a primeira parte já gravada na base terminou com duas partes e duas linhas distintas. |
| (d) Revisão de edição | A revisão pública muda ao editar a agenda. As gravações do worker usam um controle interno de concorrência. | A revisão pública da base, 3, continuou 3 depois do sucesso e de uma falha real por ativo removido. Salvar com 3 funcionou; a repetição com 3 retornou `revision_conflict`. |
| (e, g) Avisos do worker, manutenção e credencial | Abertura e recuperação passam ao destino técnico do Core pelo filtro `f3base_incidente_publicar_v1`. A identidade dos incidentes coincide com a observação periódica do Core. Estado pendente fica registrado se o Core estiver ausente ou ocupado. | Core oficial, correio interceptado no laboratório: uma abertura e uma recuperação apesar de observações repetidas de ambos os plugins. Na ausência da central as duas transições esperaram e foram entregues na ordem quando ela voltou. Zero chamadas HTTP/Slack no ensaio. |
| (f) Stories e conversas | O arquivo e os recibos pertencem à conexão e ao ativo. O cron tenta de novo depois de falha anterior ao callback; recibos incertos continuam exigindo reconciliação. | Story e miniatura de revisão anterior legíveis pelo administrador atual. Uma falha simulada da Graph gerou nova tentativa. Repetir a execução entregou o evento ao consumidor de teste uma única vez. |

**325 verificações automatizadas aprovadas** nas suítes abaixo. Esta contagem não inclui a reprodução do defeito na base, lint, backups ou sondas do Site-Teste.

| Suíte | Verificações |
|---|---:|
| Propriedade e migração na base oficial | 30 |
| Rotação entre concessões na candidata | 8 |
| Incidentes com Core real | 6 |
| Aviso e recuperação de administrador substituto | 2 |
| Controle de acesso REST e Abilities | 8 |
| Exportações e integridade das partes | 27 |
| Conjunto de plugins e documentação pelo MCP | 44 |
| Painel em Chromium | 200 |

## 4. Instalação e prova da troca

O instalador tem 75 arquivos. Os bytes foram conferidos contra a árvore entregue no fonte e os hashes do manifesto interno. No Site-Teste, `plugins/upload-base64` aplicou os bytes finais com `expected_slug=wp-mcp-meta-fator3`, SHA-256 da seção 8 e chave de idempotência. Operação `1d4a8578c52814dd593b8a17fe104f00`. A página inicial e `/wp-json/` passaram nas sondas antes e depois. Em requisições novas, `meta/status` e `meta/health` retornaram 0.29.0 e estado `ok`; `meta/selftest` aprovou as verificações locais; `system/health` retornou `healthy=true`. Inventário final do Meta: zero conexões e zero agendas. Nenhuma massa de teste foi criada no site compartilhado.

Documentação: `meta/documentation`, documento `index`, leitura com `offset`, `limit_bytes` e `expected_revision`. Site-Teste: 32 documentos, 41 páginas, verificação byte a byte contra o instalador. ID fora da lista recusado. Matriz local: 47 operações descobertas; 32 documentos, 55 páginas lidas pelo MCP. As 39 capturas em 360, 768 e 1440 px cobrem 10 abas e três subvisões com dados sintéticos.

Publicação pela frota: conferir os bytes e o SHA-256 antes de usar `plugins/upload` com o slug e o hash esperados. URL prevista após publicação pelo dono: https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-meta-fator3-0.29.0-instalador.zip. Esta rodada não publicou no repositório nem alterou produção.

## 5. Banco, migração e correção por nova versão

Sem nova tabela e sem apagar filas, conteúdo histórico ou credenciais. A versão acrescenta checkpoints de migração, revisão pública de edição, índice de escopo do acervo no armazenamento existente e estado local das transições de incidentes. A adoção é retomável por lotes. Enquanto houver migração ou coletas pendentes, o cron precisa executar. Antes da troca no Site-Teste, o backup de dados do Meta cobriu duas tabelas com 691 registros e 9 opções do Meta; os dados não acompanham os pacotes. Na frota, preservar também as chaves e os salts existentes. Falha depois da troca exige contenção do fluxo e correção por nova versão, com retomada a partir do checkpoint. Uma entrega ao Core com recibo incerto não deve ser repetida sem reconciliação.

## 6. O que permanece pendente

A frota deve trocar a versão em ctooffice dentro da sua janela, reautorizar o conector, revogar a concessão anterior e verificar as **17 agendas**: nenhuma em `not_authorized`, coleta nova na passagem seguinte, revisão de edição estável e sem regravação. O Site-Teste não tinha conexão com conta Meta; não homologa Graph/Instagram real, App Review nem recebimento na caixa postal técnica. Na bancada, a Graph e o consumidor de conversas eram simulados; o transporte de e-mail foi capturado antes da saída. O aceite de 24 horas do Pedido Core 423(e) continua separado desta entrega. A publicação em produção é da frota.

## 7. Credenciais e configuração do dono

A atualização não exige novo token, novo aplicativo ou regravação de agendas. Em Ferramentas → Fator3 MCP Meta, o dono informa token manual e segredo de aplicativo; o administrador confere App ID, conta, ativos, validade e escopos conforme CONFIGURATION.md. A versão padrão da Graph continua v24.0. Conversas e contato automático permanecem opcionais e exigem habilitação, aplicação aprovada e Página associada. No Site Core, configurar o e-mail de avisos técnicos em `f3base_avisos_tecnicos.email`.

## 8. Identidade dos arquivos

| Artefato | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-meta-fator3-0.29.0-instalador.zip | 278994 | `730f9cd17ccba8a32081444643ea5a2b6b64a037752fdfdfee5c58753171e747` |
| wp-mcp-meta-fator3-0.29.0-fonte.zip | 13906833 | `e7efc56487a9db37c712841cc74a60058acd3628279e4cf3d00735cb7cd24db7` |
| wp-mcp-meta-fator3-0.29.0-capturas.zip | 4382139 | `af8e06fe37a52982b9233bdcf3924e066bc5f250d01090705e9f130f2d7b4d7f` |

O relatório externo é canônico. A cópia no ZIP fonte precede o fechamento desse arquivo.
