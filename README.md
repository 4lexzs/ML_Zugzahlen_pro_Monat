# ML_Zugzahlen_pro_Monat

## Beschreibung des Datensatzes
Dieser Datensatz enthält Informationen über die Zugzahlen in der Schweiz, aufgeteilt nach Streckenabschnitten und Monaten.
Die Daten stammen von der Open Data Plattform der SBB und enthalten folgende Felder:

- Strecke_Bezeichnung: Name der Bahnstrecke
- bezugsmonat: Monat der Datenaufzeichnung
- Abschnitt: Bestimmter Streckenabschnitt
- DTV_Bezugsmonat: Durchschnittliche tägliche Verkehrszahlen für den Monat
- DTV_Vorjahresmonat: Durchschnittliche tägliche Verkehrszahlen des Vorjahresmonats
- geo_point_2d: Geokoordinaten des Abschnitts

## Datenschutz
Die Daten sind öffentlich zugänglich und enthalten keine personenbezogenen Informationen. 
Der Datensatz wurde unter der Open Data Lizenz veröffentlicht.


# Datenanalyse (Teil 2)

Dieser Datensatz enthält Informationen über Zugzahlen auf verschiedenen Strecken, gemessen über mehrere Monate. Der Datensatz umfasst verschiedene Felder wie Streckenbezeichnungen, Bezugsmonate, DTV-Werte (Dynamischer Tagesverkehr) und geografische Koordinaten.

Die Daten wurden von der Schweizerischen Bundesbahnen (SBB) erhoben und enthalten Informationen über den Zugverkehr auf verschiedenen Streckenabschnitten. Der Datensatz ermöglicht die Analyse von Verkehrsmustern und -trends im Schweizer Bahnnetz.

## Datenbeschreibung

Der Datensatz enthält folgende wichtige Felder:
- `Strecke_Bezeichnung`: Name der Zugstrecke
- `bezugsmonat`: Der Monat, auf den sich die Daten beziehen
- `Abschnitt`: Spezifischer Streckenabschnitt
- `DTV_Bezugsmonat`: Durchschnittlicher Tagesverkehr im Bezugsmonat
- `DTV_Vorjahresmonat`: Durchschnittlicher Tagesverkehr im entsprechenden Vorjahresmonat
- `DTV_P_Bezugsmonat`: Personenverkehr im Bezugsmonat
- `DTV_G_Bezugsmonat`: Güterverkehr im Bezugsmonat
- `geo_point_2d`: Geografische Koordinaten des Abschnitts

## Datenschutz

Der Datensatz enthält keine personenbezogenen Daten, da es sich um aggregierte Verkehrsdaten handelt. Alle Informationen beziehen sich auf öffentliche Verkehrsinfrastruktur und stellen keine datenschutzrechtlichen Bedenken dar.

Die Daten sind für Analyse- und Bildungszwecke öffentlich zugänglich gemacht worden und unterliegen den üblichen Nutzungsbedingungen für öffentliche Verkehrsdaten.

## Ziel der Analyse

Im Rahmen dieses Projekts werde ich den Datensatz analysieren, um:
1. Muster und Trends im Zugverkehr zu identifizieren
2. Vorhersagen für zukünftige Verkehrszahlen zu treffen
3. Unterschiede zwischen verschiedenen Strecken und Zeiträumen zu verstehen
4. Die Beziehung zwischen Personen- und Güterverkehr zu untersuchen

Die Ergebnisse könnten für die Verkehrsplanung, Kapazitätsmanagement und strategische Entscheidungen im Bahnverkehr nützlich sein.

# Teil 3: Modellentwicklung und Anwendung

## Modellansatz
Für die Vorhersage der Zugzahlen pro Monat wurde ein Random Forest Regressor-Modell entwickelt. Dieses Modell eignet sich besonders gut für den vorliegenden Datensatz, da es komplexe, nicht-lineare Beziehungen zwischen den Eingabevariablen (Strecken, Zeitpunkte, Abschnitte) und der Zielvariable (DTV_Bezugsmonat) erfassen kann.

## Datenaufbereitung für die Modellierung
Die folgenden Schritte wurden zur Vorbereitung der Daten für die Modellierung durchgeführt:
- Aufspaltung der Datumsinformationen (bezugsmonat) in Jahr und Monat als separate Features
- One-Hot-Encoding der kategorialen Variablen (Strecke_Bezeichnung und Abschnitt)
- Konvertierung der Zielvariable (DTV_Bezugsmonat) in numerisches Format
- Bereinigung fehlender Werte in den relevanten Spalten

## Modelleigenschaften
Der implementierte Random Forest Regressor verwendet folgende Konfiguration:
- 100 Entscheidungsbäume (n_estimators=100)
- Standard-Tiefenkonfiguration für ausbalancierte Genauigkeit und Überanpassungsschutz
- Random State 42 für Reproduzierbarkeit der Ergebnisse

## Begründung der Algorithmuswahl
Die Wahl des Random Forest Regressors basiert auf mehreren vorteilhaften Eigenschaften für diesen speziellen Anwendungsfall:
1. Robustheit gegenüber Ausreissern und nicht normalverteilten Daten
2. Fähigkeit, saisonale und streckenspezifische Muster zu erkennen
3. Geringere Gefahr der Überanpassung im Vergleich zu einzelnen Entscheidungsbäumen
4. Automatische Feature-Importance-Berechnung zur Identifikation der wichtigsten Einflussfaktoren
5. Gute Leistung bei Datensätzen mit vielen kategorialen Variablen nach One-Hot-Encoding

## Modellevaluierung
Die Leistung des Modells wurde auf einem separaten Testsatz (20% der Daten) evaluiert, mit folgenden Ergebnissen:
- Bestimmtheitsmass (R²): 0.9243
- Mittlerer absoluter Fehler (MAE): 14.76 Züge pro Tag
- Wurzel des mittleren quadratischen Fehlers (RMSE): 32.14 Züge pro Tag


# Teil 4: Evaluation

## Aufgabe 4.1 - Feature Importance
Die wichtigsten Felder für das Modell wurden identifiziert und analysiert. Die Top 10 Features sind:
1. Abschnitt_Zürich HB – Zürich Langstrasse (6.4%)
2. Strecke_Bezeichnung_Genève Aéroport - Lausanne (4.7%)
3. Strecke_Bezeichnung_Olten Ost - Heitersberg (4.7%)
4. Strecke_Bezeichnung_Killwangen - Zürich Altstetion (4.4%)  
5. Strecke_Bezeichnung_Zürich Oerlikon-Nord / Zürich Wallisellen (3.7%)

Die Visualisierung der Feature Importance wurde in `feature_importance.png` gespeichert.

## Aufgabe 4.2 - Geeignete Messmetrik
Für das Regressionsmodell wurden folgende Metriken berechnet:
- R² Score: 0.9951 (erklärt 99.5% der Varianz)
- Mean Absolute Error: 4.53 Züge/Tag
- Root Mean Square Error: 12.19 Züge/Tag

Die beste Metrik für dieses Modell ist der R² Score, da er zeigt, wie gut das Modell die Varianz in den Daten erklärt.

## Aufgabe 4.3 - Confusion Matrix
Es wurde eine Confusion Matrix erstellt, die die Zugzahlen in drei Kategorien einteilt:
- Niedrig: < 100 Züge/Tag
- Mittel: 100-300 Züge/Tag  
- Hoch: > 300 Züge/Tag

### Klassifikationsmetriken:
- **Niedrig:** Sensitivität: 95.3%, Präzision: 98.1%, Spezifizität: 99.1%
- **Mittel:** Sensitivität: 98.2%, Präzision: 97.2%, Spezifizität: 97.7%
- **Hoch:** Sensitivität: 98.6%, Präzision: 98.7%, Spezifizität: 99.7%

Die Confusion Matrix wurde in `confusion_matrix.png` visualisiert.

## Aufgabe 4.4 - Zusammenfassung
Das Random Forest Modell zeigt ausgezeichnete Leistung mit einem R² von 0.9951. Die Gründe:
- Starke zeitliche Muster in den Zugzahlen
- Streckenspezifische Charakteristiken werden gut erkannt
- Random Forest kann gut mit kategorialen Variablen umgehen

Verbesserungspotenzial:
- Integration von Wetterinformationen
- Berücksichtigung von Feiertagen und Schulferien
- Wochentagseffekte analysieren

## Erstellt Dateien:
1. `evaluation.ipynb` - Das Jupyter Notebook mit allen Berechnungen
2. `feature_importance.png` - Feature Importance Visualisierung
3. `confusion_matrix.png` - Confusion Matrix Heatmap
4. `actual_vs_predicted.png` - Vergleich von tatsächlichen und vorhergesagten Werten
