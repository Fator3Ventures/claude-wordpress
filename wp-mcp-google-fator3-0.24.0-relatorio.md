# Entrega — Fator3 MCP Google 0.24.0

Revisão 1 · 2026-10-29T11:11:07-03:00 · nova rodada minor sobre 0.23.0. Status: **apta-no-escopo-testado**. O pacote está implementado e validado nos cenários locais descritos; instalado, ativo e conferido no Site-Teste. Permanecem como limites a suíte PHPUnit integral indisponível e o aceite de contas Google reais. Esses limites não são apresentados como testes aprovados.

**Relatório externo final.** A cópia interna está identificada como “cópia anterior ao fechamento do fonte”. O relatório externo canônico é `wp-mcp-google-fator3-0.24.0-relatorio.md`. A seção 8 da cópia interna mantém o tamanho/hash do fonte como `a preencher no relatório externo após empacotamento`; o relatório externo completa esses campos sem reabrir o ZIP fonte.

## 1. Bases aceitas e entradas

Instalação nova em WordPress limpo e atualização direta de **Google 0.23.0**, sem desinstalar e sem versão intermediária. Base exata recuperada dos ZIPs publicados, conferidos por SHA-256. Não aplicar os adaptadores históricos Core323/337/340/342 ao Core atual, inclusive depois de voltar o Google à 0.23.0.

A lista mais recente localizada, `Fator3 MCP Google(20261029-030442).md`, conserva os Pedidos Google 43–46 já implementados na base. Não foi localizado novo Pedido Google 47. A rodada considera a nova implementação Core 1.61.1, seu impacto revisão 2, Meta 0.16.0, MCP 0.37.0 e LinkedIn 0.13.0. Os anexos antigos não substituem estas bases mais recentes. Normas r5 preservadas no fonte anterior orientam o fechamento e a resposta aos impactos; r4 em project_sources foi comparada. Plano anterior à implementação: `docs/PLANO-024.md`.

Entradas ZIP efetivamente selecionadas:

| Arquivo | Bytes | SHA-256 |
| --- | ---: | --- |
| `base-site-core-fator3-1.61.1-fonte(1).zip` | 5723729 | `94617ef804d05bad17c4f68d8e62300b38b0e0145856f5925b6a4aefe1fcd08e` |
| `base-site-core-fator3-1.61.1-instalador(1).zip` | 2933589 | `9cfbab0b667c877c3c14b9d6704c827665d20d7b34ff4c9b9d915d6b3c9bd6d3` |
| `wp-mcp-meta-fator3-0.16.0-fonte(1).zip` | 3268614 | `826875296447fe946cda3944dd481b199f3927a48cdb92277435785dc0386ab6` |
| `wp-mcp-meta-fator3-0.16.0-instalador(1).zip` | 315170 | `a49f3e8ae9e60814ab55cf1bd4b3277e859a477347d02f664353c1268fda0b6b` |
| `wp-mcp-fator3-0.37.0-instalador.zip` | 912702 | `cbece53fc479d9fe3963b111e49e789d92609c5462102877244dcaebcf7cf3ec` |
| `wp-mcp-google-fator3-0.23.0-fonte.zip` | 6605227 | `5f043ed6b9435059de4eccdde12e57dc269a70fa771a5cb0b72c03ac157fd4b6` |
| `wp-mcp-linkedin-fator3-0.13.0-instalador(1).zip` | 314596 | `1c45738322f4901aeacdc36615789ae961e8b9d521ba321a27de0aea76c13502` |
| `wp-mcp-google-fator3-0.23.0-instalador.zip` | 883618 | `8100b62144f4e368349ed1798c5bd9c84da66028010bc2946281853b982faab8` |

Os relatórios Core 1.61.1 e Meta 0.16.0 e o impacto Core foram lidos. Metadados e hashes dos documentos/pedidos/normas estão em `evidence/024/inputs-received.json`. Evidências recebidas e evidências históricas não são contadas como execução desta rodada.

## 2. Convivência e encaminhamentos

| Ambiente | Combinação efetivamente exercitada | Resultado |
| --- | --- | --- |
| Mínimo isolado | WordPress 7.1.2 / PHP 8.3.6 / MySQL 8.0.46 / Google 0.24.0 | 94 verificações; sem acompanhantes |
| Instalação conjunta e documentação | WordPress 7.1.3 / PHP 8.3.6 / Core 1.61.1 / MCP 0.37.0 / Meta 0.16.0 / LinkedIn 0.13.0 | 211 verificações |
| Consumidores oficiais Core | Mesma combinação conjunta, Core original com migrações nativas em bancada descartável | 103 verificações |
| Atualização, rollback e reaplicação | Google 0.23.0 → 0.24.0 → 0.23.0 → 0.24.0; WordPress 7.1.3 / PHP 8.3.6 e mesmos acompanhantes | 165 verificações |
| Site-Teste | WordPress 7.1.4 / PHP 8.3.36; Core 1.61.1, MCP 0.37.0, Meta 0.16.0, LinkedIn 0.13.0 e Pipedrive 0.4.0 observados antes | Somente Google atualizado; instalação, inventário final, configurações selecionadas, documentos e preview do backup conferidos |

Os inventários locais confirmaram exatamente os bytes dos pacotes originais: Google 172 arquivos; Core 800; MCP 467; Meta 63; LinkedIn 72 quando presentes. Nenhum arquivo oficial do Core ou dos acompanhantes foi alterado. O laboratório usa bancos descartáveis e encerrou seus processos. Não foi feito produto cartesiano de versões. Pipedrive e plugins de terceiros foram apenas observados no inventário remoto, sem teste funcional específico.

**Novos impactos emitidos:** nenhum. A comparação examinou schemas Google, configuração, contratos de leitura/conversão, integração MCP, consumidores Ads/GSC do Core, preservação de registros sociais e instalação. Não foi identificada adaptação nova a pedir a outro pacote. Sem mudança de contrato, não há ordem nova de troca dos acompanhantes.

**Resposta a impacto recebido:** `base-site-core-fator3-1.61.1-impacto-wp-mcp-google-fator3.md`, revisão 2, Pedidos core 337/340/342. Responsável pelo atendimento nesta rodada: Google. Resultado implementado/validado-wordpress: documentação instalada passa a orientar `f3base_google_ads_acervo`, preservando `f3base_google_ads` para conversões/tag; o bootstrap da proposta anterior fica inerte. O Core 1.61.1 já contém os consumidores; a suíte de 85 verificações foi executada novamente contra esse Core original, dentro do cenário de 103. Não há mudança de Core a incorporar nem pedido de retorno ao Core. Aceite com contas reais continua pendente. Pela norma r5, esta resposta e o encerramento da pendência de incorporação ficam neste relatório, sem novo arquivo de impacto.

## 3. Mudanças por pedido e evidência

| Referência | Problema e resultado | Evidência desta rodada |
| --- | --- | --- |
| Impacto Core 1.61.1 r2; Pedidos core 337/340/342 | A proposta anterior usava nome de opção ocupado por conversões. O guia novo descreve o leitor efetivo, revisões, concessões independentes, leitura local, cobertura e aceites. | `docs/CORE-ACERVOS.md`, `integration024.php`: 14 verificações com leitura pública de configuração, ausência de privilégio e preservação de opção/hooks/classes. |
| Mesma referência | Evitar reaplicar a proposta sobre classes já incorporadas pelo Core. Bootstrap histórico incondicionalmente inerte; referência de opção corrigida no código histórico. | `tests/retired-core024.php`: 1 verificação antes do Core; caso integration024 após Core. Essa pasta não integra o instalador. |
| Pedidos Google 44–45 / Pedidos core 337/340 | Acervo cifrado permanente e leitor Ads existentes preservados; consumidor oficial exercitado com 30 dias, custo/cliques, GCLID exato, associação a sessões/contatos, revisita e revogação. | `core024.php`: parte da suíte de 85, SDK real com HTTP sintético; `requests023.php`: 70 verificações em cada cenário minimum/current. |
| Pedido Google 46 / Pedido core 342 | GSC consulta × página × dia mantém concessão 1.1 independente da 1.0, paginação, limites e publicação atômica. | Suíte Core: página curta/vazia, conclusão explícita, preservação de publicação anterior e legado; fontes indicam contagens anônimas desconhecidas. |
| Pedido Google 43 | Aceitação de formatos atípicos continua condicionada à validação remota; recusas locais estritas e preservação da credencial ativa mantidas. | `requests023.php` reexecutado com HTTP sintético. Não repetir ou somar o aceite real histórico como prova nova. |
| Nova versão solicitada | Versão, README, contratos, guia, migração, validação e documentação compilada passam a 0.24.0 e às versões atuais dos acompanhantes. Novo documento consta do índice instalado. | Geradores/docs/schema e leitura integral por MCP em WordPress. |

Comparação exata 0.23.0 → 0.24.0: somente **três arquivos de runtime** diferem: `wp-mcp-google-fator3.php` (número da versão), `includes/Admin.php` (uma entrada no índice de documentos) e `includes/Data/Documentation.php` (conteúdo compilado). Não há arquivo runtime adicionado/removido. Toda lógica de negócio, SDK, coleta, autorização, jobs, callbacks, criptografia e persistência é idêntica à base. Permanecem **298 habilidades, 114 de leitura, 184 de escrita e 41 opções**; os schemas de entrada/saída são idênticos. O schema de configuração difere somente em metadado de versão. Prova: `evidence/024/runtime-diff.json`.

Durante o candidato preliminar, o teste detectou que o guia novo fora compilado mas não incluído no índice Admin. A entrada foi corrigida e **os quatro cenários completos foram executados novamente sobre o SHA final**. Resultados preliminares não compõem os totais. Um assert inicial de comparação do schema também foi ajustado para distinguir metadado de versão de estrutura contratual. Não houve release intermediária entregue.

## 4. Instalação, testes, documentação e prontidão

**Prova local corrente:** 573 verificações nativas em quatro cenários + 1 de bootstrap inerte = **574**, sem falhas finais. São verificações executadas, com repetições entre cenários, não 574 casos únicos. Lint dos 168 PHP runtime; geradores, contratos, 54 exemplos, 55 documentos-fonte e 177 links locais conferidos. Não foram observados warnings/notices/deprecated/fatal atribuídos ao Google nos logs das bancadas. Os hashes de fontes de verificação/candidato permaneceram iguais antes/depois; inventários instalados coincidiram com os ZIPs.

Em current e upgrade, o MCP autenticado leu integralmente **23 documentos instalados, 84 páginas e 4.282.755 bytes em cada cenário**. São 120 verificações documentais por cenário. SHA-256, continuação e revisão foram conferidos; atualização rejeita continuação com revisão documental antiga. A suíte Core recebida foi adaptada apenas para bootstrap/escrita de prova da bancada; hashes e diferenças de finalidade constam em `tests/core024-provenance.json`. Migrações de Core foram concluídas usando mecanismos nativos somente no laboratório.

**Instalação remota autorizada:** Site-Teste `https://fator3-teste-mcp-1.dreamhosters.com/`, via WP MCP fator3-teste, `plugins/upload-base64`, arquivo final, `overwrite:true`, `activate:true`, `expected_slug:wp-mcp-google-fator3`, `expected_sha256:803fa058182b9f43625352f2b4a1572a3cd4b728f8c07fd58314a9a111d41849`, `idempotency_key:google0240-803fa058-site-test`, baseline/probe timeout 10 segundos. Sem atualização de outros plugins.

Recibo **2ea4e8775e7866bfb3ccdcd4ccb66f63**; backup **67874b9af96789a523aa1913**. Antes 0.23.0 ativa, depois 0.24.0 ativa; `applied:true`, `recovery_status:applied`, hash recebido idêntico. Reativação silenciosa em worker independente/processo PHP novo; não declarar ciclo do activation hook, pois o recibo informa `activation_hook_cycle_completed:false`. Sondas `/` e `/wp-json/` passaram antes/depois com HTTP 200 e cache bypass verificado; isso comprova resposta interna, não homologação funcional do fornecedor nem acesso externo público.

Uma nova chamada `google/status` confirmou 0.24.0, 298 habilidades, armazenamento `ready`, recuperação não pausada, servidor MCP registrado/pronto e sem incidentes ativos. Autenticação permanece não configurada, Ads desligado, conversões não prontas e `google_checks_performed:false`. Cron observado sem trabalho vencido; isso não equivale a execução de coleta real.

Após essa chamada, o conector retornou transitoriamente **MCP -32603 Internal error**, inclusive em leitura sequencial/Get Ability Info. O serviço voltou a responder, sem repetir a instalação, e a conferência foi concluída. Foram aprovadas **15 verificações sobre a evidência remota**, separadas das 574 locais: inventário de nove plugins com somente Google alterado; SHA-256 do PHP principal `ea91eed56c8ef8aa54a31699a47dc726656921880c672a12eaec71e09b8e24c5`; revisão Google `515012b9da5d89e2ecbdd9cbeca4d4e73ae096f10b012f5317007e6dca69350b` e valores selecionados preservados; hashes da seleção Core Ads e configuração/estado Core GSC preservados; backup com `rollback_ready:true`, `preimage_verified:true`, `applied:false`, `changed:false`.

O índice remoto contém 23 documentos cujas revisões/tamanhos coincidem com a prova local. Quatro documentos foram lidos integralmente em **nove páginas remotas**: CORE-ACERVOS.md (4), GUIA-0.24.0.md (1), README.md (1) e configuration-definitions.json (3). Os conteúdos reconstruídos tiveram tamanho e SHA-256 confirmados; a continuação usou `expected_revision`. Não se afirma leitura integral remota dos outros 19 documentos, já exercitada localmente. Provas: `evidence/024/remote.json`, `remote-document-content.json` e `remote-verification.json`.

Reprodução: `reproducao/LEIA-ME.md`, manifestos fixados e `tools/release024.py`. WordPress/PHP/MySQL são reais; HTTP Google é sintético. Não foram feitos gastos, conversões, alterações de campanha, mensagens, implantação em produção ou publicação no GitHub.

## 5. Banco, retenção e reversão

Nenhuma migração nova, DDL, opção nova, concessão, seleção ou agenda automática nesta versão. O acervo Ads continua cifrado e permanente; os contratos de registros, cron e configuração permanecem iguais. No teste de atualização, ciphertexts, conexões, dados de jobs/agendas/auditoria, provas de conversão, registros sociais e payloads de configuração/concessão foram preservados; o acervo cifrado retornou os mesmos dados depois da troca. Os três payloads Ads/GSC usados para preservação são sentinelas sintéticas inativas: provam preservação byte a byte, não autorização válida de conta real atravessando a atualização. Concessões reais do SDK e revogação foram testadas separadamente no cenário Core com fornecedor sintético.

O rollback foi aplicado **somente na bancada**, com preimage exata, recusa de destino editado, volta real para 0.23.0, inventário integral conferido e reaplicação da 0.24.0. Preview não é aplicação. No Site-Teste o backup foi confirmado por preview, com preimage verificada e nenhuma aplicação; a 0.24.0 permanece ativa no inventário final.

Antes de uma reversão operacional, guardar banco, arquivos, salts e recibos; consultar o schema atual de `plugins/rollback`, executar preview do backup identificado e resolver divergências antes de aplicar. Restaurar arquivos não desfaz banco, concessões ou efeitos externos. Não reenviar conversões/jobs para fabricar teste. Não reaplicar adaptadores históricos no Core depois de rollback.

## 6. Pendências e limites

| Item | Estado, motivo e responsável |
| --- | --- |
| PHPUnit integral | `bloqueado` para esta rodada: PHARs oficiais PHPUnit 9.6.31 e phpunit-9.phar retornaram HTTP 403. Não reutilizar o total unitário da 0.23.0 como execução nova. Os testes nativos e estáticos listados foram executados e passaram. |
| Ads real em ctooffice | `pendente` com operador autorizado: GCLID de um dia comparado à origem, 30 dias de custo/cliques por campanha/moeda e alteração de orçamento existente no acervo. Não gerar alteração/gasto para prova. |
| GSC real em ctooffice | `pendente`: comparação consulta/página/dia contra propriedade autorizada, com cobertura e anonimização explícitas. |
| Service Account real | Validação remota real não repetida nesta rodada; lógica idêntica à 0.23.0. Estado do Site-Teste não contém credencial configurada. |
| Navegador/UI | Não exercitado nesta rodada; não houve alteração de layout ou fluxo de formulário. A inclusão do documento foi verificada pela API instalada. |
| Frota/produção | Não publicado no GitHub nem distribuído; responsabilidade da frota após conferência do relatório e SHA. |

A versão é corrente para continuidade do desenvolvimento. Não se declara homologação de contas reais, compatibilidade de versões não testadas, preservação remota de valores fora da seleção examinada nem ausência absoluta de impacto fora do escopo observado.

## 7. Credenciais e operação

Ferramentas → Fator3 MCP Google → Conexão: configurar Service Account por JSON (e-mail, chave privada e token_uri) ou OAuth pelos campos apresentados na conexão. O formato deve satisfazer as validações locais e obter token remoto; avisos de formato não substituem acesso autorizado. Não há credencial real incluída nos pacotes.

Para Ads, informar developer token e acesso à conta anunciante; login customer ID quando aplicável; selecionar serviços/política e conceder coleta em `ads_archive`. A leitura do Core exige concessão própria em `ads_consumer_grants`, vinculada à conexão/conta/revisão. Para GSC, selecionar e validar a propriedade Core e conceder `query_consumer_grants` para o contrato 1.1; a concessão legada 1.0 permanece separada. Use schemas atuais e os exemplos instalados, não SQL ou escrita direta de opções.

No Core, `f3base_google_ads_acervo` pertence ao leitor de Ads; `f3base_google_ads` permanece de conversões/tag. A release não habilita automaticamente nenhum deles. Acervos/concessões precisam de ato explícito do administrador e, para dados pessoais, das capacidades previstas. Não compartilhar chave privada, client secret, refresh token, access token ou developer token no relatório.

## 8. Artefatos finais

| Arquivo | Bytes | SHA-256 |
| --- | ---: | --- |
| [wp-mcp-google-fator3-0.24.0-instalador.zip](wp-mcp-google-fator3-0.24.0-instalador.zip) | 886260 | `803fa058182b9f43625352f2b4a1572a3cd4b728f8c07fd58314a9a111d41849` |
| [wp-mcp-google-fator3-0.24.0-fonte.zip](wp-mcp-google-fator3-0.24.0-fonte.zip) | 6789039 | `6e2dd4f447404b9610b091288be2841105c1c016e3eee034caa7fd31e903af0f` |
| [wp-mcp-google-fator3-0.24.0-relatorio.md](wp-mcp-google-fator3-0.24.0-relatorio.md) | Relatório externo canônico | Identifica os ZIPs; sem hash circular |

Instalador contém somente runtime, assets, licenças e documentação PHP protegida; sem testes, fixtures, dependências de desenvolvimento ou adaptadores históricos. Fonte contém código, documentação editável, scripts, testes, evidências sanitizadas, entradas documentais, reprodução e esta cópia anterior ao fechamento; sem ZIP aninhado, banco de laboratório ou credenciais reais. Evidências 023 e anteriores e encaminhamentos antigos são históricos, não novas entregas de impacto.

O fonte foi fechado uma única vez, com CRC e estrutura conferidos. Depois de extraído em diretório novo, seu build reconstruiu o instalador com os mesmos 172 arquivos e exatamente os mesmos bytes/SHA-256 do candidato homologado. A tabela acima contém a identidade final do fonte; sua cópia interna permanece anterior ao fechamento, conforme previsto.
