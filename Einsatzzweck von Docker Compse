# Einsatzzweck von Docker Compse

https://awesome-docker-compose.com/wordpress

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
```yml
services:
 
  mariadb-test:
    image: mariadb
    container_name: mariadb-test
    networks:
      - testnet
    environment:
      MYSQL_RANDOM_ROOT_PASSWORD: "1"
      MYSQL_DATABASE: wp
      MYSQL_USER: wpuser
      MYSQL_PASSWORD_FILE: /run/secrets/db_password
    secrets:
      - db_password
    volumes:
      - myvolume:/var/lib/mysql
 
  pma:
    image: phpmyadmin
    container_name: pma
    networks:
      - testnet
    ports:
      - "8081:80"
    environment:
      PMA_HOST: mariadb-test
    depends_on:
      - mariadb-test
 
  wordpress:
    image: wordpress
    container_name: wordpress
    networks:
      - testnet
    ports:
      - "8082:80"
    volumes:
      - wp-html:/var/www/html/wp-content
    environment:
      WORDPRESS_DB_HOST: mariadb-test
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_NAME: wp
      WORDPRESS_DB_PASSWORD_FILE: /run/secrets/db_password
    secrets:
      - db_password
    depends_on:
      - mariadb-test

 
networks:
  testnet:
    external: true
 
volumes:
  myvolume:
  wp-html:
 
secrets:
  db_password:
    file: ./PWs/pw.txt
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
