# Entrega — Fator3 MCP Google 0.39.0

Revisão 1 · 2026-11-18T23:35:34-03:00 · Implementação dos **Pedidos MCP Google 57 e 58**  
Slug `wp-mcp-google-fator3` · Build determinístico identificado pelo SHA-256 da seção 8  
Status **com-pendencias**. O emissor foi implementado e testado. A ampliação do tratamento das filas depende de uma nova versão do Core. O aceite na frota e o reconhecimento de conversões por contas Google reais permanecem pendentes.

## 1. De onde esta versão entra

Instalação nova ou atualização direta do Fator3 MCP Google 0.38.0. O instalador de origem tem SHA-256 `1ddeb8ef6aa734a3f8c6a95baadd2c3b6256d84e4bbbdb55d781300b8f407e33` e o fonte de origem `c2653ba3331dd2de55249966e486b2dc6f1e968fed9f31d54e2057fcbfc60716`. A numeração segue o incremento minor do projeto. Foram preservados o basename `wp-mcp-google-fator3/wp-mcp-google-fator3.php`, o provider, as ferramentas públicas e as identidades de configuração e atualização.

Requisitos: WordPress 7.1.4 ou superior e PHP 8.3 ou superior. A instalação e a atualização nativas foram exercitadas em WordPress 7.1.4, PHP 8.3.6 e MariaDB 11.8.6. A integração experimental de fila também foi exercitada em PHP 8.4.27. Aplicaram-se `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos revisão 5 de 02/11/2026, além da regra comum, do padrão Google e do arquivo de pedidos 57 e 58.

## 2. Convivência e encaminhamentos

| Pacote | Versão usada na bancada | Verificação |
|---|---|---|
| Fator3 Site Core | 1.95.0 | Fonte, instalador, relatório e revisão 2 do retorno IAM recebidos. A fila oficial foi exercitada com o emissor novo. |
| Fator3 MCP | 0.50.0 | Acompanhante identificado na entrega Core e no Site-Teste. Instalador oficial disponível no projeto, SHA-256 `97f6c6a233c2210e24cdef205a66a41c95e20eca9ad8f3644e518bc8ed4ee95f`. Transporte HTTP autenticado exercitado. |
| MCP LinkedIn, Meta e Pipedrive | 0.26.0, 0.29.0 e 0.12.0 | Pacotes oficiais presentes na bancada e no inventário do Site-Teste. Arquivos instalados conferidos contra seus ZIPs. |
| Fator3 MCP Google | 0.39.0 | 311 habilidades, sendo 123 de leitura e 188 de escrita, e 46 definições de configuração. |

Contratos vigentes: configuração 4.0.0, catálogo 3.0.0, execução 2.0.0 e armazenamento 2.0.0. Contratos PHP de entrega preservados, incluindo `site-conversion-delivery/1.1.0` e a extensão comercial `1.2.0`. A capacidade publica novos dados de diagnóstico, de vigência da prova e de retentativa. A leitura administrativa e as verificações de autorização continuam obrigatórias.

**Impacto recebido e encerrado no desenvolvimento.** O Core 1.95.0 incorporou oficialmente o detalhamento IAM do pedido 56. A prova desta rodada verificou no Core oficial a permissão e o projeto no registro e no e-mail interceptado. O impacto recebido e o adendo histórico estão referenciados no fonte. O recebimento real de correio continua com a operação.

**Impacto emitido.** `wp-mcp-google-fator3-0.39.0-impacto-base-site-core-fator3.md`, revisão 2, desenvolvimento de contrato, **acao-necessaria**, aberto para o mantenedor do Core. O detalhe de expiração inteira das conversões otimizadas já funciona na 1.95.0. As filas precisam tratar os códigos Ads de retentativa, as recusas de etapas comerciais e o limite de 90 dias para essas etapas. A ordem de implantação coordenada é MCP 0.50.0, Core com a adaptação da fila e Google 0.39.0. As funções já cobertas pelo Core 1.95.0 estão na seção 3. Não foi identificada necessidade de mudança no transporte MCP, LinkedIn, Meta ou Pipedrive.

## 3. Mudanças e evidência

| Pedido | Regra entregue | Resultado observado |
|---|---|---|
| **Pedidos MCP Google 57** | O GA4 mantém a renovação após 12 horas. Timeout, erro de rede, 429, 5xx ou falha interna da verificação preservam a última prova positiva da mesma revisão. Depois das 24 horas, o estado é `stale_transient` e o diagnóstico informa o início do período. As retentativas continuam com espera progressiva até uma hora. | Na 0.38.0, reproduzimos o bloqueio por 503 após o vencimento. Na 0.39.0, envelhecemos a prova em 400 dias e repetimos a falha, com o período transitório datado 390 dias antes. A consulta de prontidão e o envio GA4 continuaram funcionando. O aviso `renovacao_falhou` apareceu no Core. |
| **Pedidos MCP Google 57** | Uma falha conclusiva invalida a prova na primeira constatação. Um novo sucesso é necessário para restabelecer o destino. A extensão exige prova positiva da mesma identidade, configuração e revisão. | Segredo ausente na listagem bloqueou o próximo envio. Outra falha transitória não recuperou essa prova. Uma verificação positiva restabeleceu a autorização e a agenda de 12 horas. A troca de fluxo invalidou a prontidão imediatamente. |
| **Pedidos MCP Google 58** | A prova de aquisição Ads e a prova de cada ação comercial passam a valer até mudança de revisão ou recusa conclusiva. A validade das conversões otimizadas segue a mesma ação. O executor pula provas Ads válidas. | Com o prazo legado vencido simulado e mais de 72 horas desde a prova, o executor verificou apenas GA4. O Ads retornou `valid_until_rejected`, próxima renovação nula e prontidão aceita por `F3Base_Google_Conversoes::pronta()` na 1.95.0. |
| **Pedidos MCP Google 58** | A recusa de ação, credencial, acesso ou termos no envio bloqueia a ação e abre aviso no Core. Nova prova habilita reapresentar a mesma transação. A duração da prova é independente da janela de idade do evento. | Ação inexistente reteve o registro no Core oficial. A reprovação dos termos de uma ação comercial bloqueou apenas essa ação. Uma nova prova permitiu enviar o mesmo evento. A segunda conexão exigiu prova própria. |
| **Pedidos MCP Google 58** | Falha temporária de envio conserva a prova. Quando a resposta deixa a entrega incerta, o resultado `ads_retry_same_transaction` distingue a retentativa admitida com a mesma ação e o mesmo identificador. Um recibo obtido é consultado até a confirmação. | Exercitados 429, 503 e timeout. Na cópia ajustada do Core, um 503 com nove tentativas anteriores preservou o registro e o contador. Uma etapa com 45 dias voltou a sair depois de nova prova. |

O destino e o consentimento continuam a ser conferidos antes do envio. Uma seleção ambígua de aquisição entre conexões continua bloqueada. As ações comerciais têm vínculo individual com sua conexão. O contrato `enhanced_leads` usa o marcador inteiro `253402300799` unicamente para compatibilidade com a verificação de prontidão do Core. O campo de validade da prova Ads principal é nulo.

## 4. Instalação e prova da troca

Instalar apenas o ZIP instalável da seção 8 no WordPress. Para atualização, substituir o mesmo slug. A instalação pela frota usa `plugins/upload` com `expected_slug=wp-mcp-google-fator3` e `expected_sha256` da seção 8, após conferir os bytes da URL raw publicada. Caminho previsto: `https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-google-fator3-0.39.0-instalador.zip`. Publicação pendente. O fonte segue separado conforme a decisão 89.

Em requisição MCP HTTP autenticada nova, `google/status` informou versão 0.39.0 e 311 habilidades, `google/integration-status` com `compact=true` retornou `read_success=true`, e `google/storage-status` informou `storage.ready=true`, tabelas de registros e cron disponíveis e contrato 2.0.0.

| Prova | Ambiente e resultado | Evidências em `evidence/039/` |
|---|---|---|
| Base e atualização | 5 verificações na base 0.38.0 e 31 na atualização direta pelo instalador WordPress. Bytes da credencial cifrada preservados. | `base.json`, `upgrade.json` |
| Instalação limpa | ZIP instalado em banco novo com o Google como único plugin ativo. 37 verificações de funções próprias, inclusive documentação local. | `isolated.json` |
| Core oficial | 38 verificações em PHP 8.3.6, incluindo a fila persistente de aquisição, bloqueio, nova prova e confirmação assíncrona. | `core-official.json` |
| Core experimental | 44 verificações em PHP 8.4.27 com o diff do impacto, incluindo falha transitória, janela comercial e retomada. Core oficial restaurado ao final. | `core-patch.json`, `package-parity.json` |
| Pedido 56 | 16 verificações em Google 0.39.0 com Core 1.95.0 original, incluindo detalhes do e-mail e uma única abertura. | `iam-core195.json` |
| Documentação no MCP | Em cada instalação, limpa e atualizada, o índice e os 26 documentos foram lidos integralmente em 90 páginas, com 120 verificações por instalação. A remontagem confirmou o hash de cada documento e a recusa de caminho arbitrário. | `docs-clean.json`, `docs-upgrade.json` |
| Regressão e build | 1.370 testes e 16.397 asserções em cada um dos PHP 8.3.6 e 8.4.27. Zero falhas e zero pulos no executor compatível. Sintaxe dos 206 arquivos PHP instalados aprovada em ambos os runtimes. | `unit.json`, `unit84.json`, `lint.json`, `docs-build.txt` |
| Interface e prontidão | Chromium leu a tela Conversões em 360, 768 e 1440 px com “Sem renovação periódica” para Ads. As seis pastas de plugins coincidiram com os instaladores. | `browser.json`, `readiness.json`, `installed.json`, `package-parity.json` |

**Estado final.** Na bancada, ambiente recriado com seis plugins oficiais ativos, zero credenciais Google, zero jobs e zero senhas de aplicação. O servidor HTTP de ensaio foi encerrado. O Site-Teste foi consultado com Google 0.38.0, Core 1.95.0, MCP 0.50.0, LinkedIn 0.26.0, Meta 0.29.0 e Pipedrive 0.12.0. Em CTOOffice a 0.38.0 informou GA4 e Ads prontos. Nos dois sites, a rodada fez apenas leituras. Os resultados sanitizados estão em `sites.json`.

## 5. Banco, migração e correção por nova versão

Os registros de provas e os recibos da Data Manager continuam nas estruturas existentes. Os novos resultados registram a natureza da falha, início de sequência transitória e geração de prova. A revalidação positiva cria uma nova geração e permite retomar uma recusa anterior para o mesmo destino. Recibos pendentes ou entregues continuam respeitados. A operação de envio usa a trava da conexão e persiste a intenção antes do HTTP.

O código interpreta os prazos e a revisão gravados na 0.38.0 diretamente. Um histórico legado que mostra falha conclusiva impede a continuidade por falha temporária posterior. Se uma sequência legada truncada não permite verificar as tentativas omitidas, exige nova prova. Uma credencial, identidade, política, consentimento ou destino alterado exige nova autorização ou verificação conforme o vínculo. A liberação de prova vencida não amplia permissões.

Para recuperação operacional, guardar backup coerente de banco, estado do site e chaves de cifra. Conferir registros, referências e recibos antes de retomar. Uma entrega aceita pelo fornecedor não é desfeita pela troca de arquivos. Correções posteriores à instalação exigem nova versão.

## 6. O que permanece pendente

- **Mantenedor do Core.** Revisar e incorporar o diff da seção 2. O Core oficial 1.95.0 mantém seu limite de tentativas da aquisição e sua janela de sete dias das etapas. Um envio de resultado ambíguo sem `requestId` também depende da adaptação do consumidor para reapresentar a transação. A cópia experimental não é um instalador oficial.
- **Frota e dono da conta.** Publicar e distribuir pelos hashes previstos. Acompanhar CTOOffice durante 72 horas corridas após a troca, filtrar `conversion:verification` por alvo e origem, conferir GA4 com renovação e Ads sem renovação periódica. Validar envio e confirmação individual de uma conversão autorizada. A bancada usou timestamps controlados e respostas simuladas; o período de produção ainda não transcorreu para este instalador.
- **Serviços externos.** GA4, Google Ads, Data Manager e SMTP reais não foram acionados durante as simulações. A homologação externa da atribuição e o recebimento pelo destino técnico pertencem aos operadores. Sheets, Cloud Shell e campanhas reais ficaram fora do escopo.
- **Limites das ferramentas.** Execução pelo runner compatível preservado no fonte, sem o PHAR oficial PHPUnit nem a matriz histórica completa de promoção. A inspeção visual desta rodada cobriu a tela alterada em Chromium. O site de produção não recebeu injeção de falha.

## 7. Credenciais e configuração do dono

Em **Ferramentas → Fator3 MCP Google → Conversões**, selecionar a conexão, o fluxo GA4, o segredo do Measurement Protocol e a conta/ação Ads. Credenciais válidas já instaladas são aproveitadas. No Ads, confirmar ação de importação ativa, acesso da identidade, termos do cliente e habilitação das conversões otimizadas quando utilizadas. Para recuperar uma recusa, corrigir a causa, executar a verificação e acompanhar a fila do mesmo destino. Para etapa comercial, verificar a ação exata da concessão. No Core, o destino técnico de avisos deve estar configurado.

A leitura de `google/readiness-status` é local. O registro `entregue` do GA4 comprova recepção HTTP. No Ads, o `requestId` admite consulta posterior do estado da requisição. Preservar o ID de transação e o destino quando o retorno admitir retentativa.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `wp-mcp-google-fator3-0.39.0-instalador.zip` | 996195 | `9a8cadb240e6398f1a85a833fcce46bb7b1bfa251d74c5111984547a5c453fce` |
| Fonte | `wp-mcp-google-fator3-0.39.0-fonte.zip` | 23174330 | `69b6e25e450d4fcc2be6ffe60d66c01a77b727e186e84788f4b4d60270946489` |

Este é o relatório externo canônico. A cópia no fonte antecede seu fechamento. O tamanho e o hash definitivos acima foram calculados a partir do ZIP entregue.

O instalador tem raiz `wp-mcp-google-fator3/` e contém 210 arquivos. O fonte tem raiz `wp-mcp-google-fator3-0.39.0-fonte/` e reúne runtime, código de desenvolvimento, testes, documentação e evidências. O quarto arquivo da entrega é o impacto individual identificado na seção 2, com o diff integral para o Core.
