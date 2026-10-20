# Entrega — Fator3 MCP Google 0.15.0

Revisão 1 · 2026-10-20T19:56:35-03:00 · Rodada: implementação · Status: **com-pendencias**.
Slug/basename: `wp-mcp-google-fator3/wp-mcp-google-fator3.php`; provider `wp-mcp-google-fator3`.
Implementação concluída e validada no escopo local; instalação remota e homologação comercial pendentes.

## 1. De onde esta versão entra

Instalação limpa ou atualização direta Google 0.14.0→0.15.0, sem desinstalar. Base publicada conferida: instalador SHA-256 `7b9681bed81fa265ac70379fd6ebb5d4b161923a8e10a7a4ad115af58cf3d001`; fonte `05af95023adf13b27fedc556c2759df7a28197a848a48c5cc4135e85bd1836bb`. Arquivos fechados da base preservados.

Mínimos exercitados: WordPress 7.1.2, PHP 8.3.6; MySQL 8.0.46, PHP CLI server com quatro workers, bancos/portas isolados. O runtime de ferramentas teve SHA-256 de árvore registrado no manifesto desta rodada; não se reutilizou o hash de uma árvore anterior parcialmente removida. Não se afirma matriz PHP-FPM, multisite/CDN nem outros runtimes.

## 2. Convivência e encaminhamentos

Core 1.41.0 em instalação limpa e atualização Google; Core 1.40.0 com ativação Google primeiro. MCP 0.24.0; Meta/LinkedIn 0.3.0 como sentinelas no upgrade. Google também foi instalado isoladamente, sem acompanhantes. Nenhum pacote acompanhante foi modificado.

Repasse recebido: `wp-mcp-google-fator3-dependencia-core-1.41.0.zip`, 14152 bytes, SHA-256 `9854091bd070a0791f81a1fe453fd96272c0933b62977a6ebd7d7be39698c160`. Core 1.41 instalador examinado: SHA-256 `66ae54be3b0ec7a066187455b8358fc3c3431a47de8fc6aa8ac8c5efa3510919`. Sua evidência foi distinguida dos testes próprios.

Encaminhamento único: [wp-mcp-google-fator3-0.15.0-impacto-base-site-core-fator3.md](wp-mcp-google-fator3-0.15.0-impacto-base-site-core-fator3.md), r2, validacao-coordenada. Incorporação concluída; implantação e homologação pendentes. Nenhuma nova implementação exigida do Core. MCP, Meta, LinkedIn e Implantador não têm contrato alterado neste escopo; não foram emitidos avisos individuais apenas de versão. Não foi avaliada a frota inteira.

## 3. Mudanças e evidência

| Pedido/evidência | Implementação | Resultado/limite |
|---|---|---|
| Dependência recebida do Core 1.41, fluxo de conversões 236 | `sendBound(payload, destinationRef)` sob trava comum; `send()` preservado | Referência correta aceita; vazia, longa, destino errado ou outro tipo recusados sem HTTP |
| Revalidação durante o despacho | Guard relê identidade atual, verifica concessão e trava; mantém códigos locais de não entrega | Troca de destino/credencial, expiração e revogação após debug impedem coleta; reconfiguração concorrente via MCP recebe busy |
| Integração Core | Métodos PHP nos dois executores, diário e estados do Core preservados | Entregue/incerto persistidos e não repetidos; fornecedores simulados |
| Documentação corrente | Guia 0.15, migração, contratos, ajuda compilada e catálogo atualizado | 20 documentos lidos completos/paginados pelo MCP local, com versão/hash/tamanho; instruções antigas de instalação corrigidas |

Não foram criados IDs de pedidos. Configuração permanece 4.0.0; execução/armazenamento/manutenção 2.0.0; catálogo 3.0.0. Mantidos 286 abilities (111 leitura/175 escrita) e 36 opções. Schemas de entrada/saída das abilities são idênticos aos da 0.14.0. Mudanças no runtime limitadas a ConversionDelivery.php, documentação compilada e arquivo principal/versionamento. Não há nova ability de envio, fila paralela, fallback de API, migração ou habilitação automática de transporte servidor.

## 4. Instalação e prova da troca

**615 verificações aprovadas: 555 em WordPress nativo e 60 puras; zero falhas na matriz final.** Sintaxe válida em 154 arquivos PHP de runtime; instalador com 158 arquivos.

| Grupo | Percurso | Verificações nativas |
|---|---|---:|
| clean | clean / mcp-first | 220 |
| upgrade | upgrade / mcp-first | 194 |
| core140 | clean / google-first | 119 |
| isolated | clean / google-only | 22 |

Evidência vinculada: `evidence/015/validation015.json`, SHA-256 `ee949acff6b067e302af1717adddcc31602588bcff506664d6b31112f737e40e`. A suíte específica `tools/release015.py` confere candidato/identidade, cada prova e inventários finais. Não equivale ao gate integral PHPUnit/`tools/validate.py`/`build/build.py verify`. Provas recebidas ou históricas não entram na contagem. Ensaios de interrupção/observação de cron da 0.14 não foram repetidos porque esse código não mudou. A primeira tentativa do cenário Core 1.40 não chegou a instalar WordPress: MySQL falhou ao iniciar por ausência de um arquivo redo. O cenário foi executado em novo banco/diretório, com os mesmos bytes e testes; grupos já aprovados foram conservados e revalidados pelo inventário/identidade. O log de infraestrutura e o fechamento das evidências acompanham o fonte; não se atribui a causa ao plugin.

A atualização usa upload MCP autenticado local com hash/slug, verifica configuração de conversões, segredo MP cifrado, credenciais, conexões, jobs concluídos, agenda pausada e registros preservados. Rollback de arquivos, recusa de destino editado, inventário exato da base e reaplicação do candidato aprovados. Processos novos confirmam a versão. As sentinelas de dados/cron Meta e LinkedIn foram preservadas; os processos de laboratório encerrados e o runtime instalado comparado byte a byte aos pacotes.

Documentação instalada: `google/documentation`, descoberta de schema, índice e leitura completa dos 20 documentos via HTTP MCP; paginação UTF-8, hash, tamanho, recusa de travessia, revisão vencida e usuário sem administração. Não fez chamadas a fornecedores. A tela de conversões teve HTML/nonce/ausência de segredo conferidos, sem teste visual em navegador.

Site-Teste: consultado via WP MCP fator3-teste. Saúde local healthy=true; WordPress 7.1.3, PHP 8.3.30. Google 0.14.0, Core 1.40.0, MCP 0.24.0 e Meta/LinkedIn 0.3.0 ativos; conversões Google desabilitadas, sem verificação/HTTP comercial. Requisição de saúde `c4879d3a9d26e10ed0474bee`; estado de conversões `abda4630459a24ea694c8cf2`. Nenhuma instalação ou configuração remota realizada nesta rodada. Não se reivindica prova remota da 0.15.0.

A norma r4 exige URL raw publicada e conferida antes de `plugins/upload`. Essa URL não foi disponibilizada e a publicação GitHub pertence à frota. A entrega está pronta para essa etapa: `expected_slug=wp-mcp-google-fator3`, `expected_sha256` da seção 8, `overwrite:true`, `activate:true`; consultar operation-status/reconcile se a verificação ficar pendente. Não foi usada uma rota alternativa para contornar o fluxo de distribuição.

## 5. Banco e volta de versão

Sem alteração de schema ou migração. Configuração, provas e segredos existentes permanecem no armazenamento por conexão. O novo método somente verifica a referência recebida do Core. Nenhuma referência antiga é inventada, regravada ou promovida. Fila, consentimento, atribuição e diário permanecem Core.

Faça backup coerente de arquivos, banco e material de cifra. Rollback de arquivos não desfaz banco ou efeitos externos. Voltar Google à 0.14 remove sendBound e bloqueia servidor no Core 1.41 com destination_binding_unsupported. Preserve filas/diários e reconcilie resultados incertos antes de retomar. A pré-imagem local foi testada; não há backup remoto novo porque não houve instalação remota.

## 6. O que permanece pendente

- Frota: publicar URL verificável, instalar Google 0.15 e a versão Core planejada no Site-Teste, conferir status e ajuda pelo MCP remoto. A instalação do Core permanece com seu responsável.
- Dono dos ativos/mantenedores: configurar credenciais e verificar destinos autorizados; homologar conversão Ads real, sessão GA4 original e ausência de duplicação em navegador/WebView Android/Instagram.
- Acompanhamento de três dias nos 12 sites continua pendente da rodada anterior; não foi simulado como duração real nem agendado nesta tarefa.
- Sem teste visual, PHP-FPM, multisite/CDN ou homologação comercial. Debug/HTTP 2xx é recebimento, não prova de processamento/atribuição; Ads requer resultado individual correspondente.

## 7. Credenciais e configuração do dono

Ferramentas → Fator3 MCP Google — Conversões. Escolher conexão; habilitar serviços com perfil de escrita e política adequada. GA4: measurement_id, stream e segredo MP. Ads: customer_id, conversion_action, developer token/credencial com acesso e declaração administrativa de upload elegível. Configurar com revisão atual e verificar explicitamente. Segredo é cifrado; vazio mantém e remoção é explícita. Verificação expira em 24h e depende da concessão/identidade vigentes. Nenhuma credencial real coletada ou publicada.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | wp-mcp-google-fator3-0.15.0-instalador.zip | 742908 | `a7014e419c1a1a79d9a9e02112fd8f5b285fed131b50e10ea26f588d2179b169` |
| Fonte | wp-mcp-google-fator3-0.15.0-fonte.zip | 3142995 | `3d2be60367a25c649462fdd913303a6d69d12a2079c7924994174e71544e34ef` |

O relatório externo é canônico. A cópia no fonte antecede seu fechamento e não contém o hash do próprio ZIP. Fonte inclui código, runtime idêntico ao instalador, documentação editável, build/testes, evidências sanitizadas, plano e impacto corrente. Nenhum ZIP contém outro ZIP de entrega. Não foi publicado GitHub nem enviado recado externo.
