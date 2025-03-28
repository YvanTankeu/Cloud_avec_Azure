# Exercice : Governance Solution Design

[Consulter l'étude de cas ici](https://microsoftlearning.github.io/AZ-305-DesigningMicrosoftAzureInfrastructureSolutions/Instructions/CaseStudy/01-Governance.html)

---

## **Questions de l'étude de cas :**
![image](https://github.com/user-attachments/assets/443263b3-c847-4522-8987-7804ad9c60ae)

---

## **1. Cost and Accounting**

### **Question :**
**What are different ways Tailwind Traders could organize their subscriptions and management groups? Which would be the best to meet their requirements?**

### **My Solution :**
![Solution Diagram](https://github.com/user-attachments/assets/e419c98c-bd28-469a-92e9-5bef4a4a2a25)

---

## **2. New Development Project**

### **Question 1 :**
**What are the different ways Tailwind Traders could track costs for the new development project?**

### **Réponse :**
1. **Tags sur les ressources** : 
   - Ajouter un tag comme **`cost_new_dev=newR`** à toutes les ressources liées au projet.
   - Les tags permettent une analyse détaillée des coûts via Azure Cost Management.
2. **Resource Group dédié** : 
   - Créer un groupe de ressources spécifiquement pour le projet de développement.
   - Mettre uniquement les ressources associées à ce projet dans ce groupe, ce qui facilite leur gestion.

---

### **Question 2 :**
**How are you ensuring compliance with the requirements for virtual machine sizing and naming?**

### **Réponse :**
- Utiliser les **Azure Policy** au niveau du **Management Group Tailwind Traders** pour imposer :
  1. Des restrictions sur les tailles des machines virtuelles autorisées (par exemple, séries B pour des coûts réduits).
  2. Un schéma de nommage spécifique des ressources.

### **My Solution :**
![Solution Diagram](https://github.com/user-attachments/assets/9438b687-9637-4e82-8c50-757ffe176b72)

---

### **Question 3 :**
**Propose at least two ways of meeting the requirements. Explain your final decision.**

### **Réponse :**
1. **Approche avec les Tags** :
   - Ajouter des tags pour catégoriser et analyser toutes les ressources associées au projet.
   - Avantage : Facilité d’analyse avec **Azure Cost Management** et flexibilité.
2. **Approche avec Resource Group dédié** :
   - Isoler toutes les ressources du projet dans un seul Resource Group.
   - Avantage : Organisation centralisée et visibilité claire des coûts.

**Final Decision :**
- Combinaison des deux approches : **Tags** pour une flexibilité d'analyse, et un **Resource Group dédié** pour une gestion centralisée des ressources.

---
