# Entrega — Fator3 Site Core 1.62.0

Revisão 2 · Fechamento UTC: 2026-10-30T01:54:24+00:00 · Data da rodada no cliente: 29/10/2026, America/Sao_Paulo.
Slug: `base-site-core-fator3` · Versão: **1.62.0** · Contrato administrativo: **8.27.0**.
Status: **implementado, instalado e homologado tecnicamente no Site-Teste**. Atualização 1.61.1 → 1.62.0 concluída após autorização explícita do usuário. Permanecem os aceites comerciais em sites reais e a validação coordenada com o Implantador.

## 1. De onde esta versão entra

Base direta canônica **1.61.1**, sem reconstrução aproximada. Instalador-base: `base-site-core-fator3-1.61.1-instalador.zip`, 2933589 bytes, SHA-256 `9cfbab0b667c877c3c14b9d6704c827665d20d7b34ff4c9b9d915d6b3c9bd6d3`. Fonte-base: 5723729 bytes, SHA-256 `94617ef804d05bad17c4f68d8e62300b38b0e0145856f5925b6a4aefe1fcd08e`. O incremento minor corresponde ao novo ciclo; a entrega anterior foi preservada.

Entradas: pedidos Core **348–351** do documento anexado em 29/10/2026; instruções e padrão comuns revisão 4; Google 0.24.0 e Meta 0.16.0 (fonte, instalador e relatório); MCP 0.37.0, LinkedIn 0.13.0 e Pipedrive 0.4.0. Manifesto dos novos anexos em `inputs/1620/packages.json`. Os produtores Google/Meta relatam rodada documental e preservação do runtime dos contratos consumidos pela 1.61.1; não foram aplicados patches antigos.

Piso preservado e exercitado: **WordPress 7.1.2 / PHP 8.3.6**, instalação única de 64 bits. Também exercitado WordPress 7.1.3/PHP 8.3.6/MySQL 8.0.46. O piso próprio de Pipedrive 0.4.0 é PHP 8.3.36; ele ficou inativo no laboratório mínimo. A rodada remota passou em **WordPress 7.1.4 / PHP 8.3.36**, com os cinco acompanhantes ativos, inclusive Pipedrive.

## 2. Convivência e encaminhamentos

| Pacote | Versão examinada | Prova própria desta rodada |
| --- | --- | --- |
| MCP | 0.37.0 | Ativo no laboratório: registro, permissão, decoração, redator real e documentação integral. |
| Google | 0.24.0 | SDK/armazenamento reais com respostas sintéticas: Ads, GSC consultas e monitoramento de alterações. |
| Meta | 0.16.0 | SDK/armazenamento reais: grants, nomes de campanhas, relatório diário e monitoramento. |
| LinkedIn | 0.13.0 | Ativação e convivência local; cliente selecionado preservado. |
| Pipedrive | 0.4.0 | Ativação e convivência na bancada remota PHP 8.3.36; prévia e recibo do CRM testados no Core, sem envio comercial real. |

Nenhum acompanhante foi modificado ou incluído nos ZIPs Core. O Site-Teste já tinha essas cinco versões ativas na consulta inicial e conservou-as na consulta final. A bancada remota confirmou as cinco versões ativas. Apenas o Core foi atualizado; os outros oito plugins preservaram versão e ativação. Os testes sintéticos não enviaram dados a fornecedores.

Impacto tecnicamente relevante: `base-site-core-fator3-1.62.0-impacto-implantador-base.md`, revisão 3, destinatário **implantador-base 2.14.0**, classificação alerta-tecnico/validacao-coordenada, Pedido 351. Orienta consumo da revisão efetiva do perfil e renovação de planos/exceções. Preparado antes do código afetado e atualizado após os testes; não enviado. Implantador não foi executado. Nenhuma alteração de contrato requerida nos produtores Google/Meta/MCP/LinkedIn/Pipedrive foi identificada; não foram gerados avisos de versão sem consequência técnica.

## 3. Mudanças por pedido e evidência

| Pedido | Implementação | Evidência própria |
| --- | --- | --- |
| 348 | Busca somente variacoes/domínios; nome é rótulo. Variação mais longa vence sobreposição global; empate pela ordem. Ignora caixa, distingue acentos e usa fronteiras Unicode. Domínio mais específico vence. Algoritmo versionado invalida fotografia antiga. | Rodapé com quatro marcas, rótulo sem variação, caixa/acentos/fronteiras, sobreposição iniciando depois, domínio específico, JSON-LD permitido sem vazamento para nome curto, cache antigo indeterminado. |
| 349 | f3base_campanhas_origem configura conta selecionada e nome do acervo independentemente. Novas capturas elegíveis gravam conta_da_configuracao e acervo_meta_ads, política e prova. Nome URL/mapa explícito prevalece. Jornal registra origem da Campanha. | Captura anônima contra SDK Meta real concedido, persistência da prova, vínculo no relatório diário pelo fuso da conta, prévia CRM/catálogo, recibo, revogação, conflito, conta errada, fontes desligadas, consentimento e histórico preservado. Guards locais cobrem ambiguidade, paginação incompleta, geração alterada, resposta inválida e exceção. |
| 350 | canal_codigo expõe chave nas respostas públicas, no simulador e em gravada/simulada de 30 dias; dados armazenados permanecem idênticos. | Redator efetivo MCP 0.37.0, ia_organica, precedência google_ads com gclid, leitura de registro por ability, prévia CRM e projeção recursiva. canal_chave também casa com o filtro de segredos, por isso foi usado canal_codigo. |
| 351 | Perfil 3.6 conserva ID/92 condições; 16 retenções esperam no mínimo 120. f3base_perfil_retencoes permite piso 1–120 com simulação. Revisão efetiva inclui hash. | 16 retenções conformes em 120; 60 diverge do piso 120; simulação de piso 60 aceita guarda 60/120 sem mudá-la; revisão salva coincide com candidata; pin antigo e valor 121 recusados. |

Novos grupos operáveis: `f3base_campanhas_origem` e `f3base_perfil_retencoes`. Nova ability: `f3base/campanhas-origem-simular`, administração + leitura de contatos. Catálogo: **188 abilities**, **99 opções operáveis**, **175 entradas de opções** no inventário e **70 tabelas** documentadas. Não há tabela ou coluna nova nesta versão.

| Suíte local | Verificações |
| --- | ---: |
| Pedidos 348/350/351 | 37 |
| Pedido 349, leitura 350 e limites de SDK | 38 |
| Regressões 331–334, com variação textual explícita no novo contrato | 32 |
| Regressões 335/347 | 12 |
| Sessões 336/339 | 15 |
| Regressão 338 | 7 |
| Google/GSC 337/340/342 | 85 |
| Meta monitoramento 340/341 | 17 |
| Recibo/canais/nativos 343/344/346 | 20 |
| Histórico de mensagem 343(c) | 18 |
| Autorização MCP | 16 |
| Ativação de acompanhantes locais | 4 |

Documentação instalada lida integralmente pela ability pública com autorização nativa MCP: **163 documentos, 767 páginas, 1988 verificações**, mais dois contadores no arquivo de evidência. A prova foi repetida com sucesso na bancada remota, usando a cópia dos arquivos instalados no Site-Teste. Conferidos hashes, conteúdo completo, aliases, schema/contrato, confinamento, ausência de HTTP e negativas a usuário sem permissão.

Na bancada remota passaram também **75 verificações dos novos pedidos**, **122 regressões** (337/340/342: 85; 340/341: 17; 343/344/346: 20) e **16 verificações de autorização MCP**. Total funcional/permissões remoto: 213, além da convivência dos cinco acompanhantes e da documentação. Não foram repetidas remotamente as demais suítes locais da tabela.

Pelo transporte MCP remoto, fora da bancada, foram lidos integralmente RELEASE-1.62.0.md e CAMPANHAS-MARCAS-PERFIL-1.62.md, este em três páginas até proxima_linha=null. O guia tem 45 linhas e SHA-256 `8e643bd7eadabf032f4d2ac5593ed31f7e18634cca71023db7a3a6405752e6dd`. Simulações com regra candidata retornaram canal_codigo=ia_organica e, com gclid, canal_codigo=google_ads; ambas persisted=false. A chave antiga continuou redigida pelo MCP.

## 4. Instalação e prontidão

O ZIP exato da seção 8 passou por instalação limpa e atualização **1.61.1 → 1.62.0** em WordPress 7.1.3 e 7.1.2, ambos PHP 8.3.6. Em cada percurso: processos novos, ciclo/finalização, repetição, preservação de configurações e dados, desinstalação e reativação com recibos históricos/estados incertos preservados e somente pendências suspensas. Evidências: `evidence/1620/native-cycles-1620.json` e `evidence/1620/minimum/native-cycles-1620.json`. O ciclo isolado não requer produtores.

**Site-Teste atualizado:** https://fator3-teste-mcp-1.dreamhosters.com/, pelo conector WP MCP fator3-teste. Após a resposta explícita “Sim, autorizo”, o mesmo instalador da seção 8 foi enviado e instalado. Operação nativa `5ea0054b8e708e6bf9f27f77cc985dd0`; backup dos arquivos anteriores `afb26e323587d5989fb6a757`; SHA-256 do pacote confirmado pelo instalador. Core **1.62.0 ativo**, contrato **8.27.0**.

Ciclo nativo `e465177b-4ff2-4e87-bf53-6f5b72954dcf`: concluído, confirmado no executor, zero falhas e pós-atualização concluída. As sondagens internas sem cache de `/` e `/wp-json/` retornaram HTTP 200 antes e depois da troca. Essas sondagens provam saúde na mesma origem; não equivalem a verificação independente por navegador externo. A rotina automática existente conferiu cabeçalhos, navegação e a conta Pipedrive; isso não é aceite de entrega comercial.

O controlador temporário executou somente operações fechadas e uma bancada isolada por diretório e prefixo exclusivo de tabelas, com HTTP/e-mail de fornecedores bloqueados. Limpeza concluída: **101 tabelas próprias removidas, zero restantes, diretório e manifesto removidos**. Controlador removido com backup obrigatório do código; ability temporária confirmou “not found”. As sondagens passaram novamente após sua remoção. Consulta de arquivo confirmou ausência do ZIP de estágio, já consumido pela instalação. A comparação final dos nove plugins confirmou alteração apenas do Core.

A revisão 1 documentava uma transferência bloqueada e cancelada. Essa pendência foi resolvida pela autorização explícita e pela operação acima, sem reconstrução do pacote. A prova completa desta retomada está em `base-site-core-fator3-1.62.0-homologacao.json`.

## 5. Banco, preservação e reversão

Armazenamento novo é aditivo: política da campanha e piso do perfil em options; prova de campanha no JSON de novas capturas; fonte da Campanha no recibo/journal já existente. canal_codigo é projeção, não migração de registros. Nenhum contato anterior, mensagem ou retenção operacional é regravado. O hash de idempotência usa a entrada antes do enriquecimento.

Sem nova tabela/coluna; não há conversor histórico nesta versão. Foram conferidas 804 identidades de arquivos entre árvore de runtime e ZIP; zero arquivos removidos da base. A fonte contém a mesma árvore. O manifesto dos 804 arquivos remotos corresponde ao instalador. Instalações nativas de laboratório preservaram históricos e filas conforme a política existente de uninstall; isso não representa reversão automática de banco em produção. A inspeção remota somente de leitura manteve as opções verificadas inalteradas; não foi produzida fotografia integral do banco antes/depois da atualização remota.

O backup nativo remoto cobre os arquivos anteriores do plugin; não representa backup ou reversão de banco. Para implantação na frota, manter backup próprio do banco e dos arquivos. Trocar só os arquivos pelo instalador-base não desfaz capturas/configurações já gravadas. Não apagar dados ou reduzir prazos para simular rollback. Desabilitar as fontes novas por configuração é possível sem retirar os dados históricos.

## 6. Pendências, limites e responsáveis

- **Aceites 348–351 em sites reais — frota/dono:** conferir marcas nas URLs citadas; próximo contato Meta com conta/nome vigente no CRM e no relatório; canal_codigo legível; ausência de divergência de prazo. Não foram criados contatos reais, enviados avisos/e-mails, publicados arquivos no Git nem alterada a frota.
- **Implantador 2.14.0 — responsável do pacote:** validar leitura/revisão dinâmica em WordPress novo descartável; não reativar em site já entregue. Impacto individual anexo.
- **Aceite comercial Pipedrive — frota/dono:** ativação e convivência em PHP 8.3.36 comprovadas. Prévia e fotografia de intenção não provam entrega real. Testes comerciais continuam limitados aos sites expressamente autorizados pelo dono, nunca ao Site-Teste como conta de negócio.
- **Visual:** não houve revisão visual humana nem captura de navegador; alterações desta rodada usam a configuração/ajuda existentes, sem redesenho de tela ou JavaScript novo.

Nome Meta exige conta/campanha exatas e concessão ativa. Consulta somente acervo local, até 10 páginas de 100 linhas e dois segundos por toque, janela padrão 30 dias configurável até 366; leitura incompleta/ambígua/invalidada não inventa nome. Usa observação com nome mais recente e registra o dia, sem inferir identidade pela data. Registros antigos sem conta continuam fora do vínculo diário. Nomes da URL e mapas explícitos prevalecem.

A inspeção de marcas não executa JavaScript e sinaliza limites. Texto visível e destino de link são evidências distintas. O perfil não promete conformidade global: outras condições/evidências podem continuar divergentes ou indeterminadas. Alterar piso invalida revisão/plano anterior, sem alterar a guarda real. Pendências antigas de aceite comercial permanecem com a frota; não foram reabertas como defeitos de implementação desta rodada.

## 7. Credenciais e segurança da entrega

Nenhuma credencial real foi solicitada, alterada ou incluída nos novos artefatos. Leitura de nome Meta usa o SDK público do produtor e revalida sua concessão; não lê opções privadas nem chama Graph. Não houve envio a fornecedor nos testes sintéticos. Configuração candidata e simulação respeitam capacidade e revisão. Não foi relaxado o filtro do MCP para expor canal: mudou apenas o nome do alias de apresentação.

Os ZIPs não incluem banco/WordPress de laboratório, logs, helper de armazenamento, repositório Git, dependências de desenvolvimento ou outros ZIPs. O instalador não inclui QA temporário. Fonte reúne código, documentação, testes, evidências e entradas do projeto; documentos recebidos são evidência de origem, não resultados próprios. Revisão de segredos deve ser mantida antes de eventual publicação pública pela frota.

## 8. Artefatos e fechamento

| Artefato | Bytes | SHA-256 |
| --- | ---: | --- |
| `base-site-core-fator3-1.62.0-instalador.zip` | 2948015 | `3dcbae9b1e22b915ac32ae3074cec1ed15706d4a475a9cf5d5b9e12663922646` |
| `base-site-core-fator3-1.62.0-fonte.zip` | 5859483 | `dd6f4dd466a57ec2cdcbf72492a98678a966dc38e96123c5f8fa1255b61cbe0a` |

Complementos: `base-site-core-fator3-1.62.0-relatorio.md` (este relatório canônico, revisão 2), `base-site-core-fator3-1.62.0-impacto-implantador-base.md` (revisão 3) e `base-site-core-fator3-1.62.0-homologacao.json` (evidência remota complementar). Os dois ZIPs permanecem idênticos aos entregues antes da autorização; não foram reconstruídos. A cópia do relatório e as evidências internas no fonte antecedem esta homologação, complementada pelos arquivos externos atuais. Não há circularidade de hash.

Instalador: **804 arquivos**, **570 PHP validados por sintaxe**, única raiz `base-site-core-fator3/`, basename preservado. Fonte: raiz `base-site-core-fator3-1.62.0-fonte/`, runtime certificado byte a byte contra o ZIP testado. Manifesto canônico local/remoto: `dfa647c3da5b5c582252f020c19c730e7efbb534fa38e71858854bf6b38cb514`. Método: SHA-256 do JSON compacto de caminho relativo → SHA-256, chaves ordenadas lexicograficamente, sem escape de barras/Unicode. O manifesto da revisão anterior usava outra ordem de serialização; a diferença de hash não corresponde a alteração de arquivos. Provas locais ficam em `evidence/1620`; provas remotas desta retomada, no complemento externo; provas herdadas não são recontadas como novas.

Core 1.62.0 instalado e validado no Site-Teste. Nenhuma implantação em outros sites ou publicação no Git foi realizada. Preservar os hashes acima em futuras implantações.
