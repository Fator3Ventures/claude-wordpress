# Entrega — Fator3 MCP Google 0.43.1

Revisão 1 · 2026-11-20T18:17:00-03:00 · Atualização visual e corretiva · Slug `wp-mcp-google-fator3` · Versão 0.43.1, identificada pelo SHA-256 do instalador na seção 8.

**Situação: com-pendencias.** O painel está implementado e ativo no Site-Teste. O responsável visual e a frota têm os itens de aceite da seção 6.

## 1. De onde esta versão entra

A base oficial desta rodada foi o fonte do Fator3 MCP Google 0.42.0. O instalador correspondente tem SHA-256 `5de445dbbaf6afa1ec48cc97171a5d5c6ef2c502623a45f9fc930e713ec59aeb`. A 0.43.0 introduziu a nova navegação e foi instalada em homologação. A revisão identificou que o índice por cartões de Avançado contrariava o guia específico do Google. A 0.43.1 corrigiu o controle e preservou o formulário acessado pelos favoritos antigos. A instalação limpa, o salto direto de 0.42.0 para 0.43.1 e a troca de 0.43.0 para 0.43.1 foram testados.

O cabeçalho exige WordPress 7.1.4 e PHP 8.3. A bancada usou WordPress 7.1.4 com PHP 8.3.6 e 8.4.27. O Site-Teste usou WordPress 7.1.5 com PHP 8.3.37. O diretório `inputs/043/` do fonte conserva as instruções e entradas da rodada, inclusive `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos revisão 5 de 02/11/2026, o padrão Google, a regra comum, o pedido e os guias visuais.

## 2. Convivência e encaminhamentos

| Ambiente | Conjunto verificado | Verificação |
|---|---|---|
| Bancada, pacote isolado | Google 0.43.1 | Ativação, armazenamento e documentação. |
| Bancada, conjunto dos anexos | Core 1.100.1, MCP 0.54.0 e Google 0.43.1 | Prontidão, leitura da documentação por MCP, autorização e atualização nos três cenários. |
| Site-Teste, após a troca | Core 1.100.1, MCP 0.55.0, Google 0.43.1, LinkedIn 0.27.0, Meta 0.32.1 e Pipedrive 0.12.0 | Painel Google com aviso PublishPress Authors, catálogo, integração, armazenamento e inspeção da folha comum. |

A execução do Google mantém 311 operações, das quais 123 de leitura e 188 de escrita. Permanecem 46 definições de configuração, contrato de configuração 4.0.0, catálogo 3.0.0 e contratos de execução e armazenamento 2.0.0. A mudança pode ser instalada apenas no Google. O exame dos consumidores e dos pacotes acompanhantes identificou zero alterações de contrato ou de código necessárias para consumir a 0.43.1. O encaminhamento histórico ao Core sobre incidentes segue registrado como resolvido em `impacts/042/`. A identidade visual entre pacotes é uma validação coordenada da frota.

## 3. Mudanças e evidência

**Pedidos MCP Google 60.** O painel abria em Suporte, tinha navegação lateral de terceiro nível e usava estilos próprios para elementos compartilhados. Agora abre em **Operação → Visão geral**. Em Suporte, o grupo com uma única tela abre a Ajuda diretamente. As URLs com `section`, `connection_panel` e `advanced_panel` continuam levando ao formulário correspondente. O acesso ao painel conserva `manage_options`.

| Ajustes do guia Google | Implementação | Prova |
|---|---|---|
| 1–3 | Folha comum antes da própria, raiz `f3-ui`, cabeçalho `f3-heading` com nome, descrição e versão. | O SHA-256 comum consta abaixo. O h1 computado tem 23 px e peso 400 nas 27 capturas. |
| 4–6 | Grupos Operação, Configurar, Dados e Suporte. Conexão oferece quatro opções e Avançado, cinco, no topo do cartão. | Zero ocorrências da navegação lateral na matriz. O favorito antigo das credenciais abre **Conexão → Credenciais avançadas**. Ver também a página 2 do caderno. |
| 7–9 | Seções com título e ações, selos textuais de estado e cartões para os itens de conferência. | HTML das nove subabas e inspeção dos estilos. Os estados têm texto legível e os selos antigos saíram do painel. |
| 10–11 | Os passos usam as variáveis de estado e destaque. Tabelas em regiões com rolagem própria têm cabeçalho da folha comum. | Verificações de HTML, de CSS e de largura. Na Ajuda, a lista de 26 itens foi paginada e filtrada. |
| 12–13 | Botões mantêm largura natural e quebram linha. Os títulos de cartão usam 1,3 em. | Em 360 e 768 px, os controles mediram pelo menos 40 px e a navegação, 44 px. O h2 mediu 16,9 px. |
| 14–15 | Na revisão de serviços, o h1 é o nome do plugin e a tarefa é o h2. A navegação por teclado usa o foco da folha comum. | Tela de revisão exercitada em três larguras na bancada. No Site-Teste, links, botões, campos e resumos presentes exibiram contorno de 2 px ao usar Tab. |

**Folha comum.** O arquivo fornecido, o instalador e o arquivo relido no Site-Teste têm 11.886 bytes e SHA-256 `15ef0d932b1be12a541b8408b061ee276a4db9d6650476f92b5e2f41eefc0c2b`. O Google carrega `assets/f3-ui.css` somente em suas próprias telas. Conferi o mesmo hash no Core, Meta e LinkedIn e também em `core/assets/css/f3-ui.css` do MCP 0.55.0. O inventário de `assets/` do Pipedrive 0.12.0 mostrou sua folha própria `admin.css`. A identidade do sexto pacote segue pendente.

**Matriz da seção 7 do guia visual.** Cada coluna corresponde ao critério do guia na numeração original. **S** indica observação no Site-Teste, **C** combina o Site-Teste com uma prova complementar em bancada e **A** indica inspeção do arquivo entregue. A coluna 5 usa o esquema Moderno no Site-Teste e a troca para Padrão na bancada. O código e os dados do verificador estão em `tests/native/visual0431/` e `evidence/0431/`.

| Grupo e subaba | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | Pág. no PDF |
|---|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|---|
| Operação · Visão geral | S | S | S | S | C | S | C | S | S | S | S | A | 3–4 |
| Operação · Incidentes | S | S | S | S | C | S | C | S | S | S | S | A | 5–6 |
| Configurar · Conexão | S | S | S | S | C | S | C | S | S | S | S | A | 7–8 |
| Configurar · Conversões | S | S | S | S | C | S | C | S | S | S | S | A | 9–10 |
| Configurar · GTM | S | S | S | S | C | S | C | S | S | S | S | A | 11–12 |
| Configurar · Avançado | S | S | S | S | C | S | C | S | S | S | S | A | 13–14 |
| Dados · Acervo Ads | S | S | S | S | C | S | C | S | S | S | S | A | 15–16 |
| Dados · Search Console | S | S | S | S | C | S | C | S | S | S | S | A | 17–18 |
| Suporte · Ajuda | S | S | S | S | C | S | C | C | S | S | S | A | 19–20 |

1. Identidade e ordem das folhas. 2. Raiz, cabeçalho, descrição e versão. 3. Divisor e aviso externo. 4. Ordem, quantidade e níveis de navegação. 5. Cor de destaque do esquema. 6. Selos de estado. 7. Posição e associação dos rótulos. 8. Tabelas e listas longas. 9. Largura da página. 10. Altura dos alvos de interação. 11. Foco por teclado. 12. Uso das variáveis na folha própria.

As 27 capturas autenticadas têm 880 px de altura e mostram o aviso de outro plugin nas três larguras. No navegador com barra vertical, `scrollWidth` coincidiu com `clientWidth`. Em nova passagem nas mesmas larguras, com altura suficiente para retirar a barra vertical, `scrollWidth` coincidiu com `innerWidth` em 27 de 27 medições. O verificador consolidou 108 critérios. A Ajuda em bancada apresentou “1–20 de 26”, “21–26 de 26” e “1–1 de 1” após a busca. O controle de foco incluiu nova passagem por Visão geral, Avançado e Acervo Ads a partir do link Configurar. As duas medições ficaram preservadas.

## 4. Instalação e prova da troca

O instalador foi enviado em quatro partes ao Site-Teste. A operação usou o slug esperado `wp-mcp-google-fator3` e conferiu o SHA-256 da seção 8. O diário `1616077681bf3cb71e37cf2c5fecef6c` terminou em `complete`. O instalador registrou cópia do código anterior. O Google 0.43.1 permaneceu ativo. A releitura de oito arquivos no site coincidiu com o ZIP, incluindo o arquivo principal, o controlador, as duas folhas e o JavaScript. A saúde do ambiente retornou positiva, com zero recuperações pendentes.

| ID | Ambiente e cenário | Resultado observado | Evidência no fonte |
|---|---|---|---|
| T1 | WordPress limpo, Google isolado | 37 verificações aprovadas, armazenamento pronto e 26 documentos. | `isolado.json`, `limpa-isolada.json` |
| T2 | WordPress mínimo com os acompanhantes | Instalação limpa e ambas as atualizações diretas. O timeout de controle de 47 segundos foi preservado nas duas migrações e relido em outro processo. O assinante recebeu HTTP 403 nas operações de leitura e escrita testadas e teve o painel recusado. | `google431_*-php83.json`, `permissoes-*.json` |
| T3 | PHP 8.3.6 e 8.4.27 | Em cada runtime, 1.389 testes e 16.555 asserções, zero falhas e zero testes omitidos no executor compatível com PHPUnit. Lint dos 209 PHP do instalador em 8.4.27. | `unitarios-php83.json`, `unitarios-php84.json`, `lint.json` |
| T4 | HTTP MCP autenticado em cada um dos três cenários integrados | 124 verificações por cenário, 26 documentos completos, 90 páginas, hashes conferidos e zero chamadas ao fornecedor. | `docs-google431_*.json` |
| T5 | Site-Teste após a atualização | `google/status` retornou versão 0.43.1 e 311 operações. `google/integration-status` com `compact=true` devolveu `read_success=true`. `google/storage-status` indicou `storage.ready=true`. | `campo.json` |
| T6 | Interface no Site-Teste e em bancada | 27 capturas e dois detalhes dos alternadores no site. Em bancada, 18 telas em três larguras, incluindo rotas secundárias e revisão de serviços. Navegação por teclado também exercitada com JavaScript desativado. | `site-teste/`, `visual/`, `matriz.json`, caderno PDF |

No WordPress, **Suporte → Ajuda** abre o índice instalado. Pelo MCP, `google/documentation` lista os documentos e informa a revisão. Para ler, usar `document`, `expected_revision`, `offset` e `limit_bytes`, seguindo `next_offset` até o fim. No Site-Teste, o guia da 0.43.1 foi relido em quatro páginas, totalizando 6.654 bytes, SHA-256 `ee67ff2f58cfdfc974a9ca9448e646041763b4c59542adf3fbbfcf2908352a3e`. Um caminho fora do índice foi recusado.

A área temporária de transferência e a página de medição foram removidas no Site-Teste. As bases, o WordPress, o registro HTTP e a credencial sintética da bancada foram descartados após a coleta. No Site-Teste permanecem o plugin ativo e os backups privados. O PDF usa apenas as capturas do Site-Teste.

## 5. Banco, migração e correção por nova versão

Esta versão modifica a interface e a documentação. Mantém as tabelas, opções, permissões, callbacks, agendamentos e formatos já utilizados. A troca no Site-Teste foi precedida de backup das duas tabelas Google, com 2.482 registros de cron e 179 registros de dados, totalizando 2.661 linhas, e de 28 opções do plugin. Os backups privados não integram os arquivos entregues.

Em caso de interrupção, conferir o diário da instalação, a versão ativa e a prontidão do armazenamento antes de retomar. Preservar o banco consistente e a configuração da conexão. Uma correção após instalação recebe nova versão, como na passagem de 0.43.0 para 0.43.1. A atualização visual dispensa migração de dados e reconciliação com o Google.

## 6. O que permanece pendente

- **Responsável visual.** Aceitar o pedido 60 após revisar o painel e o caderno. A troca entre dois esquemas do usuário foi exercitada na bancada. As capturas do Site-Teste usam o esquema Moderno do perfil compartilhado. Os resultados cobrem o navegador Chromium utilizado.
- **Frota.** Conferir a folha comum no Pipedrive quando a versão correspondente estiver disponível. O mesmo conteúdo foi comprovado em cinco dos seis pacotes.
- **Distribuição.** A publicação e a instalação em produção pertencem à frota. O endereço raw previsto para o instalador é `https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-google-fator3-0.43.1-instalador.zip`. Os bytes dessa futura publicação ainda precisam ser conferidos antes da chamada a `plugins/upload` com `expected_slug` e `expected_sha256`. O fonte é destinado ao dono.
- **Titular da conexão.** O Site-Teste informou `auth_configured=false`. A homologação cobriu o painel e os contratos locais. Acesso a uma conta Google real e entrega de conversões seguem dependentes de credenciais e ativos autorizados. Os acompanhamentos operacionais anteriores continuam no relatório da 0.42.0.

## 7. Credenciais e configuração do dono

A atualização visual dispensa preenchimento de novos campos. Em **Ferramentas → Fator3 MCP Google → Configurar → Conexão**, **Identidade** permite escolher conta de serviço ou OAuth. Quando houver necessidade de acesso real, o titular configura a credencial correspondente, seus escopos, o projeto e os ativos autorizados. **Serviços e recursos** define os serviços e recursos padrão e **Permissões** controla o acesso. **Credenciais avançadas** reúne as ações de gestão da credencial. O endereço antigo que identifica esse formulário continua válido.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-google-fator3-0.43.1-instalador.zip](wp-mcp-google-fator3-0.43.1-instalador.zip) | 1012159 | `7cb4fd3ae52eb3a3b7ee484f074e65f0e36ba0ecbbd4f99762c2759457975a84` |
| Fonte | [wp-mcp-google-fator3-0.43.1-fonte.zip](wp-mcp-google-fator3-0.43.1-fonte.zip) | 32142714 | `5b67317adffbfb996ade08c0f5367ecb37be9a2ba8f0473fd3c4e54efc7cb8f7` |
| Caderno visual, 20 páginas | [wp-mcp-google-fator3-0.43.1-prova-visual.pdf](wp-mcp-google-fator3-0.43.1-prova-visual.pdf) | 2975269 | `45ed49fef3c4002f0b80b373610aef50268ea1193acbdf02772b554455454b0e` |

O instalador contém 214 arquivos e duas compilações produziram bytes idênticos. A árvore de fonte inclui o código de execução, os geradores de build, os testes, as medições e os JPEGs originais. O roteiro para refazer o caderno é `tests/native/visual0431/caderno.py`. A lista de pedidos após a entrega consta em `reproducao/PEDIDOS-0.43.1.md`.

Este é o relatório externo canônico. A cópia incluída na raiz do fonte antecede o fechamento desse ZIP. Os 214 arquivos do instalador foram comparados, byte a byte, com os correspondentes na árvore de fonte.
