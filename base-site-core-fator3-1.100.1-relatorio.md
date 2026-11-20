# Entrega — Fator3 Site Core 1.100.1

Revisão 1 · 20/11/2026 · Implementação e correção da interface administrativa · **Apta no escopo testado.** Os aceites de campo anteriores continuam com a frota.

## 1. De onde esta versão entra

O instalador atende a uma instalação nova e às atualizações diretas da 1.99.0 e da 1.100.0. A rodada retomada implementou o guia visual no Core 1.100.0, partindo do fonte oficial da 1.99.0. O Site-Teste já executava a 1.100.0. Na conferência final, a matriz registrou uma falha na área Informações técnicas. Esta entrega aplica a correção no patch 1.100.1. O instalador da base 1.99.0 tem SHA-256 `3509e2736dfdedd98c2fa142d99028eb629f112ba1c863138850c3f3ee5e7155`. O instalador recuperado da 1.100.0 tem SHA-256 `d913defb06b8160453a25fefff3e938a1d5785fd51da74c4de6da9cb3f0ffdae`.

O Core requer WordPress 7.1.4+ em instalação única e PHP 8.3+ de 64 bits. A bancada usou WordPress 7.1.4, PHP 8.4.27 e MariaDB 11.8.6. O Site-Teste executava WordPress 7.1.5 e PHP 8.3.37. O par de versões mínimas exatas não foi exercitado em conjunto. Foram lidos integralmente `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos na revisão 5 de 02/11/2026. As referências de interface estão em `reference/2000/`.

## 2. Convivência e encaminhamentos

O contrato do Core segue na versão 8.47.0, perfil `piso-padrao-3.6`, com 103 opções operáveis e 199 abilities. O conjunto de homologação reúne MCP 0.54.0, Google 0.42.0, Meta 0.31.0, LinkedIn 0.26.0 e Pipedrive 0.12.0. MCP e Google foram testados funcionalmente nas fronteiras abaixo. Para os demais, a prova desta rodada é de convivência com os plugins ativos.

| Contrato | Resultado |
|---|---|
| Pedidos Core 439 / MCP 91 | O MCP 0.54.0 incorporou a projeção administrativa de `token_vencendo`. Com o Core 1.100.1, passaram as 29 verificações da projeção e as 19 do transporte HTTP local, inclusive limites de 0 a 10.080 minutos e proteção dos campos vizinhos. A opção do Site-Teste devolveu 30 minutos antes e depois da troca. |
| Pedido MCP Google 59 | Na bancada com o Google 0.42.0 e o Core 1.100.1, uma fila sintética de 204 avisos com 200 reservas chegou a 204 recibos após a liberação. O cursor retomou em outro processo. O teste registrou zero submissões de e-mail. Os ensaios anteriores de encerramento administrativo estão em `evidence/2000/contratos/`. |

As mudanças de tela não exigem alteração nos acompanhantes. As correções oficiais anteriores do MCP e do Google já estão nas versões testadas. Os retornos recebidos estão em `reference/2000/` e a repetição dos testes no patch está em `evidence/2001/contratos/`. No Site-Teste, a troca foi feita somente no Core.

## 3. Mudanças e evidência

Referência funcional da rodada: **Pedidos Core 404**, padrão visual comum e 20 ajustes da aba do Site Core de 20/11/2026. A aba de ajustes não atribuiu outro número ao pedido.

| Ajustes | Resultado no painel |
|---|---|
| 1–3. Folhas e largura | O carregamento centralizado aplica a folha comum e a folha de domínio nas páginas do Core, inclusive na entrada direta de Operação. A largura máxima é 1.320 px. O frontend e o painel nativo do WordPress passam sem essas duas folhas. |
| 4–8. Cabeçalho e navegação | O nome, a descrição, o selo de versão e o divisor de avisos seguem uma estrutura única. O administrador navega entre Configurações, Contatos, Medição, Operação e Informações técnicas. O Core filtra grupos e subabas pela capacidade da conta. |
| 9–13. Organização e edição | Conexões e entregas apresenta cartões de acesso direto. As seções técnicas e avançadas são recolhíveis. Rótulos e ajuda acompanham os campos. A barra de gravação acompanha o formulário. Estados informam o significado por texto e cor. |
| 14–18. Listas, tabelas e endereços | Formulários e conteúdo privado têm busca e paginação. As tabelas largas rolam no próprio bloco. Os filtros de Medição usam a grade comum. Os endereços antigos de Operação e Relatórios abrem a área correspondente. |
| 19–20. Tela estreita | As quebras de texto técnico ficam na folha de domínio. Nos tamanhos móveis da prova, os controles visíveis testados têm pelo menos 40 px e a navegação tem pelo menos 44 px. A folha comum 1.0.0 manteve seu SHA-256 `15ef0d932b1be12a541b8408b061ee276a4db9d6650476f92b5e2f41eefc0c2b`. |
| Correção 1.100.1 | A agenda e os módulos de Informações técnicas aplicavam o modificador não previsto `is-neutral`. Os dois emissores passam a usar a classe base `f3-pill` para o estado neutro. A conferência 6 da tela técnica passou com o mesmo verificador que detectou a divergência. O inventário comparado dos instaladores está em `evidence/2001/diferenca-instaladores.json`. |

## 4. Instalação e prova da troca

**Site-Teste.** O MCP atualizou a 1.100.0 para a 1.100.1 em `fator3-teste-mcp-1.dreamhosters.com`. O SHA-256 conferiu no envio em 22 partes, na releitura do ZIP e no recibo de instalação por `plugins/upload-base64`, com slug e hash esperados. Em seguida, as duas classes PHP corrigidas, o arquivo principal e a folha comum foram conferidos individualmente contra o ZIP. A pré-imagem da instalação foi registrada e a cópia temporária do ZIP foi removida. O Core e os cinco acompanhantes ficaram ativos.

O executor confirmou **20 etapas, zero falhas e estado `concluida`** em 20/11/2026 às 15:48:23 (Brasília). As sondas da página inicial e de `/wp-json/` devolveram HTTP 200 antes e depois. A revisão da política de avisos foi preservada. A leitura final registrou zero tarefas com última execução falha e um módulo degradado, `robots-txt`, que aguardava verificação pública pelo cron. Esse módulo já constava como degradado na 1.100.0 antes da troca.

O índice de `f3base/documentacao-ler` listou 272 documentos. As 31 linhas de `docs/RELEASE-1.100.1.md` foram lidas em três páginas e comparadas com o ZIP. SHA-256 `53f606ec40805b3194e4c61a0c3c83805234c764e11c04c3ebf5f19c3ff9ab10`. Um ID ausente foi recusado com `documento_nao_catalogado`. As evidências sanitizadas estão em `evidence/2001/site-teste.json`.

| Cenário | Evidência |
|---|---|
| Instalação e atualização locais | Instalação limpa e duas atualizações diretas concluíram 20 etapas cada, com zero falhas. As duas atualizações preservaram a carência de 77 minutos gravada para o teste. Os 1.292 arquivos de cada instalação foram comparados com o ZIP. |
| Interface em Chromium | **288 de 288** verificações, com 12 critérios em 24 rotas. O [caderno visual](base-site-core-fator3-1.100.1-prova-visual.html) traz 72 capturas iniciais a 360, 768 e 1.440 px, 24 capturas adicionais de conteúdo no telefone e duas do esquema Moderno. O navegador usou dados sintéticos e um segundo plugin ativo com aviso administrativo. A matriz inclui medições com JavaScript desligado e seções expandidas. |
| Contatos | 18 cenários no navegador. A busca localizou registros além da primeira página de 25 formulários e 28 materiais. Edição, simulação, salvamento e cancelamento da remoção preservaram o item selecionado. |
| Medição e Operação | O roteiro de Medição percorreu 45 rotas ou variações e alternou análises com e sem JavaScript. A lista de 26 anotações devolveu páginas de 20 e 6. Cada uma das quatro listas de Operação exibiu 24 correspondências em páginas de 20 e 4, sem repetição. |
| Permissões e carga | A instalação limpa recusou leitura anônima e permitiu a leitura pelo administrador local. Com o MCP ativo, o administrador local fora do perfil autorizado recebeu `profile_denied` nas operações de domínio testadas. O teste de navegação verificou os grupos e destinos visíveis por capacidade. |
| Integridade | Lint de 612 arquivos PHP. Inventário, CRC e paridade entre a árvore de runtime e o instalador conferidos. Os diretórios `evidence/2000/` e `evidence/2001/` separam as evidências da 1.100.0 das provas do patch. |

A distribuição à frota usa o ZIP desta entrega com `expected_slug=base-site-core-fator3` e o SHA-256 da seção 8, após conferência do arquivo publicado. A frota pode verificar a troca com `f3base/como-usar` em modo compacto e as etapas com `f3base/saude-ler`. A versão-alvo esperada é 1.100.1, com estado `concluida`, zero falhas e confirmação do executor.

## 5. Banco, migração e correção por nova versão

A revisão visual lê as tabelas, opções e permissões existentes. O patch corrigiu a marcação HTML dos selos em duas classes administrativas. O ciclo normal de instalação registra a versão, o progresso e a confirmação. As atualizações locais preservaram o valor personalizado da política de avisos. No Site-Teste foi comparada a revisão da configuração antes e depois da troca. Correções posteriores usam nova versão. O operador conserva os backups de dados e os recibos de entregas externas para recuperação e reconciliação.

## 6. O que permanece pendente

- **Frota, Core 439.** Após a implantação em cada site, acompanhar por sete dias se os episódios transitórios respeitam a carência e se os recibos de abertura e recuperação correspondem ao histórico.
- **Frota, Google 59.** Conferir as ocorrências históricas em Pauta e Prática, Desenvolvimento de Softwares e Taberium após a implantação do conjunto vigente. Os recibos sintéticos cobrem o comportamento da fila.
- **Site Geral | Todos.** A folha comum 1.0.0 define 36 px para alguns campos móveis. O Core já aplica o token de toque de 40 px nesses controles. A eventual revisão da folha compartilhada cabe ao seu mantenedor.
- **Limites da homologação.** As capturas retratam WordPress local. Entrega real de mensagens, autorização de contas externas e operações comerciais de fornecedores ficaram fora do ensaio. A implantação de produção fica com a frota.

## 7. Credenciais e configuração do dono

O patch usa as credenciais já configuradas. A política permanece em **Configurações → Conexões e entregas → Avisos técnicos**. A confirmação do prazo por código está disponível no MCP em `f3base/config-core-ler` para a opção `f3base_avisos_tecnicos` e o caminho `/carencia_por_codigo_minutos/token_vencendo`.

## 8. Identidade dos arquivos

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| [base-site-core-fator3-1.100.1-instalador.zip](base-site-core-fator3-1.100.1-instalador.zip) | 5727867 | `15b5f18858d5e56e5cdbc96bdef83fcc60629279cc6c8e7e17d14571a9fe2f11` |
| [base-site-core-fator3-1.100.1-fonte.zip](base-site-core-fator3-1.100.1-fonte.zip) | 16703434 | `c4741babb4624daa7088785e74a0f896471fa98fca3a14cae5f62df14443210d` |

O instalador contém a raiz estável `base-site-core-fator3/`. O fonte traz código, build, testes, capturas, medições e a cópia do relatório anterior ao fechamento do arquivo. O relatório externo registra os tamanhos e hashes finais.
