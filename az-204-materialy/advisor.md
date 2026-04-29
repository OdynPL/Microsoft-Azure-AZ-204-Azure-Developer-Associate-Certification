# Azure Advisor
---

[Prev: Resource Locks](resource-locks.md) | [Next: Azure Marketplace](marketplace.md)

**Definicja:**
- **Azure Advisor** – narzędzie do rekomendacji optymalizacji kosztów, wydajności, bezpieczeństwa i dostępności.

**Znaczenie na egzaminie AZ-204:**
- Pytania o analizę rekomendacji i wdrażanie poprawek.

## Kluczowe pojęcia

- **Cost** – rekomendacje oszczędności.
- **Security** – poprawa bezpieczeństwa.
- **Performance** – wydajność.
- **Operational Excellence** – zarządzanie i automatyzacja.

**Kluczowe pojęcia dodatkowe:**
- **REST API** – dostęp do rekomendacji Advisor przez API (management.azure.com).
- **Suppressions** – możliwość ukrycia wybranych rekomendacji.
- Analiza rekomendacji i wdrożenie zmian.

## Przykład użycia
- Przegląd rekomendacji przez portal lub CLI.

## Komendy
- Pobranie rekomendacji:
  `az advisor recommendation list --category Cost`

- Pobranie rekomendacji przez PowerShell:
  `Get-AzAdvisorRecommendation -Category Cost`

## Przykład kodu C# (.NET 8)
```csharp
// Przykład 1: Wywołanie REST API Advisor z poziomu C#
using System.Net.Http;
using System.Net.Http.Headers;
using System.Threading.Tasks;

public class AdvisorExample
{
  public async Task<string> GetAdvisorRecommendationsAsync(string subscriptionId, string bearerToken)
  {
    using var client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
    var url = $"https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.Advisor/recommendations?api-version=2020-01-01";
    var response = await client.GetAsync(url);
    response.EnsureSuccessStatusCode();
    return await response.Content.ReadAsStringAsync();
  }
}
```

```csharp
// Przykład 2: Obsługa rekomendacji Advisor przez CLI z poziomu C#
using System.Diagnostics;

public class AdvisorCliExample
{
  public void ListAdvisorRecommendations()
  {
    var process = new Process
    {
      StartInfo = new ProcessStartInfo
      {
        FileName = "az",
        Arguments = "advisor recommendation list --category Cost",
        RedirectStandardOutput = true,
        UseShellExecute = false,
        CreateNoWindow = true
      }
    };
    process.Start();
    string output = process.StandardOutput.ReadToEnd();
    process.WaitForExit();
    Console.WriteLine(output);
  }
}
```

## Wskazówka egzaminacyjna
- Advisor = rekomendacje, nie wymusza zmian.
- Najczęstszy błąd: mylenie Advisor z Policy lub Cost Management.
  - Advisor nie wymusza zmian – tylko rekomenduje.
  - Advisor nie blokuje wdrożeń (w przeciwieństwie do Policy).
  - REST API Advisor nie wymaga SDK, ale wymaga autoryzacji Bearer Token.
  - Częsty błąd: oczekiwanie automatycznego wdrożenia rekomendacji.
