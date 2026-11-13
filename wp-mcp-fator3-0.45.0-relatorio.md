# Entrega — Fator3 MCP 0.45.0

Revisão 1 · 13/11/2026 · Implementação e aceite do Pedidos MCP 80 · Slug `wp-mcp-fator3` · **apta-no-escopo-testado**.

## 1. De onde esta versão entra

Instalação limpa ou atualização direta da 0.44.0. O instalador-base tem 935.339 bytes e SHA-256 `a90aa7f2e91ef1033a4a8c6ec320b1e10b45ef657132a40f8aa4215ffa55d5eb`. O fonte-base tem 4.444.369 bytes e SHA-256 `d29b885a45c5b266d1b24f7b650d86e44b2849437bdac073f582223dc188e565`. Os dois WordPress compartilhados informaram 0.44.0 ativa antes da troca.

Requisitos do pacote: WordPress 7.1.4 e PHP 8.3 ou superiores. Bancadas desta rodada: WordPress 7.1.4, PHP 8.3.6, MySQL 8.0.46, plugin isolado e conjunto integrado com Yoast SEO 28.8. Normas conferidas integralmente: `instrucoes-agentes-plugins-fator3.md` e `padrao-desenvolvimento-plugins-fator3.md`, revisão 5 de 02/11/2026 em ambos os arquivos.

## 2. Convivência e encaminhamentos

Na bancada integrada foram ativados Base Site Core 1.81.1, Google 0.34.0, Meta 0.24.1, LinkedIn 0.21.0 e Pipedrive 0.9.0. Tamanhos e hashes constam de `docs/ENTRADAS-TESTE.json`. Os instaladores fornecidos de Core, Google, Meta e LinkedIn conferem com seus relatórios. O hash do Pipedrive 0.9.0 confere com o inventário da edição LinkedIn 0.21.0. O portal de aceite apresentava esse mesmo conjunto. Na conferência imediatamente anterior à troca do MCP no Site-Teste, o Meta estava ativo na 0.25.0. A rodada preservou essa instalação. A matriz de bancada identifica os bytes efetivamente fornecidos.

Foram examinados os relatórios dos pacotes e os encaminhamentos de origem de anúncios entre Core, Google, Meta e LinkedIn. O produtor e o leitor desses dados continuam nos plugins de domínio. As duas novas habilidades usam o servidor MCP e o Yoast no mesmo WordPress. Esta entrega não requer alteração em acompanhantes, pausa de filas nem ordem coordenada de troca. A instalação isolada do servidor permanece funcional.

## 3. Mudanças e evidência

| Pedido | Mudança | Verificação |
|---|---|---|
| Pedidos MCP 80 | `content/get-term-seo` e `content/update-term-seo` para `category` e `post_tag`. Campos `title`, `description` e `indexing`. | Categoria e tag exercitadas com o Yoast 28.8. O índice de cada termo foi relido por identidade e os campos de SEO fora do pedido foram preservados. |
| Pedidos MCP 80 | Revisão vinculada ao alvo, pré-imagem privada, atualização parcial e reconstrução pelo serviço do Yoast. | Conflito de revisão, revisão de outro termo, repetição sem efeito, reparação de índice divergente, restauração de valores anteriores e recusa de gravação por perfil de leitura. |
| Pedidos MCP 80 | Ajuda integrada com procedimento de gravação, conferência no HTML e recuperação. | Índice, schema e documentos completos lidos em sessões MCP novas, antes e depois da atualização. O catálogo instalado passou de 167 para 169 habilidades próprias. As 167 anteriores conservaram os schemas de entrada e saída, os rótulos e as descrições. |

Na bancada, as suítes de instalação e SEO registraram 31 verificações. O teste adicional do endpoint MCP e do HTML público registrou 3 verificações. As sessões do guia registraram 31 verificações. Todas passaram. O verificador documental completou 193 verificações, e os 468 arquivos PHP do instalador passaram no lint com PHP 8.3.6. O ZIP contém 475 arquivos. A reconstrução gerou bytes idênticos. Os scripts estão em `tools/release0450/` e os resultados em `evidencias/0450/`.

## 4. Instalação e prova de prontidão

Na instalação limpa, o servidor iniciou sem acompanhantes e informou a ausência do Yoast ao consultar um termo. Na atualização local, uma categoria com SEO preenchido e uma conexão criadas na 0.44.0 permaneceram legíveis na 0.45.0.

O mesmo instalador foi verificado por slug e SHA-256 e instalado, em sequência, no Site-Teste e no portal do pedido. Cada troca gerou pré-imagem do plugin, sondas HTTP antes e depois e leitura de saúde em nova requisição. Ambos informaram 0.45.0 ativa, saúde positiva e zero recuperações pendentes. Os arquivos temporários de instalação estavam ausentes na conferência final. Os recibos em `evidencias/0450/aceite.json` identificam as operações e as pré-imagens. As notas da 0.45.0 e a leitura SEO responderam no Site-Teste.

**Aceite no portal.** Em `https://www.desenvolvimentodesoftwares.com.br/artigos/categorias/software/`, a habilidade atualizou a metadescrição da categoria 2 com a revisão lida antes da gravação. Resultado: `persisted=true`, `indexable_rebuilt=true`, backup `73a022dac346e4a132c7b391`. A sonda assinada retornou HTTP 200, igualdade do trecho esperado da tag e `cache_bypass_verified=true`. Uma segunda leitura externa do HTML encontrou uma única tag de metadescrição no head, com o valor gravado.

Texto gravado: “Leia artigos sobre desenvolvimento de software e decisões de engenharia. Explore arquitetura, linguagens e APIs para construir, manter e evoluir sistemas com segurança.”

A descrição editorial, consultada pela API pública do WordPress antes e depois, permaneceu “Arquitetura, linguagens, APIs e decisões de engenharia para construir e evoluir sistemas.” O nome, o slug, a contagem de posts, o pai e o link também coincidiram nas duas leituras. A habilidade de gravação recebeu somente a metadescrição. Nenhuma outra categoria foi alvo de escrita no portal.

## 5. Banco, migração e recuperação

O schema próprio permanece em 2. O adaptador lê e grava pelo Yoast e solicita a reconstrução somente do índice do termo escolhido. O WordPress mantém a descrição editorial em outro campo. O fluxo utiliza revisão, lock e backup antes da gravação. Igualdade de valores com índice íntegro retorna sem criar backup. Na bancada, um índice propositalmente divergente foi recomposto mantendo o mesmo ID.

Para recuperar o SEO, exporte a pré-imagem com uma conexão autorizada. Confirme a taxonomia e o ID, releia o termo para obter a revisão vigente e envie os valores anteriores em `content/update-term-seo`. Confira a releitura e o HTML com cache contornado. A restauração pelo mesmo contrato foi exercitada tanto para categoria quanto para tag. A publicação na frota fica com o responsável pela distribuição.

## 6. Alcance da validação

O aceite público abrange a categoria Software. O suporte a tags foi exercitado em WordPress descartável. A matriz cobre o Yoast 28.8. Chamadas a contas de Ads ou CRM e testes comerciais dos acompanhantes ficaram fora desta alteração. A indexação pelos buscadores depende de rastreamento posterior. As verificações confirmam o valor gravado e o HTML servido pelo WordPress.

## 7. Credenciais e configuração do dono

A implementação usa a conta WordPress e o perfil MCP já configurados. Em **Ferramentas → Fator3 MCP → Clientes**, confira o perfil da conexão. Para gravar, a conta precisa editar o termo e ter permissão de metadados avançados ou de configuração do Yoast; o perfil MCP precisa permitir a habilidade. A lista de campos, os efeitos e a recuperação estão em **Ajuda**, no documento de termos. As decisões anteriores sobre o alcance das senhas de aplicação e a descoberta com limite omitido continuam vigentes.

## 8. Identidade dos arquivos

| Artefato | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-fator3-0.45.0-instalador.zip | 939667 | 3659bebf22155807d12f4559cf3d9e7ef7403aec0da45fc661ad90c577c7eab9 |
| wp-mcp-fator3-0.45.0-fonte.zip | 3320693 | df7f460fd1727f2f45046fd60a9e71cabbc3201c32d0702b258f4f3349842059 |

A cópia de referência no fonte antecede o fechamento do próprio arquivo. Este relatório externo identifica os dois ZIPs finais.
