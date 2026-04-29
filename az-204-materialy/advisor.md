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

## Scenariusze egzaminacyjne
- Analiza rekomendacji i wdrożenie zmian.

## Przykład użycia
- Przegląd rekomendacji przez portal lub CLI.

## Komendy
- Pobranie rekomendacji:
  `az advisor recommendation list --category Cost`

## Przykład kodu C# (.NET 8)
```csharp
// Brak SDK do pobierania rekomendacji w runtime aplikacji. Operacje przez CLI/portal.
```

## Wskazówka egzaminacyjna
- Advisor = rekomendacje, nie wymusza zmian.
- Najczęstszy błąd: mylenie Advisor z Policy lub Cost Management.
