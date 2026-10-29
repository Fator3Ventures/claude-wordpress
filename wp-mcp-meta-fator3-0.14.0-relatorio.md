# Entrega — Fator3 MCP Meta 0.14.0

Data: 28/10/2026, America/Sao_Paulo. Responsável: manutenção do pacote Meta. Base direta: 0.13.0. Pedido: MCP Meta 22.

**Relatório externo final.** O instalador testado está fechado. O fonte foi empacotado uma única vez; a cópia interna do relatório permanece identificada como anterior ao fechamento. Os hashes abaixo correspondem aos arquivos entregues.

## 1. Bases aceitas

A versão 0.14.0 implementa o Pedido 22: tokens de usuário do sistema sem o prefixo EAA devem chegar à validação remota, mantendo os controles de formato, aplicativo, identidade, permissões, ativos e persistência já existentes. A versão minor segue a regra comum; esta rodada não é uma revisão documental da base nem um patch solicitado da entrega anterior.

Foram considerados o documento atualizado “Fator3 MCP Meta(20261028-222150).md”, os novos instaladores, fontes e relatórios, a entrega Meta 0.13.0 e as instruções comuns. A revisão 5 preservada no fonte e a orientação expressa do dono prevalecem sobre a revisão 4 reanexada: impactos apresentam consequências e pedidos, nunca respostas ou encerramentos. Meta Ads está autorizado pelos Pedidos 20/21, apesar da fronteira antiga nas instruções r4.

| Base | Instalador em bytes | SHA-256 do instalador |
|---|---:|---|
| Meta 0.13.0 | 284069 | 3ecd6ee6f277c7581adc05b4fa38c46611e3232b4400bb4a4421956c9fba8ac1 |
| Core 1.59.0 | 2825862 | 8f3992e89b44f53a59e0e2af314ff8548fe2aadfcc06afe30e395610b1b7c832 |
| MCP 0.35.0 | 905542 | cd6c3afacff83bf38678b9fa2aaf80881be02879b362a9bab250fc56c9969483 |
| Google 0.22.0 | 856534 | a84754409f89b7b9c7367c1d261c44ef93c2f6039b379c3ec5c6242ec7188ebd |
| LinkedIn 0.12.0 | 304948 | 19748e788190f371809db469a6de052a645e25f39fad1672606dc776234ec54c |
| Pipedrive 0.3.0, preservado | 59877 | 30fc784a552a89351900c169fad7300759163fb886b842f45ba807bb0977f657 |

Os tamanhos/hashes dos novos fontes e relatórios estão em inputs/0.14.0/packages.json; foram calculados sobre os anexos recebidos, inclusive cópias com sufixos no nome. A base fonte Meta 0.13.0 tem 2268353 bytes, SHA-256 2d2ec08055c4ab8806b626d3c67097e7fa3cfaaf7f9ae3df18d1576cc4e8d2f7. Não se confundem hashes de ZIP e digests de árvore instalada.

## 2. Convivência, pedidos entre pacotes e impactos

**Nenhum novo relatório de impacto nesta rodada.** A mudança interna de credenciais não altera schema, contrato SDK, grant, identificador público ou obrigação de outro pacote. Não foi identificado impacto no plugin LinkedIn no escopo comparado e testado. Os cinco acompanhantes permaneceram com os mesmos arquivos, versões e ativação no Site-Teste.

O pedido Meta 0.13.0→Core para consumir meta-ads-reader/1.0.0 foi atendido pelo Core 1.59.0 recebido: o consumidor base-site-core-fator3 está registrado, com configuração f3base_meta_ads e operações meta-ads-status/meta-ads-report. A documentação Meta corrente foi atualizada. A prova própria com o código real do consumidor passou em 41/41 verificações, incluindo 30 dias sintéticos paginados, moedas separadas, associação de contato/parceiro, revisita, valor anterior datado, cursor e revogação. Essa é uma resposta/evidência no relatório principal; o impacto histórico permanece em history/0.13.0 e não foi reemitido como encerramento.

A exclusão coordenada de mensagens instagram-message-erasure/1.0.0 foi repetida com Core 1.59.0: 20/20, tabelas reais do Core no laboratório, contato sintético cifrado, recibo, apagamento e bloqueio de reimportação. Não houve contato ou notificação real.

Os novos recursos de conversão comercial do Core/Google/LinkedIn e o consumidor site-core-quality do MCP 0.35.0 foram examinados nas interfaces pertinentes. Não exigem alteração no validador de tokens Meta. A integração de transporte testou capacidades, perfis, identidade, filtros, recibos e revogação. LinkedIn 0.12.0 permaneceu chamável independentemente; Pipedrive 0.3.0 permaneceu sem concessão e sem chamada externa. Isso não equivale à homologação de todos os fluxos comerciais desses pacotes.

Não há ordem obrigatória nova de troca entre acompanhantes. As versões listadas são a matriz comprovada nesta rodada.

## 3. Mudanças por pedido e evidência

### Pedido MCP Meta 22 — token válido sem EAA

A reprodução na 0.13.0 usou token sintético alfanumérico de 199 bytes, iniciado em E e sem EAA. A base o recusou com invalid_token_format antes de qualquer HTTP ou alteração de dados: 3/3 verificações.

Em Credentials::format, foi removida somente a condição que exigia str_starts_with(token, 'EAA'). A função continua compartilhada pelos caminhos save-connection, rotate-token e switch-identity. A mensagem e a ajuda do campo agora descrevem o tamanho e a conferência remota, sem supor prefixo.

Mantidos: tamanho de 100–16384 bytes, espaços/controles recusados, reconhecimento de App Secret de 32 hexadecimais ou igual à chave informada, prova do app, debug_token, identidade /me, permissões necessárias e acesso aos ativos. Tokens recusados remotamente, expirados ou de outro app/usuário não substituem a credencial salva. Não se inferem validade ou ads_read apenas do formato.

A renovação da mesma identidade preserva autorizações, estado ativo/pausado e datas das agendas. A troca de identidade continua exigindo prévia, confirmação vinculada ao candidato e revisão atual. Locks e transações continuam protegendo conexão e agendas. Nenhuma geração foi fixada em 5: os testes percorrem a sequência real, incluindo 4→5; a primeira credencial provada na fixture resulta em geração 2 conforme a semântica existente.

Os 53 testes específicos passaram tanto após upgrade no WP 7.1.4 quanto no mínimo WP 6.4/PHP 8.1.2. Cobrem token sem EAA nos três fluxos, recusa de App Secret/tamanho/espaços/controles em todos eles, limites exatos, refusas remotas, CAS, confirmação, anonimato e ausência de segredos na auditoria/retorno. Os 55 testes de credenciais herdados foram repetidos na 0.14.0, incluindo tokens EAA, concorrência, falhas SQL/auditoria e permissões.

### Retenção, compatibilidade e documentação

Retenção ampliada da base permanece: não foi introduzida expiração, redução de prazo ou limpeza adicional. Políticas finitas explicitamente escolhidas continuam respeitadas. A atualização não recupera dados já apagados e não remove bloqueios/recibos de privacidade. Ads somente leitura, coletas parciais, Stories, mensagens e exportações não receberam mudança funcional nesta rodada.

O diff exato dos 59 arquivos do runtime tem 17 arquivos alterados e 42 idênticos. Alterações funcionais: validador e ajuda; demais diferenças: versão, dez documentos, documentação incorporada e manifesto. Os schemas públicos de entrada/saída e catálogo de operações permanecem iguais. São 30 arquivos PHP, 25 documentos instalados e 44 operações. Evidências: runtime-diff0140.json e runtime-diff0140.patch. build/common, build/meta e build/assets são canônicos; plugin/ corresponde ao instalador final.

## 4. Instalação, testes e prontidão

Ambiente compartilhado observado: Site-Teste, WordPress 7.1.4, PHP 8.3.36, MySQL 8.0.41. A atualização do WordPress para 7.1.4 já estava presente antes da troca Meta; não foi uma mudança desta entrega. O laboratório usa WordPress real com diretório e prefixo SQL próprios, sem apagar tabelas compartilhadas.

| Prova executada | Resultado | Evidência atual |
|---|---:|---|
| Reprodução do defeito na 0.13.0 | 3/3, recusa esperada | baseline-token-repro.json |
| Upgrade direto 0.13.0→0.14.0 | 10/10 | upgrade-proof.json |
| Pedido 22 após upgrade | 53/53 | upgrade-release0140.json |
| Instalação limpa WP 7.1.4/PHP 8.3.36 | 32/32 | current-isolated0140-smoke.json |
| Regressão de credenciais | 55/55 | current-release090.json |
| Ads e coletas parciais | 44/44 | current-release0130.json |
| Privacidade de mensagens + novo processo | 76/76 + 4/4 | current-privacy0120*.json |
| Interface e ajuda com HTML WordPress/jsdom | 25/25 | ui0140-dom.json |
| Integração com os cinco acompanhantes | 27/27 | current-integration0140.json |
| Exclusão coordenada com Core 1.59.0 | 20/20 | current-coreprivacy0140.json |
| Leitor Ads Core 1.59.0, primeira execução em instalação nova | 41/41 | current-coreads0140-fresh.json |
| Instalação limpa WP 6.4/PHP 8.1.2-1ubuntu2.28 | 32/32 | minimum-isolated0140-smoke.json |
| Pedido 22 no mínimo | 53/53 | minimum-release0140.json |
| Diagnóstico instalado no Site-Teste | 8/8 | site-final-selftest.json |

Lint dos 30 PHP e build concluídos. O mínimo foi instalado do zero novamente após preparar o PHP exato 8.1.2-1ubuntu2.28; não se tomou o PHP 8.1.34 inicialmente disponível como prova do mínimo. Pacotes oficiais e hashes estão fixados no preparador/lock. Os ambientes finais corrente e mínimo registraram zero Warning/Notice/Deprecated/Fatal atribuídos ao pacote no log e criptografia disponível.

A interface foi exercitada em jsdom 27.4.0 com HTML gerado pelo WordPress e admin.js real; REST/fornecedor foram simulados. Não houve inspeção visual em navegador. WP 6.4 não tem a Abilities API nativa; a autonomia local/REST e os 44 schemas foram provados nesse ambiente. O transporte MCP real foi conferido no ambiente corrente com MCP 0.35.0.

Duas falhas preliminares de preparação foram preservadas em evidence/development0140. A fixture nova esperava geração inicial 1, enquanto a base existente resulta em 2 após a primeira prova; corrigiu-se a expectativa. O teste Ads original do Core adicionava uma capacidade ao papel depois de o usuário corrente estar em cache; a primeira chamada falhava antes da concessão. O harness passou a recarregar o usuário após mudar o papel e o cenário completo foi repetido em nova instalação, passando 41/41 na primeira execução. Essas correções não alteraram o runtime Meta ou Core. Nomes históricos de suíte/check indicam origem; a evidência registra a versão efetivamente carregada.

O instalador final SHA-256 43e8947ac0ffaf3da52c62b0515db826e6df266553d64f5561c0d3b87b7eb318 foi aplicado no Site-Teste sobre 0.13.0, com slug e hash obrigatórios, chave de idempotência e pré-imagem. A operação cdb18016a04729ada90fc26721893490 confirmou 0.14.0 ativa em novo processo PHP. Sondas internas de / e /wp-json/ passaram antes/depois. A reativação foi silenciosa, sem ciclo de activation hook; a prontidão funcional foi conferida separadamente.

Estado final: health ok, storage/crypto prontos, auditoria ok, nenhuma conexão real configurada, nenhuma agenda ativa e nenhuma issue. O selftest não homologa fornecedor. Os dois registros de negócio e o histórico vazio mantiveram o mesmo digest; as sete opções Meta foram idênticas imediatamente antes/depois da troca. O digest agregado de opções já variara entre início da rodada e pré-instalação, antes da mudança Meta; não se atribui essa variação à 0.14.0 nem se afirma igualdade de toda a rodada. Auditoria operacional foi excluída do digest de negócio.

Documentação instalada: os 25 documentos foram lidos integralmente por meta/documentation através do MCP 0.35.0, com expected_revision, total de 220502 bytes e SHA-256/bytes iguais ao instalador. As respostas integrais estão em evidence/installed-docs0140; resumo em documentation0140-proof.json. A descoberta final, após limpeza, confirmou exatamente 44 operações Meta 0.14.0 e nenhum auxiliar QA (catalog0140-final.json).

Limpeza concluída: os laboratórios foram removidos com seus prefixos SQL próprios; as últimas provas de limpeza registram 98 tabelas no ambiente integrado e 14 no mínimo, zero remanescentes, diretórios e manifesto removidos. Os dois controladores temporários e o bundle foram excluídos com guarda SHA-256. Backups de mutações preservados pelo MCP conforme seu fluxo; nenhum auxiliar QA permanece carregado. Nenhuma tabela compartilhada foi apagada.

## 5. Banco, atualização e reversão

Não há migração nova, tabela/coluna nova, alteração de schema, mudança de retenção ou concessão automática. O teste de upgrade preservou byte a byte 11 registros/ciphertexts, uma linha de histórico e opções, incluindo conexão, agenda habilitada, material de mensagens/Stories e políticas finita/sem prazo. Não foi semeado histórico Ads/grants nessa prova de upgrade; esses caminhos foram exercitados nas suítes de regressão e integração, evitando alegar uma prova inexistente.

O Site-Teste tinha zero conexões reais, por isso o ensaio de renovação usou dados sintéticos isolados. Snapshots públicos contêm somente hashes/contagens; nenhuma credencial real foi exportada. O pacote não consulta ou modifica o banco dos acompanhantes fora dos testes isolados autorizados.

Rollback: reinstalar o instalador íntegro 0.13.0 preservando banco, salts, chave de privacidade, recibos, bloqueios e políticas de retenção. Não há SQL inverso a executar. A 0.13.0 mantém os dados e tokens já gravados, mas volta a recusar novas provas/renovações sem EAA. Evitar esse rollback caso a operação dependa do formato corrigido. Não restaurar token revogado, reduzir retenção ou apagar acervo como recuperação. A pré-imagem do instalador não constitui backup/restauração do banco; o transporte registra database_effects_reversible=false.

## 6. Pendências e responsáveis

| Pendência/limite | Responsável | Aceite |
|---|---|---|
| Token real do usuário do sistema em ctooffice.com.br | Operador/frota | Renovar por fluxo autorizado, conferir app/mesmo usuário, ads_read e geração real 4→5 se ainda estiver em 4; manter 32 hex recusado |
| Dados Ads de 30 dias | Operador/frota com acesso Meta/Core | Confrontar contas, campanhas, datas, fuso, moedas e valores com o Gerenciador de Anúncios; 30 dias sintéticos não substituem esse aceite |
| Próxima execução de agendas e coleta orgânica parcial | Operador/frota | Confirmar execução/resultado em janela real. Documento recebido informa follows_and_unfollows já recombinado; não repetir a recombinação como pendência de implementação |
| Publicação e implantação de frota | Dono/Implantador | Conferir hashes e documentos, publicar/instalar pelo processo existente; nenhum push ou produção nesta rodada |
| MariaDB e inspeção visual em navegador | Manutenção, se requeridos | Não executados; MySQL 8.0.41 e DOM são as provas disponíveis |
| Funcionalidades comerciais completas dos acompanhantes | Mantenedores dos respectivos pacotes | Fora da homologação desta entrega; testes aqui cobrem as fronteiras Meta descritas |

As pendências externas não são defeitos comprovados da 0.14.0 nem foram declaradas concluídas em nome de outro responsável. Prontidão local e integração pertinente: aprovadas; homologação com fornecedor real: pendente.

## 7. Credenciais e efeitos externos

Não foram lidos, copiados, renovados ou incluídos tokens reais. Tokens e App Secrets nas fixtures são sintéticos. Testes interceptaram HTTP Meta e e-mail; chamadas observadas de provas Graph são respostas simuladas. Não houve criação/envio de contato real, mensagem, notificação, anúncio, gasto Ads ou mudança em produção/ctooffice. O SDK de Ads permaneceu local e somente leitura. Os auxiliares de QA são temporários e restritos ao Site-Teste.

## 8. Artefatos finais

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-meta-fator3-0.14.0-instalador.zip | 286331 | 43e8947ac0ffaf3da52c62b0515db826e6df266553d64f5561c0d3b87b7eb318 |
| wp-mcp-meta-fator3-0.14.0-fonte.zip | 2577045 | 917f1f3d4fd0267fcf8b5f160e5b29d2548f67c5a8df9692fe2cbd1eff18c57f |

Relatório externo: wp-mcp-meta-fator3-0.14.0-relatorio.md. Apenas o instalador é instalável. Fonte único com build, código, testes, entradas, evidências sanitizadas e esta cópia; sem ZIP aninhado, banco, segredos reais, node_modules ou auxiliares ativos. Nenhum relatório de impacto novo. Entrega ao dono; publicação e implantação em frota não foram executadas.

