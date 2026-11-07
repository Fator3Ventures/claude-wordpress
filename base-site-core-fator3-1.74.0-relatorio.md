# Entrega — Fator3 Site Core 1.74.0

Revisão 1 · 2026-11-07T08:19:22-03:00 · Implementação do pedido 374  
Slug `base-site-core-fator3` · Contrato administrativo `8.35.0`  
**Status: com-pendencias.** A correção passou nos testes do wp-admin e está ativa no Site-Teste. O aceite do pedido com a credencial real em korvena.com.br depende da implantação naquele site.

## 1. De onde esta versão entra

Instalação nova ou atualização direta **1.73.0 → 1.74.0**. A retomada usou o candidato, a bancada e os testes da conversa anterior. O pedido 374 da aba de 07/11 foi conferido contra a cópia anexada. A correção adicional para rascunhos integra o ZIP final identificado na seção 8.

A árvore de migração corresponde aos 939 arquivos do instalador-base anexo, de 4.332.427 bytes e SHA-256 `6675c1e7436e1195f6f7559a9baf62e049d871d145c84f19c04ac67f8d25655e`. O fonte-base tem SHA-256 `dcb645dd56d27eda36d011f97a2c374b3274bef8d45c2296a5a01c1cb4fda421`.

Requisitos do projeto: WordPress ≥ 7.1.4 e PHP ≥ 8.3 de 64 bits, instalação única. Laboratórios nativos: WordPress 7.1.4, PHP 8.3.6 e 8.4.27, MariaDB 11.8.6. Site-Teste: WordPress 7.1.4 e PHP 8.3.36. As duas referências centrais, `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, foram lidas na revisão 5, de 02/11/2026.

## 2. Convivência e encaminhamentos

| Acompanhante | Versão ativa no Site-Teste | Verificação desta rodada |
|---|---:|---|
| Fator3 MCP | 0.41.0 | Instalação com hash e slug, execução de abilities, leitura de documentação, sondas e saúde |
| Fator3 MCP Google | 0.31.0 | ZIP, fonte e relatório anexos conferidos. A prontidão reconheceu o Core. Armazenamento, recuperação e executor em estado `ok`. A conexão Google aguarda credencial |
| Fator3 MCP Pipedrive | 0.8.0 | ZIP, fonte e relatório anexos conferidos. O ciclo do Core registrou a etapa Pipedrive como verificada. O provider manteve a operação comercial desautorizada no site |
| Fator3 MCP Meta | 0.21.0 | Ativo após a troca. O editor alterado, o token CAPI e a política de aquisição pertencem ao Core |
| Fator3 MCP LinkedIn | 0.19.0 | Ativo após a troca. O contrato de Lead Sync e a seleção do cliente permanecem vigentes |

Os hashes dos pacotes examinados estão em `evidence/1740/packages.json`. A mudança afeta o transporte HTML privado da seção Meta no wp-admin. O Core preserva os nomes das opções, o contrato de configuração por MCP, a lógica de aquisição e os clientes Google e Pipedrive. A análise no planejamento e no encerramento identificou zero adaptações necessárias nos acompanhantes. O Site-Teste já tinha as versões vigentes e recebeu somente o Core.

## 3. Mudanças e evidência

| Pedido exato | Causa observada na 1.73.0 | Implementação e prova |
|---|---|---|
| Core 374.1 — exibir o grupo de Lead | O catálogo definia um objeto sem declarar os subcampos que o renderizador do painel utiliza. Era emitido um input de texto vazio | A tela mostra o seletor do modo padrão e o mapa de IDs de formulário com modo próprio. A gravação, releitura de dois mapeamentos e remoção de exceções passaram pelo formulário real. O mapa vazio é editado como `{}` |
| Core 374.2 — encaminhar apenas as alterações | A validação da área exigia a lista completa e a pré-checagem global considerava revisões de campos fora da edição | O POST normal da tela Meta contém apenas as opções editadas e suas revisões. Cada grupo editado segue completo. Um rascunho recusado precisa de nova edição ou de seleção explícita para ser reenviado. O navegador inspecionou os nomes enviados e a resposta da próxima página. A escrita manual sem JavaScript continua sujeita às guardas do servidor |
| Core 374.3 — salvar os campos válidos | Um erro de tipo ou revisão abortava toda a seção | O servidor valida e grava cada opção editada da seção, preserva o valor anterior da opção recusada e mostra o erro junto ao campo. O token válido foi rotacionado no mesmo POST que continha um ID de formulário inválido. Outro processo confirmou a cifra e o valor esperado. O transporte foi salvo em POST separado e relido |
| Regressões e autorização | Um POST parcial precisa distinguir omissão permitida de truncamento, conflito ou tentativa de mudança fora da área | Exercitados grupo incompleto, seção indevida, sentinela ausente, exclusão fora do envio, contexto já consumido, edição concorrente e assinante sem acesso à tela, à leitura de configuração e à documentação administrativa |

O PHP mantém nonce, capacidade `manage_options`, contexto vinculado a usuário e área, sentinela e controle de revisão por opção. A seção Meta dá confirmação por opção. As regras das outras seções continuam utilizando validação conjunta. O patch também conserva a representação de mapas que usam um ID literal igual ao marcador interno de rascunho. Nenhum asset público de visitantes mudou.

## 4. Instalação e prova da troca

O inventário inicial confirmou o domínio autorizado e o Core 1.73.0 ativo. A transferência do ZIP terminou com 4.336.155 bytes. A leitura do arquivo no servidor confirmou o SHA-256 antes da troca. A operação `plugins/upload-base64` usou `zip_path`, `activate:true`, `overwrite:true`, `expected_slug:base-site-core-fator3` e `expected_sha256` da seção 8.

O recibo `c611f6a7eee5fab2871f3dc2e5efde79` registra versão anterior 1.73.0, versão efetiva 1.74.0, `applied:true` e plugin ativo. O Core informou inicialmente `atualizacao_pendente`. Uma nova requisição confirmou o ciclo `00f1c63f-1ce4-4873-add2-350211ed536b` concluído, confirmado no executor, com zero falhas. Cabeçalhos, navegação e a etapa Pipedrive ficaram verificados.

| Ambiente e cenário | Resultado | Evidência no fonte |
|---|---|---|
| WordPress nativo, PHP 8.3.6 | 144 verificações PHP e 30 no Chromium aprovadas, incluindo acesso pelo wp-admin, token isolado, transporte isolado e resultado parcial | `evidence/1740/php83/` |
| WordPress nativo, PHP 8.4.27 | As mesmas 174 verificações aprovadas | `evidence/1740/native-run.json`, `browser.json` e resultados individuais na mesma pasta |
| Instalação limpa e isolada, atualização e reativação | Ambos os runtimes passaram. Na migração, 993 amostras e a configuração semeada conservaram seus hashes | `fresh--instalacao-limpa-1740.json`, `upgrade--upgrade-1730-1740.json` e `upgrade--reativacao-1740.json` |
| Integridade de código e build | 597 arquivos PHP com lint aprovado, sintaxe dos dois JS modificados conferida e 941 arquivos do instalador idênticos aos de cada uma das quatro instalações locais. O build reproduziu o ZIP byte a byte | `evidence/1740/lint.json`, `runtime-manifest.json` e `resumo.json` |
| Site-Teste, execução após troca | Home, REST e login responderam HTTP 200. MCP saudável, recuperação sem pendência, zero avisos de configuração do Core. Os 14 arquivos adicionados ou modificados têm o SHA-256 do instalador no servidor | `evidence/1740/site-teste.json` |
| Configuração após a troca | O Lead permaneceu `imediato`, sem exceções. O transporte permaneceu `navegador` com PageView e Lead. As revisões antes/depois são idênticas. A leitura remota do token é redigida | Mesmo arquivo |

A descoberta de `f3base/documentacao-ler` retornou o schema e o índice da versão instalada. Leitura da release anterior antes da troca e da atual depois da troca feita pelo MCP. Quatro documentos da 1.74.0 foram lidos integralmente e comparados com o texto do pacote: release em duas páginas, guia do painel em três, guia dos agentes em uma e índice principal em seis. O arquivo `docs/RELEASE-1.74.0.md` tem 15 linhas, SHA-256 `3285ff4cf2a75dc0398484c2e5ab304852997283a41d6242501cb48765ed5b2a` e cursor final nulo. A solicitação de arquivo fora da lista retornou `documento_nao_catalogado`. A prova local do leitor registrou zero chamadas HTTP.

A área temporária `wp-content/upgrade` terminou com a mesma listagem inicial. O ZIP de transferência já estava ausente na conferência de limpeza. Nenhuma fixture, conta sintética ou credencial de teste foi criada no WordPress compartilhado. A instalação foi direta no Site-Teste. A publicação raw para distribuição na frota permanece sob responsabilidade da frota.

## 5. Banco, migração e correção por nova versão

A 1.74.0 conserva o schema, as opções e a captura de contatos. O ciclo de atualização existente recompõe metadados e projeções. Salvar na tela modifica somente as opções efetivamente aceitas e seus registros de procedência. O Core cifra o token e exige exclusão explícita para apagá-lo. Resultados parciais indicam ao operador exatamente o que precisa de revisão.

O MCP conservou a pré-imagem dos arquivos do plugin sob `3081142b723161052ebb0320`. No site compartilhado, a rodada preservou as configurações da Meta e não realizou alteração de dados comerciais nem exportação de banco. As escritas de teste ocorreram em bancos descartáveis. Para falha de migração, consultar `f3base/saude-ler`, identificar a etapa registrada e retomar pelo mecanismo do Core. Correções de software posteriores recebem nova versão.

## 6. O que permanece pendente

**Core 374 em korvena.com.br — frota e responsável pela credencial.** Após instalar a versão em produção, o dono digita o token no wp-admin e salva somente esse campo. Conferir o recibo e a presença mascarada. Em nova operação, salvar apenas o transporte permitido pela configuração e reler o modo. A autorização desta rodada abrangeu o Site-Teste. O token da Korvena não foi acessado e seu salvamento em produção continua sem comprovação.

O POST autenticado do painel foi exercitado em WordPress local nas duas versões de PHP. No Site-Teste, a validação abrangeu a troca real, a identidade do código, a configuração preservada e a saúde. O aceite de um evento pela Meta exige recibo do fornecedor e é distinto do teste de persistência do token. Não houve envio de evento à Meta, nem operação comercial Google/Pipedrive iniciada para esta prova.

## 7. Credenciais e configuração do dono

Acesse **Site Core → Configurações → Meta** com uma conta que tenha `manage_options`. Use o token de eventos emitido para o dataset em `f3base_meta_capi_token`. Para envio pelo servidor, confira o Pixel/dataset e os pré-requisitos do transporte antes de selecionar a modalidade. O recibo de gravação confirma persistência. A verificação de permissão pela Meta ocorre no envio de evento. Credenciais reais não integram a entrega.

## 8. Identidade dos arquivos

| Artefato | Arquivo | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [base-site-core-fator3-1.74.0-instalador.zip](base-site-core-fator3-1.74.0-instalador.zip) | 4336155 | `a77d89d369e3c106383e83aae43bb0211ff1b7952f60ed1e97a0b2595066d1ae` |
| Fonte | [base-site-core-fator3-1.74.0-fonte.zip](base-site-core-fator3-1.74.0-fonte.zip) | 9187010 | `c3e1cbb05c982b746b663005c0368bf51ac04700df16bd591a564e64eed35e36` |

Relatório externo canônico. A cópia congelada dentro do fonte antecede o fechamento do ZIP e por isso remete a esta tabela para sua identidade final.

Checklist da seção 14 conferido. Fonte e instalador têm raízes distintas, a documentação integra o runtime e as evidências do laboratório estão limitadas ao fonte. A validação comercial em produção permanece aberta conforme a seção 6.
