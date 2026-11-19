# Entrega — Fator3 MCP 0.52.0

19/11/2026, horário de Brasília. **Pedidos MCP 89**, vinculado ao pedido Core 433. Implementação oficial instalada no Site-Teste. O aceite do MCP foi reproduzido com uma recusa controlada de agendamento Meta.

## 1. Base de migração

A versão admite instalação limpa e atualização direta testada da 0.51.0. Instalador da base: SHA-256 `d6016b33abbf3567c5c7c025e400d6ef4802b2adb4993b37bd8212b7e1042394`. Requisitos mínimos: WordPress 7.1.4 e PHP 8.3. Bancada com WordPress 7.1.4, PHP 8.4.24 e MariaDB 11.8.6. Site-Teste com WordPress 7.1.5 e PHP 8.3.36. As duas regras centrais foram relidas na revisão 5, de 02/11/2026, com a regra comum e o padrão específico do MCP.

## 2. Convivência e encaminhamentos

O WordPress registrou 172 habilidades próprias nas duas versões. Nenhuma habilidade foi adicionada ou removida. A descrição e o schema de saída de `system/health` passaram a documentar o bloco opcional. Os schemas de entrada das 172 habilidades continuam idênticos. Slug, arquivo principal, metatools, permissões de administração e rotas MCP foram preservados.

A bancada e o Site-Teste usaram Core 1.97.2, Google 0.40.0, Meta 0.30.0, LinkedIn 0.26.0 e Pipedrive 0.12.0. O produtor do contrato é o Core 1.97.2. Quando instalado antes do canal, começa a contar episódios imediatamente. O MCP 0.52.0 passa a exibi-los assim que encontra o filtro. A instalação isolada do MCP mantém o diagnóstico próprio. Nenhuma alteração foi necessária nos quatro provedores de domínio.

A revisão 3 do encaminhamento do Core identificou o ponto de integração em Diagnostics::health. A incorporação oficial e o retorno para o mantenedor estão no arquivo [wp-mcp-fator3-0.52.0-impacto-base-site-core-fator3.md](wp-mcp-fator3-0.52.0-impacto-base-site-core-fator3.md). A cópia do fonte é `docs/IMPACTO-CORE-0520.md`.

## 3. Mudança e evidência

Na 0.51.0, o diagnóstico compacto descrevia somente o marcador do próprio canal. Um erro de um pacote de domínio podia aparecer no diário do Core sem aparecer ali. A 0.52.0 lê o filtro `f3base_cron_incidentes_24h_v1` sob a capacidade `manage_options` e inclui o resultado em `incidents_24h.pacotes_fator3`. O mesmo bloco pode ser consultado na resposta completa, com `compact=true` ou com `fields=["incidents_24h"]`.

| Campo | Significado |
|---|---|
| `episodios` | Número de aberturas registradas pelo Core na janela móvel de 24 horas. A recuperação de um worker mantém a abertura na contagem até a saída da janela. |
| `ultimo_em` | Instante Unix da abertura mais recente. É nulo quando a contagem é zero. |
| `detalhe` | Nome da operação do Core com o histórico técnico, atualmente `f3base/incidentes-tecnicos-ler`. |

O MCP preserva as categorias e a cobertura do marcador do canal. Filtro ausente ou retorno nulo conservam as respostas da versão anterior. Uma leitura que pede apenas outro campo dispensa a consulta ao Core. A projeção seleciona as três chaves do contrato e mantém a guarda de 1.850 bytes do diagnóstico compacto, antes dos metadados de despacho.

**Prova no Site-Teste.** Antes do ensaio, a contagem era zero. O agendamento de `f3_meta_hml_mcp052_episodio` recebeu `could_not_set` às **13h39min23s de Brasília**. O instante `1795106363` coincidiu no diário do Core e nas três consultas ao MCP. O detalhe confirmou o gancho e zero entregas pendentes. A resposta compacta medida ocupou **991 bytes** em JSON sem indentação. O ensaio usou um gancho exclusivo e interceptou sua mensagem técnica. A remoção do auxiliar e de seu episódio levou a contagem de volta a zero. A consulta final encontrou zero linhas do teste no diário e zero opções de controle do ensaio. O pacote oficial contém somente a integração de leitura.

**Bancada.** Os seis prefixos cobertos pelo Core produziram seis aberturas. A segunda recusa no mesmo gancho e dia foi deduplicada. Um gancho recuperado continuou contado e uma abertura anterior às 24 horas saiu da janela. Em WordPress sem o Core, cinco formas de consulta reproduziram exatamente a 0.51.0. O teste também verificou retorno nulo, contagem de 64 bits, ausência de campos adicionais e recusa à conta de editor.

## 4. Instalação e prontidão

Em nova instalação, envie o ZIP instalador, ative o plugin e abra **Ferramentas → Fator3 MCP**. Para distribuição, a frota confere os bytes publicados e usa `plugins/upload` com `expected_slug=wp-mcp-fator3`, o SHA-256 da seção 8, `overwrite=true` e `activate=true`. Endereço previsto após publicação:

`https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-fator3-0.52.0-instalador.zip`

O Site-Teste usou `plugins/upload-base64` com o ZIP transferido por partes e conferido por SHA-256. A operação `a472750ea6eb835c59103c69d7b3975e` informou versão anterior 0.51.0, versão final 0.52.0, `applied=true`, `active=true` e `recovery_status=applied`. A pré-imagem de arquivos recebeu o ID `f29be121dba5afd83109dfad`. Página inicial e índice REST responderam 200 antes e depois. O arquivo de estágio e o plugin de ensaio foram removidos. O executor mantém seus recibos e pré-imagens segundo a retenção do site.

| Verificação | Resultado |
|---|---|
| Saúde | Nova requisição com `healthy=true`, ferramentas prontas, marcador de cron `current_state=active` e zero recuperações pendentes. |
| Autenticação das duas rotas | Na bancada, HTTP 401 em ambas as rotas tanto sem credencial quanto com bearer inválido. No Site-Teste, a sonda anônima devolveu 401 nas duas rotas. Também no Site-Teste, quatro requisições públicas POST chegaram ao WordPress e receberam 401 com desafio Bearer, cobrindo os dois casos em cada rota. Na primeira tentativa externa, o alias havia retornado 503 para o bearer inválido. A repetição do teste completo confirmou 401 nas quatro chamadas. |
| Migração e isolamento | Ativação isolada e atualização do ZIP anterior com a coorte. Conexão, permissões, preferências e vencimentos OAuth anteriormente gravados conferidos em novo processo. |
| Documentação | Índice, descoberta e schema lidos no Site-Teste. As duas páginas de `system/guide` para `release-0520` recompuseram os 1815 bytes da fonte, SHA-256 `74816af151540df967017a570f65ea34ad257abedbd497f5964b49d518cf06e9`. O teste de atualização detectou o hash obsoleto. A leitura documental em bancada recusou acesso indevido e não fez chamadas ao fornecedor. |
| Painel | Sete abas conferidas em 360, 768 e 1440 px. As 21 capturas e medidas estão em `evidencias/0520/painel/` e `painel.json`. |
| Pacote | 474 arquivos PHP passaram no lint. As duas árvores instaladas foram comparadas byte a byte com os 481 arquivos do ZIP. O verificador documental concluiu 204 verificações. |

Os resultados e os procedimentos estão em `evidencias/0520/` e `tools/release0520/` no fonte. Os testes CLI da bancada usaram PHP 8.4.24. O caminho administrativo em PHP 8.3 foi exercitado no Site-Teste.

## 5. Banco, migração e correção por nova versão

A alteração lê o diário do Core. O schema 2 do canal permanece vigente. A instalação libera a projeção sem regravar os incidentes, alterar as agendas ou recalcular vencimentos OAuth. O Core mantém o histórico e sua política de retenção. A pré-imagem do executor cobre arquivos do plugin. Uma correção posterior à instalação exige uma nova versão.

## 6. Aceites pendentes

**Pedidos MCP 89 concluído no Site-Teste.** A distribuição da 0.52.0 aos demais sites compete à frota. A janela de 72 horas em 12 sites prevista para o pedido Core 433 continua sob responsabilidade da frota e mede o comportamento real dos workers. O ponto de integração solicitado ao MCP está encerrado. Os aceites de campo de versões anteriores seguem no estado da frota conforme a regra do arquivo de pedidos de 19/11.

## 7. Credenciais e configuração do dono

A integração reutiliza o acesso administrativo existente. O operador pode consultar a contagem sem configurar uma credencial de fornecedor ou alterar a agenda. Uma conta sem capacidade administrativa recebe recusa em `system/health`. A versão não requer mudança nos perfis OAuth ou nas senhas de aplicação. O fonte é entregue ao dono conforme o padrão central de publicação.

## 8. Identidade dos arquivos

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-fator3-0.52.0-instalador.zip | 970642 | `44e5cfbff907a50cfd50ee4c5d5789055393f4965931d54ae24b09c60c4f8e9f` |
| wp-mcp-fator3-0.52.0-fonte.zip | 5251471 | `ae24e51083ab4ff6f0591ca43d008562d8efca783fb6054cc2d722a8b665f0de` |
| wp-mcp-fator3-0.52.0-impacto-base-site-core-fator3.md | 1908 | `ce82ea45f85b7daca64c5c1f675f7725bafe4aada15521f4a7a753bcffac5e83` |

Digest do inventário de runtime: `97222f0cfa907ce0f2d8ff7c95b3e0fd722fe1f60d775f41f5e478663dd3a499`. Relatório canônico externo: `wp-mcp-fator3-0.52.0-relatorio.md`.

O instalador reconstruído a partir do ZIP fonte entregue reproduziu integralmente os bytes e o digest do instalador acima.
