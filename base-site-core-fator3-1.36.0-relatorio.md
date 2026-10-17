# Entrega — Fator3 Site Core 1.36.0

Revisão: 1 · Data: 2026-10-17 · Fuso: America/Sao_Paulo · Rodada: implementação
Slug: base-site-core-fator3 · Basename: base-site-core-fator3/base-site-core-fator3.php
Status: **com-pendencias** — implementação e Site-Teste concluídos; aceite 212(a) no CTO e adoção Google permanecem atribuídos aos respectivos responsáveis.

## 1. De onde esta versão entra

Base direta aceita: **1.35.0**, ou WordPress limpo. Instalador-base recuperado sem alterações: 1.944.805 bytes, SHA-256 `1368395e6c5842c21e822010310c1d544000ed7d72b2f6ee234491d18c686f20`. Fonte-base: 2.056.313 bytes, SHA-256 `049ab61d5af4e005df8305b1edea6e1a55834ed4e133d3726c8cfe9ac49cd06c`. Não é necessário instalar intermediária.

Escopo: Pedidos core **212(a)** e **224**, mais resposta ao impacto Google 0.11.0 revisão 2 sobre descoberta da conversão de material/Core 222. Os pedidos 219–223 já aceitos pela frota não foram reabertos. Base documental: instruções comuns e padrão de desenvolvimento revisão 4, aba Core anexada com acréscimos de 17/10 e relatórios/impactos dos acompanhantes fornecidos.

Mínimos efetivamente exercitados: **WordPress 7.1.2, PHP 8.3.6 de 64 bits**, instalação única, MySQL 8.0.46 no laboratório. Não houve suporte mínimo novo nem alteração do cabeçalho desses requisitos. Site-Teste: WordPress 7.1.3, PHP 8.3.30, MySQL 8.0.41.

## 2. Convivência e encaminhamentos

Acompanhantes permaneceram ativos no Site-Teste: MCP **0.24.0**, Google **0.11.0**, Meta **0.3.0**, LinkedIn **0.3.0**. As funções próprias foram exercitadas também em instalação limpa sem acompanhantes. O consumidor Google atual foi testado em bancada usando suas classes reais CoreContext/ContractSchema; isso não equivale a homologar as APIs da conta.

| Destinatário | Versão examinada | Classificação / situação | Referência | Impacto |
|---|---|---|---|---|
| Fator3 MCP Google | 0.11.0 | acao-necessaria; produtor entregue, adoção opcional aberta | Impacto Google r2 / Core 222 | [base-site-core-fator3-1.36.0-impacto-wp-mcp-google-fator3.md](base-site-core-fator3-1.36.0-impacto-wp-mcp-google-fator3.md), revisão 2 |

O impacto foi iniciado no planejamento, antes do código, e atualizado com contrato real, testes, hash e estado da entrega, preservando a proposta histórica. Não foi enviado ao responsável nem implementado código no Google.

SDK administrativo **8.1.0** e SDK de medição **site-measurement-context/1.0.0** preservados. Não há nova ordem obrigatória de troca: Core pode vir antes de um futuro consumidor opcional. Foram examinadas as fronteiras de transporte MCP, configuração/implantação, Meta e LinkedIn afetadas pelos arquivos alterados; não foi identificado impacto técnico adicional que justifique outro documento. APIs comerciais, assinaturas e fluxos sociais fora do escopo não foram re-homologados.

Hashes dos instaladores acompanhantes examinados: MCP `e2c78fcf0e99da55237808bc51fe408405e367fd76a71172b497707996f8aa95`; Google `d181deaeee8ef365ac4d6a08884d9fa3d3a3164b21f0538d8ed5d56722536bf9`; Meta `0f77360b0afca8c1040c411d7bd8b56a431428993f78b9d1504384fce8b6dd03`; LinkedIn `b6d20998379236baf46ac5ae0181646e8a15fb75bbb4f37a88a68be01d2d768a`.

## 3. Mudanças e evidência

| Pedido | Problema | Mudança | Resultado e evidência |
|---|---|---|---|
| 212(a) | Conjunto bruto de análise retido; recusa posterior atribuída a fonte pequena | Leitura em lotes de até 128, liberação do buffer SQL e projeções compactas; diagnóstico distingue maior crescimento da consulta recusada | Dez resultados de domínio idênticos à base; resumo/aquisição em 28 dias sob 128 MiB. evidence/memory-*.json |
| 224 | Intenção/partes podem ficar sem evento único e aguardar rotina horária | Reagendamento na intenção, repetição idempotente, sincronização de partes e recuperação pelo próprio WP-Cron; executor limitado a até oito subpassagens | Seis partes reais concluídas em **29 segundos**, sem cron/schedule nem execução manual. evidence/site-teste.json |
| Impacto Google / Core 222 | Contrato antigo fechado não permite descobrir material | SDK opcional separado, descritor próprio, schemas, fixtures e ability administrativa | 19 checks de produtor e três do consumidor antigo; leitura MCP real. evidence/conversion-sdk.json, google-compat.json e site-teste.json |

**212(a), detalhe da prova.** Fixture nativa com 5.872 linhas de análise, 1.931 eventos e 24 conteúdos em 16/09–13/10/2026, incluindo dados de teste, automação, dimensões, sessões e continuidade. Dados e tamanho de atribuição são sintéticos. Aproximadamente 65 MiB vivos foram reservados antes da consulta para representar pressão de bootstrap.

| Medida | Base 1.35.0 | 1.36.0 |
|---|---:|---:|
| memory_limit da execução | 512M, para obter referência completa | 128M |
| Pico de arena, resumo/aquisição | 180,5 MiB | **82,5 MiB** |
| Tempo observado, resumo | 0,96 s | 3,35 s |
| Tempo observado, aquisição | 0,81 s | 3,44 s |
| Comparação de resultados | Referência | 10/10 idênticos |

A redução de memória implica mais consultas SQL na bancada; não é uma prova de redução de latência. Foram excluídos da comparação somente horário da consulta e saúde transitória da coleta. O pico não representa memória exclusiva do plugin. Nenhuma reprodução fatal foi provocada no Site-Teste/CTO.

Preservados os limites de 397 dias e 100 mil linhas por fonte, filtros e resultados. Agregados, conjuntos de identidades e índices compactos ainda crescem com a cardinalidade; não há promessa de memória constante para qualquer entrada. O lote usa estimativa adaptativa e não aumenta memory_limit. A leitura paginada não cria uma fotografia transacional entre todas as fontes.

Na recusa de memória, `fonte`/`linhas` passam a refletir a maior fonte com crescimento vivo observado quando existe; `fonte_maior_crescimento` detalha essa medida e `fonte_consulta_recusada`/`linhas_consulta_recusada` conservam a consulta que não coube. Quatro verificações cobriram recusa real de orçamento e teto de 100.001 linhas. O aceite final com dados de ctooffice continua pendente.

**224, causa e limites.** A intenção nova já agendou corretamente na reprodução local da base; não foi provada causa única para todos os relatos da frota. Reproduzido o evento ausente e a repetição idempotente que não reparava a agenda. A nova implementação cobre esse caso, a sincronização entre partes e a recuperação do evento perdido no bootstrap do WP-Cron. Leitura administrativa/ajuda não passa a reparar agenda.

O cron processa até oito subpassagens, com orçamento de 20 segundos e reserva para transporte; persiste cada parte antes da seguinte. Respeita cadência, lease, pausa, Retry-After e resultados incertos. Cinco checks cobriram 429/recuo, não repetição de resultado incerto e supressão; teste HTTP nativo com perda deliberada do evento entregou seis partes em 18 segundos, com Slack simulado. Fila grande, rede indisponível/recuo ou ausência de acionamento do WP-Cron podem ultrapassar dois minutos.

**Contrato opcional.** `site-conversion-purposes/1.0.0`, classe `F3Base_Conversoes_Contexto`, methods capabilities/snapshot e ability `f3base/conversoes-contexto-ler`. Entrada exige contract; expected_revision opcional. Retorna contact/material, eventos próprios, enabled/configured, IDs públicos, procedência e revisão. Material Ads/LinkedIn nunca herda ação de contato. Versão incompatível e revisão instável/obsoleta têm erros explícitos/data:null.

A ability exige manage_options; PHP interno projeta apenas configuração pública. O consumidor deve aplicar sua própria autorização. Nenhum token, PII, decisão individual de consentimento, escrita, agendamento ou chamada ao fornecedor no snapshot. runtime_verified/remote_access_verified são false. Não altera o catálogo fechado do SDK antigo nem configura ações nas contas.

## 4. Instalação e prova da troca

Instalador fechado antes dos ciclos nativos e usado sem mudança no Site-Teste. Raiz `base-site-core-fator3/`; `expected_slug=base-site-core-fator3`; SHA-256 na seção 8. O envio base64 integral foi recusado pelo transporte como JSON inválido antes da troca. Foi concluído upload em oito partes pelo serviço MCP, verificado tamanho/hash, seguido de `plugins/upload-base64` com zip_path, overwrite/activate e guardas de slug/hash. O ZIP temporário foi removido.

Troca 1.35.0→1.36.0 confirmada: operação `57a2ee2249c3234f9de034f3`, pacote `ab8d4a811322c25b1f8470ebbee8090b`, `applied=true`, `silent_reactivation`, PHP novo. Home e REST: HTTP 200 antes/depois. São sondas de mesma origem; não se atribui a elas prova de acesso externo de navegador.

Prontidão: `f3base/saude-ler {}` retornou versão 1.36.0, atualização `concluida`, **15 etapas, zero falhas**, confirmação pelo executor e finalização após o prazo natural. Contrato administrativo 8.1.0 preservado.

| ID | Ambiente | Cenário | Resultado | Evidência / limite |
|---|---|---|---|---|
| SINTAXE | PHP 8.3.6 | 210 arquivos PHP | Aprovado | installer.json; lint não substitui execução |
| NOVO | WP 7.1.2/PHP 8.3.6 | Instalação limpa sem acompanhantes | Aprovado | native-cycles.json |
| UPGRADE | WP 7.1.2/PHP 8.3.6 | Base 1.35.0, Plugin_Upgrader, processos novos | Aprovado | Dados, cursor, callback e segredos sintéticos preservados; prazo de finalização adiantado só na bancada |
| MEMÓRIA | WP 7.1.2/PHP 8.3.6 | 28 dias sob 128M | Aprovado na fixture | memory-candidate/parity/diagnostics; CTO não executado |
| AGENDA | WP 7.1.2/PHP 8.3.6 | Evento ausente, retomada, recuo/incerto | Aprovado | scheduler-http/guards; fornecedor simulado |
| SDK | WP 7.1.2/PHP 8.3.6 | Contratos e permissões | Aprovado | conversion-sdk/google-compat; sem conta comercial |
| DOCS | Local + Site-Teste | Índice, schemas, páginas, hash e recusa de caminho | Aprovado | docs-1360/site-teste; anônimo/editor recusados na bancada nativa |
| REAL-224 | Site-Teste + Slack real | Contato marcado, seis partes, somente WP-Cron | **29 s** | REST 201 às 14:47:32; principal 14:47:55; última 14:48:01, todos −03 |
| FINAL | Site-Teste | Prontidão e limpeza | Aprovado | site-teste.json; backups/auditoria nativos permanecem |

O contato de teste passou por `/formularios/enviar` via auxiliar administrativo temporário, com token legítimo do formulário existente e contexto_teste true. Não foi teste de interface de navegador. Evento único apareceu imediatamente, com prazo +10 s; passagens registradas tinham wp_doing_cron=true. Não houve cron/schedule, chamada manual de executor ou acesso manual a wp-cron.php no Site-Teste. A API Slack confirmou presença/conformidade da principal e as seis mensagens da thread; leitura humana não é comprovada.

Documentação: índice instalado `docs/DOCUMENTACAO.md` e `f3base/documentacao-ler`. Descoberta e schema obtidos pelo MCP; guia de agentes, release e schema de entrada lidos por inteiro. `docs/CONVERSOES-SDK-1.36.md`: **132 linhas, cinco páginas**, versão 1.36.0 e SHA-256 `efdf3c93c39290a43939b84a0b8f7665708ce9e51f74b7ef00a8656565a2ab6c` iguais até proxima_linha null. Travessia para wp-config.php recusada. Leitura é local, sem verificação implícita no fornecedor.

Estado final: Core 1.36.0 ativo; demais versões da seção 2 inalteradas, além de WP Super Cache 3.1.4, Yoast 28.7 e DreamHost Panel Login 1.0.0. Os quatro interruptores true, IDs próprios vazios e política de testes mantiveram valores e revisões. As seis mensagens sintéticas foram apagadas com ausência relida individualmente; contato eliminado, auxiliar/estado temporário removidos e ability temporária deixou de existir. Permanecem apenas backups privados e trilhas nativas de auditoria/manutenção. Registros antigos de falhas de Slack não foram apagados.

URL raw final: **não publicada nesta rodada**. Dono/frota publicam o instalador/relatório e verificam SHA-256 antes de instalar nos demais sites. Fonte permanece com o dono, conforme decisão 89. Não houve push nem alteração de outro site/plugin.

## 5. Banco e volta de versão

Nenhuma nova tabela, coluna, option de produto ou migração de estrutura. Marcador de estrutura **1.35.0** permanece intencionalmente; ciclo de instalação usa **1.36.0**. Filas, leases e procedência existentes são reutilizados. O ciclo comum pode executar sua manutenção já publicada; não se declara ausência de qualquer escrita de instalação.

Antes da troca: backup privado SQL gzip de **89 tabelas**, 16.679.983 bytes, artefato `f1757e2015964910f6a144a156cd540c`, SHA-256 `e032b86c8fe8b453fa05f8d863e7914c19903ff7077a80660e189c7329b38086`. O backup permanece no servidor e contém valores sensíveis; não integra a entrega. Pré-imagem dos arquivos do plugin: `a52f597181dfb0aba4d46406`.

Reversão: restaurar o instalador-base 1.35.0 validado/pré-imagem, preservando banco e arquivos privados; não desinstalar para atualizar. A estrutura continua compatível, mas voltam as limitações de memória/agenda e desaparece a interface opcional. Restaurar arquivos não desfaz mensagens ou efeitos externos; consumidores novos devem tolerar ausência do SDK. Restaurar banco compartilhado exige reconciliação e cuidado com alterações posteriores. **Rollback não foi executado no Site-Teste**; não houve motivo para desfazer a troca aprovada.

## 6. O que permanece pendente

1. **Frota / aceite 212(a):** instalar a versão autorizada em ctooffice e repetir `f3base/medicao-editorial`, visões aquisicao e resumo, 2026-09-16..2026-10-13, segmento sem_testes, automacao audiencia, anotacoes true, limite 5. Esperado: resultado ou diagnóstico preciso. A fixture sob 128M não substitui essa prova; CTO não foi alterado nesta rodada.
2. **Responsável Google:** adotar e validar o contrato opcional em sua próxima versão, conforme impacto r2. Google 0.11.0 continua no SDK anterior.
3. **Dono/frota:** publicar/distribuir artefatos e decidir implantação nos demais sites. Ações/IDs próprios de material em Google Ads e LinkedIn continuam vazios e dependem das contas do dono; a atualização não os inventa.
4. Fora da matriz desta rodada: rollback real, navegador, contas comerciais Google/Meta, Lead Sync LinkedIn com aplicativo real e Pipedrive. Não são apresentados como homologados. Matriz mínima já comprovada não autoriza estender suporte a runtimes diferentes sem teste.

Não há pendência do aceite 224 no Site-Teste. Não foram alterados a lista central de pedidos ou os documentos da frota; o revisor responsável registra o encerramento.

## 7. Credenciais e configuração do dono

Nenhuma credencial nova necessária. Slack usou a configuração existente em F3 Base → Configurações → Conexões e entregas → Avisos, transporte Aplicativo, formato thread e destino autorizado de homologação; token não foi lido/divulgado. Política de testes: Slack marcar; e-mail e demais destinos suprimir. Pipedrive não foi habilitado para homologação.

Conversões de material continuam nas opções existentes. GA4 usa download_material, Meta MaterialDownload. Ads requer rótulo próprio; LinkedIn requer ID próprio; vazios não herdam contato. Não houve criação automática de recursos no fornecedor, mudança de consentimento ou ativação comercial.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [base-site-core-fator3-1.36.0-instalador.zip](base-site-core-fator3-1.36.0-instalador.zip) | 1967841 | `eeec2a765d7e004aab1046fd59a25e455b6b5651d4468368fdf220b3e23d811b` |
| Fonte | [base-site-core-fator3-1.36.0-fonte.zip](base-site-core-fator3-1.36.0-fonte.zip) | 2088119 | `867b4a3dd122858019526197a093168deba6a484de123e0c8349140b1fa82063` |

Relatório externo canônico: **base-site-core-fator3-1.36.0-relatorio.md**. Complemento pertinente: **base-site-core-fator3-1.36.0-impacto-wp-mcp-google-fator3.md**, revisão 2.

A cópia deste relatório incluída no fonte é **anterior ao fechamento do próprio fonte**: seu tamanho/hash ficam identificados como pendentes nessa cópia. Somente o relatório externo recebe a identidade final após o empacotamento, evitando circularidade. Instalador e fonte não contêm outro ZIP da entrega, banco, tokens reais ou logs pessoais. O instalador não inclui executores QA, binários ou ferramentas temporárias.
