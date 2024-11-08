### **Sujet : Optimisation de la Transition Énergétique et Maintenance Préventive chez GRDF**

---

#### **Contexte**
Dans le cadre de ses engagements pour la transition énergétique, GRDF souhaite analyser ses données pour :
- Optimiser les interventions sur les équipements écologiques.
- Améliorer la maintenance préventive.
- Suivre l'impact des subventions sur l'adoption des équipements et les réductions d'émissions de CO₂.

L’objectif est de modéliser les données disponibles, d’utiliser des outils d’analyse pour répondre à des besoins métier précis, et de fournir des visualisations claires et interactives.

---

### **Objectifs**
1. **Modélisation des Données** :
   - Structurer les données en un modèle logique en étoile.
   - Établir les relations entre les tables pour permettre une analyse cohérente.
   - Tenir compte des itérations possibles, car certaines données peuvent être ajoutées ou enrichies au fil du temps (par exemple, interventions futures, nouvelles subventions).

2. **Analyse des Données** :
   - Calculer des indicateurs de performance tels que les économies d’énergie, la réduction des émissions de CO₂, et les coûts des interventions.
   - Comprendre les tendances temporelles et identifier les zones à améliorer.
   - Analyser l’impact des subventions sur l’adoption des équipements écologiques.

3. **Rapports et Visualisations** :
   - Créer des tableaux de bord pour visualiser les performances régionales, l’efficacité des techniciens, et l’impact environnemental.
   - Utiliser des slicers pour interagir avec les données (par exemple, filtrer par région, équipement, ou période).
   - Ajouter des visualisations spécifiques pour explorer les équipements nécessitant une attention particulière.

4. **Suivi en Itération** :
   - Prévoir que les fichiers de données (par exemple, `Interventions.csv`, `Subventions.csv`) pourront être mis à jour ou enrichis.
   - Adapter la structure pour permettre une intégration fluide des nouvelles données.

---

### **Étapes**

#### **Étape 1 : Modélisation des Données**
- Identifier les tables nécessaires :
  - Interventions (IDIntervention, Type, CO₂ réduit, coût total, durée, etc.).
  - Équipements (type, modèle, fabricant, consommation énergétique, etc.).
  - Régions (nom, politique écologique, population, etc.).
  - Subventions (type, montant, conditions, etc.).
  - Dates (jours, mois, trimestres, années).
  - Techniciens (nom, certifications, expérience).
- Établir les relations entre ces tables.
- Prévoir une gestion souple pour intégrer des ajouts futurs dans les fichiers, tels que :
  - Nouvelles interventions réalisées.
  - Modifications des montants des subventions.

---

#### **Étape 2 : Analyse des Données**
- Identifier les zones prioritaires :
  - Analyse régionale : performances écologiques et économiques par région.
  - Mesure Dax
```DAX
ReductionTotalCo2 = SUM(Interventions[Reduction_CO2])
CoutTotalInterventions = SUM(Interventions[Coût_Total])
CoutInterventionsSubventionnées = CALCULATE([CoutTotalInterventions], NOT(ISBLANK(Interventions[ID_Subvention])))
```
  - Analyse des équipements : types d’équipements les plus efficaces.
  ```DAX
  CoutMoyen = AVERAGEX(RELATEDTABLE(Interventions), Interventions[Coût_Total])
  ```
  - Analyse des techniciens : techniciens les plus performants en termes de réduction des émissions.
  ```DAX
   InterventionsParTechnicien = COUNTROWS(Filter(Interventions, Interventions[ID_Technicien] = Techniciens[ID_Technicien]))
  ```
- Mettre en place des indicateurs pour :
  - Mesurer l’évolution des installations écologiques.
  - Comparer les coûts des interventions préventives et correctives.
  - Évaluer les impacts des subventions.

---

#### **Étape 3 : Rapports et Visualisations**
1. **Vue d’Ensemble** :
   - Réduction totale des émissions de CO₂.
   - Coût total des interventions.
   - Croissance des installations écologiques.

2. **Analyse Régionale** :
   - Répartition des équipements écologiques par région.
   - Comparaison des performances régionales.

3. **Performance des Techniciens** :
   - Nombre d’interventions par technicien.
   - Réductions de CO₂ par technicien.

4. **Cartographie** :
   - Carte géographique des régions les plus actives.
   - Analyse visuelle des subventions et de leur impact.

---

### **Consignes Spéciales**
1. **Fichiers Itératifs** :
   - Les fichiers peuvent être mis à jour de manière itérative avec de nouvelles données.
   - Préparez le modèle et les rapports pour intégrer facilement des ajouts, comme :
     - De nouvelles interventions dans `Interventions.csv`.
     - Des ajustements dans les subventions disponibles dans `Subventions.csv`.

2. **Adaptabilité** :
   - Les visualisations et les mesures doivent rester dynamiques pour s’adapter aux ajouts futurs.
   - Privilégiez des formules et des relations génériques pour éviter les ajustements manuels à chaque ajout de données.

---

### **Questions à Explorer**
1. Quelles régions enregistrent les meilleures performances écologiques ?
2. Quels types d’équipements génèrent les économies d’énergie les plus importantes ?
3. Comment les subventions influencent-elles la transition énergétique ?
4. Quels techniciens ont les meilleures performances pour la réduction des émissions ?
5. Quels équipements ou régions nécessitent une attention particulière pour améliorer les performances ?
