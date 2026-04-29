# Azure API for FHIR
---

[Prev: Azure Cognitive Services](cognitive-services.md) | [Next: Azure Container Apps](container-apps.md)

**Definicja:**
- Usługa API do przechowywania i wymiany danych medycznych zgodnie ze standardem FHIR.

**Znaczenie na egzaminie AZ-204:**
- Często pytania o bezpieczeństwo, autoryzację, compliance.

## Kluczowe pojęcia
- **FHIR** – standard wymiany danych medycznych.
- **SMART on FHIR** – autoryzacja aplikacji medycznych.
- **RBAC** – kontrola dostępu do danych.
- **Audit Logging** – rejestrowanie operacji na danych.

**Kluczowe pojęcia dodatkowe:**
- **Access Control** – zarządzanie dostępem do zasobów FHIR przez Azure AD.
- **Export/Import** – masowa migracja danych FHIR przez API.

## Scenariusze egzaminacyjne
- Wdrożenie API for FHIR.
- Konfiguracja RBAC i audytu.
- Integracja z aplikacją medyczną.

## Przykład użycia
- Dodanie pacjenta przez REST API.
- Pobranie danych przez SDK.

## Przykład kodu C# (.NET 8)
```csharp
// Przykład 1: Dodanie pacjenta przez REST API FHIR
using System.Net.Http;
using System.Net.Http.Headers;
using System.Text;
using System.Threading.Tasks;

public class FhirExample
{
  public async Task<string> AddPatientAsync(string fhirUrl, string bearerToken, string patientJson)
  {
    using var client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
    var content = new StringContent(patientJson, Encoding.UTF8, "application/fhir+json");
    var response = await client.PostAsync($"{fhirUrl}/Patient", content);
    response.EnsureSuccessStatusCode();
    return await response.Content.ReadAsStringAsync();
  }
}
```

```csharp
// Przykład 2: Pobranie danych pacjenta z autoryzacją
using System.Net.Http;
using System.Net.Http.Headers;
using System.Threading.Tasks;

public class FhirGetExample
{
  public async Task<string> GetPatientAsync(string fhirUrl, string bearerToken, string patientId)
  {
    using var client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
    var response = await client.GetAsync($"{fhirUrl}/Patient/{patientId}");
    response.EnsureSuccessStatusCode();
    return await response.Content.ReadAsStringAsync();
  }
}
```

## Komendy
- Tworzenie API for FHIR:
  `az healthcareapis service create --resource-group rg --name myfhir --kind fhir --location westeurope`

- Pobranie danych przez PowerShell:
  `Invoke-RestMethod -Uri "https://myfhir.azurehealthcareapis.com/Patient" -Headers @{Authorization = "Bearer $token"}`

## Wskazówka egzaminacyjna
- Najczęstszy błąd: brak uprawnień RBAC lub niepoprawna autoryzacja SMART on FHIR.
- API for FHIR wymaga zgodności z przepisami (RODO, HIPAA).
  - Częsty błąd: brak Bearer Token lub niepoprawny audience w tokenie.
  - RBAC wymaga przypisania ról użytkownikom w Azure AD.
