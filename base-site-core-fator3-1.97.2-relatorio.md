# Entrega — Fator3 Site Core 1.97.2

Revisão 1 · 2026-11-19T11:01:08-03:00 · Implementação e homologação dos pedidos Core 432 a 437. Estado **com pendências de aceite de campo e fornecedor**.

## 1. De onde esta versão entra

Instalação nova ou atualização direta da base de desenvolvimento 1.96.0. O ZIP oficial de partida tem SHA-256 `dde2feadefdf08ab7973e7ea1be588b73709b723a088ef5549e43394aa7f73a5`. Os três candidatos recuperados da 1.97.0 eram idênticos, com SHA-256 `0f6a2a76485779f3eaa0f93011ae8ac3b0eea58b483912d50efca7489f5fe804`. O Site-Teste passou pela 1.97.0 e 1.97.1 até a 1.97.2. A frota que opera a 1.96.0 pode aplicar o instalador final em uma troca. A bancada verificou esse salto.

Requisitos do projeto e do cabeçalho: WordPress 7.1.4+, instalação única e PHP 8.3+, 64 bits. Bancada WordPress 7.1.4, PHP 8.4.27 e MariaDB. A versão do WordPress e do PHP no Site-Teste figura na seção de homologação. Conferidos os dois documentos centrais na revisão 5 de 02/11/2026, a regra comum e a aba do Core.

## 2. Convivência e encaminhamento

No conjunto integrado estavam ativos Core 1.97.2, MCP 0.51.0, Google 0.40.0, Meta 0.30.0, LinkedIn 0.26.0 e Pipedrive 0.12.0. A instalação limpa também foi exercitada com somente o Core. O contrato de configuração é 8.46.0. O catálogo gerado no WordPress local reúne 199 operações do domínio. No Site-Teste, o PublishPress da Fator3 usa a versão 2.0.3.

**MCP 0.51.0, Core 433.** O Core expõe a contagem de incidentes recentes. O patch experimental do canal inclui essa contagem em `system/health`. A publicação oficial dessa projeção cabe ao responsável pelo MCP. A bancada confirmou a projeção de um episódio e a rota de detalhe com o patch aplicado. O Core já oferece o detalhe nas suas próprias rotas. [Impacto no MCP](base-site-core-fator3-1.97.2-impacto-wp-mcp-fator3.md)

Google 0.40.0 fornece o dia do clique no acervo. Os workers usam a política de agenda do Meta e do LinkedIn. As verificações desta entrega não requerem alteração nos contratos de Google, Meta, LinkedIn, Pipedrive ou Implantador.

## 3. Mudanças e evidências

| Pedido | Comportamento entregue e prova |
|---|---|
| **432 · Conversão Google** | Para um GCLID elegível sem sessão, a fila preserva o destino vinculado, a referência e o instante do contato. Valida o dia no fuso do acervo quando disponível, o prazo de 90 dias, o consentimento e o recibo. GA4 sem sessão recebe `sem_sessao_ga4`. A bancada confirmou um único despacho Ads para o contato sintético e rejeitou clique futuro e fora da janela. O conjunto Google somou 52 verificações, com respostas externas simuladas. |
| **433 · Cron** | A agenda cobre seis prefixos, preserva recusas de filtros e registra etapa e operação. Atualizações concorrentes da option cron passam por comparação antes da gravação. Uma recusa de teste repetida gerou um incidente por gancho/dia. Após a remoção da causa, os workers Meta e LinkedIn retornaram, com registro do rearme e da recuperação. A origem precisa das ocorrências históricas em cada site depende da próxima evidência de campo. |
| **434 · Relatórios** | Para `formularios` e `resumo`, a rota escolhe o caminho integral ou a leitura por dia e, sob pressão, por página do site. A projeção de formulários evita carregar eventos de comportamento e quadros alheios. Cursor vinculado ao site, usuário e filtros. Com 16.800 eventos e limite de 128 MiB, os 30 dias terminaram em ambas as visões. O ensaio adicional inseriu 30 visualizações e conferiu todos os totais e linhas de cada uma das 60 fatias contra a consulta diária independente. Pico no ensaio de volume: 76,873,728 bytes. Se uma página de um único dia esgotar o orçamento, a resposta identifica a lacuna como `fatia_incompleta`, com totais nulos. Uma série com essa marca conserva lacunas. No Site-Teste, o intervalo de 19/10 a 17/11 terminou sem lacunas em uma consulta de resumo e em 30 consultas de formulários. Cada visão registrou cinco visualizações. |
| **435 · Markdown** | Shortcodes registrados são convertidos no contexto público anônimo. Até 32 blocos compartilham uma requisição assinada à página. Prazo HTTP de 6 s, 256 KiB por trecho e 1 MiB por resposta. Partes públicas do modelo do tema entram na representação. A falha de um bloco fica indicada no documento operacional e os demais trechos aproveitáveis são preservados. A bancada verificou duas ocorrências em ordem, uma única chamada, uma parte de modelo e um bloco indisponível. O Site-Teste passou de 9/14 para 14/14 páginas disponíveis. A consulta HTTP dos Markdown confirmou a biografia cadastrada nos quatro perfis, os cargos e a seção de artigos nos três perfis pessoais e a listagem de autor no diretório. Os cinco itens terminaram sem avisos de shortcode. Evidência em `evidence/1970/site-teste.json`. |
| **436 · Avisos do catálogo** | A família interna de incidentes exige sufixo SHA-256 válido. Uma chave malformada permanece visível ao operador. `como-usar` e `resumo-operacional-ler` compartilham os avisos. O ensaio abriu um registro de teste e comparou as projeções. A gravação administrativa continua restrita ao catálogo operável. |
| **437 · Sinais da caixa de e-mail** | `f3base_formularios_sinais` inclui as regras da caixa. O padrão para `email_suspeito` mantém a suspeita e desliga o aviso. Simulação, aplicação e releitura foram verificadas. Um MIME com DMARC reprovado entrou como suspeito, com zero mensagens na fila antes da aprovação. A aprovação pelo botão Salvar na tela real de Contatos gerou um único aviso, aceito pelo receptor Slack simulado. O painel mostrou a regra a 360, 768 e 1.440 px, com os controles esperados. |

Na retomada, o primeiro laboratório usava bancos distintos no processo WP-CLI e no servidor HTTP. A configuração foi corrigida e o teste de perfil público passou. A homologação remota da 1.97.0 detectou a resposta de cron recusada pelo schema e uma divergência entre as assinaturas de início e promoção do lote Markdown. Na 1.97.1, o MCP validou a resposta e os três lotes avançaram pelos cursores 8 e 11, até a publicação. A inspeção dos avisos individuais identificou trechos ausentes em três páginas. A 1.97.2 agrupou os shortcodes e ampliou o prazo da requisição pública.

## 4. Instalação e prova da troca

A frota confere o SHA-256 da seção 8 nos bytes do instalador oficial e usa `plugins/upload` com `expected_slug=base-site-core-fator3`, `expected_sha256`, `overwrite=true` e `activate=true`. O destino previsto para a distribuição é a raiz raw de `Fator3Ventures/claude-wordpress/main`. A publicação na frota cabe ao seu responsável.

No Site-Teste, a troca usou `plugins/upload-base64` com ZIP montado por transferência verificada, slug, hash, idempotência e pré-imagem. A instalação em nova requisição confirmou **20 etapas, 0 falhas, estado concluida**. O arquivo temporário do instalador final foi conferido após o upgrade. As sondas e a lista ativa ficam na evidência. Runtime do Site-Teste: WordPress 7.1.5, PHP 8.3.36.

| Prova | Resultado |
|---|---|
| Instalação limpa e migração direta | WordPress 7.1.4 e PHP 8.4.27. A versão final concluiu 20 etapas na migração. A política anterior do sinal foi preservada e a regra nova passou a aviso desligado. |
| Código, catálogo e artefatos | 611 arquivos PHP passaram no lint. 1286 arquivos do instalador comparados com a árvore de runtime. As cinco partes do catálogo e a referência Markdown foram geradas e conferidas no registro. |
| Documentação instalada | `f3base/documentacao-ler` anunciou `docs/RELEASE-1.97.2.md`. Foram lidas 4 páginas até o fim, 31 linhas, SHA-256 `a8547d01bf92e9743e4fc87f7a16a8bc12101a818e869a2801cdcaa9d407f87a`. A reconstrução correspondeu aos bytes entregues. |
| Autorização e interface | Visitante recusado na consulta de relatórios e na configuração. Painel conferido em Chromium e no HTML servido pelo WordPress. |
| Provedores e efeito externo | O código de Core e Google em WordPress foi exercitado com respostas Google simuladas. Correio e Slack foram interceptados na bancada. A projeção de incidente foi testada em uma cópia do MCP 0.51.0. |

## 5. Banco e correção por nova versão

A atualização usa o ciclo retomável do Core. A operação guarda o progresso da preparação e o identificador da geração publicada. A promoção confere o conteúdo selecionado e a revisão antes de substituir a geração anterior. Filas de conversão preservam contato, vínculo, consentimento e recibo. Os diagnósticos GA4 anteriores elegíveis são ajustados em lotes de até 50. Logs e marcadores de incidentes guardam o gancho e a data local para deduplicação. Ler a documentação e consultar as projeções não inicia envio ao fornecedor. Uma correção depois de instalar o pacote segue para outra versão.

## 6. O que permanece pendente

- **Frota e CTO Office.** O aceite do 431 observa a renovação até 22/11/2026 às 02h20 de Brasília. O aceite do 433 requer 72 horas de passagens CLI nos 12 sites, sem novo `could_not_set` nem worker ausente. A bancada demonstrou o mecanismo de recuperação.
- **CTO Office e Google.** Verificar no destino real o registro 184 e a ação 7861106540 enquanto elegível. A ação tem de aceitar o envio para comprovar o aceite comercial. O Site-Teste e a bancada não demonstram a contabilização em Ads.
- **Responsáveis pelos sites.** Conferir 30 dias em Korvena e Fator3 e 7 dias em CTO Office. Validar as páginas de autor e as duas páginas de serviço com seus temas e dados vivos. O aceite da frota para o inventário e para o e-mail depende da distribuição.
- **MCP.** Decidir a incorporação do patch ao diagnóstico agregado, conforme o encaminhamento da seção 2.
- Os ensaios locais de atualização e volume usaram PHP 8.4.27. O runtime PHP 8.3 do site compartilhado foi confirmado separadamente. A atualização desta rodada foi limitada ao Site-Teste.

## 7. Credenciais e configuração

A versão reutiliza os destinos já vinculados. O administrador pode simular e aplicar as regras de `f3base_formularios_sinais` por `f3base/config-core-escrever`, com a revisão atual. No painel, acesse **Site Core → Conexões e entregas → Avisos**. O Site-Teste confirmou `email_suspeito.aviso=false`. O site de homologação preservou a configuração existente. A bancada usou identidades sintéticas. Os arquivos de entrega contêm as evidências resumidas.

## 8. Identidade dos arquivos

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| [base-site-core-fator3-1.97.2-instalador.zip](base-site-core-fator3-1.97.2-instalador.zip) | 5706489 | `2c831351a5f5afc23a90eca5d85f469e906cbb10e65d4e13aec161f65eaaa801` |
| [base-site-core-fator3-1.97.2-fonte.zip](base-site-core-fator3-1.97.2-fonte.zip) | 8749175 | `4bc2062af62cc922eecd905e451e296c0ee4128dc85c2ab7d1dc0914895b5c48` |

Relatório externo canônico. A cópia interna antecede o fechamento do próprio ZIP fonte.
