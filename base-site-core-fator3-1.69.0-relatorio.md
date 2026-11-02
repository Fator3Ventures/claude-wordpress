# Entrega — Fator3 Site Core 1.69.0

Revisão 1 — 02/11/2026, America/Sao_Paulo. Nova versão minor sobre a base canônica 1.68.0, para os novos pacotes/pedidos e normas Fator3 revisão 5. Status: **com-pendencias**, restritas à validação do piso PHP 8.3.0 exato, navegador e aceites reais da frota/fornecedor descritos na seção 7. Implementação e instalação autorizada no Site-Teste concluídas; apta ao escopo efetivamente testado. Contrato administrativo 8.32.0.

## 1. De onde a versão entra

Instalação WordPress limpa e atualização direta 1.68.0 → 1.69.0. A base foi recuperada dos artefatos canônicos da entrega anterior, sem reconstrução a partir do site. Instalador base: 4231467 bytes, SHA-256 `afff3783f11aff3395e2a37cd3938958d93dfe1d01e5e566789f1333ccf134a8`; fonte base: 8558916 bytes, SHA-256 `9a92b147526dd9aae4fd1755472aed2cb996a4529f26837b727a5993d6244ec1`. O relatório anterior de implantação, revisão 2, está preservado em history/1680. Não foi criada versão intermediária nem ensaiado downgrade.

Cabeçalho atual: `Requires PHP: 8.3`, `Requires at least: 7.1.4`. Ambiente local efetivamente testado: WordPress **7.1.4**, PHP **8.3.6 de 64 bits**, MySQL **8.0.46**, WP-CLI **2.12.0**. PHP 8.3.0 exato não foi executado; não declarar seu piso validado por extensão. Site-Teste observado nesta rodada: WordPress **7.1.4**, PHP **8.3.36**, banco **8.4.11-0ubuntu0.26.04.1**. O WordPress identifica esse ambiente como production, mas trata-se do Site-Teste explicitamente autorizado pelo dono.

Insumo de pedidos: `Fator3 Site Core(20261102-145517).md`, 12426 bytes, SHA-256 `a489e6c1a748546c20e168a923062007d27c761486709d5149862e864c9737ca`. Instalador LinkedIn 0.17.1 recebido: 379078 bytes, SHA-256 `e3a6c06d2c254a50af60e434a0575424e552ed4f62422ea1aabcff6bd591f1f9`. Fonte recebido: SHA-256 `a7a96acae25a6d4003548677b5b14ff7c8769f216c4440178558cf948002c163`. Relatório e impactos LinkedIn 0.16.0 revisão 3 / 0.17.1 revisão 2 lidos; seus hashes e os demais insumos constam em inputs/1690/manifest.json. As instruções do projeto foram relidas integralmente e as duas normas revisão 5 integram a documentação instalada.

## 2. Convivência e impactos

| Pacote | Versão atual | Evidência própria |
| --- | --- | --- |
| Fator3 MCP | 0.38.0 | Ativo na bancada e Site-Teste; catálogo/abilities, leitura integral local de documentos e instalação remota |
| Fator3 MCP LinkedIn | 0.17.1 | Código oficial sem alteração; descoberta, adoção e campanha exercitadas com HTTP sintético; ativo no Site-Teste |
| Fator3 MCP Google | 0.26.0 | Ativação conjunta local e conservação no Site-Teste; sem novo ensaio de API real |
| Fator3 MCP Meta | 0.19.0 | Ativação conjunta, regressões de catálogo/coleção e conservação no Site-Teste |
| Fator3 MCP Pipedrive | 0.5.0 | Ativo no Site-Teste; ciclo automático confirmou a conta. Não ativado no PHP 8.3.6 local, pois declara 8.3.36 |

A fronteira alterada é Core → LinkedIn: consumidor atual `linkedin-lead-reader/1.2.0`, extensão `linkedin-lead-campaign/1.0.0`, método `resolve_campaign`, dados de assinatura adotados pela `ownership_key` canônica. Instalar primeiro LinkedIn 0.17.1 quando o site ainda não o tiver, depois Core 1.69.0. No Site-Teste o produtor atual já estava ativo. Nenhum pacote acompanhante foi editado ou redistribuído.

O impacto emitido pelo Core 1.68.0 para obter o nome de campanha está **resolvido no contrato/código**: o produtor oficial recebido fornece a interface e o consumidor 1.69.0 a utiliza e testa. Os impactos recebidos LinkedIn 0.16.0 revisão 3 (consulta pública) e 0.17.1 revisão 2 (adoção e projeção de campanha) foram atendidos neste escopo. Os comprovantes antigos permanecem no histórico; encerramento técnico não equivale ao aceite em conta real. Não há nova adaptação demandada a outro plugin nem novo relatório individual de simples aviso. Fronteiras MCP administrativo, parceiro Pipedrive por plataforma e catálogo Meta foram verificadas no alcance descrito; desempenho geral e demais serviços permanecem não reavaliados nesta rodada, sem risco concreto novo identificado.

## 3. Mudanças por pedido e evidências

| Pedido | Problema e resultado | Estado e prova |
| --- | --- | --- |
| Pedidos core 369(d) | Nome ausente passa a ser consultado pelo SDK público do LinkedIn. Mapa local e nome decorado válido têm precedência. Parceiro continua no mapa existente parceiros_plataforma.linkedin_ads; ocorrência solicita completar o mapa | implementado, validado-localmente e validado-wordpress; 60 verificações do cenário novo incluem nome vindo da API Ads com usuário 0. Não homologado-fornecedor |
| Pedidos core 369(f) | Modo automático operava somente os eventos recebidos. Agora mantém a união entre selecionados e descobertos autorizados, sem retirar os selecionados numa descoberta parcial | implementado, validado-localmente e validado-wordpress; quatro formulários operam antes do primeiro evento, com cursores preservados |
| Pedidos core 369(g) | Evento failed sobrescrevia recibo confirmed. Agora conserva o recibo confirmado, registra descoberta_pendente e adota a chave canônica fornecida pelo produtor | implementado, validado-localmente e validado-wordpress; quatro recibos 1.1 adotados, zero POST adicional; evento failed posterior não degrada o recibo |
| Pedidos core 369(h) | Teste anterior começava sem formulários. O cenário novo começa com quatro selecionados e quatro recibos 1.1, ativa todos e inclui um quinto | validado-wordpress com produtor PHP oficial/HTTP sintético; falta aceite externo com as assinaturas reais da frota |
| Pedidos core 368/370 | Preservação dos comportamentos entregues: conflitos duráveis, comparação textual, continuidade e renovação do catálogo Meta | regressões: 14 + 11 + 12 verificações. Itens não reabertos no escopo do pacote |

Arquivos principais: `class-f3base-linkedin.php` (união/ingestão/diagnóstico), `class-f3base-linkedin-descoberta.php` (preservação de recibos), `class-f3base-linkedin-cliente.php` (contrato atual e extensão), novo `class-f3base-linkedin-campanhas.php` (diário, consulta, preenchimento, recuperação), `class-f3base-linkedin-integracoes.php` (schema facultativo), `class-f3base-operacao.php` (job), cadastro de autoload/bootstrap e documentação. Runtime: três arquivos adicionados, 31 alterados, nenhum removido; lista exata em evidence/1690/runtime-diff.json.

A consulta remota pode consumir 25 segundos. Ela roda numa tarefa própria `f3base_linkedin_campanhas`, sob a tarefa anuncios do executor, com uma consulta por execução e pelo menos 27 segundos disponíveis; não aumenta a janela de 20 segundos da captura. Diário na tabela existente `f3base_linkedin_webhook`, tipo campanha, com payload cifrado de identidade/revisões/auditoria, sem respostas pessoais. Falha de persistência do diário impede avanço do cursor; reentrada permanece deduplicada. Nenhuma nova tabela ou coluna.

Tentativas configuráveis por integração em `campanhas_retry`: padrões max_tentativas=3, intervalo_segundos=300; limites 1–10 e 60–86400. Usa configuração administrativa com simulação/revisão; registra política e revisão utilizadas. Respeita retry_after do produtor. Estado revisao distingue falha, permissão, identidade ou mudança de contexto. `f3base/linkedin-campanha-reabrir` exige manage_options, prévia, revisão e motivo; registra responsável, instante e contagem anterior, sem ampliar a concessão.

Preenchimento local valida conta/formulário/resposta/submittedAt/campanha, credencial/concessão/configuração e identidade do contato. Transação bloqueia recibo e contato; preserva nome existente, lixeira e eliminação. Altera somente nome de campanha vazio e metadados de enriquecimento/revisão. **Não reenvia avisos, CRM ou conversões.** O nome pode ser preenchido depois da captura; uma entrega comercial já realizada não é reenviada para receber esse enriquecimento. O cliente direto Core continua disponível por escolha explícita, sem fallback automático; a extensão de consulta depende de linkedin_plugin atual. Não há negociação operacional com versões antigas do produtor; recibos 1.1 são histórico de migração.

## 4. Instalação e prova de prontidão

Verificações locais:

- 594 arquivos PHP aprovados no lint, com PHP 8.3.6.
- 130 verificações funcionais: request-368 (14), request-369 herdado (33), request-369-1690 (60), request-370 (11) e request-370-collector (12).
- Documentação pelo método público: 179 documentos, 795 páginas e 2078 asserções, mais duas contagens de cobertura, registradas em docs-1690.json (2080 entradas). Schemas das 192 abilities e das 102 opções operáveis gerados do registro real; nenhum HTTP na leitura documental; assinante e anônimo recusados.
- WordPress nativo: instalação limpa e atualização direta do ZIP exato sobre a base canônica 1.68.0; primeira passagem por WP-CLI --due-now concluiu a atualização. Preservação de configurações, segredos sintéticos, callback, cursores e dados populados; repetição idempotente; desinstalação com preservação seguida de reativação da mesma versão. Estruturas: 70 tabelas. Nenhum ensaio de downgrade.
- O ZIP testado foi comparado arquivo a arquivo com o runtime do fonte: 918 arquivos idênticos.

Site-Teste: https://fator3-teste-mcp-1.dreamhosters.com/. Autorização explícita do dono para atualizações/modificações necessárias. Inventário antes: Core 1.68.0 e oito outros plugins ativos. Transferência autenticada `files/upload-create` + 17 chamadas `files/upload-part` + `files/upload-finalize`; servidor confirmou 4256023 bytes e SHA-256 `8659ce0e526d378cf8424d0ff42deed660fee9f957be08f2bf26a74ce7f52996`. Transferência `71f56de1e7c55b3c32b1c0135610a6ad`; finalização `0776fe10c62bb6101f196457`.

Instalação por `plugins/upload-base64`, zip_path do arquivo recebido, expected_slug=base-site-core-fator3, expected_sha256 acima, activate=true, overwrite=true, timeouts 20 segundos e chave idempotente própria. Operação `2958b85fc4b511893825371b999f4322`; pré-imagem `de949947cf6fea246657b646` preservada. `plugins/operation-status`: complete, verified, file_state=candidate, versão 1.69.0 e ativo. Sondas internas GET `/` e `/wp-json/`: HTTP 200 antes/depois, bypass de cache comprovado em processo PHP novo. São provas da mesma origem, sem certificação de acesso externo nem benchmark comparável de desempenho.

A reativação silenciosa do instalador não foi tratada como comprovação do ciclo funcional. `f3base/saude-ler {compacto:true}` confirmou separadamente atualização concluída em **2026-11-02T12:35:17-03:00**, contrato 8.32.0, falha null, recuperação core_operacional sem pausa, zero avisos; cabeçalhos e navegação verificados. O ciclo automático confirmou a conta Pipedrive existente, sem teste de criação de contato. `system/health {compact:true}`: healthy=true, zero recuperações pendentes e zero incidentes indexados em 24h.

Documentação instalada: nove documentos completos (índice, release, agentes, LinkedIn, contratos, configuração, operação e as duas normas atuais), 11 páginas/978 linhas, com versão 1.69.0 e hashes/conteúdos idênticos ao ZIP. A nova ability linkedin-campanha-reabrir foi descoberta com schema real. Não foi criada conexão de campanha no Site-Teste; ele continua sem conexão LinkedIn para aceite real.

Limpeza: removido somente o ZIP temporário `wp-content/uploads/f3base-core1690-8659ce0e526d.zip`, com guarda do hash, operação `083b9c830363d11a732754db`. Os oito acompanhantes conservaram versão e ativação, inclusive DreamHost Panel Login 1.0.0, WP Super Cache 3.1.4 e Yoast SEO 28.8. Sem envio de mensagens a terceiros, push Git ou publicação de fonte em URL pública. A publicação/distribuição na frota continua sendo responsabilidade da frota.

## 5. Banco, migração e correção por nova versão

Sem DDL novo e sem migração destrutiva. Campos facultativos de configuração não alteram escolhas existentes. Diário de campanha e estado de descoberta seguem a preservação das estruturas atuais; contato já preenchido/descartado/eliminado não é recriado pela tarefa. O backup operacional continua o inventário existente; a pré-imagem remota preservada é de arquivos e **não equivale a backup do banco**. Esta rodada não restaurou nem exportou banco real.

Não há downgrade nem obrigação de schema reverso. O instalador 1.69.0 ficou imutável após a instalação. Qualquer correção posterior precisa de nova versão patch, construída da entrega vigente, testada em instalação limpa e atualização direta. Para recuperar consulta de campanha após corrigir permissão/fornecedor, usar a reabertura com motivo/revisão, sem apagar recibos, restaurar dados antigos ou contornar concessões.

## 6. Evidências e prontidão do consumidor

Evidências atuais em `evidence/1690`: installer.json; request-*.json; docs-1690.json; native-cycles-1690.json; runtime-diff.json; site-before.json; site-install.json; site-environment.json; site-documents.json e site-docs-verification.json. Os testes usam o código original do LinkedIn 0.17.1. Não foi necessária alteração experimental do destinatário, pois o contrato oficial já atende ao consumidor. O plano foi registrado antes da implementação e atualizado no fechamento. Histórico de impactos e relatório base preservado, sem converter evidência anterior em teste desta rodada.

## 7. Pendências de validação e responsáveis

1. **Frota/ctooffice — aceite real do 369:** ativar o modo por simulação/revisão com concessões válidas; confirmar operação dos quatro formulários e assinaturas reais 7407569, 7426857, 7453057 e 7484137; criar novo formulário autorizado e observar entrada automática e lead anterior à primeira passagem. Nenhuma dessas assinaturas reais foi manipulada nesta rodada.
2. **Frota/fornecedor — campanha:** comprovar nome e parceiro com a conta real, permissões campaign_lookup/responses, ads/leads e r_ads ou rw_ads. Testes sintéticos aprovam a integração de código, não o acesso do aplicativo ao LinkedIn. A latência depende de WP-Cron; enriquecimento tardio não reenvia entrega comercial passada.
3. **Manutenção do pacote — piso PHP:** executar PHP 8.3.0 exato se for exigida comprovação daquele patch; foram executados 8.3.6 local e 8.3.36 no Site-Teste. WordPress 7.1.4 declarado foi testado diretamente.
4. **Navegador:** não houve nova inspeção visual em navegador autenticado. Alterações do painel são textos e diagnóstico existente; o fluxo operacional foi exercitado em PHP/abilities. Não declarar aceite visual novo.
5. **Frota — pendência 20 e metas herdadas:** aceites reais dos itens já entregues e metas de bytes/desempenho continuam no acompanhamento da frota, conforme insumo atual. Não reabrir 365–368/370 como desenvolvimento pendente nem declarar metas concluídas. Documento central de pedidos não foi editado.

## 8. Credenciais e configuração exigidas

Nenhum segredo real exportado ou alterado. Para o novo caminho, manter no painel do Fator3 MCP LinkedIn a conexão selecionada (`connection_id`), token de acesso, identificação/segredo do aplicativo e contas autorizadas. A concessão do consumidor Core precisa de metadata, responses, verify, subscriptions para a descoberta; campaign_lookup e responses para campanha, conta em leads e ads e escopo r_ads ou rw_ads. O callback HTTPS continua o emitido pela integração Core. No Core, configurar campanhas_retry e o mapa existente por canal administrativo com simulação/revisão; o parceiro vem de f3base_pipedrive.parceiros_plataforma.linkedin_ads. Não informar valores secretos no relatório, fonte ou diagnóstico.

Bancada: credenciais/identidades sintéticas, HTTP e e-mail externos bloqueados. Fonte exclui laboratórios, dumps, logs brutos, binários de desenvolvimento e pacotes acompanhantes; dependências próprias necessárias ao runtime permanecem. A documentação e as evidências não contêm tokens de produção.

## 9. Identidade dos arquivos finais

| Arquivo | Bytes | SHA-256 |
| --- | ---: | --- |
| base-site-core-fator3-1.69.0-instalador.zip | 4256023 | `8659ce0e526d378cf8424d0ff42deed660fee9f957be08f2bf26a74ce7f52996` |
| base-site-core-fator3-1.69.0-fonte.zip | 5728084 | `2c4e19805fb78bfdef16f434559e9908004d1b7260613e82925f813aa826e4ee` |

[base-site-core-fator3-1.69.0-instalador.zip](sandbox:/workspace/scratch/e0ec4f78aa38/core1690/release/base-site-core-fator3-1.69.0-instalador.zip) · [base-site-core-fator3-1.69.0-fonte.zip](sandbox:/workspace/scratch/e0ec4f78aa38/core1690/release/base-site-core-fator3-1.69.0-fonte.zip).

O relatório externo é canônico. A cópia interna no fonte é anterior ao fechamento e contém marcadores explicativos, evitando referência circular ao hash do próprio ZIP. Este relatório, fonte e instalador compõem a entrega; não há novo impacto individual sem ação pertinente.
