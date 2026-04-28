# Sie können eigene Dockerfiles erstellen, testen und dokumentieren.¨

---

## Projektübersicht

```text
uebung2/
├── pw
  ├── pw.txt
├── Dockerfile
├── package.json
├── server.js
├── docker-compse.yml
```

---

# 1. Dockerfile

## Zweck
Beschreibt, wie ein Docker Image gebaut wird.

## Beispiel Dockerfile

```Dockerfile
FROM node:18
 
WORKDIR /app
 
COPY server.js /app/
COPY package.json /app/
 
RUN npm install
 
CMD ["node", "server.js"]
 
EXPOSE 3000
```

## Erklärung

- FROM node:20-alpine  
  Wählt ein kleines, effizientes Node.js Image  

- WORKDIR /app  
  Setzt den Arbeitsordner im Container  

- COPY package*.json ./  
  Kopiert nur die Paketdateien (für schnelleres Build)  

- RUN npm install  
  Installiert Abhängigkeiten  

- COPY . .  
  Kopiert den restlichen Code  

- EXPOSE 3000  
  Dokumentiert den Port  

- CMD ["node", "server.js"]  
  Startet die Anwendung  

## Braucht man es immer?
Nein  
Nur wenn ein eigenes Image erstellt wird

---

# 2. package.json

## Zweck
Definiert die Node.js Anwendung und ihre Abhängigkeiten.

## Beispiel

```json
{
  "name": "docker-node-app",
  "version": "1.0.0",
  "description": "Simple Node.js Docker App",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "author": "",
  "license": "ISC"
}
```

## Erklärung

- name → Name des Projekts  
- version → Version  
- dependencies → benötigte Pakete  

## Braucht man es immer?
Nein  
Nur bei Node.js Projekten

---

# 3. server.js

## Zweck
Die eigentliche Anwendung, die im Container läuft.

## Beispiel

```javascript
const http = require("http");
 
http.createServer((req, res) => {
  res.write("Hello Docker!");
  res.end();
}).listen(3000);
```

## Erklärung

- erstellt Webserver  
- reagiert auf Anfragen  
- läuft auf Port 3000  

## Braucht man es immer?
Nein  
Aber du brauchst immer irgendeine Anwendung

---

# 4. .dockerignore

## Zweck
Schliesst unnötige Dateien vom Build aus.

## Beispiel

```text
node_modules
.git
Dockerfile
```

## Erklärung

- verhindert grosse Images  
- beschleunigt Build  

## Braucht man es immer?
Nein  
Aber empfohlen

---

# 5. README.md

## Zweck
Dokumentation für Benutzer.

## Beispiel

```markdown
# Docker App

## Starten
docker build -t app .
docker run -p 3000:3000 app
```

## Braucht man es immer?
Nein  
Aber wichtig für Projekte

---

# Anwendung

## Image bauen

```bash
docker build -t meine-app .
```

## Container starten

```bash
docker run -p 3000:3000 meine-app
```

---

# Ergebnis

Browser öffnen:

http://localhost:3000

Ausgabe:
Docker Webserver läuft

---

# Wichtige Erkenntnisse

- Dockerfile baut das Image  
- Code wird in Container kopiert  
- CMD startet die Anwendung  
- Port muss gemappt werden  

---

# Übersicht

| Datei          | Zweck                | Pflicht |
|---------------|---------------------|--------|
| Dockerfile    | Image erstellen     | Ja     |
| package.json  | Abhängigkeiten      | Nein   |
| server.js     | Anwendung           | Nein   |
| .dockerignore | Build optimieren    | Nein   |
| README.md     | Dokumentation       | Nein   |

---

# Fazit

- Dockerfile ist das zentrale Element  
- Andere Dateien hängen vom Projekt ab  
- Das Beispiel zeigt einen vollständigen, lauffähigen Container  

---

# Prüfungs-Tipp

Wenn du:
- ein Dockerfile erklären kannst  
- die Dateien verstehst  
- das Projekt starten kannst  

Dann erfüllst du das Lernziel vollständig
