# Impacto do Fator3 MCP Google 0.34.0 no Fator3 Site Core

11/11/2026 · Revisão 3 · Etapa de entrega · Situação **aberto** · **Ação necessária** do mantenedor do Core. Pedido MCP Google 50 / Pedidos core 390. Natureza de desenvolvimento e contrato.

| Pacote | Versão | SHA-256 do instalador |
|---|---|---|
| Google anterior | 0.33.0 | a45ce1bb589452f578b67b7e28b25f2774efc2f250f02d046ff58c9f823c2ca2 |
| Google entregue | 0.34.0 | 9a5f52f35a4a7c34e21e08d12099dacb05dfdfc99d3d0cc335bde95a2676135c |
| Core examinado | 1.80.0 | 2e81a04d0a9f99f1607d5b388c4aa2590bcc0b3b853cda1fa1b7b3530302ec72 |

## Mudança e consequência

O Core 1.80.0 já obtém a campanha, o grupo e a referência do anúncio do acervo de cliques. O Google 0.34.0 permite ao mesmo cliente registrado consultar o criativo via `origin_ad()`. A extensão se identifica como `google-ads-origin/1.0.0`, com schemas em `capabilities()['extensions']['origin_ad']`. O acesso exige uma concessão específica na conta, além da autorização para cliques. O Google é responsável pela credencial, uso de cota, fila de coleta, mídia e auditoria. O Core seleciona conta, conexão, contato e quem pode ver o resultado.

## Ação do mantenedor e alteração proposta

Aplicar em cópia de trabalho do Core o patch `integration/core390/core-1.80.0.patch` do fonte Google, SHA-256 `783dd6075e4d2130eefb73c13a5bf1877a46fedf47139d9a873cbfa992ef0a90`. O comando, executado na raiz de um Core 1.80.0 íntegro, é `patch --batch --fuzz=0 -p1 -i /caminho/core-1.80.0.patch`. Ele modifica `includes/class-f3base-google-acervo.php`, acrescenta o método `anuncio_origem` e a habilidade `f3base/google-ads-anuncio-origem`. O adaptador exige `manage_options` e `f3base_ler_leads`, lê somente a seleção oficial do Core e entrega ao SDK a revisão vigente. O método local `query()` conserva o bloqueio HTTP existente. A leitura do novo criativo usa apenas o método da extensão.

Na tela do contato, oferecer a consulta usando o GCLID armazenado e a data do clique no fuso da conta, ou o ID do anúncio informado pelo formulário de lead Google. Renderizar título, descrição, imagem, vídeo, caminhos, destinos e links de campanha/grupo conforme disponíveis. Em `pending`, exibir a hora prevista e permitir nova leitura. Em `campaign_only`, mostrar os grupos PMax como candidatos. Se a extensão estiver ausente, apresentar a indisponibilidade. A inclusão da apresentação do contato e sua publicação pertencem à versão oficial do Core.

## Prontidão do Google e configuração

Instalar o Google por substituição da versão 0.33.0. No Core, escolher conta, conexão e revisão em `f3base_google_ads_acervo`. Em Acervo Ads do Google, conferir o leitor do Core, selecionar Cliques e GCLID, habilitar a leitura local e autorizar a consulta do criativo. O formulário do Google e a habilidade `ads/archive-consumer-grant` chegam ao mesmo serviço de autorização. A instalação do pacote conserva os acessos anteriores. Cada chamada revalida identidade, conta, revisão, autorização e política. O identificador do contato fica no site.

Entradas da habilidade proposta: `{"date":"2026-11-10","gclid":"CLIQUE"}` ou `{"ad_id":"123456789"}`. A conta fica vinculada à configuração do Core. A saída `found` contém `campaign`, `ad_group`, `ad_id`, `ad_type`, `headlines`, `descriptions`, `paths`, `final_urls` e `media`. O guia instalado CORE-ACERVOS.md descreve estados e limites. O Google entregue já atende o contrato para a incorporação do consumidor.

## Compatibilidade e evidência

As bancadas utilizaram WordPress 7.1.4, PHP 8.3.6, MySQL 8.0.46 e Core 1.80.0. O patch foi aplicado sem tolerância a contexto divergente. A extensão ausente foi exercitada na base Google 0.33.0. Na 0.34.0, o consumidor passou com concessão negada e habilitada, com revogação durante a leitura, com conta divergente, com dia pendente, com ID de formulário e com associação parcial ou ambígua. O ensaio privado executou a habilidade do Core sobre uma reprodução das respostas obtidas no CTO Office em leitura. O acervo original apresentou uma linha para o GCLID de 10/11 e o fornecedor devolveu o anúncio Demand Gen com logotipo e vídeo. A entrega inclui apenas evidências sanitizadas. O laboratório também exercitou PMax e carrossel com respostas controladas. O conjunto de fechamento incluiu MCP 0.44.0, Meta 0.24.1, LinkedIn 0.21.0 e Pipedrive 0.9.0. A integração, a migração, o navegador e a documentação foram exercitados com esses pacotes ativos.

As instruções de reprodução estão em `evidence/034/LEIA-ME.md` no fonte. A cópia experimental não foi instalada no Site-Teste nem no CTO Office. O caminho de migração do Google foi testado com o Core oficial.

## Resposta esperada e evolução

O mantenedor do Core deve informar a versão em que incorporou o consumo, a prova pela tela do contato e o resultado dos testes de concessão e revogação. Revisão 1 identificou a dependência no planejamento. Revisão 2 consolidou o método e a autorização separada. Revisão 3 registra a implantação do produtor e a prova experimental do consumidor. A adoção oficial continua aberta.
