<h1 id="-português"></h1>
<div align="left">
  <a href="#-english">
    <img src="https://img.shields.io/badge/Lang-English-blue?style=for-the-badge&logo=united-kingdom" alt="English">
  </a>
</div>

# 🐉 Documentação Oficial: TenshoScripts v1.0.0

Bem-vindo à documentação técnica do **TenshoScripts**. Este toolkit foi projetado para levar o Aegisub ao limite, focando em automações de Motion Graphics para a cena **Nerdcore** e **AMVs**, resolvendo limitações históricas de outros scripts.

---

## 🛠️ Diferenciais Técnicos (Por que usar?)

* **Navegação Recursiva:** Implementamos um botão **"Voltar"** em todas as GUIs. Você pode transitar entre ferramentas sem precisar fechar e reabrir o script pelo menu de automação.
* **Blindagem UTF-8 (Anti-Crash):** Utilizamos padrões de captura de 1 a 4 bytes para processar caracteres. Isso elimina o erro de **C++ Exception** ao fatiar letras acentuadas ou caracteres especiais, um problema crônico em scripts de fatiamento antigos.
* **Respeito ao Layout Original:** Todas as ferramentas inclusas detectam seu alinhamento (`\an`) e posição (`\pos`) originais, mantendo a integridade visual da frase.

---

## 1. Fadeworks Adaptado
Aplica transições de visibilidade complexas de forma simplificada, unindo Alpha e Cor.

![GUI Fadeworks](assets/gui_fadeworks.png)

### Parâmetros:
* **Fade In/Out:** Duração em milissegundos da entrada e saída ou em porcentagem em relação ao tempo da linha (exemplo: `Fade in: 0.4` fará o fade in na duração de 40% do tempo máximo da linha).
* **Alpha/Colour:** Define se o efeito afetará apenas a transparência ou se haverá transição de cores.
* **From/To:** Cores de início e fim do fade (ex: começar em branco e terminar na cor do estilo).
* **By Letter:** Ativa o sequenciamento caractere por caractere.
* **Direção:** Escolha entre **LTR** (esquerda para direita), **RTL** (direita para esquerda), **Meio->Fora** ou **Fora->Meio**.

---

## 2. Flashes
Ideal para sincronizar o impacto visual com a batida da música.

![GUI Flashes](assets/gui_flashe.png)

### Parâmetros:
* **Cor do Flash:** Cor que a legenda assumirá durante o pico do flash.
* **Intervalo (ms):** Define o tempo entre as trocas de cor.
* **Alvos (\c, \3c, \4c):** Escolha se o flash afeta o preenchimento, a borda ou a sombra de forma independente.

---

## 3. Easy Gradient (Multi-Ponto)
Gera gradientes letra por letra com até 5 cores chave e interpolação avançada.

![GUI Gradient](assets/gui_gradient.png)

### Parâmetros:
* **Interpolar HSL:** Transita as cores pelo espectro de Matiz, Saturação e Luminosidade, resultando em cores muito mais vivas que o modo RGB.
* **Cores Chave (1-5):** Define os pontos de transição. Ative as cores intermediárias para gradientes complexos.
* **Checkboxes Target:** Permite aplicar o gradiente seletivamente apenas em tags específicas (`\c`, `\3c` ou `\4c`).

---

## 4. Split Lines
Divide frases em camadas individuais.

![GUI Split](assets/gui_splitlines.png)

### Funcionalidades:
* **Modos:** Dividir por **Caractere** ou por **Palavra**.
* **Filtro de Vácuo:** O script detecta espaços e caracteres invisíveis, calculando sua largura para manter o layout, mas **não cria** linhas vazias na grade.
* **Preservação de Tags:** Mantém as tags originais da linha em cada pedaço fatiado.

---

## 5. FixLines
Ferramenta de padronização de posição baseada em cálculos proporcionais.

![GUI FixLines](assets/gui_fixlines.png)

### Funcionalidades:
* **Botões Rápidos:** Posicionamento instantâneo em **Topo** ou **Baixo**.
* **Resolução Inteligente:** Detecta automaticamente a `PlayRes` do vídeo e ajusta as coordenadas para que fiquem idênticas em qualquer resolução (ex: 720p ou 1080p).

---

## 6. YtktFade
Aplica o estilo de karaokê invisível otimizado para o renderizador do YouTube.

![GUI Ytkt](assets/gui_ytktfade.png)

### Parâmetros:
* **Ativar \2c:** Define uma cor de preenchimento específica para o momento em que a sílaba é cantada, garantindo maior legibilidade no player do YouTube.

---

## 7. Glitch (Exclusive)
Gera uma aberração cromática dinâmica com separação de canais de cor.

![GUI Glitch](assets/gui_glitch.png)

### Parâmetros:
* **Auto-Style:** Lê o seu estilo e gera cores de glitch harmonizadas automaticamente.
* **Offset (px):** Define a "violência" do efeito (quão longe as cores vão do centro).
* **Random Pos (Caos):** Gera posições aleatórias para um efeito de glitch mais orgânico e ruidoso.

---

## 8. Rainbow Wave (Exclusive)
Cria uma onda de cores arco-íris que flui pelo texto através de fatiamento temporal.

![GUI Rainbow](assets/gui_rainbow.png)

### Parâmetros:
* **Fatiamento (ms):** Define a suavidade. O padrão de **5ms** cria uma fluidez de 200 "frames" por segundo.
* **Speed & Width:** Controla a velocidade de deslocamento e quão larga é a transição de cor no texto.

---

## 9. Curves (Exclusive) - BETA
Substitui o movimento linear do `\move` por curvas de aceleração e desaceleração (Easing).

![GUI Curves](assets/gui_curves.png)
![GUI Curves ADV](assets/gui_curves_adv.png)

### Parâmetros:
* **Ease Modes:** Presets clássicos como *Quad, Cubic* e *Linear*.
* **Controle de Bézier (Avançado):** Editor de curvas estilo "Flow", permitindo configurar os pontos de influência para movimentos totalmente personalizados.

---

## 10. Reverse Karaoke (Exclusive)
Inverte a lógica do karaokê comum: o texto começa visível e desaparece conforme a música toca.

### Diferencial Técnico:
Diferente de macros simples que apenas aplicam alpha, o TenshoScripts utiliza um sistema de fatiamento por camadas sincronizadas. Isso evita o bug de cintilação (*flicker*) do YouTube, garantindo uma renderização estável em qualquer dispositivo.

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
  
# 🐉 Official Documentation: TenshoScripts v1.0.0

Welcome to the technical documentation for **TenshoScripts**. This toolkit was designed to push Aegisub to its limits, focusing on Motion Graphics automation for the **Nerdcore** and **AMV** scene, solving historical limitations found in other scripts.

---

## 🛠️ Technical Differentials (Why use it?)

* **Recursive Navigation:** We implemented a **"Back"** button in all GUIs. You can navigate between tools without closing and reopening the script from the automation menu.
* **UTF-8 Shielding (Anti-Crash):** We use 1-to-4 byte capture patterns to process characters. This eliminates the **C++ Exception** error when slicing accented letters or special characters, a chronic issue in older slicing scripts.
* **Layout Integrity:** All included tools detect your original alignment (`\an`) and position (`\pos`), maintaining the visual integrity of the line.

---

## 1. Adapted Fadeworks
Applies complex visibility transitions in a simplified way, uniting Alpha and Color.

![GUI Fadeworks](assets/gui_fadeworks.png)

### Parameters:
* **Fade In/Out:** Duration in milliseconds or as a percentage of the line's time (e.g., `Fade in: 0.4` applies fade in over 40% of the line's duration).
* **Alpha/Colour:** Sets whether the effect affects only transparency or involves a chromatic transition.
* **From/To:** Start and end colors for the fade (e.g., starting white and ending at the style's color).
* **By Letter:** Enables sequential character-by-character fading.
* **Direction:** Choose between **LTR** (left to right), **RTL** (right to left), **Middle->Out**, or **Out->Middle**.

---

## 2. Flashes
Ideal for syncing visual impact with the music beat.

![GUI Flashes](assets/gui_flashe.png)

### Parameters:
* **Flash Color:** The color the subtitle takes during the flash peak.
* **Interval (ms):** Sets the time between color swaps.
* **Targets (\c, \3c, \4c):** Choose if the flash affects fill, border, or shadow independently.

---

## 3. Easy Gradient (Multi-Point)
Generates letter-by-letter gradients with up to 5 key colors and advanced interpolation.

![GUI Gradient](assets/gui_gradient.png)

### Parameters:
* **HSL Interpolation:** Transitions colors through the Hue, Saturation, and Lightness spectrum, resulting in much more vibrant colors than standard RGB mode.
* **Key Colors (1-5):** Defines transition points. Enable intermediate colors for complex gradients.
* **Target Checkboxes:** Allows selective gradient application to specific tags (`\c`, `\3c`, or `\4c`).

---

## 4. Split Lines
Divides lines into individual layers.

![GUI Split](assets/gui_splitlines.png)

### Features:
* **Modes:** Split by **Character** or **Word**.
* **Vacuum Filter:** The script detects spaces and invisible characters, calculating their width to maintain the layout, but **does not create** empty lines in the grid.
* **Tag Preservation:** Keeps the original line tags in every sliced piece.

---

## 5. FixLines
A position standardization tool based on proportional calculations.

![GUI FixLines](assets/gui_fixlines.png)

### Features:
* **Quick Buttons:** Instant positioning to **Top** or **Bottom**.
* **Smart Resolution:** Automatically detects video `PlayRes` and adjusts coordinates to remain identical across any resolution (e.g., 720p or 1080p).

---

## 6. YtktFade
Applies the invisible karaoke style optimized for the YouTube renderer.

![GUI Ytkt](assets/gui_ytktfade.png)

### Parameters:
* **Enable \2c:** Defines a specific fill color for the moment a syllable is sung, ensuring better readability in the YouTube player.

---

## 7. Glitch (Exclusive)
Generates dynamic chromatic aberration with color channel separation.

![GUI Glitch](assets/gui_glitch.png)

### Parameters:
* **Auto-Style:** Reads your style and automatically generates harmonized glitch colors.
* **Offset (px):** Defines the "violence" of the effect (how far colors drift from the center).
* **Random Pos (Chaos):** Generates random positions for a more organic and noisy glitch effect.

---

## 8. Rainbow Wave (Exclusive)
Creates a rainbow color wave that flows through the text via temporal slicing.

![GUI Rainbow](assets/gui_rainbow.png)

### Parameters:
* **Slicing (ms):** Sets smoothness. The **5ms** default creates a 200 "fps" fluid motion.
* **Speed & Width:** Controls displacement speed and how wide the color transition is across the text.

---

## 9. Curves (Exclusive) - BETA
Replaces linear `\move` motion with professional acceleration and deceleration curves (Easing).

![GUI Curves](assets/gui_curves.png)
![GUI Curves ADV](assets/gui_curves_adv.png)

### Parameters:
* **Ease Modes:** Classic presets like *Quad, Cubic*, and *Linear*.
* **Bézier Control (Advanced):** "Flow" style curve editor, allowing coordinate influence point configuration for fully customized movements.

---

## 10. Reverse Karaoke (Exclusive)
Inverts standard karaoke logic: text starts visible and disappears as the music plays.

### Technical Advantage:
Unlike simple macros that only apply alpha, TenshoScripts uses a synchronized layer slicing system. This prevents the YouTube **flicker bug**, ensuring stable rendering on any device.

---
Developed by [Tensho](https://x.com/otenshy). MIT License.
