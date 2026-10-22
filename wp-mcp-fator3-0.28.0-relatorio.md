# Entrega — Fator3 MCP 0.28.0

Revisão 1 · 22/10/2026 · America/Sao_Paulo · Rodada de implementação.
**Pedido MCP 65 implementado e validado no Site-Teste**, em integração com LinkedIn 0.7.0. Pendências externas/editoriais delimitadas na seção 6.

Relatório externo canônico. A cópia dentro do fonte é identificada como anterior ao fechamento; tamanho e hash do próprio fonte são completados somente aqui.

## 1. Bases aceitas e identidade

Base imediata **0.27.0**, aceita na aba `Fator3 MCP(5).md`; atualização direta, sem versão intermediária. Base preservada: instalador 846316 bytes, SHA-256 `fcf5ad0099b9490abfb8e9ea6ef83c769cad053e2ee75712efce50e219f62bc1`; fonte 3376082 bytes, SHA-256 `c541e4cbe93b9fbef6608cf048fcb6abce69e844c32da0d6adba23af130d743d`.

Preservados nome Fator3 MCP, slug/pasta/provider `wp-mcp-fator3`, basename `wp-mcp-fator3/wp-mcp-fator3.php`, namespaces, Text Domain, Update URI, endpoints e IDs existentes. Incremento minor conforme normas comuns revisão 4. Nova ability aditiva `audit/get-service-operation`; contrato humano e três metatools existentes conservados.

Mínimos comprovados nesta rodada: **WordPress 7.1.2 e PHP 8.3.6 de 64 bits**. Laboratório principal WordPress 7.1.3/PHP 8.3.6/MySQL 8.0.46; Site-Teste WordPress 7.1.3/PHP 8.3.36. Instalação limpa usa somente MCP em banco e diretório novos, não reset do site compartilhado.

Pedidos atuais, relatórios, impacto LinkedIn revisão 3 e identidades recebidas estão em `docs/entradas/0280` e `evidencias/0280/entradas.json`. Dois anexos inicialmente indisponíveis foram recuperados como arquivos externos canônicos: relatório Meta 0.5.0 e impacto LinkedIn 0.7.0. O impacto coincide com a cópia interna; o relatório Meta completa hash/bytes do fonte, conferidos. Documentos centrais não foram alterados.

## 2. Convivência e encaminhamentos

| Pacote | Laboratório integrado e Site-Teste | Consequência nesta entrega |
|---|---|---|
| Fator3 Site Core | 1.47.0 | Mantém consumidor site-core-conversions, fila e contrato site-conversion-delivery/1.0.0. Nenhuma mudança requerida. |
| Fator3 MCP Google | 0.17.0 | Versão/ativação preservadas; não recebe contrato novo. |
| Fator3 MCP Meta | 0.5.0 | Metadados de apresentação atuais consumidos do registro nativo. Nenhuma tradução duplicada ou mudança de domínio. |
| Fator3 MCP LinkedIn | 0.7.0 | Descritor, introspector, evento e leitor públicos integrados ao consumidor central real. |
| Fator3 MCP | 0.27.0 → 0.28.0 | Único pacote atualizado no Site-Teste por esta tarefa. |

Impacto pertinente: **wp-mcp-fator3-0.28.0-impacto-wp-mcp-linkedin-fator3.md**, revisão 2, `validacao-coordenada`, resolvido no escopo técnico. Revisão 1 foi escrita antes do código e aceitou o handshake/recibo da contraproposta LinkedIn. Revisão 2 registra implementação e prova conjunta. LinkedIn 0.7.0 pode preceder o MCP; sem ele o MCP conserva suas funções próprias, e a integração de serviço fica indisponível. Não há adaptação requerida do Core.

Não foram identificados outros impactos técnicos nas fronteiras examinadas. Implantador não recebido: não avaliado, sem risco específico novo a encaminhar. Nenhum acompanhante, repositório, documento central ou outro site da frota foi modificado. WP Super Cache 3.1.4, Yoast 28.7 e DreamHost Panel Login 1.0.0 permanecem ativos e nas versões iniciais.

## 3. Mudanças e evidências por pedido

**MCP 65 / MCP LinkedIn 8(d).** Antes, o SDK de conversões com usuário zero persistia apenas diário local, com `service_principal_unsupported`. Agora `mutation-service-audit/1.0.0` admite o provedor no bootstrap PHP, valida o evento integral contra `f3_linkedin_introspect_service_grant` e confirma o digest efetivamente persistido. O LinkedIn retorna **central_audit=recorded** para as operações comprovadas.

O descritor fechado tem contrato, provider, event_contract, event_hook, reader e introspector. Origem dos pontos de entrada públicos, provedor/versão, leitor somente leitura, schema e decoração de política são conferidos. Não há registro/emissão/introspecção remotos, callback recebido da rede ou acesso a tabelas/classes privadas do LinkedIn no código de produção.

Referência estável por site/provedor/principal/operação, sob lock. `principal_type=service`, `user=0`, consumidor e concessão/revisão opacos, mesmo com administrador incidental. Somente metadados técnicos e hashes; nenhum snapshot, payload, contato, identificador de conta/regra ou segredo fica no registro central. Campo extra, digest/identidade divergentes ou diário sem prova são recusados. Duplicata exata não regrava a referência.

`audit/get-service-operation` recebe provider, consumer_id, principal_ref, grant_revision e operation_id. Exige manage_options, política central e permissão no leitor do domínio; este revalida proprietário da concessão, perfil de origem quando houver, conexão/ativo/regra e escopos localmente comprovados. Outro administrador não herda acesso por conhecer uma referência. Saída antes/depois usa projeção técnica fechada, com hash conferido; incerteza retorna after=null. O schema de saída mantém o envelope extensível comum do MCP; os campos de serviço estão especificados na documentação instalada.

Registro administrativo mostra “Serviço — site-core-conversions”, referências opacas e botão “Consultar recibo de serviço”. Escopo nativo temporário permite a consulta administrativa sem conceder ou reativar perfil MCP; mantém os gates do domínio e fecha ao retornar. Concessão revogada, revisão/escopo/autoridade inválidos ou leitor ausente bloqueiam detalhes e recibo atual, preservando a referência histórica. Não há consulta ao LinkedIn durante leitura, renovação, backfill, outbox ou reenvio para reparar auditoria. Revogação remota depende de observação pelo domínio.

**Itens já aceitos:** 63/64 não foram reabertos. A aba recebida confirma conector Claude real criado/autorizado pelo dono em 22/10/2026, três ferramentas respondendo e posterior exclusão/revogação. Esse é aceite recebido, não teste externo novo desta rodada. B22/ChatGPT já estava encerrado. Rotinas OAuth não foram alteradas.

## 4. Instalação, validação e estado final

Instalador final: **853885 bytes**, SHA-256 **d1d297d8aaee0e5188b92fe9eae20a9dcc07e79d639baae25f267bf64f7243b0**. Exatamente esses bytes foram usados nas duas instalações limpas, atualização direta e Site-Teste. São 459 arquivos, 450 PHP válidos; dez caminhos de runtime adicionados/alterados e nenhum removido. Reconstrução a partir do fonte deve reproduzir os mesmos bytes; verificação obrigatória no fechamento.

| Prova própria | Resultado e limite |
|---|---|
| Serviço integrado, WordPress nativo | 54 verificações, zero falhas; fornecedor simulado, consumidor MCP e domínio LinkedIn reais. Inclui identidade zero/incidental, digest/recibo, perfil dos dois leitores, outro admin/assinante, perda de escopo, leitor ausente, SQL indisponível, replay/incerteza, painel e retenção. |
| Contrato humano | 32 regressões, zero falhas; painel e HTTP MCP, antes/depois, perfil/conexão/ativo e idempotência. |
| Apresentação | 8 verificações, zero falhas; rótulos nativos, descoberta e painel. |
| Documentação local | 25 verificações, zero falhas; 24 documentos completos e leitor público de serviço. |
| Atualização direta 0.27.0 | 19 verificações, zero falhas; oito respostas de workers antes/depois, credenciais/perfis, validade de tokens, configurações false/vazias, backups, idempotência e SQL pendente preservados; 459 arquivos idênticos. Rollback apenas simulado. |
| Instalação limpa isolada | WordPress 7.1.3 e 7.1.2/PHP 8.3.6, ativação nativa e leitura em processo novo; sem acompanhantes; marcador cron confirmado. |
| Site-Teste | 35 verificações aprovadas; quatro POST sintéticos, zero chamadas reais ao LinkedIn; MCP real confirmou recorded sob usuário zero/incidental e leu recibos antes da limpeza. |
| Documentação remota | 24 documentos, 26 páginas; conteúdo completo, bytes e hashes iguais ao instalador. |
| Navegador | Registro filtrado por operação, principal/concessão e link próprio; recusa após limpar concessão; viewport/documento 1363 px, sem transbordamento horizontal da página. |

Contagens são execuções por suíte, com cenários comuns; não representam casos únicos somáveis entre ambientes. Evidências: `evidencias/0280/`; testes/build em `tools/release0280`. As provas anteriores incluídas no fonte são históricas. Não houve nova homologação comercial das APIs sociais nem revisão integral dos logs privados do site.

Instalação em `https://fator3-teste-mcp-1.dreamhosters.com/`, via `plugins/upload-base64`, slug/hash esperados, overwrite e ativação. Operação **72bd8c08bbcfc8de45104e00**, pacote **ab473c9a321d8dbf39b41e35a133b33a**, backup da 0.27.0 **210a2dce49261d5a80464336**. Aplicada na primeira chamada, ativo antes/depois; `/` e `/wp-json/` HTTP 200 antes/depois com prova de PHP novo/desvio de cache. Reativação silenciosa em worker independente, não equivalente a ciclo de ativação limpa nem prontidão comercial.

O auxiliar temporário `f3-mcp-0280-qa.php` exigiu administrador e configuração LinkedIn vazia, interceptou rede/e-mail e removeu seus dados próprios. Foi excluído com guarda de SHA-256; backup administrativo e57f4676a88de0ba605bbce7. A ability temporária ficou indisponível. ZIP temporário também excluído. Conexões/concessões/diários sintéticos do LinkedIn remanescentes: zero; referências centrais sintéticas e backups administrativos permanecem para auditoria. Nenhum simulador de consumidor central foi instalado no site.

Estado final: MCP 0.28.0 e quatro acompanhantes ativos; system/health.healthy=true após limpeza. Configurações projetadas sql_retention, file_bytes, enabled e update_channels iguais antes/depois. LinkedIn: domain_implemented=true e central_registered=true; capacidades indicam service_provider_registered, enquanto recorded é comprovado por evento. Documento novo: `system/guide` sem argumentos lista os IDs; use document=mutation-service-audit ou release-0280, byte_limit até 32768, continue pelo cursor/expected_sha256. Ajuda usa allowlist local, sem fornecedor.

## 5. Banco, preservação e reversão

Sem tabela, migração, credencial, agenda ou fila nova. Referências ficam no bucket audit existente, com user=0 e kind=service_mutation_reference; retenção administrativa normal com prévia/confirmacão. Retenção remove referência, não o diário do LinkedIn nem o efeito externo. Falha de gravação não confirma recorded nem transforma resultado confirmado/incerto em permissão de reenvio.

Atualização não reautoriza ativos ou altera concessões. Prova local preservou credenciais e validade, perfil, backups, configurações e operações pendentes. O Site-Teste preservou configurações e versões dos acompanhantes; o teste de domínio criou somente configuração sintética temporária sob guarda de vazio.

Backup da instalação cobre arquivos, não snapshot transacional do banco; database_effects_reversible=false. Voltar à 0.27.0 desabilita consumo/leitura de serviço e preserva o armazenamento existente. Não desfaz conversões, não autoriza reenvio e não recupera dados já removidos por retenção. Preserve banco e salts com o backup operacional; não desinstale para simular rollback. Reversão remota não aplicada.

## 6. Pendências e responsáveis

| Item | Estado / responsável |
|---|---|
| MCP 65 / LinkedIn 8(d) | Implementação e aceite técnico integrado comprovados. Dono/revisor confere os artefatos e encerra editorialmente as abas centrais. |
| Conversão comercial real, produto/escopos e regra API | Fora do aceite sintético; dono/Core/LinkedIn mantêm os aceites externos existentes. Nenhum envio real foi feito. |
| Publicação e demais sites | Dono/frota: distribuir bytes versionados com expected_sha256 e expected_slug; nenhum push ou instalação na frota nesta tarefa. |
| Implantador e mínimos dos acompanhantes | Não homologados por este pacote. São responsabilidades dos respectivos mantenedores; mínimos próprios do MCP foram executados. |

Nenhuma falha conhecida nas verificações finais executadas. O contrato vale para a combinação de versões e interfaces descrita; não é registro genérico de qualquer provedor PHP. Não há pendência de B22/CIMD reaberta nesta entrega.

## 7. Credenciais e configuração

Nenhum campo secreto novo. A atualização não concede acesso. LinkedIn mantém conexão/token e concessão explícita de site-core-conversions em Ferramentas → Fator3 MCP LinkedIn; precisa de conta/regra CONVERSIONS_API selecionadas e prova válida dos escopos. Não recrie credenciais ou perfis para atualizar MCP. Para agentes com perfil personalizado, autorize audit/get-service-operation e linkedin/get-service-write-operation quando o acesso ao recibo for desejado; manage_options e propriedade da concessão continuam obrigatórios.

Não há segredos reais, cookies, banco, capturas pessoais ou fixture ativa nos ZIPs. Valores sintéticos aparecem apenas nos testes de desenvolvimento, fora do instalador.

## 8. Arquivos finais e integridade

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-fator3-0.28.0-instalador.zip | 853885 | d1d297d8aaee0e5188b92fe9eae20a9dcc07e79d639baae25f267bf64f7243b0 |
| wp-mcp-fator3-0.28.0-fonte.zip | 3543405 | 1b446b52c649e791407484702df5ddf280cb8e21b7b4d0a5f6508f4b304111ed |

Apenas o instalador é instalável, raiz wp-mcp-fator3/. Fonte tem raiz wp-mcp-fator3-0.28.0-fonte/, código, build, testes, evidências e relatório interno anterior ao fechamento; nenhum ZIP contém outro ZIP. Complementos: este relatório externo canônico e wp-mcp-fator3-0.28.0-impacto-wp-mcp-linkedin-fator3.md, revisão 2. Fonte fechado uma vez; hash/tamanho do próprio fonte preenchidos somente no relatório externo.
