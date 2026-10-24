# Entrega — Fator3 Site Core 1.50.0

Revisão: 1 · Data: 2026-10-23 · Rodada: implementação dos pedidos 292 e 293 e revisão de convivência.
Slug: `base-site-core-fator3` · Contrato administrativo: `8.15.0` · 145 abilities.
Status: **com-pendencias** de aceite em produção e de fornecedor; implementação apta no escopo local e WordPress descrito abaixo.

## 1. De onde esta versão entra

Base direta aceita: **1.49.1**, instalador de 2230721 bytes, SHA-256 `4ad3be4159310578a2db47cf179d02fa061fb98021e2f66ca933b59e7db4fb40`. O fonte dessa base foi preservado. A referência funcional é a aba de pedidos recebida em `Fator3 Site Core(20261023-214428).md`, que declara 292 e 293 como pendentes; não se reabrem os pedidos já entregues.

Foram provadas instalação nova e atualização direta de 1.49.1 por `Plugin_Upgrader`, usando o instalador final da seção 8. Não é necessária versão intermediária. Instalação única, PHP de 64 bits; multisite continua fora do suporte.

Ambiente local: WordPress 7.1.3, PHP 8.3.6, MySQL 8.0.46. O mínimo declarado WordPress 7.1.2/PHP 8.3.6 foi ativado e recebeu as quatro suítes dos pedidos novos, com 56 verificações aprovadas. Site-Teste: WordPress 7.1.3/PHP 8.3.36. Não se estende essa prova a toda versão intermediária ou ambiente não exercitado.

## 2. Convivência e encaminhamentos

| Pacote | Versão efetivamente examinada e ativa no Site-Teste | Escopo próprio conferido |
|---|---|---|
| Fator3 MCP | 0.29.1 | Descoberta, transporte administrativo, leitura documental, redator de segredos e registro de abilities |
| Fator3 MCP Google | 0.19.0 | Consumo real do snapshot de medição, releitura após alteração/restauração e disponibilidade dos contratos |
| Fator3 MCP LinkedIn | 0.9.0 | Bootstrap, catálogo, adaptador real de conversões com HTTP sintético e fronteira de cliente Core/plugin |
| Fator3 MCP Meta | 0.8.0 | Ativação conjunta, convivência de registros e separação das credenciais/atribuições do Core |

Os oito ZIPs recebidos tiveram CRC, tamanho e SHA-256 conferidos. O runtime dos fontes corresponde aos instaladores: MCP com 407 arquivos comuns idênticos e 56 proteções `index.php` geradas só no instalador; Google 160, LinkedIn 59 e Meta 42 arquivos idênticos. Evidência: `evidence/1500/inputs.json`. Os acompanhantes não foram modificados por esta entrega.

Impactos recebidos e considerados, com cópias intactas em `inputs/1500/`:

- MCP 0.29.1 → Core, revisão 2: a correção de admin-post/nonce e repetição é declarada resolvida no MCP, sem adaptação obrigatória do Core. Não se amplia a autorização de telas GET nem se presume ausência de efeitos para repetir uma escrita.
- Implantador 2.11.0 → Core, revisão 4: o aviso de schema na mescla já foi corrigido na base 1.49.1. A regressão de schema/perfil foi repetida. O perfil `piso-padrao-3.6`, suas 92 condições e as fronteiras de formulários permanecem. Não se instalou o Implantador em site em operação; o aceite de uma implantação nova segue com a frota.
- LinkedIn 0.7.0 → MCP, revisão 3: o documento antigo ainda descrevia o handshake pendente no MCP 0.27.0. O relatório recebido do MCP 0.29.1 declara implementação desde 0.28.0; a combinação atual foi exercitada com adaptador real. Não se trata o estado antigo como uma nova dependência do Core.
- Meta 0.6.0 → MCP, revisão 3: mantém-se a distinção de `meta/status` como operação com efeito local. Esta versão do Core não muda perfis, concessões ou operações do Meta.

**Não foi identificada adaptação obrigatória em outro pacote nas interfaces examinadas.** Os SDKs e consumidores existentes permanecem; as duas abilities novas são descobertas pelo canal atual. Durante a homologação foi corrigido no próprio Core o formato de `credenciais-ler`, que ocultava metadados sob o redator do MCP. Não se relaxou o filtro de segredos nem se alterou o MCP. Não foram gerados impactos apenas para anunciar versão ou declarar ausência de ação. Nenhuma mensagem, publicação, documento central ou fonte de outro pacote foi alterado.

## 3. Mudanças e evidência

| Pedido | Problema | Mudança | Evidência e estado |
|---|---|---|---|
| 292 — diagnosticar resultado sem confirmação | A revisão global de uma option podia mudar após gravar o resultado de uma tarefa; isso fazia a confirmação geral falhar mesmo com o resultado específico persistido | Releitura confirma tarefa, execução, fim e código. Diagnóstico registra operação SQL, linhas afetadas, revisões esperada/lida, etapa e causa medida. Atualização de zero linhas só é aceita após comprovar bytes e revisão idênticos | `request-292.json` e `request-292-race.json`: 15 verificações; disputa real no MySQL e falha SQL injetada. `implementado`, `validado-localmente` |
| 292 — distinguir conclusão comprovada de perda real | Uma passagem posterior concluída não neutralizava a falha anterior | `checkpoint_confirmado_releitura` e `checkpoint_superado` são neutros; `checkpoint_nao_persistido` permanece falha sem resultado/prova posterior. Diário inclui instante da ocorrência e digest dos argumentos. Reconciliação conserva a evidência original e atualiza agregação da passagem concluída | Execuções e saúde expõem contagem por dia UTC, origem e código. Leitura e cenário sem prova exercitados no Site-Teste. Aceite longitudinal ainda `pendente` |
| 293 — orientação dos 14 segredos | Rótulos genéricos e ajuda insuficiente | Campos usam nome do fornecedor, origem do valor, formato e escopos. SMTP inclui o usuário configurado. Identidade salva e validade legível ficam junto ao campo; leitura não faz HTTP | Testes de renderização, datas, DOM e HTML do Site-Teste aprovados. `implementado`, `validado-wordpress` no escopo descrito |
| 293 — validar antes de persistir | Token errado podia substituir a credencial em uso | Validação local e consulta limitada ao fornecedor antes da escrita; erro em português, sem corpo remoto. Pipedrive `/users/me`; Slack `auth.test` e participação no canal; Meta `debug_token`; LinkedIn `introspectToken` com par de aplicativo. Clarity apenas formato, sem consumir exportação ao salvar | Recusas de formato, HTTP 401, escopo e participação preservam a revisão/valor anterior. HTTP de fornecedor simulado; não é homologação comercial |
| 293 — identidade e rotação | Troca de conta sem confirmação e invalidação desnecessária do estado | Confirmação explícita vinculada à candidata, configuração, usuário, site, revisão anterior e identidade. Prazo de dez minutos. Rotação comprovada conserva catálogo Pipedrive, canal Slack, cursores Meta/LinkedIn e prova Clarity sem prolongar artificialmente sua validade | `request-293.json` e `request-293-extra.json`: 41 verificações, incluindo conflito concorrente e preservação. `dom-1500.json`: 8 verificações |
| 293 — leitura administrativa | Identidade não estava disponível em operação dedicada | `f3base/credenciais-ler` retorna lista de itens com `nome`, metadados e identidade; `f3base/credenciais-verificar` recebe `credential`, revisão e confirmação. `usar_salva=true` identifica a credencial existente sem substituí-la | Permissão administrativa, ausência de segredo, filtro real do MCP e leitura remota comprovados |

A correção de apresentação foi detectada no Site-Teste antes do fechamento: nomes de options usados como chaves faziam o MCP ocultar o item inteiro. Agora são valores do campo `nome`; a entrada `credential` continua redigida. O teste usa o redator original do MCP 0.29.1, sem cópia simulada da política.

Limite explícito do LinkedIn: a introspecção normalmente confirma aplicativo, tipo de autorização, escopos e validade, mas não identifica o membro. Sem prova do membro, a troca exige confirmação e não é anunciada como mesma identidade pessoal; os cursores são conservados. Não se inventou formato fixo ou comprimento de token. O pedido LinkedIn 13 citado pelo Core não constava da documentação recebida do acompanhante; foram usados os requisitos do pedido Core 293 e a documentação oficial de introspecção.

Contrato administrativo 8.14.1 → 8.15.0: duas abilities e confirmação opcional de identidade na escrita de configuração. Sem remoção de operações. Comparação com a base: 5 arquivos adicionados, 33 alterados, 420 iguais e nenhum removido; hashes em `diff-base.json`.

## 4. Instalação e prova da troca

A instalação autorizada foi somente no **Site-Teste**. O ZIP foi transferido e verificado por SHA-256; `plugins/upload` recebeu `activate=true`, `overwrite=true`, `expected_slug=base-site-core-fator3`, `probe_timeout_seconds=30` e o hash final da seção 8.

Operação final: `4c7ea209179572768a1b72dc`; operação de pacote `30690630137415271af43b78b8380f38`; backup `bfd9295c30a6d8bf6fedb85a`. Resultado: `applied=true`, Core ativo, hash `7021163d…`. Página inicial e REST tiveram HTTP 200 antes/depois, em PHP novo e com desvio de cache conferido pelo canal. Isso prova essas sondas internas, não alcance externo independente.

A primeira troca de 1.49.1 usou candidato 1.50.0 `3f8f22…` e gerou o backup da base `e36d6daba36b420b3e3dffd2`. O ciclo de 18 etapas terminou com zero falhas e confirmação pelo executor às 22:14:24 UTC. Após o achado de apresentação, o candidato foi substituído pelo ZIP final `7021163d…`; o ciclo remoto já concluído foi preservado. **Os ciclos locais limpo e atualização foram repetidos com o hash final**, não apenas com o candidato preliminar. Nenhum candidato anterior faz parte da entrega.

| Prova | Ambiente | Resultado | Evidência | Limite |
|---|---|---|---|---|
| Lint | PHP 8.3.6 | 234 arquivos PHP aprovados; 458 arquivos no instalador | `installer.json` | Sintaxe, não comportamento |
| Pedidos 292/293 | WP 7.1.3 e 7.1.2 / PHP 8.3.6 | 56 verificações em cada ambiente | `request-292*.json`, `request-293*.json`, `minimum-final/` | HTTP comercial sintético |
| Regressão 1.49.1 | WP 7.1.3 | 46 + 11 verificações aprovadas | `review-1491*.json` | Casos efetivamente enumerados nas suítes |
| Formulários, Pipedrive, LinkedIn, Slack | WP 7.1.3 | 32, 39, 48 e 20 verificações aprovadas | `forms-1470.json`, `pipedrive-1470.json`, `linkedin-1480.json`, `slack-1480.json` | Persistência real local; fornecedores simulados |
| Contratos e regressão 1.49.0 | WP 7.1.3 | 58 verificações booleanas aprovadas; cinco entradas adicionais são metadados | `release-1490.json` | Não contar metadados como testes |
| Convivência atual e adaptador LinkedIn | WP 7.1.3 | 26 verificações de convivência e 10 de adaptador aprovadas | `coexistence-1500.json`, `provider-linkedin-1480.json` | APIs comerciais não homologadas |
| Concorrência do executor | Processos CLI/HTTP locais e MySQL | Cinco verificações aprovadas, mais duas de preparação | `scheduler-1480.json` | Não é observação de sete dias |
| Instalação nova / atualização direta | WP nativo local | Dois ciclos aprovados, dados preservados e repetição idempotente | `native-cycles-1500.json` | Runtime/DB descartáveis |
| Interface | DOM automatizado | Oito verificações aprovadas | `dom-1500.json` | Sem inspeção visual completa em navegador real |
| QA no Site-Teste | WP 7.1.3 / PHP 8.3.36 | 27 verificações aprovadas; dez chamadas HTTP interceptadas; zero chamadas reais ao fornecedor no auxiliar | `site-teste.json` | QA não grava opções, contatos, filas ou credenciais de negócio |

As contagens têm cenários comuns e não representam casos únicos somáveis. As regressões gerais ocorreram antes do último ajuste restrito à apresentação de credenciais; depois dele foram repetidas as suítes afetadas, mínimos, ciclos com o ZIP final e QA remota. Não se afirma ausência universal de impacto.

**Documentação:** a ability nativa `f3base/documentacao-ler` leu integralmente os 165 documentos em 627 páginas, com 982 verificações booleanas de texto/hash, autorização, aliases e confinamento. Pelo MCP do Site-Teste, após o ZIP final, foram relidos integralmente oito documentos em nove páginas: índice, README, configuração, contratos, release 1.50.0, guia de agentes 1.50.0, credenciais 1.50 e CHANGELOG (duas páginas). Todos correspondem aos bytes locais; tentativa de ler `../../wp-config.php` foi recusada. A comprovação negativa de perfil sem administração foi local; não se alteraram usuários/perfis do site para isso.

**Estado final:** Core 1.50.0 ativo; acompanhantes nas versões da seção 2; DreamHost 1.0.0, WPSC 3.1.4 e Yoast 28.7 preservados. Auxiliar `qa-core-1500.php` e ZIPs temporários removidos; a ability de QA deixou de existir. Backups e registros normais de auditoria foram conservados. Nenhum token real foi trocado e nenhuma mensagem foi enviada pela QA.

Para a frota, após publicação autorizada, usar `https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/base-site-core-fator3-1.50.0-instalador.zip`, conferindo bytes/hash antes de `plugins/upload`. **Esse endereço é o destino previsto, não uma publicação realizada nesta rodada.** Consultar `f3base/saude-ler` com `{}` e exigir versão correta, 18 etapas, zero falhas e `confirmada_no_executor_em` preenchido; abrir índice e release por `f3base/documentacao-ler` para confirmar o conteúdo instalado.

## 5. Banco e volta de versão

Nenhuma tabela ou coluna nova. O inventário continua com 57 tabelas e passa a 139 options; foi acrescentada `f3base_credenciais_estado`, interna, sem autoload, contendo somente identidade, situação e revisão da credencial cifrada. Os valores secretos continuam na cifra existente. A leitura nunca devolve o segredo.

O diário de execuções recebe dados de diagnóstico e correlação. Uma conclusão comprovada pode reconciliar registros anteriores da mesma tarefa/argumentos/ocorrência ou posterior, dentro da janela de 30 dias e lote limitado a 200. O resultado anterior é conservado na evidência de reconciliação. Registros antigos sem correlação suficiente não são declarados resolvidos por aproximação de horário.

A atualização reutiliza o ciclo retomável de 18 etapas; não há migração destrutiva nova. Rotação de credencial é uma ação administrativa explícita, com comparação de revisão. Se o segredo persistir mas o registro de identidade falhar, a resposta informa `credencial_salva_identidade_pendente`; deve-se verificar a credencial salva, sem repetir a troca cegamente.

Backup de arquivos não reverte banco, diário, rotação de segredos ou efeitos de fornecedores. Para voltar à base 1.49.1, usar o instalador original verificado ou a pré-imagem correspondente; conservar e avaliar os estados/dados, sem apagar opções para forçar reinstalação. Não foi realizada volta de versão no Site-Teste. A QA de credenciais não alterou configuração de negócio a restaurar.

## 6. O que permanece pendente

- **Frota/dono — pedido 292:** após implantação autorizada em ctooffice, observar sete dias e conferir que uma tarefa concluída depois não permaneça contada como `checkpoint_nao_persistido`. Toda falha restante deve ter causa medida. A versão não inventa prova para ocorrências históricas sem identidade suficiente.
- **Frota/dono — pedido 293:** homologar consultas com contas reais, seus escopos e permissões. Pipedrive deve ser conferido em ctooffice, sem trocar o token em uso, conforme a ordem recebida. O botão/ability de verificar a credencial salva não a substitui. Não se usou o Site-Teste para envio comercial ao Pipedrive.
- **LinkedIn:** confirmação de aplicativo não equivale a identidade do membro. A limitação fica explícita no resultado e exige confirmação ao trocar sem essa prova.
- **Interface:** HTML e DOM foram testados; não houve inspeção visual completa com sessão administrativa de navegador. Não é alegada homologação visual integral.
- **Implantador/frota:** aceite de site recém-implantado e demais pendências próprias do impacto recebido continuam com seus responsáveis. O aviso de schema do Core não foi reproduzido nas regressões da base corrigida.
- **Distribuição:** publicação no repositório e atualização dos outros sites não foram feitas. O dono decide a implantação; não foi criado agendamento ou monitoramento recorrente nesta rodada.

Não há falha conhecida aberta nas verificações executadas. As pendências acima são limites concretos de aceite, não trabalho declarado concluído por outro responsável.

## 7. Credenciais e configuração do dono

Tela: Site Core → Configurações, nos campos responsáveis de Conexões e entregas, Medição e anúncios e e-mail automático. Campo vazio mantém o valor; apagar é explícito. A ajuda local informa onde copiar cada credencial e distingue token pessoal, bot, usuário do sistema, CAPI, Access Token, Primary Client Secret, Key de webhook e senha SMTP.

Pipedrive exige 40 caracteres hexadecimais e domínio da empresa. Slack bot exige `xoxb-`, `chat:write`, acesso de leitura pertinente e participação no canal salvo; não aceita token de usuário/aplicativo no campo do bot. Meta exige formato EAA, validade e os escopos exibidos para leads ou CAPI. LinkedIn usa Client ID, Primary Client Secret e token com `r_marketing_leadgen_automation`; integrações Core que compartilham credenciais precisam do mesmo Client ID. Clarity valida JWT localmente ao salvar; o teste de exportação continua explícito e consome sua cota de dez consultas por projeto/dia.

`f3base/credenciais-ler` é administrativa e não chama fornecedor. `f3base/credenciais-verificar` exige `nome` e `revisao_esperada`; uma candidata vai em `credential`. Para identificar o que já existe, usar `usar_salva=true`. A prévia normal não grava o segredo; conferir o resultado, confirmar mudança quando requerida e salvar pelo fluxo administrativo com a revisão vigente. Não incluir valores em relatório, mensagem ou arquivo de evidência.

Nenhuma nova credencial é necessária apenas para instalar esta versão. As integrações existentes não são ligadas nem rotacionadas automaticamente.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `base-site-core-fator3-1.50.0-instalador.zip` | 2250902 | `7021163d158b1a353e012823e14b611c17cb45d82125d3230784eb84f2b6b8ea` |
| Fonte | `base-site-core-fator3-1.50.0-fonte.zip` | 4797482 | `6a50e171b5042641f99aaea4a7c46c7b7ace51227450a7ee4cd0c2e564805a18` |

Relatório externo canônico: `base-site-core-fator3-1.50.0-relatorio.md`. A cópia no fonte é identificada como anterior ao fechamento; os bytes/hash do próprio fonte são preenchidos somente no relatório externo após empacotar, evitando circularidade.

O instalador contém somente a raiz `base-site-core-fator3/`. O fonte contém código, build, testes, relatórios recebidos e evidências sanitizadas, sem ZIP aninhado, banco, cookies, credenciais reais, node_modules ou auxiliares QA no runtime. O build certifica que os 458 arquivos do runtime do fonte são idênticos aos do instalador final. O plano da rodada está incluído no fonte; não há impacto novo que exija documento individual nesta entrega.
