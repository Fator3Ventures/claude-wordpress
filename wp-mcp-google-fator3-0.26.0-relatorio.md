# Entrega — Fator3 MCP Google 0.26.0

Revisão 1 · 01/11/2026, America/Sao_Paulo · implementação do Pedido MCP Google 48
Slug/basename: wp-mcp-google-fator3/wp-mcp-google-fator3.php
Status: apta-no-escopo-testado; aceite de produção e homologações anteriores permanecem pendentes.

**0.26.0 implementada e ativa no Site-Teste.** Corrige core_transport/core_unsupported quando o Core publica transporte ambos, inclusive para LinkedIn indisponível. Não houve alteração de código Core ou de outro acompanhante. O instalador final passou em 552 verificações nativas e sete verificações específicas no Site-Teste, sem falhas.

## 1. Bases aceitas

Instalação WordPress limpa e atualização direta de **Google 0.25.1**, sem intermediária ou desinstalação. Base recuperada e conferida: instalador 895748 bytes, SHA-256 bdd860d479e9813246f8fd2828728ff0cc0c969c2b1e85ddb28a7c9a041d6b30; fonte 7043091 bytes, SHA-256 9b496df1ceb3786439db79bc1e7dac29ccf78bf31e9d99468011f2cc51502429. Relatório da base lido; resultados históricos não são contados como novas execuções.

Lidos o pedido Google de 01/11/2026, os relatórios Core 1.66.0 e Meta 0.18.0 e as instruções fornecidas. Normas r5 herdadas da base preservam a regra de registrar respostas/encerramentos no relatório principal. Identidades das entradas em reproducao/entradas026/inputs.json; plano anterior à implementação em reproducao/PLANO-026.md. A lista central de pedidos não foi editada.

Requisitos próprios comprovados nesta rodada: WordPress 7.1.2 e 7.1.4, PHP 8.3.6 de 64 bits e MySQL 8.0.46, em laboratórios isolados. Requisitos do cabeçalho preservados. Nenhuma atualização de dependência de produção foi necessária.

## 2. Convivência e encaminhamentos

| Pacote | SHA-256 do instalador usado | Evidência própria |
| --- | --- | --- |
| Core 1.66.0 | 0f796b2001478fe32e5ce47b5851f79148e6a1eebac7087c39a603a587692830 | 909 arquivos do fonte iguais ao instalador; produtor nativo, contexto de medição, transportes e inventário exato na bancada. |
| MCP 0.38.0 | bc550c6573527a0d71bfa560036f83e7c8aec546f49d70b8e0095da5d303c1a5 | Execução administrativa, schema, documentação paginada, upload, guarda de rollback, reversão e reaplicação autenticados. |
| Meta 0.18.0 | 5aef6b8fe85e69478285a84ed5d12c623d7834108928c911ca0e54aaf46d95f8 | 65 arquivos do fonte iguais ao instalador; ativação, convivência e sentinelas preservadas. |
| LinkedIn 0.14.0 | 91b49ab4aaac5487657496d22d2d1e3a31334a4afa2547dd7946ebdf1d9868ef | Instalador original, ativação, adaptador de transporte e sentinelas preservadas. |
| Pipedrive 0.5.0 | Não usado como entrada local | Presença/ativação e versão remotas conservadas. Não ativado no PHP 8.3.6 por exigir 8.3.36. |

**Encerramento do impacto anterior:** wp-mcp-google-fator3-0.25.1-impacto-core.md, Pedido Core 363. O relatório Core recebido informa incorporação da projeção de medição compatível e correção dos aliases sem src. Nesta rodada, o Core original 1.66.0 forneceu fotografia de medição válida, sem patch, e permitiu os ensaios GA4/Ads. A confirmação de prontidão nos sites de produção é informação da lista de pedidos recebida, não nova prova própria. A proposta histórica permanece no fonte apenas como histórico e não deve ser reaplicada.

O Pedido 48 é correção do consumidor Google para um contrato já publicado. Não exige adaptação, nova configuração ou versão Core. Meta 0.18.0 altera o diagnóstico de erros históricos de coleta; não foi identificada mudança exigida na fronteira Google. Nenhum novo impacto técnico ou pedido a outro mantenedor foi identificado no escopo examinado; não há arquivo de impacto desta rodada. Não se afirma homologação integral das funcionalidades dos acompanhantes.

## 3. Mudanças por pedido e evidências

**Pedido MCP Google 48 — implementado, validado-localmente e validado-wordpress.** A cópia do schema site-conversion-purposes/1.1.0 em includes/Data/CoreTransport140.php foi sincronizada estruturalmente com docs/schemas/conversion-snapshot-1.1.json do Core 1.66.0. Dezesseis enums selected/effective, nos quatro destinos e duas finalidades, passam a aceitar navegador, servidor e ambos. O código invalid_output, também publicado pelo Core, é reconhecido no envelope de erro.

A validação integral permanece: produtor, contrato, tipos, propriedades adicionais, revisão e valores desconhecidos continuam verificados. Não se filtra o LinkedIn para ocultar erros. core_transport.ok=true significa fotografia válida; cada destino mantém seu próprio ready/reason. LinkedIn em ambos com ready=false/reason=regra_ausente não invalida GA4/Ads nem torna o LinkedIn pronto. Essa alteração não acrescenta escolhas de transporte à configuração, não muda tags, consentimento, filas, grants ou envio.

Reprodução na 0.25.1: o Core original publica fotografia válida com LinkedIn ambos, mas o Google devolve core_unsupported; navegador funciona como controle. Três verificações específicas locais mais duas de preparação aprovadas; a sonda remota reproduziu o mesmo contraste, com sete checks da base. Esses números não integram os 552 da candidata.

Na candidata, **151 verificações de transporte**: as oito configurações nativas possíveis de f3base_conversoes_transporte (GA4 navegador/servidor × Ads navegador/servidor × LinkedIn navegador/ambos), status pelo MCP com GA4/Ads prontos por provas sintéticas, motivo LinkedIn preservado, igualdade exata dos schemas, 72 pares selected/effective independentes nas duas finalidades/quatro destinos, recusa de valores desconhecidos e envelopes malformados, preservação de configuração, ausência de HTTP/mail e recusa de usuário não administrador. Os campos opcionais de material e Meta são cobertos por fixtures do contrato; não são escolhas extras oferecidas pela configuração nativa.

Runtime: mesmos 172 caminhos, 168 PHP. Somente três arquivos distribuídos mudam: schema CoreTransport140.php, documentação compilada e arquivo principal de versão. Diff com hashes em reproducao/diff-runtime026.json. Mantidos 300 abilities (115 leitura, 185 escrita), 42 opções, configuração 4.0.0 e execução/armazenamento/manutenção 2.0.0. A documentação corrente esclarece a base 0.25.1 e distingue trechos históricos.

## 4. Instalação, testes e prontidão

| Matriz final | Ambiente | Verificações | Falhas |
| --- | --- | ---: | ---: |
| Mínimo, Google isolado | WP 7.1.2/PHP 8.3.6/MySQL 8.0.46 | 24 | 0 |
| Instalação atual integrada | WP 7.1.4, Core 1.66.0/MCP 0.38.0/Meta 0.18.0/LinkedIn 0.14.0 originais | 355 | 0 |
| Upgrade 0.25.1 → 0.26.0, rollback e reaplicação | WP 7.1.4 e mesmos acompanhantes | 173 | 0 |
| **Execuções finais locais** | **WordPress real, fornecedores sintéticos** | **552** | **0** |

Os totais incluem 124 verificações documentais por cada um dos dois ambientes integrados; não são 552 requisitos exclusivos. A matriz atual inclui 57 verificações da política de avisos da 0.25.1, exercitadas novamente com Core 1.66.0 original. Atualização inclui 37 verificações, preservando prova, ciphertext, seleção, grants, acervo cifrado, agenda pausada, tarefa concluída, política de aviso e recibo aceito, conexão adicional, cron e registros dos acompanhantes. Reversão restaura a árvore exata 0.25.1; arquivo deliberadamente editado impede rollback; reaplicação restaura 0.26.0.

Lint dos 168 PHP, catálogos, geradores, documentação e inventários aprovados. Gate tools/release026.py vincula fonte/testes/ferramentas, SHA-256 do instalador e inventário final. Evidências próprias finais em evidence/026/closed-* e summary.json. Dez laboratórios exclusivos foram removidos depois da parada dos processos, sem tocar bancos compartilhados.

Ensaios preliminares ajustaram o harness que esperava WP_Error no erro administrativo já decorado como envelope pelo MCP; a nova asserção exige recusa e código do serviço. Também restauraram no guia as instruções de stream/descrições em português e corrigiram referências documentais antigas. Nenhuma candidata preliminar foi entregue ou instalada remotamente. A matriz completa acima usa o ZIP final identificado na seção 8. PHPUnit integral não foi executado nesta rodada; não se somam resultados unitários históricos.

**Site-Teste:** https://fator3-teste-mcp-1.dreamhosters.com/ . Somente Google atualizado, diretamente 0.25.1 → 0.26.0, por plugins/upload-base64 com expected_slug=wp-mcp-google-fator3, expected_sha256 da seção 8, overwrite/activate=true e sondas de 30 segundos. Operação 1d4c8f8d3ac2e80f7cf03683567e4603; pré-imagem 761c49e9dd02589801d693e3. Home e REST retornaram HTTP 200 antes/depois. Reativação silenciosa em PHP novo; o ciclo completo de instalação limpa é comprovado separadamente na bancada. Sem publicação raw ou implantação na frota.

**Aceite remoto do 48:** sete checks aprovados no pacote final. Sonda fixa, administrativa e restrita ao Site-Teste aplica filtros somente à requisição: LinkedIn ambos/regra_ausente; produtor, consumidor e status válidos; zero HTTP externo, zero correio; configuração preservada. Não há fixture persistida. A sonda foi removida com guarda SHA-256 e backup; files/stat confirmou ausência. O schema descoberto pelo MCP contém os 16 enums ambos e invalid_output.

As 42 opções Google conservaram os hashes na visão administrativa redigida da API; revisão da entrega igual. Não é uma comparação de segredos em texto puro. Armazenamento Google pronto. Destinos de envio continuam sem prontidão comercial nesse site sem credencial/configuração de entrega. Inventário final: Google 0.26.0, Core 1.66.0, MCP 0.38.0, Meta 0.18.0, LinkedIn 0.14.0 e Pipedrive 0.5.0 ativos; versões/ativação dos demais plugins preservadas. Prévia de rollback pronta, sem aplicar reversão no site compartilhado.

**Documentação instalada:** 24 documentos, 86 páginas e 4363272 bytes lidos integralmente por google/documentation, com expected_revision e offsets UTF-8. Cada página comparada ao SHA-256 dos bytes compilados; índice e versão coincidentes. Prova em evidence/026/remote/documentation.json. Leituras completas também exercitadas por MCP HTTP após instalação limpa e upgrade, incluindo confinamento, revisão obsoleta, canal desligado e autorização. HTTP 200/documentação não comprovam acesso ao Google ou entrega comercial.

## 5. Banco e volta de versão

Sem tabela, coluna, opção, formato persistido ou migração novos. Sem regravação de credenciais, troca de seleção, concessão automática, replay de evento ou nova política de aviso. A instalação mantém estado corrente; as mudanças funcionais limitam-se à validação de leitura.

Rollback: repor o instalador íntegro 0.25.1 ou a pré-imagem nativa indicada, com prévia atual e guardas de integridade. Preservar banco e salts; não desinstalar para atualizar. A base reintroduz core_unsupported com ambos e não entende invalid_output na mesma cópia de schema. Restaurar arquivos não desfaz efeitos externos ou alterações posteriores. O rollback local aplicado/reaplicado foi comprovado; remotamente executou-se somente prévia.

## 6. Pendências e responsáveis

- **Frota/operador de ctooffice.com.br:** instalar o ZIP identificado e confirmar core_transport.ok=true com LinkedIn ambos, preservando ready/reason de cada destino. A tentativa de consulta somente leitura a esse site foi rejeitada pela revisão automática porque a autorização desta rodada cobre Site-Teste. Não houve contorno ou alteração de produção. Para esse aceite é necessária autorização explícita para o site ou execução pela frota.
- **Frota/fornecedores:** a lista recebida mantém aceites de acervos Ads/GSC em ctooffice, chave real fora do padrão e pendências da 0.22.0 (pendência 20). Não encerrados por fixtures. O aceite recebido do Pedido 47 também não é contado como nova prova desta rodada.
- **Operação:** API real, caixa postal, horários reais de WP-Cron e navegador visual não homologados nesta rodada. Interface visual/JavaScript não alterados; testes cobrem status, autorização e renovação nativos. Sem conversões reais, gastos Ads ou e-mails a clientes.
- **Acompanhantes:** Pipedrive não ativado no piso por requisito PHP; não repetida a homologação comercial integral de Core, MCP, Meta ou LinkedIn. Provas próprias limitadas às fronteiras descritas. Nenhuma regressão foi observada nesse escopo; isso não certifica toda combinação de ambientes.
- **Dono/frota:** distribuição, publicação dos arquivos permitidos e fechamento da lista central. Não houve push, publicação de fonte ou mensagem a terceiros.

## 7. Credenciais e configuração do dono

Nenhuma credencial ou configuração nova necessária. Manter conexão Google, seleção do stream, segredos, concessões e transportes existentes. Para inspeção, usar google/readiness-status e google/conversion-delivery-status com autorização administrativa. O guia 0.26.0 descreve interpretação, atualização e rollback; avisos da renovação continuam na aba Conversões, com simulação/aplicação e padrão de seis horas.

Relatório, código e evidências novas não contêm tokens reais, cookies, senhas, contatos ou dumps de banco. Testes usam dados sintéticos e transporte interceptado. Segredos redigidos da API não são tratados como credenciais verificadas.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
| --- | --- | ---: | --- |
| Instalador | wp-mcp-google-fator3-0.26.0-instalador.zip | 896007 | f75031f2a430e099b7d3603d321993a049b4fb49606b9267144a59971eeebfe4 |
| Fonte | wp-mcp-google-fator3-0.26.0-fonte.zip | 7215381 | cf3ce94a99943e9ae562abc956d8db5a9e08bfa8ff3ef7968e93d8aa5b00b567 |

Somente o instalador é instalável, com raiz wp-mcp-google-fator3/. Fonte com raiz wp-mcp-google-fator3-0.26.0-fonte/, código completo, ferramentas, testes, docs, evidências sanitizadas e reprodução. Nenhum ZIP aninhado. A cópia interna é **cópia anterior ao fechamento do fonte**; tamanho e hash do próprio fonte são preenchidos somente no relatório externo wp-mcp-google-fator3-0.26.0-relatorio.md após o fechamento único. Conferência final executada: fonte fechado extraído em diretório independente; seu próprio build reconstruiu instalador byte a byte idêntico ao ZIP testado e entregue. O fonte não foi reaberto para inserir seu próprio hash. Este é o relatório externo final; a cópia interna permanece anterior ao fechamento.
