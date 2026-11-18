# Entrega — Fator3 MCP Google 0.37.0

Revisão: 1 · Data/hora: 2026-11-18T17:31:54-03:00 · Rodada: implementação do Pedido MCP Google 55

Slug: `wp-mcp-google-fator3` · Versão/build: 0.37.0 / instalador determinístico 037

Status: **com-pendencias** — implementação e validação local concluídas; instalação pela frota e aceite em contas reais pendentes.

## 1. De onde esta versão entra

Entrada limpa e atualização direta de Google 0.36.0. A base foi recuperada dos arquivos anteriores do projeto: instalador SHA-256 `b066ed24418a1eccaa3c93504e5d817c1e06cf2e4993787fae68201e6a35ac27`, fonte SHA-256 `d7fd142652f8effaa0f7f9d26adbfc55ceee8f11c74ff20ac9c1cfdbdb1dc0b2`. Após a troca local, somente Google 0.37.0 ficou instalado.

Requisitos: WordPress >= 7.1.4; PHP >= 8.3. Exercitados: WordPress 7.1.4, PHP 8.3.6 e 8.4.27, MariaDB 11.8.6. Instalação e atualização nativas foram feitas em PHP 8.3.6; os cenários funcionais e a regressão foram executados nos dois PHP. Chromium 142.0.7444.175 foi usado nos formulários. Não há suporte contratado a runtimes inferiores ou combinações históricas.

Foram lidos integralmente `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos revisão 5 de 02/11/2026, a regra comum, o padrão Google, os novos pedidos de 18/11/2026 e o impacto Core 1.93.0 revisão 2. O pedido 55 determina o escopo. Pedidos 53/54 já aceitos não foram reabertos. Os novos pacotes acompanhantes foram usados como referências e como instaladores na bancada.

## 2. Convivência e encaminhamentos

Conjunto testado: Core 1.93.0, MCP 0.48.0, LinkedIn 0.26.0, Meta 0.28.0 e Pipedrive 0.12.0. Core/MCP/LinkedIn/Pipedrive vieram dos anexos; Meta foi reaproveitado do instalador original disponível no ambiente. `evidence/037/inputs.json` registra os hashes. A paridade completa dos arquivos instalados com os seis ZIPs consta de `installed-parity.json`. Não houve edição de acompanhantes.

| Destinatário | Versão examinada | Classificação / situação | Pedido | Impacto / revisão |
|---|---|---|---|---|
| Fator3 Site Core | 1.93.0 | validacao-coordenada / alinhado tecnicamente, aceite aberto | Google 55 e core 430 | `wp-mcp-google-fator3-0.37.0-impacto-base-site-core-fator3.md`, revisão 1 |

O encaminhamento recebido do Core foi incorporado ao publicador Google. O Core original já atende ao contrato; nenhum patch alheio foi necessário. A integração Google/MCP foi verificada por HTTP autenticado e pela revogação de uma concessão real do MCP local. Os demais acompanhantes foram ativados e preservados; não foi identificado impacto técnico que exija relatório individual para eles. Seus fluxos comerciais completos não foram auditados nesta rodada.

## 3. Mudanças e evidência

| Pedido | Problema | Mudança | Resultado e evidência |
|---|---|---|---|
| 55(a) | Tarefa avulsa presa à concessão criadora | Contexto persistido passa a pertencer ao WordPress; executor seleciona administrador atual e revalida conexão, identidade e política. Retoma bloqueios antigos causados somente pelo transporte. | Seis tipos de tarefa exercitados após revogação da senha de aplicação e rebaixamento do autor. Tarefa antiga bloqueada retomada. |
| 55(a), exportação | Aprovação dependia de intervenção por tarefa | Regra explícita por conexão, ligada ao hash dos parâmetros exatos e à identidade/revisão. Planejamento e confirmação administrativa; nova conferência antes de cada despacho. | Sem regra: zero escritas. Com regra: exportação concluída. Regra revogada: próxima exportação aguarda. Tarefa concluída não repete. |
| 55(b) | Acervo e leitores dependiam do concedente original | `SiteAuthority` revalida administrador atual autorizado. Autor original preservado e perda da autorização gera aviso técnico. | Acervo Ads, leitor Ads, leitor GA4 e leitor GSC funcionaram com substituto; ausência de administrador foi recusada. |
| 55(c), core 430 | Avisos divididos entre correio local, webhook e preferências | Fila durável `technicalnotice`, entrega ordenada pelo filtro Core, observação pelo zelador e visita administrativa. | Ausência/retorno do filtro, abertura/recuperação, repetição sem duplicação e destino técnico testados. Zero Slack. Correio interceptado. |
| 55(d) | Recuperação invalidava prova e exigia ação humana | Consentimento estável separado da prova vinculada à geração. Executor refaz a verificação, conservando os limites da identidade, política, destino e concessão. | GA4 e Ads voltaram a `ready` após recuperação; destino alterado não recebeu validação automática. |
| 55(e) | Vencimento da chave ausente | Consulta IAM da chave ativa, cache de metadados, configuração de antecedência e aviso pelo Core. Exposição em status local, compacto e de todas as conexões. | Vencimento próximo, recusa IAM com preservação do último dado, estado desatualizado e ausência de prazo finito testados. |

Novas habilidades: `google/plan-export-rule`, `google/configure-export-rule`, `google/service-account-key-status`, `google/refresh-service-account-key-status`, `google/plan-key-monitoring` e `google/configure-key-monitoring`. Catálogo: 311 habilidades, 123 de leitura e 188 de escrita; 46 opções de configuração. O campo local de webhook fica inativo; preferências antigas não controlam avisos. O Google não chama diretamente `wp_mail` nem Slack para esses eventos.

Uma regra de exportação autoriza os parâmetros exatos, inclusive consultas, datas, destino e modo de escrita. Não é uma permissão genérica para qualquer exportação futura. Alterações relevantes exigem nova revisão. Operações com resultado incerto continuam exigindo reconciliação e não são repetidas automaticamente.

## 4. Instalação e prova da troca

O mesmo candidato identificado na seção 8 foi instalado pelo `Plugin_Upgrader` nativo, acionado por WP-CLI, em banco limpo e sobre 0.36.0 populada. A pasta instalada foi comparada byte a byte com o ZIP: 209 arquivos, nenhum extra. Os cinco acompanhantes também coincidiram com seus instaladores.

Distribuição da frota ainda não executada. URL prevista após publicação autorizada: `https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-google-fator3-0.37.0-instalador.zip`. Não se afirma que essa URL já exista. Usar o schema vigente de `plugins/upload`, `expected_slug:wp-mcp-google-fator3`, `expected_sha256` da seção 8, `overwrite:true` e `activate:true`. Publicar instalador e relatório; fonte permanece fora do repositório público conforme a decisão 89. Correções posteriores exigem nova versão.

Em nova requisição, consultar `google/status` com `compact:true` e `live:false`: esperar `plugin_version:0.37.0`. Consultar `google/readiness-status` para as condições locais; não exigir prontidão comercial de instalação sem credenciais. A conclusão de uma tarefa é comprovada por seu resultado, não apenas pela admissão na fila.

| ID | Ambiente | Cenário | Resultado | Evidência | Limite |
|---|---|---|---|---|---|
| R37-01 | PHP 8.3.6 e 8.4.27 | Regressão local | 1.366 testes / 16.342 asserções por runtime; zero falhas ou pulos | `unit-final.json`, `unit84-final.json` | Executor de asserções compatíveis; não é execução do PHAR PHPUnit |
| R37-02 | WP 7.1.4, ambos PHP | Pedido 55 | 61 critérios por runtime; zero falhas | `native83-final.json`, `native84-final.json` | HTTP Google e correio sintéticos/interceptados |
| R37-03 | WP 7.1.4 / PHP 8.3.6 | Instalação limpa | ZIP instalado; 37 critérios de leitura, catálogo, schema e formulários | `clean-smoke037.json` | Ambiente local |
| R37-04 | Mesmo ambiente | 0.36.0 populada → 0.37.0 | 2 critérios de preparação, 11 de preservação e 37 de smoke | `upgrade-seed037.json`, `upgrade-final037.json`, `upgrade-smoke037.json` | Sem produção ou downgrade |
| R37-05 | MCP 0.48.0 / HTTP autenticado | Documentação integral instalada | 119 asserções; 26 documentos / 89 páginas, bytes e SHA-256 conferidos | `mcp-docs037.json` | Senha de aplicação descartável de laboratório, revogada ao terminar |
| R37-06 | Chromium / 360, 768, 1440 px | Três painéis e confirmação | 10 casos, sem transbordamento interno ou erro JS; confirmação por teclado sem JS | `ui/results.json` e imagens | Um navegador; não certifica toda a interface ou tecnologia assistiva |
| R37-07 | Ambos PHP | Sintaxe e integridade | 204 arquivos PHP por runtime sem erro; documentação e geradores conferidos | `lint-final.json`, `docs-check.json`, `installed-parity.json` | Não equivale à matriz histórica integral de build |

As evidências ficam em `plugin/wp-mcp-google-fator3/evidence/037` no fonte. O índice `google/documentation` e cada página foram lidos pelo transporte MCP, com `expected_revision` até `next_offset:null`. Há 26 documentos instalados e 54 exemplos catalogados. As evidências de versões anteriores presentes no fonte são históricas e não compõem estas contagens.

Estado final: laboratório limpo, sem credenciais Google, concessões descartáveis, tarefas de teste ou fixture ativa; Google 0.37.0 e os cinco acompanhantes vigentes ativos no banco local, servidor HTTP encerrado. Site-Teste apenas consultado: Google 0.36.0, Core 1.93.0, MCP 0.48.0, LinkedIn 0.26.0, Meta 0.28.0 e Pipedrive 0.11.1. Nenhuma instalação compartilhada ou configuração remota foi alterada.

## 5. Banco, migração e correção por nova versão

Novos estados por conexão: regras de exportação, antecedência do aviso, metadados IAM e cursor de varredura de tarefas bloqueadas. A fila técnica usa o armazenamento de registros existente. Não há nova tabela SQL. O cursor e os metadados de consulta ficam fora da revisão de configuração apresentada ao administrador.

A migração conserva credenciais cifradas, vínculos, destinos, concessões e estados dos jobs. Somente provas ou validações pendentes que coincidam com o contexto corrente adquirem autorização estável de renovação. Isso não cria prova nova nem autoriza exportações automaticamente. Os principais dados preservados foram comparados no teste de atualização, incluindo os bytes cifrados da credencial.

Manter backup coerente de banco, estado persistido e chaves de cifra WordPress antes da instalação real. Uma restauração passa pelo procedimento de recuperação e reconciliação dos efeitos externos. Resultado incerto não pode ser repetido para tentar concluir a migração. Não foi implementado downgrade; defeito descoberto depois da instalação exige uma release nova.

## 6. O que permanece pendente

1. Frota: publicação raw, instalação com hash/slug e prova por requisição nova. O trabalho desta rodada produziu e testou os arquivos, sem publicar ou instalar em ambiente compartilhado.
2. Dono/frota: aceite do Pedido 55 em CTOOffice, com tarefa pendente, reautorização e revogação da concessão anterior, seguido da leitura Core no dia seguinte. A condição temporal não foi simulada como aceite real.
3. Dono das contas: validação IAM com a chave efetiva e suas permissões; verificações GA4/Ads reais após recuperação. O Site-Teste consultado estava sem credencial Google configurada.
4. Operação: recebimento real do aviso no destino técnico Core. A bancada comprovou a seleção do destinatário e o contrato, com transporte postal interceptado.
5. Ferramentas: a regressão usou o executor de asserções compatíveis preservado no fonte. Não houve execução do PHAR PHPUnit nem promoção pelo gate histórico abrangente. Navegadores adicionais e teste completo com leitor de tela não foram realizados.

Essas pendências são registradas no checklist de encerramento; não há declaração de conformidade operacional integral.

## 7. Credenciais e configuração do dono

Conexão → Identidade: manter a identidade Google apropriada; a validade exibida se refere à chave ativa da conta de serviço. Para consultar IAM, habilitar a API e conceder `iam.serviceAccountKeys.get` à identidade utilizada. A validade da chave não é derivada da duração de um token OAuth. Quando o Google informa o marcador de ausência de prazo finito, a interface mostra esse estado. Em recusa, conferir o diagnóstico e a data da última consulta.

Definir a antecedência de aviso entre 1 e 365 dias, com planejamento e confirmação; padrão de 30 dias. A consulta periódica ocorre no executor, no máximo uma consulta a cada seis horas por conexão. Um prazo de expiração não substitui a verificação de desativação ou perda de acesso.

Avançado → Controles: informar a tarefa de exportação, conferir seus parâmetros e confirmar a regra. Desabilitar a regra impede novos despachos automáticos. No Site Core, configurar o destino técnico de avisos. Garantir a passagem do cron/zelador e a existência de administrador atual autorizado. Não incluir credenciais em relatórios ou mensagens de aceite.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `wp-mcp-google-fator3-0.37.0-instalador.zip` | 988922 | `2b3695f8d477c593a80c5a91cffac27761d14ed4d50d3d3454b625c6dda85ab5` |
| Fonte | `wp-mcp-google-fator3-0.37.0-fonte.zip` | 18520586 | `68decffc801a1e1a388914f883fdedef5b01dcbc38a59cfcd9fd449b58f02b12` |

Este é o relatório externo canônico `wp-mcp-google-fator3-0.37.0-relatorio.md`. A cópia dentro do fonte está marcada como anterior ao fechamento e mantém os campos do próprio fonte por preencher. A tabela acima identifica os bytes finais, sem reconstruir o ZIP para inserir seu próprio hash. Nenhum ZIP contém outro ZIP. O instalador é cópia dos bytes aprovados da candidata; ferramentas, testes, evidências e arquivos temporários não entram no instalador.

Complemento: `wp-mcp-google-fator3-0.37.0-impacto-base-site-core-fator3.md`, revisão 1. O fonte contém os arquivos editáveis, os geradores e a reprodução corrente em `reproducao/LEIA-ME.md`.
