# Entrega — Fator3 MCP Google 0.13.0

Revisão 1 · 20/10/2026 · Fuso America/Sao_Paulo · Implementação/correção
Situação: implementado e validado no escopo do pedido MCP Google 27; integração comercial Core 235 permanece bloqueada.
Identidade preservada: `wp-mcp-google-fator3/wp-mcp-google-fator3.php`, provider `wp-mcp-google-fator3`.

## 1. Bases aceitas

Normas Fator3: instruções comuns e padrão de desenvolvimento, revisão 4 de 16/10/2026, relidos integralmente. Plano Google 0.13.0 r1, atualizado nesta rodada; pedido 27 como escopo aprovado. Sem alteração da lista central.

Base Google 0.12.0, ZIPs imutáveis conferidos: instalador 721839 bytes/SHA-256 `d2499a5f0b2b89b5640dc86a780fc8a73335dc20d06003eb22b7185ce98162c0`; fonte 2825174 bytes/SHA-256 `a7f4efcc73ca4e64d9c76507739f6f7744894856a81f611173d97a256d80e717`.

Acompanhantes principais: Core 1.38.0, MCP 0.24.0 e, no upgrade, Meta/LinkedIn 0.3.0. Core 1.39.0 recebido em fonte/instalador com impacto r2 foi examinado adicionalmente. Seus hashes foram conferidos; seus testes publicados são evidência recebida, não prova própria Google. Dependências de laboratório, versões, origens e hashes ficam em `evidence/013`.

## 2. Convivência e encaminhamentos

Único novo impacto pertinente: `wp-mcp-google-fator3-0.13.0-impacto-base-site-core-fator3.md`, aberto/bloqueio, pedido Core 235. O contrato de leitura permanece `site-conversion-purposes/1.0.0`. O contrato novo de entrega `site-conversion-delivery/1.0.0` não representa aceitação e consulta assíncrona Data Manager. Elegibilidade do transporte Ads legado não foi demonstrada. A parte dependente aguarda alinhamento e homologação; esta versão não fornece adaptador de entrega, segredo MP ou novas opções comerciais.

O Core 1.39.0 suprime a conversão de contato Google no navegador; não deve ser promovido como pronto sem o adaptador operacional. Não houve atualização Core no Site-Teste. `configured:true` no leitor significa identificadores locais, não prontidão de envio. O ensaio próprio Core 1.39.0 certifica apenas a compatibilidade do leitor e o comportamento de conflito, não fila, captura ou fornecedor.

Impacto Google 0.12.0 → Implantador permanece resolvido no escopo técnico segundo o retorno recebido 2.10.0; não reaberto. Não há mudança de contrato que exija novo impacto MCP/Meta/LinkedIn/Implantador. Nenhum pacote alheio ou regra central foi editado; nenhum encaminhamento enviado a terceiros.

## 3. Mudanças por pedido e evidência

**Pedido 27 implementado:** `ConversionContext::read()` mapeia explicitamente o código validado `revision_conflict` para `conflict:true`, conservando `retryable:false`, erro `f3_google_core_conversion_revision_conflict` e bloco Core exato com `data:null`. Não foi criada heurística global de erros. Outros erros continuam sem conflito de revisão.

`current_revision` só aparece na recusa defensiva de uma fotografia de sucesso já validada: vem de `data.revision` da mesma operação. O erro normal do SDK 1.0.0 não a fornece e o campo é omitido. Não existe segunda consulta, revisão fabricada nem alteração do schema Core. O parâmetro opcional de saída é limpo em cada chamada. Sucesso preserva seu envelope anterior; não exige um campo novo de conflito no ramo de sucesso.

Schema da operação, catálogo, README, guia, contratos, exemplos de tratamento e documentação compilada foram atualizados. O guia agora referencia `google/status` em vez da rota inexistente `google/update-status`. Permanecem 283 operações (110 leituras/173 escritas), 34 opções, configuração 4.0.0, catálogo 3.0.0, execução 2.0.0, armazenamento/manutenção 2.0.0. Identidades e permissões administrativas preservadas.

A suíte de regressão executada contra o runtime extraído do instalador 0.12.0 falha especificamente na classificação exigida; o candidato passa. Testes puros usam produtores simulados; ensaios nativos usam WordPress e Core reais, com transporte MCP HTTP autenticado. GTM usa respostas Google simuladas, mantendo uma única leitura por diagnóstico e falha apenas no bloco adicional quando apropriado.

**Resultado final da matriz: 585 verificações aprovadas**, sendo 525 nativas e 60 puras; zero falhas no candidato definitivo. Sintaxe: 150 PHP. Instalador: 154 arquivos. Casos nativos: limpo 217, upgrade 234, isolado 22, leitor Core 1.39.0 52. Os 19 documentos instalados foram lidos integralmente e conferidos por hash via MCP nos laboratórios limpo/upgrade, incluindo catálogo de 2646981 bytes. Os totais consideram apenas a execução definitiva, sem somar ensaios preliminares nem a regressão esperadamente falha da base.

Instalação limpa, atualização direta 0.12.0, rollback/reaplicação, isolamento e leitor Core 1.39.0 foram executados e vinculados ao hash do candidato. Nenhum teste depende de credencial comercial. O servidor local é PHP CLI com quatro workers, não PHP-FPM; MySQL isolado. Todos os processos próprios foram encerrados, conforme evidências.

A documentação MCP é descoberta pelo schema, índice e leitura completa paginada; bytes e hashes de cada documento, incluindo catálogo longo, são conferidos. Guarda de revisão, caminhos arbitrários, autorização e ajuda sem credencial são exercitados. Provas 012 e anteriores dentro do fonte são históricas; não contam para os totais desta rodada. Não se afirma execução integral PHPUnit ou do gate histórico abrangente.

## 4. Instalação e prontidão

Instalar somente `wp-mcp-google-fator3-0.13.0-instalador.zip`, mantendo a pasta estável; não desinstalar para atualizar. Mínimos exercitados no laboratório: WordPress 7.1.2/PHP 8.3.6. Core/MCP são acompanhantes de teste, não travas numéricas de ativação.

**Site-Teste:** Google 0.12.0→0.13.0 ativo; WordPress 7.1.3/PHP 8.3.30, MCP 0.24.0, Core 1.38.0, Meta/LinkedIn 0.3.0 preservados. Home/REST 200 antes/depois, execução PHP nova comprovada, `healthy:true`, zero recuperações não resolvidas, storage pronto e zero incidentes Google. Operação `1718571d72aff6c1a8c776d00df0d341`, backup `b8771d2035492fdea5d0c806`; requisição de troca `2e77ca2f2fb7adc25b17d716`.

Reprodução antes: `069bacfa73829d4d7a90e7c0`, conflito false. Depois: `a2bb3c2fd6db539ed2a73827`, conflito true/retryable false, erro e data null preservados, sem current_revision. Releitura com revisão válida teve sucesso (`6fb7efb410a5d76706ce1402`). Revisão de configuração antes/depois idêntica `8cc263030b60418dd023fcc29a22f2663fb64b28a82b249d66a5d86d1cf909ef`; estados retornados das 34 opções iguais. Schema remoto anuncia booleanos e revisão opcional de 64 hex.

Índice remoto reconhece 0.13.0 e 19 documentos. README, guia 0.13.0 e CONVERSOES foram lidos integralmente (11 páginas, sendo nove de conversões), com igualdade exata de bytes/hash ao fonte. O hash do catálogo remoto no índice coincide com o local; sua leitura integral paginada foi feita nos laboratórios, não repetida no Site-Teste. A troca usa bytes/hash/slug esperados e backup do pacote. A nova requisição reconheceu 0.13.0 e confirmou pedido 27, documentação e saúde. Não há configuração comercial de teste ou mudança de acompanhante no site compartilhado.

Prontidão desta entrega refere-se à correção do pedido 27. Não significa prontidão da troca comercial Core 235, entrega Google real ou publicação na frota. Instalador e relatório são entregues ao dono; publicação raw, distribuição nos sites e aceite da lista central cabem à frota/revisor. O fonte não foi publicado no repositório; decisão 89 preservada.

## 5. Banco, configuração e reversão

Sem opção, tabela, migração, job, default ou credencial nova. O leitor continua sem rede/escrita; a auditoria normal da operação segue a política existente. No upgrade local, opções selecionadas, credenciais sintéticas cifradas, conexões, bindings, agendas pausadas, jobs concluídos e registros sociais são sentinelas de preservação. A correção não executa trabalho concluído novamente.

Rollback de arquivos à 0.12.0 reintroduz o defeito do pedido 27. A bancada exercita backup, prévia, recusa de destino alterado, retorno da base e reaplicação do mesmo candidato. Rollback de arquivos não desfaz banco, credenciais, filas ou efeitos externos. Não houve restauração do banco compartilhado.

## 6. Pendências por responsável

- Google + Core: alinhar o contrato/recibos/consulta e implementar o transporte servidor do pedido Core 235; detalhes e aceite no impacto. Não encerrado por esta entrega.
- Dono/Datta + Google: validar a API permitida para a conta, ação de importação, consentimento, valor/moeda e credenciais; homologar GA4/Ads, sessão original, Android WebView/Instagram e deduplicação Meta. Não executado com contas reais.
- Frota/revisor Google: conferir os artefatos e fechar o pedido 27 após aceite; publicar/distribuir o instalador conforme regra própria.
- Dono/frota: pendência histórica 20 (coleta completa/jobs/calendário/exportação/paginação em uso real) permanece sem prova nova; não ampliada automaticamente para esta correção.
- Não avaliados nesta rodada: navegador gráfico, multisite, cache distribuído/CDN e cron externo. Os ensaios locais não demonstram esses cenários.

## 7. Credenciais e segurança

Nenhum segredo real foi solicitado, criado, renovado, exportado ou alterado. O leitor funciona sem credencial Google. Segredos da bancada são sintéticos e isolados; bancos, chaves de laboratório, senhas temporárias e logs privados não acompanham os ZIPs. Testes, ferramentas e evidências sanitizadas ficam somente no fonte. O instalador usa allowlist e documentação PHP protegida por gate administrativo, sem Markdown/QA exposto.

## 8. Artefatos e identidade final

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `wp-mcp-google-fator3-0.13.0-instalador.zip` | 723475 | `d026247e0b25f184c3699e0fff7ee6bae8f49c8a2e63859a40bef529cc7f2297` |
| Fonte | `wp-mcp-google-fator3-0.13.0-fonte.zip` | 2876664 | `3e6f32eb323e2354a1fc2e9c90a5e20b867a4af82e34c51aaf1d484ff8666596` |

Relatório externo: `wp-mcp-google-fator3-0.13.0-relatorio.md`. Plano r3: `wp-mcp-google-fator3-0.13.0-plano.md`. Impacto pertinente r2: `wp-mcp-google-fator3-0.13.0-impacto-base-site-core-fator3.md`. Manifesto JSON complementar identifica todos os artefatos sem substituir esta tabela.

O instalador é fechado primeiro; sua árvore runtime deve coincidir byte a byte com o fonte. O relatório interno é identificado como cópia anterior ao fechamento do fonte; tamanho/hash finais do fonte ficam apenas no relatório externo. Nenhum ZIP contém outro ZIP. Não foram alterados os ZIPs 0.12.0.
