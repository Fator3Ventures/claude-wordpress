# Entrega — Fator3 Site Core 1.73.0

Revisão: 1 · Data: 2026-11-06 · Rodada: implementação dos pedidos 371, 372 e 373.
Slug: `base-site-core-fator3` · Contrato administrativo: `8.35.0`.
Status: **com-pendencias** de homologação em fornecedor e inspeção visual. Código instalado e operacional no Site-Teste; os testes descritos abaixo passaram.

Foram lidos integralmente `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos revisão 5, de 02/11/2026. As cópias estão em `reference/`. O pedido vigente foi extraído de `Fator3 Site Core(20261106-161655).md`.

## 1. De onde esta versão entra

Instalação limpa ou atualização direta da **1.72.1**. Base recuperada e preservada integralmente em `history/1.72.1-runtime/`; instalador-base de 4.323.938 bytes, SHA-256 identificado abaixo.

SHA-256 exato da base: `3d13dfc96c6dec31221dbe989bdbee27beedbcf98719be0a0447bba7078242f6`.
Requisitos: WordPress >= 7.1.4; PHP >= 8.3, 64 bits, sem multisite.

- Laboratório nativo: WordPress 7.1.4, PHP 8.4.27 e MariaDB 11.8.6. Instalação limpa, atualização e reativação exercitadas.
- Site-Teste: WordPress 7.1.4, PHP **8.3.36**, MySQL **8.4.11**. Atualização direta, rotas MCP, documentação, resposta HTTP e teste IMAP exercitados.

A suíte completa foi executada no laboratório; a prova em PHP 8.3 tem o escopo remoto especificado na seção 4. O comentário histórico do arquivo principal sobre a base 1.66.0 não amplia a matriz validada: nesta rodada a base de atualização comprovada é 1.72.1.

## 2. Convivência e encaminhamentos

Pacotes anexos examinados e ativos durante a instalação: MCP **0.41.0**, Google **0.30.0**, Meta **0.21.0**, LinkedIn **0.19.0**, Pipedrive **0.7.0**. Identidades completas em `evidence/1730/packages.json`.

Escopo: descoberta/execução genérica de abilities pelo MCP; contratos de configuração do Core; separação entre CAPI do Core e gestão Meta; supressão apenas do destino Meta na aquisição; preservação das interfaces consumidas pelos outros pacotes. Não foi identificada mudança que exija adaptação de código nos acompanhantes fornecidos. Não há relatório individual apenas para anunciar versão. As APIs comerciais desses acompanhantes não foram novamente homologadas nesta rodada.

Na conferência posterior, Pipedrive **0.8.0** apareceu ativo por atualização concorrente, não realizada nesta rodada. O Core continuou operacional e a fila sem falhas; o código da 0.8.0 não integra a análise dos anexos. Esta distinção evita atribuir homologação completa a uma versão observada somente no final.

## 3. Mudanças e evidência

| Pedido exato | Problema | Resultado | Evidência e limite |
|---|---|---|---|
| Pedidos core 371 | Ausência de marcação posterior do Lead e correspondência original protegida | `f3base_meta_lead`, modo imediato/agente por site e formulário; `f3base/meta-lead-enviar`; captura cifrada; auditoria, revisão, consentimento e recibo | 57 verificações compartilhadas da release por ambiente incluem marcação, supressão, origem/IP/UA, fbc, hash, prazo, aprovação de suspeito e repetição. POST/aceitação da Meta simulados, não homologados no fornecedor |
| Pedidos core 372 | Token CAPI recusado por exigir `ads_management`/leitura do Pixel | Gravação cifrada com aviso `capi_validacao_por_evento_pendente`; sem consulta de Ads nem evento automático ao salvar | Gravação e rotação reais no banco local, ausência de chamada HTTP na gravação, rejeição de caracteres inseguros. A UI distingue conferência local de identidade confirmada |
| Pedidos core 373 | Transporte IMAP abria incidente na primeira falha | Lista `imap_codigos_passageiros`, com simulação; transporte aguarda limites, autenticação/pasta/credencial permanecem imediatos | Teste nativo e **9 verificações no Site-Teste**: silêncio em 1 e 23 falhas, uma abertura em 24, uma recuperação; estado restaurado, zero e-mails reais |

A nova ability exige `manage_options`, simula por padrão e exige revisão inteira ao aplicar. Auditoria grava operador, motivo, instante e revisão da política antes de enfileirar. O consumidor CAPI existente mantém consentimento antes do despacho, reserva de fila, prazo e reconciliação de resultado incerto.

No modo agente, a aquisição suprime Lead automático do Pixel e CAPI; GA4, Google Ads e LinkedIn conservam seus contratos. O modo padrão permanece **imediato**. A escolha é fotografada em cada novo contato. Event_id, página e instante são estáveis; jamais são substituídos pela requisição administrativa. Contatos anteriores sem snapshot não recebem correspondência inventada. A janela é limitada a sete dias e à política mais restritiva de `f3base_meta_janela`.

Não há novo JavaScript público, novo endpoint anônimo de envio ou consulta externa na captura. O custo adicional de captura é a cifra do snapshot e leitura da política; não foi medido um ganho de desempenho nesta rodada. As metas históricas de tamanho/latência continuam fora do aceite destes três pedidos.

## 4. Instalação e prova da troca

Alvo confirmado por `core/get-site-info`: **https://fator3-teste-mcp-1.dreamhosters.com**. O rótulo de ambiente WordPress é `production`; o domínio confirma que se trata do Site-Teste autorizado.

O ZIP foi transferido em trechos com conferência SHA-256 e instalado por `plugins/upload-base64`, usando `zip_path`, `activate:true`, `overwrite:true`, `expected_slug:base-site-core-fator3` e o hash da seção 8. Operação `035105b08b0534db94d1571d336d1e49`, pré-imagem `87c875924add188066a0d43a`: versão antes 1.72.1, depois 1.73.0, `applied:true`, ativo. Não houve instalação pela frota/raw nem publicação de fonte em repositório público nesta rodada.

A primeira tentativa foi rejeitada pela revisão automática por interpretar `production` como alvo não autorizado. A leitura do domínio demonstrou correspondência com o Site-Teste; a repetição da mesma instalação foi aceita. O bloqueio foi resolvido sem mudar o alvo ou contornar a revisão.

| ID | Ambiente | Cenário | Resultado | Evidência |
|---|---|---|---|---|
| N1 | Laboratório | 12 execuções de testes nativos | **179 verificações aprovadas** | `evidence/1730/native-run.json` e JSONs individuais |
| N2 | Laboratório | Sintaxe de todo runtime, inventário e JS administrativo alterado | **597 PHP**, 939 arquivos conferidos; JS válido | `evidence/1730/lint.json` e `runtime-manifest.json` |
| N3 | Laboratório | 1.72.1 → 1.73.0 | 993 amostras e configuração preservadas | `upgrade--upgrade-1721-1730.json` |
| R1 | Site-Teste | Atualização e ciclo do executor | Concluídos, Core operacional | `evidence/1730/site-teste.json` |
| R2 | Site-Teste | Nova rota e simulações de modo/lista IMAP | Rota executável; contato inexistente recusado sem envio; prévias sem persistência | Mesmo arquivo |
| R3 | Site-Teste | Falha IMAP sintética, abertura e recuperação | 9 verificações, 2 mensagens interceptadas, **0 enviadas**, estado original preservado | `qa1730_imap-live` no mesmo arquivo |
| R4 | Site-Teste | Home, REST e login em PHP novo | HTTP 200, três asserções aprovadas | `qa1730_final-probe` |
| R5 | Site-Teste | Cabeçalhos após limpeza de cache | `verified`, evidência persistida, preferência inalterada | `evidence/1730/closing.json` |

Documentação descoberta no índice e lida integralmente por `f3base/documentacao-ler`, `arquivo:docs/RELEASE-1.73.0.md`, `linha:1`, `limite:200`: **49 linhas**, próxima linha nula, versão 1.73.0, SHA-256 `8458d95e68852f0d414a135a5eca2c39f1ee2eca27e5b64351458998be80e55b`. Os limites descritos dentro do instalador refletem o fechamento anterior ao teste remoto; este relatório adiciona a prova em PHP 8.3.

Estado final: Core 1.73.0 ativo; modo imediato; IMAP mantém 24 falhas/120 minutos; filas sem falhas/incertos. A conferência detectou atualização concorrente do Pipedrive para 0.8.0 e nova pendência de cache, posteriormente verificada. Fixture MU removida com guarda de hash; ZIP de transferência removido. Backups técnicos do canal permanecem, sem fixture executável. Nenhuma credencial real alterada.

## 5. Banco, migração e correção por nova versão

Sem novo schema de tabelas. A atualização adiciona a option `f3base_meta_lead` e completa a lista de códigos na configuração de avisos, mantendo os valores anteriores. Novos contatos guardam snapshot cifrado e auditoria em `dados`; a fila CAPI existente armazena payload cifrado e recibos. Retenção e eliminação seguem o ciclo existente do contato e cancelamento da fila.

As provas de migração conferem hashes das 993 amostras e da configuração. A reativação após desinstalação recriou 33 tabelas operacionais sem consulta prematura. No Site-Teste não foi exportado banco nem conjunto de options privadas: houve pré-imagem de arquivos do canal, não backup integral de dados. O teste IMAP ocorreu dentro de transação desfeita e conferiu a preservação do estado original.

Não há downgrade nem migração reversa. Qualquer correção após a instalação exige nova versão. Em resultado externo incerto, conservar record_id/event_id, estado e recibo para reconciliação; não repetir o efeito criando outro contato.

## 6. O que permanece pendente

- **Meta real — responsável pela conta/dono:** configurar dataset, token e test_event_code no Site-Teste; comprovar evento de servidor no Gerenciador de Eventos e correspondência. Saúde atual informa `pixel_ausente`.
- **Korvena — operação de produção:** aceite dos pedidos 371/372 com contato real no dataset 1088603200283681. Esta rodada modificou exclusivamente o Site-Teste e não reutilizou credencial de produção.
- **DreamHost — observação operacional:** próxima queda real abaixo dos limites deve permanecer sem aviso. A falha sintética foi comprovada.
- **UI/navegador:** componentes e texto atualizados; sintaxe JS e painel nativo testados, sem inspeção visual autenticada nem prova do Pixel em navegador nesta rodada.
- **Matriz:** suíte completa em PHP 8.4/MariaDB; PHP 8.3/MySQL exercitados no escopo remoto acima. Acompanhantes com APIs reais e código Pipedrive 0.8.0 não foram homologados integralmente.

Essas pendências limitam a alegação de homologação externa; não representam falha dos testes aprovados nem impedem o uso das correções no escopo verificado.

## 7. Credenciais e configuração do dono

Configurações → Meta: `f3base_meta_capi_token` (token gerado no Gerenciador de Eventos), `f3base_meta_capi_pixel_id`/`f3base_meta_pixel_id` e `f3base_meta_transporte`. Para testes, `f3base_testes.capi_test_event_code` e política CAPI de teste. Não se exige `ads_management` para provar permissão CAPI. A aceitação pelo fornecedor deve vir do recibo de evento, não da mera gravação do token.

`f3base_meta_lead` já existe em modo imediato. A regra de negócio para marcação do agente continua sob decisão do dono. `f3base_avisos_tecnicos` conserva os limites existentes e permite simular a lista passageira. Nenhum valor secreto consta nos artefatos.

## 8. Identidade dos arquivos

| Artefato | Nome | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | base-site-core-fator3-1.73.0-instalador.zip | 4332427 | `6675c1e7436e1195f6f7559a9baf62e049d871d145c84f19c04ac67f8d25655e` |
| Fonte | base-site-core-fator3-1.73.0-fonte.zip | 9160961 | `dcb645dd56d27eda36d011f97a2c374b3274bef8d45c2296a5a01c1cb4fda421` |

Este é o **relatório externo canônico**, fechado após os dois ZIPs. A cópia `RELATORIO-PRE-FECHAMENTO.md` dentro do fonte é anterior ao fechamento e não contém o hash de seu próprio pacote. O fonte contém runtime, baseline, testes, evidências, manifesto, scripts de empacotamento e referências; o instalador contém somente runtime/documentação, sem testes ativos, dependências instaladas ou ZIP aninhado.

Checklist: documentos centrais e precedência conferidos; base/alvo e mínimos declarados; três entregáveis; impactos delimitados; migração e instalação verificadas; permissões e defaults preservados; documentação acessível; integridade e limpeza comprovadas. Itens de fornecedor, inspeção visual e matriz integral permanecem explicitamente pendentes; fluxo raw/frota é não aplicável a esta instalação direta.

Downloads: [fonte](sandbox:/workspace/scratch/24dcf1d63a17/core1730/release/base-site-core-fator3-1.73.0-fonte.zip) · [instalador](sandbox:/workspace/scratch/24dcf1d63a17/core1730/release/base-site-core-fator3-1.73.0-instalador.zip).
