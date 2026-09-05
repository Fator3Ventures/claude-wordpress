# TEMPLATE do implantador — o mapa da operação

**Implantador 1.7.0 · Base Site Core Fator3 1.0.0**

Este documento é o **mapa**, não o território. Ele existe para um agente que chega sem
contexto nenhum e precisa saber, em cinco minutos: quais documentos existem, o que cada um
responde, em que ordem se lê, e qual é o fluxo executável de ponta a ponta.

Nada aqui substitui os documentos que ele aponta. Se uma frase deste arquivo discordar de
um deles, **o documento vale e este está velho** — o número da versão no nome deste arquivo
acompanha o implantador justamente para que essa discordância seja visível.

---

## 1. Os documentos, e o que cada um responde

Há **três trabalhos diferentes** nesta operação, e cada um tem o seu documento. Quase todo
erro de agente novo é ter aberto o documento do trabalho errado.

| Se o seu trabalho é… | O documento é | Ele responde |
|---|---|---|
| **construir ou corrigir o implantador**, o tema e o conteúdo | `Instrucoes-Construcao-Wordpress.md` — o prompt-mestre | como se constrói o pacote inteiro do zero: as três peças, a configuração, os lotes, o gravador único, o relatório, a suíte, o empacotamento e as armadilhas conhecidas |
| **derivar um site novo** deste template | `TEMPLATE.md`, dentro do pacote | a ordem executável de cima para baixo: copiar, renomear, trocar identidade, substituir conteúdo, preencher, rodar a suíte, instalar e publicar |
| **mudar o plugin do site** | `INSTRUCOES-DO-PLUGIN.md`, **dentro do zip do plugin** | o registro único de módulos, o catálogo de options, as duas tabelas, as rotas REST, a medição de comportamento inteira e o que a suíte cobra de quem mexer |

E mais três, que são de consulta e não de execução:

| Documento | O que é | Quando abrir |
|---|---|---|
| `README.md`, no pacote | o leia-me do OPERADOR: árvore de arquivos, pré-requisitos, instalação, execução, reversão, remoção, plugins recomendados | quando algo do implantador precisar ser instalado, executado, revertido ou desligado |
| `MANIFESTO.md`, no pacote | a identidade e o inventário da release: caminho → papel, requisito → checagem, detector → fixtures | quando você precisar saber se uma afirmação tem checagem que a cobre |
| `MEMORIA-DECISOES.md`, no pacote | o PORQUÊ de cada decisão, narrado a partir de defeitos medidos | quando você quiser mudar uma regra e precisar saber o que ela custou para existir |

**A ordem de leitura, para quem chega agora:**

1. **este arquivo**, até o fim — são poucos minutos e ele evita os erros da seção 5;
2. `Instrucoes-Construcao-Wordpress.md`, seções *As três peças* e *Instrumentar o site com o plugin* — é ali que mora a fronteira entre o que se constrói e o que se instala;
3. `TEMPLATE.md`, do começo ao fim, se o trabalho for um site novo;
4. `INSTRUCOES-DO-PLUGIN.md`, **só** se o trabalho for mexer no plugin;
5. `README.md` e `MEMORIA-DECISOES.md`, sob demanda.

---

## 2. As três peças, e qual delas é renomeada

Esta é a tabela que mais evita estrago. Um agente que não a souber vai tentar renomear o
plugin, e vai quebrar sites.

| Peça | O que é | Release | Renomeada por site? |
|---|---|---|---|
| **Tema de blocos (FSE)** | apresentação: `theme.json`, templates, parts, patterns, CSS | acompanha o pacote, com numeração própria no cabeçalho do `style.css` | **sim** |
| **Implantador** | orquestra a implantação e se autodesativa ao terminar | é a identidade da release | **sim** |
| **Plugin do site — `Base Site Core Fator3`** | comportamento persistente: medição, consentimento, leads, retenção, cabeçalhos, `llms.txt`, redirects, schema | **própria**, recomeçada em 1.0.0 | **NÃO** |

**Por que o plugin fica fora, e a razão não é organização: é dado vivo.** Até a 1.6.6 a
renomeação varria a raiz inteira e cada site produzia um **fork** do plugin, com options
`<prefixo>_ga4_measurement_id` em vez de `f3base_ga4_measurement_id`. Um plugin cujo nome de
option muda por site não é um plugin: são N plugins parecidos, e **nenhuma correção publicada
alcança nenhum deles**.

- **Nome de PASTA é endereço** — trocá-lo custa uma reinstalação.
- **Nome de OPTION é chave de dado** — trocá-lo órfã o valor sem apagar nada e sem erro.
- **Nome de TABELA** apaga a série histórica; **nome de EVENTO** quebra a série na conta do
  fornecedor, onde não há reparo depois.

Os caminhos que a ferramenta **não atravessa** são `fontes/plugin/` e `partilhado/`,
declarados com o motivo em `ferramentas/excecoes-de-prefixo.tsv`. E, porque o implantador
renomeado continua **gravando** o que o plugin **lê**, as grafias de
`fontes/plugin/dados/contrato-de-nomes.tsv` sobrevivem **também dentro dos arquivos que são
renomeados**.

**A exceção mais fácil de errar é `f3base-secao-`,** o prefixo da classe que marca uma seção
medida. Ele é carimbado pelo tema e pelo conteúdo — renomeados — e procurado pelo coletor do
plugin — não renomeado. Trocá-lo por `<prefixo>-secao-abertura` faz o observador não receber
alvo nenhum: **a medição de seções morre calada em todo site renomeado**, com o evento
continuando declarado e respondendo nada para sempre. Ele não é identidade do site: o tema
estiliza `f3base-faixa-escura`, essa sim identidade e essa sim renomeada.

Quem prova tudo isso a cada rodada: `renomeacao.plugin_intacto`,
`renomeacao.secao_medida_apos_renomear`, `renomeacao.contrato_de_nomes_completo` e
`estatica.sem_residuo_de_prefixo`.

---

## 3. O fluxo executável, de ponta a ponta

### De onde se parte

Do pacote `implantador-base`, que é o **template de criação de sites**: o site demonstrativo
do método mais as peças que produzem qualquer site da operação. Ele não é o site de ninguém.

### O que se copia e o que se renomeia

```
cp -a implantador-base <pasta-do-site-novo>
bash <pasta-do-site-novo>/ferramentas/renomear-prefixo.sh <prefixo> <pasta-do-site-novo>
```

Renomeia: tema, options e metas **do implantador**, text domain, handles, classes CSS de
identidade, prefixo das classes PHP. **Não** renomeia: `fontes/plugin/`, `partilhado/` e as
grafias do contrato de nomes. A ferramenta é idempotente — a busca é sempre pelo prefixo de
ORIGEM, em `ferramentas/prefixo-do-template.tsv` — e recusa prefixo inválido antes de
qualquer escrita.

### O que se preenche, e em qual arquivo

**O operador abre um arquivo só: `config/projeto.json`.** Os outros descrevem o pacote.

| Arquivo | O que guarda | Quem responde |
|---|---|---|
| `config/projeto.json` | contato, controlador, fato jurídico, IDs de conta, verificação de domínio, organização no grafo, regimes de formulário, `plugins_operacionais` | o operador |
| `config/site.json` | conteúdo declarado, referências internas entre objetos, identidade técnica do pacote renomeado | o agente que instancia o template |
| `config/decisoes.tsv` | as decisões do PACOTE, cada uma com o MOTIVO escrito ao lado | quem mantém o pacote |
| `config/releases-suportadas.tsv` | de qual versão instalada este implantador sabe subir | a história de homologação |

**A regra que decide em qual arquivo uma coisa mora:** uma chave só se justifica se passar
nas duas metades — existe projeto legítimo em que o valor certo é DIFERENTE, **e** o valor é
impossível de derivar. Falhou numa? Sai da configuração e vira linha de `config/decisoes.tsv`,
com o motivo ao lado.

Depois: identidade visual em `fontes/tema/`, conteúdo em `content/`, e por último
`config/site.json` → `conteudo.demonstrativo: false` — **último**, nunca antes de substituir
os arquivos.

### O que se roda

```
bash suite/verificar.sh <caminho-absoluto-do-pacote>
bash suite/verificar.sh piso <caminho-absoluto-do-pacote>
```

As duas rodadas precisam fechar com **FALHA 0**. BLOCKED com fase declarada não impede a
entrega. WARN é achado adverso que não bloqueia — leia cada um.

**Confira `navegador.comportamento_real` antes de entregar.** É a única checagem que roda o
JavaScript ENTREGUE num Chromium de verdade. N/A ali significa que a máquina não tem Chromium
com `playwright`, e **um pacote verificado sem navegador não é um pacote aprovado**: quatro
releases seguidas a bancada aprovou o que o navegador reprovou.

### O que se instala

A etapa de empacotamento publica **dois zips** em `dist/`:

| Artefato | Numeração | O que se faz com ele |
|---|---|---|
| `dist/implantador-base-<versão>.zip` | do implantador | envio de arquivo em **Plugins → Adicionar novo → Enviar plugin**; ativar e rodar. Ele se autodesativa quando termina |
| `dist/base-site-core-fator3-<versão>.zip` | do plugin, lida do cabeçalho `Version:` | **publicar no catálogo** — ver a seção 4 |

**O implantador instala o plugin sozinho**, do catálogo, pela URL declarada. Você não precisa
instalá-lo à mão.

### Como se sabe que terminou

- a rodada da suíte fecha **sem FALHA**, e o selo grava `suite/rodada.json` com o hash do
  pacote medido;
- no site, o implantador **se autodesativa** — execução terminada com o gate de aplicação
  fechado;
- `conteudo.demonstrativo_no_site` conta **zero** páginas publicadas com a marca do template,
  medido no BANCO e não na configuração;
- `plugins.site_core_versao` não avisa que a versão instalada do plugin é menor que a da
  reserva embarcada;
- os testes de ligação com os consoles (o `generate_lead` chegando no DebugView do GA4, o
  `Lead` único e deduplicado no Test Events da Meta) passaram — esses são a única prova de
  que a conta do fornecedor recebe o que o site emite.

---

## 4. O que se publica no catálogo, e com que nome

Três artefatos desta operação **não vêm do WordPress.org**: eles descem de URL declarada no
repositório `Fator3Ventures/claude-wordpress`, em `main`.

| Artefato | Nome do arquivo publicado |
|---|---|
| **Plugin do site** | **`base-site-core-fator3.zip`** |
| Servidor do canal MCP | `wp-mcp-ultimate-main.zip` |
| Complemento do canal MCP | `wp-mcp-ultimate-complemento-fator3.zip` |

> **O NOME DO ZIP DO PLUGIN MUDOU NA 1.7.0.** Publique
> **`base-site-core-fator3.zip`** — sem número no nome. O `f3base-site-core.zip` antigo
> deixou de ser lido por ninguém, e um repositório que ainda o sirva está servindo um arquivo
> que nenhum site busca.

**Enquanto esse arquivo não estiver publicado, toda implantação cai na RESERVA embutida** —
`assets/plugins/base-site-core-fator3-<versão>.zip`, dentro do bundle do implantador, byte a
byte o mesmo zip que `dist/` publica avulso. A entrega **não falha**: a reserva existe
exatamente para que um endereço que alguém moveu não derrube a implantação.

**E é justamente por isso que o passo é fácil de esquecer, e caro.** Enquanto o zip publicado
estiver atrás da versão que o pacote carrega, toda implantação instala a versão antiga **com
sucesso** — nada falha, o relatório fecha, e os sites já entregues ficam sem a correção. O
terceiro passo do ciclo de release do plugin é o único que alcança quem já está no ar:

1. subir a versão em `fontes/plugin/base-site-core-fator3.php`, **só no cabeçalho `Version:`**
   — a constante `F3BASE_PLUGIN_VERSAO` é derivada dele por `get_file_data()`, e repetir o
   número foi o defeito medido;
2. rodar a suíte, que publica `dist/base-site-core-fator3-<versão>.zip`;
3. **publicar esse zip no catálogo, com o nome `base-site-core-fator3.zip`.**

**Reverter o plugin é republicar.** Não há histórico de versões servido por terceiro: o
catálogo serve um arquivo só. Quem reverte precisa ter guardado o zip da versão de destino.

---

## 5. Os erros que um agente novo comete aqui

Cada um com a consequência, porque nenhum deles se anuncia como erro.

| Erro | Consequência |
|---|---|
| **Renomear o prefixo do plugin junto com o do site** | cada site vira um FORK: options `<prefixo>_ga4_...`, e nenhuma correção publicada alcança nenhum deles |
| **Carimbar a seção como `<prefixo>-secao-<nome>`** | o coletor não recebe alvo nenhum; `f3base_secao_vista` continua declarado, ocupa linha no relatório e responde **nada para sempre** |
| **Escrever a classe da seção só no `className` OU só no `<div class>`** | o editor reescreve o outro na primeira edição e a marca some sem aviso — `estatica.conteudo_declara_secoes` reprova as duas formas |
| **Tentar construir o plugin a partir do implantador** | trabalho jogado fora: a fonte do plugin não viaja no bundle, e nada no implantador o constrói, gera ou edita |
| **Rodar a suíte, ver verde, e não publicar o zip no catálogo** | os sites entregues continuam recebendo a versão antiga, **com sucesso**, sem nenhuma linha de erro |
| **Publicar com o nome antigo `f3base-site-core.zip`** | ninguém lê aquele endereço; toda implantação cai na reserva embutida e nunca recebe a versão nova |
| **Subir o número da versão também numa constante** | cabeçalho e constante divergem, e o site relata uma versão que não é a que está rodando — foi o defeito medido em `1.3.6` × `'1.3.5'` |
| **Preencher medição em `config/site.json`** | ela não mora ali: os IDs de conta são de `config/projeto.json` → `tracking.*`, ou das options pelo canal |
| **Declarar o token da Conversions API da Meta na configuração** | o arquivo viaja dentro do zip: o segredo é copiado para todo lugar por onde o pacote passou, e sobrevive a qualquer rotação. `estatica.segredo_fora_da_configuracao` reprova |
| **Desligar `conteudo.demonstrativo` antes de substituir o conteúdo** | `conteudo.marca_demonstrativa` acusa arquivo a arquivo e a publicação é **recusada** em tempo de aplicação |
| **Renomear um evento de comportamento depois de o site estar no ar** | a série histórica da conta do fornecedor quebra: o nome novo é uma série NOVA, a antiga para de crescer, e nenhum erro aparece |
| **Rodar a suíte numa máquina sem Chromium e entregar** | `navegador.comportamento_real` fecha N/A: a única checagem que mede o cliente fora de uma simulação não rodou |
| **Rodar `suite/verificar.sh` com caminho relativo, ou sem argumento** | reprova por desenho — `FALHA suite.invocacao`, código de saída 2 |
| **Editar `MEMORIA-DECISOES.md` para trocar o prefixo** | inventaria um passado que não aconteceu; o documento é história herdada e está declarado como exceção da renomeação |
| **Digitar um número num documento entregável** | ele envelhece em silêncio. Todo número sai GERADO por leitura de disco, e `estatica.carimbo_de_release_nos_documentos` compara com a medição de agora |

---

## 6. Onde ficar quando a dúvida for de fronteira

- **mudou o SITE** — conteúdo, identidade, contato, IDs de conta → `TEMPLATE.md`;
- **mudou o PLUGIN** — módulo, evento, option, rota, tabela → `INSTRUCOES-DO-PLUGIN.md`, e
  sai uma release do plugin sem tocar no implantador;
- **mudou o IMPLANTADOR** — lotes, preflight, relatório, suíte → `Instrucoes-Construcao-Wordpress.md`
  para construir e `README.md` para operar, e sai uma release do implantador.

**Depois da entrega, o site é do agente.** O implantador se autodesativa e não volta sozinho;
quem opera dali em diante é um agente pelo canal MCP — tema, plugins e conteúdo, sem exceção.
O pacote não protege o que instalou de quem vai operá-lo: ele **nomeia** o que divergiu, em
vez de decidir por quem opera.
