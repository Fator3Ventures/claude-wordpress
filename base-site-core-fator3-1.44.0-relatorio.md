# Entrega — Fator3 Site Core 1.44.0

Revisão 1 · 21/10/2026 · Implementação e entrega de release sobre a 1.43.0.

**Classificação: com-pendencias.** Implementação validada no laboratório e atualização concluída no Site-Teste, sem falhas de migração. Disponível para implantação controlada pela frota; aceites com contas reais, dados novos e os sites citados permanecem discriminados abaixo. Não houve publicação no GitHub nem atualização dos demais sites nesta rodada.

Escopo: **Pedidos core 246, 248, 249, 256 e 258–263**. Contrato administrativo **8.9.0**; 136 abilities do Core. O pedido adicional 263 integra esta entrega, com captura privada do valor digitado conforme a decisão do dono.

## 2. De onde a versão entra

- Instalação nova em WordPress limpo e atualização direta **1.43.0 → 1.44.0**, ambas exercitadas com o instalador final pelo Plugin_Upgrader. Não há versão intermediária a instalar.
- Base: fonte 1.43.0 e instalador 1.43.0, preservados. Instalador anterior: 2.091.980 bytes, SHA-256 `5a7c02abb97f7161617ddfd8e4d28faf2fdb22e4ae5d4ed75416dc68d76ee9e7`. Fonte anterior: 2.968.306 bytes, SHA-256 `04a1fb6196327aa32418630905088c5a366067c971472cf00510876e737db3fd`.
- Requisitos usados: `Fator3 Site Core(20261021-141715).md`, instruções comuns dos agentes, padrão de desenvolvimento dos plugins e pedido 263 recebido no chat em 21/10/2026. Os itens já entregues pela 1.43.0 não foram reabertos.
- Cabeçalho declara WordPress ≥ 7.1.2, PHP ≥ 8.3.6 de 64 bits, instalação única. Prova local: WordPress 7.1.3, PHP 8.3.6, MySQL 8 e Chromium 153.0.8010.0. O mínimo exato WordPress 7.1.2 não foi reexecutado.

## 3. Convivência

| Pacote | Versão examinada e ativa no Site-Teste | Escopo da prova |
| --- | --- | --- |
| Fator3 MCP | 0.25.0 | Atualização pelo canal de pacotes, sondas e execução das abilities novas; operação concluída. |
| Fator3 MCP Google | 0.16.0 | SDK público de destinos e reconciliação, fixtures de autorização, idempotência e recibo incerto; sem ingestão real em anúncios. |
| Fator3 MCP LinkedIn | 0.4.1 | `linkedin/admin-options` real do pacote com respostas externas simuladas: formulários, campanhas, paginação e revisão. |
| Fator3 MCP Meta | 0.4.1 | Inspeção dos contratos pertinentes e coexistência ativa; nenhuma publicação ou conversão real usada como teste. |

O Core consome interfaces públicas já existentes. **Não foi identificada mudança necessária nos outros pacotes dentro do escopo examinado**, nem ordem nova de troca. Nenhum pacote complementar foi modificado; não há relatório individual de impacto apenas para anunciar esta versão. Conta real e resultado do fornecedor não são inferidos da coexistência ativa.

## 4. Mudanças e evidência

| Pedido | Problema e resultado entregue | Estado e prova |
| --- | --- | --- |
| Pedidos core 246 | Datas de conferência Meta e início Search Console usam seletor nativo. Data/hora de qualidade e consentimento usa o fuso do WordPress, recusando datas inválidas e horários inexistentes em transição de fuso. Revisão dos textos das 20 áreas renderizadas, com lista abaixo. | implementado; validado-localmente em PHP e Chromium. A cobertura automatizada de textos e a inspeção por assunto não equivalem a aceite visual em cada tema da frota. |
| Pedidos core 248 | Seções de mapeamento do Pipedrive têm títulos distintos por assunto, inclusive pessoa e respostas de formulários. | implementado; validado-localmente, unicidade de títulos e edição estruturada em navegador. |
| Pedidos core 249 | Cliente Plugin LinkedIn descobre formulários pelo canal leads e campanhas pelo canal ads usando `linkedin/admin-options`. Paginação confere revisão; descobrir não muda cliente, credencial, seleção nem concessões. | implementado; validado-wordpress em laboratório, 8 verificações com o plugin 0.4.1. Conta externa real pendente. |
| Pedidos core 256 | Nota inicial do Pipedrive mostra a data local em `d/m/Y H:i:s P`, com deslocamento. Notas anteriores não são reescritas. | implementado; validado-localmente, conteúdo da nota conferido com fuso. Próximo contato em conta real pendente. |
| Pedidos core 258 | Comparação anterior informa dias retidos e `anterior_parcial`; nenhuma audiência retida mantém totais nulos. Explica sessões observadas versus sessões cujo início foi observado dentro da janela. | implementado; validado-localmente para cobertura completa, parcial e ausente. Releitura de fator3.com.br e apuração dos 9 versus 3 em conselar pendentes. |
| Pedidos core 259 | `f3base/conversoes-recuperar` admite captura aceita com transporte navegador ou ausente mediante confirmação explícita de não entrega e referência atualmente pronta. Audita usuário, data e vínculo; preserva transporte original. Simulação explica inelegibilidade sem gravar. | implementado; validado-wordpress em laboratório: elegibilidade, consentimento, clique único, 90 dias, vínculo, concorrência e uma entrega por destino. Recuperação real dos registros 113 e 125 não realizada. |
| Pedidos core 260 | Amostra INP guarda interação, alvo estrutural, fases e origem de script quando Long Animation Frames está disponível. LCP guarda tipo/alvo, recurso sem query/fragmento/credencial e fases disponíveis. Nova `f3base/vitais-ler` filtra período/caminho/métrica/dispositivo e apresenta p75, alvos, scripts e fase dominante. | implementado; validado-localmente em PHP e Chromium; ability executada no Site-Teste com acervo vazio. Sete dias de dados novos em ctooffice pendentes. |
| Pedidos core 261 | Automação, motivos e regra ficam na própria amostra; padrão exclui provável/declarada e legado sem classificação, com contagens. `automacao=todas` permite inspeção explícita. | implementado; validado-localmente e migração de amostra antiga comprovada como legado desconhecido, valor preservado. P75 real dos sites após troca pendente. |
| Pedidos core 262 | Folha pequena dos formulários fica inline no head, antes da folha do tema, mantendo a sobrescrita do tema. | implementado; validado-localmente e validado-wordpress no Site-Teste: HTML contém o bloco inline e não referencia `/assets/f3base-formularios.css`. PageSpeed dos sites-alvo pendente. |
| Pedidos core 263 | Fotografia dos campos da etapa na tentativa barrada: nome, estado, regras, motivo de telefone e valor; sequência ligada à sessão e instância. Correção, envio confirmado e saída observada; ability privada, agregação sem valores, retenção, interruptor e eliminação por sessão. | implementado; 33 verificações PHP e 24 de navegador; leituras executadas no Site-Teste. Captura/eliminação funcional comprovada com dados sintéticos locais; aceite posterior à troca em ctooffice pendente. |

### Detalhes do pedido 263

Em **Site Core → Configurações → Privacidade e segurança → Retenção**, os controles são **Tentativas barradas — guardar o valor digitado** e **Dias de guarda das tentativas**. Padrão ligado e **30 dias**; configurável entre 1 e 90. Desligar bloqueia novas gravações de valores no navegador e no servidor, inclusive com página em cache. Os registros anteriores seguem sujeitos à retenção e à eliminação.

A fotografia contém os campos ativos da etapa, inclusive vazios e preenchidos, quando o envio é barrado. Regras nativas incluem `valueMissing`, `typeMismatch`, `tooShort`, `tooLong`, `patternMismatch`, limites numéricos, `stepMismatch`, `badInput` e `customError`; também há `exigir-um-de`, formato de telefone com motivo e limite de arquivo sem o conteúdo/nome do arquivo. Os casos `98765-4321` e `(11) 98765-432` preservam respectivamente o motivo de ausência de DDD e quantidade de dígitos, mesmo com a mensagem do grupo apresentada no Celular.

Página, diálogo e etapa 2 usam o mesmo mecanismo. A instância acompanha as etapas; cada evento tem identificador idempotente e sequência. Correção é observada no `change` de campo anteriormente recusado; envio exige registro aceito no servidor e, na etapa 2, complemento registrado. Fechamento/saída observado não prova abandono definitivo. Sem sessão de medição disponível, a sessão operacional fica apenas na memória da página, sem novo identificador persistente. Bloqueio de JavaScript/rede ou encerramento precoce pode impedir a captura.

`f3base/formularios-tentativas-ler` exige **f3base_ler_leads**; `manage_options` sozinho não basta. Filtros: formulário, sessão, instância, período no fuso do site, segmento e paginação por `apos_id`; limite até 100. A consulta privada entrega o valor ao operador autorizado. `f3base/comportamento-ler` acrescenta `recusas_por_campo`, sem descriptografar: contagens por formulário, campo e regra. Nessa rota, os filtros novos de formulário/sessão se aplicam somente ao bloco detalhado, pois o agregado histórico não possui essas dimensões. Até 50.000 tentativas, a contagem é exata; acima disso informa corte.

Valores ficam cifrados na tabela própria do WordPress por sodium secretbox, com chave derivada do salt `secure_auth`. Não entram nos registros de lead, filas comerciais, Slack, e-mail, webhook, Pipedrive, GA4, Meta ou Clarity. Não há evento novo nessas plataformas contendo o valor. A única saída funcional do valor é a leitura privada solicitada pelo operador. Não são capturados senha, token, honeypot, campos ocultos ou arquivos. Valores extensos são limitados a 4.000 unidades de texto por campo e ao orçamento de 59 KB por fotografia, com `valor_truncado=true`; isso não modifica o envio comercial.

O endpoint valida token/revisão do formulário, campos/regras permitidos, formato, tamanho e origem declarada; aplica limites de 180 registros por origem/10 minutos e 200 por sessão/dia, além de locks de instância/sessão. Uma falha de diagnóstico não impede o envio do contato nem devolve seu valor no erro.

A leitura não mostra registros vencidos mesmo se o cron atrasar; a limpeza física usa os jobs existentes de retenção/notificações. `f3base/leads-eliminar-registro` usa a eliminação canônica e remove tentativas de **todas as instâncias da mesma sessão**. Falha impede declarar a eliminação concluída. Marcadores opacos por 91 dias impedem a recriação por repetição tardia, sem conservar valores. O fluxo de eliminação de dados pessoais do WordPress também remove sessões pelo HMAC do e-mail capturado, mesmo sem lead aceito. Sem e-mail digitado nem vínculo conhecido de sessão/contato, não se infere a identidade de formulário anônimo vazio.

### Limites históricos de desempenho

As **54 amostras de LCP** do pedido 261 não podem ser reclassificadas como humanas por aproximação. O acervo de amostras conserva a última emissão por carregamento, enquanto eventos históricos guardavam a primeira, com chaves e retenção próprias. Isso explica por que a igualdade por dia/caminho/métrica/valor não constitui vínculo confiável, mas não identifica individualmente a causa das 54 ausências. A partir desta release, classificação e atribuição acompanham a amostra. Ausência de sinal de automação continua não sendo prova de pessoa humana.

### Lista efetiva dos textos alterados — pedido 246

Foram alteradas 31 descrições de configuração, além dos rótulos, títulos e instruções relacionados abaixo. A revisão percorreu as 20 áreas renderizadas, com cobertura automatizada e inspeção por assunto. Não reescreveu documentos históricos nem removeu formatos técnicos necessários a payloads de webhook, cotas UTC ou nomes de logs. Lista completa também instalada em `docs/TEXTOS-1.44.0.md`.

| Campo | Descrição na 1.44.0 |
| --- | --- |
| `f3base_formularios` | Edite os campos, as etapas, as mensagens e os destinatários em Site Core → Formulários. Cada formulário tem uma revisão própria; salve suas alterações antes de editar outro. |
| `f3base_email_novo_lead` | Envia uma resposta automática após a confirmação de um novo lead no Pipedrive. Configure a conta de envio, os textos e a cota por hora. Cada destinatário, inclusive cópias ocultas, consome uma unidade dessa cota. |
| `f3base_meta_janela.conferida_em` | Escolha o dia em que os limites da Meta foram conferidos na documentação oficial. A conferência vale por 90 dias. |
| `f3base_gsc.inicio` | Escolha o primeiro dia da série que deseja importar. Vazio começa nos últimos 30 dias disponíveis. Períodos maiores são preenchidos em passagens sucessivas. |
| `f3base_gsc.ativo` | Coleta dados quando o MCP Google estiver disponível e a propriedade estiver autorizada. Desativar pausa novas consultas e preserva o histórico. |
| `f3base_seo_entidade.endereco` | Preencha logradouro, cidade, estado, CEP e país nas linhas do editor. O endereço é opcional; quando informado sem país, usa Brasil. |
| `f3base_pipedrive.mapa_campos` | Escolha o campo do Pipedrive que receberá cada informação do contato. Selecione Somente na nota para conservar a informação sem preencher um campo comercial. |
| `f3base_pipedrive.mapa_canais` | Associe cada origem de anúncio a uma alternativa do campo Canal. Origem não identificada significa falta de evidência, não visita orgânica comprovada. |
| `f3base_pipedrive.mapa_parceiros` | Associe cada código de parceiro à alternativa da conta. Use as opções de ausência de campanha, fora do padrão e origem não observada quando correspondam ao contato. |
| `f3base_pipedrive.mapa_pontos` | Escolha as alternativas para formulário do site, formulário com WhatsApp e formulário nativo de anúncios. Um clique sem envio não cria uma pessoa no CRM. |
| `f3base_pipedrive.mapa_servicos` | Associe as respostas do formulário às alternativas de Serviço. Respostas conhecidas podem selecionar vários serviços; respostas sem correspondência permanecem na nota. |
| `f3base_pipedrive.mapa_servicos_formularios` | Escolha o serviço associado a cada formulário nativo. Esta regra é usada quando a resposta do contato não determina o serviço. A regra do formulário tem prioridade sobre a da campanha. |
| `f3base_pipedrive.mapa_servicos_campanhas` | Escolha o serviço de cada campanha. Esta regra é usada quando não há serviço definido pela resposta ou pelo formulário. Nenhuma associação deixa o campo sem serviço inferido. |
| `f3base_pipedrive.mapa_respostas` | Selecione formulário, pergunta e campo de destino. Para perguntas com alternativas, relacione cada resposta à alternativa correspondente da conta. Respostas sem mapa permanecem na nota. |
| `f3base_pipedrive.campos_fixos` | Escolha os campos que sempre receberão um valor definido nesta integração. Confira o tipo e as alternativas da conta antes de salvar. |
| `f3base_pipedrive.parceiros_plataforma` | Defina o parceiro a usar para cada plataforma de anúncio quando não houver uma regra mais específica para a campanha. |
| `f3base_pipedrive.mapa_pessoa` | Escolha os campos da pessoa que receberão o perfil LinkedIn e o link de WhatsApp informados pelo contato. O plugin não procura perfis na rede social. |
| `f3base_pipedrive.atividade_canais` | Escolha o tipo e o assunto da primeira atividade para WhatsApp, e-mail e tarefa. Os tipos precisam existir no Pipedrive. Informar telefone não comprova que ele possui WhatsApp. |
| `f3base_pipedrive.atividade_janela` | Defina fuso, dias de atendimento, abertura, fechamento, prazo e horário de retomada. Contatos fora da janela são programados para o próximo horário útil. Feriados não são calculados e atividades existentes não mudam. |
| `f3base_pipedrive.site_alternativa` | Escolha a alternativa que representa este site quando o campo Site for uma seleção. Campos de texto recebem o endereço principal do site automaticamente. |
| `f3base_anuncios_meta.formularios` | Atualize a lista e selecione os formulários administrados por este site. Salve para aplicar. Nenhuma seleção não autoriza a importação de todos os formulários. |
| `f3base_anuncios_meta.mapeamento` | Relacione os campos recebidos aos dados de contato e associe nomes às campanhas. Adicione ou remova linhas no editor; salvar aplica as regras aos próximos contatos. |
| `f3base_anuncios_google.formularios` | Atualize a lista e selecione os formulários administrados por este site. Salve para aplicar. Nenhuma seleção não autoriza a importação de todos os formulários. |
| `f3base_anuncios_google.mapeamento` | Relacione os campos recebidos aos dados de contato e associe nomes às campanhas. Adicione ou remova linhas no editor; salvar aplica as regras aos próximos contatos. |
| `f3base_anuncios_meta.paginas` | Atualize a lista e selecione as páginas autorizadas. Salve a seleção antes de consultar os formulários dessas páginas. |
| `f3base_anuncios_google.campanhas` | Selecione as campanhas autorizadas para contatos conversacionais sem formulário identificado. Sem seleção, esses contatos são recusados. Formulários tradicionais continuam exigindo autorização própria. |
| `f3base_anuncios_linkedin` | Escolha o cliente e a conta para importar contatos do LinkedIn. Com Plugin LinkedIn, as listas usam a conexão desse plugin; a importação ainda exige os formulários e as permissões concedidos ao Site Core. |
| `f3base_pipedrive.unidade` | Selecione a unidade que receberá os novos contatos. A alternativa precisa existir no campo Unidade da conta conectada. |
| `f3base_pipedrive.linkedin_modo` | Escolha onde guardar o perfil profissional informado pelo contato. Apenas na nota conserva o endereço no resumo; Escolher campo usa o campo de pessoa selecionado; Detectar campo exige uma única opção compatível no catálogo. O plugin não procura perfis na rede social. |
| `f3base_consentimento.politica_versao` | Identifique a versão da política publicada. Mudanças nas regras podem exigir nova escolha do visitante; não concedem autorização retroativa. |
| `f3base_llms.entrega` | Arquivo gerado publica o índice para entrega direta pela hospedagem. Dinâmica produz cada resposta pelo WordPress. Escolha Arquivo gerado quando a raiz for gravável e a atualização automática estiver funcionando. |

Outras alterações de texto:

- Datas Meta e Search Console sem formato nos rótulos.
- Datas de qualidade no fuso do WordPress.
- Títulos de mapeamentos por assunto.
- Serviços e ofertas, mapeamento da pessoa e das respostas sem referência a JSON.
- Orientação para ativar JavaScript preservando valores.
- Simulação de recuperação com motivos por destino.
- Comparação anterior parcial e definições de sessões.
- Limites e exclusões da leitura de desempenho.
- Pipedrive: alternativa do site sem ID no rótulo.
- Pipedrive: orientação de ativação pelo nome do controle.
- Consentimento: ajuda da faixa não descreve modal bloqueante.
- Privacidade: captura de valores e retenção de tentativas, com limites e exclusão.

## 5. Instalação e prova de prontidão

**Laboratório:** 551 verificações reportadas pelas suítes desta release, contando as 52 verificações Google uma única vez dentro da suíte de recuperação. São verificações, não 551 cenários independentes. Distribuição: base/contratos 155; funcionalidades 33; tentativas 33; LinkedIn 8; recuperação/Google 90; renderização 86; textos 12; editor de formulários 1; documentação 68; configuração em navegador 25; formulários em navegador 5; vitais em navegador 11; tentativas em navegador 24. Sintaxe dos 223 arquivos PHP conferida. Provedores externos foram simulados; sem envio real de teste a anúncios, CRM ou e-mail.

O mesmo ZIP final passou por instalação limpa e atualização direta, migração, confirmação em requisição seguinte e repetição idempotente. No ambiente descartável, somente o relógio da espera de finalização foi acelerado. Conferidos preservação de contato, escolhas, valores vazios, segredos sintéticos, procedência, callback/cursor LinkedIn e estado incerto de e-mail; tabelas de filas preservaram os hashes observados. A migração de vital antigo conservou o valor e o marcou `legado_desconhecido`, sem atribuição inventada. Evidências e scripts de reprodução constam no fonte.

**Site-Teste:** `https://fator3-teste-mcp-1.dreamhosters.com`, Core ativo **1.43.0 → 1.44.0**. Backup privado de banco anterior: artefato `710d849a21a2e8cee0f6434c21de8e5a`, 20.523.035 bytes, SHA-256 `15fde03710a184651e3ab9f13c9e071edf2fb531ade7900fb05db85f94ef577e`; não foi baixado nem incluído na entrega. Preimagem dos arquivos: `8e90b646a8850b25eb092ff2`. Operação de pacote: `ef547630041c38759a0989d3d9f20304`, estado `complete`.

O canal de atualização confirmou o SHA-256 do instalador da seção 9, reativação silenciosa em PHP novo e home/REST HTTP 200 antes/depois. A confirmação funcional posterior foi independente: `f3base/saude-ler {}` devolveu versão 1.44.0, atualização `concluida`, zero falhas, conclusão às **12:06:16 −03** e finalização pelo executor às **12:08:48 −03**, em 21/10/2026. Recuperação não pausada, módulos inicializados e `core_operacional`. Isso comprova o ciclo do Core; não homologa fornecedores externos.

Leituras executadas após a troca:

| Ability e entrada | Resultado observado |
| --- | --- |
| `f3base/formularios-tentativas-ler`, `{"dias":1,"limite":1}` | Sucesso, tabela disponível, retenção 30 dias, acervo vazio. |
| `f3base/comportamento-ler`, `{"dias":1,"formulario":"contato-whatsapp","limite":1}` | Bloco `recusas_por_campo`, zero tentativas, contagem exata, sem valores. |
| `f3base/vitais-ler`, `{"dias":1,"metrica":"INP","automacao":"audiencia"}` | Sucesso, fuso America/Sao_Paulo e acervo vazio. |
| `f3base/documentacao-ler`, arquivo `docs/FORMULARIOS-TENTATIVAS-1.44.md`, linhas 1–34 em duas páginas | Conteúdo completo 1.44.0; SHA-256 `198b4fd0220c2b5725b3478ee0eb0ee0ad5fd1f7aa523d6445b81a3bad29a1c0`. |
| `system/probe`, GET `/`, contexto de teste, asserções de HTTP 200, presença do estilo inline e ausência da URL CSS isolada | Todas passaram; corpo completo, bypass confirmado por PHP novo. Sonda interna na mesma origem. |
| `plugins/list`, prefixos Core e wp-mcp | Os cinco pacotes da seção 3 ativos, Core 1.44.0. |

No Site-Teste não foi criado contato sintético que pudesse disparar integrações já configuradas. A fotografia de recusa, o valor e a exclusão por sessão foram exercitados no WordPress local e no navegador, não numa sessão real de ctooffice. A evidência sanitizada de hospedagem está em `evidence/site-teste-1440.json`.

Para implantação: conferir hash do ZIP; manter backup anterior de arquivos e banco; atualizar pelo fluxo de pacote já usado; consultar `f3base/saude-ler` até conclusão/finalização sem falhas; conferir a documentação e leituras acima. Executar os aceites da seção 7 somente no contexto de teste apropriado e com acompanhamento das integrações do site.

## 6. Banco e volta de versão

Migração aditiva: quatro colunas em `f3base_vitais` para automação, motivos, regra e atribuição; tabela `f3base_formulario_tentativas` com eventos, vínculo, metadados de campo, cifra e índice opaco de titular. Nova configuração `f3base_formulario_tentativas`, acrescida sem sobrescrever opções existentes. Inventário: 57 tabelas do Core, 133 options/estados, 71 definições públicas de configuração e 10 famílias de transients. Não há novo agendamento: retenção reaproveita jobs existentes. A tabela participa da verificação de prontidão em instalação nova e upgrade.

A retomada usa as etapas registradas da atualização; não recria dados apagados nem reenvia entregas incertas. Recuperação administrativa de conversões conserva o identificador de pedido igual ao registro e uma entrega por destino, com transação e comparação do estado. Entregue, incerto, cancelado e esgotado não são reenviados; recibo incerto Google é reconciliado no vínculo original.

Restaurar só arquivos não desfaz migração, consentimento nem efeitos externos. Para retorno, usar backup anterior e o fluxo de recuperação do Core, preservando/reconciliando pendências antes de reabrir executores. Voltar à 1.43.0 interrompe o diagnóstico novo **e sua limpeza**; os dados privados exigem eliminação/arquivamento autorizado ou manutenção explícita da retenção antes do retorno. Desinstalar remove a tabela de tentativas. Trocar o salt WordPress impede ler cifras anteriores; backups que contêm dados e chave têm ciclo e acesso próprios, não são apagados pela remoção de uma linha no banco ativo.

## 7. Pendências de validação

| Pedido/área | Aceite ainda necessário | Responsável/contexto |
| --- | --- | --- |
| 246/248 | Conferência visual das telas publicadas nos sites e seus temas. Testes locais cobriram controles, títulos e textos; não houve navegação autenticada em todas as telas hospedadas. | Frota/dono após implantação. |
| 249 | Selecionar formulário e campanha não vazios de uma conexão LinkedIn real, com canais leads/ads autorizados. | Operador da conta externa. |
| 256 | Próximo contato de teste em ctooffice ou korvena.com.br com nota inicial na hora local e deslocamento. | Operador Pipedrive/frota. |
| 258 | Repetir comparação de fator3.com.br e comprovar `anterior_parcial`; auditar registros de conselar que produziram 9 sessões e 3 iniciadas. A explicação semântica não substitui essa apuração. | Frota com acesso aos dois sites. |
| 259 | Após Google Ads `ready`, simular e executar recuperação dos registros 113/125 em ctooffice, reconciliar e confirmar uma conversão por registro na ação indicada; segunda recuperação sem reenvio. Não executado nesta rodada. Prazos informados: 16/01/2027 e 18/01/2027. | Operador autorizado de ctooffice/Google Ads, conforme pedido existente. |
| 260 | Após sete dias da troca em ctooffice, ler INP móvel de `/`, alvos e fase dominante. Atribuição de script depende do suporte do navegador. | Frota/analista. |
| 261 | Medir o p75 com classificação na própria amostra e contagens excluídas. Não prometer igualdade retroativa aos 77 registros tidos como humanos pelo cruzamento anterior, nem reconstruir os 54 sem vínculo. | Frota/analista após novos dados. |
| 262 | PageSpeed da home de ctooffice e korvena.net.br sem requisição da folha, e aparência preservada em cada tema. Nenhum ganho em milissegundos foi medido nesta rodada. | Frota após implantação. |
| 263 | Em ctooffice, testar vazio e os dois telefones, corrigir e enviar, ler campo/regra/valor/sessão, eliminar o registro de teste e comprovar remoção de toda a sessão, preservando outra. As recusas de 18–20/10 não podem ganhar valores retroativamente. | Frota após troca, em contexto de teste e controlando efeitos comerciais. |
| Runtime/fornecedores | WordPress mínimo exato 7.1.2, APIs reais de LinkedIn/Pipedrive/anúncios e ganho de desempenho externo não homologados nesta rodada. | Próxima homologação pertinente; não são falhas demonstradas. |

Não há bloqueio técnico observado no escopo testado. A classificação `com-pendencias` explicita os aceites externos acima e não declara os pedidos integralmente homologados em produção.

## 8. Credenciais e configuração do dono

**Nenhuma credencial nova é exigida para atualizar ou para o pedido 263.** O dono pode ajustar captura e retenção em Privacidade e segurança → Retenção. A capability `f3base_ler_leads` deve estar restrita a quem pode ler os dados privados; a nova leitura verifica essa capacidade explicitamente.

Na origem LinkedIn, conservar o cliente **Plugin LinkedIn**, a conexão e a conta atuais. A descoberta usa autorização de leads para formulários e ads para campanhas no plugin externo. Não copiar token nem client secret para viabilizar a lista; eventual concessão ausente deve ser resolvida na conexão responsável.

Para conferir a nota Pipedrive, usar a conta existente em Conexões e entregas → Pipedrive e o campo **Token de API do Pipedrive** (`f3base_pipedrive_token`), sem substituir credenciais como efeito da atualização. Confirmar o fuso em Configurações → Geral do WordPress. Para a recuperação Google, usar o `destination_ref` vigente, pronto e autorizado devolvido pelo contrato de conversões; não usar o canal legado nem considerar a mera presença de uma chave como prova de prontidão. Nenhum segredo aparece neste relatório ou nos pacotes.

## 9. Identidade dos arquivos

| Arquivo | Bytes | SHA-256 |
| --- | ---: | --- |
| base-site-core-fator3-1.44.0-instalador.zip | 2129471 | `91c4695ad4585965276c6b8cabc9ab8a91bbffc4423968f00d2330f6edf1407e` |
| base-site-core-fator3-1.44.0-fonte.zip | 3134934 | `283452e8bb12a2e073779191d1386232fdf79bbd77f2e1ae4c642616f4beb52d` |

- [base-site-core-fator3-1.44.0-instalador.zip](sandbox:/workspace/scratch/351cd9518840/release144/base-site-core-fator3-1.44.0-fonte/release/base-site-core-fator3-1.44.0-instalador.zip)
- [base-site-core-fator3-1.44.0-fonte.zip](sandbox:/workspace/scratch/351cd9518840/release144/base-site-core-fator3-1.44.0-fonte/release/base-site-core-fator3-1.44.0-fonte.zip)
- [base-site-core-fator3-1.44.0-relatorio.md](sandbox:/workspace/scratch/351cd9518840/release144/base-site-core-fator3-1.44.0-fonte/release/base-site-core-fator3-1.44.0-relatorio.md)

O instalador contém somente o plugin. O fonte contém runtime idêntico ao instalador, scripts, testes, evidências sanitizadas e documentação, sem ZIP aninhado, banco ou credenciais reais. Inclui dependências de teste Google/LinkedIn necessárias à reprodução, sem instalá-las junto ao Core.

O fonte conserva uma **cópia anterior ao fechamento do fonte** deste relatório, com o tamanho/hash do próprio fonte remetidos ao relatório externo canônico `base-site-core-fator3-1.44.0-relatorio.md`. O hash final foi preenchido somente aqui depois do empacotamento; o ZIP fonte não foi reaberto para inserir o próprio hash.
