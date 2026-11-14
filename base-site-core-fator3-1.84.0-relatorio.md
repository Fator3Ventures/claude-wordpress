# Entrega do Fator3 Site Core 1.84.0

Revisão 1 · 13/11/2026 (Brasília) · Pedidos 398 e 399 · Contrato de configuração 8.40.0
Slug WordPress `base-site-core-fator3`. **Implementada, testada e ativa no Site-Teste.** O aceite externo nas contas de mídia e a implantação em produção continuam pendentes.

## Alterações

**398. Medição de links.** A medição própria registra os cliques em a[href] na métrica f3base_clique_link. O evento traz tipo, destino, seção, alvo, classe de clique, texto visível e indicação de nova aba. A URL gravada exclui credenciais, query e fragmento. A rota protegida de download omite o identificador do arquivo. Tel e mailto guardam o endereço do link. Outros esquemas guardam só o protocolo. O teto é de 100 cliques por documento e a fila compartilhada suporta 100 eventos pendentes. A captura e o reenvio dependem de autorização para medição. Um identificador repetido confirma o mesmo clique. Um conteúdo conflitante sob o mesmo identificador recebe HTTP 409.

A tabela de eventos recebe sete colunas. A análise grava o evento e os dados de sessão na mesma transação. A consulta administrativa pode contar por destino, seção ou alvo, paginando por fotografia com cursor assinado e respeitando janela e segmento. O relatório editorial soma cada saída externa em seguintes na página de origem com navegação pareada. A abertura efetiva no outro site depende dos registros desse destino. Os campos antigos permanecem consultáveis. Somar a métrica detalhada às métricas legadas conta algumas interações duas vezes.

**399. Conversão de formulário.** A reserva de aquisição, as filas de servidor, o reprocessamento da Meta e a confirmação no navegador aplicam a distinção entre clique e formulário. Um CTA recebe clique_sem_formulario. O registro do contato e a intenção de aviso continuam seguindo a configuração do site. A opção f3base_converter_contato_sem_identificador passou a vir desligada. Se estiver explicitamente ligada, permite a exceção do telefone livre preenchido e não normalizado, sem e-mail válido. O bloqueio de CTA vale nos dois estados. O comportamento dos envios válidos de formulário permanece sujeito a consentimento, deduplicação, transporte, política de testes e configuração do destino. A versão não revisa eventos já aceitos pelos fornecedores.

## Instalação, conjunto e normas

Instalação limpa ou atualização direta do Core 1.83.0. Requisitos mínimos de WordPress 7.1.4 e PHP 8.3 de 64 bits. Laboratório com WP 7.1.4, PHP 8.3.6 e MySQL 8.0.46. Site-Teste com WP 7.1.4 e PHP 8.3.36. A instalação ocorreu somente no Site-Teste.

Normas do projeto lidas em sua revisão 5, de 02/11/2026.

| Fonte | SHA-256 |
|---|---|
| instrucoes-agentes-plugins-fator3.md | `f0c48263597444bf304be515e3a61d268751c47cd5eaf7dfcfa9db7ea47773fc` |
| padrao-desenvolvimento-plugins-fator3.md | `6dd73913cf41f0157a8e68cf922cbc2b97757537488fcf441ef67a9dee5e3166` |
| Fonte 1.83.0 | `462082c8ad085140d7c657a90df3e31ac7d99df09b6c4d3380918183d6db0677` |
| Instalador 1.83.0 | `9168a066d0e85468be3580afc88a1b063bf36b80ad8ab84b0b0ca57f4cc322cf` |

| Pacote acompanhante | Versão examinada | Resultado |
|---|---|---|
| Fator3 MCP | 0.45.0 | Descoberta e execução da leitura, agrupamentos e transferência verificada no WordPress de teste. |
| Google | 0.34.0 | Ativo no Site-Teste. Matriz do adaptador e worker aprovada em laboratório. |
| Meta | 0.25.0 | Ativo no Site-Teste. Matriz do adaptador e worker aprovada em laboratório. Bloqueio anterior ao despacho verificado. |
| LinkedIn | 0.22.0 | Ativo no Site-Teste. Matriz do adaptador e worker aprovada em laboratório. |
| Pipedrive | 0.10.0 | Ativo no Site-Teste. Regressões locais de origem e mapeamento da ficha aprovadas. |
| Implantador | 2.21.0, referência da base | O Core mantém o formato de consumo existente. A pendência documental do pedido 397 continua registrada no impacto da 1.83.0. |

Os pedidos 398 e 399 são resolvidos no Core. Os adaptadores existentes continuam recebendo somente envios que passaram pela seleção do Core. Os agrupamentos são aditivos ao esquema descoberto pelo MCP. Nenhum dos dois pedidos exige nova implementação nos acompanhantes. O plano, o anexo e o impacto histórico da base estão no fonte.

## Verificação

| Ambiente | Execução e resultado |
|---|---|
| Instalação limpa | 595 verificações registradas nos arquivos fresh--*.json. Incluem 45 verificações específicas de 398/399 e 89 de origem. |
| Migração 1.83.0 → 1.84.0 | 607 verificações nos arquivos upgrade--*.json. 993 amostras e a configuração sementes conferidas após a troca. Reativação e reinstalação do ZIP verificadas. |
| Integridade | 970 arquivos do instalador conferidos individualmente, lint de 602 arquivos PHP, 84 arquivos JS recompilados com Terser 5.44.1. Os 84 e o manifesto compilado ficaram idênticos byte a byte. |
| SDKs de navegador | Chromium 156 com o bundle de produção. Dois métodos de CTA, inclusive diante de resposta elegível simulada, geraram zero comandos. O formulário aceito acionou generate_lead (GA4), conversion (Ads), Lead (Meta), track (LinkedIn) e a função de conversão do Clarity. SDKs instrumentados, sem envio a contas de anúncios. |
| WordPress remoto | Atualização conferida por SHA-256 e slug, sondas antes/depois e processo PHP independente. Operação `720f1bb8f122d20ffed7efce8a15e63c`. Leitura integral das notas pelo MCP. 194 abilities próprias no laboratório. |
| Formulário real de teste | O formulário servido pelo Site-Teste aceitou celular novo, retornando HTTP 201, metodo whatsapp_formulario e conversao.elegivel=true. O Site-Teste usa navegador para GA4, Google Ads e LinkedIn. Um ensaio separado com automação declarada acionou audiencia_excluida e outro com telefone repetido acionou a deduplicação por destino. |
| Cliques e avisos | Quatro capturas whatsapp_cta. Todas receberam clique_sem_formulario. Cada uma tinha recibo Slack entregue/slack_thread_completa, zero fila de servidor, zero fila CAPI e zero Lead no registro Meta associado ao evento. O total de testes incluiu sete contatos sintéticos. |

**Eventos relidos em f3base/eventos-ler no Site-Teste**. As âncoras do cabeçalho e do diálogo pertenciam ao site. Os quatro links genéricos e a superfície de barra fixa foram inseridos no DOM daquela sessão para testar os casos controlados. O ensaio impediu a navegação externa e usou a coleta HTTP real. A consulta agrupada contou sete eventos em seis destinos, quatro seções e sete alvos.

| Superfície | Tipo | Seção | Alvo | Destino normalizado |
|---|---|---|---|---|
| Link interno | interno | qa1840 | qa1840~qa1840:controle:1 | `https://fator3-teste-mcp-1.dreamhosters.com/qa-interno/` |
| Link externo | externo | qa1840 | qa1840~qa1840:controle:2 | `https://example.org/qa1840` |
| E-mail | e-mail | qa1840 | qa1840~qa1840:controle:3 | `mailto:qa@example.test` |
| Telefone | telefone | qa1840 | qa1840~qa1840:controle:4 | `tel:+5511999999999` |
| Cabeçalho WhatsApp | externo | topo | topo~topo:controle:10 | `https://wa.me/5511936203481` |
| Barra fixa WhatsApp | externo | barra-fixa | barra-fixa~barra-fixa:controle:1 | `https://wa.me/5511999999999` |
| Link direto do diálogo | externo | dialogo-contato | dialogo-contato~dialogo-contato:controle:17 | `https://wa.me/5511936203481` |

O caso editorial foi exercitado no WordPress local. Três cliques no mesmo destino externo produziram contagem três em seguintes. O ensaio de reenvio e paginação também foi executado na instalação limpa e na atualização. A entrega às contas efetivas de GA4, Google Ads, Meta, LinkedIn e Clarity permanece sem comprovação externa nesta rodada.

## Estado final e materiais

O Core 1.84.0 permaneceu ativo no Site-Teste. Os sete contatos sintéticos e as linhas de sessão verificadas foram limpos. Arquivos de transporte e ferramenta PHP temporária foram removidos. A homologação gerou avisos no Slack pelo fluxo configurado. Os recibos e diários operacionais seguem a política de retenção do site. A frota de produção permanece fora desta implantação.

A árvore fonte inclui work/plugin/base-site-core-fator3, a base imediata em history/1.83.0-runtime, testes, ferramentas de build, referência e evidência em evidence/1840. O instalador usa uma única raiz base-site-core-fator3. A cópia de pré-fechamento do relatório no fonte precede o hash do próprio ZIP. A documentação de uso e os esquemas estão instalados em docs/.

| Pacote | Bytes | SHA-256 |
|---|---:|---|
| base-site-core-fator3-1.84.0-instalador.zip | 4462127 | `b1f1d28792e6c873292d7f26273da8a0ca056b7a3b38b0b5e56a8d95df6bb460` |
| base-site-core-fator3-1.84.0-fonte.zip | 57029293 | `fbf94b97a74a5038fda7bd6c7baa67bcdd7ed06de09afec17db18b731dfe9ec6` |
