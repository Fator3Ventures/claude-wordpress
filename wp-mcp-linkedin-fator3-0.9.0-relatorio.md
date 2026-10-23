# Entrega — Fator3 MCP LinkedIn 0.9.0

23/10/2026 · Base aceita: **0.8.1** · Versão entregue e corrente do pacote: **0.9.0** · Pedido: **MCP LinkedIn 12**.

**Estado: implementado e validado no escopo técnico, com pendências externas de homologação comercial já existentes.** A 0.9.0 está ativa no Site-Teste. A distribuição para os demais sites cabe ao responsável pela frota.

Relatório externo final. A cópia dentro do fonte está identificada como anterior ao fechamento; o tamanho e o SHA-256 do fonte fechado estão na seção 7 desta versão externa.

## 1. Bases aceitas e documentos considerados

Base LinkedIn 0.8.1 confirmada pela aba de pedidos recebida. Instalador: `wp-mcp-linkedin-fator3-0.8.1-instalador.zip`, **232544 bytes**, SHA-256 `172081883af66b8c4b61676396d85066d4be0778b7ca06fb22262b30a4d2374a`. Fonte: `wp-mcp-linkedin-fator3-0.8.1-fonte.zip`, **882430 bytes**, SHA-256 `bd43abba9412e7292d9810ab38ecb763d2a2efd30d1e3485652a598aeb16c024`.

Foram considerados os dois documentos normativos do projeto, a aba `Fator3 MCP LinkedIn(7).md`, os quatro conjuntos fonte/instalador/relatório novos e os impactos recebidos do Meta 0.7.1 e MCP 0.29.1. Os hashes das entradas estão em `inputs/0.9.0/manifest.json`. Os sete documentos anexos e as normas foram preservados; o relatório do LinkedIn registra a resposta ao pedido sem editar sua aba central.

| Pacote acompanhante | Versão | Bytes do instalador | SHA-256 do instalador |
| --- | --- | ---: | --- |
| Fator3 Site Core | 1.49.1 | 2230721 | `4ad3be4159310578a2db47cf179d02fa061fb98021e2f66ca933b59e7db4fb40` |
| Fator3 MCP | 0.29.1 | 873894 | `1b627aec5c24dc88f52eaf6a0d34367437d7f9e7b599f9f07850567fd57610e6` |
| Fator3 MCP Google | 0.18.1 | 799626 | `91c97cc300360511bc2477f5af9b0c2017e8b04861d015aaf0f0e5accd1cefef` |
| Fator3 MCP Meta | 0.7.1 | 150734 | `0adbea179f3a89cd66b6dce289fa8658e1723f4a9b38568794fc7c3aea5963f2` |

## 2. Convivência, fronteiras e encaminhamentos

Os acompanhantes acima foram usados nas instalações locais integradas e já estavam ativos no Site-Teste antes desta rodada. Nenhum foi atualizado por esta execução. A comparação de todos os arquivos dos acompanhantes nos dois laboratórios integrados conferiu com os ZIPs recebidos (`companion-integrity.json`). O inventário final do Site-Teste conserva suas versões e estados ativos.

O impacto Meta 0.7.1 revisão 3 originou o pedido 12 e foi usado como referência. A implementação foi adaptada e testada no domínio LinkedIn. O alerta próprio `wp-mcp-linkedin-fator3-0.8.1-impacto-wp-mcp-meta-fator3.md` foi atualizado para revisão 2 e encerrado pela resposta técnica recebida sobre R1/R2; mantém a identidade da emissão original. As 392 verificações declaradas pelo Meta são evidência recebida, não provas próprias desta entrega.

O impacto MCP 0.29.1 revisão 2 exige prova explícita `applied=false` para admitir repetição, junto dos demais sinais conservadores. A correção de fila não altera o envelope de mutações nem adiciona esse campo por suposição. Registros de efeitos incertos continuam conservados. O SDK de conversões, o Lead Reader e os contratos de auditoria permanecem iguais; os testes de integração exercitam suas fronteiras com o MCP atual.

Não foi identificada consequência técnica que exija nova ação de Core, MCP, Google ou Meta. Portanto não foi emitido novo documento individual de simples aviso. **Não foram editados nem reemitidos documentos de outros mantenedores.** As revisões indevidas de Core/MCP herdadas do fonte 0.8.1 foram apenas segregadas como histórico recebido, com aviso de que não são referências correntes; os originais e novos documentos recebidos mantêm seus bytes. A decisão sobre a lista central de pedidos cabe ao responsável por ela.

## 3. Mudança por pedido e evidência própria

**Pedido 12 — atendido.** A 0.8.1 podia marcar como `unreadable` um job reparado após a leitura que havia falhado. A migração não obtinha `job:<id>` nem comparava revisão/ciphertext; a retenção fazia o isolamento depois de liberar a trava, atualizando apenas por bucket/chave.

`Queue::isolateUnreadable` agora centraliza o fluxo: obtém a trava individual, relê o registro, decodifica o ciphertext daquele mesmo snapshot e só executa o UPDATE se revisão e payload binário ainda coincidirem. `Store::decode` reaproveita as mesmas regras de decodificação de `Store::get`. Migração e retenção passam pela rotina; o worker já a chamava e recebe a mesma proteção. O CAS protege inclusive contra um gravador que não use a trava consultiva.

Registro legível, ausente ou já isolado é um no-op. Uma gravação concorrente faz o CAS não alterar linhas. Trava ocupada adia migração/retenção, sem alterar a projeção. Falhas SQL de leitura, releitura e UPDATE propagam `storage_unavailable`. Corrupção de JSON decifrado continua distinguida de indisponibilidade do banco. O isolamento muda apenas `queue_state`/`queue_next`, preservando ciphertext, revisão, datas e expiração. Na migração, um reparo que deixe a projeção pendente será examinado no próximo lote. Jobs antigos já isolados não são reativados automaticamente.

A reprodução usa WordPress e MySQL reais, outra conexão `mysqli`, travas nomeadas reais e interleavings controlados nas fronteiras SQL. No caso de migração, o gravador de reparo mantém deliberadamente a projeção vazia, como uma restauração/gravador legado, para provar a guarda de revisão/ciphertext independentemente da projeção atualizada por `Store::put`. Não se afirma que todo reparo pela API normal reproduz esse caso.

A primeira bateria, de dez verificações, reproduziu cinco falhas na 0.8.1. A bateria completa de 18 cobre também releitura legível, falha na releitura, JSON malformado/escalar, worker, liberação da trava reentrante e no-ops. Na 0.8.1 exata, 11 dessas 18 asserções não são atendidas; são asserções de um mesmo conjunto de proteção, não onze defeitos independentes. Na 0.9.0 todas passaram em cada cenário executado. Evidências: `baseline081/`, `baseline081-full/` e `request012.json` de cada cenário em `evidence/release090/`; código em `tests/native/request012-cases.php`.

| Cenário da 0.9.0 | Regressões aprovadas | Pedido 12 aprovado | Documentação MCP aprovada | Não aplicáveis | Falhas |
| --- | ---: | ---: | ---: | ---: | ---: |
| Limpa isolada — WP 7.1.3 / PHP 8.3.6 | 134 | 18 | — | 0 | 0 |
| Limpa integrada — quatro acompanhantes atuais | 166 | 18 | 26 | 0 | 0 |
| Atualização direta 0.8.1 → 0.9.0 integrada | 173 | 18 | 26 | 0 | 0 |
| Mínimo — WP 6.4 / PHP 8.1.2-1ubuntu2.28 | 132 | 18 | — | 2 | 0 |

Total da matriz: **729 verificações aprovadas, duas não aplicáveis e zero falhas**. As duas não aplicáveis no WP 6.4 dependem da Abilities API nativa ausente nessa versão. Cada conjunto documental local tem 25 documentos/hashs e uma verificação de ausência de acesso ao fornecedor, totalizando 26. Os testes com MySQL usam 8.0.46; PHP mínimo de 64 bits foi executado funcionalmente, não somente por lint. Downloads de runtime foram conferidos pelos hashes fixados nos manifests; a assinatura GPG de índices de distribuição não foi revalidada nesta rodada.

O builder validou sintaxe dos 28 PHP, gerou schemas e foi repetido em diretório limpo com instalador idêntico. Os schemas de entrada/saída e todos os assets JS/CSS são byte a byte iguais à 0.8.1. Não houve mudança visual; não foi repetida homologação visual em navegador. As regressões de administração, permissões, rotas REST/abilities, SDK, auditoria, fila e resultado filho foram executadas. Não houve Notice/Warning/Deprecated/Fatal/Parse atribuído ao pacote nas matrizes locais.

## 4. Instalação, documentação e prontidão

No Site-Teste `https://fator3-teste-mcp-1.dreamhosters.com/`, a instalação utilizou somente o ZIP final do LinkedIn, com `expected_sha256` e `expected_slug`. A operação `d786f35f36052fb84993d5b71b051c8e` aplicou 0.8.1 → 0.9.0, manteve o plugin ativo e guardou a pré-imagem `4bcbb324b293b80c8918b09b`. Sondas da página inicial e `/wp-json/` retornaram 200 antes/depois, em PHP novo e com bypass de cache verificado. A reativação foi silenciosa; o ciclo completo do hook de ativação não foi executado nesse upgrade remoto. A instalação limpa local executou a ativação normal.

WordPress remoto 7.1.3/PHP 8.3.36: 18 casos do pedido 12 passaram em tabela temporária exclusiva, com opções compartilhadas preservadas e zero tentativas HTTP. A tabela foi removida no `finally`. O auxiliar `qa-linkedin-090.php` foi removido e a ausência confirmada; o canal exigiu backup durável para sua remoção, que foi preservado. Nenhuma fixture ativa foi instalada no pacote. A conferência dos 59 arquivos locais instalados passou contra o manifest final, SHA-256 `71ecbdb1822c08ecb654f1d5b11ce8ecb96da490756367d742f3d9683062dec3`.

Após a limpeza: `linkedin/status` 0.9.0 com `state=ok`, `issues=[]`, armazenamento/criptografia prontos, auditoria saudável e `service_audit.central_registered=true`; nenhuma conexão, agenda ativa, migração pendente ou job ilegível. A manutenção permaneceu programada. O worker não estava requerido, portanto sem evento de worker é o estado correto. `linkedin/selftest`: oito verificações locais aprovadas, `remote_homologated=false`. Catálogo: **81 operações**, todas versão 0.9.0.

A documentação instalada foi descoberta e lida **integralmente pelo MCP remoto: 25 documentos em 32 páginas**, com `expected_revision`, continuação por `next_offset`, contagem de bytes, SHA-256 e igualdade com o instalador. Provas em `site-documentation.json`; os registros de operação/inventário/estado estão em `site-test.json`. As sondas comprovam resposta interna do site e não uma homologação externa de acesso público/comercial.

## 5. Banco, preservação e reversão

Schema SQL permanece **2**, sem DDL novo na release e sem novas opções ou concessões. O upgrade integrado da 0.8.1 comprovou preservação byte a byte dos registros cifrados, revisões, datas, retenção, projeção da fila, opções existentes e agenda supervisionada; os diários/grants CAPI existentes também foram preservados. O teste remoto operou apenas a tabela própria temporária, sem selecionar ou modificar registros comerciais compartilhados.

Faça backup de arquivos, banco e salts antes de distribuir. Restaurar a pré-imagem do instalador volta à 0.8.1 e reintroduz a corrida corrigida; não desfaz coletas, conversões ou outros efeitos de negócio. Os registros já marcados `unreadable` continuam conservados e não são reabertos automaticamente. A atualização validada nesta rodada é da base imediatamente anterior aceita, 0.8.1; saltos de versões mais antigas não foram rehomologados.

## 6. Pendências, responsáveis e credenciais

- **Responsável pela lista de pedidos:** registrar o aceite técnico do pedido 12 com este relatório; a aba recebida permanece intacta.
- **Dono/operador comercial:** continuam as pendências externas 20, 92 e 116 citadas na aba recebida: conexão preenchida pelo dono, diagnóstico real de credencial recusada, concessão/escopos aprovados e regra de conversão com fonte API, entrega efetiva e contagem/Registro de serviço. Não foram usadas credenciais comerciais, gastos Ads, publicações, assinaturas ou notificações reais nesta rodada.
- **Responsável pela frota:** decidir e executar a distribuição do instalador/relatório com os hashes finais. Não houve push, publicação em repositório, envio a outros mantenedores nem instalação nos outros onze sites. O fonte segue a decisão 89 do projeto.

O Site-Teste estava e permaneceu sem conexão LinkedIn configurada. Somente fixtures sintéticas foram usadas nos laboratórios; testes locais interceptam HTTP/e-mail. Segredos, salts, banco de laboratório e material privado não integram os artefatos entregues. A aprovação comercial depende das credenciais e produtos do titular e não é substituída por esses testes.

## 7. Artefatos e integridade

| Artefato | Nome final | Bytes | SHA-256 |
| --- | --- | ---: | --- |
| Instalador | `wp-mcp-linkedin-fator3-0.9.0-instalador.zip` | 236277 | `d4857927ebacfca9321b79d13bc15f15c6969ae67047fd1793e509524b7a60f8` |
| Fonte | `wp-mcp-linkedin-fator3-0.9.0-fonte.zip` | 1022685 | `26fc1c7573becdee2f904abffc04f20a6e5be63eb5e8e6f5b0e45d1c53701733` |

Relatório externo: `wp-mcp-linkedin-fator3-0.9.0-relatorio.md`. Encaminhamento próprio atualizado: `wp-mcp-linkedin-fator3-0.8.1-impacto-wp-mcp-meta-fator3.md`, revisão 2, resolvido pela resposta recebida.

O instalador tem raiz única `wp-mcp-linkedin-fator3/`, 59 arquivos, 28 PHP e 25 documentos. O fonte tem raiz única `wp-mcp-linkedin-fator3-0.9.0-fonte/`, código/build/testes/evidências/documentos e a cópia interna deste relatório. O runtime `plugin/` confere byte a byte com o instalador. Nenhum ZIP entregue contém outro ZIP. `artifact-checks.json` documenta schemas, assets, manifest, ausência de auxiliares no instalador e reprodução do build. O ZIP fonte foi fechado uma única vez; somente este relatório externo recebeu seus metadados finais.
