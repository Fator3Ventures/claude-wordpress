# Entrega — Fator3 MCP LinkedIn 0.10.1

Revisão: 1 · Data/hora: 2026-10-23T20:34:27-03:00 · Rodada: implementação do Pedido MCP LinkedIn 13 e correção da candidata 0.10.0.
Slug: `wp-mcp-linkedin-fator3` · Versão/build: `0.10.1` / `0.10.1`.
Status: **com-pendencias de homologação externa e aceite completo no Site-Teste**. Implementação concluída; aprovada no escopo dos testes descritos; 0.10.1 é a versão corrente desta entrega.

**Relatório externo canônico, após fechamento do fonte.** A cópia interna está identificada como anterior ao fechamento; somente este relatório externo contém tamanho e SHA-256 finais do ZIP fonte.

## 1. De onde esta versão entra

Instalação limpa e atualização direta da base aceita **0.9.0**, recebida com fonte e instalador. Instalador-base: 236.277 bytes, SHA-256 `d4857927ebacfca9321b79d13bc15f15c6969ae67047fd1793e509524b7a60f8`; fonte-base: 1.022.685 bytes, SHA-256 `26fc1c7573becdee2f904abffc04f20a6e5be63eb5e8e6f5b0e45d1c53701733`.

O incremento funcional começou em 0.10.0. Após sua aplicação no Site-Teste, a revisão encontrou uma lacuna: Refresh Token informado manualmente poderia renovar uma credencial cuja continuidade de membro não fosse comprovada. A correção gerou **0.10.1**, sem substituir silenciosamente o instalador já aplicado. A 0.10.0 não é necessária para atualizar os demais sites: a atualização direta 0.9.0 → 0.10.1 foi exercitada no laboratório.

Requisitos mantidos: WordPress ≥ 6.4; PHP ≥ 8.1.2 de 64 bits; extensões utilizadas pelo plugin e MySQL com travas nomeadas e InnoDB. Validados WordPress 7.1.3/PHP 8.3.6/MySQL 8.0.46 e WordPress 6.4/PHP 8.1.2-1ubuntu2.28. Site-Teste: WordPress 7.1.3/PHP 8.3.36, conforme inventário recebido nesta rodada. Identidades publicadas, slug, basename, namespaces, prefixos, Text Domain, Update URI e permissões administrativas permanecem.

## 2. Convivência e encaminhamentos

| Pacote | Versão considerada | Prova desta rodada |
|---|---|---|
| Fator3 Site Core | 1.50.0 | Fonte/contratos e instalador; integração limpa e atualização, árvore sem alterações |
| Fator3 MCP | 0.29.1 | Fonte/contratos e instalador; catálogo, executor, redação de saída, auditoria e leitura documental |
| Fator3 MCP Google | 0.19.0 | Instalador e relatório atuais; convivência nos dois laboratórios integrados |
| Fator3 MCP Meta | 0.8.0 | Fonte/contratos e instalador; matriz integrada completa |
| Fator3 MCP Meta | 0.9.0 observada ao final | Inventário, selftest 8/8 e leitura completa de CONFIGURATION, CONTRACTS e CHANGELOG instalados no Site-Teste; sem ZIP disponível para matriz local |

O Meta passou de 0.8.0 para 0.9.0 por outra operação durante o fechamento. Esta rodada não instalou nem modificou o Meta. A documentação observada mantém suas fronteiras e acrescenta a troca de identidade própria; não foi encontrada adaptação obrigatória no LinkedIn. A convivência remota observada não é apresentada como teste local do ZIP Meta 0.9.0.

Não foi identificado novo impacto que exija desenvolvimento, mudança de contrato ou decisão de outro mantenedor. Foram examinados Lead Reader, concessões e adaptador Conversions do Core, auditoria de principal de serviço, schemas/redação/descoberta/documentação do MCP e isolamento dos pacotes sociais. O LinkedIn mantém 81 operações; os campos de entrada novos são aditivos. Não há nova ordem obrigatória de troca dos acompanhantes.

Impactos recebidos conferidos, com respostas registradas somente neste relatório:

- **Meta 0.7.1 → LinkedIn**, revisão 4 recebida no fonte Meta 0.8.0: correção de isolamento concorrente já incorporada na LinkedIn 0.9.0. As 18 provas do Pedido 12 passaram novamente nos três ambientes finais; nenhum ajuste adicional foi necessário.
- **Core 1.48.0 → LinkedIn**, preservado no histórico Core 1.50.0: permanece a distinção entre regra de conversão de servidor/API e regra do Insight Tag. Contrato e diagnóstico continuam compatíveis; aceite comercial com regra correta segue pendente, sem modificar o Core.
- **MCP 0.29.1 → LinkedIn**: mantido o tratamento conservador da idempotência; a confirmação guiada não reutiliza uma chave de transporte entre fases diferentes. A documentação própria orienta omitir a chave opcional ou diferenciar as fases.

Nenhum documento do Core, MCP ou da regra central foi editado. Os recebidos foram preservados com hashes em `inputs/0.10.1/`. Não se emitiu arquivo de impacto apenas para anunciar a versão, responder ou encerrar pedido; o encaminhamento próprio histórico da base foi arquivado em `history/received-0.9.0/`. O fechamento do Pedido 13 no documento central cabe ao revisor responsável.

## 3. Mudanças e evidência

| Pedido exato | Problema | Mudança entregue | Evidência |
|---|---|---|---|
| Pedido MCP LinkedIn 13, parte 1 | Campos podiam receber o tipo errado de valor; nome sem orientação | Rótulos/ajudas em português, placeholder `membro · aplicativo`, regras de formato e mensagens solicitadas; validade passa a usar a comprovação do fornecedor | Casos de formato em `request013.php`, HTML/DOM e duas recusas remotas pela operação pública |
| Parte 2 | Token/par novo gravado antes de conferir | Introspecção antes de ativar; exige token ativo, Client ID correspondente, validade futura e os quatro escopos de leitura; erro preserva configuração ativa, agendas e concessões | Recusa de par, inatividade, outro app, expiração, escopo e rede; renovação e callback também conferidos |
| Parte 3 | Operador não via claramente o que estava salvo | Resumo público de identidade/comprovação, Client ID, validade e escopos; escopos de escrita destacados; nenhum segredo na projeção | Provas de projeção, inspeção sem alteração da autorização e DOM |
| Parte 4 | Troca de membro/app podia ser implícita | Simulação e confirmação opaca de 10 minutos, vinculada à candidata, administrador, revisão, identidade e registros dependentes; Lead Sync/CAPI reconfirmados na mesma tela | Confirmação adulterada/fora de revisão, usuário indevido, reconfirmação, rollback SQL e callback staged |
| Parte 5 | Renomear conexão invalidava agendas | `authorization_revision` e `credential_generation`; regravação atômica das agendas atuais e concessões vigentes junto com a conexão; histórico limitado a 20 entradas | Renomeação sem HTTP, rotação comprovada, preservação da seleção, trava independente e rollback |
| Patch 0.10.1 | Refresh Token manual não comprova continuidade do membro; sobreposição antiga poderia prevalecer | Remove a prova de vínculo ao trocar refresh manualmente, remove a sobreposição antiga no commit e retém como candidata a renovação de identidade não comprovada; aceite guiado antes de ativar | 33º caso do Pedido 13, repetido na integração, atualização direta e mínimo |

**Limite da API, documentado sem inventar identidade:** a introspecção oficial não fornece o nome do membro nem o nome de exibição do aplicativo. O Client ID, validade e escopos vêm da introspecção. O nome do aplicativo obtido do rótulo é identificado como declarado pelo administrador. O membro só é consultado via OpenID userinfo quando `openid` e `profile` já estiverem autorizados; o subject é comparável dentro do mesmo Client ID. Quando indisponível, aparece “Membro não informado pelo LinkedIn”; trocar token sem identidade comprovada exige confirmação. Não se considera o nome digitado uma prova de identidade. Referências oficiais consultadas em 23/10/2026: [Token Introspection](https://learn.microsoft.com/en-us/linkedin/shared/authentication/token-introspection) e [Sign In with LinkedIn using OpenID Connect](https://learn.microsoft.com/en-us/linkedin/consumer/integrations/self-serve/sign-in-with-linkedin-v2).

O commit da troca usa trava da conexão, revisão otimista, snapshot das agendas/concessões e transação InnoDB; chamadas externas acontecem antes da transação. Preserva ativos, formulários, usuários, versão de API e ativação, respeitando a nova identidade. Não reativa agenda antiga já pausada nem concessão incompatível. Alterações benignas preservam o vínculo de auditoria de serviço CAPI; mudança de identidade ou nova concessão invalida o vínculo anterior. Jobs já iniciados e cursores continuam sujeitos aos seus checkpoints e revisões; a correção de agendas não reescreve silenciosamente trabalhos comerciais antigos.

Callback OAuth agora guarda candidata cifrada temporária; o salvamento explícito a revalida e consome. A renovação de identidade diferente ou não comprovada conserva o acesso ativo e pede confirmação. Um par OAuth/refresh aceito comprova a continuidade subsequente, sem dispensar introspecção nem aceitar membro identificado como diferente.

Mudança pública: `save-connection` recebe `dry_run`, `confirmation`, `reconfirm_leads`, `reconfirm_conversions` e `use_pending_authorization`; `oauth-start` admite os escopos opcionais OpenID. Os outros 79 schemas de entrada permanecem iguais aos da 0.9.0. Runtime: três arquivos novos, 35 modificados, nenhum removido; schema SQL continua 2. As novas validações são deliberadamente mais restritas: uma nova credencial requer o par completo e os quatro escopos solicitados.

## 4. Instalação e prova da troca

Instalador fechado antes do fonte: 62 arquivos, 29 PHP, 27 documentos. Manifesto interno conferido integralmente; build reproduzido em diretório limpo com o mesmo SHA-256. A árvore `plugin/` do fonte é idêntica ao instalador. Arquivo principal: `wp-mcp-linkedin-fator3/wp-mcp-linkedin-fator3.php`.

| ID | Ambiente/cenário | Resultado | Evidência e limite |
|---|---|---|---|
| B09 | WordPress local com 0.9.0 | Reproduzidos campo trocado aceito, token inativo gravado sem introspecção e agenda quebrada após renomear | `base-reproduction/reproduce013.json`; observação da base, não aprovação da nova versão |
| L1 | WP 7.1.3/PHP 8.3.6, limpa integrada | 167 regressões + 18 Pedido 12 + 33 Pedido 13 aprovadas; zero falhas | `patch-integrated/`; Core 1.50.0, MCP 0.29.1, Google 0.19.0, Meta 0.8.0 |
| L2 | Mesmo ambiente, atualização direta 0.9.0 → 0.10.1 | 174 regressões + 18 + 33 aprovadas; dados, opções, ciphertext e progresso preservados | `patch-upgrade/`; novo processo e runtime exato |
| L3 | WP 6.4/PHP 8.1.2 isolado, sem acompanhantes | 133 regressões + 18 + 32 aprovadas; três não aplicáveis | `patch-minimum/` e `patch-minimum-013/`; duas provas dependem da Abilities API nativa e uma do MCP ausente |
| D1 | Executor MCP real nos dois laboratórios integrados | 28 verificações em cada: 27 documentos, 34 páginas; 56 verificações aprovadas | `mcp-docs080.json`; inclui índices/revisões e leitura completa, sem sessão HTTP remota |
| U1 | DOM com WordPress real e REST autenticado | 13 verificações aprovadas, nenhum erro JS | `patch-ui/ui010.json`; jsdom 27.4.0, sem inspeção visual completa de navegador |
| I1 | Integridade dos acompanhantes em L1/L2 | Oito comparações exatas contra os quatro ZIPs recebidos | `companion-integrity.json`; nenhum patch nos acompanhantes |
| S1 | Site-Teste, 0.9.0 → 0.10.0 → 0.10.1 | Ambas aplicadas; final ativa; inicial e REST 200 antes/depois; selftest 8/8 e status ok | `site-test.json`; reativação silenciosa em PHP novo, não ciclo completo de activation hooks |
| S2 | Site-Teste, operações públicas | Segredo e Client ID em campo de token recusados com a mensagem solicitada; lista final vazia | Um teste de formato na 0.10.0 e outro na 0.10.1; não representa configuração real persistida |
| S3 | Site-Teste, documentação da 0.10.1 | 27 documentos, 28 páginas e 226.505 bytes lidos integralmente, iguais ao instalador | `site-docs.json`; manifesto remoto também coincide |

Total funcional final: **626 verificações aprovadas, três não aplicáveis e zero falhas**, além de 56 verificações documentais e 13 DOM. Não inclui a reprodução da base nem o auxiliar local da candidata. Os logs finais dos laboratórios não registraram avisos/erros PHP próprios ou dos acompanhantes. HTTP de fornecedor e e-mail foram interceptados nos testes; não foram enviadas conversões, publicações, assinaturas ou notificações comerciais reais.

O executor do Pedido 13 no mínimo inicialmente contabilizava o teste condicional de MCP ausente como aprovado. Foi corrigido para `nao-aplicavel` e reexecutado: o arquivo canônico é `patch-minimum-013/request013.json`. O resultado anterior foi preservado, sem somá-lo de novo. Ajustes preliminares de runtime, fixtures e infraestrutura estão separados em `preliminary-observations.json`; os totais acima são apenas das execuções finais.

Site-Teste: `https://fator3-teste-mcp-1.dreamhosters.com/`. A troca usou os bytes exatos do ZIP por `plugins/upload`, `expected_slug=wp-mcp-linkedin-fator3` e o SHA-256 da seção 8. Não houve publicação no repositório nem uso de URL raw nesta rodada; a verificação de uma futura URL raw cabe à frota antes da distribuição.

- Primeira troca: operação `528be7b1e5583baa6144a1ef`, pacote `3f8687303f5b10aa81e812246aff77c6`, backup de arquivos da 0.9.0 `f6586deb070bfa52312bd89c`.
- Troca final: operação `73250c039d737a11a3de994b`, pacote `8bf777e3904f70cc80950b233a25377a`, backup de arquivos da 0.10.0 `b947e48650ddb2420af8fdd9`, `applied=true` e `active_after=true`.
- Manifesto instalado: SHA-256 `d0da40959f95b45fefb7abd13188989a67008de6f2ce541c81df6352d8f6467c`, igual ao final local.
- Prontidão: `linkedin/status` sem parâmetros retorna versão 0.10.1, `state=ok`, `issues=[]`, storage/crypto prontos, zero conexões, zero jobs ilegíveis, `service_audit.central_registered=true` e manutenção agendada. `linkedin/selftest` retorna oito verificações locais `ok`; `remote_homologated=false` e `external_checks=not_run`.
- Documentação: `linkedin/documentation` com `document=index`; continuar cada documento por `next_offset`, mantendo `expected_revision`. A leitura final foi completa e conferida por conteúdo, bytes e SHA-256. Os diferentes totais de páginas locais/remotas decorrem do tamanho de página utilizado.

Estado final observado: Core 1.50.0, MCP 0.29.1, Google 0.19.0, Meta 0.9.0 e LinkedIn 0.10.1 ativos. Não ficaram conexões/fixtures sintéticas nem ferramenta temporária remota desta rodada. Os backups e registros normais das operações permanecem no mecanismo MCP; não se afirma ausência de escrita de auditoria. As sondas foram internas, na mesma origem, com PHP novo/cache bypass; não comprovam acesso público externo ou prontidão comercial.

## 5. Banco e volta de versão

Schema SQL permanece 2, sem migração destrutiva. A instalação não cria conexão, concessão, assinatura ou seleção comercial. Novos campos de revisão, comprovação e histórico ficam nos registros cifrados próprios. Candidatas OAuth/renovação usam bucket temporário com validade de dez minutos e limpeza na manutenção. Histórico de alterações fica limitado a 20 entradas.

Salvar uma conexão regrava de forma atômica apenas o conjunto pertinente de agendas atuais e concessões vigentes, com CAS e rollback em erro. Pausas, filtros, ativos, consumidores, permissões, opções e progresso mantêm seus significados. Uma troca manual de refresh incorpora os valores efetivos e remove a sobreposição antiga no mesmo commit. Não se transferem automaticamente a nova identidade os trabalhos já emitidos com checkpoint antigo.

A atualização direta foi validada com dados semeados na 0.9.0. A operação remota fornece backup dos arquivos do plugin, não backup completo do banco; `database_effects_reversible=false`. Para voltar à base, use o instalador 0.9.0 verificado ou o primeiro backup, após avaliar o estado atual. Restaurar a segunda preimagem retorna apenas à 0.10.0. Restaurar arquivos não desfaz registros de conexão, agendas/concessões, auditoria ou efeitos externos. Não apagar tabelas/opções para reverter. A versão antiga perde as proteções novas; eventual retomada deve revisar credencial, concessões e agendas. A reversão operacional do banco não foi exercitada remotamente.

## 6. O que permanece pendente

1. **Aceite completo do Pedido 13 no Site-Teste.** A revisão automática de aprovação rejeitou a criação de `wp-content/mu-plugins/f3-linkedin-qa-0100.php`: “A gravação cria um MU-plugin PHP persistente e uma habilidade pública no Site-Teste, fora do plugin LinkedIn autorizado; isso amplia o escopo e pode alterar o comportamento e a superfície de execução do site.” O arquivo não foi criado; sua ausência foi conferida. Não houve tentativa de contornar o bloqueio. As 30 verificações do auxiliar passaram somente no laboratório da candidata 0.10.0 e não contam como aceite remoto nem como matriz final 0.10.1. Foi possível concluir as verificações remotas existentes de instalação, saúde, formato e documentação. Os cenários de token inativo, troca guiada com agendas/concessões e resumo real ainda exigem homologação autorizada pelo responsável do ambiente/dono.
2. **Credenciais e fornecedor reais.** O Site-Teste tem zero conexões. Membro/app/escopos efetivos, recusa de par real, renovação real, disponibilidade de OIDC e produtos aprovados não foram homologados. O dono deve fornecer uma conexão/ativos de teste autorizados pelo fluxo administrativo. Nomes que a API não retorna continuarão explicitamente declarados ou indisponíveis.
3. **Aceites comerciais anteriores.** Conversão recebida/contada, referência de serviço no Registro em ctooffice, preenchimento só pela tela e regra API correta permanecem nas pendências 20, 92 e 116 citadas no pedido recebido. Não foram encerradas por fixtures ou por esta release.
4. **Meta 0.9.0.** Coexistência e contratos instalados observados; a matriz local com o ZIP exato não foi executada porque esse pacote não estava disponível nas fontes consultadas. Responsável pela próxima integração deve incluir o instalador quando disponibilizado; não há falha observada nem adaptação obrigatória identificada.
5. **Interface e distribuição.** Testes DOM não substituem conferência visual em navegador pelo operador. Nenhuma atualização da frota, push, publicação raw ou envio a mantenedores foi feito. Distribuição cabe à frota no escopo autorizado; fechamento do Pedido 13 cabe ao revisor central. Entrega mantém status `com-pendencias` por essas provas ausentes.

## 7. Credenciais e configuração do dono

Ferramentas → Fator3 MCP LinkedIn → Conexão. Usar `membro · aplicativo` como nome, com ajuda sempre visível. O membro é o perfil que gerou o token; App name fica em LinkedIn Developers → My apps → aplicativo → Settings. Client ID e Primary Client Secret vêm de Auth → Application credentials; o número do aplicativo é o trecho numérico da URL, não o Client ID. Access Token vem do Token Generator. Não há valores secretos neste relatório.

A política solicitada exige Access Token com pelo menos 100 caracteres e sem espaços, diferente do Client ID e da chave; Client ID alfanumérico e não apenas numérico; Primary Client Secret com menos de 100 caracteres e diferente dos outros campos; App ID só com dígitos; Refresh Token diferente do Access Token. O limite de 100 é regra de validação pedida pelo dono, não garantia universal de formato do fornecedor. A validade informada cede à introspecção.

Para gravar credencial nova, informar token e par Client ID/Primary Client Secret válidos. São obrigatórios `r_ads`, `r_ads_reporting`, `r_organization_admin` e `r_organization_social`. Escopos adicionais de escrita e produtos aprovados continuam necessários para cada operação (`rw_ads`, `w_organization_social`, `rw_organization_admin`, `rw_conversions`, conforme o caso). Lead Sync e Conversions mantêm concessões separadas; selecionar explicitamente contas, Páginas, formulários, consumidores e regra de servidor API. Não confundir regra do Insight Tag com Conversions API.

Token manual continua sendo o padrão; OAuth/OpenID é opcional. Para mostrar membro via userinfo, o aplicativo precisa estar apto e já ter `openid profile`. Ausência desses escopos não permite inventar identidade. Ao mudar membro/app ou quando não for possível comprovar continuidade, usar “Trocar identidade e regravar agendas”: revisar a simulação, reconfirmar concessões ativas na mesma tela e enviar a confirmação com a revisão atual. Renovação por Refresh Token depende de aprovação do produto no LinkedIn.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-linkedin-fator3-0.10.1-instalador.zip](wp-mcp-linkedin-fator3-0.10.1-instalador.zip) | 254066 | `6182ea63bff6788f5d2637467e7ab29d58568e37283d6ece82d3e58ee41c13bc` |
| Fonte | [wp-mcp-linkedin-fator3-0.10.1-fonte.zip](wp-mcp-linkedin-fator3-0.10.1-fonte.zip) | 1207818 | `518b83da12940f044edd99e4223348f4ef01011dc57c7c40181793c473b6d0cc` |

Relatório: `wp-mcp-linkedin-fator3-0.10.1-relatorio.md`. A cópia interna permanece anterior ao fechamento e não contém o hash do próprio ZIP. O relatório externo preenche a identidade após fechar o fonte uma única vez; os resultados funcionais e as pendências são os mesmos. Não foi emitido impacto novo nesta rodada.

Para reprodução, consultar `README.md` e `tools/lab-release0101.example.json` no fonte. `evidence/release0101/` contém provas sanitizadas; `inputs/0.10.1/input-hashes.json` registra os pacotes/documentos recebidos. Instalador e fonte têm raiz única e não contêm ZIP aninhado. Somente o instalador deve ser enviado ao WordPress.
