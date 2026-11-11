# Entrega — Fator3 MCP LinkedIn 0.21.0

Revisão 1 · 2026-11-11T02:35-03:00 · Implementação e homologação. Slug: `wp-mcp-linkedin-fator3`. Versão/build: 0.21.0. **Status: com-pendencias.** Implementado e ativo no Site-Teste; o aceite do download real do anúncio indicado ainda não foi demonstrado pelo novo contrato.

## 1. De onde esta versão entra

Instalação limpa ou atualização direta da 0.20.0, sem etapa intermediária. Base oficial: instalador 429846 bytes, SHA-256 `4b3f7321b81a28bbed6595d6922ec7d388685690d58d278f3f4b3ebc592ee743`; fonte 3543948 bytes, SHA-256 `ece3924e1d1ca54ed36f58ea6ead21f5037f4d68e03ea53b28bf6c5a93bbb5ba`. Requisitos: PHP >= 8.3 e WordPress >= 7.1.4. Exercitados WordPress 7.1.4, PHP 8.3.6 e MySQL 8.0.46. Referências integrais: instrucoes-agentes-plugins-fator3.md e padrao-desenvolvimento-plugins-fator3.md, revisão 5, 02/11/2026, e anexo de 11/11/2026, Pedidos MCP LinkedIn 24 / Pedidos core 390.

## 2. Convivência e encaminhamentos

Conjunto ativo no Site-Teste na troca, comparado aos ZIPs usados em integração:

| Pacote | Versão | SHA-256 do instalador de bancada |
|---|---|---|
| core | 1.80.0 | `2e81a04d0a9f99f1607d5b388c4aa2590bcc0b3b853cda1fa1b7b3530302ec72` |
| mcp | 0.44.0 | `a90aa7f2e91ef1033a4a8c6ec320b1e10b45ef657132a40f8aa4215ffa55d5eb` |
| google | 0.34.0 | `9a5f52f35a4a7c34e21e08d12099dacb05dfdfc99d3d0cc335bde95a2676135c` |
| meta | 0.24.0 | `ba026fc1109ebb9ffed4fc6709753b0dfb0dc9635acaa20652406cc4b2bbcf7e` |
| pipedrive | 0.9.0 | `42523b9b547fc8820c3917e192c4b48341efbb1da6815c78fcc18f8a373c09c0` |

**Core:** `wp-mcp-linkedin-fator3-0.21.0-impacto-base-site-core-fator3.md`, revisão 2, acao-necessaria, pedido core 390. O emissor está pronto. O cliente oficial já pode chamar o método; conectar a ficha do Core ao resultado é trabalho do destinatário. O patch incluído no fonte foi testado apenas na cópia descartável do Core 1.80.0. A captação continua independente da leitura do criativo. Não há dependência de atualização conjunta para as funções existentes. No MCP, as URLs e a validade atravessaram o executor na bancada; o impacto da 0.20.0 permanece encerrado. Sem impacto técnico identificado em Google, Meta e Pipedrive no escopo de ativação e contratos exercitados. Nenhum código ou documento de release oficial de acompanhantes foi alterado.

## 3. Mudanças por pedido

| Pedido MCP LinkedIn 24 | Comportamento na 0.21.0 | Evidência |
|---|---|---|
| (1) Resolver imagens, vídeos e miniaturas | GET aos serviços Images/Videos. Retorna endereços HTTPS temporários de domínios admitidos e validade em Unix UTC/ms. Endereço expirado é omitido. Em vídeo, a validade da miniatura é independente; sem dado verificável, vem nula. O resolver consulta metadados e não baixa nem grava o binário. | Ensaios de imagem, vídeo, mídia pendente, endereço externo e expiração. A mutação que desabilita o limite de validade reprova o caso correspondente. |
| (2) Uma chamada do Core por conta/criativo | SDK `resolve_ad_source`, extensão `linkedin-ad-source/1.0.0`; REST/MCP `linkedin/lead-resolve-ad-source`. Entrega nome e ID do criativo e campanha, texto, título, descrição, botão, destino, tipo, mídia, miniatura e links do Campaign Manager/publicação. Não exige Página no argumento. Valida IDs, vínculos de conta e autor/owner em cada salto. | Cliente original do Core e executor MCP reais em bancada. Projeção tipada; retornos externos sintéticos. |
| (3) Mesma origem para anúncios de formulário nativo | Em vez de creative_id, informe form_id e response_id; valida conta, formulário, tipo SPONSORED e criativo associado, além da referência de campanha quando presente. Não inclui as respostas pessoais nem dispara evento de captação, CRM ou conversão. | SDK em dois modos, resposta sem associação, conta/formulário errados, campanha divergente e revogação durante a leitura. |
| Permissão e administração | Em Concessões → Formulários, habilitar ad_source para ler os criativos das contas Ads concedidas; por resposta também exige responses e seleção do formulário. A permissão nova começa desmarcada; salvamento sensível exige simulação/confirmação. Nenhuma concessão antiga é ampliada. | Navegador real, assinante recusado, SDK sem concessão recusado antes de HTTP e migração sem alteração de privilégios. |

Uma única chamada do consumidor pode realizar até quatro GETs de metadados no caminho direto, ou cinco pela associação da resposta de lead. Leituras externas produzem a auditoria local prevista; a operação não altera a conta de anúncios. Formatos sem publicação reconhecida preservam os dados conhecidos e expõem o estado da mídia. Campos ausentes não são preenchidos por inferência. Para multi-imagem, o resultado representa a primeira imagem. O catálogo instalado contém 100 operações, 56 de leitura e 44 de escrita. Consulte AD-SOURCE.md e o schema gerado.

## 4. Instalação, testes e prontidão

**Site-Teste:** https://fator3-teste-mcp-1.dreamhosters.com/ via WP MCP fator3-teste. Um único resultado aplicado pelo upload do ZIP, expected_slug=wp-mcp-linkedin-fator3, expected_sha256 da seção 8, overwrite e activate. Versão anterior 0.20.0 → 0.21.0 ativa. Operação `465ae92abc2499f4f5075604cc21035c`; backup de arquivos `487a7f2a1adfdda62b85e167`. Rotas / e /wp-json/: HTTP 200 antes e depois. Versões e ativações imediatamente antes/depois registradas em site-teste.json; somente o LinkedIn mudou na sua operação.

Outros mantenedores atualizaram Meta e Google durante a rodada. A primeira conferência abortou antes de gravar ao detectar alteração. Depois houve `resource_busy` na tentativa de instalar: a repetição com a mesma chave devolveu o recibo da recusa. O estado nativo continuava 0.20.0, sem operação de pacote aplicada nessa tentativa; a nova tentativa após liberação da trava e atualização do inventário produziu o recibo acima. Não houve dois upgrades. Este procedimento usa o arquivo com hash conferido em teste autorizado; a publicação pela frota via URL raw permanece separada.

**Leituras após a troca:** `linkedin/status`: ok, 0 conexões. Autoteste 9/9 local. Descoberta do contrato e de documentação, schema com os dois modos, índice de 47 arquivos, hashes do índice cotejados com o instalador, leitura integral de 4 manuais em 7 páginas pela conexão MCP do próprio site. Consulta ao contrato com os identificadores do pedido no Site-Teste retornou `not_configured`: o site não tem a conexão de CTO Office. Não foi criada configuração com segredo de outro site.

**CTO Office:** a versão preexistente 0.20.0 retornou o criativo 1605615034, conta 558431216, nome «26.10.20 - Quase pronto 2», campanha 901687794, publicação urn:li:share:7518299312901107712, texto, título, descrição, CTA, destino e a referência de miniatura urn:li:image:D4E10AQH24fg6VLFasw. Somente leituras por get-creative, get-campaign e get-post. A 0.21.0 não foi instalada nesse site nesta entrega; não se obteve URL assinada nem binário real nas três consultas. Sem prova de acesso a Images/Videos do aplicativo ou de download real.

**Bancada:** matriz inicial de 715 verificações, sem falha final, com Meta 0.23.0 e Google 0.33.0 (nos casos integrados); uma instalação/DB descartáveis por suíte. Os cenários se sobrepõem deliberadamente. Sem avisos/erros PHP nos logs capturados dessas execuções.

| Suíte / cenário | Verificações | Falhas |
|---|---:|---:|
| ad-source021-integrated-clean | 38 | 0 |
| ad-source021-only-clean | 36 | 0 |
| core-frontier021-integrated-clean | 39 | 0 |
| core1680-integrated-clean | 37 | 0 |
| mcp-docs080-integrated-clean | 72 | 0 |
| mcp-docs080-integrated-upgrade | 72 | 0 |
| migration021-integrated-upgrade | 7 | 0 |
| server020-integrated-clean | 35 | 0 |
| suite-integrated-clean | 141 | 0 |
| webui020-integrated-clean | 238 | 0 |

Com Meta 0.24.0 e Google 0.33.0, repetimos 334 verificações. Com **Meta 0.24.0 e Google 0.34.0**, conjunto da troca, foram **406 verificações**: fluxo novo via MCP/SDK, regressão, cliente oficial Core, seu adaptador experimental, migração e leitura documental integral, todas aprovadas. As 238 verificações de interface ocorreram na primeira matriz, em Chrome Headless com sandbox, desktop e celular. O conjunto funcional com os cinco acompanhantes não é uma homologação das respectivas contas externas. Três mutações de código (expiração, proprietário de mídia e vínculo da campanha) e 16 mutações de documentação foram detectadas. Critérios e conjuntos em evidence/release0210.

Documentação na bancada: tanto na instalação limpa quanto após a atualização, o executor MCP do WordPress leu os 47 documentos em 58 páginas por cenário, conferindo conteúdo e SHA-256. No teste compartilhado, os agentes descobrem a operação pelo MCP e acessam a ajuda sem consultar o LinkedIn. A origem pode ser lida somente com conta e escopo autorizados; dados de formulário não fazem parte da ajuda.

## 5. Banco, migração e recuperação

Schema físico 2 preservado. No ensaio de atualização da base, 10 registros de referência mantiveram conteúdo/revisão, incluindo a concessão, material cifrado, trabalho pausado, agendamento e operação de efeito incerto. A permissão de origem não apareceu nas concessões antigas. O teste também verifica o cursor, a política de retenção e a pausa da agenda. Não foi realizado downgrade; falha futura deve ser corrigida por nova release preservando o banco. O backup da instalação abrange arquivos, não substitui o backup do banco. Não houve fixture ou token de laboratório no WordPress compartilhado.

## 6. Pendências por responsável

- **Administrador do Site-Teste:** configurar uma conexão própria que tenha acesso à conta, ao anúncio e aos endpoints de mídia, ou disponibilizar uma conta de homologação para prova equivalente explicitamente identificada. Não enviar tokens pelo chat nem replicar credenciais da produção.
- **Dono do CTO Office:** para o aceite literal, autorizar implantação nesse site ou realizar a instalação pelo fluxo da frota. Com a conexão já configurada, chamar o novo contrato com o criativo 1605615034, baixar temporariamente a imagem, validar tipo/bytes e registrar somente o resultado da prova. A leitura atual das três entidades não substitui esse aceite.
- **Mantenedor Core:** integrar à apresentação da origem em Pedidos core 390, separar endereços temporários e controlar o acesso ao registro no consumidor. Nenhuma ação de escrita no LinkedIn é necessária. Fora do escopo: testes com gasto, publicação, campanhas e webhooks reais ou implantação geral.

## 7. Credenciais e configuração

Ferramentas → Fator3 MCP LinkedIn. A conta deve estar selecionada em Ads na conexão e o membro/aplicativo precisa ler os recursos: anúncios/campanhas, conteúdo da publicação e mídia de seu proprietário. Para Lead Sync, selecione também conta/formulário e conceda leitura de respostas. A permissão de consumidor da origem é distinta de campaign_lookup. Registre somente o estado, IDs e, quando necessário, a validade; endereços assinados são tratados como efêmeros. No teste compartilhado não foi transferida credencial entre sites.

## 8. Identidade dos arquivos

Relatório externo canônico. A cópia interna antecede o fechamento do ZIP fonte. O instalador foi reconstruído a partir do fonte entregue e comparado byte a byte com o ZIP aplicado no Site-Teste.

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| `wp-mcp-linkedin-fator3-0.21.0-instalador.zip` | 439650 | `ebe4363bf55476cbe1ba30df80d8ab6b2362ee2dc379c21762aa42f4a05b1bfc` |
| `wp-mcp-linkedin-fator3-0.21.0-fonte.zip` | 3649366 | `a8142ca22c90caf5ff90003776b62037fc7f8ed2fa325448df3efcb5dae5720a` |

Relatório externo: `wp-mcp-linkedin-fator3-0.21.0-relatorio.md`. Impacto pertinente: `wp-mcp-linkedin-fator3-0.21.0-impacto-base-site-core-fator3.md`. Instalador: 91 arquivos, 90 entradas no manifesto (exclui o próprio manifesto). Fonte inclui runtime idêntico ao instalador, código editável, testes, proposta isolada e evidências sanitizadas. Python 3.12.14, zlib 1.3.2. Nenhum ZIP contém outro ZIP. Sem commit externo atribuído.
