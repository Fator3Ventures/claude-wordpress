# Entrega — Fator3 Site Core 1.63.0

30/10/2026 · revisão 1 · contrato administrativo **8.28.0**. Implementada e instalada no Site-Teste. Pedidos 352, 353, 355 e 356 têm implementação e provas técnicas; os aceites de frota/Meta continuam externos. **O pedido 354 está parcialmente implementado e não atingiu o limite de 100 ms. Não deve ser encerrado.**

## Bases aceitas

Base canônica 1.62.0: instalador 2948015 bytes, SHA-256 `3dcbae9b1e22b915ac32ae3074cec1ed15706d4a475a9cf5d5b9e12663922646`; fonte 5859483 bytes, SHA-256 `dd6f4dd466a57ec2cdcbf72492a98678a966dc38e96123c5f8fa1255b61cbe0a`. A atualização direta e a instalação limpa usam essa base e o instalador final exato. Não foram acrescentados saltos históricos ao suporte desta rodada.

Pedidos: `Fator3 Site Core(20261030-181329).md`, 20186 bytes, SHA-256 `bbf196e157449fb47f95ea24d9acb238218019c6ea2f60a60a0bbebc94fa7033`. Instruções e padrão comuns revisão 4 aplicados. Novos pacotes e relatórios Meta 0.17.0 e Pipedrive 0.5.0 examinados; identidades integrais em `inputs/1630/packages.json`. Relatos recebidos não são contabilizados como testes próprios.

## Convivência e encaminhamentos

| Pacote | Versão | Prova própria |
| --- | --- | --- |
| Fator3 MCP | 0.37.0 | Catálogo, autorização, documentação paginada e operações de instalação/sondagem no Site-Teste. |
| Fator3 MCP Google | 0.24.0 | SDK e armazenamento originais; transporte simulado nas regressões. |
| Fator3 MCP Meta | 0.17.0 | SDK original, campanha/acervos/monitoramento com respostas sintéticas; nenhuma concessão comercial nova. |
| Fator3 MCP LinkedIn | 0.13.0 | Registro e convivência, com cliente preservado. |
| Fator3 MCP Pipedrive | 0.5.0 | Ativo na bancada do Site-Teste em PHP 8.3.36; sem escrita real na conta. Inativo no laboratório PHP 8.3.6 por requisito do acompanhante. |

Somente o Core foi alterado. Os nove plugins originalmente ativos continuam ativos. Nenhum push, publicação na frota ou envio de mensagem a responsáveis foi realizado.

Encaminhamento tecnicamente necessário, identificado na homologação: **`base-site-core-fator3-1.63.0-impacto-wp-mcp-fator3.md`**, aberto, `validacao-coordenada`. O MCP 0.37.0 chama o catálogo completo de habilidades em `MutationServiceAudit::initialize`, no `wp_loaded`, inclusive no login. A pilha nativa confirma essa chamada. A inicialização mínima do Core mantém o catálogo completo quando solicitado para preservar o contrato. A alteração do MCP deve preservar a auditoria de serviço; não foi implementada nesta entrega. Há também custo próprio do Core a reduzir, e o encaminhamento não atribui toda a diferença ao MCP.

## Mudanças por pedido e evidência

### 352 — começo da visita

Consentimento, contexto e tracking passam ao início da página. Meta init/PageView com eventID executa assim que as guardas locais permitem, sem aguardar contexto-publico nem DOMContentLoaded. A exclusão do editor permanece no servidor; cookie/cabeçalho de teste e webdriver impedem o disparo antecipado. Lead e demais conversões continuam aguardando classificação e consentimento. GA4 mantém suas guardas.

Os coletores próprios observam tempo visível, profundidade e gestos em memória desde a primeira execução, com até 200 amostras. Só incorporam/enviam a observação após classificação e consentimento; exclusão/negativa descarta a fila. Eventos reproduzidos conservam o instante, e a página usa ms=0 relativo à navegação. A classificação técnica pode fazer sua própria requisição/diagnóstico; a afirmação de retenção vale para os eventos dos coletores. Tempo ativo por seção começa quando seu DOM está disponível e a coleta é autorizada.

Prova DOM com jsdom 27.4.0, rede interceptada, scripts fonte e minificados: **76 assertivas**, cobrindo normal/teste/cabeçalho/editor/robô/negativa, PageView antecipado, Lead adiado, deduplicação, hashes, início da página e rolagem humana anterior à classificação sem falso salto. Não é medição de navegador real em korvena/mvp nem prova de LCP.

### 353 — persistência da falha IMAP

Configuração em f3base_avisos_tecnicos: imap_falhas_consecutivas, padrão 3; imap_sem_leitura_minutos, padrão 20. Falha incompleta abre incidente quando qualquer limite é atingido. Histórico limitado a 20 ocorrências com data/código, leitura completa e revisão da política. Uma abertura aceita pelo wp_mail permite uma única recuperação após nova leitura completa. Aceitação pelo wp_mail não prova entrega ao destinatário.

Testados episódio transitório sem mensagens, duas passagens silenciosas, terceira abertura única, limite temporal, política personalizada, abertura recusada sem recuperação, histórico limitado, simulação sem gravação e leitura parcial no mesmo segundo que não encerra o incidente. Outros erros preservam o comportamento anterior.

### 354 — carga por contexto e diagnóstico

Mapa fechado para autoload de classes; registro de hooks compilado do código próprio; inicialização mínima no login/contexto-publico; elegibilidade de hooks separada do diagnóstico completo de saúde. O catálogo canônico conserva filtros, sanitização, tradução e contratos. Quando um acompanhante solicita habilidades, a inicialização completa acontece antes do registro das categorias.

Nova leitura administrativa: f3base/desempenho-ler e GET /f3base/v1/desempenho, com manage_options. Informa carga, registro, callbacks instrumentados e tempo próprio/inclusivo. Sondas assinadas, limitadas à página/login, 1–3 amostras, sem alterar ativação/configuração. A soma cobre callbacks instrumentados; termina no footer e não representa todo o custo PHP nem LCP.

**Aceite não atingido.** system/probe no Site-Teste, três amostras, menor generation_ms, bypass PHP comprovado. O Pipedrive foi desligado junto com o Core pela dependência e ambos reativados ao fim; demais plugins preservados:

| Rota | Core 1.63.0 + Pipedrive | Sem Core/Pipedrive | Diferença | Limite |
| --- | ---: | ---: | ---: | ---: |
| / | 870,749 ms | 408,140 ms | 462,609 ms | 100 ms |
| /wp-login.php | 484,936 ms | 337,358 ms | 147,578 ms | 100 ms |

A rodada anterior à instalação, com 1.62.0, marcou mínimos de 951,790 ms e 674,624 ms. São observações do mesmo protocolo em momentos diferentes, sujeitas à carga do servidor; não isolam causalmente cada mudança. O perfil próprio da página 1.63 registrou aproximadamente 200–216 ms e 219 arquivos do Core; login 88–93 ms e 172 arquivos. O laboratório Core sozinho demonstrou bootstrap mínimo de 7 arquivos. A pilha com MCP confirma a solicitação global do catálogo. Não declaramos que catálogos/schemas deixaram completamente de carregar na página pública do conjunto atual.

### 355 — retomada do robots.txt

Ativação existente e troca de versão agendam a retomada; a primeira passagem retoma e verifica HTTP. Estado e saúde registram suspensão, retomada, versão e confirmação. Falha reserva um aviso técnico por ciclo, com resultado da tentativa, sem repetir o efeito a cada leitura. Geração desligada e arquivos de terceiros conservam suas guardas.

Bancada nativa: ativação antecipa o job já agendado, primeira verificação confirma a entrega, falha HTTP permanece não verificada, gera apenas um aviso e respeita geração desligada. No Site-Teste, após desativação/reativação reais, o gerador voltou automaticamente, sem alternar a configuração. Estado: suspenso=false, retomada_versao=1.63.0; marcos de suspensão/retomada e prova HTTP guardados em evidence/1630/site-robots-health.json. Configuração permaneceu na revisão `5527872cb986f45a5e95b62cde4f9856677a75657d9eb22b5467510c080397f5`; verificação `verified`, código robots_http_confirmado. /robots.txt respondeu 200 com marcador do Core e hash igual ao esperado. A contagem exata de passagens reais do cron não foi instrumentada; a prova de primeira passagem é nativa e isolada.

### 356 — correspondência manual Meta

Booleano f3base_meta_correspondencia, padrão true, com simulação e escrita pelo contrato administrativo/CAS. Contato de formulário aceito, classificado, com publicidade permitida e fora de teste/editor/automação recebe somente hashes normalizados em conversao.meta_correspondencia. E-mail trim/minúsculas; telefone com país e somente dígitos antes de SHA-256. Identidade inválida é omitida. Formulário aceito ainda pendente de classificação não libera conversão nem hashes.

Escolha documentada: novo fbq('init', pixel, {em,ph}) imediatamente antes de Lead, mantendo eventID. Sem identidade válida, Lead segue o caminho anterior. Os hashes não entram no HTML, localStorage/sessionStorage nem no evento próprio de medição. Correspondência automática permanece desativada. Provas nativas e DOM verificam exclusões, normalização, opção desligada, simulação, ordem e deduplicação. Não foi comprovado recebimento pela Meta. A consulta web às páginas do fornecedor não retornou conteúdo nesta sessão; não é apresentada como validação da documentação atual da Meta.

## Instalação, prontidão e testes

Instalador final: 811 arquivos, **575 PHP com lint aprovado**. WordPress nativo local 7.1.3 e mínimo 7.1.2, PHP 8.3.6, MySQL 8.0.46: instalação limpa, atualização direta 1.62.0, repetição e remoção/reativação em ambientes descartáveis. Dados, configurações, segredos sintéticos, procedência e registros pendentes/incertos preservados. Os quatro ciclos referenciam o mesmo SHA-256 final. O atraso de finalização foi acelerado apenas no estado descartável; cada etapa usa outra requisição PHP.

| Prova no Site-Teste isolado, WP 7.1.4 / PHP 8.3.36 | Resultado |
| --- | --- |
| Elegibilidade leve dos módulos | 44 assertivas |
| Pedidos 353/355/356 e perfil/permissão | 35 assertivas |
| Regressão 348/350/351 | 37 assertivas |
| Campanhas 349 com Meta 0.17 | 38 assertivas |
| Regressão 343/344/346 | 20 assertivas |
| Regressão 337/340/342 | 85 assertivas |
| Regressão 340/341 | 17 assertivas |
| Permissões pelo canal MCP | 16 assertivas |
| Documentação integral pela habilidade pública | 2001 assertivas booleanas; 165 documentos, 771 páginas |
| Convivência | Cinco acompanhantes ativos nas versões da tabela |

Além disso: 13 assertivas locais de login/contexto mínimo e recuperação do catálogo; quatro de falha/aviso/gerador desligado; duas da pilha de inicialização MCP; 76 DOM já descritas. Contagens de documentos/páginas não foram somadas como assertivas. Evidências anteriores e tentativas exploratórias presentes no fonte são históricas; somente resultados explicitamente citados pertencem ao aceite desta rodada.

Site-Teste recebeu o ZIP exato via plugins/upload-base64, operação `917cbf741c941b44d66a6e24208e78fd`, backup `9217d54198a42498e9f802bd`. Troca 1.62.0 → 1.63.0, ativa, confirmada em requisição independente. O recibo de instalação usa reativação silenciosa; o ciclo funcional foi conferido depois. Instalação concluída e confirmada no executor, provas automáticas pós-atualização concluídas, recuperação core_operacional. Manifesto dos 811 arquivos remotos idêntico ao runtime/instalador, SHA-256 do mapa ordenado `6b3302bb499d82228b622739e871f30b0511c1bc94248af315ac9f0b225f951a`.

Telas administrativas renderizadas sem erros, configurações observadas preservadas, 189 habilidades do Core. Índice e novos documentos lidos também pelo MCP externo, integrais e com hashes conferidos. Sondagens finais de home/login/REST/robots passaram. Sonda é interna de mesma origem; não prova cache externo universal. GA4 permanece desligado/sem concessão, WhatsApp e Instagram não foram habilitados.

Limpeza: 101 tabelas exclusivas removidas, zero restantes; diretório e manifesto da bancada removidos; controlador excluído com backup obrigatório, habilidade temporária ausente; ZIP de transferência removido. Nenhuma bancada entrou no instalador. Testes de fornecedores usaram dados sintéticos e transportes interceptados, sem mensagens ou eventos comerciais reais de teste. O site compartilhado manteve suas próprias rotinas e configurações existentes.

## Banco e reversão

Sem tabela/coluna nova. Campos aditivos no estado IMAP e robots, duas extensões da política de avisos e um booleano de correspondência. Contrato administrativo 8.28.0 aditivo, sem mudança dos SDKs acompanhantes. Slug, pasta, arquivo principal, identidades, mínimos e licenças preservados.

Reverter apenas o código ao instalador canônico 1.62.0 restaura o comportamento anterior, inclusive atraso de medição/avisos e limitação da retomada; não restaurar banco para desfazer este incremento. Dados e campos aditivos permanecem. Não repetir operações comerciais para provar uma atualização.

## Pendências e responsáveis

- **Core + MCP:** pedido 354 aberto. Reduzir o custo próprio restante e coordenar a descoberta administrativa sob demanda do MCP conforme o impacto individual. Repetir o critério de 100 ms antes de encerrar.
- **Frota:** aceite 352 em korvena/mvp, PageView Meta mediano abaixo de 1000 ms, relógio próprio desde a navegação, classificação antes do LCP em página quente e observação de sete dias. Não medido nesta rodada.
- **Frota/Meta, com autorização do ativo:** aceite 356 com requisição real contendo hashes e observação de e-mail/telefone no Gerenciador de Eventos por sete dias. A marca técnica f3base_teste continua suprimindo Meta; contato sintético de homologação comercial requer o fluxo autorizado da frota.
- **Dono/frota:** decidir publicação e implantação dos artefatos fora do Site-Teste. Nenhuma publicação externa foi feita nesta tarefa.

## Credenciais

Nenhum segredo novo solicitado ou incluído. Credenciais e concessões permanecem nos produtores. Senhas de aplicação/usuários sintéticos usados na documentação ficaram exclusivamente nas bancadas e foram removidos. Relatório e evidências não contêm valores secretos. Configurações comerciais existentes não foram trocadas para satisfazer testes.

## Arquivos finais

| Arquivo | Bytes | SHA-256 |
| --- | ---: | --- |
| base-site-core-fator3-1.63.0-instalador.zip | 2986868 | afd99c56edc9445f7498e010d3123d8497fd0dd335b3cc283b5156c7de855c5b |
| base-site-core-fator3-1.63.0-fonte.zip | 6154936 | 85d71ef5885e6a6a0fb6abb381d3edfc250d067f8b9d584ec557aab019479d7f |

Relatório externo: base-site-core-fator3-1.63.0-relatorio.md. Encaminhamento adicional: base-site-core-fator3-1.63.0-impacto-wp-mcp-fator3.md. Fonte com código, geradores, locks, testes, insumos/manifestos e evidências sanitizadas; acompanhantes são fornecidos separadamente. Nenhum ZIP contém outro ZIP da entrega. A cópia interna do relatório antecede o fechamento do fonte; a identidade final do fonte consta somente no relatório externo para evitar circularidade.
