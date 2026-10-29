# Entrega — Fator3 MCP 0.37.0

Data: 29/10/2026, America/Sao_Paulo. Pacote: wp-mcp-fator3. Base direta: 0.36.0. Pedido MCP 75.

**Versão corrente: 0.37.0, instalada e ativa no Site-Teste. Situação: com-pendencias.** A leitura de logs agora decodifica os escapes UTF-8 válidos do Apache antes de mascarar, agrupar e filtrar. A busca real por desativação passou de zero a 24 grupos na mesma janela do Site-Teste. Nenhuma regressão foi observada nos cenários testados. O aceite específico de ctooffice permanece com a frota.

Foi identificada também uma limitação preexistente na projeção de metadados de credenciais do Core 1.60.0 pelo MCP. O encaminhamento separado propõe correção no contrato Core; a regra de proteção de segredos MCP foi preservada.

## 1. Bases aceitas e entradas

| Base imutável | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-fator3-0.36.0-instalador.zip | 910233 | `97648853e16d7c7fca811c6be22323244c5f2ebc3e296c22564ce7b2739cb98b` |
| wp-mcp-fator3-0.36.0-fonte.zip | 4976576 | `6dab0eeaaab2bb971a17e93bfed150e1af557dae494c1c8940d53bd0ca5d48f6` |

Entrada funcional: Fator3 MCP(20261029-030611).md, 2892 bytes/SHA-256 `39393c3bfc35b24cf428c4465870c2b18a3aee4b5cbb72d991009323e75cbcdf`. Novos anexos Core 1.60.0: fonte 5106586 bytes/SHA-256 `afdac358331e3894480b59fc8b57cc411909d3c7b399a6f998c996b35e7d25fe`; instalador na tabela seguinte; relatório 20309 bytes/SHA-256 `311dbc38a929e52c873a73e75c0cb7587fa8799f25b54c279809292ed8fc5fc7`. Os anexos foram examinados localmente e preservados sem alteração. Identidades em docs/entradas/0370/packages.json e evidencias/0370/inputs.json.

Normas comuns 01/02 revisão 5 preservadas da base prevalecem sobre cópias avulsas r4. Plano anterior ao código em docs/PLANO-0370.md. Minor incrementado por novo ciclo; não houve correção posterior a uma entrega 0.37.0 já publicada. Identidades públicas e mínimos permanecem.

O pedido recebido informa a 0.36.0 nos 12 sites, commit e55b3a9, com aceite dos pedidos 70 e 74: ctooffice com pasta sem www, três gzip e fuso −03; korvena com mod_fcgid; exclusão de usuário no Site-Teste. Esse é o aceite recebido da frota, não uma instalação repetida nesta rodada. Esses itens deixam de constar como pendências.

## 2. Convivência e encaminhamentos

| Pacote recebido/reutilizado | Bytes do instalador | SHA-256 |
|---|---:|---|
| Core 1.60.0 | 2842430 | `1dc4e94305ea55394024d6527bc06b46209f0ae51a55f734853763bcb232e27c` |
| Google 0.22.0 | 856534 | `a84754409f89b7b9c7367c1d261c44ef93c2f6039b379c3ec5c6242ec7188ebd` |
| LinkedIn 0.12.0 | 304948 | `19748e788190f371809db469a6de052a645e25f39fad1672606dc776234ec54c` |
| Meta 0.14.0 | 286331 | `43e8947ac0ffaf3da52c62b0515db826e6df266553d64f5561c0d3b87b7eb318` |
| Pipedrive 0.3.0 | 59877 | `30fc784a552a89351900c169fad7300759163fb886b842f45ba807bb0977f657` |

Core/Google/LinkedIn 0.12/Meta originais compõem a bancada. Pipedrive 0.3 foi observado ativo remotamente; não se reduziu seu mínimo PHP para ativá-lo na bancada 8.3.6. Comparação Core 1.59→1.60: 49 arquivos alterados, seis acrescentados e nenhum removido. Foram examinadas as fronteiras pertinentes de configuração, credenciais, permissões, correio, redação, diagnóstico e auditoria; isso não equivale a auditar todas as funções novas do Core.

**Atualização concorrente considerada:** o LinkedIn passou de 0.12.0 para 0.13.0 por outra sessão antes da instalação MCP. A versão, o registro público e a documentação instalada foram conferidos. RELEASE-0.13.0.md: 2360 bytes/SHA-256 `2c36009e073a4ea39e298a97b7b999b7f8d6909ceea0595f89b4143deb36f18a`. O documento informa avisos de formato, 93 operações, schemas de entrada preservados e contratos comerciais intactos. Nenhum fonte/instalador 0.13 foi recebido nesta rodada; não se atribuem a ele os ensaios locais da 0.12. Esse limite está registrado em evidencias/0370/linkedin0130-installed-release.json.

Antes da troca MCP e no fechamento: Core 1.60, Google 0.22, LinkedIn 0.13, Meta 0.14 e Pipedrive 0.3, todos ativos. Provedores auxiliares de QA Pipedrive 0.4 de outras sessões apareceram no registro; não foram invocados, alterados nem confundidos com a versão instalada do plugin. O inventário remoto prova versão/atividade, não identidade byte a byte de todos os acompanhantes. Apenas o MCP foi instalado por esta rodada.

**Novo encaminhamento:** wp-mcp-fator3-0.37.0-impacto-base-site-core-fator3.md, revisão 1, acao-necessaria, aberto; relacionado ao Core 334, sem criar número de pedido. O documento foi iniciado ao detectar a fronteira, antes de propor qualquer alteração nela. O Core retorna a lista de diagnóstico sob credenciais; fator3-redaction/1 mascara o contêiner inteiro, incluindo ajuda, rótulos e estado. A leitura genérica de uma opção secreta também mascara sua revisão; o item nativo de credenciais não inclui a revisão exigida por credenciais-verificar. O caminho consultado não fornece os metadados e CAS necessários à preparação pública completa.

Reproduzido em MCP 0.36 e 0.37 com Core 1.60: problema anterior ao pedido 75, sem vazamento de segredo. Proposta ao mantenedor Core: projeção administrativa sob contêiner neutro, nomes como valores e revisão opaca atual, sem segredos, preservando capacidades e CAS. A correção será do Core; a validação do transporte será conjunta. A tela própria do Core é a alternativa operacional enquanto se alinha o contrato. O documento foi preparado para o dono, sem envio externo.

| Pedido/impacto recebido ou anterior | Tratamento nesta rodada | Evidência e responsável |
|---|---|---|
| MCP 70/74, pedido de 29/10 | Aceite recebido; encerrados na lista da frota. | Documento recebido e regressões locais de 55/25 verificações. Não reemitidos como impactos. |
| MCP 69/71/72/73; LinkedIn→MCP r1; Core 323 | Aceites anteriores preservados; sem nova exigência de troca. | Histórico da base; 33 verificações adversariais e 45 de auditoria comercial nesta rodada. Não significam envio comercial real. |
| Core 1.60, pedidos 322/330–334 | Novidades pertinentes consideradas; novo achado 334 encaminhado acima. Reconcessão Meta Ads/330 continua sob Core/Meta/frota. | Relatório e código Core recebidos; teste próprio de prévia e autorização. Provas relatadas por outro mantenedor não são somadas às próprias. |
| LinkedIn 0.13, pedido 15 | Notas instaladas consideradas, sem adaptação exigida do transporte descrito. | Leitura documental remota; fonte e fluxo comercial 0.13 não avaliados localmente. |

Nenhum impacto novo foi emitido para os demais acompanhantes. Não foram alterados seus códigos ou documentos, a regra comum, o repositório público ou o feed de atualização.

## 3. Mudanças por pedido e evidência

**MCP 75:** o parser converte cada sequência contígua de bytes Apache \xNN somente quando ela inteira é UTF-8 válido. A conversão precede identificação do nível PHP, máscara, extração de arquivo/linha, normalização, agrupamento e filtro. Mensagens nativas e escapadas equivalentes passam a integrar o mesmo grupo. Amostras não interpretadas também são decodificadas antes de mascarar e cortar.

São preservados trechos inválidos, truncados, overlong, surrogates, valores fora do Unicode, barras literais duplicadas e controles ASCII NUL–0x1F/DEL. Hex maiúsculo é aceito. Uma única passagem; não decodifica escapes genéricos, octais, URL ou Unicode JSON. Não normaliza NFC/NFD nem altera a sensibilidade literal/caixa do filtro. Não modifica o arquivo de log, datas, caminhos físicos, parâmetros de autorização ou filtro enviado pelo cliente.

Como grupos e identificadores podem mudar, o cursor passa a hosting-error-log/3; cursores /1 e /2 são recusados, exigindo reinício sem cursor. Permanecem schemas, capacidades, perfil, política de arquivos, domínio exato/alias sem www, gzip/CRC, fuso dos arquivos e do site. Mantidos os limites: 8 KiB/página, 31 dias, 128 arquivos, 32 MiB expandidos, 16 MiB comprimidos por arquivo, cinco segundos e 5000 grupos. Falha não é apresentada como contagem completa.

Comparação instalador 0.36→0.37: quatro arquivos alterados — HostingErrorLog.php, arquivo principal e dois guias compilados — sem acréscimo/remoção de runtime. A única mudança funcional está na leitura de logs. Slug, basename, provider, namespaces, Update URI e mínimos MCP WordPress 7.1.2/PHP 8.3.6 preservados.

**969 verificações funcionais aprovadas em 19 resultados, zero falhas no fechamento.** Reexecuções não foram somadas; são asserções de ensaios, não integrações comerciais independentes.

| Ensaio | Verificações |
|---|---:|
| Novo pedido 75: parser e transporte HTTP | 75 |
| Logs 70 / usuários 74 | 55 / 25 |
| Convivência pertinente Core 1.60 | 14 |
| Unidades de redação, política e contexto | 479 |
| HTTP redação, política e pedido 68 | 79 |
| Permissões e correio com fixtures | 40 |
| OAuth/CIMD | 48 |
| Adversariais 69–73 | 33 |
| Auditoria comercial LinkedIn com fornecedor sintético | 45 |
| Instalação mínima limpa | 13 |
| Upgrade 0.36→0.37 | 24 |
| Documentação HTTP local | 39 |

Separadamente: três reproduções do defeito na base; cinco reproduções da limitação Core em cada versão (dez no total); 15 verificações de pacote, incluindo 456 lints PHP. Não contar a reprodução da limitação como sucesso do fluxo de credenciais, nem somar os lints novamente aos 15 gates. A prévia Core usa revisão obtida nativamente apenas na fixture: comprova avisos sem persistência, máscara/paridade e permissão, não preparação completa por MCP.

Casos específicos: UTF-8 de dois/três/quatro bytes, nativo/misto, inválidos preservados, segredo escapado mascarado, caminhos, mod_fcgid/Apache/PHP, gzip, agrupamento de três ocorrências, first/last em −03, filtro com acento e 40 grupos em 20 páginas sem repetição e abaixo de 8 KiB. O perfil read permanece recusado nessa leitura restrita.

Na preparação, a fixture de hex maiúsculo tinha uma expectativa textual incorreta, corrigida antes do fechamento. A expectativa inicial de metadados Core levou ao achado real acima e foi separada da validação funcional. Um laboratório inicial carecia de wp-config e foi preparado corretamente antes de produzir prova. A nota documental final sobre Core foi seguida por mínimo limpo, upgrade, leitura documental integral e pacote sobre o SHA final; não houve mudança funcional depois das regressões. Roteiro: tools/release0370/README.md.

## 4. Instalação, documentação e prontidão

**Local:** WordPress 7.1.3/PHP 8.3.6/MySQL 8.0.46, acompanhantes originais; mínimo limpo WordPress 7.1.2/PHP 8.3.6, só MCP, ativação e leitura em processos separados. Upgrade direto preservou OAuth/perfil/expiração/renovação, senha de aplicativo, opções falsas/vazias, backups, recibos concluídos/incertos e confirmação pendente. Novos workers e todos os 467 arquivos foram conferidos contra o ZIP final. Isso comprova os cenários e mínimos declarados, não todos os runtimes possíveis.

**Site-Teste:** https://fator3-teste-mcp-1.dreamhosters.com/, WordPress 7.1.4/PHP 8.3.36. Operação 138e7a295113390da2419031a2470fb5: 0.36.0→0.37.0, applied, ativo, SHA igual ao final. Sondas / e /wp-json/ retornaram 200 antes/depois com cache bypass verificado; requisição PHP independente observou o plugin ativo. O modo foi silent_reactivation, sem declarar ciclo completo de hook de ativação ou prontidão comercial. Sondas internas não homologam CDN/acesso externo.

**Prova real do pedido 75**, sem fabricar linhas nem ler log bruto: janela 28/10 00:00:00 até 29/10 00:00:00 −03, dois arquivos, zero gzip, 576 linhas e 244062 bytes examinados na leitura final. Antes, desativa encontrava 24 grupos com escapes; desativação encontrava zero. Depois, desativação encontra 24 grupos; as dez mensagens da primeira página têm o acento correto e não contêm \xNN. Zero linhas não interpretadas. O total é da janela completa limitada pela API; apenas a primeira página foi inspecionada, não se exportaram os 24 grupos. A prova de ctooffice de 24–25/10 é distinta e permanece com a frota.

**Documentação MCP:** 36 documentos, 39 páginas, 248246 bytes; conteúdo, ordem de paginação, tamanho e SHA-256 conferidos integralmente contra o instalador. Inclui release-0370, contratos, configuração, uso, recuperação e exemplos. Evidência em remote-documents.json.

Estado final observado às 00:42:17 −03 de 29/10: healthy:true, cron ativo consistente, recuperação com zero operações não resolvidas, auditoria da requisição sem falha. O histórico cron permanece incompleto por overflow antigo, com 22 erros não rastreados já presentes antes; isso não é uma afirmação de ausência de falhas de todos os jobs. Nove plugins ativos; versões dos acompanhantes iguais às imediatamente anteriores à instalação MCP. Meta health retorna 0.14.0/sucesso. ZIP temporário próprio removido, backups preservados. Recursos QA de outras sessões não foram removidos.

A revisão automática de segurança rejeitou a repetição pós-instalação de f3base/credenciais-ler por envolver uma credencial privada identificada por nome. Não houve repetição nem rota indireta. Essa prova remota 0.37 não foi feita; o achado é sustentado por ensaios locais sintéticos nas duas versões e pela observação remota anterior na 0.36. As verificações restantes foram concluídas.

## 5. Banco, reversão e preservação

Nenhuma tabela, option, migração, credencial, concessão ou agenda nova. A leitura é somente de diagnóstico; as operações normais de instalação/transferência geram seus recibos e auditoria existentes. Não houve SQL de contorno nem alteração intencional de configurações de negócio ou cron alheio.

Pré-imagem MCP 0.36: 11f85f053698a7865a824659. Dry-run de rollback: rollback_ready:true, preimage_verified:true, applied:false. Pré-imagens anteriores f766e41e7aa170828389d503 e c8dcabcdee9f9077e58a58a1 preservadas. O rollback de arquivos restaura apresentação hexadecimal e semântica anterior dos grupos; reiniciar a paginação de logs. Não reverte operações de negócio ou efeitos externos já executados. Não houve rollback real nesta rodada.

## 6. Pendências e limites

- **Frota — MCP 75:** instalar o ZIP verificado nos demais sites no escopo próprio; em ctooffice repetir since 2026-10-24T00:00:00-03:00, until 2026-10-26T00:00:00-03:00, text desativação. Confirmar a frase legível e o grupo. O aceite 70/74 já recebido não é reaberto.
- **Mantenedor Core, com validação MCP:** publicar projeção neutra de metadados e revisão opaca, testar recusa de permissão/CAS e ausência de segredos. Novo encaminhamento anexo, relacionado ao Core 334. Fluxo completo público de credenciais ainda limitado.
- **Acompanhantes/operadores:** fonte e regressão local LinkedIn 0.13 não avaliados; só inventário, registro e notas instaladas. Aceites com tokens reais, conversões, Enhanced Leads, contas/ações/consentimentos e reconcessão Meta Ads permanecem com seus responsáveis. Fornecedores e correio dos testes foram simulados/interceptados.
- **B22/CIMD:** encerramento histórico de 21/10/2026, registrado na 0.25.0 r3, preservado. 48 regressões locais e conexão existente passaram; consentimento externo novo do zero não foi repetido. Não é pendência de código reaberta.
- **Fora da matriz:** multisite, Redis/Memcached, navegador visual, outros runtimes, SMTP/IMAP e fornecedores reais, observação prolongada e CDN externo. A ausência de regressão observada limita-se às provas descritas.

Não há correção MCP conhecida pendente no escopo testado do pedido 75. A 0.37.0 não foi instalada nos outros sites nesta rodada, e nenhum trabalho de outro mantenedor foi declarado concluído.

## 7. Credenciais e operação

A atualização não exige segredo ou concessão novos e conserva autorização WordPress/perfil. Evidências públicas não incluem valores reais de credenciais, cookies, bancos, logs brutos ou helpers privados. Valores sintéticos das fixtures são identificados como tais. Não inferir uma revisão de configuração nem enfraquecer a redação para contornar o achado Core.

Não houve publicação GitHub/feed, mensagem a terceiros, envio comercial real, rota de PHP arbitrário, rota de frota, SQL em uma fase ou mudança em pacote alheio. A preparação do impacto não autoriza seu envio. O fonte é material de desenvolvimento; instalar exclusivamente o ZIP instalador.

## 8. Artefatos finais e estado de entrega

| Artefato | Nome exato | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador WordPress | wp-mcp-fator3-0.37.0-instalador.zip | 912702 | `cbece53fc479d9fe3963b111e49e789d92609c5462102877244dcaebcf7cf3ec` |
| Fonte | wp-mcp-fator3-0.37.0-fonte.zip | 5074415 | `e2654b93a9bababb283cb870b4f5f94ac17ad9a188ea23bb2cd3a8b77f7bb49c` |

Relatório externo: wp-mcp-fator3-0.37.0-relatorio.md. Novo encaminhamento: wp-mcp-fator3-0.37.0-impacto-base-site-core-fator3.md. Instalador com raiz única wp-mcp-fator3/, 467 arquivos, 456 PHP e 56 índices de silêncio; sem testes, ferramentas, fontes Markdown, ZIPs internos ou resíduos de bancada. Fonte com raiz wp-mcp-fator3-0.37.0-fonte/, runtime, documentação editável, build, testes, evidências sanitizadas e relatório interno identificado como anterior ao fechamento.

**Reconstrução final aprovada:** o ZIP fonte fechado foi extraído em outra pasta; documentação sincronizada e build executado nessa cópia produziram exatamente os mesmos 912702 bytes e SHA-256 do instalador instalado no Site-Teste. O fonte não foi reaberto para incorporar seu próprio hash.

O instalador foi congelado antes da instalação remota. Nenhum byte foi alterado depois. O fonte é empacotado uma única vez após evidências e relatório interno, sem tentar incorporar seu próprio hash. Publicação e implantação na frota pertencem ao responsável autorizado.
