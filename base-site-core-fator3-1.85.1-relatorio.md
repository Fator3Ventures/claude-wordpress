# Entrega — Fator3 Site Core 1.85.1

Revisão 1 · 14/11/2026 · Rodada de implementação dos pedidos 400 e 401, com correção de fechamento no mesmo ciclo. Slug `base-site-core-fator3`. Contrato de configuração 8.41.0.

**Status: apta-no-escopo-testado.** Versão instalada e ativa no Site-Teste. A próxima ação em produção cabe à frota.

## 1. De onde esta versão entra

O ciclo começou no instalador 1.84.0 de SHA-256 `b1f1d28792e6c873292d7f26273da8a0ca056b7a3b38b0b5e56a8d95df6bb460`. A versão intermediária 1.85.0 foi instalada no Site-Teste. Durante o fechamento identificamos um caso adicional envolvendo deduplicação de concessões de material protegido. A correção gerou a 1.85.1. Homologamos instalação limpa, atualização 1.85.0 → 1.85.1 e salto direto 1.84.0 → 1.85.1 em laboratórios independentes. A frota pode partir diretamente da 1.84.0.

Requisitos do instalador e da suíte: WordPress 7.1.4 ou superior e PHP 8.3 de 64 bits ou superior. Ambiente nativo local exercitado com WordPress 7.1.4, PHP 8.3.6 e MySQL 8.0.46.

Normas lidas integralmente, ambas na revisão 5 de 02/11/2026. SHA-256 de instrucoes-agentes-plugins-fator3.md: `f0c48263597444bf304be515e3a61d268751c47cd5eaf7dfcfa9db7ea47773fc`. SHA-256 de padrao-desenvolvimento-plugins-fator3.md: `6dd73913cf41f0157a8e68cf922cbc2b97757537488fcf441ef67a9dee5e3166`. Pedidos recebidos em Fator3 Site Core(20261114-043023).md, cópia em reference/.

## 2. Convivência e encaminhamentos

No Site-Teste foram relidos como ativos MCP 0.45.0, Google 0.34.0, Meta 0.25.0, LinkedIn 0.22.0 e Pipedrive 0.10.0. Os formatos de chamada desses plugins se mantêm. O Core entrega aos consumidores a identidade canônica da nova captura. O painel, a habilidade de simulação, o envio ao Slack, as notas de CRM e o relatório de classes pertencem ao Core. A matriz local exercitou os adaptadores Google, Meta e LinkedIn com respostas controladas. Pipedrive e Slack foram verificados na montagem das cargas e registros. A rodada não exige patch nos plugins acompanhantes. O ajuste de configuração atribuído à frota está descrito nas seções 6 e 7.

## 3. Mudanças e evidência

| Pedido | Mudança entregue | Evidência |
|---|---|---|
| 400 · Telefone | BR aceita DDD válido e número local de oito dígitos iniciado em 2–9, ou nove dígitos iniciado em 9. Reconhece +55, 55 com número completo e zero nacional. DDD 55 é preservado. Internacional explícito segue E.164. Novo diagnóstico fica registrado na captura. | 14 entradas conferidas no servidor. Formulários estrito e livre, identidade do Pipedrive, seleção para WhatsApp e hash da Meta. No Chromium, +55 sem DDD foi recusado e o prefixo 011 foi aceito. |
| 401 · E-mail | A captura guarda digitado, corrigido, classe e motivo. Faz limpeza de espaços, vírgula de domínio e ponto final. Valida a escrita e consulta entrega do domínio. A lista de erros de nove provedores é editável e simulável. A correção de sufixo depende das duas respostas DNS. | 16 entradas com DNS controlado incluíram MX, A, MX nulo, domínio inexistente, falha de DNS, sufixo confirmado, sufixo preservado, escrita inválida e endereço corrigido. Execução administrativa da habilidade e do simulador no painel. |
| 401 · Consumidores | O endereço utilizável segue para as integrações. A correção de domínio identifica o digitado no aviso principal do Slack e na nota do Pipedrive. Sem outro identificador válido, a configuração controla a conversão, a atividade padrão é Conferir contato e o e-mail automático fica inelegível. A visão emails_normalizacao soma as quatro classes no recorte. | Captura → banco → leitura → composição de Slack/CRM. A consulta retornou uma ocorrência em cada classe no conjunto sintético e apenas classe/contagem em cada linha. Formulário enviado pelo navegador retornou HTTP 201 e os valores canônicos foram relidos pelo record_id. |
| 401 · Material protegido | A concessão exige e-mail utilizável. Um envio com endereço inválido continua registrado e recebe instrução para fornecer um e-mail válido. | Ativo privado real no laboratório. Duas entradas inválidas geraram zero concessões. Endereço válido obteve um link. O reenvio manteve a mesma concessão. Uma tentativa sem e-mail após o aceite não recebeu o link anterior. |

São 138 verificações específicas de telefone/e-mail e oito de concessão privada, executadas tanto na instalação limpa quanto no ambiente de atualização. As suítes também conferiram atribuição e título de Slack da rodada 395, cliques e conversões dos pedidos 398/399, documentação, permissões e reativação. O registro tem 195 habilidades. A varredura de 104 habilidades de leitura terminou sem exceções PHP. O manifesto conferiu 975 arquivos do instalador, com análise de sintaxe em 603 arquivos PHP. O build reproduziu 84 JavaScripts e seu índice.

O resolvedor de DNS sobre HTTPS recebe apenas o domínio no endereço fixo da Cloudflare. A consulta usa orçamento de dois segundos e cache limitado de respostas definitivas. Falha de resolução mantém a classe nao_verificado elegível. Um MX válido confirma a rota do domínio. O recebimento em uma caixa individual depende do transporte de e-mail. Os valores digitado e corrigido ficam no registro privado do contato. O relatório integrado expõe as contagens.

## 4. Instalação e prova da troca

O Site-Teste recebeu exatamente o ZIP da seção 8 em um endereço raw temporário, com `expected_slug=base-site-core-fator3`, `expected_sha256`, sobrescrita e ativação. O recibo de atualização `f2f7fddd8e643e29c32d8c1fcf155114` e a releitura independente confirmaram 1.85.0 → 1.85.1 e plugin ativo. A página inicial e /wp-json/ retornaram HTTP 200 antes e depois. O ZIP temporário de homologação foi removido. Os documentos instalados AGENTES-1.85.1.md e RELEASE-1.85.1.md foram lidos integralmente pelo MCP. A versão final do simulador foi exercitada no Site-Teste com dados sintéticos e DNS real. O relatório por classes também foi consultado.

O fonte guarda os resultados por ambiente em evidence/1851, incluindo site-teste.json, navegador.json, material-1851, 400-401, validação do ZIP e as duas migrações. O diretório evidence/1850 reúne as evidências da versão intermediária. Para reproduzir o instalador, execute build/reproduzir-instalador.py no fonte e compare com a seção 8. Para inspecionar cada entrada use build/conferir-instalador.py. Os testes que escrevem no banco exigem WordPress descartável.

## 5. Banco, migração e correção por nova versão

A normalização usa a coluna JSON de dados existente. Os campos canônicos passam a ser calculados na captura e o relatório conta os envios aceitos com fotografia disponível. A atualização não reprocessa endereços ou telefones antigos. O padrão false não sobrescreve uma decisão explícita. As migrações preservaram o registro semeado do teste. O envio do formulário e a ingestão de plataforma continuam usando a deduplicação do registro. O teste do material cobre reutilização da mesma concessão para um endereço válido. Correções futuras seguem por avanço de versão. O código de simulação não cria contatos.

## 6. O que permanece pendente

A distribuição em produção, a gravação explícita da política nos 12 sites e o registro de false como padrão operacional da frota cabem ao Orquestrador após a entrega. A frota pode conferir o primeiro contato real corrigido pelo mesmo record_id no Core, no aviso e na nota. A confirmação de entrega efetiva no Slack de produção, na conta comercial do Pipedrive, no provedor de e-mail e nas contas de mídia exige tráfego real e recibos externos. Os testes desta rodada não enviaram mensagens a esses destinos. A evidência no Site-Teste usa amostras sintéticas.

## 7. Credenciais e configuração do dono

A rodada dispensa novas credenciais. Configurações → Contato → Correções de domínios de e-mail contém os pares erro=destino e o simulador da proposta. A habilidade administrativa é f3base/email-contato-simular. Para verificar o total, use f3base/relatorios-integrados-ler com visao=emails_normalizacao e leia linhas. Os novos pares entram em vigor nas próximas capturas. Consulte as notas instaladas para limites, permissões e exemplos.

No Site-Teste, a atualização preservou o valor explícito true anterior. Durante a homologação, simulamos e gravamos false com a revisão esperada e relemos false. A conferência após o patch voltou a ler false. Para a frota, ler f3base/config-core-ler, gravar f3base_converter_contato_sem_identificador=false com f3base/config-core-escrever, revisao_esperada e simular=false e reler valor_efetivo em cada site. Identificar domínio, versão e revisão no recibo de implantação.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [base-site-core-fator3-1.85.1-instalador.zip](base-site-core-fator3-1.85.1-instalador.zip) | 4472260 | `1fe1ba76880e7b6535af564a0fb702b823555d6307fb70d857b7081f64a4bfbd` |
| Fonte | [base-site-core-fator3-1.85.1-fonte.zip](base-site-core-fator3-1.85.1-fonte.zip) | 66710471 | `7500da4e768b73d5e6d1b05fd8b3d08e6a316b8366ce6262ba246e104e135855` |

O relatório externo é canônico. A cópia RELATORIO-PRE-FECHAMENTO.md dentro do fonte precede o cálculo do tamanho e do hash do próprio ZIP.
