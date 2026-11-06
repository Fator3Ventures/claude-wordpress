# Entrega — Fator3 MCP Meta 0.21.0

Revisão 1 · 2026-11-05T13:48:50-03:00 · Rodada de implementação. **Ativa no Site-Teste; apta no escopo testado.** A homologação do Pedido 27 com credenciais dos sites de produção continua pendente.

## 1. De onde esta versão entra

Base direta **0.20.0**, instalada no início e conferida pelos bytes da entrega: instalador de 332569 bytes, SHA-256 `2f229301c8dd08357ed9d023edc1d610ac1b78e01114dce45913e1979b95399b`; fonte de 740886 bytes, SHA-256 `3c99d98805db6075e22e3351cb15dd6493e117d8b1bb37b8b1076b869e4d7076`. Esta é uma nova rodada de revisão de código, funcionalidades, testes, painel e documentação. Não foi inventado um número de pedido de frota para as correções.

Requisitos declarados no cabeçalho, readme e build: **WordPress ≥ 7.1.4 e PHP ≥ 8.3 de 64 bits**. Testes em WordPress 7.1.4, PHP 8.3.36, MySQL 8.4.11; lint/build local PHP 8.3.6. O patch PHP 8.3.0 exato não foi exercitado. Slug, provider e basename preservados: `wp-mcp-meta-fator3/wp-mcp-meta-fator3.php`. Aplicados os normativos de agentes e de desenvolvimento, ambos revisão 5. O plano e a análise de fronteiras estão em planning/.

## 2. Convivência e encaminhamentos

No início: Core 1.71.0, MCP 0.40.0, Google 0.28.0, LinkedIn 0.18.0 e Pipedrive 0.6.0. No fechamento: Core 1.71.0, MCP 0.40.0, Google 0.28.0, LinkedIn 0.18.0 e **Pipedrive 0.7.0**. O recibo desta manutenção comprova instalação exclusiva do Meta. A atualização concorrente do Pipedrive tem relatório próprio. Não foi executada uma matriz cruzada entre versões antigas. Não se exige ordem especial de troca para esta release.

Foram examinados o transporte e a documentação MCP, as autorizações atuais do SDK de monitoramento do Meta, as referências dos pacotes vigentes e a seleção do painel. Core já informa a conta Ads e o dataset e verifica a concessão do consumidor; a exportação administrativa não é sua interface. LinkedIn, Google e Pipedrive não consomem os arquivos administrativos desse fluxo. Quatro arquivos de contratos públicos (entradas, saídas, catálogo de operações e schema de privacidade) são idênticos aos da base. Não foi identificado pedido de alteração a outro mantenedor; portanto, não foi emitido relatório de impacto. Isto não homologa cada função comercial desses plugins.

## 3. Mudanças e evidências

| Fluxo | Falha reproduzida na 0.20.0 | Comportamento na 0.21.0 |
|---|---|---|
| Autorização de dataset | O histórico direto negava a leitura após remover a conta Ads, mas um administrador proprietário ainda conseguia obter partes de uma exportação concluída e páginas do job do mesmo dataset. | A cada leitura de dado retido, o servidor verifica origem, conexão, dataset e a conta Ads da consulta original. A recusa `asset_access_denied` não devolve linhas nem bytes. O teste cobre novo pedido, repetição idempotente, etapa e parte de arquivo anterior; Instagram independente continua permitido. |
| Retenção e reautorização | Uma exportação enfileirada podia passar a falha terminal ao perder o escopo. | Revogar bloqueia o acesso sem mover o cursor nem apagar o arquivo. Se a seleção for explicitamente restabelecida, os mesmos bytes retidos voltam a ser acessíveis, sujeitos às demais permissões. Arquivos que já saíram do site não podem ser recolhidos. |
| Escrita incerta de uma parte | Falha sintética de releitura depois de persistir a parte cifrada deixava o recibo terminal, impedindo reconciliação pelo mesmo ID. | A mesma etapa, repetida depois da falha, reconhece a parte existente e avança uma vez. A prova verifica checkpoint, contagens, linhas, bytes e conclusão; não se repetem partes nem se usa outra chave para contornar o erro. |
| Painel e mudança de seleção | Respostas tardias, cursores e ações de A podiam aparecer sob B, inclusive depois de voltar para A. O formulário de webhook conservava um rascunho da conta anterior. | Relatórios, Histórico, Conversas e Arquivo de Stories descartam o conteúdo e a continuação da seleção anterior. A prévia de um job permanece no seu cartão. A troca interrompe o download do histórico iniciado pelo painel; não cancela retroativamente tarefas já aceitas. Estado de carregamento e instruções indicam quando consultar de novo. |
| Ajuda | O índice PHP repetia integralmente os manuais instalados. | O build fixa nomes, tamanhos e hashes; o leitor abre apenas o documento solicitado e não devolve bytes que divirjam do índice. Testes recusam alteração do mesmo tamanho, arquivo ausente, link para fora de docs/, caminho não listado e revisão obsoleta. Índice PHP: **340710 → 4152 bytes**. Instalador: **332569 → 243040 bytes**. Não foi medida latência de página em produção. |

**Reprodução separada da base.** Nos mesmos 21 cenários de interface, a 0.20.0 falhou em 14 e passou em sete controles. Os 22 checks de reprodução no WordPress da base confirmam comportamento anterior e controles, incluindo o defeito; não entram na soma de aprovações da versão entregue. Dados sintéticos demonstram um defeito reproduzível, não evidência de acesso indevido na frota.

**Matriz da versão entregue: 274 verificações, zero falhas.**

| Escopo | Suíte | Aprovações |
|---|---|---:|
| DOM | ui-dom | 19 |
| DOM | ui-identity | 22 |
| DOM | ui-messaging | 17 |
| DOM | ui-monitoring | 15 |
| DOM | selection-race-candidate | 21 |
| PHP isolado | docs-integrity | 10 |
| WP | lab-current-smoke | 36 |
| WP | lab-current-configuration | 16 |
| WP | lab-current-dataset | 77 |
| WP | lab-current-export | 27 |
| WP | lab-upgrade-upgrade | 14 |

Total por ambiente: 94 interface DOM com transporte simulado; 10 PHP isolado sobre cópia descartável dos manuais; 170 WordPress real. A suíte de exportação da candidata passou em 27 verificações, sem qualquer chamada HTTP. A suíte de datasets usa HTTP simulado e conferiu coleta parcial, autorização, controles e SDK local. Contagem exclui leitura final pelo MCP, inspeção humana em navegador, lint e reproduções da base. Código, procedimentos e evidências sanitizadas acompanham o fonte.

## 4. Instalação e prontidão

Site autorizado: https://fator3-teste-mcp-1.dreamhosters.com/. Atualização por `plugins/upload-base64` com expected_slug e expected_sha256; operação `c9e6ea556071b59d39edeebb4c430d6f`, pré-imagem de arquivos `eda8f1f5c6fb606969e481c1`. Versão anterior 0.20.0, final 0.21.0, ativa antes/depois, SHA do recibo idêntico ao desta entrega. Sondas internas de / e /wp-json/: HTTP 200, antes/depois. A distribuição raw fica com a frota: após publicação autorizada, conferir bytes efetivamente servidos antes de plugins/upload. Nenhum push ou distribuição em produção foi feito nesta rodada.

- Instalação limpa da 0.21.0 em prefixo exclusivo, sem acompanhantes; migração em outro laboratório, a partir da 0.20.0 efetivamente ativada e semeada. Diferenças de histórico de origem ou downgrade não foram usados como prova.
- Migração direta preservou 13 registros de negócio e 4 linhas históricas, incluindo credenciais sintéticas cifradas, concessões, política de retenção finita e ilimitada, agenda e cursor do job pausado.
- No site compartilhado, os dois registros de negócio, o histórico vazio e a configuração de monitoramento do Core conservaram os hashes. Duas opções internas mudaram entre capturas: f3_meta_last_maintenance e f3_meta_queue_migration. Não se atribui causalidade à atualização com base apenas nessa diferença. O snapshot não inclui a auditoria técnica das operações de teste.
- O Meta instalado bate nos 66 arquivos com a árvore do ZIP, digest `6f03ecac39ded68cc593fab53f65eb4bbcad62f30d54143fee37e029ddf7526e`. Core, MCP, Google e LinkedIn preservaram as árvores no intervalo; Pipedrive avançou separadamente. Ao final, `meta/health` retornou `ok`, storage/crypto prontos, zero conexões comerciais e zero agendas ativas.
- **Navegador autenticado:** no desktop, Relatórios mostrou versão 0.21.0, estado sem conexão e conta desabilitada. Conexão mostrou os quatro grupos e retenção ilimitada por padrão. Na Ajuda, o índice carregou, o guia administrativo da versão abriu e “leitura completa” foi confirmado visualmente. Nenhuma configuração foi gravada. As corridas entre contas foram exercitadas nas fixtures de interface.
- **Documentação MCP:** descoberta e schema da operação estática; índice da base e do alvo conferidos. Todos os **28 documentos** da 0.21.0 foram lidos integralmente em **33 páginas**, fixando expected_revision, conferindo bytes e SHA-256 a cada documento contra o runtime entregue. Descoberta final: 47 operações Meta 0.21.0 e nenhuma habilidade QA.
- Os três laboratórios (reprodução, limpa e migração) encerraram com zero tabelas remanescentes e seus diretórios removidos. Controller e bundle foram excluídos com guarda de hash e backup. Os backups técnicos do servidor permanecem sob sua política própria.

## 5. Banco, migração e correção por nova versão

Sem DDL, nova option de negócio ou regravação em massa. A mudança de autorização é aplicada na próxima leitura, inclusive a arquivos anteriores, sem varrer nem apagar acervos. Resultados e partes cifradas, revisões, grants e retenção permanecem no formato vigente. Não é necessária uma tarefa de reparo de dados para instalar.

Antes da instalação, preserve backup consistente de banco e salts. Após escrita de confirmação incerta, releia o recibo e avance novamente pelo mesmo export_id; não repita uma mutação externa sem reconciliar seu efeito. Falha futura deve ser contida e corrigida em nova versão a partir do estado existente. Não há downgrade.

## 6. Pendências e limites

O **Pedido MCP Meta 27** continua com aceite externo pendente em korvena.com.br e ctooffice.com.br: a frota precisa executar a agenda com o token salvo nesses sites e verificar linhas no leitor do Core, ou recusa legível e ação concreta. Esta rodada não usou credenciais Meta reais nem reabriu esse pedido. Não houve gasto Ads, publicação, contato comercial ou envio real de e-mail.

Não foi feita homologação em dispositivo móvel, leitor de tela ou com duas contas reais no Site-Teste, que estava sem conexões Meta. A inspeção autenticada de desktop e a matriz sintética são evidências distintas. Não foi feita atualização dos sites de produção.

## 7. Credenciais e configuração do dono

A atualização não exige novos segredos ou escopos do fornecedor. Para configurar uma conexão válida, use Ferramentas → Fator3 MCP Meta → Conexão: nome, App ID, App Secret e token de usuário do sistema; informe validade UTC apenas quando houver. Para dataset, em Ativos, confira tanto o dataset quanto a conta Ads vinculada à consulta. Uma cópia anterior no histórico não substitui essa seleção. Referências operacionais: ADMINISTRATION.md, OPERATIONS.md e SECURITY.md; nenhum valor de credencial real está na entrega.

## 8. Identidade dos arquivos

| Artefato | Nome | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | wp-mcp-meta-fator3-0.21.0-instalador.zip | 243040 | `9589456a2ee5ed13cb72941437e4350c0815907f6ba20b8eb47837a77064334a` |
| Fonte | wp-mcp-meta-fator3-0.21.0-fonte.zip | 672186 | `d53c738b10c59084f5c1e581cfcd408caffb45f004c04683e47f56fcbf3e9b49` |

Somente o instalador é instalável. O fonte contém runtime idêntico, build, testes, evidências e a cópia anterior ao fechamento do fonte. Tamanho e hash finais do fonte são preenchidos no relatório externo depois de empacotar, sem modificar o ZIP e sem autorreferência. Nenhum ZIP da entrega contém outro ZIP.
