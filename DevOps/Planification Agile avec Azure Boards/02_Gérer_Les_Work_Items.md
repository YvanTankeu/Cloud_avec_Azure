# **Gestion des éléments de travail (Work Items)**  


Dans Azure DevOps, un Work Item représente une tâche, une fonctionnalité, un bug, une user story, une épic, etc. Il permet d’organiser et de structurer le travail au sein d’un projet Agile ou Scrum.  

Dans ce contexte, nous allons utiliser les Work Items pour planifier l’optimisation de la recherche des tutoriels les plus récents sur la plateforme **eShopOnWeb**, en améliorant la rapidité et la pertinence des résultats affichés.  

---

## **Étape 1 : Créer un Work Item "Epic"**  

Un Epic est un gros projet ou une grande amélioration à faire. Il regroupe plusieurs fonctionnalités.

1. Dans la barre latérale des menus, sélectionnez **Work Items**, puis cliquez sur **New Work Item** et choisissez **Epic**.  
   
   ![image](https://github.com/user-attachments/assets/f75ae2d7-9662-483b-9f63-af5c566a04b6)  

2. Dans la fenêtre du nouvel Epic, remplissez les champs suivants :  
   - **Nom** : *Optimisation de la recherche des tutoriels récents*  
   - **Assigné à** : Sélectionnez la personne responsable  
   - **Zone** : Par exemple, *Team web* pour l'equipe en charge  
   - **Itération** : Sprint en cours, comme *Sprint 1* ou *Sprint 2*  
   - **Description** : Ajoutez une explication détaillée des objectifs de cet Epic  
   
   Cliquez sur **Save** pour enregistrer.  
   
   ![image](https://github.com/user-attachments/assets/09638c1c-ceca-47ac-865f-6bf8eedf5393)  

---

## **Étape 2 : Créer un Work Item "Feature"**  

Feature: Une fonctionnalité importante qui fait partie d'un Epic.

3. Ajoutez un **Feature** sous l'Epic "Optimisation de la recherche des tutoriels récents". Ce Feature représentera une **amélioration clé** de la recherche.  

   Pour cela, allez dans **Related Work > Add link > New Item**.  
   
   ![image](https://github.com/user-attachments/assets/8ab834b8-dd2c-4309-a34b-1ea7a61e36fa)  

4. Dans la fenêtre **New Item** :  
   - **Type de lien** : Sélectionnez **Child** pour rattacher ce Feature à l'Epic  
   - **Work Item Type** : **Feature**  
   - **Titre** : *Optimisation des performances de recherche*  
   - **Save and Close** une fois complété  
   
   ![image](https://github.com/user-attachments/assets/dc9bbea8-5a0b-465c-a355-c1280b24b701)  

---

## **Étape 3 : Créer un Work Item "Product Backlog Item"** 

Product Backlog Item (PBI) : Une tâche ou une amélioration à faire pour une Feature.

5. Ajoutez un **Product Backlog Item (PBI)** pour détailler des aspects spécifiques de l’optimisation, par exemple :  

   Pour cela, allez dans la page du Work Item **Optimisation des performances de recherche**, cliquez sur **Add link > New Link**, sélectionnez **Product Backlog Item**, puis **Save and Close**.  
   
   ![image](https://github.com/user-attachments/assets/f9c6643a-8641-4eb4-b269-82ce524ab7ab)  

---

## **Étape 4 : Créer un Work Item "Task"** 

Task : Une action précise à réaliser pour terminer un PBI.

6. Définissez des **Tasks** pour attribuer des tâches précises aux membres de l’équipe, par exemple :  

   Pour cela, allez dans la page du **Product Backlog Item**, cliquez sur **Add link > New Link**, sélectionnez **Task**, donnez un titre et enregistrez.  
   
   ![image](https://github.com/user-attachments/assets/bc960db9-2138-4a7b-9e7a-8a06c443bee2)

## FIN

Voici la hiérarchie des work items que tu as créés :

- **Epic : Formation sur les produits**  
   - **Feature : Tableau de bord de la formation**  
     - **Product Backlog Item (PBI) :** En tant que client, je veux voir les nouveaux tutoriels  
       - **Task :** Ajouter une page pour les tutoriels les plus récents  
       - **Task :** Optimiser la recherche de données pour les tutoriels les plus récents  
     - **Product Backlog Item (PBI) :** En tant que client, je souhaite demander de nouveaux tutoriels  
     - **Product Backlog Item (PBI) :** En tant que client, je veux voir les tutoriels que j'ai récemment visionnés  

![image](https://github.com/user-attachments/assets/50c7b734-1ba4-4be8-8250-50c4a29e4d0a)




  
