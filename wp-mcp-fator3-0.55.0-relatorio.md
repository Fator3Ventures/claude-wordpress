# Entrega — Fator3 MCP 0.55.0

20/11/2026 · Revisão 1 · Implementação e homologação · `wp-mcp-fator3/wp-mcp-fator3.php`

**Situação: com-pendencias.** O painel e a leitura dos avisos técnicos foram atualizados no Site-Teste. A seção 6 delimita as provas de transporte que o cliente remoto expõe.

## 1. De onde esta versão entra

Instalação nova ou atualização direta da 0.54.0. O instalador de referência tem SHA-256 `175b01ba1eeacc6655e739b70b694c2127c7df7e5858b180c773da8630392202` e o fonte `00822c5685b065e3badab94b22dde4a6972eca2dcfb4948ff84c8905e1dea57e`. Os bytes dos dois pacotes foram conferidos contra o relatório da entrega anterior.

O piso do projeto é WordPress 7.1.4 e PHP 8.3. A bancada executou WordPress 7.1.4, PHP 8.3.6 e MariaDB 11.8.6. O Site-Teste executou WordPress 7.1.5 e PHP 8.3.37. A projeção de dados também foi exercitada isoladamente em PHP 8.4.27. A rodada adotou `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos revisão 5 de 02/11/2026, a aba do MCP, a regra comum e os guias visuais de 20/11.

## 2. Convivência e encaminhamentos

Na bancada, o canal expôs as mesmas **172 habilidades próprias** da base, com os mesmos nomes e schemas de entrada e saída. A alteração do pedido 92 trata a apresentação do conteúdo devolvido pelo Core. O Core 1.100.1 já publica o inteiro e sua descrição nos dois schemas. Basta atualizar o MCP para completar a integração. O pedido 91 usa uma cópia local da folha comum 1.0.0. A carga e a ordem das folhas pertencem ao MCP.

O inventário do Site-Teste após a troca registrou Core 1.100.1, Google 0.43.0, Meta 0.32.0, LinkedIn 0.27.0, Pipedrive 0.12.0 e PublishPress Authors 4.20.1 ativos. Google e Meta foram atualizados por outras rodadas entre os inventários inicial e final. Neste ciclo, a prova funcional integrada cobre o Core. Nenhum acompanhante precisa de mudança para estes dois pedidos. A distribuição dos outros pacotes segue com seus responsáveis.

## 3. Mudanças por pedido e evidência

| Pedido | Implementação | Resultado |
|---|---|---|
| **Pedidos MCP 91 — interface** | Folha comum de 11.886 bytes carregada antes da folha do pacote, largura de 1320 px, título nativo, divisor do wp-admin, grupos e subabas com foco e quebra de linha. Formulários, seletores de autenticação, estados, cartões, tabelas e avisos utilizam os componentes do guia. Links diretos e ações dos formulários permanecem válidos. | Na base, o aviso real do PublishPress entrava no cabeçalho e levava o documento a 698 px nas sete subabas com viewport de 360 px. Na 0.55.0, as sete subabas mediram 360/360, 768/768 e 1440/1440 px (viewport/documento). O aviso do PublishPress ficou depois do divisor nos 21 cenários. O ensaio do Site-Teste aprovou as 203 verificações visuais aplicáveis. |
| **Pedidos MCP 92 — padrão de carência** | Em `SafeOutput::schema`, a regra exige `f3base/config-core-ler`, a opção explícita `f3base_avisos_tecnicos`, o descritor de tipo inteiro, a posição contratada em `schema` ou `schema_entrada` e um inteiro entre 0 e 10.080. | No Site-Teste, o padrão passou de `"[redigido]"` para `30` em ambos os blocos. Os dois schemas apresentam os 18 códigos. As quatro origens do valor continuam em 30, a resposta completa contém zero ocorrências da máscara e as duas representações JSON coincidem. |

A lista oficial de 20/11 atribui **91** ao painel e **92** à correção dos schemas. A referência a “91” no relatório imutável da 0.54.0 dizia respeito ao pedido **Core 439**, relativo à leitura do prazo nos dados da opção. As 72 verificações isoladas desta rodada exercitam extremos, descritores, vizinhos sensíveis e contextos alheios. Na configuração completa, a revisão opaca observada na 0.55.0 foi `6c0d4a7f6213885f3f57c350cc514ff75a5cc024eb7134b9a5f7b08721f3365d`.

## 4. Instalação e prova da troca

Envie o ZIP instalador e ative o pacote em uma instalação nova. Na frota, confira os bytes publicados na raiz raw do repositório, compare o SHA-256 da seção 8 e use `plugins/upload` com `expected_slug=wp-mcp-fator3`, `expected_sha256`, `overwrite=true` e `activate=true`. URL prevista após a publicação pela frota:

`https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-fator3-0.55.0-instalador.zip`

No Site-Teste, o ZIP seguiu em quatro partes, foi conferido no destino e aplicado por `plugins/upload-base64`. O primeiro recibo indicou um recurso ocupado. A repetição com a mesma chave releu o conflito. Outra consulta confirmou a base 0.54.0 saudável e zero recuperações pendentes antes da nova tentativa. A operação `86a8a6489df38df2d859050c0766ab9f` confirmou `version_before=0.54.0`, `version_after=0.55.0`, `active=true`, `applied=true`, `recovery_status=applied` e o SHA-256 do instalador. A pré-imagem tem ID `914b426681b626db9b95a5d5`. Home e índice REST devolveram HTTP 200 antes e depois.

| Ambiente | Cenário | Evidência |
|---|---|---|
| WordPress limpo e atualização | Instalação isolada, migração direta e preservação da configuração | 10 verificações na instalação limpa e 18 na migração. As árvores resultantes contêm os mesmos 482 arquivos e os mesmos bytes do ZIP final. |
| Transporte HTTP em WordPress | Leitura completa do Core antes e depois | 11 de 11 verificações em cada versão. As duas redações da base passaram a zero em `_meta["fator3/redaction"].total`. Os defaults dos 18 descritores foram comparados ao retorno nativo do Core. |
| Painel em dois esquemas de cores | Sete subabas em 360, 768 e 1440 px, com aviso de um segundo plugin ativo | 21 capturas de bancada. Dos 252 cruzamentos da matriz, 245 aprovaram o critério e sete eram verificações de toque inaplicáveis no desktop. Foram exercitados teclado, links sem JavaScript e paginação de 27 clientes sintéticos em páginas de 20 e 7. |
| Formulários e interações | Estrutura real e estados de ações | 109 verificações em 11 fluxos renderizados pelo WordPress. Em ensaio separado, oito interações no Chromium passaram com respostas AJAX simuladas. |
| Documentação e autorização | Build, leitura paginada e perfil restrito | 212 verificações documentais aprovadas. A bancada também conferiu nova versão/hash, recusa de acesso a configurações e HTTP 403 no painel de clientes para editor. Em `system/guide` no Site-Teste, três páginas reconstruíram os 2.207 bytes de `release-0550`, iguais ao Markdown do fonte, SHA-256 `98eff4b3b63a3d217983dc703ee95b5b7886bc97d6732e57360a5cb8538c2778`. |
| Rotas e prontidão | Rota principal e alias | A bancada registrou oito respostas 401, nos cenários anônimo e Bearer inválido das duas instalações. No Site-Teste, a sonda anônima retornou 401 nas duas rotas. `system/health {"compact":true}` informou versão 0.55.0, servidor saudável, marcador de cron ativo e zero recuperações pendentes. |
| Identidade e limpeza | CSS, ZIP e evidências | SHA-256 da folha comum instalada: `15ef0d932b1be12a541b8408b061ee276a4db9d6650476f92b5e2f41eefc0c2b`. O ZIP é reproduzível e os 474 arquivos PHP instaláveis passaram pelo lint em PHP 8.3.6. |

O [caderno visual](wp-mcp-fator3-0.55.0-caderno-visual.html) reúne a prova do painel. Os testes e resultados reproduzíveis estão em `tools/release0550/` e `evidencias/0550/` no fonte. O estágio do instalador foi removido e sua ausência foi confirmada. A moldura de teste temporária das capturas também foi removida e sua ausência, confirmada. Os recortes do Site-Teste mostram o cabeçalho, o aviso e a navegação. As capturas com os cartões e formulários preenchidos usam dados sintéticos da bancada.

## 5. Banco, migração e correção por nova versão

O schema de persistência segue em 2. A interface usa as opções e permissões existentes. A apresentação do valor padrão ocorre depois da leitura do Core. A migração de bancada verificou preferências, perfis, prazos OAuth e agendamento. A troca registra o recibo e a pré-imagem dos arquivos. Em caso de falha, consulte o estado da operação e preserve o recibo e os dados para uma correção em nova versão. Os seis bancos e instalações locais descartáveis foram removidos depois da validação.

## 6. O que permanece pendente

- **Pedido 92, evidência bruta no Site-Teste.** Os dois conectores do Site-Teste devolvem o texto e o conteúdo estruturado, mas omitem o membro externo `_meta`. As duas representações coincidiram e apresentaram zero máscaras. A prova direta do contador igual a zero foi executada no HTTP MCP autenticado da bancada com o ZIP final. O aceite desse membro especificamente no Site-Teste depende de uma leitura autenticada por um cliente que preserve o envelope MCP bruto.
- **Rotas no Site-Teste.** A sonda pública do próprio site recusa o cabeçalho personalizado `Authorization`. O ensaio com Bearer inválido está documentado em WordPress local. A conferência anônima das duas rotas foi executada no Site-Teste.
- **Frota.** A publicação e a implantação em produção cabem à frota. A observação histórica dos episódios do MCP 90 e dos avisos do Core 439 permanece com os responsáveis desses pedidos.

## 7. Credenciais e configuração do dono

O painel exige `manage_options`. A leitura usa uma conexão MCP autorizada para a opção do Core. Os dois pedidos utilizam as configurações existentes, sem credencial nova de fornecedor. Para conferir, abra **Ferramentas → Fator3 MCP** ou leia as notas com `system/guide`, documento `release-0550`.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-fator3-0.55.0-instalador.zip](wp-mcp-fator3-0.55.0-instalador.zip) | 979.524 | `360c254c583ffd78db8fc8fcdf0587a85a5c73f7bdbb634ee3ab6a890982bcac` |
| Fonte | [wp-mcp-fator3-0.55.0-fonte.zip](wp-mcp-fator3-0.55.0-fonte.zip) | 6.773.710 | `9aedd1ac21683eb1e957d057fd4117a79beae0784f7de009384a2ad7deb31544` |

Digest SHA-256 do inventário do runtime: `03125a8dfe3d850a085da38f44416d1238dc140d112397187b7cb1cc6f636843`. Relatório externo canônico. A cópia incluída no fonte foi congelada antes do cálculo de tamanho e hash desse arquivo.

Caderno visual: wp-mcp-fator3-0.55.0-caderno-visual.html, 5372537 bytes, SHA-256 `68b1412df02a64f6399e7cbfc30a59704ad27e28f96fb4f11bf7880163fa3cee`.
