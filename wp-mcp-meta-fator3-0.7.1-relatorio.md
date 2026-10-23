# Entrega — Fator3 MCP Meta 0.7.1

Revisão: 1 · Data: 23/10/2026 · Rodada: revisão independente da 0.7.0 recebida, correções e regressão.
Slug: `wp-mcp-meta-fator3` · Versão: **0.7.1**.
Status: **apta-no-escopo-testado**, com limites de homologação externa e do patch mínimo de PHP na seção 6.

**Relatório externo canônico.** A cópia incluída no fonte é anterior ao fechamento; a identidade final do ZIP fonte está na seção 8 deste arquivo.

## 1. De onde esta versão entra

A 0.7.0 feita em outra sessão foi recebida como fonte, instalador e relatório; foi comparada com a referência 0.6.0 e revisada em WordPress real. O dono pediu correção com incremento de patch se houvesse achados e autorizou alterações no Site-Teste, inclusive no banco. Dois defeitos foram reproduzidos; portanto, **a 0.7.1 substitui a 0.7.0 como versão corrente desta entrega**.

Instalação limpa e atualização direta de **0.7.0 → 0.7.1** foram comprovadas. Não é necessário instalar uma versão intermediária. A comparação estática com 0.6.0 contextualiza as mudanças da 0.7.0; não equivale a nova prova própria de atualização direta 0.6.0 → 0.7.1.

| Entrada imutável | Bytes | SHA-256 |
|---|---:|---|
| `wp-mcp-meta-fator3-0.7.0-instalador.zip` | 145728 | `727fab33a1b8e43c2d8980a1b6ca8deb8af39762b334ac1f524471f9d6bbfaa8` |
| `wp-mcp-meta-fator3-0.7.0-fonte.zip` | 557161 | `e90a0328787b6fea926a0848524a869d401d9510bdbd71642ad5d1831426f4b4` |
| `wp-mcp-meta-fator3-0.7.0-relatorio.md` | 18443 | `ec5796ce2f515876a3249b1716e951298e79943b1e4996e733f362c15ed07946` |

Referência 0.6.0: instalador SHA-256 `36f5cfe9a20db272fc80d3cdd8fd46da823c4eeac856e31d911e41754fd19f69`. O build do fonte recebido reproduziu o instalador 0.7.0. O build final 0.7.1 também reproduz exatamente o instalador instalado/testado.

Normas aplicadas: instruções e padrão Fator3, revisão 4 de 16/10/2026, documentos próprios recebidos, pedidos/histórico da base e impacto adicional LinkedIn 0.8.1. As convenções da rodada anterior permanecem como entrada histórica; a autorização explícita desta revisão permite o Site-Teste e patch. Não foram alteradas normas centrais, pedidos externos ou pacotes alheios.

Requisitos exercitados nesta revisão: **WordPress 7.1.3 / PHP 8.3.36** e **WordPress 6.4 / PHP 8.1.34**, PHP CLI/FPM de 64 bits, banco real com InnoDB e locks nomeados. Os mínimos declarados continuam WordPress 6.4 / PHP 8.1.2; o patch exato PHP 8.1.2 teve lint próprio, não teste funcional próprio nesta revisão. A prova funcional 8.1.2 da 0.7.0 é evidência recebida, preservada e separada.

## 2. Convivência e encaminhamentos

Inventário final efetivamente observado no Site-Teste:

| Pacote | Versão | Estado |
|---|---|---|
| Fator3 MCP Meta | 0.7.1 | ativo |
| Fator3 MCP | 0.28.0 | ativo |
| Fator3 Site Core | 1.48.0 | ativo |
| Fator3 MCP Google | 0.17.0 | ativo |
| Fator3 MCP LinkedIn | 0.8.1 | ativo |
| WP Super Cache | 3.1.4 | ativo |
| Yoast SEO | 28.7 | ativo |
| DreamHost Panel Login | 1.0.0 | ativo |

LinkedIn estava em 0.7.0 no inventário inicial e apareceu em 0.8.1 durante a sessão por alteração externa a esta tarefa. Sua instalação/atualização não foi executada por esta revisão. As regressões integradas finais convivem com 0.8.1. Não se declara teste de versões futuras de Core, MCP ou Google apenas mencionadas em planos anteriores.

| Destinatário | Versão examinada | Classificação / situação | Ticket | Encaminhamento |
|---|---|---|---|---|
| LinkedIn | 0.8.0 no planejamento; código instalado 0.8.1 na entrega | `alerta-tecnico`; R1/R2 recebidos atendidos no Meta; avaliação de concorrência aberta no LinkedIn | não atribuído | `wp-mcp-meta-fator3-0.7.1-impacto-wp-mcp-linkedin-fator3.md`, revisão 3 |

O documento adicional LinkedIn 0.8.1 → Meta foi preservado integralmente em `inputs/0.7.1`. Seus R1/R2 foram reproduzidos de forma independente no Meta 0.7.0 e corrigidos na 0.7.1. Os números R1/R2 estão invertidos entre as suítes: R1 LinkedIn = fila/R2 Meta; R2 LinkedIn = diagnóstico/R1 Meta. R3 CAPI e R4 específico de agenda LinkedIn não foram transferidos.

Na leitura estática do LinkedIn 0.8.1, migração e retenção ainda atualizam projeção ilegível sem guarda da mesma revisão/payload; na retenção, o catch executa depois da liberação da trava. A consequência concorrente é hipótese fundamentada no código, ainda não reprodução executada no domínio LinkedIn. A revisão 3 solicita essa verificação ao mantenedor e preserva as revisões anteriores. Nenhuma mensagem foi enviada.

Não há mudança de SDK público, IDs, permissões, schema ou ordem coordenada de instalação com Core/MCP/Google. O registro dos 34 IDs Meta e a exibição de rótulos nas duas telas MCP passaram. Não foi identificada consequência técnica que justifique encaminhamento separado a esses três pacotes no escopo alterado.

## 3. Mudanças e evidência

| Pedido ou origem | Problema / comportamento anterior | Mudança ou decisão | Prova própria |
|---|---|---|---|
| Revisar a 0.7.0 e corrigir achados com patch; impacto LinkedIn R2 | `last_job` ilegível lançava falha e derrubava health/status, inclusive a recuperação do worker | `Worker::health` trata somente `cipher_unreadable`/`storage_corrupt`, identifica a agenda com `schedule_job_unreadable` e conserva os demais diagnósticos; aviso excluído do e-mail horário | Na base, health e status falharam; na 0.7.1 respondem e status recupera o evento. `site-review070.json`, `site-review071.json` |
| Mesmo pedido; impacto LinkedIn R1 | Vinte jobs já indexados queued/retry e ilegíveis ocupavam o lote repetidamente, deixando job válido parado | O worker isola a projeção desses registros e permite que a próxima passagem alcance trabalho válido | Base: 0 isolados e job válido queued após duas passagens; alvo: 20 isolados e job válido complete |
| Revisão de concorrência da migração/retenção | Marcar unreadable após leitura antiga poderia sobrepor a projeção de nova revisão legível | `Queue::isolate` centraliza releitura sob lock do job e UPDATE com revisão e comparação binária do payload; migração, retenção e worker reutilizam a guarda | CAS rejeita revisão substituída; trava MySQL concorrente impede isolamento; erro transitório propaga; job legível nunca é isolado; payload/revisão/datas/retenção preservados |
| Manter melhorias M1–M5 da 0.7.0 | Diagnóstico de leitura, bootstrap, migração ilegível, manutenção e auditoria poderiam regredir | Contratos mantidos; ajuste limitado aos achados acima | Regressões M1–M5, permissões, paginação e zero SQL próprio no bootstrap estabilizado passaram |
| Reprodutibilidade e operação da revisão | Sonda temporária antiga referenciava Config com Meta inativo durante instalação | Guardas de classe nas sondas; testes nativos usam versão do laboratório; controlador de cenários isolados com cleanup | Recuperação e limpeza verificadas; essas ferramentas ficam exclusivamente no fonte |

A comparação **0.6.0 → 0.7.0** identificou alterações funcionais em AbilityLabels, Api, Queue, Schemas, Support, Worker e bootstrap, mais versão/documentação. A 0.7.0 acrescentou `meta/health`; mudou autoload/gate da fila; isolou legados ilegíveis; recuperou manutenção horária ausente; ordenou auditoria do mais recente com `since`; aumentou teto documental de offset; eliminou leitura duplicada da página de conexões. Essas mudanças foram mantidas e exercitadas pelas regressões.

Na comparação **0.7.0 → 0.7.1**, o código funcional alterado se restringe a Queue, Query, Support e Worker. Também mudam Config, cabeçalho, documentação/índice gerado e manifesto. São 21 arquivos diferentes no instalador; 7 PHP, contando os três de versão/documentação gerada. Os 34 IDs e seus schemas de entrada permanecem iguais aos da 0.7.0. Assets e comportamento visual não foram modificados. Diffs e hashes por arquivo estão em `evidence/review071/runtime-060-070.diff`, `runtime-070-071.diff` e `runtime-070-071-files.json`.

`health` não faz reparo ou chamada social. A função de observação é sem escrita; quando a operação é despachada por REST/MCP, permanecem os registros locais de auditoria já contratados. `status` continua sendo escrita local, exigindo perfil adequado. Falhas genéricas de armazenamento não são tratadas como corrupção de ciphertext.

## 4. Instalação e prova da troca

**392 verificações aprovadas no candidato**, distribuídas abaixo. Contagens são execuções de verificações por cenário, não 392 casos distintos. A reprodução deliberadamente falha na base 0.7.0 não integra esse total. Lint e comparação dos documentos são provas adicionais.

| ID | Ambiente / cenário | Resultado | Evidência em `evidence/review071/` | Limite |
|---|---|---|---|---|
| B070 | Site-Teste, 0.7.0, reprodução adversarial | 3 falhas esperadas em 5 checks: health, status e fila; controles passaram | `site-review070.json` | fixtures; zero fornecedor/e-mail |
| S071 | Site-Teste integrado WP 7.1.3/PHP 8.3.36 | correções 11/11; worker 30/30; M1–M5 21/21; metadados/permissões 82/82 = **144/144** | `site-review071.json`, `site-regression-worker.json`, `site-regression-release070.json`, `site-regression-metadata.json` | banco real; HTTP social e e-mail interceptados |
| C071 | Instalação limpa, só Meta, WP 7.1.3/PHP 8.3.36 | metadados 101/101; worker 27/27; M1–M5 23/23; correções 11/11 = **162/162** | `lab-current-setup.json`, `lab-current-*.json` | diretório privado e tabelas novas no servidor; sem acompanhantes |
| M071 | Instalação limpa, só Meta, WP 6.4/PHP 8.1.34 | smoke/REST/docs 24/24; worker 26/26; M1–M5 20/20; correções 11/11 = **81/81** | `lab-minimum-*.json` | WordPress sem Abilities API; PHP 8.1.34, não 8.1.2 |
| U071 | 0.7.0 limpa, semeada com conexão/job/resultado/agenda/histórico; troca para 0.7.1 e novo processo | **5/5**; quatro registros e uma linha de histórico preservados integralmente, inclusive ciphertext, revisão, projeção e timestamps | `lab-upgrade-setup.json`, `lab-upgrade-result.json` | não havia opções comerciais na fixture; marcadores operacionais excluídos da comparação |
| D071 | Leitura documental pelo MCP real | 17 documentos, 21 páginas, bytes/hash iguais ao instalador | `mcp-documents-content.json`, `mcp-documents-verified.json` | WORKER paginado; demais documentos lidos integralmente |
| L071 | PHP local 8.1.2-1ubuntu2.28 e 8.3.6 | 68 arquivos PHP em cada runtime, zero erros de sintaxe | `lint-final.json` | lint não substitui execução funcional |
| F071 | Encerramento | Meta ativo, health ok, homepage/REST 200, sondas e laboratórios removidos | `closure-*.json`, `lab-probe-cleanup.json` | sondas HTTP internas autenticadas de PHP fresco |

O lote do worker com 2000 jobs concluídos usa índice `runnable`, sem filesort, e alcança trabalho executável na primeira passagem. Os testes incluem locks entre conexões reais MySQL, migração limitada a 100 registros, CAS, retry futuro, autorização revogada, recuperação de cron, throttling de e-mail, retenção atrás de 150 ilegíveis e negações ao assinante. No Site-Teste, após aquecimento/conclusão dos marcadores, nova requisição registrou **zero SQL específico do Meta no bootstrap**; reparação inicial ainda pode emitir consultas. Evidências: `site-bootstrap-stable.json`, `site-maintenance-gap.json` e `site-maintenance-recovered.json`.

O instalador 0.7.1 foi enviado/instalado via MCP com identidade de pacote e backup, e reconciliado após recuperação operacional; a versão efetiva foi confirmada em requisição nova. Pacote: `3c05de7665aff130cd226dc329be6b0c`; backup da base: `30a6e1d56ff784d097e1c54e`. Provas: `site-install071-pending.json`, `site-reconciled071.json`. A compilação final produziu o mesmo SHA-256 testado.

**Incidente de teste e recuperação:** durante a troca, uma sonda MU temporária desta revisão tentou usar `Fator3\Meta\Config` enquanto o plugin estava inativo, provocando erro fatal e indisponibilidade temporária do WordPress/MCP. A causa foi a sonda, não código enviado no instalador. Com autorização do dono, ela foi desativada pelo gerenciador de arquivos da hospedagem, removida e corrigida com guarda de classe. A instalação foi reconciliada, testes repetidos e health/HTTP conferidos. A ocorrência está preservada nas evidências e no histórico do checkpoint. Não é correto afirmar que a rodada inteira ocorreu sem impacto operacional; o impacto foi recuperado.

Para outra instalação, use somente `wp-mcp-meta-fator3-0.7.1-instalador.zip`, mantendo a pasta/basename. Em `plugins/upload`, conferir `expected_slug=wp-mcp-meta-fator3` e `expected_sha256=0adbea179f3a89cd66b6dce289fa8658e1723f4a9b38568794fc7c3aea5963f2`; confirmar ativação e executar `meta/health` com `{}` em nova requisição. Estado esperado: versão 0.7.1, armazenamento/criptografia prontos, diagnósticos coerentes com as agendas existentes. Use `meta/status` somente quando desejar recuperação com escrita local. **URL raw de frota não publicada nesta tarefa**; instalação em outros sites permanece com o responsável pela frota, mediante artefato/hash desta entrega.

Documentação: índice local em `docs/`, operação `meta/documentation` com `document=index`; leitura por `document`, `offset`, `limit_bytes` e `expected_revision`. Teto de offset 16777216 e limite por página 65536. Os 17 documentos foram lidos pelo MCP, totalizados e confrontados com bytes/SHA-256 do instalador. Testes também verificaram allowlist, recusa de traversal e revisão divergente, rótulos, versão efetiva e ausência de efeitos sociais.

**Estado final:** Meta 0.7.1 ativo, `state=ok`, armazenamento e criptografia prontos, auditoria ok, zero conexões/agendas/jobs de teste, zero ilegíveis, manutenção agendada, worker desnecessário sem trabalho. Restam apenas auditoria local e os dois marcadores técnicos no armazenamento Meta. Foram removidos 14 objetos de tabela em cada um dos três laboratórios, seus diretórios privados/configurações e o marcador temporário. As quatro sondas MU preexistentes de recuperação do site foram preservadas. Nenhuma sonda Meta desta rodada permanece instalada. O inventário final está em `closure-plugins.json` e `closure-mu.json`.

## 5. Banco e volta de versão

Não há novo schema neste patch: tabela de registros schema 2 e histórico schema 1 permanecem. A quarentena altera somente `queue_state`/`queue_next` da mesma revisão ilegível, sob lock e comparação exata; não regrava payload, revisão, updated_at ou expires_at. Registros ilegíveis são conservados, não executados/apagados automaticamente. Restaurar a chave do site não autoriza retomada automática desses registros; requer diagnóstico e decisão explícita do administrador.

A atualização isolada preservou as quatro linhas comerciais e a linha de histórico cifradas. Durante testes, apenas fixtures próprias foram inseridas/alteradas/removidas; a auditoria das chamadas foi conservada. Os laboratórios usaram prefixos exclusivos e cleanup restrito a esses prefixos, sem apagar o banco compartilhado. As credenciais temporárias de configuração ficaram em diretórios privados do servidor e foram removidas, sem exportação.

Para voltar, interromper execuções concorrentes, preservar backup dos arquivos e dados/chaves correspondentes e restaurar o pacote anterior pelo mecanismo de backup. O backup de instalação indicado na seção 4 recupera arquivos; não desfaz auditoria, cron, projeções ou efeitos externos. A 0.7.0 entende `unreadable`, mas reintroduz os dois defeitos corrigidos; a reversão não é recomendada como correção desses cenários. Não há migração destrutiva a reverter neste patch.

## 6. O que permanece pendente

| Limite / pendência | Motivo e responsável |
|---|---|
| API Meta real, permissões do aplicativo, renovação real de token, ativos Instagram/Facebook, dados/Stories reais | Testes usaram credenciais sintéticas e HTTP interceptado. Dono/frota: homologar com ativos autorizados; esta revisão não atesta aceitação pelo fornecedor. |
| Execução funcional em PHP **8.1.2 exato** | O banco local não pôde abrir socket neste ambiente; laboratório remoto ofereceu 8.1.34. Lint 8.1.2 passou. Mantenedor: repetir matriz funcional exata antes de atribuir essa prova à 0.7.1; a prova recebida da 0.7.0 não foi renomeada. |
| Entrega efetiva de e-mail | Envio interceptado; testes comprovam conteúdo/throttle e aceitação simulada, não recebimento. Dono: validar canal SMTP/destino autorizado. |
| Percurso visual completo e interação por clique de todas as abas | Assets/UI não mudaram. Foram conferidos DOM/rótulos administrativos MCP e permissões; não se declara nova homologação visual completa das abas Meta. |
| Concorrência do LinkedIn 0.8.1 em migração/retenção | Achado estático encaminhado na revisão 3. Mantenedor LinkedIn: reproduzir/corrigir no próprio domínio. |
| Publicação raw e instalação na frota | Fora da execução desta revisão. Responsável pela frota recebe instalador/relatório e confere hash; fonte permanece com o dono. |

Não restaram falhas nos testes próprios do candidato. Isso não é garantia de ausência de qualquer impacto em contas reais ou combinações não exercitadas.

## 7. Credenciais e configuração do dono

Não há novos campos obrigatórios nem necessidade de recriar conexões ao atualizar. Configuração em **Ferramentas → Fator3 MCP Meta**: conexão, credencial Meta, validade UTC quando aplicável, usuários administradores autorizados, ativos explicitamente selecionados e retenção. A validação com fornecedor depende de token, escopos e ativos compatíveis com o relatório escolhido, conforme documentação instalada.

Preservar salts/chaves do WordPress é necessário para ler registros criptografados. Não trocar essas chaves como tentativa de corrigir `cipher_unreadable`. Conferir backup/origem/integridade antes de qualquer retomada. Nenhum token real, senha, cookie, dump de banco ou configuração privada foi incluído nos artefatos; evidências de teste usam valores sintéticos.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `wp-mcp-meta-fator3-0.7.1-instalador.zip` | 150734 | `0adbea179f3a89cd66b6dce289fa8658e1723f4a9b38568794fc7c3aea5963f2` |
| Fonte | `wp-mcp-meta-fator3-0.7.1-fonte.zip` | 753792 | `17d3b8e275cc7eabe191a569c14bd40d03fc5fc9cf9fa7c06ca2ff1e12f9ac2a` |

Relatório: `wp-mcp-meta-fator3-0.7.1-relatorio.md`. Complemento pertinente: `wp-mcp-meta-fator3-0.7.1-impacto-wp-mcp-linkedin-fator3.md`, revisão 3. Fonte com raiz singular `wp-mcp-meta-fator3-0.7.1-fonte/`; instalador com raiz `wp-mcp-meta-fator3/`. Somente o instalador é instalável. Nenhum ZIP contém outro ZIP. O runtime em `plugin/` é byte a byte igual ao instalador final. O fonte foi fechado somente após testes, documentação e esta cópia do relatório; o relatório externo recebe a identidade final sem reabrir ou modificar o ZIP fonte.
