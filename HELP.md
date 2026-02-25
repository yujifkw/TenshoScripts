<h1 id="-português"></h1>
<div align="left">
  <a href="#-english">
    <img src="https://img.shields.io/badge/Lang-English-blue?style=for-the-badge&logo=united-kingdom" alt="English">
  </a>
</div>

# 🐉 Documentação Oficial: TenshoScripts v1.0.1

Bem-vindo à documentação técnica do **TenshoScripts**. Este toolkit foi projetado para levar o Aegisub ao limite, focando em automações de Motion Graphics para a cena **Nerdcore** e **AMVs**, resolvendo limitações históricas de outros scripts.

---

## 🛠️ Diferenciais Técnicos (Por que usar?)

* **Navegação Recursiva:** Implementamos um botão **"Voltar"** em todas as GUIs. Você pode transitar entre ferramentas sem precisar fechar e reabrir o script pelo menu de automação.
* **Blindagem UTF-8 (Anti-Crash):** Utilizamos padrões de captura de 1 a 4 bytes para processar caracteres. Isso elimina o erro de **C++ Exception** ao fatiar letras acentuadas ou caracteres especiais, um problema crônico em scripts de fatiamento antigos.
* **Respeito ao Layout Original:** Todas as ferramentas inclusas detectam seu alinhamento (`\an`) e posição (`\pos`) originais, mantendo a integridade visual da frase.

---

## 1. Fadeworks Adaptado
Aplica transições de visibilidade complexas de forma simplificada, unindo Alpha e Cor.

![GUI Fadeworks](ASSETS/fadeworks_pt.png)

### Parâmetros:
* **Fade In/Out:** Duração em milissegundos da entrada e saída ou em porcentagem em relação ao tempo da linha (exemplo: `Fade in: 0.4` fará o fade in na duração de 40% do tempo máximo da linha).
* **Alpha/Colour:** Define se o efeito afetará apenas a transparência ou se haverá transição de cores.
* **From/To:** Cores de início e fim do fade (ex: começar em branco e terminar na cor do estilo).
* **By Letter:** Ativa o sequenciamento caractere por caractere.
* **Direção:** Escolha entre **LTR** (esquerda para direita), **RTL** (direita para esquerda), **Meio->Fora** ou **Fora->Meio**.

---

## 2. Gradiente Fácil (Multi-Ponto)
Gera gradientes letra por letra com até 5 cores chave e interpolação avançada, ou automaticamente pelos estilos.

<div align="center">
  <table>
    <tr>
      <td align="center" width="50%">
        <strong>Easy Gradient (Multi-Ponto)</strong><br>
        <img src="ASSETS/gradient_pt.png" alt="GUI Gradient">
      </td>
      <td align="center" width="50%">
        <strong>Gradient: Style Transition</strong><br>
        <img src="ASSETS/gradient_sty_pt.png" alt="GUI Gradient Styles">
      </td>
    </tr>
  </table>
</div>

### Parâmetros:
* **Interpolar HSL:** Transita as cores pelo espectro de Matiz, Saturação e Luminosidade, resultando em cores muito mais vivas que o modo RGB.
* **Cores Chave (1-5):** Define os pontos de transição. Ative as cores intermediárias para gradientes complexos.
* **Checkboxes Target:** Permite aplicar o gradiente seletivamente apenas em tags específicas (`\c`, `\3c` ou `\4c`).
* **Estilos (A, B, C):** O script lê automaticamente todos os estilos do seu arquivo. Você pode definir uma transição linear (A -> B) ou uma transição em três pontos (A -> C -> B).
* **Interpolação Completa:** Além das cores, você pode transitar tamanhos (`\fs`), criando efeitos de perspectiva ou crescimento orgânico do texto.

---

## 3. Flashes
Ideal para sincronizar o impacto visual com a batida da música.

![GUI Flashes](ASSETS/flashes_pt.png)

### Parâmetros:
* **Cor do Flash:** Cor que a legenda assumirá durante o pico do flash.
* **Intervalo (ms):** Define o tempo entre as trocas de cor.
* **Alvos (\c, \3c, \4c):** Escolha se o flash afeta o preenchimento, a borda ou a sombra de forma independente.

---

## 4. Split Lines
Divide frases em camadas individuais.

![GUI Split](ASSETS/split_pt.png)

### Funcionalidades:
* **Modos:** Dividir por **Caractere** ou por **Palavra**.
* **Filtro de Vácuo:** O script detecta espaços e caracteres invisíveis, calculando sua largura para manter o layout, mas **não cria** linhas vazias na grade.
* **Preservação de Tags:** Mantém as tags originais da linha em cada pedaço fatiado.

---

## 5. Transform (\t)
Ferramenta para criação rápida de animações de transformação sem necessidade de digitar tags manuais.

![GUI Transform](ASSETS/transform_pt.png)

### Parâmetros:
* **Intervalo (ms):** Define o tempo de início e fim da animação. O tempo de fim padrão é preenchido automaticamente com a duração da linha.
* **Alvos de Cor:** Permite transformar de forma independente as cores Primária (`\1c`), Secundária (`\2c`), Borda (`\3c`) e Sombra (`\4c`).
* **Tamanho e Alpha:** Anima a variação de escala da fonte (`\fs`) e a transparência global (`\alpha`).

---

## 6. Random Font (Caos)
Cria um efeito de instabilidade através da oscilação rápida de fontes e tamanhos.

![GUI RandomFonts](ASSETS/textfx_pt.png)

### Parâmetros:
* **Intervalo de Troca:** Define a velocidade da oscilação (Mínimo de `40ms` para garantir a renderização).
* **Variação de Tamanho:** Define um intervalo (ex: `5px`) para que o tamanho da fonte mude aleatoriamente para cima ou para baixo.
* **Modo Caractere:** Quando ativo, cada letra da frase assume uma fonte diferente entre si, gerando um efeito de distorção máxima.


## 7. YtktFade
Aplica o estilo de karaokê invisível otimizado para o renderizador do YouTube.

![GUI Ytkt](ASSETS/ytkt_pt.png)

### Parâmetros:
* **Ativar \2c:** Define uma cor de preenchimento específica para o momento em que a sílaba é cantada, garantindo maior legibilidade no player do YouTube.

---

## 8. FixLines
Ferramenta de padronização de posição baseada em cálculos proporcionais.

![GUI FixLines](ASSETS/fix_pt.png)

### Funcionalidades:
* **Forçar Alinhamento:** Permite aplicar ou não `\an5` às linhas posicionadas.
* **Resolução Inteligente:** Detecta automaticamente a `PlayRes` do vídeo e ajusta as coordenadas para que fiquem idênticas em qualquer resolução (ex: 720p ou 1080p).

---

## 9. Glitch Dinâmico (Pago)
Gera uma aberração cromática dinâmica com separação de canais de cor.

![GUI Glitch](ASSETS/glitch_pt.png)

### Parâmetros:
* **Auto-Style:** Lê o seu estilo e gera cores de glitch harmonizadas automaticamente.
* **Offset (px):** Define a "violência" do efeito (quão longe as cores vão do centro).
* **Random Pos (Caos):** Gera posições aleatórias para um efeito de glitch mais orgânico e ruidoso.

---

## 10. Rainbow Wave (Pago)
Cria uma onda de cores arco-íris que flui pelo texto através de fatiamento temporal.

![GUI Rainbow](ASSETS/rainbow_pt.png)

### Parâmetros:
* **Fatiamento (ms):** Define a suavidade. O padrão de **5ms** cria uma fluidez de 200 "frames" por segundo.
* **Speed & Width:** Controla a velocidade de deslocamento e quão larga é a transição de cor no texto.

---

## 11. Reverse Karaoke (Pago)
Inverte a lógica do karaokê comum: o texto começa visível e desaparece conforme a música toca.

### Como Usar:
Faça a divisão de sílabas padrão na linha (`\k`) e depois execute a automação.

### Diferencial Técnico:
Diferente de macros simples que apenas aplicam alpha, o TenshoScripts utiliza um sistema de fatiamento por camadas sincronizadas. Isso evita o bug de cintilação (*flicker*) do YouTube, garantindo uma renderização estável em qualquer dispositivo.

---

## 12. Curves (Pago) - BETA
Substitui o movimento linear do `\move` por curvas de aceleração e desaceleração (Easing).

<div align="center">
  <table>
    <tr>
      <td align="center" width="50%">
        <strong>Curves (Presets Beta)</strong><br>
        <img src="ASSETS/curves_pt.png" alt="GUI Curves">
      </td>
      <td align="center" width="50%">
        <strong>Curves: Advanced Bézier Editor</strong><br>
        <img src="ASSETS/curves_adv_pt.png" alt="GUI Curves Advanced">
      </td>
    </tr>
  </table>
</div>

### Parâmetros:
* **Ease Modes:** Presets clássicos como *Quad, Cubic* e *Linear*.
* **Controle de Bézier (Avançado):** Editor de curvas estilo "Flow", permitindo configurar os pontos de influência para movimentos totalmente personalizados.

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
  
# 🐉 Official Documentation: TenshoScripts v1.0.1

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
