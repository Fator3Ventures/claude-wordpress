# Entrega — Fator3 MCP Google 0.36.0

14/11/2026 · **Implementada e homologada no Site-Teste. Aceite em produção pendente para o pedido 54.**

## 1. Bases de instalação

Instalação limpa ou atualização direta da **0.35.0** para a **0.36.0**, sem versão intermediária. Mínimos do pacote: WordPress 7.1.4 e PHP 8.3. Bancada usada: WordPress 7.1.4, PHP 8.3.6 e MariaDB 11.8.6. O instalador anterior tem 979.405 bytes e SHA-256 `c1fdf87b53e197fca8aa9f93816e1047b065283a3edfca3c44b4c2b16484045a`. O fonte anterior tem 8.876.389 bytes e SHA-256 `a8a1e8c4e50128295ad56dee7407d373655a04004f508f8bb918b991c7ac12c8`.

A rodada aplicou `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos na revisão 5 de 02/11/2026, a regra comum de 14/11 e a aba do pacote Google. No fonte, os pedidos recebidos estão em `plugin/wp-mcp-google-fator3/inputs/pedidos-google-53-54.md`. As referências a evidências abaixo usam a pasta `plugin/wp-mcp-google-fator3/evidence/036/`.

## 2. Contratos e versões verificadas

| Interface | Valor |
|---|---|
| Habilidades | 305 no total, sendo 120 de leitura e 185 de escrita |
| Configuração | 44 opções públicas, contrato 4.0.0 |
| Catálogo de habilidades | 3.0.0 |
| Execução | 2.0.0 |
| Armazenamento, manutenção e agenda de cron | 2.0.0 cada |

| Pacote | Versão no fechamento | Prova |
|---|---|---|
| Fator3 Site Core | 1.87.3 | Instalador fornecido, registro do acervo pelo Core e contrato do leitor do Google |
| Fator3 MCP | 0.45.0 | Transporte HTTP autenticado, habilidades e índice de documentos |
| Fator3 MCP Meta | 0.27.0 | Ativação simultânea em WordPress e inventário do Site-Teste |
| Fator3 MCP LinkedIn | 0.24.0 | Ativação simultânea em WordPress e inventário do Site-Teste |
| Fator3 MCP Pipedrive | 0.11.1 | Ativação simultânea em WordPress e inventário do Site-Teste |

A atualização do Google é independente da ordem de troca dos acompanhantes. O único acréscimo à interface compartilhada é o campo de leitura `cron.scheduling.resolution_receipts`. Consumidores que já leem `health` e `active_errors` recebem o diagnóstico corrigido pela mesma chamada. O escopo avaliado inclui o transporte MCP, o leitor do Core e os pacotes de mídia e CRM. Nenhuma alteração de código em outro pacote foi identificada para estes pedidos. As versões intermediárias observadas durante a rodada estão nas evidências de convivência.

## 3. Mudanças e aceite por pedido

### Pedidos MCP Google 53 — telas administrativas

Em **Ferramentas → Fator3 MCP Google**, as nove abas estão distribuídas em três grupos.

| Grupo | Abas |
|---|---|
| Configurar | Conexão, Conversões, GTM e Avançado |
| Dados | Acervo Ads e Search Console |
| Suporte | Visão geral, Incidentes e Ajuda |

O cabeçalho identifica o plugin, a finalidade e a versão. A escolha da conexão fica em cartão próprio. A navegação quebra linhas em telas estreitas. Os estados têm texto e cor, os formulários têm rótulos e as tabelas têm rolagem no próprio bloco. Busca, total e paginação permitem localizar registros fora da primeira página. Os endereços existentes com `section` abrem a aba correspondente já no grupo correto. A conexão selecionada acompanha a navegação.

**Aceite em Chromium 150.** 51 capturas reais, 17 por largura, em 360, 768 e 1440 px. A cobertura inclui as nove abas, os painéis internos de Conexão e Avançado e as duas formas de autenticação. A navegação e a página couberam nas três larguras. O navegador verificou busca em outras páginas, limites anterior/próxima, estados com e sem resultados, rótulos e seleção da conexão. O administrador salvou e restaurou o nome de uma conexão pelo formulário. O WordPress recusou a abertura da tela e a gravação pelo assinante e recusou o formulário administrativo com nonce inválido. Provas em `telas/`, `telas/checks.json` e `permissoes.json`.

### Pedidos MCP Google 54 — resolução de falhas de agendamento

O diagnóstico compara a intenção da operação com uma observação posterior confirmada pelo WordPress. Ele verifica gancho, argumentos, direção da operação e, quando aplicável, frequência, intervalo e horário. Uma chamada avulsa do executor pode ser atendida por uma ocorrência equivalente que cumpra o prazo. Erros sem uma confirmação compatível continuam ativos. O campo `resolved_at` registra o instante da confirmação e `resolved_by` identifica a observação. Os últimos 100 vínculos ficam disponíveis mesmo quando um erro mais recente ocupa a posição do anterior no histórico.

Nos quatro sites citados, a leitura da 0.35.0 encontrou um erro ativo de manutenção por site. As observações foram copiadas com seus identificadores para uma bancada WordPress. A primeira leitura da 0.36.0 reconheceu os quatro casos, sem intervenção nem escrita na opção de cron. A manutenção persistiu a resolução e a repetição foi idempotente.

| Histórico de origem | Leitura em produção na 0.35.0 | Primeira leitura da 0.36.0 na bancada |
|---|---|---|
| Twinia | `degraded`, 1 erro | `idle`, 0 erros ativos |
| Conselar | `degraded`, 1 erro | `idle`, 0 erros ativos |
| Fator3 Capital | `degraded`, 1 erro | `idle`, 0 erros ativos |
| Fator3 Grupo | `degraded`, 1 erro | `idle`, 0 erros ativos |

**Aceite no Site-Teste.** Uma tentativa controlada de agendar `f3_mcp_google_maintenance` produziu `degraded` e um erro ativo em `google/status`. O agendamento posterior do mesmo evento produziu `idle` e zero erros nas leituras completa e compacta. O erro `00001794707150433488_e7924b408015e447` foi resolvido pela observação `00001794707342366002_286e95c84b0ddb4b`, em `resolved_at=1794707342`. Após a remoção da ferramenta de teste, foram verificadas a ausência do plugin, da opção temporária, da ocorrência de teste e do registro sintético. O evento normal de manutenção permaneceu presente. Provas em `site-teste.json`, `upgrade.json` e `reproducao-quatro-sites.json`.

## 4. Instalação, prontidão e cobertura

O único arquivo instalável é o ZIP com sufixo `-instalador.zip`. Na administração, use **Plugins → Adicionar plugin → Enviar plugin**. O basename é `wp-mcp-google-fator3/wp-mcp-google-fator3.php`. No Site-Teste, o atualizador recebeu o ZIP por transporte autenticado com SHA-256 e slug esperados. Registrou a troca ativa 0.35.0 → 0.36.0 no recibo `42dac8b8b140cf835dcc1fb23845b8e7`. As sondas do início do site e de `/wp-json/` retornaram HTTP 200 antes e depois.

| Consulta após a troca no Site-Teste | Resultado |
|---|---|
| `google/status` | `plugin_version=0.36.0`, `abilities_registered.total=305`, cron e trabalho em `idle`, zero erros ativos e zero incidentes abertos |
| `google/integration-status` com `compact=true` | `success=true`, `read_success=true`, conexão `default`. Anunciados leitores Search Console 1.0.0/1.1.0, GA4 1.0.0 e Google Ads 1.0.0 |
| `google/storage-status` | `ready=true`, `state=ready`, contrato 2.0.0 |
| `google/documentation` | 26 documentos no índice. Guia da 0.36.0 e acompanhamento do cron lidos até o fim, com tamanho e SHA-256 iguais aos documentos do fonte |

| Verificação | Resultado |
|---|---|
| Instalação limpa | 5 verificações com o Google como único plugin ativo |
| Atualização populada | 6 verificações na base e 39 após a troca, incluindo credencial cifrada, configurações, tarefa, falha real e casos que devem continuar ativos |
| Reprodução dos quatro históricos | 16 verificações via Abilities API nas leituras completa e compacta |
| Convivência | 7 verificações no conjunto final, incluindo registro de acervo do Core |
| Suíte unitária | 1.366 casos e 16.252 asserções, zero falhas e zero pulos. Bootstrap e providers originais, com executor local compatível. O download do PHAR oficial do PHPUnit expirou |
| Documentação pelo MCP HTTP na bancada | 97 verificações, 26 documentos, 89 páginas, 4.484.624 bytes lidos e nenhum HTTP externo durante a leitura |
| Catálogo e empacotamento | 54 exemplos, 167 links locais, 201 arquivos PHP do instalador aprovados no lint e 205 arquivos de runtime com paridade byte a byte |

Na distribuição da frota, o responsável confere os hashes da seção 7 e o hash do instalador servido pelo repositório antes do primeiro `plugins/upload`. Parâmetros de instalação: `expected_slug=wp-mcp-google-fator3` e `expected_sha256` da seção 7. [Endereço do instalador após a publicação pela frota](https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-google-fator3-0.36.0-instalador.zip)

## 5. Banco, continuidade e recuperação

A versão usa a opção de diagnóstico de agendamento existente. O novo histórico de vínculos é aditivo e limitado. A leitura calcula a resolução em memória. A manutenção normal ou uma gravação de agenda posterior persiste a mudança sob o bloqueio do plugin. Não há alteração de esquema SQL nem reconfiguração de credenciais. O teste de atualização comparou os bytes das opções e da credencial cifrada, confirmou sua leitura e recuperou a tarefa gravada na 0.35.0.

O atualizador identificou a cópia de arquivos `70eff93ca262130eb10f5e9f`. Restaurar arquivos não desfaz registros ou opções já gravados. A recuperação de dados usa o backup do banco do site. Uma correção de código após a instalação exige nova versão.

## 6. Pendências e credenciais

O aceite final do pedido 54 exige instalar a versão nos quatro sites e reler `google/status`. O responsável pela frota deve conferir `plugin_version=0.36.0`, a saída do erro histórico de `active_errors` e seu vínculo em `resolution_receipts`. O critério é que **esse erro** deixe de degradar a saúde. Qualquer falha nova tem diagnóstico próprio. Os quatro sites foram consultados somente para leitura nesta rodada.

O proprietário não precisa inserir credenciais para atualizar o painel ou reconciliar o cron. Conexões e permissões existentes seguem em uso. Chamadas a contas reais do Google, inclusive Ads e Sheets, envio de conversões e execução do Cloud Shell ficaram fora da homologação desta rodada. O teste do MCP cobriu o transporte e os documentos servidos localmente. As pendências externas de Ads e entrega de avisos da 0.35.0 não foram reavaliadas.

## 7. Identidade dos arquivos

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| `wp-mcp-google-fator3-0.36.0-instalador.zip` | 983527 | `b066ed24418a1eccaa3c93504e5d817c1e06cf2e4993787fae68201e6a35ac27` |
| `wp-mcp-google-fator3-0.36.0-fonte.zip` | 17798934 | `d7fd142652f8effaa0f7f9d26adbfc55ceee8f11c74ff20ac9c1cfdbdb1dc0b2` |

O fonte fechado contém 2.397 arquivos, incluindo as 51 capturas e a cópia do relatório anterior ao fechamento. A reconstrução a partir de uma extração nova produziu um instalador idêntico, byte a byte, ao instalado no Site-Teste.
