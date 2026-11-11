# Entrega — Fator3 Site Core 1.81.1

Revisão 1 · 2026-11-11T13:02:00Z · Implementação, correção e homologação dos pedidos 389, 390 e 391. Status **com-pendencias** nos aceites com contas comerciais reais. Instalado e ativo no Site-Teste.

## 1. De onde esta versão entra

Slug e basename publicados: base-site-core-fator3 e base-site-core-fator3/base-site-core-fator3.php. A rodada partiu do fonte e do instalador oficiais da 1.80.0. A 1.81.0 foi instalada no Site-Teste. O teste adicional de atraso comercial identificou uma inversão de ordem no Slack e motivou o patch 1.81.1. O pacote final suporta instalação limpa e atualização direta de ambas as bases. O contrato administrativo continua em 8.38.0.

Normas aplicadas: instrucoes-agentes-plugins-fator3.md e padrao-desenvolvimento-plugins-fator3.md, revisão 5 de 02/11/2026. Pedidos da lista Fator3 Site Core de 11/11/2026 12:03:33. Requisitos: WordPress 7.1.4+, PHP 8.3+ de 64 bits. Laboratório com WordPress 7.1.4, PHP 8.3.6 e MySQL 8.0.46. Site-Teste com WordPress 7.1.4 e PHP 8.3.36 no servidor web e na prova CLI final.

## 2. Convivência e encaminhamentos

No Site-Teste estavam ativos o MCP 0.44.0, Google 0.34.0, Meta 0.24.1, LinkedIn 0.21.0 e Pipedrive 0.9.0. O laboratório carregou os mesmos pacotes. Os três relatórios de impacto de mídia resultaram em adaptadores de leitura no Core. O contrato pipedrive-api-client/1.0.0 conserva o tratamento de resultado incerto. O Core faz a entrega de origem pelo seu próprio fluxo comercial. O contrato de configuração e os pontos de autoria tratados na 1.80.0 continuam cobertos pelas regressões. O Implantador 2.20.0 foi considerado pelo impacto recebido, sem ensaio conjunto novo desse instalador. O MCP serviu à troca do pacote, ao catálogo e à leitura dos documentos.

| Destinatário | Classificação | Encaminhamento |
|---|---|---|
| Meta 0.24.1 | Validação coordenada da conta Korvena | base-site-core-fator3-1.81.1-impacto-wp-mcp-meta-fator3.md, revisão 1 |
| LinkedIn 0.21.0 | Validação coordenada da conta CTO Office | base-site-core-fator3-1.81.1-impacto-wp-mcp-linkedin-fator3.md, revisão 1 |

O contrato Google foi incorporado e verificado também para GCLID, data, resultado parcial de campanha e revogação. O Site-Teste recusou uma leitura sem seleção compatível com conta_divergente antes de acessar o fornecedor. As chamadas reais de Google Ads dependem da seleção local e da concessão para a conta. Esta entrega não solicita alteração nos demais pacotes.

## 3. Mudanças e evidência

| Pedido | Mudança entregue | Evidência |
|---|---|---|
| 389 · Sonda de listagem em cron sem HTTPS | A URL de upgrade usa o esquema, host e porta de home_url e conserva o caminho instalado de content_url. Confere a resposta direta, o arquivo público com token e a negativa de listagem. | No Apache do Site-Teste, WP-CLI em PHP 8.3.36 sem HTTPS obteve 404 no upgrade e 200 no controle, com estado verificado e novo recibo. O hash do bloco de regras ficou igual ao da base. Em WordPress descartável, o caso de controle simulou HTTP 200 no upgrade e terminou pending. |
| 390 · Anúncio de origem | O Core seleciona a conta do contato e busca os dados no SDK de Meta, LinkedIn ou Google. Eventos pagos recebem os campos disponíveis, links estáveis, cópia da imagem ou miniatura e, quando fornecido, link do vídeo. O Slack edita Origem pelo mesmo timestamp. O Pipedrive recebe uma nota fixada e o arquivo na oportunidade confirmada. Na ficha, o administrador pode consultar um contato histórico. | Meta 28/28, LinkedIn 39/39, Google 22/22 na matriz dos SDKs. Dois ciclos por provedor, um upload concluído no Slack, uma edição da resposta, uma nota e um arquivo. Testes também cobrem edição de nota já existente, destino em negócio, falta de files:write, origem orgânica e criação remota incerta. |
| 391 · Aviso individual do Slack | Mensagem principal e até quatro respostas, nesta ordem: Acontecimento, Origem, Visitas e Links. Omite campos sem valor. Inclui cargo, interesse, hora de submissão, parceiro e classificação comercial quando disponíveis. O link comercial é acrescentado na resposta existente. | Na 1.81.0, a espera expirava em uma hora e outra resposta podia passar à frente de uma retentativa. A 1.81.1 usa o estado da fila. O ensaio de duas horas, a retentativa do Slack e a confirmação repetida passaram. Em um aviso antigo com Links já publicado, os blocos Visitas e Links ocupam a mesma resposta, nessa ordem. |

Quando o CRM ainda processa o contato e não há dados de visita, o link do WordPress na última resposta aguarda a classificação. As demais mensagens podem sair antes. Falha comercial terminal libera Links. Sob cota horária, os threads individuais aguardam a próxima janela. O download de mídia aceita JPEG, PNG e GIF de até 4 MiB. A ausência de arquivo conserva a referência textual. O enriquecimento é assíncrono.

## 4. Instalação e prova da troca

Usou-se o instalador local transferido por partes para o diretório de upgrade do Site-Teste. A transferência e plugins/upload-base64 com zip_path, overwrite e activate verificaram expected_slug e expected_sha256. O código foi carregado em nova requisição. A operação final foi b5474d482bd5f5cd2a1dada04ae82e6d. A página inicial e /wp-json/ responderam 200 antes e depois. Uma leitura posterior do inventário confirmou 1.81.1 ativa. URL raw pública e publicação da frota pendentes. Cabe à frota publicar o instalador e o relatório e verificar o hash dos bytes servidos antes de distribuir.

| Prova | Resultado |
|---|---|
| Instalação limpa e duas bases de atualização | Ciclos completos de instalação, catálogo, desinstalação e reativação. Nas duas migrações, conferência de 993 amostras e configuração por hash antes e depois. |
| Testes nativos | Em cada um dos três percursos passaram 52 verificações de origem e entrega, 8 de ordem, 17 de correções, 223 de contratos e funções e três grupos de regressão com 48, 29 e 69 verificações. |
| APIs do Core | 194 habilidades registradas. As 103 de leitura foram exercitadas, com 66 sucessos e 37 recusas controladas. Zero exceções e avisos PHP nessa bateria. |
| Pacote e interface | Manifesto de 962 arquivos, lint de 600 PHP. Chromium 156 em WordPress local abriu a ficha, enviou a consulta por botão e nonce e conferiu o retorno ao mesmo contato com horário de consulta. |
| Canais no Site-Teste | 47 verificações aprovadas sobre tabelas temporárias em conexão própria. Dados fictícios, arquivos em bytes e HTTP de fornecedores interceptado. As credenciais e os contatos comerciais não participaram da prova. |
| Sonda no Site-Teste | Com o PHP padrão do processo, wp cron event run retornou zero em PHP 8.2.35 e o carimbo do Core ficou antigo. A execução com PHP 8.3.36 e is_ssl() falso avançou o recibo de 1794401828 para 1794402077 e confirmou o diretório. O llms.txt havia sido regenerado pela operação existente do Core antes da prova. |
| Documentação e limpeza | O MCP leu integralmente docs/DOCUMENTACAO.md, docs/RELEASE-1.81.1.md e docs/AGENTES-1.81.1.md por páginas. Os textos e hashes conferem com o instalador. Ambos os auxiliares de teste e o ZIP temporário estavam ausentes na verificação final. O MCP reteve seus backups privados de alteração. |

Dados e hashes da prova em evidence/1811/site-teste.json do fonte. Suites por base em evidence/1811/entrega-*.log. A própria hospedagem executou o comando abaixo com PHP 8.3.36. O código de saída deve ser acompanhado de um novo carimbo reverificado_em em f3base/servidor-aplicar com acao=consultar.

```sh
WP_CLI_PHP=/usr/local/php83/bin/php PATH="/usr/local/php83/bin:$PATH" wp cron event run f3base_servidor_reverificar
```

## 5. Banco, migração e correção por nova versão

Os comprovantes de entrega usam as partes do aviso já identificadas, o diário de oportunidades e uma opção por contato. A opção guarda campos estáveis, identificadores, data, vínculo com o destino e estado de escrita. A consulta manual usa resultado temporário associado ao administrador. O complemento reaproveita a nota confirmada e o arquivo associado. Quando a API perde a resposta depois do despacho, o recibo de incerteza bloqueia nova criação automática. A eliminação do contato remove o agendamento e o comprovante local. Configuração e histórico foram verificados no ensaio de migração. Efeitos já aceitos por Slack ou Pipedrive exigem reconciliação no próprio destino. Correções posteriores recebem nova versão.

## 6. O que permanece pendente

O responsável pela hospedagem deve confirmar o executável de PHP usado **no agendamento regular**. O teste sob acesso administrativo comprovou a diferença entre o binário padrão e o PHP 8.3 explícito. A configuração do agendador do provedor não foi inspecionada. A matriz comprovou o consumo dos SDKs com respostas sintéticas. Permanece o aceite do criativo e das permissões nas contas Korvena e CTO Office, bem como a conferência visual da entrega num canal Slack e CRM de homologação com credenciais designadas. Os sites de produção só foram consultados. A prova negativa com a regra retirada foi feita com resposta HTTP simulada. O Apache compartilhado manteve a proteção ativa.

## 7. Credenciais e configuração do dono

No Site Core, configure o app do Slack, o canal e o formato thread em Conexões e entregas. Habilite chat:write e files:write no bot para edição da resposta e envio de mídia. No Pipedrive, confira a conta, o domínio e os direitos de leitura da oportunidade, gravação de nota e anexação de arquivo. Em Meta, configure a extensão ad_origin na conta escolhida. Em LinkedIn, conceda ad_source e, para formulário nativo, responses. Em Google, conceda clicks e origin_ad na conta selecionada. A consulta administrativa exige manage_options e f3base_ler_leads. O relatório registra tipos de acesso, sem valores de credenciais.

## 8. Identidade dos arquivos

| Artefato | Arquivo | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | base-site-core-fator3-1.81.1-instalador.zip | 4435171 | 8a03bc5dfd3f94d81a953bb7134a14bacbc6883c5b038b4ef0fee1241c1dcb02 |
| Fonte | base-site-core-fator3-1.81.1-fonte.zip | 42554019 | 9beff6ac439196104f8658abb159aaea2ddd1f635242e6a4ef963306913e1a5b |

A cópia em RELATORIO-PRE-FECHAMENTO.md precede a compactação do fonte. O relatório externo identifica os dois ZIPs finais.

A leitura integral do manifesto confirmou 8974 arquivos com tamanho e SHA-256. O instalador reconstruído a partir do ZIP de fonte extraído corresponde byte a byte ao usado no Site-Teste.
