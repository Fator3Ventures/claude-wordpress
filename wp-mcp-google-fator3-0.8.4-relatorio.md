# Fator3 MCP Google 0.8.4 — entrega e validação

12/10/2026 · Implementação integral do plano 0.8.4, revisão 2, pedidos Google 22 e 23. Uma única release. Base de ensaio: WordPress limpo ou Google 0.8.3; sem bloqueio no código pelo número da versão anterior.

## Resultado

A release corrige a detecção/reposição do evento executor e torna a configuração de serviços previsível: prévia, mescla explícita, comparação efetiva e confirmação obrigatória de reduções. O código dos plugins MCP e Site Core não foi alterado. Service Account continua sendo o padrão; OAuth permanece separado por aba.

### Evento executor e diagnóstico

- `google/status.cron.scheduling`, contrato **2.0.0**, consulta a agenda nativa atual e a intenção do ciclo de ativação. Distingue `present`, `missing`, `invalid`, `inactive` e `unknown`. Ausência não depende de erro histórico ou de haver jobs pendentes.
- `cron.health` pode ser `degraded` com `cron.work_health:idle`. O primeiro inclui problemas da agenda/observabilidade; o segundo descreve o trabalho. O histórico de uma gravação bem-sucedida não comprova que o evento continua presente.
- Consultas e carregamento do plugin não recompõem eventos nem convertem o formato legado do cron. Ativação, manutenção, observação CLI e execução admitida podem recompor o evento ausente, sem executar novamente o trabalho remoto.
- A reposição é restrita a `f3_mcp_google_jobs_tick`, intervalo de 60 segundos, argumentos vazios. Eventos MCP/Core permanecem independentes. Multiplicidade, formato inválido ou leitura inconclusiva não são corrigidos silenciosamente.
- A geração do ciclo, a trava e a guarda de recuperação impedem reparações obsoletas. Foi coberta também a desativação ocorrida enquanto outro processo já estava dentro do agendador nativo: esse processo remove sua gravação obsoleta e a próxima ativação estabelece a nova geração.
- Origens CLI/HTTP/manual e seus históricos permanecem separados. Atividade CLI recente, presença do evento e execução do callback são provas distintas.

### Configuração e painel

- Contrato de configuração **4.0.0**; `google/configure` aceita `dry_run` e `merge:true`. A resposta fornece os serviços efetivos antes/depois, alterações, revisão e hash da prévia.
- Sem `merge`, a seleção informada substitui o mapa completo, como antes. Omitir `services` preserva a seleção; `services:null` é inválido. Mescla vazia não altera a seleção. Substituição vazia desativa os serviços e exige confirmação quando houver redução.
- O diff considera a herança da seleção e os interruptores GA/Ads. Reduzir `write` para `read`, por exemplo, exige confirmação mesmo se os escopos OAuth não mudarem.
- Uma redução exige `confirm_service_reduction:true`, `expected_revision` e `expected_plan_hash`. A confirmação é vinculada ao pedido, ator, site, conexão e configuração corrente. Não pode ser reaproveitada depois de uma mudança relevante.
- A recusa acontece antes de gravar qualquer vínculo do pedido. A escrita continua verificada; valor igual, falha e restauração incerta conservam resultados diferentes. Não há anúncio de sucesso sem comprovação.
- O painel mostra a prévia e abre revisão específica para confirmar reduções. Formulários antigos são recusados. Modelos e controles de serviço utilizam o mesmo cálculo do diff.

Exemplo para acrescentar GTM preservando os serviços atuais:

```json
{"services":{"gtm":"write"},"merge":true,"dry_run":true}
```

Aplicar o mesmo pedido com `dry_run:false` e a `expected_revision` devolvida pela prévia. Se a prévia exigir confirmação, revisar o diff e incluir também `expected_plan_hash` e `confirm_service_reduction:true`. Não preencher automaticamente confirmações de reduções em um implantador.

### Contratos e distribuição

Permanecem **282 habilidades**, sendo 108 de leitura e 174 de escrita, e 34 opções. Todos os metadados `meta.fator3.version` indicam 0.8.4. Execução/catálogo 2.0.0, SDK `search-console-reader/1.0.0` e política MCP 1 foram preservados. Nenhuma habilidade ou serviço foi acrescentado/retirado nesta release.

README, changelog, contratos, guia, SDK, migração, validação e acompanhamento de cron foram atualizados. Os downloads autenticados foram comparados byte a byte com os documentos da release. O script Cloud Shell revisado continua disponível dessa forma; os originais ficam nos fontes. Nenhum script foi executado no Google Cloud.

O instalador contém **140 arquivos e 18 diretórios, todos com `index.php` silencioso**. Não contém Markdown, `docs/`, `reference/`, testes, histórico Git ou `.htaccess`. Os documentos são dados PHP protegidos para download autenticado. O pacote-fonte deve permanecer fora do diretório público do WordPress.

## Validação executada

Bancada descartável: **WordPress 7.1.2, PHP 8.3.6, MySQL 8.0.46, MCP 0.21.0 e Core 1.30.0**. Persistência, HTTP, painel, nonce, autenticação MCP, atualização de ZIP, cron e processos concorrentes reais; respostas Google simuladas.

| Verificação | Resultado |
|---|---:|
| PHPUnit 9.6.17, suíte completa | 1.113 testes; 12.636 asserções |
| Integração MCP/cron/configuração | 307 verificações, incluindo 282 de metadados das habilidades |
| Concorrência entre processos | 12 verificações |
| WP-CLI, HTTP cron e executor manual | 7 verificações |
| Retenção/isolamento de tokens MCP | 8 verificações |
| SDK e consumo pelo Core real | 24 verificações |
| Painel, pacote HTTP e exemplos dos contratos | 64 verificações |
| Atualização MCP primeiro | 14 verificações |
| Atualização Google primeiro | 14 verificações |
| Instalação limpa | 6 verificações |
| Total nativo, separado da suíte PHPUnit | **456 verificações** |
| Sintaxe PHP do código e testes | 178 arquivos aprovados |
| Documentação | 28 documentos, 111 links locais e 41 exemplos válidos |

As contagens não significam 456 cenários de negócio independentes: incluem verificações de metadados e exemplos. Os nomes de cada verificação constam em `wp-mcp-google-fator3/evidence/084` no ZIP fonte, junto ao log PHPUnit, resumo e auditoria do pacote.

### Matriz cruzada do plano

| Aceite | Evidência desta entrega |
|---|---|
| I01 — consultas sem reparação | `integration.json` |
| I02 — reparação somente Google | `integration.json`, `triggers.json` |
| I03 — ciclos independentes | `integration.json`, `concurrency.json` |
| I04 — prova atual separada de histórico | `integration.json` |
| I05 — disputa e reparação concorrente | `concurrency.json` |
| I06 — configuração pela ponte real | `integration.json`, `admin-package.json` |
| I07 — atualização nas duas ordens | `upgrade-mcp-first.json`, `upgrade-google-first.json` |
| I08 — retenção e pré-imagem Google | Ambos os relatórios de atualização |
| I09 — tokens MCP isolados | `token-isolation.json` |
| I10 — catálogo e autorização | `integration.json` |
| I11 — geração obsoleta e desativação | `concurrency.json` |
| I12 — ordem, atraso e divergência | `integration.json`, suíte `Release084Test` |

As atualizações ocorreram pela entrada HTTP autenticada do MCP, com nova requisição após cada troca. Preservaram cifras, seleção e vínculos. A retenção manteve a pré-imagem real do Google; a prévia de rollback continuou pronta depois da poda. Não foi executado rollback efetivo nem restauração de banco.

O instalador final tem exatamente o hash usado nesses ensaios, nos testes HTTP e na instalação limpa:

```text
f06474bcba158ef838450c2c7a95cbff3bc876c3ddcfa05e5a5434fce06940f7
```

### Insumos identificados

| Pacote | SHA-256 |
|---|---|
| Google 0.8.3 instalador | `1c60bc7bff22011c85e80a488a445c088cc3f12c6a99372fdcda67919b3dd9ce` |
| MCP 0.20.0 instalador reconstruído, igual ao hash publicado | `858b38b703cfebe110bbb61918ff412d0b36ce38467ce525ce4dc2bcae216f3d` |
| MCP 0.21.0 instalador | `6c1a788f6a11ad60b9fa53fda8a091ce11b74b1981f521c5d7d8c428fda47ce7` |
| MCP 0.21.0 fonte recebido | `4f1acff8cd3a1d3018cc961b6d9362deb0c11f41b7bfb3f81d4fe869fbac32a3` |

## Instalar

1. Manter backup conjunto dos arquivos e dados, credenciais e estado de recuperação, conforme `docs/MIGRACAO.md`. Caso haja migração ou recuperação pendente, concluir o procedimento correspondente antes de admitir trabalho remoto.
2. Instalar `wp-mcp-google-fator3-0.8.4-instalador.zip`, substituindo a 0.8.3 **sem desinstalar**. Em instalação limpa, ativar o plugin e configurar a conexão Service Account.
3. Reabrir o painel e atualizar a descoberta do catálogo no consumidor MCP. Conferir versão 0.8.4, contrato de configuração 4.0.0, seleção existente e `cron.scheduling.checks.executor`.
4. Se o evento estiver ausente, usar uma passagem admitida de manutenção/executor e conferir a pós-condição. A consulta de status, sozinha, não executa a reparação. Testar os recursos Google utilizados por meio de `google/selftest`, observando reprovação e cobertura incompleta.

Os testes de CLI utilizaram usuário WordPress autorizado e perfil MCP de manutenção na bancada. Um processo CLI observado não comprova que há crontab configurado no servidor.

## Limites da evidência

Não houve implantação em produção, uso de conta Google real, alteração de crontab hospedado, envio externo ou observação da frota. Não foram homologados multisite, Redis/Memcached reais ou Core 1.31.0, cujo pacote não estava disponível. O orçamento de manutenção é cooperativo; uma operação nativa já iniciada pode ultrapassar o prazo. Escritores externos que ignoram as travas podem alterar o estado depois de uma leitura confirmada.

O relatório MCP recebido continha fixtures do plano Google 0.8.4. Esta entrega acrescenta integração com os bytes finais do Google; não converte os ensaios anteriores em homologação de APIs Google reais.

## Arquivos

- `wp-mcp-google-fator3-0.8.4-instalador.zip`: pacote para WordPress.
- `wp-mcp-google-fator3-0.8.4-fonte.zip`: código, testes, documentação, scripts de referência, evidências, plano e histórico Git local.
- `impacto-google-0.8.4-para-mcp.md` e `impacto-google-0.8.4-para-site-core.md`: relatórios para os responsáveis pelos outros plugins, sem envio automático.
- `SHA256SUMS-google-0.8.4.txt`: hashes dos arquivos entregues.

