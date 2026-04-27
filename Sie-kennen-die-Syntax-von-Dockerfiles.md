# Sie kennen die Syntax von Dockerfiles.

---

### Wichtige Befehle

| Befehl       | Bedeutung |
|-------------|----------|
| FROM        | Basis-Image |
| WORKDIR     | Arbeitsverzeichnis |
| COPY        | Dateien kopieren |
| ADD         | Kopieren + URL/Archive |
| RUN         | Befehle beim Build |
| CMD         | Startbefehl |
| ENTRYPOINT  | Fixer Startbefehl |
| ENV         | Umgebungsvariablen |
| EXPOSE      | Port dokumentieren |
| LABEL       | Metadaten |
| USER        | Benutzer |
| VOLUME      | Volume definieren |

---

### Grundstrucktur

```Dockerfile
FROM <image>
WORKDIR <verzeichnis>
COPY <quelle> <ziel>
RUN <befehl>
EXPOSE <port>
CMD ["startbefehl"]
```

---

### Wichtige Unterschiede

#### COPY vs ADD
- COPY → einfaches Kopieren (empfohlen)
- ADD → kann auch URLs laden und Archive entpacken

👉 Best Practice: **immer COPY verwenden, wenn möglich**

---

#### CMD vs ENTRYPOINT
- CMD → kann überschrieben werden
- ENTRYPOINT → wird immer ausgeführt

---