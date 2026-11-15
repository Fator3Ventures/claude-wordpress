# Entrega — Fator3 MCP Meta 0.27.0

Revisão 1 · 15/11/2026 UTC · **Apta no escopo testado** · Pedidos MCP Meta 30. Release exclusiva do plugin `wp-mcp-meta-fator3`.

## 1. Entrada e versões

Instalação limpa e atualização direta da 0.26.0. Nenhuma intermediária. WordPress mínimo 7.1.4 e PHP mínimo 8.3 de 64 bits. Ambiente verificado: WordPress 7.1.4, PHP 8.3.6 de 64 bits, MariaDB 11.8.6 e Chromium 150.0.7871.181. Normas: `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, revisão 5 de 02/11/2026; complementos específicos Meta e Regra comum de 14/11. Referência visual de entrada: Meta 0.26.0 e LinkedIn 0.23.0.

## 2. Convivência, escopo e impactos

No laboratório, o Core 1.87.3 foi testado com o Meta 0.27.0 em dois conjuntos: MCP 0.45.0, Google 0.35.0, LinkedIn 0.23.0 e Pipedrive 0.10.0; e MCP 0.46.0, Google 0.36.0, LinkedIn 0.24.0 e Pipedrive 0.11.0. Os 44 testes passaram em cada conjunto, inclusive descoberta de 47 operações, leitores do Core e documentação. Hashes dos instaladores em `evidence/027/bases.json` e `companions-next.json`.

Inventário do Site-Teste na verificação após instalar o Meta:

| Pacote | Versão ativa |
|---|---|
| Fator3 MCP | 0.45.0 |
| Fator3 MCP Google | 0.35.0 |
| Fator3 MCP LinkedIn | 0.24.0 |
| Fator3 MCP Meta | 0.27.0 |
| Fator3 MCP Pipedrive | 0.11.0 |
| Fator3 Site Core | 1.87.3 |

Sem ordem especial de troca. Nenhuma alteração de contrato, dados ou permissão foi identificada para o LinkedIn ou os demais plugins. Nenhum relatório de impacto foi gerado. O Meta mantém as leituras e o histórico de Instagram, Facebook e anúncios; escrita em anúncios, Pixel, CAPI e contatos não entram nesta entrega.

## 3. Pedidos MCP Meta 30 — mudanças e evidência

- A versão fica à direita do título nas três larguras. Os três grupos e suas dez abas mantêm os endereços existentes, com quebra de linha nas subabas. A orientação e a ação principal ficam juntas; os estados de coletas, agendas, consultas e ativos têm texto e cor.
- Busca sem distinção de acento e navegação Anterior/Próxima em conexões, ativos, usuários carregados, consumidores/concessões, coletas, agendas, índice de ajuda, Stories e linhas de resultados. Cada controle indica o intervalo visível e a quantidade carregada. Filtrar ou mudar de página conserva as marcações dos ativos. A busca não lê silenciosamente novas páginas remotas.
- Tabelas largas rolam dentro da região acessível pelo teclado e mantêm as palavras inteiras. Em Relatórios, Histórico, Conversas e Arquivo de Stories, voltar ao lote anterior usa a consulta original. Alterar a seleção limpa resultados e cursores; respostas atrasadas são descartadas.
- Na 0.26.0, a verificação de 360 px registrou falha de alinhamento do selo nas duas telas de referência e ausência de busca/paginação na tabela. Evidência anterior em `referencia/` e `ui-matrix-base.json`; verificação da candidata em `ui-matrix.json`.
- **39 PNG** em `capturas/`: dez abas × três larguras (360, 768 e 1440 px) mais três subvisões × três larguras (edição de conexão, agendas e configuração da recepção). O arquivo externo de capturas abre por `index.html`, inclui os PNG completos e o SHA-256 de cada imagem. As imagens vêm do wp-admin em laboratório, com dados fictícios.
- A comparação das duas distribuições está em `runtime-diff.json`. As alterações executáveis ficam no painel, além da identidade da versão. Ajuda e documentos de migração, administração e release foram atualizados.

**Testes automatizados:** 684 verificações aprovadas. Cada suíte é contada uma vez; os 44 testes repetidos contra outra combinação são identificados. Falhas propositais na referência, tentativas descartadas e sondas do Site-Teste não entram no total.

| Suíte (arquivo JSON em evidence/027) | Aprovadas |
|---|---:|
| release022 | 46 |
| release0221 | 20 |
| smoke | 40 |
| configuration | 16 |
| export-integrity | 27 |
| dataset | 77 |
| access0221 | 8 |
| worker023 | 8 |
| migration | 18 |
| origin | 38 |
| combination | 44 |
| combination-next | 44 |
| grant | 20 |
| core-alone | 1 |
| docs-lint | 26 |
| docs-integrity | 14 |
| docs-build | 10 |
| ui-origin | 7 |
| panel-forms | 20 |
| ui-matrix | 200 |

## 4. Instalação e prova da troca

Conferir SHA-256 e slug. No WordPress de teste, o MCP instalou o ZIP com `expected_sha256`, `expected_slug=wp-mcp-meta-fator3`, verificação HTTP e manutenção da ativação. A versão passou de 0.26.0 para 0.27.0. Os caminhos / e /wp-json/ passaram nas sondas. `meta/status`: versão 0.27.0, estado ok, armazenamento e criptografia prontos. `meta/selftest`: verificações locais aprovadas. `system/health`: healthy=true. Em `meta/documentation`, os 32 arquivos instalados foram reconstruídos pela rota e comparados com o ZIP. Abrir Ferramentas → Fator3 MCP Meta → Suporte → Ajuda para conferir a versão. Registro sanitizado em `site-teste.json` e `docs-site.json`. Produção e publicação no repositório da frota ficam fora desta entrega.

## 5. Banco, retenção e recuperação

Nenhuma alteração de esquema, retenção, credencial, permissão, revisão ou agenda por causa da nova interface. O teste de migração verificou a preservação de 15 registros, quatro linhas de histórico e uma opção do cenário controlado. O progresso da migração anterior continua como estava. A busca/paginação funciona na memória do navegador. Salvar uma configuração continua sendo a ação explícita existente. Antes de instalar no Site-Teste foram exportadas as duas tabelas do Meta (630 linhas) e 8 opções. Nenhum valor foi incluído na entrega. A volta de arquivos não desfaz mudanças de dados realizadas pelo operador; se houver defeito, corrigir com nova versão.

## 6. Limites da validação

O navegador e o WordPress do laboratório são reais. As linhas e cursores usados para repetir as consultas são sintéticos; os testes dos leitores simulam respostas de Graph/CDN. Não foram homologados conta comercial real, disponibilidade de métricas por versão da Graph, entrega de webhook, mídia real nem execução agendada sob tráfego de produção. O Site-Teste tinha 0 conexão(ões) Meta na verificação final. Não houve operação comercial externa.

## 7. Credenciais e configuração

Não é preciso redigitar credenciais existentes. Para uma nova conexão, o responsável informa o token do usuário do sistema e o segredo do aplicativo nos campos protegidos. Nome, App ID, validade (UTC), contas, permissões e ativos são configurados e conferidos separadamente. A versão padrão da Graph é v24.0; permissões dependem do relatório, por exemplo instagram_basic, instagram_manage_insights, pages_read_engagement ou ads_read, conforme o guia instalado. Nenhum segredo é exibido no relatório.

## 8. Identidade dos arquivos

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-meta-fator3-0.27.0-instalador.zip | 273138 | `77e2364a471c41399b6fa5d11feecebabcc1d2722bd5bca89eacbee803733ca6` |
| wp-mcp-meta-fator3-0.27.0-capturas.zip | 4104307 | `3b81422e6c009f0fe6a40b30de82c88f50577dd170cdaf16e88d0ecd65327501` |
| wp-mcp-meta-fator3-0.27.0-fonte.zip | 5314902 | `fd1f2a5d17a131a2c93f4f32915ee99a716f9dd6baf5ede6a13b4458d835efab` |

Fonte editável e runtime instalável têm raízes próprias e não contêm ZIPs internos. O manifesto do instalador permite conferir cada arquivo. Compressão do build: Python 3.12.14 / zlib 1.3.2.
