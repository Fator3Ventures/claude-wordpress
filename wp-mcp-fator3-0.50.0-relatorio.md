# Entrega — Fator3 MCP 0.50.0

18/11/2026 · Revisão 1 · Implementação e homologação no Site-Teste · Entrega com pendências de integração e de frota.

O pacote corrige o publicador do canal nos pedidos MCP 85 e 86. A manutenção diferencia progresso, estagnação e falha. O registro do canal exige confirmação em duas requisições HTTP independentes. O Core 1.94.0 também publica pelo seu próprio observador. O encaminhamento ao responsável pelo Core contém a alteração testada para ambos usarem a mesma decisão.

## 1. Base de migração

Instalação limpa ou atualização direta da 0.49.0. Instalador da base com 964290 bytes e SHA-256 c1981c997840231a47492333ebb48125b2e8b8dd8619ec660bc8ad205883b134. Slug wp-mcp-fator3, basename wp-mcp-fator3/wp-mcp-fator3.php. Mínimos de projeto WordPress 7.1.4 e PHP 8.3. As provas locais usaram WordPress 7.1.4 e MariaDB 11.8.6. O ensaio de volume e a migração do ZIP final usaram PHP 8.3.6. A retomada da operação interrompida e a bancada HTTP também foram exercitadas com PHP 8.4.27. O Site-Teste usava WordPress 7.1.5 e PHP 8.3.36.

Foram lidas integralmente as revisões 5 de 02/11/2026 de instrucoes-agentes-plugins-fator3.md e padrao-desenvolvimento-plugins-fator3.md, a regra comum, a aba do MCP e Fator3 MCP(20261118-224545).md. A base e o prazo de aceite são os indicados nos pedidos.

## 2. Convivência e encaminhamentos

| Pacote | Bancada integrada e Site-Teste |
|---|---|
| Site Core | 1.94.0 |
| Google | 0.37.0 |
| Meta | 0.29.0 |
| LinkedIn | 0.26.0 |
| Pipedrive | 0.12.0 |

Os hashes dos instaladores usados na bancada estão em evidencias/0500/bases.json. O MCP também passou na instalação limpa sem acompanhantes. A mudança conserva o catálogo de 172 habilidades próprias e acrescenta o parâmetro opcional stall_passes à política de manutenção.

O MCP fornece ChannelIncidents::observeRegistration(). O Core 1.94.0 possui um caminho próprio que publica para o mesmo recurso. A proposta delega esse ponto ao MCP e conserva a leitura passiva para compor o histórico. Na reprodução com o Core oficial, uma única falha web abriu o incidente pelo observador_core. Na cópia com a delegação, a abertura ocorreu na segunda observação HTTP, com origem publicador_canal. Distribuir o MCP e incorporar a delegação na próxima versão oficial do Core para o aceite de ponta a ponta. Os conectores e o Implantador não precisam de adaptação para esses dois pedidos. [Impacto individual no Core](https://chatgpt.com/library?file_id=libfile_fde3_f-68d050f76b688191ba8f03e2f4dfdcc8_32706b9c47908191baafe72f89b6caee&account_id=personal)

## 3. Mudanças por pedido

| Pedido | Comportamento da versão | Prova própria |
|---|---|---|
| MCP 85 — manutenção parcial | Conta execuções do lote. Consulta de saúde não incrementa a contagem. Inventário em avanço, páginas restantes e esgotamento do orçamento podem produzir continuidade normal. Uma falha efetiva abre incidente na passagem. A mesma seleção protegida sem avanço abre após o limite configurado. | Com o limite mínimo de 1, 2.000 backups nativos vencidos foram eliminados em 55 passagens, sem abertura do incidente da manutenção. Com o limite em 2, um backup protegido permaneceu intacto e abriu na segunda passagem. Quatro consultas intermediárias preservaram o contador. Após liberação, a limpeza terminou e recuperou o incidente. |
| MCP 85 — política e retomada | O novo campo Passagens sem avanço aceita de 1 a 96, padrão 3. A gravação exige a revisão corrente. Alterar somente o limiar preserva a seleção já congelada. | O navegador verificou rótulo, ajuda e largura em 360, 768 e 1440 px. Simulação preservou 3, gravação persistiu 4 e o laboratório repôs 3. A falha de E/S simulada abriu imediatamente com limiar 4. |
| MCP 86 — registro no cron | O publicador ignora CLI e inicialização incompleta. Duas observações conclusivas de falha em requisições HTTP distintas abrem o incidente. Uma leitura saudável zera a contagem e recupera um episódio aberto. | O ensaio com o observador chamado durante a inicialização do adaptador reproduziu a abertura em WP-CLI na 0.49.0. Na 0.50.0, wp cron event run --due-now executou a manutenção sem publicar registro-wordpress, tanto com servidor sadio quanto deliberadamente desabilitado na bancada. |
| MCP 86 — web e cron HTTP | A primeira falha fica como suspeita. Chamadas duplicadas dentro de uma requisição produzem uma única amostra. | Seis requisições HTTP reais contra WordPress local cobriram falha isolada, saúde intermediária, segunda falha em contexto de cron HTTP, repetição e recuperação web. No ensaio HTTP o marcador DOING_CRON foi definido para exercitar esse contexto. O teste de WP-CLI executou o comando real. |

A política ordinária observa o registro sadio em intervalos de cinco minutos. Depois da primeira falha, a próxima requisição elegível pode confirmar a suspeita. Para manutenção, consultar last_run.status, continuation_required, stalled e stall_counts em system/maintenance-policy. Para disponibilidade, consultar o histórico de registro no Core. Os resultados detalhados estão em evidencias/0500 e a reprodução em tools/release0500.

## 4. Instalação e prontidão

O Site-Teste foi atualizado de 0.49.0 para 0.50.0 com o ZIP da seção 8. O canal conferiu o tamanho e o SHA-256 do arquivo temporário em wp-content/upgrade. A operação plugins/upload-base64 usou zip_path, expected_sha256, expected_slug=wp-mcp-fator3, activate=true, overwrite=true e prazo de 30 segundos por sonda.

Operação a8210785cdc3171c57fa9e57df1990db. Plugin ativo, applied=true, recovery_status=applied. As duas sondas passaram e o arquivo temporário estava ausente na conferência posterior. Às 19h58 e às 20h00 de São Paulo, system/health confirmou a versão, as duas rotas registradas, as ferramentas prontas, o marcador de cron ativo e zero recuperações em aberto. A política tinha próxima execução agendada. A simulação remota com limiar 4 conservou a revisão e o valor salvo 3.

| Verificação | Resultado |
|---|---|
| Instalação limpa, migração e operação interrompida | 7, 10 e 6 verificações aprovadas, respectivamente |
| Manutenção e registro | 14 verificações no ensaio de volume e estagnação, 6 cenários HTTP e duas passagens CLI no candidato |
| Ajuda instalada | system/guide descoberto. O índice apontou release-0500. Leitura das três páginas idêntica aos 2558 bytes do Markdown canônico. SHA-256 10a507e1d7ec22cc57980a0430062dd296f353dbdbf39ff805e9c3896def1e19. ID ausente recusado. |
| Build | 202 verificações documentais, lint nos 474 PHP e inspeção dos 481 arquivos do instalador. Identidade verificada nas quatro instalações de prova. |

Para a frota, publicar instalador e relatório no repositório de distribuição, medir o hash da URL raw e aplicar com plugins/upload, expected_slug e expected_sha256. A comprovação no Site-Teste empregou a transferência privada descrita acima.

## 5. Banco, migração e correção por nova versão

O schema de dados continua na versão 2. As novas contagens ficam no armazenamento existente por site. A política anterior recebe o padrão do novo campo na leitura. A revisão usada pela seleção preserva a identificação dos lotes da 0.49.0. No laboratório, o processo da base foi interrompido antes da remoção de um componente SQL. Depois da instalação da 0.50.0, a seleção original continuou válida, o ajuste do limiar foi aceito e uma tentativa de alterar o critério de exclusão foi recusada enquanto o lote estava em andamento. A retomada concluiu a seleção. Configuração, conexão, credencial sintética e sentinela da base passaram nas verificações de migração. A pré-imagem do Site-Teste ficou no recibo 94b2088fbb0e32104d2e99b4. Correções posteriores usam nova versão.

## 6. Pendências e responsáveis

- **Equipe do Core.** Incorporar e publicar a delegação testada. O Core 1.94.0 oficial do Site-Teste ainda decide pelo caminho antigo quando executa seu próprio observador. O impacto individual contém o patch e a prova.
- **Frota.** Distribuir os pacotes coordenados e acompanhar 24 horas nos 11 sites, com WP-CLI a cada 15 minutos. Conferir no histórico contexto, origem e horário das transições. A janela começa após a implantação em cada site.
- **Frota.** Na próxima troca em site com acúmulo, conferir a redução real do acervo e a ausência de aviso de manutenção durante o avanço. A medição anterior de retenção por 24 horas em CTOOffice continua com a frota.
- **Alcance das evidências.** As falhas induzidas, a interrupção SQL e as execuções com 2.000 backups ocorreram em bancos descartáveis. O Site-Teste foi verificado por leituras autenticadas e simulação de configuração. No fim, o Core indicava destino configurado, registro recuperado e zero entregas pendentes para esse incidente. O recebimento na caixa postal e a operação dos 11 sites ficam fora da homologação desta rodada.

## 7. Credenciais e configuração do dono

A atualização utiliza a conexão autorizada existente e as permissões administrativas do WordPress. Em Ferramentas → Fator3 MCP → Configurar → Arquivos e banco, o dono pode simular e salvar o número de passagens sem avanço. O destino de aviso permanece no Site Core, em Avisos técnicos por e-mail. A alteração do destino é independente do limiar. O ensaio do painel local usou credenciais descartáveis.

## 8. Identidade dos arquivos

| Artefato | Nome e link | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador WordPress | [wp-mcp-fator3-0.50.0-instalador.zip](https://chatgpt.com/library?file_id=libfile_fde3_f-f658e72e8c808191809e6dab6ced7099_32706b9c47908191baafe72f89b6caee&account_id=personal) | 966854 | 97f6c6a233c2210e24cdef205a66a41c95e20eca9ad8f3644e518bc8ed4ee95f |
| Fonte | [wp-mcp-fator3-0.50.0-fonte.zip](https://chatgpt.com/library?file_id=libfile_fde3_f-a276d4f588a88191b49c0dd11446b8cd_32706b9c47908191baafe72f89b6caee&account_id=personal) | 3426173 | 6996cd0aeedb4543df96b341915ddce32e89b7545ff7e22250887390fee43cc4 |

Relatório externo da entrega. A cópia interna foi fechada antes do cálculo da identidade do próprio fonte. O checklist de encerramento está em evidencias/0500/checklist.json. O instalador é o arquivo próprio para o WordPress.
