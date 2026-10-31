# Entrega — Fator3 Site Core 1.65.0

**Revisão 5 — 31/10/2026, America/Sao_Paulo. Homologação remota autorizada e executada; Core 1.65.0 ativo no Site-Teste. Estado da entrega: `com-pendencias`. Não liberada para a frota.**

Esta revisão registra a execução da autorização explícita “Autorizo” para enviar e instalar o ZIP identificado na seção 8 no Site-Teste. Preserva o planejamento revisão 3 em `PLANO-1.65.0.md`, o relatório revisão 4 em `history/1650/`, os registros históricos e o relatório separado de recuperação. O código recuperado já continha a implementação descrita abaixo. Na retomada foram refeitas as provas locais pertinentes; nesta rodada foram concluídos envio, instalação, pós-atualização e os ensaios remotos descritos. O runtime e o instalador permanecem inalterados. O fonte incorpora o modelo do ensaio temporário, as evidências e este relatório; seu hash mudou por esses complementos.

## 1. Bases aceitas

- Diretrizes do projeto: `01-instrucoes-agentes-plugins-fator3.md` e `02-padrao-desenvolvimento-plugins-fator3.md`, revisão 4 de 16/10/2026, lidas integralmente na recuperação; diretrizes relidas na retomada.
- Base imutável: Core 1.64.0, contrato 8.29.0. Instalador-base: 3020630 bytes, SHA-256 `e8c34d1cfbd347f6947e4e208fed92c11579c735f843d6c2e002c4fe29ce6588`.
- Alvo: Core 1.65.0, contrato administrativo 8.30.0. Mantidos slug/pasta `base-site-core-fator3`, basename `base-site-core-fator3/base-site-core-fator3.php`, namespaces, dados e contratos dos acompanhantes.
- Entrada de requisitos: `Fator3 Site Core(20261031-123104).md`, SHA-256 `a654c575bfb8d765c53f449a1816df37d7277837d6eb0b3be90df4bf523146e5`; pedidos 354, 360, 361 e planejamento revisão 3.
- Decisões preservadas: todas as visitas elegíveis, sem amostragem de 10%, sem retirar detalhe para atingir orçamento; Clarity independente do atraso publicitário. O teto de 20 ms não instrumentados foi retirado do aceite, mantendo-se a métrica diagnóstica.

As revisões 1–3 eram de planejamento. A revisão 4 registrou implementação recuperada, provas locais, desvios e impedimento de aprovação. A revisão 5 remove esse impedimento após a autorização do dono e registra somente os resultados efetivamente observados. A instalação de teste não encerra os aceites de campo nem implementa o desvio P2.

## 2. Convivência e encaminhamentos

| Pacote | Versão | Evidência desta retomada |
|---|---|---|
| Fator3 MCP | 0.38.0 | Ativo na bancada e no Site-Teste; transporte usado para instalação e ensaios remotos |
| Fator3 MCP Google | 0.24.0 | Ativo na bancada e no Site-Teste; sem envio comercial |
| Fator3 MCP Meta | 0.17.0 | Ativo na bancada e no Site-Teste; sem envio comercial |
| Fator3 MCP LinkedIn | 0.13.0 | Ativo na bancada e no Site-Teste; sem envio comercial |
| Fator3 MCP Pipedrive | 0.5.0 | Ativo no Site-Teste e incluído no comparativo com/sem; não ativado no PHP 8.3.6 local, pois exige 8.3.36 |

Não se identificou mudança de contrato que exigisse desenvolvimento de outro pacote. Não foram alterados acompanhantes nem gerados encaminhamentos apenas para anunciar versão. A convivência observada abrange inicialização, página/login, MCP, pós-atualização e o comparativo com/sem Core e Pipedrive. O pós-check Pipedrive confirmou a conta; isso não comprova entrega de contato. Não houve ensaio comercial dos SDKs nem aceites de outro responsável. O inventário final conserva os cinco acompanhantes ativos nas versões acima.

## 3. Mudanças por pedido e evidência

### 361 — executor e atualização urgente

O orçamento CLI passa a ser configurável entre 30 e 600 segundos, padrão 120, pela opção `f3base_cron_cli_segundos`. A configuração administrativa continua com validação de capacidade e revisão. O orçamento web/MCP permanece em 30 segundos. A restrição a três rotinas não interrompe a drenagem CLI; prioridade e antiguidade ordenam o trabalho, respeitando orçamento, checkpoint e recuos. Migração e pós-atualização são urgentes e ordenadas antes da manutenção.

A reserva acompanha o orçamento restante, com mínimo de 180 segundos. O limite HTTP se aplica dentro do trabalho do Core, sem bloquear chamadas posteriores de outro plugin. O resumo operacional acrescenta vencidas, maior atraso e motivos de parada, mantendo o limite de 4096 bytes e omissão explícita.

Provas refeitas: comando nativo WP-CLI 2.12.0, 15 tarefas sintéticas drenadas em uma passagem, ordem da mais antiga, orçamento de 600 segundos, reserva superior a 600 e ocorrência compartilhada executada uma vez com dois processos concorrentes. Nos ciclos locais, instalação e atualização confirmaram a migração na primeira passagem CLI. No Site-Teste, a atualização já estava confirmada antes da passagem natural CLI observada; não se atribui essa migração remota à CLI. Os callbacks sintéticos comprovam o executor; não comprovam entrega aos fornecedores ou funcionamento contínuo por 24 horas.

### 354 — CTA e catálogo público

O conteúdo final passa uma vez pelo parser de CTA; fragmentos fora desse fluxo conservam processamento próprio. A memoização é limitada e inclui configuração e superfície. Foram aprovadas 64 fixtures de equivalência e cenários adicionais de 30 níveis aninhados, conteúdo já processado, CTA acrescentado posteriormente e superfície de cabeçalho.

O diagnóstico de desempenho registra a primeira abertura indevida do catálogo completo, com hook/chamador/caminho relativo e sem argumentos. Na bancada de páginas estáveis: zero aberturas do catálogo, cinco consultas, nenhuma consulta de estrutura ou UPDATE, 55 classes, descoberta abaixo de 5 ms e tempo próprio abaixo de 100 ms. O comparativo remoto exigido pelo pedido passou nesta rodada, conforme a seção 4. O caso de fator3.com.br com 424 callbacks relatado pela frota permanece sem reprodução nesta entrega.

### Ativos, carga inicial, coleta e anúncios

O salvamento prepara a projeção pública em arquivo por SHA-256, com temporário, rename, hash e manifesto revisionado. Tokens de visita, nonces e campos privados não entram no arquivo compartilhado. A visita estável não compila nem gera esses ativos. O zelador recupera falhas; arquivos substituídos são conservados por 30 dias para HTML antigo em cache. Falta de arquivo/manifesto ou divergência de versão usa configuração atual e scripts completos como reserva.

O pacote traz 32 composições de consentimento, contexto, tempo ativo e carregadores de fornecedores. Um bootstrap pequeno inicia a observação efêmera e a classificação; os scripts principais usam `defer`. Os handles existentes e dados específicos da página são preservados. O cliente de contatos recebe sete grupos de destinos/conversões, retirando a cópia do catálogo comportamental e dos tokens de resumo sem retirar eventos.

Os controles por destino oferecem imediato, atraso fixo, interação ou prazo, ocioso ou prazo, de 0 a 30 segundos; referência em navegação, elegibilidade ou `load` legado. Conversão prioritária é optativa e falsa por padrão. GA4/Ads compartilham o download gtag com agendamentos por destino. A migração põe Clarity em imediato, preservando os demais destinos; consentimento, exclusões, revogação e marca de teste prevalecem.

Formulários emitem CSS com o primeiro formulário renderizado. A análise reutiliza a lista de campos, invalida por mutação e lê valores atuais. Nos testes com 100 entradas, as varreduras caíram de 103 para 3, mantendo idêntico o evento final de abandono, inclusive limpeza programática, novo campo e renomeação. Os tempos de 157,14 ms para a base e 58,57 ms para a candidata são uma amostra de CPU em jsdom; não estimam o resultado em celulares.

Os testes DOM preservaram deduplicação, correspondência antes do Lead, token, recibos, sequência e restrições de elegibilidade. A classificação começou cedo e sua requisição foi reutilizada. Retentativa de token, confirmação e recuo após segundo 403 passaram no fonte e no minificado.

### Desvios e metas não comprovadas

- **P2 parcial:** ofertas continuam carregadas com a análise, inclusive quando não há oferta inicial no HTML. A API síncrona e a observação de inserções dinâmicas foram preservadas. A divisão em um arquivo tardio não foi implementada: o comportamento atual evita uma nova janela de perda de abertura/fechamento. Não declarar atendido o critério “páginas sem recurso não o baixam” para ofertas.
- A separação adicional entre análise e funcionalidade de formulário não foi demonstrada como uma entrega independente. Houve cache de campos e CSS condicionado, sem claim de todo o redesenho P2.
- Metas de 3 KiB gzip síncronos e 20/30 KiB nos primeiros três segundos não estão integralmente comprovadas. O somatório conservador dos scripts síncronos do cabeçalho foi 3089 bytes (17 acima de 3 KiB). Todos os downloads JS próprios da fixture somaram 36798 bytes gzip; não foi medida a janela dos primeiros três segundos.
- Não houve HAR/CPU/CWV de navegador real, teste de campanhas, confirmação de replay remoto, ensaio de margem de conversão ou prova de invalidação de CDN. A redução local de bytes não estabelece causalidade sobre saída de visitantes ou LCP.

### Comparação com HTML novamente gerado

A evidência antiga de HTML foi substituída para este comparativo porque ainda continha a configuração completa repetida em `f3baseLeadsDados.medicao`. O código recuperado já usava a projeção reduzida. O novo teste confere suas sete chaves e usa dependências realmente referenciadas no HTML gerado por cada versão.

| Métrica da mesma fixture de artigo | 1.64.0 | 1.65.0 |
|---|---:|---:|
| HTML sem compressão | 37245 bytes | 33717 bytes |
| HTML gzip estimado | 8835 bytes | 9488 bytes |
| Downloads próprios de JS | 8 | 6 |
| JS externo próprio, soma gzip | 38172 bytes | 36798 bytes |
| JS próprio síncrono no cabeçalho, soma gzip | 26129 bytes | 3089 bytes |
| HTML + JS externo, soma gzip | 47007 bytes | 46286 bytes |

Redução total estimada: **721 bytes, aproximadamente 1,5%**. A melhora maior está na redução do código síncrono, não no volume total frio. Gzip foi calculado offline por arquivo, nível 9, `mtime=0`; o somatório inline não reproduz a compressão conjunta do documento. Não inclui SDKs remotos, headers de transporte ou cache real. Evidência: `evidence/1650/transfer-comparison.json`; reprodutor: `tests/asset-transfer-1650.py`.

## 4. Instalação, prontidão e provas

### Pacote e bancada

O instalador contém 897 arquivos, dos quais 591 PHP passaram no lint em PHP 8.3.6. O runtime do fonte foi comparado byte a byte com esse ZIP. Mínimos exercitados: WordPress 7.1.2 e PHP 8.3.6; matriz adicional WordPress 7.1.4 com o mesmo PHP. MySQL descartável e transporte/e-mail externos bloqueados.

| Prova refeita | Resultado | Evidência no fonte |
|---|---|---|
| Configuração, ativos, CTA e executor | 31 verificações aprovadas | `evidence/1650/request-1650.json` |
| Gates administrativos e fronteiras | 5 aprovadas | `evidence/1650/guards-1650.json` |
| Equivalência CTA | 64 aprovadas | `evidence/1650/request-360-cta.json` |
| Proteção cron/fallback | 9 aprovadas | `evidence/1650/request-360-cron.json` |
| Documentação por API nativa WordPress | 1910 verificações; 169 documentos, 721 páginas | `evidence/1650/docs-1650.json` |
| Coleta e elegibilidade, fonte/minificado | 76 aprovadas | `evidence/1650/dom-1650.json` |
| Atrasos, Clarity, gtag e revogação | 28 aprovadas | `evidence/1650/delays-1650.json` |
| HTML WordPress executado em jsdom | 19 aprovadas; seis dependências defer | `evidence/1650/html-runtime.json` |
| Detalhe de abandono e custo de campos | 3 aprovadas; 103 → 3 varreduras | `evidence/1650/form-performance.json` |
| Recibos e renovação de token | 26 aprovadas | `evidence/1650/request-332-dom.json` |
| WP-CLI real, drenagem e concorrência | 15 tarefas; ocorrência concorrente única | `evidence/1650/native-cli-1650.json` |
| Limpa, atualização 1.64, repetição, desinstalação/reinstalação | Aprovadas no WP 7.1.4 e no piso 7.1.2, com o ZIP exato | `evidence/1650/native-cycles-1650.json` e `evidence/1650-min/native-cycles-1650.json` |

Nos ciclos, a desinstalação suspende trabalho pendente conforme o contrato; a reinstalação preserva esse estado e os dados. A comparação é feita com o estado previsto após desinstalação, não com uma expectativa incorreta de manter tarefas executáveis após removê-lo.

As páginas estáveis do candidato ficaram em 7,176 / 8,457 / 7,367 ms próprios; login em 0,232 / 0,387 / 0,148 ms. Cinco consultas na página, zero no login; nenhuma escrita/estrutura; 55 e 11 classes, respectivamente. Catálogo completo fechado e descoberta dentro de 5 ms. Esses números são locais, com tema sintético e sem Yoast/Pipedrive ativos. Não substituem o site real. O profiler conserva uma requisição de preparação após configurar a fixture, fora do orçamento estável, seguida de aquecimento e três amostras por rota. Evidências em `performance-1650.json` e `*-profile.json`.

### Documentação instalada e canal remoto

O instalador inclui especificação, configuração, contratos, operação e recuperação, notas `docs/RELEASE-1.65.0.md`, guia `docs/AGENTES-1.65.0.md` e índice `docs/DOCUMENTACAO.md`. A prova local continua abrangendo os 169 documentos e as permissões pelas abilities nativas.

No Site-Teste atualizado, a operação `f3base/documentacao-ler` foi descoberta e seu schema lido. O índice retornou versão 1.65.0 e 169 documentos. Foram lidos integralmente seis documentos: RELEASE, AGENTES, CONFIGURACAO, DOCUMENTACAO, CONTRACTS e MEDICAO-EVENTOS-1.33. O último tem 305 linhas, recuperadas em duas páginas de 200 e 105 linhas, com versão/hash constantes e continuação encerrada. Todos os textos e hashes foram comparados com os arquivos do runtime exato. Caminho benigno fora da allowlist foi recusado com `documento_nao_catalogado`. Não se leu arquivo privado.

Evidências: `site-documentation-pages.json`, `site-documentation-verification.json` e `site-documentation-index.json`. O ensaio remoto não percorreu os 169 textos nem utilizou perfil remoto sem capacidade administrativa. A prova completa da matriz de permissões no painel/transporte remoto permanece pendente; as cinco verificações locais de gates não são apresentadas como esse ensaio remoto.

### Site-Teste: instalação e pós-atualização

Origem: `https://fator3-teste-mcp-1.dreamhosters.com/`. WordPress 7.1.4, PHP 8.3.36. Estado final consultado: **Core 1.65.0 ativo**, com os cinco acompanhantes da seção 2 ativos.

O bloqueio da revisão automática registrado na revisão 4 foi resolvido pela autorização explícita do usuário para o pacote e o destino apresentados. O envio anterior incompleto havia sido cancelado. Nesta rodada, um novo envio de 16 partes foi finalizado com 4156410 bytes e SHA-256 idêntico ao autorizado. A instalação validou o slug esperado, preservou a pré-imagem e substituiu 1.64.0 por 1.65.0, mantendo o plugin ativo. Operação `97335b7509aec573c0facca51f8ecd8a`; backup de arquivos `9a1ddc3f1560f2bb000b6e4d`. Evidência: `site-installation-authorized.json`.

O instalador informou reativação silenciosa e execução PHP nova, sem alegar ciclo completo do hook de ativação ou prontidão comercial. As sondagens antes/depois de `/` e `/wp-json/` passaram com HTTP 200 e bypass confirmado. Os primeiros tempos após instalação incluíram aquecimento e atualização; não entram no aceite de desempenho estável. A limpeza de cache foi solicitada ao provedor, sem prova de invalidação de CDN externa.

O resumo do Core confirmou atualização concluída, sem falha, em 31/10/2026 às 13:55:43 -03. Os pós-checks confirmaram cabeçalhos, navegação e conta Pipedrive. A recuperação está despausada (`core_operacional`); a leitura registrada não mostrou falhas/incertos nas sete filas monitoradas. Essa leitura é uma fotografia do estado, não um acompanhamento de 24 horas.

Foram comparadas por revisão/hash quatro configurações: comportamento, consentimento e llms ficaram idênticos. Em carregamento de destinos, a única chave preexistente alterada foi Clarity, pela migração prevista; foram acrescentadas as novas chaves de referência, conversão prioritária e controles GA4/Ads/GTM. A evidência guarda hashes e nomes, sem valores de credenciais. Não se afirma igualdade de todas as opções do site. Evidência: `site-config-preservation.json`.

### Passagem CLI real

A hospedagem registrou uma passagem natural CLI de 14:00:12 a 14:00:30 -03, run `500ca516-9733-4af4-a61d-ccd836053c23`. O pai terminou com `passagem_concluida`, consumiu 17966 ms de 120 segundos e registrou 18 trabalhos de manutenção, além da rotina de captação. Há 19 registros filhos: 15 com `lote_concluido` e quatro com `executado_sem_confirmacao` (manutenção, cache e e-mail). Estes quatro não são contados como confirmação de resultado do módulo.

Após essa passagem, o resumo registrou nove hooks vencidos, maior atraso de 293 segundos e nenhuma espera por causa. São métricas móveis de tarefas recorrentes; não representam uma fila zerada nem garantia de todos os efeitos externos. A migração já estava concluída antes desse run. Evidências: `site-authorized-cli.json` e `site-after-authorized-summary.json`.

### Desempenho remoto

O profiler próprio do Core foi executado com três amostras por rota:

| Métrica | Página | Login |
|---|---|---|
| Tempo próprio por amostra | 76,109 / 76,134 / 87,592 ms | 17,142 / 4,910 / 5,043 ms |
| Consultas próprias | 3 SELECT em cada amostra | 0 |
| Classes carregadas | 58 | 12 |
| Aberturas do catálogo completo | 0 | 0 |
| Escritas ou consultas de estrutura | 0 | 0 |
| Descoberta | 0,052 / 0,058 / 0,052 ms | Nenhuma chamada |

Todas as amostras ficaram abaixo de 100 ms próprios. O tempo próprio não é o tempo total da página. O profiler da página registrou quatro parseamentos de CTA e seis fragmentos memorizados no conteúdo real, sem abertura do catálogo completo. Evidências: `site-performance-pagina.json` e `site-performance-login.json`.

O comparativo do pedido 354 usou três amostras após aquecimento por rota e condição. Um componente MU temporário, restrito ao Site-Teste, às duas rotas, a chave de curta validade e à sonda assinada do MCP, retirou Core e Pipedrive apenas da lista de carregamento daquela requisição. Não houve desativação persistente. Um cabeçalho conferiu a presença/ausência efetiva dos dois arquivos principais. Todas as amostras tiveram HTTP 200 e PHP novo confirmado.

| Rota | Com Core + Pipedrive — 3 amostras | Sem ambos — 3 amostras | Diferença dos mínimos | Limite |
|---|---|---|---:|---:|
| Página | 398,523 / 375,878 / 390,762 ms | 316,278 / 328,381 / 322,019 ms | **59,600 ms** | ≤100 ms: passou |
| Login | 245,968 / 242,854 / 253,702 ms | 260,129 / 268,654 / 256,111 ms | **−13,257 ms** | ≤100 ms: passou |

Foi usada a duração de geração PHP exposta pela sonda, não o tempo de transporte HTTP. O resultado negativo no login é compatível com a variação das amostras e não demonstra aceleração causada pelos plugins. Este ensaio verifica o critério na condição atual do Site-Teste; não mede isoladamente causalidade de cada plugin, CWV ou todas as páginas de produção. Evidência: `site-with-without-core-pipedrive.json`; modelo sem chave: `tests/site-performance-1650.php`.

### Ativos públicos, navegador e limpeza

O manifesto público ficou vigente, sem erro e sem amostragem, no perfil 16. O arquivo de configuração de 3639 bytes foi servido com HTTP 200 e SHA-256 `00540d51c7775467850141dbef3e4ee72e4c7e3b84334b754ce7a6c4c6a61036`, igual ao manifesto. Essa sonda é interna à origem; não prova cache/CDN externo. Evidência: `site-public-assets.json`.

No Chrome, a página inicial carregou, exibiu conteúdo e dois formulários, e o FAQ respondeu à expansão com a resposta visível. A sessão já estava autenticada como administrador, condição excluída da coleta; portanto o teste não comprova os fornecedores de uma visita anônima elegível. Os scripts próprios observados usavam `defer`. Não apareceu erro de JavaScript do site na captura; houve uma mensagem de extensão do navegador. Nenhum formulário foi enviado. Evidência textual: `site-browser-smoke.json`.

O componente MU temporário foi apagado com confirmação e sondagens antes/depois aprovadas; backup da remoção `827f962ee3f5b5cfee62a4b0`. A inspeção final do caminho do ZIP temporário retornou arquivo inexistente após a instalação. Não há componente de comparação ativo nem ZIP de staging nesse caminho. As pré-imagens de recuperação gerenciadas pelo MCP permanecem disponíveis. `system/health` terminou saudável, com zero recuperação pendente. Evidências: `site-authorized-cleanup.json`, `site-authorized-health.json` e `site-authorized-final-versions.json`.

## 5. Banco, preservação e reversão

Sem novas tabelas ou colunas. A versão acrescenta preferência de orçamento CLI, manifesto/erro derivado dos ativos e marcador de atualização urgente. Contatos, filas, intenções e recibos não são apagados para migrar o executor. Os ciclos nativos verificaram preservação e repetição idempotente.

A pré-imagem de arquivos da instalação remota está identificada na seção 4. O instalador declara `database_effects_reversible:false`: restaurar esses arquivos não reverte automaticamente migrações ou efeitos de banco. Rollback de código para 1.64.0 conserva dados e volta aos limites/políticas anteriores. Não restaurar o banco apenas para reverter este incremento. Preservar a guarda externa à pasta do plugin e conferir intenções/recibos antes de reprocessar. Invalidar HTML de cache após atualização ou troca de configuração; os ativos antigos são conservados por 30 dias, mas isso não comprova purga de cache externo.

## 6. Pendências e responsáveis

| Pendência real | Responsável | Condição de conclusão |
|---|---|---|
| Matriz remota de perfis/permissões | Core + operador | Repetir recusa de dados/configuração com perfil sem capacidade administrativa no painel e no transporte remoto; gate local e allowlist remota já verificados |
| Convivência de campo e cache externo | Core + operação | Completar navegadores/SDKs reais e invalidar/conferir caches externos; inicialização, página/login e MCP passaram no Site-Teste |
| Ofertas condicionais e separação adicional P2 | Core | Implementar sem perda de eventos dinâmicos ou obter decisão explícita sobre o desvio; não encerrado nesta candidata |
| Bytes iniciais, HAR/CPU/CWV, saída em 0,5/1/3/5/10 s, BFCache e navegadores internos | Core + operador | Navegadores/dispositivos representativos, coleta integral, rede/caches reais e destinos de teste |
| Replay e fornecedores/campanhas | Operação de campanhas + Core | Confirmar início/cobertura e ausência de duplicação sem conversões sintéticas em campanhas reais |
| CTA/catálogo e tempo próprio em fator3.com.br/korvena.com.br | Frota + Core | Reproduzir páginas problemáticas e validar próprios ≤100 ms |
| Aceites 360 e 361 de campo | Frota | 24 h nos 12 sites após implantação autorizada; cron, filas, contatos e mapa nos prazos requeridos |

Encerrados nesta rodada: autorização, envio/instalação no Site-Teste, pós-atualização, passagem CLI observada, leitura documental selecionada, preservação das quatro configurações verificadas, desempenho próprio e comparativo com/sem. **Os pedidos 354/360/361 e a liberação para produção não estão encerrados**, devido às pendências acima. A entrega está `com-pendencias`, sem o bloqueio de instalação da revisão anterior.

## 7. Credenciais e efeitos externos

Nenhuma credencial de fornecedor foi solicitada, alterada ou incluída nos artefatos. O ensaio remoto usou uma chave temporária própria, omitida dos arquivos entregues, e o componente foi removido. Não foram enviados formulários ou comandos de campanha, criados contatos de teste, alterado GTM ou publicado código em repositório. O cron normal da hospedagem permaneceu operando as rotinas preexistentes; não se confunde essa operação com um ensaio de entrega comercial. Os testes locais usam destinos sintéticos e bloqueio de HTTP/e-mail. As evidências remotas contêm versões e diagnóstico técnico, sem valores de credenciais.

## 8. Arquivos finais e integridade

| Artefato | Bytes | SHA-256 |
|---|---:|---|
| `base-site-core-fator3-1.65.0-instalador.zip` | 4156410 | `f99d5cf933da2490baebe1d7fbe48d71a98d6b0ae00f51c0748267a471e8ed42` |
| `base-site-core-fator3-1.65.0-fonte.zip` | 7761359 | `d4a0393a6a5f49846f5d019eb3ed51b936c12bd23d1859b6f9a46bbea39109f9` |

O instalador é o único ZIP instalável, com raiz `base-site-core-fator3/`. O fonte tem raiz `base-site-core-fator3-1.65.0-fonte/`, runtime em `work/plugin/`, build, testes, fixtures seguras, insumos, planejamento e evidências. Não contém laboratórios prontos, bancos, node_modules, ZIPs aninhados ou pacotes acompanhantes. `source-manifest.json` lista hashes dos arquivos. A cópia interna deste relatório é marcada como anterior ao fechamento do fonte; o hash final do fonte fica apenas neste relatório externo, evitando circularidade.

Links canônicos dos artefatos:

- [base-site-core-fator3-1.65.0-fonte.zip](https://chatgpt.com/library?file_id=libfile_de3594659a488191a8f7c092e3491310&account_id=personal)
- [base-site-core-fator3-1.65.0-instalador.zip](https://chatgpt.com/library?file_id=libfile_a1dbfc6131708191826a5bd1101d6265&account_id=personal)
- [base-site-core-fator3-1.65.0-relatorio.md](https://chatgpt.com/library?file_id=libfile_8ecce6b58e048191a442279f88cc6046&account_id=personal)
- [base-site-core-fator3-1.65.0-notas-da-versao.md](https://chatgpt.com/library?file_id=libfile_d4d9fe71ae0881919895385739e21e78&account_id=personal)
- [base-site-core-fator3-1.65.0-guia-agentes.md](https://chatgpt.com/library?file_id=libfile_07db9a5185748191adfc5724850dbcfb&account_id=personal)

O relatório de recuperação permanece como registro histórico separado. As notas e o guia reproduzem a documentação instalada; este relatório prevalece para o estado de validação e as pendências de conclusão.
