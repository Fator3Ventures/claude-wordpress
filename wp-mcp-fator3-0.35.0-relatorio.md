# Entrega — Fator3 MCP 0.35.0

**Relatório externo canônico. A cópia interna do fonte antecede o fechamento. ZIPs imutáveis.**

Revisão 1 · 28/10/2026 · America/Sao_Paulo · Rodada: implementação.  
Slug: `wp-mcp-fator3` · Basename: `wp-mcp-fator3/wp-mcp-fator3.php`.

**Versão corrente: 0.35.0, instalada e ativa no Site-Teste. Status: com-pendencias.** O pedido de auditoria central comercial do LinkedIn foi implementado e validado localmente com os produtores originais. A instalação, o schema e a documentação foram confirmados remotamente. Permanecem os aceites de fornecedor real e o aceite gzip da frota já existente; não há correção de código conhecida pendente no escopo MCP testado.

## 1. Bases aceitas e entradas

Base direta **MCP 0.34.0**, preservada: instalador903878 bytes, SHA-256 `5d96b6a33cfc4a7c729c106268f4bc9d8938b34384da022345d7b7dae611a295`; fonte4720710 bytes, SHA-256 `4ae0f1bf02b65dae833ad08252be49c69685a76e7da26fb63182bf5f68b2c7b5`; relatório20198 bytes, SHA-256 `707c2823eb6bd514d17ce08f5ffc657f931a1d66a1fb2d304f3873ff7ff5a872`. Atualização direta0.34→0.35 comprovada, sem versão intermediária. O incremento minor segue a regra vigente para implementação.

Entrada nova: `wp-mcp-linkedin-fator3-0.12.0-impacto-wp-mcp-fator3.md`, revisão1, referência **Pedido Core323**. Documento de3632 bytes, SHA-256 `ea8cc39c32dc65ab2b7a3443ed0d3680195ccab869737db3b6de34a3f9c9b843`. Nenhum número novo de pedido MCP foi inventado. O anexo de pedidos MCP69–73 repete a rodada anterior; seus comportamentos e a pendência externa do70 foram preservados.

Foram examinados os instaladores, fontes e relatórios novos Core1.59.0, Google0.22.0 e LinkedIn0.12.0. Meta0.13.0 e Pipedrive0.3.0 mantêm as entradas aceitas anteriormente. Tamanhos/SHA-256 completos em `docs/entradas/0350/packages.json` e `evidencias/0350/inputs.json`. Normas comuns01/02 revisão5, preservadas da base aceita, prevalecem sobre as cópias avulsas revisão4 anteriores. Planejamento anterior ao código em `docs/PLANO-0350.md`.

Mínimos MCP mantidos: WordPress7.1.2/PHP8.3.6, 64 bits. Laboratórios: WordPress7.1.2 e7.1.3, PHP8.3.6, MySQL8.0.46, PHP-FPM/lighttpd. Site-Teste: WordPress7.1.3/PHP8.3.36. Pipedrive não foi ativado no PHP local8.3.6, inferior ao seu mínimo8.3.36.

## 2. Convivência e encaminhamentos

| Pacote | Versão considerada e observada ativa no Site-Teste | Cobertura própria desta rodada |
|---|---|---|
| Site Core | 1.59.0 | Produtor comercial real nos testes LinkedIn; configuração, política, correio sintético, permissões, descoberta e convivência na atualização |
| Google | 0.22.0 | Insumos, contratos e código da fronteira examinados; carregamento/descoberta com a matriz nova; reconciliação comercial não rehomologada pelo MCP |
| LinkedIn | 0.12.0 | Aquisição, serviço comercial, grants distintos, usuário zero, recibos, replay, autorização, leitura HTTP e painel; transporte LinkedIn sintético |
| Meta | 0.13.0 | Integridade do instalador aceito, carregamento/descoberta e inventário remoto; operações comerciais fora do escopo próprio |
| Pipedrive | 0.3.0 | Entrada aceita e inventário remoto; sem ativação local ou chamadas ao fornecedor |

Também permaneceram ativos DreamHost Panel Login1.0.0, WP Super Cache3.1.4 e Yoast SEO28.8. Nenhum acompanhante foi editado, instalado ou rebaixado nesta rodada MCP.

| Instalador acompanhante | Bytes | SHA-256 |
|---|---:|---|
| base-site-core-fator3-1.59.0-instalador.zip | 2825862 | `8f3992e89b44f53a59e0e2af314ff8548fe2aadfcc06afe30e395610b1b7c832` |
| wp-mcp-google-fator3-0.22.0-instalador.zip | 856534 | `a84754409f89b7b9c7367c1d261c44ef93c2f6039b379c3ec5c6242ec7188ebd` |
| wp-mcp-linkedin-fator3-0.12.0-instalador.zip | 304948 | `19748e788190f371809db469a6de052a645e25f39fad1672606dc776234ec54c` |
| wp-mcp-meta-fator3-0.13.0-instalador.zip | 284069 | `3ecd6ee6f277c7581adc05b4fa38c46611e3232b4400bb4a4421956c9fba8ac1` |
| wp-mcp-pipedrive-fator3-0.3.0-instalador.zip | 59877 | `30fc784a552a89351900c169fad7300759163fb886b842f45ba807bb0977f657` |

### Impactos novos emitidos

Nenhum. A alteração admite o consumidor que o LinkedIn0.12.0 já publica no schema do leitor e no contrato de serviço. Não requer mudança em outro pacote. Foram examinadas as fronteiras de identidade, auditoria, autorização, deduplicação, documentação e atualização. Essa conclusão não homologa todas as operações dos acompanhantes. O atendimento do impacto recebido é registrado abaixo, sem reemitir um documento apenas para encerrá-lo.

### Tratamento de impactos recebidos e anteriores

| Referência original | Resultado e evidência | Responsável / limite |
|---|---|---|
| LinkedIn0.12→MCP, revisão1, Core323 | **Atendido no código MCP0.35.0 e validado localmente.** Mesma suíte original registra ausência de recibo na0.34; expectativa adaptada confirma `recorded` na0.35. Mais45 checks próprios cobrem os critérios de aceite. Schema e leitor registrados no Site-Teste. | MCP. Não equivale a conversão aceita por uma conta LinkedIn real. |
| Core1.59 / Google0.22, Core323 | O Core recebido incorpora a reconciliação Google `site-stage-conversion-reconcile/1.0.0`, sem novo envio. Relatórios/fontes examinados; nenhuma adaptação MCP adicional necessária. | Implementação e testes comerciais declarados pelos mantenedores; não contados como testes próprios MCP. |
| Google39/Core316 | Os relatórios Google0.22/Core1.59 informam consumidor enhanced1.1 implementado no Core1.58. A antiga pendência de código não é repetida como aberta. | Primeiro aceite real Enhanced Leads continua com o operador. |
| MCP0.32→Core, revisão1, Core300 | Correção anterior do permission_callback preservada na matriz atual;8 checks de permissão e32 de correio sintético passaram. | Core/MCP. Nenhum e-mail real enviado. |
| MCP67/68 e Core301 | Redação e legibilidade anteriores preservadas:479 unitários e regressões HTTP pertinentes. | Escopo documentado pelas suítes, sem ampliar exposição de segredos. |
| MCP69–73 | Regressões41+33+4+4 aprovadas; sem nova implementação desses itens. | Pedido70 ainda exige aceite de `.gz` nas últimas24h em site autorizado da frota. |

O relatório Core1.59 recebido registra bloqueio de instalação naquela sessão. **O inventário atual desta rodada já encontrou Core1.59 ativo antes da troca MCP e confirmou a mesma versão depois.** Isso atualiza a observação de instalação; não atribui ao MCP a instalação do Core nem comprova seus aceites comerciais pendentes. Meta20(e) e demais demandas de outro mantenedor mantêm seus desfechos no relatório daquele pacote.

## 3. Mudanças e evidências

### Auditoria comercial

`MutationServiceAudit::identity_schema()` passa de um consumidor para uma enumeração explícita de dois: `site-core-conversions` e `site-core-quality`. O schema compartilhado rege a validação do evento, a confirmação do recibo e a entrada de `audit/get-service-operation`. O painel existente já preserva `consumer_id` na consulta e no rótulo, sem remapeamento para aquisição.

Mantidos: provider exclusivo `wp-mcp-linkedin-fator3`; contratos `mutation-service-audit/1.0.0` e `linkedin-service-mutation/1.0.0`; descritor exato de seis campos; origem física dos pontos públicos; hook/leitor/introspector; identidade de cinco campos e evento de dez campos; hashes/ref opacos; concessão/revisão corrente; prova do evento; digest persistido exato; administrador, perfil e propriedade no leitor. Não há registro remoto de descritor nem ability para emitir eventos artificialmente.

O serviço pode emitir como usuário WordPress zero, mas isso não lhe concede leitura administrativa. O Registro mantém só referência técnica; before/after são consultados no leitor autorizado do produtor. Nenhum payload, contato, hash de e-mail, `li_fat_id`, token ou segredo novo é armazenado na referência central. Replay confirmado ou incerto mantém o diário e não repete HTTP/hook nem cria outra referência. Eventos anteriores não são importados nem reenviados automaticamente.

Comparação integral do instalador com0.34.0: **467 arquivos, nenhum acrescentado ou removido, quatro alterados**: `wp-mcp-fator3.php`, `includes/MutationServiceAudit.php`, `includes/guide-content.php` e `includes/guide-documents.php`. A mudança funcional é a enumeração; os outros arquivos atualizam versão e documentação. Manual corrente, contrato de auditoria e notas0.35 foram atualizados, inclusive referências antigas de versão-base do manual.

### Testes executados

**959 checks aprovados, zero falhas no fechamento**, em25 arquivos de resultados. São asserções/checks agrupados pelos respectivos ensaios, não959 integrações comerciais independentes. Reexecuções de uma suíte não foram somadas novamente. A linha de base e os checks de pacote são contados separadamente.

| Grupo | Checks | Evidência em `evidencias/0350/` |
|---|---:|---|
| Unitários de redação/política e Pedido68 | 479 | unit.json, policy-unit.json, unit-68.json |
| Política, redação, correio, permissões e OAuth HTTP | 167 | policy-http.json, http-68.json, provider-mail-permissions.json, mail-http.json, redaction-http.json, oauth-regression.json |
| Transporte/recusa, idempotência, mídia, descoberta, busca, admin nativo e documentos | 125 | adversarial.json, idempotency.json, media-http.json, discovery.json, guide-search.json, native-admin.json, docs-http.json |
| Pedidos69–73, adversariais, concorrência e artefatos de cache | 82 | integration-69-73.json, adversarial-69-73.json, concurrency-71.json, cache-artifacts-73.json |
| Serviço comercial próprio e suíte LinkedIn/Core recebida | 69 | service-commercial.json, candidate-stages012.json |
| Instalação limpa mínima e atualização direta | 37 | clean-activate-7.1.2.json, clean-readback-7.1.2.json, upgrade.json |

`test-summary.json` enumera as25 suítes. Adicionais: **24 checks de linha de base**, **15/15 checks de pacote**, **456 arquivos PHP aprovados no lint**. O verificador também rejeitou ZIPs com runtime ausente, teste/tool intruso, arquivo adulterado ou raiz errada; reprodução do instalador aprovada.

A reprodução inicial usou MCP0.34, LinkedIn0.12 e Core1.59 originais: o envio sintético foi aceito, a introspecção foi válida e a ausência de recibo central comercial ocorreu como previsto (`service_record_unconfirmed`). Na0.35, a cópia `stages035.php` muda apenas a expectativa desse recibo para `recorded`; o teste original permanece preservado. Ambos têm24 checks agrupados. Essa mudança de expectativa está explícita e não remove casos negativos.

O ensaio próprio comprova aquisição anterior, duas concessões comerciais, usuário zero, digest persistido, leitura central, painel renderizado, recusa a outro administrador, usuário zero, consumidor/ref/revisão/operação adulterados, evento excedente, digest divergente e concessão revogada. Cobre replay entregue/incerto sem nova chamada remota, perfis incompletos e leitura MCP autenticada de uma terceira concessão criada pela habilidade pública decorada do produtor. As fixtures foram ajustadas para usar essa fronteira pública; nenhuma permissão do runtime foi relaxada.

WordPress, plugins e persistência são reais nos laboratórios; **o transporte dos fornecedores é sintético e e-mail é interceptado**. O teste do painel verifica HTML e dados técnicos, sem homologação visual em navegador. As regressões reutilizadas foram executadas na matriz atual; resultados históricos presentes no fonte não entram na contagem desta rodada.

## 4. Instalação, documentação e prontidão

### Bancada

Instalação limpa WordPress7.1.2 sem acompanhantes: ativação nativa em processo separado, versão/atividade, cron, documentação, descoberta, execução e saúde HTTP aprovados;467 arquivos iguais ao ZIP. Upgrade0.34→0.35 em WordPress7.1.3: todos os workers observaram a nova versão, com OPcache sem validação automática de timestamps; preservados senha de aplicativo, OAuth e perfil, expiração/renovação, opções falsas/vazias, backup privado, recibos concluídos/incertos e confirmação SQL pendente. Recibo anterior reproduzido sem duplicação; cursor documental antigo recusado; prévia de rollback pronta.

### Site-Teste

Destino: `https://fator3-teste-mcp-1.dreamhosters.com/`. Instalado exclusivamente o MCP, pelo fluxo próprio de pacote, após as provas locais e conferência de SHA-256/slug. O estágio privado foi removido ao concluir, com guarda do hash. Nenhum controlador QA, concessão comercial ou fixture foi criado no site.

- Operação de pacote: `50935f9d3ffb851d8e94b06cb598d6d8`.
- Pré-imagem0.34 preservada: `c8dcabcdee9f9077e58a58a1`.
- Versão0.34→0.35, ativa antes/depois; requisição PHP independente confirmada.
- Sondas da raiz e `/wp-json/`: HTTP200 antes/depois, execução PHP nova comprovada, marca de teste. Evidência da própria hospedagem, sem alegar acesso externo/CDN.
- Saúde0.35: `healthy:true`, cron ativo/coerente, recuperação sem pendências. O resumo de incidentes declara cobertura parcial; não foi usado para afirmar ausência absoluta de erros.
- Descritor LinkedIn registrado sem erro; schema central e leitor do produtor admitem exatamente os dois consumidores. Consulta de identidade inexistente retorna `service_not_found`; consumidor arbitrário é recusado pelo schema, sem efeito.
- Prévia de rollback: `rollback_ready:true`, `preimage_verified:true`, `applied:false`. Não foi executada reversão.
- Acompanhantes e seus estados de atividade permaneceram iguais ao inventário anterior.

Evidências: `site-teste.json` e `site-teste-negatives-cleanup.json`. A atualização técnica não é prontidão comercial: o instalador declara `business_readiness_verified:false`. Nenhuma conversão real foi enviada para tentar alterar essa condição.

### Documentação instalada por MCP

`system/guide` foi consultado remotamente: **34 documentos,37 páginas,235630 bytes**, leitura completa com continuação e guarda de SHA-256. Todos os conteúdos, tamanhos e hashes foram comparados byte a byte com a documentação do instalador final; evidência em `site-teste-documents.json`.

Pontos correntes: `release-0350`, `mutation-service-audit`, `operacao` e schemas por Get Ability Info. A documentação distingue aquisição/comercial, emissão/leitura, autorizações, recibo persistido, falta de backfill, rollback e aceites externos. Referências a releases anteriores estão identificadas como histórico no manual.

## 5. Banco, reversão e preservação

Sem tabela, option, schema de dados ou migração nova. Schema MCP2 e contratos de serviço1.0.0 preservados; alteração aditiva da enumeração de consumidor. As referências comerciais usam o armazenamento e retenção existentes. Não há limpeza de histórico, novo segredo, concessão automática ou reprocessamento de fila.

Para voltar os arquivos à0.34, usar a pré-imagem da operação após prévia e conferência da pós-imagem atual. Referências comerciais já gravadas permanecem no banco, mas o leitor0.34 não admite `site-core-quality`. Retornar à0.35 torna essa interface disponível novamente, sujeito à concessão/propriedade corrente. Não apagar recibos nem trocar event_id para forçar reenvio.

Rollback de pacote não desfaz migrações arbitrárias, envio externo ou alterações de outro plugin; o recibo declara `database_effects_reversible:false`. A ausência de migração nova nesta versão MCP não altera essa semântica geral. Preservar banco, salts, diretório privado e diários dos produtores. O backup anterior à0.34 também não foi podado.

## 6. Pendências e limites

- **Operador/fornecedores:** aceite real de conversão comercial Google/LinkedIn, conta/ação/consentimento e primeiro Enhanced Leads permanecem externos. O pedido de código MCP está atendido, sem declarar esses aceites concluídos.
- **Pedido MCP70, frota:** conferir últimas24h em um site autorizado com `.gz` na janela após atualizar seu MCP. A rodada não instala nos outros sites nem encerra esse aceite.
- **OAuth/CIMD:**48 regressões locais passaram e a conexão existente permaneceu funcional. Não foi iniciado consentimento/CIMD externo novo do zero; o histórico B22 não é uma regressão nova demonstrada nesta versão.
- **Fora da matriz:** fornecedores reais, SMTP/IMAP real, multisite, Redis/Memcached, outros runtimes, inspeção visual de navegador, CDN externo e observação prolongada. A leitura comercial completa foi validada localmente; no Site-Teste foram verificadas instalação, saúde, schemas, registro do provedor, recusas e documentos, sem criar concessão real.
- **Demandas de acompanhantes:** implementação/limpeza e aceites fora do MCP permanecem com seus responsáveis. A observação remota Core1.59 não substitui o relatório ou as provas comerciais do Core.

**Nenhuma regressão observada nos cenários testados.** Isso tem o alcance das evidências descritas, sem garantia universal de ausência de impacto.

## 7. Credenciais e operação

A atualização não exige segredo ou escopo novo. O canal MCP não concede privilégios WordPress nem substitui a autorização do produtor. As concessões comerciais pertencem a identidades e ações específicas; usar os valores opacos efetivamente devolvidos pelo produtor, sem reconstruí-los.

Segredos reais, cookies, bancos de laboratório, logs brutos e helpers privados não integram os artefatos. Valores sintéticos usados nos testes estão identificados como tais. Preparação/instalação do próprio MCP foi autorizada pela rodada; não houve mensagens a terceiros, publicação GitHub, feed de atualização, implantação na frota ou alteração de pacote alheio.

## 8. Artefatos finais e estado de entrega

| Artefato | Nome exato | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador WordPress | wp-mcp-fator3-0.35.0-instalador.zip | 905542 | `cd6c3afacff83bf38678b9fa2aaf80881be02879b362a9bab250fc56c9969483` |
| Fonte | wp-mcp-fator3-0.35.0-fonte.zip | 4883759 | `70dd1ba0bac4900334ea843da50e4761f5c5a0f8a630fe5fca225758d151bb2e` |
| Relatório externo canônico | wp-mcp-fator3-0.35.0-relatorio.md | — | Não autorreferenciado |

Instalador: raiz única `wp-mcp-fator3/`,467 arquivos,456 PHP e56 índices de silêncio. Runtime digest `75ade4b2d36f70596df8f71648044ad6380901aa9e7c8e4995e875ac7b3bd787`. Nenhum teste, fixture, ferramenta, evidência, fonte documental separado ou ZIP aninhado no instalador.

Fonte: raiz única `wp-mcp-fator3-0.35.0-fonte/`; código distribuído, documentação editável, ferramentas de reprodução, testes e evidências sanitizadas. Nenhum ZIP contém outro ZIP. A cópia interna `wp-mcp-fator3-0.35.0-relatorio-base.md` foi fechada antes do ZIP fonte e identifica essa condição; seu próprio hash/tamanho não é inserido no arquivo que o contém. Após congelar o fonte uma única vez, ele foi reextraído em outra pasta; o instalador reconstruído conferiu byte a byte com o ZIP final instalado no Site-Teste. CRC e raiz do fonte aprovados.

Estado final: MCP0.35.0 corrente e ativo no Site-Teste; estágio desta instalação removido; pré-imagem mantida; acompanhantes preservados; entregáveis identificados e congelados. Instalar somente o ZIP instalador, depois conferir versão, saúde, esquema e documentação. Distribuição à frota segue seu fluxo próprio.
