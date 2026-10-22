# Entrega — Fator3 MCP 0.27.0

Revisão 1 · Data/hora: 2026-10-22T18:27:36-03:00 · Rodada: implementação dos Pedidos MCP 63 e 64 e resposta ao impacto LinkedIn 0.6.0.
Slug/basename: `wp-mcp-fator3` / `wp-mcp-fator3.php` · Versão/build 0.27.0.
Status: **com-pendencias de aceite no cliente Claude e de contrato de serviço LinkedIn**. A implementação dos pedidos 63/64 está pronta e validada no escopo descrito; não equivale ao encerramento de todos os aceites externos.

Relatório externo canônico. A cópia dentro do fonte é identificada como anterior ao fechamento; tamanho e hash do próprio fonte são completados somente aqui.

## 1. De onde esta versão entra

Instalação nova ou atualização direta da **0.26.1**, última base aceita. Instalador-base imutável: 841342 bytes, SHA-256 `ed8035e6e326ac3c2021bac1ae9c11fde39c26686e1763299b445c3992cb5384`. Fonte-base: 3127316 bytes, SHA-256 `6457cebb4b4d72489dd40181214c8d85d102e303e40d662e7730c31da67c7c1b`. Os arquivos aceitos não foram substituídos. Não há intermediária necessária.

Entradas: `Fator3 MCP(4).md` (63/64 abertos), impacto LinkedIn 0.6.0 revisão 3, fontes/instaladores/relatórios Core 1.47.0 e LinkedIn 0.6.0; padrão comum revisão 4. Documentos e identidades em `docs/entradas/0270` e `evidencias/0270/entradas.json`. Numeração dos pedidos, identidades publicadas, endpoints, Text Domain e Update URI preservados. Versão minor nova; nenhuma candidata foi instalada e depois alterada nesta rodada.

Requisitos comprovados: WordPress **7.1.2** e PHP **8.3.6**, instalação limpa em processo novo, além de WordPress 7.1.3/PHP 8.3.6/MySQL 8.0.46 em laboratório e WordPress 7.1.3/PHP 8.3.36 no Site-Teste. Não há alegação de suporte a runtimes menores.

## 2. Convivência e encaminhamentos

| Acompanhante | Laboratório e Site-Teste | Escopo efetivamente conferido |
|---|---|---|
| Fator3 Site Core | 1.47.0 | ativação, coexistência e catálogo; nenhum código ou fluxo comercial alterado |
| Fator3 MCP Google | 0.17.0 | coexistência; chave de idempotência acrescentada pelo canal traduzida; capacidades preservadas |
| Fator3 MCP Meta | 0.4.1 | coexistência e catálogo; rótulos próprios do Meta não são reescritos |
| Fator3 MCP LinkedIn | 0.6.0 | descritor explícito, escrita humana sintética, antes/depois, identidade, perfil, ativo e revogação |

As versões recebidas já estavam instaladas no Site-Teste e foram preservadas. WP Super Cache 3.1.4, Yoast 28.7 e DreamHost Panel Login 1.0.0 também permaneceram ativos. O MCP funciona isolado; não foi criada dependência de ordem ou de versão dos acompanhantes para as funções próprias.

Impacto pertinente: **`wp-mcp-fator3-0.27.0-impacto-wp-mcp-linkedin-fator3.md`**, revisão 2, entrega, `decisao-necessaria / validacao-coordenada`, aberto para **Pedidos LinkedIn 8(d)**. A revisão 1 nasceu antes da implementação. **Pedido LinkedIn 10** revalidado: a 0.6.0 registra o descritor humano sem depender do adaptador legado restrito à 0.5.0.

A proposta `mutation-service-audit/1.0.0` separa principal de serviço, concessão/revisão opacas, introspecção pública e leitura administrativa autorizada. **É proposta; não há runtime desse contrato nesta versão.** A 0.6.0 não emite evento de serviço e não fornece essa fronteira pública de introspecção/leitura. O responsável LinkedIn deve confirmar ou contrapropor o contrato; MCP implementará a parte dependente após alinhamento. O contrato humano `mutation-audit/1.0.0` permanece restrito, sem assumir o administrador do consentimento. Não foi declarado encerrado o registro central de todos os envios CAPI.

Não se identificou alteração técnica de contrato que exigisse encaminhamento ao Core, Google, Meta ou Implantador. Não foram modificados pacotes alheios nem enviados documentos a terceiros. APIs comerciais dos acompanhantes e o pacote Implantador não foram homologados nesta rodada.

## 3. Mudanças e evidência

| Pedido | Comportamento entregue | Estado / prova |
|---|---|---|
| MCP 63(a,c) | rótulos em palavras e português no registro público; painel usa o mesmo rótulo; IDs originais preservados | implementado / validado-wordpress; oito verificações locais, catálogo remoto e abas Clientes conectados/Registro |
| MCP 63(b) | descrição do `idempotency_key` acrescentado pelo transporte em português, inclusive para acompanhantes | implementado / validado-wordpress; schema efetivo local e remoto; parâmetros próprios de terceiros preservados |
| MCP 64(a) | CIMD aceita capacidades extras se a lista contém `authorization_code`/`code`; não anuncia nem emite grants extras | implementado / validado-wordpress; documento real chega ao consentimento no Site-Teste; 42 verificações novas, 48 de regressão e 29 de fluxo HTTP |
| MCP 64(b) | `system/oauth-diagnostics` e seção no Diagnóstico exibem identificador, categoria e hora | implementado / validado-wordpress; falha sintética correlacionada entre autorização, rota e tela |
| LinkedIn 10 e 8(d) | revalidação do descritor humano; proposta separada para serviço | 32 verificações próprias da fronteira atual; proposta de serviço pendente de alinhamento/implementação conjunta |

**Rótulos.** O mapa único contém 171 rótulos, incluindo metatools e as três leituras nativas `core/`; o catálogo remoto visível continha 164 habilidades próprias e três nativas, todas iguais ao mapa português (167, zero divergências). Os metatools mantêm seus identificadores públicos e também receberam rótulos. Os callbacks nativos WordPress são identificados pela origem; não se atribui sua propriedade ao MCP. O painel não mantém outra tradução independente. Exemplos: “Plugins: enviar e instalar pacote” e “Registro: consultar antes e depois de uma operação”.

**CIMD.** Quando informados, `grant_types` e `response_types` devem ser listas textuais não vazias que contenham, respectivamente, `authorization_code` e `code`. Outros valores são ignorados na negociação. Valores não textuais, vazios ou com controle são recusados. Ausência dos campos conserva o default anterior de registro. Continuam inalterados: HTTPS público, prevenção de SSRF, identidade exata do documento, nenhum redirecionamento do download, limite 64 KiB, cache no máximo uma hora, `none`, redirect registrado, PKCE S256, audiência, perfil e consentimento. O endpoint de token continua recusando JWT bearer com `unsupported_grant_type`.

**Diagnóstico.** `system/oauth-diagnostics` recebe `{}`; retorna `entries` com somente `diagnostic_id`, `category`, `time` (Unix), além de total, limite 128, ordem e retenção. Exige `manage_options` e política da conexão MCP. A tela usa a mesma projeção. Não retorna URL/hash do cliente, código, token ou payload. A leitura não modifica o anel nem faz rede; anel ausente é vazio, corrompido/ilegível é `oauth_diagnostics_unavailable`, symlink é recusado. Filtra pelo site e valida o formato de cada registro. A retenção continua sendo as últimas 128 falhas, sem limpeza administrativa implícita.

## 4. Instalação e prova da troca

Use o instalador da seção 8, `expected_slug: wp-mcp-fator3`, `expected_sha256` exato e `overwrite:true`. A frota pode usar `plugins/upload` após publicar/conferir a URL raw; **não houve push ou implantação na frota nesta rodada**. No Site-Teste, o arquivo final foi enviado em partes, conferido por hash e instalado por `plugins/upload-base64` com caminho local, `activate:true` e conferência em novo worker PHP.

Operação `ed41ff0f823f3ea48530789e70ab43d5`, backup recuperável dos arquivos 0.26.1 `191c122676068eba2c3bf32e`. Resultado `applied:true`, ativo antes/depois, `/` e `/wp-json/` HTTP 200 antes/depois com bypass assinado. `system/health` confirmou **0.27.0**, `healthy:true` e descritor LinkedIn admitido. A concessão OAuth já utilizada permaneceu com o mesmo identificador, perfil maintenance e revisão 1. Retenção SQL, limite de arquivo, habilitação e canais de atualização ficaram iguais.

| Prova | Resultado | Evidência |
|---|---|---|
| Sintaxe do instalador | 449 PHP, zero erros; 458 arquivos no ZIP | `lint-installer.json` |
| Rótulos, metadados e integração | 8 + 42 + 48 + 29 + 32 = **159 verificações funcionais**, zero falhas | `language.json`, `oauth-metadata.json`, `oauth-regression.json`, `oauth-http-cimd.json`, `acceptance.json` |
| Atualização nativa 0.26.1 → 0.27.0 | 19 verificações; tokens/perfis, recibos, confirmação SQL, opções false/vazias, backup e estado incerto preservados; todos os arquivos conferidos | `upgrade.json`, `upgrade-package.json` |
| Workers e reversão | oito respostas antes/depois corretas com OPcache sem validação por timestamp; prévia de rollback validada sem aplicar | `upgrade-package.json` |
| Instalação limpa isolada | ZIP final; WordPress 7.1.3 e 7.1.2; PHP 8.3.6; cron confirmado, leitor/guia disponíveis, acompanhantes ausentes | `clean.json`, `clean-minimum.json` |
| Documentação local | 22 documentos completos e leitor público, 23 verificações | `documents.json`, `documents-checks.json` |
| Documentação pelo MCP Site-Teste | 22 documentos, 24 páginas, bytes/hash iguais aos arquivos locais, versão 0.27.0 | `site-documents.json` |
| Site-Teste e navegador | instalação, saúde, catálogo, rótulos das duas abas, diagnóstico correlacionado, consentimento Claude alcançado | `site-tests.json` |

O documento Claude foi baixado realmente: **342 bytes**, SHA-256 `049f8cf53fbaaa902e71402620e96269a8973917b90e69c98b0edccfb9b07f79`. No navegador do Site-Teste, uma requisição sintética usando essa identidade e redirect real chegou a “Claude wants to access your site”. **Não foi pressionado Allow nem criado um conector no aplicativo Claude.** O ensaio HTTP completo de código/PKCE, renovação/replay, revogação e três ferramentas foi executado em laboratório com usuário/token sintéticos; a fixture altera somente a identidade de URL do documento para eliminar dependência de DNS.

O documento sintético hospedado no Site-Teste sem `authorization_code` foi recusado. Identificador `3f8f4ca82c5658ee2c944631`, categoria `metadata_invalid`, 22/10/2026 **18:20:19 −03:00** (a tela apresenta 21:20:19 UTC). O mesmo registro retornou pela rota administrativa. O JSON de teste, o JSON temporário do documento Claude e o ZIP de transferência foram removidos após uso. Permanecem o backup recuperável, a auditoria administrativa e essa falha no anel limitado; o cache público de metadados segue a validade normal. Nenhum grant, perfil ou segredo foi criado/modificado para contornar o consentimento.

Documentação de entrada: `system/guide` com `{}`; leitura por `document`, `byte_limit` até 32768, cursor/hash. `oauth-cimd`: SHA-256 `56b9d68a2af1181422f2cee39fafa0ed5ee1bc2cec10d1521e9d3ff2d12a04e1`; `release-0270`: `52d80df1c7c3f31b155ea191287236d074bc9a16f549e65f1d387604be301a3e`. Catálogo/schema completo gerado em `docs/CONTRATOS-INSTALADOS.json`. Documentos históricos conservam suas versões; o manual de entrada identifica a release corrente.

## 5. Banco e volta de versão

Sem migração ou alteração do schema 2. Configurações, credenciais, prazos, políticas, confirmações e diários não são reiniciados. Falhas de autorização já eram gravadas em arquivo privado com envelope PHP; a novidade é a projeção administrativa limitada. Não há importação retroativa de mutações.

Para reversão, conferir o estado atual e usar o backup de arquivos da 0.26.1 com as guardas de `plugins/rollback`. O laboratório validou somente a prévia, e nenhum rollback foi aplicado no Site-Teste. Voltar arquivos preserva os dados, remove a rota nova e restaura a recusa de capacidades CIMD extras. Não desfaz efeitos externos, operações feitas após a troca ou a auditoria. Não restaurar banco antigo sobre filas vivas.

## 6. O que permanece pendente

1. **MCP 64 — aceite do cliente Claude:** dono/frota deve iniciar nova conexão no próprio Claude, concluir consentimento e comprovar as três ferramentas com a nova concessão CIMD. O servidor já aceita o documento real e mostra a falha inválida; não foi simulada uma conexão do aplicativo como se fosse real. Não é necessário revogar uma conexão válida para isso.
2. **LinkedIn 8(d):** responsável LinkedIn confirma/ajusta a proposta de principal de serviço; MCP e LinkedIn implementam/validam o contrato alinhado. Diário local e `service_principal_unsupported` permanecem o comportamento correto em background. Não há alegação de auditoria central completa CAPI.
3. **Frota/fornecedores:** publicação e distribuição são do dono/frota; nenhum anúncio, publicação LinkedIn, envio CAPI real ou homologação comercial foi realizado. Ausência de prova externa não é convertida em aceite.

**B22/ChatGPT continua encerrado**, conforme relatório 0.25.0 revisão 3 de 21/10/2026. A regressão de metadados ChatGPT passou e a conexão atual continuou operante; não foi exigida reautorização. B22 não substitui o aceite novo específico do Claude.

## 7. Credenciais e configuração do dono

Nenhuma nova credencial ou campo secreto. O conector Claude usa a URL MCP do site, login WordPress e consentimento com perfil adequado; o documento CIMD público é resolvido pelo servidor. Falhas são consultadas em **Ferramentas → Fator3 MCP → Diagnóstico** ou `system/oauth-diagnostics`. Não colar tokens, códigos ou senhas no relatório/chat.

Tokens sociais e concessões CAPI continuam sob responsabilidade dos acompanhantes e não foram alterados. Testes locais usam valores sintéticos; fonte/evidências não contêm banco, cookies, credenciais reais ou capturas de navegador.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-fator3-0.27.0-instalador.zip](wp-mcp-fator3-0.27.0-instalador.zip) | 846316 | `fcf5ad0099b9490abfb8e9ea6ef83c769cad053e2ee75712efce50e219f62bc1` |
| Fonte | [wp-mcp-fator3-0.27.0-fonte.zip](wp-mcp-fator3-0.27.0-fonte.zip) | 3376082 | `c541e4cbe93b9fbef6608cf048fcb6abce69e844c32da0d6adba23af130d743d` |

Relatório canônico: `wp-mcp-fator3-0.27.0-relatorio.md`. Impacto individual LinkedIn revisão 2 relacionado na seção 2. Instalador com raiz `wp-mcp-fator3/`; fonte com raiz `wp-mcp-fator3-0.27.0-fonte/`, código, build, testes e evidências sanitizadas. Nenhum ZIP contém outro ZIP. O instalador reproduzido do fonte deve ser idêntico ao testado, verificado pelo script de fechamento. O hash final do fonte aparece somente neste relatório externo; a cópia interna é anterior ao fechamento.
