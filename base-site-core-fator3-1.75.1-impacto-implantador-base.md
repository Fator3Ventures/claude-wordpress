# Impacto do Fator3 Site Core 1.75.1 no implantador-base

09/11/2026 · Revisão 2 · Etapa de entrega · Situação aberta · Pedido Core 379 · Classificação `acao-necessaria` · Natureza de desenvolvimento do tema-modelo.

O planejamento da 1.75.0 registrou o contrato de marcação explícita e o identificador posicional para temas existentes. A revisão de entrega conserva esse contrato no patch 1.75.1. O Core partiu da 1.74.0. O instalador final `base-site-core-fator3-1.75.1-instalador.zip` tem SHA-256 `9fff30dc9b75a60fc193373c4366659bf6db13c35025f677b5f46e8988181dc6`.

O fonte examinado e modificado em cópia isolada foi `implantador-base-2.18.0-fonte.zip`, SHA-256 `22498b7dd7665513f013b3ec31f7890d6b6039226906cda552defd87e6985a55`. O responsável pelo implantador define a versão de incorporação.

## Consequência para o tema

O Core registra a seção e o alvo técnico em `f3base_clique_inerte` e `f3base_friccao`. Quando o elemento tocado ou um ancestral na mesma seção traz `data-f3base-alvo`, o valor acompanha o evento. Sem essa marca, o Core calcula um identificador por seção, tipo de elemento e posição no DOM. Reordenar dois títulos na mesma seção altera os identificadores posicionais. Um identificador declarado permite comparar o mesmo componente após a edição.

Use até 48 letras ASCII minúsculas, dígitos, hífens ou sublinhados, iniciando com letra ou dígito. Reserve um ID estável por alvo dentro da seção. O valor entra na medição e segue as políticas de destino da seção. O autor escolhe um identificador técnico fixo. Ele não deve incorporar nomes próprios, conteúdo de campos ou URLs.

## Patch experimental e reprodução

O arquivo `impactos/implantador-2.18.0-pedido-379.patch` dentro do fonte do Core altera dois arquivos do destinatário.

| Arquivo no implantador | Alteração comprovada |
|---|---|
| `content/pages/home.html` | Adiciona a classe nativa `f3-alvo-introducao` ao primeiro bloco de título e ao HTML serializado desse bloco |
| `fontes/tema/functions.php` | Usa `render_block_core/heading` e `WP_HTML_Tag_Processor` para transformar a declaração válida em `data-f3base-alvo="introducao"` no H2 renderizado |

No diretório que contém `content/` e `fontes/`, aplique `patch -p1 < /caminho/impactos/implantador-2.18.0-pedido-379.patch` e execute o laboratório com `F3BASE_IMPLANTADOR` apontando para a cópia alterada. As instruções estão em `tests/README.md`. A revisão do bloco continua disponível no editor de blocos. O patch dispensa JavaScript adicional no tema e dispensa migração do banco.

O WordPress 7.1.4 renderizou o grupo real da home. Sem marca, a auditoria contou três textos sem alvo. Com a marca, contou dois e encontrou exatamente um título com o identificador introducao. Uma classe com barra foi ignorada. As três verificações passaram no Core 1.75.1. A evidência é `evidence/1750/patch--implantador-2180.json`.

## Aceite e responsáveis

O responsável pelo implantador deve incorporar a marcação às seções pertinentes, incluindo as variantes para texto, logo e etapas quando usadas. A amostra de patch trata o título. Depois de reordenar o componente, confira a marca na página renderizada com `f3base/conteudo-instrumentacao-ler`, faça dois cliques em alvos distintos e confira a sessão e a visão de blocos. O Core já reconhece o atributo e atende temas sem marca. A frota decide quais temas publicados adotarão as marcações. O aceite e a distribuição da versão oficial do implantador permanecem abertos.
