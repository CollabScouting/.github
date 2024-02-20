# Projektmanagment

[![Creative Commons Lizenzvertrag](https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-nc-sa/4.0/)  
Ironscout App von Collabscouting ist lizenziert unter einer [Creative Commons Namensnennung - Nicht-kommerziell - Weitergabe unter gleichen Bedingungen 4.0 International Lizenz](http://creativecommons.org/licenses/by-nc-sa/4.0/).

# Framework 

## App
Flutter Version: 
Flutter 2.10.5 • channel stable • https://github.com/flutter/flutter.git
Framework • revision 5464c5bac7 (9 months ago) • 2022-04-18 09:55:37 -0700
Engine • revision 57d3bac3dd
Tools • Dart 2.16.2 • DevTools 2.9.2

## Server
Django Version:

## Manager
Angular Web-Framework [Angular CLI Overview and Command Reference](https://angular.io/cli) version 13.3.4

## Bonus

Python Skript zum Download der Fotos für die Urkunden [hier](https://github.com/CollabScouting/projectmangement/tree/master/Urkunden/Picture_Download)

# Beschreibung
Anbei die Beschreibung des Bezirksvorstandes. Tatsächliche Softwarelösungen können hiervon abweichen!
**Für die Funktionalität können die [Anleitungen](https://github.com/CollabScouting/projectmangement/blob/master/Anleitungen%20App_2022-09-23.pdf) für Stationsteams und Läufergruppen angeschaut werden.**

## Spielgruppen App für den IronScout2222

Jedes Jahr im Herbst findet für Rover, Leiter und Mitarbeiter der Deutschen Pfadfinderschaft Sankt Georg (DPSG), des Bundes der Pfadfinderinnen und Pfadfinder (BdP), des Verbandes Christlicher Pfadfinderinnen und Pfadfinder (VCP) und der Pfadfinderinnenschaft Sankt Georg (PSG) der mittlerweile legendäre Ironscout statt.
Angelehnt an den Ironman ist der Ironscout ein 22-stündiger Lauf. Als Team muss man in dieser Zeit, nur mit Hilfe einer Karte und einem Kompass, möglichst viele Stationen finden, an denen man verschiedene Aufgaben absolvieren muss.
Für die Ausführung der Stationsaufgaben werden Punkte verteilt, durch die am Ende des Laufes schließlich der Sieger der Läuferteams aus ganz Deutschland gekürt wird. Zusätzlich wird die kreativste und beste Station für ihre Arbeit belohnt.
Die Aufnahme und Zusammenrechnung der Punkte für das Großspiel stellt eine Herausforderung dar, da die Daten oft fehlerhaft auf Papier erhoben und durch zu Auswertung zusammengetragen werden müssen, was eine weitere Fehlerquelle darstellt. Zusätzlich herrscht direkt nach Ende des Spiels ein enormer Zeitdruck, da die Siegerehrung wenige Stunden nach Ende stattfindet. 


## Aufgabenstellung:
Die Läuferteams bei Ironscout sollen mit einer mobilen Handy-App unterstützt werden. Die Mobile App tauscht die Daten mit einem zentralen Server aus, von dem die Konfigurationen geladen wird und auf dem die Ergebnisse des Spiels ausgewertet werden. Sie App bietet nach dem Konzept der Location Based Services, Spielaufgaben an verschiedenen Orten an.

## Funktionale Anforderungen der App.
*	Login in die App ist nur registrierten Teams möglich. Die Authentifizierung erfolgt über QR-Code oder User Name Passwort. Die Authentifizierungsinformationen werden auf dem zentralen Server bereitgestellt.
*	Das anmelden mit mehreren Handys es ist möglich, aber nur ein Device kann in einem Moment verwendet werden. Wechsel zwischen den Devices soll möglich sein. (Knopf: Ich bin dran.)
*	Die App nimmt die aktuelle Position des Devices über GPS-Koordinaten auf, und zeigt sie auf einer Karte an.
*	Optional: Der GPS-Track des Laufes soll gespeichert und auf der Karte angezeigt werden. 
  *	Optional: Export des Tracks in einem Standardformat.
*	Die aktuelle Position des Teams wird an den zentralen Server übermittelt.
*	Wenn die Teams spezielle Orte erreichen, sollen Spielaufgaben freigeschaltet werden. Die Geoinformationen zu den Orten werden auf dem zentralen Server bereitgestellt.
*	Es gibt zwei Arten von Orten. Tote Stationen und Spielposten.
  *	Tote Stationen: Hier müssen Gruppen eine kleine Aufgabe lösen. Zum Beispiel ein Foto machen oder einen kleinen Text schreiben. Die Erfüllung der Aufgabe (also das Foto oder der Text mit Informationen zum Ort) sollen an den zentralen Server übermittelt werden.
  *	Stationsorte: An den Stationsorten gibt es Posten-Cluster. Wenn die Spielgruppe ein Cluster erreicht, können Sie dort an einem Spiel teilnehmen. Das Spiel wird separat bewertet. Allerdings können die Spielegruppen das Spiel bewerten. Also müssen die Spieler die konkrete Stationsgruppe auswählen und können dort eine Bewertung für das Spiel abgeben. Die Bewertungsinformationen werden an die Server übermittelt.
*	Unabhängig vom erfolgreichen Login, ist die Teilnahme an den Spielen nur in einem vorgegebenen Zeitfenster möglich. Diese wird vom Server aus vorgegeben.
*	Optional: Notfall-Telefon: aus der App heraus soll eine zentrale Telefonnummer angerufen werden können.


## Zentraler Server:
*	Hier wird die Spielkonfiguration eingetragen
*	Hier werden die Ergebnisse der Spiele gesammelt und angezeigt.
  *	Alle erreichten Orte. 
  * Zu den Toten Stationen sollen Fotos und Texte für eine manuelle Kontrolle prüfbar sein.
  * Zu den Spielgruppen werden die einzelnen Bewertungen angezeigt. 
*	Alle Ergebnisse eines Teams sollen zusammengefasst werden.
  * Für jedes Team alle Punkte aus den toten Stationen.
  * Für die (Achtung) Stationsgruppen alle Bewertungen der Teams.
*	Die aggregierten Ergebnisse sollen in einem Exportformat ausgelesen werden können. Zum Beispiel CSV.
*	Die aktuellen oder zuletzt bekannten Positionen der Teams sollen während des Spiels auf einer Karte angezeigt werden.
*	Die GPS-Tracks der Teams sollen auch zentral gehalten werden.
*	Ein Export des gelaufenen Weges soll am Spielende möglich sein. Export als GPS-Track und Bild.

Technische Anforderungen:
*	Die App soll auf gängigen Android und IOs Geräten laufen.
*	Das gesamte System muss während des Spiels mit 140 Gruppen funktionieren.




Architektur

1.	Das verteilte System soll ein (zentrales) Backend besitzen, auf dem die Spielergebnisse aufgezeichnet und automatisch ausgewertet werden. 
2.	Dazu gibt es Clients auf dem die Funktionalen Anforderungen angeboten.
  *	Ein Frontend für die Spielgruppen (Handy App)
  *	Ein Frontend für die Spielleitung (Potentiell Browser-WebApp)
  *	Optional: Ein Frontend für die Stationsteams (Potentiell Browser-WebApp) auf dem die Spielergebnsise der einzelnen Teams eingetrgen werden. (Für diese Arbeit out of Scope.)

Backend
Technische Anforderungen
*	Standard (Cloud) Datenbank (SQL oder noSQL?) Mit Replikaiton oder one
*	Web API (REST) zur Connection der Clients/Frontends
*	Wo gehostet?
*	Wie wird Datensynchronisation auch bei sporadischen offline Verbindungen sichergestellt?
  * Replikation der Datenbank
  * Wedemarks?/Last update?


Handy-App
*	Herausforderung: Plattformübergreifend.
*	Mögliche Lösungen: 
  * Progressive Web-Anwendung. – Wie komme ich an die Geodaten?
  * Platformübergreifend Anwendungen. Z.B. Xamarin. – Wie synchronisiere ich die Daten?




