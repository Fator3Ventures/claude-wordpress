# Entrega — Fator3 MCP Google 0.22.0

Revisão 1 · 28/10/2026 · America/Sao_Paulo. Slug/basename `wp-mcp-google-fator3/wp-mcp-google-fator3.php`. Base direta **0.21.0**. Referência nova: **Pedidos Core 323**, impacto Core 1.58.0→Google revisão 2; sem inventar numeração de pedido Google.

**Implementada e ativa no Site-Teste; versão corrente desta entrega.** Sem regressões identificadas nos cenários exercitados. Há pendências de incorporação do patch Core e homologação Google real. A atualização não concede ações nem envia conversões automaticamente.

**Relatório externo canônico, fechado após o fonte.** A cópia interna está identificada como anterior ao fechamento e não contém o hash do próprio ZIP. Runtime, instalador e evidências são os mesmos.

## 1. Base e entradas aceitas

Base Google 0.21.0 exata: instalador 836.718 bytes, SHA-256 `25da9ef78e303f30ce2f73b8f98743a26e09b8ed238177474e4a956578a63814`; fonte 5.345.878 bytes, SHA-256 `ebbd0be2946eb3b32240c2390c04d3887f55f3a7a15ac1deda38759e3d661c81`. Entrega anterior preservada.

Pacotes/relatórios novos examinados: Core1.58.0, MCP0.34.0 e Meta0.13.0; ZIPs conferidos por CRC e SHA-256. Instaladores:

| Pacote | SHA-256 recebido |
|---|---|
| Core1.58.0 | `71bf6497a2f2e2c605baf64f0f82c273201915039506b58ac220fc572afbd5e4` |
| MCP0.34.0 | `5d96b6a33cfc4a7c729c106268f4bc9d8938b34384da022345d7b7dae611a295` |
| Meta0.13.0 | `3ecd6ee6f277c7581adc05b4fa38c46611e3232b4400bb4a4421956c9fba8ac1` |

Inventário completo dos anexos/fontes/relatórios: evidence/022/inputs-received.json. LinkedIn0.11.0 e Pipedrive0.2.0 continuam insumos locais da base; também lido o relatório Pipedrive0.3.0, que acrescenta relatório agregado por seu cliente Core, sem demanda dirigida ao Google. Sua identidade recebida no relatório é 30fc784a552a89351900c169fad7300759163fb886b842f45ba807bb0977f657; esse hash não é apresentado como medição própria do ZIP0.3.

Normas comuns revisão5 aplicadas, prevalecendo sobre cópias avulsas rev4. Plano history/022/PLANO.md anterior à implementação; impacto criado no planejamento e revisado quando o patch consumidor entrou no escopo. Mínimos próprios mantidos: WordPress7.1.2/PHP8.3.6; testes MySQL8.0.46. Mesmo slug, prefixos, permissões, namespaces, Text Domain e Update URI.

## 2. Convivência e encaminhamento ao Core

Matriz principal: **Core1.58.0, MCP0.34.0, Meta0.13.0 e LinkedIn0.11.0 originais**, sem alteração de seus arquivos; inventários comparados aos instaladores. Pipedrive0.2.0 não foi ativado no PHP8.3.6 porque exige8.3.36. Não foi criado requisito de presença/versão/ordem dos acompanhantes para instalar o Google.

**Core316/Google39:** Core1.58.0 já implementa o consumidor enhanced1.1. Seu montador real também foi exercitado no fluxo comercial com dados sintéticos, incluindo caso sem clique. Encerrada a pendência de implementação do consumidor registrada na entrega anterior; permanece o aceite Google real. Isso é desfecho no relatório, sem reemitir o impacto histórico por confirmação de atendimento.

**Core323:** Google entrega o produtor1.2, as concessões por ação e confirmação assíncrona. O Core1.58 original só processa pendentes e deixa os recibos comerciais incertos. Essa consequência concreta motivou o novo impacto `wp-mcp-google-fator3-0.22.0-impacto-base-site-core-fator3.md`, revisão2, não uma simples mudança de versão/hash.

Conforme orientação de implementar dependências Core sem aguardar retorno, **o consumidor de reconciliação também foi implementado e testado**. Está em `integration/core323/`: diff aplicável, arquivo completo, instruções e hashes. Modifica apenas class-f3base-qualidade-destinos.php sobre a base1.58.0. SHA-256 do diff `a10ef8971a47ac38950e6759aa80b378380021a2e388f8fc1c23e252602d2eaa`. O worker consulta até dois incertos Google após1800s, reserva o intervalo antes da chamada, renova a trava, exige configuração/ação/referência e extensão exatas, sem reconstruir dados pessoais ou chamar sendBound. Mantém incerto em revogação, ausência de suporte ou erro; admite consulta com prova de envio expirada. Não muda banco nem numera uma release oficial Core.

**Nenhum arquivo Core foi alterado no Site-Teste.** O mantenedor Core deve incorporar o patch em sua próxima versão e executar seus gates completos. A prova com esse patch está separada da coexistência com o Core original. Nenhuma mensagem externa, publicação GitHub ou distribuição na frota foi realizada.

## 3. Mudanças implementadas

Contrato opcional `site-conversion-delivery/1.2.0` no quarto argumento de f3base_conversoes_adaptador, com consumer_id=site-core-quality, purpose=crm_stage e ação completa exata. Aquisição1.0/1.1 e GA4 preservados. Capabilities locais anunciam aquisição exata ou null somente quando sua ausência é comprovada; corrupção, ambiguidade, reutilização e divergência bloqueiam. Nenhum fallback de ação.

Concessão independente por conexão/conta/ação/consumidor/finalidade/identidade/geração, com CAS e trava compartilhados. Sem herança da aquisição. Até100 ações armazenadas por conexão. Prova por ação por24h; renovação prevista12h, até duas ações por conexão/passagem, orçamento e backoff; auditoria/diagnóstico sanitizados. Revogação e troca de identidade são reavaliadas antes de cada HTTP. A agregação de renovação no executor foi corrigida antes do fechamento para que sucesso comercial não virasse falso erro do cron.

Quatro habilidades novas, com painel próprio:

| Habilidade | Efeito |
|---|---|
| google/stage-conversion-status | leitura local, sem Google |
| google/configure-stage-conversion | concessão/revogação local |
| google/verify-stage-conversion | leitura/validateOnly no Google, prova e auditoria locais |
| google/reconcile-stage-conversion | consulta do recibo remoto e atualização local, sem reenvio |

Payload fechado publicado em docs/stage-conversion-payload.json: event_id é a identidade estável da conversão, order_id igual a event_id, contato/etapa/ação/data vinculados, RFC3339 não futuro e até7dias, um clique no máximo, consentimento GRANTED. Sem clique exige identificador pessoal válido e enhanced pronto na ação exata. **Valor fixo zero/BRL**; verificação recusa ação que force padrão incompatível, sem modificar a ação Google.

Data Manager permanece o transporte: um evento por pedido, reserva durável antes do HTTP e deduplicação por site/ação/evento, inclusive após reconcessão. Email/telefone/clique e hashes pessoais não são persistidos pelo Google; hash do contexto técnico não contém esses identificadores. Ingestão aceita é incerto, não entregue. A extensão `site-stage-conversion-reconcile/1.0.0` e reconcileBound(event_id,destination_ref) confirmam só um evento no destino exato, respeitando cooldown e concessão. A operação administrativa Google não altera a tabela Core.

**294 habilidades:113 de leitura e181 de escrita;38 opções.** Configuração4.0.0, execução/armazenamento2.0.0 mantidos. Todos os290 nomes, schemas e efeitos públicos anteriores foram comparados com Google0.21 sob MCP0.34; não mudaram. Há10 arquivos de runtime alterados/adicionados, incluindo StageConversionDelivery.php e documentação compilada; hashes em runtime-changes.json.

Referências primárias consultadas: [events.ingest](https://developers.google.com/data-manager/api/reference/rest/v1/events/ingest), [requestStatus.retrieve](https://developers.google.com/data-manager/api/reference/rest/v1/requestStatus/retrieve) e [ValueSettings](https://developers.google.com/google-ads/api/reference/rpc/v22/ConversionAction.ValueSettings). Prova sintética valida o contrato implementado; não comprova entrega/atribuição na conta real.

## 4. Testes, instalação e prontidão

| Prova | Resultado |
|---|---:|
| PHPUnit9.6.37/PHP8.3.6, suíte completa | **1257 testes,15021 asserções; zero falhas/erros/skips** |
| Casos unitários novos, incluídos acima |33 testes,243 asserções |
| clean | 2798 |
| upgrade | 2765 |
| clean-713 | 2739 |
| google-first | 1325 |
| isolated | 1130 |
| Total nativo, cinco cenários |**10757 verificações** |
| Contratos auxiliares ausente/incompleto/matriz/resposta |60 verificações |
| Core1.58 + patch proposto, laboratório separado |**59 verificações** |
| Lint do runtime |161PHP válidos;165 arquivos |
| Documentação |49 documentos de origem,51 exemplos,158 links;21 documentos instalados |

Os cinco grupos finais consolidam duas execuções com a mesma identidade de código/testes/ferramentas e os mesmos bytes. Cada relatório filho e ambiente foi conferido; processos encerrados, inventário do candidato exato e zero avisos/erros PHP Google. Provas em evidence/022/validation022.json, final-a/, final-b/, core-patch/ e unit-junit.xml. As contagens incluem comparação individual de schemas/eventos; não representam conversões reais.

Novo fluxo:51 verificações por ambiente integrado, com Core original e transporte Google interceptado; prévia local, consentimento/tráfego/data, userData sem clique, ação e evento distintos,0/BRL, incerteza, repetição, revogação após reserva e confirmação no produtor sem reingestão. No Core original a falta de reconciliação automática é observada expressamente. Patch:56 verificações funcionais mais3 de aplicação/identidade; mesmo recibo Core confirmado, cooldown, processing, revogação e consulta com prova de envio expirada. Não são testes completos de uma nova release Core.

Painel renderizado em WordPress e exercitado com jsdom27.4.0; os controles comerciais são conferidos pela renderização nativa. Sem inspeção visual em navegador. Documentos íntegros reconstruídos via MCP HTTP nos laboratórios. No Site-Teste, todos os21 hashes/tamanhos do índice coincidem com o fonte; README, guia, CONTRACTS e payload comercial foram lidos integralmente e comparados byte a byte.

Preliminares: ajustes nas fixtures de tokens OAuth/constante de tempo/capacidade do administrador e nas expectativas de auditoria; descoberta e correção da agregação de renovação comercial no cron. A primeira matriz parou no DOM porque NODE_PATH não apontava jsdom; execução final usa a dependência fixada. Tentativas preliminares permanecem identificadas e não entram nos totais aprovados. Não houve mudança de runtime depois da instalação final.

**Site-Teste:** <https://fator3-teste-mcp-1.dreamhosters.com/>. Atualização0.21→0.22 por plugins/upload-base64, slug/SHA-256 esperados, overwrite/activate, pré-imagem recuperável. Operação/pacote `ac8e30618fa01a27015bdef46e4a5494`, backup `5753081ae2f321913e71b117`; applied=true, ativo e nova requisição PHP confirmados. Home e REST200 antes/depois, bypass de cache; escopo interno mesma origem, sem inferência de acesso público externo. system/health healthy=true.

Configuração antes/depois idêntica, revisão `12a9d64f8d91a1292ddcd7e6ac497362abe1b9b6cf7c489699d7f6b7b37c3efe`; retenções0 preservadas. **80 eventos de auditoria anteriores idênticos**. Nenhuma concessão/configuração Google foi criada. Status comercial anuncia1.2, actions vazio; ação sintética consultada retorna stage_grant_missing, aquisição null comprovada, google_checks_performed=false. Não foi disparado evento real nem criada sonda temporária nesta rodada.

Inventário final compartilhado: MCP0.34.0, Core1.57.1, Google0.22.0, Meta0.13.0, **LinkedIn0.12.0**, Pipedrive0.3.0. LinkedIn mudou de0.11 para0.12 por outra sessão antes da troca Google; não foi sobrescrito. O pacote/relatório0.12 não integrou os insumos de bancada desta rodada; sua convivência é observação remota de inventário/saúde, não homologação funcional própria. Core remoto permanece1.57.1: o teste Core323 foi realizado localmente com1.58 original e, separadamente, com o patch proposto.

## 5. Banco, conservação e reversão

Sem nova tabela, opção catalogada, segredo ou migração destrutiva. stage_actions fica na configuração de conversões existente; recibos e auditoria usam estruturas atuais. Atualização direta, rollback de arquivos para0.21 e reaplicação preservaram sentinelas, credenciais sintéticas e registros de teste.

Reverter arquivos não desfaz envio nem resolve recibo incerto. Antes de voltar para0.21, suspender destinos comerciais no Core, preservar banco/salts/recibos e reconciliar quando autorizado. Não apagar recibos nem gerar event_id novo para repetir a mesma conversão. O patch Core pode ser revertido pelo arquivo-base identificado; estados já confirmados permanecem e incertos deixam de ser consultados automaticamente.

## 6. Pendências e responsáveis

- **Mantenedor Core:** incorporar o patch testado e publicar sua release com gates próprios; no Site-Teste, decidir atualização Core separadamente. A implementação está entregue, não aguardando retorno para ser escrita.
- **Dono da conta/frota:** conceder e verificar ações comerciais exclusivas, confirmar consentimento, termos/enhanced e homologar primeiro evento real0/BRL e consulta confirmada. Conta Google não está configurada no Site-Teste; nenhum aceite comercial foi inferido das fixtures.
- **Aceites anteriores:** primeiro contato enhanced de ctooffice, credenciais e diagnóstico de próximo incidente real continuam dependentes do operador; não reconstituídos retroativamente. Core316 não permanece como pendência de código do consumidor.
- **Distribuição/limites:** sem publicação GitHub/frota; LinkedIn0.12 e Pipedrive0.3 não tiveram testes funcionais de fornecedor nesta entrega; outros bancos, multisite e navegador visual não foram homologados.

## 7. Credenciais e permissões

Nenhum segredo novo emitido. Mantidos SA/OAuth, developer token Ads e escopo Data Manager, conforme configuração existente; cada concessão exige administração atual e identidade/política autorizadas. Consentimento e elegibilidade do contato pertencem ao Core e são revalidados no envio. Instalação não habilita serviços, concedentes ou contas. Laboratórios só usam dados/credenciais sintéticos e HTTP interceptado; ZIPs/evidências não incluem banco, wp-config, salts, cookies ou segredo real.

## 8. Identidade dos arquivos

| Artefato | Nome | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador WordPress | wp-mcp-google-fator3-0.22.0-instalador.zip |856534|`a84754409f89b7b9c7367c1d261c44ef93c2f6039b379c3ec5c6242ec7188ebd`|
| Fonte completo | wp-mcp-google-fator3-0.22.0-fonte.zip |5989075|`1d9ba106eb9ababad67b964fa4ad44246acc27eeda3e83e7866ea57386d77abf`|

Relatório e impacto são arquivos adicionais. Apenas o instalador é instalável. Fonte inclui runtime idêntico, docs editáveis, build, testes, plano/entradas, evidências sanitizadas, patch Core e reprodução em reproducao/LEIA-ME.md; sem ZIP aninhado, vendor/node_modules ou dependências de laboratório. O relatório dentro do fonte antecede seu fechamento; este externo contém hash/tamanho finais, sem reabrir o ZIP.
