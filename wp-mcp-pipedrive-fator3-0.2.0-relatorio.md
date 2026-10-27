# Entrega — Fator3 MCP Pipedrive 0.2.0

Revisão: **2** · Data: **26/10/2026, America/Sao_Paulo** · Rodada: instalação e homologação autorizadas
Slug: `wp-mcp-pipedrive-fator3` · Versão/build: `0.2.0`
Status: **apta-no-escopo-testado** — instalada e ativa no Site-Teste; retenção, preservação, rotas MCP, documentação e saúde verificadas. Fornecedor real e inspeção visual completa de navegador não foram exercitados nesta rodada.

**Relatório externo canônico atualizado.** A revisão 1 registrava a instalação compartilhada bloqueada pela revisão automática. A instrução posterior do dono, “instale e teste no site-teste”, autorizou a implantação, executada com sucesso nesta revisão. Os ZIPs fonte/instalador permanecem byte a byte iguais à entrega original. A cópia interna do relatório no fonte permanece congelada na revisão 1; o estado atual de homologação é o desta revisão 2 e de seu complemento de evidências.

## 1. De onde esta versão entra

Base direta: **0.1.0 → 0.2.0**, sem intermediária. Instalador da base: 42.095 bytes, SHA-256 `3366d83ca8908e407a0736812d30b8fa1506a8c1458a28cfb47eda6fd8f3c54f`. Fonte da base: 159.941 bytes, SHA-256 `bb06315b60a5b0a36c0458d9dcb000505e52b5f444278a3effb26414186a3f2c`.

Escopo implementado: **Pedidos MCP Pipedrive 2(a–d)**, diário sem prazo, aberto em 26/10/2026. A aba recebida informa o item 1 já entregue e homologado pela frota na 0.1.0; essa homologação histórica não é atribuída a esta execução.

Considerados os fontes, instaladores e relatórios Core 1.56.0, MCP 0.33.0, Meta 0.12.0; a entrega Pipedrive anterior; o impacto Pipedrive 0.1.0→Core; e as normas revisão 5 distribuídas pelo Core, que prevalecem sobre a revisão 4 reanexada. As entradas e seus hashes estão no fonte original. Respostas e encerramentos são registrados neste relatório, sem reemitir impacto apenas para comunicar seu desfecho.

Ambiente efetivamente executado: **WordPress 7.1.3, PHP 8.3.36 de 64 bits, MySQL 8.0.41/InnoDB**. São os mínimos WordPress/PHP do cabeçalho. A instalação limpa e a atualização nativa foram provadas na rodada anterior em laboratórios descartáveis. Agora foi realizada a atualização no Site-Teste compartilhado.

## 2. Convivência e encaminhamentos

| Pacote | Início desta instalação | Estado final observado |
|---|---|---|
| Pipedrive | 0.1.0 ativo | **0.2.0 ativo**, instalado por esta execução |
| Core | 1.56.0 ativo | 1.56.0 ativo |
| MCP | 0.33.0 ativo | 0.33.0 ativo |
| Google | 0.20.0 ativo | 0.20.0 ativo |
| Meta | 0.12.0 ativo | 0.12.0 ativo |
| LinkedIn | 0.10.1 ativo | **0.11.0 ativo**, mudança externa às operações desta execução |

DreamHost Panel Login 1.0.0, WP Super Cache 3.1.4 e Yoast 28.7 permaneceram ativos. Foram observados nove plugins no início e no fim. Esta execução alterou somente o produto Pipedrive e o instrumento temporário de seu teste; não atualizou nem reverteu acompanhantes. A última sonda, após observar LinkedIn 0.11.0, confirmou home/REST com HTTP 200 e o status Pipedrive 0.2.0. Isso não é homologação funcional das integrações sociais dos outros plugins.

**Encaminhamento anterior:** `wp-mcp-pipedrive-fator3-0.1.0-impacto-base-site-core-fator3.md`, revisão 1, Core 294 C1–C8/Pipedrive 1, solicitava ao mantenedor Core o cliente `pipedrive-api-client/1.0.0`. O histórico recebido informa entrega desde Core 1.51.0. A inspeção e oito verificações da rodada de implementação com o cliente original Core 1.56.0 confirmaram o contrato no escopo exercitado. O bloqueio de cliente ausente está superado; não se declara nova homologação integral C1–C8/A1–A16 no fornecedor.

**Novos impactos: zero.** Foram avaliados contrato Core, transporte/autorização/documentação MCP e convivência. A política de retenção é própria do Pipedrive; as novas rotas usam o registro/gate existentes. Nenhuma mudança técnica foi solicitada a outro mantenedor. Publicação e distribuição aos sites-porta continuam com a frota e não foram executadas.

## 3. Mudanças e evidência

| Pedido | Comportamento entregue | Evidência |
|---|---|---|
| 2(a): prazo configurável por MCP/painel; opção e padrão sem prazo | `diario_dias=0` significa sem prazo; escolha explícita de 1–36.500 dias. Rotas `pipedrive/retencao-ler` e `pipedrive/retencao-configurar`, mais formulário administrativo | Padrão zero após atualização; gravação/releitura via conexão MCP; POST nativo do painel; recusa de revisão antiga, prazo inválido e prazo finito sem confirmação |
| 2(b): recibos expiram sem eliminar a linha técnica | Recibos cifrados continuam em 180 dias; diário tem política independente | No Site-Teste, recibo vencido removido e linha de 400 dias preservada byte a byte após prévia/aplicação |
| 2(c): status informa prazo vigente | `status.data.retencao` inclui diário, recibos, prévias e revisão | Status consultado pela conexão real mostra zero/sem prazo mesmo sem autorização comercial Core |
| 2(d): atualização preserva registros | Sem expurgo ou migração destrutiva na troca; escolha explícita preservada | Atualização nativa anterior preservou três operações e duas linhas antigas; banco compartilhado vazio antes/depois, com fixtures removidas ao final |

Todos os quatro itens estão **implementados e validados em WordPress**. O aceite de retenção foi exercitado na instalação compartilhada, com cliente sintético em memória e nenhum HTTP ao fornecedor. Não se confunde essa prova local com homologação no Pipedrive real.

A opção própria `f3_pipedrive_retention` usa JSON e autoload desativado. Ausência significa padrão sem prazo, sem gravação na leitura. Configuração exige `manage_options`, revisão esperada e confirmação para prazo finito. Comparação atômica, geração de revisão, releitura persistida e trava compartilhada com a limpeza protegem concorrência. Política ilegível/trava indisponível falham sem expurgo.

Salvar não exclui registros nem chama fornecedor. Limpeza continua sob demanda em prévia/aplicação, sem cron. Recibos: 180 dias desde a criação da prévia; prévias: 900 segundos. Tentativas incertas e suas linhas são preservadas para reconciliação. Identidades públicas, seis rotas anteriores, duas tabelas e schema 1 foram preservados; são oito rotas no total. Não há token, cliente HTTP ou orçamento próprio.

## 4. Instalação e prova da troca

Site: `https://fator3-teste-mcp-1.dreamhosters.com/`. Instalação via **WP MCP fator3-teste**, `plugins/upload-base64`, com `activate=true`, `overwrite=true`, `expected_slug=wp-mcp-pipedrive-fator3` e SHA-256 da seção 8. O pacote instalado é o mesmo que passou nos testes anteriores.

- Operação de instalação: `eb2b10fafcb95b67d5979ded`.
- Operação do pacote: `a1205569292e9dc1125c7a2803496cdd`.
- Backup dos arquivos anteriores: `7161f5dba3b515f7d15f9727`.
- Backup prévio das duas tabelas próprias: artefato `df46cfd9289200351e384fd16c78bfef`, 1.126 bytes, SHA-256 `4c20b2390756e213268bdcb9df67b4cb426b83e944a99bfb33c74a8ebac595cc`, zero linhas.
- Resultado: `applied=true`, `recovery_status=applied`, versão anterior 0.1.0, final 0.2.0, ativa antes/depois. Reativação silenciosa em PHP novo; o mecanismo não afirma execução do ciclo completo de hooks de ativação nessa troca.
- Home e REST responderam HTTP 200 antes/depois. Os **21 arquivos instalados** tiveram seus SHA-256 comparados individualmente com o runtime do instalador: todos iguais.

| Prova | Resultado | Escopo |
|---|---|---|
| Rodada anterior: operações/REST/transações/concorrência | 76/76 | WordPress descartável |
| Rodada anterior: retenção/painel/revisão/travas | 33/33 | WordPress descartável |
| Rodada anterior: integração MCP/documentos | 25/25 | Executor original MCP 0.33.0 |
| Rodada anterior: cliente original Core | 8/8 | Core 1.56.0 e HTTP sintético |
| Rodada anterior: upgrade/reativação | 9/9 + 2/2 | Atualização nativa e novo processo |
| Rodada anterior: código/empacotamento | 37/37 | Lint, schemas, ZIP e reprodução |
| **Esta rodada: cenário na instalação compartilhada** | **22/22** | Prévia/aplicação, linha de 400 dias, recibos, painel, permissões, restauração e limpeza |
| Esta rodada: conexão MCP real | Aprovado | Oito rotas 0.2.0, leitura/gravação/releitura de política, repetição sem alteração e recusas esperadas |
| Esta rodada: documentação | **9/9 documentos completos** | Textos, bytes e hashes iguais aos arquivos entregues |
| Esta rodada: REST anônimo | **401 nas duas rotas consultadas** | `retencao-ler` e `status` |
| Esta rodada: saúde final | **11/11 verificações** | Saúde local; home/REST com 200 em sonda final |

As **153 verificações funcionais anteriores** são mantidas como evidência histórica; as **22 verificações desta rodada** são informadas separadamente. Não se somam sondas, verificações negativas ou tentativas preliminares como testes funcionais adicionais.

O cenário compartilhado criou uma linha concluída e uma tentativa incerta com 400 dias, além de nova prévia. Usou o código Pipedrive efetivamente instalado, cliente em memória e bloqueio HTTP limitado à requisição de teste. Confirmou preservação exata da linha antiga, expiração independente do recibo, prévia, aplicação, replay sem nova chamada, ausência do valor da nota no diário, status sem prazo, painel renderizado/POST com nonce, recusa de usuário anônimo e restauração do cliente original. Foram três chamadas sintéticas, uma escrita sintética, **zero tentativas HTTP**.

O primeiro formato do instrumento temporário foi recusado pelo executor antes do cenário. Seu schema/registro foram ajustados; consulta intermediária confirmou zero linhas. A execução final passou 22/22, sem alterar nenhum arquivo do produto. O instrumento foi removido com hash esperado; a ability temporária deixou de existir. Backup de remoção: `8b849f0094d9c61017e9839c`; operação `ae5cce6a12bf3f01492b7f5b`.

**Documentação MCP:** `pipedrive/documentacao-ler` leu índice, especificação, configuração, uso, contratos, agentes, operação, release e schemas pela conexão autenticada. O conteúdo completo dos nove documentos e sua identidade 0.2.0 foram comparados ao fonte. A evidência atual supera a pendência anterior de sessão MCP externa para leitura documental e política.

**Estado final:** Pipedrive 0.2.0 ativo; diário explicitamente configurado com `diario_dias=0`, `diario_sem_prazo=true`, `recibos_dias=180`, `previas_segundos=900`. Configuração persistida e relida. Duas tabelas próprias novamente com zero linhas; nenhum fixture remanescente. Hashes do schema e da autorização Core iguais antes/depois. Somente a nova opção de retenção foi persistida; o contador auto_increment do diário avançou com os testes e não foi redefinido.

A autorização comercial permaneceu desativada. `pipedrive/status` retorna `operacao_nao_autorizada` para essa dimensão e, simultaneamente, informa a política local correta. Isso é a recusa esperada do estado previamente existente. Nenhuma operação real de CRM, mensagem, e-mail ou publicação foi feita.

## 5. Banco e volta de versão

Mantidas `{prefix}f3_pipedrive_operations` e `{prefix}f3_pipedrive_journal`, schema 1. A troca não executa expurgo. Reativação/reinstalação preservam a política; desativação/desinstalação preservam registros. Backup de banco e salts WordPress é necessário para recuperação dos recibos cifrados; backups privados não foram exportados para os artefatos entregues.

O diário guarda metadados técnicos, caminhos/IDs, classe, status, chaves alteradas e saldo, sem conteúdo de notas/valores pessoais. Recibos privados são separados. Prazo finito usa a data original e autoriza exclusão futura; ampliar prazo ou voltar a zero não recupera exclusões anteriores.

**Reversão para 0.1.0:** o código antigo ignora a nova política e pode apagar diário com mais de 180 dias na próxima prévia/aplicação. Interromper operações antes de voltar e preservar banco; preferir correção adiante. Restaurar arquivos não reverte opções, exclusões ou efeitos externos. Operações incertas exigem reconciliação, nunca reset/reenvio automático.

## 6. Limites e ações restantes

- **Instalação compartilhada e aceite local de retenção: concluídos.** A rejeição automática anterior foi superada após a autorização explícita do dono, sem contorno de controles.
- **Fornecedor real:** não exercitado nesta rodada; não necessário ao teste local de retenção. A autorização comercial continua como encontrada. A homologação recebida da 0.1.0 não é nova prova da 0.2.0.
- **Painel:** renderização PHP e POST com nonce testados; inspeção visual completa em navegador não realizada. Não há captura de tela de homologação.
- **Acompanhantes:** convivência observada nas versões da seção 2; suas integrações de negócio não foram retestadas. A alteração LinkedIn para 0.11.0 foi observada durante o trabalho, sem operação de atualização deste agente.
- **Frota:** publicação raw e instalação nos sites-porta permanecem fora desta execução. URL prevista após publicação, ainda não comprovada: `https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-pipedrive-fator3-0.2.0-instalador.zip`. Conferir SHA-256 antes de instalar.
- **Revisor dos pedidos:** usar esta revisão para avaliar baixa do item 2. A aba central não foi alterada por este agente.
- **Suporte:** mínimos WordPress/PHP comprovados; MySQL 8.0.41 exercitado; multisite não suportado. Outras versões de banco não foram homologadas.

## 7. Credenciais e configuração do dono

Nenhuma credencial nova. Token/conta, concessão e orçamento permanecem no Core, sem exposição de valores. Esta instalação não habilitou consumidores comerciais. Os sites-porta históricos korvena.net.br/korvena.com.br não foram acessados nem alterados.

Retenção: **Ferramentas → Fator3 MCP Pipedrive → Retenção do diário de operações**. Zero significa sem prazo. Pelo MCP, ler `pipedrive/retencao-ler {}` e usar a revisão recebida em `pipedrive/retencao-configurar`, com `diario_dias` e `revisao_esperada`; prazo positivo exige `confirmar_expurgo=true`. Conferir `persisted`, `changed` e política retornada. Perfil somente de leitura não concede escrita; todas as operações continuam administrativas.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador inalterado | `wp-mcp-pipedrive-fator3-0.2.0-instalador.zip` | 48865 | `b7065e4780cbc2166605164e4a822338b76627bef48c5f05a9fb9c3505efbb4a` |
| Fonte inalterado | `wp-mcp-pipedrive-fator3-0.2.0-fonte.zip` | 186893 | `803617faeb4244d6bbf375d3fe11f4652973ee49432c92f5b505f9378f69e7ef` |
| Evidência complementar | `wp-mcp-pipedrive-fator3-0.2.0-homologacao-site-teste.zip` | 26802 | `4115eacd2a4b135174e34be4928be91e520c4300b7a428dfd09c3bc2e1f92d2d` |

Relatório canônico: `wp-mcp-pipedrive-fator3-0.2.0-relatorio.md`, revisão 2. Somente o instalador é instalável. Fonte: raiz `wp-mcp-pipedrive-fator3-0.2.0-fonte/`, com código, build, testes e evidência da implementação; sua cópia interna do relatório não foi reescrita após o fechamento. O complemento contém o cenário de teste compartilhado, instruções e evidências sanitizadas, sem banco, credenciais, cookies ou ZIPs aninhados. Nenhum código de produto foi alterado nesta homologação; a versão permanece 0.2.0.
