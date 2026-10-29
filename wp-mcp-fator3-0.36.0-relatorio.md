# Entrega — Fator3 MCP 0.36.0

Data: 28/10/2026, America/Sao_Paulo. Pacote: `wp-mcp-fator3`. Base direta: 0.35.0. Pedidos MCP 70 (reduzido) e 74.

**Versão corrente: 0.36.0, instalada e ativa no Site-Teste. Situação: com-pendencias.** Os dois defeitos foram reproduzidos na base e corrigidos. O aceite remoto do pedido 74 foi cumprido. O pedido 70 foi validado localmente e com logs reais no Site-Teste; o aceite específico em ctooffice, com host `www` e arquivo `.gz`, permanece com a frota. Nenhuma regressão foi observada nos cenários testados.

O fonte foi fechado uma única vez, depois do relatório interno e das evidências. Sua reconstrução em outra pasta produziu um instalador byte a byte idêntico ao instalado no Site-Teste.

## 1. Bases aceitas e entradas

| Base imutável | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-fator3-0.35.0-instalador.zip | 905542 | `cd6c3afacff83bf38678b9fa2aaf80881be02879b362a9bab250fc56c9969483` |
| wp-mcp-fator3-0.35.0-fonte.zip | 4883759 | `70dd1ba0bac4900334ea843da50e4761f5c5a0f8a630fe5fca225758d151bb2e` |

Entradas novas: “Fator3 MCP(20261028-231454).md”, 5077 bytes, SHA-256 `c2cd91505997112a019bc966868a6a5766a1af1ca94858dea28f3ec1a6d76975`; fonte, instalador e relatório Meta 0.14.0. Os anexos foram examinados localmente. Suas identidades completas estão em `docs/entradas/0360/packages.json` e `evidencias/0360/inputs.json`. As normas comuns 01/02 revisão 5 preservadas da base prevalecem sobre cópias avulsas revisão 4. O plano anterior à implementação está em `docs/PLANO-0360.md`.

O documento de pedidos informa que a 0.35.0 já foi instalada nos 12 sites, com aceites dos itens 69/71/72/73 e da auditoria comercial do Core 323. Esse é um resultado recebido da frota, não uma instalação executada nesta rodada. A 0.35.0 e seus artefatos foram preservados.

## 2. Convivência e encaminhamentos

| Pacote corrente considerado | Instalador: bytes | SHA-256 |
|---|---:|---|
| Core 1.59.0 | 2825862 | `8f3992e89b44f53a59e0e2af314ff8548fe2aadfcc06afe30e395610b1b7c832` |
| Google 0.22.0 | 856534 | `a84754409f89b7b9c7367c1d261c44ef93c2f6039b379c3ec5c6242ec7188ebd` |
| LinkedIn 0.12.0 | 304948 | `19748e788190f371809db469a6de052a645e25f39fad1672606dc776234ec54c` |
| Meta 0.14.0 | 286331 | `43e8947ac0ffaf3da52c62b0515db826e6df266553d64f5561c0d3b87b7eb318` |
| Pipedrive 0.3.0 | 59877 | `30fc784a552a89351900c169fad7300759163fb886b842f45ba807bb0977f657` |

Os cinco estavam ativos no Site-Teste antes da troca MCP e conservaram versão e ativação depois. Core/Google/LinkedIn/Meta originais compõem a bancada funcional; Pipedrive foi observado remotamente, sem concessão ou operação comercial. Seu mínimo PHP não foi reduzido para ativação na bancada PHP 8.3.6. Os hashes acima identificam os pacotes aceitos; o inventário remoto comprova versões/atividade, não uma comparação byte a byte de todos os acompanhantes instalados.

**Impactos novos emitidos: nenhum.** Foram avaliados transporte MCP, autorização, schemas Meta, diagnóstico/redação, registro de mutações e auditoria comercial. As correções são próprias do MCP, e a mudança interna do Meta não exige adaptação de outro mantenedor. Não há ordem nova de troca coordenada. Os níveis/amostras adicionais de logs e a invalidação do cursor antigo estão documentados no contrato instalado. Não foi gerado impacto apenas para avisar versão ou encerrar pedido.

**Tratamento de pedidos e impactos recebidos/anteriores:**

| Referência | Desfecho nesta rodada | Prova e responsável |
|---|---|---|
| Pedidos MCP 70, revisão de 28/10 | Implementado alias sem `www`, Apache/mod_fcgid e amostras mascaradas. Aceite de frota ainda aberto. | MCP: 55 checks novos e leitura real no Site-Teste. Frota: ctooffice com `.gz`. |
| Pedidos MCP 74, de 28/10 | Implementado e aceite do Site-Teste cumprido. | MCP: 25 checks novos; usuário próprio criado/excluído em duas fases e auditoria aplicada. |
| Pedidos MCP 69/71/72/73; LinkedIn 0.12→MCP r1, Core 323 | Recebido o aceite da frota para a 0.35.0; comportamento preservado na 0.36.0. | Documento atualizado de pedidos; 74 checks de regressão 69–73 e 45 de auditoria comercial nesta rodada. Não equivale a conversão real aceita pelo fornecedor. |
| Meta 0.14, Pedido MCP Meta 22 | Token válido sem prefixo EAA é uma mudança do Meta. Schemas recebidos permanecem byte a byte iguais aos da 0.13.0; nenhuma adaptação MCP necessária. | Comparação própria; suíte original Meta repetida, 53/53 com Graph simulado; `meta/health` remoto retorna 0.14.0/ok. |
| Meta 0.13→Core, leitor Ads; exclusão coordenada de mensagens | O relatório Meta 0.14 recebido registra atendimento no Core 1.59 e provas de 41/41 e 20/20, respectivamente. | Informação dos mantenedores Meta/Core; não somada aos testes próprios MCP. Histórico não reemitido como impacto. |

## 3. Mudanças por pedido e evidência

**Pedido 70.** A descoberta prefere o domínio exato e admite somente a remoção de um `www.` inicial. Mantém as guardas de caminho, raiz e permissão; um caminho exato recusado não autoriza fallback. O parser reconhece envelope DreamHost, `mod_fcgid: stderr:` e mensagens Apache nativas. O nível explícito PHP prevalece quando presente. Foram acrescentados `error`, `critical`, `alert`, `emergency`, `info` e `debug`, com mapeamento documentado. Agrupamento, gzip/CRC, conversão Pacific→fuso do site e orçamento permanecem.

`unparsed_samples` oferece até três fragmentos mascarados, cada um limitado a 256 bytes JSON, dentro dos 8 KiB por página. A redação ocorre antes do corte, incluindo credenciais identificáveis, valores conhecidos, URLs, e-mails, IPs, textos entre aspas e trechos SQL/stack. `unparsed_scope:scanned_files` explicita que linhas sem data reconhecível não podem ser atribuídas à janela dos grupos. A máscara não é garantia de classificação de todo texto pessoal arbitrário. O cursor passa a `hosting-error-log/2`; clientes com cursor anterior reiniciam a consulta.

**Pedido 74.** A operação e o carregador administrativo verificam `wp_delete_user`, carregando `wp-admin/includes/user.php` quando necessário. Após exclusão nativa, limpa-se o cache e relê-se o estado. `applied/changed/persisted:true` exige remoção confirmada; a auditoria dessa operação preserva os indicadores. Falhas têm diagnóstico real sanitizado e limitado, sem stack ou SQL, com códigos específicos. Falha de hook pode deixar efeitos parciais: `applied/persisted:null`, sem repetição automática; a confirmação concluída reproduz o recibo. Preservam-se autorização, CAS, alvo, backup e duas fases.

`delete_content:true` mantém a política nativa do WordPress: posts podem ir à lixeira. Em multisite, a semântica nativa é remover a participação no site; essa modalidade não foi homologada nesta rodada. O tratamento de exceções das demais abilities não foi ampliado.

Comparação com o instalador 0.35.0: oito arquivos alterados, nenhum acrescentado/removido. São Helpers, Users, Audit, DataSafety, HostingErrorLog, arquivo principal e dois documentos compilados. A redação antiga de grupos foi extraída sem alteração de comportamento; o mascaramento mais conservador é usado nos novos fragmentos diagnósticos. Identidades públicas, slug, basename, namespaces e mínimos foram mantidos.

**Testes próprios: 1017 verificações funcionais aprovadas em 21 resultados, zero falhas no fechamento.** Reexecuções não foram somadas. São asserções de ensaios, não 1017 integrações comerciais independentes.

| Ensaios | Verificações |
|---|---:|
| Novos logs / exclusão de usuários | 55 / 25 |
| Unidades de redação, política e contextos 0.31–0.33 | 479 |
| Transporte HTTP de redação, política e pedido 68 | 79 |
| Permissões e correio com fixtures | 40 |
| OAuth/CIMD | 48 |
| Administração nativa e negativos 0.30 | 44 |
| Regressões 69–73 | 74 |
| Auditoria comercial LinkedIn | 45 |
| Suíte original Meta 0.14 | 53 |
| Instalação limpa mínima | 13 |
| Upgrade direto 0.35→0.36 | 24 |
| Documentação completa pelo HTTP MCP local | 38 |

Separadamente: cinco reproduções aprovadas dos defeitos na base; 15 checks de pacote, incluindo lint dos 456 arquivos PHP, inventário exato, reconstrução e rejeição de adulterações. Remotamente: 20 verificações de aceitação e 35 documentos lidos em 38 páginas, conferidos integralmente contra o ZIP final. Não somar os 456 lints novamente aos 15 checks de pacote.

Durante a preparação, duas expectativas de fixtures foram corrigidas: posts vão à lixeira pela política nativa, e um contador entre processos exigia invalidar o cache da bancada. A execução final passou. Uma invocação do lint sem a variável do runtime foi refeita com PHP 8.3.6 configurado. Ajustes finais de espaçamento documental foram seguidos por leitura HTTP integral, readback mínimo e check do ZIP final; o código funcional não mudou depois da regressão.

## 4. Instalação, documentação e prontidão

**Bancada:** WordPress 7.1.3/PHP 8.3.6/MySQL 8.0.46, com acompanhantes originais. Instalação limpa WordPress 7.1.2/PHP 8.3.6 sem acompanhantes, ativação em processo separado, cron, capacidades, saúde e 467 arquivos iguais ao ZIP. Upgrade direto da 0.35.0 verificou workers novos, OPcache, preservação de senha de aplicativo, OAuth/perfil/expiração/renovação, opções falsas/vazias, backups, recibos concluídos/incertos e confirmação pendente. A prévia de rollback verificou a pré-imagem. Esses cenários comprovam os mínimos MCP declarados, não todos os runtimes possíveis.

**Site-Teste:** `https://fator3-teste-mcp-1.dreamhosters.com/`, WordPress 7.1.4/PHP 8.3.36. Apenas o MCP foi trocado, da 0.35.0 para a 0.36.0. Operação `f880cade13100fa7555497a207321b0a`, `applied:true`, SHA igual ao instalador final. Sondas `/` e `/wp-json/` retornaram 200 antes/depois; requisição PHP independente observou a nova versão. Saúde final `healthy:true`, cron ativo consistente e recuperação sem operação não resolvida. Essas sondas têm origem interna e não homologam CDN/acesso externo ou prontidão comercial.

Pedido 74: criado o usuário sintético 7, sem conteúdo; prévia sem efeito e confirmação aplicada/persistida. `users/get` posterior retornou “User not found”. `audit/list` confirmou uma operação aplicada, `d5a27be7bd66ad584c9ff1b6`, sem replay. O usuário foi removido, sem SQL. Backup privado do usuário `d8c6285aff4a0d6cd754d1f8` preservado.

Pedido 70: consulta real das 24 h terminadas às 20:39:39 −03 examinou dois arquivos, 498 linhas e 211389 bytes. Encontrou 60 grupos na janela, zero linhas não reconhecidas; a primeira página devolveu nove grupos, incluindo warning/error, em −03. Não se exportou o log bruto nem se paginaram os 60 grupos para o fonte. Nenhum `.gz` foi examinado nessa janela. De 20:36:00 a 20:45:33 −03, a consulta de fatal retornou zero grupos; essa observação curta não prova ausência de falhas futuras ou de outros níveis.

**Documentação instalada:** 35 documentos, 38 páginas, 242375 bytes lidos pelo MCP remoto. Conteúdo, tamanho e SHA-256 de cada um coincidem com o ZIP final; ver `evidencias/0360/remote-documents.json`. Incluem configuração, uso, contratos, autorização, recuperação, exemplos e `release-0360`. O guia não depende de acesso ao relatório externo.

Estado final: nove plugins ativos; acompanhantes com as mesmas versões/ativação. Usuário descartável e ZIP de transporte removidos. Pré-imagens e auditoria preservadas. Nenhuma concessão comercial, conexão de fornecedor, cron alheio ou configuração de negócio foi alterada intencionalmente pelo teste MCP.

## 5. Banco, reversão e preservação

Nenhuma tabela, option ou migração nova do MCP. A auditoria existente recebe os indicadores da exclusão; a operação nativa modifica usuário/conteúdo conforme a intenção confirmada. Não houve SQL de contorno no Site-Teste.

Pré-imagem da atualização: `f766e41e7aa170828389d503`. `plugins/rollback` em dry-run confirmou `rollback_ready:true`, `preimage_verified:true`, `applied:false`. A pré-imagem anterior `c8dcabcdee9f9077e58a58a1` foi preservada. Rollback de arquivos restaura as limitações da 0.35.0; não recria usuário, posts ou efeitos externos de hooks. Recuperação de dados requer examinar o backup privado e o estado real. Não repetir exclusão incerta com nova chave para forçar execução.

## 6. Pendências e limites

- **Frota — MCP 70:** depois da troca autorizada em ctooffice, ler últimas 24 h, confirmar agrupamento dos avisos PHP no fuso −03 e uma janela que contenha `.gz`. Alias/gzip passaram com fixtures locais; o Site-Teste não tem host `www` e não apresentou gzip nessa janela. A implementação está entregue, mas esse aceite específico não foi declarado concluído.
- **Operador/fornecedores:** aceites reais de conversões comerciais Google/LinkedIn, primeiro Enhanced Leads, contas/ações/consentimentos e demais tarefas dos acompanhantes permanecem com seus responsáveis. Graph e envios dos ensaios foram simulados; a consulta remota Meta usada aqui foi somente de saúde.
- **B22/CIMD:** o encerramento histórico de 21/10/2026, registrado na 0.25.0 r3, permanece vigente. Não foi reaberto como pendência de código desta versão. As 48 regressões locais e a conexão existente passaram; consentimento externo novo do zero não foi repetido.
- **Fora da matriz:** multisite, Redis/Memcached, SMTP/IMAP ou fornecedores reais, outros runtimes, observação prolongada, navegador visual e CDN externo. A ausência de regressão observada se limita às provas descritas.

Não há correção de código conhecida pendente no escopo MCP testado. Não foi instalada a 0.36.0 nos demais sites nem encerrado trabalho pertencente a outro mantenedor.

## 7. Credenciais e operação

A atualização não exige segredo, escopo ou concessão novos. Preserva as permissões WordPress e do canal. A senha do usuário descartável foi gerada pelo WordPress; nenhum valor secreto foi publicado. Diagnósticos/evidências entregues não incluem tokens de confirmação, credenciais reais, cookies, bancos, logs brutos ou helpers privados. Fixtures contêm valores sintéticos identificados.

Não houve publicação GitHub/feed, mensagem a terceiros, envio comercial real, rota de PHP arbitrário ou alteração de pacote alheio. O roteiro de reprodução está em `tools/release0360/README.md`; o fonte é material de desenvolvimento, não o ZIP instalável.

## 8. Artefatos finais e estado de entrega

| Artefato | Nome exato | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador WordPress | wp-mcp-fator3-0.36.0-instalador.zip | 910233 | `97648853e16d7c7fca811c6be22323244c5f2ebc3e296c22564ce7b2739cb98b` |
| Fonte | wp-mcp-fator3-0.36.0-fonte.zip | 4976576 | `6dab0eeaaab2bb971a17e93bfed150e1af557dae494c1c8940d53bd0ca5d48f6` |

Relatório externo: `wp-mcp-fator3-0.36.0-relatorio.md`. Instalador com raiz única `wp-mcp-fator3/`, 467 arquivos, 456 PHP e 56 índices de silêncio; sem testes, ferramentas, fontes Markdown, ZIPs aninhados ou resíduos de bancada. O fonte tem raiz `wp-mcp-fator3-0.36.0-fonte/`, runtime, documentação editável, build, testes, evidências sanitizadas e relatório interno identificado como anterior ao fechamento.

**Reconstrução final aprovada:** o fonte fechado foi extraído em outra pasta; seu build produziu exatamente os mesmos 910233 bytes e SHA-256 do instalador instalado no Site-Teste. O fonte não foi reaberto para incorporar o próprio hash.

O instalador foi congelado antes da instalação remota e do empacotamento do fonte. Nenhuma mudança posterior foi feita em seus bytes. Instalar exclusivamente o ZIP instalador e conferir seu SHA-256; publicação e implantação na frota ficam com o responsável autorizado.
