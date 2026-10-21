# Entrega — Fator3 Site Core 1.42.0

Revisão 1 · 20/10/2026 · Rodada: implementação · **Status: com-pendencias**.
Slug/basename preservado: `base-site-core-fator3/base-site-core-fator3.php`.
Implementação dos pedidos core 238–242 concluída e validada localmente. Homologação externa e instalação da frota não realizadas nesta rodada.

## 1. De onde esta versão entra

Instalação limpa ou atualização direta da 1.41.0, sem desinstalar. Base imutável: instalador SHA-256 `66ae54be3b0ec7a066187455b8358fc3c3431a47de8fc6aa8ac8c5efa3510919`, 2.037.832 bytes. Escopo confirmado em `Fator3 Site Core(10).md`; os itens 238–241 estavam fora da entrega anterior e agora foram implementados, junto com 242.

Runtime exercitado: WordPress 7.1.3, PHP 8.3.6 e MySQL 8.0.46. O mínimo WordPress 7.1.2 herdado não foi reensaiado nesta rodada; não é nova prova de suporte mínimo. Sem prova PHP-FPM, multisite ou CDN.

## 2. Convivência e encaminhamentos

Google 0.15.0 recebido e conferido: instalador SHA-256 `a7014e419c1a1a79d9a9e02112fd8f5b285fed131b50e10ea26f588d2179b169`; fonte `3d2be60367a25c649462fdd913303a6d69d12a2079c7924994174e71544e34ef`. Seu impacto r2 fecha a incorporação de sendBound e não solicita novo desenvolvimento Core. A integração local Core 1.42 + Google 0.15 foi exercitada com fornecedores simulados, sem modificar o Google. A homologação comercial anterior continua pendente.

Nenhuma nova alteração de contrato Google, Meta, LinkedIn ou transporte MCP. Não foi gerado novo documento de impacto apenas para anunciar versão. Foram avaliadas as fronteiras de conversões, descoberta de abilities e campos de credenciais existentes; o código do Implantador não estava disponível e não foi presumido examinado.

Contrato administrativo **8.7.0**: nomes descritivos da configuração e do e-mail automático; dois nomes novos de ability, com aliases anteriores por esta versão. Consumidores devem redescobrir o schema. `f3base/c0-ler` e `f3base/c0-homologar` continuam aceitos na 1.42.0, com os mesmos gates e sem duplicar filas. Use `f3base/email-novo-lead-ler` e `f3base/email-novo-lead-homologar`. Catálogo gerado: 136 abilities e 70 opções operáveis. A compatibilidade técnica está em `compat/email-legado.php`; os códigos antigos não são nomes comerciais na interface.

## 3. Mudanças e evidência

| Pedido | Resultado implementado | Evidência e limite |
|---|---|---|
| 238 | Notas novas somente com contato, respostas, página/formulário, campanha/anúncio, data/hora e link WordPress. IDs, hashes e operações incertas ficam no diário. Assunto do e-mail configurável, padrão E-mail – primeiro contato; nota somente data/hora. Atividade WhatsApp existente no lead é reaproveitada sem sobrescrever edições. | 43 verificações do fluxo Pipedrive, incluindo perda de resposta de lead/nota/atividade e repetição sem duplicar. Conta e HTTP simulados. Notas antigas não foram reescritas. |
| 239 | Aba E-mail automático ao novo lead com configuração, senha mascarada, apagar e revisão; estado, cota, contagens e último erro sanitizado. Aba Credenciais complementares cobre os cinco campos citados. | Renderização PHP e autorização; senha não reapresentada. O dono deve salvar a senha com envio desligado, depois ativar. |
| 240 | Frase informa que vamos entrar em contato, sem prazo nem canal prometido. Removida dependência do prazo da primeira atividade. | Mensagem com prazo antigo vencido é gerada; recusa de destinatário antes de DATA e resposta SMTP incerta preservadas. |
| 241 | Marca, remetente, SMTP, nome, assinatura, apresentação, contato e WhatsApp configuráveis; serviços do catálogo da conta. Novos nomes de options, tabela, agenda e abilities; migração preserva configuração e recifra segredo. Site novo incompleto não envia. | Upgrade real local preservou valores, segredo, cotas e estados incertos. Valores comerciais legados existem somente no código de migração para preservar sites existentes; não são defaults novos. |
| 242 | Um só schema de entrada aceita os contratos 1.0.0 e 1.1.0; cada saída conservada. | Ambos executados pela Abilities API WordPress, ok=true e contrato solicitado. Contrato inválido recusado. Erro da 1.41 reproduzido no Site-Teste pelo MCP. |

Texto de serviço selecionado sem apresentação continua bloqueando envio. O assunto e os textos são congelados na intenção; a operação não inventa IDs ou conteúdo. Após aceite SMTP, a atividade é complementar: falha no CRM não reenvia e-mail. Atividade de e-mail com POST incerto permanece para conferência, sem recriação automática. A ausência de múltiplas atividades é proteção local e reconciliação; não há trava distribuída entre operadores e vários sites.

## 4. Instalação e prova da troca

**221 verificações funcionais aprovadas**, mais os ciclos nativos de instalação limpa/upgrade e lint de **219 arquivos PHP**. Contagens: release 40, fluxo Pipedrive 43, renderização de 15 páginas 30, documentação 69 e integração Google 39. Evidências da rodada estão no fonte; testes históricos não foram somados.

Ciclos usam Plugin_Upgrader com o ZIP final, sem editar o runtime instalado; processos novos confirmam versão, contrato, estrutura, configuração, migração da senha e estados incertos. Nova instalação funciona sem acompanhantes. A repetição da atualização retorna atual. O hash do candidato consta em `evidence/native-cycles-142.json` e corresponde à seção 8. O snapshot compara conteúdo, normalizando somente os nomes migrados e a ordenação JSON. A espera de finalização foi acelerada no estado descartável do teste.

Documentação instalada inclui RELEASE-1.42.0.md, AGENTES-1.42.0.md, índice, ajuda, schemas, catálogo e inventário regenerados. Leitura completa/paginada, hashes, confinamento e gate administrativo exercitados pela API WordPress. Não foi executado transporte HTTP MCP local nesta rodada; não se apresenta a prova nativa como prova MCP remota.

Site-Teste consultado somente em leitura: Core 1.41.0, Google 0.15.0, MCP 0.24.0; inventário request `ac97056ba4b1fa5527dc8d46`. O item 242 foi reproduzido. Nenhuma configuração ou instalação remota foi alterada e nenhum contato real foi criado. Bancos locais descartáveis preservados para evidência; processos de execução encerrados.

Frota: publicar instalador/relatório, conferir SHA-256 dos bytes raw e usar `plugins/upload` com expected_slug=base-site-core-fator3, expected_sha256 da seção 8, overwrite=true e activate=true. A URL da versão ainda não foi publicada/verificada nesta rodada; não houve push. Depois da troca, conferir prontidão, documentação e os dois contratos de conversões pelo MCP remoto.

## 5. Banco e volta de versão

A migração renomeia `{prefixo}f3base_c0` para `{prefixo}f3base_email_novo_lead`, conserva estados/IDs, migra referências de intenção no contato/diário, cota e agenda. Configuração e senha passam a `f3base_email_novo_lead` e `f3base_email_novo_lead_smtp_senha`; cifra é refeita porque depende do nome. Allowlist operacional e metadados de procedência acompanham a mudança. Pré-imagens antigas das opções são mantidas para diagnóstico/reversão, sem uso no despacho atual. Erro de decifragem interrompe a migração, sem habilitar envio.

Somente sites com configuração legada recebem materialização dos valores antes fixos. Ativação não é ligada pela migração; a escolha anterior é conservada. Intenções pendentes deixam de usar corpos com promessa antiga. Estados enviados/incertos e provas nunca são reabertos automaticamente.

Backup coerente deve incluir banco, arquivos, salts e guarda operacional. **Não reverter somente arquivos:** a tabela foi renomeada e as identidades migradas. Suspenda executores, restaure backup coerente e reconcilie efeitos externos posteriores. A reinstalação da 1.41 isolada pode criar outro diário vazio e comprometer deduplicação; não é um procedimento suportado de reversão. Nenhum efeito externo é desfeito por restauração.

## 6. O que permanece pendente

- Frota: publicação/distribuição, instalação 1.42 e aceites MCP no Site-Teste. A prova remota ainda é da base 1.41.
- Dono e operação Pipedrive: inserir senha pela tela; homologar caixa controlada, Smart Bcc, nota e primeira atividade em ctooffice e preservar configuração de ctooffice/korvena. Limpar exclusivamente os recursos de teste criados nessa futura homologação. Nenhum e-mail real foi enviado nesta rodada.
- Navegador real: Chromium ausente; tentativa registrada. HTML PHP foi conferido, sem afirmar prova visual ou de interação no navegador.
- Atribuição real GA4, Ads e WebView permanecem pendentes do fluxo anterior; esta entrega não os encerra.
- WordPress mínimo herdado e outros runtimes não foram repetidos. Código do Implantador não avaliado.

A primeira comparação de snapshot do upgrade detectou a renomeação esperada dentro do JSON; o teste foi ajustado para comparar conteúdo canônico, mantendo todos os demais campos, e os dois ciclos passaram. A primeira renderização do harness precisava carregar o helper administrativo submit_button; corrigido apenas no teste. Esses ensaios não alteraram os ZIPs publicados anteriores.

## 7. Credenciais e configuração do dono

Configurações → Conexões e entregas → E-mail automático ao novo lead: remetente, host/porta/segurança/usuário SMTP, nome, marca, assinatura, texto da unidade, cota, alocação e senha. Contato/WhatsApp opcionais. Serviços usam catálogo da conta conectada. Homologação exige caixas controladas explicitamente listadas. Credenciais complementares são privadas, cifradas, com revisão e remoção explícita; salvar não comprova acesso remoto. Nenhum valor secreto de produção foi coletado.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | base-site-core-fator3-1.42.0-instalador.zip | 2050027 | `280f54f8afb58301fb686a659003d432195c62dbfb5b52d055a022335cf3aeac` |
| Fonte | base-site-core-fator3-1.42.0-fonte.zip | 2901683 | `219399346190d57c804a273cdff9be3076f5b494ebf90843f69be6b525a078f0` |

O relatório externo é canônico. A cópia no fonte é anterior ao seu fechamento e não contém o hash do próprio ZIP. Fonte inclui runtime idêntico, build/testes, documentação e evidências sanitizadas; Google 0.15 acompanha apenas como dependência inalterada dos testes. Nenhum ZIP contém outro ZIP. Esta entrega não edita a lista central da frota nem presume que seus aceites foram concluídos.
