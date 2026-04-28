# Sie kennen den Einsatzzweck von Docker Compse

## docker-compose.yml

```yaml
services:
  web:
    build: .
    container_name: WebS
    ports:
      - 3000:3000
    depends_on:
      - db
  db:
    image: mysql
    container_name: DatenB
    ports:
      - 3306:3306
    environment:
      MYSQL_ROOT_PASSWORD_FILE: /run/secrets/dbpw
      MYSQL_DATABASE: webDB
    secrets:
      - dbpw
secrets:
  dbpw:
    file: ./pw/pw.txt
```

---

## Anwendung

```bash
docker compose up -d
```

Startet:
- MariaDB (Datenbank)
- phpMyAdmin (localhost:8080)
- Wordpress (localhost:8081)

---

## 🔍 Was wurde ersetzt?

| docker run | docker-compose |
|----------|----------------|
| -d | automatisch |
| --name | container_name |
| -p | ports |
| -e | environment |
| -v | volumes |
| --network | networks |

---

## Vorteil

Statt 3 langen Befehlen:
```bash
docker run ...
docker run ...
docker run ...
```

nur noch:
```bash
docker compose up -d
```

---

## Verbesserung (Best Practice)

Passwort besser in `.env` auslagern:

```env
MYSQL_PASSWORD=geheim
```

```yaml
environment:
  MYSQL_PASSWORD: ${MYSQL_PASSWORD}
```

---
