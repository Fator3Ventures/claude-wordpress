# Entrega — Fator3 Site Core 1.90.0

Revisão 1 · 2026-11-16T11:45:54-03:00 · Implementação dos pedidos 418 a 420  
Estado da entrega: **com-pendencias** de homologação na frota. A implementação passou no laboratório e no Site-Teste. O aceite da frota depende da instalação e de uma janela de 24 horas corridas no CTO Office.

## 1. De onde esta versão entra

Instalação nova ou atualização direta da **1.89.2**. A base utilizada foi o instalador fornecido, SHA-256 `01b62a0223624cc167ef49a4ff03ac8d82cc8893954aeac2d7b7968bde4b9bfa`. O laboratório exerceu o piso declarado em WordPress 7.1.4 e PHP 8.3.6 de 64 bits, na série PHP 8.3. O teste no site compartilhado partiu da 1.89.2 ativa. O instalador recuperado dos chats foi conferido, instalado e entregue com o mesmo hash.

## 2. Convivência e encaminhamentos

Contrato administrativo **8.42.0**, contrato de dados **8.38.0**, perfil **piso-padrao-3.6**, **104 opções operáveis** e **197 operações**. A comparação dos catálogos da 1.89.2 e da 1.90.0 confirma os mesmos 197 nomes. Na leitura de pendências de aparelhos, `itens` permanece como alias de `sem_nome`. Os clientes interessados em fichas comerciais incompletas podem ler `sem_ficha_comercial`.

O Site-Teste manteve ativos MCP 0.46.0, Google 0.36.0, Meta 0.27.0, LinkedIn 0.24.0 e Pipedrive 0.11.1. A troca se restringe ao Core. A inspeção do Implantador 2.23.0 confirmou a descoberta dos contratos e a propriedade do catálogo pelo Core. A conciliação de filas, as confirmações e o enriquecimento para Slack são internos ao Core. Nenhum acompanhante exige alteração para os três pedidos. A presença dos acompanhantes no site comprova convivência de instalação e leitura remota. A rodada não exerceu contas externas desses fornecedores.

## 3. Mudanças e evidências

**Pedidos core 418.** `lm-x525` ganhou a ficha **LG Q60**, codinome `mmh4p`, ano 2019, faixa intermediária e linha premium não. O preço de R$ 259,00 é estimativa de seminovo baseada na variante brasileira K12 Prime. A referência e as fontes estão em `reference/419/README.md`. O catálogo curado passou a 1.350 códigos, todos conferidos com seis campos e preço positivo.

**Pedidos core 419.** O runtime inclui 256 fragmentos comprimidos da lista Google Play de 15/11/2026. A base tem 44.528 códigos distintos com Model preenchido. Em 43.102 existe nome comercial utilizável. Nos 624 ambíguos e nos 802 sem nome comercial publicado, o Core identifica a situação e conserva o código técnico. A ficha curada tem precedência. A fonte Google fornece identidade e codinome quando determinados, mantendo desconhecidos ano, preço, faixa e linha premium. O Slack usa o mesmo enriquecimento na leitura de perfis retidos. `f3base/como-usar` informa data, contagem e hash da fonte.

Na prova com a base Google isolada, 26 dos 30 códigos históricos receberam nome. Os ausentes foram `220333QPG`, `2606FRN72L`, `M2006C3LII` e `tecno kl4h`. Com o catálogo curado ativo os 30 receberam ficha. Uma consulta em três páginas separou o desconhecido sintético dos códigos `m8_wifi`, `rmx3938` e `sm-j600gt`, reconhecidos sem ficha comercial. A ambiguidade de `m8_wifi` foi sinalizada. A projeção do Slack foi exercitada localmente, sem disparo. Provas em `evidence/1900/wordpress-catalogo.json`, `projecao-google.json`, `codinomes.json` e `curados.json`.

**Pedidos core 420.** No controle da 1.89.2, o WP-CLI gravou a próxima ocorrência e removeu a atual. A segunda passagem, via HTTP, recebeu dois `could_not_set` sobre o mesmo estado já salvo. Na 1.90.0, a segunda passagem confirmou as duas operações sem alterar os bytes da agenda. A reserva única recusou a segunda execução e registrou HTTP como origem recusada e CLI como dona. A prova reproduz esse mecanismo no laboratório. A atribuição dos 620 registros históricos do CTO Office a uma única causa não foi demonstrada.

O Core concilia o evento específico em `cron`, confere o estado persistido e repete a gravação condicional se outra escrita vencer a disputa. Erros de persistência continuam observáveis. A recuperação CAPI manteve uma passagem diária por perfil. No teste separado de item novo, a falha induzida no agendamento individual provocou uma antecipação. A repetição de 100 ciclos de reinserção e releitura não provocou gravações extras. Pipedrive passa a confirmar a verificação local de orçamento e LinkedIn agrega os resultados por integração.

### Ensaio de 24 horas simuladas

Por perfil foram 288 intervalos, três requisições simultâneas a `wp-cron.php` a cada 5 minutos e uma execução de `wp cron event run --due-now` a cada 15 minutos. WP-Cron por visita permaneceu ligado. A instrumentação isolou os seis ganchos, bloqueou saídas externas e preservou os callbacks e tabelas das filas sob teste.

Cada célula mostra **concluídas por HTTP / concluídas por CLI**. Zero nos dois canais indica gancho inativo naquele perfil.

| Gancho | Perfil B | Perfil C | Perfil E |
|---|---:|---:|---:|
| `f3base_wp_mail_processar` | 278 / 10 | 267 / 21 | 0 / 0 |
| `f3base_pipedrive_processar` | 275 / 13 | 281 / 7 | 280 / 8 |
| `f3base_email_novo_lead_processar` | 22 / 2 | 17 / 7 | 21 / 3 |
| `f3base_linkedin_notificacoes` | 0 / 0 | 282 / 6 | 0 / 0 |
| `f3base_conversoes_servidor` | 17 / 7 | 19 / 5 | 19 / 5 |
| `f3base_capi_recuperar` | 1 / 0 | 1 / 0 | 0 / 1 |

Somando os três perfis: **1.875 ocorrências concluídas**, **3.232 operações de agenda já persistidas**, **zero** `could_not_set`, **zero** ocorrências executadas duas vezes e **zero** falhas nas filas. Foram 2.592 requisições HTTP com resposta 200 e 288 execuções WP-CLI bem-sucedidas. As reservas recusadas, discriminadas por origem e gancho, estão em `evidence/1900/filas-24h.json`. As contagens e os rastros sintéticos no mesmo diretório permitem refazer a agregação conforme `tests/420/README.md`.

## 4. Instalação e prova da troca

| Prova | Resultado observado |
|---|---|
| Instalação limpa em banco descartável | O WP-CLI instalou e ativou o ZIP em WordPress 7.1.4 e PHP 8.3.6. O Core informou 1.90.0, 1.350 fichas e a operação de consulta disponível. O verificador de atualizações do WordPress encontrou indisponibilidade de rede externa no laboratório. |
| Correspondência dos bytes | Os 1.263 arquivos do instalador coincidem com o fonte e com a instalação limpa. Os três perfis executaram o mesmo PHP. Os 17 arquivos que diferem entre as árvores do ensaio e o ZIP são de documentação e histórico de mudanças. Lint da rodada original: 609 arquivos PHP aprovados. |
| Site-Teste | Atualização 1.89.2 → 1.90.0 ativa. Recibo `062fa1aac1eae3624b352bceaf679275`. Home e REST responderam 200 antes e depois. O diagnóstico confirmou 20 etapas concluídas em 8 s e zero falhas. O ZIP temporário de homologação ficou ausente após a instalação, conforme a verificação do caminho. |
| Leitura pelo MCP | O índice lista 244 documentos. `docs/RELEASE-1.90.0.md` foi lido em duas páginas, até o fim, e confrontado integralmente com o instalador. SHA-256 `f5f880a8399d201dd3ed47fd7ee7fe615303a8b4ccc1030406c35d265756d359`. Um ID fora do catálogo foi recusado. |
| Catálogo remoto | `f3base/aparelhos-sem-nome-ler` retornou as duas listas, com zero códigos retidos no Site-Teste e cursor final nulo. As provas com perfis não vazios constam do laboratório. |

Estado final do Site-Teste: zero tarefas com última falha e zero módulos degradados. Logo após a troca, o módulo de robots.txt aguardava confirmação pública. Executamos o evento de verificação já vencido e uma nova leitura confirmou o módulo ativo. O ensaio com dados sintéticos ficou restrito aos bancos descartáveis. O site compartilhado recebeu somente o instalador.

**Procedimento da frota.** Publicar o instalador no repositório conforme o fluxo da frota, conferir o SHA-256 dos bytes servidos e usar `plugins/upload` com `expected_slug=base-site-core-fator3`, `expected_sha256` da seção 8, sobrescrita e ativação. Aguardar em nova requisição `f3base/como-usar` com `versao_alvo=1.90.0`, `estado=concluida`, `falhas=0` e `confirmada_no_executor_em` preenchido. O canal de homologação no Site-Teste foi `plugins/upload-base64` com `zip_path`, slug e hash verificados. A distribuição pública cabe à frota.

## 5. Banco, migração e correção por nova versão

A alteração usa a opção de cron e a reserva de ocorrência já existentes. As tabelas das filas e o índice único de ocorrências são preservados. O registro de disputa identifica a ocorrência dona e a origem recusada. A consulta de aparelhos enriquece a leitura com as bases locais. A instalação não demanda reimportação, reenvio de mensagens, troca de credenciais ou migração reversa. Se uma execução for interrompida, conferir o estado da atualização e os recibos antes de retomar. Correções após a instalação seguem em nova versão.

## 6. Pendências e responsáveis

- **Frota, CTO Office.** A leitura prévia na 1.89.2 percorreu 143 códigos e terminou com seis pendentes, inclusive `lm-x525` em dois perfis. Após a troca, percorrer a consulta com `limite=200` e `apos=proximo_apos` até o cursor nulo. Confirmar a saída do LG Q60 de `sem_nome` e verificar os códigos remanescentes contra o índice Google Play.
- **Frota, janela de 24 horas corridas a partir da troca.** Somar os `could_not_set` dos seis ganchos no log do CTO Office, exigir menos de 10, verificar zero duplicações em `f3base_execucoes`, filas sem falha e motivo de cada antecipação de CAPI. O ensaio de laboratório cobriu a carga descrita acima.
- **Limites da rodada.** As provas de Slack, CAPI, Pipedrive e LinkedIn cobriram a projeção de dados, o agendamento e a confirmação locais, conforme a função de cada integração. Entregas a contas reais e comportamento com tráfego de produção permanecem separados. A revisão conferiu o gate administrativo no código. Não houve nova sessão com perfil restrito no Site-Teste nem ensaio visual de navegador.

## 7. Credenciais e configuração

A atualização não cria campos de credencial nem exige importação de CSV. Correções locais do catálogo continuam em `f3base_medicao_editorial.catalogo_aparelhos`. A base Google Play e as instruções de regeneração estão no fonte. A cópia de runtime é local ao plugin.

## 8. Identidade dos arquivos

| Artefato | Nome | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [base-site-core-fator3-1.90.0-instalador.zip](base-site-core-fator3-1.90.0-instalador.zip) | 5622059 | `84a978143955df3803a6724fe5e967e1114b89476e198a52b594d6dc599c660f` |
| Fonte | [base-site-core-fator3-1.90.0-fonte.zip](base-site-core-fator3-1.90.0-fonte.zip) | 7382701 | `4c91802d6db0a07cd72f21dc9a7afbd95f922b262c381e687cee3ea772b975a3` |
| Catálogo comercial | [base-site-core-fator3-1.90.0-catalogo-aparelhos.csv](base-site-core-fator3-1.90.0-catalogo-aparelhos.csv) | 79554 | `eb9d9665658ff876dc7cb487899e4a585dbc6c4cefa1a957292855cd513299e2` |

A cópia dentro do fonte antecede o fechamento do ZIP. O tamanho e o hash finais do fonte constam deste relatório externo.
