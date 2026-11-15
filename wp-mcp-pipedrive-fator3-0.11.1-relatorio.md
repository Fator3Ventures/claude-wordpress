# Entrega — Fator3 MCP Pipedrive 0.11.1

Revisão 1 · 14/11/2026 (São Paulo) · **apta-no-escopo-testado**: Pedido 13 validado em WordPress; versão instalada e ativa no Site-Teste. Produção e CRM real não foram alterados. Slug: wp-mcp-pipedrive-fator3.

## 1. De onde esta versão entra

Instalação limpa de site único e atualização direta da 0.10.0 ou da 0.11.0. Não instale a 0.11.0 como passo intermediário. A 0.10.0 é a base da rodada: instalador de 460.556 bytes, SHA-256 7d021e6117c3dd10d8b64059fefced863736ecf90f30e89942e6e32b4569ceb4; fonte SHA-256 00705cab5640591a4c06b6077612aa3116f9dc2c9ac4af62b3f6335da5943675. A 0.11.0 foi instalada primeiro no Site-Teste; a 0.11.1 corrigiu um rótulo identificado na revisão visual e reconhece esse mesmo rótulo na busca.

Requisitos: WordPress 7.1.4+, PHP 8.3+ de 64 bits com OpenSSL e banco InnoDB. Bancada executada: WordPress 7.1.4, PHP 8.3.6, MariaDB 11.8.6 e Chromium 150.0.7871.181. As normas instrucoes-agentes-plugins-fator3.md e padrao-desenvolvimento-plugins-fator3.md foram lidas na revisão 5 de 02/11/2026. Pedido e padrões específicos desta rodada estão em inputs/.

## 2. Convivência e encaminhamentos

| Pacote | Versão da matriz final e do Site-Teste | Verificação |
|---|---:|---|
| Fator3 Site Core | 1.87.3 | Registro do consumidor, status, orçamento, autorização/recusa e recibos. |
| Fator3 MCP | 0.45.0 | Descoberta, schemas, execução, permissões e leitura integral dos documentos. |
| Fator3 MCP Google | 0.36.0 | Ativação e paridade da árvore instalada com o ZIP. |
| Fator3 MCP Meta | 0.27.0 | Ativação e paridade. Referência visual do pedido: 0.26.0. |
| Fator3 MCP LinkedIn | 0.24.0 | Ativação e paridade. Referência visual do pedido: 0.23.0. |

A matriz final foi executada com cinco instaladores locais identificados por SHA-256, no conjunto encontrado **após a ativação da 0.11.1**. No início da rodada as versões de Google, Meta e LinkedIn eram 0.35.0, 0.26.0 e 0.23.0. As trocas desses pacotes não foram feitas pela implementação do Pipedrive. Manifesto final: evidence/0111/companion-installers.json. Sem dependência de ordem nova. A operação com CRM requer o cliente do Core; uso via agente requer o MCP. Não há alteração exigida no código dos acompanhantes. O documento de impacto do Core descreve a revisão de contexto e os resultados de recusa; o canal MCP conserva as 22 interfaces.

**Escopo comercial mantido.** Leitura por lista fechada de leads, notas, campos, filtros, etiquetas, tipos de atividade, usuário atual, negócios, pessoas, organizações, atividades, funis e etapas. Escrita genérica por prévia/confirmar: leads e notas, exclusões específicas de registros e manutenção autorizada de campos, filtros e etiquetas. Os fluxos dedicados registram WhatsApp já enviado, encerram ou editam lead arquivado e registram perda. Métodos, caminhos e chaves exatos: SPECIFICATION.md, documento MCP especificacao. Ficam fora HTTP arbitrário, envio de WhatsApp, manipulação de token e endpoints de campos v2 não homologados.

## 3. Mudanças e evidência

**Pedidos MCP Pipedrive 13 — implementado e validado em WordPress.** Cabeçalho com o nome, uma descrição e versão à direita. Os três grupos quebram linha; a subaba ativa tem sublinhado e indicação acessível. Cartões explicam a tarefa e suas ações; estados têm cor e texto. Formulários passam para uma coluna e as regras avançadas continuam recolhíveis.

| Grupo | Destinos e mudança verificável |
|---|---|
| Operação | Visão geral distingue autorização e cadência. Diário pesquisa todo o histórico por operação, ID, método e resultado, cruza filtros e mostra intervalo, total, Anterior e Próxima. |
| Configurar | Regras de operação conserva editor guiado/JSON, simulação e confirmação. Retenção explica o efeito de zero e o aceite explícito para expurgo futuro. |
| Suporte | Pendências pesquisa e conta somente itens da conta e do administrador, em grupos de dez. Os rótulos, como “Registrar perda” e “Sem prova da intenção”, também funcionam na busca. Ajuda oferece pesquisa no índice e nas tabelas de referência. |

No diário, a contagem usa somente metadados públicos selecionados; a prova selada não é pesquisável. Em telas estreitas a tabela tem rolagem própria. Links de abas anteriores usam redirecionamento 302 em GET; mantêm documento, modo JSON, filtros, cursor e resultado de formulário. O diário preserva o antigo ponto de entrada e aponta para Pendências e Retenção. Os formulários continuam protegidos no servidor e o retorno após envio usa 303.

**835 verificações aprovadas, zero falhas:** 631 em instalação limpa, 17 na atualização da 0.10.0, 17 na atualização da 0.11.0, 90 na matriz final e 80 em navegador (51 para navegação, rótulos, busca e layout; 29 para fluxos de edição, autorização, retenção e navegação). Os 19 controles de empacotamento/encerramento são adicionais. Asserções e versões: evidence/0111/. O ZIP de capturas contém **18 PNGs originais de páginas inteiras**, com índice: seis abas × 360, 768 e 1440 px. São do wp-admin autenticado da bancada, com dados sintéticos. A página de diário foi testada também sem JavaScript.

## 4. Instalação e prova da troca

Instale apenas o ZIP instalador, com substituição do plugin ativo. No Site-Teste usou-se plugins/upload-base64 com expected_slug e SHA-256; a sondagem de / e /wp-json/ retornou HTTP 200 antes e depois. Recibo final: 0cf5bb6d0e4bb58d618b1dc240385e22. Ativo: **0.11.1**. Saúde geral positiva. No MCP, as 22 operações anunciam a versão nova com os mesmos schemas da 0.10.0. Os 12 documentos foram relidos integralmente no site por pipedrive/documentacao-ler com revisão fixada: **156.192 bytes, 26 partes**, comparadas com os bytes do instalador.

Em pipedrive/status, o Site-Teste informa cliente registrado e contrato pipedrive-api-client/1.0.0. Manteve **operacao_nao_autorizada**, com chamada_externa=false. Conta e saldo reais não são inferidos desse retorno. Em instalação autorizada, o esperado é code=ok, conta reconhecida, revisão e orçamento local válidos. Esse ramo foi exercitado com Core original e resposta sintética do fornecedor. A frota pode confirmar a versão visual em Ferramentas → Fator3 MCP Pipedrive → Operação → Visão geral.

## 5. Banco, migração e correção por nova versão

Sem tabela, coluna, índice ou opção nova. Abrir abas e pesquisar não inicia escrita comercial. As duas migrações preservaram regras brutas e revisão, retenção de 730 dias, recibos, progresso, pendência e diário; os cenários tinham cinco operações e três linhas do diário. Repetir recibo válido não escreveu, e a troca de contexto impediu repetição incompatível. No Site-Teste, regras e retenção permaneceram idênticas; operações, diário e marcadores de pendência permaneceram em zero. Configurações do Core e permissões não foram modificadas.

Uma troca de arquivos não desfaz atos comerciais, expurgos já realizados nem restaura a validade de prévias de uma revisão anterior. Para corrigir após instalação, publique uma versão posterior e confirme novamente a integridade; não se exige downgrade.

## 6. O que permanece pendente

O Pedido 13 tem evidências visuais e funcionais completas na bancada e prova de instalação no Site-Teste. Homologação comercial em conta Pipedrive real e inspeção visual em korvena.com.br não foram executadas. A recusa do Site-Teste já existia antes da rodada; não foi necessário habilitar acesso comercial para testar este pedido. Não houve medição com volume de produção; buscas amplas no diário e contagem exata de pendências dependem do tamanho do histórico local. As checagens de rolagem e teclado foram feitas no Chromium; não se declara teste em Safari, Firefox ou tecnologia assistiva externa. Publicação raw/main, troca na frota e aceite em produção ficam para a distribuição.

## 7. Credenciais e configuração do dono

Nenhuma credencial é informada no Pipedrive desta entrega. O token, a identidade da conta, o orçamento e a autorização do consumidor ficam no Fator3 Site Core. Não é necessário reconfigurá-los para instalar. Para homologar operação comercial, use uma conta autorizada e confira a identidade em pipedrive/status antes de simular.

## 8. Identidade dos arquivos

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-pipedrive-fator3-0.11.1-instalador.zip | 474886 | 02fc0692722488de17174a59b58b80217a5609f2c8a4a586ca6016951532dcc5 |
| wp-mcp-pipedrive-fator3-0.11.1-fonte.zip | 4482246 | 93b52f536e211ac5d857f57d931a9842fec676a487aed1cad763a7868c3f02e6 |
| wp-mcp-pipedrive-fator3-0.11.1-capturas.zip | 4125837 | da5e1c3c490061cbeeca1e0837dff731ea7c9b57853261b60353d5fdeca0ad9f |
| wp-mcp-pipedrive-fator3-0.11.1-impacto-base-site-core-fator3.md | 2366 | a248e45180a1d7f013b83f89ed3e8262f471bf933e9919c074fef46304878ba9 |
