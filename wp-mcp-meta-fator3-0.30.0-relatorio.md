# Entrega — Fator3 MCP Meta 0.30.0

19/11/2026, horário de Brasília. **Pedidos MCP Meta 32.** Versão instalada no Site-Teste. Classificação: **com-pendencias** quanto ao aceite com contas reais de produção; apta no escopo de WordPress, canal e Graph simulada descrito abaixo.

## 1. Base de migração

Instalação limpa e atualização direta do Meta 0.29.0 oficial, sem versão intermediária. Fonte-base SHA-256 `e7efc56487a9db37c712841cc74a60058acd3628279e4cf3d00735cb7cd24db7`; instalador-base `730f9cd17ccba8a32081444643ea5a2b6b64a037752fdfdfee5c58753171e747`. Requisitos: WordPress 7.1.4+ e PHP 8.3+ de 64 bits. Bancada: WordPress 7.1.4, PHP 8.4.27 e MariaDB 11.8.6. Site-Teste: WordPress 7.1.5 e PHP 8.3.36. As duas diretrizes centrais foram lidas na revisão 5, de 02/11/2026; foram aplicadas também a aba Meta e a regra comum.

## 2. Convivência e escopo

Matriz final na bancada e no Site-Teste: **MCP 0.51.0, Site Core 1.96.0, Google 0.40.0, LinkedIn 0.26.0, Pipedrive 0.12.0**. Os dois ZIPs anexos do canal conferem com o relatório MCP 0.51.0. A atualização do Google observada durante a rodada foi incorporada à matriz final. Os registros de versões, tamanhos e hashes usados estão em `evidence/030/arquivos-de-entrada.json`.

O Meta continua lendo Instagram profissional, Páginas e Meta Ads, com histórico, agendamento e exportação. Escrita em anúncios não faz parte deste plugin; pixel, CAPI e contatos pertencem ao Site Core. A revisão não altera nomes, permissões, entradas das 47 habilidades, grants, cron ou contratos de consumidores. O canal foi testado com os novos valores de saída. O resumo operacional do Core lê `state`, `issues` e os totais legados; `partial_schedules` continua incluindo todas as parciais. O Core não precisa ser modificado para receber o estado corrigido e não precisa emitir e-mail por demografia indisponível. Nenhum impacto técnico que exija ação no LinkedIn, Google, Pipedrive ou canal foi identificado; nenhum relatório de impacto individual emitido.

## 3. Mudanças e provas — Pedidos MCP Meta 32

| Situação | Resultado verificado |
|---|---|
| Público por cidade, gênero, idade ou país sem dados e perfil correspondente com menos de 100 seguidores | A passagem recebe `outcome=nao_aplicavel`. A agenda informa motivo, seguidores medidos, mínimo, conta e instante em `availability_assessment`. Quatro agendas com perfil de 11 seguidores: saúde `ok`, quatro não aplicáveis, nenhuma falha. |
| Próxima execução, inclusive ao atravessar o mínimo | A agenda mantém habilitação e horário. A próxima passagem consulta os insights novamente. Com 99 seguidores, a exceção se aplica quando a resposta é vazia; com exatamente 100, vazio continua visível como falha e um detalhamento válido completa a coleta. Com 180, as quatro agendas coletaram sem nova leitura de perfil. Zero retornado numa linha válida é preservado. |
| Relatório de conta com dados úteis e lacunas só em `follows_and_unfollows` | Parcial esperada, inclusive com paginação e com detalhamento vazio; sem inferir a causa pelo total de seguidores. Uma métrica adicional ausente, uma recusa HTTP, um total inválido, o fim prematuro do plano ou a ausência de linhas úteis impedem o tratamento como parcial esperada. |
| Falha independente ou perfil sem prova suficiente | Vazio com contagem ausente, conta divergente, erro transitório, recusa da Graph e dados inválidos não recebem dispensa. A falha permanece localizável na agenda. As duas categorias esperadas não ocultam outros problemas de cron, orçamento ou autorização. |

Campos aditivos em `meta/health` e `meta/status`: `not_applicable_schedules`, `expected_partial_schedules` e `unexpected_partial_schedules`. O total histórico de parciais é a soma das duas últimas categorias. A coleta conserva o estado técnico terminal `status=partial` quando há lacunas; o aplicativo deve ler também `outcome` e o motivo. Suporte → Diagnóstico mostra as categorias separadas e explica a contagem de cada agenda. A leitura de saúde continua local. A chamada adicional `id,followers_count` só é feita após um retorno válido e vazio de demografia de seguidores, com o mesmo ativo e a mesma credencial, dentro do orçamento existente. A observação do perfil demonstra elegibilidade; não é uma confirmação do fornecedor sobre a causa específica do vazio.

**446 verificações automatizadas aprovadas**, sem falhas: 35 de elegibilidade; 5 da projeção da classificação pelo MCP; 58 de regressão de diagnóstico; 29 de orçamento, prioridade, quota e notificação; 18 de migração; 40 de inicialização e integridade; 44 da matriz com os acompanhantes; 14 do leitor de documentação; 200 de navegação e layout e 3 da tela de diagnóstico com contagens. A suíte de elegibilidade fez 58 leituras da Graph simulada, das quais 15 de perfil. Evidências: `evidence/030/`. Foram capturados 42 estados de tela com dados sintéticos, em 360, 768 e 1440 px.

## 4. Instalação e prova da troca

O instalador foi enviado ao **Site-Teste** pelo canal de teste autorizado, com slug e SHA-256 esperados, substituindo somente o Meta. Recibo: ativo antes e depois, versão 0.29.0 → 0.30.0, digest do ZIP igual ao da seção 8. Chamadas independentes posteriores: `meta/status` e `meta/health` informaram 0.30.0 e `ok`, sem tentativa de reparo; `meta/selftest` aprovou oito verificações; `system/health` indicou `healthy=true`. O Site-Teste tinha e manteve zero conexões e zero agendas ativas. Os 32 documentos foram lidos integralmente pelo MCP do site, com revisão conferida e conteúdo comparado byte a byte com o ZIP. A bancada verificou também descoberta, permissões e leitura integral pelo canal. Não se instalou dado, conta ou auxiliar de teste no WordPress compartilhado.

Para a frota, o responsável confere os hashes, publica conforme a regra vigente e usa o instalador com `expected_sha256` e `expected_slug=wp-mcp-meta-fator3`. Não houve publicação no repositório nem atualização de produção nesta rodada.

## 5. Banco, retenção e recuperação

Nenhuma nova tabela, coluna, migração de lotes ou política de expiração. A nova evidência é gravada nos registros de coletas/agendas e nas páginas de resultado da passagem; nenhum resultado antigo é reescrito só para corrigir a contagem. O painel pode mostrar o diagnóstico anterior até a próxima execução. Alterar a seleção da agenda limpa os indicadores da seleção anterior e preserva os jobs e resultados já gravados.

A troca de arquivos conservou os hashes de 16 registros de negócio, 4 linhas de histórico e 2 opções de negócio da massa de atualização, além das pausas, cursores, permissões, retenção finita e ilimitada e estado de migração. O marcador de inicialização da própria base foi medido após nova requisição ainda na 0.29.0. Antes da alteração no Site-Teste foram criadas cópias privadas das duas tabelas Meta (714 linhas) e das opções Meta (12 linhas). Nenhum valor de banco foi incluído nos arquivos de entrega. Correções posteriores exigem versão nova; não se prescreve downgrade.

## 6. Aceite em campo pendente

Leitura de produção **somente da 0.29.0**: Conselar e Fator3 Grupo apresentavam quatro falhas de público e uma parcial diária; no fator3.com.br as cinco agendas estavam completas. Os três estados estão em `evidence/030/producao-base.json`. Essas leituras comprovam a referência do pedido; as contagens da bancada são sintéticas. Não houve verificação da nova versão com credencial comercial real. A operação da Graph e o cron natural da frota permanecem pendentes de homologação.

Após a atualização autorizada da frota, aguardar uma passagem das quatro agendas nos três sites, conferir a contagem lida e as classificações por agenda em `meta/health`, o estado da diária e a continuidade da conta acima do mínimo. Caso haja falha independente, o estado global deve continuar `degraded` e identificar a causa. Não é necessário editar agendas para obter a nova medição.

## 7. Credenciais e configuração

A atualização não exige regravar credenciais nem ampliar escopos. Na configuração inicial, o dono cola token e segredo na tela de Conexão; o administrador preenche identificação e App ID, confirma ativos, validade e escopos no painel. Graph padrão v24.0. Instagram/Páginas: pages_show_list, pages_read_engagement, read_insights, instagram_basic e instagram_manage_insights conforme o recurso; ads_read só para anúncios/datasets. Não cole credenciais em conversas nem no relatório. Consulte CONFIGURATION.md.

## 8. Identidade dos arquivos

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-meta-fator3-0.30.0-instalador.zip | 282739 | `9c9b1577638a1feac9edd0bee6041ea5713631ffb5bc236e100042e91727eeee` |
| wp-mcp-meta-fator3-0.30.0-fonte.zip | 18407054 | `cbe231112355ce6e2fb5548e47750d58ac7ad12d28a9f1593d8dfb517f84e7a9` |
| wp-mcp-meta-fator3-0.30.0-capturas.zip | 4442978 | `50693b538b7d53d9581a0c4da26f8744828291f1c950d97dd4bde018e0d9325b` |

A cópia de relatório contida no fonte precede o fechamento desse ZIP.
