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

## **Fichiers Fournis**

### 1. `Interventions.csv`
```csv
InterventionID,DateID,TechnicianID,ClientID,AddressID,EquipmentID,Duration,Cost
1,20231101,101,201,301,401,2.5,
2,20231102,102,202,302,402,1.0,75
3,20231101,101,203,303,403,3.0,
4,20231103,103,204,304,404,1.5,100
5,20231102,104,201,301,405,2.0,
6,20231104,102,202,302,401,1.5,80
7,20231105,101,203,303,402,2.5,
8,20231106,104,204,304,403,3.5,200
```

---

### 2. `Clients.csv`
```csv
ClientID,FullName,PhoneNumber,Email,ClientType
201,Alice Martin,0612345678,alice.martin@mail.com,Particulier
202,Bob Durand,0623456789,bob.durand@mail.com,Entreprise
203,Chloé Bernard,0634567890,chloe.bernard@mail.com,Particulier
204,David Lefèvre,0645678901,david.lefevre@mail.com,Particulier
205,Emma Roux,0656789012,emma.roux@mail.com,Entreprise
206,François Morel,0667890123,francois.morel@mail.com,Particulier
```

---

### 3. `Addresses.csv`
```csv
AddressID,Street,City,PostalCode,Region
301,10 Rue de Paris,Paris,75001,Île-de-France
302,20 Avenue de Lyon,Lyon,69002,Auvergne-Rhône-Alpes
303,15 Boulevard Toulouse,Toulouse,31000,Occitanie
304,5 Place de Bordeaux,Bordeaux,33000,Nouvelle-Aquitaine
305,25 Rue de Lille,Lille,59000,Hauts-de-France
306,30 Avenue de Nantes,Nantes,44000,Pays de la Loire
```

---

### 4. `Equipments.csv`
```csv
EquipmentID,EquipmentType,Model,Manufacturer,WarrantyPeriod
401,Chaudière,Ch-1234,ThermoFrance,5 ans
402,Radiateur,Rad-5678,ChaufferPro,3 ans
403,Chaudière,Ch-9876,ThermoFrance,5 ans
404,Radiateur,Rad-4321,EcoHeat,2 ans
405,Radiateur,Rad-8765,ChaufferPro,3 ans
406,Chaudière,Ch-6543,ThermoFrance,4 ans
```

---

### 5. `Technicians.csv`
```csv
TechnicianID,FullName,ExperienceYears,CertificationLevel,Region
101,Jean Dupont,5,Expert,Île-de-France
102,Marie Leclerc,3,Intermédiaire,Auvergne-Rhône-Alpes
103,Thomas Garnier,10,Expert,Occitanie
104,Claire Fontaine,7,Avancé,Nouvelle-Aquitaine
105,Hugo Petit,4,Intermédiaire,Hauts-de-France
106,Laura Vincent,6,Expert,Pays de la Loire
```

---

### 6. `Dates.csv`
```csv
DateID,Date,Month,Year,DayOfWeek
20231101,2023-11-01,Novembre,2023,Mercredi
20231102,2023-11-02,Novembre,2023,Jeudi
20231103,2023-11-03,Novembre,2023,Vendredi
20231104,2023-11-04,Novembre,2023,Samedi
20231105,2023-11-05,Novembre,2023,Dimanche
20231106,2023-11-06,Novembre,2023,Lundi
```

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



