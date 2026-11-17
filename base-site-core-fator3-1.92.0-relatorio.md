# Entrega — Fator3 Site Core 1.92.0

Revisão 1 · 17/11/2026 · Pedidos 426 e 427 · base-site-core-fator3

**Status: com-pendencias de observação.** Implementação concluída e instalada no Site-Teste. Migração 1.91.0 → 1.92.0 confirmada pelo executor, zero falhas. Aceite de 24 horas reais e de frota ainda aberto. Normas lidas integralmente: instrucoes-agentes-plugins-fator3.md e padrao-desenvolvimento-plugins-fator3.md, revisão 5 de 02/11/2026; também o padrão específico do Core e Regra comum vigentes no projeto.

## 1. Base, conjunto vigente e requisitos

Instalação nova ou atualização da 1.91.0. Requisitos: WordPress ≥ 7.1.4 e PHP ≥ 8.3 de 64 bits. Runtime validado localmente: WP 7.1.4, PHP 8.4.24 e MariaDB 11.8.6. Site-Teste: WP 7.1.4 e PHP 8.3.36. Não foi executado downgrade.

| Pacote | Versão integrada |
|---|---|
| Core | 1.92.0 |
| MCP | 0.46.0 |
| Google | 0.36.0 |
| Meta | 0.28.0 |
| LinkedIn | 0.25.0 |
| Pipedrive | 0.11.1 |
| WP Activity Log | 5.7.0 |

O Site-Teste também mantém WP Super Cache 3.1.5, Yoast 28.8, PublishPress Authors 4.20.0 e sua integração 2.0.3. Não houve troca dos pacotes acompanhantes. Contrato administrativo Core 8.44.0; dicionário de dados 8.39.0; perfil piso-padrao-3.6. Nenhuma tabela nova nesta versão.

Fonte base recuperado: base-site-core-fator3-1.91.0-fonte.zip, SHA-256 f780f372f3ffe1417a240eb94f9f2aa7329f5a1d0fb3e270ff6c600d40758f77. Instalador-base: 5.640.204 bytes, SHA-256 5d0358f62d42a9232ee1bce216bd8ea2b41ea284bc16ef454ad8f9c103aa3e41.

## 2. Pedido 426 — agenda completa

F3Base_Agenda_Filas cobre todo o prefixo f3base_, incluindo eventos únicos com record_id, migração, complementos e avisos, além das seis filas. Mantém gravação por delta com comparação atômica e a identidade timestamp/gancho/argumentos serializados. Falha real de persistência continua could_not_set; veto false ou WP_Error permanece veto.

Os observadores nulos conhecidos do WP Activity Log continuam executando. A proteção temporária conserva a decisão anterior, reposiciona o Core ao final dos filtros e devolve a identidade do observador antes de chamá-lo. Reconhece também a composição com WorkerCron do Meta 0.28.0. A alternância Core → Meta → Core foi exercitada. A proteção de antecipação sem trabalhador continua específica das seis filas.

agenda_das_filas declara cobertura f3base_*, a lista de ganchos, suporte a eventos únicos/recorrentes e identidade dos argumentos. No Site-Teste, os três filtros estão registrados e os quatro ganchos exemplificados pelo pedido constam da lista. Uma consulta pode mostrar callbacks registrados posteriormente; a reordenação efetiva é feita ao entrar na operação coberta.

## 3. Pedido 427 — identificação de aparelhos

A base Google Play permanece a referência de 15/11/2026: 44.528 códigos Model, SHA-256 74f0ced35bdfa216580c030477db29be01f5cc3e62e7196855c7519503d735bd. Revisão da regra: 2026-11-17.2.

Quando o nome ainda é técnico, são pesquisados outros modelos do mesmo Device. O candidato precisa ter nome comercial diferente de seu próprio Model e do código consultado. Grafia e sufixos regionais conhecidos são normalizados, preservando o sinal + como variante. Uma marca, um Device e um único nome comercial resolvem a identidade. Conflito conserva o código como modelo_ambiguo.

Resultado auditado: **1.939 decisões entre modelos — 412 nomes resolvidos e 1.527 ambiguidades**. A diferença em relação aos 2.449 citados no pedido está documentada pelos critérios de elegibilidade e pelas listas completas; não foi forçada uma contagem igual. A auditoria independente percorreu todos os 44.528 códigos e rastreou cada nome até a referência.

Foram aceitas **313 famílias** com pelo menos dois irmãos publicados, uma única marca/Device/nome e variação de uma letra regional final. Código ausente usa familia_google; entrada exata e correção local conservam precedência. Não há consulta externa durante a visita.

| Código | Ficha brasileira | Ano | Preço de referência |
|---|---|---:|---:|
| 25062rn2da | Redmi 15 | 2025 | R$ 1.500,00 estimados |
| lm-x420 | LG K40 | 2019 | R$ 200,00 estimados, usado |

As 30 fichas anteriores da frota permanecem byte a byte iguais nos seis campos comerciais. As 32 passaram pela projeção de perfis em WordPress real, sem nome ou ficha incompletos. Catálogo curado: 1.352 códigos. Fontes de pesquisa, fichas e listas de ambiguidades/famílias ficam em reference/427. O CSV integral e as auditorias são insumos internos do fonte, sem download avulso.

## 4. Impactos entre plugins

Os impactos 423 emitidos pelo Core 1.91.0 foram atualizados **nos próprios documentos**, revisão 2 em tests/191/impactos. A implementação foi incorporada pelos pacotes oficiais Meta 0.28.0 e LinkedIn 0.25.0; relatórios recebidos em reference/1920-companions. O aceite de 24 horas do 423 continua independente.

Não foi identificado novo pedido de desenvolvimento para MCP, Google, Meta, LinkedIn, Pipedrive ou Implantador nos itens 426/427. O acréscimo de diagnóstico é aditivo e o Core já está pronto. Nenhuma release de outro responsável foi modificada. Não há relatório de impacto externo novo apenas para informar versão.

## 5. Validação executada

| Ensaio | Resultado e limite |
|---|---|
| PHP | 609 arquivos aprovados em lint PHP 8.4.24 e TOKEN_PARSE PHP 8.3.36 no ZIP final |
| Instalação limpa local | 49 verificações aprovadas: inicialização, configuração, leitura, permissões e 32 perfis |
| Atualização local 1.91.0 → 1.92.0 | 49 verificações aprovadas com os seis pacotes Fator3 e WPAL ativos |
| Agenda local | 111 verificações aprovadas, incluindo record_id, recorrência, argumentos distintos, vetos em duas prioridades, falha de banco, seis filas e alternância com Meta |
| Controle 1.91.0 | Remoção já persistida reproduziu could_not_set; a mesma operação retorna confirmação na 1.92.0 |
| Concorrência nativa | 24 horas simuladas, 97 processos PHP CLI executando wp-cron.php, 194 chamadas HTTP de cron e 97 visitas; zero erro nativo de agenda |
| Transportes do laboratório | Um aviso Slack e um PageView CAPI aceitos por respostas locais simuladas; CAPI com uma tentativa; nenhuma chamada a fornecedor real |
| Diário de execução | Nenhum sucesso duplicado por gancho, horário da ocorrência e hash dos argumentos; reservas concorrentes preservadas |
| Google Play | 44.528 códigos, 256 fragmentos, 313 famílias; auditoria independente e recompilação idêntica de 259 arquivos de catálogo |
| Ativos públicos | 117 arquivos JavaScript/CSS idênticos aos da 1.91.0; nenhuma alegação de ganho de velocidade nesta rodada |
| Documentação | 197 abilities em cinco arquivos gerados do registro; índice, guia do agente e notas da release lidos integralmente via MCP |
| Site-Teste | 23 verificações de agenda em tabela temporária, catálogo e metadados aprovados; home, robots.txt e wp-cron.php retornaram HTTP 200 |

O relógio simulado não equivale a uma janela real. O executor de linha de comando usado foi PHP com o wp-cron nativo, não o comando WP-CLI. A primeira fixture CAPI sem decisão válida foi barrada; o ensaio aprovado inclui permissão sintética explícita no banco descartável. Nenhuma credencial ou mensagem real foi usada nos ensaios locais.

Evidências atuais: evidence/1920. Ensaios: tests/192. Provas em evidence/1910 e anteriores são históricas, não validações da 1.92.0.

## 6. Instalação e estado final do Site-Teste

Destino: fator3-teste-mcp-1.dreamhosters.com. ZIP transferido em blocos com comparação do hash anterior; total e SHA-256 confirmados antes de instalar. plugins/upload-base64 recebeu expected_slug e expected_sha256, ativou o pacote e confirmou 1.91.0 → 1.92.0. A troca começou em 17/11/2026 19:47:09 America/Sao_Paulo (Unix 1794955629). O executor confirmou conclusão às 19:47:16 (1794955636), zero falhas. Não houve alteração do instalador após essa homologação.

A leitura de log da janela inicial [19:47:09,19:49:11) foi completa: zero could_not_set, um arquivo examinado, 70 linhas e nenhuma linha não interpretada. A leitura posterior também encontrou zero fatal. Isso comprova apenas essas janelas curtas.

Na consulta de saúde de encerramento: nenhuma tarefa com última falha; robots.txt ainda constava como degradado por **aguardar nova confirmação HTTP do próprio Core**. A sonda retornou 200, mas não substitui o recibo dessa verificação. Essa pendência de pós-atualização acompanha a observação agendada.

A ferramenta temporária f3-qa-core-1920.php foi removida e a ausência do ZIP de staging foi confirmada (o instalador o consumiu). Nenhuma fixture está no instalador. Os ensaios remotos de agenda usaram tabela TEMPORARY e cache privado da conexão, sem disparar seus registros comerciais.

## 7. Pendências e aceite

- Janela real de 24 horas do Site-Teste: [1794955629,1795042029), de 17/11 19:47:09 a 18/11 19:47:09, America/Sao_Paulo. Conferência somente por leitura agendada para **18/11/2026 às 19:52:54**, com verificação de cobertura, trocas de versão, qualquer f3base_, duplicidades e pós-atualização. A tarefa anterior da 1.91.0 foi preservada; sua janela neste site foi interrompida pela atualização atual.
- Frota: o aceite em ctooffice, korvena.com.br e fator3.com.br deve começar após a troca de cada site. Nenhuma instalação em produção foi realizada nesta rodada. Zero por janela é o critério; ausência de registros sem cobertura não é prova de zero.
- Homologação com entrega externa a Slack/Meta continua distinta do transporte simulado utilizado no laboratório.

## 8. Identidade da entrega

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| base-site-core-fator3-1.92.0-instalador.zip | 5651480 | 28b2ec8cfc6e24622b2f30cae42582475ff246be493c2b604c86403f5964d7b5 |
| base-site-core-fator3-1.92.0-fonte.zip | 7739043 | e255339e738267714df9d1cdbea0a865cf85a1186a36c239acb428cc26c2e02f |

O instalador tem raiz única base-site-core-fator3, 1.268 arquivos e nenhum ZIP aninhado. Todos os bytes conferem com work/plugin/base-site-core-fator3. O fonte tem raiz base-site-core-fator3-1.92.0-fonte, manifestos, scripts, referências e evidências; sem dependências instaladas ou banco de laboratório. Não há commit Git nesta entrega.

Arquivos finais: [base-site-core-fator3-1.92.0-instalador.zip](sandbox:/workspace/scratch/bf416b7555b3/release/base-site-core-fator3-1.92.0-instalador.zip) e [base-site-core-fator3-1.92.0-fonte.zip](sandbox:/workspace/scratch/bf416b7555b3/release/base-site-core-fator3-1.92.0-fonte.zip).

## 9. Checklist de encerramento

Concluídos: leitura e precedência das normas; base/alvo e versões; requisitos e runtimes separados; fonte/instalador/relatório; documentação embarcada e acessível por MCP; instalação limpa e atualização; testes dos pontos afetados; integridade dos ZIPs; preservação dos 30 modelos; revisão dos impactos nos próprios documentos; limpeza dos temporários do Site-Teste; inventário final.

Pendentes: observação de 24 horas reais, confirmação de pós-atualização do robots e aceite de frota. Não aplicáveis: downgrade, suporte a versões antigas, publicação pública do fonte e mudança em pacotes de terceiros. A implementação está concluída; a entrega permanece com-pendencias até as comprovações operacionais acima.
