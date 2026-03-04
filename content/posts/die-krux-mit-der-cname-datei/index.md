---
title: Die Krux mit der verflixten CNAME Datei
date: 2026-03-08
tags:
- Dev
- Hugo
---

{{< lead >}}
Nur weil man etwas schon hundertmal gemacht hat, heißt das noch lange nicht, dass es beim hundertundersten Mal automatisch funktioniert.
{{< /lead >}}

Was für ein Rätsel musste ich dieses Mal wieder lösen? Nach jedem Deployment über GitHub Actions verschwand plötzlich meine Custom Domain aus GitHub Pages. 

Einfach wieder weg.

Ich bin fast verrückt geworden. 

Ich hatte mich genau an das Hugo-Tutorial gehalten und dachte eigentlich, dass ich mich mit GitHub Pages ganz gut auskenne, schließlich hatte ich schon etliche Seiten mit 11ty, Jekyll und Material for MKDocs gebaut.

Was ich allerdings noch nicht wirklich kannte, war Hugo. Ich habe schon viele verschiedene Static-Site-Generatoren benutzt, aber eben noch nie Hugo. _Natürlich_ war mein erster Gedanke: "Verdammtes GitHub Pages, das ist sowas von broken." Also habe ich in diese Richtung recherchiert, mir verschiedenste anderen Workflows angeschaut und den einen oder anderen auch direkt umgesetzt um zu prüfen, ob damit das Problem behoben war. 

War es nicht. Also wieder zwei Haare weniger am Kopf. 

Das Build-Artifakt schien für mich ebenfalls in Ordnung. Nach dem dritten Durchlauf dämmerte es mir: _Was, wenn bei Hugo die CNAME-File nicht ins Root-Verzeichnis gehört, sondern woanders hin?"_

Genau da lag das Problem: Die Datei `CNAME`, die für die Custom Domain notwendig ist, lag nicht im static-Ordner von Hugo. Dadurch wurde sie bei jedem Build überschrieben beziehungsweise gelöscht. Das Ergebnis war, dass GitHub Pages nach jedem Deployment die Custom Domain wieder verloren hat, da die Datei gelöscht worden war.

Ziemlich verrückt, wenn man bedenkt, wie lange ich danach gesucht habe.

Was lernt man daraus? Nur weil man etwas schon hundertmal gemacht hat, heißt das noch lange nicht, dass es beim hundertundersten Mal automatisch funktioniert. Sobald ein neues Tool ins Spiel kommt, gelten plötzlich wieder ein paar andere Regeln.