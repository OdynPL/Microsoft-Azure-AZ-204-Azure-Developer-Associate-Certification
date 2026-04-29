# Azure Cost Management
---

[Prev: Azure DevTest Labs](devtest-labs.md) | [Next: Resource Locks](resource-locks.md)

**Definicja:**
- **Azure Cost Management** – narzędzia do monitorowania, analizowania i optymalizacji kosztów w Azure.

**Znaczenie na egzaminie AZ-204:**
- Pytania o alerty kosztowe, raporty, budżety.

## Kluczowe pojęcia
- **Budgets** – limity wydatków, alerty.
- **Cost Analysis** – raporty i wykresy kosztów.
- **Advisor Recommendations** – sugestie optymalizacji.

## Scenariusze egzaminacyjne
- Ustawianie budżetu i alertów.
- Analiza kosztów subskrypcji.

## Przykład użycia
- Tworzenie budżetu przez portal lub REST API.

## Komendy
- Tworzenie budżetu:
  https://learn.microsoft.com/en-us/azure/cost-management-billing/costs/tutorial-acm-create-budgets

## Przykład kodu C# (.NET 8)
```csharp
// Brak SDK do zarządzania kosztami w runtime aplikacji. Operacje przez portal/REST API.
```

## Wskazówka egzaminacyjna
- Cost Management = monitoring i alerty, nie blokuje wydatków.
- Najczęstszy błąd: mylenie alertów z blokadą wydatków.
