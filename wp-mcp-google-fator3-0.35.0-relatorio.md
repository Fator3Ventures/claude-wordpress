# Entrega — Fator3 MCP Google 0.35.0

14/11/2026 · Implementação e correção · **com-pendencias** na homologação do fornecedor. A versão está ativa no Site-Teste. Relatório externo após o fechamento dos dois ZIPs.

## Base de migração

Atualização direta do Google 0.34.0 para 0.35.0. Identidade WordPress `wp-mcp-google-fator3/wp-mcp-google-fator3.php`. Instalador anterior de 975572 bytes, SHA-256 `9a5f52f35a4a7c34e21e08d12099dacb05dfdfc99d3d0cc335bde95a2676135c`. Fonte anterior de 8685871 bytes, SHA-256 `2e84a28642224abbde92749ca3a1a142e0c1f1dab6d1a073ab6a5c3fcb9f716d`.

A rodada aplicou a revisão 5, de 02/11/2026, de `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`. Os pedidos recebidos estão em `inputs/pedidos-google-51-52.md`. O inventário de entradas e os resultados desta versão estão em `evidence/035/`, dentro da árvore editável do fonte.

## Convivência e encaminhamentos

| Pacote | Versão ativa no Site-Teste | Verificação |
|---|---|---|
| Fator3 Site Core | 1.85.1 | Contrato do leitor de origem, acervo e adaptador de conversões |
| Fator3 MCP | 0.45.0 | Descoberta, leitura documental, atualização, concessão e revogação |
| Fator3 MCP LinkedIn | 0.22.0 | Ativação e convivência no upgrade |
| Fator3 MCP Meta | 0.25.0 | Ativação e convivência no upgrade |
| Fator3 MCP Pipedrive | 0.10.0 | Ativação e convivência no upgrade |

O leitor de origem e os contratos de conversão do Core conservam suas assinaturas. A prova de leitura no Core 1.85.1 incluiu revogar a autorização de consumidor durante uma consulta e conferir a supressão do resultado. A nova configuração do Slack pertence ao Google. Os acompanhantes vigentes operam com seus contratos existentes.

## Mudanças por pedido

| Pedido | Implementação e aceite observado | Estado |
|---|---|---|
| Pedidos MCP Google 51 | Consultas tipadas e genéricas deixam de emitir o cabeçalho `developer-token`. O painel reúne nível do projeto, gerenciadora e versão da API. O preflight, o autoteste, as conversões e o contrato de configuração indicam o nível do projeto. O salvamento deixa de testar o token ou emitir recibo. O nível Explorer permitiu `ads/search`. A verificação Data Manager com `validateOnly` produziu `google_ads.ready=true` na conexão descartável, com HTTP simulado. | implementado, validado-wordpress. Aceite remoto pelo Google pendente |
| Pedidos MCP Google 52 | Acervo, leitores locais e agendas recorrentes conservam a autorização após revogar a credencial MCP usada ao salvar. A identidade Google, as permissões do administrador, a política e o recurso continuam verificados. Uma agenda antiga bloqueada por revogação voltou a despachar um filho. A coleta concluiu e um leitor de acervo conseguiu ler o dia publicado. | implementado, validado-wordpress |
| Tarefas avulsas do pedido 52 | Ao observar bloqueio da tarefa por `f3_google_channel_revoked` ou `f3_google_channel_changed`, reserva-se um incidente por conexão e tarefa antes do envio. O primeiro aviso informa início UTC, recurso e rota de recuperação. A repetição do erro não duplicou os avisos de e-mail e Slack interceptados. `google/status` completo publicou o incidente. | validado-wordpress. Entrega real pelos transportes pendente |

A documentação instalada inclui migração, telas e recuperação. O guia no Site-Teste foi lido nos 24.544 bytes e corresponde ao arquivo do fonte. O navegador confirmou a retirada do campo de token e do controle de remoção, a ajuda do nível, a navegação por teclado e o ajuste das caixas do Ads nas larguras de 390 e 1.440 pixels.

Referência do fornecedor para o encerramento do token e a atribuição de acesso ao projeto. [Google Ads API — developer token](https://developers.google.com/google-ads/api/docs/api-policy/developer-token)

## Instalação e prontidão

Instale o ZIP com sufixo `-instalador.zip` em **Plugins → Adicionar plugin → Enviar plugin**. Para atualização automatizada, valide o SHA-256 e o slug informados ao fim deste relatório. Os mínimos são WordPress 7.1.4 e PHP 8.3. O laboratório executou WordPress 7.1.4, PHP 8.3.6 e MySQL 8.0. A instalação isolada exercitou o diagnóstico de Tag Manager. O painel foi exercitado na bancada integrada. A presença do plugin MCP permite executar as habilidades pelo transporte MCP.

No Site-Teste, o recibo confirmou Google 0.34.0 → 0.35.0, ativo antes e depois, SHA idêntico ao pacote entregue e sondas aprovadas. Uma credencial MCP exclusiva da homologação foi criada, usada e revogada. Na conexão Google sintética, a primeira busca sem nível retornou o bloqueio esperado. Depois da declaração, a busca e a verificação de conversão passaram. O acervo continuou coletando após a revogação. Essas 14 verificações usaram o código instalado e respostas de fornecedor interceptadas.

As gravações da homologação ocorreram numa transação revertida ao final. O instalador temporário de testes foi desativado e removido. A leitura posterior confirmou a ausência do recibo temporário e apenas a conexão original `default`, sem credencial Google. O destino real permanece com `ready=false` e `reason=integration_disabled`. A auditoria administrativa do WordPress registra as operações de homologação.

### Cobertura executada

| Verificação | Resultado |
|---|---|
| Casos unitários do pacote | 1.366 aprovados, 16.220 asserções, zero falhas e zero pulos |
| Regressões 51 e 52 no WordPress | 24 verificações, incluindo continuidade do consumidor, retomada de agenda, restrição de política e deduplicação de avisos |
| Atualização 0.34.0 e convivência | 20 + 7 verificações. Destino Ads previamente pronto preservou a referência e a validade da prova anterior |
| Credenciais e rotação | 49 verificações |
| Leitor de origem com o Core vigente | 22 verificações com respostas sintéticas |
| Navegador | 97 verificações, Chromium 156, 1.440 × 900 e 390 × 844 |
| Documentação via MCP | 26 documentos, 89 páginas, 4.481.017 bytes, 97 verificações, zero HTTP externo durante a leitura |
| Plugin isolado | 5 verificações com o Core e o transporte MCP ausentes |
| Empacotamento | 205 arquivos no instalador. Segunda montagem produziu os mesmos bytes. Paridade integral com a árvore de runtime do fonte |
| Catálogo e sintaxe | 305 habilidades, 44 opções, 54 exemplos e 167 links locais verificados. 422 arquivos PHP passaram no lint |

O servidor de distribuição do PHPUnit respondeu HTTP 403. A suíte foi executada com o bootstrap original, seus providers de dados e hooks de isolamento em um executor local de asserções. A evidência identifica esse executor. As rotinas nativas, o navegador e o MCP utilizaram WordPress e banco reais, em processos separados.

## Banco, migração e recuperação

A migração grava uma declaração de continuidade com escopo do projeto nas conexões antigas elegíveis. O nível continua **Não informado** até a declaração administrativa. O valor cifrado anterior é preservado para reproduzir a assinatura das provas já emitidas, sem ser enviado ao Google. O administrador deve confirmar o nível no Cloud Console, principalmente antes de usar o Planejador. Uma nova identidade ou nova política mantém as exigências de autorização e verificação. As agendas só retomam automaticamente os dois bloqueios de transporte previstos. Outros bloqueios continuam exigindo revisão.

O backup anterior à implantação cobre a tabela de opções e as tabelas do Google de registros e cron. Identificador privado `efd30c19992b930c9a4c2a75e7b3095a`, 2961 linhas, 2616045 bytes, SHA-256 `84ccdaf71710b450db4f299d548db48fb7919898f96d047966650fe40fcd2782`. Ele contém dados sensíveis e permanece no armazenamento de recuperação do Site-Teste. Em caso de inconsistência, preserve o estado e o backup, confira as revisões e entregue a correção numa nova versão.

## Pendências e limites

1. O responsável pela conta de homologação deve autorizar uma credencial Google e uma conta Ads de teste. A resposta de `validateOnly` foi simulada. A aceitação por um projeto real e a confirmação comercial de uma conversão continuam pendentes.
2. O envio real de avisos exige um `admin_email` válido e um Incoming Webhook Slack do canal do site. Os testes verificaram conteúdo, destino, deduplicação e interpretação das respostas com transportes interceptados. O Core 1.85.1 oferece o canal técnico por e-mail. O Google possui uma configuração de webhook própria em **Incidentes**.
3. O binário oficial do PHPUnit não foi executado nesta rodada. A reprodução padrão continua disponível por `phpunit.xml` com PHPUnit 9.6. A versão instalada em produção ficou fora desta rodada.

## Credenciais e operação

Em **Conexão → Identidade**, ative a conta de serviço ou o OAuth do projeto. Em **Conexão → Serviços e recursos → Acesso ao Google Ads**, informe o nível Cloud e, se aplicável, o ID da conta administradora. Selecione os recursos permitidos. Em **Conversões**, configure conta e ação de conversão e verifique o destino. O diagnóstico informa a necessidade de habilitar a Data Manager API e conceder as permissões correspondentes.

Em **Incidentes**, configure o webhook HTTPS do canal Slack. O segredo é cifrado e o painel informa apenas se está configurado. A tentativa de e-mail usa o endereço administrativo do WordPress. A aceitação pelo transporte e o recebimento pelo destinatário são estados distintos. Na tarefa avulsa bloqueada, revise os parâmetros e recrie a intenção por `google/create-job`.

## Identidade dos arquivos

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-google-fator3-0.35.0-instalador.zip | 979405 | `c1fdf87b53e197fca8aa9f93816e1047b065283a3edfca3c44b4c2b16484045a` |
| wp-mcp-google-fator3-0.35.0-fonte.zip | 8876389 | `a8a1e8c4e50128295ad56dee7407d373655a04004f508f8bb918b991c7ac12c8` |

[wp-mcp-google-fator3-0.35.0-fonte.zip](https://chatgpt.com/library?file_id=libfile_fde3_f-517e971fbb7c81919ced2e819d2f0325_32706b9c47908191baafe72f89b6caee&account_id=personal) · [wp-mcp-google-fator3-0.35.0-instalador.zip](https://chatgpt.com/library?file_id=libfile_fde3_f-8194f3dafbf88191a74a9c4e305f0a01_32706b9c47908191baafe72f89b6caee&account_id=personal)
