# Fator3 MCP 0.22.0 — implementação e validação

Data: 15/10/2026. **Candidata implementada, com validação real ChatGPT pendente (B22).** Não houve implantação em produção nem publicação de feed. O código inclui MCP-03 nesta release.

## Atualização direta solicitada

A base efetivamente instalada nos ensaios foi **MCP 0.21.0 + Core 1.31.0 + Google 0.8.5**. Foram executadas, em bancos descartáveis distintos, estas sequências:

| Ordem | Primeira troca | Segunda troca | Resultado |
|---|---|---|---|
| MCP primeiro | MCP 0.21.0 → 0.22.0 | Core 1.31.0 → 1.33.0 | 33 verificações aprovadas |
| Core primeiro | Core 1.31.0 → 1.33.0 | MCP 0.21.0 → 0.22.0 | 34 verificações aprovadas |

As trocas usaram os ZIPs originais, rota tipada e HTTP autenticado. Uma nova requisição verificou cada versão. Quatro workers PHP-FPM aquecidos, com OPcache e `validate_timestamps=0`, terminaram executando a candidata. O runtime independente MU foi conferido por hash.

**MCP 0.21.1 e Core 1.32.0 não foram instalados e não são etapas da atualização.** O fonte MCP 0.21.1 foi aproveitado como base de desenvolvimento das limpezas já preparadas; isso não implica instalar esse pacote. Não há bloqueio de instalação por presença, ordem ou versão dos companheiros. Dados correntes da 0.21.0 permanecem utilizáveis sem importação histórica.

Foram preservados clientes DCR, tokens válidos, concessões, perfis, revogações, senhas de aplicação, sessão atual, backup, confirmação SQL pendente, recibo de idempotência e seleção de retenção. Também permaneceram as credenciais/configurações Google, conexão não padrão, job concluído, agenda pausada e auditoria. O refresh emitido antes da troca renovou após a atualização; sua reutilização revogou a família. O hook de ativação inicial do Core já ativo não se repetiu.

## O que mudou

- **Ativação:** diário assinado distingue `native_activation` para plugin novo/inativo de `silent_reactivation` para atualização ativa. Hook concluído, estado ativo, saúde e prontidão funcional são provas separadas. Timeout/fatal com efeito incerto permanece pendente; reconciliação não repete o hook. Falha nativa comprovada permite restauração dos arquivos, sem alegar reversão dos efeitos no banco.
- **OAuth/CIMD:** lista plural válida negocia a interseção com o único método implementado, `none`. O documento atual ChatGPT, com singular `private_key_jwt` e plural contendo `none`, é aceito. Plural malformado não recebe fallback. Sem plural, singular `none` funciona; sem ambos, a política local assume cliente público `none`, conforme documentado. Token endpoint, descoberta e persistência usam o mesmo método efetivo.
- **Diagnóstico:** categorias distintas para cliente indisponível, busca, documento inválido/inseguro, método incompatível e persistência. ID opaco correlaciona resposta a uma fila privada de até 128 registros, sem tokens, códigos, segredos, documento ou URL completa da autorização. Falha do logger mantém a recusa.
- **MCP-03:** contrato `executor-registration/1.0.0` registra e admite bridges de qualquer provedor aderente. Exige identidade, metadados, modo e alvos explícitos; conjunto vazio autoriza zero. Perfil Personalizado precisa da bridge e do alvo. Proíbe execução aninhada e alvos de outro provedor. Contexto raiz vincula usuário, conexão e política e fecha mesmo em exceções. A antiga exceção nominal de autorização Google foi substituída pelo mecanismo comum.
- **Google 0.8.5:** adaptação delimitada declara as duas bridges pelo registro comum, preservando seus seis namespaces, nomes, schemas e grants. Declaração explícita inválida não ganha fallback. A declaração real da futura 0.8.6 permanece uma integração separada.
- **Distribuição:** contrato `package-distribution/1.0.0` publica registro, seleção local, manifesto explícito e guarda de revisão. Preserva MCP/Core/Google e aceita pacotes optativos. Canal MCP selecionado não cai silenciosamente para outra origem; filtros de pacotes não selecionados preservam o resultado anterior. Recibo público não expõe URL de feed. Upload manual mantém hash, staging, backup e prova.
- **Transporte:** preserva envelopes, nulos, zeros, erros parciais, cursores, cobertura e identidade efetiva. Resultado superior a 2 MiB falha explicitamente, sem corte apresentado como sucesso. `mcp.public:false` explícito é preservado e impede admissão de bridge privada.

Não foram adicionadas novas abilities de negócio próprias: permanecem 166 contratos exportados. Identidade/rotas atuais, contrato de política 1, esquema de dados 2 e `server-integration/1.0.0` foram preservados. Não foram alterados os pacotes Core ou Google.

## Evidência automatizada e ChatGPT

Ambiente: WordPress 7.1.2, PHP 8.3.6, MySQL 8.0.46, lighttpd/PHP-FPM, single-site. APIs externas foram bloqueadas ou simuladas. Fontes, testes e JSONs ficam no ZIP fonte, respectivamente em `fontes/`, `tools/release0220/` e `evidencias/0220/`.

A captura pública de `https://chatgpt.com/oauth/client.json`, obtida em 15/10/2026, foi usada na matriz de negociação. Como o PHP da bancada não resolvia o DNS externo, o cenário integrado substitui somente `client_id` por uma URL HTTPS controlada com IP público; o documento preserva os métodos e redirect ChatGPT. O percurso local passa pelo redirecionamento ao login WordPress, cookie de sessão sintético válido, formulário/nonce de consentimento, código S256, token, `initialize`, `tools/list`, leitura e refresh. Não é um login manual no navegador nem uma nova conexão real criada pela interface ChatGPT.

| Execução | Verificações | Resultado |
|---|---:|---|
| Matriz CIMD/cache/diagnóstico | 48 | Aprovadas |
| Percurso HTTP CIMD controlado | 24 | Aprovadas; `chatgpt_end_to_end:false` |
| Percurso HTTP DCR | 25 | Aprovadas; registro, consentimento, código, leitura e refresh |
| Ativação e recuperação | 12 | Aprovadas |
| Guardas do worker | 11 | Aprovadas |
| Instalação Google realmente nova | 5 | Aprovadas, sem manutenção reparadora antes da leitura |
| Bridges e transporte social | 37 | Aprovadas, incluindo laboratório sem Google |
| Ciclo/remoção de provedores e grants | 18 | Aprovadas |
| Registro, metadados e exceção de callback | 15 + 7 + 2 | Aprovadas |
| Declarações Google explícitas/adaptação | 7 | Aprovadas |
| Distribuição/origem/revisão | 16 | Aprovadas |
| Core/Google, duas ordens de carregamento | 22 por ordem | Aprovadas |
| Política da manutenção Google | 4 | Aprovadas |
| Suíte de integração do fonte Google 0.8.5 | 313 | Aprovadas com classes reais; inclui catálogo/metadados |
| SDK Core → Google | 26 | Aprovadas, respostas remotas simuladas |
| Isolamento de manutenção/cron | 6 | Aprovadas |
| Mutação e releitura pública Core | 7 | Aprovadas no escopo descrito em B29 |
| Exclusão tipada de termo | 4 | Aprovadas: prévia, backup, ausência e replay |
| Cabeçalhos de versão/companheiros inativos | 12 | Aprovadas; não certificam versões de negócio fictícias |
| Auditoria do instalador | 14 | Aprovadas; inclui lint dos 447 PHP distribuídos |
| Documentação e exemplos | 79 + 3 | Aprovadas; schemas Draft 2020-12/jsonschema 4.25.1 |

As contagens são verificações de cada suíte, não um total de cenários independentes. Evidências históricas não foram somadas. As duas atualizações diretas e a instalação limpa referenciam o SHA-256 do instalador final. A mudança final de visibilidade foi revalidada nas fronteiras afetadas, nos pacotes reais e nas atualizações diretas.

**Executado efetivamente com ChatGPT: nenhum teste de nova conexão nesta entrega.** B22 permanece pendente. A documentação oficial consultada foi https://developers.openai.com/plugins/build/auth. O diagnóstico recebido em 15/10, cujo DCR terminava no login, não foi contabilizado como teste desta candidata.

## Aceites B01–B35

O mapeamento abaixo é autoritativo. Alguns nomes internos reaproveitados nas suítes usam numeração antiga; avalie o cenário e o JSON, não apenas seu prefixo.

| Aceite | Estado e prova |
|---|---|
| B01 | Premissa reformulada pela instrução final: nenhuma instalação 0.21.1. Diagnóstico no fonte anterior e contador nativo na candidata; `activation.json`, `google-new-install.json`. Não se declara reprodução dinâmica da 0.21.1. |
| B02 | Validado: upload combinado de Google ausente, hook, canal e tabelas prontos antes de manutenção; `google-new-install-detail.json`. |
| B03 | Validado: inativo, idêntico, ativação explícita, substituição inativa e atualização ativa sem repetir hook; `activation.json`. |
| B04 | Validado nos cenários de hook lento/timeout, fatal após efeito, reconciliação e saída inesperada. Não é uma simulação de todas as falhas possíveis de infraestrutura. |
| B05 | Validado: token inválido/expirado/consumido, política/capability/hash alterados, lock concorrente e estado divergente; `worker-guards.json`. |
| B06 | Validado para a base solicitada 0.21.0, workers aquecidos e atualização direta. Percurso 0.21.1 dispensado pela nova premissa; `upgrade-*.json`. |
| B07 | Validado: backup/pré-imagem, rollback prévio sem aplicar, estado corrente e rollback real por falha comprovada. Efeito de banco da fixture permanece explicitamente. |
| B08 | Validado com Google 0.8.5: 281 abilities, nomes antigos ausentes, grants antigos insuficientes, bridge+alvo e manutenção limitada; `google-policy.json`. |
| B09 | Validado: duas ordens de carregamento em processos novos e HTTP; isolamento de manutenção/cron; `companions-load-*.json`, `isolation.json`. |
| B10 | Validado: configuração 4.0.0, redução/merge/objeto vazio/null, revisão, ator, SDK e conexão não padrão; `google/integration.json`, `google/core.json`. |
| B11 | Validado: MCP/Core nas duas ordens, estado Google preservado; `upgrade-mcp-first.json`, `upgrade-core-first.json`. |
| B12 | Validado: instalação limpa sem companheiros, companheiros inativos e cabeçalhos divergentes, sem gate de versão; `clean.json`, `metadata-*.json`. |
| B13 | Validado: confirmações, retenção, idempotência, revogações, backups e termo tipado; `upgrade-*.json`, `term-delete.json`. |
| B14 | Validado: inventário, rebuild determinístico, SHA, guia, schemas e sintaxe; `package-audit.json`, `documentation.json`, `schemas.json`. |
| B15 | Validado: plural ChatGPT, interseção vazia, plural inválido e legado; `oauth-metadata.json`. |
| B16 | Validado: identidade, URLs, redirects, tipos JSON, tamanho e URI de retorno; `oauth-metadata.json`, `oauth-http-cimd.json`. |
| B17 | Validado: somente `none`, recusa Basic/segredo/assertion, PKCE, recurso, consentimento, código único e refresh. Não implementa private_key_jwt. |
| B18 | Validado: categorias, ID, persistência falha, logger falho e ausência de marcadores sensíveis; `oauth-metadata.json`. |
| B19 | Validado: cache válido/vencido, teto, no-cache/no-store, falha de busca/gravação sem promover documento inválido. |
| B20 | Validado: DCR novo e estado da 0.21.0 preservado, refresh e reuso; `oauth-http-dcr.json`, `upgrade-*.json`. |
| B21 | Validado em HTTP automatizado com cliente controlado; cookie válido sintetiza a sessão WordPress. Sessão 2025-11-25 e modo stateless 2026-07-28 têm provas distintas. |
| B22 | **Pendente: nova conexão efetiva ChatGPT em endpoint de homologação. Impede homologação integral CIMD.** |
| B23 | Validado na fachada MCP: registro opcional, colisões, seleção/diagnóstico local sem HTTP, manifesto explícito; `distribution.json`. |
| B24 | Validado na fronteira MCP: seleção, origem não selecionada, falha sem fallback, guarda de revisão e upload manual. A adoção do recibo por Google 0.8.6, inclusive MCP ausente, permanece C01. |
| B25 | Validado com fixtures independentes Meta/LinkedIn, descoberta autenticada, metadados e ausência seletiva. Não certifica os produtos reais. |
| B26 | Validado com fixtures: leitura/escrita/Personalizado, grant nativo, seleção vazia, conta alterada, job de outro ator, revogação e simulação; `provider-lifecycle.json`. |
| B27 | Validado: nulos/zeros/erros/cursor/partições, `complete:true` sem promover garantia de cobertura e limite explícito de tamanho; `bridges-social.json`. |
| B28 | Validado: remoção seletiva de fixtures entre requisições, preservação dos demais e isolamento de pausa/manutenção dos pacotes reais. Atualização de produtos sociais reais depende C02/C03. |
| B29 | Validação delimitada: conteúdo alterado pelo MCP e HTML/cache/llms relidos no Core real. Yoast ausente foi recusado; noindex foi exercitado por fixture nativa. Não se declara escrita SEO positiva via Yoast. |
| B30 | Validado: registro e alvo genéricos, provedor ausente, listas inválidas/vazias, conflitos, metadados incoerentes e private flag; `registry-*.json`. |
| B31 | Validado: raiz autenticada, modo, bridge+alvo, identidade/política vigente, executor aninhado e alvo estrangeiro; `bridges-social.json`, `google-policy.json`. |
| B32 | Validado com Google 0.8.5 original e declaração consumidora fixture: deduplicação, precedência e inválido sem fallback; `google-declarations.json`. |
| B33 | Validado sem Google, dois provedores/ordens, consulta precoce, reentrância e callback que lança exceção. WordPress e capabilities nativas permanecem disponíveis. |
| B34 | Validado: revogação, mudança de política, remoção entre chamadas e fechamento após exceção. A autorização usa o registro comum. |
| B35 | Validado com Core 1.33.0 real: seis slots, 22 eventos, paginação/revisão, `data:null`, flags falsas e capability/grants; `companions-load-*.json`. |

## Integrações condicionadas e matriz

| Integração | Estado |
|---|---|
| C01 — distribuição Google 0.8.6 | Pendente: pacote consumidor indisponível; produtor MCP e fixture validados. |
| C02 — Fator3 Meta | Pendente: pacote real não fornecido. Fixtures não certificam apps/tokens/Instagram. |
| C03 — Fator3 LinkedIn | Pendente: pacote real não fornecido. Não se certifica Lead Sync ou ingestão comercial. |
| C04 — leitura Google externa | Pendente: nenhuma consulta a conta Google real executada. |
| C05 — bridges declaradas por Google 0.8.6 | Pendente: pacote não fornecido. MCP-03 está implementado e validado independentemente dessa entrega. |
| C06 — medição Core 1.33.0 | Validado no transporte e SDK local. Não certifica emissão no navegador, recebimento remoto ou todos os aceites próprios do Core. |

M01: MCP limpo e Google realmente novo por upload combinado. M02/M03: adaptadas à instrução final para as duas ordens MCP/Core partindo de 0.21.0/1.31.0, com Google 0.8.5; não foi ensaiada troca Google 0.8.4 → 0.8.5 nesta entrega. M04: origem MCP 0.21.1 dispensada, sem instalação intermediária. M05: conjunto final em bancada nova e duas ordens de carregamento. M06: fixtures sociais isoladas/conjuntas e remoção seletiva. M07: Core 1.33.0 real validado; demais candidatos condicionados acima. M08: bridges de provedores independentes em WordPress sem Google.

| Pedido | Entrega |
|---|---|
| MCP-01 | Implementado e validado: ativação, diário, incerteza e atualização ativa. |
| MCP-02 | Implementado e validado no produtor/fachada; adoção Google 0.8.6 pendente C01. |
| MCP-03 | **Implementado nesta 0.22.0**, com registro/admissão/autorização genéricos e transição Google comprovada. |
| MCP-04 | Documentação e transporte implementados/validados; limites externos e SEO descritos. |
| MCP-SOC-01 | Fronteira MCP validada com fixtures; homologação dos produtos reais pendente C02/C03. |

## Limites, instalação e continuidade

Atualize por substituição do pacote, sem desinstalar nem limpar opções, concessões ou tabelas. Não instale intermediários. Não há necessidade de nova autorização das conexões válidas por causa desta release; uma conexão CIMD que nunca concluiu deverá iniciar a autorização novamente após instalar a candidata. Não houve limpeza geral de cache ou reemissão de credenciais.

Os testes são single-site e sem cache persistente Redis/Memcached. Não houve ensaio de frota, multisite completo, tráfego remoto real, serviços Google/Meta/LinkedIn reais ou observação prolongada. Não se transforma um callback de ativação concluído em prova automática de prontidão de domínio.

As falhas encontradas durante o desenvolvimento foram corrigidas e reexecutadas: interpretação de objeto JSON como lista, adaptação incompleta dos namespaces Google, comparação de política sensível à ordem das chaves, incerteza após resposta 5xx promoção indevida de `public:false` e oferta MCP antiga após troca explícita de origem. Os ajustes de bancada (URL local explícita, opção sintética inicialmente ausente e cache da fixture de corrida) estão nos scripts. Esses incidentes não foram ocultados como validação externa.

Para fechar B22: instalar esta mesma candidata no endpoint de homologação escolhido, criar nova conexão CIMD pelo ChatGPT, concluir login/consentimento, código/token, initialize/listagem/leitura, registrar versão/hash e resultados sem segredos. Depois conferir conexão DCR existente e refresh. Nenhuma alegação de homologação integral deve ser feita antes dessa evidência.

## Identificação do pacote

- Instalador: `wp-mcp-fator3-0.22.0-instalador.zip`, 762.280 bytes, 455 arquivos, 447 PHP e 55 índices silenciosos.
- SHA-256 instalador: `622b75d20c3dc115bb8391d08f59c484ebbc6ac78547b8dac08b0f6b10e1fa7d`.
- Digest do inventário de runtime: `42206b96cd7ca9d6e1b580232212602fab4beeb080d4620c8e5de7f25a1cf21d`.
- Insumos originais e hashes: `docs/ENTRADAS-TESTE.json`.
- Reprodutibilidade: `tools/release0220/README.md`, `tools/build_packages.py`, `tools/check_package.py` e `tools/pack_source.py`.

Este relatório-base acompanha o fonte sem seu próprio hash, evitando circularidade. O relatório externo acrescenta a identificação do ZIP fonte; `SHA256SUMS-0.22.0.txt` confere os três artefatos finais.

## Insumos originais identificados

| Papel | Arquivo | SHA-256 |
|---|---|---|
| MCP base instalada | `wp-mcp-fator3-0.21.0-instalador.zip` | `6c1a788f6a11ad60b9fa53fda8a091ce11b74b1981f521c5d7d8c428fda47ce7` |
| Core base instalada | `base-site-core-fator3-1.31.0.zip` | `bd84d4d9f06d4ecda6340a483b04c5b39e386ab528b5d29a8803a266ffe0d6a8` |
| Core alvo fornecido | `base-site-core-fator3-1.33.0.zip` | `de427cb219be769d9e44ae9aaf5e6f31055990b3d8f9b8664ac0faa596f61364` |
| Google entregue | `wp-mcp-google-fator3-0.8.5.zip` | `acd644d1cd9d7a766c03cad9cdd3c67c44635d1b0b2b49936060a588316be96f` |

## Artefato fonte final

`wp-mcp-fator3-0.22.0-fonte.zip` — 2,565,319 bytes; SHA-256 `50ff0c8734a7c133561dc44d45256fa0923bc7735655a25b6792d469e69bfda8`.

Contém runtime, contratos, exemplos, ferramentas, testes, evidências e relatório-base. Dependências da bancada, bancos e credenciais locais não são distribuídos. O instalador reconstruído após extrair este ZIP é idêntico byte a byte ao entregue.
