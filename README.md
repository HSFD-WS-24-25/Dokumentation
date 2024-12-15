# Dokumentation
Alles, was nicht direkt die Code-Funktionalität beschreibt.

## Lokales Setup

### Repositories klonen
Zunächst sowohl das Frontend- als auch das Backend-Repository klonen.

### Konfiguration der `.env`-Dateien
Anhand der bereitgestellten `.env.example`-Dateien die `.env`-Dateien anlegen. Alternativ können fertige `.env`-Dateien direkt genutzt werden.

### PostgreSQL-Datenbank anlegen
Es muss eine PostgreSQL-Datenbank eingerichtet werden. Dies kann entweder manuell erfolgen oder mithilfe von Docker. [Offizielle PostgreSQL-Installation](https://www.postgresql.org/download/) und [Docker-Image](https://hub.docker.com/_/postgres) stehen zur Verfügung.

#### Beispiel: Docker verwenden
Mit folgendem Befehl wird eine PostgreSQL-Datenbank über Docker eingerichtet:

```bash
sudo docker run --name postgres -p 5432:5432 -h 127.0.0.1 -e POSTGRES_USER=root -e POSTGRES_PASSWORD=secret_password -d postgres:latest
```

Die Datenbank wird mit dem Benutzer _root_ und dem Passwort _secret_password_ auf Port 5432 gestartet.

Die Verbindungsdaten müssen in der `.env`-Datei des Backends eingetragen werden:

```bash
DATABASE_URL='postgresql://root:secret_password@127.0.0.1:5432/postgres'
```

### Abhängigkeiten installieren
Sobald alle Vorbereitungen abgeschlossen sind, in beiden Repositories `npm install` ausführen.

### Datenbank initialisieren
Die Datenbank kann vom Backend aus mit folgendem Befehl initialisiert werden:

```bash
npx prisma migrate dev
```

### Optional: Datenbank befüllen
Um die Anwendung sinnvoll testen zu können, kann die Datenbank mit Beispieldaten befüllt werden. Hierzu bitte `npm run role` und `npm run seed` ausführen.

### Anwendung starten
Jetzt ist alles bereit. Die Anwendungen können mit folgendem Befehl gestartet werden:

```bash
npm run dev
```

Die Nutzer sind jetzt angelegt, der eigene Nutzer wird in der Datenbank ebenfalls angelegt und kann dann Anfragen ans Backend stellen. Da andere Nutzer bereits existieren, werden wir zunächst als _guest_ angelegt.
Mittels `npx prisma studio` lässt sich die Weboberfläche von Prisma öffnen, die eigene role_id kann dann auf den gewünschten Wert (hier 1 für Admin) gesetzt werden.