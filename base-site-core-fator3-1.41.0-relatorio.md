# Entrega — Fator3 Site Core 1.41.0

Revisão 3 · 20/10/2026 · Rodada: implementação · Status: **com-pendencias**.
Slug: base-site-core-fator3. Contrato administrativo 8.6.0 (aditivo à 8.5.0).

## 1. De onde esta versão entra

Instalação limpa e atualização direta da 1.40.0. Base publicada preservada, SHA-256 d3bc062730e71520662282f969f32ded12065762301406f9a61a3601a98736fb. Validado em WordPress 7.1.3, PHP 8.3.6 e MySQL 8.0.46. O mínimo WordPress 7.1.2 é herdado do cabeçalho; não foi repetido nesta rodada e não é prova nova de suporte.

## 2. Convivência e encaminhamentos

Google 0.14.0: compatível com navegador. Servidor exige a extensão PHP sendBound, implementada e entregue em dependência para incorporação pelo mantenedor. A versão Google publicada sem a extensão fica bloqueada com destination_binding_unsupported. Não há fallback automático para navegador nem renumeração silenciosa do Google.

Encaminhamento único: base-site-core-fator3-1.41.0-impacto-wp-mcp-google-fator3.md, revisão 2, acao-necessaria, incorporação/homologação pendentes. Nenhuma alteração de código nova exigida em MCP, Meta, LinkedIn ou Implantador no escopo examinado.

## 3. Mudanças por pedido e evidência

| Pedido | Implementação | Evidência/limite |
|---|---|---|
| Correções do fluxo Core 236, solicitadas após revisão | Identidade do destino no snapshot de aceite; fila/reconciliação fiel; vinculação administrativa explícita/auditada de legado sem identidade | Teste local de A→B, recusa, recuperação e preservação; sem inferência da conta histórica |
| Diagnósticos do mesmo fluxo | Conserva códigos simbólicos do fornecedor; fallback para código inválido; estado independente | Readiness e erro de envio preservados; não grava resposta bruta |
| Sessão original GA4 | Leitura da tag conferida com cookies; procedência, horários e janela de 24h validados | Implementado controle temporal; atribuição real e fim efetivo de sessão continuam sem homologação |
| Revisão das descrições solicitada diretamente | 13 resumos de páginas, 47 entradas de rótulo/descrição; remoção de ajuda genérica e exemplos repetidos; catálogo regenerado; transporte visível em Tags | 70 schemas/defaults preservados; HTML de 13 páginas gerado localmente. Não houve validação visual em navegador real |

Não foram inventados IDs de pedidos. Itens 238–241 do anexo têm alterações funcionais fora do plano aprovado: histórico Pipedrive, tela SMTP, conteúdo do e-mail e migração para configuração independente não foram implementados. Nome funcional do grupo de e-mail ajustado editorialmente; aliases/identificadores antigos mantidos. Meta e e-mail automático preservam sua lógica.

## 4. Instalação e provas

| Prova própria | Resultado | Limite |
|---|---|---|
| Sintaxe PHP | 217 arquivos válidos | PHP 8.3.6 |
| Regras e metadados Core | 229 verificações | WordPress local, adaptador simulado |
| Dependência Google | 39 verificações, incluindo worker Core real | HTTP externo simulado, sem credencial comercial |
| Documentação | 69 verificações de leitura/paginação/hash/permissão | Ability local; não é transporte MCP remoto da 1.41 |
| HTML de configuração | 26 verificações em 13 páginas | Render PHP; Chromium ausente |
| Captura GA4 JavaScript | 7 verificações | Node VM; tag simulada |
| Regressão navegador/servidor | 6 verificações | Node VM; sem WebView |
| Compatibilidade editorial | 70 opções com schemas/defaults idênticos à base | Metadados e contrato administrativo versionado separadamente |
| Instalação/upgrade | WordPress limpo e upload nativo 1.40→1.41, processos novos; snapshot anterior/posterior igual; repetição idempotente | Confirmação de espera acelerada somente no laboratório |

Assets: quatro scripts de contato somam 17.950 bytes em gzip local; teto anterior 21.517. Isso não equivale à medição HTTP do servidor. Nenhum novo script de carga foi adicionado.

Site-Teste consultado por WP MCP fator3-teste: Core 1.40.0, Google 0.14.0 e MCP 0.24.0 ativos; system/health respondeu com sucesso. Nenhuma instalação remota: plugins/upload exige URL, e a URL de publicação da frota ainda não existe nesta rodada. Não foram editados dados/configurações remotos. A instalação futura deve usar expected_slug=base-site-core-fator3 e o SHA-256 da seção 8; consultar operation-status/reconcile se a verificação ficar pendente.

## 5. Banco e reversão

Sem remoção ou renomeação de tabela. Novos contatos incluem referências e evidência temporal no JSON já existente. Vinculação administrativa registra usuário/data e confirmação de não entrega, sob lock, transação e comparação de snapshot. Referências antigas não são sobrescritas. Entregue/incerto não voltam automaticamente à fila.

Backup antes da troca. Reversão à 1.40 reintroduz lacunas anteriores: suspender o worker e avaliar dados antes de retomar. Voltar arquivos não desfaz chamadas externas. Não apagar o diário para liberar pendências.

## 6. Pendências e limites

- Mantenedor Google: incorporar a dependência numa nova versão publicada; código e testes já entregues.
- Frota: publicar URL verificável, instalar/homologar a 1.41 no Site-Teste e conferir leitura documental pelo MCP.
- Homologação: navegador real, WebViews Android/Instagram, peso HTTP e uma ocorrência atribuída à sessão original no GA4. Chromium não está instalado no runtime; o teste visual não foi concluído.
- GA4: o ID nativo gerado pela tag tem semântica de início documentada; identificadores customizados não são suportados. Dados de navegador não são prova criptográfica nem comprovam o fim efetivo da sessão. HTTP 2xx e debug não encerram atribuição analítica.
- Não reexecutada a matriz mínima WordPress 7.1.2. Nenhum envio comercial realizado.

## 7. Credenciais e configuração

Nenhuma credencial real coletada. Para servidor: Google configurado/verificado, segredo MP e destino GA4; Google Ads exige acesso/destino elegível conforme a integração. Credenciais ficam no Google. Para recuperação, usar apenas referência opaca obtida da capacidade atual e confirmação operacional de não entrega. Exemplos e fixtures são sintéticos.

## 8. Identidade dos arquivos

| Artefato | Nome | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | base-site-core-fator3-1.41.0-instalador.zip | 2037832 | `66ae54be3b0ec7a066187455b8358fc3c3431a47de8fc6aa8ac8c5efa3510919` |
| Fonte | base-site-core-fator3-1.41.0-fonte.zip | 2907382 | `871bb10708b9251d571b50611bdbdab89dd1d27fb05bc36b74d721f8bba18cf3` |

O relatório externo é canônico; a cópia dentro do fonte é anterior ao seu fechamento. A dependência Google tem nome, bytes e hash no impacto individual. Instalador e runtime do fonte correspondem byte a byte. Nenhum ZIP inclui outro ZIP de entrega.
