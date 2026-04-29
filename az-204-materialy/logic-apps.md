

# Azure Logic Apps
---

[Prev: Key Vault](key-vault.md) | [Next: Managed Identity](managed-identity.md)

- Usługa do budowy workflow bez kodowania (**low-code/no-code**).
- Integracja z wieloma usługami przez **konektory** (Outlook, Teams, SQL, HTTP, Service Bus, Event Grid).
- Automatyzacja procesów biznesowych, integracja systemów, ETL.

## Znaczenie na AZ-204
- Pozwala szybko zautomatyzować procesy bez pisania kodu.
- Integruje się z usługami Azure, SaaS, on-premises.
- Umożliwia budowę rozgałęzionych workflow, obsługę błędów, retry.

## Kluczowe pojęcia
- **Workflow**: sekwencja wyzwalaczy i akcji.
- **Trigger**: wyzwalacz startujący workflow (np. HTTP, czas, zdarzenie).
- **Action**: pojedyncza operacja (np. wysłanie maila, zapis do bazy).
- **Connector**: gotowy moduł do integracji z usługą (ponad 400 konektorów).
- **Run History**: historia wykonania workflow.
- **Parameters**: parametryzacja workflow.
- **Managed Identity**: bezpieczny dostęp do innych usług.
- **Error Handling**: obsługa błędów, retry, warunki.

## Scenariusze egzaminacyjne
- Tworzenie workflow przez portal lub ARM/Bicep.
- Wyzwalanie przez HTTP, Event Grid, Service Bus.
- Integracja z Outlook, Teams, SQL, Functions.
- Obsługa błędów i retry policy.
- Użycie Managed Identity do dostępu do Key Vault, Storage.

## Przykład użycia
- Tworzenie workflow przez portal Azure.
- Dodanie wyzwalacza (np. HTTP request, timer).
- Dodanie akcji (np. wysłanie maila przez Outlook, zapis do SQL).
- Użycie warunków, pętli, obsługa błędów.

## Komendy
- Tworzenie Logic App:
	`az logic workflow create --resource-group rg --name mylogic --definition @workflow.json --location westeurope`
- Wyświetlenie historii uruchomień:
	`az logic workflow run list --resource-group rg --name mylogic`

## Wskazówka egzaminacyjna
- Logic Apps nie uruchamiają kodu C#, tylko workflow.
- Najczęstszy błąd: brak uprawnień do usługi docelowej (np. Key Vault).
- Retry i obsługa błędów są konfigurowalne dla każdej akcji.

## Przykład użycia

- Tworzenie workflow przez portal Azure.
- Dodanie wyzwalacza (np. HTTP request).
- Dodanie akcji (np. wysłanie maila przez Outlook).

- Brak kodu C#, konfiguracja graficzna.

---

