# Entrega — Fator3 MCP 0.46.0

Revisão 1 · 15/11/2026 · Slug `wp-mcp-fator3` · Pedidos MCP 81, 82 e 83 · Estado **com pendência de aceite em produção para o pedido 83**.

**Relatório externo canônico.** O ZIP de fonte contém a cópia anterior ao seu fechamento. A tabela abaixo identifica os bytes finais de ambos os pacotes.

## 1. Base, padrões e conjunto vigente

A 0.46.0 admite instalação limpa e atualização direta da 0.45.0. O instalador-base tem 939.667 bytes e SHA-256 `3659bebf22155807d12f4559cf3d9e7ef7403aec0da45fc661ad90c577c7eab9`. O fonte-base tem 3.320.693 bytes e SHA-256 `df7f460fd1727f2f45046fd60a9e71cabbc3201c32d0702b258f4f3349842059`. O basename é `wp-mcp-fator3/wp-mcp-fator3.php`. O pacote declara PHP 8.3 e WordPress 7.1.4 como mínimos.

Foram lidos integralmente `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos na revisão 5 de 02/11/2026. Também foram usados a Regra comum com o padrão visual, o padrão específico do Fator3 MCP, o arquivo dos Pedidos MCP 81–83 e o fonte, instalador e relatório do Core 1.87.3 fornecidos na rodada. O padrão completo orientou o checklist de encerramento.

| Pacote | Versão de referência conferida na bancada integrada e no Site-Teste |
|---|---:|
| Fator3 Site Core | 1.87.3 |
| Fator3 MCP Google | 0.36.0 |
| Fator3 MCP LinkedIn | 0.24.0 |
| Fator3 MCP Meta | 0.27.0 |
| Fator3 MCP Pipedrive | 0.11.1 |

Os acompanhantes avançaram durante a rodada. As versões da tabela correspondem ao inventário imediatamente anterior à troca do MCP e ao inventário final. Os nomes, tamanhos e hashes das oito entradas estão em `docs/ENTRADAS-TESTE.json`. O catálogo da bancada integrada contém 169 habilidades próprias do canal e seis provedores.

## 2. Mudanças, contratos e uso pelos agentes

| Pedido | Implementação | Aceite observado |
|---|---|---|
| Pedidos MCP 81 | Cabeçalho com descrição e versão, dois níveis de navegação, agrupamento em Operação, Configurar e Suporte, filtros de atividade, pesquisa e paginação de clientes e rolagem própria das tabelas. Os sete endereços antigos redirecionam à seção correspondente. | Chromium autenticado no WordPress atualizado. Foram 21 capturas de sete abas a 360, 768 e 1440 px, 90 asserções aprovadas, incluindo navegação visível, busca de 27 clientes, ida e volta entre páginas e leitura das notas. Capturas em `evidencias/0460/telas/`. |
| Pedidos MCP 82 | As operações longas de banco registram a entrada, executam em PHP CLI e preservam a sessão de banco da operação. A verificação percorre o conteúdo armazenado em blocos para calcular o hash. A chamada pode devolver `retryable` e um `operation_id` com prefixo `sqljob:`. | No Site-Teste, a confirmação real de uma alteração de uma linha respondeu `running`. A consulta de status mostrou `verificar_artefato` e depois `complete`. A auditoria marcou 126,269 s entre o início e a conclusão. A gravação e a restauração foram confirmadas por leitura independente. Zero fatais no log da janela. |
| Pedidos MCP 83 | As continuações são vinculadas ao fatal e retornam em `stack`, com argumentos omitidos. Diretórios aleatórios equivalentes recebem chave normalizada nas mensagens AH01276. | No Site-Teste, as mesmas 172 ocorrências passaram de 172 grupos a um. Na bancada, o reprocessamento de 75 linhas históricas sanitizadas do CTO Office reuniu cinco TypeError em um fatal com a pilha e produziu zero grupos de aviso para as continuações. |

**Contrato para agentes e para a frota.** Em `db/execute`, `db/batch`, `db/search-replace`, `db/export` e `db/restore`, leia a resposta imediata. Se contiver `retryable:true` e `operation_id` iniciado por `sqljob:`, consulte `operations/status` com o mesmo ID. Quando chegar `result`, interprete o êxito ou erro desse resultado. Uma prévia concluída fornece o `confirm_token` para a habilidade de origem. A fase de confirmação pode gerar outro trabalho. Os identificadores da fase e do trabalho têm usos distintos. Um consumidor que presumir conclusão imediata precisa incorporar essa consulta antes de avançar. Em `system/error-log`, leia `stack` no grupo fatal e `count` no grupo de sondas.

As rotas do servidor, o alcance nativo das senhas de aplicação e o comportamento da descoberta sem limite explícito seguem as decisões do dono. A busca em código PHP dos cinco acompanhantes vigentes por chamadas diretas às cinco operações SQL não localizou consumidor a corrigir. O Core 1.87.3 respondeu a `f3base/aplicabilidade-ler` pelo MCP 0.46.0 no Site-Teste. Esta rodada dispensa release coordenada dos acompanhantes. A frota é responsável por distribuir o canal e aplicar o procedimento de consulta nos agentes consumidores.

## 3. Instalação e prova

A troca no Site-Teste usou `plugins/upload`, URL HTTPS temporária dos bytes do ZIP, `expected_slug=wp-mcp-fator3`, o SHA-256 da seção 7, sobrescrita e ativação. O recibo `43d4ad3aad19f3bcf119ee97f69461e3` registra a passagem da 0.45.0 para a 0.46.0 e a aprovação das sondas anterior e posterior. `system/health` em nova chamada confirmou servidor saudável, WordPress 7.1.4 e PHP 8.3.36. Os hashes de Admin.php, HostingErrorLog.php e SqlWork.php lidos da instalação conferiram com o ZIP. A leitura integral de `system/guide` com `document=release-0460` retornou 2.491 bytes e SHA-256 `fd23c683fa65136f59dcd12868e0c38999aafa9621eb95fd9a7e92a5fdbb38a5`, igual ao documento canônico. No painel, o caminho é **Ferramentas → Fator3 MCP → Suporte → Ajuda**.

| Ambiente | Procedimento e resultado |
|---|---|
| WordPress 7.1.4 isolado | Instalação nativa do ZIP em banco novo, sem acompanhantes. Os 477 arquivos coincidiram com o instalador. Os 17 testes de SQL passaram. |
| WordPress 7.1.4 integrado | Instalação da base 0.45.0, configuração de valor próprio, ativação dos cinco acompanhantes e atualização pelo ZIP final. A opção persistiu com o valor anterior. Os 477 arquivos coincidiram com o instalador e passaram os 17 testes de SQL. |
| PHP 8.3.6 e 8.4.24, MariaDB 11.8.6 | Lint nos 470 arquivos PHP do ZIP em cada versão. SQL real no piso e no runtime de bancada, prévia, idempotência, autorização, corrupção detectada, restauração por linha e por tabela. Sete verificações específicas de logs passaram no PHP 8.3.6. A documentação compilada passou por 195 verificações. |
| Transporte MCP HTTP em bancada | Confirmação autenticada retornou em 3,34 s. O trabalho terminou em 125,61 s com latência instrumentada de 125 s, efeito conferido e os dois marcos na auditoria. |
| Site-Teste | O trabalho `sqljob:4a61e716515412cb815b900c43c04f81` registrou `accepted` às 01:57:51 UTC e `complete` às 01:59:57 UTC de 15/11/2026. A consulta ao log entre 01:57:45 e 02:00:05 UTC encontrou zero grupos fatais. A linha do rascunho recebeu a alteração e voltou ao valor original por `db/restore`. O rascunho, o ZIP de transporte e o arquivo temporário de instrumentação foram removidos e suas ausências verificadas. Os backups e recibos produzidos pelos mecanismos nativos continuam sujeitos à retenção do site. |
| CTO Office | A consulta em produção na 0.45.0 confirmou os cinco fatais e quatro grupos de aviso filtrados por `#1` na janela de 13/11 17h a 14/11 11h, UTC−03. Os registros da janela foram lidos sob autorização e sanitizados, preservando data, fluxo e ordem dos quadros. O extrato e a prova da 0.46.0 estão em `evidencias/0460/ctooffice-*`. |

## 4. Banco, continuidade e recuperação

O schema de dados do canal permanece na versão 2. O executor mantém a transação enquanto a requisição HTTP termina. Solicitações e resultados ficam cifrados no armazenamento privado do site, vinculados ao site, conexão e usuário. A conclusão registra a fase e o resultado no audit. A coleta dos recibos do trabalho é agendada para 24 horas. O site precisa de PHP CLI compatível, das extensões utilizadas, dos mesmos salts e de acesso ao armazenamento privado. Se o processo não iniciar, verifique o cron CLI. Se o executor for interrompido após iniciar, confira o recibo da fase e a pré-imagem antes de repetir uma mutação. A restauração por linha utiliza a pré-imagem e valida a pós-imagem prevista.

O painel conserva as configurações existentes. Correções posteriores à instalação exigem uma nova versão a partir do estado alcançado. O responsável pela frota deve verificar o SHA-256 e o slug, instalar um site por vez e conferir versão, saúde e operações pertinentes. A publicação do ZIP de distribuição e a troca nos demais sites cabem à frota.

## 5. Limites e pendência

A prova de duração do pedido 82 induziu 125 segundos de latência dentro do verificador da pré-imagem de uma linha descartável. Ela comprova a continuidade depois do limite HTTP, a auditoria e o resultado gravado. A vazão de uma cópia grande sob carga real não foi medida. O teste preservou os dados de negócio do Site-Teste.

O aceite direto do pedido 83 em **ctooffice.com.br com a 0.46.0** depende da distribuição pela frota. Repetir `system/error-log` na janela de 13/11/2026 17:00 a 14/11/2026 11:00, UTC−03. Em `level=fatal`, conferir o grupo do TypeError do pedido core 402, cinco ocorrências e a pilha. Em `level=warning`, conferir a ausência de grupos independentes de continuação. Se a rotação já tiver removido a janela, o extrato sanitizado preserva a prova histórica em bancada. Os serviços comerciais de Ads e CRM ficaram fora do escopo funcional desta mudança.

## 6. Credenciais e configuração

A atualização usa a conexão administrativa já autorizada, com a capacidade apropriada para a instalação. Para uma conexão nova, configure autenticação e perfil em **Ferramentas → Fator3 MCP → Configurar → Conexão / Clientes**. Para executar SQL, confira o canal e a autorização de escrita em **Arquivos e banco**. Nenhuma nova credencial de fornecedor é necessária. O relatório e as evidências distribuídas omitem senhas, tokens de confirmação e conteúdo privado do site.

## 7. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `wp-mcp-fator3-0.46.0-instalador.zip` | 948268 | `0c595a473dc9edd1b97e5be206a904b0afa79d8d9ee5553490a2ca6a5b7d5da8` |
| Fonte | `wp-mcp-fator3-0.46.0-fonte.zip` | 7472131 | `58c1f3f28c77f619c085fc03665ff7fb3c971d91dd80e68d54acabfce8a5c89b` |
