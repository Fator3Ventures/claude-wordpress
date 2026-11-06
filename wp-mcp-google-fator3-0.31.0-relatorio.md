# Entrega — Fator3 MCP Google 0.31.0

Revisão 1 · 06/11/2026, America/Sao_Paulo · Rodada de implementação.
Slug/basename: `wp-mcp-google-fator3/wp-mcp-google-fator3.php`.
Status: **com-pendencias de homologação no fornecedor; correção implementada e validada no Site-Teste**.

Foram lidos integralmente `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos revisão 5 de 02/11/2026, e o pedido `Fator3 MCP Google(20261106-161732).md`. Cópias e relatórios recebidos constam em `reproducao/entradas031/`. A autorização explícita do dono abrange as alterações necessárias no Site-Teste.

## 1. De onde esta versão entra

Instalação limpa ou atualização direta **0.30.0 → 0.31.0**. Base: instalador de 944896 bytes, SHA-256 `4920abef86f65cc27178f16b2ea852b447d755507a6a8c82357b63b07c91b60e`, entregue na rodada anterior e confirmado instalado antes da troca. Incremento minor; identidades públicas preservadas.

Requisitos: **WordPress >= 7.1.4 e PHP >= 8.3**. Bancadas executadas: WordPress 7.1.4, PHP 8.3.6, MySQL 8.0.46. Site-Teste: WordPress 7.1.4 e PHP 8.3.36, obtidos por `system/health`. Navegador: Chrome headless shell 152.0.7940.0, Playwright 1.62.1 e Node 24.22.1. PHPUnit 9.6.37 com dependências do `composer.lock` preservado. Não se declara execução em PHP 8.3.0 exato ou em outros navegadores.

A base serve à reprodução e à migração; a versão operacional final é 0.31.0. Não há matriz histórica nem procedimento de downgrade.

## 2. Convivência e encaminhamentos

Os anexos foram conferidos por cabeçalho interno, raiz e SHA-256. O conjunto abaixo foi usado nas bancadas completas, incluindo instalação limpa, atualização e navegador.

| Pacote | Versão fornecida e testada | SHA-256 do instalador |
|---|---|---|
| Site Core | 1.72.1 | `3d13dfc96c6dec31221dbe989bdbee27beedbcf98719be0a0447bba7078242f6` |
| MCP | 0.41.0 | `4a31d22788d66b9342efdc25d4b75d919efa4320035bc607c0b396691ca783e5` |
| LinkedIn | 0.19.0 | `613cb47cfb3be2b91dfa1f20f39c465780a6fffb5432b645290448fe592a0f0c` |
| Meta | 0.21.0 | `9589456a2ee5ed13cb72941437e4350c0815907f6ba20b8eb47837a77064334a` |
| Pipedrive | 0.7.0 | `8f58b26c8408c02604c16bcfd30fcb92e3bbae308ebc107defad21555e5b5779` |

**Mudança concorrente observada:** o inventário imediatamente anterior à instalação Google ainda tinha Core 1.72.1/Pipedrive 0.7.0. Na primeira leitura posterior, apareceram Core **1.73.0** e Pipedrive **0.8.0**. A operação desta rodada substituiu somente o Google. Após detectar a mudança, foram feitas leituras de saúde, catálogo, diagnóstico e documentação; nenhuma nova mutação foi executada no ambiente compartilhado por esta rodada.

O Core 1.73.0 foi obtido depois, seu relatório foi lido e os arquivos modificados foram comparados à 1.72.1. Instalador: 4332427 bytes, SHA-256 `6675c1e7436e1195f6f7559a9baf62e049d871d145c84f19c04ac67f8d25655e`. Uma bancada adicional com Google 0.31.0, MCP 0.41.0 e Core 1.73.0 executou 37 verificações, sem os outros acompanhantes. Esse recorte complementa a prova remota do conjunto final; não é uma nova matriz completa com Pipedrive 0.8.0.

**Sem relatório individual de impacto.** A causa do item 49 está no callback de permissão do Google. Foram examinados `Discovery::eligibility`, `AuthorizationPolicy::check` e a decoração `AbilityRuntime` do MCP 0.41.0. O MCP original permanece aplicando o perfil da conexão; não é preciso alterá-lo. Foram comparados **610 schemas**, correspondentes às entradas e saídas das 305 operações: nenhuma mudança. Autorização, política por ativo, armazenamento e interfaces consumidas pelos acompanhantes permanecem vigentes. Não há ordem especial de troca exigida pela correção Google.

## 3. Mudanças e evidência

| Pedido | Problema | Mudança e prova |
|---|---|---|
| **Pedidos MCP Google 49** | A descoberta do MCP verifica `permission_callback` quando não há campo obrigatório. Ideias aceita sementes alternativas ou retomada. Com Ads desligado, o callback Google recusava a habilidade, que desaparecia do catálogo. As outras três consultas tinham campos obrigatórios e apareciam, embora também perdessem o diagnóstico na execução. | As quatro consultas optam internamente por permissão de diagnóstico: canal aberto, administrador e capacidade adicional continuam exigidos. O gate Ads executa antes do callback e recusa serviço desligado com `f3_google_connector_off`. Descoberta/informação/execução reais no Site-Teste confirmam o aceite. |
| Código e autorização | Uma indisponibilidade do serviço era tratada como recusa de permissão antes de o domínio explicar a configuração. | `Ability::register` aceita o opt-in somente em `mode=read`; `KeywordPlanner::register` o aplica às quatro consultas. Escritas e outras habilidades conservam o gate original. Perfis personalizados, canal fechado, usuário sem administração e seleção de conexão foram exercitados pelo MCP HTTP real. |
| UI de configuração | O campo de nível não explicava todos os estados nem a diferença entre declaração administrativa e comprovação de acesso. | Acesso ao Google Ads tem região nomeada, descrição próxima ao seletor e grupo de conferência MCP após o formulário. Test/Explorer/Basic/Standard e as cinco rotas são explicados. Inspeção visual e testes em 1440×900 e 390×844, sem transbordamento ou erro JavaScript nos estados medidos. |
| Testes e documentação | A regressão entre serviço desligado, descoberta e execução não tinha prova dedicada. | Dez casos unitários novos, cenários MCP reais, guia 0.31.0, planejador, migração, validação e notas da versão. Quatro casos falharam na base; todos passam no alvo. Documentação instalada e fonte editável correspondem. |

A solução preserva o schema de sementes (`keywords`, `url`, `site`, palavras com URL) e `resume_id`. Não foi acrescentado campo obrigatório artificial. Descobrir uma rota não concede acesso à conta Google. As consultas continuam sujeitas a credencial, seleção de serviços, política de ativos e nível do projeto, e só arquivam resultados depois desses gates.

## 4. Instalação e prova da troca

Ambiente: `https://fator3-teste-mcp-1.dreamhosters.com/`, via WP MCP fator3-teste. Instalador final transferido por `plugins/upload-base64`, com `activate:true`, `overwrite:true`, `expected_slug:wp-mcp-google-fator3`, `expected_sha256` da seção 8 e chave idempotente da rodada.

Operação **`9d5b1cb6df2fc3902964f489edd6acf7`**, pré-imagem de arquivos **`18f2d29939117bdfab3f1738`**. Recibo: 0.30.0 → 0.31.0, ativo antes/depois, `applied:true`, hash exato, reativação silenciosa em requisição PHP nova e worker independente. `/` e `/wp-json/` responderam HTTP 200 antes e depois, em sondas internas à origem com cache contornado. Não se infere delas acesso público externo ou prontidão comercial.

Aceite remoto do pedido 49:

1. `discover-abilities {"prefix":"ads/keyword","per_page":20}` passou de quatro para **cinco rotas**, todas da 0.31.0.
2. `get-ability-info` de `ads/keyword-ideas` devolveu schema e metadados de leitura.
3. `ads/keyword-ideas {"url":"https://www.engagia.com.br/"}` devolveu **`f3_google_connector_off`** no resultado do domínio, com instrução para ativar Ads. O transporte externo o apresenta como `INVALID_ARGUMENT`; o erro interno comprovado é o do conector desligado, sem recusa de perfil.
4. `system/health`: `healthy:true`. `google/readiness-status`: armazenamento, recuperação, executor, incidentes e Core aprovados; bloqueio somente pela ausência de credencial Google. Ads permaneceu desligado e nenhuma conta foi conectada.

| Prova da candidata | Resultado | Evidência no fonte |
|---|---:|---|
| Suíte unitária | **1304 testes, 15501 asserções**, zero falhas | `evidence/031/unit.json`, `unit-junit.xml` |
| Instalação limpa isolada e regressão local | 116 verificações | `evidence/031/isolated/` |
| Conjunto completo dos anexos e planejador | 175 verificações | `evidence/031/current/` |
| Migração direta, descoberta e documentação | 163 verificações | `evidence/031/upgrade/` |
| Navegador e verificações de persistência | 50 verificações, incluindo três ativações de acompanhantes | `evidence/031/browser/` |
| Conferência adicional com Core 1.73.0 | 37 verificações | `evidence/031/late-core/` |
| Sintaxe, contratos e pacote | 179 PHP da allowlist; 610 schemas idênticos; 202 arquivos de runtime; ZIP reproduzido byte a byte | `lint.json`, `schema-parity.json`, `installer.json`, `runtime-diff.json` |

São **541 verificações adicionais** nas cinco bancadas, além da suíte unitária. A soma inclui regressões repetidas em cenários distintos; não representa 541 casos únicos. Sete verificações de reprodução da base ficam fora desse total. Uma repetição de 17 verificações da atualização corrigiu apenas o rótulo herdado do teste de origem e também não aumenta o total. Os JSONs identificam versão, runtime e SHA do candidato. Os processos dos laboratórios foram encerrados. As advertências WordPress.org nos logs privados decorreram do bloqueio de HTTP externo das bancadas.

Documentação: **25 documentos completos pelo transporte MCP local**, com paginação, revisão, recusa de caminho arbitrário e autorização. No Site-Teste, os 25 nomes/tamanhos/hashes do índice coincidiram com o pacote. Foram lidos integralmente **GUIA-0.31.0.md, PLANEJADOR.md, README.md e MIGRACAO.md**, em oito páginas, com bytes idênticos ao fonte. O guia tem 10576 bytes e SHA-256 `b4f84bf9a75c487cc2e615256d6b261598fa8fad8af0293fce3238df85dfcb37`. A continuação usou `expected_revision`.

Estado final observado: Google 0.31.0, Core 1.73.0, MCP 0.41.0, LinkedIn 0.19.0, Meta 0.21.0 e Pipedrive 0.8.0, todos ativos. Não foram criadas fixtures, conexões, campanhas ou credenciais sintéticas no Site-Teste. Os testes com identidade fictícia ficaram em bancos descartáveis. Evidência remota sanitizada: `evidence/031/site-test.json`.

## 5. Banco, migração e correção por nova versão

Sem DDL, nova option de negócio, migração em massa ou ativação automática de serviços. A atualização local preservou configurações, revisões, credenciais cifradas, candidata OAuth, conexão adicional, job concluído e acervo cifrado do planejador. A leitura documental em novo worker confirmou a troca de versão e rejeitou a revisão antiga.

A pré-imagem remota cobre arquivos; não é backup integral do banco. Nenhuma configuração comercial foi gravada por esta implantação. Preserve banco e salts na recuperação de dados. Uma falha posterior exige nova versão; não há downgrade. Resultados externos incertos devem ser reconciliados pelos recibos existentes antes de nova tentativa.

## 6. O que permanece pendente

- **Dono/frota — fornecedor real e pendência 20:** executar o aceite do planejador em ctooffice.com.br com acesso Basic e a URL https://www.engagia.com.br/. O Site-Teste está sem credenciais; a recusa correta não comprova retorno de ideias reais.
- **Dono/frota — aceites anteriores:** acervos Ads/GSC comparados às telas dos fornecedores, chave real fora do padrão com aviso e OAuth em conta real permanecem pendentes. Esta rodada não os declara homologados com base em fixtures.
- **Conjunto concorrente:** Pipedrive 0.8.0 foi observado no Site-Teste, mas seu ZIP/fonte não estava disponível nas consultas de fontes durante o fechamento. A matriz local completa usa os anexos fornecidos; Core 1.73.0 tem a prova adicional descrita. Não foram retestadas todas as funções comerciais dos acompanhantes.
- **Frota — distribuição:** publicação raw e implantação nos demais sites não foram executadas. Publique os artefatos autorizados, confira o SHA-256 dos bytes servidos e use `plugins/upload` com `expected_slug`/`expected_sha256`. A versão instalada permanece imutável.
- **Escopo visual/runtime:** inspeção em Chrome nas duas larguras indicadas; sem certificação em outros navegadores, leitor de tela ou PHP 8.3.0 exato.

O aceite do item 49 no **Site-Teste** está comprovado. O aceite com Google Ads real em ctooffice.com.br permanece para a operação autorizada nesse ambiente.

## 7. Credenciais e configuração do dono

Nenhum segredo novo é necessário para instalar. Para usar o planejador, selecione a conexão em **Ferramentas → Fator3 MCP Google**; prepare e ative a identidade em **Conexão → Identidade**; em **Serviços e recursos**, configure Ads, conta alvo e token de desenvolvedor, MCC quando necessário e nível do projeto. Basic/Standard permitem planejamento; Test exige conta de teste; Explorer/Não informado impedem as consultas.

O canal Google deve estar aberto e a conexão MCP deve permitir a operação. `manage_options` e eventual capacidade adicional continuam obrigatórios. Informe credenciais somente nos campos próprios. A presença no catálogo e a declaração do nível não substituem validação de acesso ao fornecedor.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-google-fator3-0.31.0-instalador.zip](wp-mcp-google-fator3-0.31.0-instalador.zip) | 947286 | `e577dd444b063d99e42a4c63840095d9f176f82bd864e21d09c76a877d9e670e` |
| Fonte | [wp-mcp-google-fator3-0.31.0-fonte.zip](wp-mcp-google-fator3-0.31.0-fonte.zip) | 7886524 | `70d788ba1f4213359fdd99a380fcf747d7fd2eacb5659f1d5997797b2087222b` |

Relatório externo canônico: `wp-mcp-google-fator3-0.31.0-relatorio.md`. A cópia interna é anterior ao fechamento do fonte; os bytes/hash finais desse ZIP são preenchidos somente no relatório externo. Fonte com raiz única, runtime idêntico ao instalador, testes, geradores, documentação editável e evidências sanitizadas. Nenhum ZIP contém outro ZIP; nenhum banco, cookie, log privado ou ferramenta ativa de QA integra o instalador.

Checklist da seção 14 conferido: normas/revisões, base/alvo, mínimos, identidades, contratos, escopo dos impactos, autorização, documentação instalada, instalação limpa, atualização, preservação, hashes, empacotamento e estado final. As pendências da seção 6 permanecem explícitas. O fluxo raw/frota não foi usado nesta implantação direta; a transferência do instalador foi conferida pelo SHA-256 do recibo.
