# Demo OCR-D @ DHd 2022

## Demo 1 - Download einer METS und inspizieren des OCR-D Workspace

* Werk: https://digital.staatsbibliothek-berlin.de/werkansicht?PPN=PPN680203753
* METS: https://content.staatsbibliothek-berlin.de/dc/PPN680203753.mets.xml

Wir laden ("klonen") das METS-XML für das Werk

```sh
ocrd workspace clone -d loewenthal1896 https://content.staatsbibliothek-berlin.de/dc/PPN680203753.mets.xml
```

Wechseln wir in das Verzeichnis und listen alle im METS verzeichneten Dateien:

```sh
cd loewenthal1896
ocrd workspace find -k fileGrp -k mimetype -k ID -k url

FULLTEXT	text/xml	https://content.staatsbibliothek-berlin.de/dc/PPN680203753-00000001.ocr.xml	FILE_0001_FULLTEXT
FULLTEXT	text/xml	https://content.staatsbibliothek-berlin.de/dc/PPN680203753-00000002.ocr.xml	FILE_0002_FULLTEXT
FULLTEXT	text/xml	https://content.staatsbibliothek-berlin.de/dc/PPN680203753-00000003.ocr.xml	FILE_0003_FULLTEXT
[...]
```

Die `PRESENTATION` Dateigruppe enthält Referenzen, mit denen `browse-ocrd` nicht zurecht kommt, daher entfernen wir diese Referenzen:

```sh
ocrd workspace remove-group -kr PRESENTATION
```

Die hochauflösendsten Bilder, die in der METS referenziert sind, sind in der
`DEFAULT` Dateigruppe. Um mit der bestehenden OCR zu vergleichen, laden wir
auch die `FULLTEXT` Dateigruppe herunter:

```sh
ocrd -l DEBUG workspace find --file-grp DEFAULT --download
ocrd -l DEBUG workspace find --file-grp FULLTEXT --download
```

(Mit der `-l/--log-level DEBUG`-Option schalten wir detailliertes Logging ein, um den Fortschritt des Downloads beobachten zu können)

Dann können wir uns diesen Workspace mit browse-ocrd ansehen

```sh
browse-ocrd mets.xml
```

![](screenshots/browse-ocrd-01.png)

## Demo 2 - Binarisierung, Segmentierung, Erkennung mit Calamari

Für die Binarisierung verwenden wir den `ocrd-cis-ocropy-binarize` Prozessor:

```sh
ocrd-ci-ocropy-binarize -I DEFAULT -O OCR-D-BIN
```

Anschließend nutzen wir kraken für die Segmentierung:

```sh
```

## Tools

* [OCR-D/core](https://github.com/OCR-D/core)
* [OCR-D/ocrd\_calamari](https://github.com/OCR-D/ocrd_calamari)
* [OCR-D/ocrd\_tesserocr](https://github.com/OCR-D/ocrd_tesserocr)
* [OCR-D/ocrd\_fileformat](https://github.com/OCR-D/ocrd_fileformat)
* [cisocrgroup/ocrd\_cis](https://github.com/OCR-D/ocrd_calamari)
* [browse-ocrd](https://github.com/hnesk/browse-ocrd)

