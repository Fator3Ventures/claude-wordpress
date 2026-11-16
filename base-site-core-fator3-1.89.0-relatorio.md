# Entrega — Fator3 Site Core 1.89.0

Revisão 1 · 15/11/2026 · Implementação do pedido 414 · `base-site-core-fator3`

**Estado da entrega — `com-pendencias`.** Implementação concluída, instalada e ativa no Site-Teste. Em instalação limpa e na atualização da base em laboratório, os 26 identificadores do pedido passaram a devolver fichas completas. O aceite com sessões reais do CTO Office e da Korvena depende da distribuição dessa versão pela frota.

## 1. De onde esta versão entra

Instalação limpa ou atualização direta da **1.88.1**. Recuperei o runtime candidato, o instalador, o laboratório e as evidências do chat anterior. O instalador recuperado coincidiu byte a byte com a árvore da entrega e foi usado no Site-Teste. A retomada completou a prova com o Implantador, a navegação administrativa, a verificação remota e o fechamento dos arquivos.

A base foi conferida pelos hashes do instalador `102ccb77b229870bb03310a559c147ec8d2a6d9bf1e670aeffb5661c641801cc` e do fonte `4c17935c0468ce7346673e95c1a7a93bebd0e52fe2a467ae0d16a49c85c8eb87`. Os requisitos são WordPress 7.1.4 ou superior em instalação única e PHP 8.3 ou superior de 64 bits. Os dois cenários locais rodaram em WordPress 7.1.4 e PHP 8.3.6.

## 2. Convivência e encaminhamentos

O contrato administrativo permanece em **8.41.0**, com o perfil `piso-padrao-3.6`. O laboratório com os acompanhantes registrou **103 opções operáveis e 197 operações `f3base/*`**. A versão preserva o conjunto de operações da base. O detalhe de sessão ganha os dados comerciais de cada aparelho.

| Pacote | Versão | Verificação |
|---|---|---|
| Fator3 MCP | 0.46.0 | Transporte de documentação, prontidão e consulta no Site-Teste |
| Fator3 MCP Google | 0.36.0 | Ativo durante regressão local e após a troca no Site-Teste |
| Fator3 MCP LinkedIn | 0.24.0 | Ativo nos dois ambientes |
| Fator3 MCP Meta | 0.27.0 | Ativo nos dois ambientes |
| Fator3 MCP Pipedrive | 0.11.1 | Ativo nos dois ambientes |
| Fator3 Implantador | 2.23.0 | Código do instalador oficial carregado em laboratório. Dez verificações de versão, catálogo padrão, regras locais, geração de plano e restauração da configuração |

O Implantador 2.23.0 consulta o perfil e os contratos públicos do Core. No ensaio, uma lista local vazia permaneceu vazia. As regras específicas para Galaxy A10 e Moto E6s conservaram a prioridade após a geração do plano. O teste usou o instalador do Implantador com SHA-256 `b14123e5cd0d2f145b3e0dacb7bf811ebc45e240fa4836df37d6c761e3acca9a`. A primeira tentativa do chat anterior usou perfil de leitura. Na retomada, uma conta sintética do laboratório executou os quatro contratos necessários com permissão explícita, e a associação foi revogada após a prova. A análise e o ensaio encerraram a integração sem necessidade de mudança em outro pacote. A troca isolada do Core é suficiente.

## 3. Mudanças e evidências

| Pedido | Comportamento entregue | Evidência |
|---|---|---|
| 414(a) · Códigos da frota | Os 26 identificadores passam a ter marca, nome, ano, preço estimado positivo, faixa e classificação de linha premium. | `base-prova.json`, `limpa-414.json` e `upgrade-414.json` em `evidence/1890/`. A base devolveu 26 pendentes. A nova versão devolveu zero do pedido e manteve visível o identificador desconhecido de controle. |
| 414(b) · Abrangência | O catálogo foi de 1.156 para **1.346 códigos**. Entraram **190 códigos e 74 fichas**, com 147 códigos de 2017 a 2019. O arquivo de origem da 1.88.1 registrava quatro valores distintos na coluna marca, Samsung, Motorola, Xiaomi e realme. As quatro receberam modelos antigos. A versão também inclui OPPO, Infinix, TECNO e LG, além de registros Positivo e Nokia. | `catalogo.json` e `reference/414/`. As 74 fichas novas se dividem em 33 com referência de preço publicada e 41 com estimativa por comparável. Cada uma identifica o critério e a fonte. |
| 414(c) · Nome comercial | O índice compilado aceita variações de caixa, espaços e parênteses. A busca preserva o sinal “+” e distingue variantes. Nomes normalizados ambíguos ficam fora da associação automática. Regras locais continuam valendo. | Ensaios de variantes, ambiguidade e prioridade em `tests/pedido-414.php`. |
| 414 · Sessão retida | O detalhe em `f3base/sessao-detalhar` enriquece na leitura o perfil antes sem ficha. Em sessão do Moto E6s semeada na 1.88.1, a 1.89.0 retornou Motorola, 2020, **R$ 239,00**, entrada e linha premium “não”. | O hash do perfil gravado coincidiu antes e depois da atualização. A consulta preservou a cronologia e fez zero chamadas HTTP. |

Os preços têm data-base de 15/11/2026. A faixa considera a posição do produto na linha do fabricante. O catálogo completo é o CSV da seção 8. Os critérios e links por ficha nova ficam em `reference/414/referencias-precos.csv`.

## 4. Instalação e prova da troca

No Site-Teste, o ZIP temporário foi montado com verificação de tamanho e SHA-256, no mesmo domínio de homologação. `plugins/upload` recebeu a URL temporária, o SHA-256 da seção 8, `expected_slug=base-site-core-fator3`, substituição e ativação. Recibo `ac2b44616ab29e768b2a5c90a1b7252a`. A confirmação no executor levou **6 segundos**, entre `iniciado_em=1794784507` e `confirmada_no_executor_em=1794784513`. As 20 etapas terminaram com `versao_alvo=1.89.0`, `estado=concluida` e `falhas=0`.

| Prova | Resultado observado |
|---|---|
| Integridade e sintaxe | 999 arquivos de runtime conferidos contra o ZIP e o manifesto. Os 608 arquivos PHP passaram no lint. A raiz é `base-site-core-fator3/` e o basename publicado foi preservado. |
| WordPress limpo e atualização | 84 verificações do pedido 414 em cada cenário. No cenário de atualização, os registros vieram da 1.88.1. Em ambos, a consulta percorreu sete páginas e o controle desconhecido apareceu na saída. |
| Regressões | 263 verificações em cada cenário de instalação e 263 no ambiente com os cinco acompanhantes ativos. A bateria do pedido 413 passou em 215 verificações por cenário, com validação adicional do exportador CSV e do catálogo de 1.346 códigos. |
| Painel | Chromium exercitou 80 telas ou estados nas larguras de 360, 768 e 1.440 px. As 240 capturas passaram pela conferência de HTTP, versão, largura e ausência de erro crítico. As 13 interações de paginação, filtros, detalhe e exportação passaram. |
| Autorização | No WordPress local, o visitante sem autenticação teve o acesso negado a `f3base/aparelhos-sem-nome-ler` e `f3base/sessao-detalhar`. |
| Site-Teste | Home e REST responderam HTTP 200 antes e depois. O Core permaneceu ativo. A saúde final registrou zero módulos degradados e zero tarefas com falha na última execução. O arquivo temporário de instalação foi removido com guarda de hash. |
| Documentação por MCP | A leitura remota de `docs/DOCUMENTACAO.md` (42 páginas de até oito linhas), `docs/AGENTES-1.89.0.md` (uma) e `docs/RELEASE-1.89.0.md` (duas) reconstruiu os textos do ZIP. A versão e o hash permaneceram estáveis durante a leitura. O leitor recusou um documento fora do índice. |

A área `evidence/1890/` contém os resultados, inclusive `site-teste-final.json`, `painel.json`, `implantador.json` e o comparativo da frota. No Site-Teste a nova operação respondeu com zero códigos examinados, pois o ambiente não tinha observações retidas. A prova funcional com os 26 identificadores foi feita no WordPress de laboratório.

## 5. Banco, migração e correção por nova versão

O pedido 414 muda os dados embarcados e a resolução durante a consulta. A versão preserva tabelas, sessões, configurações e fichas históricas já identificadas. Na atualização local, o SHA-256 do perfil bruto do Moto E6s permaneceu `ba0c96b4dc4fa6477799955942122a2ee8adcc9b7f12c877904a2525fee443f5`. A leitura devolveu a ficha nova sem regravar o registro.

O Site-Teste registrou a pré-imagem dos arquivos do plugin antes da troca. A prova de preservação dos registros é do laboratório. Em caso de interrupção, consulte a etapa e o estado via `f3base/como-usar` e `f3base/saude-ler`. A correção de uma versão instalada segue por nova versão.

## 6. O que permanece pendente

**Aceite em produção pelo responsável da frota.** A releitura de 15/11 encontrou a **1.88.1** tanto no CTO Office como na Korvena. A listagem do CTO Office continha 32 códigos sem nome em 127 examinados, e a da Korvena continha um em três. Ao executar o catálogo embarcado da 1.89.0 sobre essas listas no laboratório, o Core identificou 30 dos 32 no CTO Office e um de um na Korvena. Os dois restantes, `infinix x6525b` e `m7_wifi`, estão fora dos 26 do pedido. As listas agregadas e o resultado local estão em `frota-retomada.json` e `frota-comparacao-local.json`.

Após receber e conferir o ZIP, a frota publica a entrega e verifica o SHA-256 servido pela URL raw antes de instalar. Nos dois sites, o aceite consiste em percorrer `f3base/aparelhos-sem-nome-ler` até `proximo_apos=null`, inclusive se uma página vier sem itens, e confirmar a ausência dos 26 códigos. No CTO Office, conferir também uma sessão retida do Moto E6s em `sessoes[]` de `f3base/sessao-detalhar`. A implantação em produção e essa leitura posterior seguem pendentes. A rodada não chamou fornecedores comerciais nem enviou mensagens reais de teste.

## 7. Credenciais e configuração do dono

O catálogo embarcado fica ativo com a atualização. Ele dispensa credenciais, importação e ações do Implantador. O administrador pode ajustar `f3base_medicao_editorial.catalogo_aparelhos` na tela de conteúdo, audiência e IA ou pelo contrato de configuração, com simulação e revisão esperada. O guia instalado descreve o formato das linhas.

## 8. Identidade dos arquivos

| Artefato | Arquivo | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [base-site-core-fator3-1.89.0-instalador.zip](base-site-core-fator3-1.89.0-instalador.zip) | 4547919 | `f48d257ab67f04a95dc50af8a3ea31241560380d8e1f740ff4574de84b6ef177` |
| Fonte | [base-site-core-fator3-1.89.0-fonte.zip](base-site-core-fator3-1.89.0-fonte.zip) | 116810124 | `522a6546b4b629478b3e2043168dd6bfe7bf1a4d99a1e5ec06a83d992beb7384` |
| Catálogo | [base-site-core-fator3-1.89.0-catalogo-aparelhos.csv](base-site-core-fator3-1.89.0-catalogo-aparelhos.csv) | 79288 | `7c5ec118fdfffc1a44b8de3b74bce54c6e667a1d07355dcfb80ea5db21dd232a` |

Este é o **relatório externo canônico**. A cópia no fonte foi congelada antes do empacotamento e remete a esta tabela para o tamanho e o hash do próprio ZIP. Para produção, a frota publica a entrega no destino previsto para o instalador. [URL raw prevista](https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/base-site-core-fator3-1.89.0-instalador.zip)
