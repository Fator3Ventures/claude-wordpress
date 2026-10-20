# Entrega — Fator3 Site Core 1.39.0

Situação: **implementação Core entregue com pendências; bloqueada para implantação em produção**. Escopo exclusivo dos pedidos 230–235 do anexo Fator3 Site Core(7).md. O antigo planejamento 1.39 descartado não integra esta entrega. Data: 20/10/2026 UTC.

## 1. Bases aceitas

Core 1.38.0, instalador de 1.993.463 bytes, SHA-256 `1b0de25e1dd4276fe7f7d8e428dfc0eb01a249d4108f680aa65bd3a4de3e59ee`; fonte SHA-256 `ccaadfd063b4ca803db5988db54a7f78b8a6325ac44fb349b54b6285333fc87d`. Bases mantidas imutáveis. Identidade: `base-site-core-fator3/base-site-core-fator3.php`. Normas comuns revisão 4 e padrão de desenvolvimento lidos. Minor 1.39.0; contrato administrativo aditivo 8.4.0; piso-padrao-3.5 preservado.

## 2. Convivência e encaminhamentos

Site-Teste consultado via WP MCP fator3-teste: Core 1.38.0, MCP 0.24.0 e Google 0.12.0 ativos. Nenhum acompanhante foi modificado, nenhuma mensagem foi enviada, nenhuma publicação na frota foi feita.

- `base-site-core-fator3-1.39.0-impacto-wp-mcp-google-fator3.md`: bloqueio/ação necessária no adaptador de entrega GA4 e Ads. SDK de configuração existente não comprova transporte servidor.
- `base-site-core-fator3-1.39.0-impacto-implantador-base.md`: validação coordenada de novos mapas e contrato 8.4.0. Não declarar pronto enquanto Google não implementar/homologar o adaptador e a meta Ads não for ajustada pelo dono/Datta.

## 3. Mudanças por pedido e evidência

| Pedido | Implementação | Evidência e limite |
|---|---|---|
| 230 | Histórico anterior antes da jornada atual, inclusive sexta sessão em diante; entrada, páginas, tempo visível, cliques e formulários. Notas/complementos consultam sessões já registradas na mesma oportunidade/conta; lock por oportunidade; corte por orçamento explícito. | Journey 27 checagens; notes acrescenta 6 checagens de reenvio/complemento. Histórico paginado 20 sessões, até 500/10.000 eventos; texto 6.500 caracteres. Não afirma histórico ilimitado. Homologação real CTO/Korvena pendente; notas antigas sem diário de sessões não foram retroativamente reconciliadas. |
| 231 | Campanha por ID também para web; objeto nome/parceiro/objetivo; padrão de parceiro por plataforma; legado por nome como último recurso. | Fixtures validam precedência, conta divergente e defaults Google/LinkedIn. Nome original recebido preservado. Configuração real da conta pendente. |
| 232 | Campos fixos validados contra catálogo da conta, somente em lead novo. Mapas vazios por padrão. | Fixture HTTP comprova alternativa 152 em novo lead e preservação do valor 999 em existente. Valores são sintéticos, nenhum hardcode de cliente no runtime. |
| 233 | Oito recortes com motivo de ausência, reservas manuais incluídas, novas fatias antes de retentativas e histórico diário. | 15 checagens com timeout e respostas simuladas. Três dias/12 sites não observados nesta rodada. |
| 234 | Normalização de caminho no vínculo e filtros SQL de saídas. | Sete saídas com barra final reaparecem nos filtros de plataforma e caminho em WordPress real local. Reconciliação CTO 14–19/10 pendente. |
| 235 | Diário por registro/destino, captura de IDs GA4 no mesmo POST com consentimento, worker servidor, confirmação individual, bloqueio de incertos, recuperação administrativa. Meta mantém fila e IDs Pixel/CAPI. | 24 checagens conjuntas de configuração/fila e 6 JavaScript. Google 0.12.0 não oferece o adaptador: GA4/Ads ficam bloqueados. Não há prova de entrega real aos fornecedores. |

Artefatos de evidência no fonte: release-1390, journey-1390, notes-1390, clarity-1390, pipedrive-flow-1390, docs-1390, browser-1390, assets-1390, native-cycles, installer e site-teste-1390. São **188 checagens locais distintas** (notes reutiliza as 27 de journey), além dos ciclos nativos. Pipedrive usa transportes HTTP simulados. Não equivalem a fornecedor real.

## 4. Instalação e prontidão

213 arquivos PHP passaram em lint. Bancada descartável: PHP 8.3.6, WordPress 7.1.3, MySQL 8.0.46. Instalação limpa e atualização direta 1.38.0 → 1.39.0 via Plugin_Upgrader passaram no **ZIP final**, incluindo preservação de opções/dados, callback, listas vazias, procedência e repetição idempotente. Mínimos históricos do cabeçalho não foram novamente homologados.

Documentação instalada: RELEASE-1.39.0.md, AGENTES-1.39.0.md, índices, configuração/ajuda/schema gerados e inventário. 132 abilities, 67 entradas no gerador do catálogo; duas novas abilities administrativas. Teste local de leitura paginada/hash/allowlist e recusa anônima: 69 checagens. No MCP real foi lido o índice da **base 1.38.0**; não é prova da documentação 1.39 instalada remotamente.

Site-Teste não recebeu o candidato: seu Google 0.12.0 ainda não fornece o transporte, e a 1.39 suprime o envio Google de contato pelo navegador. Evitou-se interromper esse fluxo no ambiente compartilhado. Estado final observado: Core 1.38.0 ativo, sem mutação remota nesta rodada. Instalação e leitura da documentação 1.39 pelo MCP real continuam pendentes.

Scripts consentimento/contexto/formulários/leads: gzip nível 9 local 21.306 → **20.125 bytes**, abaixo do teto informado de 21.517. Não é medição HTTP/CDN. Nenhum novo script ou pedido no carregamento; IDs no POST existente. Eventos de materiais permanecem separados.

## 5. Banco e reversão

Nova tabela `f3base_conversoes_servidor`, chave record_id/destino, agenda/estados sem payload pessoal. Instalação idempotente. A captura aceita contém marcador para recuperação de falha de enfileiramento. Novos mapas são aditivos e vazios. Consentimento ausente/revogado impede envio; tráfego de teste é suprimido nesta fila.

Backup inclui banco, diário e guarda operacional. Antes de restore, suspender execuções e reconciliar entregas; restaurar banco antigo pode remover prova de envio. Reversão de arquivos não desfaz envio externo e pode reativar tags antigas. Não apagar diário de idempotência. Eliminação cancela entradas; uninstall preserva o diário. A fila não permite retry de resultado incerto; máximo de dez tentativas com não entrega comprovada.

## 6. Pendências e responsáveis

1. **Google**: implementar `site-conversion-delivery/1.0.0` para GA4 Measurement Protocol e Ads/importação privada, credenciais no próprio Google, validação de destino/resultado individual. Contrato detalhado na documentação e impacto. Valor Ads atual 0 BRL; validar adequação da configuração antes de ativar.
2. **Dono/Datta**: configurar importação Ads como única principal de Contatos e coordenar ações antigas. Meta exige transporte servidor+browser/Lead devidamente configurado. Nada disso foi alterado automaticamente.
3. **Homologação integrada**: Site-Teste com adaptador pronto, MCP documental 1.39, Android WebView/Instagram, consentimento negado e aceitação Meta/GA4/Ads. Simulação/fixtures não encerram 235.
4. **Operação dos sites**: Pipedrive real CTO/Korvena com limpeza dos contatos de teste; comparação histórica CTO para 234; observação Clarity em 12 sites por três dias. Não houve envio de contatos reais nem limpeza de recursos de terceiros.
5. **230 histórico legado**: conferir notas criadas antes do diário de sessões desta versão; nenhuma reconciliação retroativa de notas antigas foi executada. O orçamento/paginação são limites explícitos da apresentação.
6. **Implantador**: validar novo schema e merge/CAS/readback, sem copiar IDs entre contas.

Até esses aceites, esta é uma entrega de implementação revisável, **não autorização técnica de produção nem encerramento integral dos pedidos**.

## 7. Credenciais

Nenhuma credencial real acrescentada ou distribuída. Fixtures usam segredos sintéticos somente na bancada; ZIPs não contêm banco, cookies, runtimes ou credenciais da hospedagem. Segredos GA4/Ads pertencem ao plugin Google; tokens existentes de CRM/Meta não foram alterados.

## 8. Arquivos finais

| Artefato | Nome | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | base-site-core-fator3-1.39.0-instalador.zip | 2004862 | `e0ab847ebb1f2490656e19300f7254431ce8c6be6d095e0432b68d1b1cda9938` |
| Fonte | base-site-core-fator3-1.39.0-fonte.zip | 2096129 | `3eacddaac2d6ae506fc3ae448f7cc1c7973c83502a04105ae4ae38c43b1ee807` |

Somente instalador é instalável, raiz `base-site-core-fator3/`. Fonte possui código/build/testes/evidências sanitizadas e cópia deste relatório anterior ao fechamento. O hash final do fonte consta somente neste relatório externo. Nenhum ZIP contém outro ZIP da entrega.
