# Fator3 Site Core 1.80.0 — relatório de entrega

**Resultado.** O Core 1.80.0 está ativo no Site-Teste. A atualização direta da 1.79.0 foi concluída e confirmada pelo executor. Cabeçalhos públicos, navegação e conta Pipedrive retornaram verificados na rotina de pós-atualização. Nenhum site de produção recebeu esta versão nesta rodada.

## Escopo e entradas

Rodada nova sobre o instalador e o fonte da 1.79.0 implementada por outro agente. Foram conferidos os oito ZIPs fornecidos, os relatórios Core, MCP, LinkedIn, Pipedrive, o impacto Pipedrive revisão 2 e as quatro comparações de interface 1.78.0/1.79.0. A lista com tamanhos e SHA-256 está em `evidence/1800/entradas.json`. Base Core recebida de 4.405.963 bytes, SHA-256 `111e639d652f3cd99411130e454fdf2c6a2e5ab7c5b3d8f524bf8a37398a067f`. Fonte da base com SHA-256 `c60c35c6fcfb9ac0b1122b9aa8832814542e6ca2c1244480aee817dd8b458afe`.

A implementação seguiu `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos na revisão 5 de 02/11/2026, lidos integralmente. As cópias do fonte coincidem byte a byte com as fontes do projeto. O incremento de minor identifica a nova rodada. Versão mínima declarada em cabeçalho e documentação: WordPress 7.1.4, PHP 8.3 de 64 bits. Baselines operacionais: instalação nova ou atualização da 1.79.0. Basename preservado: `base-site-core-fator3/base-site-core-fator3.php`.

## Correções e efeitos observáveis

| Área | Falha reproduzida ou verificada no código | Correção e prova |
|---|---|---|
| Inicialização com WP Super Cache 3.1.5 | Ao registrar a própria desinstalação, o provedor atualizava uma opção no carregamento dos plugins. O callback global do Core consultava o diagnóstico pós-atualização, que podia chamar `wp_salt()` antes de sua definição. O caminho dependia de um recibo de cabeçalhos já existente. | O observador de opções em `bootstrap-hooks.php` e em `class-f3base-configuracao-medicao.php` só reage a opções com aviso persistido ativo. Uma reavaliação pertinente durante o carregamento é agrupada para `init`. A primeira carga passou com o fornecedor real e a gravação de uma opção alheia fez zero leituras do estado pós-atualização. O painel preserva os diagnósticos dinâmicos. |
| Duas sessões de edição | A renovação AJAX podia recusar um formulário quando outra sessão havia alterado uma opção diferente da mesma área. | A renovação valida usuário, permissão, nonce e prazo. O POST confere a revisão de cada opção efetivamente editada e conserva a escrita condicional no banco. No navegador, opções distintas persistiram. Na mesma opção, a segunda gravação mostrou o conflito e o banco reteve o primeiro valor. Subcampos da mesma opção compartilham a revisão. |
| Formulário público e atribuição | O caminho do Referer já traz o prefixo do WordPress em subdiretório. Reconstruir a URL com o caminho inteiro repetia o prefixo. Um ID zero também permitia a resolução implícita do post global. | O post publicado identificado pelo token tem prioridade. Na ausência da página, o fallback aceita o caminho da própria instalação e separa a página armazenada da URL usada na atribuição. Testes cobriram subdiretório, consulta de campanha, slug com ponto codificado, travessia, controles, barra invertida, outro host e ID zero. |
| Painel e links internos | Abrir a área Contato da 1.79.0 com `#%ZZ` gerou uma exceção JavaScript observada no Site-Teste. | A resolução de fragmentos ignora escapes inválidos e reabre os ancestrais recolhidos ao navegar pelo histórico. O mesmo endereço na 1.80.0 carregou com HTTP 200, sem o erro, sem transbordamento horizontal a 390 px e com Salvar visível. |
| MCP 0.44.0 | A classificação de escrita de `f3base/config-core-escrever` dependia da interpretação do transporte. | A anotação agora explicita `readonly=false`. O schema efetivo foi consultado via MCP. A simulação de uma alteração retornou `persisted=false`; a releitura confirmou o mesmo valor e a mesma revisão. |

A diferença entre “Restringir o histórico” e “Exibir e permitir reenvio do histórico” nas capturas é uma escolha persistida por site. No laboratório, as duas escolhas foram gravadas e relidas pela interface e o valor inicial foi restaurado. O Core não força uma delas na atualização.

## Testes próprios da versão entregue

| Cenário | Resultado |
|---|---|
| WordPress nativo descartável 7.1.4, PHP 8.3.6, MySQL 8.0.46 | 425 asserções na fase limpa e 430 na atualização da 1.79.0. A segunda contagem inclui os testes da primeira fase repetidos sobre a base migrada. As duas terminaram com desinstalação e reativação no ambiente descartável. |
| Integridade de dados | 993 amostras sintéticas de Web Vitals e a configuração de contato conservaram os hashes na migração. A suíte verificou a política de recriação das tabelas operacionais após desinstalação. |
| Instalação limpa pelo ZIP final | Plugin_Upgrader aplicou o instalador. Em um processo novo, o Core estava ativo, o ciclo estava concluído e os 955 arquivos instalados coincidiam com o manifesto. |
| Catálogo e documentação | 193 habilidades registradas. Todas as 102 de leitura foram executadas em cada fase. Em cada uma, houve 66 retornos de sucesso e 36 recusas controladas por condições ou parâmetros. Zero exceções, avisos ou depreciações PHP nessa varredura. Catálogo e referência conferidos com o registro. Auditoria local com 146 Markdown em docs/, zero arquivos fora do índice e zero referências quebradas. |
| Painel | 11 verificações em Chromium, desktop 1440 px e celular 390 px. Gravação concorrente, conflito, aviso ao operador, seleção de histórico, botão e índice responsivos. Observação autenticada adicional no Site-Teste nas duas versões. A varredura de 23 telas da entrega anterior é histórica. |
| Pipedrive 0.9.0 | 31 verificações próprias nas três suítes do emissor, usando o cliente real do Core e respostas HTTP sintéticas. Orçamento, prévia, aplicação, recibo e repetição. HTTP 2xx com JSON ilegível ou mais de 512 KiB resultou em incerteza persistida e nova consulta sem reenvio. |
| LinkedIn 0.20.0 | 37 verificações no teste oficial do pedido 369 com o SDK real e provedor simulado: autorização, descoberta, captação, deduplicação, revogação e preservação dos contatos. MCP 0.44.0 e Pipedrive 0.9.0 ativos no mesmo WordPress. |
| Yoast 28.8, PublishPress Authors 4.18.0 e WP Super Cache 3.1.5 | Conferência dos três ZIPs por SHA-256. Duas respostas HTTP públicas de artigo, com e sem PublishPress, com seis condições aprovadas por resposta. Reaquecimento confirmado com uma cópia anônima HTTP 200. Grafo misto reproduzido no tema do Implantador 2.20.0 e correção exercitada em cópia. |
| Build | Lint PHP nos 597 arquivos do runtime. Os 955 arquivos do instalador foram conferidos por nome, ordem e SHA-256, sem divergência. Há 926 arquivos idênticos à base, 27 alterados e dois novos documentos. A árvore pública assets/ e as bibliotecas de e-mail conservaram os bytes da 1.79.0. |

A verificação de sintaxe e as suítes funcionais pertencem a esta rodada. A triagem PHPCS da 1.79.0 permanece histórica. Esta rodada não mediu latência de produção, não repetiu a prova específica de regras Apache com prefixo personalizado e não testou Firefox ou Safari.

## Site-Teste e documentação operacional

O site estava em Core 1.78.0 no início da rodada. O instalador oficial recebido levou o site até a 1.79.0. A candidata inicial que ainda tinha o defeito de inicialização foi interrompida **antes de instalar**. A transferência parcial foi cancelada. O ZIP definitivo levou o site diretamente da 1.79.0 à 1.80.0 com slug e SHA-256 esperados e sondas públicas aprovadas antes e depois. Uma tentativa de login do navegador retornou HTTP 503 durante a homologação; a repetição autenticada carregou Contato com HTTP 200. A conta sintética de teste foi removida, a consulta por ID confirmou sua ausência e os dois ZIPs temporários já não estavam no diretório de atualização. O site manteve os acompanhantes ativos.

| Ativo no Site-Teste | Versão |
|---|---|
| Core / MCP / Google | 1.80.0 / 0.44.0 / 0.31.0 |
| LinkedIn / Meta / Pipedrive | 0.20.0 / 0.21.0 / 0.9.0 |
| Yoast / PublishPress Authors / WP Super Cache | 28.8 / 4.18.0 / 3.1.5 |

A descoberta retornou a habilidade `f3base/documentacao-ler` da 1.80.0 e 208 arquivos consultáveis pelo índice. A leitura de cinco documentos completos comparou texto e SHA-256 com o instalador. O índice teve 305 linhas em seis páginas e o guia do painel, 83 em duas páginas. Também foram lidos integralmente o guia do agente, as notas da release e as instruções de operação. Um arquivo inexistente retornou `documento_nao_catalogado`. O catálogo descreve os pré-requisitos, exige `manage_options` e orienta ler, simular, aplicar e reler a opção. Os recibos sanitizados estão em `evidence/1800/site-teste.json` e `config-simulacao.json`.

A rotina do Core confirmou a identidade da conta Pipedrive. A consulta `pipedrive/status` do consumidor, por sua vez, retornou `operacao_nao_autorizada` conforme a configuração comercial do Site-Teste. O teste preservou essa autorização. Não houve escrita comercial em CRM nem importação de leads reais para homologar esta versão. O LinkedIn respondeu ao status no Site-Teste. O exercício funcional de CRM e Lead Sync usou o fornecedor simulado. Google e Meta foram conferidos no inventário ativo, sem homologação de suas APIs externas nesta rodada.

## Contratos, impacto e implantação

Contrato administrativo 8.38.0, perfil piso-padrao-3.6 e contrato pipedrive-api-client/1.0.0. A revisão 2 do impacto Pipedrive fica atendida na fronteira testada. O controle de autorização e orçamento pertence ao Core. O consumidor Pipedrive persiste a incerteza e impede reenvio. As implementações dos acompanhantes fornecidos foram examinadas sem encontrar leitor direto dos arquivos `docs/dados/abilities-N.json`. Clientes externos que leem esses arquivos diretamente não foram inventariados.

A revisão 3 do impacto no Implantador registra a reprodução em 2.20.0 e a prova do patch. Cabe ao mantenedor do Implantador incorporar e distribuir a mudança no tema para preservar o crédito de WebPages de terceiros em grafos mistos. O patch está em `impactos/implantador-2.20.0-grafo-misto.patch` no fonte. Esse encaminhamento já existia na 1.78.0. Nenhuma atualização coordenada de MCP, Google, Meta, LinkedIn ou Pipedrive é requisito para corrigir o Core.

Para implantar na frota, usar o instalador e a identidade abaixo. Conferir plugin ativo, versão e recibo de pós-atualização em `f3base/resumo-operacional-ler`. As opções e credenciais existentes são preservadas. Não há campo novo a preencher. A decisão e a distribuição em produção continuam com a frota. O ZIP foi transferido diretamente ao Site-Teste por partes com verificação de hash. Um repositório raw público não foi usado nesta rodada.

## Identidade dos artefatos

| Artefato | Bytes | SHA-256 |
|---|---:|---|
| base-site-core-fator3-1.80.0-instalador.zip | 4.416.884 | `2e81a04d0a9f99f1607d5b388c4aa2590bcc0b3b853cda1fa1b7b3530302ec72` |
| base-site-core-fator3-1.80.0-fonte.zip | 32.976.499 | `048875c5f2a7e94d07765e95da61088cf2806f621b91707d30cdf351babd13eb` |

Relatório externo canônico, emitido após o fechamento e a conferência dos dois ZIPs.

## Encerramento

A seção 14 do padrão foi conferida. O Core foi implementado, empacotado, instalado e validado no Site-Teste. O fonte inclui runtime, base de migração, testes, provas, build e encaminhamentos. O instalador contém somente a árvore do plugin e a documentação instalada. As ações remanescentes pertencem à frota para distribuição, ao mantenedor do Implantador para a ponte editorial do tema e ao dono da conta Pipedrive caso deseje homologação comercial.
