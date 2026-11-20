# Entrega — Fator3 MCP Pipedrive 0.13.0

Revisão 1 · 20/11/2026 · Interface, testes e documentação
Slug: wp-mcp-pipedrive-fator3 · Build: 0.13.0 · **Status: com-pendencias**

## 1. De onde esta versão entra

Instalador para WordPress limpo ou atualização direta **0.12.0 → 0.13.0**. Base oficial recuperada e conferida: 489789 bytes, SHA-256 813923a62af52c58a3f39bfa658f51fab75a87ba0b3327ac76133d3aad6b5792. Fonte-base: SHA-256 bd69147f8880d3a95b62114f17afc0b0216692c39e100fd5b58a4ad726bc1317.

Foram lidos integralmente instrucoes-agentes-plugins-fator3.md e padrao-desenvolvimento-plugins-fator3.md, ambos na revisão 5 de 02/11/2026, além do padrão Pipedrive, regra comum, ajustes de tela, Guia Visual e Folha comum de 20/11/2026. Referências em reference/0130. O padrão completo rege a precedência. A divergência entre altura móvel do guia e CSS é documentada, sem declaração de conformidade integral.

Requisitos: WordPress 7.1.4+ e PHP 8.3+ de 64 bits, OpenSSL, mbstring e InnoDB. Prova local: WordPress **7.1.4**, PHP **8.3.6**, MariaDB **11.8.6**, Chromium **142.0.7444.175**. O Site-Teste observado usa WordPress 7.1.5 e PHP 8.3.37; seu Pipedrive permaneceu em 0.12.0.

## 2. Convivência e encaminhamentos

Conjunto final testado, com instaladores originais e comparação de cada arquivo: **Core 1.100.1, MCP 0.54.0, Google 0.42.0, Meta 0.31.0 e LinkedIn 0.27.0**. O LinkedIn estava na 0.26.0 no início e avançou no compartilhado durante a rodada, por ação externa; a matriz foi repetida com a 0.27.0. Hashes dos cinco ZIPs em evidence/0130/companion-installers.json.

| Destinatário | Classificação e situação | Referência | Encaminhamento |
|---|---|---|---|
| Site Geral / Todos | Validação coordenada, aberta | Guia Visual e folha f3-ui 1.0.0, sem novo número | [wp-mcp-pipedrive-fator3-0.13.0-impacto-site-geral.md](wp-mcp-pipedrive-fator3-0.13.0-impacto-site-geral.md), revisão 1; patch preciso e 10 medições experimentais |
| Site Core | Fronteira revalidada, sem patch necessário | Pedido Core 430; impacto anterior Pipedrive 0.12.0, revisão 2 | 16 verificações atuais de abertura, recuperação, leitura, incerteza e reconciliação; recebimento real continua com dono/frota |

Os 23 schemas de entrada e saída são iguais aos da 0.12.0; somente o identificador de versão documental avança. Não há novas opções, rotas, permissões, jobs ou dependências. Nenhum impacto de código adicional foi identificado nos demais acompanhantes no escopo examinado. O Core atual descarta a abertura ainda não enviada ao recuperar o episódio; o teste foi ajustado após examinar recuperar/retirar_pendentes, e cobre também a recuperação da abertura reconciliada como aceita. A projeção pública do Pipedrive já atende ao contrato.

## 3. Mudanças e evidência

Pedido exato: **Fator3 MCP Pipedrive — ajustes de tela**, base 0.12.0, 20/11/2026; 18 itens, sem número novo.

| Itens | Problema e mudança | Evidência |
|---|---|---|
| 1–3 | Folha comum antes da folha de domínio; raiz f3-ui; cabeçalho com h1, descrição por grupo, versão e hr.wp-header-end. | Hash da folha idêntico; aviso externo fora do cabeçalho nas seis subabas. |
| 4–8 | Navegação em dois níveis, seções e estados comuns; estilos locais obsoletos removidos. | Nomes, ordem, slugs, links antigos e capacidade manage_options preservados; foco e mudança de cor do perfil verificados. |
| 9–13 | Métricas, avisos, índice, alternadores, barra compacta de revisão e cartões de edição. Remoção de linha recolhida, sujeita à prévia/confirmacão existente. | Edição guiada/JSON, erro escapado, confirmação, cancelamento e retorno dispensável exercitados. |
| 14–18 | Filtros, total, paginação e rolagem interna de tabelas; tipografia e tokens comuns. | Busca além da primeira página; sem duplicação; três larguras; campos móveis com pendência comum detalhada abaixo. |

Documentação instalada atualizada: guia do painel, instalação, operação, contratos, agentes, exemplos, especificação, índice e changelog. A folha própria ficou com layout específico do domínio e sem cores/medidas em pixels próprias. As capturas estão no [caderno visual](wp-mcp-pipedrive-fator3-0.13.0-prova-visual.html); todas usam dados sintéticos.

## 4. Instalação e prova da troca

**O pacote novo não foi instalado no Site-Teste nesta rodada.** O acesso ao compartilhado foi somente de leitura; estado final saudável, Pipedrive 0.12.0, acompanhantes nas versões finais da seção 2. Não há URL raw nova publicada nem recibo de implantação da 0.13.0. A publicação/instalação pela frota deve usar o instalador desta entrega, expected_slug=wp-mcp-pipedrive-fator3 e o SHA-256 da seção 8, conferindo os bytes da URL raw oficial antes da troca.

| Ambiente | Cenário | Resultado | Evidência e limite |
|---|---|---|---|
| WP local limpo | Instalação do ZIP final e regressões | **650/650** | clean/*.json; fornecedor sintético, rede e e-mail externos bloqueados |
| WP local com 0.12.0 | Atualização, comparação e nova requisição | **17/17** | upgrade/*.json; regras, revisão, retenção, recibos, diário, progresso e bloqueios preservados |
| Cinco acompanhantes originais | Contrato Core, permissões e executor MCP | **109/109** | matrix/*.json; todas as árvores iguais aos instaladores oficiais |
| Chromium | Guia: 12 critérios × 6 subabas | **67/72**, cinco pendências | browser0130.json; 18 capturas principais e esquema Café |
| Chromium | Verificações adicionais, listas e edição | **35/35 + 51/51 + 29/29** | browser0130.json, browser0110.json e browser090.json |
| Chromium com Core/MCP originais | Contagem e consulta de incidentes | **18/18** | browser0120-matrix.json; três capturas adicionais, transporte sintético |
| Cópia experimental da folha | Campos móveis e largura | **10/10** | common-proposal.json; correção não integra a folha oficial entregue |
| Build | Lint, ZIP, schemas, inventário e reprodução | **14/14**, 69 arquivos PHP | package.json; 44 arquivos de runtime, sem QA |

Documentação pelo executor MCP original: os **12 documentos**, em **88 páginas de 2.048 bytes**, foram lidos integralmente e comparados aos hashes/bytes do runtime. Descoberta: 23 operações na versão 0.13.0. Operação para conferência após implantação: pipedrive/documentacao-ler com documento=index e, depois, release; seguir proximo_offset e sha256_esperado. Essa prova usa o executor PHP nativo do MCP em WordPress real; não representa uma nova sessão HTTP MCP no compartilhado.

Os testes principais terminaram em 0.13.0, com logs PHP vazios e zero erros Pipedrive nos três cenários. O plugin de aviso, o cliente sintético do navegador e o arquivo de senha foram removidos pela rotina de limpeza. A folha experimental foi restaurada byte a byte. Nenhum componente temporário entra no instalador.

## 5. Banco, migração e correção por nova versão

A revisão muda apresentação e documentação; não cria migração de tabelas nem amplia permissões. A atualização da base preservou o conteúdo comparado byte a byte e a retenção personalizada de 730 dias. Não habilita cadência nem concede autorização ao fornecedor. Para recuperação, preservar banco, salts e recibos de efeitos externos; uma correção posterior à instalação deve ser publicada como nova versão. A restauração de dados locais não desfaz uma operação comercial já executada no fornecedor.

## 6. O que permanece pendente

- **Site Geral / Todos:** cinco pendências do critério 10: Diário, Regras, Retenção, Pendências e Ajuda contêm inputs de 36 px. O guia exige 40 px. Folha comum preservada, proposta testada e encaminhada no impacto individual. Por isso o status é com-pendencias.
- **Aviso externo sem JavaScript:** nas seis rotas móveis o conteúdo Pipedrive mede 338 px e a navegação funciona, mas o botão longo da fixture externa fica fora do contêiner e leva o documento a 487 px. Com JavaScript ativo, o WordPress reposiciona o aviso junto ao divisor e a página mede exatamente 360 px. O ensaio não altera a folha global nem o código de outro plugin. Não se declara ausência de transbordamento global nessa combinação sem JavaScript.
- **Frota:** publicar os artefatos permitidos, validar a URL raw e instalar/homologar a 0.13.0 no Site-Teste. O fonte não foi publicado em repositório público. Não houve implantação de produção.
- **Dono/frota:** aceite comercial anterior em conta real e recebimento de avisos técnicos continuam pendentes. A bancada não enviou WhatsApp, e-mail real nem gravação ao Pipedrive. Testes simulados não encerram esse aceite.

## 7. Credenciais e configuração do dono

Não há credencial nova. O token e a autorização do consumidor operacao continuam no Fator3 Site Core. No WordPress: Ferramentas → Fator3 MCP Pipedrive; Configurar → Regras de operação para horários, textos e motivos; Configurar → Retenção para o prazo. O destinatário técnico é configurado no Core. Alterações exigem manage_options e os mecanismos existentes de nonce, titular, revisão e confirmação.

## 8. Identidade dos arquivos

| Artefato | Nome | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-pipedrive-fator3-0.13.0-instalador.zip](wp-mcp-pipedrive-fator3-0.13.0-instalador.zip) | 498605 | a460c89705de5ed7b5e2b839f115bc9df6a0316edb3036d451e3e189465467db |
| Fonte | [wp-mcp-pipedrive-fator3-0.13.0-fonte.zip](wp-mcp-pipedrive-fator3-0.13.0-fonte.zip) | 10067738 | ca6acf5776fc6d8fe5eaaa982cd8a856431b85e7625fa1f7d18b85764f59b6d1 |

Relatório externo canônico. A cópia no fonte é anterior ao fechamento; seu próprio tamanho/hash só aparecem no relatório externo. O fonte inclui código, build, testes, referências, capturas, medições, checklist e impacto; nenhum ZIP contém outro ZIP. Complementos: impacto Site Geral e caderno visual com 22 capturas selecionadas. Os hashes finais de todos os artefatos constam no manifesto externo.
