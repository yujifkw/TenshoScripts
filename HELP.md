<h1 id="-português"></h1>
<div align="left">
  <a href="#-english">
    <img src="https://img.shields.io/badge/Lang-English-blue?style=for-the-badge&logo=united-kingdom" alt="English">
  </a>
</div>

# 🐉 Documentação Oficial: TenshoScripts v1.0.3

Bem-vindo à documentação técnica do **TenshoScripts**. Este toolkit foi projetado para levar o Aegisub ao limite, focando em automações de Motion Graphics para a cena **Nerdcore** e **AMVs**, resolvendo limitações históricas de outros scripts.

---

## 🛠️ Diferenciais Técnicos da Engine

* **Navegação em State Machine:** Transite entre ferramentas, painéis básicos e avançados de forma contínua usando o botão **"Voltar"**, sem duplicar processamento ou fechar o script.
* **Blindagem UTF-8 (Anti-Crash):** Captura segura de caracteres de 1 a 4 bytes, eliminando o clássico *C++ Exception* ao fatiar letras acentuadas ou emojis.
* **Motor de "Culling" e Limite de 40ms:** Ferramentas de fatiamento contínuo geram as fatias apenas onde a animação ocorre, envelopando o tempo inativo em "Linhas Clean" estáticas. Isso reduz o peso do arquivo `.ass` em até 80% e elimina travamentos no player de vídeo.
* **Motor de Viagem no Tempo:** Fatiar uma linha normalmente quebra tags como `\fad` e `\t`. O TenshoScripts recalcula dinamicamente os tempos absolutos dessas tags para tempos relativos (suportando offsets negativos nativos do VSFilter), mantendo seus fades e blurs perfeitamente intactos nas fatias.

---

## 1. Fadeworks Adaptado
Aplica transições de visibilidade complexas de forma simplificada, unindo Alpha e Cor.

![GUI Fadeworks](ASSETS/fadeworks_pt.png)

### Parâmetros:
* **Fade In/Out:** Duração em milissegundos da entrada e saída ou porcentagem relativa (`0.4` fará o fade em 40% do tempo da linha).
* **Alpha/Colour:** Define se o efeito afetará apenas a transparência ou se haverá transição de cores cruzadas.
* **From/To:** Cores de início e fim do fade.
* **By Letter:** Ativa o sequenciamento caractere por caractere (com purga automática de tags de karaoke residuais para evitar quebra do retextmod).
* **Direção:** Escolha entre `LTR` (esquerda para direita), `RTL` (direita para esquerda), `Meio->Fora` ou `Fora->Meio` (com cálculo radial perfeito para números pares e ímpares de caracteres).

---

## 2. Gradiente Fácil (Multi-Ponto)
Gera gradientes letra por letra com até 5 cores chave e interpolação avançada, ou automaticamente através de Estilos.

<div align="center">
  <table>
    <tr>
      <td align="center" width="50%">
        <strong>Gradiente Multi-Ponto</strong><br>
        <img src="ASSETS/gradient_pt.png" alt="GUI Gradient">
      </td>
      <td align="center" width="50%">
        <strong>Gradiente: Transição de Estilo</strong><br>
        <img src="ASSETS/gradient_sty_pt.png" alt="GUI Gradient Styles">
      </td>
    </tr>
  </table>
</div>

### Parâmetros:
* **Interpolar HSL:** Transita as cores pelo espectro de Matiz, Saturação e Luminosidade em vez do espaço RGB, resultando em cores vibrantes que não passam por tons de cinza ou marrom no meio do caminho.
* **Cores Chave (1-5):** Define os pontos de parada. Ative as cores intermediárias para gradientes ultracomplexos.
* **Checkboxes Target:** Aplique o gradiente seletivamente apenas em tags específicas (`\c`, `\3c` ou `\4c`).
* **Estilos (A, B, C):** Lê automaticamente sua tabela de estilos. Transição linear (A -> B) ou ancorada em três pontos (A -> C -> B).
* **Interpolação Completa:** Transita matematicamente cores, bordas (`\bord`), sombras (`\shad`) e tamanhos (`\fs`), gerando efeitos de perspectiva 3D ou crescimento orgânico do texto.

---

## 3. Flashes
Ideal para sincronizar o impacto visual com a batida da música.

![GUI Flashes](ASSETS/flashes_pt.png)

### Parâmetros:
* **Cor do Flash:** Cor que a legenda assumirá durante o pico (BPM).
* **Intervalo (ms):** Define o tempo entre as alternâncias.
* **Suavizar Transição:** Quando desmarcado, faz cortes secos. Quando marcado, cria um efeito pulsante interligando os flashes com `\t`.

---

## 4. Split Lines
Divide frases em camadas individuais mantendo o layout original estrito.

![GUI Split](ASSETS/split_pt.png)

### Funcionalidades:
* **Modos:** Dividir por **Caractere** ou por **Palavra**.
* **Preservação Tipográfica:** Extrai e remonta tags globais e locais, incluindo `\fs` original e ancoragens horizontais.
* **Filtro de Vácuo:** Detecta espaços e calcula sua métrica (`text_extents`) para manter o kerning correto, mas aborta a criação de linhas inúteis vazias na grid.

---

## 5. Transform (\t)
Criação rápida de animações de transição temporal.

![GUI Transform](ASSETS/transform_pt.png)

### Parâmetros:
* **Intervalo (ms):** Define tempo de Início e Fim (o fim herda a duração da linha por padrão).
* **Alvos de Cor & Tamanho:** Permite transicionar `\1c`, `\2c`, `\3c`, `\4c`, escalar fonte (`\fs`) e opacidade global (`\alpha`) simultaneamente.

---

## 6. Texto & Fontes FX
Um poderoso motor integrado de motion tipográfico. Substitui o antigo Random Fonts e engloba 5 ferramentas de manipulação letreiral com geração de "linhas clean" dinâmicas.

![GUI TextFX](ASSETS/textfx_pt.png)

### Efeitos Disponíveis:
* **Variar Fontes:** Sorteia fontes de uma lista predefinida. **Normalização Inclusa:** Utiliza um dicionário de "Altura-X" invisível para corrigir a caixa das fontes (ex: *Lucida Console* ganha escala diferente para não "murchar" perto da *Roboto*).
* **Typewriter (Máquina de Escrever):** Revela as letras em sequência baseada em `ms/char`. 
* **Embaralhar (Unscramble):** Efeito de descriptografia (Hacking). Antes de revelar a letra real, exibe símbolos aleatórios por 120ms.
* **Caos Símbolos:** O texto sofre corrupção contínua ao longo do tempo (30% de chance de virar um caractere corrompido a cada frame fatiado).
* **Inverter Letras:** Substitui letras pelos seus equivalentes espelhados em código Unicode. Se as direções **Horizontal (X)** ou **Ambos (X+Y)** forem escolhidas, a string inteira é reordenada de trás pra frente (Espelho Verdadeiro).

### A Mágica do "Pulo Dinâmico" (Centralizar)
Ao ativar o **Pulo Dinâmico** no Typewriter ou Embaralhar, as sílabas que ainda não foram reveladas são fisicamente *apagadas* da linha em vez de apenas escondidas com alpha. Se a sua linha tiver alinhamento central (`\an5`, `\an8`, etc), a frase inteira se recalcula e "pula" para o centro a cada nova letra impressa na tela!

---

## 7. YtktFade
Otimizador de compressão para YouTube.

![GUI Ytkt](ASSETS/ytkt_pt.png)

### Parâmetros:
* **Alpha Constante:** Injeta alphas que forçam os renderizadores web (VP9/AV1) a manter a qualidade da borda do karaokê.
* **Ativar \2c:** Aplica cores secundárias de preenchimento.

---

## 8. FixLines
Padronização de posição por cálculos matemáticos relativos.

![GUI FixLines](ASSETS/fix_pt.png)

### Funcionalidades:
* **Forçar Alinhamento (\an5):** Anula alinhamentos prévios e centraliza o ponto de âncora.
* **Cálculo Delta:** Captura a resolução real (`PlayRes`) e posiciona legendas em exata proporção.

---

## 9. Glitch Dinâmico (Pago)
Gerador avançado de aberração cromática (RGB Split) estático e animado.

![GUI Glitch](ASSETS/glitch_pt.png)

### Diferenciais Técnicos:
* **Flicker Tipográfico:** Ative "Negrito" ou "Itálico" e o motor joga uma moeda (50% de chance) a cada frame gerado por camada: o glitch piscará com quebra de peso de fonte durante o tempo da distorção, criando um visual extremamente agressivo.
* **Modo Caos (Random Pos):** Solta a âncora do núcleo (`\c1`). Enquanto as bordas tremem no X, o núcleo vibra em direções aleatórias no eixo Y.
* **Tipos de Execução:** Escolha fatiar todo o texto ("Sempre") ou gerar a corrupção apenas no **Começo** ou no **Final** da linha, otimizando o restante do tempo com Culling.
* **Integração com Karaokê:** Gere glitchs sílaba por sílaba (sincronizado com `\k` nativo ou ReverseK). 
* **Centralizar Karaoke:** Usa a mesma engenharia de "Pulo Dinâmico" do *Text FX* para forçar a centralização do texto enquanto as palavras vão aparecendo no glitch!

---

## 10. Onda Arco-Íris (Pago)
Cria pulsos radiais cromáticos varrendo o texto sem sobrepor camadas no Aegisub.

![GUI Rainbow](ASSETS/rainbow_pt.png)

### Parâmetros:
* **Usar Cor do Estilo:** No lugar das cores RGB fixas, você pode selecionar um estilo secundário. O motor utilizará a matemática de uma **Curva Senoidal (`math.sin`)** para gerar um "pulso" macio (fade-in e fade-out perfeito), substituindo a cor atual pela cor do estilo de forma líquida.
* **Lógica de Passo Blindada:** Opera com um limite inferior rígido de `40ms`, impedindo a criação de sanduíches de milissegundos que engasgariam renderizadores.
* **Culling de Ponta a Ponta:** Calcula de forma absoluta onde a onda termina na última letra e compacta todos os segundos restantes da legenda original numa única linha estática.

---

## 11. Karaoke Reverso (Pago)
Inverte a lógica do karaokê: a linha inteira já está cantada na tela e vai *desaparecendo* conforme os tempos de `\k` estouram.

### Diferencial Técnico:
Processado sem o uso instável de chaves `\t` com alpha cruzado. Ele varre as sílabas e aplica estados binários de visibilidade `\alpha&H00&` (atual/futuro) e `\alpha&HFF&` (passado), garantindo zero bugs de cintilação, além de preservar as tags de tamanho (`\fs`) e posições globais da linha base.

---

## 12. Curvas (Pago) - BETA
Substitui o engessado `\move` do Aegisub por interpolação de movimento via Easing.

<div align="center">
  <table>
    <tr>
      <td align="center" width="50%">
        <strong>Modo Básico (Quad/Cubic)</strong><br>
        <img src="ASSETS/curves_pt.png" alt="GUI Curves">
      </td>
      <td align="center" width="50%">
        <strong>Modo Bézier Avançado</strong><br>
        <img src="ASSETS/curves_adv_pt.png" alt="GUI Curves Advanced">
      </td>
    </tr>
  </table>
</div>

### Parâmetros Easing:
* **Usar Cubic:** Checkbox rápido para alternar a aceleração entre o cálculo Quadrático (`t * t`) e Cúbico (`t ^ 3`), entregando um "arranque" muito mais forte.
* **Modos CSS Padrão:** O painel avançado inclui presets da indústria como *Expo In*, *Expo Out*, *Back In-Out* e *Back Out* (Movimento elástico perfeito).
* **Análise Vetorial de Bézier:** Edite coordenadas `x1, y1` e `x2, y2` idênticas às ferramentas de interpolação do After Effects.
* **Preservação de Sub-Efeitos:** Fatiar em dezenas de pedaços quebraria um fade-in. A engine nativa do Curves converte todas as suas durações globais e joga-as para tempos negativos localizados `\t(-offset, ...)` para manter transições de cor e afins intocadas durante o voo da curva!

---

Desenvolvido por [Tensho](https://x.com/otenshy). Licença MIT.

<br />
<br />
<hr />
<br />
<br />

<h1 id="-english"></h1>
<a href="#-português">
    <img src="https://img.shields.io/badge/Lang-Português-green?style=for-the-badge&logo=brazil" alt="Português">
  </a>
  
# 🐉 Official Documentation: TenshoScripts v1.0.3

Welcome to the technical documentation for **TenshoScripts**. This toolkit was designed to push Aegisub to its limits, focusing on Motion Graphics automation for the **Nerdcore** and **AMV** scene, solving historical limitations found in other scripts.

---

## 🛠️ Technical Differentials (Why use it?)

* **Recursive Navigation:** We implemented a **"Back"** button in all GUIs. You can navigate between tools without closing and reopening the script from the automation menu.
* **UTF-8 Shielding (Anti-Crash):** We use 1-to-4 byte capture patterns to process characters. This eliminates the **C++ Exception** error when slicing accented letters or special characters, a chronic issue in older slicing scripts.
* **Layout Integrity:** All included tools detect your original alignment (`\an`) and position (`\pos`), maintaining the visual integrity of the line.

---

## 1. Adapted Fadeworks
Applies complex visibility transitions in a simplified way, combining Alpha and Color.

![GUI Fadeworks](ASSETS/fadeworks_en.png)

### Parameters:
* **Fade In/Out:** Duration in milliseconds or as a percentage of the line's duration (e.g., `Fade in: 0.4` will set the fade in duration to 40% of the total line time).
* **Alpha/Colour:** Sets whether the effect affects only transparency or involves a color transition.
* **From/To:** Start and end colors for the fade (e.g., starting from white and ending at the style's default color).
* **By Letter:** Enables sequential character-by-character fading.
* **Direction:** Choose between **LTR** (Left-to-Right), **RTL** (Right-to-Left), **Middle->Out**, or **Out->Middle**.

---

## 2. Easy Gradient (Multi-Point)
Generates letter-by-letter gradients with up to 5 key colors and advanced interpolation, or automatically based on styles.

<div align="center">
  <table>
    <tr>
      <td align="center" width="50%">
        <strong>Easy Gradient (Multi-Point)</strong><br>
        <img src="ASSETS/gradient_en.png" alt="GUI Gradient">
      </td>
      <td align="center" width="50%">
        <strong>Gradient: Style Transition</strong><br>
        <img src="ASSETS/gradient_sty_en.png" alt="GUI Gradient Styles">
      </td>
    </tr>
  </table>
</div>

### Parameters:
* **HSL Interpolation:** Transitions colors through the Hue, Saturation, and Lightness spectrum, resulting in much more vibrant colors than standard RGB mode.
* **Key Colors (1-5):** Defines the transition points. Enable intermediate colors for complex gradients.
* **Target Checkboxes:** Allows selective gradient application to specific tags (`\c`, `\3c`, or `\4c`).
* **Styles (A, B, C):** The script automatically reads all styles in your file. You can set a linear transition (A -> B) or a three-point transition (A -> C -> B).
* **Full Interpolation:** Beyond colors, you can transition sizes (`\fs`), creating perspective or organic text growth effects.

---

## 3. Flashes
Ideal for syncing visual impact with the music beat.

![GUI Flashes](ASSETS/flashes_en.png)

### Parameters:
* **Flash Color:** The color the subtitle takes during the flash peak.
* **Interval (ms):** Sets the time between color swaps.
* **Targets (\c, \3c, \4c):** Choose if the flash affects fill, border, or shadow independently.

---

## 4. Split Lines
Divides lines into individual layers.

![GUI Split](ASSETS/split_en.png)

### Features:
* **Modes:** Split by **Character** or **Word**.
* **Vacuum Filter:** The script detects spaces and invisible characters, calculating their width to maintain the layout, but **does not create** empty lines in the grid.
* **Tag Preservation:** Keeps the original line tags in every sliced piece.

---

## 5. Transform (\t)
A tool for quickly creating transformation animations without the need to type manual tags.

![GUI Transform](ASSETS/transform_en.png)

### Parameters:
* **Interval (ms):** Sets the start and end time of the animation. The default end time is automatically filled with the line's duration.
* **Color Targets:** Allows independent transformation of Primary (`\1c`), Secondary (`\2c`), Border (`\3c`), and Shadow (`\4c`) colors.
* **Size and Alpha:** Animates font size variation (`\fs`) and global transparency (`\alpha`).

---

## 6. Random Font (Chaos)
Creates an instability effect through the rapid oscillation of fonts and sizes.

![GUI RandomFonts](ASSETS/textfx_en.png)

### Parameters:
* **Switch Interval:** Sets the oscillation speed (Minimum of `40ms` to ensure stable rendering).
* **Size Variation:** Defines a range (e.g., `5px`) for the font size to change randomly up or down.
* **Character Mode:** When enabled, every letter in the sentence takes on a different font, generating a maximum distortion effect.

---

## 7. YtktFade
Applies the invisible karaoke style optimized for the YouTube renderer.

![GUI Ytkt](ASSETS/ytkt_en.png)

### Parameters:
* **Enable \2c:** Defines a specific fill color for the moment a syllable is sung, ensuring better readability in the YouTube player.

---

## 8. FixLines
A position standardization tool based on proportional calculations.

![GUI FixLines](ASSETS/fix_en.png)

### Features:
* **Force Alignment:** Allows you to apply or not apply `\an5` to the positioned lines.
* **Smart Resolution:** Automatically detects video `PlayRes` and adjusts coordinates to remain identical across any resolution (e.g., 720p or 1080p).

---

## 9. Dynamic Glitch (Paid)
Generates dynamic chromatic aberration with color channel separation.

![GUI Glitch](ASSETS/glitch_en.png)

### Parameters:
* **Auto-Style:** Reads your style and automatically generates harmonized glitch colors.
* **Offset (px):** Defines the "violence" of the effect (how far colors drift from the center).
* **Random Pos (Chaos):** Generates random positions for a more organic and noisy glitch effect.

---

## 10. Rainbow Wave (Paid)
Creates a rainbow color wave that flows through the text via temporal slicing.

![GUI Rainbow](ASSETS/rainbow_en.png)

### Parameters:
* **Slicing (ms):** Sets smoothness. The **5ms** default creates a 200 "fps" fluid motion.
* **Speed & Width:** Controls displacement speed and how wide the color transition is across the text.

---

## 11. Reverse Karaoke (Paid)
Inverts standard karaoke logic: text starts visible and disappears as the music plays.

### How to Use:
Perform the standard syllable division on the line (`\k`) and then run the automation.

### Technical Advantage:
Unlike simple macros that only apply alpha, TenshoScripts uses a synchronized layer-slicing system. This prevents the YouTube **flicker bug**, ensuring stable rendering on any device.

---

## 12. Curves (Paid) - BETA
Replaces linear `\move` motion with professional acceleration and deceleration curves (Easing).

<div align="center">
  <table>
    <tr>
      <td align="center" width="50%">
        <strong>Curves (Beta Presets)</strong><br>
        <img src="ASSETS/curves_en.png" alt="GUI Curves">
      </td>
      <td align="center" width="50%">
        <strong>Curves: Advanced Bézier Editor</strong><br>
        <img src="ASSETS/curves_adv_en.png" alt="GUI Curves Advanced">
      </td>
    </tr>
  </table>
</div>

### Parameters:
* **Ease Modes:** Classic presets like *Quad, Cubic*, and *Linear*.
* **Bézier Control (Advanced):** "Flow" style curve editor, allowing coordinate influence point configuration for fully customized movements.

---

Developed by [Tensho](https://x.com/otenshy). MIT License.
