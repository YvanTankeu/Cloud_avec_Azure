# **Exercice : Design Authentication and Authorization Solutions**

[Consulter l'étude de cas ici](https://microsoftlearning.github.io/AZ-305-DesigningMicrosoftAzureInfrastructureSolutions/Instructions/CaseStudy/07-Access.html)

---

## **1. New User Accounts**

### **Processus pour l’intégration des comptes d’utilisateur de l’acquisition**
1. **Synchronisation des comptes on-premises avec Entra ID** :
   - Utilisation d'Entra Connect pour synchroniser les identités on-premises des 75 nouveaux employés vers Entra ID.
   - Mise en place d'une synchronisation hybride pour assurer une gestion centralisée des identités.
     
   ![image](https://github.com/user-attachments/assets/5eaeb0b4-9a02-48c5-a6ec-86f6b93f2e58)

### **Processus pour l’ajout des comptes partenaires**
1. **Utilisation des identités B2B d’Entra** :
   - Inviter les 15 employés du partenaire en tant qu’utilisateurs invités via Azure AD B2B (Business-to-Business).
   - Configurer des politiques d'accès conditionnel spécifiques à ces utilisateurs pour limiter leur portée d’accès.

   ![image](https://github.com/user-attachments/assets/227049cb-8ce1-437c-a8f4-cfe5569d8741)

2. **Étapes spécifiques** :
   - Étape 1 : Créer une invitation B2B pour les utilisateurs externes.
   - Étape 2 : Assigner des rôles et permissions basés sur leurs responsabilités.
   - Étape 3 : Configurer l'accès conditionnel pour s'assurer que seules des connexions sécurisées sont autorisées.


### **Avantages** :
1. Centralisation des identités pour simplifier la gestion.
2. Sécurisation de l'accès des utilisateurs partenaires grâce à des politiques granulaires.
3. Optimisation de la conformité grâce à une approche basée sur les rôles et les responsabilités.

---

## **2. Recommendations pour l’amélioration des solutions d’identité**

### **Recommandations :**
1. **Implémenter des politiques d'accès conditionnel avancées** :
   - Importance : Renforce la sécurité en basant l'accès sur des conditions telles que l'emplacement ou le type d'appareil.
   - Justification : Protège contre les menaces provenant d'appareils compromis.

2. **Adopter l’authentification sans mot de passe** :
   - Importance : Réduit les risques liés au phishing et améliore l'expérience utilisateur.
   - Justification : L’utilisation de Windows Hello ou des clés FIDO2 offre une sécurité supérieure.

3. **Mettre en œuvre la rotation automatique des secrets avec Azure Key Vault** :
   - Importance : Garantit que les secrets comme les mots de passe ne deviennent pas obsolètes ou compromis.
   - Justification : Réduit les risques de violations liées à une mauvaise gestion des secrets.

---

## **3. New Application Access**

### **Accès pour l’application de développement commercial**
1. **Utilisation des identités managées** :
   - Créer une identité managée pour la VM.
   - Configurer l'accès au SQL Azure Database via RBAC.

2. **Étapes spécifiques** :
   - Étape 1 : Activer une identité managée pour la VM.
   - Étape 2 : Assigner un rôle RBAC approprié (ex. Lecteur de données SQL).
   - Étape 3 : Configurer l’application pour utiliser l'identité.

### **Accès pour les ressources on-premises**

   - Utiliser AAD Proxy pour creer un compte de service dans azure pour cette application On promise.


Schema final

![image](https://github.com/user-attachments/assets/601c9990-3a98-400a-a8c4-0710eac751ee)


