# Cross-Validation

Bei der Cross-Validation wird ein Modell benfalls in Trainings & Testdaten aufgeteilt.  
Nach der Aufteilung wird ebnfalls ein $R^{2}$ berechnet, doch danachg  werden die Daten in neue Blöcke aufgeteilt und weitere $R^{2}$ berechnet.

Alle diese berechneten $R^{2}$ werden aufsummiert und der Mittelwert davon berechnet.

**Benefit:**  
Durch das mehrmalige Ausführen bei dieser Methode werden die _zufälligen_ Schwankungen besser ausgegelichen und man kann mit einerhöheren Sicherheit das Bestiimmtheitsmaß evaluieren.  
Besonders bei der _Polynomialen Regression_ können erhebliche Schwankungen auftreten.

# K-Fold Cross Validation

```python
X = df[["x", "y", "z"]].values
Y = df[["price"]].values

from sklearn.linear_model import LinearRegression
from sklearn.model_selection import cross_val_score, RepeatedKFold

scores = cross_val_score(LinearRegression(), X, Y, cv = RepeatedKFold(n_repeats = 1000))

import numpy as np

print(np.mean(scores))
```

## Beschreibung

Zuerst werden die zwei verwendeten Variablen erstellt. Wichtig dabei ist der Befehl `.values`. Ohne diesen liegen die Daten im falschen Format vor.  
Mit den Parametern `cv` und `n_repeats` stellt man die die Cross-Validation an sich und die Wiederholungsanzahl ein. 

Am Ende wird das Ergebnis nur noch ausgegeben.
