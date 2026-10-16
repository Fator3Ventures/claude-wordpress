# Entrega — Fator3 MCP 0.23.0

Revisão 1 · 16/10/2026 · Slug: wp-mcp-fator3 · Basename: wp-mcp-fator3/wp-mcp-fator3.php
Status: **implementado e validado-wordpress/MCP, com-pendencias**. As três correções prioritárias estão entregues e o pacote final está ativo no Site-Teste. A matriz ampliada contém limites e aceites externos explicitados abaixo; não se declara homologação de fornecedor ou novo consentimento ChatGPT.

## 1. De onde esta versão entra

Base direta: 0.22.0, além de instalação limpa, sem versão intermediária. Instalador base: 762280 bytes, SHA-256 `622b75d20c3dc115bb8391d08f59c484ebbc6ac78547b8dac08b0f6b10e1fa7d`. Fonte base: 2565319 bytes, SHA-256 `50ff0c8734a7c133561dc44d45256fa0923bc7735655a25b6792d469e69bfda8`.

As duas diretrizes Fator3 foram lidas integralmente na revisão 3, de 16/10/2026. O plano MCP revisão 2 e os novos relatórios/impactos foram incorporados; originais preservados em docs/entradas e docs/PLANO-0230.md. Pedidos MCP 60, M91-01/N24, M91-02/N25 e MCP-221-08 são os eixos implementados. IDs históricos MCP-221 não designam a versão-alvo.

| Acompanhante recebido | SHA-256 do instalador |
|---|---|
| Core 1.33.0 | de427cb219be769d9e44ae9aaf5e6f31055990b3d8f9b8664ac0faa596f61364 |
| Google 0.10.0 | 3e30634b1d1f87b9b4fdeba2a37ac382b1394a1ec7f7235166aa15d107ef8b52 |
| Meta 0.2.0 | f5cb81781038e487741adc3a1d82791f149d37a5219f7d4747b0acf9ae27d57f |
| LinkedIn 0.2.0 | 64da9956452d3943546758690cf5cb5ff6508cbf502780bbcc1ca1492e6e8324 |

Todos os nomes, bytes e hashes dos insumos estão em evidencias/0230/inputs.json. Core 1.34.0 é plano sem binário. Implantador atual não foi fornecido. A linha mínima declarada permanece WordPress 7.1.2/PHP 8.3; a execução local foi WordPress 7.1.2/PHP 8.3.6/MySQL 8.0.46. Não se afirma teste do patch PHP 8.3.0. A documentação também passou com PHP -n, sem mbstring.

## 2. Convivência e encaminhamentos

Nenhum acompanhante foi alterado. Bootstrap em PHP novo passou com MCP primeiro, acompanhantes primeiro, MCP sozinho e cada um dos quatro pares. A presença/versão de outro plugin não é uma trava global. Gates de domínio e do canal são cumulativos; registro de provider/executor não concede acesso. Contratos server-integration/1.0.0, executor-registration/1.0.0, package-distribution/1.0.0, policy_contract 1 e execução 2.0.0 foram mantidos.

| Destinatário | Versão examinada | Classificação | Arquivo próprio |
|---|---|---|---|
| base-site-core-fator3 | 1.33.0; 1.34.0 apenas plano | informativo | [wp-mcp-fator3-0.23.0-impacto-base-site-core-fator3.md](wp-mcp-fator3-0.23.0-impacto-base-site-core-fator3.md) |
| wp-mcp-google-fator3 | 0.10.0 local; 0.9.0 no Site-Teste | informativo | [wp-mcp-fator3-0.23.0-impacto-wp-mcp-google-fator3.md](wp-mcp-fator3-0.23.0-impacto-wp-mcp-google-fator3.md) |
| wp-mcp-meta-fator3 | 0.2.0 | informativo | [wp-mcp-fator3-0.23.0-impacto-wp-mcp-meta-fator3.md](wp-mcp-fator3-0.23.0-impacto-wp-mcp-meta-fator3.md) |
| wp-mcp-linkedin-fator3 | 0.2.0 | informativo | [wp-mcp-fator3-0.23.0-impacto-wp-mcp-linkedin-fator3.md](wp-mcp-fator3-0.23.0-impacto-wp-mcp-linkedin-fator3.md) |
| implantador-base | binário e versão atual não fornecidos | nao-avaliado | [wp-mcp-fator3-0.23.0-impacto-implantador-base.md](wp-mcp-fator3-0.23.0-impacto-implantador-base.md) |

Os cinco encaminhamentos estão preparados, não enviados. Números de testes informados pelos mantenedores não foram somados aos ensaios próprios.

## 3. Mudanças e evidência

| Pedido | Mudança e resultado |
|---|---|
| MCP 60 / MCP-221-09 | Captura a origem da chave antes da decoração; conserva schema/required/valor nativos, inclusive optional/read e decoração repetida. Apenas a chave acrescentada pelo MCP é retirada do callback. Fingerprint e isolamento persistidos conservados. |
| Autorização e replay | Revalida a permissão sob lock. Sucesso com chave nativa volta ao callback com a mesma chave para obter recibo e revalidar domínio; o payload guardado não substitui grant/seleção atual. Registros antigos não são expurgados. |
| M91-01 / Core N24 | Projeção pública tipada em sucesso/erro, texto e structuredContent, com redação de folhas secretas aninhadas. DataSafety.php permanece byte a byte igual à base para SQL/options. |
| M91-02 / Core N25 | ok:false/code:revision_conflict/data:null recebe success:false/error_code:revision_conflict/conflict:true/retryable:false. Código nativo e null são conservados; não há inferência por mensagem. |
| MCP-221-08 | 16 documentos allowlisted no instalador, páginas UTF-8 por bytes sem mbstring, cursor assinado, SHA-256/revisão, bloqueio de caminhos/URLs e cursor obsoleto. Modo topic legado mantido. Leitor não faz HTTP nem grava auditoria. |

A allowlist pública aceita checks_passed/all_checks_passed booleanos; passed booleano de sonda ou inteiro não negativo; credential.configured booleano; token_configured/secret_configured booleanos; credential_generation/credential_revision/authorization_revision inteiros não negativos. Filhos desconhecidos de credential e tipos inesperados permanecem redigidos. Schemas JSON são tratados como descritores, sem confundir nomes de propriedades com valores secretos. confirm_token/confirmation_token válidos de 64 hexadecimais continuam disponíveis ao cliente autorizado; logs não recebem esses valores nem payloads de erros de domínio.

Precedência: success explícito prevalece sobre ok; error_code explícito prevalece sobre code. revision_conflict comum força conflict:true/retryable:false. Código nativo desconhecido é conservado em code, com fallback operation_failed quando falta error_code; não vira conflito por conter essa palavra. A normalização é idempotente.

| Evidência própria | Resultado | Limite |
|---|---|---|
| contracts.json | 90 verificações sem falha: schemas, replay, revogação, tipos, segredos, Core/Google reais, bridges, sociais, documentação e gates | Fornecedores simulados/sem credenciais |
| google-paging.json | 31 verificações; cinco seções completas, próxima página sem perda; maior JSON decorado observado 1006344 bytes | Registros Google sintéticos, sem coleta real |
| linkedin-lead-http.json | 5 verificações; um POST simulado, replay do recibo, revisão inteira e negativas | Nenhuma assinatura ou entrega de lead real |
| concurrency.json | 5 verificações: chamadas HTTP concorrentes, conexão/usuário distintos e revogação | Não certifica todas as janelas de revogação em voo |
| bootstrap-matrix.json | 7 combinações em processos PHP novos | Mesmo laboratório descartável, dados próprios |
| activation / worker-guards / distribution | 12 + 11 + 16 verificações sem falha, executadas nesta rodada | Fixtures; não prova distribuição raw da frota |
| oauth-metadata / oauth-http-cimd / oauth-http-dcr | 48 + 24 + 25 verificações sem falha | OAuth HTTP real local com cliente sintético; B22 não realizado |
| clean.json / upgrade.json | ZIP final em banco novo; 18 verificações de upgrade direto, OPcache sem checagem de timestamps | Site local, nenhum segredo real |
| guide-no-mbstring.json | 16 documentos reconstruídos sem extensão mbstring | Classes reais com três shims WP explícitos; não é prova HTTP |
| documentation / package-audit | 80 invariantes documentais, 14 de pacote e lint dos 448 PHP | Lint é separado de teste funcional |
| site-runtime / site-documentation | 456/456 arquivos exatos, sem extras/symlinks; 16 documentos completos em 18 páginas | Leitura autenticada no Site-Teste |

As regressões herdadas foram executadas durante a estabilização da candidata; evidências atuais estão em 0230, e as históricas da base foram restauradas em 0220. Os bytes finais foram novamente instalados/checados em instalação limpa, upgrade direto, contratos principais, documentação e Site-Teste. O relatório não transforma evidência antiga em teste novo.

Rastreabilidade dos aceites: V01–V03, V05–V06, V08, V10, V13–V15, V17, V19, V21–V22, V26–V27, V29 e V31 têm as provas descritas acima. V04 cobre normalização/erros controlados, sem injeção nova de falha SQL real; V07 cobre perfil/alvo/bridge aninhada, sem repetir toda a matriz de servidores alternativos; V09 cobre origem/revisão genéricas, sem feed Google remoto; V11–V12 cobrem jobs/exportação/revogação e assinatura simulada, sem homologação completa de leads pessoais/consumidor; V16 cobre hashes/worker/pré-imagem de rollback, sem repetir todas as divergências históricas de pós-imagem; V25 cobre concorrência/revogação antes de replay/estados antigos, sem todas as janelas de mudança durante espera; V28 cobre gates administrativos de abilities, sem nova revisão visual completa do painel/REST. V23–V24 têm prova local com binários reais e API simulada; a parte de conta real segue pendente. V18, V20 e V30 são pendências externas. V32 comprova a linha mínima nos patches informados, não todos os patches inferiores. Não se marca V01–V32 integralmente aprovado.

## 4. Instalação e prova da troca

O instalador final desta seção é o ativo no Site-Teste fator3-teste-mcp-1.dreamhosters.com. Foi usado plugins/upload-base64 com activate:true, overwrite:true, expected_slug:wp-mcp-fator3, expected_sha256 e probe_timeout_seconds:30. Operação final: `05de472c08405a5a6ba0ad1280731026`; pré-imagem final: `dc1bd7a58ff8751ff7725234`. Reativação silenciosa em PHP novo, sem repetir o hook inicial; home e /wp-json/ retornaram 200. Ativação não foi tomada como prontidão comercial.

Houve quatro instalações sequenciais de estabilização 0.23.0 no site, com hashes distintos registrados em site-tests.json; somente o último ZIP é entregue. A primeira veio da 0.22.0 (backup `0f9898a378057e8fd7029269`); as seguintes pré-imagens são candidatas intermediárias. Não houve reinstalação de acompanhantes. Estado final: MCP 0.23.0, Core 1.33.0, Google 0.9.0, Meta/LinkedIn 0.2.0. Google 0.10.0 foi testado localmente.

No pacote final, a leitura verificou cada arquivo por SHA-256 através de files/stat, organizada em planos de leitura, e conferiu o inventário sem extras. Esses planos e a auditoria permanecem como histórico de manutenção; nenhum plugin QA, arquivo ZIP temporário público, conexão social ou coleta comercial foi criado. As tentativas de compactar a própria árvore foram recusadas pelas guardas; elas não foram alteradas ou contornadas.

Em requisições novas, o Google preservou os quatro indicadores; o Core preservou revision_conflict/conflict:true/data:null; Meta/LinkedIn passaram da validação da chave até not_configured para conexão inexistente. O envelope externo do conector pode usar INVALID_ARGUMENT; o payload de domínio contém o código corrigido. connection_count=0 nos dois sociais confirma o limite de homologação real.

Destino raw previsto, ainda não publicado/testado: [instalador 0.23.0](https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-fator3-0.23.0-instalador.zip). Publicação e implantação na frota são etapas separadas. Não houve publicação GitHub ou alteração de outros sites.

## 5. Banco e volta de versão

Não há migração nova, expurgo, importação histórica ou troca de schema. Preserva OAuth, perfis, tokens, opções, sessões, backups, jobs e registros existentes. O novo marcador native_key pertence somente aos recibos novos. Chave/intenção divergente continua conflito; running/uncertain/compacted não reexecutam.

Falha antiga completa, inclusive invalid_input da retirada da chave na 0.22.0, continua devolvida. Reconciliar no produtor e usar nova chave somente após provar ausência de efeito. Sucesso antigo nativo sem prova de encaminhamento recebe idempotency_revalidation_required; não expõe recibo nem reabre execução. Sucessos com chave exclusivamente MCP mantêm replay.

Rollback exige conferir a pré-imagem e o estado atual. A pré-imagem da última troca é uma candidata intermediária, não diretamente a 0.22.0. Para retornar à base, usar o ZIP base identificado sob procedimento coordenado, preservando banco/salts e verificando conflitos; não forçar pré-imagem antiga sobre árvore divergente. Retornar à 0.22.0 restaura também seus defeitos conhecidos. Restaurar código não desfaz efeitos externos nem alterações de dados de acompanhantes.

## 6. O que permanece pendente

1. Novo consentimento/conexão ChatGPT por CIMD B22; a conexão de manutenção existente e o cliente local sintético não são essa prova.
2. Meta/LinkedIn e Google com recursos e credenciais reais autorizados. Pedido 60 tem prova funcional local, sem conta social real no Site-Teste. Nenhuma assinatura, webhook ou ingestão comercial real foi homologada.
3. Core 1.34.0 e os payloads próprios de 212/217; repetir N24/N25 quando o binário existir. O produtor LinkedIn não prova o consumidor Core.
4. Implantador atual, publicação/download raw e decisão 89 sobre o fonte. Fonte/evidências permanecem privados nesta entrega.
5. Complementar os cenários parciais V04/V07/V09/V11–V12/V16/V25/V28 e, se exigida prova do patch inferior exato, PHP 8.3.0. As limitações não são apresentadas como testes aprovados nem como bloqueio global de instalação.

## 7. Credenciais e configuração do dono

Nenhuma credencial real nova foi necessária ou incluída. Conexões/perfis existentes permanecem. Configuração do MCP em Ferramentas → Fator3 MCP, com capacidade administrativa e perfil explícito; ajuda estática preserva seu gate edit_posts e a política do canal. Para testes reais sociais/Google, o dono deve fornecer conexão autorizada, ativos selecionados e grants pertinentes no plugin produtor. Registro não concede acesso. Nunca inserir tokens, salts ou dumps privados no relatório/fonte/publicação.

## 8. Identidade dos arquivos

| Artefato | Arquivo | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-fator3-0.23.0-instalador.zip](wp-mcp-fator3-0.23.0-instalador.zip) | 818313 | `6a64708f5737eb08c6f726dd5941b28d36a28ecbb45f79f32d2c96d00030a4ab` |
| Fonte | [wp-mcp-fator3-0.23.0-fonte.zip](wp-mcp-fator3-0.23.0-fonte.zip) | 2801809 | `7594fa0dff260a0664281c321521cb6017598cad4fceb7ca3d1ed772ef5ad1ff` |

Instalador: raiz wp-mcp-fator3/, 456 arquivos, 448 PHP, 55 índices silenciosos; sem testes/docs de desenvolvimento nem ZIP aninhado. Documentação operacional compilada é parte do runtime. Fonte: raiz wp-mcp-fator3-0.23.0-fonte/, runtime em fontes/wp-mcp-fator3, build, testes, documentos canônicos, insumos identificados e evidências sanitizadas; sem bancos, dependências binárias, cookies, wp-config ou segredos reais.

O relatório-base dentro do fonte é anterior ao fechamento do próprio ZIP: os campos do fonte ficam pendentes nessa cópia para evitar hash circular. O relatório externo completa os dois valores após empacotamento. Os cinco impactos são os arquivos próprios da seção 2. Nomes históricos em contratos/testes indicam sua introdução; a identidade executável e a revisão/hash da ajuda são as da 0.23.0 entregue.
