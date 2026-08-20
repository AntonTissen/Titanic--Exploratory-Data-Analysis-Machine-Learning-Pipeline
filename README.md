# Titanic - Exploratory Data Analysis & Machine Learning Pipeline

Dieses Projekt ist eine durchgehende Datenanalyse- und Machine-Learning-Pipeline für den berühmten **Titanic-Datensatz** von Kaggle. Das Ziel ist es, vorherzusagen, welche Passagiere den Schiffbruch der Titanic überlebt haben.

## 🎯 Projektziel
Entwicklung eines maschinellen Lernmodells (Entscheidungsbaum), das basierend auf demografischen und reisebezogenen Daten der Passagiere vorhersagt, ob diese überlebt haben (`Survived` = 1) oder nicht (`Survived` = 0).

---

## 🛠️ Eingesetzte Methoden & Workflow

Das Projekt wurde Schritt für Schritt ohne vorgefertigte Schablonen entwickelt, mit Fokus auf sauberes Feature Engineering und logische Datenaufbereitung:

### 1. Datenbereinigung & Umgang mit fehlenden Werten (Imputation)
*   **Embarked:** Die wenigen fehlenden Werte wurden mit dem Modus (dem am häufigsten vorkommenden Hafen) aufgefüllt.
*   **Cabin:** Da über 77 % der Kabineneinträge fehlten, wurde die Spalte in ein neues binäres Merkmal `Has_Cabin` (1 = Kabine bekannt, 0 = unbekannt) umgewandelt.
*   **Age:** Fehlende Alterswerte wurden nicht einfach pauschal ersetzt, sondern präzise über den Median der extrahierten Titel-Gruppen (siehe Feature Engineering) imputiert.

### 2. Feature Engineering (Merkmalserstellung)
*   **Titel-Extraktion:** Aus den Passagiernamen wurden die Titel (z. B. *Mr, Miss, Mrs, Master*) isoliert. Seltene Titel wurden zu einer Kategorie `Rare` zusammengefasst. Das diente der besseren Altersschätzung und spiegelt den sozialen Status wider.
*   **Familiengröße (`Family_Size`):** Erstellt durch die Kombination von `SibSp` (Geschwister/Ehepartner) und `Parch` (Eltern/Kinder) plus dem Passagier selbst.

### 3. Datenvorbereitung (Preprocessing)
*   **Kategoriales Encoding:** 
    *   Binäres Encoding für das Geschlecht (`Sex`: female = 0, male = 1).
    *   One-Hot-Encoding (Erstellung von Dummy-Variablen) für die Spalten `Title` und `Embarked`.
*   **Feature Selection:** Entfernung irrelevanter oder verrauschter Spalten (`PassengerId`, `Name`, `Ticket`, `Cabin`).

### 4. Modellierung & Evaluation
*   Aufteilung der Daten in 80 % Trainings- und 20 % Testdaten (**Train-Test-Split**).
*   Training eines **Decision Tree Classifiers** (Entscheidungsbaums) auf den Trainingsdaten.
*   Evaluierung der Genauigkeit auf den zuvor ungesehenen Testdaten.

---

## 📊 Wichtigste Erkenntnisse (Insights)

Während der explorativen Analyse (EDA) wurden folgende Muster aufgedeckt:
*   **Der Geschlechter-Effekt:** Frauen hatten eine Überlebensrate von **74,2 %**, Männer von nur **18,9 %** (Bestätigung von "Frauen und Kinder zuerst").
*   **Der Kabinen-Effekt:** Passagiere mit einer dokumentierten Kabinennummer (`Has_Cabin` = 1) hatten in allen Klassen eine signifikant höhere Überlebenschance (66,7 % vs. 30,0 %).
*   **Der Familien-Effekt:** Alleinreisende und sehr große Familien (ab 5 Personen) hatten deutlich geringere Überlebenschancen. Kleine Familien (2-4 Personen) hatten mit bis zu 72 % die besten Chancen.

---

## 🏆 Testergebnis

*   **Modell:** Decision Tree Classifier
*   **Genauigkeit (Accuracy) auf den Testdaten:** **78,2 %**
*   Das Modell übertrifft die Baseline (Raten oder "alle sterben") von ca. 61,6 % deutlich und beweist die hohe Aussagekraft der generierten Features.

---

## 💻 Tech-Stack
*   **Sprache:** Python 3
*   **Bibliotheken:** Pandas, Scikit-Learn
