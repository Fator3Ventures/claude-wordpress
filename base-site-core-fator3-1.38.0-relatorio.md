# Entrega — Fator3 Site Core 1.38.0

Revisão 1 · 19/10/2026 · Rodada: implementação · Status: com-pendencias.
Slug: base-site-core-fator3 · Basename: base-site-core-fator3/base-site-core-fator3.php.
Código implementado e validado no escopo abaixo; homologação Pipedrive em produção pendente.

## 1. De onde esta versão entra

Instalação limpa e atualização direta da 1.37.0, sem versão intermediária. Base desta conversa conferida: SHA-256 a7cd1c225bb9de76a5d1c3ad4b2184df47a6270856da902b8a268a4105ad20ad. A base não foi alterada.
Requisitos executados: WordPress 7.1.2, PHP 8.3.6 64 bits, MySQL 8.0.36-2ubuntu3. Instalação isolada no laboratório, sem acompanhantes, com fixture MU bloqueando transportes externos. Padrões/instruções r4 de 16/10 e Pedidos Core(5) lidos.

## 2. Convivência e encaminhamentos

Contrato administrativo **8.3.0**, aditivo à 8.2.0. **65 options operáveis**, **68 entradas no contrato**, **130 abilities**, entrada/saída zero. Perfil **piso-padrao-3.5**, revisão 2026-10-12-core-1.31.0. SDKs site-measurement-context/1.0.0 e site-conversion-purposes/1.0.0 e schemas preservados byte a byte. Nenhuma nova option, tabela ou ability; f3base_pipedrive recebe whatsapp_texto e os mapas aceitam whatsapp_link.

Site-Teste: MCP 0.24.0, Google 0.11.0, Meta 0.3.0, LinkedIn 0.3.0, DreamHost 1.0.0, WP Super Cache 3.1.4, Yoast 28.7, ativos antes/depois e não modificados. Prova de convivência: bootstrap, operação Core, MCP documental e Slack; não equivale a testar todas as funções dos acompanhantes.

| Destinatário | Versão examinada | Classificação / situação | Referência | Impacto |
|---|---|---|---|---|
| implantador-base | 2.9.0 citado no pedido; runtime não fornecido | validacao-coordenada / aceite externo pendente | Pedidos core 227–229 | base-site-core-fator3-1.38.0-impacto-implantador-base.md r2 |

MCP, Google, Meta e LinkedIn: fronteiras públicas mantidas, sem impacto técnico adicional identificado nesta rodada. Impacto do Implantador preparado antes da implementação e atualizado nesta entrega. Não enviado; outro pacote não foi modificado. O encaminhamento anterior 8.2 não é declarado concluído pelo Core.

## 3. Mudanças e evidência

| Pedido | Mudança | Prova e limite |
|---|---|---|
| 227 | AGENTES-1.36.0.md corrigido para config-core-escrever; CONFIGURACAO.md para piso-padrao-3.5. Sem alias. | Leitura integral paginada via MCP após instalação, hashes idênticos aos arquivos do ZIP. |
| 228 | Quatro campos de confirmação, tempo esperado e observado na seção 4. | Consulta real f3base/como-usar. |
| 229(a–c) | Regra única C1/wa.me; principal Slack com telefone clicável, linha WhatsApp na thread/resumo/e-mail/nota; fixos sem link. | 45 checks específicos e Slack real: celular na principal/Contato, fixo sem link, fallback legível. |
| 229(d) | Nota C1 WhatsApp/Reenvio; mapas opcionais whatsapp_link para lead e pessoa com catálogo textual. Pessoa existente só enriquece campo vazio, com confirmação. | Fluxo Pipedrive simulado em WordPress: payloads, enriquecimento, repetição e preservação. Prévia MCP real com nota e C1. Aceite CRM real pendente. |
| 229(e) | Segunda etapa usa telefone novo mesmo com resumo inicial congelado; linha em nova parte e nota complementar. | Fixture nativa verifica apresentação e renderizadores Slack/HTML; etapa 2 real não enviada nesta rodada. |
| 229(f–g) | f3base_pipedrive.whatsapp_texto vazio por padrão, variáveis nome/empresa/unidade e URL encoding. Marcas/supressões e exclusão de clique sem formulário preservadas. | Fixtures de modelo, tipos, catálogo, autorização e supressões; visitante dos testes reais suprimido, nenhum CRM enfileirado. |

Detalhes em docs/WHATSAPP-1.38.md. Links maiores que o campo CRM são omitidos integralmente; o texto pré-preenchido interpolado é limitado a 1700 bytes codificados, preservando caracteres e URL completa. Não verifica existência da conta WhatsApp. Novas apresentações/entregas usam a configuração; atualização não reabre filas nem reescreve mensagens antigas.

## 4. Instalação e prova da troca

Site-Teste: https://fator3-teste-mcp-1.dreamhosters.com/. Upload privado por files/upload-create/part/finalize, hash remoto conferido; plugins/upload-base64 com overwrite=true, activate=true, expected_slug=base-site-core-fator3 e SHA-256 da seção 8. Operação 60bdcc0d125691e3087a72ae, reativação silent_reactivation em PHP independente. Sondas home/REST 200 antes/depois, origem interna. Acesso HTTP externo à página de teste também 200.

Publicação raw não realizada. Destino convencional, ainda não publicado por esta rodada: https://raw.githubusercontent.com/Fator3Ventures/claude-wordpress/main/base-site-core-fator3-1.38.0-instalador.zip. Frota deve publicar e comparar bytes servidos antes de distribuir; o teste desta rodada usou o ZIP privado idêntico.

**Prova de confirmação:** f3base/como-usar com `{"compacto":true,"incluir":["saude"]}`, campo atualizacao:

| Campo | Observado |
|---|---|
| versao_alvo | 1.38.0 |
| estado | concluida |
| falhas | 0 |
| confirmada_no_executor_em | 1792379791 — 19/10/2026 00:16:31 −03 |

15 etapas concluídas. Tempo esperado para planejamento: **2–6 minutos após upload**, baseado na observação da frota da 1.37 (fonte recebida), sujeito a cron/hospedagem. **Observado nesta instalação: 113 segundos desde a solicitação do upload**, e 74 segundos desde iniciado_em=1792379717. Finalização natural, sem adiantar relógio remoto.

| ID | Ambiente / cenário | Resultado | Evidência | Limite |
|---|---|---|---|---|
| LINT | PHP 8.3.6 | 212 arquivos válidos | installer.json | Sintaxe |
| NAT | WordPress real descartável | 234 checks aprovados | comercial-1370 (56), whatsapp-1380 (45), contracts-1380 (9), pipedrive-flow-1380 (39), docs-1380 (68), slack-retorno-1370 (17) | Fornecedores simulados |
| CYCLE | Limpo e 1.37→1.38 via Plugin_Upgrader | Ambos aprovados; preservação/idempotência | native-cycles.json, SHA do ZIP final | Espera adiantada só no laboratório |
| MCP | Documentos e contrato instalados | 8.3.0, 65 operáveis; hashes conferidos | site-teste-1380.json | Admin autorizado; recusa anônima/confinamento testados localmente |
| SLACK | Dois envios reais marcados teste | 7 mensagens celular e 6 fixo; conformidade remota confirmada | f3base/avisos-slack-verificar; site-teste-1380.json | Não comprova leitura humana |
| CLEAN | Apenas recursos sintéticos da rodada | 13 mensagens ausentes após exclusão, dois contatos eliminados | Limpeza Slack 345e2e72468b0745b0417dbd | Históricos de auditoria/execução permanecem |

Índice docs/DOCUMENTACAO.md; schema real de f3base/documentacao-ler, arquivo/linha/limite até200, proxima_linha até nulo, versão/hash estáveis. WHATSAPP-1.38, AGENTES-1.38.0, RELEASE-1.38.0 e ambos os guias do 227 lidos no site. Nenhuma credencial revelada. Instalador corresponde byte a byte à árvore testada.

Estado final: Core 1.38.0 ativo, acompanhantes preservados. Pipedrive do Site-Teste segue desativado. Não se alteraram configurações comerciais ou destinos. Sem contatos/mensagens sintéticos remanescentes; arquivos privados de pacote/backup preservados para recuperação.

## 5. Banco e volta de versão

Sem mudança estrutural: marcador de estrutura 1.35.0 preservado; ciclo de instalação 1.38.0. Completar padrões acrescenta whatsapp_texto vazio; mapas/escolhas/dados/cursor/credenciais sintéticas preservados no upgrade. Projeção de apresentação passa a versão5, guardada cifrada no mecanismo existente. Jobs mantêm locks/checkpoints/deduplicação; atividades já existentes não são recriadas.
Backup do banco antes da instalação: artifact_id 4e77bd8a784075924a29c106241949bb, 17305327 bytes, SHA-256 c640ad192d1ed75291fa9bdb6fcc0176a281be8251654da7c6efbdcad9c680ef. Privado, recuperável pelo MCP; bytes não baixados/incluídos. Backup de arquivos: d2d5f542f1aa49eed9b2329d.
Restaurar arquivos1.37 não apaga efeitos de API, notas, campos ou banco. Se necessária reversão integral, pausar fluxos, preservar diário e avaliar backup consistente; não foi exercitada volta de versão. Configuração nova desconhecida pela1.37 deve ser avaliada antes de gravações nessa base.

## 6. O que permanece pendente

- **Pipedrive real:** CTOoffice consultado nesta rodada segue1.37.0. Publicação/distribuição1.38 cabe à frota. Depois da troca e dos mapas da conta, projeto Pipedrive/frota deve homologar nota do lead/C1 clicáveis e remover registros sintéticos, usando homologacao=true só durante teste; restaurar opção ao final. Nenhuma produção foi atualizada ou recurso CRM real criado nesta rodada.
- **Implantador:** responsável valida contrato8.3.0 no runtime2.9.0; fonte não fornecido. Impacto r2 entregue.
- **Navegador/admin:** editor visual completo não foi exercitado; preservação do mapa na troca de seleção LinkedIn implementada e revisada em código. Complemento etapa2 e texto predefinido foram testados nativamente, sem envio real adicional.
- Frota: publicar raw, conferir hash servido e decidir rollout. Retorno/aceites comerciais históricos da1.37 continuam sob seus responsáveis.

## 7. Credenciais e configuração do dono

Nenhuma credencial nova para montar links. Configuração: Ferramentas → Fator3 Site Core → Integrações → Pipedrive; whatsapp_texto opcional, pais_telefone e mapa_campos.whatsapp_link/mapa_pessoa.whatsapp_link. Usar chaves reais de campos textuais no catálogo da conta; preferir texto longo se houver mensagem predefinida. Exige manage_options. Contrato/leitura/escrita: f3base/config-core-contrato-v1, config-core-ler e config-core-escrever com revisão/simulação.
Entrega Pipedrive exige token existente, domínio, responsável, catálogo e atividade habilitada; Slack usa bot/canal configurados, chat:write e escopo de leitura apropriado para verificar thread. Não houve alteração de token/escopo. Contato sintético não autoriza gasto Ads ou envio ao visitante; testes deste trabalho tiveram resposta ao visitante suprimida.

## 8. Identidade dos arquivos

| Artefato | Nome final e link | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | [base-site-core-fator3-1.38.0-instalador.zip](base-site-core-fator3-1.38.0-instalador.zip) | 1993463 | `1b0de25e1dd4276fe7f7d8e428dfc0eb01a249d4108f680aa65bd3a4de3e59ee` |
| Fonte | [base-site-core-fator3-1.38.0-fonte.zip](base-site-core-fator3-1.38.0-fonte.zip) | 2131485 | `ccaadfd063b4ca803db5988db54a7f78b8a6325ac44fb349b54b6285333fc87d` |

Relatório externo canônico. Cópia no fonte identificada como anterior ao fechamento; hash/tamanho finais do fonte preenchidos somente aqui. Complementos: plano1.38 r2 e impacto implantador-base r2. Nenhum ZIP contém outro ZIP, banco de laboratório, runtime ou segredo real.
