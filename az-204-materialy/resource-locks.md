# Resource Locks
---

[Prev: Azure Cost Management](cost-management.md) | [Next: Azure Advisor](advisor.md)

**Definicja:**
- **Resource Locks** – blokady uniemożliwiające przypadkowe usunięcie lub modyfikację zasobów.

**Znaczenie na egzaminie AZ-204:**
- Pytania o zabezpieczenie zasobów przed usunięciem.

## Kluczowe pojęcia
- **CanNotDelete (Delete Lock)** – blokuje usunięcie zasobu.
- **ReadOnly (Read Lock)** – blokuje modyfikacje i usunięcie.
- **Scope** – blokada na poziomie zasobu, grupy, subskrypcji.

## Scenariusze egzaminacyjne
- Ochrona kluczowych zasobów (np. Key Vault, Storage).

## Przykład użycia
- Tworzenie blokady przez CLI.

## Komendy
- Tworzenie blokady:
  `az lock create --name myLock --lock-type CanNotDelete --resource-group myRG --resource-name myVM --resource-type Microsoft.Compute/virtualMachines`

## Przykład kodu C# (.NET 8)
```csharp
// Brak SDK do zarządzania blokadami w runtime aplikacji. Operacje przez CLI/portal.
```

## Wskazówka egzaminacyjna
- Resource Lock ≠ RBAC (Lock = techniczna blokada, RBAC = uprawnienia).
- Najczęstszy błąd: mylenie blokad z uprawnieniami.
