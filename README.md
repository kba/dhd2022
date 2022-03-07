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
```



## Tools

* [OCR-D/core](https://github.com/OCR-D/core)
* [browse-ocrd](https://github.com/hnesk/browse-ocrd)
