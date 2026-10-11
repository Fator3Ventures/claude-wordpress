# Guia — Fator3 MCP Google 0.8.3

## Atualização

Instalar `wp-mcp-google-fator3-0.8.3-instalador.zip` em WordPress limpo ou substituir a 0.8.2 sem desinstalar. A base delimita ensaios, sem bloqueio no código por versão de origem. Ler `MIGRACAO.md` (no pacote-fonte) para migração pendente, backup, pausa/drenagem e retorno dos arquivos. Matriz: Core 1.30.0 + MCP 0.19.0.

## Configuração

Em Ferramentas → Fator3 MCP Google, selecionar a conexão e o método de autenticação. **Service Account** permanece primeira opção e padrão. Importar a chave JSON, revisar a identidade candidata e ativá-la explicitamente; conceder acesso à identidade nos serviços necessários. OAuth fica em aba separada: uma identidade ativa por conexão. O plugin não cria projeto/chave sem solicitação; o script Cloud Shell revisado tem download autenticado; o original histórico acompanha o pacote-fonte.

Habilitar serviços, testar credencial e selecionar propriedade/stream/conta. IDs explícitos prevalecem; a resolução opcional do Measurement ID Core não cria propriedade nem injeta tag. Ads mantém developer token obrigatório. Credencial válida não comprova acesso a todo recurso; consultar `google/selftest` e sua cobertura, sem interpretar incompleto como aprovado integralmente.

## Operação e manutenção

O painel Operação mostra a manutenção: estado da última passagem, idade da observação, próxima execução, orçamento e progresso por família. O botão Avançar um lote usa `google/migrate-storage` com a autorização e nonce usuais. JSON fica recolhido e pode ser expandido e copiado pelo usuário.

`google/storage-status` e `google/status` incluem `maintenance_contract_version:1.0.0`. `complete` exige inventário integral examinado sem pendência; `pending` pede novo lote; `failed` fornece erros. Bloqueio por recuperação aparece em `blocked_by`, sem alterar a amostra histórica. `read_success:false` impede tratar o resultado como contagem conhecida. Consultas não limpam nem migram o histórico.

Uma passagem automática compartilha 100 unidades/1.000 ms entre cron, origens arquivadas e cache; o limite é cooperativo. Muitas conexões, inclusive removidas, avançam por cursor. Cópia verificada precede exclusão. Cache SQL obsoleto não prevalece sobre cache externo mais novo; entradas vencidas/sem validade conhecida são descartáveis. Saúde do cache e erros não exibem payloads ou segredos.

O resultado do trabalho remoto, a gravação do histórico e o resultado da manutenção são independentes. Não repetir uma escrita Google porque a limpeza falhou. `ultima_cli`, `ultima_http` e `ultima_manual` permanecem separados. Ler `ACOMPANHAMENTO-CRON.md` (no pacote-fonte).

## Contratos e limites

282 habilidades (108 leituras/174 escritas), 34 opções, configuração 3.0.0, execução/catálogo 2.0.0 e leitor PHP `search-console-reader/1.0.0`. Nenhuma habilidade/serviço novo; concessões SDK continuam explícitas. Core controla tags, consentimento, coleta e commit próprios; MCP controla canal, perfis e atualização. `contexto_teste` não cria autorização nas APIs Google.

Documentos e scripts são disponibilizados pelo painel com autenticação. O instalador não contém Markdown, `docs/`, `reference/` ou `.htaccess` expostos; cada diretório tem índice silencioso. Fontes/testes ficam no ZIP fonte, fora do diretório público. Consulte `VALIDACAO.md` (no pacote-fonte) para evidências e limitações.

## Diagnóstico da 0.8.3

Ao receber `state:yielded`, a chamada cedeu a outra passagem. `success:true` confirma esse encerramento normal; `work_success:null` e zero itens indicam que ela não executou trabalho. O CLI encerra normalmente. Falhas reais continuam com erro.

`history_status:pending` preserva resultado durável para reconciliação local. `unconfirmed` indica prova insuficiente. Não reenvie uma operação Google por causa do histórico. `observability_error:null` com `last_observability_error.resolved_at` significa recuperação confirmada daquela identidade; confira também cobertura e manutenção.

Em `cron.scheduling`, compare operação, gancho, origem e timestamp ao aviso WordPress. `confirmed` preserva o aviso original, `failed` indica pós-condição ausente e `unconfirmed` indica falta de prova. A remoção exige ausência da ocorrência antiga. Leia o roteiro `ACOMPANHAMENTO-CRON.md` (no pacote-fonte) antes de classificar uma linha como inofensiva.

Core 1.30.0 mantém publicidade e medição independentes. Atualizar Google não altera essa política, tags ou consentimento. Inclua a tabela Core `f3base_slack_manutencao` e as opções no backup conjunto; preserve a guarda ativa pelo protocolo de recuperação. Nenhuma mensagem Slack é reenviada pelo Google.
