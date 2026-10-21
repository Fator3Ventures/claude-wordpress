# Entrega — Fator3 MCP 0.25.0

Revisão: 2 · Data/hora: 2026-10-21T10:12:03-03:00 · Fuso: America/Sao_Paulo.
Rodada: implementação do pedido MCP 62, com revisão documental do fechamento.
Slug: `wp-mcp-fator3` · Versão: `0.25.0`.
Status: `apta-no-escopo-testado` para o pedido MCP 62; B22/CIMD permanece `pendente`.

Histórico: a revisão 1 foi fechada em 2026-10-21T09:51:02-03:00. Esta revisão 2 organiza o relatório conforme o padrão rev4, explicita estados de evidência, credenciais e responsáveis pelas pendências. Não altera código, instalador, fonte, resultados de testes ou instalação. A cópia congelada dentro do fonte permanece a anterior ao fechamento da revisão 1.

## 1. De onde esta versão entra

Implementado o pedido **MCP 62**, com atualização da base **0.24.0**. O pacote final foi instalado e conferido no Site-Teste https://fator3-teste-mcp-1.dreamhosters.com/. Os quatro plugins acompanhantes foram considerados e mantidos nas versões existentes. Não houve publicação em frota, GitHub ou fonte automática de atualização.

O pedido 61 permanece resolvido na base; a regressão de booleanos e proteção de segredos foi exercitada novamente. A validação externa CIMD B22 continua pendente e não integra o aceite do pedido 62.

Base imediata aceita: instalador fornecido `wp-mcp-fator3-0.24.0-instalador.zip`, SHA-256 `e2c78fcf0e99da55237808bc51fe408405e367fd76a71172b497707996f8aa95`. Foram comprovadas instalação limpa e atualização direta 0.24.0 → 0.25.0; nenhuma versão intermediária é necessária nesse percurso.

Requisitos mínimos declarados e exercitados: WordPress 7.1.2 e PHP 8.3.6. Também foi usado WordPress 7.1.3; o Site-Teste executa PHP 8.3.30. Os testes nativos locais usaram MySQL e FPM/HTTP, conforme as evidências do fonte.

## 2. Convivência e encaminhamentos

| Componente | Referência fornecida e conferida |
|---|---|
| Site Core | 1.43.0; instalador SHA-256 `5a7c02abb97f7161617ddfd8e4d28faf2fdb22e4ae5d4ed75416dc68d76ee9e7` |
| MCP Google | 0.16.0; instalador SHA-256 `e0dfee63fbd9ad9fcc6b5ab9a3b9d492d7e497822154e0572589a45f3116248c` |
| MCP LinkedIn | 0.4.1; instalador SHA-256 `a1f2bd2393c7f1b1780f106f4a7c3ac46776a8a7cc7071f1e269daad7ec34c43` |
| MCP Meta | 0.4.1; instalador SHA-256 `719e3db7bb55f58cd08c2e78420e06374a6a4b08fad693e849677783ddc82de2` |

Os relatórios dos quatro companions e as instruções de desenvolvimento rev4 de 16/10/2026 foram lidos integralmente. As entradas e hashes adicionais estão em `evidencias/0250/inputs.json`; o plano atualizado está em `docs/PLANO-0250.md`.

Não há dependência obrigatória de companion. Permanecem server-integration 1.0.0, executor-registration 1.0.0, package-distribution 1.0.0, policy_contract 1 e schema de dados/resultado 2. Não foi identificado impacto que exija alteração em outro plugin; por isso não foi produzido um pedido artificial de impacto. A limitação de rollback com arquivos novos citada pelo Google não foi alterada; este release não acrescenta arquivos ao runtime.

As referências dos relatórios recebidos são entradas de análise; as provas próprias de coexistência são `companions-setup.json`, `acceptance-companions.json` e `site-tests.json`. A revisão não declara homologação das contas ou APIs externas dos acompanhantes. Os contratos preservados não exigem troca coordenada dos outros quatro plugins para instalar este MCP.

## 3. Mudanças e evidência

| Pedido | Implementação e comportamento | Evidência |
|---|---|---|
| Pedidos MCP 62a — assuntos separados | Oito abas com URL própria: Conexão do servidor, Clientes conectados, Arquivos e banco, Operações, Registro, Diagnóstico, Atualizações e Ajuda. Navegação visual por botões arredondados, coerente com os sociais atuais. URLs e identificadores antigos das abas continuam aceitos. | admin.json, dom.json, browser.json |
| Pedidos MCP 62b — português e ajuda individual | Rótulos administrativos em português; cada permissão adicional tem ajuda própria e associação acessível ao campo. Os nomes de produtos, protocolos e IDs públicos permanecem técnicos. | admin.json, dom.json, browser.json |
| Pedidos MCP 62c — habilidades selecionáveis | Catálogo real em lista pesquisável com nome humano e identificador. Pesquisa não desmarca nem omite valores selecionados na submissão. Identidades existentes e tipos de conteúdo também usam seletores com nomes. | admin.json, dom.json, browser.json |
| Pedidos MCP 62d — datas e estados | Registro com seletores nativos de data/hora em UTC e resultado Todos/Concluído/Falhou. Operações com lista de estados em português. Intervalos inválidos são recusados; segundos da expiração são preservados. Links antigos com ISO continuam aceitos. | admin.json, admin-minimum.json, browser.json |
| Pedidos MCP 62e — atualização do próprio plugin | A tela exibe somente o canal do MCP, sem rótulo com nome de arquivo. Salvar ou desabilitar preserva as entradas dos demais pacotes; há controle de revisão, permissão e HTTPS. O contrato remoto multipacote não foi removido. | admin.json, admin-minimum.json, site-tests.json |
| Pedidos MCP 62f — ajuda curta e manual separado | Ajuda contextual por campo e página própria de documentos com paginação. Foram atualizadas referências de versão, base e matriz; material histórico é identificado como tal. | site-documents.json, acceptance-isolated.json, browser.json |
| Pedidos MCP 62g — configuração estruturada | Perfil, permissões, identidades, habilidades, tipos, expiração, limite por arquivo, retenção SQL e fonte de atualização são configuráveis em campos próprios. Exemplos e detalhes técnicos JSON são apenas de leitura, sem editor JSON operacional. | admin.json, admin-minimum.json, dom.json, browser.json |

O limite global de arquivo e o limite individual de Manutenção aceitam 1 MiB a 1 GiB. O campo individual vazio volta a herdar o canal. Constantes e filtros definidos pelo administrador do servidor são informados como restrições efetivas; a tela não edita arquivos PHP de configuração.

A interface mantém validação de capacidades, nonce, revogação e versão de política. Habilidades/tipos de provedores temporariamente ausentes podem permanecer em seleções preexistentes, sem autorizar novos identificadores desconhecidos. O salvamento do canal preserva valores falsos, vazios, campos adicionais e entradas de outros provedores. Alterações concorrentes exigem recarregar.

Os subitens a–g pertencem ao pedido existente **Pedidos MCP 62**, sem criar novos tickets. Todos estão `implementado`, `validado-localmente` e `validado-wordpress` nas camadas especificadas. `homologado-fornecedor` é `nao-aplicavel` ao aceite dessa interface administrativa. As evidências citadas ficam em `evidencias/0250/` no fonte; o detalhamento de ambientes e limites está na seção 4.

## 4. Instalação e prova da troca

Em instalação limpa, envie somente o instalador pelo WordPress, ative e configure explicitamente a conexão/perfil. Para a frota 0.24.0, valide o SHA-256 e use o fluxo de atualização com expected_slug, expected_sha256, overwrite e activate explícitos, conforme `docs/ATUALIZACAO.md`. Confirme a versão em requisição nova e acompanhe operation-status/reconcile se houver verificação pendente. Não desinstale para atualizar.

No MCP, `system/guide` lista os documentos; use `document:administracao`, `document:release-0250` ou `document:atualizacao`, mantendo o cursor e expected_sha256 entre páginas. Nenhuma etapa deste trabalho publicou automaticamente a versão para outros sites.

A instalação autorizada no Site-Teste usou `plugins/upload-base64`, com ZIP temporário local ao servidor, `expected_slug: wp-mcp-fator3`, `expected_sha256` igual ao instalador da seção 8, `overwrite: true` e `activate: true`. A origem pública raw não foi publicada nesta rodada; sua publicação e conferência cabem à frota quando autorizadas. A prontidão foi comprovada por `system/health` e `plugins/list`; a preservação de configuração foi conferida por `system/settings` e os arquivos alterados por `files/stat` com hash.

### Testes executados na implementação

| Camada | Ambiente e evidência | Resultado |
|---|---|---|
| Administração nativa | WordPress 7.1.3, PHP 8.3.6, MySQL, FPM/HTTP; admin.json | 69 verificações aprovadas |
| Administração no mínimo | WordPress 7.1.2, PHP 8.3.6; admin-minimum.json | 69 verificações aprovadas |
| MCP isolado | WordPress 7.1.2 / PHP 8.3.6; acceptance-isolated.json | 39 verificações aprovadas, incluindo leitura integral de 19 documentos |
| Coexistência | WordPress 7.1.3 / PHP 8.3.6 com os quatro companions atuais; acceptance-companions.json e companions-setup.json | 45 verificações e 4 ativações aprovadas |
| Atualização direta | 0.24.0 → ZIP final 0.25.0, HTTP nativo; upgrade.json e upgrade-package.json | 19 verificações aprovadas; todos os arquivos instalados coincidem com o ZIP |
| Instalação limpa | ZIP final em bancos/raízes novos, WordPress 7.1.2 e 7.1.3 / PHP 8.3.6; clean-minimum.json e clean.json | Ativação e leitura em processo novo aprovadas, sem companions |
| Projeção de resultados | Classes reais da versão; projection.json | 18 verificações aprovadas, preservando booleanos públicos e redação de segredos |
| DOM | HTML real de WordPress, jsdom 27.4.0; dom.json | 237 verificações aprovadas; pesquisa, seleção enviada, nomes, IDs e ajuda acessível |
| Sintaxe | PHP 8.3.6 sobre o instalador extraído; lint-installer.json | 448 arquivos PHP sem erro |
| Site-Teste | WordPress 7.1.3 / PHP 8.3.30; site-tests.json | Saudável após atualização; configurações e companions preservados |
| Navegador real | Chrome, sessão administrativa no Site-Teste; browser.json | Oito abas conferidas; pesquisa, filtros de data/resultado e paginação do manual funcionais |
| Documentação remota | system/guide, páginas completas; site-documents.json | 19 documentos com bytes e SHA-256 iguais aos fontes canônicos |

As contagens são verificações/assertivas, não quantidade de cenários independentes. Testes DOM não são apresentados como teste visual: a aparência e as interações também foram inspecionadas no Chrome. Capturas serviram à inspeção e não fazem parte do fonte.

A atualização direta verificou pré-imagem, oito respostas de novos workers com OPcache sem revalidação por timestamp, versão efetiva, preservação de senha de aplicação, token e refresh OAuth, prazo, perfil, recibo de idempotência, operação incerta, confirmação SQL pendente e backup privado. A prévia de rollback foi exercitada sem aplicar restauração.

### Estado final registrado no Site-Teste

O executor informou versão 0.25.0 ativa e sondas aprovadas. A candidata usada na inspeção inicial foi seguida pelo pacote com a revisão documental final, antes do fechamento da entrega. O pacote canônico é exclusivamente o hash `7f32527a88514f2f319e02308f491b96b3112b783f1b38791da85aab071ea961` acima.

- Operação inicial, partindo da 0.24.0: `e735740b145a4348811e50ed2cb99851`; pré-imagem `04a48ff551463a719105854a`.
- Operação do pacote final: `6b4fb083cf61153a70fb43d68e0940f9`; pré-imagem `cf5dabd3222881e7eee8c99f`.
- Os 14 arquivos modificados tiveram hashes lidos do servidor e comparados ao instalador final.
- sql_retention, file_bytes, enabled e update_channels permaneceram iguais; o contexto de política da conexão permaneceu igual.
- Core 1.43.0, Google 0.16.0, LinkedIn 0.4.1 e Meta 0.4.1 permaneceram ativos nas mesmas versões.
- O arquivo ZIP temporário foi removido por caminho exato e hash após a conferência. Pré-imagens de recuperação permanecem disponíveis.

Os resultados acima são os registros de encerramento da implementação. A revisão 2 verificou a organização documental, os campos de configuração no código já validado e a integridade dos dois ZIPs; não repetiu testes de execução nem alterou o ambiente remoto.

## 5. Banco e volta de versão

A release não introduz migração ou nova estrutura de banco. A interface grava as configurações existentes de perfis, limites de arquivos, retenção SQL e canal de atualização por seus fluxos autorizados. Salvar retenção não exclui backups: aplicar limpeza continua exigindo simulação e confirmação. Salvar o canal de atualização não instala pacotes.

Na troca real, `sql_retention`, `file_bytes`, `enabled`, `update_channels`, contexto da conexão e versões dos acompanhantes foram preservados. O teste de atualização direta também verificou senha de aplicação, tokens OAuth e refresh, prazo, perfil, recibo de idempotência, operação incerta e confirmação SQL pendente. Os contratos de autenticação, dados e resultado permanecem nas versões documentadas na seção 2.

As pré-imagens de arquivos das duas operações estão identificadas na seção 4. O teste de atualização exercitou a prévia de rollback, sem aplicar restauração; as pré-imagens não equivalem a um backup completo do banco compartilhado.

Qualquer reversão deve começar pela consulta do diário e pela prévia do rollback corrente; uma pré-imagem de uma etapa anterior não deve ser aplicada ignorando a sequência de alterações. Restauração de arquivos não promete reversão de efeitos de banco dos companions.

## 6. O que permanece pendente

Mínimos declarados e exercitados nesta rodada: WordPress 7.1.2 e PHP 8.3.6. WordPress 7.1.3 também foi exercitado; o Site-Teste usa PHP 8.3.30. Não se declara teste desta candidata em PHP 8.3.0 ou em navegadores adicionais.

Não foram executadas chamadas de negócio às APIs externas Google, Meta, LinkedIn, Pipedrive ou Slack. A coexistência, o catálogo e os diagnósticos locais não substituem homologação dessas integrações com contas reais.

B22, conexão nova ChatGPT com CIMD, segue pendente. A preservação de uma conexão OAuth existente não comprova esse fluxo novo. Não houve reemissão automática de credenciais ou ampliação de perfis.

O diagnóstico do Site-Teste já indicava histórico incompleto de incidentes cron por limite de retenção antes da troca; isso continua identificado, embora o estado atual de saúde e os registros essenciais estejam confirmados. A versão não tenta reparar histórico antigo nem comprova todos os jobs dos provedores.

| Item | Estado, motivo e próxima ação | Responsável |
|---|---|---|
| B22 — nova conexão ChatGPT/CIMD | `pendente`. É um fluxo externo novo, não comprovado pela preservação OAuth. Realizar a autorização de uma conexão nova e validar descoberta, chamada e revogação; registrar evidências próprias do cliente. Não bloqueia o pedido 62. | Dono/administrador da conta ChatGPT, com o mantenedor MCP na validação do servidor. |
| APIs e fluxos de negócio Google, Meta, LinkedIn, Pipedrive e Slack | `nao-aplicavel` ao aceite do pedido 62; homologação externa não realizada. Cada cenário precisa de conta, token, ativo e escopo autorizados. | Responsável pelo plugin/integração correspondente e dono do ativo. |
| Histórico cron incompleto no Site-Teste | Limitação preexistente registrada; não há prova de todos os jobs nem recuperação retroativa dos incidentes descartados. Avaliar retenção apenas em tarefa operacional própria, se necessária. | Operação do Site-Teste e mantenedor do job afetado. |
| PHP inferior a 8.3.6 e navegadores adicionais | `nao-aplicavel` à matriz comprovada; suporte inferior ou validação adicional não foi declarado. | Mantenedor MCP, caso seja solicitado ampliar a matriz. |
| Publicação e distribuição à frota | Não executadas nesta rodada. Conferir o instalador e o relatório, publicar sob autorização operacional e verificar hash dos bytes raw antes da instalação. | Dono da entrega e responsável pela frota. |

## 7. Credenciais e configuração do dono

A atualização preserva as credenciais existentes e não exige preencher segredo novo. Para configurar um cliente, o administrador abre **Ferramentas → Fator3 MCP → Conexão do servidor**, copia a URL exibida e escolhe a forma de autenticação aceita pelo cliente.

| Tela/forma | Campos e ação do dono | Limites |
|---|---|---|
| Conexão do servidor → OAuth | Informar a URL no cliente e autorizar com a conta WordPress, escolhendo o perfil no consentimento. | Não exige gerar senha de aplicação nessa tela. A comprovação de uma nova conexão ChatGPT/CIMD permanece B22. |
| Conexão do servidor → Senha de aplicação | Escolher **Perfil da nova conexão** (Leitura ou Conteúdo); gerar a senha apenas quando necessária e configurar usuário/senha no cliente compatível. | A senha é exibida uma única vez. Revogá-la interrompe os clientes que a utilizam. |
| Clientes conectados | Selecionar **Usuário WordPress**, **Identidade autenticada**, **Nome do cliente**, **Perfil de acesso**, habilidades, tipos de conteúdo, diretórios, permissões adicionais e **Expiração (UTC)**. | Nome do cliente é rótulo, não segredo. As permissões WordPress continuam limitando o acesso. Nova emissão e revogação são ações explícitas. |
| Arquivos e banco / Atualizações | Definir limites e retenção pertinentes; preencher a fonte HTTPS do próprio MCP somente quando existir endereço publicado autorizado. | O perfil e o canal geral continuam valendo; os campos não concedem acesso às contas sociais. |

No Site-Teste, não foram emitidas credenciais, ampliados perfis ou alterados tokens dos acompanhantes nesta entrega. As credenciais sintéticas dos laboratórios serviram somente aos testes. Tokens sociais, escopos e ativos pertencem às telas e contratos de seus respectivos plugins; nenhum valor secreto faz parte dos artefatos.

## 8. Identidade dos arquivos

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-fator3-0.25.0-instalador.zip | 832809 | `7f32527a88514f2f319e02308f491b96b3112b783f1b38791da85aab071ea961` |
| wp-mcp-fator3-0.25.0-fonte.zip | 3005021 | `0ca0f140ba2b234f99067cb704a24aba43a85fd0855ba346a5ca709270c21fe4` |
| wp-mcp-fator3-0.25.0-relatorio.md | Este documento | Relatório externo, sem hash de si próprio para evitar autorreferência |

Instalador com 456 arquivos, dos quais 448 PHP. São 14 arquivos alterados e 442 idênticos à base 0.24.0; nenhum arquivo de runtime foi acrescentado ou removido. Os módulos de autenticação, SQL, recuperação e distribuição remota permanecem com seus contratos públicos. O ZIP não leva a bancada, testes, documentação bruta, credenciais ou ZIPs aninhados. A documentação instalada é compilada em uma lista fechada de documentos.

O fonte inclui código editável, documentação canônica, testes, scripts de construção e evidências sanitizadas. Sua reprodução foi conferida extraindo o próprio fonte, regenerando os guias e reconstruindo um instalador com o mesmo SHA-256. O hash externo do fonte é calculado somente após fechar o arquivo.

Links dos artefatos desta entrega:

- [wp-mcp-fator3-0.25.0-instalador.zip](sandbox:/workspace/scratch/d7106ddbcd96/release0250/entrega/wp-mcp-fator3-0.25.0-instalador.zip)
- [wp-mcp-fator3-0.25.0-fonte.zip](sandbox:/workspace/scratch/d7106ddbcd96/release0250/entrega/wp-mcp-fator3-0.25.0-fonte.zip)
- [wp-mcp-fator3-0.25.0-relatorio.md](sandbox:/workspace/scratch/d7106ddbcd96/release0250/entrega/wp-mcp-fator3-0.25.0-relatorio.md)

Relatório externo canônico, revisão 2. Tamanho e hash do fonte foram preenchidos somente após o fechamento do ZIP. A revisão documental posterior é permitida pela seção 3.1 do padrão e não modifica a cópia anterior ao fechamento preservada dentro do fonte. Os dois ZIPs mantêm exatamente os bytes, hashes e evidências certificados na revisão 1.
