# Entrega — Fator3 Site Core 1.33.0

15/10/2026. **Instalador validado para WordPress novo e atualização direta da 1.31.0. Não instalar a 1.32.0 antes.** O pacote incorpora a funcionalidade preparada naquela versão.

## O que mudou

- Ciclo de atualização próprio da versão alvo, com histórico, reserva renovável, retomada, falhas explícitas e confirmação posterior. Conclusão antiga não aprova a nova release.
- SDK `site-measurement-context/1.0.0`: contexto configurado/efetivo de GA4, GTM, Google Ads, Meta, LinkedIn e Clarity, políticas, procedência e revisão; catálogo paginado de 22 eventos e duas abilities autenticadas.
- Schemas fechados, fixtures e documentação instalada/paginada. Contexto não contém tokens nem dados de pessoas, não consulta fornecedores e não concede acessos.
- Ponte do implantador concentrada em adaptador, sem mudar responsabilidades ou aplicar configurações no site.
- Fronteira do cliente LinkedIn interno e diagnóstico de disponibilidade. O webhook opcional da 1.32 está incluído, com recibo durável e validação de assinatura.
- Diagnóstico do ciclo na tela com horários legíveis; exclusão de 404 mantida quando o navegador atualiza o contexto; leitor documental comporta os schemas completos.
- Incluídas as correções preparadas na 1.32 para Slack, cotas/diagnóstico Pipedrive, atribuição da sessão de captura e relatórios editoriais.

**Limite de escopo:** a troca para um provedor LinkedIn externo não está implementada nem liberada. Falta o SDK LI-04 concreto. A prova conjunta do novo SDK com Google 0.8.6 também aguarda binário. Essas pendências estão separadas das funcionalidades entregues, sem seletor que prometa uma troca inexistente.

## Instalação

1. Use o ZIP `base-site-core-fator3-1.33.0.zip` no instalador nativo do WordPress; sobre a 1.31.0, substitua o plugin mantendo suas configurações e dados. Em site novo, instale e ative.
2. Consulte F3 Base → Operação ou `f3base/saude-ler`. O alvo deve ser 1.33.0; acompanhe o ciclo e as etapas. O cron/executor conclui as tarefas pendentes; uma passagem posterior confirma a conclusão administrativa.
3. Mantenha o cron normal e confira os diagnósticos próprios das integrações. Instalação não ativa integrações comerciais nem reenvia histórico por conta própria.

O fluxo combinado de substituição do plugin ativo pelo MCP 0.21.1 retornou `package_verification_pending` / `activation_unconfirmed` na bancada. O percurso **validado nesta entrega é o atualizador nativo WordPress**. O achado foi documentado para o MCP; seu código não foi alterado. Não há trava de instalação por versão de acompanhantes e não há sequência de conversores de versões antigas.

## Evidência dos bytes entregues

- Instalador: `1,855,213` bytes, 356 arquivos.
- SHA-256: `de427cb219be769d9e44ae9aaf5e6f31055990b3d8f9b8664ac0faa596f61364`.
- WordPress 7.1.2, PHP 8.3.6, MySQL 8, Chromium; MCP 0.21.1 e Google 0.8.5 reais. APIs externas simuladas ou bloqueadas.
- Mesmo SHA-256 na instalação nativa limpa e no upgrade nativo 1.31→1.33; ambos aprovados. Primeiro GET pós-upgrade: HTTP 200, 359.04 ms na bancada, tag presente e captura antes da migração. Esse tempo não é previsão de desempenho em produção.
- Preservação por hash: contatos, sessão e origem, campanha, recibo nativo, filas Pipedrive/avisos, arquivo privado, concessão e segredos cifrados selecionados. Procedência/canal/data e lista vazia preservados.
- Sintaxe: 204 PHP e 28 JavaScript; nove pares fonte/minificado conferidos. Seis schemas e 11 fixtures do SDK; catálogo com 22 eventos.
- As 17 suítes de regressão de `execucoes-finais.json` terminaram sem falha; testes adicionais de ciclo, documentação, navegador, HTTP MCP/LinkedIn e empacotamento constam do resumo. Não se soma contagem antiga nem se usa número de assertions como garantia universal.

Não houve implantação na frota, acesso a korvena.net.br, mensagem real nem homologação remota de credenciais/destinos. Os arquivos de evidência distribuídos contêm resumos; banco, cookies, logs, screenshots e credenciais de laboratório foram excluídos.

## Rastreabilidade do plano

A premissa de implantação mais recente substitui o ensaio intermediário da 1.32 pelo caminho direto da 1.31. As demais limitações abaixo são explícitas.

| Aceite | Situação | Evidência / limite |
|---|---|---|
| A01 | Atendido na base acordada | Ciclo distinto sobre 1.31.0; checkpoint completo antigo não aprova a nova versão; novo agendamento ignora recuo anterior. |
| A02 | Atendido | Doze etapas e conclusão persistidas no alvo; confirmação em passagem posterior. Fixture avança o timestamp em 61 s, sem mudar regra do produto. |
| A03 | Atendido nos pontos ensaiados | Falhas SQL na abertura e em etapa; recuo e retomada conservam etapas comprovadas. Não é prova exaustiva de queda a cada instrução. |
| A04 | Atendido | Dois processos PHP simultâneos; um ciclo concluído e concorrente recusado; renovação de reserva e liberação por proprietário. |
| A05 | Atendido no percurso local | Reexecução idempotente sem DDL e sem alteração do checkpoint concluído; consultas de SDK sem rede/escrita e captura antes da migração. |
| A06 | Atendido | Instalação nova e atualização direta 1.31→1.33 com ZIP final; lista vazia e autoria preservadas. 1.32 intermediária dispensada pelo dono. |
| A07 | Atendido | Erro SQL, estado malformado e falha de CAS explícitos; não reclassificados como instalação nova. |
| A08 | Atendido | Primeiro GET com tag e captura de contato antes de executar a migração; verificação de estrutura em testes de falha. |
| A09 | Atendido nas fixtures | Hashes de contato, sessão/origem, campanha, recibo, filas, concessão, arquivo e segredos; autoria/canal/data e corte de coleta preservados. |
| A10 | Atendido | Tela mostra alvo, ciclo, etapa, datas no fuso e falha; Saúde usa o mesmo resumo. Prova de executor separada de prova HTTP. |
| A11 | Parcial de matriz | SDK Google real com grant/conexão não padrão, usuário zero, falhas e persistência locais. Não foram reexecutadas todas as combinações remotas de quota, ambiguidade e revogação previstas no plano. |
| A12 | Atendido nos acompanhantes disponíveis | MCP 0.21.1/Google 0.8.5 nas duas ordens, autorização e guardas independentes. Pacotes futuros não executados. |
| A13 | Atendido | Todos os documentos catalogados legíveis; paginação/hash, schemas/fixtures, recusa anônima e leitura em recuperação/checkpoint inválido. |
| A14 | Atendido nas fixtures | Filas/recibos selecionados preservados na troca; regressões de Slack, Pipedrive, captura e ingestão sem destinos reais. |
| A15 | Atendido | Instalador final identificado por SHA-256; fontes idênticas, sintaxe e manifestos; mesmos bytes no ensaio limpo e upgrade. |
| A16 | Atendido | SDK PHP local e duas abilities HTTP MCP; leitura sem credenciais ou PII; autorização nativa e de transporte. |
| A17 | Atendido | Seis slots, físico/efetivo, filtro, vazio, módulo indisponível, Clarity e SQL indisponível; não afirma entrega remota. |
| A18 | Atendido | Revisões estáveis sem relógio; mudanças de option/filtro e snapshot instável; paginação com revisão obrigatória na continuação. |
| A19 | Atendido com amostragem de emissão | 22 eventos declarados; seis schemas fechados, 11 fixtures e fonte geradora; parâmetros dos payloads capturados comparados. Nem todo evento foi disparado no navegador nesta rodada. |
| A20 | Atendido nos cenários locais | Chromium/minificados: consentimento negado/aceito/revogado, teste, 404 real e editor autenticado; formulário, atribuição e arquivo privado. APIs de destinos bloqueadas. |
| A21 | Atendido no escopo Core | Adaptador JSON isolado; ausência/ambiguidade/validador/permissões e escrita sem aplicar site. Validador externo é fixture; desacoplamento definitivo não entregue. |
| A22 | Parcial por ambiente | Escrita MCP refletida no HTML e invalidação local de cache/llms. Yoast ausente diagnosticado. Noindex previamente gravado respeitado em fixture; mutação SEO por Yoast e cache externo não homologados. |
| A23 | Parcial — externo não implementado | Cliente interno preservado e diagnóstico explícito; seleção/grant do produtor externo aguardam LI-04 concreto. |
| A24 | Pendente externo | Não há troca, drenagem, commit ou retomada entre dois provedores sem SDK concreto; modo externo indisponível. |
| A25 | Atendido no cliente interno | Polling/recibo/webhook e deduplicação com fixtures; mesma ingestão comercial preservada. Não encerra a troca externa. |
| A26 | Parcial — interno | Falhas e diagnóstico do cliente interno ensaiados; revogação/remoção do futuro provedor externo não implementadas. |
| A27 | Atendido documental; matriz parcial | Cinco donos e universos documentados; isolamento executado com Core/MCP/Google disponíveis; Meta/LinkedIn novos sem binários. |
| I01 | Pendente de binário Google | Produtor Core entregue; adaptador Google 0.8.6 e retirada das leituras privadas Google ainda exigem teste conjunto. |
| I02 | Pendente de SDK LinkedIn | Entrypoint, métodos e schemas LI-04 não recebidos; não há adoção externa nesta release. |
| I03 | Pendente de homologação remota | Conta/app/formulário/callback HTTPS e lead/destino autorizados; L07/L14 não encerrados pela bancada. |

## Tickets e encaminhamentos

| Ticket | Resultado |
|---|---|
| CORE-01/02 | Produtor de contexto/catálogo entregue; contrato detalhado em `docs/MEDICAO-SDK-1.33.md`. Google recebe encaminhamento para adaptar consumidor e executar I01. |
| CORE-03 | Recuperação Google Ads segue fora do Core desta entrega; depende de GOOGLE-03/06 e homologação comercial. |
| CORE-04 | Ponte atual encapsulada; contrato definitivo/transferência continuam com implantador. |
| CORE-05 | Documentação e efeito público tratados dentro da matriz disponível; limites A22/A27 declarados. |
| CORE-SOC-01 | Fronteira interna e diagnóstico entregues; adoção externa não implementada por ausência do SDK concreto. |
| CORE-SOC-02 | Roteiro entregue; execução externa pendente (I03/L07/L14). |

O último encaminhamento Google revisão 2 / planos Google 0.8.6 e MCP 0.22 revisão 4 resolve a divergência documental da bridge. Sua implementação e homologação continuam pertencendo aos acompanhantes. Não foram alterados MCP, Google, Meta, LinkedIn, tema ou implantador.

## Arquivos

- `base-site-core-fator3-1.33.0.zip`: instalar no WordPress.
- `base-site-core-fator3-1.33.0-fontes-e-testes.zip`: fontes idênticas ao instalador, scripts de teste, schemas/fixtures, geradores e resumo das evidências. Não instalar esse ZIP como plugin.
- `encaminhamento-core-1.33.0-mcp-google.md` e `encaminhamento-core-1.33.0-meta-linkedin.md`: documentos para o responsável encaminhar. Não foram enviados a terceiros.
- `SHA256SUMS-1.33.0.txt`: integridade dos artefatos.
