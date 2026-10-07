![CI Pipeline](https://github.com/MrrBoo/cicd-fil-rouge/actions/workflows/ci.yml/badge.svg?branch=main)

# TaskFlow — dépôt fil rouge CI/CD

TaskFlow est une petite API de gestion de tâches écrite en Python avec FastAPI.
C'est le projet fil rouge du module CI/CD (Mastère DevOps M1, Sup de Vinci) :
pendant trois jours, vous allez construire autour d'elle un pipeline complet
qui teste, construit, sécurise et livre l'application.

## Lancer l'API en local

Prérequis : Python 3.10 ou plus récent.

```bash
python3 -m venv .venv
source .venv/bin/activate          # Windows : .venv\Scripts\activate
pip install -r requirements-dev.txt
uvicorn app.main:app --reload
```

L'API répond sur http://localhost:8000 et sa documentation interactive est sur
http://localhost:8000/docs.

## Vérifier le code

```bash
pytest           # tests automatiques
ruff check .     # lint
ruff format .    # mise en forme
```

## Lancer avec Docker

```bash
docker build -t taskflow .
docker run --rm -p 8000:8000 taskflow
```

## Endpoints

| Méthode | Chemin | Rôle |
| --- | --- | --- |
| GET | `/health` | État de l'API et version |
| GET | `/tasks` | Liste des tâches |
| GET | `/tasks/search?q=...` | Recherche dans les titres |
| POST | `/tasks` | Crée une tâche (`{"title": "..."}`) |
| GET | `/tasks/{id}` | Détail d'une tâche |
| PATCH | `/tasks/{id}/done` | Marque une tâche comme faite |
| DELETE | `/tasks/{id}` | Supprime une tâche (en-tête `X-API-Token` requis) |

## Configuration

| Variable | Rôle | Défaut |
| --- | --- | --- |
| `APP_VERSION` | Version affichée par `/health` | `0.1.0` |
| `DB_PATH` | Fichier SQLite | `taskflow.db` |
| `API_TOKEN` | Jeton exigé pour supprimer une tâche | vide (suppression désactivée) |
| `NOTIFY_WEBHOOK_URL` | Webhook appelé à chaque création de tâche | vide (désactivé) |

## Équipe
Ibrahim KONE

Stanislas de Dieuleveult
<!-- Lab J1 : remplacez par les noms du binôme -->

## Gouvernance du dépôt

<!-- Lab J1 : listez les règles activées sur main, pourquoi chacune, et ajoutez la capture du push refusé -->

Ajout d'un workflow ci.yml pour effectuer un job de test et de lint

<img width="454" height="207" alt="image" src="https://github.com/user-attachments/assets/bfa56ee2-719f-4005-891d-e6e8beb27039" />


Paramètres utilisés dans le ruleset pour que le merge sur la branche main ne se fasse que lorsque les 2 jobs sont en verts

<img width="1852" height="896" alt="image" src="https://github.com/user-attachments/assets/208a1457-8149-4ecb-a0fe-92f451da4b5e" />


Si le job test ou lint n'est pas vert, on ne peut pas merge

<img width="358" height="424" alt="image" src="https://github.com/user-attachments/assets/74ecbb63-7247-4aa9-8fb6-b9433491471e" />

# LAB Jour 1 - Partie 2

Ajout du cache, matrice python, concurrency et rapport de test en artefact. Comme on peut le voir, le job test ne passe pas même si tout est vert.

<img width="454" height="285" alt="image" src="https://github.com/user-attachments/assets/32ded1c9-c165-43d9-a178-cabb6c7f16a4" />

Il faut ajouter un nouveau job CI OK qui va fait un seul check

<img width="454" height="213" alt="image" src="https://github.com/user-attachments/assets/9e40b90d-24bf-4b1e-bd86-eb03bc1d8ccf" />

<img width="454" height="252" alt="image" src="https://github.com/user-attachments/assets/e9768011-54cb-4eb5-902b-65f6d6a87d7d" />

<img width="454" height="229" alt="image" src="https://github.com/user-attachments/assets/2bcf7acb-df9a-41f2-90de-803d321e8019" />

On a bien les artefacts que l'on peut télécharger

<img width="454" height="137" alt="image" src="https://github.com/user-attachments/assets/984e2416-7dc3-44b4-b5bc-4411673e08f7" />


