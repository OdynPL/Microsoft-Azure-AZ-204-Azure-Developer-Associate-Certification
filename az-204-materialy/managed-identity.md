
# Azure Managed Identity

- Automatyczne zarządzanie tożsamością dla zasobów Azure (np. App Service, VM, Functions, Logic Apps).
- Umożliwia uwierzytelnianie do usług Azure bez przechowywania haseł, certyfikatów, secretów.
- Integracja z Key Vault, Storage, SQL Database, Service Bus, Event Hubs, Cosmos DB i innymi.

## Znaczenie na AZ-204
- Pozwala na bezpieczne uwierzytelnianie aplikacji w Azure.
- Eliminuje konieczność zarządzania poświadczeniami w kodzie.
- Wspiera automatyzację, DevOps, CI/CD.

## Kluczowe pojęcia
- **System-assigned Managed Identity**: tożsamość przypisana do konkretnego zasobu (np. App Service), tworzona i usuwana razem z zasobem.
- **User-assigned Managed Identity**: tożsamość tworzona niezależnie, może być przypisana do wielu zasobów.
- **Azure AD Token**: token JWT wydawany dla Managed Identity, używany do uwierzytelniania w innych usługach.
- **DefaultAzureCredential**: klasa w Azure SDK, automatycznie wykrywa i używa Managed Identity w środowisku Azure.
- **Role Assignment**: przypisanie roli (np. Reader, Contributor) Managed Identity do zasobu docelowego.
- **MSI_ENDPOINT/MSI_SECRET**: zmienne środowiskowe używane przez SDK do komunikacji z usługą Managed Identity.

## Scenariusze egzaminacyjne
- Uwierzytelnianie aplikacji .NET do Key Vault, Storage, SQL Database przez Managed Identity.
- Przypisanie roli Managed Identity do zasobu (np. Key Vault Secrets User).
- Różnica między system-assigned a user-assigned identity.
- Użycie DefaultAzureCredential w kodzie .NET.
- Diagnostyka błędów uprawnień (brak roli, brak tożsamości).

## Przykład użycia w C# (.NET 8)

### 1. Odczyt sekretu z Key Vault przez Managed Identity
```csharp
using Azure.Identity;
using Azure.Security.KeyVault.Secrets;

var credential = new DefaultAzureCredential();
var client = new SecretClient(new Uri("https://myvault.vault.azure.net/"), credential);
KeyVaultSecret secret = await client.GetSecretAsync("MySecret");
Console.WriteLine(secret.Value);
```

### 2. Odczyt pliku z Azure Storage przez Managed Identity
```csharp
using Azure.Identity;
using Azure.Storage.Blobs;

var credential = new DefaultAzureCredential();
var blobClient = new BlobClient(new Uri("https://myaccount.blob.core.windows.net/container/file.txt"), credential);
var response = await blobClient.DownloadContentAsync();
Console.WriteLine(response.Value.Content.ToString());
```

### 3. Połączenie z Azure SQL Database przez Managed Identity
```csharp
using Azure.Identity;
using Microsoft.Data.SqlClient;

var connection = new SqlConnection(
		new SqlConnectionStringBuilder
		{
				DataSource = "myserver.database.windows.net",
				InitialCatalog = "mydb",
				Authentication = SqlAuthenticationMethod.ActiveDirectoryManagedIdentity
		}.ConnectionString);
await connection.OpenAsync();
```

### 4. Odbiór wiadomości z Service Bus przez Managed Identity
```csharp
using Azure.Identity;
using Azure.Messaging.ServiceBus;

var credential = new DefaultAzureCredential();
var client = new ServiceBusClient("<namespace>.servicebus.windows.net", credential);
var receiver = client.CreateReceiver("myqueue");
ServiceBusReceivedMessage message = await receiver.ReceiveMessageAsync();
Console.WriteLine(message.Body.ToString());
```

## Komendy
- Włączenie system-assigned identity:
	`az webapp identity assign --name myapp --resource-group rg`
- Tworzenie user-assigned identity:
	`az identity create --name myidentity --resource-group rg`
- Przypisanie roli do identity:
	`az role assignment create --assignee <identityId> --role "Key Vault Secrets User" --scope <resourceId>`

## Wskazówka egzaminacyjna
- Managed Identity nie działa poza Azure (np. lokalnie DefaultAzureCredential użyje innego mechanizmu).
- Najczęstszy błąd: brak przypisanej roli do zasobu docelowego.
- System-assigned identity jest usuwana razem z zasobem, user-assigned może być współdzielona.
- Diagnostyka: sprawdź uprawnienia i czy tożsamość jest włączona.

---

[Prev: Logic Apps](logic-apps.md) | [Next: Monitor](monitor.md)
