> Relatório externo canônico. A cópia interna do fonte é anterior ao fechamento do ZIP e não contém seu hash final.

# Entrega — Fator3 Site Core 1.72.1

Revisão 2 · 2026-11-06T10:12:40-03:00 · Rodada: reconstrução ampliada do fonte e validação da implementação existente.

Slug: `base-site-core-fator3`. Status geral de homologação: **com-pendencias**. A reconstrução solicitada está concluída, com **617 verificações funcionais aprovadas**, build reproduzível e instalador original preservado. Permanecem pendências de ambientes e integrações não exercitados, discriminadas na seção 6.

Foram lidos integralmente `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, ambos revisão 5, de 02/11/2026. O pedido explícito desta rodada autoriza reconstruir e regenerar o **fonte da 1.72.1**. A ampliação se restringe a ferramentas de desenvolvimento, testes, evidências e documentação externa ao runtime; nenhum byte do instalador foi alterado. Não é uma nova release de código executável.

## 1. De onde esta versão entra

Base: **1.72.0 → 1.72.1**, além de instalação limpa. A base 1.72.0 foi recuperada da pasta instalada no Site-Teste, com 933 arquivos. O candidato 1.72.1 veio do instalador original preservado naquele ambiente, com 935 arquivos. Seus hashes por arquivo constam no fonte.

Requisitos declarados: **WordPress >= 7.1.4, PHP >= 8.3, 64 bits**, instalação única. Ambiente funcional efetivamente executado: **WordPress 7.1.4, PHP 8.4.27, MariaDB 11.8.6**. Ferramentas: Python 3.12.14, Node 24.22.1, npm 11.9.0, Terser 5.44.1, jsdom 27.4.0 e rcssmin 1.2.2. PHP 8.3 e MySQL 8.4 não foram executados.

Identidade: `base-site-core-fator3/base-site-core-fator3.php`, Text Domain `f3base`, contrato administrativo **8.34.0**. Não houve instalação remota da 1.72.1 nesta reconstrução.

## 2. Convivência e encaminhamentos

O inventário remoto recuperado registra Core 1.72.0, MCP 0.41.0, Google 0.30.0, LinkedIn 0.19.0, Meta 0.21.0 e Pipedrive 0.7.0. É a combinação observada no Site-Teste durante a recuperação. Os testes funcionais novos executaram somente o Core no laboratório local; não se declara homologação integrada desses acompanhantes.

A correção administrativa da 1.72.1 mantém contrato 8.34.0, permissões e schema da 1.72.0. A reconstrução atual preserva todo o runtime. Não foi identificada adaptação exigida dos outros plugins por essa correção ou pelos novos arquivos de desenvolvimento; nenhum relatório de impacto individual foi emitido. Integrações com fornecedores e acompanhantes seguem não avaliadas nesta rodada.

## 3. Mudanças e evidência

Pedido vigente sem ID numérico: “Reconstrua a 1.72.1 tentando recuperar o máximo de trabalho já realizado. Gere novamente os arquivos fonte da 1.72.1 atualizado”.

| Item | Resultado | Prova e classificação |
|---|---|---|
| Recuperação integral | Runtime 1.72.1, runtime-base 1.72.0 e material de desenvolvimento 1.71.0 preservados | `validado-localmente`: manifestos, SHA-256 e comparação dos 935 arquivos da candidata |
| Build atual reconstruído | 84 JS e `includes/ativos-build.php`, incluindo CSS incorporado, reproduzidos byte a byte | `validado-localmente`: 85 arquivos idênticos; `assets-reproduzidos.json` |
| Instalador reproduzido | 4.323.938 bytes; mesmo SHA-256 do original | `validado-localmente`: ZIP reproduzido, integridade CRC e identidade de todos os arquivos |
| Painel duplicado | Base 1.72.0 renderiza dois painéis/formulários; 1.72.1 renderiza um | `validado-wordpress`: hooks nativos, visões qualidade/vitais, filtros escapados e recusa sem autorização; sem prova visual |
| Perfis do cliente e vitais | Scripts completos, perfis de tracking/público e contatos, origem, fila entre versões, consentimento, supressão e deduplicação | `validado-localmente`: 395 asserções em jsdom, provedores controlados |
| Custo da sonda pública | Instrumentação suprimida nos contextos públicos esperados; conservada nos demais | `validado-localmente`: 68 asserções em 17 contextos HTTP com dispatcher WordPress; sem banco nesse grupo |
| Schema e consulta de vitais | Migração aditiva, retomada, idempotência, recusa de estruturas incompatíveis, filtros, p75 e maior sequência concorrente | `validado-wordpress`: 52 asserções; dois processos concorrentes e 993 linhas sintéticas |
| Regressão de medição | Fases, denominadores, p75, zero, erros e paginação | `validado-wordpress`: 27 asserções do teste 1.71.0 reaproveitado e executado na 1.72.1 |
| Instalação e atualização direta | WordPress limpo e troca 1.72.0 → 1.72.1 concluídos; dados/configuração sintéticos preservados | `validado-wordpress`: etapas em processos separados e hashes antes/depois |
| Reativação | 33 tabelas auxiliares restauradas, zero consultas prematuras às tabelas removidas | `validado-wordpress`: desinstalação e reativação no laboratório, conforme política de retenção |
| Documentação e seleção de assets | Leitura paginada íntegra, recusa a travessia/anônimo, seleção dos quatro perfis | `validado-wordpress`: 37 asserções; transporte MCP remoto não exercitado |

Contagem atual: **395 cliente + 68 sonda HTTP + 154 WordPress nativo = 617 verificações**, todas aprovadas. São asserções, incluindo casos parametrizados. **596 arquivos PHP aprovados no lint** e **85 arquivos gerados idênticos** são contagens separadas.

A suíte específica original da rodada interrompida não foi encontrada. `build/` e `tests/` documentam a reconstrução; `history/1.71.0/` conserva os scripts, testes, evidências, lockfiles e insumos anteriores. A regressão de medição reaproveitada tem origem explicitada. Resultados históricos não entram no total atual.

O pacote inclui `docs/RECONSTRUCAO-1.72.1.md`, instruções de execução no `README.md`, `evidence/1721-reconstrucao/resumo.json`, manifestos e evidências sanitizadas. O manifesto original de assets conserva rótulos legados de gerador; as ferramentas realmente usadas nesta reconstrução e os hashes reproduzidos estão no relatório JSON do build.

A comparação de tamanho de arquivos consta em `tamanhos-assets.json`: contatos completo caiu de 17.382 bytes na 1.71.0 para 16.087, enquanto tracking cresceu 281 bytes. Não se infere melhora de latência ou de vitais reais a partir desses tamanhos. A economia histórica de bytes de página não foi medida novamente.

## 4. Instalação e prova de prontidão

O orquestrador `tests/run-native.py` cria um laboratório novo, instala WordPress 7.1.4 e Core 1.72.1, exercita a versão, prepara uma segunda instalação com o runtime 1.72.0 recuperado, semeia dados sintéticos e troca diretamente para a 1.72.1. Cada etapa PHP roda em processo novo. Os ciclos retornaram `finalizacao_concluida` ou `atualizacao_concluida`, conforme a etapa; os 12 subprocessos terminaram com código zero.

A atualização conservou **993 amostras sintéticas** e o checksum da configuração. Essa população foi criada exclusivamente para o teste; não é uma cópia das 993 amostras observadas no Site-Teste durante a primeira recuperação. HTTP externo e e-mail do WordPress permaneceram bloqueados pelo MU-plugin de laboratório.

A implementação de leitura documental foi executada localmente, com revisão e hash de `RELEASE-1.72.1.md`, `VITAIS-VERSAO.md` e `AGENTES-1.72.1.md`. Os serviços locais foram encerrados após os testes. Bancos, WordPress, senhas e logs brutos de laboratório não integram a entrega.

No ambiente compartilhado, a rodada apenas recuperou código e removeu o ZIP temporário 1.72.0 criado por ela. Não houve alteração de configuração, dados, acompanhantes ou instalação da candidata. O instalador original 1.72.1 foi preservado. A publicação e distribuição pela frota não foram executadas.

Para a instalação compartilhada futura, conferir o SHA-256 da seção 8, publicar os bytes verificados conforme o fluxo da frota e descobrir o contrato real de upload. O schema anteriormente consultado de `plugins/upload-base64` aceita `zip_path`, `expected_slug`, `expected_sha256`, `overwrite`, `activate` e `idempotency_key`; nenhuma chamada de instalação foi feita nesta reconstrução. Depois da troca, conferir em novo processo `plugins/list`, `f3base/saude-ler` e `f3base/documentacao-ler`, além do painel `admin.php?page=f3base-medicao&area=tecnico&visao=vitais` no navegador.

## 5. Banco, migração e correção por nova versão

A 1.72.1 mantém o schema da 1.72.0. O teste adicional do código herdado da 1.72.0 confirma introdução aditiva de `versao_origem`, preservação das linhas sintéticas existentes, retomada após falha DDL e recusa de schema incompatível. O teste de atualização direta conserva os dados e opções sintéticos por checksum.

Desinstalação tem política distinta: remove a tabela operacional de vitais, conserva a configuração e permite recriar as tabelas na reativação. A preservação das 993 amostras foi comprovada na atualização, sem alegação de retenção após desinstalação. Não houve migração nem escrita de dados no Site-Teste por esta reconstrução.

Na primeira recuperação, a revisão automática recusou a exportação integral dos valores das opções WordPress por possível exposição de informações sensíveis e falta de autorização específica. Foram obtidos somente metadados/hashes. Esta rodada não repetiu essa exportação; trabalhou com código e dados sintéticos. Esse bloqueio não constitui resultado de teste do plugin, e nenhum backup recuperável das opções reais foi produzido.

Correções de runtime após instalação exigem nova versão. Não há downgrade nem migração reversa. A regeneração do fonte 1.72.1 atende à instrução explícita atual; seu instalador permanece imutável.

## 6. Pendências de validação

| Pendência | Motivo e continuidade |
|---|---|
| PHP 8.3 e MySQL 8.4 | Ambiente executado foi PHP 8.4.27/MariaDB 11.8.6; responsável pelo Core deve repetir a suíte nesses runtimes quando requeridos |
| Navegador, layout e `SCRIPT_DEBUG` ligado | A prova atual valida HTML nativo e jsdom; inspeção visual e esse modo permanecem para homologação do Core |
| Implantação no Site-Teste e transporte MCP remoto | Fora da reconstrução do fonte; frota deve instalar os bytes verificados e conferir saúde/documentação após a troca |
| Acompanhantes e fornecedores reais | Sem contas/SDKs reais no laboratório; responsáveis devem validar integrações no conjunto vigente |
| Scripts específicos originais perdidos | Não localizados; substituídos por suíte reconstruída, identificada e executada |

Instalação limpa, atualização local direta, regressões funcionais listadas e build, antes pendentes no relatório revisão 1, estão comprovados nesta revisão. A reconstrução do fonte foi concluída; as pendências acima delimitam a homologação.

## 7. Credenciais e configuração do dono

A correção de painel não introduz tokens ou campos novos. O acesso exige administrador com `manage_options`. O laboratório não usa credenciais de fornecedores e não exige valores do dono. Configurações e salts gerados localmente não integram o fonte. Há fixtures históricas com marcadores e credenciais sintéticas de laboratório, explicitamente identificadas; não são dados do site real.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador original preservado | [base-site-core-fator3-1.72.1-instalador.zip](base-site-core-fator3-1.72.1-instalador.zip) | 4323938 | `3d13dfc96c6dec31221dbe989bdbee27beedbcf98719be0a0447bba7078242f6` |
| Fonte reconstruído e ampliado | [base-site-core-fator3-1.72.1-fonte.zip](base-site-core-fator3-1.72.1-fonte.zip) | 10642789 | `4e24102711431bc5ad75702fe76b89183f4dc87dbc4b8c9aad07d75993c29262` |

Relatório externo canônico: `base-site-core-fator3-1.72.1-relatorio.md`. A cópia incluída no fonte precede o fechamento desse ZIP; tamanho e hash finais são preenchidos somente no relatório externo. Nenhum ZIP contém outro ZIP.

## 9. Histórico e checklist de encerramento

- Revisão 1: recuperação do instalador, lint, reprodução do ZIP e fonte inicial com histórico 1.71.0; testes específicos ainda indisponíveis.
- Revisão 2: recuperação do runtime-base 1.72.0, ampliação do histórico 1.71.0, reconstrução do build e dos testes, execução local completa e novo ZIP-fonte solicitado pelo dono. Fonte anterior: 5.728.046 bytes, SHA-256 `ccdf8917b868b3da789982c31292791a9a46ad4d84f95f9543c6de38236731b0`. Relatório anterior arquivado no fonte.

Checklist pertinente conferido: normas/revisões e precedência; base/alvo e requisitos; preservação dos contratos; três artefatos coerentes; 935 arquivos íntegros; 596 lints; 617 asserções; build de 85 arquivos idênticos; instalador reproduzido; instruções, lockfiles e evidências; nomes, hashes e tamanhos; fonte sem dependências instaladas, bancos ou ZIPs internos; nenhum impacto individual sem consequência técnica; limitações explícitas. Não se declara homologação nos ambientes ou integrações pendentes.
