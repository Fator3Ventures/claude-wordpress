# Entrega — Fator3 Site Core 1.83.0

Revisão 1 · 2026-11-13T18:42-03:00 · Pedidos 396 e 397  
Slug `base-site-core-fator3` · Versão 1.83.0 · Contrato administrativo 8.39.0  
**Status — com pendências de aceite em produção e de cobertura da frota.** Instalador conferido e ativo no Site-Teste.

## 1. De onde esta versão entra

Instalação WordPress limpa ou atualização direta da 1.82.0. Conferimos o fonte oficial anterior (SHA-256 `9e30debe6a0c77a4d9b3c4058cdd3117830c5551a2d1992a95826ba7d2d6b69c`) e o instalador anterior (`90bda2bbe2181a44330da121a349d3aa8b967e20ccf848ea7f9b51ac72c94482`). A árvore anterior está em `history/1.82.0-runtime`. As duas normas do projeto são da revisão 5, de 02/11/2026.

WordPress mínimo 7.1.4 e PHP mínimo 8.3 de 64 bits. O laboratório executou WordPress 7.1.4, PHP 8.3.6 e MySQL 8.0.46. O Site-Teste executou WordPress 7.1.4 e PHP 8.3.36.

## 2. Convivência e encaminhamentos

| Pacote | Versão | Evidência |
|---|---|---|
| Fator3 MCP | 0.45.0 | Descoberta, leitura de documentação, transferência e atualização do ZIP |
| Google | 0.34.0 | Teste oficial do provedor com o worker do Core e consulta agregada real ao GA4 da CTO Office |
| Meta | 0.25.0 | Teste oficial do provedor com o worker e repetição da entrega em transporte controlado |
| LinkedIn | 0.22.0 | Teste oficial do provedor com o worker e repetição da entrega em transporte controlado |
| Pipedrive | 0.10.0 | Coexistência e exercício de nota e mapeamentos de lead/pessoa no laboratório |
| Implantador | 2.21.0 | Cinco verificações do contrato de cache e um ajuste no texto que informa a quantidade de parâmetros |

O mantenedor do Implantador recebe o impacto `base-site-core-fator3-1.83.0-impacto-implantador-base.md`, revisão 1, e o patch incluído no fonte. O código do Implantador consome os 47 nomes da versão vigente do Core. A documentação do Implantador ainda cita 35. A alteração documental foi aplicada e validada numa cópia. O Core pode ser instalado independentemente dessa publicação. Os impactos históricos e as regressões de origem das plataformas permanecem no fonte.

## 3. Mudanças e evidência

**396 — aparelho na sessão e no contato.** A coleta de medição registra a primeira observação disponível por classe de tráfego, sessão e visitante. O navegador consulta modelo e versão principal do sistema quando a API está disponível, memória aproximada, núcleos lógicos, largura e altura da tela, DPR e rede efetiva. A coleta depende da autorização de medição. O servidor repete a verificação, limita o esquema e mantém uma única linha por identidade de sessão. O navegador coordena abas por Web Locks quando disponível. A ausência dessa API ainda admite consultas concorrentes em abas distintas, resolvidas pela chave única no servidor.

A faixa deriva do catálogo editável. Sem modelo, a classificação usa memória e núcleos disponíveis. Para iPhone, a tela e o DPR dão uma estimativa explícita. A ficha particular do contato materializa os sinais a partir da referência em `dados.contexto`; a limpeza da medição também vence essa referência. O aviso Slack e a nota Pipedrive consultam a observação retida. Os papéis `modelo_aparelho` e `faixa_aparelho` mapeiam campos personalizados de texto no lead ou na pessoa. As dimensões estão disponíveis nas consultas editoriais e integradas, inclusive na visão de qualidade. O novo perfil exclui IP e user agent bruto e não integra as conversões de anúncios. A ficha histórica geral já possuía dados técnicos próprios. As cópias já entregues a Slack e CRM obedecem à retenção do destino.

O GA4 da propriedade 541364734 confirmou, entre 6 e 12/11, SM-A075M para Galaxy A07 4G (41 sessões), SM-A065M para Galaxy A06 (37) e SM-A032M para Galaxy A03 Core (23). Moto G05 aparece no campo de modelo em 29 sessões. O catálogo inicial do ZIP contém os quatro nomes do pedido. No Site-Teste foram acrescentadas e relidas as três correspondências Samsung por código. Ao implantar na frota, aplicar estes aliases no catálogo de cada site. Modelo presente sem correspondência permanece com faixa desconhecida. O recorte de Android/Chrome de 11 a 12/11 mostrou SM-A065M em 11 sessões. Os relatórios do GA4 são agregados.

**397 — registro único de parâmetros.** O cache consome a união dos papéis definidos em `F3Base_Atribuicao`. A atribuição e o JavaScript usam as projeções de campanha e clique. São 47 nomes únicos. `ref` permanece funcional.

| Novos nomes | Tratamento |
|---|---|
| gad_source, gad_campaignid, utm_creative_format, utm_marketing_tactic | Cache e atribuição de campanha. A captura reduzida remove o ID de campanha Google. |
| msclkid, ttclid, twclid, epik, rdt_cid, dclid | Cache e evidência de clique pago, sujeita à autorização publicitária |
| igshid, _gl | Somente cache |

Em cada instalação indicada abaixo, uma alteração com pré-imagem nomeada gravou a lista em uma linha. O agente releu o arquivo, verificou o conjunto e solicitou a purga. O provedor confirmou o agendamento. Os recibos completos e os hashes antes e depois constam de `evidence/1830/frota-397.json`.

| Instalação | Nomes acrescentados | SHA-256 após a gravação (prefixo) |
|---|---:|---|
| ctooffice.com.br | 12 | da931c14a73099 |
| Site-Teste | 12 | 5da869785aac2e |
| korvena.com.br | 12 | 1d1616c4f3d9e4 |
| conselar.com.br | 12 | 3f6ffb3218af65 |
| desenvolvimentodesoftwares.com.br | 12 | 61345bd3233aa7 |
| engagia.com.br | 12 | fdd8256c2d4e77 |
| fator3.com.br | 12 | d0d926cbc79a09 |
| fator3capital.com.br | 12 | 4b8d0f8d9d91b2 |
| fator3grupo.com.br | 12 | eb999a2c334f50 |
| fator3ventures.com.br | 12 | 4af1a70bd03242 |
| twinia.com.br | 12 | f7805ff8b5a9e7 |

Os backups nomeados estão sob `wp-content/.f3-wpsc-backups/`, com bloqueio de acesso HTTP. O pequeno arquivo usado para testar o bloqueio foi removido. O circuito de entrega de leads do pedido 395 também passou pelas regressões, inclusive edição do cabeçalho com manutenção de ts e thread.

## 4. Instalação e prova da troca

A operação de atualização `39d6c83463db89bc4213ddc379cd83e0` validou o ZIP pelo SHA-256 da seção 8 e pelo slug `base-site-core-fator3`. O Site-Teste passou de 1.82.0 ativa para 1.83.0 ativa. As sondas antes e depois passaram, e outro processo PHP confirmou a ativação. O transporte usou uma URL temporária no próprio Site-Teste. O arquivo temporário e a extensão de QA foram removidos. A URL raw permanente de distribuição depende da publicação pela frota.

| ID | Ambiente | Prova e resultado |
|---|---|---|
| T1 | WordPress local | Suíte em instalação limpa e atualização direta. Os 53 controles específicos de 396/397 passaram em cada fase, incluindo persistência, leitura privada, mapeamento de CRM, vitais por modelo, expiração e limpeza. |
| T2 | WordPress local | Regressões de consentimento, atribuição, filas e integrações, desinstalação e reativação. O catálogo gerado coincide com 194 abilities registradas. |
| T3 | Build | 967 arquivos conferidos, 601 arquivos PHP passaram no lint. Os 84 arquivos JavaScript reproduzidos e os metadados do build conferem por bytes. O instalador final passou pelo Plugin_Upgrader e os 967 arquivos conferiram nas duas instalações. |
| T4 | Chromium 156 | Negativa sem consulta, escopo de Client Hints, uma observação em duas abas, versão principal, revogação durante a consulta e modelo vazio na ausência da API. Sinais do navegador emulados. |
| T5 | Site-Teste | 12 verificações, incluindo o status failed e os 12 faltantes ao reproduzir a configuração antiga, verified com a configuração vigente, primeira observação, iPhone sintético, ficha, aviso e nota renderizados e limpeza do contato. A leitura integral de docs/RELEASE-1.83.0.md retornou a versão nova. |
| T6 | CTO Office | Quatro GET anônimos, dois limpos e dois com gad_source e gad_campaignid. Todos retornaram HTTP 200 e o mesmo HTML completo de 195.674 bytes, incluindo o marcador do provedor. SHA-256 `8ddc68aa99892f527c16babd6c86e8e90fedf21bfa69f995cb7a9751bc36fbf9`. Um pedido limpo foi classificado HIT. Nos pedidos marcados a ferramenta confirmou a igualdade do conteúdo e deixou o indicador individual de HIT indeterminado. |
| T7 | Integrações | Os trabalhadores Meta, Google e LinkedIn passaram com as versões da seção 2. Para o Pipedrive a nota foi criada a partir do contato persistido e as duas projeções de campo foram verificadas com catálogo controlado. |

Testes reproduzíveis e resultados em `tests/` e `evidence/1830/`. Para o comportamento específico da release, use `396-397.php`, `navegador-396.py` e `implantador-397.php`. O arquivo `site-teste.json` distingue sondas externas, dados sintéticos e limpeza. O site de teste permaneceu com a versão 1.83.0 ativa.

## 5. Banco, migração e correção por nova versão

A instalação ou migração cria a tabela privada `<prefixo>f3base_aparelhos`, com chave composta de classe, sessão e visitante, e índice temporal. A gravação repetida preserva a primeira observação. O corte de retenção acompanha o da análise e a leitura verifica a validade antes da remoção periódica. Linhas anteriores à atualização não têm histórico de aparelho retroativo. O Core não altera arquivos de cache da frota por conta própria. Para a distribuição, preserve a pré-imagem da configuração e os dados da instalação. Uma correção posterior do instalador deve ser uma nova versão.

## 6. O que permanece pendente

- A comparação individual Android/Chrome × GA4 em ctooffice.com.br e a observação em iPhone físico aguardam a implantação do Core na CTO Office e tráfego consentido. O site ainda informava Core 1.82.0. A consulta agregada não identifica a mesma sessão nos dois sistemas.
- A conta configurada no Site-Teste é a conta comercial fator3.pipedrive.com. A homologação está desativada, e o consumidor administrativo do Pipedrive está desautorizado. Nenhum contato ou nota deste ensaio foi enviado à conta comercial. A verificação da nota diretamente na conta e a remoção posterior dessa nota ainda requerem um destino autorizado.
- O pedido cita 12 sites. Houve confirmações de 10 sites de produção e do Site-Teste. O inventário definitivo e a conexão de escrita dos demais domínios não foram obtidos. Configuração e purga desses domínios continuam pendentes.

## 7. Credenciais e configuração do dono

O pacote usa as credenciais já cadastradas. Para classificar aparelhos na frota, edite **Configurações → Medição e anúncios → Conteúdo, audiência e IA → Faixa por modelo de aparelho**. No catálogo existente, acrescente `SM-A075M=entrada`, `SM-A065M=entrada` e `SM-A032M=entrada`. Para usar o filtro comercial, em Pipedrive associe os papéis a campos de texto do lead ou da pessoa no catálogo da conta. A faixa estimada descreve o aparelho e não constitui medida de perfil comercial do visitante.

## 8. Identidade dos arquivos

| Artefato | Bytes | SHA-256 |
|---|---:|---|
| base-site-core-fator3-1.83.0-instalador.zip | 4.453.751 | `9168a066d0e85468be3580afc88a1b063bf36b80ad8ab84b0b0ca57f4cc322cf` |
| base-site-core-fator3-1.83.0-impacto-implantador-base.md | 1.827 | `eafc9595941de04b16aa83308776c8afd9638af81ee181b331ccceae4e89aeb1` |
| base-site-core-fator3-1.83.0-fonte.zip | 52.198.365 | `462082c8ad085140d7c657a90df3e31ac7d99df09b6c4d3380918183d6db0677` |
