# Entrega — Fator3 Site Core 1.65.1

31/10/2026 · correção do mesmo ciclo · base 1.65.0 · contrato administrativo 8.30.0. Horários de campo abaixo em UTC−03.

**A 1.65.1 está implementada, empacotada e ativa no Site-Teste.** Esta correção entrega a separação de módulos P2, o estado incremental de formulário, os complementos 354(h–j) e a ordem de publicação do 362. O 362 passou na troca real de versão. O 354 foi implementado e testado, mas seu aceite em fator3.com.br permanece aberto porque esse site não foi medido nesta execução. A entrega continua **com pendências de campo e de comprovação dos orçamentos de front-end**; não equivale à conclusão de todos os aceites da frota.

## 1. O que estava faltando e por quê

Na 1.65.0, as ofertas ainda acompanhavam a análise mesmo sem oferta na página, e a análise específica de formulário não tinha sido entregue como módulo separado. A justificativa registrada era evitar perda de eventos na janela de carregamento dinâmico. Isso foi uma decisão técnica de adiar implementação, sem autorização para reduzir o escopo; não havia impedimento de credencial ou fornecedor para resolver essa parte. A regra do dono de implementar tudo foi aplicada nesta correção: a janela de carga recebeu captura e reconciliação de eventos, em vez de permanecer como desvio P2.

P2 significa **carregar o código específico de cada recurso quando esse recurso existe**. O coletor comum mantém transporte, recibos e uma ponte para os primeiros eventos; formulário e oferta têm seus módulos específicos. A separação funcional foi concluída. Ela não comprova, por si só, diminuição do total de bytes nem aprovação de todos os testes de produção.

| Frente | Entrega desta correção | Situação |
|---|---|---|
| P2 — presença de formulário/oferta | Módulos separados; seleção PHP; quatro composições prontas; carga dinâmica deduplicada; captura antes da carga | Implementada e aprovada nos cenários descritos abaixo |
| P3 — custo do formulário | Atualização do campo lógico alterado; observador compartilhado; reconciliação final para autofill/alterações programáticas | Implementada; ganho no ensaio de digitação, com custo inicial maior registrado |
| 354(h) — profundidade | Contagem real em pre_render_block/render_block, incluindo chamadas internas de do_blocks | Implementada; profundidade equilibrada e HTML aprovado |
| 354(i) — cache entre requisições | Chave por conteúdo/revisão/superfície; expiração de até 1 h; invalidação por conteúdo e contato | Implementada; cache frio/quente e invalidação aprovados |
| 354(j) — diagnóstico | Raízes/cabeçalhos e bytes de entrada/hash/parser/saída por fase | Implementada e observada no Site-Teste |
| 354 — até 100 ms em fator3.com.br | Depende de três amostras nesse domínio | Não comprovado nesta execução |
| 362 — primeira cópia com ativos | Manifesto vigente antes da confirmação/prova; reserva inline impedida de entrar no cache durante a troca | Aprovado na atualização real do Site-Teste |
| Metas de 3 KiB e 20/30 KiB | Permanecem como metas do plano; não atendidas/comprovadas integralmente | Em aberto; não convertidas em opcionais |

## 2. Base, compatibilidade e alterações

Base imutável: instalador 1.65.0 com SHA-256 `f99d5cf933da2490baebe1d7fbe48d71a98d6b0ae00f51c0748267a471e8ed42`. Mantidos slug `base-site-core-fator3`, basename, namespaces, opções do usuário e contratos comerciais. Não houve alteração exigida em outro pacote; não se emitiu documento de impacto sem ação técnica para um acompanhante. O contrato administrativo permanece 8.30.0.

### P2 e formulário

- `f3base-analise.js` conserva coleta comum, transporte, recibos e a ponte. Os novos `f3base-formulario-analise.js` e `f3base-ofertas-modulo.js` contêm a análise específica de cada recurso.
- O PHP declara a presença durante a renderização e seleciona `analise-0`, `analise-1`, `analise-2` ou `analise-3`: nenhum recurso específico, formulário, oferta ou ambos. Os arquivos já estão compilados; presença conhecida não cria uma cadeia adicional de downloads. O modo de depuração conserva fontes independentes.
- Recursos inseridos depois são detectados por DOM/eventos delegados. A carga é única, com repetição limitada em falha. A API síncrona de ofertas preserva contexto, instâncias e frequência antes da chegada do módulo. O arquivo legado continua disponível para HTML antigo em cache.
- A ponte preserva ordem, horário e identidade de eventos técnicos, inclusive foco/input e abertura/fechamento antes da carga. Saída antes do download é reconciliada antes do flush do coletor; carga tardia não duplica o evento. Revogação elimina observações pendentes. Valores digitados e nomes de arquivos não são copiados para a análise.
- O JavaScript funcional do formulário permanece independente e condicionado à renderização. A análise usa um IntersectionObserver compartilhado e atualiza apenas o campo lógico alterado; mudanças no DOM invalidam associações e o encerramento reconcilia valores atuais. Formulário removido do DOM conserva a posição técnica necessária ao abandono. Não foi adicionada amostragem de visitas.

### 354(h–j)

`F3Base_Servicos` aumenta a profundidade no último pre_render_block somente quando o bloco não foi substituído por outro filtro, e a diminui em render_block. Um do_blocks interno não reinicia essa profundidade. O carimbo fica na raiz efetiva e no template-part do cabeçalho; o conteúdo recebe sua passada final em the_content. A definição de raiz deixou de depender de pai nulo.

O resultado de the_content é reaproveitado entre requisições públicas anônimas por cache de objeto persistente ou transiente. A chave combina versão do algoritmo/plugin, SHA-256 do conteúdo, revisão de f3base_contato, superfície/configuração e geração de invalidação. TTL de 3600 s; save_post e adição/alteração/remoção do contato trocam a geração. Entradas antigas expiram sem varredura ilimitada. Conteúdo autenticado, administrativo, preview, protegido por senha ou maior que 1 MiB não é persistido; erro do parser também não é persistido.

O estado interno `f3base_cta_cache` e a família de transientes `f3base_cta_<sha256>` foram declarados no inventário. Não há nova tabela ou coluna. A primeira visita elegível após invalidação pode gravar o transiente; as amostras aquecidas abaixo só o leram. A memória da requisição mantém os limites de 128 entradas/2 MiB.

### 362

A migração prepara e verifica os arquivos e o manifesto públicos antes de o executor confirmar o ciclo. O recibo registra o hash e o horário do manifesto. A prova pós-atualização também exige o manifesto vigente antes de gerar a cópia de cache. Falha de publicação, trava ou revisão concorrente mantém o ciclo pendente; não confirma uma publicação inexistente.

Uma visita concorrente pode conservar a reserva inline, mas recebe DONOTCACHEPAGE enquanto o manifesto não estiver vigente, impedindo o WP Super Cache de congelar essa reserva. A visita não compila arquivos. Os ativos imutáveis antigos permanecem disponíveis pela política existente de 30 dias.

## 3. Pacote e provas locais

O instalador final contém 907 arquivos. Todos os 591 arquivos PHP passaram no lint em PHP 8.3.6. Instalação limpa, atualização direta 1.65.0 → 1.65.1, repetição idempotente, preservação de dados e desinstalação/reinstalação passaram em **WordPress 7.1.4 e 7.1.2**, usando o instalador final. A primeira passagem nativa do WP-CLI confirmou o ciclo; a finalização posterior foi idempotente.

| Prova | Resultado | Evidência em `evidence/1651/` |
|---|---|---|
| P2, fontes/minificados e quatro composições | 44 verificações aprovadas | `p2-dom.json` |
| Formulário com HTML gerado pelo WordPress | 44 verificações aprovadas | `request-317-dom.json` |
| Contratos/persistência do pedido 317 | 29 verificações aprovadas | `request-317.json` |
| Regressão de executor, ativos e configuração | 31 verificações aprovadas | `request-1651.json` |
| Paridade de HTML de CTA | 64 comparações aprovadas | `request-360-cta.json` |
| Profundidade, do_blocks aninhado e cabeçalho | 6 verificações aprovadas; caso com 420 links faz um parse | `request-354-depth.json` |
| Cache de conteúdo frio/quente e invalidação | 3 + 7 verificações aprovadas | `request-354-cold.json`, `request-354-warm.json` |
| Ordem de publicação/confirmação e reserva não cacheável | 10 verificações aprovadas | `request-362.json` |
| Documentação, índice, leitura completa e hashes | 1918 verificações aprovadas | `docs-1651.json` |
| Instalação/atualização nos dois WordPress | Aprovadas com o mesmo SHA do instalador | `native-cycles-1651.json`, `minimum/native-cycles-1651.json` |

As 64 comparações verificam o HTML de saída do carimbo de CTA, não identidade byte a byte de toda a página entre versões: URLs de ativos e composição de scripts mudam nesta versão. Provedores de bancada são simulados; esse resultado não prova entrega comercial ou replay em uma plataforma externa.

### Navegador real

Chrome 155/Linux, janela 1363×936 e cenário interno 390×844, sem limitação artificial de CPU/rede. Foram 120 execuções alternadas, 20 por combinação de versão e cenário: página sem recursos, formulário inicial e recursos dinâmicos com carga retardada. **A candidata passou em 60/60**. A base passou em 40/60 e falhou nos 20 casos de oferta aberta/fechada no mesmo ciclo de execução antes da varredura do observador. Os coletores eram simulados, sem conversão comercial.

| Medição do cenário com formulário | 1.65.0 | 1.65.1 |
|---|---:|---:|
| Inicialização, p50 | 0,8 ms | 1,7 ms |
| Inicialização, p95 | 1,3 ms | 3,0 ms |
| Lote de 100 inputs, p50 | 12,7 ms | 3,5 ms |
| Lote de 100 inputs, p95 | 17,9 ms | 6,5 ms |

Houve menos trabalho durante digitação, mas maior custo inicial nesse cenário. Esses tempos são do ensaio, não INP/CWV de campo. Evidência: `browser-120.json`, com amostras e hash da fixture.

Um ensaio separado usou navegação real de ida/volta: **duas restaurações por BFCache**, pageshow.persisted verdadeiro, uma página, um início e um fechamento de formulário, sem duplicação nem valores de campos no payload. Evidência: `bfcache-real.json`. Os eventos pagehide/pageshow do ensaio de 120 casos eram sintéticos e não foram usados como prova de BFCache real.

### Bytes e limites do resultado

Gzip local nível 9, não transferência medida em rede: coletor comum/perfil sem recurso específico **6815 B**; perfil com formulário **7786 B**; perfil com oferta **7447 B**; ambos **8398 B**. Módulos avulsos de formulário e oferta: 2030 e 1348 B. O perfil público 16 observado no Site-Teste tem 20674 B gzip, sem contar configuração, análise, bibliotecas locais ou outros ativos.

O antigo par análise + ofertas somava 6630 B gzip local; o novo perfil sem recurso específico tem 185 B a mais. A ponte necessária para preservar eventos tem custo. Portanto, separar módulos **não autoriza declarar redução total de bytes**. Não foi comprovada a janela de downloads dos primeiros três segundos, nem o cumprimento integral de 3 KiB síncronos/20 KiB sem formulário/30 KiB com formulário. O inventário completo está em `assets.json`; essas metas continuam abertas.

## 4. Instalação real no Site-Teste

Domínio: `fator3-teste-mcp-1.dreamhosters.com`. Operação de instalação `594b48e251f1548054f648c989144e60`; backup `702bef685a959cde32149d2b`. Versão anterior 1.65.0, versão final ativa 1.65.1. Instalador usado: exatamente o hash da seção 7.

As revisões e todos os hashes de campos das configurações f3base_contato, f3base_formularios, f3base_carregamento_destinos e f3base_pipedrive permaneceram iguais antes/depois. Não se reproduziram valores de configuração no relatório. A documentação RELEASE-1.65.1 foi lida integralmente pela ability instalada; SHA-256 `d1143012e69df4fc42cc98042b67a316bd4104abc237b6b219967570bb7ca47c`.

### 362 — primeira cópia após a troca

| Evidência do ciclo `c0086d80-021e-4974-9966-fc540e5a6411` | Horário/resultado |
|---|---|
| Manifesto 1.65.1 gerado | 15:37:10 · epoch 1793471830 |
| Confirmação no executor | 15:37:10 · epoch 1793471830 |
| Primeiro buffer da home entregue ao WP Super Cache | 15:37:11 · epoch 1793471831; já referencia `wp-content/f3base-publico/` |
| Artefato cacheado servido | mtime 1793471831; corpo coincide com artefato e permanece estável; HTTP 200 |
| Prova de cabeçalhos | 15:37:16 · verificado |
| Navegação | 15:37:17 · observada |
| Conta Pipedrive | 15:37:26 · verificada; isso não é prova de entrega de lead |

Manifesto/configuração: `00540d51c7775467850141dbef3e4ee72e4c7e3b84334b754ce7a6c4c6a61036`. O observador temporário gravou o primeiro buffer uma única vez, antes da escrita final do WP Super Cache. Buffer: 142497 B, SHA-256 `a15a060cabd790e97fce732ebb5bd843e6404830c9e3b6b1310792d1b0769a98`. Cópia final servida: 142570 B, SHA-256 `4c8a5c28f1f7e132eed2e013bbe0892053dee375abe944173e53f688e8d0e01b`; a diferença inclui o rodapé acrescentado pelo cache. A sonda confirmou a cópia final, não igualdade entre esses dois hashes.

A conferência final, após a limpeza, continuou servindo esse mesmo artefato com a referência pública. A sonda é interna ao mesmo domínio; não comprova comportamento de todos os caches/CDNs externos. Evidências: `site-first-cache.json`, `site-cache-served.json`, `site-final-cache.json`, `site-assets-current.json` e `site-summary-current.json`.

### 354 — desempenho observado

Todas as leituras abaixo são da ability f3base/desempenho-ler na **1.65.1 do Site-Teste**, escopo callbacks e carga próprios do Core. Não representam TTFB total nem uma medição de fator3.com.br.

| Série | Amostra 1 | Amostra 2 | Amostra 3 | Interpretação |
|---|---:|---:|---:|---|
| Página, primeira série | 76,277 ms | 83,063 ms | **129,983 ms** | A terceira excedeu 100 ms; evidência preservada |
| Página, repetição sequencial após conclusão da atualização | 84,817 ms | 80,794 ms | 72,465 ms | Três resultados abaixo de 100 ms no Site-Teste |
| Login | 9,372 ms | 9,392 ms | 9,474 ms | Três resultados abaixo de 50 ms |

Na primeira série, a terceira amostra registrou 41,102 ms na carga de F3Base_Modulo_Endpoint_Leads e 18,839 ms no callback do conteúdo já cacheado; o carimbo de blocos ficou em 21,111 ms. Isso localiza o aumento registrado, mas não determina sua causa no servidor. A segunda série não apaga a primeira nem garante ausência de variação futura.

Em todas as seis amostras de página: **4 SELECTs, nenhuma consulta de estrutura/UPDATE, 58 classes, zero aberturas do catálogo completo**. No login: zero consultas, 12 classes e zero aberturas. O conteúdo teve um acerto persistente e zero parseamentos por amostra. O carimbo de blocos registrou 109 callbacks, 27 raízes no contador, seis parseamentos e profundidade final zero. Na série sequencial, seu tempo próprio foi 20,976/25,852/21,327 ms; o callback the_content, 0,544/0,648/2,091 ms.

Diagnóstico por fase na página: render_block recebeu 66811 B, calculou hash sobre 66401 B e passou 30998 B ao parser; the_content recebeu 9887 B e devolveu 9985 B do cache, sem parse. Os contadores medem trabalho das fases, não bytes de rede; 27 raízes não significam 27 execuções do parser.

Os números recebidos do dono para fator3.com.br na 1.65.0 — 182,4/157,7/166,2 ms — são evidência de entrada. Não foi feita medição da 1.65.1 nesse domínio: os conectores disponíveis nesta execução não incluem fator3.com.br. O requisito de três resultados próprios ≤100 ms nesse site **permanece sem aceite**. Também não se repetiu nesta correção o comparativo com/sem Core e Pipedrive da 1.65.0.

### Limpeza e estado final

Removidos, com backup gerenciado e conferência de hash, os dois HTMLs de ensaio, o observador temporário de primeiro cache, seu recibo no servidor e o ZIP temporário de transferência. As cópias de evidência estão no fonte. A remoção do observador foi acompanhada por sondas antes/depois. A leitura final confirmou Core 1.65.1 ativo, saúde positiva e zero recuperações pendentes. Os caminhos do observador e do ZIP foram conferidos como ausentes. Não houve remoção de dados de usuário para realizar a atualização.

## 5. O que falta para encerrar tudo

| Pendência | Por que não está concluída | Evidência necessária |
|---|---|---|
| 354 em fator3.com.br | Não há acesso a esse domínio entre os conectores desta execução | Instalar a candidata no fluxo da frota e obter três amostras próprias ≤100 ms; conferir HTML e contadores |
| Comportamento em korvena.com.br e demais páginas afetadas | Não foram atualizadas/medidas nesta rodada; Site-Teste não representa essas páginas | Regressão nas páginas reais, com estado de cache documentado |
| Orçamentos de bytes e carga inicial | O código foi separado, mas há custo da ponte e os limites não foram comprovados | Medir janela de 3 s em artigo e campanha com formulário; otimizar o que exceder sem retirar coleta |
| HAR/CPU/CWV e saídas em 0,5/1/3/5/10 s | Ensaios atuais usam ambiente controlado; não abrangem dispositivos/redes representativos | Comparação de campo com cache frio/quente e destinos de teste |
| SDKs, replay, tags de campanha e navegadores internos | Coletores simulados não comprovam fornecedores externos; não foram alteradas campanhas | Início/cobertura/duplicação e retornos em navegadores reais autorizados |
| Matriz remota de permissões | A conexão usada é administrativa; verificações locais de gates não substituem contas remotas restritas | Recusas no painel e transporte com perfil sem capacidade administrativa |
| Aceites 360/361 de frota | A janela real de 24 h e as implantações nos 12 sites não ocorreram nesta execução | Cron/filas por 24 h, lead de teste nos destinos definidos, mapa no prazo e retirada de conteúdo não público |

Essas pendências não foram reclassificadas como opcionais. O trabalho de implementação de P2 e dos complementos 354/362 está entregue; a conclusão operacional depende das provas acima. Não houve disparo de mensagens a terceiros, alteração de campanhas ou envio sintético de conversões comerciais nesta correção.

## 6. Banco e reversão

Não há novo schema SQL. O cache de CTA é derivado e reconstruível; opções de usuário e registros existentes foram preservados. Reverter arquivos para 1.65.0 preserva dados, mas devolve o comportamento anterior de módulos e de confirmação/publicação. O backup de instalação permite restaurar arquivos; não desfaz efeitos de banco nem ações externas. Não restaurar o banco apenas para reverter código e não apagar filas/contatos para obter um estado limpo.

## 7. Arquivos finais e integridade

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| `base-site-core-fator3-1.65.1-instalador.zip` | 4206718 | `059d7da03484eb3d9eb7327f49787144466f451fcf51730ea0357d92c03f168a` |
| `base-site-core-fator3-1.65.1-fonte.zip` | 8035411 | `279b11eea6e273a0a42c93434fd44b3b6b75a21745139b30581672358eadadf5` |

Terceiro arquivo: `base-site-core-fator3-1.65.1-relatorio.md` (este documento). O fonte contém runtime, fontes de build, testes, entradas recebidas e evidências; o fechamento compara cada um dos 907 arquivos de runtime com o instalador. Não inclui dependências instaladas, laboratórios, dumps ou ZIPs de acompanhantes. O manifesto interno registra hashes por arquivo. A cópia deste relatório dentro do fonte é anterior ao cálculo do hash do próprio ZIP; este relatório externo é o canônico.

Os pacotes 1.65.0 anteriores permanecem como histórico. Esta correção não os substitui nem transforma suas provas em testes da 1.65.1. As evidências novas ficam em `evidence/1651/`; evidências de versões anteriores conservam a identificação de origem.
