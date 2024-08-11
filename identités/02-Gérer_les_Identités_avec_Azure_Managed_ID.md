Déployer une Application Web Azure en .NET avec Accès au Key Vault via Identité Managée
=======================================================================================

J'ai un Key Vault dans Azure qui contient mes mots de passe et autres secrets. Je souhaite les lister dans mon application web Azure développée en C# avec .NET. Ce tutoriel vous guidera à travers les étapes pour déployer votre application web sur Azure App Service, configurer une identité managée pour accéder en toute sécurité à votre Key Vault, et afficher les secrets dans votre application web.

- Scénario
  Vous avez une application web en .NET que vous souhaitez déployer sur Azure App Service. Votre application doit accéder à des secrets stockés dans Azure Key Vault, comme des mots de passe ou des clés API, pour les afficher ou les utiliser. Pour garantir la sécurité, vous utiliserez une identité managée, ce qui évite de stocker des informations d'identification sensibles dans votre code.! 

   ![image](https://github.com/user-attachments/assets/005294fb-092f-43ee-af09-58741797d7a5)

Pour suivre le tuto voic les prerequis

  - Créer et déployer une application web sur Azure App Service : Vous devez avoir une application web déjà déployée sur Azure. Si ce n’est pas le cas, suivez les [instructions](https://learn.microsoft.com/fr-fr/azure/key-vault/general/tutorial-net-create-vault-azure-web-app?tabs=azure-cli#create-a-net-core-app) pour créer et déployer une application web sur Azure App Service.

  - Créer une ressource Azure Key Vault et le provisionner de mots de passes : Configurez un Key Vault dans Azure pour stocker vos secrets de manière sécurisée.

Configurer l’application web pour se connecter au coffre de clés

1 - Créer une identité managée dans azure pour votre application web

  Dans le portail d'azure, allez sur votre webapp -> Settings -> Identity -> System Assigned -> Switch from "Off" to "On"  et cliquez sur "Save" pour sauvegader 

 ![donneruneidentitealawebapp1](https://github.com/user-attachments/assets/0ea2280e-960b-4e09-9d57-96e3cb9fb955)

 Une fois cela fait on vous demandera si vous voulez activer identité gérée attribuée par le système

 ![donneruneidentitealawebapp2](https://github.com/user-attachments/assets/ed957bab-5681-4e78-83c1-5ba343072663)

 la suite ressemblera a ca avec une ID d’objet : objet de principal de service de l’identité managée.

![donneruneidentitealawebapp3](https://github.com/user-attachments/assets/7feec3ec-d8a6-4f3b-b876-71ec3523502f)


2 - Attribuer l’accès à une identité managée a votre application web

  Pour permettre à votre application web d'accéder aux secrets dans Azure Key Vault, vous devez lui accorder les autorisations nécessaires via le contrôle d'accès en fonction du rôle (RBAC).

  Dans la ressource web application, allez dans Acces Control(IAM)  

  ![role1](https://github.com/user-attachments/assets/238b548c-588a-4fc9-8299-106f801e8d8e)

  -> Add role assignment

  ![role2](https://github.com/user-attachments/assets/daa54502-f887-46fd-8415-bc935e2026c3)

  -> Dans job function roles, entrez le role "Key Vault Secrets User" et puis Next

  ![15](https://github.com/user-attachments/assets/a86c0fa5-9a58-435b-93de-d05620fe8c6c)

  -> Cliquez dans "Managed identify" et puis "Select Members"

  ![16](https://github.com/user-attachments/assets/0402581f-ad7c-4d26-b236-4d7a9dfabda3)

  -> Dans cette fenêtre, choisissez votre abonnement de webapp  dans "Select Members"

  ![7](https://github.com/user-attachments/assets/ab76d28e-11e9-496f-ac31-d99924043487)

  -> Selectionnez votre identiy manage de tout a lheure

  ![8](https://github.com/user-attachments/assets/94c44528-f452-4fc1-b920-4031b3929875)

  -> Choisir le membre, qui est votre appliction web et cliquez sur select une fois fait
  
  ![9](https://github.com/user-attachments/assets/3732d0f2-ef6c-4afd-9040-0f1a9b566e8f)



  




 





