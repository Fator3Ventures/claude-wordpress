# Entrega — Fator3 MCP Pipedrive 0.4.0

Revisão 1 · 2026-10-29T01:03:23-03:00 · Rodada: implementação.
Slug/basename preservados: `wp-mcp-pipedrive-fator3/wp-mcp-pipedrive-fator3.php`.
Estado: **apta no escopo testado, com pendências de configuração comercial e aceite no fornecedor**. Instalada e ativa no Site-Teste. Pedidos 4–9 implementados; não declarados aceitos na conta real nem retirados da lista central por este agente.

## 1. De onde esta versão entra

Atualização direta da 0.3.0 e instalação limpa. Base recuperada íntegra da entrega anterior: instalador 59.877 bytes, SHA-256 `30fc784a552a89351900c169fad7300759163fb886b842f45ba807bb0977f657`; fonte 178.523 bytes, SHA-256 `c5d053f8a63e3a63f79645811bb0c62495bb8b5f6975bc796527ff5bc861cf29`. Não se instalou intermediária.

Entradas: `Fator3 MCP Pipedrive(3).md` (abertos 4–9, base0.3.0); fontes, instaladores e relatórios anexados de Core 1.60.0, MCP 0.36.0, Google 0.22.0, Meta 0.14.0 e LinkedIn 0.12.0. CRC dos pacotes conferido. Normas comuns revisão 5, de23/10/2026, prevalecem sobre a cópia avulsa revisão 4; os arquivos da revisão 5 no Core 1.60 coincidem com os já recebidos na base0.3. Plano anterior ao código em `PLANO-0.4.0.md`.

Identidade, namespace, Text Domain, Update URI, autor, licença e mínimos preservados. Corrente testado: WordPress 7.1.4/PHP 8.3.36 64bits/MySQL 8.0.41. Mínimo de backend testado: WordPress 7.1.3/PHP 8.3.36/MySQL 8.0.41, instalação própria com PHP/JSON/HTML/TXT/CRT da distribuição7.1.3. JS/CSS/imagens/temas de distribuição foram omitidos nesse ensaio; não é prova visual do mínimo. Arquivo de origem SHA-256 `d2a09acb6a15e3b9c471d72557753c266d6f41a79ed19bfe04cbfe49e283b2a5`; derivação e cobertura em `evidence/minimum-input.json`. Lint local usou PHP 8.3.6; as provas funcionais rodaram no PHP 8.3.36 do Site-Teste.

## 2. Convivência e encaminhamentos

| Pacote | Fonte/relatório recebido | Versão na integração final e no Site-Teste |
|---|---|---|
| Site Core | 1.60.0 | 1.60.0 |
| MCP | 0.36.0 | 0.37.0 |
| Google | 0.22.0 | 0.22.0 |
| Meta | 0.14.0 | 0.14.0 |
| LinkedIn | 0.12.0 | 0.13.0 |
| Pipedrive | 0.3.0 | 0.4.0 |

MCP e LinkedIn foram atualizados por outra manutenção durante a rodada. Nenhum desses pacotes foi sobrescrito, rebaixado ou alterado por nós no site compartilhado. A matriz final foi fixada em cópias privadas no laboratório; 41 verificações passaram no executor original MCP 0.37.0. As primeiras execuções também exercitaram MCP 0.36.0, mas a prova final de convivência é a tabela acima. Não se atribui homologação comercial dos acompanhantes a esses testes.

Contratos preservados: `pipedrive-api-client/1.0.0`, registro público de provider/prefixo MCP e política de conexão. Core segue único detentor de token, transporte, identidade/revisão, pausa, saldo e orçamento `operacao`. Rotas fixas GET/POST/PATCH dos novos fluxos cabem no contrato público existente. Nenhum SDK, cron, token ou cliente HTTP paralelo foi introduzido.

**Impactos novos:** nenhum identificado nas fronteiras examinadas; zero arquivos de impacto emitidos. Não há pedido de alteração em outro pacote nem ordem especial de troca além de ter o contrato Core disponível e autorizado. A autorização não é concedida pela atualização.

**Tratamento dos relatos recebidos:** Core 1.60 trata pré-validação de credenciais; não muda o contrato Pipedrive consumido. Meta 0.14 e Google 0.22 não exigem mudança Pipedrive. O relato LinkedIn 0.12 sobre site-core-quality/MCP 0.34 é histórico: MCP 0.36 recebido já documenta o atendimento no ciclo0.35. Esses desfechos ficam neste relatório, sem reemissão de impacto. O pedido 3/relatório0.3.0 permanece implementado e passou49 regressões; a comparação com a tela do Pipedrive continua pendência 20 da frota, conforme o documento recebido. As contagens reais65/2 citadas no anexo são prova da frota na0.3.0, não coleta nova desta rodada.

## 3. Mudanças e evidência

| Pedido | Implementação | Prova e limite |
|---|---|---|
| 4 | Option `f3_pipedrive_operation_rules`, revisão, simulação prévia, frase de ordem do dono; dias/fuso/janela/períodos/prazos/exclusões/etiquetas/textos configuráveis; `cadencia-fila` por IDs | Dia útil9h30, exclusão por etiqueta, texto aprovado, prazo alterado em simulação sem nova versão; histórico desconhecido e coleta parcial impedem item devido. Regras comerciais reais ainda não carregadas. |
| 5 | `whatsapp-registrar`, uma atividade por tipo/lead, linha escapada, próximo período UTC, chave por mensagem e recibo sem expurgo automático | Criação, anexação, repetição sem nova escrita, conflito de corpo/chave, duplicidade, trava entre conexões e timeout bloqueando outra chave. Registra envio confirmado pelo operador; não envia WhatsApp. |
| 6 | `lead-encerrar` com prévia: linha final+done e arquivo; `negocio-perder` com lista aprovada de lost_reason | Motivo inválido sem escrita; prévia sem mutação; efeitos e replay; cliente original Core com orçamento exato. Archive_reason também validado no caminho genérico. Listas só via configuração simulada e confirmada. |
| 7 | `lead-arquivado-editar`: desarquivar, editar allowlist, rearquivar preservando motivo e reler datas | Caminho completo e edição403 com rearquivamento confirmado; recibo mostra data original/nova. Arquivamento original sem data/motivo é recusado. Falha/resultado incerto mantém bloqueio para reconciliação. |
| 8 | `auditoria` por ID/regra: quatro origens, próxima atividade, título, organização/pessoa, etapa e reunião | Fixtures incluem organização4891 e negócio8, apenas sintéticos. Compara nomes somente em memória e não os retorna; configuração incompleta aparece como tal. Não se consultou DD8 ou organização real. |
| 9 | `contar-por-campo` com catálogo, paginação, arquivos de leads/negócios, vazios, IDs de opções e HMAC para demais valores | Contagens incluindo arquivo/vazio, quatro entidades, privacidade e orçamento/paginação parcial. Múltipla escolha conta cada opção por registro; pessoas/organizações não têm coleção de arquivo nessa API. |

São **19 rotas**: nove anteriores e dez novas (`configuracao-ler`, `configuracao-simular`, `operacao-aplicar`, `cadencia-fila`, `whatsapp-registrar`, `lead-encerrar`, `negocio-perder`, `lead-arquivado-editar`, `auditoria`, `contar-por-campo`). As rotas de encerramento/perda/edição criam prévia; aplicar é separado. Todos os schemas, permissões e classificações read/write estão instalados.

Não há transação distribuída no fornecedor. O recibo persiste etapas, códigos e efeitos parciais; uma interrupção conserva trava/estado e não repete automaticamente. A edição arquivada tenta rearquivar após falha de edição. Unicidade é coordenada entre operações cooperantes deste plugin: escritores externos não compartilham o mutex; a reconsulta após criação detecta duplicidade sem apagar atividade alheia. Escrita genérica de lead também respeita trava pendente.

Paginação e saída são limitadas e explícitas: 120 chamadas/120s máximos, 12.000 registros; fila200 itens, auditoria1.000 ocorrências, contagem200 grupos. Padrão100 chamadas/45s. Falha, limite, cursor inválido, identificador ilegível, estado/contexto concorrente ou campo/regra ausente impedem declaração de completude. HMACs dependem dos salts e não expõem valores livres da conta. Custos20/10 são unidades estimadas do contrato local Core, não os tokens oficiais de cada endpoint.

Fontes técnicas consultadas: [Activities](https://developers.pipedrive.com/docs/api/v1/Activities), [Leads](https://developers.pipedrive.com/docs/api/v1/Leads), [Deals](https://developers.pipedrive.com/docs/api/v1/Deals), [migração v2](https://pipedrive.readme.io/docs/pipedrive-api-v2-migration-guide) e [restrição de arquivados](https://developers.pipedrive.com/changelog/post/breaking-change-archived-deals-and-leads-will-not-be-returned-in-existing-endpoints-and-will-not-be-editable). Não foi incorporado SDK externo.

## 4. Instalação e prova da troca

Instalador final **84775 bytes**, SHA-256 **`70100900ebd7b358e96c9778eaa359aeb454203f759136da380adcb853b383fe`**, aplicado em [Site-Teste](https://fator3-teste-mcp-1.dreamhosters.com/) com `plugins/upload-base64`, `expected_slug=wp-mcp-pipedrive-fator3`, hash obrigatório, overwrite/activate explícitos e chave idempotente. Operação `a9e9f6eef61a2f7d038a08f5c8ef181f`; pré-imagem `3bb7bfd9730bf455761c2595`. Resultado applied=true,0.3.0→0.4.0 ativa em novo PHP. Sondas internas de `/` e `/wp-json/`:200 antes/depois. Não houve publicação raw/GitHub nesta rodada.

| Ambiente/cenário | Aprovadas | Evidência no fonte |
|---|---:|---|
| WP7.1.4 instalação limpa, funções base/autorização/concorrência | 89 | current-native.json |
| Relatório anterior | 49 | current-report.json |
| Retenção | 33 | current-retention.json |
| Pedidos4–9 | 56 | current-release.json |
| MCP 0.37 original,11 documentos, perfis e leituras novas | 41 | current-integrated.json |
| Core 1.60, retenção e escrita anterior | 8 | current-core.json |
| Core 1.60, relatório | 6 | current-core-report.json |
| Core 1.60, WhatsApp/encerramento/orçamento real do cliente | 7 | current-core-workflows.json |
| Upgrade0.3.0→0.4.0 + reinício/reativação | 11 | upgrade-verify-upgrade.json; upgrade-upgrade-restart.json |
| WP7.1.3/PHP 8.3.36 backend: base+relatório+retenção+novos pedidos | 227 | minimum-native/report/retention/release.json |

**527 verificações funcionais/de integração aprovadas**, incluindo as11 de upgrade; **58 verificações estáticas/de empacotamento** adicionais. Lint de32 PHP entre runtime/testes/build. Logs dos laboratórios corrente e mínimo: zero Warning/Notice/Deprecated/Fatal atribuídos ao Pipedrive; logs globais continham ocorrências de outros componentes, não foram declarados vazios. HTTP do fornecedor/e-mail interceptados. Teste com cliente original Core verifica encoder, contrato, autorização e consumo; respostas Pipedrive continuam simuladas.

Documentação compartilhada:11 documentos,12 páginas, conteúdo integral recebido via `pipedrive/documentacao-ler`, versão0.4.0, SHA/bytes idênticos ao instalador; `shared-documents.json` e `shared-documents-bytecheck.json`. Árvores completas do instalador, laboratório e site compartilhado coincidem em30arquivos. O último ajuste antes de fechar foi exclusivamente documental; a árvore final foi instalada novamente no laboratório e seus41 testes MCP/documentais repetidos.

As primeiras rodadas localizaram expectativas de fixture inadequadas: negócio já perdido no teste de auditoria, contagem de diário após outra suíte e versões alteradas por terceiros. Foram corrigidos preparação/ordem e expectativas comprovadas, com execução final limpa; não se ocultou falha funcional como sucesso. Evidências intermediárias em development. A contagem de opções múltiplas foi refinada para cada opção, conforme o pedido.

Limpeza: laboratórios corrente98 tabelas, upgrade14 e mínimo14 removidos somente pelos prefixos próprios; zero remanescentes e diretórios removidos. Dois controladores temporários e dois ZIPs de QA excluídos com guarda SHA. Backups normais do MCP preservados. Catálogo final:19 rotas Pipedrive 0.4.0, zero auxiliares qa-pipedrive040. Health final healthy=true e recovery unresolved=0. Inventário final corresponde à seção2, todos ativos. Não houve remoção de tabela compartilhada.

## 5. Banco e volta de versão

Duas tabelas anteriores e schema 1 preservados; nenhuma migração nova. Regras locais são criadas apenas ao aplicar simulação, e travas/recibos somente em execução explícita. No Site-Teste, operações/diário continuaram vazios; hashes de tabelas, retenção, schema e autorização Core ficaram iguais imediatamente antes/depois. `shared-preservation.json` registra as quatro comparações verdadeiras. Instalação não inicializou regras comerciais nem autorizou a conta.

Prova de upgrade semeou recibo concluído, prévia pendente e tentativa running cifrados, duas linhas antigas e retenção730 dias. Conteúdo/ciphertexts/configuração preservados byte a byte e após reativação. As provas sintéticas vivem apenas nos prefixos descartáveis, já removidos.

Para voltar, reinstalar0.3.0 preservando banco, options, salts, recibos e travas. A pré-imagem cobre arquivos, não desfaz efeitos do fornecedor nem restaura banco. A0.3.0 perde as dez rotas novas e não observa as novas travas de fluxo em sua escrita genérica: suspender escritas até reconciliar pendências antes de voltar. Não apagar chaves de mensagem para tentar novamente. Preferir correção adiante quando houver execução incerta. Reconciliação automática/liberação automática de travas não está nesta versão; guia fluxos descreve conferência por IDs e manutenção após ordem explícita do dono.

## 6. O que permanece pendente

| Pendência | Responsável | Critério |
|---|---|---|
| Horários, textos, prazos, exclusões, mapeamento de quatro origens, etiquetas/tipo WhatsApp e motivos de perda | Dono/operador SDR | Fornecer/usar versões aprovadas de “Regras de operação do Pipedrive” e “Referência para agentes”, procedimento 9; simular e aplicar a configuração com revisão/frase. Referências não vieram anexadas e buscas acessíveis não as localizaram. |
| Aceites reais4–9 em korvena.com.br, inclusive testes descartáveis e comparação com tela | Frota/operador autorizado | Confirmar fila9h30, unicidade/replay, encerramento, rearquivamento/datas, auditoria de registros ainda naquele estado e contagem da mesma seleção; remover somente registros de teste criados. |
| Pendência20 do relatório0.3.0 | Frota | Contagens por Parceiro/motivo iguais à tela; não encerrada aqui. |
| Operação comercial no Site-Teste | Dono/operador Core | Status continua operacao_nao_autorizada, como antes; conceder autorização/conta apenas pelo fluxo próprio do Core, se desejado. |
| Publicação e distribuição nos sites-porta | Dono/Implantador | Conferir artefatos/hashes e usar processo da frota; nenhum push ou implantação em produção nesta rodada. |
| Inspeção visual em navegador e matriz MariaDB | Manutenção, se necessária | Não realizadas; provas disponíveis são PHP/REST/MCP, renderização HTML administrativa e MySQL 8.0.41. Mínimo foi ensaio de backend, não frontend completo. |

As pendências de negócio/fornecedor não foram inventadas como concluídas. Não houve consulta de dados privados em outro site nem nova tentativa do acesso anteriormente recusado fora do Site-Teste.

## 7. Credenciais e configuração do dono

Nenhum token real foi lido, exportado, renovado ou incluído. Credencial e escopos continuam no Site Core; todas as novas chamadas usam consumer operacao. O status local e documentação são utilizáveis sem autorização comercial, com manage_options obrigatório. `configuracao-ler` retorna origem padrao_pendente, cadência desabilitada, listas vazias de horários/textos/perda e apenas os nove motivos de arquivamento explicitamente fornecidos no pedido 6.

Textos/configuração comercial não foram inventados. Nomes, e-mails, telefones e títulos do fornecedor não saem nas leituras agregadas/auditoria; a fila retorna apenas textos aprovados da option. O registro WhatsApp aceita mensagem do operador para gravar na atividade, sem disparar comunicação. As evidências contêm somente IDs/nomes/canários sintéticos e hashes/contagens de preservação.

## 8. Identidade dos arquivos

| Artefato | Nome | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | wp-mcp-pipedrive-fator3-0.4.0-instalador.zip | 84775 | 70100900ebd7b358e96c9778eaa359aeb454203f759136da380adcb853b383fe |
| Fonte | wp-mcp-pipedrive-fator3-0.4.0-fonte.zip | 297237 | 1484739a125a4f349fcef68e84e34137ef262822359f900af14d4200c97e32d6 |

Relatório externo canônico: `wp-mcp-pipedrive-fator3-0.4.0-relatorio.md`. A cópia interna no fonte é anterior ao fechamento; este relatório externo contém o tamanho/hash finais do fonte. Só o instalador é instalável. Fonte único com código/build/testes/entradas/evidências sanitizadas e este relatório; nenhum ZIP aninhado, segredo, banco, helper ativo ou dependência local privada. Documentação e schemas fazem parte do instalador. Zero relatórios novos de impacto.
