# Azure Logic Apps Standard vs Consumption
---

[Prev: Azure API Apps](api-apps.md) | [Next: Azure Static Web Apps](static-web-apps.md)

**Definicja:**
- Dwa modele uruchamiania Logic Apps: **Standard** (kontener, single-tenant) i **Consumption** (multi-tenant, pay-per-execution).

**Znaczenie na egzaminie AZ-204:**
- Często pytania o limity, różnice, wybór modelu.

## Kluczowe pojęcia
- **Standard** – hostowane na App Service, wsparcie dla kodu, VNet, deployment slots, wyższe limity.
- **Consumption** – rozliczanie za wywołania, szybki start, ograniczone możliwości integracji.
- **Stateful/Stateless** – Standard obsługuje oba tryby.
- **Custom Connectors** – pełne wsparcie w Standard.

## Scenariusze egzaminacyjne
- Wybór modelu do integracji z VNet.
- Ograniczenia liczby akcji, czasów trwania, retry.
- Deployment przez ARM/Bicep.

## Przykład użycia
- Tworzenie Logic App Standard przez portal lub ARM.
- Porównanie kosztów i limitów.

## Komendy
- Tworzenie Logic App Standard:
  `az logic workflow create --resource-group rg --name mylogic --definition @workflow.json --location westeurope --sku Standard`

## Przykład kodu C# (.NET 8)
```csharp
// Przykład: Wywołanie Logic App Standard przez HTTP trigger
using System.Net.Http;
using System.Threading.Tasks;

public class LogicAppStandardCaller
{
  public async Task<string> CallLogicAppStandardAsync(string logicAppUrl, string payload)
  {
    using var client = new HttpClient();
    var response = await client.PostAsync(logicAppUrl, new StringContent(payload, System.Text.Encoding.UTF8, "application/json"));
    response.EnsureSuccessStatusCode();
    return await response.Content.ReadAsStringAsync();
  }
}
```

## Wskazówka egzaminacyjna
- Standard = wyższe limity, integracja z VNet, deployment slots.
- Najczęstszy błąd: wybór Consumption gdy potrzebny jest dostęp do VNet lub deployment slots.
