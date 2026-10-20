# Entrega — Fator3 Site Core 1.40.0

Revisão 1 · 20/10/2026 · Implementação dos pedidos 236 e 237.
Slug: base-site-core-fator3 · Versão: 1.40.0 · Status: **com-pendencias de homologação real**.

## 1. De onde esta versão entra

Instalação limpa e atualização direta de Core 1.39.0 ou 1.38.0. Bases publicadas preservadas. Testes em WordPress 7.1.3, PHP 8.3.6 e MySQL 8.0.46 locais. Não é necessário instalar 1.39 como intermediária para a frota na 1.38.

## 2. Convivência e encaminhamentos

Google 0.13 continua suficiente para navegador. Servidor exige a dependência Google implementada e entregue em patch, sua incorporação à versão do mantenedor e configuração validada. O código da dependência não aguardou resposta do mantenedor. Não foi publicada uma release Google nem implementado o pedido Google 29.

| Destinatário | Base examinada | Situação | Documento |
|---|---|---|---|
| MCP Google | 0.13.0; plano 0.14 recebido | Código/patch entregue; incorporação e validação real pendentes | impacto-wp-mcp-google-fator3, r2 |
| Implantador | Identidade implantador-base da aba; runtime não reexaminado | Schema/CAS e implantação a validar | impacto-implantador-base, r2 |

A revisão 2 do plano elimina Data Manager obrigatório/contrato de entrega 1.1 especulativo. Preservado site-conversion-delivery/1.0.0. O contrato de **leitura** site-conversion-purposes/1.1.0 foi implementado por negociação, sem alterar respostas 1.0.

## 3. Mudanças e evidência

| Pedido | Mudança | Resultado |
|---|---|---|
| 236 | f3base_conversoes_transporte por GA4/Ads, navegador padrão, validação de prontidão | Decisão gravada com o contato e devolvida no POST; troca afeta apenas novos registros; recuperação não cruza transporte |
| 236 legado | Preservação de registros/filas servidor da 1.39 | Históricos sem prova não são automaticamente reenviados; materiais e Meta preservados |
| Google 28 | Adapter GA4/Ads, segredo MP, tela/abilities, grant background, verificação, diagnóstico | Quinze testes de contrato/falhas e cinco de bootstrap WordPress; preserva adapter existente; sem HTTP de fornecedor durante status |
| 237 | C0, snapshot cifrado, SMTP DreamHost/TLS, Smart Bcc, quota por destinatário | Intenção única após lead novo confirmado; corpo só após todos os RCPT; checkpoint incerto antes de enviar |
| 237 histórico | Atividade C0 E-mail e aviso Slack no thread existente | Falha de atividade não repete e-mail; reconcilia marcador; resultado SMTP incerto não é automaticamente reenviado |

Senha SMTP usa option secreta cifrada. Contrato administrativo 8.5.0. C0 desligado por padrão; sem disparo retroativo por simples ativação. Serviço sem texto aprovado fica pendente. Prazo C1 vencido mantém pendência para revisão operacional, sem promessa falsa. Teste comum é suprimido; exceção administrativa única por registro, allowlist e uma hora de validade.

## 4. Instalação e prova da troca

Instalador na seção 8, pasta/basename preservados. Usar upload nativo WordPress; expected_slug=base-site-core-fator3 e SHA-256 indicado. Não foi publicada URL raw nem feita instalação remota nesta rodada.

| Teste | Ambiente | Resultado | Limite |
|---|---|---|---|
| Sintaxe | PHP 8.3.6 | 215 arquivos do instalador válidos | Não certifica outros runtimes |
| Regras 236/C0 | WordPress/MySQL | 33 verificações | Provedores simulados |
| SMTP e elegibilidade C0 | PHP/WordPress | 8 verificações | Sem envio real; recusa RCPT, quota, timeout e desconexão simulados |
| Conversão navegador | Node VM | 6 verificações | Não é WebView Android/Instagram |
| Pipedrive regressão | WordPress/MySQL | 41 verificações | API simulada; preserva fluxo anterior |
| Documentação | Ability local no WordPress | 69 verificações de paginação/hash/permissão | Sem transporte MCP remoto da 1.40 |
| Google contrato | PHP fixtures | 15 verificações | Sem credenciais/chamadas Google reais |
| Core + Google alterado | WordPress real local | 5 verificações | Bootstrap, hook, schema negociado, permissão e prontidão ausente |
| Instalação/upgrade | WordPress Plugin_Upgrader | Limpo, 1.39→1.40 e 1.38→1.40 | ZIP final identificado nas evidências; sem produção |
| Peso JS | Gzip9 local | 20.175 bytes nos quatro scripts, referência 21.517 | HTTP/CDN real ainda não medido |
| Site-Teste | MCP remoto, somente plugins/list | Core 1.39, Google 0.13, MCP 0.24 | Nenhum plugin/configuração alterado |

Docs no instalador: RELEASE-1.40.0.md, AGENTES-1.40.0.md, schemas, ajuda e inventário regenerados. Descoberta/leitura via f3base/documentacao-ler. Testes usam banco descartável e nenhum contato comercial real; não há recurso remoto criado para limpar.

## 5. Banco e volta de versão

Nova tabela f3base_c0 e contador local f3base_c0_cota; snapshots/intenções nos contatos. Diário de conversões preservado. Novos defaults não ativam conexão, servidor ou C0. Antes de reversão, pausar execução e manter backup do banco/diários. Voltar à 1.39 pode reintroduzir envio servidor incondicional; não usar como rollback automático. Restaurar arquivos não desfaz efeitos externos.

## 6. O que permanece pendente

Instalação/homologação remota do pacote, documentação pelo MCP remoto, HTTP comprimido real, WebViews, GA4 sessão original/DebugView, Ads ação real, SMTP/Smart Bcc/atividade e Slack reais. A dependência Google está implementada em patch; precisa incorporação e testes na release final do mantenedor. Não entregar seu ZIP de repasse ao instalador WordPress.

A elegibilidade Ads requer recibo real anterior fornecido pelo administrador mais leitura da ação; o request_id do recibo não é confirmado por endpoint de recibos. A prova local vence em 24h e pausa servidor até renovação. Não há Data Manager ou fallback automático. Para C0 atrasado cujo prazo C1 venceu, é necessária revisão operacional da promessa. Não há botão de reenvio automático de C0 incerto.

Esses limites impedem declarar homologação completa de produção. O modo navegador está implementado e testado localmente; servidor/C0 permanecem sujeitos à configuração e provas acima.

## 7. Credenciais e configuração do dono

C0: marca, senha no campo cifrado f3base_c0_smtp_senha, textos de serviço aprovados, caixa controlada para homologação e alocação de cotas da caixa compartilhada (100 destinatários/hora, incluindo Cco/usos manuais). Google: segredo MP do stream, conexão autorizada, conta/ação Ads e prova real de elegibilidade. Configurar, verificar e só então selecionar servidor no Core. Nenhum segredo real está nos pacotes ou evidências.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | base-site-core-fator3-1.40.0-instalador.zip | 2029901 | `d3bc062730e71520662282f969f32ded12065762301406f9a61a3601a98736fb` |
| Fonte | base-site-core-fator3-1.40.0-fonte.zip | 2125576 | `ef6c3fb7d39ca0556c963fdb1ac2d2c6706d5addf4d48532462aabea75ea2517` |
| Repasse Google | wp-mcp-google-fator3-dependencia-core-1.40.0.zip | 252673 | `a67067f1367814596cea2fdadcc8aed90f8085aced3995868e0339c372d6d1a3` |

Relatório externo canônico. Cópia no fonte anterior ao fechamento; o hash do próprio fonte só consta neste relatório externo. Os ZIPs fonte/repasse não contêm ZIPs internos.
