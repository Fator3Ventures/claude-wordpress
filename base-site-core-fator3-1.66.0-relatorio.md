# Entrega — Fator3 Site Core 1.66.0

Revisão: 1 · Data: 31/10/2026, America/Sao_Paulo · Rodada: implementação e correção
Slug: `base-site-core-fator3` · Versão: 1.66.0 · Build identificado pelo SHA-256 da seção 8
Status: apta no escopo testado; aceites de produção e metas anteriores de bytes pendentes.

## 1. De onde esta versão entra

Instalação limpa e atualização direta da **1.65.1**. A base publicada foi preservada: instalador de 4206718 bytes, SHA-256 `059d7da03484eb3d9eb7327f49787144466f451fcf51730ea0357d92c03f168a`. O fonte-base tem 8035411 bytes e SHA-256 `279b11eea6e273a0a42c93434fd44b3b6b75a21745139b30581672358eadadf5`. Não há versão intermediária.

Entradas: lista de frota `Fator3 Site Core(20261101-021708).md`, pacotes/relatórios Google 0.25.1, Meta 0.18.0 e LinkedIn 0.14.0, e impacto Google 0.25.1 para Core. Cópias textuais e manifesto de hashes estão em `inputs/1660`. A lista recebida encerra o 362 nos 12 sites e confirma 354(h–j) na 1.65.1; esta rodada trata os acréscimos 354(k,l) e os novos 363/364.

Requisitos comprovados: WordPress **7.1.2 e 7.1.4**, PHP **8.3.6** de 64 bits e MySQL 8.0.46 em laboratório. Site-Teste: WordPress **7.1.4**, PHP **8.3.36**. Ciclos nativos com WP-CLI 2.12.0. Cabeçalho, slug, basename, contratos e identidades de atualização preservados; a nova rodada incrementa a versão minor.

## 2. Convivência e encaminhamentos

| Pacote | Versão considerada | Evidência própria desta rodada |
|---|---|---|
| Fator3 MCP | 0.38.0 | Ativação local e canal MCP remoto de instalação, leitura e verificação. |
| Fator3 MCP Google | 0.25.1 | Ativação local; no Site-Teste, check `core` de prontidão voltou a `ok` e contexto de finalidades de conversão ficou legível. |
| Fator3 MCP Meta | 0.18.0 | Ativação local; 43 verificações com SDK e armazenamento originais, concessões/acervo sintéticos e transporte externo bloqueado. |
| Fator3 MCP LinkedIn | 0.14.0 | Ativação e convivência; extensão LinkedIn do contexto observada no Site-Teste. |
| Fator3 MCP Pipedrive | 0.5.0 | Ativo no Site-Teste; hashes preservados e conta confirmada pela pós-verificação automática. Inativo na bancada PHP 8.3.6 por exigir 8.3.36. |

Os acompanhantes não foram alterados ou redistribuídos. Seus hashes completos recebidos constam de `inputs/1660/packages.json`. Os cinco permaneceram ativos no Site-Teste.

**Impacto recebido do Google:** `wp-mcp-google-fator3-0.25.1-impacto-core(1).md`, correspondente ao encaminhamento 0.25.1 para Core. Resolvido pela projeção mínima compatível: o Core passa a emitir apenas os campos admitidos pelo contrato publicado. A correção está no instalador identificado na seção 8; a prova própria está em `request-363.json` e `site-test-receipts.json`.

Preservados: contrato administrativo **8.30.0**, `site-measurement-context/1.0.0` e `site-conversion-purposes/1.1.0`. Não se exige nova versão, alteração de consumidor, reconfiguração de tags ou ordem especial dos acompanhantes. Não foi identificado novo impacto técnico que exija encaminhamento individual; não foram emitidos arquivos apenas para anunciar a versão.

## 3. Mudanças e evidência

| Pedido | Correção entregue | Prova própria |
|---|---|---|
| **354(k)** | Cache entre requisições para o carimbo das raízes efetivas e do cabeçalho. Chave inclui SHA-256 do HTML, revisão de contato, superfície, versão e geração de invalidação. | Processos frio/quente independentes: uma análise de HTML na primeira execução e zero na segunda; mesmo hash de saída; invalidação por `save_post` seguida de nova análise. |
| **354(l)** | Bloco filho retorna imediatamente após ajustar a profundidade, antes de carregar configuração, calcular hash ou inspecionar filtros. | Fixture com 424 blocos filhos: uma raiz carimbada, profundidade final zero e todos os 424 links preservados. |
| **363(a)** | Projeção SDK sem `ga4`, `google_ads`, `gtm`, `clock` e `accelerate_conversion` nos campos que o schema 1.0.0 não admite. Configuração e execução das tags permanecem. | Fotografia completa validada; política em 49.152 combinações discretas e 180 variações individuais de prazo; leitura real deixou de retornar `unreadable`. |
| **363(b,c)** | Regressão do contrato e remoção de estratégia `defer` dos aliases sem `src`, inclusive aliases de consentimento/contexto. Arquivos físicos conservam sua estratégia. | 187 assertivas agregadas; alias sem estratégia e sem aviso; usuário anônimo sem permissão para executar a ability. |
| **364(a,b)** | Declarações dos sete grupos antes dependentes do bootstrap passam a compor o catálogo central antes dos filtros externos. | Primeira leitura antecipada e leitura final iguais; todas as 181 options do catálogo da fixture comparadas ao valor gravado em cinco contextos; 190 verificações por contexto. |
| **364(c)** | Resumo operacional avisa sobre nomes `f3base_*` gravados e não declarados no catálogo da requisição. | Nome desconhecido sem exposição de valor, guarda administrativa e aviso real `option_gravada_fora_catalogo` no Site-Teste. |
| **362, regressão** | Preservada a publicação dos ativos antes da confirmação do ciclo e das provas que geram cache. | 10 verificações locais e sequência real manifesto → confirmação → cópia pública no Site-Teste. |

**Cache de raízes:** usa cache de objeto; sem cache persistente de objeto, agrupa as raízes em um único transiente limitado a 128 entradas e 2 MiB. Cada entrada conserva sua expiração individual de até uma hora. Leitura do agrupamento uma vez por requisição; gravação agrupada no footer antes do relatório de desempenho, com alternativa no shutdown. `save_post` e mudança de `f3base_contato` invalidam a geração e descartam gravações pendentes da geração antiga. Escritas concorrentes podem reduzir o aproveitamento do cache, provocando nova análise; não tornam válido HTML de outra chave. Permanecem exclusões para contexto autenticado, administrativo, preview, conteúdo protegido, entrada acima de 1 MiB e erro do processador.

A fixture de 424 filhos mediu **95,528 ms fria** e **27,741 ms quente**; inclui renderização nativa da fixture, não equivale ao custo próprio do Core em fator3.com.br. SHA-256 idêntico de saída: `fc5f0253892477d1327a19014776c7d54106fa075682094b098a02f13baffb49`. As **64 comparações de HTML** existentes passaram novamente. Cache de `the_content`, contagem de profundidade, raízes e bytes por fase foram preservados.

**Escopo da matriz 363:** 4 modos × 6 destinos = 4096 combinações, multiplicadas por 2 estados de ativação, 3 referências de relógio e 2 estados de antecipação: **49.152**. Os prazos 1–30 foram verificados individualmente nos seis destinos (**180** casos). A política é a projeção que causava a incompatibilidade. A fotografia completa também é validada; não se afirma enumerar o produto cartesiano de todos os prazos.

**Escopo da matriz 364:** cinco inicializações WordPress em processos PHP de bancada, com leitura antecipada em `plugins_loaded` e marcação dos contextos público, REST, MCP, cron e CLI. Não são cinco chamadas externas reais. A leitura MCP real foi conferida separadamente no Site-Teste. Grupos centralizados: histórico de e-mail, acervo/estado GA4, acervo Google Ads, Meta Ads, monitoramento/estado Meta, prova SMTP e WhatsApp/estado. O perfil público foi regenerado; página estável continua sem abrir o catálogo completo.

O aviso de catálogo consulta somente nomes, limitado a 1001 linhas para detectar corte, examina até 1000, mostra até dez nomes e sinaliza resultado parcial. No Site-Teste apontou **21 nomes**, incluindo estados internos fora do catálogo declarativo; a lista de dez foi sinalizada parcial. Isso é diagnóstico de declaração, não prova de perda de configuração, e não apaga nem normaliza valores automaticamente.

Principais evidências em `evidence/1660`: `request-363.json`, cinco `request-364-*.json`, `request-354-roots-*.json`, `roots-*.json`, `request-354-cold.json`, `request-354-warm.json`, `request-354-depth.json`, `request-360-cta.json`, `request-362.json`, `meta-ads-1660.json` e `companions1660.json`. Só resultados finais aprovados integram a conclusão; testes históricos não são contados como reexecutados.

## 4. Instalação e prova da troca

Instalador com **909 arquivos**, dos quais **591 PHP** aprovados no lint PHP 8.3.6. O mesmo ZIP fechado foi usado nos dois WordPress e no Site-Teste.

| ID | Ambiente e cenário | Resultado | Evidência | Limite |
|---|---|---|---|---|
| N1 | WP 7.1.4 / PHP 8.3.6: instalação limpa | Primeiro cron nativo confirmou; repetição, desinstalação e reinstalação aprovadas. | `native-cycles-1660.json` | Bancada isolada, sem fornecedor. |
| N2 | Mesmo ambiente: atualização direta 1.65.1 → 1.66.0 | Dados/configurações preservados; confirmação nativa aprovada. | Mesmo arquivo | Não é reinstalação sobre a mesma versão. |
| N3 | WP 7.1.2 / PHP 8.3.6: ambos os cenários | Instalação limpa e atualização direta aprovadas. | `minimum/native-cycles-1660.json` | Piso declarado. |
| D1 | Documentação instalada em WordPress | 2048 assertivas booleanas; 173 documentos, 787 páginas de leitura; conteúdo/hash, confinamento e permissões aprovados. | `docs-1660.json` | As duas contagens de documentos/páginas não são assertivas. |
| R1 | Site-Teste: 1.65.1 → 1.66.0 | Instalação aplicada, ativo, sondas home/API HTTP 200 e recuperação sem pendência. | `site-test-receipts.json` | Sonda interna da mesma origem. |
| R2 | Site-Teste: ciclo e pós-verificação | Concluídos automaticamente; cabeçalhos, navegação e conta Pipedrive verificados. | Mesmo arquivo | Sem criar contato ou entrega comercial. |
| R3 | Site-Teste: documentação por MCP | Notas 1.66.0 e guia de agentes lidos integralmente; hashes iguais aos arquivos do ZIP. | Mesmo arquivo | Demais documentos lidos integralmente em bancada D1. |
| R4 | Site-Teste: limpeza | ZIP temporário removido com guarda de hash e backup; saúde final normal, `unresolved:0`. | `site-test-cleanup.json` | Não foi instalado componente auxiliar remoto. |

Operação de pacote: `5598520dc9289bc793f66541b29b072d`; pré-imagem `ee3da5bf827c7e088e731b3f`. Aplicação por `plugins/upload`, com `expected_slug:base-site-core-fator3`, ativação, sobrescrita, SHA-256 da seção 8 e chave idempotente. O endereço de estágio foi removido; **não há URL raw final publicada nesta rodada**. O instalador é entregue como arquivo. Publicação na frota segue a decisão do dono.

Confirmação no executor e manifesto vigente em **31/10/2026 23:38:10 −03**; artefato de cache servido com mtime **23:38:11 −03**, corpo correspondente ao artefato e referência `wp-content/f3base-publico/`. Pós-verificação concluída às **23:38:28 −03**. Esta sequência preserva a correção 362; não se instalou observador para registrar cada possível requisição intermediária.

Leituras funcionais reais:

- `f3base/medicao-contexto-ler`: antes `unreadable`; depois `ok:true`, contrato 1.0.0.
- `google/readiness-status`: check `core` com `state:ok/code:ok`. O estado global continua bloqueado pela credencial Google não configurada no Site-Teste, motivo independente do Core.
- `google/conversion-delivery-status`: `core_transport.ok:true`, finalidades 1.1.0 legíveis. Destinos deste site estão desativados; isso não é aceite GA4 de ctooffice.com.br.
- `f3base/config-core-ler` para `f3base_meta_ads`: antes `option_desconhecida`; depois option reconhecida e presente no banco. O Site-Teste não tem conta Meta selecionada; prontidão comercial não é afirmada.
- Hashes de contato, formulários, carregamento de destinos e Pipedrive iguais antes/depois.

Desempenho do Site-Teste por `f3base/desempenho-ler`, sondas sem cache de página, três amostras por rota:

| Medida | Amostra 1 | Amostra 2 | Amostra 3 |
|---|---:|---:|---:|
| Página — próprio Core (ms) | 53,374 | 59,122 | 52,983 |
| Login — próprio Core (ms) | 10,317 | 10,312 | 10,220 |
| `carimbar_bloco` na página (ms) | 1,955 | 1,830 | 1,881 |

Em cada página: 109 callbacks, 27 raízes efetivas, seis acertos de cache nas raízes, um no conteúdo, **zero parseamentos**, profundidade final zero, cinco consultas próprias e **zero aberturas do catálogo completo**. Login: zero consultas próprias e zero aberturas. A contagem de raízes inclui entradas sem link elegível, que retornam sem cache/análise. São tempos instrumentados de callbacks/carga, não TTFB nem diferença com/sem plugin. Não substituem as medições em fator3.com.br.

Bancada Core sozinho: páginas 5,579 / 5,660 / 6,023 ms; logins 0,369 / 0,318 / 0,129 ms, também sem catálogo completo. Preparação e aquecimento ficam identificados em `performance-1660.json`; não são apresentados como números de produção.

## 5. Banco e volta de versão

Sem nova tabela, coluna ou migração destrutiva nesta rodada. Dados de contato, seleção, concessões, configurações e acervos são preservados. Mudam os metadados do ciclo, os perfis derivados e os caches de CTA; o cache de raízes usa a família de transientes já pertencente ao Core. Nada é marcado como escolha do dono por mero preenchimento de cache.

Os ciclos nativos conferem preservação das estruturas históricas, retomada idempotente e comportamento de desinstalação: histórico mantido e trabalho pendente suspenso, sem repetir efeitos externos. Não se executou desinstalação no Site-Teste.

Volta de arquivos: pré-imagem registrada ou instalador canônico 1.65.1. Ela reintroduz as falhas 363/364 e a ausência de cache persistente de raízes. Restaurar arquivos não desfaz estado do executor, caches, dados ou efeitos externos. Caches derivados devem seguir a rotina de regeneração da versão ativa; não apagar options ou tabelas comerciais. Esta rodada não é prova de rollback comercial ponta a ponta.

## 6. O que permanece pendente

| Pendência | Motivo e responsável |
|---|---|
| **354: três amostras ≤100 ms em fator3.com.br** | Código k/l entregue; sem acesso a esse site nesta rodada. A frota deve aplicar o ZIP identificado e medir a página por `f3base/desempenho-ler` com três amostras, conservando as provas de HTML. Resultado do Site-Teste não encerra esse aceite. |
| **363: GA4 pronto em ctooffice e ausência de `core_context_unreadable` nos 12** | Correção do contrato e leitura real comprovadas; falta implantação/aceite da frota nas contas configuradas. Não alterar credenciais para satisfazer o teste. |
| **364: seleção Meta e conta/nome de campanha em korvena.com.br e ctooffice** | Catálogo e integração SDK testados; Site-Teste sem seleção comercial. Frota deve reler seleção gravada e simular o par `utm_campaign=utm_id=120256596454580242` nos sites indicados. |
| **Metas anteriores de 3 KiB e 20/30 KiB** | Continuam abertas no plano anterior. Esta rodada corrige PHP, contrato e catálogo; não houve nova redução dos assets nem medição de bytes no navegador. Responsabilidade do pacote, não encerrada por este relatório. |
| **Diagnóstico de nomes fora do catálogo no Site-Teste** | Aviso solicitado implementado e observado: 21 nomes, lista parcial de dez. Classificar estados internos/legados antes de eventual expansão do catálogo; não inferir perda de dados nem executar limpeza automática. |

Não foram reexecutados testes comerciais de mensagens, contatos, conversões ou todos os fluxos de navegador dos acompanhantes. Nenhum resultado sintético foi tratado como entrega ao fornecedor. O 362 foi encerrado pela frota na lista recebida; a regressão própria desta troca foi aprovada. Fonte/instalador/relatório estão prontos para a decisão de publicação, sem marcar os aceites de campo como concluídos.

## 7. Credenciais e configuração do dono

Nenhuma credencial nova, rotação ou alteração de segredo. Não é necessário regravar contato, destinos, seleção Meta ou Pipedrive para habilitar as correções. No Site-Teste, ausência de credencial Google e de conta Meta selecionada foi mantida como configuração observada. Nos sites com configuração comercial, usar as leituras das seções anteriores e as concessões existentes.

O relatório e as evidências de preservação usam hashes; não incluem segredos ou valores de contatos. O fonte exclui bancos, dumps, logs brutos, dependências instaladas, extrações dos acompanhantes e ZIPs aninhados. HTTP/e-mail comercial ficaram bloqueados nos ensaios locais.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `base-site-core-fator3-1.66.0-instalador.zip` | 4218989 | `0f796b2001478fe32e5ce47b5851f79148e6a1eebac7087c39a603a587692830` |
| Fonte | `base-site-core-fator3-1.66.0-fonte.zip` | 8187553 | `280a7fa4e706c5f1af3034bd1d11dc8dd466cf33958a4a33ebb4a24ad16b3b0c` |

Relatório externo canônico: `base-site-core-fator3-1.66.0-relatorio.md`. A cópia interna antecede o fechamento do fonte, evitando autorreferência do hash. O empacotador certifica igualdade dos 909 arquivos de runtime com o instalador testado e gera o manifesto do fonte. Os três arquivos constituem a entrega; não há novo impacto individual.

