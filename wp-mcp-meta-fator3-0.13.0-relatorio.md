# Entrega — Fator3 MCP Meta 0.13.0

28/10/2026 · America/Sao_Paulo. Implementação dos Pedidos MCP Meta 20 e 21. Versão corrente desta entrega: **0.13.0**, instalada e ativa no Site-Teste. Nenhuma implantação na frota/produção nem publicação no repositório foi executada.

**Relatório externo final.** Instalador e fonte fechados. A cópia deste relatório dentro do fonte é anterior ao fechamento e não contém o hash do próprio arquivo ZIP, evitando circularidade.

## 1. Bases aceitas

Base direta: **0.12.0**, sem exigir versão intermediária. Instalador-base: `wp-mcp-meta-fator3-0.12.0-instalador.zip`, 253225 bytes, SHA-256 `b519203886d0964fa531c70cd0a66e2f8e199ff04700f0c3c5fa946d6d83e880`. Fonte-base: 1973443 bytes, SHA-256 `255236ad214851283c5cdad5be523ef9ff2290a636dd3d008738bc17c75bca5b`. Relatório-base: 21652 bytes, SHA-256 `0a8d259f0fad53a298dc4e06ebca1f1d0d59a568e51d46c2f46fd89915ebc774`.

Foram considerados o código/fonte e relatório da base, os novos pedidos de 28/10/2026, os pacotes e relatórios recebidos, os impactos pertinentes e as instruções comuns revisão 5 preservadas em `inputs/0.12.0`. A r5 prevalece sobre a cópia r4 reanexada: impactos contêm consequências e pedidos; respostas, comprovações e encerramentos ficam no relatório principal. A ordem expressa do pedido 20 inclui Ads de leitura no Meta e prevalece sobre sua exclusão nos padrões antigos. Identidades publicadas, capacidades administrativas e contratos anteriores foram preservados. Incremento minor por funcionalidade nova, conforme padrão.

Inventário inicial: Core 1.57.1, MCP 0.33.0, Google 0.20.0, LinkedIn 0.11.0 e Pipedrive 0.2.0. Durante a rodada, outros trabalhos atualizaram Google para 0.21.0, Pipedrive para 0.3.0 e MCP para 0.34.0. Os novos fontes, instaladores e relatórios Google/Pipedrive foram recuperados e examinados. Seus hashes completos estão em `inputs/0.13.0/packages-concurrent.json`; os anteriores, em `packages.json`.

| Acompanhante final | Identidade usada na validação |
| --- | --- |
| Core 1.57.1 | Instalador SHA-256 `ee1c0eb8f46b7640a69e6b4e71697d5fc43bc9cd77f147c6219de1a410c5af62` |
| Google 0.21.0 | Instalador SHA-256 `25da9ef78e303f30ce2f73b8f98743a26e09b8ed238177474e4a956578a63814` |
| LinkedIn 0.11.0 | Instalador SHA-256 `34541afa67c0991e9dc0b5474ab8678dff8cf806eace6ceb1edb47983f9e0308` |
| Pipedrive 0.3.0 | Instalador SHA-256 `30fc784a552a89351900c169fad7300759163fb886b842f45ba807bb0977f657` |
| MCP 0.34.0 | Runtime instalado observado: 467 arquivos, digest de árvore `e60d12e0a303b7adce3b201c9889176311a0332bb308ee18591704cc31d1a9f2`; não é hash de ZIP |

Não foi recebido pacote MCP 0.34.0 nas duas buscas realizadas. Seu guia instalado foi lido integralmente, e o runtime foi copiado para o laboratório e comparado ao digest congelado antes da instalação Meta. A fonte instalada de `ConnectionContext.php` foi comparada à 0.33.0 recebida e permaneceu igual. A prova com 0.33.0 continua em arquivo separado. A ausência de resultado nas buscas não afirma inexistência global do pacote.

## 2. Convivência e encaminhamentos

**Impacto recebido do Core 1.56.0, revisão 1, Meta18(b)/Core309:** o SDK de exclusão local foi entregue na base Meta 0.12.0. O Core 1.57.1 recebido já integra a chamada posterior à exclusão do contato (Pedidos Core 312). Nesta rodada, a prova com Core real verificou ingestão sintética, reconciliação, exclusão automática no Meta e bloqueio de reimportação: 20/20 em `evidence/current-coreprivacy0130.json`. Isso confirma a fronteira exercitada; não é homologação de contato real. Não se reemite impacto para responder ou encerrar essa demanda.

**Novo encaminhamento ao Core:** `wp-mcp-meta-fator3-0.13.0-impacto-base-site-core-fator3.md`, revisão 2, `acao-necessaria`, demanda aberta, pedido Meta20(e)/linha 95 item (5) de Growth Campanhas. A revisão 1 foi emitida no planejamento, antes do código do SDK; está preservada em `planning/IMPACTO-CORE-0130-rev1.md`. A revisão 2 detalha consequências substantivas para identidade, observações anteriores, cursor e concessão. Cabe ao mantenedor Core registrar seu consumidor e associar gasto a contatos/parceiros. **O consumidor Ads do Core não foi implementado nesta entrega.** Meta pode ser instalado antes dele: concessões ficam desligadas por padrão.

**Google 0.21.0/Core316:** relatório e impacto recebidos foram considerados. A negociação de conversões avançadas, esquemas compactos e diagnósticos não altera o leitor GA4 nem impõe mudança ao Meta. O encaminhamento permanece com Core/Google; não se declara seu atendimento pelo Meta.

**MCP 0.34.0:** pedidos 69–73 tratam de diagnósticos, logs, idempotência de upload, pré-imagens/poda e sonda da cópia servida. A instalação Meta usou o executor atualizado, digest esperado e chave de idempotência. Perfis, revogação, recibos e sanitização foram novamente testados. Não foi identificada exigência adicional de código Meta nessa fronteira.

**LinkedIn 0.11.0 e Pipedrive 0.3.0:** namespaces, contratos e arquivos alheios preservados. Capabilities LinkedIn permaneceu executável com a versão esperada; Pipedrive permaneceu registrado e negou operação sem concessão, sem chamada externa. Não há impacto novo identificado no LinkedIn nas fronteiras exercitadas e nenhum relatório de impacto foi gerado para ele. Não se afirma cobertura de todas as funcionalidades internas desses pacotes.

## 3. Mudanças por pedido e evidência

### Pedido 20 — Meta Ads de leitura e acervo sem prazo

O canal `ads` usa conta selecionada explicitamente e `ads_read` conferido na geração atual da credencial. Só são permitidos GETs necessários de contas, metadados, insights e criativos; não há criação/edição de campanhas, gastos, leads comerciais, Pixel ou CAPI neste módulo.

`ads_insights` oferece níveis account, campaign, adset e ad, com granularidade diária. Preserva IDs/nomes, gasto/moeda, impressões, alcance/frequência, cliques/link clicks, resultados e custos com tipos, ações e metadados de criativo quando disponíveis. Moeda e fuso IANA vêm da conta. Dinheiro/contagens ficam como strings, ausência como null; não se transforma falta de dado em zero. Leads de formulário e site usam os tipos específicos, sem somar novamente o agregado de leads. O resultado principal não é inferido.

Datas explícitas vão até ontem no calendário da conta; `time_increment=1`, `use_unified_attribution_setting=true` e `action_report_time=mixed` são declarados. Campos opcionais de resultados/custos são consultados separadamente quando recusados, com identidade e continuação conferidas antes de combinar dados. Indisponibilidade de criativo/campo fica registrada como parcial, preservando os demais valores. Não há escolha arbitrária de campos orgânicos para Ads; `fields` fica omitido ou vazio.

Backfill é explícito e retomável, por dia/página do mais recente ao mais antigo. Guarda o que já foi obtido quando um dia antigo é recusado, sem afirmar que a recusa prova o limite histórico do fornecedor. Seleção até 3660 dias, máximo 10000 páginas por job; dividir cargas extensas. Não foi homologado um horizonte histórico real de cada conta. Agenda usa revisão dos dias recentes (padrão sete dias, configurável de 1 a 30), intervalo padrão diário e fuso da conta.

O histórico existente recebe partição Ads por conexão/conta/nível/atribuição, com identidade incluindo entidade/dia/moeda/fuso. Revisitas substituem a observação corrente sem somar gasto duas vezes. Ads não expira, inclusive quando a conexão tenha política finita. `last_available_fields` conserva cada último valor não nulo com seu instante, separado da ausência corrente; a última observação integral bem-sucedida também permanece. Dia sem linhas não cria zeros nem elimina silenciosamente fatos anteriores; consumidores devem observar cobertura e `last_seen`. Exportações CSV/JSON usam o acervo existente. Retenção máxima das funções anteriores permanece; expiração de tokens/cursores e exclusão explícita de privacidade mantêm seus limites próprios.

SDK local `meta-ads-reader/1.0.0`: registro por objeto, callback de configuração/revisão, consentimento administrativo por consumidor/conexão/conta, paginação consistente e revogação. Revalida a origem administrativa e a autorização do transporte que concedeu acesso; credencial vencida não impede leitura local já concedida. Cron sem usuário exige cliente registrado e concessão válida. Impede objeto fabricado, conta cruzada, cursor de configuração anterior e concessão revogada. Não devolve token nem faz Graph. Acrescenta somente três abilities (`ads-consumers`, `get-ads-grant`, `save-ads-grant`), preservando as 41 anteriores: **44 no total**.

Interface: relatórios/níveis Ads e aba de consumidores com concessão/revogação. Novos documentos instalados `META-ADS.md` e `META-ADS-READER.md`, com schemas e exemplos atualizados. Provas principais: 44 cenários em `current-release0130.json`, repetidos no mínimo; 11 cenários DOM Ads; contratos de transporte na integração 0.33/0.34.

Aceite Site-Teste sem conta: resposta real `not_configured`, “Conexão não cadastrada.”; sem retorno enganoso de métricas. No laboratório, conta não selecionada e `ads_read` ausente foram recusados antes do fornecedor. Os 30 dias sintéticos nos quatro níveis validam transformação/armazenamento; **não substituem comparação ao Gerenciador de Anúncios**.

### Pedido 21 — Coletas orgânicas parciais

Valores vazios/total null deixam de contar como úteis; zero continua sendo dado válido. Quando um grupo de métricas é recusado, a coleta isola os campos e preserva os que funcionam. Linhas em preparação são descartadas antes do fallback para evitar duplicação. Erros próprios de campo ficam em `unavailable_metrics`; revogação global, quota e transporte continuam falhas/retries apropriados, sem transformar token inválido em sucesso parcial.

Resultados de jobs e cobertura incluem `successful_rows`, contagem da página e `outcome`. Agendas guardam `last_run_status`, `last_successful_rows`, métricas indisponíveis e `last_partial_at`; `last_success_at` só avança após persistência útil. Para compatibilidade, um status legado partial pode existir sem linhas úteis, mas `outcome=failed` e a agenda falha sem avanço de sucesso. `meta/health` separa `partial_schedules` de `failed_schedules`; parcial útil não dispara aviso de falha integral.

Foram exercitados vazio/suprimido/recusado junto de métrica válida, todas indisponíveis, falha global, páginas e retomada. A recombinação real de `follows_and_unfollows` na `ig-conta-diario` de ctooffice/korvena e reversão de A-METASEG-2710 pertencem à frota após aceite, sem alteração remota nesta rodada.

### Revisão de regressão

Diff integral contra 0.12.0 em `evidence/runtime-changes0130.json`: 40 arquivos alterados/adicionados, preservando slug/basename/provider e namespaces. Código novo principal em `build/meta/Ads.php` e `AdsReader.php`; alterações pertinentes em conexões, relatórios, histórico, fila/agendas, schemas, acesso e interface. Esquemas de banco permanecem os mesmos. Suítes anteriores foram executadas novamente com runtime 0.13.0, incluindo retenção, Stories/mensagens, credenciais, diagnóstico, fila e privacidade.

## 4. Instalação, prontidão e testes

Matriz nativa: WordPress **7.1.3/PHP 8.3.36** e WordPress **6.4/PHP 8.1.2-1ubuntu2.28**, MySQL **8.0.41**, 64 bits. Ambientes descartáveis no Site-Teste com diretório e prefixo SQL exclusivos; o banco compartilhado não foi apagado. Fixtures de negócio bloquearam HTTP e e-mail externos. Dependências de runtime mínimo foram baixadas de pacotes oficiais com hashes fixados. Lint PHP, build e geração de metadados foram concluídos antes de congelar o instalador.

| Prova final | Resultado | Evidência em `evidence/` |
| --- | ---: | --- |
| Ads e parcial, WP 7.1.3 | 44/44 | current-release0130.json |
| Privacidade e reinício | 76/76 + 4/4 | current-privacy0120.json; current-privacy0120-restart.json |
| Stories/mensagens/retenção | 77/77 | current-release0110.json |
| Diagnóstico | 41/41 | current-release0100.json |
| Credenciais/identidade | 55/55 | current-release090.json |
| Registros ilegíveis | 11/11 | current-review071.json |
| Health/manutenção | 23/23 | current-release070.json |
| Fila/worker | 27/27 | current-release060.json |
| Instalação/documentos/REST nativo | 32/32 | current-isolated0130-smoke.json |
| Integração MCP 0.33 e acompanhantes novos | 27/27 | current-integration0130.json |
| Integração MCP 0.34 instalado | 27/27 | current-integration-mcp034.json |
| Exclusão com Core 1.57.1 real | 20/20 | current-coreprivacy0130.json |
| Atualização direta 0.12.0 → 0.13.0 | 10/10 | upgrade-install.json; upgrade-proof.json |
| Mínimo WP 6.4/PHP 8.1.2: instalação | 32/32 | minimum-isolated0130-smoke.json |
| Mínimo: Ads/parcial | 44/44 | minimum-release0130.json |
| Mínimo: privacidade/reinício | 76/76 + 4/4 | minimum-privacy0120.json; minimum-privacy0120-restart.json |
| DOM Ads/credenciais/mensagens | 11/11 + 25/25 + 17/17 | ui0130-dom.json; ui0130-credentials.json; ui0130-messaging-stories.json |
| Selftest compartilhado | 8/8 | site-selftest.json |
| Documentação MCP integral | 25/25 | site-documentation0130.json |
| Catálogo final sem auxiliares | 44 operações | site-final-catalog.json |

Os 53 testes DOM usam HTML produzido pelo WordPress e jsdom 27.4.0 com REST simulado; não houve inspeção visual em navegador. `current-environment090.json` e `minimum-environment090.json` registram ambiente/criptografia e ausência de problemas PHP do pacote na execução observada. Não houve teste nativo MariaDB, fornecedor Graph real nem prova externa de todas as camadas de cache/CDN.

As primeiras execuções de suítes históricas encontraram expectativas de 41 operações/escopos antigos e estado deixado por outra suíte; foram corrigidas as fixtures e repetidas em instalação isolada. A integração inicial encontrou os hashes Google/Pipedrive alterados por atualizações concorrentes; os novos pacotes foram examinados antes da repetição. A primeira detecção MCP 0.34 no teste falhou por espaçamento do cabeçalho, corrigida com o leitor WordPress; a evidência negativa foi preservada em `development0130/integration034-header-fixture.json`. As evidências finais da tabela não têm falhas. Nem todas as tentativas preliminares possuem arquivo separado; não são apresentadas como testes aprovados. Uma descrição herdada em `upgrade-proof.json` cita 0.11.1; o log `upgrade-install.json` demonstra que a versão efetivamente instalada e semeada foi 0.12.0, com 11 registros e um histórico. O rótulo da suíte foi corrigido para reprodução futura, sem editar a evidência bruta.

**Instalação compartilhada:** `https://fator3-teste-mcp-1.dreamhosters.com/`, atualização 0.12.0 → 0.13.0, operação de pacote `15ea55ab4c3e399443f2e25a25a4e24d`, pré-imagem `a7aba69c4814e9c7f74bde26`. Verificação em nova requisição PHP, plugin ativo, recuperação `applied`. Home e REST HTTP 200 antes/depois com bypass comprovado internamente (`internal_same_origin`, sem prova de acesso público externo). O ciclo de activation hook não foi repetido; o carregamento normal confirmou o runtime e os schemas já compatíveis.

`site-before.json`, `site-after.json` e `site-preservation.json` comprovam os mesmos registros de negócio (2), histórico (0) e opções Meta, excluídos eventos esperados de auditoria/diagnóstico; a escassez desses dados não substitui a atualização semeada do laboratório. Runtime final: 59 arquivos, 30 PHP, árvore SHA-256 `e5ee6f8b98a1953bd4e13f5483328b6546b353797e4842750682cccc5696256c`. Todos os acompanhantes conservaram seus hashes na troca Meta. O digest de árvore ordena caminhos relativos e calcula SHA-256 da concatenação `caminho + NUL + sha256(bytes) + LF`.

Os 25 documentos foram lidos integralmente pelo MCP 0.34.0, com revisão esperada, tamanho, SHA-256 e igualdade de bytes ao instalador. Estado final: health `ok`, storage/crypto prontos, zero conexões Meta, zero agendas ativas/parciais/falhas; a recusa sem conexão é esperada. O laboratório final removeu suas 93 tabelas próprias e diretório/manifesto; os três arquivos temporários foram removidos com guarda de hash e backup. Catálogo final sem `meta/qa-*`. Backups e auditoria do MCP permanecem conforme política do serviço. Ver `site-cleanup.json`.

**Conclusão de validação:** sem regressões observadas nas fronteiras exercitadas. A entrega está pronta como pacote e instalação local; a operação Ads real ainda depende de credenciais/ativos e dos aceites abaixo.

## 5. Banco, retenção e reversão

Mantidos schema de registros 2 e histórico 1, sem nova tabela ou migração destrutiva. Ads usa partição do histórico existente e bucket cifrado de concessões. Normalização acrescenta ativos Ads vazios; não concede conta, consumidor ou agenda automaticamente. Preservados ciphertext, configurações, revisões e política finita explicitamente escolhida na fixture da base; o histórico Ads tem retenção própria sem prazo.

Rollback para 0.12.0: pausar agendas Ads e revogar concessões antes da substituição de arquivos. Dados novos permanecem, mas a base anterior não os interpreta. Guardar backup de arquivos/banco e preservar salts/chave de privacidade, bloqueios e recibos. Não voltar a versões anteriores à 0.12.0 com recepção de mensagens habilitada: elas não interpretam os bloqueios de exclusão. Restauração não desfaz efeitos já entregues ao consumidor e não deve ressuscitar contatos apagados. Desativação/desinstalação preserva dados, removendo eventos próprios. Nenhuma poda dos dados do usuário foi realizada.

## 6. Pendências e responsáveis

| Responsável | Pendência e critério |
| --- | --- |
| Operador/frota | Autorizar e configurar contas 1803436740776667 em korvena.com.br e 2098846280719695 em ctooffice.com.br; conferir 30 dias por campanha em gasto, impressões e cliques contra o Gerenciador, com mesmo fuso e atribuição. Site-Teste não possui conexão Meta. |
| Frota | Após implantação e aceite do pedido 21, recombinar follows_and_unfollows na ig-conta-diario dos dois sites e desfazer A-METASEG-2710. Não houve mudança nessas agendas remotas. |
| Mantenedor Core | Implementar consumidor meta-ads-reader/1.0.0, concessão/configuração, relação por campanha/conta/parceiro e validação coordenada descrita no impacto. |
| Operador/frota | Aceites reais anteriores de App Review/mensagens/novas métricas e credenciais permanecem conforme quadro da frota; esta rodada não declara sua resolução. |
| Dono/frota | Publicar/implantar os artefatos após seu fluxo; conferir hash e slug. Fonte permanece com o dono. Nenhum push foi feito. |

Não foram criados números de pedido Core, encerramentos de itens externos ou autorização comercial por inferência. Não há bloqueio local conhecido após os testes finais; as pendências acima limitam o aceite de negócio real.

## 7. Credenciais e proteção

Nenhum token real foi cadastrado, renovado, exportado ou incluído no fonte. Fixtures usam identificadores/segredos sintéticos e impedem chamadas externas/e-mail. Credenciais de banco do ambiente foram usadas apenas pelo processo isolado, sem inclusão nos artefatos. Não foram enviados contatos, mensagens, notificações ou alterações de anúncios reais. Consultas locais do SDK respeitam concessões e não expõem credencial; a retenção de dados não amplia a validade de tokens ou cursores.

## 8. Artefatos finais

Instalador: `wp-mcp-meta-fator3-0.13.0-instalador.zip` — **284069 bytes**, SHA-256 **`3ecd6ee6f277c7581adc05b4fa38c46611e3232b4400bb4a4421956c9fba8ac1`**. Raiz `wp-mcp-meta-fator3/`; basename preservado. É o mesmo ZIP instalado e testado, sem alteração posterior.

Fonte: `wp-mcp-meta-fator3-0.13.0-fonte.zip` — **2268353 bytes**, SHA-256 **`2d2ec08055c4ab8806b626d3c67097e7fa3cfaaf7f9ae3df18d1576cc4e8d2f7`**. Raiz `wp-mcp-meta-fator3-0.13.0-fonte/`; inclui código canônico, runtime idêntico ao instalador, build, testes, entradas, plano, evidências, histórico e este relatório, sem ZIP aninhado, banco ou node_modules.

Relatório externo: `wp-mcp-meta-fator3-0.13.0-relatorio.md`. Encaminhamento novo: `wp-mcp-meta-fator3-0.13.0-impacto-base-site-core-fator3.md`, revisão 2, apenas consequências e pedido ao Core.
