# Entrega — Fator3 MCP 0.24.0

Revisão 1 · Data/hora: 2026-10-17T09:17:32-03:00 · Rodada: implementação e homologação do Pedido MCP 61.
Slug/basename: `wp-mcp-fator3` / `wp-mcp-fator3/wp-mcp-fator3.php`.
Status: **com-pendencias — implementada, ativa no Site-Teste e apta no escopo testado**. Pedido 61 aprovado no ambiente solicitado. Pendências externas e mínimo PHP não ensaiado estão na seção 6.

## 1. De onde esta versão entra

Instalação nova ou atualização direta **0.23.0 → 0.24.0**, sem intermediária. A base é a entrega final anterior: instalador 818313 bytes, SHA-256 `6a64708f5737eb08c6f726dd5941b28d36a28ecbb45f79f32d2c96d00030a4ab`; fonte 2801809 bytes, SHA-256 `7594fa0dff260a0664281c321521cb6017598cad4fceb7ca3d1ed772ef5ad1ff`. Ambos foram conferidos antes de alterar o candidato.

Lidos integralmente: `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, **revisão 4, 16/10/2026**. Cópias revisão 3 encontradas estão superadas. Pedido vigente: `Fator3 MCP(1).md`, situação 16/10/2026; os pedidos 1–60 não foram reabertos. Planejamento registrado antes da alteração em `docs/PLANO-0240.md`.

Laboratório: **WordPress 7.1.2 / PHP 8.3.6 / MySQL 8.0.46**, com instalação limpa nativa e atualização em HTTP MCP. Core WordPress obtido de `https://wordpress.org/wordpress-7.1.2.zip`; identidade em `evidencias/0240/inputs.json`. Cabeçalho conserva os mínimos herdados WP 7.1.2/PHP 8.3; **PHP 8.3.0 não foi executado**, portanto não é suporte comprovado por esta rodada. Site-Teste: WP 7.1.3/PHP 8.3.30.

## 2. Convivência e encaminhamentos

Core **1.35.0**, Google **0.11.0**, Meta **0.2.0** e LinkedIn **0.2.0** foram ativados no laboratório e permaneceram nas mesmas versões no Site-Teste. Core/Google reais foram exercitados nas regressões de diagnósticos e conflito de revisão; os sociais tiveram presença/bootstrap, sem chamadas a suas APIs. Nenhum acompanhante foi alterado.

A correção afeta a projeção das sondas de manutenção WordPress. Não altera contratos, schemas, credenciais, configuração ou regras de domínio dos acompanhantes, nem exige mudança de código neles. **Não foram gerados impactos individuais de simples aviso de versão.** O risco operacional para a frota está descrito no próprio Pedido 61 e nesta entrega. Implantador atual não fornecido nesta rodada: não avaliado; não foi introduzida dependência dele.

O impacto recebido `wp-mcp-google-fator3-0.11.0-impacto-wp-mcp-fator3.md`, revisão 2, encerra M91-01/M91-02 no recorte testado pelo mantenedor Google. Foi lido do fonte recebido e preservado em `docs/entradas`; não traz nova mudança solicitada ao MCP. Seus testes não foram contados como provas próprias. Contratos `server-integration/1.0.0`, `executor-registration/1.0.0`, `package-distribution/1.0.0`, política 1 e resultados 2 permanecem.

## 3. Mudanças e evidência

| Pedido exato | Problema | Implementação | Resultado |
|---|---|---|---|
| **Pedidos MCP 61** | `cache_bypass_verified` era classificado como sensível pelo trecho `pass` de `bypass`, retornando `[redigido]` na 0.23.0. | Exceção pelo nome exato, limitada a `is_bool`, em `SafeOutput::error()` de `includes/Release014.php`. A projeção recursiva atende amostras, totais, probe_before/probe_after, respostas de sucesso e falha. | true/false preservados; tipos string, inteiro, null, array e objeto continuam redigidos. Aceite real de plugins/upload aprovado no Site-Teste. |
| Documentação da release | Agente precisa interpretar a prova de bypass e a resposta da própria atualização. | Manual 0.24.0, atualização direta, notas da release, exemplo e semântica de true/false incluídos no leitor instalado. | 17 documentos completos, hash/revisão e paginação; cursor da 0.23.0 recusado após a troca. |

Somente **quatro arquivos do instalador** mudaram: `wp-mcp-fator3.php` (versão), `includes/Release014.php` (exceção booleana), `includes/guide-content.php` e `includes/guide-documents.php` (documentação compilada). Os outros **452 arquivos são idênticos** à base. O produtor `Probe`, `Recovery`, autenticação e `DataSafety.php` de SQL/options permanecem byte a byte iguais. Não há coerção de false, alteração da expressão geral de segredos ou abertura do contêiner `credential`.

`true` comprova o marcador PHP assinado na sonda interna; `false` registra ausência dessa prova. Nenhum dos dois certifica acesso público externo, cache HIT ou prontidão comercial. A resposta da requisição que substitui a 0.23.0 ainda pode usar a projeção antiga carregada. Em nova requisição, `plugins/operation-status` recuperou os booleanos do diário bruto, e as novas sondas conservaram os valores. Registros eventualmente já redigidos não são reconstruídos por inferência.

## 4. Instalação e prova da troca

| Evidência própria | Cenário e resultado | Limite |
|---|---|---|
| `projection-base.json` / `projection.json` | Defeito reproduzido na base; 18 verificações aprovadas na candidata, incluindo true/false, tipos inválidos, idempotência, nomes semelhantes e segredos adjacentes. | Classes reais isoladas, não substitui HTTP. |
| `acceptance-isolated.json` | 36 verificações HTTP aprovadas com MCP sem acompanhantes, documentação e gates. | Bootstrap em laboratório descartável; separado da ativação limpa nativa. |
| `clean.json` | ZIP final em outro banco/raiz vazios; ativação nativa, cron pronto e documento 0.24.0 em processo novo, sem reparo. | Ambiente local single-site. |
| `acceptance-companions.json` | 43 verificações aprovadas; transporte textual/estruturado em sucesso/erro; produtores Google/Core reais; leitura documental e recusa a usuário sem administração. | Sem credenciais/APIs de fornecedores. |
| `upgrade.json` / `upgrade-package.json` | 19 verificações aprovadas no salto 0.23.0→0.24.0; OPcache sem checagem de timestamps; OAuth, renovação, opções false/vazias, backup, recibo incerto, replay e confirmação SQL preservados; 456 arquivos exatos, sem extras. | Credenciais/dados sintéticos. Rollback verificado por prévia, sem aplicação. |
| `package.json` | Build determinístico, inventário preservado, quatro diferenças e lint de **448 arquivos PHP** do instalador. | Lint separado dos testes funcionais. |
| `site-tests.json` | Troca remota única do MCP, novas requisições, upload por URL e true/false reais; saúde final e limpeza aprovadas. | Homologação no Site-Teste; não é distribuição raw da frota. |
| `site-documentation.json` | **17 documentos / 19 páginas**, bytes, SHA-256 e conteúdo idênticos ao pacote; confinamento e revisão antiga recusados. | Mesma conexão de manutenção existente, não novo consentimento CIMD. |

Os números são verificações e incluem repetições entre cenários, não casos independentes de fornecedor. Falhas iniciais de asserções da bancada foram corrigidas (identidade de objetos PHP, criação repetida do usuário e leitura correta do armazenamento); a implementação funcional permaneceu a exceção booleana única. Evidências anteriores à pasta 0240 são históricas.

### Site-Teste

Destino autorizado: `https://fator3-teste-mcp-1.dreamhosters.com/`. Estado e hash do entrypoint 0.23.0 foram relidos imediatamente antes da troca. Uma instalação por `plugins/upload-base64`, com `overwrite:true`, `activate:true`, `expected_slug:wp-mcp-fator3`, `expected_sha256:e2c78fcf0e99da55237808bc51fe408405e367fd76a71172b497707996f8aa95` e timeout de sonda 30 s:

- Operação `f4e8f129d9d4e8a10fbd1a93cb17bd67`; pré-imagem de arquivos `b456da47292f3d600599e4f3`.
- Resultado `applied:true`, 0.23.0→0.24.0, ativo antes/depois, `silent_reactivation`, sem repetir hook inicial. A pré-imagem cobre os arquivos; não é backup integral do banco.
- `plugins/operation-status` em nova requisição: complete, candidate, expected_version 0.24.0, verificação concluída e sondas booleanas. Home e REST retornaram HTTP 200.
- `plugins/upload` real por URL HTTPS do próprio Site-Teste instalou uma fixture **inerte e inativa**, de 295 bytes, slug `f3-mcp-probe-0240`, SHA-256 `249b5ab0fcf0be5f6531e7f080f7e758d8aecc5a64a4ba742c34c023c3fce23a`. Operação `7d1388bb885eef62868a1a90bee9dacd`: **seis valores true** — quatro amostras e dois totais, antes/depois. O transporte textual e estruturado foi verificado localmente.
- Uma sonda do ZIP estático retornou HTTP 200 e **false** na amostra e no total, sem marcador PHP.
- Fixture removida pelo fluxo nativo de confirmação de `plugins/delete`; ZIP temporário removido com SHA-256 esperado. Ausência confirmada. Permanecem somente pré-imagens/diários/auditoria normais das operações; nenhum plugin de teste ativo, conexão sintética ou arquivo público temporário foi deixado.
- Conferidos remotamente os hashes dos **quatro arquivos alterados** e toda a documentação compilada. A comparação completa dos 456 arquivos foi local; não se alega nova leitura remota dos 452 arquivos inalterados.

Estado final: MCP **0.24.0**, Core **1.35.0**, Google **0.11.0**, Meta/LinkedIn **0.2.0**, todos ativos. `system/health` saudável, recuperação sem pendências e marcador cron confirmado. Nenhuma configuração comercial foi alterada.

Para a frota, publicar o instalador/relatório sob autorização própria; destino previsto `https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-fator3-0.24.0-instalador.zip`. **Essa URL não foi publicada nem validada nesta rodada.** Conferir os bytes raw contra a seção 8 antes de `plugins/upload`. Fonte não foi publicado no repositório público.

## 5. Banco e volta de versão

Sem nova migração, tabela, schema, default, importação, retenção ou limpeza. A atualização conserva dados e controles da 0.23.0; testes locais confirmaram opções, credenciais, OAuth/renovação, recibos, estado incerto, backup e confirmação SQL. No site, a conexão de manutenção continuou funcionando em novas requisições; não foi feita auditoria integral dos valores privados de todos os acompanhantes.

Rollback de arquivos deve conferir a pré-imagem, a pós-imagem atual e a ausência de alterações posteriores. A prévia local de retorno à base passou; não houve rollback remoto. Restaurar a 0.23.0 recupera também a redação indevida do Pedido 61. Reversão de arquivos não desfaz dados/efeitos externos ou operações de acompanhantes. Backups e diários de manutenção não foram expurgados.

## 6. O que permanece pendente

- **Frota:** publicação, conferência raw e distribuição para os outros sites. Este pedido não autorizou publicação GitHub automática.
- **Dono/pacote:** nova conexão real ChatGPT/CIMD, B22 histórico, permanece sem homologação. A conexão existente foi usada; não equivale a novo login/consentimento. O documento recebido exclui B22 dos pedidos da frota; não bloqueia o aceite 61.
- **Matriz de runtime:** PHP 8.3.0 não foi exercitado; teste local usa 8.3.6 e remoto 8.3.30. Multisite, CDN/cache distribuído, painel em navegador e falhas de infraestrutura não foram ensaiados nesta correção sem alteração visual.
- **Responsáveis pelos domínios:** APIs/ativos reais Google, Meta e LinkedIn e pendências comerciais anteriores não foram reabertos. Ativação de acompanhantes não é homologação de fornecedor. Implantador atual não avaliado.

Não há falha funcional pendente no Pedido MCP 61 dentro do escopo executado.

## 7. Credenciais e configuração do dono

Nenhum novo campo ou segredo é necessário. Configuração continua em **Ferramentas → Fator3 MCP**, com permissões administrativas e perfil explícito por conexão. `system/guide` conserva o gate documental `edit_posts` e a política do canal; operações administrativas não foram flexibilizadas. Tokens, cookies, salts, dumps e credenciais de laboratório/produção não integram a entrega.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `wp-mcp-fator3-0.24.0-instalador.zip` | 821425 | `e2c78fcf0e99da55237808bc51fe408405e367fd76a71172b497707996f8aa95` |
| Fonte | `wp-mcp-fator3-0.24.0-fonte.zip` | 2942099 | `cd3550c20c2f02c23791c93a7e3ae3966ed69facf5b96fcf0eb0d29294fae44c` |

Somente o instalador é instalável: raiz `wp-mcp-fator3/`, 456 arquivos, incluindo documentação operacional compilada, runtime e dependências. Sem QA ou testes no instalador. Fonte: raiz `wp-mcp-fator3-0.24.0-fonte/`, runtime em `fontes/wp-mcp-fator3/`, documentação editável, build, testes, evidências sanitizadas, entradas e relatório. **Nenhum ZIP contém outro ZIP.**

Relatório externo canônico. A cópia dentro do fonte é identificada como anterior ao fechamento: seus campos de tamanho/hash do próprio fonte são completados somente aqui, sem reabrir o ZIP para inserir hash circular.

Checklist de encerramento conferido: base/alvo; três artefatos; impactos avaliados antes da implementação; identidade/hash; documentação instalada e paginada; instalação limpa; atualização direta; gates, dados e segredos; limpeza e estado final. Exceções/pendências estão na seção 6. Outros plugins e documentos centrais não foram modificados.
