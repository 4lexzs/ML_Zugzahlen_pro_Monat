# ML_Zugzahlen_pro_Monat

## Datensatzbeschreibung

Der verwendete Datensatz enthält Verkehrszahlen für verschiedene Zugstrecken der SBB (Schweizerische Bundesbahnen). Er umfasst die folgenden Hauptkomponenten:

- **Strecke_Bezeichnung**: Name der Bahnstrecke
- **bezugsmonat**: Monat, auf den sich die Daten beziehen
- **Abschnitt**: Spezifischer Abschnitt der Strecke
- **DTV_P_Bezugsmonat**: Durchschnittlicher täglicher Personenverkehr im Bezugsmonat (Zielwert)
- **DTV_P_Vorjahresmonat**: Personenverkehr im entsprechenden Monat des Vorjahres
- **DTV_G_Bezugsmonat**: Durchschnittlicher täglicher Güterverkehr im Bezugsmonat
- **Verschiedene geografische Informationen**: Abschnitt_von, Abschnitt_bis, geo_point_2d

Der Datensatz umfasst mehr als 15.000 Einträge, die die monatlichen Verkehrszahlen für über 1.300 eindeutige Streckenabschnitte enthalten.

## Datenschutzaspekte

Der verwendete Datensatz enthält öffentlich zugängliche Verkehrsdaten der SBB und wurde unter einer offenen Lizenz veröffentlicht. Es handelt sich um aggregierte Daten, die keine personenbezogenen Informationen enthalten. Die Daten zeigen lediglich die durchschnittlichen täglichen Verkehrszahlen für bestimmte Streckenabschnitte.

Da es sich um offene Verkehrsstatistiken handelt, bestehen keine besonderen Datenschutzbedenken. Die Daten erlauben keine Rückschlüsse auf individuelle Personen oder deren Reiseverhalten. Sämtliche Analysen und Vorhersagen beziehen sich auf aggregierte Verkehrszahlen und nicht auf einzelne Zugfahrten oder Personen.

## Projektziel

Das Hauptziel dieses Projekts ist die Entwicklung eines Machine-Learning-Modells, das zukünftige Personenverkehrszahlen für Zugstrecken basierend auf historischen Daten, geografischen Merkmalen und anderen relevanten Faktoren vorhersagen kann. Diese Vorhersagen können für die strategische Planung, Kapazitätsoptimierung und Ressourcenallokation im Bahnverkehr genutzt werden.

## Projektstruktur

Das Projekt ist in drei Hauptnotebooks unterteilt:

1. **data_description.ipynb**: Analyse und Aufbereitung der Daten
   - Datenimport und Bereinigung
   - Explorative Datenanalyse
   - Feature-Engineering und -Auswahl
   - Datenvisualisierung

2. **model.ipynb**: Modellierung und Vorhersage
   - Datensplit (Training/Test)
   - Algorithmusauswahl und -training
   - Modellbewertung
   - Manuelle Überprüfung von Vorhersagen

3. **evaluation.ipynb**: Detaillierte Modellevaluation
   - Feature-Importance-Analyse
   - Berechnung von Leistungsmetriken
   - Konfusionsmatrixanalyse
   - Sensitivitäts- und Spezifitätsberechnungen

## Modellansatz

Für die Vorhersage der Zugzahlen pro Monat wurde ein Random Forest Regressor-Modell entwickelt. Dieses Modell eignet sich besonders gut für den vorliegenden Datensatz, da es:

1. Komplexe, nicht-lineare Beziehungen erfassen kann
2. Robust gegenüber Ausreissern und nicht normalverteilten Daten ist
3. Saisonale und streckenspezifische Muster erkennen kann
4. Eine automatische Feature-Importance-Berechnung bietet
5. Gut mit kategorialen Variablen nach Encoding umgehen kann

## Ergebnisse und Erkenntnisse

Das trainierte Random-Forest-Regressionsmodell erreicht einen beeindruckenden R²-Wert von über 0,99, was bedeutet, dass es mehr als 99% der Varianz in den Personenverkehrszahlen erklären kann. Die wichtigsten Erkenntnisse sind:

1. Der Personenverkehr im Vorjahresmonat ist mit Abstand der stärkste Prädiktor für aktuelle Verkehrszahlen, was auf eine hohe zeitliche Stabilität der Verkehrsmuster hindeutet.

2. Der Güterverkehr und die spezifische Strecke haben deutlich geringeren, aber dennoch messbaren Einfluss auf die Personenverkehrszahlen.

3. Die Kategorisierung in niedrige, mittlere und hohe Verkehrsaufkommen zeigt, dass das Modell besonders gut darin ist, zwischen diesen Kategorien zu unterscheiden, mit hoher Sensitivität und Spezifität für alle Kategorien:
   - **Niedrig (< 50 Züge/Tag):** Sensitivität: 95.3%, Spezifität: 99.1%
   - **Mittel (50-150 Züge/Tag):** Sensitivität: 98.2%, Spezifität: 97.7%
   - **Hoch (> 150 Züge/Tag):** Sensitivität: 98.6%, Spezifität: 99.7%

4. Über 90% der Vorhersagen liegen innerhalb einer 10%-Fehlergrenze, was für Verkehrsplanungszwecke mehr als ausreichend ist.

## Technologien und Methoden

- **Programmiersprache**: Python 3
- **Hauptbibliotheken**: pandas, numpy, scikit-learn, matplotlib, seaborn
- **Algorithmus**: Random Forest Regressor
- **Evaluationsmetriken**: RMSE, R², Konfusionsmatrix, Sensitivität, Spezifität

## Mögliche Verbesserungen

Für zukünftige Iterationen dieses Projekts könnten folgende Verbesserungen implementiert werden:

1. Einbeziehung weiterer Features wie Streckenlänge, Bevölkerungsdichte entlang der Strecke oder Anzahl der Haltestellen
2. Berücksichtigung von Feiertagen, Schulferien oder besonderen Ereignissen
3. Analyse der Wochentagseffekte auf das Verkehrsaufkommen
4. Integration von Wetter- und Klimadaten
5. Erprobung fortgeschrittenerer Algorithmen wie Gradient Boosting oder neuronale Netze
6. Entwicklung separater Modelle für verschiedene Streckentypen (z.B. Hauptstrecken vs. Nebenstrecken)
