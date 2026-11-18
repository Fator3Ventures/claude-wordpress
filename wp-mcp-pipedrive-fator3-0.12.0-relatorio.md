# Entrega — Fator3 MCP Pipedrive 0.12.0

Revisão 1 · Data: 2026-11-18T16:29:00-03:00 · Rodada: implementação e validação.
Slug: wp-mcp-pipedrive-fator3 · Versão/build: 0.12.0 / instalador da seção 8.
Status: com-pendencias. Implementação validada em bancada; publicação e implantação compartilhada aguardam a frota.
Relatório externo canônico após fechamento do fonte. A cópia interna é anterior ao fechamento e permanece imutável.

## 1. De onde esta versão entra

Instalação limpa ou atualização direta 0.11.1 → 0.12.0. Base recuperada da entrega anterior: wp-mcp-pipedrive-fator3-0.11.1-instalador.zip, 474886 bytes, SHA-256 02fc0692722488de17174a59b58b80217a5609f2c8a4a586ca6016951532dcc5. A árvore da base foi conferida contra o fonte 0.11.1; nenhum artefato anterior foi sobrescrito.

Requisitos: WordPress >= 7.1.4, PHP >= 8.3 de 64 bits, mysqli, OpenSSL, mbstring e InnoDB.
Runtimes executados com a candidata: WordPress 7.1.4, PHP 8.3.6 e 8.4.27; MariaDB 11.8.6. Navegador: Chromium Headless 142.0.7444.175, WordPress nativo e PHP 8.4.27.
Site-Teste somente consultado: WordPress 7.1.5, PHP 8.3.36 e Pipedrive 0.11.1 ativo. Esse inventário não é prova da candidata em PHP 8.3.36.

Leitura integral de instrucoes-agentes-plugins-fator3.md e padrao-desenvolvimento-plugins-fator3.md, ambos revisão 5 de 02/11/2026; também regra comum, aba Pipedrive, pedido vigente e impactos fornecidos. Cópias em inputs/.

## 2. Convivência e encaminhamentos

| Pacote | Versão testada | Origem |
|---|---|---|
| Site Core | 1.93.0 | Anexos desta rodada |
| MCP | 0.48.0 | Anexos desta rodada |
| LinkedIn | 0.26.0 | Anexos desta rodada |
| Google | 0.36.0 | Pacote existente e inventário Site-Teste |
| Meta | 0.28.0 | Pacote existente e inventário Site-Teste |

Os cinco instaladores foram conferidos por hash e suas árvores instaladas permaneceram idênticas aos originais. Identidades em evidence/0120/companion-installers.json. A matriz foi executada nos dois runtimes, somente com esse conjunto vigente.

| Destinatário | Classificação / situação | Referência | Documento |
|---|---|---|---|
| Core 1.93.0 | validacao-coordenada / alinhado tecnicamente; aceite operacional pendente | Pedido Core 430, impacto recebido revisão 2 | wp-mcp-pipedrive-fator3-0.12.0-impacto-base-site-core-fator3.md, revisão 2 |

O Core já publica episódios de autorização recusada e recuperada. O plugin acrescenta leitura pública sem duplicar o produtor. Nenhum patch foi aplicado no Core ou nos acompanhantes.
MCP: política e NativeAdminCall verificados. Google, Meta e LinkedIn: convivência e identidade verificadas; suas APIs/campanhas/funcionalidades fora dessa fronteira não foram integralmente auditadas.

## 3. Mudanças e evidência

Fator3 MCP Pipedrive(8).md informa nenhum pedido em aberto. Pedidos MCP Pipedrive 13 foi entregue na 0.11.1. Não foi criado Pedido 14. Esta versão atende à solicitação atual do dono e à consequência técnica do Pedido Core 430.

| Referência | Problema | Implementação | Evidência |
|---|---|---|---|
| Pedido Core 430 / impacto | Diagnóstico da central não aparecia no domínio Pipedrive | pipedrive/incidentes-ler, readonly, filtro por pacote e cursor global | 18 asserções de contrato e 14 com Core original por runtime |
| Solicitação atual: UI | Distinguir incidente, fila e entrega incerta | Quadro em Suporte → Pendências com quatro contagens, estado parcial, explicações e links | 18 verificações específicas no navegador; três larguras; sem JavaScript |
| Solicitação atual: testes/documentação | Provar isolamento, permissões e continuidade | Regressões negativas, deduplicação, recuperação, reserva incerta; 12 documentos e schemas atualizados | 784 asserções PHP por runtime; 87 páginas de documentação por matriz |
| Pedidos MCP Pipedrive 13, regressão | Preservar navegação e busca existentes | Mantidos seis destinos e nomes em português | 51 verificações de painel e 29 de formulários |

São 23 operações: 12 de leitura e 11 de escrita. Os schemas de entrada das 22 anteriores e o schema de saída comum permanecem iguais à base. A nova leitura exige manage_options, política da conexão e permissão da ability do Core. Página vazia pode ter continuação; contagem parcial não representa o total. Falha de consulta não confirma recuperação.

Nenhum schema de banco, cron, credencial, regra comercial ou limite de escrita foi alterado. Ler o quadro não consulta CRM, publica incidente, envia aviso ou reconcilia entrega. O Core mantém suas rotinas independentes de observação.

## 4. Instalação e prova da troca

O instalador tem raiz única wp-mcp-pipedrive-fator3/ e 43 arquivos. Plugin_Upgrader nativo realizou instalações limpas e atualização da base nos dois runtimes. As bancadas usaram os bytes exatos da seção 8.

| ID | Ambiente | Cenário | Resultado | Evidência / limite |
|---|---|---|---|---|
| PHP84 | WP 7.1.4 / PHP 8.4.27 | Limpa, atualização, matriz | 650 + 17 + 107 = 784 aprovadas | evidence/0120/clean, upgrade, matrix; fornecedor sintético |
| PHP83 | WP 7.1.4 / PHP 8.3.6 | Mesmos três cenários | 784 aprovadas | evidence/0120/php83; fornecedor sintético |
| UI | WordPress / Chromium 142 | Seis abas, formulários e central integrada | 51 + 29 + 18 = 98 aprovadas | browser*.json; 21 capturas; dados sintéticos |
| ZIP | Python e ambos PHP | Sintaxe, schemas, inventário, reprodução | 14 invariantes por execução | package-verification*.json |
| SITE | Site-Teste compartilhado | Inventário, saúde e preservação | Saúde positiva, 0.11.1 ativa, nenhuma mutação | site-consulta.json; candidata não instalada |

Documentação: índice local e pipedrive/documentacao-ler. Os 12 documentos foram lidos integralmente pelo executor MCP original em cada matriz: 87 páginas de 2048 bytes, com versão/hash e bytes conferidos. Descoberta: 23 operações da 0.12.0. Trata-se do executor original em processo WordPress isolado; não de uma sessão remota da candidata no site compartilhado.

Painel: larguras 360, 768 e 1440 px; o novo quadro usou Core/MCP originais, com operação comercial indisponível. Nenhum erro JavaScript. As suítes PHP terminaram com logs vazios; a navegação gerou três avisos do atualizador WordPress por bancada devido ao bloqueio deliberado de rede. Nenhum erro do Pipedrive nesses logs. Servidores descartáveis encerrados; nenhuma fixture publicada no compartilhado.

### Procedimento pendente da frota

1. Publicar instalador e relatório na raiz de Fator3Ventures/claude-wordpress/main, sem fonte/evidências.
2. URL prevista: https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-pipedrive-fator3-0.12.0-instalador.zip. A consulta ao arquivo em main retornou NOT_FOUND nesta rodada; os bytes raw não foram conferidos.
3. Consultar o schema vigente de plugins/upload; conferir bytes servidos; usar expected_slug=wp-mcp-pipedrive-fator3 e expected_sha256=813923a62af52c58a3f39bfa658f51fab75a87ba0b3327ac76133d3aad6b5792. Aguardar verificação posterior sem repetir uma troca incerta.
4. Em nova requisição, confirmar versão ativa, saúde, preservação dos dados, descoberta das 23 operações e leitura integral dos documentos.
5. Executar pipedrive/incidentes-ler com objeto vazio; seguir proximo_apos até fim=true. Esperado: sucesso administrativo, version=0.12.0, chamada_externa=false. Lista vazia não confirma autorização CRM.
6. Conferir pipedrive/status. A base já retornou operacao_nao_autorizada nesta rodada. A autorização deve ser tratada no Core pelo dono, sem substituir a prova por fixture.

A seção 4.4 do padrão exige publicação raw e conferência anterior à instalação compartilhada. Nenhum push, envio Base64 ou substituição desse fluxo ocorreu. Não há recibo de implantação da 0.12.0 no Site-Teste.

## 5. Banco, migração e correção por nova versão

Nenhuma migração nova. A atualização preservou regras/revisão, retenção, diário, recibo, progresso e pendência sintéticos; novo processo conferiu persistência e replay. Não ativa cadência, troca token nem elimina fila.

Site-Teste: zero registros nas tabelas próprias de operações/diário, zero progressos e zero pendências; hash da retenção e ausência de regra própria configurada permaneceram iguais. Constatação de leitura, sem prova de atualização compartilhada.

Preservar banco, salts, recibos e pendências antes da troca. Em interrupção, conferir arquivos e prontidão sem presumir reversão de efeitos externos. Correção após instalação/entrega exige nova versão. Não há downgrade ou migração reversa. Entrega incerta do Core exige inspeção do transporte e reconciliação explícita por id e reserva.

## 6. O que permanece pendente

| Pendência | Motivo / responsável |
|---|---|
| Publicação raw e implantação no Site-Teste | Candidata não disponível em main na consulta. Frota publica, confere e instala conforme padrão. |
| Aceite do CRM real | A base já retorna operacao_nao_autorizada. Dono/frota verificam a conta no Core; nenhuma chamada comercial real nesta rodada. |
| Entregabilidade postal | Correio interceptado. Dono/frota conferem destino e recebimento real; aceite de transporte não prova chegada à caixa postal. |
| Sessão MCP remota e WP 7.1.5 com a candidata | Dependem da implantação. Prova atual: executor original em WP 7.1.4 e PHP 8.3.6/8.4.27. |

Pacote implementado e validado-localmente/validado-wordpress em bancada. Não está homologado-fornecedor nem implantado no compartilhado. Não declarar conformidade integral nem fechar o aceite operacional do impacto antes dessas provas.

## 7. Credenciais e configuração do dono

Nenhum novo segredo ou campo. O token e domínio permanecem no Site Core, com sua verificação de conta e permissões. O dono mantém a habilitação adequada às operações comerciais.

E-mail técnico: Site Core, Conexões → Avisos técnicos. O Pipedrive mostra somente se existe destino configurado; não revela o endereço. Na ausência de destino, a fila fica no Core.
Diagnóstico: Ferramentas → Fator3 MCP Pipedrive → Suporte → Pendências.
Documentação: Ferramentas → Fator3 MCP Pipedrive → Suporte → Ajuda.
Nenhum valor de credencial foi lido ou alterado.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | wp-mcp-pipedrive-fator3-0.12.0-instalador.zip | 489789 | 813923a62af52c58a3f39bfa658f51fab75a87ba0b3327ac76133d3aad6b5792 |
| Fonte | wp-mcp-pipedrive-fator3-0.12.0-fonte.zip | 5013074 | bd69147f8880d3a95b62114f17afc0b0216692c39e100fd5b58a4ad726bc1317 |

Relatório externo canônico: wp-mcp-pipedrive-fator3-0.12.0-relatorio.md.
Encaminhamento: wp-mcp-pipedrive-fator3-0.12.0-impacto-base-site-core-fator3.md, revisão 2.

O fonte contém esta cópia pré-fechamento, código, docs, testes, build e evidências sanitizadas. Não contém outro ZIP, dump, segredo, WordPress instalado ou binários de runtime. Instalador reproduzível byte a byte; identidade do fonte calculada depois de congelar sua cópia interna.

Checklist: evidence/0120/checklist.md. Publicação, implantação compartilhada e homologação externa permanecem pendentes; os demais resultados têm os limites descritos acima. Entrega ao dono, sem mensagens a terceiros ou publicação pública.

Complemento: wp-mcp-pipedrive-fator3-0.12.0-impacto-base-site-core-fator3.md, 4554 bytes, SHA-256 c3573abd47778d08eb4cdf7279df8a94d600c4e377d0119379f19c6316f48ce7.
