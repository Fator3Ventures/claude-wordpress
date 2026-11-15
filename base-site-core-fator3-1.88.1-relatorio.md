# Entrega — Fator3 Site Core 1.88.1

Revisão 1 · 2026-11-15T11:22:00-03:00 · Retomada da implementação e homologação do pedido 413  
Slug `base-site-core-fator3` · Build 1.88.1 · **Situação: com-pendencias**, restrita à entrega em um canal dedicado de testes do Slack. Implementação concluída e instalada no Site-Teste.

## 1. De onde esta versão entra

Instalação limpa ou atualização direta da versão vigente **1.87.3 → 1.88.1**. O fonte e o instalador da 1.87.3 vieram da rodada anterior, com SHA-256 `584c297fc8ca3f63fc4549455d236dbdc58fb115aadc4b76fa9038e417e500d0` e `d8f8c05aa3220e5dea01723211718932ca54b13e644d70cdb95dc51ccc760fed`, respectivamente.

A retomada recuperou o fonte parcial, o catálogo de preços, o plano, as provas e o instalador da **1.88.0**, já instalado no laboratório. Um teste com o exportador de sessões revelou a perda da rede efetiva no CSV. A correção recebeu o patch 1.88.1. A única versão desta rodada destinada à instalação é a 1.88.1.

Requisitos de operação em site único: WordPress 7.1.4 ou superior e PHP 8.3 ou superior, em 64 bits. O laboratório executou WordPress 7.1.4 com PHP 8.3.6 e 8.4.24. As normas centrais lidas foram `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambas na revisão 5 de 02/11/2026. A regra comum, o padrão do Core e a instrução posterior do dono sobre os preços integram a base da entrega.

## 2. Convivência e encaminhamentos

| Contrato ou pacote | Resultado |
|---|---|
| Contrato administrativo e perfil | 8.41.0 · `piso-padrao-3.6` · 103 opções operáveis |
| Operações `f3base/*` | 197 no WordPress, uma a mais que na 1.87.3. Entrou `f3base/aparelhos-sem-nome-ler`. Nenhuma remoção. |
| Acompanhantes vigentes | MCP 0.46.0, Google 0.36.0, Meta 0.27.0, LinkedIn 0.24.0 e Pipedrive 0.11.1. Os cinco ficaram ativos na atualização local e no Site-Teste. |
| Pedido MCP Pipedrive 13 | O impacto recebido do mantenedor declara atendido o contrato `pipedrive-api-client/1.0.0`. O Core preserva a interface. A prova comercial descrita pelo mantenedor está identificada no documento recebido em `reference/413/`. |

Somente o Core precisa ser trocado. O catálogo funciona com o Core isolado. A leitura remota usa o MCP. A mudança é aditiva para os leitores do Core e os campos técnicos continuam disponíveis no perfil. A revisão avaliou os cinco acompanhantes e o uso da documentação pelo Implantador. O pedido 413 dispensa desenvolvimento coordenado nesses pacotes. Identidades e hashes dos acompanhantes estão em `evidence/1880/acompanhantes.json`.

## 3. Mudanças e evidência

| Pedido | Mudança | Resultado observado |
|---|---|---|
| Pedidos core 413(a) | Formatação específica para o Slack na mensagem principal e no acontecimento da thread. | Texto e blocos ocultaram código do modelo, versão principal do sistema, memória, núcleos e rede efetiva nos cinco casos. Tela, DPR e faixa aparecem quando disponíveis e o consentimento permite. O perfil técnico continua disponível aos outros consumidores. |
| Pedidos core 413(b) | Identificação local por código, ano, preço e marcação de família premium. Leitor administrativo dos códigos desconhecidos. | `25078PC3EG` → **POCO C85 · 2025 · ~R$ 1.164**. `SM-A075M` → **Galaxy A07 · 2025 · ~R$ 718**. `SM-S928B` → **Galaxy S24 Ultra · 2024 · ~R$ 5.399 · linha premium**. Código inventado → **nome comercial não identificado**. A leitura paginada recuperou esse código no laboratório e recusou usuário sem autorização. |
| Pedidos core 413(c–d) | Catálogo do pacote e correções locais por código ou nome comercial. Raiz Samsung aceita quando a ficha é inequívoca. | POCO C85 recebe faixa entrada com catálogo do site vazio. `SM-A175M` resolve para **Galaxy A17 · 2025 · ~R$ 920**. A regra local por nome alterou a faixa e a regra por código alterou a ficha. |
| Pedido posterior sobre preços | Preservação dos valores existentes e conclusão da pesquisa ou estimativa para cada lacuna. Exclusão da coluna `observacao`. | **1.156 códigos únicos**, 985 valores preservados e 171 preenchidos. Todos os valores positivos. O resolvedor instalado devolveu, para cada código, os mesmos seis campos do CSV. |
| Correção encontrada na retomada | A classificação de rede do servidor sobrescrevia o sinal do navegador na linha de sessão. O Core preserva `rede_efetiva` e o objeto `rede` com suas finalidades próprias. | O CSV real de uma sessão filtrada por 8 GB e linha premium trouxe `4g`, a classificação do servidor, 8 núcleos, sistema 15, tela 360×800 @2x, ano 2024 e preço 5399.00. |

A lista de **15/11/2026** contém 685 códigos Samsung, 275 Xiaomi, 133 Motorola e 63 realme. O preço é uma estimativa em reais na data da pesquisa. As 171 lacunas correspondiam a 61 grafias comerciais. Em 35 havia referência publicada, 21 usaram comparação com outros aparelhos, 3 usaram preços anunciados de itens sem estoque e 2 compartilharam o valor do mesmo aparelho sob outro nome. O campo numérico conserva os centavos e a mensagem do Slack arredonda para reais inteiros. Fontes e justificativas estão em `reference/413/referencias-precos.csv`. O CSV final está em `reference/413/catalogo-aparelhos.csv`, SHA-256 `74a3c18a6b83209433e50fef76fc7abb5eb7f6a29c4a5a50f550ee61979d9663`.

A captura e a composição do aviso consultam o índice embarcado. A procedência da referência externa de modelos e sua licença Apache-2.0 acompanham o fonte e a atribuição instalada. O catálogo cobre os códigos fornecidos. Um código novo ou ambíguo permanece identificável para revisão administrativa.

## 4. Instalação e prova da troca

O instalador tem raiz única `base-site-core-fator3/` e basename `base-site-core-fator3/base-site-core-fator3.php`. No Site-Teste, o arquivo servido por HTTP foi comparado byte a byte com o ZIP final. A operação `plugins/upload` recebeu `expected_slug=base-site-core-fator3`, o SHA-256 da seção 8, ativação e substituição da base. O recibo da troca foi `13a10eff13072520e93aec59ead7b279`. O arquivo de transporte temporário foi removido após a conferência.

Para a distribuição pela frota, confira o SHA-256 servido no endereço de publicação contra a seção 8 antes de instalar. O endereço a seguir é o destino previsto para a publicação pela frota. [URL raw prevista para o instalador](https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/base-site-core-fator3-1.88.1-instalador.zip)

| Ambiente | Prova | Resultado |
|---|---|---|
| ZIP final | Árvore, CRC, manifesto, reprodução e lint em dois PHPs | 997 arquivos verificados. Os 608 PHP passaram em 8.3.6 e 8.4.24. A reconstrução produziu os mesmos bytes do instalador. |
| WordPress 7.1.4 limpo | Apenas Core ativo, PHP 8.4.24 | 215 verificações do pedido 413 e 263 verificações de regressão aprovadas. Exportador e leitor do CSV exercitados separadamente. |
| WordPress 7.1.4 no PHP 8.3.6 | Fluxo funcional do pedido 413 na instalação limpa | 215 verificações aprovadas. |
| Atualização local direta | Base 1.87.3, 55 contatos sintéticos, cinco acompanhantes ativos | 215 verificações do pedido e exportação real aprovadas. As 263 verificações de regressão também passaram via usuário de laboratório com perfil explícito de leitura do MCP. Após revogação, o MCP recusou a leitura com `connection_context_required`. |
| Painel em Chromium | 80 telas ou estados a 360, 768 e 1.440 px de largura | **240 capturas** com HTTP 200, selo 1.88.1 e largura correta. **13 interações** verificaram paginação, filtros, detalhe legado, CSV, abas e navegação. |
| Site-Teste compartilhado | Home e REST antes e depois, pacote ativo, prontidão do Core e duração | Ambas as sondas retornaram HTTP 200. `atualizacao.versao_alvo=1.88.1`, `estado=concluida`, `falhas=0`, `confirmada_no_executor_em=1794751593`. As 20 etapas terminaram em **7 s**. Saúde final com zero módulos degradados e zero tarefas cuja última execução falhou. |
| Leitura no Site-Teste via MCP | Catálogo, códigos sem nome, relatórios editorial/integrado e documentação paginada | Catálogo com 1.156 códigos. Os dois relatórios aceitaram os filtros combinados em um caminho de controle vazio. A nova operação respondeu e encontrou zero códigos retidos naquele ambiente. |

Após a ativação, consulte `f3base/como-usar` e `f3base/saude-ler` com `compacto=true`. O índice local é `docs/DOCUMENTACAO.md`. A leitura por `f3base/documentacao-ler` remontou o índice em quatro páginas, o guia `docs/AGENTES-1.88.1.md` em três e as notas `docs/RELEASE-1.88.1.md` em três. Os três textos coincidiram integralmente com o ZIP. Um documento fora do índice foi recusado. As provas, parâmetros e SHA-256 documentais estão em `evidence/1880/site-teste-final.json`.

## 5. Banco, migração e correção por nova versão

O pedido reutiliza a opção `f3base_medicao_editorial.catalogo_aparelhos` e o perfil de aparelho retido. Criou zero tabelas e zero opções de configuração. A ficha comercial acompanha observações novas no perfil existente. Para perfis antigos com o código ainda retido, o enriquecimento ocorre na leitura. Dados já eliminados por retenção continuam ausentes.

Na atualização local, os 55 contatos conservaram os identificadores e os hashes dos respectivos payloads. A impressão agregada antes e depois foi `dfd9d0065fd04b31f9263d96af1b3c123095f73e14b383562829e664822e1fb2`. No Site-Teste, o instalador registrou backup de arquivos do plugin. Esse recibo não comprova backup do banco. O executor existente registra as etapas de avanço e retoma pendências. Qualquer correção posterior segue em nova versão. Em caso de interrupção, leia prontidão e filas antes de repetir efeitos externos.

## 6. O que permanece pendente

**Entrega real da mensagem e da thread a um canal dedicado de testes do Slack.** A composição foi exercitada nos formatos compacto, completo e thread, incluindo texto alternativo, blocos e consentimento. O Site-Teste usa aplicativo Slack, política de testes `marcar` e o canal operacional compartilhado `#growth-wordpress`. A rodada teve zero postagens nesse canal. Para concluir o aceite externo, o responsável pela homologação precisa indicar um canal dedicado e autorizar seu uso pelo aplicativo. O critério é receber o aviso dos modelos conhecidos e do desconhecido e conferir a principal e as respostas na thread.

A instalação desta rodada abrangeu o laboratório e o Site-Teste. Publicação do pacote e instalação nos sites de produção pertencem à frota. Não houve operação comercial em CRM, e-mail ou mídia nem medição de latência de produção. A pesquisa de preços usa a data do catálogo e inclui estimativas, identificadas no fonte.

## 7. Credenciais e configuração do dono

O catálogo funciona sem chave, conta de fornecedor ou ajuste inicial. Para sobrescrever uma faixa, abra **Site Core → Configuração → Conteúdo, audiência e IA → Catálogo local de aparelhos**. Por exemplo, `Galaxy A07 4G=entrada`. Para acrescentar uma ficha, use `CODIGO-EXEMPLO=Marca|Modelo exemplo|2025|1199.90|intermediário|não`. Na configuração via MCP, simule, confira a revisão e confirme. A nova leitura administrativa exige `manage_options` no servidor.

O transporte do Slack continua usando a configuração de avisos e as credenciais já cadastradas. A release não exige novo segredo. A seleção de um canal dedicado para o aceite externo permanece com o dono do destino.

## 8. Identidade dos arquivos

| Artefato | Nome final e link | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador WordPress | [base-site-core-fator3-1.88.1-instalador.zip](base-site-core-fator3-1.88.1-instalador.zip) | 4540822 | `102ccb77b229870bb03310a559c147ec8d2a6d9bf1e670aeffb5661c641801cc` |
| Fonte completo | [base-site-core-fator3-1.88.1-fonte.zip](base-site-core-fator3-1.88.1-fonte.zip) | 96591016 | `4c17935c0468ce7346673e95c1a7a93bebd0e52fe2a467ae0d16a49c85c8eb87` |

Relatório externo canônico. A cópia incluída no fonte é anterior ao fechamento do ZIP e remete a esta tabela para sua identidade definitiva.
