### **Exercice Avancé : Analyse des Interventions avec DAX**

---

#### **Contexte**
GRDF souhaite exploiter les données d'interventions pour obtenir des analyses détaillées sur les performances des techniciens, le coût des interventions et les tendances temporelles. Vous allez utiliser les données déjà modélisées pour répondre à des besoins métiers précis en créant des mesures DAX simples et avancées, des visualisations interactives, et en analysant les résultats.

---

### **Objectifs**
1. **Mesures simples** : Créez des mesures de base comme les totaux, moyennes et nombres.
2. **Mesures conditionnelles** : Répondez à des scénarios spécifiques en utilisant des conditions.
3. **Analyses temporelles** : Effectuez des calculs basés sur les périodes (mois, années).
4. **Analyse des performances** : Identifiez les techniciens et régions les plus performants.
5. **Création de tables virtuelles** : Exploitez des résumés ou classements pour des analyses spécifiques.
6. **Visualisations interactives** : Configurez des rapports visuels pour explorer les données et répondre aux questions métiers.

---

### **Étapes**

#### **Étape 1 : Créer des Mesures Simples**
- Calculez le coût total des interventions.
- Calculez la durée moyenne des interventions.
- Déterminez le nombre total d'interventions.

#### **Étape 2 : Mesures Conditionnelles**
- Calculez le coût moyen par type d’équipement.
- Créez une mesure pour filtrer et calculer le coût total des interventions n'excédant pas un certain montant.
- Ajoutez une mesure conditionnelle pour analyser le coût total des interventions dans une région spécifique.

#### **Étape 3 : Calculs Temporels**
- Analysez le coût total des interventions pour le mois en cours.
- Calculez la croissance des coûts d'un mois à l'autre pour analyser les tendances.

#### **Étape 4 : Analyse des Performances**
- Mesurez le nombre d’interventions effectuées par chaque technicien.
- Analysez le coût total des interventions réalisées par chaque technicien.
- Identifiez les techniciens les plus performants en termes de coût moyen par intervention.

#### **Étape 5 : Tables Virtuelles**
- Créez une table virtuelle pour afficher le top 5 des régions avec le coût total d’interventions le plus élevé.
- Analysez les types d’équipements les plus fréquents en termes de nombre d'interventions.

#### **Étape 6 : Visualisations Interactives**
1. Configurez une **matrice** regroupant les données :
   - Lignes : Régions.
   - Colonnes : Types d’équipements.
   - Valeurs : Coût total, nombre d’interventions.

2. Créez un **graphique en barres** :
   - Axe X : Nom des techniciens.
   - Valeurs : Coût total par technicien, nombre d’interventions par technicien.

3. Configurez un **graphique en ligne** pour analyser les tendances :
   - Axe X : Mois.
   - Valeurs : Coût total des interventions, croissance des coûts mois sur mois.

4. Ajoutez une **carte géographique** :
   - Lieux : Ville (table `Addresses`).
   - Valeurs : Coût total par ville.

5. Intégrez des **slicers** interactifs :
   - Région.
   - Type d’équipement.
   - Nom du technicien.

---

### **Questions Métier**
1. Quelle région a enregistré le coût total le plus élevé pour les chaudières ?
2. Quel technicien a la meilleure performance en termes de coût moyen par intervention ?
3. Quelle est la croissance des coûts mois sur mois pour le mois de novembre ?
4. Quels sont les 5 types d'équipement les plus courants en termes de nombre d'interventions ?
5. Quelle région représente le pourcentage le plus élevé du coût total des interventions ?


### **Critères d’Évaluation**
1. **Utilisation de DAX** :
   - Mesures simples et avancées correctement mises en œuvre.
   - Pertinence des mesures pour répondre aux besoins métiers.

2. **Rapport Visuel** :
   - Les visualisations sont interactives et faciles à comprendre.
   - Les slicers permettent une exploration fluide des données.

3. **Analyse** :
   - Les réponses aux questions métiers sont précises et basées sur des analyses DAX.
