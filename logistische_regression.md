# Klassifizierung und Logistische Regression

## Klassifizierung

Der Unterschied zwischen Regression und Klassifizierung ist, dass man sich bei der Klassifizierung zwischen zwei Merkmalen ( zum Beispielk Farbe `binäre Klassifizierung`) entscheiden muss.  
Ein weiteres Beispiel wäre: *Wird ein Bewerber erfolgreich sein oder nicht?*  
**Es gibt keine Werte wie `0.5 Kinder`**  

## Logistische Regression

Die logistische Regression liefert immer Werte zwischen 0 und 1. IMMER!  
Teil der logistischen Regression ist die `SIGMOID-Funktion`. Dieser Liefert eine 'abgerundete' Funktion für Werte im Bereich 0 - 1. **Dieser Werte 0 & 1 werden aber nie erreicht!**

## Im Code

Um Daten anzuzeigen kann man folgenden Code verwenden:

```python
# Beispieldaten um einen erfolgreichen Kauf (success) anhand von Alter und Interesse vorherhzusagen
X = df[["age", "interest"]].values
y = df["success"]

X_train, X_test, y_train, y_test = train_test_split_(X, y, random_state = 0, test_size=0.25)

import matplotlib.pyplot as plt

# Daten in einem Scatter-Plot anzeigen // In Farbe wird die Zielvariable angezeigt (y_train)
plt.scatter(X_train[:, =], X_train[:, 1], c = y_train)
plt.xlabel("Alter")
plt.ylabel("Interesse")
plt.show()
```
Um eine korrekte Klassifizierung zu gewährleisten ist es oftmals notwendig die Daten zu skalieren bevor man diese anzeigt. Grund dafür ist, dass oftmals der Abstand zwischen den einzelnen Punkten entscheidend ist und dieser nur NACH der Skalierung passt.

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_train = scaler.fit(X_train)
X_test = scaler.fit(X_test)
```