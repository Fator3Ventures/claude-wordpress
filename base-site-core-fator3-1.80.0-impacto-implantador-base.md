# Impacto no Fator3 Implantador — autoria de páginas diferentes no mesmo grafo

**Revisão 3 · 10/11/2026 · Entrega · acao-necessaria**. Revalidação do encaminhamento da 1.78.0, revisão 2. Emissor base-site-core-fator3 1.80.0, base 1.79.0. Destinatário implantador-base 2.20.0, na cópia do tema que ele distribui. O responsável pela incorporação é o mantenedor do Implantador. A versão que resolverá o encaminhamento cabe a esse mantenedor.

## Reprodução e correção verificada

No WordPress 7.1.4 com Yoast 28.8 e PublishPress Authors 4.18.0, monte uma consulta singular com um Article, o WebPage correspondente, um segundo WebPage e o Person creditado neste último. O Core atribui o autor editorial às peças da publicação atual. Depois dele, o filtro `f3pa_schema_graph` do tema, prioridade 1001, também troca a referência de autor do outro WebPage. O teste `mixed-oficial` reproduziu a troca na cópia oficial 2.20.0.

Aplicar `impactos/implantador-2.20.0-grafo-misto.patch` do fonte do Core com `patch -p1` na raiz do Implantador. O patch restringe a troca por identidade de página e vínculo do artigo e preserva o Person referenciado por outra peça. A prova `mixed-proposta` manteve o autor da segunda página e a identidade desse Person. No ensaio separado de HTML público, Article e WebPage do artigo exibiram o perfil editorial com PublishPress ativo e a organização com PublishPress desativado. O registro da rodada está em `evidence/1800/provedores--mixed-*.json` e `evidence/1800/yoast-http-*.json`.

| Identidade | SHA-256 |
|---|---|
| Instalador do Core 1.80.0 | 2e81a04d0a9f99f1607d5b388c4aa2590bcc0b3b853cda1fa1b7b3530302ec72 |
| Instalador do Implantador 2.20.0 | 1f2d5b9f01a3d5d1a08877e3510915304ef80263834be5c13e3f7fe429919dc1 |
| fontes/tema/autoria.php distribuído | 0870b92b67be69f164b308f0e58c54a681ccbdda6c860fb0c27f184410aefc6b |
| Mesmo arquivo com a proposta | 7c5e244d059b43a98ee5bea0b8f85136dd4d3a61d6c9e7404e9134976ef7836e |

## Aceite do destinatário

Incorporar a correção no tema distribuído, atualizar o manifesto previsto pelo Implantador e validar a atualização do tema em sites existentes. Incluir coautoria, paginação, arquivos de perfil e Person compartilhado por várias peças. A prova desta rodada cobre o grafo misto de artigo. Nenhuma mudança de schema, permissão, dado persistido ou ordem de instalação é exigida do Core. O patch foi exercitado somente em cópia descartável do tema. O encaminhamento anterior continua aberto no escopo da versão 2.20.0 examinada. Não foi criado outro ticket.
