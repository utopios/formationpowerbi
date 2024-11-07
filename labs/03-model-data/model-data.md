```markdown
# Exercice : Modélisation en Étoile pour GRDF dans Power BI

## **Contexte**
GRDF souhaite structurer ses données pour mieux analyser ses interventions, équipements, clients, et adresses. En plus de concevoir un modèle en étoile, vous devrez :
1. Ajouter des hiérarchies dans les dimensions pour simplifier l'analyse.
2. Configurer des matrices pour explorer les données de manière hiérarchique.
3. Créer des colonnes calculées pour compléter les données manquantes.

---

## **Objectifs**
1. Importer les fichiers de données dans Power BI.
2. Construire un modèle en étoile avec des relations correctement définies.
3. Ajouter des colonnes calculées pour enrichir les données.
4. Configurer des hiérarchies dans certaines tables dimensionnelles.
5. Créer une matrice pour explorer les données avec les hiérarchies.
6. Répondre à des questions sur les résultats obtenus.


---

## **Instructions**

### Étape 1 : Importer et Nettoyer les Données
- Importez les fichiers CSV dans Power BI.
- Nettoyez les données si nécessaire (valeurs nulles, doublons).

### Étape 2 : Construire un Modèle en Étoile
- Identifiez la table des faits : `Interventions`.
- Reliez les dimensions :
  - `Interventions.DateID` → `Dates.DateID`
  - `Interventions.ClientID` → `Clients.ClientID`
  - `Interventions.AddressID` → `Addresses.AddressID`
  - `Interventions.EquipmentID` → `Equipments.EquipmentID`
  - `Interventions.TechnicianID` → `Technicians.TechnicianID`

### Étape 3 : Ajouter des Colonnes Calculées
- Dans Power BI, ajoutez une colonne calculée dans `Interventions` CostTotal qui vaut cost ou 50 * Duration si cost null

### Étape 4 : Créer des Hiérarchies
- Dans `Dates` : **Année > Mois > Jour**
- Dans `Addresses` : **Région > Ville > Rue**
- Dans `Equipments` : **Type d'Équipement > Modèle > Fabricant**

### Étape 5 : Configurer une Matrice
- Créez une matrice affichant les **coûts des interventions** regroupés par :
  - **Colonnes** : Hiérarchie des dates (Année > Mois > Jour).
  - **Lignes** : Hiérarchie des adresses (Région > Ville).
  - **Valeurs** :
    - Total des Coûts : `SUM(Interventions[Cost])`
    - Durée Totale : `SUM(Interventions[Duration])`

---

## **Questions**

1. **Hiérarchies :**
   - Quels champs avez-vous utilisés pour chaque hiérarchie ?
   - Comment ces hiérarchies facilitent-elles l'analyse ?

2. **Matrice :**
   - Quelle région a enregistré le coût total le plus élevé en novembre ?
   - Quelle région a eu la plus longue durée totale d’interventions pour les chaudières ?

3. **Colonnes Calculées :**
   - Comment la colonne calculée pour les coûts a-t-elle impacté l’analyse ?



