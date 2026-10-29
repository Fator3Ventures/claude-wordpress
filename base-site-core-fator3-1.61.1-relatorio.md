# Entrega — Fator3 Site Core 1.61.1

Revisão: 1 · Data/hora: 2026-10-29T12:40:00Z · Rodada: implementação e homologação técnica
Slug: `base-site-core-fator3` · Versão: `1.61.1` · Contrato administrativo: `8.26.0`
Status: **com-pendencias de aceite real e revisão visual**. Implementação e provas técnicas abaixo concluídas; Site-Teste atualizado e ciclo confirmado.

## 1. De onde esta versão entra

Atualização direta da base canônica **1.61.0**, além de instalação limpa. A entrega anterior permanece preservada. O incremento patch segue a orientação do dono para versões adicionais no mesmo ciclo; não foi aplicada a regra minor padrão contra essa orientação.

Base recebida: instalador `base-site-core-fator3-1.61.0-instalador.zip`, 2879882 bytes, SHA-256 `77f914d180bafb9432e6e8dea332bf57ad6839e63670ccd282c3c8469703f4f1`; fonte 5374927 bytes, SHA-256 `dc105748e851704f4580c10ac0e247fcb6409ec4a69125c7259b7bd7c77b054a`. Não foi reconstruída uma base aproximada.

Entradas: instruções e padrão comuns revisão 4 de 16/10/2026; pedidos Core 335–347 de 29/10; entrega 1.61.0; fontes, instaladores, relatórios e impactos Google 0.23.0 e Meta 0.15.0; MCP 0.37.0, LinkedIn 0.13.0 e Pipedrive 0.4.0. Manifestos recebidos em `inputs/1610` e `inputs/1611/packages.json`. Contrato oficial Pipedrive de Persons/Mailbox preservado em `inputs/1611/pipedrive-openapi.yaml`.

Piso comprovado do Core: **WordPress 7.1.2 / PHP 8.3.6**. Instalação/atualização também testadas em WordPress 7.1.3/PHP 8.3.6/MySQL 8.0.46. Site-Teste: WordPress 7.1.4/PHP 8.3.36. O piso individual do Pipedrive 0.4.0 continua PHP 8.3.36.

## 2. Convivência e encaminhamentos

No Site-Teste permaneceram ativos MCP 0.37.0, Google 0.23.0, Meta 0.15.0, LinkedIn 0.13.0 e Pipedrive 0.4.0. A bancada isolada copiou esses runtimes e confirmou ativação em novo processo PHP. No laboratório PHP 8.3.6, Pipedrive 0.4.0 não foi ativado. Nenhum acompanhante foi alterado ou redistribuído no instalador/fonte Core.

| Destinatário | Versão examinada | Classificação / situação | Pedidos | Impacto individual |
| --- | --- | --- | --- | --- |
| MCP Google | 0.23.0 | alerta-tecnico e validacao-coordenada; conflito de opção resolvido no Core, aceite real aberto | Core 337/340/342; Google 44–46 | `base-site-core-fator3-1.61.1-impacto-wp-mcp-google-fator3.md`, revisão 2 |
| MCP Meta | 0.15.0 | validacao-coordenada; consumidor implementado, aceite real aberto | Core 340/341; Meta 23/24 | `base-site-core-fator3-1.61.1-impacto-wp-mcp-meta-fator3.md`, revisão 2 |

Os encaminhamentos foram preparados durante a integração e atualizados com o hash/testes finais; não foram enviados a terceiros. A proposta Google usava `f3base_google_ads`, já pertencente à conversão/tag. O leitor novo usa **`f3base_google_ads_acervo`**, preservando a opção anterior. Não aplicar o patch antigo recebido sobre esta versão.

Produtores Google 0.23.0 e Meta 0.15.0 devem estar disponíveis antes de habilitar seus consumidores. A instalação Core não concede acesso automaticamente. Google Ads, GSC consultas e monitoramento Meta exigem seleções/concessões próprias. A ausência do produtor pausa sua fronteira; funções próprias do Core continuam disponíveis. Não há alteração de contrato exigida de MCP, LinkedIn ou Pipedrive nesta rodada; não foram gerados impactos meramente informativos. Implantação em frota e publicação raw não foram executadas.

## 3. Mudanças e evidência

| Pedido | Problema tratado | Implementação | Evidência própria |
| --- | --- | --- | --- |
| 337 | GCLID sem enriquecimento local de clique | Leitor público Google Ads, associação exata, checkpoint por sessão/contato, conta/campanha/grupo/palavra-chave/rede/dispositivo e cobertura. Projeções em sessões e contatos. Revogação ou mudança de origem oculta observação antiga. | 85 verificações conjuntas Google/GSC, incluindo persistência e revogação; local e Site-Teste. |
| 340 | Falta de fotografia Google e leitura de alterações Google/Meta | Sete datasets Ads; blocos Google/Meta e continuações independentes em campanhas; contato por IDs e dia no fuso da conta; parceiro por mapa explícito. Alterações por entidade/campo com valores operacionais e autoria protegida. | 30 dias, 90 cliques, 30000000 micros; revisita substitui recorte; nenhuma chamada de fornecedor na leitura. Meta confirma valor antigo/novo e retirada de autoria sem capacidade. |
| 341 | Recebimento Meta e incidente ausentes no Core | Consumidor público `meta-ads-monitoring/1.0.0`, recebimentos browser/servidor e EMQ datada separados. Aviso exige zero confirmado, otimização ativa e atividade do pixel/evento/dia ou gasto concedido; reserva durável e deduplicação. | 17 verificações local/remotas: dia normal, zero sem atividade, pixels navegador/CAPI distintos, incidente válido, repetição e revogação. Transportes de aviso interceptados. |
| 342 | GSC editorial apenas por página | Acervo independente consulta × página × dia, publicação atômica após conclusão, retomada, revisita, lacunas e filtros exatos; `escopo=consultas` no histórico e `gsc_escopo=consultas` no editorial. | Página curta mantém parcial invisível; conclusão vazia publica; revisita substitui; histórico por página preservado. Incluído nas 85 verificações Google/GSC. |
| 343(c) | Aceite SMTP sem prova da mensagem no histórico | Message-ID e política congelados antes do envio; worker limitado consulta mensagem e thread, exige identidade exata e vínculo pessoa/lead; estados confirmado, nao_confirmado_no_prazo ou nao_conferido e instante no recibo individual. | 18 verificações local/remotas: identidade inválida, vínculo errado, excluída, paginação, prazo, erro, linha SMTP concluída, idempotência e eliminação. Somente respostas sintéticas de CRM. |
| Preservação de 335/336/338/339/343(a,b)/344/345/346/347 e 330–334 | Evitar regressão da base 1.61.0 | Sem reabrir implementações encerradas; mantidos contratos e funcionalidades da entrega anterior. | Regressões: 335/347 12; 336/339 15; 338 7; 343/344/346 20; coletor 345 5; 331–334 32; Meta desempenho 46 verificações. |

Novos grupos operáveis: `f3base_google_ads_acervo`, `f3base_meta_monitoramento`, `f3base_gsc_consultas`, `f3base_email_historico`. Catálogo efetivo: 187 abilities Core, 97 opções operáveis, 173 entradas no inventário de opções e 70 tabelas documentadas. A renderização das telas, simulação/gravação com revisão e negativas administrativas somam 22 verificações de fronteira. Foram preservados slug, basename, namespaces e identidade de atualização.

Limites de dados explícitos: termo individual de busca permanece nulo quando não fornecido; GCLID ambíguo não escolhe candidato; Google usa dia UTC e adjacentes, não promete encontrar um clique antigo reutilizado fora dessa janela. Revisões Ads são diárias, sem fotografia simultânea global do período. Custos e moedas não são misturados. Contagens Meta não são somadas como eventos únicos; EMQ observada não vira história retroativa. GSC não informa quantidade de consultas anônimas nessa dimensão: valor nulo com motivo, sem subtração inventada. O aceite de 342 que pede essa quantidade não pode ser declarado atendido com o contrato disponível.

## 4. Instalação e prova da troca

Site autorizado: https://fator3-teste-mcp-1.dreamhosters.com/ . Instalador transferido em partes com SHA-256 conferido e instalado por `plugins/upload-base64`, `overwrite=true`, `activate=true`, `expected_slug=base-site-core-fator3` e hash da seção 8. A operação foi sequencial; não houve troca de outros plugins.

Operação de pacote: `9d6b1c764b1d071c7809a1989d85255d`; backup de arquivos anterior: `31d0144f4ed2a2f437b295b5`. Versão antes/depois: 1.61.0 → 1.61.1, ativa em ambos. Sondas internas sem cache de `/` e `/wp-json/` passaram com HTTP 200 antes/depois; não são prova de acesso externo nem de negócio. O backup de arquivos não cobre reversão do banco.

A migração avançou por suas etapas nativas e foi confirmada no executor; estado final **concluida**, sem falhas, contrato 8.26.0. As observações pós-atualização já existentes concluíram cabeçalhos, navegação e verificação da conta Pipedrive configurada. Esse recibo automático de infraestrutura não comprova o novo histórico de e-mail nem autoriza teste comercial no Site-Teste. A tentativa limitada `executar-pendentes` para migração retornou sem resultados porque a confirmação já havia sido processada; a prova final está na leitura persistida do ciclo.

| Prova | Ambiente | Resultado | Evidência no fonte | Limite |
| --- | --- | --- | --- | --- |
| Sintaxe e empacotamento | PHP 8.3.6 | 569 arquivos PHP válidos; 800 arquivos de runtime | `evidence/1611/installer.json` | Lint não substitui comportamento. |
| Instalação limpa e atualização direta | WP 7.1.3 / PHP 8.3.6 | Fresh, upgrade 1.61.0, repetição, desinstalação preservadora e reativação passaram | `native-cycles-1611.json` | Banco descartável; transportes bloqueados. |
| Piso declarado | WP 7.1.2 / PHP 8.3.6 | Mesmos ciclos passaram com o mesmo ZIP final | `minimum/native-cycles-1611.json` | Não declara piso menor. |
| Google/GSC, Meta, e-mail e fronteiras | WP 7.1.3 e bancada WP 7.1.4 | 85 + 17 + 18 + 22 verificações passaram em cada ambiente | `request-*.json`, `site-request-*.json`, `site-boundaries-1611.json` | SDKs reais, fornecedores simulados. |
| Permissões MCP | Local e bancada Site-Teste | 16 verificações, incluindo revogação, passaram | `permissions-mcp-1571.json`, `site-permissions-1571.json` | Identidade sintética isolada. |
| Documentação completa | Local e bancada Site-Teste | 1974 verificações; 160 documentos / 762 páginas; sem falhas | `docs-1611.json`, `site-docs-1611.json` | Leitor real do pacote e autorização MCP, sem HTTP de fornecedor. |
| Documento novo pelo canal remoto | Site-Teste compartilhado | 62 linhas completas, continuação nula, versão 1.61.1 e hash conferidos | `site-doc-publica.json` | Manual `ACERVOS-E-EMAIL-1.61.1.md`. |
| Runtime instalado | Site-Teste | 800 arquivos com manifesto igual ao ZIP final | `site-read-final.json` | Manifesto SHA-256 `c1654e58ca6599f2667f6b990cfbd5c2cb8aa2cef4bf7de18d3a5bcadfe858da`. |
| Limpeza | Site-Teste | 101 tabelas isoladas removidas; zero restantes; diretório e manifesto removidos; controlador retirado | `site-cleanup.json`, `site-remove-controller.json` | Backups técnicos do MCP permanecem recuperáveis. |

Índice instalado: `docs/DOCUMENTACAO.md`. Leitor: `f3base/documentacao-ler`, parâmetros `arquivo`, `linha`, `limite` (máximo 200), retorno com versão, SHA-256 e próxima linha. Leitura integral também verifica allowlist, travessia negada e ausência de chamadas externas. Hash do manual novo: `0029a6455bb0c73c6874d98f7759878dd431af662a353150f36479977688f1ca`.

Na atualização nativa foi detectada e corrigida a guarda antiga do schema de contatos, que poderia pular as novas colunas; schema incrementado para 8 e prontidão passa a exigir as colunas efetivas. A matriz foi repetida com o ZIP final. O arquivo temporário de upload já estava ausente após a instalação: uma exclusão com guarda foi recusada por divergência e `files/stat` confirmou ausência, sem contornar a guarda.

Estado final: Core 1.61.1 ativo e ciclo concluído; acompanhantes inalterados; nenhum recurso de fixture ativo. DreamHost Panel Login 1.0.0, WP Super Cache 3.1.4 e Yoast SEO 28.8 permaneceram como encontrados. A comparação de opções na inspeção do site prova ausência de mudança pela leitura, não uma fotografia completa do banco antes/depois; preservação da atualização é demonstrada pelos ciclos locais. Nenhuma URL raw foi publicada nesta rodada.

## 5. Banco e volta de versão

Alterações aditivas: `google_ads` e `google_em` em sessões e leads; `pixel_id` em `f3base_meta_eventos`; `historico`, `historico_proxima`, `historico_final` na fila de e-mail; tabelas `f3base_gsc_consultas_coletas`, `f3base_gsc_consultas_linhas`, `f3base_gsc_consultas_lacunas`. Configurações e estados novos seguem o inventário. A publicação do GSC usa transação; revisita incompleta conserva publicação anterior. Workers mantêm checkpoints e limites; leituras não reparam concessões.

Antes de produção, guardar banco, arquivos, salts e guarda operacional segundo o procedimento da frota. Para voltar à 1.61.0, pausar tarefas novas e conferir recibos/efeitos antes de restaurar os arquivos da base. Colunas/tabelas aditivas podem permanecer, mas a base não as interpreta. Não foi realizado downgrade no site compartilhado. Desativação remove agendas Core; desinstalação mantém dados comerciais e suspende pendências, conforme política anterior. Eliminação de titular limpa enriquecimento e prova do e-mail; não reenvia mensagem. Nenhuma restauração de arquivos desfaz SMTP, avisos ou alterações remotas já aceitas.

## 6. O que permanece pendente

- **Dono/frota + Google — 337/340:** em ctooffice.com.br, habilitar seleção/concessões e comparar GCLID e 30 dias de gasto/cliques por campanha com a conta real. Não houve implantação de produção nesta rodada.
- **Dono/frota + Google — 342:** comparar consulta × página × dia com Search Console real. Quantidade de consultas anônimas não é disponibilizada pelo contrato recebido; continua desconhecida, com motivo. Não marcar esse subcritério como concluído.
- **Dono/frota + Meta — 340/341:** conferir alteração real, janela histórica efetivamente disponível e próximo incidente natural. Não zerar campanha para fabricar alerta; disponibilidade de 22–26/10 depende da Meta. Contagens e EMQ têm semânticas distintas.
- **Dono/frota — 343(c):** próximo lead autorizado em ctooffice.com.br ou korvena.com.br, com Mailbox acessível ao token, Message-ID preservado pelo transporte e comparação individual no histórico. Testes reais Pipedrive continuam restritos aos sites da decisão do dono; não foram criados contatos nem enviados e-mails reais para este aceite.
- **Responsável Core/revisor — interface:** revisão visual interativa no navegador pendente. O Playwright está disponível, mas Chromium não está instalado. Renderização PHP, textos, campos e estados foram testados localmente e no Site-Teste; não equivalem a aceite visual/responsivo.
- **Frota/dono — distribuição:** publicação raw, rollout e aceites reais herdados da 1.61.0 permanecem fora desta execução. O fonte fica com o dono conforme a decisão 89, sem push ao repositório público.

Não há falha conhecida nos testes executados do candidato final. As pendências acima não foram convertidas em sucesso por inferência de código ou relatório de fornecedor.

## 7. Credenciais e configuração do dono

Nenhum segredo novo foi solicitado, exportado ou entregue. Google/Meta mantêm credenciais e seleção de ativos nos respectivos produtores. O Core recebe apenas concessões públicas e usa opções tipadas com `revisao_esperada`, simulação e verificação administrativa no servidor. Leitura de GCLID/contatos/autoria requer também a capacidade pessoal pertinente.

Configurar `f3base_google_ads_acervo` com conexão, conta de dez dígitos e mapa de parceiros por ID; `f3base_meta_monitoramento` com conexão, conta, relatórios e datasets; `f3base_gsc_consultas` com janela/horário e propriedade GSC já comprovada. Esses três grupos entram desligados. Avisos Meta também entram desligados; habilitação grava operador autorizado e utiliza Slack do site ou e-mail técnico. Ausência ou revogação de concessão não recebe fallback por credencial administrativa.

`f3base_email_historico` entra ativo para mensagens novas com política congelada antes do SMTP: padrão 48 horas, consulta por mensagem a cada 60 minutos; worker verifica vencidos a cada cinco minutos. Requer conta Pipedrive válida e Mailbox legível. E-mail legado sem identidade congelada permanece `nao_conferido`. `confirmado` descreve a observação daquele instante; exclusão posterior no CRM não reescreve automaticamente o recibo.

Guia instalado com parâmetros, exemplos, autorização, limites e recuperação: `docs/ACERVOS-E-EMAIL-1.61.1.md`, complementado por `AGENTES-1.61.1.md`, schemas e inventário gerados do runtime. O domínio Pipedrive é fixado pela conta verificada; as novas consultas usam somente GET, sem corpos, e não escrevem no CRM.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
| --- | --- | ---: | --- |
| Instalador | `base-site-core-fator3-1.61.1-instalador.zip` | 2933589 | `9cfbab0b667c877c3c14b9d6704c827665d20d7b34ff4c9b9d915d6b3c9bd6d3` |
| Fonte | `base-site-core-fator3-1.61.1-fonte.zip` | 5723729 | `94617ef804d05bad17c4f68d8e62300b38b0e0145856f5925b6a4aefe1fcd08e` |

Relatório externo canônico: `base-site-core-fator3-1.61.1-relatorio.md`. A cópia no fonte é identificada como anterior ao fechamento; o hash/tamanho final do fonte são preenchidos somente no relatório externo para evitar circularidade. O runtime do fonte é conferido byte a byte contra os 800 arquivos do instalador testado. Nenhum ZIP da entrega contém outro ZIP, banco de laboratório, logs brutos ou credenciais reais.

Os dois impactos técnicos da seção 2 acompanham a entrega e também constam do fonte. Evidências antigas são históricas; o conjunto vigente é `evidence/1611`. Instalador tem raiz `base-site-core-fator3/`; fonte tem raiz `base-site-core-fator3-1.61.1-fonte/`. Somente o instalador é instalável no WordPress.
