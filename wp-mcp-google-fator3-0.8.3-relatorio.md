# Entrega — WP MCP Google 0.8.3

**Implementado o escopo Google da próxima release**, em uma única versão estável. Base de referência: WordPress limpo ou Google 0.8.2 pronta/pendente, sem travar a origem por número no código. Integração: Core 1.30.0 + MCP 0.19.0, mantidos inalterados.

## O que mudou

| Plano | Entrega |
|---|---|
| G083-01 — admissão | Disputa normal retorna `yielded`, zero trabalho próprio e sucesso do envelope/CLI; erros reais de armazenamento continuam falhas |
| G083-02 — fechamento | Evento terminal durável precede projeções; `confirmed`, `pending` e `unconfirmed` são distintos; reconciliação não repete jobs/HTTP; retenção conserva fontes pendentes |
| G083-03 — recuperação | Identidade do erro observada e reconferida sob lease; erro órfão da 0.8.2 pode ser resolvido; erro novo concorrente e histórico permanecem; idade não apaga falha |
| G083-04 — UX/contratos | Painel mostra cessão, pendência, erro ativo/resolvido, falhas de agenda, horário do site e JSON recolhido; catálogo e documentação atualizados |
| G083-05 — agenda | Pós-condição por agendar/reagendar/remover/limpar; `cron.scheduling` 1.0.0; leitura persistida e visão efetiva conferidas; `could_not_set` preservado como código original |

Preservados Service Account como padrão, OAuth separado, 282 habilidades, configuração 3.0.0, execução/catálogo 2.0.0, manutenção 1.0.0 e SDK `search-console-reader/1.0.0`. Sem novos serviços ou permissões implícitas. A limpeza de desativação/desinstalação continua funcionando com bootstrap mínimo e guarda pausada. O observador WP-CLI mantém manutenção limitada mesmo sem callback Google; o executor solta a admissão antes dessa limpeza.

## Validação

- **1.084 testes / 12.505 asserções** aprovados. Após o ajuste final da manutenção do observador, mais **45 testes / 218 asserções** focados aprovados; são um subconjunto de regressão, não 45 testes novos. Sintaxe PHP, tokens de formatação, catálogo/schemas e links conferidos.
- WordPress 7.1.2, PHP 8.3.6, MariaDB 10.11.14. CLI/HTTP locais, processos independentes e barreiras determinísticas forçaram as disputas. Um efeito sintético aplicado permaneceu único após duas reconciliações.
- `wp-cron.php` real reproduziu aviso no reagendamento cuja intenção já estava persistida por outro processo, preservando eventos Core/terceiro. Uma remoção SQL realmente recusada permaneceu falha, com a ocorrência vencida presente. Um callback por caso, sem ocultar o log.
- Gravação/leitura recusada, cache divergente, contexto ausente, telemetria recusada, erro órfão, resolução recusada, identidade nova no mesmo segundo, retenção pendente, lacunas e recuperação exercitados. Dois subsites reais preservaram isolamento de cache/diagnóstico.
- Core: SDK real/HTTP Google simulado, conexão não padrão, permissões/grants, coleta/commit, quota futura, disputa do executor, duas ordens de carga e guardas independentes. Atualização preservou políticas, três decisões granulares, tabela Slack e conversões históricas sintéticas, sem tentativa de reenvio.
- Plugin_Upgrader: instalação limpa e atualização de 0.8.2 pronta/pendente, retorno dos arquivos antes/depois da manutenção e desinstalação isolada/purge. Canal MCP: `plugins/upload`, hash, ativação em novo processo e sondas home/REST em loopback; download do ZIP simulado.
- Interface: 36 verificações de formulários e **39 verificações no navegador**, incluindo teclado, cópia, mobile e uso sem JavaScript. **13 verificações de downloads** autenticados/recusa, com documentos/script comparados byte a byte.
- Pacote: **138 arquivos / 18 diretórios**, todos com índice silencioso; **110 verificações HTTP** com autoindex habilitado e controle positivo. Sem `.htaccess`, Markdown, `docs/`, `reference/`, testes ou credenciais no instalador. Documentos e Cloud Shell são dados PHP protegidos acessíveis pelo painel autenticado; script não executado.
- Regressão 411: os três PUTs vazios retornaram 204 em servidor local, com `Content-Length: 0` e corpo vazio.

As evidências finais, sondas e instruções de reprodução estão no ZIP fonte. A bancada não integra os arquivos distribuídos. Ensaios de código-fonte e de pacotes são correlacionados no manifesto; ajustes documentais e o callback de manutenção do observador tiveram verificações específicas. A contagem dos companheiros é separada das 282 habilidades Google.

## Impactos e limites

Nenhum código Core/MCP alterado: 369 e 523 arquivos, respectivamente, comparados com os ZIPs recebidos. Os relatórios separados delimitam contratos e encaminham `f3_mcp_cron_observed` ao MCP. O novo timeout/resultado inconclusivo do atualizador MCP foi conferido em seu fonte; não se reutiliza a conclusão histórica de rollback da 0.18.0.

Sem implantação em produção, credencial Google real, crontab hospedado ou envio externo. O transporte Google foi simulado; cache externo controlado, sem Redis/Memcached reais. Não se promete SLA de desempenho nem eliminação de todas as linhas de log WordPress. Diagnóstico de agenda é limitado a 100 intenções ativas, com excesso declarado; ausência de amostra não comprova sucesso.

Os **pedidos Google 20 e 21** estão cobertos pelo pacote; os aceites operacionais continuam pendentes de publicação/observação do responsável: **sete dias, 13 sites para o pedido 20 e 14 para o pedido 21**, com listas nominais confirmadas. São diferentes da pendência 20 do estado da frota. Esta entrega não encerra automaticamente nenhum aceite externo.

## Instalação

Utilize somente o ZIP `-instalador.zip` para substituir a instalação, sem desinstalar. Preserve backup coerente, chaves e guardas conforme MIGRACAO.md. Redescubra o catálogo MCP e confira versão, status e selftest. O ZIP `-fonte.zip` contém desenvolvimento/testes/documentação e deve permanecer fora da pasta pública de plugins. Guia e relatórios de impacto acompanham a entrega.

## SHA-256 do instalador

`1c60bc7bff22011c85e80a488a445c088cc3f12c6a99372fdcda67919b3dd9ce`

## SHA-256 do pacote-fonte

`41fe7f82c758e52aac7828935deef3125075b4b45a80f882b4ccf55b6d70a264`
