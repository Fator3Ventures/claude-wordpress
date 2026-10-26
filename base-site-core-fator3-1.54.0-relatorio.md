# Entrega — Fator3 Site Core 1.54.0

Data: 26/10/2026 (UTC). Base direta: 1.53.0. Contrato administrativo: 8.19.0. Pedido principal: 302, de 25/10/2026. Normas aplicadas: revisão 5, de 23/10/2026.

A implementação foi concluída, instalada e homologada no Site-Teste. O ciclo sintético de registro externo, vínculo de duas sessões, leitura, desfazimento e exclusão passou. A implantação na frota e a execução do caso real do CTO Office permanecem pendentes; não são declaradas como aceite concluído.

## 1. Bases aceitas

| Componente | Identidade aceita |
|---|---|
| Core 1.53.0 — instalador | 2574091 bytes; SHA-256 `086adf2530809c73d30d38ccb747b0a8de8c7cd7419543273c2e2c50940d99f1` |
| MCP 0.32.0 — instalador | 885606 bytes; SHA-256 `fd2097055383a26e6ca5b79b655f0b3740c337a42dab6ce2b43b4236c07496b1` |
| MCP 0.32.0 — fonte recebido | 4443847 bytes; SHA-256 `d7413eda5cae051c35c9f08f21a3e47cb9fc02e8e0d22462dd094b2cbf445c4e` |

Preservados slug e basename `base-site-core-fator3/base-site-core-fator3.php`, namespaces e identidades públicas. Cliente público Pipedrive do Core permanece no contrato 1.0.0. PHP mínimo 8.3.6 de 64 bits e WordPress mínimo 7.1.2 foram exercitados. Google 0.19.0, Meta 0.10.1, LinkedIn 0.10.1 e Pipedrive 0.1.0 são bases herdadas; não houve nova homologação integral de seus fornecedores.

## 2. Convivência e encaminhamentos

**Por que houve arquivo de impacto na 1.53.0:** o documento `base-site-core-fator3-1.53.0-impacto-wp-mcp-fator3.md`, revisão 2, registrava uma ação concreta no MCP 0.31.0: a redação indevida de regras booleanas cujo nome contém `token`, além da validação coordenada do correio. Não era requisito genérico de gerar mais um arquivo.

**Atendimento recebido:** MCP 0.32.0 preserva a política tipada e mantém redação de segredos. A suíte `mcp032-policy-1540.json` aprovou quatro verificações: regras/linhas, política tipada, contadores e senha redigida. A alternativa `linhas` permanece compatível. O escopo de sinais/contadores examinado está encerrado; isso não declara encerramento de outros impactos históricos.

**Defeito devolvido pelo MCP ao Core:** `wp-mcp-fator3-0.32.0-impacto-base-site-core-fator3.md`, revisão 1, de 25/10/2026, pediu alinhar a permissão declarada à permissão efetiva do correio. Atendimento nesta versão, responsável Core:

| Ability | Permissão declarada e efetiva |
|---|---|
| `email-enviar` | `f3base_enviar_email` E `f3base_ler_leads` |
| `email-registros-ler` | `f3base_ler_leads` |
| `email-caixa-consultar`, `email-reprocessar` | `manage_options` E `f3base_ler_leads` |
| `email-caixa-verificar` | `manage_options` |

A infraestrutura de registro aceita callback específico sem mudar os demais chamadores. As verificações dentro da execução foram preservadas. O decorador real MCP 0.32.0 recusou prévias e recibos incertos em cache após revogar cada capacidade, recusou chave nova e perfil de leitura, sem SMTP. Evidências: `permissions-native-1540.json` (21 verificações) e `permissions-mcp032-1540.json` (26).

**Resultado:** correção solicitada ao Core atendida e retestada. Não foi identificada nova alteração necessária no MCP para o pedido 302; nenhum novo impacto é emitido nesta rodada. Os 464 arquivos da cópia MCP usada são iguais ao instalador recebido. Nenhum runtime de outro plugin foi alterado. Relatório/impacto recebidos ficam em `inputs/1540`; o encaminhamento anterior fica no histórico.

## 3. Pedido 302 — mudanças e evidências

| Item | Comportamento entregue | Prova |
|---|---|---|
| (a) Contato externo | `f3base/contato-externo-registrar`, simulação padrão, chave idempotente, método, identidade, empresa, primeiro contato com fuso, origem declarada e link. Nenhuma notificação, e-mail automático ou conversão. CRM opcional. | 69 verificações de fluxo e privacidade; 14 verificações CRM |
| (b) Vínculo manual | `f3base/contato-sessao-vincular`, lote, simulação, revisão obrigatória, executor autenticado, decisor declarado, data e motivo cifrados; mesma rota desfaz. | Duas sessões, conflitos, classe de tráfego, propriedade, lote inválido, desfazimento e auditoria |
| (c) Leitura e relatórios | Jornada e detalhe mostram vínculo manual separado dos fatos observados. Aquisição e conteúdo aceitam `tipo_atribuicao`. Não há conversão retroativa. | Leituras, recortes todas/manual/observada, contagens e eventos originais preservados |
| (d) Dados pessoais e exclusão | Identidade, origem, referência CRM e auditoria cifradas no contato. Índice de vínculos só contém identificadores, classe e instante. Exclusão remove os vínculos. | Ausência de dados pessoais em colunas abertas/sessões/eventos; exportador e apagador nativos; exclusão em cascata |
| (e) Relatório | Casos, resultados, limites e pendência real documentados neste relatório. | Evidências sanitizadas no fonte |

### Registro e efeitos

São aceitos whatsapp, telefone, email, presencial e outro. Para whatsapp/telefone/email exige-se telefone ou e-mail; presencial/outro admite identidade sem endereço. A data RFC3339 deve conter fuso, representar um calendário válido e não estar no futuro. A origem usa `canal`, `parceiro`, chaves UTM existentes e `link_referencia`. Ela é declarada, não inferida da visita.

A simulação não grava contato, não acessa fornecedor e não devolve dados pessoais no recibo do transporte. Na gravação, a identidade e a chave são protegidas por HMAC; repetição não duplica, conteúdo diferente conflita e contato eliminado não é recriado pela chave antiga. As colunas abertas nome/email/pagina ficam vazias e sessao fica nula. A consulta autorizada faz projeção em memória; busca exata por e-mail usa índice HMAC.

A opção Pipedrive `vincular_existente` confirma o UUID por GET na conta verificada e cifra a referência. Não cria lead, pessoa, nota, atividade ou fila. Apagar o registro local não apaga o lead preexistente. A opção `entregar` exige chave configurada de `mapa_pontos`; persiste a intenção com o contato e usa fila durável. Configuração removida posteriormente exige revisão. Contato de teste só entrega com homologação ativa. O transporte CRM foi simulado; nenhum lead real foi criado nesta validação.

### Vínculo, privacidade e cobertura

As novas rotas exigem conjuntamente `manage_options`, `f3base_ler_leads` e `f3base_gerir_leads`. Uma sessão manual só pertence a um contato; sessões desconhecidas, ambíguas ou de outra classe são recusadas. O lote usa transação InnoDB no mesmo handle, revisão bloqueada e auditoria cifrada. Perda de confirmação do commit retorna persistência indeterminada, sem fingir sucesso ou repetir a escrita automaticamente.

Limites explícitos: 1–20 sessões por lote, 100 vínculos ativos e 500 alterações por contato. Jornada manual: dez sessões por página, até 500 eventos de análise por sessão, com sinal de corte e consulta de sessão para detalhamento. Revogação conhecida impede exibir eventos revogados. Desfazer não depende da retenção dos eventos.

O filtro `observada` seleciona sessões sem vínculo manual ativo; `atribuicao_manual`, as que possuem vínculo; `todas` conserva a cobertura anterior. Canal e conteúdo continuam agrupados pelos fatos observados, sem substituir o canal pela origem declarada ou contar a mesma sessão duas vezes. Agregados expirados e robôs sem identidade de sessão ficam fora dos recortes filtrados, com aviso de cobertura. Busca parcial por nome/telefone não abre o acervo cifrado.

No MCP 0.32.0, **use chaves distintas para simular e gravar**: o transporte inclui `simular` no conteúdo idempotente. Repetições de gravação mantêm a mesma chave e parâmetros. O Core nativo não consome a chave na simulação. Essa diferença está documentada e coberta por oito verificações integradas, incluindo recibo sem dados pessoais e recusa após exclusão.

### Matriz de validação

| Ambiente/suíte | Resultado |
|---|---|
| WordPress 7.1.3, PHP 8.3.6, MySQL 8; Core isolado | 302: 69; CRM: 14; permissões: 21 — aprovadas |
| Mesmo laboratório com MCP 0.32.0 real | Permissões: 26; fluxo 302 no canal: 8; política de sinais: 4 — aprovadas |
| Regressões próprias | Correio/estado: 27; correio/transportes: 19; correio/CRM: 38; formulários: 32; Pipedrive: 39 — aprovadas |
| Documentação instalada | 851 verificações; 116 documentos, 593 páginas — aprovadas |
| WordPress mínimo 7.1.2, PHP 8.3.6 | Instalação, 302/69, CRM/14, permissões/21, documentação/851 — aprovadas |
| Instalação limpa e upgrade nativo 1.53.0 → 1.54.0 | Instalador final, estruturas prontas, configuração/dados preservados, migração repetida sem efeito |
| Site-Teste WordPress 7.1.3, PHP 8.3.36 | 302/69, CRM/14, permissões/21 e documentação/851 — aprovadas em fixture isolada |
| Sintaxe PHP | 530 arquivos do instalador aprovados |

Os testes de fornecedor são mocks de transporte; WordPress, banco, callbacks, filas e decorador MCP indicados são reais. Não houve SMTP/IMAP real, Slack, conversão de anúncios ou registro de contato real. As contagens por suíte não representam casos únicos somáveis. O controlador Site-Teste retorna as 21 permissões em stdout; as asserções detalhadas correspondentes constam da evidência nativa local.

## 4. Instalação, prontidão e documentação

Site-Teste: atualização efetiva de 1.53.0 para 1.54.0, plugin ativo antes/depois. Backup do pacote: `6f5d76f7a8d70939e6feed33`; operação: `84ea3961aa74bbe32f7541edf42fd24a`. Probes da home e REST responderam 200 antes/depois em requisição PHP nova com nonce assinado. Essa é prova interna de mesma origem, não disponibilidade externa independente.

Prontidão final do Core: `ok=true`, `estado=concluida`, zero falhas, contrato 8.19.0 e 153 abilities. Os 716 arquivos instalados correspondem ao runtime do ZIP final. Manifesto ordenado SHA-256: `ec620d3d0b38ad73c27e5fc03fafea4a604b600e9f1711a56f5f296ea5383dab`. Opções lidas pelas telas permaneceram iguais; correio e envio continuaram desligados. As duas novas rotas foram descobertas pelo MCP real com simulação padrão.

A homologação copiou o Core instalado para tabelas e diretório temporários exclusivos no Site-Teste, sem tocar os contatos compartilhados. Limpeza confirmada: 71 tabelas removidas, zero remanescentes, diretório e manifesto removidos. Controlador e ZIP de transporte removidos; probes finais aprovados. Nenhum mecanismo de teste foi incluído no instalador.

Guias correntes incluem `CONTATOS-EXTERNOS-1.54.md`, `AGENTES-1.54.0.md` e `RELEASE-1.54.0.md`. Inventários, schemas, contratos e índice documental foram regenerados. Documentos correntes foram lidos integralmente pela ability documental com paginação, hash e verificações de permissão; os schemas públicos novos também foram lidos no conector Site-Teste.

## 5. Banco e reversão

Migração aditiva: tabela `<prefixo>f3base_contato_sessoes`, registrada no inventário de instalação/desinstalação; armazenamento cifrado e índice HMAC no registro existente do contato. Nenhuma migração copia identidade para eventos. Formulários, visitas, configurações e filas existentes são preservados.

A troca do ZIP não reverte automaticamente dados. Para rollback completo, usar fotografia coerente de arquivos e banco com o procedimento vigente de pausa/esvaziamento das filas; contato e índice devem ser restaurados juntos. A versão anterior não entende a funcionalidade nova, portanto não operar esses registros após simples downgrade. Não houve rollback no Site-Teste.

## 6. Pendências e sequência da frota

O caso real fornecido pelo dono, no CTO Office, **não foi executado**. A consulta disponível indicou Core 1.52.1 e MCP 0.30.1, ainda sem estas rotas. O aceite da frota fica com o responsável pela implantação e pelo registro operacional:

1. Publicar/implantar o instalador conforme a regra da frota, validar SHA-256 e slug e confirmar prontidão.
2. Confirmar um telefone/e-mail do contato a partir de fonte autorizada. O número de WhatsApp citado no pedido pode ser o destino comercial, não prova de que pertence à pessoa; não foi atribuído a ela.
3. Simular e registrar a conversa na data/hora fornecida, com origem declarada e `pipedrive.acao=vincular_existente`, usando o UUID original do lead. Confirmar que não houve criação remota.
4. Simular e aplicar o vínculo das duas sessões indicadas pelo dono, com revisão atual, decisor e motivo; ler jornada e ambas as sessões, mantendo a atribuição observada.
5. Confirmar ausência de filas/notificações/conversões inesperadas e registrar o aceite em evidência privada.

Identificadores e dados pessoais reais não foram copiados para este relatório distribuível ou para as fixtures. As provas locais e Site-Teste não substituem esse aceite real. Testes de entrega em fornecedor e de caixa de e-mail real continuam fora desta rodada.

Conforme a norma, os artefatos são entregues ao dono; a frota publica instalador/relatório na raiz raw do repositório público e confere hash antes de upload, com `expected_sha256` e `expected_slug`. Não houve push. O fonte permanece privado até decisão do dono.

## 7. Credenciais e estado final

Nenhuma credencial ou token é necessário para reproduzir as suítes simuladas. O controlador temporário reutilizou internamente a conexão do WordPress apenas para tabelas isoladas, sem incluí-la na evidência; foi removido. Usuários, senhas de aplicativo e contatos de teste são descartáveis. A entrega não contém banco, cookies, credenciais ou logs pessoais. A operação real de CRM exige configuração já verificada no site; seus valores não são expostos.

## 8. Artefatos finais

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| `base-site-core-fator3-1.54.0-instalador.zip` | 2587117 | `c3542b4c293b46357d013abb05e6f302611fe8392d01dd85ceb330fe2b6b66a7` |
| `base-site-core-fator3-1.54.0-fonte.zip` | 3642476 | `0e691e0fa05c9575464cd107ded05e577a3611c5189dde6dfcddad916b8b8145` |

Relatório canônico: `base-site-core-fator3-1.54.0-relatorio.md`. Somente o instalador é instalável; sua raiz é o slug sem versão. O fonte contém o mesmo runtime byte a byte, build, testes, evidências sanitizadas, normas, entradas e histórico, sem ZIPs internos. A cópia do relatório dentro do fonte é explicitamente anterior ao fechamento; a identidade final do fonte consta apenas no relatório externo, evitando circularidade.

Reprodução em `build/README.md` e `build/COMPANIONS.md`. O instalador foi fechado antes da homologação final e permaneceu inalterado.
