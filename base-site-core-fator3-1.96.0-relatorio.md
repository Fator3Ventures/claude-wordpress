# Entrega — Fator3 Site Core 1.96.0

**Implementado e homologado no Site-Teste.** O executor confirmou o Core 1.96.0 em 19/11/2026 às **00h01min11s de Brasília**, com 20 etapas e zero falhas. O pedido Core 431 corrige avisos permanentes em provas de conversão com renovação em dia. Os pedidos Google 57 e 58 alinham o Core à prova Ads sem vencimento e à retomada de conversões vinculadas.

## 1. Origem e requisitos

Instalação limpa ou atualização direta do Core oficial 1.95.0. A instalação usa um único ZIP. O instalador de base tem 5.671.022 bytes e SHA-256 `6971df93ecf39e14e584e0fc3dc802aee77ab4f2d58eb5b8ce35d6a503a4c21c`. O fonte de partida tem SHA-256 `3f05a234fa5edf844ced5bb79bc1b79116cab39186ce7954bb78ab819903d638`.

Requisitos de execução: WordPress 7.1.4 ou superior, instalação única e PHP de 64 bits a partir de 8.3. A bancada utilizou WordPress 7.1.4, PHP 8.3.6 e 8.4.27 e MariaDB. O Site-Teste informou WordPress 7.1.5 e PHP 8.3.36. As fontes do projeto continham `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, revisão 5 de 02/11/2026. Foram conferidos os dois documentos, a regra comum, a aba do Core, o pedido 431 e os relatórios dos pacotes entregues.

## 2. Configuração e convivência

Contrato administrativo `8.45.0`, perfil `piso-padrao-3.6`, 104 opções operáveis e 199 operações de domínio. A regra nova é calculada a partir dos dados da prova existente. A opção de antecedência continua aplicável a credenciais e à Graph API. Sua descrição explica a regra específica das provas de conversão. A atualização preserva os nomes e os schemas de entrada das operações.

| Pacote | Bancada e Site-Teste ao concluir | Abrangência verificada |
|---|---|---|
| Site Core | 1.96.0 | Instalação, migração, projeção administrativa, coleta e duas filas |
| MCP | 0.51.0 | Operações administrativas de leitura, troca por hash, documentação paginada e saúde do canal |
| Google | 0.39.0 | Prazo e renovação de prova, aquisição, etapas, erros transitórios e recibos, com respostas externas simuladas |
| Meta | 0.29.0 | Worker e coletor do incidente de agenda |
| LinkedIn | 0.26.0 | Deduplicação e recuperação de aviso pelo produtor |
| Pipedrive | 0.12.0 | Seleção do registro na projeção de incidentes do pacote |

Os seis runtimes da bancada coincidiram arquivo por arquivo com os instaladores oficiais. No Site-Teste, o MCP 0.51.0 já estava ativo. O Core foi atualizado e em seguida foi aplicado o instalador oficial do Google 0.39.0 em substituição à 0.38.0. Na conexão consultada, a entrega de conversões estava desligada antes e depois da troca. O ensaio das filas com eventos e dados pessoais fictícios ficou na bancada.

## 3. Pedidos atendidos

| Pedido | Alteração e prova |
|---|---|
| **Core 431, prazo de prova** | A antecedência usa o último quarto da duração observada e respeita a renovação normal prevista pelo produtor. Na prova GA4 de 24 horas com renovação em 12 horas, a falha de renovação leva ao aviso seis horas antes do fim. Uma retentativa do fornecedor após falha não empurra esse limiar. A prova Ads sem vencimento encerra o aviso de prazo antigo. |
| **Core 431, registros anteriores** | A bancada reproduziu dois falsos positivos em Core 1.95.0 e atualizou o mesmo banco. Na primeira coleta pelo Core 1.96.0, os dois registros passaram a recuperado com a mesma referência e uma mensagem de recuperação por destino. Com renovação em dia, 73 observações horárias representando 72 horas mantiveram os registros recuperados e geraram zero novos e-mails. |
| **Core 431, generalização** | Uma segunda conexão com quatro destinos comprovou o isolamento e o cálculo para durações de oito horas, 24 horas e 20 dias. Com renovação atrasada, houve abertura ainda antes do vencimento. A agenda normal tardia limitou a antecedência. Dados incompletos conservaram o episódio. Permaneceu um incidente separado para falha de renovação. Uma credencial com 13 dias de saldo ainda entrou no alerta de 14 dias. |
| **Google 57 e 58, aquisição Ads** | O Core conserva a transação e o destino em recusa conclusiva ou no código expresso de reenvio da mesma transação. Uma aquisição de 45 dias, já com nove tentativas, recebeu 503 simulado e retomou com o mesmo identificador. A autorização, a prontidão e o consentimento voltam a ser avaliados. Uma linha anterior com consentimento revogado foi cancelada antes do despacho. |
| **Google 58, etapas comerciais** | A fila pode retomar uma etapa Ads recusada após nova prova, com a mesma ação, referência, etapa, evento e revisão. A janela Ads foi ampliada de sete para até 90 dias, sujeita à idade do clique. A janela LinkedIn continua em sete dias. Uma etapa de 45 dias recuperou da recusa de termos. Nos ensaios negativos, mudança do destino e incerteza genérica impediram o reenvio. |

Na bancada, o ensaio do produtor oficial passou em **44 verificações no PHP 8.3.6**. Em PHP 8.4.27, as mesmas verificações e sete adicionais para estados antigos e limites passaram, totalizando **51**. As fixtures guardam as respostas de cada fase. A leitura do pacote MCP 0.51.0 confirmou que os pedidos MCP 87 e 88 pertencem ao canal e preservam o contrato consumido pelo Core. Os retornos de IAM e do quórum de registro da rodada anterior constam dos relatórios recebidos. As mudanças atuais dispensam adaptação do MCP, Meta, LinkedIn, Pipedrive ou Implantador.

Encaminhamento técnico de planejamento e entrega: [base-site-core-fator3-1.96.0-impacto-wp-mcp-google-fator3.md](base-site-core-fator3-1.96.0-impacto-wp-mcp-google-fator3.md). O fonte inclui a proposta do mantenedor, sua revisão inicial e os ensaios do código incorporado.

## 4. Instalação e prova da troca

| Verificação | Resultado |
|---|---|
| Bancada limpa e migração direta | Em dois bancos independentes, o executor concluiu as 20 etapas nas origens nova e 1.95.0, com zero falhas. A migração preservou os identificadores dos episódios já entregues. |
| Instalador | Raiz única `base-site-core-fator3/`, 1.280 arquivos conferidos no manifesto e 611 PHP aprovados em verificação sintática. O código de testes e os transportes simulados ficam no fonte. |
| Homologação no Site-Teste | Para o Core e para o Google, `plugins/upload-base64` usou `zip_path`, slug e SHA-256 esperados, pré-imagem e idempotência. A aplicação do Core limpou a pasta temporária de upgrade. O primeiro envio do Google usando aquele caminho encontrou o ZIP ausente. O inventário confirmou a versão antiga, o ZIP foi transferido de novo em outro caminho e o segundo envio aplicou a 0.39.0. As duas trocas concluídas devolveram HTTP 200 para a página inicial e /wp-json/ antes e depois. A conferência final encontrou os dois caminhos temporários ausentes. |
| Executor | `f3base/como-usar` com `compacto=true` retornou `versao_alvo=1.96.0`, `estado=concluida`, `falhas=0` e `confirmada_no_executor_em=1795057271`. A confirmação ocorreu cinco segundos após a abertura do ciclo. Uma leitura durante a instalação ainda indicava “em andamento”. A consulta completa e o inventário posterior confirmaram o conjunto ativo. |
| Documentação | O índice instalado incluiu a release. As 21 linhas da nota foram lidas em três páginas e coincidiram byte a byte com o ZIP, SHA-256 `9824c4b6fab75d0da6b8a90127894d4345f00bb86954b4dabdae1aea3794f685`. O guia de agentes foi lido integralmente. A consulta a documento fora do índice recebeu `documento_nao_catalogado`. A leitura administrativa do contrato confirmou o texto atualizado de `antecedencia_dias`. |
| Outros contratos e interface | A prova conjunta gerou cinco mensagens interceptadas para Google, LinkedIn e Pipedrive e recusou leitura ao visitante. Meta e cron passaram na prova dedicada. A aba Avisos foi aberta com sessão administrativa em 360, 768 e 1.440 px, sem excesso de largura no documento. Essa aba mostra avisos de novos contatos. O campo técnico de antecedência não foi encontrado nessa tela. O contrato administrativo permite consultar a regra. |

Na distribuição, a frota confere o hash dos bytes publicados no fluxo oficial e usa `plugins/upload` com `expected_slug=base-site-core-fator3` e o hash da seção 8. Para conferir os avisos do pedido 431, leia `f3base/incidentes-tecnicos-ler` e compare com as verificações e renovações por conexão no Google. O laboratório e o Site-Teste têm comprovantes separados em `evidence/1960/`.

## 5. Banco, dados e retomada

A atualização usa o schema existente. Não acrescenta tabelas, opções ou destinos. Os dois fluxos preservam as chaves históricas e as reservas de envio. Os casos de reenvio automático são definidos pelo resultado do Google. Se uma linha antiga já tiver perdido a causa original e conservar apenas o código genérico de limite esgotado, a operação requer conferência do histórico. A gravação da reserva antes do envio, a leitura de recibos pendentes e as verificações de elegibilidade continuam em vigor. O histórico de efeitos externos é preservado. Correções posteriores à instalação seguem em nova versão.

## 6. Limites e responsáveis

- **CTO Office e frota.** Na consulta de leitura desta rodada, o CTO Office ainda executava Core 1.95.0 com dois avisos Google `prova_vencendo` abertos e zero entregas pendentes nesses registros. O aceite de campo requer atualizar o site, verificar a primeira coleta e observar 72 horas reais sem reabertura enquanto as renovações estiverem em dia. A implantação da rodada foi restrita ao Site-Teste.
- **Responsáveis Google e e-mail.** A entrega e o recebimento em conta Ads, GA4 e caixa postal reais ficam para os destinos autorizados. O ensaio usou WordPress e banco reais, respostas Google simuladas e correio interceptado. A capacidade do Core de reenfileirar não garante aceitação comercial nem contabilização no relatório do fornecedor.
- **Estado final.** O MCP do Site-Teste indicou saúde positiva. A projeção dos três incidentes consultados conservou seus estados e contagens de fila após as trocas. Os três bancos sintéticos, suas identidades e as instalações locais desta rodada foram descartados após a coleta das evidências.

## 7. Credenciais e configuração

A versão reutiliza as autorizações existentes. Em `f3base/config-core-contrato-v1`, informe `nome=f3base_avisos_tecnicos` para consultar a descrição pública da regra. `antecedencia_dias` continua controlando credenciais e Graph. A margem de prova é calculada automaticamente a partir da verificação e da renovação do produtor. Não é preciso editar a antecedência dos 11 sites para eliminar o falso positivo.

## 8. Identidade dos arquivos

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| [base-site-core-fator3-1.96.0-instalador.zip](base-site-core-fator3-1.96.0-instalador.zip) | 5674742 | `dde2feadefdf08ab7973e7ea1be588b73709b723a088ef5549e43394aa7f73a5` |
| [base-site-core-fator3-1.96.0-fonte.zip](base-site-core-fator3-1.96.0-fonte.zip) | 8615195 | `632b51fe0124a1008474268f82e2edf4820305954221d2613c7e199ce2738afd` |

A cópia interna do relatório antecede o cálculo da identidade do próprio ZIP fonte. O relatório externo contém os dois hashes finais.
