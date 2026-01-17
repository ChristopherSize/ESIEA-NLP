# Classification de toxicité de commentaires à l'aide du roBERTa-base modèle

L'objectif de ce modèle est de dire si un commentaire tombe ou pas dans l'une des catégories suivantes:

* toxic
* severe_toxic
* obscene
* threat
* insult
* identity_hate

## Description du contenu du dosier

* treated_data: C'est un répertoire qui contient nos résultats sous formats csv. Plus précisement, nous avons:
    1. cleaned_test.csv: Correspond à notre jeu test nettoyé par notre data pipeline
    2. cleaned_train.csv: Correspond à notre jeu d'entrainement nettoyé par notre data  pipeline
    3. submission_classified.csv: Correspond aux prédictions effectué par CHATGPT5 sur cleaned_test.csv
    4. stopwords (1).txt: Correspond aux "stopwords" qui ont été utilisé dans notre data pipeline
    5. test_predictions.csv: Contient les prédictions de notre modèle
* model-card.md: Contient les informations sur l'entrainement de notre modèle
* NLP_Data_pipeline.ipynb: C'est le data pipeline qui nous permis de nettoyer nos données
* roBERTa-base: Contient les fichiers de notre modèle (Le modèle étant très volumineux, ces fichiers n'ont pas été sauvegardé)