# Entrega — Fator3 MCP Google 0.12.0

Revisão: 1 · Data/hora: 2026-10-19T00:56:31-03:00 · Rodada: implementação
Slug/basename: `wp-mcp-google-fator3/wp-mcp-google-fator3.php` · Build: `20261019-012-d2499a5f`
Status: **apta-no-escopo-testado**. Instalação, atualização e novos contratos aprovados no recorte descrito; APIs Google comerciais e distribuição na frota continuam pendentes.

Normas aplicadas: instruções aos agentes e padrão de desenvolvimento/entrega, ambos revisão 4 de 16/10/2026, relidos integralmente. Escopo: plano 0.12.0 r2, atualizado para r4; aba `Fator3 MCP Google(2).md`, situação de 18/10; Core 1.38.0 entregue. As duas consequências técnicas foram documentadas antes da implementação e atualizadas na entrega.

## 1. De onde esta versão entra

Aceita **WordPress limpo** e atualização direta **Google 0.11.0 → 0.12.0**, sem desinstalar ou instalar versão intermediária. Base: fonte liberado 0.11.0, SHA-256 `c142e10c544a73008bf4c132b85b36cd921fd6313aff5491e99dce61ba12c37e`; instalador base `d181deaeee8ef365ac4d6a08884d9fa3d3a3164b21f0538d8ed5d56722536bf9`. A base permanece imutável.

Mínimos efetivamente reensaiados: **WordPress 7.1.2/PHP 8.3.6**, preservando o Pedido MCP Google 25. Laboratório single-site com MySQL 8.0.46 e lighttpd 1.4.74/PHP-FPM. O core WordPress veio de arquivo local recuperado sem wp-config, wp-content ou banco anterior; não é apresentado como download oficial novo. A árvore local de ferramentas foi reidentificada por hash nesta rodada, com versões dos binários medidas; o atestado de runtime da 0.11.0 não foi reutilizado. Detalhes em `evidence/012/inputs-portable.json` e `runtime-origin.json`.

## 2. Convivência e encaminhamentos

Matriz principal: Core **1.38.0**, MCP **0.24.0**, Meta/LinkedIn **0.3.0**. Também foi exercitado Core **1.35.0 → 1.38.0**, com Google antes/depois do Core, e Google isolado sem acompanhantes. Os quatro schemas de conversões da 1.38.0 são byte a byte iguais aos da 1.36.0. Essa comparação não é execução funcional própria da combinação 0.12.0/Core 1.36.0.

Não há dependência numérica/artificial de instalação. Ausência do SDK adicional afeta somente o contexto de conversões. Configuração Google 4.0.0, catálogo 3.0.0, execução/storage/manutenção 2.0.0, SDKs existentes e identidades públicas foram preservados. O contrato administrativo Core 8.3.0 não é importado pelo novo leitor.

| Destinatário | Examinado | Classificação / situação | Referência | Documento vigente |
|---|---|---|---|---|
| Core | 1.38.0; schemas 1.36.0; transição 1.35.0 | validacao-coordenada / resolvido no aceite Google | P12-01 a P12-03; vínculo Core 222 | `wp-mcp-google-fator3-0.12.0-impacto-base-site-core-fator3.md` r4 |
| Implantador | relatório 2.9.0; não executado | validacao-coordenada / alinhado; confirmação do destinatário pendente | Pedido MCP Google 26 / IMP-GOOGLE-01 | `wp-mcp-google-fator3-0.12.0-impacto-implantador-base.md` r2 |

MCP e sociais tiveram regressões pertinentes verificadas, sem nova alteração solicitada em seus contratos; não foram emitidos impactos só para anunciar versão. Nenhum pacote destinatário foi editado/publicado nem foram enviadas mensagens a terceiros.

## 3. Mudanças e evidência

| Pedido / item | Problema e comportamento entregue | Estado e prova |
|---|---|---|
| **Pedido MCP Google 26 / P12-06** | WordPress relê false como string vazia. `Configuration::effective()` normaliza opções declaradas booleanas; `effective_value` sempre true/false. `persisted_value` conserva a representação do WordPress. Campos textuais/null não são convertidos. | implementado, validado-localmente, validado-wordpress: 67 asserções por execução da suíte `booleans012`, na instalação limpa, upgrade Google-primeiro e instalação MCP. Escrita pública com revisão; leituras em requisições novas, conexões padrão/nomeada; cinco campos booleanos também no leitor administrativo com canal fechado. |
| **P12-01** | Novo consumidor opcional `CoreConversions`, contrato `site-conversion-purposes/1.0.0`, provider exato, métodos e schemas empacotados. Rejeita estrutura/tipos/finalidades/revisões inválidos; preserva null/vazio, falhas e procedência. Não lê options privadas nem arquivos do Core. | implementado, validado-localmente, validado-wordpress: 41 verificações contratuais e produtor Core real. |
| **P12-02** | Nova leitura `google/conversion-context`, sem credencial Google. Respeita canal, perfil MCP, manage_options e capacidade adicional; callback direto também protegido. `connection_id` não vai ao produtor. | validado-wordpress: gates de administrador/editor/anônimo, capacidade adicional, canal fechado, perfil MCP negado; sucesso e conflito reais no Site-Teste. |
| **P12-03** | `gtm/diagnostico` acrescenta `core_conversion_context`, separado do contexto/catálogo antigo. Compara revisões antes/depois da leitura GTM existente; conflito só no bloco adicional preserva o diagnóstico antigo válido. | validado-wordpress em laboratório com Core real e Google simulado: resultado coerente, mutação de material durante GTM, nenhuma repetição do GET e ausência opcional. |
| **P12-04** | Catálogo derivado do registro: **283 operações, 110 leituras/173 escritas**; 34 definições de configuração. Ajuda instalada inclui manual de conversões e três schemas PHP. | geração conferida; 19 documentos lidos integralmente pelo MCP remoto em 60 páginas, SHA-256 igual ao pacote local validado. |
| **P12-05 / regressão Pedido 25** | Clean, upgrade da base, isolamento, instalação MCP, preservação e rollback; mínimos e identidade mantidos. | cinco laboratórios concluídos; 154 arquivos runtime, 150 PHP com sintaxe válida. |

Contato mantém `generate_lead`; material usa `download_material`, rótulo Ads próprio e ID LinkedIn próprio. Material vazio não herda contato. `enabled:true/configured:false` é estado válido. `configured:true` só descreve identificadores locais, nunca acesso ou entrega; `runtime_verified` e `remote_access_verified` permanecem false.

Não há criação automática de key events, ações Ads, tags/publicações GTM, campanhas, grants, bindings ou jobs. O adaptador puro não grava nem usa rede. A operação é leitura local, efeito remoto none; auditoria sanitizada conserva a política existente, inclusive em falhas e quando audit_local_reads está ligado. Não há reparo silencioso de configuração/agenda/storage.

O Pedido 26 está atendido pelo pacote; a confirmação do Implantador e o encerramento na lista central/frota pertencem aos respectivos responsáveis. Não foi criado Pedido 27.

## 4. Instalação e prova da troca

A candidata aprovada foi copiada sem reconstrução e instalada no Site-Teste por `plugins/upload-base64`, com `expected_slug:wp-mcp-google-fator3`, SHA-256 da seção 8, overwrite/activate true e `probe_timeout_seconds:30`. Foi a única troca remota desta rodada. A base 0.11.0 e o hash do arquivo principal foram relidos imediatamente antes. Publicação Git/raw e distribuição na frota **não foram realizadas**; a frota deverá conferir os bytes servidos pela URL versionada antes de usar `plugins/upload`.

Operação: `2d3edabaa89bb57e192c1d25`; diário do pacote: `73e6d5506de1c9ac89281f0eae079193`; backup de arquivos: `38ea419cb8e4f6cfd8e285af`. Reativação silenciosa em PHP novo confirmada. Home e REST responderam 200 nas sondas internas antes/depois; essas sondas não são homologação de navegador externo ou APIs comerciais.

| ID | Ambiente/cenário | Resultado | Evidência no fonte |
|---|---|---|---|
| V12-01 | Schemas, fixtures adversárias e ausência/método ausente | 41 verificações, zero falhas | `evidence/012/contracts-*.json` |
| V12-02 | WordPress limpo com acompanhantes | 311 asserções, zero falhas | `evidence/012/clean/` |
| V12-03 | Upgrade Google primeiro, Core antigo→atual | 164 asserções, zero falhas | `evidence/012/upgrade-google-first/` |
| V12-04 | Upgrade Core primeiro, Google 0.11→0.12 | 46 asserções, zero falhas | `evidence/012/upgrade-core-first/` |
| V12-05 | Instalação isolada, sem Core/MCP | 21 asserções, zero falhas | `evidence/012/isolated/` |
| V12-06 | Instalação inicial via HTTP MCP e processo novo | 100 asserções, zero falhas | `evidence/012/install/` |
| V12-07 | Site-Teste WP 7.1.3/PHP 8.3.30 | Google 0.12.0 ativo, storage pronto, healthy true, zero recuperações não resolvidas | `evidence/012/remote012.json` |

Total local: **642 asserções nativas + 41 contratuais = 683**, com repetições entre cenários; não são 683 casos únicos nem execução integral do PHPUnit. O validador específico `tools/release012.py` vinculou instalador, inventários e entradas de verificação. O gate abrangente histórico `tools/validate.py`/`build/build.py verify` não foi executado nem declarado aprovado.

No Site-Teste, `google/conversion-context` retornou contato/material, quatro destinos ligados sem identificadores completos e flags de verificação false. Uma revisão obsoleta retornou `revision_conflict/data:null`. Caminho documental arbitrário foi recusado. Todos os 19 documentos tiveram revisão, bytes e hash conferidos; os dez arquivos runtime alterados tiveram SHA-256 remoto igual ao instalador. A revisão da configuração selecionada permaneceu `57787e7fc3d7f3e4cdb8225007072c60fd9801aa4c46c1a904972f67e5f83fc6`, com valores observáveis inalterados. Segredos não foram expostos.

Estado final: Google 0.12.0, Core 1.38.0, MCP 0.24.0, Meta/LinkedIn 0.3.0; Yoast 28.7, WP Super Cache 3.1.4 e DreamHost Panel Login 1.0.0 preservados e ativos. Nenhuma fixture/configuração sintética foi criada remotamente. Permanecem os registros normais de auditoria/atualização e o backup recuperável. Os cinco laboratórios encerraram seus próprios processos.

## 5. Banco e volta de versão

Nenhuma nova tabela, migração, default, cifra ou configuração é introduzida por esta release. A instalação limpa usa as estruturas atuais do Google; o upgrade preservou opções, credenciais cifradas sintéticas, conexões, bindings, job concluído, agenda pausada e sentinelas sociais. Essas são provas locais, sem alegar inspeção de segredos ou homologação de jobs comerciais no site remoto.

No laboratório, rollback de arquivos à 0.11.0 e reaplicação da 0.12.0 foram executados; uma pós-imagem adulterada foi recusada. No Site-Teste, `plugins/rollback` com o backup acima e `dry_run:true` retornou `rollback_ready:true`, `changed:false`, `applied:false`; não se desfez a entrega.

O backup do pacote cobre seus arquivos. **Não é backup de banco, configuração, material de cifra nem efeitos externos.** Restaurar arquivos remove o novo consumidor e restaura a leitura 0.11.0, sem desfazer gravações ou efeitos ocorridos depois. Preserve backup coerente e use o protocolo de recuperação/drenagem existente quando for necessária restauração de banco. Não desinstale para atualizar.

## 6. O que permanece pendente

- Homologação em contas reais GA4/GSC/Ads/GTM/Sheets: a rodada usou fixtures Google; os leitores locais não comprovam permissões, ações de conversão, consentimento ou entrega. Mantida a pendência histórica 20 sobre jobs completos/calendário/exportação e paginação na frota.
- Implantador 2.9.0: relatório/identidade examinados, mas o fluxo de implantação inteiro não foi executado; seu responsável deverá confirmar a leitura tipada com a 0.12.0. Seu tratamento de compatibilidade com 0.11.0 pode permanecer.
- Core 1.36.0: equivalência dos schemas conferida, sem executar essa combinação. Core 1.35/1.38 e as duas ordens de avanço foram testados; downgrade do Core após a troca não foi executado.
- Navegador gráfico, multisite, cache distribuído/CDN e cron externo não foram homologados. O painel só recebeu novas entradas no índice documental; leitura/permissões foram exercitadas pelas APIs, sem nova prova visual.
- Frota/repositório: nenhum push, publicação raw, retirada de entrega antiga ou atualização dos outros sites foi realizado. Não há commit novo atribuído a este trabalho. A próxima distribuição cabe ao dono/frota; fonte não publicado publicamente.

Essas pendências limitam as alegações de homologação; não bloquearam o comportamento local entregue e validado.

## 7. Credenciais e configuração do dono

A leitura `google/conversion-context` não requer credencial nova. Os identificadores de contato/material pertencem ao Core e devem ser configurados pelo seu contrato administrativo; vazio é válido e não deve ser preenchido automaticamente a partir de contato.

Para APIs Google, permanece **Ferramentas → Fator3 MCP Google**: selecionar conexão, importar Service Account ou configurar OAuth (`oauth_client_id`, `oauth_client_secret`, `oauth_refresh_token`), validar e ativar explicitamente; declarar serviços e ativos. Ads continua exigindo `ads_developer_token` e eventual login customer ID. GTM exige acesso ao contêiner e escopo apropriado. Não foram coletados nem adicionados segredos nesta rodada. Confira `google/configuration-schema`, `google/preflight` e o guia instalado antes de efeitos remotos autorizados.

## 8. Identidade dos arquivos

| Artefato | Nome do arquivo | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `wp-mcp-google-fator3-0.12.0-instalador.zip` | 721839 | `d2499a5f0b2b89b5640dc86a780fc8a73335dc20d06003eb22b7185ce98162c0` |
| Fonte | `wp-mcp-google-fator3-0.12.0-fonte.zip` | 2825174 | `a7f4efcc73ca4e64d9c76507739f6f7744894856a81f611173d97a256d80e717` |

Somente o instalador é instalável. O fonte tem uma raiz versionada, runtime completo, documentação editável, schemas/fixtures, testes, build, instruções, evidências sanitizadas e cópia deste relatório. Nenhum ZIP da entrega contém outro ZIP.

Este é o relatório externo canônico. A cópia interna é identificada como **cópia anterior ao fechamento do fonte**: tamanho/hash do próprio fonte só são preenchidos aqui após empacotamento, sem reabrir o ZIP. A tabela usa somente nomes de arquivos, preservando o Pedido 25(b). O manifesto externo complementa a conferência automatizada. Impactos vigentes estão referenciados na seção 2 e acompanham a entrega.
