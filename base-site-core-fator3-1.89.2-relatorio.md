# Entrega — Fator3 Site Core 1.89.2

**Pedido 417.** As 11 fichas Motorola passam a identificar o próprio aparelho, e o Moto G8 Power Lite entra no catálogo. A 1.89.2 foi instalada e validada no Site-Teste. O aceite ao vivo do CTO Office aguarda a implantação pela frota.

## 1. De onde esta versão entra

Instalação em WordPress limpo ou atualização direta da 1.89.1. Os dois caminhos passaram em WordPress 7.1.4 com PHP 8.3.6 de 64 bits. Requisitos de produção: WordPress ≥ 7.1.4 e PHP ≥ 8.3 de 64 bits. Base de partida do instalador 1.89.1 conferida pelo SHA-256 `8182d7dc2c2763bb45854840e6768e1477b4d687bbf217fa2417d0e4c18a0bd2`.

## 2. Convivência e encaminhamentos

No Site-Teste estavam ativos Fator3 MCP 0.46.0, MCP Google 0.36.0, MCP LinkedIn 0.24.0, MCP Meta 0.27.0 e MCP Pipedrive 0.11.1. A troca é isolada do Site Core. Relatórios, Slack e Pipedrive já consomem os campos comerciais do Core. O contrato administrativo permanece em 8.41.0. O formato dos campos e a prioridade das regras locais permanecem os da base. Nenhum outro pacote exige desenvolvimento para o pedido 417.

## 3. Mudanças e evidências

A seleção anterior aceitava um nome comercial do Google Play mesmo quando a linha tinha outro Device. Por exemplo, o código `moto g play - 2024` apontava para o Edge 60 Pro, de 2025, topo e premium. A nova ficha usa o Device `fogona`, ano 2024, faixa entrada e linha premium não.

| Código | Device | Nome do aparelho | Ano | Preço estimado (R$) | Faixa | Premium |
|---|---|---|---:|---:|---|---|
| motorola edge 20 pro | pstar | motorola edge 20 pro | 2021 | 896,72 | topo | sim |
| moto g - 2025 | kansas | moto g - 2025 | 2025 | 960,75 | entrada | não |
| moto g stylus 5G (2022) | milanf | moto g stylus 5G (2022) | 2022 | 480,40 | intermediário | não |
| moto g51 5G | cypfq | moto g51 5G | 2021 | 599,00 | intermediário | não |
| motorola edge 40 pro | rtwo | motorola edge 40 pro | 2023 | 1777,39 | topo | sim |
| moto g 5G (2022) | austin | moto g 5G (2022) | 2022 | 429,54 | intermediário | não |
| motorola edge (2022) | tesla | motorola edge (2022) | 2022 | 898,64 | topo | sim |
| moto g stylus 5G - 2023 | genevn | moto g stylus 5G - 2023 | 2023 | 621,70 | intermediário | não |
| moto g play - 2024 | fogona | moto g play - 2024 | 2024 | 847,71 | entrada | não |
| motorola edge 2025 | oulu | motorola edge 2025 | 2025 | 1978,07 | topo | sim |
| motorola razr 2022 | oneli | motorola razr 2022 | 2022 | 1260,00 | topo | sim |
| moto g(8) power lite | blackjack | Moto G8 Power Lite | 2020 | 890,00 | entrada | não |


O nome próprio estabelece os codinomes válidos. Um nome regional anterior permanece quando compartilha o mesmo Device e marca Google. Entre os 93 códigos com vários nomes, 59 têm linha própria. Os outros 34 mantêm a escolha anterior e estão discriminados em `reference/417/ambiguidades-sem-linha-propria.csv`. Os três exemplos regionais do pedido foram preservados. O catálogo ganhou uma linha e conservou integralmente 1.337 fichas anteriores.

Fontes de identificação, regras de faixa, preços e método de estimativa ficam em `reference/417/README.md` e `fichas-pesquisadas.csv`. Preços convertidos ou calculados por comparável constituem estimativas. O preço do Razr 2022 usa um comparável nacional explicitamente identificado na fonte.

| Prova | Resultado |
|---|---|
| Regressão independente do gerador | 11 erros reproduzidos na 1.89.1. Zero na 1.89.2. Todos os 1.349 códigos percorridos, incluindo 139 com linha própria. |
| Regras do gerador | Código sintético distinto dos 11. Mantém alias de mesmo Device, rejeita ficha sem correspondência, respeita a escolha sem linha própria e produz o mesmo resultado ao inverter os candidatos. |
| WordPress limpo e atualização da 1.89.1 | 1.349 × 6 campos conferidos pelo resolvedor público em cada instalação. Todos os preços são positivos. |
| Perfis retidos | No mesmo banco, a consulta paginada dos 12 códigos passou de uma pendência a nenhuma. Três páginas por leitura, cursor final nulo e hash das observações idêntico antes e depois. |
| Integridade | Dados compilados novamente com resultado idêntico. As mudanças no PHP do instalador são a versão, a indicação da base de atualização e a revisão do catálogo. |
| Site-Teste | 1.89.2 ativa, revisão 2026-11-15.4 e 1.349 códigos. A atualização concluiu 20 etapas em 5 segundos, sem falhas. Página inicial e REST responderam HTTP 200 antes e depois. |

Os resultados de cada comparação estão em `evidence/1892/`. A prova operacional do Site-Teste usa o ZIP com o mesmo hash entregue. As notas de release foram relidas pelo MCP em duas páginas e o conteúdo conferido com o arquivo local. A consulta no Site-Teste retornou lista vazia com zero códigos retidos. O teste funcional com 12 perfis está nas evidências de laboratório.

## 4. Instalação e prova da troca

1. A frota compara os hashes do instalador e do fonte na seção 8, publica os artefatos conforme o fluxo do projeto e confere novamente o hash do instalador servido. [Destino do instalador no repositório](https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/base-site-core-fator3-1.89.2-instalador.zip).
2. Usar `plugins/upload` com o endereço publicado, `expected_slug=base-site-core-fator3`, o SHA-256 do instalador, sobrescrita e ativação. Acompanhar `f3base/como-usar` até `versao=1.89.2`, atualização concluída, revisão `2026-11-15.4` e 1.349 códigos. A confirmação técnica no Site-Teste consta do recibo `1724a67fd927268dc5296ed38472b316`.
3. Executar `f3base/aparelhos-sem-nome-ler` no CTO Office, com `limite=200`. A cada resposta, passar `proximo_apos` como `apos` até o cursor nulo. O aceite exige a união de todas as páginas vazia. Os nomes das 11 fichas podem ser conferidos por código no CSV distribuído.

## 5. Banco, migração e correção por nova versão

O patch substitui o catálogo embarcado. Novas observações usam a ficha corrigida. Um perfil retido sem nome comercial pode ser enriquecido na leitura. Perfis já gravados com nome preservam o registro original, inclusive nos relatórios históricos. A versão não reenvia mensagens de Slack nem atualiza retroativamente registros do Pipedrive. A atualização executa a rotina normal e retomável de prontidão do Core. Correções posteriores seguem em nova versão.

## 6. Validação pendente

Na última consulta de produção, o CTO Office ainda executava a 1.89.1. Entre os 132 códigos examinados apareceu apenas `moto g(8) power lite`, em um perfil, com cursor final nulo. Essa consulta está em `evidence/1892/ctooffice-ultima-leitura.json`. O aceite ao vivo permanece pendente. A validação concentrou-se no catálogo, na instalação e na leitura real da documentação. Por solicitação do dono, a suíte geral não foi repetida. Não foram realizados envios externos de Slack ou Pipedrive.

## 7. Credenciais e configuração

Basta atualizar o Site Core. Nenhuma credencial, configuração adicional ou importação de CSV é necessária. As referências de pesquisa ficam no pacote fonte.

## 8. Identidade dos arquivos

| Tipo | Nome | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [base-site-core-fator3-1.89.2-instalador.zip](base-site-core-fator3-1.89.2-instalador.zip) | 4552457 | `01b62a0223624cc167ef49a4ff03ac8d82cc8893954aeac2d7b7968bde4b9bfa` |
| Fonte | [base-site-core-fator3-1.89.2-fonte.zip](base-site-core-fator3-1.89.2-fonte.zip) | 6138589 | `64e2a24b3ec5447d034de59c9cc7bb639823a439a7ef0edf04d229fa1fdac0f1` |
| Catálogo | [base-site-core-fator3-1.89.2-catalogo-aparelhos.csv](base-site-core-fator3-1.89.2-catalogo-aparelhos.csv) | 79503 | `2c9521aced4ab6bb286cbdf79649ce428333f9ca4cffe491fc822648ec6de214` |

O ZIP fonte fica abaixo do limite de 100.000.000 bytes.
