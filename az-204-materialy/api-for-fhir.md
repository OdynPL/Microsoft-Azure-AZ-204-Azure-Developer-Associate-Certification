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

## Scenariusze egzaminacyjne
- Wdrożenie API for FHIR.
- Konfiguracja RBAC i audytu.
- Integracja z aplikacją medyczną.

## Przykład użycia
- Dodanie pacjenta przez REST API.
- Pobranie danych przez SDK.

## Komendy
- Tworzenie API for FHIR:
  `az healthcareapis service create --resource-group rg --name myfhir --kind fhir --location westeurope`

## Wskazówka egzaminacyjna
- Najczęstszy błąd: brak uprawnień RBAC lub niepoprawna autoryzacja SMART on FHIR.
- API for FHIR wymaga zgodności z przepisami (RODO, HIPAA).
