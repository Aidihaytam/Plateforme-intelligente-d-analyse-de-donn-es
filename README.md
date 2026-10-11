# Plateforme intelligente d'analyse de données

Plateforme web d'analyse économique, commerciale et marketing destinée à transformer des données brutes en indicateurs, analyses et recommandations exploitables.

## 1. État du projet

Le projet est en cours de développement.

### Technologies prévues

- **Backend :** PHP 8.5, Symfony 7.4 LTS, Doctrine ORM
- **Base de données :** PostgreSQL 17
- **Frontend prévu :** React, TypeScript, HTML et CSS
- **Service analytique prévu :** Python, Pandas, NumPy et bibliothèques adaptées
- **Environnement :** Docker, Docker Compose et WSL2
- **Gestion de versions :** Git et GitHub

### Fonctionnalités prévues

- Gestion des utilisateurs et authentification
- Création et gestion de projets d'analyse
- Import de fichiers CSV et Excel
- Profilage et contrôle de la qualité des données
- Nettoyage et analyse statistique
- Indicateurs économiques et marketing
- Modèles de machine learning lorsque cela est pertinent
- Simulations, analyse des risques et recommandations
- Assistant IA capable d'expliquer les résultats calculés

Les fonctionnalités sont développées progressivement. Consultez le code et l'historique Git pour connaître l'état réel de chaque module.

## 2. Prérequis

Avant de commencer, installez :

- Git
- Docker Desktop avec le moteur Linux et l'intégration WSL2 activés, ou un environnement Linux disposant de Docker Engine et du plugin Docker Compose
- Une distribution Ubuntu sous WSL2 si vous utilisez Windows
- PhpStorm, recommandé pour le développement

PHP, Composer et PostgreSQL sont exécutés dans des conteneurs Docker pour l'environnement de développement.

## 3. Récupérer le projet

Après la publication du dépôt sur GitHub, chaque membre de l'équipe devra exécuter les commandes suivantes dans son terminal [WSL] :

```bash
git clone <URL_DU_DEPOT_GITHUB>
cd plateforme-intelligente-analyse
```

Remplacez `<URL_DU_DEPOT_GITHUB>` par l'adresse réelle du dépôt.

## 4. Configurer les variables d'environnement

À la racine du projet, créez votre fichier `.env` local à partir du modèle fourni :

```bash
cp .env.example .env
```

Le fichier `.env` contient les paramètres locaux de la base de données. Il ne doit jamais être publié sur GitHub.

Adaptez les valeurs du fichier `.env` uniquement si nécessaire. Les identifiants fournis par défaut sont réservés au développement local.

## 5. Construire et lancer les conteneurs

Depuis la racine du projet, dans le terminal [WSL] :

```bash
docker compose config -q
docker compose build
docker compose up -d
```

Explication :

- `docker compose config -q` vérifie la syntaxe et la configuration de Compose.
- `docker compose build` construit l'image du backend à partir du Dockerfile.
- `docker compose up -d` démarre les services en arrière-plan.

Vérifiez ensuite l'état des conteneurs :

```bash
docker compose ps
```

Le service PostgreSQL utilise le port `5433` sur la machine hôte et le port `5432` à l'intérieur du réseau Docker.

Le backend est exposé sur le port `8000`.

## 6. Installer les dépendances Symfony

Après avoir démarré les services, exécutez à la racine du projet :

```bash
docker compose exec backend composer install
```

Cette commande installe les dépendances PHP déclarées dans `backend/composer.json` et verrouillées par `backend/composer.lock`.

Elle doit être exécutée après chaque récupération du projet lorsque les dépendances ne sont pas encore installées, ou lorsqu'elles ont été mises à jour.

## 7. Vérifier le backend

### Vérifier la version de Symfony

```bash
docker compose exec backend php bin/console --version
```

### Vérifier la configuration Symfony

```bash
docker compose exec backend php bin/console lint:container
```

### Vérifier la connexion à la base de données

```bash
docker compose exec backend php bin/console dbal:run-sql "SELECT current_database();"
```

La base attendue est `intelligent_analysis`.

### Accéder au backend

Lorsque le conteneur backend fonctionne, ouvrez :

http://localhost:8000

Cette adresse sert à vérifier le serveur HTTP. Toutes les routes et fonctionnalités de l'application ne sont pas encore développées.

## 8. Commandes Docker utiles

| Commande | Utilité |
|---|---|
| `docker compose ps` | Voir l'état des services |
| `docker compose logs -f backend` | Suivre les journaux du backend |
| `docker compose logs -f database` | Suivre les journaux de PostgreSQL |
| `docker compose exec backend sh` | Ouvrir un shell dans le conteneur backend |
| `docker compose exec backend php bin/console` | Afficher les commandes Symfony disponibles |
| `docker compose stop` | Arrêter les services sans supprimer les conteneurs |
| `docker compose up -d` | Démarrer les services |
| `docker compose down` | Arrêter et supprimer les conteneurs du projet |

**Attention :** ne lancez pas `docker compose down -v` sans accord de l'équipe. L'option `-v` peut supprimer le volume de la base de données et donc les données locales.

## 9. Structure actuelle du projet

```text
plateforme-intelligente-analyse/
├── backend/
│   ├── config/
│   ├── migrations/
│   ├── public/
│   ├── src/
│   │   ├── Entity/
│   │   └── Repository/
│   ├── Dockerfile
│   ├── composer.json
│   └── composer.lock
├── docker-compose.yml
├── .env.example
├── .gitignore
└── README.md
```

Cette structure évoluera à mesure que les modules frontend et analytique seront ajoutés.

## 10. Règles de travail en équipe

- Récupérer les dernières modifications avant de commencer une tâche.
- Créer une branche dédiée aux nouvelles fonctionnalités.
- Faire des commits courts et explicites.
- Tester les modifications avant de les pousser sur GitHub.
- Ne jamais publier de mots de passe, tokens, clés API ou fichiers `.env` personnels.
- Ne pas supprimer les volumes Docker sans vérifier leur contenu.
- Documenter les nouvelles étapes d'installation et les changements importants.

Exemples de messages de commit :

```text
feat: add user authentication
fix: correct database connection
docs: update installation instructions
test: add user repository tests
```

## 11. Prochaines étapes

1. Finaliser la configuration Symfony et Doctrine.
2. Vérifier et corriger la configuration de sécurité.
3. Préparer et exécuter les migrations de base de données.
4. Développer l'authentification et les premières fonctionnalités métier.
5. Ajouter progressivement le frontend React et le service Python.
6. Mettre en place les tests et l'intégration continue.

---

README initial — environnement de développement local.# Plateforme-intelligente-d-analyse-de-donn-es
