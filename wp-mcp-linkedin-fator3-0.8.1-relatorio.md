# Entrega — Fator3 MCP LinkedIn 0.8.1

Revisão: 1 · Data: 2026-10-23 · Rodada: revisão independente da 0.8.0 recebida.
Slug: `wp-mcp-linkedin-fator3` · Versão: `0.8.1`.
Status: apta no escopo testado, com as pendências de homologação externa e de matriz explicitadas na seção 6. A versão corrente desta entrega passa a ser **0.8.1**, pois a revisão encontrou e corrigiu quatro problemas. A 0.8.0 recebida foi preservada como base imutável.

## 1. De onde esta versão entra

Patch expressamente autorizado pelo dono. Consideradas as instruções comuns e o padrão de desenvolvimento Fator3, revisão 4, a documentação instalada, o fonte/instalador 0.8.0 e seu relatório externo revisão 2, a base 0.7.0 e os dois impactos recebidos do Core/MCP. As exceções particulares da entrega anterior (sem Site-Teste e sem impactos avulsos) são histórico daquela rodada; esta revisão atende ao novo pedido de testar e ajustar impactos.

| Base aceita | Bytes | SHA-256 |
|---|---:|---|
| Instalador 0.8.0 recebido | 227651 | `035a84fea5a02480c933c626cda994c49e58649ab4fb192f90b1f526238e8c35` |
| Fonte 0.8.0 recebido | 757543 | `aa3b79a7a7c5e502007c0b49e1b729b6ec76fed3443decb2ee04d14730ec0d52` |
| Instalador 0.7.0, origem do Site-Teste | 207524 | `85b1cc8d16ab972e9acc2ad90bf81f0806b30a66e0833be311e33bf4a6b1d515` |

Instalação limpa e atualizações diretas 0.8.0→0.8.1 e 0.7.0→0.8.1 ensaiadas. O build do fonte recebido reproduziu o ZIP 0.8.0 byte a byte. Ambiente local próprio: WordPress 7.1.3, PHP 8.3.6 e MySQL 8.0.46; mínimo em instalação limpa: WordPress 6.4/PHP 8.1.2. Site-Teste: WordPress 7.1.3/PHP 8.3.36. Pacotes de runtime conferidos pelos hashes fixados nos arquivos de dependências; a assinatura GPG do índice PHP 8.1, registrada na sessão anterior, não foi revalidada nesta rodada.

## 2. Convivência e encaminhamentos

A matriz própria usou os instaladores disponíveis e as mesmas versões efetivas do Site-Teste:

| Acompanhante | Versão | SHA-256 do instalador local |
|---|---|---|
| Fator3 Site Core | 1.48.0 | `91097a3819cce15fcc66adfa5d8503537cacdb51cfd3ad04ba73e5f7c27a18de` |
| Fator3 MCP | 0.28.0 | `d1d297d8aaee0e5188b92fe9eae20a9dcc07e79d639baae25f267bf64f7243b0` |
| Fator3 MCP Google | 0.17.0 | `42bd11080b518c82e0960753fa7b08d7adae28743cfcd3e96f9b83bf3f4709b0` |
| Fator3 MCP Meta | 0.6.0 | `36f5cfe9a20db272fc80d3cdd8fd46da823c4eeac856e31d911e41754fd19f69` |

O relatório recebido da 0.8.0 também apresenta provas do conjunto Core 1.49.0/MCP 0.29.0/Google 0.18.0/Meta 0.7.0. Essas provas foram consideradas e preservadas em `history/received-0.8.0/`, mas os quatro instaladores posteriores não estavam disponíveis para reexecução nesta revisão. Não apresentamos a matriz anterior como prova própria da 0.8.1.

| Destinatário | Consequência e situação | Documento |
|---|---|---|
| Core 1.48.0 | Contratos e separação dos IDs preservados; prontidão agora bloqueia token cuja prova vigente é conhecida como vencida/inativa. Revalidar credencial, sem alterar payload ou regra. Interface resolvida no conjunto testado; aceite comercial pendente. Pedido 289. | `base-site-core-fator3-1.48.0-impacto-wp-mcp-linkedin-fator3.md`, revisão 3 do destinatário |
| MCP 0.28.0 | Auditoria de serviço confirmada; nenhuma adaptação exigida. Corrigida contradição editorial entre previsão e implementação concluída. MCP 65/LinkedIn 8(d) resolvidos tecnicamente; encerramento editorial pelo dono. | `wp-mcp-fator3-0.28.0-impacto-wp-mcp-linkedin-fator3.md`, revisão 3 do destinatário |
| Meta 0.6.0 | Alerta de pontos equivalentes a R1/R2 observados estaticamente; reprodução pelo mantenedor ainda necessária. Não declarar Meta corrigido ou Meta 0.7.0 testado. | `wp-mcp-linkedin-fator3-0.8.1-impacto-wp-mcp-meta-fator3.md`, revisão 1, aberto |

Avaliação prevista antes das correções em `planning/REVISAO-081.md`. Os documentos recebidos conservam as provas e a autoria dos emissores, com retorno identificado do destinatário. Google: nenhuma consequência técnica nova identificada nas fronteiras examinadas. Nenhum SDK, slug, namespace, assinatura pública, identidade de serviço ou contrato de auditoria foi renomeado. Não há dependência de atualização conjunta; somente LinkedIn foi atualizado no Site-Teste. Nenhum encaminhamento foi enviado a terceiros.

## 3. Mudanças e evidência

### Comparação 0.7.0 → 0.8.0 recebida

Inspecionados os diffs do build e do runtime e reexecutadas as regressões. A 0.8.0 acrescentou fila indexada/schema 2, supervisão do worker, recuperação da manutenção, registro dos consumidores em `init`, diagnóstico CAPI local, ordenação/filtro de auditoria, ajustes de retenção/listagens e da suíte (M1–M6). O runtime ganhou quatro arquivos, alterou 30 e manteve 23, sem remoções. A operação `diagnose-conversions` elevou o catálogo para 81; `audit.since` e o limite documental foram as mudanças de schema já declaradas. As melhorias foram preservadas pelo patch.

### Achados corrigidos na 0.8.1

| ID / gravidade | Problema reproduzido | Correção e limite |
|---|---|---|
| R1 / alta | Vinte jobs já indexados queued/retry com cifra ilegível permaneciam no lote inicial em todas as passagens e impediam um job válido de avançar. A cobertura de migração da 0.8.0 só protegia registros ainda sem projeção. | `Jobs::run` isola apenas o job ilegível em execução de background, sob a trava própria; `Queue::isolateUnreadable` muda somente queue_state/queue_next. Payload, revisão, datas e retenção ficam intactos. Falha de resultado filho pausa o pai legível; não o isola. Erros de banco não são tratados como cifra ilegível. |
| R2 / média | `Worker::health` lançava exceção ao ler o last_job ilegível de uma agenda e inviabilizava todo o status. | Captura somente erros de cifra/armazenamento corrompido e acrescenta `schedule_job_unreadable`. Health continua sem HTTP, gravação ou reparo. Erros de infraestrutura continuam explícitos. |
| R3 / média | Prova local vinculada à credencial atual, com expiração conhecida vencida ou active=false, não impedia ready=true. Afetava capabilities preexistente e o diagnóstico novo. | Validade da prova aplicada às duas interfaces; códigos token_expired/token_rejected e requisito token_proof_valid quando existe prova vigente. Sem mudar o fallback anterior de escopos da concessão quando não há prova vinculada; envio ainda exige introspecção remota. |
| R4 / média | A agenda era desativada automaticamente por erro de autorização, mas health descartava agendas desativadas antes de observar o erro, omitindo a falha. | O diagnóstico conserva o aviso de autorização. Contagem de agendas ativas, atraso e necessidade de worker continuam restritos às habilitadas. Não reativa nem renova concessões. |

Os quatro casos falharam no instalador 0.8.0 exato; as 127 verificações originais passaram. Depois da reprodução foram acrescentados mais três casos de proteção (prova inativa, resultado filho corrompido e trava concorrente), totalizando sete testes novos. Todos passaram no patch.

A lógica mudou em `build/common/Queue.php`, `build/common/Query.php`, `build/linkedin/Worker.php` e `build/linkedin/Conversions.php`. O runtime final tem 58 arquivos: 28 PHP e 24 documentos. Em relação à 0.8.0: um documento acrescentado, 26 arquivos alterados (incluindo versão, documentação e manifesto), 31 idênticos, nenhum removido. JavaScript, CSS, input-schemas.json e output-schema.json são byte a byte iguais aos da 0.8.0. Permanecem as 81 operações. `evidence/review081/package-comparison.json` e o diff contêm a lista exata.

## 4. Instalação e prova da troca

Instalar somente o ZIP instalador, com `expected_slug=wp-mcp-linkedin-fator3` e o SHA-256 da seção 8. O pacote não foi publicado em repositório nem distribuído à frota; não há URL raw final criada nesta rodada. No Site-Teste foi usada `plugins/upload-base64`, com conteúdo do ZIP final, overwrite/activate e validação de identidade. Operação de pacote `1b48062d68adc3803ab1d9da5625b1e7`, pré-imagem `94279c6a4d178493fcdb3686`: 0.7.0→0.8.1, ativo antes/depois, aplicado; home e REST com HTTP 200 em processos novos.

| Cenário próprio | Resultado | Evidência no fonte | Limite |
|---|---|---|---|
| Base 0.8.0 exata, isolada | 127 aprovadas; quatro falhas novas esperadas, reproduzindo os achados | `evidence/review081/base080-clean6/` | Fixture de fornecedor |
| 0.8.1 limpa, isolada | 134/134 aprovadas | `cert081-clean/` | Sem acompanhantes |
| 0.8.1 limpa, integrada | 166/166 aprovadas; 24 documentos/31 páginas pelo executor MCP real | `cert081-integrated/` | MCP executado localmente no WordPress real |
| 0.8.0→0.8.1 integrada | 173/173 aprovadas; preservação exata de registros cifrados, opções e projeção de schema 2; docs completas | `cert081-upgrade080b/` | Dados sintéticos persistidos na base real |
| 0.7.0→0.8.1 integrada | 173/173 aprovadas; preservação de dados e schema 1→2; docs completas | `cert081-upgrade070/` | Aviso f3base preexistente no arranque da 0.7.0; processo novo da 0.8.1 comprova ausência desse aviso |
| WP 6.4/PHP 8.1.2, limpa isolada | 132 aprovadas; duas não aplicáveis; zero falhas | `cert081-minimum/` | Abilities API ausente nessa versão; não é prova de MCP no mínimo |
| Auxiliar de Site-Teste, ensaio local | 25 verificações aprovadas | `cert081-siteqa-local2/` | Perfil de laboratório configurado explicitamente |
| Site-Teste, WP 7.1.3/PHP 8.3.36 | 25/25 aprovadas, três POST sintéticos, nenhuma chamada real ao LinkedIn | `site-teste.json` | HTTP interceptado; não comprova conversão comercial |
| Documentação remota, pacote instalado | 24 documentos completos/31 páginas; bytes e SHA-256 iguais ao instalador | `site-mcp-docs.json` | Leitura pelo conector autenticado do Site-Teste |
| Sintaxe/ZIP | 28 PHP válidos; 58 arquivos íntegros; nenhum teste/auxiliar/ZIP aninhado no instalador | `package-validation.json` | Verificação estática de pacote |

Os diretórios abreviados estão sob `evidence/review081/`. Os cinco cenários locais certificados verificaram correspondência exata entre árvore instalada e ZIP. Nenhum warning/notice/fatal do pacote foi detectado nesses cenários. A ocorrência f3base no ensaio de salto da 0.7.0 é anterior à troca, coerente com M2 e sua sonda de processo novo; não é defeito novo do patch.

Durante o preparo, um ensaio de atualização falhou porque a fixture criava uma agenda por Store::put sem armar o worker na base 0.8.0. A fixture foi corrigida para reproduzir o estado que a API pública cria; a suíte final passou. Um primeiro ensaio do auxiliar remoto, em laboratório, foi recusado pelo perfil MCP ainda não configurado; o perfil de laboratório foi estabelecido e o teste repetido. Não houve alteração de runtime para contornar autorização. As provas finais não misturam esses erros de preparação com defeitos de produção.

Documentação descoberta por `linkedin/documentation`, leitura com `document`, `offset`, `limit_bytes=16384` e `expected_revision`, concatenação até next_offset=null. Catálogo remoto retornou versão 0.8.1 e leitor público. As suítes também verificam confinamento de caminhos, revisão divergente, negação administrativa e ausência de chamadas ao fornecedor/efeitos de configuração durante a leitura.

**Estado final do Site-Teste:** LinkedIn 0.8.1 ativo, status.state=ok, issues=[], storage_ready/crypto_ready=true, audit_health=ok, central_registered=true. Selftest: oito verificações locais ok; system/health.healthy=true. Nenhuma conexão, concessão, agenda ou job sintético restante. Auxiliar removido com hash guardado e catálogo `linkedin-qa/` vazio. Permanecem somente registros administrativos/referências de auditoria e backups normais. Outros plugins mantidos: Core 1.48.0, MCP 0.28.0, Google 0.17.0, Meta 0.6.0, WP Super Cache 3.1.4, Yoast 28.7 e DreamHost Panel Login 1.0.0.

## 5. Banco e volta de versão

O patch mantém schema 2: nenhuma coluna, tabela ou opção nova obrigatória. Atualização da 0.8.0 preservou inclusive a projeção da fila; da 0.7.0 aplicou a migração já existente, sem reescrever os payloads. Em execução, o novo isolamento muda unicamente queue_state para unreadable e queue_next para zero após falha de leitura sob trava; não repara nem apaga ciphertext. Um registro isolado exige investigação das chaves/dados e recuperação deliberada, sem reenvio automático.

A pré-imagem remota cobre arquivos do pacote; não é backup integral de banco ou de efeitos de fornecedor. Para voltar à 0.8.0, restaurar arquivos compatíveis com schema 2; os quatro problemas retornam. Voltar à 0.7.0 também remove a supervisão e exige o procedimento de migração documentado ao avançar novamente. Downgrade não ensaiado nesta rodada. Preservar banco e salts; não desinstalar para simular reversão. Restaurar arquivos não desfaz um evento externo nem autoriza repetir resultado incerto.

## 6. O que permanece pendente

- Dono da integração/conta: homologar conversão comercial real, produto `rw_conversions`, ativo/regra CONVERSIONS_API autorizados, vínculo com Core e contagem única. Nenhum desses resultados é inferido dos POST sintéticos. A ação em CTO Office permanece no impacto recebido do Core.
- Responsáveis pela rodada conjunta: disponibilizar os bytes Core 1.49.0/MCP 0.29.0/Google 0.18.0/Meta 0.7.0 caso seja necessário certificar novamente esse conjunto com o patch. Há evidência recebida da 0.8.0, não execução própria da 0.8.1 com ele.
- Mantenedor Meta: confirmar ou descartar R1/R2 na versão corrente, conforme alerta. Não houve modificação desse plugin.
- Dono/revisor: encerramento editorial MCP 65/LinkedIn 8(d), decisão de distribuição e eventual publicação raw. Nenhuma distribuição à frota realizada.
- Não ensaiados: downgrade, atualização no mínimo WP 6.4/PHP 8.1.2 e navegador visual. JS/CSS não mudaram e as rotas administrativas afetadas foram exercitadas; isso não é teste visual.

Não foram identificadas regressões adicionais nos cenários executados. Isso não equivale a garantia de ausência de impacto em ambientes, ativos ou versões não ensaiados.

## 7. Credenciais e configuração do dono

Ferramentas → Fator3 MCP LinkedIn. Token manual continua suportado; Client ID/Primary Client Secret e autorização externa aplicam-se à inspeção/renovação conforme documentação. Para CAPI, `rw_conversions` e `r_ads`, conta selecionada, regra API ativa e concessão explícita ao consumidor `site-core-conversions`. Core usa regra de servidor própria, distinta da regra de navegador. Nenhum segredo, credencial real ou autorização nova foi incluído na entrega. Gates `manage_options`, dono/revisão da concessão e perfil MCP foram preservados.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `wp-mcp-linkedin-fator3-0.8.1-instalador.zip` | 232544 | `172081883af66b8c4b61676396d85066d4be0778b7ca06fb22262b30a4d2374a` |
| Fonte | `wp-mcp-linkedin-fator3-0.8.1-fonte.zip` | 882430 | `bd43abba9412e7292d9810ab38ecb763d2a2efd30d1e3485652a598aeb16c024` |

A cópia deste relatório no fonte é explicitamente anterior ao fechamento. O relatório externo canônico recebe tamanho e hash do fonte após fechar o arquivo, evitando circularidade. Fonte no singular, com runtime idêntico ao instalador, código canônico, testes, evidências sanitizadas e impactos. Nenhum ZIP contém outro ZIP.

Complementos entregues: os três documentos de impacto da seção 2. Os impactos recebidos foram atualizados preservando identidade/histórico; os artefatos 0.8.0 não foram sobrescritos. Esta entrega estabelece a 0.8.1 como versão corrente no escopo revisado.
