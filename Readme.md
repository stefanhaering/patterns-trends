# Proposal for Semester Project

**Patterns & Trends in Environmental Data / Computational Movement
Analysis Geo 880**

| Semester:      | FS23                                     |
|:---------------|:---------------------------------------- |
| **Data:**      | Posmo-Daten von Stefan und Miriam  |
| **Title:**     | Wer verschwendet mehr Zeit mit Warten an ÖV-Haltestellen?                |
| **Student 1:** | Stefan Häring                       |
| **Student 2:** | Miriam Jakob                       |

## Abstract 
<!-- (50-60 words) -->

## Research Questions
In unserer Projektarbeit möchten wir unsere tägliche Wartezeit an Haltestellen von öffentlichen Verkehrsmitteln (ÖV) untersuchen. Dabei wird ausschliesslich der Beginn einer Reise betrachtet. Folgende Fragen sollten beantwortet werden:
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
https://data.geo.admin.ch/ch.bav.haltestellen-oev/haltestellen-oev/haltestellen-oev_2056_de.csv.zip


## Analytical concepts
<!-- Which analytical concepts will you use? What conceptual movement spaces and respective modelling approaches of trajectories will you be using? What additional spatial analysis methods will you be using? -->

Um den Start einer Reise zu finden, werden die Daten auf eine bestimmte Abfolge von Bewegungen (Segmente) durchsucht. Diese Bewegungen werden durch deren Geschwindigkeit definiert und sollten in folgender Reihenfolge vorliegen:
1. keine Bewegung: Person über längere Zeit (difftime >10 min) am selben Ort  
2. langsame Bewegung: Gehen/Fahrrad (Segmente mit Geschwindigkeit <35 km/h)
3. Wartezeit: Person am selben Ort (Difftime (Min(Segment schnell), Max(Segment langsam)))
4. schnelle Bewegung: ÖV (Segmente mit Geschwindigkeit >=35 km/h)

Zusätzliche räumliche Analyse: Die Positionen der Wartezeit werden auf ihre Übereinstimmigkeit mit Standorten von ÖV-Haltestellen überprüft. (Buffer um Haltestellen mit Positionsdaten der Wartezeit verschneiden.)

## R concepts
<!-- Which R concepts, functions, packages will you mainly use. What additional spatial analysis methods will you be using? -->
Segmente erstellen mit moving window.
- langsame Bewegung: Gehen/Fahrrad (Segmente mit Geschwindigkeit <35 km/h)
- schnelle Bewegung: ÖV (Segmente mit Geschwindigkeit >=35 km/h)

Zeit an Standort ermitteln mit difftime:
- keine Bewegung: Person über längere Zeit (difftime >10 min) am selben Ort  
- Wartezeit: Person am selben Ort (difftime (Min(Segment schnell), Max(Segment langsam)))

Finden der Wartezeiten mit lag/lead (Package "dbplyr"):
Langsame und schnelle Bewegungen werde in einer zusätzlichen Spalte mit "langsam" und "schnell benennt. Mit lag kann eine Bewegungsänderung von "langsam" zu "schnell" festgestellt werden. Diese werden mit "Ende Wartezeit" in einer separaten Spalte benannt. Die Zeile davor wird mit "Start Wartezeit" benannt.

Zusätzliche Analyse mit Geoprocessing-Tools:
Die Positionen der Wartezeit werden auf ihre Übereinstimmigkeit mit Standorten von ÖV-Haltestellen überprüft. Buffer um Haltestellen mit Positionsdaten der Wartezeit verschneiden.

Auswertung zur Beantwortung der Fragestellung

## Risk analysis
<!-- What could be the biggest challenges/problems you might face? What is your plan B? -->
Möglicherweise gibt es bei Reisen mit Zwischenstops (z.B. Zug haltet an Bahnhof, Umsteigen) zusätzliche Segmente, welche als "langsame Bewegung" zugeordnet werden. Dieses Problem könnte mit der Grösse des moving window entgegengewirkt werden.
Durch das Kriterium "1. keine Bewegung: Person über längere Zeit (difftime >10 min) am selben Ort" der Bewegungsabfolge könnten Reisezwischenstops relativ einfach entfernt werden. Die Umsetzung im R könnte jedoch eine Herausforderung darstellen, da die Daten nicht in Form von Segmenten vorliegen.
Da wir die gauen Wartezeitpunkte erhalten möchten, ist es wichtig den genauen Endpunkt des Segments "langsame Bewegung" und den genauen Startpunkts des Segments "schnelle Bewegung" zu wissen. Mit einem moving window könnte dies eine Herausforderung darstellen.

## Questions? 
<!-- Which questions would you like to discuss at the coaching session? -->
- moving window: Wie erhalten wir einen genauen Start- und Endpunkt eines Segments?
- Wie findet man eine Abfolge von relevanten Segmenten (Annahme: Zwischenstops der Zugreise verursachen Segmente mit "langsame Bewegung")
- (Wie finden wir die Wartezeit? Es scheint ein Muster von 3 Punkten mit selben Datetime am Start des Wartens zu geben. Beim Start der Reise gibt es 2 Punkte mit selbem Datetime.)


