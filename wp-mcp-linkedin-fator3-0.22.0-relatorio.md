# Entrega — Fator3 MCP LinkedIn 0.22.0

13/11/2026 · implementação e homologação parcial do Pedido MCP LinkedIn 24 / Pedidos core 390. **Versão corrente: 0.22.0, ativa no Site-Teste.** O CTO Office foi consultado em sua instalação 0.21.0. Destino da entrega: dono do plugin; sem publicação em repositório público.

## 1. Base de migração

Instalação nova ou atualização direta de LinkedIn 0.21.0 (439.650 bytes; SHA-256 `ebe4363bf55476cbe1ba30df80d8ab6b2362ee2dc379c21762aa42f4a05b1bfc`). Slug e basename preservados. Normas lidas integralmente: instrucoes-agentes-plugins-fator3.md e padrao-desenvolvimento-plugins-fator3.md, ambas rev. 5 de 02/11/2026. Considerados Regra comum, lista LinkedIn de 11/11 (item 24; próximo número 25), entrega anterior e relatórios anexos. Não foi atribuído número novo. Mínimos: PHP 8.3 de 64 bits e WordPress 7.1.4. Laboratório: WP 7.1.4, PHP 8.3.6 e MySQL 8.0.46.

## 2. Convivência e encaminhamentos

| Pacote | Referência inicial testada | Conjunto final testado | SHA-256 do instalador final |
|---|---|---|---|
| core | 1.81.1 | 1.81.1 | `8a03bc5dfd3f94d81a953bb7134a14bacbc6883c5b038b4ef0fee1241c1dcb02` |
| mcp | 0.44.0 | 0.45.0 | `3659bebf22155807d12f4559cf3d9e7ef7403aec0da45fc661ad90c577c7eab9` |
| meta | 0.24.1 | 0.25.0 | `8ff54d9ec66f29c78982b6c15577436a51b934c54c73cebe88227449580ea530` |
| google | 0.34.0 | 0.34.0 | `9a5f52f35a4a7c34e21e08d12099dacb05dfdfc99d3d0cc335bde95a2676135c` |
| pipedrive | 0.9.0 | 0.10.0 | `7d021e6117c3dd10d8b64059fefced863736ecf90f30e89942e6e32b4569ceb4` |

Os cabeçalhos principais das fontes anexas coincidiram com os instaladores correspondentes. O conjunto do site mudou durante a rodada. As versões novas de Meta, Pipedrive e MCP foram instaladas por outras operações. O histórico de cada grupo de testes separa os conjuntos. Não é necessária ordem especial para este incremento do LinkedIn: o contrato e a concessão não mudaram. O consumidor oficial do Core 1.81.1 foi testado sem patch. Fonte histórica do impacto LinkedIn→Core foi anotada com o encerramento do desenvolvimento; o relatório de impacto recebido Core→LinkedIn rev. 1 não foi editado. Não há nova ação de desenvolvimento a encaminhar a Core, MCP, Meta, Google ou Pipedrive. Acompanhar eventual falha de entrega comercial pertence ao dono do fluxo.

## 3. Mudanças e evidências

- **Formulário da resposta e destino do criativo.** A 0.21.0 validava o formulário da resposta, mas seguia para a campanha e publicação mesmo que o criativo declarasse outro destino de formulário. No modo nativo, o leitor agora transmite o ID autorizado para AdSource::resolve. Se o destino declarado for inválido ou divergir, devolve ad_source_binding_invalid depois das duas leituras necessárias e antes das demais; sem campos de origem. URLs de destino não são aceitas como prova de formulário. Se o criativo omite o destino, a referência verificada da resposta basta e lead_form_urn fica nulo. Sem formulário de entrada, o modo por criativo continua operando pela conta. Provas: destino divergente, malformado, alternativo, ausente, SDK, administração e consumidor oficial.
- **Validade de mídia e miniatura.** A 0.21.0 interpretava apenas a última ocorrência de e na query e ignorava épocas numéricas curtas. Em URL com um vencimento anterior ao atual e outro futuro, devolvia o link vencido. A 0.22.0 calcula o mínimo entre vencimentos reconhecidos na URL e no metadado, trata zero como vencido e não reescreve a URL assinada. Mídia e miniatura têm prazos independentes. Mantém URL nula se vencida e prazo nulo se desconhecido.
- **Documentação instalada.** AD-SOURCE.md explica como distinguir identificação, resolução do endereço e download; CONFIGURATION.md descreve a concessão por conta e o requisito adicional para respostas nativas. Índice, migração e notas atualizados. Mesmas 100 operações e o mesmo contrato linkedin-ad-source/1.0.0; não há payload novo.

## 4. Instalação e prontidão

Na frota, conferir SHA antes de instalar o ZIP com expected_slug e expected_sha256. No Site-Teste autorizado foi usado plugins/upload-base64 com conferência de slug e SHA, overwrite e activate. Operação `f829ff497d808d3b965721d8f85b26c9`, cópia de segurança `0fdb5dfb34d3ee612a7ce114`. Ativo antes e depois, versão 0.21.0 → 0.22.0. Sondas HTTP da página inicial e /wp-json/ responderam 200 antes/depois. linkedin/status: ok, zero conexões. Autoteste: 9/9. O índice remoto identificou a 0.22.0 e os hashes de todos os 48 documentos correspondem aos arquivos do instalador. Três manuais (anúncio de origem, configuração e notas) foram lidos integralmente em seis páginas e comparados byte a byte. Antes da atualização, o mesmo endpoint de manual identificava a 0.21.0.

| Verificação no WordPress descartável | Resultado na primeira matriz | Repetição na matriz final |
|---|---:|---:|
| Origem, autorizações, MCP e adaptador oficial do Core | 51/51 | 51/51 |
| LinkedIn sem acompanhantes | 47/47 | Independente dos acompanhantes |
| Regressão funcional | 141/141 | 141/141 |
| Migração direta com dados | 7/7 | 7/7 |
| Manuais por MCP em instalação nova e após migração | 73/73 + 73/73 | 73/73 + 73/73 |
| **Total por conjunto** | **392/392** | **345/345** |

O conjunto intermediário (MCP 0.44.0, Meta 0.25.0 e Pipedrive 0.10.0) também passou em 345/345. As repetições são dos mesmos cenários, não testes distintos. Na prova de defeito, sete das 51 asserções de integração falharam na 0.21.0; todas passaram na 0.22.0. Instalador idêntico ao runtime exercitado, sem avisos PHP nos testes finais. Em laboratório os plugins e o WordPress são reais, e a rede do LinkedIn é simulada. A documentação completa no laboratório percorreu 48 documentos em 59 páginas por instalação.

**Fornecedor real.** Em 13/11/2026, no CTO Office (LinkedIn 0.21.0 + Core 1.81.1), a consulta administrativa de leitura ao criativo 1605615034 na conta 558431216 retornou a campanha 901687794, publicação, formulário, texto, título, descrição, botão, destino e mídia temporária. O JPEG baixado tinha 1200 × 1200 pixels, 109.952 bytes, SHA-256 `21ac1f76e3771234243c8a0d3d886899b23d0ca7273481bad5e73ff9c909dc98`. O primeiro cliente recebeu HTTP 403; em duas novas leituras independentes com identificadores de cliente diferentes (inclusive WordPress/7.1.4) o HTTP foi 200, com o mesmo hash e decodificação completa. A URL temporária e o binário não integram a entrega. Conferidas por leitura a concessão ad_source, responses e seleção da conta/formulário. Evidências em evidence/release0220.

## 5. Banco, migração e correção

Nenhuma alteração de tabela, índice, option de versão de banco ou concessão implícita. Na troca de arquivos foram preservados os bytes e revisões de 10 registros de referência, incluindo fila pausada, recibo de resultado incerto, escopo e retenção. A entrada direta da 0.21.0 foi exercitada. O contrato continua somente leitura. Em incidente, conter apenas o fluxo afetado e corrigir por nova versão; sem downgrade.

## 6. Pendências e responsáveis

- O Site-Teste não tem uma conexão LinkedIn. A tentativa pelo novo instalador com o identificador do pedido devolveu not_configured. Para reproduzir ali o anúncio real, o administrador deve cadastrar e autorizar uma conexão de teste com acesso à conta. Nenhuma credencial foi copiada da produção.
- O download real acima é prova do caminho administrativo por criativo na 0.21.0. Não houve instalação de 0.22.0 no CTO Office, leitura de respostas pessoais nem acionamento da ficha ou das entregas reais a Slack/Pipedrive. Essas etapas são de responsabilidade do administrador e do operador do Core, com destinos de homologação. Outro vídeo real também não foi utilizado; o cenário de vídeo e miniatura foi exercitado com fixtures.

## 7. Credenciais e configuração

Em Ferramentas → Fator3 MCP LinkedIn, manter a conta selecionada em Anúncios e configurar as credenciais da própria conexão. Em Concessões, o consumidor precisa de ad_source na conta; para a consulta por resposta, também precisa de responses e do formulário autorizado. Simular, conferir e confirmar alterações explícitas. Não há permissão de escrita em anúncio exigida para esta consulta. Nenhum token, contato, URL assinada ou conteúdo da mídia consta dos artefatos.

## 8. Identidade dos arquivos

Instalador: `wp-mcp-linkedin-fator3-0.22.0-instalador.zip`, 442167 bytes, SHA-256 `b15cd0806b52303aa4023087ad15dfdb17709271ccdf3704f67fa63dc5b583a4`. Raiz única, 92 arquivos, 91 entradas no manifesto que exclui o próprio manifesto.

Fonte: `wp-mcp-linkedin-fator3-0.22.0-fonte.zip`, 3763490 bytes, SHA-256 `da4ea667277a5f966a167505bf358c587bc2fae294c8199713d8536b359d77c2`. Apenas o instalador é instalável.
