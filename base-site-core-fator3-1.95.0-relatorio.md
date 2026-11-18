# Entrega — Fator3 Site Core 1.95.0

**18 de novembro de 2026 · Implementado, instalado e confirmado no Site-Teste.** O executor registrou a conclusão às **20h17min42s de Brasília**, com zero falhas. A bancada validou o quórum do MCP 0.50.0 e a entrega do diagnóstico de permissão IAM do Google 0.38.0. O aceite em produção e a confirmação na caixa postal ficam com os operadores.

## 1. Origem e requisitos

Instalação nova em WordPress ou atualização direta do Core 1.94.0 para 1.95.0. A troca usa um único instalador. O ZIP de base tinha 5.668.055 bytes e SHA-256 `0eff84a92622b3daa2aebd81437bbb2c33eaea648d1955c46e29ef70aedf9008`. O fonte oficial de partida tinha SHA-256 `bb4e4c4058c8b3e2511cf55a8fb198c5219c3178d48bae5826f91f36a7d7bb8c`. Os patches recebidos serviram para identificar as mudanças de contrato entre as equipes.

Requisitos do pacote: WordPress 7.1.4 ou superior, instalação única e PHP de 64 bits a partir de 8.3. A bancada exerceu WordPress 7.1.4 com PHP 8.3.6 e 8.4.27. No Site-Teste, o MCP informou WordPress 7.1.5 e PHP 8.3.36. Documentos centrais lidos e conferidos: `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos na revisão 5, de 02/11/2026. Também foram aplicadas a regra comum e a aba específica do Site Core.

## 2. Contratos, versões e ordem de troca

Contrato administrativo `8.45.0`, perfil `piso-padrao-3.6`, 104 opções operáveis e 199 operações de domínio. A release amplia a resposta de `f3base/incidentes-tecnicos-ler` com o bloco opcional `iam`. A contagem, os nomes das operações, o acesso administrativo e os campos de configuração foram preservados. O dicionário de dados instalado passa a indicar a base efetiva de atualização 1.94.0.

| Componente | Bancada integrada | Site-Teste após a troca | Verificação própria |
|---|---|---|---|
| Site Core | 1.95.0 | 1.95.0 | Instalação nova, migração direta, fila, contexto do incidente e documentação |
| MCP | 0.50.0 | 0.50.0 | Seis requisições HTTP de registro, efeito de CLI e leitura administrativa autenticada |
| MCP Google | 0.38.0 | 0.37.0 | Produtor oficial, coleta IAM, GA4 com resposta simulada e aviso entregue ao transporte de ensaio |
| LinkedIn | 0.26.0 | 0.26.0 | Aberturas repetidas e recuperação pelo produtor |
| Meta | 0.29.0 | 0.29.0 | Worker, coleta e deduplicação do incidente de agenda |
| Pipedrive | 0.12.0 | 0.12.0 | Leitura do incidente sintético na projeção do pacote |

Para distribuir o conjunto completo, instalar MCP 0.50.0 antes do Core e disponibilizar Google 0.38.0 para o diagnóstico IAM. O coletor do Core enriquece uma abertura anterior assim que o Google expõe o contexto. No Site-Teste, a única troca desta rodada foi a do Core. Na bancada integrada, comparamos todos os arquivos dos seis runtimes instalados com os ZIPs oficiais. Houve zero divergências.

## 3. Pedidos implementados e encaminhamentos

| Pedido | Implementação | Resultado observado |
|---|---|---|
| Core 430 / MCP 86 | O MCP decide a indisponibilidade do registro. O observador do Core delega ao método local do canal. O Core continua responsável pela fila, entrega, reconciliação e histórico. | Uma falha isolada seguida de saúde gerou zero incidentes no Core. Duas falhas HTTP consecutivas em requisições distintas abriram um único episódio. A primeira leitura saudável seguinte o recuperou. Os observadores foram chamados várias vezes dentro da mesma requisição e também por WP-CLI. O histórico registrou somente abertura em cron HTTP e recuperação web, ambas pelo publicador do canal. |
| MCP Google 56 | O Core aceita a permissão fixa e o identificador público do projeto para o evento de leitura dos metadados da chave. O assunto do aviso especifica “validade da chave não consultável”. A recuperação utiliza a mesma referência e o corpo inclui o projeto, quando disponível. | 16 verificações com o Google 0.38.0. A consulta simulada ao IAM retornou 403 de permissão, a consulta GA4 funcionou e houve uma mensagem de abertura. As novas observações conservaram o episódio. O teste distinguiu recusa de token, serviço IAM indisponível e recuperação. |
| MCP Google 56, episódios existentes | O coletor usa a mesma identidade do produtor. Dados acrescentados depois da abertura completam o registro. Uma abertura em fila pode ganhar os detalhes enquanto está pendente. | A migração de um episódio já notificado preservou a data, o identificador e o recibo da 1.94.0. Duas coletas pelo Core 1.95.0 resultaram em zero novos e-mails. Uma leitura MCP HTTP autenticada confirmou a permissão e o projeto. Onze verificações de fila e acesso passaram em cada uma das versões PHP 8.3.6 e 8.4.27. |
| Retorno do MCP 84 | A edição MCP 0.49.0 já incorporou a inscrição tardia de rota solicitada na rodada 1.94.0. A entrega atual usa o sucessor oficial 0.50.0. | O relatório recebido documenta a incorporação na 0.49.0. A prova própria exerceu o novo pacote em conjunto com o Core sob inicialização precoce, CLI, web e cron HTTP. |

O fonte conserva as propostas originais, as revisões de planejamento e as respostas finais em `reference/1950/`. Os encaminhamentos de entrega são [base-site-core-fator3-1.95.0-impacto-wp-mcp-fator3.md](base-site-core-fator3-1.95.0-impacto-wp-mcp-fator3.md) e [base-site-core-fator3-1.95.0-impacto-wp-mcp-google-fator3.md](base-site-core-fator3-1.95.0-impacto-wp-mcp-google-fator3.md). Os três outros produtores testados conservaram seus contratos. A análise das interfaces do Implantador dispensou mudança nesse pacote.

## 4. Instalação e prova da troca

| Verificação | Evidência |
|---|---|
| Instalação limpa e migração oficial | Em dois bancos independentes, a instalação nova e a atualização de 1.94.0 percorreram 20 etapas, terminaram com zero falhas e receberam confirmação do executor. |
| Integridade do pacote | O instalador contém 1.278 arquivos na raiz do plugin. Todos coincidiram com a árvore fonte. Os 611 PHP passaram na verificação sintática. O inventário do runtime em relação à 1.94.0 registra dois novos documentos e 24 arquivos alterados. |
| Aplicação no Site-Teste | O canal reconstituiu os 5.671.022 bytes e conferiu o SHA-256. A habilidade `plugins/upload-base64` usou `zip_path`, slug e hash esperados, pré-imagem e chave de idempotência. As sondas da home e de /wp-json/ retornaram HTTP 200 antes e depois. A releitura do caminho temporário confirmou a remoção do ZIP. |
| Prova pelo MCP | `plugins/list` confirmou o Core ativo. A primeira leitura de `f3base/como-usar` ainda indicava atualização pendente. Em processo posterior, a projeção compacta trouxe `versao_alvo=1.95.0`, `estado=concluida`, `falhas=0` e `confirmada_no_executor_em=1795043862`. A confirmação depende da passagem do executor após a troca. Nesse site, ocorreu seis segundos após o início do ciclo. |
| Documentação instalada | O índice forneceu a nota da release. As 24 linhas de `docs/RELEASE-1.95.0.md` foram lidas em três páginas, remontadas e comparadas byte a byte com o arquivo entregue, SHA-256 `bbc939e61b1e453b74882c88cc8deced28e3ce64ba807de13ed4874223dd542b`. O guia `docs/AGENTES-1.95.0.md` também foi lido e comparado integralmente. Uma consulta fora do índice retornou `documento_nao_catalogado`. |
| Estado final | Saúde MCP positiva e destino técnico configurado. Antes e depois da troca, os três registros consultados tinham zero entregas pendentes. O incidente de registro continuou recuperado, com uma entrada histórica. O aviso preexistente de vencimento de refresh do canal constava como aberto nas duas leituras. |

As evidências sanitizadas estão em `evidence/1950/`, inclusive os recibos dos dois bancos locais, o aceite HTTP e a homologação do Site-Teste. Para distribuição, a frota confere o hash do instalador servido pelo fluxo oficial e usa `plugins/upload` com o slug e SHA-256 esperados.

## 5. Persistência, recuperação e permissões

O novo campo opcional `iam` é gravado sob a trava existente na opção do incidente. Dentro da fila, o contexto é registrado por transição. No enriquecimento, o Core distingue a última abertura pendente de episódios anteriores mesmo quando têm o mesmo horário. Uma entrega que já recebeu reserva continua exigindo a reconciliação administrativa existente. A identificação do recurso usa a referência opaca do site.

O ciclo de instalação reutiliza suas 20 etapas. O armazenamento continua nas opções existentes. O diagnóstico dispensa tabelas, capacidades e opções novas. Episódios antigos recebem dados na próxima coleta aplicável. As correções posteriores seguem em versão nova. E-mails que o WordPress já entregou ao transporte e decisões de reconciliação já registradas têm efeitos próprios.

## 6. Pendências de aceite

- **Frota.** A observação de 24 horas nos 11 sites começa após a distribuição coordenada do MCP 0.50.0 e do Core 1.95.0. Comparar as novas transições com as passagens de WP-CLI e a saúde do canal. A produção ficou fora desta implantação.
- **Responsável Google e operador da caixa técnica.** Confirmar abertura e recuperação em conta de serviço real e o recebimento na caixa autorizada. A bancada usou o plugin Google oficial com respostas IAM, OAuth e GA4 simuladas e e-mail interceptado no WordPress. O Site-Teste continuava na versão Google 0.37.0.
- **Cobertura da rodada.** Houve ensaios de acesso administrativo e do visitante pelo WordPress e MCP. Não houve inspeção visual em navegador nem teste de tráfego comercial. A interface alterada foi o conteúdo do aviso e do resultado administrativo. A emulação das falhas ficou restrita a bancos descartáveis. Os quatro bancos e as respectivas instalações foram removidos após as verificações.

## 7. Credenciais e configuração do dono

A release reutiliza as credenciais e o destinatário configurados. O endereço de avisos fica em **Site Core → Avisos técnicos por e-mail**. Para conferir o estado da conta de serviço, use o painel de identidade do MCP Google. O relatório e o instalador dispensam o compartilhamento de credenciais ou dados da caixa.

## 8. Identidade dos arquivos

| Arquivo | Tamanho em bytes | SHA-256 |
|---|---:|---|
| [base-site-core-fator3-1.95.0-instalador.zip](base-site-core-fator3-1.95.0-instalador.zip) | 5671022 | `6971df93ecf39e14e584e0fc3dc802aee77ab4f2d58eb5b8ce35d6a503a4c21c` |
| [base-site-core-fator3-1.95.0-fonte.zip](base-site-core-fator3-1.95.0-fonte.zip) | 8224196 | `3f05a234fa5edf844ced5bb79bc1b79116cab39186ce7954bb78ab819903d638` |

O ZIP fonte contém o código, os geradores, os testes, os pedidos recebidos e as evidências desta rodada. O fonte inclui uma cópia deste relatório anterior ao cálculo da identidade do próprio ZIP.
