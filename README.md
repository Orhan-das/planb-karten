# planb-karten

Offline-Karten, Routen und Ortssuche für die iPhone-App **BlackOut PlanB**, die Vorsorge-App für Stromausfall und Krisen. Die Dateien werden einmal geladen, solange es Internet gibt. Danach laufen Karte, Suche und Routen auf dem Gerät, ohne Netz.

*English summary below.*

## Was hier liegt

Die Dateien stehen nicht im Repository selbst, sondern in den [Veröffentlichungen (Releases)](../../releases). Die neueste Kartenliste steht unter `releases/latest/download/katalog.json`.

Je Region gibt es drei Dateien:

| Datei | Inhalt | Format |
|---|---|---|
| `<id>-karte.pmtiles` | Kartendarstellung (Vektorkacheln) | [PMTiles](https://github.com/protomaps/PMTiles) |
| `<id>-routen.tar` | Routendaten für Fuß, Rad, Auto | Tar-Archiv mit [Valhalla](https://github.com/valhalla/valhalla)-Kacheln (`.gph`) |
| `<id>-orte.sqlite` | Suche nach Orten, Straßen, Hausnummern und Notfall-Orten (Krankenhaus, Apotheke, Trinkwasser, Polizei, Feuerwehr, Tankstelle) | SQLite |

Dateien über 2 GB sind in Teile zerlegt. Die Teile werden nacheinander zusammengesetzt.

## Kartenliste `katalog.json`

```json
{
  "stand": "2026-11-12",
  "basis": "https://github.com/Orhan-das/planb-karten/releases/download/<tag>",
  "regionen": [
    {
      "id": "at", "name": "Österreich", "gruppe": "Europa",
      "bbox": [9.53, 46.37, 17.16, 49.02],
      "stand": "2026-11-11", "bau": "20261112-1141",
      "karte": "at-karte.pmtiles", "karteBytes": 1043455531,
      "routen": "at-routen.tar", "routenBytes": 1222410240,
      "orte": "at-orte.sqlite", "orteBytes": 72642560,
      "basis": "https://github.com/Orhan-das/planb-karten/releases/download/<tag>",
      "pruefsummen": { "karte": "<sha256>", "routen": "<sha256>", "orte": "<sha256>" }
    }
  ]
}
```

| Feld | Bedeutung |
|---|---|
| `gruppe` | Kontinent, oder ein Landesname, wenn ein Land in Regionen geteilt ist (z. B. „Deutschland“) |
| `bbox` | West, Süd, Ost, Nord |
| `umriss` | vereinfachter Umriss der Region |
| `stand` | Datenstand von OpenStreetMap |
| `bau` | Kennung des Routen-Durchlaufs. Nur Regionen mit gleicher Kennung passen an den Grenzen zusammen. |
| `karteTeile`, `routenTeile` | Liste der Teile, falls eine Datei zerlegt ist |
| `basis` | Adresse der Dateien, falls sie in einer anderen Veröffentlichung liegen als die Kartenliste |
| `pruefsummen` | SHA-256 (hex) der vollständigen Datei je Teil. Bei zerlegten Dateien gilt die Summe der zusammengesetzten Datei. |

Ältere Veröffentlichungen bleiben bestehen, weil die Kartenliste auf sie verweisen kann.

## Lizenz und Namensnennung

Alle Kartendaten stammen von **OpenStreetMap**: © OpenStreetMap-Mitwirkende, verfügbar unter der [Open Database License (ODbL) 1.0](https://opendatacommons.org/licenses/odbl/1-0/). Die Dateien hier sind daraus abgeleitet und stehen ebenfalls unter der ODbL; siehe [LICENSE.md](LICENSE.md).

Wer die Dateien nutzt, nennt „© OpenStreetMap-Mitwirkende“ gut sichtbar ([Richtlinie der OSMF](https://osmfoundation.org/wiki/Licence/Attribution_Guidelines)).

## Ohne Gewähr

Die Daten können fehlerhaft, unvollständig oder veraltet sein. Routen kennen keine Sperren, Baustellen oder Verkehrslage. Vor Ort gelten Beschilderung, Behörden und eigene Einschätzung. Für Notrufe immer die Notrufnummer des Landes wählen.

---

## English summary

Offline maps, routing and place search for the iPhone app **BlackOut PlanB**. Files are in the [Releases](../../releases); the current catalogue is `releases/latest/download/katalog.json`. Each region has a map (`PMTiles`), routing tiles (`tar` of Valhalla `.gph` tiles) and a search database (`SQLite`). `pruefsummen` holds the SHA-256 of each complete file.

Map data © OpenStreetMap contributors, available under the [ODbL 1.0](https://opendatacommons.org/licenses/odbl/1-0/); the files here are derived databases under the same licence. No warranty: data may be wrong or outdated, routes ignore closures and traffic. In an emergency, call the local emergency number.
