# Entrega — Fator3 Site Core 1.29.0

**Instalador:** `base-site-core-fator3-1.29.0-instalador.zip`  
**Contrato:** 6.5.0  
**Base de implantação:** Core 1.28.0 ou WordPress novo, sem trava de versão e sem garantia de rollback.  
**Matriz testada:** MCP 0.19.0 e MCP Google 0.8.2.

## O que muda para a equipe

- Configurações com entrada por tarefa, busca e grupos recolhidos. Conexões e entregas centraliza contas, avisos, origens de anúncios e qualidade. Contatos continua para atendimento/formulários; Medição para relatórios. Links antigos são redirecionados.
- Descrições explicam efeito, exemplo e limites. Mapas são editados visualmente. Salvar apenas GTM não exige preencher outras áreas nem regrava valores que não foram alterados.
- Retorno à Meta genérico por instalação: conta, funil, estado do CRM, formulário e campanha. O mapa de Korvena não é padrão. Etapas podem ser registradas pelo CRM ou manualmente, com histórico e precedência.
- Melhorias de formulários, captura/conversão, comunicação, histórico de 365 dias, diagnóstico de captação, Clarity, ofertas, cron e eliminação estão rastreadas por pedido em `docs/RELEASE-1.29.0.md`.

## Prova da entrega

O ZIP indicado foi instalado pelo MCP real em WordPress descartável com Core 1.28.0. As 11 verificações do ciclo passaram, incluindo captura antes da finalização, listas vazias e procedência. Os **357 arquivos instalados correspondem byte a byte** ao ZIP e aos fontes entregues. A instalação nova também passou.

As regressões de captura, avisos, histórico, qualidade, formulários, cron e navegador passaram. Verificação sintática: 193 PHP e 28 JavaScript, sem erro. Nove assets públicos minificados têm manifesto. Histórico com 30.368 linhas sintéticas teve limites/índices conferidos. Telas e e-mail foram renderizados no Chromium. Os resultados e imagens estão no ZIP de fontes, em `suite/versao-1290/evidencias/`.

Transportes comerciais foram simulados; não houve envio a conta real, alteração nos sites da frota ou teste em korvena.net.br. Há distinção entre teste de implementação e homologação de conta.

## Como ativar o retorno comercial

1. Abra **Site Core → Configurações → Conexões e entregas → Pipedrive** e verifique a conta.
2. Em **Qualidade e Meta**, carregue funis/etapas, cadastre as etapas locais e associe regras por formulário/campanha quando necessário. A interface recusa ambiguidades e conta/funil incompatíveis com o catálogo.
3. Confira dataset, credencial e evidência de publicidade dos formulários nativos. Segredos entram pela tela do dono e não são reapresentados.
4. Ative acompanhamento e envio separadamente. O pacote começa desligado e sem regras. Confirme recepção nas contas reais antes da operação comercial.

A verificação de dataset é somente leitura. “Entregue” na fila significa aceite da API, não comprova atribuição a anúncio ou processamento final. O polling recupera estado atual; não inventa etapas intermediárias. Retenção ampliada não restaura eventos anteriormente eliminados.

## Documentação e aceites externos

A documentação completa acompanha o instalador em `wp-content/plugins/base-site-core-fator3/docs/`, acessível também por `f3base/documentacao-ler`. Comece em DOCUMENTACAO.md; veja QUALIDADE-META-1.29.md, CONFIGURACOES-1.29.md e VALIDACAO.md. Catálogos, schemas, dicionário e inventário de dados foram atualizados.

Ainda precisam de homologação no ambiente real: permissões/dataset/eventos Meta, webhook/campos e conversão lead→negócio no Pipedrive, sete dias de captação/Clarity/cron na frota, navegadores internos em aparelhos físicos e limites PHP/proxy. A colocação dos blocos de artigo é do tema/implantador. Esses pontos não foram apresentados como homologados por respostas simuladas.

## Arquivos

| Arquivo | Uso |
|---|---|
| base-site-core-fator3-1.29.0-instalador.zip | Instalação no WordPress |
| base-site-core-fator3-1.29.0-fontes-e-testes.zip | Código, suíte, evidências, plano/pedidos de referência e diff |
| relatorio-core-1.29.0.md | Este relatório |
| impactos-core-1.29.0-mcp-google-tema.md | Encaminhamento aos outros responsáveis |
| SHA256SUMS.txt | Verificação dos artefatos |

SHA-256 do instalador: `6be8fa44c19850662f480d1c3fcdd7dc1326d55d31d9d094bb57cd9ad9c1cc5e`.
