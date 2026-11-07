# TD FHIR · déroulé de la séance (samedi 17 octobre)

**Objectif de fin de séance** : vous savez écrire, valider et rechercher des ressources FHIR, et vous avez
transformé un export FHIR en deux tables OMOP (PERSON et MEASUREMENT) pour répondre à une question clinique.

Tout se fait dans **`seance1_etudiant.ipynb`**. Les cellules marquées `# À COMPLÉTER` contiennent des `...`
à remplacer.

| Partie du notebook | Moment de la séance | Ce que vous faites | Vous avez fini quand… |
|---|---|---|---|
| A · Exercices | parties 01 et 02 | écrire, valider, interroger des ressources (18 min) | `obs2` passe la validation |
| B · TP 1 | partie 03 | interroger le serveur FHIR public en Python | vous avez un tableau des glycémies du serveur |
| C · TP 2 | partie 04 (25 min) | construire PERSON et MEASUREMENT avec DuckDB | `sortie/person.parquet` et `sortie/measurement.parquet` existent |
| D · Explorer | bonus | jouer avec le critère, un patient à la loupe, défis | — |

---

## A · Exercices des parties 01 et 02

1. **A1 · Écrire et valider une ressource (8 min)** : écrire `obs2`, la glycémie de la même patiente le
   lendemain à 8 h 10, à 1,26 g/L ; la valider avec `fhir.resources` ; la rattacher au séjour `Encounter/sejour-001`.
2. **A2 · Exécuter une recherche (5 min)** sur le serveur public.
3. **A3 · FHIRPath en Python (5 min)**.

## B · TP 1 : interroger un serveur FHIR (partie 03)

Le code est celui des slides : exécutez chaque étape, puis répondez aux questions « À faire » de la slide.
Remplacez `G3` par votre numéro de groupe.

| Étape | Ce qu'elle fait |
|---|---|
| 0 | Vérifie que le serveur répond |
| 1 | Lit le CapabilityStatement : version FHIR et types de ressources |
| 2 | Recherche des patients (`family=Martin`) |
| 3 | Crée un patient et sa glycémie en une seule transaction |
| 4 | Suit la pagination (`link` `next`) : **ce code resservira en séance 2** |
| 5 | Aplatit les glycémies en tableau, puis les montre par unité |

## C · TP 2 : d'un export FHIR à un mini-entrepôt OMOP (partie 04 · 25 min)

`donnees/export_fhir/` contient ce que renverrait un `$export` (Bulk Data) d'un hôpital fictif.

| Étape | Durée | À faire |
|---|---|---|
| C1 · Explorer | 3 min | compter les observations par code LOINC, unité et statut |
| C2 · Aplatir et harmoniser | 8 min | garder les glycémies valides, tout convertir en mg/dL |
| C3 · PERSON | 5 min | une ligne par patient (150) |
| C4 · MEASUREMENT | 5 min | une ligne par glycémie, avec le concept et l'unité OMOP |
| C5 · Question clinique | 4 min | qui a au moins deux glycémies ≥ 126 mg/dL ? Combien sans diagnostic codé ? |
| C6 · Sauvegarder | 1 min | exporter les deux tables en Parquet dans `sortie/` |

Pièges prévus dans les données : trois unités (mg/dL, g/L, mmol/L), deux codes LOINC de glycémie, des HbA1c
à ne pas confondre avec la glycémie, des mesures annulées ou saisies par erreur.

## D · Explorer (bonus)

Faire varier le seuil du critère, suivre un patient sur la durée, relever les défis : en fin de TP ou à la maison.
