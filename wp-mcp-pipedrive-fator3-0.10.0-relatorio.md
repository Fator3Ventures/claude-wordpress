# Entrega — Fator3 MCP Pipedrive 0.10.0

Revisão 1 · 13/11/2026 · Implementação de **Pedidos MCP Pipedrive 12**  
Slug: `wp-mcp-pipedrive-fator3` · **Status: com-pendencias — validado no Site-Teste; aceite comercial em korvena.com.br pendente.**

## 1. De onde esta versão entra

Instalação limpa, de site único, ou atualização direta **0.9.0 → 0.10.0**. A base veio da última entrega oficial: instalador 452.473 bytes, SHA-256 `42523b9b547fc8820c3917e192c4b48341efbb1da6815c78fcc18f8a373c09c0`; fonte 419.738 bytes, SHA-256 `f64f79e648e150edc8c31e102d71ed23d591413ab04446e75240790f8f66cc78`. Os 40 arquivos do runtime inicial conferiam com o ZIP anterior. As duas normas nas fontes do projeto foram lidas integralmente (revisão 5, 02/11/2026); o pedido e as referências estão em inputs/ no fonte.

Requisitos: WordPress 7.1.4+, PHP 8.3+ de 64 bits, OpenSSL, mbstring e InnoDB. Execução de bancada: WordPress 7.1.4, PHP 8.3.6 e MySQL 8.0.46. Não se reivindica ensaio de todos os níveis de correção do PHP nem de outros bancos.

## 2. Convivência e encaminhamentos

Foram usados os cinco instaladores anexados, com identidade interna, hash confrontado com os relatórios dos mantenedores e conferência de arquivos na instalação integrada. Este mesmo conjunto estava ativo no Site-Teste. Relação completa de tamanhos e SHA-256, inclusive dos fontes: evidence/0100/companion-installers.json.

| Pacote | Versão | Fronteira examinada |
|---|---:|---|
| Fator3 Site Core | 1.81.1 | O cliente pipedrive-api-client/1.0.0 continua responsável pelo acesso ao CRM. O fluxo de origem do Core mantém nota própria fixada na oportunidade; esta entrega modifica só o campo note da atividade WhatsApp. |
| Fator3 MCP | 0.44.0 | Descoberta, autorização e execução. O schema atualizado é publicado pelo emissor. A paridade da matriz usa o instalador oficial; os 55 arquivos index.php que diferem/estão ausentes na pasta de runtime do fonte do MCP estão inventariados separadamente. |
| Fator3 MCP Google | 0.34.0 | Coexistência e identidade dos arquivos ativos. |
| Fator3 MCP Meta | 0.24.1 | Coexistência e identidade dos arquivos ativos. |
| Fator3 MCP LinkedIn | 0.21.0 | Coexistência e identidade dos arquivos ativos. |

Não foi identificada adaptação, permissão adicional ou mudança de ordem de instalação em outro plugin. Os consumidores de **whatsapp-registrar**, em especial o SDR, devem passar o novo parâmetro em todo registro novo; as demais 21 operações conservam sua interface. Sem relatório individual de impacto de pacote nesta versão.

## 3. Mudanças e evidência

**Pedidos MCP Pipedrive 12 — implementado e validado em WordPress.** Antes, cada chamada anexava uma nova linha com o prefixo de configuração e não havia um próximo passo substituível. Agora a atividade contém um cabeçalho [IA], o histórico de mensagens, seguido de um único rodapé operacional. Por exemplo, após dois registros:

```text
[IA]
13/11 10h42, nós: Posso enviar os horários?
13/11 11h05, Ana: Sim, na sexta.
Próximo: Perguntar se 14h funciona na sexta.
```

| Regra | Comportamento verificado |
|---|---|
| Próximo passo e autor | Informe `proximo`, de 1 a 4.000 caracteres e em uma linha. `autor` é opcional, até 80 caracteres; aceita o nome do contato e usa o autor configurado na ausência (padrão: nós). A data do registro usa o fuso das regras, com formato fixo dia/mês e hora. |
| Nota existente | No próximo registro elegível, conserva o histórico e os links, remove prefixos operacionais repetidos e substitui os rodapés anteriores. Preserva menções a “[IA]” e “Próximo:” dentro de mensagens e as citações em bloco. Mensagem e próximo passo novos são escapados como texto. Não edita notas em massa. |
| Repetição de chamada | Mesma chave e mesmos dados devolvem o recibo sem chamar a API. Trocar o próximo passo ou a mensagem com a mesma chave é conflito. Uma nova operação sem próximo passo não grava. A exceção permite consultar um recibo já existente da 0.9.0 com a entrada original. |
| Verificação e reconciliação | Depois da escrita, o plugin relê o registro e compara também a divisão visível em linhas. Se o fornecedor unir o rodapé à mensagem, a operação fica pendente; a recuperação não libera evidência com esse defeito. A pessoa principal, o vencimento, o progresso e as proteções de conta/administrador continuam verificados. |
| Documentação | Schema publicado para MCP e REST, guia de uso, fluxos, contrato, guia para agentes e histórico explicam a transição. O prefixo e o formato legados continuam aplicáveis à linha de encerramento; o novo formato fixo é específico de whatsapp-registrar. |

O plugin não envia mensagens de WhatsApp. A operação registra na atividade uma comunicação que já ocorreu. Não houve nova rota externa, job, cron, callback nem criação de outra nota de CRM.

## 4. Instalação e prova da troca

O Site-Teste recebeu o ZIP da seção 8 pela operação **plugins/upload-base64**, com ativação, substituição, `expected_slug=wp-mcp-pipedrive-fator3`, chave de idempotência e o SHA-256 esperado. Recibo `571b1101bf9f6cd7fda826eb3fcda6ea`; backup de arquivos `77cbdd332be82f1490192bb8`. O WordPress informou a troca de 0.9.0 ativa para 0.10.0 ativa. GET / e /wp-json/ retornaram 200 antes e depois; a consulta de saúde posterior confirmou healthy=true. A concessão comercial continuou desativada no Site-Teste.

| Prova do instalador final | Resultado | Limite |
|---|---:|---|
| WordPress limpo | 613 verificações aprovadas | Inclui formatação, escrita e releitura de notas, idempotência, recuperação, regras e regressões. CRM simulado. |
| Migração direta da 0.9.0 com dados e reinício de processo | 17 aprovadas | Recibo anterior sem novo GET nem nova escrita; opções, regras, diário e registros preservados. |
| WordPress com os cinco pacotes anexados | 90 aprovadas | Código nativo do Core e do MCP; transporte do fornecedor interceptado. |
| **Total funcional de bancada** | **720 aprovadas, 0 reprovadas** | Sem somar lint, build, sondas do site ou testes históricos. Os três cenários terminaram sem erros no log e com os 41 arquivos iguais aos do instalador. |
| Site-Teste | 22 operações; 12 documentos | Schema de whatsapp-registrar inclui proximo e autor. Documentação servida pelo MCP reconstruída e comparada integralmente com o pacote. Nenhuma fixture instalada no ambiente compartilhado. |

**Para repetir:** siga tests/README.md e execute build/lab.py nos cenários clean, upgrade e matrix. Evidências por suíte, manifesto, recibo, catálogo e verificações da troca: evidence/0100/. Na instalação compartilhada: chame `pipedrive/configuracao-ler {}`, `pipedrive/retencao-ler {}` e `pipedrive/status {}`. As duas primeiras mantiveram exatamente os dados de antes; a última devolveu `operacao_nao_autorizada`, como antes. Para ler a documentação, descubra `pipedrive/documentacao-ler`, comece por `{}` ou `{"documento":"fluxos"}` e siga `proximo_offset` com o mesmo `sha256_esperado` até `fim=true`.

Frota: antes de distribuir por `plugins/upload`, publicar e verificar bytes de `https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-pipedrive-fator3-0.10.0-instalador.zip`, usar o hash desta entrega e o slug esperado. Esta URL é o destino previsto; não foi publicada nem testada nesta rodada.

## 5. Banco, migração e correção por nova versão

O schema permanece 1. Sem migração de tabelas, redefinição das regras, alterações em credenciais ou reescrita retroativa do CRM. Em registros novos, o recibo local vincula o próximo passo e o autor à mesma chave; a evidência de recuperação inclui o resumo da disposição das linhas. As novas verificações respeitam recibos e bloqueios existentes. A troca preservou o conteúdo das opções próprias e seu autoload no Site-Teste, com zero registros nas tabelas de operações e diário antes e depois. A bancada de migração exerceu tabelas com dados.

Preservar as tabelas f3_pipedrive_operations e f3_pipedrive_journal, as opções próprias, configuração do Core e os salts do WordPress. O backup de arquivos da instalação não restaura efeitos na conta. Após escrita incerta, consultar o recibo e as operações de recuperação; não reenviar cegamente. Falha após a instalação exige nova versão corretiva.

## 6. O que permanece pendente

**Aceite comercial do Pedido 12:** a consulta a korvena.com.br encontrou 0.9.0 ativa. A frota distribui a 0.10.0 ao site-porta. Depois, o responsável pelo aceite, com a conta e os ativos de teste autorizados, deve exercitar uma nota nova e outra já existente e confirmar o cabeçalho, última linha, histórico e ausência de duplicação. Remover no mesmo trabalho os objetos de teste que forem criados (atividade, nota, lead e pessoa, respeitando vínculos) e comunicar o resultado ao SDR. Nenhum dado de cliente foi usado nem houve envio de WhatsApp, instalação em produção ou aviso de aceite. O Pedido 11 não foi reaberto; a aba atual registra o aceite da 0.8.0 e lista somente o 12 como pendente.

Não houve nova rodada visual em navegador: as telas não foram modificadas. Não se verificou como o fornecedor comercial normaliza todo HTML possível; as notas sintéticas cobrem parágrafos, divisões, formatação inline, citações, texto plano e links.

## 7. Credenciais e configuração do dono

Nenhuma nova credencial. No Site Core, configurar o token Pipedrive (campo f3base_pipedrive_token), conferir a identidade da conta e da pessoa operadora, habilitar o consumidor wp-mcp-pipedrive-fator3 e autorizar somente as operações necessárias no perfil MCP. No painel Ferramentas → Fator3 MCP Pipedrive, conferir tipo de atividade WhatsApp, fuso, autor e regras da cadência. O teste usa IDs e conteúdo sintéticos; não há valores secretos neste relatório.

## 8. Identidade dos arquivos

| Artefato | Nome final e link | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [wp-mcp-pipedrive-fator3-0.10.0-instalador.zip](wp-mcp-pipedrive-fator3-0.10.0-instalador.zip) | 460556 | `7d021e6117c3dd10d8b64059fefced863736ecf90f30e89942e6e32b4569ceb4` |
| Fonte | [wp-mcp-pipedrive-fator3-0.10.0-fonte.zip](wp-mcp-pipedrive-fator3-0.10.0-fonte.zip) | 367908 | `00705cab5640591a4c06b6077612aa3116f9dc2c9ac4af62b3f6335da5943675` |

**Relatório externo canônico, fechado após gerar e verificar o ZIP do fonte.** O instalador inclui somente o runtime. O fonte reúne código, build, testes, evidências, documentos do projeto, pedidos e cópia do relatório. Os dois ZIPs usam raiz própria e não contêm ZIP aninhado.
