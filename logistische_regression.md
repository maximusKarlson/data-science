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

## Entscheidungsgrenzen visualisieren

Als Hilfe für die Vorhersage ist es gut wenn man eine Grenze visualisieren kann die einem hilft zu unterschieden wo genau das Modell die Grenzen *gezogen* hat.  
Dafür hilft folgende Funktion die als `helper.py` im gleichen Ordner wie das Jupyter Notebook abgespeichert werden kann und dann einfach im Notebook importiert werden kan.

```python
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np

try:
    get_ipython().magic('matplotlib inline')
    get_ipython().magic('config InlineBackend.figure_formats = set(["retina"])')
except NameError:
    pass

def plot_classifier(model, X, Z, proba = False, xlabel = None, ylabel = None):
    # https://matplotlib.org/examples/color/colormaps_reference.html
    plt.set_cmap("RdYlBu")
    
    x_min = X[:, 0].min() - 1
    x_max = X[:, 0].max() + 1
    
    y_min = X[:, 1].min() - 1
    y_max = X[:, 1].max() + 1
    
    xx, yy = np.meshgrid(
        np.linspace(x_min, x_max, 1000),
        np.linspace(y_min, y_max, 1000)
    )

    if proba:
        zz = model.predict_proba(np.c_[xx.ravel(), yy.ravel()])[:, 1]
        plt.imshow(zz.reshape(xx.shape), 
                   origin = "lower", 
                   aspect = "auto", 
                   extent = (x_min, x_max, y_min, y_max), 
                   vmin = 0, 
                   vmax = 1, 
                   alpha = 0.25)
    else: 
        zz = model.predict(np.c_[xx.ravel(), yy.ravel()])
        plt.contourf(xx, yy, zz.reshape(xx.shape), 
                     alpha = 0.25, 
                     vmin = 0, 
                     vmax = 1)

    plt.scatter(X[:, 0], X[:, 1], c=Z)
    
    if xlabel is not None:
        plt.xlabel(xlabel)
       
    if ylabel is not None:
        plt.ylabel(ylabel)
        
    # Damit wird die Grafik genau so groß angezeigt wie der
    # schattierte Farbbereich:
    plt.xlim(x_min, x_max)
    plt.ylim(y_min, y_max)

    plt.show()
```

**Benutzung:**

```python
# Im notebook kann man die Funktion wie folgt importieren
from helper import plot_classifier

# Benutzung // Beispiel mit den gleichen Daten wie weiter oben beschrieben
# Modell: Blau - JA // Rot - NEIN
# Bei Benutzung der Trainingsdaten sieht man somit direkt wo dieses Modell Fehler macht - Roter Hintergrund + Blauer Punkt etc.
# Parameter: proba = TRUE s.u.
plot_classifier(model, X_train, y_train, proba = False, xlabel = "Alter", ylabel="Interesse")
```
Das mächtige an der Funktion ist, dass wir nicht nur einen 'harten' Übergang visualisieren können `proba = False`, sonder auch einen fließenden `proba = True`. Setzt man diesen Wert auf True entsteh an der Grenzlinie ein weißes Gebiet welches hilft zu verstehen an welchen Stellen das Modell `unsicher` ist.

## Klassifizierung mit mehreren Klassen

