# Aufbau/erstellen einer YAML-Datei.
Eine YAML-Datei ist eine Datei, die Dinge **strukturiert beschreibt**  
(z. B. für Docker Compose).

Denk daran wie:
**Ein Baum mit Einrückungen**

---

## Grundprinzip

### 1. Schlüssel und Wert

```yaml
name: Max
```

links = Schlüssel  
rechts = Wert  

---

### 2. Einrückung = gehört zusammen

```yaml
person:
  name: Max
  alter: 25
```

`name` und `alter` gehören zu `person`  
weil sie eingerückt sind  

---

### 3. Liste mit `-`

```yaml
hobbys:
  - Fussball
  - Gaming
  - Musik
```

`-` = Liste  

---

## Beispiel (Docker Compose)

```yaml
services:
  web:
    image: nginx
    ports:
      - "80:80"
```

---

## Erklärung

- `services` → Hauptbereich  
- `web` → Container  
- `image` → welches Image  
- `ports` → Liste von Ports  

---

## Wichtigste Regeln

- Einrückung mit **Leerzeichen (kein Tab!)**  
- `:` trennt Schlüssel und Wert  
- `-` steht für Listen  
- Struktur kommt durch Einrückung  

---

## Merksatz

👉 YAML =  
**Einrückung + `:` + `-`**

---

## Kurz-Zusammenfassung

- YAML ist einfach aufgebaut  
- Struktur durch Einrückung  
- Wird bei Docker Compose verwendet  
