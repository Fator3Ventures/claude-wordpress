# Fator3 MCP Meta 0.32.1 — entrega dos pedidos 34 e 35

20/11/2026 · Revisão 1 · Fuso America/Sao_Paulo. **Ativo e testado no Site-Teste.** Corrige o falso incidente de público; o aceite de produção depende da implantação pela frota e de 26 horas de observação. O Core oficial ainda pode enviar e-mails de recuperação de episódios já notificados. A proposta ao Core está identificada na seção 2.

## 1. Versões, alcance e requisitos

Aplicável diretamente à **0.31.0** usada na frota e à **0.32.0** que introduziu o guia visual no Site-Teste. A 0.32.1 é uma correção de patch. Slug e basename: `wp-mcp-meta-fator3/wp-mcp-meta-fator3.php`. WordPress 7.1.4+, PHP 8.3+ de 64 bits. Referências: `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos revisão 5 de 02/11/2026, padrão Meta, regra comum, guia visual comum e específico e Pedidos MCP Meta 34 e 35. A instalação mantém os cinquenta esquemas de entrada, as rotas, as capacidades e os nomes de opções.

## 2. Convivência e impacto externo

Na bancada testamos Core 1.100.1, MCP 0.54.0, Google 0.42.0, LinkedIn 0.27.0 e Pipedrive 0.13.0. No Site-Teste, o inventário após a instalação mostrou **Core 1.100.1, MCP 0.55.0, Google 0.43.1, LinkedIn 0.27.0 e Pipedrive 0.12.0**. Esses pacotes não foram substituídos por esta manutenção do Meta. O transporte do Site-Teste leu toda a documentação e os autotestes do Meta. Na instalação compartilhada a folha do Meta coincide byte a byte com as do Core, Google, LinkedIn e MCP (neste último, em `core/assets/css/f3-ui.css`). O Pipedrive 0.12.0 instalado não forneceu a folha no caminho padrão; a 0.13.0 examinada em bancada fornece o mesmo hash. Nenhuma adaptação identificada no LinkedIn.

**Impacto no Site Core.** A 0.32.1 fecha as quatro agendas falsamente classificadas como incidentes e não faz nova abertura. O Core 1.100.1 transforma a recuperação de um episódio já notificado em um novo e-mail com o assunto de recuperação. Para atender também à condição de nenhuma mensagem de `agenda_parada` causada pela reclassificação, há uma [proposta para o mantenedor do Core](wp-mcp-meta-fator3-0.32.1-impacto-base-site-core-fator3.md). Ela foi preparada em cópia isolada. O ensaio da proposta passou em 153 verificações no WordPress isolado, além de 22 controles de reserva e repetição. Foram zero e-mails novos de abertura **e** de recuperação para os quatro episódios reclassificados. O pacote Core oficial não foi alterado. O histórico de e-mails aceitos antes da atualização permanece preservado.

## 3. Mudanças, testes e diferenças observadas

**Agendas e disponibilidade.** Uma resposta demográfica válida, completa, com zero linhas úteis e apenas indisponibilidades atribuídas às métricas demográficas solicitadas, resolve a execução sem dados. O resultado `nao_aplicavel` e `availability_assessment` ficam visíveis na agenda. `below_minimum_followers` exige uma contagem válida do perfil; sem essa prova o motivo é `audience_data_unavailable`. Nenhum zero substitui um valor suprimido e `last_success_at` não avança sem linhas úteis. A mesma agenda continua habilitada na cadência original. Uma falha de autenticação, permissão, quota, rede ou formato continua diagnosticável.

| Observação | Agenda diária | Agenda semanal |
|---|---:|---:|
| Sem execução resolvida nem falha comprovada | 50 horas: 2 intervalos + 2 h | 14 dias + 2 h |
| Falha real persistente, contada da primeira tentativa que falhou | 26 horas: próxima tentativa prevista + 2 h | 7 dias + 2 h |
| Execução concluída com indisponibilidade comprovada | Resolve a pendência; mantém a agenda | Resolve a pendência; mantém a agenda |

**Comprovação na fila do Core.** A evidência anterior em CTO Office confirmou as quatro agendas semanais com erros exclusivos de `follower_demographics`, zero linhas úteis, diagnóstico nulo e quatro episódios Meta abertos. A quantidade de seguidores não ficou demonstrada nessa conta. Reproduzimos a assinatura em WordPress e no Core oficiais, com Graph simulada e transporte SMTP bloqueado. Na atualização **0.31.0 → 0.32.1**, foram 32 verificações sobre a versão anterior e 113 sobre a corrigida; nenhum passo carregou a 0.32.0 nesse banco. No primeiro bootstrap, os quatro episódios fecharam. Em observações repetidas até **93.604 segundos** de avanço do relógio Meta, havia **0 novas aberturas de público, 4 recuperações na fila e 1 abertura da falha diária real**. O teste leu `f3base/email-wordpress-fila-ler`. A atualização **0.32.0 → 0.32.1** também passou, inclusive quando um episódio existia só no Core e outro continha uma abertura antiga pendente no produtor.

**Regressão e documentação.** A suíte integrada somou **633 verificações sem falhas**, em 12 instalações de WordPress 7.1.4, PHP 8.4.27, MariaDB 11.8.6. O total inclui 32 verificações de reprodução na base e 112 após a correção na prova de incidentes. Preservação do histórico, política de recuperação, orçamentos, cron, contratos e integração MCP foram exercitados. O instalador tem 81 arquivos, incluindo 44 PHP; o fonte contém cópia byte a byte do runtime. Entraram uma classe de revisão e ajustes internos em coleta, prazos, diagnóstico e normalização de respostas. A folha comum tem SHA-256 `15ef0d932b1be12a541b8408b061ee276a4db9d6650476f92b5e2f41eefc0c2b`; a folha específica de 4.205 bytes permanece idêntica à 0.32.0.

**Painel do Pedido 34.** Os três grupos e dez subabas mantêm seus endereços, inclusive sem JavaScript. O WordPress posiciona os avisos externos depois do cabeçalho e antes da navegação quando o script de administração é executado. Os cartões, os estados e os formulários usam a folha comum; listas longas conservam busca, total e paginação. A nova descrição da demografia distingue ausência de dados de contagem comprovada abaixo do mínimo. A bancada com dados aprovou 360 verificações do guia, cinco de interação/paleta, 22 fluxos de navegação e três verificações específicas de texto do diagnóstico. As 33 imagens locais passaram pela conferência do título, versão, aviso e botão.

**Conferência no Site-Teste.** Em cada célula, critérios aprovados / 12 do guia §7. Aviso real do PublishPress Authors, três larguras do documento e uma segunda paleta nativa do WordPress. O recorte mostra o painel e omite a identificação do usuário. Elementos comercialmente preenchidos, como listas longas, foram exercitados na bancada. O auxiliar de medição foi removido e o Meta permaneceu ativo.

| Subaba | 360 px | 768 px | 1440 px |
|---|---:|---:|---:|
| Conexão | 12/12 | 12/12 | 12/12 |
| Ativos | 12/12 | 12/12 | 12/12 |
| Consumidores de anúncios | 12/12 | 12/12 | 12/12 |
| Relatórios | 12/12 | 12/12 | 12/12 |
| Coletas | 12/12 | 12/12 | 12/12 |
| Histórico | 12/12 | 12/12 | 12/12 |
| Conversas | 12/12 | 12/12 | 12/12 |
| Arquivo de Stories | 12/12 | 12/12 | 12/12 |
| Diagnóstico | 12/12 | 12/12 | 12/12 |
| Ajuda | 12/12 | 12/12 | 12/12 |

[Caderno visual: 30 imagens no Site-Teste e 30 na bancada](wp-mcp-meta-fator3-0.32.1-prova-visual.html). Imagens, medidas, controle das versões e diagnóstico em `evidence/0321/`. Nas capturas normais os avisos aparecem depois do cabeçalho; sem JavaScript, a navegação continua por URL e os avisos conservam a posição original do WordPress.

## 4. Instalação e validação no Site-Teste

O MCP recebeu o ZIP pelo slug esperado e pelo SHA-256 da seção 8; confirmou 0.32.0 → 0.32.1, ativo antes e depois, com as duas sondagens bem-sucedidas. WordPress 7.1.5, PHP 8.3.37, MCP saudável e oito verificações locais do Meta aprovadas. O site tinha **zero conexões e zero agendas ativas**; não serviu de fonte de prova sobre público comercial. Pelo leitor instalado `meta/documentation`, o índice e os **32 documentos completos**, em **45 páginas e 328.954 bytes**, coincidiram individualmente com os bytes do ZIP. Não houve implantação em produção ou publicação de arquivos em repositório.

## 5. Banco, migração e recuperação

Antes da troca no Site-Teste, foram salvadas cópias privadas das duas tabelas do Meta (809 registros) e de 12 opções. Nenhuma nova tabela, nome de option ou permissão. Na primeira execução o Meta verifica as evidências duráveis da mesma consulta; reclassifica apenas a passagem comprovada, preserva os jobs e páginas e reconcilia o mesmo identificador do episódio. Um marcador técnico existente registra a conclusão; os valores das opções de negócio são preservados. Uma falha de persistência ou interrupção durante a reconciliação pode ser retomada sem repetir uma abertura obsoleta. Registros sem prova suficiente não são reescritos. Não há reprocessamento da Graph nem regravação de credenciais na migração. Instalar por atualização, sem desinstalar. Corrigir versões publicadas com nova versão. Não apagar incidentes, e-mails ou histórico para obter um resultado de aceite.

## 6. Limites e critérios em produção

CTO Office foi consultado apenas em leitura e estava na 0.31.0. A consulta ao site revelou supressão dos dados, mas não comprova que o perfil estivesse abaixo do limiar numérico. Os instantes da bancada foram controlados; não equivalem a 26 horas decorridas em produção. Depois que a frota atualizar um site afetado, conferir de imediato e ao completar 26 horas: agendas habilitadas e sem `schedule_collection_unresolved`, episódios fechados, nenhuma nova abertura de público e fila distinguindo as aberturas históricas, recuperações históricas e mensagens novas. Um controle diário com falha operacional continua devido após 26 h. Material da bancada não prova entrega de e-mail externo nem acesso comercial às APIs da Meta.

## 7. Credenciais e procedimento para o dono

Use **Ferramentas → Fator3 MCP Meta → Suporte → Diagnóstico** e inspecione a última coleta/avaliação. Para o aceite use `meta/list-schedules`, `meta/health`, `f3base/incidentes-tecnicos-ler` e `f3base/email-wordpress-fila-ler`, com acesso administrativo autorizado. Não é necessário recriar agendas, regravar tokens ou alterar a carência do Core. Para ver o comportamento da proposta no Core antes de atualizar a frota, siga o encaminhamento da seção 2.

## 8. Identidade dos arquivos

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| [wp-mcp-meta-fator3-0.32.1-instalador.zip](wp-mcp-meta-fator3-0.32.1-instalador.zip) | 311792 | `c8dd8e3bfd43e5ece774920ecc12d12b1b4ceb2d1080b1ddca2da3d731568e70` |
| [wp-mcp-meta-fator3-0.32.1-fonte.zip](wp-mcp-meta-fator3-0.32.1-fonte.zip) | 38695209 | `deac164f5e76e77b0fad2c894b15b74345951b5169ce37ebc057f363bc9f3b40` |
| [wp-mcp-meta-fator3-0.32.1-impacto-base-site-core-fator3.md](wp-mcp-meta-fator3-0.32.1-impacto-base-site-core-fator3.md) | 5813 | `ac19a1952fdb012c939ddfd2687599010cfbd81386ffe153256e2418e6e24b18` |
| [wp-mcp-meta-fator3-0.32.1-proposta-base-site-core-fator3.zip](wp-mcp-meta-fator3-0.32.1-proposta-base-site-core-fator3.zip) | 15262 | `0d13e52d59e51622a74fd407d23244467ae95a03485296a2b965872b2a32297c` |
| [wp-mcp-meta-fator3-0.32.1-prova-visual.html](wp-mcp-meta-fator3-0.32.1-prova-visual.html) | 11241444 | `58a9ca1066c84c93d24860f23e2ae1b1b48c274fe003b943607c03ef552c690e` |

A cópia interna do relatório precede o fechamento do fonte.
