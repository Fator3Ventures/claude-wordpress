# Entrega — Fator3 MCP 0.49.0

Revisão 1 · 18/11/2026 · Implementação e homologação · Com pendências operacionais na frota.

O MCP 0.49.0 corrige o registro da rota principal e do alias quando o WordPress inicializa o REST antes da criação do transporte. A edição foi instalada no Site-Teste. As leituras autenticadas das 18h29 e das 18h38 de São Paulo confirmaram ambas as rotas registradas, as ferramentas prontas, o marcador de cron ativo e a saúde positiva. Foram lidos integralmente instrucoes-agentes-plugins-fator3.md e padrao-desenvolvimento-plugins-fator3.md, ambos na revisão 5 de 02/11/2026, a regra comum, a aba MCP, o pedido MCP84 e o impacto do Core 1.94.0 revisão 2.

## 1. De onde esta versão entra

Instalação limpa ou atualização direta da 0.48.0 oficial. SHA-256 do instalador da base: 3ace23b8e4405d0444048fcbddd51479ee63dee3c49d4373760151ef8b67d28f. Requisitos do projeto: WordPress >= 7.1.4 e PHP >= 8.3. Execução efetiva em WordPress 7.1.4 com PHP 8.3.6 e 8.4.27 e MariaDB 11.8.6 na bancada e WordPress 7.1.5 com PHP 8.3.36 no Site-Teste. Slug e basename: wp-mcp-fator3 e wp-mcp-fator3/wp-mcp-fator3.php.

## 2. Convivência e encaminhamentos

| Pacote | Bancada integrada | Site-Teste na homologação |
|---|---|---|
| Site Core | 1.94.0 | 1.94.0 |
| Google | 0.37.0 | 0.36.0 |
| Meta | 0.29.0 | 0.29.0 |
| LinkedIn | 0.26.0 | 0.26.0 |
| Pipedrive | 0.12.0 | 0.11.1 |

A matriz da bancada usou os instaladores identificados em evidencias/0490/bases.json. O inventário real do Site-Teste está em site-teste.json. Google e Pipedrive estavam em versões diferentes das referências da bancada. A ação de instalação desta rodada atualizou somente o canal. A release foi exercitada também sem acompanhantes. APIs comerciais e o Implantador ficam fora da mudança.

MCP84 / Core430. O Core 1.94.0 já usa o SDK de registro de forma passiva. O MCP incorpora a inscrição tardia do transporte proposta pelo Core. Na distribuição coordenada, usar o Core 1.94.0 e o MCP 0.49.0 para obter as duas partes da correção. O Site-Teste já estava com o Core 1.94.0 antes da troca do canal. A revisão 2 do impacto registra a incorporação da correção e a observação operacional que cabe à frota. [Impacto no Site Core](https://chatgpt.com/library?file_id=libfile_fde3_f-eb477343ece081918ebdffe194aff0dd_32706b9c47908191baafe72f89b6caee&account_id=personal)

## 3. Mudanças e evidência

**Pedidos MCP 84 / Core 430.** O construtor em core/includes/Server/Transport/HttpTransport.php agenda o registro na prioridade 16 quando essa etapa é futura. Após a conclusão do hook, ou já na prioridade 16 ou superior, chama a rotina existente imediatamente. A rotina preserva a propriedade de cada rota e os callbacks de permissão. A versão mantém as duas rotas, os três metatools existentes e o catálogo de 172 habilidades próprias. A documentação instalada passou a incluir release-0490 e as instruções de atualização indicam a base e o instalador corretos.

| Cenário em processo novo | Resultado |
|---|---|
| 0.48.0, REST iniciado por terceiro durante init na prioridade 5 | Servidor e ferramentas prontos, mas ambas as rotas ausentes, com mcp_route_missing |
| 0.49.0, observador do próprio Core | O observador conservou o REST sem inicializar nessa etapa. Registro completo ao fim |
| 0.49.0, terceiro inicia REST antes do adaptador | Duas rotas presentes e sem conflito |
| 0.49.0, transporte criado nas prioridades 10, 16 e 21 do hook REST | Registro completo nos três casos e um callback na rota primária |
| 0.49.0, terceiro ocupa rota principal | Callback preservado, diagnóstico mcp_route_conflict e alias registrado |

A prova identifica uma causa suficiente da falha na base. A identificação do produtor de cada incidente antigo depende de telemetria histórica. A regressão na base e os seis cenários do candidato deram o resultado esperado em PHP 8.3.6 e 8.4.27 com WordPress 7.1.4. Os casos estão em tools/release0490 e os resultados em evidencias/0490/ordem-php83.json e ordem.json. O WordPress também emitiu avisos de registro de tema no ensaio que força a inicialização precoce.

## 4. Instalação e prova da troca

No Site-Teste foi preparado um ZIP temporário em wp-content/upgrade. A finalização conferiu os 964290 bytes e o SHA-256 da seção 8. A habilidade plugins/upload-base64 recebeu zip_path, expected_slug=wp-mcp-fator3, expected_sha256, activate=true, overwrite=true e tempo de 30 segundos por sonda. Operação 403631cc11e3010fd9a413fe6d4515cd. A resposta registrou 0.48.0 → 0.49.0, plugin ativo, applied=true, recovery_status=applied e aprovação das sondas anterior e posterior. O caminho temporário já estava ausente na conferência final. Para a frota, o fluxo previsto é publicar o instalador e relatório, conferir o hash servido na URL raw e aplicar por plugins/upload com o slug e o hash finais.

| Prova | Resultado e limite |
|---|---|
| Instalação limpa e migração em laboratório | Ativação do ZIP final sem acompanhantes e atualização com o conjunto integrado. Sete verificações aprovadas na instalação limpa e dez na migração da base completa. Nos três ensaios, os 481 arquivos instalados coincidiram byte a byte com o ZIP. |
| Acesso HTTP às rotas | No WordPress local, as duas rotas responderam 401 sem credencial e com Bearer inválido. No Site-Teste, a sonda confirmou 401 sem credencial em ambas, com bypass de cache. A sonda recusou o cabeçalho Authorization para o teste remoto com Bearer inválido. |
| Registro e saúde no Site-Teste | Requisição autenticada em processo posterior, MCP 0.49.0 e Core 1.94.0. Servidor e ferramentas presentes, duas rotas registradas, cron active e zero recuperações em aberto. |
| Ajuda instalada pelo MCP | Descoberta de system/guide, índice com a nota corrente e documento release-0490 remontado em três páginas. Os 2111 bytes coincidiram com o Markdown canônico, SHA-256 3efcc77d1f3f16698ac5186ba74b3ad4c2ae2275b98f72c4578ca03580e58464. ID ausente recusado. |
| Painel de manutenção | Capturas do wp-admin local em 360, 768 e 1440 px. Página e seção couberam nas três larguras. Os seis campos numéricos tinham rótulo e texto de ajuda associados. Imagens e medidas em evidencias/0490. |
| Build | 201 verificações documentais aprovadas, lint nos 474 PHP, CRC e manifesto conferidos. Rebuild byte a byte idêntico. |

O primeiro ensaio de migração teve 9 de 10 verificações aprovadas. O preparo instalava isoladamente o carregador da sentinela e omitia seu diretório de recuperação. Reproduzimos o mesmo diagnóstico na 0.48.0 antes da troca. Em outro banco, uma operação nativa de recuperação da base preparou o diretório e a sentinela. A saúde da recuperação estava normal antes e depois da atualização. Os resultados das duas preparações estão em evidencias/0490/preparo-recuperacao.json.

Somente o laboratório recebeu a fixture que altera a ordem de inicialização. O Site-Teste manteve a fila do Core e os estados observados entre as duas leituras. Evidências sanitizadas em evidencias/0490.

## 5. Banco, migração e correção por nova versão

O schema de dados permanece 2. A correção usa o estado do hook na requisição corrente e dispensa migração de banco. A atualização direta preservou configurações, conexão, credencial sintética e sentinela no ensaio de migração. A instalação no Site-Teste registrou a pré-imagem b1d8ac12b81885ae4fca710f. Em caso de interrupção, consultar o recibo da operação antes de repetir. Uma correção posterior à instalação exige uma nova versão.

## 6. O que permanece pendente

- Frota: publicar instalador e relatório e verificar os bytes raw. A distribuição em produção e a medição de 24 horas da retenção em CTOOffice continuam pendentes.
- MCP/Core e frota: observar novas passagens naturais e comparar o histórico de registro com a saúde autenticada. O incidente constava como recuperado na base e nas duas leituras posteriores à instalação. Uma amostra curta não estabelece estabilidade por um dia.
- Operador do Core: definir destino técnico autorizado e conferir o recebimento em caixa postal. O destino estava vazio e o incidente de registro tinha 26 entregas pendentes. A conta deve considerar a fila existente antes de habilitar o envio.

## 7. Credenciais e configuração do dono

A troca utiliza as conexões e perfis já configurados. O painel administrativo fica em Ferramentas → Fator3 MCP. OAuth, as senhas de aplicação e as capacidades WordPress continuam sob o controle do site. O destino de avisos fica no Core em Avisos técnicos por e-mail. Usar a conta autorizada para essa finalidade.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-fator3-0.49.0-instalador.zip](https://chatgpt.com/library?file_id=libfile_fde3_f-de1b2d2b08708191a6ab87f16267febb_32706b9c47908191baafe72f89b6caee&account_id=personal) | 964290 | c1981c997840231a47492333ebb48125b2e8b8dd8619ec660bc8ad205883b134 |
| Fonte | [wp-mcp-fator3-0.49.0-fonte.zip](https://chatgpt.com/library?file_id=libfile_fde3_f-a896e72381ac8191b54492209e2fadbf_32706b9c47908191baafe72f89b6caee&account_id=personal) | 3699774 | f266281d1158cde59c8193d9f045e45bc833489794e7e8c1bdd00e80ea6002bd |

Digest do inventário de runtime: a96e87db3d11cc4275f4a77585998b191cd437da6fd45bf4de326bcc20e20e5e. O instalador é o ZIP próprio para o WordPress. A frota publica os arquivos conforme o padrão de distribuição. O fonte é entregue ao dono.

O checklist de encerramento está em evidencias/0490/checklist.json, no fonte.

Este é o relatório externo da entrega. A cópia no fonte foi fechada antes do cálculo da identidade final do próprio ZIP.
