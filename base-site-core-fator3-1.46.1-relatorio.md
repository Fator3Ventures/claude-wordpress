# Entrega — Fator3 Site Core 1.46.1

Revisão 1 · 22/10/2026 · continuação da homologação e correção do pedido 281 · **com-pendencias** de frota, fornecedores e observação longitudinal. A correção de cache está implementada e validada no escopo abaixo. Horários em America/Sao_Paulo.

## 1. De onde esta versão entra

Instalação limpa ou atualização direta de **1.46.0 para 1.46.1**. Base: instalador 1.46.0, 2.175.518 bytes, SHA-256 `b6de147c8e900c2cb9367bafb2dad6494372bbd81953c44b5e4d4990f8f34ad6`; fonte-base 3.175.636 bytes, SHA-256 `c213a8a7a8657ed188c0148dd4014942d45be67851adf15a5aa4db653e95aef0`. Os arquivos já entregues da 1.46.0 permanecem inalterados.

Patch da mesma rodada, conforme a preferência do dono por incrementar o terceiro número quando há mais de uma versão no ciclo. Escopo: concluir a prova de reaquecimento do pedido 281 e corrigir o impedimento encontrado no modo real do WP Super Cache. Pedidos 263 e 274–283 da base são preservados. Contrato 8.11.0, perfil piso-padrao-3.6 e estrutura de banco 1.45.0 permanecem.

## 2. Convivência e encaminhamentos

Site-Teste: WordPress 7.1.3, PHP 8.3.36, MySQL 8.0.41; Core 1.46.1 com MCP 0.25.0, Google 0.16.0, Meta 0.4.1, LinkedIn 0.4.1, WP Super Cache 3.1.4 e Yoast 28.7. O contrato dos acompanhantes MCP/Google continua compatível. O modo observado do cache é `wp-cache-cabecalhos`.

Não foi identificado novo impacto de desenvolvimento para MCP, Google, Meta, LinkedIn ou Implantador neste patch: a correção é interna ao reaquecimento do Core, sem novas dependências, cópias compartilhadas ou mudança de contrato. O impacto já entregue `base-site-core-fator3-1.46.0-impacto-implantador-base.md`, revisão 2, continua **aberto / acao-necessaria**; esta entrega não afirma que o Implantador o resolveu. O fonte conserva esse documento e o relatório externo da base em `history/1.46.0/`. Não houve envio a terceiros, publicação no repositório ou implantação na frota.

## 3. Mudanças e evidência

| Pedido | Problema confirmado | Correção e prova |
|---|---|---|
| 281 — reaquecimento | A 1.46.0 aceitava apenas simple/expert. O Site-Teste usa corpo PHP protegido e metadados do WP Super Cache; a tarefa retornava cache_nao_compativel. | Reconhecimento do par anônimo wp-cache/meta-wp-cache e execução também em wp-cache-cabecalhos. Prova local e no WordPress remoto com HTTP real. |
| 281 — limite da remoção | Renovar exige retirar somente a cópia vencida selecionada, preservando variantes privadas e alterações concorrentes. | Conferência de caminho, URI, chave, nome, prefixo, metadados, mtime e SHA-256. Sem executar PHP. Pares recentes, privados, dinâmicos, symlinks e formatos desconhecidos são excluídos. Variantes gzip são reconhecidas. |
| 281 — prova observável | HTTP 200 sozinho não prova geração ou uso do cache. | Resultado copia_gerada/copia_servida exige igualdade entre corpo HTTP e conteúdo armazenado. ultima_execucao registra modo, código e quantidade na ability; nome ajustado após observar ocultação do candidato pelo transporte MCP. |

O GET de reaquecimento usa a origem e o caminho público selecionado, sem cookies, parâmetros ou redirecionamento, com Accept-Encoding: identity. Mantidos: desligado por padrão, histórico de pessoas, teto móvel por hora incluindo falhas, até três requisições por execução, recuo por página e exclusão da coleta do Core. O Core não altera TTL nem liga o preload durante instalação/execução.

O reconhecimento da chave PHP foi conferido com o formato padrão do WP Super Cache 3.1.4. Filtros de terceiros que alterem essa chave não são presumidos como variantes anônimas. A proteção por conferência de arquivos reduz interferência com escritores concorrentes; não equivale a uma transação atômica com processos externos do provedor.

## 4. Instalação e prova da troca

Laboratório descartável: WordPress 7.1.3, PHP 8.3.6, MySQL 8.0.36. **103 verificações direcionadas aprovadas**: 11 de regressão do cache simple/expert, 18 do modo com cabeçalhos e 74 de documentação, paginação e autorização. **228 arquivos PHP** passaram no lint. Instalação limpa e atualização direta da 1.46.0 pelo Plugin_Upgrader passaram com o ZIP final desta entrega; preservação de dados/opções/segredos, repetição idempotente e prontidão foram conferidas. A espera de finalização é acelerada somente no estado descartável do laboratório.

Os 605 testes PHP, 33 casos de navegador e 26 verificações visuais descritos na 1.46.0 são evidência herdada da base, não reexecução deste patch. Não houve alteração de JavaScript ou telas que exigisse repetir aquela matriz.

Antes da troca remota, o Core foi preparado/drenado e o banco exportado para armazenamento privado no site: **21.521.341 bytes**, SHA-256 `51e299b6da5bc73c1372736ba72405bfc5b2d122ef9039db3139c251309cd0cf`. O conteúdo do banco não foi baixado nem incluído nos artefatos. A retomada avançou a guarda operacional de geração 4 para **5**. Também foi preservada a configuração anterior do WP Super Cache em `wp-content/f3-core-state/qa1461-wp-cache-config-before.php`.

O instalador foi transmitido em partes, conferido por hash e aplicado pelo canal nativo com expected_slug=base-site-core-fator3, overwrite=true e activate=true. A operação final `d553348b83662b1e667350cd` confirmou applied=true, plugin ativo e sondas de home/REST aprovadas antes e depois. O pacote privado inicial da 1.46.1 foi substituído pelo pacote final após o ajuste do diagnóstico; nenhum candidato intermediário foi entregue. A atualização direta 1.46.0 → 1.46.1 foi demonstrada separadamente no laboratório com esse mesmo ZIP final.

### Prova de cache real no Site-Teste

Em **22/10/2026 às 09:15:04–09:15:06 −03**, foi usada a home, que já tinha histórico humano elegível. Não foram inseridas visitas sintéticas para selecioná-la. Um fixture temporário, restrito ao host e ao cron, envelheceu somente o mtime do par anônimo dessa página para `agora − 86405`, após conferir os hashes. Isso exercita a expiração de forma controlada; não representa espera real de 24 horas.

O executor real fez **uma requisição**, registrou **copia_gerada**, HTTP 200, duração de 992 ms e gerado_em=1792671306. O GET seguinte, também sem cookies, recebeu corpo com SHA-256 `57cf711d7f62885449878aae0aea641ee3dcbf3b13093ecc8a47c0fc8743da73`, igual ao artefato recém-gravado e com marcador do WP Super Cache. O conjunto body/metadados foi real; o transporte HTTP não foi simulado.

| Contador do Core | Antes | Depois |
|---|---:|---:|
| Eventos | 3156 | 3156 |
| Análise | 1279 | 1279 |
| Sessões | 258 | 258 |

O fixture PHP e seu JSON foram removidos; o evento temporário ficou ausente. As cópias privadas de segurança permanecem para recuperação. Nenhum contato ou página foi criado nesta continuação.

Estado final do piloto autorizado: **reaquecimento ativo**, janela de visitas de **7 dias**, limite de **20 páginas/hora**, TTL **86400**, preload **0**. A configuração foi feita explicitamente para o piloto solicitado; não é novo padrão imposto pelo instalador. A agenda regular do Core permanece. A leitura MCP confirma resultados e ultima_execucao sem ocultação.

A verificação pública do próprio Core também confirmou cabeçalhos e HIT na geração atual às 09:19:46 −03 (status verified, pending=false).

Prontidão: Core 1.46.1 operacional, geração 5, **18 etapas concluídas**, zero falhas e zero esperas. A documentação atual foi lida integralmente por `f3base/documentacao-ler`, proxima_linha=null, com hashes iguais aos arquivos locais: `docs/RELEASE-1.46.1.md` = `03289344f773e7887572133ff940eee526b1c599f8a00de80c617bfc1c3315a5`; `docs/AGENTES-1.46.1.md` = `a05518f99c1f06e462588c620d9ba97f6861b00cc752d0caf3647345ad408294`. Evidência saneada: `evidence/site-teste-1461.json`.

## 5. Banco e volta de versão

Sem tabela, coluna ou migração estrutural nova. O estado existente do reaquecimento recebe o diagnóstico ultima_execucao e conserva reservas/resultados. As configurações de contato, integrações e credenciais permanecem.

Para reverter este piloto, desligue o reaquecimento e restaure a configuração de TTL anterior (3600) pelo provedor, usando a cópia privada como referência. Para voltar o plugin à 1.46.0, prepare a recuperação, restaure arquivos/banco coerentes e reconcilie antes de retomar. A 1.46.0 conserva a limitação do reaquecimento neste modo. Cache de página é regenerável; apagar ou restaurar cache não substitui backup do conteúdo. A guarda do Core não pausa automaticamente os acompanhantes.

## 6. O que permanece pendente

- **Frota/cache:** implantar a correção no outro site do piloto (Korvena.net) e observar os quatorze dias após a implantação. A ativação e prova pontual do Site-Teste estão concluídas; não comprovam a observação longitudinal.
- **Frota/redes oficiais — 283:** instalar em fator3.com.br e reler as duas fontes Perplexity após a primeira passagem das 02:00. O aceite de 302 → 200 e estado atual no Site-Teste já foi registrado na 1.46.0; esta continuação não alterou essa implementação nem executou a frota.
- **Frota/CRM e dispositivos:** permanecem os aceites reais de Pipedrive, Slack, SMTP, seguidores/notas/aprovação e autofill em Android/Kwai descritos no relatório da 1.46.0. Não há novo comprovante de fornecedor ou dispositivo físico nesta entrega.
- **Frota/operações e Implantador:** permanecem a espera esgotada de fator3.com.br e o impacto aberto do Implantador. Nenhum resultado de outro responsável foi presumido.
- **Runtime:** o mínimo PHP 8.3.6 foi exercitado; a rodada usa WordPress 7.1.3. O mínimo 7.1.2 preservado do cabeçalho não recebeu nova prova. Sem nova declaração de suporte a multisite ou formatos personalizados de chave de cache.

## 7. Credenciais e configuração do dono

Nenhuma credencial nova. O piloto usa a opção administrativa existente f3base_cache_reaquecimento (ativo, dias_visita, paginas_por_hora), com guarda de revisão, e a configuração do WP Super Cache. Consultar `f3base/cache-reaquecimento-ler` não dispara aquecimento. Os segredos e destinos das integrações continuam nos campos já documentados na base; não são necessários para a correção de cache.

## 8. Identidade dos arquivos

| Arquivo final | Bytes | SHA-256 |
|---|---:|---|
| base-site-core-fator3-1.46.1-instalador.zip | 2185721 | 2e834ba27728a32a22fa588cc05863d1d69ccc2e09b0c05e016d88404eaadc76 |
| base-site-core-fator3-1.46.1-fonte.zip | 3201244 | add385d393dca6afe7c095a73b0476369fee658d0eca0e29cc66a4b2bc0f92e0 |

[Instalador](base-site-core-fator3-1.46.1-instalador.zip) · [Fonte](base-site-core-fator3-1.46.1-fonte.zip).

Instalador com raiz única base-site-core-fator3/, sem fixtures, laboratório, bancos ou runtime. Fonte com código, build, testes, evidências saneadas, histórico identificado e cópia deste relatório anterior ao fechamento. Tamanho/hash do próprio fonte são preenchidos somente no relatório externo canônico, evitando circularidade. Nenhum ZIP contém outro ZIP da entrega. A entrega recomendada passa a ser 1.46.1; os artefatos 1.46.0 permanecem como histórico.
