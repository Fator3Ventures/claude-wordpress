# Entrega — Fator3 Site Core 1.55.0

26/10/2026. Horários em America/Sao_Paulo (UTC−03). Implementados os pedidos 303–306 sobre a 1.54.0, preservando o pedido 302. Instalador final ativo no Site-Teste, atualização concluída e confirmada pelo executor. Aceites externos de e-mail e da frota continuam pendentes conforme seção 6.

## 1. Bases e identidade

Normas: instruções de agentes e padrão de desenvolvimento, revisão 5 de 23/10/2026, em inputs/1510. Cópias antigas de revisão 4 não as substituem. Escopo recebido: “Fator3 Site Core”, atualização de 26/10/2026, pedidos 303–306; síntese em inputs/1550/plano.md.

| Base | Bytes | SHA-256 |
|---|---:|---|
| Core 1.54.0 instalador | 2587117 | c3542b4c293b46357d013abb05e6f302611fe8392d01dd85ceb330fe2b6b66a7 |
| Core 1.54.0 fonte | 3642476 | 0e691e0fa05c9575464cd107ded05e577a3611c5189dde6dfcddad916b8b8145 |
| MCP 0.33.0 instalador | 888204 | f16ee3e31e4143ffb42c566ea6da4f2da81d3771a01a0f90b5d34e3d02ac8caa |
| MCP 0.33.0 fonte | 4585261 | fdef8375bd72533062dff506be52664057619655e948afa3b89e22d4114e2ed6 |

Slug/basename preservados: base-site-core-fator3/base-site-core-fator3.php. Versão 1.55.0; contrato 8.20.0; 153 abilities; inventários com 147 opções, 59 tabelas e 11 famílias de transients. Mínimos preservados: WordPress 7.1.2/PHP 8.3.6 de 64 bits. Testados também WordPress 7.1.3/PHP 8.3.6 e Site-Teste WordPress 7.1.3/PHP 8.3.36.

## 2. Convivência e impactos

Os pedidos pertencem ao Core. Nenhum acompanhante foi alterado. MCP original 0.33.0: 26 verificações de permissões com decorador real, cinco de política tipada e oito regressões do contrato 302, além da leitura integral da documentação. Revogação impede reaproveitar recibos de prévia/incerteza; perfil somente leitura não escreve.

O arquivo de impacto anterior comunicava a fronteira de permissões de e-mail entre produtor e MCP. A correção do produtor foi entregue no Core 1.54.0; o relatório recebido do MCP 0.33.0 encerra o ponto. Esse encerramento fica neste relatório. Não há pedido técnico novo ao MCP nem novo arquivo de impacto.

No Site-Teste permaneceram ativos MCP 0.33.0, Google 0.19.0, Meta 0.10.1, LinkedIn 0.10.1 e Pipedrive 0.1.0, sem mudanças de versão. Convivência de carregamento confirmada; não equivale à homologação integral de seus fornecedores. Cliente Pipedrive público do Core preservado no contrato 1.0.0; testes CRM com transporte simulado.

## 3. Pedidos e evidências

### 303 — Sessão administrativa

Adicionada f3base_sessao_admin_dias, inteira 1–365, padrão 365, persistida e disponível na tela e config-core-ler/config-core-escrever. auth_cookie_expiration recebe três argumentos e só aplica a opção com remember=true/manage_options. Vale no próximo login; não estende tokens existentes. Sem Lembrar-me permanece cookie de navegador. Logout, senha e salts conservam a revogação nativa.

A premissa de que o Core não alterava sessões diverge da base: já existia f3base_sessao e o Site-Teste tinha política legada de 90 dias. Ela foi preservada para outros usuários. Os 14 dias nativos foram comprovados com a política legada desligada na fixture; a preservação dos 90 dias foi testada separadamente. Não houve migração silenciosa das demais contas.

Validade assinada do cookie/token: 365 ou 30 dias; expiração física do cookie persistente inclui a tolerância nativa de 12 horas do WordPress. Sem Lembrar-me: Expires=0 e validade interna nativa de dois dias. Nenhuma alteração dessa semântica.

24 checks passaram em laboratório atual, mínimo e Site-Teste isolado: valores/limites, capacidades, cookies/tokens e revogação. Leitura real confirmou a opção persistida em 365. Provas em evidence/1550/request-303.json, minimum/request-303.json, site-request-303.json e site-admin-session.json.

### 304 — Autenticação própria de e-mail

Sem Authentication-Results explicitamente confiável, o Core verifica DKIM sobre os bytes brutos, SPF com Return-Path/IP da fronteira Received confiável e alinhamento/política DMARC. mx_confiaveis é configurável, padrão *.dreamhost.com. Cabeçalho forjado não concede aprovação nem descarte.

DKIM: RSA-SHA256/Ed25519-SHA256, simple/relaxed, corpo integral e From assinado; recusa assinatura parcial, SHA-1, From ambíguo e adulteração. SPF tem limites de termos/consultas vazias. DMARC usa descoberta organizacional limitada conforme RFC 9989, com p/sp/np. DNS do host por UDP/TCP, oito segundos/64 consultas, cache positivo máximo de 300 segundos e negativo de 30; falha temporária não comprova ausência de política.

DMARC pass aceita; fail com reject/quarantine descarta conforme pedido; sem DMARC aceita somente DKIM/SPF alinhado comprovado; demais casos ficam suspeitos. Método/resultado ficam no payload cifrado lido por email-registros-ler. Descarte conserva apenas identidade técnica e resultado mínimo cifrado.

DNS indisponível gera suspeito/autenticacao_pendente, sem contato, CRM, Slack ou aceite automático. Até duas pendências são reavaliadas antes de mensagens novas, dentro do limite total da passagem, sem voltar cursor. A mensagem fica na INBOX para revalidação; ausência posterior vira autenticacao_ausente. Exportação, apagamento, retenção e restauração cobrem pendências sem contato; tombstones evitam reimportação.

38 checks de criptografia/SPF/DMARC/DNS passaram nos três ambientes, incluindo assinatura independente PHPMailer, adulteração, cabeçalhos forjados, reject/quarantine, DNS indisponível e Ed25519. Pipeline/privacidade também exercitados na suíte 305. DNS real resolveu gmail.com e _dmarc.gmail.com no servidor. Essa resolução não equivale ao recebimento Gmail, ainda pendente.

### 305 — IMAP, coleta e classificação de teste

LIST/NAMESPACE resolvem prefixo/separador e nomes curtos/completos sem duplicar INBOX. email-caixa-verificar simula por padrão e informa ausências/nomes efetivos; simular=false cria e reconfirma com LIST, sem importar/mover ou alterar cursor. A coleta aplicada garante os destinos. MOVE continua obrigatório, sem fallback DELETE/EXPUNGE.

Busca por UID acima do cursor com INTERNALDATE >= ativado_em como instantes. SINCE por dia UTC foi removido: podia excluir UID 1 na virada da data do servidor antes do filtro preciso. Date do cabeçalho não define ativação. UIDVALIDITY divergente continua interrompendo. O critério aparece na leitura.

Assunto iniciado por [TESTE F3BASE] ou From em remetentes_teste marca teste, fora dos relatórios normais, CRM somente em homologação e aviso elegível à exclusão de testes. Não enfraquece autenticação. Referências/e-mail não fundem contatos comerciais com testes; não há reclassificação retroativa automática.

Dez checks de protocolo e 26 de pipeline passaram nos três ambientes: UID 1/virada de data, prefixo/criação/falha, idempotência, pendência/retomada, classificação, exclusão de aviso com Slack simulado, privacidade e retenção.

IMAP real: INBOX., separador ponto, INBOX.Importados/INBOX.Sent já existentes pela intervenção anterior da frota. Duas pastas próprias aleatórias foram comprovadas ausentes, criadas pelo cliente Core e removidas vazias. Identidade INBOX, configuração e cursor preservados; nenhuma mensagem lida/enviada nesse teste. A primeira limpeza da fixture perdeu conexão ao eliminar uma pasta selecionada; corrigida para selecionar INBOX antes de DELETE, limpou o resíduo e passou integralmente. Nenhuma alteração do produto. Provas site-imap.json/site-providers.json.

Caixa vazia, UIDNEXT 1. Ainda não há prova de mensagem externa nova importada/movida pelo cron real nem de aviso Slack real apagado nesta rodada.

### 306 — Último sucesso de cache e robots

Corrigidos wrappers que descartavam o retorno dos módulos. ultimo_sucesso só avança com prova nova, persistida e confirmada, usando código/escopo da evidência. Cache exige perfil ativo, HIT/cabeçalhos, tokens e proteção do artefato; robots exige HTTP correspondente. Recuo, trava, cache desligado e falha HTTP preservam sucesso anterior e registram motivo. Saúde/tela mostram prova pública e data ao lado.

Nove checks passaram nos três ambientes. No Site-Teste compartilhado, o cron HTTP real confirmou, sem forçar a confirmação:

| Tarefa | Prova em 26/10/2026 | Último sucesso | Código / escopo |
|---|---|---|---|
| Cache | 01:57:36, HIT e proteção confirmados | 01:57:40 | cabecalhos_comprovados / cache_http_confirmado |
| Robots | 01:57:20, HTTP 200 e hashes iguais | 01:57:21 | robots_http_confirmado / robots_http_confirmado |

Provas site-health.json/site-request-306.json. Cache desligado foi testado no ambiente isolado do próprio Site-Teste; o compartilhado permaneceu ativo. A fixture CLI foi ajustada para reproduzir HTTPS. O runtime não mudou após o fechamento do instalador.

### 302 — Contato externo e vínculo preservados

Regressões: 69 checks de registro/simulação/idempotência, vínculo/desfazimento com revisão/auditoria, jornada/sessão, filtros por atribuição, PII cifrada, eliminação com vínculos e ausência de conversões; 14 de CRM opcional/vínculo existente e oito pelo MCP. Sem lead comercial, e-mail, Slack ou conversão reais gerados pelos testes.

O documento recebido informa que o caso Marcela na CTO Office já foi executado pela frota na 1.54.0. Trata-se de evidência recebida, não nova consulta desta rodada. Contato/vínculos reais não foram repetidos.

## 4. Instalação, testes e prontidão

ZIP final: 534 PHP sem erro de sintaxe. Instalação nova e upgrade direto 1.54.0 → 1.55.0 passaram em WordPress 7.1.2 e 7.1.3/PHP 8.3.6, preservando dados, preferências, credenciais cifradas, cursor e procedência; repetição idempotente. Espera acelerada só nos bancos descartáveis. No Site-Teste, confirmação pelo executor real.

107 checks dos pedidos novos e 335 regressões de 300/301/302, formulários e Pipedrive passaram. Documentação: 860 verificações, 117 documentos, 597 páginas, leitura integral/hash, catálogo/confinamento; provas nativas, com MCP e isoladas no servidor. Leitura remota real de docs/OPERACAO-1.55.md confirmou o SHA-256 local. Permissões nativas: 21 checks; MCP: 26. Nomes históricos de suítes identificam origem; JSON informa versão efetivamente testada.

Site-Teste: início 01:56:51; 17 etapas terminadas 01:56:54; executor confirmou 01:58:01, estado concluida/zero falhas. Backup anterior 437aa46112fe81b162b01552; operação cbeffe0787ee01798e7d83b98ab07c0f. Os 721 arquivos instalados coincidem com o runtime local; manifesto SHA-256 ec7b09b465d7d25d4ba99d7e5db90605ad44d980b472aa2e001616b1260472db.

Home/REST HTTP 200 nas sondas internas antes/depois e após remover o controlador. São provas de mesma origem, não de rede externa. Recuperação core_operacional/pausado=false. Telas renderizadas, opções preservadas, recepção habilitada e envio automático desabilitado como antes.

Limpeza: dois laboratórios remotos, 71 tabelas próprias removidas em cada, diretório/manifesto eliminados; pastas IMAP próprias eliminadas; controlador e ZIP temporários apagados. Backups auditáveis do MCP mantidos. QA não entra no instalador. Apto no escopo comprovado; aceite externo completo depende da seção 6.

## 5. Banco e reversão

Sem DDL novo. Nova opção/subcampos aditivos, payload cifrado com autenticação/teste e estados na coluna existente. Credenciais, listas vazias deliberadas, ativado_em e cursor preservados. Cache DNS transitório sem mensagem/PII.

Reversão coordenada por backup conforme OPERACAO-E-RECUPERACAO.md. Antes de voltar à 1.54.0, desligar coleta e reconciliar autenticacao_pendente/autenticacao_ausente: a base não reavalia esses estados. Não copiar dados/credenciais de laboratório. Alterar duração não revoga sessões existentes; usar os mecanismos nativos quando necessário.

## 6. Pendências explícitas

1. Receber na caixa de homologação um Gmail real e uma mensagem controlada com From de domínio reject por servidor não autorizado; comprovar aceitação/descarte/método. Não havia mensagens nem conta Gmail conectada utilizável. DNS indisponível e mensagens assinadas/adulteradas passaram em fixture, sem substituir o ensaio externo.
2. Observar mensagem externa nova [TESTE F3BASE] coletada/movida pelo cron real e exclusão do aviso real. Caixa vazia e pastas canônicas preexistentes. Criação real de destinos próprios foi comprovada sem remover pastas de uso.
3. A frota decide a publicação e observa um dia nos 12 sites para confirmar sucesso de cache/robots com menos de 24 h. Somente Site-Teste instalado nesta entrega; sem publicação, push ou alteração da frota.
4. Contas não administrativas conservam a política legada. Impor 14 dias onde estavam configurados 90 seria mudança adicional de preferência, não aplicada.

Não há pendência técnica nova do MCP. Os aceites externos acima não são declarados concluídos.

## 7. Credenciais

Nenhuma credencial nova exigida/exibida/incluída. Caixa existente usada apenas no host autorizado. Fonte sem mensagem bruta, chave privada, senha, dump real ou configuração do ambiente; chaves de testes efêmeras. Identificadores de backup/recibo são de auditoria.

## 8. Arquivos finais

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| base-site-core-fator3-1.55.0-instalador.zip | 2609157 | 1d7e54fb86ea4c61de5e58df22e81b5e93aad3018bc5802fb3fd86ff48dd41a0 |
| base-site-core-fator3-1.55.0-fonte.zip | 3755919 | 054afe0bdece974adad005f0910735d10af0f73059a9ee807cf96bbbe3b33b97 |

Instalador: pasta estável, runtime/documentação corrente. Fonte: mesmo runtime byte a byte, ferramentas/testes/evidências sanitizadas/locks e histórico identificado; sem ZIPs aninhados, laboratórios ou credenciais. Relatório externo canônico: base-site-core-fator3-1.55.0-relatorio.md. Cópia interna anterior ao fechamento evita hash circular. Sem quarto arquivo de impacto.
