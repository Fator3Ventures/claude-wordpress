# Entrega — Fator3 MCP Google 0.33.0

Revisão 1 · 10/11/2026, America/Sao_Paulo. Plugin instalado e ativo no Site-Teste. A autorização de uma conta Google real segue pendente.

## 1. Base de migração

A base de desenvolvimento é a versão **0.32.0 entregue pelo outro agente**, com fonte e instalador identificados separadamente. O instalador-base tem 966316 bytes e SHA-256 `e9edc5ba77678df6b3ad4f98ad35138d00a37172436fbd9dae523821f0c37afa`. O ZIP fonte recebido tem SHA-256 `bc7696642b0668c7a522cc0677f059c2b7feaa23b78d67e17c5267ee9a39ea60`. O incremento minor segue o padrão do projeto. A migração direta da base foi testada em WordPress novo. No Site-Teste, o estado encontrado exigiu a troca direta de **0.31.0 para 0.33.0**.

Foram lidos integralmente `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, revisão 5 de 02/11/2026. O cabeçalho mantém slug, basename `wp-mcp-google-fator3/wp-mcp-google-fator3.php`, nome do menu, namespace, autor, licença, Text Domain e Update URI. Requisitos declarados: WordPress a partir de 7.1.4 e PHP a partir de 8.3. Execução efetiva: WordPress 7.1.4 com PHP 8.3.6 e MySQL 8.0.46 na bancada e com PHP 8.3.36 no Site-Teste.

## 2. Convivência e encaminhamentos

| Acompanhante ativo no conjunto | Versão | SHA-256 do instalador usado na bancada |
|---|---|---|
| Fator3 Site Core | 1.80.0 | `2e81a04d0a9f99f1607d5b388c4aa2590bcc0b3b853cda1fa1b7b3530302ec72` |
| Fator3 MCP | 0.44.0 | `a90aa7f2e91ef1033a4a8c6ec320b1e10b45ef657132a40f8aa4215ffa55d5eb` |
| Fator3 MCP Meta | 0.23.0 | `0c5f029f8a167ac8f624c6386f13aaf9f388a8c228538bb623a58e8cebf60065` |
| Fator3 MCP LinkedIn | 0.20.0 | `4b3f7321b81a28bbed6595d6922ec7d388685690d58d278f3f4b3ebc592ee743` |
| Fator3 MCP Pipedrive | 0.9.0 | `42523b9b547fc8820c3917e192c4b48341efbb1da6815c78fcc18f8a373c09c0` |

A base do Meta foi o pacote 0.23.0 já entregue na rodada anterior e ativo no site. A conferência estrutural dos 305 descritores públicos do Google, incluindo entrada e saída, encontrou somente a atualização da versão anunciada nos metadados. A leitura documental por MCP, as cinco operações do Planejador e a interpretação das respostas foram exercitadas com o transporte 0.44.0. Os formulários de recursos são internos ao Google. O resultado dispensa mudanças coordenadas ou relatório de impacto para outro pacote. Os onze plugins instalados no Site-Teste foram comparados antes e depois. A única diferença de versão ou ativação registrada foi a atualização do Google.

## 3. Mudanças por pedido e evidência

| Fluxo analisado | Problema na 0.32.0 | Correção na 0.33.0 |
|---|---|---|
| Consultar recursos | O retorno do formulário anunciava conclusão após erro de acesso ou resposta parcial. Nos painéis de GTM e Search Console, o resultado da consulta era descartado. | Os três painéis informam o desfecho. Um erro ao guardar a consulta nos Serviços tem mensagem própria. Uma página parcial continua utilizável. |
| Consultas concorrentes | Um formulário antigo iniciava a busca, e uma consulta em andamento podia alimentar o cache depois de uma mudança de configuração. | O formulário confere a revisão. Se o contexto mudar durante a leitura, a resposta é descartada. A gravação de uma lista completa usa a chave da identidade que iniciou a busca. |
| Seleção de propriedade e planilha | O campo de propriedade impedia digitar o ID descrito na ajuda. O campo de planilha ignorava as sugestões da consulta. Com JavaScript desligado, campos inicialmente ocultos dificultavam habilitar e preencher no mesmo envio. | GA4 e Sheets aceitam valor conhecido ou sugestão da página consultada. Uma URL de planilha é normalizada pelo validador existente. Sem JavaScript, o administrador pode habilitar, preencher, revisar e confirmar no mesmo fluxo. O servidor preserva os vínculos dos serviços que ficarem desligados. |
| Organização e documentação | O administrador precisava localizar a consulta e relacionar o resultado ao campo de destino. | A tela liga a seleção à consulta de recursos e agrupa verificação, revisão e salvamento. O guia explica como usar ID, URL e sugestões, interpretar listas parciais e refazer consultas desatualizadas. O índice e o guia de migração identificam a versão atual. |

A suíte original da base passou em **1.343 testes e 16.243 asserções**. Dos seis testes acrescentados ao PHPUnit, cinco falharam na base. O sexto confirma que uma página vazia retornada com sucesso continua válida. No candidato, os seis passaram e a suíte completa totalizou **1.349 testes e 16.262 asserções**, com zero falhas, erros, avisos ou testes ignorados. Chamadas Google em testes usaram respostas sintéticas. PHP lint passou nos 200 arquivos PHP do instalador. A checagem documental conferiu 26 documentos instalados, 54 exemplos e 167 links locais. Dois builds produziram bytes idênticos.

## 4. Instalação e prontidão

| Faixa em WordPress real | Verificações aprovadas | Resultado |
|---|---:|---|
| Google isolado | 46 | Ativação limpa, requisitos exatos do WordPress, agenda única, ajuda local, autonomia e diagnóstico. O teste de diagnóstico cobriu administrador, assinante, visitante e nonce. |
| Formulários de recursos | 5 | O WordPress executou os handlers protegidos e comprovou recusa, revisão vencida, falha de persistência e retorno aos painéis GTM e Search Console. |
| Migração pelo transporte MCP | 18 | O MCP trocou o ZIP oficial 0.32.0 pelo candidato. Outra requisição confirmou a nova versão e a conexão selecionada. O inventário final conferiu os 204 arquivos do Google contra o ZIP. |
| Documentação, transporte e Planejador | 157 | Os 26 documentos foram lidos por completo em 89 páginas, com 4.469.135 bytes e SHA-256 de cada documento conferido. O servidor não fez chamadas externas durante a leitura. |
| Navegador com o conjunto ativo | 96 | Três verificações ativaram os acompanhantes. As outras 93 foram do Chromium 156.0.8078.79, em 1440 × 900 e 390 × 844, incluindo formulários reais, navegação, permissões, ausência de transbordamento e salvamento sem JavaScript. |

**Site-Teste.** Instalação única pelo MCP, com `expected_slug` e `expected_sha256`. O recibo registrou a troca e a ativação em requisição PHP independente. A página inicial e `/wp-json/` devolveram HTTP 200 antes e depois. `system/health` informou estado saudável. `google/status` compacto confirmou 0.33.0, estado `idle`, zero erros ativos de agenda e zero incidentes abertos. A prontidão apontou armazenamento, recuperação, executor, incidentes e contexto do Core em ordem. O índice remoto trouxe os 26 documentos. O guia de 22.662 bytes foi lido em seis páginas e comparado integralmente ao do pacote, SHA-256 `9187b11c5606f04bddf3e707defd7e8e600c2fee843b63bdd2ba057de8127d55`. A descoberta no site retornou as cinco operações `ads/keyword-*` e o catálogo do Google informou 305 habilidades.

## 5. Banco, migração e correção por nova versão

A 0.33.0 mantém o schema e o formato dos dados da 0.32.0. Na bancada, a atualização preservou a revisão da configuração, os serviços, o vínculo da planilha, a credencial OAuth cifrada e legível, a candidata, a conexão secundária e o conteúdo de uma tarefa concluída. O instalador dos acompanhantes permaneceu o vigente. A troca deve ser feita por substituição do plugin ativo, sem desinstalação. Reabra os formulários de configuração após atualizar.

Antes da troca no site compartilhado foram exportadas para a área privada do próprio MCP 26 opções do prefixo Google, 114 linhas da tabela de registros e 2.206 da tabela de cron. São cópias com a retenção do serviço. O recibo da atualização também registrou o backup do pacote anterior. Esses backups não cobrem as salts do WordPress ou arquivos externos de estado. O banco compartilhado foi preservado. Em recuperação, conservar as salts e os arquivos que protegem dados cifrados e seguir o procedimento instalado em `MIGRACAO.md`. Qualquer correção de software após esta entrega requer nova versão.

## 6. Pendências e responsáveis

- **Dono da conexão Google:** a conexão `default` está com o canal habilitado e sem credencial ativa. O código de prontidão é `f3_google_not_configured`. Configurar a identidade e o acesso aos ativos autorizados para homologar a leitura no Google. As entregas GA4 e Google Ads estão sem destinos selecionados.
- **Operador de Ads, se houver uso comercial:** validar o nível do projeto, a conta e as permissões antes da homologação do Planejador e das conversões. A descoberta das cinco operações foi verificada sem movimentar uma conta de anúncios.
- **Frota:** a distribuição pública e a implantação em outros sites ficam com o responsável pela frota. Esta rodada instalou somente no Site-Teste. Os testes visuais cobriram Chromium nas duas larguras registradas.

## 7. Credenciais e acesso

Os testes de laboratório usaram contas locais descartáveis, credenciais sintéticas e respostas do fornecedor interceptadas. As verificações no Site-Teste usaram a conexão administrativa MCP já autorizada. Nenhuma credencial Google foi inserida no site. Os artefatos de entrega contêm código, documentação e provas sanitizadas. O fonte conserva as fixtures de teste recebidas da base.

## 8. Arquivos finais

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| `wp-mcp-google-fator3-0.33.0-instalador.zip` | 966668 | `a45ce1bb589452f578b67b7e28b25f2774efc2f250f02d046ff58c9f823c2ca2` |
| `wp-mcp-google-fator3-0.33.0-fonte.zip` | 8397009 | `33eb3988b54a6729de773c57b069d65792eb71c1ee9df6b99756fde620707ca8` |

O instalador possui raiz `wp-mcp-google-fator3/`. O fonte possui raiz `wp-mcp-google-fator3-0.33.0-fonte/`, testes reproduzíveis e evidências da rodada em `plugin/wp-mcp-google-fator3/evidence/033/`.
