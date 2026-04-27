# Sie verstehen wie in Docker compose mit Passwörtern oder sonstigen geheimen Informationen umgegangen wird.

---

## Ziel

Verstehen, wie man Passwörter und sensible Daten sicher in Docker Compose verwendet.

---

## Unsichere Methode

```yaml
services:
  db:
    image: postgres
    environment:
      POSTGRES_PASSWORD: meinpasswort
```

### Problem

- Passwort steht im Klartext  
- Jeder mit Zugriff auf die Datei kann es sehen  
- Unsicher für reale Anwendungen  

---

## Methode 1: .env Datei

### .env Datei

```env
POSTGRES_PASSWORD=geheim
```

---

### docker-compose.yml

```yaml
services:
  db:
    image: postgres
    environment:
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
```

---

### Vorteile

- Passwort nicht direkt in YAML  
- einfacher zu verwalten  
- besser für Entwicklung  

---

### Nachteile

- immer noch im Klartext gespeichert  
- nicht sicher für Produktion  

---

## Methode 2: Docker Secrets

### Secret erstellen

```bash
echo "geheim" | docker secret create db_password -
```

---

### docker-compose.yml

```yaml
services:
  db:
    image: postgres
    secrets:
      - db_password

secrets:
  db_password:
    external: true
```

---

### Zugriff im Container

Das Passwort wird als Datei bereitgestellt:

```bash
/run/secrets/db_password
```

---

### Vorteile

- kein Klartext in Dateien  
- sicher gespeichert  
- nur Container hat Zugriff  

---

## Unterschied

| Methode   | Sicherheit | Einsatz        |
|-----------|------------|----------------|
| Klartext  | niedrig    | vermeiden      |
| .env      | mittel     | Entwicklung    |
| Secrets   | hoch       | Produktion     |

---

## Wichtige Regeln

- keine Passwörter direkt im YAML speichern  
- .env nicht ins Repository hochladen  
- Secrets für produktive Systeme verwenden  

---

## Fazit

- einfache Projekte nutzen .env  
- produktive Systeme nutzen Docker Secrets  
- Sicherheit ist ein wichtiger Teil von Docker Compose  