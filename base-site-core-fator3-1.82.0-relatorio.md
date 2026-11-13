# Entrega — Fator3 Site Core 1.82.0

13/11/2026 · Slug base-site-core-fator3 · Estado com pendências de aceite na frota. Relatório externo canônico. O fonte contém a cópia anterior ao seu fechamento.

## 1. De onde esta versão entra

Instalação nova ou atualização direta da versão oficial 1.81.1. Os documentos instrucoes-agentes-plugins-fator3.md e padrao-desenvolvimento-plugins-fator3.md foram conferidos na revisão 5. O fonte de partida tem SHA-256 9beff6ac439196104f8658abb159aaea2ddd1f635242e6a4ef963306913e1a5b. O basename, as capacidades e o contrato administrativo 8.38.0 foram preservados. Os mínimos são PHP 8.3 de 64 bits e WordPress 7.1.4.

## 2. Convivência e encaminhamentos

Matriz instalada e ativa no Site-Teste e na bancada com fornecedores sintéticos:

| Pacote | Versão | Interação verificada ou referência |
|---|---|---|
| Fator3 MCP | 0.45.0 | Instalação autenticada com hash e slug, documentação e saúde |
| Fator3 MCP Google | 0.34.0 | Acervo com concessão e contrato de anúncio de origem |
| Fator3 MCP Meta | 0.25.0 | Consulta de criativo, imagem e repetição do worker |
| Fator3 MCP LinkedIn | 0.22.0 | Consulta de criativo, miniatura e repetição do worker |
| Fator3 MCP Pipedrive | 0.10.0 | Coexistência e integração do Core com o CRM em transporte controlado |

Os pedidos são de responsabilidade do Core. Nenhuma revisão de contrato foi solicitada aos acompanhantes. Os impactos anteriores de Meta e LinkedIn têm notas de acompanhamento no fonte. O relatório da Meta conserva a validação da conta da Korvena. O relatório do LinkedIn registra o download administrativo de um JPEG na 0.21.0 e mantém em aberto o aceite comercial da conta do CTO Office. A nova versão do Pipedrive já comporta o campo adicional de WhatsApp referido por seu mantenedor.

## 3. Mudanças e evidência

**392 — recibo no contato.** A tabela de leads recebe a coluna anulável anuncio_entrega. A migração usa a trava do contato, copia os dados antes de apagar a option e reaproveita IDs já confirmados do CRM. Um arquivo privado atribuído pela 1.81.1 volta a aguardar comprovação. A listagem omite o recibo. A rota f3base/leads-registros-ler com record_id fornece a projeção de detalhe. A suíte verificou migração repetida, registros órfãos, prazo vencido, limpeza da fila e catálogo sem ocorrências.

**394 — complemento na conversa original.** O Core identifica a mensagem principal pelo relacionamento entre as partes gravadas, confere seu canal e entrega o arquivo com channel_id e thread_ts. Havendo imagem, a legenda da nova resposta traz os campos obtidos do anúncio e os links. Sem mídia, o texto usa resposta própria. O recibo de conclusão do upload inicia uma leitura de files.info. São necessárias evidências do arquivo no canal e na thread. Quando shares informa só o ts do compartilhamento, o Core confere os arquivos da resposta em conversations.replies. Se a escrita for incerta, reaproveita o identificador reservado. Quando possível, os campos ficam acessíveis na resposta Origem enquanto a imagem aguarda confirmação. O nome inicial da campanha pode vir da captura, da linha de clique arquivada, do mapa por conta ou da consulta local do dataset campaign no dia da captura e no anterior.

**395 — primeira linha do Slack.** Este pedido substitui o 393. O cabeçalho e a resposta Origem usam a mesma atribuição comercial. O método email termina em “Recebido por e-mail”. Os formulários identificam Site, Meta, LinkedIn ou Google. O clique para WhatsApp conserva seu rótulo. A origem distingue plataforma paga, outra fonte com campanha e orgânico. [TESTE] permanece quando aplicável. Uma resolução posterior altera só o título do aviso principal com chat.update no mesmo canal e ts, preservando o corpo original. Em sinais contraditórios a interface informa “Origem conflitante”. Para campanha sem fonte reconhecível usa “Origem não identificada”.

**Testes executados.** A suíte em WordPress 7.1.4, PHP 8.3.6 e MySQL 8.0.46 passou em 497 verificações na instalação limpa e 509 na atualização. As contagens incluem a repetição dos testes de regressão em cada cenário. As 89 verificações de origem de cada fase cobriram rótulos, compartilhamentos ausentes, canal ou thread divergentes, leitura de arquivo sem thread_ts, acervo paginado, conta divergente e atualização idempotente do cabeçalho. A matriz de provedores passou em 28 verificações da Meta, 22 do Google e 39 do LinkedIn. Em cada plataforma, duas passagens do worker resultaram em uma atualização da principal, um compartilhamento, uma nota no CRM e um anexo. Erros de transporte, mídia e permissões foram simulados. Os diretórios evidence/1820 e tests contêm as provas e a reprodução.

## 4. Instalação e prova da troca

No Site-Teste, a operação 90e2437434cae6ebd3090bf02275080f aplicou o ZIP conferido sobre o plugin ativo 1.81.1. A leitura em novo processo mostrou 1.82.0 ativa. O executor confirmou o ciclo e verificou cabeçalhos, navegação e Pipedrive. A página inicial e /wp-json/ responderam HTTP 200 antes e depois, com bypass de cache confirmado. O catálogo registrou quantidade 0, com leitura completa.

A bancada do Site-Teste executou 79 verificações com WordPress 7.1.4 e PHP 8.3.36 em tabelas temporárias e transporte HTTP interceptado. O ensaio incluiu a primeira linha, o mesmo ts após a correção, texto tardio, mídia e canais divergentes. O arquivo temporário de teste e o ZIP de transporte foram removidos. A sonda posterior à remoção passou. Cinco documentos instalados foram recuperados pelo MCP, em oito páginas ao todo, e coincidiram com os arquivos do instalador. A suíte local verificou a recusa de leitura anônima e a correspondência do catálogo de 194 abilities.

Para instalar via painel, envie o instalador ZIP e substitua a versão existente. Em instalação automatizada, confira slug e SHA-256 antes da troca. Leia f3base/resumo-operacional-ler até constar atualizacao.estado concluida. Os nomes e a versão dos acompanhantes devem constar ativos no inventário. Com f3base/documentacao-ler consulte docs/RELEASE-1.82.0.md.

## 5. Banco, migração e correção por nova versão

O repositório de contatos passa ao schema 9. A instalação faz o DDL e agenda a migração das opções da 1.81.1 em lotes de até 50. A próxima passagem do zelador também processa os itens restantes. Apagar ou anonimizar o registro trata o estado associado segundo a política existente. O prazo de tentativas é de 30 dias desde o início. Ao concluir ou expirar, a fila e os contadores transitórios são limpos. O recibo acompanha a retenção do contato. Na atualização de laboratório, preservaram-se 993 amostras sintéticas e a configuração de contato. O instalador foi também reaplicado pelo Plugin_Upgrader e os 964 arquivos instalados conferiram byte a byte. Todos os 600 arquivos PHP do runtime passaram pelo verificador de sintaxe. Correções subsequentes seguem por nova versão.

## 6. O que permanece pendente

O aceite final do operador depende dos próximos contatos reais da frota. No CTO Office, conferir na tela do Slack o cabeçalho do contato pago, as informações do criativo e a imagem na thread. Na próxima entrada real de e-mail, verificar a linha sem segmento de origem. Conferir também no CTO Office a contagem de avisos de catálogo após a atualização e a migração. A instalação desta rodada foi realizada apenas no Site-Teste. A bancada validou o protocolo com respostas controladas. A visualização em um workspace Slack real não foi exercitada nesta rodada. Os estados de sites fora do Site-Teste descritos na seção 2 provêm dos respectivos relatórios.

## 7. Credenciais e configuração do dono

O bot deve participar do canal e possuir chat:write, files:write e files:read. Quando o Slack omite thread_ts em shares, a credencial precisa conseguir ler a conversa correspondente por conversations.replies. Em ausência de permissão a ficha conserva a situação pendente. O acesso a nomes no acervo depende da seleção e concessão feitas no Google e da cobertura da captura. As integrações Meta e LinkedIn usam suas concessões de leitura por conta. O instalador não contém credenciais nem fixtures e a rodada não alterou segredos da frota.

Referências do protocolo: [files.completeUploadExternal](https://docs.slack.dev/reference/methods/files.completeUploadExternal/), [files.info](https://docs.slack.dev/reference/methods/files.info/) e [objeto file](https://docs.slack.dev/reference/objects/file-object/).

## 8. Identidade dos arquivos

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| base-site-core-fator3-1.82.0-instalador.zip | 4442101 | 90bda2bbe2181a44330da121a349d3aa8b967e20ccf848ea7f9b51ac72c94482 |
| base-site-core-fator3-1.82.0-fonte.zip | 47366733 | 9e30debe6a0c77a4d9b3c4058cdd3117830c5551a2d1992a95826ba7d2d6b69c |

O relatório externo fecha a identidade do fonte depois de gerar o ZIP. O manifesto do runtime e os recibos do Site-Teste identificam o instalador efetivamente testado.
