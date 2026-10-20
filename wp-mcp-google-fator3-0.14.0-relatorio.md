# Relatório de entrega — Fator3 MCP Google 0.14.0

20/10/2026 · Base direta Google 0.13.0 · Pedidos MCP Google 28 e 29.
Identidade preservada: `wp-mcp-google-fator3/wp-mcp-google-fator3.php`; provider `wp-mcp-google-fator3`.

## Resultado

Implementados adaptadores GA4/Ads para o contrato `site-conversion-delivery/1.0.0`, configuração e segredo por conexão, verificação explícita, prontidão revogável, preservação da identidade GA4 e confirmação individual Ads. Integração efetiva com os dois executores Core 1.40.0 e seu diário; fila e deduplicação continuam Core. Contexto de transporte 1.1.0 negociado, leitor anterior 1.0.0 preservado. O pacote recebido do Core foi revisto e incorporado sem aguardar retorno.

Cron distingue lacuna de observação, resultado desconhecido e trabalho devido. Causas são registradas quando observadas; status não repara estado. Próxima passagem só encerra lacuna mediante prova de metadados/sequência estáveis e ausência de vencimento em todo o intervalo. Interrupção antiga sem prova continua explicitamente desconhecida.

Catálogo: 286 habilidades (111 leitura, 175 escrita), 36 opções; configuração 4.0.0. Mínimos WordPress 7.1.2/PHP 8.3.6. Nenhuma alteração dos plugins acompanhantes.

## Validação efetivamente executada

**833 verificações aprovadas: 773 em WordPress nativo e 60 puras. Zero falhas na matriz final.** Sintaxe validada em 154 arquivos PHP de runtime; inventário instalador com 158 arquivos. O catálogo, documentos compilados e links locais foram conferidos. Prova vinculada: `evidence/014/validation014.json`.

| Grupo | Percurso | Verificações |
|---|---|---:|
| clean | clean / mcp-first | 291 |
| upgrade | upgrade / mcp-first | 309 |
| google-first | clean / google-first | 79 |
| isolated | clean / google-only | 42 |
| core139 | clean / mcp-first | 52 |
| Contratos puros | ausência, método ausente, matriz e regressão de resposta | 60 |

WordPress 7.1.2, PHP 8.3.6, MySQL isolado, servidor PHP CLI com quatro workers e HTTP MCP reais. Core 1.40.0 na integração principal; 1.39.0 no leitor compatível. MCP 0.24.0; Meta/LinkedIn 0.3.0 usados como sentinelas no upgrade. Respostas Google simuladas; rede externa bloqueada na bancada. Os processos de laboratório foram encerrados e os inventários instalados conferidos.

A atualização usa 0.13.0→0.14.0 por upload MCP autenticado, verifica configuração/segredos cifrados/conexões/registros preservados, rollback real de arquivos, recusa de destino editado e reaplicação do mesmo candidato. Isolamento sem acompanhantes e ambas as ordens de ativação foram executados.

Casos de conversão incluem revisão vencida, segredo/fluxo divergentes, declaração de elegibilidade Ads, troca de perfil, revogação, múltiplas conexões, isolamento de segredo, timeout, resposta parcial/ambígua e resposta individual. Diário Core real registra entregue/incerto e não repete os registros. O ensaio de cron inclui saída antecipada de processo, fatal PHP, limite real de CPU e SIGKILL, além de inserção+remoção entre fotografias e recusa de apagar uma lacuna com base apenas na fila vazia atual. A idade de uma passagem é avançada em fixture; isso não equivale a acompanhar três dias reais.

A ajuda instalada foi percorrida integralmente e paginada via MCP em processos HTTP novos, com hash e tamanho por documento, incluindo o catálogo longo. Interfaces administrativas tiveram HTML/nonce/ausência de segredo verificados; não houve validação visual de navegador.

As rodadas de desenvolvimento encontraram e corrigiram carregamento de classes, adaptação ao executor Core fora de um hook específico e leitura física por conexão. Uma rodada também registrou divergência na reaplicação após rollback; a verificação passou a conferir integralmente a árvore da base antes da reaplicação. A causa dessa divergência não foi determinada; a matriz final usa novo laboratório e exige a comparação integral antes da reaplicação. As rodadas anteriores não entram na contagem final. Os 15 testes recebidos no patch Core e os 585 históricos da 0.13.0 também não entram. O gate específico não representa execução integral do PHPUnit nem do gate histórico `tools/validate.py`/`build/build.py verify`.

## Site-Teste

Google atualizado de 0.13.0 para 0.14.0 no Site-Teste com o instalador validado. Sondas autenticadas do pacote comprovaram home e REST anônimos com HTTP 200 antes/depois e ativação em requisição PHP nova. Estado Google: storage.ready=true, 286 habilidades; três rotas novas disponíveis. As 34 opções públicas preexistentes mantiveram seus estados; o catálogo passou a 36 opções. Os demais plugins preservaram versão e ativação. Core permaneceu 1.39.0. Conversões continuam desabilitadas/não verificadas; nenhuma credencial ou envio comercial foi configurado. A leitura de transporte 1.1.0 responde core_unsupported nesse Core; o leitor anterior permanece. O cron mostra no_due_work atual, interval_proven=false e uma lacuna histórica anterior sem fotografia inicial; a lacuna foi preservada, não apagada como se houvesse prova. Índice com 20 documentos e quatro documentos atuais completos foram lidos pelo MCP e comparados aos hashes locais.

Instalação: requisição `99b37a730f0dd608638a0823`, operação `ebbdd08fab7065c1ac47913f27241e40`, backup `67a8867d0102db5a7d1b0261`. Google observado depois: 0.14.0; Core observado: 1.39.0. A configuração pública preexistente foi comparada antes/depois; versões e ativação dos demais plugins preservadas. Detalhes e requisições em `evidence/014/summary.json` e arquivos associados. Redações do conector sobre campos sensíveis não constituem prova de valores secretos; a preservação de ciphertext foi exercitada no upgrade nativo.

## Limites e continuidade

GA4 `entregue` significa recebimento HTTP e mantém `processed:null`; não prova processamento nem atribuição. A prontidão Ads combina leitura da ação e declaração administrativa de upload elegível; não valida um recibo remoto. Sem credenciais/configuração/prova, os adaptadores ficam indisponíveis. Data Manager não foi introduzido sem evidência de necessidade; não existe fallback automático de transporte.

Permanecem pendentes credenciais e acessos comerciais, Android WebView/GA4 na sessão original, conversão Ads real, ausência de duplicação no navegador e observação de três dias nos 12 sites. Também não são reivindicados PHP-FPM, multisite/CDN ou o aceite de produção do pedido 20. O instalador não habilita envios automaticamente.

Há um único encaminhamento ativo ao Core, `wp-mcp-google-fator3-0.14.0-impacto-base-site-core-fator3.md` r2. Não há nova mudança de código Core exigida; restam configuração autorizada e homologação. Não houve publicação GitHub, instalação Core remota nem mensagem externa a destinatário não identificado.

## Artefatos e hashes

- Instalador: `wp-mcp-google-fator3-0.14.0-instalador.zip` · 742208 bytes · SHA-256 `7b9681bed81fa265ac70379fd6ebb5d4b161923a8e10a7a4ad115af58cf3d001`.
- Fonte: `wp-mcp-google-fator3-0.14.0-fonte.zip` · 3060947 bytes · SHA-256 `05af95023adf13b27fedc556c2759df7a28197a848a48c5cc4135e85bd1836bb`.
- Este é o relatório externo final; o exemplar dentro do fonte antecede seu fechamento e não se auto-referencia por hash. O fonte contém runtime idêntico ao instalador, documentos editáveis, build, testes e provas. Não contém instalador ZIP aninhado. Os ZIPs fechados não devem ser regenerados sem nova identidade e validação.

Base Google 0.13.0 instalador SHA-256 `d026247e0b25f184c3699e0fff7ee6bae8f49c8a2e63859a40bef529cc7f2297`. Core 1.40.0 recebido: instalador `d3bc062730e71520662282f969f32ded12065762301406f9a61a3601a98736fb`, fonte `ef6c3fb7d39ca0556c963fdb1ac2d2c6706d5addf4d48532462aabea75ea2517`. Manifesto completo de dependências: `evidence/014/inputs.json`; inclui o hash observado do runtime PHP utilizado nesta rodada, sem reutilizar sua identidade histórica.
