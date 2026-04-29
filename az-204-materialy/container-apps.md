# Azure Container Apps
---

[Prev: Azure API for FHIR](api-for-fhir.md) | [Next: Azure Durable Functions](durable-functions.md)

**Definicja:**
- Usługa do uruchamiania kontenerów w modelu serverless, bez zarządzania klastrem.

**Znaczenie na egzaminie AZ-204:**
- Często pytania o różnice względem AKS/ACI, skalowanie, event-driven.

## Kluczowe pojęcia
- **Container App** – pojedyncza aplikacja kontenerowa.
- **Environment** – izolowane środowisko dla wielu aplikacji.
- **Ingress** – publiczny lub prywatny dostęp HTTP.
- **Scale** – automatyczne skalowanie na podstawie zdarzeń (KEDA).
- **Revision** – wersjonowanie wdrożeń.

## Scenariusze egzaminacyjne
- Wdrożenie kontenera przez portal, CLI, Bicep.
- Skalowanie na podstawie kolejek, HTTP, CPU.
- Różnice względem AKS i ACI.

## Przykład użycia
- Tworzenie Container App przez CLI.
- Konfiguracja autoskalowania przez KEDA.

## Komendy
- Tworzenie środowiska:
  `az containerapp env create --name myenv --resource-group rg --location westeurope`
- Tworzenie Container App:
  `az containerapp create --name myapp --resource-group rg --environment myenv --image mcr.microsoft.com/azuredocs/containerapps-helloworld:latest --target-port 80 --ingress external`

## Wskazówka egzaminacyjna
- Container Apps = serverless, nie zarządzasz klastrem.
- Najczęstszy błąd: brak ustawionego ingress lub złe limity skalowania.
