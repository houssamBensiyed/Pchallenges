### Questions théoriques

1) COUNT, SUM, AVG servent à résumer un ensemble de lignes en une seule valeur  
- `COUNT` compte des éléments (lignes ou valeurs)  
- `SUM` additionne des valeurs numériques  
- `AVG` calcule la moyenne (souvent \( \text{SUM} / \text{COUNT} \) en ignorant les `NULL`)

2) Non, `COUNT(*)` et `COUNT(colonne)` ne sont pas interchangeables  
- `COUNT(*)` compte toutes les lignes, y compris celles où `colonne` vaut `NULL`  
- `COUNT(colonne)` compte فقط les lignes où `colonne` n’est pas `NULL`  
Exemple : si une table a 10 lignes dont 3 avec `email = NULL`, alors `COUNT(*) = 10` mais `COUNT(email) = 7`

3) `MAX` et `MIN` fonctionnent aussi sur les dates et les chaînes  
- Sur des dates : `MAX(date_commande)` donne la date la plus récente, `MIN(...)` la plus ancienne (comparaison chronologique)  
- Sur des chaînes : `MAX(nom)` / `MIN(nom)` comparent selon l’ordre lexicographique et la collation (ex. sensibilité à la casse, accents, langue)

### Challenges pratiques

Les noms de tables/colonnes ci-dessous sont des exemples (adapte à ton schéma : `orders/commandes`, `products/produits`, etc.).

1) Challenge 1  nombre total de commandes  
```sql
SELECT COUNT(*) AS total_commandes
FROM commandes;
```

2) Challenge 2  prix moyen de tous les produits  
```sql
SELECT AVG(prix) AS prix_moyen
FROM produits;
```

3) Challenge 3 montant de la commande la plus chère  
Cas A (si la table `commandes` a déjà un total, ex. `montant_total`) :  
```sql
SELECT MAX(montant_total) AS commande_plus_chere
FROM commandes;
```

Cas B (si le total doit être calculé depuis des lignes, ex. `ligne_commandes(commande_id, quantite, prix_unitaire)`) :  
```sql
SELECT MAX(total_commande) AS commande_plus_chere
FROM (
  SELECT commande_id,
         SUM(quantite * prix_unitaire) AS total_commande
  FROM ligne_commandes
  GROUP BY commande_id
) t;
```