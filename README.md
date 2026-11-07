# TD FHIR · M2 Data Science en santé

Séance 1 de l'option Data (Université de Lille) : **samedi 17 octobre 2026**.
Ce dossier contient le notebook de la séance, les données fictives et de quoi l'ouvrir sur votre ordinateur
ou dans le navigateur. Le déroulé pas à pas est dans **[TD.md](TD.md)**.

> Toutes les données sont **synthétiques** : aucune ne concerne une personne réelle.
> N'écrivez jamais de données réelles sur le serveur FHIR public.

| Votre situation | Voie | À télécharger |
|---|---|---|
| Python 3.10 ou plus sur votre ordinateur | A · En local | quelques paquets Python (pip) |
| Pas de Python, ou installation qui bloque | B · Codespaces | rien (tout se passe chez GitHub) |

## Ce qu'il faut

- Une connexion Internet pour le TP 1 (serveur FHIR public). Le TP 2 fonctionne hors ligne.
- Ce dossier :
  ```bash
  git clone https://github.com/Lille-Health-Data-Science/td-fhir-sante.git
  cd td-fhir-sante
  ```

## A · En local

```bash
python -m venv .venv
source .venv/bin/activate          # Windows : .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook seance1_etudiant.ipynb
```

Ouvrez le notebook **depuis ce dossier** : il lit ses données dans `donnees/`.

## B · Dans le navigateur, avec GitHub Codespaces

Sur la page GitHub du dépôt : *Code › Codespaces › Create codespace on main*. Les paquets s'installent seuls
(2 à 3 min). Ouvrez ensuite `seance1_etudiant.ipynb` dans l'éditeur et choisissez le noyau Python proposé.
Un compte GitHub gratuit suffit (heures incluses).

## Vérifier que tout marche

1. Exécutez la première cellule du notebook : elle vérifie les versions des paquets et la présence de `donnees/`.
2. Exécutez la première cellule de la partie C : elle doit afficher **Patient 150**, **Observation 984**,
   **Condition 55**.
3. Exécutez l'étape 0 de la partie B : « Serveur joignable » (sinon, voir ci-dessous).

## Rendre le projet « application diabète »

La remise se fait par `git push` sur votre dépôt de rendu `<nom>.<prenom>.optiondata.2026` :
votre notebook ou script, la courbe, et une demi-page de réponses (`REPONSES.md`).
Le `.gitignore` fourni évite de pousser les fichiers produits (`sortie/`) et les fichiers techniques.

## En cas de problème

| Message | Solution |
|---|---|
| `ModuleNotFoundError` | `pip install -r requirements.txt` dans le même environnement que Jupyter (noyau du `.venv`) |
| `FileNotFoundError: donnees/...` | Le notebook n'a pas été ouvert depuis ce dossier : relancer Jupyter depuis `td-fhir-sante` |
| « Serveur injoignable » (étape 0) | Vérifier le réseau, ou lancer un serveur local : `docker run -p 8080:8080 hapiproject/hapi:latest`, puis `BASE = "http://localhost:8080/fhir"` |
| `412` à l'étape 3 | Le serveur refuse une copie exacte d'une ressource existante : relancer la cellule, l'identifiant est tiré au hasard |
| Autre chose | Écrire à l'enseignant avec une capture d'écran |

## Contenu du dossier

| Élément | Rôle |
|---|---|
| `seance1_etudiant.ipynb` | Le notebook de la séance : exercices (A), TP 1 serveur FHIR (B), TP 2 FHIR → OMOP (C), bonus (D) |
| `donnees/export_fhir/` | Export FHIR fictif au format Bulk Data (NDJSON) : 150 patients, 984 observations, 55 diagnostics |
| `donnees/concepts.csv` | Identifiants OMOP utiles au TP 2 (extrait pédagogique, à vérifier dans Athena) |
| `requirements.txt` | Paquets Python et versions minimales |
| `.devcontainer/` | Configuration GitHub Codespaces (voie B) |

La suite : la séance 2 reprend ce flux dans un pipeline Airflow, dépôt
[`td-airflow-sante`](https://github.com/Lille-Health-Data-Science/td-airflow-sante).
