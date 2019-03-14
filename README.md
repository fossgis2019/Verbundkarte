# Verbundkarte als Slippy Map

FOSSGIS 2019 Demo: Verbundkarte als Slippy Map konvertieren

Die [Verbundekarte](http://kursbuch.bahn.de/hafas/kbview.exe/dn?rt=1&mainframe=IK_verbund) aus dem [Elektronischem Kursbuch](http://kursbuch.bahn.de/hafas/kbview.exe/dn?rt=1&mainframe=search)
wird als interaktive Karte im Internet veröffentlicht.

Leider ist die Bedienung dieser Karte etwas verältet und entspricht nicht der aktuellem Stand der Technik.

In diesem Demo konvertieren wir diese Karte in eine moderne Leaflet-basierte interaktive Karte.

# Rechtlicher Hinweis

Das Urheberrecht an den Kartendaten liegt bei DB Netz AG, I.NPP 41 (V).

Aus urheberrechtlichen Gründen ist die Karte nur interaktiv zur Tabellensuche nutzbar, darf aber nicht ausgedruckt werden.

# Werkzeuge

* [Wget](https://www.gnu.org/software/wget/) um Daten herunterzuladen
* [ImageMagick](https://www.imagemagick.org/) um Bilder zu verarbeiten
* [libvips](https://libvips.github.io/libvips/) um Kachel-Pyramide zu erstellen
* [Leaflet](https://leafletjs.com/) als Web Mapping Client

# Kartenbild erstellen

## Daten herunterladen

```
wget -q -N -P data http://kursbuch.bahn.de/hafas-res/img/kbview/karten/vk-0-0.jpg
wget -q -N -P data http://kursbuch.bahn.de/hafas-res/img/kbview/karten/vk-0-1.jpg
wget -q -N -P data http://kursbuch.bahn.de/hafas-res/img/kbview/karten/vk-0-2.jpg
...
wget -q -N -P data http://kursbuch.bahn.de/hafas-res/img/kbview/karten/vk-5-10.jpg
```

## Bilder schneiden

```
magick data/vk-0-0.jpg -crop 522x373+0x0 images/t-0-0.jpg
...
magick data/vk-5-0.jpg -crop 650x373+0x0 images/t-5-0.jpg
...
magick data/vk-0-10.jpg -crop 522x550+0x0 images/t-0-10.jpg
...
magick data/vk-5-10.jpg -crop 650x550+0x0 images/t-5-10.jpg
```

## Bilder zusammenfügen

Zeilen:

```
magick images/t-0-0.jpg images/t-1-0.jpg images/t-2-0.jpg images/t-3-0.jpg images/t-4-0.jpg images/t-5-0.jpg +append images/t-0.jpg
...
magick images/t-0-10.jpg images/t-1-10.jpg images/t-2-10.jpg images/t-3-10.jpg images/t-4-10.jpg images/t-5-10.jpg +append images/t-10.jpg
```

Gesamtes Bild:

```
magick images/t-0.jpg images/t-1.jpg images/t-2.jpg images/t-3.jpg images/t-4.jpg images/t-5.jpg images/t-6.jpg images/t-7.jpg images/t-8.jpg images/t-9.jpg images/t-10.jpg -append data/vk.jpg
```

# Kartenklien erstellen

Siehe [European Inland Waterways as a Slippy Map](https://github.com/fossgis2019/European-Inland-Waterways) für eine Anleitung.



