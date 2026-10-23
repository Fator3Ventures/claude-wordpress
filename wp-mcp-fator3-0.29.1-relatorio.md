# Entrega — Fator3 MCP 0.29.1

Revisão 1 · 23/10/2026 · Rodada: revisão independente da 0.29.0 recebida.
Slug: `wp-mcp-fator3` · Versão corrente: **0.29.1**.
Status: **apta-no-escopo-testado**, com limites externos na seção 6.

Relatório externo canônico. A cópia no fonte antecede seu fechamento; tamanho e SHA-256 do próprio fonte são preenchidos somente no relatório externo.

## 1. De onde esta versão entra

A 0.29.0 feita em outra sessão foi comparada à referência aceita 0.28.0, revisada e testada com os acompanhantes atualizados. Três defeitos foram reproduzidos; conforme a instrução expressa do dono, foram corrigidos incrementando somente o patch. **A 0.29.1 substitui a 0.29.0 como versão corrente desta entrega.** Os arquivos recebidos foram preservados.

| Entrada | Bytes | SHA-256 |
|---|---:|---|
| MCP 0.29.0 instalador | 870821 | `1720f2db05c5a6ee90d1269ebdc764c14fb6b60e2878f765cf1183093ef1fb2a` |
| MCP 0.29.0 fonte | 3745528 | `c59bc9ff5afab9de2b55f58d57b1efc362791d10ae441ac69f6861c3d891ae2c` |
| MCP 0.28.0 instalador de referência | 853885 | `d1d297d8aaee0e5188b92fe9eae20a9dcc07e79d639baae25f267bf64f7243b0` |

O fonte recebido reproduziu o instalador 0.29.0 byte a byte. Foram comprovadas instalação limpa e atualizações diretas **0.29.0→0.29.1** e **0.28.0→0.29.1**; não existe etapa intermediária obrigatória.

Mínimos declarados e executados: WordPress **7.1.2**, PHP **8.3.6**; também executado WordPress 7.1.3. Banco local MySQL 8.0.46; PHP CLI/FPM, quatro workers, OPcache com `validate_timestamps=0`. Site-Teste: WordPress 7.1.3/PHP 8.3.36. Identidade, basename, namespaces, rotas, IDs e três metatools preservados.

Aplicadas as normas comuns revisão 4 e os dois impactos adicionais enviados pelo dono. Escopo limitado ao MCP; nenhum código ou documento central de outro plugin foi alterado.

## 2. Convivência e encaminhamentos

| Acompanhante | Laboratório integrado próprio | Site-Teste após a troca | SHA-256 do instalador local |
|---|---|---|---|
| Site Core | 1.48.0 | 1.48.0 | `91097a3819cce15fcc66adfa5d8503537cacdb51cfd3ad04ba73e5f7c27a18de` |
| Google | 0.18.1 | 0.17.0, preservado | `91c97cc300360511bc2477f5af9b0c2017e8b04861d015aaf0f0e5accd1cefef` |
| Meta | 0.7.1 | 0.7.1 | `0adbea179f3a89cd66b6dce289fa8658e1723f4a9b38568794fc7c3aea5963f2` |
| LinkedIn | 0.8.1 | 0.8.1 | `172081883af66b8c4b61676396d85066d4be0778b7ca06fb22262b30a4d2374a` |

O Core 1.49.0 é mencionado na prova recebida da outra sessão, mas seu instalador não foi localizado para reexecução. O 1.48.0 foi o mais recente obtido e é o instalado no Site-Teste. A compatibilidade com Google 0.18.1 foi exercitada localmente; não se atribui essa versão ao teste remoto.

**Impacto Meta 0.6.0 → MCP, revisão 3:** considerado e confirmado. `meta/status` continua escrita local; perfil read e custom sem autorização explícita são recusados, maintenance é aceito. `meta/health` da 0.7.1 permanece leitura. Para observar estado atual, omitir `idempotency_key`. Não houve ampliação de perfis.

**Impacto LinkedIn 0.7.0 → MCP, revisão 3:** o texto foi emitido contra o MCP 0.27.0, antes da implementação central. O handshake, registro e recibo de `mutation-service-audit/1.0.0` foram implementados na 0.28.0 e passaram novamente com LinkedIn 0.8.1: usuário zero/incidental, concessão, digest, antes/depois, revogação, retenção e ausência de reenvio. Não há importação automática de diários. MCP 65/LinkedIn 8(d) estão resolvidos tecnicamente no conjunto testado; encerramento editorial pertence ao dono. A previsão histórica não foi tratada como falta de implementação atual.

Quatro alertas individuais foram preparados antes do código dependente e atualizados na entrega, sem mudança obrigatória nos destinatários ou ordem conjunta de instalação:

- `wp-mcp-fator3-0.29.1-impacto-wp-mcp-google-fator3.md` — repetição exige prova explícita de ausência de efeito.
- `wp-mcp-fator3-0.29.1-impacto-wp-mcp-meta-fator3.md` — mesma proteção e confirmação do contrato de status.
- `wp-mcp-fator3-0.29.1-impacto-wp-mcp-linkedin-fator3.md` — mesma proteção e auditoria de serviço preservada.
- `wp-mcp-fator3-0.29.1-impacto-base-site-core-fator3.md` — nonce em admin-post GET e permissão do domínio preservada.

Situação: revisão 2, resolvidos no MCP; alertas sem ação imediata obrigatória. Os originais recebidos estão em `docs/entradas/0291`; os encaminhamentos próprios em `docs/impacto-mcp-0.29.1-para-*.md`. Nenhuma mensagem foi enviada a terceiros. Implantador não recebido: não avaliado.

## 3. Mudanças e evidência

A comparação de instaladores **0.28.0→0.29.0** encontrou dois arquivos adicionados e 13 alterados, nenhum removido: 459→461 arquivos. Foram examinadas e preservadas as melhorias M1–M7: chamada nativa de administrador; busca sem acentos e redução das consultas de política; descrições de parâmetros em português; liberação de falha transitória; pesquisa documental; filtro por provedor e schemas na descoberta; proteção de conexões sem rótulo e leitores ausentes.

| Achado próprio | Efeito observado na 0.29.0 | Correção 0.29.1 |
|---|---|---|
| R1 — alta: idempotência sem prova de ausência de efeito | Mesma chave executou duas vezes quando applied faltava/era null, persisted/changed eram null ou partial=true. Recibos antigos com esses estados também eram descartados. Isso pode repetir uma operação já aplicada pelo fornecedor. | Requer success=false, retryable=true e **applied=false explícito**. persisted/changed/partial presentes devem ser false. Resultados desconhecidos/parciais e códigos de incerteza continuam conservados e reproduzidos. |
| R2 — baixa: busca ignorava termos | Um 13º termo inexistente era descartado e a consulta ainda retornava resultados, em descoberta e documentação. | Todos os termos são considerados; repetições são deduplicadas, mantendo busca sem diferença de acento/caixa. |
| R3 — média: admin-post GET confundido com tela | Com nonce válido, a escrita aderente era recusada; sem nonce, a leitura passava pela exceção de tela administrativa. | admin-post exige nonce para qualquer método. Com nonce, chega ao permission_callback do provedor. GET de tela comum permanece restrito a leitura. |

Os testes adicionais reproduziram **13 verificações negativas** na base: nove relacionadas a R1, duas a R2 e duas a R3. São manifestações de três defeitos, não 13 bugs distintos. Controles de applied=true, operation_uncertain, ausência de efeito explícita, OAuth, senha de aplicativo e perfis continuaram funcionando.

O código funcional do patch muda somente `ExecutionCoordinator.php`, `NativeAdminCall.php` e `SystemTools.php`. Há atualização de versão/documentação compilada e inclusão da nota de release. O instalador final contém **463 arquivos, 452 PHP**; oito caminhos diferem da 0.29.0, dos quais dois são novos documentos/índice. Sem alteração de CSS/JavaScript, SDK, schema obrigatório, tabela ou credencial. Diffs e hashes estão em `evidencias/review0291`.

Ocorrências de preparação registradas: o check CLI inicial usava usuário 1 com política maintenance criada pelo setup, contrariando a premissa “sem política”; a fixture foi ajustada para usar o administrador nativo sem política. A primeira suíte de serviço recusou LinkedIn 0.8.1 por uma guarda antiga fixada em 0.7.0; a guarda foi atualizada após conferir o contrato. Não foram correções de runtime nem falhas ocultadas dos cenários finais.

## 4. Instalação e prova da troca

**319 verificações aprovadas** nos cenários finais abaixo. Contagem de execuções, com sobreposição entre suítes; não representa 319 casos independentes. Ativações de preparação não entram no total. Lint, pacote e provas remotas são adicionais.

| Prova própria | Verificações | Resultado / limite |
|---|---:|---|
| Adversarial: efeitos desconhecidos, recibos antigos, termo 13 e perfis Meta | 18 | Sem falhas; efeitos sintéticos |
| Chamadas administrativas nativas, OAuth/aplicativo e recusas | 26 | HTTP real local; nonce, admin-ajax, admin-post, REST e CLI |
| Idempotência transitória, resultado concluído e conflito | 7 | HTTP MCP real |
| Descoberta, filtros, schemas, idioma e equivalência de perfis | 17+17 | 712 habilidades no catálogo integrado, incluindo fixtures; Meta 34 |
| Pesquisa documental e renderização de conexões sem rótulo | 11+3 | Sem HTTP de fornecedor; sem warning no formulário |
| Auditoria LinkedIn de serviço e humana | 54+32 | Classes reais dos dois plugins; HTTP LinkedIn sintético |
| Idioma e leitor documental local | 8+27 | Contratos e documentos preservados |
| Documentação integral pelo MCP HTTP | 29 | 26 documentos/28 páginas, 201406 bytes, hashes iguais |
| Limpo, somente MCP, WordPress 7.1.3 e 7.1.2 | 13+13 | Ativação em processo separado; HTTP, cron e arquivos exatos |
| Atualização direta da 0.29.0 e da 0.28.0 | 22+22 | MCP HTTP/Plugin_Upgrader, quatro workers FPM; todos os arquivos finais iguais ao ZIP |
| Sintaxe | 452 arquivos PHP | PHP 8.3.6, zero erros |

Os laboratórios bloquearam HTTP externo e interceptaram e-mail. Nenhuma conversão, publicação social ou mensagem real foi enviada. Logs locais: nenhum notice/warning/deprecation/fatal apontando para o runtime MCP instalado; avisos de preparação das fixtures foram separados. Processos dos laboratórios foram encerrados.

**Site-Teste:** o mesmo instalador final foi instalado via MCP de **0.28.0 para 0.29.1**. Operação de pacote `8e576298df043d3b092f6f78b049379c`, operação administrativa `b0c51ea703b2a38305100df9`, backup da pré-imagem `841b0048fbad5637e6272c2f`. Ativo antes/depois, reativação silenciosa em PHP novo; home e `/wp-json/` HTTP 200 antes/depois, com evidência de bypass de cache. Essa reativação não equivale a ciclo completo de hook de ativação; o ciclo foi exercitado nas instalações limpas.

Em requisições novas: MCP 0.29.1, `system/health.healthy=true`, LinkedIn 0.8.1 state=ok e Meta 0.7.1 state=ok. As quatro projeções de configuração (`sql_retention`, `file_bytes`, `enabled`, `update_channels`) permaneceram iguais. Busca com 13º termo inexistente retornou zero; descoberta Meta retornou 34 habilidades, primeira página de 25 com schemas. Os 26 documentos foram lidos integralmente pelo conector autenticado e confrontados byte a byte com o conteúdo compilado do instalador.

Navegador real: aba Clientes conectados e edição de conexão sem rótulo abriram com versão 0.29.1, sem avisos PHP e sem estouro horizontal (1348 px). Nenhum formulário foi salvo. Capturas usadas só na inspeção, não incluídas na entrega.

Estado final: MCP 0.29.1 ativo; os sete acompanhantes do inventário remoto mantiveram versões/ativação. Nenhuma sonda ou fixture desta revisão foi instalada no servidor. ZIP temporário apagado com conferência de hash; permanecem backup e auditoria normais. Não houve publicação Git/raw nem distribuição à frota.

Para nova instalação, usar somente o ZIP instalador da seção 8, `expected_slug=wp-mcp-fator3`, conferir SHA-256 e preservar backup. Prontidão: `system/capabilities` versão 0.29.1, `system/health`, `system/guide {"document":"release-0291"}`. Índice documental: `system/guide {}`; leitura com document/cursor/expected_sha256 e byte_limit até 32768.

## 5. Banco e volta de versão

Sem migração, tabela, coluna, opção, cron, segredo ou concessão nova. O patch conserva recibos de falhas com efeitos não comprovadamente ausentes, em vez de liberá-los. Não reaplica ou importa operações anteriores.

Ambos os ensaios de atualização preservaram senha de aplicativo, concessão e tokens OAuth sem extensão de validade, renovação por refresh, opções false/vazias, confirmação SQL pendente, backup privado, recibo concluído e recibo incerto. Recibo concluído não duplicou conteúdo. Cursor documental antigo foi recusado; rollback em **prévia** conferiu a pré-imagem. Não foi aplicado downgrade nesta revisão.

Restaurar arquivos para 0.29.0 reintroduz os três defeitos. Backup de plugin não desfaz banco, auditoria ou efeitos externos; preservar backup operacional e salts. Não desinstalar para simular reversão, nem criar nova chave para contornar resultado incerto sem investigar o efeito anterior.

## 6. O que permanece pendente

- APIs comerciais e ativos reais: testes de fornecedor foram sintéticos. Não comprovam aceite de conversão, atribuição, permissões externas ou entrega de e-mail.
- Core 1.49.0: citado em evidência recebida, mas não disponível para nova execução. Google 0.18.1 foi testado localmente; o remoto manteve 0.17.0.
- Fluxo comercial do Core com Google Ads/LinkedIn configurados: o teste nativo alcançou decisões de domínio com configuração ausente; não homologou campanhas reais.
- Multisite, downgrade aplicado e novo ciclo OAuth completo de cliente Claude real não foram executados nesta revisão. O conector ChatGPT existente foi preservado e usado após a atualização. Isso não reabre o aceite anterior de B22/CIMD.
- Publicação raw e distribuição à frota cabem ao dono/responsável; nenhuma publicação foi feita nesta tarefa. Encerramento editorial MCP 65/LinkedIn 8(d) permanece com o dono.

Não restam falhas nos cenários finais executados. Essa conclusão não é garantia de ausência de qualquer impacto em ambientes ou contas não ensaiados.

## 7. Credenciais e configuração do dono

Nenhum novo campo obrigatório, token, consentimento ou perfil. Não é necessário recriar conexões por causa do patch. Manter as permissões administrativas e os perfis existentes.

Para autores de provedores: `retryable=true` sozinho não autoriza repetir a mesma chave; declarar `applied=false` somente quando a ausência de efeito estiver comprovada. Depois de timeout com resultado desconhecido, conservar o recibo e reconciliar. Para usuários do Meta, usar health para leitura e status somente com perfil que autorize escrita local.

Nenhum segredo real, cookie, dump de banco, configuração privada de laboratório ou captura de navegador foi incluído nos artefatos. Evidências de escrita usam dados sintéticos.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `wp-mcp-fator3-0.29.1-instalador.zip` | 873894 | `1b627aec5c24dc88f52eaf6a0d34367437d7f9e7b599f9f07850567fd57610e6` |
| Fonte | `wp-mcp-fator3-0.29.1-fonte.zip` | 3945818 | `99ea12645e25d75f2466feebc4ac146e776f33b398d74802f4f6a48327a4142a` |

Relatório: `wp-mcp-fator3-0.29.1-relatorio.md`. Os quatro impactos individuais estão relacionados na seção 2 e também acompanham a entrega.

Instalador com raiz `wp-mcp-fator3/`; fonte com raiz singular `wp-mcp-fator3-0.29.1-fonte/`, código, documentação, build, testes e evidências. Nenhum ZIP contém outro ZIP. O fonte é fechado após o instalador e reproduz exatamente o mesmo instalador testado e instalado. Esta cópia interna antecede o fechamento do fonte; o relatório externo completa sua identidade sem alterar o ZIP.
