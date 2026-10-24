# Entrega — Fator3 MCP Google 0.19.0

23/10/2026 · Pedido MCP Google 36 · Implementação concluída; homologação com credenciais Google reais pendente.

**Relatório externo final.** O fonte contém uma cópia identificada como anterior ao fechamento; os hashes finais abaixo são os canônicos desta entrega.

## Bases aceitas

Base direta **0.18.1**. Instalador de referência: 799.626 bytes, SHA-256 `91c97cc300360511bc2477f5af9b0c2017e8b04861d015aaf0f0e5accd1cefef`. Fonte de referência: 4.177.792 bytes, SHA-256 `7b8dd2e3425bc1c4e0ddcbff51318069a98293d276e5b18564a603df8d0ab659`.

Considerados: `Fator3 MCP Google(8).md` (situação de 23/10/2026, item 36), instruções comuns e padrão de desenvolvimento revisão 4, pacotes/fontes/relatórios Core 1.49.1, MCP 0.29.1, Meta 0.8.0 e LinkedIn 0.9.0, e impacto MCP 0.29.1 → Google, revisão 2. As evidências recebidas orientaram a revisão; os testes abaixo são próprios desta rodada. A versão minor segue a regra comum e não altera as identidades publicadas.

## Convivência e encaminhamentos

| Pacote | Versão testada | SHA-256 do instalador |
|---|---|---|
| core | 1.49.1 | `4ad3be4159310578a2db47cf179d02fa061fb98021e2f66ca933b59e7db4fb40` |
| mcp | 0.29.1 | `1b627aec5c24dc88f52eaf6a0d34367437d7f9e7b599f9f07850567fd57610e6` |
| meta | 0.8.0 | `36e4e098955576c3d43ea1b1bd2c14fe68608472b8666a652e84da5165ce25e1` |
| linkedin | 0.9.0 | `d4857927ebacfca9321b79d13bc15f15c6969ae67047fd1793e509524b7a60f8` |

**Não houve modificação do Core nem dos outros acompanhantes.** A preservação das comprovações é implementada no Google. Permanecem o leitor `search-console-reader/1.0.0`, o adaptador `site-conversion-delivery/1.0.0`, a configuração 4.0.0 e os contratos de execução/armazenamento 2.0.0.

O impacto recebido está resolvido no MCP: `retryable` sozinho não prova ausência de efeito. O Google não passou a emitir `applied=false` por suposição; as recusas da nova validação preservam a credencial e não alegam ausência de registros técnicos da chamada. O teste nativo confirma a regra conservadora no MCP 0.29.1. Não há adaptação obrigatória, ordem conjunta de atualização ou novo impacto técnico identificado nas fronteiras examinadas. Por isso, esta entrega não inclui documentos de simples aviso de versão. Nenhuma mensagem foi enviada a mantenedores e nenhum trabalho alheio é declarado concluído.

## Mudanças por pedido e evidência

O item 36 foi implementado nos cinco pontos:

1. **Campos e orientação.** Rótulos e ajudas em português usam os nomes do Google. Nome editável também em `default`, mantendo seu ID e o placeholder solicitado. JSON exige os campos e formatos definidos no pedido; `web`/`installed` são recusados com a mensagem solicitada. MCC aceita dez dígitos com ou sem hífens; developer token exige 22 caracteres permitidos; Client ID/secret OAuth são validados; delegação aceita vazio ou e-mail.
2. **Conferência antes de gravar.** A chave submetida assina JWT e obtém um token novo antes de persistir a candidata ou chave ativa. O cache de uma chave anterior não substitui essa prova. Ativar a candidata repete a validação. Novo developer token passa por `customers:listAccessibleCustomers` antes de salvar. Falhas preservam o segredo anterior; conflitos de revisão e falhas de persistência usam o mecanismo verificado de rollback. A mensagem `invalid_grant` não afirma revogação como causa única.
3. **Resumo da conexão.** Conta salva, projeto, últimos oito caracteres da chave, autenticação, último acesso a recurso/serviços e aceite do developer token com contexto MCC. Nunca mostra chave privada, access token ou developer token. O comprovante acompanha a credencial/configuração; não se transforma em garantia permanente de acesso. Observações de acesso usam cache de até 30 dias e não revogam concessões ao expirar.
4. **Outra conta.** Candidata de outro `client_email` exige simulação e confirmação explícita. A lista mostra os resultados dos recursos vinculados; revisão e hash são vinculados também à conexão e ao administrador. A confirmação revalida autenticação e recursos. Serviços/recursos continuam selecionados; verificações da identidade antiga não autorizam a nova.
5. **Rotação da mesma identidade.** Preserva grants de consumidor Search Console do Core, referências e validade das comprovações de conversão, revisão de execução e fila. A troca não amplia validade, não cria prova e não muda cursores. O principal estável inclui e-mail, projeto, client_id e delegação; mudar esses dados não recebe preservação automática. Histórico limitado às últimas vinte rotações, com data, administrador e sufixos.

Três habilidades administrativas novas: `google/rename-connection`, `google/plan-identity-change` e `google/switch-identity`. Catálogo final: **290 habilidades (112 leitura, 178 escrita), 37 opções**. Os esquemas de entrada/saída e efeitos das 287 habilidades anteriores são idênticos aos da 0.18.1 com o mesmo MCP 0.29.1. O catálogo nativo de referência é fixado pelos hashes dos pacotes; a decoração do MCP não é confundida com uma mudança do Google.

Diferença do instalador: **um arquivo novo, dezesseis alterados, nenhum removido**; novo validador `includes/Auth/Validation.php`. O fonte também inclui testes, guia corrente, contratos regenerados, plano e reprodução. `runtime-diff-0181.json` e `source-diff-0181.json` detalham os arquivos.

## Instalação, prontidão e provas

Instalar o ZIP de instalador sobre a **0.18.1**, sem desinstalar. Mínimos comprovados: WordPress **7.1.2** e PHP **8.3.6**. Laboratórios com MySQL **8.0.46** e WordPress 7.1.2/7.1.3; site real com WordPress 7.1.3/PHP 8.3.36. O fonte não é o ZIP de instalação.

| Cenário nativo | WordPress | Verificações | Resultado |
|---|---|---:|---|
| clean | 7.1.2 | 1479 | aprovado |
| clean-713 | 7.1.3 | 1386 | aprovado |
| upgrade | 7.1.3 | 1410 | aprovado |
| google-first | 7.1.2 | 86 | aprovado |
| isolated | 7.1.2 | 82 | aprovado |

Total: **4.443 verificações nativas**, zero falhas. Clean e clean-713 integram Core/MCP; upgrade inclui também Meta/LinkedIn atuais; google-first inverte a ordem de ativação; isolated executa somente Google, inclusive prontidão por WP-CLI. O cenário upgrade aplica via MCP HTTP autenticado, exercita rollback e reaplica a versão, preservando configuração, segredos cifrados, filas, registros e dados sociais de fixture. O inventário final dos arquivos dos acompanhantes foi conferido contra seus instaladores. Todos os processos de laboratório foram encerrados.

Adicionalmente: **1.169 testes PHPUnit / 14.384 asserções**, 60 verificações de contratos auxiliares, lint de **156 arquivos PHP** (160 arquivos no instalador), documentação/geradores consistentes e **18 verificações DOM/interação** via jsdom 27.4.0. O gate contabiliza a execução DOM como uma verificação; o arquivo de detalhes registra suas dezoito verificações, sem inflar o total nativo. A análise documental percorreu 39 documentos de trabalho e 147 links locais. Os resultados finais são `evidence/019/validation019.json`, `unit.xml` e seus relatórios associados.

Os testes de credenciais cobrem JSON OAuth no campo errado, formato inválido, `invalid_grant` simulado, tentativa de usar cache antigo, candidata revogada entre preparo e ativação, corrida de revisão, persistência/rollback, recusa de não administrador, identidade sem acesso, plano adulterado, rotação com grants/provas/fila e developer token recusado. As falhas preliminares de fixtures/ambiente e seus ajustes estão registradas em `preliminary-observations.json`; não são contadas como aprovação.

### Site-Teste

Atualização aplicada via MCP em `https://fator3-teste-mcp-1.dreamhosters.com/`: **0.18.1 → 0.19.0**, ativa, `applied=true`, com SHA-256 idêntico ao candidato validado. Operação `84b890542449e41af6156c5d`; operação de pacote `1797c39875d0c8c0ac6dac7ba03ebba3`; backup do pacote anterior `5a95108b15f82670a09f4084`.

As sondas de `/` e `/wp-json/` passaram com HTTP 200 antes e depois. `system/health` retornou saudável, onze verificações aprovadas. A reativação foi silenciosa; não é prova de ciclo completo do hook de ativação nem de prontidão comercial. Core 1.49.1, MCP 0.29.1, Meta 0.8.0 e LinkedIn 0.9.0 continuam ativos nas mesmas versões. As três novas habilidades foram descobertas com versão 0.19.0.

Prontidão final: **blocked / f3_google_not_configured**, igual à situação inicial por ausência de credencial. Armazenamento, recuperação, executor, incidentes e Core: `ok`; destinos GA4/Ads: `not_configured / destination_not_selected`. Não houve mudança de configuração comercial, gasto de anúncio, publicação ou envio a clientes. Não houve distribuição à frota nem push público.

Documentação instalada lida integralmente por `google/documentation`: **20 documentos, 74 páginas, 3.811.026 bytes**, comparação exata de conteúdo, offsets, revisões e tamanhos contra a documentação embutida no instalador. A leitura usa `expected_revision` em cada continuação. O gate local também verifica autorização administrativa, allowlist e leitura sem chamadas externas. Evidência remota sanitizada em `site-teste019.json`.

## Banco e reversão

Não há nova tabela, migração destrutiva nem migração no esquema de banco de outro plugin. A opção protegida `f3_mcp_google_credential_receipts` registra comprovações/histórico por conexão; o nome fica no registro existente de conexões. A rotação atualiza as revisões das provas existentes junto da chave em uma gravação protegida pela revisão/rollback. Nenhum prazo de prova é estendido.

Rollback de arquivos foi testado localmente com o pacote anterior. Não desfaz gravações ou efeitos já ocorridos. Voltar à 0.18.1 remove as novas validações e o fluxo guiado; futuras rotações feitas nela podem exigir nova verificação de destinos. No Site-Teste o backup da operação ficou disponível, sem rollback remoto porque a instalação e a conferência passaram. Não apagar/desinstalar o plugin para reverter; não restaurar banco compartilhado por inteiro.

## Pendências e responsáveis

- **Dono/operador das credenciais Google:** fornecer ambiente e chaves de teste autorizadas e executar o aceite real 36(a–f), sobretudo chave realmente revogada, troca de conta e rotação com recursos reais. O Site-Teste não tinha credencial; HTTP Google foi interceptado nos laboratórios. A implementação está entregue, mas a homologação com o fornecedor não está concluída.
- **Responsável pela revisão central:** fechar editorialmente o pedido após o aceite. O documento central e os impactos de terceiros não foram alterados.
- **Responsável pela distribuição:** decidir a publicação e implantação na frota. Esta rodada atualizou somente o Site-Teste.

Não foi feita inspeção visual completa em navegador; HTML e interação DOM foram testados. Ausência de achados nos cenários executados não garante ausência de todo impacto em contas comerciais ou combinações não testadas.

## Credenciais, sem valores secretos

Não foi recebida nem criada credencial Google real. Chaves RSA e respostas HTTP dos ensaios são descartáveis/sintéticas. Nenhum banco de laboratório, cookie, token de sessão ou chave privada gerada em execução integra a entrega. Segredos de configuração permanecem cifrados pelo mecanismo existente; resumo/histórico exibem apenas metadados. Guardas de capacidade e nonce/revisão são aplicadas no servidor; o transporte MCP exige suas permissões próprias.

## Arquivos finais e identidade

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| `wp-mcp-google-fator3-0.19.0-instalador.zip` | 809436 | `d15868915e3fdf886d7e883a82d9d302df7242808fc94d45bf3e1857234759d1` |
| `wp-mcp-google-fator3-0.19.0-fonte.zip` | 4462572 | `0d90b1a0dbc186a9e0b2adf66843dad4abd928fb2c616a56442213597b0eefb2` |

Relatório: `wp-mcp-google-fator3-0.19.0-relatorio.md`. Instalador com raiz `wp-mcp-google-fator3/`; fonte com raiz `wp-mcp-google-fator3-0.19.0-fonte/`, código integral, testes, evidências sanitizadas, documentos e scripts de reprodução. Nenhum ZIP contém ZIP aninhado. A cópia interna é anterior ao fechamento; o hash final do fonte consta apenas do relatório externo, evitando circularidade.
