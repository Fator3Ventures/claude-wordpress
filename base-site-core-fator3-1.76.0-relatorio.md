# Entrega — Fator3 Site Core 1.76.0

Revisão 1 · 09/11/2026 · Implementação e homologação dos Pedidos core 383–385  
Slug `base-site-core-fator3` · Contrato administrativo 8.37.0  
**Estado da entrega — com-pendencias de aceite externo para os pedidos 383 e 384.** O Site-Teste executa a 1.76.0. O pedido 385 passou pela prévia instalada de retorno CRM em homologação.

## 1. De onde esta versão entra

Instalação limpa ou atualização direta da 1.75.1 para a 1.76.0. Recuperei a aba de pedidos de 09/11 às 18:42 UTC e o relato de progresso da conversa original. O artefato integral recuperado foi o fonte 1.75.1. Reconstruí as mudanças da rodada a partir desse fonte e validei novamente os três pedidos. A base conferida tinha instalador SHA-256 `9fff30dc9b75a60fc193373c4366659bf6db13c35025f677b5f46e8988181dc6` e fonte SHA-256 `ebc04d4f325d2f76dc9680935b32d268cff149dba4ff6788ed887eca73ba6f6a`.

Mínimos do projeto e dos cabeçalhos de instalação — WordPress 7.1.4 e PHP 8.3 de 64 bits, instalação única. O laboratório executou WordPress 7.1.4, PHP 8.3.6 e MySQL 8.0.46. O Site-Teste confirmou WordPress 7.1.4 e PHP 8.3.36. Foram lidos integralmente `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos na revisão 5 de 02/11/2026, e consultada a regra comum de entrega de 16/10.

## 2. Convivência e encaminhamentos

Somente o Core precisou de troca. O inventário do Site-Teste confirmou MCP 0.41.0, Google 0.31.0, Meta 0.21.0, LinkedIn 0.19.0 e Pipedrive 0.8.0 ativos. O teste de implantação usou o MCP real. O teste comercial exercitou a lógica do Core com um adaptador local que anuncia uma ação CRM pronta e falha caso receba tentativa de envio. Permanecem vigentes as capacidades e os requisitos do contrato de entrega de conversão 1.2.0 dos produtores.

A análise das fronteiras compreendeu transporte MCP, Meta CAPI do Core, adaptadores comerciais Google e LinkedIn, etapas do Pipedrive e instalação pelo Implantador. Os três defeitos foram corrigidos dentro do Core. Nenhuma nova solicitação técnica a outro pacote. O impacto histórico 379 no Implantador pertence à rodada 1.75.1.

## 3. Mudanças e evidência

| Pedido | Defeito e mudança | Prova |
|---|---|---|
| **Pedidos core 383** | O script suprimia a captura de toda sessão marcada. O transporte agora capta PageView e Lead de teste para os eventos habilitados em Ambos ou Servidor, quando a política CAPI é marcar e há código válido. O evento guarda a classe no momento da captura e o retry a reconfere. O teste usa identidade de página própria, sem observar um disparo de Pixel. A política é reavaliada no endpoint e o código é acrescentado no worker. | Chromium verificou o script minificado com PageView e Lead, tráfego comum, código ausente, modo navegador e recusa. No WordPress isolado, a captura e o worker produziram um POST de PageView de teste e um de Lead de teste com código, além do PageView comum sem código. O HTTP interceptado retornou 200 e events_received=1. A fila registrou entregue e a repetição do despacho concluído não gerou novo POST. |
| **Pedidos core 384** | O worker tratava a falta de um cadastro de lead como negativa para todo PageView. A reserva agora relê a referência da navegação. Em modo granular exige ambas as categorias, recibo vigente e política correspondente. Em modo legado distingue aceite explícito, política pré-autorizada, falta de decisão e negativa registrada. O rodapé bloqueia novas capturas e comunica ao servidor a revogação de referências legadas novas. A fila reavalia as suspensões da 1.75.1 ainda elegíveis. | PageView pré-aprovado terminou entregue com HTTP 200 simulado. Negar após a captura e antes do worker devolveu negativa_explicita, e a nova captura com cookie denied recebeu HTTP 403. Foram exercitados recibo granular revogado, categoria recusada, política alterada, expiração, referência perdida, política que exige decisão e retomada de linha antiga sem HTTP iniciado. |
| **Pedidos core 385** | O Core exigia um retrato de consentimento do site inclusive para o lead nativo, cuja normalização grava publicidade e origem. O retorno ao Google Ads e ao LinkedIn usa F3Base_Publicidade::resolver, identifica o nativo por método e origem e continua exigindo o retrato nos leads do site. A prévia aceita o nativo de teste e a operação de entrega conserva a supressão. | No Site-Teste, a bancada normalizou dois formulários Meta sintéticos, gravou os contatos dentro de uma transação e chamou a prévia real para a etapa. LinkedIn devolveu elegivel e consentimento_nao_permite. Ambos retornaram envio_realizado=false. O descarte da transação foi confirmado por nova leitura. A matriz adicional cobriu três origens, dois destinos, política estrita, negativa, teste e retrato de site. |

O código vigente está em `assets/f3base-meta-transporte.js`, `assets/f3base-consentimento.js`, `includes/class-f3base-meta-transporte.php`, `includes/class-f3base-capi-fila.php`, `includes/class-f3base-consentimento-decisoes.php` e `includes/class-f3base-qualidade-destinos.php`. Os perfis minificados, a documentação e os metadados do contrato acompanham o runtime.

## 4. Instalação e prova da troca

O instalador foi fechado e transferido em 17 partes para o Site-Teste. O servidor confirmou tamanho e SHA-256 antes da operação `plugins/upload-base64`, com origem `zip_path`, sobrescrita, ativação, `expected_slug=base-site-core-fator3` e o hash da seção 8. A operação `905f5c62036832bd534314043f4a7e32` confirmou 1.75.1 → 1.76.0 e ativação em novo PHP. Pré-imagem `02eca5f543ae6432bbd80626`.

| Ambiente | Resultado |
|---|---|
| WordPress limpo e migração direta | **69 verificações dos pedidos em cada caminho.** Na migração, 993 amostras e a configuração semeada conservaram suas assinaturas. A reativação restaurou 33 estruturas e a sonda registrou zero leituras prematuras. |
| Navegador | **16 verificações** em Chromium Headless Shell 156.0.8078.79, executando os assets entregues em uma origem HTTPS interceptada. Inclui confirmação da revogação e supressão após recusa. |
| Build | Terser 5.44.1 reproduziu os 84 arquivos JavaScript. O catálogo PHP e as 84 saídas eram idênticos byte a byte à compilação final. PHP 8.3.6 aprovou a sintaxe de 597 arquivos, 57 JSON foram analisados e 945 arquivos do instalador corresponderam ao runtime do fonte. |
| Site-Teste | **44 verificações da bancada CRM.** Duas prévias de formulários nativos normalizados e 42 verificações da matriz sintética de preparação. Perfil de ação da etapa e configuração de destino restritos à requisição de teste. O executor confirmou atualização concluída, cabeçalhos, navegação e etapa Pipedrive. Saúde positiva e sondas novas da home e do login com HTTP 200. |
| Documentação e arquivos | Descoberta de `f3base/documentacao-ler`, leitura do índice, 23 linhas de `docs/RELEASE-1.76.0.md` e 5 de `docs/AGENTES-1.76.0.md`, ambos até o fim. Caminho fora do catálogo recusado. Dois hashes documentais e oito de código/assets no site iguais ao pacote. |

As provas reproduzíveis estão em `tests/` e os resultados sanitizados em `evidence/1760/`. O host confirmou a ausência do PHP temporário da bancada e do ZIP de transferência. O mecanismo de escrita do MCP mantém backups administrativos de arquivo. A produção e o repositório público não fizeram parte da implantação. Na distribuição futura pela frota, conferir o instalador servido na raiz raw de Fator3Ventures/claude-wordpress contra a seção 8 antes de usar `plugins/upload`.

## 5. Banco, migração e correção por nova versão

A 1.76.0 utiliza as colunas existentes de referência e versão de política da fila CAPI e a tabela existente de decisões. Em modo legado, o servidor recebe um comprovante primário do navegador, guarda um hash na fila e registra a revogação por até oito dias antes da elegibilidade para expurgo. O worker consulta a negativa na transação de início de HTTP. Se o rodapé não conseguir confirmar a revogação, o navegador guarda a pendência e a retoma em navegação posterior. A negativa local bloqueia a captura imediatamente.

A retomada das suspensões antigas exige mesmo dataset, token, prazo vigente, payload, zero tentativas e ausência de cancelamento. O registro de entrega conserva seu event_id. Uma vez iniciada a requisição externa, o resultado deve ser conciliado antes de qualquer repetição. A instalação preserva as configurações e os contatos. A correção de versão instalada é feita por nova release. O banco e os salts ficam sob o backup operacional de dados.

## 6. Pendências e responsáveis

- **Growth e frota, pedido 383.** O Site-Teste informou ausência de token CAPI. Confirmar na Korvena, após implantação autorizada, o mesmo event_id no recibo do Core e na aba Eventos de teste do dataset configurado. O HTTP 200 da bancada foi produzido por um serviço simulado.
- **Growth e frota, pedido 384.** Correlacionar um PageView de tráfego real com o recibo entregue/HTTP 200 da Meta após a implantação na Korvena. Verificar separadamente um navegador que recusou o consentimento. A prova local cobre o bloqueio antes de um novo envio. Linhas antigas sem referência individual só permitem reavaliar a política registrada na captura. Uma revogação posterior daquele visitante não pode ser atribuída retroativamente a essas linhas pelos dados da 1.75.1.
- **Operação, pedido 385.** Aceite da prévia concluído no Site-Teste. Contas Google Ads e LinkedIn reais, seus mapeamentos e entrega comercial dependem da configuração e habilitação do respectivo produtor. A bancada comprova o preparo do Core, sem enviar conversões aos fornecedores.

## 7. Credenciais e configuração do dono

Para CAPI, conferir o token de acesso e o Pixel/dataset do servidor, o modo de transporte e a lista de eventos. Para uma sessão marcada, configurar o destino CAPI como marcar e o código de Eventos de teste do mesmo dataset. A liberação de Servidor continua sujeita às provas de homologação já exigidas pelo Core. A prévia CRM exige as capacidades administrativas de configuração e leitura de leads, uma ação comercial exclusiva por etapa, um destino ativo e um adaptador pronto. A rodada não exige cadastrar segredo novo no ambiente produtivo.

## 8. Identidade dos arquivos

| Artefato | Arquivo | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [base-site-core-fator3-1.76.0-instalador.zip](base-site-core-fator3-1.76.0-instalador.zip) | 4.381.465 | `d830b488509814f44f4d78109cf8669e6b09717d9cbc50a0b42a1545f4a5f3ea` |
| Fonte | [base-site-core-fator3-1.76.0-fonte.zip](base-site-core-fator3-1.76.0-fonte.zip) | 13.992.465 | `b15aa3ee61fa0a035e92d9a869f98ff470992de50c92462e375a5199fcfd5de7` |

Relatório externo canônico. A cópia incluída no fonte antecede o fechamento do ZIP.

Checklist de encerramento da seção 14 conferido. A implantação na Korvena e os dois recibos externos descritos na seção 6 permanecem pendentes.
