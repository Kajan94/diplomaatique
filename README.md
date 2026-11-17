# DiplomAAtique · Du texte OCR à une recherche d’arrêtés

Projet universitaire réalisé en équipe. Le programme part d’un recueil au format texte issu de l’OCR, sépare les arrêtés, puis extrait leurs articles et leurs métadonnées dans des fichiers JSON. L’interface Flask permet de retrouver les actes importés dans SQLite.

![Recherche d’un arrêté fictif par mot-clé](docs/recherche-jardin.jpg)

## Reproduire le résultat

Le dossier `exemple/` fournit un recueil fictif et son contexte. L’extraction et son test utilisent la bibliothèque standard Python.

~~~sh
python diplomaatique.py exemple/raa-fictif.txt exemple/raa-fictif.json --output output
python -m unittest discover -s tests
~~~

Le test vérifie les deux identifiants d’arrêté et la répartition des articles. L’[arrêté du jardin](exemple/resultat/raa-fictif-01.json) contient **deux articles**. Celui de la [bibliothèque](exemple/resultat/raa-fictif-02.json) en contient **un**.

### Consulter le résultat dans le navigateur

~~~sh
python -m pip install -r requirements.txt
python app.py
~~~

Sur [localhost:5000](http://127.0.0.1:5000/), chercher **jardin**. L’application indexe les JSON générés dans `output/`.

## Où intervenir

- **Découpage et normalisation** — `cleaner.py` et `arrete_separate.py`.
- **Extraction des champs** — `extractors/` contient notamment les règles des articles, des visas et des autorités.
- **Restitution** — `app.py`, `controllers/`, `models/` et `views/` organisent la recherche et les pages.

La qualité des champs dépend du texte OCR. L’exemple du jardin montre un cas où l’autorité émettrice demande une relecture.

[Projet dans le portfolio](https://kajan94.github.io/Portefolio/#diplomaatique)
