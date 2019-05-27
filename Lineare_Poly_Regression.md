# Lineare und Polynomiale Regression
In diesem Dokument werden zuerst die Grundlagen der multiplen Regression / Unterschiede zur linearen Regression erklärt und danach die Realsierung in Python dargestellt.

## Multivariate Regression

Multivariate Regression 'fittet' eine mehrdimensionale Ebene in mehrdimensionale Daten.  
$\to$ gleiche Vorgehenweise wie beider linearen Regression nur im mehrdimensionalen Raum.  
*Zusäzliche Daten werden dem Mondell zugeführt.*

$R^{2}$ wird immer noch gleich berechnet: $\frac{SS(mean) - SS(fit)}{SS(mean)}$

### Vergleich von Linearer und Multivariater Regression

Um herauszufinden ob es sich lohnt mehr Variablen in das Modell aufzunehmen, kann man den `F-Wert` berechnen.  
**Formel:**

$F = \frac{SS(simple) - SS(multiple) / (p_{multiple} - p_{simple})}{SS(multiple) / (n - p_{multiple})}$

## Benötigte Libraries  
Folgende Biliotheken müssen importiert werden:
```
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
```

Danach kann mit folgendem Syntaxt die Regression (egal ob linear oder polynomial) berechnet werden.  
```
X = df[["width", "length"]]
Y = df[["profit"]]

X_train, X_test, y_train, y_test = train_test_split(X, Y, random_state = 7, test_size = 0.25)

model = LinearRegression()
model.fit(X_train, y_train)

print(model.score(X_test, y_test))
```

**Unterschied Poly- Linear:**  
Der Unterschied liegt lediglich in der Anzahl der für `X` definierten Spalten.  
Mann kann sehen wie sich `R^2` vergrößert bzw. verrignert wenn man mehr oder weniger Variablen verwendet.

# Polynomiale Features

Die polynomialen Features ist eine Methode die einen Datensatz mit weiteren Spalten anreichert um eine detailierte Regression zu erhalten.

**Idee:**  
Eine normale Regressionskurve vom Grad 2 wird so beschrieben: $f(x) = ax^{2} + bx + c$  
Die x-Werte (1, 3) und y-Werte (2, 4) werden nun miteinander erweitert.  
Anschaulich sieht die finale Formel dann wie folgt aus:  
$f(x) = ax_{1} + bx_{2} + cx_{1}^{2} + dx_{1}*x_{2} + ex_{2}^{2} + g$

## Umsetzung in Python

Um diese Funktion in Python zu implementieren muss man zunächst folgende Bibliothek importieren  
```
from sklearn.preprocessing import PolynomialFeatures
```
Hat man diese Bibliothek importiert kann man die Funktion `PolynomialFeatures` verwenden
```
pf = PolynomialFeatures(degree = 3, include_bias = False)
pf.fit(X_train)
```
**Wichtig:** Der Parameter `degree=` gibt an wie viele neuen "Erweiterungen" erstellt werden.  
Mit `print(pf.powers_)` kann man sich die neue Matrix ausgeben lassen - diese beschreibt genau die gleiche Formel wie [oben](#polynomiale-features) beschrieben.


Beispiel Output der `pf.transform(X_train)` - Funktion mit `degree=2`:  
(`print(pf.powers_)` - Funktion:
[[1 0]
 [0 1]
 [2 0]
 [1 1]
 [0 2]])

Erster Wert: $x_{1}$ mit 1 potentziert wird und $x_{2}$ mit 0.  
Zweiter Wert: $x_{1}$ mit 0 potentziert wird und $x_{2}$ mit 1.  
usw.

```
from sklearn.preprocessing import PolynomialFeatures

pf = PolynomialFeatures(degree = 2, include_bias = False)
pf.fit(X_train)

# print(pf.powers_)

X_train_transformed = pf.transform(X_train)
X_test_transformed = pf.transform(X_test)

model = LinearRegression()
model.fit(X_train_transformed, y_train)

print(model.score(X_test_transformed, y_test))
```

## Ergebnis:

Als Ergebnis erhält man einen $R^{2}$ Wert von `0.9843167492664864`. Ohne die Polynomial Features war man auf den gleichen Daten bei einem Wert von circa `0.91`. 