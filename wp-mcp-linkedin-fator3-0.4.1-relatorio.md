# Entrega — Fator3 MCP LinkedIn 0.4.1

Data: 21/10/2026. Relatório externo final. A cópia interna no fonte é identificada como anterior ao fechamento; somente este relatório externo contém tamanho e SHA-256 finais do fonte.

## 1. Bases aceitas

Base recebida: **0.3.0**. Pedidos: **LinkedIn 4**, conforme aba recebida de 20/21 de outubro. Instruções comuns e padrão de desenvolvimento, revisão 4 de 16/10/2026, aplicados. A 0.4.0 foi marco intermediário instalado somente no Site-Teste nesta rodada. A revisão visual encontrou rótulos de diagnóstico em inglês; a entrega final é **0.4.1**, por instrução explícita do dono: mais de uma versão no mesmo ciclo incrementa o **patch**. O candidato local 0.5.0 não foi instalado nem publicado. ZIPs anteriores não foram renomeados nem regravados.

Identidade preservada: `wp-mcp-linkedin-fator3`, basename `wp-mcp-linkedin-fator3/wp-mcp-linkedin-fator3.php`, namespace `Fator3\LinkedIn`, prefixo público `linkedin/`, Text Domain e Update URI existentes. Cabeçalho mantém autor Fator3, licença GPL-2.0-or-later, descrição específica e mínimos comprovados WordPress 6.4 / PHP 8.1.2 de 64 bits.

| Base própria | Bytes | SHA-256 |
| --- | ---: | --- |
| `wp-mcp-linkedin-fator3-0.3.0-fonte.zip` | 228685 | `a7e104ec20bd238e9227546acd888895562a95c452394dd633e52e1e3ae54d18` |
| `wp-mcp-linkedin-fator3-0.3.0-instalador.zip` | 79465 | `b6d20998379236baf46ac5ae0181646e8a15fb75bbb4f37a88a68be01d2d768a` |

| Acompanhante recebido | Bytes | SHA-256 |
| --- | ---: | --- |
| `base-site-core-fator3-1.43.0-instalador.zip` | 2091980 | `5a7c02abb97f7161617ddfd8e4d28faf2fdb22e4ae5d4ed75416dc68d76ee9e7` |
| `wp-mcp-fator3-0.24.0-instalador(4).zip` | 821425 | `e2c78fcf0e99da55237808bc51fe408405e367fd76a71172b497707996f8aa95` |
| `wp-mcp-google-fator3-0.16.0-instalador(1).zip` | 756123 | `e0dfee63fbd9ad9fcc6b5ab9a3b9d492d7e497822154e0572589a45f3116248c` |

Fontes e relatórios dos três acompanhantes foram considerados; o inventário completo de insumos e hashes está em `evidence/inputs.json`. A descrição introdutória histórica dos pedidos não substitui as versões atuais recebidas.

## 2. Convivência e encaminhamentos

Core **1.43.0**, MCP **0.24.0**, Google **0.16.0**, Meta **0.4.1** e LinkedIn **0.4.1** coexistem ativos no Site-Teste. Nenhum arquivo dos três acompanhantes foi alterado. Foram avaliados identidade, registro de providers/abilities, transporte MCP, autorização, SDK, tabelas/options e carregamento da administração.

Nenhum impacto técnico novo que exija mudança em outro plugin foi identificado; **zero arquivos de impacto** emitidos. `admin-options` e os campos opcionais `label`/`next_at` de agendas são aditivos. SDK LinkedIn 1.0/1.1, grants, ownership, callbacks e assinatura criptográfica permanecem compatíveis. Core conserva medição, consentimento, contatos e pipeline comercial. Google conserva suas APIs; MCP continua responsável pelo transporte. Meta Ads não foi incorporado ao pacote Meta.

Instalação em ordem serial no ambiente compartilhado: Meta e depois LinkedIn, conferindo o primeiro antes de iniciar o segundo. Laboratório também cobriu acompanhantes antes dos sociais, sociais antes dos acompanhantes, ordem LinkedIn primeiro e cada plugin isolado. Implantador não fornecido: **não avaliado**, sem consequência concreta identificada para encaminhar.

## 3. Mudanças por pedido e evidência

| Pedido | Implementação | Evidência e limite |
| --- | --- | --- |
| LinkedIn 4 — navegação e abertura | Abas Conexão, Ativos, Coletas, Relatórios, Formulários e concessões, Diagnóstico e Ajuda; URLs próprias e pílulas; configuração local e carga por seção. | DOM/REST e navegador do Site-Teste; reload conserva `tab=leads`. |
| LinkedIn 4 — nomes | Usuários WordPress por nome, organizações/contas por metadados, campanhas por lista e formulários pelo nome da conta autorizada. Descoberta de contas em páginas de 10. | Busca/paginação, falha do fornecedor, preservação de seleção, proprietário de formulário e revisão concorrente verificados. |
| LinkedIn 4 — formulário sem JSON | Concessões por consumidor, conta/formulário e permissões; diário de assinaturas próprias; relatórios e agendas com campos próprios e datas/horas. | Configuração e concessão persistidas por REST real no laboratório; nenhum editor JSON no painel. |
| LinkedIn 4 — português | Pivôs Conta, Grupo de campanhas, Campanha, Anúncio e dimensões de público; métricas, estados e rótulos em português; API em seção avançada. | Pivôs e campos conferidos no navegador 0.4.1. Dados livres de nomes/conteúdo do fornecedor não são traduzidos. |
| Revisão 0.4.1 | Tradução dos diagnósticos, preservando códigos dos contratos; usuário e revisão novamente conferidos no servidor. | Autotestes, DOM e regressões de autorização. |

Agendas antigas continuam válidas sem nome; a edição mantém instante exato de `next_at` quando não alterado e preserva último job/código. Salvar apenas configuração preserva tokens, ativos e formulários já selecionados. Descoberta falha ou parcial não apaga seleção. Dados técnicos dos contratos não são renomeados por tradução de tela.

### Matriz executada sobre os ZIPs finais 0.4.1

| Cenário | WordPress / PHP | Verificações nativas | Resultado |
| --- | --- | ---: | --- |
| Limpo, trio antes dos sociais | 7.1.3 / 8.3.6 | 81 | 0 falhas |
| Atualização direta 0.3.0, sociais antes do trio | 7.1.3 / 8.3.6 | 84 | 0 falhas |
| Atualização 0.4.0, trio antes dos sociais | 7.1.3 / 8.3.6 | 84 | 0 falhas |
| Mínimo, LinkedIn antes do Meta, sem acompanhantes ativos | 6.4 / 8.1.2 | 79 | 0 falhas |
| Meta isolado | 7.1.3 / 8.3.6 | 48 | 0 falhas |
| LinkedIn isolado | 7.1.3 / 8.3.6 | 31 | 0 falhas |

Total **407 execuções de verificações** nos seis cenários, e não 407 testes distintos. O cenário isolado deste pacote tem 31 verificações. Mais **20 fluxos DOM** dos dois plugins passaram usando HTML/JS servido pelo WordPress e REST autenticada real, com jsdom 27.4.0. Foram verificados configuração, nomes, seleção explícita, falha externa, consultas, agendas, concessões, autoteste e ajuda. PHP lint integra o build. MySQL 8.0.46 real, ambientes descartáveis; HTTP de fornecedores controlado por fixtures e SMTP bloqueado.

As provas estão em `evidence/matrix.json`, diretórios de cada cenário, `clean-ui/ui-dom-tests.json`, `site-browser.json` e `site-installation.json`. A pasta `history-040/` contém provas históricas da versão intermediária, separadas das atuais. O Chrome local não iniciou por restrição de socket; a revisão visual foi realizada no navegador do Site-Teste. DOM não foi tratado como prova visual, e fixtures não foram tratadas como acesso real a fornecedor.

Documentação MCP final: **13 documentos deste pacote, 18 páginas**, lidos integralmente por `linkedin/documentation`, continuando com `next_offset` e `expected_revision`. Conteúdo reconstruído, tamanho e SHA-256 coincidem com os arquivos do instalador. Conjunto da entrega: 28 documentos / 37 páginas. Inclui administração, configuração, contratos/schemas, guia de agentes, SDK, operação, segurança, migração e notas da versão. Leitura local não exige fornecedor nem modifica estado. Evidência: `evidence/site-documentation.json`.

## 4. Instalação e prontidão

Instalador final aplicado em `https://fator3-teste-mcp-1.dreamhosters.com/` via WP MCP fator3-teste, com `expected_sha256`, `expected_slug`, backup e uma operação por vez. Estado anterior desta revisão: **0.4.0 ativo**; estado final: **0.4.1 ativo**, operação `complete`, arquivo candidato verificado, SHA igual ao da seção 8.

- Operação do pacote: `8064ad0e174931357cfcb979a13c3184`.
- Backup da pré-imagem 0.4.0: `265fc1a4dbd88ea1710c5d46`.
- Sondas da home e `/wp-json/`: HTTP 200 antes e depois.
- Reativação silenciosa em requisição PHP nova; `activation_hook_cycle_completed=false`. Ativação limpa completa foi exercitada no laboratório.
- Autoteste: 8 verificações locais aprovadas; armazenamento e criptografia prontos; zero conexões antes/depois da revisão.
- `business_readiness_verified=false` e `remote_homologated=false`: instalação validada não é homologação comercial ou do fornecedor.

Para atualizar outro ambiente, fazer backup de arquivos e banco, verificar SHA-256 e substituir a pasta estável pelo **instalador**; não usar o fonte na tela de plugins nem executar uninstall. Preservar salts e credenciais. Conferir versão, autoteste, configuração, seleção autorizada e uma consulta permitida. A publicação e atualização dos demais sites ficam com o dono/frota; não houve push, publicação no repositório ou implantação em produção nesta rodada.

## 5. Banco e reversão

Sem alteração de schema ou formato de cifra nesta versão. Conexões cifradas, grants, agendas, jobs e resultados existentes são preservados. Atualizações de 0.3.0 e 0.4.0 foram verificadas no laboratório, incluindo ciphertext e dados existentes; agendas recebem somente campos opcionais compatíveis. Banco compartilhado não foi apagado nem substituído.

Reversão de arquivos usa pré-imagem compatível, seguida de conferência de versão, configuração e cron. Isso **não** restaura banco, desfaz coletas, callbacks ou efeitos externos. O instalador declara `database_effects_reversible=false`. Para recuperação completa, usar backup coordenado de arquivos/banco/salts. Não foi executado rollback no site compartilhado. A versão anterior não oferece a nova edição de nomes/horários, embora os dados sejam preservados. Cron depende de tráfego ou disparo do servidor; site sem agendas pode mostrar próximo worker nulo.

## 6. Pendências e responsáveis

| Pendência | Responsável | Critério de continuidade |
| --- | --- | --- |
| Aplicativo, acesso às Páginas e Lead Sync reais | Dono da conta/LinkedIn e frota | Bloqueio de aplicativo/administração informado nos pedidos (pendência 92, A-LI-1610). Aprovar produtos e permissões e selecionar ativos autorizados antes da homologação. |
| Fluxos reais e aceite de produção | Dono/frota | Listas, analytics, webhook, desafio e notificação reais não exercitados; homologação da frota/pendência 20 continua externa. Nenhuma assinatura real foi criada. |
| Descoberta do cliente externo no Core 249 | Responsável Core | O consumidor recebido já existe no Core 1.43.0; a lacuna de descoberta do cliente externo não é corrigida por este painel. Não declarar conclusão de trabalho do Core. |
| Aceite final das melhorias visuais e retirada dos itens na aba central | Dono/revisor | Conferir esta entrega e suas evidências; a aba central não foi alterada pelo agente do pacote. |
| Demais sites da frota | Dono/frota | Publicação e implantação após decisão do dono, usando hashes finais. |
| Implantador | Responsável pelo pacote | Não avaliado por falta de base nesta rodada; não há mudança de contrato exigida por esta entrega. |

O site autorizado está sem conexões sociais, portanto nomes e relatórios reais de fornecedores não foram homologados nele. Não foram copiados tokens de produção, criados leads, gastos de Ads, publicações ou assinaturas reais. Limites registrados em `evidence/test-boundaries.json`.

## 7. Credenciais e configuração

Token manual e dados do aplicativo conforme o produto. Pages, Ads e Lead Sync exigem as respectivas aprovações e permissões, papéis administrativos e seleção explícita de organizações, contas e formulários. Versão padrão preservada `202609`, alteração apenas avançada. Concessões ao consumidor são explícitas; ele mantém recepção/deduplicação/ingestão. Não configurar callback ou assinatura de terceiro sem autorização própria.

Entradas humanas de configuração e dados exigem `manage_options`, inclusive REST/MCP; a lista de usuários associados não concede administração. Nonce no painel, checagem no servidor e revisão otimista da conexão preservados. Segredos permanecem cifrados e nunca retornam na projeção pública. Campos de token/chave vazios preservam o segredo; remoção é explícita. Nenhum valor de credencial, cookie, banco, sessão ou nome pessoal do navegador acompanha os artefatos.

## 8. Arquivos finais, bytes e SHA-256

| Arquivo | Bytes | SHA-256 |
| --- | ---: | --- |
| `wp-mcp-linkedin-fator3-0.4.1-instalador.zip` | 102166 | `a1f2bd2393c7f1b1780f106f4a7c3ac46776a8a7cc7071f1e269daad7ec34c43` |
| `wp-mcp-linkedin-fator3-0.4.1-fonte.zip` | 289465 | `059a201660863eef69e6dccffce9c67ac96cd580bf88bf3cea31ba712b2b21ff` |

Relatório externo: `wp-mcp-linkedin-fator3-0.4.1-relatorio.md`. Instalador com raiz `wp-mcp-linkedin-fator3/`; fonte com raiz `wp-mcp-linkedin-fator3-0.4.1-fonte/`, runtime em `plugin/wp-mcp-linkedin-fator3/`, build reproduzível, testes, documentação, planejamento, evidências sanitizadas e esta cópia de relatório anterior ao fechamento. **Nenhum ZIP contém outro ZIP da entrega.**

O fonte foi preparado com build próprio do provedor; reconstrução reproduziu byte a byte o instalador final. `README.md` descreve dependências fixadas, execução isolada e composição da matriz conjunta. `evidence/reproducible-build.json` registra a conferência. O fonte é fechado uma única vez; seu hash final consta exclusivamente no relatório externo.
