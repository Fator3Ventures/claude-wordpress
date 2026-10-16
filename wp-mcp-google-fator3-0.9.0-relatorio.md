# Entrega — Fator3 MCP Google 0.9.0

Release única do escopo planejado como 0.8.6, revisão 4. A instrução final substitui as entradas intermediárias: WordPress limpo ou Google **0.8.4 → 0.9.0**, MCP **0.21.0 → 0.22.0** e Core **1.31.0 → 1.33.0**. Não houve implantação em produção ou modificação nos fontes/instaladores dos acompanhantes. Números de versão identificam ensaios, sem condicionar instalação, ativação ou ordem no código.

## Resultado funcional

- Coleta completa optativa GA4/GSC com orçamento, paginação nativa, cursor opaco, retomada e jobs explícitos. Plano fixa identidade, conexão, recursos, datas, filtros e política; continuidade e leitura revalidam a concessão. Outra concessão do mesmo usuário não herda acesso a resultado protegido.
- Cobertura e qualidade por propriedade/período, preservando metadados nativos, parcialidade, causa de parada e desconhecido versus zero. GSC mantém `all_rows_guaranteed:false`; completar o plano não remove limites da origem.
- Calendário por semana ISO, mês, trimestre e ano, com política de períodos parciais. Usuários/sessões vêm de consulta ao intervalo nativo; CTR tem proveniência e regra para denominador zero. Não há soma de moedas ou universos incompatíveis.
- Exportação com `require_complete` como padrão; `allow_partial` precisa ser explícito. Todas as fontes são preparadas antes de escrever. Recibo separa extração, aplicação e verificação. Replace confere o retângulo exportado por releitura limitada em lotes; append confirmado reutiliza recibo e não se repete diante de resultado desconhecido. O append não anuncia releitura integral quando a API não informa a faixa inserida.
- Contexto de medição e catálogo Core pelos schemas e SDK públicos 1.0.0, com seis slots, revisão, procedência e paginação. Eliminadas as leituras privadas dos dois adaptadores. Binding verifica revisão após descoberta e antes da gravação; concorrência otimista não equivale a transação entre plugins.
- Distribuição pelo SDK público MCP, dono único, seleção/revisão e recibo que preserva a intenção com produtor ausente. Removidas leitura de opções privadas e interferência nos filtros MCP. ZIP manual continua independente.
- Bridges Google declaradas pelo registro público MCP, autorização de bridge e alvo separadas e recusa de alvos Core/Meta/LinkedIn ou executores aninhados.
- Schemas de status, armazenamento, cache e cron completos para os campos exercitados. Service Account padrão, configuração verificada, selftest, PUT vazio, cron por origem, recuperação e isolamento atuais preservados.
- **281 habilidades**, 108 leituras e 173 escritas, todas com `meta.fator3.version:0.9.0`; 34 opções. Catálogo 3.0.0, configuração 4.0.0, execução 2.0.0, armazenamento/manutenção 2.0.0 e leitor GSC 1.0.0 preservados. Confirmações de exportação usam intenção 2.0.0 e a política efetiva; autorização antiga não é reinterpretada para outro efeito.

Não foram reinseridos importadores/migrações históricos, aliases removidos ou reparos durante diagnóstico. As tabelas correntes da 0.8.4 são utilizadas diretamente. Grants de rotas retiradas não concedem `google/maintenance`.

## Validação do instalador final

**1148 testes unitários / 13650 asserções e 1451 verificações nativas aprovadas.** Contagens nativas incluem repetição na matriz. Testes recebidos dos outros plugins e ensaios preliminares não foram somados.

| Grupo | Testes/verificações | Resultado |
|---|---:|---|
| lab-controls | 11 | Aprovado |
| unit | 1148 | Aprovado |
| native-clean | 501 | Aprovado |
| native-repro | 501 | Aprovado |
| native-install | 16 | Aprovado |
| native-upgrade | 386 | Aprovado |
| native-upgrade-google-first | 38 | Aprovado |
| native-no-companions | 9 | Aprovado |
| package | 128 | Aprovado |
| build-negative | 17 | Aprovado |

Ambiente: WordPress 7.1.2, PHP 8.3.6, MySQL 8.0.46, PHP-FPM/lighttpd e WP-CLI 2.12.0. Banco e HTTP WordPress/MCP reais; APIs Google simuladas. Duas instalações limpas executaram em paralelo com bancos, portas e processos separados. Instalação sem acompanhantes e upload/ativação combinados também passaram, observando opções, tabelas, cron e credencial ausente **antes** da manutenção.

Atualizações foram feitas por MCP HTTP autenticado, com SHA-256 esperado e nova requisição após troca. Nos dois percursos, valores `false`, cifras, vínculos, serviços, conexão adicional, job concluído, agenda pausada e auditoria foram preservados. Prévia de rollback aprovada, sem aplicar retorno. O inventário final dos três plugins foi conferido por Python após parar os processos: todos os arquivos coincidem com os ZIPs, sem arquivos antigos extras. Essa conferência é um gate de liberação.

### Ressalvas de integração observadas

1. **Intervalo MCP 0.22.0/Google 0.8.4:** o novo registro MCP não admite as bridges Google da base 0.8.4; seu adaptador nominal cobre 0.8.5. A atualização continua possível pelo executor de pacotes. A 0.9.0 declara as bridges explicitamente. Atualizar Google primeiro evita esse intervalo; as duas ordens chegaram ao trio final validado. Não é uma trava do Google.
2. **Conflito intermitente na bancada inicial:** ocorreram recusas de pós-imagem/rollback em diretórios sob a pasta de trabalho, com arquivos antigos extras após a substituição. Os percursos em diretórios temporários passaram; a causa anterior não foi estabelecida. O gate final foi ampliado, sem relaxar rollback ou limpar arquivos antigos por código Google. Não se atribui o problema ao MCP nem se declara uma correção inexistente. O encaminhamento MCP inclui a observação e os dados necessários para investigar eventual reprodução em homologação.
3. A leitura de snapshot Core comprova configuração observada; não comprova emissão no navegador, consentimento individual ou recebimento remoto. Ads continua dependente da configuração e homologação própria de cada instalação.

## Rastreabilidade G01–G12

| Grupo | Entrega e evidência principal |
|---|---|
| G01 | Schemas reutilizáveis de status/storage/cache/cron; Release090StatusTest e exportador de contratos. |
| G02 | Instalação combinada, pacote inativo idêntico e primeira leitura antes de manutenção; native-install. |
| G03 | Manifesto parametrizado, cenários sem entradas desnecessárias, diretórios próprios, hashes e controles negativos; tools/lab.py, lab-controls e build-negative. |
| G04 | Handler MCP, grants, configuração, SDK GSC, cron, recuperação e isolamento Core/LinkedIn; integration/core/isolation/triggers/tokens. |
| G05 | Guias, contratos, catálogo, exemplos e documentação PHP regenerados; check-docs e pacote allowlist. |
| G06 | CoreContext/CoreBinding/TagManager com contrato público completo; testes de revisão/slots/paginação e public-sdk com Core real. |
| G07 | Distribution/Updater com SDK e recibo públicos; Release090DistributionTest e public-sdk com MCP real. |
| G08 | Registro explícito e revalidação de principal; public-sdk, integração e isolamento. Ressalva transitória 0.8.4 encaminhada ao MCP. |
| G09 | Collection/Quality/FrozenInput e jobs; Release090CollectionTest, envelope nativo e limites. |
| G10 | Exportação estrita, recibos, releitura e replay; BlendSheetsTest e testes atuais de confirmação/gates. |
| G11 | Calendar e agregados nativos; virada ISO, datas civis/DST, períodos parciais, CTR zero/null e usuários nativos. |
| G12 | Contratos e fixtures de cinco provedores, sem tokens ou coleta social no Google; public-sdk/isolation e documentação. |

## Matriz C01–C21 e atualização do escopo

| Critério | Resultado |
|---|---|
| C01 | Aprovado: cobertura explícita de campos, casos indisponíveis e fixture de tipo incorreto. |
| C02 | Substituído pela instrução final: a base 0.8.5 não é instalada. Correção do combinado MCP comprovada com Google 0.9.0 em C04. |
| C03 | Aprovado: limpo, duas ordens e Google sem acompanhantes. |
| C04 | Aprovado: instalação combinada e pacote presente/inativo, nova requisição antes de manutenção. |
| C05 | Retirado pela instrução final: MCP 0.21.1 não integra o percurso. A base real 0.21.0 entra em C08. |
| C06 | Aprovado: 0.8.4 → 0.9.0 direto, preservação e rollback em dry_run. |
| C07 | Retirado pela instrução final: Google 0.8.5 não foi instalado; nenhuma passagem intermediária exigida. |
| C08 | Aprovado para o trio final nas duas ordens, com ressalva transitória de descoberta e observação preliminar descritas acima. |
| C09 | Aprovado: persistência/estrutura/agendamento, diagnóstico sem reparo e hooks de terceiros preservados. |
| C10 | Aprovado: MCP 0.22.0 e Core 1.33.0 reais; transporte Google simulado. |
| C11 | Aprovado: identidade do código/ZIP/evidências, controles negativos e inventário final instalado. |
| C12 | Aprovado: documentação corrente e protegida; Core configuração 7.1.0, Google configuração 4.0.0 e SDKs distintos. |
| C13 | Classificação individual abaixo; nenhum opcional anunciado como implementado. |
| C14 | Aprovado no consumidor: contrato Core completo, seis slots, revisão/procedência, paginação e produtor real. Não substitui prova de emissão do Core. |
| C15 | Aprovado: seleção pública, dono único, ausência/falha sem troca implícita de origem e ZIP manual. |
| C16 | Aprovado na 0.9.0: declaração/autorizações e rejeição de alvos alheios; lacuna do adaptador transitório encaminhada ao MCP. |
| C17 | Aprovado com APIs simuladas: páginas, filtros locais, recortes com erro, orçamento, revogação e continuação. |
| C18 | Aprovado com respostas controladas: metadados ausentes/conflitantes, limites e distinção de zero/null. |
| C19 | Aprovado em testes simulados: estrito/parcial, destino preservado antes da escrita, verificação delimitada e append sem replay cego. Sem planilha real. |
| C20 | Aprovado em testes simulados: calendário e agregado nativo, incluindo períodos parciais e zero denominador. |
| C21 | Aprovado para isolamento por fixtures Meta/LinkedIn e produtor Core real. Não certifica binários sociais não fornecidos. |

## Tickets recebidos

| Ticket | Situação nesta entrega |
|---|---|
| GOOGLE-01 | Implementado: adaptador público Core e catálogo. |
| GOOGLE-02 | Implementado: distribuição pública MCP. |
| GOOGLE-03 | Condicionado no plano: homologação Google Ads não executada. |
| GOOGLE-04 | Implementado: registro público de bridges. |
| GOOGLE-05 | Implementado: regressão, diagnóstico, documentação e receitas existentes. |
| GOOGLE-06 | Condicionado no plano: novo SDK de leads Ads não incluído. |
| GOOGLE-07 | Implementado: coleta completa limitada e retomada. |
| GOOGLE-08 | Implementado: exportação com política de completude e verificação. |
| GOOGLE-09 | Implementado: qualidade e proveniência por recorte. |
| GOOGLE-10 | Implementado: calendário e agregações nativas. |
| GOOGLE-11 | Receitas documentadas; novos atalhos opcionais não priorizados. |
| GOOGLE-SOC-01 | Opcional no plano: escritor Sheets social não incluído. Os provedores conservam CSV/JSON próprios. |

## Pacotes e reprodução

Instalador: **147 arquivos / 18 diretórios**, todos com índice silencioso. Sem Markdown, docs/, reference/, testes, ferramentas ou .htaccess públicos. Documentação/scripts correntes ficam em dados PHP protegidos e downloads autenticados. Fonte inclui documentação integral, scripts Cloud Shell revisado/original, testes, contratos e evidence/090. Scripts não foram executados.

SHA-256 instalador: `333e3f177be1095ac9e568e66d4d8cab9b4dfbd4d6a86505e8b7a02583182b32`.

| Entrada | Versão | SHA-256 |
|---|---|---|
| mcp | 0.22.0 | `622b75d20c3dc115bb8391d08f59c484ebbc6ac78547b8dac08b0f6b10e1fa7d` |
| core | 1.33.0 | `de427cb219be769d9e44ae9aaf5e6f31055990b3d8f9b8664ac0faa596f61364` |
| baseline | 0.8.4 | `f06474bcba158ef838450c2c7a95cbff3bc876c3ddcfa05e5a5434fce06940f7` |
| candidate | 0.9.0 | `333e3f177be1095ac9e568e66d4d8cab9b4dfbd4d6a86505e8b7a02583182b32` |
| baseline_mcp | 0.21.0 | `6c1a788f6a11ad60b9fa53fda8a091ce11b74b1981f521c5d7d8c428fda47ce7` |
| baseline_core | 1.31.0 | `bd84d4d9f06d4ecda6340a483b04c5b39e386ab528b5d29a8803a266ffe0d6a8` |

O fonte contém manifesto portátil, JUnit, grupos nativos, controles de build e instruções em tools/README.md. Dependências do laboratório são externas; nenhuma credencial ou banco local acompanha o pacote. Evidence/084, evidence/085 e docs/history são históricos e não integram as contagens desta entrega. O relatório e encaminhamentos são anexos de entrega, fora da identidade do runtime.

## Limites

Sem implantação, chamadas Google/Meta/LinkedIn reais, emissão de tags no navegador, execução Cloud Shell, homologação Ads/Sheets, crontab hospedado, CDN, multisite completo ou Redis/Memcached real. Dados de homologação anteriores fornecidos pelo usuário não foram reexecutados. Rollback de arquivos não reverte banco, configuração ou efeitos remotos. Não há promessa de snapshot consistente de dados Google recentes, atomicidade entre plugins ou todas as linhas GSC.
