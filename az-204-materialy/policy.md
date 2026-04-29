# Azure Policy
---

[Prev: Azure Durable Functions](durable-functions.md) | [Next: Azure Blueprints](blueprints.md)

**Definicja:**
- **Azure Policy** – usługa do wymuszania reguł i zgodności zasobów w subskrypcji.

**Znaczenie na egzaminie AZ-204:**
- Często pytania o kontrolę zgodności, audyt, blokowanie działań.

## Kluczowe pojęcia
- **Policy Definition** – opisuje regułę (np. dozwolone regiony).
- **Policy Assignment** – przypisanie reguły do zakresu (np. subskrypcja, grupa zasobów).
- **Initiative** – grupa reguł (policy set).
- **Effect** – akcja: audit, deny, append, deployIfNotExists.

## Scenariusze egzaminacyjne
- Blokowanie tworzenia zasobów poza regionem.
- Wymuszanie tagów.
- Audyt zasobów bez szyfrowania.

## Przykład użycia
- Tworzenie i przypisanie policy przez Azure CLI.

## Komendy
- Tworzenie policy:
  `az policy definition create --name allowed-locations --rules rules.json --params params.json --mode All`
- Przypisanie policy:
  `az policy assignment create --policy allowed-locations --scope /subscriptions/{subId}`

## Przykład kodu C# (.NET 8)
```csharp
// Brak SDK do zarządzania policy w runtime aplikacji. Policy działa na poziomie zarządzania zasobami.
```

## Wskazówka egzaminacyjna
- Policy nie zatrzymuje istniejących zasobów – działa na nowe i zmieniane.
- Najczęstszy błąd: mylenie Policy z RBAC.
