# Entrega — Fator3 MCP LinkedIn 0.5.0

22/10/2026 · Base direta 0.4.1 · Pedidos MCP LinkedIn 5, 6 e 7.
**Estado: implementado e instalado no Site-Teste, com pendências explícitas de integração e homologação.** Não é declaração de aceite de produção.

## 1. Bases aceitas

Instruções comuns aos agentes e padrão de desenvolvimento, ambos revisão 4 de 16/10/2026, lidos integralmente. Pedidos e pacotes foram lidos dos anexos locais. Slug/pasta/basename wp-mcp-linkedin-fator3, namespace Fator3\LinkedIn, prefixo linkedin/, Text Domain e Update URI preservados. Minor incrementado de 0.4.1 para 0.5.0. Nenhuma versão acompanhante foi renumerada.

| Base fornecida | Bytes | SHA-256 |
| --- | ---: | --- |
| wp-mcp-linkedin-fator3 0.4.1 | 102166 | `a1f2bd2393c7f1b1780f106f4a7c3ac46776a8a7cc7071f1e269daad7ec34c43` |
| Fonte recebida do mesmo pacote | 289465 | `059a201660863eef69e6dccffce9c67ac96cd580bf88bf3cea31ba712b2b21ff` |
| base-site-core-fator3 1.46.1 | 2185721 | `2e834ba27728a32a22fa588cc05863d1d69ccc2e09b0c05e016d88404eaadc76` |
| Fonte recebida do mesmo pacote | 3201244 | `add385d393dca6afe7c095a73b0476369fee658d0eca0e29cc66a4b2bc0f92e0` |
| wp-mcp-fator3 0.25.0 | 832809 | `7f32527a88514f2f319e02308f491b96b3112b783f1b38791da85aab071ea961` |
| Fonte recebida do mesmo pacote | 3005021 | `0ca0f140ba2b234f99067cb704a24aba43a85fd0855ba346a5ca709270c21fe4` |
| wp-mcp-google-fator3 0.17.0 | 767299 | `42bd11080b518c82e0960753fa7b08d7adae28743cfcd3e96f9b83bf3f4709b0` |
| Fonte recebida do mesmo pacote | 3312383 | `e76a58051a634eeb1f4c5dbb698a5847f13eb2309259a1d5449730ae89c6ea3c` |
| wp-mcp-meta-fator3 0.4.1 | 114664 | `719e3db7bb55f58cd08c2e78420e06374a6a4b08fad693e849677783ddc82de2` |
| Fonte recebida do mesmo pacote | 317219 | `79fb3d75075fe2cadc8b9b58b0dfe1a1f56901f7677ad8c9e4537e4109c6ecc7` |

Os relatórios recebidos dos cinco pacotes foram considerados como evidência recebida, sem convertê-los em testes desta rodada. Manifesto completo, incluindo documentos, está em inputs/manifest.json no fonte. Código relevante examinado: cliente e concessões Lead Reader/Core, decoração/autorização/mascaramento/auditoria MCP, renovação/incidentes Google e isolamento do Meta.

## 2. Convivência e encaminhamentos

Matriz local integrada: Core 1.46.1, MCP 0.25.0, Google 0.17.0, Meta 0.4.1 e LinkedIn 0.5.0; 89 verificações aprovadas. No Site-Teste, Core/MCP/Meta estavam nas mesmas versões, mas Google era 0.16.0. Essa instalação foi preservada; não se declara Google 0.17.0 instalado remotamente.

O pacote mantém autonomia de painel/REST/documentação/SDK. Core continua responsável por contatos, ingestão e deduplicação; não houve troca automática de provedor. Renovação mantém a revisão consumida pelo Core; reautorização nova conserva registros, mas exige reconfirmação de concessões. Meta e Google não foram modificados.

Um único encaminhamento técnico relevante: **wp-mcp-linkedin-fator3-0.5.0-impacto-wp-mcp-fator3.md**, iniciado no planejamento (R1) e atualizado até entrega (R3), situação aberto/acao-necessaria. O MCP 0.25.0 não oferece contrato público para exibir antes/depois no Registro. O LinkedIn implementou diário próprio e evento versionado; a implementação central continua com o responsável MCP. Arquivo preparado, sem envio a terceiros.

Implantador não foi fornecido e sua fronteira específica não foi avaliada; não se criou encaminhamento meramente informativo. Eventual implantação pela frota continua sob responsabilidade do dono. Não houve push ao repositório nem alteração em outros sites.

## 3. Mudanças por pedido e evidência

| Pedido | Entrega no pacote | Resultado e limite |
| --- | --- | --- |
| 5 | Rótulos e descrições em português em todas as abilities | Catálogo remoto conferido: 73; 42 IDs anteriores preservados, nenhum rótulo com identificador como texto |
| 6 | Gestão de grupos/campanhas/anúncios, conta/organização, publicações, comentários, inicialização de mídia, buscas e nova aba | Fluxos simulados aprovados; antes/depois no Registro central continua pendente do MCP |
| 7 | Refresh cifrado, manutenção, avisos, status e autorização opcional no navegador | Renovação/avisos simulados aprovados; primeira autorização/renovação real depende de app habilitado e aceite do dono |

São 31 operações novas. Os 41 schemas anteriores além de save-connection permanecem idênticos; save-connection recebe apenas refresh_token, refresh_expires_at e clear_refresh_token. Relatórios, SDK Lead Reader 1.0/1.1 e seleção explícita de ativos permanecem.

Gestão Ads cria sempre DRAFT. Ativação tem operação e confirmação separadas; pode iniciar gasto. Exclusão de rascunho usa DELETE; demais estados são marcados PENDING_DELETION, sem afirmar exclusão física. Campanhas aceitam campos do pedido e segmentação por nome, inclusões/exclusões, seleção de resultado ambíguo e páginas posteriores. Criativo confere conta, campanha, autoria da publicação e formulário selecionado. Leituras existentes continuam em query com paginação.

Cada escrita de gestão exige introspecção de escopos, ativo autorizado, revisão do objeto/conta/Página, prévia válida de dez minutos, chave request_key, confirmação, releitura e diário cifrado. Chave repetida retorna o resultado registrado; nova chave não libera intenção incerta. Travas serializam alvo/conexão no site. Existe janela de concorrência externa entre GET e envio: a API não oferece transação condicional implementada aqui. Não se promete exclusão dessa janela.

request_key é a chave do domínio. No MCP 0.25.0, omitir idempotency_key opcional do transporte nas duas fases ou diferenciar suas chaves evita conflito entre prévia/aplicação. confirm_token usa formato permitido pelo redator do MCP; nenhuma proteção de segredo foi removida. operation_id de domínio fica em data e correlaciona o diário.

Publicações: texto, imagem, vídeo e artigo com título/descrição/miniatura na criação; edição altera o texto, conforme Posts API. Comentário é em nome da Página selecionada e sobre publicação da mesma Página. Mídia precisa pertencer à Página e estar disponível. A operação de upload inicializa a autorização; não transfere bytes nem finaliza vídeo. O MCP pode redigir uploadToken; painel/REST autorizado fornecem as instruções. Essas limitações estão instaladas em MANAGEMENT.md.

Renovação usa sobreposição cifrada vinculada ao token/app-base: aumenta geração da credencial e preserva revisão de autorização, ativos, concessões, cursores e diário. Falha conserva token atual, abre incidente, agenda retentativa e aviso deduplicado ao admin_email. Sem refresh, avisa nas janelas observadas de 14/3 dias e após expiração. A execução depende de cron. Token manual permanece padrão; OAuth é opcional, com retorno HTTPS local, state de uso único vinculado ao administrador/sessão/revisão e validade de dez minutos.

Referências técnicas oficiais consultadas: [introspecção](https://learn.microsoft.com/en-us/linkedin/shared/authentication/token-introspection), [refresh](https://learn.microsoft.com/en-us/linkedin/shared/authentication/programmatic-refresh-tokens), [Posts API](https://learn.microsoft.com/en-us/linkedin/marketing/community-management/shares/posts-api?view=li-lms-2026-10) e [campanhas](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads/account-structure/create-and-manage-campaigns?view=li-lms-2026-09). O padrão mensal do pacote permanece 202609. Documentação técnica não substitui homologação com produto/conta reais.

## 4. Instalação, documentação e prontidão

| Prova própria nesta rodada | Resultado |
| --- | --- |
| PHP lint e sintaxe JS | 20 arquivos PHP; admin.js e management.js aprovados |
| Instalação limpa, WordPress 7.1.2 / PHP 8.3.6 / MySQL 8.0.46 | 61/61 verificações |
| Atualização direta da base imutável 0.4.1 | 63/63; dados, configuração e diário preservados |
| Matriz integrada com cinco plugins | 89/89, inclusive wrapper MCP, confirmação e filtros de saída |
| Interface DOM com HTML/JS do WordPress e REST autenticada | 12/12; prévia, edição/invalidação, rascunho confirmado e diário |
| Site-Teste WordPress 7.1.3 / PHP 8.3.36 | Troca aplicada, sete cenários sintéticos e oito autotestes locais aprovados |
| Documentação pelo MCP real | 16 documentos completos, 17 páginas, bytes e hashes iguais ao instalador |
| Build determinístico e runtime do fonte | SHA-256 e todos os arquivos iguais ao instalador final |

As contagens são execuções, com regressões repetidas entre ambientes; não são 213 casos únicos. HTTP/e-mail externos foram interceptados nos ensaios. Fixtures de timeout, escopo, proprietário, revisão, repetição, OAuth/state, renovação, falha/backoff, concessões e seleção passaram. A prova DOM não é captura visual de navegador.

Instalação no Site-Teste via WP MCP fator3-teste, plugins/upload-base64 com expected_slug e expected_sha256. Operação de pacote b6451e2a6e57c5724b9f6364a49a77df; backup b533be07d835c6a30c85955c. Resultado applied=true, ativo antes/depois, versão 0.4.1→0.5.0. Sondas home/REST retornaram 200 antes/depois, com PHP novo e bypass de cache verificado. Isso comprova bootstrap, não prontidão comercial.

A conferência encontrou manutenção sem agendamento no estado anterior. O ciclo normal de desativação/ativação apenas do LinkedIn restabeleceu f3_linkedin_maintenance; próxima execução observada 2026-10-22T15:03:04+00:00. A troca silenciosa de ZIP não executa necessariamente activation hooks. **Na frota, conferir access_lifecycle.next_maintenance após instalar; se nulo, fazer ciclo normal de ativação antes de confiar em renovação/avisos.** O plugin não faz reparo de cron durante leitura documental.

Aceite simulado no Site-Teste: prévia DRAFT sem envio, recusa de escopo, renovação automática preservando revisão, status de renovação, avisos de 14/3 dias com deduplicação e nenhuma escrita remota/e-mail real. Auxiliar temporário removido; catálogo linkedin-qa/ ficou vazio. Configuração final: zero conexões, criptografia/armazenamento prontos, audit_health=ok, LinkedIn ativo e cron agendado. Registros de auditoria sintéticos foram mantidos como rastro; configurações/prévias de teste foram removidas.

Instalador inclui especificação, configuração, uso, segurança, migração, recuperação, agentes, changelog e schemas. linkedin/documentation usa allowlist, offsets UTF-8, revisão e SHA-256; a leitura completa não consulta LinkedIn nem altera o armazenamento de domínio. Rótulos conferidos por discover-abilities; revisão visual da lista/tela pelo dono não foi simulada como prova.

## 5. Banco, preservação e reversão

Sem nova tabela ou ALTER destrutivo. Reutiliza f3_linkedin_records cifrada; novos buckets credential, credential_health, token_proof, oauth_state, write_preview, mutation e mutation_guard. Prévias/state expiram; diário de mutações e bloqueios de intenção não têm expiração automática. Prever backup e capacidade de armazenamento. Nenhuma assinatura comercial foi criada, migrada ou removida por instalação/autoteste.

Salvar configuração após refresh conserva token efetivo. Nova autorização/troca manual conserva seleções/registros, mas exige reconfirmar concessões/vínculo do diário: não se presume identidade remota igual. Remover token/segredo é ato explícito.

Rollback exige backup de arquivos, banco e salts, suspensão de escritores e exame do diário. A 0.4.1 ignora a sobreposição credential e pode reutilizar token-base antigo; planeje credencial válida ou reautorização. Restaurar banco não desfaz efeito remoto já ocorrido. Desinstalar conserva dados para limpeza explícita. Não apague diário para liberar repetição incerta.

## 6. Pendências e responsáveis

- **MCP / pedido 6(c):** contrato e exibição autorizada de antes/depois no Registro central. Diário local já existe; impacto R3 aberto.
- **Dono + aplicação LinkedIn / pedidos 6 e 7:** homologação real em ctooffice, somente após ordem e data: grupo/campanha DRAFT na conta 558431216, releitura, renomeação e exclusão; publicação/exclusão de teste na Página fator3 40774077; OAuth e primeira renovação automática real registrada. Nada disso foi executado nesta rodada.
- **Responsável LinkedIn + revisor:** repetir matriz nos mínimos declarados WordPress 6.4/PHP 8.1.2 de 64 bits. Cabeçalhos herdados foram mantidos, mas esta rodada só prova os runtimes da tabela acima; os mínimos não são suporte novamente comprovado.
- **Dono/revisor visual:** revisão manual da nova aba, retorno OAuth e lista de habilidades no navegador. DOM+REST cobre interação, sem provar layout visual.
- **Operação da frota:** conferir cron/validade e produtos/escopos/ativos antes de ativar uso; fonte permanece com o dono e nenhum envio/publicação em repositório foi feito.

Pedido 5 está implementado e conferido no catálogo. Pedidos 6/7 têm código e testes simulados entregues, com as dependências acima. O relatório não encerra pedido de outro responsável nem altera a aba central de governança.

## 7. Credenciais e dados

Nenhum token, refresh, segredo, cookie, banco de laboratório ou credencial real foi incluído. Fixtures usam textos sintéticos explícitos. O Site-Teste começou e terminou sem conexão LinkedIn cadastrada. Avisos de teste foram interceptados; nenhum email real foi enviado. Tokens continuam cifrados e ausentes das respostas de configuração. URLs assinadas de mídia não devem ser copiadas a logs/relatórios. Preserve salts ao restaurar backup.

## 8. Artefatos finais

| Arquivo | Bytes | SHA-256 |
| --- | ---: | --- |
| wp-mcp-linkedin-fator3-0.5.0-instalador.zip | 155689 | `dcef9a7b236bdb84055baa4aa6db73ba2fcd3bdd9a7cea30905c2e771a563199` |
| wp-mcp-linkedin-fator3-0.5.0-fonte.zip | 398863 | `00c7a230d61f85e43e69c9d0e3c0f31a88fa6dab4f4174ae6ce25c29fbf55486` |

Relatório externo: wp-mcp-linkedin-fator3-0.5.0-relatorio.md. Impacto técnico: wp-mcp-linkedin-fator3-0.5.0-impacto-wp-mcp-fator3.md. Somente o instalador é instalável. Fonte tem raiz wp-mcp-linkedin-fator3-0.5.0-fonte/, código, build, testes, evidências, normas e cópia interna deste relatório identificada como anterior ao fechamento. Nenhum ZIP contém outro ZIP da entrega. Os hashes finais são dos arquivos efetivamente entregues e do instalador aplicado no Site-Teste.
