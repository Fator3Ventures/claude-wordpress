# Entrega — Fator3 MCP Google 0.11.0

Revisão 1 · Data/hora: 2026-10-16T22:14:39-03:00 · Rodada: implementação, validação e instalação de teste.
Slug/basename: `wp-mcp-google-fator3` / `wp-mcp-google-fator3.php`.
Status: **com-pendencias — apta no escopo testado**, instalada e ativa no Site-Teste. Pendências de fornecedor, distribuição na frota e contrato de material explicitadas abaixo.

## 1. De onde esta versão entra

Instalação nova ou atualização direta **0.10.0 → 0.11.0**, sem intermediária. Base: `wp-mcp-google-fator3-0.10.0-instalador.zip`, 703838 bytes, SHA-256 `3e30634b1d1f87b9b4fdeba2a37ac382b1394a1ec7f7235166aa15d107ef8b52`; fonte base, 2615432 bytes, SHA-256 `c8a31a7ecedab64d222fb28bf2335f686540572384214f01f65fb5c8a80d0450`. Cópias recebidas com sufixo `(2)` têm esses mesmos bytes.

Foram lidos integralmente `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos revisão 4, de 16/10/2026. O incremento minor segue esse padrão. O documento de pedidos informa a 0.10.0 na frota; o estado inicial do Site-Teste confirmou essa versão.

**Requisitos declarados e executados: WordPress 7.1.2 e PHP 8.3.6**, com MySQL 8.0.46 no laboratório. Instalação limpa e atualização ocorreram nesses patches exatos. WordPress/PHP inferiores deixaram de integrar o suporte declarado; a frota deve conferir esses requisitos antes de distribuir. Não se exige versão numérica de acompanhante para ativar as funções próprias.

## 2. Convivência e encaminhamentos

Pacotes reais examinados e usados nos ensaios: MCP 0.23.0, Core 1.35.0, Meta 0.2.0 e LinkedIn 0.2.0. Hashes dos insumos em `evidence/011/input-origins.json` e `validation011.json`. Nenhum desses pacotes foi alterado. O teste de atualização substituiu Google primeiro e reaplicou os mesmos acompanhantes no laboratório; no Site-Teste somente Google foi atualizado.

| Destinatário | Classificação / situação | Recorte | Documento |
|---|---|---|---|
| `wp-mcp-fator3` | `validacao-coordenada` / resolvido no escopo testado | M91-01/M91-02; G91-01/03 | `wp-mcp-google-fator3-0.11.0-impacto-wp-mcp-fator3.md`, revisão 2 |
| `base-site-core-fator3` | `decisao-necessaria` / aberto | Core 222; I01/GSC | `wp-mcp-google-fator3-0.11.0-impacto-base-site-core-fator3.md`, revisão 2 |

Os dois documentos foram abertos no planejamento e atualizados na entrega; não foram enviados a terceiros. Os impactos sociais recebidos não exigem mudança Google: isolamento foi exercitado, sem novo relatório individual de simples aviso. Implantador atual não fornecido: não avaliado; nenhuma nova dependência ou exportação social foi criada. O risco operacional dos mínimos está explícito neste relatório para o responsável pela distribuição.

## 3. Mudanças e evidência

| Pedido | Resultado | Evidência própria |
|---|---|---|
| **Pedidos MCP Google 25(a)** | Cabeçalho e metadados Composer alinhados a WP 7.1.2/PHP 8.3.6; manuais atualizados. | `minimum011.json` nos quatro cenários: versões executadas iguais às declaradas, requisito nativo WordPress aceito, armazenamento pronto e ajuda local. |
| **Pedidos MCP Google 25(b)** | Tabela de identidade contém somente nomes finais, bytes e SHA-256, sem links para ambiente local. | Seção 8 e conferência de empacotamento. |
| M91-01/M91-02 | Consumidor Google preservado, sem compensação para transporte. Preflight real sem credencial conserva `checks_passed:false`, `all_checks_passed:false`, `passed:0`, `credential.configured:false`. Conflito do produtor Core conserva `revision_conflict`, `conflict:true`, `retryable:false`, `data:null`. | `contracts011.json`; dados de contas ausentes/sintéticos, HTTP MCP real local. A fixture herdada também verifica remoção de segredo aninhado. |
| Core 222 | Manual explica `download_material` separado de `generate_lead` e dos identificadores de contato. SDK 1.0.0 fechado permanece; não há descoberta automática de material nem criação de eventos-chave/ações/tags. | Consumidor real valida descritor, seis slots, catálogo paginado e SDK GSC. Ampliação depende do contrato proposto no impacto Core. |
| Documentação da release | 282 operações preservadas (109 leituras/173 escritas), 15 documentos compilados, mesma fonte para painel/MCP. | Geradores conferidos; leitura integral local e remota; continuação da documentação 0.10.0 recusada após upgrade. |

No instalador, somente **dois arquivos diferem da 0.10.0**: `wp-mcp-google-fator3.php` (versão/requisitos) e `includes/Data/Documentation.php`. Os outros 149 arquivos são idênticos; não há nova rotina funcional, migração, opção ou alteração de autorização. Configuração 4.0.0, catálogo 3.0.0, execução/armazenamento/manutenção 2.0.0 e SDKs 1.0.0 permanecem.

## 4. Instalação e prova da troca

| Cenário local | Verificações | Resultado |
|---|---:|---|
| WordPress limpo com acompanhantes | 195 | Aprovado no mínimo exato; funções próprias, SDKs, documentação, entrega por bytes e isolamento social. |
| Atualização direta 0.10.0, rollback e reaplicação | 187 | Aprovado; configuração/cifra/registros/pausa preservados; documento novo e recusa de revisão antiga. |
| WordPress limpo somente com Google | 17 | Aprovado sem acompanhantes. |
| Instalação inicial por HTTP MCP | 33 | Aprovado; prontidão em requisição nova antes de manutenção e requisitos exatos. |

**432 verificações nativas**, em quatro bancos descartáveis independentes, com processos encerrados. O total conta verificações repetidas entre cenários, não 432 casos únicos. **147 arquivos PHP** do runtime passaram no lint; os **151 arquivos** de cada instalação local correspondem ao instalador. Suíte PHPUnit completa e gate abrangente histórico não foram executados nesta rodada de requisitos/documentação; o validador específico é `tools/release011.py`. As evidências 010 e anteriores são históricas, não contadas novamente.

Reprodução: prover os insumos versionados da matriz e um PHP 8.3.6 configurado com as extensões descritas em `tools/lab.py`; preencher o manifesto com caminhos e hashes reais. Gerar catálogo e documentação, criar o candidato com `build/build.py candidate` e executar `tools/release011.py --manifest <manifesto> --work-base <diretorio-vazio> --evidence <evidencias-vazias> --php <executavel-php-configurado>`. O script confere dependências, runtime, código/testes, relatórios e árvores instaladas; qualquer divergência impede seu resultado aprovado. WordPress de laboratório foi reconstruído de arquivos de core 7.1.2 recuperados localmente, excluindo `wp-config`, todo `wp-content` e bancos anteriores; essa origem não é apresentada como download oficial novo.

### Site-Teste

Em `https://fator3-teste-mcp-1.dreamhosters.com/`, pelo conector autorizado, foi feita **uma atualização** via `plugins/upload-base64`, `activate:true`, `overwrite:true`, `expected_slug:wp-mcp-google-fator3` e SHA-256 da seção 8. A versão-base e o hash do arquivo principal foram conferidos imediatamente antes. O ambiente atendia aos mínimos: **WP 7.1.3/PHP 8.3.30**.

- Operação de pacote: `03f171d4a39a84a7cc7d9cf1450f2597`; pré-imagem de arquivos: `92a80f9a3a232c961148b7ad`.
- Resultado: `applied:true`, `active:true`, 0.10.0 → 0.11.0, reativação silenciosa em processo PHP novo. A pré-imagem cobre arquivos; não é backup integral do banco.
- Sondas internas de `/` e `/wp-json/`: HTTP 200 antes/depois. Não comprovam acesso externo ou cache HIT.
- Nova requisição `google/status`: 0.11.0 e `storage.ready:true`; `system/health`: saudável. Hashes dos dois arquivos alterados coincidem com o instalador.
- `google/documentation` descoberto pelo schema; **15 documentos reconstruídos em 53 páginas**, com tamanho e SHA-256 iguais ao conteúdo final compilado. A ajuda não consultou APIs Google.
- Uma conexão existente preservada no resumo local. Diferenças antes/depois restringem-se a observações temporais e cron já em funcionamento; não se declara auditoria integral dos ciphertexts remotos. Prova detalhada de preservação de cifra ocorreu no laboratório.

Estado final: Google **0.11.0**, MCP **0.23.0**, Core **1.35.0**, Meta/LinkedIn **0.2.0**, saudáveis. Nenhuma fixture, conexão sintética, consulta comercial, token novo ou alteração de configuração foi criada no site. Permanecem a pré-imagem e os registros normais de manutenção. Não foi aplicado rollback no site compartilhado.

Este foi o fluxo direto de homologação no Site-Teste, usando bytes locais com hash. **Publicação raw e distribuição na frota não foram realizadas.** Quando a frota publicar, deve verificar o arquivo efetivamente servido e usar `plugins/upload` com `expected_sha256` e `expected_slug`; não há URL publicada comprovada nesta entrega.

## 5. Banco e volta de versão

Não há mudança de schema SQL, formato de registros, defaults ou seleção. Instalação nova cria as estruturas existentes; atualização usa os dados 0.10.0 diretamente. Os ensaios preservaram opções, segredos cifrados sintéticos, conexão adicional, job concluído, agenda pausada e sentinelas sociais de tabelas/cron.

No laboratório, rollback restaurou 0.10.0 e a candidata foi reaplicada; alteração deliberada de arquivo impediu o rollback. Em operação, preservar backup coerente de arquivos, banco e material de cifra. Restaurar arquivos não desfaz efeitos Google, dados ou tarefas executadas; não repetir uma escrita remota por falha de manutenção. A pré-imagem indicada é a da única troca remota desta rodada.

## 6. O que permanece pendente

- **Core/Google — Core 222:** aceite e publicação de contrato optativo versionado para descobrir conversões por finalidade. A 0.11.0 mantém o SDK atual e a separação documental; não implementa o contrato ainda inexistente.
- **Dono/frota:** publicação do instalador/relatório, verificação raw e distribuição para os demais sites, conferindo os novos mínimos. Fonte não foi publicado no repositório público.
- **Dono/contas:** GA4/GSC reais, coleta completa/calendário/completude em produção, destino Sheets real e Google Ads. Testes de dados foram simulados; acesso real e resultado comercial não são homologados por esta entrega.
- **Matriz adicional:** navegador gráfico, multisite, cache distribuído/CDN, cron externo e versões inferiores aos mínimos não foram exercitados. Não houve mudança visual nesta rodada. Implantador atual permanece não avaliado.

## 7. Credenciais e configuração do dono

Nenhuma credencial nova é necessária para esta atualização. Configuração continua em **Ferramentas → Fator3 MCP Google**: Service Account padrão, JSON candidato e ativação explícita; OAuth em área própria. Habilitar serviços e bindings autorizados, conceder acesso aos ativos e executar diagnóstico explicitamente. Ads exige developer token e acesso à conta. Documentação estática exige administração e não exige conexão Google ativa. Nenhum valor secreto integra a entrega.

## 8. Identidade dos arquivos

| Artefato | Nome do arquivo | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `wp-mcp-google-fator3-0.11.0-instalador.zip` | 704694 | `d181deaeee8ef365ac4d6a08884d9fa3d3a3164b21f0538d8ed5d56722536bf9` |
| Fonte | `wp-mcp-google-fator3-0.11.0-fonte.zip` | 2729018 | `c142e10c544a73008bf4c132b85b36cd921fd6313aff5491e99dce61ba12c37e` |

Somente o instalador é instalável: raiz única `wp-mcp-google-fator3/`. Fonte: raiz `wp-mcp-google-fator3-0.11.0-fonte/`, runtime idêntico em `plugin/wp-mcp-google-fator3/`, código editável, scripts, testes, documentação, evidências sanitizadas, entradas e relatório. Nenhum ZIP contém outro ZIP.

O relatório externo é canônico. A cópia interna é marcada **cópia anterior ao fechamento do fonte**; tamanho/hash do próprio fonte são preenchidos somente no relatório externo depois de empacotar, sem reabrir o ZIP para inserir um hash circular.
