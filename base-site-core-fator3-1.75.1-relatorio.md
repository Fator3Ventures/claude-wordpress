# Entrega — Fator3 Site Core 1.75.1

Revisão 1 · 09/11/2026 · Implementação e homologação dos pedidos Core 375–382  
Slug `base-site-core-fator3` · Versão final 1.75.1 · Contrato administrativo 8.36.0  
**Status com-pendencias de aceite externo.** A versão está instalada, ativa e confirmada no executor do Site-Teste. A seção 6 identifica as provas que dependem da frota, do fornecedor ou de instrumentação de navegador.

## 1. De onde esta versão entra

Para a frota, os caminhos exercitados são instalação em WordPress limpo e atualização direta **1.74.0 → 1.75.1**. O Site-Teste passou por **1.74.0 → 1.75.0 → 1.75.1**. O candidato 1.75.0 implementou os oito pedidos. Um teste adicional mostrou que o fechamento antigo do evento comportamental não declarava a ausência dos campos técnicos. O incremento de patch corrige essa projeção na mesma rodada.

O fonte original da 1.74.0 tem SHA-256 `c3e1cbb05c982b746b663005c0368bf51ac04700df16bd591a564e64eed35e36`. O instalador-base de 4.336.155 bytes tem SHA-256 `a77d89d369e3c106383e83aae43bb0211ff1b7952f60ed1e97a0b2595066d1ae`. O fonte entregue contém a árvore da base usada na migração.

Requisitos mínimos do projeto e dos cabeçalhos do plugin: WordPress 7.1.4, PHP 8.3 de 64 bits e instalação única. No laboratório foram usados WordPress 7.1.4, PHP 8.3.6 e MySQL 8.0.46. No Site-Teste, a leitura de saúde após a instalação informou WordPress 7.1.4 e PHP 8.3.36. As referências `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md` são as revisões 5 de 02/11/2026. A aba vigente consultada é a de 09/11, com os pedidos 375 a 382.

## 2. Convivência e encaminhamentos

| Pacote | Versão no teste | Verificação e fronteira |
|---|---:|---|
| Fator3 MCP | 0.41.0 | Transferência com SHA-256, instalação com guarda de slug, descoberta, execução, revisão de configuração e leitura após a troca |
| Google MCP | 0.31.0 | Ativo e reconhecido na saúde após a troca. Os dados analíticos próprios e o parâmetro do evento GA4 continuam no Core |
| Meta MCP | 0.21.0 | Ativo e reconhecido. O navegador e a fila CAPI alterados nesta rodada pertencem ao Core |
| LinkedIn MCP | 0.19.0 | Ativo e reconhecido. O teste do caminho de lead avalia a conversão em prévia |
| Pipedrive MCP | 0.8.0 | Ativo, com etapa de pós-atualização verificada. O recibo comprova a política que restringe o teste comercial aos domínios autorizados |

A troca no Site-Teste exigiu apenas o Core. A prontidão dos cinco acompanhantes foi conferida no mesmo WordPress. O teste comercial nos fornecedores tem os limites da seção 6.

| Destinatário | Versão examinada | Classificação e situação | Pedido | Documento |
|---|---:|---|---:|---|
| implantador-base | 2.18.0 | Ação necessária. Proposta aplicada em cópia isolada, integração testada e incorporação oficial aberta | 379 | [Impacto no implantador-base](base-site-core-fator3-1.75.1-impacto-implantador-base.md) |

O planejamento definiu o atributo e o comportamento em temas sem marca. O patch em `impactos/implantador-2.18.0-pedido-379.patch` usa o bloco de título real da home do destinatário. Após renderização nativa, a auditoria identificou três textos sem marca na amostra original e dois na alterada. O título recebeu o alvo estável `introducao`. O Core já aceita a marca do tema.

## 3. Mudanças e evidência

| Pedido | Mudança | Resultado observado |
|---|---|---|
| 375 · E-mail acima de 2 MiB | Lê cabeçalho, estrutura MIME e trecho de texto. Registra o contato suspeito com remetente declarado, assunto, tamanho, metadados de anexos e sinal da regra de descarte. Grava antes de mover. A lista de exceções explícitas começa vazia | Na caixa real do Site-Teste, três mensagens sintéticas de 2.326.819, 2.601.143 e 2.326.854 bytes viraram suspeitas. O cabeçalho longo e a resposta automática apareceram como sinais. Os três IDs foram relidos pela API de contatos e as mensagens localizadas na pasta de importados. O par IMAP instrumentado registrou 13 comandos para três UIDs e zero leituras de partes de anexo |
| 376 · Pixels Meta em paralelo | Inicializa os IDs adicionais sob os mesmos controles de consentimento, supressão e correspondência do principal. Um evento de navegador compartilha o identificador entre destinos. CAPI conserva um destino | O emissor JavaScript com `fbq` instrumentado registrou PageView e Lead nos dois IDs com o mesmo identificador por ocorrência. A correspondência foi passada a ambos, o Lead de teste foi suprimido e o teste PHP confirmou um único destino do servidor |
| 377 · Último campo por sessão | A linha de fechamento analítico expõe identificador técnico, etapa e contagem. A visão de formulários aceita o filtro de sessão. O patch 1.75.1 explicita `nao_observado` nos fechamentos legados e preserva o zero observado | A consulta do WordPress instalado devolveu `seu-nome`, etapa 1 e 1 campo para a observação sintética. Dois fechamentos comportamentais, um sem navegação pareada, devolveram ausência de prova. A visão integrada filtrou a sessão. A prova local verificou que o valor do nome fica fora do relatório |
| 378 · Fotografia do abandono | Opção separada da captura de tentativas recusadas, desligada por padrão. Blur de campo alterado e saída atualizam a mesma linha cifrada, por instância e sequência. O aceite elimina a fotografia. Retenção, cotas e capacidade de leitura são aplicadas | No Site-Teste a guarda recusou a captura no padrão. Na requisição de teste isolada, o nome foi preservado, o e-mail apagado ficou vazio na única linha e a eliminação da sessão impediu o reenvio. No laboratório foram testados escrita atrasada, eraser após apagar o e-mail, cifragem, consentimento e exclusão de campos sensíveis |
| 379 · Elemento tocado | Clique inerte e fricção carregam seção e alvo declarado ou posicional. Tetos padrão de 30 e 15 por carregamento. O clique inerte repete o mesmo alvo após a janela de 1,2 s. A auditoria aponta os textos sem marca e o relatório agrega os alvos | O listener reconheceu dez alvos distintos no DOM. A API do Site-Teste apresentou dez alvos em uma sessão semeada, incluindo `equipe` e `socios:titulo:10`. A prova no tema-modelo usou o fonte real do implantador 2.18.0 |
| 380 · Cadência do relatório | A gravação da configuração agenda, troca ou remove o evento e devolve o resultado. O zelador reconcilia o agendamento ausente e o resumo sinaliza divergência | No Site-Teste, a gravação de nenhuma deixou zero eventos e mensal recriou `f3base_cadencia_relatorio`. Mecanismo e hook foram relidos. O horário original ficou restaurado em **30/11/2026 às 06h de Brasília**. O laboratório também cobriu frequência semanal e evento ausente |
| 381 · Telefone do formulário WhatsApp | O schema aceita valor escalar sem a ambiguidade do `oneOf`. Entrada inválida identifica o campo e o motivo. O valor informado é preservado na prévia | No Site-Teste o telefone sintético passou pela simulação e aplicação em `contato-whatsapp`. As 11 etapas chegaram ao recibo terminal `com_pendencias`. A captura foi confirmada e a limpeza local eliminou o contato. Slack e envio externo seguiram as políticas de homologação |
| 382 · Reserva órfã no reaquecimento | Expiração e liberação conferem a revisão e o dono. A leitura expõe as reservas do módulo e do executor, a trava de banco e as intenções. A espera por orçamento volta a ser elegível e há aviso de atraso superior a duas horas | Na 1.75.1 instalada foi criada uma reserva sintética vencida. A inspeção mostrou dono e prazo. A execução após simulação, revisão e motivo retornou `reserva_orfa_liberada`. O laboratório preservou uma reserva vigente, recuperou uma inválida e verificou a elegibilidade da próxima passagem |

## 4. Instalação e prova da troca

No Site-Teste o ZIP foi transferido ao servidor, selado pelo SHA-256 e instalado com `plugins/upload-base64`, origem `zip_path`, `expected_slug=base-site-core-fator3`, `expected_sha256` da seção 8, ativação e sobrescrita habilitadas. Operação final `d690cc84738f82dffcd0a27a18c8f0bd`, pré-imagem `5664c4296243118a0b4c508c`. A operação anterior, para a 1.75.0, foi `6bbbbbc598c3dc658bc2ce6dc2a1a376`.

| Ambiente | Cenário | Resultado |
|---|---|---|
| WordPress limpo e atualização direta | Instalação, 50 asserções dos pedidos em cada caminho, reativação e comparação de 993 registros e configuração no upgrade | Ciclos concluídos. Na reativação, 33 estruturas restauradas e zero leituras prematuras |
| JavaScript e compilação | 11 verificações DOM. Reprodução de 84 saídas JS minificadas e da estrutura PHP gerada | 85 arquivos idênticos byte a byte. A biblioteca web-vitals vendorizada é inventariada separadamente |
| Validação estática | Sintaxe PHP, JavaScript de primeiro nível em assets e leitura dos JSON do runtime | 597 PHP, 29 JS e 57 JSON verificados |
| Site-Teste | `plugins/list`, `f3base/resumo-operacional-ler`, `system/health`, `system/probe` com tráfego de teste e cache contornado | Versão ativa 1.75.1. Ciclo concluído e confirmado no executor. Saúde positiva. Home e login HTTP 200, com campo de usuário reconhecido no login |
| Paridade e documentação | Cabeçalho, arquivos de e-mail, formulário, relatórios, cache, assets e guias | Doze hashes do site idênticos ao ZIP. Índice lido em `f3base/documentacao-ler`. As 32 linhas de `docs/RELEASE-1.75.1.md` e as três de `docs/AGENTES-1.75.1.md` foram lidas integralmente e os hashes conferidos |

O índice para o operador é `docs/DOCUMENTACAO.md`. O contrato 8.36.0 pode ser lido por MCP e nos schemas embarcados em `docs/dados/`. O SHA-256 do guia de release instalado é `9a22b5de96d3af4b2f38006b420cfbdfab70a98b7eecc57129517731e11c8377`.

O pacote de transferência e as duas bancadas temporárias saíram do servidor. A configuração de testes recuperou a revisão original e a captura global de abandono ficou desativada. Permanecem os **três contatos suspeitos sintéticos**, as respectivas mensagens na pasta de importados e os recibos de homologação. O perfil consultado com regime WhatsApp e hipótese de retenção de 60 meses indicou 90 itens conformes, P53 indeterminado por contexto de acessos e P78 divergente na política de testes. O P78 já constava da entrega anterior. O detalhe verificável está em `evidence/1750/site-teste.json`.

A publicação raw cabe à frota. Após a publicação no repositório público, o caminho previsto para `plugins/upload` é `https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/base-site-core-fator3-1.75.1-instalador.zip`, com o hash e slug desta entrega. A homologação acima utilizou o ZIP do dono transferido diretamente.

## 5. Banco, migração e correção por nova versão

A fotografia reaproveita a tabela de tentativas e a chave de cifragem derivada dos salts do site. O registro é substituído segundo a sequência e a identificação da instância. A nova versão preserva as tentativas anteriores. A eliminação utiliza as rotinas de privacidade e as guardas de reenvio. O dado histórico de comportamento sem campo observado continua identificável como tal. Os novos padrões de opções são aplicáveis mesmo quando o site só possui a estrutura antiga.

Na caixa, o fluxo recupera o que estiver disponível nos registros históricos de cabeçalho excedido. Para uma mensagem anteriormente descartada, a recuperação integral dos metadados exige que o UID ainda seja localizável na mesma caixa. Uma interrupção entre persistência e movimentação requer reconciliar registro, UID e pasta antes de repetir. No cache, a intervenção sobre uma reserva vencida deixa motivo e ator no diário. Na agenda, conferir a recorrência e o próximo horário no retorno da escrita.

Preservar o banco, o registro de configuração e os salts do WordPress no backup operacional. Os dados e efeitos externos são conciliados pelos seus recibos. A correção foi exercitada em avanço por nova versão, incluindo a troca 1.75.0 → 1.75.1 no Site-Teste.

## 6. O que permanece pendente

- **Growth Campanhas e dono, pedido 376.** A entrega em dois datasets reais depende dos dois IDs de teste e de acesso ao Gerenciador de Eventos. A prova atual cobre as chamadas produzidas pelo cliente. Em CTO Office, a futura conferência inclui mesmo event_id, volume do pixel principal por sete dias e diagnóstico de tags externas.
- **Growth e frota, pedidos 377–379.** Em navegador real e modo de teste foram tocados dez títulos na home, preenchido apenas o nome sintético e abandonada a página. A consulta de audiência do Site-Teste devolveu zero sessões de teste naquele período, inclusive com automações. O percurso visual ficou sem correlação individual no servidor. A leitura dos campos e dos dez alvos foi provada separadamente com registros sintéticos nas abilities instaladas. Faltam o abandono real da Korvena, a comparação com Clarity e uma amostra comparável de INP. O perfil de medição e a elegibilidade dessa sessão merecem conferência pela frota antes de atribuir a ausência a uma causa.
- **Frota, pedidos 375 e 382.** A caixa própria do Site-Teste estava acessível por IMAP, com o serviço geral desligado. A prova usou os componentes reais de leitura, classificação, persistência e movimentação em homologação restrita à chamada. O alvo de resposta automática foi previamente semeado como descartado e reprocessado pelo caminho de persistência. O cron recorrente da caixa ligada e a prévia/aplicação da rota administrativa de reprocessamento não foram exercitados ponta a ponta nessa caixa. Para o cache da Korvena, conferir a última execução do dia e a entrega de `/mvp/` pela cópia aquecida depois da implantação.
- **Implantador e frota, pedido 379.** Incorporar e publicar a marcação do tema-modelo. O patch validado no destinatário acompanha o fonte e o relatório de impacto. A decisão de distribuição para a frota e a atualização dos sites de produção continuam com o dono.

## 7. Credenciais e configuração do dono

A nova versão usa as credenciais já configuradas no site. Para revisar e-mails, mantenha a caixa IMAP/SMTP, a identidade e as pastas de acordo com o ambiente. Controle exceções de descarte por `f3base_email_site.descartes_acima_limite`. Para Meta, configure os pixels de navegador em Site Core → Configurações → Meta e os datasets de monitoramento somente após a definição do dono.

A opção `f3base_formulario_tentativas.capturar_abandono` vem desativada. A decisão de ativá-la e definir se exige consentimento de medição cabe ao dono. `abandono_exige_medicao` inicia habilitada. A leitura dos valores depende de `f3base_ler_leads`. Segredos de fornecedor, salts, IPs de visitantes, tokens do WordPress e valores de contatos reais ficam fora dos artefatos.

## 8. Identidade dos arquivos

| Artefato | Arquivo | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [base-site-core-fator3-1.75.1-instalador.zip](base-site-core-fator3-1.75.1-instalador.zip) | 4.372.056 | `9fff30dc9b75a60fc193373c4366659bf6db13c35025f677b5f46e8988181dc6` |
| Fonte | [base-site-core-fator3-1.75.1-fonte.zip](base-site-core-fator3-1.75.1-fonte.zip) | 9.315.610 | `ebc04d4f325d2f76dc9680935b32d268cff149dba4ff6788ed887eca73ba6f6a` |
| Impacto | [base-site-core-fator3-1.75.1-impacto-implantador-base.md](base-site-core-fator3-1.75.1-impacto-implantador-base.md) | 3.556 | `dd8e64e7c9f3c815d750e919b34861fc4094f41b5cd52a269904051877a2c5c8` |

A cópia dentro do fonte antecede o fechamento. A identidade final do ZIP de fonte aparece no relatório externo canônico. Checklist da seção 14 do padrão conferido, com os aceites pendentes discriminados na seção 6.
