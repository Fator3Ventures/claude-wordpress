# Fator3 Site Core 1.77.0

Revisão 1 · 10/11/2026 · Pedidos core 386, 387 e 388 · Slug `base-site-core-fator3` · Contrato administrativo 8.38.0.

**Estado da entrega — com-pendencias de aceite em produção para a medição de CLS do pedido 388.** Implementação concluída. Os três pedidos passaram no Site-Teste.

## 1. Base e requisitos

Atualização direta da 1.76.0 ou instalação limpa. A base conferida tem instalador SHA-256 `d830b488509814f44f4d78109cf8669e6b09717d9cbc50a0b42a1545f4a5f3ea` e fonte `b15aa3ee61fa0a035e92d9a869f98ff470992de50c92462e375a5199fcfd5de7`. Os pedidos vieram da revisão de 10/11 da lista Fator3 Site Core. Foram lidos `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos na revisão 5 de 02/11/2026. Mínimos de instalação única do Core confirmados no cabeçalho e no manual: WordPress 7.1.4 e PHP 8.3 de 64 bits.

## 2. Pacotes vigentes e impactos

O Site-Teste executou Core 1.77.0, MCP 0.42.0, Google 0.31.0, Meta 0.21.0, LinkedIn 0.19.0 e Pipedrive 0.8.0. A implantação, a auditoria e a leitura da sessão e dos documentos usaram o MCP 0.42.0 instalado. Conferi a integridade dos dois ZIPs anexados, os hashes informados pelo mantenedor e os 420 arquivos presentes nas duas árvores. O relatório do mantenedor atribui à nova versão a mudança no contrato de poda dos backups.

O Core resolveu os três pedidos em suas próprias interfaces. A classe é opcional nos blocos existentes e o nível de cobertura comercial continua no campo anterior. A origem chega em um campo aditivo. A análise do planejamento e da entrega não identificou desenvolvimento obrigatório no MCP, Google, Meta, LinkedIn, Pipedrive ou Implantador. A marcação dos grupos de conteúdo de Korvena é atividade editorial da equipe do site. A homologação de ponta a ponta com serviços de anúncios, CRM e disparos externos está fora dos três critérios desta rodada.

## 3. Implementação e aceite

| Pedido | Alteração | Evidência no Site-Teste |
|---|---|---|
| 386 · Alvos por classe | O tratamento de clique inerte procura declarações no nó tocado e nos ancestrais até a seção. O atributo válido vence no mesmo nó e a primeira classe válida resolve o empate. A auditoria propaga a cobertura e informa classes concorrentes. A classe não acrescenta CSS, arquivo ou varredura inicial. | Chromium clicou nos dois textos. A leitura de `f3base/sessao-detalhar` encontrou `teste-grupo` e `teste-atributo` na seção `homologacao`. O filtro incluiu automação para exibir a sessão do Chromium. O Gutenberg abriu o grupo como bloco válido, gravou a página pela REST do editor (HTTP 200) e preservou a classe no HTML servido. Na auditoria posterior, nenhum dos dois parágrafos apareceu em `textos_sem_alvo`; o aviso das duas classes mostrou o atributo como efetivo. |
| 387 · Origem sem sessão | O cliente usa a origem atual para o contato sem sessão. O servidor completa os parâmetros suportados a partir da página. No formulário, verifica origem e correspondência com a página do formulário. `gad_campaignid` continua string. O Core aplica normalização e consentimento de publicidade e identifica a fonte em `cobertura_fonte`. | O clique no link wa.me e o envio do formulário gravaram sessão nula, `gclid=QA1770Google`, `utm_campaign=Campanha QA1770`, `gad_campaignid=770123` e `plataforma=google_ads`. Nos dois ensaios JavaScript o teste fez o rastreador retornar sessão nula e manteve os coletores e endpoints reais. O formulário com JavaScript desativado recuperou os mesmos dados e gravou `pagina_servidor`. Nenhuma conversa de WhatsApp foi enviada. |
| 388 · Primeira pintura | O PHP emite a etapa 2 oculta e com os controles desabilitados. O JS habilita os campos ao revelar o complemento. A validação do envio nativo aceita só a primeira etapa. | A sonda do WP verificou `data-etapa="2" hidden` no HTML de origem. Em Chromium sem JS o complemento estava invisível e o POST nativo persistiu a primeira etapa (HTTP 303). Com JS, a etapa 2 apareceu após o aceite; o complemento respondeu HTTP 200 e a releitura confirmou o texto no mesmo registro. |

## 4. Instalação, testes e documentação

- O WordPress 7.1.4 com PHP 8.3.6 e MySQL 8.0.46 executou a instalação limpa e a troca da versão anterior. Em cada fase passaram 29 verificações dos pedidos novos e 69 de regressão dos pedidos 383–385. A migração preservou as 993 amostras sintéticas e a configuração por comparação de hash. As duas fases também passaram pelos testes de desinstalação e reativação previstos pelo projeto.
- A compilação com Terser 5.44.1 reproduziu 84 JavaScripts e o catálogo PHP byte por byte. O lint com PHP 8.3.6 passou nos 597 arquivos PHP do instalador. O ZIP contém 947 arquivos de runtime. A verificação comparou todos os nomes e todos os hashes com o manifesto do fonte. Nenhum ZIP contém outro ZIP.
- No Site-Teste, WordPress 7.1.4 e PHP 8.3.36 receberam o instalador fechado pelo transporte privado em 17 partes. O servidor verificou o hash final. `plugins/upload-base64` conferiu `expected_slug` e `expected_sha256` na operação `bb21d43f92f423e5640eb1b4c94c9be4`. O recibo confirmou 1.76.0 → 1.77.0, ativo antes e depois. As sondas do MCP passaram antes e depois e o ciclo do Core terminou. A verificação posterior confirmou os cabeçalhos na resposta pública do cache.
- O índice MCP anunciou os dois guias da 1.77.0. A leitura integral de `docs/RELEASE-1.77.0.md` e `docs/AGENTES-1.77.0.md` retornou os mesmos SHA-256 dos arquivos do instalador. A resposta de `f3base/como-usar` descreveu a classe e a precedência. No código do painel foram conferidos o título Fator3 Site Core, o menu Site Core e a verificação de capacidade administrativa.
- Após a homologação, foram eliminados os três contatos sintéticos, a página, o usuário editor temporário e o arquivo PHP da bancada. O staging do ZIP estava ausente. A última sonda recebeu 200 na página inicial e na raiz REST e 404 na rota temporária. Os históricos operacionais de teste, de exclusão e de backup seguem a retenção do ambiente.

## 5. Dados, configuração e recuperação

A release não cria tabela nem exige nova opção, segredo, permissão ou integração. A nova informação de origem vale para novas capturas. Parâmetros de anúncios de registros antigos não são recompostos. Uma correção posterior à implantação segue por nova versão do pacote. A restauração operacional dos dados segue o backup do site.

## 6. Pendências e responsáveis

**Frota e equipe Korvena — pedido 388.** Após a implantação em produção, rodar três medições PageSpeed Insights em desktop na página `/software-sob-medida-meta-1/` e verificar se a mediana do CLS é zero. A rodada comprovou o HTML e os dois fluxos do formulário no Site-Teste. Não foi feita alteração em produção nem medição de PSI em Korvena. Os aceites de produção dos pedidos anteriores, registrados na pendência 143 da frota, seguem com seus responsáveis.

**Equipe editorial Korvena — pedido 386.** Com o pacote implantado, declarar as classes dos grupos de conteúdo planejados em `/software-sob-medida-meta-1/` e `/mvp/`. O aceite técnico do Core para o recurso foi concluído no Site-Teste.

## 7. Credenciais e acesso

A instalação exige o perfil WordPress/MCP com autorização para substituir e ativar o Core. A leitura de contatos e a auditoria mantêm os controles existentes. O fonte, o instalador e as evidências desta rodada não incluem a credencial temporária de homologação.

## 8. Identidade dos arquivos

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| base-site-core-fator3-1.77.0-instalador.zip | 4390364 | `428b7dbfb2c8c0b9a072559c9295a49bec4a7619fbb490eead97aeee60ffb1f5` |
| base-site-core-fator3-1.77.0-fonte.zip | 18684479 | `4c8c167b2a668c68b9074ffbded56fd01ee340f19be813c2712cb72df4a2fbdd` |

O instalador reproduzido a partir do ZIP do fonte tem o SHA-256 da tabela. A cópia de relatório no fonte antecede seu fechamento. Checklist da seção 14 conferido. A única pendência de aceite dos pedidos desta versão é a medição de CLS em produção.
