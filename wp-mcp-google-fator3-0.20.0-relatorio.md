# Entrega — Fator3 MCP Google 0.20.0

Revisão 1 · 2026-10-26T21:40:33-03:00 · Referência America/Sao_Paulo. Os documentos de planejamento e changelog datados 27/10 usam a data UTC da rodada.
Slug: `wp-mcp-google-fator3` · Base direta: **0.19.0** · Nova rodada: pedidos Google **37 e 38**, com Core 1.56.0, MCP 0.33.0, Meta 0.12.0, LinkedIn 0.10.1 e Pipedrive 0.1.0.

**Implementada, validada no escopo abaixo e ativa no Site-Teste.** 0.20.0 é a versão corrente desta entrega. Permanece pendente a homologação GA4 real com o consumidor Core e seu acervo (pedido Core 313). Não houve publicação na frota nem no GitHub.

**Relatório externo canônico, fechado após o fonte.** A cópia interna antecede o fechamento e remete a este arquivo para tamanho e SHA-256 finais do ZIP fonte. Runtime e evidências permanecem idênticos; não há hash circular.

## 1. Origem e critérios

A base exata foi recuperada e conferida: instalador 0.19.0, 809.436 bytes, SHA-256 `d15868915e3fdf886d7e883a82d9d302df7242808fc94d45bf3e1857234759d1`; fonte 4.462.572 bytes, SHA-256 `0d90b1a0dbc186a9e0b2adf66843dad4abd928fb2c616a56442213597b0eefb2`. O documento recebido `Fator3 MCP Google(9).md` abriu os pedidos 37/38. Fontes, instaladores e relatórios dos acompanhantes foram considerados; identidades completas em `evidence/020/inputs.json`, relatórios recebidos em `inputs/020`.

Aplicada a norma comum **revisão 5, 23/10/2026**, presente nos pacotes atuais, que prevalece sobre a revisão 4 avulsa. Plano `docs/PLANO-0.20.0.md` e impacto Core foram produzidos antes do código do SDK. Respostas e desfechos ficam neste relatório; o impacto não recebeu revisão apenas para comunicar conclusão.

Requisitos Google mantidos: WordPress ≥7.1.2, PHP ≥8.3.6, OpenSSL e banco compatível com a estrutura atual. Identidades, basename, namespace, prefixos, Text Domain, Update URI, permissões e rotas permanecem. **290 abilities: 112 leitura / 178 escrita; 38 opções; configuração 4.0.0; execução e armazenamento 2.0.0.** Nenhuma tabela nova ou migração destrutiva.

## 2. Pedidos implementados

| Pedido | Comportamento entregue | Prova e limite |
|---|---|---|
| 37(a) | `audit_retention` aceita 0, padrão 0 quando não há valor explícito. Zero mantém todos os eventos; positivo continua sendo quantidade. Gravável por `google/configure-local` e pelo painel. | Schema/validação, mais de 1.000 eventos mantidos no SQL nativo e gravação remota confirmada. |
| 37(b) | `job_detail_days` e `job_summary_days` aceitam 0 sem prazo. Resumo 0 equivale a infinito; detalhe 0 exige resumo 0. Expiração de novas tarefas/reservas usa 0 corretamente. | Casos de ordem, conservação de resultados/resumos/deduplicação e testes da fila existentes. |
| 37(c) | Atualização conserva valores explícitos e registros; não limpa histórico ao ativar. Com retenção 0, limpeza ignora também datas de expiração antigas ainda presentes. | Upgrade direto/rollback/reaplicação preserva os registros semeados. Casos SQL e unitários conservam tarefas encerradas e resultados já expirados. Registros apagados antes da atualização não são reconstruídos. |
| 38(a) | Contrato `ga4-reader/1.0.0` no hook `f3_mcp_google_register_consumers`, cliente opaco por identidade de objeto, callback de configuração e concessão administrativa por conexão/propriedade/identidade. Revogação funciona inclusive com consumidor desativado. | Cliente sem usuário corrente, recusa de cliente forjado, mudança de propriedade, revogação, administrador sem permissão e troca de identidade. GSC conserva contrato e concessões separados. |
| 38(b) | `runReport` com dimensões, métricas, datas ISO, filtros e cursor. Retorna valores brutos como strings, cabeçalhos, row_count e metadados de qualidade. | Mesmas linhas que `ga/run-report` para fixture idêntica de 30 dias. Cursor vincula consulta, limite, revisões e concessão. Dados do fornecedor ainda não homologados. |
| 38(c) | Reserva local durável e trava por propriedade, `returnPropertyQuota:true`, consumed/remaining observados, bloqueio por cota e prazo de nova tentativa. Sem retry automático. | Esgotamento, 429, contenção e falha de persistência recusam avanço; cota conhecida e erro ficam explícitos. Saldo pode mudar por consumidores externos. |
| 38(d/e) | Auditoria identifica actor plugin/ID/versão, propriedade, run/request e tentativas. Falha de auditoria impede iniciar ou avançar. Não há persistência de linhas/filtros do relatório. | Auditoria real em WordPress/SQL com consumidor de fixture e provas de ausência de linhas nas options/auditoria. O acervo continua sendo responsabilidade do Core. |

O período por requisição tem até 366 dias; até 9 dimensões e 10 métricas; limite por página até min(5.000, max_rows). Filtros são FilterExpression camelCase, até 16 KiB cada, profundidade limitada; Google valida compatibilidade semântica. Ordenação por todas as dimensões e cursor de 24h não criam snapshot imutável. Paginação ou cardinalidade não garantem todas as linhas possíveis da propriedade.

Metadados originais de amostragem, `(other)`, restrições, truncamento, fuso e moeda são preservados. A Data API não fornece flag de finalização: `estimated_unfinalized_dates` usa hoje e os dois dias anteriores no fuso retornado, explicitamente como heurística. Fuso ausente/inválido resulta em null; `finalization_guaranteed` é sempre false, inclusive para períodos antigos.

O controle da cota serializa as consultas locais de consumidores por propriedade, com reserva de 30s para processo interrompido. Esgotamento horário aguarda conservadoramente uma hora; diário considera meia-noite PST; 429 sem cota preserva observação anterior, marca indisponibilidade e respeita espera maior do Retry-After. Outros chamadores, incluindo `ga/run-report`, podem consumir a mesma cota: não existe reserva global do saldo Google. Nenhuma repetição acontece dentro do SDK.

## 3. Comparação e convivência

A comparação de runtime identificou **20 arquivos alterados/adicionados**, dos quais três novos para SDK/cliente/cota. Lista e hashes em `runtime-changes.json`. As mudanças se concentram em retenção, registro/escopo/auditoria dos consumidores, configuração, bootstrap e documentação. Não houve alteração de código Core, MCP, Meta, LinkedIn ou Pipedrive.

O catálogo nativo 0.19.0 foi capturado com **o mesmo MCP 0.33.0**, evitando confundir decoração do canal com alteração Google. As 290 identidades e seus efeitos permanecem. Os únicos schemas públicos alterados são `google/configure-local` (campo auditoria e ampliação para zero), `google/configure-consumer` (contract/property opcionais, GSC como padrão) e `google/integration-status` (lista de contratos e projeção GA4). Os demais schemas são idênticos ao baseline comparado. Os schemas JSON e a documentação PHP compilada foram regenerados e conferidos.

| Acompanhante | Verificação |
|---|---|
| Core 1.56.0 / MCP 0.33.0 | Instalações limpas nas duas versões WordPress; ordem Google primeiro; SDKs existentes, transporte/documentação, comparação de catálogo e upgrade autenticado. |
| Meta 0.12.0 / LinkedIn 0.10.1 | Instalação junto à atualização, preservação de dados cifrados/sentinelas e inventário final dos arquivos. |
| Pipedrive 0.1.0 | Pacote/relatório examinados e inventário ativo remoto antes/depois. Não ativado no laboratório PHP 8.3.6, inferior ao mínimo próprio 8.3.36. |

Não foi identificada regressão nas fronteiras exercitadas. Isso não equivale a homologar todas as operações comerciais dos acompanhantes ou outros bancos/ambientes não testados.

## 4. Testes concluídos

| Prova | Resultado |
|---|---:|
| PHPUnit 9.6.37 / PHP 8.3.6 | **1.199 testes, 14.529 asserções**, zero falhas/erros/skips |
| Novos casos unitários 37/38 | 30 testes, 130 asserções, incluídos no total |
| Limpa WP 7.1.2, Core/MCP atuais | 2.671 verificações |
| Limpa WP 7.1.3, Core/MCP atuais | 2.612 verificações |
| Upgrade direto 0.19.0 → 0.20.0, WP7.1.3 | 2.638 verificações, incluindo rollback nativo e reaplicação |
| Google primeiro, WP7.1.3 | 1.183 verificações, incluindo SDKs e regressões de conversão |
| Google isolado, WP7.1.2 | 1.053 verificações |
| Contratos de conversão: ausente, incompleto, matriz e resposta | 60 verificações |
| Lint PHP do runtime | 159 arquivos válidos; instalador com 163 arquivos |
| Documentação via MCP HTTP nativo | 20 documentos reconstituídos, 74 páginas, hashes conferidos |
| Painel autenticado via jsdom 27.4.0 | 18 verificações; sem alegação de inspeção visual em navegador |

As **10.157 verificações nativas** incluem conferência individual de eventos retidos. Todos os laboratórios usaram MySQL 8.0.46, bloquearam HTTP externo/e-mail e encerraram seus processos. O transporte Google foi simulado; não houve gravação comercial. Runtime instalado e ZIP candidato foram comparados byte a byte. Evidências em `evidence/020`, com identidade do candidato, insumos e scripts de reprodução.

Tentativas preliminares corrigiram o harness (corpo de token em formulário, tolerância aos segundos transcorridos no cooldown, preparação do incidente usado pelo DOM e localização dos relatórios históricos). Dois testes antigos passaram a configurar auditoria finita explicitamente para continuar testando sua limpeza. Essas tentativas não estão contadas como aprovadas. A matriz final reúne três grupos concluídos na primeira execução e os dois grupos concluídos na execução seguinte; mesmo instalador e mesmas suítes pertinentes. Avisos WordPress.org no laboratório decorrem do bloqueio intencional de rede; nenhuma advertência/erro PHP do runtime Google foi encontrado nos grupos finais.

## 5. Site-Teste

WordPress **7.1.3**, PHP **8.3.36**, MCP **0.33.0**. Atualização autenticada por `plugins/upload-base64`, com hash e slug esperados; versão anterior 0.19.0, versão final 0.20.0, `applied:true`, ativo, verificação em novo processo PHP. Operação `e9d38596b4db3c991c157cf4`; pacote `370e8d6bb3fbcee94f9bccc108b48ff5`; backup `24ccc3247f96e20fc4ec3056`.

As sondas internas de `/` e `/wp-json/` retornaram **200 antes e depois**, com bypass de cache verificado. São sondas de mesma origem; não comprovam acesso público externo nem prontidão comercial. `system/health` final: **healthy=true**. Acompanhantes permanecem nas mesmas versões e ativos.

Antes: auditoria efetiva 1.000 por padrão, detalhes 365 e resumos 730; 76 eventos, nenhuma tarefa/agenda. Depois da instalação, `google/configure-local` gravou os três valores em 0, com persistência confirmada (`25aea39b9e379a7bc0161de2`). `google/configuration-schema` expôs 0 efetivo, padrão 0 e mcp_mutable true. `google/maintenance` terminou complete/success, sem erros (`03f8da0290df490c1d2462c7`). A leitura posterior contém **79 eventos, incluindo todos os 76 anteriores**, e nenhuma tarefa removida. Como o site não possuía resultados de tarefas, a conservação de resultados expirados é a prova semeada nos laboratórios, não uma alegação de dados remotos inexistentes.

Índice remoto: 20 documentos com versão 0.20.0. README, guia 0.20.0 e SDK-PHP foram lidos integralmente pelo MCP remoto e comparados exatamente ao fonte. A reconstituição integral dos demais documentos já foi exercitada no MCP HTTP nativo. Nenhuma fixture/ability temporária foi instalada no Site-Teste.

**Limite do pedido 38:** o Site-Teste continua sem credencial Google (`configured:false`) e o Core 1.56.0 registra somente Search Console; a lista GA4 de consumidores é vazia. Portanto, a concessão ao Core, a consulta real de 30 dias, comparação real e revogação real não foram executadas. Nenhum site de produção foi alterado para contornar essa ausência.

## 6. Impactos e pedidos

**Emitido nesta rodada:** `wp-mcp-google-fator3-0.20.0-impacto-base-site-core-fator3.md`, revisão 1 de planejamento, pedido Google 38 / Core 313, ação necessária. O impacto existe porque há um novo contrato a consumir e um acervo a implementar no Core. O SDK Google já está entregue, com schema e exemplo no SDK-PHP; não foi necessário aguardar retorno do Core. Isso não implementa nem declara concluído o acervo no pacote Core. O documento foi preparado para encaminhamento; nenhuma mensagem externa foi enviada.

**Tratamento dos recebidos/anteriores:** o impacto MCP 0.29.1 → Google sobre repetição incerta permanece respeitado; `retryable` não é autorização para repetir uma escrita. O novo SDK é exclusivamente leitura e não repete automaticamente. Os relatórios atuais Core/Meta tratam ingestão/exclusão de mensagens; LinkedIn trata credenciais; Pipedrive depende de contrato próprio Core; não impõem nova mudança no Google no escopo examinado. Não foram emitidos impactos de simples aviso, resposta ou encerramento para esses pacotes. Os documentos recebidos permanecem como histórico.

## 7. Operação, reversão e pendências

1. **Core 313:** implementar consumidor/coletor/acervo usando o contrato público. Conferir concessão, propriedade, revisão, cotas, qualidade, falhas e persistência antes de habilitar agenda. Sem BigQuery e sem ler segredos/opções privadas Google.
2. **Homologação Google 38:** com Core compatível e propriedade autorizada, executar o aceite real de 30 dias, igualdade de recorte/contagem, auditoria e revogação. Provas sintéticas não substituem esse aceite. O aceite real de credenciais do pedido 36 permanece fora desta rodada.
3. **Distribuição:** os arquivos estão prontos; publicação de URL raw/GitHub e implantação na frota não foram executadas. A única alteração remota desta rodada foi o Google e sua retenção no Site-Teste autorizado.
4. **Conservação:** retenção ilimitada aumenta o uso de armazenamento e não amplia validade de tokens, cursores ou locks. Valores positivos explícitos existentes permanecem nos outros sites até alteração pela operação pública. Exclusão administrativa continua explícita; dados eliminados antes não reaparecem.
5. **Reversão:** preservar banco e salts. Rollback de arquivos foi testado no laboratório e não desfaz estado local/remoto. Atenção: a 0.19.0 não conhece 0 como ilimitado e normaliza para seus mínimos; antes de operar uma reversão de produção, interromper a manutenção e restaurar uma configuração/backup coerente. Preferir correção adiante para conservar o histórico ilimitado.

## 8. Arquivos

| Artefato | Nome | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | wp-mcp-google-fator3-0.20.0-instalador.zip | 822259 | `8c2456de80896dc7078321248a1df01c89745fc7f80a2c6e769ef1b6d543bbfd` |
| Fonte completo | wp-mcp-google-fator3-0.20.0-fonte.zip | 4890228 | `42c410ddcdf3fc2c1208a738e3ff3ecee1c6be09d1c7884c1bb558d21bba5e00` |
| Impacto Core, revisão 1 | wp-mcp-google-fator3-0.20.0-impacto-base-site-core-fator3.md | 2719 | `a0673be7de0842721838077447ae67619f3d254ffd92d68b80416660ac163c37` |

Somente o instalador é instalável. O fonte contém runtime igual, documentação canônica, build, testes, insumos de referência e evidências sanitizadas; sem dependências vendor/node_modules, banco, credenciais ou ZIP aninhado. Relatório externo canônico: `wp-mcp-google-fator3-0.20.0-relatorio.md`. Reprodução em `reproducao/LEIA-ME.md`.
