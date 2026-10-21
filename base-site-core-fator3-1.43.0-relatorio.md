# Fator3 Site Core 1.43.0 — relatório de implementação

Data: 21/10/2026. Base fechada: **1.42.0**. Contrato administrativo: **8.8.0**. Implementação e pacotes produzidos; **não instalado na frota e não publicado em repositório**. Aceite em contas reais continua pendente.

## Escopo entregue

Os pedidos 243–255 do arquivo “Fator3 Site Core(20261021-044849).md” orientaram esta versão. A dependência recebida do MCP Google 0.16.0 foi incorporada no Core, sem esperar nova resposta e sem criar outro relatório de impacto obrigatório.

| Pedido | Alteração e evidência | Limite de aceite |
|---|---|---|
| 243 | Marcador de migração com tipo textual; cadência continua após falha isolada e registra a opção. Auditoria dos tipos padrão. | Validado no WordPress local. |
| 244, 247 | Cartão do e-mail; senha identificada com usuário SMTP; conta, conteúdo e homologação; frases e variáveis editáveis; serviços por nome; prévia sintética; testes de conexão e envio separados. WhatsApp vazio herda Contato. | Testes reais de autenticação, caixa final e entrega comercial não executados. |
| 245 | Pipedrive omite `note` vazia. Núcleo confirmado não é recriado ao tratar atividade; regressão de reaplicação sem duplicação. | API remota simulada; verificar o caso real que motivou o pedido. |
| 246 | Controles estruturados, rótulos, ajuda, estados, datas/horas, barra de salvar e aviso de alterações. Textos do e-mail, consentimento e formulário editáveis; confirmação, avisos e resumo da equipe com campos e prévia. Rótulos e descrições de SEO, destinos de teste e segredos LinkedIn revisados. | Revisão ampla implementada, mas não se declara inspeção manual de cada texto de todas as páginas. A revisão integral de copy e de todos os textos públicos permanece parcial. |
| 248 | Catálogo v2 preserva `field_name`; geração anterior de catálogo descartada; mapas, alternativas e atividades com controles; token na conexão; tipo legado fora da tela. | Nomes novos exigem atualizar o catálogo. Mapas sem catálogo conservam o valor salvo e pedem revisão. |
| 249 | Seções de conexão/importação/mapeamento/estado; listas Meta, Google e LinkedIn com cliente Core; webhook copiável; mapeamentos em linhas. | Descoberta completa de ativos no cliente externo Plugin LinkedIn não está implementada: o contrato consumido limita-se a formulários concedidos/identificados. Não há troca automática de cliente. |
| 250 | Eventos Meta em seletor; rótulos nos controles; funis/etapas por catálogo e formulários/campanhas por dados locais disponíveis; token em uma área. | Catálogos reais e regras comerciais precisam de homologação. |
| 251 | Filas em Operação, 20 linhas; ações e diário por registro; detalhes Slack carregados somente quando abertos. Avisos com menos de 30 controles visíveis, destinatários e transporte condicional; canais Slack por nome. | Tempo medido localmente; não é prova do tempo na hospedagem. |
| 252 | Credenciais por assunto, estado/data, exclusão explícita; resumo complementar sem campos de segredo duplicados. | Teste de credencial usa os verificadores existentes; não comprova toda a operação remota. |
| 253 | Menu Site Core, cartões, retirada do quadro de medição, redirects e verificação de domínio em SEO, retenção e homologação centralizadas, destinatários em Avisos, seleção de blocos e minutos, estado Google e link de configuração. | A navegação foi verificada em HTML nativo renderizado e no Chromium; falta aceite administrativo na hospedagem. |
| 254 | Mensagens com rótulo/prévia; grupos de campos por caixas de seleção; número WhatsApp próprio só mediante escolha. O JSON de definição fica oculto no transporte. | Referências técnicas necessárias, como material protegido e conexão externa, ainda usam identificadores em seus fluxos específicos. |
| 255 | Comparação sem audiência retida retorna nulo/motivo; pré-estimativa rejeita custo excessivo; GSC explicita ausência de comparação; cron renova redes vencidas e relatório mostra data da fonte. | Histórico não é reclassificado. Lista indisponível não é inventada nem declarada válida. |

## MCP Google 0.16.0

O Core consome `site-conversion-delivery/1.0.0` e a extensão `site-conversion-reconcile/1.0.0`. O executor consulta recibos `incerto` por `reconcileBound`, sob trava e com referência de destino fixada. Confirmação posterior não repete `events:ingest`. Rejeição só se torna final com prova de não entrega.

O instalador do Google recebido tem SHA-256 `e0dfee63fbd9ad9fcc6b5ab9a3b9d492d7e497822154e0572589a45f3116248c`; a dependência recebida, `9f4542b810b6b9817312beb236c782507a8bd589f182f19d83adbb525f630822`. O fonte inclui a cópia do plugin Google utilizada na prova. O instalador Core não instala, modifica ou redistribui o Google como plugin embutido.

O Google 0.16.0 lê o ID de medição GA4 do Core e renova suas verificações. A tela Core consulta prontidão e oferece o link do segredo, sem campo duplicado. Não é necessária nova alteração de contrato a repassar ao Google para estas correções.

## Verificações executadas

**458 asserções/verificações locais aprovadas**, além de dois ciclos de instalação nativa:

| Suíte | Verificações | Ambiente |
|---|---:|---|
| Configuração, tipos, cadência, texto e relatórios | 154 | WordPress/MySQL; dados sintéticos |
| Renderização de configurações | 86 | HTML produzido pelo PHP do WordPress |
| Custo da consulta | 5 | 8.001 contatos sintéticos; inclui período anterior |
| Google 0.16.0 | 52 | Core e Google reais, HTTP simulado |
| Fluxos Pipedrive | 46 | CRM simulado; novo/existente, resposta perdida, complemento e nota vazia |
| Documentação e confinamento da leitura | 69 | Serviço nativo de documentação |
| Configurações no navegador | 20 | Chromium 153, HTML nativo e CSS isolado |
| Editor de formulário | 6 | PHP e Chromium; seleção de campos e herança de WhatsApp |
| Textos de confirmação e avisos | 12 | Gravação, HTML/texto, Slack e confirmação nativa |
| Filas | 8 | 20 linhas e detalhes sob demanda |

Sintaxe: **222 arquivos PHP** aprovados em PHP 8.3.6. WordPress 7.1.3. Assets alterados minificados com Terser 5.44.1. Não foram enviados e-mails, mensagens ou conversões a provedores reais nestes testes.

A pré-estimativa com 8.001 contatos respondeu em 0.0065 s. Renderização local das filas: Avisos 0.0032 s; Pipedrive 0.0053 s. Esses tempos não extrapolam para volume ou infraestrutura de produção.

Instalação limpa e atualização direta **1.42.0 → 1.43.0** usam `Plugin_Upgrader`, migração, finalização e repetição sem novo efeito. Preservados contatos, escolhas explícitas/vazias, autoria, segredos, cursores, callback e entregas incertas. Os novos textos padrão complementam a configuração de Contato com revisão e evento próprios, preservando os valores anteriores e a autoria; a prova também conserva um texto personalizado já existente. O atraso de finalização foi acelerado apenas no estado descartável. O arquivo `native-cycles-143.json` vincula a prova ao SHA-256 do instalador entregue.

## Pacotes

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| base-site-core-fator3-1.43.0-instalador.zip | 2091980 | `5a7c02abb97f7161617ddfd8e4d28faf2fdb22e4ae5d4ed75416dc68d76ee9e7` |
| base-site-core-fator3-1.43.0-fonte.zip | 2968306 | `04a1fb6196327aa32418630905088c5a366067c971472cf00510876e737db3fd` |

Instale somente o ZIP **instalador**. O fonte contém runtime, build, testes e evidências; não é um instalador. A base 1.42.0 permanece intacta, SHA-256 `280f54f8afb58301fb686a659003d432195c62dbfb5b52d055a022335cf3aeac`.

## Antes de promover para a frota

Homologar no Site-Teste com MCP Google 0.16.0 e contas autorizadas: confirmação Ads posterior sem repetição; atualização do catálogo Pipedrive e atividade que antes falhava; conexão e envio SMTP a caixa controlada; seleção e gravação de ativos; comparação sem audiência; renovação Perplexity; tempo real das filas. Esses atos externos não foram executados nesta entrega.

Pendências funcionais explícitas: revisão exaustiva de todos os textos públicos/configurações (246) e descoberta administrativa completa no cliente externo Plugin LinkedIn (parte de 249). A versão não declara esses dois aceites concluídos.
