# Entrega — Fator3 Site Core 1.51.0

Revisão 1 · 24/10/2026 UTC · Implementação dos pedidos **294 C1–C8 e 295**. Slug `base-site-core-fator3`; contrato administrativo **8.16.0**.

**Implementada e ativa no Site-Teste.** Novo Fator3 MCP Pipedrive 0.1.0 instalado com seus bytes originais. Contrato integrado confirmado e duas leituras reais concluídas na conta Pipedrive configurada. Operação administrativa restaurada para **desligada**, sem consumidores autorizados; entrega de leads continua pronta. Nenhuma implantação em produção ou publicação Git nesta rodada.

Este é o relatório externo canônico, concluído após o empacotamento do fonte. Não há falha conhecida aberta nos cenários executados. Isso não demonstra ausência universal de impacto nem encerra os aceites de fornecedor/produção indicados nas pendências.

## 1. Bases aceitas

Base direta Core **1.50.0**: instalador 2250902 bytes, SHA-256 `7021163d158b1a353e012823e14b611c17cb45d82125d3230784eb84f2b6b8ea`; fonte 4797482 bytes, SHA-256 `6a50e171b5042641f99aaea4a7c46c7b7ace51227450a7ee4cd0c2e564805a18`. Os 458 arquivos de runtime da base foram comparados byte a byte com o instalador antes da edição.

Lidos a aba Site Core recebida, o pedido conjunto MCP Pipedrive/Core, o impacto Pipedrive 0.1.0→Core revisão 1 e os relatórios atuais Meta/Pipedrive/LinkedIn. Aplicadas as instruções e padrão comuns **revisão 5, de 23/10/2026**, encontrados no fonte Meta 0.9.0. Cópias instaladas das normas atualizadas; documentos centrais e pacotes de outros mantenedores não foram alterados. Entradas, nomes, bytes e hashes constam em `evidence/1510/inputs.json` e `inputs/1510/`.

Plano e impacto técnico de validação coordenada foram registrados antes da implementação. Minor 1.51.0 e contrato 8.16.0 seguem o alvo explícito do pedido 294. Não há mudança de slug, basename, namespaces, Text Domain, Update URI ou das 145 abilities Core.

## 2. Convivência e encaminhamentos

| Pacote | Versão considerada e instalada | SHA-256 do instalador de referência |
|---|---|---|
| Fator3 MCP | 0.29.1 | `1b627aec5c24dc88f52eaf6a0d34367437d7f9e7b599f9f07850567fd57610e6` |
| Fator3 MCP Google | 0.19.0 | `d15868915e3fdf886d7e883a82d9d302df7242808fc94d45bf3e1857234759d1` |
| Fator3 MCP Meta | 0.9.0 | `e26aede1591426e06b8a69b5ad405cf13cb70c28d41b607346188c9d21a15662` |
| Fator3 MCP LinkedIn | 0.10.1 | `6182ea63bff6788f5d2637467e7ab29d58568e37283d6ece82d3e58ee41c13bc` |
| Fator3 MCP Pipedrive | 0.1.0 | `3366d83ca8908e407a0736812d30b8fa1506a8c1458a28cfb47eda6fd8f3c54f` |

Os runtimes novos Meta/LinkedIn/Pipedrive foram comparados com os fontes recebidos: respectivamente **43, 62 e 20 arquivos iguais**. Seus pacotes não foram modificados. Os quatro acompanhantes anteriores foram ativados juntos no laboratório; o cliente original Pipedrive foi exercitado contra o contrato real Core. No Site-Teste os seis pacotes Fator3 ficaram ativos juntos. DreamHost 1.0.0, WP Super Cache 3.1.4 e Yoast 28.7 foram preservados.

**Impacto recebido:** `wp-mcp-pipedrive-fator3-0.1.0-impacto-base-site-core-fator3.md`, revisão 1, pedido 294 C1–C8. A assinatura proposta foi implementada: hook, register_consumer, capabilities/status/request, envelopes e contexto esperados pelo CoreClient original. Registro, autorização, identidade, orçamento, saldo, revisão, incerteza e recuperação foram testados. Leitura integrada real comprovada no Site-Teste; escritas comerciais e aceites próprios do Pipedrive ainda exigem homologação coordenada. O arquivo recebido permanece histórico, sem reedição para anunciar atendimento.

**Impacto emitido:** `base-site-core-fator3-1.51.0-impacto-wp-mcp-pipedrive-fator3.md`, revisão 1, classificação validacao-coordenada. Apresenta o contrato novo, configuração explícita, códigos, revisão e critérios ao mantenedor Pipedrive/frota. Mantido como documento de planejamento porque não houve mudança substantiva no contrato proposto; resultados e atendimento estão neste relatório. Nenhum encaminhamento foi enviado a terceiros por ferramenta.

Meta 0.9.0 e LinkedIn 0.10.1 adicionaram verificações próprias de credenciais. Core não altera essas conexões nem absorve seus validadores. A fixture antiga de LinkedIn foi atualizada para o formato e scopes exigidos pelo pacote atual; o adaptador comercial passou sem alteração de contrato. Não foi identificada mudança obrigatória em MCP/Google/Meta/LinkedIn nas fronteiras examinadas, nem emitido impacto de simples anúncio/encerramento. Acompanhamento anterior do Core 1.50.0 permanece histórico; não se declaram concluídas tarefas alheias.

## 3. Mudanças por pedido e evidência

| Pedido | Resultado | Evidência |
|---|---|---|
| 294 C1 | Contrato PHP `pipedrive-api-client/1.0.0`, registro em plugins_loaded, cliente ligado ao provider/callback; registro não autoriza | Cliente original Pipedrive 0.1.0 em WordPress; registro e status real pelo MCP |
| 294 C2 | Host api.pipedrive.com fixo; caminhos /v1/ e /api/v2/; métodos GET/POST/PUT/PATCH/DELETE; corpo 64 KiB, timeout 20 s, sem redirecionamento ou retry | Recusas de URL/caminho codificado/traversal/merge/ids/credenciais/tamanho; métodos e argumentos de transporte conferidos; erro/timeout/exceção não liberam reenvio |
| 294 C3 | Orçamento operacao independente, GET 20/escrita 10, reserva atômica por dia UTC; teto padrão 3000 ajustável | Teto 40 em laboratório e conta real: duas leituras consumiram 40, terceira retornou orcamento_esgotado e remote_dispatched=false; entregas permaneceram em zero |
| 294 C4 | Saldo oficial e UTC por vínculo de credencial/conta; piso 3000 só para operação; 429 continua pausa compartilhada | Laboratório prova saldo baixo sem bloquear entrega e 429 bloqueando ambas; leituras reais retornaram 27354 e 27334, com horários, persistidos no diagnóstico |
| 294 C5 | f3base_pipedrive_operacao nasce false/[]/3000, catálogo operável e procedência; exige ativo e provider listado | A1 real recusou antes da autorização; escrita pela ability com revisão e auditoria; consumidor não listado/objeto forjado/usuário não administrador recusados |
| 294 C6 | Recuperação e geração integram guarda/revisão; gravações pertinentes compartilham trava com reserva/despacho | Preparar/retomar reais no laboratório; processo PHP novo ainda registra cliente e retorna core_em_recuperacao; duas conexões MySQL provam exclusão; mudança durante reserva recusa e devolve reserva |
| 294 C7/C8 | Estado em pipedrive-verificar e como-usar; docs/contratos; Core 1.51.0 e contrato 8.16.0 | Leituras reais dos dois diagnósticos, schemas, 169 documentos nativos; impacto técnico entregue |
| 295 | Removido mínimo Meta arbitrário de 100; usar_salva valida remotamente com avisos específicos, sem rotacionar segredo | 25 provas: três tokens Meta salvos curtos/sem EAA, normalização, identidade persistida, mesma cifra/revisão, recusa remota, conflito e autorização |
| 295 — apresentação | Avisos de prefixo, mínimo legado, espaços e quebras; ajuda atualizada; controles não entram em header | Renderização WordPress, DOM, leitura pelo redator original MCP, resposta/log sem marcadores secretos; fornecedor decide validade/escopos |

A Meta documenta que o comprimento dos tokens varia: https://developers.facebook.com/documentation/facebook-login/guides/access-tokens . A identidade é conferida por https://developers.facebook.com/docs/graph-api/reference/debug_token/ . O tamanho antigo deixou de decidir validade. O Core mantém limite de entrada e segurança de transporte; valores legados com controles internos são enviados apenas como parâmetros codificados para a Meta avaliar.

A normalização remove espaços/quebras nas extremidades ao usar ou gravar. Ler a credencial antiga não altera sua cifra. Identidade e avisos aceitos ficam vinculados à revisão exata; uma recusa não troca o token nem reutiliza identidade de outra revisão. Tokens sociais dos acompanhantes não foram alterados.

Diferença de runtime contra 1.50.0: **5 adicionados, 28 alterados, 430 idênticos, nenhum removido**. Inclui documentação e schemas gerados. As mudanças funcionais ficam no cliente/orçamento/saldo Pipedrive, coordenação das gravações pertinentes, normalização/verificação de credenciais e sua apresentação. Formulários e filas comerciais permanecem sob seus módulos existentes.

## 4. Instalação, prontidão e testes

| Prova própria | Ambiente | Resultado |
|---|---|---|
| Contrato 294 | WordPress 7.1.3 / PHP 8.3.6 / MySQL 8.0.46 descartáveis | 46 verificações aprovadas, transporte sintético; cliente Pipedrive original |
| Recuperação 294 | Mesmo laboratório, incluindo PHP novo com Core pausado | 6 verificações aprovadas |
| Credenciais 295 | Mesmo laboratório | 25 verificações aprovadas |
| Regressões credenciais 293 | Mesmo laboratório, redator MCP original | 32 + 9 verificações aprovadas |
| Execução/concorrência 292 | Mesmo laboratório | 11 + 4 verificações aprovadas |
| Revisão anterior, formulários, CRM, LinkedIn, Slack, release | Mesmo laboratório | 46 + 11 + 32 + 39 + 48 + 20 + 63 verificações aprovadas |
| Convivência de acompanhantes / adaptador LinkedIn | Pacotes atuais; HTTP sintético | 32 + 10 verificações aprovadas |
| Documentação nativa | Ability pública WordPress real | 169 documentos em 633 páginas, leitura integral/hash, autorização/confinamento e zero HTTP; 998 entradas de evidência |
| DOM de credenciais | jsdom, JavaScript final | 10 verificações aprovadas, incluindo aviso da credencial salva |
| Mínimos Core exatos | **WordPress 7.1.2 / PHP 8.3.6**, 64 bits / MySQL 8.0.46 | Instalação limpa final e 118 verificações de 294, recuperação, 295 e regressões 293 aprovadas |
| Instalação e atualização direta | WordPress 7.1.3 / PHP 8.3.6, processos novos | Instalação limpa e **1.50.0 → 1.51.0 por Plugin_Upgrader**; dados/configuração/cifras/procedência/cursor preservados; migração repetida idempotente |
| Build | PHP 8.3.6 | 235 PHP sem erro de sintaxe; instalador com 463 arquivos, CRC/bytes iguais ao fonte |

As contagens incluem verificações compartilhadas; não são total de casos únicos. O Pipedrive 0.1.0 declara mínimo WP7.1.3/PHP8.3.36. No laboratório menor foi carregado apenas como fixture do consumidor original, sem afirmar suporte/ativação abaixo do mínimo; sua instalação integrada foi feita no Site-Teste compatível. Testes locais bloqueiam HTTP e e-mail reais. Observações preliminares e ajustes de harness estão em `evidence/1510/preliminary-observations.md`.

**Site-Teste:** WordPress **7.1.3**, PHP **8.3.36**, Core 1.51.0 ativo. Atualização pelo instalador final, slug/hash esperados, activate=true/overwrite=true, operação `e47d9a9fd2e420333a086841`, pacote `c2ceef0a4ccdb6e3f1d6f9fdeb8bdcff`, backup `c446d86036f93f987600f3d0`. O ciclo completou **18 etapas, zero falhas**, finalizado e confirmado pelo executor em `1792807449` UTC.

Pipedrive 0.1.0 instalado depois, activate=true/overwrite=false, operação `5d152307f931cc570ac31f5a`, pacote `125c7ffea54f4beb97cdcb789a94ab00`. Home e /wp-json/ retornaram 200 antes/depois de ambas as instalações, com bypass comprovado; sondas de mesma origem não equivalem a prova de alcance público externo. Saúde final healthy=true e todas as 11 verificações locais verdadeiras.

**Prova real A1/A2/A3/A11:** antes de autorizar, status devolveu operacao_nao_autorizada e cliente registrado. Autorizado temporariamente só wp-mcp-pipedrive-fator3, status confirmou conta **14725895**, domínio fator3.pipedrive.com e teto 3000. Dois GET /v1/dealFields?limit=1 retornaram HTTP200. O segundo sob teto40 levou o consumo local a40; a terceira tentativa foi barrada sem despacho. Último saldo oficial **27334 em 2026-10-24T02:04:15Z**. Nenhum POST/PUT/PATCH/DELETE foi enviado ao CRM, nem criado lead/pessoa/organização/etiqueta de teste. Não há IDs comerciais a eliminar.

Estado final: operação **false, consumidores=[], teto3000**, consumo real conservado40/reservado0, sem zerar auditoria ou contadores. Valores da opção foram restaurados; a procedência administrativa e o histórico do teste permanecem. A configuração de entrega f3base_pipedrive conserva exatamente valor e revisão anteriores; diagnóstico verificado/entregando=true. Dois ZIPs temporários removidos com hash e backup. Nenhum MU-plugin/controlador QA foi instalado nesta rodada no ambiente compartilhado.

**Documentação pelo MCP externo:** índice Core com169 documentos; os quatro documentos novos foram lidos integralmente em seis páginas, incluindo PIPEDRIVE-OPERACAO em três páginas. Texto e SHA-256 iguais aos arquivos do instalador. Índice Pipedrive e seu contrato também lidos, este em três páginas com guarda de hash; texto/hash iguais ao pacote recebido. A prova integral dos demais documentos Core é nativa local, não se afirma releitura remota dos169.

## 5. Banco e reversão

Core não cria tabela nova. Adiciona f3base_pipedrive_operacao (configuração explícita), f3base_pipedrive_operacao_orcamento (reservas/contadores por dia/conta) e f3base_pipedrive_saldo_conta (até oito vínculos HMAC com saldo/UTC). Não guarda token nesse último estado. As options não usam autoload e são preservadas. O saldo observado não é aumentado por suposição ao virar o contador UTC; verificações existentes podem renovar evidência.

Coordenação por trava MySQL nomeada por instalação; CAS continua responsável por reservas/procedência. Configuração/credencial/estado/autorização pertinentes compartilham essa trava. Escrita concorrente ocupada recusa sem despacho, exigindo releitura. Código externo que grava SQL diretamente não participa desse protocolo. Resultado após início de HTTP é conservador: uma falha incerta não devolve consumo nem autoriza reenvio.

A instalação do Pipedrive cria suas duas tabelas de operações/diário e schema próprio, conforme relatório recebido. Não há migração de dados entre pacotes. Manter backup de banco e salts. Desativar Pipedrive ou restaurar o instalador Core1.50.0 verificado reverte arquivos/capacidade nova, mas não desfaz dados, auditoria, cotas ou efeitos externos. Não desinstalar/apagar options para forçar rollback. Nenhum rollback remoto foi executado.

## 6. Pendências e responsáveis

- **Frota/dono:** distribuir Core1.51.0 antes do Pipedrive em eventual site-porta de produção, conferir hashes e habilitar explicitamente o provider/conexão. Não houve push nem instalação fora do Site-Teste.
- **Mantenedor Pipedrive + frota:** homologar os aceites comerciais A5–A9 e repetição/recibo/diário com dados de teste autorizados, além do formulário/entrega real A14 com o acompanhante desligado. Core provou separação/bloqueios em laboratório e leitura/orçamento reais, não executou mutações comerciais do novo plugin.
- **Frota/CTOoffice:** repetir pedido295 na credencial real existente após implantar a versão, sem rotação desnecessária. Site-Teste não possui f3base_anuncios_meta_token salvo; por isso a aceitação Meta remota foi testada com respostas sintéticas, não com token real. Essa ausência foi conferida por leitura pública administrativa.
- **Revisor central:** revisar/encerrar editorialmente os pedidos294/295 e os critérios aplicáveis. Abas centrais não foram alteradas. A documentação original do Pipedrive ainda descreve a dependência anterior; este relatório registra o atendimento/limite integrado, sem modificar o pacote alheio.
- **Limites de prova:** sem inspeção visual integral em navegador, sem suporte multisite/runtime menor, sem repetição real de falhas de saldo/429/recuperação na conta compartilhada. Esses casos foram provocados no laboratório para preservar o ambiente de homologação. Provas de sete dias e demais pendências históricas do Core1.50.0 não são encerradas nesta rodada.

## 7. Credenciais e configuração do dono

Nenhuma credencial nova foi solicitada, exportada, substituída ou revogada. Token Pipedrive continua no Core; novo plugin não lê option privada nem faz HTTP próprio. Conta/domínio/usuário devem ser conferidos no status antes de autorizar operação. Para novo site, preparar credencial pela tela oficial e verificar o acesso/mapeamento existente.

Configuração de operação: ler schema/revisão em config-core-ler para f3base_pipedrive_operacao; simular e aplicar configuração explícita pelo gravador. Não elevar limite ou apagar saldo/contadores para contornar uma recusa. HTTP429 continua restrição da conta. Usar o fluxo de prévia/aplicação do Pipedrive para escritas, com reconciliação quando o efeito é incerto.

Pedido295: usar credenciais-verificar com nome, revisao_esperada e usar_salva=true. O Core consulta o fornecedor e registra identidade/avisos sem alterar a cifra salva. Campos novos continuam sujeitos a preflight e confirmação de mudança de identidade; não confirmar automaticamente só para vencer uma recusa.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `base-site-core-fator3-1.51.0-instalador.zip` | 2270123 | `7d6c9b8391e8f3a83a85dacbabea56cf93da6f6b04e7e195fcdceb4774f9f192` |
| Fonte | `base-site-core-fator3-1.51.0-fonte.zip` | 5022652 | `285317445bf2e4861952815479a6a90bff76889ee53f7cee84014ae0df4d73a8` |

Relatório: `base-site-core-fator3-1.51.0-relatorio.md`. Complemento técnico: `base-site-core-fator3-1.51.0-impacto-wp-mcp-pipedrive-fator3.md`.

Instalador é o único ZIP instalável, raiz base-site-core-fator3/. Fonte tem raiz base-site-core-fator3-1.51.0-fonte/, runtime idêntico, build, testes, evidências sanitizadas, entradas e cópia deste relatório anterior ao fechamento. Sem ZIP aninhado, banco, credenciais reais, cookies, logs brutos ou dependências de laboratório. Hash do próprio fonte é preenchido somente no relatório externo.

Destino raw previsto para publicação pela frota, **não publicado nesta rodada**: https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/base-site-core-fator3-1.51.0-instalador.zip . Conferir bytes servidos e SHA-256 antes de plugins/upload, com expected_slug=base-site-core-fator3. Fonte permanece com o dono conforme regra vigente.
