# Entrega — Fator3 Site Core 1.89.1

Revisão 1 · 15/11/2026 · Patch do pedido 415 · `base-site-core-fator3`

**Instalado e validado no Site-Teste.** Na atualização em laboratório, a consulta paginada passou de dois códigos sem nome a zero. O aceite em produção depende da instalação da 1.89.1 no CTO Office.

## 1. De onde esta versão entra

Base de migração **1.89.0**, instalador SHA-256 `f48d257ab67f04a95dc50af8a3ea31241560380d8e1f740ff4574de84b6ef177`. A base do fonte tinha 116.810.124 bytes e SHA-256 `522a6546b4b629478b3e2043168dd6bfe7bf1a4d99a1e5ec06a83d992beb7384`. O número de patch **1.89.1** e a validação restrita ao ajuste foram solicitados pelo dono. Não há versão intermediária.

Requisitos do pacote: WordPress 7.1.4 ou superior, instalação única e PHP 8.3 ou superior de 64 bits. A atualização local foi exercitada em WordPress 7.1.4 e PHP 8.3.6. Documentos centrais conferidos nas fontes do projeto: `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, revisão 5 de 02/11/2026.

## 2. Convivência e encaminhamentos

O contrato administrativo continua em **8.41.0**, com perfil `piso-padrao-3.6`, 103 opções operáveis identificadas na base e 197 operações publicadas no catálogo. Nenhuma operação entrou ou saiu. No Site-Teste permaneceram ativos o MCP 0.46.0, Google 0.36.0, LinkedIn 0.24.0, Meta 0.27.0 e Pipedrive 0.11.1. A troca isolada do Core basta. O patch conserva o formato dos dados e a precedência das regras locais. O Implantador continua consumindo o mesmo contrato. A comparação do PHP e dos catálogos dispensou encaminhamento técnico aos acompanhantes.

## 3. Mudanças e evidências

**Pedido 415.** O catálogo passou de **1.346 para 1.348 códigos**. A revisão embarcada é `2026-11-15.3`. Os seis campos das correções são:

| Código observado | Marca | Nome comercial | Ano | Preço estimado em 15/11/2026 | Faixa | Linha premium |
|---|---|---|---:|---:|---|---|
| `infinix x6525b` | Infinix | Infinix SMART 8 Pro | 2024 | R$ 800,00 | entrada | não |
| `m7_wifi` | Multilaser | M7 Wi-Fi | 2021 | R$ 292,89 | entrada | não |

O manual da Infinix liga X6525B ao SMART 8 Pro. A referência brasileira de preço é a oferta de 128 GB e 4 GB de RAM rastreada em 14/11. No tablet, a lista Google Play registra o mesmo identificador para diferentes variantes. O cadastro usa o nome da família e toma o NB355 de 32 GB como referência para ano e preço. As configurações individuais dos visitantes não foram inferidas. A procedência por campo, os critérios e a amostra dos identificadores do Google Play estão em `reference/415/`. As referências dos pedidos 413 e 414 continuam no fonte.

**Redução do pacote de desenvolvimento.** Na 1.89.0, as evidências acumuladas ocupavam 88.378.857 bytes comprimidos e o diretório histórico ocupava 20.759.192. O novo fonte entrega a árvore integral do runtime, assets, documentação editável, esquemas, pesquisas usadas no catálogo, geradores, scripts de regressão, fixtures e provas da rodada. Saíram do novo ZIP capturas e evidências de rodadas encerradas, cópias de runtimes e arquivos históricos de planejamento. Esses materiais continuam disponíveis na entrega original. O empacotamento passa a exigir fonte menor que **100.000.000 bytes** antes de substituir o ZIP de saída.

Resultado final: **116.810.124 → 5.522.183 bytes**, redução de **95,27%**. O limite considerou MB decimal.

## 4. Instalação e prova da troca

| Prova | Resultado |
|---|---|
| Delta em relação à base certificada | Os 1.346 códigos, 452 nomes e 152 raízes do índice anterior continuam apontando para fichas idênticas. Entraram exatamente os dois códigos do pedido. A comparação binária de 608 arquivos PHP admitiu somente a versão do cabeçalho, o comentário de migração e a revisão do catálogo. |
| API em WordPress local | Na 1.89.0, dois perfis sintéticos produziram duas pendências. Após a troca, a mesma consulta realizou duas chamadas de uma posição, examinou os mesmos códigos e terminou com `itens=[]` e `proximo_apos=null`. Os seis campos de cada nova ficha foram conferidos. |
| Catálogo instalado | O resolvedor PHP do Core devolveu os seis campos esperados para todos os 1.348 códigos do CSV. Todos os preços são positivos. |
| Empacotamento | Instalador com raiz `base-site-core-fator3/` e basename publicado. Os 1.001 arquivos coincidem com o runtime do fonte. Mesma árvore usada no laboratório e no Site-Teste. |
| Site-Teste | O ZIP temporário servido no domínio de teste foi instalado por `plugins/upload` com `expected_sha256`, `expected_slug`, substituição e ativação. Recibo `04dba51ce644c7e3284cf03c426cf5ae`. As 20 etapas terminaram em 6 segundos: `versao_alvo=1.89.1`, `estado=concluida`, `falhas=0`, `confirmada_no_executor_em=1794789193`. Home e REST passaram antes e depois. |
| Leitura remota e encerramento | `f3base/como-usar` confirmou os 1.348 códigos e a revisão. As notas instaladas foram lidas por `f3base/documentacao-ler` em duas páginas com texto igual ao do ZIP. O arquivo temporário foi removido. O evento já agendado de verificação de robots.txt foi executado no Site-Teste. A saúde final registrou zero módulos degradados e zero tarefas com falha na última execução. |

O diretório `evidence/1891/` contém os resultados sanitizados. O Site-Teste não tinha perfis retidos para reproduzir o par de códigos. A comparação funcional foi feita pelo mesmo endpoint no WordPress local com os dois perfis semeados na base.

## 5. Banco, migração e correção por nova versão

A atualização lê as tabelas e regras locais existentes. Nenhuma tabela, coluna, opção ou credencial foi acrescentada. Os hashes dos dois perfis brutos coincidiram antes e depois. O catálogo identifica os registros retidos na leitura. A atualização no Site-Teste gerou a pré-imagem dos arquivos do plugin. Uma correção posterior segue em nova versão.

## 6. Validação pendente

Na consulta real ao CTO Office, a listagem da 1.89.0 retornou `infinix x6525b` e `m7_wifi`, um perfil de cada, entre 129 códigos; a paginação chegou ao fim. A homologação local reproduziu ambos. A frota pode instalar o ZIP da seção 8 no CTO Office e repetir `f3base/aparelhos-sem-nome-ler` com `limite=200`, percorrendo `proximo_apos` até nulo. O aceite solicitado é a lista agregada vazia. A observação de produção anterior à troca está em `ctooffice-antes.json`.

Conforme a dispensa do dono, esta rodada não repetiu a suíte geral, os testes de interface, integrações comerciais nem uma instalação limpa do patch como cenário independente. A prova local foi a atualização da base no mesmo banco. Para distribuição pela frota, conferir o hash dos bytes publicados antes de instalar. [Destino raw previsto](https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/base-site-core-fator3-1.89.1-instalador.zip)

## 7. Credenciais e configuração

Basta atualizar o Core. Os dois modelos entram pelo catálogo embarcado. Nenhum segredo, importação ou alteração de configuração local é necessário.

## 8. Identidade dos arquivos

| Tipo | Nome | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [base-site-core-fator3-1.89.1-instalador.zip](base-site-core-fator3-1.89.1-instalador.zip) | 4549839 | `8182d7dc2c2763bb45854840e6768e1477b4d687bbf217fa2417d0e4c18a0bd2` |
| Fonte | [base-site-core-fator3-1.89.1-fonte.zip](base-site-core-fator3-1.89.1-fonte.zip) | 5522183 | `12315893695bf4cefe1c4aa178f22f216ce009fa3bc32598a4aafd5cbd0cc845` |
| Catálogo | [base-site-core-fator3-1.89.1-catalogo-aparelhos.csv](base-site-core-fator3-1.89.1-catalogo-aparelhos.csv) | 79411 | `439993dd7c7a8d1ad5cdd6a8d924c256e0d8db30f32c8da196173d2b890d6ff2` |

Relatório externo canônico. A cópia interna foi congelada antes do fechamento do ZIP.
