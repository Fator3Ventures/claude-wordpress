# Entrega — Fator3 MCP 0.54.0

20/11/2026 · Revisão documental 1. **Pedidos MCP 91**, originado no pedido Core 439. A leitura da carência de aviso de vencimento foi corrigida e homologada no Site-Teste.

## 1. Base de migração

A 0.54.0 admite instalação limpa e atualização direta da 0.53.0. O instalador da base tem SHA-256 `8403d4b5ce901bb3261d00823508b3c7f12507e2283a4d42c5d9822a7463c2a7`. O fonte da base tem SHA-256 `7d45bba94249bd0b9ef687a285809b20e81ef5dc1b5a7a8503bb7d5b9c587c84`. O cabeçalho mantém WordPress 7.1.4 e PHP 8.3 como requisitos mínimos. Bancada com WordPress 7.1.4, PHP 8.4.27 e MariaDB 11.8.6. Site-Teste com WordPress 7.1.5 e PHP 8.3.37.

Foram lidos integralmente `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, revisão 5 de 02/11/2026, a regra comum, a aba do MCP e a entrega do Core 1.99.0. Os hashes do instalador e do fonte fornecidos para o Core coincidem com seu relatório. A revisão 2 do encaminhamento ao MCP apresentou o pedido novo. Foi atribuído o próximo número do canal, 91.

## 2. Convivência e encaminhamentos

O conjunto ativo na bancada de atualização e no Site-Teste foi Site Core 1.99.0, Google 0.41.0, Meta 0.31.0, LinkedIn 0.26.0 e Pipedrive 0.12.0. O Core publica o contrato de configuração 8.47.0. A comparação dos catálogos ativos confirmou os mesmos 172 nomes de habilidades próprias do canal e os mesmos schemas de entrada e saída. A operação de leitura pertence ao Core. O canal transporta e apresenta o resultado.

A integração usa o contrato já publicado pelo Core 1.99.0. A atualização do canal basta para os sites com esse Core; as integrações dos quatro provedores e o Implantador dispensam adaptação para esta mudança. O retorno formal ao Core identifica as revisões do encaminhamento e o aceite do destinatário em `wp-mcp-fator3-0.54.0-impacto-base-site-core-fator3.md`. A mesma versão do retorno está em `docs/IMPACTO-CORE-0540.md` no fonte.

## 3. Mudança e evidência do pedido 91

O Core usa `token_vencendo` como código de um aviso cuja carência é configurada em minutos. Na 0.53.0, o classificador do canal encontrava o componente `token` tanto no nome do membro do mapa quanto na chave que representa o ponteiro exato da folha. Em ambos os casos mascarava o valor que o administrador precisava conferir.

A nova projeção atua somente na resposta de `f3base/config-core-ler` com `nome=f3base_avisos_tecnicos`. Para o mapa, exige o caminho contratado e inteiro entre 0 e 10.080, inclusive. Para a folha exata, exige só duas chaves, `existe` com valor booleano verdadeiro e `valor` com o inteiro na faixa. Na leitura completa, reconhece o mapa nas quatro origens publicadas pelo Core. Um vizinho sensível, um caminho distinto, uma outra opção ou um tipo inválido passa pela política de apresentação vigente. A mudança é local a `SafeOutput`. O remetente continua responsável por autorizar a operação.

| Leitura autorizada no Site-Teste | MCP 0.53.0 | MCP 0.54.0 |
|---|---|---|
| `token_vencendo` no mapa de 18 códigos | `"[redigido]"` | `30` minutos |
| Ponteiro exato do mesmo código | `"[redigido]"` | `{"existe":true,"valor":30}` |
| Folhas de controle | `agenda_parada=30`, `credencial_recusada=0` | Mesmos valores e tipos |
| Texto JSON e conteúdo estruturado | Idênticos | Idênticos, inclusive na chamada separada só da folha |

A revisão da opção permaneceu `6c0d4a7f6213885f3f57c350cc514ff75a5cc024eb7134b9a5f7b08721f3365d`. O ensaio no Site-Teste usou apenas leituras da configuração. Na projeção solicitada, o número de ocorrências visíveis da máscara caiu de duas para zero. O cliente do Site-Teste entrega o texto e o conteúdo estruturado e omite a chave externa `_meta`. O inventário de redações foi verificado diretamente no transporte HTTP MCP autenticado da bancada.

Na bancada, o ensaio do contrato registrou 29 verificações bem-sucedidas em cada fase. O teste HTTP anterior conferiu os dois caminhos exatos em `_meta["fator3/redaction"].paths` e `total=2`. No instalador final verificou `paths=[]`, `total=0` e paridade entre texto e estrutura. O ensaio HTTP final passou em 19 verificações, incluindo valores efetivamente gravados de 0 e 10.080, retorno em `valor`, `valor_efetivo` e `valor_bruto`, padrão declarado 30 nas duas situações, restauração da configuração original e recusa ao editor. A coleção de projeção cobre ainda sete dados inválidos, envelope malformado, credencial sintética vizinha e contextos alheios. Os resultados estão em `evidencias/0540/` e o roteiro em `tools/release0540/README.md`.

## 4. Instalação e prontidão

Na instalação nova, envie o ZIP instalador, ative o plugin e abra **Ferramentas → Fator3 MCP**. Para a distribuição, a frota confere o SHA-256 do instalador e usa `plugins/upload` com `expected_slug=wp-mcp-fator3`, `expected_sha256`, `overwrite=true` e `activate=true`. Endereço previsto após publicação:

`https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-fator3-0.54.0-instalador.zip`

No Site-Teste, o ZIP foi transferido em quatro partes, conferido por SHA-256 e aplicado por `plugins/upload-base64`. A operação `26b9018350ca20d92701fabc18e9075d` confirmou 0.53.0 → 0.54.0, `active=true`, `applied=true` e `recovery_status=applied`. A pré-imagem recebeu o ID `662fc89a95185b2f4276d2a1`. A página inicial e o índice REST devolveram HTTP 200 antes e depois. O estágio foi conferido como ausente. Uma nova requisição confirmou saúde, ferramentas prontas, marcador de cron ativo e zero recuperações pendentes.

| Prova complementar | Resultado |
|---|---|
| Instalação e preservação | 10 verificações na instalação isolada e 18 na atualização direta. Os 481 arquivos nas duas árvores instaladas coincidiram com os bytes do ZIP. Opções, perfil, expirações OAuth e agenda foram lidos em novo processo. |
| Autenticação | As duas rotas publicadas receberam HTTP 401 sem credencial e com Bearer inválido, nos quatro casos de cada ambiente. O Site-Teste retornou desafio Bearer nas quatro respostas. |
| Documentação | 210 verificações documentais aprovadas. A descoberta, o schema, a paginação e a rejeição de hash obsoleto foram testados em bancada. No Site-Teste, três páginas de `system/guide` reconstruíram os 2390 bytes de `release-0540`, SHA-256 `255b39b64c830019153b449076b09961b40175ae918034a2e269bc6f065f53c8`, idênticos à fonte. |
| Painel e código | Sete abas a 360, 768 e 1440 px no Chromium. O ensaio preservou o valor gravado após simular uma mudança. Os 474 arquivos PHP do instalador passaram pelo lint. |

## 5. Banco, migração e correção por nova versão

O schema de persistência continua em 2. A projeção nova é feita na resposta, após a execução da consulta, sem migrar tabelas, gravar a opção do Core, reclassificar incidentes ou enviar e-mail. A pré-imagem cobre os arquivos do plugin. O registro da instalação e os recibos administrativos seguem a política do executor. Uma correção de software após a implantação exige outra versão.

## 6. Aceites pendentes

O aceite técnico do MCP 91 foi concluído no Site-Teste. A frota deve distribuir o ZIP e executar a mesma leitura administrativa em cada destino. A observação de sete dias do pedido **Core 439** verifica a entrega de avisos sob as carências configuradas. O aceite de campo do **MCP 90** acompanha os episódios de `agenda_parada` em 14 sites. Os dois acompanhamentos permanecem sob responsabilidade da frota. A correção desta entrega permite consultar o prazo efetivo por site.

## 7. Credenciais e configuração do dono

O operador usa a autorização existente do MCP e uma conta com `manage_options` e acesso à operação. O serviço do Core precisa estar habilitado. A entrega não requer credencial de fornecedor nem nova senha. Os dados temporários e bancos descartáveis da bancada foram removidos. Nenhuma política de aviso do Site-Teste foi modificada pelo ensaio.

## 8. Identidade dos arquivos

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-fator3-0.54.0-instalador.zip | 976085 | `175b01ba1eeacc6655e739b70b694c2127c7df7e5858b180c773da8630392202` |
| wp-mcp-fator3-0.54.0-fonte.zip | 5365785 | `00822c5685b065e3badab94b22dde4a6972eca2dcfb4948ff84c8905e1dea57e` |
| wp-mcp-fator3-0.54.0-impacto-base-site-core-fator3.md | 3647 | `cec4a418cc838217206ea5842315c34b6cfaeeef6158dd4ac7c32f346ed0af8e` |

Digest SHA-256 do inventário de runtime: `51d2472b110d5eaa5b53b42d9a53deaa916884e452254ac9d9b913a6b11240ea`.

O instalador reconstruído a partir do fonte entregue reproduziu integralmente os bytes do ZIP homologado.
