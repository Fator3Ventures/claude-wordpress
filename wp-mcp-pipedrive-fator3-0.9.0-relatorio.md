# Entrega — Fator3 MCP Pipedrive 0.9.0

Revisão 1 da entrega · 10/11/2026 · Implementação do plano, testes e atualização do Site-Teste  
Slug: `wp-mcp-pipedrive-fator3` · Base 0.8.0 → versão 0.9.0 · **Status: com-pendencias**  
A versão está ativa e saudável no Site-Teste. O código e a integração estão validados no escopo abaixo. O aceite comercial do **Pedidos MCP Pipedrive 11** em korvena.com.br continua aberto.

## 1. De onde esta versão entra

Instalação limpa em site único ou atualização direta da 0.8.0. Base oficial recebida do dono: instalador de 122.083 bytes, SHA-256 `89e41f2f7a2124eb1a5961fe06d6aff60fd168b8d6dd2ea1b21a272772ff7f30`; fonte de 507.256 bytes, SHA-256 `b4ae837c77c84c4e31a21b5a34b9f5d479189e10e02508026e4b41c2e74cc93b`. Os 36 arquivos do runtime de origem foram conferidos. O plano aprovado, o parecer que fixa as decisões de implementação e os dois documentos normativos, ambos na revisão 5 de 02/11/2026, estão em `inputs/` no fonte.

Requisitos: WordPress 7.1.4+, PHP 8.3+ de 64 bits, OpenSSL com AES-256-GCM, mbstring e tabelas InnoDB. Bancada efetiva: WordPress 7.1.4, PHP 8.3.6, MySQL 8.0.46 e Chromium 156.0.8078.79. O mínimo do WordPress e o ramo 8.3 do PHP foram exercitados; não se certificaram todas as versões de correção nem todos os bancos compatíveis.

## 2. Convivência e encaminhamentos

Conjunto final: Site Core **1.78.0**, MCP **0.43.0**, Google **0.31.0**, Meta **0.21.0** e LinkedIn **0.20.0**. Os cinco instaladores e suas árvores estão identificados em `evidence/090/companion-installers.json`. O LinkedIn passou de 0.19.0 para 0.20.0 durante a rodada: a matriz de 90 verificações foi repetida integralmente; a anterior ficou apenas no histórico. Google, Meta e LinkedIn coexistem e não fornecem contratos usados pela cadência. Nenhuma ação foi solicitada a seus mantenedores.

| Destinatário | Classificação e situação | Decisão e documento vigente |
|---|---|---|
| Site Core 1.78.0 | Validação coordenada; resolvido no escopo técnico | Mantidos autorização, orçamento, limites e trava do transporte. [Impacto, rev. 2](wp-mcp-pipedrive-fator3-0.9.0-impacto-base-site-core-fator3.md). |
| MCP 0.43.0 | Validação coordenada; resolvido no escopo técnico | Nomes e efeitos publicados; perfis personalizados exigem concessão do administrador quando aplicável. [Impacto, rev. 2](wp-mcp-pipedrive-fator3-0.9.0-impacto-wp-mcp-fator3.md). |

Sem ticket, alteração de código ou ciclo de instalação obrigatório em nenhum destinatário. A comparação integrada usa o transporte do Core e o executor do MCP originais com respostas de fornecedor sintéticas.

## 3. Mudanças e evidência

| Pedido ou item do plano | Comportamento entregue | Evidência no fonte, em evidence/090 |
|---|---|---|
| P0 · Escrita com desfecho incerto | Se a escrita foi despachada e o Core devolve 2xx ilegível, excessivo ou inconsistente, ou outro resultado ambíguo, a entidade continua bloqueada, com recibo. A repetição não reenvia; uma recusa definitiva, como 422 confirmado, tem tratamento distinto. | nativo-clean/escritas090, restart090 e nativo-matrix/core-workflows. Processos novos leram os marcadores persistidos. |
| P1 · Fila e simulação | A fila retorna até 200 itens por página, com cursor vinculado ao contexto e cobertura explícita. Uma página sem devidos pode ter continuação. Leituras incompletas não equivalem a conta vazia. A simulação de regras usa até 20 leads verificados e exige confirmação para salvar. | nativo-clean/fila090. Em massa esparsa, 201 leads: 2 páginas/4 GET; 1.000: 5 páginas/10 GET. Em 200 leads e 5.000 atividades: 11 GET e 220 unidades observadas. Medições sintéticas, sem extrapolação para a conta real. |
| P2 · Recuperação | Consultar pendências, obter prévia e confirmar resolução por operação administrativa. A conta, o ator, a intenção e as evidências precisam corresponder. A decisão concilia progresso, auditoria e liberação em uma transação local. Preserva o recibo original. Evidência insuficiente mantém o bloqueio. | nativo-clean/recuperacao090, policy090 e nativo-matrix/integrated. Falha induzida na auditoria não deixou a entidade parcialmente liberada. |
| P3 · Retenção e concorrência | A trava de retenção protege política e limpeza; não atravessa o HTTP. A entidade e a revisão continuam protegidas. Operações compostas também acionam a limpeza oportunista limitada; recibo em execução ou com pendência não expira por essa limpeza. | nativo-clean/travas090 e mutacoes-fila-retencao. Em processos distintos, o segundo lead prosseguiu e o mesmo lead ficou bloqueado. O Core ainda pode recusar contenção no transporte. |
| P4 · Configuração guiada | WhatsApp, horários, toques e textos são editáveis sem JSON. A tela separa regras avançadas, revisão antes/depois e consentimento; informa horário, custo e estado. Após simular, atualizar a página ou reenviar o mesmo POST não cria outra prévia. No MCP e REST, a frase de confirmação continua exigida. | browser090 e nativo-clean/painel090: WordPress real, também a 390 px e sem JavaScript. |
| P5 e P7 · Ajuda e documentação | Ajuda com links permitidos e guias longos formatados por seção. Dez guias e dois JSON acompanham o runtime; explicam permissões, limites, recuperação, cobertura e regras. | nativo-clean/doc090 e site-documentos. O ensaio documental detectou os oito defeitos plantados; as cópias servidas pelo MCP têm os mesmos bytes do pacote. |
| P6 · Build e testes | Catálogo fechado com 22 operações, 11 de leitura e 11 de escrita. Schemas gerados do código; reprodução exata do ZIP instalável; suíte de política, mutações e conferência de build. | verificacao-final, site-catalogo e mutacoes-contratos. Os antigos mutantes m13/m14 referiam-se a linhas substituídas: seus equivalentes testam perda da continuação e supressão ou alcance incorreto do mutex. |
| Pedidos MCP Pipedrive 11 | Preservada a correção da 0.8.0: nota sem marcador visível, progresso local, participante principal conforme a pessoa do lead e idempotência da operação. Não foi criado um novo número de pedido para o plano de manutenção. | nativo-clean/requests080 e nativo-matrix/core-workflows. Implementado e validado em WordPress com fornecedor sintético. Aceite em conta real pendente. |

Não foram introduzidos cron, callback público nem transporte próprio ao fornecedor. A paginação de leads não congela a conta em uma fotografia: alterações concorrentes podem exigir reinício; a sobreposição detecta mudanças de fronteira observáveis. A simulação de até 20 leads é uma amostra identificada.

## 4. Instalação e prova da troca

No Site-Teste, o instalador da seção 8 foi submetido a `plugins/upload-base64` com `expected_slug=wp-mcp-pipedrive-fator3`, `expected_sha256` igual ao hash abaixo, substituição e ativação. Recibo `3bca5fb9f0161c70209a0259b0069157`; backup de arquivos `07ea1df2474c7bc52d72f6dc`. A ferramenta confirmou 0.8.0 ativa → 0.9.0 ativa e verificou a ativação em novo processo PHP. Usou reativação silenciosa; o gancho de ativação completo não rodou nessa troca. O banco já tinha schema 1; a criação do schema em instalação limpa foi testada separadamente.

| Ambiente | Prova | Resultado observado |
|---|---|---|
| WordPress limpo | Instalação nativa, operações, políticas e documentação | 591 verificações funcionais aprovadas, nenhuma falha. |
| WordPress com a base 0.8.0 | Atualização nativa do ZIP, dados e replay após novo processo | 17 aprovadas, nenhuma falha. |
| WordPress e cinco acompanhantes | Executor MCP, cliente Core, fluxos e relatório | 90 aprovadas, nenhuma falha. |
| Chromium com wp-admin local | Cadastro guiado, consentimento, envio repetido, navegação estreita e sem JS | 29 aprovadas, nenhuma falha. **Total funcional: 727** (698 WP/PHP + 29 navegador). Mutações, lint e sondas remotas não entram nesse total. |
| Site-Teste compartilhado | `pipedrive/configuracao-ler {}`, `pipedrive/retencao-ler {}`, `pipedrive/status {}`, `pipedrive/pendencias-ler {}` | Regras e retenção preservadas. As últimas duas recusaram com `operacao_nao_autorizada`, de acordo com a concessão anterior no Core. |
| Site-Teste compartilhado | Catálogo, documentação, arquivos e saúde | 22 operações descobertas. Os 12 documentos lidos de ponta a ponta por MCP e os outros 28 arquivos por hash coincidem com o instalador. WordPress saudável; GET em / e /wp-json/ retornou 200 antes e depois. |

Para conferir a ajuda: descubra `pipedrive/documentacao-ler`, chame `{}` ou `{"documento":"uso","limite_bytes":16000}`; enquanto `fim=false`, envie `offset=proximo_offset` e `sha256_esperado` do documento. A conferência usou a lista fechada do instalador, inclusive schemas e regras iniciais. Para repetir a bancada: `tests/README.md`. O site compartilhado ficou sem fixtures, controlador de teste nem operações de CRM criadas.

A distribuição da frota é separada desta instalação: URL prevista `https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-pipedrive-fator3-0.9.0-instalador.zip`. Não houve publicação nem validação dos bytes nessa URL nesta rodada. Antes de instalar pela frota, confrontar os bytes servidos com o SHA-256 do relatório e usar `plugins/upload` com hash e slug esperados.

## 5. Banco, migração e correção por nova versão

Schema 1 preservado. As tabelas próprias guardam operações/prévias/progresso e diário. As opções guardam regras, retenção, versão do schema, marcadores por entidade e estado temporário de limpeza/formulário. O conteúdo sensível de recibos e do progresso depende dos salts existentes do WordPress. Preserve as duas tabelas, as opções próprias, os salts e a configuração do Core antes da troca. O backup do instalador cobre arquivos, não restaura efeitos no CRM.

No Site-Teste, a cópia anterior das opções foi conferida com a leitura posterior, inclusive valores e autoload. A revisão das regras permaneceu idêntica. As tabelas de operações e diário estavam e continuaram com zero linhas. Na bancada, a base tinha regras, progresso, recibo, pendência, diário e retenção deliberadamente preenchidos; foram preservados e conferidos em novo processo. Marcadores legados sem prova de intenção suficiente continuam bloqueados. Se uma aplicação comercial for incerta, consultar o caso e a evidência antes de qualquer nova operação. Uma falha após instalação exige **nova versão corretiva**; não há migração reversa prevista.

## 6. O que permanece pendente

- **SDR | Pipedrive / dono da conta — Pedidos MCP Pipedrive 11:** em korvena.com.br, criar um lead de teste com pessoa, registrar WhatsApp, conferir no Pipedrive participante principal e nota sem marcador, repetir com a mesma chave para verificar que o recibo retorna sem segunda atividade, e remover os dados de teste. Nenhuma alteração foi feita na produção.
- **Dono da conta / frota:** medir volume, custo e tempo na conta autorizada antes de dimensionar o uso operacional. O Site-Teste permaneceu sem concessão comercial. O fornecedor, seu limite real e o tempo de rede não foram homologados nesta rodada.
- **Frota, na distribuição:** publicar apenas os artefatos autorizados, verificar o raw e as concessões dos perfis que usarão recuperação. O wp-admin em navegador foi exercitado na bancada, não no navegador autenticado do Site-Teste. MySQL 8.4 e todas as variantes de runtime não foram exercitados.

## 7. Credenciais e configuração do dono

No **Fator3 Site Core**, usar a tela de credencial Pipedrive para configurar o token da conta (`f3base_pipedrive_token`). Conferir domínio, identidade da conta e usuário; habilitar `f3base_pipedrive_operacao.ativo` e conceder o consumidor `wp-mcp-pipedrive-fator3` somente no site autorizado. Na conexão MCP, o administrador escolhe as operações explícitas. Leitura do catálogo não concede autorização de escrita. No WordPress, a configuração de regras fica em **Ferramentas → Fator3 MCP Pipedrive**; a ajuda e a retenção local são acessíveis ao administrador mesmo sem concessão comercial.

## 8. Identidade dos arquivos

| Artefato | Nome final e link | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-pipedrive-fator3-0.9.0-instalador.zip](wp-mcp-pipedrive-fator3-0.9.0-instalador.zip) | 452473 | `42523b9b547fc8820c3917e192c4b48341efbb1da6815c78fcc18f8a373c09c0` |
| Fonte | [wp-mcp-pipedrive-fator3-0.9.0-fonte.zip](wp-mcp-pipedrive-fator3-0.9.0-fonte.zip) | 419738 | `f64f79e648e150edc8c31e102d71ed23d591413ab04446e75240790f8f66cc78` |

**Relatório externo canônico, finalizado após empacotar o fonte.** O fonte inclui o runtime exato, scripts e casos reproduzíveis, documentação, insumos de planejamento, impactos e evidências sanitizadas. Os dois ZIPs têm raiz própria e não contêm outros ZIPs. O instalador usa armazenamento sem compressão para ser byte a byte reproduzível entre versões de zlib; o ZIP do fonte usa deflate. O relatório externo e os dois impactos são destinados ao dono e à frota conforme suas competências.
