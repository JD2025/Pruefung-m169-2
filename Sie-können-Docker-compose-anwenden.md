# Sie können Docker compose anwenden.

---

## Container starten

```bash
docker compose up
```

Startet alle Services aus der `docker-compose.yml`

---

### Im Hintergrund starten (empfohlen)

```bash
docker compose up -d
```

`-d` = detached (läuft im Hintergrund)

---

## Container stoppen & löschen

```bash
docker compose down
```

Stoppt und entfernt:
- Container
- Netzwerke

---

## Container neu starten

```bash
docker compose restart
```

---

## Status anzeigen

```bash
docker compose ps
```

Zeigt laufende Container

---

## Logs anzeigen

```bash
docker compose logs
```

Alle Logs anzeigen

```bash
docker compose logs -f
```

Live Logs (wie „tail“)

---

## Einzelnen Service starten

```bash
docker compose up web
```

Startet nur den Service `web`

---

## Container stoppen (ohne löschen)

```bash
docker compose stop
```

---

## ▶Gestoppte Container wieder starten

```bash
docker compose start
```

---

## Alles löschen (inkl. Volumes)

```bash
docker compose down -v
```

Entfernt auch Daten (Vorsicht!)

---

## Image neu bauen

```bash
docker compose build
```

---

### Neu bauen + starten

```bash
docker compose up --build
```

---

## Andere Compose-Datei verwenden

```bash
docker compose -f andere-datei.yml up
```

---

## Merksatz

docker compose =  
**Container starten, stoppen und verwalten mit einem Befehl**

---

## Kurz-Zusammenfassung

- `up` → starten  
- `down` → stoppen & löschen  
- `ps` → Status  
- `logs` → Logs  
- `build` → Image bauen  

---