# Entrega — Fator3 MCP LinkedIn 0.12.0

Revisão 1 — 28/10/2026. Rodada de implementação sobre 0.11.0. Estado: **apta-no-escopo-testado**, com pendências de homologação do fornecedor e auditoria central comercial. A versão 0.12.0 passa a ser a corrente desta entrega.

**Relatório externo canônico, após o fechamento do fonte.** A cópia congelada dentro de `wp-mcp-linkedin-fator3-0.12.0-fonte.zip` é identificada como anterior ao fechamento. Seus resultados são os mesmos; somente este relatório externo contém bytes e SHA-256 finais do próprio fonte, evitando circularidade.

## 1. Bases aceitas

Instalação limpa e atualização direta **0.11.0 → 0.12.0**, sem versão intermediária. Base: entrega LinkedIn 0.11.0 recebida em WP Plugin, com instalador de 283.053 bytes, SHA-256 `34541afa67c0991e9dc0b5474ab8678dff8cf806eace6ceb1edb47983f9e0308`, e fonte de 1.490.342 bytes, SHA-256 `5048b99a73ed9ec2beed7545832b13d88d63dafe432100722f2989eb86ee493e`. O README e o relatório dessa base estão preservados em `history/received-0.11.0/`.

Aplicadas as normas comuns revisão 5, de 23/10/2026, documentos do pacote, versões e relatórios recebidos. O novo escopo vem do **Pedido Core 323**, encaminhado por `base-site-core-fator3-1.58.0-impacto-wp-mcp-linkedin-fator3.md`, revisão 2. Não foi encontrado pedido LinkedIn posterior ao 14, já tratado na base. O incremento minor corresponde à nova capacidade opcional, preservando os contratos existentes.

## 2. Convivência e encaminhamentos

Os instaladores acompanhantes foram usados sem modificações. O inventário completo dos arquivos recebidos, com tamanhos e hashes, está em `inputs/0.12.0/packages.json`. Relatórios recebidos são contexto; os resultados abaixo distinguem as provas executadas nesta rodada.

| Pacote | Versão recebida | SHA-256 do instalador | Prova própria nesta rodada |
|---|---|---|---|
| Core | 1.58.0 | `71bf6497a2f2e2c605baf64f0f82c273201915039506b58ac220fc572afbd5e4` | Ativo nos laboratórios integrados; adaptador, elegibilidade, repositório e fila reais exercitados. |
| MCP | 0.34.0 | `5d96b6a33cfc4a7c729c106268f4bc9d8938b34384da022345d7b7dae611a295` | Executor, autenticação, schemas, documentação e auditoria de aquisição; limitação comercial identificada. |
| Google | 0.21.0 | `25da9ef78e303f30ce2f73b8f98743a26e09b8ed238177474e4a956578a63814` | Ativo nos laboratórios integrados; convivência e integridade, sem homologação da API Google. |
| Meta | 0.13.0 | `3ecd6ee6f277c7581adc05b4fa38c46611e3232b4400bb4a4421956c9fba8ac1` | Ativo nos laboratórios integrados; convivência e integridade, sem homologação da API Meta. |
| Pipedrive | 0.3.0 | `30fc784a552a89351900c169fad7300759163fb886b842f45ba807bb0977f657` | Fonte e instalador conferidos. Não ativado localmente: exige PHP 8.3.36, superior ao PHP 8.3.6 disponível. |

Foram comparadas integralmente dez árvores instaladas dos acompanhantes, cinco na instalação limpa e cinco no upgrade, além dos cinco fontes recebidos. Os 16 anexos originais também permanecem byte a byte iguais. Evidências: `companion-integrity.json`, `received-source-trees.json` e `received-unchanged.json`, em `evidence/release0120/`. **Código e documentação de Core, MCP e demais pacotes não foram alterados.**

### Impacto emitido nesta rodada

Destinatário: mantenedor MCP. Documento: `wp-mcp-linkedin-fator3-0.12.0-impacto-wp-mcp-fator3.md`, revisão 1, `acao-necessaria`, demanda aberta. Não há número novo de pedido MCP atribuído. O MCP 0.34.0 aceita somente `site-core-conversions` no schema de identidade de auditoria. Deve admitir explicitamente `site-core-quality` no contrato, leitor e painel, mantendo as validações existentes.

A prova com os pacotes originais confirmou entrega sintética e introspecção local válida, mas ausência de recibo central comercial: `central_audit=service_record_unconfirmed`. O LinkedIn preserva o diário local e não reenvia por esse motivo. A aquisição continua com auditoria central registrada. Trata-se de nova consequência técnica, e não de simples confirmação do impacto recebido. O documento emitido durante a validação do candidato permanece com sua identidade original; não foi revisado só para anunciar o fechamento. A mesma limitação foi reproduzida com o instalador final.

Ordem de adoção: LinkedIn 0.12.0 pode ser instalado primeiro; o fluxo comercial requer Core 1.58.0 ou versão compatível efetivamente validada. A confirmação central comercial depende de uma futura versão MCP que aceite o consumidor, seguida de teste coordenado. Nenhum outro impacto substantivo foi identificado nas fronteiras examinadas. A integração nativa Pipedrive permanece não avaliada por incompatibilidade do runtime local.

### Tratamento dos impactos recebidos e anteriores

**Pedido Core 323 — impacto Core 1.58.0 → LinkedIn, revisão 2.** Documento recebido com 7.288 bytes, SHA-256 `30db19cf3adee5a6ec8a24f3eaa21f962b5ed23b5eb170fca2def0f955ccfa94`. Responsável pela execução desta fronteira: mantenedor LinkedIn. Resultado: `implementado`, `validado-localmente` e `validado-wordpress` para contrato 1.2.0, concessão por ação, referência vinculada, payload fechado, deduplicação e revalidação. Evidências: `stages012.php`, `stages012-core.php`, `mcp-stages012.php`, `upgrade012.php` e suas saídas nas matrizes finais. A parte LinkedIn foi atendida; homologação externa e evolução MCP continuam pendentes dos responsáveis. O documento recebido foi preservado, sem gerar ou reentregar impacto de encerramento. O histórico anterior não é apresentado como novo encaminhamento.

## 3. Mudanças por pedido e evidência

**Pedido Core 323 — conversões comerciais.** Foi implementado o contrato opcional `site-conversion-delivery/1.2.0`, consumidor `site-core-quality`, finalidade `crm_stage`. A aquisição 1.0.0 e seu consumidor `site-core-conversions` continuam independentes. Contatos, consentimento, elegibilidade, etapas e fila permanecem sob responsabilidade do Core; o LinkedIn não lê seu armazenamento privado.

| Mudança | Comportamento e prova |
|---|---|
| Concessão por ação | Conexão, conta, ação, consumidor, finalidade, concedente e revisões vinculados a referência aleatória opaca. Regra ativa `CONVERSIONS_API` da conta exata, escopos e papel validados. Prévia é padrão; gravar exige confirmação e CAS. Não reaproveita ação da aquisição, inclusive no sentido inverso. Testes cobrem duas ações, concessão/revogação, conflitos e acesso não administrativo. |
| Adaptador e capacidades | Seleção explícita da ação e `sendBound`. Capacidades SDK estritamente locais, sem escrita ou HTTP. Referência vazia, alterada ou antiga é recusada; não escolhe destino alternativo. Token deve ter prova atual. Alterações benignas preservam referências; troca explícita de identidade revalida e gira referências; mudança de autorização invalida a concessão. |
| Payload fechado | Valida contrato, finalidade, IDs, instante original RFC3339, equivalência exata em milissegundos e janela de sete dias. Admite somente identificadores previstos, sem identidade em texto nem campos extras. Apenas `eventId`, `conversion`, `conversionHappenedAt` e `user` chegam ao fornecedor. Casos negativos bloqueados antes do HTTP. |
| Concorrência e recuperação | Bloqueios conexão → concessão → entrega, com revalidação imediatamente antes do HTTP. Chave comercial inclui consumidor, finalidade, conta, regra e evento; digest HMAC do envelope detecta conteúdo divergente. Confirmado ou incerto não repete envio após reinício. Timeout, 5xx e exceção mantêm incerteza; recusa comprovada tem recibo próprio. Exercitados processos distintos, revogação concorrente e usuário WordPress zero. |
| Integração Core real | Prévia sem fila/envio; consentimentos atual e snapshot; exclusões, tráfego de teste/homologação, origem e contato inelegível; datas inválidas e falta de identidade. Duas etapas em regras diferentes enviam uma vez; referência alterada e reutilização da aquisição bloqueiam; incerteza é terminal. HTTP do fornecedor é sintético, sem substituir o adaptador, repositório ou fila Core. |
| Operação e interface | Novo painel “Conversões de etapas comerciais” em Ativos, com seleção descoberta, prévia, confirmação e revogação. Três operações novas: `get-stage-conversion-grants`, `stage-conversion-capabilities`, `save-stage-conversion-grant`. HTML/JS e REST autenticado reais exercitados em 26 verificações DOM. |
| Auditoria de serviço | Leitor próprio aceita os dois consumidores, resolve a concessão a partir do diário e mantém autorização/posse. Testados consumidor forjado, revisões, dono, revogação e redação. Limitação MCP documentada sem simular recibo central bem-sucedido. |
| Documentação e build | Documentação própria atualizada, com `STAGE-CONVERSIONS.md` e `RELEASE-0.12.0.md`, schemas e conteúdo compilado correspondentes. Build reproduz exatamente o instalador final. |

Comparação com a base: **4 arquivos adicionados, 26 alterados e nenhum removido** no runtime. São 71 arquivos, 33 PHP, 31 documentos e 93 operações, ante 90 na base. O único schema de operação existente alterado é `get-service-write-operation`, ampliando o enum de consumidor; nomes e campos obrigatórios existentes foram preservados. Evidências: `runtime-changes.json`, `runtime-0110-0120.diff` e `schema-comparison.json`.

Regressões exercitadas incluem funções próprias, permissões, filas, histórico, retenção, callback e fluxos anteriores cobertos pelas suítes da base. Não houve mudança de seletor de provedor do Core, criação automática de concessões ou novo agendamento comercial LinkedIn. Os ajustes de fixtures e harness estão separados em `preliminary-observations.json`; suas execuções preliminares não foram somadas ao resultado final.

## 4. Instalação e prova de prontidão

Todas as matrizes abaixo usaram o mesmo instalador final, SHA-256 `19748e788190f371809db469a6de052a645e25f39fad1672606dc776234ec54c`. Laboratórios descartáveis, WordPress e MySQL reais, HTTP externo e e-mail interceptados. Não foram usados contatos ou credenciais reais.

| Matriz final | Ambiente | Verificações funcionais | Aprovadas | Não aplicáveis | Falhas | Documentais | DOM |
|---|---|---:|---:|---:|---:|---:|---:|
| Instalação limpa integrada | WP 7.1.3 / PHP 8.3.6 / MySQL 8.0.46 | 246 | 245 | 1 | 0 | 32 | 0 |
| Atualização direta 0.11.0 | Mesmo ambiente integrado | 262 | 261 | 1 | 0 | 32 | 0 |
| LinkedIn isolado | WP 7.1.3 / PHP 8.3.6 / MySQL 8.0.46 | 230 | 228 | 2 | 0 | 0 | 0 |
| Mínimos declarados | WP 6.4 / PHP 8.1.2 / MySQL 8.0.46 | 230 | 226 | 4 | 0 | 0 | 0 |
| Interface e integração complementar | WP 7.1.3 / PHP 8.3.6 / MySQL 8.0.46 | 29 | 29 | 0 | 0 | 32 | 26 |
| **Total de execuções** | | **997** | **989** | **8** | **0** | **96** | **26** |

Os totais são execuções em diferentes matrizes, não casos únicos. Não aplicáveis são as condições identificadas pelas suítes conforme recursos presentes, não sucessos presumidos. Todos os processos finais retornaram zero. Logs finais sem Notice, Warning, Deprecated ou Fatal. As 96 verificações documentais incluem índice e 31 documentos em cada uma de três matrizes integradas. A interface foi exercitada com jsdom 27.4.0, sem inspeção visual em navegador. A versão Pipedrive recebida não foi ativada no runtime local inferior ao seu mínimo.

### Site-Teste compartilhado

Destino: `https://fator3-teste-mcp-1.dreamhosters.com/`. Única instalação alterada: LinkedIn 0.11.0 → 0.12.0, por **WP MCP fator3-teste**, ability real `plugins/upload-base64`, com arquivo final, `activate=true`, `overwrite=true`, `expected_slug=wp-mcp-linkedin-fator3`, SHA-256 exato e timeouts de 10 segundos. Chave idempotente: `linkedin-0120-19748e788190-20261028`. Nenhum helper de teste foi instalado no ambiente compartilhado.

Recibo aplicado: operação `2c781b200395d0b197a1ccd8bd9743a8`, backup de arquivos `4c1a954d307436842bfc8867`, `applied=true`, `active_after=true`, versão final 0.12.0. Reativação silenciosa comprovada em requisição PHP nova e worker independente; isso não equivale a completar ciclo de hook de ativação nem homologação comercial.

Home e `/wp-json/` retornaram HTTP 200 antes/depois, com bypass de cache assinado verificado. As sondas são internas de mesma origem: não comprovam acesso externo universal nem cache público atualizado. A invalidação de cache foi solicitada ao provedor.

Estado final observado: `linkedin/status` com armazenamento e criptografia prontos, `state=ok`, sem issues, sem conexões e sem agendas ativas, migração completa e zero jobs ilegíveis. `linkedin/selftest` aprovou **9/9**, sem testes externos. Capacidade comercial da ação consultada: `ready=false`, `reason=sem_concessao`; lista de concessões vazia. Portanto, a instalação não habilitou envio comercial automaticamente.

Documentação instalada lida integralmente pelo índice e leitor MCP, usando paginação e guarda de revisão: **31 documentos, 33 páginas e 272.425 bytes**, todos idênticos ao instalador. O acesso documental não chama fornecedor nem altera configuração. Detalhes em `site-docs.json`.

Os demais plugins mantiveram suas versões e ativação: Core **1.57.1**, MCP 0.34.0, Google 0.21.0, Meta 0.13.0, Pipedrive 0.3.0, DreamHost 1.0.0, WP Super Cache 3.1.4 e Yoast 28.8. O Core 1.58.0 foi testado localmente, mas não foi instalado no Site-Teste por esta rodada LinkedIn. Não houve envio real de conversões, gasto Ads, publicação, mensagem a clientes, push GitHub ou implantação em frota.

Para instalação pelo dono/frota: conferir a identidade da seção 8 e instalar somente o ZIP instalador, preservando banco e salts. A raiz é `wp-mcp-linkedin-fator3/`. Após atualizar, verificar status/selftest e documentação; depois configurar credencial, ativos e concessão explícita. Capacidade local pronta não substitui homologação remota. Evidências completas em `site-test.json` e nos diretórios das cinco matrizes.

## 5. Banco e volta de versão

Schemas preservados: registros **2**, histórico **1**. Não há tabela/opção nova. As concessões comerciais usam o bucket cifrado `conversion_grant`, com chave `site-core-quality:<action>`; os recibos usam `conversion_event`. A aquisição mantém chaves e comportamento existentes. Retenção, histórico, configurações e filas da base permanecem.

O upgrade foi semeado na 0.11.0 e verificado antes das mutações dos testes seguintes: oito provas de preservação integral das linhas de registros/histórico, ciphertext, revisões, política, conexão, concessão, referências e diários confirmado/incerto, incluindo introspecção e ausência de concessão comercial automática. Após a comparação, o harness retira somente a concessão sintética de aquisição e restaura a retenção padrão para cenários independentes; não é uma rotina do plugin nem um procedimento de produção.

O diário comercial persiste referências e digest técnicos, sem payload, record_id, stage_id, hash de e-mail ou li_fat_id. Confirmado/dispatching/incerto não autoriza novo HTTP. Ausência de recibo central não autoriza reenvio.

Antes de voltar para 0.11.0, desabilitar o destino comercial no Core, preservar banco/salts/diários e coordenar o estado das reservas. A base não anuncia o contrato 1.2.0. O backup do instalador cobre arquivos, **não desfaz banco nem efeitos no fornecedor**; o próprio recibo informa `database_effects_reversible=false`. Não apagar diários para forçar repetição. Não foi necessário executar rollback no Site-Teste.

## 6. Pendências de validação e responsáveis

| Item | Estado e limite | Responsável / próxima ação |
|---|---|---|
| Auditoria central comercial | `pendente`: MCP 0.34.0 não admite `site-core-quality`; recibos locais e deduplicação funcionam. | Mantenedor MCP: tratar o impacto desta entrega e executar aceite coordenado. |
| Core comercial no Site-Teste | `pendente`: servidor permanece 1.57.1; Core 1.58.0 foi validado em laboratório real. | Mantenedor Core/implantador: planejar sua implantação e configurar o mapa de ações. |
| Fornecedor LinkedIn real | `pendente`, não `homologado-fornecedor`: tokens, aprovação do aplicativo, regras e atribuição Campaign Manager reais não foram usados. | Dono da conta/aplicativo: fornecer acesso autorizado e homologar em destino próprio. HTTP sintético e aceite 201 não comprovam atribuição. |
| Pipedrive nativo com acompanhantes | `nao-avaliado`: mínimo próprio PHP 8.3.36 supera o runtime local. Integridade dos bytes conferida; Site-Teste permanece ativo. | Responsável pela integração: repetir convivência em PHP compatível se necessária. |
| Inspeção visual em navegador | `pendente`: 26 verificações DOM/REST aprovadas, sem inspeção visual humana. | Responsável pela homologação de interface: revisar o painel com credenciais de teste. |
| Publicação e frota | Não executadas nesta rodada; fonte destinado ao dono. | Frota: verificar hashes, publicar/distribuir conforme autorização aplicável. |

Não foram observadas regressões nas provas executadas. Isso não constitui garantia de ausência de qualquer impacto em contas, combinações de versões ou fornecedores não testados. As pendências acima delimitam o uso; a instalação e os fluxos anteriores permanecem utilizáveis no escopo demonstrado.

## 7. Credenciais e configuração, sem valores secretos

Em **Ferramentas → Fator3 MCP LinkedIn → Conexão**, o dono informa **Access Token**, **Client ID** e **Primary Client Secret**, além da identificação da conexão. Tokens manuais permanecem padrão. Refresh Token só quando o aplicativo/produto tiver aprovação correspondente; a release não cria esse direito.

Em **Ativos**, selecionar contas autorizadas e, em **Conversões de etapas comerciais**, carregar regras, escolher a ação exata, revisar a prévia e confirmar. A regra precisa estar ativa, pertencer à conta e usar `CONVERSIONS_API`; são necessários `rw_conversions`, `r_ads` e papel compatível na conta. A criação/descoberta da conexão também segue os pré-requisitos existentes documentados em `CREDENTIALS.md`. O aplicativo deve ter acesso aprovado à API pertinente; listar escopo não comprova aprovação.

Usar regra própria por etapa, distinta da aquisição. O Core recebe a referência opaca e configura o mapa comercial, sem receber token/segredo LinkedIn. Não foi preenchida nenhuma credencial real nem concedido acesso comercial no Site-Teste. IDs de ações dos testes são sintéticos. O instalador contém instruções completas em `CONFIGURATION.md`, `CREDENTIALS.md`, `STAGE-CONVERSIONS.md` e `SERVICE-AUDIT.md`.

## 8. Identidade dos arquivos e fechamento

| Artefato | Bytes | SHA-256 |
|---|---:|---|
| `wp-mcp-linkedin-fator3-0.12.0-instalador.zip` | 304948 | `19748e788190f371809db469a6de052a645e25f39fad1672606dc776234ec54c` |
| `wp-mcp-linkedin-fator3-0.12.0-fonte.zip` | 1713239 | `15c182cc89605cb1fc18121d8db81fd9008daa06cb787f7224a973d18f4f65d1` |

Arquivos da entrega:

- [wp-mcp-linkedin-fator3-0.12.0-instalador.zip](sandbox:/workspace/scratch/be41fc0d56c8/li012/entrega/wp-mcp-linkedin-fator3-0.12.0-instalador.zip)
- [wp-mcp-linkedin-fator3-0.12.0-fonte.zip](sandbox:/workspace/scratch/be41fc0d56c8/li012/entrega/wp-mcp-linkedin-fator3-0.12.0-fonte.zip)
- [wp-mcp-linkedin-fator3-0.12.0-relatorio.md](sandbox:/workspace/scratch/be41fc0d56c8/li012/entrega/wp-mcp-linkedin-fator3-0.12.0-relatorio.md)
- [wp-mcp-linkedin-fator3-0.12.0-impacto-wp-mcp-fator3.md](sandbox:/workspace/scratch/be41fc0d56c8/li012/entrega/wp-mcp-linkedin-fator3-0.12.0-impacto-wp-mcp-fator3.md)

O instalador reproduzido byte a byte é o mesmo usado nos testes e no Site-Teste. O fonte tem uma raiz única `wp-mcp-linkedin-fator3-0.12.0-fonte/`, runtime idêntico ao instalador, código de build, testes, evidências sanitizadas, planejamento, entradas documentais e esta cópia do relatório. Não contém ZIPs aninhados, banco de laboratório, runtimes privados ou dependências de desenvolvimento instaladas. As provas das versões anteriores estão identificadas como histórico e não integram os totais desta rodada.

O fonte é fechado uma única vez. Somente o relatório externo recebe os bytes e SHA-256 finais do fonte; o ZIP não é reaberto para inserir sua própria identidade. Instalador e fonte tornam-se imutáveis após a entrega. Complemento de impacto: somente o encaminhamento substantivo ao MCP listado acima.
