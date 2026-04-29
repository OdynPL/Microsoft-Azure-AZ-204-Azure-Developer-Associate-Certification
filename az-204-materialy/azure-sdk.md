# Azure SDK for .NET
---

[Prev: Azure with Docker](azure-with-docker.md)

**Definicja:**
- **Azure SDK for .NET** – zestaw oficjalnych bibliotek do pracy z usługami Azure w aplikacjach .NET.
- Umożliwia zarządzanie zasobami, dostęp do danych, autoryzację, monitorowanie, integrację z usługami PaaS/SaaS.

## Znaczenie na egzaminie AZ-204
- Wymagana znajomość najważniejszych bibliotek, wzorców autoryzacji, obsługi błędów, asynchroniczności.
- Często pytania o wybór SDK, różnice między management/data, obsługę poświadczeń.

## Kluczowe biblioteki i ich zastosowanie

| Biblioteka                                 | Przeznaczenie                        | Przykład użycia                                      |
|--------------------------------------------|--------------------------------------|------------------------------------------------------|
| Azure.Identity                             | Autoryzacja, DefaultAzureCredential  | Autoryzacja do Key Vault, Storage, Service Bus       |
| Azure.Storage.Blobs                        | Praca z Blob Storage                 | Upload/download plików, zarządzanie kontenerami      |
| Azure.Data.Tables                          | Praca z Table Storage                | CRUD na tabelach, batch, filtrowanie                 |
| Azure.Messaging.ServiceBus                 | Kolejki i topiki Service Bus         | Wysyłanie/odbiór wiadomości, sesje, dead-letter      |
| Azure.Messaging.EventHubs                  | Event Hub                            | Wysyłanie/odbiór zdarzeń, checkpointing              |
| Azure.Security.KeyVault.Secrets            | Sekrety w Key Vault                  | Pobieranie/zapisywanie sekretów                      |
| Azure.Security.KeyVault.Keys               | Klucze w Key Vault                   | Operacje kryptograficzne, zarządzanie kluczami       |
| Azure.Security.KeyVault.Certificates       | Certyfikaty w Key Vault              | Zarządzanie certyfikatami, auto-rotacja              |
| Azure.Monitor.Query                        | Log Analytics, KQL                   | Zapytania do logów, analiza metryk                   |
| Azure.ResourceManager.*                    | Zarządzanie zasobami (ARM)           | Tworzenie, modyfikacja, usuwanie zasobów             |
| Azure.Messaging.WebPubSub                  | Komunikacja WebSocket                | Real-time messaging, broadcast, grupy                |
| Azure.Messaging.SignalR                    | SignalR Service                      | Real-time messaging, autoryzacja, grupy              |
| Azure.AI.TextAnalytics, Azure.AI.Vision    | Cognitive Services                   | Analiza tekstu, obrazów, AI                          |
| Azure.Containers.ContainerRegistry         | Azure Container Registry (ACR)        | Zarządzanie repozytoriami, obrazami                  |
| Azure.Identity.ClientSecretCredential      | Uwierzytelnianie przez client secret | Scenariusze serwisowe, automatyzacja                 |

## Przypadki użycia
- Pobieranie sekretu z Key Vault przez DefaultAzureCredential
- Upload pliku do Blob Storage z autoryzacją przez Managed Identity
- Wysyłanie wiadomości do Service Bus z obsługą retry
- Zapytania KQL do Log Analytics
- Zarządzanie zasobami przez Azure.ResourceManager
- Integracja z Cognitive Services (analiza tekstu, obrazów)
- Praca z ACR (listowanie, usuwanie obrazów)

## Przykład kodu C# (.NET 8)
```csharp
// Pobieranie sekretu z Key Vault
var client = new SecretClient(new Uri("https://myvault.vault.azure.net/"), new DefaultAzureCredential());
KeyVaultSecret secret = await client.GetSecretAsync("MySecret");

// Upload pliku do Blob Storage
var blobClient = new BlobClient(new Uri("https://myaccount.blob.core.windows.net/mycontainer/myfile.txt"), new DefaultAzureCredential());
await blobClient.UploadAsync("plik.txt");

// Wysyłanie wiadomości do Service Bus
var sender = new ServiceBusClient("<connection-string>").CreateSender("myqueue");
await sender.SendMessageAsync(new ServiceBusMessage("Hello AZ-204!"));
```

## Wskazówki egzaminacyjne
- Zawsze używaj DefaultAzureCredential jeśli to możliwe (obsługuje Managed Identity, Visual Studio, CLI).
- Rozróżniaj SDK management (Azure.ResourceManager) i data (np. Azure.Storage.Blobs).
- Obsługuj błędy (try/catch, retry policy).
- Preferuj async/await.
- Sprawdzaj wersje bibliotek – na egzaminie wymagane są najnowsze (track2).
