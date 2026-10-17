# Entrega — Fator3 Site Core 1.35.0

Data: 2026-10-17 UTC (rodada iniciada em 16/10 no fuso de São Paulo). Estado: **implementado e instalado no Site-Teste**. Aceites específicos em produção/fornecedores permanecem identificados abaixo; não houve publicação na frota nem no GitHub.

## 1. De onde esta versão entra

Base direta imutável: Fator3 Site Core 1.34.0, instalador SHA-256 `3d3d3ffa084026a0f36e3badf852cba8aeb30620503878534328bddb9a260be1`. Pedidos recebidos em `Fator3 Site Core(1).md`: 212(a), 219, 220, 221, 222(a/b/c) e 223. Normas comuns revisão 4. Os relatos de instalação da 1.34 nos 12 sites são evidência recebida, não provas executadas nesta rodada.

Slug/pasta/basename preservados: `base-site-core-fator3/base-site-core-fator3.php`; provider, namespaces e Text Domain preservados. Versão minor 1.35.0. Contrato administrativo **8.1.0**; SDK `site-measurement-context/1.0.0`, schema 1, seis slots e enumeração fechada preservados. Cabeçalho mínimo agora **WordPress 7.1.2 / PHP 8.3.6, 64 bits**, exercitado em instalação nova e atualização direta.

## 2. Convivência e encaminhamentos

| Pacote | Versão observada | Prova desta rodada |
|---|---|---|
| Fator3 MCP | 0.23.0 | Upload MCP HTTP real em bancada e troca no Site-Teste |
| Fator3 MCP Google | 0.10.0 | Consumidor real de SDK: descritor, snapshot e catálogo paginado; ativo no Site-Teste |
| Fator3 MCP LinkedIn | 0.2.0 | Ativo e preservado no Site-Teste; Lead Sync remoto não reensaiado |
| Fator3 MCP Meta | 0.2.0 | Ativo e preservado no Site-Teste; API orgânica não alterada |
| WP Super Cache / Yoast SEO | 3.1.4 / 28.7 | Ativos antes/depois; sondas internas home/REST 200; HIT público não comprovado |
| Implantador | 2.8.0 recebido | Não executado nesta rodada; validação do responsável pendente |

Encaminhamentos criados no planejamento e atualizados no mesmo documento até revisão 3/entrega:

- `base-site-core-fator3-1.35.0-impacto-wp-mcp-google-fator3.md`: decisão necessária sobre descoberta de material. O consumidor 0.10.0 tem nomes fechados; adicionar download_material ao SDK 1.0.0 seria incompatível. A proposta inicial foi substituída: o evento opera no Core, mas sua configuração completa é administrativa 8.1.0. O SDK mantido descreve contato e não descobre material. Responsáveis Core/Google devem negociar revisão explícita para ampliar essa descoberta.
- `base-site-core-fator3-1.35.0-impacto-implantador-base.md`: validar mínimos e configuração aditiva; preservar contato e não ativar conversões de material automaticamente. Slug do destinatário confirmado no insumo anterior. Aceite de seu binário cabe ao responsável Implantador.

Não há alteração de contratos do MCP/Lead Sync/Meta orgânico nesta rodada; não se geraram avisos de versão sem consequência técnica. Impactos preparados para o dono, sem envio a terceiros e sem alteração dos outros pacotes. Nenhuma ordem de troca de acompanhantes foi necessária no Site-Teste: já estavam nas versões acima.

## 3. Mudanças e evidência

| Pedido | Implementação | Prova própria e limite do aceite |
|---|---|---|
| 212(a) | Reserva de memória adaptativa à folga (10%, mínimo 256 KiB, máximo 20 MiB), liberação de cache do alocador e diagnóstico de arena/viva/pico/base/crescimento por fonte. Usa memory_get_usage(true), não o pico nem memória do SO; não aumenta memory_limit. | WordPress real: 24 conteúdos, 28 dias, limite PHP 128 MiB com 126 MiB alocados; resumo/aquisicao e totais exatos aprovados. Recusas por teto, SQL e insuficiência têm diagnóstico. Site-Teste: 16/09–13/10 respondeu em ambas as visões, 149 visualizações, 117 sessões. Período CTO não foi reexecutado. |
| 219 | Cabeçalho deixa de prometer WP 6.4/PHP 8.1 e declara os mínimos ensaiados. | Instalação limpa e upgrade 1.34→1.35 aprovados em WP 7.1.2/PHP 8.3.6; MySQL 8.0.46. |
| 220 | Com blocos nos dois lados, compara conteúdo canônico exibido, sem fallback de notificação reconstruído; ignora block_id e flags emoji/verbatim. Sem blocos, normaliza escapes/autolinks HTTP/mailto. | Raiz e cinco respostas sintéticas com normalizações foram equivalentes; alteração textual real em cada parte foi divergente. Envio real e edição manual Slack pendentes. Alterar só fallback com blocos intactos não é divergência do conteúdo exibido. |
| 221 | Texto de alternativa Meta passa pelo value/rótulo do catálogo em varchar/text; múltiplos por vírgula; chave desconhecida e resposta livre preservadas; enum/set continuam IDs CRM. | Catálogo nativo e campos CRM reais do código, com valores sintéticos; rótulos, múltiplos, fallback, livre e enum aprovados. Prévia do contato Korvena indicado no pedido não foi lida. |
| 222 | Material usa download_material, MaterialDownload (Pixel trackCustom e CAPI), label Ads e conversion_id LinkedIn próprios; quatro interruptores false por padrão. Reserva separada por sessão/formulário; Pipedrive conteudo→site se chave ausente; relatório comercial intencao e totais separados. | Scripts completos e minificados: nomes/IDs corretos, controles independentes, ausência de fallback, consentimento, teste, modo servidor e contato preservado. PHP/DB: CAPI, ponto 151/53/54, deduplicação, migração idempotente, legado suspenso sem reescrever payload e entregue preservado. Tag Assistant/Events Manager e ações remotas não homologados. |
| 223 | array_values antes do espalhamento de coleção LinkedIn em array_merge, com lista vazia válida. | Renderer PHP real de Conexões e entregas chegou ao fechamento do formulário e botão de salvar com principal pausada; campos novos também renderizados. Inspeção visual e error.log Korvena pendentes. |

Evidências do fonte: `requests-1350.json` (46 verificações focadas), `editorial-1320.json` (script editorial-1350.php executado com 1.35) / `memory-1350.json` (45 verificações, incluindo 24 conteúdos reais e o limite real), `browser-routing.json` (32), `meta-routing.json` (6), `medicao-sdk-1330.json` (46, script herdado executado com 1.35), `google-compat.json` (3), `docs-1350.json` (373, predominantemente páginas de documentação), `native-cycles.json`, `mcp-cycle-1350.json`, `site-teste-1350.json`. Quantidades não equivalem a cenários externos independentes.

Lint: 209 PHP sem erro. JavaScript exercitado em Node VM com EventTarget e captura simulada de fornecedores; não é navegador gráfico. Tentativa de obter Chromium falhou por pacote de download inválido; nenhum resultado visual/Tag Assistant foi inventado. Os dois ativos alterados foram gerados com rjsmin 1.2.5; ativos herdados permanecem conforme manifesto com procedência do Terser da base.

Documentação instalada: RELEASE/AGENTES/CONVERSOES-CONTEUDO 1.35, índice atual, configuração, contratos, ajuda, inventário e dicionário regenerados do código (67 opções operáveis, 129 abilities Core, 54 tabelas inventariadas). O SDK 1.0.0 é explicitamente incompleto para material. Leitura local paginada, hash, confinamento e recusa a usuário sem permissão aprovados. Pelo MCP remoto, guia em duas páginas até proxima_linha nula e documento de material completo, hashes iguais ao instalador; ../wp-config.php recusado como documento_nao_catalogado. Leitura de ajuda não chamou fornecedor nem habilitou destinos.

## 4. Instalação e prova da troca

| Ambiente | Caminho | Resultado |
|---|---|---|
| WordPress descartável 7.1.2 / PHP 8.3.6 64 bits / MySQL 8.0.46 | Instalação nova sem acompanhantes obrigatórios | Ativo, estrutura pronta, 15 etapas; confirmação em requisição separada |
| Mesmo mínimo | Upgrade direto do instalador 1.34.0 | Configuração, procedência, callback, cursores e registro/filas sentinelas preservados por comparação; repetição sem nova migração |
| Bancada MCP HTTP 0.23.0 | plugins/upload-base64 sobre 1.34.0 | Upgrade, docs, revisão obsoleta e booleanos aprovados; **372 arquivos instalados idênticos ao ZIP final** |
| Site-Teste WP 7.1.3 / PHP 8.3.30 / MySQL 8.0.41 | Upgrade 1.34.0→1.35.0 | applied, ativo antes/depois, silent_reactivation; home e REST 200 antes/depois; ciclo concluída, 15 etapas, 0 falhas |

SHA-256 do instalador efetivamente validado e aplicado: `1368395e6c5842c21e822010310c1d544000ed7d72b2f6ee234491d18c686f20`. Operação remota `888380a6d4495406ab596d75bff18d3c`, request `3b867de4b85f295534782fe8`; pré-imagem de arquivos `9b59b2f6fb8569ed412f8cbb`. Backup SQL gzip privado anterior: artifact `30af1fc81d3dd42df04eeb30282dde90`, 16,610,135 bytes, SHA-256 `8faab28d876ecc9132a0969a28447f25f4a1511088550523b98875022fdc182c`. O backup contém dados originais e não acompanha o fonte público.

Ciclo remoto: início 1792197776, etapas concluídas 1792197781, finalização 1792197842 (Unix UTC), observada em requisição independente após intervalo real. Em bancada somente, o atraso de confirmação foi acelerado e identificado. Estado final real: **concluída**, versão 1.35.0, sem falhas. Os quatro interruptores de material foram relidos false, procedência padrão confirmada, contrato 8.1.0. Nenhuma configuração comercial foi ativada para testar. Sondas internas não comprovam acesso externo nem cache HIT.

## 5. Banco e volta de versão

Não há nova tabela/coluna estrutural nesta rodada. Acrescenta opções e migração versionada de estado existente: a reserva de aquisição de material usa SHA-256 truncado de `material|sessao|formulario`; a sessão original do lead/jornada permanece. Atualização só alcança reservas que ainda coincidem com a sessão antiga, tornando a migração repetível. Pendências CAPI de material sob nome Lead são suspensas (`evento_material_legado`) antes de envio. O payload histórico não é renomeado; entrega confirmada não é apagada/recriada. O consumidor também aplica a guarda antes do despacho. Incerteza/em envio conserva necessidade de reconciliação.

Retenções anteriores preservadas. Backup deve incluir banco, arquivos privados e guardas operacionais dos componentes. Reversão só de arquivos pode retomar a semântica antiga; usar backup compatível, suspender consumidores e reconciliar efeitos externos antes de reabrir filas. Não houve ensaio de rollback remoto nesta rodada; não se promete reversão automática de efeitos no banco/fornecedores.

## 6. O que permanece pendente

- **Frota/CTO:** repetir 212(a) no intervalo exato do pedido, após implantação autorizada; consulta Site-Teste não substitui o ambiente de 128 MiB do CTO. Crescimento por fonte não é perfil de memória por plugin; o diagnóstico declara a ausência dessa atribuição exclusiva.
- **Frota/Slack:** teste real em canal autorizado, raiz e respostas intactas e depois edição manual. Aqui não se enviaram/editaram mensagens em canal de terceiros; os testes foram sintéticos.
- **Frota/Korvena:** prévia do contato 4d3d1121… e abertura visual da tela/error.log após implantação. Não houve leitura de seus dados pessoais nem alteração do site nesta rodada.
- **Dono/CTO/plataformas:** escolher interruptores/ações próprias, validar ebook-porque-demora e contato-whatsapp em Tag Assistant, Meta e prévia Pipedrive. Eventos-chave, ações primárias, otimização e recebimento real não foram modificados/comprovados.
- **Google/Core e Implantador:** ações dos dois impactos; não declarar concluído trabalho do destinatário. SDK 1.0 não descobre material.
- **Validação visual/rollback:** navegador gráfico indisponível; renderer PHP e Node VM cobertos. Rollback, Lead Sync real, janelas 24/48 h e entregas externas antigas não foram reabertos nesta rodada; permanecem sob seus responsáveis na frota.

O dono recebe código pronto e a instalação de teste concluída. Os seis pedidos não são marcados como aceitos em produção apenas pela prova local.

## 7. Credenciais e configuração do dono

Nenhum valor de token, senha, cookie, banco ou log pessoal consta dos pacotes. Credenciais da instalação de teste foram preservadas; transportes de laboratório usam fixtures e bloqueio de rede/correio. O fonte não contém WordPress, dumps, backups privados nem dependências de fornecedor.

Material: configure `f3base_conversoes_conteudo` com quatro booleanos (ga4, meta, google_ads, linkedin); label em `f3base_google_ads.conteudo_conversion_label`; ID em `f3base_linkedin_conteudo_conversion_id`. Sem identificador próprio, Ads/LinkedIn não enviam material. Ativar Meta material invalida a homologação anterior do modo servidor e exige prova incluindo MaterialDownload; modo efetivo protegido é ambos até homologação compatível. Configurar não comprova recebimento. Use revisões e manage_options; o dono decide se material é conversão-chave/primária.

## 8. Identidade dos arquivos

Somente o instalador é instalável. Fonte tem raiz `base-site-core-fator3-1.35.0-fonte/`, código, scripts, testes, evidências sanitizadas, impactos e cópia deste relatório anterior ao fechamento do fonte. Nenhum ZIP contém outro ZIP da entrega. A cópia interna não contém o hash do próprio fonte; o relatório externo final fornece esse hash.

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| `base-site-core-fator3-1.35.0-instalador.zip` | 1944805 | `1368395e6c5842c21e822010310c1d544000ed7d72b2f6ee234491d18c686f20` |
| `base-site-core-fator3-1.35.0-fonte.zip` | 2056313 | `049ab61d5af4e005df8305b1edea6e1a55834ed4e133d3726c8cfe9ac49cd06c` |

Relatório externo final: `base-site-core-fator3-1.35.0-relatorio.md`. Impactos adicionais: os dois arquivos nomeados na seção 2.
