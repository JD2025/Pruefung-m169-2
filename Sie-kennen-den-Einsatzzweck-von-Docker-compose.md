# Sie kennen den Einsatzzweck von Docker Compse

## docker-compose.yml

```yaml
version: "3.9"

services:
  mariadb:
    image: mariadb
    container_name: mariadb-test
    environment:
      MYSQL_RANDOM_ROOT_PASSWORD: 1
      MYSQL_DATABASE: wp
      MYSQL_USER: wpuser
      MYSQL_PASSWORD: geheim
    volumes:
      - myvolume:/var/lib/mysql
    networks:
      - testnet

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: pma
    ports:
      - "8080:80"
    environment:
      PMA_HOST: mariadb
    networks:
      - testnet

  wordpress:
    image: wordpress
    container_name: wordpress
    hostname: wordpress-titel
    ports:
      - "8081:80"
    environment:
      WORDPRESS_DB_HOST: mariadb
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_NAME: wp
      WORDPRESS_DB_PASSWORD: geheim
    volumes:
      - wp-html:/var/www/html/wp-content
    networks:
      - testnet

volumes:
  myvolume:
  wp-html:

networks:
  testnet:
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
