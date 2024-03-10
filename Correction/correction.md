
# Réponses de l'exercice 4

#### 1. Sélection des films
```sql
SELECT NOM FROM `films`; 
```
#### 2. Sélection des films à venir
```sql
SELECT NOM FROM `films` WHERE DATE_SORTIE >= (SELECT NOW()); 
```
#### 3. Sélection des salles gérées par Jean
```sql
SELECT NOM FROM `salles`, projections 
  WHERE projections.ID_EMPLOYES = (SELECT ID FROM employes WHERE PRENOM = "Jean")
  AND salles.ID = projections.ID_SALLES;
```
#### 4. Sélection du planning des employés
```sql
SELECT salles.NOM, employes.NOM, employes.PRENOM, projections.HORAIRE FROM salles, projections, employes 
  WHERE projections.ID_EMPLOYES = employes.ID
  AND salles.ID = projections.ID_SALLES; 
```
#### 5. Sélection des films de la catégorie 1 
```sql
SELECT * FROM films, categories, relations_films_categories
  WHERE films.ID = relations_films_categories.ID_FILMS
  AND categories.ID = relations_films_categories.ID_CATEGORIES
  AND categories.ID = 1 
```
#### 6. Films pour les -12
```sql
SELECT films.NOM FROM films,classification_age_public
  WHERE classification_age_public.ID = films.ID_CLASSIFICATION_AGE_PUBLIC
  AND classification_age_public.INTITULE = "Tous publics";
```
#### 7. Films projetés par Jean
```sql
SELECT films.NOM FROM films, projections, employes 
  WHERE projections.ID_EMPLOYES = employes.ID
  AND projections.ID_FILMS = films.ID
  AND employes.PRENOM = "Jean";
```
#### 8. Afficher le nombre de films et pas la liste
```sql
SELECT count(films.NOM) FROM films, projections, employes 
  WHERE projections.ID_EMPLOYES = employes.ID
  AND projections.ID_FILMS = films.ID
  AND employes.PRENOM = "Jean";
```
#### 9. Afficher les films + catégories + classifications
```sql
SELECT F.NOM, C.NOM, CAP.INTITULE, P.HORAIRE FROM films F, projections P, categories C, relations_films_categories RFC, classification_age_public CAP
  WHERE F.ID = P.ID_FILMS
  AND F.ID = RFC.ID_FILMS
  AND RFC.ID_CATEGORIES = C.ID
  AND F.ID_CLASSIFICATION_AGE_PUBLIC = CAP.ID;
```
#### 10. La même chose avec les horaires croissant
```sql
SELECT F.NOM, C.NOM, CAP.INTITULE, P.HORAIRE FROM films F, projections P, categories C, relations_films_categories RFC, classification_age_public CAP
    WHERE F.ID = P.ID_FILMS
    AND F.ID = RFC.ID_FILMS
    AND RFC.ID_CATEGORIES = C.ID
    AND F.ID_CLASSIFICATION_AGE_PUBLIC = CAP.ID
    ORDER BY P.HORAIRE ASC; 
```
#### 11. La même chose que pour Jean
```sql
SELECT F.NOM, C.NOM, CAP.INTITULE, P.HORAIRE FROM films F, projections P, categories C, relations_films_categories RFC, classification_age_public CAP, employes E
    WHERE F.ID = P.ID_FILMS
    AND F.ID = RFC.ID_FILMS
    AND RFC.ID_CATEGORIES = C.ID
    AND F.ID_CLASSIFICATION_AGE_PUBLIC = CAP.ID
    AND P.ID_EMPLOYES = E.ID
    AND E.PRENOM = 'Jean'
    ORDER BY P.HORAIRE ASC; 
```
#### 12. Mettre à jour le planning des employés
```sql
UPDATE projections 
  SET ID_EMPLOYES = 5
  WHERE ID_EMPLOYES = 2; 
```
#### 13. 
```sql
UPDATE employes 
SET MAIL = "nouvel@email.com"
WHERE ID = (
    SELECT ID FROM (
        SELECT ID FROM employes
        ORDER BY ID
        LIMIT 1 OFFSET 2
    ) AS subquery
);
```
#### 14. Ajouter un nouveau film
```sql
INSERT INTO `films` (`ID`, `NOM`, `URL_AFFICHE`, `LIEN_TRAILER`, `RESUME`, `DUREE`, `DATE_SORTIE`, `ID_CLASSIFICATION_AGE_PUBLIC`) VALUES (NULL, 'Bob Marley One Love', 'https://fr.web.img6.acsta.net/c_310_420/pictures/24/01/18/11/59/2019347.jpg', 'https://www.allocine.fr/video/player_gen_cmedia=19604528&cfilm=290882.html', 'Bob Marley: One Love célèbre la vie et la musique d\'une icône qui a inspiré des générations à travers son message d\'amour et d\'unité.\r\n\r\nPour la première fois sur grand écran, découvrez l\'histoire puissante de Bob Marley, sa résilience face à l’adversité, le chemin qui l’a amené à sa musique révolutionnaire.\r\n', '01:47:00', '2024-02-17', '1');
```

#### 15. Suppression avancée

Afin de se faciliter la vie dans les sélections multiples (et accessoirement pour réussir à faire la requête, parce que sinon on se confronte à des problèmes), on va définir une variable, qui s'écrit en SQL avec `INTO @ma_variable`.
```sql
SELECT MIN(films.DATE_SORTIE) INTO @OLD_DATE FROM films;

DELETE FROM relations_films_categories WHERE ID_FILMS IN (
    SELECT ID FROM films WHERE DATE_SORTIE = @OLD_DATE
);
DELETE FROM projections WHERE Id_Films IN (
    SELECT ID FROM films WHERE DATE_SORTIE = @OLD_DATE
);

DELETE FROM films WHERE films.DATE_SORTIE = @OLD_DATE;
```
#### 16. Supprimer toutes les classifications inutilisées
```sql
DELETE FROM classification_age_public
  WHERE classification_age_public.ID NOT IN (SELECT ID_CLASSIFICATION_AGE_PUBLIC FROM films);
```
#### 17. 
```sql
INSERT INTO `classification_age_public` (`ID`, `AVERTISSEMENT`, `INTITULE`) VALUES (NULL, '', 'Interdit aux moins de 18 ans non classé X'), (NULL, '', 'Interdit aux moins de 18 ans classé X');
```

#### 18. 
```SQL
DROP DATABASE IF EXISTS cinema
```
