# Azure Container Apps
---

[Prev: Azure API for FHIR](api-for-fhir.md) | [Next: Azure Durable Functions](durable-functions.md)

**Definicja:**
- Usługa do uruchamiania kontenerów w modelu serverless, bez zarządzania klastrem.

**Znaczenie na egzaminie AZ-204:**
- Często pytania o różnice względem AKS/ACI, skalowanie, event-driven.

## Kluczowe pojęcia
- **Container App** – pojedyncza aplikacja kontenerowa.
- **Environment** – izolowane środowisko dla wielu aplikacji.
- **Ingress** – publiczny lub prywatny dostęp HTTP.
- **Scale** – automatyczne skalowanie na podstawie zdarzeń (KEDA).
- **Revision** – wersjonowanie wdrożeń.

## Scenariusze egzaminacyjne
- Wdrożenie kontenera przez portal, CLI, Bicep.
- Skalowanie na podstawie kolejek, HTTP, CPU.
- Różnice względem AKS i ACI.

## Przykład użycia
- Tworzenie Container App przez CLI.
- Konfiguracja autoskalowania przez KEDA.

## Komendy
- Tworzenie środowiska:
  `az containerapp env create --name myenv --resource-group rg --location westeurope`
- Tworzenie Container App:
  `az containerapp create --name myapp --resource-group rg --environment myenv --image mcr.microsoft.com/azuredocs/containerapps-helloworld:latest --target-port 80 --ingress external`

## Przykład kodu C# (.NET 8)
```csharp
// Przykład: Pobranie listy Container Apps przez REST API
using System.Net.Http;
using System.Net.Http.Headers;
using System.Threading.Tasks;

public class ContainerAppsExample
{
  public async Task<string> ListContainerAppsAsync(string subscriptionId, string resourceGroup, string bearerToken)
  {
    using var client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
    var url = $"https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.App/containerApps?api-version=2023-05-01";
    var response = await client.GetAsync(url);
    response.EnsureSuccessStatusCode();
    return await response.Content.ReadAsStringAsync();
  }
}
```

## Wskazówka egzaminacyjna
- Container Apps = serverless, nie zarządzasz klastrem.
- Najczęstszy błąd: brak ustawionego ingress lub złe limity skalowania.
