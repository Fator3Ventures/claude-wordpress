# Entrega — Fator3 Site Core 1.30.0

Implementação do plano consolidado de 11/10/2026, baseado no documento de pedidos das 14:28:16 (SHA-256 a4401b4e81f0adac7285257d65e4989fc02a798145d00095be103dc8b5b29282).

A versão inclui a manutenção dos avisos Slack e os itens 173, 174, 180, 189, 192 e 193. O código está implementado e validado localmente. O aceite visual integral do item 180 permanece pendente, pelos limites descritos abaixo.

## Arquivos

- `base-site-core-fator3-1.30.0-instalador.zip`: instalar/atualizar no WordPress; inclui código, assets e documentação para agentes.
- `base-site-core-fator3-1.30.0-fontes.zip`: código, scripts de teste, evidências finais resumidas e plano de referência; não instalar este ZIP como plugin.
- `base-site-core-fator3-1.30.0-impacto.md`: encaminhamento aos responsáveis por MCP, MCP Google e temas.
- `base-site-core-fator3-1.30.0-SHA256.txt`: integridade dos arquivos da entrega.

## Escopo e implantação

Referência de implantação: WordPress novo ou Core 1.29.0, sem trava rígida por versão e sem compromisso de retorno. Contrato 6.6.0. Matriz: MCP Fator3 0.19.0 e MCP Google 0.8.2; nenhum companheiro/tema alterado.

| Demanda | Entrega |
|---|---|
| Slack da conversa | Leitura de aviso/thread, verificação, correção própria, limpeza de testes e registro durável de teste de conexão, pela integração atual. |
| 173 | Resolvedor de WhatsApp compartilhado pelas duas etapas, preservando URL/texto do CTA. Inventário de gatilhos data-f3base-abrir-formulario. |
| 174 | Causa e orientação dos avisos degradados, descoberta da credencial/abilities; clique simples sem formulário fictício. Regressões de título, reconciliação e partes órfãs. |
| 180 | Hierarquia/classes do índice e compartilhar conforme pedido; IDs somente na composição que usa o índice, inclusive padrões/partes, preservando IDs autorais. |
| 189 | Explicação do aviso WordPress, observação e reconciliação limitada da agenda própria, sem encobrir falhas. |
| 192 | Publicidade pré-autorizada por instalação, distinta de medição e de consentimento individual, com negativa prioritária e persistente. |
| 193 | Catálogo Pipedrive paginado e completo pela tela e MCP, com conta/revisão e preservação em falha. |

## Instalação e dados

Instale o ZIP normal pelo WordPress/MCP. A atualização cria a tabela de manutenção Slack e complementa a opção de publicidade, conservando escolhas, listas vazias e procedência. Não envia mensagens de teste, reativa integrações ou converte autorizações históricas em aceites individuais. Finalização e provas externas seguem o executor existente.

Leia SLACK-1.30.md, PUBLICIDADE-1.30.md, QUALIDADE-CATALOGO-1.30.md, CRON-DIAGNOSTICO-1.30.md e IMPACTO-1.30.0.md. Catálogo e schemas instalados são acessíveis por f3base/documentacao-ler.

## Limites de evidência

Testes de Slack/Pipedrive/Meta usam transportes simulados e validam contratos/estados, não entrega a uma conta real. Homologação do workspace e observação de cron na frota continuam externas. Os fontes dos temas fator3-tech-blocos 3.3.0 e korvena-blocos 2.4.0 não estavam disponíveis; o Site-Teste conectado tem somente F3 Base 1.6.16. O HTML foi alinhado à estrutura descrita no pedido e testado localmente, mas igualdade integral/aparência com os dois temas ainda requer comparação dos seus arquivos/CSS. Não se realizou teste em korvena.net.br nem alteração remota.

## Validação local

Ensaios concluídos em 11/10/2026, com WordPress 7.1.2, PHP 8.3.6, MariaDB 10.11.14 e Chromium 138, usando dados sintéticos e transportes externos bloqueados ou simulados. Nenhuma mensagem enviada a terceiros e nenhuma instalação remota alterada. Não houve teste em korvena.net.br.

| Evidência | Asserções | Resultado |
|---|---:|---|
| instalacao-nova.json | 10 | Passou |
| ciclo-instalacao.json | 11 | Passou |
| slack-manutencao.json | 43 | Passou |
| publicidade.json | 25 | Passou |
| catalogo-1300.json | 7 | Passou |
| correcoes-1300.json | 21 | Passou |
| browser-publicidade.json | 7 | Passou |
| browser-http.json | 10 | Passou |
| browser-banco.json | 10 | Passou |
| browser-advanced.json | 17 | Passou |
| comunicacao.json | 81 | Passou |
| historico.json | 27 | Passou |
| historico-volume.json | 6 | Passou |
| complementos.json | 12 | Passou |
| crm-complemento.json | 8 | Passou |
| slack-app.json | 16 | Passou |
| avisos.json | 30 | Passou |
| qualidade.json | 18 | Passou |
| release.json | 29 | Passou |
| contratos-1290.json | 11 | Passou |
| webhook.json | 29 | Passou |
| operacao-1290.json | 16 | Passou |
| diagnostico-1290.json | 6 | Passou |
| telas.json | 9 | Passou |
| funcional.json | 28 | Passou |
| novidades.json | 27 | Passou |
| operacao.json | 18 | Passou |

197 arquivos PHP e 28 arquivos JavaScript passaram na verificação sintática. Os nove assets públicos minificados acompanham manifesto de bytes e SHA-256, produzidos com Terser 5.44.0. As duas ordens frias de carregamento de MCP 0.19.0/Google 0.8.2 e as guardas de recuperação independentes passaram; o SDK Google real passou em 20 verificações com HTTP simulado. As contagens são asserções, não percentuais de cobertura nem aceites executados na frota.

## Resultados principais

- Instalação limpa com estrutura pronta. Atualização 1.29.0 → 1.30.0 por `plugins/upload-base64` do MCP real, com home/REST, primeira página em menos de dois segundos, captura antes da finalização e preservação de listas vazias, opções e procedência. A auditoria de composição usa tema sintético local.
- Slack: intenção de teste persistida sem lead fictício; autoria/workspace; presença remota distinta de aceite; thread com 19 mensagens em duas páginas; edição no mesmo timestamp; revisão/chave idempotente; exclusão das próprias respostas de teste preservando principal com resposta humana; recusa de produção/ID desconhecido; falta de escopo, 429 e timeout sem repetição cega; token alterado invalida vínculo; conteúdo cifrado; telas sem HTTP no GET.
- Publicidade: independente da medição; fundamento da política sem consentimento individual inventado; negativa de cookie antigo, referência perdida, revogação expirada e marca manual preservadas. Captação nativa com negativa mapeada e sem inferência pelo nome do campo. A CAPI enfileira e inicia sob política sem medição, e relê a negativa antes do HTTP. Não ocorre disparo automático de conversões históricas.
- Navegador com assets minificados e endpoints/banco reais por HTTP local: publicidade liberada e analytics negado no Consent Mode; atribuição do toque atual sem sessão/histórico persistente de audiência; recibo real de negativa e preservação após recarga/versão antiga. Formulário em duas etapas mantém URL e texto completo do CTA também no sucesso da segunda etapa, com um contato e anexo. Rolagem por roda e toque, diálogo/foco/Escape, erro 5xx legível e ausência de erro JavaScript.
- Catálogo: simulação sem consumo remoto; paginação integral de funis e etapas; atualização atômica; falha preserva snapshot anterior; conta/revisão e troca de credencial; disponibilidade falsa/desconhecida preservada.
- Artigos: IDs autorais inclusive sem aspas, colisões e estabilidade; `data-id` não é tratado como âncora; composição com índice antes/depois do conteúdo e em padrão reutilizável; cards e feed preservados; classes/hierarquia conforme pedido. Não foi homologada igualdade visual com os dois temas da frota.
- Cron: estado desejado comprovado distinto de falha real/causa indeterminada; reconciliação limitada às tarefas próprias; falhas WordPress não suprimidas; hooks de terceiros intactos; dois processos não repetem callback.
- Regressões de comunicação, anexos, histórico, entregas, formulários, CRM, webhook, Clarity/ofertas e telas administrativas. O histórico de volume usa 30.368 linhas sintéticas; não constitui promessa de latência na frota.

## Limites e pendências de homologação

1. Item 180: os fontes de fator3-tech-blocos 3.3.0 e korvena-blocos 2.4.0 não estavam disponíveis. A consulta somente leitura do Site-Teste mostrou F3 Base 1.6.16. Comparar o HTML/CSS e a aparência dos blocos com os dois temas antes de retirar filtros/workarounds do tema. Esse aceite permanece parcial.
2. Slack/Pipedrive/Meta: os testes locais validam payload, estados e falhas simuladas. Escopos, presença e apresentação na conta real continuam dependentes da homologação externa. A leitura Slack pode exigir autorização de history no aplicativo já existente.
3. Cron na frota, cache/proxy, proteção dos arquivos privados e quotas reais precisam de observação no servidor. Safari iOS e navegadores internos Instagram/Facebook em aparelhos físicos não foram exercitados.

As evidências finais resumidas acompanham o ZIP de fontes. Falhas injetadas, tentativas intermediárias, cookies, logs, runtimes e imagens de inspeção não são distribuídos. A última atualização foi repetida com diretório de conteúdo novo para evitar reaproveitar arquivos de execuções anteriores do laboratório. Consulte RELEASE-1.30.0.md e IMPACTO-1.30.0.md.

## Orientação de implantação

Usar instalação nova ou atualização da 1.29.0. Fazer backup conjunto de banco/arquivos e observar o protocolo de recuperação já documentado. Instalar o ZIP instalador, conferir a versão e `f3base/saude-ler`, finalizar pendências pelo executor existente e atualizar o catálogo de abilities do agente. A documentação instalada está em `docs/` e é lida por `f3base/documentacao-ler`.

A atualização não publica teste Slack, não limpa mensagens automaticamente, não reenvia conversões históricas e não altera código dos companheiros ou temas. A política de publicidade pré-autorizada é a decisão implementada no plano: negativas explícitas têm prioridade; medição permanece independente. Homologar ações externas com um aviso de teste autorizado e registrado, usando as novas abilities, antes de operar mensagens reais.
