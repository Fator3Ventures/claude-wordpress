# Entrega — Fator3 Site Core 1.45.0

Implementação dos pedidos **264–270, 272 e 273**, com atualização concluída no Site-Teste. Base direta 1.44.0. Contrato administrativo 8.10.0. Publicação no GitHub e implantação na frota não foram feitas. A opção de telefone livre em ctooffice continua dependente da decisão 111.

## 1. Bases aceitas

Requisitos: Fator3 Site Core(20261021-172554).md, incluindo o item 273 no corpo; instruções comuns e padrão de desenvolvimento revisão 4, de 16/10/2026. O pedido 263 já integra a base 1.44.0 e foi preservado; a decisão posterior 272 muda sua retenção.

Base exata: `base-site-core-fator3-1.44.0-instalador.zip`, 2.129.471 bytes, SHA-256 `91c4695ad4585965276c6b8cabc9ab8a91bbffc4423968f00d2330f6edf1407e`. Fonte-base: 3.134.934 bytes, SHA-256 `283452e8bb12a2e073779191d1386232fdf79bbd77f2e1ae4c642616f4beb52d`. Identidades, basename, namespaces, provider e prefixos preservados.

## 2. Convivência e encaminhamentos

No Site-Teste permaneceram ativos MCP 0.25.0, MCP Google 0.16.0, MCP Meta 0.4.1 e MCP LinkedIn 0.4.1. Nenhum desses pacotes foi alterado. Não surgiu mudança necessária no MCP Google nem novo contrato que exija aguardar seu responsável.

Único impacto técnico: `base-site-core-fator3-1.45.0-impacto-implantador-base.md`, revisão 2. O schema mensal e a opção de telefone exigem conferência dos lotes e das cópias compartilhadas. O documento registra o impacto recebido do Implantador 2.10.0 e distingue suas provas da validação própria do Core. Foi preparado, não enviado.

## 3. Mudanças por pedido e evidência

| Pedido | Implementado | Evidência e limite |
|---|---|---|
| 264 | Leitura gzip com integridade, fonte lógica única e prova diária persistida com SHA-256, tamanhos e linhas; códigos distinguem ausência inicial de rotação posterior. Retenção sai do hash de processamento com ponte da regra anterior. | Fixtures confirmam duas fontes adjacentes, compressão/remoção sem rebaixar prova, CRC/truncamento recusados e ausência de duplicação. Dias antigos sem prova continuam parciais. Sete dias em ctooffice pendentes. |
| 265 | Linhas de IA, detalhes e série semanal preferem caminho canônico do catálogo; caminho bruto fica identificado como evidência. | Post sintético acessado por /@post-ID devolve caminho canônico nos três segmentos testados. Aceite em conselar após troca. |
| 266 | Regra rede-efetiva-2 aplica automacao-suspeita a qualquer agente fora das faixas oficiais; preserva declaração e dados brutos. | Googlebot, Bingbot e GPTBot em fixtures; histórico não regravado silenciosamente. Conferência das sete requisições de fator3.com.br pendente. |
| 267 | Falhas HTTP Clarity conservam corpo saneado até 1.024 bytes e Retry-After válido; leitura em clarity-ler, modo resposta. | HTTP 400 simulado gravado/lido pela ability, token removido, limite e cabeçalho conferidos. Próxima falha real ainda não observada. |
| 268 | Evidência versionada de faixas AWS/Google Cloud/Azure, navegador antigo e ausência de interação; recorrência por caminho/hora/dias; motivo persistido, diagnóstico de 500 e alerta de dois dias sem consumo. | Fixtures confirmam classificação, correção após interação, preservação de regras antigas e headless/webdriver, alerta com baixo volume e entrada inválida 400. A causa histórica dos 500 da twinia não foi reconstruída. |
| 269 | Chaves de mapeamento compatíveis com o consumidor, nomes em palavras, recusa de chave desconhecida e mensagem própria para chave antiga. | Validação das chaves e controles renderizados no navegador; valores não editados preservados. |
| 270 | Prova de autoria nova sem update_time, com campos materiais; exclusão de organização própria exclusiva; motivo por objeto mantido. | Quatro cenários Pipedrive simulados: exclusão integral apesar de timestamps, edição humana, organização compartilhada e prova antiga. Aceite remoto novo em ctooffice pendente. |
| 272 | Retenções mensais 1–120, padrão 60 em instalação nova; operações seis; qualidade Meta sete dias; exceções preservadas; migração auditada sem redução no instante da troca. | Instalação nova, migração idempotente, preservação de autoria e configurações; tabela abaixo comprova valores reais do Site-Teste. A frota ainda deve aplicar 60 aos sites existentes. |
| 273 | Formato livre por campo, desligado por padrão; texto exato e classe/motivo; grupo aceita telefone livre preenchido; sem link/busca por telefone inválido; tarefa Conferir contato sem e-mail; marca nos diários e opção de conversão. | Página/diálogo no navegador, endpoint e diários no laboratório; Site-Teste HTTP 201 com livre e 400 desligado. Valor exato e sem_ddd lidos no registro. Aviso suprimido e contato de teste eliminado. Pipedrive real não exercitado. |

Retenção observada no Site-Teste, com origem preservada em todos os itens:

| Configuração | Antes | Depois |
|---|---|---|
| f3base_comportamento | {"retencao_dias": 365, "retencao_eventos_dias": 365} | {"retencao_meses": 13, "retencao_eventos_meses": 13} |
| f3base_acessos | {"retencao_horaria_dias": 30, "retencao_meses": 25} | {"retencao_horaria_meses": 1, "retencao_meses": 25} |
| f3base_pipedrive | {"retencao_entregas_dias": 30} | {"retencao_entregas_meses": 1} |
| f3base_formulario_tentativas | {"retencao_dias": 90} | {"retencao_meses": 3} |
| f3base_clarity | {"retencao_meses": 0} | {"retencao_meses": 120} |
| f3base_retencao_meses | 12 | 12 |

O grupo novo de retenções técnicas usa 60 meses e operações seis; contatos existentes continuam em 12 meses até decisão/aplicação da frota. Clarity sem expiração passa a 120 por ordem expressa. Valores previamente gravados acima do novo teto de contatos não são reduzidos silenciosamente; novas gravações acima de 120 são recusadas.

Telefone livre mantém conversões conforme consentimento, identificação da visita/clique, destino e prazo. `f3base_converter_contato_sem_identificador=true` preserva a política; false impede novas conversões desse caso nos transportes do Core. Marca fica no registro e nos diários; não há novo evento com valor livre para GA4, Meta ou Clarity. Valores de tentativas barradas continuam cifrados, só no WordPress, com capacidade f3base_ler_leads e exclusão por sessão/titular. Aviso e nota CRM com valor/marca se referem ao contato efetivamente aceito.

## 4. Instalação e prontidão

**505 verificações PHP e 72 verificações/casos de navegador passaram.** Evidências individuais em `evidence/`: regras, retenção, migração, logs, automação, formulário, fronteiras, exclusão CRM simulada, renderização, documentação e interface. Lint: 226 arquivos PHP. Chromium 153; Terser 5.44.1. Testes de telefone usam também o bundle minificado. Serviços externos dos testes locais foram simulados.

Instalação nova e atualização direta do instalador 1.44.0 original para o **ZIP final desta entrega** passaram pelo Plugin_Upgrader em WordPress 7.1.3/PHP 8.3.6/MySQL 8.0.36. Configuração, listas vazias, contatos, diários e credenciais sintéticas foram comparados; migração repetida retorna atual. O cabeçalho preserva o mínimo WordPress 7.1.2 comprovado nas entregas anteriores; esta rodada local foi executada em 7.1.3. Não foi testado multisite nem PHP de 32 bits.

Site-Teste: https://fator3-teste-mcp-1.dreamhosters.com/. Atualização 1.44→1.45 concluída, 18 etapas concluídas, zero falhas, confirmação pelo executor, Core operacional e não pausado. ZIP final instalado com SHA-256 `91620d8baadfd42911d624880838879501c722d20d37ecd734213541f920dc06`, operação de pacote `148e772917f8c9211cf09cb12c2f9801`. Home e REST retornaram 200 nas sondas internas. Isso não equivale a certificação de cache público ou entrega comercial.

O primeiro candidato do teste foi seguido de um ajuste exclusivamente documental no nome de uma ability; o instalador final foi novamente instalado e os ciclos locais repetidos com seu hash exato. Nenhuma versão foi publicada no repositório.

Homologação do telefone no Site-Teste: formulário temporário, dados sintéticos, sem e-mail e com celular sem DDD; HTTP 201, valor preservado inclusive espaços e marca sem_ddd. Outro formulário com opção desligada retornou campo_invalido/400. Aviso ficou suprimido_teste; integração Pipedrive estava desligada. O registro `525fed00dcec55c7352497d66c0b52d1` foi eliminado pelo fluxo Core e a leitura posterior retornou registro ausente. Definições de formulário e política de testes foram restauradas por revisão; arquivo temporário de upload removido. Nenhum formulário existente recebeu formato livre.

Documentação instalada inclui especificação, retenção, telefone, operação/recuperação, configuração, guia de agentes, schemas e ajuda gerada. Leitura MCP integral dos quatro documentos novos, com proxima_linha=null e hashes conferidos:

- `docs/RELEASE-1.45.0.md`: `b03636ac9099d4311e0d30398c005fabc1fccd26efddbe03f855666797da5bd2`.
- `docs/AGENTES-1.45.0.md`: `122bafd2a6d3ca9bd0fb8ed4f703696db593003c56e7af0f10b2e98d89a4b0d5`.
- `docs/RETENCAO-1.45.md`: `cdb3e1aaa0d4abd3c22c26c9936779c2199f54fa608abcbcf0ba94291c0bc464`.
- `docs/TELEFONE-1.45.md`: `748cd82b719e5b1cbe0b46d477c397d79ae484f44adfcbefdeac5eb234c2e63f`.

O schema e a ajuda foram regenerados do runtime: 73 opções documentadas, 136 abilities locais, quatro páginas de catálogo; descoberta efetiva pode variar com disponibilidade de módulos e recuperação. Documentos históricos e perfis antigos em dias permanecem históricos; use 8.10.0 e a política mensal atual para novos lotes.

## 5. Banco e reversão

Mudanças aditivas: analise.automacao_evidencia e telefone_estado em conversoes_servidor/capi_fila; CAPI schema 4. Novas opções f3base_retencoes_tecnicas e f3base_converter_contato_sem_identificador. Renomes de retenção são registrados em config_complementacoes com autoria preservada. Não há reclassificação retroativa de sessões sem evidência nova.

Antes da troca: Core drenado, backup SQL gzip privado no próprio servidor, ID `6580f717eff73495c6698996931cb31b`, 20829769 bytes, SHA-256 `16e25c1012ab611b3e61913634c4deb946d4b05f6a3c153cd605be9868ff4931`. O conteúdo do banco não foi exportado para os artefatos. Pré-imagem do primeiro instalador: `55be3b73a6bb30d74f5ad4f9`. A retomada reconciliou estados de 15 partes Slack e dois complementos preexistentes, sem afirmar entrega externa desses itens.

Reversão exige arquivos e banco coerentes do ponto anterior, operações pausadas e reconciliação dos efeitos externos; retornar somente o código à 1.44.0 não desfaz as chaves mensais e pode mudar prazos. Não repetir entrega incerta. As guardas operacionais de Core, Google e MCP têm donos distintos e não devem ser sobrepostas indiscriminadamente por um dump. O fonte não contém banco, credenciais reais, cookies ou logs pessoais.

## 6. Pendências

- **Frota:** implantar após revisão dos artefatos; conferir conversão e só então gravar os 60 meses deliberados nos 12 sites. Esta rodada não fez aplicação em massa.
- **Frota:** aceites de sete dias dos pedidos 264 e 268 em ctooffice/twinia; manter 01–13/10 parcial quando não houver prova. Conferir caminhos em conselar e exclusão de Googlebot fora das faixas em fator3.com.br.
- **Frota:** próxima falha HTTP real Clarity legível; diagnóstico da causa de futuros 500 na twinia. A evidência histórica de corpo vazio não permite afirmar a causa anterior.
- **Frota/dono:** teste Pipedrive real em ctooffice após a troca, com contato novo sem edição e outro editado; provas antigas conservadoras não são promovidas. Site-Teste não estava entregando ao CRM.
- **Dono:** decisão 111 antes de ligar formato livre em contato-whatsapp de ctooffice e antes de mudar a política de conversão. Nenhuma dessas decisões foi antecipada.
- **Implantador:** cumprir o encaminhamento individual de schema/cópias; sua implementação não foi declarada concluída.

Não foi criado escopo de DNS reverso, atualização de outros plugins, implantação na frota ou publicação GitHub. Não foram criados avisos de impacto só para anunciar versão.

## 7. Credenciais

Foi usada a conexão já autorizada do WP MCP fator3-teste. Nenhuma credencial real foi criada, alterada, exibida ou incluída nos arquivos. Tokens dos fixtures locais são sintéticos. Homologação de Pipedrive/Clarity/Ads reais e permissões de contas externas continua sujeita aos destinos autorizados; presença de código não comprova recebimento do fornecedor.

## 8. Arquivos finais

| Artefato | Bytes | SHA-256 |
|---|---:|---|
| `base-site-core-fator3-1.45.0-instalador.zip` | 2152375 | `91620d8baadfd42911d624880838879501c722d20d37ecd734213541f920dc06` |
| `base-site-core-fator3-1.45.0-fonte.zip` | 3150684 | `c1b6bed0f6be31e45e7f41cd513b70fa03656d9013af8929443b6249f8577f18` |

O instalador tem raiz base-site-core-fator3/ e é o único ZIP instalável. O fonte tem raiz base-site-core-fator3-1.45.0-fonte/, código, build, testes e evidências saneadas, sem ZIP interno. Sua cópia deste relatório é identificada como anterior ao fechamento; este relatório externo é canônico para tamanho/hash do fonte.

Relatório: `base-site-core-fator3-1.45.0-relatorio.md`. Encaminhamento necessário: `base-site-core-fator3-1.45.0-impacto-implantador-base.md`. Os quatro arquivos acompanham esta entrega.
