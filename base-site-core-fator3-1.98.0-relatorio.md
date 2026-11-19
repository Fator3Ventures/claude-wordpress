# Entrega — Fator3 Site Core 1.98.0

Revisão 1 · 19/11/2026 · Pedido Core 438 implementado e homologado no Site-Teste. O aceite de campo em Engagia está pendente.

## 1. De onde esta versão entra

Instalação nova ou atualização direta da 1.97.2, sem versão intermediária. O instalador oficial de partida tem SHA-256 `2c831351a5f5afc23a90eca5d85f469e906cbb10e65d4e13aec161f65eaaa801`. O fonte de partida tem SHA-256 `4bc2062af62cc922eecd905e451e296c0ee4128dc85c2ab7d1dc0914895b5c48`. Foram lidos integralmente `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, revisão 5 de 02/11/2026, além do padrão do Site Core e da regra comum enviados pelo projeto.

Requisitos atuais de WordPress 7.1.4 e PHP 8.3 de 64 bits em instalação única. Contrato de configuração 8.46.0, perfil `piso-padrao-3.6`, 103 opções operáveis e 199 abilities próprias. Os geradores conferiram os cinco catálogos e a referência de operações contra o registro ativo. A versão conserva o conjunto de operações.

## 2. Convivência e encaminhamento

O Site-Teste estava com MCP 0.52.0, Google 0.40.0, Meta 0.30.0, LinkedIn 0.26.0, Pipedrive 0.12.0, Yoast 28.9 e WP Super Cache 3.1.5 ativos. O ensaio isolado também cobriu o Core sozinho. O pacote de entrada do MCP 0.52.0 foi identificado pelos hashes SHA-256 `44e5cfbff907a50cfd50ee4c5d5789055393f4965931d54ae24b09c60c4f8e9f` do instalador e `ae24e51083ab4ff6f0591ca43d008562d8efca783fb6054cc2d722a8b665f0de` do fonte.

O retorno do mantenedor encerrou a dependência de código **Core 433 / MCP 89**. Antes e depois da atualização, o canal oficial `system/health` retornou `incidents_24h.pacotes_fator3` com zero episódios, último instante nulo e detalhe `f3base/incidentes-tecnicos-ler`. O relatório recebido registra também o caso positivo com uma falha sintética. A integração segue compatível. O pedido 438 atua no filtro de grafo já existente do Yoast. Os demais plugins e o Implantador permanecem aptos a consumir o contrato atual, sem encaminhamento de desenvolvimento ou ordem especial de troca.

## 3. Mudanças e evidência

**Pedidos core 438.** Em Engagia, a consulta à página 28 em produção, ainda na 1.97.2, confirmou os dois cartões verificados e as duas ofertas pendentes. Dois GETs de `/precos/` responderam 200 com HIT do cache de página e o mesmo corpo. Os dois IDs esperados estavam ausentes. O diagnóstico registrou HTTP 403 no perfil LinkedIn.

O cache interno do grafo guardava o resultado da extensão do Yoast antes de existir uma prova do cartão. Sua chave não incluía a elegibilidade atual das ofertas. Ao reutilizar o grafo, o Core também deixava de registrar os marcadores da renderização. O ensaio com a 1.97.2 reproduziu a pendência tanto no WordPress local quanto no Site-Teste.

A 1.98.0 reavalia o grafo na renderização de páginas com oferta cadastrada. Uma prova válida de conteúdo já habilita a emissão na próxima renderização. A leitura pública seguinte confirma, para cada item, o nó completo, o preço, a assinatura e o marcador do Core. A prova negativa atual conserva a causa de divergência ou conflito na consulta. Nas demais páginas o cache interno continua disponível. O observador solicita a atualização do cache após mudança de contexto ou elegibilidade e agenda a próxima verificação das ofertas pendentes. Uma pendência estável pode voltar a solicitar a atualização depois de cinco minutos.

| Cenário | Resultado |
|---|---|
| Site-Teste, Core 1.97.2 | Os dois cartões passaram na verificação. Em duas passagens, ambos permaneceram pendentes. As duas buscas no HTML servido deram HIT e não localizaram os IDs. |
| Site-Teste, Core 1.98.0 | Com o mesmo cadastro e Yoast ativo, ambos os IDs apareceram. Depois de editar o texto do primeiro cartão, os GETs dos dois IDs e do novo texto devolveram 200 com o mesmo SHA-256 do corpo. Houve HIT. A releitura persistida confirmou duas ofertas publicadas, ambas com emissor confirmado. |
| WordPress local em `/precos/` | O parser de JSON-LD confirmou exatamente dois nós Offer, com valores mensais de R$ 497 e R$ 1.500. Os sufixos dos IDs são `05c2ec61956d4673ea24d319` e `505a0b0361d204ac5c993cee`. Com a prova reiniciada, uma passagem do cron deixou as duas pendentes e a segunda publicou ambas. |
| Integridade da prova | Ao alterar o preço visível de apenas um cartão, o verificador registrou divergência. Na renderização seguinte permaneceu apenas a outra oferta. Provas vencidas suprimiram a emissão. A retirada do marcador manteve a confirmação pendente. Um Service de terceiro preservou o conflito na consulta e bloqueou a emissão do Core. Duas leituras sucessivas da mesma pendência não repetiram a solicitação de limpeza. |
| Perfil sameAs com HTTP 403 | Um recurso HTTP controlado respondeu 403 no ensaio local. A verificação geral ficou inconclusiva, enquanto os dois nós foram observados como publicados. O estado do perfil social é independente da emissão e da confirmação de cada oferta. |

As evidências estão em `evidence/1980/` no fonte. Os ensaios locais usam requisições HTTP distintas ao WordPress. O adaptador local emite um grafo de ensaio pelo filtro do Yoast. O Site-Teste usa o plugin Yoast real e um permalink exclusivo de homologação.

## 4. Instalação e prova da troca

O ZIP final foi instalado em WordPress 7.1.4 com PHP 8.4.24, tanto em instalação limpa quanto sobre o instalador oficial da 1.97.2. Cada ciclo concluiu 20 etapas com zero falhas e confirmação no executor. O manifesto conferiu 1.288 arquivos. Os 611 arquivos PHP do runtime passaram no lint.

No Site-Teste, WordPress 7.1.5 e PHP 8.3.37, a transferência em 22 partes conferiu bytes e SHA-256 antes de `plugins/upload-base64`. A operação usou `expected_slug=base-site-core-fator3`, o SHA-256 da seção 8 e ativação após a troca. As sondas anterior e posterior passaram. O slug foi preservado. A atualização e a confirmação no executor ocorreram em requisições distintas.

| Leitura do Site-Teste | Resultado observado |
|---|---|
| `f3base/como-usar` e `f3base/saude-ler` | `versao_alvo=1.98.0`, `estado=concluida`, 20 etapas, `falhas=0`, `confirmada_no_executor_em=1795123097`, em 19/11/2026 às 18h18min17s de Brasília. Uma consulta inicial retornou `em_andamento`. A confirmação depende da primeira passagem disponível do executor. |
| `f3base/documentacao-ler` | O índice anunciou `docs/RELEASE-1.98.0.md`. Quatro páginas cobriram as 17 linhas e reproduziram integralmente o arquivo local, SHA-256 `28bd7d0ea871e9729e031d700c64204bb7053545f61dc43d942a11a32add2896`. |
| Acesso | As operações administrativas de consulta foram exercitadas pelo perfil de manutenção autorizado no Site-Teste. No laboratório, a consulta anônima foi recusada. Os resultados locais registram também a decisão do perfil MCP e o caso do administrador com o Core sozinho. |
| Limpeza | A configuração voltou à revisão original. Saíram os dois registros de prova do ensaio, com os outros cinco preservados. A página temporária foi movida à lixeira e o permalink passou a responder 404. O ZIP temporário da atualização já havia sido removido. `system/health` encerrou com `healthy=true`. |

A homologação usou o arquivo transferido e verificado no próprio Site-Teste. A publicação da URL raw para distribuição na frota cabe à operação de distribuição.

## 5. Banco, migração e correção por nova versão

O ciclo executa as etapas registradas de preparação das integrações, estruturas, configurações, manutenção, verificação, agendas, perfil público e ativos. O detalhamento por etapa acompanha a evidência de instalação. Esta rodada reutiliza a opção interna `f3base_ofertas_evidencia_v2`. Um item pendente pode registrar `ultima_solicitacao_cache_em` para limitar a frequência de solicitação da limpeza. As opções existentes e o cadastro de ofertas são preservados. A versão não cria tabela, opção operável ou novo evento.

A retomada das ofertas ocorre pelo verificador e pelo evento `f3base_ofertas_verificar`. A limpeza de cache e as provas já gravadas têm efeito próprio. A política de recuperação é correção para frente em nova versão.

## 6. O que permanece pendente

**Frota Engagia.** Após instalar o ZIP da seção 8, conferir o HTML servido de `https://www.engagia.com.br/precos/` e a consulta `f3base/schema-verificar`. O aceite de campo exige os dois nós Offer no corpo servido e os itens `plano-engagia` e `ghostwriter` em `publicada` com emissor confirmado. A implantação da 1.98.0 neste domínio ficou fora da homologação no Site-Teste. O pedido 438 sai do desenvolvimento desta rodada. O próximo número disponível é 439.

A frota segue responsável pela janela operacional de 72 horas do Core 433. Esta rodada não homologou a identidade do perfil LinkedIn, rich results do Google, entrega por CDN externa ou aparência visual dos cartões em navegador. A validação de ofertas usou o HTML efetivamente servido e o estado persistido.

## 7. Credenciais e configuração

A versão utiliza o cadastro de serviços e ofertas vigente. Não requer novo segredo, autorização de conta de anúncios ou credencial de fornecedor.

## 8. Identidade dos arquivos

| Tipo | Arquivo | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | base-site-core-fator3-1.98.0-instalador.zip | 5708805 | `419dab4e9e822ed5a77239dcaef5598554cf50700c633f9625a0dcf91cbb7d5b` |
| Fonte | base-site-core-fator3-1.98.0-fonte.zip | 8844518 | `88e5e4a2c5fdc2507ad0669165079923872c3cd008ca15c159c0b892905c3951` |

Relatório externo canônico. O fonte contém a cópia anterior ao fechamento com os mesmos resultados funcionais. A linha de identidade do fonte foi completada após o empacotamento.
