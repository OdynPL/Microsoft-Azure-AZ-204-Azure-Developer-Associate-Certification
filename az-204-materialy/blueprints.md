# Azure Blueprints
---

[Prev: Azure Policy](policy.md) | [Next: Azure Private Link](private-link.md)

**Definicja:**
- **Azure Blueprints** – narzędzie do wdrażania zestawu zasobów, policy, ról i szablonów ARM jako jeden pakiet.

**Znaczenie na egzaminie AZ-204:**
- Pytania o automatyzację wdrożeń zgodnych z polityką organizacji.

## Kluczowe pojęcia
- **Blueprint Definition** – opis blueprinta (co wdraża).
- **Artifact** – element blueprinta (np. policy, role, ARM template).
- **Assignment** – przypisanie blueprinta do subskrypcji.

## Scenariusze egzaminacyjne
- Wdrażanie środowisk zgodnych z compliance.
- Automatyzacja powtarzalnych wdrożeń.

## Przykład użycia
- Tworzenie blueprinta przez portal lub REST API.

## Komendy
- Tworzenie blueprinta (tylko przez portal lub REST API, CLI nie obsługuje):
  https://learn.microsoft.com/en-us/azure/governance/blueprints/create-blueprint-portal

## Przykład kodu C# (.NET 8)
```csharp
// Pobranie listy przypisanych blueprintów przez REST API
using System.Net.Http;
using System.Net.Http.Headers;
using System.Threading.Tasks;

public class BlueprintExample
{
  public async Task<string> ListBlueprintAssignmentsAsync(string subscriptionId, string bearerToken)
  {
    using var client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
    var url = $"https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.Blueprint/blueprintAssignments?api-version=2018-11-01-preview";
    var response = await client.GetAsync(url);
    response.EnsureSuccessStatusCode();
    return await response.Content.ReadAsStringAsync();
  }
}
```

## Wskazówka egzaminacyjna
- Blueprints = automatyzacja governance, compliance.
- Najczęstszy błąd: mylenie z ARM/Bicep lub Policy.
