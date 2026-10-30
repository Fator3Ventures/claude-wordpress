# Entrega — Fator3 MCP Pipedrive 0.5.0

Revisão 1 · 30/10/2026, America/Sao_Paulo · Rodada de implementação.
Slug/basename: `wp-mcp-pipedrive-fator3/wp-mcp-pipedrive-fator3.php`.
**Implementada, instalada e ativa no Site-Teste. Status: com-pendencias de configuração e aceite no fornecedor real.** Pedido MCP Pipedrive10. Nenhuma implantação em sites-porta ou publicação no repositório realizada.

## 1. De onde esta versão entra

Instalação limpa e atualização direta **0.4.0 → 0.5.0**, sem intermediária. Base exata: instalador84775 bytes/SHA-256 `70100900ebd7b358e96c9778eaa359aeb454203f759136da380adcb853b383fe`; fonte297237 bytes/SHA-256 `1484739a125a4f349fcef68e84e34137ef262822359f900af14d4200c97e32d6`. Recuperados pela identidade da entrega anterior; os hashes e a versão instalada0.4.0 foram conferidos.

Entrada funcional: `Fator3 MCP Pipedrive(4).md`, pedido 10 de30/10. Considerados os novos fontes, instaladores e relatórios Core1.62.0, MCP0.37.0, Google0.24.0 e Meta0.16.0. Identidades completas em inputs050/manifesto.json. LinkedIn0.13.0 foi observado e copiado do Site-Teste para a bancada; nenhum novo ZIP LinkedIn foi recebido.

Instruções/padrão atuais r4 foram lidos integralmente e comparados à r5 preservada na base. A diferença pertinente da r5 limita arquivos de impacto a consequências/pedidos e mantém respostas no relatório principal. Não houve novo encaminhamento técnico nesta rodada, portanto não há conflito operacional entre essas orientações. Plano anterior à implementação: PLANO-0.5.0.md.

Mínimos preservados: **WordPress7.1.3/PHP8.3.36, 64 bits, OpenSSL, site único, InnoDB**. Testes remotos em WP7.1.4 e backend WP7.1.3, ambos PHP8.3.36/MySQL8.4.11. O mínimo usa arquivos de backend WordPress7.1.3 em instalação descartável, sem assets/UI: não é prova visual. Lint local PHP8.3.6 é separado desses testes funcionais.

## 2. Convivência e encaminhamentos

| Acompanhante | Versão testada | Fronteira efetivamente exercitada |
| --- | --- | --- |
| Core | 1.62.0 | Cliente público original pipedrive-api-client/1.0.0, codificação HTTP, orçamento, recibos, recusa e registro; respostas de fornecedor sintéticas. |
| MCP | 0.37.0 | Descoberta, executor original, perfil/permissões, redação, documentação e instalação remota. |
| Google | 0.24.0 | Ativação e convivência, sem homologação das APIs Google. |
| Meta | 0.16.0 | Ativação e convivência, sem homologação Graph. |
| LinkedIn | 0.13.0 | Ativação e convivência da cópia instalada, sem homologação LinkedIn. |

A bancada congelou cópias dos acompanhantes antes dos testes. Nenhum acompanhante compartilhado foi instalado, alterado ou reconfigurado. Inventário final preservou essas cinco versões ativas. A prova de convivência não certifica todas as funcionalidades desses pacotes.

**Impactos emitidos: nenhum.** Foram avaliados transporte/orçamento Core, registro/autorização MCP, schema aditivo das regras Pipedrive e convivência dos acompanhantes. Não foi identificada adaptação a solicitar a outro pacote. Google/Meta relataram mudanças documentais nas fronteiras pertinentes; Core1.62.0 preserva o cliente público consumido. Os resultados recebidos não foram contados como provas próprias. Não há nova ordem de troca ou dependência artificial.

O pedido informa0.4.0 instalada pela frota nos sites-porta e regras comerciais salvas em korvena.com.br. Esse é histórico recebido. A rodada atual atende o código do item10; o aceite final dessa conta permanece com o dono/frota. Nenhum item foi fechado no documento central nem mensagem enviada a outro responsável.

## 3. Mudanças e evidência

| Pedido 10 | Resultado implementado | Prova e limite |
| --- | --- | --- |
| (1) WhatsApp400/idempotência | Criação/atualização v2 mantém nota+done e envia due_time UTC em HH:MM. Chaves permanentes e recibos preservados; nota vazia/null aceita, sem linha duplicada no replay. | Fixture estrita recusa segundos e aprova POST/PATCH200; integração pelo cliente/encoder original Core passou. A diferença do prazo é a hipótese técnica tratada; não se afirma causa confirmada nem HTTP200 no fornecedor real. |
| (2) Auditoria de etapa | stage_change_time nulo/ausente usa add_time. Sem ambas datas, identifica o item em itens_nao_avaliados e continua; avaliacao_completa distingue qualidade dos dados de coleta_completa. | Fixture de6415 por add_time, item6416 sem data e6417 depois dele; coleta completa, avaliação parcial e continuação comprovadas. IDs foram usados em dados inteiramente sintéticos. |
| (2) Nome de pessoa na organização | Regra opcional com palavras de empresa, partículas ignoradas e mínimo de tokens; compara nome/sobrenome de todas as pessoas visíveis ligadas, inclusive pessoa diferente do contato do lead. | Organização4891 sintética com pessoa ligada9663 diferente de9662; inclusões/exclusões e ausência de nomes na saída passaram. Regra comercial precisa ser configurada na conta. |
| (3) Nota final | Prefixo, formato fechado e autor configuráveis; data local no fuso IANA. Padrão: [IA] 29/10 13h36, nós: mensagem. HTML escapado; marcador autenticado preservado. | Conversão UTC→São Paulo, escape, formato alternativo e lead-encerrar via operação pública aprovados. |
| (4) Prazos/calendário | Minutos úteis a partir da entrada, sem arredondar a período; feriados por data; primeiro período do próximo dia útil, sem aproximação por360 minutos. | Entrada10h vence11h; sexta17h30 com segunda feriado vence terça09h30; feriado sem item devido. |
| (4) Textos/variáveis | Variantes ordenadas por condição de campo, texto-base de fallback, mapa explícito de variáveis e primeiro_nome. Falta de dado impede texto/devido. | Três seleções de texto, preenchimento e campo ausente passaram; texto não é executado. Campos são do lead, raiz/custom_fields; não há busca implícita de nomes em pessoas. |
| (4) Canais/entrega | Restrições cumulativas de encerramento/arquivo; espera com revisão/limite configuráveis, exemplo30/1680 minutos corridos. | Fila, encerramento e arquivo genérico recusam canal protegido; revisão aos30min e limite28h, com calendário e falta de instante, passaram. Estado de entrega vem de campo operado externamente, não de integração WhatsApp. |
| (4) Adoção | Opt-in de última linha de saída datada por prefixo/autor, mapa de trecho→toque ou etiqueta; janela de idade e data de entrada; marcador autenticado tem preferência. | Nota válida reconhecida; autor de cliente, data inválida, texto novo desconhecido e configuração ausente não avançam. Sem escrita de adoção na leitura. |

Todos os recursos usam a configuração versionada `f3_pipedrive_operation_rules`, com simulação, revisão/CAS e frase de ordem do dono. Campos novos são opcionais; a atualização não preenche valores da conta nem regrava regras antigas. Sem token, transporte HTTP, cron ou envio de WhatsApp próprios. Permanecem19 operações, permissões administrativas, contrato1.0.0, identidades e duas tabelas/schema1.

Calendário limitado a dez anos de busca, listas/valores limitados pelo schema, texto final até16KiB, coleta até12000 registros. Histórico ambíguo/faltante não é adivinhado. A fila pode retornar dados pessoais somente dentro do texto explicitamente interpolado; não copiar esse texto para logs/evidências públicas. Auditoria e relatório agregado continuam retornando códigos/IDs sem nomes. Paginação parcial ou mudança de contexto bloqueia a indicação de ação devida, inclusive na revalidação final.

## 4. Instalação e prova da troca

**626 verificações aprovadas**, contabilizando somente o resultado final de cada suíte, com repetições entre ambientes:

| Ambiente/cenário | Verificações |
| --- | ---: |
| WP7.1.4/PHP8.3.36: native, report, retention | 89 +49 +33 |
| Mesmo ambiente: regressões0.4 e Pedido 10 | 56 +48 |
| Mesmo ambiente: MCP/convivência e cliente Core original | 41 +8 +6 +7 |
| Atualização direta0.4→0.5 e reinício | 12 +2 |
| WP7.1.3/PHP8.3.36: native, report, retention, regressões0.4, Pedido 10 | 89 +49 +33 +56 +48 |

São verificações funcionais/documentais/permissões, não626 casos comerciais independentes. Fornecedor/credenciais são sintéticos; HTTP externo e e-mail bloqueados nas bancadas. Testes incluem falta de administrador, concorrência, revisão/estado alterado, idempotência, duplicidade, erro/timeout, retenção e paginação. Zero avisos/fatais atribuídos aos arquivos Pipedrive nos diagnósticos das bancadas; não se afirma ausência de logs de todos os acompanhantes.

Um teste herdado do Core esperava09:30:00; foi ajustado para09:30 e reexecutado com chave de fixture nova, passando7/7. Nenhuma mudança no runtime foi feita para esse ajuste. No fechamento, foram corrigidos metadado de versão do schema e referências antigas de base/rollback na documentação. O código PHP funcional permaneceu idêntico ao testado; o pacote final passou por instalação/atualização, leitura integral novamente e comparação dos manifestos.

Provas adicionais: **67 gates de pacote, incluindo36 lints PHP**; **13 verificações documentais finais no mínimo**; **19 comparações compartilhadas**. Esses contadores são separados das626. Scripts e evidências em build/, tests/ e evidence/.

**Site-Teste:** https://fator3-teste-mcp-1.dreamhosters.com/, conector WP MCP fator3-teste. `plugins/upload-base64` com activate/overwrite true, expected_slug, expected_sha256 da seção 8 e chave idempotente. Operação **0da87b951fc66531aca103d189e796a6**, backup **cac7ffd72afbf2ae420bb0bc**. Estado applied;0.4.0→0.5.0 ativa. Reativação silenciosa confirmada em requisição PHP independente; não se declara execução integral do activation hook nem prontidão comercial.

Sondas internas de `/` e `/wp-json/`: HTTP200 antes/depois, sem cache; não são prova externa de CDN/navegador. Os31 arquivos instalados coincidem byte a byte com o ZIP. Tabelas próprias continuam com zero linhas; hashes de retenção, regras brutas, schema e autorização Core permanecem iguais ao estado anterior. Operação comercial Core continua **operacao_nao_autorizada**, como antes; nenhum acesso ao fornecedor foi habilitado.

**Documentação:**11 documentos pelo executor MCP original em61 páginas na bancada, conteúdo/hash conferidos. No Site-Teste, os mesmos11 documentos foram lidos integralmente pelo transporte conectado em13 páginas; versão0.5.0, fim, tamanho/hash e conteúdo iguais ao instalador. Schema e catálogo reais conferidos. Descoberta final:19 operações Pipedrive0.5.0 e zero QA próprio.

**Limpeza:** current101 tabelas, upgrade14, mínimo14 removidas —129 tabelas próprias, zero restantes e três diretórios removidos. Dois controladores e dois ZIPs temporários próprios excluídos com guarda de hash. Backups/auditoria nativos mantidos. Saúde final healthy=true, recovery.unresolved=0; histórico cron de24h tem contagens incompletas e dois incidentes confirmados preexistentes, sem alegar ausência global de incidentes.

## 5. Banco e volta de versão

Nenhuma tabela/coluna/migração nova. Opções, schema, retenção e recibos não são regravados na atualização. A prova de upgrade semeou três operações done/ready/running, duas linhas de diário, configuração0.4.0 com revisão e trava persistente; todos preservados byte a byte. Reativação/reinício mantêm escolha finita de retenção. Isso não é backup integral do banco compartilhado.

Novos parâmetros só são gravados ao aplicar uma simulação autorizada. Recibos WhatsApp continuam permanentes; recibos comuns seguem retenção própria. Recusas400 antigas não são apagadas nem reexecutadas. Depois de conferir recusa definitiva sem efeito, tentativa nova usa nova chave; resultado incerto exige reconciliação, nunca troca de chave como contorno.

Backup remoto cobre arquivos0.4.0. Restaurar arquivos não desfaz notas, atividades, mudanças de arquivo ou outros efeitos remotos. Se regras0.5.0 já tiverem sido salvas, voltar à0.4.0 exige também restaurar a cópia anterior das regras: schema0.4.0 é fechado e recusa campos novos. Guardar banco, salts, regras, recibos e arquivos antes da reversão. Não apagar recibos/travas para fabricar sucesso. Nenhum rollback compartilhado foi aplicado nesta rodada.

## 6. O que permanece pendente

- **Dono/frota, Pedido 10:** configurar por simulação os campos/IDs/textos/feriados/canais, política de nomes e mapa de adoção reais. O modelo expressa as novas regras; a atualização não transforma automaticamente a configuração comercial gravada em korvena.com.br. O documento de pedidos não fornece o objeto completo das regras efetivas dessa conta.
- **Dono/frota, aceite fornecedor em korvena.com.br:** criar lead exclusivamente de teste e excluí-lo no mesmo trabalho; conferir POST/PATCH200, repetição da chave sem duplicar nota, formato local da linha final, fila até1 hora útil, feriado e canal LinkedIn protegido. Conferir6415/4891 reais somente por leitura. Esta rodada não acessou esse site nem escreveu em registro real.
- **Frota:** publicar/distribuir depois de conferir bytes/SHA; a instalação deste agente foi somente no Site-Teste. Nenhum push/envio externo foi realizado.
- **Limites:** sem integração de envio/recibos WhatsApp, sem navegador visual, multisite, outros runtimes/caches ou observação prolongada. A API oficial foi consultada em Activities/Deals; consulta documental e fixture não encerram homologação comercial. Reconciliação automática de operações incertas continua indisponível.

O item10 está implementado e validado no escopo sintético/WordPress descrito; não está declarado homologado no fornecedor nem encerrado na lista central.

## 7. Credenciais e configuração do dono

Nenhum segredo novo. Token e autorização do consumidor operacao continuam no Fator3 Site Core; o plugin recebe somente o cliente público. Ferramentas → Fator3 MCP Pipedrive mantém status/ajuda e retenção. Regras comerciais: configuracao-ler → configuracao-simular → operacao-aplicar com revisão e frase aprovada. Schema/guia completos estão instalados em schemas/fluxos.

Cadência inicial permanece desligada, motivos de perda não inventados, sem leitura/escrita de credencial privada por este pacote. Configuração de conta e permissão MCP são independentes. Artefatos/evidências não incluem valores secretos, banco de laboratório, logs pessoais, cookies ou helper de transferência. Nomes/mensagens dos testes são sintéticos. Sem mudanças em plugins alheios.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
| --- | --- | ---: | --- |
| Instalador | wp-mcp-pipedrive-fator3-0.5.0-instalador.zip | 95019 | `59e8c99d5bb8a54fcfeaba06c56d816b940a1fe97a7d6b473d13a252c6e5042a` |
| Fonte | wp-mcp-pipedrive-fator3-0.5.0-fonte.zip | 447838 | `12217911a656f192a32df80fb6716abd009da6f3efe16252418c30a6e00b229a` |

Relatório externo canônico: wp-mcp-pipedrive-fator3-0.5.0-relatorio.md. A cópia no fonte é anterior ao fechamento; seu tamanho/hash foram preenchidos somente neste relatório externo, sem reabrir o ZIP fonte.

Instalador: raiz única wp-mcp-pipedrive-fator3/,31 arquivos, somente runtime/licença/documentação; sem QA ou ZIP interno. Fonte: raiz wp-mcp-pipedrive-fator3-0.5.0-fonte/, runtime idêntico, build, testes, evidências sanitizadas, entradas e relatório. Nenhum ZIP contém outro ZIP. Build determinístico; após fechar o fonte, extração e reconstrução conferem os mesmos bytes do instalador.
