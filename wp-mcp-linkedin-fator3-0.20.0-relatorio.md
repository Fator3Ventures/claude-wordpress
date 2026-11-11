# Entrega — Fator3 MCP LinkedIn 0.20.0

Revisão: 1 · 2026-11-10T20:40-03:00 · Rodada: implementação, migração, integração e validação
Slug: `wp-mcp-linkedin-fator3` · Versão/build: 0.20.0 · Status: apta-no-escopo-testado. Ativa no Site-Teste. Acesso ao fornecedor com conta real permanece pendente.

## 1. De onde esta versão entra

Instalação inicial em WordPress limpo ou atualização direta da base oficial 0.19.0. O instalador anterior recebido tem 397354 bytes e SHA-256 `613cb47cfb3be2b91dfa1f20f39c465780a6fffb5432b645290448fe592a0f0c`; o fonte anterior tem 3056323 bytes e SHA-256 `25f3458b99584a68bb56920c12ef828508d6cb0f2c72eceb0921d24d3eae3a62`. Requisitos: WordPress >= 7.1.4 e PHP >= 8.3; bancada em WordPress 7.1.4, PHP 8.3.6, MySQL 8.0.46. Contraprovas baseadas no plano revisão 1 e no parecer de 10/11/2026. Instruções de agentes e padrão de desenvolvimento Fator3: revisão 5 de 02/11/2026, lidas integralmente.

## 2. Convivência e encaminhamentos

Todos os acompanhantes abaixo estavam ativos na prova integrada e no Site-Teste. A entrada de apenas um pacote dispensa reordenar a inicialização da frota. Identidades dos instaladores usados na bancada:

| Pacote | Versão | SHA-256 |
|---|---|---|
| base-site-core-fator3 | 1.78.0 | `503a07a6fc1106d1582596c96f10fa9c558fb92cea968782efe26f923b2ccce6` |
| wp-mcp-fator3 | 0.43.0 | `c0f3a10ad4275dc51abd4ab01ac9d2647914fb13d214b9e4f460cd989ddf4951` |
| wp-mcp-google-fator3 | 0.31.0 | `e577dd444b063d99e42a4c63840095d9f176f82bd864e21d09c76a877d9e670e` |
| wp-mcp-meta-fator3 | 0.21.0 | `9589456a2ee5ed13cb72941437e4350c0815907f6ba20b8eb47837a77064334a` |
| wp-mcp-pipedrive-fator3 | 0.8.0 | `89e41f2f7a2124eb1a5961fe06d6aff60fd168b8d6dd2ea1b21a272772ff7f30` |

Impacto individual: **wp-mcp-fator3**, alerta-tecnico, encerrado no emissor, sem ticket. Ver `wp-mcp-linkedin-fator3-0.20.0-impacto-wp-mcp-fator3.md`, revisão 2. Quatro campos anteriormente observados e uma hipótese adicional ficaram comprovados; o emissor adicionou projeções legíveis. O redator do MCP e suas proteções continuam em vigor. No Core testamos a leitura por SDK, as autorizações e a reconciliação; as revisões históricas continuam tipadas. Nenhum impacto identificado para Google, Meta e Pipedrive na ativação conjunta e nos contratos exercitados. As alterações nos modelos compartilhados são somente da cópia do LinkedIn. Os serviços externos dos acompanhantes não foram acionados.

## 3. Mudanças e evidência

| Pedido do plano | Problema | Implementação e prova |
|---|---|---|
| L20-01 | Criar ou reativar conexão sem token | Retorna application_required antes de gravar; permite rascunho pausado e conserva segredo na edição vazia. Conexão inválida legada gera connection_without_token sem reparo nem consulta externa. Casos positivo, negativo e migração. |
| L20-02, L20-04 | Rótulo de outro formulário, textos de campo ou lista ambíguos | Ajuda associada explicitamente ao campo; nome da agenda, concessão ativa, dias de guarda e seletor por canal conferidos no DOM. Mensagem de lista local vazia distingue concessões de respostas do LinkedIn. |
| L20-03, L20-05 | Resultado fora do campo de visão, perda de foco e caixas deformadas | Resultado junto da ação e faixa visível; uma resposta tardia não toma o foco de uma ação posterior. Confirmação consumida leva à próxima ação habilitada. Caixas quadradas nas duas larguras. |
| L20-06 | Consulta local de estado criava eventos de auditoria | 25 leituras sem escrita; alteração, chamada real à fronteira e recusa nas entradas testadas deixam o evento da camada apropriada. Diários, retenção e históricos permanecem. |
| L20-07 | Valores públicos mascarados pelo MCP | Projeções de método de entrada, preservação de campo vazio, resultado de manutenção, verificação de acesso do SDK e prazo de aviso. Quatro operações em JSON-RPC HTTP real no WordPress isolado; valor fora do enum não é exposto. |
| L20-08 | Recuperação ambígua na leitura paginada | Revisão ausente indica como continuar; divergente indica reinício. Código público revision_conflict conservado; continuação válida conferida. |
| L20-09 a L20-12 | Navegação e editor escondiam tarefas; Ajuda mostrava marcação | Seis seções, 12 painéis, URLs antigas e fragmentos de conversão; 20 conexões por página, busca global e edição da 51ª; grupo de dados recolhível e guia de campos. Simulação funciona com zero vínculos e é descartada ao editar. Ajuda agrupa manuais/schemas/histórico; Markdown restrito, sem HTML executável. |
| L20-13 | Identidade dependia só da compressão ZIP | Verificação de CRC, conjunto completo de caminhos, manifesto e bytes do runtime; alterar um byte invalida a prova. Build Python 3.12.14, zlib 1.3.2. |
| L20-14 | Reformatação geral misturada à alteração funcional | Adiada conforme D5 do parecer; a versão faz alterações localizadas. Não se atribui à entrega equivalência sintática de uma reformatação global. |
| L20-15 | Ausência de barreiras visuais e de teclado para a UI nova | Chrome Headless 156.0.8078.79 com sandbox; tela real, duas larguras, zoom por CSS de 200%, foco, rolagem, áreas de clique, navegação e entrada malformada. Detalhes e quatro capturas sintéticas em evidence/release0200. |
| L20-16 | Manual, schema e catálogo podiam divergir do código | Build consulta o registro e gera o catálogo das 99 operações, códigos e faixas. Lint inclui títulos sem versão e campo documentado em formulário incorreto. As 16 mutações documentais foram rejeitadas. |
| L20-17 | Reaproveitamento de banco contaminava suítes independentes | Chamadas com duas suítes independentes recusadas antes de criar diretórios ou banco. O requisito explícito de stages é executado na mesma fixture do seu consumidor. |

Contratos de escrita preservados: 25 schemas aceitam dry_run, 20 aceitam confirm_token e 2 aceitam confirmation. A exigência depende da operação e da fase. A bancada verifica prévia, escrita controlada na fronteira sintética, reapresentação e ausência de reenvio quando o efeito é incerto. Nenhum orçamento ou objeto real foi criado. A interface mantém o retorno OAuth em Aplicativo, antes da autorização, com o fluxo manual e o rascunho pausado. Resultados medidos e efeitos externos têm alcances diferentes.

## 4. Instalação e prova da troca

**Site-Teste:** https://fator3-teste-mcp-1.dreamhosters.com/. Uma atualização pela capacidade de instalação com arquivo Base64, overwrite e activate, expected_slug=wp-mcp-linkedin-fator3, expected_sha256 da seção 8 e chave idempotente. Versão anterior 0.19.0; após a troca, somente 0.20.0 ativa. Recibo: `5727f8ee42b93e27a2c96c3b2ced14df`; backup de arquivos: `485b3558f0a90af1d559f339`. Inventário antes/depois: os outros plugins mantiveram versão e ativação. Prontidão: estado ok, zero avisos, nove verificações locais aprovadas; HTTP 200 em / e /wp-json/ nas sondas de origem antes e depois; zero conexões LinkedIn configuradas. A publicação pela frota via URL raw é etapa distinta; sem URL raw desta entrega, push ou publicação em produção nesta rodada.

Banco de teste próprio por suíte; sem execução remota no fornecedor. Mesmos bytes do instalador da seção 8. As contagens abaixo são verificações por execução, com repetição intencional entre cenários. Total: 755 verificações, zero falhas na matriz final.

| Suíte / evidência | Verificações | Falhas |
|---|---:|---:|
| core1680-integrated-clean / request-369.json | 37 | 0 |
| lifecycle019-only-clean / lifecycle019.json | 12 | 0 |
| mcp-docs080-integrated-clean / mcp-docs080.json | 69 | 0 |
| mcp-docs080-integrated-upgrade / mcp-docs080.json | 69 | 0 |
| mcp-stages012-integrated-clean / mcp-stages012.json | 5 | 0 |
| mcp-stages012-integrated-clean / stages012.json | 24 | 0 |
| migration020-integrated-upgrade / migration020.json | 8 | 0 |
| requests017-only-clean / requests017.json | 47 | 0 |
| requests018021-only-clean / requests018021.json | 27 | 0 |
| server020-integrated-clean / server020.json | 35 | 0 |
| server020-only-clean / server020.json | 26 | 0 |
| suite-integrated-clean / native-tests.json | 141 | 0 |
| worker019-only-clean / worker019.json | 19 | 0 |
| webui020-integrated-clean / results.json | 236 | 0 |

Documentação: na instalação limpa e na migrada, o executor nativo do MCP leu 45 documentos, em 56 páginas por instalação; reconstrução comparada em tamanho, SHA-256 e conteúdo com os arquivos efetivamente instalados. No site compartilhado, descoberta/schema e índice da operação `linkedin/documentation`; 8 manuais completos conferidos contra o instalador em 14 respostas de conteúdo; lista em site-teste.json. Homologação de fornecedor não inferida da leitura local da ajuda.

Contraprovas: mutações de guarda, auditoria, paginação, transporte, rótulos, texto de lista, checkbox, geometria e foco. Para cada mutante, ver mutation-runtime.json: o critério responsável falha. As contraprovas rodam unicamente em cópias isoladas, nunca no site compartilhado. O relatório de bancada distingue os pacotes candidatos dos bytes finais. Não há credencial, cookie, banco ou instalador mutante na entrega.

## 5. Banco, migração e correção por nova versão

Schema físico 2 conservado; a atualização não regrava configurações para consertar estados antigos. No ensaio direto 0.19.0→0.20.0, 12 registros amostrados preservaram conteúdo e revisão: material cifrado, concessões, agendamento, cursores, recibo incerto, auditoria e política. O diagnóstico do registro inválido não altera o registro. Falha futura exige correção em nova versão, com preservação do banco e reconciliação de efeitos incertos. Backup de arquivos do instalador não substitui backup do banco. Não se executou downgrade.

## 6. O que permanece pendente

Dono/frota: homologar OAuth, escopos, dados de ativos, leads e conversões em conta LinkedIn autorizada. O Site-Teste foi usado exclusivamente para a troca e leituras de prontidão, sem inserir conexão, token, campanha ou fixture. Retomar L20-14 somente se houver motivo autônomo para a reformatação geral. Os testes de navegador desta rodada usam Chrome; não se declara compatibilidade visual ensaiada em Safari/Firefox ou prova com leitor de telas. A matriz não reexecutou todas as suítes históricas Node/jsdom. Métricas de zoom referem-se ao redimensionamento CSS de 200% no navegador exercitado. A publicação/distribuição pela frota e a decisão 89 sobre publicação do fonte seguem separadas.

## 7. Credenciais e configuração do dono

Ferramentas → Fator3 MCP LinkedIn → Conexões → Nova conexão. Para OAuth: salve pausada, cadastre o endereço de retorno no aplicativo e autorize apenas os escopos necessários. Para token manual: informe ID, segredo, token e validade UTC, e marque a conexão ativa. Campo secreto vazio preserva o valor. Depois selecione os ativos; a seleção do aplicativo não concede acesso ao consumidor por si só. Em Manutenção → Diagnóstico execute o autoteste local, depois valide o ativo apenas com permissão de acesso real. PRIMEIROS-PASSOS.md contém as ações e AGENTS.md os contratos do MCP. Nenhum segredo consta dos artefatos de entrega.

## 8. Identidade dos arquivos

Relatório externo canônico. A cópia no fonte é anterior ao fechamento do ZIP; este relatório completa sua identidade final.

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| `wp-mcp-linkedin-fator3-0.20.0-instalador.zip` | 429846 | `4b3f7321b81a28bbed6595d6922ec7d388685690d58d278f3f4b3ebc592ee743` |
| `wp-mcp-linkedin-fator3-0.20.0-fonte.zip` | 3543948 | `ece3924e1d1ca54ed36f58ea6ead21f5037f4d68e03ea53b28bf6c5a93bbb5ba` |

O instalador contém 88 arquivos; o manifesto identifica 87, excluindo a si próprio. O fonte traz runtime integral, build, testes e evidências. Nenhum ZIP contém outro ZIP. Sem commit externo atribuído. O relatório canônico é `wp-mcp-linkedin-fator3-0.20.0-relatorio.md`.
