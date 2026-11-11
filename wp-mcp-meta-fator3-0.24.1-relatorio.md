# Entrega — Fator3 MCP Meta 0.24.1

11/11/2026 · Implementação e correção · **Pedido MCP Meta 28 / Pedidos core 390**. A parte do Meta está implementada. O aceite da integração oficial na Korvena permanece pendente.

## 1. Base de migração

A referência da frota nesta rodada era o Meta 0.23.0 (instalador: 259.876 bytes; SHA-256: 0c5f029f8a167ac8f624c6386f13aaf9f388a8c228538bb623a58e8cebf60065). A funcionalidade foi instalada primeiro no Site-Teste como 0.24.0. A conferência do catálogo MCP mostrou que a descrição da operação de concessão só mencionava histórico local. O patch 0.24.1 corrige a apresentação e a declaração dos efeitos, mantendo o binário anterior imutável. Foram validados os dois caminhos diretos até a entrega: 0.23.0 → 0.24.1 (frota) e 0.24.0 → 0.24.1 (Site-Teste). Só é necessário instalar o ZIP final.

Foram lidos integralmente instrucoes-agentes-plugins-fator3.md e padrao-desenvolvimento-plugins-fator3.md, ambos revisão 5 de 02/11/2026, e o pedido de 11/11/2026. O pedido atual autoriza a nova leitura de anúncios; gestão de anúncios, criação de lead e atribuição comercial não mudam de responsável.

## 2. Convivência e encaminhamentos

No inventário inicial do Site-Teste: MCP 0.44.0, Google 0.33.0, LinkedIn 0.20.0, Pipedrive 0.9.0, Core 1.80.0 e Meta 0.23.0. Ao final, o inventário confirmou MCP 0.44.0, Google **0.34.0**, LinkedIn **0.21.0**, Pipedrive 0.9.0, Core 1.80.0 e Meta **0.24.1**, ativos. As atualizações de Google e LinkedIn ocorreram em paralelo; esta rodada substituiu apenas o Meta. As notas instaladas google/CHANGELOG.md e linkedin/RELEASE-0.21.0.md identificam os Pedidos MCP Google 50 e MCP LinkedIn 24, também vinculados ao Core 390. Cada provedor resolve a origem da própria plataforma, com concessão separada. Não foram identificadas alterações exigidas de LinkedIn, Google, MCP ou Pipedrive: nenhum deles precisa ler os novos campos, registrar outro consumidor ou mudar uma concessão. A coexistência foi verificada no inventário e na saúde do WordPress compartilhado; seus fluxos comerciais independentes não foram homologados aqui.

**Impacto funcional sobre o Core:** wp-mcp-meta-fator3-0.24.1-impacto-base-site-core-fator3.md. O Core oficial 1.80.0 registra o leitor, mas não chama a nova extensão. O fonte contém o patch experimental em integration/core/ (aplicável com patch -p1) e a evidência de integração com a cópia do destinatário. Não foi distribuída uma versão do Core. O impacto solicita implementação e aceite coordenado; não encerra o pedido.

## 3. Mudanças e evidências por pedido

Anteriormente, a integração de histórico podia informar ID e nome do criativo de uma observação, mas não consultava a peça atual por conta e anúncio. Agora o cliente PHP registrado oferece `$client->ad_origin(['connection_id' => $conexao, 'account_id' => $conta, 'ad_id' => $anuncio])`, com um array de três strings, conforme o manual META-ADS-READER.md. O contrato da extensão é meta-ad-origin/1.0.0. O contrato de histórico meta-ads-reader/1.0.0 continua com status e query locais. Nenhuma nova ability pública para consultar anúncios por ID foi criada.

O resultado identifica anúncio, conjunto e campanha e fornece os nomes, texto principal, título, descrição, botão, destino, mídia, post vinculado, permalink do Instagram e link do Gerenciador conforme disponíveis. Distinção entre mídia principal, cartões e alternativas; campos indisponíveis são nulos. Para vídeo: ID, miniatura e reprodução quando concedidos. Para mídia assinada: instante da consulta e validade conhecida ou desconhecida, sem prometer disponibilidade futura. O plugin não copia o arquivo de mídia para o WordPress nesta operação.

A configuração da permissão é local, por consumidor, conexão e conta, com revisão esperada e controle explícito separado no painel. Antigas concessões não adquirem a permissão. A consulta usa apenas GET à Graph API, começa na conta selecionada, confere o ID e a conta retornados e revalida a concessão antes dos acessos e da entrega. Uma revogação durante a consulta impede a entrega dos dados. A auditoria não registra texto, token ou URL assinada.

**326 verificações automatizadas aprovadas, sem falhas na rodada final:** 28 no novo contrato e no adaptador do Core; sete no navegador (controles, persistência, revogação e largura móvel); uma com Core ativo e provedor ausente; 35 nos dois caminhos de migração; 14 de integridade documental; 241 em funcionalidades e regressões do Meta. Testes nativos em WordPress 7.1.4 / PHP 8.3.6 de 64 bits e MySQL, com schema e opções reais; respostas Graph controladas e sem envio externo de e-mail. A conferência de 36 PHP por sintaxe e do manifesto do instalador é separada desses 326 casos. O fonte contém as verificações individuais em evidence/024/.

**Fornecedor real:** o conector oficial da Meta retornou quatro anúncios ativos na campanha 120256596454580242. Para AD01 (120256886100270242), foram conferidos o vínculo com a campanha e o conjunto, os nomes, o ID do criativo e duas imagens de 1.080 × 1.920. Uma imagem foi baixada integralmente da CDN: HTTP 200, image/png, 1.450.433 bytes, SHA-256 7072a7d6fd562ae0a3c4021907e350a91aad6226e60da33f5cd51cf48342686b. Não houve escrita na conta de anúncios. Essas leituras comprovam o anúncio e a mídia; não comprovam todos os campos pela nova integração instalada na Korvena. Fonte do mapa de campos público: SDK oficial facebook-python-business-sdk, classe AdCreative; código e manuais do plugin descrevem a projeção usada.

## 4. Instalação e prontidão

Instalar wp-mcp-meta-fator3-0.24.1-instalador.zip, com raiz wp-mcp-meta-fator3/ e basename wp-mcp-meta-fator3/wp-mcp-meta-fator3.php. Requisitos declarados: WordPress ≥ 7.1.4 e PHP ≥ 8.3 de 64 bits. Não há obrigação de testar versões inferiores; a combinação efetivamente executada está na seção 3. O Meta inicia sozinho. Para usar o anúncio de origem, instalar o consumidor oficial compatível quando disponível, selecionar a conta no Core e autorizar Consulta por ID em Ferramentas → Fator3 MCP Meta → Configurar → Consumidores de anúncios.

**Site-Teste ao fechar:** pacote ativo, estado de instalação complete, saúde ok e autoteste local aprovado. A página inicial e o índice REST responderam HTTP 200. O catálogo expõe explicitamente a configuração local e a consulta opcional; meta/capabilities confirmou a extensão, desabilitada por padrão. O MCP devolveu a íntegra dos **32 documentos, em 41 páginas**, com hashes do conteúdo remontado iguais aos do instalador. Zero conexões Meta, zero concessões e zero agendas ativas no teste compartilhado. Os cenários com credenciais sintéticas ocorreram apenas no laboratório isolado. Evidências em evidence/024/site-teste.json e mcp-documentation.json.

## 5. Banco, migração e correção

Não há mudança de schema, cron ou retenção. A permissão adicional fica no registro cifrado da concessão; ausência significa desligada. Os testes compararam contagens e digests dos registros de negócio, histórico e opções, além de agendas, jobs pausados, recibos de mensagem e progresso de migração. A atualização da 0.24.0 preservou também uma permissão remota marcada; a atualização da 0.23.0 preservou a concessão local sem liberá-la para o provedor.

No Site-Teste, antes da primeira troca, foram feitos backups privados das duas tabelas do Meta e das oito opções com o prefixo do plugin. Os recibos de instalação conferem slug e SHA-256 e o MCP mantém sua pré-imagem. Não foram apagadas tabelas, inseridas credenciais de produção ou ativadas fixtures no ambiente compartilhado. Correção posterior requer nova versão; não há procedimento de downgrade nesta rodada.

## 6. Pendência e responsáveis

O mantenedor do Core deve incorporar o adaptador e ligá-lo à atribuição da URL v1 ou do formulário nativo. O responsável pela Korvena deve habilitar a concessão por ID depois que os pacotes oficiais estiverem disponíveis e executar a consulta a partir do Core. Comparar campos e download com o anúncio real e registrar ausências do fornecedor. A Korvena estava com Meta 0.23.0 e Core 1.80.0; não foi alterada nesta rodada. Um teste de vídeo real também não foi realizado: reprodução, miniatura e indisponibilidade do vídeo foram verificadas por fixtures, e a confirmação no fornecedor usou uma imagem real.

## 7. Credenciais e efeitos

O Core não recebe token nem chave do aplicativo. A consulta ao fornecedor exige credencial vigente verificada com ads_read e acesso atual à conta. Eventual acesso negado à publicação ou ao vídeo é indicado; a chamada não amplia a permissão na Meta. Esta entrega não envolve publicação em produção, envio a terceiros, compra de mídia ou troca de segredo.

## 8. Artefatos e integridade

- **wp-mcp-meta-fator3-0.24.1-instalador.zip** — 267153 bytes; SHA-256: 6113dab515dfc26633598cab2bfcd5f48386d4dfee5f8330f4548db7aae1d361. Único ZIP instalável.
- **wp-mcp-meta-fator3-0.24.1-fonte.zip** — 835205 bytes; SHA-256: 6c23572c22ee8f7ffe13f8a657fce4f3c0977d1ab4e391f5ff080393bebc37e0. Contém código, build, runtime, testes, evidências sanitizadas, patch do Core e relatório anterior ao fechamento.
- **wp-mcp-meta-fator3-0.24.1-impacto-base-site-core-fator3.md** — pedido de integração ao Core, acompanhado do patch no fonte.
