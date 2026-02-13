# Déployer une application 2048 avec Docker — Exo 1

## 1. Installer Docker

```bash
# Télécharge et exécute le script d'installation officiel de Docker
curl -fsSL https://get.docker.com | sh
```

---

## 2. Récupérer le code source

```bash
# Clone le repo du jeu 2048 depuis GitHub
git clone https://github.com/ttwthomas/2048.git

# Se placer dans le répertoire du projet
cd 2048/
```

---

## 3. Créer le Dockerfile

```bash
# Créer le fichier Dockerfile à la racine du projet
vim Dockerfile
```

Contenu du `Dockerfile` :

```dockerfile
# Utilise l'image officielle Nginx (version stable, basée sur Alpine pour un poids minimal)
FROM nginx:stable-alpine3.20

# Copie le contenu du dossier "app" dans le répertoire par défaut de Nginx
COPY app /usr/share/nginx/html
```

> **Qu'est-ce qu'un Dockerfile ?**
> C'est une recette qui décrit étape par étape comment construire une image Docker.
> Ici on part d'une image Nginx existante et on y ajoute nos fichiers statiques.

---

## 4. Construire l'image Docker (build)

```bash
# Construit une image Docker à partir du Dockerfile
# -t : donne un nom (tag) à l'image pour la retrouver facilement
docker build -t mon-app-2048 .
```

> Le `.` à la fin indique le contexte de build (le répertoire courant).
> Docker lit le `Dockerfile`, exécute chaque instruction et produit une **image**.

---

## 5. Lancer un conteneur (run)

```bash
# Démarre un conteneur à partir de l'image créée
# -p 30080:80 : redirige le port 30080 de l'hôte vers le port 80 du conteneur (Nginx)
docker run -p 30080:80 mon-app-2048
```

> Le jeu 2048 est maintenant accessible sur `http://<IP_DU_SERVEUR>:30080`

---

## 6. Gérer les images Docker

### Lister les images présentes sur la machine

```bash
docker images
```
