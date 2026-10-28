# Entrega — Fator3 Site Core 1.59.0

Revisão 2 · 28/10/2026 · America/Sao_Paulo · Rodada de implementação.  
**Status: com-pendencias.** Implementação, documentação e pacotes concluídos; validação local aprovada. Core 1.59.0 instalado, ativo e validado tecnicamente no Site-Teste após autorização expressa do dono. Homologações de fornecedores permanecem pendentes. Slug `base-site-core-fator3`; basename `base-site-core-fator3/base-site-core-fator3.php`.

A cópia interna do fonte corresponde à revisão 1 anterior à instalação remota e ao próprio fechamento do ZIP. Esta revisão 2 atualiza somente o relatório externo; instalador e fonte publicados permanecem byte a byte inalterados. A identidade final do fonte pertence somente ao relatório externo, sem reabrir o ZIP. A entrega 1.58.0 e seus artefatos permanecem imutáveis.

## 1. Bases aceitas e entrada da versão

Base direta **Core 1.58.0 canônica**: instalador 2816484 bytes, SHA-256 `71bf6497a2f2e2c605baf64f0f82c273201915039506b58ac220fc572afbd5e4`; fonte 4690094 bytes, SHA-256 `279b9609867b7459347d7bf1434b536073eb20fb2b996b4fdbcd6e644e37b50c`. O incremento minor identifica a incorporação dos retornos comerciais após a entrega da 1.58, sem sobrescrever seus pacotes.

Caminhos validados localmente: instalação limpa e atualização direta 1.58.0 → 1.59.0. O Site-Teste foi atualizado diretamente da base 1.57.1 para 1.59.0; esse salto também passou no laboratório local. Instalador 1.57.1: 2707842 bytes, SHA-256 `ee1c0eb8f46b7640a69e6b4e71697d5fc43bc9cd77f147c6219de1a410c5af62`. As matrizes executadas estão identificadas na seção 4.

Mínimos Core preservados: WordPress 7.1.2, PHP 8.3.6 de 64 bits, instalação única. Contrato administrativo **8.23.0** conservado, sem alteração de schemas públicos. A 1.59 não cria tabela, option, segredo ou migração destrutiva; as estruturas comerciais e de teste continuam com origem 1.58.

Entradas novas em `inputs/1590`: relatórios Google 0.22/LinkedIn 0.12, impacto Google → Core revisão 2, manifest de pacotes e cópia literal do impacto LinkedIn → MCP revisão 1. Plano anterior à implementação em `history/1590/PLANO.md`. Normas canônicas recebidas permanecem, com Norma 02 revisão 5 para impactos, respostas e fechamento. Pedidos 314–329 e Meta 20(e) da base conservam seu escopo; o acréscimo desta rodada trata da fronteira do Pedido Core 323.

## 2. Convivência, ações e retornos

| Acompanhante considerado | Bytes do instalador | SHA-256 | Fronteira |
| --- | ---: | --- | --- |
| MCP 0.34.0 | 903878 | `5d96b6a33cfc4a7c729c106268f4bc9d8938b34384da022345d7b7dae611a295` | Autorização/documentação, implantação privada e limite de auditoria central comercial. |
| Google 0.22.0 | 856534 | `a84754409f89b7b9c7367c1d261c44ef93c2f6039b379c3ec5c6242ec7188ebd` | Produtor comercial 1.2, extensão de reconciliação e aquisição/GA4 preservados. |
| Meta 0.13.0 | 284069 | `3ecd6ee6f277c7581adc05b4fa38c46611e3232b4400bb4a4421956c9fba8ac1` | Consumidor Ads e contratos Instagram existentes. |
| LinkedIn 0.12.0 | 304948 | `19748e788190f371809db469a6de052a645e25f39fad1672606dc776234ec54c` | Produtor comercial por ação, referência e diário local. |
| Pipedrive 0.3.0 | 59877 | `30fc784a552a89351900c169fad7300759163fb886b842f45ba807bb0977f657` | Cliente Core preservado; exige PHP 8.3.36. |

Fontes novos: Google 5989075 bytes, SHA-256 `1d9ba106eb9ababad67b964fa4ad44246acc27eeda3e83e7866ea57386d77abf`; LinkedIn 1713239 bytes, SHA-256 `15c182cc89605cb1fc18121d8db81fd9008daa06cb787f7224a973d18f4f65d1`. Tamanhos/hashes recebidos constam do manifest `inputs/1590/packages-google0220-linkedin0120.json`; `(1)` nos anexos é sufixo local, não versão diferente. A árvore de acompanhantes permanece original, sem edição pelo Core.

O inventário próprio anterior à implantação (`evidence/1590/installed-before.json`) confirma Core 1.57.1, MCP 0.34, Google 0.22, LinkedIn 0.12, Meta 0.13 e Pipedrive 0.3, ativos, além de DreamHost 1.0, WP Super Cache 3.1.4 e Yoast 28.8. A saúde retornou `healthy:true`, e home/REST retornaram 200 com bypass assinado interno; isso não comprova acesso externo universal. Os recibos de instalação Google/LinkedIn descritos pelos emissores pertencem às respectivas rodadas, não à implantação Core 1.59. Pipedrive não deve ser ativado no PHP 8.3.6 do laboratório, inferior ao seu mínimo.

### Inventário de ações, respostas e desfechos

| Referência / origem | Ação nesta rodada Core | Situação e responsável |
| --- | --- | --- |
| Core 1.58 → Google, revisão 2, Pedido 323 | Considerar o produtor 1.2 entregue pelo Google 0.22, preservando aquisição e os bloqueios por capacidade efetiva. | Produtor e fronteira Core `validado-localmente` em `return-google0220` (74 assertivas); aceite externo separado. |
| Google 0.22 → Core, revisão 2 | Incorporar e revisar a consulta de recibos comerciais incertos, anunciada por `site-stage-conversion-reconcile/1.0.0`. | Consumidor incorporado à 1.59 e `validado-localmente` com o produtor original; ciclos locais aprovados; implantação remota concluída após autorização expressa. Responsável Core. |
| Core 1.58 → LinkedIn, revisão 2, Pedido 323 | Considerar o produtor 1.2 entregue no LinkedIn 0.12, com concessão por ação e referência vinculada. | Produtor e fronteira Core `validado-localmente` em `return-linkedin0120` (63 assertivas), com transporte sintético. |
| LinkedIn 0.12 → MCP, revisão 1 | Arquivar e registrar a limitação `site-core-quality` no Registro central, sem alterar o MCP nem reenviar o documento. | Demanda aberta do mantenedor LinkedIn ao MCP; a prova própria reproduziu `service_record_unconfirmed`, sem reenvio por esse motivo. |
| Google 39 / Core 316, retorno Google 0.22 | Registrar o desfecho de implementação do consumidor 1.1 já entregue no Core 1.58. | Código anterior atendido; primeira conversão real Enhanced Leads permanece aceite do operador. |
| Meta 20(e), Instagram 18(b), GA4 313 e demais aceites da base | Preservar os contratos e pendências previamente delimitados; reexecutar as regressões pertinentes. | Não são novos encaminhamentos; resultados desta rodada e aceites externos permanecem distintos. |

O impacto Google recebido está em `inputs/1590/wp-mcp-google-fator3-0.22.0-impacto-base-site-core-fator3(1).md`. Seu texto introduz a consequência assíncrona concreta, não apenas uma nova versão. O impacto LinkedIn → MCP foi preservado literalmente em `inputs/1590/wp-mcp-linkedin-fator3-0.12.0-impacto-wp-mcp-fator3.md`, 3632 bytes, SHA-256 `ea8cc39c32dc65ab2b7a3443ed0d3680195ccab869737db3b6de34a3f9c9b843`.

**Nenhum novo impacto Core é emitido apenas para encerramento.** Respostas e atendimento ficam neste relatório, conforme Norma 02 revisão 5. Nenhuma mensagem externa foi enviada por esta rodada. A limitação MCP já tem documento substantivo do mantenedor LinkedIn; não se cria duplicata nem se apresenta recibo central inexistente.

## 3. Mudanças por pedido e evidência

**Pedido Core 323 — reconciliação Google.** O Core 1.58 podia usar o produtor comercial 1.2, mas deixava a ingestão Google incerta sem consultar seu resultado. A 1.59 usa o mesmo adaptador/ação para `reconcileBound(event_id,destination_ref)`, somente quando anunciado exatamente `site-stage-conversion-reconcile/1.0.0`. Não chama `sendBound` nesse caminho, não cria novo event_id e não remonta identificadores pessoais.

A incorporação parte do patch Google de SHA-256 `a10ef8971a47ac38950e6759aa80b378380021a2e388f8fc1c23e252602d2eaa`, aplicado à classe-base identificada por SHA-256 `84c429dda8697699357aa219ed028925811f0cfc86101ac3fd0edc7bdb683b20`. O arquivo proposto pelo emissor tinha SHA-256 `a26bdc81a189c2e598627da4e89329a9c5df1817379c25bd0cd77c3fba382876`. A revisão Core acrescenta guardas próprias de CAS final pelo timestamp reservado, configuração antes/depois da consulta, razões global/ação autorizadas e prova estrita de não entrega. Portanto, a classe final Core não é descrita como cópia literal do arquivo proposto.

| Mudança | Comportamento | Prova própria / limite |
| --- | --- | --- |
| Intervalo e concorrência | Até dois incertos Google por passagem, mínimo local 1800s, reserva anterior à consulta e trava renovável. Timestamp permanece data real. | `return-google0220.php`, limites/concorrência e ciclos nativos. |
| Seleção vinculada | Destino/qualidade ativos, etapa existente, configuração, ação, referência e extensão exatas. Razões globais/por ação só `ok` ou `stage_verification_required`. | Produtor Google original; bloqueios sem HTTP em revogação/alteração. |
| Resultado assíncrono | Entregue só com confirmação; recusado só com `non_delivery_proven:true`; inconclusivo mantém incerto. Prova de envio expirada pode consultar; concessão revogada não. | Mesmo recibo confirmado sem nova ingestão, processing/cooldown e erro. |
| Capacidade efetiva Google/LinkedIn | Remoção de textos estáticos que tratavam Google 0.21/LinkedIn 0.11 como únicas versões; anúncio e concessão atuais decidem disponibilidade. | Casos Core-only, produtores originais e documentação. |
| LinkedIn comercial | Contrato 1.2 por ação, consumidor/finalidade próprios; aquisição independente, sem reconciliação Google inferida. | `return-linkedin0120.php` com HTTP sintético. |
| Auditoria central | Preservar diário local e motivo de ausência no MCP 0.34; não reenviar nem trocar consumidor para preencher registro. | Fronteira LinkedIn/MCP e impacto recebido, com resultados próprios separados. |
| Documentação e versão | RELEASE/AGENTES 1.59, guia de reconciliação, índice e contratos; schema administrativo 8.23.0 e origem das estruturas preservados. | `docs-1590.php`, inventário/dicionário e comparação de schemas. |

Comparação do candidato com o instalador Core 1.58 em `evidence/1590/runtime-diff.json`: 3 arquivos adicionados (guias 1.59), 17 alterados e nenhum removido. Alteração funcional concentrada na classe de qualidade/destinos; os demais itens são cabeçalho, documentação e dados gerados.

A rotina de consulta reutiliza o worker existente. Não há nova ability administrativa Core, tabela, option ou segredo. O contador `reconciliados` mede chamadas de consulta, não confirmações. O backoff Google continua podendo impedir HTTP durante sua janela, inclusive quando maior que o mínimo Core.

Pedidos 322 e aceites reais da base não são declarados encerrados por esse acréscimo. Aviso por e-mail, e-mail automático Smart BCC e webhook genérico no teste sob demanda continuam bloqueados antes do transporte sem exclusão individual segura comprovável. Homologação de CRM real continua restrita aos sites autorizados pelo dono.

## 4. Instalação, prontidão, documentação e testes

**Casos locais registrados: `validado-localmente`.** Instalador final: 2825862 bytes, SHA-256 `8f3992e89b44f53a59e0e2af314ff8548fe2aadfcc06afe30e395610b1b7c832`, 773 arquivos e lint aprovado dos 555 PHP em PHP 8.3.6, conforme `evidence/1590/installer.json`. Os cinco ciclos nativos abaixo passaram; a implantação remota foi concluída conforme os recibos abaixo.

| Suite própria desta rodada | Assertivas booleanas | Resultado |
| --- | ---: | --- |
| `return-google0220` | 74 | aprovadas |
| `return-linkedin0120` | 63 | aprovadas |
| `request-316-real` | 52 | aprovadas |
| `companions-321-324` | 66 | aprovadas |
| `request-321-no-http` | 3 | aprovadas |
| `meta-ads-0130` | 41 | aprovadas |
| `review-324-bound` | 32 | aprovadas |
| `permissions-mcp-1571` | 16 | aprovadas |
| `request-323` | 31 | aprovadas |
| `request-313` | 95 | aprovadas |
| `request-312-1571` | 32 | aprovadas |
| `docs-1590` | 1734 | aprovadas |

Contagens por suite da última execução registrada em `evidence/1590/<suite>.json`, sem somar repetições ou resultados dos emissores. `return-linkedin0120` contém também o metadado numérico de 3 POSTs sintéticos; ele não é uma 64ª assertiva. `docs-1590` contém 1734 assertivas booleanas, além de `documents=148` e `pages=661`: suas 1736 entradas não são 1736 testes. As suites usam WordPress e produtores originais com HTTP sintético; não homologam contas reais.

Google: 74 assertivas confirmam a consulta do mesmo recibo, sem nova ingestão, intervalo/limite, proof expiry, revogação, estados inconclusivos e guardas concorrentes. Aquisição foi reexercitada em 52 assertivas; GA4 em 95. LinkedIn: 63 assertivas comprovam a fronteira de concessão, ação, elegibilidade, payload, binding e deduplicação; `return-linkedin0120-observed.json` registra `central_audit=service_record_unconfirmed` no MCP 0.34, sem atribuir recibo central inexistente. A regressão Instagram foi concluída nesta rodada: 32 assertivas aprovadas em `request-312-1571.json`, incluindo recusa de transação externa, falha parcial Meta, mesma chave na retomada e exclusão coordenada. O consolidado `local-summary.json` registra 2.239 assertivas booleanas aprovadas em 12 suites, sem contar metadados numéricos ou os ciclos nativos.

Documentação lida integralmente pela ability pública em laboratório, com índice, páginas, hashes, schemas, versão, permissões negativas e ausência de HTTP. Guias novos: RELEASE-1.59.0.md, AGENTES-1.59.0.md e RECONCILIACAO-COMERCIAL-1.59.md; QUALIDADE-DESTINOS-1.58.md descreve a fronteira vigente. Guias anteriores permanecem para os demais pedidos. A leitura remota complementar e a validação no servidor estão descritas abaixo.

### Ciclos nativos concluídos

| Ambiente local | Cenário | Resultado / evidência |
| --- | --- | --- |
| WordPress 7.1.2 / PHP 8.3.6 | Instalação limpa e atualização 1.58.0 → 1.59.0 | Aprovados: `native-wp712/native-cycles-1590.json`. |
| WordPress 7.1.3 / PHP 8.3.6 | Instalação limpa e atualização 1.58.0 → 1.59.0 | Aprovados: `native-wp713/native-cycles-1590.json`. |
| WordPress 7.1.3 / PHP 8.3.6 | Atualização direta 1.57.1 → 1.59.0 | Aprovada: `native-from1571-wp713/native-cycles-1590.json`. |

Os cinco cenários confirmam versão 1.59.0, estrutura pronta, finalização e preservação/reinstalação. As três atualizações conservam os hashes antes/depois das fotografias verificadas. Na desinstalação, históricos e recibos incertos permanecem; pendentes são suspensos. O tempo de finalização foi acelerado somente no estado descartável, com requisições novas separadas. Todos os registros identificam o mesmo SHA-256 do instalador final. Pipedrive não foi ativado no PHP 8.3.6, inferior ao mínimo 8.3.36 do acompanhante.

### Instalação e estado final remoto — 28/10/2026

Após a autorização expressa “Autorizo”, foi executada a operação `plugins/upload-base64` usando o ZIP privado, `expected_slug=base-site-core-fator3`, SHA-256 `8f3992e89b44f53a59e0e2af314ff8548fe2aadfcc06afe30e395610b1b7c832`, `activate=true`, `overwrite=true` e chave `core1590-install-8f3992e89b44-20261028`. Recibo de pacote **`28bd5954d97485cb71e508375a3be502`**: `version_before=1.57.1`, `version_after=1.59.0`, `active_after=true`, `applied=true`, `recovery_status=applied`. Backup recuperável de arquivos anteriores: **`cae81b4bb5f3b25ba177fdaa`**. A pré-imagem cobre arquivos/ativação; não desfaz banco, migrações nem efeitos externos. Registro de execução: `site-install-authorized.json`.

A rejeição automática anterior pertence ao histórico da revisão 1. Foi resolvida pela autorização expressa; não existe bloqueio de instalação pendente. O pacote foi transferido por 11 partes e conferido integralmente antes de instalar. Nenhuma URL pública de estágio foi criada.

O ciclo interno **`f6c88256-4550-43ec-bf30-4271d5f2be69`** concluiu as **17 etapas sem falhas** e confirmou a finalização no executor. O pós-atualização automático concluiu cabeçalhos (`cabecalhos_verificados`), navegação (`observada`) e Pipedrive (`conta_verificada`). Esses resultados foram lidos do estado persistido; não são atribuídos a uma execução manual do teste completo do lead.

A leitura do site confirmou Core 1.59.0, contrato 8.23.0, WordPress 7.1.3 e PHP 8.3.36. O resumo operacional retornou JSON válido de 2957 bytes; a leitura não alterou as opções observadas nem chamou fornecedores. As 176 operações públicas Core permanecem disponíveis. Todos os **773 arquivos instalados** correspondem à árvore do instalador, comprovados pelo hash do manifesto ordenado `bc32851db3078939e18ec43219d9af07bbae57945fe6a23cbfff03e9f38dee14`. Evidência: `site-read.json`.

| Prova no servidor, em ambiente isolado | Resultado | Limite |
| --- | --- | --- |
| Instalação isolada em WordPress 7.1.3 / PHP 8.3.36 | Core e acompanhantes ativados; estrutura pronta | Banco de teste separado; não simula dados reais do dono. |
| Pedido 323 | 31 assertivas aprovadas | Core isolado e adaptadores sintéticos; nenhuma conversão real. |
| Documentação instalada via ability pública e transporte MCP do laboratório | 1.734 assertivas aprovadas; 148 documentos, 661 páginas, hashes e conteúdo integral | Cópia isolada dos arquivos instalados; sem HTTP a fornecedor. Os dois metadados numéricos não são testes. |
| Permissões MCP | 16 assertivas aprovadas | SMTP, WhatsApp, Instagram, GA4 e revogação; contas/recibos sintéticos. |
| Leitura direta pelo conector da instalação compartilhada | Índice e seis documentos completos com hash igual ao instalador | DOCUMENTACAO, RELEASE-1.59.0, AGENTES-1.59.0, RECONCILIACAO-COMERCIAL-1.59, CONFIGURACAO e CONTRACTS; o último lido em quatro páginas de até 30 linhas. |

A primeira execução de `request-323` falhou em `323_old_adapters_blocked`, pois o caso exige ausência de produtores comerciais modernos e os acompanhantes Google 0.22/LinkedIn 0.12 estavam ativos. O teste foi repetido na seleção Core-only do laboratório isolado e as 31 assertivas passaram, sem editar o teste ou o runtime. A combinação com os produtores originais novos permanece coberta pelos testes locais `return-google0220` (74) e `return-linkedin0120` (63). A falha e a repetição foram preservadas nos registros, não contadas como aprovação única de todos os ambientes.

**Limpeza concluída:** 98 tabelas exclusivas do ensaio removidas, zero remanescentes; diretório privado isolado e option de controle removidos. Controlador temporário `wp-content/mu-plugins/f3-core-qa1590.php` apagado com a pré-imagem obrigatória do canal (`08ffbecab518b70a40fa68a4`). ZIP privado de estágio apagado após uso. Não restam testes ativos desta rodada; permanecem somente os backups privados do canal, sem execução ativa. Recibos: limpeza `e43f886a356ba2d540533b8e`, retirada do controlador `502d04500ead2bf48d59f7b8`, retirada do ZIP `b49b3fab56396d1f0f5c4fdd`.

**Estado final:** Core 1.59.0, MCP 0.34.0, Google 0.22.0, LinkedIn 0.12.0, Meta 0.13.0 e Pipedrive 0.3.0 ativos. DreamHost 1.0.0, WP Super Cache 3.1.4 e Yoast 28.8 preservados. Saúde `healthy:true`, recuperação sem operações pendentes, home e REST com HTTP 200 após retirar o controlador. As sondas são internas da mesma origem e não comprovam acesso externo universal. GA4 permanece desligado e sem concessão; o acervo real de 30 dias não foi homologado. WhatsApp/Instagram permanecem sem captura ativa nesta instalação. O envio autenticado de e-mail existente permanece habilitado; esta rodada não prova entrega SMTP real.

Os registros remotos desta retomada ficam no ambiente de trabalho em `evidence/1590/site-*.json`, e seus resultados/identidades estão consolidados nesta revisão. Não foram inseridos retroativamente no ZIP fonte já publicado. O relatório interno congelado e os ZIPs conservam a identidade entregue na revisão 1.

O harness remoto tem allowlist curta e isolamento; ensaios de retorno Google/LinkedIn permanecem no laboratório local. Não se implantam testes contra contas reais nem se criam concessões para a instalação parecer pronta. Sondas served/bypass de mesma origem não comprovam cache externo universal. Publicação GitHub e implantação na frota não estão incluídas por inferência.

## 5. Banco, preservação e reversão

A versão 1.59 conserva tabelas/colunas/options da 1.58; não altera sua data de introdução. `f3base_qualidade_destinos` mantém chave, ação, referência, revisão, estado, código, HTTP e timestamp real. A consulta trabalha no recibo existente; não migra nem reenvia histórico. As demais tabelas comerciais, de privacidade, wp_mail e teste mantêm as regras anteriores de preservação.

Desativação/desinstalação não desfaz conversão, mensagem, CRM ou exclusão externa. Históricos e tombstones permanecem; pendentes das filas protegidas são suspensos conforme contratos da base. A preservação/reinstalação está registrada nos cinco ciclos próprios desta rodada, identificados na seção 4.

Antes de restore, pausar/drenar e reconciliar pelo fluxo Core; preservar banco, salts/chaves, diretório privado, guarda operacional e diários dos produtores. Voltar os arquivos para 1.58.0 deixa incertos comerciais sem consulta automática, mas não apaga confirmações já gravadas. Não apagar recibos, trocar event_id, limpar deduplicação ou converter incerto em pendente. Um recibo mais recente no produtor pode ser consultado posteriormente quando o vínculo continuar autorizado.

A pré-imagem remota de arquivos/ativação é `cae81b4bb5f3b25ba177fdaa`, da operação `28bd5954d97485cb71e508375a3be502`; não equivale a backup completo do banco. Backup de arquivos não é reversão transacional de efeitos externos; não prometer rollback de fornecedor com base na cópia do plugin.

## 6. Pendências e responsáveis

| Responsável | Pendência / critério |
| --- | --- |
| Mantenedor Core | Instalação, ciclo, documentação, comparação de runtime e limpeza remotos concluídos. Permanecem os limites funcionais e homologações de fornecedor listados abaixo. |
| Operador Google | Concessão e ação comercial exclusivas; conta/termos/prova válidos; primeiro evento real confirmado no mesmo recibo, sem nova ingestão; aquisição Enhanced Leads permanece aceite separado. |
| Operador LinkedIn | Concessão por ação, escopos e regra API válidos; primeira entrega comercial real e leitura do diário local. HTTP sintético não prova atribuição no Campaign Manager. |
| Mantenedor MCP | Tratar impacto LinkedIn 0.12 revisão 1 para `site-core-quality` no schema/leitor/painel de auditoria central; preservar validações e provar recibo confirmado antes de fechar a demanda. |
| Mantenedor Core / transportes | Dependência de exclusão individual segura de e-mail/Smart BCC/webhook do Pedido 322; enquanto ausente, não declarar aceite ponta a ponta. |
| Operador/frota | Aceites anteriores de contatos, Meta Ads/GA4/Instagram, resposta humana, marcas, autenticação recebida de e-mail e provas pós-atualização, conforme relatórios da base. |
| Operador Pipedrive | Convivência nativa exercitada em PHP 8.3.36 e verificação automática da conta concluída. Aceite comercial/CRM ponta a ponta permanece restrito aos sites e destinos autorizados. |

A autorização expressa foi recebida e a operação específica de substituir/ativar o Core 1.59.0 foi concluída. Instalação autorizada não inclui criar conta/concessão comercial nem enviar conversão real. Os aceites externos e a limitação 322 mantêm a entrega com pendências mesmo se os gates locais e a implantação técnica forem concluídos.

## 7. Credenciais, permissões e operação

Nenhum segredo novo é emitido pelo Core. As concessões comerciais continuam no produtor e precisam de administração atual, conta/ação exatas e identidade/política vigentes. A aquisição não concede etapas por inferência. A configuração Core continua com revisão, simulação e validação integral; schemas públicos permanecem 8.23.0.

Google: credenciais Ads/Data Manager e termos/enhanced pertencem ao plugin Google; Core consome capacidades, referência e recibo, sem receber token. LinkedIn: `rw_conversions`, `r_ads`, papel e regra API pertencem à concessão do produtor; Core não troca consumidor para contornar auditoria central. Meta/Pipedrive/caixa/Slack mantêm suas instruções anteriores.

Reconciliação não exige reconstruir dados pessoais nem permite usar credencial revogada. Prova de envio expirada tem exceção estrita para consulta do recibo já admitido; não libera novo envio. Não colocar tokens, salts, cookies, payload pessoal, dumps ou grants reais em ZIPs/evidências. Os transportes dos testes são sintéticos; a instalação não é homologação de credenciais.

## 8. Artefatos, identidade e distribuição

Somente o instalador é instalável. O fonte contém runtime idêntico ao instalador, build/testes/locks, entradas rastreadas, histórico, evidências sanitizadas e relatório pré-fechamento. Não inclui ZIPs aninhados, laboratórios, node_modules, dumps, segredos ou extrações dos acompanhantes. O empacotador compara as árvores e produz `source-manifest.json`; as identidades finais correspondem aos bytes validados e às árvores comparadas.

| Arquivo | Bytes | SHA-256 |
| --- | ---: | --- |
| `base-site-core-fator3-1.59.0-instalador.zip` | 2825862 | `8f3992e89b44f53a59e0e2af314ff8548fe2aadfcc06afe30e395610b1b7c832` |
| `base-site-core-fator3-1.59.0-fonte.zip` | 4884074 | `26093d43ebfdc09b97ccbcb366a69673cd2154747e9f35b5953593a7c03c56c8` |

Relatório externo: `base-site-core-fator3-1.59.0-relatorio.md`. Os impactos recebidos e os documentos 1.58 permanecem como insumo/histórico; não há novo impacto Core de encerramento nesta rodada. Tamanho/hash final do fonte preenchidos somente neste relatório externo, sem alterar o ZIP para inserir seu próprio hash.

Este fechamento distingue pacote validado localmente, instalação técnica remota concluída e aceites pendentes de fornecedor. Os artefatos anteriores 1.58 não são substituídos. Mesmo após concluir as provas técnicas, as pendências explicitadas de conta real, auditoria central e limpeza 322 continuam com seus responsáveis.

## Checklist de encerramento

Normas 01 e 02 revisão 5 lidas integralmente. Identidade/versão, contratos, documentação instalada, testes próprios, atualização e instalação limpa locais, preservação de dados, empacotamento e separação dos retornos/impactos conferidos. Fonte e instalador compartilham os mesmos 773 arquivos de runtime. Não foram alterados outros plugins, enviadas mensagens ou realizadas conversões reais. Implantação, leitura documental, saúde e limpeza no Site-Teste concluídas. Homologações externas e os limites dos pedidos 322/323 continuam explícitos; a instalação técnica não certifica conversões, atribuição nem captura real nos fornecedores.

### Histórico documental

Revisão 1: pacotes e testes locais concluídos, implantação bloqueada por revisão automática. Revisão 2: autorização recebida, instalação 1.57.1 → 1.59.0 e provas/limpeza remotas concluídas; nenhum byte dos ZIPs foi alterado. Os links de instalador/fonte continuam válidos.
