# intelligence-engineering-5

# Image Classification

Dieses Projekt beschäftigt sich mit der Klassifikation von Bildern mithilfe von Machine Learning. Zur gemeinsamen Entwicklung verwenden wir Git, Python, Jupyter Notebook und Data Version Control (DVC).

Die Trainingsdaten werden zentral in Google Cloud Storage gespeichert und über DVC versioniert.

## 1. Voraussetzungen

Folgende Software muss installiert sein:

- Python
- pip
- Git
- Google Cloud CLI

Die Google Cloud CLI kann unter folgendem Link heruntergeladen werden:

https://cloud.google.com/sdk/docs/install

## 2. Repository klonen

```bash
git clone <repository-url>
cd <repository-name>
```

## 3. Virtuelle Python-Umgebung einrichten

Eine virtuelle Umgebung verhindert Konflikte mit anderen lokal installierten Python-Bibliotheken.

```bash
python -m venv .venv
```

### macOS / Linux

```bash
source .venv/bin/activate
```

### Windows (PowerShell)

```powershell
.venv\Scripts\Activate.ps1
```

## 4. Abhängigkeiten installieren

Alle benötigten Python-Bibliotheken werden über die `requirements.txt` installiert.

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Die Installation kann aufgrund der umfangreichen Machine-Learning-Abhängigkeiten einige Minuten dauern.

Optional können die installierten Abhängigkeiten auf Konflikte überprüft werden:

```bash
pip check
```

## 5. Google Cloud authentifizieren

Der Datensatz befindet sich in einem privaten Google Cloud Storage Bucket.

Vor dem erstmaligen Download muss eine Authentifizierung mit dem freigeschalteten Google-Account erfolgen:

```bash
gcloud auth application-default login
```

Im Browser muss der Google-Account ausgewählt werden, für den die Zugriffsberechtigung erteilt wurde.

Es ist nicht notwendig, ein eigenes Google-Cloud-Projekt oder einen eigenen Bucket zu erstellen.

## 6. Datensatz herunterladen

Der Datensatz wird nicht direkt im Git-Repository gespeichert, sondern über DVC verwaltet.

```bash
dvc pull
```

DVC lädt automatisch die zum aktuellen Git-Stand passende Datenversion herunter und stellt die ursprüngliche Ordnerstruktur wieder her.

## 7. Jupyter Notebook starten

```bash
jupyter notebook
```

Anschließend können die Notebooks im Browser geöffnet und ausgeführt werden.

## 8. Änderungen beziehen

Um den aktuellen Stand des Projekts einschließlich der zugehörigen Datenversion herunterzuladen:

```bash
git pull
dvc pull
```

Falls sich die Python-Abhängigkeiten geändert haben:

```bash
pip install -r requirements.txt
```

## 9. Datensatz aktualisieren

Falls Änderungen am Datensatz vorgenommen werden, müssen diese zunächst mit DVC erfasst werden:

```bash
dvc add data/raw/
dvc push
```

Anschließend werden die aktualisierten DVC-Metadaten mit Git versioniert:

```bash
git add data/raw.dvc data/.gitignore
git commit -m "Update dataset"
git push
```

Änderungen am Originaldatensatz sollten vorher innerhalb der Gruppe abgestimmt werden.

## 10. Versionierung

| Bestandteil | Versionierung |
|---|---|
| Python-Code | Git |
| Jupyter Notebooks | Git |
| Requirements | Git |
| DVC-Konfiguration | Git |
| `.dvc`-Metadatendateien | Git |
| Bilddatensatz | DVC |
| Große trainierte Modelle | DVC, sofern eingerichtet |
| Virtuelle Umgebung | Keine |
| Zugangsdaten und API-Keys | Keine |

Zugangsdaten, API-Keys und private Konfigurationsdateien dürfen nicht in das Git-Repository eingecheckt werden.

## 11. Wichtige Befehle

| Befehl | Beschreibung |
|---|---|
| `git pull` | Aktuellen Quellcode herunterladen |
| `git push` | Git-Commits hochladen |
| `dvc pull` | Daten herunterladen |
| `dvc push` | Daten hochladen |
| `dvc status` | Änderungen an versionierten Daten überprüfen |
| `dvc add` | Dateien oder Verzeichnisse versionieren |
| `pip install -r requirements.txt` | Abhängigkeiten installieren |
| `jupyter notebook` | Jupyter starten |

## 12. Troubleshooting

### Zugriff auf den Datensatz verweigert (403)

Überprüfen, ob der richtige Google-Account verwendet wird und die erforderlichen Bucket-Berechtigungen vorhanden sind.

Gegebenenfalls erneut authentifizieren:

```bash
gcloud auth application-default login
```

### DVC unterstützt Google Cloud Storage nicht

```bash
pip install "dvc[gs]"
```

### Fehlende Python-Bibliotheken

Überprüfen, ob die virtuelle Umgebung aktiviert wurde, und die Abhängigkeiten erneut installieren:

```bash
pip install -r requirements.txt
```

### Fehlende Daten

```bash
dvc pull
```
