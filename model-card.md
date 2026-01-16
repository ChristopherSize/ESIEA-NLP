
# Model Card : RoBERTa-base modèle fine tuné pour la classification de la toxicité des commentaires

## Détails

### Description

Ce modèle est une version fine tuné de **`roberta-base`** pour de la **classification multi-class**. L'objectif c'est la prédiction de la présence de multiple trait toxiques dans su text. Il peut distinguer 6 catégories différentes:

* toxic
* severe_toxic
* obscene
* threat
* insult
* identity_hate

- **Dévelopé par:** MVOGO ZE Aurel Danial, OUMAR DIAWARA
- **Langue(s) (NLP):** Anglais
- **Licence:** [`Licence`](https://huggingface.co/FacebookAI/roberta-base)

### Provenance du Modèle 

- **Repository:** [`repo`](https://github.com/ChristopherSize/ESIEA-NLP)

## Objectif

- Le modèle peut être utilisé dans des forums ou des plateformes a fin de détecter des propos clivant et de prendre les décision qui s'impose. 

### Recommendations

**NB:** Il est primordial d'être sur un environnement ayant des gpu pour accélérer le processus.

## Comment utiliser le modèle

Pour utiliser le modèle il faudra suivre les instructions suivantes:
- Vos données d'entrainements, de tests et de vérifications doivent être des fichiers csv
- Commencer avec le fichier **NLP_Data_pipeline.ipynb** insérer le chemin d'accès vers vos données d'entrainements ensuite inséré le nom du fichier dans le quel vous souhaité conserver vos données nettoyé.
- Faites la même chose pour vos données de test
- Ensuite utiliser le fichier **fine-roberta**, insérer le chemin d'accès vers vos différents fichiers et exécuter les cellules.



## Détails sur l'entrainement

### Données d'entrainement

Les données utilisé ont été créé par Google Jigsaw pour attirer l'attention sur les commentaires toxiques présents sur les réseaux sociaux. Ces données viennent essentiellement de la plateforme wikipedia.

#### Pré-traitement

Avant de fine-tuné notre modèle avec nos données, nous avons pré-traité les données pour avoir retirer les particularité suivante:
- Les accents
- La punctuation
- Les majuscules (car RoBERTa fait la différence entre Anglais et anglais)
- Les urls
- les chiffres
- les "stopwords"
- Les extensions des images

Par la suite nous avons transformé nos données en token à l'aide d'un tokenizer avec les paramètres suivants:
- add_special_tokens=True (Avec ceci on insère les tokens spéciales [CLS] et [SEP] dans chaques phrases)
- return_tensors='pt' (Ceci nous permet d'avoir un tenseur en sortie)
- truncation=True (Tronquer les listes de token qui dépasse la taille maximal)
- max_length=128 (La taille maximal de la liste de nos token) 
- padding='max_length' (Pour des listes de plus petites taille, on rajoute du padding car toutes les listes doivent avoir la même taille)
- return_attention_mask=True (Le mask d'attention c'est la matrice qui indique au modèle sur quelle cellule il doit ce concentrer)

#### Training Hyperparameters

- number_of_labels: 6
- epochs: 2
- learning_rate: 1.5e-06
- weight_decay: 0.001
- batch_size: 128
- warmup: 0.2
- optimizer: Adam

#### Vitesse, Taille, Temps 

Nous avons 159571 observations dans notre jeu de données et fine-tuné le modèle sur google colab avec GPUT4 nous a pris 1h50minutes.
Effectuer des prédictions sur notre jeu d'entrainement nous a pris 20 minutes

## Evaluation

<!-- This section describes the evaluation protocols and provides the results. -->

### Testing Data, Factors & Metrics

#### Testing Data

<!-- This should link to a Dataset Card if possible. -->

{{ testing_data | default("[More Information Needed]", true)}}

#### Factors

<!-- These are the things the evaluation is disaggregating by, e.g., subpopulations or domains. -->

{{ testing_factors | default("[More Information Needed]", true)}}

#### Metrics

<!-- These are the evaluation metrics being used, ideally with a description of why. -->

{{ testing_metrics | default("[More Information Needed]", true)}}

### Results

{{ results | default("[More Information Needed]", true)}}

#### Summary

{{ results_summary | default("", true) }}

