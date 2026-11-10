# Impacto no Fator3 Implantador · crédito de autoria em grafos mistos

Emissor base-site-core-fator3 1.78.0 · Destino implantador-base/implantador-base.php 2.20.0 · Etapa entrega · Revisão 2, 10/11/2026 · Classificação acao-necessaria · Aberto para o dono do Implantador.

## Alcance e reprodução

A análise do planejamento identificou uma segunda escrita no filtro wpseo_schema_graph. No WordPress 7.1.4 com PHP 8.3.6, Yoast 28.8, PublishPress Authors 4.18.0 e perfil aprovado, o Core atribui crédito apenas às peças atuais. A ponte f3pa_schema_graph do tema em fontes/tema/autoria.php, prioridade 1001, volta a atribuir esse crédito a todas as peças WebPage/Article. Reproduzido com um artigo, seu WebPage, outro WebPage e a pessoa creditada nesse último. O tema oficial trocou o crédito alheio. O responsável pelo tema pode reproduzir pelo modo mixed-oficial de tests/integracao-1780.php do fonte do Core. O teste injeta um grafo misto na consulta singular real. O HTML normal de artigo com perfil aprovado passou separadamente.

## Correção exercitada no destinatário

Na cópia local do Implantador 2.20.0, aplicar impactos/implantador-2.20.0-grafo-misto.patch com patch -p1 na raiz implantador-base. O SHA-256 de fontes/tema/autoria.php muda de 0870b92b67be69f164b308f0e58c54a681ccbdda6c860fb0c27f184410aefc6b para 7c5e244d059b43a98ee5bea0b8f85136dd4d3a61d6c9e7404e9134976ef7836e. Instalador oficial do destinatário 642033 bytes, SHA-256 1f2d5b9f01a3d5d1a08877e3510915304ef80263834be5c13e3f7fe429919dc1.

A proposta confere @id/url do WebPage e o vínculo do artigo com a página consultada, filtra os candidatos a remoção pelos autores das peças alteradas e preserva a pessoa usada em outro nó. A assinatura aprovada entra pelo @id editorial. A rotina de perfil também restringe o nó alterado à página atual. O modo mixed-proposta confirmou o crédito aprovado no artigo e na sua página, o autor da página externa e o respectivo Person. O arquivo oficial foi restaurado na cópia do tema de teste.

## Aceite e distribuição

O mantenedor do Implantador deve incorporar a correção na fonte distribuída do tema, atualizar a identidade e os manifestos de assets do tema conforme o seu mecanismo de implantação e validar sua própria suíte de perfis, coautoria, paginação e atualização de tema em sites existentes. Conferir também grafos com Person compartilhado por outras peças. O ensaio do Core cobre o fluxo de artigo com outra página no mesmo grafo. A release oficial do Implantador e o tema do Site-Teste não foram substituídos por esse patch. Nenhum ticket externo aberto.

O Core 1.78.0 atende os três pontos do impacto de entrada da 2.20.0 em seu próprio runtime. O ajuste adicional de autoria só se aplica quando a ponte editorial do tema atua em grafo misto. Para aplicar o Core, atualizar o ZIP, invalidar os caches, conferir autoria pública e reaplicar a revisão gerenciada de servidor com bloquear_listagem ligado. O Implantador continua consumindo as mesmas abilities e pode usar o campo aditivo upgrade_http na prova de C7.
