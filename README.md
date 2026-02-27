# Bayesian Probability Bands — TradingView

Indicateur Pine Script v5 affichant des bandes de probabilite bayesiennes sur le graphique, basees sur un modele conjugue Normal-Inverse-Gamma (NIG) applique aux log-returns.

La distribution predictive posterieure (Student-t) est recalculee a chaque barre sur une fenetre rolling. Les quantiles sont projetes en prix via `close * exp(quantile)`.

---

## Fonctionnement

Le prior NIG est mis a jour analytiquement sur les `n` derniers log-returns pour produire les hyperparametres posterieurs `(mu_n, kappa_n, alpha_n, beta_n)`. La distribution predictive resultante est une Student-t dont les quantiles sont approches par expansion de Cornish-Fisher a l'ordre 2. Trois bandes (68%, 95%, 99%) sont tracees symetriquement autour du close courant.

---

## Installation & Usage

1. Ouvrir l'editeur Pine Script dans TradingView (icone `{}` en bas du graphique).
2. Supprimer le contenu par defaut, coller l'integralite du fichier `bayesian_nig_bands.pine`.
3. Cliquer **Ajouter au graphique**.

### Parametres disponibles

| Parametre | Defaut | Description |
|-----------|--------|-------------|
| `Lookback window` | 50 | Nombre de barres pour le posterior rolling |
| `Prior mu0` | 0.0 | Moyenne a priori des log-returns |
| `Prior kappa0` | 1.0 | Poids du prior sur la moyenne |
| `Prior alpha0` | 2.0 | Parametre de forme du prior (doit etre > 1) |
| `Prior beta0` | 0.001 | Parametre d'echelle du prior |
| `68% / 95% / 99% band` | on | Activation individuelle de chaque bande |
| `Show posterior info` | on | Table des hyperparametres posterieurs courants |

### Notes

- Les bandes ne s'affichent qu'apres `lookback` barres disponibles.
- L'approximation Cornish-Fisher est fiable pour `df > 4` (soit `alpha_n > 2`), ce qui est garanti des que le lookback est suffisant avec le prior par defaut.
- Compatible tous timeframes et tous instruments.

---

## License

MIT License

Copyright (c) 2026

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
