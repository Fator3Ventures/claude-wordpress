# Entrega — Fator3 Site Core 1.60.0

Revisão: 1 · Data/hora: 2026-10-29T00:49:54+00:00 · Rodada: implementação, integração e homologação autorizada no Site-Teste
Slug: `base-site-core-fator3` · Versão/build: `1.60.0` / `1.60.0`
Status: **apta-no-escopo-testado**. Código entregue e Site-Teste confirmado; os aceites reais específicos da frota estão discriminados na seção 6.

## 1. De onde esta versão entra

Instalação WordPress limpa ou atualização direta da base canônica **Core 1.59.0**, sem intermediária. Fonte recebido: 4884074 bytes, SHA-256 `26093d43ebfdc09b97ccbcb366a69673cd2154747e9f35b5953593a7c03c56c8`; instalador-base: 2825862 bytes, SHA-256 `8f3992e89b44f53a59e0e2af314ff8548fe2aadfcc06afe30e395610b1b7c832`. Os dois originais permaneceram inalterados.

Entrada funcional: `inputs/1600/Fator3 Site Core(20261028-235316).md`, com a regra do dono de 28/10 para credenciais e os pedidos 322 e 330–334. Os itens 314–321 e 323–329 já aceitos pela frota não foram reabertos; regressões pertinentes foram reexecutadas. Normas 01/02 revisão 5, de 23/10/2026, incluídas no runtime; os avulsos revisão 4 são anteriores. Plano e avaliação prévia: `history/1600/PLANO.md` e `history/1600/IMPACTO-META-330.md`.

Requisitos preservados: WordPress **7.1.2**, PHP **8.3.6 de 64 bits**. Provas nativas em WordPress 7.1.2 e 7.1.3/PHP 8.3.6; instalação e provas no Site-Teste em WordPress **7.1.4/PHP 8.3.36**. Contrato administrativo **8.24.0**; perfil `piso-padrao-3.6`; ciclo de instalação de **17 etapas**, sem nova migração estrutural. O mínimo do Pipedrive 0.3 é PHP 8.3.36 e não foi reduzido.

## 2. Convivência e encaminhamentos

| Acompanhante | Versão examinada e observada no Site-Teste | Escopo |
|---|---|---|
| MCP | 0.36.0 | Autorização, schemas, leitura documental, upload privado idempotente, sondas e recibos. |
| Meta | 0.14.0 | SDK original `meta-ads-reader/1.0.0`; concessões e histórico locais reais do SDK, sem Graph nos ensaios. |
| Google | 0.22.0 | Presença e integração preservadas; contratos comerciais/GA4 anteriores não alterados. |
| LinkedIn | 0.12.0 | Presença, autorização e integração preservadas; contrato comercial anterior não alterado. |
| Pipedrive | 0.3.0 | Ativo no Site-Teste/PHP 8.3.36; catálogo observado pelo ciclo. Preflight de candidato inválido não cria contato. |

MCP 0.36 e Meta 0.14 já estavam instalados antes do Core. Não se alterou nem redistribuiu código de acompanhante. Identidades integrais dos pacotes novos em `inputs/1600/packages.json`; matriz de reprodução em `build/COMPANIONS.md`. A combinação observada não é homologação universal de todas as funções desses pacotes.

### Impactos e pedidos emitidos nesta rodada

| Destinatário | Versão examinada | Classificação / situação | Ticket | Documento |
|---|---|---|---|---|
| Responsável Meta / frota | Meta 0.14.0 | Consequência de implantação: uma reconcessão explícita por consumidor/conta após a troca; sem alteração solicitada na API Meta. Implementação e prova Core concluídas, ação operacional da frota pendente onde Ads estiver ativo. | Core 330 | `base-site-core-fator3-1.60.0-impacto-wp-mcp-meta-fator3.md`, conteúdo do encaminhamento prévio, sem revisão para mero encerramento. |

O hash antigo incluía o mapa. O novo cobre acesso e geração monotônica; não se reaproveita silenciosamente a autorização antiga. Após a primeira reconcessão, editar parceiros mantém a concessão. Desligar/religar ou trocar/restaurar conta exige nova concessão, impedindo reviver uma anterior. O SDK Meta 0.14 passou nas 46 verificações locais e nas 46 no ambiente isolado do Site-Teste. As respostas e esse resultado são registrados aqui, sem criar documento novo apenas para declarar atendimento.

### Tratamento de impactos recebidos e anteriores

Os relatórios MCP 0.36 e Meta 0.14 foram considerados com seus fontes originais e hashes. A regra nova de credenciais foi aplicada ao consumidor Core; não foi presumido que avisos do produtor corrigiriam validações locais do Core. O patch Google 0.22 e o encaminhamento LinkedIn 0.12 → MCP, preservados em `inputs/1590`, pertencem à base 1.59 e não foram reaplicados nem reemitidos. A lacuna de auditoria descrita contra MCP 0.34 é histórica; não é apresentada como defeito atual de 0.36. O aceite dos itens anteriores permanece no estado da frota indicado pelo pedido recebido.

Não foi identificado novo contrato obrigatório para Google, LinkedIn, Pipedrive, Implantador ou tema: fronteiras, seleção de clientes e proprietários de estado foram preservados. Isso não substitui aceites reais desses responsáveis.

## 3. Mudanças e evidência

| Pedido | Problema | Mudança | Resultado / prova |
|---|---|---|---|
| 322(a) | Host `www` barrava os sites autorizados para CRM. | Remove apenas o `www.` inicial antes da comparação exata de ctooffice.com.br/korvena.com.br. | Ensaios com host `www`; Site-Teste continua fora da criação de objetos CRM por esse caminho. |
| 322(b) | Aviso e automático não tinham entrega/limpeza individual comprovável. | Salto `aviso_email` e automático só à própria caixa explicitamente homologada. Intenção durável antes de SMTP, Message-ID exclusivo e assinatura; confirmação por IMAP; exclusão de UID autoral com UIDPLUS. | 31 verificações de e-mail, 37 do caminho completo com transportes simulados. Sem Cco/Smart Bcc, Sent APPEND ou atividade comercial de e-mail. Mensagem alheia marcada Deleted preservada; ACK perdido reconciliado sem reenvio. |
| 322(c) | Slack suprimido sem indicação operacional suficiente. | Recibo informa `f3base_testes`, `destinos.slack`, valor e política efetiva. | Suprimido é declarado; política do site não é alterada pelo teste. |
| 330 | Mapa editorial invalidava concessão; sem padrão da conta. | `parceiro_padrao`, origem `mapa_conta_core`; campanha explícita prevalece. Revisão de acesso separada do mapa, com geração protegida pelo Core. Cursor ainda vinculado ao mapa e aos dados. | 46 verificações com Meta 0.14, repetidas no servidor; edição mantém grant, mudança de acesso bloqueia. |
| 331 | JSON-LD obrigatório deixava marcas sempre em falha. | `superficies_permitidas`: corpo, cabecalho, rodape, dados_estruturados; união com caminhos exatos, motivo em cada ocorrência. | JSON-LD permitido e menção visível fora dos caminhos proibida. Caminho tem precedência na indicação do motivo. |
| 332 | 403 ausente da saúde e 409 de robô degradava sinal humano. | Contagens diárias de `token_invalido` e `renovacao_aceita`; recibo HMAC de renovação, vinculado ao evento e agente, TTL e consumo único. Robôs/automação ficam em contagens e última resposta próprias. | Endpoint nativo com token vencido, renovação aceita e replay; Googlebot 409 sem mudar última operacional. 26 verificações JS fonte/minificado. |
| 333 | Cookie emitido no host sem `www` não marcava a navegação canônica. | Redireciona a `/f3base-teste/` no host de `home_url()` antes do cookie, preservando apenas saída explícita. | Três verificações HTTP nativas: redirecionamento, ausência de cookie no host divergente e cookie no canônico. |
| 334 | Formatos locais recusavam antes do fornecedor. | Formato vira `avisos` com regra/motivo na tela e nas rotas; espaços externos aparados com aviso. Recusa local de tipo, tamanho e controles; URLs mantêm validações. Clarity passa a conferir o candidato antes da gravação. | Fixtures e preflight **real** no Site-Teste: Pipedrive 39 caracteres → HTTP 401; Slack sem prefixo → HTTP 200 com recusa da API. Ambos com aviso e revisão salva preservada. |

O diagnóstico da análise conserva o legado sem misturá-lo com as contagens novas; mantém 30 dias de contagens diárias. Automação declarada/provável não se torna observação operacional. O recibo de renovação não é autorização de coleta e não dispensa token/consentimento válidos. O limite de credencial é 8192 bytes; controles são recusados antes de aparar. Remoção explícita de segredo permanece suportada; campo vazio na tela não substitui o salvo sem a ação de apagar. Não se registra conteúdo de credencial em avisos.

Clarity usa a cota de exportação compartilhada de 10 consultas/projeto/dia e a trava existente; quota ou indisponibilidade preserva a salva. Aceitar token não prova remotamente a seleção administrativa de projeto; essa limitação é exibida. Não se presume validade de fornecedor por formato ou por HTTP 200 isolado.

O recibo novo do caminho é versão 2; recibos versão 1 e limpeza antiga continuam interpretáveis. Mensagem movida para fora de INBOX antes da exclusão fica pendente, e o retorno à caixa permite retomar a limpeza. Troca de identidade/UIDVALIDITY bloqueia; não há EXPUNGE geral. O webhook de aviso continua explicitamente bloqueado nesse teste porque não dispõe de contrato de exclusão individual. Conversões são prévia, sem envio. A caixa de homologação deve ser exclusiva e sem encaminhamentos/regras externas que produzam cópias fora do alcance; a prova não cobre backups do provedor.

Foi corrigido também o prazo SMTP na instância correta do cliente, removendo uso de propriedade dinâmica obsoleta do PHPMailer nos caminhos afetados. Minificados e manifesto de assets foram reconstruídos com Terser 5.44.1. Nenhuma atualização incidental de dependências.

## 4. Instalação e prova da troca

Instalador final desta seção: SHA-256 da seção 8, slug esperado `base-site-core-fator3`. Foi transferido em partes ao estágio privado, montado e conferido por hash, e instalado por `plugins/upload-base64` com `zip_path`, `activate:true`, `overwrite:true`, chave idempotente e sondas de 30 s. Operação `bf465c2cf2fd2b18fa94ec0f8cd29b1c`; pré-imagem `031b7fe7fd67dbb498715bbe`. Arquivo público/raw não foi necessário nem publicado. A frota decide eventual publicação no repositório e nos outros sites.

Leitura de prontidão: `f3base/resumo-operacional-ler`, parâmetros `{"campos":["pacotes","atualizacao","recuperacao","cron_24h"]}`. Resultado final: Core 1.60.0/contrato 8.24.0 ativo, atualização `concluida`, confirmada no executor em `1793234251`, recuperação `core_operacional`, sem pausa/falha. Cabeçalhos e navegação verificados; Pipedrive `verificacao_automatica_reaproveitada`, corretamente distinguida de nova consulta de catálogo. Home e `/wp-json/` responderam 200 nas sondas antes/depois e após a retirada do controlador.

| ID | Ambiente | Cenário | Resultado | Evidência | Limite |
|---|---|---|---|---|---|
| N1 | WP 7.1.3 / PHP 8.3.6 | Limpa + 1.59→1.60, repetir migração, uninstall e reativação | Ambos aprovados no instalador final | `evidence/1600/native-cycles-1600.json` | Bancos descartáveis; intervalo final acelerado só na fixture. |
| N2 | WP 7.1.2 / PHP 8.3.6 | Mesmos ciclos e preservação das cinco tabelas preenchidas | Ambos aprovados no mesmo hash | `evidence/1600/minimum/native-cycles-1600.json` | Mesmo limite da fixture. |
| F1 | WP nativo / Meta 0.14 real | Pedido 330 e regressões de histórico/cursor/concessão | 46 verificações | `request-330-meta0140.json`; `site-request-330-meta0140.json` | Sem Graph e sem concessão real de cliente. |
| F2 | WP nativo local e Site-Teste isolado | Pedidos 331–334 | 31 verificações em cada execução | `request-331-334.json`; `site-request-331-334.json` | HTTP de fornecedor controlado; endpoint/persistência reais. |
| F3 | WP nativo e peers SMTP/IMAP simulados | Propriedade, destinatários, entrega, exclusão e mensagem movida | 31 verificações; repetidas no mínimo | `request-322-mail.json` | Não mede entregabilidade real. |
| F4 | WP nativo, fornecedores simulados | Caminho completo exercitável e limpeza | 37 verificações | `request-322-full-1600.json` | Slack/CRM/SMTP/IMAP sintéticos; conversões prévia, webhook bloqueado. |
| F5 | WP nativo | Estado, reentrada, autorização, CRM/Slack e limpeza | 41 + 20 verificações | `request-322-1600.json`; `request-322-remotes-1600.json` | Primeira suite também passou no Site-Teste isolado. |
| F6 | HTTP PHP local | Host canônico antes do cookie | 3 verificações | `request-333-http.json` | Não é navegação gráfica em korvena.net.br. |
| J1 | jsdom 27.4.0 | Renovação + regressão do formulário; fonte e minificado | 26 + 44 verificações | `request-332-dom.json`; `request-317-dom.json` | Não é navegador gráfico. |
| R1 | Laboratório WP nativo | IMAP, marcas, formulários, canais, qualidade, identidade, execução automática e permissões | Suites aprovadas, sem falhas booleanas | `request-305-imap`, `request-325`, `request-317`, `request-315-318-319`, `request-314-317-328-329`, `review-328-329-1600`, `review-identidade-1580`, `request-326`, `permissions-mcp-1571` | Somente execuções em `evidence/1600`; históricos não entram como novas provas. |
| D1 | WP 7.1.2 e Site-Teste WP 7.1.4 | Documentação integral, hashes, schemas e acesso | 153 documentos, 670 páginas, 1768 assertivas + 2 contagens; zero falha | `minimum/docs-1600.json`; `site-docs-1600.json` | A execução local preliminar de 1766 entradas antecede a atualização da cópia documental do inventário; não é o fechamento. |
| S1 | Site-Teste compartilhado | Candidatos fora do padrão consultados nos fornecedores | Ambos recusados remotamente, avisos emitidos, salva inalterada | `site-preflight-real.json` | Invocação da ability pública por controlador fechado; revisão permaneceu interna, sem expor segredo. |
| S2 | Site-Teste compartilhado | Arquivos, telas e estado final | 779 arquivos idênticos ao instalador; opções inspecionadas preservadas | `site-read.json`; `release-integrity.json`; `site-final-summary.json` | Prova de origem interna; não reivindica cache/CDN externo universal. |

PHP: lint dos **556 arquivos** do runtime em PHP 8.3.6. Fonte/instalador/servidor têm os mesmos 779 arquivos; manifesto SHA-256 `05ed166d32333328af6729553d82a7d1564b17fa39296af75157f1af6288523a`.

Documentação: índice `docs/DOCUMENTACAO.md`, ability `f3base/documentacao-ler`. Além da leitura integral paginada pela ability no servidor, seis documentos atuais foram lidos integralmente pelo conector e seus hashes comparados à árvore final: índice, release, agentes, credenciais, caminho e Meta Ads. Dicionário, inventário e schemas gerados do catálogo executável Core isolado; 176 abilities e 90 opções operáveis documentadas. O inventário fechado inclui 164 opções e 67 tabelas. Leituras não fazem chamadas a fornecedores.

Estado final da homologação: tabela/usuário/arquivos de QA isolados; **98 tabelas temporárias eliminadas, zero restante, diretório e manifesto removidos**. Controlador MU e ZIP de estágio removidos por hash. Preflight não trocou credenciais; não criou pessoas/leads/mensagens reais. Permanecem o Core instalado, os acompanhantes preexistentes, os recibos de operação e backups privados legítimos do canal. Nenhuma suite alterou o banco compartilhado para simular dados comerciais. Um candidato anterior, ainda em transferência, foi cancelado antes da instalação após a revisão do caso de mensagem movida; somente o hash final da seção 8 foi instalado.

## 5. Banco e volta de versão

Nenhuma tabela nova ou mudança destrutiva de schema. Campos aditivos de configuração, diagnóstico e recibos; tabelas, listas vazias, autoria, segredos cifrados, cursores e registros históricos da base preservados nos ciclos. A geração de acesso Meta só é gravada na opção com comparação de revisão, junto da mudança de acesso; leituras não migram autorização. Diagnóstico novo mantém contagens legadas separadas.

Antes de voltar versão, preservar backup conjunto de arquivos, banco, diretório privado/estado e salts; suspender e reconciliar execuções pendentes. Restaurar apenas o ZIP 1.59 não desfaz diagnósticos, recibos novos, concessões ou efeitos externos. Não retomar recibo versão 2 num runtime antigo sem concluir sua limpeza na 1.60. A desinstalação conserva as cinco tabelas históricas, suspende pendências declaradas e remove os agendamentos próprios; não apaga mensagens/CRM por iniciativa da desinstalação. O canal declara `database_effects_reversible:false` para a troca.

## 6. O que permanece pendente

- **Frota / ctooffice.com.br:** execução real do 322 com `www`, caixa exclusiva homologada, Slack autorizado e Pipedrive, releitura e limpeza na conta, no Slack e na caixa; repetir com Pipedrive desligado. Implementação comprovada em peers/SDKs controlados, sem afirmar esse aceite externo. korvena.com.br segue autorizado para CRM, sujeito à presença do formulário. Site-Teste não foi usado para criar objetos de CRM.
- **Frota / korvena.com.br:** reconceder Meta Ads uma vez após atualizar, selecionar parceiro padrão, observar campanha não mapeada e confirmar grant preservado depois de editar parceiros. Nenhuma concessão de produção foi criada por esta entrega.
- **Frota / ctooffice.com.br e korvena.net.br:** aplicar a exceção de marca desejada e conferir páginas reais; aceitar saúde com token vencido numa cópia real de cache e marca de teste em navegação entre hosts. As provas nativas/DOM/HTTP cobrem a implementação, sem afirmar navegação gráfica nesses sites.
- **Frota/dono:** publicação do pacote nos demais 11 sites e eventual URL raw. A autorização exercida aqui foi a instalação no Site-Teste. Nenhum pacote acompanhante foi alterado; os aceites anteriores da pendência 20 do estado da frota continuam sob seu responsável.

Não resta falha de implementação observada nas provas encerradas. Entregabilidade, regras externas de caixa, backups do provedor e auditorias/aceites de outras contas não são inferidos de fixtures. Webhook sem exclusão individual continua declarado bloqueado, sem promessa de apagar efeitos que o contrato não oferece.

## 7. Credenciais e configuração do dono

Telas e rotas atuais em `docs/CREDENCIAIS-1.60.md`, `CAMINHO-LEAD-1.60.md`, `META-ADS-CORE-1.60.md`. Pipedrive usa token pessoal e domínio configurado; Slack usa credencial aceita pelo fornecedor e canal selecionado; Meta/LinkedIn conservam seus ativos/escopos; Clarity requer projeto selecionado e cota disponível. Padrões históricos são orientação e aviso, não prova nem recusa de validade remota. URLs de webhook permanecem estritas.

Para o caminho de e-mail: `f3base_email_site.envio_ativo`, alocação confirmada, endereço próprio incluído em `homologacao_emails`, acesso IMAP com UIDPLUS e SMTP válidos; automático requer sua configuração ativa. Não alterar política global de teste para habilitar silenciosamente Slack. Em Meta, gravar `parceiro_padrao`/`parceiros` usando a revisão atual e reconceder pelo Meta 0.14 com a revisão de acesso vigente. A instalação não ativa essas integrações por conveniência.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `base-site-core-fator3-1.60.0-instalador.zip` | 2842430 | `1dc4e94305ea55394024d6527bc06b46209f0ae51a55f734853763bcb232e27c` |
| Fonte | `base-site-core-fator3-1.60.0-fonte.zip` | 5106586 | `afdac358331e3894480b59fc8b57cc411909d3c7b399a6f998c996b35e7d25fe` |

Relatório externo canônico: `base-site-core-fator3-1.60.0-relatorio.md`. A cópia interna é anterior ao fechamento do fonte; o tamanho/hash do próprio fonte é preenchido somente neste relatório externo para evitar circularidade. Complemento pertinente: `base-site-core-fator3-1.60.0-impacto-wp-mcp-meta-fator3.md`, encaminhamento técnico prévio referido na seção 2. Os links de entrega acompanham os quatro arquivos na mensagem final.

O fonte contém runtime final, build/reprodução, testes, locks, planos, insumos documentais, evidências sanitizadas e histórico identificado. Não contém ZIP dentro de ZIP, laboratório, banco, log bruto, node_modules, extrações de acompanhantes, senhas, grants reais ou dados de clientes. `source-manifest.json` permite conferir a árvore. Resultado de build e comparação byte a byte registrados no fechamento; não se deve reaplicar scripts históricos de patch sobre a árvore final.
