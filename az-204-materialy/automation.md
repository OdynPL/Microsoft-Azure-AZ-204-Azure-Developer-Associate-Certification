# Azure Automation
---

[Prev: Azure Files](files.md) | [Next: Azure DevTest Labs](devtest-labs.md)

**Definicja:**
- **Azure Automation** – usługa do automatyzacji zadań administracyjnych (runbooki, update management).

**Znaczenie na egzaminie AZ-204:**
- Pytania o runbooki, harmonogramy, integrację z PowerShell.

## Kluczowe pojęcia
- **Runbook** – skrypt automatyzujący zadania (PowerShell, Python).
- **Update Management** – zarządzanie aktualizacjami VM.
- **Webhook** – wyzwalanie runbooka przez HTTP.

## Scenariusze egzaminacyjne
- Automatyczne czyszczenie zasobów.
- Harmonogram backupów.

## Przykład użycia
- Tworzenie runbooka i uruchamianie przez CLI.

## Komendy
- Tworzenie konta Automation:
  `az automation account create --name myaccount --resource-group myRG --location westeurope`
- Tworzenie runbooka:
  `az automation runbook create --automation-account-name myaccount --resource-group myRG --name myrunbook --type PowerShell`

## Przykład kodu C# (.NET 8)
```csharp
// Brak SDK do uruchamiania runbooków z poziomu aplikacji. Integracja przez webhook lub REST API.
```

## Wskazówka egzaminacyjna
- Automation ≠ Logic Apps (Automation = admin, Logic Apps = integracja).
- Najczęstszy błąd: mylenie Automation z Functions/Logic Apps.
