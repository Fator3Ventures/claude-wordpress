# Entrega — Fator3 MCP Google 0.30.0

Revisão 1 · 2026-11-06T11:51:08+00:00 · Rodada independente de melhoria.
Slug/basename: `wp-mcp-google-fator3/wp-mcp-google-fator3.php`.
Status: com-pendencias. Versão instalada e apta nos cenários comprovados abaixo.
Relatório externo canônico após o fechamento do fonte. A cópia no ZIP identifica seu estágio anterior ao fechamento.

## 1. De onde esta versão entra

A base é o fonte 0.29.0, SHA-256 `d9154f6225c879ac362c1b45a76a753717303f6db9f2682e8afce5606ad75cb3`, e o instalador 0.29.0, SHA-256 `2e6c061b725b95c56dd3087a4660308fe7d7f78c2e88151fb6eee110c854c2a9`. A rodada incrementa a versão para 0.30.0 e comprova instalação limpa e atualização direta. Requisitos mantidos: WordPress >= 7.1.4 e PHP >= 8.3. Foram executados WordPress 7.1.4, PHP 8.3.6, MySQL 8.0.46, PHPUnit 9.6.37, Node 24.22.1, Playwright 1.62.1 e Chrome for Testing headless shell 152.0.7940.0.

`instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md` foram lidos integralmente na revisão 5, de 02/11/2026. O checklist de encerramento foi conferido com as limitações da seção 6. As cópias utilizadas estão em `reproducao/entradas030`.

## 2. Convivência e encaminhamentos

O Site-Teste manteve MCP 0.41.0, Core 1.72.0, Meta 0.21.0, LinkedIn 0.19.0 e Pipedrive 0.7.0. Todos permaneceram ativos antes e depois da troca do Google. A prontidão local da integração Core retornou `ok` em ambas as versões do Google. Na bancada local, os instaladores vigentes de MCP, Meta, LinkedIn e Pipedrive foram identificados por SHA-256, ativados e mantidos durante os testes. O teste de autonomia executou somente o Google.

O instalador do Core 1.72.0 usado na rodada anterior não foi localizado nas fontes recuperadas. Por isso, a combinação completa com Core não foi repetida localmente nesta rodada. Não foi instalado Core anterior como substituto. Essa limitação está registrada no manifesto, nas instruções de reprodução e na seção 6.

As alterações examinadas estão no ciclo OAuth, no painel e na documentação do Google. Não houve alteração do contrato de configuração 4.0.0, dos nomes de abilities, dos contratos de conversões ou das interfaces dos acompanhantes. Nenhum impacto que exija implementação em outro plugin foi identificado nesse escopo; não foi emitido encaminhamento novo. Os encaminhamentos de rodadas anteriores permanecem identificados como históricos no fonte.

## 3. Mudanças e evidência

| Pedido | Problema reproduzido | Implementação | Evidência |
|---|---|---|---|
| Analisar e melhorar o código | Trocar Client ID com segredo vazio reutilizava o segredo do aplicativo anterior; a primeira configuração também aceitava ausência de segredo. | Exige o par correspondente ao novo aplicativo e usa revisão capturada antes da gravação. Segredo vazio preserva somente o mesmo aplicativo. | Testes unitários e WordPress verificam recusa, ausência de alteração e preservação da autorização ativa. |
| Melhorar as funcionalidades | Desconectar removia o token ativo e deixava a candidata pronta para restaurar acesso. | Remove tokens, e-mails e escopos das autorizações salva e candidata no mesmo lote verificado. Mantém cada Client ID com seu segredo. | Falha de gravação reverte o lote; repetição é estável; outra conexão permanece intacta; callback anterior fica desatualizado. |
| Melhorar as funcionalidades | A ativação OAuth omitia o contêiner GTM vinculado. | OAuth e conta de serviço compartilham a seleção de serviços vinculados. GTM passa pelo preflight antes da promoção OAuth. | Recusa simulada do GTM mantém a candidata e a autorização salva; acesso simulado confirmado permite a promoção. |
| Ampliar testes automatizados | Faltavam regressões dos caminhos acima. | Quinze novos testes unitários, cenários nativos de gravação e atualização, verificações de navegação e POST real. | A reprodução inicial falhou em seis casos na 0.29.0; a suíte consolidada aprovada tem 1.294 testes e 15.461 asserções, aumento de 15 testes e 82 asserções. |
| Melhorar UI e textos | Estado ativo e candidata se confundiam; a importação OAuth exibia a promessa de validação de uma chave de serviço. | Três etapas: aplicativo Web, consentimento e ativação. Cartões das duas contas, ajuda associada aos campos, ação de consentimento desabilitada sem aplicativo completo, descrição própria da importação e do alcance da revogação. | Navegador real em 1440 × 900 e 390 × 844; capturas inspecionadas; sem transbordamento; segredos ausentes do HTML; mensagens e retornos de formulário conferidos. |
| Melhorar documentação | Faltava um roteiro do ciclo OAuth e das consequências de cada ação. | Guia 0.30.0 com roteiro, tabela de efeitos e recuperação, changelog, migração, orientação a agentes e reprodução atualizados. | Build confere 305 abilities, 43 definições, 54 exemplos, links e geradores. Os 25 documentos instalados foram lidos integralmente pelo MCP local. |

O instalador tem 202 arquivos. O diff de runtime identifica 17 arquivos modificados, incluindo documentos compilados, sem arquivos removidos ou adicionados. A sintaxe dos 179 arquivos PHP declarados na lista de runtime foi conferida; arquivos de índice são gerados pelo build. As 72 dependências de desenvolvimento instaladas coincidem com o lock. Evidências em `evidence/030` e testes novos em `tests/OAuthLifecycle030Test.php`, `tests/native/oauth030.php`, `tests/native/upgrade030.php` e `tests/browser/admin030.cjs`.

## 4. Instalação e prova da troca

O instalador validado foi enviado ao Site-Teste por `plugins/upload-base64`, com `expected_slug=wp-mcp-google-fator3`, SHA-256 da seção 8, sobrescrita, ativação e chave idempotente. Não houve publicação pública nem instalação em outros sites. A origem foi o conteúdo integral do ZIP; URL raw pública não se aplica a esse fluxo.

Operação `779b5de7adccf2ee4542dafddf66a798`; pré-imagem `6251aacc9c1297ecd61b567e`. O recibo confirmou 0.29.0 → 0.30.0, estado ativo, bytes aplicados e reativação silenciosa em processo PHP independente. As sondas internas de `/` e `/wp-json/` passaram com HTTP 200 e prova de PHP novo. Essas sondas não comprovam acesso externo nem prontidão das APIs Google.

| Ambiente | Cenário | Resultado | Evidência | Limite |
|---|---|---:|---|---|
| PHPUnit | Suíte completa | 1.294 testes / 15.461 asserções | `unit-junit.xml`, `unit.json` | WordPress e fornecedor com dublês locais |
| WordPress isolado | Instalação limpa, autonomia, OAuth, diagnóstico e documentos | 108 verificações | `isolated/` | Sem acompanhantes |
| WordPress com MCP e canais | Instalação limpa, OAuth e formulários de tarefas/auditoria | 62 verificações | `current/` | Core ausente |
| Atualização por MCP HTTP | 0.29.0 → 0.30.0, preservação, desconexão e manuais | 142 verificações | `upgrade/` | Credenciais sintéticas; Core ausente |
| Navegador | Configuração, desktop/celular, POST, modo sem JavaScript e administrador/assinante | 55 verificações | `browser/` | Chrome em laboratório; inclui três ativações de acompanhantes |
| Site-Teste | Instalação, inventário, status, prontidão, schema e documentação | Aprovado no escopo local | `site-test.json` | Sem credencial Google configurada |

Total adicional: 367 verificações de WordPress, MCP e navegador. As tentativas de bancada que revelaram restrições antigas do próprio teste foram corrigidas: a criação de outra conexão atualiza a revisão global; `google/disconnect` não aceita `expected_revision` em seu schema público; o teste de tarefas continha uma versão fixa; a navegação precisou de seletor restrito à barra de abas após adicionar um link contextual com o mesmo texto. As execuções finais acima estão completas e aprovadas.

Novas requisições remotas confirmaram Google 0.30.0 ativo; armazenamento, recuperação, executor, incidentes e Core em estado `ok`. A prontidão segue `blocked` por `f3_google_not_configured`. O índice remoto dos 25 documentos coincide integralmente em nomes, bytes e SHA-256 com o fonte. Guia, migração e README foram reconstruídos em sete páginas MCP e comparados byte a byte. O schema de configuração foi consultado com `include_values=false`.

Os processos de laboratório foram encerrados. Sessões e application passwords temporárias foram eliminadas pelos testes. Nenhum dado de teste, cookie ou segredo foi enviado ao Site-Teste. Não houve alteração dos acompanhantes, das credenciais do dono ou da seleção de serviços. Avisos de conexão a WordPress.org na bancada decorreram do bloqueio deliberado de HTTP externo.

## 5. Banco, migração e correção por nova versão

Não há tabela nova nem migração destrutiva. A atualização conserva opções, valores cifrados, conexão adicional, vínculos, revisão da configuração, candidata OAuth e tarefa concluída. A nova regra de desconexão só é aplicada quando a ação é solicitada. Falha no lote local conserva o estado anterior; uma revogação já aceita pelo Google não pode ser desfeita pelo WordPress. O resultado da operação distingue o efeito remoto quando a gravação local falha.

Preserve banco, salts e recibos ao recuperar uma instalação. Formulários abertos antes da atualização devem ser recarregados. Qualquer correção posterior à instalação exige nova versão. A versão 0.30.0 entregue conserva os mesmos bytes que foram validados e instalados.

## 6. O que permanece pendente

- Consentimento, renovação, revogação e acesso GTM em conta real Google. O Site-Teste não tem credencial configurada. As respostas de fornecedor usadas nos testes são sintéticas. O dono deve fornecer o aplicativo Web e autorizar a conta pelos campos do painel.
- Repetição local da combinação completa com Core 1.72.0, dependente da disponibilização de seu instalador original. A observação remota do estado `ok` da integração não substitui essa repetição.
- PHP 8.3.0 exato, outros navegadores e UI remota do Site-Teste não foram executados. A UI foi exercitada no Chrome de laboratório. Os mínimos declarados permanecem PHP 8.3 e WordPress 7.1.4.

## 7. Credenciais e configuração do dono

Abra **Ferramentas → Fator3 MCP Google → Conexão → Identidade → Conta Google · OAuth**. Confira a conexão selecionada. Configure o aplicativo Web e sua URL de retorno, escolha os serviços e recursos, autorize a conta e compare a identidade candidata antes de ativar. Ao trocar Client ID, informe também seu Client secret. Para um mesmo aplicativo, segredo vazio mantém o valor existente.

**Desconectar esta conexão** remove ambas as autorizações locais e conserva os aplicativos. **Revisar revogação no Google** usa a autorização salva e exige confirmação; seu efeito pode atingir outros clientes do mesmo usuário/projeto. Uma candidata de outro projeto é retirada apenas localmente. O guia instalado descreve esses efeitos e a retomada. Referência técnica conferida: [Google OAuth para aplicações Web](https://developers.google.com/identity/protocols/oauth2/web-server#tokenrevoke).

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | wp-mcp-google-fator3-0.30.0-instalador.zip | 944896 | `4920abef86f65cc27178f16b2ea852b447d755507a6a8c82357b63b07c91b60e` |
| Fonte | wp-mcp-google-fator3-0.30.0-fonte.zip | 7712998 | `1ea6b2cbc9eb0e280336933a03af1c198bec63839b171d3d561d5b0afb0eaaee` |
| Relatório | wp-mcp-google-fator3-0.30.0-relatorio.md | Documento externo canônico | A cópia no fonte antecede seu fechamento |

O fonte contém o runtime completo, documentos editáveis, testes, scripts de build, instruções e evidências sanitizadas. Dependências executáveis e instaladores de terceiros ficam fora do fonte e estão identificados por hash. Os ZIPs não contêm outros ZIPs. Distribuição pública e alterações de código de outros plugins não fazem parte da rodada.

Após o fechamento, o fonte foi extraído em diretório novo e seu build reconstruiu exatamente os 944896 bytes do instalador instalado. Ambos os ZIPs passaram na verificação de integridade, raiz única e ausência de ZIPs internos.
