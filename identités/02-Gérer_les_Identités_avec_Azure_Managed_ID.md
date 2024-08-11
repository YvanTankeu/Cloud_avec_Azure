Déployer une Application Web Azure en .NET avec Accès au Key Vault via Identité Managée
=======================================================================================

J'ai un Key Vault dans Azure qui contient mes mots de passe et autres secrets. Je souhaite les lister dans mon application web Azure développée en C# avec .NET. Ce tutoriel vous guidera à travers les étapes pour déployer votre application web sur Azure App Service, configurer une identité managée pour accéder en toute sécurité à votre Key Vault, et afficher les secrets dans votre application web.

- Scénario
  Vous avez une application web en .NET que vous souhaitez déployer sur Azure App Service. Votre application doit accéder à des secrets stockés dans Azure Key Vault, comme des mots de passe ou des clés API, pour les afficher ou les utiliser. Pour garantir la sécurité, vous utiliserez une identité managée, ce qui évite de stocker des informations d'identification sensibles dans votre code.! 

   ![image](https://github.com/user-attachments/assets/005294fb-092f-43ee-af09-58741797d7a5)

Pour suivre le tuto voic les prerequis

  - Créer et déployer une application web sur Azure App Service : Vous devez avoir une application web déjà déployée sur Azure. Si ce n’est pas le cas, suivez les [instructions](https://learn.microsoft.com/fr-fr/azure/key-vault/general/tutorial-net-create-vault-azure-web-app?tabs=azure-cli#create-a-net-core-app) pour créer et déployer une application web sur Azure App Service.

  - Créer une ressource Azure Key Vault et le provisionner de mots de passes : Configurez un Key Vault dans Azure pour stocker vos secrets de manière sécurisée.


1 - Créer une identité managée dans azure pour votre application web

  Dans le portail d'azure, allez sur votre webapp -> Settings -> Identity -> System Assigned -> Switch from "Off" to "On"  et cliquez sur "Save" pour sauvegader 

 ![donneruneidentitealawebapp1](https://github.com/user-attachments/assets/0ea2280e-960b-4e09-9d57-96e3cb9fb955)

 Une fois cela fait on vous demandera si vous voulez activer identité gérée attribuée par le système

 ![donneruneidentitealawebapp2](https://github.com/user-attachments/assets/ed957bab-5681-4e78-83c1-5ba343072663)

 la suite ressemblera a ca

![donneruneidentitealawebapp3](https://github.com/user-attachments/assets/7feec3ec-d8a6-4f3b-b876-71ec3523502f)


  Creez en une identite manage en cliquant sur create comme vous le voyez en image, j'en ai deja cree un au nom de identitePrincipal

  ![image](https://github.com/user-attachments/assets/8e2844de-3e78-429b-aa65-a1e359b51bda)


