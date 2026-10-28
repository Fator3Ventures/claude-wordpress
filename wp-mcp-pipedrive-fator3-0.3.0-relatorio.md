# Entrega — Fator3 MCP Pipedrive 0.3.0

Revisão 1 · 28/10/2026, America/Sao_Paulo · Rodada: implementação e testes.
Slug/basename: `wp-mcp-pipedrive-fator3/wp-mcp-pipedrive-fator3.php`.
Status: **com-pendencias**. Implementado e instalado no Site-Teste; apto no escopo sintético e integrado testado. Aceite com a tela do Pipedrive real ainda pendente.

## 1. De onde esta versão entra

Instalação limpa e atualização direta **0.2.0 → 0.3.0**, sem intermediária. Base aceita: instalador 0.2.0, 48.865 bytes, SHA-256 `b7065e4780cbc2166605164e4a822338b76627bef48c5f05a9fb9c3505efbb4a`. Fonte-base: 186.893 bytes, SHA-256 `803617faeb4244d6bbf375d3fe11f4652973ee49432c92f5b505f9378f69e7ef`.

Pedido da rodada: `Fator3 MCP Pipedrive(2).md`, item **Pedidos MCP Pipedrive 3**, de 28/10/2026. Item 2 consta encerrado no documento recebido e sua retenção foi preservada. O anexo Google não orientou implementação, conforme escolha explícita pelo Pipedrive. Normas comuns revisão 5, de 23/10/2026, incorporadas à fonte; prevalecem sobre as cópias avulsas da revisão 4.

Pacotes novos examinados e com CRC/SHA-256 conferidos:

| Pacote | Artefato | Bytes | SHA-256 |
|---|---|---:|---|
| Core 1.57.1 | instalador | 2707842 | `ee1c0eb8f46b7640a69e6b4e71697d5fc43bc9cd77f147c6219de1a410c5af62` |
| Core 1.57.1 | fonte | 4145747 | `0600d83f31389055593645daf366465472c165b4a8ab2f85720da112e0b9aeb5` |
| LinkedIn 0.11.0 | instalador | 283053 | `34541afa67c0991e9dc0b5474ab8678dff8cf806eace6ceb1edb47983f9e0308` |
| LinkedIn 0.11.0 | fonte | 1490342 | `5048b99a73ed9ec2beed7545832b13d88d63dafe432100722f2989eb86ee493e` |

O manifesto `evidence/inputs.json` contém a identidade medida dos anexos, inclusive nomes com sufixos de upload. Os relatórios Core/LinkedIn e da base Pipedrive integram inputs/. Relato recebido sobre distribuição da 0.2.0 pela frota não foi usado como prova própria desta rodada.

Mínimos comprovados em WordPress real: **WordPress 7.1.3, PHP 8.3.36 de 64 bits, MySQL 8.0.41/InnoDB**. OpenSSL exigido pela base. Site único; multisite não suportado. O lint local usa PHP 8.3; não substitui o ensaio remoto do piso declarado.

## 2. Convivência e encaminhamentos

Combinação exercitada no laboratório integrado e inventariada no Site-Teste: Core **1.57.1**, MCP **0.33.0**, Google **0.20.0**, Meta **0.12.0**, LinkedIn **0.11.0**, Pipedrive **0.3.0**. Só o Pipedrive foi atualizado nesta rodada. Os outros pacotes já estavam nessas versões. Não há ordem de troca nova: detectar contrato Core `pipedrive-api-client/1.0.0` e autorização por site continua obrigatório.

**Impactos emitidos:** nenhum. Avaliados cliente Core, orçamento operacao, transporte/perfil/schema MCP, documentação e isolamento de retenção/tabelas. O Core permite os GET usados e continua dono do token/transporte; MCP já admite o provider e sua nova ability; LinkedIn não compartilha opções, tabelas nem rotas com esta funcionalidade. Nenhuma alteração de outro pacote foi necessária.

**Tratamento de impactos anteriores:** o encaminhamento histórico `wp-mcp-pipedrive-fator3-0.1.0-impacto-base-site-core-fator3.md` solicitou o cliente Core. A resposta/atendimento já registrado na base permanece compatível: o contrato publicado no Core 1.57.1 foi usado de fato em seis checks do novo relatório, além de oito checks de retenção/cliente. Responsáveis: mantenedor Core pelo contrato, mantenedor Pipedrive por seu consumo. Esta confirmação não reabre todos os aceites comerciais históricos e não produz nova edição do impacto. Não foi declarado concluído trabalho alheio com base apenas em mocks.

## 3. Mudanças por pedido e evidência

### Pedidos MCP Pipedrive 3 — relatório agregado

**Implementado; validado em WordPress; não homologado com fornecedor real.** Nova `pipedrive/relatorio`, nona operação pública. Mantidos slug, provider, namespaces, Text Domain, Update URI e capacidades anteriores.

- Uma chamada administrativa reúne internamente catálogo de campos, leads ativos, leads arquivados, negócios ativos v2 e negócios arquivados v2; GETs somente pelo Core e consumidor `operacao`.
- Leads agrupados simultaneamente por estado, Parceiro, Unidade, Canal, Campanha, Ponto de conversão e motivo de arquivamento. Os grupos permitem somar marginais e cruzar Parceiro com motivo.
- Negócios por IDs de funil/etapa, status e arquivamento; ganhos/perdas por motivo. Campo customizado opcional para motivo de ganho, pois não há motivo nativo documentado.
- Total visível de leads ativos mais negócios open/won/lost não arquivados/excluídos, independente do período, e comparação com `limite_plano` informado pelo chamador. Sem limite informado, comparação nula e pendência explícita; não foi inventado endpoint de plano nem usado orçamento de API como limite de registros.
- `completo`, `coleta_completa`, pendências, páginas por fonte e custo. Falhas, repetição de cursor, orçamento/tempo/tamanho, ausência de campos/datas e duplicatas produzem parcial explícito.
- Nenhum texto livre do fornecedor é emitido: opções por ID, funis/etapas por IDs, categorias livres por HMAC ou código numérico de dicionário de entrada. Não saem nomes, e-mails, telefones, títulos ou IDs de registros individuais. Dicionários e registros vivem apenas na requisição, sem cache/diário próprio. HMAC não equivale a anonimização estatística; contagens pequenas continuam administrativas.
- Novos GETs estreitos em `pipedrive/api-ler`: `/api/v2/deals` e `/api/v2/deals/archived`, somente limit/cursor. Não ampliadas escritas nem adicionada execução arbitrária.

**Semântica temporal:** padrão por criação (`add_time`) para leads e distribuição de negócios, com estado atual; ganhos/perdas por `won_time`/`lost_time`. Datas inclusivas no fuso IANA (padrão America/Sao_Paulo). `criterio_leads: arquivamento` usa archive_time nos arquivados e retorna parcial se ausente, nunca presumindo update_time. Não é snapshot histórico/transacional; registros reabertos não compõem histórico de ganhos/perdas passados. Comparação com a tela exige mesmos critérios, visibilidade e códigos.

**Limites operacionais:** páginas de 100; padrão de 100 chamadas, configurável até 120; duração cooperativa 45 s, até 120 s, mais eventual chamada em curso de até 20 s; até 12.000 registros, 200 grupos e 32.000 bytes de dimensões agregadas. Sem retomada/retry automáticos. Contas acima desses limites retornam parcial; não se promete coleta ilimitada em uma chamada.

**Custo:** Core 1.57.1 debita 20 unidades locais por GET enviado, inclusive falha HTTP. Não são tokens oficiais da API. Recusa anterior ao envio não soma custo; envio incerto fornece gasto nulo e intervalo mínimo/máximo. Prova com cliente Core original confirmou cobrança de 100 unidades para as cinco fontes e 20 para erro remoto interceptado, sem confundir variação de saldo global com custo exclusivo.

**Retenção herdada:** diario_dias 0 permanente por padrão, prazo finito explícito, recibos 180 dias e prévias 900 s. A nova leitura não chama cleanup nem grava configuração. Schema de banco permanece 1.

## 4. Instalação e prontidão

Site: <https://fator3-teste-mcp-1.dreamhosters.com/>. Instalação pelo conector **WP MCP fator3-teste**, `plugins/upload-base64`, com overwrite/activate verdadeiros, expected_slug e SHA-256 final conferidos. Pacote transmitido diretamente; não houve publicação raw, push ou distribuição pela frota.

- Resultado: **applied**, ativo antes/depois, versão observada **0.2.0 → 0.3.0**, nova requisição PHP.
- Operação: `d29faf687e8e68e690bb4ca7`; operação de pacote `7fe9ac732321ed77272148ae0ff40c16`; backup recuperável da árvore anterior `017d975b36cf5756efd25455`.
- Instalador: `30fc784a552a89351900c169fad7300759163fb886b842f45ba807bb0977f657`, 59.877 bytes. Seus 22 arquivos são idênticos à árvore fonte e ao runtime instalado, por SHA-256 de cada arquivo.
- Home e REST: HTTP 200 antes/depois e após limpeza. Saúde final: 11/11 checks locais aprovados. Isso não certifica conectividade comercial com Pipedrive.
- Tabelas próprias: zero linhas antes/depois; hashes iguais. Retenção configurada `diario_dias:0`, revisão/digest preservados. Option de autorização Core com digest inalterado; permaneceu `operacao_nao_autorizada`.
- Chamada real da nova ability pelo MCP recusou corretamente a ausência de autorização, sem habilitá-la. Testes funcionais da conta usaram cliente em memória/HTTP interceptado, nunca conta real.

| Prova | Aprovados | Escopo |
|---|---:|---|
| Regressão nativa | 77 | Operações, autorização, CAS concorrente, documentação e armazenamento |
| Relatório nativo | 49 | Paginação, fuso, contagens, período, orçamento/tempo, parciais e privacidade |
| Retenção | 33 | Prazo, confirmação, nonce, revisão e locks entre conexões |
| MCP integrado | 29 | Executor original, perfil de leitura, nova ability e nove documentos completos |
| Core original / retenção | 8 | Cliente real do pacote Core, transporte interceptado |
| Core original / relatório | 6 | Cinco endpoints, cobrança e erro parcial, transporte interceptado |
| Atualização direta | 9 | Dados/opções/diário preservados, documentação atual |
| Reinício/reativação | 2 | Escolha de retenção preservada |
| Relatório no Site-Teste compartilhado | 49 | Instalação final, fixture em memória, zero HTTP ao fornecedor |
| Verificação estática/build | 44 | 24 PHP lintados, schemas, ZIP, hashes e reprodução byte a byte |

**Total funcional: 262 checks aprovados** (213 em laboratório e 49 no compartilhado), além dos 44 checks estáticos. Os checks de saúde são separados dessa soma. Houve uma falha inicial do worker de concorrência por marcador 0200 herdado no teste; corrigido para 0300 e repetido em laboratório limpo, 77/77. O incidente e a prova final foram preservados. Não houve alteração do runtime para esconder a falha.

O candidato recebeu ajustes documentais antes do fechamento, sem mudar PHP funcional. O instalador final repetiu instalação limpa, relatório (49), integração MCP/documentação (29), atualização direta (9+2) e teste compartilhado (49). As regressões anteriores sobre os mesmos bytes PHP continuam identificadas como tais. `evidence/` separa cenários, tentativa inicial, identidade e instalação final.

Documentação MCP: `pipedrive/documentacao-ler`, nove IDs, leitura integral paginada e SHA-256. Laboratório: 29 páginas conferidas com o runtime final. Compartilhado: documento `uso` inteiro, 12.225 bytes, SHA-256 `02c5ae307b23a8ad0672318c10c7d07d6ca42312990bb94ccd413a21ab931a7e`, fim true. Ajuda funciona sem autorização comercial.

Exemplo (limite fictício, substituir por valor da conta):

```json
{"data_inicio":"2026-09-28","data_fim":"2026-10-27","limite_plano":1500}
```

Antes de usar números: conferir success, data.completo, coleta_completa, pendencias, fontes e custo. Leia `uso` para campos e dicionários de códigos.

**Limpeza final:** removidos os dois laboratórios privados, suas 93 e 14 tabelas isoladas, os controladores temporários, a fixture e o bundle QA. Nenhuma tabela compartilhada ou configuração alheia foi apagada. Backups normais de arquivos/troca permanecem sob a política do MCP. Inventário final mantém os seis plugins nas versões listadas acima.

## 5. Banco e reversão

Nenhuma migração, tabela, option, job ou credencial novos. A atualização de laboratório preservou byte a byte três operações sintéticas e duas linhas do diário de 400 dias, incluindo estado incerto, além da opção finita de 730 dias. Reinício e reativação preservaram a escolha. No compartilhado, as tabelas já estavam vazias e permaneceram assim; essa observação não substitui a prova com dados no laboratório.

A pré-imagem da instalação cobre arquivos do plugin, não rollback de banco ou chamadas externas. Voltar para 0.2.0 remove a nova leitura e mantém schema/retenção; backups do banco e salts continuam necessários para recuperação de recibos. A revisão Core inclui a versão do consumidor: prévias antigas podem exigir recriação após troca de versão; não repetir mutação incerta. Não se recomenda voltar à 0.1.0, que tinha expurgo antigo.

## 6. Pendências de validação e responsáveis

1. **Aceite do item 3 em korvena.com.br — pendente, dono/frota e responsável pelo Pipedrive:** executar período de 30 dias com token autorizado e visibilidade global, confirmar mapeamentos/limite/códigos e comparar Parceiro e motivo de arquivamento com a tela do Pipedrive. Não houve instalação nos sites-porta nem acesso à tela real nesta rodada. Os números de fixtures não são dados da conta.
2. **Autorização comercial no Site-Teste — mantida desligada:** dono/administrador do Core decide eventual habilitação em ambiente/conta apropriados. Não foi necessária para os testes sintéticos.
3. **Categorias reais e motivo de ganho — validar no aceite:** campos textuais saem em códigos; informar dicionário conhecido para comparação legível. Sem campo de motivo de ganho, a saída registra sem_campo; sem limite do plano informado, a comparação não fecha. Sem archive_time, critério de arquivamento fica parcial.
4. **Escala e consistência da conta — pendente fornecedor:** limites finitos, permissões de visibilidade e movimentos concorrentes podem produzir parcial ou divergência com fotografia da tela. Nesta versão não há snapshot/retomada de relatório. Responsável pelo aceite deve registrar os mesmos filtros e instante de leitura.

A revisão automática recusou uma consulta opcional de metadados em korvena.net.br por considerá-la fora do Site-Teste explicitamente autorizado e não necessária à implementação local. A recusa não foi contornada; foi adotada a alternativa de testes sintéticos no ambiente autorizado. Nenhum dado privado dessa conta foi obtido por essa tentativa.

## 7. Credenciais

Nenhuma credencial deve ser preenchida neste plugin. Token, domínio e identidade verificada continuam no Core. Uso comercial exige `f3base_pipedrive_operacao` ativo e consumidor `wp-mcp-pipedrive-fator3` autorizado, mais orçamento e saldo adequados. Operações e tela exigem manage_options; MCP também aplica perfil da conexão. Não há token/secret real nos ZIPs ou evidências. Credenciais sintéticas dos testes são exclusivas dos laboratórios removidos.

## 8. Identidade final dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador WordPress | `wp-mcp-pipedrive-fator3-0.3.0-instalador.zip` | 59877 | `30fc784a552a89351900c169fad7300759163fb886b842f45ba807bb0977f657` |
| Fonte completo | `wp-mcp-pipedrive-fator3-0.3.0-fonte.zip` | 178523 | `c5d053f8a63e3a63f79645811bb0c62495bb8b5f6975bc796527ff5bc861cf29` |
| Relatório canônico | `wp-mcp-pipedrive-fator3-0.3.0-relatorio.md` | medido no arquivo entregue | sem autorreferência |

Somente o instalador é instalável. Raiz fonte: `wp-mcp-pipedrive-fator3-0.3.0-fonte/`; raiz instalador: `wp-mcp-pipedrive-fator3/`. Nenhum ZIP contém ZIP da entrega. Fonte inclui plano anterior à implementação, código, docs, schemas, build reprodutível, testes, entradas e evidências sanitizadas. Não inclui banco, wp-config, salts ou ferramentas temporárias no runtime. Não há relatório de impacto novo porque não se identificou consequência dirigida a outro pacote.

A cópia dentro do fonte está marcada **cópia anterior ao fechamento do fonte**. O hash/tamanho finais acima foram preenchidos neste relatório externo depois de empacotar, sem reabrir o ZIP fonte. Identidade do instalador e evidências permanecem iguais nas duas cópias.

## 9. Referências técnicas consultadas

Documentação primária Pipedrive, consultada em 28/10/2026, além do código/contrato Core 1.57.1:

- [Leads](https://developers.pipedrive.com/docs/api/v1/Leads): listas separadas e campos customizados herdados de negócios.
- [Deals](https://developers.pipedrive.com/docs/api/v1/Deals): coleções v2 e paginação por cursor.
- [Mudança dos arquivados](https://developers.pipedrive.com/changelog/post/breaking-change-archived-deals-and-leads-will-not-be-returned-in-existing-endpoints-and-will-not-be-editable): separação de ativos/arquivados.
- [Limites de uso](https://support.pipedrive.com/en/article/usage-limits-in-pipedrive): total combinado de leads ativos e negócios não arquivados; conferência na tela Uso.
- [Billing](https://developers.pipedrive.com/docs/api/v1/Billing): catálogo consultado não fornece o limite combinado do plano; a implementação exige valor informado, sem inventar rota.
