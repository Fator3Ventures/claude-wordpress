# Entrega — Fator3 MCP Pipedrive 0.7.0

Revisão 1 · 2026-11-05T13:17:23-03:00 · Rodada: implementação.  
Slug: `wp-mcp-pipedrive-fator3` · Versão: 0.7.0 · Build identificado pelo SHA-256 do instalador na seção 8.  
Status: **apta-no-escopo-testado**. O Site-Teste está com a 0.7.0 ativa. A auditoria separa falta de dados de falta de atividade; a configuração permite corrigir a confirmação sem repetir a simulação.

## 1. De onde esta versão entra

Atualização direta da 0.6.0 ou instalação limpa. O instalador-base oficial, usado na bancada e identificado antes da troca no Site-Teste, tem SHA-256 `0cfec48e6142064d6024b49e9026e79e359178ae04846fd5c442597c6b70908e`; origem e identidade do fonte em `inputs/README.md`. A release substitui a 0.6.0. Documentos centrais do projeto: revisão 5 de 02/11/2026; plano no fonte.

Requisitos: WordPress ≥ 7.1.4 e PHP ≥ 8.3, site único, PHP de 64 bits com OpenSSL/mbstring e InnoDB. Instalação limpa observada: **WordPress 7.1.4, PHP 8.3.36, MySQL 8.4.11**. O ensaio comparativo local usou PHP 8.3.6. Não se amplia essa prova para combinações não executadas.

## 2. Convivência e encaminhamentos

| Plugin | Início no Site-Teste | Cópia testada com o Pipedrive 0.7.0 | Final no Site-Teste |
| --- | --- | --- | --- |
| Site Core | 1.71.0 | 1.71.0 | 1.71.0 (ativo) |
| MCP | 0.40.0 | 0.40.0 | 0.40.0 (ativo) |
| Google | 0.28.0 | 0.28.0 | 0.28.0 (ativo) |
| Meta | 0.20.0 | 0.21.0 | 0.21.0 (ativo) |
| LinkedIn | 0.18.0 | 0.18.0 | 0.18.0 (ativo) |

O inventário final concorda com as versões congeladas para a prova de integração. Só o Pipedrive foi substituído por esta rodada. O Core fornece o cliente `pipedrive-api-client/1.0.0`, a autorização, a credencial e o orçamento; o MCP fornece transporte e política de conexão. Ausência de autorização suspende operações de conta, preservando a Ajuda e as leituras administrativas locais. Não há alteração obrigatória em acompanhantes nem nova ordem de troca.

O **Pedido Core 294, C1–C8**, permanece como contrato em regressão. As mudanças desta rodada são internas: proteção de recibos, coleta de dados via contrato existente e interface do próprio Pipedrive. A revisão dos relatórios de acompanhantes e dos limites de Google, Meta e LinkedIn não identificou providência técnica para seus mantenedores. Não se emitiu relatório de impacto. O Implantador não integrou a bancada. Origem, escopo e limites da pesquisa sobre pedidos estão em `inputs/README.md`.

## 3. Mudanças e evidência

A nova rodada solicitada pelo dono não tem número de ticket. Mantêm-se os itens herdados de **Pedidos MCP Pipedrive 10**, sem alterar sua situação de homologação comercial na aba de origem.

| Frente | Problema e mudança | Prova |
| --- | --- | --- |
| Auditoria e contagem | Uma página incompleta podia produzir “sem próxima atividade”; vínculos duplicados consumiam espaço antes da deduplicação. A avaliação agora considera a cobertura de cada fonte, indexa vínculos uma vez e distingue achado, item não avaliado e resultado truncado. Cada lista de achados/não avaliados admite até 1.000 itens; o agrupamento mantém até 200 chaves ordenadas com contagens exatas para os grupos devolvidos. Registros exigem ID; catálogos aceitam a chave do campo. | Mesma suíte de 25 verificações no WordPress: **9 passaram e 16 falharam na 0.6.0; 25 passaram na 0.7.0.** Falhas são da comparação intencional com a base. Evidências: `baseline060-insights070.json`, `current-insights070.json`. |
| Escritas e reconciliação | O recibo WhatsApp reconhece a mesma entrada mesmo com ordem diferente de propriedades. Cada operação devolve apenas os recibos que lhe pertencem. Uma etapa só prossegue se o diário confirmar a anterior; a expiração do diário ou uma escrita direta não deve contornar reconciliação pendente. O mesmo UUID de lead, escrito com letras maiúsculas ou minúsculas, respeita a mesma pendência. Para marcadores antigos, o plugin examina até 64 marcadores e até 256 grafias quando o vínculo não pode ser determinado por um recibo legível. Sem prova de que o marcador pertence a outro registro, interrompe a escrita antes do fornecedor; negócios continuam isolados pelo ID numérico. | 34 verificações em `current-writes070.json`: replay, mudança de conta/ator, ambiguidade histórica, diário removido, checkpoint interrompido e retenção. Nenhum envio externo. |
| Interface de configuração | Na etapa de confirmação, frase incorreta ou ordem não marcada conserva a prévia válida do mesmo administrador. A regra não muda, o prazo não se estende e não há nova consulta aos leads. Prévia vencida ou de outra revisão requer nova simulação. | Chromium 152.0.7940.0: 38 verificações, incluindo recuperação do formulário, revisão concorrente, nonce, acesso e tela estreita; `browser.json`. |
| Documentação | Ajuda reorganizada por tarefa; guias completos exibem títulos, listas, tabelas e código escapado. Exemplos JSON permanecem texto original paginado, com verificação de revisão. Atualizados índice, contratos, recuperação e notas de release. | Os 12 documentos do ZIP foram lidos pelo MCP do Site-Teste e comparados com seus bytes originais (`shared-documents.json`). |

**Custo da auditoria:** com 2.000 leads, 2.000 negócios e 2.000 atividades sintéticos, a mediana local caiu de **602,207 para 53,404 ms**. Foram sete processos intercalados por versão, com aquecimento; cada auditoria fez 62 GET simulados e produziu os mesmos 40 achados, com SHA-256 idêntico. `tests/bench-audit070.php` e `evidence/audit-benchmark070.json` permitem reproduzir a medição. Ela mede processamento PHP com dados em memória, não o tempo de rede, o WordPress nem a latência de uma conta real.

## 4. Instalação e prova da troca

O mesmo instalador da seção 8 passou por instalação limpa e atualização direta em WordPress isolado. Na integração, o plugin ativo conviveu com os cinco acompanhantes; a simulação de dados e dos efeitos do fornecedor ocorreu somente nas bancadas. A linha abaixo distingue asserções das suítes do número de verificações do pacote.

| Cenário | Asserções aprovadas, por suíte | Evidências JSON no diretório `evidence/` do fonte |
| --- | --- | --- |
| Operações nativas, relatório e retenção | 90 + 49 + 33 | `current-native`, `current-report`, `current-retention` |
| Regressões de release, requisitos e qualidade | 56 + 48 + 32 | `current-release`, `current-requests050`, `current-quality060` |
| Integridade e auditoria 0.7.0 | 34 + 25 | `current-writes070`, `current-insights070` |
| Coexistência MCP e fluxos Core | 42 + 8 + 6 + 7 | `current-integrated`, `current-core`, `current-core-report`, `current-core-workflows` |
| Atualização direta e novo processo | 15 + 2 | `upgrade-verify-upgrade`, `upgrade-upgrade-restart` |
| Documentos no WordPress e interação no navegador | 17 + 38 | `ui-documents050`, `browser` |

**502 asserções aprovadas: 464 em PHP e 38 no navegador.** A matriz equivalente do fonte 0.6.0 tinha 432; diferença de 70 (34 de integridade, 25 de auditoria e 11 adicionais de navegador). Esse total soma cada suíte principal uma vez. Protótipos, tentativas, benchmark e o verificador de entrega não entram nessa contagem. Separadamente, o verificador final passou em 101 verificações, com lint de 43 arquivos PHP, reconstrução do ZIP e comparação dos 35 arquivos do runtime.

**[Site-Teste](https://fator3-teste-mcp-1.dreamhosters.com/):** `plugins/upload-base64` com `activate=true`, `overwrite=true`, `expected_slug=wp-mcp-pipedrive-fator3` e o SHA-256 da seção 8. Recibo `4d7fff07e0179395dbeb542900d5f17e`, pré-imagem de arquivos `008a119087416d73a6e59449`, recuperação `applied`. O recibo registra 0.6.0 → **0.7.0 ativa**, confirmação em nova requisição PHP independente e respostas HTTP 200 de `/` e `/wp-json/` antes e depois. São sondas internas à origem com cache contornado; não representam acesso público externo.

Em `pipedrive/status {}`, resultado `operacao_nao_autorizada`. O cliente está registrado, mas a autorização comercial neste site continua desativada. A recusa é o resultado esperado. A descoberta final encontrou 19 operações Pipedrive e nenhuma operação temporária desta rodada. Leitura de `pipedrive/documentacao-ler {}` e de cada ID até o fim: **12 documentos em 16 páginas**, todos idênticos à versão instalada. O documento `schemas` tem 50.199 bytes e SHA-256 `7f102b6fb852beb0bd6f88b79d95dcb8d6f9dc3f47bed353c9b299f02a565165`; a continuação usa `offset` e `sha256_esperado`. Saúde do MCP: `healthy=true`. Os três diretórios de bancada foram retirados; nenhuma tabela com seus prefixos permaneceu. Os dois controladores temporários e o ZIP de testes foram removidos.

## 5. Banco, migração e correção por nova versão

Schema próprio **1**, sem migração estrutural. A bancada de migração semeou 4 operações e 3 entradas de diário na base 0.6.0, incluindo recibo WhatsApp, regra de cadência, política finita e pendência. Após a atualização, as linhas, os valores brutos/revisões, a retenção e a pendência permaneceram. Repetir a chave original no mesmo contexto sintético devolveu o recibo sem nova escrita; mudança de contexto impediu o replay. Novo processo e reativação mantiveram a escolha de retenção. Evidências: `upgrade-seed-upgrade.json`, `upgrade-verify-upgrade.json`, `upgrade-upgrade-restart.json`.

No Site-Teste, as tabelas próprias conservaram 0 operações e 0 linhas de diário. Os hashes das linhas, das regras, da política de retenção e da opção de autorização do Core permaneceram iguais; prazo do diário: 0 dias (zero significa sem prazo). `shared-preinstall.json` e `shared-snapshot.json` demonstram a preservação desse estado selecionado, sem divulgar valores de configuração ou credenciais.

Nenhum job, webhook, transporte HTTP ou token próprio foi criado. A pré-imagem da instalação cobre os arquivos do plugin, não o banco inteiro. Após falha, preservar banco, salts, diário e recibos; reconciliar o efeito externo antes de nova tentativa. Uma correção após a instalação exige nova versão; não há downgrade.

## 6. O que permanece pendente

- **Dono/frota — Pedido 10:** permanece pendente o aceite comercial em `korvena.com.br`, com campos, permissões e ativos reais da conta autorizada. O Site-Teste usou respostas sintéticas; não se enviaram mensagens a clientes nem se modificaram negócios reais.
- **Frota — distribuição:** o instalador não foi publicado na raiz raw do repositório público. O endereço previsto após publicação é `https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-pipedrive-fator3-0.7.0-instalador.zip`. Esse endereço não foi usado para a troca no Site-Teste. Antes de instalar na frota, publicar somente os artefatos autorizados, conferir o SHA-256 dos bytes servidos e usar `expected_sha256` e `expected_slug`. O fonte permanece com o dono (decisão 89).
- A prova de interface exerceu formulários em Chromium com backend WordPress isolado. Não homologa a sessão visual autenticada do painel compartilhado, outros temas, uma conta Pipedrive real ou uma nova concessão OAuth no canal MCP. A evidência de coexistência não é homologação de APIs de Google, Meta ou LinkedIn. Não foi localizada uma aba central do Pipedrive mais recente do que a cópia identificada em `inputs/README.md`.

## 7. Credenciais e configuração do dono

O token de API Pipedrive (`f3base_pipedrive_token`) fica **no Site Core**, junto à identidade da conta e do usuário autorizados pelo dono. No site-porta correto, configurar pelo contrato do Core `f3base_pipedrive_operacao.ativo` e conceder o consumidor `wp-mcp-pipedrive-fator3`; verificar com `pipedrive/status`. Não habilitar essa permissão no Site-Teste apenas para executar a bancada. O painel Pipedrive não recebe token e não cria credencial própria.

As operações e o painel exigem administrador com `manage_options`; pelo MCP também se exige o perfil explícito da conexão, com leitura e escrita separadas. Abrir **Ferramentas → Fator3 MCP Pipedrive → Ajuda** para configurar regras, simular e revisar antes de aplicar. Nenhum valor de credencial deve ser informado no chat, em fixtures ou no relatório.

## 8. Identidade dos arquivos

| Artefato | Nome final e link | Bytes | SHA-256 |
| --- | --- | ---: | --- |
| Instalador WordPress | [wp-mcp-pipedrive-fator3-0.7.0-instalador.zip](wp-mcp-pipedrive-fator3-0.7.0-instalador.zip) | 118.218 | `8f58b26c8408c02604c16bcfd30fcb92e3bbae308ebc107defad21555e5b5779` |
| Fonte | [wp-mcp-pipedrive-fator3-0.7.0-fonte.zip](wp-mcp-pipedrive-fator3-0.7.0-fonte.zip) | 295.866 | `2b1d0c1f5dad13a31beb348fe9c249acde678a29dbb7081c05b7597cef07677d` |

Relatório externo canônico. A cópia no fonte é anterior ao fechamento. O ZIP do fonte foi conferido integralmente: raiz única, sem ZIP aninhado e todos os bytes de runtime iguais aos do instalador. Apenas o instalador é instalável. A raiz do instalador é `wp-mcp-pipedrive-fator3/`; a do fonte é `wp-mcp-pipedrive-fator3-0.7.0-fonte/`. O fonte contém código, build, testes, evidências sanitizadas, documentação e a cópia interna deste relatório.
