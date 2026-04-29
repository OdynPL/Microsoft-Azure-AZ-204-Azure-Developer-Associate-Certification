# Azure Notification Hubs
---

[Prev: Azure Static Web Apps](static-web-apps.md) | [Next: Azure Cognitive Services](cognitive-services.md)

**Definicja:**
- Usługa do wysyłania powiadomień push do aplikacji mobilnych (Android/iOS).

**Znaczenie na egzaminie AZ-204:**
- Często pytania o integrację z FCM, APNS, architekturę push.

## Kluczowe pojęcia
- **Notification Hub** – centralny punkt wysyłki powiadomień.
- **Registration** – rejestracja urządzenia (token push).
- **Tag** – grupowanie odbiorców.
- **Template** – szablony powiadomień.
- **PNS** – Push Notification Service (FCM, APNS, WNS).

## Scenariusze egzaminacyjne
- Wysyłka powiadomień do wielu platform.
- Integracja z FCM (Android), APNS (iOS).
- Ustawienie tagów i szablonów.

## Przykład użycia
- Rejestracja urządzenia przez SDK.
- Wysyłka powiadomienia przez portal lub REST API.

## Komendy
- Tworzenie Notification Hub:
  `az notification-hub create --resource-group rg --namespace-name myns --name myhub --location westeurope`

## Przykład kodu C# (.NET 8)
```csharp
// Przykład: Wysyłka powiadomienia push przez REST API
using System.Net.Http;
using System.Net.Http.Headers;
using System.Threading.Tasks;

public class NotificationHubSender
{
  public async Task SendPushAsync(string hubNamespace, string hubName, string sasToken, string payload)
  {
    using var client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("SharedAccessSignature", sasToken);
    client.DefaultRequestHeaders.Add("ServiceBusNotification-Format", "gcm"); // lub apns dla iOS
    var url = $"https://{hubNamespace}.servicebus.windows.net/{hubName}/messages/?api-version=2015-01";
    var response = await client.PostAsync(url, new StringContent(payload, System.Text.Encoding.UTF8, "application/json"));
    response.EnsureSuccessStatusCode();
  }
}
```

## Wskazówka egzaminacyjna
- Najczęstszy błąd: brak poprawnej konfiguracji PNS lub brak rejestracji urządzenia.
- Notification Hubs nie przechowuje historii powiadomień.
