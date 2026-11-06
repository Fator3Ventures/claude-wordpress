# Entrega — Fator3 MCP LinkedIn 0.19.0

05/11/2026, America/Sao_Paulo · Revisão 1 · Implementação, correção e validação. **Apta no escopo testado; ativa no Site-Teste.** Homologação de acesso a uma conta LinkedIn real permanece separada.

**Relatório externo canônico.** A cópia congelada no fonte antecede o fechamento; as evidências funcionais são as mesmas. Este relatório externo acrescenta os números finais do fonte.

## 1. De onde esta versão entra

Instalação limpa ou atualização direta da **0.18.0** para **0.19.0**. Base: instalador de 379539 bytes, SHA-256 `1e6c6e398ab2c507d827e428ae3b28099753459ef1b97a04ddf1c3922d819460`; fonte aceito de 2825148 bytes, SHA-256 `a620cd49f037553f5a244c31840ea7dd7f31bb4a5f57093e8e48efc3eeeca5c1`. Identidades públicas, 99 operações, SDK e schema físico 2 preservados.

Pedido direto: nova rodada da análise de código e funcionalidades, melhorias no painel, testes e documentação. Sem novo ID na aba central. Aplicadas `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambas revisão 5 de 02/11/2026. Mínimos: PHP 8.3 e WordPress 7.1.4. Testes locais: PHP 8.3.6, WordPress 7.1.4 e MySQL 8.0.46.

## 2. Convivência e encaminhamentos

| Pacote | Versão inicial no Site-Teste | Versão na troca e na regressão final |
|---|---:|---:|
| Site Core | 1.71.0 | 1.71.0 |
| Fator3 MCP | 0.40.0 | 0.41.0 |
| Google | 0.28.0 | 0.28.0 |
| Meta | 0.20.0 | 0.21.0 |
| Pipedrive | 0.6.0 | 0.7.0 |

Os cinco acompanhantes estavam ativos. MCP, Meta e Pipedrive avançaram por outras rodadas; a instalação do LinkedIn foi precedida por nova leitura do inventário. Os hashes dos instaladores usados estão em `evidence/release0190/packages-tested.json`; o inventário e os hashes dos arquivos principais do site estão em `site-teste.json`. Não houve alteração nos documentos centrais, código ou instalação oficial dos outros plugins por esta rodada.

**Nenhum novo relatório individual de impacto.** A correção de validação protege precisamente os consumidores Lead Sync e CAPI do Core: consultar metadados de um ativo deixou de mudar a revisão da conexão usada pelas concessões. A preparação de jobs e as prévias são internas ao LinkedIn. Não há mudança de SDK, contrato MCP ou necessidade de atualização coordenada de outro pacote. Os testes de prontidão, revogação, transporte MCP e consumidor Core foram executados com os pacotes originais. Isso não certifica todos os fluxos comerciais dos acompanhantes.

## 3. Mudanças e evidência

| Problema reproduzido | Resultado entregue e prova |
|---|---|
| **Validar conta** salvava a prova sobre a própria configuração. Sem editar nada, a revisão passava de 1 para 2 e concessões vigentes perdiam prontidão | A observação passa a um registro cifrado próprio, vinculado à revisão, geração e credencial. A autorização do principal e o contexto são verificados após a chamada remota. A validação manteve a revisão em 1, o leitor de leads utilizável e a CAPI pronta. Mudanças concorrentes e permissão revogada impediram gravar prova obsoleta |
| Prova opcional ilegível prejudicava a leitura da configuração | Uma prova ilegível aparece como `remote_proof:null`, com `remote_proof_error`; as configurações continuam legíveis. Uma validação autorizada substitui a observação por revisão, sem sobrescrever outra escrita concorrente. Falha SQL continua sendo erro. Nenhuma concessão obsoleta é reativada |
| Uma agenda podia ser desativada depois de uma falha de armazenamento, inclusive se o job já tivesse sido inserido e apenas sua confirmação se perdesse | A agenda conserva o horário original e a chave da ocorrência. A tentativa seguinte respeita o intervalo de cinco minutos, adota o job existente e avança a agenda uma única vez. Perda real de autorização continua bloqueando a agenda. Na base, nove de 16 critérios aplicáveis falharam; na versão entregue passaram **19/19**, incluindo corrupção, concorrência e falha SQL |
| Diagnóstico de credenciais percorria repetidamente as mesmas conexões e provas | Para **35 conexões**, a projeção do ciclo de credenciais e escopos caiu de **457 SELECTs para 1** na tabela do plugin. Preservados expiração, vínculo após renovação, estado desconhecido sem prova e ação de incidente. Não houve consulta ao fornecedor, gravação ou exposição de segredos nessa leitura. A contagem não mede tempo total de carregamento do WordPress |
| Abrir Diagnóstico usava filtros de relatório que podiam consultar nomes no LinkedIn. Respostas antigas podiam substituir resultados de outra seleção | **Estado local** e **Verificar acesso a um ativo** têm controles próprios. Abrir a aba usa IDs já salvos; somente a validação explícita consulta o ativo. O estado mostra pendências e ações; detalhes técnicos são carregados ao expandir. Trocar o alvo descarta o resultado atrasado. A base falhou nos três critérios comparáveis de abertura, filtros e ordem de resposta; a versão nova passou nos 12 testes específicos |
| Leitura automática antes da prévia podia sobrescrever nome/orçamento digitados; prévia atrasada podia reabilitar execução, inclusive com alvo diferente | A leitura automática obtém a revisão sem preencher o editor. A leitura explícita recupera valores e moeda. A confirmação fica vinculada ao comando revisado, é consumida antes de aguardar I/O e não é reaproveitada após edição. A tela identifica o efeito de ativar, publicar ou excluir |
| Alterar uma campanha podia reenviar campos não editados ou aplicar a audiência escolhida para outra. Uma edição parcial de datas podia remover ou arredondar o outro limite | A edição envia apenas os campos alterados. A troca de alvo limpa rascunho e segmentação; reler o catálogo mantendo o mesmo alvo preserva a escolha. Uma edição de início/fim recompõe o período pela revisão lida e mantém a precisão da data não editada. **19 dos 22 critérios de gestão falharam na 0.18.0; os 22 passaram na 0.19.0** |
| No celular, uma dica de configuração ficava ao lado do rótulo e o espremia mesmo com espaço disponível | A descrição passou para baixo do controle. Em **390 px**, o rótulo passou de 85 para 266 px e a dica de 177 para **300 dos 300 px disponíveis**. Em desktop, a dica ocupa 422 px, respeitando o limite de leitura de 70 caracteres aproximados |

O guia de primeiros passos, os manuais de administração, gestão, operação, migração e as notas da versão explicam os novos comportamentos, as ações locais e os momentos de consulta ou escrita remota. A documentação histórica permanece identificada como tal.

## 4. Instalação e prova da troca

| Cenário | Resultado observado |
|---|---|
| Build e instalador | 36 arquivos PHP validados por lint; 86 arquivos, incluindo 43 documentos; ZIP determinístico, raiz correta e runtime do fonte idêntico ao instalador |
| Instalação limpa isolada | 12 verificações do diagnóstico de credenciais e 47 dos fluxos anteriores, zero falhas |
| Migração direta 0.18.0 → 0.19.0 | Cinco verificações de migração; sete registros selecionados comparados antes de operar o alvo. Cifras, revisões, cursor, política e recibo incerto preservados |
| Job, agenda, prova de ativo e grants | 19 verificações, zero falhas; HTTP do fornecedor sintético, SQL/locks/transações reais |
| Gestão de anúncios/publicações | 22 verificações de interface e ordem de respostas, zero falhas. HTML, scripts e REST autenticado reais; respostas do fornecedor sintéticas e tentativas indevidas de confirmação interceptadas antes de qualquer escrita |
| Diagnóstico e regressão de interface | 12 verificações específicas e suítes anteriores de 28 e 54 verificações, zero falhas nas execuções finais. Em tentativas simultâneas a bancada atingiu timeout no HTTP local; as suítes foram reexecutadas em bancos separados. O harness de autenticação passou a consumir as respostas de redirect e abrir diretamente a tela sob teste |
| Navegador gráfico real | **42/42** no Chrome Headless Shell 152.0.7940.0 com sandbox, em **1440×900 e 390×844**. Seis abas, login, foco por teclado, opções de remoção, autoteste e geometria de controles. Sem transbordamento horizontal nos estados medidos e sem erros JS. Em bancada, a base falhou nos dois critérios de posicionamento da descrição |
| Regressão integrada vigente | **443 verificações declaradas, zero falhas** sobre o ZIP final e o conjunto da seção 2. Um cenário histórico específico de outra origem é não aplicável à instalação limpa. Sem entradas de erro do plugin ou acompanhantes no log da execução final |
| Documentação pelo executor MCP local | 43 documentos completos, 52 páginas, 66 verificações, zero falhas. Índice, limites de UTF-8, revisão, bytes e conteúdo do ZIP conferidos |

Os JSON de evidência, incluindo a comparação da base, ficam em `evidence/release0190/`. As imagens de comparação são geráveis na bancada por `tests/native/webui019.php`; o fonte guarda o teste, os hashes e as medidas. As suítes se sobrepõem: seus números não são um total de casos únicos.

**Site-Teste:** `https://fator3-teste-mcp-1.dreamhosters.com/`, via WP MCP fator3-teste. Uma atualização direta da 0.18.0 com o SHA-256 da seção 8, slug `wp-mcp-linkedin-fator3` e chave idempotente. Operação `d40bcef315b8fb96d2a7cff8191b0e21`; backup de arquivos `b14dab2a7ac53c7c057e7425`; `applied:true`, ativo. As sondas internas de `/` e `/wp-json/` retornaram **HTTP 200** antes e depois.

Em leitura independente, **0.19.0**, `linkedin/status` com `state:ok`, zero conexões e agendas ativas; `selftest` com nove itens locais aprovados. A lista de conexões retornou a página vazia esperada. O manifesto e o arquivo principal coincidiram com o instalador. Pelo MCP 0.41.0, os hashes e tamanhos do índice coincidiram nos 43 documentos. Sete manuais, incluindo o schema longo, foram lidos na íntegra em nove páginas e comparados byte a byte. Os cinco acompanhantes mantiveram versão, ativação e hash de seu arquivo principal entre imediatamente antes e depois da troca LinkedIn. Não foram criadas contas, jobs ou anúncios sintéticos no site compartilhado. A distribuição para produção e a publicação raw permanecem a cargo da frota.

## 5. Banco, migração e correção por nova versão

O schema físico continua em 2; não há tabela nova nem conversão em massa. A prova nova usa o bucket cifrado `validation_proof` apenas após validação explícita bem-sucedida. Observações antigas permanecem históricas. Um job inserido com confirmação local perdida continua identificável por sua chave original; o atraso de retry fica no registro da agenda. Conservam-se estado da fila, salts e mecanismos de revisão. A prova do instalador cobre arquivos, não reversão de banco. Em caso de falha, preserve os dados, reconcilie efeitos incertos e corrija em nova versão.

## 6. Pendências e limites

- **Dono/frota:** confirmar permissões, acesso real a ativos, webhooks e conversões numa conta autorizada. O Site-Teste não tem conexão LinkedIn configurada. Não houve gasto Ads, publicação, envio de conversão, criação de contato comercial ou implantação em ctooffice nesta rodada.
- **Visual:** Chrome em duas larguras e estados delimitados. Não há certificação de Safari, Firefox, leitor de tela, aparelho físico ou de todas as combinações de formulário.
- **Desempenho:** a medição mostra número de consultas da projeção de credenciais, não latência ponta a ponta, consumo de toda a página nem desempenho de fornecedor.
- **Acompanhantes:** os contratos pertinentes e a convivência foram verificados; não se retestaram todas as funcionalidades comerciais dos outros pacotes.

## 7. Credenciais e configuração do dono

Nenhum novo segredo é necessário para a atualização. A entrada administrativa continua em Ferramentas → Fator3 MCP LinkedIn. Para validar acesso real, escolha a conexão ativa e o ativo já autorizado; o aplicativo precisa dos escopos/produtos correspondentes. Credenciais salvas não são exibidas. O autoteste e o estado local não aprovam acesso ao fornecedor. As provas desta rodada usam apenas dados sintéticos ou estado operacional não secreto.

## 8. Identidade dos arquivos

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| `wp-mcp-linkedin-fator3-0.19.0-instalador.zip` | 397354 | `613cb47cfb3be2b91dfa1f20f39c465780a6fffb5432b645290448fe592a0f0c` |
| `wp-mcp-linkedin-fator3-0.19.0-fonte.zip` | 3056323 | `25f3458b99584a68bb56920c12ef828508d6cb0f2c72eceb0921d24d3eae3a62` |

Somente o instalador é instalável. O checklist da seção 14 do padrão foi conferido: requisitos, identidade, preservação, instalação limpa, atualização, testes, documentação, impactos, conteúdo e estado final do site. Limites ainda abertos constam na seção 6.
