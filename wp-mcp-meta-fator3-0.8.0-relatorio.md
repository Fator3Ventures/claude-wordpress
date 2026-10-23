# Entrega — Fator3 MCP Meta 0.8.0

23/10/2026 · responsável pelo pacote Meta · base aceita 0.7.1.
**Relatório externo definitivo.** O ZIP fonte foi fechado uma única vez; sua cópia interna deste relatório antecede o fechamento para evitar circularidade.

## 1. Bases aceitas

Pedido desta rodada: considerar novas versões, pedidos e relatórios de impacto e implementar nova versão. Aplicadas as instruções comuns e o padrão de desenvolvimento revisão 4 de 16/10/2026. A aba recebida **Fator3 MCP Meta(6).md** declara base 0.7.1 e nenhum pedido aberto; o próximo número 15 não foi atribuído. A mudança decorre de achado próprio reproduzido nesta revisão. A versão minor 0.8.0 segue a regra padrão para a nova rodada.

Base imutável: instalador Meta 0.7.1, **150734 bytes**, SHA-256 `0adbea179f3a89cd66b6dce289fa8658e1723f4a9b38568794fc7c3aea5963f2`; fonte 0.7.1, **753792 bytes**, SHA-256 `17d3b8e275cc7eabe191a569c14bd40d03fc5fc9cf9fa7c06ca2ff1e12f9ac2a`. Os artefatos fechados da base não foram alterados.

Pacotes recebidos, conferidos contra os relatórios e usados na revisão:

| Pacote | Instalador: bytes / SHA-256 | Fonte: bytes / SHA-256 |
|---|---|---|
| Core 1.49.1 | 2230721 / `4ad3be4159310578a2db47cf179d02fa061fb98021e2f66ca933b59e7db4fb40` | 4664837 / `065cad9b9f82f62432ae5c9c87662bb8213a1db3b42b84309ce9409dd69602cc` |
| MCP 0.29.1 | 873894 / `1b627aec5c24dc88f52eaf6a0d34367437d7f9e7b599f9f07850567fd57610e6` | 3945818 / `99ea12645e25d75f2466feebc4ac146e776f33b398d74802f4f6a48327a4142a` |
| Google 0.18.1 | 799626 / `91c97cc300360511bc2477f5af9b0c2017e8b04861d015aaf0f0e5accd1cefef` | 4177792 / `7b8dd2e3425bc1c4e0ddcbff51318069a98293d276e5b18564a603df8d0ab659` |
| LinkedIn 0.9.0 | 236277 / `d4857927ebacfca9321b79d13bc15f15c6969ae67047fd1793e509524b7a60f8` | 1022685 / `26fc1c7573becdee2f904abffc04f20a6e5be63eb5e8e6f5b0e45d1c53701733` |

Os quatro acompanhantes já estavam ativos no Site-Teste antes desta rodada; não se atribui sua instalação ao agente Meta. Entradas, manifestos e relatórios recebidos estão em `inputs/0.8.0`. Provas próprias novas estão exclusivamente identificadas em `evidence/release080`; provas antigas conservadas no fonte são históricas.

## 2. Convivência e encaminhamentos

Conjunto integrado efetivamente usado: WordPress **7.1.3**, PHP **8.3.36** de 64 bits, MySQL **8.0.41**, Core **1.49.1**, MCP **0.29.1**, Google **0.18.1**, LinkedIn **0.9.0**, Meta **0.8.0**. Continuaram ativos WP Super Cache 3.1.4, Yoast SEO 28.7 e DreamHost Panel Login 1.0.0.

**Impacto recebido MCP 0.29.1 → Meta, revisão 2:** resolvido no MCP, sem alteração obrigatória no produtor. A documentação Meta passou a explicitar que `retryable` não prova ausência de efeito, que não se deve acrescentar `applied=false` sem prova, e que observação atual de `health` deve omitir chave de idempotência. O envelope Meta não foi alterado. Prova própria: os erros Meta busy/upstream_error/rate_limited sem applied não são transientes no coordenador; duas execuções com a mesma chave e callback sintético retornam o recibo com apenas uma execução do callback. O controle explícito não aplicado continua elegível. Read permite health e recusa status; custom sem status recusa reparo; maintenance permite status. Isso é prova de contrato local real com falha sintética, não de retry de fornecedor.

**Impacto recebido LinkedIn 0.8.1 → Meta, revisão 2:** R1/R2 encerrados pela resposta Meta 0.7.1. O alerta inverso de concorrência foi tratado pelo mantenedor LinkedIn como pedido 12 na 0.9.0. A inspeção própria confirma trava individual, decodificação do mesmo payload e CAS de revisão/cifra, usados por migração e retenção. As provas específicas LinkedIn são recebidas de seu mantenedor; não foram reexecutadas integralmente aqui.

O impacto próprio original `wp-mcp-meta-fator3-0.7.1-impacto-wp-mcp-linkedin-fator3.md` foi atualizado para **revisão 4, encerrado**, preservando a emissão original e o histórico. Não foi criado novo impacto apenas para notificar a versão. Nenhuma mudança em código de acompanhantes, regra central ou aba de pedidos. Nenhum encaminhamento foi enviado.

Integridade própria em Site-Teste: **1176 arquivos**, sem divergência frente aos pacotes aceitos: MCP 463, Core 453, Google 159, LinkedIn 59 e Meta 42. Verifica os arquivos esperados; não substitui homologação completa das funcionalidades comerciais dos acompanhantes. Não há ordem obrigatória de troca para esta correção. Evidências: `r080-site-companions.json`, `runtime-manifests.json` e `linkedin090-static-review.json`.

## 3. Mudanças e evidências

### Achado próprio: isolamento baseado em duas leituras

Na 0.7.1, Queue::isolate lia revisão/payload e chamava Store::get, que fazia uma segunda leitura para decidir legibilidade. Um gravador externo que ignora a trava consultiva pode alterar o payload entre as leituras e restaurar exatamente revisão e bytes originais antes do UPDATE. O CAS então aceita o primeiro snapshot, embora a decisão tenha sido tomada sobre o segundo. O resultado reproduzido foi um job **legível** com projeção **unreadable**.

A gravação normal Store::put incrementa revisão e não produz essa restauração. A reprodução usa outra conexão MySQL e interleaving determinístico de gravador/restauração externa; não prova ocorrência nem frequência em produção. Na base 0.7.1, dois dos oito checks falharam como esperado: projeção indevida e duas leituras. Os seis controles passaram. Evidência `negative071.json`.

**Correção:** Store::decode concentra as mesmas regras de cifra/JSON/tipo antes usadas por Store::get. Queue::isolate decodifica diretamente o payload do snapshot usado no CAS. Mantidos trava do job, igualdade binária do ciphertext, revisão, códigos de erro e atualização exclusiva de queue_state/queue_next. Não há segunda leitura decisória. Falha SQL não é tratada como corrupção; cifra/JSON inválidos continuam isolados sem regravar os bytes de negócio.

Alteração funcional limitada a `build/common/Support.php` e `build/common/Queue.php`, refletida no runtime Meta. Configuração/cabeçalho/readme e documentação gerada refletem 0.8.0. Assets, schemas de entrada/saída e as 34 identidades públicas foram preservados. Nenhuma assinatura pública existente foi alterada; não foi copiado o template LinkedIn inteiro. Diff reproduzível em `runtime.patch` e `diff-summary.json`.

### Matriz de execução própria

| Ambiente/cenário | Checks | Resultado |
|---|---:|---|
| Base 0.7.1, reprodução em tabela exclusiva no Site-Teste | 8 | 2 falhas esperadas, 6 controles aprovados |
| Limpo, WP 7.1.3/PHP 8.3.36, somente Meta, primeira candidata¹ | 218 | 0 falhas |
| Limpo, WP 6.4/PHP 8.1.34, somente Meta | 137 | 0 falhas |
| **Limpo, WP 6.4/PHP 8.1.2-1ubuntu2.28, somente Meta** | **137** | **0 falhas** |
| Atualização direta 0.7.1 → 0.8.0, WP 7.1.3/PHP 8.3.36 | 5 | 0 falhas |
| Metadados/documentação após a atualização, pacote final | 101 | 0 falhas |
| Site-Teste integrado, pacote final | **168** | **0 falhas** |
| Selftest final pelo MCP | 8 | 0 falhas; externo não executado |
| Leitura documental pelo MCP, pacote final | 17 documentos / 21 chamadas | conteúdo, bytes e SHA-256 exatos |
| Lint do fonte PHP e runtime | 82 arquivos em cada PHP | sem erros em 8.3.6 e 8.1.2-1ubuntu2.28 |

¹ A primeira candidata tinha apenas um título histórico incorreto no changelog, corrigido antes do instalador final. O PHP era idêntico. As provas da matriz mínima, atualização, integração e leitura documental usam a documentação final. Não se soma a matriz como se todos fossem cenários distintos: há repetições por runtime.

Os 137 checks do mínimo são: snapshot 8, smoke/REST/documentos 24, worker 26, regressões 0.7.0 20, regressões 0.7.1 11 e suite geral 48. WordPress 6.4 não tem Abilities API nessa instalação; painel, REST e ajuda local foram exercitados sem MCP ou acompanhantes. O mínimo funcional desta rodada é **PHP 8.1.2-1ubuntu2.28**, não apenas lint. Pacotes oficiais fixados por SHA-256 foram extraídos somente no laboratório privado; não houve substituição do PHP do site.

Os 168 checks integrados são: worker 30, regressões de saúde/retenção 21, revisão adversarial 11, snapshot 8, metadados/autorização/UI HTML 82 e fronteira MCP/integridade 16. A suite geral cobre consulta, checkpoint, exportação, histórico, token/asset selection, erros Graph e backfill com respostas simuladas. Os casos de concorrência usam MySQL real e trava de outra conexão, não somente mocks.

Observações adicionais: bootstrap sem SQL próprio do Meta; marcas em autoload; remoção controlada do evento de manutenção e recuperação na requisição seguinte. Diagnóstico e status preservam seus contratos. Testes de UI inspecionam HTML gerado pelo WordPress, sem alegação de navegação visual completa em navegador.

Ajustes somente no harness: guarda antiga recusava o marcador técnico history_generation; passou a permitir esse marcador e manteve recusa a dados de negócio. A tentativa inicial bloqueada foi preservada em `r080-site-review.json`; a execução final aprovou 11 checks. A instalação mínima em PHP 8.1.2 emitiu aviso de PCRE JIT indisponível no host; desabilitado apenas no CLI de laboratório, suites finais com stderr vazio. Houve também aviso de ABSPATH no primeiro teste do runtime, corrigido na configuração privada do harness. Nenhum desses ajustes alterou o instalador.

## 4. Instalação e prontidão

Site autorizado: https://fator3-teste-mcp-1.dreamhosters.com/ . Alteração realizada por plugins/upload-base64 com overwrite, activate, expected_slug e SHA-256 do instalador final. Atualização **0.7.1 → 0.8.0**, ativa antes/depois, reativação em PHP novo, applied=true. Operação de pacote `1496500865136bbfd53372940b0ae289`; backup `19984b07579a4be93357da18`. Sondas anônimas de home e REST retornaram 200 antes/depois, com bypass verificado. São requisições internas same-origin; não se afirma prova de acesso externo ou invalidação de cache público.

A instalação por MCP usa reativação silenciosa e não comprova isoladamente o ciclo de activation hook nem prontidão comercial. A instalação limpa nativa separada e os testes funcionais acima complementam essa limitação. Na atualização isolada, conexão cifrada, job concluído, job pausado com checkpoint, resultado, agenda, histórico e opção de negócio permaneceram byte a byte iguais, incluindo projeções, revisão e datas.

Estado final: Meta 0.8.0 ativo; health state=ok, issues vazio, armazenamento e criptografia prontos, unreadable_jobs=0, zero conexões/agendas ativas. Selftest local aprovado; remote_homologated=false. O inventário final tem oito plugins ativos no total, nas versões registradas.

Os **17 documentos** instalados foram lidos pelo MCP até o fim e comparados com o ZIP: versão 0.8.0, tamanho e hash estáveis. WORKER.md foi lido em cinco páginas; os demais em uma cada. Identificadores, rótulos em português, permissões de assinante, REST e confinamento documental também foram exercitados. Prova: `mcp-document-verification.json` e conteúdo completo em `mcp-documents.json`.

Pronta para entrega e implantação coordenada pelo dono/frota, com os limites externos da seção 6. Não houve publicação no repositório público nem implantação nos demais sites.

## 5. Banco, preservação e reversão

Sem migração nova ou mudança de schema, sal, chave, prefixo, estrutura de configuração ou formato cifrado. O isolamento altera apenas projeção técnica quando o snapshot conferido é ilegível. Registros já unreadable não são reativados automaticamente; recuperação deve inspecionar chave, payload e autorização antes de qualquer ação explícita.

Os laboratórios usam diretórios privados e prefixos aleatórios próprios; cada cleanup removeu 14 tabelas exclusivas, diretório e manifesto. O WordPress compartilhado não foi reinstalado e o banco do site não foi apagado. Credenciais de banco ficaram no servidor e não integram evidências.

Final confirmado por leitura: zero tabelas qa080/f3qa080, zero opção de laboratório, zero usuários meta080 e zero linhas de histórico sintético. As quatro sondas desta rodada e o controlador foram removidos. Restam apenas os quatro MU-plugins de recuperação que já pertenciam ao ambiente. No armazenamento Meta permanecem auditoria legítima e marcadores técnicos history_generation/migration; não há conexões, jobs, resultados ou agendas de teste. Backups/auditoria do MCP foram preservados.

Reversão de arquivos pode usar o backup da operação ou o instalador imutável 0.7.1. Como não há migração nova, os dados continuam compatíveis, mas o retorno reintroduz a janela corrigida. Backup do pacote não reverte efeitos de banco nem equivale a restauração de site; a ferramenta declarou database_effects_reversible=false. Não foi executado rollback final, pois a versão validada deve permanecer corrente.

## 6. Pendências e limites

Não há correção de código pendente identificada nos testes desta rodada. Não se garante ausência universal de impacto além do escopo exercitado.

| Tema | Situação e responsável |
|---|---|
| Homologação social real e entrega de e-mail | Não executadas nesta rodada; dono/frota com ativos e destinos autorizados. Fixtures interceptaram HTTP e e-mail. |
| Pendência geral 20 da aba recebida | Permanece com a frota para prova em produção de rotação, histórico/exportação, Story após expirar, aviso e gates previstos. O 403 de assinante foi provado aqui em teste; isso não fecha prova de produção. |
| Pendência geral 88 | Estado/configuração da frota permanece sob seu responsável; nenhum site além do Site-Teste alterado. |
| APIs comerciais de Core/Google/LinkedIn | Convivência, inventário e integridade próprios; suites completas e homologações externas desses domínios não foram repetidas. |
| MariaDB e multisite | Não exercitados nesta rodada; banco real usado MySQL 8.0.41. Não ampliar suporte por inferência. |
| Frota e documentos centrais | Entregar ao dono para atualização da referência corrente e implantação; nenhuma alteração editorial central ou publicação foi realizada aqui. |

Nenhum número novo de backlog foi inventado. Relatórios recebidos e inspeção estática de outro pacote não são apresentados como testes próprios daquele mantenedor.

## 7. Credenciais

Nenhuma nova credencial exigida, alterada ou exportada. Não há token social real no Site-Teste usado para esta validação. Testes empregaram valores sintéticos e grants temporários próprios, removidos ao final, restaurando a identidade MCP original. Chaves do site e credenciais de banco não saíram do servidor; arquivos temporários privados foram removidos.

O modelo de tokens manuais e concessões existentes permanece. Nenhum segredo, cookie, dump de banco ou runtime PHP baixado integra a entrega. Domínios comerciais e de fornecedores não receberam operações reais desta rodada.

## 8. Artefatos finais

Somente o instalador é instalável. O fonte inclui código canônico, runtime, scripts, testes, provas sanitizadas, planejamento, entradas documentais e esta cópia pré-fechamento. Não contém ZIPs aninhados. O relatório externo traz a identidade definitiva do fonte, depois de seu fechamento único.

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-meta-fator3-0.8.0-instalador.zip | 153819 | `36e4e098955576c3d43ea1b1bd2c14fe68608472b8666a652e84da5165ce25e1` |
| wp-mcp-meta-fator3-0.8.0-fonte.zip | 996667 | `ef929b96e4336c350b0d7f802b082f166051127ab10063ac05f114b669c3ce99` |
| wp-mcp-meta-fator3-0.8.0-relatorio.md | Arquivo externo | Não se registra hash autorreferente |

Complemento: atualização do impacto original `wp-mcp-meta-fator3-0.7.1-impacto-wp-mcp-linkedin-fator3.md`, revisão 4, encerrado. Não é um novo encaminhamento de versão. O hash do instalador coincide com a instalação real, o runtime empacotado e as verificações documentais.


Fechamento conferido: ZIPs íntegros, raízes corretas, sem ZIPs aninhados; runtime fonte igual ao instalador validado no Site-Teste.
