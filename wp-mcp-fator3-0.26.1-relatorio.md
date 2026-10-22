# Entrega — Fator3 MCP 0.26.1

Data: 2026-10-22T12:34:29-03:00. Implementado e instalado no Site-Teste. Entrega final da rodada: **0.26.1**, seguindo patch após a candidata 0.26.0. Não houve publicação em GitHub ou implantação na frota.

## 1. Bases aceitas

Base de desenvolvimento aceita: MCP **0.25.0**. Instalador: 832809 bytes, SHA-256 `7f32527a88514f2f319e02308f491b96b3112b783f1b38791da85aab071ea961`. Fonte: 3005021 bytes, SHA-256 `0ca0f140ba2b234f99067cb704a24aba43a85fd0855ba346a5ca709270c21fe4`. Relatório externo revisão 3 preservado nas entradas; foi a fonte de encerramento de B22.

| Pacote | Base recebida e testada localmente | Site-Teste final |
|---|---|---|
| Fator3 MCP | 0.25.0 → 0.26.1 | 0.26.1 ativo |
| Site Core | 1.46.1 | 1.46.1, preservado |
| MCP Google | 0.17.0 | 0.16.0, preservado |
| MCP Meta | 0.4.1 | 0.4.1, preservado |
| MCP LinkedIn | 0.5.0 | 0.5.0, preservado |

Instaladores recebidos: Core SHA-256 `2e834ba27728a32a22fa588cc05863d1d69ccc2e09b0c05e016d88404eaadc76`; Google `42bd11080b518c82e0960753fa7b08d7adae28743cfcd3e96f9b83bf3f4709b0`; Meta `719e3db7bb55f58cd08c2e78420e06374a6a4b08fad693e849677783ddc82de2`; LinkedIn `dcef9a7b236bdb84055baa4aa6db73ba2fcd3bdd9a7cea30905c2e771a563199`. Manifesto completo de entradas em evidencias/0260/entradas.json; relatórios recebidos em docs/entradas/0260. Resultados declarados nesses relatórios são evidência dos respectivos responsáveis, não ensaios próprios desta entrega.

A aba Fator3 MCP(3) não tinha novo pedido aberto. O escopo novo vem do impacto LinkedIn 0.5.0, **Pedido LinkedIn 6(c)**. Não foi inventado um Pedido MCP 63. Aplicadas as instruções/padrão comuns revisão 4.

## 2. Convivência e encaminhamentos

A instalação continua independente dos acompanhantes. Identidade wp-mcp-fator3/wp-mcp-fator3.php, provider, namespaces, Text Domain, Update URI, URLs MCP e ferramentas-raiz preservados. Contratos server-integration/1.0.0, executor-registration/1.0.0, package-distribution/1.0.0, política 1 e guarda SQL selection-guard/2 mantidos.

Único impacto técnico desta rodada: [encaminhamento ao LinkedIn](sandbox:/workspace/scratch/d7106ddbcd96/release0260/entrega/wp-mcp-fator3-0.26.1-impacto-wp-mcp-linkedin-fator3.md). Foi iniciado antes do código dependente e atualizado na entrega. O MCP oferece mutation-audit/1.0.0 e adapta exclusivamente o evento/leitor público já existente no LinkedIn 0.5.0. Nenhum arquivo dos acompanhantes foi alterado. Core, Google e Meta não exigiram novo encaminhamento de desenvolvimento no escopo avaliado. Isso não equivale a testar todas as suas operações de negócio.

## 3. Mudanças por pedido e evidência

**LinkedIn 6(c):** Registro central recebe referências também de ações originadas no painel. audit/get-operation consulta before/after pelo leitor público do provedor, com administrador, usuário/conexão de origem, política atual e ativo selecionado. Snapshots não são copiados para o banco MCP. Uma referência estável por provedor/operation_id; tentativas MCP e replay ficam correlacionados sem novo efeito de negócio. O painel mostra operação, estado e consulta Antes/Depois; valores são escapados e campos sensíveis redigidos.

**Correção da candidata:** na inspeção real da 0.26.0, um mapeamento de integração nativa revogado fazia a consulta do painel falhar antes de chegar ao diário. A 0.26.1 usa a identidade WordPress nativa, sem reativar esse mapeamento. O escopo temporário permite somente o leitor admitido, mantém seu callback original e fecha em finally. OAuth/Application Passwords continuam sujeitos à conexão e à revogação. A regressão foi incorporada à bancada e conferida no Site-Teste.

**B22/CIMD:** encerrado no Site-Teste em **21/10/2026**, com MCP 0.25.0 e a conexão MCP WP fator3-teste criada pelo usuário. Concessão nova às 10:53:15 −03:00, client_id https://chatgpt.com/oauth/client.json; health às 10:54:21, request_id 1cfab1a4cc0693846b2f6903. Leitura de conexões e documentação pela conexão real confirmada no relatório 0.25.0 revisão 3. Login/consentimento são sustentados pelo grant novo e validações de código/PKCE; não há screenshot dessas telas. Protocolo 2026-07-28 stateless; descoberta efetiva comprovada, sem captura bruta de tools/list. Não foram repetidos renovação/revogação reais do ChatGPT ou testes de toda frota. OAUTH-CIMD e manual vigente agora registram esse encerramento.

## 4. Instalação, prontidão e documentação

| Prova própria | Resultado |
|---|---|
| Lint do instalador final, PHP 8.3.6 | 449 arquivos PHP, zero erro |
| Funcionalidade, fronteira LinkedIn, MCP HTTP e painel nativo | 31 verificações, zero falha |
| Documentos locais e habilidade pública | 22 verificações, zero falha |
| Atualização HTTP nativa 0.25.0 → 0.26.1 | 19 verificações, zero falha |
| Instalação limpa, WordPress 7.1.3 / PHP 8.3.6 | Ativação e leitura em processo novo aprovadas |
| Instalação limpa mínima, WordPress 7.1.2 / PHP 8.3.6 | Ativação, registro do leitor e guia aprovados |
| Site-Teste, WordPress 7.1.3 / PHP 8.3.36 | 0.26.1 ativa, healthy:true |
| Painel real em Chrome | Versão, coluna Operação, detalhe, restrição nativa corrigida e ausência de overflow horizontal conferidos |
| Documentação remota | 21 documentos completos conferidos por bytes/SHA-256 contra o fonte |

A bancada usa WordPress/MySQL/PHP-FPM reais, com respostas LinkedIn sintéticas no limite HTTP. Criação, prévia, confirmação e replay exercitaram o plugin LinkedIn real; **nenhum anúncio/publicação real foi criado**. O caso de sucesso Antes/Depois foi renderizado pelo WordPress local; o navegador do Site-Teste conferiu o painel e o erro controlado de referência inexistente. Não se afirma ensaio visual de mutação de negócio real.

A atualização preservou perfis, tokens/prazos, senha de aplicação, refresh, backups privados, recibos concluídos/incertos e confirmação SQL pendente. O teste aqueceu oito respostas FPM da base e conferiu oito respostas novas, com opcache.validate_timestamps=0. Todos os 457 arquivos do destino corresponderam ao ZIP final, sem extras. Rollback foi simulado com pré-imagem verificada, sem aplicação.

No Site-Teste houve uma troca por vez: 0.25.0 → candidata 0.26.0 → final 0.26.1. Operação final `b7d074fd4c29dd261c03ff7529390a99`, backup imediato `1af6e1d8fbc6cfd8ea92da10`; o backup da base 0.25.0 é `f6d77b4768778b1e25f26072`. Home e REST retornaram 200 após a instalação. Outros plugins, limite de arquivo, retenção SQL, habilitação e canais de atualização foram preservados. ZIPs temporários removidos. A conta/conexão existente foi mantida.

Documentação completa embutida no instalador, disponível por system/guide, sem leitura arbitrária de arquivos: catálogo, paginação UTF-8, versão, revisão e hash. Documentos novos mutation-audit e release-0261; schema efetivo por Get Ability Info. Na conferência remota final, sete documentos alterados foram relidos integralmente; catorze mantiveram os bytes já lidos e tiveram seu hash reconfirmado no catálogo 0.26.1. Manifesto em site-documents.json. Evidências desta rodada em evidencias/0260; os demais diretórios são históricos.

Ambiente de desenvolvimento: PHP 8.3.6 Ubuntu pacote .13, MySQL 8.0.46 e dependências públicas com hashes no manifesto. A distribuição antiga de php8.3-zip .11 não estava mais disponível; foi substituída pela .13 do repositório oficial, registrada com hash. Houve ajustes nos scripts de fixture para retorno de conexão e atualização automática de last_seen; as falhas iniciais não foram omitidas como se fossem provas aprovadas. Notice de tradução antecipada f3base apareceu no ambiente conjunto, sem falha nos testes MCP; não foi alterado código do Core.

## 5. Banco e reversão

Schema SQL continua **2**; não há migração destrutiva, tabela adicional ou limpeza automática. Referências usam o bucket audit existente, com dados mínimos; o diário e seus snapshots continuam pertencendo ao LinkedIn. A retenção explícita da auditoria pode remover a referência sem apagar o diário. Não há importação retroativa de operações anteriores ou recomposição automática de evento perdido.

Retornar os arquivos à base remove a consulta nova e preserva metadados. Reversão deve conferir a pós-imagem e escolher o backup da versão desejada; o backup imediato do Site-Teste contém a candidata 0.26.0, não a base 0.25.0. Rollback de arquivos não desfaz banco ou efeitos externos. O instalador final não reemite tokens nem muda revogações.

## 6. Pendências, limites e responsáveis

- Implementação MCP do impacto LinkedIn 6(c): concluída e coberta pelos ensaios descritos. Não há bloqueio técnico aberto desta entrega.
- Operação real de publicidade/publicação LinkedIn: não executada nesta rodada; responsável LinkedIn/operador decide e autoriza um ensaio de negócio quando necessário. A prova aqui é de integração com transporte sintético.
- Próxima versão LinkedIn: responsável LinkedIn deve adotar explicitamente o descritor público e ajustar a indicação histórica central_audit; o adaptador automático atual é delimitado à 0.5.0. Orientação no impacto técnico, sem modificar o pacote alheio.
- B22 não permanece pendente no Site-Teste. Validação adicional de outros sites ou fluxos reais de renovação/revogação é uma atividade distinta, não implicitamente concluída.
- Distribuição na frota/GitHub fica com o responsável pela frota; não foi executada nesta tarefa. Google 0.17.0 foi usado localmente e não substituiu o 0.16.0 do ambiente compartilhado.

## 7. Credenciais e permissões

Utilizada a conexão OAuth MCP já autorizada e a sessão administrativa existente do navegador. Nenhum segredo real foi incluído no fonte, relatório ou eventos; nenhuma credencial real foi criada, reemitida ou ampliada. Bancada usa valores sintéticos e transporte externo interceptado. Provas incluem não administrador, administrador diferente, perfil sem leitor, ativo removido e Application Password revogada. Snapshot redigido não é material restaurável; o produtor continua responsável por sua projeção pública.

## 8. Arquivos finais

Relatório externo canônico. A cópia dentro do fonte é identificada como anterior ao fechamento; tamanho e hash do próprio fonte são completados somente aqui.

| Arquivo | Bytes | SHA-256 |
|---|---:|---|
| wp-mcp-fator3-0.26.1-instalador.zip | 841342 | `ed8035e6e326ac3c2021bac1ae9c11fde39c26686e1763299b445c3992cb5384` |
| wp-mcp-fator3-0.26.1-fonte.zip | 3127316 | `6457cebb4b4d72489dd40181214c8d85d102e303e40d662e7730c31da67c7c1b` |

- [Instalador](sandbox:/workspace/scratch/d7106ddbcd96/release0260/entrega/wp-mcp-fator3-0.26.1-instalador.zip)
- [Fonte](sandbox:/workspace/scratch/d7106ddbcd96/release0260/entrega/wp-mcp-fator3-0.26.1-fonte.zip)
- [Relatório](sandbox:/workspace/scratch/d7106ddbcd96/release0260/entrega/wp-mcp-fator3-0.26.1-relatorio.md)
- [Impacto LinkedIn](sandbox:/workspace/scratch/d7106ddbcd96/release0260/entrega/wp-mcp-fator3-0.26.1-impacto-wp-mcp-linkedin-fator3.md)

Somente o instalador é instalável. O fonte contém código, build, testes, documentação, entradas e evidências sanitizadas; nenhum ZIP da entrega fica dentro de outro ZIP. A reprodução a partir do fonte extraído deve gerar exatamente o SHA-256 do instalador testado.
