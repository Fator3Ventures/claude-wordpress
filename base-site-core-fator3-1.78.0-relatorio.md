# Fator3 Site Core 1.78.0

Revisão 1 · Implementação e homologação · 2026-11-10T14:54:24-03:00 · Contrato administrativo 8.38.0.

**apta-no-escopo-testado.** O Core atende autoria WebPage, C6 e C7 do impacto consolidado do Fator3 Implantador 2.20.0. O instalador final está ativo no Site-Teste. Há um encaminhamento adicional para a autoria de páginas externas no filtro do tema distribuído pelo Implantador.

## 1. Base e escopo

Slug base-site-core-fator3, basename base-site-core-fator3/base-site-core-fator3.php. Base direta 1.77.0. O instalador de origem tem 4.390.364 bytes e SHA-256 428b7dbfb2c8c0b9a072559c9295a49bec4a7619fbb490eead97aeee60ffb1f5. O fonte de origem tem SHA-256 4c8c167b2a668c68b9074ffbded56fd01ee340f19be813c2712cb72df4a2fbdd. Os pedidos anteriores 386–388 entraram na suíte de regressão. A numeração dos pedidos novos segue o relatório de entrada.

Lidos integralmente instrucoes-agentes-plugins-fator3.md e padrao-desenvolvimento-plugins-fator3.md, ambos revisão 5 de 02/11/2026. PHP mínimo 8.3 de 64 bits, WordPress mínimo 7.1.4, site único. Cabeçalho, documentação e laboratório conferidos.

## 2. Conjunto de pacotes

| Componente | Referência examinada | Fronteira exercitada |
| --- | --- | --- |
| Core | 1.77.0 → 1.78.0 | Instalação limpa, migração, funções próprias e administração |
| MCP | 0.43.0 | Installer com conferência de hash, arquivos, leitura da documentação, operação e sondas do Site-Teste |
| Implantador | 2.20.0 | Fonte e instalador do anexo, impacto rev. 3 e módulo real de autoria do tema em WordPress isolado |
| Yoast / PublishPress Authors / WP Super Cache | 28.8 / 4.18.0 / 3.1.5 | HTML com e sem PublishPress, reescrita editorial, cópia anônima e recibo do worker |
| Google / Meta / LinkedIn / Pipedrive | 0.31.0 / 0.21.0 / 0.19.0 / 0.8.0 | Versões instaladas conferidas no Site-Teste. Nenhuma mudança de contrato dessas integrações neste ciclo |

O MCP 0.43.0 traz uma correção de ajuda e preserva as interfaces utilizadas. O diretório evidence/1780 contém as identidades dos pacotes e os recibos. O Implantador completo não estava instalado no Site-Teste. Seu código de tema foi avaliado em ambiente isolado.

## 3. Pedidos e impactos

| Entrada | Alteração no Core | Critério observado |
| --- | --- | --- |
| Autoria, impactos 2.19.0 rev. 2 e 2.20.0 rev. 3 | Aplica a política vigente ao WebPage identificado pelo próprio @id/url e ao artigo. Considera a política efetiva na chave do cache. A limpeza de Person respeita referências e equipe. | HTTP 200, conteúdo esperado e login técnico ausente no HTML e JSON-LD. Com perfil editorial aprovado, artigo e página creditam a editora. Sem PublishPress, ambos creditam a organização. A função do Core preservou o WebPage externo e a pessoa legítima. |
| C6, impacto 2.20.0 rev. 3 | Corrige a expressão para a barra invertida e rejeita resultado de validação inconclusivo. Examina caminhos antes da consulta ao permalink. | Caminho canônico aceito. Dez casos recusados, incluindo query, fragmento, travessia, ponto, barra codificada e rota técnica. A seleção foi executada com warnings convertidos em exceções. O worker retornou HTTP 200, copia_gerada e comprovação pelo hash da cópia WPSC. |
| C7, impacto 2.20.0 rev. 3 | Com bloquear_listagem ligado, gera regra Apache específica para o caminho real do diretório upgrade e acrescenta o GET exato ao recibo do servidor. | No Site-Teste, 200 vazio antes e 404 depois, com e sem barra final. Controle de arquivo 200. Em Apache isolado, o prefixo personalizado, o arquivo interno, o subdiretório, o nome vizinho e a preferência desligada tiveram o resultado previsto. |

Encaminhamento aberto, classificação acao-necessaria, sem ticket. **base-site-core-fator3-1.78.0-impacto-implantador-base.md** descreve o filtro posterior que altera o crédito de um WebPage externo quando há perfil editorial aprovado. O fonte inclui o patch exercitado na cópia do destinatário. Essa pendência pertence ao tema do Implantador. MCP e conectores de fornecedores não requerem mudança de código para estes pedidos.

## 4. Instalação e provas

1. WordPress 7.1.4, PHP 8.3.6 e MySQL 8.0.46 em dois bancos descartáveis. Foram executadas 47 verificações do ciclo e 98 de regressão em cada fase, além das verificações de instalação, atualização e reativação. Na migração direta, 993 amostras sintéticas e o hash da configuração de contato foram preservados. A reativação recompôs as 33 tabelas operacionais removidas pela desinstalação deliberada do laboratório.
2. Apache 2.4.58 com PHP, Yoast e WP Super Cache reais. O teste gerou visitas elegíveis e leu o resultado pelo próprio f3base/cache-reaquecimento-ler. Uma requisição da passagem final gerou e confirmou a cópia com orçamento de 20 por hora. A suíte de autoria usou o módulo oficial do tema e o instalador administrativo do PublishPress. A prova de grafo misto fez uma entrada sintética numa consulta WordPress singular.
3. PHP lint em 597 arquivos. Os 949 arquivos do instalador coincidem em SHA-256 com o runtime do fonte e as duas instalações locais testadas. Nenhuma mudança nos bytes de assets públicos. As verificações administrativas recusaram escrita, leitura de estado e leitura de ajuda em contexto anônimo.
4. Site-Teste, WordPress 7.1.4/PHP 8.3.36. O MCP recebeu o ZIP em partes, verificou o SHA-256 e instalou localmente por plugins/upload-base64 com expected_slug, expected_sha256, overwrite e activate. Os controles da home e da REST retornaram 200 em requisições novas antes e depois. O executor concluiu a atualização. O ZIP temporário deixou de existir no diretório de estágio.
5. Aplicada a revisão corrente de f3base/servidor-aplicar. A primeira passagem já confirmou a listagem e o HTTP 404, enquanto a publicação de llms.txt ainda estava pendente. A reverificação registrou status geral verificado, llms verificado, controle HTTP 200 e upgrade_http 404. A sonda MCP e um GET externo independente confirmaram 404 na URL pública.
6. O índice MCP anunciou 203 arquivos. docs/AGENTES-1.78.0.md e docs/RELEASE-1.78.0.md foram lidos por inteiro e seus hashes conferiram com o instalador. No site compartilhado também foram comparados o cabeçalho e os quatro arquivos PHP funcionais alterados, por hash. A prova completa de todos os arquivos ocorreu no laboratório.

## 5. Configuração, dados e recuperação

Nenhuma migração nova de schema, credencial, capability, fila ou tabela. A regra de servidor só é escrita pelo fluxo de aplicação existente, com comparação de revisão e backup do bloco. O operador de cada site com a preferência ligada deve reaplicar o bloco gerenciado e conferir status e upgrade_http. Uma instalação com prefixo personalizado usa o caminho público de content_url. Em Nginx, a configuração equivalente depende da hospedagem. Para o reaproveitamento de HTML, invalidar os caches e confirmar o artigo como visitante. Manter backups dos dados de cada site pelo fluxo habitual. Correções depois de instalada esta versão seguem por nova release.

## 6. Pendências e responsáveis

O mantenedor do Implantador deve incorporar e homologar a proteção de páginas alheias na ponte editorial e distribuir o tema atualizado. A equipe da frota é responsável por conferir o SHA-256 do arquivo publicado e repetir as provas nas instalações que receberão o pacote. Homologação desta rodada limitada ao Site-Teste e ao laboratório. A base histórica 1.77.0 já registrava acompanhamento de CLS em tráfego de produção para o pedido 388. Esse indicador permanece fora do aceite dos três pedidos desta rodada.

## 7. Credenciais e acesso

Os três pedidos não exigem credenciais adicionais. A aplicação do servidor, os documentos e o estado do worker requerem manage_options no servidor. O acesso remoto do Site-Teste ocorreu pelo MCP autorizado. Os arquivos de evidência não contêm cookies, segredos nem dados de visitantes reais da homologação.

## 8. Identidade dos arquivos

| Arquivo | Bytes | SHA-256 |
| --- | ---: | --- |
| base-site-core-fator3-1.78.0-instalador.zip | 4393299 | 503a07a6fc1106d1582596c96f10fa9c558fb92cea968782efe26f923b2ccce6 |
| base-site-core-fator3-1.78.0-fonte.zip | 23387922 | 37aade0938d38e77274877aed9c86eb1d964032bd2e51cd0e3af932cecb9869c |

O relatório dentro do fonte antecede o fechamento. O arquivo externo contém a identidade final dos dois ZIPs. Checklist de encerramento conferido contra a revisão 5 do padrão.
