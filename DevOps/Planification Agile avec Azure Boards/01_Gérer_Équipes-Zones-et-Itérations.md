# Gestion des Équipes des zones et des iterations dans Azure Boards

## Ajout d'une équipe à un projet dans Azure Boards

Azure Boards permet d’organiser le travail en équipes distinctes au sein d’un projet. Chaque équipe peut avoir ses propres itérations, zones et configurations. Voici comment ajouter une équipe :

### Étape 1 : Accéder aux paramètres du projet
1. Ouvrez **Azure DevOps** et accédez à votre projet.
   ![image](https://github.com/user-attachments/assets/222bcc26-42de-4be9-afc0-5e355c3dfae3)

2. Cliquez sur **Project Settings** (Paramètres du projet).
   ![image](https://github.com/user-attachments/assets/7bffd525-d710-4335-85f5-74a0c7a92891)

4. Dans le menu latéral, sélectionnez **Teams**.
   ![image](https://github.com/user-attachments/assets/dd46404a-15e3-41a4-b629-701b9fb34f61)


### Étape 2 : Créer une nouvelle équipe
1. Cliquez sur **New Team** (Nouvelle équipe).
   ![image](https://github.com/user-attachments/assets/21b72192-d85a-4fb8-ae74-4f45f9c833c5)

   
3. Renseignez les informations suivantes :
   - **Nom de l’équipe** : Choisissez un nom pertinent pour votre équipe.
   - **Membres** : Ajoutez les utilisateurs qui feront partie de cette équipe.
   - **Description** *(optionnel)* : Fournissez une description de l’équipe.
   - **Administrateur de l’équipe** *(optionnel)* : Désignez un administrateur si nécessaire.
   - **Permissions** : Configurez les autorisations pour l’administrateur et les membres.
     ![Teams_4](https://github.com/user-attachments/assets/55b5804c-db5c-482d-a8d6-89eb73fd8f0a)

4. Cliquez sur **Create** pour valider la création de l’équipe.

### Étape 3 : Configuration des itérations (Sprints) et des zones

Une fois dans l'équipe **The EShop team**, cliquez sur **Iterations and Area Paths** pour configurer les itérations et les zones propres à cette équipe.

![image](https://github.com/user-attachments/assets/6bb40d98-733e-4ee3-87c1-b1484af45cb7)

#### Assigner des **itérations** à l'équipe

1. Accédez à l'onglet **General** du menu **Boards**, puis cliquez sur **Iterations**.
   
   ![image](https://github.com/user-attachments/assets/ff75732c-17f0-4d05-88aa-6c1d0cb0449b)

2. Cliquez sur **+ Select Iteration(s)** pour créer de nouvelles itérations (Sprints).
   
  ![image](https://github.com/user-attachments/assets/2b0dc1bb-b1a6-46a8-a6a8-2e4f0b536078)


3. Sélectionnez **Sprint 1** et cliquez sur **Save and Close**.
   
   ![image](https://github.com/user-attachments/assets/9e51048a-da6c-45e2-8443-67a38ab46673)

4. Modifiez l'itération en cliquant sur **Edit**.
   
   ![image](https://github.com/user-attachments/assets/09d569e6-5ae8-450f-8c0d-ce5d70d3df4f)

5. Remplissez les détails de l'itération :
   - **Iteration name** (Nom de l'itération)
   - **Start date** (Date de début)
   - **End date** (Date de fin)
   - **Location** (Projet auquel l'itération appartient)
   
   ![image](https://github.com/user-attachments/assets/7d081bfb-3c11-4b11-9a22-314a22c6c61a)

6. Répétez ces étapes pour créer **Sprint 2** et **Sprint 3**.

#### Assigner un **Area Path** à l'équipe

1. Dans le même panneau de configuration (**Project Settings > Boards > Team Configuration**), accédez à l'onglet **Areas**.
   
   ![image](https://github.com/user-attachments/assets/a1f061cc-4cb8-4b23-abaf-81ff3adfe164)


2. Cliquez sur l'icône **(...)** à côté de la zone par défaut et sélectionnez **Include sub-areas**.
   
   ![image](https://github.com/user-attachments/assets/38566239-9053-4463-846f-387acd977b78)

> **Remarque :** Par défaut, toutes les équipes excluent les sous-zones. En activant cette option, l'équipe pourra voir tous les éléments de travail des sous-équipes. Si cette option est désactivée, les éléments assignés à d'autres équipes seront retirés automatiquement de leur vue.
