# Entrega — Fator3 Site Core 1.92.1

Revisão 1 · 17/11/2026 · Correção do pedido 428 · base-site-core-fator3  
**Estado: com-pendencias.** Implementação e homologação no Site-Teste concluídas. O aceite do CTO Office requer a distribuição da 1.92.1 pela frota.

## 1. De onde esta versão entra

Instalação limpa ou atualização direta da 1.92.0, reproduzidas com o instalador final. Patch corretivo do ciclo 1.92. Mínimos do projeto: WordPress 7.1.4 e PHP 8.3 de 64 bits. Laboratório: WordPress 7.1.4, PHP 8.4.24 e MariaDB 11.8.6. Site-Teste: WordPress 7.1.4 e PHP 8.3.36.

A base do código é o fonte oficial 1.92.0, SHA-256 e255339e738267714df9d1cdbea0a865cf85a1186a36c239acb428cc26c2e02f. O instalador de origem tem SHA-256 28b2ec8cfc6e24622b2f30cae42582475ff246be493c2b604c86403f5964d7b5. Os nomes restituídos foram lidos no fonte oficial 1.91.0, SHA-256 f780f372f3ffe1417a240eb94f9f2aa7329f5a1d0fb3e270ff6c600d40758f77. O snapshot Google Play é o de 15/11/2026, SHA-256 74f0ced35bdfa216580c030477db29be01f5cc3e62e7196855c7519503d735bd.

Padrões lidos integralmente: instrucoes-agentes-plugins-fator3.md e padrao-desenvolvimento-plugins-fator3.md, ambos revisão 5 de 02/11/2026. Aplicadas também a Regra comum e a aba Fator3 Site Core3 padrão.

## 2. Convivência e encaminhamentos

O Core mantém o contrato 8.44.0, dicionário 8.39.0, perfil piso-padrao-3.6, 104 opções e 197 abilities. A revisão do catálogo passa a 2026-11-17.3. A mudança é interna à seleção de valores. Mantidos os campos, a autorização administrativa, o transporte MCP, a precedência das fichas locais e as integrações. O instalador carrega os mesmos 117 arquivos JavaScript/CSS da base.

Site-Teste e laboratório de atualização com MCP 0.46.0, Google 0.36.0, Meta 0.28.0, LinkedIn 0.25.0, Pipedrive 0.11.1 e WP Activity Log 5.7.0. A instalação limpa foi isolada dos acompanhantes. A revisão do planejamento e a conferência final das fronteiras de MCP, Google, Meta, LinkedIn, Pipedrive e Implantador não identificaram adaptação a encaminhar.

## 3. Pedido 428 e evidência

O CTO Office reproduziu o erro pela consulta administrativa: Model `motorola one macro`, Device `lima`, nome `moto g(8) play`. A igualdade entre Model e Marketing Name havia sido interpretada como sinal suficiente de SKU. Vários produtos compartilham a placa; a igualdade também é comum quando o fabricante publicou o nome comercial nos dois campos.

O compilador agora preserva o nome próprio quando diverge do código em pontuação ou sufixos, quando tem espaço ou palavras de marca/série, ou quando falta formato de SKU. Exige um identificador ASCII compacto com algarismo e separadores internos válidos, filtra mercados e exige evidência comercial de outro Model. Entre irmãos, nomes próprios de venda conflitantes e múltiplas marcas/Devices impedem transferência. Nomes alternativos meramente técnicos também são descartados. O critério completo está em docs/RELEASE-1.92.1.md. A marca é obtida do snapshot, com vocabulário adicional de séries. A execução no site lê fragmentos locais.

**Resultado das 412 trocas.** Foram restituídos literalmente 359 nomes da 1.91.0. Permaneceram 53 inferências que atendem aos controles. Todos os 211 nomes anteriores com espaço foram restituídos. Nesse grupo, 20 já tinham ficha brasileira exata protegendo a exibição e 191 dependiam da correção no índice. A coluna Model isoladamente contém espaço em 212 linhas. A diferença vem de grafias do fornecedor, inclusive sublinhados.

| Código observado | Resultado esperado e verificado no pacote |
|---|---|
| motorola one macro | motorola one macro |
| moto g96 5g | moto g96 5g |
| moto g57 e moto g57 power | cada variante é identificada pelo próprio nome |
| moto g06 power, moto e(7i) power, nokia c12 | nome próprio conforme o fabricante |
| zte 8045 e zte blade a5 2019ru | ZTE 8045 e ZTE Blade A5 2019RU |
| motorola edge 20 | o índice conserva o próprio nome mesmo sem a ficha curada |
| 25062rn2da e lm-x420 | Redmi 15 e LG K40 pelo resolvedor brasileiro |

As 1.352 fichas por código são servidas pelo mesmo arquivo brasileiro da 1.92.0, idêntico em bytes. O índice Google Play conserva os 44.528 códigos. Há 312 famílias regionais aceitas. A família `hlte510` perdeu a unanimidade. Um código ausente dessa família perde a inferência antiga inclusive na projeção de um perfil retido. Os dois códigos brasileiros de controle continuam resolvidos. Uma variante inédita comprovada de Redmi 15, 25062RN2DZ, passou pelo teste. Um código novo sem base fica visível como código pendente.

**Efeitos fora das 412 linhas.** Houve 1.491 diferenças em outras tuplas do índice, das quais 357 mudaram o texto do nome, inclusive grafia. Entre essas 357, 217 antes exibiam um mercado. As demais incluem nomes próprios que recuperaram a grafia do cadastro e escolhas baseadas em linhas do próprio Model após filtrar mercados. A lista integral está em reference/428/outras-diferencas.csv no fonte. Não houve transferência entre Models além das 53 auditadas.

### Decisão individual das 412 trocas

A tabela descreve o índice Google Play anterior à sobreposição brasileira. Na coluna 211, “sim” identifica o subconjunto pedido. “Desfeita” significa retorno exato à 1.91.0. Os motivos consideram primeiro a validade do nome próprio, depois a qualidade da evidência dos irmãos. Um rótulo que é território também consta do motivo.

| Model | Nome 1.91.0 | Nome 1.92.0 | Nome 1.92.1 | Decisão | Grupo 211 | Motivo |
|---|---|---|---|---|---|---|
| 007hw | 007HW | U8850 | 007HW | desfeita | não | candidato sem evidência de nome comercial |
| 008z | 008Z | 009Z | 008Z | desfeita | não | candidato sem evidência de nome comercial |
| 4024x | 4024X | PLAY&#95;P1 | 4024X | desfeita | não | candidato sem evidência de nome comercial |
| 4047d | 4047D | U5 3G | 4047D | desfeita | não | candidato sem evidência de nome comercial |
| 4047g | 4047G | U5 3G | 4047G | desfeita | não | candidato sem evidência de nome comercial |
| 4047n | 4047N | U5 3G | 4047N | desfeita | não | candidato sem evidência de nome comercial |
| 4047x | 4047X | U5 3G | 4047X | desfeita | não | candidato sem evidência de nome comercial |
| 5038d | 5038D | SOUL 4.5 | SOUL 4.5 | mantida | não | código técnico e nome comercial concordante |
| 5056e | 5056E | DLGICELDL1 plus | 5056E | desfeita | não | evidência conflitante no Device |
| 5080u | 5080U | SHINE LITE | 5080U | desfeita | não | evidência conflitante no Device |
| 5g ug phone u23 | 5G UG Phone U23 | Optus X Pro 5G | 5G UG Phone U23 | desfeita | sim | nome próprio com espaço |
| 5g ug tablet t26 | 5G UG Tablet T26 | ZTE Pad X1102N | 5G UG Tablet T26 | desfeita | sim | nome próprio com espaço |
| 6014x | 6014X | 6010A | 6014X | desfeita | não | candidato sem evidência de nome comercial |
| 6016d | 6016D | 6010A | 6016D | desfeita | não | candidato sem evidência de nome comercial |
| 6016e | 6016E | 6010A | 6016E | desfeita | não | candidato sem evidência de nome comercial |
| 6016x | 6016X | 6010A | 6016X | desfeita | não | candidato sem evidência de nome comercial |
| 710c | 710C | Desire 816 | Desire 816 | mantida | não | código técnico e nome comercial concordante |
| 8050d | 8050D | 8050E | 8050D | desfeita | não | candidato sem evidência de nome comercial |
| 8050g | 8050G | 8050E | 8050G | desfeita | não | candidato sem evidência de nome comercial |
| 8050x | 8050X | 8050E | 8050X | desfeita | não | candidato sem evidência de nome comercial |
| 8053 | 8053 | 8057 | 8053 | desfeita | não | candidato sem evidência de nome comercial |
| 8054 | 8054 | 8057 | 8054 | desfeita | não | candidato sem evidência de nome comercial |
| 8055 | 8055 | 8057 | 8055 | desfeita | não | candidato sem evidência de nome comercial |
| 8056 | 8056 | 8057 | 8056 | desfeita | não | candidato sem evidência de nome comercial |
| 9002w | 9002W | 9002A | 9002W | desfeita | não | candidato sem evidência de nome comercial |
| 9002x | 9002X | 9002A | 9002X | desfeita | não | candidato sem evidência de nome comercial |
| 9027g | 9027G | Alcatel 3T 8 | Alcatel 3T 8 | mantida | não | código técnico e nome comercial concordante |
| 9029w | 9029W | Alcatel JOY TAB KIDS | Alcatel JOY TAB KIDS | mantida | não | código técnico e nome comercial concordante |
| a31 | A31 | A13t | A31 | desfeita | não | candidato sem evidência de nome comercial |
| a33f | A33f | A33m | A33f | desfeita | não | candidato sem evidência de nome comercial |
| a460t | A460T | Pixi3-4 TF | Pixi3-4 TF | mantida | não | código técnico e nome comercial concordante |
| a464bg | A464BG | Pixi3-3.5 TF | Pixi3-3.5 TF | mantida | não | código técnico e nome comercial concordante |
| a466bg | A466BG | Pixi4-4 3G Telus | Pixi4-4 3G Telus | mantida | não | código técnico e nome comercial concordante |
| a506zt | A506ZT | nubia S2e | nubia S2e | mantida | não | código técnico e nome comercial concordante |
| a67l | A67L | FOXXD A67L Gen2 | FOXXD A67L Gen2 | mantida | não | código técnico e nome comercial concordante |
| agm x1 | AGM X1 | E20T | AGM X1 | desfeita | sim | nome próprio com espaço |
| airstick | AirStick | TSUTAYA Stick | AirStick | desfeita | não | formato insuficiente para SKU |
| airtel imagine | Airtel Imagine | Celtiis Smart 1 | Airtel Imagine | desfeita | sim | nome próprio com espaço |
| alba 10" | Alba 10" | 101c Platinum | Alba 10" | desfeita | sim | nome próprio com espaço |
| alba 4 | Alba 4 | 40 Neon | Alba 4 | desfeita | sim | nome próprio com espaço |
| alba 4" android | Alba 4" Android | 40d Titanium | Alba 4" Android | desfeita | sim | nome próprio com espaço |
| alba 7 | Alba 7&#92;'&#92;' | 70 Platinum v2 | Alba 7&#92;'&#92;' | desfeita | sim | grafia própria distinta do código |
| alba 7" | Alba 7&#92;'&#92;' | 70 Platinum v2 | Alba 7&#92;'&#92;' | desfeita | sim | grafia própria distinta do código |
| alcatel 4015t | ALCATEL 4015T | ONE TOUCH 4015X | ALCATEL 4015T | desfeita | sim | nome próprio com espaço |
| alcatel 9026s | Alcatel&#95;9026S | A3 10&#92;'&#92;' | Alcatel&#95;9026S | desfeita | não | grafia própria distinta do código |
| alcatel one touch 4027a | ALCATEL&#95;ONE&#95;TOUCH&#95;4027A | PIXI3(4.5) | ALCATEL&#95;ONE&#95;TOUCH&#95;4027A | desfeita | não | grafia própria distinta do código |
| alcatel one touch 4030x | ALCATEL ONE TOUCH 4030X | one&#95;touch&#95;4030&#95;TLVE | ALCATEL ONE TOUCH 4030X | desfeita | sim | nome próprio com espaço |
| alcatel one touch 4037r | ALCATEL ONETOUCH 4037R | ALCATEL ONE TOUCH 4037N | ALCATEL ONETOUCH 4037R | desfeita | sim | grafia própria distinta do código |
| alcatel one touch 5020n | ALCATEL ONE TOUCH 5020N | TCL J300 | ALCATEL ONE TOUCH 5020N | desfeita | sim | nome próprio com espaço |
| alcatel one touch 5036a | ALCATEL ONE TOUCH 5036A | ALCATEL ONE TOUCH 5036D | ALCATEL ONE TOUCH 5036A | desfeita | sim | nome próprio com espaço |
| alcatel one touch 5036f | ALCATEL ONE TOUCH 5036F | ALCATEL ONE TOUCH 5036D | ALCATEL ONE TOUCH 5036F | desfeita | sim | nome próprio com espaço |
| alcatel one touch 5036x | ALCATEL ONE TOUCH 5036X | ALCATEL ONE TOUCH 5036D | ALCATEL ONE TOUCH 5036X | desfeita | sim | nome próprio com espaço |
| alcatel one touch 5037a | ALCATEL&#95;ONE&#95;TOUCH&#95;5037A | ALCATEL ONE TOUCH 5036D | ALCATEL&#95;ONE&#95;TOUCH&#95;5037A | desfeita | não | grafia própria distinta do código |
| alcatel one touch 5037e | ALCATEL ONE TOUCH 5037E | ALCATEL ONE TOUCH 5036D | ALCATEL ONE TOUCH 5037E | desfeita | sim | nome próprio com espaço |
| alcatel one touch 5037x | ALCATEL&#95;ONE&#95;TOUCH&#95;5037X | ALCATEL ONE TOUCH 5036D | ALCATEL&#95;ONE&#95;TOUCH&#95;5037X | desfeita | não | grafia própria distinta do código |
| alcatel one touch 6010x | ALCATEL ONE TOUCH 6010X | ALCATEL ONE TOUCH 601 | ALCATEL ONE TOUCH 6010X | desfeita | sim | nome próprio com espaço |
| alcatel one touch 6030n | ALCATEL ONE TOUCH 6030N | ALCATEL ONE TOUCH 6030X | ALCATEL ONE TOUCH 6030N | desfeita | sim | nome próprio com espaço |
| alcatel one touch 6033a | ALCATEL ONE TOUCH 6033A | ALCATEL ONE TOUCH 6033X | ALCATEL ONE TOUCH 6033A | desfeita | sim | nome próprio com espaço |
| alcatel one touch 6040a | ALCATEL ONE TOUCH 6040A | ALCATEL ONE TOUCH 6040D | ALCATEL ONE TOUCH 6040A | desfeita | sim | nome próprio com espaço |
| alcatel one touch 6040e | ALCATEL ONE TOUCH 6040E | ALCATEL ONE TOUCH 6040D | ALCATEL ONE TOUCH 6040E | desfeita | sim | nome próprio com espaço |
| alcatel one touch 6040x | ALCATEL ONE TOUCH 6040X | ALCATEL ONE TOUCH 6040D | ALCATEL ONE TOUCH 6040X | desfeita | sim | nome próprio com espaço |
| alcatel one touch 930d | ALCATEL ONE TOUCH 930D | Megafon Login | ALCATEL ONE TOUCH 930D | desfeita | sim | nome próprio com espaço |
| alcatel one touch 990a | ALCATEL ONE TOUCH 990A | One Touch 990A | ALCATEL ONE TOUCH 990A | desfeita | sim | nome próprio com espaço |
| alcatel one touch p310a | ALCATEL ONE TOUCH P310A | ONE&#95;TOUCH&#95;P310X | ALCATEL ONE TOUCH P310A | desfeita | sim | nome próprio com espaço |
| alcatel onetouch 4037r | ALCATEL ONETOUCH 4037R | ALCATEL ONE TOUCH 4037N | ALCATEL ONETOUCH 4037R | desfeita | sim | nome próprio com espaço |
| alcatel onetouch p310a | ALCATEL ONETOUCH P310A | ONE&#95;TOUCH&#95;P310X | ALCATEL ONETOUCH P310A | desfeita | sim | nome próprio com espaço |
| alcatel onetouch pop d3 | ALCATEL ONETOUCH POP D3 | ALCATEL ONE TOUCH 4037N | ALCATEL ONETOUCH POP D3 | desfeita | sim | nome próprio com espaço |
| alcatel&#95;one&#95;touch&#95;991&#95;orange | ALCATEL&#95;ONE&#95;TOUCH&#95;991&#95;Orange | ALCATEL ONE TOUCH 991 | ALCATEL&#95;ONE&#95;TOUCH&#95;991&#95;Orange | desfeita | não | marca ou palavra de série no código |
| am-h100 | AM-H100 | IDOL 2 S | AM-H100 | desfeita | não | candidato sem evidência de nome comercial |
| amazing a30 | Amazing A30 | BLADE A320 | Amazing A30 | desfeita | sim | nome próprio com espaço |
| amazing x5s | Amazing X5s | T620 | Amazing X5s | desfeita | sim | nome próprio com espaço |
| android edition by sfr staraddict | Android edition by sfr STARADDICT | SKATE | Android edition by sfr STARADDICT | desfeita | sim | nome próprio com espaço |
| android edition startext | Android Edition StarText | T60 | Android Edition StarText | desfeita | sim | nome próprio com espaço |
| aquos-tvl23b | AQUOS-TVL23B | SHARP PH 2K Smart TV | AQUOS-TVL23B | desfeita | não | marca ou palavra de série no código |
| archos 101c platinum | Archos 101c Platinum | Alba 10 | Archos 101c Platinum | desfeita | sim | nome próprio com espaço |
| archos 70 platinum | Archos 70 platinum | Alba 7 | Archos 70 platinum | desfeita | sim | nome próprio com espaço |
| archos 80c platinum | Archos 80c Platinum | Archos 50c Platinum | Archos 80c Platinum | desfeita | sim | nome próprio com espaço |
| axon 7 mini | AXON 7 mini | B2017G | AXON 7 mini | desfeita | sim | nome próprio com espaço |
| b1-780 | B1-780 | Iconia One 7 | Iconia One 7 | mantida | não | código técnico e nome comercial concordante |
| base lutea 2 | BASE Lutea 2 | SKATE | BASE Lutea 2 | desfeita | sim | nome próprio com espaço |
| base tab 7.1 | BASE Tab 7.1 | V9A | BASE Tab 7.1 | desfeita | sim | nome próprio com espaço |
| beeline smart 2 | Beeline Smart 2 | V815W | Beeline Smart 2 | desfeita | sim | nome próprio com espaço |
| bgh joy x5 | BGH Joy X5 | Blade V580 | BGH Joy X5 | desfeita | sim | nome próprio com espaço |
| blade a310 | BLADE A310 | Blade A462 | BLADE A310 | desfeita | sim | nome próprio com espaço |
| blade a511 | Blade A511 | Blade A515 | Blade A511 | desfeita | sim | nome próprio com espaço |
| blade a6 max | BLADE A6 MAX | ZTE BLADE A0605 | BLADE A6 MAX | desfeita | sim | nome próprio com espaço |
| blade a602 | BLADE A602 | DL2 PLUS | BLADE A602 | desfeita | sim | nome próprio com espaço |
| blade a610 | BLADE A610 | Bland A610 | BLADE A610 | desfeita | sim | nome próprio com espaço |
| blade apex | Blade Apex | Blade G LTE | Blade Apex | desfeita | sim | nome próprio com espaço |
| blade g lte | Blade G LTE | Blade Apex | Blade G LTE | desfeita | sim | nome próprio com espaço |
| blade l5 | Blade L5 | T520 | Blade L5 | desfeita | sim | nome próprio com espaço |
| blade l5 plus | Blade L5 Plus | BLADE L0510 | Blade L5 Plus | desfeita | sim | nome próprio com espaço |
| blade s6 plus | Blade S6 Plus | LS-5503 | Blade S6 Plus | desfeita | sim | nome próprio com espaço |
| blade v+ | Blade V+ | Blade Q Lux | Blade V+ | desfeita | sim | nome próprio com espaço |
| blade v8 | BLADE V8 | BLADE V0800 | BLADE V8 | desfeita | sim | nome próprio com espaço |
| blade v8 mini | BLADE V8 MINI | BLADE V0850 | BLADE V8 MINI | desfeita | sim | nome próprio com espaço |
| blade v8 se | BLADE V8 SE | BLADE V0820 | BLADE V8 SE | desfeita | sim | nome próprio com espaço |
| box r lite 4k | Box R Lite 4K | Kickpi | Box R Lite 4K | desfeita | sim | nome próprio com espaço |
| bush 5" 4g | Bush 5 4G | 50 Helium Plus | Bush 5 4G | desfeita | sim | grafia própria distinta do código |
| bush 5" android | Bush 5" Android | 50c Neon | Bush 5" Android | desfeita | sim | nome próprio com espaço |
| bush 7.0 mytablet | Bush 7.0 MyTablet | 70 Platinum | Bush 7.0 MyTablet | desfeita | sim | nome próprio com espaço |
| bush 8.0 mytablet | Bush 8.0 MyTablet | Archos80cpl&#95;loreal | Bush 8.0 MyTablet | desfeita | sim | nome próprio com espaço |
| bush spira b1 8" | Bush Spira B1 8&#92;'&#92;' | 80 Platinum v2 | Bush Spira B1 8&#92;'&#92;' | desfeita | sim | grafia própria distinta do código |
| bush spira b2 8 tablet | Bush Spira B2 8 tablet | 80 Oxygen | Bush Spira B2 8 tablet | desfeita | sim | nome próprio com espaço |
| bush spira b3 5.5 | BUSH SPIRA B3 5.5 | 55 Cobalt Plus | BUSH SPIRA B3 5.5 | desfeita | sim | nome próprio com espaço |
| bush spira d3 5 | BUSH SPIRA D3 5 | 50d Oxygen | BUSH SPIRA D3 5 | desfeita | sim | nome próprio com espaço |
| bush spira d5.5 dual camera | BUSH SPIRA D5.5 Dual Camera | Archos Sense 55 DC | BUSH SPIRA D5.5 Dual Camera | desfeita | sim | nome próprio com espaço |
| bv4000pro-ru | BV4000Pro&#95;RU | Blackview BV4000Pro | BV4000Pro&#95;RU | desfeita | não | grafia própria distinta do código |
| c103 | C103 | Coolpad C1-U02 | Coolpad C1-U02 | mantida | não | código técnico e nome comercial concordante |
| c106-8 | C106-8 | Cool C1 | Cool C1 | mantida | não | código técnico e nome comercial concordante |
| cameleon c5 | CAMELEON C5 | Accent Camelon C5 | CAMELEON C5 | desfeita | sim | nome próprio com espaço |
| canalatv1 | CANALATV1 | CANAL+ BOX | CANAL+ BOX | mantida | não | código técnico e nome comercial concordante |
| chc-u03 | CHC-U03 | Cherry Mini | Cherry Mini | mantida | não | código técnico e nome comercial concordante |
| chc-u23 | CHC-U23 | Cherry Mini | Cherry Mini | mantida | não | código técnico e nome comercial concordante |
| che2-l11 | Che2-L11 | HONOR 4X | HONOR 4X | mantida | não | código técnico e nome comercial concordante |
| che2-l23 | Che2-L23 | HONOR 4X | HONOR 4X | mantida | não | código técnico e nome comercial concordante |
| che2-tl00 | Che2-TL00 | HONOR 4X | HONOR 4X | mantida | não | código técnico e nome comercial concordante |
| che2-tl00h | Che2-TL00H | HONOR 4X | HONOR 4X | mantida | não | código técnico e nome comercial concordante |
| che2-tl00m | Che2-TL00M | HONOR 4X | HONOR 4X | mantida | não | código técnico e nome comercial concordante |
| che2-ul00 | Che2-UL00 | HONOR 4X | HONOR 4X | mantida | não | código técnico e nome comercial concordante |
| chm-u01 | CHM-U01 | 荣耀畅玩4C | 荣耀畅玩4C | mantida | não | código técnico e nome comercial concordante |
| conexis x1 | ConeXis X1 | BLADE A506 | ConeXis X1 | desfeita | sim | nome próprio com espaço |
| cph1605fw | CPH1605fw | CPH1605 | CPH1605fw | desfeita | não | candidato sem evidência de nome comercial |
| cph1705 | CPH1705 | CHP1705 | CPH1705 | desfeita | não | candidato sem evidência de nome comercial |
| cph1938 | CPH1938 | F11 | CPH1938 | desfeita | não | candidato sem evidência de nome comercial |
| cph2179 | CPH2179 | CPH2185 | CPH2179 | desfeita | não | candidato sem evidência de nome comercial |
| cph2223 | CPH2223 | A74 | CPH2223 | desfeita | não | candidato sem evidência de nome comercial |
| cph2235 | CPH2235 | Reno5 | Reno5 | mantida | não | código técnico e nome comercial concordante |
| cph2239 | CPH2239 | CPH2185 | CPH2239 | desfeita | não | candidato sem evidência de nome comercial |
| cph2241 | CPH2241 | CPH2185 | CPH2241 | desfeita | não | candidato sem evidência de nome comercial |
| cph2309 | CPH2309 | A55s 5G | CPH2309 | desfeita | não | candidato sem evidência de nome comercial |
| cph2365 | CPH2365 | A74 | CPH2365 | desfeita | não | candidato sem evidência de nome comercial |
| cun-al00 | CUN-AL00 | Y5II | CUN-AL00 | desfeita | não | candidato sem evidência de nome comercial |
| cun-tl00 | CUN-TL00 | Y5II | CUN-TL00 | desfeita | não | candidato sem evidência de nome comercial |
| cygnus mini | Cygnus mini | STARSHINE 5 | Cygnus mini | desfeita | sim | nome próprio com espaço |
| cygnus&#95;mini | Cygnus mini | STARSHINE 5 | Cygnus mini | desfeita | sim | grafia própria distinta do código |
| dialog q143l | Dialog Q143L | T82 | Dialog Q143L | desfeita | sim | nome próprio com espaço |
| dive 50 dual | Dive 50 Dual | Dive 50 | Dive 50 Dual | desfeita | sim | nome próprio com espaço |
| dl1018a | DL1018A | CompumaxBlue | DL1018A | desfeita | não | marca ou palavra de série no código |
| dl2 plus | DL2 PLUS | BLADE A602 | DL2 PLUS | desfeita | sim | nome próprio com espaço |
| dtac phone m1 | dtac phone M1 | BLADE A510 | dtac phone M1 | desfeita | sim | nome próprio com espaço |
| e2371ch | E2371CH | Sero7 LE | E2371CH | desfeita | não | marca ou palavra de série no código |
| eda52 | EDA52 | EDA56-0 | EDA52 | desfeita | não | candidato sem evidência de nome comercial |
| explosion | Explosion | CJ-1984 | Explosion | desfeita | não | formato insuficiente para SKU |
| extreme e8 | Extreme E8 | BLADE A910 | Extreme E8 | desfeita | sim | nome próprio com espaço |
| f30 | F30 | L675 | F30 | desfeita | não | candidato sem evidência de nome comercial |
| f5281ch | F5281CH | Sero 8 pro | F5281CH | desfeita | não | marca ou palavra de série no código |
| f52&#95;09 | F52&#95;09 | F52 | F52&#95;09 | desfeita | não | candidato sem evidência de nome comercial |
| frd-l02 | FRD-L02 | Honor 8 | Honor 8 | mantida | não | código técnico e nome comercial concordante |
| gionee f205l | GIONEE F205L | F205 | GIONEE F205L | desfeita | sim | nome próprio com espaço |
| gionee m7l | GIONEE M7L | M7 | GIONEE M7L | desfeita | sim | nome próprio com espaço |
| gn5005 | GN5005 | P7 | GN5005 | desfeita | não | candidato sem evidência de nome comercial |
| gn8003l | GN8003L | M6 | GN8003L | desfeita | não | candidato sem evidência de nome comercial |
| gn9010l | GN9010L | S6 | GN9010L | desfeita | não | candidato sem evidência de nome comercial |
| h5111 | H5111 | Awadjidjè | Awadjidjè | mantida | não | código técnico e nome comercial concordante |
| h5111l | H5111L | H5111L&#95;common | H5111L | desfeita | não | candidato sem evidência de nome comercial |
| h6032 | H6032 | eNOVA | H6032 | desfeita | não | evidência conflitante no Device |
| h6733 pro | H6733 Pro | GH6733 | H6733 Pro | desfeita | sim | nome próprio com espaço |
| helios x1 | Helios X1 | T57 | Helios X1 | desfeita | sim | nome próprio com espaço |
| hisense enigma plus | Hisense Enigma Plus | Hisense U54 | Hisense Enigma Plus | desfeita | sim | nome próprio com espaço |
| hisense infinity e30 lite | Hisense Infinity E30 Lite | Hisense U963 | Hisense Infinity E30 Lite | desfeita | sim | nome próprio com espaço |
| hisense infinity h12 pro | Hisense Infinity H12 Pro | Hisense H20 | Hisense Infinity H12 Pro | desfeita | sim | nome próprio com espaço |
| hk google tv-a | HK Google TV-A | KONKA 4K OLED Google TV | HK Google TV-A | desfeita | sim | nome próprio com espaço |
| hlte311t | HLTE311T | Hisense H20 | HLTE311T | desfeita | não | evidência conflitante no Device |
| hlte501n | HLTE501N | 700T | HLTE501N | desfeita | não | candidato sem evidência de nome comercial |
| hlte510m | HLTE510M | Hisense H20 | HLTE510M | desfeita | não | evidência conflitante no Device |
| hppap33 | HPPAP33 | Puya&#95;Plus | Puya&#95;Plus | mantida | não | código técnico e nome comercial concordante |
| huawei c8813 | HUAWEI C8813 | C8813D | HUAWEI C8813 | desfeita | sim | nome próprio com espaço |
| hw-w900 | HW-W900 | CJ-1984 | HW-W900 | desfeita | não | candidato sem evidência de nome comercial |
| ideatab s2007a-f | IdeaTab S2007A-F | IdeaTV | IdeaTab S2007A-F | desfeita | sim | nome próprio com espaço |
| ideatab s2007a-h | IdeaTab S2007A-H | IdeaTV | IdeaTab S2007A-H | desfeita | sim | nome próprio com espaço |
| ideatab s2010a-d | IdeaTab S2010A-D | IdeaTV | IdeaTab S2010A-D | desfeita | sim | nome próprio com espaço |
| ideatab s2010a-f | IdeaTab S2010A-F | IdeaTV | IdeaTab S2010A-F | desfeita | sim | nome próprio com espaço |
| ideatab s2010a-h | IdeaTab S2010A-H | IdeaTV | IdeaTab S2010A-H | desfeita | sim | nome próprio com espaço |
| k83 | K83 | ZTE ZPAD8 | ZTE ZPAD8 | mantida | não | código técnico e nome comercial concordante |
| kabode max | Kabode Max | 5.99 | Kabode Max | desfeita | sim | nome próprio com espaço |
| karbonn&#95;a1 | Karbonn&#95;A1 | U N721 | Karbonn&#95;A1 | desfeita | não | marca ou palavra de série no código |
| kicka 6 plus 4g | Kicka 6 Plus 4G | Celtiis Smart 1 | Kicka 6 Plus 4G | desfeita | sim | nome próprio com espaço |
| kpn smart 200 | KPN Smart 200 | SKATE | KPN Smart 200 | desfeita | sim | nome próprio com espaço |
| l-ement&#95;tab1040 | L-EMENT TAB 1040 | L-IXIR TAB 1041 | L-EMENT TAB 1040 | desfeita | sim | grafia própria distinta do código |
| l-ement&#95;tab1040&#95;bt | L-EMENT&#95;TAB1040&#95;BT | L-IXIR TAB 1041 | L-EMENT&#95;TAB1040&#95;BT | desfeita | não | marca ou palavra de série no código |
| l2h&#95;edla&#95;gl | L2H&#95;EDLA&#95;GL | Sunmi L2H | Sunmi L2H | mantida | não | código técnico e nome comercial concordante |
| l697 | L697 | E20T | L697 | desfeita | não | candidato sem evidência de nome comercial |
| led39k680x3du | LED39K680X3DU | LED85XT910G3DU | LED39K680X3DU | desfeita | não | marca ou palavra de série no código |
| led42k680x3du | LED42K680X3DU | LED85XT910G3DU | LED42K680X3DU | desfeita | não | marca ou palavra de série no código |
| led50k680x3du | LED50K680X3DU | LED85XT910G3DU | LED50K680X3DU | desfeita | não | marca ou palavra de série no código |
| led50xt900x3du | LED50XT900X3DU | LED85XT910G3DU | LED50XT900X3DU | desfeita | não | marca ou palavra de série no código |
| led55k680x3du | LED55K680X3DU | LED85XT910G3DU | LED55K680X3DU | desfeita | não | marca ou palavra de série no código |
| led55xt900x3du | LED55XT900X3DU | LED85XT910G3DU | LED55XT900X3DU | desfeita | não | marca ou palavra de série no código |
| led58k280u | LED58K280U | LED85XT910G3DU | LED58K280U | desfeita | não | candidato sem evidência de nome comercial |
| led58k680x3du | LED58K680X3DU | LED85XT910G3DU | LED58K680X3DU | desfeita | não | marca ou palavra de série no código |
| led60k380 | LED60K380 | LED85XT910G3DU | LED60K380 | desfeita | não | candidato sem evidência de nome comercial |
| led65k680x3du | LED65K680X3DU | LED85XT910G3DU | LED65K680X3DU | desfeita | não | marca ou palavra de série no código |
| led65xt800x3du | LED65XT800X3DU | LED85XT910G3DU | LED65XT800X3DU | desfeita | não | marca ou palavra de série no código |
| led65xt900x3du | LED65XT900X3DU | LED85XT910G3DU | LED65XT900X3DU | desfeita | não | marca ou palavra de série no código |
| led75xt910g3du | LED75XT910G3DU | LED85XT910G3DU | LED75XT910G3DU | desfeita | não | marca ou palavra de série no código |
| lenovo k11 | Lenovo K11 | moto e6s | Lenovo K11 | desfeita | sim | nome próprio com espaço |
| lenovo k13 | Lenovo K13 | moto e(7i) power | Lenovo K13 | desfeita | sim | nome próprio com espaço |
| lenovo k14 | Lenovo K14 | moto e20 | Lenovo K14 | desfeita | sim | nome próprio com espaço |
| lenovo k14 note | Lenovo K14 Note | moto g31 | Lenovo K14 Note | desfeita | sim | nome próprio com espaço |
| lenovo k14 plus | Lenovo K14 Plus | moto e40 | Lenovo K14 Plus | desfeita | sim | nome próprio com espaço |
| lenovo k15 | Lenovo K15 | moto e32 | Lenovo K15 | desfeita | sim | nome próprio com espaço |
| lenovo tab 2 a7-30dc | LenovoTAB2 A7-30DC | TAB 2 A7-30HC | LenovoTAB2 A7-30DC | desfeita | sim | grafia própria distinta do código |
| lenovo xt2091-7 | Lenovo XT2091-7 | Lenovo K12 Pro | Lenovo XT2091-7 | desfeita | sim | nome próprio com espaço |
| light tab 2w | Light Tab 2W | V9A | Light Tab 2W | desfeita | sim | nome próprio com espaço |
| linx ps474s | Linx PS474S | CJ-1984 | Linx PS474S | desfeita | sim | nome próprio com espaço |
| lm-x420 | LM-X420 | X4(2019) | X4(2019) | mantida | não | código técnico e nome comercial concordante |
| lt100k6900a | LT100K6900A | LED85XT910G3DU | LT100K6900A | desfeita | não | marca ou palavra de série no código |
| m40se&#95;eea | M40SE&#95;EEA | M40SE&#95;ROW | M40SE&#95;EEA | desfeita | não | candidato sem evidência de nome comercial |
| mediapad 7 lite | MediaPad 7 Lite | S7 | MediaPad 7 Lite | desfeita | sim | nome próprio com espaço |
| medion life p4310 | MEDION LIFE P4310 | SKATE | MEDION LIFE P4310 | desfeita | sim | nome próprio com espaço |
| megafon sp-a5 | MegaFon SP-A5 | BLADE | MegaFon SP-A5 | desfeita | sim | nome próprio com espaço |
| megafon v9+ | MegaFon V9+ | V9A | MegaFon V9+ | desfeita | sim | nome próprio com espaço |
| miracle | Miracle | CINK SLIM | Miracle | desfeita | não | marca ou palavra de série no código |
| mobi-buckeye | MOBI-Buckeye | MOBI-SECTV | MOBI-Buckeye | desfeita | não | formato insuficiente para SKU |
| mobi-sectv | MOBI-SECTV | MOBI-Buckeye | MOBI-SECTV | desfeita | não | formato insuficiente para SKU |
| mobicel&#95;z6 | Mobicel&#95;Z6 | Z6 | Mobicel&#95;Z6 | desfeita | não | marca ou palavra de série no código |
| mogo | MoGo | P&#95;FHD&#95;2020 | MoGo | desfeita | não | formato insuficiente para SKU |
| mogo pro | MoGo Pro | P&#95;FHD&#95;2020 | MoGo Pro | desfeita | sim | nome próprio com espaço |
| monte carlo | Monte Carlo | SKATE | Monte Carlo | desfeita | sim | nome próprio com espaço |
| moto e(7i) power | moto e(7i) power | Lenovo K13 | moto e(7i) power | desfeita | sim | nome próprio com espaço |
| moto e32 | moto e32 | Lenovo K15 | moto e32 | desfeita | sim | nome próprio com espaço |
| moto e40 | moto e40 | Lenovo K14 Plus | moto e40 | desfeita | sim | nome próprio com espaço |
| moto g(7) optimo (xt1952dl) | moto g(7) optimo (XT1952DL) | moto g(7) play | moto g(7) optimo (XT1952DL) | desfeita | sim | nome próprio com espaço |
| moto g(9) power | moto g(9) power | Lenovo K12 Pro | moto g(9) power | desfeita | sim | nome próprio com espaço |
| moto g04s | moto g04s | moto g04 | moto g04s | desfeita | sim | nome próprio com espaço |
| moto g06 | moto g06 | moto g06 power | moto g06 | desfeita | sim | nome próprio com espaço |
| moto g06 power | moto g06 power | moto g06 | moto g06 power | desfeita | sim | nome próprio com espaço |
| moto g200 5g | moto g200 5G | motorola edge S30 | moto g200 5G | desfeita | sim | nome próprio com espaço |
| moto g23 | moto g23 | moto g13 | moto g23 | desfeita | sim | nome próprio com espaço |
| moto g37j | moto g37j | moto g77 power | moto g37j | desfeita | sim | nome próprio com espaço |
| moto g51 5g | moto g51 5G | moto g51 | moto g51 5G | desfeita | sim | nome próprio com espaço |
| moto g53 5g | moto g53 5G | moto G53 | moto g53 5G | desfeita | sim | nome próprio com espaço |
| moto g57 | moto g57 | moto g57 power | moto g57 | desfeita | sim | nome próprio com espaço |
| moto g57 power | moto g57 power | moto g57 | moto g57 power | desfeita | sim | nome próprio com espaço |
| moto g96 5g | moto g96 5G | motorola edge 50 fusion | moto g96 5G | desfeita | sim | nome próprio com espaço |
| motorola defy x | motorola defy x | Motorola Defy 2 | motorola defy x | desfeita | sim | nome próprio com espaço |
| motorola edge (2021) | motorola edge (2021) | motorola edge 5G UW (2021) | motorola edge (2021) | desfeita | sim | nome próprio com espaço |
| motorola edge 20 | motorola edge 20 | motorola edge 轻奢版 | motorola edge 20 | desfeita | sim | nome próprio com espaço |
| motorola edge 20 fusion | motorola edge 20 fusion | motorola edge 20 lite | motorola edge 20 fusion | desfeita | sim | nome próprio com espaço |
| motorola edge 20 lite | motorola edge 20 lite | motorola edge 20 fusion | motorola edge 20 lite | desfeita | sim | nome próprio com espaço |
| motorola edge 20 pro | motorola edge 20 pro | motorola edge s pro | motorola edge 20 pro | desfeita | sim | nome próprio com espaço |
| motorola edge 30 fusion | motorola edge 30 fusion | moto S30 | motorola edge 30 fusion | desfeita | sim | nome próprio com espaço |
| motorola edge 5g uw (2021) | motorola edge 5G UW (2021) | motorola edge (2021) | motorola edge 5G UW (2021) | desfeita | sim | nome próprio com espaço |
| motorola edge 60s pro | motorola edge 60s pro | motorola edge 60 pro | motorola edge 60s pro | desfeita | sim | nome próprio com espaço |
| motorola edge 70 | motorola edge 70 | moto X70 Air | motorola edge 70 | desfeita | sim | nome próprio com espaço |
| motorola edge 70 pro | motorola edge 70 pro | motorola edge 70 pro+ | motorola edge 70 pro | desfeita | sim | nome próprio com espaço |
| motorola edge 70 pro+ | motorola edge 70 pro+ | motorola edge 70 pro | motorola edge 70 pro+ | desfeita | sim | nome próprio com espaço |
| motorola edge plus (2022) | motorola edge plus (2022) | motorola edge 30 pro | motorola edge plus (2022) | desfeita | sim | nome próprio com espaço |
| motorola edge plus 5g uw (2022) | motorola edge plus 5G UW (2022) | motorola edge 30 pro | motorola edge plus 5G UW (2022) | desfeita | sim | nome próprio com espaço |
| motorola one 5g ace | motorola one 5G ace | moto g 5G | motorola one 5G ace | desfeita | sim | nome próprio com espaço |
| motorola one 5g uw | motorola one 5G UW | motorola one 5G | motorola one 5G UW | desfeita | sim | nome próprio com espaço |
| motorola one macro | motorola one macro | moto g(8) play | motorola one macro | desfeita | sim | nome próprio com espaço |
| motorola razr 60 ultra | motorola razr 60 ultra | motorola razr ultra 2025 | motorola razr 60 ultra | desfeita | sim | nome próprio com espaço |
| motorola razr 70 | motorola razr 70 | motorola razr 2026 | motorola razr 70 | desfeita | sim | nome próprio com espaço |
| motorola razr 70 plus | motorola razr 70 plus | motorola razr plus 2026 | motorola razr 70 plus | desfeita | sim | nome próprio com espaço |
| motorola razr fold | motorola razr fold | motorola razr fold 2026 | motorola razr fold | desfeita | sim | nome próprio com espaço |
| motorola razr fold 2026 | motorola razr fold 2026 | motorola razr fold | motorola razr fold 2026 | desfeita | sim | nome próprio com espaço |
| motorola razr plus 2026 | motorola razr plus 2026 | motorola razr 70 plus | motorola razr plus 2026 | desfeita | sim | nome próprio com espaço |
| mtc975 | MTC975 | ALCATEL ONE TOUCH 5035D | MTC975 | desfeita | não | marca ou palavra de série no código |
| mxxce4x | MXXCE4X | MXXCE4S | MXXCE4X | desfeita | não | candidato sem evidência de nome comercial |
| mz607 | MZ607 | XOOM 2 | XOOM 2 | mantida | não | código técnico e nome comercial concordante |
| mz608 | MZ608 | XOOM 2 | XOOM 2 | mantida | não | código técnico e nome comercial concordante |
| mz616 | MZ616 | XOOM 2 | XOOM 2 | mantida | não | código técnico e nome comercial concordante |
| n721 | N721 | U N721 | N721 | desfeita | não | candidato sem evidência de nome comercial |
| n9510 | N9510 | Z932L | N9510 | desfeita | não | candidato sem evidência de nome comercial |
| newman n2 | Newman N2 | CJ-1984 | Newman N2 | desfeita | sim | nome próprio com espaço |
| nokia c12 | Nokia C12 | Nokia C12 Pro | Nokia C12 | desfeita | sim | nome próprio com espaço |
| nos neva 80 | NOS NEVA 80 | Blade V770 | NOS NEVA 80 | desfeita | sim | nome próprio com espaço |
| nos novu iii | NOS NOVU III | BLADE A520 | NOS NOVU III | desfeita | sim | nome próprio com espaço |
| nubia 8031 | Nubia 8031 | ZTE 8030 | Nubia 8031 | desfeita | sim | nome próprio com espaço |
| nx402 | NX402 | NX40X&#95;APT | NX402 | desfeita | não | candidato sem evidência de nome comercial |
| one touch p310a | ONE&#95;TOUCH&#95;P310A | ONE&#95;TOUCH&#95;P310X | ONE&#95;TOUCH&#95;P310A | desfeita | não | grafia própria distinta do código |
| optimus monte carlo | Optimus Monte Carlo | SKATE | Optimus Monte Carlo | desfeita | sim | nome próprio com espaço |
| oraimo r401s | oraimo R401S | R401 | oraimo R401S | desfeita | sim | nome próprio com espaço |
| orange monte carlo | Orange Monte Carlo | SKATE | Orange Monte Carlo | desfeita | sim | nome próprio com espaço |
| orange novi | Orange Novi | Blade Apex | Orange Novi | desfeita | sim | nome próprio com espaço |
| own one | Own One | Blade V6 | Own One | desfeita | sim | nome próprio com espaço |
| own one plus | OWN One Plus | Blade V580 | OWN One Plus | desfeita | sim | nome próprio com espaço |
| own s5010 | OWN S5010 | ALCATEL ONE TOUCH 6033X | OWN S5010 | desfeita | sim | nome próprio com espaço |
| p30hd&#95;eea | P30HD | P30HD&#95;ROW | P30HD | desfeita | não | grafia própria distinta do código |
| p30t&#95;y | P30T&#95;Y&#95;EEA | P30T&#95;Y&#95;ROW | P30T&#95;Y&#95;EEA | desfeita | não | grafia própria distinta do código |
| pcrt01 | PCRT01 | Reno3 元气版 5G | Reno3 元气版 5G | mantida | não | código técnico e nome comercial concordante |
| pdst00 | PDST00 | Reno5 Pro 5G | Reno5 Pro 5G | mantida | não | código técnico e nome comercial concordante |
| pemm20 | PEMM20 | A55 5G | PEMM20 | desfeita | não | candidato sem evidência de nome comercial |
| plane 7547s 3g ps7159pg | Plane 7547S 3G PS7159PG | Plane 7547S 3G | Plane 7547S 3G PS7159PG | desfeita | sim | nome próprio com espaço |
| pmt1196&#95;3g | PMT1196&#95;3G | LS96A7G | PMT1196&#95;3G | desfeita | não | candidato sem evidência de nome comercial |
| pmt3077&#95;wi | PMT3077&#95;Wi | MULTIPAD WIZE 3027 | MULTIPAD WIZE 3027 | mantida | não | código técnico e nome comercial concordante |
| pmt3096&#95;3g | PMT3096&#95;3G | LS96A7G | PMT3096&#95;3G | desfeita | não | candidato sem evidência de nome comercial |
| pmt3137&#95;3g | PMT3137&#95;3G | MT3237&#95;3G | PMT3137&#95;3G | desfeita | não | candidato sem evidência de nome comercial |
| pmt3197&#95;w&#95;eu | PMT3197&#95;W&#95;EU | Prestigio SmartKids | PMT3197&#95;W&#95;EU | desfeita | não | marca ou palavra de série no código |
| pmt3437&#95;3g | PMT3437&#95;3G | MT3237&#95;3G | PMT3437&#95;3G | desfeita | não | candidato sem evidência de nome comercial |
| pmt3507&#95;4g | PMT3507&#95;4G | Multipad Wize 3407 4G | PMT3507&#95;4G | desfeita | não | marca ou palavra de série no código |
| pmt3607&#95;4g | PMT3607&#95;4G | Multipad Wize 3407 4G | PMT3607&#95;4G | desfeita | não | marca ou palavra de série no código |
| pmt3718&#95;3g | PMT3718&#95;3G | Prestigio Muze 3708 3G | Prestigio Muze 3708 3G | mantida | não | código técnico e nome comercial concordante |
| pmt4111&#95;3g | PMT4111&#95;3G | CD10A7G | PMT4111&#95;3G | desfeita | não | candidato sem evidência de nome comercial |
| pmt4238&#95;4g&#95;ru | PMT4238&#95;4G&#95;RU | HP8A6L | PMT4238&#95;4G&#95;RU | desfeita | não | marca ou palavra de série no código |
| pmt5771&#95;4g | PMT5771&#95;4G | PMT7781&#95;4G&#95;D&#95;CIS | PMT5771&#95;4G | desfeita | não | marca ou palavra de série no código |
| pmt5791&#95;4g | PMT5791&#95;4G | PMT7781&#95;4G&#95;D&#95;CIS | PMT5791&#95;4G | desfeita | não | marca ou palavra de série no código |
| psp3514duo | PSP3514DUO | WIZE U3 | PSP3514DUO | desfeita | não | marca ou palavra de série no código |
| psp3515duo&#95;ru | PSP3515DUO&#95;RU | MUZE U3 LTE | PSP3515DUO&#95;RU | desfeita | não | marca ou palavra de série no código |
| psp3522duo | PSP3522DUO | Wize J3 | PSP3522DUO | desfeita | não | marca ou palavra de série no código |
| psp5530duo | PSP5530DUO | PSP5531 | PSP5530DUO | desfeita | não | marca ou palavra de série no código |
| psp5553duo | PSP5553DUO | MUZE E5 LTE | PSP5553DUO | desfeita | não | marca ou palavra de série no código |
| pvg100 | PVG100 | Palm | Palm | mantida | não | código técnico e nome comercial concordante |
| pvg100e | PVG100E | Palm | Palm | mantida | não | código técnico e nome comercial concordante |
| px1900 | PX1900 | PX1900ES | PX1900 | desfeita | não | candidato sem evidência de nome comercial |
| px3000 | PX3000 | LED55K360X3D | PX3000 | desfeita | não | candidato sem evidência de nome comercial |
| r7f | R7f | R7 Lite | R7 Lite | mantida | não | código técnico e nome comercial concordante |
| r7g | R7g | R7 Lite | R7 Lite | mantida | não | código técnico e nome comercial concordante |
| r7st | R7st | R7s | R7st | desfeita | não | marca ou palavra de série no código |
| rc8l1t | RC8L1T | RC8L1T-RW1 | RC8L1T | desfeita | não | candidato sem evidência de nome comercial |
| redmi note 9s | Redmi Note 9S | Redmi Note 9 Pro | Redmi Note 9S | desfeita | sim | nome próprio com espaço |
| rm02 | RM02 | arrows M02 | arrows M02 | mantida | não | código técnico e nome comercial concordante |
| rmx3998 | RMX3998 | realme 12 5G | realme 12 5G | mantida | não | código técnico e nome comercial concordante |
| sgh-s730g | SGH-S730G | Amazing | Amazing | mantida | não | código técnico e nome comercial concordante |
| sh930w | SH930W | vizio VP800 | SH930W | desfeita | não | marca ou palavra de série no código |
| sharp 4k tvh | SHARP 4K TVH | SHARP 4K TVT | SHARP 4K TVH | desfeita | sim | nome próprio com espaço |
| smart board mx series (v5) | SMART Board MX Series (V5) | SMART Board® RX Series | SMART Board MX Series (V5) | desfeita | sim | nome próprio com espaço |
| smart tv e | Smart TV E | Miramage Google TV | Smart TV E | desfeita | sim | nome próprio com espaço |
| smart tv p | Smart TV P | Miramage Google TV | Smart TV P | desfeita | sim | nome próprio com espaço |
| smart&#95;green | Smart Green | Verda | Smart Green | desfeita | sim | grafia própria distinta do código |
| smart&#95;plus | SMART&#95; PLUS | alcatel PIXI 4 (5.5) | SMART&#95; PLUS | desfeita | sim | grafia própria distinta do código |
| smarttv 4k m5 | SmartTV 4K M5 | SmartTV 4K L5 | SmartTV 4K M5 | desfeita | sim | nome próprio com espaço |
| solo aspire m | SOLO Aspire M | ALCATEL ONETOUCH POP 3 (5) | SOLO Aspire M | desfeita | sim | nome próprio com espaço |
| sp2 | SP2 | Twist SE | Twist SE | mantida | não | código técnico e nome comercial concordante |
| st1009 | ST1009 | M10 | ST1009 | desfeita | não | marca ou palavra de série no código |
| staraddict ii | STARADDICT II | V970 | STARADDICT II | desfeita | sim | nome próprio com espaço |
| swift 2 | Swift 2 | Swift2 Add-X | Swift 2 | desfeita | sim | nome próprio com espaço |
| swtv-24hk-4k | SWTV-24HK-4K | SWTV-24HK-4K NF | SWTV-24HK-4K | desfeita | não | marca ou palavra de série no código |
| swtv-24hk-4k nf | SWTV-24HK-4K NF | SWTV-24HK-4K | SWTV-24HK-4K NF | desfeita | sim | nome próprio com espaço |
| t47&#95;09 | T47&#95;09 | T47 | T47&#95;09 | desfeita | não | candidato sem evidência de nome comercial |
| tcl d35 | TCL D35 | Soul 3.5 | TCL D35 | desfeita | sim | nome próprio com espaço |
| tcl s530t | TCL S530T | ONE TOUCH 6012D | TCL S530T | desfeita | sim | nome próprio com espaço |
| tcl s950t | TCL S950T | ALCATEL ONE TOUCH 6040D | TCL S950T | desfeita | sim | nome próprio com espaço |
| tecno r6s | TECNO R6S | R6 | TECNO R6S | desfeita | sim | nome próprio com espaço |
| telenor smart | Telenor Smart | ALCATEL ONE TOUCH 985 | Telenor Smart | desfeita | sim | nome próprio com espaço |
| telenor touch pad | Telenor Touch Pad | V9A | Telenor Touch Pad | desfeita | sim | nome próprio com espaço |
| telenor&#95;smart | Telenor&#95;Smart | ALCATEL ONE TOUCH 985 | Telenor&#95;Smart | desfeita | não | marca ou palavra de série no código |
| thinkphone 25 by motorola | ThinkPhone 25 by motorola | motorola edge 60 neo | ThinkPhone 25 by motorola | desfeita | sim | nome próprio com espaço |
| tmn smart a60 | tmn smart a60 | V9800 | tmn smart a60 | desfeita | sim | nome próprio com espaço |
| tmn smart a8 | tmn smarta8 | ALCATEL ONE TOUCH 991 | tmn smarta8 | desfeita | sim | grafia própria distinta do código |
| tt102 | TT102 | V9A | TT102 | desfeita | não | candidato sem evidência de nome comercial |
| u601s pro | U601S  Pro | U601S | U601S  Pro | desfeita | sim | nome próprio com espaço |
| u9500e | U9500E | Ascend D | Ascend D | mantida | não | código técnico e nome comercial concordante |
| v1938ct | V1938CT | V1938A | V1938CT | desfeita | não | candidato sem evidência de nome comercial |
| v2006 | V2006 | X50 Pro | X50 Pro | mantida | não | código técnico e nome comercial concordante |
| v2033 | V2033 | V2054 | V2033 | desfeita | não | candidato sem evidência de nome comercial |
| v2034 | V2034 | V2054 | V2034 | desfeita | não | candidato sem evidência de nome comercial |
| v2039 | V2039 | V2054 | V2039 | desfeita | não | candidato sem evidência de nome comercial |
| v2068 | V2068 | V2054 | V2068 | desfeita | não | candidato sem evidência de nome comercial |
| v2069a | V2069A | vivo Y75s | vivo Y75s | mantida | não | código técnico e nome comercial concordante |
| v2070 | V2070 | V2054 | V2070 | desfeita | não | candidato sem evidência de nome comercial |
| v2102 | V2102 | V2054 | V2102 | desfeita | não | candidato sem evidência de nome comercial |
| v2109 | V2109 | V2110 | V2109 | desfeita | não | candidato sem evidência de nome comercial |
| v2135 | V2135 | T1x | V2135 | desfeita | não | candidato sem evidência de nome comercial |
| v2146 | V2146 | T1x | V2146 | desfeita | não | candidato sem evidência de nome comercial |
| v2180a | V2180A | U5x | V2180A | desfeita | não | candidato sem evidência de nome comercial |
| v2snc&#95;eea | V2sNC | V2s | V2sNC | desfeita | não | grafia própria distinta do código |
| v2snc&#95;ru | V2sNC | V2s | V2sNC | desfeita | não | grafia própria distinta do código |
| v2splusnc&#95;eea | V2sPLUSNC | V2sPLUS | V2sPLUSNC | desfeita | não | grafia própria distinta do código |
| v2splusnc&#95;ru | V2sPLUSNC | V2sPLUS | V2sPLUSNC | desfeita | não | grafia própria distinta do código |
| v8514 | V8514 | V811W | V8514 | desfeita | não | candidato sem evidência de nome comercial |
| v880 | V880 | BLADE | V880 | desfeita | não | evidência conflitante no Device |
| v881 | V881 | 009Z | V881 | desfeita | não | candidato sem evidência de nome comercial |
| v961 | V961 | V970 | V961 | desfeita | não | candidato sem evidência de nome comercial |
| v9e+ | V9e+ | V9A | V9e+ | desfeita | não | formato insuficiente para SKU |
| verda | Verda | Smart Green | Verda | desfeita | não | formato insuficiente para SKU |
| versity 9740 | Versity 9740 | Versity | Versity 9740 | desfeita | sim | nome próprio com espaço |
| versity 9753 | Versity 9753 | Versity | Versity 9753 | desfeita | sim | nome próprio com espaço |
| viva&#95;h701&#95;lte | Viva&#95;H701&#95;LTE | Viva i701G | Viva i701G | mantida | não | código técnico e nome comercial concordante |
| vivo 2018 | vivo 2018 | iQOO Z5 | vivo 2018 | desfeita | sim | nome próprio com espaço |
| vodafone smart chat | Vodafone Smart Chat | T60 | Vodafone Smart Chat | desfeita | sim | nome próprio com espaço |
| x501&#95;usa&#95;om | X501&#95;USA&#95;OM | X501&#95;USA&#95;Cricket | X501&#95;USA&#95;OM | desfeita | não | marca ou palavra de série no código |
| xoom 2 me | XOOM 2 ME | XOOM 2 | XOOM 2 ME | desfeita | sim | nome próprio com espaço |
| xt910k | XT910K | Droid RAZR | Droid RAZR | mantida | não | código técnico e nome comercial concordante |
| xt910s | XT910S | Droid RAZR | Droid RAZR | mantida | não | código técnico e nome comercial concordante |
| y220-u10 | Y220-U10 | Y220 | Y220-U10 | desfeita | não | candidato sem evidência de nome comercial |
| y300 | Y300 | Amber5S&#95;Pro | Amber5S&#95;Pro | mantida | não | código técnico e nome comercial concordante |
| ypy&#95;s350 | Ypy S350 | Ypy S350p | Ypy S350 | desfeita | sim | grafia própria distinta do código |
| z6201v | Z6201V | Verve Connect | Verve Connect | mantida | não | código técnico e nome comercial concordante |
| z755 | Z755 | Grand S Flex | Z755 | desfeita | não | evidência conflitante no Device |
| z793c | Z793C | N9511 | Z793C | desfeita | não | candidato sem evidência de nome comercial |
| z851m | Z851M | ZTE Overture 3 | ZTE Overture 3 | mantida | não | código técnico e nome comercial concordante |
| z930l | Z930L | Blade G LTE | Z930L | desfeita | não | evidência conflitante no Device |
| z998 | Z998 | Blade G LTE | Z998 | desfeita | não | evidência conflitante no Device |
| zte 8030ru | ZTE 8030RU | ZTE 8030 | ZTE 8030RU | desfeita | sim | nome próprio com espaço |
| zte 8045 | ZTE 8045 | Russia | ZTE 8045 | desfeita | sim | nome próprio com espaço e candidato geográfico |
| zte a520s | ZTE A520S | BA603 | ZTE A520S | desfeita | sim | nome próprio com espaço |
| zte a53 | ZTE A53 | ZTE Blade A53+ | ZTE A53 | desfeita | sim | nome próprio com espaço |
| zte b2017 | ZTE B2017 | B2017G | ZTE B2017 | desfeita | sim | nome próprio com espaço |
| zte blade a125 | ZTE BLADE A125 | TE BLADE B125 | ZTE BLADE A125 | desfeita | sim | nome próprio com espaço |
| zte blade a3 2019ru | ZTE Blade A3 2019RU | ZTE Blade A3 2019 | ZTE Blade A3 2019RU | desfeita | sim | nome próprio com espaço |
| zte blade a3 2020ru | ZTE Blade A3 2020RU | ZTE Blade A3 2020 | ZTE Blade A3 2020RU | desfeita | sim | nome próprio com espaço |
| zte blade a5 2019ru | ZTE Blade A5 2019RU | Ukraine, Kazakhstan, Azerbaijan | ZTE Blade A5 2019RU | desfeita | sim | nome próprio com espaço e candidato geográfico |
| zte blade a5 2020ru | ZTE Blade A5 2020RU | ZTE Blade A5 2020 | ZTE Blade A5 2020RU | desfeita | sim | nome próprio com espaço |
| zte blade a51 lite ru | ZTE Blade A51 Lite RU | Nubia N40 | ZTE Blade A51 Lite RU | desfeita | sim | nome próprio com espaço |
| zte blade a520c | ZTE BLADE A520C | BLADE A521 | ZTE BLADE A520C | desfeita | sim | nome próprio com espaço |
| zte blade a53 | ZTE Blade A53 | ZTE Blade A53+ | ZTE Blade A53 | desfeita | sim | nome próprio com espaço |
| zte blade v ultra z982 | ZTE BLADE V Ultra Z982 | ZTE BLade Zmax | ZTE BLADE V Ultra Z982 | desfeita | sim | nome próprio com espaço |
| zte n960 | ZTE N960 | SKATE | ZTE N960 | desfeita | sim | nome próprio com espaço |
| zte v10 | ZTE V10 | V9A | ZTE V10 | desfeita | sim | nome próprio com espaço |
| zte v881 | ZTE V881 | 009Z | ZTE V881 | desfeita | sim | nome próprio com espaço |
| zte v960 | ZTE V960 | SKATE | ZTE V960 | desfeita | sim | nome próprio com espaço |
| zte v970t | ZTE V970T | V970 | ZTE V970T | desfeita | sim | nome próprio com espaço |
| zte-mimosa x | ZTE-Mimosa X | V970 | ZTE-Mimosa X | desfeita | sim | nome próprio com espaço |
| zte-tureis | ZTE-Tureis | T60 | ZTE-Tureis | desfeita | não | marca ou palavra de série no código |
| zte-u v881 | ZTE-U V881 | 009Z | ZTE-U V881 | desfeita | sim | nome próprio com espaço |
| zte-u v960 | ZTE-U V960 | SKATE | ZTE-U V960 | desfeita | sim | nome próprio com espaço |
| zte&#95;u n721 | ZTE&#95;U N721 | U N721 | ZTE&#95;U N721 | desfeita | sim | nome próprio com espaço |
| ztu31 | ZTU31 | Blade V770 | ZTU31 | desfeita | não | evidência conflitante no Device |
| zumbo s 2017 | Zumbo&#95;S&#95;2017 | LAI Zumbo S 2017 | Zumbo&#95;S&#95;2017 | desfeita | não | grafia própria distinta do código |

## 4. Instalação e prova da troca

No Site-Teste o pacote foi preparado em área temporária exclusiva, com SHA-256 conferido antes da instalação. plugins/upload-base64 aplicou expected_slug e expected_sha256. A versão ativa passou de 1.92.0 para 1.92.1. O executor confirmou a conclusão em 17/11/2026 às 20h59min33s, horário de Brasília. O recibo de encerramento mostra zero falhas, zero tarefas com última falha e zero módulos degradados. O arquivo de staging já tinha sido consumido pelo instalador.

| Prova | Ambiente e resultado |
|---|---|
| Reprodução do erro | CTO Office real e controle WordPress local na 1.92.0 devolveram moto g(8) play para motorola one macro. |
| Mesmo perfil após atualização | O perfil sintético foi gravado antes da atualização. Na versão nova, a leitura devolveu motorola one macro e manteve a classe de faixa. O JSON histórico permaneceu intacto. |
| Ability remota na 1.92.1 | No Site-Teste, uma observação sintética com o nome antigo permitiu testar a consulta real. f3base/aparelhos-sem-nome-ler devolveu código e nome motorola one macro, marca Motorola, Device lima. Uma linha de teste inserida, uma removida e zero restantes. |
| Instalação e atualização nativas | Plugin_Upgrader em instalações locais separadas. Todos os 1.270 arquivos instalados conferidos com o manifesto em novos processos, tanto na instalação limpa quanto na atualização. |
| Autorização | Administrador no WordPress isolado executou a ability. A leitura sem privilégio foi recusada. No laboratório com MCP ativo, a CLI recebeu profile_denied e o callback do Core foi testado diretamente. A execução pela conexão MCP foi provada no Site-Teste. |
| Regressão no pacote | Decisões das 412 conferidas nos fragmentos do ZIP e no resolvedor PHP. Treze cenários sintéticos novos no compilador, incluindo marca futura, regiões, nome contendo termo geográfico, conflito entre irmãos e reutilização de Device por outra marca. |
| Integridade | 44.528 códigos, 256 fragmentos, todas as famílias verificadas; recompilação dos 258 arquivos Google Play idêntica em bytes. Lint de 609 PHP, correspondência de 197 abilities com o registro, zero diferenças no ZIP e nenhum ZIP aninhado. |
| Documentação MCP | Índice lido em duas páginas, guia e release integralmente. Texto e SHA-256 conferidos contra o pacote, tentativa de ler ID inexistente recusada. Os recibos sanitizados constam de evidence/1921. |

Prontidão: f3base/como-usar com compacto=true deve informar versao=1.92.1, estado=concluida, falhas=0 e catalogo_aparelhos.revisao=2026-11-17.3. Para distribuição operacional pela frota, conferir o SHA-256 dos bytes no raw de Fator3Ventures/claude-wordpress e passar expected_slug=base-site-core-fator3 e o digest desta entrega a plugins/upload.

## 5. Banco, migração e recuperação

Não há novas tabelas, colunas ou opções. A instalação executa o ciclo normal de versão do Core e troca o índice estático. A observação bruta, a escolha histórica de faixa e as regras locais são preservadas. A leitura de perfis Google Play recalcula a identificação pelo código e remove o nome derivado de famílias retiradas. A configuração local conserva prioridade. Correções posteriores recebem nova versão. Os testes não acionaram Slack, CAPI nem fornecedores.

## 6. Pendências

**Aceite 428 no CTO Office, sob responsabilidade da frota.** A última consulta desta rodada encontrou Core 1.92.0 ativo e o nome antigo. A frota deve instalar o pacote conferido e repetir f3base/aparelhos-sem-nome-ler com {"apos":"motorola one macq","limite":1}. Com o perfil ainda retido, conferir codigo e nome_comercial iguais a motorola one macro e device igual a lima. A distribuição em produção é separada da prova concluída no Site-Teste.

O aceite de 24 horas de cron dos pedidos 423/426 pertence à rodada anterior. A troca do Core no Site-Teste às 20h59 de 17/11 interrompe a permanência contínua na versão exata 1.92.0. Preservar a identificação da versão em qualquer análise dessa janela. O pedido 428 não alterou o código da agenda. A confirmação automática de robots/cabeçalhos no Site-Teste já aparecia normalizada no último resumo de saúde.

O snapshot e os dados geográficos são finitos. Uma futura grafia de mercado ou um nome curto ambíguo ainda pode exigir revisão do cadastro. O pacote aplica o mesmo critério de proteção na recompilação de novos Models, e preserva códigos inéditos sem evidência suficiente. A atribuição comercial entre irmãos é uma inferência documentada.

## 7. Credenciais e configuração do dono

Nenhuma credencial adicional. A operação de leitura requer manage_options. Se houver ficha própria do site, ela pode ser conferida no painel Site Core, na opção Catálogo local de aparelhos, com simulação antes da gravação. O pedido 428 dispensa alterações de configuração.

## 8. Identidade dos arquivos

| Artefato | Nome final | Bytes | SHA-256 |
|---|---|---:|---|
| Instalador | base-site-core-fator3-1.92.1-instalador.zip | 5652556 | 1276d416b79a6f7ac2b0b7d87284aa150a71f9058836467d6886282d12f4a099 |
| Fonte | base-site-core-fator3-1.92.1-fonte.zip | 7905449 | 181209fd00d59643b0c9cfa186caa559ef05a4083b75b102f7719aa12e804106 |

Relatório externo canônico. A cópia incluída no fonte antecede o fechamento do ZIP. A lista das decisões e os testes estão contidos no fonte.
