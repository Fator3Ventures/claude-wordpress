# Entrega — Fator3 MCP LinkedIn 0.11.0

Revisão: 1 · Data/hora: 2026-10-26T21:59:13-03:00 · Rodada: implementação do Pedido MCP LinkedIn 14.
Slug: `wp-mcp-linkedin-fator3` · Versão/build: `0.11.0` / `0.11.0`.
Status: **com-pendencias de homologação externa e aceite completo no Site-Teste**. Implementação concluída, sem regressões detectadas no escopo testado; 0.11.0 é a versão corrente desta entrega e está ativa no Site-Teste.

**Relatório externo canônico, fechado após o fonte.** A cópia interna antecede o fechamento e remete a este arquivo para tamanho e SHA-256 finais do ZIP fonte. Runtime, escopo e resultados permanecem iguais.

## 1. De onde esta versão entra

Instalação limpa e atualização direta da base aceita **0.10.1**. Instalador-base: 254.066 bytes, SHA-256 `6182ea63bff6788f5d2637467e7ab29d58568e37283d6ece82d3e58ee41c13bc`; fonte-base: 1.207.818 bytes, SHA-256 `518b83da12940f044edd99e4223348f4ef01011dc57c7c40181793c473b6d0cc`. A base foi recuperada e conferida contra as identidades recebidas. Nenhuma versão intermediária é necessária.

Escopo: **Pedido MCP LinkedIn 14(a–d), “Guarda de dados sem prazo: auditoria, coletas e acervo histórico”**, aberto em 26/10/2026. O pedido 13 já está aceito no documento recebido; sua implementação e a correção de identidade da 0.10.1 foram preservadas e submetidas a regressão.

Prevalece a norma comum **revisão 5**, recebida nos fontes atuais, sobre a cópia avulsa revisão 4. O plano anterior à implementação está em `planning/RELEASE-0110.md`. Requisitos mantidos: WordPress ≥6.4, PHP ≥8.1.2 de 64 bits, criptografia autenticada, InnoDB e travas nomeadas. Executados WordPress 7.1.3/PHP 8.3.6/MySQL 8.0.46 e WordPress 6.4/PHP 8.1.2-1ubuntu2.28/MySQL 8.0.46. O Site-Teste usa WordPress 7.1.3/PHP 8.3.36 conforme inventário recebido dos pacotes atuais. Identidades públicas, permissões administrativas, slug, basename, namespaces, prefixos e Update URI permanecem.

## 2. Convivência e encaminhamentos

| Pacote | Versão considerada | Prova própria e limite |
|---|---|---|
| Fator3 Site Core | 1.56.0 | Fonte, contratos, relatório e instalador; ativo nas três matrizes integradas, runtime exato |
| Fator3 MCP | 0.33.0 | Catálogo, executor original, permissões, redação de saída, auditoria e leitura documental; ativo nas três matrizes integradas |
| Fator3 MCP Meta | 0.12.0 | Fonte/relatório/contratos e convivência ativa; runtime exato; não se declara nova homologação das operações Meta |
| Fator3 MCP Google | 0.19.0 e 0.20.0 | 0.19.0 na integração inicial e upgrade; 0.20.0 recebido durante o fechamento e validado em uma matriz integrada adicional |
| Fator3 MCP Pipedrive | 0.1.0 e 0.2.0 | Fontes, relatórios, contratos e bytes instalados conferidos; inativo no laboratório PHP 8.3.6, inferior ao mínimo próprio 8.3.36; ativo no Site-Teste |

Google 0.20.0 e Pipedrive 0.2.0 foram observados já ativos antes da nossa instalação e recuperados para análise. O relatório recebido do Pipedrive ainda registra implantação bloqueada na sessão de origem; o inventário remoto posterior comprova 0.2.0 ativa, sem atribuir essa atualização a esta tarefa. A prova local com o novo Google passou com os mesmos bytes finais do LinkedIn. Não se extrapola a observação remota de Pipedrive para uma prova funcional local desse pacote.

**Impactos e pedidos emitidos nesta rodada: nenhum.** Foram avaliadas descoberta/autorização/transporte/documentação MCP, registro de auditoria de serviço, Lead Reader, adaptador CAPI do Core e isolamento das integrações. O novo histórico pertence ao LinkedIn e não publica um SDK a ser implementado por outro mantenedor. Não exige nova ordem de troca dos acompanhantes.

O impacto Google 0.20.0 → Core, revisão 1, Google 38/Core 313, foi lido: trata do novo leitor GA4 e do acervo do Core. Não solicita alteração no LinkedIn nem muda seus contratos. A retenção Pipedrive 0.2.0 também permanece local ao seu namespace. Os relatórios atuais Core/MCP/Meta não trouxeram ação obrigatória nova para o LinkedIn no escopo examinado.

**Tratamento de impactos recebidos e anteriores**, com desfechos somente neste relatório:

- **MCP 0.29.1 → LinkedIn, revisão 2:** mantém-se a idempotência conservadora; `retryable` não autoriza repetir uma escrita incerta. A coleta histórica tem chave de intenção, checkpoint e replay próprios. Provas: regressões nativas, replay do backfill/exportação e executor MCP 0.33.0. Responsável: mantenedor LinkedIn; sem nova ação neste encaminhamento.
- **Meta 0.7.1 → LinkedIn, revisão 4, Pedido LinkedIn 12:** atendimento anterior preservado. A primeira implementação de retenção desta rodada desviou do isolamento de jobs ilegíveis; a regressão detectou o problema antes da entrega. Corrigido reutilizando `Queue::isolateUnreadable`, travas e CAS existentes. As 18 provas concorrentes passaram em cada uma das cinco matrizes finais. Responsável: mantenedor LinkedIn; encerramento anterior mantido.
- **Core 1.48.0 → LinkedIn, revisão 2, Core 289:** permanece a exigência de regra de servidor `CONVERSIONS_API`, distinta do Insight Tag. Contratos e diagnóstico preservados nas regressões integradas. Implementação da interface permanece atendida; habilitação e aceite comercial da conversão real continuam com o dono/frota, sem alteração no Core.

Nenhum documento ou código do Core, MCP, Google, Meta ou Pipedrive foi editado. As seis árvores-fonte recebidas foram comparadas integralmente aos ZIPs; 15 comparações dos runtimes acompanhantes também passaram. Cópias de referência e identidades estão em `inputs/0.11.0/`. Não se gerou arquivo de impacto para anúncio, resposta ou encerramento. A baixa do pedido no documento central cabe ao revisor responsável.

## 3. Mudanças e evidência

| Pedido exato | Problema | Mudança | Resultado e evidência |
|---|---|---|---|
| 14(a) | Auditoria local fixa em 30 dias | Política própria configurável por MCP/painel; padrão `unlimited`; alternativa finita de 1 a 36.500 dias; prévia e revisão esperada | Evento com 100 dias preservado após manutenção; mudança finita simulada e confirmada; CAS e limpeza posterior testados; schema remoto confirmado |
| 14(b) | Conexões só aceitavam prazo finito | `retention_mode=unlimited`, padrão para conexão nova; escolhas finitas existentes preservadas, inclusive 3.650 dias | Defaults, intenção finita por dias explícitos, atualização da política e preservação de páginas antigas testados |
| 14(c) | Métricas só existiam nas páginas de coleta | Acervo diário cifrado, sem expiração, Pages e Ads; backfill retomável e exportações CSV/JSON autenticadas | Três relatórios de Página, pivôs campanha/criativo/conversão, datas anteriores à instalação, lacunas, replay, acesso e exportação testados com fornecedor interceptado |
| 14(d) | Atualização não podia apagar o acervo existente | Migração em lotes que conserva páginas de origem, ciphertext/revisões e escolhas explícitas; páginas bloqueadas ficam retidas para revisão | Upgrade real 0.10.1 → 0.11.0 preservou todos os registros semeados e importou métrica de 2020; rollback SQL da gravação histórica também testado |

São **90 operações públicas**, nove aditivas: `get-retention`, `save-retention`, `history-status`, `history-migrate`, `history-query`, `create-backfill`, `history-export`, `history-export-step` e `history-export-read`, todas sob `linkedin/`. `configuration-schema` expõe modo da conexão, política efetiva e schema de retenção. As configurações existentes recebem campos aditivos; a capacidade de janela longa fica restrita aos relatórios históricos pertinentes. Concessões, Lead Sync, CAPI e gestão comercial conservam suas fronteiras.

O acervo é particionado por principal, concessão MCP quando aplicável, conexão, canal, ativo e relatório. Cada leitura/exportação exige administrador e autorização atual; revogação, retirada do ativo ou pausa da conexão bloqueiam o acesso. Token vencido, isoladamente, não impede consulta local autorizada. Cursores se vinculam à seleção, revisão de autorização e geração do acervo. Dados permanecem cifrados e a exportação não cria URL pública.

As métricas usam o dia informado na resposta, identidade do ativo, dimensões/pivôs, moeda, versão da API e proveniência. A observação mais recente atualiza a mesma chave sem somar novamente o mesmo dado; observação antiga não sobrescreve a nova, e consultas com subconjunto de campos não apagam outras métricas. Agregados mensais, snapshots sem dia e identidades divergentes não viram séries diárias. Respostas vazias e descartes registram cobertura; ausência de dado não vira zero. A janela efetiva de cada página é guardada separadamente do plano total.

Backfill usa a fila existente, com janelas de sete dias, intervalo congelado e limite de páginas. Exige início explícito; não consulta datas futuras ou granularidade `ALL`. O código limita janelas conhecidas do provedor e devolve o ajuste; a disponibilidade diária real depende do relatório, aprovação e conta. O teto de retenção anunciado pela API não garante dados diários por todo o período. Referências oficiais Microsoft Learn, regras por relatório e exemplos estão em `docs/HISTORY.md`, consultadas nesta rodada.

Consulta local limita páginas e bytes. Exportação usa partes cifradas, leitura base64 com SHA-256 e teto de 64 MiB por exportação; divide-se o período para volumes maiores. A montagem JSON/CSV, proteção contra fórmulas e interrupção quando a geração histórica muda foram exercitadas. A cobertura publicada é explicitamente uma amostra recente, não prova de completude de todo o intervalo.

Comparação com a base: **cinco arquivos novos, 32 modificados, nenhum removido** no runtime. A revisão também corrigiu, antes da primeira instalação 0.11.0, ID duplicado no formulário de retenção e guardas de contexto/intervalo da ingestão. Uma falha preliminar de revogação estava no teste, que chamava entrada local em vez do executor MCP; o teste foi corrigido e passou pelo transporte adequado. Esses achados não exigem patch posterior, pois foram resolvidos antes da entrega desta nova versão.

## 4. Instalação e prova da troca

Instalador com **67 arquivos, 32 PHP e 29 documentos**, manifesto integral conferido e build reproduzido em árvore limpa com SHA-256 idêntico. `plugin/wp-mcp-linkedin-fator3/` no fonte reproduz exatamente o runtime do ZIP testado. O instalador é o único arquivo instalável.

| ID | Ambiente | Cenário | Resultado | Evidência em `evidence/release0110/` | Limite |
|---|---|---|---|---|---|
| L1 | WP 7.1.3/PHP 8.3.6/MySQL 8.0.46 | Limpa integrada, Google 0.19.0 | 224 aprovadas; 1 não aplicável | `final-integrated/` | Fornecedor/e-mail interceptados |
| L2 | Mesmo ambiente integrado | Atualização direta 0.10.1 → 0.11.0 | 225 aprovadas | `final-upgrade/` | Dados de fixture; preservação verificada antes das demais mutações |
| L3 | WP 6.4/PHP 8.1.2/MySQL 8.0.46 | Mínimos, LinkedIn isolado | 209 aprovadas; 4 não aplicáveis | `final-minimum/` | Abilities API/MCP ausentes nos casos correspondentes; upgrade não aplicável |
| L4 | WP 7.1.3/PHP 8.3.6/MySQL 8.0.46 | Limpa, LinkedIn isolado | 211 aprovadas; 2 não aplicáveis | `final-isolated/` | MCP e upgrade não aplicáveis |
| L5 | WP 7.1.3/PHP 8.3.6/MySQL 8.0.46 | Limpa integrada com Google 0.20.0 | 224 aprovadas; 1 não aplicável | `final-latest/` | Pipedrive 0.2.0 presente/inativo pelo mínimo PHP próprio |
| D1 | Executor MCP original 0.33.0 | Documentos completos em L1/L2/L5 | 90 verificações aprovadas; 29 documentos/36 páginas por matriz | `mcp-docs080.json` de cada matriz | Executor local, sem sessão HTTP remota |
| U1 | WordPress real, REST autenticado, jsdom 27.4.0 | Painel de identidade, retenção e histórico | 20 verificações aprovadas; sem erro JS | `final-integrated/ui011.json` | Sem inspeção visual completa em navegador |
| I1 | Três matrizes integradas | Integridade dos cinco acompanhantes | 15 árvores idênticas aos ZIPs recebidos | `companion-integrity.json` | Não equivale à homologação comercial de cada acompanhante |
| S1 | Site-Teste compartilhado | Atualização autenticada da 0.10.1 | 0.11.0 ativa; `applied=true`; sondas 200 antes/depois; selftest 9/9 | `site-test.json` | Reativação silenciosa em PHP novo, não ciclo completo de activation hooks |
| S2 | MCP remoto autenticado | Índice e leitura documental integral | 29 documentos, 30 páginas, 254.834 bytes, todos idênticos | `site-documentation.json` | Conteúdo documental local |

**Total funcional final: 1.093 verificações aprovadas, oito não aplicáveis e zero falhas**, além das 90 verificações documentais locais, 20 DOM e conferências remotas. Não inclui tentativas preliminares nem duplica os testes históricos recebidos. Todos os processos finais retornaram zero; os logs não contêm avisos/erros PHP próprios ou dos acompanhantes. Houve problemas de infraestrutura no arranque/reuso do MySQL descartável; foram resolvidos com banco isolado novo, sem alterar o plugin nem contar tentativas incompletas como aprovação.

Site: `https://fator3-teste-mcp-1.dreamhosters.com/`. Atualização por **`plugins/upload-base64`**, bytes exatos, `expected_slug=wp-mcp-linkedin-fator3`, SHA-256 da seção 8, `activate=true`, `overwrite=true`. Operação `8fafd439673c30d1ebb0421f`; pacote `e23a7c9c3c0dfd041fda0a8474ce2132`; pré-imagem `c9a83bffd9ab264e5d402ec5`. Sondas de mesma origem para `/` e `/wp-json/` retornaram 200 com bypass de cache verificado. Elas não demonstram acesso público externo nem prontidão comercial.

Prontidão: `linkedin/status {}` retornou `state=ok`, `issues=[]`, armazenamento/criptografia prontos, `unreadable_jobs=0` e registro central de serviço ativo. `linkedin/selftest {}` passou nas nove verificações. `configuration-schema` confirmou `finite/unlimited` e o schema da auditoria. `get-retention` retornou `audit_mode=unlimited`, revisão 0; o campo `audit_days=30` é somente o valor para eventual modo finito, não um prazo aplicado ao modo ilimitado. A política não foi alterada para finita durante o aceite remoto.

`history-migrate {}` terminou com `complete=true`, zero páginas e zero bloqueios; `history-status` confirmou a migração completa e acervo sem prazo. Há zero conexões e zero agendas ativas no Site-Teste. Não foram inseridas fixtures, auxiliares/MU-plugins, credenciais ou dados comerciais no site. A preservação de auditoria com 100 dias e coleta de datas anteriores à instalação está comprovada nos laboratórios, não em dados remotos inexistentes.

Inventário imediatamente antes/depois da instalação mudou somente o LinkedIn. Permanecem ativos Core 1.56.0, MCP 0.33.0, Google 0.20.0, Meta 0.12.0, Pipedrive 0.2.0 e os demais plugins observados. Nenhum arquivo de outro pacote foi sobrescrito. URL raw final: **não publicada/não utilizada**; a instalação ocorreu pelos bytes autenticados. Não houve push em GitHub nem atualização da frota.

## 5. Banco e volta de versão

A tabela de registros mantém schema 2. Acrescentada `{prefix}f3_linkedin_history`, schema próprio 1, com índices de partição, dia, paginação e cobertura. Novas opções: `f3_linkedin_history_schema` e `f3_linkedin_retention0110`. Buckets próprios guardam política, progresso da migração, geração, retenções para revisão e exportações. Detalhes em `HISTORY.md`.

A atualização cria a estrutura e protege a auditoria existente, sem remover registros. Preserva payloads cifrados, revisões, identidades, concessões, agendas e prazos finitos explícitos. Migração avança 25 páginas por passagem, incluindo páginas expiradas ainda fisicamente presentes; não elimina a origem. Páginas ilegíveis, sem dia válido ou sem autorização ficam retidas para revisão. Após corrigir a causa, `history-migrate` com `restart=true` reavalia idempotentemente.

Depois da migração, a manutenção pode aplicar a política finita já escolhida para resultados brutos, conservando as métricas no acervo. Escolher prazo finito de auditoria exige revisão e confirmação da prévia; salvar não remove imediatamente, mas autoriza limpeza posterior pela data original. Voltar a ilimitado não recupera registros já apagados. Tokens, confirmações, cursores e capacidades temporárias mantêm seus vencimentos de segurança.

Preservar backup de arquivos, banco e salts/chaves do WordPress. Desativar/desinstalar mantém os dados. **Reverter somente os arquivos para 0.10.1 não desfaz a migração e pode reativar a limpeza antiga, que não entende unlimited.** Para uma reversão fiel, interromper worker/manutenção e restaurar banco e salts do mesmo backup antes de reativar a versão antiga. O teste de rollback SQL histórico comprova atomicidade de uma gravação; não é um teste de downgrade completo de produção. Preferir correção adiante quando já houver novo acervo.

## 6. O que permanece pendente

| Pendência | Motivo | Responsável/próximo passo |
|---|---|---|
| Aceite integral do Pedido 14 no Site-Teste | Schema e política confirmados; não há conexão nem amostra real com mais de 30 dias | Dono/frota disponibiliza conexão autorizada; mantenedor confere manutenção com evento antigo e backfill real quando a API fornecer |
| Homologação de seguidores, visualizações, publicações e anúncios reais | HTTP do LinkedIn interceptado nos testes; quotas, escopos, granularidade e horizonte dependem da conta | Dono autoriza ativos e executa recortes conhecidos; comparar exportação com o fornecedor |
| Inspeção visual completa do painel | Foram exercitados HTML/JS/REST reais por DOM, sem navegador visual | Mantenedor/dono confere apresentação no navegador |
| Prova local ativa do Pipedrive 0.2.0 | Runtime local 8.3.6 abaixo do mínimo próprio 8.3.36 | Mantenedor/frota, se precisar de homologação combinada completa; observação remota ativa não substitui essa prova |
| Aceites comerciais anteriores de credencial e CAPI | Não fazem parte da retenção local e não foram executados nesta rodada | Dono/frota, com regra de servidor e concessões adequadas |
| Distribuição para outros sites e URL raw | Esta entrega atualizou apenas o Site-Teste | Frota, sob sua autorização e conferência dos hashes |

Não há achado técnico conhecido restante nos cenários executados. Não se declara ausência de impacto em toda combinação possível, bancos diferentes, volume de produção ou serviços externos não homologados. O pedido central permanece com seu revisor para considerar essas pendências.

## 7. Credenciais e configuração do dono

Sem credenciais novas para a retenção/acervo local. Configuração em **Ferramentas → Fator3 MCP LinkedIn**: aba Retenção para auditoria; modo da conexão para coletas; aba Histórico e ação de coleta retroativa para acervo. As escolhas finitas existentes não são convertidas silenciosamente para ilimitadas.

Pelo MCP, ler `get-retention`, simular `save-retention` com `expected_revision`, `audit_mode` e `audit_days` quando pertinente, e confirmar com `dry_run=false` após avaliar a prévia. A omissão de `dry_run` mantém simulação. Para resultados, usar o fluxo de revisão/salvamento de conexão existente com `retention_mode`.

Backfill requer conexão LinkedIn válida, aprovação dos produtos/escopos de leitura pertinentes e seleção explícita de Página/conta Ads. Usar os campos e a verificação de credencial existentes; nenhum segredo deve ir para o relatório/chat. O histórico de conversões Ads usa leitura analítica por pivô e não envia conversões à CAPI. Acesso ao acervo continua sujeito à autorização atual, mesmo sem chamada ao LinkedIn.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `wp-mcp-linkedin-fator3-0.11.0-instalador.zip` | 283053 | `34541afa67c0991e9dc0b5474ab8678dff8cf806eace6ceb1edb47983f9e0308` |
| Fonte | `wp-mcp-linkedin-fator3-0.11.0-fonte.zip` | 1490342 | `5048b99a73ed9ec2beed7545832b13d88d63dafe432100722f2989eb86ee493e` |

O fonte contém uma única raiz `wp-mcp-linkedin-fator3-0.11.0-fonte/`, runtime idêntico ao instalador, build, testes, documentação, insumos e evidências sanitizadas. Sem ZIP aninhado, banco, wp-config, credenciais reais, runtimes externos ou node_modules. Os artefatos históricos recebidos ficam identificados como histórico, sem serem somados às provas desta rodada. O fonte não será reaberto para inserir seu próprio hash. Somente o instalador deve ser instalado; três artefatos principais, nenhum impacto novo.
