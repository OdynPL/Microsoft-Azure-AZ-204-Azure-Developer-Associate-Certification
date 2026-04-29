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
// Brak SDK do zarządzania blueprintami w runtime aplikacji. Operacje tylko przez portal/REST.
```

## Wskazówka egzaminacyjna
- Blueprints = automatyzacja governance, compliance.
- Najczęstszy błąd: mylenie z ARM/Bicep lub Policy.
