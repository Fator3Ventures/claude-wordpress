# Entrega — Fator3 Site Core 1.56.0

26/10/2026. Horários em America/Sao_Paulo (UTC−03). Base direta 1.55.0; contrato administrativo 8.21.0; 157 abilities. Implementados os pedidos 307–311 e o consumidor Instagram solicitado pelo Meta 0.11.1. Instalador final ativo no Site-Teste, ciclo concluído e confirmado pelo executor. **Estado: implementado, com pendências de aceite externo**, detalhadas na seção 6. WhatsApp e Instagram permanecem desligados no Site-Teste.

## 1. Bases aceitas

Normas aplicadas: instruções comuns e padrão de desenvolvimento, revisão 5 de 23/10/2026, em inputs/1510. Escopo atual: documento “Fator3 Site Core” de 26/10/2026, pedidos 307–311, preservando a entrega 302 da 1.54.0 e 303–306 da 1.55.0. Plano em inputs/1560/plano.md. A conversa e os vínculos reais de CTO Office já relatados no pedido 309 não foram recriados.

| Base recebida | Bytes | SHA-256 |
|---|---:|---|
| Core 1.55.0 instalador | 2609157 | 1d7e54fb86ea4c61de5e58df22e81b5e93aad3018bc5802fb3fd86ff48dd41a0 |
| Core 1.55.0 fonte final | 3755919 | 054afe0bdece974adad005f0910735d10af0f73059a9ee807cf96bbbe3b33b97 |
| MCP 0.33.0 instalador | 888204 | f16ee3e31e4143ffb42c566ea6da4f2da81d3771a01a0f90b5d34e3d02ac8caa |

Meta 0.11.1 original: instalador SHA-256 b084bf2498eddc0eb93410c04efdd166ba84b2831541e2b5a2acf8dcfe3aa6c1; fonte e12e1d6f3a9b9daa8907840bdda40903ec307596971cdff458e7de88a25415b1. Relatório e impacto recebidos preservados em inputs/1560. O fonte 1.55.0 foi obtido na versão final correspondente ao instalador; candidatos antigos não foram usados como base de atualização.

Identidades mantidas: base-site-core-fator3/base-site-core-fator3.php, nome Fator3 Site Core, provider, namespaces, Text Domain e Update URI existentes. Mínimos comprovados: WordPress 7.1.2 e PHP 8.3.6 de 64 bits; também testado WordPress 7.1.3. Perfil piso-padrao-3.6 e ciclo de 17 etapas preservados.

## 2. Convivência e encaminhamentos

| Pacote/fronteira | Versão | Resultado e evidência própria |
|---|---|---|
| Fator3 MCP | 0.33.0 | Runtime original, sem alteração. Nove checks de autorização/revogação, cinco de política, documentação e instalação remota no Site-Teste. |
| Fator3 MCP Meta | 0.11.1 | SDK original instagram-first-message/1.0.0: 12 checks com Graph simulado; registro, callback, recibo, deduplicação, reconciliação e supressão. Presente no Site-Teste sem erro de inicialização. |
| Fator3 MCP Google | 0.19.0 | Preservado ativo no Site-Teste; sem nova homologação do fornecedor. |
| Fator3 MCP LinkedIn | 0.10.1 | Preservado ativo no Site-Teste; sem nova homologação do fornecedor. |
| Fator3 MCP Pipedrive | 0.1.0 | Preservado ativo no Site-Teste. Pipeline próprio do Core testado com transporte simulado, sem objetos comerciais reais. |
| WP Super Cache / Yoast | 3.1.4 / 28.7 | Preservados ativos; home e REST aprovados antes/depois. |

**Resposta ao impacto recebido** wp-mcp-meta-fator3-0.11.1-impacto-base-site-core-fator3.md, revisão 3, MCP Meta 18(b), responsabilidade Core: consumidor site-core implementado por hook público; política por conexão/conta desligada por padrão; recebimento mínimo cifrado; deduplicação própria; recibo persistido junto ao contato; reconciliação sem aceitar record_id arbitrário; tombstone após exclusão. Provas em meta-1560.json, request-307-311.json e permissions-*-1560.json. Atendido no escopo do consumidor local, com transporte Graph simulado. Não se declara concluída a homologação externa do Meta nem a eliminação coordenada de seu diário.

**Impacto emitido nesta rodada:** base-site-core-fator3-1.56.0-impacto-wp-mcp-meta-fator3.md, revisão 1 de planejamento, ação necessária. O SDK recebido não oferece exclusão dos metadados locais já persistidos no Meta. Solicita-se contrato público para essa eliminação e impedimento de reimportação, inclusive após revogação. A exclusão do Core informa pendente_sdk_exclusao_meta; não acessa classes/options privadas do Meta. O documento de planejamento é preservado sem revisão apenas para comunicar fechamento. Esta seção registra a implementação e o desfecho parcial do pedido recebido.

**Não há impacto novo nem alteração a pedir ao MCP 0.33.0.** As regras de contato, SMTP e atribuição são do Core; o canal existente descobre e transporta as quatro novas abilities. O MCP tem seu próprio operation_id: a aprovação também devolve aprovacao_operation_id, que corresponde ao identificador da decisão gravada no contato, sem depender de classes privadas do canal. Não foram enviados encaminhamentos por mensagem nem alterados os pacotes acompanhantes. Google, LinkedIn, Pipedrive e Implantador não tiveram contrato novo exigido por esta rodada.

## 3. Mudanças por pedido e evidência

### 307 — aprovação sem entrega

Aprovar com entregar=false grava aprovado_sem_entrega, instante, versão, usuário operador e operation_id próprio, conservando a decisão anterior no histórico. leads-registros-ler e fila Pipedrive projetam esse estado; leads-ler acrescenta a contagem total e por linha, e relatorios-integrados-ler, visão operacao, separa a aprovação das falhas. entregar=true conserva a solicitação normal do pipeline, sem conversão retroativa.

Para o legado, a leitura usa histórico de aprovação ou a combinação auditável captura original suspeita, captura corrente aceita, revisão posterior e intenção original captura_nao_aceita, sem regravar o registro. Mostra “aprovado sem entrega (anterior à regra)” e a evidência utilizada; não presume aprovação de todo contato aceito sem CRM.

Leitura prévia de CTO Office confirmou os estados legados dos registros 121 e 123: o 121 possui histórico de aprovação; o 123 conserva captura original suspeita, revisão 2 e captura corrente aceita. O caso 123 foi reproduzido em fixture. A nova projeção nesses registros reais depende da implantação da 1.56.0 pela frota; não foi aplicada em CTO Office nesta entrega. Em Site-Teste isolado, simulação, gravação, histórico, projeção de entrega, leads-ler e relatório de operação passaram. Evidência: request-307-311.json e site-request-307-311.json.

### 308 — celular brasileiro de oito dígitos

DDD brasileiro válido + oito dígitos iniciados por 6, 7, 8 ou 9 é classificado como celular, regra br-celular-8-prefixo-6-9, sem inserir nono dígito. Prefixos 2–5 permanecem fixos; DDD inválido não é classificado. Atividade inicial, link wa.me, diagnóstico e relatório telefones_normalizacao usam a mesma regra. Classificação informa versão e regra; sinais antigos de “incompleto” são reavaliados na leitura quando correspondem precisamente ao novo caso. Não altera números, atividades ou objetos CRM históricos.

Provas com os quatro prefixos, fixo, DDD inválido, atividade e link preservando dígitos; regressões de formulário e Pipedrive: 32 e 39 checks. Fluxo Pipedrive existente continua com seleção por identidade e unidade. O aceite comercial dos dois leads reais mencionados no pedido permanece com a frota/SDR; nenhuma atividade real foi criada nesta rodada.

### 309 — WhatsApp por ponte Slack

Nova configuração f3base_whatsapp_site e abilities whatsapp-conversa-verificar e whatsapp-conversa-consultar. Leitura incremental conversations.history, credencial Slack existente, allowlist de bots/usuários, direção explícita, telefone em campo próprio, exclusão de equipe/próprio número/números configurados. Os caminhos dos campos são configuráveis; não se afirma que o exemplo seja o envelope real Twinia.

Ativação começa no instante corrente, sem importar histórico. Janela estável com páginas de 15 mensagens e até 500 identidades pendentes cifradas; escolhe a primeira mensagem elegível antes de criar contatos, até 15 por passagem. Estado/revisão preservam o cursor; 429 respeita Retry-After. Mudança de configuração ou envelope incompleto pausa sem avançar. reler_janela permite revisar e reconstruir o preparo da mesma janela/canal/número, sem apagar contatos ou deduplicação. Agenda de 300 segundos integrada ao executor, com autorização atual do operador.

Contato whatsapp_conversa retém somente código, trecho de triagem limitado a 300 caracteres e campos privados necessários, cifrados. Código mapeado usa as chaves de atribuição; código ausente/desconhecido fica WhatsApp sem origem. Não cria sessão, evento ou conversão de anúncios. [TESTE F3BASE] em qualquer posição gera classe teste e bloqueia Pipedrive/Slack, inclusive com homologação global. Mensagens seguintes do mesmo número não criam contato novo. A exclusão remove também cópia pendente antes de eliminar o contato e conserva tombstone.

Comercial exige mapa_pontos existente e aviso Slack configurado; não cria alternativa remota do Pipedrive. Intenções ficam junto ao contato, recuperáveis pelas filas existentes, sem e-mail automático nem contingência por e-mail. A fixture CRM comprovou telefone existente → nota de triagem no lead aberto, sem lead novo. Filtros de relatórios aceitam whatsapp_conversa e instagram_conversa.

Provas: 17 checks do coletor (paginação, primeira mensagem, bloqueio de formato, releitura revisada, 429/escopo, cifra, exclusão), sete CRM, além da suíte integrada. Repetidos no ambiente isolado do Site-Teste. **Não equivalem ao aceite Twinia real:** o canal de teste não está configurado; a ability retornou whatsapp_canal_ausente. A leitura disponível da ponte não estabeleceu campos próprios de telefone/direção. O coletor não percorre replies nem infere telefone a partir do nome; se os campos estiverem só em threads/texto livre, a ponte precisa fornecer envelope compatível. Não foi captada conversa real [BIO], nem enviado aviso real.

### 310 — notas instaladas e índice de mudanças

Restauradas docs/history/RELEASE-1.49.0.md até 1.55.0, incluindo 1.49.1, 1.52.0 e 1.52.1; catálogo documental permite a pasta histórica e rejeita symlinks. 1.52.0 é identificada como candidato substituído por 1.52.1, não base recomendada. CHANGELOG e dados/mudancas.json indexam notas e detalhes; documentos atuais da 1.56.0 explicam contratos, uso, configuração e recuperação.

Site-Teste pelo MCP: RELEASE-1.53.0 retornou integralmente, SHA-256 ce8357414f82edc2641cc9d0c4b748e7b32694023a24212394329f182ad6016c. como-usar com incluir=["mudancas"] e desde_versao=1.48.0 retornou **10 entradas**. Não envie assuntos=[] quando desejar todos: lista vazia é um filtro sem assuntos. CONVERSAS-1.56.md lido em duas páginas até proxima_linha=null, SHA-256 4b10e328e77b9e31a454de42e7bb170ee1ec9fa5d81ca07cd3df5d5a80ac392a.

Índice instalado: 127 documentos; leitura completa em laboratório e fixture remota: 614 páginas/897 checks, sem chamadas de fornecedor. A documentação nativa foi gerada com Core sozinho; o MCP acrescenta seu contrato de transporte quando presente. Evidências docs-1560.json, site-docs-1560.json, site-docs-mcp.json e site-mudancas.json.

### 311 — prova SMTP antes de habilitar

Novos defaults 587/tls; configurações existentes são preservadas. email-smtp-verificar conecta, negocia TLS e autentica, sem MAIL/RCPT/DATA. Mesmo em simulação, grava recibo técnico por 15 minutos, ligado ao host, porta, segurança, usuário, remetente e revisão do segredo; isso está explícito no contrato. Ativar envio ou mudar identidade SMTP com envio ativo exige prova recente correspondente. Envio já ativo e configuração inalterada não é desligado pelo upgrade. Prova aparece na tela e tem ação administrativa com nonce.

Cliente comum ao envio manual e automático valida DNS/IP público, fixa IP e valida certificado pelo hostname; não desliga verificação TLS nem faz downgrade. Falhas distinguem porta recusada/sem resposta, TLS, protocolo e autenticação. Incerteza após transmissão continua sem repetição automática.

Site-Teste real, PHP 8.3.36: **587/tls autenticado sem envio; 465/ssl também autenticado sem envio**. A falha de 465 em CTO Office não foi reproduzida neste host/instante e não se declara porta 465 indisponível em toda DreamHost. Ambos retornaram mensagens_enviadas=0 e data_transmitido=false; o último recibo foi 587/tls. A recusa sem prova, validade, configuração divergente e códigos de falha foram comprovados por fixtures; 18 checks de transporte, mais guardas na suíte integrada e permissões. Evidência site-smtp.json. Não foi enviado e-mail real para provar entrega, DKIM, SPF ou DMARC nesta rodada.

### Consumidor Instagram — Meta 18(b)

Registro do consumidor pelo hook público f3_meta_register_messaging_consumers; habilitação explícita por conexão/conta nos dois plugins. Valida contrato, chave, escopo, ativação e cobertura oldest_available_matches_signed_webhook; lifetime_first_unverified. Não inventa telefone, e-mail, UTM, sessão, anúncio, consentimento ou origem espontânea quando a origem é desconhecida. Sem texto/anexos pelo contrato recebido. Identificadores mínimos ficam cifrados no contato; recibo e deduplicação são duráveis.

Reconciliação consulta deliveryReceipt e confirma somente recibo real do Core; evidence_changed exige revisão e não confirma o contato antigo como prova nova. Contato eliminado retorna suppressed. Sem consumidor/SDK/política válidos, não usa contato-externo-registrar como substituto. O rótulo genérico “Contato Instagram” só é usado transitoriamente no despacho CRM explicitamente habilitado quando não há nome; não é identidade, não busca pessoas por esse rótulo e não preenche nome inferido no contato.

SDK Meta original testado com Graph simulado e webhook assinado sintético; interrupção após gravação reconciliada sem contato duplicado, exclusão e reimportação bloqueada. Política comercial dessa integração não foi ativada no Site-Teste. O fluxo de criação CRM Instagram com rótulo genérico não teve homologação comercial externa; permanece parte do aceite de opt-in.

## 4. Instalação e prontidão

Instalador fechado com **735 arquivos, 538 PHP sem erro de sintaxe** em PHP 8.3.6. Mesmos bytes usados nos testes e no Site-Teste. Runtime não alterado após o fechamento.

| Ambiente | Prova | Resultado |
|---|---|---|
| WordPress 7.1.3 / PHP 8.3.6 | Instalação limpa + upgrade nativo 1.55.0 | Ambos passaram; configurações/dados de fixture preservados, repetição atual sem nova migração |
| WordPress 7.1.2 / PHP 8.3.6 | Instalação limpa + upgrade nativo 1.55.0 | Ambos passaram, mesmo ZIP |
| Core isolado | Pedidos/autorizações/documentos e regressões | Passaram; fornecedores controlados |
| Core + MCP 0.33.0 + Meta 0.11.1 | Permissões, política, SDK e documentação | Passaram; Graph simulado |
| Site-Teste, WP 7.1.3 / PHP 8.3.36 | Atualização 1.55.0 → 1.56.0, fixture isolada e SMTP real | Concluída; testes aprovados; zero e-mails na prova SMTP |

Suítes locais: integrada 307–311 (62), coletor WhatsApp (17), CRM WhatsApp (7), transporte SMTP (18), Meta SDK (12), permissões nativas/MCP (9 cada), política MCP (5), formulários (32), Pipedrive (39), regressões 300 transportes (19), 300 CRM (38), 301 (59), 302 (69), 302 CRM (14), permissões herdadas 1550 (21), documentação (897). Contagens são asserções, não quantidade de cenários externos independentes. Uma execução CRM após outras suítes identificou notas de outros contatos de fixture; o teste passou a filtrar a nota sintética da conversa sob teste, sem alteração do runtime. Provas finais e remotas passaram.

Site-Teste: ciclo iniciou **14:42:35**, completou 17 etapas **14:42:38**, confirmado pelo executor **14:43:41**, estado concluida, zero falhas. Operação de pacote 47037f25bdef3be5e420407bd9a36014; backup anterior 4ee52c829e8a8b7b81dc87ed. Home/REST anônimos com bypass de cache passaram antes/depois da troca; são provas da mesma origem, não medição externa de rede.

Manifesto dos 735 arquivos instalados igual ao local: **882218b81f63076795db29a449af86f6105277a679353243616897175bccdb77**. Tela SMTP renderizada com prova; opções preservadas durante leitura; 157 abilities; nenhuma chamada de fornecedor nessa inspeção. E-mail da caixa permaneceu ativo como já configurado, WhatsApp e Instagram desligados.

Fixture no próprio Site-Teste repetiu integrada 62, coletor 17, CRM 7, SMTP 18, pedido 302 com 69, permissões 9 e documentação 897. Usou prefixo SQL aleatório e WordPress separado, nunca apagou banco compartilhado. Limpeza comprovada: **71 tabelas próprias removidas, zero restantes, diretório e manifesto eliminados; controlador e ZIP temporários removidos**. O canal exigiu backup para apagar PHP, preservado; não foi contornado. Sondas depois da remoção passaram. Evidências em evidence/1560/site-*.json.

## 5. Banco, retenção e reversão

Sem nova tabela ou migração destrutiva. Contatos conversacionais usam a tabela existente, payload privado cifrado, intenções de entrega e chave idempotente; nenhuma cópia pessoal em sessões/eventos. Novas options de configuração/estado para WhatsApp, Instagram e prova SMTP constam no inventário (152 options, 59 tabelas inventariadas, 11 transientes); não são novas tabelas desta versão. Defaults não ativam consumidores. Aprovação acrescenta histórico e decisão; projeção legada não regrava registros. Estado do coletor tem pendências cifradas e autorização/revisão do operador. A retenção/exclusão normal dos contatos aplica-se, com tombstone mínimo contra reimportação.

Antes de voltar arquivos, desative explicitamente captação WhatsApp/Instagram e preserve o backup normal do banco. Reverter para 1.55.0 remove capacidades/leitura novas, mas não desfaz contatos, intenções ou entregas externas; o backup de plugin não restaura banco. O código anterior não conhece plenamente os novos métodos; evite operar esses contatos no código anterior e prefira correção adiante ou restauração coordenada do backup pertinente. Não apagar options/diários manualmente para contornar deduplicação. Recuperação de janela usa a rota revisada documentada; resultados incertos CRM/Meta exigem reconciliação.

Exclusão local não apaga mensagens originais no Slack, objetos no CRM ou diário Meta. A pendência Meta é explicitamente exibida; ver impacto. Nada nesta entrega afirma que cópias externas foram eliminadas.

## 6. Pendências e responsáveis

1. **Frota / responsável Twinia:** fornecer e conferir envelope real com telefone e direção em campos próprios, bot/usuário permitido e canal de teste; obter scopes channels:history/groups:history e participação do bot. Se os campos só existem em replies/texto livre, adequar a ponte. Executar mensagem [TESTE F3BASE] real e conferir contato teste sem aviso/CRM. O código está entregue; a interoperabilidade Twinia real ainda não está demonstrada.
2. **Frota / operação Pipedrive:** criar/confirmar Ponto de conversão próprio e mapa_pontos, configurar origem [BIO] e demais códigos, habilitar após prova e validar primeira conversa real/nota no lead aberto e repetição sem duplicação em CTO Office. Não criar alternativas nem leads fora desse procedimento. Nenhum aceite comercial real desta rodada.
3. **Mantenedor Meta:** atender a API pública de eliminação pedida no impacto revisão 1. Até lá, Core apaga sua cópia e impede reimportação, mas registra pendência externa. Não declarar exclusão coordenada concluída.
4. **Dono / frota / Meta:** autorização instagram_manage_messages, token/conta/Página adequados e homologação externa com webhook/mensagem controlados; validar opt-in comercial e limites de cobertura. Fixture SDK não substitui App Review nem entrega real.
5. **Frota:** decidir publicação e troca nos demais sites; depois conferir projeções dos registros 121/123 e regra de celular na prévia comercial. Somente Site-Teste foi atualizado aqui; CTO Office teve leitura, sem implantação/gravação. Não houve push/publicação no repositório nem alteração da lista central de pedidos.
6. **Frota / hospedagem:** se 465 voltar a falhar no host original, colher o código por fase. Não há reprodução dessa falha no Site-Teste; 587/tls e bloqueio sem prova estão comprovados. Aceites históricos de 1.55.0 (caixas reais, observação diária e sessão persistente) não foram declarados encerrados por esta rodada.

Os pedidos não foram retirados de documento externo: o revisor da frota registra seu aceite, distinguindo código entregue, testes controlados e fornecedor real.

## 7. Credenciais

Nenhuma credencial nova solicitada, criada, exposta no relatório ou incluída no pacote. Slack reutiliza o segredo cifrado do Core; Instagram usa SDK e conexão sob responsabilidade Meta; Pipedrive usa cliente e token existentes; prova SMTP usa a senha cifrada já configurada na caixa do Site-Teste. Somente autenticação SMTP foi feita no fornecedor real, sem mensagem. Fixtures usam identidades/segredos sintéticos e bloqueiam HTTP/mail externos.

Fonte exclui bancos, wp-config de laboratório, logs, cookies, tokens e runtimes acompanhantes. Evidências técnicas são sanitizadas; exemplos de nomes/telefones nas fixtures são sintéticos. Metadados técnicos de instalação/backup e inputs fornecidos pelo dono ficam identificados. Nenhum dump de contato real ou conversa Slack foi incluído.

## 8. Arquivos finais e integridade

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| base-site-core-fator3-1.56.0-instalador.zip | 2667464 | e9dd77379d64706ad37de2428dc91a02bdaeb0649f68b38d3024ffcaac4ebed9 |
| base-site-core-fator3-1.56.0-fonte.zip | 3950523 | 36b54c1711c39aaeb8e32c1ab1b77d84d58bc5c82de905b2699b50ae38aa9b85 |

Complementos: base-site-core-fator3-1.56.0-relatorio.md (este relatório) e base-site-core-fator3-1.56.0-impacto-wp-mcp-meta-fator3.md (pedido técnico ao Meta, revisão 1).

Instalador contém somente a pasta base-site-core-fator3/ e seu runtime. Fonte contém código idêntico ao instalador, build, locks, testes, evidências, inputs, histórico e cópia deste relatório identificada como anterior ao fechamento; hash final do fonte fica nesta cópia externa para evitar circularidade. Nenhum ZIP da entrega contém outro ZIP. Só o instalador é instalável.

Para implantação autorizada pela frota: publicar os bytes finais e conferir o SHA-256 servido, então usar plugins/upload com expected_slug=base-site-core-fator3 e expected_sha256 acima; esperar ciclo concluído e confirmada_no_executor_em. A URL temporária do Site-Teste foi removida e não é origem de distribuição. Não há URL raw nova publicada por esta sessão.
