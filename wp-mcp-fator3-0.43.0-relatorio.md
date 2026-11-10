# Entrega — Fator3 MCP 0.43.0

Revisão 1 · 10/11/2026 · Correção de **Pedidos MCP 79** · **apta-no-escopo-testado**. O Site-Teste executa a versão 0.43.0. O atalho **Notas desta versão** abriu as notas da 0.43.0 no painel autenticado.

## 1. De onde a versão entra

Instalação limpa ou atualização direta do MCP 0.42.0, última entrega deste pacote e versão observada no Site-Teste antes da troca. A base conferida tem instalador de 939.742 bytes, SHA-256 `d423deb27cc8fe2daaf65a3bf34f42505afdc990f8eac216d383d32a0f1244e0`, e fonte de 4.401.612 bytes, SHA-256 `a783a342f9b2cc36c02a36d6ffead3b735b678ebe1ae011934511baaf1a26513`.

Os requisitos mínimos do plugin são WordPress 7.1.4 e PHP 8.3. A bancada usou WordPress 7.1.4, PHP 8.3.6 e MySQL 8.0.46. O Site-Teste informou WordPress 7.1.4 e PHP 8.3.36. Documentos centrais lidos integralmente: `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos na revisão 5 de 02/11/2026. A aba vigente do MCP traz o pedido 79. Também foi conferida a regra comum de entrega de 16/10/2026.

## 2. Convivência e encaminhamentos

| Pacote | Versão ativa na bancada integrada e no Site-Teste |
|---|---|
| Fator3 Site Core | 1.77.0 |
| Fator3 MCP Google | 0.31.0 |
| Fator3 MCP Meta | 0.21.0 |
| Fator3 MCP LinkedIn | 0.19.0 |
| Fator3 MCP Pipedrive | 0.8.0 |

O Core 1.77.0 foi fornecido com fonte, instalador e relatório. Os ZIPs coincidiram com os hashes do mantenedor: instalador `428b7dbfb2c8c0b9a072559c9295a49bec4a7619fbb490eead97aeee60ffb1f5` e fonte `4c8c167b2a668c68b9074ffbded56fd01ee340f19be813c2712cb72df4a2fbdd`. Os demais instaladores correspondem ao conjunto vigente identificado no Site-Teste. A bancada verificou a ativação dos acompanhantes e a descoberta de uma habilidade de cada um.

A correção usa o catálogo documental e a versão do próprio MCP. A comparação dos 167 contratos próprios instalados com a 0.42.0 confirmou os mesmos nomes e schemas de entrada e saída. A revisão das interfaces de documentação, transporte e registro de provedores não identificou alteração a encaminhar a outro pacote. A troca desta rodada envolve apenas o MCP.

## 3. Mudanças e evidência

**Pedidos MCP 79 — implementado, validado-localmente e validado-wordpress.** A tela de Ajuda tinha o identificador `release-0400` fixo no endereço de **Notas desta versão**. O atalho agora compõe o identificador com a mesma constante de versão usada por `system/health`. A mudança está em `includes/views/help.php`. O seletor continua permitindo consultar versões anteriores, e o link sobre pré-imagens na tela **Arquivos e banco** continua vinculado ao documento específico da 0.42.0.

| Verificação no Site-Teste | Antes | Depois |
|---|---|---|
| Versão do MCP | 0.42.0 | 0.43.0 |
| Destino lido do HTML do atalho | `release-0400` | `release-0430` |
| Documento selecionado após seguir esse endereço | `release-0400` | `release-0430` |
| Título apresentado | Fator3 MCP 0.40.0 — administração de clientes e configuração do site | Fator3 MCP 0.43.0 — Notas da versão instalada |

A sonda leu o HTML do painel administrativo por HTTPS autenticado, extraiu o endereço do link e abriu esse endereço em uma segunda requisição. Uma chamada independente a `system/health` confirmou a versão 0.43.0 e `healthy=true`. Os 783 bytes de notas apresentados nessa tela tiveram o mesmo SHA-256 da leitura integral por `system/guide` e do documento distribuído: `1af50ffb7edc520aa93b8769391b362c573f7110cb939c5e8b7d9adec9bae481`.

## 4. Instalação e prova de prontidão

No Site-Teste, o instalador foi transferido em quatro partes. Após verificar tamanho e SHA-256 no servidor, `plugins/upload-base64` recebeu `zip_path`, `expected_slug=wp-mcp-fator3`, o hash da seção 8, `overwrite=true` e `activate=true`. A operação `14e029f8f1ff041767fa552894c0cd86` registrou 0.42.0 → 0.43.0, ativo antes e depois. Pré-imagem da troca: `14b3e07f8046c39fea8cf77f`. A página inicial e a raiz REST responderam HTTP 200 antes e depois. As sessões de teste foram encerradas. A ausência do ZIP temporário e da sonda de homologação foi confirmada após sua remoção.

| Ambiente | Resultado |
|---|---|
| WordPress descartável | 123 verificações aprovadas. Foram 3 na base, 54 na instalação limpa e 66 na atualizada. A cobertura inclui reprodução do defeito, destino do link, notas históricas, documento desconhecido, permissão administrativa, preservação de dados e leitura integral dos 42 documentos em cada instalação candidata. |
| Navegador | Chromium 156.0.8078.79 clicou no link a 1.365 e a 390 px de largura e comparou o texto completo exibido com o Markdown canônico. |
| Pacote | Todos os 477 arquivos instalados nos dois ambientes corresponderam ao ZIP. Os 461 arquivos PHP passaram no lint e o JavaScript próprio passou na verificação de sintaxe. O build reproduziu o SHA-256 da seção 8. |
| Documentação instalada no Site-Teste | Os hashes dos 42 documentos anunciados por `system/guide` corresponderam ao fonte. O MCP leu integralmente as notas da versão e os guias de administração, operação e atualização. O arquivo da tela instalada também coincidiu com o fonte. |

Para fazer a conferência manual, abra **Ferramentas → Fator3 MCP → Ajuda → Notas desta versão** e compare o título com `plugin_version` de `system/health`. As instruções de reprodução estão em `tools/release0430/README.md`. A evidência sanitizada está em `evidencias/0430/`.

## 5. Banco, migração e recuperação

O MCP continua com schema de dados 2. O atalho é calculado na renderização e dispensa opção, migração ou job. A atualização direta preservou a credencial de laboratório, o perfil de manutenção, o limite de arquivo e uma pré-imagem gerada na base. A instalação usou a recuperação de pacote existente. Em caso de interrupção, consulte o recibo com `plugins/operation-status`. Correções posteriores seguem por nova versão.

## 6. Pendências e limites da validação

O pedido 79 cumpriu o aceite no Site-Teste. A publicação do instalador e do relatório e a implantação nos demais sites cabem à frota, com conferência do SHA-256 dos bytes servidos pelo repositório raw. A bateria de navegador cobriu Chromium em duas larguras. Os testes dos acompanhantes cobriram ativação e registro de contratos. O fluxo de Ajuda é local e dispensa homologação em contas de fornecedores.

O guia geral **Administração** conserva no próprio título a referência à edição 0.41.0. Esse título histórico fica em documento separado das notas da versão, cujo destino e conteúdo foram conferidos na seção 3.

## 7. Credenciais e configuração do dono

O acesso à tela de Ajuda exige uma conta WordPress com `manage_options`. O operador usa a conexão administrativa MCP já autorizada para instalar o pacote e conferir a versão. A consulta estática por `system/guide` conserva sua permissão existente. O pedido 79 dispensa novos campos, senhas e tokens. A sonda de aceite exigiu permissão administrativa e restringiu as requisições ao endereço do painel do Site-Teste. A evidência contém somente metadados.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-fator3-0.43.0-instalador.zip](./wp-mcp-fator3-0.43.0-instalador.zip) | 940636 | `c0f3a10ad4275dc51abd4ab01ac9d2647914fb13d214b9e4f460cd989ddf4951` |
| Fonte | [wp-mcp-fator3-0.43.0-fonte.zip](./wp-mcp-fator3-0.43.0-fonte.zip) | 4407935 | `4f63b91ad094e1836cd04c3e5fc5b0b6aa4542ba63d57f01179d99f61a2dd4b4` |

Relatório externo canônico. A cópia incluída no fonte antecede o fechamento do ZIP. Checklist de encerramento da seção 14 conferido.
