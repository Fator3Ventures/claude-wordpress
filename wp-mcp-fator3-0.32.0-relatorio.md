# Entrega — Fator3 MCP 0.32.0

Revisão 1 · 25/10/2026 · America/Sao_Paulo · Rodada: implementação.
Slug: `wp-mcp-fator3` · Basename: `wp-mcp-fator3/wp-mcp-fator3.php`.

**Versão corrente: 0.32.0, implementada, instalada e ativa no Site-Teste. Status: com-pendencias.** A correção de apresentação Core301 passou; a validação de Core300 revelou uma falha de autorização de resultados em cache no Core 1.53.0, também reproduzida com MCP 0.31.0. Não houve novo envio de correio. A correção de domínio fica com o mantenedor Core, com encaminhamento específico nesta entrega.

**Relatório externo canônico.** O fonte contém uma cópia anterior ao seu fechamento; a identidade final do ZIP aparece abaixo, evitando circularidade.

## 1. De onde esta versão entra

Base aceita: **MCP 0.31.0**, preservada sem alteração. Instalador-base: 883088 bytes, SHA-256 `2285c633b5d11c9990bed376f17291612b44958b073e0db2489efac20c1ec4ef`. Fonte-base: 4330580 bytes, SHA-256 `f8b80acd519a1d9800e97aac52c490e3aba96355b6ed95e81f5c61f88c0242ce`.

Entrada principal: Core **1.53.0**, seu relatório e impacto para MCP **revisão 2**, vinculados aos pedidos **Core 300 e Core 301 atualizado**. A rodada não inventa um número MCP novo. Aplicadas as normas comuns revisão 5 de 23/10/2026, mais atuais que as cópias revisão 4 existentes em project_sources. Os pacotes e documentos foram lidos dos anexos locais; os hashes de 12 ZIPs aceitos constam de `docs/entradas/0320/packages.json`.

Percursos comprovados: instalação limpa e atualização direta **0.31.0 → 0.32.0**, sem intermediária. Mínimos preservados/testados: WordPress **7.1.2**, PHP **8.3.6**, 64 bits. Integrado local: WordPress **7.1.3**, PHP **8.3.6**, MySQL **8.0.46**. Site-Teste: WordPress **7.1.3**, PHP **8.3.36**. Não ampliar essa matriz para runtimes não exercitados.

## 2. Convivência e encaminhamentos

| Acompanhante | Versão aceita | SHA-256 do instalador | Evidência própria |
|---|---|---|---|
| Site Core | 1.53.0 | `086adf2530809c73d30d38ccb747b0a8de8c7cd7419543273c2e2c50940d99f1` | Integrado local e Site-Teste; mapas, contadores e correio |
| Google | 0.19.0 | `d15868915e3fdf886d7e883a82d9d302df7242808fc94d45bf3e1857234759d1` | Ativação, descoberta e integridade local; ativo no Site-Teste |
| Meta | 0.10.1 | `f80d934fe1851bc887a0174190b42d73b36a8637f2f4824bdb5cfeb7a674ee95` | Ativação, diagnóstico, descoberta e integridade local; ativo no Site-Teste |
| LinkedIn | 0.10.1 | `6182ea63bff6788f5d2637467e7ab29d58568e37283d6ece82d3e58ee41c13bc` | Ativação, diagnóstico, descoberta e integridade local; ativo no Site-Teste |
| Pipedrive | 0.1.0 | `3366d83ca8908e407a0736812d30b8fa1506a8c1458a28cfb47eda6fd8f3c54f` | Presença ativa e registro do provedor no Site-Teste; sem operação comercial |

Não foi ativado Pipedrive no PHP local 8.3.6, abaixo do mínimo 8.3.36 declarado por ele. No Site-Teste permaneceram também DreamHost Panel Login 1.0.0, WP Super Cache 3.1.4 e Yoast SEO 28.7. A lista de versões/atividade dos oito plugins alheios é idêntica antes/depois. Não houve edição ou instalação de pacote acompanhante nesta rodada. As árvores locais de Core, Google, Meta e LinkedIn foram comparadas aos instaladores aceitos.

### Impacto emitido nesta rodada

**`wp-mcp-fator3-0.32.0-impacto-base-site-core-fator3.md`, revisão 1 — acao-necessaria, demanda-aberta.** O achado surgiu na validação Core300; foi registrado no plano antes de qualquer alteração na fronteira dependente. Responsável: mantenedor Core. Alinhar permission_callback aos gates de domínio, inclusive antes de reapresentar resultados idempotentes. Não é pedido de troca simultânea, concessão de capacidades no MCP ou reexecução de envio. Os critérios e o reprodutor estão no impacto.

### Tratamento dos impactos recebidos e anteriores

| Origem / pedido | Resposta desta rodada | Responsável / evidência |
|---|---|---|
| `base-site-core-fator3-1.53.0-impacto-wp-mcp-fator3.md`, revisão 2, Core301 atualizado | **Atendido no MCP 0.32.0**: mapas tipados nos dois diagnósticos e nas quatro projeções de configuração; linhas, revisão e contagens preservadas. | MCP; unitários 144, HTTP 21, aceite remoto e comparação antes/depois |
| Mesmo impacto, Core300 | Cinco abilities descobertas; perfis e recusas de novas intenções, revisão, incerteza, idempotência e auditoria passaram. **Aceite integral de autorização pendente**: reapresentação em cache após revogação expõe falha do permission_callback Core. | Core corrige domínio; MCP fornece 28 checks aprovados e reprodutor com 3 falhas em cada versão-base/alvo |
| Impacto Core 1.52.1 de contadores, atendido na 0.31.0 | Atendimento preservado; `passagens_24h` continua com três inteiros. Não reemitido impacto antigo para encerrar. | `current/companions.json` e regressão de redação |
| Pedido MCP67, base 0.31.0 | Tipos, schemas, casos de segredo, paridade das representações e metadados de redação preservados na matriz executada. | 218 checks unitários herdados e 30 checks HTTP |

As respostas acima ficam neste relatório, conforme norma revisão 5. O impacto emitido apresenta uma nova consequência técnica própria para o destinatário.

## 3. Mudanças e evidência

`SafeOutput` acompanha o caminho absoluto durante a sanitização. A exceção para `f3base_formularios_sinais` fica limitada aos caminhos publicados:

- `avisos.sinais_formularios.regras` e `assuntos[N].sinais_formularios.regras`, com `option` exata no objeto pai.
- `opcoes.f3base_formularios_sinais.{valor,padrao_declarado,valor_efetivo,valor_bruto}`.
- Prévia de configuração `antes`, `depois` ou `lido` na raiz, somente quando `nome` identifica exatamente a option. Até dois envelopes `data` do transporte são reconhecidos.

São aceitos até 100 sinais, nomes conforme `[a-z0-9_]{1,80}`, e cada regra deve conter **exatamente** `suspeito` e `aviso` como booleanos reais. Arrays e stdClass são preservados. Strings, coerções, campos extras, objetos arbitrários e mapas inválidos permanecem redigidos. Chaves numéricas aceitas pelo schema também foram verificadas. Caminhos semelhantes, schemas com exemplos, senha de correio e tokens fora da política não ganham a exceção.

`lido` sem identificação da option continua conservador: a operação real de gravação Core pode exigir releitura por `f3base/config-core-ler`. Não foi alterado esse contrato Core nem afrouxada a redação geral para contornar a ausência de contexto.

No Site-Teste, `token_vencido` e `token_revisao_anterior` retornaram `{suspeito:false,aviso:false}` e `token_assinatura_invalida_ou_ausente` retornou `{suspeito:true,aviso:true}`. As duas projeções coincidem com `linhas`, e a revisão permaneceu `6eb92dfababd5f4cc8b7ff8f6534472cd56aa76e5c05daa66a18725031769626`. Os contadores de 7/30 dias não mudaram.

O runtime difere da base em **4 arquivos**, com **460 arquivos idênticos**, nenhuma adição ou remoção: `includes/Release014.php` (mudança funcional), `includes/guide-content.php`, `includes/guide-documents.php` e bootstrap de versão. Nenhuma alteração em DataSafety, autenticação, autorização, execução, auditoria, SQL, recibos, schemas de banco, agenda ou credenciais. A política opera sobre a apresentação, sem regravar a configuração Core.

### Achado de autorização do Core

Em Core 1.53.0, a execução de email-enviar exige envio **e** leitura de leads, mas seu permission_callback admite `manage_options` como alternativa. Após uma prévia com chave idempotente, revogar qualquer capacidade de um administrador não bloqueia a reapresentação da prévia anterior. Uma nova intenção é corretamente recusada. O mesmo ocorreu com MCP 0.31.0 e 0.32.0: **8 verificações por combinação, 3 falhas de autorização em cada uma**. Esses casos não estão incluídos nos checks aprovados.

O teste complementar de recibo incerto manteve `smtp_sem_confirmacao`, `success=false` e `reenvio_automatico=false`; não repetiu SMTP. Não seria seguro executar a mutação novamente para descobrir uma permissão omitida pelo produtor. A solução solicitada está no permission_callback do Core, preservando suas verificações internas. Até essa correção, revogar a conexão ou usar perfil que recuse a ability corta o acesso pelo canal; a instalação desta versão não toma essa decisão pelo dono.

## 4. Instalação e prova da troca

| Cenário | Verificações finais | Resultado / evidência em `evidencias/0320/` |
|---|---:|---|
| Regras tipadas e redação anterior, PHP 8.3.6 | 144 + 218 | Todas aprovadas; `unit/` |
| Integrado WP 7.1.3 / Core 1.53.0 | 265 | Política HTTP 21; correio 28; redação HTTP 30; OAuth/CIMD 48; acompanhantes 16; adversarial 18; idempotência 7; mídia 9; descoberta 17; busca 11; admin nativo 26; documentos 34. `current/` |
| WP 7.1.2 limpo, somente MCP | 13 | Ativação 3; processo novo, inventário, cron, saúde e HTTP 10. `minimum/` |
| Atualização nativa 0.31.0 → 0.32.0 | 22 | Todas aprovadas; `upgrade-final/` |
| Sintaxe do instalador | 453 arquivos PHP | Sem falha; `lint.json` |
| Site-Teste WP 7.1.3 / PHP 8.3.36 | 15 | Todas aprovadas; `site-test.json` |
| Reprodutor de autorização do Core | 8 por versão MCP | **3 falhas por versão**, demanda aberta; `provider-base0310/` e `current/provider-mail-permissions.json` |

São **662 verificações automatizadas finais do MCP aprovadas**, mais lint e aceite remoto. Não se somam setup, tentativas anteriores ou as falhas conhecidas do produtor. O script de atualização foi ajustado para criar o diretório de evidência e falhar caso não consiga gravar o recibo; uma nova instalação isolada repetiu a atualização com sucesso e recibo salvo. Isso não alterou o instalador. Logs finais sem erro inesperado: as recusas de perfil/input são intencionais; três avisos nativos de atualização WordPress refletem rede externa bloqueada no laboratório. Instalação mínima e atualização final sem warnings.

Atualização local com quatro workers aquecidos e `opcache.validate_timestamps=0`: novas requisições observaram 0.32.0; application password, concessão/perfil OAuth, validade e renovação do token, confirmação SQL pendente, recibo concluído sem duplicação, recibo incerto, options false/vazias e backup privado permaneceram válidos. Todos os 464 arquivos instalados corresponderam ao ZIP, sem extras. Rollback foi somente pré-visualizado com preimagem válida.

### Site-Teste

Instalado em `https://fator3-teste-mcp-1.dreamhosters.com/` pelo conector existente: transferência em quatro partes, finalização com tamanho/hash e `plugins/upload` do ZIP temporário no mesmo site; `expected_slug=wp-mcp-fator3`, SHA-256 da seção 8, `activate=true`, `overwrite=true`. Operação **9b09f31d1fa82b1ac8ba7863d8155ff6**, backup **898a04af15968d9add1d6b2a**. Troca ativa 0.31.0 → 0.32.0; home e REST com HTTP 200 antes/depois e cache bypass confirmado. Reativação silenciosa em worker independente; o recibo não alega novo ciclo completo de activation hook nem prontidão comercial.

Consulta posterior `plugins/operation-status`: complete, file_state=candidate, active=true, verification_reason=verified, versão 0.32.0. `system/health`: healthy=true, sem falha de auditoria ou recuperação pendente. Plugins alheios preservados. SQL com senha/token sintéticos continuou mascarado. `email-enviar` em simulação para identificador inexistente retornou `contato_nao_elegivel`, `success=false`, isError=true, sem SMTP.

Documentação por `system/guide`: **31 documentos, 33 páginas, 217011 bytes UTF-8**, lidos até o fim com expected_sha256 e comparados byte a byte aos textos do instalador. Títulos e seções históricos conservam suas referências; envelope de versão, `release-0320` e `redacao` identificam o contrato desta entrega. Texto/structuredContent dos diagnósticos/configuração foram iguais. O conector não repassa `_meta` bruto: JSON Pointer e metadados de redação foram comprovados pelo transporte HTTP real local, não atribuídos à ponte remota.

O ZIP temporário foi removido com guarda de hash; files/stat confirmou ausência. Nenhuma rota ou arquivo PHP de QA, contato, usuário, mensagem ou configuração comercial foi criado no Site-Teste. Backups e registros normais da operação foram mantidos. Publicação raw/frota não foi executada e não há URL pública final inventada; o dono confere os hashes antes de distribuir.

## 5. Banco e volta de versão

Não há migração, tabela/coluna nova, configuração nova ou transformação de dados nesta versão. A leitura da política manteve sua revisão, valores e procedência; a atualização não troca configurações ou credenciais dos acompanhantes. A execução normal do canal e da instalação registra auditoria, recibos, backup e estado operacional próprios; não significa ausência absoluta de escritas no banco.

Voltar para 0.31.0 reintroduz o mascaramento dos três mapas token_* e não corrige a pendência do Core. O backup do uploader cobre arquivos; restaurá-lo não desfaz banco, auditoria, tráfego de sondas ou efeitos externos. O recibo declara `database_effects_reversible=false`. Não foi feito downgrade no site compartilhado.

## 6. O que permanece pendente

- **Core 1.53.0 / Core300:** corrigir permission_callback e repetir o reprodutor de revogação de capacidades. Responsável: mantenedor Core. O impacto individual traz critérios de aceite e mitigação operacional; não afirmar autorização de correio integralmente homologada.
- **SMTP/IMAP reais:** não testados nem configurados nesta rodada. Os testes de correio usam contatos/recibos sintéticos locais e simulação remota sem contato elegível. Entrega no fornecedor e sincronização da caixa dependem de conta própria autorizada e homologação pelo dono/Core.
- **OAuth/CIMD de clientes externos:** 48 regressões nativas com HTTP controlado passaram; a conexão OAuth existente serviu ao aceite remoto. Isso não substitui nova autorização interativa no ChatGPT/Claude nem encerra pendências históricas de B22/CIMD.
- **Outros fornecedores, frota e runtimes:** nenhuma operação comercial Google/Meta/LinkedIn/Pipedrive, gasto, publicação ou distribuição foi realizada. Outras combinações, multisite e todos os formatos possíveis de segredo não foram homologados. Não se afirma impacto zero universal.

## 7. Credenciais e configuração do dono

Não há credencial ou campo novo a preencher no MCP. Tela preservada: **Ferramentas → Fator3 MCP**. Instalar a atualização não exige reemitir tokens ou application passwords. A conexão de manutenção não concede capacidades WordPress de domínio; configuração e segredos de e-mail continuam pertencendo ao Core. As contas locais de teste são descartáveis; nenhum segredo, cookie, dump de banco ou corpo privado de mensagem integra a entrega.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | wp-mcp-fator3-0.32.0-instalador.zip | 885606 | `fd2097055383a26e6ca5b79b655f0b3740c337a42dab6ce2b43b4236c07496b1` |
| Fonte | wp-mcp-fator3-0.32.0-fonte.zip | 4443847 | `d7413eda5cae051c35c9f08f21a3e47cb9fc02e8e0d22462dd094b2cbf445c4e` |

Relatório externo: **wp-mcp-fator3-0.32.0-relatorio.md**. Impacto: **wp-mcp-fator3-0.32.0-impacto-base-site-core-fator3.md**. Só o instalador é instalável: raiz `wp-mcp-fator3/`, 464 arquivos, incluindo 56 índices de proteção. O fonte possui raiz `wp-mcp-fator3-0.32.0-fonte/`, código, build, testes, entradas, documentos, evidências sanitizadas e esta cópia do relatório. Nenhum ZIP contém outro ZIP da entrega. O fonte é gerado uma única vez após congelar instalador, evidências e relatório interno; seu hash fica no relatório externo canônico.
