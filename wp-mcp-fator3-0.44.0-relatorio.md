# Entrega — Fator3 MCP 0.44.0

Revisão 1 · 10/11/2026 (Brasília) · Implementação do plano da 0.44.0 e homologação no Site-Teste · **apta-no-escopo-testado**.

## 1. De onde a versão entra

Instalação limpa ou atualização direta da 0.43.0. A base veio do instalador oficial de 940.636 bytes, SHA-256 `c0f3a10ad4275dc51abd4ab01ac9d2647914fb13d214b9e4f460cd989ddf4951`. A leitura anterior no Site-Teste confirmou 0.43.0 e saúde positiva. As normas aplicadas foram `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambas na revisão 5 de 02/11/2026.

Mínimos declarados no pacote: WordPress 7.1.4 e PHP 8.3. Bancada executada com WordPress 7.1.4, PHP 8.3.6 e MySQL 8.0.46. O Site-Teste informou WordPress 7.1.4 e PHP 8.3.36. O incremento é de 0.43.0 para 0.44.0. O schema de dados permanece em 2.

## 2. Convivência e impactos recebidos

| Componente | Versão ativa na matriz | Prova |
|---|---:|---|
| Core Fator3 | 1.78.0 | Registro dos provedores na instalação integrada e inventário compartilhado |
| Google | 0.31.0 | 7 verificações das bridges, incluindo equivalência entre JSON textual e estruturado e simulação sem mudança de revisão |
| Meta | 0.21.0 | Ativação conjunta e registro do provedor |
| LinkedIn | 0.20.0 | 35 verificações da suíte do emissor, com credenciais e fronteira HTTP sintéticas |
| Pipedrive | 0.9.0 | 59 verificações integradas, 22 de política e 28 de recuperação |

Os dois documentos de impacto estão na revisão 2 e encerram a ação nos emissores. No LinkedIn, as projeções públicas de modo de entrada, preservação de segredo em branco, resultado da renovação, verificação de acesso e prazo de aviso atravessam o transporte com os tipos esperados. O valor de uma credencial continua sujeito à redação. No Pipedrive, o catálogo contém 22 operações, 11 de leitura e 11 de escrita. `pendencias-ler` é leitura. `recuperacao-previa` e `recuperacao-confirmar` exigem autorização de escrita. Não há ordem adicional de troca nesta matriz. Os hashes dos instaladores e dos impactos recebidos estão em `docs/ENTRADAS-TESTE.json` e `evidencias/0440/fontes-da-rodada.json`.

Os contratos de integração de servidor, executores, distribuição e auditoria permanecem na revisão 1.0.0. O instalador desta entrega atualiza apenas o MCP. A avaliação encontrou compatibilidade nos cenários exercitados e dispensou um novo documento para os mantenedores dos acompanhantes.

## 3. Mudanças e respectiva evidência

As referências P44 são as do plano fornecido. A rodada não recebeu novos números oficiais. A regressão do atalho **Notas desta versão** continua vinculada a **Pedidos MCP 79**. Duas decisões posteriores do dono foram aplicadas: retirar P44-S1 e manter a descoberta integral por padrão dentro de P44-A2.

| Item | Resultado e teste |
|---|---|
| P44-S1, decisão do dono | Senhas novas e antigas continuam nativas do WordPress. Uma senha emitida pelo painel com perfil MCP Leitura criou um rascunho via REST (201). A política XML-RPC da bancada recusou igualmente as duas origens de senha (403). |
| P44-S2, S3 | Traduções e documentação compiladas em PHP. GET anônimo aos antigos Markdown e catálogos JSON retorna 404; o cliente autenticado lê o guia. O build recusa diretórios de desenvolvimento e os antigos catálogos, mesmo introduzidos no manifesto. |
| P44-A1, A2, A3 | Omitir `readonly` inclui leitura e escrita. A chamada sem argumentos retornou os 845 alvos sintéticos em 327.752 bytes. `summary:true` ocupou 688 bytes. A projeção de três campos usou 66.063 bytes (27% do compacto). `per_page` e `cursor` continuam explícitos. |
| P44-A4, A5, A6, A7 | JSON textual conserva acentos e barras. Temas do manual têm continuação por cursor. As instruções de inicialização orientam o primeiro acesso. As quatro metatools saíram do catálogo de alvos executáveis, e as habilidades nativas `core/*` mostram o provedor. |
| P44-A8 | Descrição nos 770 parâmetros das 167 habilidades próprias, com 91 saídas específicas. Cada saída foi confrontada com uma resposta efetiva: 70 tiveram pelo menos um sucesso, 21 somente recusas ou erros de domínio esperados na bancada. Os 167 nomes e seus parâmetros publicados foram conservados. |
| P44-A9 | A varredura de 1.025 literais identificou dez mensagens em inglês no OAuth e zero fora do OAuth. Os 132 pares de arquivo e código das mensagens traduzidas permanecem. |
| P44-G1, G2 | A janela retém os 100 incidentes não resolvidos mais recentes; os já resolvidos contam no resumo de 24 horas. A migração conserva a contagem anterior de excedentes em recibo. `system/health` devolve detalhes quando solicitados com `fields:["cron"]`. |
| P44-G3 | O teto se aplica por conexão. Na sessão de teste, 33 inicializações retornaram HTTP 200; a primeira sessão retornou 404, e a segunda credencial manteve sua sessão. Ensaios cobriram concorrência, rebaixamento de teto, legado e reversão após falha de banco. |
| P44-T1, T2 | As sete abas horizontais abrem pela Visão geral. Indicadores, endereço e avisos usam o estado do WordPress. As rotas de Planos e Fonte de manifesto continuam acessíveis pelos endereços antigos. |
| P44-T3, T4, T5 | Um formulário grava acesso ao canal, escrita SQL e MiB sob uma revisão. Um veto a uma das três opções reverteu o conjunto. A prévia de limpeza permanece no painel. Atividade mostra cliente e ação e permite filtrar. O Diagnóstico reúne a sonda privada e o manifesto. |
| P44-T6, T7, T8 | Ajuda abre pelo índice, com Markdown escapado e paginação por seção. O perfil personalizado agrupa as habilidades e filtra as selecionadas sem perdê-las ao salvar. A tela de emissão aplica `no-store` e limpa a senha ao sair. Horários do painel seguem o fuso do site. |
| P44-DOC1, DOC2, DOC3, DOC4 | Índice por tarefa, guias de administração e agentes, versão derivada do pacote, histórico separado e metadados de cada documento. A leitura em sessão nova reconstruiu o histórico de 100.636 bytes em 13 páginas com SHA-256 válido. |
| P44-DOC5, DOC6, DOC7 | A porta documental passou em 192 verificações e protege o build. O manual descreve as duas preferências de exclusão, verificadas pelo fluxo nativo do WordPress. O catálogo compilado redundante foi removido. |
| Pedidos MCP 79 | O atalho na Ajuda aponta para `release-0440`; o teste compartilha a versão de referência de `system/health`. |
| Regressões detectadas nesta rodada | Concessões OAuth antigas sem data, `rewrite/flush` sem regras e validação de planos salvos na 0.43.0. Dois planos reais da versão anterior concluíram na nova. Uma divergência real do contrato continuou impedindo a execução. |

O texto do cabeçalho passa a indicar **Configuração em Ferramentas → Fator3 MCP**. A ação administrativa de arquivos e banco controla o canal correspondente. A redação foi alterada na distribuição deste plugin; a manutenção da aba central permanece a cargo de Site Geral | Todos.

## 4. Instalação e prova de prontidão

No wp-admin, instale o ZIP pela tela de plugins. No serviço MCP, use `plugins/upload-base64` com `zip_path`, `expected_slug:wp-mcp-fator3`, `expected_sha256`, `overwrite:true` e `activate:true` para substituir uma instalação ativa. O Site-Teste recebeu quatro partes. O servidor conferiu o total e o SHA-256 antes da operação `49d662ed89013082c70217203c101743`, com pré-imagem `52a54db7bd693f31ad5a0170`. Versão observada antes e depois: **0.43.0 → 0.44.0**.

A leitura independente de `system/health` com `compact:true` confirmou `healthy:true` e versão **0.44.0**, requisição `b5ff4ea84278f84a3e38e313`. A sonda recebeu HTTP 404 nos cinco caminhos públicos testados. O MCP leu as notas completas da 0.44.0 e confirmou seu SHA-256. Sem argumentos, a descoberta devolveu as 844 habilidades visíveis à conexão do Site-Teste, com `has_more:false`. As sete telas responderam com a aba, o título e a versão corretos. O atalho de notas abriu e renderizou o documento atual. As verificações do ambiente compartilhado, a remoção dos arquivos temporários e os recibos estão em `evidencias/0440/site-teste.json`. A atividade gerada pelo ensaio segue a política normal de auditoria. O Site-Teste confirmou os quatro campos LinkedIn observáveis sem conta cadastrada e a recusa `operacao_nao_autorizada` da leitura Pipedrive sem autorização comercial. O quinto campo LinkedIn, o prazo de aviso, foi exercitado com conta sintética na bancada. O pacote não foi publicado no canal de distribuição da frota.

O ZIP de laboratório foi conferido byte a byte na instalação limpa e na migração integrada. A porta de distribuição conferiu 467 arquivos PHP, 474 membros e build reproduzível. O JavaScript passou na verificação de sintaxe. A interface passou em 25 verificações do painel PHP e 51 no Chromium em 1.365 e 390 px, com nove linhas completas de atividade na primeira dobra do desktop. As capturas acompanham o fonte. Para repetir os ensaios, veja `tools/release0440/` e as instruções de documentação e matriz nesse diretório.

## 5. Banco, migração e recuperação

A instalação mantém 11 tabelas próprias no schema 2. A migração direta foi exercitada com a mesma credencial nativa, perfil personalizado, revisão, limite de 5 MiB, critérios de retenção, backup anterior legível e incidentes de cron semeados antes da troca. A atualização preserva planos e backups. A migração do histórico de cron é repetível. Ao atingir o teto, uma nova sessão substitui a menos recente da sua própria conexão.

Desativar remove o marcador agendado. Excluir pelo WordPress preserva os dados por padrão. Em site individual, a preferência de exclusão em Diagnóstico permite apagar o acervo privado, tabelas e opções próprias, simulações e trabalhos pendentes do MCP. Itens de outros plugins e senhas nativas do WordPress são preservados. Esse fluxo destrutivo foi testado somente em cópias descartáveis. Antes de optar pela remoção, conserve fora do diretório privado os backups necessários e revogue no WordPress as senhas que deseja encerrar.

Após uma falha de instalação, consulte o estado da operação e da pré-imagem antes de repetir. A 0.44.0 distribuída é imutável. Se for necessária uma correção do executável, emita nova versão com a migração de avanço pertinente.

## 6. Limites de validação

- APIs comerciais de LinkedIn, Pipedrive e Google: as suítes usam dados sintéticos ou operações locais. A utilização comercial de uma conta real depende das credenciais, dos ativos e do consentimento do dono dessa conta.
- Implantador: o pacote vigente não foi fornecido para ensaio. A publicação e a implantação nos sites da frota ficam com o responsável pela distribuição.
- Interface: Chromium local em duas larguras e comprovação HTTP das telas compartilhadas. O texto da aba de governança do pacote permanece sob responsabilidade de Site Geral | Todos.
- Contratos de saída: a amostra de cada uma das 21 habilidades exercitadas apenas em falha cobre o código de domínio observado. A comprovação de todos os seus caminhos de sucesso requer os recursos que cada operação administra.
- Multisite: a limpeza destrutiva opcional está desabilitada. A matriz de instalação e exclusão usa sites individuais. A bancada não mediu acesso XML-RPC liberado por um site que permita esse método.

## 7. Credenciais

Em Ferramentas → Fator3 MCP → Clientes, selecione conta WordPress, nome e perfil do cliente. Para senha de aplicação, copie-a no ato da emissão e configure usuário e senha no cliente. Para OAuth, use o fluxo de autorização, recurso e identidade correspondentes ao site. O perfil do cliente limita as chamadas MCP. Em outras interfaces WordPress valem as capacidades da conta e a política do site. A atualização não exige reemitir as senhas existentes. Nenhum valor de credencial integra o relatório ou as evidências.

## 8. Identidade dos arquivos

Revisão canônica após o fechamento do fonte. A cópia interna antecede o cálculo da identidade do próprio ZIP.

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-fator3-0.44.0-instalador.zip | 935339 | `a90aa7f2e91ef1033a4a8c6ec320b1e10b45ef657132a40f8aa4215ffa55d5eb` |
| wp-mcp-fator3-0.44.0-fonte.zip | 4444369 | `d29b885a45c5b266d1b24f7b650d86e44b2849437bdac073f582223dc188e565` |

Relatório externo canônico: `wp-mcp-fator3-0.44.0-relatorio.md`. Arquivos da entrega: [instalador](wp-mcp-fator3-0.44.0-instalador.zip) e [fonte](wp-mcp-fator3-0.44.0-fonte.zip).
