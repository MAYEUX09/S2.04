# SAÉ 2.04 - Analyse Statistique et Suivi des Capteurs Industriels

Ce projet a pour objectif d'améliorer les chaînes de production d'une usine productrice de rouleaux de papier en automatisant la détection d'erreurs des capteurs et en gérant leur cycle de vie. Le système remplace une vérification manuelle chronophage par une approche automatisée et mathématique.

### Objectifs du Projet

* Automatiser la détection des erreurs en créant des algorithmes Python capables de repérer instantanément le bruit excessif et les dérives de mesure.


* Gérer le cycle de vie des capteurs grâce à une base de données PostgreSQL pour stocker l'historique des équipements, de leur mise en service à leur fin de vie.


* Visualiser la contrôlabilité du système à l'aide de cartes de contrôle permettant d'identifier les pannes et les dérèglements.



### Partie 1 : Statistiques et Cartes de Contrôle

L'analyse de la fiabilité des capteurs repose sur des calculs statistiques appliqués aux données brutes extraites de la base de données.

* **Extraction et comparaison :** Le système compare les mesures automatiques des capteurs avec les valeurs de référence manuelles (calcul de la différence `controlvalue - sensorvalue`) pour identifier les erreurs brutes.


* **Calcul des indicateurs :** La moyenne globale de l'erreur ($\mu$) et son écart-type ($\sigma$) sont calculés via des requêtes SQL d'agrégation (`AVG` et `STDDEV`) afin d'évaluer respectivement le biais et le bruit de fond de chaque capteur.


* **Cartes de contrôle :** Des graphiques générés avec Matplotlib affichent l'évolution des erreurs dans le temps, en superposant la moyenne, les limites d'avertissement ($\pm 1\sigma$) et les limites de contrôle ($\pm 2\sigma$).


* **Analyse approfondie :** Le "Capteur 3" a été spécifiquement sélectionné pour les tests algorithmiques en raison de son comportement réaliste, combinant un bruit de fond modéré avec des valeurs aberrantes régulières.



### Partie 2 : Base de Données et Cycle de Vie

L'architecture de la base de données initiale a été étendue pour intégrer un historique complet des interventions de maintenance.

* **Table `SensorEvent` :** Cette nouvelle table agit comme un journal de bord consignant la nature des interventions (`COMMISSIONING`, `RECALIBRATION`, `SCRAP`) et leur horodatage.


* **Vue `SensorTimeline` :** Une vue SQL préparatoire a été mise en place pour centraliser les dates clés et le nombre d'incidents par équipement, garantissant un code clair et performant.


* **Indicateurs de maintenance :** Le système exécute des requêtes complexes utilisant la fonction `NULLIF` pour éviter les divisions par zéro, permettant de calculer le nombre moyen de réétalonnages par an, le taux de survie à un an (robustesse initiale) et la fiabilité à un mois (défauts de jeunesse).



### Technologies Utilisées

* **Python :** Exploité dans un environnement Jupyter Notebook, avec les bibliothèques `psycopg` pour la connexion à la base de données et `matplotlib` pour la génération des cartes de contrôle.


* **PostgreSQL :** Utilisé pour le stockage des mesures, l'architecture relationnelle et le calcul direct d'agrégats statistiques.



**Auteurs :** Ouameur Aïssa, Mayeux Ounays, Platel Alban.
