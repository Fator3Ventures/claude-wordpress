# Entrega — Fator3 MCP LinkedIn 0.24.0

Revisão 1 · 14/11/2026, horário de Brasília · Pedidos MCP LinkedIn 26 · **apta-no-escopo-testado**. Versão corrente no Site-Teste; distribuição na frota a cargo do dono.

## 1. De onde esta versão entra

Instalação limpa ou atualização direta da **0.23.0**. O instalador-base tem 448442 bytes, SHA-256 `7f4b6d131081169894fe73f550aa317305e60d2b64ee5aaf7ca02735dd6fc201`; o fonte-base, 3846008 bytes, SHA-256 `7bbd20a3dc765eb8f551ec9e286eb4c3cbfe9566927da8eefe51af22ff18e8b1`. O pacote exige WordPress ≥ 7.1.4 e PHP ≥ 8.3 de 64 bits. Laboratório: WordPress 7.1.4, PHP 8.3.6, MariaDB 11.8.6 e Chromium Headless Shell 150.0.7871.181.

Referências lidas: `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos rev. 5 de 02/11/2026; Regra comum, inclusive a diretriz visual de 14/11; aba Fator3 MCP LinkedIn, sem número próprio de revisão; Pedido 26; última entrega LinkedIn; relatório e pacotes oficiais do Core 1.87.3. As cópias da Regra comum e do padrão LinkedIn anexadas são iguais às das fontes do projeto. O histórico da frota de 09/11 na aba é referência histórica.

## 2. Convivência e escopo

| Pacote | Versão | SHA-256 do instalador exercitado |
|---|---|---|
| Fator3 Site Core | 1.87.3 | `d8f8c05aa3220e5dea01723211718932ca54b13e644d70cdb95dc51ccc760fed` |
| Fator3 MCP | 0.45.0 | `3659bebf22155807d12f4559cf3d9e7ef7403aec0da45fc661ad90c577c7eab9` |
| Fator3 MCP Google | 0.35.0 | `c1fdf87b53e197fca8aa9f93816e1047b065283a3edfca3c44b4c2b16484045a` |
| Fator3 MCP Meta | 0.26.0 | `f1b2fc7b10dd7824c63cd4d67221d32e2b50eb2136d774dc589078d706e8a0a7` |
| Fator3 MCP Pipedrive | 0.10.0 | `7d021e6117c3dd10d8b64059fefced863736ecf90f30e89942e6e32b4569ceb4` |

A troca é exclusiva do LinkedIn e dispensa ordem especial entre acompanhantes. O plugin conserva leituras de Pages, Ads e Lead Sync, administração das conexões e concessões, coletas, exportação, operações de anúncios/publicações com prévia e envio de conversões autorizado. Seleção do cliente em `f3base_anuncios_linkedin`, consentimento, contatos, deduplicação e pipeline permanecem no Site Core. O MCP provê o transporte e a autorização próprios. Conferidos os cabeçalhos, os hashes do Core e a igualdade do adaptador LinkedIn entre seu instalador e o runtime do fonte. Os três schemas JSON publicados e as 100 operações LinkedIn conservam o contrato. Nenhum encaminhamento técnico novo: não houve mudança de código ou documento oficial de Core, MCP ou outros pacotes.

## 3. Mudanças por pedido e evidência

**Pedidos MCP LinkedIn 26.** No relato da frota, Estado e Token quebravam no meio a 750 px. Na reprodução independente com 56 conexões sintéticas na 0.23.0, ambos ocuparam duas linhas a 360 px; a 750 px permaneceram em uma linha, sem rolagem horizontal própria. A navegação móvel escondia destinos à direita. No candidato final, a 360, 750 e 768 px, os dois cabeçalhos ficaram em uma linha e a tabela rolou dentro da própria região, inclusive pelo teclado. A página e a navegação ficaram dentro da largura disponível.

| Item da Regra comum | Conferência e ajuste |
|---|---|
| 1. Cabeçalho | Título existente, resumo em português e selo de versão à direita. |
| 2. Dois níveis de navegação | Seis grupos em pílulas; subabas sublinhadas nos grupos com mais de um destino. As linhas quebram e os destinos ficam acessíveis. Testados os 12 endereços diretos e os fragmentos antigos das concessões de conversões. |
| 3. Cartões e ações | Títulos e instruções nos cartões. Relatórios e Coletas ganharam orientação antes do formulário. Cadastro, consulta de diagnóstico e leitura de ajuda têm ação principal distinguível. Ações de confirmação mantêm prévias e guardas existentes. |
| 4. Estados | Conexão ativa/pausada, token salvo/ausente, coletas, agendas e diagnóstico usam texto e cor; retornos da concessão distinguem informação, confirmação, atenção e erro. Um token salvo não indica validação remota. |
| 5. Formulários | Rótulos acima dos campos de valor; grupos de seleção mantêm rótulos associados. Em tela estreita a grade cai para uma coluna. Opções de renovação, versão da API e manutenção permanecem recolhíveis. |
| 6. Listas e tabelas | Busca e paginação na lista completa de conexões; filtros sem distinção de acento e páginas de 20 nos resultados carregados, referência de campos, agendas, coletas, concessões e seleções de ativos. O total indica o conjunto carregado quando a origem externa ainda tem mais páginas. Os comandos de continuação remota foram preservados. Enter no filtro não envia o formulário. |
| 7. Português | Orientações, totais, selos e controles de busca e página em português. Nomes oficiais do fornecedor, escopos e identificadores técnicos continuam literais. |
| 8. Larguras e leitura | 12 abas × 3 larguras, mais imagens do editor, da rolagem e da comparação. Sem transbordamento de página nas telas verificadas. |

A implementação está nos assets administrativos, no template de administração e na referência de campos. Não há novo script na página pública nem nova chamada ao fornecedor para filtrar ou paginar resultados já carregados. Não foram alterados slug, basename, `manage_options`, rotas REST/MCP, contrato `linkedin/save-connection`, tabelas ou opções. O guia atualizado está em `docs/ADMINISTRATION.md`, além das notas correntes e guia de migração.

## 4. Instalação, prontidão e testes

No [Site-Teste](https://fator3-teste-mcp-1.dreamhosters.com/), `plugins/upload-base64` recebeu o ZIP com `expected_slug=wp-mcp-linkedin-fator3`, SHA da seção 8, sobrescrita e ativação. A homologação usou os bytes locais conferidos. Operação `ba78238bc83461572016e351c9c64ee8`; cópia de segurança de arquivos `f9b70ad65c76d9590c161488`. Versão ativa **0.23.0 → 0.24.0**. `linkedin/status {}`: `ok`, 0 conexões ao encerrar. `system/health`: saudável. `linkedin/selftest`: 9/9 aprovadas verificações locais. Página inicial e REST: HTTP 200 em ambas. O laboratório e o navegador são ambientes descartáveis; nenhuma conexão, retorno de fornecedor ou usuário sintético foi cadastrado no Site-Teste.

| Grupo | Resultado |
|---|---:|
| Funções próprias, instalação limpa sem acompanhantes | 135/135 |
| Regressão com o conjunto vigente | 141/141 |
| Origem de anúncios e adaptador oficial do Core | 51/51 |
| Conversões de aquisição e etapas comerciais | 25/25 |
| Preservação e migração da base | 8/8 |
| Rotação da concessão e limites de autorização | 17/17 |
| Documentação via MCP: instalação limpa e após atualização | 77/77 + 77/77 |
| **Total nativo** | **531/531** |
| **Navegador: navegação, geometria, teclado, filtros e paginação** | **141/141** |

Nenhum aviso PHP nos logs dos grupos nativos finais. Lint em 38 arquivos PHP e verificação sintática dos quatro scripts administrativos. O teste visual usou WordPress, HTML/CSS e JavaScript do pacote, com tráfego externo bloqueado. Validou busca sem acento, navegação entre páginas de conexões, edição por ID, pesquisa em uma resposta sintética com 41 linhas e ausência de segunda consulta ao paginar os itens locais. As imagens integram o fonte e o complemento `wp-mcp-linkedin-fator3-0.24.0-capturas.zip`. Extraia e abra `capturas/index.html`: as 36 imagens principais estão agrupadas por aba e largura; os quadros adicionais identificam a versão e a situação.

Documentação: as 51 entradas foram lidas integralmente pelo executor MCP em 62 páginas por instalação no laboratório. No Site-Teste, os hashes das 51 entradas do índice foram confrontados com o instalador; guia do painel e notas correntes foram relidos integralmente pelo MCP e comparados byte a byte. Evidências, reprodução e limites em `evidence/release0240/` e no README do fonte.

Para a distribuição, a frota confere os hashes contra a seção 8. A URL prevista após publicação é `https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-linkedin-fator3-0.24.0-instalador.zip`. Antes do primeiro `plugins/upload`, conferir o SHA-256 servido, além do slug. Publicação e troca nos demais sites não foram realizadas nesta rodada.

## 5. Banco, migração e correção por nova versão

Sem alteração de esquema, gravação implícita de configurações ou reprocessamento de fila. Na atualização direta, os dez registros sintéticos conservaram o conteúdo cifrado e as revisões, inclusive o cursor pausado, o agendamento e o recibo de resultado incerto. Filtrar itens no navegador não revoga seleções ocultas. Para conter um incidente, preservar o banco, os sais e os recibos pertinentes e corrigir em versão posterior. Não há downgrade.

## 6. O que permanece pendente

Implantação nos demais sites e aceite final na instalação onde o pedido foi registrado: responsabilidade da frota. A evidência visual provém do Chromium em WordPress de laboratório com dados sintéticos. Safari, Firefox e aparelhos físicos não foram exercitados. A interface não exigiu validar conta real, produto Lead Sync, desafio de webhook, assinatura, recebimento de lead ou conversão real; esses efeitos não foram provocados nem homologados nesta rodada.

## 7. Credenciais e configuração do dono

Nenhuma credencial nova. Em **Ferramentas → Fator3 MCP LinkedIn → Conexões**, o dono insere os valores secretos (token de acesso e, se aplicável, segredo do aplicativo e token de renovação); valores vazios conservam os salvos. O operador preenche nome, ID público do aplicativo e validade, escolhe ativos e formulários, simula e confirma alterações. O fornecedor concede os produtos e escopos; Lead Sync requer o produto aprovado, papéis no ativo, consumidor autorizado e, para notificações, webhook e assinatura verificados. Provas locais de painel não substituem essa confirmação externa.

## 8. Identidade dos arquivos

- **Instalador:** `wp-mcp-linkedin-fator3-0.24.0-instalador.zip` · 452765 bytes · SHA-256 `0836ea7805e16671a5ef33cd0a5152fd6a78e96862f9296616bd5f8d8205dcc9`. Raiz única, 96 arquivos, 95 entradas no manifesto que exclui a si próprio.
- **Fonte:** `wp-mcp-linkedin-fator3-0.24.0-fonte.zip`. 9660303 bytes · SHA-256 `8ec04cc497165b18235948c4eb0187a9829734eab0e50efabdaee8eb5d957ce1`. Relatório externo canônico. A cópia no fonte é anterior ao fechamento.
- **Capturas:** `wp-mcp-linkedin-fator3-0.24.0-capturas.zip` · 5719531 bytes · SHA-256 `fd1c883247db3ef679398507297bdf54d39a2a18f6b4c514a15e555b8194c4a6`. Originais PNG, índice local e manifesto das dimensões e hashes.
