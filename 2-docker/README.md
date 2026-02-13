# Cours Docker — Mémo

## Créer une image Docker

Créer un fichier `Dockerfile` :

```dockerfile
FROM ubuntu:24.04
RUN apt-get update
RUN apt-get install -y nginx
CMD ["nginx", "-g", "daemon off;"]
```

Builder (construire) et lancer l'image :

```bash
docker build -t mon-image .
docker run -p 8080:80 mon-image
```

---

## Réseau

Les conteneurs ont leur propre carte réseau (virtuelle).
Pour exposer un port du conteneur sur l'hôte :

```bash
docker run -p 8080:80 mon-image
```

`-p` permet de mapper le port **8080** de l'hôte sur le port **80** du conteneur.

---

## Volumes

Permet de stocker des données en dehors du conteneur (persistance).

```bash
docker run -v ./data:/var/lib/mysql mysql
```

`-v` permet de mapper le dossier `./data` de l'hôte sur le dossier `/var/lib/mysql` du conteneur.

---

## Commandes de base

```bash
# Liste des conteneurs en cours d'exécution
docker ps
docker container ls

# Liste des images
docker images

# Stopper et supprimer un conteneur
docker stop <container_id>
docker rm <container_id>
```

---

## Commandes utiles

```bash
# Rentrer dans un conteneur
docker exec -it <container_id> bash

# Voir les logs d'un conteneur
docker logs <container_id>

# Lancer un conteneur en arrière plan
docker run -d mon-image

# Arrêter et supprimer un conteneur
docker stop abc123 && docker rm abc123

# Arrêter tous les conteneurs d'un fichier docker-compose.yml
docker-compose down
```

---

## Docker Compose

Permet de définir et gérer des applications multi-conteneurs.

Fichier `docker-compose.yml` :

```yaml
services:
  redis:
    image: "redis:latest"
  web:
    build: .
    ports:
      - "5000:5000"
```

```bash
docker compose up
```

Équivalent à :

```bash
docker run redis:latest
docker build -t mon-image .
docker run -p 5000:5000 mon-image
```