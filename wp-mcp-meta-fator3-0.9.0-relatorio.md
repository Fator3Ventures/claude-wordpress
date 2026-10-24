# Entrega — Fator3 MCP Meta 0.9.0

23/10/2026 · Revisão 1 · Implementação do **Pedido MCP Meta 15**, despacho **D-20261023-50**. Slug: `wp-mcp-meta-fator3`.

**Implementada e ativa no Site-Teste.** Testes funcionais, atualização, mínimos, interface DOM e integração aprovados no escopo abaixo. Homologação com credenciais reais da Meta permanece pendente. Este é o relatório externo canônico; a cópia no fonte antecede o fechamento.

## 1. Bases aceitas

Base direta **0.8.0**: instalador de 153819 bytes, SHA-256 `36e4e098955576c3d43ea1b1bd2c14fe68608472b8666a652e84da5165ce25e1`. Fonte-base de 996667 bytes, SHA-256 `ef929b96e4336c350b0d7f802b082f166051127ab10063ac05f114b669c3ce99`. Os artefatos aceitos não foram alterados.

Considerados o documento `Fator3 MCP Meta(8).md`, que declara o pedido 15 aberto sobre a 0.8.0; as instruções comuns e padrão de desenvolvimento **revisão 5**; o plano anterior ao código; os pacotes, relatórios e impactos recebidos. Não foram criados IDs de pedido nem modificada a aba central.

Core 1.50.0: instalador 2250902 bytes / SHA-256 `7021163d158b1a353e012823e14b611c17cb45d82125d3230784eb84f2b6b8ea`; fonte 4797482 bytes / `6a50e171b5042641f99aaea4a7c46c7b7ace51227450a7ee4cd0c2e564805a18`. Google 0.19.0: instalador 809436 bytes / `d15868915e3fdf886d7e883a82d9d302df7242808fc94d45bf3e1857234759d1`; fonte 4462572 bytes / `0d90b1a0dbc186a9e0b2adf66843dad4abd928fb2c616a56442213597b0eefb2`. CRC e identidade desses ZIPs foram conferidos antes da extração. MCP 0.29.1 e LinkedIn 0.9.0 foram examinados a partir dos pacotes aceitos na rodada anterior.

A versão minor segue a regra do projeto. A instalação não migra ou revalida credenciais existentes automaticamente. A atualização direta comprovada é **0.8.0 → 0.9.0**, sem versão intermediária.

## 2. Convivência e encaminhamentos

| Pacote | Referência examinada / estado final observado | Conferência própria |
|---|---|---|
| Fator3 Site Core | 1.50.0 | 458 arquivos iguais ao instalador recebido; ativação conjunta; credenciais e ingestão comercial continuam próprias do Core |
| Fator3 MCP | 0.29.1 | 463 arquivos iguais ao pacote aceito; política real de concessões, recibo/repetição, redator de segredos, descoberta e leitura documental |
| Fator3 MCP Google | 0.19.0 | 160 arquivos iguais ao instalador recebido; presença conjunta sem alteração do pacote |
| Fator3 MCP LinkedIn | Fonte/instalador examinados: 0.9.0; instalado durante a rodada por outro responsável: 0.10.0 e depois **0.10.1** | Documentação instalada, catálogo e chamada real de capabilities; versão retornada igual à carregada. Não foi feita comparação do ZIP final 0.10.1 |
| Fator3 MCP Meta | 0.9.0 | 43 arquivos iguais ao instalador final desta entrega; fluxos administrativos exercitados no ambiente integrado |

A atualização do LinkedIn não foi feita por esta rodada. Sua referência 0.9.0 tinha instalador SHA-256 `d4857927ebacfca9321b79d13bc15f15c6969ae67047fd1793e509524b7a60f8`; não se atribui esse hash à 0.10.1. O relatório do Core 1.50.0 e a documentação instalada do LinkedIn descrevem validação de credenciais própria em seus domínios. O Meta não chama esses validadores nem modifica concessões ou cursores desses plugins.

**Não foi identificada adaptação obrigatória no LinkedIn, Core, Google ou MCP nas interfaces examinadas.** A nova operação é aditiva e usa a descoberta existente. Não foi emitido relatório de impacto apenas para anunciar a versão, responder ou encerrar pedidos.

Tratamento de impactos recebidos/anteriores, registrado aqui conforme a revisão 5:

- **MCP 0.29.1 → Meta, revisão 2:** mantida a orientação de que `retryable` não comprova ausência de efeito. O teste usa o executor real: falha Meta de efeito incerto conserva recibo e não executa novamente o callback. `health` continua leitura; `status` continua escrita local e é recusado no perfil Leitura.
- **LinkedIn 0.8.1 → Meta, revisão 2, R1/R2:** as correções já aceitas continuam cobertas pelas regressões de ilegibilidade, autorização, isolamento e snapshot. Nenhum novo pedido ao LinkedIn decorreu desta implementação.
- **Meta 0.7.1 → LinkedIn, histórico do pedido 12:** o acompanhamento registrado na base 0.8.0 permanece histórico; não se reemite nem revisa o arquivo para comunicar encerramento. A entrega atual não declara concluído trabalho do mantenedor do LinkedIn.

Um achado de integração foi corrigido **no Meta**: o nome legado `token_identity` acionava o redator do MCP e ocultava também os metadados públicos. A projeção aditiva `connection.identity` mantém nome, app, validade e permissões legíveis. O campo legado permanece; os segredos continuam omitidos e a política do MCP não foi relaxada. O redator original foi exercitado com a saída real do Meta.

## 3. Mudanças por pedido e evidências

| Parte do pedido 15 | Implementação | Prova |
|---|---|---|
| Rótulos e ajuda | Textos literais solicitados, sempre abaixo dos campos, no cadastro/edição e renovação; placeholder do nome; App ID de 15–17 dígitos; App Secret de 32 hexadecimais; token EAA com pelo menos 100 caracteres | Renderização PHP e 19 verificações de interação DOM; ajuda, estados de erro, prévia e confirmação |
| Conferência antes de gravar | Formato local, `debug_token` com o aplicativo informado, identidade por `/me`, validade e leitura de todos os ativos selecionados. Página também precisa permitir derivar sua credencial. Nenhum cache de candidata é salvo | Erro 190, `is_valid=false`, aplicativo divergente, ativo recusado, expiração, resposta incompleta e quota: bytes da configuração/agendas preservados |
| Resumo do que está salvo | Identidade e nome confirmados, app, validade remota, permissões e alerta de escopos além das cinco de leitura. `expires_at` remoto substitui a data digitada | HTTP sintético, renderização, DOM e filtro MCP real. Nome de usuário vem de `/me`; nome do app vem de `debug_token`. Nomes ausentes não são inventados |
| Troca guiada | Nova `meta/switch-identity`, com `dry_run`, `expected_revision` e confirmação válida por dez minutos; valida novamente no commit | Candidata diferente, agenda alterada e repetição da confirmação aceita são recusadas. Fluxo integrado troca a identidade e regrava ambas as agendas de teste |
| Agendas acompanham revisão | Conexão, revisões das agendas compatíveis e evento de auditoria na mesma transação InnoDB. Nome, par de app validado e rotação da mesma identidade não invalidam a autorização anterior | Falhas SQL injetadas na agenda e na auditoria desfazem todos os registros da gravação; duas sessões MySQL comprovam exclusão por trava |

A confirmação vincula candidata, aplicativo, identidade, permissões, expiração, site, ator/concessão, revisão da conexão e revisões das agendas. Não armazena o token em claro no comprovante. Uma candidata nova, outra revisão ou agenda alterada exige nova simulação.

O rebase conserva consulta, principal/concessão de origem, pausa, próxima data, frequência, último job e dados. Origem revogada continua sem autorização. Agendas já incompatíveis por mudança anterior de ativos/autorização aparecem em `schedules_requiring_review`; não são reautorizadas silenciosamente. A troca guiada exige que todas ainda usem ativos selecionados e conserva seus principais. Jobs e cursores iniciados sob outra identidade permanecem intactos e sujeitos à revisão antiga: não se mistura progresso entre identidades.

As 34 entradas de schema anteriores são idênticas à base 0.8.0; a nova operação eleva o catálogo a **35**. Salvar/renovar agora envolve leitura do fornecedor, anunciada nos metadados de efeito. Permanecem IDs, namespaces, prefixos, permissões administrativas e contratos de consulta. Diferença de runtime: **1 arquivo adicionado, 29 alterados, 13 idênticos, nenhum removido**. A nova classe é `ConnectionChanges`.

Referência técnica: [Meta — Debug Token](https://developers.facebook.com/docs/graph-api/reference/debug_token/). A identidade humana usa leitura complementar de `/me`, pois o diagnóstico de token não é tratado como fonte do nome de usuário. Os formatos locais exigidos vêm do pedido 15; não são uma garantia universal de formato para todos os produtos Meta.

## 4. Instalação, prontidão e testes

**Site-Teste atualizado de 0.8.0 para 0.9.0** pelo instalador final da seção 8, com `activate=true`, `overwrite=true`, hash e slug esperados. Operação `b855e89a265ac72401285e91`; operação de pacote `d7f08734a46cd49dd96f711e663e2c16`; backup `70f312b77dfbf9b62e096331`. Resultado `applied=true`, ativo, versão conferida em PHP novo.

Home e `/wp-json/` tiveram HTTP 200 antes/depois, com desvio de cache conferido pelo canal. Essas são sondas internas de mesma origem; não são prova de alcance externo independente. A troca usa reativação silenciosa. A instalação limpa com hook de ativação foi provada separadamente em laboratório descartável.

| Cenário | Ambiente | Resultado |
|---|---|---|
| Pedido 15 ampliado | WP 7.1.3 / PHP 8.3.36 / MySQL 8.0.41, Meta isolado | 55 verificações aprovadas: recusas, preservação, confirmação, concorrência, rollback, permissão e ajuda |
| Regressões de worker/saúde/ilegibilidade/snapshot | Mesmo ambiente | 27 + 23 + 11 + 8 verificações aprovadas |
| Instalação isolada e documentação nativa | Mesmo ambiente | 24 de smoke e 103 de catálogo/documentação/autorização aprovadas |
| Mínimos exatos, instalação limpa | **WP 6.4 / PHP 8.1.2-1ubuntu2.28**, 64 bits / MySQL 8.0.41 | **124 verificações aprovadas**: pedido 15 (55), smoke (24), snapshot (8), worker (26), ilegibilidade (11) |
| Atualização direta 0.8.0 → 0.9.0 | WP 7.1.3 / PHP 8.3.36, processos novos | 5 provas de preservação e 103 de metadados/documentação aprovadas; conexão, agenda, dois jobs, página de resultado, histórico e opção de negócio conservados |
| Interface | HTML gerado pelo WordPress e jsdom 27.4.0 | 19 verificações de interação aprovadas |
| Credenciais no Site-Teste integrado | Pacotes da seção 2 | 11 verificações aprovadas; 13 chamadas Meta interceptadas, zero chamadas reais ao fornecedor |
| Fronteiras no Site-Teste integrado | MCP original, Core/Google e LinkedIn observado 0.10.1 | 19 verificações aprovadas; 1124 arquivos de MCP/Core/Google/Meta conferidos; sem disparo de e-mail/API social |
| Selftest final | Site-Teste | 8 verificações aprovadas |
| Build | PHP 8.3.6 | Lint dos 22 PHP do runtime, sintaxe JavaScript e instalador com 43 arquivos |

As contagens incluem casos comuns e não são um total de casos únicos. Os testes nativos são WordPress real em diretório/prefixo exclusivos no próprio Site-Teste, sem acompanhantes; não são restauração nem limpeza do banco compartilhado. O candidato teve ajustes de metadados/documentação após parte das regressões; mínimo, atualização e integração usaram o instalador final. Evidências preliminares não são contadas como aprovação. Os ajustes do harness e o achado do redator estão identificados em `evidence/0.9.0/preliminary-observations.md`.

**Documentação pelo MCP:** índice e todos os **17 documentos** instalados foram lidos integralmente em **19 páginas / 20 chamadas**, incluindo três páginas do schema. Conteúdo UTF-8, bytes, versão e SHA-256 são iguais ao instalador. A revisão foi fixada nas continuações. A prova nativa também cobre confinamento, autorização e ausência de HTTP/escritas na leitura documental.

**Estado final:** Meta 0.9.0 ativo, `health.state=ok`, sem issues, conexões ou agendas de teste, sem atraso/fila ilegível. Os laboratórios tiveram suas 14 tabelas privadas e diretórios removidos. Os três auxiliares desta rodada foram retirados; restaram os quatro MU-plugins originais de recuperação. Backups do MCP e auditoria técnica foram conservados. DreamHost 1.0.0, WPSC 3.1.4 e Yoast 28.7 preservados.

## 5. Banco e reversão

Nenhuma tabela, coluna ou option nova; schemas existentes preservados. A identidade recebe metadados adicionais no registro cifrado da conexão. As agendas recebem as revisões atuais apenas nas gravações autorizadas. O evento de rebase usa o bucket de auditoria existente, com revisão anterior/nova e IDs das agendas, retenção de 30 dias.

Conexão, agendas e evento usam transação InnoDB e revisão otimista, sob travas nomeadas. A agenda mantém seu principal. Falha em gravação confirma rollback nos testes; falha de confirmação de commit retorna `persistence_unconfirmed` e exige releitura antes de repetir. Mesmo uma recusa ou prévia pode produzir a auditoria técnica normal da chamada. Não se afirma ausência de todos os efeitos locais.

Para voltar, usar o instalador original 0.8.0 verificado ou o backup de arquivos da operação. **Backup de plugin não desfaz banco, troca de token, revisão de agendas nem efeitos externos.** A versão anterior não oferece as novas validações/confirmações. Preservar e avaliar os registros, sem desinstalar ou apagar opções para forçar retorno. Não foi executado rollback remoto.

## 6. Pendências e responsáveis

- **Operador/dono das contas Meta:** homologar o pedido 15 com tokens, aplicativo e ativos reais autorizados. A validade, scopes, nomes e acesso nos ensaios são respostas sintéticas. A leitura de metadados não comprova disponibilidade de toda métrica/relatório no fornecedor.
- **Revisor central:** aceitar e encerrar editorialmente o pedido 15 após o aceite aplicável. A aba central não foi modificada.
- **Frota/dono:** decidir publicação e implantação nos demais sites. Não houve push público nem instalação fora do Site-Teste.
- **Pendências de frota 20 e 88:** permanecem com seus responsáveis; e-mail real, rotação em produção, histórico exportado, Story expirado, perfil de assinante em produção e conexão de twinia não são encerrados por ensaios sintéticos.
- **Limites de prova:** sem inspeção visual integral em navegador; HTML/DOM foram exercitados. Para LinkedIn 0.10.1, a prova é do instalado e de suas interfaces; seu ZIP final não foi comparado nesta rodada.

Não há falha conhecida aberta nos cenários executados. Isso não estabelece ausência universal de impacto em versões ou contas não exercitadas.

## 7. Credenciais e configuração do dono

Tela: Ferramentas → Fator3 MCP Meta → Conexão. O App ID e App Secret ficam em Meta for Developers → Meus apps → app → Configurações do app → Básico. O token de usuário do sistema é gerado em Meta Business Suite → Configurações → Usuários → Usuários do sistema → usuário → Gerar token, escolhendo o mesmo app. As ajudas completas e os cinco escopos estão na tela e em CONFIGURATION.md.

Nenhuma credencial real foi recebida, exportada, substituída ou revogada nesta rodada. Token e App Secret vazios mantêm o valor salvo. Nova candidata exige o par de aplicativo; sua validade remota prevalece sobre a data digitada. A troca guiada tem prévia e confirmação; não usar “Anular tokens”, pois a revogação pode alcançar usos da mesma credencial no Core. A instalação sozinha não requer segredo novo nem liga uma integração comercial.

## 8. Identidade dos arquivos

| Artefato | Nome | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `wp-mcp-meta-fator3-0.9.0-instalador.zip` | 173724 | `e26aede1591426e06b8a69b5ad405cf13cb70c28d41b607346188c9d21a15662` |
| Fonte | `wp-mcp-meta-fator3-0.9.0-fonte.zip` | 1218318 | `2c80d2e290c2ef453c1d92d9b7cea6f5f0bf77a8585bc46cd77f7ba0f4023e65` |

Relatório: `wp-mcp-meta-fator3-0.9.0-relatorio.md`. Instalador com raiz `wp-mcp-meta-fator3/`, único ZIP instalável. Fonte com raiz `wp-mcp-meta-fator3-0.9.0-fonte/`, código canônico, runtime idêntico, testes, evidências sanitizadas, plano e documentos recebidos. Não contém ZIP aninhado, banco, cookies, credenciais reais, node_modules ou auxiliares QA no runtime.

A cópia do relatório no fonte é anterior ao fechamento; bytes/hash do próprio fonte são preenchidos somente neste relatório externo. Nenhum relatório de impacto novo acompanha a entrega porque não há consequência ou solicitação própria a outro mantenedor identificada nas fronteiras avaliadas.
