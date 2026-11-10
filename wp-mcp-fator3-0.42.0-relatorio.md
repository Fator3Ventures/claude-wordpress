# Entrega — Fator3 MCP 0.42.0

Revisão 1 · 09/11/2026 · Correção e homologação de **Pedidos MCP 78**, correspondente à pendência 136 da frota. Estado da entrega **apta-no-escopo-testado**. O Site-Teste executa o instalador desta entrega.

## 1. De onde a versão entra

Instalação limpa ou atualização direta da versão entregue 0.41.0. O Site-Teste confirmou a base antes da troca. Instalador anterior de 936.186 bytes, SHA-256 `4a31d22788d66b9342efdc25d4b75d919efa4320035bc607c0b396691ca783e5`. Fonte anterior de 4.461.108 bytes, SHA-256 `09e6c3c34b85f3ad4b5828ec7c9335a9667f9a463e890261f40b550f86824534`. A aba de pedidos de 09/11 às 23:28 continha o pedido 78.

Requisitos mínimos de WordPress 7.1.4 e PHP 8.3. A bancada usou WordPress 7.1.4, PHP 8.3.6 e MySQL 8.0.46. O Site-Teste respondeu com WordPress 7.1.4 e PHP 8.3.36. As duas fontes normativas vigentes foram lidas integralmente: `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambas na revisão 5 de 02/11/2026.

## 2. Convivência e encaminhamentos

| Pacote ativo na bancada integrada e no Site-Teste | Versão | SHA-256 do instalador de bancada |
|---|---|---|
| Fator3 Site Core | 1.76.0 | `d830b488509814f44f4d78109cf8669e6b09717d9cbc50a0b42a1545f4a5f3ea` |
| Fator3 MCP Google | 0.31.0 | `e577dd444b063d99e42a4c63840095d9f176f82bd864e21d09c76a877d9e670e` |
| Fator3 MCP Meta | 0.21.0 | `9589456a2ee5ed13cb72941437e4350c0815907f6ba20b8eb47837a77064334a` |
| Fator3 MCP LinkedIn | 0.19.0 | `613cb47cfb3be2b91dfa1f20f39c465780a6fffb5432b645290448fe592a0f0c` |
| Fator3 MCP Pipedrive | 0.8.0 | `89e41f2f7a2124eb1a5961fe06d6aff60fd168b8d6dd2ea1b21a272772ff7f30` |

O Core, seu fonte e relatório vieram com o pedido. Os outros instaladores correspondem às versões identificadas no Site-Teste. A bancada ativou os cinco acompanhantes e conferiu suas habilidades. Entre os 167 contratos próprios comparados com a 0.41.0, somente `backups/prune` mudou de schema. A seleção usa o índice privado e o histórico de operações do próprio MCP. A avaliação dos produtores, das credenciais e dos contratos de registro não identificou alteração a encaminhar a outro pacote. Só o MCP precisou de troca.

## 3. Mudanças e evidência

**Pedidos MCP 78 — implementado, validado-localmente e validado-wordpress.** A 0.41.0 interrompia o inventário antes de consultar as cópias e devolvia seleção vazia, sem cursor ou instante de corte. No Site-Teste, a reprodução da base registrou 400 itens examinados nesse estado. Além disso, o histórico de instalação guarda o arquivo principal do plugin, enquanto o operador forneceu o slug da pasta.

- Cada prévia de pacote fixa `age_cutoff` na primeira chamada. O cursor assinado recupera a posição e os critérios da prévia da mesma conexão e site. O inventário é independente das listagens concorrentes. A página parcial recebe `selection_status=inventory_incomplete`, `next_cursor` preenchido e nenhum hash aplicável. Após terminar a varredura, o cursor também permite percorrer mais de 200 candidatos.
- O filtro aceita a pasta do plugin ou o caminho completo do arquivo principal. Conserva duas vias de elegibilidade: troca posterior concluída do mesmo plugin ou criação anterior ao limite de idade. Exclusões e referências ativas são respeitadas. A confirmação relê os componentes e as referências antes da remoção.
- Em **Ferramentas → Fator3 MCP → Arquivos e banco**, o formulário SQL identifica sua própria política de retenção. A seção **Pré-imagens de plugins** explica a simulação e abre o guia de leitura dos resultados. O manual e o schema instalado descrevem o novo estado, prazo e cursor.

| Simulação no Site-Teste | Examinados ao fim de cada página | Resultado final |
|---|---|---|
| Site Core, dois dias | 200 → 400 → 447 | Três pré-imagens e 54.354.921 bytes. Versões 1.73.0 → 1.74.0, 1.74.0 → 1.75.0 e 1.75.0 → 1.75.1. As duas últimas ainda tinham menos de dois dias e já haviam sido substituídas. |
| F3 News PublishPress, dois dias | 200 → 400 → 447 | Uma pré-imagem de 45.569 bytes. |
| Mesmo plugin, 3.650 dias | 200 → 400 → 447 | Zero selecionadas. Alterar somente o prazo demonstrou a seleção por idade. |

As três simulações terminaram com inventário completo, zero bloqueios e zero remoções. O corte foi idêntico em todas as páginas de cada consulta. Os IDs de requisição e as contagens por página estão em `evidencias/0420/site-retention.json`.

## 4. Instalação e prova da troca

O instalador fechado foi transferido em quatro partes ao Site-Teste. O servidor confirmou tamanho e SHA-256. A chamada `plugins/upload-base64` usou o caminho temporário, `expected_slug=wp-mcp-fator3`, o SHA-256 da seção 8, sobrescrita e ativação. A operação `a0d872e40327624bf06e9db52f76f761` confirmou a troca 0.41.0 → 0.42.0. A pré-imagem da instalação tem ID `b5f5973c432ce5d4d884f9fb`. As sondas da página inicial e de `/wp-json/` receberam HTTP 200 antes e depois. Uma nova chamada a `system/health` confirmou `healthy=true` e versão 0.42.0. O ZIP de transferência foi removido e uma leitura posterior confirmou sua ausência.

| Prova automatizada | Resultado |
|---|---|
| Base e retenção | 3 verificações da base, 12 na instalação limpa e 14 na migração. Incluem 202 candidatos em dois lotes, cursor adulterado, mudança de critérios, referência criada depois da prévia, repetição da confirmação, seleção por slug e por arquivo principal e aplicação de prévia da base. As remoções desta prova ocorreram em bancos descartáveis. |
| Integração, ajuda e painel | 45 verificações na instalação limpa e 54 na integrada. Leitura integral dos 41 documentos instalados em ambas, com tamanho e SHA-256. Inclusão das seções e do link de ajuda conferida no HTML produzido pelo WordPress. |
| Navegador | Chromium 156.0.8078.79, sessão administrativa no WordPress de bancada. Em 1.365 e 390 px de largura, o link coube na tela e abriu o documento do pedido 78. |
| Empacotamento | Inventário de 476 arquivos igual ao instalador. Sintaxe de 461 arquivos PHP e do JavaScript próprio verificada. Os textos dos 41 guias correspondem aos documentos canônicos. O build repetido reproduziu o mesmo ZIP. |
| Evidência no Site-Teste | Índice dos 41 documentos conferido por hash. Leitura completa pelo MCP das notas da versão e dos documentos de retenção, administração, operação e atualização. Quatro arquivos instalados, incluindo a implementação de retenção e a tela alterada, conferidos por SHA-256. |

O fonte reúne as provas em `evidencias/0420/`, a matriz em `docs/RELEASE-SPEC.json` e os passos de reprodução em `tools/release0420/README.md`.

## 5. Banco, migração e correção por nova versão

O schema de dados continua na revisão 2. A prévia guarda o avanço do inventário na tabela de estado já usada pelos planos de retenção. O cursor é vinculado à conexão, ao site, à prévia e a seus critérios, e expira em uma hora. Uma prévia parcial não autoriza a confirmação. Cada confirmação válida limita a remoção aos componentes congelados do lote. Novos arquivos concorrentes podem exigir nova varredura.

Na migração, a credencial de teste continuou autenticando, o perfil de manutenção e o limite configurado foram preservados e a confirmação por ID preparada na 0.41.0 ainda funcionou na 0.42.0. A instalação preserva os backups existentes. Para recuperar o estado de uma operação de pacote, consulte seu recibo e a pré-imagem correspondente. Correções após a instalação exigem nova versão. A entrega não requer migração reversa.

## 6. Pendências e limites da validação

O pedido 78 cumpriu seu critério de aceite no Site-Teste. O caso originalmente relatado em ctooffice tem inventário próprio. A atualização e a repetição da simulação nesse site e nos demais destinos cabem à equipe de frota. Deve conferir o hash do instalador publicado antes de cada troca. Nenhuma ação deste teste aplicou a política de exclusão no Site-Teste. As contas externas dos acompanhantes ficaram fora do escopo da retenção.

A análise da Ajuda identificou um atalho genérico herdado, **Notas desta versão**, que aponta para a 0.40.0. A seção **Pré-imagens de plugins** e o índice de documentos abrem a 0.42.0. A correção do atalho genérico cabe ao MCP em versão posterior. A validação da série PHP 8.3 cobriu 8.3.6 e 8.3.36.

## 7. Credenciais e configuração do dono

A rodada utilizou a conexão administrativa MCP existente. Para acesso por um novo cliente, um administrador configura a identidade em **Ferramentas → Fator3 MCP → Clientes conectados**, com perfil e capacidades compatíveis com arquivos e manutenção. A simulação exige acesso ao canal. O operador informa `policy`, `plugin` e `older_than_days`, confere os itens e usa o hash do lote somente quando decidir aplicar. O fluxo dispensa credenciais de fornecedores. As evidências guardam contagens, versões, hashes públicos e referências de requisição.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-fator3-0.42.0-instalador.zip](./wp-mcp-fator3-0.42.0-instalador.zip) | 939742 | `d423deb27cc8fe2daaf65a3bf34f42505afdc990f8eac216d383d32a0f1244e0` |
| Fonte | [wp-mcp-fator3-0.42.0-fonte.zip](./wp-mcp-fator3-0.42.0-fonte.zip) | 4401612 | `a783a342f9b2cc36c02a36d6ffead3b735b678ebe1ae011934511baaf1a26513` |

Relatório externo canônico. A cópia incluída no fonte antecede o fechamento do ZIP e identifica este relatório. Checklist de encerramento da seção 14 conferido.
