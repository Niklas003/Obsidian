

## 1️⃣ Problem ohne Normalisierung

- In jedem Layer passiert sehr viel **lineare und nicht-lineare Transformation**: Attention, FFN, Residual Connections.
- Wenn man einfach alles stapelt, kann das dazu führen, dass:
    1. **Signale explodieren oder verschwinden** (z. B. sehr große oder sehr kleine Werte im Hidden State)
    2. Das **Training instabil wird**, Gradient Descent nicht richtig funktioniert
- Besonders bei **tiefen Modellen** (z. B. 12+ Layers) summieren sich die Effekte → Training sehr langsam oder bricht ab.

---

## 2️⃣ Layer Normalization

- **LayerNorm** normalisiert jeden Hidden-State-Vektor $h_i$ **über seine Features**:

$$
\hat{h}_i = \frac{h_i - \mu_i}{\sigma_i}  $$

- $\mu_i$ = Mittelwert über die Features, $\sigma_i$ = Standardabweichung.
- Danach skaliert und verschiebt man ihn noch mit lernbaren Parametern $\gamma, \beta$ :  $$
    \text{LayerNorm}(h_i) = \gamma \cdot \hat{h}_i + \beta  
$$
---

## 3️⃣ Vorteile

1. **Stabilisierung**: Hidden States bleiben in einer kontrollierten Größenordnung → verhindert Explodieren/Verschwinden.
2. **Schnelleres Training**: Gradienten fließen besser, Optimierung konvergiert schneller.
3. **Residual Connection effizienter**: Wenn man Residuals ohne Normierung addiert, könnten bestimmte Features dominant werden → Normierung sorgt für Balance.

💡 **Merke:** Ohne Normalisierung könnten einige Dimensionen der Hidden States die anderen übertönen, und das Modell lernt instabil oder sehr langsam.
