# Entrega — Fator3 MCP Google 0.18.1

Revisão: 1 · Data/hora: 2026-10-23T13:50:50+00:00 · Rodada: revisão independente da versão 0.18.0
Slug: `wp-mcp-google-fator3` · Versão/build: `0.18.1`
Status: **apta no escopo testado** · Versão corrente deste trabalho: **0.18.1**

## 1. De onde esta versão entra

Foi revisada a 0.18.0 fornecida pelo dono, comparando-a à 0.17.0 entregue anteriormente. A 0.18.0 original passou em 1.160 testes PHPUnit, com 14.271 asserções, e em 2.773 verificações da matriz nativa reproduzida nesta revisão. Cinco cenários adicionais, porém, demonstraram classificações incorretas no novo diagnóstico. Por isso, a versão recebida foi corrigida e o patch avançou para **0.18.1**.

Entradas conferidas:

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| Google 0.18.0 fonte | 3735340 | `1f21d41cc98274d28af643f927a722c0f842737fe9a879b65161ca0ce1bea70a` |
| Google 0.18.0 instalador | 798769 | `b1ce908558502c8edf2c6928112d5a772b3690810cfc11405dcfe0547f2baea9` |
| Google 0.17.0 instalador | 767299 | `42bd11080b518c82e0960753fa7b08d7adae28743cfcd3e96f9b83bf3f4709b0` |

Os 159 arquivos do instalador recebido correspondem byte a byte aos respectivos arquivos do fonte recebido. A atualização direta **0.18.0 → 0.18.1** foi testada, assim como **0.17.0 → 0.18.1** e instalação limpa. Não há versão intermediária obrigatória.

Requisitos executados: WordPress **7.1.2** e **7.1.3**, PHP **8.3.6**, MySQL **8.0.46**. WP-CLI **2.12.0**, PHPUnit **9.6.37**, jsdom **27.4.0**. Dependências e hashes estão no fonte.

## 2. Convivência e encaminhamentos

A matriz principal usou MCP **0.28.0**, Site Core **1.48.0**, Meta **0.6.0** e LinkedIn **0.7.0**. Um ensaio adicional de atualização direta usou Meta **0.7.0** e LinkedIn **0.8.1**, mantendo MCP 0.28.0 e Core 1.48.0; foram preservados registros sociais, configurações e segredos, com inventários finais exatos dos cinco pacotes.

**Nenhuma alteração foi feita no Core, no MCP, no Meta ou no LinkedIn.** Não foi identificado impacto técnico que exija mudança de contrato ou implementação nesses mantenedores. Não foi emitido documento de impacto ao Core. A correção é interna ao diagnóstico do Google.

Permanecem as **287 habilidades**, as **36 opções**, os oito checks de prontidão e os contratos `google-readiness/1.0.0`, `site-conversion-delivery/1.0.0`, configuração `4.0.0` e manutenção `2.0.0`. Os schemas de entrada e saída de todas as habilidades são idênticos aos da 0.18.0. O detalhe livre dos incidentes ganha `complete` para indicar contagem parcial; nenhum campo existente foi retirado.

O relatório recebido menciona testes suplementares com Core 1.49.0 e MCP 0.29.0. Esses instaladores não estavam entre os arquivos disponíveis desta revisão; essa combinação não é reivindicada como prova própria.

## 3. Mudanças e evidência

Comparação 0.17.0 → 0.18.0: 55 arquivos de código, documentação, build e testes alterados/adicionados, excluindo evidências históricas. No runtime, 15 arquivos afetados, incluindo a adição de `Readiness.php`. Foram examinadas a tradução das descrições GTM, a nova prontidão, o cache restrito às leituras do Core, a seleção GA4 por fluxo, as correções de observação do executor e a ampliação documental dos schemas.

| Achado reproduzido na 0.18.0 | Consequência | Correção na 0.18.1 |
|---|---|---|
| Canal fechado, credencial válida e destinos vazios produziam `ready` na leitura direta usada pelo painel | Orientação falsa de disponibilidade | Check `credential` bloqueia com `channel_disabled`; preservado o gate externo existente |
| Fluxo GA4 selecionado sem ID de medição do Core aparecia como não configurado | Perda de configuração podia desaparecer do veredito | Seleção local é distinguida de configuração incompleta; o bloqueio efetivo é mantido. Também cobre Ads parcialmente configurado |
| Validação Ads pendente sobrepunha `grant_revoked` | Indicava apenas espera quando era necessária nova autorização | Atenção por pendência somente quando a causa efetiva é `verification_required`; serviço desligado e demais bloqueios prevalecem |
| Um incidente aberto após 100 resolvidos era ignorado | Diagnóstico dizia não haver incidentes abertos | Filtro de abertos e conexão aplicado antes da paginação; limite de 100 e indicação de contagem parcial |
| Configuração de conversões ilegível era apenas `attention` | Subestimava um impedimento real de entrega | Classificação `blocked` para leitura de configuração malsucedida |

A mensagem de atenção passou a **“Conexão requer atenção”**; o painel mostra **“Requer atenção”**, sem afirmar que uma entrega pendente já funciona.

A prova negativa está em `evidence/0181/negative-0180.json`: cinco falhas observadas no instalador original. A suíte `readiness0181` verifica os cinco casos e controles adicionais de serviço desabilitado, destino Ads parcial, integração desabilitada, paginação com mais de 100 abertos e isolamento de conexão. São 40 verificações por execução, contando os controles já existentes.

O patch altera três arquivos de lógica/apresentação (`Readiness.php`, `Automation/Alerts.php`, `Admin/ConversionScreen.php`), além da versão e da documentação compilada. Não altera o transporte, a seleção de conexão ou o cache do Core. A consulta pública de alertas mantém seu comportamento padrão; o filtro de abertos é um argumento interno opcional usado pela prontidão.

## 4. Instalação e prova da troca

Instalador: `wp-mcp-google-fator3-0.18.1-instalador.zip`. `expected_slug`: `wp-mcp-google-fator3`. Use o SHA-256 da seção 8. A revisão não publica URL raw nem instala em site remoto. O pacote pode ser instalado pelo fluxo habitual de atualização do WordPress/MCP após backup do ambiente de destino.

Prontidão: habilidade `google/readiness-status`, parâmetros `{}` ou `{"hours_ahead":6}`; CLI `wp mcp-google readiness --user=<administrador> --format=json`. O resultado esperado depende da configuração real: falta de credencial ou bloqueio efetivo deve produzir `blocked`, e não prontidão artificial. Os gates administrativos e de canal permanecem vigentes.

| Ambiente/cenário | Verificações | Resultado |
|---|---:|---|
| Limpo, WordPress 7.1.2, Core/MCP antes do Google | 1006 | Passou |
| Limpo, WordPress 7.1.3 | 869 | Passou |
| Atualização 0.17.0 → 0.18.1, rollback e reaplicação | 830 | Passou |
| Atualização direta 0.18.0 → 0.18.1, rollback e reaplicação | 206 | Passou |
| Google antes de Core/MCP | 119 | Passou |
| Google isolado, incluindo WP-CLI real e autorização | 33 | Passou |
| **Matriz principal** | **3063** | **Sem falhas** |
| Convivência adicional Meta 0.7.0 / LinkedIn 0.8.1, atualização direta | 99 | Passou; inventários exatos |
| Repetição independente do rollback 0.17.0 fora do diretório sincronizado | 33 | Passou; inventário exato |

Também passaram **1.160 testes PHPUnit / 14.271 asserções**, **60 verificações de contratos**, lint de **155 arquivos PHP**, conferência do instalador e validação documental. O DOM autenticado exercita o painel; não equivale a inspeção visual em navegador.

A seleção GA4 em conexões separadas e a detecção de ambiguidade passaram. O teste que muda a medição do Core durante o despacho confirmou recusa antes da coleta. A leitura de prontidão continua sem chamadas ao provedor ou alteração da configuração.

Documentação: descoberta do schema, índice e leitura integral paginada via **MCP HTTP real local**, com verificação dos hashes e da versão 0.18.1; controles de acesso, revisão de continuação e identificadores inválidos passaram. Evidência corrente em `evidence/0181/validation0181.json` e seus dois relatórios de origem, com a mesma identidade de código/testes/ferramentas.

Estado final: laboratórios encerrados, processos de HTTP e banco parados, candidato exato instalado nos cenários finais. Nenhum site remoto ou repositório foi modificado.

## 5. Banco e volta de versão

Não há nova tabela, migração, hook de manutenção ou opção. A revisão não muda as regras de envio, o formato da fila nem a autorização administrativa. Os testes de atualização preservaram configurações, segredos cifrados, tarefas concluídas, agendamentos pausados, auditoria e dados sociais; não houve repetição de tarefa concluída.

O rollback de arquivos foi testado com pré-imagem e recusa de destino editado, seguido de reaplicação. Restaurar arquivos não desfaz dados, efeitos externos ou operações posteriores do site; mantenha o backup habitual antes de uma instalação real.

## 6. O que permanece pendente

- Não foram usados tokens Google reais, nem testados propagação efetiva na Data Manager, atribuição comercial ou renovação durante dois dias. Respostas Google e e-mail foram simulados e o laboratório bloqueia tráfego externo.
- Não houve instalação no Site-Teste remoto, ensaio multisite, PHP-FPM ou validação visual em navegador. Isso não é apresentado como homologação de produção.
- Duas tentativas preliminares de rollback para 0.17.0 encontraram um arquivo residual na conferência do diretório sincronizado; uma delas mostrou explicitamente `.rsync-tmp`. A matriz final e a repetição fora desse diretório passaram sem mudar Google/MCP. A sincronização do ambiente é a hipótese sustentada por essa observação, não uma causa provada. As ocorrências permanecem registradas em `preliminary-observations.json`; o instalador não contém esses arquivos.
- A primeira versão da nova fixture de incidentes interferia em uma fixture do teste de DOM. Foi isolada por conexão e pelos próprios IDs; a matriz final passou. Essa correção pertence aos testes, não ao runtime.

Não há correção de produto conhecida deixada aberta dentro dos cenários finais executados. As limitações acima delimitam a conclusão.

## 7. Credenciais e configuração do dono

Nenhuma credencial real foi solicitada ou incorporada. A configuração permanece em Ferramentas → Fator3 MCP Google: credencial e serviços na aba Conexão, destinos e verificação na aba Conversões. O ID GA4 continua vindo do Site Core. Não há novo campo obrigatório. Quem já possui destino verificado não precisa reconfigurá-lo por causa deste patch, salvo se o diagnóstico revelar um bloqueio real preexistente.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | `wp-mcp-google-fator3-0.18.1-instalador.zip` | 799626 | `91c97cc300360511bc2477f5af9b0c2017e8b04861d015aaf0f0e5accd1cefef` |
| Fonte | `wp-mcp-google-fator3-0.18.1-fonte.zip` | 4177792 | `7b8dd2e3425bc1c4e0ddcbff51318069a98293d276e5b18564a603df8d0ab659` |

O fonte contém código, documentação editável, build, testes, evidências e instruções de reprodução. Não contém instaladores aninhados, banco, vendor, node_modules, configurações privadas ou arquivos de estado dos testes. O relatório externo é canônico.

Relatório externo canônico fechado após o empacotamento do fonte. A cópia interna antecede esse fechamento.
