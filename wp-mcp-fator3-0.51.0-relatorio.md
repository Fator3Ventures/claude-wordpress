# Entrega — Fator3 MCP 0.51.0

18/11/2026, horário de Brasília. O instalador está ativo no Site-Teste. Esta edição atende aos Pedidos MCP 87 e 88. O aceite de campo tem os limites registrados na seção 6.

## 1. Base de migração

Instalação limpa e atualização direta da 0.50.0 oficial. O SHA-256 desse instalador é 97f6c6a233c2210e24cdef205a66a41c95e20eca9ad8f3644e518bc8ed4ee95f. WordPress 7.1.4 e PHP 8.3 são os requisitos mínimos. A bancada exerceu WordPress 7.1.4, PHP 8.3.6 e MariaDB 11.8.6. O Site-Teste executa WordPress 7.1.5 e PHP 8.3.36. O plugin isolado passou nas provas de ativação, guia e saúde. Na atualização, a configuração, as conexões e os vencimentos de acesso e renovação emitidos pela versão anterior foram preservados.

## 2. Convivência e encaminhamentos

172 habilidades próprias no catálogo WordPress. Mantidos os nomes e schemas de entrada e saída. As descrições de `connections/list` e `connections/revoke` documentam os novos comportamentos. Os prazos da resposta pública OAuth mudaram. As três ferramentas de descoberta, descrição e execução conservam seus nomes. A rota principal e o alias seguem registrados. O contrato de eventos continua em `incidentes/1`.

A matriz integrada usou Site Core 1.95.0, Google 0.38.0, Meta 0.29.0, LinkedIn 0.26.0 e Pipedrive 0.12.0. O Site-Teste confirmou as mesmas versões. As alterações afetam as credenciais emitidas pelo canal. Os provedores de domínio continuam a gerir a autorização de seus respectivos fornecedores. O Core consome o vencimento informado pelo canal. Os pedidos desta edição dispensam alteração dos pacotes acompanhantes.

Pedidos anteriores 84 e 86 e pedido Core 430. O Core 1.95.0 oficial incorporou a delegação da observação do registro. Em seis requisições HTTP, o histórico do Core registrou exatamente uma abertura em cron e uma recuperação web, com origem `publicador_canal`. O acompanhamento do encaminhamento está em `docs/IMPACTO-CORE-0500.md`, revisão 3 no fonte desta edição. A observação de frota continua na seção 6.

## 3. Mudanças por pedido

| Pedido | Comportamento entregue | Prova |
|---|---|---|
| Pedidos MCP 87 | Um administrador pode revogar um registro histórico existente pelo ID completo e pela revisão corrente. A tela Clientes mostra o registro e pede confirmação. A listagem indica Sem acesso para o legado e verifica o estado da credencial para concessões e senhas de aplicação. | 106 registros históricos em páginas de 17. A revisão divergente foi recusada. A revisão correta encerrou só o registro escolhido, e a repetição conservou a nova revisão. Duas concessões do mesmo cliente e usuário continuaram respondendo por HTTP. A revogação pelo painel também foi confirmada. |
| Pedidos MCP 88 | Cada nova emissão e cada renovação emitem um token de acesso válido por 86.400 segundos e um de renovação válido por 7.776.000 segundos. `expires_in` vale 86.400. O vencimento deslizante usa o instante da troca. O diagnóstico interno de retenção usa os mesmos prazos. | O endpoint HTTP entregou os novos valores e o banco confirmou as duas durações. Na revogação da concessão de teste, o bearer ainda vigente recebeu HTTP 401 na chamada seguinte. O reuso de uma renovação consumida invalidou a família. O evento de manutenção compactou os tokens vencidos. Com o aviso de 14 dias e datas simuladas, o alerta permaneceu recuperado no dia 75 e abriu no dia 76. |

A listagem informa tanto o status armazenado quanto o acesso efetivo. Um registro histórico pode ter `status=active` e rótulo **Sem acesso** até o encerramento administrativo. A relação de migração fica no histórico. A aplicação da revogação seleciona o identificador exato sob a guarda da revisão. A verificação de validade na lista consulta as credenciais das concessões da página. O incidente de vencimento usa o prazo individual gravado, inclusive para tokens emitidos na 0.50.0.

## 4. Instalação e prontidão

A frota publica o instalador, confere o SHA-256 dos bytes servidos e chama `plugins/upload` com `expected_slug=wp-mcp-fator3`, o digest da seção 8, `overwrite=true` e `activate=true`. URL prevista após publicação pela frota:

`https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/wp-mcp-fator3-0.51.0-instalador.zip`

No Site-Teste, a transferência por partes conferiu tamanho e SHA-256 antes de aplicar `plugins/upload-base64`. O executor informou versão anterior 0.50.0, versão final 0.51.0, `active=true`, `applied=true` e `recovery_status=applied`. As sondas de página inicial e índice REST retornaram 200 antes e depois. Operação `e2b9c35816e5cd0fcb9ffd7525f8fbee`, pré-imagem `569cd95586085b3f59ed4443`. A leitura seguinte de `system/health` confirmou saúde, ferramentas prontas, marcador de cron ativo e zero recuperações pendentes. O ZIP temporário foi removido pelo executor. O estado de prontidão comercial de outros plugins tem verificação própria.

| Verificação | Resultado |
|---|---|
| Integridade | 481 arquivos no instalador, 474 PHP analisados. Três instalações locais contêm os mesmos bytes do ZIP. |
| Rotas MCP | Site-Teste devolveu HTTP 401 em ambas as rotas sem credencial. Em bancada, as duas devolveram 401 tanto sem credencial quanto com bearer inválido. A sonda do Site-Teste restringe o envio de Authorization. |
| Documentação instalada | A descoberta encontrou `system/guide`. O índice contém `release-0510`. As três páginas recebidas do Site-Teste recompõem os 2.373 bytes do documento, SHA-256 `868c596201e6244403d2808cbe1aa5e1b3066b60758e908e52cd57e53cf108e9`. Um ID desconhecido produziu recusa. Em bancada, sessão de editor, ausência de chamadas ao fornecedor e detecção de revisão documental obsoleta também foram testadas. |
| Painel | Sete abas avaliadas em 360, 768 e 1440 px, com mais três capturas do registro histórico. A largura do documento ficou dentro da janela nas sete abas. |
| Evidências | `evidencias/0510/` no fonte contém os resultados, os hashes, as capturas e a comparação dos contratos. A documentação passou em 203 verificações. O ensaio específico dos dois pedidos passou em 27 verificações. |

## 5. Banco, migração e correção por nova versão

A versão conserva o schema 2. A instalação preserva as datas existentes. Uma emissão cria os dois tokens e grava o instante de renovação e o novo vencimento da concessão na mesma transação. A revogação histórica atualiza a política do registro e marca as sessões ligadas a ele. Pré-imagens de pacote cobrem os arquivos. Restaurar arquivos não recompõe políticas, tokens consumidos ou concessões revogadas. Para restabelecer o acesso de uma concessão encerrada, use um novo consentimento. Uma correção de software após a implantação exige nova versão.

## 6. Pendências e responsáveis

- **Fator3Ventures, Pedidos MCP 87.** O site continuava na 0.50.0. A chamada autorizada ao ID histórico exato na revisão 1 devolveu `connection_invalid`. A releitura confirmou o mesmo estado armazenado e as duas concessões independentes ativas. Após a atualização pela frota, localizar o ID exato do pedido, reler a revisão, executar `connections/revoke`, confirmar `revoked=true` e `status=revoked`, e realizar uma chamada com cada um dos dois conectores independentes. As chamadas com duas credenciais distintas foram exercitadas em bancada. O teste de campo não forneceu prova de execução pelo conector Claude.
- **Site-Teste, Pedidos MCP 88.** A consulta agregada após a implantação ainda encontrou apenas os prazos antigos entre os tokens ativos. No primeiro uso de uma renovação existente, conferir o par do mesmo grant no mesmo segundo de criação usando apenas os campos `kind`, `created_at`, `expires_at` e a ligação interna com o grant. A diferença entre vencimento e criação deve ser 86.400 para at e 7.776.000 para rt. A aceitação de campo da revogação exige uma concessão descartável e uma chamada subsequente com o próprio cliente. A observação de uma concessão real alcançando a janela depende da última renovação e da política de aviso. No Site-Teste a política confirmou 14 dias. A recusa HTTP e a fronteira do dia 76 foram comprovadas na bancada.
- **Frota, Core 430.** Acompanhar os 11 sites por 24 horas para comparar as transições naturais do registro com as passagens de WP-CLI. A prova controlada já está encerrada no Core oficial.

## 7. Credenciais e configuração do dono

Os conectores existentes conservam suas credenciais e perfis. Uma renovação existente precisa ocorrer antes do vencimento já gravado. Após vencer, a retomada requer novo consentimento. Nenhum segredo de produção é necessário para verificar os prazos agregados. A bancada usou credenciais e contas sintéticas, com saída de correio bloqueada. No Site-Teste, a alteração permanente desta rodada é a atualização do canal e seus recibos normais. O fonte é entregue ao dono, conforme a regra central vigente para publicação pública da fonte.

## 8. Identidade dos arquivos

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-fator3-0.51.0-instalador.zip | 969301 | `d6016b33abbf3567c5c7c025e400d6ef4802b2adb4993b37bd8212b7e1042394` |
| wp-mcp-fator3-0.51.0-fonte.zip | 5529802 | `567bef18d2bdd4dd5a784c1dbde2e4f73f4db826e8f5e0a46622ca54bb0c0c7f` |

Digest do inventário de runtime: `32f90c2c61754f5a70114a5195f3b00a5b4ac3a451021b50ee710859f0385f56`. A compilação do instalador é determinística. O nome do relatório externo é `wp-mcp-fator3-0.51.0-relatorio.md`.

O instalador reconstruído a partir do ZIP fonte entregue produziu o mesmo SHA-256 do instalador acima.
