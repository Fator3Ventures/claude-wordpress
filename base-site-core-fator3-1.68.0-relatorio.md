# Entrega — Fator3 Site Core 1.68.0

Revisão 2 — 02/11/2026, America/Sao_Paulo. Complemento de implantação após autorização explícita do dono. ZIPs da entrega original preservados, sem recompilação ou mudança de versão. Status: com-pendencias, exclusivamente pelos aceites e dependências discriminados na seção 6.

Rodada solicitada para considerar os novos pacotes e pedidos. Fechamento original em 01/11/2026 (America/Sao_Paulo; execução UTC em 02/11). Versão minor sobre a última entrega canônica 1.67.0. Código e artefatos concluídos para o escopo tecnicamente disponível; 369(d) possui dependência aberta de contrato do LinkedIn, descrita abaixo. Core 1.68.0 instalado e ativo no Site-Teste em 02/11/2026 às 00:40:13 -03, com atualização interna concluída e sondas aprovadas.

## 1. Bases aceitas

Normas comuns: 01-instrucoes-agentes-plugins-fator3.md e 02-padrao-desenvolvimento-plugins-fator3.md, revisão 4, 16/10/2026. Preservados slug/pasta/basename base-site-core-fator3, provider, prefixos, Text Domain e Update URI. Instalador é o único ZIP instalável. Fonte é uma árvore de desenvolvimento, sem ZIP aninhado.

Base Core 1.67.0: instalador `d781cdbccfb00fc3224385e4e12e8e67bf4a06b58e2c1f1d6a686bca3df94c6b`; fonte `b27e26695befc939cf147891baffa5bbb6aa930f9f25ef97a4269d539358755c`. Arquivos publicados não foram reescritos. A lista de pedidos recebida ainda citava 1.66.0 como última versão da frota; esta rodada usa a última entrega final 1.67.0, e registra a divergência em vez de retroceder a base.

Pedidos recebidos: Fator3 Site Core(20261102-022438).md, 20076 bytes, SHA-256 `aa900eb08e736cb48fb59fce554d761c597ac5b57aaef3c813c3e729c8e6d82e`. Cópia no fonte tem telefone removido; manifesto conserva o hash do insumo original. LinkedIn 0.15.0 instalador: 345084 bytes, SHA-256 `e12b2b468b71c53d7ecc67c55f758ee1af5ba2b24082f9b12046c66944169e85`; fonte recebido SHA-256 `0e2ca16e82629d4c5f9324514415a5877f946d27455b906b9fc15ede09f21c96`. Relatório e impacto revisão 3 recebidos foram lidos, sem tratá-los como testes próprios.

## 2. Convivência e encaminhamentos

Bancadas com Core 1.68.0 e MCP 0.38.0, Google 0.26.0, Meta 0.19.0 e LinkedIn 0.15.0. Ativação dos quatro acompanhantes e leitura documental pelo MCP foram repetidas nos dois WordPress. A fronteira alterada foi exercitada com o PHP real do LinkedIn 0.15.0, usando exclusivamente respostas HTTP sintéticas. Meta 0.19.0 teve repetida a integração da comparação de eventos da 1.67.0. Não se declarou fornecedor real homologado. Pipedrive 0.5.0 foi observado no inventário remoto, mas não teve o pacote inteiro requalificado nesta rodada; foi testada a resolução local do parceiro já configurado.

Contrato administrativo Core passa de 8.30.0 para 8.31.0, aditivo: novo campo opcional formularios_modo e nova ability. Contrato público LinkedIn 1.2 é negociado quando disponível; seleção explícita conserva negociação 1.1. Compatibilidade com produtor anterior é mantida no código, sem afirmar uma nova matriz de homologação com todas as versões antigas.

Encaminhamento pertinente: `base-site-core-fator3-1.68.0-impacto-wp-mcp-linkedin-fator3.md`, iniciado antes da implementação e atualizado na entrega, revisão 2, classes validacao-coordenada/acao-necessaria. Abrange adoção 1.2 e ausência de contrato de nome de campanha. Nenhum pacote acompanhante foi modificado; nenhum encaminhamento foi enviado a terceiros. Sem impacto novo identificado nas fronteiras Google, MCP e Meta: comportamento de APIs existentes preservado, sem nova exigência a esses produtores.

## 3. Mudanças por pedido e evidências

| Pedido | Entrega | Evidência própria / limite |
| --- | --- | --- |
| 368(a) | trim de bordas textuais antes da persistência; comparação equivalente do histórico; registro na lixeira preservado | request-368: 14 verificações por ambiente; defeito textual reproduzido na base 1.67.0 no ciclo de upgrade |
| 368(b) | conflito real grava ocorrência com identidade/campos sem valores; conserva contato; página continua somente após gravação | Falha SQL injetada exige repetição; replay deduplicado; coletor SDK avança janela sem substituir o contato |
| 368(c) | codigo/em em ultima_falha; código e contagens propagados ao resultado de integração/Execuções/diagnóstico | Erro HTTP simulado no produtor real alcança cursor e resultado da tarefa |
| 369(a,b,c,e) | opt-in todos_conta_autorizada, outbox 1.2, checkpoint por escopo, marco max(criação, ativação), recibo de assinatura reutilizado, inclusão/instante visíveis | request-369: 33 verificações por ambiente, produtor PHP real, assinatura única, CAS/replay, paginação 5+2, revisão, identidade, permissão e revogação |
| 369(d) | mapeamento tem precedência; nome decorado do LinkedIn é preservado; parceiro usa parceiros_plataforma.linkedin_ads; ocorrência pede completar mapa | Nome ausente da resposta não pode ser consultado pelo SDK 0.15.0. Dependência aberta, sem perda da importação; item não integralmente encerrado |
| 370 | catálogo Meta renovado em cada coleta com metadados mínimos; perguntas somente novas; coleta de conhecidos continua durante paginação/falha; instante de inclusão persistido | request-370: 11 verificações; request-370-collector: 12 verificações, incluindo fluxo completo pelo HTTP WordPress simulado |
| 365/366/367 | correções da base final preservadas | 213/37/248 verificações, mais 9 da fronteira Meta 0.19.0, por ambiente. Aceite na frota não inferido |

Alterações principais: LinkedIn_Descoberta e Meta_Descoberta novos; integração dos coletores, diário de ocorrências, assinatura SDK, diagnóstico, seleção administrativa e resolução de aquisição Pipedrive. Registro de bootstrap recompilado: somente os dois hooks novos do LinkedIn diferem da base. Mapa de autoload regenerado. Sem alteração nos assets JS/CSS ou nos SDKs externos. Todo PHP do runtime passou lint: 593 arquivos.

Ocorrências usam tabela existente f3base_linkedin_webhook, tipo ocorrencia e payload cifrado. Consulta mostra total e últimos 50 itens; não devolve resposta preenchida. Um conflito tratado possui ok=true/codigo=conteudo_conflitante_registrado e não equivale a falha de transporte. Gravação recusada mantém a página pendente. Os testes de implementação não criaram contato real, e-mail externo ou assinatura LinkedIn real. Na implantação autorizada, o próprio ciclo pós-atualização registrou a verificação da conta Pipedrive existente; isso não é homologação de importação ou entrega comercial.

## 4. Instalação, documentação e prontidão

| Ambiente | WordPress | PHP / MySQL | Resultado |
| --- | --- | --- | --- |
| Bancada atual descartável | 7.1.4 | 8.3.6 / 8.0.46 | Instalação limpa, atualização nativa direta 1.67.0→1.68.0, idempotência, desinstalação preservando dados e reativação aprovadas |
| Bancada mínima descartável | 7.1.2 | 8.3.6 / 8.0.46 | Mesmos ciclos aprovados |
| Site-Teste compartilhado | 7.1.4; Core 1.67.0 → 1.68.0 | PHP 8.3.36; não usado como bancada limpa | Instalação autorizada, ativa, atualização interna concluída, sondas HTTP e leitura documental aprovadas |

Os quatro ciclos nativos usaram o ZIP final SHA-256 `afff3783f11aff3395e2a37cd3938958d93dfe1d01e5e566789f1333ccf134a8`. WP-CLI oficial 2.12.0 executou a primeira passagem --due-now; migração/finalização confirmadas em processo novo. Preservados callback, opções, campos vazios, procedência, segredos sintéticos, contatos, filas, recibos e estados incertos. 70 tabelas/70 proprietários de estrutura conferidos, sem ausência.

Por ambiente: regressões 360 CTA (64) e 362 (10), além das suites acima. Documentação instalada lida integralmente, com paginação, hashes, confinamento de caminho, schemas e negação a anônimo/assinante: 1947 entradas de verificação, incluindo contadores documentais, por execução. Leitura repetida sem e com o MCP real carregado. Nenhum HTTP externo nessa leitura. A nova operação consta no registro e documentação gerada. O relatório não confunde lint, fixtures HTTP, WordPress nativo e fornecedor real.

Durante preparação do laboratório, uma cópia transitória do MySQL perdeu arquivo de redo entre execuções. As provas finais usaram datadirs novos e isolados, sem reutilizar aquele banco nem alterar site compartilhado. Falhas preliminares de harness (allowlist de versão e include de template administrativo) foram corrigidas antes das matrizes finais; não são ocultadas como falha de produto ou usadas como prova aprovada.

Site-Teste, antes da troca: class-f3base-cache-pagina.php tinha 44769 bytes e SHA-256 `f6f839293b98bfac0d079c4e6f46acd60f0a9a5e9676b868d89eaaed744c050a`. O final canônico 1.67.0 tem 45047 bytes e SHA-256 `9b2e68a7b77bec58f28c4cc2921470ceb10e37d86004c87149c692bec9ee1740`; essa última correção está no 1.68.0. A leitura remota depois da troca confirmou exatamente esses 45047 bytes e esse hash. A divergência da instalação anterior foi, portanto, eliminada pela instalação do pacote final.

Histórico da primeira tentativa: transferência f7e8fb5684eb445df9381cd5625e773f, três partes aceitas; a quarta foi recusada pela revisão automática por exigir autorização explícita de envio/implantação no destino. Cancelamento confirmado pela operação 3818b63b2b38942ea91c3e18, sem troca do plugin. Esse bloqueio foi resolvido pela resposta posterior do dono: “Autorizo”, em resposta ao pedido explícito de envio e instalação no Site-Teste.

Implantação autorizada em https://fator3-teste-mcp-1.dreamhosters.com/: nova transferência 23a133ce5fc78a445eb71d4de95e58e6, 17 partes, finalização aa6c1160e2c0f7301e471c5f. O servidor conferiu 4231467 bytes e SHA-256 `afff3783f11aff3395e2a37cd3938958d93dfe1d01e5e566789f1333ccf134a8`. Executado `plugins/upload-base64`, com `zip_path` do arquivo recebido, `expected_slug=base-site-core-fator3`, esse `expected_sha256`, `activate=true`, `overwrite=true` e chave idempotente própria. Usado transporte autenticado pelo MCP; não houve publicação em URL raw pública nem push ao repositório da frota.

Operação do pacote: `03bbcaa7cbbe6f4545b52d64adb4d596`; pré-imagem: `5cf9efc27800c1803d76e010`. `plugins/operation-status` confirmou `status=complete`, `verification_reason=verified`, `file_state=candidate`, versão 1.68.0 e ativo. Sondas de `/` e `/wp-json/` retornaram 200 antes e depois, com bypass de cache comprovado e processo PHP novo. São sondas internas da mesma origem, sem prova independente de acesso externo. A reativação silenciosa não equivale a execução do hook de ativação: a conclusão funcional foi conferida separadamente em `f3base/saude-ler`.

Prontidão Core: `f3base/saude-ler {compacto:true}` confirmou versão 1.68.0, contrato 8.31.0, atualização concluída em 00:40:15 -03, sem falha, recuperação `core_operacional` e não pausada. Pós-atualização concluiu cabeçalhos do cache, navegação e verificação da conta Pipedrive às 00:40:31 -03. Zero avisos; todas as filas resumidas com zero falhas e zero resultados incertos. `system/health {compact:true}` retornou `healthy=true`, nenhuma recuperação pendente e nenhum incidente registrado na janela de 24 horas. Meta sem Pixel, Google Ads desabilitado e LinkedIn sem conexão permanecem impedimentos preexistentes para homologar fornecedores.

Cron observado sem execução manual forçada: antes da implantação havia 2 hooks vencidos, atraso máximo de 178 segundos; durante a conferência, 10 hooks e 773 segundos. Às 00:46:08 -03, a execução regular havia reduzido o saldo para 4 hooks e 52 segundos, sem esperas por causa nem falhas nas filas. Isso confirma avanço da agenda no período; não equivale a ausência permanente de atraso, prova de crontab ou aceite de todos os fornecedores. Evidência final: site-install-final.json.

Documentação remota: operação descoberta, schema lido e oito documentos completos conferidos contra os bytes do instalador: DOCUMENTACAO.md, AGENTES-1.68.0.md, RELEASE-1.68.0.md, LINKEDIN-LEAD-SYNC.md, META-ACESSO-1.28.md, CONTRACTS.md, CONFIGURACAO.md e OPERACAO-E-RECUPERACAO.md. Foram nove páginas, 365 linhas; CONTRACTS.md foi lido em duas páginas, com versão/hash estáveis. Todos os oito hashes e conteúdos coincidiram. O catálogo de documentos foi consultado, e a nova ability `f3base/linkedin-formularios-configurar` foi descoberta com seu schema. Não foi repetida no site a matriz integral dos 1947 controles locais nem alterada uma conexão para produzir teste comercial.

Limpeza: removido somente `wp-content/uploads/f3base-core1680-authorized-afff3783f11a.zip`, com guarda pelo hash exato (operação a92a0a4b5c1875f04449052d); leitura posterior confirmou arquivo ausente. Pré-imagem do plugin preservada. Inventário final conservou os demais oito plugins com versões e ativação anteriores: MCP 0.38.0, Google 0.26.0, LinkedIn 0.15.0, Meta 0.19.0, Pipedrive 0.5.0, WP Super Cache 3.1.4, Yoast 28.8 e DreamHost Panel Login 1.0.0.

## 5. Banco e reversão

Sem tabela/coluna nova; não há migração destrutiva ou reprocessamento de contatos históricos. Configuração opcional não muda integrações existentes. Estado de descoberta e ocorrências são preservados conforme o inventário e diário já existentes. Voltar à 1.67.0 exige desativar a seleção automática e retirar a chave opcional antes da reversão, porque o schema antigo a desconhece. Preservar histórico e recibos, manter pré-imagem e conferir prontidão; não restaurar banco ou apagar dados como rotina. O rollback perde os recursos desta versão.

## 6. Pendências e responsáveis

1. **LinkedIn/Core — 369(d):** produtor deve fornecer contrato público de nome da campanha quando ausente da resposta; Core deverá adotá-lo após decisão/pacote. Detalhe e aceite no impacto. Não classificado como implementação concluída.
2. **Site-Teste — resolvido nesta revisão:** autorização recebida, pacote final instalado e ativo, pré-imagem preservada, hash/versão/prontidão/documentação conferidos e ZIP temporário removido. Os aceites com fornecedores abaixo continuam separados dessa prova de implantação.
3. **Frota — aceites reais:** 368 em conflito real autorizado; 369 em ctooffice após opt-in e concessões; 370 com criação real de formulário e observação ≤1h com cron. Não executados em produção nesta rodada. Seleção automática do cliente Core direto não foi adicionada; recurso utiliza o contrato do Plugin LinkedIn 0.15.0.
4. **Frota — 365/366/367 e metas anteriores:** manter lista recebida e aceites externos pendentes. Esta rodada não fecha metas de bytes/desempenho nem comprova recebimento de um próximo evento real. Documento central de pedidos não alterado.

## 7. Credenciais

Nenhum valor real de token, segredo, cookie ou senha exportado. Testes locais usaram credenciais e identidades sintéticas; HTTP e correio externos bloqueados. Conexões e grants reais não foram modificados. O fonte contém testes/manifestos e evidências sanitizadas; exclui laboratório, dumps, logs brutos, acompanhantes e dependências de desenvolvimento instaladas. Dependências necessárias ao runtime permanecem no instalador conforme a base.

## 8. Artefatos finais

| Arquivo | Bytes | SHA-256 |
| --- | ---: | --- |
| base-site-core-fator3-1.68.0-instalador.zip | 4231467 | `afff3783f11aff3395e2a37cd3938958d93dfe1d01e5e566789f1333ccf134a8` |
| base-site-core-fator3-1.68.0-fonte.zip | 8558916 | `9a92b147526dd9aae4fd1755472aed2cb996a4529f26837b727a5993d6244ec1` |

Fonte: runtime completo idêntico byte a byte ao instalador, build/testes, plano, insumos sanitizados, evidências atuais/históricas identificadas, impacto e cópia deste relatório marcada como anterior ao fechamento. Instalador: raiz única base-site-core-fator3/, 915 arquivos. Documentos instalados incluem RELEASE-1.68.0.md, AGENTES-1.68.0.md, DOCUMENTACAO.md, configuração/schema e registro de abilities.

Artefatos complementares desta rodada: este relatório português, agora revisão 2 de implantação, e o impacto wp-mcp-linkedin-fator3 revisão 2, inalterado. Hash final do fonte é inserido somente no relatório externo para evitar circularidade. Evidências originais: evidence/1680/wp714, wp712, installer.json, site-before.json e site-install-blocked.json. Complementos de implantação: site-install-authorized.json, site-docs-authorized.json e site-docs-verification.json. Esses novos registros estão consolidados neste relatório externo; os ZIPs imutáveis e sua cópia anterior do relatório não foram reempacotados. Estado final: Core 1.68.0 instalado e ativo no Site-Teste, validação local e operacional remota aprovadas no escopo descrito; dependência 369(d) e aceites reais da frota permanecem abertos.
