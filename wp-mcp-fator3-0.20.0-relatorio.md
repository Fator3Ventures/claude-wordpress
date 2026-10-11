# Fator3 MCP 0.20.0 — entrega e validação

Data: 11/10/2026. Base: MCP 0.19.0. Escopo: plano revisão 5, pedidos 47 e 49–55, mais diagnóstico do marcador cron MCP. O pedido 46 foi preservado e teve regressão executada; a correção de pacotes do pedido 48 permanece vigente.

**Resultado:** nova versão implementada e empacotada. **372 verificações passaram, sem falhas**, além de lint dos **444 arquivos PHP distribuídos** e ativação do instalador final em banco/document root novos. O ZIP contém 453 arquivos, com 436 membros de runtime idênticos à 0.19.0, 13 alterados e 4 acrescentados. Rebuild determinístico e equivalência integral ZIP/fonte foram conferidos.

## Implementação por pedido

| Pedido | Implementação | Evidência principal |
|---|---|---|
| 47 | Reconhecimento restritivo do `.htaccess` exato com `mod_php.c`/engine off, preservando bytes. | Fixture de 205 bytes; aceitação/rejeição de regras e 30 verificações HTTP no Apache antes/depois. 403 permanece bloqueado; configuração 404 continua 404. |
| 49 | `users/update.user_nicename`, validação canônica, unicidade, lock e releitura. | Atualização, colisão, recusa de normalização e autenticação por login/e-mail preservada. |
| 50 | Backup/restauração de binários em fluxo, parser JSON estrutural, verificação de hash/identidade, índice reconstruível e referências duráveis. | Arquivos de 13.021.030 bytes e 32 MiB; exclusão de anexo com derivados/original, restauração dos três arquivos e reconstrução assistida do anexo/metadados. |
| 51 | Revisão canônica baseada em estado persistido completo, independente da representação do cache. | Patch/update → SEO em requisições HTTP independentes, para posts e páginas; revisão igual à releitura e conflito real preservado. |
| 52 | Rebuild sobre o modelo Yoast existente, com confirmação de identidade/contagem. | Vinte mudanças consecutivas, no-op, limpeza, bloqueio de indexação desabilitada e duplicatas preexistentes. |
| 53 | `content/update-term` com capacidades nativas, backup, revisão e duas fases para mudança de URL. | Nome/slug, ciclo de pai, seleção alterada, relações preservadas, permalink/breadcrumb do indexable e arquivo público com HTTP 200/BreadcrumbList. |
| 54 | `content/deduplicate-seo-indexables`, transação e seleção limitada, preservando menor ID. | Duplicatas criadas pelo comportamento do builder 0.19; limpeza, replay, conflito, dependências externas, falha de banco e HTML SEO idêntico antes/depois. |
| 55 | URL/ID de imagem social coerentes, associação local verificável, limpeza de IDs antigos. | URL apenas, ID apenas, incompatibilidade, mesma URL com ID ausente, URL externa e limpeza; HTML público com imagem PNG real de 1200×630, largura, altura e MIME. |
| Cron | Agenda/diagnóstico exclusivos de `f3_mcp_cron_observed`, erro original e pós-condição persistida/efetiva. | Dois processos reais `wp-cron.php`, callback único, incidentes reschedule/unschedule preservados com confirmação por releitura, leitura sem replay, desativação/reativação. |

O fonte Yoast **28.5** confirma o terceiro argumento opcional do builder para atualizar o modelo existente. O schema real inclui `blog_id` na hierarquia e `updated_at` com `ON UPDATE`; o reparo tipado não afrouxa as guardas do SQL genérico. Colunas/dependências não modeladas impedem a exclusão. O grupo permanece limitado a 1.000 linhas/4 MiB.

**Limite do diagnóstico do pedido 51:** a causa do incidente original em produção não foi demonstrada. A tentativa de variar o filtro do cache tampouco reproduziu mudança no hash antigo. A implementação adota representação persistida canônica e passou os encadeamentos HTTP; isso é a evidência obtida, sem atribuir uma causa não provada. Após atualizar, faça nova leitura: revisões antigas não são convertidas.

## Memória, recuperação e falhas

Na fixture de **32 MiB**, o codec acrescentou **2 MiB** ao pico de memória. O fluxo completo de exclusão, incluindo WordPress e hooks, acrescentou **11 MiB**, com `memory_limit=99M` e uso inicial de aproximadamente 74,5 MiB. A guarda antiga de tamanho × 6 recusaria esse arquivo. A memória do codec e a do fluxo completo são medidas distintas.

A exclusão preservou os arquivos antes da chamada nativa. Os backups filhos foram restaurados por `files/restore`; a pré-imagem de metadados foi usada para reconstrução assistida pela API WordPress, com ID e valores recuperados. Não foi criada `media/restore`. O backup pai não é aceito como arquivo. O limite de anexos permanece 64 MiB de binários/16 MiB de metadados. Restauração de PHP conserva a barreira existente e recusa arquivos acima de 2 MiB ou sem orçamento para validação.

Foram exercitados metadados sem índice, reconstrução de inventário, exportação em partes, seleção de retenção, JSON malformado/chaves repetidas, escapes e ordem de propriedades. Referências pai/filho também têm registro durável separado do índice. Falhas de seleção, permissão, indexação e banco não foram tratadas como sucesso. Hooks de terceiros e escritores que não compartilham o lock continuam fora de uma transação global.

## Integração e ciclo de instalação

Ambiente: WordPress 7.1.2, PHP 8.3.6, MySQL 8.0.46, PHP-FPM/lighttpd e Apache 2.4. Yoast 28.5 real; persistência do indexable habilitada **somente nas fixtures de teste** por filtro do próprio provedor. Nenhuma configuração de produção foi alterada.

- **MCP 0.19.0 → 0.20.0 pelo HTTP MCP:** 17 verificações, incluindo pool aquecido, credenciais, perfis, tokens, renovação/revogação e confirmação SQL pendente. Falha deliberada após bootstrap restaurou a versão anterior; nova falha após instalar restaurou a 0.20.0. A ativação independente foi verificada. O hash do instalador ensaiado é o da entrega.
- **Pedido 48:** 24 verificações de pacotes, incluindo migração lenta, timeout inconclusivo, estado pendente, reconciliação, erro 500, 403 e conflito de pós-imagem. Não foi reintroduzido rollback automático por timeout.
- **Core 1.30.0:** 123 abilities registradas; novos contratos reconhecidos; migração e finalização pelo executor, observando sua janela nativa. Pausa e retomada independentes verificadas. O teste de recuperação inicialmente encontrou uma fixture pausada antes da migração: ela foi regularizada com instalador e retomada nativos, conforme o script e recibo.
- **Google 0.8.3:** 282 abilities por seus namespaces; status/manutenção, resultados incompletos e ponte MCP real preservados. Foram 20 verificações da ponte/políticas, com zero chamadas Google externas. Instaladores finais 0.8.2 e 0.8.3 foram aplicados pelo canal MCP; versão em novo runtime e dado de teste preservado. Não se usou o recibo de candidato anterior como prova do ZIP final.
- **Instalação limpa:** ZIP final extraído em novo document root, novo banco e ativado, sem importar opções predecessoras.

Os identificadores históricos 018/019 em alguns nomes internos de testes foram conservados nos scripts reutilizados. Os campos de versão executora, destino e SHA-256 dos recibos identificam os bytes efetivamente testados.

## Contratos e operação

O pacote contém guia autenticado atualizado. Os fontes incluem `docs/RELEASE-020.md`, manual, changelog, **167 contratos MCP exportados**, scripts e evidências JSON. As novas rotas mantêm confirmação vinculada à conexão/seleção e validade de 600 segundos. `operations/plan` continua sem SEO e sem `f3base/*`.

Para reparação SEO, solicite a prévia de `content/deduplicate-seo-indexables` com `id`; confirme os mesmos parâmetros com `confirm_token`. Para alterar slug/pai de termo, use `content/update-term`; nome e descrição sem mudança de URL permanecem em uma fase com backup. A instalação não limpa termos/indexables automaticamente.

O instalador continua versionado, sem update feed e fora das atualizações automáticas. Confira SHA-256, aplique primeiro em site piloto por ordem do dono, releia catálogo/revisões e confira resultados públicos antes de executar limpezas autorizadas. Backups de recuperação devem preservar as guardas atuais e respeitar gerações/reconciliação dos provedores. Não há promessa de downgrade do Core.

## Limites da validação

Esta entrega implementa o plugin; os testes são locais. Não comprovam rollout, sete dias de operação, serviços reais Slack/Google/Pipedrive, temas específicos da frota, Redis/Memcached real ou matriz completa multisite. O ciclo Core 1.29→1.30 não foi repetido nesta bancada; foi validado o Core 1.30 instalado/migrado e sua integração com a MCP. A reprodução de falhas de cron usa injeção controlada em torno das operações nativas, não demonstra a causa dos `could_not_set` de produção.

A lista de pedidos do dono não foi encerrada automaticamente. O responsável pela verificação na frota pode usar estes contratos e recibos para o aceite operacional.

## Identidade dos pacotes

Instalador MCP 0.20.0: **753.933 bytes**, SHA-256:

`858b38b703cfebe110bbb61918ff412d0b36ce38467ce525ce4dc2bcae216f3d`

Core 1.30.0 ensaiado: `a5dacbf3e4f7418ba41b80bd21323979904443f9fb9ca55a42eb08bfe1be02f1`.

Google 0.8.3 final ensaiado: `1c60bc7bff22011c85e80a488a445c088cc3f12c6a99372fdcda67919b3dd9ce`.

Os hashes dos fontes e deste relatório constam de `SHA256SUMS-0.20.0.txt`. O pacote de fontes exclui dependências, bancos, ZIPs defeituosos de teste e credenciais de execução.
