# Entrega — Fator3 MCP LinkedIn 0.27.0

Revisão 1 · 20/11/2026 · nova versão de interface. **Implementada e homologada no Site-Teste para o escopo do painel.** O aceite administrativo usou WordPress real e dados sintéticos; não incluiu chamadas comerciais ao LinkedIn.

## 1. De onde esta versão entra

Atualização direta da 0.26.0 (instalador SHA-256 `607a7b432bcf974047cc648506087690ba46998aaf0dc931662f9ecadf2e02bd`) ou instalação limpa. Regras centrais: instrucoes-agentes-plugins-fator3.md e padrao-desenvolvimento-plugins-fator3.md, revisão 5 de 02/11/2026. Requisitos PHP 8.3 de 64 bits e WordPress 7.1.4. Em laboratório: WordPress 7.1.4, PHP 8.4.27; no Site-Teste: WordPress 7.1.5, PHP 8.3.37.

## 2. Convivência e encaminhamentos

| Plugin | Versão usada na integração |
|---|---|
| Fator3 Site Core | 1.100.1 |
| Fator3 MCP | 0.54.0 |
| Fator3 MCP Google | 0.42.0 |
| Fator3 MCP Meta | 0.31.0 |
| Fator3 MCP Pipedrive | 0.12.0 |
| Fator3 MCP LinkedIn | 0.26.0 de origem; 0.27.0 de destino |

Examinados os relatórios dos dois pacotes fornecidos e conferidos os cabeçalhos e hashes dos instaladores (`evidence/release0270/entradas.json`). O pedido de 20/11 “Fator3 MCP LinkedIn — ajustes de tela” enumera 15 ajustes visuais; não atribui um novo número de demanda ao cadastro central. A fronteira de Lead Sync e conversões com o Site Core, o transporte MCP e a interoperação com os demais provedores continuam iguais. A folha comum é local a cada pacote e não depende de carregamento pelo Meta ou pelo Core. Comparar o SHA-256 entre os seis instaladores da frota cabe à coordenação visual e não exige alteração de código ou relatório de impacto individual desta versão. Nenhum pacote ou guia oficial alheio foi modificado.

## 3. Mudanças e evidências

| Itens da proposta | Alteração no LinkedIn |
|---|---|
| 1–3: carga, escopo e cabeçalho | Cópia literal da folha comum 1.0.0 antes de admin.css, apenas na tela do plugin; raiz f3-ui, título nativo, descrição do grupo e versão separados, com hr.wp-header-end para o WordPress posicionar os avisos. |
| 4–5: navegação | Configurar tem Conexões, Ativos, Formulários, Conversões de aquisição e Etapas comerciais. Dados tem Relatórios, Coletas, Histórico e Anúncios e publicações. Suporte tem Diagnóstico, Retenção e Ajuda. Os links diretos de todas as subabas continuam válidos; os grupos também abrem sem JavaScript. O estado ativo acompanha o esquema de cores do usuário. |
| 6–9: estados e ações | Selos com texto e estados semânticos, resultado dispensável sob a barra administrativa, blocos avançados e de risco com os componentes comuns e barra de salvar no formulário. Falhas têm anúncio de erro; o botão Dispensar pode ser usado por teclado. A autorização, a prévia e a confirmação das operações de domínio permanecem no servidor. |
| 10–12: campos e listas | Rótulos ligados aos campos, notas abaixo, totais de lista e paginação, tabela de conexões com rolagem própria. Busca, seleção e edição preservadas. |
| 13–15: tela estreita e foco | Caixas de marcar nativas; botões e campos editáveis com alvo de 40 px e navegação de 44 px nas larguras estreitas; contorno de foco comum. |

Folha `assets/f3-ui.css`: 11886 bytes, SHA-256 `15ef0d932b1be12a541b8408b061ee276a4db9d6650476f92b5e2f41eefc0c2b`, idêntica ao arquivo avulso e ao bloco da Folha comum fornecida. A distribuição tem 102 arquivos. Em relação à 0.26.0: 61 idênticos, 39 modificados e dois novos, sem remoções. Os três schemas instalados, o código das 100 operações, o modelo de persistência e as rotinas de coleta permanecem iguais. A diferença completa está em `evidence/release0270/diff-runtime.json`.

## 4. Instalação e prova da troca

As suítes passaram com **136 verificações isoladas e 142 integradas**. O teste estrutural do painel fez 79 verificações de navegação, marcação e autorização. Cada teste de upgrade (isolado e integrado) fez oito verificações: as oito linhas de domínio e as duas de histórico mantiveram o respectivo conteúdo e a revisão. A ajuda foi lida integralmente pelo MCP: **54 documentos em 64 páginas**. Cada cenário executou o mesmo ZIP, registrou zero avisos ou erros PHP e descartou a base sintética. Matriz e evidências detalhadas: `evidence/release0270/matriz-nativa.json`.

No Site-Teste, enviamos o ZIP com `expected_slug` e `expected_sha256`. Operação `31adebbcc93a7b6245799403c2bcf0a2`; pré-imagem de arquivos `db8cf128bfd80ca79ca1cdf8`. Antes e depois, a página inicial e /wp-json/ responderam HTTP 200. Novas requisições confirmaram a versão 0.27.0 ativa, a saúde do WordPress e nove verificações locais do autoteste. O índice MCP remoto tem os mesmos 54 hashes dos manuais e schemas instalados. Estado observado após a troca: 0 conexões, 0 agendas e 0 linhas de histórico. A folha comum servida por HTTP no Site-Teste retornou 200, com os mesmos 11.886 bytes e SHA-256 do arquivo fornecido. Os documentos de administração e da versão foram lidos integralmente nesse site. Nenhum registro de domínio sintético foi criado no site compartilhado.

### Aceite visual por subaba

36 capturas integrais em Chromium e três larguras, com aviso de um plugin de laboratório independente. A conferência da seção 7 somou 474 verificações visuais e interativas sem falhas; o detalhe de medidas, teclado, esquema administrativo, navegação e estados está em `evidence/release0270/visual027/results.json`. Os números das colunas correspondem à seção 7 do Guia Visual. Critério 10 em 360 e 768 px; itens sobre tabelas/campos valem quando há o componente. Os links abaixo apontam para as imagens no **ZIP de fonte extraído**. Para consultar a partir deste relatório avulso, abra o caderno visual entregue ao lado dele: o índice permite selecionar subaba e largura, e mostra o primeiro viewport de cada captura.

| Subaba | 360 px | 768 px | 1440 px | 1. Folha e ordem | 2. Identidade | 3. Aviso alheio | 4. Navegação | 5. Esquema WP | 6. Selos | 7. Campos | 8. Tabelas | 9. Largura | 10. Toque | 11. Foco | 12. CSS local |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Conexões | [Captura](evidence/release0270/visual027/360-connections.webp) | [Captura](evidence/release0270/visual027/768-connections.webp) | [Captura](evidence/release0270/visual027/1440-connections.webp) | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim |
| Ativos | [Captura](evidence/release0270/visual027/360-assets.webp) | [Captura](evidence/release0270/visual027/768-assets.webp) | [Captura](evidence/release0270/visual027/1440-assets.webp) | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim |
| Formulários | [Captura](evidence/release0270/visual027/360-leads.webp) | [Captura](evidence/release0270/visual027/768-leads.webp) | [Captura](evidence/release0270/visual027/1440-leads.webp) | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim |
| Conversões de aquisição | [Captura](evidence/release0270/visual027/360-conversions.webp) | [Captura](evidence/release0270/visual027/768-conversions.webp) | [Captura](evidence/release0270/visual027/1440-conversions.webp) | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim |
| Etapas comerciais | [Captura](evidence/release0270/visual027/360-stages.webp) | [Captura](evidence/release0270/visual027/768-stages.webp) | [Captura](evidence/release0270/visual027/1440-stages.webp) | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim |
| Relatórios | [Captura](evidence/release0270/visual027/360-reports.webp) | [Captura](evidence/release0270/visual027/768-reports.webp) | [Captura](evidence/release0270/visual027/1440-reports.webp) | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim |
| Coletas | [Captura](evidence/release0270/visual027/360-jobs.webp) | [Captura](evidence/release0270/visual027/768-jobs.webp) | [Captura](evidence/release0270/visual027/1440-jobs.webp) | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim |
| Histórico | [Captura](evidence/release0270/visual027/360-history.webp) | [Captura](evidence/release0270/visual027/768-history.webp) | [Captura](evidence/release0270/visual027/1440-history.webp) | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim |
| Anúncios e publicações | [Captura](evidence/release0270/visual027/360-management.webp) | [Captura](evidence/release0270/visual027/768-management.webp) | [Captura](evidence/release0270/visual027/1440-management.webp) | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim |
| Diagnóstico | [Captura](evidence/release0270/visual027/360-diagnostics.webp) | [Captura](evidence/release0270/visual027/768-diagnostics.webp) | [Captura](evidence/release0270/visual027/1440-diagnostics.webp) | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim |
| Retenção | [Captura](evidence/release0270/visual027/360-retention.webp) | [Captura](evidence/release0270/visual027/768-retention.webp) | [Captura](evidence/release0270/visual027/1440-retention.webp) | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim |
| Ajuda | [Captura](evidence/release0270/visual027/360-help.webp) | [Captura](evidence/release0270/visual027/768-help.webp) | [Captura](evidence/release0270/visual027/1440-help.webp) | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim |

## 5. Banco, migração e recuperação

A mudança é de apresentação. Não acrescenta tabelas, colunas, options ou migração de domínio. A fotografia de upgrade contém conexão, concessão, job, mutação, configuração, prova, agendas e histórico. A atualização mantém estes registros; não é necessário recriar conexões, tokens ou agendas. Retomada de jobs, migrações já existentes e recibos permanecem na camada de domínio da base. A versão instalada é imutável: uma correção posterior exige novo número.

## 6. Limites e ações do responsável

O Site-Teste não estava conectado a uma conta comercial LinkedIn. Nenhum token foi renovado em conta real, nenhum desafio ou notificação de webhook foi enviado, e não houve criação/alteração de anúncios, publicação nem conversão real. Esta versão não altera essas funções. A homologação visual foi feita em Chromium sobre WordPress real com perfis e registros sintéticos. A frota decide a instalação em produção e a conferência dos demais pacotes contra o hash canônico.

## 7. Credenciais e configuração

O dono fornece os segredos da integração em Configurar → Conexões (Access Token e, conforme o fluxo, segredo do aplicativo/token de renovação); identificadores, conexões, contas, Pages, formulários, ações e escopos são selecionados e conferidos no próprio painel. Os campos secretos permanecem mascarados. Lead Sync e concessões continuam exigindo os ativos selecionados, escopos do aplicativo e permissões aprovadas pelo LinkedIn; a assinatura usa a callback já configurada no consumidor. Simulação e confirmação continuam obrigatórias onde aplicáveis. O cliente do Site Core para captação permanece sob sua própria configuração; não há nova credencial nem migração para o redesign.

## 8. Arquivos

- Instalador: `wp-mcp-linkedin-fator3-0.27.0-instalador.zip` · **467462 bytes** · SHA-256 `53c85e6a377d534ad172334cf6d26b7880a0c0830935cc2c459c6e20888b9db8`.
- Caderno visual: `wp-mcp-linkedin-fator3-0.27.0-caderno-visual.pdf` · **3449875 bytes** · SHA-256 `58a7d7a42663bfc10f9f06cab1d4f1e64cc689893f958413537d5ff5279cb2b6`.

Fonte: `wp-mcp-linkedin-fator3-0.27.0-fonte.zip` · **11752609 bytes** · SHA-256 `813497b2cad50536955b894964c523b5573d11df354fe4caf29c0d779d646869`. A cópia interna do relatório antecede esse cálculo.
