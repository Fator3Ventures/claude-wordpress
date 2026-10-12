# Site Core 1.31.0

Contrato Core 6.7.0. Base de implantação: WordPress novo ou Core 1.30.0. Não existe trava de versão de origem. Matriz conferida com MCP 0.21.0 e MCP Google 0.8.4; os contratos de integração continuam sendo verificados, sem usar quantidade de abilities como requisito.

## Entrega e rastreabilidade

| Pedido | Comportamento nesta release |
|---|---|
| Cron C131-02 a C131-04 | Confirma a intenção completa na agenda persistida e na leitura efetiva, restringe o diagnóstico aos hooks conhecidos do Core, preserva tentativas/recuo por intenção e invalida retomada com configuração substituída ou tarefa desligada. |
| 194 | Métodos Slack de leitura usam GET com query; normalização rich_text automática não representa edição humana. Exclusão da raiz de teste pode prosseguir com leitura pontual e autoria comprovadas mesmo quando a leitura de thread falha; informa cobertura e timestamps restantes conhecidos. |
| 195 | Ajuda por campo e por estrutura JSON com efeito, padrão e vazio. Corrige mensagem WhatsApp vazia, entrega do índice, retenções, bloqueio de listagem e `historico_sem_decisao=negar`. |
| 196 | Referências geradas do catálogo, inventário, tabelas instaladas e fonte dos eventos. Perfil atual `piso-padrao-3.5` confere os dez destinos de teste. A versão 3.4 permanece histórica. |
| 197 | A marca de teste é fixada por navegação. Remover o cookie não transforma o tempo acumulado e a saída da página anterior em audiência normal nem abre outra sessão nessa página. |
| 198 | Oito recortes iniciais; até duas consultas compartilhadas entre retentativas e testes manuais. Falha HTTP continua contando no teto de dez, mas pode ser repetida no mesmo dia após cinco minutos. Não inicia consulta com menos de 25 segundos úteis. O resumo conta recortes com e sem resposta. |
| 199 | Eventos `f3base_form_aberto`, `iniciado`, `recusado`, `enviado` e `fechado` na base de eventos e GA4, respeitando consentimento e política de teste. Detalhe contém somente ID/código; nunca valor digitado. O relatório agrega o funil por formulário. Gatilho interceptado não conta como saída para WhatsApp. |
| 200 | O endpoint público sem cache resolve `X-F3Base-Teste: 1` para o navegador antes da coleta. O agente deve aplicar o cabeçalho a todas as requisições do mesmo site, inclusive fetch/beacon, ou usar o cookie. |
| 201 | Mapa da plataforma/conta traduz ID de campanha antes da projeção para CRM e relatório; preserva nome/ID original e procedência da tradução. |
| 202 | Superfície Meta + meio pago identifica `meta_ads`, com procedência explícita de inferência. Nome de anúncio vazio usa seu ID, inclusive no lead nativo. |
| 203 | O novo lead Pipedrive recebe `organization_id` da pessoa confirmada por leitura; contempla pessoa nova ou existente. O vínculo enviado também é conferido na releitura do lead. |
| 204 | Título e nota nativos usam o nome conhecido do formulário, com ID entre parênteses. Sem catálogo disponível, a ausência do nome fica explícita. |
| 205 | Importação nativa não herda classificação de editor nem cookie/cabeçalho do operador. Marca de teste nativa deriva do payload da plataforma. |
| 206 | Formulário selecionado fora das páginas autorizadas é registrado por ID, sem impedir a leitura dos seguintes. Sucesso parcial não avança a cobertura completa; o alerta operacional contém os IDs problemáticos. |
| 207 | Atraso considera intervalo mediano das passagens CLI observadas; usa tolerância de 20% ou cinco minutos, mínimo 15 minutos. Erro real continua exigindo atenção imediatamente. Sem amostra suficiente, informa que usa a cadência solicitada. |
| 208 | Em Meta Ads, `utm_content`/`utm_term` numéricos preenchem anúncio/grupo sem exigir `f3_ads_v`. O contrato existente chama conjunto de `grupo_id`; não há uma segunda dimensão concorrente. Nome mapeado tem precedência sobre o ID no CRM. |

## Uso por agentes

Leia `docs/AJUDA-OPCOES.md`, `docs/dados/configuracao-schema.json`, `docs/DICIONARIO-DADOS.md`, `docs/dados/contrato.json`, `dados/contrato-de-nomes.tsv` e `dados/eventos-comportamento.tsv`. São instalados junto ao plugin e acessíveis pela leitura autorizada do canal e por `f3base/documentacao-ler`.

Os eventos de formulário têm detalhe `id-do-formulario:codigo-do-motivo` quando houver código e apenas o ID nos demais. Aberto é contado uma vez por instância de envio. Iniciado exige campo não vazio; o honeypot não dispara início. Fechado significa encerramento observado sem aceite, não prova desistência definitiva. Um diálogo fechado e reaberto pode terminar enviado; ambas as etapas são preservadas. Adaptadores de diálogo customizados devem chamar `window.f3baseFormularios.fechar(form)` ao fechar; diálogos HTML nativos são observados automaticamente. O fluxo de aceite só emite enviado após confirmação do servidor.

A atribuição inferida não é prova de entrega do anúncio pela plataforma. Os identificadores explícitos continuam prevalecendo; tráfego orgânico e contas diferentes não recebem mapa de campanha alheio. Mudanças de mapeamento não reescrevem notas antigas já entregues; a projeção atual e os valores preservados permitem auditoria.

O alerta operacional de captação não possui um switch separado: acompanha `f3base_anuncios_meta.ativo`, com entrega pelo canal em `f3base_avisos` e contingência pelos destinatários internos de `f3base_contato.email_leads`. Nenhum bot deve alterar esses destinos durante um teste real sem autorização.

## Atualização e limites

A atualização estrutural mantém os registros e amplia `detalhe` para 160 caracteres nas tabelas de comportamento/eventos, para comportar ID de formulário e código. Complementação de padrões preserva procedência e listas vazias. O pacote não converte dados dos outros plugins.

O teto Clarity é por projeto, compartilhado com consumidores externos. Retentativa melhora cobertura, mas não garante resposta do fornecedor. A janela de três dias e o comportamento na frota precisam ser observados depois da implantação pelo dono. A cadência CLI observada não prova o conteúdo do crontab.

Leia `docs/CRON-DIAGNOSTICO-1.31.md` e `docs/IMPACTO-1.31.0.md`. A validação usa WordPress e banco reais locais, com APIs remotas simuladas; não representa publicação nem homologação de contas reais.

---

# Validação — Site Core 1.31.0

Concluída em 12/10/2026. WordPress 7.1.2, PHP 8.3.6, MySQL 8.0.46 e Chromium 138; instalação local descartável, dados sintéticos, APIs externas simuladas ou bloqueadas. Nenhum site da frota foi alterado. Não houve teste em korvena.net.br.

**546 verificações aprovadas**, mais lint dos 197 arquivos PHP do plugin. O resumo legível por máquina e os testes acompanham o ZIP de fontes. A contagem corresponde a asserções executadas, não a requisitos distintos.

| Grupo | Verificações |
|---|---:|
| browser-banco-1310 | 10 |
| cron-1310 | 17 |
| pedidos-1310 | 25 |
| integracoes-1310 | 17 |
| crm-1310 | 6 |
| slack-manutencao | 44 |
| slack-app | 16 |
| publicidade | 25 |
| complementos | 12 |
| comunicacao | 82 |
| historico | 27 |
| avisos | 30 |
| qualidade | 18 |
| crm-complemento | 8 |
| operacao-1290 | 16 |
| diagnostico-1290 | 6 |
| telas | 9 |
| funcional | 28 |
| novidades | 27 |
| webhook | 29 |
| browser-1310 | 9 |
| cron-falhas-1310 | 4 |
| cron-nativo-1310 | 3 |
| operacao | 18 |
| estatica-1310 | 8 |
| instalacao-nova | 5 |
| atualizacao-1300-1310 | 11 |
| google-sdk | 20 |
| companheiros-reais | 16 |

## Evidência relevante

- Navegador com minificados e endpoints WordPress reais: cinco eventos do formulário observados no GA4 simulado e gravados em `f3base_eventos`; ID/código corretos; nenhum falso link externo WhatsApp antes da conversa. Visita só com cabeçalho marcada corretamente. Remoção do cookie preserva sessão e marca da saída; consulta SQL confirma somente `teste` nas duas sessões verificadas.
- Clarity: primeira tentativa retorna timeout; o mesmo recorte é repetido e os oito terminam respondidos no mesmo dia, em nove chamadas contabilizadas. Passagem curta não inicia HTTP. Limite total, reserva compartilhada, 429 e espera preservados.
- Pipedrive: fluxo completo simulado cria organização/pessoa/lead; pessoa já existente fornece sua organização. `organization_id` enviado e relido em ambos. Projeção de campanha/parceiro/canal/anúncio cobre valores vazios e leads nativos.
- Captação: formulário inválido no meio da lista não impede o posterior; problema e alerta têm ID; cobertura completa anterior é preservada. Cron CLI horário não gera alerta no intervalo normal; passagem perdida e erro geram estados distintos.
- Slack: leitura por query, normalização rich_text, thread paginada, autoria, idempotência, limites, timeout e exclusão da raiz com thread indisponível. Mensagens humanas e de produção preservadas.
- Cron: intervalo, argumentos e grade; divergência SQL/leitura efetiva; SQL real recusado; diagnóstico não persistido; limite de tentativas; leitura sem reparo; nenhuma mutação de hook estranho. Entrada real `wp-cron.php` com falha injetada registra o erro e executa um callback. Dois processos concorrentes executam uma única ocorrência.
- Companheiros reais: duas ordens de carregamento, registro SDK, conexão não padrão, consulta GSC com HTTP simulado, restrições e pausa/retomada independentes. A consulta SDK não fabrica passagem cron nem usuário humano.
- Instalação nova e atualização **1.30.0 → 1.31.0** por `plugins/upload-base64` do MCP 0.21.0. Primeiro GET bem-sucedido, tags e captura disponíveis antes da finalização; opções, listas vazias e procedência preservadas. A composição usa apenas tema sintético local.
- Referências geradas: 54 tabelas, 17 eventos declarados, dez destinos de teste no perfil 3.5, catálogo completo de opções e nomes. Nove pares fonte/minificado com hashes conferidos.

## Limites da validação

Entrega real em Slack/Pipedrive/Meta/Google/Clarity não foi realizada. A prova de contas, permissões e recebimento nas plataformas, bem como os períodos de observação na frota, permanece com a implantação. As falhas de banco são injetadas deliberadamente e geram erros esperados no log do laboratório; não são apresentadas como falhas espontâneas do pacote.

A execução não amplia o escopo para tema ou implantador, nem altera os plugins MCP e MCP Google. Veja `IMPACTO-1.31.0.md` para o encaminhamento. Runtimes, banco, cookies, tokens de laboratório, logs intermediários e screenshots não integram os arquivos distribuídos.

## Instalador

`base-site-core-fator3-1.31.0-instalador.zip`, 1.857.577 bytes, SHA-256 `bd84d4d9f06d4ecda6340a483b04c5b39e386ab528b5d29a8803a266ffe0d6a8` (calculado pela frota em 12/10/2026 sobre o ZIP entregue; os 375 arquivos conferem com `manifesto-core-1.31.0.json` do pacote fonte, SHA-256 do fonte `d6eedfba9a6d8ab3d5ca922e25a93ab2ec24ad207fabb9b38536320f601efe95`).
