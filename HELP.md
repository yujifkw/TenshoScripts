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

* **Preservação Estrutural Rigorosa:** O motor lê, protege e remonta as tags de posicionamento e tipografia (como `\pos`, `\an` e `\fs`) em cada fatia gerada. Isso garante que o layout original e o tamanho da sua legenda nunca sejam quebrados ou perdidos, independentemente da complexidade do efeito.
* **Navegação em State Machine:** Transite entre ferramentas, painéis básicos e avançados de forma contínua usando o botão **"Voltar"**, sem duplicar processamento ou fechar o script.
* **Blindagem UTF-8 (Anti-Crash):** Captura segura de caracteres de 1 a 4 bytes, eliminando o clássico *C++ Exception* ao fatiar letras acentuadas ou emojis.
* **Motor de "Culling" e Limite de 40ms:** Ferramentas de fatiamento contínuo geram as fatias apenas onde a animação ocorre, envelopando o tempo inativo em "Linhas Clean" estáticas. Isso reduz o peso do arquivo `.ass` em até 80% e elimina travamentos no player de vídeo.
* **Motor de Viagem no Tempo:** Fatiar uma linha normalmente quebra tags como `\fad` e `\t`. O TenshoScripts recalcula dinamicamente os tempos absolutos dessas tags para tempos relativos (suportando offsets negativos nativos do VSFilter), mantendo seus fades e cores perfeitamente intactos nas fatias.

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

## 3. Piscadas
Ideal para sincronizar o impacto visual com a batida da música.

![GUI Flashes](ASSETS/flashes_pt.png)

### Parâmetros:
* **Cor do Flash:** Cor que a legenda assumirá durante o pico (BPM).
* **Intervalo (ms):** Define o tempo entre as alternâncias.
* **Suavizar Transição:** Quando desmarcado, faz cortes secos. Quando marcado, cria um efeito pulsante interligando os flashes com `\t`.

---

## 4. Dividir Linhas
Divide frases em camadas individuais mantendo o layout original estrito.

![GUI Split](ASSETS/split_pt.png)

### Funcionalidades:
* **Modos:** Dividir por **Caractere** ou por **Palavra**.
* **Preservação Tipográfica:** Extrai e remonta tags globais e locais, incluindo `\fs` original e ancoragens horizontais.
* **Filtro de Vácuo:** Detecta espaços e calcula sua métrica (`text_extents`) para manter o kerning correto, mas aborta a criação de linhas inúteis vazias na grid.

---

## 5. Transformar (\t)
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

## 8. Fixar Linhas
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

Welcome to the technical documentation of **TenshoScripts**. This toolkit was designed to push Aegisub to its absolute limits, focusing on Motion Graphics automation for the **Nerdcore** and **AMV** scene, solving historical limitations of other scripts.

---

## 🛠️ Engine's Core Technical Features

* **Strict Structural Preservation:** The engine reads, protects, and rebuilds positioning and typographic tags (such as `\pos`, `\an`, and `\fs`) in every generated slice. This ensures your subtitle's original layout and size are never broken or lost, regardless of the effect's complexity.
* **State Machine Navigation:** Seamlessly transition between tools, basic, and advanced panels using the **"Back"** button, without duplicating processing tasks or closing the script.
* **UTF-8 Shielding (Anti-Crash):** Safe capture of 1 to 4-byte characters, completely eliminating the classic *C++ Exception* crash when slicing accented letters or emojis.
* **"Culling" Engine & 40ms Limit:** Continuous slicing tools only generate slices where the animation actually occurs, wrapping the inactive time into static "Clean Lines". This reduces the `.ass` file weight by up to 80% and eliminates video player stuttering.
* **Time Travel Engine:** Slicing a line usually breaks global tags like `\fad` and `\t`. TenshoScripts dynamically recalculates the absolute times of these tags into relative times (supporting VSFilter's native negative offsets), keeping your fades and colors perfectly intact across slices.

---

## 1. Adapted Fadeworks
Applies complex visibility transitions in a simplified way, merging Alpha and Color.

![GUI Fadeworks](ASSETS/fadeworks_en.png)

### Parameters:
* **Fade In/Out:** Input and output duration in milliseconds or relative percentage (`0.4` will fade over 40% of the line's time).
* **Alpha/Colour:** Defines if the effect will only affect transparency or if there will be cross-color transitions.
* **From/To:** Starting and ending fade colors.
* **By Letter:** Activates character-by-character sequencing (with automatic purging of residual karaoke tags to prevent retextmod breakage).
* **Direction:** Choose between `LTR` (Left-to-Right), `RTL` (Right-to-Left), `Mid->Out`, or `Out->Mid` (with perfect radial calculation for both even and odd character counts).

---

## 2. Easy Gradient (Multi-Point)
Generates letter-by-letter gradients with up to 5 key colors and advanced interpolation, or automatically through Styles.

<div align="center">
  <table>
    <tr>
      <td align="center" width="50%">
        <strong>Multi-Point Gradient</strong><br>
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
* **Interpolate HSL:** Transitions colors through the Hue, Saturation, and Lightness spectrum instead of RGB space, resulting in vibrant colors that don't pass through gray or muddy tones halfway.
* **Key Colors (1-5):** Defines the stopping points. Enable mid-colors for ultra-complex gradients.
* **Target Checkboxes:** Selectively apply the gradient only to specific tags (`\c`, `\3c`, or `\4c`).
* **Styles (A, B, C):** Automatically reads your style table. Choose a linear transition (A -> B) or a 3-point anchored transition (A -> C -> B).
* **Complete Interpolation:** Mathematically transitions colors, outlines (`\bord`), shadows (`\shad`), and font sizes (`\fs`), generating 3D perspective effects or organic text growth.

---

## 3. Flashes
Ideal for synchronizing visual impact with the music beat.

![GUI Flashes](ASSETS/flashes_en.png)

### Parameters:
* **Flash Color:** The color the subtitle will assume during the peak (BPM).
* **Interval (ms):** Defines the time between alternations.
* **Smooth Transition:** When unchecked, makes hard cuts. When checked, creates a pulsing effect linking the flashes with `\t`.

---

## 4. Split Lines
Splits sentences into individual layers while maintaining strict original layout.

![GUI Split](ASSETS/split_en.png)

### Features:
* **Modes:** Split by **Character** or by **Word**.
* **Typographic Preservation:** Extracts and rebuilds global and local tags, including original `\fs` and horizontal anchor points.
* **Whitespace Filter:** Detects spaces and calculates their metrics (`text_extents`) to maintain proper kerning, but prevents the creation of useless empty lines on the grid.

---

## 5. Transform (\t)
Quick creation of temporal transition animations.

![GUI Transform](ASSETS/transform_en.png)

### Parameters:
* **Interval (ms):** Defines Start and End time (the end inherits the line duration by default).
* **Color & Size Targets:** Allows simultaneous transitioning of `\1c`, `\2c`, `\3c`, `\4c`, font scale (`\fs`), and global opacity (`\alpha`).

---

## 6. Text & Font FX
A powerful integrated typographic motion engine. It replaces the old Random Fonts and encompasses 5 lettering manipulation tools with dynamic "clean line" generation.

![GUI TextFX](ASSETS/textfx_en.png)

### Available Effects:
* **Random Fonts:** Randomly selects fonts from a predefined list. **Normalization Included:** Uses an invisible "X-Height" dictionary to correct font bounding boxes (e.g., *Lucida Console* gets a different scale so it doesn't "shrink" next to *Roboto*).
* **Typewriter:** Reveals letters in sequence based on `ms/char`. 
* **Unscramble:** Decryption (Hacking) effect. Before revealing the actual letter, it displays random symbols for 120ms.
* **Chaos Symbols:** Text suffers continuous corruption over time (30% chance to turn into a corrupted character on each sliced frame).
* **Invert Letters:** Replaces letters with their mirrored equivalents using Unicode code points. If **Horizontal (X)** or **Both (X+Y)** directions are chosen, the entire string is reordered backward (True Mirror).

### The "Dynamic Jump" Magic (Center)
By enabling **Dynamic Jump** in Typewriter or Unscramble, syllables that haven't been revealed yet are physically *deleted* from the line instead of just being hidden with alpha. If your line has central alignment (`\an5`, `\an8`, etc.), the entire sentence recalculates and "jumps" to the center with every new letter printed on the screen!

---

## 7. YtktFade
Compression optimizer for YouTube.

![GUI Ytkt](ASSETS/ytkt_en.png)

### Parameters:
* **Constant Alpha:** Injects alphas that force web renderers (VP9/AV1) to maintain the karaoke's outline quality.
* **Enable \2c:** Applies secondary fill colors.

---

## 8. Fix Lines
Position standardization via relative mathematical calculations.

![GUI FixLines](ASSETS/fix_en.png)

### Features:
* **Force Alignment (\an5):** Overrides previous alignments and centers the anchor point.
* **Delta Calculation:** Captures the actual video resolution (`PlayRes`) and positions subtitles in exact proportion. Perfect for migrating `1080p` `.ass` files to Shorts/TikTok (`1080x1920`) projects without breaking the layout.

---

## 9. Dynamic Glitch (Paid)
Advanced generator for static and animated chromatic aberration (RGB Split).

![GUI Glitch](ASSETS/glitch_en.png)

### Technical Differentials:
* **Typographic Flicker:** Enable "Bold" or "Italic" and the engine flips a coin (50% chance) on every frame generated per layer: the glitch will flicker with font weight breaks during the distortion, creating an extremely aggressive look.
* **Chaos Mode (Random Pos):** Detaches the core anchor (`\c1`). While the edges shake on the X-axis, the core vibrates in random directions on the Y-axis.
* **Execution Types:** Choose to slice the whole text ("Always") or generate corruption only at the **Start** or **End** of the line, optimizing the rest of the time with Culling.
* **Karaoke Integration:** Generate glitches syllable by syllable (synced with native `\k` or ReverseK). 
* **Center Karaoke:** Uses the same "Dynamic Jump" engineering from *Text FX* to force text centering while words appear in the glitch!

---

## 10. Rainbow Wave (Paid)
Creates radial chromatic pulses sweeping through the text without stacking overlapping layers in Aegisub.

![GUI Rainbow](ASSETS/rainbow_en.png)

### Parameters:
* **Use Style Color:** Instead of fixed RGB colors, you can select a secondary style. The engine will use the math of a **Sine Wave (`math.sin`)** to generate a soft "pulse" (perfect fade-in and fade-out), seamlessly replacing the current color with the style color.
* **Shielded Step Logic:** Operates with a rigid lower limit of `40ms`, preventing the creation of millisecond sandwiches that would choke renderers.
* **End-to-End Culling:** Calculates exactly where the wave finishes on the final letter and compresses all remaining seconds of the original subtitle into a single static line.

---

## 11. Reverse Karaoke (Paid)
Inverts standard karaoke logic: the entire line is already sung on screen and *disappears* as the `\k` times hit.

### Technical Differential:
Processed without the unstable use of cross-alpha `\t` tags. It scans the syllables and applies binary visibility states `\alpha&H00&` (current/future) and `\alpha&HFF&` (past), ensuring zero flicker bugs while preserving font size (`\fs`) and global positioning tags from the base line.

---

## 12. Curves (Paid) - BETA
Replaces Aegisub's rigid `\move` tag with motion interpolation via Easing.

<div align="center">
  <table>
    <tr>
      <td align="center" width="50%">
        <strong>Basic Mode (Quad/Cubic)</strong><br>
        <img src="ASSETS/curves_en.png" alt="GUI Curves">
      </td>
      <td align="center" width="50%">
        <strong>Advanced Bézier Mode</strong><br>
        <img src="ASSETS/curves_adv_en.png" alt="GUI Curves Advanced">
      </td>
    </tr>
  </table>
</div>

### Easing Parameters:
* **Use Cubic:** Quick checkbox to switch acceleration between Quadratic (`t * t`) and Cubic (`t ^ 3`) calculation, delivering a much stronger start-up burst.
* **Standard CSS Modes:** The advanced panel includes industry presets like *Expo In*, *Expo Out*, *Back In-Out*, and *Back Out* (Perfect elastic motion).
* **Bézier Vector Analysis:** Edit `x1, y1` and `x2, y2` coordinates identically to After Effects interpolation tools.
* **Sub-Effects Preservation:** Slicing into dozens of pieces would break a fade-in. The Curves native engine converts all your global durations and throws them into localized negative times `\t(-offset, ...)` to keep color transitions and blurs completely untouched during the curve's flight!

---

Developed by [Tensho](https://x.com/otenshy). MIT License.

<br />
