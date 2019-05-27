# Principal Component Analyse (Dimensionsreduktion)

Nehmen wir das Beispiel Nahrungsmittel: Kohlenhydrate, Eiweiß, Fett usw.  
Um zu entscheiden ob man wirklich alle Eigenschaften / Dimensionen braucht, macht man eine PCA.  
Brennwert wird zum Beispiel aus mehreren der anderen Variablen berechnet. D.h. herrscht eine Abhängigkeit und man kann die entsprechende Dimension weglassen.

**Mathematisch:** Wir haben k Dimensionen und wollen n<k Dimensionen

Grundsätzlich besitzt PC1 die größte Varianz des gesamten Datensatzes. PC2 die zweitgrößte Varianz etc.  
Hat man zum Beispiel eine 'normale' Regression zwischen einer X und Y Achse, dreht man einfach die Regressionsgerade zur neuen X-Achse.
Somit beschreibt nun die neue X-Achse (PC1) die größte Varianz. Die alte Y-Achse gibt jetzt wieder nur noch die Höhe an, jedoch wird diese nun als PC2 beschrieben. Und wie man in dem Schaubild dann sieht,  beschreibt diese Achse eine geringere Varianz (hoch / runter) als die PC1 (links / rechts)

![PCA Analyse](/Users/maximilianstaebler/code/udemy/data-science/bilder/pca.png)

**Merksätze:**  
Hierbei werden neue Dimensionen gefunden, die absteigend möglichst viel Varianz erfassen  
Die erste Dimension enthält die meiste Varianz, die zweite dann etwas weniger etc.  
Dadurch können wir die Daten "automatisch" komprimieren  
Neue Dimensionen werden automatisch gefunden  
Können uns angeben lassen, wie viel Varianz enthalten geblieben ist  

**Achtung:** Neue Dimensionen haben keine direkte Bedeutung mehr! PC's sind Kombinationen aus den Daten

# PCA un d PCA-Regression

Die PCA braucht im Vergleich zur PCA-Regression eine Vorgabe auf wie viele Hauptkomponenten der Datensatz reduziert werden soll.  
Die PCA-Regression dagegen hilft dabei herauszufinden welche Anzahl an Hauptkomponenten am besten geeignet ist.