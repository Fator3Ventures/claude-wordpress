# Entrega — Fator3 MCP Meta 0.23.0

Revisão 1 · 10/11/2026 · Revisão, correção e instalação de homologação · `wp-mcp-meta-fator3/wp-mcp-meta-fator3.php`

**Status global `com-pendencias`.** Versão ativa e aprovada no Site-Teste para administração local, diagnóstico, persistência e contratos exercitados. O aceite com ativos Meta reais do Pedido MCP Meta 27 continua pendente.

## 1. De onde esta versão entra

Instalação limpa ou atualização direta do Meta 0.22.1 fornecido, também identificado como ativo no inventário anterior à instalação. Seu instalador tem 258974 bytes e SHA-256 `c52f3098c0b08accf8e79672687b1bc428cb08f04d4dc38a1c97c78758a15a2a`. A numeração segue o incremento minor do projeto.

Foram lidos os documentos `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos revisão 5, de 02/11/2026. O relatório e o runtime da 0.22.1 identificam a base. O Google 0.32.0 e suas imagens de configuração foram considerados como referência de apresentação e como pacote acompanhante.

Requisitos do produto: WordPress 7.1.4 ou superior e PHP 8.3 ou superior de 64 bits. Bancada executada com WordPress 7.1.4, PHP 8.3.6, MySQL 8.0.46 e Chromium Headless Shell 156.0.8078.79. O Site-Teste respondeu com WordPress 7.1.4 e PHP 8.3.36.

## 2. Convivência e encaminhamentos

| Plugin | Conjunto fornecido e ativado na bancada | Ativo no Site-Teste após a troca | Fronteira verificada |
|---|---:|---:|---|
| Fator3 Site Core | 1.80.0 | 1.80.0 | Registro do consumidor nos SDKs de anúncios e monitoramento, com versão correta em ambos |
| Fator3 MCP | 0.44.0 | 0.44.0 | Descoberta, schema, execução, leitura e paginação documental |
| Fator3 MCP Google | 0.32.0 | 0.31.0 | Ativação e coexistência da versão fornecida na bancada |
| Fator3 MCP LinkedIn | 0.20.0 | 0.20.0 | Ativação e coexistência |
| Fator3 MCP Pipedrive | 0.9.0 | 0.9.0 | Ativação e coexistência |
| Fator3 MCP Meta | 0.23.0 | 0.23.0 | Fluxos detalhados nas seções 3 e 4 |

Os doze ZIPs anexos passaram em verificação de integridade. Versão interna de cada instalador e SHA-256 dos seis instaladores e respectivos fontes foram comparados com os relatórios entregues. Os identificadores estão em `evidence/023/inputs.json`. A matriz com Google 0.32.0 foi executada localmente. A implantação desta rodada trocou exclusivamente o Meta.

Nenhum relatório de impacto é necessário para esses acompanhantes. O agendamento, a interface e a construção do diagnóstico são locais ao Meta. O resultado detalhado de uma tentativa de recuperação agora informa corretamente a falha nos campos existentes. Os 47 schemas de entrada, o schema de saída, os rótulos publicados e o contrato JSON de privacidade são idênticos aos da base. O consumidor do Core foi exercitado pelas suas próprias interfaces.

## 3. Mudanças e evidência

Solicitação de revisão de uma entrega de outro agente, sem novo identificador numérico atribuído. Foram reproduzidas oito asserções reprovadas na base, relativas aos comportamentos abaixo, e todas passam no alvo.

| Comportamento na 0.22.1 | Correção na 0.23.0 | Prova |
|---|---|---|
| Ao bloquear o reagendamento no WordPress, `meta/status` informava `scheduled=false` acompanhado de `code=ok`. A manutenção horária podia registrar `recovery=true` mesmo após duas tentativas recusadas. | A função que agenda o worker devolve o par resultado/código da mesma tentativa. A manutenção registra o resultado da conferência final. O estado observado antes de um reparo e a releitura posterior continuam distinguíveis. | Falha injetada no filtro real `pre_schedule_event`, segunda tentativa bem-sucedida, ausência de trabalho, recuperação autorizada e evento existente exercitados em WordPress. `regression-base.json` e `regression.json`. |
| A faixa **Primeiros passos** somava um token de uma conexão e ativos de outra. Também ocultava etapas com conexão pausada, token vencido ou dataset isolado sem conta de anúncios. | A prontidão local exige uma única conexão ativa, token com prazo local válido e ativo utilizável. O painel explica onde conferir o acesso efetivo. | Quatro estados incompletos e uma conexão pronta em Chromium. `settings-base.json` e `settings-final.json`. |
| Trocar a conta de anúncios durante a descoberta de datasets mantinha resultados desmarcados da conta anterior. Uma resposta atrasada podia repor a lista e o cursor antigos. | A troca descarta a paginação e as descobertas desmarcadas da conta anterior. Cada resposta é vinculada à solicitação que a originou. Seleções salvas e marcações pendentes permanecem na conexão. A orientação fica junto ao seletor e está associada a ele para tecnologia assistiva. | Casos A→B e A→B→A, resposta tardia, novo resultado utilizável e larguras 390/1440 px. Salvar pela REST real do WordPress e recarregar a tela confirmou os IDs escolhidos, a revisão e a preservação dos outros canais e conexão. `ui-assets.json`. |

Documentação operacional atualizada em ADMINISTRATION.md, WORKER.md e CHANGELOG.md. Os exemplos da versão foram capturados no WordPress descartável com o fornecedor simulado.

## 4. Instalação e prova da troca

**379 verificações próprias aprovadas na candidata.** São asserções executadas nos cenários abaixo. Os resultados da 0.22.1 e as leituras adicionais do site compartilhado ficam fora da soma.

| Cenário | Verificações aprovadas | Escopo |
|---|---:|---|
| WordPress limpo, apenas Meta | 233 | Funcionalidades, capacidade administrativa, REST, erros, histórico, exportação, datasets, documentos e integridade do runtime |
| Falha e recuperação do cron em WordPress isolado | 8 | Resultado do worker, tentativas e manutenção com e sem trabalho |
| Atualização direta semeada | 16 | Base e alvo em processos PHP distintos, persistência e reativação |
| WordPress com os seis plugins fornecidos | 44 | Ativação e identidade, 47 operações descobertas, dois consumidores Core, saúde, autoteste e os 32 documentos reconstruídos por meio do executor instalado do MCP em 51 páginas |
| Chromium | 28 | 13 verificações com renderer PHP e respostas REST controladas, 11 com login e REST local e atrasos de validação simulados, 4 de gravação e releitura real dos ativos com descoberta simulada |
| Integridade e geração documental | 50 | Limites de leitura, índice, UTF-8, regras positivas e negativas do build |
| **Total** | **379** | **Zero falhas na candidata** |

O build verificou a sintaxe de 35 arquivos PHP. Os 71 arquivos instaláveis são idênticos à árvore `plugin/wp-mcp-meta-fator3/` do fonte. As evidências detalhadas e instruções estão em `evidence/023/` e `tests/README.md`.

**Site-Teste.** Foram feitos backups privados das duas tabelas Meta e das oito opções do pacote antes da troca. O inventário ainda correspondia à base no instante anterior à operação. Foi usado `plugins/upload-base64` com `activate=true`, `overwrite=true`, slug e hash verificados e uma chave de idempotência. A operação `08155ae68b05357c3cea0dbf5ac9ca25` confirmou aplicação da 0.23.0, plugin ativo, nova requisição PHP e pré-imagem dos arquivos `4bcddc6513dd88143977154c`. A página inicial e a REST responderam HTTP 200 nas sondas internas antes e depois da instalação.

Após a troca, `system/health` retornou saudável, `meta/health` retornou `ok` e os oito itens de `meta/selftest` passaram. Os dois registros do Core 1.80.0 estão presentes. A descoberta retornou 47 operações Meta da 0.23.0. O schema e o índice de `meta/documentation` foram consultados, e os 32 documentos remotos foram lidos em 41 páginas e comparados, em conteúdo, à cópia do instalador. Travessia de caminho, continuação sem revisão e uso da revisão do manual WORKER da base produziram, respectivamente, `not_found`, `invalid_input` e `revision_conflict`.

O Site-Teste terminou com zero conexões e zero agendas Meta ativas e histórico de zero linhas. Os cenários sintéticos permaneceram em bancos descartáveis. Os registros operacionais da própria instalação, backups e auditorias de leitura permanecem no ambiente.

## 5. Banco, migração e correção por nova versão

A versão usa as tabelas, opções e formatos da base, sem migração de esquema. A prova de atualização comparou contagem e digest de 13 registros de negócio, quatro linhas de histórico e uma opção. Também conferiu a pausa e o cursor, concessão de monitoramento, políticas de retenção, agenda ativa, recibos e marcador parcial de migração de histórico. O novo valor de recuperação descreve a próxima manutenção executada e não reescreve o histórico.

Para recuperar dados, conservar banco e salts. Diante de falha operacional, registrar o estado da fila, os recibos e o resultado de cada tentativa. Uma correção após a instalação requer nova versão. A distribuição para a frota segue o fluxo raw com conferência de `expected_slug` e `expected_sha256`.

## 6. O que permanece pendente

- **Pedido MCP Meta 27 — dono/frota.** Homologar as permissões do aplicativo, a identidade, os ativos, as consultas e retornos reais da Meta em korvena.com.br e ctooffice.com.br, com as credenciais autorizadas. O Site-Teste está sem conexão Meta e a rodada não gerou requisições comerciais.
- **Frota.** Distribuição aos demais sites e publicação do instalador pelo fluxo habitual. O Google 0.32.0 foi exercitado na bancada nesta rodada. O Site-Teste utilizava Google 0.31.0.
- **Limites da prova.** O navegador foi Chromium com viewports de desktop e celular. Não houve teste em aparelho físico, leitor de tela, PHP 8.3.0 exato ou homologação funcional completa dos demais fornecedores.

## 7. Credenciais e configuração do dono

Para a atualização, conservar as configurações e chaves existentes. Para consultar a Meta, acessar **Ferramentas → Fator3 MCP Meta → Configurar → Conexão**, informar o nome, App ID, App Secret, token de usuário do sistema e validade UTC quando aplicável. Em **Ativos**, selecionar a conexão e os ativos autorizados. Para datasets, escolher a conta de anúncios antes da descoberta, marcar os datasets e salvar. A aba **Diagnóstico** permite confirmar o acesso da conta. Os campos e escopos de cada recurso constam da documentação instalada. O painel e a execução de operações de domínio exigem capacidade administrativa.

## 8. Identidade dos arquivos

| Artefato | Arquivo | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-meta-fator3-0.23.0-instalador.zip](wp-mcp-meta-fator3-0.23.0-instalador.zip) | 259876 | `0c5f029f8a167ac8f624c6386f13aaf9f388a8c228538bb623a58e8cebf60065` |
| Fonte | [wp-mcp-meta-fator3-0.23.0-fonte.zip](wp-mcp-meta-fator3-0.23.0-fonte.zip) | 769434 | `8de7518432457b90438280d0ec528224d1d61575a8a47912c797422909397332` |

O relatório externo registra a identidade final. A cópia no fonte é anterior ao fechamento e remete a este arquivo.

Conferidos os itens aplicáveis do checklist da seção 14. O relatório registra separadamente o conjunto testado localmente, o conjunto observado no Site-Teste e as pendências externas.
