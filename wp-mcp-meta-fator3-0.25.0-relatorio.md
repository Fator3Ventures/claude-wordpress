# Entrega — Fator3 MCP Meta 0.25.0

Revisão 1 · 2026-11-13T16:52:14+00:00 · Evolução do pedido MCP Meta 28 / Core 390  
Slug: wp-mcp-meta-fator3 · Versão/build público: 0.25.0 · Estado: **com-pendencias** (aceite da ficha real na Korvena).

## 1. De onde esta versão entra

Instalação limpa ou atualização direta do Meta 0.24.1. Base verificada: instalador de 267153 bytes, SHA-256 `6113dab515dfc26633598cab2bfcd5f48386d4dfee5f8330f4548db7aae1d361`; fonte `6c23572c22ee8f7ffe13f8a657fce4f3c0977d1ab4e391f5ff080393bebc37e0`. Requisitos: WordPress 7.1.4 ou superior e PHP 8.3 ou superior de 64 bits. Laboratório: WordPress 7.1.4, PHP 8.3.6 de 64 bits e MySQL 8.0.46. Instruções centrais e padrão de desenvolvimento: revisão 5 de 02/11/2026; cópias em inputs/.

## 2. Convivência e encaminhamentos

Conjunto fornecido/observado e testado: Core 1.81.1, MCP 0.44.0, Google 0.34.0, LinkedIn 0.21.0 e Pipedrive 0.9.0, com Meta 0.25.0. O Core oficial foi ativado sem patch. O impacto recebido do Core (revisão 1, 11/11/2026) orienta validar a ficha da Korvena. A implementação do consumidor está no Core distribuído; a pendência operacional consta da seção 6. O pedido Meta 28 foi a referência vigente identificada; não foi criado número novo.

Somente o Meta exige substituição para estas correções. O SDK continua em meta-ads-reader/1.0.0 com extensão meta-ad-origin/1.0.0. O Core já interpreta avisos de leitura parcial. Nenhuma alteração de contrato ou pedido adicional para Core, LinkedIn, Google, MCP ou Pipedrive foi identificado. Não foi emitido novo relatório de impacto. O teste de coexistência não inclui envio de Slack, sincronização comercial nem tráfego real de outras plataformas.

Core oficial: instalador `8a03bc5dfd3f94d81a953bb7134a14bacbc6883c5b038b4ef0fee1241c1dcb02`; fonte `9beff6ac439196104f8658abb159aaea2ddd1f635242e6a4ef963306913e1a5b`. Identidade dos demais instaladores: wp-mcp-fator3-0.44.0-instalador.zip: a90aa7f2e91ef1033a4a8c6ec320b1e10b45ef657132a40f8aa4215ffa55d5eb; wp-mcp-google-fator3-0.34.0-instalador.zip: 9a5f52f35a4a7c34e21e08d12099dacb05dfdfc99d3d0cc335bde95a2676135c; wp-mcp-linkedin-fator3-0.21.0-instalador.zip: ebe4363bf55476cbe1ba30df80d8ab6b2362ee2dc379c21762aa42f4a05b1bfc; wp-mcp-pipedrive-fator3-0.9.0-instalador.zip: 42523b9b547fc8820c3917e192c4b48341efbb1da6815c78fcc18f8a373c09c0.

## 3. Mudanças e evidência

| Pedido / caso | Falha reproduzida em 0.24.1 | Resultado em 0.25.0 |
|---|---|---|
| Meta 28 · imagem por hash | HTTP válido sem a imagem solicitada aparecia como consulta completa | Preserva texto; retorna imagem nula, aviso e estado parcial no Core. Hash alheio não serve de substituto. |
| Meta 28 · validade do endereço | URL já vencida bloqueava a busca pelo hash ou era entregue sem alternativa | Descarta o endereço; tenta resolver o hash na conta autorizada. Sem substituta, a leitura é parcial. Sem indício de validade, não inventa data. |
| Meta 28 · vídeo incompleto | A resposta sem arquivo podia aparecer como completa | Mantém o ID e a miniatura disponível; separa avisos de ausência de reprodução e miniatura. |
| Meta 28 · variantes | O vídeo principal podia herdar a reprodução de outro ID | A referência de outra variante permanece identificada como tal; o principal não recebe sua mídia. |
| Meta 28 · texto da foto | A legenda nativa não chegava ao campo Texto | A legenda é usada na ausência de mensagem e corpo. |
| Operação | A tela não explicava o resultado de uma consulta com mídia incompleta | A permissão por ID descreve o estado parcial. O guia do SDK e a ajuda instalada descrevem avisos e campos. |

A versão-base falhou em seis das 38 verificações da matriz de origem. A candidata passou nas mesmas 38, com o adaptador, resolvedor e projetor **reais** do Core e dados controlados da Graph/CDN. O Core validou um PNG conhecido pelos bytes e recusou campanha divergente. Também foram exercitados: revogação durante a leitura, escopo da conta e do anúncio, carrossel, publicação e URL de mídia recusada. Não foram acrescentados verbos remotos, permissões automáticas nem downloads de mídia pelo próprio Meta.

## 4. Instalação e prova da troca

Instalado exclusivamente no Site-Teste pelo MCP `plugins/upload-base64`, com os bytes finais, `expected_slug=wp-mcp-meta-fator3`, SHA-256 da seção 8, sobrescrita e ativação. Recibo: 0.24.1 ativa → 0.25.0 ativa; operação `complete`. Foi uma instalação direta de teste. URL raw: não usada; distribuição pela frota em repositório público não foi executada.

| Ambiente | Verificação | Resultado | Evidência no fonte |
|---|---|---|---|
| WordPress limpo e atualização | Preservação de registros, histórico, opções, retenção e concessões por revisão | 18 verificações de migração, nenhuma falha | evidence/025/clean-install.json, migration.json |
| WordPress com Core oficial | SDK de origem e ficha (resolvedor/projeção); comportamento sem provedor | 38 + 1 aprovadas | origin.json, core-alone.json |
| Navegador do laboratório | Controle de autorização, recarga, revogação, largura móvel e erros de página | 7 aprovadas | ui-origin.json |
| Laboratório com os seis plugins | Versões ativas, descoberta, saúde, autoteste e bytes dos manuais via transporte MCP | 44 aprovadas | combination.json |
| Funcionalidades próprias, permissões, documentação e build | Coletas, histórico, configuração, dataset, exportação, agendamento, fronteiras e empacotamento | 291 aprovadas | evidence/025/totais.json e resultados por suíte |
| Site-Teste após troca | Saúde `ok`, autoteste local aprovado, armazenamento e criptografia prontos; página inicial e /wp-json/ HTTP 200 antes e depois | Completo no escopo local | site-teste.json |
| Site-Teste via MCP | Índice e leitura integral de 32 documentos em 41 páginas; 301118 bytes comparados ao instalador | Todas as revisões e conteúdos SHA-256 coincidem | mcp-documentation.json |

Total de **399 verificações automatizadas aprovadas**, sem falhas na candidata. A contagem exclui a reprodução na base, as sondas pós-instalação e a leitura documental do site compartilhado. Todos os ambientes isolados foram descartados pelo runner. No Site-Teste o Meta ficou ativo; no momento da verificação havia zero conexões e zero concessões, e o consumidor do Core estava registrado sem seleção. Não se criou credencial, contato ou campanha de teste ali.

## 5. Banco, migração e correção por nova versão

Não há mudança de esquema ou de retenção. Não há reprocessamento de leads, exclusão de histórico ou ampliação de concessão. Antes da instalação foram exportadas as duas tabelas do Meta (553 linhas) e oito opções do plugin no Site-Teste. Não se distribuem backups com valores privados. Antes e depois da instalação o histórico do Site-Teste informou zero linhas e migração concluída; no laboratório a atualização preservou também histórico não vazio, digests de opções e privilégios ligados/desligados. Em caso de falha depois da instalação, preservar o estado e corrigir por nova versão de avanço; não fazer downgrade.

## 6. O que permanece pendente

Em 13/11, o inventário disponível da Korvena mostrava Core 1.81.1 e Meta 0.24.1 ativos, consumidor pronto e concessão de consulta por ID habilitada na conta da campanha. Isso confirma a configuração, não o resultado de uma consulta. A revisão automática bloqueou a abertura do wp-admin em produção porque a autorização desta rodada cobre o Site-Teste. Nenhum pacote foi instalado nem dados alterados na Korvena. Falta ao administrador autorizado abrir um contato do anúncio indicado no impacto, executar **Consultar anúncio na plataforma**, conferir IDs e campos contra o Gerenciador e confirmar download atual (tipo, dimensão e hash sem URL assinada). As evidências históricas de mídia do Meta 0.24.1 não são apresentadas como validação desta versão. Não houve teste com vídeo real nesta rodada.

## 7. Credenciais e configuração do dono

Em **Ferramentas → Fator3 MCP Meta → Configurar**, use uma conexão de sistema com token verificado, escopo ads_read e acesso à conta do anúncio. Em **Consumidores de anúncios**, confira a conta, a concessão de histórico e a permissão independente de **consulta por ID**. O Core deve selecionar a mesma conexão e conta. O consumidor não recebe o segredo. O titular do site controla as autorizações. A consulta ao fornecedor é somente leitura.

## 8. Identidade dos arquivos

| Artefato | Arquivo | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-meta-fator3-0.25.0-instalador.zip](wp-mcp-meta-fator3-0.25.0-instalador.zip) | 268364 | `8ff54d9ec66f29c78982b6c15577436a51b934c54c73cebe88227449580ea530` |
| Fonte | [wp-mcp-meta-fator3-0.25.0-fonte.zip](wp-mcp-meta-fator3-0.25.0-fonte.zip) | 876790 | `397153c833f2a80101174c1371073a5aa0cdfd282eb1eee57ea59ad9ed54dc70` |

Relatório externo canônico. A cópia no fonte é anterior ao fechamento do ZIP; os valores definitivos estão nesta tabela.
