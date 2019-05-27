# Nominale Daten

Die `one-hot-methode` ist eine Funktion in `pandas` die es ermöglicht nominale Daten in die lineare regression miteinzubeziehen.
Dabei werden neue Spalten erstellt. Diese Spalten enthalten viele 0-Werte aber kodieren die vorher definierte (nominale) Spalte.

**Pandas-Funktion:**  
```
import pandas as pd
df = pd.read_csv("./filename")

df_nom = pd.get_dummies(df, columns = "beispielspalte")
```
`pd.get_dummies`erzeugt standardmäßig ein neues Dataframe. Als Konfention wird das vorher erstellte `df` überschrieben.
```
df = pd.get_dummies(df, columns = "beispielspalte")
```

**WICHTIG:**  
Erweitert man ein Dataframe mit der `one-hot-methode` muss man die letzte Spalte der neu erzeugten Spalten weglassen.  
Der Hintergrund dafür ist die Lineare Abhängigkeit.

*Beispiel:*  
Hat man mit der `one-hot-methode` ein Dataframe um die Spalten *Köln, München und Berlin* erweitert, dann kann man sich aus den Spalten Köln und München erschließen ob ein gewisses Hotel in Berlin steht oder nicht. (Wenn es in München oder Köln steht kann es nicht in Berlin stehen <->).

Daher vermeidet man diese Redundanz indem man die letzte Spalte einfach wegglässt!

## Code-Beispiel

```
import pandas as pd

df = pd.read_csv("./filename")
df = pd.get_dummies(df, columns = "beispielspalte")
df.head()

# Lineare Regression inklsuive nominale Daten

Y = df[["Preis in Mio"]].values
X = df[["Gewinn", "Quadratmeter", "Stadt_Köln", "Stadt_München"]].values

from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, Y, random_state = 0, test_size = 0.25)

model = LinearRegression()
model.fit(X_train, y_train)

print(model.score(X_test, y_test))
```

**Interpretation Beispiel-Output:**

`model.score()-output`: Vergleichbar mit $R^{2}$-Wert bevor die `one-hot-methode` usgeführt wurde (Müsste $R^{2}$-Wert erhöhen)

*Koeffizienten deuten:*

`model.coef_` liefert ein Array zurück  
Beispielarray: `array([[1.13, 3.88, -3.27, -6.34]])`

Interessant sind vorallem die zwei letzten Zahlen, da diese den Einfluss vom Standort Köln und München beschreiben.
Beziehen tuen sich beide Werte auf den Standort Berlin (weggelassene Spalte).  
Ein Hotel in Berlin hat den Preis von 100% - in Köln sind die Hotels *-3.27* mal einen bestimmten Wert günstiger und in München sind die Hotels *-6.34* mal einen Wert günstiger als in Berlin.  
D.h. in München sind die Hotels am günstigsten und in Berlin am teuersten.

Mit der `predict` Funktion kann man sich auch Preise von Hotels, abhängig vom Standort schätzen lassen:
```
model.predict([[10000, 300, 0, 0], [10000, 300, 1, 0], [10000, 300, 0, 1]])
```
Dieser Code würde nun jeweils ein Hotel für Berlin, Köln und München schätzen. (Codiert durch die letzten zwei Spalten)  