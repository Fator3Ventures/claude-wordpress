# Entrega — Fator3 MCP 0.33.0

Revisão 1 · 25/10/2026 · America/Sao_Paulo · Rodada: implementação.
Slug: `wp-mcp-fator3` · Basename: `wp-mcp-fator3/wp-mcp-fator3.php`.

**Versão corrente: 0.33.0, instalada e ativa no Site-Teste. Status: apta-no-escopo-testado.** O pedido MCP 68 foi implementado e validado. A correção de autorização do Core 1.54.0 foi confirmada, encerrando o encaminhamento emitido pela 0.32.0. Não foi identificado novo impacto técnico que exija ação de outro mantenedor.

**Relatório externo canônico.** O fonte contém uma cópia interna anterior ao fechamento. A identidade final dos ZIPs é registrada abaixo, evitando circularidade; ambos são imutáveis.

## 1. De onde esta versão entra

Base aceita **0.32.0**, preservada: instalador 885606 bytes, SHA-256 `fd2097055383a26e6ca5b79b655f0b3740c337a42dab6ce2b43b4236c07496b1`; fonte 4443847 bytes, SHA-256 `d7413eda5cae051c35c9f08f21a3e47cb9fc02e8e0d22462dd094b2cbf445c4e`. Percursos comprovados: WordPress limpo e atualização direta **0.32.0 → 0.33.0**, sem intermediária.

Entradas: pedido MCP **68**, Core **1.54.0**, relatório do Core e encerramento recebido do impacto de autorização da 0.32.0. Normas comuns **revisão 5**, de 23/10/2026; as cópias antigas revisão 4 não substituem essa norma. Os hashes dos 12 ZIPs aceitos estão em `docs/entradas/0330/packages.json`. A implantação anterior da 0.32.0 nos 12 sites consta do pedido recebido; não foi executada ou revalidada pela presente rodada.

Mínimos mantidos e exercitados: WordPress **7.1.2**, PHP **8.3.6**, 64 bits. Laboratório integrado: WordPress **7.1.3**, PHP **8.3.6**, MySQL **8.0.46**, PHP-FPM/lighttpd e OPcache sem validação de timestamps. Site-Teste: WordPress **7.1.3**, PHP **8.3.36**. A nova versão minor segue a regra do projeto.

## 2. Convivência e encaminhamentos

| Pacote | Versão aceita | SHA-256 do instalador | Cobertura própria |
|---|---|---|---|
| Site Core | 1.54.0 | `c3542b4c293b46357d013abb05e6f302611fe8392d01dd85ceb330fe2b6b66a7` | Escrita/leitura reais, redação, correio e gates locais; aceite no Site-Teste |
| Google | 0.19.0 | `d15868915e3fdf886d7e883a82d9d302df7242808fc94d45bf3e1857234759d1` | Ativação, descoberta e integridade locais; ativo no Site-Teste |
| Meta | 0.10.1 | `f80d934fe1851bc887a0174190b42d73b36a8637f2f4824bdb5cfeb7a674ee95` | Ativação, diagnóstico, descoberta e integridade locais; ativo no Site-Teste |
| LinkedIn | 0.10.1 | `6182ea63bff6788f5d2637467e7ab29d58568e37283d6ece82d3e58ee41c13bc` | Ativação, diagnóstico, descoberta e integridade locais; ativo no Site-Teste |
| Pipedrive | 0.1.0 | `3366d83ca8908e407a0736812d30b8fa1506a8c1458a28cfb47eda6fd8f3c54f` | Ativo no Site-Teste; configuração Core consultada, sem efeito comercial |

O fonte Core 1.54.0 tem 3642476 bytes e SHA-256 `0e691e0fa05c9575464cd107ded05e577a3611c5189dde6dfcddad916b8b8145`. Pipedrive não foi ativado no PHP local 8.3.6, inferior ao mínimo 8.3.36 declarado por ele. A integridade das árvores locais Core/Google/Meta/LinkedIn foi comparada aos respectivos instaladores. Nenhum acompanhante foi editado ou atualizado nesta rodada.

No Site-Teste, também permaneceram DreamHost Panel Login 1.0.0, WP Super Cache 3.1.4 e Yoast SEO 28.7. Versão e atividade dos oito plugins alheios são idênticas antes/depois. Não há nova exigência de ordem de troca entre pacotes: a instalação própria continua independente de acompanhantes.

### Impactos e pedidos emitidos

**Nenhum novo encaminhamento.** Foram examinadas as fronteiras de apresentação, contratos Core de configuração/instrumentação, autorização de correio, descoberta dos acompanhantes e idempotência. A solução MCP usa o contexto da chamada e não pede ao Core que acrescente `nome`. Não muda contrato, configuração ou responsabilidade de outro pacote. Operações comerciais externas e interfaces não pertinentes a essa mudança permanecem fora da homologação desta rodada.

### Respostas e encerramentos de impactos anteriores

| Documento / pedido | Resultado | Responsável e evidência |
|---|---|---|
| `wp-mcp-fator3-0.32.0-impacto-base-site-core-fator3.md`, revisão 1, Core300 | **Atendido pelo Core 1.54.0; encerrado.** Revogar envio ou leitura de leads impede reapresentar prévia privada e recibo incerto. | Core corrigiu os callbacks; MCP repetiu 8 checks com 0.32.0 e 8 com 0.33.0, todos aprovados. Correio ampliado: 32 checks. |
| Pedido MCP68(a) | **Implementado, validado-localmente e validado-wordpress.** `lido` aplicado sem `nome` e `token_indisponivel` legíveis. | MCP; 117 unitários novos, 28 HTTP e aceite Site-Teste. |
| Pedido MCP68(b/c) | **Implementado, validado-localmente e validado-wordpress.** Nomes herdados legíveis; credenciais e formas inválidas mantêm máscaras e caminhos. | MCP; casos negativos, JSON Pointer e paridade em HTTP bruto. Ponte do conector não expõe `_meta`. |
| Core301, impacto Core1.53 revisão 2, e MCP67 | Atendimento anterior preservado. | 144 + 218 unitários, 21 HTTP de política, 30 HTTP de redação e contadores reais. |
| Core302 — contato externo e vínculo de sessão | Novas abilities e schemas visíveis; código dos gates examinado. Não exige adaptação MCP nesta rodada. | `f3base/contato-externo-registrar` e `f3base/contato-sessao-vincular`; não foram executadas mutações comerciais. |

Conforme a norma revisão 5, o encerramento fica neste relatório; não é gerado um relatório de impacto de retorno. Os testes declarados no relatório recebido do Core são evidência recebida, separada dos testes próprios acima.

## 3. Mudanças, comportamento e riscos

`SafeOutput::call_context` extrai apenas a ability efetivamente resolvida e o nome da option dos argumentos usados na chamada. O contexto é local à resposta, passado pela apresentação de sucesso/erro e nunca retido globalmente. Executores genérico/de leitura aceitam objeto, stdClass e JSON textual; valores e credenciais não são guardados nesse contexto. O objeto de negócio, a comparação, os recibos e os snapshots internos não são reescritos.

- **Escrita aplicada:** em `f3base/config-core-escrever`, `lido` da option `f3base_formularios_sinais` fica legível mesmo sem `nome` na resposta. Mantém a validação da 0.32.0: até 100 sinais, nomes válidos, exatamente `suspeito` e `aviso` booleanos. Contexto incorreto, forma inválida, propriedades adicionais e caminhos alheios permanecem fechados.
- **Mensagem de interface:** somente `f3base/conteudo-instrumentacao-ler`, em `por_url.URL.formularios.N.complemento.mensagens.token_indisponivel` e `linhas.N.formularios.N.complemento.mensagens.token_indisponivel`. Texto de até 1000 caracteres UTF-8; credenciais reconhecíveis, JWT, chave privada e atribuições de segredo continuam redigidos. Não há liberação geral de `token_*`.
- **Chaves herdadas:** somente `f3base/config-core-ler`, no caminho `opcoes.NOME.chaves_herdadas`. Preserva lista de nomes, lista vazia ou null legítimo. Até 4096 itens e 1024 bytes por nome, com segmentos alfanuméricos, sublinhado, hífen e ponto. Nome vazio representa a raiz. Itens inválidos são mascarados individualmente; mapa ou lista excessiva é mascarado inteiro.
- **Metadados:** mantém `_meta["fator3/redaction"]`, JSON Pointer, total/truncated, scope=structuredContent e paridade entre texto e objeto. Campos mascarados continuam identificados; valores públicos preservados não recebem falsa indicação.

O runtime muda em **5 arquivos**, conserva **459 arquivos byte a byte**, sem adição/remoção: `includes/Release014.php`, `core/includes/Server/Handlers/Tools/ToolsHandler.php`, os dois guias compilados e o bootstrap de versão. `DataSafety`, políticas de autorização, autenticação, execução de mutações, SQL, auditoria, banco, agenda e credenciais não foram alterados. A documentação corrente distingue os registros históricos.

Risco residual: a apresentação reconhece segredos por estrutura e padrões, não por conhecimento de todo texto possível. Uma string arbitrária colocada pelo produtor num campo legítimo de interface não pode ser identificada semanticamente como segredo. As exceções ficam restritas aos campos e tipos públicos descritos; não se aplicam a SQL, armazenamento ou campos de credencial.

## 4. Instalação e prova de prontidão

| Cenário | Checks finais | Resultado / evidência em `evidencias/0330/` |
|---|---:|---|
| Unitários PHP mínimo | 218 + 144 + 117 = 479 | Todos aprovados; redação anterior, política e pedido68 |
| Integrado WP7.1.3 / Core1.54 | 306 | Todos aprovados; suites detalhadas em summary.json e current/ |
| Instalação limpa WP7.1.2, MCP apenas | 13 | Ativação, processo novo, cron, HTTP e inventário exato |
| Atualização direta 0.32.0 → 0.33.0 | 22 | Todos aprovados; arquivos, workers, OAuth, recibos e rollback-preview |
| Reprodutor de autorização em MCP0.32 / Core1.54 | 8 | Todos aprovados; correção pertence ao Core |
| Pacote | 15 | Inventário, reconstrução idêntica, rejeição de ZIPs inválidos, versão e segurança |
| Sintaxe | 453 PHP | Todos aprovados no PHP8.3.6; incluído na validação de pacote |
| Site-Teste WP7.1.3 / PHP8.3.36 | 21 | Todos aprovados; site-test.json |
| Documentação remota | 32 documentos / 34 páginas | 222057 bytes, todos idênticos ao pacote; remote-documents.json |

**828 checks locais funcionais finais**, mais 15 de pacote, lint e 21 de aceite remoto. Não se somam setup ou tentativas anteriores. Os 306 integrados incluem pedido68 HTTP28, política21, correio32, autorização8, redação30, OAuth/CIMD48, adversarial18, idempotência7, mídia9, descoberta17, busca11, admin26, documentos35 e acompanhantes16.

Foram corrigidas expectativas/fixtures do ensaio durante a preparação: formulário sintético inicialmente ausente, campo `changed` inexistente na resposta aplicada Core, executor de leitura que precisa estar habilitado e código de recusa antecipada `permission_denied` no Core1.54. O texto de diagnóstico remove também o prefixo Bearer. O token Pipedrive fica em option separada, não dentro da configuração `f3base_pipedrive`. Os ensaios finais passaram; essas correções de harness não mudaram o runtime. O build também detectou e impediu uma divergência inicial no cabeçalho de versão, corrigida antes do pacote testado.

O log integrado registra três avisos nativos de atualização WordPress por rede externa bloqueada no laboratório. A primeira tentativa do harness registrou um TypeError por fixture ausente, corrigido antes da suíte final. Instalação mínima e atualização final não registraram warning/fatal. Recusas de perfil e entrada nos ensaios negativos são intencionais. Resumo sanitizado em log-review.json. Instruções de reprodução: `tools/release0330/README.md`.

### Troca e aceite no Site-Teste

Destino: `https://fator3-teste-mcp-1.dreamhosters.com/`, conexão OAuth existente pelo endpoint `/wp-json/mcp/wp-mcp-fator3`. Upload em quatro partes via `files/upload-create`, `files/upload-part` e `files/upload-finalize`, com conferência de 888204 bytes e SHA-256. `plugins/upload` recebeu URL do ZIP no próprio site, `expected_slug=wp-mcp-fator3`, hash esperado, `overwrite=true`, `activate=true` e sonda de 30s. A troca retornou `applied=true`, versão0.33.0 e atividade preservada.

- Operação do pacote: `5b254321b6c054febcce216ca318c051`; status posterior `complete`, `verified`, ativo, arquivos `candidate`.
- Backup: `9ed5f3716f55a8984f1f2177`; pré-imagem conferida por `plugins/rollback` com `dry_run=true`, sem aplicar reversão.
- Sondas `/` e `/wp-json/`: aprovadas antes/depois, com bypass verificado. São sondas internas na mesma origem; não certificam todo acesso público externo ou prontidão comercial.
- Saúde final `healthy=true`, 11 verificações verdadeiras e cron confirmado. A conexão continuou funcional. Nenhum outro plugin foi trocado.

O aceite leu a política e simulou o **mesmo valor**, `alteraria=false`. A aplicação usou `simular=false`, revisão vigente e chave idempotente distinta da simulação. Retornou `ok=true`, `persisted=true`, `lido` completo e sem `nome`, operação `fdd4e2f18bfab4687d0d0171`. A releitura confirmou valor e revisão `6eb92dfababd5f4cc8b7ff8f6534472cd56aa76e5c05daa66a18725031769626` inalterados. A auditoria Core foi confirmada; procedência/auditoria podem ser atualizadas mesmo sem mudança da preferência. A verificação comportamental Core permaneceu `pending/requer_observacao`, sem efeito síncrono requerido: isso não equivale a homologar a política antispam em tráfego real.

Os formulários reais `contato` e `contato-whatsapp` passaram a devolver “Não foi possível preparar o envio. Tente novamente.” nas duas projeções de instrumentação, com cobertura HTML completa. `chaves_herdadas` passou de máscara para `[]` nas configurações sinais e Pipedrive. Nomes não vazios foram comprovados no laboratório, removendo uma chave da option sintética e restaurando-a em seguida.

Consultas reais das options `f3base_pipedrive_token` e `f3base_email_site_senha` permaneceram `[redigido]`. SELECT de constantes sintéticas comprovou senha/token mascarados e razões de redação. Nenhuma credencial foi revelada, alterada ou reemitida. A ponte do conector não retorna `_meta`; seus caminhos foram comprovados no HTTP MCP bruto local, incluindo valores inválidos, caminhos escapados e texto/structuredContent iguais.

Os 32 documentos foram lidos integralmente por `system/guide`, com paginação e hash esperado, e comparados byte a byte ao instalador. O ZIP temporário público foi removido com guarda pelo hash. Nenhum PHP de QA foi instalado no Site-Teste, nenhuma mensagem foi enviada e nenhuma mutação comercial foi executada. Os serviços locais foram encerrados; a frota não foi alterada nesta rodada.

## 5. Banco e volta de versão

Sem migração de schema/options, nova tabela ou mudança de prefixos. O upgrade preservou dados de configuração false/vazio, credenciais Application Password/OAuth, validade dos tokens, refresh, recibo concluído e incerto, confirmação SQL pendente e backup privado. A atualização conserva o perfil da conexão; não concede capacidades para contornar decisões do Core.

A instalação/validação grava somente os registros operacionais normais e a confirmação auditada da política com o mesmo valor. O backup verificado permite voltar os arquivos à 0.32.0 com `plugins/rollback`; reaparecerá o mascaramento do pedido68. Restaurar arquivos não reverte banco, auditoria ou efeitos externos. Não houve rollback efetivo nesta rodada. Preserve o backup até o aceite operacional.

## 6. Pendências e limites de validação

Não há pendência de implementação ou de aceite do **pedido68**. A entrega é apta para as funções e combinações testadas, sem promessa de ausência absoluta de impacto.

- SMTP/IMAP reais, entrega de correio, APIs comerciais Google/Meta/LinkedIn/Pipedrive e caso comercial Core302: **não homologados nesta rodada**. Responsável operacional/dono de cada integração. Os testes usam prévias/recibos sintéticos, sem efeito externo.
- As novas abilities Core302 foram descobertas e seus schemas/gates examinados; não foram exercitadas sobre contatos reais. Simulação e aplicação devem usar chaves de transporte diferentes; repetição da mesma intenção mantém sua chave.
- OAuth/CIMD tem 48 regressões locais e conexão OAuth real existente comprovada. Não foi criada uma nova conexão nem repetido consentimento/CIMD externo do zero nesta rodada. Registros B22 históricos não são evidência de falha nova desta versão.
- Interfaces visuais em navegador, multisite, runtimes fora da matriz, cache persistente Redis/Memcached e observação prolongada: não avaliados nesta rodada. A mudança não altera UI.
- `verification.pending` da política no Core é observação de comportamento de domínio, não falha de persistência ou de legibilidade. Nenhum tráfego foi forçado para tentar mudar esse estado.

## 7. Credenciais

Nenhum preenchimento ou novo escopo é necessário para esta atualização. Use a conexão existente em Ferramentas → Fator3 MCP. Configurações e credenciais de fornecedores continuam sob seus donos. Para correio, o produtor exige `f3base_enviar_email` e `f3base_ler_leads`; administrar WordPress sozinho não substitui essas capacidades. A atualização MCP não as concede. Valores de senha/token não integram o relatório ou os artefatos.

## 8. Estado final e uso

Considere **0.33.0 como corrente**. Instale exclusivamente o ZIP instalador, preserve dados e confirme versão/saúde/documentação após cada instalação. Os ZIPs anteriores permanecem imutáveis. Para outros sites, o responsável pela frota deve usar o processo vigente de publicação/verificação dos bytes e o instalador certificado; nenhuma publicação GitHub ou distribuição à frota foi feita nesta rodada.

## 9. Identidade dos arquivos

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| `wp-mcp-fator3-0.33.0-instalador.zip` | 888204 | `f16ee3e31e4143ffb42c566ea6da4f2da81d3771a01a0f90b5d34e3d02ac8caa` |
| `wp-mcp-fator3-0.33.0-fonte.zip` | 4585261 | `fdef8375bd72533062dff506be52664057619655e948afa3b89e22d4114e2ed6` |

O instalador contém 464 arquivos, 453 PHP, uma única raiz `wp-mcp-fator3/` e nenhum teste, ferramenta, fixture ou ZIP aninhado. O fonte contém runtime equivalente, código, build, documentação editável, entradas rastreadas, testes e evidências sanitizadas. Dependências binárias, laboratórios, credenciais, helpers privados e estado de sessão são excluídos. Não há relatório de impacto adicional nesta entrega.

Arquivos finais:

- [wp-mcp-fator3-0.33.0-instalador.zip](sandbox:/workspace/scratch/d7106ddbcd96/release0330/final/wp-mcp-fator3-0.33.0-instalador.zip)
- [wp-mcp-fator3-0.33.0-fonte.zip](sandbox:/workspace/scratch/d7106ddbcd96/release0330/final/wp-mcp-fator3-0.33.0-fonte.zip)
- [wp-mcp-fator3-0.33.0-relatorio.md](sandbox:/workspace/scratch/d7106ddbcd96/release0330/final/wp-mcp-fator3-0.33.0-relatorio.md)

Fechamento: o fonte tem 1892 arquivos. Reconstruído a partir do ZIP fonte extraído, o instalador é byte a byte idêntico ao certificado, incluindo os 56 índices de silêncio gerados pelo build. O resumo e o aceite remoto finais estão dentro do fonte.
