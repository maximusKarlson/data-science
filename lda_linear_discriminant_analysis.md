# LDA - Linear Diskrimininazanalyse

Die `lda` ist verwandt mit der `pca` und hat ebenfalls eine Dimensionsreduktion zum Ziel.  Der Unterschied hierbei ist aber, dass die lda das Hauptziel einer `besseren Unterscheidung zwischen zwei Kriterien` zum Ziel hat. Und nicht wie bei der pca die Varianz zur Hauptachse darstellt.  

## Funtkionsprinzip

Grundsätzlich erstellt die `lda` eine lineare Regressionskurve anhand der Daten (x und y-Achse beim linearen Beispiel) und stellt die Abstände der Datenpunkt zu dieser Achse dann da.

Im zweiten Schritt wird der Mittelwert der beiden Kategorien berechnet und versucht diese Mittelwerte möglichst weit voneinander entfernt auf der *reduzierten* 1-D Darstellung (ursprünglich 2-D) darzustellen.

Innerhalb jeder Kategorie soll zudem die Varianz reduziert werden. (wird meistens mit $$ s^2 $$ dargestellt).

Beide Kriterien werden gleichzeitig betrachtet bei folgenden Funtkion:

$$\frac{mü_{1} - mü_{2}{1}}{s_{1}^2 + s_{2}^2}$$

**Wichtig:**  
Für eine optimale `lda` sollte der Zähler (oben) der oberen Funtkion möglichst groß und der Nenner (nenner) möglichst klein sein.