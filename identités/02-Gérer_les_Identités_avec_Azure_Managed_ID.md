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
  
  ![9](https://github.com/user-attachments/assets/0d394662-de95-4779-b0d9-f7917857181a)


3 - Creez des secrets dans azure Key Vault

  Pour acceder a nos secrets, il va falloir que ceux-ci existent, alors nous devons creer nos secrets.

  La ressource Kyevault qui a ete creer dans les prerequis, on doit l'acceder pour creer nos secrets qui sont consideres comme des mots de passe.

  Dans Keyvault -> Objects -> Secrets, vous verrez la liste des secrets que jai creee tres facilelemt

  ![keyvault1](https://github.com/user-attachments/assets/70b41271-6ee5-41cd-92ab-10b873577643)

  Pour en creer, vous devez cliquer sur

  -> sur "Generat/Import"

  ![keyvault2](https://github.com/user-attachments/assets/772c6ad0-201f-4260-a736-39605bff50aa)

  -> la fenêtre de creation apparait, entrez le nom et la valeur de votre secret et par la suite cliquez sur "Create"

  ![keyvault3](https://github.com/user-attachments/assets/28fb5876-4266-47aa-8af0-a284e4c15121)


4 - Acceder aux secrets via notre application web

Voici le code que jai utilise pour acceder au secrets via l'application web

    using Azure;
    using Azure.Identity;
    using Azure.Security.KeyVault.Secrets;
    using Azure.Core;
    using Microsoft.AspNetCore.Builder;
    using Microsoft.Extensions.DependencyInjection;
    
    var builder = WebApplication.CreateBuilder(args);
    var app = builder.Build();
    
    // Configuration des options du client
    SecretClientOptions options = new SecretClientOptions()
    {
        Retry =
        {
            Delay = TimeSpan.FromSeconds(2),
            MaxDelay = TimeSpan.FromSeconds(16),
            MaxRetries = 5,
            Mode = RetryMode.Exponential
        }
    };
    
    // Créez un client pour accéder au Key Vault
    var client = new SecretClient(new Uri("https://<your-unique-key-vault-name>.vault.azure.net/"), new DefaultAzureCredential(), options);
    
    // Route pour récupérer et afficher tous les secrets
    app.MapGet("/", async () =>
    {
        var secretValues = new List<string>();
    
        // Récupérez les propriétés de tous les secrets
        await foreach (var secretProperties in client.GetPropertiesOfSecretsAsync())
        {
            try
            {
                // Récupérez chaque secret par son nom
                KeyVaultSecret secret = await client.GetSecretAsync(secretProperties.Name);
                secretValues.Add($"{secretProperties.Name}: {secret.Value}");
            }
            catch (RequestFailedException ex)
            {
                // Gestion des erreurs éventuelles lors de la récupération d'un secret
                secretValues.Add($"Erreur pour {secretProperties.Name}: {ex.Message}");
            }
        }
    
        // Retournez les secrets comme une chaîne formatée
        return string.Join("\n", secretValues);
    });
    
    app.Run();

pour un resulat incroyable

![keyvault4](https://github.com/user-attachments/assets/5ed145cc-0723-4095-84f5-2a67b73f72d4)







 





