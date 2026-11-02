# Entrega — Fator3 MCP LinkedIn 0.16.0

Revisão 1 — 02/11/2026. Rodada de implementação minor sobre 0.15.0. Status **apta-no-escopo-testado**, com adoção complementar pelo Core e homologação do fornecedor pendentes. Plugin `wp-mcp-linkedin-fator3`, basename `wp-mcp-linkedin-fator3/wp-mcp-linkedin-fator3.php`. Versão corrente desta entrega: **0.16.0**, instalada e ativa no Site-Teste.

## 1. De onde a versão entra

Instalação limpa e atualização **direta 0.15.0 → 0.16.0**, sem intermediária. Base aceita entregue anteriormente: instalador 345084 bytes, SHA-256 `e12b2b468b71c53d7ecc67c55f758ee1af5ba2b24082f9b12046c66944169e85`; fonte 2345227 bytes, SHA-256 `0e2ca16e82629d4c5f9324514415a5877f946d27455b906b9fc15ede09f21c96`. A base permaneceu imutável. Minor corresponde à nova extensão pública opcional; as correções anteriores e os contratos 1.0/1.1/1.2 são preservados.

Normas do projeto, documentação instalada, última entrega e impactos recebidos foram considerados. Entrada nova: Core 1.68.0, relatório/impacto revisão 2 e Pedidos core 369(d). A evidência mais recente do relatório Core registra instalação concluída, embora seu impacto ainda retenha a observação anterior de bloqueio. O inventário atual do Site-Teste confirmou Core 1.68.0 ativo; não foi presumido bloqueio vigente. Pedidos LinkedIn 18–21 foram mantidos e regressados.

## 2. Convivência e impacto pertinente

| Pacote | Versão examinada | Validação nesta rodada |
| --- | --- | --- |
| Fator3 Site Core | 1.68.0 | Runtime original integrado; consumidor Lead Reader real, descoberta, assinatura, ingestão, deduplicação e mapa local. |
| Fator3 MCP | 0.38.0 | Executor original, autorização, nova operação, erros e leitura integral dos documentos; ativo no Site-Teste. |
| Fator3 MCP Google | 0.26.0 | Ativo na bancada integrada e Site-Teste; fluxos existentes do Core na regressão. |
| Fator3 MCP Meta | 0.19.0 | Ativo na bancada integrada e Site-Teste; isolamento dos namespaces/registros preservado. |
| Fator3 MCP Pipedrive | 0.5.0 | Extraído e identificado; não ativado localmente por exigir PHP 8.3.36. Ativo, com versão/estado preservados, no Site-Teste. |

Hashes exatos dos instaladores recebidos constam em `evidence/release0160/inputs.json`: Core `afff3783f11aff3395e2a37cd3938958d93dfe1d01e5e566789f1333ccf134a8`; MCP `bc550c6573527a0d71bfa560036f83e7c8aec546f49d70b8e0095da5d303c1a5`; Google `f75031f2a430e099b7d3603d321993a049b4fb49606b9267144a59971eeebfe4`; Meta `f7629f48fffb774542a480fb55f29a151762b06a27b34c9a0c3188da3599451b`; Pipedrive `59e8c99d5bb8a54fcfeaba06c56d816b940a1fe97a7d6b473d13a252c6e5042a`.

Um único impacto técnico pertinente: **`wp-mcp-linkedin-fator3-0.16.0-impacto-base-site-core-fator3.md`**, revisão 3, situação aberto, `acao-necessaria`/`validacao-coordenada`, Pedidos core 369(d). Foi emitido no planejamento, atualizado na implementação e fechado como documento da entrega. Solicita adoção de consulta complementar autorizada e política de enriquecimento/retry pelo Core. A adoção da descoberta 1.2, pendente no impacto da 0.15.0, já está presente no Core recebido e foi validada. Não foi criado impacto apenas para informar versão aos demais pacotes.

Atualizar somente LinkedIn permite ao Core 1.68.0 aproveitar a decoração. O novo método complementar ainda precisa de consumo explícito pelo Core; não há bloqueio artificial para instalar esta versão. Nenhum código, documento central ou relatório recebido de Core/MCP/Google/Meta/Pipedrive foi alterado. A cópia adaptada de teste Core pertence exclusivamente à bancada deste fonte; o runtime Core utilizado veio do instalador original.

## 3. Mudanças e evidências

**Pedidos core 369(d), continuidade de LinkedIn 20/21 — implementado, validado-localmente e validado-wordpress.** A versão 0.15.0 não solicitava campos opcionais da campanha. `get_response` e `read_responses` agora projetam explicitamente `leadMetadataInfo`, além dos campos padrão documentados e metadados auxiliares. Nome decorado só é aceito quando ID coincide com a referência de campanha no lead e proprietário coincide com a conta autorizada; conta decorada, se presente, também precisa coincidir. Campos de resposta, consentimentos, identidade, versão e timestamp continuam preservados. A normalização textual da 0.15.0 permanece.

Campo aditivo `response.campaign` fornece contrato, conta, ID/nome, origem, situação, código e retryable. Nome ausente ou decoração inválida não descarta lead autorizado. Nome de decoração divergente/malformada é retirado do raw para impedir consumo incorreto por clientes antigos. Não se inventa nome a partir de ID. A leitura normal não faz consulta Ads nem exige nova concessão.

**Fallback público — implementado, validado-wordpress; adoção Core pendente.** Nova extensão `linkedin-lead-campaign/1.0.0`, anunciada por capabilities/descriptor, com método `resolve_campaign` e ability `linkedin/lead-resolve-campaign`. Entrada fechada vinculada a connection_id/account_id/form_id/response_id e revisões; recusa campaign_id arbitrário. A consulta relê o lead autorizado e retorna somente sua campanha. Se faltar decoração válida, exige escopo introspectado r_ads/rw_ads e consulta GET restrito à conta/campanha referenciada. ID/conta da resposta Ads são verificados. Dois GETs e uma introspecção no máximo, sem retry automático ou escrita comercial.

Permissão opcional `campaign_lookup` exige `responses`, seleção da conta em Ads e Leads e formulário concedido. Prévia/confirmação e CAS são obrigatórios para sua concessão; o painel apresenta opção/descrição em português e inclui a permissão na confirmação. Não amplia grants antigos. Serviço com usuário corrente 0 usa autorização atual do configurador, revalida revisões/seleção/principal antes/depois dos despachos e recusa dados após revogação concorrente. Nenhum uso de admin-options, token privado ou cache persistente como mecanismo de enriquecimento.

Diagnósticos distinguem `not_provided`, `not_applicable`, `not_authorized`, `stale_context`, `invalid_metadata` e `temporarily_unavailable`; falhas preservam código, efeito none e retryable. Erros não devolvem respostas pessoais. Documentação operacional e schema da campanha integram o instalador; contratos anteriores e 97 operações preservados, total **98**. Único schema preexistente alterado: enum aditivo de permissões em save-grant.

**Consumidor Core e contatos.** O Core original foi exercitado com HTTP sintético que só fornece decoração quando a projeção a solicita. Coleta com usuário 0 importou o nome; mapa local manteve precedência. Nova decoração sobre um lead histórico sem nome foi não bloqueante, sem duplicação nem sobreposição do contato original. O Core mantém sua proteção de conteúdo conflitante; completar nome histórico deve usar política própria de enriquecimento, não reimportação. O fallback novo foi provado no produtor/SDK/MCP; não foi atribuído ao runtime Core que ainda não o chama.

| Ensaio final | Resultado |
| --- | --- |
| Contraste da base 0.15.0, WP 7.1.4 | 2 verificações reproduzem ausência de projeção e método complementar. |
| Instalação limpa integrada, WP 7.1.4/PHP 8.3.6/MySQL 8.0.46 | 443 verificações funcionais, zero falhas; 39 dirigidas ao pedido novo e MCP. |
| Documentação pelo executor MCP 0.38.0 local | 39 verificações, zero falhas; 38 documentos/46 páginas, conteúdo e hash conferidos. |
| Atualização direta 0.15.0 → 0.16.0 | 10 verificações de preservação + 39 dirigidas, zero falhas. Tabelas de registros/histórico idênticas por hash, grants, cron e identidades de serviço preservados. |
| Consumidor Core 1.68.0 original | 37 verificações, zero falhas, com descoberta, recibo, ingestão, falhas, revogação e dados históricos. |
| Mínimo isolado WP 6.4/PHP 8.1.2 | 35 dirigidas + 135 nativas, zero falhas; 2 casos não aplicáveis por capacidades ausentes no ambiente. |
| Painel autenticado | 46 verificações DOM, zero falhas, jsdom 27.4.0/Node 24.22.1, HTML/JS reais e REST. Não equivale a inspeção visual em navegador. |
| Build/integridade | 35 PHP com lint; build repetido idêntico; 80 arquivos instalados idênticos ao ZIP nas matrizes; 98 schemas e 38 documentos. |
| Site-Teste | Troca aplicada, 9 autotestes locais, sondas 200, 38 documentos/40 páginas iguais ao instalador. |

As matrizes finais usam exatamente o instalador da seção 8 (exceto contraste da base, intencional). Nenhum erro de log próprio ou de acompanhante nas execuções finais. A regressão cobre OAuth/avisos, gestão de escritas, CAPI/aquisição/etapas, histórico, retenção, descoberta, paginação, perfis MCP e revogação. São WordPress/PHP/MySQL reais com fornecedor/e-mail sintéticos. Testes novos incluem HTTP 401/403/404/429/503, timeouts em lead/OAuth/Ads, malformed payload, grant revogado em três momentos, configurador sem autorização, revisão obsoleta e orçamento esgotado.

Na preparação, três testes antigos falharam porque fixavam o total em 97; a expectativa foi atualizada para a operação aditiva, mantendo todas as demais verificações. O teste DOM novo inicialmente procurou o identificador técnico na confirmação; foi corrigido para o texto público em português, e repetido. Não foram ocultadas falhas de runtime. Antes do fechamento, a candidata foi endurecida para recusar ID/nome Ads malformados sem warning. As provas finais posteriores passaram com o hash entregue. Não se afirma ausência universal de impacto fora da matriz descrita.

## 4. Instalação e prova de prontidão

Site autorizado: `https://fator3-teste-mcp-1.dreamhosters.com/`, canal WP MCP fator3-teste. Inventário anterior confirmou LinkedIn 0.15.0 e os cinco acompanhantes da seção 2 ativos. Foi substituído exclusivamente LinkedIn por `plugins/upload-base64`, com activate/overwrite=true, expected_slug=wp-mcp-linkedin-fator3, SHA-256 integral da seção 8, idempotency_key próprio, timeout inicial 15 s e posterior 20 s. Bytes locais validados; a publicação raw de frota não foi executada.

Operação `edcb97459b54cc2c2fc53e92b6922765`, backup `c1001f33b440d662bd8cb6a6`, request_id `aeee5d27aa5a4840768eec97`. Resultado applied=true, recovery_status=applied, versão 0.16.0 ativa. Sondas internas `/` e `/wp-json/` retornaram 200 antes/depois, com bypass de cache verificado. Não comprovam disponibilidade pública externa. A ativação foi silent_reactivation em processo PHP novo, sem ciclo de activation hook.

Nova requisição confirmou versão, armazenamento/criptografia prontos, zero conexões, state=ok, issues vazio e ausência de migração pendente. Nove autotestes aprovados, remote_homologated=false. `linkedin/lead-resolve-campaign` aparece com schema fechado e anotação de leitura remota. Documentação foi lida integralmente por linkedin/documentation, com expected_revision, next_offset, bytes e SHA-256: todos os 38 documentos coincidem com o instalador. Acompanhantes mantiveram exatamente versão/estado. Nenhum fixture, credencial real, lead comercial ou campanha foi criado nesse site.

Pronta para a atualização do plugin no escopo testado. A instalação não comprova disponibilidade dos produtos LinkedIn, autorização de contas ou comportamento real do fornecedor. Evidência detalhada em `evidence/release0160/site-results.json` e `site-documentation.json`.

## 5. Banco, preservação e volta de versão

Sem nova tabela, schema físico, migração, bucket ou cron. A auditoria existente pode registrar consultas; o limitador de quota existente continua registrando 429. Configuração de campaign_lookup é gravação explícita de grant, com revisão e principal; não ocorre na instalação. CAPI, recibos, filas, retenção, catálogo de descoberta, outbox e concessões anteriores foram preservados na atualização por hash de tabelas e provas funcionais.

Backup operacional deve incluir arquivos, banco e salts. Pré-imagem do MCP restaura arquivos/ativação, não desfaz banco ou efeitos externos; o recibo registra database_effects_reversible=false. Para voltar à 0.15.0, parar previamente o consumo da extensão nova e reconfigurar a concessão sem campaign_lookup conforme decisão do dono. A versão anterior não oferece o método nem solicita a decoração; dados existentes e recibos não devem ser apagados. Não restaurar banco antigo para completar nome nem repetir lead/webhook/conversão. A atualização não usa desinstalação.

## 6. Pendências de validação e responsáveis

- **Responsável Core:** adotar resolve_campaign quando o nome faltar, mediante nova autorização, e implementar enriquecimento/retry sem reimportar lead. Critérios estão no impacto individual, situação aberto. A adoção 1.2 já recebida não é reaberta como pendência.
- **Dono/frota:** homologar com conta/aplicativo/produtos reais Lead Sync e Ads, resposta sem decoração e leitura restrita de campanha; validar revogação/quotas e tratamento no consumidor. Site-Teste tem zero conexões LinkedIn; fornecedor real não foi chamado nesta rodada.
- **Frota:** publicar instalador/relatório na raiz raw autorizada, conferir bytes/hash antes da distribuição e seguir a regra de histórico. Não houve push, publicação nem envio de documentos a terceiros. O fonte fica com o dono.
- **Interface:** testes DOM com WordPress real cobrem o fluxo; inspeção visual manual em navegador não executada.
- **Pipedrive:** mínimo próprio impediu ativação local no PHP 8.3.6; coexistência ativa confirmada no Site-Teste não equivale a homologação de API/CRM. Nenhum contrato Pipedrive foi alterado.

Instalação limpa, atualização direta, mínimo próprio de runtime e leitura documental MCP foram exercitados; não são pendências. Nenhuma API garante nome quando associação/metadado não existe, e ausência diagnosticada não deve impedir receber o lead.

## 7. Credenciais e configuração do dono

Tela: Ferramentas → Fator3 MCP LinkedIn. Campos existentes: Token de acesso (Access Token), Client ID, Primary Client Secret, Refresh Token opcional e seleção de ativos/formulários. Nenhum segredo é retornado nas APIs ou incluído nesta entrega. Lead Sync depende do produto aprovado e escopo `r_marketing_leadgen_automation`; a consulta Ads complementar exige `r_ads` ou `rw_ads`, acesso à conta e seleção explícita em Leads/Ads. Não pressupõe rw_ads se r_ads for suficiente.

Na aba Concessões, selecionar consumidor e formulários/conta, manter responses e marcar a nova permissão de consulta de campanha quando desejada; simular, examinar e confirmar. Consumidor precisa descobrir a extensão e usar revisões públicas vigentes. A permissão não cria anúncios, publicações, contatos, webhooks ou conversões. A leitura decorada normal continua funcionando com o acesso Lead Sync já autorizado. Não é necessário fornecer nova credencial para instalar a versão; autorização real é necessária para usar APIs externas.

## 8. Identidade dos arquivos e fechamento

**Relatório externo canônico.** Identidades finais conferidas após o fechamento do fonte. A cópia interna é identificada como anterior ao fechamento, conforme o padrão do projeto.

| Artefato | Bytes | SHA-256 |
| --- | ---: | --- |
| [wp-mcp-linkedin-fator3-0.16.0-instalador.zip](wp-mcp-linkedin-fator3-0.16.0-instalador.zip) | 363060 | `beb018c0e89a6fcc25beff7d5e2955f606c78ea1cbc8148c17666dd4e9c50bc8` |
| [wp-mcp-linkedin-fator3-0.16.0-fonte.zip](wp-mcp-linkedin-fator3-0.16.0-fonte.zip) | 2466061 | `5218e5d7603e4e755ebba7bdd0cfbbfa175546d22b76d149ca1b42199675a3a1` |

Relatório canônico: `wp-mcp-linkedin-fator3-0.16.0-relatorio.md`. Complemento pertinente: [wp-mcp-linkedin-fator3-0.16.0-impacto-base-site-core-fator3.md](wp-mcp-linkedin-fator3-0.16.0-impacto-base-site-core-fator3.md), revisão 3. Fonte e instalador têm raízes únicas versionada/slug, respectivamente; nenhum ZIP contém outro ZIP. O fonte inclui código autoral, runtime byte a byte igual ao instalador, testes, evidências, plano, entradas e cópia deste relatório. Dependências externas e bancos/segredos de bancada ficam fora da entrega.

O instalador foi fechado antes do fonte e não foi modificado após a validação. O relatório interno é a cópia anterior ao fechamento do fonte; o externo completa a identidade final do ZIP fonte sem reabri-lo. Essa diferença técnica evita circularidade de hash e não muda resultados/evidências. Não substituir arquivos desta versão após entrega sem nova versão do plugin.
