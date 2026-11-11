# Entrega — Fator3 MCP Google 0.34.0

Revisão 1 · 2026-11-11T02:37-03:00 · Instalada e ativa no Site-Teste. Pedido MCP Google 50 / Pedidos core 390.

## 1. Base de migração

Base direta Google **0.33.0**. O instalador recebido tem 966668 bytes e SHA-256 `a45ce1bb589452f578b67b7e28b25f2774efc2f250f02d046ff58c9f823c2ca2`. O fonte recebido tem 8397009 bytes e SHA-256 `33eb3988b54a6729de773c57b069d65792eb71c1ee9df6b99756fde620707ca8`. O desenvolvimento preserva o slug, o basename, a identidade do cabeçalho e as interfaces publicadas da série. O novo método acrescenta funcionalidade e justifica a versão minor. A atualização foi exercitada sem desinstalar a base. Foram lidos os documentos instrucoes-agentes-plugins-fator3.md e padrao-desenvolvimento-plugins-fator3.md, revisão 5 de 02/11/2026.

Requisitos declarados e executados em bancada: WordPress 7.1.4 e PHP 8.3.6, com MySQL 8.0.46. O Site-Teste informou WordPress 7.1.4 e PHP 8.3.36.

## 2. Convivência e encaminhamentos

Versões ativas observadas no fechamento e exercitadas juntas, incluindo troca direta e leitura pelo Core:

| Acompanhante | Versão | SHA-256 do instalador de laboratório |
|---|---|---|
| Site Core | 1.80.0 | `2e81a04d0a9f99f1607d5b388c4aa2590bcc0b3b853cda1fa1b7b3530302ec72` |
| MCP | 0.44.0 | `a90aa7f2e91ef1033a4a8c6ec320b1e10b45ef657132a40f8aa4215ffa55d5eb` |
| Meta | 0.24.1 | `6113dab515dfc26633598cab2bfcd5f48386d4dfee5f8330f4548db7aae1d361` |
| LinkedIn | 0.21.0 | `ebe4363bf55476cbe1ba30df80d8ab6b2362ee2dc379c21762aa42f4a05b1bfc` |
| Pipedrive | 0.9.0 | `42523b9b547fc8820c3917e192c4b48341efbb1da6815c78fcc18f8a373c09c0` |

O ensaio inicial usou Meta 0.23.0 e LinkedIn 0.20.0. Uma rodada intermediária confirmou Meta 0.24.0. O mesmo instalador Google passou novamente com os dois acompanhantes vigentes no fechamento. O plano, o histórico das entradas e os resultados por conjunto estão em `evidence/034`. As fronteiras do MCP, Meta, LinkedIn e Pipedrive foram conferidas na ativação e convivência. O contrato novo é de consumo opcional pelo Core.

| Destinatário | Classificação | Pedido | Encaminhamento |
|---|---|---|---|
| Site Core 1.80.0 | Ação necessária, aberta | Core 390 | wp-mcp-google-fator3-0.34.0-impacto-base-site-core-fator3.md, revisão 3. Patch experimental em `integration/core390/core-1.80.0.patch`, SHA-256 `783dd6075e4d2130eefb73c13a5bf1877a46fedf47139d9a873cbfa992ef0a90`. |

## 3. Mudanças e evidência

| Pedido | Mudança no produtor | Prova |
|---|---|---|
| Google 50 / Core 390, localizar o anúncio | Extensão PHP `google-ads-origin/1.0.0`. Busca exata por GCLID e data local no acervo cifrado ou leitura por ID decimal de formulário de lead. A consulta externa leva IDs da conta, campanha, grupo e anúncio. | Contrato com o Core em WordPress, acervo real e respostas do Google Ads. |
| Conteúdo e mídia | Tipo do anúncio, nomes e IDs, caminhos disponíveis, destinos, textos, links, recursos de imagem e vídeo. Imagens em cartões Demand Gen são resolvidas por ID. PMax informa os grupos candidatos quando só há campanha no clique. | Demand Gen em vídeo com mídia real. Carrossel e PMax com dados controlados. |
| Dia ainda sem publicação | Estado `pending` com estimativa UTC, quando a agenda e a janela de coleta a permitem. Cron inativo ou janela indisponível devolvem motivo e previsão nula. | Teste com cron real do WordPress e dia sem publicação, sem envio de GCLID ao Google. |
| Permissão, UI e documentação | Controle no formulário do leitor em Acervo Ads. A autorização é específica para conta, conexão e consumidor. O SDK expõe os schemas, e o guia do painel e o manual do Core descrevem a leitura. | Concessão legada, revogação durante a chamada, conta divergente, usuário sem permissão e navegador desktop/celular. |

**Caso real.** Em ctooffice.com.br, a busca local por um GCLID de 10/11/2026 retornou uma linha do acervo da campanha **[Demand Gen] CTO Office — BR**. A consulta da campanha 24432229853 e do grupo 199590019177 identificou o anúncio 830488453329, tipo `DEMAND_GEN_VIDEO_RESPONSIVE_AD`. A API devolveu cinco títulos, um título longo, duas descrições, URL final, uma imagem com papel `LOGO` e um vídeo do YouTube. O logotipo respondeu como PNG e a miniatura do vídeo como JPEG, ambos com HTTP 206 e assinatura de imagem válida. O novo SDK executou as mesmas duas consultas em laboratório com as respostas reais capturadas. As operações no CTO Office foram de leitura pela versão instalada 0.33.0. A autoria visual de uma impressão específica não é fornecida nesse retorno.

A saída do YouTube inclui ID, reprodução e miniatura. O campo de download do vídeo recebe nulo. Para PMax sem origem individual, o leitor informa a campanha e seus grupos candidatos. Referências do fornecedor: [campos do recurso Asset](https://developers.google.com/google-ads/api/fields/v24/asset) e [relatórios de recursos Performance Max](https://developers.google.com/google-ads/api/performance-max/asset-reporting).

## 4. Instalação e prova da troca

Substituir o ZIP pelo basename `wp-mcp-google-fator3/wp-mcp-google-fator3.php`. O MCP do Site-Teste recebeu os bytes autorizados via `plugins/upload-base64`, com `expected_slug=wp-mcp-google-fator3` e `expected_sha256=9a5f52f35a4a7c34e21e08d12099dacb05dfdfc99d3d0cc335bde95a2676135c`. O recibo declarou 0.33.0 → 0.34.0, ativação em requisição PHP independente e cópia do pacote anterior. A raiz e `/wp-json/` responderam 200 nas sondas anteriores e posteriores.

`system/health` retornou saudável. `google/status` informou 0.34.0, estado idle e zero incidentes. O catálogo apresentou 305 habilidades, e o schema efetivo de `ads/archive-consumer-grant` trouxe `origin_ad`. A prontidão registrou armazenamento, recuperação, executor e contexto do Core em ordem. O bloqueio de credencial e os destinos sem configuração constam na seção 6.

**Testes.** PHPUnit 9.6.37 aprovou 1.362 testes e 16.280 asserções. São 13 casos PHPUnit adicionais. O WordPress real exercitou as faixas abaixo. Os números contam verificações por execução e incluem reexecuções com outros acompanhantes.

| Cenário | Verificações aprovadas | Prova no fonte |
|---|---:|---|
| Instalação limpa e Google isolado, diagnóstico e formulários | 51 | `evidence/034/isolated-final` |
| Atualização 0.33.0 → 0.34.0, MCP antes do Google | 18 | `evidence/034/upgrade-final` |
| Transporte, redação, docs completas e descoberta do Planejador | 157 | `evidence/034/docs-final` |
| Navegador, concessão de criativo, acessibilidade e formulários | 99 | `evidence/034/browser-final` |
| Consumidor proposto, respostas sintéticas, Google antes do MCP | 28 | `evidence/034/core390` |
| Consumidor proposto, reprodução fiel das consultas do CTO Office | 29 | `evidence/034/cto-replay` |
| Core experimental com o contrato ausente na base 0.33.0 | 5 | `evidence/034/absent` |
| Convivência e integração com Meta 0.24.0 | 36 | `evidence/034/current` |
| Atualização com Meta 0.24.0, Google antes do MCP | 18 | `evidence/034/current-up` |
| Integração com Meta 0.24.1 e LinkedIn 0.21.0 | 36 | `evidence/034/fechamento` |
| Migração com o conjunto de fechamento | 18 | `evidence/034/fechamento-up` |
| Navegador com o conjunto de fechamento | 99 | `evidence/034/fechamento-ui` |
| Documentação pelo transporte do conjunto de fechamento | 100 | `evidence/034/fechamento-doc` |

Os 26 documentos instalados foram conferidos integralmente na bancada por MCP em 89 páginas, 4474672 bytes e zero HTTP externo durante as leituras. No Site-Teste, CORE-ACERVOS.md foi conferido nos 9.675 bytes, SHA-256 `896140738458adf3b3dc4e6c4fce0f557e4f3cc5b2207477e7ea9f4c41242630`. O guia 0.34.0 foi conferido nos 23.087 bytes, SHA-256 `cfb8e0019ef34c4ba010fb76f68b90d7821db64c9b929b34af443969692813a8`. O navegador usado foi Chromium headless shell 156.0.8078.79. As capturas do controle ficam junto à evidência. O inventário de migração confrontou os 205 arquivos instalados do Google com o ZIP. A documentação autenticada, o allowlist do instalador e a sintaxe PHP/JS também foram verificados.

A frota é responsável pela distribuição geral. A URL prevista do instalador para essa etapa é `https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-google-fator3-0.34.0-instalador.zip`. A publicação pública e a conferência dos bytes raw pela frota estão pendentes.

## 5. Banco, migração e correção por nova versão

O banco conserva o mesmo esquema. A concessão de leitura pode ganhar o atributo booleano `origin_ad` por ato do administrador. Grants já existentes começam sem esse acesso. A atualização preservou conexão secundária, opções, revisão, vínculos, credencial cifrada, candidata e tarefa concluída. A execução do novo método usa auditoria local. As consultas de criativos não gravam no Google.

Antes da troca no Site-Teste, foram exportadas no próprio site 26 opções do Google, 114 registros e 2.229 linhas de cron. O mecanismo de pacote registrou backup do instalador anterior. As cópias de banco não incluem salts ou arquivos de estado externos. Para recuperação, preservar o banco, o diretório de estado e as salts conforme MIGRACAO.md. Corrigir software por nova versão. Os testes que usaram identidades, contatos e concessões sintéticos ocorreram apenas em bancadas isoladas.

## 6. Pendências

O mantenedor do Core deve incorporar o consumo e a exibição no contato, publicar sua versão e validar a tela com o operador. No CTO Office, a prova em produção cobre as leituras com o plugin existente. A execução direta de uma nova versão do Core e do Google em produção permanece a cargo dos responsáveis.

O Site-Teste está sem credencial Google configurada e sem destinos de conversão selecionados. A prontidão retorna `f3_google_not_configured`. A prova de criativos reais usou o CTO Office. PMax e carrossel passaram em bancada com dados controlados. A API fornece metadados do vídeo, e a entrega de um arquivo de vídeo exigiria outra origem autorizada.

## 7. Credenciais e configuração do dono

Em Ferramentas → Fator3 MCP Google → Conexão, configurar e ativar a identidade autorizada. Em Serviços e recursos, habilitar Google Ads com leitura, indicar conta anunciante e conferir o developer token e a gerenciadora, quando aplicável. Em Permissões, autorizar a conta. Em Acervo Ads, habilitar a coleta de cliques e conceder ao leitor do Core o acesso local e a consulta do criativo. O contato só precisa do par GCLID/data ou do ID do anúncio de lead. O relatório, os exemplos e a evidência entregue omitem GCLID real, credenciais e respostas brutas privadas.

## 8. Identidade dos arquivos

| Artefato | Nome | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | wp-mcp-google-fator3-0.34.0-instalador.zip | 975572 | `9a5f52f35a4a7c34e21e08d12099dacb05dfdfc99d3d0cc335bde95a2676135c` |
| Fonte | wp-mcp-google-fator3-0.34.0-fonte.zip | 8685871 | `2e84a28642224abbde92749ca3a1a142e0c1f1dab6d1a073ab6a5c3fcb9f716d` |
| Impacto Core | wp-mcp-google-fator3-0.34.0-impacto-base-site-core-fator3.md | 5193 | `6811919e1748f7a02f15014f7a7b52b3d36c24cf2d94970c47b53bf1e212eca2` |

Este é o relatório externo canônico. A cópia congelada no fonte antecede o cálculo da identidade do ZIP.
