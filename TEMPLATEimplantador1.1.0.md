# TEMPLATE — como nasce um site novo a partir daqui

Este pacote é um **template de criação de sites**. Ele não é o site de ninguém: é o
site demonstrativo do método, mais as três peças que produzem qualquer site desta
operação. O agente que cria um site novo **copia deste pacote** em vez de inventar
markup, e a ordem abaixo é executável de cima para baixo.

Duas coisas que este documento não faz, e é deliberado: não traz número nenhum — número
em documento entregável envelhece em silêncio, e os que existem no pacote saem gerados
em `README.md` e `MANIFESTO.md` — e não repete a explicação de nenhuma regra, que mora
em `MEMORIA-DECISOES.md`.

---

## Ordem de execução

### 1. Copiar o pacote e renomear o prefixo

```
cp -a implantador-base <pasta-do-site-novo>
bash <pasta-do-site-novo>/ferramentas/renomear-prefixo.sh <prefixo> <pasta-do-site-novo>
```

O prefixo é o **nome técnico deste site**: diretório e slug do tema, slug do plugin
persistente, prefixo das options e das metas, text domain, handles de asset, classes CSS
e prefixo das classes PHP. Ele obedece `[a-z][a-z0-9-]`, tem pelo menos duas letras, e a
ferramenta **recusa** prefixo vazio, com caractere fora dessa faixa, igual ao do template
ou em colisão com o espaço de nome do WordPress — a lista de recusas e o motivo de cada
uma estão em `ferramentas/prefixos-recusados.tsv`.

- **Rodar duas vezes com o mesmo prefixo não muda nada na segunda.** A busca é sempre
  pelo prefixo de ORIGEM, declarado em `ferramentas/prefixo-do-template.tsv`, que a
  ferramenta nunca reescreve.
- **A renomeação acontece uma vez, a partir do template.** Para um prefixo diferente,
  parta de uma cópia nova — renomear o já renomeado não é suportado, e fingir que é
  produziria um pacote meio num prefixo e meio noutro.
- **O que sobra do prefixo antigo está declarado**, arquivo a arquivo com o motivo, em
  `ferramentas/excecoes-de-prefixo.tsv`. `estatica.sem_residuo_de_prefixo` confere que
  nada sobrou fora dessa lista.
- **`MEMORIA-DECISOES.md` não é reescrito, e isso é decisão.** Ele narra defeitos
  medidos citando diretórios e nomes que existiram em sites reais. Trocar o prefixo
  nessas frases inventaria um passado que não aconteceu: nenhum site com o seu prefixo
  produziu aqueles diretórios. O documento viaja com o pacote como história herdada,
  atribuída a quem a produziu; o site novo abre o próprio registro.

### 2. Trocar a identidade

| O que | Onde |
|---|---|
| Nome e tagline do site | `config/site.json` → `site.nome`, `site.tagline` |
| Endereço canônico | `config/site.json` → `ambiente.url_canonica` |
| Sufixos de domínio de prévia da hospedagem | `config/site.json` → `ambiente.dominios_de_previa` |
| Organização para dados estruturados | `config/site.json` → `seo.organizacao.*` |
| Cores, tipografia, espaçamento | `fontes/tema/theme.json` → `settings.color.palette`, `settings.typography`, `settings.spacing` |
| Regras que o theme.json não expressa | `fontes/tema/style.css` |
| Prova de contraste da paleta nova | `fontes/tema/CONTRASTE.md` |
| Logotipo em vetor, servido no markup | `assets/logo.svg` |
| Logotipo em bitmap, para a biblioteca | `assets/logo.png` |
| Ícone do site | `assets/favicon.png` |
| Imagem social padrão | `assets/social.png` |

A paleta é **lockdown**: valor avulso não é aceito pelo editor, e cor literal no tema é
acusada. Toda cor nova entra como preset em `theme.json` e é usada por `var:preset|…`.
`a11y.contraste` recalcula os pares em uso a cada rodada — paleta nova que não passa no
piso AA reprova ali.

### 3. Substituir o conteúdo

Cada página declarada em `config/site.json` → `paginas[]` tem um arquivo em
`content/pages/<ref>.html`; cada post em `posts[]` tem `content/posts/<slug>.html`.
Todos abrem hoje com a marca de conteúdo demonstrativo — é ela que diz a quem abre o
arquivo que aquilo é do template e é substituível.

- Troque o conteúdo de cada arquivo, **e a marca sai junto**.
- Ajuste `paginas[]`, `posts[]` e `categorias[]` para o que este site tem de verdade.
- As frases obrigatórias e as proibidas deste projeto vivem em `copy_contrato` e são
  conferidas por `copy.contrato` — ajuste-as antes de escrever, não depois.
- **Nada de placeholder.** `estatica.detector_placeholder` reprova `{{x}}`, `[[x]]`,
  `[x]`, TODO, TBD, XXX, LOREM e a palavra de exemplo em maiúscula no conteúdo publicado.

### 4. Preencher contato e controlador

| Chave | O que segura enquanto estiver vazia |
|---|---|
| `contato.whatsapp_e164` | o regime whatsapp **não existe**: `formulario.contato-whatsapp` fecha N/A e o CTA **não é publicado**, nem como link simples |
| `formularios[].caixa_de_leads` (regime `cf7-email`) | o regime **não existe**: `formulario.landing-cf7` fecha N/A e a caixa de leads não tem destino declarado. A chave mora **dentro da entrada do regime**, e não no topo de `contato`: ela é propriedade do formulário, e nenhum módulo do site-core a lê |
| `contato.controlador.razao_social` | a política de privacidade **não publica** |
| `contato.controlador.documento` | idem |
| `contato.controlador.endereco` | idem |
| `contato.controlador.encarregado` | escolhe qual das duas redações do encarregado é servida |

A política de privacidade é o caso a ler com atenção: **nenhuma página deste pacote fica
esperando decisão do implantador para ir ao ar.** A intenção declarada é produção, e o
que segura a publicação é a guarda MEDIDA do controlador — chave vazia fecha BLOCKED
nomeando quais faltam. Preenchidas as chaves, a página publica sozinha na execução
seguinte, sem passo manual.

### 5. Desligar o conteúdo demonstrativo

`config/site.json` → `conteudo.demonstrativo: false`.

**Este é o último passo do conteúdo, e ele vem depois da substituição — nunca antes.**
Desligar a chave com os arquivos ainda marcados não cala nada: `conteudo.marca_demonstrativa`
acusa a divergência arquivo a arquivo, e a publicação é **recusada** em tempo de aplicação,
com o nome do arquivo e as duas saídas. Enquanto a chave estiver ligada e
`ambiente.tipo` for `producao`, `conteudo.demonstrativo` fecha WARN nomeando as páginas
que continuam sendo do template.

### 6. Rodar a suíte

```
bash suite/verificar.sh <caminho-absoluto-do-pacote>
bash suite/verificar.sh piso
```

Caminho **absoluto**: rodar sem argumento reprova por desenho. As duas rodadas precisam
fechar com **FALHA 0**. BLOCKED com fase declarada não impede a entrega — é medição que
este ambiente não pode fazer. WARN é achado adverso que não bloqueia: leia cada um e
decida; nenhum deles sai sem nomear o que está adverso e o que custa.

### 7. Instalar

O bundle sai em `dist/implantador-base-<versão>.zip`, montado pela primeira etapa do
comando único. A instalação, a execução em lotes, a reversão e o desligamento do canal
estão em `README.md`, e nada disso muda por site.

---

## Depois da instalação: o agente

A premissa que governa esta parte do pacote, nas palavras de quem a definiu: *"Após a
instalação, todas as futuras modificações serão realizadas por um agente através de MCP.
Então o template e plugins não devem tentar evitar que futuras modificações sejam
realizadas."*

O implantador se autodesativa e não volta sozinho. Quem opera o site a partir dali é um
agente, pelo canal MCP — e esta seção diz o que ele **encontra**, o que o pacote
**garante a ele** quando alguém reativa o implantador, e o que o pacote **não faz**.

### O que o pacote garante ao agente

- **Preenche quando falta, não sobrescreve o explícito.** O `href` da política de
  privacidade só é gravado quando está vazio ou é `#`; o `href` do CTA só é reescrito
  quando ainda é o do modelo. Destino que alguém trocou fica como está, no render e no
  clique.
- **Edição vence reexecução.** Toda option do bloco do site-core passa por uma regra de
  três vias: o pacote registra a **base** — o último valor que ele mesmo aplicou — e
  compara base, observado e desejado. Observado igual à base: atualização segura.
  Observado diferente da base e configuração intocada: **preserva**, e o relatório nomeia
  a option e o motivo.
- **Quando a configuração vence, ela sai nomeada.** O único caminho pelo qual o pacote
  grava por cima de uma edição do agente é a configuração ter mudado *aquela mesma coisa*
  depois da última aplicação. Aí ele grava e o relatório imprime a **sobreposição** com os
  dois valores — o que estava no site e o que foi aplicado. Não existe reversão calada.
- **A primeira execução com base declara o que fez.** Numa instalação que já tem a option
  e ainda não tem base, o observado é tratado como base e o desejado é aplicado — e a
  linha do relatório **diz que a base nasceu agora**, porque só nessa execução o pacote
  não consegue distinguir uma edição de um valor que sempre esteve ali.
- **Conteúdo substituído não volta.** O conteúdo que este pacote publica é
  demonstrativo. Uma vez que o agente o trocou pelo do cliente, nenhuma atualização do
  template sobrescreve: o pacote só grava conteúdo em objeto que ninguém tocou, e a
  divergência preservada sai nomeada por campo.
- **Par de redirect removido não volta.** O par que estava na base e não está mais na
  option foi apagado por quem opera o site: a união não o recria, nem pela configuração
  nem por uma etapa que o recompute, e o relatório o nomeia. Refazer o par pelo canal o
  traz de volta na execução seguinte — a marca de removido não é permanente.

### O que o agente encontra

| O que ele quer | Onde está |
|---|---|
| Ler os leads recebidos | rotas de **banco** do canal (`db/query`), credenciadas e auditadas |
| Reindexar uma categoria rasa que o pacote marcou como `noindex` | grava `wpseo_noindex = 'index'` no termo; o módulo honra o valor do termo em vez de recalcular |
| Ligar GA4, Google Ads, Meta ou LinkedIn | as options de medição, pelo canal: `f3base_gtm_container_id`, `f3base_ga4_measurement_id`, `f3base_google_ads`, `f3base_meta_pixel_id`, `f3base_linkedin_partner_id`, `f3base_linkedin_conversion_id` |
| Saber quais options ele pode gravar | `f3base_operaveis`, que o implantador grava com a lista |
| Saber o que o pacote aplicou por último | `f3base_base_merge` — a base de merge do conteúdo e das options |
| Acrescentar uma chave que o pacote não conhece a uma option de grupo | grava normalmente: os sanitizadores **preservam** a chave desconhecida em vez de descartá-la na primeira leitura |

### O que o pacote não faz

- **Não expõe os leads ao REST.** O CPT de contingência nasce com
  `show_in_rest => false`, e isso **não** é impedir modificação: é não expor dado pessoal
  de titular a toda credencial autenticada do site. A saída existe e é a de cima — as
  rotas de banco do canal, que são credenciadas e auditadas. O que não existe é a
  exposição por padrão.
- **Não pede ao canal que recuse a escrita do agente.** Os filtros de options protegidas
  do servidor MCP saíram do pacote inteiros. O que ficou no lugar é rastro: toda escrita
  passa pelo gravador único, a procedência fica registrada, e a cadência do modo
  somente-relatório relê as options e reporta o que divergiu.
- **Não recusa ID de medição fora da forma esperada.** Ele preserva o valor e emite um
  aviso nomeando a forma — apagar em silêncio é o que este pacote parou de fazer.

---

## O que muda por site

| Item | Onde |
|---|---|
| Prefixo técnico e tudo preso a ele | `ferramentas/renomear-prefixo.sh` (passo 1) |
| Nome, tagline, endereço, domínios | `config/site.json` → `site.*`, `ambiente.*` |
| Identidade visual | `fontes/tema/theme.json`, `fontes/tema/style.css`, `assets/*` |
| Conteúdo editorial | `content/pages/*.html`, `content/posts/*.html` |
| Páginas, posts, categorias, mídia declaradas | `config/site.json` → `paginas`, `posts`, `categorias`, `midia` |
| Navegação | `config/site.json` → `navegacao` |
| Contato e controlador | `config/site.json` → `contato.*` |
| Contrato de copy | `config/site.json` → `copy_contrato` |
| Herança do template | `config/site.json` → `conteudo.demonstrativo` |
| Resíduo da instalação limpa | `config/site.json` → `conteudo.exemplo_do_wordpress` |
| Estrutura de permalinks e cobertura das URLs antigas | `config/site.json` → `ambiente.permalinks_decisao` |
| Plugins operacionais e protegidos do cliente | `config/site.json` → `plugins.operacionais`, `plugins.protegidos` |
| Piso de ambiente da hospedagem | `config/site.json` → `ambiente.limites_minimos` |
| Retenção e base legal | `config/site.json` → `retencao.*` |
| Medição de GA4, Google Ads, Meta e LinkedIn | options do site-core: `f3base_gtm_container_id`, `f3base_ga4_measurement_id`, `f3base_google_ads`, `f3base_meta_pixel_id`, `f3base_linkedin_partner_id`, `f3base_linkedin_conversion_id` — todas operáveis pela tela e pelo canal, todas nascendo vazias e inertes. Container preenchido desliga toda tag direta |

## O que nunca se toca

Isto não é preferência: é o que fez este pacote parar de repetir defeito. Mexer aqui é
recomeçar do zero a série de correções que a memória registra.

| Item | Onde vive |
|---|---|
| **A arquitetura das três peças** — implantador que se autodesativa, tema FSE, site-core persistente | `implantador-base.php`, `fontes/tema/`, `fontes/site-core/` |
| **O gravador único**: nenhuma escrita de option fora dele | `includes/class-f3base-imp-gravador.php` · detector `estatica.detector_escrita_unica` |
| **O journal e a preimagem**: toda mutação reversível registrada antes de acontecer | `includes/class-f3base-imp-journal.php` |
| **Os gates da autodesativação**: entregáveis e canal, cada veredito derivado num lugar só | `includes/class-f3base-imp-entrega.php` · detector `estatica.gate_fonte_unica` |
| **Os seis estados fechados** — OK, FALHA, BLOCKED, N/A, WAIVED, WARN | `suite/lib/regra.php` · detector `estatica.estados_fechados` |
| **A disciplina de teto e piso**: detector sem fixture negativa e positiva não entra | `suite/fixtures/` · runner `suite/lib/piso.php` |
| **WARN só com achado adverso** | detector `estatica.warn_tem_ramo_adverso` |
| **Contagem sempre com nomes** | detector `estatica.contagem_com_nomes` |
| **Unidade reflete as internas**: nenhuma unidade fecha mais leve que a checagem que ela contém | detector `estatica.unidade_reflete_internas` |
| **O comando único**: empacotar, verificar, selar — nesta ordem, sem atalho | `suite/verificar.sh` |
| **A allow-list de caminhos**: arquivo fora do inventário aborta o build | `suite/inventario.tsv` |
| **Os blocos gerados dos documentos**: número em entregável sai de leitura de disco | `suite/lib/documentos.php` · detector `estatica.carimbo_de_release_nos_documentos` |
| **Conteúdo editorial em arquivo, código executável em arquivo** | `content/`, `*.js` · detector `estatica.detector_codigo_em_string` |
| **O lockdown do theme.json** | `fontes/tema/theme.json` · checagens `tema.*` |
| **O registro da origem do template** | `ferramentas/prefixo-do-template.tsv` |
| **A memória de decisões deste template** | `MEMORIA-DECISOES.md` |
