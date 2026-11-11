# Impacto do Fator3 Site Core 1.81.1 no Fator3 MCP Meta

Revisão 1 · 11/11/2026 · Entrega · Validação coordenada em aberto na Korvena. Pedidos Core 390 e MCP Meta 28.

| Referência | Versão | SHA-256 do instalador |
|---|---|---|
| Core de partida | 1.80.0 | 2e81a04d0a9f99f1607d5b388c4aa2590bcc0b3b853cda1fa1b7b3530302ec72 |
| Core com o consumidor entregue | 1.81.1 | 8a03bc5dfd3f94d81a953bb7134a14bacbc6883c5b038b4ef0fee1241c1dcb02 |
| Fator3 MCP Meta | 0.24.1 | 6113dab515dfc26633598cab2bfcd5f48386d4dfee5f8330f4548db7aae1d361 |

## O que está pronto

O consumidor base-site-core-fator3 registra seu cliente no gancho oficial e usa F3Base_Meta_Ads::anuncio_origem com a conexão e a conta selecionadas. O método ad_origin devolve meta-ad-origin/1.0.0. O Core verifica conta e anúncio, separa os links estáveis do endereço temporário de mídia e resolve o criativo fora da gravação do contato. O texto e a imagem disponíveis atualizam a resposta Origem do Slack e a oportunidade confirmada pelo diário do Pipedrive. A consulta manual na ficha também atende contatos anteriores.

O patch de referência entregue pelo mantenedor Meta foi incorporado à implementação do consumidor. A matriz local com Core e Meta oficiais passou nas 28 verificações do SDK. O cron executado duas vezes criou uma nota e um anexo no lead sintético e fez uma edição de Slack. Graph, Slack e Pipedrive usaram respostas controladas. O fonte preserva origin024.json e worker-meta.json em evidence/1811.

## Validação na conta da Korvena

1. O administrador do site confere os pacotes ativos e instala as versões da tabela na janela autorizada para a Korvena. A consulta desta rodada encontrou Core 1.80.0 e Meta 0.23.0. O leitor anterior de histórico indicou pronto.
2. No Meta, selecione a conta usada pela campanha 120256596454580242 e conceda ao consumidor a leitura de origem do anúncio por ID. Confira a mesma seleção no Core. O administrador precisa de leitura dos contatos e administração do site para a consulta manual.
3. Abra a ficha de um contato com anúncio 120256886100270242 e use **Consultar anúncio na plataforma**. Compare conta, campanha, conjunto, anúncio, nome, texto, CTA e destino com o Gerenciador. Abra a publicação quando houver URL estável. Verifique as variantes oferecidas em anúncios dinâmicos. Anote a data da consulta.
4. Confirme que uma imagem ou miniatura atual pode ser baixada pelo leitor autorizado. Registre formato, dimensões e hash dos bytes, sem copiar a URL assinada. O relatório anterior do Meta registrou uma imagem de 1.450.433 bytes, 1080 × 1920. A mídia pode mudar na plataforma. A ficha faz leitura e não inicia reenvio de mensagens comerciais.

Uma recusa ad_origin_not_granted ou grant_revoked exige revisar a concessão do consumidor. Divergência de conta exige revisar a seleção local. A ficha exibe a referência disponível. O administrador e o mantenedor Meta encerram a validação com versão, data, conta coincidente e resultado por tipo de campo. O contrato exercitado está completo nos dois pacotes. A pendência se refere ao anúncio e às credenciais da instalação.
