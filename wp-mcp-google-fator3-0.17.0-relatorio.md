# Entrega — Fator3 MCP Google 0.17.0

Data: 22/10/2026. Implementação concluída para os pedidos **33, 34 e 35**. Base direta: **Google 0.16.0**. O instalador entregue é o mesmo candidato validado; não foi publicado nem instalado na frota nesta rodada.

## 1. Bases aceitas

| Pacote | Base recebida | Situação nesta entrega |
|---|---|---|
| Fator3 MCP Google | 0.16.0 | Atualizado para 0.17.0 |
| Site Core Fator3 | 1.46.1 | Original, sem alteração |
| Fator3 MCP | 0.25.0 | Original, sem alteração |
| Fator3 MCP Meta | 0.4.1 | Preservado no upgrade |
| Fator3 MCP LinkedIn | 0.4.1 | Preservado no upgrade |

Pedidos lidos da aba Google recebida, incluindo o relato da Data Manager de 21/10. Normas comuns revisão 4 aplicadas. Hashes dos insumos aceitos e dos ambientes estão em `evidence/017/inputs.json` e `validation017.json` no fonte. Bases fornecidas não foram renumeradas nem regravadas.

## 2. Convivência e encaminhamentos

**Esta versão não modifica o Core.** O Core 1.46.1 recebido já contém `reconciliar` e o contrato `site-conversion-reconcile/1.0.0` necessário ao Ads. A integração foi exercitada usando esse instalador original: ingestão incerta, consulta posterior e confirmação sem nova ingestão.

Não há arquivo de impacto novo: não foi identificado desenvolvimento ou ajuste de contrato necessário em Core, MCP, Meta ou LinkedIn. Foram avaliados registro de habilidades, descoberta MCP, autorização, auditoria, SDK de medição/conversões, cron, opções, tabelas e rollback. Os impactos presentes nas evidências históricas do fonte pertencem às versões anteriores. A dependência técnica da 0.16 está atendida no Core recebido; isto não altera tickets nem declara trabalho de terceiros concluído por esta entrega.

Preservados: slug, pasta, basename, namespaces, 286 identificadores públicos de habilidades, 111 leituras/175 escritas, 36 opções declaradas e contratos públicos. Os schemas de entrada/saída das 286 habilidades permanecem idênticos aos da base. A configuração permanece 4.0.0, catálogo 3.0.0, execução/armazenamento/manutenção 2.0.0. São **158 arquivos de runtime**, nos mesmos caminhos da 0.16; sete arquivos têm bytes alterados.

## 3. Mudanças por pedido e evidência

| Pedido | Implementação | Evidência principal |
|---|---|---|
| 33 — Permissões por recurso | 231 operações com rótulos em português, ações específicas e sem rótulos duplicados dentro de cada serviço. Identificador de habilidade/método na descrição, associado ao controle por `aria-describedby`. | `labels017.json`, 525 verificações por cenário; DOM autenticado. |
| 34 — Diagnóstico Data Manager | Resposta padronizada com `success:false`, `error_code` e `provider_error`: HTTP, estado, motivo, campo e mensagem sanitizados. Mesmo diagnóstico no incidente; auditoria registra código de falha. Não persiste resposta bruta, corpo de evento, token ou contato. | `delivery017.json`; retorno, incidente, auditoria e UI exercitados com HTTP 400 sintético. |
| 34 — Primeira validação recusada | NOT_FOUND em `destination_references` agenda nova validação em 5 minutos, com espera progressiva limitada a 1 hora, mesmo sem prova anterior. O executor existente executa `validateOnly`; não coleta conversão. Destino, credencial, política ou concessão alterados impedem a tentativa com autorização antiga. | Falha inicial → execução sem usuário interativo → sucesso; bloqueios antes de HTTP; outros erros iniciais não armam repetição. |
| 34 — Preservação GA4/Ads | Configuração parcial preserva campos omitidos; mudanças de destino ou segredo revogam apenas a prova afetada. Salvar Ads mantém GA4 pronto e vice-versa. Concessões são mantidas por destino; editar um destino não transfere o outro para o novo administrador. | Provas comparadas byte a byte, prontidão, administrador diferente, mudança concorrente e upgrade com provas legadas válidas. |
| 35 — Habilidades | Todos os 286 rótulos registrados em português; os nomes públicos permanecem iguais. Catálogo editável em `docs/labels-pt-br.json`, compilado para arquivo já existente. | Registro nativo completo, catálogo por MCP HTTP e correspondência com documentação compilada. |

A causa da disponibilidade posterior da ação no relato real **não foi estabelecida**. A mensagem orienta conferir o destino e informa a nova validação automática; não atribui o erro definitivamente à propagação.

## 4. Instalação, prontidão e provas

Ambiente nativo: **WordPress 7.1.2, PHP 8.3.6, MySQL 8.0.46**, servidor PHP CLI com quatro processos, bancos isolados. Os mínimos declarados foram executados. Dependências Ubuntu de PHP foram recompostas na revisão disponível 8.3.6-0ubuntu0.24.04.13; manifesto de hashes incluído. Google e e-mail foram simulados, com dados sintéticos.

| Cenário | Verificações nativas | Resultado |
|---|---:|---|
| Instalação limpa | 771 | Aprovado |
| Atualização 0.16 → 0.17, rollback e reaplicação | 678 | Aprovado |
| Google ativado antes de Core/MCP | 625 | Aprovado |
| Google isolado | 22 | Aprovado |

Total: **2096 verificações nativas**, zero falhas na matriz final. Além disso, **60 verificações de contrato/resposta**, lint de **154 arquivos PHP**, geração documental, comparação de schemas/identidades e inventário exato. O teste DOM contém **13 verificações de interação**, subordinadas à sua verificação de execução na matriz (não somadas duas vezes ao total nativo).

`tools/release017.py` vincula evidências ao SHA-256 exato do instalador, dos insumos e do código/testes. A suíte de regressão exercita renovação, deduplicação, respostas incertas, GA4, Core, formulários e nonce. A fixture de clique foi ajustada à exigência do Core 1.46.1 de instante de atribuição válido; a regra Core não foi alterada.

Documentação instalada: índice e leitura completa/paginada pelo MCP HTTP autenticado, UTF-8, versão/hash, recusa de continuação obsoleta e controle administrativo. Inclui o guia 0.17.0 e catálogo atual. Leitura de ajuda não chamou Google. `documentation017.json` contém hashes e páginas lidas. Esta é uma matriz dirigida, não uma reexecução do gate integral histórico PHPUnit/tools/validate.py.

**Site-Teste:** consultado antes/depois via WP MCP fator3-teste, saudável, com WordPress 7.1.3/PHP 8.3.36, Google **0.16.0**, Core **1.46.1**, MCP **0.25.0**, Meta/LinkedIn **0.4.1**, todos ativos. Não houve instalação remota nesta rodada. `site-teste017.json` contém a evidência sanitizada. O estado remoto não é apresentado como teste do candidato 0.17.

Chrome for Testing 156.0.8078.47 foi obtido, mas não iniciou: criação de socket negada pelo ambiente. A interação foi validada por **jsdom 27.4.0** sobre HTML/JS nativos e páginas autenticadas: seleção reversível, descrições acessíveis, formulário de conversões, senha e diagnóstico do incidente. Não há aprovação visual ou de layout móvel.

## 5. Banco e reversão

Sem tabela nova ou migração destrutiva. A opção existente de conversões recebe metadados por destino: `granted_by_target`, `pending_verification` e estado de renovação. Provas da base são reconhecidas sem migração. Incidentes usam o repositório já existente. A instalação não habilita transporte nem troca credenciais.

Upgrade, rollback real e reaplicação pelo MCP preservaram configuração, ciphertext, conexão adicional, registros, agendas e sentinelas Meta/LinkedIn. O rollback recuperou o inventário exato da 0.16; edição posterior de arquivo impediu a reversão automática, como esperado.

Reverter arquivos não desfaz configurações nem eventos externos. Quando concessões dos dois destinos pertencem a administradores diferentes, o campo compartilhado legado fica zerado: a 0.16 bloqueia envio até autorização explícita, em vez de reaproveitar concessão de outra pessoa. Preserve backup coerente de arquivos, banco, salts, recibos e fila Core; não apague registros incertos para provocar reenvio.

## 6. Pendências e responsáveis

| Pendência | Responsável | Limite desta entrega |
|---|---|---|
| Publicar instalador/relatório na raiz raw e instalar com SHA-256 e slug esperados | Dono/frota | Artefatos entregues; sem push, publicação ou instalação remota. |
| Conferir painel em navegador real após instalação | Dono/frota | DOM aprovado; Chrome local impedido por socket. |
| Reproduzir a ação real da Data Manager, inclusive demora de disponibilidade | Dono da conta Google | Testes sintéticos não comprovam causa ou prontidão da conta real. |
| Acompanhar renovação por dois dias e homologações Ads 113/125, GA4 e primeiro contato com clique | Dono/frota | Permanecem os aceites reais anteriores; esta rodada não envia conversão comercial. |

Nenhuma espera por desenvolvimento Core é necessária. Multisite, PHP-FPM e outros runtimes não foram homologados nesta rodada.

## 7. Credenciais e privacidade

Credencial do conector Site-Teste utilizada somente para leitura. Laboratórios usam credenciais sintéticas e senhas de aplicação descartáveis; sessões são removidas ao final. Nenhuma credencial real, cookie, banco de laboratório ou log pessoal integra os artefatos. Os diagnósticos mascaram segredos conhecidos, tokens, e-mail e números potencialmente pessoais, com campos e tamanhos limitados. Os testes incluem resposta que ecoa segredo e contato fictícios.

## 8. Artefatos

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| `wp-mcp-google-fator3-0.17.0-instalador.zip` | 767299 | `42bd11080b518c82e0960753fa7b08d7adae28743cfcd3e96f9b83bf3f4709b0` |
| `wp-mcp-google-fator3-0.17.0-fonte.zip` | 3312383 | `e76a58051a634eeb1f4c5dbb698a5847f13eb2309259a1d5449730ae89c6ea3c` |

Somente o instalador é instalável. O fonte contém código editável, build, testes, evidências sanitizadas e esta cópia do relatório anterior ao fechamento. Nenhum ZIP da entrega contém outro ZIP. O hash final do fonte aparece apenas no relatório externo, evitando circularidade.

Referências técnicas consultadas: [validação de eventos Data Manager](https://developers.google.com/data-manager/api/reference/rest/v1/events/ingest), [erros Data Manager](https://developers.google.com/data-manager/api/devguides/concepts/understand-errors) e [BadRequest](https://developers.google.com/data-manager/api/reference/rest/v1/BadRequest).
