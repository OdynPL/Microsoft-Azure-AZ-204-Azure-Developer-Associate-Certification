# Azure Marketplace
---

[Prev: Azure Advisor](advisor.md) | [Next: Azure .NET Aspire](dotnet-aspire.md)

**Definicja:**
- **Azure Marketplace** – katalog gotowych rozwiązań, usług i aplikacji do wdrożenia w Azure.

**Znaczenie na egzaminie AZ-204:**
- Pytania o wdrażanie aplikacji z Marketplace, licencjonowanie, integrację.

## Kluczowe pojęcia
- **Offer** – produkt dostępny w Marketplace.
- **Plan** – wariant produktu.
- **Private Offer** – niestandardowa oferta dla wybranych klientów.

## Scenariusze egzaminacyjne
- Wdrażanie VM z Marketplace.
- Zakup SaaS przez Marketplace.

## Przykład użycia
- Wdrażanie zasobu przez portal lub CLI.

## Komendy
- Wyszukiwanie ofert:
  `az vm image list --all --publisher Microsoft`

## Przykład kodu C# (.NET 8)
```csharp
// Brak SDK do wdrażania Marketplace w runtime aplikacji. Operacje przez portal/CLI.
```

## Wskazówka egzaminacyjna
- Marketplace = gotowe rozwiązania, nie własne szablony.
- Najczęstszy błąd: mylenie Marketplace z własnymi ARM/Bicep.
