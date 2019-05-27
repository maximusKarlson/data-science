# Numpy

`Numpy` ermöglicht es Vekotren zu verarbeiten und mit ihnen zu rechnen. Dabei wird die CPU des Computers viel weniger belastet, als würde man das gleich in Python mit einer for-Schleife oder ähnlichem 'nachprogrammieren'.

**Verwendung:**  
```
import numpy as np
```

## Beispiele

```
# Erstellung eines Arrays
np.array([1, 2, 3, 4, 5, 6, 7, 8, 9])
```

Man kann sich mit `numpy`auch extrem einfach Vektoren geneieren lassen:
```
np.ones(5)
# Output: array([1., 1., 1., 1., 1.])

np.zeros(5) + 2
# Output: array([2., 2., 2., 2., 2.])

np.repeat(2, 5)
# Output: array([2, 2, 2, 2, 2])

np.arrange([1, 10, 2])
# Output: array([1, 3, 5, 7, 9])

np.linspace(0, 2018, 10)
# Output: array([0., 224, 448, 672.......])
```

**Matrizen mit `numpy`**

```
np.array([1, 2, 3,], [4, 5, 6])

# Zwei Zeilen, 3 Spalten
np.ones((2, 3))
np.zeros((2, 3))

# Marize neu anordnen - 1 Zeile, 7 Spalten
np.arrange(1, 7)
```

`np.where()`

```
noten = np.array([1, 2, 3, 4, 5, 6])

np.where(noten <= 4, "bestanden", "nicht bestanden")
```