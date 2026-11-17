# Impacto do Fator3 Site Core 1.91.0 em Meta

17/11/2026 · Revisão 1 · Etapa de entrega · Situação aberta · Ação necessária · Pedidos core 423(e)

| Identidade | Versão / SHA-256 |
|---|---|
| Emissor, base instalada | Site Core 1.90.0 · `84a978143955df3803a6724fe5e967e1114b89476e198a52b594d6dc599c660f` |
| Emissor entregue | `base-site-core-fator3-1.91.0-instalador.zip` · `5d0358f62d42a9232ee1bce216bd8ea2b41ea284bc16ef454ad8f9c103aa3e41` |
| Destinatário, instalador examinado | wp-mcp-meta-fator3 0.27.0 · `77e2364a471c41399b6fa5d11feecebabcc1d2722bd5bca89eacbee803733ca6` |
| Patch desta proposta | `tests/191/impactos/wp-mcp-meta-fator3.patch` · `8ddac331d2dc62933b5be8329a5e89709e318f9a96ecaacbf69b089cbe2e2274` |
| Natureza | Bug de confirmação de agendamento e validação coordenada |

## Mudança e consequência

A frota relatou `could_not_set` nos eventos `f3_meta_worker` com o WP Activity Log ativo. O sensor de cron registra callbacks no fim dos filtros WordPress e pode apagar o retorno de uma escrita anterior. No Core esse encadeamento foi reproduzido com os três filtros reais do WP Activity Log 5.7.0. O Core 1.91.0 reposiciona os próprios callbacks para as seis filas que administra. Os eventos deste pacote têm outro proprietário.

## Ação do responsável

Aplicar a proposta a uma cópia de wp-mcp-meta-fator3 0.27.0. Conservar os nomes de hook, opções, estados de trabalho, locks e assinaturas públicas. Validar com o sensor ativo tanto a criação quanto a remoção nativa. Entregar pela próxima release do destinatário, com recibos separados de persistência da agenda e processamento do item.

## Diagnóstico e alteração proposta

Pontos de mudança em `includes/Query.php`, `Jobs::scheduleTickResult()` (chamado por `scheduleTick()`). A proposta fixa o timestamp da tentativa antes da escrita. Se a API devolver `could_not_set`, relê `wp_get_scheduled_event($hook, $args, $quando)`. Somente o registro com aquela identidade confirma a tentativa. Horário diferente, argumentos diferentes ou ausência de evento conservam a falha. O patch preserva a convenção prévia de reaproveitar um worker já agendado. Uma pendência antiga ou fora do prazo exige inspeção e recuperação pelo executor do pacote. 

A partir da raiz do destinatário, use `patch --dry-run -p1 < CAMINHO_DO_PATCH` e, em cópia de desenvolvimento, `patch -p1 < CAMINHO_DO_PATCH`. O diff completo está abaixo e também no fonte do emissor.

```diff
--- a/includes/Query.php
+++ b/includes/Query.php
@@ -90,10 +90,14 @@
             return Store::lock('worker-event', static function () use ($delay) {
                 $hook = Config::KEY.'_worker';
                 if (wp_next_scheduled($hook)) return ['scheduled'=>true,'code'=>'ok'];
-                $result = wp_schedule_single_event(time()+max(5,$delay), $hook, [], true);
+                $when = time()+max(5,$delay);
+                $result = wp_schedule_single_event($when, $hook, [], true);
                 $next = wp_next_scheduled($hook) ?: null;
                 $error = is_wp_error($result) ? sanitize_key($result->get_error_code()) : '';
                 $ok = $next !== null && ($result === true || $error === 'duplicate_event');
+                if ($error === 'could_not_set' && wp_get_scheduled_event($hook, [], $when)) {
+                    $ok = true;
+                }
                 $code = $ok ? 'ok' : ($error ?: 'schedule_unconfirmed');
                 $attempt = ['at'=>time(),'success'=>$ok,'next'=>$next,'code'=>$code];
                 update_option(Config::KEY.'_worker_schedule_attempt', $attempt, false);
```

## Prontidão do emissor e sequência

O Core instalado no Site-Teste expõe a origem, o perfil e os filtros posteriores em `f3base/aplicabilidade-ler`. O contrato do Core para filas próprias está entregue. O destinatário pode corrigir seus eventos em ciclo independente. A presença do patch do destinatário não exige configuração nem uma nova mudança no Core. Não há migração de dados ou nova credencial.

## Validação e limites

O diff aplicou em verificação seca na árvore da versão examinada. Métodos da cópia alterada foram executados em namespace isolado sobre WordPress 7.1.4 e PHP 8.3.36, com funções de agenda controladas. 5 verificações passaram para Meta. Por método, a criação normal e o erro com ocorrência exata retornaram sucesso. Ausência, outro timestamp e outros argumentos retornaram falha. Prova em `tests/191/impactos/prova.php`, resultados em `evidence/1910/wordpress.json`. A instalação oficial do destinatário permaneceu na versão examinada.

A releitura trata a interpretação do retorno pelo pacote. Um erro emitido pelo próprio WordPress ao remover a ocorrência pode continuar no log antes do callback do worker. Para esse caso o responsável deve reproduzir o filtro tardio do WP Activity Log na remoção e verificar a ocorrência, a execução e o log separadamente. Não suprimir globalmente o erro e não marcar trabalho processado só porque a agenda foi confirmada.

## Resposta e encerramento

O responsável por Meta deve retornar a versão que incorpora a correção ou a solução equivalente, o comportamento com WP Activity Log ativo e os recibos por hook, inclusive após remoção e retomada. A proposta segue aberta para incorporação e homologação no pacote oficial.
