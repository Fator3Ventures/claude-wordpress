# Impacto no Fator3 Implantador 2.21.0 — documentação da lista de rastreamento

Revisão 1 de 13/11/2026, entrega do Core 1.83.0. Pedido 397. Destinatário e responsável pela incorporação: mantenedor do Implantador. Situação: ajuste documental confirmado em cópia.

## Alteração solicitada

A documentação instalada pelo Implantador apresenta 35 nomes como a quantidade corrente. O Core 1.83.0 fornece 47. Atualize o texto de `includes/documentos.php` para indicar que a fonte de verdade é `cache.requisitos.configuracao_requerida.wpsc_tracking_parameters`. O operador consulta `rastreamento.faltantes` para conferir o site. A contagem deve acompanhar a versão do Core identificada no exemplo.

O patch `impactos/implantador-2.21.0-documentacao-397.patch` acompanha o fonte do Core. Aplique com `patch -p1` na raiz de uma cópia do Implantador. Foi aplicado à cópia extraída do instalador 2.21.0, SHA-256 `f29a91db9a225089295c0bde462819578b9291d3251262ec7afa63442970349c`. O arquivo corrigido passou por `php -l`.

## Diagnóstico e aceite

O método `F3Base_Imp_Cache::perfil()` chama `F3Base_Imp_Integracoes::core_cache('consultar')`, que executa a ability pública de verificação do Core. O ensaio carregou os dois pacotes no WordPress 7.1.4 com PHP 8.3.6. Foram aprovadas cinco verificações: os 47 nomes chegaram ao perfil, ref ficou fora, a variável de outro componente foi preservada, a atribuição foi escrita em uma linha e a segunda geração produziu bytes idênticos.

O Core já fornece o contrato exigido. O Implantador 2.21.0 pode consumir o novo Core antes da revisão do texto. Para conferir, use `tests/implantador-397.php` no laboratório e consulte `evidence/1830/implantador-221.json` e `implantador-patch.json`. A incorporação do patch no pacote do destinatário está pendente.
