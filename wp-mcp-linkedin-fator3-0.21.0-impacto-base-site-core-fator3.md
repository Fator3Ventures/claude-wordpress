# Impacto do Fator3 MCP LinkedIn 0.21.0 no Fator3 Site Core

Revisão 2 · 11/11/2026 · Etapa: entrega · Classificação: acao-necessaria · Situação: emissor pronto; incorporação ao fluxo de Pedidos core 390 pendente no destinatário.
Emissor: wp-mcp-linkedin-fator3, base 0.20.0 → 0.21.0, 439650 bytes, SHA-256 `ebe4363bf55476cbe1ba30df80d8ab6b2362ee2dc379c21762aa42f4a05b1bfc`. Destinatário: base-site-core-fator3 1.80.0, SHA-256 `2e81a04d0a9f99f1607d5b388c4aa2590bcc0b3b853cda1fa1b7b3530302ec72`. Ticket do emissor: Pedidos MCP LinkedIn 24.

## Diagnóstico e consequência

O método de campanha existente enriquece campanha de uma resposta autorizada. Ele não entrega texto, botão, destino, publicação e mídia do anúncio. O Core 1.80.0 tem adaptador genérico em `includes/class-f3base-linkedin-cliente.php::chamar`; já registra uma identidade por integração, insere a conexão e a conta configuradas e verifica os métodos do descritor. Com o emissor novo, esse adaptador já consegue chamar o método; o código atual do Core não apresenta o anúncio completo ao usuário. A captação de leads e a deduplicação são independentes deste enriquecimento.

## Interface emitida e autorização

No leitor fornecido por `PublicApi::lead_reader($consumer)`, o descritor anuncia `extensions.ad_source=linkedin-ad-source/1.0.0` e o método `resolve_ad_source`. Pelo transporte administrativo o nome é `linkedin/lead-resolve-ad-source`. Fase única de leitura; publicação, mídia e campanha precisam manter vínculos verificáveis com o criativo. O consumidor requer uma concessão ativa com permissão nova ad_source e conta autorizada em Ads. Na seleção por resposta são exigidos também responses e um formulário habilitado. A instalação não amplia permissões existentes. Quem conceder ad_source autoriza a leitura por ID dos criativos de toda a conta concedida; explique a abrangência antes de habilitar.

Dentro do escopo de uma integração já selecionada no Core, chamar:

```php
$r = F3Base_Linkedin_Cliente::chamar('resolve_ad_source', ['creative_id' => '777']);
// Para o Lead Sync, usar exclusivamente o outro modo:
$r = F3Base_Linkedin_Cliente::chamar('resolve_ad_source', ['form_id' => '8331', 'response_id' => 'response_1']);
```

Em sucesso: `$r['data']['ad_source']`. Os IDs e links da campanha/publicação são estáveis. O par `media` e `thumbnail` contém url e expires_at_ms separadamente; validade não fornecida é nula. Endereços são temporários e devem ser resolvidos sob demanda. Não persistir o envelope completo, não registrar URLs assinadas, não gravá-las como attachments nem copiar automaticamente mídia a partir de um endereço enviado pelo navegador. O cliente precisa mostrar o estado de mídia ausente sem apagar o restante. Um erro de autorização ou ligação entre entidades rejeita a leitura, sem disparar nova captação nem reenvio.

## Alteração sugerida, patch e evidência

O fonte do emissor inclui `impacts/core-1.80.0-ad-source.patch`, aplicável com patch -p1 na raiz do Core 1.80.0. Acrescenta `F3Base_Linkedin_Cliente::origem_anuncio`, que respeita a seleção do cliente, valida a versão do contrato e separa `origem` de `midia_temporaria`. No ponto da ficha de origem de Pedidos core 390, chamar esse wrapper sob a integração do registro e as permissões de leitura do próprio contato. Guardar apenas referências estáveis; a exibição de uma mídia deve conferir a validade e obter uma nova leitura quando necessário. O wrapper é um exemplo testado de consumo; não é a implementação da tela do Core.

**Provas na bancada:** com o Core oficial intacto, o adaptador leu uma origem pela integração selecionada (suíte ad-source021 integrada, 38 verificações). Em outra instalação descartável, o teste `core-frontier021.php` conferiu o hash do arquivo original, aplicou o patch na cópia do Core, percorreu a origem de formulário nativo e verificou que a URL temporária não aparece na projeção persistível (39 verificações); o arquivo foi restaurado ao terminar. A suíte oficial do Core para o fluxo anterior passou em 37 verificações. WordPress e acompanhadores reais no laboratório; fornecedor sintético nestes testes. Não se alterou a release oficial do Core.

## Aceite e encaminhamento

1. Sem concessão, fornecer indicação para habilitar o acesso, manter a captação vigente e não reutilizar dados de outro registro.
2. Com a concessão e o leitor 0.21.0 ativos, a ficha recupera por conta/criativo ou por formulário/resposta os metadados do anúncio e separa links estáveis e temporários. Rejeitar revisões vencidas, conta divergente, criativo não associado ou acesso revogado.
3. Para campos incompletos, mostrar a indisponibilidade; não reproduzir anúncios nem gerar consumo de verba. Com conta autorizada, verificar o download da imagem do criativo indicado no pedido. O relatório de entrega distingue o que foi verificado em cada site.

Responsável pela integração na ficha e pela respectiva entrega: mantenedor do Core. Responsável pelas concessões e validação das contas: administrador do site. A revisão 1, prévia, está preservada em inputs/0.21.0; a revisão 2 encerra a entrega do emissor. Nenhum encaminhamento foi enviado a terceiros.
