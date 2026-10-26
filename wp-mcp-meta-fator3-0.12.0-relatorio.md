# Entrega — Fator3 MCP Meta 0.12.0

Revisão 1 · 26/10/2026 · Rodada: implementação.  
Slug: `wp-mcp-meta-fator3` · Basename: `wp-mcp-meta-fator3/wp-mcp-meta-fator3.php`.  
Status: **apta no escopo local testado, com integração automática de exclusão no Core e homologação externa pendentes**.

## 1. De onde esta versão entra

Base direta aceita: **0.11.1**, sem versão intermediária obrigatória. Foram examinados o código entregue, os pedidos anteriores, a ampliação de retenção solicitada pelo dono e as novas entradas do Core 1.56.0. A versão minor 0.12.0 segue a regra de nova rodada. As instruções comuns e o padrão de desenvolvimento **revisão 5, de 23/10/2026**, prevalecem sobre a cópia revisão 4 reanexada, inclusive a regra expressa de não gerar impactos apenas para responder ou encerrar pedidos.

| Base/entrada | Bytes | SHA-256 |
|---|---:|---|
| `wp-mcp-meta-fator3-0.11.1-instalador.zip` | 235017 | `b084bf2498eddc0eb93410c04efdd166ba84b2831541e2b5a2acf8dcfe3aa6c1` |
| `wp-mcp-meta-fator3-0.11.1-fonte.zip` | 1778388 | `e12e1d6f3a9b9daa8907840bdda40903ec307596971cdff458e7de88a25415b1` |
| `base-site-core-fator3-1.56.0-instalador.zip` | 2667464 | `e9dd77379d64706ad37de2428dc91a02bdaeb0649f68b38d3024ffcaac4ebed9` |
| `base-site-core-fator3-1.56.0-fonte.zip` | 3950523 | `36b54c1711c39aaeb8e32c1ab1b77d84d58bc5c82de905b2699b50ae38aa9b85` |

Entradas novas preservadas em `inputs/0.12.0`: relatório do Core, impacto `base-site-core-fator3-1.56.0-impacto-wp-mcp-meta-fator3.md`, revisão 1, e identidades dos pacotes. O documento de impacto continua identificado como planejamento em sua origem; a existência do instalador foi verificada separadamente. Plano desta rodada: `planning/RELEASE-0120.md`.

Instalação limpa e atualização direta foram exercitadas em WordPress real descartável. Matriz final: **WordPress 7.1.3/PHP 8.3.36** e **WordPress 6.4/PHP 8.1.2-1ubuntu2.28**, ambos de 64 bits, MySQL 8.0.41. O PHP 8.1.34 usado na preparação do laboratório não é a prova do mínimo. Lint local adicional: PHP 8.3.6, 28 arquivos aprovados.

## 2. Convivência e encaminhamentos

Os cinco acompanhantes abaixo foram carregados juntos no laboratório nativo, com hashes dos arquivos de runtime conferidos antes/depois. Permanecem nas mesmas versões no Site-Teste; somente o Meta foi atualizado nesta rodada.

| Acompanhante testado | Versão | Bytes do instalador de referência | SHA-256 do instalador |
|---|---|---:|---|
| Fator3 Site Core | 1.56.0 | 2667464 | `e9dd77379d64706ad37de2428dc91a02bdaeb0649f68b38d3024ffcaac4ebed9` |
| Fator3 MCP | 0.33.0 | 888204 | `f16ee3e31e4143ffb42c566ea6da4f2da81d3771a01a0f90b5d34e3d02ac8caa` |
| Fator3 MCP Google | 0.19.0 | 809436 | `d15868915e3fdf886d7e883a82d9d302df7242808fc94d45bf3e1857234759d1` |
| Fator3 MCP LinkedIn | 0.10.1 | 254066 | `6182ea63bff6788f5d2637467e7ab29d58568e37283d6ece82d3e58ee41c13bc` |
| Fator3 MCP Pipedrive | 0.1.0 | 42095 | `3366d83ca8908e407a0736812d30b8fa1506a8c1458a28cfb47eda6fd8f3c54f` |

Evidência: `tests/companion-hashes0120.json`, `evidence/integrated-integration0120.json` e inventários em `evidence/shared-install0120.json`. DreamHost 1.0.0, WP Super Cache 3.1.4 e Yoast 28.7 também permaneceram ativos no site compartilhado; isso comprova convivência de carregamento, não homologação funcional completa desses produtos.

**Impactos emitidos nesta rodada:** nenhum. O escopo examinado foi o diário de mensagens, ingestão pelo Core, autorização do transporte MCP, retenção, cron e carregamento simultâneo dos demais pacotes. Não foi identificada consequência nova que exigisse pedido independente ao LinkedIn, Google ou Pipedrive. Não se gerou arquivo de impacto para registrar a resposta ao Core. Os documentos antigos permanecem como histórico, sem reentrega como encaminhamento atual.

**Tratamento do impacto Core 1.56.0 → Meta, revisão 1, Meta18(b)/Core309:** o Meta entrega o contrato público local **`instagram-message-erasure/1.0.0`**, schema gerado, quatro métodos SDK, autorização corrente, revisão, idempotência, recibo mínimo e impedimento durável de reimportação. A exclusão funciona com token Meta revogado e conexão removida. O atendimento do lado Meta está comprovado pelas suítes de privacidade e integração de 20 verificações com o consumidor real do Core. **O Core 1.56.0 ainda não invoca esse contrato automaticamente.** Seu mantenedor deve capturar o alvo antes de apagar o payload privado, confirmar a transação local e integrar a chamada/recibo; a indicação `pendente_sdk_exclusao_meta` não foi encerrada no código alheio por esta entrega.

**Impacto anterior Meta 0.11.1 → Core, revisão 3, Meta18(b)/Core309:** o consumidor `instagram-first-message/1.0.0` está agora disponível no Core 1.56.0. A prova própria cobre registro no bootstrap, opt-in dos dois lados, persistência mínima cifrada, recibo, deduplicação, reconciliação e exclusão local Core. O teste coordenador chama explicitamente o novo SDK Meta após a exclusão Core e comprova os dois bloqueios. Isso não equivale a declarar entregue a futura automação de exclusão do Core.

Os cuidados anteriores de repetição incerta do MCP 0.29.1, revisão 2, e preservação de jobs/convivência do impacto LinkedIn 0.8.1, revisão 2, R1/R2, continuam cobertos pelas regressões `integration0120` e `review071`. Não houve troca de cliente Lead Sync, alteração de estado ou código LinkedIn. Meta 0.12.0 pode ser instalado antes da futura integração Core: o contrato de ingestão permanece compatível e a atualização não ativa contatos nem exclui registros automaticamente.

## 3. Mudanças e evidência

| Pedido | Mudança entregue | Evidência e limite |
|---|---|---|
| Exclusão pública dos identificadores Meta após exclusão do contato | SDK `Fator3\Meta\Messaging`: `privacyContract()`, `privacyStatus($target)`, `eraseLocalData($request)`, `erasureReceipt($idempotencyKey)` | 76 verificações no ambiente corrente e 76 no mínimo; quatro adicionais após reinício em cada ambiente |
| Eliminar mesmo após revogação do token ou remoção da conexão | Operação inteiramente local, sem exigir token, ativo selecionado, consumidor ou conexão ainda existente | Casos sem conexão, token revogado e repetição depois de remover a conexão; nenhuma chamada Graph para exclusão |
| Autorização atual, revisão e repetição verificável | `manage_options` atual; concessão MCP válida quando presente; escrita remota somente em perfil maintenance/custom; schemas fechados; revisão opaca e chave estável | Rejeições de anônimo, assinante, perfil leitura, concessão revogada, revisão obsoleta, alvo cruzado e reutilização de chave |
| Remover identificadores e associação ao contato, impedindo reimportação | Exclusão integral do `message_event`; bloqueio HMAC cifrado sem identificadores brutos; recibo técnico sem conexão/conta/remetente/mensagem/evento/contato | Testes em pending, reserved, uncertain, persisted, suppressed e evidence_changed; inspeção do bloqueio/recibo; limpeza do diário e reinício |
| Concorrência, falha parcial e continuação automática | Trava comum com receive/process; bloqueio gravado antes da remoção; revisão do escopo; remoção de cursores do cron; worker não agenda cursor anterior à exclusão | Falhas injetadas na remoção e no recibo, retomada da mesma requisição, corrida entre consulta e tick, chamada reentrante no consumidor e ausência de recriação do registro |
| Preservar retenção ampliada e funcionalidades existentes | Nenhuma redução de retenção; histórico, resultados, auditoria, exportações, diário e Stories continuam com políticas da base; exclusão somente explícita | 77 verificações de regressão no corrente, 75 no mínimo; atualização preserva dados e escolha finita explícita posterior à migração anterior |

O alvo contém `connection_id`, `account_id` e exatamente um de `sender_id` ou `event_id`. **event_id é a chave do remetente escopado à conexão/conta**, não o message_id Graph nem o record_id do Core. A escrita acrescenta `expected_revision`, SHA-256 opaco retornado por `privacyStatus`, e `idempotency_key`, 16–128 caracteres permitidos, sem dados pessoais. Essa revisão não é a revisão inteira de `deliveryReceipt`. O schema executável está em `docs/messaging-privacy-schema.json`; exemplos e limites em `docs/MESSAGE-PRIVACY.md`.

Uma exclusão preventiva de alvo ausente também cria bloqueio. A mesma chave/alvo repete o recibo confirmado; outro alvo é `idempotency_conflict`. Estado restaurado fora do SDK invalida a repetição concluída com `erasure_state_changed`, exigindo nova leitura e requisição. Após falha parcial, o bloqueio pode existir sem exclusão concluída: não há sucesso presumido. A mesma requisição pode retomar após corrigir a causa.

O recibo contém contrato, receipt_id opaco, estado, presença/remoção local, impedimento de reimportação, revisão, instante e `external_copies_erased=false`. A consulta do recibo é histórica; `privacyStatus` é a leitura corrente. Os HMACs retidos são pseudônimos técnicos necessários à proteção, não promessa de anonimização absoluta.

**Fronteira de transação:** a operação recusa uma transação SQL ativa com `transaction_active`, sem confirmar ou desfazer trabalho do consumidor. A detecção usa SAVEPOINT aleatório e RELEASE; erro 1305 fora de transação é esperado e tratado. Outros erros falham de forma fechada. Referência oficial: [MySQL SAVEPOINT/RELEASE](https://dev.mysql.com/doc/refman/8.0/en/savepoint.html). A hipótese inicial de usar `@@session.in_transaction` mostrou-se incompatível com o servidor; foi corrigida no candidato antes da instalação final e novamente provada nas duas matrizes.

Não foram acrescentadas abilities nem endpoints de exclusão: são quatro métodos públicos PHP para consumidores locais. O consumidor continua responsável pela autorização da sua operação de domínio e proteção da entrada. As 41 abilities, seus schemas de entrada, JavaScript e CSS permanecem iguais à base. Mudanças funcionais concentram-se em `MessagePrivacy.php` e `Messaging.php`; demais alterações são bootstrap, versão, build, catálogo e documentação. A comparação está em `evidence/runtime-diff0120.json`.

## 4. Instalação e prova da troca

Pacote final instalado em **https://fator3-teste-mcp-1.dreamhosters.com/** pela operação `plugins/upload-base64`, com `overwrite=true`, `activate=true`, `expected_slug=wp-mcp-meta-fator3` e SHA-256 da seção 8. A base ativa observada era 0.11.1. Operação de pacote: `3c854c127000166fdfc0a9cff7b69280`; backup de arquivos: `f0be8f0c6bbef40af419c573`. Resultado confirmado: 0.12.0 ativa, aplicação concluída, PHP novo. A substituição usa reativação silenciosa; não se confunde com instalação limpa, coberta separadamente nos laboratórios.

Home e REST retornaram HTTP 200 antes/depois em sondas anônimas internas com bypass de cache verificado. Isso não prova acesso por uma rede externa nem homologação comercial. Em requisições posteriores, `meta/health {}` retornou versão 0.12.0, armazenamento/criptografia disponíveis, `state=ok`, sem issues, zero conexões e zero agendas ativas. `meta/selftest {}` aprovou 8/8 verificações locais, com `external_checks=not_run` e `remote_homologated=false`. Evidência: `shared-install0120.json`.

| Ambiente/cenário | Resultado | Evidência em `evidence/` |
|---|---:|---|
| WP 7.1.3/PHP 8.3.36, mensagens/insights/Stories/retenção/exportação, incluindo miniatura com editor de imagem real | 77/77 | `current-release0110.json` |
| Mesmo ambiente, SDK de privacidade e falhas | 76/76 | `current-privacy0120.json` |
| Mesmo ambiente, reinício após limpeza do diário | 4/4 | `current-privacy0120-restart.json` |
| Instalação isolada limpa, REST/admin/permissões, catálogo | 30/30 | `current-isolated0120-smoke.json` |
| Consumidor real Core 1.56.0, coordenação explícita de exclusão | 20/20 | `integrated-coreprivacy0120.json` |
| MCP e cinco acompanhantes, autorização/transporte, hashes e repetição | 25/25 | `integrated-integration0120.json` |
| Metadados de 41 abilities, documentação integral paginada e registro MCP | 123/123 | `integrated-release090-metadata.json` |
| Regressões de identidade, Stories e aviso por incidente | 41/41 | `integrated-release0100.json` |
| Preservação de payload/revisão/data de job ilegível em concorrência | 11/11 | `integrated-review071.json` |
| Saúde, recuperação e ausência de envio indevido | 23/23 | `integrated-release070.json` |
| WP 6.4/PHP 8.1.2, regressões de mensagens/Insights/arquivo/retenção | 75/75 | `minimum-release0110.json` |
| Mesmo mínimo, privacidade / reinício / instalação isolada | 76/76; 4/4; 30/30 | `minimum-privacy0120.json`, `minimum-privacy0120-restart.json`, `minimum-isolated0120-smoke.json` |
| Atualização direta 0.11.1 → 0.12.0 | 10/10 | `upgrade0120.json` |
| Site-Teste compartilhado, diagnóstico após instalação | 8/8 | `shared-install0120.json` |
| Site-Teste, leitura completa e igualdade dos documentos com o instalador | 23/23 | `shared-docs0120.json` |

São verificações/asserções dos cenários descritos, não testes de carga nem acessos reais ao fornecedor. No mínimo não há editor de imagem: os dois casos que exigem o editor real foram executados no ambiente corrente; o comportamento de editor indisponível passou no mínimo. `minimum-environment090.json` confirma versão exata, MySQL, 64 bits, criptografia e ausência de problemas no log do pacote.

Na atualização foram preservados byte a byte 11 registros cifrados, incluindo duas conexões, dois jobs, quatro eventos, resultado, agenda e Story, mais uma linha de histórico. Configurações e política ilimitada foram preservadas; uma política finita deliberadamente escolhida após a migração de retenção anterior também permaneceu. Nenhuma chave de privacidade ou exclusão foi criada pela atualização.

**Documentação:** `meta/documentation {"document":"index"}` lista os 23 documentos. Leituras usam `document`, `offset`, `limit_bytes` e `expected_revision`; concatenação sem separadores, SHA-256 e bytes integrais foram conferidos. O teste nativo usa páginas de 257 bytes; a leitura final pelo transporte MCP leu cada documento completo e o comparou byte a byte ao instalador. `MESSAGE-PRIVACY.md` e o schema gerado estão instalados e disponíveis ao Core/agentes.

**Limpeza:** tabelas, diretórios e manifestos dos laboratórios foram removidos: 89 tabelas no laboratório integrado corrente e 14 em cada laboratório de atualização/mínimo, zero remanescentes em cada limpeza. O MU temporário `f3-meta-qa0120.php` foi removido com guarda de hash e backup; sondas posteriores passaram. Evidências `current-cleanup0120.json`, `upgrade-cleanup0120.json`, `minimum-cleanup0120.json` e `shared-install0120.json`. Auxiliares de recuperação preexistentes e backups da ferramenta foram preservados. Não foram criados contatos comerciais no banco compartilhado.

**Falhas encontradas durante desenvolvimento:** além da detecção SQL corrigida, fixtures precisaram iniciar o orçamento HTTP, separar uma premissa de armazenamento global vazio, conceder as capacidades de leads ao administrador descartável do Core e concluir a migração pendente da base antes do snapshot de atualização. As políticas do produto não foram afrouxadas para fazer os testes passarem. As evidências finais acima passaram; tentativas anteriores em `development0120/` são históricas, não provas aprovadas. Não houve modificação no instalador depois da instalação final.

## 5. Banco e volta de versão

Não há tabela nova nem migração automática de dados nesta versão. Mantêm-se a tabela cifrada de registros e o histórico existentes. Somente uma **exclusão explícita** pode criar a option cifrada `f3_meta_message_privacy_key` e registros sem expiração nos buckets `message_suppression`, `message_erasure_receipt` e `message_privacy_scope`. O segredo aleatório HMAC é independente do token Meta; registros novos não guardam identificadores brutos de remetente/mensagem/contato, connection_id/account_id ou o event_id público anterior.

A ordem é bloqueio durável, avanço da revisão do escopo, remoção das continuações do cron, remoção CAS do evento, confirmação da ausência e recibo. Uma falha não desfaz o bloqueio nem declara conclusão inexistente. A limpeza administrativa do diário não remove o impedimento. A ausência/corrupção da chave com bloqueios existentes falha de forma fechada; não cria identidade substituta silenciosamente.

**Restauração:** preservar conjuntamente salts, chave de privacidade, bloqueios e recibos. Restaurar backup anterior à exclusão, ou remover chave e bloqueios manualmente, pode reintroduzir dados e remover a proteção; reaplicar as exclusões antes de reabilitar ingestão. O SDK não elimina backups externos.

**Rollback para 0.11.1:** preservar o backup e os dados; antes de voltar, desativar recepção/webhook/contatos e suas agendas. A 0.11.1 não interpreta os novos bloqueios e não deve retomar ingestão após uma exclusão feita na 0.12.0. Restaurar apenas arquivos não recupera registros apagados, não desfaz efeitos externos e não confirma a integração do Core. Não foi feito rollback destrutivo no site compartilhado; a preservação da base foi provada no laboratório de atualização.

## 6. O que permanece pendente

1. **Mantenedor Core:** integrar o SDK após a confirmação da própria transação, preservar temporariamente o alvo cifrado até conferir o recibo e manter o tombstone próprio. O teste de coordenação explícita passou; o fluxo automático de exclusão no Core 1.56.0 continua pendente e não foi modificado por esta rodada.
2. **Dono/operador Meta:** homologar credenciais, produtos, App Review, escopos, ativos, origens disponíveis e capacidades reais dos pedidos 18/19. O site compartilhado tem zero conexões Meta; os testes usam Graph sintético. Não se declara acesso real, identificação de origem indisponível, criação de contato real ou entrega externa comprovada.
3. **Limites do contrato:** a exclusão é do diário local escopado a uma conexão/conta/remetente. Não apaga Graph, Core, Pipedrive, cópias/respostas ou cursores já entregues ao cliente. Consultas autorizadas de conversas ainda leem a fonte remota. Outra connection_id/conta é outro escopo; não há identificação transversal de pessoas. Preservar o bloqueio depende da guarda/restauração correta dos dados técnicos.
4. **Matriz adicional:** MariaDB nativo, carga prolongada e outros sistemas de banco não foram exercitados. Não houve nova prova visual de navegador: JavaScript/CSS e fluxo de interface não mudaram; os testes REST, metadados e permissões foram executados. Implantador não disponível nesta matriz, portanto sua integração é `nao-avaliado`, sem risco novo concreto identificado nesta alteração.
5. **Frota/publicação:** não houve push, publicação raw nem implantação em produção/frota. A URL raw final depende do responsável por implantação; quando publicada, conferir exatamente slug e hash da seção 8. Os artefatos são entregues ao dono para essa etapa.

## 7. Credenciais e configuração do dono

Nenhuma credencial real foi incluída em código, evidência ou relatório. Foram usados identificadores, tokens e respostas sintéticos nos laboratórios; zero chamadas Graph reais, contatos reais ou notificações reais. O teste Core usou suas classes reais em banco descartável e 13 respostas HTTP sintéticas; capacidades de leads foram concedidas somente ao administrador descartável, sem alteração de roles do site compartilhado.

Tokens manuais, seleção de ativos, opt-in de recepção/contatos e aprovação de escopos continuam na configuração existente em Ferramentas → Fator3 MCP Meta. A instalação não configura nem ativa esses recursos automaticamente. Para exclusão local, não é necessário preencher token novo: é necessária autorização administrativa atual. Revogação da concessão MCP continua impedindo uso pelo agente revogado; revogação do token Meta não impede um administrador autorizado de apagar dados locais.

Preservar salts, chave de criptografia/privacidade e backups técnicos necessários. Nunca colocar identificadores pessoais na chave de idempotência. Retenção ilimitada continua como padrão de conservação dos dados existentes; não amplia prazos de tokens, nonces, locks ou cursores, nem recupera dados já apagados.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `wp-mcp-meta-fator3-0.12.0-instalador.zip` | 253225 | `b519203886d0964fa531c70cd0a66e2f8e199ff04700f0c3c5fa946d6d83e880` |
| Fonte | `wp-mcp-meta-fator3-0.12.0-fonte.zip` | 1973443 | `255236ad214851283c5cdad5be523ef9ff2290a636dd3d008738bc17c75bca5b` |

Relatório: `wp-mcp-meta-fator3-0.12.0-relatorio.md`. **Este é o relatório externo canônico, fechado após o fonte.** A cópia incluída no fonte antecede seu fechamento e remete a este arquivo para os bytes e SHA-256 finais, evitando circularidade. O instalador tem raiz `wp-mcp-meta-fator3/`; o fonte tem raiz `wp-mcp-meta-fator3-0.12.0-fonte/`, runtime idêntico ao instalador, código canônico, build, testes, evidências sanitizadas e esta cópia. Nenhum ZIP contém outro ZIP. Nenhum relatório de impacto novo acompanha esta rodada.
