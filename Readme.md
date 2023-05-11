# Proposal for Semester Project

**Patterns & Trends in Environmental Data / Computational Movement
Analysis Geo 880**

| Semester:      | FS23                                     |
|:---------------|:---------------------------------------- |
| **Data:**      | Posmo-Daten von Stefan (seit 28.4.23) und Miriam (seit 3.5.23)  |
| **Title:**     | Wer verschwendet mehr Zeit mit Warten an ÖV-Haltestellen?                |
| **Student 1:** | Stefan Häring                       |
| **Student 2:** | Miriam Jakob                       |

## Abstract 
xxxxxxxxxxxxxxxxxxxxxxxxxxxx
<!-- (50-60 words) -->

## Research Questions
In unserer Projektarbeit möchten wir unsere tägliche Wartezeit an Haltestellen von öffentlichen Verkehrsmitteln (ÖV) untersuchen. Dabei wird ausschliesslich der Beginn einer Reise betrachtet. Dafür sollten folgende Fragen beantwortet werden:
Wie oft reisen wir mit den ÖV?
Sind die Wartezeiten von Reise zu Reise unterschiedlich lang?
Wer verbringt durchschnittlich mehr Wartezeit an den Haltestellen?


<!-- (50-60 words) -->

## Results / products
<!-- What do you expect, anticipate? -->
Anhand der Startpunkte einer Reise erhalten wir die Gesamtanzahl unserer ÖV-Reisen. Miriams Anzahl wird höher sein als Stefans.
Pro Startpunkt wird eine Wartezeit angegeben. Diese Daten zeigen, wie unterschiedlich die Wartezeiten der jeweiligen Person sind. Hier werden die Daten von Stefan eine grössere Streuung aufweisen als diejenigen von Miriam.
Insgesamt ist der Mittelwert der Wartezeiten bei Stefan grösser als bei Miriam.


## Data
<!-- What data will you use? Will you require additional context data? Where do you get this data from? Do you already have all the data? -->
Als Grundlage dienen Posmo-Daten von Miriam (3.5.23-heute) und Stefan (28.4.23-heute). Diese Daten liegen als CSV-Datei vor und beinhalten u.a. Datum & Zeit ("datetime") und x-Koordinaten ("long_x") und y-Koordinaten ("lat_y").
Um ähnliche Ereignisse, welche nicht an ÖV-Haltestellen stattfinden, auszuschliessen, wird die Position der Haltestellen benötigt. Dafür verwenden wir den Datasatz "Haltestellen des öffentlichen Verkehrs" vom Bundesamt für Verkehr (BAV). Dieser steht öffentlich zur Verfügung:
https://www.geocat.ch/geonetwork/srv/ger/catalog.search#/metadata/841d42ff-8177-4e07-a96b-e8e5455ae048


## Analytical concepts
<!-- Which analytical concepts will you use? What conceptual movement spaces and respective modelling approaches of trajectories will you be using? What additional spatial analysis methods will you be using? -->

-keine Bewegung ->langsame Bewegung (Gehen/Fahrrad)->Pause ->schnelle Bewegung ÖV
-Buffer um Bhf ->Validierung

## R concepts
<!-- Which R concepts, functions, packages will you mainly use. What additional spatial analysis methods will you be using? -->

## Risk analysis
<!-- What could be the biggest challenges/problems you might face? What is your plan B? -->

## Questions? 
<!-- Which questions would you like to discuss at the coaching session? -->
-Bahnhof-Layer für Validierung
