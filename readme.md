# Bases de données

Un cinéma vous a demandé de faire une application de gestion des salles, des films projetés et du personnel.

## Cahier des charges
Le site permettra de gérer les ressources du cinéma (personnel, salles, horaires), pour optimiser les projections.

Vous devez donc créer une base de données qui stockera toutes ces infos :

<details open>
  <summary><b>les salles</b></summary>

  - ID
  - nom de la salle
  - nombre de places
  - accessibilité PMR
</details>

<details>
  <summary><b>Les films</b></summary>

  - ID
  - nom du film
  - url de l'affiche
  - lien du trailer
  - résumé
  - durée
  - date de sortie
</details>

<details>
  <summary><b>les catégories de films</b></summary>

  - ID
  - nom de la catégorie
  - Description
</details>

<details>
  <summary><b>classification age public</b></summary>

  - id
  - intitulé (voir ci-dessous)
  - Avertissement (peut être adjoint à n'importe quel classement) : booléen

  Les valeurs attendues seront :

    - Tous publics
    - Interdit aux moins de 12 ans
    - Interdit aux moins de 16 ans
    - Interdit aux moins de 18 ans non classé X 
    - Interdit aux moins de 18 ans classé X 
</details>

<details>
  <summary><b>Les employés</b></summary>

  - ID
  - Nom
  - Prénom
  - mail
  - téléphone
  - année d'arrivée dans le cinéma
</details>

### Les associations 
Les films seront associés aux catégories et aux classifications. 
Ils seront projetés dans des salles, à des horaires donnés, avec un employé possiblement différent pour chaque horaire. C'est l'horaire qui fera la différence entre plusieurs projections dans une même salle.

## Exercice 1
Construire le MCD du projet.

## Exercice 2
Préparer une base de données spécifique à ce projet. Exporter le SQL, et l'importer dans la base de données.

## exercice 3
Remplir la base avec des données d'exercice :
  Au moins 6 films (dont 2 avec des dates antérieures à aujourd'hui), 4 salles, 5 employés (dont 1 qui s'appelle Jean), 3 catégories.

## exercice 4
Vérifier avec quelques requêtes que tout se passe comme prévu :

1. Afficher les titres de tous les films.
2. Afficher les titres des prochains films (pas de dates antiérieures à maintenant).
3. Afficher le nom des salles que gèrera Jean.
4. Lister chaque employé et sa ou ses salle(s) associée(s).
5. Retrouver tous les films de la première catégorie.
6. Retrouver les films qui sont accessibles aux enfants (-12)
7. Retrouver les films projetés par Jean.
8. Afficher le nombre de ces films (et pas la liste).
9. Sélectionner tous les films, en leur associant le nom de la categorie à laquelle ils appartiennent et la classification d'âge, ainsi que les horaires des futures projections.
10. Faire la même chose, juste pour les films que gèrera Jean.
11. Finalement, l'employé 2 sera en arrêt pendant 1 mois, modifiez la base pour réattribuer les horaires à d'autres personnes.
12. Modifiez l'adresse mail de l'employé 3.
13. Ajoutez le dernier film qui vient de sortir.
14. Supprimez le film qui n'est plus projeté depuis le plus longtemps, en faisant une règle de sélection (admettons que vous ne voyez pas les films, vous voulez faire une commande SQL qui supprime sans que vous sachiez quel est ce film).
15. Supprimez toutes les classifications qui sont inutilisées.
16. Rajoutez-les, en fait c'est une erreur de votre employé ;)
17. Bravo, vous êtes très fort !