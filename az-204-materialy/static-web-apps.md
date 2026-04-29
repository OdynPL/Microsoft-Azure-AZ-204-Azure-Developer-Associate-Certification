# Azure Static Web Apps
---

[Prev: Azure Logic Apps Standard vs Consumption](logic-apps-standard-vs-consumption.md) | [Next: Azure Notification Hubs](notification-hubs.md)

**Definicja:**
- Usługa do hostowania statycznych aplikacji webowych (SPA, JAMstack) z automatycznym CI/CD.

**Znaczenie na egzaminie AZ-204:**
- Często pytania o hosting SPA, autoryzację, integrację z GitHub Actions.

## Kluczowe pojęcia
- **Static Web App** – hostowanie plików statycznych (HTML, JS, CSS).
- **API (Functions)** – wbudowane Azure Functions jako backend.
- **Authentication** – wbudowana obsługa logowania (Azure AD, GitHub, Google).
- **Custom domains** – własne domeny, certyfikaty SSL.
- **CI/CD** – automatyczne wdrożenia z repozytorium.

## Scenariusze egzaminacyjne
- Hosting SPA (React, Angular, Vue).
- Konfiguracja autoryzacji i custom domains.
- Deployment przez GitHub Actions.

## Przykład użycia
- Publikacja aplikacji React z GitHub do Static Web Apps.
- Konfiguracja autoryzacji przez portal.

## Komendy
- Tworzenie Static Web App:
  `az staticwebapp create --name myapp --resource-group rg --source https://github.com/user/repo --location westeurope`

## Przykład kodu C# (.NET 8)
```csharp
// Przykład: API backend w Azure Static Web Apps (Function)
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Http;
using System.Net;

public class ApiFunction
{
  [Function("HelloApi")]
  public HttpResponseData Run([HttpTrigger(AuthorizationLevel.Anonymous, "get")] HttpRequestData req)
  {
    var response = req.CreateResponse(HttpStatusCode.OK);
    response.WriteString("Hello from Static Web Apps API!");
    return response;
  }
}
```

## Wskazówka egzaminacyjna
- Static Web Apps automatycznie integruje się z GitHub Actions.
- Najczęstszy błąd: brak pliku routes.json przy customowych ścieżkach lub brak autoryzacji.
