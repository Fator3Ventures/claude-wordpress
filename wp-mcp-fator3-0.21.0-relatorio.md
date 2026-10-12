# Fator3 MCP 0.21.0 — relatório de implementação

**Resultado:** versão implementada e empacotada, com pedidos 56–59, correção de cron e consideração do plano Google 0.8.4. A exclusão tipada de termos do pedido 46 permanece disponível e passou na regressão. Nenhum site da frota foi alterado.

**Validação executada:** 360 verificações funcionais passaram, sem falhas finais; 84 verificações de coerência documental, 14 verificações do pacote e lint dos 444 arquivos PHP também passaram. São contagens separadas: não se somam os 444 arquivos como cenários funcionais. Há 47 cenários do plano ligados às suas evidências em `evidencias/acceptance021.json`. O consolidado com as contagens por suíte está em `evidencias/release-validation021.json`.

## Alterações entregues

| Demanda | Comportamento da 0.21.0 | Evidência principal |
|---|---|---|
| 56 — hierarquia Yoast | Preserva menor ID e referências sobreviventes a ele; apaga a hierarquia própria das duplicadas; recusa referências sobreviventes a IDs removidos e links não modelados | seo021, failures020, edges020 |
| 57 — indexable órfão | Nova `content/delete-orphan-seo-indexable`, com identificação por ID, duas fases, backup, verificação transacional e releitura de ausência | seo021 |
| 58 — poda seletiva | `artifact_ids` para backups comuns/legados; política com `exclude_ids`; seleção e corte congelados; bytes confirmados sem dupla contagem; referências revalidadas | backups021, retention-edges021, upgrade-http |
| 58 — prévia de rollback | `plugins/rollback dry_run:true` verifica prontidão e hashes sem restaurar; omissão conserva a aplicação existente, agora protegida também contra poda concorrente | backups021 |
| 59 — tokens | Filtra elegíveis antes do limite; conta remanescentes; preserva tokens válidos, expiração desconhecida e guardas de refresh; revalida revisões e grants | tokens021 |
| Cron | `mcp-cron-marker/2`: prova atual separada de histórico/intenção; ausência explícita; gravação com lock/recibo; sem recriação no bootstrap ou diagnóstico | cron021, cron-concurrency021, native-cron020, clean021, upgrade-http, upgrade-missing021 |
| 46 — termos | Rota de exclusão em duas fases, backup e ausência do termo/relações órfãs preservados | term-delete020 |

Arquivos runtime alterados: Backups, CronMarker, PackageService, Probe, Retention, SeoIndexables, StateMaintenance, SystemTools, TokenRetention, descrições em português, guia embutido e entrypoint do plugin. O instalador tem 453 arquivos; 441 são idênticos aos da 0.20.0. Não foram adicionadas classes runtime ou dependências.

## Plano Google considerado

A evidência fornecida para Google 0.8.4 é um **plano**, não o pacote final. Sua previsão de configuration 4.0.0 e cron.scheduling 2.0.0 foi incorporada à documentação e a 13 verificações de contrato. SDK server-integration/1.0.0, policy_contract:1 e execution 2.0.0 continuam sendo as referências de integração.

A ponte real Google 0.8.3 passou em 20 verificações. As 13 adicionais usam o handler/políticas MCP e a ponte real, substituindo somente os callbacks e schemas de configuração/status por fixtures sintéticas. Comprovam que o transporte conserva `dry_run`, `merge`, `confirm_service_reduction`, `expected_revision`, `expected_plan_hash`, recusas, conflitos, diffs e resultados not_applied. Não preenche confirmações nem desvia configuração local para google/prepare-operation. A simulação continua sujeita à autorização de escrita.

Os estados do executor, os erros atuais, os incidentes históricos e a saúde do trabalho Google permanecem distintos. Não há alteração do cron Google/Core. O catálogo registrado é a autoridade; nenhuma trava foi introduzida pela versão planejada ou por uma contagem fixa de abilities. Foram exportados 168 contratos MCP; a matriz instalada apresentou 123 abilities Core e 282 Google.

**Limite:** esses testes não homologam a implementação final Google 0.8.4. O pacote final requer releitura dos schemas e integração própria. Alterações apenas planejadas do Core 1.31.0 também não são declaradas homologadas.

## Bancada e provas

WordPress 7.1.2, PHP 8.3.6, MySQL 8.0.46, Yoast 28.5, Core 1.30.0 e Google 0.8.3. Banco/document root descartáveis, lighttpd e quatro workers PHP-FPM; OPcache habilitado com validate_timestamps=0. HTTP externo e correio bloqueados. Credenciais dos testes são sintéticas.

Três defeitos foram reproduzidos no código original 0.20.0: confirmação cron emprestada do histórico após ausência, aceitação de intervalo incorreto e primeira janela vazia de tokens com pendentes posteriores. Essa evidência está separada das verificações da candidata.

Foram executados dois escritores sobrepostos de histórico e dois processos nativos wp-cron. Na execução registrada houve um callback e uma ocorrência futura final; leituras não repetiram callbacks. Timeout de lock, SQL inválido, falha de gravação e overflow ficaram explícitos. O ensaio de isolamento por site usa tabelas separadas de options/state; não equivale a homologar uma rede multisite completa.

A correção de SEO foi exercitada com mãe e três filhas, referências ao ID mantido, ancestral externo de duplicada, dependências bloqueantes, objeto recriado, falha de backup/SQL e repetição de confirmação. Posts/metadados, linhas e hierarquia sobreviventes foram conferidos. A comparação do HTML completo normaliza somente tokens públicos do Core no formato timestamp.HMAC, que variam com o relógio; todos os outros bytes são comparados. Não foram usados os IDs ou dados dos sites reais.

A poda preservou envelope, árvore e diário da pré-imagem escolhida, inclusive por política de idade. A prévia de rollback permaneceu pronta; a restauração efetiva sem dry_run foi exercitada. Falha real de persistência após quarentena produziu resultado parcial e foi retomada pelo mesmo lote. Foram verificados bytes, componente alterado, referência nova, ID inexistente, categoria incorreta, cursor com exclusão divergente e inventário incompleto.

A atualização real 0.20.0 → 0.21.0 ocorreu por MCP HTTP com os bytes finais do instalador, incluindo rollback após falha deliberada, pool aquecido, senha de aplicação, OAuth, revogação, confirmação SQL pendente e plano de poda criado pela 0.20.0. Um ensaio separado comprovou agenda ausente após a atualização. Como a 0.20.0 recria seu marcador até em sondas anteriores ao upload, a fixture remove o evento apenas no runtime antigo; a 0.21.0 é então relida sem intervenção da fixture. Instalação limpa usa outro banco/document root e comprova ativação nativa e criação do marcador.

Falhas iniciais corrigidas na preparação dos testes: comparação literal incluía tokens dependentes do relógio; encerramento antecipado nativo wp-cron precisava de registro no shutdown para medir a sobreposição; a fixture Google exigia registro controlado e identidade sintética ainda válida; a bancada Core exigia sua migração nativa. As evidências finais refletem os testes corrigidos, sem atribuir esses problemas à frota.

## Operação e compatibilidade

Não há exclusão automática na ativação. Fazer nova prévia e confirmar explicitamente para SEO, termos e poda. Manter a pré-imagem até 18/10 continua sendo uma decisão operacional por ID, sem prazo embutido no plugin. Após aplicar um lote de tokens, repetir a prévia sem cursor para examinar os remanescentes.

O cron principal deixa de herdar `last_operation.status`; clientes devem observar `current_state`, intenção e prova atual. Limpeza com intenção inativa retorna status principal unobserved e absence.status confirmed. Erros nativos anteriores permanecem no histórico. Falha conhecida de gravação continua afetando a cobertura mesmo após uma gravação posterior bem-sucedida. Não se promete detectar um processo morto que não conseguiu persistir nenhum sinal.

Schema MCP permanece 2; URLs principal/alias, perfis, credenciais, guardas SQL e SDK são preservados. A prévia de rollback não desfaz efeitos de banco/hooks e a aplicação revalida as condições. Leitura de cron não repara agenda; ativação/desativação administrativas são transições explícitas.

## Entrega

Instalador: `wp-mcp-fator3-0.21.0-instalador.zip`, 761.272 bytes, SHA-256 `6c1a788f6a11ad60b9fa53fda8a091ce11b74b1981f521c5d7d8c428fda47ce7`.

Fonte inclui código, documentação canônica, schemas exportados, scripts de bancada e evidências JSON. Exclui runtimes baixados, bancos locais, credenciais e ZIPs defeituosos de teste. `tools/release021/README.md` registra dependências, ordem dos ensaios e limites de reprodução. O ZIP é determinístico e conferido contra manifesto fechado.

Não houve rollout, chamadas reais a serviços Google/Pipedrive, avisos Slack, teste de Redis/Memcached, matriz multisite completa ou monitoramento de sete dias. As provas são locais e não demonstram a causa dos incidentes originais de produção.

Pacote fonte: wp-mcp-fator3-0.21.0-fonte.zip, 2073905 bytes, SHA-256 `4f1acff8cd3a1d3018cc961b6d9362deb0c11f41b7bfb3f81d4fe869fbac32a3`.
