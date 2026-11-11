# Impacto do Fator3 Site Core 1.81.1 no Fator3 MCP LinkedIn

Revisão 1 · 11/11/2026 · Entrega · Validação coordenada em aberto no CTO Office. Pedidos Core 390 e MCP LinkedIn 24.

| Referência | Versão | SHA-256 do instalador |
|---|---|---|
| Core de partida | 1.80.0 | 2e81a04d0a9f99f1607d5b388c4aa2590bcc0b3b853cda1fa1b7b3530302ec72 |
| Core com o consumidor entregue | 1.81.1 | 8a03bc5dfd3f94d81a953bb7134a14bacbc6883c5b038b4ef0fee1241c1dcb02 |
| Fator3 MCP LinkedIn | 0.21.0 | ebe4363bf55476cbe1ba30df80d8ab6b2362ee2dc379c21762aa42f4a05b1bfc |

## O que está pronto

O Core usa o leitor registrado da integração de origem. O adaptador F3Base_Linkedin_Cliente::origem_anuncio exige linkedin-ad-source/1.0.0. No formulário nativo o leitor recebe form_id e response_id. Na atribuição do site recebe creative_id. O fluxo confere conta, campanha e criativo e separa a mídia temporária dos links estáveis. A ficha permite uma nova consulta em um contato anterior sem disparar captação ou envio.

O patch de referência do LinkedIn foi incorporado ao consumidor. A suíte nativa registrou 39 verificações aprovadas com ambos os plugins ativos, incluindo revogação e relações entre entidades. A prova de duas execuções do worker utilizou um negócio aberto em vez de criar outro lead. A nota fixada e o anexo foram vinculados a esse negócio. A prova está em evidence/1811/ad-source021.json e worker-linkedin.json. As chamadas de rede foram simuladas.

## Validação no CTO Office

1. O administrador confere a instalação na janela autorizada do CTO Office. A consulta desta rodada encontrou Core 1.80.0 e LinkedIn 0.20.0. Instale ambos os pacotes da tabela.
2. Na integração vinculada ao formulário, conceda ao consumidor ad_source para a conta Ads 558431216. Essa permissão inclui a leitura por ID dos criativos da conta concedida. Para o fluxo por resposta, confira também responses e a seleção do formulário. Não é necessária permissão para escrever anúncios.
3. No contato de referência do pedido, use **Consultar anúncio na plataforma**. Confira a campanha 901687794, o criativo 1605615034 e o vínculo da publicação. Abra a campanha no Campaign Manager, confira o texto, o botão e o destino. Quando houver mídia, confira se a imagem ou miniatura pode ser baixada com a autorização atual. Registre tipo, tamanho e data.
4. Se a API negar a consulta, registre o código, a versão, o modo de seleção e o tipo de concessão. Se um vídeo estiver disponível, compare link de reprodução e miniatura. Preserve ausência de dados quando a plataforma omitir um campo. Evite persistir URL assinada ou reproduzir o contato comercial.

O mantenedor LinkedIn e o administrador podem encerrar a validação com o resultado da própria conta, sem nova alteração de código no contrato testado. A confirmação da entrega visual em um workspace Slack e em uma conta Pipedrive reais exige destinos de homologação designados pelo responsável.
