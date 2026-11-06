# Entrega — Fator3 MCP 0.41.0

Revisão 1 · 2026-11-05T13:55-03:00 · Rodada de implementação · **Apta no escopo testado**. Fator3 MCP 0.41.0 ativo no Site-Teste.

Identidade publicada `wp-mcp-fator3/wp-mcp-fator3.php`. Foram aplicadas as revisões 5 de 02/11/2026 de `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`. A solicitação direta do dono para esta rodada abrange código, testes, interface de configuração e documentação. O pedido MCP 77 é anterior e seu limite de aceite consta na seção 6.

## 1. De onde a versão entra

Instalação nova ou atualização direta do MCP 0.40.0 entregue na rodada anterior. A bancada exercitou ambos os caminhos. A referência do instalador era de 932250 bytes, SHA-256 `2434f99df49c56b6f0200d0ddca18c6dffe1b7c6058c2c88f04859f1e046bd81`. O fonte anterior tinha 4365881 bytes, SHA-256 `f6a05b6f86745ffa08fac7ada577cbb555cef67e963085f91788c2d4895eda54`.

O projeto requer WordPress ≥ 7.1.4 e PHP ≥ 8.3. A bancada usou WordPress 7.1.4, PHP 8.3.6, MySQL 8.0.46 e Chromium 152.0.7940.0. O Site-Teste informou WordPress 7.1.4 e PHP 8.3.36.

## 2. Convivência e encaminhamentos

A conferência do Site-Teste antes da troca identificou versões mais recentes de Meta e Pipedrive. A bancada foi recriada com o conjunto abaixo, e o catálogo de contratos foi extraído de uma instalação WordPress com os cinco acompanhantes ativos. A contagem de testes deste relatório corresponde à certificação com esse conjunto. Além da identidade dos ZIPs, foram conferidos os 1287 arquivos dos acompanhantes na bancada com os bytes de seus instaladores (`companion-parity.json`).

| Pacote | Versão | SHA-256 do instalador |
|---|---|---|
| base-site-core-fator3 | 1.71.0 | `7aa9f94e4ecfd30db81ab10603981fb3e4503f7039aeaf5b0fae1ab287d37e57` |
| wp-mcp-google-fator3 | 0.28.0 | `10d3722e12d1493308273ab0febbabe68f8dd4c901c7abb3a7c03d3cec3e8919` |
| wp-mcp-linkedin-fator3 | 0.18.0 | `1e6c6e398ab2c507d827e428ae3b28099753459ef1b97a04ddf1c3922d819460` |
| wp-mcp-meta-fator3 | 0.21.0 | `9589456a2ee5ed13cb72941437e4350c0815907f6ba20b8eb47837a77064334a` |
| wp-mcp-pipedrive-fator3 | 0.7.0 | `8f58b26c8408c02604c16bcfd30fcb92e3bbae308ebc107defad21555e5b5779` |

A revisão comparou os 167 schemas de entrada e saída das habilidades próprias, a descoberta dos provedores registrados no MCP e o uso de uma cópia da tabela de leads do Core. O catálogo gerado a partir do registro ativo também correspondeu, byte a byte, à especificação no fonte (`installed-contracts.json`). Os filtros e a recuperação dos recibos pertencem ao MCP. As alterações preservaram os contratos de registro com os acompanhantes. A avaliação dos contratos limitou as ações de implementação ao MCP. A troca desta rodada requer apenas substituir o MCP.

## 3. Mudanças e evidência

| Pedido | Problema reproduzido na 0.40.0 | Mudança verificada |
|---|---|---|
| Melhorar código e funcionalidades | A listagem de conexões relia cada política e consultava cada concessão OAuth individualmente. | `connections/list` obtém as políticas da página e agrupa a verificação das concessões. O teste compara proprietário, validade, revogação, perfil de manutenção, privacidade e paginação. A leitura seguinte reflete a retirada de uma senha de aplicação ou de uma concessão. |
| Corrigir confirmação e repetição | Após uma alteração do próprio perfil, repetir a confirmação produzia conflito com a revisão que a própria operação acabara de substituir. O nome informado também se perdia no executor. | A mesma solicitação confirmada devolve o recibo original sem repetir a escrita. A prévia ainda pendente exige a revisão corrente e uma credencial revogada ou sem autorização sobre a conta não recupera o recibo. O nome passa a integrar a alteração e a validação do token. Os testes também cobrem o rótulo de backup, sua consulta e a transferência em partes. Para uma prévia da 0.40.0 emitida com nome, gere uma nova prévia antes de confirmar na 0.41.0. |
| Melhorar os controles e textos da tela | O Registro montava 838 opções de habilidade no cenário integrado. Com um alvo contendo `#`, a paginação enviava o cursor ao fragmento da URL. Um filtro com tipo inválido ampliava silenciosamente a consulta. | Identificação do evento e período/resultado são grupos distintos. A busca aceita o ID exato de habilidades históricas e oferece sugestões baseadas na página exibida. O formulário explica UTC e o término exclusivo. Rótulos e instruções ficam junto aos campos, dentro da largura da coluna. A paginação mantém filtros e cursor, inclusive com acentos, espaços, `+`, `%`, `&` e `#`. Filtros inválidos exibem erro. |
| Ampliar testes e documentação | As regressões da listagem, da confirmação e das duas páginas do Registro não tinham prova dedicada na base. | A suíte reproduz os comportamentos na base e avalia o candidato pelo WordPress. O manual administrativo e as notas `release-0410` documentam repetição, filtro por horário e paginação. O guia instalado pode ser lido integralmente pelo transporte MCP. |

Em uma página com 12 identidades sintéticas no mesmo cenário, o total passou de **20 para 3 consultas SQL**. As consultas de políticas passaram de 13 para 1 e as de concessões OAuth, de 6 para 1. A medição conta as consultas SQL durante a execução da listagem. Autenticação, transporte HTTP e duração total de uma requisição ficam fora dessa contagem. Evidências em `connections-list-0.40.0.json` e `connections-list-0.41.0.json`.

## 4. Instalação e prova da troca

Os resultados abaixo estão em `evidencias/0410/`. A soma de **336 verificações funcionais** inclui 39 na base 0.40.0 e 297 na 0.41.0. A contagem completa consta em `local-acceptance.json`. Cada suíte registra as verificações individuais.

| Cenário | Verificações aprovadas | Evidências |
|---|---:|---|
| Primeira ativação isolada | 6 | `clean-activation.json` |
| Atualização direta e recuperação | 14 | `migration-before.json`, `migration-preview.json`, `migration-after.json` |
| Listagem de conexões na base e no alvo | 39 | `listing-tests-0.40.0.json`, `listing-tests-0.41.0.json` |
| Confirmação de perfil na base e no alvo | 28 | `connection-policy-before.json`, `connection-policy-after.json` |
| Registro na base e no alvo | 30 | `history-baseline.json`, `history-candidate.json` |
| Chromium no Registro | 28 | `browser-history.json` |
| Regressão em telas de configuração | 89 | `browser.json`, `configuration-writers.json` |
| Contratos e leitura pelo transporte | 63 | `schema-before.json`, `schema-after.json`, `integration-and-guide.json` |
| Backups e recuperação de linhas SQL | 39 | `row-backup.json`, `scale.json`, `interruption-and-lock.json` |

A primeira ativação ocorreu com o MCP sozinho em banco novo. A atualização usou o ZIP 0.41.0 sobre a 0.40.0 em outra instalação, com os cinco acompanhantes ativos. Em Chromium, o Registro foi exercitado por teclado nas larguras de 1365 e 375 pixels, com duas páginas de resultados e consulta de habilidade histórica. Durante a homologação local, o primeiro candidato excedeu a coluna do formulário por 2 pixels. A versão entregue corrige a margem dos controles e foi reavaliada nas duas larguras. Os formulários estão registrados em `evidencias/0410/screens/history-filters-1365.png` e `history-filters-375.png`. Na regressão de SQL, os testes cobriram seleção de linhas, conflito, interrupção e restauração. Na integração, a descoberta passou pelo transporte real do WordPress. A atualização e a restauração de um registro sintético usaram a estrutura instalada do Core.

O pacote passou em 18 verificações estáticas. Elas incluem a análise de sintaxe de 461 arquivos PHP e do JavaScript do painel. A comparação em separado cobriu os 475 arquivos instalados em cada ambiente da bancada. As evidências estão em `package-check.json` e `installed-parity.json`.

No Site-Teste, a operação `b1743d05f004b4dac610dc7a74812f5d` de `plugins/upload-base64` conferiu o slug e o SHA-256 e confirmou a troca de 0.40.0 para 0.41.0. A página inicial e a REST API responderam HTTP 200 antes e depois da instalação. Uma nova chamada a `system/health` confirmou a saúde do canal. Durante a instalação do MCP, os demais 8 plugins conservaram versão e atividade. O arquivo temporário da transferência foi removido. Evidências em `site-teste.json`.

A leitura autorizada de `connections/list` verificou os rótulos de estado e, ao avançar, a continuidade pelo cursor entre duas páginas (`site-connections.json`). A descoberta identificou o guia, a busca abriu a seção do Registro e as proteções recusaram caminho externo e revisão divergente (`site-guide-discovery.json` e `site-guide-search.json`). O conector leu integralmente **40 documentos em 46 páginas**. Os conteúdos e seus hashes corresponderam aos da entrega. A comparação também verificou 15 arquivos instalados. Evidências em `site-guide.json` e `runtime-files.json`.

Para distribuir pela frota, o responsável publica o instalador e o relatório e verifica o SHA-256 dos bytes servidos por [esta URL raw de destino](https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-fator3-0.41.0-instalador.zip). Em seguida, usa `plugins/upload` com `expected_slug` igual a `wp-mcp-fator3`, `expected_sha256` igual ao valor da seção 8 e ativação explícita. A homologação efetuada aqui foi a do Site-Teste.

## 5. Banco, migração e correção por nova versão

A atualização usa o schema de estado 2 e o contrato de perfis 1 já publicados. A bancada verificou o hash da senha de aplicação, a revisão e as restrições do perfil, o limite de arquivo, a retenção e a fonte de atualização de outro pacote. Um recibo em andamento preservou seu estado. Uma prévia de restauração emitida na 0.40.0 concluiu na 0.41.0 a partir do backup da linha sintética. Em caso de interrupção, consulte o recibo e o estado persistido, reconcilie o efeito e retome apenas a etapa pendente. Uma falha de código após a instalação requer correção em nova versão.

## 6. O que permanece pendente

- **Pedido MCP 77, frota.** O aceite referente à escrita no registro 46 de korvena.com.br continua a cargo da frota. A bancada usou a estrutura real do Core com dados sintéticos. A instalação e a escrita em produção ficaram fora desta rodada.
- **Runtime e navegador.** O teste do piso usou WordPress 7.1.4 e a série PHP 8.3 nas revisões declaradas na seção 1. PHP 8.3.0 exato e outros navegadores ficaram fora da matriz executada nesta rodada.
- **Limite da prova de integração.** As provas usaram o transporte WordPress e a área de teste. Alterações de perfil ocorreram com credenciais sintéticas em bancada. Homologação de APIs comerciais e ações nas contas de clientes ficaram fora deste escopo.

## 7. Credenciais e configuração do dono

Use **Ferramentas → Fator3 MCP → Registro** para consultar metadados. Informe a habilidade exata, inclusive quando o provedor já saiu do catálogo. Escolha o início (inclusive) e o fim (exclusivo) em UTC. Para revisar uma conexão, abra **Clientes conectados** com permissão administrativa. O acesso via MCP à gestão da conexão exige perfil de manutenção, e alterar o perfil exige autorização sobre a conta. O agente consulta `system/guide` com `document: "release-0410"` e pode usar a identificação e a revisão obtidas em `connections/list` para elaborar uma prévia. Uma credencial existente e autorizada é suficiente.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-fator3-0.41.0-instalador.zip](./wp-mcp-fator3-0.41.0-instalador.zip) | 936186 | `4a31d22788d66b9342efdc25d4b75d919efa4320035bc607c0b396691ca783e5` |
| Fonte | [wp-mcp-fator3-0.41.0-fonte.zip](./wp-mcp-fator3-0.41.0-fonte.zip) | 4461108 | 09e6c3c34b85f3ad4b5828ec7c9335a9667f9a463e890261f40b550f86824534 |

Relatório externo canônico. A cópia no fonte é anterior ao fechamento do próprio ZIP.
