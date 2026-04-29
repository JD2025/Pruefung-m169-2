# Dockerfiles nachvollziehen.

## Beispiel: Produktionsnahes Dockerfile

```Dockerfile
FROM node:18-alpine

# Metadaten
LABEL maintainer="dev@example.com"

# Arbeitsverzeichnis setzen
WORKDIR /app

# Nur package Dateien kopieren (Caching)
COPY package*.json ./

# Abhängigkeiten installieren
RUN npm install --production

# Benutzer erstellen (Sicherheit)
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# Restlichen Code kopieren
COPY . .

# Rechte setzen
RUN chown -R appuser:appgroup /app

# Benutzer wechseln
USER appuser

# Umgebung setzen
ENV NODE_ENV=production

# Port dokumentieren
EXPOSE 3000

# Startbefehl
CMD ["node", "server.js"]
```

---

## Schritt-für-Schritt Erklärung

### 1. FROM node:18-alpine
Kleines, schnelles Basis-Image  
Spart Speicher und ist sicherer  

---

### 2. LABEL
Metadaten über das Image  
z. B. Entwickler, Version  

---

### 3. WORKDIR /app
Arbeitsordner wird gesetzt  
Alle folgenden Befehle laufen hier  

---

### 4. COPY package*.json ./
Kopiert nur package.json + package-lock.json  
Vorteil: Docker kann Cache nutzen  

---

### 5. RUN npm install --production
Installiert nur notwendige Pakete  
Keine Dev-Dependencies → kleineres Image  

---

### 6. Benutzer erstellen

```Dockerfile
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
```

Sicherheit:
- Container läuft nicht als root  
- reduziert Risiko  

---

### 7. COPY . .
Kopiert gesamten Code ins Image  

---

### 8. Rechte setzen

```Dockerfile
RUN chown -R appuser:appgroup /app
```

Damit der neue Benutzer Zugriff hat  

---

### 9. USER appuser
Container läuft jetzt als normaler User  
Best Practice für Sicherheit  

---

### 10. ENV NODE_ENV=production
Setzt Umgebung  
beeinflusst Verhalten der App  

---

### 11. EXPOSE 3000
Dokumentiert den Port  

---

### 12. CMD ["node", "server.js"]
Startet die Anwendung  

---

## Gesamtablauf

1. Basis-Image laden  
2. Arbeitsumgebung vorbereiten  
3. Abhängigkeiten installieren  
4. Benutzer einrichten  
5. Code kopieren  
6. Sicherheit setzen  
7. App starten  

---

## Wichtige Konzepte (prüfungsrelevant)

### 🔹 Caching
- `package.json` zuerst kopieren  
- schnellerer Build  

---

### 🔹 Sicherheit
- kein root Benutzer  
- eingeschränkte Rechte  

---

### 🔹 Image-Größe
- alpine verwenden  
- nur production dependencies  

---

### 🔹 Layer-Prinzip
- jede RUN/COPY = neue Layer  
- kombinieren spart Platz  

---

## Typische Prüfungsfragen

- Warum nicht als root laufen?  
Sicherheitsrisiko  

- Warum alpine nutzen?  
kleiner und schneller  

- Warum COPY getrennt?  
besseres Caching  

- Unterschied RUN vs CMD?  
RUN = Build  
CMD = Start  

---

## Fazit

Ein komplexes Dockerfile nachvollziehen bedeutet:
- jede Zeile technisch verstehen  
- Best Practices erkennen  
- Ablauf erklären können  

Wenn du DAS kannst → bist du auf Prüfungsniveau 
