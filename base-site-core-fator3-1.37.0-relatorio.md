# Entrega — Fator3 Site Core 1.37.0

Revisão 1 · 18/10/2026 · Pedidos core 225 e 226(a–h).
**Estado: implementado e instalado no Site-Teste; com pendências de aceite comercial em fornecedor real.** Os limites e responsáveis constam na seção 6. Não houve implantação em produção, envio de encaminhamentos nem publicação pela frota.

## 1. Bases aceitas

- Base direta: **1.36.0**, instalador com 1.967.841 bytes e SHA-256 `eeec2a765d7e004aab1046fd59a25e455b6b5651d4468368fdf220b3e23d811b`; fonte com 2.088.119 bytes e SHA-256 `867b4a3dd122858019526197a093168deba6a484de123e0c8349140b1fa82063`.
- Referências recebidas: Fator3 Site Core(4).md; Instruções comuns e Padrão de desenvolvimento r4, 16/10; plano Google 0.12.0 r2 e impacto Google→Core r2, 17/10. O plano Core 1.37.0 foi atualizado de r1 condicional para r2 com o escopo 226 e r3 com o resultado desta execução.
- O aceite da base nos 12 sites e o encerramento de 212(a)/224 são informações recebidas do acompanhamento da frota, não testes repetidos nesta rodada. Aceites adicionais de produção continuam sob o item 20, sem reabertura dos anteriores.
- Identidades preservadas: pasta/slug/provider `base-site-core-fator3`, basename `base-site-core-fator3/base-site-core-fator3.php`, namespace `f3base`, Text Domain e Update URI existentes. Versão minor incrementada por alteração funcional do pedido 226.

## 2. Convivência e encaminhamentos — pedido 225

| Item | Base 1.36.0 | Entrega 1.37.0 |
|---|---|---|
| Contrato administrativo | 8.1.0 | **8.2.0**, aditivo |
| Perfil | piso-padrao-3.5 | piso-padrao-3.5, revisão 2026-10-12-core-1.31.0 |
| Opções operáveis | 65 | **65**; adicionadas 0, removidas 0 |
| Entradas no contrato | 68 | 68; três não operáveis: nav_id, operaveis, politica_canal |
| Opções no JSON de referência | 67 | 67: 65 operáveis mais duas de governança |
| Abilities do provider Core | 130 | **130**; adicionadas 0, removidas 0 |
| SDK de medição | site-measurement-context/1.0.0 | Inalterado, schema_revision textual "1" |
| SDK de finalidades | site-conversion-purposes/1.0.0 | Inalterado, schema_revision textual "1" |
| Estrutura | Marcador 1.35.0 | Marcador 1.35.0; ciclo de instalação 1.37.0 |

Mudam cinco propriedades de `f3base_pipedrive`: empresas_invalidas, mapa_servicos_formularios, mapa_servicos_campanhas, atividade_canais e atividade_janela. `mapa_campos` admite respostas_formulario e lead_nativo_id. Tipos/recusas estão no código e nos schemas instalados; a quantidade de opções operáveis não aumenta por subpropriedade.

| Acompanhante | Evidência nesta rodada | Consequência |
|---|---|---|
| MCP 0.24.0 | Ativo no Site-Teste; instalação, descoberta e documentação exercitadas | Transporte preservado |
| Google 0.11.0 | Ativo e compatível na descoberta de saúde do Site-Teste | Ambos os SDKs e schemas conferidos byte a byte contra a base |
| Google 0.12.0 r2 | Plano/impacto recebidos; pacote novo não fornecido | O contrato aceito da 1.36 já atende; sem nova dependência de 1.37 |
| Meta 0.3.0 / LinkedIn 0.3.0 | Presença e versões observadas; APIs reais não chamadas | Interfaces externas preservadas; normalização Core testada com payloads sintéticos |
| Implantador 2.5.0 citado na aba | Runtime não fornecido: `nao-avaliado` | Conferir descoberta/edição de configuração 8.2.0 |

Encaminhamento tecnicamente pertinente: **base-site-core-fator3-1.37.0-impacto-implantador-base.md**, r2, `validacao-coordenada`. A r1 foi preparada antes da implementação; a r2 registra contrato real, hash e provas, preservando o histórico. Não foi enviado. Não há novo impacto Google apenas para anunciar versão; o limite avaliado é a conservação dos SDKs. Não se declara concluído trabalho de outro plugin.

## 3. Mudanças por pedido e evidência

| Pedido | Implementação | Prova e limite |
|---|---|---|
| 225 | Metadados de convivência, contagens e delta explícitos neste relatório | Contrato executável e descoberta remota: 130 abilities na 1.37.0 |
| 226(a) | Modelo explícito sem {site} omite host; {unidade} usa rótulo; empresa inválida usa pessoa | Casos de título, limite e marca de teste; sem retitular oportunidades anteriores |
| 226(b) | Empresa inválida não gera busca/criação/vínculo novo; lista configurável e normalização de caixa/acentos | Vazios, negativos, nome da pessoa, URL/e-mail/telefone; pessoa/organização anterior preservadas |
| 226(c) | Todas as respostas em campo longo, rótulos/alternativas e nota preservados; Google retém column_name | Site e três origens nativas; complemento reúne respostas iniciais/adicionais; arquivos ficam fora do campo |
| 226(d) | Serviço por resposta, formulário nativo ou campanha, nessa ordem; aviso de ausência com IDs de origem | Prioridades, catálogo e alternativas inválidas; IDs reais dependem do projeto Pipedrive |
| 226(e) | C1 WhatsApp/E-mail/tarefa; tipo/assunto configuráveis; expediente e fuso; plano durável antes do POST | Fim de expediente, fim de semana, antes da abertura, arredondamento de segundos, DDD inválido e retomada; hora na conta real ainda pendente |
| 226(f) | Negócio aberto: nota/tarefa de reenvio; lead aberto de outra origem: nota; ambiguidades exigem revisão | Nenhum novo lead no negócio, título/atividades anteriores preservados; timeouts de lead/nota/atividade reconciliados sem duplicação |
| 226(g) | Papel lead_nativo_id para Meta/Google/LinkedIn e motivo explícito de anúncio ausente/omitido | Normalização/persistência/projeção das três origens; não determina a causa histórica dos dois casos Apex sem payloads/IDs completos |
| 226(h) | Link e prazo enviados pela outbox da thread original, com confirmação distinguida de previsão | Principal, deduplicação, 429, timeout, supressão e troca de destino; nenhuma mensagem real enviada nesta rodada |

A C1 usa entrada do contato no Core. Padrão: segunda a sexta, 08:00–19:00, America/Sao_Paulo, mais 60 minutos; sem tempo suficiente, próximo dia útil 09:30. Antes da abertura em dia útil, 09:30 desse dia. Sem calendário de feriados. O envio usa HH:MM UTC, arredondando segundos para cima. Tipos WhatsApp/E-mail/task precisam existir na conta; celular elegível não comprova WhatsApp alcançável.

A 1.36.0 não assegurava anúncio e ID nativo em toda entrega: payload, política/consentimento, mapa e tipo do campo condicionavam o resultado; o papel dedicado legado era Meta. A 1.37 não inventa identificadores nem reprocessa automaticamente os casos históricos. Referência operacional completa: `docs/PIPEDRIVE-1.37.md` dentro do instalador.

## 4. Instalação e prontidão

**Instalador final único:** SHA-256 `a7cd1c225bb9de76a5d1c3ad4b2184df47a6270856da902b8a268a4105ad20ad`. O mesmo arquivo foi usado no ciclo nativo e no Site-Teste.

| Prova própria | Resultado |
|---|---|
| Lint | 212 arquivos PHP aprovados; prova sintática separada da funcional |
| WordPress nativo descartável | WordPress 7.1.2, PHP 8.3.6 de 64 bits, MySQL 8.0.36-2ubuntu3 |
| Instalação limpa | Plugin ativado, estrutura pronta, finalização e repetição idempotente aprovadas |
| Atualização direta 1.36 → 1.37 | Plugin_Upgrader em processos distintos; sentinelas de dados, opções, escolhas Pipedrive, credenciais sintéticas e cursor preservadas |
| Comercial | 56 verificações de regras/prazos/validação |
| Fluxo Pipedrive | 33 verificações; APIs simuladas; criação, reuso, falhas após persistência e complemento |
| Origens nativas | 19 verificações; Meta, Google e LinkedIn, incluindo ID, anúncio ausente e rótulo Google |
| Slack | 17 verificações com fornecedor simulado; retorno à thread e guardas |
| Contrato | 9 verificações; contagens, perfil, catálogo e acesso |
| SDK de finalidades | 19 verificações; autorização, revisão, separação e leitura sem efeitos |
| Documentação nativa | 64 verificações; paginação, hashes, caminhos e acesso administrativo |

Total: **217 verificações nas sete suítes**, além de lint, ciclos e comparação dos SDKs. Ajustes do relógio de filas e isolamento dos registros ocorreram somente no banco descartável; não representam latência real dos fornecedores. Evidências sanitizadas estão em `evidence/` no fonte. Nenhum resultado da base foi reapresentado como teste novo.

**Site-Teste:** https://fator3-teste-mcp-1.dreamhosters.com/ . Antes: 1.36.0 ativa e operacional. Depois: **1.37.0 ativa, 15 etapas concluídas, zero falhas, finalização natural e guarda operacional sem pausa**. Home e REST responderam 200 nas sondas antes/depois, em requisição PHP nova. Escopo dessas sondas: origem interna do servidor; não certificam alcance externo de rede. Instalação: request `717407ff9b99b09db8654dc9`, operação de pacote `3266f1e820f520a3f9fcacce1ebbc49a`.

Documentos DOCUMENTACAO, RELEASE-1.37.0, AGENTES-1.37.0 e PIPEDRIVE-1.37 foram lidos integralmente pelo MCP. O último foi percorrido em três páginas de 25 linhas; todos tiveram texto e SHA-256 comparados aos bytes do instalador. Contrato remoto confirmou 8.2.0 e as cinco propriedades; descoberta confirmou 130 abilities da 1.37.0. A URL anônima do guia retornou 404 sem seu conteúdo. A primeira asserção esperava 403; a verificação seguinte confirmou o 404 e ausência do texto. Isso é proteção documental, não indisponibilidade da ajuda autenticada.

Pipedrive permaneceu desligado no Site-Teste. Nenhum teste comercial real, envio ao Slack, troca de credencial ou mudança em outro plugin foi executado ali. A ativação silenciosa do instalador foi seguida da conferência do ciclo de negócio do Core; apenas a confirmação do upload não foi tratada como prontidão.

## 5. Banco e reversão

Sem nova tabela ou coluna. Novos campos operacionais ficam no journal da fila Pipedrive e o retorno reutiliza a tabela de partes Slack. Defaults complementam o grupo existente sem ligar integrações, atividade ou homologação e preservam escolhas/listas anteriores. A fonte mantém os scripts de ciclo e as hashes das sentinelas.

Backup privado do banco no Site-Teste antes da troca: artefato `2cc43d616fed3ddb3d52ebe883599f46`, 17.148.272 bytes, SHA-256 `55b28cb4932757427a6f5c44d28efb5e9015675a73ee81847da4eeb59a604527`, 47.424 linhas. Foi preservado no servidor e não integra a entrega. Pré-imagem dos arquivos registrada pelo instalador: `df317c3c0be07242a145eed3`.

Reverter arquivos não desfaz efeitos externos. Para recuperação, preservar banco, arquivos privados, filas e guardas; preparar/drenar e reconciliar antes de retomar. Não desinstalar para atualizar e não restaurar silenciosamente um banco antigo sobre trabalho novo. O instalador informa database_effects_reversible=false. Nenhum rollback foi necessário.

## 6. Pendências e responsáveis

| Pendência | Responsável e condição de aceite |
|---|---|
| Campo longo respostas_formulario e campo ID nativo, mapas de serviços e tipos C1 da conta | Projeto Pipedrive fornece chaves/IDs reais e confere o catálogo antes de ativar |
| Homologação real de Pipedrive e retorno Slack | Projeto Pipedrive + dono/frota, exclusivamente CTOoffice/korvena.com.br: implantação autorizada, cookie/formulário de teste, homologacao=true temporário, releitura de título/empresa/campos/oportunidade/prazo/thread e remoção dos dados sintéticos pelo responsável |
| Limpeza dos quatro mapas legados korvena | Frota, somente após aceite do novo campo; não executada pelo Core |
| Casos Apex de 10/10 | Projeto Pipedrive fornece IDs completos e payloads/histórico para determinar a causa; sem evidência suficiente nesta rodada |
| Contrato 8.2.0 no Implantador | Responsável Implantador valida descoberta/edição; runtime 2.5.0 não fornecido, sem declaração de compatibilidade operacional |
| Publicação e distribuição na frota | Dono/frota confere SHA-256, publica instalador/relatório conforme regra comum e decide rollout; fonte permanece com o dono até decisão 89 |
| Aceites de produção da base ainda em acompanhamento | Responsáveis do item 20; permanecem independentes desta entrega |

O código solicitado está implementado e as provas próprias estão concluídas. Pendências de conta, produção e pacote alheio não foram declaradas resolvidas. Não houve novo escopo de Ads, gastos, BigQuery, Porter ou exportações sociais.

## 7. Credenciais

Nenhum segredo novo. Tokens existentes permanecem no mecanismo cifrado do Core. Os testes locais usaram somente marcadores sintéticos; as ferramentas da bancada bloqueiam transportes externos. O Site-Teste conservou a configuração/credencial anterior e o Pipedrive desligado. Fonte, instalador, evidências e relatório não contêm cookies, dumps, senhas reais ou tokens de hospedagem. O backup privado contém dados originais e não é distribuído.

## 8. Arquivos finais

| Tipo | Arquivo | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [base-site-core-fator3-1.37.0-instalador.zip](base-site-core-fator3-1.37.0-instalador.zip) | 1987998 | `a7cd1c225bb9de76a5d1c3ad4b2184df47a6270856da902b8a268a4105ad20ad` |
| Fonte | [base-site-core-fator3-1.37.0-fonte.zip](base-site-core-fator3-1.37.0-fonte.zip) | 2137408 | `2ac3c74e09c8d43cdd30e323b98fecf48979065458d65f7ca0f43eadba1944d7` |

Apenas o instalador é instalável; raiz `base-site-core-fator3/`. Fonte: raiz `base-site-core-fator3-1.37.0-fonte/`, código, build, testes, evidências sanitizadas, planejamento, impacto e cópia deste relatório anterior ao fechamento. Nenhum ZIP contém outro ZIP. O hash final do fonte consta somente neste relatório externo para evitar circularidade.

Complementos: `base-site-core-fator3-1.37.0-impacto-implantador-base.md` r2 e `base-site-core-fator3-1.37.0-plano.md` r3. O manifesto de arquivos descomprimidos e as evidências do instalador estão no fonte.
