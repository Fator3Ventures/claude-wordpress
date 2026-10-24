# Entrega — Fator3 MCP 0.30.1

24/10/2026 00:30 -0300 · Revisão 1 · Pedido MCP 66 · Slug/basename `wp-mcp-fator3/wp-mcp-fator3.php`.

**Nova versão implementada e ativa no Site-Teste.** Entrega corrente: **0.30.1**. Converte JPEG/PNG em novo WebP, preserva a origem e fornece a revisão pública necessária ao fluxo. Foram aprovadas 295 verificações locais finais, além das conferências remotas descritas abaixo. Status do aceite completo do pedido: **com-pendencias**, por AWN sem conexão disponível e falta de WebP simulada somente nos laboratórios. Não houve distribuição à frota.

## 1. Bases e escopo

Base direta imutável **0.29.1**: instalador 873894 bytes, SHA-256 `1b627aec5c24dc88f52eaf6a0d34367437d7f9e7b599f9f07850567fd57610e6`; fonte 3945818 bytes, SHA-256 `99ea12645e25d75f2466feebc4ac146e776f33b398d74802f4f6a48327a4142a`. Considerado também seu relatório externo atualizado, revisão 2.

Pedido recebido: `Fator3 MCP(7).md`, um pedido aberto, 66. Instruções comuns/padrão revisão 5, recebidas no fonte Meta 0.9.0, prevaleceram sobre a cópia local anterior revisão 4. Plano e avaliação de impacto anteriores ao código em `docs/PLANO-0300.md`; entradas preservadas em `docs/entradas`. Nenhum ID de pedido foi criado e os documentos centrais não foram editados.

A minor 0.30.0 foi instalada durante a homologação. O teste remoto revelou que media/get não devolvia revision, apesar de o novo fluxo exigi-la. Essa lacuna foi corrigida em **0.30.1**, incrementando o patch e preservando os bytes do instalador 0.30.0. A matriz final foi reexecutada com 0.30.1. Não se apresenta a candidata intermediária como a entrega corrente.

## 2. Pacotes atualizados e impactos

| Pacote | Versão considerada | Verificação nesta rodada |
|---|---|---|
| Site Core | 1.51.0 | Laboratório integrado e Site-Teste; 463 arquivos locais idênticos ao instalador recebido |
| MCP Google | 0.19.0 | Integração, descoberta, fronteiras administrativas; 160 arquivos locais idênticos |
| MCP Meta | 0.9.0 | Integração, perfis e descoberta; 43 arquivos locais idênticos |
| MCP LinkedIn | 0.10.1 | Integração, fronteiras administrativas/auditoria; 62 arquivos locais idênticos |
| MCP Pipedrive | 0.1.0 | Seis habilidades e schemas preservados no Site-Teste; contrato Core registrado, autorização fechada |

O Pipedrive exige PHP 8.3.36 e não foi ativado no laboratório PHP 8.3.6. No Site-Teste, PHP 8.3.36/WP 7.1.3 atendem seu mínimo; pipedrive/status retornou `operacao_nao_autorizada`, `registro_cliente:registrado` e `chamada_externa:false`. O gate do Core foi conservado, sem conceder acesso nem testar a API comercial. As demais versões instaladas finais foram Core 1.51.0, Google 0.19.0, Meta 0.9.0, LinkedIn 0.10.1 e Pipedrive 0.1.0, todos ativos. DreamHost 1.0.0, WPSC 3.1.4 e Yoast 28.7 também foram preservados.

Comparação do catálogo remoto antes/depois: **726 → 727 habilidades**, somente `media/convert` adicionada; nenhuma removida, nenhuma alteração de provider, readonly ou hash de schema das habilidades anteriores. As versões de todos os acompanhantes permaneceram iguais. Isso demonstra preservação das interfaces examinadas, não homologação universal de operações/credenciais comerciais.

**Nenhuma adaptação obrigatória em outro plugin foi identificada.** Não foi emitido impacto apenas para comunicar versão ou encerramento. Os alertas anteriores MCP 0.29.1 → acompanhantes sobre repetição conservadora continuam atendidos: resultados incertos e applied ausente/null não autorizam reenvio. Os casos de pesquisa por todos os termos e nonce administrativo também permaneceram aprovados. As atualizações Meta/LinkedIn preservam seus validadores e concessões próprios; não se fecha por esta entrega nenhum aceite comercial desses mantenedores.

## 3. Implementação e correções

- `media/convert`: id, formato webp, qualidade opcional 1–100 e expected_revision obrigatória. JPEG/PNG reais, original anterior a eventual redução de imagem grande, editor WordPress → save, novo anexo image/webp, cópia exata de título/alt/legenda e derivados por MediaImages::generate.
- Coordenação: trava do post de origem e da árvore de uploads; autorização nativa upload_files/edit_post e política do canal; revisão obsoleta recusada antes da escrita; idempotência impede duplicação da mesma intenção.
- Resultado: novo id/revision, source_id/source_revision, arquivos com MIME/dimensões/bytes/SHA-256, source_file, savings_bytes e original_preserved. A economia compara o original da origem com o WebP convertido antes de eventuais reduções; pode ser negativa. full e converted_original podem representar o mesmo arquivo.
- Falta de WebP: media_webp_unsupported com applied/changed/persisted false antes de criar mídia. Falha posterior à inserção informa novo id e efeito parcial; interrupção durante inserção conserva applied null e pede reconciliação. Um editor que retorna extensão diferente não deixa arquivo silencioso com sucesso declarado. Auditoria/recibos técnicos normais podem existir em recusas.
- Correção 0.30.1: media/get fornece revision sob trava de leitura e comparação antes/depois. O teste público usa essa revisão, sem recorrer a função PHP interna para preencher a entrada.

Não se altera automaticamente conteúdo, imagem destacada ou ícone do site. O filtro de saída WebP existe apenas durante a conversão/geração e é removido em sucesso/erro; não muda configuração persistente. Qualidade opcional vale para o convertido, enquanto derivados usam os padrões nativos. PNG animado não tem preservação de animação prometida. Pré-imagem de mídia mantém o limite existente de 64 MiB do conjunto.

Diff de runtime contra 0.29.1: **1 arquivo adicionado, 6 alterados, 457 idênticos, nenhum removido**. Nova classe MediaConversion; registro e coordenação de mídia; versão, rótulo e guias compilados. MediaImages::generate e os demais domínios foram preservados. Guia instalado inclui RELEASE-0300 e RELEASE-0301.

## 4. Testes e Site-Teste

| Matriz final 0.30.1 | Ambiente | Verificações aprovadas |
|---|---|---:|
| Instalação limpa, leitura em processo novo, mídia e fluxo MCP público | WP 7.1.2 / PHP 8.3.6 / MySQL 8.0.46, MCP isolado | 77 |
| Ativação conjunta e atualização direta 0.29.1 → 0.30.1 | WP 7.1.3 / PHP 8.3.6 / MySQL 8.0.46, quatro acompanhantes | 27 |
| Mídia e sequência pública ler → converter → reler → desfazer | Mesmo integrado | 64 |
| Descoberta/equivalência, pesquisa, idempotência, admin e casos adversos | Mesmo integrado | 96 |
| Documentação completa por MCP HTTP, conflitos e confinamento | Mesmo integrado | 31 |
| **Total final local** | **Sem falhas; contagens não representam casos únicos entre ambientes** | **295** |

A suíte de mídia tem 55 verificações por ambiente, incluindo regressões anteriores, PNG transparente, JPEG, original grande, revisão, perfis, travas, ausência de editor, falhas de save/geração, saída inesperada, exceção na inserção e desfazimento. O fluxo público agrega nove verificações por ambiente. Credenciais, perfis/grants, recibos, confirmações SQL pendentes, backups e configurações false/vazias foram conservados no upgrade; refresh token continuou utilizável, sem renovação artificial de validade. Preimagem do plugin foi verificada em prévia de rollback.

Lint: **453 PHP aprovados em PHP 8.3.6**. Instalador: **464 arquivos**, CRC/inventário e igualdade de cada arquivo instalado provados no laboratório. Os 728 arquivos dos quatro acompanhantes no laboratório permaneceram exatos, sem extras. Três avisos do atualizador WordPress foram causados pelo bloqueio deliberado de HTTP externo; nenhum aviso/erro PHP próprio ou dos acompanhantes foi observado. E-mail e HTTP de fornecedores foram bloqueados nos laboratórios. As provas antigas/intermediárias não foram somadas ao total final.

Site-Teste: https://fator3-teste-mcp-1.dreamhosters.com/ · WP 7.1.3 / PHP 8.3.36. Duas trocas com hash/slug conferidos:

| Troca | Operação do canal | Backup de arquivos |
|---|---|---|
| 0.29.1 → 0.30.0 | `1f8dbd65fb15d60a1b2cb4ff` | `022abbac7cf5ce3812bd63d0` |
| 0.30.0 → 0.30.1 | `ce0ed495c6710e178b839a14` | `9ddd39005e8e3f00374b6978` |

Ambas retornaram applied=true, active_after=true e sondas `/` e `/wp-json/` HTTP 200 antes/depois, com desvio de cache confirmado. São sondas internas de mesma origem, não prova externa independente. A reativação remota foi silenciosa em novo PHP; o ciclo completo de ativação foi testado separadamente na instalação limpa.

| Conversão remota temporária | Origem → novo ID | Original | WebP convertido | Economia |
|---|---|---:|---:|---:|
| JPEG | 121 → 123 | 14987 bytes | 2268 bytes | 12719 bytes |
| PNG | 122 → 124 | 3284 bytes | 2510 bytes | 774 bytes |

Doze arquivos (originais, seus derivados e os novos WebP) foram relidos por files/stat e coincidem em bytes/hash. Revisões, título, alt e legenda foram conferidos por media/get; os originais ficaram idênticos. Repetição com a mesma chave devolveu id 123 sem duplicar. O desfazimento por media/delete dos novos anexos preservou ambos os originais; depois os quatro anexos sintéticos e quatro arquivos temporários desta rodada foram removidos. Backups e auditoria normais foram mantidos. Nenhum MU-plugin ou rota PHP de teste foi criado no Site-Teste.

Documentação remota: **28 documentos, 30 páginas, 207184 bytes**, lidos integralmente com revisão/hash fixados; conteúdo UTF-8 e SHA-256 iguais ao pacote. Saúde final, após limpeza: healthy=true, **11 verificações aprovadas**. Evidências sanitizadas em `evidencias/0301/` no fonte.

## 5. Dados e reversão

Sem nova tabela, coluna, opção ou concessão. A conversão cria um anexo e seus metadados/arquivos, mais os registros normais de backup/auditoria. A origem é conferida em revisão e em todos os arquivos conhecidos. Hooks externos não oferecem transação global; divergência ou interrupção é explícita, sem promessa de rollback automático.

Para desfazer uma conversão: restaurar antes eventuais referências de página; usar media/delete do novo id, force=true, prévia, confirm_token e revisão atual. Não excluir a origem. Retornar os arquivos do plugin à 0.29.1 exige o primeiro backup acima ou seu instalador verificado; o segundo backup retorna somente à 0.30.0. Rollback de plugin não apaga os anexos nem reverte banco/efeitos externos. Não desinstalar nem limpar opções para voltar. A reversão remota do plugin não foi aplicada; a reversão das mídias sintéticas foi exercitada.

## 6. Aceites ainda pendentes

1. **AWN / frota e dono:** não há conexão específica de awnventures.com.br disponível nesta sessão. A busca de integrações retornou apenas WordPress.com, que não comprova acesso a esse site. Não foram convertidos o anexo 14 nem alterada a página 28. Após disponibilizar acesso autorizado e instalar a entrega: reler anexo 14/página 28, converter com revisão atual, substituir somente seu core/image por content/patch-page com expected_revision, verificar a página/LCP e registrar A-WEBP-2110/pendência 34. Desfazer restaurando o bloco do anexo 14 e, se sem referências, excluir o novo WebP.
2. **Cenário sem suporte no Site-Teste / responsável pelo ambiente:** media_webp_unsupported foi provado nos dois laboratórios nativos, sem criar arquivo/anexo. O servidor compartilhado possui suporte WebP; esse cenário não foi simulado ali. Não se afirma cumprimento integral desse item do aceite remoto.
3. **Revisor central:** aceitar/encerrar o Pedido MCP 66 apenas após os aceites aplicáveis. A aba central permanece intacta. Distribuição da frota e publicação no repositório não foram feitas.

Não há defeito conhecido aberto nos cenários exercitados. Essa afirmação não substitui os aceites pendentes nem a homologação comercial dos acompanhantes.

## 7. Uso e configuração

Nenhuma credencial nova é necessária. O servidor precisa de editor WordPress capaz de salvar WebP; o chamador precisa das capacidades nativas e perfil autorizado. Perfil Conteúdo conserva a política existente de mídia; Personalizado exige concessão explícita de media/convert; Leitura não converte.

Sequência: media/get do id de origem → guardar revision → media/convert com id, formato webp, expected_revision e idempotency_key da intenção → media/get do novo id. O retorno revision é do novo anexo; source_revision é da origem. Não preencher revisão inventada. Erro de conflito exige releitura; efeito incerto exige reconciliação antes de outra chave. Guias: system/guide document=release-0301 e release-0300.

## 8. Identidade dos artefatos

| Artefato final | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-fator3-0.30.1-instalador.zip | 879690 | `4dbe9ea5e3c9c2bc6ef5aaa574800e482226f0f1406e87a4fd818c68aa7260da` |
| wp-mcp-fator3-0.30.1-fonte.zip | 4209674 | `81478d432f54e63979f28234388f7cccb6e7fb6d281f5c3d6999258bd0208ecc` |

Relatório externo: wp-mcp-fator3-0.30.1-relatorio.md. A cópia interna precede o fechamento do fonte e não contém o hash do próprio ZIP. Instalador com raiz única wp-mcp-fator3/; fonte com raiz única wp-mcp-fator3-0.30.1-fonte/. Sem ZIP aninhado, credenciais reais ou banco de laboratório. Somente o instalador é instalável.

Referência intermediária preservada, não corrente: instalador 0.30.0, 879170 bytes / `b753dd37c2b30542c39064966911b33aacb31466e7e4b0c240821ff67ac052c1`.

Manifesto dos pacotes recebidos (nomes locais dos anexos):

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| base-site-core-fator3-1.51.0-instalador(1).zip | 2270123 | `7d6c9b8391e8f3a83a85dacbabea56cf93da6f6b04e7e195fcdceb4774f9f192` |
| base-site-core-fator3-1.51.0-fonte(1).zip | 5022652 | `285317445bf2e4861952815479a6a90bff76889ee53f7cee84014ae0df4d73a8` |
| wp-mcp-google-fator3-0.19.0-instalador(6).zip | 809436 | `d15868915e3fdf886d7e883a82d9d302df7242808fc94d45bf3e1857234759d1` |
| wp-mcp-google-fator3-0.19.0-fonte(6).zip | 4462572 | `0d90b1a0dbc186a9e0b2adf66843dad4abd928fb2c616a56442213597b0eefb2` |
| wp-mcp-meta-fator3-0.9.0-instalador(3).zip | 173724 | `e26aede1591426e06b8a69b5ad405cf13cb70c28d41b607346188c9d21a15662` |
| wp-mcp-meta-fator3-0.9.0-fonte(3).zip | 1218318 | `2c80d2e290c2ef453c1d92d9b7cea6f5f0bf77a8585bc46cd77f7ba0f4023e65` |
| wp-mcp-linkedin-fator3-0.10.1-instalador(3).zip | 254066 | `6182ea63bff6788f5d2637467e7ab29d58568e37283d6ece82d3e58ee41c13bc` |
| wp-mcp-linkedin-fator3-0.10.1-fonte(3).zip | 1207818 | `518b83da12940f044edd99e4223348f4ef01011dc57c7c40181793c473b6d0cc` |
| wp-mcp-pipedrive-fator3-0.1.0-instalador(2).zip | 42095 | `3366d83ca8908e407a0736812d30b8fa1506a8c1458a28cfb47eda6fd8f3c54f` |
| wp-mcp-pipedrive-fator3-0.1.0-fonte(2).zip | 159941 | `bb06315b60a5b0a36c0458d9dcb000505e52b5f444278a3effb26414186a3f2c` |
