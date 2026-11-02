# Entrega — Fator3 MCP LinkedIn 0.15.0

Rodada de implementação de 02/11/2026. Revisão 1 do relatório. **Versão corrente entregue: 0.15.0**, instalada e ativa no Site-Teste. Pedidos LinkedIn 18–20 implementados; pedido 21 implementado no produtor, com adoção e aceite conjunto do Core ainda pendentes. Nenhum código ou documento do Core, MCP ou outros responsáveis foi alterado.

Este é o relatório externo canônico, concluído após o fechamento do ZIP fonte. A cópia interna preserva a identificação anterior ao fechamento, sem referência circular.

## 1. Bases aceitas e entradas

Base direta aceita: `wp-mcp-linkedin-fator3` 0.14.0. Instalador de 325350 bytes, SHA-256 `91b49ab4aaac5487657496d22d2d1e3a31334a4afa2547dd7946ebdf1d9868ef`. Fonte recebido: SHA-256 `91b485c5a64ce4dc2fb8e5fba030f9abba76221d8cd9c2c66d55e7c46c0246fe`; relatório recebido `5b462756dacbf7754f93602f5ac66030b7b7951ae062fd42c04f96f4af65ad3a`.

Foram considerados os pedidos 18–21 de `Fator3 MCP LinkedIn(20261102-013138).md`, os pacotes/relatórios novos de Core 1.67.0, Google 0.26.0 e Meta 0.19.0, MCP 0.38.0 e Pipedrive 0.5.0 de referência, normas do projeto e histórico de impactos preservado na base. A cópia de trabalho dos pedidos remove o telefone do lead; os originais e pacotes estão identificados em `inputs/0.15.0/packages.json`. Os documentos recebidos dos acompanhantes foram usados como entrada, não reescritos como resposta da rodada.

O incremento minor segue a regra comum para implementação. Slug, basename `wp-mcp-linkedin-fator3/wp-mcp-linkedin-fator3.php`, namespaces, chaves, Update URI e interfaces anteriores foram preservados. Contrato Lead Reader 1.2 é aditivo; 1.0/1.1 continuam disponíveis.

## 2. Convivência e encaminhamentos

| Pacote examinado | Versão | SHA-256 do instalador | Prova/limite |
|---|---|---|---|
| Fator3 Site Core | 1.67.0 | d781cdbccfb00fc3224385e4e12e8e67bf4a06b58e2c1f1d6a686bca3df94c6b | Ativo na bancada integrada e Site-Teste; conversões comerciais exercitadas |
| Fator3 MCP | 0.38.0 | bc550c6573527a0d71bfa560036f83e7c8aec546f49d70b8e0095da5d303c1a5 | Executor original, perfis/revogação, Registro e leitura documental |
| Fator3 MCP Google | 0.26.0 | f75031f2a430e099b7d3603d321993a049b4fb49606b9267144a59971eeebfe4 | Ativo na convivência; não houve homologação de fornecedor Google |
| Fator3 MCP Meta | 0.19.0 | f7629f48fffb774542a480fb55f29a151762b06a27b34c9a0c3188da3599451b | Ativo na convivência; não houve homologação de fornecedor Meta |
| Fator3 MCP Pipedrive | 0.5.0 | 59e8c99d5bb8a54fcfeaba06c56d816b940a1fe97a7d6b473d13a252c6e5042a | Extraído/inativo no PHP 8.3.6 por exigir 8.3.36; ativo no Site-Teste |

Um impacto técnico pertinente: **`wp-mcp-linkedin-fator3-0.15.0-impacto-base-site-core-fator3.md`**, revisão 3, aberto. Abrange efeito pré-envio e normalização (Core 368), contrato 1.2, seleção automática, consumo de eventos e assinatura compartilhada (Core 369). Foi iniciado no planejamento e atualizado na implementação/entrega. O Core 1.67.0 registra 1.1 e conserva seleção explícita; sua integração comercial automática não está concluída por esta entrega.

As correções 19/20 recebidas da frota foram incorporadas. Os impactos históricos respondidos pela base continuam históricos; não se reabre nem se encerra item central sem prova e atribuição. Não foi encontrada alteração técnica que exigisse novo impacto individual para MCP, Google, Meta ou Pipedrive. O MCP aceita os estados e metadados publicados sem alterar seu código. Não foram criados avisos de versão sem ação.

## 3. Mudanças por pedido e evidências

**18 — criações recusadas, escape e prévia.** Respostas 400/401/403/404/422 vazias ou com envelope de erro sem objeto/id/recibo terminam `rejected`, `remote_effect:none`, sem exigir reconciliação. HTTP, código e mensagem sanitizada ficam em `last_error`. Respostas com recibo/objeto, formatos ambíguos, 5xx, timeout e resposta perdida conservam incerteza. A regra é de criação, não uma alteração indiscriminada dos fluxos de atualização/exclusão.

A nova `linkedin/close-write-operation` exige proprietário/admin, revisão atual, motivo, nota e reconhecimento explícito do risco. A prévia é padrão e não envia HTTP. A confirmação grava autor/instante/estado anterior no diário, marca `closed` e mantém o efeito remoto anterior, inclusive `unknown`. Nova chave pode prosseguir; repetir a chave antiga preserva o diário. Encerrar não prova inexistência no LinkedIn nem elimina risco de duplicata.

Migração limitada a 50 registros por passagem: não transforma código genérico antigo em prova de rejeição. A 0.14.0 não preservava HTTP/corpo suficientes no diário; os incidentes `ea7838f5…` e `66c4c78e…` usam a evidência recebida, restrita a operação, conexão `linkedin-cto-office`, conta, prefixo e corpo pertinente. A migração conserva código antigo e origem da evidência; não inventa recibo nem apaga registros. Diagnóstico persistido completo também permite classificação. Casos sem prova ficam incertos e têm a saída administrativa documentada.

A prévia de grupo exige `fields.schedule.start`. O 403 de aplicativo sem conta autorizada recebe `app_account_not_listed` e orientação Developers → aplicativo → Products → Advertising API → View Ad Accounts → Add Ad Account. MANAGEMENT/TROUBLESHOOTING explicam que a guarda compara a mesma intenção — operação, conta, Página, publicação, alvo e corpo — inclusive por outra chave/conexão; não bloqueia todo o site.

**19 — finder e efeito antes do envio.** As duas consultas a `leadNotifications` usam `q=criteria` com `owner.value.sponsoredAccount`. `leadFormResponses?q=owner` foi preservado. Falhas de schema/preflight anteriores ao POST retornam `remote_effect:none`, com ownership_key quando calculável. Repetição de operação já enviada mantém efeito confirmado/incerto. Testes conferem o wire format, ausência de POST e semântica de replay. Os quatro webhooks validados pela frota em ctooffice são evidência recebida, não novos webhooks criados nesta sessão.

**20 — resposta textual canônica.** O método compartilhado por getter/finder aplica trim exclusivamente às bordas de strings de `textQuestionAnswer.answer`. Espaços internos, opções múltiplas, tipos não textuais, identidade e timestamps permanecem. Teste compara os dois caminhos byte a byte no formato sintético correspondente ao relato. Não foram reescritos leads/contatos do Core.

**21 — todos os formulários.** Opção explícita `all_forms_accounts` na conexão e concessão, com simulação/confirmação e revisões. Novos cadastros e atualizações antigas ficam desabilitados por padrão. Concessão automática exige contrato `linkedin-lead-reader/1.2.0`, as quatro permissões e callback do próprio site. O catálogo amplia apenas a autorização concedida.

Worker periódico percorre formulários com paginação/checkpoint, verifica proprietário, ID, versão e data de criação, cria a assinatura no mesmo processamento e persiste evento/checkpoint atomicamente. Hook `f3_linkedin_lead_form_discovered` e método `list_form_events` permitem notificação e recuperação durável; Registro local inclui `form_discovery`. Chave estável/diário evita POST duplicado após interrupção. Falha de assinatura fica explícita; não é declarada sucesso. Novas operações: `lead-discovery-status`, `lead-run-discovery`, `lead-list-form-events`, além da rota de encerramento; **97 operações no total**.

Limites publicados em LEAD-DISCOVERY: uma linha por tarefa/passagem, até 20 tarefas, orçamento global verificado entre tarefas de 20 segundos e orçamentos HTTP por operação; intervalo 5–1440 minutos, padrão 60 após ciclo completo; teto de 10000 formulários por catálogo. Depende de WP-Cron/cron real. Catálogo e eventos não expiram automaticamente. Hook é notificação; consumidor precisa persistir checkpoint e deduplicar. Assinatura já existente de outra intenção não é adotada implicitamente.

### Validação executada

Todos os ensaios finais abaixo usam o instalador SHA-256 `e12b2b46…` completo da seção 8; fornecedor, e-mail e dados comerciais de bancada são sintéticos. MySQL 8.0.46 e WordPress reais; não se trata apenas de mocks de classes WordPress.

| Ensaio | Resultado |
|---|---|
| Contraste na base 0.14.0 | 10 verificações reproduzem a prévia permissiva, 4xx incerto, finder incorreto e diferença textual |
| Upgrade integrado 0.14.0 → 0.15.0, WP 7.1.4/PHP 8.3.6 | 431 verificações funcionais registradas, zero falhas, 1 não aplicável; inclui 27 de preservação/migração e 28 dos pedidos novos |
| Documentação pelo executor MCP 0.38.0 local | 36 verificações, zero falhas; 35 documentos lidos integralmente em 43 páginas |
| Instalação limpa integrada | 28 verificações dirigidas, zero falhas |
| Mínimo WP 6.4/PHP 8.1.2, LinkedIn isolado | 135 verificações nativas (2 não aplicáveis) e 27 dirigidas, zero falhas nos resultados finais |
| Interface autenticada, laboratório limpo | 44 verificações DOM aprovadas, HTML/JS reais + REST; jsdom 27.4.0/Node 24.22.1, não inspeção visual em navegador |
| Build e integridade | Lint dos 34 PHP; 76 arquivos instalados idênticos ao ZIP; versão/schemas/manifesto coerentes |
| Site-Teste | 9 autotestes locais; 35 documentos/37 páginas com bytes e hashes iguais ao instalador; sondas 200 |

A matriz integrada exercita OAuth/avisos da 0.14, gestão, CAPI/aquisição, conversões comerciais por ação, revogação/perfis MCP, históricos/retomadas, retenção, isolamento e novos fluxos. As provas novas incluem crash entre evento/checkpoint com rollback e retomada sem outro POST, paginação de eventos e formulários, versão nova, proprietário estrangeiro e revogação antes de envio.

Correções da bancada: contagens antigas atualizadas para 97, asserções do Registro passaram a paginar e DOM passou a aguardar a renderização assíncrona. A matriz completa de upgrade foi repetida depois dessas correções e ficou sem falhas. No mínimo, a regressão nativa e o teste dirigido final estão em processos separados; o resultado anterior do teste dirigido falhou por consultar só a primeira página do Registro, sem alteração de runtime posterior.

Nenhum erro de log atribuído ao arquivo do pacote nas execuções. Na preparação/atualização houve um tipo de notice do WordPress por inicialização precoce de Abilities API; está preservado em environment.json e não apareceu nas matrizes limpas. Não se declara ausência universal de impacto: os resultados cobrem a matriz e as fronteiras exercitadas, sem homologação do fornecedor real.

## 4. Instalação e prontidão

Site-Teste autorizado: `https://fator3-teste-mcp-1.dreamhosters.com/`, canal WP MCP fator3-teste. Inventário anterior: LinkedIn 0.14.0 e os cinco acompanhantes da seção 2 ativos. Foi substituído exclusivamente o LinkedIn, via `plugins/upload-base64`, com `expected_slug`, `expected_sha256`, idempotência, pré-imagem e sondas. O transporte Base64 do pacote validado foi usado nesta bancada; publicação raw pela frota não foi executada.

Operação `56985276877a20a582826b627b3cc1c0`; backup `365299839b7eb1f16619f7af`; request_id da troca `23bfed260869a226f2c25954`. Resultado `applied:true`, `recovery_status:applied`, versão 0.15.0 ativa. `/` e `/wp-json/` retornaram 200 antes/depois, com bypass de cache verificado pelo canal. São sondas internas da mesma origem; não comprovam acesso público externo.

Nova requisição confirmou storage/crypto prontos, zero conexões LinkedIn, sem problemas, fila sem migração pendente e serviço de auditoria registrado. Autoteste com nove checks aprovado; `remote_homologated:false`. Acompanhantes mantiveram versões/estado. Ativação do canal foi `silent_reactivation`, com novo processo PHP, sem ciclo de activation hook; bootstrap/status e documentação confirmaram funcionamento. Não foi configurada credencial real, criada campanha, enviado lead/conversão ou instalado fixture nesse site.

**Pronto para atualização do plugin**, preservando fluxos explícitos. Habilitar a seleção automática para o Core depende de sua adoção do contrato e da configuração autorizada. A troca não valida por si só acesso a contas/produtos LinkedIn, entrega de webhook ou ingestão comercial.

## 5. Banco, preservação e reversão

Schema físico e tabela existentes preservados. Novos buckets cifrados `lead_scan`, `lead_catalog`, `lead_form_event`; opções próprias de checkpoint/cron. Dados anteriores fora das mutações migradas foram conferidos por hash de linhas; nenhuma configuração antiga foi automaticamente ampliada. O marcador final da migração evita consulta nova no bootstrap após conclusão. A manutenção retoma passagem incompleta.

Backup operacional deve conter arquivos, banco e salts. A pré-imagem da troca recupera arquivos, não efeitos de banco/fornecedor (`database_effects_reversible:false` no recibo). Voltar arquivos à 0.14.0 não apaga eventos, catálogo, encerramentos ou webhooks. A base ignora seleção automática; não repetir intenção por ter retornado arquivos. Desative a seleção/cron com decisão explícita e preserve recibos. Restauração antiga do banco pode perder evidência e provocar duplicatas; exige coordenação. Atualização não deve usar desinstalação.

## 6. Pendências e responsáveis

- **Core:** adotar contrato 1.2, seleção automática, evento/checkpoint e recibo do produtor, conforme impacto; conferir recuperação do conteúdo conflituoso do pedido 368 sem duplicar contato.
- **Frota/dono, ctooffice:** após instalar, conferir no diário real a liberação dos dois incidentes do pedido 18, testar criação inválida/repetição corrigida e remover o grupo de teste; validar próximo lead e formulário novo com webhook/ingestão. Esses aceites reais não foram executados aqui.
- **Frota:** publicar instalador/relatório na raiz raw autorizada, conferir hash e slug antes da troca e seguir a regra de histórico. Nenhum push, publicação ou envio a terceiros foi realizado nesta rodada. Fonte entregue ao dono.
- **Limite de convivência:** Pipedrive não foi ativado na bancada PHP 8.3.6; apenas presença ativa e estabilidade de instalação foram observadas no Site-Teste. Não há alegação de teste funcional das APIs Google/Meta/Pipedrive.

## 7. Credenciais e autorização

Não há valores de token/segredo neste relatório ou instalador. A bancada usa dados sintéticos e não envia e-mails reais. Nenhuma nova credencial é exigida para aplicar as correções; autorização efetiva continua dependente de produtos, escopos, conta, papel e revisão. Descoberta automática exige opt-in e callback autorizada, com revalidação antes do envio; revogação e perfil MCP continuam bloqueando execução. Não foi ampliada concessão real nem alterado documento central de pedidos.

## 8. Artefatos e identidades finais

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-linkedin-fator3-0.15.0-instalador.zip | 345084 | e12b2b468b71c53d7ecc67c55f758ee1af5ba2b24082f9b12046c66944169e85 |
| wp-mcp-linkedin-fator3-0.15.0-fonte.zip | 2345227 | 0e2ca16e82629d4c5f9324514415a5877f946d27455b906b9fc15ede09f21c96 |

Complementos: `wp-mcp-linkedin-fator3-0.15.0-relatorio.md` e `wp-mcp-linkedin-fator3-0.15.0-impacto-base-site-core-fator3.md`. Instalador tem somente a raiz `wp-mcp-linkedin-fator3/`. Fonte tem raiz `wp-mcp-linkedin-fator3-0.15.0-fonte/`, runtime idêntico, build, testes, evidências sanitizadas, plano, entradas e cópia interna do relatório. Nenhum ZIP aninhado, runtime de laboratório, banco, node_modules ou fixture ativa integra a entrega.

Evidências principais: `evidence/release0150/summary.json`, `integrated-upgrade/`, `clean-directed/`, `minimum-regression/`, `minimum-directed/`, `ui/`, `baseline/`, `site-test.json`, `site-documentation.json` e `source-changes.json`. Plano e impacto acompanham a fonte. O instalador identificado foi conferido no laboratório e instalado no Site-Teste; os arquivos finais são imutáveis após esta entrega.
