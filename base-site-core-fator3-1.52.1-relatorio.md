# Entrega — Fator3 Site Core 1.52.1

Revisão 1 · 24/10/2026 · Rodada: implementação e homologação · Fuso America/Sao_Paulo.
Slug: `base-site-core-fator3` · Versão/build: **1.52.1 / 20261024** · Contrato administrativo **8.17.0** · **146 abilities Core** · Perfil `piso-padrao-3.6`.
Status: **apta no escopo testado, com pendências de aceite em produção e no fornecedor**. Os pedidos 296, 297 e 298 estão implementados. Site-Teste na versão final, ciclo de 17 etapas concluído com zero falhas. Nenhuma regressão nova identificada nos testes executados; isso não comprova ausência de todo impacto possível.

Relatório externo canônico, fechado após o fonte. A 1.52.0 foi candidata de homologação desta rodada; a 1.52.1 acrescenta a correção de nomes mascarados pelo canal MCP. Não é necessário instalar a 1.52.0 antes da versão final.

## 1. De onde esta versão entra

Entrada comprovada: WordPress limpo e atualização direta **1.51.0 → 1.52.1** por Plugin_Upgrader. Base: instalador 1.51.0, **2270123 bytes**, SHA-256 `7d6c9b8391e8f3a83a85dacbabea56cf93da6f6b04e7e195fcdceb4774f9f192`. A configuração, credenciais cifradas, procedência, listas explicitamente vazias, históricos e cursores usados no teste permaneceram iguais. A repetição do ciclo retornou `atual`.

Requisitos exercitados: WordPress **7.1.2 e 7.1.3**, PHP **8.3.6 de 64 bits**, MySQL **8.0.46** no laboratório; WordPress **7.1.3/PHP 8.3.36** no Site-Teste. Não se afirma suporte a multisite ou a versões inferiores. Pipedrive completo não foi ativado no PHP local abaixo do mínimo 8.3.36 declarado por ele.

Instalação Core existente exige `f3base_email_migracao_142=concluida`. Ausência interrompe o ciclo com `email_migracao_142_pendente`, antes de redefinir dados. Instalação nova, sem resíduos antigos, cria o marcador junto aos padrões atuais. Atualização de versões mais antigas não foi homologada: concluir a migração na base compatível antes desta troca.

## 2. Convivência e encaminhamentos

| Pacote examinado | Versão | Prova desta rodada |
|---|---|---|
| Fator3 MCP | 0.30.1 | Registro/dispatcher, atualização por ZIP e leitura MCP reais no Site-Teste; convivência local |
| Fator3 MCP Google | 0.19.0 | Árvore preservada da base; consumidor CoreContext/SDK e convivência, transporte simulado |
| Fator3 MCP Meta | 0.10.1 | Runtime original conferido contra instalador; convivência/registro |
| Fator3 MCP LinkedIn | 0.10.1 | Runtime original conferido, SDK real com HTTP simulado; convivência |
| Fator3 MCP Pipedrive | 0.1.0 | Consumidor original no teste de contrato; pacote completo no Site-Teste retorna cliente registrado e `operacao_nao_autorizada`, sem chamada externa |
| Implantador | 2.11.0, relatório recebido | Aviso de schema examinado contra Core atual; implantador não instalado em site existente |

Os cinco acompanhantes permanecem ativos no Site-Teste. DreamHost Panel Login 1.0.0, WP Super Cache 3.1.4 e Yoast 28.7 também permaneceram ativos. Nenhum runtime de acompanhante foi modificado. `evidence/1521/inputs.json` identifica as entradas; `companions.json` comprova quatro instaladores iguais às cópias usadas e Google igual à base. Os runtimes de terceiros não são republicados no fonte Core; `build/COMPANIONS.md` explica como fornecê-los para repetir os testes.

### Impactos e pedidos emitidos

Somente **MCP 0.30.1**: `base-site-core-fator3-1.52.1-impacto-wp-mcp-fator3.md`, revisão 1, demanda aberta. O canal mascarou contadores/limiares contendo “passagens”. O patch Core usa `execucoes_esperadas_perdidas` e `limiar_execucoes_perdidas`; a leitura final mostrou **0 e 2**, com limite de transporte **3**. A revisão geral desse falso positivo no MCP continua com seu mantenedor. Não foi enviado relatório por Slack/e-mail nem alterada a lista central.

### Tratamento dos impactos recebidos e anteriores

- **Pipedrive 0.1.0 → Core, C1–C8/Pedido 294:** o contrato `pipedrive-api-client/1.0.0` já entrou na 1.51.0. Regressão com consumidor original aprovada: 46 verificações e seis de recuperação, além da fila legada. Não há mudança de assinatura nesta release. O relatório original Pipedrive, que examinou Core 1.50.0, permanece histórico; seu bloqueio por contrato ausente não descreve a combinação atual. Escritas reais A1–A16 e saldo real continuam com a frota nos sites autorizados.
- **Implantador 2.11.0, impacto revisão 4, Pedidos 20/21:** não se reproduziu o aviso de `type` ausente em `rest_validate_value_from_schema` nas declarações/consultas de herança do Core atual, inclusive no servidor. Nenhuma alteração desnecessária em Config_Mescla. Não se declara reexecução dos lotes completos do Implantador; seu aceite em site recém-implantado permanece com o responsável/frota.
- **Relatórios MCP 0.30.1 e Meta 0.10.1:** considerados. A projeção de provas de cache do MCP foi observada na troca; as mudanças do Meta relativas a stories/auditoria não exigiram alteração de contrato Core. Google/LinkedIn preservaram os contratos exercitados. Não foram gerados documentos de mero encerramento, conforme norma revisão 5.

## 3. Mudanças e evidência

| Pedido | Implementação | Prova |
|---|---|---|
| 296(a–b) | Retirada de `compat/email-legado.php`, classe/alias/etapa antiga e helpers de migração sem chamador. E-mail usa configuração corrente e textos do site. Nova `f3base/email-legado-limpar`, administrativa, simulável, com revisão e conferência de conteúdo antes de excluir três options e a tabela antiga | 25 verificações: autorização, divergência, revisão obsoleta, segredo cifrado, tabela vazia/não copiada/copiada, preservação e repetição; limpeza real do resíduo existente no Site-Teste |
| 296(c–f) | Retirada do importador CF7 não chamado e dos ganchos/inferência Elementor; leitura histórica mantida. 59 documentos substituídos arquivados somente no fonte | Varredura abaixo; 112 documentos atuais lidos integralmente; inventário de transições abaixo |
| 297 | Medição incremental do catálogo, teto relativo à memória disponível até 32 MiB, lotes de 100 rotas e resolução SQL por caminho quando não cabe. Falha conserva pendência e agenda nova tentativa | Oito verificações, incluindo processo previamente acima de 128 MiB, fallback, falha SQL injetada e recuperação; coleta real do Site-Teste sem erro e sem pendências |
| 298(a–c) | Duas ausências consecutivas, três falhas consecutivas de transporte; transporte recente não vira atraso por idade da última cobertura. Incidente com uma reserva de abertura, supressão antes do envio e fechamento somente após abertura confirmada | 18 verificações, incluindo limites, repetição, recuperação precoce e falha de wp_mail |
| 298(d–e) | Meta/LinkedIn antes das entregas e da manutenção; entregas Pipedrive/Slack/avisos antes da manutenção. Cada hook prioritário tem orçamento próprio de 30 s, uma execução por passagem, mantendo travas, revisão, recuperação, cotas e backoff | Seis callbacks vencidos executados na primeira passagem mesmo com orçamento normal já esgotado; tempos abaixo |
| Correção de homologação | Nomes públicos do diagnóstico evitam falso positivo do MCP; versão incrementada de 1.52.0 para 1.52.1 | Leitura MCP final com números visíveis; testes afetados repetidos |

A limpeza não copia dados pessoais para o relatório. Simulação retorna existência, prova e revisão; conteúdo divergente interrompe sem apagar. A aplicação usa trava, reconferência e releitura. Não apaga configuração atual, leads, credenciais atuais nem histórico comercial. O checksum da revisão não contém valores legíveis.

A prioridade mede o trabalho do executor; não elimina latência de rede, limites do fornecedor ou pausas administrativas. O fechamento do incidente registra início, fim, duração e causa, além da hora do estado e do envio. A supressão vale antes da entrega a wp_mail; um e-mail já aceito pelo transporte não pode ser retirado da fila SMTP por este código. Envio incerto/falho não é repetido automaticamente e não gera falsa recuperação.

### Varredura do pedido 296

Foram examinados PHP, JS, JSON, Markdown, testes e fixtures. Os termos pessoais identificados no pedido não aparecem no runtime Core nem no conjunto Core entregue. E-mails restantes no runtime são exclusivamente exemplos `example.com`, `example.org` e `example.test`; telefones/wa.me dos testes são sintéticos. Não ficou remetente, nome de pessoa, telefone ou assinatura pessoal como padrão de envio.

Domínios/marcas da frota encontrados foram classificados: Author URI/Update URI Fator3 são a identidade obrigatória do pacote; os demais aparecem em instruções de escopo/homologação e referências históricas, não como configuração de e-mail. A cópia do pedido novo foi sanitizada para não republicar o trecho pessoal citado como evidência; seu hash original está no manifesto. Os acompanhantes intactos foram analisados à parte, sem incorporar seus exemplos/documentação no fonte Core.

### Inventário das outras transições

| Item | Decisão e motivo |
|---|---|
| `F3Base_Email_Legado`, alias `integracao=f3base_c0`, etapa `email_novo_lead_migracao` | Retirados: migração encerrada; atualização antiga não é reexecutada |
| Helpers antigos de options do e-mail e `copiar_legado()` CF7 | Retirados: sem chamador após a remoção do adaptador |
| Elementor — filtros e inferência | Retirados; valor histórico `elementor` continua aceito na leitura, sem reconstruir eventos |
| `retencoes_mensais` | Mantida: também complementa padrões canônicos preservando autoria; conversor idempotente permite recuperação de configurações antigas/restauradas sem reduzir silenciosamente o prazo |
| `linkedin_integracoes` e leitura da configuração anterior | Mantidas: instalam a integração principal e contexto durável no site novo; diário preserva cursores/UUIDs e retomada. Remover exige separar primeiro a inicialização atual da transição |
| `identidade_pipedrive` | Mantida: vincula prova/catalogação à identidade efetiva da conta e à credencial; protege catálogo antigo/restaurado e troca de contexto |
| `conversoes_conteudo` | Mantida: separa reservas de material e suspende eventos antigos ainda não despachados; não transforma histórico nem reenvia aceitos. A ausência de pendências em toda a frota não foi presumida |
| `f3base_acessos_legado`, `f3base_contatos_legados`, `legado_desconhecido` | Mantidos conforme pedido: acervo histórico e classificação de leitura |
| Projeção `f3base_nav_id`, aliases de navegação/configuração e aliases documentais vigentes | Mantidos: interfaces publicadas ainda consumíveis; sem remoção genérica fora do escopo |
| Leitura de incidentes antigos e marcadores históricos de instalação/retomada | Mantida: evita repetir avisos/efeitos e conserva evidência após atualização/restore |
| Leitores de estados antigos, cursores, atribuição e filas de aquisição/conversão | Mantidos: dados podem sobreviver ao código que os originou; preservação não significa ativar escritores antigos |
| SDKs Google/LinkedIn e contrato Pipedrive | Mantidos: contratos vigentes, não classificados como legado removível |
| Documentos de releases/impactos/planos e manuais já substituídos | 59 arquivados em `history/docs-ate-1.51.0/`; permanecem apenas manuais ainda vigentes no instalador |

### Memória e tempos no Site-Teste

Na leitura do catálogo real na **1.52.1**, 58 rotas: processo alocado antes **250613760 bytes (239,00 MiB)**; memória útil inicial **249269112 bytes**; pico incremental amostrado **103128 bytes (100,71 KiB)**; teto **33554432 bytes (32 MiB)**; memory_limit **512 MiB**. O pico é o maior incremento observado contra o início da montagem, não o RSS total do processo.

A coleta real que resolveu a pendência durante a homologação 1.52.0 começou com **252710912 bytes** alocados e mediu **66224 bytes** incrementais. Terminou sem erro e com **0 pendentes**, estado depois confirmado por `f3base/como-usar` como `ativo`. A passagem final 1.52.1 também terminou sem pendentes; não havia novo dia a reprocessar. No laboratório isolado 1.52.1, o dia sintético foi concluído com **206049280 bytes** já alocados antes do catálogo, e o fallback/falha/retentativa passaram. A amostra pequena teve incremento líquido máximo 0 porque buffers anteriores foram liberados; a medida real do catálogo acima fornece o pico não nulo.

Tempos da passagem controlada **1.52.1**, em milissegundos, no mesmo servidor:

| Hook | Duração do executor (ms) |
|---|---:|
| `f3base_anuncios_consultar` | 43 |
| `f3base_linkedin_consultar` | 33 |
| `f3base_linkedin_notificacoes` | 27 |
| `f3base_avisos_processar` | 29 |
| `f3base_leads_avisos` | 27 |
| `f3base_pipedrive_processar` | 45 |

Captura foi despachada antes da entrega; manutenção permaneceu aguardando. São callbacks sintéticos através do executor real e de seus checkpoints, sem APIs comerciais. Não representam a latência nativo→Core→CRM/Slack em produção. A medição permanente fica nos resultados/diários com prioridade e duração.

## 4. Instalação e prova da troca

Instalador final enviado por `plugins/upload-base64` com `expected_slug=base-site-core-fator3`, SHA-256 da seção 8, `overwrite=true`, `activate=true`. No Site-Teste, a rodada fez 1.51.0 → candidato 1.52.0 → final 1.52.1. Operação final de pacote `ee8f8725a0c2cfef6beb8e423fc5ac4f`, backup de arquivos `ef8ae794e393ae10a24618f3`. O teste nativo separado prova a entrada direta 1.51.0 → 1.52.1.

A leitura final retornou `atualizacao.estado=concluida`, 17 etapas, `falhas=0`, `recuperacao.codigo=core_operacional`. Todos os **406 arquivos instalados** coincidem com a árvore final pelo manifesto SHA-256; o empacotador também compara cada byte com o ZIP. Sondas internas de `/` e `/wp-json/`: HTTP 200 antes/depois, com bypass verificado. Não se afirma prova de acesso externo/CDN.

| Ambiente/cenário | Resultado | Evidência no fonte |
|---|---|---|
| PHP 8.3.6 | 235 arquivos runtime com lint aprovado | `evidence/1521/installer.json` |
| WordPress 7.1.3 local — três pedidos | 51 assertivas aprovadas; autorização, conflito, preservação, falhas e recuperação | `evidence/1521/request-296.json`, `request-297.json`, `request-298.json` |
| WordPress 7.1.2 local | Mesmas 51 assertivas e documentação aprovadas | `evidence/1521/minimum/` |
| Instalação limpa e atualização direta | Dois ciclos nativos aprovados, repetição idempotente e preservação | `evidence/1521/native-cycles-1521.json` |
| Convivência final | MCP/Google/Meta/LinkedIn ativos juntos; contratos/SDKs aprovados | `evidence/1521/coexistence-1521.json` |
| Regressão ampla do candidato | Formulários, filas Pipedrive/Slack, LinkedIn, revisão 1491, pedidos 292/294/295 e recuperação aprovados; disputa do executor entre processos aprovada | `evidence/1520/` — versão e cenário explícitos em cada arquivo |
| Site-Teste isolado — final | 51 assertivas novas aprovadas, HTTP/SMTP de fornecedor bloqueados | `evidence/1521/site-teste.json` |
| Documentação integral | 112 documentos, 573 páginas, 823 assertivas; 825 entradas incluem duas contagens | `evidence/1521/docs-1521.json` e prova no servidor |
| MCP direto | Índice, release e guia de agente lidos integralmente; texto e hashes iguais aos arquivos | `site-teste.json`, `direct_documents` |
| Site compartilhado — final | Ciclo concluído, acessos ativos, limpeza confirmada, nove plugins ativos, `healthy=true` | `site-teste.json`, `final-state.json` |

A renderização da conexão `integracao=f3base_email_novo_lead` foi executada no servidor e conferida. O teste do e-mail com marca e textos configurados passou no laboratório isolado. O Site-Teste compartilhado tem esse envio desligado e sem marca/texto/SMTP completos; isso foi preservado. Não foi enviado e-mail real nem realizada inspeção visual em navegador nesta rodada.

As primeiras tentativas do harness ajustaram a verificação de home durante WP_INSTALLING, o carregamento das funções de tela admin em CLI e a apresentação de um timestamp escalar da coleta. Não eram defeitos de runtime e não contam como aprovações. A coleta que antecedeu a falha de apresentação foi confirmada por releitura persistida; o harness final foi corrigido e repetido. O falso positivo MCP exigiu o patch de produto descrito acima.

Estado final: 69 tabelas exclusivas do laboratório final removidas, diretório/manifesto excluídos, MU temporários e ZIPs de transporte removidos. Laboratório anterior também limpo. Permanecem os backups/auditoria normais do canal, não controladores ativos. Nenhum dado CRM real foi criado. Não foi feita publicação Git/raw nem atualização dos outros 11 sites; URL de distribuição será a aprovada pela frota, com os bytes da seção 8.

## 5. Banco e volta de versão

Não há nova tabela de produção nem migração destrutiva automática nesta release. A instalação atualiza seu diário, complementa a configuração preservando autoria e executa as etapas atuais idempotentes. Catálogo e alarmes ampliam estados existentes; incidentes usam schema 2 e conservam evidência de abertura antiga para não reenviar. As medições de prioridade acrescentam metadados aos diários existentes.

A única eliminação nova é **explícita**: `f3base/email-legado-limpar`, com simulação, revisão atual e prova do conteúdo corrente. No Site-Teste havia `f3base_c0` compatível; foi removida. As outras duas options e a tabela já estavam ausentes. Releitura final confirmou todas ausentes; testes isolados também cobriram as quatro remoções e divergências. A API não cria cópia adicional de segredos antigos em avisos ou relatório.

Antes de implantação, preservar banco, salts e arquivos e respeitar o fluxo de recuperação Core/MCP. Restaurar apenas o ZIP anterior não desfaz limpeza, novos estados ou efeitos remotos. Para recuperar resíduo eliminado, exige-se backup anterior do banco; não é necessário restaurá-lo para operar o e-mail atual. Voltar à 1.51.0 também reintroduz seu adaptador e conteúdo legado, portanto não é uma solução para o pedido 296.

## 6. O que permanece pendente

1. **Frota/dono:** publicação do instalador final e troca nos demais sites; limpeza conferida após a troca em cada site. Não apagar quando a simulação apontar divergência.
2. **Frota:** sete dias sem a antiga recusa de orçamento de catálogo nos 12 sites, e sete dias de incidentes reais em ctooffice/korvena com os limites de avisos exigidos. Isso requer implantação futura; não foi convertido em aceite por testes sintéticos.
3. **Responsável comercial/frota:** entrega SMTP real e latência ponta a ponta de leads/Slack/Pipedrive. Pipedrive comercial somente nos sites autorizados pelo dono, não no Site-Teste. Operação de conta permaneceu desligada neste ambiente.
4. **Mantenedor MCP:** falso positivo geral de redação dos campos operacionais, conforme impacto emitido. Os campos novos do Core já são legíveis na 1.52.1; não há dependência desse ajuste para instalar esta versão.
5. **Responsável Implantador/frota:** repetir seu cenário completo caso o aviso de schema reapareça, com input/schema exatos; o problema não foi reproduzido no Core atual. Não instalar Implantador em site em operação para esse teste.
6. **Limites da prova:** sem inspeção visual em navegador, sem homologação de APIs comerciais, sem teste de versões inferiores aos mínimos nem alegação de regressão exaustiva de cada funcionalidade histórica.

## 7. Credenciais e configuração do dono

Nenhuma credencial nova é exigida por 296–298. Marca, remetente, assinatura, textos e SMTP continuam na tela **F3 Base → Configurações → Conexões e entregas → E-mail automático ao novo lead**, opção `f3base_email_novo_lead`; senha permanece no cofre atual. Não fornecer segredo no chat.

A nova limpeza exige `manage_options`. Primeiro `{"simular":true}`; conferir `ok`, itens e revisão; depois `{"simular":false,"revisao":"<revisao retornada>"}`; reler. Não contornar precondição ou divergência. A atualização não habilita integrações, operação Pipedrive, captura de valores ou destinos publicitários por conta própria.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `base-site-core-fator3-1.52.1-instalador.zip` | 2117492 | `b93a2fe56fa857f46dfa1d6acb1ac674555f7d4dac2f1a84db4b197992db6fcb` |
| Fonte | `base-site-core-fator3-1.52.1-fonte.zip` | 2959833 | `458bf68fcbef212fd09241f97bc2692ef70409224c70ee10426d5a54fec74e83` |

Comparação do instalador: **2270123 → 2117492 bytes**, redução de **152631 bytes (6,72%)**. Árvore descompactada: 463 → 406 arquivos; 10974368 → 10659060 bytes. O arquivo `runtime-diff.json` lista 3 adições, 60 remoções e 51 modificações, incluindo identidade/documentação. Fonte contém Core, testes, build, normas, entradas sanitizadas, evidências e história; não contém ZIP aninhado, banco ou dependências de laboratório.

Complemento técnico: `base-site-core-fator3-1.52.1-impacto-wp-mcp-fator3.md`, revisão 1. Plano executado no fonte. A cópia interna deste relatório é anterior ao fechamento do fonte; somente este relatório externo traz seu tamanho/hash final, sem circularidade. O instalador e o runtime testado não foram alterados ao fechar o fonte.
