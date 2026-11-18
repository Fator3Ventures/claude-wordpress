# Entrega — Fator3 Site Core 1.94.0

**Revisão 1 · 18/11/2026 · Implementação e homologação · Com pendências de aceite na frota.**

A 1.94.0 está ativa no Site-Teste. O executor confirmou a atualização às **18h13min26s de Brasília**, com zero falhas. O Core deixou de inicializar o REST ao verificar o registro do canal MCP e passou a guardar o contexto das novas transições. A migração preservou a fila existente.

## 1. De onde esta versão entra

Instalação limpa ou migração direta de `base-site-core-fator3` 1.93.0. A base oficial tem 5.664.727 bytes e SHA-256 `eec2ee1fda142863966de9568b61ee5f6914ebb1af371207d8074e7c77f9c1a8`. As duas conversas anteriores deixaram um instalador idêntico e duas cópias do fonte em andamento. A mais recente continha os testes atualizados de autorização e integração. Nesta retomada, esses testes foram executados novamente, o instalador foi aplicado, o encaminhamento foi fechado para entrega e o fonte foi empacotado.

Requisitos do projeto: instalação única de WordPress 7.1.4 ou superior e PHP de 64 bits a partir de 8.3. A bancada usou WordPress 7.1.4 e PHP 8.3.6 nas provas de instalação e atualização. Os contratos integrados foram exercitados também em PHP 8.4.27. O Site-Teste executava WordPress 7.1.5 e PHP 8.3.36. As fontes do projeto contêm `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos na revisão 5 de 02/11/2026, além da regra comum e da aba do Core.

## 2. Convivência e encaminhamentos

Contrato administrativo `8.45.0`, perfil `piso-padrao-3.6`, 104 opções e 199 operações de domínio. A leitura administrativa `f3base/incidentes-tecnicos-ler` passou a incluir `historico_registro` no incidente de registro do canal após uma nova transição. O catálogo de operações mantém os mesmos nomes.

| Pacote | Bancada integrada | Site-Teste ao concluir | Fronteira verificada |
|---|---|---|---|
| MCP | 0.48.0 | 0.48.0 | Registro de rotas, estado local, autorização e documentação |
| Google | 0.37.0 | 0.36.0 | Abertura, repetição e recuperação com o produtor oficial da 0.37.0 na bancada |
| LinkedIn | 0.26.0 | 0.26.0 | Abertura e recuperação de incidente com deduplicação |
| Meta | 0.29.0 | 0.29.0 | Worker, observador e recuperação com transporte de e-mail interceptado |
| Pipedrive | 0.12.0 | 0.11.1 | Leitura paginada e seleção de um incidente sintético do Pipedrive na bancada |

Os seis runtimes da bancada, incluindo o Core, foram confrontados arquivo por arquivo com os instaladores oficiais após a retirada do patch experimental. O ensaio de cron usou WP Activity Log 5.7.0. O Implantador fica fora das interfaces alteradas.

**Encaminhamento ao MCP.** A inscrição tardia da rota continua relevante quando um terceiro inicializa o REST cedo. O [impacto individual do MCP](base-site-core-fator3-1.94.0-impacto-wp-mcp-fator3.md), revisão 2, contém causa, matriz de testes, arquivo e método, patch e aceite. Código do Core pronto. Incorporação oficial pelo mantenedor do MCP em aberto.

**Retornos dos demais mantenedores.** O relatório Google 0.37.0 registra a incorporação do produtor de avisos solicitado na 1.93.0. As provas próprias desta rodada exercitaram o contrato público de publicação e recuperação. Os relatórios LinkedIn 0.26.0, Pipedrive 0.12.0 e Meta 0.29.0 documentam suas respectivas integrações. A análise desses retornos e os ensaios da bancada dispensaram novas alterações de contrato nesses quatro pacotes.

## 3. Mudanças e evidência

| Pedido | Resultado | Prova |
|---|---|---|
| Core 430 / MCP84 | O observador consulta `ServerContract::status()` após a inicialização. Uma leitura inconclusiva preserva o episódio. Ausência real de rota, conflito ou falha verificada mantêm diagnóstico próprio. | Mesma sequência de inicialização em WP-CLI. Na 1.93.0, REST iniciado pelo observador e `mcp_route_missing`. Na 1.94.0, registro completo e lista de erros vazia. Com terceiro iniciando REST cedo, reproduzimos a falha residual do MCP e validamos o patch isolado. |
| Core 430 | Até 12 mudanças de estado do recurso `registro-wordpress` ficam no histórico administrativo. Cada entrada distingue observador do Core e publicação recebida, CLI, cron HTTP ou web, versão dos pacotes e estágio dos hooks. A fila conserva as entregas na ordem original. | 25 verificações na bancada, incluindo rota ausente, recuperação, leituras repetidas, fase incompleta, retenção das 12 transições, filtragem de texto livre e entrega da fila inteira ao coletor. |
| Core 423(g) | Regressão da agenda com WP Activity Log ativo. | Uma passagem WP-CLI com cache deliberadamente divergente executou os 16 ganchos uma vez cada. Foram 24 gravações próprias, zero erros, zero divergências finais e zero ganchos do ensaio remanescentes. |
| Core 429 | Regressão do catálogo sobre o instalador final. | 259 arquivos do catálogo idênticos à 1.93.0, incluindo os 256 fragmentos. O índice contém 44.528 códigos. A comparação histórica registra os 19 televisores corrigidos e as 272 mudanças de nome preservadas. |

O ensaio integrado de Google, LinkedIn e Pipedrive produziu cinco mensagens sintéticas interceptadas por execução, uma ocorrência do Pipedrive na projeção filtrada e zero chamadas HTTP. O visitante recebeu `permission_denied` pelo MCP e `ability_invalid_permissions` no WordPress isolado. A evidência de e-mail termina no coletor local.

## 4. Instalação e prova da troca

| Verificação | Resultado |
|---|---|
| Instalação limpa e migração 1.93.0 → 1.94.0 | A bancada registrou 20 etapas, confirmação no executor e zero falhas nos dois bancos. Na atualização foram preservados o aviso pendente, a antecedência de 11 dias e o atraso de 77 minutos configurados para o teste. |
| Integridade | 1.276 arquivos do runtime coincidiram com o instalador em conteúdo e ordem. CRC íntegro, raiz única e 611 arquivos PHP aprovados em verificação sintática. |
| Homologação no Site-Teste | O ZIP temporário da rodada anterior já estava em `wp-content/upgrade/`. A leitura do SHA-256, o tamanho e o arquivo principal da base coincidiram. `plugins/upload-base64` com `zip_path`, `expected_slug=base-site-core-fator3`, hash esperado e chave de idempotência registrou a pré-imagem e aplicou a atualização. |
| Prontidão | As sondas da página inicial e de `/wp-json/` retornaram HTTP 200 antes e depois. Em novas chamadas, `plugins/list` retornou `active=true` e `f3base/como-usar` com `compacto=true` confirmou `versao_alvo=1.94.0`, `estado=concluida`, `falhas=0` e `confirmada_no_executor_em=1795036406`. |
| Documentação pelo MCP | O índice incluiu `docs/RELEASE-1.94.0.md`. As 23 linhas foram lidas em três páginas, com o mesmo SHA-256 `9a60e41634e41f4eff74e2e3a9bbcfe43c4e754dd49afa851d0596746e905d22`. O texto remontado coincidiu com o instalador e uma consulta a documento ausente recebeu `documento_nao_catalogado`. |
| Estado e limpeza | A saúde do MCP retornou positiva. A única troca efetuada foi a do Core. A releitura do caminho do ZIP temporário confirmou sua ausência. A fila do canal preservou as 25 entregas observadas antes da troca. O e-mail técnico estava vazio. |

Na distribuição, a frota publica o instalador e o relatório pelo fluxo oficial, confere o hash dos bytes servidos e usa `plugins/upload` com hash e slug esperados. As evidências sanitizadas da homologação estão no fonte, em `evidence/1940/site-teste.json` e `revalidacao-final.json`.

## 5. Banco, migração e correção por nova versão

A 1.94.0 acrescenta `historico_registro` ao valor da opção existente do incidente do canal quando ocorre nova transição. O registro usa a trava por recurso, o identificador opaco vigente e a mesma gravação da fila. As reservas e transições anteriores permanecem válidas. A próxima abertura ou recuperação dá início ao novo histórico. O resultado de entrega incerta exige conferência do transporte antes da reconciliação administrativa. Correções de código posteriores à instalação seguem em nova versão.

## 6. O que permanece pendente

- **Mantenedor do MCP.** Incorporar e versionar o ajuste do transporte para o cenário de inicialização por terceiros. A cópia experimental e o MCP oficial foram testados separadamente.
- **Frota.** Conferir as primeiras transições naturais após a atualização e compará-las com uma leitura autenticada do canal. O histórico da 1.93.0 não permite atribuir a cada episódio antigo a causa reproduzida em laboratório.
- **Frota e responsável pelo e-mail.** Configurar o destino técnico autorizado e conferir abertura e recuperação na caixa postal. Com 25 entregas pendentes no registro do canal, o preenchimento do destino pode liberar avisos já acumulados. Nenhuma entrega foi marcada manualmente.
- **Aceite do pedido 423(g).** A observação de 24 horas no CTO Office, Korvena e Fator3 e a distribuição em produção seguem com a frota. O teste com divergência induzida de cache está concluído.
- **Fornecedores.** A bancada integrou as versões vigentes com transporte interceptado. Renovação de credenciais, provedores comerciais e entrega SMTP em uso real dependem dos ativos e destinos autorizados.
- **Metadado herdado.** O dicionário estático `docs/dados/contrato.json` conserva `base_atualizacao=1.90.0`. Para a instalação desta release, a origem efetivamente exercitada foi 1.93.0, como registram a nota de versão instalada e o recibo do executor.

## 7. Credenciais e configuração do dono

A atualização usa as credenciais existentes. O destino fica em **Site Core → Avisos técnicos por e-mail**, campo `f3base_avisos_tecnicos.email`. A leitura e a reconciliação de incidentes exigem acesso administrativo. As evidências desta rodada omitem os destinatários e os valores das credenciais.

## 8. Identidade dos arquivos

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| [base-site-core-fator3-1.94.0-instalador.zip](base-site-core-fator3-1.94.0-instalador.zip) | 5668055 | `0eff84a92622b3daa2aebd81437bbb2c33eaea648d1955c46e29ef70aedf9008` |
| [base-site-core-fator3-1.94.0-fonte.zip](base-site-core-fator3-1.94.0-fonte.zip) | 8109112 | `bb4e4c4058c8b3e2511cf55a8fb198c5219c3178d48bae5826f91f36a7d7bb8c` |

Relatório externo canônico. A cópia interna foi congelada antes do fechamento do fonte.
