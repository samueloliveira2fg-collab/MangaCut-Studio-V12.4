# MANGACUT STUDIO — HANDOFF COMPLETO PARA CODEX

**Data da montagem deste pacote:** 21/11/2026  
**Última versão de código confirmada nesta conversa:** `MangaCut Studio V12.4 — Transform Tools Fix` (17/11/2026).  
**Arquivo de release:** `MangaCut_Studio_V12_4_TRANSFORM_TOOLS_FIX.zip`.  
**Status:** esta entrega é um pacote de contexto e fontes de teste. Não é uma nova versão do editor e não contém correções novas feitas nesta montagem.

---

## 0. INSTRUÇÃO PRINCIPAL AO CODEX

Trabalhe a partir da V12.4, preservando o editor atual. Não reescreva tudo do zero e não substitua o motor PSD sem comparação formal. O objetivo é corrigir as deficiências funcionais e a fidelidade de PSD/camadas antes de fazer a refatoração ampla de desempenho.

**Ordem de trabalho acordada com o usuário:**
1. Corrigir erros/bugs funcionais e de arquitetura, com prioridade em PSD, camadas, grupos, máscaras, canais, importação/exportação e ferramentas.
2. Fazer testes reais de importação, edição, exportação e reabertura com os 54 PSDs fornecidos.
3. Corrigir ferramentas de seleção, transformação, pincéis e histórico, sem regressões.
4. Só no final fazer juntos: **(a) otimização geral/arquitetura de armazenamento e memória e (b) treinamento/fine-tuning da IA**.

Não execute fine-tuning agora. Não inicie uma grande migração para tiles ou troca de parser agora. Estude essas arquiteturas e deixe-as preparadas para a fase final, enquanto corrige os problemas de fidelidade.

### Regras de segurança do projeto
- Nunca achatar automaticamente nem descartar grupos/camadas sem aprovação explícita.
- Nunca sobrescrever o PSD original. Exportar para novo arquivo e manter o original intacto.
- Nunca reduzir resolução de exportação. Prévia pode ser reduzida, saída PNG/PSD deve manter dimensões originais.
- Preservar pixels, alfa, coordenadas, bounds, hierarquia, nomes Unicode e modo de cor.
- Se algo não puder ser interpretado/editado, preservar os bytes originais quando tecnicamente possível e avisar precisamente; não fingir compatibilidade completa.
- Mudança estrutural só entra com teste de regressão que compare pixels e árvore de camadas.
- Marcar resultados como PASS, FAIL, BLOCKED ou NOT RUN; nunca reportar teste não executado como aprovado.

---

## 1. OBJETIVO DO PRODUTO

MangaCut Studio é um editor local/offline estilo Photoshop/Photopea, focado em recorte/remoção de fundo de personagens e elementos de mangás/HQs. O desafio central é separar fundo branco de partes brancas legítimas do personagem (olhos, cabelo, roupa, brilho, pele, linhas e áreas fechadas), sem destruir line art, retículas, hachuras, balões ou detalhes finos.

O usuário quer:
- recorte preciso com seleção de objeto, seleção rápida e varinha mágica;
- remoção de fundo e edição de máscaras com pincel apagar/restaurar;
- camadas raster independentes, pastas/grupos aninhados, merge e visibilidade/lock;
- transformações move/scale/rotate/flip sem deslocar o sistema de coordenadas das ferramentas;
- pincéis (round, soft, pencil, ink, marker) e controles de tamanho/opacidade/flow/hardness/smoothing;
- pen tool vetorial / caminhos convertidos em seleção;
- histórico undo/redo confiável;
- importação/exportação PSD com grupos, máscaras, alfa e pixels preservados;
- PNG lossless em resolução integral e projeto `.mcut` editável;
- interface com workspaces: MangaCut original, estilo Photoshop/Photopea e foco Máscaras/Fundo/Camadas;
- atalhos e menus funcionais;
- avisos de RAM sem bloqueio desnecessário, sem limite artificial de resolução;
- manter a interface local no navegador e os originais protegidos.

Créditos desejados no produto: `@edymbk` e `E.D.I.T.H. (assistente IA de edymbk)`.

---

## 2. RELEASE MAIS RECENTE: V12.4

### Arquivo/fonte
- ZIP original: `MangaCut_Studio_V12_4_TRANSFORM_TOOLS_FIX.zip`.
- Código extraído: pasta `MangaCut_Studio_V12_4_TRANSFORM_TOOLS_FIX/`.
- Entry principal: `index.html` (~240 KB).
- Testes: `tests/`.
- IA: `ai_backend/` e `ai_training/`.
- 39 exemplos/referências: `exemplos/painel_01` a `painel_39`.

### O que V12.4 alterou
- Ponteiro é convertido do espaço visual para as coordenadas locais da camada, usando transformação inversa para translação, escala, rotação e espelhamento.
- Pincel, borracha, restauração, varinha, conta-gotas e seleção rápida acompanham a camada transformada.
- Seleção de objeto converte o retângulo visível em quadrilátero no espaço da camada.
- Prévia da máscara e contorno da seleção seguem as transformações da camada.
- Cursor de pincel acompanha escala e rotação.
- Matriz reutilizada por quadro em overlays/prévia.
- Inclui teste de regressão de coordenadas.

### Resultados documentados pelo próprio pacote V12.4
- 5 scripts JS inline: sintaxe PASS.
- Geometria de transformações: identidade/deslocamento, escala 2×, rotação 90°, flip horizontal e bounds: PASS.
- Fixture PSD sintética com 1.501 camadas + 2 grupos aninhados: PASS.
- Fixture Grayscale nativo + alpha: PASS.
- Importação de 54 PSDs reais: 54 PASS, 0 FAIL; 470 camadas raster e 55 grupos no resumo histórico.
- Round-trip individual: cinco arquivos passaram; detalhes abaixo.
- `loki puto.psd`: round-trip pendente porque ultrapassou o limite da execução.
- Teste interativo browser completo: não executado, ambiente bloqueou navegação local.

**Importante:** a auditoria V12.4 contém os resultados acima, mas o arquivo de release não traz os 54 PSDs dentro de `tests/psd_inputs/`. Esta entrega agora os acompanha em três arquivos separados. Codex deve reproduzir todos os testes usando `MANGACUT_PSD_TEST_DIR`.

### Round-trips aprovados na V12.4
- `1.psd`: PASS; 21 camadas; 2 grupos; pixels/estrutura True; modo de cor 3→3.
- `2.psd`: PASS; 17 camadas; 2 grupos; pixels/estrutura True; modo de cor 3→3.
- `6.psd`: PASS; 7 camadas; 2 grupos; pixels/estrutura True; modo de cor 3→3.
- `Gojo Combat.psd`: PASS; 23 camadas; 5 grupos; pixels/estrutura True; modo de cor 3→3.
- `Doriutaaaa.psd`: PASS; 19 camadas; 0 grupos; pixels/estrutura True; modo de cor 1→1.

**Não generalizar 5/54 como round-trip completo.** Os outros 49 foram importados, mas round-trip individual ainda não está documentado como aprovado.

---

## 3. HISTÓRICO RESUMIDO DE EVOLUÇÃO

- **V3/V4:** biblioteca local de painéis de mangá/HQ para estudo de cor, luminosidade, linha, retícula, textura e contornos; 39 referências acumuladas. As referências eram análise visual, não dataset com máscaras de verdade.
- **V7:** expansão de PSDs de teste, camadas, exportação por faixas e limites artificiais de resolução removidos/relaxados; foco em preservar pixels e estruturas.
- **V8:** qualidade de prévia independente da exportação: Auto, 100%, 67%, 45% e 25%; níveis Auto originalmente descritos pelo usuário: ≤3 MP Full, 3–8 MP Medium, 8–26 MP Low, >26 MP Quarter. Exportação deve ficar sempre em 100% original.
- **V9:** grupos/pastas: criar, renomear, recolher, visibilidade, lock, mover, ungroup, merge below, merge folder, merge visible; preservar `lsct` quando possível.
- **V10:** presets de pincel (round, soft, pencil, ink, marker); controles de size/opacity/flow/hardness/smoothing; edição/visualização de máscara.
- **V11:** interface Photopea/Photoshop, menus e atalhos; workspaces visuais desejados (sem alterar o motor de performance).
- **V12.1:** relatório descreve remoção de limites artificiais (40 camadas, limite 1500 parser e limite 120 writer), com avisos em vez de achatamento automático; importação de camadas de PSD mantém grupos quando parser consegue interpretá-los.
- **V12.2:** correções de hierarquia de grupos, ordenação das camadas no writer e tratamento inicial de Grayscale.
- **V12.3:** gravação PSD nativa Grayscale 8-bit, incluindo canal alpha opcional; preservação de modo no `.mcut`.
- **V12.4:** correção de coordenadas de ferramentas em camadas transformadas.

Relatórios de V12.0 a V12.4 estão em `MangaCut_Studio_V12_4_TRANSFORM_TOOLS_FIX/AUDITORIA_TECNICA_V12*.md`.

---

## 4. ACERVO PSD ATUAL

### Inventário verificado agora
- 54 arquivos `.psd` listados na Library e materializados nesta entrega.
- Não foi encontrado `.psb` nesta coleção de 54 arquivos.
- Tamanho total: **1,056,437,472 bytes (0.984 GiB)**.
- Os arquivos reais estão nos três ZIPs de acervo separados (ou já extraídos na pasta `PSDs/`, caso a entrega seja descompactada).
- CSV completo: `PSD_54_INVENTARIO.csv` (tamanho, dimensão, camadas, grupos, avisos, status de import e round-trip).
- SHA256: `PSD_54_MANIFEST_SHA256.json`.

### Observação de proveniência
Os resultados de importação/dimensões/camadas/avisos no CSV foram copiados do relatório JSON incluído na V12.4. O SHA-256 e o tamanho foram calculados novamente nesta montagem, diretamente dos 54 arquivos materializados. A importação não foi rerodada durante a simples montagem do handoff.

### Lista dos 54 PSDs
- `1.psd` — 1159×1647 px; 21 camadas raster; 2 grupos; warnings 0; import PASS; round-trip PASS.
- `10.psd` — 2768×2459 px; 14 camadas raster; 0 grupos; warnings 0; import PASS; round-trip NOT_RUN.
- `14bbbjkut.psd` — 1484×501 px; 5 camadas raster; 0 grupos; warnings 1; import PASS; round-trip NOT_RUN.
- `2.psd` — 1880×2255 px; 17 camadas raster; 2 grupos; warnings 0; import PASS; round-trip PASS.
- `6(1).psd` — 4774×6400 px; 19 camadas raster; 0 grupos; warnings 1; import PASS; round-trip NOT_RUN.
- `6.psd` — 1920×1080 px; 7 camadas raster; 2 grupos; warnings 1; import PASS; round-trip PASS.
- `9.psd` — 1828×1760 px; 14 camadas raster; 0 grupos; warnings 0; import PASS; round-trip NOT_RUN.
- `A quanto tempo que não pode-upscaled-2- (1).psd` — 8640×6704 px; 7 camadas raster; 2 grupos; warnings 1; import PASS; round-trip NOT_RUN.
- `ANDANDO DO RIO.psd` — 5600×7976 px; 8 camadas raster; 2 grupos; warnings 1; import PASS; round-trip NOT_RUN.
- `bicho caverna.psd` — 3352×1918 px; 9 camadas raster; 1 grupos; warnings 1; import PASS; round-trip NOT_RUN.
- `Bloqueia.psd` — 1920×1356 px; 1 camadas raster; 1 grupos; warnings 0; import PASS; round-trip NOT_RUN.
- `Dedin_com_a_bola.psd` — 2740×4000 px; 2 camadas raster; 0 grupos; warnings 0; import PASS; round-trip NOT_RUN.
- `Documento.psd` — 1534×768 px; 2 camadas raster; 0 grupos; warnings 0; import PASS; round-trip NOT_RUN.
- `Doriutaaaa.psd` — 6236×2692 px; 19 camadas raster; 0 grupos; warnings 1; import PASS; round-trip PASS.
- `emo morrendo.psd` — 3420×3094 px; 18 camadas raster; 0 grupos; warnings 1; import PASS; round-trip NOT_RUN.
- `entao_itadori_sera_meu_receptaculo.psd` — 1920×1080 px; 13 camadas raster; 0 grupos; warnings 1; import PASS; round-trip NOT_RUN.
- `Então-upscaled-3-_magic-upscaled-8-.psd` — 2400×1980 px; 6 camadas raster; 3 grupos; warnings 1; import PASS; round-trip NOT_RUN.
- `Eras matança causa-upscaled-7-.psd` — 1352×1176 px; 2 camadas raster; 0 grupos; warnings 0; import PASS; round-trip NOT_RUN.
- `Familia tj.psd` — 3564×2745 px; 5 camadas raster; 0 grupos; warnings 0; import PASS; round-trip NOT_RUN.
- `Gaara humiliating Rock Lee.psd` — 4506×2820 px; 3 camadas raster; 0 grupos; warnings 0; import PASS; round-trip NOT_RUN.
- `Gojo Combat.psd` — 2457×1628 px; 23 camadas raster; 5 grupos; warnings 1; import PASS; round-trip PASS.
- `gojo sofreu os danos (1).psd` — 1920×1080 px; 1 camadas raster; 0 grupos; warnings 0; import PASS; round-trip NOT_RUN.
- `Gojo Vs Sukuna 12.psd` — 5000×3000 px; 6 camadas raster; 1 grupos; warnings 1; import PASS; round-trip NOT_RUN.
- `Guts Agony.psd` — 4182×3024 px; 12 camadas raster; 2 grupos; warnings 2; import PASS; round-trip NOT_RUN.
- `Guts Lyingdown.psd` — 5968×3304 px; 12 camadas raster; 1 grupos; warnings 2; import PASS; round-trip NOT_RUN.
- `hahaha.psd` — 1920×1080 px; 4 camadas raster; 0 grupos; warnings 1; import PASS; round-trip NOT_RUN.
- `hahahacop (2).psd` — 2160×1104 px; 2 camadas raster; 0 grupos; warnings 0; import PASS; round-trip NOT_RUN.
- `hahahacop (4).psd` — 2400×1350 px; 2 camadas raster; 0 grupos; warnings 0; import PASS; round-trip NOT_RUN.
- `Kaiser correndo.psd` — 3840×2160 px; 5 camadas raster; 0 grupos; warnings 1; import PASS; round-trip NOT_RUN.
- `Kurona Zoom Out.psd` — 4800×6836 px; 12 camadas raster; 2 grupos; warnings 1; import PASS; round-trip NOT_RUN.
- `LEVANTANDO.psd` — 5600×7976 px; 13 camadas raster; 4 grupos; warnings 1; import PASS; round-trip NOT_RUN.
- `LEVANTO AGORA SIM.psd` — 5600×7976 px; 4 camadas raster; 1 grupos; warnings 1; import PASS; round-trip NOT_RUN.
- `lidar-upscaled-5-_magic-upscaled-0- (1).psd` — 1556×2400 px; 5 camadas raster; 2 grupos; warnings 0; import PASS; round-trip NOT_RUN.
- `loki puto.psd` — 4608×3584 px; 17 camadas raster; 1 grupos; warnings 1; import PASS; round-trip NOT_RUN.
- `Luffy Gear.psd` — 735×630 px; 5 camadas raster; 0 grupos; warnings 1; import PASS; round-trip NOT_RUN.
- `Mao_gojo_1_parte.psd` — 2768×4000 px; 2 camadas raster; 0 grupos; warnings 0; import PASS; round-trip NOT_RUN.
- `Minato Rasengan.psd` — 2331×2165 px; 6 camadas raster; 1 grupos; warnings 0; import PASS; round-trip NOT_RUN.
- `Naruto And Cloud Strife Combat.psd` — 3400×3152 px; 3 camadas raster; 0 grupos; warnings 0; import PASS; round-trip NOT_RUN.
- `o grande rei-upscaled-7-.psd` — 1472×1850 px; 12 camadas raster; 3 grupos; warnings 0; import PASS; round-trip NOT_RUN.
- `o sukuna ta levando.psd` — 5000×3000 px; 12 camadas raster; 3 grupos; warnings 2; import PASS; round-trip NOT_RUN.
- `Olho_gojo.psd` — 2772×4000 px; 3 camadas raster; 0 grupos; warnings 0; import PASS; round-trip NOT_RUN.
- `os 3.psd` — 3361×1907 px; 3 camadas raster; 0 grupos; warnings 0; import PASS; round-trip NOT_RUN.
- `Puxando a espada.psd` — 3370×4029 px; 27 camadas raster; 0 grupos; warnings 1; import PASS; round-trip NOT_RUN.
- `Rengoku.psd` — 3564×1349 px; 15 camadas raster; 0 grupos; warnings 1; import PASS; round-trip NOT_RUN.
- `Rock Lee and Gaara Fight.psd` — 1692×3180 px; 5 camadas raster; 0 grupos; warnings 0; import PASS; round-trip NOT_RUN.
- `Rocklee Fighting Pose.psd` — 8000×5000 px; 17 camadas raster; 0 grupos; warnings 1; import PASS; round-trip NOT_RUN.
- `Tanjiro cabeça baixa.psd` — 2847×2188 px; 4 camadas raster; 0 grupos; warnings 0; import PASS; round-trip NOT_RUN.
- `Tanjiro corte foda.psd` — 3564×5200 px; 22 camadas raster; 1 grupos; warnings 2; import PASS; round-trip NOT_RUN.
- `toma soco (1).psd` — 3180×1080 px; 8 camadas raster; 3 grupos; warnings 0; import PASS; round-trip NOT_RUN.
- `ubers.psd` — 1890×1417 px; 11 camadas raster; 7 grupos; warnings 1; import PASS; round-trip NOT_RUN.
- `Urahara 6.psd` — 3889×4091 px; 13 camadas raster; 2 grupos; warnings 1; import PASS; round-trip NOT_RUN.
- `william timido.psd` — 2944×4164 px; 4 camadas raster; 0 grupos; warnings 0; import PASS; round-trip NOT_RUN.
- `yuta expansion color.psd` — 3840×2160 px; 20 camadas raster; 2 grupos; warnings 2; import PASS; round-trip NOT_RUN.
- `Ywhach 3.psd` — 2100×2377 px; 4 camadas raster; 0 grupos; warnings 0; import PASS; round-trip NOT_RUN.

### Importação histórica
Todos os 54 estão como PASS na bateria histórica. Isso significa que o parser importou estrutura e reconheceu camadas/grupos sem marcar `flattened=true`; não significa que cada camada preserve todos os recursos avançados do Photoshop ou que todos os 54 já passaram por edição+exportação+reabertura.

### Rodar de novo os testes
Na raiz onde a pasta do projeto e a pasta `PSDs/` são irmãs, definir `MANGACUT_PSD_TEST_DIR`.

PowerShell:
```powershell
$env:MANGACUT_PSD_TEST_DIR = (Resolve-Path .\PSDs).Path
Push-Location .\MangaCut_Studio_V12_4_TRANSFORM_TOOLS_FIX
node --expose-gc .\tests\test_real_psds.cjs
Pop-Location
```

Round-trip é mais pesado e deve ser executado **um PSD por processo**:
```powershell
$env:MANGACUT_PSD_TEST_DIR = (Resolve-Path .\PSDs).Path
Push-Location .\MangaCut_Studio_V12_4_TRANSFORM_TOOLS_FIX
Get-ChildItem $env:MANGACUT_PSD_TEST_DIR -Filter *.psd | Sort-Object Name | ForEach-Object {
  Write-Host "Round-trip: $($_.Name)"
  node --expose-gc .\tests\test_real_roundtrip.cjs $_.Name
  if ($LASTEXITCODE -ne 0) { Write-Warning "Falhou/pendente: $($_.Name)" }
}
Pop-Location
```
Helpers prontos em `FERRAMENTAS_CODEX/`.

---

## 5. DEFICIÊNCIAS CONFIRMADAS NO CÓDIGO V12.4

Estes itens foram identificados por inspeção do `index.html` da V12.4; são problemas reais do caminho de código, não apenas sugestões genéricas.

### P0 — Máscara PSD independente não é regravada como máscara independente
- Reader lê o canal `-2` e cria `userMask`.
- A máscara importada é aplicada visualmente.
- No writer editado, `getLayerImageData()` incorpora o resultado da máscara no alpha da camada.
- O writer serializa canais `[-1,0,1,2]` em RGB ou `[-1,0]` em Grayscale; não emite canal `-2`, mask bounds, defaultColor ou flags como máscara PSD editável independente.
- **Resultado:** recorte visual pode sobreviver, mas a máscara independente PSD pode ser perdida/achatada no alpha depois de editar e reexportar.
- Corrigir: write/read round-trip de máscara com bounds próprios, flags, default color, position e dimensões diferentes das layer bounds; manter mask editável no Photoshop.

### P0 — Pixels de camada fora dos limites do canvas são recortados na importação
- `decodedLayer(info, record)` decodifica dimensões locais `cw/ch`, mas cria `Uint8ClampedArray(w*h*4)` para o documento inteiro.
- Só copia a interseção com canvas (`x0/x1/y0/y1`).
- Há aviso no reader: pixels externos à tela não são preservados no re-export.
- **Resultado:** layers parcialmente fora do documento podem perder conteúdo escondido fora da tela.
- Corrigir: representar bounds originais da layer (`left/top/right/bottom`) e manter todos os pixels mesmo fora do documento; exportar offsets negativos/positivos originais e expandir só na renderização do canvas.

### P1 — Full-canvas RGBA por camada
- Cada layer aloca `w*h*4`, inclusive layer minúscula. O renderizador/exportador e diversas ferramentas assumem arrays full-document.
- Isso é um gargalo estrutural e também uma fonte de risco de falhas em documentos extensos. A otimização geral foi reservada para a fase final, mas preservar os bounds agora é uma correção de fidelidade indispensável.
- Não fazer migração parcial para arrays recortados sem adaptar todos os leitores/consumidores. Registrar o trabalho para a fase final de otimização.

### P1 — Grupo exportado recebe blend mode `norm` fixo
- No writer, o marcador de grupo (`lsct`) é escrito com `8BIM` + blend key `norm`.
- `opacity` e visibilidade são emitidas, mas o blend/pass-through específico do grupo não é preservado pelo writer.
- Corrigir estrutura para armazenar e serializar blend mode e pass-through corretamente, inclusive grupos aninhados.

### P1 — Canais adicionais e metadata PSD são incompletos
- Reader trata principalmente canais `-1,0,1,2` e `-2` (mask). Outros canais não são armazenados/reemitidos como originais.
- Writer gera extras mínimos (Pascal/Unicode layer name e marcador `lsct`); blocks originais `luni`, `lyid`, `lfx2/lrFX`, `vmsk`, Smart Object tags (`SoLd`, `SoLE`), ICC, recursos e blocos desconhecidos não são preservados por completo.
- Corrigir com um inventário de tagged blocks e pass-through de bytes desconhecidos quando seguro; não inventar interpretação para payload desconhecido.

### P1 — blend modes limitados
- O mapa `toCanvasBlend` cobre apenas um subconjunto dos códigos Photoshop; código não mapeado cai em `source-over`.
- Writer converte somente o mapa inverso conhecido; outros modos podem virar `norm`.
- Criar matriz de suporte explícito e testes por modo; para modo sem suporte, preservar bytes e avisar.

### P1 — formatos e profundidades limitados
- Reader rejeita `depth !== 8`.
- Reader aceita apenas RGB (mode 3, pelo menos 3 canais) e Grayscale (mode 1).
- Writer só aceita `colorMode 1 ou 3`; cabeçalho gera 8 bpc.
- RGB16/32, CMYK, Lab, Indexed, Bitmap, Multichannel e PSB não estão completos.
- Header PSD V1 limita width/height e estruturas de tamanho; PSB precisa de parser/writer separado ou implementação consciente de 64-bit lengths.

### P2 — import fallback só composto
- Se nenhum pixel layer é reconhecido, reader usa composição original e marca `flattened=true`/grupos read-only. Esse fallback pode ocorrer em documentos avançados que só tenham tipos de layer não suportados.
- Deve ser comunicado ao usuário antes de qualquer salvamento de projeto, e preservar original intacto.

### P2 — Browser QA incompleto
- A V12.4 não teve teste interativo completo no browser por bloqueio ambiental.
- Testes de coordenadas incluem PASS sintético, mas os checks de selection inspector/overlay foram code checks, não interação manual browser E2E.
- Fazer Playwright/browser tests com gestos reais, sem depender da navegação `file://` bloqueada. Carregar UI via server local controlado em test harness.

---

## 6. PLANO TÉCNICO RECOMENDADO PARA CODEX

### Fase A — harness e testes (antes de alterar o parser)
1. Rodar a bateria 54/54 de importação com `MANGACUT_PSD_TEST_DIR`.
2. Guardar baseline detalhado: header, depth/mode, dimensions, tree, layer bounds, names, visibility, opacity, lock, blend, channel ids, mask bounds, resources/tags, warnings.
3. Rodar round-trip individual para todos os 54 e salvar relatório sem juntar tudo no mesmo processo.
4. Para cada PSD que tem warning, explicar o warning e decidir se é suportado, preservado opaco ou não suportado.
5. Comparar imagem composta original vs export reaberto (pixel diff/PSNR/SSIM quando adequado, mas para pass pixel-perfect usar igualdade exata onde deve ser lossless).
6. Comparar árvore de layers/groups e channels antes/depois.
7. Testar o arquivo de saída em aplicativo compatível (Photoshop/Photopea) quando disponível.

### Fase B — fidelidade PSD/camadas
1. Máscara raster `-2` independente e round-trip exato.
2. Bounds e pixels fora do canvas, sem recorte destrutivo.
3. Groups: blend mode, pass-through, opacity, visibility, nested tree, group mask.
4. Clipping masks, alpha channels e additional channels; channels must not be silently dropped.
5. Tagged blocks e image resources: preserve unknown data raw; maintain layer ID and Unicode names.
6. Efeitos (layer styles), vector masks/paths, Smart Objects: preserve opaque payloads when possible, editability warnings when not supported.
7. Blend modes coverage with exact PSD blend keys.
8. RGB8/Grayscale8 baseline, then RGB16/Grayscale16, RGB32, CMYK 8/16, PSB and other modes by staged test fixtures.

### Fase C — ferramentas e edição
- Brush / eraser / restore on transformed layers and mask-only mode.
- Magic wand: tolerance, contiguous/non-contiguous, add/subtract/intersect, antialias, feather; protect enclosed white figure regions.
- Quick/object selection + refine edge and brush corrections.
- Pen path and conversion to selection.
- Transform and coordinate mapping under nested group transforms.
- Undo/redo atomic, no buffer alias corruption; undo masks/paint/transforms/groups.
- Layer visibility, lock, rename, reorder, drag to group, group merge, merge visible, blend modes.
- Export PNG full-resolution, PSD preserve structure; `.mcut` save/reopen same UI state.

### Fase D — depois, juntas: otimização + IA
**Só executar quando o usuário liberar/chegar à fase final.**
- Considerar sparse tile storage 256×256, lazy decode, COW, immutable snapshots, cache/mipmap, scratch disk/LRU memory budget; adaptar `newLayerSampler`, `getLayerImageData`, thumbnails, mask, save `.mcut`, writer, brush, selection, transforms, compositing and history. Benchmark before/after.
- Fine-tuning IA só com pares de entrada + máscara revisada; não usar PSD cru como ground truth.

---

## 7. ARQUITETURA E BIBLIOTECAS EXTERNAS — PESQUISA

Nenhuma das bibliotecas abaixo foi incorporada à V12.4. O Codex deve clonar/instalar em branch de experiência, fixar versão e executar bateria de comparação antes de adotar.

### PhotoCraft — arquitetura de referência forte
- https://github.com/storytold/photocraft
- Projeto Rust, não dependência JavaScript drop-in.
- Ideias especialmente relevantes: tiles sparse 256×256, copy-on-write via Arc, snapshots imutáveis, lazy decoding, cache/mipmap, compositor CPU como referência e GPU como caminho acelerado, preservar raw PSD tags desconhecidas e decodificar dados só quando pedidos.
- Licença do core reportada como dual MIT/Apache-2.0; revisar `LICENSE`, notices e dependências de terceiros antes de copiar qualquer arquivo. Logos/marcas não são automaticamente licenciados como código.
- O projeto segue alpha e reconhece gaps de compatibilidade/renderer Photoshop. É referência de arquitetura, não prova de compatibilidade total.
- Repos auxiliares: https://github.com/storytold/craft-libs

### ag-psd — candidato JS prioritário para comparação
- https://github.com/Agamnentzar/ag-psd
- MIT. JS/TS, read/write PSD; suporte a dados brutos/lazy, grupos, máscaras e recursos; versões recentes adicionaram melhorias de modos/profundidades e limites de memória.
- Testar versão estável recente fixada, `totalMemoryLimit`, comportamento de entradas malformadas, `useRawData`, `skipLayerImageData`/`skipCompositeImageData` e round-trip em todo corpus. Não confiar sem pixels/tree/channel comparison.

### @webtoon/psd — segundo leitor independente
- https://github.com/webtoon/psd
- MIT, TS, browser/Node, PSD/PSB parser, fornece layer tree/bounds/pixels; não é writer e efeitos são incompletos.
- Usar como diagnóstico cruzado de layer hierarchy/bounds/channels.

### PhotoshopAPI — ferramenta local/QA, não writer final
- https://github.com/EmilDohne/PhotoshopAPI
- BSD-3-Clause, C++20/Python; PSD/PSB, groups, pixel masks, smart objects, ICC e vários color modes/depths.
- Em desenvolvimento inicial; limitações de merged composite export e features planejadas. Bom candidato para parser/validator/fixtures RGB16/CMYK, com validação.

### selection-tools — protótipo de seleção
- https://github.com/techeclecticdesign/selection-tools
- MIT; rectangle/ellipse/lasso/color select/magic wand, bitmap masks, marching ants, selection transform.
- Adaptar somente a lógica/ideias; seu modelo de coordenadas/estado precisa integrar com layers, transforms e undo do MangaCut.

### magic-wand-js
- https://github.com/Tamersoul/magic-wand-js
- MIT; algoritmo de seleção por cor/contorno. Código antigo: referência para comparação, não dependência direta sem testes contra retículas e pixels finos.

### Canvasmith
- https://github.com/laxmanverma/canvasmith
- MIT; referência de editor canvas/headless APIs e undo/redo, não substituto do motor atual.

### ONNX Runtime
- https://github.com/microsoft/onnxruntime
- MIT; já é parte da arquitetura local de IA via Python, e há opção Web futura para estudar quando IA for liberada.

### SkyTNT Anime Segmentation
- Código: https://github.com/SkyTNT/anime-segmentation
- Model: https://huggingface.co/skytnt/anime-seg
- Revisar Apache-2.0 upstream e pinned revision/weights; atualmente usado como modelo base, não treinado pelo usuário.

### Outras ideias a pesquisar com prudência
- OpenCV.js para processamento clássico e seleções/contornos; Apache-2.0 para OpenCV atual, validar pacote/port específico.
- SAM2: https://github.com/facebookresearch/sam2 — Apache-2.0, útil para segmentação assistida em estudo futuro, mas pesado e não afinado especificamente para line art.
- libvips: https://github.com/libvips/libvips — LGPL-2.1-or-later, candidato para processamento de imagens grandes em backend nativo; verificar distribuição/licença.
- IMG.LY background-removal-js: https://github.com/imgly/background-removal-js — AGPL, risco de copyleft; não adotar sem decisão de licença consciente.

### PhotoCraft: o que aproveitar sem copiar o editor inteiro
1. Tile store sparse 256×256 e lazy decode como projeto da futura otimização.
2. `Arc`/COW e snapshots transacionais para histórico.
3. Contrato de compositor CPU determinístico + GPU opcional.
4. Pass-through de tags PSD não interpretadas.
5. Leitura de canal sob demanda e preflight de memória/budget.
6. Teste diferencial de renderização import/export.
7. Separar parser, document model, compositing, UI e tools.

---

## 8. IA / DATASET: RELAÇÃO EXATA COM OS 54 PSDs

- **Nenhum dos 54 PSDs pode ser descrito como usado no treinamento da IA.**
- **Nenhum PSD tem uso em inferência da IA demonstrado em logs ou relatórios desta versão.**
- A evidência disponível confirma uso dos 54 para import test do motor PSD; cinco passaram round-trip individual.
- O pacote contém 39 painéis em `exemplos/`, mas não tem máscaras anotadas pareadas nem manifesto supervisionado.
- Código AI está presente e pode inferir usando o modelo base depois de baixar seus pesos; isso é diferente de treino.
- Não inventar dataset de treinamento, acurácia, percentuais de certeza nem pesos treinados.

Ver `AI_STATUS_E_TREINAMENTO.md` para protocolo e estrutura de dados.

---

## 9. ARTEFATOS INCLUÍDOS NESTA ENTREGA

- `MangaCut_Studio_V12_4_TRANSFORM_TOOLS_FIX.zip` — release original, sem reempacotar.
- `MangaCut_Studio_V12_4_TRANSFORM_TOOLS_FIX/` — fonte extraída com `index.html`, IA, scripts, 39 exemplos, fixtures e auditorias.
- `PSD_54_INVENTARIO.csv` — inventário dos 54 PSDs.
- `PSD_54_MANIFEST_SHA256.json` — hashes/tamanhos e resultados de import registrados.
- `AI_STATUS_E_TREINAMENTO.md` — estado real da IA e protocolo supervisionado.
- `FERRAMENTAS_CODEX/` — scripts PowerShell/Bash para rodar bateria de PSD.
- `RELATORIOS_ANTERIORES/` — summary antigo e relatórios Lote4/Lote5/15 PSDs. `MangaCut_Codex_Resumo.md` é antigo e foi supersedido pela V12.4 e este handoff.
- Três arquivos `MangaCut_PSD_Acervo_...zip`, com os 54 PSDs originais divididos para envio.

---

## 10. PEDIDO DIRETO AO CODEX

Faça uma análise de engenharia, não uma reescrita cosmética. Comece reproduzindo os testes e estudando o motor atual. Em seguida apresente uma matriz de problemas com: local de código, caso de teste que reproduz, impacto nos pixels/estrutura, solução proposta, risco e testes necessários.

Priorize primeiro máscaras PSD independentes e pixels fora do canvas porque são perdas de fidelidade confirmadas pela inspeção. Depois grupos/blend/clipping, extra channels/ICC/tagged blocks, e formatos/profundidades. Só depois atacar seleção, pincéis, histórico e UI que estejam realmente com bug.

Não substituir o writer por `ag-psd`/PhotoCraft/PhotoshopAPI sem demonstrar round-trip 54/54, ou explicar precisamente os arquivos/recursos não suportados e preservar dados desconhecidos.

Cada correção deve:
1. ter teste reproduzível antes/depois;
2. comparar pixels e transparência;
3. comparar layer order/tree, group parent, bounds e canais;
4. manter PSD original intocado;
5. atualizar auditoria e changelog;
6. incluir screenshots/browser test quando a mudança afeta UI.

**Não treinar IA nem realizar a otimização geral nesta etapa.** Deixar ambas como último ciclo combinado pelo usuário.
