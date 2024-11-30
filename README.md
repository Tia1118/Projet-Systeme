# Projet-Systeme
Ce script Python analyse un fichier SAM (Sequence Alignment/Map) pour répondre à plusieurs questions importantes sur les données de séquençage alignées. Il permet de :

Vérifier la validité d'un fichier SAM :

S'assurer que le fichier à la bonne extension ( .sam), qu'il n'est pas vide, et qu'il contient des données compatibles avec le format SAM.
Stocker les données dans une structure Python :

Les données sont lues et stockées dans un dictionnaire pour faciliter l'accès et l'analyse.
Analyser les lectures (alignements) :

Combien de lectures sont mappées ou non mappées ?
Comment les reads (et paires de reads) sont-ils mappés en fonction du flag ?
Où les reads sont-ils mappés (par chromosome) et l'alignement est-il homogène ?
Avec quelle qualité les reads sont-ils mappés (score de mapping) ?
Permettre des filtres pour l'analyse :

Filtrer les reads par qualité de mapping (par exemple, les reads entièrement mappés ou avec une qualité < 30).
Le script inclut une visualisation des résultats sous forme de graphiques pour mieux interpréter les données.

Prérequis
Python 3.x installé.
Modules Python nécessaires :
argparse: Gestion des arguments en ligne de commande.
csv: Lecture des fichiers CSV générés à partir des fichiers SAM.
matplotlib: Visualisation des résultats sous forme de graphiques.
collections: Utilisé pour des comptages simples.
Installez les dépendances si nécessaire :

frapper

Copier le code
pip install matplotlib
Utilisation
Commandes
Exécution simple : Fournir le fichier SAM à analyser.

frapper

Copier le code
python script_analyse_sam.py --input fichier.sam
Exécution avec filtres : Ajoutez des paramètres pour filtrer les résultats :

Filtrer par qualité de cartographie < 30:
frapper

Copier le code
python script_analyse_sam.py --input fichier.sam --qualite 30
Analyser uniquement les lectures entièrement mappées :
frapper

Copier le code
python script_analyse_sam.py --input fichier.sam --entierement-mappes
Arguments
--input:Chemin vers le fichier SAM.
--qualite: (Optionnel) Score de qualité maximale à inclure dans l'analyse (par défaut : aucun filtre).
--entierement-mappes: (Optionnel) Inclure uniquement les reads sans erreurs d'alignement.
Structure du script
1. Vérification de la validité du fichier SAM
Le script vérifie que :

Le fichier existe.
Il est à la bonne extension .sam.
Il n'est pas vide.
Il contient des lignes compatibles avec le format SAM (par exemple, des en-têtes @ou des colonnes attendues).
2. Chargement des données dans un dictionnaire
Les lignes du fichier SAM sont lues et stockées dans une structure de type dictionnaire Python pour une manipulation facile. Chaque ligne est représentée comme une clé avec ses colonnes associées.

3. Analyse des lectures
3.1. Lit mappés/non mappés
Le drapeau (colonne 2) indique si un read est mappé :

Un read est considéré comme non mappé si le bit 4du flag est activé.
Résultat affiché en pourcentage et en nombre absolu.
3.2. Comptage des lectures par flag
Chaque valeur unique de FLAGest comptée pour comprendre les différents types d'alignements (paires mappées, non mappées, etc.).

3.3. Répartition par chromosome
La colonne de référence (chromosome) est analysée pour déterminer le nombre de lectures alignées sur chaque chromosome. Cela permet d'identifier les biais d'alignement.

3.4. Qualité de la cartographie
La colonne MAPQest utilisée pour analyser la qualité de cartographie. Les lectures sont regroupées par tranche de partitions pour interpréter la précision des alignements.

Résultats et visualisation
Les résultats de l'analyse sont affichés sous forme de tableaux et de graphiques.

Graphiques générés :
Répartition des lectures mappés/non-mappés :
Diagramme à barres.
Comptage des lectures par flag :
Histogramme.
Alignement par chromosome :
Diagramme circulaire.
Qualité de la cartographie :
Histogramme des scores MAPQ.
